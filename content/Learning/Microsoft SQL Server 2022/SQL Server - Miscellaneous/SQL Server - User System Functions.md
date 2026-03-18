---
id: SQL Server - User Functions
aliases: SQL Procedural Programming - User Functions in SQl Server
tags:
  - uni
  - db
  - SQL
module: ICDT 1202Y
author: S.Sunhaloo
date: 2025-02-08
status: Completed
---

## List of Contents

- [[#User Functions]]
  - [[#Current Users]]
  - [[#System Users]]
  - [[#User Name Function]]

---

> [!INFO]
> This note / file will only focus on _user_ related functions. I will not really be explaining most things as these functions may only return a single value and are really simple to understand.
>
> > I needed to make this note because I did use a _user-related_ function in '[[Database Systems - Labsheet 3 ( L1S2 )#Question 5 | Database Systems - Labsheet 3 ( L1S2 )]'

---

# User Functions

## Current Users

> [!INFO] Resources
>
> - https://learn.microsoft.com/en-us/sql/t-sql/functions/current-user-transact-sql?view=sql-server-ver16

Its very simple to use this function simply do $\downarrow$:

```SQL
-- displays the 'current' user that is using database(s)
SELECT CURRENT_USER AS 'Current User';
```

In my case, it needs to return `dbo` as I am using the Windows Local Server:

```console
Current User
dbo
```

### Purpose

Well, the main purpose of the this is to be able to get the **Current User** ( _duh_ ). But we can use it to _audit_ / monitor people doing database things.

Lets' say that we have an attribute `current_user` in our table 'table_name'. Now **many** users have access to this table and they can all `INSERT` _records_ into that table.

Say that we needed to get the records that where inserted by a specific user. Therefore we could run something like this:

```SQL
-- display all the records inserted by user 'your_mama69'
SELECT * FROM table_name
WHERE CURRENT_USER = 'your_mama69';
```

> This, in my case, should return **no** result!

```console
branchNo	street	city	postcode
```

But if we do something like this $\downarrow$:

```SQL
-- display all the records inserted by user 'dbo'
SELECT * FROM Branch
WHERE CURRENT_USER = 'dbo';
```

Here, we should get some type of output ( _I am also running this for the first time_! ):

```console
branchNo	street	city	postcode
B002	56 Clover Dr	London	NW10 6EU
B003	162 Main St	Glasgow	G11 9QX
B004	32 Manse Rd	Bristol	BS99 1NZ
B005	22 Deer Rd	London	SW1 4EH
B007	16 Argyll St	Aberdeen	AB2 3SU
```

> Well, these are all the _records_ **inserted** by the user `dbo` ( _which is me_ )!

---

> [!INFO] I think you get the point!
> Therefore, I am just going write '_code blocks_'; maybe with a little explanation of each of them... _Keyword 'maybe'_.
>
> > Nevertheless, I want to move fast with this!

> [!WARNING]
> All the "_commands_" / statements below were ran on the `master` database!

## System Users

- SQL Statement:

```SQL
-- displays the 'system' user
PRINT 'Current System User / Login: ''' + SYSTEM_USER + '''';
```

- Output:

```console
Current System User / Login: 'DESKTOP-QFST42T\username'
```

> [!SUCCESS] And Yes!!!
>
> If you go into the Windows Terminal ( _'Powershell' obviously_ ), then type the following:
>
> ```powershell
> # basically the same command found on Linux / Unix systems
> whoami
> ```
>
> In my case, I get the following output $\downarrow$:
>
> ```console
> desktop-qfst42t\username
> ```
>
> > Which is basically the _same_ thing!

## Session Users

> [!INFO] Resource
>
> - https://learn.microsoft.com/en-us/sql/t-sql/functions/session-user-transact-sql?view=sql-server-ver16

Its is similar to '[[#Current Users]' but has some minor differences in some cases.

- SQL Statement:

```SQL
-- displays the 'session' user
PRINT 'Current Session User / Login: ''' + SESSION_USER + '''';
```

- Output:

```console
Current Session User / Login: 'dbo'
```

## User Name Function

> Yes! Its a **function**!

> [!INFO] Resource
>
> - https://learn.microsoft.com/en-us/sql/t-sql/functions/user-name-transact-sql?view=sql-server-ver16

- SQL Statement:

```SQL
-- displays the 'user name' depending on 'ID'
-- NOTE: the 'ID' can be found from 'sys.database_principles' table
-- additionally, passing make it acts like 'CURRENT_USER'
PRINT 'User Name: ''' + USER_NAME() + '''';
```

- Output:

```console
User Name: 'dbo'
```

Let us first check what we have in the 'sys.database_principles' table!

- SQL Statement ( _output of principal database table_ ):

```SQL
-- display the name and 'id' of database principals
SELECT
	name AS 'Name',
	principal_id AS 'Principal ID'
FROM sys.database_principals;
```

- Output of `SELECT` statement:

```console
Name	Principal ID
public	0
dbo	1
guest	2
INFORMATION_SCHEMA	3
sys	4
hrdm	5
db_owner	16384
db_accessadmin	16385
db_securityadmin	16386
db_ddladmin	16387
db_backupoperator	16389
db_datareader	16390
db_datawriter	16391
db_denydatareader	16392
db_denydatawriter	16393
```

- SQL Statement ( _passing the `ID` parameter_ ):

```SQL
-- displays the 'user name' depending on 'ID'
PRINT 'User Name: ''' + USER_NAME(5) + '''';
```

- Output:

```console
User Name: 'hrdm'
```

---

> [!INFO] There Are Many More!!!
> Because there are many many more _functions_ and _system variables_... I suggest you to search for them by yourself!
>
> > Because I am a lazy motherfucker!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!
