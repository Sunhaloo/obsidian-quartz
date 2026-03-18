---
id: SQL Commands - Data Definition Language ( DDL )
aliases:
  - SQL Commands - Data Definition Language ( DDL )
tags:
  - SQL
  - db
  - uni
author: S.Sunhaloo
date: 2024-08-12
status: Completed
---

> [!INFO]
> This file / notes is part of [[Microsoft SQL Server 2022 Introduction | MS SQL Server 2022]]
> I am trying to make the notes more atomic $\Rightarrow$ Containing a _single_ topic
>
> > Take my last statement as a grain of salt!

## List of Contents

- [[#Writing Comments in SQL]]
- [[#Create Database]]
- [[#Create Tables]]
  - [[#Create a Simple Table]]
  - [[#Create a Normal Table]]
  - [[#Identity / Serial Property]]
  - [[#Deleting / Removing Table| DROP Tables] this is actually found below [[#Renaming a Column| renaming columns]]
- [[#Create Types]]
  - [[#Creating User-Defined Data Type ( Without Constraints )]]
    - [[#Command to Create User-Defined Data Type| The Actual Command]]
    - [[#Adding New Field `Address` to Table| Example of using User-Defined Datatypes]]
  - [[#Create Rules]]
    - [[#Creating User-Defined Data Type ( With Constraints )]]
    - [[#Command to Create Rule| The Actual Command]]
    - [[#Alter Table 'NewEmployees'| Example for Creating Rules]]
- [[#Create Domains]]
  - [[#What the Hell is a Domain?]]
  - [[#Creating Domains]]
- [[#Alter Command]]
  - [[#Alter Command - Add Column| Add Columns]]
    - [[#Alter Command - Drop Column| Drop Column]]
      - [[#Drop Columns WITHOUT Constraints]]
      - [[#Drop Columns WITH Constraints]]
  - [[#Alter Command - Add Constraint]]
    - [[#Adding Constraints - Without No Check| Adding Constraints Without NOCHECK]]
    - [[#Adding Constraints - With No Check| Adding Constraints WITH NOCHECK]]
  - [[#Alter Command - Add Default| Add DEFAULT]]
  - [[#Alter Command - Add Foreign Key| Add Foreign Key]]
  - [[#Renaming a Column| Renaming a Column] $\rightarrow$ Adding this here because not place to put it
- [[#Schemas]]
  - [[#Features of Schemas]]
  - [[#Creating Schemas]]
    - [[#Example Create Schema Tester| Example of Creating Schema]]
- [[#Index / Indexes| Index]]
  - [[#What the heck is an Index?| What is a Index?]]
  - [[#Features of Indexes]]
  - [[#Create Index]]

---

# Data Definition Language ( DDL )

> This '[[Database Languages#Data Definition Language ( DDL ) | Data Definition Language]' is a note that I made; you can read a little bit more about DDL... "_if you want to_".

## Writing Comments in SQL

To write comments in SQL; simply use 2 hyphen characters ( `--` )

### Single Line Comments

```SQL
-- this is a comment
-- this is the same as the Lua Programming Language
```

### Multi-Line Comments

```SQL
/*
This is a multi-line comment
It's similar to C and Java's multi-line comment.
*/
```

---

## Create Database

If you have seen the image of [[Microsoft SQL Server 2022 Introduction#Server v/s Database| Server v/s Database]. Then you will immediately know where we are going with this!

We are now going to create a new **Database** with the identifier name `Test`.

> "_But what is the command?_" you ask... Patient Son, Patient!
> Because we need to learn it first then I can show you the actual command.

```SQL
CREATE DATABASE db_name;
```

Hence, in our case, we need to modify the above $\uparrow$ _template_ command to this $\downarrow$:

```SQL
CREATE DATABASE Test;
```

> [!INFO]
> When you are going to create that database; you will not see anything appear on the [[Microsoft SQL Server 2022 Introduction#The Object Explorer| Object Explorer].
> This is because ( _from what I can see_ ) it's not in real-time.
> Hence, we need to press the <button> Refresh</button> icon found near our [[Microsoft SQL Server 2022 Introduction#Disconnecting from Server| disconnect button].

> [!WARNING]
> If you use [[Git Setup | Git] or [GitHub](https://www.github.com), then you know that we can have many [[Archives - Old/Git Docs/Git Branches| branches] like `main` or `master` and the other user created ones.
> We do **not** really have this here but we have it in terms of _Database names_.
> When you are going to create that database `Test`; when you are going to type it in the _Editor_. You will be typing it in the `master` **database**
>
> > Check this out $\downarrow$
> > ![[SQL Server 2022 - 'master' Database.png]]
> > This is **fine**! We did not create any problems ( _yet_ )
>
> ---
>
> Follow well now!!!
> **After** creating our database `Test`. <span style="color: orange;"> We need to switch to our <code> Test</code> Database!!!</span> .
> You can either:
>
> - Select the Database `Test` in the Object Explorer and make sure it becomes `Test` ( _check the image $\uparrow$_ )
> - You can also use the drop-down menu and then select the `Test` database.
>
> > If you do <span style="color: red;"> <strong> not</strong> </span> do this step; all of our tables, indices and more will be created in our `master` Database.
> > And that's not good mate!

#### Verification - Creation of Database `Test`

We can verify if our database has been created correctly by running the following command $\downarrow$:

```SQL
SELECT * FROM sys.datbases WHERE name = "db_name";
```

Hence, we are going to run:

```SQL
SELECT * FROM sys.datbases WHERE name = "Test";
```

But I am not going to run that command with the `WHERE` clause, I am only going to run `SELECT * FROM sys.databases;`

Thus, our output file will be:

```csv
master
tempdb
model
msdb
Dreamhome
Test <--- Here is our Database `Test`!
```

> [!SUCCESS]-
> Hence, we can say that we have successfully created our Database `Test`!

> [!NOTE]
> The output does not contain the "_Header_"; if we take the example from above $\uparrow$, the header would have been _name_.
> I will find a way to get the output with _Headers_.
>
> > For the moment, please bear with me.

---

## Create Tables

Now, we have created our Database `Test`. We can now create our Database Objects like _tables_, _indices_ and more!

> [!WARNING]
> Don't Forget to switch to the `Test` Database
>
> > Else everything will be fucked up!

### Create a Simple Table

Let's go ahead and create the table `Student`; this table will only contain 2 columns / fields / attribute.

Table: Student

| First_Name | Last_Name |
| ---------- | --------- |

> If you did Computer Science in HSC... this will be a piece of cake for you!

```SQL
CREATE TABLE Student (
	First_Name VARCHAR(20),
	Last_Name VARCHAR(20),
);
```

#### Verification - Creation of Table `Student`

To check if we created our table `Student`; then we can run the command below $\downarrow$:

```SQL
SELECT name, type_desc, create_date FROM sys.tables;
```

In this case, our `.csv` output file will contain the fields _name_, _type_desc_ and _create_date_

```csv
Student,USER_TABLE,2024-08-05 04:15:48.537
```

### Create a Normal Table

Let's now go ahead an create a _Staff_ table.

Table: Staff

| StaffID | Staff_Name | NIC | DOB | Faculty | Address | Phone_Number |
| ------- | ---------- | --- | --- | ------- | ------- | ------------ |

Here is the command $\downarrow$:

```SQL
CREATE TABLE Staff (
	StaffID INTEGER PRIMARY KEY DEFAULT 0000,
	Staff_Name VARCHAR(20),
	NIC VARCHAR(14) NOT NULL CHECK ( NIC LIKE 'S%'),
	DOB DATE,
	Address VARCHAR(50),
	Phone_Number INTEGER CHECK ( Phone_Number LIKE '5%')
);
```

#### Verification - Creation of Table `Staff`

```SQL
SELECT name, type_desc, create_date FROM sys.tables;
```

We are going to now see 2 tables; table _Student_ and also our newly created _Staff_ table.

```csv
Student,USER_TABLE,2024-08-05 04:15:48.537
Staff,USER_TABLE,2024-08-05 04:55:41.030
```

> [!TIP]
> BTW I have a simple note where I explain some basic keys like _Primary Keys_ and _Foreign Keys_.
> Here is the note '[[Database Systems - Keys]'.

### Identity / Serial Property

> They are used to create _key values_.

The `IDENTITY` property applies the following conditions ( _on the column that we have applied it_ ):

- New value is generated based on the current **Seed** ( _starting value_ ) and increments ( _also user-defined_ )
- New value for particular transaction is different from other concurrent transaction on the table
  - Example: Automatically incrementing identification number

> Here is an example below $\downarrow$:

We are now going to create the table 'NewEmployees'

| <u> ID</u> | FirstName | LastName |
| ---------- | --------- | -------- |

```SQL
CREATE TABLE NewEmployees (
	-- `ID` field has the property IDENTITY added
	ID INT IDENTITY(1, 1),
	FirstName VARCHAR(20),
	LastName VARCHAR(20),
	CONSTRAINT PK_NewEmployees PRIMARY KEY ( ID )
);
```

#### Verify Creation of Table

Simply run the SQL command found below $\downarrow$:

```SQL
SELECT name, type_desc, create_date FROM sys.tables
WHERE name = 'NewEmployees';
```

Here are the results for our query $\uparrow$:

```csv
name,type_desc,create_date
NewEmployees,USER_TABLE,2024-08-12 16:27:57.693
```

> [!TIP] Changing the parameters of `IDENTITY`
> As you can see from the above example, we have written ( _more like "typed"_ ) `IDENTITY(1, 1)`
> But what does that actually mean?
> The _first_ number / parameter, is called the **Seed** value. This is basically the **starting** value.
> The _second_ number / parameter, is the number that we are going to be incrementing, in this case, we are incrementing the auto-generated value by 1
> But what if you had something like `IDENTITY(12, 2)`?
> This simply means that it will:
>
> - Start at the number `12`
> - Increment by `2` ( 1, 3, 5, 7, ... )

---

> [!INFO]
> To learn more about `TYPE`, we can visit:
>
> - Websites:
>   - https://learn.microsoft.com/en-us/sql/t-sql/statements/create-rule-transact-sql?view=sql-server-ver16

## Create Types

Think of it like Object Oriented Programming.

Basically, we can also create **user-defined** datatypes ( _from our "raw" datatypes_ ) in [[Database Languages#Structured Query Language ( SQL ) | SQL].

> I kinda hate Object Oriented Programming.
> Hence, I don't know how I feel about this one.

> We are going to add a field `Address` in the table 'NewEmployees'

### Creating User-Defined Data Type ( Without Constraints )

We are going to alter the table 'NewEmployees' to become like this $\downarrow$:

| <u> ID</u> | FirstName | LastName | Address |
| ---------- | --------- | -------- | ------- |

#### Command to Create User-Defined Data Type

Here is the _template_ to create user-defined datatypes.

```SQL
-- without any constraints
CREATE TYPE type_name FROM DATATYPE

-- with constraints
CREATE TYPE type_name FROM DATATYPE NOT NULL DEFAULT default value
```

> [!INFO]
> These user-defined datatypes that we are creating are **permanent**.
> They are stored as _objects_ in the database.
> If you want to remove them, you can use the command:
>
> ```SQL
> DROP TYPE type_name;
> ```

> Create our address datatype

```SQL
CREATE TYPE AddressType FROM VARCHAR(50);
```

In this case, we do not have any constraints associated with it.

##### Verification - Creation of Type

With the command below $\downarrow$, we can check the table 'sys.types' and search for name where `is_user_defined` has a value of 1

```SQL
SELECT name, system_type_id FROM sys.types
WHERE is_user_defined = 1;
```

Here are the results of our query:

```csv
name,system_type_id
AddressType,167
```

##### Adding New Field `Address` to Table

As we have already created the table, we are going to use the `ALTER` command to add the new column

```SQL
ALTER TABLE NewEmployees
-- ADD column_name Address
-- where 'AddressType' is our user-defined datatype
ADD Address AddressType;
```

Add 1 value to our table 'NewEmployees'

> If I do not add this, I will not be able to get a `.csv` output.

```SQL
INSERT INTO NewEmployees ( FirstName, LastName, Address ) VALUES ( 'Guy1', 'SometingWong', 'Address thing 1' );
```

> Not including any value for `ID` because I want to test its _auto-generation_!

Check if our field / column has been created successfully.

```csv
ID,FirstName,LastName,Address
1,Guy1,SometingWong,Address thing 1
```

> As we can all see ( _and agree_ ); our `IDENTITY` is working correctly!

> [!SUCCESS]- Double Success
> Hence, we can say that we have learned about `TYPE` and `IDENTITY`

### Create Rules

> Do you follow your _rules and regulations_? ( - \_ - )

This is basically creating [[SQL Commands - Data Definition Language ( DDL )#Create Types| user-defined] datatypes **with** _constraints_

#### Creating User-Defined Data Type ( With Constraints )

##### STEPS:

1. Create your desired datatype from the base datatypes
2. Create the Rule / Constraint
3. _Bind_ the constraint to that datatype

> For this example I will adding another field / column to our table 'NewEmployees'
> I will also be using the lecturer's note.

Create the User-Defined Data Type

```SQL
CREATE TYPE GenderType FROM CHAR(1);
```

###### Command to Create Rule

Create the Rule / Constraint for our User-Defined Data Type

```SQL
CREATE RULE GenderTypeRule AS @list IN ( 'M', 'F' );
```

Finally **Bind** the Rule / Constraint to that user-defined data type

```SQL
EXEC SP_BINDRULE 'GenderTypeRule', 'GenderType';
```

##### Alter Table 'NewEmployees'

We are now going to add a field ( _I think I have already said this_ ) called `Gender` to that table.

| <u> ID</u> | FirstName | LastName | Address | Gender |
| ---------- | --------- | -------- | ------- | ------ |

> Again, here also using the `ALTER` command

```SQL
ALTER TABLE NewEmployees
ADD Gender GenderType;
```

We can quickly check if it has been added by running $\downarrow$:

```SQL
SELECT * FROM NewEmployees;
```

Here are the results:

```csv
ID,FirstName,LastName,Address,Gender
1,Guy1,SometingWong,Address thing 1,NULL
```

> Because we did not add any value for `Gender` to record '1'
> This is why we have `NULL`

But if we run these commands below $\downarrow$:

```SQL
UPDATE NewEmployees
SET Gender = 'M'
WHERE ID = 1;
```

We are going to **now** get:

```csv
ID,FirstName,LastName,Address,Gender
1,Guy1,SometingWong,Address thing 1,M
```

> [!SUCCESS]
> I think we have completed 1 percent of `CREATE RULE`
>
> > What do you think?

> [!TIP]
>
> ##### Create Rule - Range Constraint
>
> ```SQL
> CREATE RULE rule_name AS @range> = 0 AND @range <= 100
> ```

---

## Create Domains

### What the Hell is a Domain?

Here is the full explanation that I made for **Domain** $\Rightarrow$ '[[Entity Relationship Diagram ( ERD ) and Relationships#What is Attribute Domain?]'

Basically, long story short, the **domain** of an attribute / field / column is simply the **Data Type**.

But then if you are going to create _user-defined_ data type, then use the fucking `TYPE` statement.
In addition, we can have constraints; basically `RULES`.

We have covered all of this above $\uparrow$

> Just glance back!

> [!TIP]- What is the **purpose** of a Domain?
> It defines a specific **type** with associated constraints that can be **reused** across multiple columns or tables.
> It essentially creates a **template** for a _data type_ which **includes** _validation rules_.

> [!TIP]- The **scope** of a Domain?
> It applies constraints to **any** _column_ that uses it... those constraints are part of the **type definition**.

> [!TIP]- Where are Domains used?
> They are used when you want to define a specific data type what **multiples** columns / tables can _share_ and where you **want** _constraints_ consistently enforced.

> [!NOTE]
> `DOMAIN` are clearly **better** than `TYPES` because when you are going to create a "_type_".
> I don't think that you are going to create it **without** any constraints; hence you are going to use `RULES`.
> Because I don't remember I will list out the steps to create a `TYPE` with constraints ( `RULES` ) again
>
> > Do you really think that I will type things again?
>
> ![[#STEPS]]
>
> > We even got an example as a bonus!
>
> But there is one **problem**... <span style="color: red;"> <code> RULES</code> are a Legacy Feature</span> !!!
> Thus, they are said to be outdated and are considered to be **obsolete** in many modern [[University Data View ( L1S1 )#Database Systems Notes| Database Systems].
> This is where `DOMAIN`s come into play because of their:
>
> 1. Simplicity
> 2. Modern Usage
> 3. Maintainability
> 4. Portability

### Creating Domains

Here is the _template_ for creating `DOMAINS` $\downarrow$:

```SQL
CREATE DOMAIN domain_name AS data_type
  [DEFAULT default_value]
  [CONSTRAINT constraint_name CHECK (condition)];
```

### Examples of Creating Domains

> [!WARNING]
> I did **not** run these commands that I am going to provide...
> Because they are from [ChatGPT](https://chat.openai.com)

#### Example: Domain with Age Validation

```SQL
-- create domain of type `INTEGER`
CREATE DOMAIN AgeDomain AS INT
-- checks if the age is between 0 and 18
CONSTRAINT valid_age CHECK (VALUE > = 0 AND VALUE <= 18);
```

#### Example: Domain to Validate Phone Number Ranges

```SQL
-- create domain of type `VARCHAR`
CREATE DOMAIN PhoneNumberDomain AS VARCHAR(15)
-- check if the phone number contains 8 digits
CONSTRAINT valid_phone CHECK (VALUE LIKE '_________');
```

#### Example: Domain with Default Value

```SQL
-- create domain of type `DECIMAL` ( 2 DP )
CREATE DOMAIN SalaryDomain AS DECIMAL(10, 2)
-- which has a default value of '30000'
DEFAULT 30000
CONSTRAINT valid_salary CHECK (VALUE > = 10000 AND VALUE <= 100000);
```

---

## Alter Command

The `ALTER` command will be used to change the **structure** of a table

What do I mean by "_structure_"? Think of a table, it have records and fields.
Normally ( _most, if not all of the time_ ) the _records_ hold the **data** but the _fields_ holds the _[[Entity Relationship Diagram ( ERD ) and Relationships#What is an Attribute? | attributes]_.

When I talk about changing the _structure_ of a table; I am referring to the **fields**.

Basically the `ALTER` command will help you to:

- Add / Drop columns
- Add / Drop constraints
- Add / Drop default

> [!TIP]
> If you want to change a **value** in a _record_. This will require you to use the `UPDATE` command.

### Example: Customer Table

Let's go ahead a create a really simple 'Customer' table.

| First_Name | Last_Name |
| ---------- | --------- |

> [!NOTE]
> When we are going to add other columns in the table, the order will be at the back.
> What I am trying to say is that `First_Name` will **always** be at the front... _Obviously you can change it by dragging your mouse_.
> Nevertheless, I will be writing it in _my_ way.

As you can see, this table does not even have a Primary Key.

> We are going to be adding them later on!
> _Using the `ALTER` command obviously_

#### Create Table 'Customer'

```SQL
CREATE TABLE Customer (
	First_Name VARCHAR(20),
	Last_Name VARCHAR(20)
);
```

> [!TIP]- Verification - Creation of 'Customer' Table
>
> ```SQl
> SELECT name, type_desc, create_date FROM sys.tables
> WHERE name = 'Customer';
> ```
>
> Here is the output after running the query
>
> ```csv
> name,type_desc,create_date
> Customer,USER_TABLE,2024-08-13 16:12:23.767
> ```

> [!INFO]-
> Similar to above $\uparrow$, I am going to add 1 record into the table; else I will **not** be able to output the data as a `.csv` file.

#### Alter Command - Add Column

We are going to modify our table so that it will become something like this $\downarrow$:

| <u> CustomerID</u> | First_Name | Last_Name | Address |
| ------------------ | ---------- | --------- | ------- |

Here is the _template_ for the `ALTER` command to <u> add</u> a new **column**

```SQL
ALTER TABLE table_name
ADD column1 DATATYPE,
	column2 DATATYPE;
```

Hence, in this case, we are going to have:

```SQL
ALTER TABLE Customer
ADD CustomerID INTEGER,
	-- using our user-defined datatype that we made earlier
	Address AddressType;
```

> Reference for user-defined datatype [[SQL Commands - Data Definition Language ( DDL )#Command to Create User-Defined Data Type| above] $\uparrow$.

Here are the results after running the command `SELECT * FROM Customer;`:

```csv
First_Name,Last_Name,CustomerID,Address
First Person,Some Last Name,NULL,NULL
```

> We are **not** going to add any data yet!
> This is because we are going to create our constraints first then add the data
> Else, our data might be _flawed_

#### Alter Command - Drop Column

What if we want to delete a column in our table.

This can be done using the following command below $\downarrow$:

##### Drop Columns WITHOUT Constraints

```SQL
ALTER TABLE table_name
DROP COLUMN column1,
            column2;
```

Here is an example ( _from our example_ ):

> We are going to be removing the `Address` column as it does not have any constraints attached to it.

```SQL
ALTER TABLE Customer
DROP COLUMN Address;
```

Hence, our 'Customer' table currently look like $\downarrow$:

| <u> CustomerID</u> | First_Name | Last_Name |
| ------------------ | ---------- | --------- |

> [!TIP]- Verification - Removal / `DROP` of Column
>
> ```SQL
> SELECT * FROM Customer;
> ```
>
> Here are the results after running the above $\uparrow$ command:
>
> ```csv
> First_Name,Last_Name,CustomerID
> First Person,Some Last Name,NULL
> ```
>
> > [!SUCCESS]
> > We have removed our column `Address`!

##### Drop Columns WITH Constraints

> [!BUG] You **cannot** do it DIRECTLY!!!
> It's basically a 2 step process:
>
> - Remove / `DROP` the `CONSTRAINT`
> - Remove / `Drop` the `COLUMN` ( _after removing the constraint_ )

> [!NOTE]
> I will cover "_Alter Command - Constraints_" Later on.
> But bear with me for this one.

###### Step 1: Drop Constraint

```SQL
ALTER TABLE table_name
DROP CONSTRAINT constraint_name1,
DROP CONSTRAINT constraint_name2;
```

###### Step 2: Drop Column

```SQL
ALTER TABLE table_name
DROP COLUMN column1,
            column2;
```

#### Alter Command - Add Constraint

> You can refer more about Constraints in the file / note '[[SQL Commands - Data Definition Language - Constraints]'

Let's go ahead and create another column called `Gender` for our 'Customer' table.

It will then become like:

| <u> CustomerID</u> | First_Name | Last_Name | Gender |
| ------------------ | ---------- | --------- | ------ |

```SQL
ALTER TABLE Customer
ADD Gender CHAR(1);
```

> [!TIP]- Verification - Creation of 'Customer' Table
>
> ```SQl
> SELECT * FROM Customer;
> ```
>
> Here is the output after running the above $\uparrow$ query
>
> ```csv
> First_Name,Last_Name,CustomerID,Gender
> First Person,Some Last Name,NULL,NULL
> ```

##### Adding Constraints - Without No Check

The code block below $\downarrow$ is the _template_ for adding `CONSTRAINTS` in SQL

```SQL
ALTER TABLE table_name
ADD CONSTRAINT constraint_name1 CHECK (condition1),
    CONSTRAINT constraint_name2 CHECK (condition2);
```

Hence, we can use:

```SQL
ALTER TABLE Customer
ADD CONSTRAINT gender_chk CHECK ( Gender IN ( 'M', 'F' ) );
```

> [!WARNING]
> Currently I do **not** how to use _SQL Commands_ to check if our constraint has been created.
> In this case, we can simply head over to the [[Microsoft SQL Server 2022 Introduction#The Object Explorer | object explorer] and look at the **constraints** there.
> Another method would be to purposely make a mistake when inserting a value ( _I like to live a complicated life_ )
>
> ```SQL
> UPDATE Customer
> SET Gender = 'C'
> WHERE First_Name = 'First Person' AND Last_Name = 'Some Last Name';
> ```
>
> Hence, I get this error _successfully_!
>
> ```console
> The UPDATE statement conflicted with the CHECK constraint...
> ```
>
> > [!SUCCESS] But if I run
> >
> > ```SQL
> > UPDATE Customer
> > SET Gender = 'M'
> > WHERE First_Name = 'First Person' AND Last_Name = 'Some Last Name';
> > ```
> >
> > I get $\downarrow$:
> >
> > ```SQL
> > First_Name,Last_Name,CustomerID,Gender
> > First Person,Some Last Name,NULL,M
> > ```

##### Adding Constraints - With No Check

In terms of syntax; we just need to do a minor change:

```SQL
ALTER TABLE table_name WITH NOCHECK
ADD CONSTRAINT constraint_name1 CHECK (condition1),
    CONSTRAINT constraint_name2 CHECK (condition2);
```

###### What Does `WITH NOCHECK` Do?

If you are talking about altering a table that does <span style="color: red;"> <strong> not</strong> </span> have _any_ values, then the above $\uparrow$ command will be a bit _overkill_.
But that does not mean that you cannot include it when we do **not** have values. _You absolutely can_!!!

So when a table already have values, for example:

- You created your 'Customer' table and forgot to add `Gender` column
- Now, you add the `Gender` column using `ALTER` command
- You continue to add values to `Gender` ( _still without any constraints_ )
- Someone tells you to update the table's `Gender` column you add a constraint

Now you have already populated the `Gender` column. Hence we use the `WITH NOCHECK` to not _disturb_ or create more problem with the older / other values.

##### Removing / `DROP` Constraints

> I am actually re-typing this.
> I know that I am going against the [conceptual note-taking method](https://www.youtube.com/watch?v=MYJsGksojms)
> But this is kind-of a documentation; so I guess, it makes sense for me to re-type it.

As we have seen above we can remove a constraint using the _template_ below $\downarrow$:

```SQL
ALTER TABLE table_name
DROP CONSTRAINT constraint_name1,
DROP CONSTRAINT constraint_name2;
```

#### Alter Command - Add Default

> Again, if you need any reference, please head to [[SQL Commands - Data Definition Language - Constraints#Default Constraint| SQL Commands - Constraints ( DDL )]]

Below $\downarrow$ you will find the _template_ for adding `DEFAULT` constraint to an existing column:

```SQL
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
DEFAULT default_value FOR column_name;
```

Here is a concrete example:

> I did not modify the table 'Customer'... I am just writing this

```SQL
ALTER TABLE Customer
ADD CONSTRAINT default_paid
DEFAULT 'F' FOR Paid;
```

#### Alter Command - Add Foreign Key

Simple, I will give you the _template_... and an example.

> You see I am getting tired now.

Here is the _template_ for adding a Foreign Key with `ALTER` command

```SQL
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
FOREIGN KEY (column_name) REFERENCES referenced_table_name (referenced_column_name);
```

#### Alter Command - Combination

Here is an example of combining multiple _constraints_ together.

> This is an example from the lecturer.
> But have customised the Table Name for my scenario.

> I will also try to write a template.

```SQL
ALTER TABLE table_name
ADD column_name DATATYPE CONSTRAINT constraint_name enter_constraints_here;
```

Here is the example $\downarrow$:

```SQL
ALTER TABLE Customer
ADD nid VARCHAR(20) NULL CONSTRAINT nid_unique UNIQUE;
```

---

# Renaming a Column

> [!INFO]
> You can find more information about _renaming columns_ in SQL using the link in the _description box below_ ( _like, share and subscribe mfs_ )
>
> > [!TIP] Description Box
> >
> > - https://learn.microsoft.com/en-us/sql/relational-databases/tables/rename-columns-database-engine?view=sql-server-ver16
>
> > This is a joke BTW, I am not forcing you to subscribe.

To rename a existing column in SQL Server, we can use the `EXEC sp_rename` command.

> Below $\downarrow$ lies the following template ( _say in a godly voice_ )

```SQL
EXEC sp_rename 'table_name.column_name', 'new_column_name', 'COLUMN';
```

## Example: Renaming Column in Customer Table

First of all let's check what are the current fields / columns that we have, because I have _Alzheimer_ and I forgot...

> Let's not talk about that again... I am 19 years old ( Current Date: 13/08/2024 @20:27 )
>
> > You can see that I am on Windows, because in my [Polybar](https://github.com/polybar/polybar) I also have _seconds_ in my _time_.

```SQL
SELECT * FROM Customer;
```

> [!TIP]- Verification - Fields in 'Customer' Table
>
> ```csv
> First_Name,Last_Name,CustomerID,Gender
> First Person,Some Last Name,NULL,M
> test1,test1.5,2,M
> test2,test2.5,3,M
> test3,test3.5,4,M
> ```

### Renaming `CustomerID` to `ID`

We can simply execute $\downarrow$:

```SQL
EXEC sp_rename 'Customer.CustomerID', 'ID', 'COLUMN';
```

#### Verification - Renaming of `CustomerID` $\rightarrow$ `ID`

Here is the `.csv` output after running `SELECT * FROM Customer;`

```csv
First_Name,Last_Name,ID,Gender
First Person,Some Last Name,NULL,M
test1,test1.5,2,M
test2,test2.5,3,M
test3,test3.5,4,M
```

> [!BUG] But Proceed with CAUTION!!!!!!
> Yes, we are able to _rename_ the actual **field**... _But what about it's constraint_
> For example we have:
>
> ```SQL
> CONSTRAINT tbl_CustomerPK PRIMARY KEY ( CustomerID )
> ```
>
> As you can clearly see $\uparrow$, we have `CustomerID` in the `PRIMARY KEY` constraint. Hence, you **should** be careful when renaming **fields**
>
> > If you are going to do this, I recommend altering the `CONSTRAINT` names.

---

# Deleting / Removing Table

> [!INFO]
> To learn more about the `DROP` command, you can visit:
>
> - https://learn.microsoft.com/en-us/sql/t-sql/statements/drop-table-transact-sql?view=sql-server-ver16

> The correct term is _`DROP`ing_ a Table
> _I hope you laughed_

Here is the command _template_ that we can use to delete / `DROP` a table $\downarrow$:

```SQL
DROP TABLE table_name;
```

Here is a **simple** ( _I will talk about it later on_ ) example:

```SQL
DROP TABLE YourMom;
```

> [!WARNING]
> Now, if you only have **only** 1 table created in your _database_; then use the above $\uparrow$ command and be happy!
> But that is normally **not** the case. In my labsheets that I have been doing... The first labsheet was to create 7 tables.
> In addition, some of them were _referenced_ with <span style="color: orange;"> Foreign Keys</span> !
> Hence, we need to first remove these _referencing Foreign Key constraints_ before we can finally `DROP` our table.

---

> [!INFO]
> To learn more about Schemas, you can use the resources below $\downarrow$:
>
> - Wesbsites:
>   - https://learn.microsoft.com/en-us/sql/t-sql/statements/create-schema-transact-sql?view=sql-server-ver16
>   - https://learn.microsoft.com/en-us/sql/relational-databases/security/authentication-access/ownership-and-user-schema-separation?view=sql-server-ver16

# Schemas

## What is a Schema?

It is a logical container or namespace that groups together a collection of database objects like tables, views, constraints.

It helps to organise and manage these objects within a database; provides a way to categorise and control access to them.

> [!NOTE]-
> It is the [[Database Administrator] that gives the privilege / permission to create schemas.

## Features of Schemas

1. Namespace Management
   - It allows multiple objects with the name to exist in the **same** database _as long as they belong to different schemas_
   - Example: We can have `HR.Customer` and `Sales.Customer` ( where `HR` and `Sales` are the Schema names )
2. Security and Permissions
   - Assign different permissions to different schemas $\Rightarrow$ controlling who can access and modify the objects within each schema
3. Ownership
   - It is normally owned by a specific database user or role

> [!INFO]
> The `dbo` which is prefixed with every table that you create in SQL Server is the **default** _schema_.

## Creating Schemas

Below you will find the _template_ for creating schemas $\downarrow$:

```SQL
CREATE SCHEMA schema_name;
```

### Example: Create Schema Tester

```SQL
CREATE SCHEMA Tester;
```

#### Verification - Creation of Schema

We can verify if our schema has been successfully created.

Run the following command

```SQL
SELECT name FROM sys.schemas.
WHERE name = 'Tester';
```

You should have an output like this $\downarrow$:

```csv
name
Tester
```

#### Using the Schema `Tester`

Let's go ahead a create a dummy table 'TableTest'

Here is the command to create tables in the schema `Tester`

```SQL
CREATE TABLE TableTest (
	col1_test INTEGER,
	col2_test CHAR(4)
);
```

> [!TIP]- Verification - Creation of Table 'TableTest'
>
> ```SQL
> SELECT name, create_date FROM sys.tables;
> ```
>
> Here is the output after running the above $\uparrow$ command:
>
> ```csv
> name,create_date
> TableTest,2024-08-14 17:15:06.670
> ```

> [!TIP]
> The commands are literally the same thing!
> Basically, if you want to create into a schema, we need to supply the schema name before typing our the command; something like this $\downarrow$:
>
> ```SQL
> -- Only Typing Out Clause
> -- create table
> CREATE TABLE schema_name.table_name
> -- alter table
> ALTER TABLE schema_name.table_name
> -- update table
> UPDATE TABLE schema_name.table_name
> -- drop table
> DROP TABLE schema_name.table_name
> ```

---

# Index / Indexes

## What the heck is an Index?

> Think of it like [cache](https://www.geeksforgeeks.org/cache-memory/)!

It is a **database object** that improves the **speed** of data _retrieval_ operations on a table at the **cost** of <span style="color: orange;"> additional storage space</span> and maintenance overhead.

> [!TIP] Analogy
> Think of it as a book's index page!
> Where you can quickly find the page number of a specific topic without having to read the entire book.

## Features of Indexes

1. Purpose ( _more like "more speed"_ )
   - Used to enhance the performance of commands like `SELECT` queries and `WHERE` clauses
     - Find rows more quickly rather than scanning the **whole** table
2. Index Usage
   - Most useful when you frequently search a table based on specific columns
   - Speed up **sorting** operations in `ORDER BY` clauses

### Example Scenario

> This scenario was provided by [ChatGPT](https://chat.openai.com)

You have a 'Customer' ( _stealing my scenario WTF_ ) table with millions of records.
Without any index, searching for specific customer by `name` would require scanning **every** _record_.

Here comes _indexes_ to the rescue ( _Yeeeeaahhhhh_ ).

If you create an index on the `name` column, the database will quickly retrieve the relevant row(s) using the index.

## Create Index

> [!NOTE]
> The way the lecturer wrote the `CREATE INDEX` command is slightly ( _I find it very different_ ) compared to the way ChatGPT gave me.
>
> > I will include both I guess

### ChatGPT's Command

```SQL
CREATE [UNIQUE] [CLUSTERED|NONCLUSTERED] INDEX index_name
ON schema_name.table_name (column_name1 [ASC|DESC], column_name2 [ASC|DESC], ...);
```

> [!INFO]
> Where things '_constraints_' / '_features_' that are in the `[]` are optional
>
> > Like if you want to use them then you can use them.

### Lecturer's Command

```SQL
CREATE INDEX index_name ON schema_name.table_name ( column_name );
```

> I find ChatGPT's version better; yes it might not be simpler. But it give you all the possible ways to be able to do it.

### Lecturer's Command Example

Lets take the example below $\downarrow$

> I will only be including the lecturer's example.
> This is because I am getting a bit lazy now and also I need to start doing other module's notes and stuff.
> I am getting fucked _left, right_ and _center_... _Not to mention the front also_...

```SQL
CREATE INDEX StaffNoInd ON Staff (staffNo);
```

#### Its Default Values

If you take a look ( _yes... a "look" not a "glance"_ ); you will see that we have many options.
But what are the _default options_ if you do **not** specify them like the lecturer did?

> I will be writing in Bullet Points

- It is **not** `UNIQUE` by default
- `NONCLUSTERED` by default
- The default `schema_name` will be `dbo` ( _open you eyes in the Object Explorer you will see it_ )
- Similar to `ORDER BY`; it will be `ASC` by default

> [!SUCCESS]
> Fucking Finally, I have managed to create a nice and with actual examples and possibilities with output as `.csv` files.
> I am done with this now, need to move on
>
> > Will come back to this later on!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
