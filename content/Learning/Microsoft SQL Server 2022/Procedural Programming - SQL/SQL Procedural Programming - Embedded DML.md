---
id: SQL Procedural Programming - Embedded DML
aliases: SQL Procedural Programming with Database Operations
tags:
  - uni
  - db
  - SQL
module: ICDT 1202Y
author: S.Sunhaloo
date: 2025-01-29
status: Completed
---

> [!NOTE]
> This file is related to most things that we learned from [[Microsoft SQL Server 2022 Data View#Microsoft SQL Server 2022 SQL Commands Folder | SQL Data Manipulation Language] Lectures / Notes. This is because the reason we have _Procedural Programming_ is to run these **DML Commands** using _Stored Procedures_.
>
> > Head over to '[[SQL Procedural Programming - Introduction#Benefits of SQL Stored Procedures | SQL Procedural Programming - Introduction]' to learn more about their benefits!
>
> I initially thought taking these notes was unnecessary, but as the lecturer pointed out, "_the commands are slightly different from what we simply write_", making them essential.

## List of Contents

- [[#INSERT Command in Stored Procedures | INSERT Command]]
  - [[#Example Simple Stored Procedures to Insert Data | Example Template]]
    - [[#Example Actual Usage In SQL Server | Actual Example]]
    - [[#Execution of Stored Procedure - INSERT Command]]
- [[#DELETE Command in Stored Procedures | DELETE Command]]
  - [[#Example Simple Stored Procedures to Insert Data | Example Template]]
  - [[#Example 1 Delete Command in Stored Pocedure | Example 1]]
    - [[#Execution of Stored Procedure - DELETE Command]]
  - [[#Example 2 Delete Command with System Variable ROWCOUNT | Example 2]]
    - [[#Execution of Stored Procedure - DELETE Command with ROWCOUNT]]
- [[#SELECT Command in Stored Procedures | SELECT Command]]
  - [[#Example 1 Running SELECT Command Directly | Example 1: Running Command Directly]]
  - [[#Example 2 Running SELECT Command with Variables | Example 2: Running Command with Variables]]
  - [[#Example 3 Use Multiple Variables IN the SELECT Command | Example 3: Output Multiple Values ( with Variables )]]
- [[#Lecture Exercises]]
  - [[#Lecture Exercise 1]]
  - [[#Lecture Exercise 2]]

---

> [!WARNING] Critical Mistake!!!
> When I wrote most of the I did **not** add the [[SQL Procedural Programming - Exception Handling#Raising the Exception | THROW] statement!
>
> This is because I don't have anything to _raise_... Nevertheless, if some type of "_internal_" error occurs; it should be handled by the `BEGIN CATCH ... END CATCH` part!

> [!INFO] General Points
>
> - They can execute **transactions** on the database application $\Rightarrow$ Preserving transaction **[[Database Transactions - ACID#Atomicity | atomicity]**
> - They are a _server-sided_; they ensure **consistency** for such _transactions_
> - A Stored Procedure may only contain **one** SQL Statement
>   - ( A Bad ) Example: A single `PRINT 'Hello Motherfuckers'`

# INSERT Command in Stored Procedures

Well, from our notes from the file '[[SQL Commands - Data Manipulation Language - INSERT]', we know that the general _template_ for inserting values into a table are:

```SQL
INSERT INTO table_name ( field1, field2, field3, ... ) VALUES ( value1, value2, value3, ... );
```

> Well, its basically the same things but instead of passing the **values** directly... Pass the **parameters** into the `VALUES` "_function_"!

## Example: Simple Stored Procedures to Insert Data

> I will be writing the "_template_" first

```SQL
CREATE PROCEDURE sp_insert_values
	-- our parameters
	@param_1 DATATYPE,
	@param_2 DATATYPE,
	@param_3 DATATYPE,
	...
AS
BEGIN
	-- exception handling
	BEGIN TRY
		-- insert command to... well, insert values!
		-- NOTE: notice how we don't use `@field_1`!!!
		INSERT INTO table_name ( field_1, field_2, field_3, ... ) VALUES (  @param_1, @param_2, @param_3, ... );
	END TRY

	-- catch the exception
	BEGIN CATCH
		-- adding just a simple message
		PRINT 'Error: ' + ERROR_MESSAGE();
	END CATCH
END
```

### Example: Actual Usage In SQL Server

> [!INFO] Prerequisites
> Well, I have created a simple 'Test_DB' **database** whereby I have created a 'test' **table** and I am going to insert 1 value into the table.
>
> > For the fields / column of the table 'test'. Please refer to the `INSERT INTO test ( <here> )`!

#### "Prerequisites Commands"

```SQL
-- on master; create the database
CREATE DATABASE Test_DB

-- switch to the 'Test_DB' database
-- create the 'test' table
CREATE TABLE test (
	-- columns / fields
    test_id CHAR(4),
    product_name VARCHAR(20),
    condition VARCHAR(15),
    price FLOAT,

    -- constraints

    -- primary key
    CONSTRAINT PK_tbltest PRIMARY KEY ( test_id ),
    -- primary key constraint
	CONSTRAINT PK_test_id_format CHECK ( test_id LIKE 'T%' ),
	-- check if whether condition of product falls in these categories below
	CONSTRAINT chk_condition CHECK ( condition IN ( 'New', 'Good', 'Bad' ) )
);

-- check if we have any data in the 'test' table
SELECT * FROM test;
```

Hence, we **should** get _nothing_!

```console
test_id    product_name    condition    price
```

#### Create Procedure to Insert Data

```SQL
CREATE PROCEDURE sp_insert_values
	-- our parameters
	@test_id CHAR(4),
	@product_name VARCHAR(20),
	@condition VARCHAR(15),
	@product_price FLOAT
AS
BEGIN
	-- exception handling
	BEGIN TRY
		-- insert the values into table by passing the parameters
		INSERT INTO test ( test_id, product_name, condition, price ) VALUES (  @test_id, @product_name, @condition, @product_price );

		-- output appropriate message
		PRINT 'Insertion of Data has been Successful!'
	END TRY

	-- catch the exception
	BEGIN CATCH
		-- adding just a simple message
		PRINT 'Error: ' + ERROR_MESSAGE();
		PRINT 'At Line Number : ' + ERROR_LINE();
	END CATCH
END
```

##### Execution of Stored Procedure - INSERT Command

###### First Condition: No Fault

```SQL
-- no faults
EXEC sp_insert_values @test_id = 'T001', @product_name = 'Pilot G2', @condition = 'New', @product_price = 45.95;
```

Therefore, in our table we are going to get:

```console
test_id    product_name    condition    price
T001       Pilot G2        New          45.95
```

###### Second Condition: Error with Data

```SQL
-- raising primary key constraint error
EXEC sp_insert_values @test_id = 'S001', @product_name = 'Check Primary Key', @condition = 'Bad', @product_price = 00.00;
```

This is what I get $\downarrow$:

> Changed the format of the output message for improved readability on paper ( _paper does not have horizontal scrollbar_ )

```console
(0 rows affected)
Error: The INSERT statement conflicted with
the CHECK constraint "PK_test_id_format".
The conflict occurred in
database "Test_DB", table "dbo.test", column 'test_id'.
Msg 245, Level 16, State 1,
Procedure sp_insert_values,
Line 22 [Batch Start Line 56]
Conversion failed when converting
the varchar value
'At Line Number : ' to data type int.
```

# DELETE Command in Stored Procedures

Similar to our `INSERT` command, we are going to now try to use the `DELETE` command in the Stored Procedure.

> BTW, if you need the notes for `DELETE` $\Rightarrow$ Please visit the file / note '[[SQL Commands - Data Manipulation Language - DELETE]'

Again, here is our _template_ for using the `DELETE` command by itself $\downarrow$:

```SQL
DELETE table_name WHERE condition;
```

## Example: Simple Stored Procedures to Insert Data

> Here is a _general template_!

```SQL
CREATE PROCEDURE sp_delete_value
	-- our parameter
	@param_1 DATATYPE
AS
BEGIN
	-- exception handling
	BEGIN TRY
		-- run the `DELETE` command
		DELETE table_name WHERE field_1 = @param_1;

		--output appropriate message
		PRINT 'Record was Deleted Successfully'
	END TRY

	-- catch the exception
	BEGIN CATCH
		-- adding just a simple message
		PRINT 'Error: ' + ERROR_MESSAGE();
	END CATCH
END
```

### Example 1: Delete Command in Stored Pocedure

> [!INFO]
> I am going to delete the value that we entered in the 'test' **table** which is found in the 'Test_DB' **database**.

#### Creation of Stored Procedure

```SQL
CREATE PROCEDURE sp_delete_value_from_test
	-- our parameter
	@test_id CHAR(4)
AS
BEGIN
	-- exception handling
	BEGIN TRY
		-- run the `DELETE` command
		DELETE test WHERE test_id = @test_id;

		--output appropriate message
		PRINT 'Record was Deleted Successfully';
	END TRY

	-- catch the exception
	BEGIN CATCH
		-- NOTE: use `SELECT` to get message in
		-- output tab as a table
		SELECT 'Error: ' + ERROR_MESSAGE() As 'Error Message';
	END CATCH
END
```

##### Execution of Stored Procedure - DELETE Command

###### Deleting Record Found in Table

Before, we delete; let's confirm that the record is present:

```SQL
SELECT * FROM test;
```

We should only have 1 record in the table 'test' $\downarrow$:

```console
test_id    product_name    condition    price
T001       Pilot G2        New          45.95
```

---

```SQL
-- delete the only record found in the test table
EXEC sp_delete_value_from_test @test_id = 'T001';
```

```console
(1 row affected)
Record was Deleted Successfully
```

We now, should have **nothing** in the table 'test'. Running the same `SELECT * FROM test;` $\downarrow$

```console
test_id    product_name    condition    price
```

###### Deleting Record NOT Found in Table

```SQL
EXEC sp_delete_value_from_test @test_id = 'T001';
```

```console
(0 rows affected)
Record was Deleted Successfully
```

> [!WARNING]
> Well, as you know; the `DELETE` command will not give use any **errors** even if the record you are trying to delete does **not** exists.
>
> Hence, we are going to create another Stored Procedure that will make the use of the system variable `@@ROWCOUNT` so that we can have proper _errors_.

### Example 2: Delete Command with System Variable ROWCOUNT

> [!INFO] Before We Start, "_What is the `ROWCOUNT` System Variable_?"
> Well, a System Variable in SQL Server is a **variable** that cannot be _declared_ or _assigned_.
> We can ( _from what I am seeing and understanding_ ) only make comparison with it similar to something like a function like `string.isdigit()` from Python.
>
> The purpose of the `@@ROWCOUNT` system variable ( _system variables should be preceded with `@@` characters_ ) is that is stores the number of rows which have been affected by the last **executed statement**

#### Creation of Delete Stored Procedure with ROWCOUNT System Variable

```SQL
CREATE PROCEDURE sp_delete_value_from_test
	-- our parameter
	@test_id CHAR(4)
AS
BEGIN
	-- exception handling
	BEGIN TRY
		-- run the `DELETE` command
		DELETE test WHERE test_id = @test_id;

		-- check if the "a" number of rows have been affected
		IF @@ROWCOUNT = 0
		BEGIN
			-- meaning that the record was not found
			PRINT 'Record You are Trying to Delete Has NOT Been Found!!!'
		END
		ELSE
		BEGIN
			-- if the at record has been found
			--output appropriate message
			PRINT 'Record was Deleted Successfully';
		END
	END TRY

	-- catch the exception
	BEGIN CATCH
		-- NOTE: use `SELECT` to get message in
		-- output tab as a table
		SELECT 'Error: ' + ERROR_MESSAGE() As 'Error Message';
	END CATCH
END
```

> [!TIP]
> If you have already pasted the first iteration of the _Stored Procedure_ with the `DELETE` command. You can then copy the above $\uparrow$ code from and then change the `CREATE` command to the `ALTER` command so that you **don't** need to `DROP` the Stored Procedure!

##### Execution of Stored Procedure - DELETE Command with ROWCOUNT

> Running the **same** command from above $\uparrow$:

```SQL
-- execute the same command to delete the same record
EXEC sp_delete_value_from_test @test_id = 'T001';
```

We now should get the a proper message!

```console
(0 rows affected)
Record You are Trying to Delete Has NOT Been Found!!!
```

> [!TIP]
> The System Variable `@@ROWCOUNT` can also be used with the `UPDATE` command.
>
> > I you want an example of how this is done ( _which is basically the same_ ); you can check out [[#Lecture Exercise 1]]

# SELECT Command in Stored Procedures

> Does it need an _introduction_? Like actually, does it?
> In addition, I don't think that I will be adding a _template_ for this one.

## Example 1: Running SELECT Command Directly

> [!INFO]
> These tables and fields that I am going to be selecting comes from '[[Database Systems - Labsheet 2 ( L1S2 )]'.

```SQL
-- create procedure that will display all values from table 'lecturer'
CREATE PROCEDURE sp_display_lecturer
    -- as we are going to be displaying everything
    -- we are not going to pass any parameters
AS
BEGIN
    -- exception handling
    -- not really need; but if you delete the 'lecturer' table...
    BEGIN TRY
		-- use the select command to display everything
        SELECT 'Lecturer ID; ' = lid, 'Lecturer Name: ' = lname, 'Details: ' = title + ' --> ' + department + ' Department.' FROM lecturer;
    END TRY

    BEGIN CATCH
        -- catch the exception and handle the error
        PRINT 'Error: ' + ERROR_MESSAGE();
    END CATCH
END
```

In our case, we should get the result of $\downarrow$:

```console
Lecturer ID; 	Lecturer Name: 	Details:
L1	Ricardo	Lecturer --> ICT Department.
L2	Paula	Assoc Prof --> ICT Department.
L3	Emma	Assoc Prof --> SIS Department.
L4	Jeremy	Senior Lecturer --> SIS Department.
L5	Sabrina	Senior Lecturer --> Science Department.
L6	Gordon	Lecturer --> Mech Department.
```

> [!NOTE]
> Given that we use the `SELECT` command. Our output will be in the 'Results' tab!

## Example 2: Running SELECT Command with Variables

Here, instead of running the "_raw_" `SELECT` command directly, we are going to place _said_ command in a **variable**.

```SQL
-- create procedure that will display names from table 'lecturer'
CREATE PROCEDURE sp_display_lecturer_names
    -- our parameter
    @id CHAR(2)
AS
BEGIN
    -- exception handling
    -- not really need; but if you delete the 'lecturer' table...
    BEGIN TRY
        -- declaration of variable
        DECLARE @lecturer_name VARCHAR(40);

        -- initialise / set the variable
        SET @lecturer_name = ( SELECT lname FROM lecturer WHERE lid = @id );

        -- output the result to the user
        PRINT 'Name of Lecturer: ' + @lecturer_name;
    END TRY

    BEGIN CATCH
        -- catch the exception and handle the error
        PRINT 'Error: ' + ERROR_MESSAGE();
    END CATCH
END
```

### Execution of Stored Procedure

```SQL
EXEC sp_display_lecturer_names @id = 'L1';
EXEC sp_display_lecturer_names @id = 'L2';
EXEC sp_display_lecturer_names @id = 'L3';
```

This is was I will get based on the parameter that I pass $\downarrow$:

```console
Name of Lecturer: Ricardo
Name of Lecturer: Paula
Name of Lecturer: Emma
```

> This is actually very nice!

## Example 3: Use Multiple Variables IN the SELECT Command

This is _similar_ to the [[#Example 1 Running SELECT Command Directly | first example]; but now, instead of passing directly to a string. We are going to pass the **values** into the _variables_.

```SQL
-- create procedure that will display details of lecturer from table 'lecturer'
CREATE PROCEDURE sp_display_lecturer_details
    -- our parameter
    @id CHAR(2)
AS
BEGIN
    -- exception handling
    -- not really need; but if you delete the 'lecturer' table...
    BEGIN TRY
        -- declaration of variables
        DECLARE @lecturer_name VARCHAR(30);
        DECLARE @lecturer_title VARCHAR(30);
        DECLARE @lecturer_dept VARCHAR(30);

        -- select the appropriate details
        SELECT @lecturer_name = lname, @lecturer_title = title, @lecturer_dept = department
        FROM lecturer WHERE lid = @id;

        -- check if rows has been found
		IF @@ROWCOUNT = 0
        BEGIN
            -- meaning no records with `lid = @id` has been found
            PRINT 'NO Records Has Been Found With ID: ' + @id;
        END
        ELSE
        BEGIN
            -- if record is found ==> output the details of lecturer
            SELECT 'Name: ' = @lecturer_name, 'Title: ' = @lecturer_title, 'Department: ' = @lecturer_dept;
        END
    END TRY

    BEGIN CATCH
        -- catch the exception and handle the error
        PRINT 'Error: ' + ERROR_MESSAGE();
    END CATCH
END
```

### Execution of Stored Procedure

```SQL
EXEC sp_display_lecturer_details @id = 'L1';
EXEC sp_display_lecturer_details @id = 'L2';
EXEC sp_display_lecturer_details @id = 'L3';
```

> I will be adding all the output in the same code block below $\downarrow$:

```console
Name: 	Title: 	Department:
Ricardo	Lecturer	ICT

Name: 	Title: 	Department:
Paula	Assoc Prof	ICT

Name: 	Title: 	Department:
Emma	Assoc Prof	SIS
```

---

# Lecture Exercises

> [!INFO]
> I am also writing / doing the Lecture Exercises here because it has things like using `UPDATE` command.
> Hence, it could be used as further example.
>
> In addition, the exercises are found in the Lecture Notes in the PDF itself $\Rightarrow$ '[[Database Systems - Error Handling + Embedded DML.pdf]'

> [!WARNING]
> This is also part of the of the [[shitter] as the commands to create the database, tables and values are written there.

## Lecture Exercise 1

```SQL
-- create the procedure sp_upd_del_lec
CREATE PROCEDURE sp_upd_del_lec
    -- our parameters
    @id CHAR(2),
    @new_title VARCHAR(30),
    @new_dept VARCHAR(30)
AS
BEGIN
    -- exception handling
    BEGIN TRY

        -- update part of the code

        -- our update command that will update the title and department of the lecturer ( given an id )
        UPDATE lecturer SET
            -- get the new value for title from the parameter
            title = @new_title,
            -- get the new value for department from the parameter
            department = @new_dept
        -- where to change those values / data
        WHERE lid = @id;

        -- check whether the record has been update
        IF @@ROWCOUNT = 0
        BEGIN
            -- meaning that the record could not be updated
            PRINT 'Record Could NOT Be Updated Where ID is ' + CAST(@id AS VARCHAR(30)) + ' !';
        END
        ELSE
        BEGIN
            -- meaing that the record was updated ==> output appropriate message
            PRINT 'Updated Title and Department Where ID is: ' + CAST(@id AS VARCHAR(30));
        END

        -- delete part of the code

        -- NOTE: we cannot simply delete the required lecturer from the 'lecturer' table
        -- this is because 'lecturer' table is "connected" with 'module' table and itself is "connected" with 'registers'
        -- therefore, we need to delete from 'registers' then 'module' and last but not least 'lecturer'

        -- delete records from 'registers' table
        DELETE registers
        -- find the 'moduleid'
        WHERE moduleid IN (
            -- find the 'lecturerid'
            SELECT mid FROM module
            WHERE lecturerid IN (
                SELECT lid FROM lecturer
                -- find the lecturer whereby his / her department
                -- is our parameters `@new_dept`
                WHERE department = @new_dept
            )
        );

        -- delete records from 'module' table
        DELETE module
        -- find the 'lecturerid'
        WHERE lecturerid IN (
            SELECT lid FROM lecturer
            -- find the lecturer whereby his / her department
            -- is our parameters `@new_dept`
            WHERE department = @new_dept
        );

        -- start deleting records from the main / parent table 'lecturer'
        DELETE lecturer
        -- ==> don't delete the newly added record but delete the others
        WHERE lid != @id AND department = @new_dept;

        -- check whether the delete command was succesfully run

        -- declaration of variable `records_deleted_count`
        DECLARE @records_deleted_count INT = @@ROWCOUNT;

        -- start the condition
        IF @records_deleted_count = 0
        BEGIN
            -- meaning that no records has been changed
            PRINT 'NO Records Has Been Deleted!!!';
        END
        ELSE
        BEGIN
            -- deletion of records was successful
            -- output appropriate message
            PRINT CAST(@records_deleted_count AS VARCHAR(30)) + ' Unwanted Records Deleted Where Department Was: ' +  CAST(@new_dept AS VARCHAR(30));
        END
    END TRY

    BEGIN CATCH
        -- catch and handle the error
        PRINT 'Error: ' + ERROR_MESSAGE();

        -- NOTE: need to cast Error Line as its of INTEGER datatype
        PRINT 'Occurred At Line: ' + CAST(ERROR_LINE() AS VARCHAR(10));
    END CATCH
END
```

### Running the Stored Procedure

#### Tables, Tables, Tables

But first, let's check the values that are currently inside the table 'lecturer', 'module' and 'registers'.

```SQL
-- run the commands below to output the values from each table
SELECT * FROM lecturer;
SELECT * FROM module;
SELECT * FROM registers;
```

> I will be placing everything in the single code block below $\downarrow$:

```console
lid lname	title	department
L1	Ricardo	Lecturer	ICT
L2	Paula	Assoc Prof	ICT
L3	Emma	Assoc Prof	SIS
L4	Jeremy	Senior Lecturer	SIS
L5	Sabrina	Senior Lecturer	Science
L6	Gordon	Lecturer	Mech


mid	mname	level	credits	lecturerid
M1	Database	1	3	L3
M2	Maths	1	3	L5
M3	Programming	1	3	L1
M4	Biology	2	5	L5
M5	Web	2	5	L2


studentid	moduleid	reg_date	grade
S01	M1	2019-01-12	A
S01	M2	2019-01-12	A
S01	M5	2019-01-13	B
S03	M1	2020-01-15	B
S03	M5	2020-01-14	A
S04	M2	2019-01-11	C
S04	M4	2019-01-10	B
```

#### Execution of Command

In this case, I want to give the lecturer with 'lid' `L1`, i.e, `Ricardo` a new title of `Senior Lectuerer` and a new department of `Science`.
Hence, this means that the lecturer which currently have the department of `Science` will be **gone**.

> - `L5` will be gone from 'lecturer'
> - `M2`, `M3` and `M4` will be gone from 'module'
> - `M2` and `M4` will be gone from 'registers'

> [!NOTE] Why will `M3` be gone from 'module'
> My reasoning is that because its _attached_ to the lecturer `Ricardo` and **before** we execute the Stored Procedure. He **was** in the department of `ICT` where he was teaching _programming_.
> Now given that we change the department of `Ricardo` $\Rightarrow$ There is currently no one to teach programming.

```SQL
-- give lecturer with `L1` a new title and department
EXEC sp_upd_del_lec @id = 'L1', @new_title = 'Senior Lecturer', @new_dept = 'Science';
```

> Results for executing the above Stored Procedure

```console
(1 row affected)
Updated Title and Department Where ID is: L1

(3 rows affected)

(3 rows affected)

(1 row affected)
1 Unwanted Records Deleted Where Department Was: Science
```

Therefore running the above $\uparrow$ `SELECT` commands again will give us $\downarrow$:

```console
lid	lname	title	department
L1	Ricardo	Senior Lecturer	Science
L2	Paula	Assoc Prof	ICT
L3	Emma	Assoc Prof	SIS
L4	Jeremy	Senior Lecturer	SIS
L6	Gordon	Lecturer	Mech


mid	mname	level	credits	lecturerid
M1	Database	1	3	L3
M5	Web	2	5	L2


studentid	moduleid	reg_date	grade
S01	M1	2019-01-12	A
S01	M5	2019-01-13	B
S03	M1	2020-01-15	B
S03	M5	2020-01-14	A
```

## Lecture Exercise 2

```SQL
-- procedure that will update the number of credits
CREATE PROCEDURE sp_module
    -- our parameter
    @module_id CHAR(2)
AS
BEGIN
    -- exception handling
    BEGIN TRY
		-- declaration of variable
        DECLARE @updated_records_count INT;

        -- update part of the code
        UPDATE module SET
            -- change the level of credits
            credits = 5
        -- condition / where to change the credits
        WHERE mid = @module_id AND level > 1 AND credits < 5;

		-- initialise the variable to get the amount of rows update
		SET @updated_records_count = @@ROWCOUNT

        -- check if records have been updated
        IF @updated_records_count = 0
        BEGIN
            -- meaning that no records was changed
            PRINT 'NO Records Were Changed!!!';
        END
        ELSE
        BEGIN
            -- changes where made to the record ==> output appropriate message
            PRINT CAST(@updated_records_count AS VARCHAR(10)) + ' Records Updated!';
        END

        -- display part of the code

        -- declaration and initialisation
        DECLARE @lecturer_name VARCHAR(30);

        -- find the lecturer that teaches these modules
        SELECT @lecturer_name = lname FROM lecturer
        WHERE lid IN (
            SELECT lecturerid FROM module
            WHERE mid = @module_id AND level > 1 AND credits = 5
        );

        -- output the name of the lecturer
        IF @lecturer_name IS NULL
        BEGIN
            -- meaning that there were not lecturers teaching this module
            PRINT 'NO Lecturers Were Teaching the Module ' + @module_id;
        END
        ELSE
        BEGIN
            -- output the name of the lecturer
            PRINT 'Lecturer Teaching Those Module(s): ' + @lecturer_name;
        END
    END TRY

    BEGIN CATCH
        -- catch and handle the exception
        PRINT 'Error: ' + ERROR_MESSAGE();
        PRINT 'Error Found At Line: ' + CAST(ERROR_LINE() AS VARCHAR(11));
    END CATCH
END
```

### Running the Stored Procedure

But first let me show you our current 'module' table $\downarrow$:

```console
mid	mname	level	credits	lecturerid
M1	Database	1	3	L3
M2	Maths	1	3	L5
M3	Programming	1	3	L1
M4	Biology	2	5	L5
M5	Web	2	5	L2
```

> [!WARNING] The Stored Procedure Will **NOT** Do Anything!!!
> The reason why our Stored Procedure `sp_module` will **not** work is because of this very line: `WHERE mid = @module_id AND level > 1 AND credits = 5`
>
> As you can see; `AND`.
>
> > Well that's $\uparrow$ the reason!

#### Update the Values in Table

Hence, if you want to see any changes when we `EXEC`ute the Stored Procedure... Let's go ahead and _update_ the value for `level` where `mid` is `M1`.

```SQL
-- update the first module id
UPDATE module SET
	-- change the level something greater than 1
	level = 2
-- our search condition
WHERE mid = 'M1';
```

Hence, in this case, the **values** for the _first_ record will become $\downarrow$:

```console
mid	mname	level	credits	lecturerid
M1	Database	2	3	L3
```

#### Execution of Stored Procedure

```SQL
-- execute / run the stored procedure on the first record itself
EXEC sp_module @module_id = 'M1';
```

We should get a result that looks just like this $\downarrow$:

```console
1 Records Updated!
Lecturer Teaching Those Module(s): Emma
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!
