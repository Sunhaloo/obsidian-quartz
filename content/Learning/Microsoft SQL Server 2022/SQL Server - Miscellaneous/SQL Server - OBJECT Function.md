---
id: SQL Server - OBJECT Function
aliases: SQL Procedural Programming - OBJECT_ID Function
tags:
  - uni
  - uom
  - db
  - SQL
module: ICDT 1202Y
author: S.Sunhaloo
date: 2025-01-25
status: Completed
---

## List of Contents

- [[#The Object Identification Function]]
	- [[#Parts of the Function]]
	- [[#Usage]]
		- [[#Find the Object ID of an Object]]
		- [[#Find If Object Exists]]

---

> [!INFO] Resources
> - https://learn.microsoft.com/en-us/sql/t-sql/functions/object-id-transact-sql?view=sql-server-ver16
> - https://learn.microsoft.com/en-us/sql/relational-databases/system-catalog-views/sys-objects-transact-sql?view=sql-server-ver16&redirectedfrom=MSDN
> - https://learn.microsoft.com/en-us/sql/t-sql/language-elements/try-catch-transact-sql?view=sql-server-ver16#retrieve-error-information

# The Object Identification Function

Given that you have the code / function ( *from the documentation* ) below $\downarrow$:

```SQL
OBJECT_ID ( ' [ database_name . [ schema_name ] . | schema_name . ]
  object_name' [ , 'object_type' ] )
```

## Parts of the Function

As you can see in this `OBJECT_ID` function, we are passing in 2 parameters.

1. First Parameter
	- This is the **name** of the object that you are trying to *find*
2. Second Parameter
	- The *Object Type* that we are trying to search for

For the first parameter, this is pretty self explanatory while what should we place in the second parameter?

> Well, go read the fucking documentation... Second link in the *Resources Callout*
> By the way this is <strong> <span style="color: red;"> not</span> </strong> a joke. Please go ahead and read the documentation for the full specifications!

Nevertheless, for the most, we use these $\downarrow$ values for the **second** *parameter*:

- `U` $\Rightarrow$ User-Defined Tables
- `V` $\Rightarrow$ Views
- `C` $\Rightarrow$ Check Constraints
- `P` $\Rightarrow$ Stored Procedures

> Now, I think you know how to use the `OBJECT_ID` function... *Do I*?

## Usage

> As our lecturer did not show us how to use this function and I by myself is learning this function.
> I am going to take examples straight from the documentation ( *first link in Resource Callout* )

### Find the Object ID of an Object

Well as the name of the function suggests, we are able to find the *Object ID* from `OBJECT_ID`

```SQL
SELECT OBJECT_ID('sp_sum_even_cubes') AS 'Object ID';
```

If I run this command, I should get the *Object ID* for this [[SQL Procedural Programming - Introduction | Stored Procedure]]

```console
Object ID
658101385
```

Now what **error** will be shown to us if we don't have the *thing* that we are trying to find for...

> Let's fuck around and find out!
> *Computer Science as a whole* $\uparrow$

```SQL
SELECT OBJECT_ID('big_shitter') AS 'Object ID';
```

```console
Object ID
NULL
```

> ["*Impressive*"](https://www.youtube.com/watch?v=cISYzA36-ZY&t=138)

### Find If Object Exists

> This is what we are mostly going to be using it for!

In this case, let's check that the Stored Procedure `sp_sum_even_cubes` **exists** and then output some appropriate message and then `DROP` / *delete* the Stored Procedure.

```SQL
-- declaration and initialisation of variables
DECLARE @object_name VARCHAR(50) = 'sp_sum_even_cubes';

-- check whether the stored procedure exists
-- in this case we are assuming that the stored procedures does not exist
IF OBJECT_ID(@object_name, 'P') IS NULL
BEGIN
	-- ouput appropriate message
	PRINT 'The Stored Procedure Does NOT Exists!'
END
-- if the stored procedures is still here
ELSE
BEGIN
	-- ouput appropriate messages
	PRINT 'The Stored Procedure Exists! Deleting Stored Procedure'
	
	-- drop / delete the stored procedure using dynamic SQL
	DECLARE @sql NVARCHAR(MAX) = 'DROP PROCEDURE ' + @object_name;
	-- execute the program *inline*
	EXEC sp_executesql @sql;
	
	-- output confirmation message
	PRINT 'The Stored Procedure Has Been Deleted!'
END
```

> I accidentally ran the program without considering that I needed to place the output...

Running the "*program*" above $\uparrow$, in my case, I am going to get $\downarrow$:

```console
The Stored Procedure Does NOT Exists!
```

> [!NOTE]
> Even here, I would still use the `BEGIN ... END` keyword even if we had **only one** statement *inside*!

> [!WARNING]
> I know **nothing** about Dynamic SQL. So when I first initially wrote the code above $\uparrow$, I place the *name* of Stored Procedures directly inside the `OBJECT_ID` function.
> Then my programming brain kicked in and said that I would have to replace the *name* of *an object* **twice** as we need to change the object name in the parameter and in the `DROP` command.
>
> Hence, this is why I **declared** a variable `@object_name` so that we can only write the name **once** and move on with our life.
> But simply writing `DROP PROCEDURE @object_name` did <strong> <span style="color: red;"> not</span> </strong> work.
>
> Therefore, I asked [ChatGPT](https://chat.openai.com) about it and it gave me this. Basically what I am trying say is that I was trying to "*automate*" the process; but I did lacked knowledge... This is called a **Skill Issue** in the profession.

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!