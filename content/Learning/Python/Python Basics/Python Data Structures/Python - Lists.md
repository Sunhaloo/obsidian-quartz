---
id: Python - Lists
aliases: Lists in Python
tags:
  - python
  - data-structures
  - arrays
  - lists
author: S.Sunhaloo
date: 2025-04-06
status: Completed
---

## List of Contents

- [[#Lists in Python]]
	- [[#Arrays V/S Lists]]
- [[#Creation of Lists]]
- [[#Displaying - Accessing Lists]]
	- [[#Displaying List and List Value(s)]]
	- [[#Accessing List Value(s)]]
- [[#Unpacking of Lists]]
- [[#Functions and Methods of Lists]]
	- [[#Insertion of Data]]
		- [[#Append Method]]
		- [[#Insert Method]]
		- [[#Extend Method]]
		- [[#List Comprehension - Insertion of Elements]]
		- [[#Insertion of Data in Other Ways]]
	- [[#Removal of Data]]
		- [[#Clear Method]]
		- [[#Pop Method]]
		- [[#Remove Method]]
		- [[#Delete Statement]]
		- [[#List Comprehension - Removal of Elements]]
		- [[#Removal of Data in Other Ways]]
	- [[#Miscellaneous Methods / Functions]]
		- [[#List Equality - Inequality]]
		- [[#Split Method]]
		- [[#Copy Method]]
		- [[#Count Method]]
		- [[#Index Method]]
		- [[#Reverse Method]]
		- [[#Sort Method]]
		- [[#Sorted Function]]
		- [[#Join Method]]

---

# Lists in Python

> [!TIP] What is a '*List*'?
> It is a *data structure* that can store **values** of a *variety* of **data types**.
>

Think of *list* like a simple, ruled **notepad** or **[field note](https://fieldnotesbrand.com/)** where you can write *objects* on each line. Additionally, we can write whatever we want: numbers, decimal numbers, fractions, words, sentences!

> I see them just like **ruled notepads**!

## Arrays V/S Lists

As compared to **arrays**; lists are **mutable**. This means that items can be added, removed and these items can be of different *data types*. Additionally, they are **dynamic** as they can *grow* or *shrink* ( *in size* ) during the execution of the program.

Arrays are **not** *mutable* nor *dynamic*. This is due to the fact they can only store <span style="color: orange;"> one</span> **type** of data and they have a **fixed** size!

> I think of *arrays* like **ruled notebooks**!

### Example: C Arrays

Here is a little example of how we create **arrays** in [[C Data View V2 | C]]!

```C
#include <stdio.h>

int main(int argc, char *argv[])
{
    // array of integers
    int array_ints[5] = {1, 2, 3, 4, 5};

    printf("\n\tDisplaying Array of Integers\n\n");

    // display array of integers
    for (int i = 0; i < sizeof(array_ints) / sizeof(array_ints[0]); i++) {
        // output the index and value on screen
        printf("\t    Index: %d | Value: %d\n", i, array_ints[i]);
    }

    printf("\n\t----------------------------\n");

    // array of characters
    char array_chars[6] = {'A', 'B', 'C', 'X', 'Y', 'Z'};

    printf("\n\tDisplaying Array of Characters\n\n");

    // display array of characters
    for (int i = 0; i < sizeof(array_chars) / sizeof(array_chars[0]); i++) {
        // output the index and value on screen
        printf("\t    Index: %d | Value: %c\n", i, array_chars[i]);
    }

    printf("\n\t----------------------------\n");

    // string data type ==> made up of array of characters
    char string_data[29] = "Never Going to Give You Up!!!";

    printf("\n\tDisplaying Array of Strings\n\n");

    printf("   Sentence: ");

    // display array of characters
    for (int i = 0; i < sizeof(string_data) / sizeof(string_data[0]); i++) {
        // output the index and value on screen
        printf("%c", string_data[i]);
    }

    printf("\n\n\t----------------------------\n");

    return 0;
}
```

As you can '*C*' ( *hehehe* )... When you create arrays; they has a fixed size and elements are not removed or added from the array.

> Don't believe me? Look at our *String Array* above

---

# Creation of Lists

To create list in Python, we use the `[]` characters.

```python
# list of integers numbers only
int_list = [1, 2, 3, 4, 5]

# list containing most data types
general_list = [
	44,
	5.5,
	"A",
	"Something",
	True,
	2 + 5j,
	None,
	[1, 2, 3],
	(4, 5, 6),
	{7, 8, 9},
	{"x": "nice", "y": "not nice"},
]
```

> [!INFO] `type()` of List
> If we run `print(type(int_list))` or `print(type(general_list))` we should see that we get:
>
> ```console
> <class 'list'>
> ```
>
> Nevertheless, the word '*list*' is **not** a reserved word in Python and you can create a list called `list` like so:
>
> ```python
> list = [1, "shitter", 'A']
> ```
>
> > Nevertheless, this is **not** recommended!
>

> [!TIP]
> We can also have a list of **objects**!

## Type Annotation / Hinting

As you know; in Python, we do **not** declare any variables. But there is something called *type hinting* whereby a programmer can suggest what **data type** will go into a specific variable.

Here is a little example:

```python
# declaration of variables with 'type hinting' or 'type annotation'
num: int = 69
floating_num: float = 6.9
character_thingy: str = "A"
some_text: str = "Some Text Here"
true_false: bool = False
complex_num: complex = 1 + 2j
```

> [!INFO]
> We have already covered that in '[[Python Language Basics#Basic Data Types | Python Language Basics]]'.

But for Lists its a bit like C ( *not really* ):

```python
# list of strings
str_list: list[str] = ["string", "data", "type"]

# list of integers
int_list: list[int] = [1, 2, 3]

# list of lists ==> multi-dimensional list
list_list: list[list] = [
	["string", "data", "type"],
	[1, 2, 3]
]
```

> [!TIP]
> From the code above; you can see that we have the *list of list*.
>
> ```python
> # list of lists ==> multi-dimensional list
> list_list: list[list] = [["string", "data", "type"], [1, 2, 3]]
> ```
>
> But what I you want to *show* that the **list** being inserted should contain *string* data type...
>
> Therefore, we can "*type the type hinting*!" like so:
>
> ```python
> # list inside the list should contain integer numbers
> list_list: list[list[int]] = [
> 	[1, 2, 3],
> 	[1, 2, 3]
> ]
> ```

> [!WARNING]
> You are **still** able to insert *other* data types!
>
> Again, this is because *its for other programmers*; its main purpose is to **improve** readability and allow [static type checkers](https://en.wikipedia.org/wiki/Type_system) to list of potential errors.
>
> Nevertheless, you can still **do** something like this:
>
> ```python
> # it just feels wrong
> list_list: list[list[int]] = [
> 	["feels", "very", "wrong"],
> 	[1, 2, 3]
> ]
> ```
>
> > But your **type checker** ( *I use [pyright](https://github.com/microsoft/pyright) and VIM BTW* ) will definitely *scream* at you!
>

---

# Displaying - Accessing Lists

## Length of List

Now, the function length which as you know can be used with strings to calculate the **length** of a string... Can also be used to calculate the *length* / **size** of a list?

Yes! Instead of passing a *string* a parameter inside the `len()` function... We are just going to pass the actual list ( *variable name* ).

```python
# our main function
def main():
    # create a list of integers ==> has 5 items
    int_list = [1, 2, 3, 4, 5]
    # create a list of boolean values ==> has 3 items
    bool_list = [True, False, True]
    # create a list of strings ==> has 4 items
    str_list = ["Aryton Senna", "", "Lewis Hamilton", "Sebastien Vettel"]

    # output the size of each list
    print("\n<< Size of Lists > > \n")

    print(f"Size of Integer List = {len(int_list)}")
    print(f"Size of Boolean List = {len(bool_list)}")
    print(f"Size of String List = {len(str_list)}")


# source the main function
if __name__ == "__main__":
    main()
```

> [!TIP]
> If you have a program / code that uses the length of list **often**.
>
> You **should** place the length of that specific list into a variable as the code will then only have to *run* the `len(list)` only **once**!
>
> > For optimisation purposes!
>
> > [!INFO]
> > Nevertheless, this don't not apply to Python! :-(
>

## Displaying List and List Value(s)

There are many ways to display a list in Python. I am going to show you some version including the *Pythonic* way.

> I am going to be writing everything in a single code block!

```python
# our main function
def main():
    # list of integer numbers
    int_list = [1, 2, 3, 4, 5]

    print("\nPythonic Version\n")

    # the pythonic way of displaying list
    # "unpack" the values
    print(*int_list)

    print("\n'Normal' Version\n")

    # "normal" way to display values of list
    # interate through the list
    for num in int_list:
        # output the value at each index
        print(num)

    print("\n'C' Version\n")

    # doing it like in 'C'
    # interate through the length of list
    for i in range(len(int_list)):
        # output the index and its corresponding value
        print(f"Index = {i} | Value: {int_list[i]}")

    print("\n'C' - Python Version\n")

    # doing the same thing above but using 'enumerate' function
    for index, num in enumerate(int_list):
        # output the index and its corresponding value
        print(f"Index = {index} | Value: {num}")


# source the main function
if __name__ == "__main__":
    main()
```

> [!TIP] Enumerate Function
> For the `enumerate()` function, if you run the code above for with the `enumerate()` function. You should see this output.
>
> ```console
> Index = 0 | Value: 1
> Index = 1 | Value: 2
> Index = 2 | Value: 3
> Index = 3 | Value: 4
> Index = 4 | Value: 5
> ```
>
> As you can see, the *index* **starts** with '0'!
>
> For my codes whereby I wanted to used this but did **not** want it to start at '0'. I simply added '1' to the `index` *variable*.
>
> ```python
> print(f"Index = {index + 1} | Value: {num}")
> ```
>
> But looking at the official Python documentation over at 'https://docs.python.org/3/library/functions.html#enumerate'. I saw that you can do something like this:
>
> ```python
> for index, num in enumerate(int_list, start=1):
> 	# output the index and its corresponding value
> 	print(f"Index = {index} | Value: {num}")
> ```
>
> > Nevertheless, they both does the **same** fucking thing!
>

## Accessing List Value(s)

Now, given that you can **output** ( *or display* ) values from a list like so:

```python
# "normal" way to display values of list
# interate through the list
for num in int_list:
	# output the value at each index
	print(num)
```

> Snippet from code above.

Nevertheless, we <span style="color: red;"> cannot</span> do / use this for things like **algorithms** and such.

This is because the code above just displays the **actual** *item* / *value* and does **not** really care about that item's *position*.

While with something like:

```python
# interate through the length of list
for i in range(len(int_list)):
	# output the index and its corresponding value
	print(f"Index = {i} | Value: {int_list[i]}")
```

Here, we can **easily** access **both** the *data item* and its corresponding **index** ( *or position* ).

> [!WARNING]
> Algorithms need to be very fast and *clear* for the other programmer to understand.
>
> > *As they can sometime be complex*!
>
> Therefore, the `enumerate()` function is **not** an option here!

> [!NOTE]
> I use *value* / *data item* or *element* interchangeably!

---

# Unpacking of Lists

We all know what [[Python Language Basics#Basic Data Types | multiple assignment]] looks like:

```python
x = y = z = "What!"
lewis_hamilton, sebastien_vettel, max_verstappen = 44, 5, 33
```

Well, we are going to be doing something similar but with lists!

> [Same same but different](https://www.youtube.com/watch?v=7tTfL-DtpXk&t=13s)

Study the code below:

```python
# general list containing some elements
general_list = [55, "shit", 69.69, True]

# unpack the elements found in the general list
a, b, c, d = general_list

# output the values of variables 'a', 'b', 'c' and 'd'
print(f"\nValue of 'a': {a}")
print(f"Value of 'b': {b}")
print(f"Value of 'c': {c}")
print(f"Value of 'd': {d}")
```

The output for this unpacking is going to look like this:

```console

Value of 'a': 55
Value of 'b': shit
Value of 'c': 69.69
Value of 'd': True
```

> [!WARNING]
> The **exception** '*ValueError*' will be raised if you try to unpack something like this:
>
> ```python
> # integer list containinig 2 elements
> int_list: list[int] = [1, 2]
>
> # take the first 3 elements ( NOT possible )
> x, y, z = int_list
> ```
>
> The '*ValueError*' should be raised:
>
> ```console
> ValueError: not enough values to unpack (expected 3, got 2)
> ```

> [!TIP]
> This can also work with "*normal*" **string** like so:
>
> ```python
> # string variable assigned 'Hello World'
> greetings = "Hello World"
>
> # take the first and third character and leave the rest
> first_char, _, third_char, *_ = greetings
>
> # display the first and last character
> print(f"First Character = {first_char}, Third Character = {third_char}")
> ```
>
> We should get:
>
> ```console
> First Character = H, Third Character = l
> ```
>

#### Special Operator

There are 2 operators ( *more like 1 operator* ) that we are going to be using here, they are the:

1. `_`
2. `*`

I like to think at the `_` character as the "*leave it here*" and the `*` character as the "*take all in*" operator.

Given that we now have another list:

```python
# integer list containing 10 elements
int_list: list[int] = [num + 1 for num in range(10)]

# skip the first and last value --> take the rest
_, *inside_values, _ = int_list

# take the first and last value --> skip the rest
first_value, *_, last_value = int_list

# output the variables
print(f"\nInside Values: {inside_values}")
print(f"First Value: {first_value}")
print(f"Last Value: {last_value}")
```

Well, the output for this is going to be like this:

```console
Inside Values: [2, 3, 4, 5, 6, 7, 8, 9]
First Value: 1
Last Value: 10
```

> Please refer to '[[#List Comprehension - Insertion of Elements | List Comprehension]]'!

As you can see from the above example; the `_` character acts like a *placeholder* **leaving out** everything that we **don't** need while the `*` operator acts like a `SELECT * FROM table_name;` ( *if you understand databases* ).

Additionally, we can **combine** them to make this: `*_`; which I like to call "*leave everything out*!"

> [!TIP] The `_` Character
> The keen eyes of yours might have notice somethings... I keep calling the `_` a "*character*" and **not** an "*operator*"!
>
> Yes, this is because its just a simple '\_' character and has <span style="color:red;"> no</span> special meaning in Python.
>
> Heck we can even print it out!
>
> ```python
> # integer list containing 10 elements
> int_list: list[int] = [num + 1 for num in range(10)]
>
> # skip the first and last value --> take the rest
> _, *inside_values, _ = int_list
>
> # output content of '_' character
> print(f"Value: {_}")
>
> # take the first and last value --> skip the rest
> first_value, *_, last_value = int_list
>
> # output content of '_' character
> print(f"Value: {_}")
> ```
>
> Therefore, we can see what values has been assigned to it
>
> ```console
> Value: 10
> Value: [2, 3, 4, 5, 6, 7, 8, 9]
> ```
>
> > [!INFO]
> > Nevertheless, the `*` character is an actual **operator** in Python!

#### Example: Unpacking with Function

```python
# import the 'randint' function from the 'random' module
from random import randint


# function that will perform arithmetic operation on a list of numbers
def calculation(num_list: list[int]):
    # find the maximum, minimum, sum and average of numers in list
    max_int = max(num_list)
    min_int = min(num_list)
    sum_list = sum(num_list)
    avg_list = sum(num_list) / len(num_list)

    # return numbers in a list
    return [max_int, min_int, sum_list, avg_list]


# our main function
def main():
    # integer list containing some elements
    # NOTE: as you can see in Python we use the '_' as a placeholder
    int_list: list[int] = [randint(0, 100) for _ in range(30)]

    # call the function and use unpacking to unpack all values
    max_num, min_num, list_sum, list_avg = calculation(int_list)

    # display the values
    print("\n << Case 1: Display All Values > > \n")
    print(f"Maximum Value: {max_num}")
    print(f"Minimum Value: {min_num}")
    print(f"Sum Value: {list_sum}")
    print(f"Average Value: {list_avg}")

    # call the function and use unpacking to unpack maximum and average value
    max_num, *_, list_avg = calculation(int_list)

    # display the values
    print("\n << Case 2: Display Maximum and Average Value > > \n")
    print(f"Maximum Value: {max_num}")
    print(f"Average Value: {list_avg}")

    # call the function and use unpacking to unpack mininum and sum in a list
    _, *min_sum_list, _ = calculation(int_list)

    # display the values
    print("\n << Case 3: Display Minimum and Sum Value ( List ) > > \n")
    print(f"[Minimum Value, Sum Value]: {min_sum_list}")


# source the main function
if __name__ == "__main__":
    main()
```

---

## Before We Start - Help!

To see a **list** ( *yes an actual list* ) of all the *functions* or *methods* associated with a *list*... We can do use the `dir()` function like so:

```python
# output all the function / methods of a list
print(dir(list))
```

This will output a *list* with **all** the functions and methods associated with *any* list in Python.

Now, if you want to see the *details* of a **specific** function or method of *any* list... We can use the `help()` function like so:

```python
# help page for `len()` function
help(len)

# help page for `.append()` method
help(list.append)
```

> [!NOTE]
> See how for the **functions**... We **don't** need to use the `()` characters and **no** need to pass in any *list objects*.
>
> The same thing applies to **methods** whereby we **do** need to add a *list placeholder* but **no** need to *include* `()` and any parameters.

# Functions and Methods of Lists

Below you are going to find a bunch of *functions* and *methods* that can be used with **lists**. Well, let's get started!

## Insertion of Data

There are 2 **main** *methods* to **insert** elements into list, they are:

1. `list_name.append(element)`
2. `list_name.insert(index, element)`
3. `original_list.extend(list_name)`

### Append Method

As the word '*append*' suggest;. We are going to **add** elements into the **end** of the list.

> [!INFO]
> With the `.append()` method, we are going to pass the **actual** *element* as **parameter**.

> Just like writing in a *physical* notepad!

```python
# empty list
general_list = []

# output the general list ( before insertion )
print(f"General List ( Before Insertion ): {general_list}")

# append 'hello', 44, 'SS92', True to `general_list`
general_list.append("hello")
general_list.append(44)
general_list.append("SS92")
general_list.append(True)

# output the general list ( after insertion )
print(f"General List ( After Insertion ): {general_list}")
```

#### Example Code: User Input Insertion - Append

```python
# our main function
def main():
    # empty list that will hold integer numbers
    int_list: list[int] = []

    # exception handling
    try:

        # output the integer list ( before insertion )
        print(f"Integer List ( Before Insertion ): {int_list}")

        # ask the user to enter amount of integer numbers to enter
        user_amount = int(input("\nPlease Enter Amount of Numbers to Add: "))

        print()

        # iterate through the number of values to enter
        for amount in range(user_amount):
            # ask the user to enter an integer number
            user_num = int(input(f"Please Enter Integer Value ( #{amount + 1} ): "))

            # add ( "append" ) that value entered to list of integers
            int_list.append(user_num)

    # if the user does not enter integer values
    except ValueError as e:
        # output the error in question
        print(f"\nError: {e}")
        # output appropriate message
        print("<< Please Enter Integer Numbers Only!!! > > ")

    # always display the values of integer list
    finally:
        # output the integer list ( after insertion )
        print(f"\nInteger List ( After Insertion ): {int_list}")


# source the main function
if __name__ == "__main__":
    main()
```

### Insert Method

With the `.insert()` method... We are going to **specify** at which *index* / *position* and what *element* is going to be added in the list.

> [!INFO]
> Therefore, we are going to have to pass **two** parameters whereby the *first* parameter is the **index** of insertion and the *second* parameter is going to be the **element** to be added.

> Think of having the power of "spreadshits" ( *yes, "spreadshits"* ) with you!

```python
# general list containing some elements
general_list = [2, 4, 6]

# output the general list ( before insertion )
print(f"General List ( Before Insertion ): {general_list}")

# add ( "insert" ) the element 1, 3, 5, 7 in the correc position
# NOTE: position for next insertion is going to change
# as we are adding elements
# insert at 0th index
general_list.insert(0, "hello")
# inserted 1 value before ==> insert at 2th index
general_list.insert(2, 33.3)
# inserted 2 values before ==> insert at 4th index
general_list.insert(4, "SS92")
# inserted 3 values before ==> insert at 6th index
general_list.insert(6, False)

# output the general list ( after insertion )
print(f"General List ( After Insertion ): {general_list}")
```

> Need to add the **output** here because I need to explain something!

> [!TIP] Output
> The value should be in their **correct** *position*:
>
> ```console
> General List ( Before Insertion ): [2, 4, 6]
> General List ( After Insertion ): ['hello', 2, 33.3, 4, 'SS92', 6, False]
> ```

> [!NOTE]
> 1. Keep Inserting At '**0**'
>
> ```console
> General List ( Before Insertion ): [2, 4, 6]
> General List ( After Insertion ): [False, 'SS92', 33.3, 'hello', 2, 4, 6]
> ```
>
> In this case, you can see that the values were inserted in a _**descending** sequence of elements_.
>
> 2. Insert at '*1*', '*2*', '*3*', '*4*'
>
> ```console
> General List ( Before Insertion ): [2, 4, 6]
> General List ( After Insertion ): [2, 'hello', 33.3, 'SS92', False, 4, 6]
> ```
>
> See how we just inserted everything _in an **ordered** sequence_ and **not** at their correct *position*!

> [!WARNING]
> The first parameter ( *i.e index / position of insertion* ) **can** take *negative values*!
>
> Below is a little example code:
>
> ```python
> # general list containing 1 element
> general_list = ["original element"]
>
> # << Insert to the Left > >
>
> # insert at -1th index
> general_list.insert(-1, "-1")
> # insert at -2th index
> general_list.insert(-2, "-2")
>
> # << Insert to the Right > >
>
> # insert at -1th index
> general_list.insert(3, "1")
> # insert at -2th index
> general_list.insert(4, "2")
>
> # display the general list
> print(f"\n\t\t\tGeneral List\n\t<< {general_list} > > ")
> ```
>
> As you can see above, we have `-1` and `-2` as *values* for our **index** / insert *position*.
>
> In this case, we are going to have any output that looks something like this:
>
> ```console
>
>                        General List
>       << ['-2', '-1', 'original element', '1', '2'] > >
> ```
>
> > [!BUG] Warning the Warning
> > Look at now how we have **two** elements in the list *initially*
> >
> > ```python
> > # general list containing 1 element
> > general_list = ["original 0th element", "original -1th element"]
> >
> > # insert at -1th index
> > general_list.insert(-1, "-1")
> >
> > # display the general list
> > print(f"\n\t\t\tGeneral List\n\t<< {general_list} > > ")
> > ```
> >
> > Its going to insert <span style="color: red;"> in-between</span> instead of **before** first element's *position*. Again, this is because the *2nd* element in our initial list **also** has the *index* of `-1`!
>

#### Example Code: User Input Insertion - Insert

```python
# our main function
def main():
    # list that holds integer numbers
    int_list: list[int] = [2, 4, 6]

    # exception handling
    try:
        # output the integer list ( before insertion )
        print(f"Integer List ( Before Insertion ): {int_list}")

        # ask the user to enter amount of integer numbers to insert
        user_amount = int(input("\nPlease Enter Amount of Numbers to Add: "))

        print()

        # iterate through the number of values to enter
        for amount in range(user_amount):
            # ask the user to enter insert position / index
            user_index = int(input("Please Enter Insert Position of Value: "))
            # ask the user to enter integer number to add
            user_num = int(
                input(f"Please Enter Value to Insert at Position '{user_index}': ")
            )

            # add ( "insert" ) that value at required insert position
            int_list.insert(user_index, user_num)

            # display the list after inserting each value
            print(f"\nInteger List ( After Adding '{user_num}' ): {int_list}\n")

    # if the user does not enter integer values
    except ValueError as e:
        # output the error in question
        print(f"\nError: {e}")
        # output appropriate message
        print("<< Please Enter Integer Numbers Only!!! > > ")

    # always display the values of integer list
    finally:
        print("\n<< After Insertion of Values > > \n")
        # output the integer list ( after insertion )
        print(f"Integer List ( After Insertion ): {int_list}")


# source the main function
if __name__ == "__main__":
    main()
```

> Here, we are going to have *1 extra* ( *in terms of program function* ) line to ask the user to enter **index** of the integer value to *add*!

### Extend Method

Compared to our `.append()` and `.insert()` method which takes an **element** and **index** ( *for the `.insert()` method* ).

But with the `.extend()` method, we are **not** going to pass the *position* nor the *element* itself.

> [!INFO]
> The `.extend()` method takes *another* **list** ( _or more specifically an '**iterable**'_ ) as a parameter!

```python
# general list containing some elements
general_list = [True, False, "Hello World"]

# output the general list ( before insertion )
print(f"General List ( Before Insertion ): {general_list}")

# integer list containing some elements
int_list: list[int] = [1, 2, 3, 4, 5]

# add the elements found in the general list
general_list.extend(int_list)

# output the general list ( after insertion )
print(f"General List ( After Insertion ): {general_list}")
```

In this case, out output is going to look like this:

```console
General List ( Before Insertion ): [True, False, 'Hello World']
General List ( After Insertion ): [True, False, 'Hello World', 1, 2, 3, 4, 5]
```

> [!NOTE]
> See how when we added the **elements** found in the list 'int_list' to our 'general_list'.
>
> We see that it keeps its "*order*" and it appends that *whole* list to the **end** of our general list ( *just like the `.append()`* ) method.
>
> > Basically, what I am trying to say is that we **won't** be able to change the **order** during the *insertion* with the `.extend()` method!
>

### List Comprehension - Insertion of Elements

Even though that this should have been in the section / heading below as we are **not** using any *functions* or *methods* here to **add** elements into a list.

Nevertheless, many people use *list comprehension* as its really cool and functional!

```python
# integer list containing integer numbers starting from 500 to 550
int_list:list[int] = [(num + 500) for num in range(51)]

# output the integer list ( after insertion )
print(f"Integer List ( After Insertion  ): {int_list}")
```

As you can it is really useful for things like **bulk inserts** and generating lists based on **ranges** or simple **conditions**

Below you are going to find some more examples:

```python
# integer list that hold even integer numbers
list_even: list[int] = [even_num for even_num in range(51) if even_num % 2 == 0]

# integer list that hold odd integer numbers
list_odd: list[int] = [odd_num for odd_num in range(51) if odd_num % 2 != 0]

# list that holds surnames of people
surnames: list[str] = ["senna", "hamilton", "vettel", "verstappen"]

# re-define 'surnames' so that all surnames are upper-cased
surnames: list[str] = [surname.upper() for surname in surnames]

# list that holds car brands
car_brands: list[str] = ["Mazda", "Nissan", "Toyota", "Porsche", "BMW"]

# list that holds car brands with 'a' in their brand name
car_brands_with_a: list[str] = [brand for brand in car_brands if "a" in brand]
```

Again, I am not going to include a example with user-input as this is primarily used on conditions that I mentioned above ( *i.e bulk insert and / or specific* ).

### Insertion of Data in Other Ways

The **simplest** and **easier** ways to *add* elements into a list in Python are to use the `.append()` and `.insert()` methods.

But that does not mean that there *no* other ways to insert elements into a list! In this very section, we are going to learn some ways on *adding* elements **without** using any functions or methods.

> [!NOTE]
> Our **element** to insert should be of *type* **list**!
>
> If you are going to **add** the element `element`; then you are going to have to add `[element]`.

> [!TIP]
> <p align="center"> Don't Use These Ways!!!</p>

#### Concatenation Operator

> Do I even need to write anything here?

```python
# general list containing 1 element
general_list = [0]

# insert at 0th index ( single element )
first_new_list = [-1] + general_list

# insert at 0th index ( multiple elements )
second_new_list = [-3, -2] + first_new_list

# insert at the last index ( single element )
third_new_list = second_new_list + [1]

# insert at the last index ( multiple element )
forth_new_list = third_new_list + [2, 3]
```

The output for the above code will be:

```console
[-3, -2, -1, 0, 1, 2, 3]
```

> [!WARNING]
> This is very **limited** and very **inefficient**!
>
> This is due to the fact at we can only add values "*before*" or "*after*". What I mean is that we <span style="color: red;"> cannot</span> add to a **specific index** inside the list.
>
> We can only insert element(s) at the very first index ( *0th index* ) or very last index ( *length of array - 1* )!
> Additionally, we **need** to create another list **each time** we want to *add* elements into the list.



#### Slice Operator

As you know, you can use the *slice* `:` operator do manipulate text / characters in a string. But we can also use it to insert data into a list.

##### Before We Start

The *anatomy* of the slice operator is as follows:

```console
variable_name = [start:end:step]
```

> [!NOTE]
> - The value of `start` is **inclusive** ( *starts with `1`* )
> - The value of `end` is **exclusive** ( *starts with `0`* )

Additionally, this is an example code that you can play with to get an idea for the `:` operator.

```python
# variable that will hold a string of numbers ( literally )
numbers = "123456789"
# variable that will hold an email
email_string = "someone@joe'smama.com"

print("\n<< Display Odd and Even Numbers > > \n")

# display odd numbers only
print(f"Odd Numbers: {numbers[::2]}")
# display even numbers only
print(f"Even Numbers: {numbers[1::2]}")

print("\n<< Email String - Manipulation > > \n")

# display the reverse of the string
print(f"Reversed String: {email_string[::-1]}")

"""
NOTE: I am starting from '1' even for 'stop' ( for the sake of the comment )
username ==> start from first character
"""

# break down the email
print(
	f"Username: {email_string[:7]} | Domain: {email_string[8:17]} | Top-Level Domain: {email_string[-4::]}"
)
```

##### Mimic Append Method

```python
# general list containing some elements
general_list = [1, 2, 4]

# adding single element
general_list[len(general_list) :] = [5]
# adding multiple elements
general_list[len(general_list) :] = ["six", "seven", "eight"]
```

In this case, the output is going to be:

```console
[1, 2, 4, 5, 'six', 'seven', 'eight']
```

##### Mimic Insert Method

```python
# general list containing some elements
general_list = [1, 2, 4, 6]

# variables that will hold insert indices / positions
# insert at the 2th index
insert_position_1 = 2
# insert at the 4th index ( after adding 1 value )
insert_position_2 = 4
# insert at the 6th index ( after adding 2 values )
insert_position_3 = 6

# adding single element
general_list[insert_position_1:insert_position_1] = [3]
general_list[insert_position_2:insert_position_2] = [5]
# adding multiple elements
general_list[insert_position_3:insert_position_3] = ["seven", "eight", "nine"]

# insert at 0th index ( single element )
general_list[0:0] = [0]
# insert at 0th index ( multiple elements )
general_list[0:0] = ["-1", "-2", "-3"]
```

In this case, the output is going to be:

```console
['-1', '-2', '-3', 0, 1, 2, 3, 4, 5, 6, 'seven', 'eight', 'nine']
```

#### Combining Both Concatenation and Slice Operator

> This is actually getting annoying now!

```python
# general list containing 1 element
general_list = [-1, 0, 1]

# insert at 1th index and 3th index ( after adding 1 element )
first_new_list = general_list[:1] + ["|"] + general_list[1:]
second_new_list = first_new_list[:3] + ["|"] + first_new_list[3:]
```

The output for the code above should look like this:

```console
[-1, '|', 0, '|', 1]
```

> [!INFO] Some Notes and *Useful* Information
> - Elements to insert should be of *type* **list**
> - **Need** to create new list *each time*
>
> > [!WARNING]
> > <p align="center"> Worst Than Hitler!!!</p>
>

## Removal of Data

There are 3 **main** *methods* and 1 *statement* to **remove** elements from a list, they are:

1. `list_name.clear()`
2. `list_name.pop(index)`
3. `list_name.remove(element)`

### Clear Method

As the word '*clear*' suggests. We are going to **remove** *all* the elements from a list.

> [!INFO]
> With the `.clear()` method, we have **nothing** to pass ( *as parameters* ).
>
> > [!WARNING]
> > This is going to **delete** <span style="color: red;"> everything</span> from the list!!!
>

> Its like *burning* a while notepad!

```python
# general list containing some elements
general_list = [55, "shit", 69.69, True, False, 5 + 4j]

# output the general list ( before clearing )
print(f"General List ( Before Clearing ): {general_list}")

# clear the list
general_list.clear()

# output the general list ( after clearing )
print(f"General List ( After Clearing ): {general_list}")
```

Well, we should have **nothing** in our `general_list` at the end of our program:

```console
General List ( Before Clearing ): [55, 'shit', 69.69, True, False, (5+4j)]
General List ( After Clearing ): []
```

### Pop Method

From above, we know that our [[#Append Method | `.append()`]] method is going to *insert* elements at the **end** of a list.

Similarly, the `.pop()` method is going to *remove* elements found at the **end** of a list.

> [!INFO]
> Now, if you want to **only** remove the *last* element from a list... Then, **no** need to pass any parameters!
>
> > By default, the parameter for the *index* is set to `-1`.
>
> But if you want to **remove** a *specific* element... Then, you **are** going to have the pass the *index* of that element.

> Its like removing 1 plate from a stack of plates!

```python
# general list containing some elements
general_list = [55, "shit", 69.69, True, False, 5 + 4j]

# output the general list ( before removal )
print(f"General List ( Before Removal  ): {general_list}\n")

# pop the last 2 elements
general_list.pop()
print(f"General List ( During Removal  ): {general_list}")
general_list.pop()
print(f"General List ( During Removal  ): {general_list}")

# remove the first element
general_list.pop(0)
print(f"General List ( During Removal  ): {general_list}")

# output the general list ( after popping )
print(f"\nGeneral List ( After Popping ): {general_list}")
```

In this case, the output we are expecting is:

```console
General List ( Before Removal  ): [55, 'shit', 69.69, True, False, (5+4j)]

General List ( During Removal  ): [55, 'shit', 69.69, True, False]
General List ( During Removal  ): [55, 'shit', 69.69, True]
General List ( During Removal  ): ['shit', 69.69, True]

General List ( After Popping ): ['shit', 69.69, True]
```

> [!INFO]
> If we are trying to remove data from an <strong> <span style="color: red;"> empty</span> </strong> list; the `.pop()` method will **raise** a '*IndexError*'!

> [!TIP] Keeping the value popped!
> It is good that I mention that we can place the *element* that we just popped into a **variable** to be used later... Here is a shitty example ( *that does the job of explaining this* ):
>
> ```python
> # general list containing some elements
> general_list = [55, "shit", 69.69, True, False, 5 + 4j]
>
> # remove the last element and place that element into a variable
> last_value_removed = general_list.pop()
>
> # display the element that was remvoed
> print(f"Element Removed: {last_value_removed}")
> ```
>
> In this case, we are going to see that the output is going to be:
>
> ```console
> Element Removed: (5+4j)
> ```

#### Example Code: User Input to Remove Multiple Items From End

```python
# our main function
def main():
    # general list containing some elements
    general_list = [55, "shit", 69.69, True, False, 5 + 4j]

    # exception handling
    try:
        # output the general list ( before removal )
        print(f"General List ( Before Removal  ): {general_list}\n")

        # ask the user to enter amount of integer to remove from list
        user_amount = int(
            input("\nPlease Enter Amount Elements to Remove ( From End ): ")
        )

        # iterate through the amount
        for amount in range(user_amount):
            # remove the last element from list
            general_list.pop()
            # display the list during removal of that element
            print(f"General List ( During Removal  ): {general_list}")

    # if the user does not enter integer values
    except ValueError as e:
        # output the error in question
        print(f"\nError: {e}")
        # output appropriate message
        print("<< Please Enter Integer Numbers Only!!! > > ")

    # if there is nothing in list when trying to remove
    except IndexError as e:
        # output the error in question
        print(f"\nError: {e}")
        # output appropriate message
        print("<< There is Nothing in List! > > ")

    # always display the elements of general list
    finally:
        print("\n<< After Removal of Elements > > \n")
        # output the general list ( after removal )
        print(f"General List ( After Removal  ): {general_list}\n")


# source the main function
if __name__ == "__main__":
    main()
```

### Remove Method

Do you want to the difference? **Element** and *not* **Index**. That's all you need to know here!

> [!INFO]
> With the `.remove()` method, we are going to pass the **actual** *element* as **parameter**.

> [!WARNING]
> The `.remove(element_of_correct_datatype)` method is _data type **sensitive**_!
>
> This means that we **need** to know the *data type* of the element that we are trying to **remove**.

```python
# general list containing some elements
general_list = [55, "shit", 69.69, True, False, 5 + 4j]

# output the general list ( before removal )
print(f"General List ( Before Removal  ): {general_list}")

# WARNING: the below code will NOT run...
# stops the execution of the program!!!
# uncomment code to verify
# general_list.remove("55")

# remove the element '55' from the list
general_list.remove(55)
# remove the element 'True' from the list
general_list.remove(True)
# remove the element '5 + 4j' from the list
general_list.remove(5 + 4j)
# remove the element 'shit' from the list
general_list.remove("shit")

# output the general list ( after removal )
print(f"General List ( After Removal ): {general_list}")
```

Therefore, the output for the above code will be:

```console
General List ( Before Removal  ): [55, 'shit', 69.69, True, False, (5+4j)]
General List ( After Removal ): [69.69, False]
```

> [!INFO]
> If an **element** that we are trying to remove does <span style="color: red;"> not</span> exists; the `.remove()` method will **raise** a '*ValueError*'!

> Its like *crossing* out tasks in out notepad **at random**!

> [!WARNING] First Occurrence Only
> Let's say that you have the following code below
>
> ```python
> # integer list containing some elements
> int_list: list[int] = [1, 27, 33, 44, 33, 33, 69, 5, 55]
>
> # output the general list ( before removal )
> print(f"General List ( Before Removal  ): {int_list}")
>
> # removing the element '33' from the list
> int_list.remove(33)
>
> # output the general list ( after removal )
> print(f"General List ( After Removal ): {int_list}")
> ```
>
> If we now use the `.remove()` function and try to remove the element '33', this will be the output:
>
> ```console
> General List ( Before Removal  ): [1, 27, 33, 44, 33, 33, 69, 5, 55]
> General List ( After Removal ): [1, 27, 44, 33, 33, 69, 5, 55]
> ```
> As you can see, it only removed the **first occurrence** of the *element* '33'!
>
> Meaning to delete every instance '33', we could:
>
> 1. Run `int_list.remove(33)` multiple times
> 2. Use **List Comprehension** like `int_list: list[int] = [num_to_keep for num_to_keep in int_list if num_to_keep != 33]` ( *re-declaring if you wish* )
> 3. Simply use a `for` loop and iterate *backwards* with the `.remove()` method
>
> > But this is what I was saying about '*First Occurrences*'!

#### Example Code: User Input Specific Elements to Remove

```python
# our main function
def main():
    # integer list containing some elements
    int_list: list[int] = [1, 2, 3, 4, 5, 6, 8, 9, 0]

    # exception handling
    try:
        # output the integer list ( before removal )
        print(f"Integer List ( Before Removal  ): {int_list}")

        # ask the user to enter amount of elements to remove
        user_amount = int(input("\nPlease Enter Amount of Values to Remove: "))

        print()

        # iterate through the amount
        for amount in range(user_amount):
            # display the list
            print(f"\nInteger List: {int_list}")

            # ask the user to enter element to remove
            user_element = int(input("Please Enter Element to Remove: "))

            # exception handling
            try:
                # remove that specific element from the list
                int_list.remove(user_element)

            # if the user enter something that is not found in the list
            except ValueError as e:
                # output the error in question
                print(f"\nError: {e}")
                # output appropriate message
                print(f"<< Element {user_element} is NOT Found in List! > > ")

    # if the user does not enter integer values
    except ValueError as e:
        # output the error in question
        print(f"\nError: {e}")
        # output appropriate message
        print("<< Please Enter Integer Numbers Only!!! > > ")

    # always display the elements of integer list
    finally:
        print("\n<< After Removal of Elements > > \n")
        # output the integer list ( after removal )
        print(f"Integer List ( After Removal ): {int_list}")


# source the main function
if __name__ == "__main__":
    main()
```

### Delete Statement

> [!TIP]
> <p align="center"> Do Yourself a Favour and Never Implement This!!!</p>

We don't normally use `del` but who said that it does not work?

> Consider a mix between the [[#Slice Operator]] and the [[#Pop Method]]!

> [!INFO]
> The way that we are going to use is going to be with `del`, **indices** of elements and **list** *data type*.

Consider the example below:

```python
# integer list containing some elements
int_list = [55, "shit", 69.69, True, False, 5 + 4j]

# output the integer list ( before removal )
print(f"Integer List ( Before Removal  ): {int_list}")

# remove at 4th index ( after removal of 1 element )
# NOTE: mimic the pop method
del int_list[-1]

# remove from 1th index to 4th index
del int_list[1:5]

# output the integer list ( after removal )
print(f"Integer List ( After Removal ): {int_list}")
```

In this case, we should only have 1 value left in the list:

```console
Integer List ( Before Removal  ): [55, 'shit', 69.69, True, False, (5+4j)]
Integer List ( After Removal ): [55]
```

> [!NOTE]
> To be honest it **does** make sense. For example, if we have `del list_name[0]`.
>
> We know by itself, `list_name[0]` is going to access the value found at *0th index* and as the word '*del*' suggests... We are going to be **deleting** the value found at the 0th index!
>
> Additionally, we can combine this with the slice operator `:` and have the ability to remove a bunch of things in whatever way to want!

##### Mimic Clear Method

We can use the `del` statement to mimic the `.clear()` method like so:

```python
# general list containing some elements
general_list = [55, "shit", 69.69, True, False, 5 + 4j]

# output the general list ( before removal )
print(f"General List ( Before Removal  ): {general_list}")

# remove every element from list
del general_list[:]

# output the general list ( after removal )
print(f"General List ( After Removal ): {general_list}")
```

Well, as expected we have nothing in the list!

```console
General List ( Before Removal  ): [55, 'shit', 69.69, True, False, (5+4j)]
General List ( After Removal ): []
```

#### Example Code: Even / Odd Lists

```python
# our main function
def main():
    # empty list which will keep track of what to delete
    indices_to_del = []

    # exception handling
    try:
        # ask the user how many values he wants to list to have
        user_list_amount = int(input("Please Enter Amount of Values to have in List: "))

        # integer list containing integer values in the sepecified amount
        int_list = [num for num in range(user_list_amount + 1)]

        # display the screen
        print("\n\t<< Even / Odd List Generator > > \n")
        print("\tOption [1]: Even List")
        print("\tOption [2]: Odd List\n")

        # ask the user to enter if he wants to create even / odd list
        user_list = int(input("Do You Want an Even or Odd List: "))

        # if the user wants an even list
        if user_list == 1:
            # make a copy of the list
            even_list = int_list

            # find all indices of value to remove
            for index in range(len(int_list)):
                # check if value at index is even
                if even_list[index] % 2 != 0:
                    # add that index to `indices_to_del` as it contains odd numbers
                    indices_to_del.append(index)

            # delete all odd numbers found in `even_list`
            # NOTE: deleting in reversed so as to avoid index shifting
            for index in indices_to_del[::-1]:
                # delete all the odd numbers from list
                del even_list[index]

            # display the even list
            print(f"\n\t << Even List > > \n{even_list}\n")

        # if the user wants an odd list
        elif user_list == 2:
            # make a copy of the list
            odd_list = int_list

            # find all indices of value to remove
            for index in range(len(int_list)):
                # check if value at index is odd
                if odd_list[index] % 2 == 0:
                    # add that index to the `indices_to_del` as it contains even numbers
                    indices_to_del.append(index)

            # delete all even numbers found in `even_list`
            # NOTE: deleting in reversed so as to avoid index shifting
            for index in indices_to_del[::-1]:
                # delete all the even numbers from list
                del odd_list[index]

            # display the odd list
            print(f"\n\t << Odd List > > \n{odd_list}\n")

        # if the user does not enter correct input
        else:
            # output appropriate message
            print("\n<< Invalid Input! Exiting! > > \n")

            # exit the program with errors
            exit(1)

    # if the user does not enter integer values
    except ValueError as e:
        # output the error in question
        print(f"\nError: {e}")
        # output appropriate message
        print("<< Please Enter Integer Numbers Only!!! > > ")


# source the main function
if __name__ == "__main__":
    main()
```

> One of the **worst** programs ( *in terms of optimisation* ) what I created... I have made some shitty programs!
>
> To create an even list from a list of **ordered** integer numbers we could simply do something like this:
>
> ```python
> # integer list containing 100 numbers
> int_list: list[int] = [num for num in range(101)]
>
> # create the even integer list
> even_list: list[int] = int_list[::2]
>
> # create the odd integer list
> odd_list: list[int] = int_list[1::2]
>
>
> print(f"\n\t<< Even List > > \n{even_list}")
> print(f"\n\t<< Odd List > > \n{odd_list}")
> ```

> [!NOTE]
> Given that we did do:
>
> 1. `even_list = int_list` and `odd_list = int_list` to copy the list
> 2. `indices_to_del[::-1]` to reverse the list
>
> > [!WARNING] Obsidian Markdown is Fucking Me Up!
> > Because I use the plugin [Iconize](https://github.com/FlorianWoelki/obsidian-iconize); to use these icons... I need to type `::`... Well, I think you get the idea of why its not rendering for the above inline code block.
>
> There are actual *methods* and *functions* that does the same things but **better** in terms of *performance* and *readability* and others shits!
>
> Additionally, while using slice operator to **reverse** the list... We are going to be creating a **new instance** of that list *each* time we reverse it!
>
> > As my lecturer said "*I trust the guy that wrote these functions and methods*".
>

### List Comprehension - Removal of Elements

From using [[#List Comprehension - Insertion of Elements | list comprehension]] to insert elements into a list based on a *specific* **condition**.

Similarly, we are going to be **removing** elements from a list using said *list comprehension*.

```python
# general list containing some elements
general_list = [55, "shit", 69.69, True, False, 5 + 4j]

# output the general list ( before removal )
print(f"General List ( Before Removal  ): {general_list}")

# remove the element '69.69' from the general list
general_list = [element for element in general_list if element != 69.69]

# output the general list ( after removal )
print(f"General List ( After Removal  ): {general_list}")
```

In this case, we should **not** have the element '69.69' in our `general_list`:

```console
General List ( Before Removal  ): [55, 'shit', 69.69, True, False, (5+4j)]
General List ( After Removal  ): [55, 'shit', True, False, (5+4j)]
```

> [!WARNING]
> Okay, I have to spill the beans! Using list **comprehension** to remove element from the **same** list like we did above with the `general_list` is actually called ( *drumroll please* ) <span style="color:orange;"> reassignment</span> .
>
> Well, it does *look* like we are using list comprehension to "**remove**" that element but not really.
>
> > With the above code, we are simply reassigning the list!
>
> > [!SUCCESS] But
> > If we did use another *variable name* for our list like [`fuck_you_tony`](https://www.youtube.com/watch?v=WsHeLhsFrvw).
> >
> > Then this would actually be called '**Removal of Element**'!!!
>

### Removal of Data in Other Ways

Similar with our '[[#Insertion of Data in Other Ways]]'... Just don't listen to what I am talking about here!

> [!TIP]
> <p align="center"> Don't Use These Ways!!!</p>

#### Slice Operator

Compared to the [[#Slice Operator]] found above... We are also going to use the same `:` operator to **remove** elements from a list!

```python
# general list containing some elements
general_list = [55, "shit", 69.69, True, False, 5 + 4j]

# output the general list ( before removal )
print(f"General List ( Before Removal  ): {general_list}")

# remove every element from list
# NOTE: mimicking `.clear()` method
# we did already looked at how we used `del` and slice operator to clear list
# here is another way of doing it
general_list[:] = []

# output the general list ( after removal )
print(f"General List ( After Removal  ): {general_list}")
```

> *Do I even need to write the output*?

> [!TIP]
> To be honest this is just the *same* thing as [[#Delete Statement]] but **instead** of using the `del` *keyword* at the beginning of the list.
>
> We are instead going to just fill these *indices* with **nothingness** with ` = []`!
>
> > But things like `[start:stop]` works just as well as we expect them to *run*.

> [!INFO] Argument
> Well, in that case, we might as we do this:
>
> ```python
> # re-create the variable `general_list`
> general_list = []
> ```
>
> Simple, Done and Dusted!
>
> [But Wait! There's More](https://www.youtube.com/watch?v=wkGLxQ3iolo)... The thing that we just did is called a fucking **declaration** and in this case we **don't** want to *re-declare* our variable.

#### My Version

Again, its one of those *shitty* codes that is completely **un-optimised** but works as expected!

In my version, I am still keeping the original list as it is. I am going to create another list which will take all the elements that we need to reject the element that we don't need ( *obviously* ).

```python
# general list containing some elements
general_list = [55, "shit", 69.69, True, False, 5 + 4j]
# empty list that will hold the values of 'general_list'
updated_general_list = []

# output the original general list ( before removal )
print(f"Original General List ( Before Removal  ): {general_list}")
# output the updated general list ( before insertion )
print(f"Updated General List ( Before Insertion  ): {updated_general_list}")

# remove the elements '5 +4j' and 'shit' from the list

# iterate through the original list
for element in general_list:
    # condition to be able to removed required elements
    if element != 5 + 4j and element != "shit":
        # add ( "append" ) other elements into updated list
        updated_general_list.append(element)


# output the original general list ( after removal )
print(f"Original General List ( After Removal  ): {general_list}")
# output the updated general list ( after insertion )
print(f"Updated General List ( After Insertion  ): {updated_general_list}")
```

> [!NOTE] My Dumbass Also Thought About This!!!
> I also did think of this code which to be honest... I don't think you should look at!
>
> ```python
> # general list containing some elements
> general_list = [55, "shit", 69.69, True, False, 5 + 4j]
>
> # output the original general list ( before removal )
> print(f"Original General List ( Before Removal  ): {general_list}")
>
> # clear the list
> general_list.clear()
>
> # remove the elements '5 +4j' and 'shit' from the list
>
>
> # iterate through the original list
> for element in general_list:
>    # condition to be able to removed required elements
>    if element != 5 + 4j and element != "shit":
>        # add ( "append" ) other elements into updated list
>        general_list.append(element)
>
>
> # output the original general list ( after removal )
> print(f"Original General List ( After Removal  ): {general_list}")
>
> ```

## Miscellaneous Methods / Functions

> I don't know what to call this section... But I know that I am here for this!

### List Equality - Inequality

As the name suggests, we are going to try to see if 2 *lists* are **equal** to each other.

> [!INFO] 
> Now, you might be asking yourself about how we can go about this... Well just use '\==' operator.
>
> > Like we usually do!
>
> > [!NOTE] Little Rant
> > BTW because I am using one of the greatest program to write this; [Obsidian](https://obsidian.md); additionally, I have the plugin [dataview](https://github.com/blacksmithgu/obsidian-dataview) installed which prevents me to write 2 equal signs consecutively in *inline code blocks*.
> > Hence the `'=='` ( *but this now does show any errors, WTF!* )
>

```python
# import the 'randint' function from the random module
from random import randint

# integer list containing some elements
int_list: list[int] = [1, 2, 3, 4, 5]
# character list containing some elements
char_list: list[str] = [chr(num) for num in range(65, 70)]

# check if lists are equal to each other

# << integer list > >
print(f"Integer List Equal? {int_list == [randint(0, 9) for i in range(5)]}")
print(f"Integer List Equal? {int_list != [num for num in range(5, 0, -1)]}")
print(f"Integer List Equal? {int_list == [1, 2, 3, 4, 5]} <---\n")

print("-" * 50, "\n")

# << character list > >
print(f"Character List Equal? {char_list == [randint(0, 9) for i in range(5)]}")
print(f"Character List Equal? {char_list != [chr(num) for num in range(69, 64, -1)]}")
print(f"Character List Equal? {char_list == [chr(num) for num in range(65, 70)]} <---")
```

We should simply get something like this:

```console
Integer List Equal? False
Integer List Equal? True
Integer List Equal? True <---

-------------------------------------------------- 

Character List Equal? False
Character List Equal? True
Character List Equal? True <---
```

> I think you do get the point!

### Split Method

> [!NOTE]
> This is **not** part of the `dir(list)` *functions* and *methods*. But as we can **create** list it... I think its worth adding it here!
>

> [!INFO]
> The `.split()` can take an **optional** *parameter* of string.
> By **default** this *parameter* is ' ' or `<Space> `
>
> > See below for examples!
>

> [!WARNING]
> The `.split()` method can **only** be used on **string** *data types*!

```python
# string variable that is assigned a word
one_word = "One"
# string variable that is assigned a some numbers
some_nums = "2 | 2 | 3 | 4 | 5 | 6"
# string variable that is assigned a sentence
some_string = "At Your Service Sir"
# string varaible holding the header of a text file
header_csv_file = "Barcode Number,Product Name,Quantity,Production Date, Expiry Date"

print(f"\nSplitted Word: {one_word.split()}")
print(f"Splitted Numbers: {some_nums.split(' | ')}")
print(f"Splitted Sentence: {some_string.split()}")
print(f"Splitted CSV Header: {header_csv_file.split(',')}")

# ask the user to enter full name separated by ' ' / <Space> character
user_full_name = input(
    "\nPlease Enter Full Name ( seperated by 'Space' characters ): "
).split()

print(f"\nSplitted Full Name: {user_full_name}")
```

The output for the above code block will look something like this:

```console

Splitted Word: ['One']
Splitted Numbers: ['1', '2', '3', '4', '5', '6']
Splitted Sentence: ['At', 'Your', 'Service', 'Sir']
Splitted CSV Header: ['Barcode Number', 'Product Name', 'Quantity', 'Production Date', ' Expiry Date']

Please Enter Full Name ( seperated by 'Space' characters ): Aryton GOAT Senna          

Splitted Full Name: ['Aryton', 'GOAT', 'Senna']
```

> [Heheheh](https://www.youtube.com/watch?v=ZwOxM0-byvc&t=5s)...

> [!WARNING]
> This is code below is **not** going to be possible as; again, the `.split()` method works only with **string** *data types*!
>
> ```python
> # this is NOT allowed
> ```

> [!INFO]
> I use the `.split()` method ( *heavily* ) when reading and **extracting** *words* or *characters* from a **text file**!
>
> Additionally, you can place the "*splitted*" output into a **varaible**.
>
> > I was lazy here and just printed them out!
>

### Copy Method

Remember when we finished writing the '[[#Example Code Even / Odd Lists | Even / Odd List]]' example code, I told you that there was *specific* functions / methods that can **copy** the *elements* a list into **another** list?

> [!INFO]
> With the `.copy()` method, we have **nothing** to pass ( *as parameters* ).

> Well, here we are!

```python
# character list containing 1000 elements
character_list: list[str] = [chr(num) for num in range(32, 1032)]

# create a copy of the list containing the characters
character_list_copy: list[str] = character_list.copy()
```

Following my lecturer's advice... Instead of using the a `for` loop and the `.append()` method to create a **copy** of a list. Just use the **simple** and **effective** `.copy()` method!

### Count Method

As the word '*count*' suggests, there will be some *counting* that will be involved with this method!

> [!INFO]
> The `.count(element)` method is going to *count* the **number of occurrences** that the `element` element appears in the list.
>
> Additionally, our `element` can be of **any** *type*!

```python
# general list containing some elements ( with some repeating elements )
general_list = [1, 1, "hello", "hello", "A", "A", True, False, False, 69.69]

# count number of occurrences of each element in the list
print(f"\n'{general_list[0]}' Count: {general_list.count(1)}")
print(f"'{general_list[2]}' Count: {general_list.count('hello')}")
print(f"'{general_list[4]}' Count: {general_list.count('A')}")
print(f"'{general_list[6]}' Count: {general_list.count(True)}")
print(f"'{general_list[7]}' Count: {general_list.count(False)}")
print(f"'{general_list[9]}' Count: {general_list.count(69.69)}")
```

In this case, we should get the output:

```console

'1' Count: 3
'hello' Count: 2
'A' Count: 2
'True' Count: 3
'False' Count: 2
'69.69' Count: 1
```

> [!WARNING] But Wait!
> The keen eyes of yours might see that we only have **two** '1' and **one** 'True' element. But how are we getting **three** for each of them?
>
> Well, you know how in some light switches or even the switches in the back of *power supplies* had '0' and '1'?
>
> This is basically the same thing happening here:
>
> ```console
> On = 1 = True
> Off = 0 =  False 
> ```
>
> > [!NOTE] Therefore
> > In our above list, as we have **two** '1' and **one** True. It just becomes **three** if we use our `.count()` method.
> >
> > Additionally, if we try to count the number of occurrences of an **element** that is <span style="color: red;"> not</span> found in the list; the `.count()` method will return the value '**0**'!
>

### Index Method

As the word '*index*' suggests... This method is going to return the **index** of an element found in the list.

> [!INFO]
> The `.index(element)` method is going to take the actual **element** that we are trying to find the *index* of.
>
> Similar to our `.count()` method, the `element` can be of **any** *type*!

```python
# general list containing some elements ( with some repeating elements )
general_list = [1, "hello", "A", 69.69]

# count number of occurrences of each element in the list
print(f"\n'{general_list[0]}'s Index: {general_list.index(1)}")
print(f"'{general_list[1]}'s Index: {general_list.index('hello')}")
print(f"'{general_list[2]}'s Index: {general_list.index('A')}")
print(f"'{general_list[3]}'s Index: {general_list.index(69.69)}")
```

Here, we should get an output like this:

```console
'1's Index: 0
'hello's Index: 1
'A's Index: 2
'69.69's Index: 3
```

> [!INFO]
> If an **element** that we are trying to find the *index* of does <span style="color: red;"> not</span> exists; the `.index()` method will **raise** a '*ValueError*'!

### Reverse Method

> Well, do I need to explain?

> [!INFO]
> Our `.reverse()` method does **not** take any *parameters* similar to out lovely little `.copy()` method!

```python
# general list containing some elements
general_list = [55, "shit", 69.69, True, False, 5 + 4j]

# output the general list ( before reversing )
print(f"General List ( Before Reversing ): {general_list}")

# clear the list
general_list.reverse()

# output the general list ( after reversing )
print(f"General List ( After Reversing ): {general_list}")
```

Therefore, the output that we are going to get is:

```console
General List ( Before Reversing ): [55, 'shit', 69.69, True, False, (5+4j)]
General List ( After Reversing ): [(5+4j), False, True, 69.69, 'shit', 55]
```

> As you can, we successfully **reversed** our list!

### Sort Method

The `.sort()` method is going to allow us to *sort* our **elements** found in our list. This sorting can be either be in *ascending* or *descending* order or other *special options*!

> [!INFO]
> The `.sort()` method can take 2 **optional** parameters:
>
> - key ( *only used on string data types* )
> - reverse
>
> > Refer to the example below for both *knowledge* and *understanding*!
>

> [!WARNING]
>
> > [!NOTE]
> > This will do an **in-place** sorting whereby it will *move* the elements in the list that we just sorted.
>
> The `.sort()` method can only work on **either** *string* **or** *integer* data types and <span style="color: red;"> not</span> **both**!
>
> In short, we can sort the following below:
>
> ```python
> int_list: list[int] = [1, 4, 3, 2, 5]
> char_list: list[str] = ['z', 'a', 'j', 'b', 'x', 'c', 'y']
> code_list: list[str] = ['99SS', 'B050', 'A1020', '01YS', '1X10']
> ```
>
> But the following <span style="color: red;"> cannot</span> be sorted by the `.sort()` method!
>
> ```python
> general_list = [55, "shit", 69.69, True, False, 5 + 4j]
> ```

#### Ascending Order

```python
# integer list containing some elements
int_list: list[int] = [1, 4, 3, 2, 5]
# character list containing some elements
char_list: list[str] = ["z", "a", "j", "b", "x", "c", "y"]

# output the integer list before sorting
print(f"Integer List ( Before Sorting ): {int_list}")

# sort the integer list ( ascending order )
int_list.sort()

# output the integer list after sorting
print(f"Integer List ( After Sorting [ Ascending Order ] ): {int_list}")

# output the character list before sorting
print(f"Char List ( Before Sorting ): {char_list}")

# sort the character list ( ascending order )
char_list.sort()

# output the character list after sorting
print(f"Character List ( After Sorting [ Ascending Order ] ): {char_list}")
```

Well, we should have our list sorted in the **ascending** order:

```console
Integer List ( Before Sorting ): [1, 4, 3, 2, 5]
Integer List ( After Sorting [ Ascending Order ] ): [1, 2, 3, 4, 5]
Char List ( Before Sorting ): ['z', 'a', 'j', 'b', 'x', 'c', 'y']
Character List ( After Sorting [ Ascending Order ] ): ['a', 'b', 'c', 'j', 'x', 'y', 'z']
```

#### Descending Order

Its basically the **same** code as above but we just added the 'reverse' *parameter* like so:

```python
# sort the integer list ( descending order )
int_list.sort(reverse=True)
# sort the character list ( descending order )
char_list.sort(reverse=True)
```

Well, we should have our list sorted in the **descending** order:

```console
Integer List ( Before Sorting ): [1, 4, 3, 2, 5]
Integer List ( After Sorting [ Descending Order ] ): [5, 4, 3, 2, 1]
Char List ( Before Sorting ): ['z', 'a', 'j', 'b', 'x', 'c', 'y']
Character List ( After Sorting [ Descending Order ] ): ['z', 'y', 'x', 'j', 'c', 'b', 'a']
```

#### Sort By Length of Element

Given the program below:

```python
# list containing models of cars
car_models: list[str] = ["RX-7", "R32", "Supra", "E46 M3", "992 GT3 RS"]

# output the car model list before sorting
print(f"Car Model List ( Before Sorting ): {car_models}")

# sort the car models list ( normally )
car_models.sort()

# output the car model list after sorting
print(f"Car Model List ( After Sorting [ Ascending ] ): {car_models}")
```

The above code will [simply](https://www.youtube.com/watch?v=OtjsHokKUgI&t=9s)sort the list in **ascending** order based on the *first character* of the string!

Therefore, our output should look something like this:

```console
Car Model List ( Before Sorting ): ['RX-7', 'R32', 'Supra', 'E46 M3', '992 GT3 RS']
Car Model List ( After Sorting [ Ascending ] ): ['992 GT3 RS', 'E46 M3', 'R32', 'RX-7', 'Supra']
```

But what about sorting these *strings* ( *elements* ) in terms of their lengths?

> [!NOTE]
> We are basically using the above code but we changed this line:
>
> ```python
> # sort the car models list ( sorting by length of strings )
> car_models.sort(key=len)
> ```

In this case, we are going to get an output that looks like this:

```console
Car Model List ( Before Sorting ): ['RX-7', 'R32', 'Supra', 'E46 M3', '992 GT3 RS']
Car Model List ( After Sorting [ Ascending ] ): ['R32', 'RX-7', 'Supra', 'E46 M3', '992 GT3 RS']
```

> In this case, we can see that its sorted the *strings* by its **length** ( *i.e 3, 4, 5, ...* ).

#### Example: Sorting Objects

```python
# our 'Car' class
class Car:
    # our constructor function
    def __init__(self, id: int, brand: str, model: str, capacity: int, mileage: int):
        # attributes of car objects
        self.id = id
        self.brand = brand
        self.model = model
        self.capacity = capacity
        self.mileage = mileage

    # method to display all the details of car object
    def display_details(self):
        print(f"\nCar ID: {self.id}")
        print(f"\nCar Brand: {self.brand}")
        print(f"Car Model: {self.model}")
        print(f"Car Capacity: {self.capacity}")
        print(f"Car Mileage: {self.mileage}\n")

    # method that will return the mileage of the car object
    def get_mileage(self):
        # return the mileage
        return self.mileage


# our main function
def main():
    # ( empty ) list that will keep track of all car objects
    car_objects = []

    # exception handling
    try:
        # ask the user how many car objects to create
        car_amount = int(input("\nPlease Enter Number of Cars: "))

        # variable that will generate car ID automatically
        car_id = 0

        # iterate through the amount of cars
        for car in range(car_amount):
            print(f"\n\t<< Car #{car} > > \n")

            # start asking the user about car details
            car_brand = input("Please Enter Brand of Car: ")
            car_model = input("Please Enter Model of Car: ")
            car_capacity = int(input("Please Enter Capacity: "))
            car_mileage = int(input("Please Enter Mileage: "))

            # create the car ID automatically
            car_id += 1

            # add ( "append" ) that car object to car list
            car_objects.append(
                Car(car_id, car_brand, car_model, car_capacity, car_mileage)
            )

        print("\n<< Car Objects List Before Sorting\n > > ")

        # output the car objects list before sorting
        for car in car_objects:
            print("-" * 50)
            # call method to display details of car
            car.display_details()

        # sort the car objects ( found in the list ) by its mileage
        car_objects.sort(key=Car.get_mileage, reverse=True)

        print("\n<< Car Objects List After Sorting\n > > ")

        # output the car objects list after sorting
        for car in car_objects:
            print("-" * 50)
            # call method to display details of car
            car.display_details()

    # if the user does not enter integer value where required
    except ValueError:
        # output appropriate message
        print("\n\t<< Please Enter Integer Values!!! > > \n")


# source the main function
if __name__ == "__main__":
    main()
```

### Sorted Function

> [!NOTE] Just Look at `.sort()` Method
> Yes!, this is literally the **same** ( *parameters, rules* ) thing as our `.sort()` method.
>
> But with ( *from what I can see* ) **1** difference!
>
> Instead of doing an **in-place** sorting. The output of the `sorted()` **function** can be placed in a variable.
>
> > Additionally, we can do something like `print(sorted(list_name))`!
> > Try doing this with the `.sort()` method... *You won't be able to*!
>

#### Actually!

The sorted function also works on the *strings*!

```python
# string variable which has been assigned 'axbzcy 5h2k0l1'
random_string: str = "axbzcy 5h2k0l1"

# output the string with 'sorted' function applied
print(f"\nCharacters Sorted ( Ascending Order ): \n - {sorted(random_string)}")
print(
    f"\nCharacters Sorted ( Descending Order ): \n - {sorted(random_string, reverse=True)}"
)
```

Therefore, we are going to these lists:

```console
Characters Sorted ( Ascending Order ): 
 - [' ', '0', '1', '2', '5', 'a', 'b', 'c', 'h', 'k', 'l', 'x', 'y', 'z']

Characters Sorted ( Descending Order ): 
 - ['z', 'y', 'x', 'l', 'k', 'h', 'c', 'b', 'a', '5', '2', '1', '0', ' ']
```

> Its like its performing a `.split()` method!

#### Sorted Function on Lists

```python
# integer list containing some elements
int_list: list[int] = [1, 4, 3, 2, 5]
# character list containing some elements
char_list: list[str] = ["z", "a", "j", "b", "x", "c", "y"]

# integer list that holds sorted ( ascending order )
asc_sorted_int_list: list[int] = sorted(int_list)
# character list that holds sorted ( ascending order )
asc_sorted_char_list: list[str] = sorted(char_list)

# integer list that holds sorted ( descending order )
desc_sorted_int_list: list[int] = sorted(int_list, reverse=True)
# character list that holds sorted ( descending order )
desc_sorted_char__list: list[str] = sorted(char_list, reverse=True)

print("\n<< Originals > > \n")

print(f"\tInteger List: \n\t   - {int_list}\n")
print(f"\tCharacter List: \n\t   - {char_list}")

print("\n<< Sorted ( Ascending Order ) > > \n")

print(f"\tInteger List: \n\t   - {asc_sorted_int_list}\n")
print(f"\tCharacter List: \n\t   - {asc_sorted_char_list}")

print("\n<< Sorted ( Descending Order ) > > \n")

print(f"\tInteger List: \n\t   - {desc_sorted_char__list}\n")
print(f"\tCharacter List: \n\t   - {desc_sorted_int_list}")
```

Similarly, we should be having this as output:

```console

<< Originals > >

        Integer List: 
           - [1, 4, 3, 2, 5]

        Character List: 
           - ['z', 'a', 'j', 'b', 'x', 'c', 'y']

<< Sorted ( Ascending Order ) > >

        Integer List: 
           - [1, 2, 3, 4, 5]

        Character List: 
           - ['a', 'b', 'c', 'j', 'x', 'y', 'z']

<< Sorted ( Descending Order ) > >

        Integer List: 
           - ['z', 'y', 'x', 'j', 'c', 'b', 'a']

        Character List: 
           - [5, 4, 3, 2, 1]
```

### Join Method

> [!NOTE]
> Similar to the `.split()` method, this does **not** form part of the list *functions* and *methods*... But as I think its a <span style="color: #0db9d7"> cool</span> method... Again, I think its worth adding it here!

> [!WARNING]
> This method only accepts list of **strings** ( *i.e `list[str]`* ). This means that we can use it with lists like:
>
> ```python
> car_brands: list[str] = ["Mazda", "Toyota", "Nissan", "Porsche", "Aston Martin"]
> numbers: list[str] = ['1', '2', '3', '4', '5']
> characters: list[str] = ['A', 'B', 'C', 'x', 'y', 'z']
> ```
>
> But the following <span style="color: red;"> cannot</span> be used with the `.join()` method!
>
> ```python
> general_list = [55, "shit", 69.69, True, False, 5 + 4j]
> int_list: list[int] = [1, 2, 3, 4, 5]
> float_list: list[float] = [1.2, 2.3, 3.4, 4.5, 5.6]
> ```

```python
# string lists containing some elements
sentence: list[str] = ["Today", "is", "a", "nice", "day"]
csv_header: list[str] = [
    "Barcode Number",
    "Product Name",
    "Quantity",
    "Production Date",
    " Expiry Date",
]

# join the elements with ' ' / <Space> to form a sentence
print(" ".join(sentence))

# join th elements with ',' character to form CSV header
print(",".join(csv_header))
```

Therefore, our output is going to look like this:

```console
Today is a nice day
Barcode Number,Product Name,Quantity,Production Date, Expiry Date
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!