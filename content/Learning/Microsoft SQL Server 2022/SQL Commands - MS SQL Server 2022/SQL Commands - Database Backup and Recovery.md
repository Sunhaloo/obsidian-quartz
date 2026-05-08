---
id: SQL Commands - Database Backup and Recovery
aliases: SQL Commands - DCL ( Database Backup - Recovery / Restoration )
tags:
  - SQL
  - uni
  - db
  - uom
author: S.Sunhaloo
date: 2025-03-27
status: Completed
---

> [!WARNING]
> We have already completed all the lecture **notes** and **slides** regarding [[Microsoft SQL Server 2022 Data View | Microsoft SQL Server 2022].
>
> But I need to make this note / file as in [[Database Systems - Tutorial 4 ( L1S2 ) | Database Tutorial 4 ( L1S2 ) - Question 8] requires us to create a backup of the 'UniDB' database.
>
> Therefore, I am making this note to be able to do that question.
>
> > [!NOTE]
> > This note / file will be a bit different in terms of the presentation as I don't have any lecture PDFs to base myself.
> > 
> > This note will be a little bit like my programming notes.
>

## List of Contents

- [[#Database Backup and Recovery - Restoration]]
	- [[#Database and Transaction Log Backups]]
		- [[#Simple Backups]]
		- [[#Proper Backup Backups]]
	- [[#Database Restoration]]
		- [[#Restore Database Command]]
			- [[#Create Another Database - Use Different Database Name]]
			- [[#Backup to Same Database ( Proper Way )]]

---

> [!INFO] Resources
> - https://learn.microsoft.com/en-us/sql/relational-databases/backup-restore/backup-overview-sql-server?view=sql-server-ver16
> - https://learn.microsoft.com/en-us/sql/relational-databases/backup-restore/full-database-backups-sql-server?view=sql-server-ver16
> - https://learn.microsoft.com/en-us/sql/relational-databases/system-tables/backupset-transact-sql?view=sql-server-ver16
> - https://learn.microsoft.com/en-us/sql/relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server?view=sql-server-ver16
> - https://learn.microsoft.com/en-us/sql/relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server?view=sql-server-ver16
> - https://learn.microsoft.com/en-us/sql/t-sql/statements/restore-statements-transact-sql?view=sql-server-ver16

# Database Backup and Recovery - Restoration

## Database and Transaction Log Backups

### Simple Backups

Given that I have the database 'PL_SQL' which I am not currently using... Let's go ahead and try to back this up!

> I am going to backup **both** the actual *database* and its *transactions logs*.

- Backup Actual Database

```SQL
-- backup our database 'PL_SQL'
BACKUP DATABASE PL_SQL
-- specify backup file name
-- and use default location of backup
TO DISK = 'PL_SQL_DB.bak';
```

> [!SUCCESS] Output
>
> ```console
> Processed 568 pages for database 'PL_SQL', file 'PL_SQL' on file 1.
> Processed 2 pages for database 'PL_SQL', file 'PL_SQL_log' on file 1.
> BACKUP DATABASE successfully processed 570 pages in 0.027 seconds (164.785 MB/sec).
> ```

- Backup Database Transactions Logs

```SQL
-- backup our database 
-- transactions logs for 'PL_SQL'
BACKUP LOG PL_SQL
-- specify backup file name
-- and use default location of backup
TO DISK = 'PL_SQL_LOG.bak';
```

> [!BUG] Output
>
> ```console
> The statement BACKUP LOG is not allowed while the recovery model is SIMPLE. Use BACKUP DATABASE or change the recovery model using ALTER DATABASE.
Msg 3013, Level 16, State 1, Line 3
BACKUP LOG is terminating abnormally.
> ```
>
> We are going to get to the bottom of this later!

> [!TIP] Some Tips!
> - You can run these commands from the 'master' database or any other database
> - Even though the `.bak` *file extension* is not necessary
> 	- Please do add it as its the standard ( *Linux users might understand this while Windows Fucking users might not*! )

#### Output Location

If you have not touch any settings during the installation of Microsoft SQL Server.
Then the output directory for these backups should be $\downarrow$:

```console
C:\Program Files\Microsoft SQL Server\MSSQL._n_\MSSQL\Backup
```

> [!NOTE] Changed Default Installation Directory
> In my case, because I changed my installation directory for SQL Server. This `Backup` folder, *for me*, is found under:
>
> ```console
> C:\Microsoft SQL Server\SQL Server ( itself )\MSSQL16.SQLEXPRESS\MSSQL
> ```

### Proper Backup Backups

Even though the above $\uparrow$ database backup statements are good and will do the backup as intended.

Nevertheless, this is not a proper way of doing things. But before, I get into the new statement that we need to run.

Let us take a look at '*Backup Set*' and *Media Set*

#### Backup Set and Media Set

> [!TIP] What is a Backup Set?
> A **backup set** contains the *backup* from a single, successful backup operation.

> [!TIP] What is a Media Set?
> A **media set** is an ordered *collection* of backup media, tapes or disk files.

> [!INFO] What is the Difference Between Them?
> - 1 **media set** can contain *many* **backup set**
> - **Media Set** contains additional information like *header* / *metadata* for the **backup set**

Just know that the "*media*" set refers to the physical storage media being used. As [jeyoung](https://github.com/jeyoung) told me that you could have a database that is 1 Terabytes in size but it can be stored on 5 different 200 GB hard disks.

Now let's go ahead and run some codes!

---

Before we start we are going to first going to switch the database recovery model to a 'FULL RECOVERY' model instead of using the 'SIMPLE' model.

```SQL
-- alter the database to switch from 'SIMPLE' to 'FULL RECOVERY'
ALTER DATABASE PL_SQL SET RECOVERY FULL;
```

- Backup Actual Database

```SQL
-- backup database itself
BACKUP DATABASE PL_SQL
-- default output location ( check info callout )
TO DISK = 'FULL_PL_SQL_DB.bak'
-- format the storage medium before writing to it
WITH FORMAT,
	-- specify the name of backup
	NAME = 'Full Backup of PL_SQL Database',
	-- specify the media name ( physical storage medium )
	MEDIANAME = 'SomeDick',
	-- give the description of the backup
	DESCRIPTION = 'First Backup of Procedural SQL Test Database',
	-- expire the backup file
	EXPIREDATE = '2025-03-27'
	-- output progress every 10 percent
	STATS = 10;
```

> We could have used `RETAINDAYS` instead of `EXPIREDATE` and pass in an **integer** number as the number of days to retain the backup.

> [!WARNING]
> You are going to have to run the `ALTER` command **together** with the other backup statements.

> [!SUCCESS] Output
> 10 percent processed.
> 20 percent processed.
> 30 percent processed.
> 40 percent processed.
> 50 percent processed.
> 60 percent processed.
> 70 percent processed.
> 80 percent processed.
> 90 percent processed.
> 100 percent processed.
> Processed 568 pages for database 'PL_SQL', file 'PL_SQL' on file 1.
> Processed 2 pages for database 'PL_SQL', file 'PL_SQL_log' on file 1.
> BACKUP DATABASE successfully processed 570 pages in 0.024 seconds (185.384 MB/sec).

> [!INFO] Output to a Different Location
> If you want to, for example, output to the Desktop directory like so:
>
> ```SQL
> TO DISK = 'C:\Users\YourMama\Desktop'
> ```
>
> <p align="center"> <span style="color: orange;"> You won't be able to!!!</span> </p>
>
> If you are try this with the above $\uparrow$ command, you are going to get an error that looks like this $\downarrow$:
>
> ```console
> Msg 3201, Level 16, State 1, Line 6 Cannot open backup device 'C:\Users\username\Desktop'.
> Operating system error 5(Access is denied.).
> Msg 3013, Level 16, State 1, Line 6 BACKUP DATABASE is terminating abnormally.
> ```
>
> If you want to still change the output directory you are going to have to use [SQL Server Configuration Manager](https://learn.microsoft.com/en-us/sql/tools/configuration-manager/sql-server-configuration-manager?view=sql-server-ver16) to be able to grant storage permission to specific directories in your computer system.

#### Format Option

As the name suggests, the `WITH FORMAT` option will... Well **format** the physical storage medium first and then write to it. So in this case as we are using it, we are going to <strong> <span style="color: red;"> delete</span> </strong> every previous backup and write the new one.

> [!WARNING] So be careful when you are using it!
> Hence, SQL Server provides the user with other options so that he / she does not need to necessarily use the `WITH FORMAT` and be able to use others. Below is a table about the other options.
>
> | Option | Description | Effect |
> | ------ | ----------- | ------ |
> | `WITH FORMAT` | Writes a new media header; creates a new set  | Erases all previous backups on the device |
> | `WITH INIT` | Overwrites existing backup sets | Replaces backups from the beginning of the file |
> | `WITH SKIP` | Ignores header checks ( expiration, etc ) | Writes backup without validating media header |


---

- Backup Database Transactions Logs

```SQL
-- alter the database to switch from 'SIMPLE' to 'FULL RECOVERY'
ALTER DATABASE PL_SQL SET RECOVERY FULL;

-- backup database itself
BACKUP LOG PL_SQL
-- default output location ( check info callout )
TO DISK = 'FULL_PL_SQL_LOG.bak';
```

> [!TIP]
> Even though I just wrote these 3 lines in the above $\uparrow$ code block... Things like `NAME`, `MEDIANAME`, `DESCRIPTION`, `STATS` are **allowed** here!

> [!SUCCESS] Output
> Processed 13 pages for database 'PL_SQL', file 'PL_SQL_log' on file 1.
> BACKUP LOG successfully processed 13 pages in 0.004 seconds (24.414 MB/sec).

> [!WARNING]
>
> <p align="center"> <span style="color: red;"> Do NOT Use <code> FORMAT</code> with Transactions Logs</span> </p>
>
> This is because we are trying to backup a **log** file. As you know *logs* are like *audits* and keep track of every user's movements. Then why the fuck does one need to delete the log file?

## Database Restoration

Given that we now have our backup files are stored in the `Backup` folder we have these files:

```console
Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a---          27/03/2025    22:45        4771840 FULL_PL_SQL_DB.bak
-a---          27/03/2025    22:31         176128 FULL_PL_SQL_LOG.bak
-a---          28/03/2025    10:39        5230592 L1S2_Rev_DB.bak
-a---          28/03/2025    10:39         110592 L1S2_Rev_LOG.bak
```

> Yes, I do run MS SQL Server on Windows ( *therefore, 'All Windows Users Are Suckers' also applies to me* )!

Therefore, let's go ahead and completely delete our database ( *including its database transaction logs* ).

```SQL
-- delete database
-- and transactions logs for that database
DROP DATABASE L1S2_Revision;
```

### Restore Database Command

#### Create Another Database - Use Different Database Name

In this case, we are going to create a new database with a **different** name but it should have the same contents as our 'L1S2_Revision' database.

> Apparently, there is nothing inside the 'PL_SQL' database... This is why I switched to this 'L1S2_Revision' database.

> [!INFO] 'L1S2_Revision' Database
> Currently, we have these Tables and [[SQL Procedural Programming - Introduction | Stored Procedures] in our database $\downarrow$:
>
> ```console
> -- tables
> name
> programme
> lecturer
> student
> module
> registers
>
> -- stored procedures
> name
> sp_electricity
> sp_sum_all
> sp_even_cubes
> sp_ins_prog
> sp_disp_lect
> sp_disp_grade
> sp_num_dept
> sp_upgrade
> sp_del_prog
> sp_maths_op
> sp_perimeter
> sp_triangle
> ```

- Restore the Actual Database

```SQL
-- restore the database itself
-- with a different database name
RESTORE DATABASE L1S1_Revision_V2
-- specify the path of backup file
FROM DISK = 'C:\Microsoft SQL Server\SQL Server ( itself )\MSSQL16.SQLEXPRESS\MSSQL\Backup\L1S2_Rev_DB.bak'
-- display the progress
WITH STATS = 25;
```

> [!WARNING]- Always Specify **Absolute** Path!!!
> Compared to `TO DISK` where you can just add the *file name* for the backup... `FROM DISK` requires one to specify the full path of the backup file.

> [!SUCCESS] Output
> 26 percent processed.
> 51 percent processed.
> 76 percent processed.
> 100 percent processed.
> Processed 624 pages for database 'L1S1_Revision_V2', file 'L1S2_Revision' on file 1.
> Processed 2 pages for database 'L1S1_Revision_V2', file 'L1S2_Revision_log' on file 1.
> RESTORE DATABASE successfully processed 626 pages in 0.025 seconds (195.468 MB/sec).

- Restore the Database Transaction Logs

```SQL
-- restore the database transaction logs
-- with a different database name
RESTORE LOG L1S1_Revision_V2
-- specify the path of backup file
FROM DISK = 'C:\Microsoft SQL Server\SQL Server ( itself )\MSSQL16.SQLEXPRESS\MSSQL\Backup\L1S2_Rev_LOG.bak'
-- bring database online
WITH RECOVERY,
	-- display progress
	STATS = 24;
```

> [!BUG] Output
> Msg 3117, Level 16, State 4, Line 3
> The log or differential backup cannot be restored because no files are ready to rollforward.
> Msg 3013, Level 16, State 1, Line 3 RESTORE LOG is terminating abnormally.

> This is not going to work as when we did the backup... We did not specify any other specific option...
> In the next section below $\downarrow$ We are going to learn how to *restore* databases with the same name and do it *properly*.

> [!SUCCESS] Nevertheless!
> We did manage to *restore* the database's Tables and Stored Procedures.
>
> ```SQL
> -- select and use 'L1S2_Revision_V2' database
> USE L1S2_Revision_V2
> GO
>
> -- select the tables from database
> SELECT name FROM sys.tables;
> -- select the stored procedures from database
> SELECT name FROM sys.procedures;
> ```
>
> ```console
> name
> programme
> lecturer
> student
> module
> registers
>
> name
> sp_electricity
> sp_sum_all
> sp_even_cubes
> sp_ins_prog
> sp_disp_lect
> sp_disp_grade
> sp_num_dept
> sp_upgrade
> sp_del_prog
> sp_maths_op
> sp_perimeter
> sp_triangle
> ```

---

#### Backup to Same Database ( Proper Way )

What is the meaning of "*proper*" anyways!

- Restore the Actual Database and Database Transaction Logs

```SQL
-- restore the database itself
-- with a same database name
RESTORE DATABASE L1S1_Revision_V2
-- specify the path of backup file
FROM DISK = 'C:\Microsoft SQL Server\SQL Server ( itself )\MSSQL16.SQLEXPRESS\MSSQL\Backup\L1S2_Rev_DB.bak'
-- over-writes the existing database with the same name
WITH REPLACE,
	-- set database in pending state
	NORECOVERY,
	-- display the progress
	STATS = 25;


-- restore the database transaction logs
-- with a same database name
RESTORE LOG L1S1_Revision_V2
-- specify the path of backup file
FROM DISK = 'C:\Microsoft SQL Server\SQL Server ( itself )\MSSQL16.SQLEXPRESS\MSSQL\Backup\L1S2_Rev_LOG.bak'
-- set database in pending state
WITH NORECOVERY;


-- recover the database
-- completes restore process by
-- 1. rolling forward committed transactions
-- 2. rolling back uncommitted transactions
RESTORE DATABASE L1S1_Revision_V2 WITH RECOVERY
```

> [!WARNING] Recommendation by MS SQL Server!
> Running the above command give me this:
>
> ```console
> Msg 3102, Level 16, State 1, Line 6
> RESTORE cannot process database 'L1S1_Revision_V2' because it is in use by this session. It is recommended that the master database be used when performing this operation.
> Msg 3013, Level 16, State 1, Line 6
> RESTORE DATABASE is terminating abnormally.
> Msg 3102, Level 16, State 1, Line 19
> RESTORE cannot process database 'L1S1_Revision_V2' because it is in use by this session. It is recommended that the master database be used when performing this operation.
> Msg 3013, Level 16, State 1, Line 19
> RESTORE LOG is terminating abnormally.
> Msg 3102, Level 16, State 1, Line 29
> RESTORE cannot process database 'L1S1_Revision_V2' because it is in use by this session. It is recommended that the master database be used when performing this operation.
> Msg 3013, Level 16, State 1, Line 29
> RESTORE DATABASE is terminating abnormally
> ```
>
> So just switch to the 'master' database before running this:
>
> ```SQL
> -- switch to 'master' database
> USE master GO
> ```

> [!SUCCESS] Output
> 26 percent processed.
> 51 percent processed.
> 76 percent processed.
> 100 percent processed.
> Processed 624 pages for database 'L1S1_Revision_V2', file 'L1S2_Revision' on file 1.
> Processed 2 pages for database 'L1S1_Revision_V2', file 'L1S2_Revision_log' on file 1.
> RESTORE DATABASE successfully processed 626 pages in 0.018 seconds (271.484 MB/sec).
> Processed 0 pages for database 'L1S1_Revision_V2', file 'L1S2_Revision' on file 1.
> Processed 3 pages for database 'L1S1_Revision_V2', file 'L1S2_Revision_log' on file 1.
> RESTORE LOG successfully processed 3 pages in 0.012 seconds (1.953 MB/sec).
> RESTORE DATABASE successfully processed 0 pages in 0.173 seconds (0.000 MB/sec).

##### Explanation of `REPLACE`, `NORECOVERY` and `RECOVERY`

- `REPLACE`
	- Allows SQL Server to over-write the existing Database
	- Similar to running `DROP DATABASE DB_Name` $\Rightarrow$ From what I can understand; it does it for you
	- Allows you to use the same database name
	- <span style="color: orange;"> Need to backup everything first though</span>
- `NORECOVERY`
	- Leaves the database in "*restoring*" or "*pending*" state
	- Meaning that users in the system will **not** be able to access / modify the ( *existing* ) database during that time
- `RECOVERY` $\Rightarrow$ Refer to Last Statement in Code Block $\uparrow$
	- Bring the database online and allows users to access and modify things!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!