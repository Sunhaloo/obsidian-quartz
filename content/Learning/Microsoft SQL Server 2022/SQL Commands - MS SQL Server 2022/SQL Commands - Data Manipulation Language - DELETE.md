---
id: SQL Commands - Data Manipulation Language - DELETE
aliases:
  - SQL Commands - DML ( The DELETE Statement )
tags:
  - SQL
  - uni
  - db
author: S.Sunhaloo
date: "2024-08-31"
status: Completed
---

> [!INFO]
> The Lecture Notes / Slides are found in "[[Database Systems - SQL ( DML - Part 1 ).pdf]".
> The _sub-heading_ for the `DELETE` statement starts at page 15.

## List of Contents

- [[#The Delete Command]]
  - [[#General Template for DELETE Command]]
    - [[#Example]]
      - [[#DELETE A Single Record]]
      - [[#Delete Everything in a Table]]

---

> [!WARNING]
> Similar to [[SQL Commands - Data Manipulation Language - UPDATE | `UPDATE`]  v/s [[SQL Commands - Data Definition Language ( DDL )#Alter Command| `ALTER`]]
>
> The `DELETE` command will delete / remove **values** that is found _inside_ of a table and **not** `DROP` the actual table.
> Notes for `DROP` command can be found [[SQL Commands - Data Definition Language ( DDL )#Drop Columns WITH Constraints| here]]

# The Delete Command

> So let's start!

## General Template for DELETE Command

```SQL
DELETE table_name
WHERE search_condition;
```

## Example

### DELETE A Single Record

We are going to remove a **single** record from the table 'StaffPropCount'

> If you don't know where we got this table.
> Please review and refer to the '[[SQL Commands - Data Manipulation Language - INSERT]'; where I was talking about the [[SQL Commands - Data Manipulation Language - INSERT#Inserting Data with SELECT Statement / Command | `INSERT... SELECT`] command.

> [!INFO] Here are the values from the 'StaffPropCount' Table
> The contents / values for the table currently includes $\downarrow$:
>
> ```csv
> staffNo	fname	lname	propCount
> SA9	    Mary	Howe	1
> SG14	David	Ford	1
> SG37	Ann	Beech	    2
> SG5	    Susan	Brand	0
> SL21	John	White	0
> SL41	Julie	Lee	    1
> ```

We are going to remove the record where the `staffNo` is 'SG5'!

Hence, we are going to have to run the something like this $\downarrow$:

```SQL
DELETE StaffPropCount
-- our search condition ==> delete a single record
WHERE staffNo = 'SG5';
```

> [!TIP]- Verification of Removal of Record
> To check if the record we wanted gone... is _gone_. We can use the following statements:
>
> ```SQL
> -- first command
> SELECT * FROM StaffPropCount;
> -- second command
> SELECT * FROM StaffPropCount
> WHERE staffNo = 'SG5';
> ```
>
> > I will be running the first command.
>
> Hence, our output should be something like:
>
> ```csv
> staffNo	fname	lname	propCount
> SA9	    Mary	Howe	1
> SG14	David	Ford	1
> SG37	Ann	Beech	    2
> SL21	John	White	0
> SL41	Julie	Lee	    1
> ```

### Delete Everything in a Table

Now, instead of deleting a **single** record; we are now going to remove **all** _values_ from the table.

This is actually so simple to do that it is almost dangerous to do!

```SQL
-- remove all values from a table
DELETE StaffPropCount
```

> [!TIP]- Verification of Removal of Data from Table
> Hence, we should have not even a single piece of data that is in our table.
>
> ```SQL
> SELECT * FROM StaffPropCount;
> ```
>
> > This will return **nothing**!
>
> ```csv
> staffNo	fname	lname	propCount
> ```

> [!WARNING]
> Again, this will <span style="color: red;"> <strong> not</strong> </span> delete the _table_.
> _Again_ and fucking _again_, if you want to delete the table; use the `DROP` command.
>
> ```SQL
> DROP TABLE StaffPropCount;
> ```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!
