---
id: Microsoft SQL Server 2022 Data View
aliases: MS SQL Server 2022 Data View
tags:
  - dataview
  - SQL
  - db
  - uni
  - uom
author: S.Sunhaloo
date: 2023-08-21
---

## In-Progress

```dataview
TABLE status, date
FROM "Learning/Microsoft SQL Server 2022"
WHERE status = "In-Progress"
```

## HOLD

```dataview
TABLE status, date
FROM "Learning/Microsoft SQL Server 2022"
WHERE status = "HOLD"
```


# Microsoft SQL Server 2022 Folder

```dataview
TABLE status, date
FROM "Learning/Microsoft SQL Server 2022"
WHERE file.name != "Microsoft SQL Server 2022 Data View"
SORT file.ctime ASC
```

# Microsoft SQL Server 2022 SQL Commands Folder

```dataview
TABLE status, date
FROM "Learning/Microsoft SQL Server 2022/SQL Commands - MS SQL Server 2022"
WHERE file.name != "Microsoft SQL Server 2022 Data View"
SORT file.ctime ASC
```

# Microsoft SQL Server 2022 PL/SQL Folder

```dataview
TABLE status, date
FROM "Learning/Microsoft SQL Server 2022/Procedural Programming - SQL"
WHERE file.name != "Microsoft SQL Server 2022 Data View"
SORT file.ctime ASC
```

# Microsoft SQL Server 2022 Miscellaneous Folder

```dataview
TABLE status, date
FROM "Learning/Microsoft SQL Server 2022/SQL Server - Miscellaneous"
WHERE file.name != "Microsoft SQL Server 2022 Data View"
SORT file.ctime ASC
```

---

# Linking Related Files

## Microsoft SQL Server Related Files

- [[Microsoft SQL Server 2022 Introduction]]

## SQL Commands Related Files

- [[SQL Commands - Data Definition Language ( DDL )]]
- [[SQL Commands - Data Definition Language - Constraints]]
- [[SQL Commands - Data Manipulation Language - INSERT]]
- [[SQL Commands - Data Manipulation Language - SELECT]]
	- [[SQL Commands - Data Manipulation Language - Pattern Matching]]
	- [[SQL Commands - Data Manipulation Language - Aggregate Functions]]
	- [[SQL Commands - Data Manipulation Language - GROUP BY and HAVING]]
	- [[SQL Commands - Data Manipulation Language - Sub Queries]]
		- [[SQL Commands - Combination of 2 or More Queries]]
	- [[SQL Commands - Data Manipulation Language - JOIN]]
- [[SQL Commands - Data Manipulation Language - UPDATE]]
- [[SQL Commands - Data Manipulation Language - DELETE]]
- [[SQL Commands - Data Control Language ( DCL ) - Views and Privileges]]
	- [[SQL Commands - Database Backup and Recovery]]

## PL/SQL Related Files

- [[SQL Procedural Programming - Introduction]]
- [[SQL Procedural Programming - Exception Handling]]
- [[SQL Procedural Programming - Embedded DML]]
- [[SQL Procedural Programming - Cursors]]
- [[SQL Procedural Programming - Triggers]]

## SQL Server - Miscellaneous Related Files

- [[SQL Server - OBJECT Function]]
- [[SQL Server - INSERTED and DELETED Tables]]
- [[SQL Server - Cursor Status Function]]
- [[SQL Server - User System Functions]]