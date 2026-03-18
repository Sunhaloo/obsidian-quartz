---
id: SQL Commands - Data Manipulation Language - SELECT
aliases: SQL Commands - DML ( The SELECT Statement )
tags:
  - SQL
  - uni
  - db
author: S.Sunhaloo
date: 2024-08-15
status: Completed
---

> [!INFO]
> The Lecture Notes / Slides are found in "[[Database Systems - SQL ( DML - Part 1 ).pdf]".
> The _sub-heading_ for the `SELECT` statement starts at page 17.

## List of Contents

- [[#The SELECT Command]]
  - [[#Template]]
    - [[#Literals]]
  - [[#Examples]]
    - [[#Display Everything]]
    - [[#Displaying Everything with Specific Output Amount]]
      - [[#Displaying Everything Within a Range]]
    - [[#Display Specific Rows and Specific Columns]]
      - [[#The Alias / AS Command]]
      - [[#Display Without Repetition]]
    - [[#Calculated Fields]]
    - [[#Comparison Search Condition]]
      - [[#The WHERE Clause]]
    - [[#Compound Comparison Search Condition]]
    - [[#Range Search Condition]]
    - [[SQL Commands - Data Manipulation Language - Pattern Matching] $\leftarrow$ Found in Another File / Note
    - [[#NULL Search Condition]]
      - [[#Example of Query with NULL Values]]
    - [[#Ordering of Columns]]
      - [[#Single Column Ordering]]
      - [[#Multi-Column Ordering]]

---

> [!NOTE]
> Before I start; I would like to say something.
> There are things that I did not know that we could do in SQL ( _insert mind-blown meme here_ )
> Like there is so much that we did **not** learn in HSC.

# The SELECT Command

## Template

Now look at this template that our Lecturer gave us.

```SQL
SELECT [DISTINCT | ALL] {* | [columnExpression [AS newName] [, ...]}
FROM TableName [alias] [, ...]
[WHERE condition]
[GROUP BY columnList] [HAVING condition]
[ORDER BY columnList]
```

Then I went to check Microsoft's SQL Select statement documentation over at: https://learn.microsoft.com/en-us/sql/t-sql/queries/select-transact-sql?view=sql-server-ver16.

I found that it is _similar_ but not the same! Here is the template given by Microsoft $\downarrow$:

```SQL
<SELECT statement> ::=
    [ WITH { [ XMLNAMESPACES ,] [ <common_table_expression> [,...n] ] } ]
    <query_expression>
    [ ORDER BY <order_by_expression> ]
    [ <FOR Clause> ]
    [ OPTION ( <query_hint> [ ,...n ] ) ]
<query_expression> ::=
    { <query_specification> | ( <query_expression> ) }
    [  { UNION [ ALL ] | EXCEPT | INTERSECT }
        <query_specification> | ( <query_expression> ) [...n ] ]
<query_specification> ::=
SELECT [ ALL | DISTINCT ]
    [TOP ( expression ) [PERCENT] [ WITH TIES ] ]
    < select_list >
    [ INTO new_table ]
    [ FROM { <table_source> } [ ,...n ] ]
    [ WHERE <search_condition> ]
    [ <GROUP BY> ]
    [ HAVING < search_condition > ]
```

> [!WARNING]
> As you can see in the above $\uparrow$ code block; we have the characters `::=`.
> Even in HSC, I have never used it ( _who the fuck in `::=`_? ).
> Hence, I will only be focusing on what I learned in HSC and with the Lecturer.

### Literals

> [!TIP]- What are Literals?
> They are constant **values** assigned to constant **variables**.

#### Non-Numeric Literals

What do you do if you want to display a "_string_" in a _Programming Language_.

Let's say that we are using [[Learning/Python/Python Data View| Python]; we would do something like this

```python
# strings are written within the '"' character
print("Hello World")
```

This also applies to SQL and here instead of using the `"` character. We are simply going to use the `'` character.

```SQL
-- strings are written within the ''' character
-- it should look something like this v
city = 'Port Louis'
```

#### Numeric Literals

> Well, from the above $\uparrow$ example; I guess you are already familiar with writing **numeric literals**

> [!TIP]
> If you are really going to learn / understand the `SELECT` command; then I suggest we start "_seeing_" and **writing** <span style="color: green;"> Examples</span> !!!

---

# Examples

## Template for Simple SELECT Commands

```SQL
SELECT col1, col2, col3, ... FROM table_name;
```

### Display Everything

To display every single fucking shitty values / fields; we can simply run the following command $\downarrow$:

> In this example; we are going to retrieve every data / fields from the 'Staff' table.
> Again, please refer to [[University Data View ( L1S1 )#Database Systems Labsheets| Database Labsheets] if you have not created the tables and inserted the values.

```SQL
SELECT * FROM Staff;
```

> [!TIP] Output of our little Statement / Command
> We should get every values from that table!
>
> ```csv
> staffNo,fname,lname,position,sex,DOB,salary,branchNo
> SA9,Mary,Howe,Assistant,F,1970-02-19,9000,B007
> SG14,David,Ford,Supervisor,M,1958-03-24,18000,B003
> SG37,Ann,Beech,Assistant,F,1960-11-10,12000,B003
> SG5,Susan,Brand,Manager,F,2040-06-03,24000,B003
> SL21,John,White,Manager,M,2045-10-01,30000,B005
> SL41,Julie,Lee,Assistant,F,1965-06-13,9000,B002
> ```

### Displaying Everything with Specific Output Amount

We just learned that we can use the `*` operator to _select_ all the **records** with all of its **fields** from a table.

Now, listen to this... What if we have a table that have a lot of records like in the thousands. We just want to get **some** _records_ so that we can see how the **data** looks like in that specific table.

> How we would do that?

This is achieved using the `TOP` keyword! Take a look at this $\downarrow$:

```SQL
-- select all fields for first 3 records only from 'Staff'
SELECT TOP 3 * FROM Staff;
```

> [!WARNING] Yes!
> The `TOP` keyword will **start** at the _first_ record **to** that _specified number_!

> [!TIP] Therefore, Our Output Should Be:
>
> ```csv
> staffNo,fname,lname,position,sex,DOB,salary,branchNo
> SA9,Mary,Howe,Assistant,F,1970-02-19,9000,B007
> SG14,David,Ford,Supervisor,M,1958-03-24,18000,B003
> SG37,Ann,Beech,Assistant,F,1960-11-10,12000,B003
> ```

#### Displaying Everything Within a Range

> What about a **Specific Range**?
> Well, let's get right into it!

Now, with this one; we are going to have to use the `OFFSET` and `FETCH` keyword. But, additionally, we are going to have to follow a _series_ of **steps**.

> Let me list them our for you!

1. `SELECT` everything with our trusty `*` operator
2. `ORDER BY` a specific column in found in table ( <strong> <span style="color: red;"> You must include this!!!</span> </strong> )
3. Use `OFFSET` to **skip** $x$ amount of records from the top
4. Use `FETCH` to actually _retrieve_ the desired amount of records

With this knowledge, let's try to retrieve the record `3`, `4` and `5`!

```SQL

```

> [!TIP] Our Correct Output!
>
> ```csv
> SG37,Ann,Beech,Assistant,F,1960-11-10,12000,B003
> SG5,Susan,Brand,Manager,F,2040-06-03,24000,B003
> SL21,John,White,Manager,M,2045-10-01,30000,B005
> ```
>
> If you take a look above $\uparrow$ at our _full_ 'Staff' table; you should see that we clearly retrieved `3`, `4` and `5`!

### Display Specific Rows and Specific Columns

Now, selecting every rows and columns from a **small** table is cool!

But what if you are selecting a table with a million values. BTW, this is not a joke, there might be a billion values in a table.

Like the big, big companies like Google and other **must** have databases with bi-zillion amount of data.

#### Display ID, Names and Salary of all Staffs

```SQL
SELECT staffNo, lname, fname, salary FROM Staff;
```

> [!TIP] Output of Selecting Specific Rows / Columns
> Here we are going to get **every** _rows_ but <span style="color: red;"> not</span> every _fields_
>
> ```csv
> staffNo,lname,fname,salary
> SA9,Howe,Mary,9000
> SG14,Ford,David,18000
> SG37,Beech,Ann,12000
> SG5,Brand,Susan,24000
> SL21,White,John,30000
> SL41,Lee,Julie,9000
> ```

#### The Alias / AS Command

Now, look at the output again from our previous statement that we ran!

In the header of the `.csv` file you will see something like this:

```csv
staffNo,lname,fname,salary
```

Hence, in when the person is looking at the result ( _like in SQL Management Studio_ ); he will see something like this:

```csv
staffNo	lname	fname	salary
SA9	    Howe	Mary	9000
SG14	Ford	David	18000
SG37	Beech	Ann	    12000
SG5	    Brand	Susan	24000
SL21	White	John	30000
SL41	Lee	    Julie	9000
```

> But what if I don't want to display `staffNo`, `lname` and `fname` and add my own **temporary** thing?
> Because here `lname` could meaning **somethings** like "_Last Name_" or "_Loser's Name_"
> I think you get the point

##### Here comes the AS Command

It allows us to change the _field_ name **temporarily**.

> [!WARNING]
> **Temporarily** and **not** permanently!
> It will not change the actual _structure_ of the table; it simply provides a more readable way when selecting information.

Therefore if we run the same command as above $\uparrow$, but this time using `AS`:

```SQL
SELECT staffNo AS Staff_Number, lname AS Last_Name, fname AS First_Name, salary AS Salary FROM Staff;
```

Hence, out output should be as follows $\downarrow$:

```csv
Staff_Number	Last_Name	First_Name	Salary
SA9	    Howe	Mary	9000
SG14	Ford	David	18000
SG37	Beech	Ann	    12000
SG5	    Brand	Susan	24000
SL21	White	John	30000
SL41	Lee	    Julie	9000
```

> [!SUCCESS]
> As you can see the header _values_ have changed!
>
> ```csv
> Staff_Number	Last_Name	First_Name	Salary
> ```

### Display Without Repetition

#### Display With Repetition

Let's go ahead and display all the values for `propertyNo` from the 'Viewing' table.

```SQL
SELECT propertyNo FROM Viewing;
```

Take a look at the output after running the statement above $\uparrow$:

```csv
propertyNo
PA14 <--- as you can see repetition
PG36
PG4 <---
PA14 <---
PG4 <---
```

#### The DISTINCT Command

The `DISTINCT` command will **not** _display_ the repetition.

```SQL
SELECT DISTINCT propertyNo FROM Viewing;
```

We should have no repetition in our output $\downarrow$:

```csv
propertyNo
PA14
PG36
PG4
```

> Here we can clearly see that the repetition has been _removed_ when **running** the `SELECT` command.

> [!INFO]
> It will _not_ "<span style="color: green;"> display</span> " and **not** "<span style="color: red;"> remove</span> " from the table!

> [!WARNING] Warning
> What if we have multiple field / columns to display?
> You would think that we need to write the SQL statement like so:
>
> ```SQL
> SELECT DISTINCT col1, DISTINCT col2 FROM table_name;
> ```
>
> > [!BUG] This is Wrong!!!
>
> In SQL, the `DISTINCT` keyword can only be used **once**!
> Hence to avoid repetition, we can simply write
>
> > [!SUCCESS] Valid Code
> >
> > ```SQL
> > SELECT DISTINCT col1, col2, ... FROM table_name;
> > ```

### Calculated Fields

Do you remember the _Calculated Fields / Values_ from [[Microsoft Access ( 2007 )]?

> I know you don't!

So basically sometimes we need to change the values of one or some fields <span style="color: red;"> <strong> without</strong> </span> changing the values changing the _original_ values from the table... _I don't know the specific reasons why a company would do so_.

> But still, I need to know "_how_" we do it!

Normally, when we are create a **Calculated Field**; as the name suggest, its a field where we normally ( _most of the time_ ) perform mathematical operations on some [[#Numeric Literals | numeric] fields.

> Hence, instead of giving out a template; I will go straight to the Example!

#### Display Monthly Salary of All Staff

In our 'Staff' table, we have a `salary` field that keep track of the yearly salary of our customers

> [!INFO]- Yearly Salary of Staff
> I need to place this here just to show you the different
> Run the following statement $\downarrow$:
>
> ```SQL
> SELECT staffNo, salary FROM Staff;
> ```
>
> Here is the output after running that $\uparrow$ statement:
>
> ```csv
> staffNo,salary
> SA9,9000
> SG14,18000
> SG37,12000
> SG5,24000
> SL21,30000
> SL41,9000
> ```

Therefore to display the **monthly** salary instead of the yearly one, we can simply do:

```SQL
SELECT staffNo, (salary / 12) FROM Staff;
```

> No need to add the ( calculated ) field inside `()`!

Thus, we are now going to get a different output:

```csv
staffNo,(No column name)
SA9,750
SG14,1500
SG37,1000
SG5,2000
SL21,2500
SL41,750
```

> Bruh! these people don't get paid!!!

> [!NOTE]
> Did you see something in the output when we calculated the **monthly** salary of the staffs?
> Your shitty eyes might not have seen it; so let me show it to you:
>
> ```csv
> staffNo,(No column name)
> ```
>
> As you can see, we have `(No column name)`.
> This is literally like MS Access; where we need to provide the column name.
> Hence, this is why I showed you the [[#Here comes the AS Command | AS] command earlier.
> Hence, instead of writing / typing the previous statement ( _whatever the fuck you want_ ): we can do something like this:
>
> ```SQL
> -- did not add calculated field inside () to show it works
> SELECT staffNo, salary / 12 AS Monthly_Salary FROM Staff;
> ```
>
> > [!SUCCESS]
> > Hence, this will be the header of the `.csv` file $\downarrow$:
> >
> > ```csv
> > staffNo	Monthly_Salary
> > ```

### Comparison Search Condition

#### The WHERE Clause

> "[and his name is ~~John Cena~~ WHERE](https://www.youtube.com/watch?v=2D-ZO2rGcSA)"
> I think we all like even a baby / monkey / your mama ( [we got him](https://www.youtube.com/watch?v=m6gWWOKTcYM) )

We use the `WHERE` clause to specify certain search conditions.

##### Staffs with Salary More than 10 000

```SQL
SELECT staffNo, fname, lname, position, salary FROM Staff
WHERE salary > 10000;
```

> [!TIP]- Staffs with Salary More than 10 000
>
> ```csv
> staffNo,fname,lname,position,salary
> SG14,David,Ford,Supervisor,18000
> SG37,Ann,Beech,Assistant,12000
> SG5,Susan,Brand,Manager,24000
> SL21,John,White,Manager,30000
> ```

##### Simple Comparison Operators

| Operator | Meaning                  |
| -------- | ------------------------ |
| $=$      | Equal                    |
| $\lt\gt$ | Not Equal To             |
| $\lt$    | Less Than                |
| $\gt$    | Greater Than             |
| $\lt=$   | Less Than OR Equal To    |
| $\gt=$   | Greater Than OR Equal To |

##### Rules for Evaluating Conditional Expressions

- Expression is evaluated **from** _left_ **to** _right_ $\rightarrow$
- Sub-expressions in **brackets** are evaluated **first**
- `NOT`s are evaluated **before** `AND`s and `OR`s
- `AND`s are evaluated **before** `OR`s

> [!TIP]
> The use of parentheses is always recommended in order to remove any possible ambiguities.

### Compound Comparison Search Condition

> Think of this like an `if... and/or...then` condition.

#### Display All Branch Offices in London / Glasgow

This will how the command will be $\downarrow$:

```SQL
SELECT * FROM Branch
WHERE city = 'London' OR city = 'Glasgow';
```

> [!TIP]- Branch Offices in London / Glasgow
> We should only get the _details_ of Branch Offices in **London** and **Glasgow** only!
>
> ```csv
> branchNo,street,city,postcode
> B002,56 Clover Dr,London,NW10 6EU
> B003,162 Main St,Glasgow,G11 9QX
> B005,22 Deer Rd,London,SW1 4EH
> ```
>
> As you can see only outputs offices where they are located in either 'London' or 'Glasgow'

### Range Search Condition

There are 2 ways do perform a **range** search condition.

You are your regular:

1. [[#Simple Comparison Operators | Comparison Operators]]
2. `BETWEEN` Keyword

#### Using Comparison Operators

Let's go ahead and find all the staff with a `salary` between 20 000 and 30 000. In this, example, we are going to display all the _details_ for those specific staffs.

```SQL
SELECT * FROM Staff
WHERE salary > = 20000 AND salary <= 30000;
```

> I will show you the output after I show you how the above $\uparrow$ command will become when using the `BETWEEN` keyword.

#### Using `BETWEEN` Keyword

If we want to use the `BETWEEN` keyword for the above $\uparrow$ statement; we can easily convert the _operators_ to `BETWEEN` like so:

```SQL
SELECT * FROM Staff
-- no need to type salary and the comparison operators
WHERE salary BETWEEN 20000 AND 30000;
```

> [!TIP] Hence, the output after running the above _results_...
> Using the first code block:
>
> ```csv
> staffNo,fname,lname,position,sex,DOB,salary,branchNo
> SG5,Susan,Brand,Manager,F,2040-06-03,24000,B003
> SL21,John,White,Manager,M,2045-10-01,30000,B005
> ```
>
> Using the second code block:
>
> ```csv
> staffNo,fname,lname,position,sex,DOB,salary,branchNo
> SG5,Susan,Brand,Manager,F,2040-06-03,24000,B003
> SL21,John,White,Manager,M,2045-10-01,30000,B005
> ```
>
> > As you can see its the same shit!

### List Search Condition

Remember that when we **created** our '[[Database Systems - Labsheet 1 ( L1S1 )#Staff Table| Staff]' table, we added the constraint $\downarrow$:

```SQL
-- where `position` could either be:
-- 'Manager' or 'Supervisor' or 'Assistant'
CONSTRAINT chk_position_tblStaff CHECK ( position IN ( 'Manager', 'Supervisor', 'Assistant' ) )
```

Now, we want to display the staffs where the position is "_Manager_" and "_Supervisor_".

Hence, we can use the following command below to show these people's `staffNo`, Last Name, First Name and lastly `position`

```SQL
SELECT staffNo, lname AS Last_Name, fname AS First_Name, position FROM Staff
-- check this "list" of values.
WHERE position IN ( 'Manager', 'Supervisor' );
```

> [!TIP]- Output of Staff that are Managers and Supervisors
> We should get a result that looks something like this $\downarrow$:
>
> ```csv
> staffNo,Last_Name,First_Name,position
> SG14,Ford,David,Supervisor
> SG5,Brand,Susan,Manager
> SL21,White,John,Manager
> ```

> [!INFO]
> We could have done the same thing but instead using the `IN` keyword / command; we used the `OR` keyword... Hence, the statement would have looked like this:
>
> ```SQL
> SELECT staffNo, lname AS Last_Name, fname AS First_Name, position FROM Staff
> -- using `OR` keyword instead of the usual `IN`
> WHERE position = 'Manager' OR position = 'Supervisor';
> ```
>
> This will output the **same** result at the above $\uparrow$ command that we used previously.
> But then why use a _list of values_.
> Well, here comes one of my favourite word ( _insert drum roll please_ )... "**Performance**"
> While the `OR` keyword is good, its not really efficient in terms of typing and performance if the search condition is large ( _having multiple `OR ... OR ... OR ... OR ...`_ ) and if the table has many values.

### NULL Search Condition

Similar to [[Python Language | Python]'s `None` _reserved_ word. We can have `NULL` in SQL where we can specify if a "_cell_" ( _like a particular record's field_ ) is either `NULL` or not!

> [!NOTE]
> If you have a lot of `NULL` values in your Tables / Databases in general...
> Then your Databases / Tables are **shit**
>
> "_Why can't we have `NULL` values?_"
>
> In general if you table has a lot of `NULL` values; this means that you are having / will have:
>
> - Inconsistency of Data
> - Decreases the Storage Space

#### Example of Query with NULL Values

Here, we will find the all the "_viewings_" on property 'PG4' where a 'comment' has not been supplied.

```SQL
SELECT clientNo, viewDate FROM Viewing
WHERE propertyNo = 'PG4' AND comment IS NULL;
```

> [!TIP]- Client who did Not add a Comment
> Here is the results after running the above $\uparrow$ statement:
>
> ```csv
> clientNo,viewDate
> CR56,2004-05-26
> ```

> [!WARNING] Friendly Warning
> Here we do <span style="color: red;"> not</span> use the `=` character to find if the value is `NULL` or not.
>
> ```SQL
> -- this is WRONG!!!
> comment = NULL
> ```
>
> The <span style="color: green;"> correct</span> way is like we have used above $\uparrow$ in the example.
>
> ```SQL
> -- this is correct
> comment IS NULL
> ```

### Ordering of Columns

Well, we did this in HSC; hence, I think I am going to continue to explain the other stuff.

#### Templates

> Take this _template_ as a grain of salt.
> Because what we need to know and see are the examples; as with the examples we are going to see how its working.

##### Single Column Ordering

> [!INFO]
> If you do **not** specify if it is going to be `ASC` or `DESC`...
> Just know that by _default_ it will **always** be in a _random_ order.

```SQL
SELECT column1, column2, column3, ... FROM table_name
ORDER BY column_to_order [ASC|DESC];
```

Let's take some examples:

> Yes, I am taking the same examples from the Lecturer's slides because I want to not like "_fake_" the result that we got!
> See, who told you that I am a bad person... _fucking shitter_!

```SQL
SELECT staffNo, branchNo, lname AS Last_Name, fname AS First_Name FROM Staff
-- orders the table by `salary` column
-- which is descending
ORDER BY salary DESC;
```

Here is the above $\uparrow$ command's output:

```csv
staffNo,branchNo,Last_Name,First_Name
SL21,B005,White,John
SG5,B003,Brand,Susan
SG14,B003,Ford,David
SG37,B003,Beech,Ann
SA9,B007,Howe,Mary
SL41,B002,Lee,Julie
```

---

```SQL
SELECT propertyNo, ptype, room, rent FROM PropertyForRent
-- orders the table by `ptype` column
-- which is ascending
ORDER BY ptype;
```

> [!NOTE]
> If you just place the **column name** only and do not specify the **order**.
> Then by default it will be `ASC`.
>
> > BTW I said "_do not specify the **order**_"
> > If you do not add the `ORDER BY` "_constraint_" ( _I guess_ ); then the fucking order will be fucking random.

And here again, is the above $\uparrow$ command's output:

```csv
propertyNo,ptype,rooms,rent
PG16,Flat,4,450
PG36,Flat,3,375
PG4,Flat,3,350
PL94,Flat,4,400
PG21,House,5,600
PA14,House,6,650
```

##### Multi-Column Ordering

```SQL
SELECT column1, column2, column3, ... FROM table_name
ORDER BY column1_to_order [ASC|DESC], column2_to_order [ASC|DESC], ...;
```

Now, I have to tell you something... "_I don't understand the lecture slide_"

> [!TIP] Lecturer's Note
>
> > This is found on page 42
> > This is what the Lecturer wrote:
>
> - Four flats in this list ( _referring to 'PropertyForRent' table_ )
>   - As no minor key specified, system arranges these rows in any order it chooses.
>   - To arrange the in order of `rent`, specify minor order
>
> Before I decipher this $\uparrow$; let me go ahead and show you the statement and also the output.

Hence, we are going to have something that look like this:

```SQL
SELECT propertyNo, ptype, rooms, rent FROM PropertyForRent
-- order by:
-- ptype ---> ASC
-- rent ---> DESC
ORDER BY ptype, rent DESC;
```

> [!TIP] Output of Multi-Column Ordering Example
> Here is the output after running the statement $\uparrow$:
>
> ```csv
> propertyNo,ptype,rooms,rent
> PG16,Flat,4,450
> PL94,Flat,4,400
> PG36,Flat,3,375
> PG4,Flat,3,350
> PA14,House,6,650
> PG21,House,5,600
> ```

###### My Understanding on Multi-Column Ordering

If we take a look at this statement $\downarrow$:

```SQL
ORDER BY ptype, rent DESC;
```

As `ptype` is **first** and `rent` is **second**.

It will first execute the first `ORDER BY` and then proceed to the second `ORDER BY`; so on and so forth.

1. Primary Ordering
   - The results are **first** sorted by `ptype`
   - Meaning all rows with the same `ptype` value will be grouped together
2. Secondary Ordering
   - Now, within each group of rows that have the same `ptype`
     - Rows are then sorted by `rent` in `DESC` order
   - Hence, for each specific `ptype`
     - Properties with higher rent will appear before those lower rent

> [!TIP] "_Minor_"?
> Hence, the "_minor key_" and "_minor order_" was basically that $\uparrow$:
>
> - Primary Ordering
> - Secondary Ordering
>
> > This is not the "_minor_" that you are thinking BTW!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!
