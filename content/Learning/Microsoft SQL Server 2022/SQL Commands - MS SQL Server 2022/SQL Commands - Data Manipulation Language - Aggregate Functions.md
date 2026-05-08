---
id: SQL Commands - Data Manipulation Language - Aggregate Functions
aliases:
  - SQL Commands - DML ( SELECT ---> Built-In Functions )
tags:
  - SQL
  - uni
  - db
  - uom
author: S.Sunhaloo
date: "2024-08-04"
status: Completed
---

> [!INFO]
> This is actually part of the file / note [[SQL Commands - Data Manipulation Language - SELECT]]
> These notes are found in the "[[Database Systems  - SQL ( DML - Part 1 ).pdf]" starting at page 44 ( *the GOAT himself $\rightarrow$ 44* )
> Nevertheless, there will be thing that I will also include from "[[Database Systems  - SQL ( DML - Part 2 ).pdf]"
> > Because all of it is related!

> [!NOTE]
> You will see that we have things like `GROUP BY` and `HAVING` that I was referring to.
> Here is the file: "[[SQL Commands - Data Manipulation Language - GROUP BY and HAVING|SQL Commands - DML ( SELECT ---> GROUP BY and HAVING )]"
>
> Why am I adding this here?
> Again, I was referring to a file that did not exists yet!
> > But now it does!
>

## List of Contents

