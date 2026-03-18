---
id: SQL Commands - Data Manipulation Language - INSERT
aliases: SQL Commands - DML ( The INSERT Statement )
tags:
  - SQL
  - db
  - uni
author: S.Sunhaloo
date: 2024-08-21
status: Completed
---

> [!INFO]
> Some of the notes are taken from the lecturer which she took from the book 'Database Systems - A Practical Approach to Design, Implementation, and Management' By Thomas Connolly and Carolyn Begg
>
> > Starts at the bottom of Page 149
> > This file / notes is part of [[Microsoft SQL Server 2022 Introduction | MS SQL Server 2022]]
> > I am trying to make the notes more atomic $\Rightarrow$ Containing a _single_ topic
>
> > Take my last statement as a grain of salt!
>
> In addition, the Lecture Notes / Slides for this is $\Rightarrow$ "[[Database Systems - SQL ( DML - Part 1 ).pdf]"
>
> > Because we are going to refer to some pages in it ( "_innit_" ).

## List of Contents

- [[#The INSERT Statement]]
  - [[#What is the INSERT Statement?]]
  - [[#Template for INSERT Statement]]
- [[#INSERT Data into Tables]]
  - [[#Creating Tables for Examples]]
  - [[#Inserting Data Without Specifying Field Names]]
    - [[#Making Intentional Mistakes]]
  - [[#Inserting Data While Specifying Field Names]]
  - [[#Inserting Data with BULK INSERT]]
  - [[#Inserting Data with SELECT Statement / Command]]

---

# The INSERT Statement

> [!WARNING]
> In [[Microsoft SQL Server 2022 Introduction | Microsoft SQL Server], we run multiple commands **all at once**.
> This means that you can for example ( in the same [[Microsoft SQL Server 2022 Introduction#New Query | Query] ):

## What is the INSERT Statement?

The `INSERT` statement is used to add new rows / records into a table in a database. It can be used in several ways:

- Adding values to **all** columns: You can insert values into all columns of a table, either by explicitly specifying the column names or without specifying them if you're inserting values for every column in the order they appear in the table
- Adding values to **specific** columns: You can insert values into only specific columns of a table by listing the column names before the values, allowing the rest of the columns to use their default values or remain `NULL`

## Template for INSERT Statement

> [!NOTE]-
> For the moment; I will only be adding the _simplest_ `INSERT` statement's templates.
> This is because:
>
> 1. There are much more "_difficult_" ( _more like never saw them in my life_ ) versions
> 2. I have not yet used / learned the other ways to `INSERT` values

### Adding Values to All Columns

```SQL
INSERT INTO table_name ( value1, value2, value3, ... );
```

In this case, the `INSERT` command, will check you table field ( _header_ ) names / attributes and then will insert the values accordingly.

> I don't know why but I cannot convey this information properly...
> I will be writing examples to show you later on

### Adding Values to Specific Columns

> [!TIP]
> **Always** use this one!!!

```SQL
INSERT INTO table_name ( field_1, field_2, field_3, ... ) VALUES ( value_1, value_2, value_3, ... );
```

Here, we are specifying the order of the field / columns names. Hence, when we are going to insert the values in the `VALUES` `( here )`.
We need to then add it in the order that we wrote our columns names.

> Again, don't worry we are going to have examples!

## Template for BULK Insert

### What the Heck is that Now?

> You are going to like this one!

Suppose you have a simple 'Customer' table. Now, someone comes up to you and gives you 3 pages with many _values_ to add into our table.

> I would haven beaten the shit out of him!

As you can see, it would be very difficult to `INSERT` many values by typing out:

```SQL
INSERT INTO Customer ( field_1, field_2, field_3, ) VALUES ( value_1, value_2, value_3, ... );
```

But, now in an alternate universe, that same person comes up to you, give you a pendrive containing a `.csv` file which contains all the data that we need to `INSERT` in the 'Customer' table...

> I would **still** beat his ass up!

> [!INFO]
> Hence, this is why we have the `BULK` insert command / statement!

### Bulk Insert Template

```SQL
BULK INSERT table_name
FROM 'file_path'
WITH (
    FORMAT = 'file_format',
    -- the value for `row_number` is usually '2'
    FIRSTROW = row_number,
    FIELDTERMINATOR = 'field_terminator',
    ROWTERMINATOR = 'row_terminator'
);
```

> We are going to get into these `FORMAT`, `FIRSTROW`, ...
> Be patient Son!

# INSERT Data into Tables

## Creating Tables for Examples

### Creating 'Branch' Table

This is how the table 'Branch' should look like:

| <u> branchNo</u> | street | city | postcode |
| ---------------- | ------ | ---- | -------- |

Use the SQL statement below $\downarrow$ to create the table in [[Microsoft SQL Server 2022 Introduction | Microsoft SQL Server 2022].

```SQL
-- create table 'Branch'
CREATE TABLE Branch (
	-- columns / fields
    branchNo CHAR(4),
    street VARCHAR(20),
    city VARCHAR(15),
    postcode VARCHAR(8),

    -- constraints

    -- primary key
    CONSTRAINT PK_tblBranch PRIMARY KEY ( branchNo ),
    -- primary key constraint
    CONSTRAINT start_with_PK_tblBranch CHECK ( branchNo LIKE 'B%' )
);
```

> [!TIP]- Verification of Creation of Table 'Branch'
> Run the following command below $\downarrow$ to check whether we have successfully created our table:
>
> ```SQL
> SELECT name, type_desc, create_date FROM sys.tables
> WHERE name = 'Branch';
> ```
>
> You should get the result of $\downarrow$:
>
> ```csv
> name	type_desc	create_date
> Branch	USER_TABLE	2024-08-21 08:09:56.840
> ```

### Creating 'Staff' Table

Similarly, this is how we need to have our 'Staff' table created

| <u> staffNo</u> | fName | lName | position | sex | DOB | salary | branchNo $\uparrow$ |
| --------------- | ----- | ----- | -------- | --- | --- | ------ | ------------------- |

Use the SQL statement below $\downarrow$ to create the table in Microsoft SQL Server 2022.

```SQL
-- create table 'Staff'
CREATE TABLE Staff (
	-- columns / fields
    staffNo VARCHAR(4),
    fname VARCHAR(25),
    lname VARCHAR(20),
    position VARCHAR(15),
    sex CHAR(1),
    DOB DATE,
    salary INTEGER,
    branchNo CHAR(4),

	-- contraints

    -- primary key
    CONSTRAINT PK_tblStaff PRIMARY KEY ( staffNo ),
    -- primary key constraint
    CONSTRAINT start_with_PK_tblStaff CHECK ( staffNo LIKE 'S%' ),

	-- check constraints
    CONSTRAINT chk_position_tblStaff CHECK ( position IN ( 'Manager', 'Assistant', 'Supervisor' ) ),
    CONSTRAINT chk_sex_tblStaff CHECK ( sex IN ( 'M', 'F' ) ),
    CONSTRAINT chk_salary_tblStaff CHECK ( salary > 7000 ),

	-- foreign key
    CONSTRAINT FK_branchNo_tblStaff FOREIGN KEY ( branchNo ) REFERENCES Branch ( branchNo ),
	-- foreign key constraint
    CONSTRAINT start_with_FK_branchNo_tblStaff CHECK ( branchNo LIKE 'B%' )
);
```

> [!TIP]- Verification of Creation of Table 'Staff'
> Run the following command below $\downarrow$ to check whether we have successfully created our table:
>
> ```SQL
> SELECT name, type_desc, create_date FROM sys.tables
> WHERE name = 'Staff';
> ```
>
> You should get the result of $\downarrow$:
>
> ```csv
> name	type_desc	create_date
> Staff	USER_TABLE	2024-08-21 08:10:16.620
> ```

> [!NOTE]
> Please refer to '[[SQL Commands - Data Definition Language ( DDL )]' and '[[SQL Commands - Data Definition Language - Constraints]' if you are a bit "_washed_" or "_rusty_".

## Inserting Data Without Specifying Field Names

In this example, we are going to be using this '[[#Adding Values to All Columns]' _template_

Let's say that we have the following values...

| <u> branchNo</u> | street       | city     | postcode |
| ---------------- | ------------ | -------- | -------- |
| B005             | 22 Deer Rd   | London   | SW1 4EH  |
| B007             | 16 Argyll St | Aberdeen | AB2 3SU  |
| B003             | 163 Main St  | Glasgow  | G11 9QX  |
| B004             | 32 Manse Rd  | Bristol  | BS99 1NZ |
| B002             | 22 Deer Rd   | London   | SW1 4EH  |

> [!NOTE]
> Think of these values above $\uparrow$ as the values that the guy gave us **on the page** to insert into the table 'Branch'.

Currently, our table 'Branch' does not have any values in **any** _fields_.
You can check this using the following command $\downarrow$:

```SQL
SELECT * FROM Branch;
```

Here is the result $\rightarrow$ It should be **nothing**.

```csv
-- as you can see nothing is present in the table 'Branch'
branchNo	street	city	postcode
```

### Insert Data / Values into Table 'Branch'

I think you know where this is going... This is pretty simply, we just need to do:

> Here is the _template_ again!

```SQL
INSERT INTO table_name VALUES ( col1, col2, col3, ... );
```

Thus, modifying the above $\uparrow$ command will give us $\downarrow$:

```SQL
INSERT INTO Branch VALUES ( 'B005', '22 Deer Rd', 'London', 'SW1 4EH' );
```

> [!TIP]- Verification of Insertion of Data into Table 'Branch'
>
> ```SQL
> SELECT * FROM Branch;
> ```
>
> Hence, we are going to get the results of:
>
> ```csv
> branchNo	street	city	postcode
> B005	22 Deer Rd	London	SW1 4EH
> ```

#### Making Intentional Mistakes

> Making these mistake to show _me, myself_ and _I_
> What errors we are going to get.
>
> > "_A good programmer, understand the mistakes and then fixes the mistakes accordingly_"

##### Mistake 1: Not Adding Primary Key Value

Let's go ahead add another record. But this time, we are going to not add the `PRIMARY KEY`.

> [!NOTE]
> If you have been reading '[[SQL Commands - Data Definition Language - Constraints#The Primary Key Constraint| SQL Commands - Constraints ( DDL )]'; you will know that the `PRIMARY KEY` Constraint is made up of `UNIQUE` and `NULL` Constraints.
> Hence, in the scenario, we are going to see what errors we are going to get when we do not add the _Primary Key_ into the `INSERT` command
>
> > BTW I am **not** going to do every errors in the _world_... Obviously.

Insert the following statement $\downarrow$:

```SQL
INSERT INTO Branch VALUES ( '16 Argyll St', 'Aberdeen', 'AB2 3SU' );
```

Here, you are going to get a message that looks something like this:

```console
Column name or number of supplied values does not match table definition.
```

> Wait, I thought it was going to give another type of error.
> Like missing Primary Key.

##### Mistake 2: Adding Values in Wrong Order

Like I have been saying and also adding the values; I have added the values in the order that the 'Branch' table has been created.
Now, we are going to try to add a record whereby the its _values_ are **not** in the correct order of the field names in the table.

Try inserting the values found below $\downarrow$; using this command:

```SQL
INSERT INTO Branch VALUES ( 'SW1 4EH', '22 Deer Rd', 'B005', 'London' );
```

We need to get an error that looks something along the lines of this:

```console
String or binary data would be truncated in table
'DatabaseName.dbo.Branch', column 'branchNo'.
Truncated value: 'SW1 '.
```

## Inserting Data While Specifying Field Names

> [!TIP]
> _Again_, **Always** use this one!!!

This is pretty simple, again, here is the _template_.

```SQL
INSERT INTO Customer ( field1, field2, field3, ) VALUES ( value1, value2, value3, ... );
```

Here is a concrete example of adding another record into the table 'Branch';

```SQL
-- adding another record into table 'Branch' while specifying columns
INSERT INTO Branch ( branchNo, street, city, postcode ) VALUES ( 'B007', '16 Argyll St', 'Aberdeen', 'AB2 3SU' );
```

> [!TIP]- Verification of Adding Records to Table 'Branch'
>
> ```SQL
> SELECT * FROM Branch;
> ```
>
> Here is the output after running the command above $\uparrow$
>
> ```csv
> branchNo	street	city	postcode
> B005	22 Deer Rd	London	SW1 4EH
> B007	16 Argyll St	Aberdeen	AB2 3SU ---> Our Record
> ```

When we are adding the values above $\uparrow$ ( _without specifying the column names_ ). We are adding it in the order that the fields are in the actual table.

> Like the way the order is... `branchNo`, `street`, `city` and `postcode`.

But here we can also shuffle the way the fields are order.

> [!NOTE]
> I will not change the order in the **actual** table.
> But, it will facilitate your life as you only need to remember the field / attribute names ( _and not the order also_ )
>
> > You will see what I am trying to say.

```SQL
INSERT INTO Branch ( city, branchNo, postcode, street ) VALUES ( 'Glasgow', 'B003',  'G11 9QX', '162 Main St' );
```

> Let's try adding this record into our table and then we can see if the insertion was in the correct _order_.

> [!TIP]- Verification of Adding Records to Table 'Branch'
> Here is the result after running `SELECT * FROM Branch WHERE branchNo = 'B003';`:
>
> ```csv
> branchNo	street	city	postcode
> B003	162 Main St	Glasgow	G11 9QX
> ```

---

Now, we have tried some _possibilities_; let's go ahead and add the rest of the date using the following statements found in the code block below:

```SQL
-- Inserting Data / Values into table 'Branch'
INSERT INTO Branch ( branchNo, street, city, postcode ) VALUES ( 'B004', '32 Manse Rd', 'Bristol', 'BS99 1NZ' );
INSERT INTO Branch ( branchNo, street, city, postcode ) VALUES ( 'B002', '56 Clover Dr', 'London', 'NW10 6EU' );
```

> [!TIP] Today is the $4^{th}$ of March 2025 @15:44
> I just found out that you don't need to run multiple `INSERT` commands ( _like $\uparrow$_ ).
>
> Instead we could have simply ran this $\downarrow$:
>
> ```SQL
> -- Inserting Data / Values into table 'Branch'
> INSERT INTO Branch ( branchNo, street, city, postcode ) VALUES
> ( 'B004', '32 Manse Rd', 'Bristol', 'BS99 1NZ' ),
> ( 'B002', '56 Clover Dr', 'London', 'NW10 6EU' );
> ```
>
> > "_This is superior_!!!"... Thank You Karishma!

> [!INFO]
> You can just copy all of this, place it in the Query _Editor_ and then press `<F5> ` to run the commands.
> But this _feature_ does <span style="color: red;"> <strong> not</strong> </span> work in every SQL DBMSs.
> Hence, the lecturer always tells us to run it one at a time...
>
> > I do **not**. Coming from Oracle 10g ( _which was released in 2003_ ) where we need to use it because the lecturer at [[University Data View ( Level 1 Semester 1 ) | UTM] did not know any shit!
> > I will gladly use this "_run-all_" command.

Therefore after populating our 'Branch' table; you can see that we have all these values in the table

```csv
branchNo	street	city	postcode
B002	56 Clover Dr	London	NW10 6EU
B003	162 Main St	Glasgow	G11 9QX
B004	32 Manse Rd	Bristol	BS99 1NZ
B005	22 Deer Rd	London	SW1 4EH
B007	16 Argyll St	Aberdeen	AB2 3SU
```

---

## Inserting Data with BULK INSERT

> Have you ever opened a `.csv` file.
> If **not**; then go ahead and die.

### Inserting Values into Table 'Staff' using BULK INSERT

> [!NOTE]
> The lecturer did not gave us any `.csv` file for the 'Staff' table.
> Hence, I am going to create my own `.csv` file from the values that we need to add into the table 'Staff'
>
> > Here we go!!!

#### Data / Values to Insert

| <u> staffNo</u> | fName | lName | position   | sex | DOB       | salary | branchNo $\uparrow$ |
| --------------- | ----- | ----- | ---------- | --- | --------- | ------ | ------------------- |
| SL21            | John  | White | Manager    | M   | 1-Oct-45  | 30000  | B005                |
| SG37            | Ann   | Beech | Assistant  | F   | 10-Nov-60 | 12000  | B003                |
| SG14            | David | Ford  | Supervisor | M   | 24-Mar-58 | 18000  | B003                |
| SA9             | Mary  | Howe  | Assistant  | F   | 19-Feb-70 | 9000   | B007                |
| SG5             | Susan | Brand | Manager    | F   | 3-Jun-40  | 24000  | B003                |
| SL41            | Julie | Lee   | Assistant  | F   | 13-Jun-65 | 9000   | B002                |

#### The `.csv` File

<p align="center"> File Name: <code> staff.csv</code> </p>

```csv
staffNo,fName,lName,position,sex,DOB,salary,branchNo
SL21,John,White,Manager,M,1-Oct-45,30000,B005
SG37,Ann,Beech,Assistant,F,10-Nov-60,12000,B003
SG14,David,Ford,Supervisor,M,24-Mar-58,18000,B003
SA9,Mary,Howe,Assistant,F,19-Feb-70,9000,B007
SG5,Susan,Brand,Manager,F,3-Jun-40,24000,B003
SL41,Julie,Lee,Assistant,F,13-Jun-65,9000,B002
```

> [!INFO]
> You will see that the header starts on row **4** and the actual values starts at row **2**.
> You will see what parameters / options we are going to set so that we can `BULK INSERT` our data correctly without errors.
>
> > [!NOTE]
> > SQL is not like programming languages and we do not start with '0'. Instead it is similar to MATLAB where we start with '1'.

> I hope my `staff.csv` file will work

### Explaining the BULK INSERT Command

Here is the template again for the `BULK` Insert command $\downarrow$:

```SQL
BULK INSERT table_name
FROM 'file_path'
WITH (
    FORMAT = 'file_format',
    FIRSTROW = row_number,
    FIELDTERMINATOR = 'field_terminator',
    ROWTERMINATOR = 'row_terminator'
);
```

#### Explaining _Some_ Parts

```SQL
FORMAT = 'file_format'
```

This can take 2 pre-defined values:

1. `CSV`
2. `TXT`

> I think this one is pretty self-explanatory

```SQL
-- where `row_number` is an INTEGER number
FIRSTROW = row_number
```

With this option, we are going to specify the **row** in which the actual <span style="color: orange;"> <strong> data</strong> </span> lives.

> Hence in our case we ( _if you would please glance back at the above $\uparrow$ `.csv` values_ ), we need to start at '2' because our **actual data** lives / starts at row '2'.

```SQL
-- can take the values of ',', ';', '|', ' ', '\t'
-- or any custom character that you would like ( depending on your fucking .csv file of course )
FIELDTERMINATOR = ','
```

Here, we can specify what character are our values in the `.csv` file are separated with.
In fact, this _option_ `FIELDTERMINATOR` is quite a jack of all trades; this is because it can take any character.
For example if you have $\downarrow$:

```csv
please insert this

SL21aJohnaWhiteaManageraMa1-Oct-45a30000aB005
```

In the example above $\uparrow$, our values are separated with the character 'a'. Hence `FIELDTERMINATOR = 'a'`

> Therefore in our case, we are going to use the character `,` as our `FIELDTERMINATOR`.

```SQL
-- the character that we are going to use to end the current record
-- telling SQL that we need to change line to insert the other record.
ROWTERMINATOR = '\n'
```

> [!NOTE]
> Sometimes you might see people use the "_character(s)_" `0x0a`. This is basically the same thing as `\n`.
>
> > [!INFO]
> > If you have used VS Code on both Linux / Unix and Window system. You will know that we something called Line Feed ( LF ) and Carriage Line Feed ( CRLF ).
> > Basically Linux / Unix based system _end_ lines of text in different format than Windows ( _because its shit $\rightarrow$ "for programmers"_ )
> > In addition, sometimes if you push something **from** a Windows machine using `git push -u origin branch_name`; you will see that it will say something along the lines of $\downarrow$:
> >
> > ```console
> > ... CRLF will be replaced by LF...
> > ```
> >
> > This is because Git needs to convert is to the most appropriate type of "_end of line sequence / character_".
> >
> > From what I am guessing...
>
> But just know that we typically use the characters `\n` or `0x0a`!

### Insert Data / Values into Table 'Staff'

Hence, we can use the following command to insert our data **from** the `staff.csv` file into our table.

```SQL
BULK INSERT Staff
-- in my case the file was found on the 'Desktop' folder / directory
-- where 'username' was my username
FROM 'C:\Users\username\Desktop\staff.csv'
WITH (
    FORMAT = 'CSV',
    FIRSTROW = 2,
    FIELDTERMINATOR = ',',
    ROWTERMINATOR = '\n'
);
```

> [!TIP]- Verification of Insertion of Values into Table 'Staff'
> Select all the values from the table 'Staff' using $\downarrow$:
>
> ```SQL
> SELECT * FROM Staff;
> ```
>
> Here are the data / values that has been added:
>
> ```csv
> staffNo	fname	lname	position	sex	DOB	salary	branchNo
> SA9	Mary	Howe	Assistant	F	1970-02-19	9000	B007
> SG14	David	Ford	Supervisor	M	1958-03-24	18000	B003
> SG37	Ann	Beech	Assistant	F	1960-11-10	12000	B003
> SG5	Susan	Brand	Manager	F	2040-06-03	24000	B003
> SL21	John	White	Manager	M	2045-10-01	30000	B005
> SL41	Julie	Lee	Assistant	F	1965-06-13	9000	B002
> ```

---

## Inserting Data with SELECT Statement / Command

> Here also I will be giving the example first

### Creating Table

Let's go ahead and create the table 'StaffPropCount'.

```SQL
CREATE TABLE StaffPropCount (
	-- columns / fields
	staffNo VARCHAR(4),
	fname VARCHAR(25),
    lname VARCHAR(20),
	propCount INTEGER,

	-- constraints

	-- primary key
	CONSTRAINT PK_tblStaffPropCount PRIMARY KEY ( staffNo ),
	-- primary key constraint
	CONSTRAINT start_with_PK_tblStaffPropCount CHECK ( staffNo LIKE 'S%' )
);
```

### Inserting the Data / Values into Table

Instead of getting values from a `.csv` file or someone has told you to enter some fucking shitty-ass values.
We can also `INSERT` data from **another** _table_ with the `SELECT` command.

In the example that I am going to give; I will be taking the values from our table 'Staff' and also 'PropertyForRent'.

> [!INFO]
> If you need all the table that I am using and also the values.
> You can use the file / note '[[Database Systems - Labsheet 1 ( L1S1 )]' and also '[[Database Systems - Labsheet 3 ( L1S1 )]'.

#### Template for `INSERT... SELECT` Statement

```SQL
INSERT INTO table_name0 (col1, col2, ...)
SELECT col1, col2, ...
FROM table_name1, table_name2
-- join operation
WHERE table_name1.col1 = table_name1.col1
GROUP BY col1, col2, ...;
```

For us, this should look something like this $\downarrow$:

```SQL
-- this is good
-- NOTE: this very example is wrong in the lecture slides.
INSERT INTO StaffPropCount (staffNo, fName, lName, propCount)
SELECT s.staffNo, s.fName, s.lName, COUNT(*)
FROM Staff s, PropertyForRent p
WHERE s.staffNo = p.staffNo
GROUP BY s.staffNo, s.fName, s.lName;
```

> [!BUG] Ask the Lecturer about this!!!

> [!WARNING]
>
> > What I am talking about is found on page 10!
>
> So the Lecturer told us to "_Populate the 'StaffPropCount' table using details from the 'Staff' and 'PropertyForRent' tables_"
> Hence, the _correct_ answer for this example / question is:
>
> ```SQL
> INSERT INTO StaffPropCount (staffNo, fName, lName, propertyCount)
> -- please excuse the character `\` in the `COUNT()` function
> -- needed to add this because of Markdown
>
> -- this is the list of staff who currently
> -- manage at least 1 property
> SELECT s.staffNo, s.fName, s.lName, COUNT(\*)
> FROM Staff s, PropertyForRent p
> WHERE s.staffNo = p.staffNo
> GROUP BY s.staffNo, s.fName, s.lName
> UNION
> -- this one is the list of staff who do not
> -- manage any properties
> SELECT s.staffNo, s.fName, s.lName, 0
> FROM Staff s
> WHERE NOT EXISTS (
>    SELECT 1
>    FROM PropertyForRent p
>    WHERE p.staffNo = s.staffNo
> );
> ```
>
> Therefore, we are going to get the following output $\downarrow$:
>
> ```csv
> staffNo	fname	lname	propCount
> SA9	Mary	Howe	1
> SG14	David	Ford	1
> SG37	Ann	Beech	2
> SG5	Susan	Brand	0
> SL21	John	White	0
> SL41	Julie	Lee	1
> ```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!
