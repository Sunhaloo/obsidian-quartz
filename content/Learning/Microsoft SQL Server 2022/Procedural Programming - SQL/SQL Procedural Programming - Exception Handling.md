---
id: SQL Procedural Programming - Exception Handling
aliases: SQL Procedural Programming TRY ... CATCH
tags:
  - uni
  - uom
  - db
  - SQL
module: ICDT 1202Y
author: S.Sunhaloo
date: 2025-01-24
status: Completed
---

## List of Contents

- [[#Exception Handling in SQL Server]]
	- [[#General Template]]
	- [[#Raising the Exception]]
		- [[#General Template for THROWing Exceptions | General Template for THROW]]
			- [[#Error Numbers - Codes and Description]]
			- [[#Value for State]]
	- [[#Usage]]

---

> [!INFO] Resources
> - https://learn.microsoft.com/en-us/sql/t-sql/language-elements/try-catch-transact-sql?view=sql-server-ver16
> - https://www.sqlshack.com/how-to-implement-error-handling-in-sql-server/

# Exception Handling in SQL Server

## General Template

```SQL
CREATE PROCEDURE sp_procedure_name
	-- our parameter
	@param_1 DATATYPE,
	@param_2 DATATYPE
AS
BEGIN
	-- exception handling
	-- this is just like the `try` part in Python
	BEGIN TRY
		-- statements
		
		-- some condition
		BEGIN
			-- raise en exception
			THROW ERROR_NUMBER, 'MESSAGE', STATE;
		END
		
		-- statements
		
	END TRY
	
	-- catch the exception
	-- this is just like the `try` part in Python
	BEGIN CATCH
		-- messages / output things goes here
	END CATCH
END
```

### Example from Documentation

> In my 2 celled brain, I think placing this here will make sense

This is the **first** example that Microsoft gave us... I need this because I think that these *functions* ( *see in the code* ) will be important to me.

```SQL
-- Verify that the stored procedure does not already exist.
IF OBJECT_ID('usp_GetErrorInfo', 'P') IS NOT NULL
    DROP PROCEDURE usp_GetErrorInfo;
GO

-- Create procedure to retrieve error information.
CREATE PROCEDURE usp_GetErrorInfo
AS
SELECT ERROR_NUMBER() AS ErrorNumber,
    ERROR_SEVERITY() AS ErrorSeverity,
    ERROR_STATE() AS ErrorState,
    ERROR_PROCEDURE() AS ErrorProcedure,
    ERROR_LINE() AS ErrorLine,
    ERROR_MESSAGE() AS ErrorMessage;
GO

BEGIN TRY
    -- Generate divide-by-zero error.
    SELECT 1 / 0;
END TRY

BEGIN CATCH
    -- Execute error retrieval routine.
    EXECUTE usp_GetErrorInfo;
END CATCH;
```

> [!WARNING]
> These functions $\uparrow$ like: `ERROR_NUMBER()`, `ERROR_MESSAGE()`, `ERROR_LINE()` and the others can **only and only** be used in the `BEGIN CATCH ... END CATCH` block.
>
> > Again, they **cannot** be use elsewhere!!!
>

## Raising the Exception

Well, if you take a look at the official Microsoft Documentation ( *first link in the Resources Callout* ), you are not going to see things that we *beginners* will actually use. Instead you are going to the **proper** / *more complicated* way of doing things.

> This is why I am making this note is because
> the way I used it in the [[Test#Question 2| Database Labsheet 1 ( L1S2 )] was **not** like the documentation

To raise an exception in *Python*, we use the `raise` keyword. But in SQL, we can `THROW` that shit!

### General Template for THROWing Exceptions

```SQL
THROW ERROR_NUMBER, 'MESSAGE', STATE;
```

But how are we going to find about what *Error Number* to choose and what *State* to choose. Because your's truly did his research you can find it below $\downarrow$

#### Error Numbers - Codes and Description

| Error Number | Scenario | Description |
| ------------ | -------- |----------- |
| 50000 | General Exception | Similar to Python's `except Exception:` |
| 50001 | Data Validation Error | Invalid data or missing required input |
| 50002 | Input Format Error | Invalid Format or Type |
| 50003 | Business Logic Violation | Violation of business rules or constraints |
| 50004 | Record Not Found | Data not found for a given identifier |
| 50005 | Duplicate Data Error | Attempt to insert a duplicate value where not allowed |
| 50006 | Permission Denied | User lacks sufficient permissions for an action |
| 50007 | Dependency Error | Error caused by missing or unavailable dependencies |
| 50008 | Operation Timeout | A query or operation timed out before completion |

#### Value for State

Well the *first* thing to know is that its **mandatory** and the *second* thing is that the value for `STATE` has a range of **1** - **255**.

Now, the thing about the state is that you can **choose** whatever the fuck you want from that *range*.
But it is generally considered good practice to change the number if you have for example *Data Validation Error* where we use the *state value* of '1' and we use '2' for *Input Format Error*.

Therefore when we are going to **debug** our program if any error occurred... We can easily see that is the error has we have planned ahead with our *State Values*!

## Usage

### Example 1: Some Simple THROWs

Given that you have this *block* of code below $\downarrow$:

```SQL
-- raise some general exceptions
THROW 50000, 'General Exception has Been Raised!!!', 1;
THROW 50000, 'See how I continue to use a State Value of 1', 1;

-- raise input format error
THROW 50002, 'Input Format Error Exception has Been Raised!!!', 2;
-- raise permisson error
THROW 50006, 'Permission Denied Exception has Been Raised!!!', 2;
```

If you were to run this very code block, you are going to see the message of:

```console
Msg 50002, Level 16, State 2, Line 6
Input Format Error Exception has Been Raised!!!
```

> This will be shown in <span style="color: red;"> red</span> BTW!

Now you might be saying: "*Well this is **not** how it should have ran*"... Like it should display all the exceptions all at once.

> This is where you are **very wrong**!

The code above $\uparrow$ works as intended and its doing its job well. In most, programming languages when you are going to *raise* or "*receive*" an exception from the program and you **don't** have your `TRY` and `CATCH` ( _not in the **Python Interpreter**_ ).

Therefore, this is what to be expected as, when SQL will interpret the line of code. It will see that the current line is raising an exception ( *or what normies call it... Error* ) and it will **halt** the *program* immediately.

### Example 2: Mimic `ValueError` from Python

Let's go ahead and create a simple procedure that will accept a **value** from a user and checks if its really a number.

```SQL
CREATE PROCEDURE sp_ValueError
	-- take user input as a parameter
	@user_input NVARCHAR(10)
AS
BEGIN
	-- exception handling
	BEGIN TRY
		-- try to convert data entered by user into a float value / datatype
		DECLARE @user_num FLOAT = TRY_CAST(@user_input AS FLOAT);

		-- if we could NOT convert the user's input into a number
		IF @user_num IS NULL
		BEGIN
			-- meaning that user did not initially entered a "number" value
			-- raise an exception
			THROW 50002, 'User did not Enter a Number Value!!!', 1;
		END
		ELSE
		BEGIN
			-- user did enter a "number" value
			PRINT 'Nicely Done! Number Entered: ' + CAST(@user_num AS VARCHAR(10));
		END
	END TRY

	BEGIN CATCH
		-- catch and handle the error
		PRINT 'Error: ' + ERROR_MESSAGE();
	END CATCH
END
```

#### Running the Program

##### Input is NOT a Number

```SQL
EXEC sp_ValueError @user_input = 'Bruh'
```

```console
Error: User did not Enter a Number Value!!!
```

##### Input is a Number

```SQL
EXEC sp_ValueError @user_input = '6.9'
```

```console
Nicely Done! Number Entered: 6.9
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!