- [[#Aggregate Functions]]
	- [[#Templates]]
	- [[#COUNT Function]]
		- [[#Examples of COUNT Function]]
	- [[#They are Different]]
	- [[#SUM and AVG Function]]
		- [[#Example of AVG Function]]
		- [[#Example of SUM Function]]
	- [[#MIN and MAX Functions]]

---

> [!INFO] Resource
> - Website:
> 	- https://learn.microsoft.com/en-us/sql/t-sql/functions/aggregate-functions-transact-sql?view=sql-server-ver16

# Aggregate Functions

> [!TIP] What are Aggregate Functions?
> They are functions in SQL that perform a calculation on a set of values and return a single value.

> [!TIP] Common Aggregate Functions
> 1. `COUNT()`
> 2. `SUM()`
> 3. `AVG()`
> 4. `MIN()`
> 5. `MAX()`

> [!TIP] Some Properties of Aggregate Functions
> - Each operate on a **single** column / field of a table and returns a single value
> - `COUNT()`, `MIN()` and `MAX()` apply to **[[SQL Commands - Data Manipulation Language - SELECT#Non-Numeric Literals | Non-Numeric]** and **[[SQL Commands - Data Manipulation Language - SELECT#Numeric Literals | Numeric]**
> - `SUM()` and `AVG()` are used on *Numeric* fields **only**.
> - `COUNT(*)` ( *we are going to see this later* ) $\rightarrow$ counts **all rows / records** of a table
> 	- Regardless if the table has `NULL` / duplicate values
> 	- Hence, we could use the `DISTINCT` keyword to remove the duplicates
> - Apart from `COUNT(*)` $\rightarrow$ because `COUNT(col_name)` <span style="color: orange;"> removes</span> the `NULL` and duplicate values!
> 	- Each function will eliminate `NULL` first
> 	- After that, it operates **only** on remaining Non-`NULL` values
> - `DISTINCT` keyword has no effect with `MIN()` and `MAX()`
> 	- May have *issues* with `SUM()` and `AVG()`

> [!NOTE]
> Aggregate Functions will return 'No Column Name' as the header in the results / `.csv` file.
> Hence, we are going to use the [[SQL Commands - Data Manipulation Language - SELECT#The Alias / AS Command | `AS`] keyword to give name to those columns.

## COUNT Function

Basically the `COUNT()` function will return the number of values in a specified columns.
In other words; it return the number of *records* in a table.

The `COUNT()` function is weird in the sense that you can use whatever column that you want. Because it will return the **same** *value* for any field that you choose to pass in as *argument* into the `()`.

### Templates

> Like I have been saying with my other [[Microsoft SQL Server 2022 Data View | SQL] notes.
> Take these templates with a grain of salt!

#### Single Fields / Column

```SQL
SELECT COUNT(col1) FROM table_name;
```

#### Multiple Fields / Columns

```SQL
-- I don't understand why someone would use that
-- nevertheless, we COULD / know how to do it!
SELECT COUNT(col1), COUNT(col2) FROM table_name;
```

#### All Columns

Similar to doing [[SQL Commands - Data Manipulation Language - SELECT#Display Everything | this] $\downarrow$:

```SQL
-- where we use the '*' character
SELECT * FROM table_name;
```

We are also going to do something close here:

```SQL
SELECT COUNT(*) FROM table_name;
```

> This is the $\uparrow$ most used "*way*" of the `COUNT()` function.
> But that does not mean its good for everything.
> Because when [[SQL Commands - Data Manipulation Language - SELECT#The DISTINCT Command | `DISTINCT`] will come we are going to have to use the 'Single Column' *template*.
> I will give example below! $\downarrow$

### Examples of COUNT Function

> [!NOTE]
> For this I will be using the same table for every "*sub-examples*" of the `COUNT()` function.
> This is to be able to show you that *weirdness* that I was talking about $\uparrow$

I will be using the 'Staff' table that I re-created in my `Test` Database. Here is how the current version of the 'Staff' table looks like.

```csv
staffNo,fname,lname,position,sex,DOB,salary,branchNo
SA9,Mary,Howe,Assistant,F,1970-02-19,9270,B007
SG14,David,Ford,Manager,M,1958-03-24,20000,B003
SG37,Ann,Beech,Assistant,F,1960-11-10,12360,B003
SG5,Susan,Brand,Manager,F,2040-06-03,25956,B003
SHIT,NULL,lastname,Manager,F,2024-08-30,20000,B007
SL21,John,White,Manager,M,2045-10-01,32445,B005
SL41,Julie,Lee,Assistant,F,1965-06-13,9270,B002
```

---

#### Example 1: Passing a Single Column

```SQL
SELECT COUNT(staffNo) AS Total FROM Staff;
```

> [!TIP]- Output for `COUNT()` - Example 1
> This will be the result.
>
> ```csv
> Total
> 7
> ```

#### Example 2: Passing Multiple Columns

> Like I have said I have never used it and I don't know why you will have to do this...
> Fuck me bro, while writing the line just above, I thought of a use case where you might need to use this method...

Let's say that your table is not "*square*"; then I think that this will work

![[SQL Commands - Square vs Not-Square Table Difference.png | 650]]

```SQL
SELECT COUNT(staffNo) AS COUNT_staffNo, COUNT(fname) AS COUNT_fname FROM Staff;
```

> [!TIP] Output for `COUNT()` - Example 2
> Hence, we are going to get this... As you can see they are **different**!
> ```csv
> COUNT_staffNo	COUNT_fname
> 7           	6
> ```

#### Example 3: Using `*` As "Argument"

This will count **EVERYTHING**!!!

```SQL
SELECT COUNT(*) AS COUNT_ALL FROM Staff;
```

> [!TIP] Output for `COUNT()` - Example 2
> Here it will count **everything** like the `NULL` and also **duplicate** *values*.
>
> ```csv
> COUNT_ALL
> 7
> ```

#### Example 3: Using the `DISTINCT` Keyword

Let's say that we have to find the different properties that have been view in May 2004.Then we are going to have to use the `DISTINCT` keyword else we are going to have **duplicate** values.

Like take a look at this table:

```SQL
SELECT clientNo, propertyNo, viewdate FROM Viewing;
```

This is the values for the 3 fields from the 'Viewing' Table.

```csv
clientNo	propertyNo	viewDate
CR56	    PA14	    2004-05-24 <--- In May + Duplicate
CR56	    PG36	    2004-04-28
CR56	    PG4	        2004-05-26 <--- In May + Duplicate
CR62	    PA14	    2004-05-14 <--- In May Only
CR76	    PG4	        2004-04-20
```

Hence, we are not here to find our *how many people in total* have view each property.
We are here to find out **how many different properties have visited / viewed a in May**.
Hence, <span style="color: red;"> need</span> to use the `DISTINCT` keyword for us to get the *result* we want!

Thus, this will be the statement that we are going to run $\downarrow$:

```SQL
SELECT COUNT(DISTINCT propertyNo) AS MayView_COUNT FROM Viewing
-- specify we need the month to be in May
WHERE viewDate > '2004-05-01' AND viewDate < '2004-05-31';
```

> [!TIP]- Output of **Different** Properties Viewed in May
> This should be the correct output after running the `COUNT()` function with the `DISTINCT` keyword.
>
> ```csv
> MayView_COUNT
> 2
> ```

---

> [!NOTE] Are They Not Bland or Feel Like Information are Missing?
> Yes, we do *know* how many *client* came to visit in the month of May...
>
> "*But who are they? What properties did they view?*"
>
> Hence, our query result can be improve and I will take an example...
>
> > For now, you might no understand what some of these **keywords** are going to...
> > But I will go over them later on or on another note ( *check above $\uparrow$* )
>
> ```SQL
> -- in addition to displaying `COUNT()`, we are going to display the `clientNo`, `propertyNo`
> SELECT clientNo, propertyNo, COUNT(DISTINCT propertyNo) AS MayView_COUNT FROM Viewing
> -- again, specifying the view date to be in the month of May
> WHERE viewDate BETWEEN '2004-05-01' AND '2004-05-31'
> -- allow normal fields to be able to display with Aggregate Functions`
> -- NOTE: take the above comment as a grain of salt; I have not yet understood how it works...
> GROUP BY clientNo, propertyNo;
> ```
>
> Hence, this will output something like this:
>
> ```csv
> clientNo	propertyNo	MayView_COUNT
> CR56	    PA14	    1
> CR56	    PG4 	    1
> CR62	    PA14	    1
> ```
>
> > Much more pleasing and yes it has more information also!
>

---

## They are Different

Okay, I did not know where to place this and it feels wrong to place it in a "warning" context; because it is a fundamental knowledge of how *Aggregate Functions* work

Let's take a really simple example; something like this $\downarrow$:

> This example was taken from the Lecture Slides ( *DML Part 2* )
> Because I was trying to come up with a good example; but I failed miserably.
> Hence, Lecture Note's Examples it is!

> [!WARNING]
> It might seem weird for now, but I will go over them later on.
> > Like I will make another file / note covering the *clauses* that I will be using in the example below $\downarrow$:

```SQL
SELECT branchNo, COUNT(staffNo) FROM Staff
WHERE COUNT(staffNo) > 1;
```

> [!INFO] Explanation of above $\uparrow$ Statement
> This should return; for each Branch with more than 1 member of Staff.

> [!BUG] But this will **NOT** work
> You are going to get an error that will look something like this $\downarrow$:
>
> ```console
> An aggregate may not appear in the WHERE clause
> unless it is in a subquery contained in a HAVING clause or a select list,
> and the column being aggregated is an outer reference.
> ```

> [!TIP] Explanation of `WHERE` v/s `HAVING`
> Basically:
>
> - `WHERE` $\rightarrow$ Filters by **Individual Rows**
> - `HAVING` $\rightarrow$ Filters **Groups**
>
> For *Aggregate Functions*; for us to use them **with** like simple columns / fields like `staffNo`, `city`, we need to first do a `GROUP BY`
>
> > Don't fucking ask me why BTW!
>

In short, what I am trying to say is that we need to first do `GROUP BY` and if we want to *replicate* the `WHERE` clause; we need to instead use `HAVING`

Thus, in our example that we took that did not run using `WHERE`; its corrected version will be $\downarrow$:

```SQL
SELECT branchNo, COUNT(staffNo) AS Staff_COUNT FROM Staff
-- we do the grouping first ---> because simple and aggregate functions
-- don't work together
GROUP BY branchNo
-- find all the 'branches' with a "count" of staff greater than 1
HAVING COUNT(staffNo) > 1;
```

> [!TIP]- Therefore the output will be
>
> ```csv
> branchNo	Staff_COUNT
> B003	    3
> B007	    2
> ```

> [!WARNING]- Friendly Warning
> The table is different from the [[Database Systems - Labsheet 1 ( L1S1 )#Staff Table| Staff Table] that we created in the Labsheet.
> This is the reason why I included the current version of the 'Staff' table in this very note [[#Examples of COUNT Function | above] $\uparrow$.

> [!SUCCESS] I think we are done for the time being with the `COUNT()` Function!

## SUM and AVG Function

> Yes, I am combining them together!

Well, well, well, look who we found! The `SUM()` function... I think you already know where this is going!

> Let me get straight to the examples!

### Example of AVG Function

#### Example 1: Find the Average of `salary` of All Staffs

```SQL
SELECT AVG(salary) AS AVG_Salary FROM Staff;
```

> [!TIP]- Output of Average Salary of All Staffs
> This should be the result if we are using our modified table with its modified values...
>
> ```csv
> AVG_Salary
> 18471
> ```

### Example of SUM Function

#### Example 1: Find Sum and Average Salary of All Staff

```SQL
SELECT SUM(salary) AS Total_Salary, AVG(salary) AS AVG_Salary FROM Staff;
```

> [!TIP]- Result for Sum and Average Salary of All Staff
> Here is the output after running the above $\uparrow$ command:
>
> ```csv
> Total_Salary	AVG_Salary
> 129301      	18471
> ```

#### Example 2: Find Number of Managers, Sum and Average of Their Salary

```SQL
SELECT COUNT(staffNo) AS Manager_COUNT, SUM(salary) AS Salary_COUNT, AVG(salary) AS AVG_Salary FROM Staff
WHERE position = 'Manager';
```

> [!TIP]- Result for Number of Managers, Sum + Average of Their Salary
> This should be the results according the the modified 'Staff' table.
>
> ```csv
> Manager_COUNT	Salary_COUNT	AVG_Salary
> 4	            98401       	24600
> ```

## MIN and MAX Functions

As we have said above $\uparrow$; the `COUNT()`, `MIN()` and `MAX()` Function **works** on *numeric* and *non-numeric* data types.

> Hence, we are going to do some examples with "*non-numerics*".
> So that I can get an idea of how it works with the *English Alphabet*.

### Example of MIN and MAX Function

#### Example 1: Find the Minimum and Maximum Salary of Staff

```SQL
SELECT MIN(salary) AS Minimum_Salary, MAX(salary) AS Maximum_Salary FROM Staff;
```

> [!TIP]- Output of Minimum and Maximum Salary
> After running the above $\uparrow$ command; we should get something that looks like this $\downarrow$
>
> ```csv
> Minimum_Salary	Maximum_Salary
> 9270                   	32445
> ```

---

> [!SUCCESS] I think we are done here!!!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!
