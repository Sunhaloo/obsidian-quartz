---
id: SQL Commands - Data Definition Language - Constraints
aliases:
  - SQL Commands - Data Definition Langauge ( Constraints
  - Defaults and More )
tags:
  - SQL
  - db
  - uni
  - uom
author: S.Sunhaloo
date: "2024-08-13"
status: Completed
---

> [!INFO]
> This file / note is part of [[Microsoft SQL Server 2022 Introduction | MS SQL Server 2022] *documentation*.
> I have already covered the basics of [[Database Languages#Data Definition Language ( DDL ) | Data Definition Language] in the file / note '[[SQL Commands - Data Definition Language ( DDL )]'

## List of Contents

- [[#The Unique Constraint| UNIQUE Constraint]]
- [[#The Not Null Constraint| NOT NULL Constraint]]
- [[#The Primary Key Constraint| PRIMARY KEY Constraint]]
- [[#Foreign Key Constraint| FOREIGN KEY Constraint]]
- [[#Default Constraint| DEFAULT Constraint]]
- [[#Check Constraint| CHECK Constraint]]

---

> [!WARNING]
> I will only be going over / typing our the *clause* and **not** the whole commands.
> > But if I have to write an example; I will be typing everything out.

# Constraints, Defaults and More

## The Unique Constraint

The `UNIQUE` constraint in SQL Server ensures that **all** values in a column or set of columns are <span style="color: green;"> <em> distinct</em> </span> .

This means that there will be **no** *duplicate* values that will be inserted into a specific field.

### Example - Unique Constraint

#### Method 1: Next to Field Name

Here is the template:

```SQL
column_name DATATYPE UNIQUE
```

Here is an actual example $\downarrow$:

```SQL
Email VARCHAR(100) UNIQUE
```

#### Method 2: With `CONSTRAINT` Statement

Here is the template:

```SQL
CONSTRAINT constraint_name UNIQUE ( field )
```

Again, we have an actual example here:

```SQL
CONSTRAINT unique_email UNIQUE ( Email )
```

## The Not Null Constraint

### Method 1: Next to Field Name

```SQL
column_name DATATYPE NOT NULL
```

Here is an example $\downarrow$:

```SQL
PhoneNumber INTEGER NOT NULL
```

### Method 2: With `CONSTRAINT` Statement

Here is the template with the use of `CONSTRAINT` statement

```SQL
CONSTRAINT constraint_name CHECK ( column_name IS NOT NULL )
```

Some example for visualising it better:

```SQL
CONSTRAINT notnull_PhoneNumber CHECK ( PhoneNumber IS NOT NULL )
```

## The Primary Key Constraint

As you know a Primary Key <span style="color: red;"> <strong> cannot</strong> </span> be `NULL`; it needs to have a value at all costs!

> If not, what's even the point of the Primary Key!
> *To sit there and dance*?

### Unique and Not Null Combination

The `PRIMARY KEY` constraint is a **combination** of both the `UNIQUE` and `NOT NULL` constraints.

For example, if you have something like this $\downarrow$:

```SQL
StaffID INTEGER UNIQUE NOT NULL
```

This can simply become:

```SQL
StaffID INTEGER PRIMARY KEY
```

#### Method 1: Next to Field Name

```SQL
column_name DATATYPE PRIMARY KEY;
```

> I have only added the template here.
> Because I already gave an example above $\uparrow$.

#### Method 2: With `CONSTRAINT` Statement

```SQL
CONSTRAINT contraint_name PRIMARY KEY ( primary_key_column )
```

Here is an actual example:

```SQL
CONSTRAINT PK_tblStaff PRIMARY KEY ( StaffID )
```

### Composite Primary Key

As you know a **Composite** Primary Key is a key that is made up with 2 or more fields that can uniquely identify each record in a table.

In [[Microsoft Access ( 2007 ) | Microsoft Access] to create a Composite Primary Key you just need to select ( *with the mouse... yuk* ) the columns that you want to become part of the composite primary key and then right click and fucking finally select *Primary Key*.

In SQL Server ( *or SQL in general* ), we can achieve this like so:

```SQL
CONSTRAINT contraint_name PRIMARY KEY ( column1, column2 )
```

Here is a concrete example of using the above $\uparrow$ command:

```SQL
CONSTRAINT PK_tblOrders PRIMARY KEY ( CustomerID, OrderID, ProductID )
```

> [!WARNING]
> We can **only** use the *second method* in this case; because we need to pass in many values in `()`.

## Foreign Key Constraint

So we all know what a [[Database Systems - Keys#Foreign Keys| Foreign Key] is... *Do You*?

> [!TIP]- Here is a Simple Definition
> A Foreign Key is a field / column that is in one table that is a Primary Key field / column in **another** table.

In SQL ( *from what I understand* ), we need to create a new column ( *for our Foreign Key* ); which by the way, can have the same name or different in the table where it becomes a Foreign Key.

> I know that this $\uparrow$ was one of the shittiest explanation that I have ever gave.
> So let me **show** it to you.

Suppose that we have 2 tables; table 'Branch' and table 'Staff'

> I am literally copying the my lecturer's table... *Because I fucking can*!!! ( *add evil laugh here* )

### Creating Tables

<p align="center"> Table: Branch</p>

```SQL
-- create table 'Branch'
CREATE TABLE Branch (
	-- primary key field of table 'Branch'
    branchNo CHAR(4),
	-- other fields of table 'Branch'
    street VARCHAR(20),
    city VARCHAR(15),
    postcode VARCHAR(8),
	-- specify that `branchNo` is a primary key
    CONSTRAINT PK_tblBranch PRIMARY KEY ( branchNo ),
	-- values entered in field `branchNo` should start with character 'B'
    CONSTRAINT start_with_PK_tblBranch CHECK ( branchNo LIKE 'B%' )
);
```

<p align="center"> Table: Staff</p>

```SQL
-- create table 'Staff'
CREATE TABLE Staff (
	-- primary key field of table 'Staff'
    staffNo VARCHAR(4),
	-- other fields of table 'Staff'
    fname VARCHAR(25),
    lname VARCHAR(20),
    position VARCHAR(15),
    sex CHAR(1),
    DOB DATE,
    salary INTEGER,
    -- foreign key of table 'Staff'
    branchNo CHAR(4),
	-- specify that `staffNo` is a primary key
    CONSTRAINT PK_tblStaff PRIMARY KEY ( staffNo ),
	-- values entered in field `staffNo` should start with character 'S'
    CONSTRAINT start_with_PK_tblStaff CHECK ( staffNo LIKE 'S%' ),

	-- check if `position` is either 'Manager' or 'Assistant' or 'Supervisor'
    CONSTRAINT chk_position_tblStaff CHECK ( position IN ( 'Manager', 'Assistant', 'Supervisor' ) ),
	-- check if `sex` is either 'M' or 'F'
    CONSTRAINT chk_sex_tblStaff CHECK ( sex IN ( 'M', 'F' ) ),
	-- check if `salary` is greater than 7000
    CONSTRAINT chk_salary_tblStaff CHECK ( salary > 7000 ),

	/*
	specify that field `branchNo` in table 'Staff' is
	the primary key of table 'Branch'

	`branchNo` ==> Primary Key of table 'Branch'
	which becomes a Foreign Key in table 'Staff'
	*/
    CONSTRAINT FK_branchNo_tblStaff FOREIGN KEY ( branchNo ) REFERENCES Branch ( branchNo ),
	-- values entered in field `branchNo` should start with character 'B'
    CONSTRAINT start_with_FK_branchNo_tblStaff CHECK ( branchNo LIKE 'B%' )
);
```

### Template for Creating Foreign Key

Hence, we can make a template!

#### Method 1: Next to Field Name

> This clause is found in the "*foreign key*" table
> What I am trying to say is that; *when the Primary Key becomes the Foreign Key*.

```SQL
column_name DATATYPE FOREIGN KEY REFERENCES original_table_name ( original_field_name_in_original_table )
```

#### Method 2: With `CONSTRAINT` Statement

```SQL
CONSTRAINT constraint_name FOREIGN KEY ( new_table_field_name ) REFERENCES original_table_name ( original_field_name_in_original_table )
```

#### Give Foreign Keys Different Names

> [!BUG]- This is **NOT** Recommended!!!
> But we *can* do it.

Let's say that you have a table named 'Orders' and we have another table 'Customers'.

> Here is a visual representation below $\downarrow$

<p align="center"> Table: Customers</p>

| <u> CustomerID</u> | First_Name | Last_Name | Address |
| ----------------- | ---------- | --------- | ------- |

<p align="center"> Table: Orders</p>

| <u> OrderI</u> | CustomerID | OrderDate |
| ------------- | ---------- | --------- |

As you can clearly see, we have `CustomerID` in the table 'Orders' which becomes the *Foreign Key*.

Instead of writing it like so:

```SQL
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    CONSTRAINT FK_Customer FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

We write it like:

```SQL
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
	-- Our CustomerID
    X INT,
    OrderDate DATE,
    CONSTRAINT FK_Customer_X FOREIGN KEY (X) REFERENCES Customers(CustomerID)
);
```

## Default Constraint

The `DEFAULT` constraint is used to to add default value to a record.

Let's say that we have like `EmployeeID` and the `EmployeeID` is in the format of 'EMP2023'.
Now, a new employee has just been employed and he does not currently have an Employee ID.
Hence, we can give him, a temporary ID like 'TMP-EMP' by default.

What I really mean is that, if you do **not** add any *value* to the field / attribute `EmployeeID` it will automatically populate a value ( *that you told it to enter* )

This is how you can implement in your columns / fields $\downarrow$:

### Method 1: Next to Field Name

```SQL
column_name DATATYPE DEFAULT default_value
```

> [!NOTE]-
> That `default_value` must be of the same `DATATYPE`
> For example if you have `VARCHAR` then your `DEFAULT` value can be something like: 'TMP-EMP'

```SQL
Number INTEGER DEFAULT 0
EmployeeID VARCHAR(7) PRIMARY KEY DEFAULT 'TMP-EMP'
```

### Method 2: With `CONSTRAINT` Statement

This is the template for using `DEFAULT` values in a `CONSTRAINT` statement

```SQL
CONSTRAINT contraint_name DEFAULT default_value FOR column_name
```

Here $\downarrow$ is the above $\uparrow$ example using the `CONSTRAINT` method:

```SQL
CONSTRAINT DF_tblTable_Number DEFAULT 0 FOR Number
CONSTRAINT DF_tblEmployee_Employee DEFAULT 'TMP-EMP' FOR EmployeeID
```

## Check Constraint

This is the one that we are going to be using the most because it can do things like:

- Check if value entered is in range ( $\gt$ or $\lt$ )
- Check if value entered is what is required ( from a list of values )
- Check if value starts with a character or set of characters

### Method 1: Next to Field Name

```SQL
column_name DATATYPE CHECK ( enter_check_here )
```

### Method 2: Next to Field Name

```SQL
CONSTRAINT constraint_name CHECK ( enter_check_here )
```

> I will be showing you the examples below in the *sub-headings*...
> I will also be only using the second *method* with the `CONSTRAINT` statement

#### Check Constraint - Range

Take a look at this table $\downarrow$:

Table: Employee

| EmployeeID | First_Name | Last_Name | DOB | Address | Position | Salary |
| ---------- | ---------- | --------- | --- | ------- | -------- |------ |

Now, let's say that we are going to have a range for our salary.
Our salary in this case must be *greater or equal* to 25 000 and *less than or equal* 50 000.

Hence, our check constraint would look something like this:

> I am only writing the *clause* and **not** the whole *command* / *statement*
> In addition, like I said I will be using the second *method* only

```SQL
CONSTRAINT chk_tblEmployee_salary CHECK ( salary > = 20000 AND salary <= 50000 )
```

##### `BETWEEN` SQL Constraint

Now there is one thing we can do to reduce the amount of typing that we do... We can use the in `BETWEEN` constraint.

This will so the same job as:

```console
salary > = 20000 AND salary <= 50000
```

Here is the shorten version of the above $\uparrow$ 'Salary' clause:

```SQL
CONSTRAINT chk_tblEmployee_salary CHECK ( salary BETWEEN 20000 AND 50000 )
```

#### Check Constraint - List of Values

In this company an employee can take a *position* of 'Sales', 'Technician', 'Delivery' or 'Manager'

Hence, we can create a `CHECK` constraint that will allow the user to only enter these $\uparrow$ specific *positions*.

> Let me show you the template first!

```SQL
CONSTRAINT constraint_name CHECK ( column_name IN ( 'list', 'of', 'values' ) )
```

Thus, we have $\downarrow$:

```SQL
CONSTRAINT chk_tblEmployee_position CHECK ( Position IN ( 'Sales', 'Technician', 'Delivery', 'Manager' ) )
```

#### Check Constraint - Value Prefix

What do I mean by "*Value Prefix*"?

Let's say that you have `StudentID` which is in the format below $\downarrow$:

| `StudentID` |
| ---------- |
| <p align="center"> S001</p> |
| <p align="center"> S002</p> |
| <p align="center"> S521</p> |
| <p align="center"> ...</p> |

As you can see we have the character 'S' in front of every *number* in the `StudentID`.

Hence, we can check if the format is correctly entered by using the *template* below.

```SQL
CONSTRAINT start_with_StudentID CHECK ( StudentID LIKE 'S%' )
```

> [!WARNING] BIG Warning
> This will <span style="color: red;"> <strong> not</strong> </span> populate the character 'S'*automatically*
> This is just a **check** to see if the value **entered** by a user is in *that* required format.

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!
