---
id: SQL Server - Cursor Status Function
aliases: SQL Procedural Programming Cursor's Status Function
tags:
  - uni
  - db
  - SQL
module: ICDT 1202Y
author: S.Sunhaloo
date: 2025-02-07
status: Completed
---

## List of Contents

- [[#What is Cursor Status?]]
  - [[#Syntax]]
  - [[#Return Types]]

---

> [!INFO] Resources
>
> - My Notes:
>   - [[SQL Procedural Programming - Cursors]]
>   - [[SQL Procedural Programming - Exception Handling]]
> - https://learn.microsoft.com/en-us/sql/t-sql/functions/cursor-status-transact-sql?view=sql-server-ver16
> - https://www.tutorialspoint.com/sql/sql-cursor-functions-cursor-status.htm

# What is Cursor Status?

So let's say that you created a `CURSOR`, right, right! If you want to get the "_status_" of it... You can use the `CURSOR_STATUS` Function.

> Fuck my life!

When the first that I encountered this very function is when I was doing the [[Database Systems - Labsheet 3 ( L1S2 )#Question 1 | Database Labsheet 3 Question 1].

Whereby, you had to create a [[SQL Procedural Programming - Embedded DML | Stored Procedure] that would display details about a student for a specific _user-entered_ year.

Now, after `OPEN`ing a Cursor, you obviously have to **close** it. But what if you have you little `BEGIN ... TRY` block and inside you have a nice `THROW` **exception**; if some type of error occurs.

Then obviously, the code will _immediately_ switch to the `BEGIN ... CATCH` block. But the Cursor might be still **opened**!

That is why we have the the following _code_ in our `BEGIN ... CATCH` block $\downarrow$:

```SQL
BEGIN CATCH
	-- catch and handle the exception
	PRINT 'Error: ' + ERROR_MESSAGE();
	PRINT 'Error Found at Line: ' + CAST(ERROR_LINE() AS VARCHAR(10));

	-- ensure the cursor is closed if it's still open
	IF CURSOR_STATUS('local', 'cur_disp_stud_mod') > = -1
	BEGIN
		CLOSE cur_disp_stud_mod;
		DEALLOCATE cur_disp_stud_mod;
	END;
END CATCH
```

In this case, even if any **exceptions** occurs; the `CURSOR_STATUS` function will check if the Cursor is still open, and if need be; close it.

## Syntax

> Below you will find the _creation_ of Cursor from Microsoft themselves!

```SQL
CURSOR_STATUS
     (
          { 'local' , 'cursor_name' }
          | { 'global' , 'cursor_name' }
          | { 'variable' , 'cursor_variable' }
     )
```

> [!NOTE]
> I am not going to go in-depth about things like `local` / `global`.
>
> If you have done programming even if its just `print("Fuck You!!!")`, then you should not that are _local_ / _global_ variables.
>
> > "_Amma leave at that_"

## Return Types

Let's go ahead and take a look at what **Return Value** that we get:

> Well, for more _comprehensive_ information please [click here](https://learn.microsoft.com/en-us/sql/t-sql/functions/cursor-status-transact-sql?view=sql-server-ver16#return-types)

| Return Values | Meaning ( In Short )                                                   |
| ------------- | ---------------------------------------------------------------------- |
| 1             | Cursor Variable is **Opened** and **Contains** _at least_ 1 **Record** |
| 0             | Cursor Variable Still **Opened** and _Result Set_ is **Empty**         |
| -1            | Cursor Variable **Closed** and _Result Set_ is **Empty**               |
| -2            | Not Applicable                                                         |
| -3            | Cursor _Name_ Specified is **NOT** Found                               |

> [!INFO]
> This is the reason that we have the line of $\downarrow$:
>
> ```SQL
> CURSOR_STATUS('local', 'cursor_name') > = -1
> ```
>
> It will be able to close the Cusor if the cursor either returns the **value** `1` or `0`!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!
