---
id: SQL Commands - Data Control Language - Views and Privileges
aliases: SQL Commands - DCL ( Views - Granting and Revoking Access )
tags:
  - SQL
  - uni
  - uom
  - db
module: ICDT 1202Y
author: S.Sunhaloo
date: 2024-09-28
status: Completed
---

> [!INFO]
> The Lecture Slides for this file / note is called '[[Database Systems - SQL Views and Privileges.pdf]'

## List of Contents

- [[#Views]]
	- [[#Create Views]]
		- [[#Explanation for WITH CHECK OPTION]]
		- [[#Creation of Views Examples]]
	- [[#Drop Views]]
		- [[#Drop View Syntax]]
		- [[#Example Dropping Bombs... I mean Views | Examples of Dropping Views]]
- [[#Login and User]]
	- [[#Create Logins]]
		- [[#Transact-SQL Syntax for Creating Users]]
		- [[#Example Creating a Login]]
		- [[#Example Deleting / Removing Login from User]]
	- [[#Create Users]]
		- [[#Transact-SQL Syntax for Creating Users]]
		- [[#Example Creating a User]]
		- [[#Example Deleting / Removing a User]]
	- [[#Login with Created Login and User]]
- [[#Privileges]]
	- [[#GRANT Command]]
		- [[#Example of GRANT Command]]
	- [[#REVOKE Command]]
		- [[#Example REVOKE Command]]

---

# Views

> [!TIP] What is a **Base Relation**?
> It is a named relation corresponding to an entity in a conceptual schema ( *see below $\downarrow$* ), whose tuples / rows are **[[ANSI - SPARC Model#Internal Level / Physical Level | physically]** stored in the database.
> > [!INFO]
> > If you want, you can check out:
> > - [[Entity Relationship Diagram ( ERD ) and Relationships]]
>

> [!TIP] What is a **View**?
> - Dynamic result of 1 or more **relational** operations operating on **base relations** to produce another *virtual* relation.
> - The relation is **virtual**
> 	- Does **not** really exists; but **produced** upon request
> - **Contents** of a *view* are defined as query on 1 ore more base relations
> - **Dynamic** $\Rightarrow$ Changes made to **base relation** that affect *view attributes* are **immediately** reflected in the view.

> [!TIP] Purpose of **Views**
> 1. Hide the complexity of database from certain users
> 2. Users have **personalised** view
> 	- Different people can have different view for the same data
> 3. Simplification of complex operations on base relations

## Create Views

> [!TIP] Syntax for Creation of Views
>
> The code snippet is found in the Lecture Note at page 9.
>
> ```SQL
> CREATE VIEW ViewName [ (newColumnName [,...]) ]
> AS
>    subselect
>    [WITH [CASCADED | LOCAL] CHECK OPTION]
> ```
>
> To be honest, I don't really understand *format* ( *for the syntax* ).
> Hence, I asked [ChatGPT](https://chat.openai.com) to generate a better one this is what I got.
> ```SQL
> CREATE VIEW ViewName AS
> SELECT column1, column2, ...
> FROM TableName
> WHERE condition;
> ```

---

### Explanation for WITH CHECK OPTION

Given that you are `INSERT`ing data into the `VIEW` ( *not the table check the example below $\downarrow$* ); the `WITH CHECK OPTION` ensures that the *inserted* row satisfies the condition **view**'s `WHERE` clause.

This `WHERE` clause might look like this:

```SQL
WHERE First_Name LIKE 'S&';
```

> This also applies to the `UPDATE` command.

#### Why Use It?

- Data Integrity
	- Ensures that only **valid** data ( *defined by the view* ) can be *inserted* / *updated*
- Security and Control
	- Prevention of accidental *insertion* / *updates* that might break business logic / view

#### Example

Given something like this $\downarrow$:

```SQL
-- firsly create the view
CREATE VIEW ActiveStaff AS
SELECT staffNo, lname, fname
FROM Staff
WITH CHECK OPTION;

-- To create another view based on ActiveStaff
CREATE VIEW AllActiveStaff AS
SELECT staffNo, lname, fname
FROM ActiveStaff
-- condition
WHERE fname IS NOT NULL
-- using the `WITH CHECK OPTION`
-- for checking insertion / update "anomalies"
WITH CHECK OPTION;
```

---

### Creation of Views Examples

> [!NOTE]
> Please refer to page **11** and **13** for the **difference** between '*Horizontal View*' and '*Vertical View*'!

#### Example 1: Simple Staff View

This *personalised* view will display simple information about a staff like: First Name, Last Name and Staff Number.

```SQL
-- creating and giving the view a name
CREATE VIEW Simple_Personalised_View AS
-- select all the columns from the table
SELECT staffNo AS Staff_Number, lname AS Last_Name, fname AS First_Name FROM Staff;
```

> [!TIP]- Verification of Creation of View `Simple_Personalised_View`
> To verify if our `VIEW` has been created successfully, we can use the statement below $\downarrow$
>
> ```SQL
> -- check if the view has been created correctly
> SELECT name, create_date, modify_date, with_check_option FROM sys.views
> WHERE name = 'Simple_Personalised_View';
> ```
>
> This is the output after query for data from the 'sys.view' table
>
> ```csv
> name	create_date	modify_date	with_check_option
> Simple_Personalised_View	2024-10-02 21:03:14.087	2024-10-02 21:03:14.087	0
> ```

> [!INFO]- Using the View
> We have only **created** the view only. Let's try to actually use it!
> To use the view, we simply "*call*" with the `SELECT` command like we are calling some columns from a table.
>
> ```SQL
> SELECT * FROM Simple_Personalised_View;
> ```
>
> Hence, this should be the output...
>
> ```csv
> Staff_Number	Last_Name	First_Name
> SA9	Howe	Mary
> SG14	Ford	David
> SG37	Beech	Ann
> SG5	Brand	Susan
> SHIT	lastname	NULL
> SL21	White	John
> SL41	Lee	Julie
> ```

> But this is a really shit example, because we could have done $\downarrow$:
>
> ```SQL
> SELECT staffNo AS Staff_Number, lname AS Last_Name, fname AS First_Name FROM Staff;
> ```
>
> This will give use the **same** output as above $\uparrow$:
>
> ```csv
> Staff_Number	Last_Name	First_Name
> SA9	Howe	Mary
> SG14	Ford	David
> SG37	Beech	Ann
> SG5	Brand	Susan
> SHIT	lastname	NULL
> SL21	White	John
> SL41	Lee	Julie
> ```
>
> Let's try creating a good ( *example* ) view!

#### Example 2: Advanced Syntax ( Different Way of Writing It )

> [!NOTE]
> This example should not have been called "*Advanced Syntax ( Different Way of Writing It )*"; It's actually called "*Grouped Views*".
> It is found in page 15 in the Lecture Slide.
>
> > She ( *the lecturer* ) is so smart! ( *compared to others, cough cough GOPEE* )

```SQL
-- creating, giving name, specifying column names
-- using (ID, NAME) instead of using `AS`
-- example: staffNo ---> ID
CREATE VIEW ActiveEmployees (ID, Name) AS
-- selecting columns to be displayed with the view
-- concating the columns `fname` and `lname`
SELECT staffNo, CONCAT(fname, ' ', lname) AS Name FROM Staff
-- please check above ^
WITH CHECK OPTION;
```

> [!TIP]- Verification of Creation of View `ActiveEmployees`
> Checking if we have successfully created our `VIEW`
>
> ```SQL
> -- check if the view has been created
> SELECT name, create_date, modify_date, with_check_option FROM sys.views
> WHERE name = 'ActiveEmployees';
> ```
>
> ```csv
> name	create_date	modify_date	with_check_option
> ActiveEmployees	2024-10-02 21:23:29.567	2024-10-02 21:23:29.567	1
> ```

> [!INFO]- Using the View
> Here what it would look like if we did $\downarrow$:
>
> ```SQL
> SELECT * FROM ActiveEmployees
> WHERE Name LIKE 'J%';
> ```
>
> ```csv
> ID	Name
> SL21	John White
> SL41	Julie Lee
> ```

## Drop Views

### Drop View Syntax

```SQL
DROP VIEW view_name;
```

#### Example: Dropping Bombs... I mean Views

Well, let's go ahead an delete **all** of our views that we have created. But first, let's check what views that we have with $\downarrow$:

```SQL
SELECT name, create_date, modify_date, with_check_option FROM sys.views;
```

Hence, I have these all of these view found below:

```csv
name	create_date	modify_date	with_check_option
Simple_Personalised_View	2024-10-02 21:03:14.087	2024-10-02 21:03:14.087	0
ActiveEmployees	2024-10-02 21:23:29.567	2024-10-02 21:23:29.567	1
ActiveStaff	2024-10-02 21:55:27.930	2024-10-02 21:55:27.930	1
AllActiveStaff	2024-10-02 21:55:38.117	2024-10-02 21:55:38.117	1
ManagerStaff	2024-08-28 05:59:48.553	2024-08-28 05:59:48.553	0
Staff3	2024-08-28 06:00:53.883	2024-08-28 06:00:53.883	0
```

> [!INFO]
> I did not mention this. But now I remember.
> For this file / note; I **not** used the *usual* database 'Dreamhome'.
> I used a 'Test' database, where I do all my *tests* because I can then do shitty shits!

Hence, we run the *these* command below $\downarrow$:

```csv
DROP VIEW Simple_Personalised_View;
DROP VIEW ActiveEmployees;
DROP VIEW ActiveStaff;
DROP VIEW AllActiveStaff;
DROP VIEW ManagerStaff;
DROP VIEW Staff3;
```

> [!NOTE]-
> We cannot do something like:
>
> ```SQL
> -- this CANNOT be done!!!
> DELETE * FROM sys.views;
> ```
>
> Nevertheless, I did ask ChatGPT this question and it gave me this code block.
>
> > "*[I have not idea what am doing / reading](https://www.youtube.com/watch?v=rR4n-0KYeKQ&t=20s)*"
> 
> ```SQL
> DECLARE @sql NVARCHAR(MAX) = '';
>
> -- Generate DROP VIEW statements dynamically
> SELECT @sql = @sql + 'DROP VIEW ' + QUOTENAME(name) + ';' + CHAR(13)
> FROM sys.views
> WHERE name IN (
> 	'Simple_Personalised_View',
> 	'ActiveEmployees',
> 	'ActiveStaff',
> 	'AllActiveStaff',
> 	'ManagerStaff',
> 	'Staff3'
> );
>
> -- Execute the dynamically generated SQL
> EXEC sp_executesql @sql;
> ```

> [!TIP] We should have *nothing* in the 'sys.views' table

---

# Login and User

> [!NOTE]
> - `LOGIN` grants access to the SQL **server**
> - `USER` grants a *login* access to the **database**

> [!INFO] Resources
> Websites:
> - https://learn.microsoft.com/en-us/sql/relational-databases/security/authentication-access/create-a-database-user?view=sql-server-ver16

## Create Logins

### Transact-SQL Syntax for Creating Login

```SQL
CREATE LOGIN login_name
WITH PASSWORD = 'insert_password_here';
-- the "command" `GO` indicated the end of a batch of T-SQL statements
-- NOTE: it is NOT an SQL Command
GO
```

#### Example: Creating a Login

```SQL
CREATE LOGIN testing_login
WITH PASSWORD = '1234567890';
GO
```

> [!TIP]- Verification of Creation of `LOGIN`
> With the SQL statement below $\downarrow$; we are able to list the `LOGIN` found in the **Server**
>
> > Yes, **Server**!
> > `LOGIN` are tied to **Server** ( *at the Server Level* )
> > `USER` are tied to **Database** ( *at the Database Level* )
>
> ```SQL
> SELECT name, type_desc, create_date
> FROM sys.server_principals
> WHERE type_desc = 'SQL_LOGIN';
> ```
>
> ```csv
> name	type_desc	create_date
> sa	SQL_LOGIN	2003-04-08 09:10:35.460
> ##MS_PolicyEventProcessingLogin##	SQL_LOGIN	2022-10-08 06:32:02.537
> ##MS_PolicyTsqlExecutionLogin##	SQL_LOGIN	2022-10-08 06:32:02.543
> hrdm	SQL_LOGIN	2024-08-28 06:15:01.633
> testing_login	SQL_LOGIN	2024-10-03 20:26:21.490 <--- what we created
> ```

#### Example: Deleting / Removing Login from User

If we want to remove a user from a `LOGIN`, we can use something like this $\downarrow$:

```SQL
DROP LOGIN testing_login;
```

> [!TIP]- Verification of Deletion of Login
>
> ```SQL
> SELECT name, type_desc, create_date
> FROM sys.server_principals
> WHERE type_desc = 'SQL_LOGIN' AND name = 'testing_login';
> ```
>
> We should have nothing present!
>
> ```csv
> name	type_desc	create_date
> ```

## Create Users

### Types of Users

#### SQL User with Login

Someone like a [[Database Administrator] is one who is an '*SQL User with Login*'.
This is because they need access **many** / **all** of the database on the instance of SQL Server

#### SQL User with Password

This is like us people ( *i.e students* ) who log into the [[University of Mauritius Data View ( L1S1 )| University]'s SQL Server.

We **don't** need access to all of the database ( *we actually only have access to 1 database* )

In addition, if a person **cannot** authenticate with the Windows Authentication; he / she can use this method to log into the SQL Server.

### Transact-SQL Syntax for Creating Users

```SQL
CREATE USER user_name
FOR LOGIN login_name
WITH DEFAULT_SCHEMA = schema_name;
```

#### Example: Creating a User

> I will be using the same `LOGIN` credential that I created above $\uparrow$:

```SQL
-- ensure that you use the correct database
USE Test;

-- actually creating the user
CREATE USER testing_user
FOR LOGIN testing_login
WITH DEFAULT_SCHEMA = dbo;
```

> [!TIP]- Verification of Creation of `USER`
> Similar to verification of `LOGIN`; we are going user another *table* to view the current *users* in the **current** database
>
> ```SQL
> SELECT name, type_desc, create_date, modify_date
> FROM sys.database_principals
> WHERE type_desc IN ('SQL_USER', 'WINDOWS_USER') and name = 'testing_user';
> ```
>
> I currently have these users in the database 'Test' $\downarrow$:
>
> ```csv
> name	type_desc	create_date	modify_date
> testing_user	SQL_USER	2024-10-03 20:40:09.430	2024-10-03 20:40:09.430
> ```

#### Example: Deleting / Removing a User

If we want to remove a user that we created, we can do something like $\downarrow$:

```SQL
-- specify the database ( in this case Test )
USE Test

-- actually remove the user
DROP USER testing_user
```

> [!TIP]- Verification of Deletion of User
>
> ```SQL
> SELECT name, type_desc, create_date, modify_date
> FROM sys.database_principals
> WHERE type_desc IN ('SQL_USER', 'WINDOWS_USER') and name = 'testing_user';
> ```
>
> We should have nothing present!
>
> ```csv
> name	type_desc	create_date	modify_date
> ```

## Login with Created Login and User

Now, we have created our `LOGIN` and `USER`. What we are going to do now it *suck it*... No, not really.
To be able to login use the newly created *credentials* with [[Microsoft SQL Server 2022 Introduction#Opening Management Studio | SQL Server Management Studio].

### Steps

- Select `SQL Server Authentication` for the 'Authentication' option
- Enter Login Name and Password
- Then simply hit <button> Connect</button>

# Privileges

## GRANT Command

When you use the `GRANT` command, you are granting *permissions* to the **database [[#Create Users | user]**.

> This *database user* is mapped onto his / her [[#Create Logins | login].

### `GRANT` Syntax Template

```SQL
GRANT { permission_list }
ON { securable_object }
TO { principal }
WITH GRANT OPTION
```

Whereby:

- `permission_list` are commands like:
	- `SELECT`, `INSERT`, `UDPATE`, `DELETE`
- `securable_object` are basically database objects like:
	- `TABLE`, `VIEW`, `PROCEDURE`
- `principal` well, its the:
	- `USER`, `ROLE`, `GROUP`
- `WITH GRANT OPTION`
	- This allows that user `principal` to be able to "*hand-out*" **permissions**

### Example of GRANT Command

#### Example: `GRANT ALL` Privileges to a User on An Object

> [!INFO]
> Okay, hear me out!
> You know how we have like 'sys.tables', 'sys.views' and much more!
> I asked, obviously ChatGPT this question
>
> > Is there a table like sys.table where we can see what privileges / permission such as SELECT, etc?
>
> It gave me this answer :LiSkull:
>
> ```SQL
> SELECT 
>    prin.name AS PrincipalName,
>    perm.permission_name AS Permission,
>    perm.state_desc AS State,
>    obj.name AS ObjectName,
>    perm.class_desc AS ObjectType
> FROM 
>    sys.database_permissions AS perm
> JOIN 
>    sys.database_principals AS prin
>    ON perm.grantee_principal_id = prin.principal_id
> LEFT JOIN 
>    sys.objects AS obj
>    ON perm.major_id = obj.object_id
> -- I added this `WHERE` clause below
> WHERE prin.name = 'testing_user';
> ```

> [!TIP] Check User `testing_user` current *things*
> Running the code block above will give us $\downarrow$:
>
> ```csv
> PrincipalName	Permission	State	ObjectName	ObjectType
testing_user	CONNECT	GRANT	NULL	DATABASE
> ```

Now, let's go ahead an give the beloved `testing_user` all the privileges.

```SQL
GRANT ALL PRIVILEGES
ON Staff
TO testing_user
WITH GRANT OPTION;
```

> [!TIP]- Verification of `GRANT` of Privileges
> Running the **same** code block from above $\uparrow$ will now give us as result... this:
>
> ```csv
> PrincipalName	Permission	State	ObjectName	ObjectType
> testing_user	CONNECT	GRANT	NULL	DATABASE
> testing_user	DELETE	GRANT_WITH_GRANT_OPTION	Staff	OBJECT_OR_COLUMN
> testing_user	INSERT	GRANT_WITH_GRANT_OPTION	Staff	OBJECT_OR_COLUMN
> testing_user	REFERENCES	GRANT_WITH_GRANT_OPTION	Staff	OBJECT_OR_COLUMN
> testing_user	SELECT	GRANT_WITH_GRANT_OPTION	Staff	OBJECT_OR_COLUMN
> testing_user	UPDATE	GRANT_WITH_GRANT_OPTION	Staff	OBJECT_OR_COLUMN
> ```
>
> > Hence, success $\checkmark$
>

> [!BUG]
> So the next step is to check whether we actually have **permissions** like `SELECT`, `UPDATE`, etc.
> But because Microsoft if Micro-soft ( *like Mr Dick is soft* ); Apparently when I try to login with the like I said with the above [[#Login with Created Login and User | step]. I get this fucking error message:
>
> ```console
> A connection was successfully established with the server, but then an error occurred during the login process. (provider: SSL Provider, error: 0 - The certificate chain was issued by an authority that is not trusted.) (Microsoft SQL Server, Error: -2146893019)
> ```
> This means that; Yes, it did recognise my username and password. But I think the issue comes in the form of *Encryption*
>
> > Well, that the heck do I know... [Developers](https://www.youtube.com/watch?v=Vhh_GeBPOhs)
>

#### Example: `GRANT` Some Privileges to a User

> [!TIP]- Verification of `GRANT`ing Some Permission
> Running the SQL Code block provided by ChatGPT
>
> ```SQL
> SELECT 
>    prin.name AS PrincipalName,
>    perm.permission_name AS Permission,
>    perm.state_desc AS State,
>    obj.name AS ObjectName,
>    perm.class_desc AS ObjectType
> FROM 
>    sys.database_permissions AS perm
> JOIN 
>    sys.database_principals AS prin
>    ON perm.grantee_principal_id = prin.principal_id
> LEFT JOIN 
>    sys.objects AS obj
>    ON perm.major_id = obj.object_id
> -- I added this `WHERE` clause below
> WHERE prin.name = 'testing_user' AND obj.name = 'Branch';
> ```
>
> ```csv
> PrincipalName	Permission	State	ObjectName	ObjectType
> testing_user	INSERT	GRANT	Branch	OBJECT_OR_COLUMN
> testing_user	SELECT	GRANT	Branch	OBJECT_OR_COLUMN
> ```

> Again, the next step would be to actually try these commands on the table... But Fuck You Microsoft!

## REVOKE Command

Well, this is the opposite of the `GRANT` command. Instead of *giving-out* permissions to a user... We are going to remove his / her **rights**. Because we are powerful people and we do whatever the fuck we want.

### `REVOKE` Syntax Template

```SQL
REVOKE [GRANT OPITION FOR] [ALL PRIVILEGES / permission]
-- or ON securable
ON database_object
-- or user
FROM pricipal
[CASCADE]
```

#### Explanation on `CASCADE`

> [!INFO]
> For a more visual explanation; please refer to the Lecture Slides from page 25 to page 27!

Basically, you know how we have the [[#`GRANT` Syntax Template | option] to grant a user the **permission**... _so that he can **grant** other users permissions_

Hence, we use the `CASCADE`, for example on `user_1`; which has granted permissions to `user_2` and in addition, `user_2` has granted some other permission to `user_3`.

Therefore, **ALL** the people that has *received* privileges from `user_1`.

> I know that this was a shit explanation... I suggest you to look and read the Lecture Slides on this!

### Example REVOKE Command

#### Example: Revoke Some Privilege / Permissions from User

First up, let's see what privileges / permissions our user `testing_user` currently have!

> [!TIP]- Current Privileges / Permissions
> Run the following SQL statement...
>
> ```SQL
> SELECT 
>    prin.name AS PrincipalName,
>    perm.permission_name AS Permission,
>    perm.state_desc AS State,
>    obj.name AS ObjectName,
>    perm.class_desc AS ObjectType
> FROM 
>    sys.database_permissions AS perm
> JOIN 
>    sys.database_principals AS prin
>    ON perm.grantee_principal_id = prin.principal_id
> LEFT JOIN 
>    sys.objects AS obj
>    ON perm.major_id = obj.object_id
> -- I added this `WHERE` clause below
> WHERE prin.name = 'testing_user';
> ```
>
> ```csv
> PrincipalName	Permission	State	ObjectName	ObjectType
> testing_user	CONNECT	GRANT	NULL	DATABASE
> testing_user	INSERT	GRANT	Branch	OBJECT_OR_COLUMN
> testing_user	SELECT	GRANT	Branch	OBJECT_OR_COLUMN
> testing_user	DELETE	GRANT_WITH_GRANT_OPTION	Staff	OBJECT_OR_COLUMN
> testing_user	INSERT	GRANT_WITH_GRANT_OPTION	Staff	OBJECT_OR_COLUMN
> testing_user	REFERENCES	GRANT_WITH_GRANT_OPTION	Staff	OBJECT_OR_COLUMN
> testing_user	SELECT	GRANT_WITH_GRANT_OPTION	Staff	OBJECT_OR_COLUMN
> testing_user	UPDATE	GRANT_WITH_GRANT_OPTION	Staff	OBJECT_OR_COLUMN
> ```

Hence, let's start by removing the privilege of `UPDATE` from the 'Staff' table.

---

```SQL
REVOKE UPDATE
ON Staff
FROM testing_user;
```

> [!BUG] Bug Wait!!!
> When I try to run the above $\uparrow$ code; I got this *simple* error $\downarrow$:
>
> ```console
> To revoke or deny grantable privileges, specify the CASCADE option.
> ```
>
> > BTW read that title again!

---

> Trying again with the `CASCADE` option...

```SQL
REVOKE UPDATE
ON Staff
FROM testing_user
CASCADE;
```

> [!TIP]- Output of Verification
> Hence, it should remove `UPDATE` privilege from the 'Staff' table or does it remove **all** because of the `CASCADE` option?
>
> ```csv
> PrincipalName	Permission	State	ObjectName	ObjectType
> testing_user	CONNECT	GRANT	NULL	DATABASE
> testing_user	INSERT	GRANT	Branch	OBJECT_OR_COLUMN
> testing_user	SELECT	GRANT	Branch	OBJECT_OR_COLUMN
> testing_user	DELETE	GRANT_WITH_GRANT_OPTION	Staff	OBJECT_OR_COLUMN
> testing_user	INSERT	GRANT_WITH_GRANT_OPTION	Staff	OBJECT_OR_COLUMN
> testing_user	REFERENCES	GRANT_WITH_GRANT_OPTION	Staff	OBJECT_OR_COLUMN
> testing_user	SELECT	GRANT_WITH_GRANT_OPTION	Staff	OBJECT_OR_COLUMN
> ```

> [!WARNING] Friendly Warning
> The reason why we have to include the `CASCADE` [[#Explanation on `CASCADE` | option] is because when we *granted* privileges / permissions to the user `testing_user`; we used the `WITH GRANT OPTION`... Well, "*option*".
>
> And even though that user `testing_user` did **not** "*hand-out*" any permissions to any other user. We still need to include that `CASCADE` option.
> Just because we have used `WITH GRANT OPTION` on that specific user.
>
> > Well my guess is now that if we did not have that `WITH GRANT OPTION`.
> > We would not have be forced to use the `CASCADE` option when *revoking*!
>

#### Example: Revoking ALL Privilege / Permission from User

> This is simple enough!

```SQL
-- revoke all the permission from the 'Staff' table
REVOKE ALL PRIVILEGES
ON Staff
FROM testing_user
CASCADE;

-- revoke all the permission from the 'Branch' table
REVOKE ALL PRIVILEGES
ON Branch
FROM testing_user
CASCADE;
```

> You could user `EXEC` and stuff to revoke permission on multiple table at the same time
> But I am good right now :BoBxsUpsideDown:!

> [!WARNING]
> When I run these code above, which it **did** run. But I got this <span style="color: orange;"> Warning</span> ...
>
> ```console
> # I had to break the sentence in separate
> # line because of PDF conversion
>
> The ALL permission is deprecated
> and maintained only for compatibility.
> It DOES NOT imply ALL permissions
> defined on the entity.
> ```
>
> This means that we need to **explicitly** specify the commands that we want to revoke; like specify `SELECT`, `INSERT` and others.

> [!TIP]- Verification of `REVOKE ALL`
> Again, running the *same* SQL statement from above $\uparrow$, we are going to get this:
>
> ```csv
> PrincipalName	Permission	State	ObjectName	ObjectType
> testing_user	CONNECT	GRANT	NULL	DATABASE
> ```

> [!SUCCESS]
> We have completed most things for Data Control Language!!!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!