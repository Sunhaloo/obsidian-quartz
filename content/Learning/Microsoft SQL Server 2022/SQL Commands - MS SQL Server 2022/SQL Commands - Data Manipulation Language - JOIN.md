---
id: SQL Commands - Data Manipulation Language - JOIN
aliases: SQL Commands - DML ( JOINs )
tags:
  - SQL
  - uni
  - db
author: S.Sunhaloo
date: 2024-09-19
status: Completed
---

> [!INFO]
> The Lecture Slides for this file / note is called '[[Database Systems - SQL ( DML - Part 2 ).pdf]' $\Rightarrow$ `JOIN`s starts at page 21.

## List of Contents

- [[#What is a JOIN?]]
  - [[#Types of JOIN]]
    - [[#INNER JOIN]]
    - [[#LEFT OUTER JOIN]]
    - [[#RIGHT OUTER JOIN]]
    - [[#FULL OUTER JOIN]]

---

# What is a JOIN?

It is an operation that allows for the **combination** _row_ from 2 or more **tables**.

# Types of JOIN

## INNER JOIN

> [!TIP]
> Return **only** rows where there is a match in **both** tables

### Examples of INNER JOIN

#### Example: Without `=`

```SQL
SELECT Client.clientNo, lname AS Last_Name, fname AS First_Name, propertyNo, comment FROM Client
INNER JOIN Viewing ON Client.clientNo = Viewing.clientNo;
```

##### Outputs

```csv
clientNo	Last_Name	First_Name	propertyNo	comment
CR56	Stewart	Aline	PA14	too small
CR56	Stewart	Aline	PG36	NULL
CR56	Stewart	Aline	PG4	NULL
CR62	Tregear	Mary	PA14	no dining room
CR76	Kay	John	PG4	too remote
```

#### Example: With `=`

What we wrote above $\uparrow$ can be simplified to this:

```SQL
SELECT Client.clientNo, lname AS Last_Name, fname AS First_Name, propertyNo, comment FROM Client, Viewing
-- because by by default
-- it is an inner join
WHERE Client.clientNo = Viewing.clientNo;
```

##### Same Output

```csv
clientNo	Last_Name	First_Name	propertyNo	comment
CR56	Stewart	Aline	PA14	too small
CR56	Stewart	Aline	PG36	NULL
CR56	Stewart	Aline	PG4	NULL
CR62	Tregear	Mary	PA14	no dining room
CR76	Kay	John	PG4	too remote
```

> [!NOTE]
> By **default** a `JOIN` is _inner_. To make it an _outer_ join, we need to specify the `LEFT` `RIGHT`, etc.

---

> [!TIP]
> With **outer**, we are table to all output the rows that are **not** _matched_ in **both** tables.

> To understand the types of _outer_ joins, we are going to use Venn Diagrams.

## LEFT OUTER JOIN

![[Left Outer Join - Venn Diagram.png]]

> Think of it as giving priority to the **left** table

### Example: `LEFT JOIN`

List all _branch office_ and any _properties_ that are in the same city.

```SQL
SELECT Branch.branchNo, Branch.city, PropertyForRent.propertyNo, PropertyForRent.city FROM Branch
LEFT JOIN PropertyForRent ON Branch.city = PropertyForRent.city;
```

```csv
branchNo	city	propertyNo	city
B002	London	PL94	London
B003	Glasgow	PG16	Glasgow
B003	Glasgow	PG21	Glasgow
B003	Glasgow	PG36	Glasgow
B003	Glasgow	PG4	Glasgow
B004	Bristol	NULL	NULL
B005	London	PL94	London
B007	Aberdeen	PA14	Aberdeen
```

> [!INFO]
> As you can see, we have a record / row that is `NULL`.
> Because these _values_ does not exists in the table 'PropertyForRent'

## RIGHT OUTER JOIN

![[Right Outer Join - Venn Diagram.png]]

### Example: `RIGHT JOIN`

List all _branch office_ and any _properties_ that are in the same city.

> We are "_flipping_" the condition around

```SQL
SELECT Branch.branchNo, Branch.city, PropertyForRent.propertyNo, PropertyForRent.city FROM Branch
RIGHT JOIN PropertyForRent ON Branch.city = PropertyForRent.city;
```

```csv
branchNo	city	propertyNo	city
B007	Aberdeen	PA14	Aberdeen
B003	Glasgow	PG16	Glasgow
B003	Glasgow	PG21	Glasgow
B003	Glasgow	PG36	Glasgow
B003	Glasgow	PG4	Glasgow
B002	London	PL94	London
B005	London	PL94	London
```

## FULL OUTER JOIN

![[Full Outer Join - Venn Diagram.png]]

> This one take every value ( _from what I understand_ )

### Example: `FULL JOIN`

List the branch offices and properties that are in the same city along with any unmatched branches or properties.

```SQL
SELECT Branch.branchNo, Branch.city, PropertyForRent.propertyNo, PropertyForRent.city FROM Branch
FULL JOIN PropertyForRent ON Branch.city = PropertyForRent.city;
```

```csv
branchNo	city	propertyNo	city
B002	London	PL94	London
B003	Glasgow	PG16	Glasgow
B003	Glasgow	PG21	Glasgow
B003	Glasgow	PG36	Glasgow
B003	Glasgow	PG4	Glasgow
B004	Bristol	NULL	NULL
B005	London	PL94	London
B007	Aberdeen	PA14	Aberdeen
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!
