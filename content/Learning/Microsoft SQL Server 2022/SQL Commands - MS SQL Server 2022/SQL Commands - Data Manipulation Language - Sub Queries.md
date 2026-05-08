---
id: SQL Commands - Data Manipulation Language - Sub Queries
aliases:
  - SQL Commands - DML ( Sub Queries in SQL )
tags:
  - SQL
  - uni
  - uom
  - db
author: S.Sunhaloo
date: "2024-09-13"
status: Completed
---

> [!INFO]
> The Lecture Slides for this file / note is called '[[Database Systems  - SQL ( DML - Part 2 ).pdf]' $\Rightarrow$ **Sub Queries** starts at page 12.
> This file / note is definitely related with this note $\rightarrow$ '[[SQL Commands - Data Manipulation Language - SELECT]'
>
> But some other notes that could also be related are:
>
> 1. [[SQL Commands - Data Manipulation Language - Aggregate Functions]]
> 2. [[SQL Commands - Data Manipulation Language - GROUP BY and HAVING]]
> 3. [[SQL Commands - Data Manipulation Language - JOIN]]

## List of Contents

- [[#Sub Query]]
	- [[#Examples of Sub-Queries]]
		- [[#IN Keyword]]
	- [[#ANY / SOME - ALL Keyword]]

---

# Sub Query

> [!TIP] Lecturer's Notes
> - SQL statement can have a ( *or multiple* ) `SELECT` "*statements*" embedded within them
> - This "*sub-select*" can be used in `WHERE` and `HAVING` clauses of an **outer** `SELECT`, where it is called a **sub-query** or a **nested-query**.
> - Sub-selects may also appear in `INSERT`, `UPDATE`, and `DELETE` statements

> Let's get a real example going to be able to understand this "*nested-select*" statements.

## Examples of Sub-Queries

> Before I start did I explain ( *myself* ) the `IN` keyword; because I think I have been using it...
> I guess we have used it over at [[SQL Commands - Data Manipulation Language - SELECT#List Search Condition | List Search Condition]]
> Well, if I have not; I guess I will explain it when I encounter it.

### Example: Sub Query with Equality

Carefully **read** and **understand** the SQL code below $\downarrow$:

```SQL
-- this is normal as always
SELECT staffNo, lname AS Last_Name, fname AS First_Name, position FROM Staff
-- but here...
WHERE branchNo = (
	-- subquery
	SELECT branchNo FROM Branch
	-- we CANNOT add the ';' character here
	-- because the code does not end here
	WHERE street = '162 Main St'
-- the code ends here v
);
```

> [!TIP]- Output of Sub-Query with **Equality**
> This should be the output $\downarrow$:
>
> ```csv
> staffNo	Last_Name	First_Name	position
> SG14   	Ford    	David   	Supervisor
> SG37   	Beech    	Ann     	Assistant
> SG5    	Brand    	Susan   	Manager
> ```

---

#### IN Keyword

> [!NOTE] Key Points
> Here the `WHERE` clause look like this:
>
> ```SQL
> -- right now we are explaining the '=' character
> WHERE branchNo = ...
> ```
>
> Let's go ahead the run only the Sub-Query part and we are going to see it's results
> ```SQL
> -- sub-query only
> SELECT branchNo FROM Branch
> WHERE street = '162 Main St';
> ```
>
> > We need to get only **1** result!!!
> > Yes! **result** and <span style="color: red;"> not</span> *record*.
>
> ```csv
> branchNo
> B003
> ```
> > [!WARNING] But what if the **Sub-Query** returns more the 1 result / record?
> > This is where the `IN` keyword comes into play.
> > Basically if your sub-query will return more than 1 value / record; then simple swap the `=` character for `IN`
> > Now how are you going to know if your sub-query / sub-queries is going to return more than 1 value?
> > No, especially if you have **multiple** sub-queries and you **don't** have the table in front of you!
> > 
> >  Because I don't think in a company they are going to give you fucking pieces of paper with the tables printed on them
> >  But if you ask for them, **they will surely give you the _termination letter_**!!!
>
> > [!TIP] Hence...
> > This is why you use the `IN` keyword for every sub-query that you write.
> > Like really how are you going to know how many values it will return ( *if you have an answer $\rightarrow$ please DM me!* )

---

> Moving On!

### Example: Sub-Query with Aggregate Functions

As you know from our notes on Aggregate Functions; we cannot do things like $\downarrow$.

> These are going to be "*shit*" examples BTW.

```SQL
-- this is wrong
WHERE salary > AVG(salary)
-- this is also wrong
WHERE number > COUNT(staffNo)
-- this is also also wrong
WHERE total > SUM(pay)
```

Therefore, we can definitely use the **sub-queries** to add like the `HAVING` clause!

> これを見てください!

```SQL
-- select the fields as we do normally
SELECT staffNo, fName, lname, position,
	-- also the select the fields that
	-- we want to use the aggregate function on
	-- use '-' to indicate sub-query at 'field' / 'column' level
	salary - (SELECT AVG(salary) FROM Staff) AS SalDiff
FROM   Staff
-- similar to the `HAVING` clause
WHERE  salary > (SELECT AVG(salary) FROM Staff);
```

> [!TIP]- Output of Sub-Query with **Aggregate Functions**
> ```csv
> staffNo	fName	lname	position	SalDiff
> SG14	David	Ford	Supervisor	1000
> SG5 	Susan	Brand	Manager 	7000
> SL21	John	White	Manager 	13000
> ```

### Example: Nested Sub-Queries

Here we are definitely going to use the [[#IN Keyword].

```SQL
SELECT propertyNo, street, ptype, rooms, rent FROM PropertyForRent
WHERE staffNo IN (
		-- this will return multiple values
        SELECT staffNo FROM Staff
		-- even though this sub-query will return 1 value only
		-- I am still going to use the `IN`
		-- this is because it won't hurt anyone...
        WHERE branchNo IN (
            SELECT branchNo FROM Branch
            WHERE street = '162 Main St'
        )
);
```

> [!TIP]- Output of Sub-Query with **Nested Sub-Queries**
> This should be the output $\downarrow$:
>
> ```csv
> propertyNo	street	ptype	rooms	rent
> PG16    	5 Novar Dr	Flat	4	450
> PG21    	18 Dale Rd	House	5	600
> PG36    	2 Manor Rd	Flat	3	375
> ```

## ANY / SOME - ALL Keyword

> [!TIP] Notes From Lecture Slides
> - `ANY` and `ALL` *may* be used with **sub-queries** that produces a *single* column of *numbers*
> - `ALL` $\Rightarrow$ **Only** be `true` if is satisfies <span style="color: red;"> <strong> all</strong> </span> produced by sub-query
> - `ANY` $\Rightarrow$ `true` if it satisfies <span style="color: orange;"> <strong> any</strong> </span> values produced by sub-query
> - If sub-query is **empty**
> 	- `ALL` returns `true`
> 	- `ANY` return `false`
>
> > `SOME` = `ANY`
>

### Example: ALL Keyword

This is the *template*:

```SQL
SELECT column_name(s)
FROM table_name
-- operator could be '=', '> ', '<' and so on
WHERE column_name operator ALL (
	SELECT column_name FROM table_name  WHERE condition
);
```

#### Example: Without `WHERE`

> [!WARNING]
> This $\downarrow$ example is redundant as the `ALL` keyword is performing the *same* action as the `SELECT` statement ( *in this case* ).

```SQL
SELECT ALL staffNo, lname As Last_Name, fname AS First_Name FROM Staff;
```

> [!TIP]- Output of `ALL` Example 1 without `WHERE`
>
> ```csv
> staffNo	Last_Name	First_Name
> SA9 	Howe	Mary
> SG14	Ford	David
> SG37	Beech	Ann
> SG5 	Brand	Susan
> SL21	White	John
> SL41	Lee 	Julie
> ```

#### Example: With `WHERE`

List the details of the staff whose salary is larger than the *salary* of **every** member from the branch `B003`.

```SQL
SELECT * FROM Staff
-- find the person from the list / table 'Staff'
-- where their salary is greater COMPARED to the people
-- working in `B003`
WHERE salary > ALL (
	SELECT salary FROM Staff
	WHERE branchNo = 'B003'
);
```

> [!TIP]- Output for `ALL` Example with `WHERE`
>
> ```csv
> staffNo	fname	lname	position	sex	DOB	salary	branchNo
> SL21	John	White	Manager	M	2045-10-01	30000	B005
> ```
>
> > [!NOTE]
> > The question did not ask for "*any*" member of the same branch, that is `B003`.
> > Instead, who is the staff that has the largest salary <span style="color: red;"> compared</span> to the *salaries* of the people at `B003`.

### Example: ANY / Some Keyword

Here are the csv output for table 'Staff'

```csv
staffNo	fname	lname	position	sex	DOB	salary	branchNo
SA9	Mary	Howe	Assistant	F	1970-02-19	9000	B007
SG14	David	Ford	Supervisor	M	1958-03-24	18000	B003
SG37	Ann	Beech	Assistant	F	1960-11-10	12000	B003
SG5	Susan	Brand	Manager	F	2040-06-03	24000	B003
SL21	John	White	Manager	M	2045-10-01	30000	B005
SL41	Julie	Lee	Assistant	F	1965-06-13	9000	B002
```

> I will be using the same example that I used above $\uparrow$

When we used the `ALL` keyword above $\uparrow$, it returned `SL21`. The staff with the `lname` of `John`. But why?

This is because it is comparing the values of `salary` from the branch `B003`. What I mean is that we have:

```csv
SG14	David	Ford	Supervisor	M	1958-03-24	18000	B003
SG37	Ann	Beech	Assistant	F	1960-11-10	12000	B003
SG5	Susan	Brand	Manager	F	2040-06-03	24000	B003
```

Here the biggest salary is `24000`. Hence, the `ALL` keyword compared it with the **largest** values.

#### Example: With `WHERE`

> [!INFO]
> I think we **cannot** use the `ANY` / `SOME` keyword without a sub-query.

> [!TIP] What is the meaning of `ANY` is SQL?
> From what I understand it will find most / any value that fit in a specific criteria.
> > Let's go the the example

```SQL
SELECT * FROM Staff
-- using the same example as above
-- in this case switched `ALL` with `ANY`
WHERE salary > ANY (
	SELECT salary FROM Staff
	WHERE branchNo = 'B003'
);
```

From our values;

```csv
SG14	David	Ford	Supervisor	M	1958-03-24	18000	B003
SG37	Ann	Beech	Assistant	F	1960-11-10	12000	B003
SG5	Susan	Brand	Manager	F	2040-06-03	24000	B003
```

It will found find the smallest value for `salary` from the branch `B003` ( *like the sub-query* ). Hence, in this case, the smallest value for `salary` is going to be `12000`.

Therefore, as **output**, we are going to get $\downarrow$:

```csv
staffNo	fname	lname	position	sex	DOB	salary	branchNo
SG14	David	Ford	Supervisor	M	1958-03-24	18000	B003
SG5	Susan	Brand	Manager	F	2040-06-03	24000	B003
SL21	John	White	Manager	M	2045-10-01	30000	B005
```

> Where we have found most / any of the staff; where their salary is greater than the minimum salary of the *sub-query*.

## EXISTS and NOT EXIST Keyword

> [!WARNING]
> They are <span style="color: red;"> <strong> only</strong> </span> used with sub-queries!!!

> [!TIP] Notes from Lecture Slides
>
> > These notes are found on page 33 on the lecture slide '[[Database Systems  - SQL ( DML - Part 2 ).pdf]'.
>
> - Produces a simple `true` / `false` *result*
> - `EXISTS` $\downarrow$:
> 	- `true` $\Rightarrow$ if and only if there exist **at least** one row in the table returned by the *sub-query*
> 	- `false` $\Rightarrow$ if the *sub-query* returns an **empty** result table

### Example of `EXIST` Keyword

```SQL
SELECT staffNo, lname as Last_Name, fname AS First_Name, position FROM Staff s
WHERE EXISTS (
	SELECT * FROM Branch b
	WHERE s.branchNo = b.branchNo
	AND city = 'London'
);
```

> [!TIP] Output of the `EXIST` Example
> This will be the output after running the above $\uparrow$ command:
>
> ```csv
> staffNo	Last_Name	First_Name	position
> SL21	White   	John    	Manager
> SL41	Lee     	Julie   	Assistant
> ```

> [!NOTE]
> This is similar to a simple `JOIN` statement
> Go to the file / note '[[SQL Commands - Data Manipulation Language - JOIN]'
> We are now going to convert the above $\uparrow$ SQL Command with the `EXIST` keyword to a simple *inner* ` JOIN` statement.
>
> ```SQL
> -- hence, "translated" to
> SELECT staffNo, lname as Last_Name, fname AS First_Name, position FROM Staff s, Branch b
> WHERE s.branchNo = b.branchNo
> AND city = 'London';
> ```
>
> Hence, this should return the same result!
>
> ```csv
> staffNo	Last_Name	First_Name	position
> SL21	White   	John    	Manager
> SL41	Lee     	Julie   	Assistant
> ```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!
