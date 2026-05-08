---
id: SQL Procedural Programming - Introduction
aliases: Mircrosoft SQL Server PL/SQL Introduction
tags:
  - uni
  - uom
  - db
  - SQL
module: ICDT 1202Y
author: S.Sunhaloo
date: 2025-01-22
status: Completed
---

## List of Contents

- [[#Difference Between SQL Queries and Stored Procedures]]
- [[#Benefits of SQL Stored Procedures]]
- [[#The Actual Code Writing]]
	- [[#Before We Start]]
	- [[#Create Procedures]]
		- [[#Running the Stored Procedure]]
	- [[#Casting]]
	- [[#Output Parameters]]
	- [[#IF Statements]]
	- [[#WHILE Statements]]
	- [[#ALTER Procedure]]
	- [[#DROP Procedure]]
	- [[#Examples]]
		- [[#Example 1]]
		- [[#Example 2]]
		- [[#Example 3]]

---

# Some Questions

> I will only be including links where you can go read it on your own
> We are not really interested in knowing the specific details of this *type* of Programming

> [!INFO] What is Procedural Programming?
> - https://en.wikipedia.org/wiki/Procedural_programming
>
> As we are using [[Microsoft SQL Server 2022 Data View | Microsoft SQL Server], we need to understand that different [[Database Systems - Relational Model | relational database model] uses different types of "*special syntax*"
> Hence, in our case we are going to use the [Transact SQL](https://en.wikipedia.org/wiki/Transact-SQL) whereby is expand on the basic SQL commands and includes things like:
>
> 1. Local Variables
> 2. Functions
> 3. Basic Maths Operations and Functions
> 4. Conditions and Loops
>
> > Basically, what I am trying to say is that we are going to be using something that is proprietary to Microsoft and will not work on, for example, [PostgreSQL](https://www.postgresql.org/)!

> [!INFO] What is Stored Procedure?
> - https://en.wikipedia.org/wiki/Stored_procedure

# Difference Between SQL Queries and Stored Procedures

| SQL Queries | SQL Stored Procedures |
| ----------- | --------------------- |
| Small, Simple "*Code*" for One Time Operations | Large, Complex ( *actual* ) Code for Reuse |
| Need to compiled **everytime** | Only compiled **once**; can be executed many times |
| **No** ability to pass Parameters | **Ability** to pass Parameters |
| Does **not** contain Programming Constructs | **Contains** Programming Constructs like `IF`, `WHILE`, `AND`... |
| Exceptions **cannot** be catched and Raised | Exceptions **can** be catched and Raised |  

> [!NOTE] Ask ChatGPT to provide more differences!

# Benefits of SQL Stored Procedures

1. Reduced Server / Client Network Traffic
	- Stored as an "**Object**" ( *Similar to a Table $\Rightarrow$ In the Database Itself* )
	- SQL Commands are executed as a **Single Batch** of code
	- Only the `EXEC sp_stored_procedure_name` command is sent across network instead of all lines of code in SQL Query
2. [Stronger Security](https://learn.microsoft.com/en-us/sql/relational-databases/stored-procedures/stored-procedures-database-engine?view=sql-server-ver16#stronger-security)
	- Ability to perform operations in **underlying** database
		- This can be done my multiple users / clients **without** the need of direct access to Database Server
		- This is done using `EXECUTE AS` clause which allows for *impersonation* of another user
	- Only the `EXEC` call is passed over the network
		- Meaning attackers / hackers does not know that the tables, database objects are
	- Procedure Parameters safeguards against [SQL Injection Attacks](https://en.wikipedia.org/wiki/SQL_injection)
		- This is because **parameters** are treated as *literal values* and **not** as *executable code*
3. Reuse of Code
	- Repetitious Code can be encapsulated in a Store Procedures
	- Does not waste time writing the same SQL Queries / Codes
4. [Easier Maintenance](https://learn.microsoft.com/en-us/sql/relational-databases/stored-procedures/stored-procedures-database-engine?view=sql-server-ver16#easier-maintenance)
5. Improved Performance
	- Compiled at **first** Run $\Rightarrow$ Creates an *execution plan* that is reused
	- Massive changes made by the Procedure might make it run slower $\Rightarrow$ Just need to recompile or Change Execution Plan

# The Actual Code Writing

## Before We Start

> There is always some things to say before doing "*a*" main thing!

In SQL Server and in [[Microsoft SQL Server 2022 Introduction#SQL Server Management Studio Installation | SQL Server Management Studio] we know that **tables** are found in the `tables` "*folder*" ( *or whatever you want to call it* ).

Well for **Stored Procedures** they are stored in the directory `db_name/Programmability/Stored Procedures`. In addition if you want to view all **user-defined** Stored Procedures in the database. Then you can use the following command $\downarrow$:

```SQL
SELECT name, type_desc, create_date FROM sys.procedures;
```

The about should look something like this:

```console
name	     type_desc	           create_date
sp_maths_op	 SQL_STORED_PROCEDURE  2025-01-22 15:55:24.127
```

### The Microsoft's Way of Checking for Stored Procedures

While researching on [[SQL Procedural Programming - Exception Handling | `TRY ... CATCH`]. I was looking that the official [documentation](https://learn.microsoft.com/en-us/sql/t-sql/language-elements/try-catch-transact-sql?view=sql-server-ver16#retrieve-error-information) from Microsoft and found out that the check for **already created** Stored Procedures differently.

> Let's take look!

```SQL
-- Verify that the stored procedure does not already exist.
IF OBJECT_ID('usp_GetErrorInfo', 'P') IS NOT NULL
    DROP PROCEDURE usp_GetErrorInfo;
GO
```

> The code above $\uparrow$ is basically taken from the documentation.

> [!INFO]
> I thought that this **function** deserved its own little note ( *making atomic notes* )
> Therefore, I suggest you to take a look at the file '[[SQL Server - OBJECT Function#Find If Object Exists | SQL Server - OBJECT Function]' whereby it was created after writing the above code block

## Create Procedures

> Well Remember Visual Basic... *That Fucker*!

This is the template for creating a Stored Procedure in Microsoft SQL Server $\downarrow$:

```SQL
CREATE PROCEDURE sp_name
	-- parameters that will be supplied
	@param_1 DATATYPE,
	@param_2 DATATYPE,
	@param_3 DATATYPE
AS
BEGIN
	-- declaration of variables
	DECLARE @x DATATYPE;
	-- intialisation of variable `@x`
	SET @x = VALUE;
	-- declaration and initialisation of variables ( similar to C )
	DECLARE @y DATATYPE = VALUE;
	
	-- code / statements goes here
END
```

> Again, similar to [[C Language Basics|C], we place the `;` character at the end

### Running the Stored Procedure

```SQL
-- stored procedure with no parameters being
EXEC sp_stored_procedure_name;

-- stored procedure with parameters in order
EXEC sp_stored_procedure_name VALUE, VALUE, VALUE, ...;

-- stored procedure with parameters not in order
EXEC sp_stored_procedure_name @param_1 = VALUE, @param_2 = VALUE, @param_3 = VALUE, ...;

```

## Casting

Similar to most programming languages... We are going to need to "*type-cast*" of variables so that we can you it in the `PRINT` function as it **only** allows for `CHAR` or `VARCHAR` datatypes.

> [!NOTE]
> We use the `+` symbol to **concatenate** 2 *string*!

Here is a simple example:

```SQL
CREATE PROCEDURE sp_casting
	-- in this case no parameters are being passed
AS
BEGIN
	DECLARE @x INT = 44;

	-- inline casting
	PRINT 'On the 23 of January of 2024 the number ' + CAST(@x AS VARCHAR(2)) + ' offically became a Ferrari driver!!!';
	
END
```

As result / message we should get something like this... A simple sentence that tell a lot of things...

```console
On the 23 of January of 2024 the number 44 offically became a Ferrari driver!!!
```

## Output Parameters

> This is considered the best way to "*return*" a parameter to the main program.

Consider the code below $\downarrow$:

```SQL
CREATE PROCEDURE sp_param_out
	-- parameters that will be supplied
	@param_1 DATATYPE,
	@param_2 DATATYPE,
	@param_3 DATATYPE OUTPUT
AS
BEGIN
	-- code / statements goes here
END
```

Well, if you want to use the value of `@param_3` outside the procedure. Then you need to *run* the program like so:

```SQL
-- declare the variable outside the procedure
DECLARE @param_3_out DATATYPE;

-- run the stored proeedure
EXEC sp_param_out @param_1 = VALUE, @param_2 = VALUE, @param_3_out OUTPUT,

-- use the value / parameter
PRINT 'Parameter 3 Was: ' + CAST(@param_3_out)
```

> [!WARNING]
> You see that in our declaration of **parameters**; we do have 3 parameters that are going to be passed into the procedure.
> But this does not mean that its like other programming languages whereby you supply that **third** parameter.
>
> In this case, we do **only** have *2* parameters that we can pass through in this Stored Procedure.
> But during the `EXEC`ution, we are going to pass `@param_3_out OUTPUT` ( *as third parameter* ) so that we can get to use *that* value outside the procedure.
>
> > Remember to declare another variable that will be used as the **output**; in this case it was `param_3_out`!
>

## IF Statements

Well, in SQL Server Procedural Programming; we only have one type of *selection* and only one type of *loop* ( *we are going to take a look after* ).

In addition, the other thing is that normally we can do something like this $\downarrow$:

- C Programming Language

```C
#include <stdio.h>

int main() {
	if ( condition = value ) {
		// statements
	}
	else if ( condition = value ) {
		// statements
	}
	else {
		// statements
	}
	return 0;
}
```

- Python Programming Langauge

```python
def main():
	if condition = value:
		# statements
		pass
	elif condition = values:
		# statements
		pass
	else:
		# statements
		pass


# source the main function
if __name__ == '__main__':
	main()
```

> [!INFO]
> The codes above $\uparrow$ was basically created to tell you that we don't even have "*else if*" in SQL Procedural Programming!
>
> Therefore, we only have to use **nested** `IF` statements

> [!TIP] Tips - Declaration of Variables
> Before we start writing any SQL code. Did you notice something?
>
> In SQL Procedural Programming, we use the `@` symbol before a variable or parameter or whatever to indicate that this *variable* is part of the "*declaration*" of the variable **in the SQL Procedure**!
> Again, just to refresh your memory, the reason why we have procedures in the first place is to make our life easier when running SQL queries or performing repetitive, complex commands / statements in SQL.
>
> Hence, your `staff` table could have the attribute / field `Staff_Name`. Therefore the makers of this language allows us to use something like `@Staff_Name` whereby keeping the same name as the field but now we can perform *Procedural Language Operations* on it!
>
> Another things that I would like to talk about is `BEGIN ... END`. You are going to see below $\downarrow$ how we write code with `IF` statements. People ( *even the lecturer* ) said that you can exclude the `BEGIN ... END` *thing* if you **only** have *1* statement in your `IF` ( *something like a little `SELECT`* ).
>
> > But I consider you to place it anyways!
>

> [!NOTE] System Variables
> Similar to functions and procedures... SQL have **built-in** *variables*. These variable **cannot** be *declare* or even *assigned* a value.
>
> > These **System Variables** are preceded with 2 `@` characters! 
>
> They are just use to display warning or perform "*checking*" conditions. An example for a System Variable is `@@ROWCOUNT`.

This is how you are going to use the `IF` statements:

```SQL
CREATE PROCEDURE sp_if_statements
	-- parameters that will be supplied
	@param_1 DATATYPE,
	@param_2 DATATYPE,
AS
BEGIN
	-- some declaration and initalisation just for show
	DECLARE @variable_1 DATATYPE = VALUE;
	
	-- our start of if statements
	IF condition
	BEGIN
		-- statments goes here
		
		-- nested if statement
		IF condition
		BEGIN
			-- statments goes here
		END
		ELSE
		BEGIN
			-- nested if statement ( basically "else if" )
			IF condition
			BEGIN
				-- statments goes here
			END
		END
	END
	-- our "else if condition" that is similar to C --> this is allowed
	ELSE IF condition
	BEGIN
		-- statments goes here
	END
END
```

> [!INFO] Some Comments
> Again, we don't have something like `elif` but as you can see in the few last lines $\uparrow$. We can absolutely do something like `ELSE IF` and [I think that is superior](https://www.youtube.com/watch?v=wVn2-_sU3Zc&t=304s) ( *readability and so on* )!

## WHILE Statements

Again, we only have one type of *loops* in SQL Procedural Programming and its the mother fucking `WHILE` loop.

> You know how I feel about my `WHILE` loops! Fucking hate those motherfuckers!

Well, this is a general "*template*" for using `WHILE` loops including things like `BREAK` and `CONTINUE` $\downarrow$:

```SQL
CREATE PROCEDURE sp_while_loops
	-- parameters that will be supplied
	@param_1 INT,
	@param_2 INT
AS
BEGIN
	-- some declaration and initialization just for show
	DECLARE @counter DATATYPE = VALUE;
	
	-- our while loop
	WHILE condition
	BEGIN
		-- our start of if statements
		IF condition
		BEGIN
			-- statements
			CONTINUE;
		END

		-- another if condition ( could have use "ELSE IF" if you wanted to )
		IF condition
		BEGIN
			-- exit the while loop completely
			BREAK;
		END
		-- some statements
		
	END
	-- some other statements
	
END
```

## ALTER Procedure

Similar to the `ALTER` command for tables. We can use it to change the Stored Procedure that we just wrote.

For example, you created a Stored Procedure and found out that you have a mistake in there. Hence you can use the `ALTER` command instead of the `CREATE` command to change the Stored Procedure.

Below there is a code that we created that we have some errors in it.

```SQL
CREATE PROCEDURE sp_param_out
	-- parameters that will be supplied
	@param_1 DATATYPE,
AS
BEGIN
	-- code / statements goes here
	-- ERROR Found Here
END
```

Hence, we can use the `ALTER` to change the code without the need to `DROP` ( *we will get to that later* ). This can be done like so $\downarrow$:

```SQL
ALTER PROCEDURE sp_param_out
	-- parameters that will be supplied
	@param_1 DATATYPE,
AS
BEGIN
	-- code / statements goes here
	-- ERROR has been corrected
END
```

## DROP Procedure

Well, as the name suggest, we can "*drop*" / delete the Stored Procedure that we create.

Let's create a simple Stored Procedure what will show the names of the stored procedure found in the current database.

### Creation of Stored Procedure

```SQL
CREATE PROCEDURE sp_list_stored_procedure
AS
BEGIN
	-- select the field 'name' from the table `sys.procedures`
	SELECT name FROM sys.procedures;
END

```

After the execution with the simple command of `EXEC sp_list_stored_procedure;`; we should get `sp_list_stored_procedure` in that table.

> Well, if you created other Stored Procedure. They are also going to appear here.

This should look something like this $\downarrow$:

```console
name
sp_add_nums
sp_list_stored_procedure
```

### DROP Procedure

Run the command below to delete the Stored Procedure `sp_list_stored_procedure`:

```SQL
DROP PROCEDURE sp_list_stored_procedure;
```

Now, if we run the command `SELECT name FROM sys.procedure` we should not have any `sp_list_stored_procedure` in that table

```console
name
sp_add_nums
```

## Examples

These examples are taken from the **first** lecture that we did. You can find the PDF here [[Database Systems - SQL Procedural Programming.pdf]]

### Example 1

```SQL
-- create procedure to add 2 numbers
CREATE PROCEDURE sp_add_nums
	@num1 INT,
	@num2 INT
AS
BEGIN
	-- declaration of variables
	DECLARE @sum INT;
	
	-- perform the addition
	SET @sum = @num1 + @num2;
	
	-- output the sum
	PRINT 'The Sum of the 2 Numbers: ' + CAST(@sum AS VARCHAR(10));
END
```

After running the Stored Procedure with the command:

```SQL
-- execution of command + passing of parameters
EXEC sp_add_nums @num1 = 1, @num2 = 1;
```

We should get something like this $\downarrow$:

```console
The Sum of the 2 Numbers: 2
```

### Example 2

```SQL
-- create procedure to add 2 numbers and check if its greater than 10
CREATE PROCEDURE sp_add_nums
	@num1 INT,
	@num2 INT
AS
BEGIN
	-- declaration of variables
	DECLARE @sum INT;
	
	-- perform the addition
	SET @sum = @num1 + @num2;

	-- check if the sum is greater than 10
	IF @sum > 10
	BEGIN
		-- if the sum is greater than 10
		-- output the appropriate message
		PRINT 'The Sum of the 2 Numbers Exceeds 10!';
	END
	ELSE
	BEGIN
		-- if the sum is less than 10
		PRINT 'The Sum of the 2 Numbers: ' + CAST(@sum AS VARCHAR(10));
	END
END
```

#### Execution of Stored Procedure

```SQL
EXEC sp_add_nums @num1 = 1, @num2  = 1;
```

This should give us the result of $\downarrow$:

```console
The Sum of the 2 Numbers: 2
```

But if you are going to sum some large number... You are going to get this message $\downarrow$:

```SQL
EXEC sp_add_nums @num1 = 100, @num2  = 100;
```

```console
The Sum of the 2 Numbers Exceeds 10!
```

### Example 3

```SQL
CREATE PROCEDURE sp_add_nums
	@number FLOAT,
	@threshold FLOAT
AS
BEGIN
	-- declaration and initialisation of variable
	DECLARE @sum FLOAT = 0;

	-- while loop
	WHILE @sum < @threshold
	BEGIN
		-- add the sums
		SET @sum = @sum + @number;
	END

	-- output appropriate message
	PRINT 'The Sum is: ' + CAST(@sum AS VARCHAR(10));
END
```

If we execute this Stored Procedure like so $\downarrow$:

```SQL
EXEC sp_add_nums @number = 5, @threshold = 100;
```

We should get something like this:

```console
The Sum is: 100
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!
