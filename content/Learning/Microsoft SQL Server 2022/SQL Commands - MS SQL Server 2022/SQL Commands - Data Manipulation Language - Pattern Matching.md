---
id: SQL Commands - Data Manipulation Language - Pattern Matching
aliases:
  - SQL Commands - DML ( SELECT ---> Pattern Matching )
tags:
  - SQL
  - uni
  - db
  - uom
author: S.Sunhaloo
date: "2024-09-02"
status: Completed
---

> [!INFO]
> This is actually part of the file / note [[SQL Commands - Data Manipulation Language - SELECT]]
> But I did not really understood it well when we did it in Lecture.
> Hence, I will be making a separate note and getting good that this "*pattern matching*" thing.
> Again the notes for this is found on; Page 35 in the "[[Database Systems  - SQL ( DML - Part 1 ).pdf]".

## List of Contents

- [[#What is Pattern Matching?]]
- [[#Pattern Matching in SQL]]
	- [[#Pattern Matching Symbols]]
- [[#Scenarios]]
	- [[#Scenario 1 With the '%' Symbol]]
	- [[#Scenario 2 With the '_' Symbol]]
	- [[#Scenario 3 Escape Character]]

---

# What is Pattern Matching?

> [!TIP]- Resources
> - Websites:
> 	- https://en.wikipedia.org/wiki/Pattern_matching

> [!NOTE]
> I will not get into the details to much.
> But just know that this is used to match certain *patterns* like "*strings*" or *formally* known as [[SQL Commands - Data Manipulation Language - SELECT#Non-Numeric Literals | Non-Numeric Literals]]

Basically what if we have some data that look like this:

```console
# this is NOT a .csv file

Address Field / Columns
# the `Address` field has all of these values below
Monza, Italy, Europe
Nürburgring – Nordschleife, Germany, Europe
Road America, Wisconsin, United States
```

What if we wanted to find all the race tracks that are found in 'Europe'?

This is where **pattern matching** comes it because in this *sea of strings*; we can specify to find where we have 'Europe' in that *sea of strings*.

# Pattern Matching in SQL

## Pattern Matching Symbols

In [[Microsoft SQL Server 2022 Data View | SQL]; we have 2 symbols ( *or ways* ) that we can pattern match.

> [!TIP] The `%` Symbol
> This means that we can search for a **sequence of 0 or more characters**.

> [!TIP] The `_` Symbol
> This means that we can search of for any single character.

> They will make more sense when we are going to execute them
> I do hope so; because when I did that in lecture I was fucking lost!

## Scenarios

### Scenario 1: With the '%' Symbol

Remember when we were [[Database Systems - Labsheet 1 ( L1S1 )| creating] our tables; we used a check constraints for some of our Primary Key field.

> Let me show you again

```SQL
-- branch table
CONSTRAINT start_with_PK_tblBranch CHECK ( branchNo LIKE 'B%' )
-- staff table
CONSTRAINT start_with_PK_tblStaff CHECK ( staffNo LIKE 'S%' )
```

> There were also for `propertyNo`, `clientNo` and others
> But this is just for me to remind you what we did!

> [!NOTE] Therefore, what does the `B%` or `S%` actually means?
> It means that when we are entering the data for `branchNo` and `staffNo`; they should look something like this:
>
> > We did `branchNo CHAR(4)` and `staffNo CHAR(4)`; hence we can only add *total length* of 4 characters
>
> - Branch Table `branchNo` data:
> 	- `B001`
> 	- `B123`
> 	- `B0A7`
> - Staff Table `staffNo` data:
> 	- `SL34`
> 	- `S509`
> 	- `S1L2`

As you can see all the **values** of `branchNo` and `staffNo`; all starts with `B` and `S` respectively.

> [!SUCCESS] Therefore, we conclude
> That something like `B%` means that:
>
> - The **first** character must be `B`
> 	- But the *rest* of the string can be **anything**
> 	- But remember if we are talking about insertion of values ( *which we are not here* ) then we would need to pay attention to the *length* of characters we can add

> [!TIP] Last Character
> Again, we know that `%` means any sequence of 0 or more characters.
> Hence, we can do something like this:
>
> ```SQL
> LIKE '%e';
> ```
>
> What does `%e` could possibly mean?
> From what we know we can have 0 or many characters with the `%` sign and is before the character `e`.
>
> $\Rightarrow$ Hence, this means that we can have **any** sequence of characters of *length* of at **least** 1; with the **last** character as `e`!

> [!TIP] Before and After
> From the above $\uparrow$ '*tip*', we can conclude that `LIKE %e` means sequence of character is on the *left* and the **last** character is `e`.
> But what about...
>
> ```SQL
> LIKE %shit%
> ```
>
> Applying the same principles, we are going to have:
> $\Rightarrow$ Any sequence of 0 or more characters to the **left** of 'shit' and additionally, any sequence of 0 or more characters to the **right** of shit.

> [!NOTE]
> I have check all of these values by inserting them in the table.
> They did not pose any sort of problem.

#### Example for Scenario 1

```SQL
SELECT ownerNo, lname AS Last_Name, fname AS First_Name, address AS Address, telNo AS Telephone_Number
FROM PrivateOwner
WHERE address LIKE '%Glasgow%';
```

> This again, should search for the 'Glasgow' in the *sea of strings*
> Or as the Lecturer said: "*sequence of characters, of length containing `Glasgow`*"

> [!TIP] Output of Scenario 1 - Example
> This should be the output after running the statement above $\uparrow$:
>
> ```csv
> ownerNo,Last_Name,First_Name,Address,Telephone_Number
> CO40,Murphy,Tina,"63 Well St, Glasgow G42",0141-943-1728
> CO87,Farrel,Carol,"6 Achray St, Glasgow G32 9DX",0141-357-7419
> CO93,Shaw,Tony,"12 Park Pl, Glasgow G4 0QR",0141-225-7025
> ```

### Scenario 2: With the '\_' Symbol

As we have said from the [[#Pattern Matching Symbols | beginning], the `_` character means we can search of any **single** character.

It's **not** like `%` where it can *be* a sequence of 0 or more characters.

Instead, it like you have a word with 4 characters and you are search for that for 4 characters.

Let's take the example for `branchNo` again.

> Yes, I am running out of ideas.
> For more ideas, I should have looked on the net!
> That would have been so much better.

As you know the field of `branchNo` contains values such as:

- `B003`
- `B005`
- `B007`

Hence, we can do something like `B___` to find the exact number of characters.

> I say we get on with the examples
> Because I don't even know what I am saying anymore.

#### Example for Scenario 2

> [!WARNING]- Friendly Warning
> She really give any examples from the **lecture slides**.
> Nevertheless, like I have said, she did gave some examples in class where I completely fucked up!

##### Example 1: 'Branch' Table and `branchNo`

```SQL
SELECT * FROM Branch
WHERE branchNo LIKE '___7';
```

> [!TIP] Output of Scenario 2 - Example 1
> Like I want it to return this record:
>
> ```csv
> branchNo	street	city	postcode
> B007	16 Argyll St	Aberdeen	AB2 3SU
> ```
>
> Here is the output after running the above $\uparrow$ statement:
>
> ```csv
> branchNo,street,city,postcode
> B007,16 Argyll St,Aberdeen,AB2 3SU
> ```
>
> > [!SUCCESS] Fucking Success!!!
>

##### Example 2: 'PrivateOwner' Table and `address`

> This is going to be a really shit example
> But I think **I** am getting the point now!

```SQL
SELECT * FROM PrivateOwner
WHERE telNo LIKE '0141-___';
```

> [!BUG] Shit!
> > [!TIP] Output of Scenario 2 - Example 2
> > This should return 3 records; I guess
> > 
> > ```csv
> > ownerNo	fname	lname	address	telNo
> > ```
>
> > It did **not** output shit!!!
>
> Now I think I know where the problem is coming from!
> Let's try again
>
> ```SQL
> SELECT * FROM PrivateOwner
> WHERE telNo LIKE '0141-%';
> ```
>
> > [!SUCCESS]
> > This is correct! 出力を見てみましょう $\downarrow$
> > 
> > ```csv
> > ownerNo,fname,lname,address,telNo
> > CO40,Tina,Murphy,"63 Well St, Glasgow G42",0141-943-1728
> > CO87,Carol,Farrel,"6 Achray St, Glasgow G32 9DX",0141-357-7419
> > CO93,Tony,Shaw,"12 Park Pl, Glasgow G4 0QR",0141-225-7025
> > ```
>

From this mistake above $\uparrow$ that I made, I can now understand why I could not do it in the Lecture / Class and here also?
Because I am fucking dumb!

> Let's take another example!

##### Example 3: 'Branch' Table and `city`

```SQL
SELECT * FROM Branch
WHERE city LIKE 'L_____';
```

> [!TIP] Output of Scenario 2 - Example 3
> > I fucking got it!
>
> This will be and output after running the above $\uparrow$ statement:
>
> ```csv
> branchNo,street,city,postcode
> B002,56 Clover Dr,London,NW10 6EU
> B005,22 Deer Rd,London,SW1 4EH
> ```

### Scenario 3: Escape Character

Now that if we wanted to search for something like `15%` ( *again I am taking example from the Lecture Slides* ).

Like it will go ahead and search for something like `15sfdg` for example. Hence, how can you include that `15%`?

> From the `15%` example $\downarrow$

This is done using `LIKE '15#%'ESCAPE'#'`

Let's take the same example, because I don't really really understand why you would include '%' as a part of a value in a database / table.

##### Example: Escape Character

Just run these following Code Block!

```SQL
-- insert shit values into table Branch
INSERT INTO Branch ( branchNo, street, city, postcode ) VALUES ( 'BTTT', 'testing', '15%', 'testing' );

-- check if record has been entered
SELECT * FROM Branch
WHERE branchNo = 'BTTT';

-- find '15%'
SELECT * FROM Branch
WHERE city LIKE '15#%'ESCAPE'#';
```

> [!TIP] Output of Scenario 3 ( Escape Character )
> This should be the output after execution
>
> ```csv
> branchNo,street,city,postcode
> BTTT,testing,15%,testing
> ```

---

# Exact Matching v/s Pattern Matching

## Example of Exact Matching

```SQL
SELECT * FROM Staff
WHERE fname = 'Julie';
```

> [!TIP]- Output of Exact Matching
> In this case, we should get only 1 record as output $\downarrow$:
>
> ```csv
> staffNo	fname	lname	position	sex	DOB	salary	branchNo
> SL41	Julie	Lee	Assistant	F	1965-06-13	9270	B002
> ```

## Example of Pattern Matching

```SQL
SELECT * FROM Staff
WHERE fname LIKE 'J';
```

> [!TIP]- Output of Pattern Matching
> In this case, we are going to have 2 records as output $\downarrow$:
>
> ```csv
> staffNo	fname	lname	position	sex	DOB	salary	branchNo
> SL21	John	White	Manager	M	2045-10-01	32445	B005
> SL41	Julie	Lee	Assistant	F	1965-06-13	9270	B002
> ```

> [!NOTE] Takeaways!
> > Not the box that you take food with you BTW...
>
> Basically if you have an **exact value / record** in mind and you know that you can easily find it or your table is small!
> You can use **Exact Matching** ( `=` )!
>
> Nevertheless, what if your table has a *million* values / records.
> And in our case, you have multiple `Julie`, then you are going to need to use **Pattern Matching**!

> [!SUCCESS] I think we are Done!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!
