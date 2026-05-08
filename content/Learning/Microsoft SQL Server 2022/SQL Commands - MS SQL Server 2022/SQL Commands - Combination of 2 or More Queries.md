---
id: SQL Commands - Combination of 2 or More Queries
aliases: SQL UNION, INTERSECT, EXCEPT ( Difference )
tags:
  - SQL
  - uni
  - uom
  - db
module: ICDT 1202Y
author: S.Sunhaloo
date: 2024-09-27
status: Completed
---

> [!INFO]
> The Lecture Slides for this file / note is called '[[Database Systems  - SQL ( DML - Part 2 ).pdf]]' $\Rightarrow$ **Sub Queries** starts at page 12.
> This file / note is definitely related with this note $\rightarrow$ '[[SQL Commands - Data Manipulation Language - Sub Queries]]'
>
> But some other notes that could also be related are:
>
> - [[SQL Commands - Data Manipulation Language - JOIN]]

## List of Contents

- [[#Difference Between the Three Types]]
	- [[#SQL Syntax]]
	- [[#UNION]]

---

# Difference Between the Three Types

![[SQL - Commands - UNION, INTERSECT, EXCEPT.png | 600]]

> [!INFO]
> I will be referring to them as table '*R*' and table '*S*'!

# UNION

> As you know, it will take everything from the Venn Diagram ( *inside the "circles"* )

> [!TIP]- What is this `UNION` thing?
>
> > This was the bullet point from the lecture slide at page 35.
>
> A table containing all rows that are in **either** the *first* table 'R' **or** the *second* table 'S' **or** *both*.

## UNION Compatible

> [!WARNING]
> To be **union-compatible** $\Rightarrow$ They need to have the <span style="color: red;"> same</span> **structure**!

From that above $\uparrow$, it means that the 2 tables must contain **same**:

- Number of **Columns** ( *and not rows*! )
	- Each column must have the same:
		- Data Types
		- Length ( *like the `CHAR(4)` like the number '4'* )

> That, SQL does **not** no anything about that.
> It is **us** ( *the user* ) that has to check all of these!
>
> "*that the data values in the corresponding columns come from the same domain*".

---

> [!WARNING] Friendly Warning
> You can skip this part if you want to...
>
> > Read the `bug` note below $\downarrow$

## SQL Syntax - CORRESPONDING

```SQL
operator [ALL] [CORRESPONDING [BY {column1 [, ... ]}]
```

> Where `operator` are **set operators** like `UNION`, `INTERSECT`, `EXCEPT` / `MINUS`

> [!INFO] `ALL` Keyword
> If *typed*; if will **not** remove duplicate rows from the result!
> Example:
> - `UNION ALL` $\Rightarrow$ Return **with** *duplicated* rows
> - `UNION` ( *without `ALL`* ) $\Rightarrow$ Return *unique* rows **only**

> [!INFO] `CORRESPONDING` Keyword
> If *typed*; It matches **columns** by their *names*
> - Allowing set operations to be performed on columns with the **same** *name* across both result sets
>
> > [!WARNING]
> > The `CORRESPONDING` Keyword works only on the `UNION` set operator in SQL Server 2022!

### Example: `CORRESPONDING` Syntax

```SQL
-- cAr3Fu1
SELECT city, branchNo FROM Branch
UNION ALL CORRESPONDING BY city
SELECT city, propertyNo FROM PropertyForRent;
```

> [!BUG]- This Does **NOT** Work
> The keyword `CORRESPONDING` is part of SQL Standard *commands*...
> But [[Microsoft SQL Server 2022 Introduction | Microsoft SQL Server 2022]] has **not** implemented it...
> Hence, if you want to run the above $\uparrow$ statement; then the equivalent of it would be $\downarrow$:
>
> ```SQL
> SELECT city, branchNo 
> FROM Branch
> UNION ALL
> SELECT city, propertyNo 
> FROM PropertyForRent;
> ```
>
> You are going to have make sure that **both** queries select the **same** *columns*!
>
> > In our case it does!!!
>
> ```csv
> city    	branchNo
> Bristol 	B004
> London	    B005
> Aberdeen	B007
> Aberdeen	PA14
> Glasgow	    PG16
> ```
>
> > This is part of the output... The output if much much longer!

---

### Example of `UNION` Keyword

#### Without "`CORRESPONDING`"

Construct a list of all cities where there are **either** branch offices or a property.

```SQL
( SELECT city AS City FROM Branch
WHERE city IS NOT NULL )
UNION
( SELECT city AS City FROM PropertyForRent
WHERE city IS NOT NULL );
```

> [!TIP]- Output of Example for `UNION` keyword
>
> ```csv
> City
> Aberdeen
> Bristol
> Glasgow
> London
> ```

#### With "`CORRESPONDING`"

> Again please refer to the `bug` callout above $\uparrow$.

```SQL
( SELECT city AS City FROM Branch
WHERE city IS NOT NULL )
UNION ALL
( SELECT city AS City FROM PropertyForRent
WHERE city IS NOT NULL );
```

> [!TIP]- Output of Example for `UNION ALL` keywords
>
> ```csv
> City
> London
> Glasgow
> Bristol
> London
> Aberdeen
> Aberdeen
> Glasgow
> Glasgow
> Glasgow
> Glasgow
> London
> ```
>
> As you can see; it does **not** remove the duplicate values!

# INTERSECT

> As you know from mathematics, it will take what is in the **middle** of the Venn Diagram.

### Example of `INTERSECT` Keyword

#### Without "`CORRESPONDING`" Only!

```SQL
( SELECT city FROM Branch )
INTERSECT
(SELECT city FROM PropertyForRent );
```

> [!TIP]- Output of Example for `INTERSECT` keyword
>
> This should be the output after running the above $\uparrow$ statement:
>
> ```csv
> city
> Aberdeen
> Glasgow
> London
> ```

> [!NOTE]
> The the version of "*With `CORRESPONDING`*" meaning `INTERSECT ALL` is **not** available in SQL Server.
> Hence, only the statement above $\uparrow$ works and will give you the intersection **without** any duplicate values.

# EXCEPT / MINUS

> This will find the **difference** 

> [!BUG] The `MINUS` Keyword does **not** work in SQL Server 2022!

### Example of `EXCEPT` Keyword

#### Without "`CORRESPONDING`" Only!

```SQL
( SELECT city FROM Branch )
EXCEPT
( SELECT city FROM PropertyForRent );
```

> [!TIP]- Output of Example for `EXCEPT` keyword
>
> ```csv
> city
> Bristol
> ```


---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!