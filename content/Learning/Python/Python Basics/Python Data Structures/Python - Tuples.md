---
id: Python - Tuples
aliases: Tuples in Python
tags:
  - python
  - data-structures
  - tuples
author: S.Sunhaloo
date: 2025-04-22
status: Completed
---

## List of Contents

- [[#What are Tuples?]]
- [[#Creation of Tuples]]
- [[#Displaying - Accessing Tuples]]
	- [[#Displaying Tuples and Tuples Value(s)]]
	- [[#Accessing Tuples Value(s)]]
- [[#Unpacking of Tuples]]
- [[#Functions and Methods of Tuples]]
	- [[#Tuple Equality - Inequality]]
	- [[#Count Method]]
	- [[#Index Method]]
- [[#Insertion and Removal?!?]]

---

> [!NOTE]
> Again, I expect you to have **already** read the notes / files '[[Python - Lists]]' and '[[Python - Two Dimensional Lists]]' before coming here!
>
> > Because I will **not** be explaining everything again!
>

# What are Tuples?

Remember how I was talking about the **difference** between *lists* and *arrays* in the note '[[Python - Lists#Arrays V/S Lists | Python - Lists]]'.

I was saying that how **arrays** have a *specific size* and how its can only keep only **one** *type* of data.

Well, **tuples** are **more related** to *arrays* than lists!

> [!WARNING] I Want Your Attention
> With **tuples** upon creation, the *elements* found inside that tuples <span style="color: red;"> cannot</span> be changed **during** the execution of the program!

This is useful for things that does **not** *change* as much! Things like colours of the rainbow, amount of legs humans have.

> "*You have 3 legs*" [That's What She Said](https://www.youtube.com/watch?v=dBUGfs9rwms)

> [!NOTE]
> Nevertheless, compared to *arrays*; tuples **can** in-fact hold multiple *data types*!

> [!TIP]
> In Python, **tuples** are basically **lists** in terms of its "*methods*" used to display them, interact with them and more!

---

# Creation of Tuples

To create tuples in Python, we use the `()` characters.

```python
# tuples of integers numbers only
int_tuple = (1, 2, 3, 4, 5)

# tuple containing most data types
general_tuple = (
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
)
```

> [!INFO] `type()` of Tuple
> If we run `print(type(int_tuple))` or `print(type(general_tuple))` we should see that we get:
>
> ```console
> <class 'tuple'>
> ```
>
> Nevertheless, the word '*tuple*' is **not** a reserved word in Python and you can create a tuple called `tuple` like so:
>
> ```python
> tuple = (1, "shitter", 'A', 69.69)
> ```
>
> > Nevertheless, this is **not** recommended as we are not going to be able to use [[#Type Annotation / Hinting]]!
>

> [!WARNING] Before We Continue... Real Real Talk!
> Back when I wrote this kind-of "*tutorial documentation*" ( *what I like to call them* ). I place a lot of emphasis on the **syntax** of Python instead of learning how to "**Problem-Solve**".
>
> This was back when I was just starting to learn Programming and Python as a whole. The reason why I did this ( *back in the day* ); its because of the **shitty education** system!
>
> Since very little, we have been engraved in our minds that we need to "*hit a certain specific word*" to **pass** the exams or whatever.
>
> But life is **not** about passing exams. Instead, I think that **learning** and **constant learning** is more important than simple regurgitation.
>
> Therefore, even right now my brain is telling... "*Yo mate, you need to write everything down*"... I am going to let go!
>
> > At the end of the day, we only have **one life**!
>

## Type Annotation / Hinting

You are going to see me **not** using any *type hinting* the the code blocks below ( *and above* ). This is because of the nature of **tuples**!

Given that the **elements** of tuples are *locked* ( *in a way* ); therefore, when we use type hinting with tuples, we **need** to specify *each* elements's data type!

> [!NOTE]
> Given that I use Neovim ( *BTW* ) and uses things like *Pyright*, *Ruff* and *Black* for Language Servers, formatters and type linting...
>
> I get a lot of **warning** even if the code will work fine. This is because of the **code convention** that we *need* to follow and different languages all have their very own code convention that needs to be followed!

Here is a little example of why I did **not** write any *type hinting* for tuples!

![[Python - Tuples ( Incorrect Type Hinting ).png]]

The correct way to do this is by doing something like this:

```python
# type hinting: method 1
int_tuple_1: tuple[int, int, int, int, int] = (1, 2, 3, 4, 5)

# type hinting: method 2
int_tuple_2: tuple[int, ...] = tuple(num for num in range(100))
```

The **first method** can be use when there are *little* amount of elements inside the tuple while the **second method** when there are a *lot* of elements inside the tuple!

> [!TIP] Tuple Comprehension
> Yes, we can still use '**Tuple Comprehension**' to *initialise* our tuple!

> [!WARNING]
> If we did not **prefix** the `(num for num in range(100))` with `tuple`... We would have created a **generator** and <span stlye="color: red;"> not</span> a **tuple**.
>
> ```python
> # generator data type example
> print(type(num for num in range(100)))
> ```
>
> The output should be:
>
> ```console
> <class 'generator'>
> None
> ```
>
> Therefore we need to **prefix** `tuple` when running this type of *code*.
>
> > BTW this is good, as the `print()` function is trying to also **output** the *type* of the `range()` function!
>

One more thing, for *general tuples* like `general_tuple`. We could simply to do:

```python
# tuple containing most data types
general_tuple: tuple = (
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
)
```

> [!NOTE]
> Now you might be asking as of why I did **not** write any of the type hinting as its pretty simple and easy to do.
>
> > This is because I am a lazy mofo!
>

---

# Displaying - Accessing Tuples

## Length of Tuples

The code block below shows how the `len()` function can be used to calculate the length of both 1D-tuples and 2D-tuples.

```python
# create a tuple of integers ==> has 5 items
int_tuple = (1, 2, 3, 4, 5)
# create a tuple of boolean values ==> has 3 items
bool_tuple = (True, False, True)
# create a tuple of strings ==> has 4 items
str_tuple = ("Aryton Senna", "", "Lewis Hamilton", "Sebastien Vettel")

# tuple of tuple of integers
int_tuples = ((1, 2, 3, 4), (5, 6), (7, 8, 9))


# output the size of each tuple
print("\n<< Size of 1D-Tuple > > \n")

print(f"Size of Integer Tuple = {len(int_tuple)}")
print(f"Size of Boolean Tuple = {len(bool_tuple)}")
print(f"Size of String Tuple = {len(str_tuple)}")
print(f"Size of Integer Tuple of Tuples = {len(int_tuples)}")

print("\n<< Size of 2D-Tuple > > \n")

# iterate through the tuple of tuple of integers
for index, row in enumerate(int_tuples):
    # output the length of each inner tuple
    print(f"Length Of Tuple At Index {index}: {len(row)}")
```

In this case, we are going to get the output of:

```console

<< Size of 1D-Tuple > >

Size of Integer Tuple = 5
Size of Boolean Tuple = 3
Size of String Tuple = 4
Size of Integer Tuple of Tuples = 3

<< Size of 2D-Tuple > >

Length Of Tuple At Index 0: 4
Length Of Tuple At Index 1: 2
Length Of Tuple At Index 2: 3
```

## Displaying Tuples and Tuples Value(s)

As we know that **tuples** functions in pretty much the same way in terms of **lists** for things like *displaying* elements, *accessing* elements... I am literally going to **copy** the code from '[[Python - Lists#Displaying List and List Value(s) |Python - Lists ]]' and '[[Python - Two Dimensional Lists#Displaying 2D-Lists and List Value(s) | Python - Two Dimensional Lists]]'

```python
# tuple of integer numbers
int_tuple = (1, 2, 3, 4, 5)

print("\nPythonic Version\n")

# the pythonic way of displaying tuple
# "unpack" the values
print(*int_tuple)

print("\n'Normal' Version\n")

# "normal" way to display values of tuple
# interate through the tuple
for num in int_tuple:
    # output the value at each index
    print(num)

print("\n'C' Version\n")

# doing it like in 'C'
# interate through the length of tuple
for i in range(len(int_tuple)):
    # output the index and its corresponding value
    print(f"Index = {i} | Value: {int_tuple[i]}")

print("\n'C' - Python Version\n")

# doing the same thing above but using 'enumerate' function
for index, num in enumerate(int_tuple):
    # output the index and its corresponding value
    print(f"Index = {index} | Value: {num}")

# tuple of tuples of integer numbers
int_tuples = ((1, 2, 3), (4, 5, 6), (7, 8, 9))

print("\nPythonic Version\n")

# using the pythonic way to display each tuple "element"
# unpack the tuples ( inside the main tuple )
print(*int_tuples)

print("\nDisplaying Rows Only\n")

# without using 'range()' function
# iterate through the rows in the tuple
for row_tuple in int_tuples:
    # output each row of the tuple
    print(row_tuple)

print()

# using the 'range()' function
# iterate through the rows in the tuple
for i in range(len(int_tuples)):
    # output each row of the tuple
    print(int_tuples[i])

print("\nDisplaying Individual Elements\n")

# without using 'range()' function
# iterate through the rows in the tuple
for rows in int_tuples:
    # iterate through the columns in the tuple
    for cols in rows:
        # output each element of ( each inner ) tuple
        print(cols)

print()

# using the 'range()' function
# iterate through the rows in the tuple
for i in range(len(int_tuples)):
    # iterate through the columns in the inner tuple
    for j in range(len(int_tuples[i])):
        # output each element of ( each inner ) tuple
        print(int_tuples[i][j])
```

This massive ( *that's what she said ( again )* ) code is represented below:

```console

Pythonic Version

1 2 3 4 5

'Normal' Version

1
2
3
4
5

'C' Version

Index = 0 | Value: 1
Index = 1 | Value: 2
Index = 2 | Value: 3
Index = 3 | Value: 4
Index = 4 | Value: 5

'C' - Python Version

Index = 0 | Value: 1
Index = 1 | Value: 2
Index = 2 | Value: 3
Index = 3 | Value: 4
Index = 4 | Value: 5

Pythonic Version

(1, 2, 3) (4, 5, 6) (7, 8, 9)

Displaying Rows Only

(1, 2, 3)
(4, 5, 6)
(7, 8, 9)

(1, 2, 3)
(4, 5, 6)
(7, 8, 9)

Displaying Individual Elements

1
2
3
4
5
6
7
8
9

1
2
3
4
5
6
7
8
9
```

## Accessing Tuples Value(s)

Given that we, *in practice*, never going to change the **elements** found in tuple. This means that we can use something like the code below to **get** / **access** the individual elements.

```python
# "normal" way to display values of tuples
# interate through the tuple
for num in int_list:
	# output the value at each index
	print(num)
```

Therefore, we can do some computation with the numbers like so:

```python
# our main function
def main():
    # empty integer list
    int_list: list[int] = []

    # output the integer list ( before insertion )
    print(f"Integer List ( Before Insertion ): {int_list}")

    # tuple of integer numbers
    int_tuple = (1, 2, 3, 4, 5)

    # iterate through the integer tuple
    for num in int_tuple:
        # calculate the square of each number and append to the list
        int_list.append(pow(num, 2))

    # output the integer list ( after insertion )
    print(f"Integer List ( After Insertion ): {int_list}")


# source the main function
if __name__ == "__main__":
    main()
```

We should see this as our output!

```console
Integer List ( Before Insertion ): []
Integer List ( After Insertion ): [1, 4, 9, 16, 25]
```

> [!NOTE]
> Again this is possible because we are **not** going to do any *sorting*, *insertion* or *removal* of **elements** from our tuple!

---

## Number of Methods for Tuples

If we take a look '[[Python - Lists#Before We Start - Help! | Python - Lists]]'; I told you that there is something call the `dir()` function whereby it will tell us what *functions* / *methods* are available for a specific thing / *data type*.

Therefore:

```python
# output all the function / methods of a list
print(dir(tuple))
```

> I have change the *output* format for easy **readability**!

```console
[
    "__add__",
    "__class__",
    "__class_getitem__",
    "__contains__",
    "__delattr__",
    "__dir__",
    "__doc__",
    "__eq__",
    "__format__",
    "__ge__",
    "__getattribute__",
    "__getitem__",
    "__getnewargs__",
    "__getstate__",
    "__gt__",
    "__hash__",
    "__init__",
    "__init_subclass__",
    "__iter__",
    "__le__",
    "__len__",
    "__lt__",
    "__mul__",
    "__ne__",
    "__new__",
    "__reduce__",
    "__reduce_ex__",
    "__repr__",
    "__rmul__",
    "__setattr__",
    "__sizeof__",
    "__str__",
    "__subclasshook__",
    "count",
    "index",
]
```

> [!INFO] Wait a Second!
> As you can see, for tuples there are **only** *2* methods ( *like actual methods* ).
>
> "*But what about `.insert()`, `.remove()` and all of the others*" You ask!
>
> [You Fucking Idiot](https://www.youtube.com/watch?v=lg0-GF6pAsg)
>
> We have just said that *tuples* **cannot** be changed!

# Unpacking of Tuples

Similar to '[[Python - Lists#Unpacking of Lists | Unpacking of Lists]]', we can *unpack* **tuples**!

```python
# general tuple containing some elements
general_tuple: tuple[int, ...] = tuple(num for num in range(10))

# unpack the elements found in the general list
a, *x, b = general_tuple

# output the values of variables 'a', 'x' and 'b'
print(f"\nValue of 'a': {a}")
print(f"Value of 'x': {x}")
print(f"Value of 'b': {b}")
```

We should have this as our output:

```console

Value of 'a': 0
Value of 'x': [1, 2, 3, 4, 5, 6, 7, 8]
Value of 'b': 9
```

> [!NOTE]
> As you can see the `type(x)` is going to be a **list**!
>
> ```console
> <class 'list'>
> ```
>
> Hence, when we actually use the unpacking *operator* ( `*` ) with **tuples**; it take all the values that its unpacking and place them into a **list**.
>
> If you really need to **use** *tuples*... You can simply convert it to a `tuple` and use **another** *variable* to hold the converted tuple.
>
> ```python
> # convert the list of 'x' to a tuple
> x_tuple = tuple(x)
>
> print(f"Value of 'x_tuple': {tuple(x_tuple)}")
>
> # display the type of 'x_tuple'
> print(f"\nType of 'x_tuple': {type(x_tuple)}")
> ```
>
> Therefore, we should not get this as output for `x`:
>
> ```console
> Value of 'x_tuple': (1, 2, 3, 4, 5, 6, 7, 8)
>
> Type of 'x_tuple': <class 'tuple'>
> ```

---

# Functions and Methods of Tuples

## Tuple Equality - Inequality

Again, similar to our 'List Equality - Inequality' over at '[[Python - Lists#List Equality - Inequality | Python Lists]]'. We can also do this with *tuples*!

> Stealing the code from list; tell me whose going to stop me!

```python
# import the 'randint' function from the random module
from random import randint

# integer tuple containing some elements
int_tuple: tuple[int, ...] = (1, 2, 3, 4, 5)
# character tuple containing some elements
char_tuple: tuple[str, ...] = tuple(chr(num) for num in range(65, 70))


# check if tuples are equal to each other

# << integer tuple > >
print(f"Integer Tuple Equal? {int_tuple == (randint(0, 9) for i in range(5))}")
print(f"Integer Tuple Equal? {int_tuple != (num for num in range(5, 0, -1))}")
print(f"Integer Tuple Equal? {int_tuple == (1, 2, 3, 4, 5)} <---\n")

print("-" * 50, "\n")

# << character tuple > >
print(f"Character Tuple Equal? {char_tuple == (randint(0, 9) for i in range(5))}")
print(f"Character Tuple Equal? {char_tuple != (chr(num) for num in range(69, 64, -1))}")
print(
    f"Character Tuple Equal? {char_tuple == tuple(chr(num) for num in range(65, 70))} <---"
)
```

Therefore, we should get the **same** output:

```console
Integer Tuple Equal? False
Integer Tuple Equal? True
Integer Tuple Equal? True <---

-------------------------------------------------- 

Character Tuple Equal? False
Character Tuple Equal? True
Character Tuple Equal? True <---
```

> Again, we need to **convert** that _random number **generator**_ to our **tuple** with `tuple()`

## Count Method

Well, you know how the `.count()` method work... If **not** just refer to our note / file '[[Python - Lists#Count Method | Python - Lists]]' for more information.

```python
# our main function
def main():
    # tuple of characters containing some elements
    char_tuple: tuple = ("A", "A", "H", "A", "A", "B", "C")

    # variable to keep track of starting number
    char_ascii = 61

    print()

    # iterate over 13 times ( letters of english alphabet )
    for char in range(13):
        # count the number occurence of a character
        print(
            f"Character '{chr(char_ascii)}' Count: {char_tuple.count(chr(char_ascii))}"
        )

        # increment the tracker for ascii character
        char_ascii += 1


# source the main function
if __name__ == "__main__":
    main()
```

Therefore, our output should be like this:

```console

Character '=' Count: 0
Character '> ' Count: 0
Character '?' Count: 0
Character '@' Count: 0
Character 'A' Count: 4
Character 'B' Count: 1
Character 'C' Count: 1
Character 'D' Count: 0
Character 'E' Count: 0
Character 'F' Count: 0
Character 'G' Count: 0
Character 'H' Count: 1
Character 'I' Count: 0
```

## Index Method

Similarly, if you don't know anything about this method, just refer back to '[[Python - Lists#Index Method | Python - Lists]]' man!

```python
# our main function
def main():
    # tuple of characters containing some elements
    char_tuple: tuple = (
        "B",
        "D",
        "C",
        "F",
        "A",
    )

    # variable to keep track of starting number
    char_ascii = 63

    print()

    # iterate over 26 times ( letters of english alphabet )
    for char in range(13):
        # exception handling
        try:
            # count the number occurence of a character
            print(
                f"Character '{chr(char_ascii)}' Count: {char_tuple.index(chr(char_ascii))}"
            )

            # increment the tracker for ascii character
            char_ascii += 1

        # if the element has not been found in tuple
        except ValueError:
            # output appropriate message
            print(f"\n<< Character '{chr(char_ascii)}' Has NOT Been Found!!! > > \n")

            # do increment the tracker for the ascii character
            char_ascii += 1


# source the main function
if __name__ == "__main__":
    main()
```

We should have something like this:

```console


<< Character '?' Has NOT Been Found!!! > >


<< Character '@' Has NOT Been Found!!! > >

Character 'A' Count: 4
Character 'B' Count: 0
Character 'C' Count: 2
Character 'D' Count: 1

<< Character 'E' Has NOT Been Found!!! > >

Character 'F' Count: 3

<< Character 'G' Has NOT Been Found!!! > >


<< Character 'H' Has NOT Been Found!!! > >


<< Character 'I' Has NOT Been Found!!! > >


<< Character 'J' Has NOT Been Found!!! > >


<< Character 'K' Has NOT Been Found!!! > >

```

## Insertion and Removal?!?

> [Sike ┌П┐ !!!](https://www.youtube.com/watch?v=GPXkjtpGCFI&t=6s)

Yes, we **cannot** *insert*, *remove*, *sort* or *split* ( *and more* ) elements from a **tuple** as they are fixed... [Or can we](https://www.youtube.com/watch?v=JwYzHW_q3c4&t=7s)?

> [!INFO]
> Like we have seen... There are only 2 "*real*" **methods** associated with **tuples**!
>
> But what is in a pinch, we need to **insert** an element or **split** the tuple?
>
> > [!SUCCESS] Shitty, Unrecommended Fix!
> > Just Convert It To A `list`!!!
>
> By converting to a list, we will be able to use **all** the *functions* and *methods* associated with a `list`!

---

> [!WARNING]
> Even though that converting tuples into list is **not** recommended... That does not mean that you **cannot** do it.
>
> But by "*definition*", you should re-think your whole entire program and life you are using tuples and trying to **add** or **remove** elements from them.
>
> But then again, just remember that you *could* do it and then have access to all the *goodies* that **lists** provides us!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!