---
id: SQL Procedural Programming - Cursors
aliases: SQL Procedural Programming Traversing Result Sets with Cursors
tags:
  - uni
  - uom
  - db
  - SQL
module: ICDT 1202Y
author: S.Sunhaloo
date: 2025-02-04
status: Completed
---

## List of Contents

- [[#What is Database Cursor?]]
	- [[#Why use Cursors?]]
- [[#Steps to Use Cursors]]
	- [[#The Steps]]
	- [[#Steps with Syntax]]
- [[#Example of Cursor]]
	- [[#Running / Execution of Cursor]]

---

> [!NOTE] Resources
> - https://learn.microsoft.com/en-us/sql/relational-databases/cursors?view=sql-server-ver16
> - https://en.wikipedia.org/wiki/Cursor_(databases)
> - https://learn.microsoft.com/en-us/sql/t-sql/language-elements/declare-cursor-transact-sql?view=sql-server-ver16

# What is Database Cursor?

Typically, when you run a `SELECT` Command ( *for example* ). The *output* / *result* that will get is called the **result set**.

For example, let's say that we are working with this table below $\downarrow$:

```console
lid	lname	title	department
L1	Ricardo	Lecturer	ICT
L2	Paula	Assoc Prof	ICT
L3	Emma	Assoc Prof	SIS
L4	Jeremy	Senior Lecturer	SIS
L5	Sabrina	Senior Lecturer	Science
L6	Gordon	Lecturer	Mech
```

> I know that this is going to be a really *bad example* but bear with me!

Let's say that the above **result set** is only part of it and there are more *lecturers*.

If we want to so a simple **bulk** update whereby we are going to change all the lecturer in the `departement` of `ICT` to `Mech`. Then, the command that we are going to run will look something like this:

```SQL
-- update every lecturer's departement
-- to 'Mech' where their current department
-- is 'ICT'
UPDATE lecturer SET
	-- change the department to 'Mech'
	department = 'Mech'
-- condition
WHERE department = 'ICT';
```

Therefore, we are going to have the new **updated** result set of $\downarrow$:

```console
lid	lname	title	department
L1	Ricardo	Lecturer	Mech
L2	Paula	Assoc Prof	Mech
L3	Emma	Assoc Prof	SIS
L4	Jeremy	Senior Lecturer	SIS
L5	Sabrina	Senior Lecturer	Science
L6	Gordon	Lecturer	Mech
```

> [!WARNING] This is not how it works in Real Life!
> This almost **never happens**!
>
> Yes, in Universities specially, there might be department changes but not in "*bulk*"!

This is where **Cursors** come into play; whereby one can write elaborate code that will check a / multiple row(s) and then do an operation according to *some condition*!

For example, instead of the *condition* being on the `department`. The condition can be on the `lid` whereby, we can check **row by row** for the *value* of `lid` and then perform certain operation on it. In this case, the "*updated*" result set could look like this $\downarrow$:

```console
lid	lname	title	department
L1	Ricardo	Lecturer	Mech
L2	Paula	Assoc Prof	Science
L3	Emma	Assoc Prof	SIS
L4	Jeremy	Senior Lecturer	Programming
L5	Sabrina	Senior Lecturer	Science
L6	Gordon	Lecturer	ICT
```

## Why use Cursors?

Again, in most applications that are connected to a database **server** ( *via the Database API* ). The application normally does **not** work on the **entire** *result set*. Instead they work on **parts** of *result set*!

> [!INFO] In Short
> A database *cursor* is an **object** that enables traversal over the rows of the *result set*.
> It allows for the processing of **individual** row(s) returned by a *query*.

> [!INFO] Types of Cursors
> Resource: https://learn.microsoft.com/en-us/sql/relational-databases/cursors?view=sql-server-ver16#type-of-cursors
>
> There are 4 types of **Cursors** in [[Microsoft SQL Server 2022 Introduction | SQL Server], namely:
>
> 1. Forward Only / *Firehose* Cursors
> 2. Static
> 3. Keyset
> 4. Dynamic
>
> > To learn more about these 'Types'; click the link above $\uparrow$!
>
> > [!NOTE] Default Cursor in SQL Server
> > The **default** Cursor when you do `DECLARE CURSOR` ( *will get to Syntax later on* ) is going to be a **forward only**.
>

# Steps to Use Cursors

Weather you are using 'Microsoft SQL Server' or some other type of relational database servers ( *like PostgreSQL* ). There are some "*mandatory*" steps to be able to *create* and *use* a cursor.

> The reason why "*mandatory*" is because even if you go to Wikipedia $\uparrow$. The steps are pretty much the **same**!

## The Steps

1. Provide the **result set** of an SQL statement to the *Cursor*.
	- Define the **characteristics** / *code* of the cursor
2. *Execute* / *Run* the SQL Statement for Cursor to get populated with **all** the *rows* of the result set
3. Starts iterating ( *with our trusty `WHILE` loop* ) through that result set given
4. Retrieve the row **in** the cursor you want to see.
	- <span style="color: orange;"> Remember</span> : Operation to *retrieve* 1 row / "*block*" of rows from Cursor is called **Fetch**
5. If you have added things like `UPDATE` or `DELETE` in the *second* setup
	- These commands are executed at *this* step
6. Finally, **close** the Cursor

### Steps with Syntax

Here are the above $\uparrow$ Steps with the Syntax!

1. Declare and Define the Result Set to the Cursor

```SQL
-- declaration and definition of cursor
DECLARE CURSOR cursor_name FOR
	-- provide the 'SELECT' statement
	SELECT field_1, field_2, ... FROM table_name
	WHERE condition;
```

2. Open the Cursor to get Populated by Execution of `SELECT` Statement

```SQL
-- open cursor and populate it
OPEN cursor_name;
```

3. Fetch 1 Row from Cursor into variable / *variable list*

```SQL
-- fetch the first row from cursor to variable(s)
FETCH NEXT FROM cursor_name INTO @var_1, @var_2, ...;
```

4. Check whether `FETCH` was **successful** with *system variable* `@@FETCHSTATUS` and continue to `FETCH` with `WHILE` loop

```SQL
-- keep looping and fetching rows if successful
WHILE @@FETCHSTATUS = 0
BEGIN
	-- continue to populate cursor with rows
	FETCH NEXT FROM cursor_name INTO @var_1, @var_2, ...;
	-- other statements here like 'UPDATE', 'DELETE', etc
END;
```

5. Close the Cursor

```SQL
-- close the cursor object
CLOSE cursor_name;
```

6. Last but not least, Deallocate the Cursor

```SQL
-- "remove" the cursor
DEALLOCATE cursor_name;
```

> [!TIP] Some Facts
> 1. We can have **multiple** cursors
> 2. We can have **nested** cursors

# Example of Cursor

> This example is an "*updated*" version of the one in the Lecture Notes.
> The lecture notes can be found over at '[[Database Systems - Cursors + Triggers.pdf]'.

```SQL
-- declaration of variables
DECLARE @lecturer_id CHAR(2), @lecturer_name VARCHAR(30), @lecturer_title VARCHAR(30);

-- declaration and definition of cursor
DECLARE cursor_results CURSOR FOR
	-- our 'SELECT' statement in this case
    SELECT lid, lname, title
    FROM lecturer
    WHERE department = 'ICT';

-- exception handling
BEGIN TRY
	-- open the cursor and populate it with 'SELECT' statement
    OPEN cursor_results;
	
	-- fetch the first row from cursor to variable(s)
    FETCH NEXT FROM cursor_results INTO @lecturer_id, @lecturer_name, @lecturer_title;
    
	-- keep looping and fetching rows if successful
    WHILE @@FETCH_STATUS = 0
    BEGIN
		-- NOTE: execution of Stored Procedure happens here
		
        -- Instead of executing a stored procedure, we print the values
        PRINT 'Lecturer ID: ' + @lecturer_id + ' | Lecturer Name: ' + @lecturer_name + ' | Lecturer Title: ' + @lecturer_title;
        
		-- continue to populate cursor with rows
        FETCH NEXT FROM cursor_results INTO @lecturer_id, @lecturer_name, @lecturer_title;
    END;
	
	-- close and "remove" the cursor
    CLOSE cursor_results;
    DEALLOCATE cursor_results;
END TRY

-- catch and handle the exception
BEGIN CATCH
	-- output appropriate error message
    PRINT 'Error: ' + ERROR_MESSAGE();
    PRINT 'Error occurred at line: ' + CAST(ERROR_LINE() AS VARCHAR(10));

	-- check if whether cursor is closed
    IF CURSOR_STATUS('local', 'cursor_results') > = -1
    BEGIN
		-- close and "remove" the cursor if it stays open
        CLOSE cursor_results;
        DEALLOCATE cursor_results;
    END;
END CATCH;
```

## Running / Execution of Cursor

In this case, running the above $\uparrow$ "*code*" will give us $\downarrow$:

```SQL
Lecturer ID: L1 | Lecturer Name: Ricardo | Lecturer Title: Lecturer
Lecturer ID: L2 | Lecturer Name: Paula | Lecturer Title: Assoc Prof
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!