---
id: Python - Two Dimensional Lists
aliases: Two Dimensional Lists
tags:
  - python
  - data-structures
  - arrays
  - lists
author: S.Sunhaloo
date: 2025-04-20
status: Completed
---

## List of Contents

- [[#Creation of 2D-List]]
- [[#Displaying - Accessing 2D-Lists]]
	- [[#Displaying 2D-Lists and List Value(s)]]
	- [[#Unpacking of 2D-Lists]]
- [[#Functions and Methods of 2D-Lists]]
	- [[#Insertion of Data]]
		- [[#Append Method]]
		- [[#Insert Method]]
		- [[#Extend Method]]
		- [[#List Comprehension - Insertion of Elements]]
	- [[#Removal of Data]]
		- [[#Clear Method]]
		- [[#Pop and Remove Method]]

---

> [!NOTE]
>
> > "*Lists of Lists*"
>
> That's it!
>
> As from now, I will **not** explain everything in *detail*. What do I mean by that?
>
> I assume that you already know how the **rows** and **columns** of a 2D-Lists are and other *important* stuff that your lecturers should have told you.
>
> Furthermore, Given that I already have **explained** and **showed** you *functions* and *methods* in the '[[Python - Lists]]' notes. Also I will **not** be writing any **example** ( *sub-heading* ) code!
>
> I am just going to refer to that note for the specific functions and methods that I talking about in here!
>
> > Nevertheless, I will need to explain extensively sometimes!
>

# Creation of 2D-List

This is how we create 2D-Lists ( *with [[Python - Lists#Type Annotation / Hinting | type annotations]]* ) in Python.

> I will be calling '2D-Lists' "*list of list*" in the comments of my codes.

```python
# list of list of integer numbers
int_lists: list[list[int]] = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# list of list containing most data types
general_lists = [
    [],
    [27, 44, 5],
    [100.0, 69.69, 55.55],
    ["A", "B", "C", "x", "y", "z"],
    ["Hello", "My", "Friends"],
    [False, True, False],
    ((1, 2), [3, 4], (5, 6)),
    {"x": "nice", "y": "not nice"},
]
```

> [!TIP]
> Similarly, we can have a "*lists of lists*" of **objects**!

# Displaying - Accessing 2D-Lists

## Length of 2D-Lists

Because our lists now contain *other* lists inside of it. And these "*other*" lists can contains elements themselves.

We need to first ask ourselves what **length** of *which* list(s) we are trying to find!

### Length of Overall Lists

In this "*method*" we are going to find the length of the *main* list itself.

```python
# list of list of integer numbers
int_lists: list[list[int]] = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# output the overall length of list of integers
print(f"\nOverall Length of Integer List: {len(int_lists)}")
```

We should get '3' as the **overall** length:

```console

Overall Length of Integer List: 3
```

### Length of Each Individual Lists

To get the length of **each** lists, we could simply *iterate* through the **outer**a list ( *which holds the other lists* ).

```python
# list of list of integer numbers
int_lists: list[list[int]] = [[1, 2, 3, 4], [5, 6], [7, 8, 9]]

# iterate through the list of list of integers
for index, row in enumerate(int_lists):
    # output the length of each inner list
    print(f"Length Of Inner List At Index {index}: {len(row)}")
```

Therefore, we should get length of **each** list at each *iteration*:

```console
Length Of Inner List At Index 0: 4
Length Of Inner List At Index 1: 2
Length Of Inner List At Index 2: 3
```

> [!NOTE] The `enumerate()` Function
> - Link to Python Documentation: https://docs.python.org/3/library/functions.html#enumerate
>
> > Just think of this at an *iterator*!
>
> > [!WARNING] Problems and Alternative
> > Here, I had to use the `enumerate()` function to avoid displaying the **actual** list:
> >
> > ```console
> > Length of List At Index [1, 2, 3, 4]: 4
> > Length of List At Index [5, 6]: 2
> > Length of List At Index [7, 8, 9]: 3
> > ```
> >
> > To **avoid** using the `enumerate()` function, we could have simply used the following code:
> >
> > ```python
> > # list of list of integer numbers
> > int_lists: list[list[int]] = [[1, 2, 3, 4], [5, 6], [7, 8, 9]]
> >
> > # iterate through the list of list of integers
> > for i in range(len(int_lists)):
> >    # output the length of each list
> >    print(f"Length of List At Index {i}: {len(int_lists[i])}")
> > ```
> >
> > We should get the same thing as our original code above:
> >
> > ```console
> > Length of List At Index 0: 4
> > Length of List At Index 1: 2
> > Length of List At Index 2: 3
> > ```

## Displaying 2D-Lists and List Value(s)

The code block below will guide you to displaying the *lists* and *elements* of two dimensional lists.

```python
def main():
    # list of list of integer numbers
    int_lists: list[list[int]] = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

    print("\nPythonic Version\n")

    # using the pythonic way to display each list "element"
    # unpack the lists ( inside the main list )
    print(*int_lists)

    print("\nDisplaying Rows Only\n")

    # without using 'range()' function
    # iterate through the rows in the list
    for row_list in int_lists:
        # output each row of the list
        print(row_list)

    print()

    # using the 'range()' function
    # iterate through the rows in the list
    for i in range(len(int_lists)):
        # output each row of the list
        print(int_lists[i])

    print("\nDisplaying Individual Elements ( Row-Wise )\n")

    # without using 'range()' function
    # iterate through the rows in the list
    for rows in int_lists:
        # iterate through the columns in the list
        for cols in rows:
            # output each element of ( each inner ) list
            print(cols)

    print()

    # using the 'range()' function
    # iterate through the rows in the list
    for i in range(len(int_lists)):
        # iterate through the columns in the inner list
        for j in range(len(int_lists[i])):
            # output each element of ( each inner ) list
            print(int_lists[i][j])

    print("\nDisplaying Individual Elements ( Column-Wise )\n")

    # using the `range()` function
    for i in range(len(int_lists)):
        # iterate through the columns in the inner list
        for j in range(len(int_lists[i])):
            # output each element of ( each inner ) list
            print(int_lists[j][i])


# source the main function
if __name__ == "__main__":
    main()
```

Now, we normally don't display each **row** of the *outer* list. Instead we normally ( *what I have been doing* ) display **each element** individually.

Another thing! This means that the most *versatile method* to display a 2D-List is going to be with the last *method* in the above code block as we can do things like this:

```python
# display the elements of each rows in a tabular like format
# iterate through the rows in the list
for i in range(len(int_lists)):
	# iterate through the columns in the inner list
	for j in range(len(int_lists[i])):
		# output each element in a tabular like format
		print(int_lists[i][j], end="\t")

	# change the line as "row list" changes
	print()
``` 

This is going to output something like this:

```console
1       2       3
4       5       6
7       8       9
```

> [!WARNING]
> Yes, if we take a look back our *normal* lists notes, we are going to see that I made a title called '[[Python - Lists#Accessing List Value(s) | Accessing List Value(s)]]'.
>
> Now, we can see that I have added something like "*without range() function*"!
>
> Its the same thing here, whereby these are **not** for *modifying* the elements but instead its *just* used for **displaying** "*things*" on the screen!

> [!WARNING] The 17th of June of 2025 @17:03:07
> While doing [[Programming - Labsheet 6 ( L1S2 )#Question 9 | Question 9]], I realised something...
>
> <p align="center"> <em> Square Matrices</em> are <strong> NOT</strong> <em> Rectangular Matrices</em> </p>
>
> > Who would have fucking thought!!!
>
> Yes, they are **don't** use the *same* "*function*" to display the elements found inside the list.
>
> You know how we have our simple algorithm that displays a lists in *row-wise* position $\downarrow$:
>
> ```python
> # using the 'range()' function
> # iterate through the rows in the list
> for i in range(len(int_lists)):
> 	# iterate through the columns in the inner list
> 	for j in range(len(int_lists[i])):
> 		# output each element of ( each inner ) list
> 		print(int_lists[i][j])
> ```
>
> Therefore if you wanted to display the **Square Matrix** in term of '<em> <span style="color: orange;"> Column-Wise</span> </em> '. Then we just need to change `i` and `j`'s position inside our print statement just like so:
>
> ```python
> # simply change the position
> print(int_lists[j][i])
> ```
>
> > [!BUG] This Does **NOT** Fucking Work with *Rectangular Matrices*!
> > > Its because of the **outer** `for` loop!
> >
> > Yes, let's say that we have this two-dimensional list:
> >
> > ```python
> > # list of list of integer numbers
> > int_lists: list[list[int]] = [[1, 2, 3, 0], [4, 5, 6, 0], [7, 8, 9, 0]]
> > ```
> >
> > Given that here `i` will only go from '0' to '2' because of `len(int_lists)` but what about `j`?
> >
> > `j` will go from '0' to '3' as `len(int_lists[i])`; but we simply <span style="color: orange;"> cannot</span> do this as `i` just does *three* iteration.
> >
> > > Hence, the '*IndexError*'!
> >
>

---

# Unpacking of 2D-Lists

## Unpack Elements From Outer List

From what I have been saying its that 2D-Lists are basically storing *other* **lists**!

Therefore, we are going to *unpack*a the "*inner*" lists!

```python
# list of list of integer numbers
int_lists: list[list[int]] = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# unpack the list elements found in the outer list
x, _, z = int_lists

# output the "list value" of 'x', 'y', 'z'
print(f"\nList Stored in 'x': {x}")
print(f"List Stored in 'z': {z}")

```

We should have each individual **inner** list be assigned to the proper variables ( *i.e `x`,  `y`, `z`* ) like so:

```console

List Stored in 'x': [1, 2, 3]
List Stored in 'z': [7, 8, 9]
```

## Unpacking Elements From Inner Lists

But what if instead of taking the **list** *elements* found in the "*outer*" list; we instead need to run some computation with the elements found in the **inner** list?

Therefore, we could do something like this:

```python
# function to check if inner lists are of same size
def calc_length_inner_list(outer_list: list[list[int]]):
    # iterate through the rows in the list
    for i in range(len(outer_list)):
        # check if the length of inner list is same
        if len(outer_list[i]) == 3:
            # do nothing
            pass

        # if the length of 1 or more inner list are not the same
        else:
            # output appropriate message
            print("\n\t<< Inner List NOT Formatted Correctedly... Exiting!!! > > ")

            # exit the program
            exit(1)


# our main function
def main():
    # list of list of integer numbers
    int_lists: list[list[int]] = [[2, 3], [4, 5, 6], [7, 8, 9]]

    # call the function to validate length of inner lists
    calc_length_inner_list(int_lists)

    # if we are here ==> everything is okay
    print("\n\t<< List Properly Formatted > > \n")

    # iterate through the rows of the list
    for i in range(len(int_lists)):
        # unpack the elements found in the list
        x, y, z = int_lists[i]

        # display each invididual element
        print(
            f"List #{i}: First Element = {x} | Second Element = {y} | Third Element = {z}"
        )


# source the main function
if __name__ == "__main__":
    main()
```

Here we could get the output(s) like these:

```console
        << Inner List NOT Formatted Correctedly... Exiting!!! > >
```

```console
        << List Properly Formatted > >

List #0: First Element = 1 | Second Element = 2 | Third Element = 3
List #1: First Element = 4 | Second Element = 5 | Third Element = 6
List #2: First Element = 7 | Second Element = 8 | Third Element = 9
```

> [!NOTE]
> In this code, I expect someone has manually "*hard-coded*" the *list of list* of integers.
>
> Therefore, I want to check if the **length** of the *inner* lists are the **same**. If **not**, we tell the user that the list is **not** properly *formatted* and the program closes itself!
>
>

---

## Before We Start

Below you are going to find some function that I will be calling in the *example* code blocks. Therefore, do take a look or refer to here if you find a **function** that you don't know what it does!

### Display Rows in 2D-Lists

```python
# function to display each rows in 2D-lists ( without range function )
def display_2d_lists_rows(some_list: list[list]):
    # iterate through the rows of the list
    for rows in some_list:
        # display the individual inner list
        print(rows)
```

### Display Elements in 2D-Lists As Table

```python
# function to display each element in 2D-lists in a table ( without range function )
def display_2d_lists_table(some_list: list[list]):
    # iterate through the rows of the list
    for rows in some_list:
        # iterate through the columns of the list
        for element in rows:
            print(f"{element}\t", end="")

	    # change the line
	    print()
```

---

# Functions and Methods of 2D-Lists

## Insertion of Data

> [!INFO]
> I will **not** be writing about things like '[[Python - Lists#Concatenation Operator | Concatenation Operator]]' and '[[Python - Lists#Slice Operator | Slice Operator]]' as they were just for **fun**!
>
> > "*And also nobody uses them to really really insert elements into a list*!"

### Append Method

> [!NOTE]
> Please refer to the [[Python - Lists#Append Method | Append Method]] found in the note '[[Python - Lists]]' for more details about the function itself!

Okay, there are several ways and *things* that we can insert into the **outer** list.

#### Append List to Outer List Itself

```python
# empty list
general_list = []

# output the general list ( before insertion )
print(f"General List ( Before Insertion ): {general_list}")

# append other lists inside to the 'general_list'
general_list.append(["hello", "world", "from", "list"])
# sorting the numbers ( inner list ) before appending
general_list.append(sorted([44, 5, 33, 55, 27]))
general_list.append([69.69, 55.55, 121.0101, 00.00])
general_list.append([True, False, True, False])

# output the general list ( after insertion )
print("\n<< General List ( After Insertion ) > > \n")

# call the function to display the list
display_2d_lists_rows(general_list)
```

Therefore, the output should result in this:

```console
General List ( Before Insertion ): []

<< General List ( After Insertion ) > >

['hello', 'world', 'from', 'list']
[5, 27, 33, 44, 55]
[69.69, 55.55, 121.0101, 0.0]
[True, False, True, False]
```

> See how the **elements** of the *inner* list of *integers* are **sorted**!

> [!NOTE]
> We could also insert *normal* elements **instead** of *lists*!
>
> Therefore, we need to be careful about these.

#### Append Elements to Inner Lists

Compared to the things that we did above. Here, instead of *adding* the **whole** list(s) itself.

We are going to be inserting **elements** in ( *specific* ) **inner** lists!

```python
# general list of lists containing some elements
general_list = [
    ["hello", "world", "from", "list"],
    [44, 5, 33, 55, 27],
    [69.69, 55.55, 121.0101, 00.00],
    [True, False, True, False],
]

# output the general list ( before insertion )
print("\n<< General List ( Before Insertion ) > > \n")

# call the function to display the list
display_2d_lists_rows(general_list)

# append elements inside the innner list of the 'general_list'
general_list[0].append("another one")
general_list[1].append(9)

# sort the list found at index '1' after integer value inserted
general_list[1].sort()

general_list[2].append(-1.5)
general_list[3].append(True)

# output the general list ( after insertion )
print("\n<< General List ( After Insertion ) > > \n")

# call the function to display the list
display_2d_lists_rows(general_list)
```

In this case, we are *filling* the **inner** list of the `general_list`:

```console

<< General List ( Before Insertion ) > >

['hello', 'world', 'from', 'list']
[44, 5, 33, 55, 27]
[69.69, 55.55, 121.0101, 0.0]
[True, False, True, False]

<< General List ( After Insertion ) > >

['hello', 'world', 'from', 'list', 'another one']
[5, 9, 27, 33, 44, 55]
[69.69, 55.55, 121.0101, 0.0, -1.5]
[True, False, True, False, True]
```

### Insert Method

> [!NOTE]
> Please refer to the [[Python - Lists#Insert Method | Insert Method]] found in the note '[[Python - Lists]]' for more details about the function itself!

#### Insert List to Outer List Itself

```python
# general list of list containing some elements
general_list = [[1, 2, 3]]

# output the general list ( before insertion )
print("\n<< General List ( Before Insertion ) > > \n")

# call the function to display the list
display_2d_lists_rows(general_list)

# insert other lists inside to the 'general_list'
general_list.insert(-1, ["hello", "world", "from", "list"])
general_list.insert(-2, sorted([44, 5, 33, 55, 27]))
general_list.insert(4, [69.69, 55.55, 121.0101, 00.00])
general_list.insert(5, [True, False, True])

# output the general list ( after insertion )
print("\n<< General List ( After Insertion ) > > \n")

# call the function to display the list
display_2d_lists_rows(general_list)
```

We should see that we are inserting actual **inner** lists:

```console

<< General List ( Before Insertion ) > >

[1, 2, 3]

<< General List ( After Insertion ) > >

[5, 27, 33, 44, 55]
['hello', 'world', 'from', 'list']
[1, 2, 3]
[69.69, 55.55, 121.0101, 0.0]
[True, False, True]
```

#### Insert Elements to Inner Lists

Well, I think you have already guess what I am going to do!

```python
# general list of lists containing some elements
general_list = [
    ["hello", "world", "from", "list"],
    [44, 5, 55, 27],
    [69.69, 55.55, 121.0101, 00.00],
    [True, False, True, False],
]

# output the general list ( before insertion )
print("\n<< General List ( Before Insertion ) > > \n")

# call the function to display the list
display_2d_lists_rows(general_list)

# insert elements inside the innner list of the 'general_list'
general_list[0].insert(1, "what")
general_list[0].insert(5, "now")

general_list[1].insert(0, 1)
general_list[1].insert(4, 2)
general_list[1].insert(7, 3)

# INFO: look how it inserts just before the last element
general_list[2].insert(-1, 11.11)
general_list[3].insert(len(general_list[3]), True)

# output the general list ( after insertion )
print("\n<< General List ( After Insertion ) > > \n")

# call the function to display the list
display_2d_lists_rows(general_list)
```

We should see that we have any output like this:

```console

<< General List ( Before Insertion ) > >

['hello', 'world', 'from', 'list']
[44, 5, 55, 27]
[69.69, 55.55, 121.0101, 0.0]
[True, False, True, False]

<< General List ( After Insertion ) > >

['hello', 'what', 'world', 'from', 'list', 'now']
[1, 44, 5, 55, 2, 27, 3]
[69.69, 55.55, 121.0101, 11.11, 0.0]
[True, False, True, False, True]
```

### Extend Method

With this method, we **cannot** perform the '*Extend Other List to Outer List*'!

This is because of the simple fact that its going to **combine** that list that we are trying add... Just take a look below!

```python
# integer list of list containing some elements
int_list: list[list[int]] = [[1, 2, 3], [4, 5, 6]]

# WARNING: this will just combine individual elements to the outer list
int_list.extend([7, 8, 9])

# output the supposed to be 2D-List
print(f"Integer List ( After Insertion ): {int_list}")
```

I mean why would someone want to do this!

> Famous last words!

```console
Integer List ( After Insertion ): [[1, 2, 3], [4, 5, 6], 7, 8, 9]
```

> [!WARNING] So Don't Use It ( *in this case* )!

#### Extend Lists to Inner Lists

Nevertheless, we can still user the `.extend()` method with the individual 1D-lists that are found inside.

```python
# general list of lists containing some elements
general_list = [
    ["hello", "world", "from", "list"],
    [44, 5, 55, 27],
    [69.69, 55.55, 121.0101, 00.00],
    [True, False, True, False],
]

# output the general list ( before insertion )
print("\n<< General List ( Before Insertion ) > > \n")

# call the function to display the list
display_2d_lists_rows(general_list)

# insert elements inside the innner list of the 'general_list'
general_list[0].extend(["again", "hello", "world"])

general_list[1].extend([num for num in range(11)][::-2])
# sort the list found at index '1' after integer value inserted
general_list[1].sort()

general_list[2].extend([1.2, 2.3, 3.4, 4.5])
general_list[3].insert(len(general_list[3]), True)

# output the general list ( after insertion )
print("\n<< General List ( After Insertion ) > > \n")

# call the function to display the list
display_2d_lists_rows(general_list)
```

Now, its going to be just fine!

```console

<< General List ( Before Insertion ) > >

['hello', 'world', 'from', 'list']
[44, 5, 55, 27]
[69.69, 55.55, 121.0101, 0.0]
[True, False, True, False]

<< General List ( After Insertion ) > >

['hello', 'world', 'from', 'list', 'again', 'hello', 'world']
[0, 2, 4, 5, 6, 8, 10, 27, 44, 55]
[69.69, 55.55, 121.0101, 0.0, 1.2, 2.3, 3.4, 4.5]
[True, False, True, False, True]
```

### List Comprehension - Insertion of Elements

I am just going to write **one** simple code that I know *everyone* will just get!

```python
# import the 'randint' function from random module
from random import randint

# integer list of list containing 100 random integer values ( 0 to 9 )
int_list: list[list[int]] = [[randint(0, 9) for i in range(10)] for i in range(10)]

# call the function to display the list ( like a table )
display_2d_lists_table(int_list)
```

> So beautiful!

```console
3       2       0       0       8       4       1       7       8       7
3       4       3       2       0       6       7       5       9       3
4       3       2       4       0       4       9       1       7       0
3       0       0       1       3       2       8       7       3       3
2       1       1       4       4       4       2       2       3       7
2       5       2       8       1       2       6       7       9       5
3       3       5       1       1       7       0       8       4       5
9       2       9       4       7       0       7       2       2       0
6       2       3       7       2       3       1       4       4       4
6       3       8       3       8       4       3       8       9       2
```

> [!INFO] One More Thing!
> > "*STFU! There is always one more fucking thing*!" You Right Now!
>
> In this case, you can see that I have used the function `display_2d_list_table` to display the list. If you just take a look again at the *code* found **in** that function. You will see that I have **not** use the `range()` function at all!
>
> This very simple function will go about displaying all the *elements* in a **row** and move on to the next **row**. This means that the *element* is the one who is considered to be at the columns position.
>
> But what if you want to display all the *element* in a **column** first? Meaning instead of moving from "*horizontally*", we are going to move "*vertically*"!
>
> > Check the code below!
>
> ```python
> # integer list of list containing some elements
> # INFO: it would be harder to see with random value
> int_list: list[list[int]] = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
>
> print("\n<< Display Row Wise WITHOUT Range Function > > \n")
>
> # display the list normally without range function
> for rows in int_list:
>    for num in rows:
>        print(f"{num}\t", end="")
>    print()
>
> print("\n<< Display Row Wise WITH Range Function > > \n")
>
> # display the list normally with range function
> for i in range(len(int_list)):
>    for j in range(len(int_list[i])):
>        print(f"{int_list[i][j]}\t", end="")
>    print()
>
> print("\n<< Display Column Wise WITH Range Function > > \n")
>
> # display the list column-wise with range function
> for i in range(len(int_list)):
>    for j in range(len(int_list[i])):
>        print(f"{int_list[j][i]}\t", end="")
>    print()
>
> print("\n<< Display Column Wise WITHOUT Range Function > > \n")
>
> # WARNING: this cannot be done without the range function
> # okay, lets try this
>
> for rows in int_list:
>    for nums in reversed(rows):
>        print(f"{nums}\t", end="")
>    print()
>
> print("\n\t<< NOT THE SAME!!! > > ")
>
> print("\n<< Display Column Wise WITHOUT Range Function AGAIN > > \n")
>
> for rows in reversed(int_list):
>    for nums in reversed(rows):
>        print(f"{nums}\t", end="")
>    print()
>
> print("\n\t<< NOT THE SAME AGAIN!!! > > ")
> ```
>
> The output for the above code block is going to be:
>
> ```console
>
> << Display Row Wise WITHOUT Range Function > >
>
> 1       2       3
> 4       5       6
> 7       8       9
>
> << Display Row Wise WITH Range Function > >
>
> 1       2       3
> 4       5       6
> 7       8       9
>
> << Display Column Wise WITH Range Function > >
>
> 1       4       7
> 2       5       8
> 3       6       9
>
> << Display Column Wise WITHOUT Range Function > >
>
> 3       2       1
> 6       5       4
> 9       8       7
>
>        << NOT THE SAME!!! > >
>
> << Display Column Wise WITHOUT Range Function AGAIN > >
>
> 9       8       7
> 6       5       4
> 3       2       1
>
>        << NOT THE SAME AGAIN!!! > >
> ```
>
> > This is why I say that with the `range()` function; *its just superior*! Additionally, we also **cannot** do *modification* or data manipulation **without** the `range()` function.
> > So I think that its better to use the *version* with the `range()` function as most ( *if not all* ) programming languages has its own *version* of the `range()` function!

## Removal of Data

### Clear Method

Again, as we have lists **inside** of list which contains element... Therefore, there are going to be 2 main ways of *clearing* the list.

#### Clearing the Entire List

```python
# general list of lists containing some elements
general_list = [
    ["hello", "world", "from", "list"],
    [44, 5, 55, 27],
    [69.69, 55.55, 121.0101, 00.00],
    [True, False, True, False],
]

# output the general list ( before clearing )
print("\n<< General List ( Before Clearing ) > > \n")

# call the function to display the list
display_2d_lists_rows(general_list)

# clear the entire list of list
general_list.clear()

# output the general list ( after clearing )
print(f"\n<< General List ( After Clearing ): {general_list}")
```

This should remove **everything** from our *main* 2D-list!a

```console

<< General List ( Before Clearing ) > >

['hello', 'world', 'from', 'list']
[44, 5, 55, 27]
[69.69, 55.55, 121.0101, 0.0]
[True, False, True, False]

<< General List ( After Clearing ): []
```

> [!WARNING]
> > I just need to write this here! :)
>
> This is going to **delete** <span style="color: red;"> everything</span> from the list!!!

#### Clearing Inner Lists

In this case, we are going to clear a **specific** *inner* list found in our 2D-list.

```python
# our main function
def main():
    # general list of lists containing some elements
    general_list = [
        ["hello", "world", "from", "list"],
        [44, 5, 55, 27],
        [69.69, 55.55, 121.0101, 00.00],
        [True, False, True, False],
    ]

    # output the general list ( before clearing )
    print("\n<< General List ( Before Clearing ) > > \n")

    # call the function to display the list
    display_2d_lists_rows(general_list)

    # exception handling
    try:
        # ask the user what index of list to clear
        user_index = int(input("\nPlease Enter Index of ( Inner ) List to Clear: "))

        # validate the user index with compound inequality
        # NOTE: this is an example of early fail
        # instead of using a whole `if... then... else...`
        if not 0 <= user_index < len(general_list):
            # output appropriate message
            print("\n<< Please  Enter Valid Index!!! > > \n")

            # handle the error gracefully
            return -1

        # clear the required index
        general_list[user_index].clear()

    # if the user does not enter integer values
    except ValueError as e:
        # output the error in question
        print(f"\nError: {e}")
        # output the error in question
        print("<< Please Enter Integer Values!!! > > \n")

    # always display the values of integer list
    finally:
        # output the general list ( after clearing )
        print("\n<< General List ( After Clearing ) > > \n")

        # call the function to display the list
        display_2d_lists_rows(general_list)


# source the main function
if __name__ == "__main__":
    main()
```

---

### Pop and Remove Method

> [!INFO] What about `.pop()`, `.remove()` and other *functions* / *method*?
> Well, if you go back above and a quick look at the structure of this note... You are going see 2 things:
>
> 1. For all of the *methods* we talked about they pretty much have the same **structure**
> 2. We are breaking it down into '*Outer List*' and *Inner List(s)*
>
> Therefore, as I think that programming is more of a *trial and error* thing. I guess you should try to do the other codes by yourself!
>
> > Because I feel like I am going to waste my time writing about these which are just going to be repeats of the above codes
>

---

> [!WARNING] "*What about the others*?"
> Well, in '[[Python - Lists]]' I did show you how to use most of the *functions* and *methods* associated with **lists**.
>
> Therefore, I should expect you to try and **solve your problem** with some "*fucking around and finding out*"!
>
> Hence, I think that my job here is complete!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!