---
id: SQL Server - INSERTED and DELETED Tables
aliases: SQL Server Triggers ( INSERTED and DELETED ) Tables
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

- [[#What are these Tables?]]
	- [[#But What's Their Purpose]]

---

> [!WARNING]
> This note is just an theoretical overview of 'INSERTED' and 'DELETED' tables.
> If you want to learn more about the nitty - gritty details, I suggest:
>
> - https://learn.microsoft.com/en-us/sql/relational-databases/triggers/use-the-inserted-and-deleted-tables?view=sql-server-ver16
> - https://dotnettutorials.net/lesson/magic-tables-in-sql-server/

# What are these Tables?

Similar to the things like 'sys.tables' and 'sys.procedures'. We have the built-in table 'INSERTED' and 'DELETED'.

## But What's Their Purpose

> To be honest with you, I don't actually know the real purpose of meaning of these tables...

### Purpose of INSERTED Table

But lets say that you run the command:

```SQL
-- insert command
INSERT INTO table_name ( field_1, field_2, field_3, ... ) VALUES ( value_1, value_2, value_3 );
```

Well, in this will **insert** this $\uparrow$ record in the table 'table_name'... *Obviously*!

Now, when you do run this command... It will also **populate** the table 'INSERTED'.

### Purpose of DELETED Table

Similarly, if you where to do something like $\downarrow$:

```SQL
-- delete record
DELETE table_name
WHERE search_condition;
```

Again, yes your record will be **deleted** from the table 'table_name'. But also it will **populate** the table 'DELETED'

#### But what if you run the 'UPDATE' Command?

As you know ( *apparently I completely missed this... Thanks Rayyan* ), an `UPDATE` statement is simply composed of and `DELETE` and `INSERT` statement

This is why we **don't** have an 'UPDATED' table because there is *no* need for it.

```mermaid
graph LR
	A[UPDATE] --> B[DELETE]
	B[DELETE] --> C[INSERT]
```

In the case for the `UPDATE` command, it will **first** *populate* the 'DELETED' table and then *populate* the 'INSERTED'.

> [!INFO] Characteristics of These Tables
> - The can **neither** be changed nor updated
> - They can only store **1** record
> 	- That is the *previous* record

# Quirks and Features

## Getting Values into Variables

**Both** the 'INSERTED' and 'DELETED' table can have multiple rows / records when either `INSERT`, `DELETE` or `UPDATE` *event*. Hence, it is **recommended** that we *initialise* our variables like so $\downarrow$:

```SQL
-- declaration of variables
DECLARE @var_1 DATATYPE;
DECLARE @var_2 DATATYPE;

-- get the value from 'INSERTED' table
SELECT @var_1 = value_1 FROM INSERTED;

-- get the value from 'DELETED' table
SELECT @var_2 = value_2 FROM DELETED;
```

In this case, both *variables* will have **a single** value in them.

> Similar to what we have been doing over [[SQL Procedural Programming - Embedded DML#Example 3 Use Multiple Variables IN the SELECT Command | here]!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!