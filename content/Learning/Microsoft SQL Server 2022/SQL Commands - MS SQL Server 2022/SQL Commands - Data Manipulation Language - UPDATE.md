---
id: SQL Commands - Data Manipulation Language - UPDATE
aliases:
  - SQL Commands - DML ( The UPDATE Statement )
tags:
  - SQL
  - uni
  - db
author: S.Sunhaloo
date: "2024-08-30"
status: Completed
---

> [!INFO]
> The Lecture Notes / Slides are found in "[[Database Systems - SQL ( DML - Part 1 ).pdf]".
> The _sub-heading_ for the `SELECT` statement starts at page 12.

## List of Contents

- [[#The Update Command]]
  - [[#General Template for UPDATE Command]]
  - [[#Examples using UPDATE Command]]
    - [[#Update All Records For A Field]]
    - [[#Update Specific Records For A Field]]
    - [[#Update Multiple Columns]]

---

> [!WARNING]
> We are talking about the `UPDATE` command here! <span style="color: red;"> <strong> Not</strong> </span> the [[SQL Commands - Data Definition Language ( DDL )#Alter Command| `ALTER`] command.
>
> The `UPDATE` command will change the **values** _inside_ a table while the `ALTER` command will change the **structure** of a table.
>
> > Remember this well!!!

# The Update Command

Like I have said, we can use `UPDATE` to change the **value(s)** that is found inside of a table.

## General Template for UPDATE Command

Here is the _template_ for the `UPDATE` command below $\downarrow$:

```SQL
UPDATE table_name
SET col1 = new_value1,
	col2 = new_value2,
	col3 = new_value3,
	...
WHERE search_condition;
```

> [!NOTE]- The `WHERE` Clause
> Now, the `WHERE` clause is optional.
> We have 2 possibilities:
>
> 1. Omit
>    - Named columns are updated for all rows in table
> 2. Specified
>    - **Only** those rows that satisfy the `search_condition` will be updated
>
> > [!INFO]
> > Now, when you are updating a record / cell with another value; it should be of the **same** data type.
> > I think that this is basic but I have ADHD and I need to include this...

## Examples using UPDATE Command

### Update All Records For A Field

Here is the template for updating **all** _rows_ $\downarrow$:

```SQL
UPDATE table_name
SET field_name = new_value;
-- as you can see no `WHERE` clause
```

We are going to update our 'Staff' table to give all staff a 3% pay increase.

> [!INFO]- Check Current Salary of Staffs
> But first, let's see all the staff's current salary; go ahead and run the following command.
>
> ```SQL
> SELECT staffNo, salary FROM Staff;
> ```
>
> Here is the output of our results
>
> ```csv
> staffNo	salary
> SA9	    9000
> SG14	18000
> SG37	12000
> SG5	    24000
> SL21	30000
> SL41	9000
> ```

#### Updating Salary of All Staffs

```SQL
UPDATE Staff
-- increases the salary by 3%
SET salary = salary*1.03;
```

> [!TIP]- Verification of `UPDATE` for `salary`
> Using the same command as above $\uparrow$ ( _check "Checking Current Salary..._ )
> We can clearly see that their `salary` has increased.
>
> ```csv
> staffNo	salary
> SA9	9270
> SG14	18540
> SG37	12360
> SG5	24720
> SL21	30900
> SL41	9270
> ```
>
> > [!SUCCESS]
> > As you can see it has been `UPDATE`d

### Update Specific Records For A Field

Now we going to do the same thing but...

> [Same-same, same-same, but different. But still same.](https://www.youtube.com/watch?v=7tTfL-DtpXk)

Here we are actually going to use the fucking `WHERE` clause.

> I don't know if you can notice but I wanna go to bed... It is still 20:59 BTW.

Here is the _template_ when using the `WHERE` clause.

```SQL
UPDATE table_name
SET field_name = new_value
WHERE search_condition;
```

Now we are going to update all 'Manager' to increase their `salary` a further 5%.

> Nepotism and Corruption Obviously.

> [!INFO]- Check Current Salary of Managers
> Run the following command $\downarrow$:
>
> ```SQL
> SELECT staffNo, salary FROM Staff
> WHERE position = 'Manager';
> ```
>
> We should get something like this:
>
> ```csv
> staffNo	salary
> SG5	    24720
> SL21    30900
> ```

#### Updating Salary of All Managers

```SQL
UPDATE Staff
-- increases the salary by 5% for all Managers
SET salary = salary*1.05
-- include to `WHERE` clause to specify search condition
WHERE position = 'Manager';
```

> [!TIP]- Verification of `UPDATE` for `salary` for Managers Only
> As you can see we are now going to get an output of:
>
> ```csv
> staffNo	salary
> SG5	    25956
> SL21	32445
> ```
>
> > [!SUCCESS]
> > There we have it. We can say that we know how to fucking change values for a / one specific field / record / row ( _or whatever the fuck you want to call it_ ).

### Update Multiple Columns

> I think you know where this is going!

We can refer back to the [[#General Template for UPDATE Command | general command] for `UPDATE` for the _template_.

#### Promoting Staff to Manager and Increase Salary

Therefore, here we are going to include 2 columns for us to update:

1. `position`
2. `salary`

> But again let's check the current "_stats_" of this invidiual

> [!INFO]- Checking "_Stats_" of Employee / Staff
> Run the following command below $\downarrow$:
>
> ```SQL
> SELECT staffNo, position, salary FROM Staff
> WHERE staffNo = 'SG14'
> ```
>
> We should get something like so:
>
> ```csv
> staffNo	position	salary
> SG14	Supervisor	18540
> ```

##### Running the Command

```SQL
UPDATE Staff
	-- field 1
SET position = 'Manager',
	-- field 2
	salary = 20000
-- search condition
WHERE staffNo = 'SG14';
```

> [!TIP]- Verification of Promotion!
>
> > Fuck his promotion, nepotism and corrupted piece of shit
>
> We can run the above command again $\uparrow$ ( _check "Checking Status / Stats of Employee"_ )
> We should get something like this $\downarrow$:
>
> ```csv
> staffNo	position	salary
> SG14	Manager	    20000
> ```
>
> > [!SUCCESS] Extreme Success
> > We have completed everything that have been done with `UPDATE` command in the Lecture Slides.

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!
