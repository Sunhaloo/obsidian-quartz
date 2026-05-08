---
id: SQL Commands - Data Manipulation Language - GROUP BY and HAVING
aliases: SQL Commands - DML ( SELECT ---> GROUP BY and HAVING )
tags:
  - SQL
  - uni
  - db
  - uom
author: S.Sunhaloo
date: 2024-09-05
status: Completed
---

> [!INFO]
> This is actually part of the file / note [[SQL Commands - Data Manipulation Language - SELECT]]
> These notes are found in the "[[Database Systems  - SQL ( DML - Part 2 ).pdf]".
> Here is another file: "[[SQL Commands - Data Manipulation Language - Aggregate Functions]"
>
> Why is this file here?
>
> Because I used commands that are found here in there $\uparrow$; **before** making this note / file.

## List of Contents

- [[#Grouping]]
	- [[#The Group By Clause]]
		- [[#Examples of GROUP BY]]
- [[#Having]]
	- [[#The Having Clause]]
		- [[#Examples of HAVING]]

---

# Grouping

## The Group By Clause

> [!TIP] Lecturer's Notes
> `GROUP BY` groups the data from the `SELECT` <u> table(s)</u> ( *I don't really understand this* ) and produces  a **single** summary row for each group.
>
> - Each item in `SELECT` list must be **single-valued** *per group*, and `SELECT` clause may only contain:
> 	- field / column / attribute names
> 	- [[SQL Commands - Data Manipulation Language - Aggregate Functions| aggregate functions]]
> 	- constants
> 	- expressions involving the combinations of the above $\uparrow$
> - All column names in `SELECT` list must appear in `GROUP BY` clause unless *name* is used only in aggregate functions
> 	- Basically what the Lecturer was trying to say is that:
> 		- If you do **have** a "*normal*" ( non-aggregate ) field that **needs** to be displayed *alongside* with an aggregate function; we <span style="color: red;"> WILL</span> need to use the `GROUP BY` clause
> 		- Else no need if you only have either:
> 			1. *Selects* full list of non-aggregate fields
> 			2. *Selects* full list of aggregate functions
> - "*ISO*" ( _or **SQL Standard ( ISO / IEC )**_ ) considers two `NULLS` to be equal for purposes of `GROUP BY`
>
> > [!WARNING]
> > If `WHERE` is used with the `GROUP BY` clause; `WHERE` is applied <span style="color: green;"> <strong> first</strong> </span> .
> > Hence, the *groups* are formed from the remaining rows satisfying the predicate.
>

---

> I did not understand shit!!!
> Like what is it even talking about.
>
> Nevertheless, I placed the last point in a <span style="color: orange;"> warning</span> because I always do this mistake.

---

> [!INFO]
> I will be taking examples for the Lecture Slides.
>
> > Obviously, I don't agree to everything that the Lecturer wrote; hence, I will be changing some stuff

### Examples of GROUP BY

#### Example: Errors!!!

Remember how we were talking about things like: "*you need to have `GROUP BY` if you have a non-aggregate and an aggregate field in a `SELECT` statement*"?

We are now going to prove this $\downarrow$

Let's take the first

```SQL
-- selecting non-aggregate field together with aggregate field
SELECT branchNo, COUNT(staffNo) AS Staff_COUNT, SUM(salary) AS Total_Salary FROM Staff
```

> This should return an Error that looks something along the lines of:

> [!BUG]- Error
> ```console
> Column 'Staff.branchNo' is invalid in the select list
> because it is not contained in
> either an aggregate function
> or the GROUP BY clause.
> ```

##### Correction of the above $\uparrow$ code

```SQL
-- selecting non-aggregate field together with aggregate field
SELECT branchNo, COUNT(staffNo) AS Staff_COUNT, SUM(salary) AS Total_Salary FROM Staff
-- need to use GROUP BY clause
-- NOTE: DO NOT add ',' character after writing group by
GROUP BY branchNo
-- in this case, we have also "ordered" the output by 'ascending'
ORDER BY branchNo;
```

> [!SUCCESS]
> This should return our results $\downarrow$
>
> ```csv
> branchNo	Staff_COUNT	Total_Salary
> B002	1	9000
> B003	3	54000
> B005	1	30000
> B007	1	9000
> ```

> [!TIP] Takeaways
>
> > Not the thing that they give you after you ask for more "*briani*" in weddings.
> > Fuck those people! Why not... *Fuck Society*!
>
> 1. `GROUP BY` only takes the non-aggregate functions as arguments.
> 2. There is not trailing commas as the end of the `GROUP BY` statement.
>
> 	```SQL
> 	-- WRONG!!!
> 	GROUP BY col1, col2, col3...,
> 	-- GOOD
> 	-- no trailing ',' character
> 	GROUP BY col1, col2, col3...
> 	```

#### Examples: Multiple Non-Aggregate Fields

Similar to above ( *and also what we have been saying* ); we are going to place all the fucking "*normal*" attributes in the `GROUP BY` clause.

```SQL
SELECT branchNo, staffNo, COUNT(*) Staff_COUNT FROM PropertyForRent
-- adding all the non-aggregate fields
GROUP BY branchNo, staffNo
ORDER BY branchNo, staffNo;
```

> [!TIP]- Output of `GROUP BY` with **Multiple** Non-Aggregate Fields
>
> ```csv
> branchNo	staffNo	Staff_COUNT
> B003	NULL	1
> B003	SG14	1
> B003	SG37	2
> B005	SL41	1
> B007	SA9 	1
> ```

#### Example: Group By with Where Clause

> As we have said again in the <span style="color: orange;"> warning</span> ;
> We need to first write the `WHERE` clause "*statement*"; thus, they will be "grouped" on the `WHERE` condition
> If that makes sense.

```SQL
SELECT staffNo, COUNT(*) AS Staff_COUNT FROM PropertyForRent
-- as you can see the 'WHERE' clause comes first
-- NOTE: here also we don't need to add the ',' character
WHERE staffNo IS NOT NULL
GROUP BY staffNo;
```

> [!TIP]- Output of `GROUP BY` with `WHERE`
> Here are the results after running the above $\uparrow$ command:
>
> ```csv
> staffNo	Staff_COUNT
> SA9	1
> SG14	1
> SG37	2
> SL41	1
> ```

---

# Having

> What are you having for ( *insert something here* )

> [!TIP] Explanation
> Okay, now we have been able to display the non-aggregate columns with the *built-in* functions.
> I now have a question... "*How can we classify the aggregate functions*?"
> This is where the `HAVING` clause comes into play
>
> With **aggregate** functions, we cannot simply use the `WHERE` clause to perform something like this:
>
> > [!BUG] Wrong!!!
> > ```SQL
> > -- did I mention that this is wrong?
> > SELECT COUNT(staffNo) AS Staff_COUNT FROM Staff
> > -- you CANNOT do this!!!
> > WHERE COUNT(staffNo) > 1;
> > ```
> > 
> > This is the output that you are going to get $\downarrow$:
> > ```console
> An aggregate may not appear in the WHERE clause
> unless it is in a subquery contained in a
> HAVING clause or a select list,
> and the column being aggregated is an outer reference.
> > ```



> [!NOTE]
> You could say that the note / file '[[SQL Commands - Data Manipulation Language - Aggregate Functions]' is related to the `HAVING` clause.

## The Having Clause

### Examples of HAVING

#### Example: Simple Example Without `GROUP By`

> Using *my* example for above
> [So that was a fucking lie](https://www.youtube.com/watch?v=G4Uw3m_dPpw); Yes, I normally create my own examples!
> Nevertheless, this is a really *shitty* example, because the output is *shit*.
> But just know that it works with `HAVING`

```SQL
-- did I mention that this is right?
SELECT COUNT(staffNo) AS Staff_COUNT FROM Staff
-- you CAN do this!!!
HAVING COUNT(staffNo) > 1;
```

> [!TIP]- Output of the Shittiest Example
> Here is the shittiest result that I have ever seen $\downarrow$:
>
> ```csv
> Staff_COUNT
> 6
> ```

#### Example: `GROUP BY` with `HAVING`

```SQL
SELECT branchNo, COUNT(staffNo) AS Staff_COUNT, SUM(salary) AS Total FROM Staff
-- grouping because of non-aggregate function
-- again we do NOT add trailing commas
GROUP BY branchNo
-- satisfy the condition
-- using having because its a aggregate function
HAVING COUNT(staffNo) > 1
-- just ordering `branchNo` in ascending order
ORDER BY branchNo;
```

> [!TIP] Output of `GROUP BY` together with `HAVING`
>
> > This is a "*real*" example from the Lecture Slides
>
> ```csv
> branchNo	Staff_COUNT	Total
> B003	3	54000
> ```
>
> > [!NOTE]
> > If the output does **not** look like what is on page 8 in the Lecture Slides...
> > This is because I think I updated the data for the table Staff look like what is on page 8 in the Lecture Slides...
> > Again "*I think*"... Don't Judge!

---

> [!SUCCESS]
> We have completed `GROUP BY` and `HAVING` in a single sitting!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!
