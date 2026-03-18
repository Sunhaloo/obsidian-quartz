---
id: Python - Dictionaries
aliases: Dictionaries in Python
tags:
  - data-structures
  - dictionaries
  - python
author: S.Sunhaloo
date: 2025-04-25
status: Completed
---

## List of Contents

- [[#What are Dictionaries?]]
- [[#Creation of Dictionaries]]
	- [[#Converting to Dictionaries]]
- [[#Displaying - Accessing Dictionaries]]
- [[#Unpacking of Dictionaries]]
- [[#Function and Methods of Dictionaries]]
	- [[#But Before We Start... The `zip` Function | The zip Function]]
	- [[#Insertion of Data]]
		- [[#Direct Assignment]]
		- [[#Update Method]]
		- [[#Keyword Arguments]]
		- [[#Set Default Method]]
	- [[#Removal of Data]]
		- [[#Clear Method]]
		- [[#Pop Method]]
		- [[#Pop Item Method]]
	- [[#Miscellaneous Methods / Functions]]
		- [[#Copy Method]]
		- [[#Get Method]]

---

# What are Dictionaries?

> [!TIP] Definition of Dictionaries
> It is a *data structure* ( *obviously* ) that stores *elements* in `key: value` pairs.
>
> - Duplication of Items:
> 	- `key` <strong> <span style="color: red;"> cannot</span> </strong> be duplicated; meaning **unique**
> 		- They should also be **immutable**
> 	- `value` **can** be duplicated
> - *In Python*, dictionaries are **ordered**
> - Uses [Hashing](https://en.wikipedia.org/wiki/Hash_function) to allow efficient *insert*, *remove* and *search* operations
>
> > [!INFO] The Analogy
> > Think of Dictionaries like actual phyiscal "*dictionaries*". Whereby we can consider the actual '*word*' that we are searching for as the `key` and the **meaning** of that '*word*' would be the `value`.
>
> > Now, kids these days have never held a dictionary in their lives!
>

> [!WARNING] Warnings, Warnings, Warnings!
>
> > [!WARNING] Key Values
> > The *value* of the `key` should be **hashable**!
> >
> > Meaning that we **cannot** have things like:
> >
> > - Lists
> > - Sets
> > - Tuple **with** *non-hashable* data types
> >
> > > Nevertheless, `value` can be of **non-hashable** *data types*!
> >
> > > BTW, its basically the **same** stuff that we saw when creating [[Python - Sets#Creation of Sets | sets]]!
> >
>
> > [!WARNING] Again, [[Python - Sets#Accessing Sets Value(s) | Sets]] $\neq$ Dictionaries!
> > As you can see above, we still use the `{}` for creating list.
> >
> > Like we have said; to create an **empty** *set* we need to use `set()` but if you do something like `set_name: set = {}`. You *Language Server* will start screaming at you as you just created a **dictionary**!
> >
> > > "*I use VIM BTW*!"
> >
>

> [!NOTE] One More Thing!
> Similar to [[Python - Sets | Sets]], I have **never** used Python's Dictionaries.
>
> Hence, *me and you*, are going to learn this right here and right now!

---

# Creation of Dictionaries

To create a dictionary in Python, we use the `{}` characters!

```python
# dictionary containing hashable data types
general_dict: dict = {
    1: 1,
    2: "something",
    "some_nums": [69.69, 55, 27],
    "set": {1, 2, 3, "A", "B", "C"},
    "a_dict": {1: "one", 2: "two", 3: "three"},
    ("Mazda", "BMW", "Porsche", "Lancia", "Lotus"): ["Car", "Brands"],
}
```

> [!NOTE] Bad, Bad Dictionary
> An example of a bad dick... *I mean 'dict'* would be:
>
> ```python
> # dictionary containing non-hashable "key" data types
> bad_dict = {
>    [1, 2, True, None]: "not nice",
>    ([1, 2, 3, 4], {1, 2, 3}): "doing what?",
>    {"Something", "in my", "ass"}: "uuuhuuhmmmm",
> }
> ```
>
> The above code should return a '*TypeError*'!
>
> ```console
> Traceback (most recent call last):
>  File "/home/username/Desktop/dicts.py", line 2, in module
>    bad_dict = {
>               ^
>    ...<3 lines> ...
>    }
>    ^
> TypeError: unhashable type: 'list'
> ```
>
> > [!NOTE] Additionally
> > You **cannot** do something like this:
> >
> > ```python
> > some_dict: dict = {1: 1, 2: }
> > ```
> >
> > This is going to return a '*SyntaxErrorr*'!
> >
> > ```console
> > File "/home/username/Desktop/dicts.py", line 1
> >   some_dict: dict = {1: 1, 2: }
> >                              ^
> > SyntaxError: expression expected after dictionary key and ':'
> > ```

> [!INFO] `type()` of Dictionaries
> If we  run `print(type(general_set))` we should see that we get:
>
> ```console
> <class 'dict'>
> ```
>
> Nevertheless, the word '*dict*' is **not** a reserved word in Python and you can create a dictionary called `dict` like so:
>
> ```python
> dict = {1: "one", 2: "two", 3: "three"}
> ```
>
> > Nevertheless, this is **not** recommended!
>

> [!WARNING]
> 1. We **cannot** have the same *keys*
> 	- Similar to [[Database Systems - Keys#Primary Keys | Primary Keys]]
> 	- We can only have <span style="color: green;"> one</span> unique key inside our dictionary
> 2. We **can** have the same *values*
> 	- The above limitation does not apply to values as we can have **different** "*sub-things*" with **same** "*parent-things*"
> 	- For example:
> 		- `cars: dict[str, str] = {"Audi": "Volkswagen", "Bugatti": "Volkswagen"}`
> 		- `family: dict[str, str] = {"parent_father": "son_1", "parent_mother": "son_1"}`

## Converting to Dictionaries

As you know we can simply use things like `list()`, `tuple()` and `set()` to **convert** from *data type* to the above mentioned data types.

> Just a simple example

```python
# string variable and initialised with 'Hello World'
greetings: str = "Hello World"

# start to convert to list, tuple and set
print(f"String Converted to List: {list(greetings)}")
print(f"String Converted to Tuple: {tuple(greetings)}")
print(f"String Converted to Set: {set(greetings)}")
```

Running the above code block, we get:

```console
String Converted to List: ['H', 'e', 'l', 'l', 'o', ' ', 'W', 'o', 'r', 'l', 'd']
String Converted to Tuple: ('H', 'e', 'l', 'l', 'o', ' ', 'W', 'o', 'r', 'l', 'd')
String Converted to Set: {'l', 'r', ' ', 'd', 'e', 'W', 'H', 'o'}
```

### What About `dict()`?

As dictionaries are formed using `key:value` pairs. Hence, we <strong> <span style="color: red;"> cannot</span> </strong> convert something like `int_nums = [1, 2, 3, 4]` this to a *dictionary* simply by using `dict()`.

```console
> > > greeting: str = "Hello World"
> > > int_list: list[int] = [1, 2, 3, 4, 5]
> > > 
> > > print(dict(greeting))
Traceback (most recent call last):
  File "<python-input-5> ", line 1, in <module>
    print(dict(greeting))
          ~~~~^^^^^^^^^^
ValueError: dictionary update sequence element #0 has length 1; 2 is required
> > > 
> > > 
> > > print(dict(int_list))
Traceback (most recent call last):
  File "<python-input-8> ", line 1, in <module>
    print(dict(int_list))
          ~~~~^^^^^^^^^^
TypeError: cannot convert dictionary update sequence element #0 to a sequence
> > > 
```

> As you can see... it does **not** work!

### Therefore!

To be able to convert things like *list*, *sets* or *tuples* into **dictionaries**, there is a format that needs to be followed.

```python
# structure should be like so:

# list of list of 2 elements
list_of_list: list[list] = [["one", 1], ["two", 2], ["three", 3], ["four", 4]]

# list of tuple of 2 elements
list_of_tuple: list[tuple[str, int]] = [
	("one", 1),
	("two", 2),
	("three", 3),
	("four", 4),
]
# list of set of 2 elements
list_of_set: list[set] = [{"one", 1}, {"two", 2}, {"three", 3}, {"four", 4}]

# tuple of list of 2 elements
tuple_of_list: tuple[list, ...] = (
	["one", 1],
	["two", 2],
	["three", 3],
	["four", 4],
)
# tuple of tuple of 2 elements
tuple_of_tuple: tuple[tuple[str, int], ...] = (
	("one", 1),
	("two", 2),
	("three", 3),
	("four", 4),
)
# tuple of set of 2 elements
tuple_of_set: tuple[set, ...] = ({"one", 1}, {"two", 2}, {"three", 3}, {"four", 4})

# set of tuple of 2 elements
set_of_tuple: set[tuple[str, int]] = {
	("one", 1),
	("two", 2),
	("three", 3),
	("four", 4),
}
```

> Refer to '[[Python - Sets#Creation of Sets | Creation of Sets]]' for as to why we **cannot** have '*sets of lists*' and '*sets of dictionaries*'.
>
> TLDR: its because they are **un-hashable**!

#### Hence, Converting to Dictionaries

Converting the above $\uparrow$ code block gives us:

```python
# display the list of 'x'
print(dict(list_of_list))
print(dict(list_of_tuple))
print(dict(list_of_set))

print()
print()

# display the tuple of 'x'
print(dict(tuple_of_list))
print(dict(tuple_of_tuple))
print(dict(tuple_of_set))

print()
print()

# display the set of 'tuple'
# of hashable data type
print(dict(set_of_tuple))
```

We should get something that looks like this:

```console
{'one': 1, 'two': 2, 'three': 3, 'four': 4}
{'one': 1, 'two': 2, 'three': 3, 'four': 4}
{'one': 1, 2: 'two', 'three': 3, 'four': 4}


{'one': 1, 'two': 2, 'three': 3, 'four': 4}
{'one': 1, 'two': 2, 'three': 3, 'four': 4}
{'one': 1, 2: 'two', 'three': 3, 'four': 4}


{'three': 3, 'one': 1, 'two': 2, 'four': 4}
```

> [!INFO] You would not really make a **Set** become a **Dictionary**!
> This is due to the fact that *Sets* are **unordered**.
>
> For example, doing `print(dict(list_of_set))` **will** give you different *key* and *value* pair / combination!
>
> ```console
> # sometimes you can get this:
> {1: 'one', 'two': 2, 'three': 3, 4: 'four'}
>
> # or sometimes we get this:
> {'one': 1, 2: 'two', 3: 'three', 'four': 4}
> ```
>
> The above **dictionary** has a completely different meaning from $\downarrow$:
>
> ```console
> # this is what we wanted originally
> {'one': 1, 'two': 2, 'three': 3, 'four': 4}
> ```

---

# Displaying - Accessing Dictionaries

## Length of Dictionaries

> [!NOTE] From My Understanding
> Logically speaking, the number of `key` should be **equal to** the number of `value`. Therefore, the *length* of the dictionary should be the **amount** of `key: value` pairs.

```python
# dictionary containing hashable data types
general_dict: dict = {
    1: 1,
    2: "something",
    "some_nums": [69.69, 55, 27],
    "sets": {1, 2, 3, "A", "B", "C"},
    "a_dict": {1: "one", 2: "two", 3: "three"},
    ("Mazda", "BMW", "Porsche", "Lancia", "Lotus"): ["Car", "Brands"],
}

# dictionary of numbers-string ( key-value )
int_str_dict: dict[int, str] = {1: "one", 2: "two", 3: "three"}

# output the size of each dictionary
print("\n<< Size of Dictonaries > > ")

print(f"Size of General Dictionary: {len(general_dict)}")
print(f"Size of Integer-String Dictionary: {len(int_str_dict)}")
```

Therefore, we should get an output that looks like this:

```console
<< Size of Dictonaries > >

Size of General Dictionary: 6
Size of Integer-String Dictionary: 3
```

> [!SUCCESS]- [Nice Job Team](https://www.youtube.com/shorts/9gBNhMvsfNg)
> My understanding was correct! 

## Displaying Dictionaries ( Key - Value )

### Displaying Whole Dictionary

To display the **whole** dictionary *all at once*, we can use the simply and mighty `print()` function.

```python
# dictionary of numbers-string ( key-value )
int_str_dict: dict[int, str] = {1: "one", 2: "two", 3: "three"}

# display the entire dictionary
print(int_str_dict)
```

Therefore, we should have our humble output:

```console
{1: 'one', 2: 'two', 3: 'three'}
```

### Displaying All Values of Dictionary

#### The `.values()` Method / Function

To only display the **values** part of the '*key-value*' pairs, we need to use the `.values()` method.

```python
# dictionary of numbers-string ( key-value )
int_str_dict: dict[int, str] = {1: "one", 2: "two", 3: "three"}

# display all the values of the dictionary
print(int_str_dict.values())
```

We should get a *list* of containing all the values inside our dictionary like so:

```console
dict_values(['one', 'two', 'three'])
```

> "*Wait, WTF! This is not a really a list of values*"?

#### What is `dict_values()`?

The `dict_values([])` is called a '**Dictionary View Object**' and its supposed to be better than just a *simple* list!

Because lists are **static** and *inefficient*; as from Python 3 and later versions, they decided to use these *dictionary view objects*!

To be honest, I am **not** going to into details right now, because I currently don't know how Hash Tables / Hash Mapping works. Therefore, here is the simpler, analogical version of it.

Think of these '**Dictionary View Objects**' as [[SQL Commands - Data Control Language ( DCL ) - Views and Privileges#Create Views | database views]]. I am saying this due to its similarity in behaviour.

As you know, when we create a view in *database terms*; its going to create a **child** table. And as you already know, the parent table does still have *control* over the child table.

Hence, any changes made to the **parent table** is going to be *reflected* inside / on the **child** table.

> If your parents lie a lot to people; you are also going to start lying to people... "*Am I not right*"?

Additionally, it makes complete and utter sense to forgo *lists* as *dictionaries* uses **hash tables** / **mappings** for its internal working. Therefore, why not use something that is miles better and efficient that "*simple*" lists!

> [!INFO] If you need more information
> Please go and read the top comment / answer!
>
> Link to StackOverflow question and answer: https://stackoverflow.com/questions/47273297/python-understanding-dictionary-view-objects
>
> Additionally, here is the official Python documentation for 'Dictionary View Objects': https://docs.python.org/3/library/stdtypes.html#dict-views

> [!TIP] `type()` of `dict_values([])`
> The data type is going to be of $\downarrow$:
>
> ```console
> <class 'dict_values'>
> ```

### Displaying All Keys of Dictionary

Similarly, we have a method / function called `.keys()`. This function will allow us display all the **keys** found inside our dictionary

```python
# dictionary of numbers-string ( key-value )
int_str_dict: dict[int, str] = {1: "one", 2: "two", 3: "three"}

# display all the keys of the dictionary
print(int_str_dict.keys())
```

In this case, we should get an output that look something like this:

```console
dict_keys([1, 2, 3])
```

> [!TIP] `type()` of `dict_keys([])`
> The data type is going to be of $\downarrow$:
>
> ```console
> <class 'dict_keys'>
> ```

> [!NOTE] `for` Loops with `dict_name`
> By default if we try to do something like this ( *similar to a [[Python - Lists#Displaying List and List Value(s) | list]]* ) $\downarrow$:
>
> ```python
> # dictionary of numbers-string ( key-value )
> int_str_dict: dict[int, str] = {1: "one", 2: "two", 3: "three"}
>
> # display all the keys of the dictionary
> for index, key in enumerate(int_str_dict, start=1):
>    print(f"Index: {index} --> Key: {key}")
> ```
>
> This, by *default* will automatically fetch the **keys** of the dictionary!
>
> - In this case, the output is going to be like so:
>
> ```console
> Index: 1 --> Key: 1
> Index: 2 --> Key: 2
> Index: 3 --> Key: 3
> ```

### Displaying All Key-Value Item of Dictionary

> To be honest, I **don't** know how to explain this...

If you want to display a [[Python - Tuples|tuple]] of '*key-value*' pairs, then we just need to use the `.items()` method / function!

```python
# dictionary of numbers-string ( key-value )
int_str_dict: dict[int, str] = {1: "one", 2: "two", 3: "three"}

# display all the 'key-value' pairs of the dictionary
print(int_str_dict.items())
```

Like I have said, we should get a list containing tuples of 2 elements:

```console
dict_items([(1, 'one'), (2, 'two'), (3, 'three')])
```

> [!TIP] `type()` of `dict_items([])`
> The data type is going to be of $\downarrow$:
>
> ```console
> <class 'dict_items'>
> ```

#### They Are Really Useful!!!

Yes, the method / function `.items()` is really useful for **displaying**; as it returns a '*tuple of 2 elements*' whereby the *first* element is the **key** and the *second* element is the **value** associated to that key.

This means that we can use it to iterate through a **dictionary** with a `for` loop!

> Like so! $\downarrow$

> [!INFO] More Code Block!
> I was going to just write a simple fucking `for` loop that will just do the job!
>
> But because I am a, what I like to call, "*complicated piece of fucking shit*"... I decided to also try to use the `enumerate()` function with the `for` loop... *Just because I fucking can*!
>
> Nevertheless, I did find something interesting... Its about **unpacking** values with `for` loops!
>
> > Take a look at this!
>

1. Simple `for` Loop to display **key** and **value**

```python
# dictionary of containing the student IDs
student_id_dict: dict[str, str] = {
    "student_1": "ID001",
    "student_2": "ID002",
    "student_3": "ID003",
    "student_4": "ID004",
}

# display the each student with corresponding ID
for student, id in student_id_dict.items():
    print(f"Student: {student} --> ID: {id}")
```

- Output for the above code block:

```console
Student: student_1 --> ID: ID001
Student: student_2 --> ID: ID002
Student: student_3 --> ID: ID003
Student: student_4 --> ID: ID004
```

> Very nice and simple; I think this is what is mostly used to be honest!

##### Now, Enumeration!

Study the code below $\downarrow$:

```python
# dictionary of containing the student IDs
student_id_dict: dict[str, str] = {
    "student_1": "ID001",
    "student_2": "ID002",
    "student_3": "ID003",
    "student_4": "ID004",
}

# display "index", student name and corresponding ID
for index, student, id in enumerate(student_id_dict.items()):
    # format the output like so
    print(f"Index: {index} ==> Student: {student} --> ID: {id}")
```

We would initially think that the output would be in this *format*:

```console
Index: 0 ==> Student: student_1 --> ID: ID001
Index: 1 ==> Student: student_2 --> ID: ID002
Index: 2 ==> Student: student_3 --> ID: ID003
Index: 3 ==> Student: student_4 --> ID: ID004
```

> **Wrong**!!!

In this case, we are going to get an <span style="color: red;"> error</span> like this:

```console
Traceback (most recent call last):
  File "/home/username/Desktop/dicts.py", line 11, in <module>
    for index, student, id in enumerate(student_id_dict.items()):
        ^^^^^^^^^^^^^^^^^^
ValueError: not enough values to unpack (expected 3, got 2)
```

> [!WARNING] The Reason
> We all know that `dict_name.items()` will return a '**tuple of 2 elements**'. This means that we are going to get something like this in return: `(key, value)`!
>
> But what actually happening when we do `enumerate(dict_name.items())`?
>
> Instead of getting something like this $\downarrow$, whereby each "*value*" is correctly mapped onto each variable.
>
> ```python
> # working with the above example
> # taking iteration '0' as example here
> index = 0
> student = "student_1"
> id = "ID001"
> ```
>
> We are actually getting something like this!
>
> ```console
> # again, taking iteration '0' as example
> (0, ("student_1", "ID001"))
> ```

###### Therefore!!!

We are going to have to **mimic** the output `enumerate(student_id_dict.items())`!

```python
# dictionary of containing the student IDs
student_id_dict: dict[str, str] = {
    "student_1": "ID001",
    "student_2": "ID002",
    "student_3": "ID003",
    "student_4": "ID004",
}

# display "index", student name and corresponding ID
# see how we unpaking the inner tuple
# that contains the 'key' and the 'value'
for index, (student, id) in enumerate(student_id_dict.items()):
    # format the output like so
    print(f"Index: {index} ==> Student: {student} --> ID: {id}")
```

Here, we should correctly get the output:

```console
Index: 0 ==> Student: student_1 --> ID: ID001
Index: 1 ==> Student: student_2 --> ID: ID002
Index: 2 ==> Student: student_3 --> ID: ID003
Index: 3 ==> Student: student_4 --> ID: ID004
```

# Unpacking of Dictionaries

Now, we are *unpacking* **Dictionaries** and not **list**!

This means that its **not** going to be as simple as this $\downarrow$:

```python
# integer list containinig 2 elements
int_list: list[int] = [1, 2]

# take the first 3 elements ( NOT possible )
x, y, z = int_list
```

There are several ways of *unpacking* a dictionary, and all of the ways has some relation with what we learned in the section '[[#Displaying Dictionaries ( Key - Value )]]'!

> Let's get started!

## Unpacking Keys of Dictionaries

The code below will show you how to only unpack the **keys** from a dictionary:

```python
# dictionary of numbers-string ( key-value )
int_str_dict: dict[int, str] = {1: "one", 2: "two", 3: "three", 4: "four", 5: "five"}

# unpack the keys of the dictionary
a, *x, b = int_str_dict

# display the values of 'a', '*x' and 'b'
print(f"\nValue of 'a': {a}")
print(f"Value of 'x': {x}")
print(f"Value of 'b': {b}")
```

This will output all the keys from the dictionary like so $\downarrow$:

```console
Value of 'a': 1
Value of 'x': [2, 3, 4]
Value of 'b': 5
```

> [!INFO]
> Again, as you *already* know, doing something like `*x` will return a **list of elements**!
>
> In this case, it returns a *list of integer* numbers whereby each of the elements inside of *that list* is the **key** part of a 'key-value' pair of the dictionary `int_str_dict`.

## Unpacking Values of Dictionaries

Similarly, we could instead *unpack* the actual **values** of each 'key-value' pair, simply by using the method / function `.values()`!

```python
# dictionary of numbers-string ( key-value )
int_str_dict: dict[int, str] = {1: "one", 2: "two", 3: "three", 4: "four", 5: "five"}

# unpack the values of the dictionary
a, *x, b = int_str_dict.values()

# display the values of 'a', '*x' and 'b'
print(f"\nValue of 'a': {a}")
print(f"Value of 'x': {x}")
print(f"Value of 'b': {b}")
```

Well, instead of seeing the *keys* in the output, we should see the **values**:

```console
Value of 'a': one
Value of 'x': ['two', 'three', 'four']
Value of 'b': five
```

## Unpacking Key-Value Item of Dictionaries

> Again, the shit that I have trouble explaining

Well, we should receive **tuples** in our outputs, right?

```python
# dictionary of numbers-string ( key-value )
int_str_dict: dict[int, str] = {1: "one", 2: "two", 3: "three", 4: "four", 5: "five"}

# unpack the 'key-value' items of the dictionary
a, *x, b = int_str_dict.items()

# display the values of 'a', '*x' and 'b'
print(f"\nValue of 'a': {a}")
print(f"Value of 'x': {x}")
print(f"Value of 'b': {b}")
```

This is what we got:

```console
Value of 'a': (1, 'one')
Value of 'x': [(2, 'two'), (3, 'three'), (4, 'four')]
Value of 'b': (5, 'five')
```

> And we do get **tuples** in our outputs!

---

# Functions and Methods of Dictionaries

We are now going to learn about the different *functions* and *methods* that are associated with **dictionaries**.

> [!INFO]
> Similar to [[Python - Sets#Functions and Methods of Sets | Sets]], I am **not** going to be writing about every *functions* and / or *methods* that can be used with dictionaries
>
> Therefore, I suggest you take a look at the functions / method we covered over at '[[Python - Lists#Functions and Methods of Lists | Python - Lists]]'!

## But Before We Start... The `zip` Function

> Again and again and fucking again... There always something before we start!

As we have seen [[#Converting to Dictionaries | above]] $\uparrow$; we **cannot** directly traditional, vanilla *lists*, *tuples* or *sets* into **dictionaries**.

Therefore, if we have 2 **one-dimensional**, vanilla *list* ( _not talking about **lists of list** or others_ ), we can use the `zip()` function to **combine** them to make a dictionary!

### How does `zip()` Works?

Take a look at the code found below $\downarrow$:

```python
# create a list of integer numbers
int_list: list[int] = [1, 2, 3]
# create a list of strings
str_list: list[str] = ["one", "two", "three", "one more"]

# "zipping" the 2 lists together
# INFO: we are going to create a list
# that contains the combined data items
combined_list: list[tuple[int, str]] = list(zip(int_list, str_list))

# display the combined list
print(f"\nThe Combined List is: {combined_list}")
```

The output for the above code is going to be:

```console
The Combined List is: [(1, 'one'), (2, 'two'), (3, 'three')]
```

As you can see, we create, *in this case*, a **list of tuples containing 2 elements**!

This means that this `combined_list` can be directly converted into a **dictionary**... Adding the following code to the above, we should get a dictionary of 3 *data items* whereby we have the *integer numbers* as **keys** and *string* "*words*" becomes the actual **values**!

```python
# add the following code to the above code
# convert the combined list into a dictionary
dictionary = dict(combined_list)

# display the newly created dictionary
print(f"\nDictionary From Combined List: {dictionary}")
```

In this case, the updated output is going to look like this:

```console
The Combined List is: [(1, 'one'), (2, 'two'), (3, 'three')]

Dictionary From Combined List: {1: 'one', 2: 'two', 3: 'three'}
```

> Very Nice!

### The Problem!

Did you notice the *lists* that we defined in the very first code snippet?

Did you notice how the **length** of `int_list` was '3' and `str_list` was '4'?

> If **not**, then you are not paying attention... *Go Fuck Youself*!

Now, there is a option called `strict` that we can pass inside the `zip()` function. And therefore, the `zip()` function will only create the "*combined*" list, if and only if, the *length* of the individual lists are the **same**.

> Modifying the same initial code snippet from above $\uparrow$:

```python
# just need to add the argument / parameter 'strict'
combined_list: list[tuple[int, str]] = list(zip(int_list, str_list, strict=True))
```

Now, when we run the code, we are going to get this a `ValueError`!

```console
Traceback (most recent call last):
  File "/home/username/Desktop/zip.py", line 9, in <module>
    combined_list: list[tuple[int, str]] = list(zip(int_list, str_list, strict=True))
                                           ~~~~^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
ValueError: zip() argument 2 is longer than argument 1
```

Again this happens because of the *difference* in **length** for the 2 lists!

> [!INFO] Correcting the Inconsistency...
> If we "*correct*" the length of the 2 lists, we should be able to get the "*correct*" output!
>
> > "*What is correct anyways in this fucked up world*!"
>
> This is a different code BTW... Instead of using *lists*, we are using **tuples**!
>
> ```python
> # create a tuple of integer numbers
> int_tuple: tuple[int, ...] = (1, 2, 3, 4)
> # create a tuple of strings
> str_tuple: tuple[str, ...] = ("one", "two", "three", "four")
>
> # "zipping" the 2 tuples together
> # INFO: we are going to create a tuple
> # that contains the combined data items
> combined_tuple: tuple[tuple[int, str], ...] = tuple(
> 	# the argument / parameter 'strict' is set to 'True'
>    zip(int_tuple, str_tuple, strict=True)
> )
>
> # display the combined tuple
> print(f"\nThe Combined Tuple is: {combined_tuple}")
>
> # convert the combined tuple into a dictionary
> dictionary = dict(combined_tuple)
>
> # display the newly created dictionary
> print(f"\nDictionary From Combined Tuple: {dictionary}")
> ```
>
> In this case, we **make sure** that our *dictionary* that we are creating is actually real... What I am trying to say its that if you have 2 *lists* and we are **creating** a *dictionary* from those 2... We should ensure that the *length* is **equal** or else it would seem as ifsome data might be *lost*.
>
> > I think you get what I am trying to say... Ahh Yes! The output:
>
> ```console
> The Combined Tuple is: ((1, 'one'), (2, 'two'), (3, 'three'), (4, 'four'))
>
> Dictionary From Combined Tuple: {1: 'one', 2: 'two', 3: 'three', 4: 'four'}
> ```

> [!BUG] Zip Objects
> If you do something like this:
>
> ```python
> # combined_data = zip(data_structure_x1, data_structure_x2)
> ```
>
> This is only going to create an '**object of zip**', using the example of `combined_list` and just **removing** the *type casting* with the `list()`, when we display that *combined list*... Instead of getting a '*list of tuples*' or *other*, we get this:
>
> ```console
> The Combined Zip-Object is: <zip object at 0x7c15ed899c00>
> ```
>
> Now, because of how `zip()` is classified as an **iterator**, Python consumes it ( *memory / garbage collection type of system* ). It <strong> <span style="color: red;"> cannot</span> </strong> be used again!
>
> Therefore, if we taking a look at the following code below $\downarrow$, we see that the *conversion to dictionary* is being done **directly**!
>
> ```python
> # create a list of integer numbers
> int_list: list[int] = [1, 2, 3]
> # create a list of strings
> str_list: list[str] = ["one", "two", "three", "one more"]
>
> # "zipping" the 2 lists together
> # INFO: in this case, we are going to a zip object
> combined_zip_obj: zip = zip(int_list, str_list)
>
> # display the combined zip object
> print(f"\nThe Combined Zip is: '{combined_zip_obj}'")
>
> # convert the combined zip object into a dictionary
> dictionary = dict(combined_zip_obj)
>
> # display the newly created dictionary
> print(f"\nDictionary From Combined Zip: {dictionary}")
> ```
>
> The output of the above $\uparrow$ code snippet is going to look like this $\downarrow$:
>
> ```console
> The Combined Zip is: '<zip object at 0x7e047848bbc0> '
>
> Dictionary From Combined List: {1: 'one', 2: 'two', 3: 'three'}
> ```
>
> If we were to convert `combined_zip_obj` into a *list* / *tuple* inside the `print()` statement... We are going to "**exhaust**" that `zip` and therefore, we are going to have <span style="color: orange;"> nothing</span> inside our **dictionary**!
>
> ```python
> # create a list of integer numbers
> int_list: list[int] = [1, 2, 3]
> # create a list of strings
> str_list: list[str] = ["one", "two", "three", "one more"]
>
> # "zipping" the 2 lists together
> # INFO: in this case, we are going to a zip object
> combined_zip_obj: zip = zip(int_list, str_list)
>
> # display the combined zip object
> print(f"\nThe Combined Zip Coverted to List is: {list(combined_zip_obj)}")
>
>
> # convert the combined zip object into a dictionary
> # INFO: because we have already performed and action / operation on 'combined_zip_obj'
> # i.e converting the zip object into a list inside the `print()`
> # the variable 'combined_zip_obj' inside the `dict()` function is actually empty
> dictionary = dict(combined_zip_obj)
>
> # display the newly created dictionary
print(f"\nDictionary From Combined Zip: {dictionary}")
> ```
>
> Therefore we are **not** going to get anything inside our dictionary!
>
> ```console
> The Combined Zip Coverted to List is: [(1, 'one'), (2, 'two'), (3, 'three')]
>
> Dictionary From Combined Zip: {}
> ```

> [!SUCCESS] In Short,
> The `zip()` function create a **tuple** of *2 elements*.
>
> Additionally, think of `zip()` and the "*exhaustion*" part like a database **view**!
>
> Whereby someone creates a **temporary** *view* for a user and as mentioned before, all the data from the *parent* table is translated into that view. Now, think of `zip()` function as a database view that has been created for a "**one-time-use**" only!
>
> This means that after we use it... The data inside the *child* table $\rightarrow$ In this case, the *zipped* data items gets **deleted**!
>
> > But we not understand how the `zip()` function works. Yippeee!

## Insertion of Data

There are several ways / *methods* that we can insert data into a **dictionary**; these are:

1. Direct Assignment
2. `dict_name.update()`
3. `dict_name.setdefault()`

### Direct Assignment

As you know, we <strong> <span style="color: red;"> cannot</span> </strong> do something like this:

```python
# empty list that will hold integer numbers
int_list: list[int] = []

# try to insert '5' into the list at index '0'
int_list[0] = 5
```

Here, we are going to get the error `IndexError`:

```console
Traceback (most recent call last):
  File "/home/username/Desktop/test.py", line 5, in <module>
    int_list[0] = [5]
    ~~~~~~~~^^^
IndexError: list assignment index out of range
```

Therefore this **only** works when there are *elements present* inside the **list**!

> Nevertheless, this can be used with **Dictionaries**!

```python
# empty dictionary that will contain numbers-string ( key-value )
int_str_dict: dict[int, str] = {}

# output the integer-string dictionary ( before insertion )
print(f"\nInteger-String Dictionary ( Before Insertion ): {int_str_dict}")

# use direct assignment to insert the 'key-value' pairs inside dictionary
int_str_dict[1] = "one"
int_str_dict[2] = "two"
int_str_dict[3] = "three"

# output the integer-string dictionary ( after insertion )
print(f"Integer-String Dictionary ( After Insertion ): {int_str_dict}")

# try to insert 'key-value' pair '1: one' again
int_str_dict[1] = "one"

# output the integer-string dictionary ( after insertion of '1: one' again )
print(f"\nInteger-String Dictionary ( Inserting '1: one' Again ): {int_str_dict}")

# try to insert 'key-value' pair '1: the one'
int_str_dict[1] = "the one"

# output the integer-string dictionary ( after insertion of '1: the one' )
print(f"\nInteger-String Dictionary ( Inserting '1: the one' ): {int_str_dict}")
```

The output of the above code is going to be $\downarrow$:

```console
Integer-String Dictionary ( Before Insertion ): {}
Integer-String Dictionary ( After Insertion ): {1: 'one', 2: 'two', 3: 'three'}

Integer-String Dictionary ( Inserting '1: one' Again ): {1: 'one', 2: 'two', 3: 'three'}

Integer-String Dictionary ( Inserting '1: the one' ): {1: 'the one', 2: 'two', 3: 'three'}
```

As you can see, the *dictionary* was initially **empty** and after using *direct assignment* to insert those 3 'key-value' pairs. We are going to see that we our *data* has been correctly entered

Therefore, we can see that the format for using **direct assignment** to insert data into our dictionary is going to be as follows:

> [!TIP] Direct Assignment Usage
> ```console
> dict_name[key] = value
> ```

> [!INFO] **Updating** 'Key-Value' Pairs!!!
> Try to do `int_str_dict[1] = "one"` again will result in... **No Change**!
>
> Because the *pair* was already present in the dictionary; no change occurs and the dictionary stays intact.
>
> But look at how when we do `int_str_dict[1] = "the one"`, We now see that the **value** for the **key** `1` has changed from `one` to `the one`!

#### Example Code: User Input - Direct Assignment

```python
# our main function
def main():
    # empty dictionary that will hold
    # each student name's marks in the form 'key-value'
    student_marks_dict: dict[str, float] = {}

    # exception handling
    try:
        # ask the user to enter the amount of students / marks to enter
        student_amount = int(
            input("\nPlease Enter Amount of Student's Marks to Input: ")
        )

        # iterate through the number of students provided
        for num_students in range(student_amount):
            # display the current student number
            print("\n" + "-" * 50, "\n")
            print(f"\t << Student Number #{num_students} > > \n")

            # ask the user to enter the student's name
            student_name = input("Please Enter Student Name: ").title()
            # ask the user to enter the mark for that student
            student_mark = float(input(f"Please Enter Marks for '{student_name}': "))

            # add that student-mark 'key-value' pair to the dictionary
            student_marks_dict[student_name] = student_mark

        # display the dictionary in a correct format
        print("\n" + "-" * 50, "\n")
        print("\t<< Student Marks Dictionary > > \n")

        # iterate through the tuples of 'key-value' pairs
        for student_names, student_marks in student_marks_dict.items():
            # display the student name and respective marks
            print(f"Student Name: {student_names} ==> Marks: {student_marks}")

    # if the user does not enter 'float' values
    except ValueError as e:
        # output the error in question
        print(f"\nError: {e}")

        # output appropriate message
        print("\n<< Please Enter Integer Numbers Only For Amount of Students!!! > > ")
        print("\n" + "-" * 66, "\n")
        print("<< Please Enter Decimal Numbers Only For Student Marks!!! > > \n")


# source the main function
if __name__ == "__main__":
    main()
```

### Update Method

The `.update()` method for **dictionaries** is like our '[[Python - Lists#Append Method | Append Method]]' for *lists*.

> [!NOTE] To Update or Not To Update?
> The first thing that comes to mind when you hear someone talk about *an* ( *in general* ) `update()` function.
>
> You know that its going to do some **modification**; in most cases, an **update** means to improve something or change *things* for the better.
>
> But here! The `.update()` method for **dictionaries** will also <strong> <span style="color: orange;"> insert</span> </strong> **new** data into the specified dictionary, in addition to **updating** the *values*.
>
> > [!WARNING] Updates the **Values** Only!!!
> > Yes, the `.update()` method can also modify **existing** data inside out dictionary but ( *yeess, butt 🍑* ) it can only **modify** the <span style="color: red;"> value</span> of the 'key-value' pair!
>
> > This is the reason as to why I placed the `.update()` method in the '*Insertion of Data*' category!
>

#### Inserting 'Key-Value' Pairs Into Dictionaries

Even when trying to **insert** data using the `.update()` method; there are several ways that this can be done!

##### Inserting 'Key-Value' Pairs From Another Dictionary

We are now going to be ( "*kind of like*" *Avinash Utam Mungur* ) **combining** ( *if need be... updating 'values' of key-value pairs* ) 2 dictionaries

1. In this example, we are only going to **combine** 2 dictionaries into 1.

```python
# dictionary that only contains integer data-types
int_int_dict: dict = {1: 1, 2: 2, 3: 3}

# dictionary that only contains string data-types
str_str_dict: dict = {"BMW": "E46", "Nissan": "GTR R32", "TOYOTA": "Supra"}

# output the 'integer-integer' dictionary before insertion
print(f"Integer Dictionary ( Before Insertion ): {int_int_dict}")
# output the 'string-string' dictionary before insertion
print(f"String Dictionary ( Before Insertion ): {str_str_dict}")

# add the contents of `str_str_dict` into `int_int_dict`
int_int_dict.update(str_str_dict)

# output a rule
print("\n" + "-" * 70, "\n")

# output the 'integer-integer' dictionary after insertion
print(f"Integer Dictionary ( After Insertion ): {int_int_dict}")
# output the 'string-string' dictionary before insertion
print(f"String Dictionary ( After Insertion ): {str_str_dict}")
```

- The output for the above code is going to look like this:

```console
Integer Dictionary ( Before Insertion ): {1: 1, 2: 2, 3: 3}
String Dictionary ( Before Insertion ): {'BMW': 'E46', 'Nissan': 'GTR R32', 'TOYOTA': 'Supra'}

---------------------------------------------------------------------- 

Integer Dictionary ( After Insertion ): {1: 1, 2: 2, 3: 3, 'BMW': 'E46', 'Nissan': 'GTR R32', 'TOYOTA': 'Supra'}
String Dictionary ( After Insertion ): {'BMW': 'E46', 'Nissan': 'GTR R32', 'TOYOTA': 'Supra'}
```

As you can see, we took all of the **data** ( *'key-value' pairs* ) from the `str_str_dict` and added *copied* these data into the `int_int_dict.

Nevertheless, the data inside the `str_str_dict` does **not** change!

> This is the reason as to why I said "*copied*"

2. During the *combination* process, we are going to also **update** the *value* of a 'key-value' pair.

```python
# dictionary that only contains integer data-types
old_dict: dict[int, int] = {1: 1, 2: 2, 3: 3}

# dictionary that only contains integer data-types
new_dict: dict[int, int] = {1: 666, 4: 4, 3: 999}

# output the old dictionary before insertion
print(f"Old Dictionary ( Before Insertion ): {old_dict}")

# add the contents of `str_str_dict` into `int_int_dict`
old_dict.update(new_dict)

# output the old dictionary after insertion
print(f"Old Dictionary ( After Insertion ): {old_dict}")
```

- The output for the code $\uparrow$ is going to look like this $\downarrow$:

```console
Old Dictionary ( Before Insertion ): {1: 1, 2: 2, 3: 3}
Old Dictionary ( After Insertion ): {1: 666, 2: 2, 3: 999, 4: 4}
```

This is basically applying the same principle from above $\uparrow$ but now we have also **updated** the value for the key `1` and also `3` while **adding** the new 'key-value' pair `5: 5`.

##### Inserting 'Key-Value' Pairs From Iterables

If you are here, I think that you did take a look at the section of '[[#Converting to Dictionaries]]'.

This means that you know what *types* ( *the format* ) of data structures that can be used to make **dictionaries**.

> Again, please refer to the above $\uparrow$ section... Not going to be re-explaining!

> [!INFO]
> Note that we <span style="color: red;"> cannot</span> pass **multiple** arguments as parameters inside the `.update()` method / function!

```python
# dictionary that only contains 'integer-string' pairs
int_str_dict: dict[int, str] = {1: "one", 2: "two", 3: "three"}

# output the integer-string dictionary before insertion
print(f"Integer - String Dictionary ( Before Insertion ): {int_str_dict}")

# list of tuples of 2 elements containing 'integer' and 'string' elements
int_str_list: list[tuple[int, str]] = [(1, "the one"), (4, "four")]

# tuples of tuples of 2 elements containing 'integer' and 'string' elements
int_str_tuple: tuple[tuple[int, str], ...] = ((5, "five"), (6, "six"))

# add - update the contents of dictionary with `int_str_list`
# INFO: in addition to inserting data; it will also update key '1'
int_str_dict.update(int_str_list)

# add the contents of dictionary with `int_str_tuple`
int_str_dict.update(int_str_tuple)

# output the integer-string dictionary after insertion
print(f"Integer - String Dictionary ( After Insertion ): {int_str_dict}")
```

Now, the output of the above code should be like so:

```console
Integer - String Dictionary ( Before Insertion ): {1: 'one', 2: 'two', 3: 'three'}
Integer - String Dictionary ( After Insertion ): {1: 'the one', 2: 'two', 3: 'three', 4: 'four', 5: 'five', 6: 'six'}
```

> [!WARNING] *List of Tuples* or *Tuples of Tuples* Only!!!
> Yes! Even though we can convert *the above $\uparrow$ mentioned* data structures.
>
> Nevertheless, with the `.update()` function, we can only pass in:
>
> - Other dictionaries ( *obviously* )
> - List of Tuples 
> - Tuple of Tuples
>
> > Nothing more and nothing less!
>

> [!TIP] Nevertheless!
> We can see that the general format for **both** '*List of Tuples*' and '*Tuple of Tuples*' are going to be like so:
>
> ```python
> # list of tuples of 2 elements
> key_value_list = [(key, value), (key, value), (key, value)]
>
> # tuple of tuples of 2 elements
> key_value_tuple = ((key, value), (key, value), (key, value))
> ```

### Keyword Arguments

I think this is the *second* simplest way to either **insert** or **modify** ( *"update" if you prefer* ) data into a dictionary.

As you know, we **cannot** pass **multiple** '*list of tuples*' and / or '*tuple of tuples*' inside the `.update()` method.

But with this "*method*"; you will be <span style="color: green;"> able</span> to pass **multiple** 'key-value' pairs inside the `.update()` function.

> [!WARNING] **Keys** should be *Identifiers*
> What I mean by "*identifiers*" is that it should be like a **variable** ( *or "constant" if you prefer* ).
>
> Take a look at the **arguments** that is being passed inside the function.

```python
# empty dictionary that will keep user's data
user_details_dict: dict = {}

# output the integer-string dictionary before insertion
print(f"Integer - String Dictionary ( Before Insertion ): {user_details_dict}")

# add the following data into the dictionary
user_details_dict.update(username="Biggie Cheese", age=30, status="dancing")
# add - update the following data into the dictionary
user_details_dict.update(status="working", pension=False, salary=1234.5678)

# output the integer-string dictionary after insertion
print(f"Integer - String Dictionary ( After Insertion ): {user_details_dict}")
```

The output for the above code is found below $\downarrow$:

```console
Integer - String Dictionary ( Before Insertion ): {}
Integer - String Dictionary ( After Insertion ): {'username': 'Biggie Cheese', 'age': 30, 'status': 'working', 'pension': False, 'salary': 1234.5678}
```

> [!NOTE]
> The keen eyes of yours might have already noticed that all the *identifiers* now has the "*type*" of **string**!
>
> > That's all that I have to say here!
>

> [!WARNING] Neovim Users
> > "*I use VIM BTW*!!!"
>
> If you are like me and have a *janked* 'LSP' setup, you are going to see that you get error when you do use this method.
>
> > Just ignore it!
>
> I mean, it might be a bad practice but it works!
>
> > Its not janked if its showing errors / practice that should not be used.
>

> [!TIP] The Format!
> As you can clearly see with your eyes... *Obviously you cannot see with your fucking buttocks, can you*?
>
> The format for using the "*keyword argument method*" is going to look like this:
>
> ```python
> dict_name.update(key=value, key=value, key=value)
> ```

### Set Default Method

> [!INFO]
> Similar to the `.update()` function being mostly an "**update**" / "modification" method; which can also insert data into a dictionary.
>
> The `.setdefault()` method / function is basically the same *thing* as the `.update()` method whereby its **not** really a "*method*" to insert data into a dictionary.
>
> > It's main purpose is to return the **value** of a specified *key*!
>
> But as it can also **insert** a 'key-value' pair if it does <span style="color: red;"> not</span> find *that* 'key-value' pair inside the **dictionary**.
>
> > [!WARNING]
> > The 'key-value' pair that is going to be **inserted** will see odd at first!
> >
> > This is because the **first** argument that can be passed inside the `.setdefault()` method is going to be the *key* itself. "*Where are we going to provide the actual value for that key*"?
> >
> > The thing is you don't; I mean you specify and and Python does that automatically for you... Very Nice!
> >
> > > That is where the **second** argument comes into play!
> >
>
> > Let's get coding!
>

1. **Not** Passing Any `default` Arguments

```python
# empty dictionary that will keep user's data
# dictionary that can contain any type of data
general_type_dict: dict = {1: "one", 2: "two"}

# output the integer-string dictionary before insertion
print(f"Integer - String Dictionary ( Before Insertion ): {general_type_dict}")

# return the value associated with key '1'
key_1_value = general_type_dict.setdefault(1)
# return the value assciated with the key '2'
key_2_value = general_type_dict.setdefault(2)
# return the value assciated with the key '3'
key_3_value = general_type_dict.setdefault(3)
# return the value assciated with the key '4'
key_4_value = general_type_dict.setdefault(4)

# display the values of the variables found above
print("\n" + "-" * 50, "\n")

print(f"Variable 'key_1_value' Contains: {key_1_value}")
print(f"Variable 'key_2_value' Contains: {key_2_value}")
print(f"Variable 'key_3_value' Contains: {key_3_value}")
print(f"Variable 'key_4_value' Contains: {key_4_value}")

print("\n" + "-" * 50, "\n")

# output the integer-string dictionary after insertion
print(f"Integer - String Dictionary ( After Insertion ): {general_type_dict}")
```

- In this case, the output for the above program is going to look like this:

```console
Integer - String Dictionary ( Before Insertion ): {1: 'one', 2: 'two'}

-------------------------------------------------- 

Variable 'key_1_value' Contains: one
Variable 'key_2_value' Contains: two
Variable 'key_3_value' Contains: None
Variable 'key_4_value' Contains: None

-------------------------------------------------- 

Integer - String Dictionary ( After Insertion ): {1: 'one', 2: 'two', 3: None, 4: None}
```

2. Passing *something* inside the `default` Argument

```python
# empty dictionary that will keep user's data
# dictionary that can contain any type of data
general_type_dict: dict[int, str] = {1: "one", 2: "two"}

# output the integer-string dictionary before insertion
print(f"Integer - String Dictionary ( Before Insertion ): {general_type_dict}")

# return the value associated with key '1'
key_1_value = general_type_dict.setdefault(1, "just inserted")
# return the value assciated with the key '2'
key_2_value = general_type_dict.setdefault(2, "just inserted")
# return the value assciated with the key '3'
key_3_value = general_type_dict.setdefault(3, "just inserted")
# return the value assciated with the key '4'
key_4_value = general_type_dict.setdefault(4, "just inserted")

# display the values of the variables found above
print("\n" + "-" * 50, "\n")

print(f"Variable 'key_1_value' Contains: {key_1_value}")
print(f"Variable 'key_2_value' Contains: {key_2_value}")
print(f"Variable 'key_3_value' Contains: {key_3_value}")
print(f"Variable 'key_4_value' Contains: {key_4_value}")

print("\n" + "-" * 50, "\n")

# output the integer-string dictionary after insertion
print(f"Integer - String Dictionary ( After Insertion ): {general_type_dict}")
```

- Same thing as before, we now we have provided a `default` **value** for the data that were originally **not** found inside the dictionary

```console
Integer - String Dictionary ( Before Insertion ): {1: 'one', 2: 'two'}

-------------------------------------------------- 

Variable 'key_1_value' Contains: one
Variable 'key_2_value' Contains: two
Variable 'key_3_value' Contains: just inserted
Variable 'key_4_value' Contains: just inserted

-------------------------------------------------- 

Integer - String Dictionary ( After Insertion ): {1: 'one', 2: 'two', 3: 'just inserted', 4: 'just inserted'}
```

> [!INFO] Common Sense
> "*I personally don't have that $\nwarrow$*!
>
> So if we provide a **key** into the `.setdefault()` method / function that is you know is *present* inside the dictionary; well, its going to return that **value** for *that* key!
>
> Now, if you provide a **key** that is <span style="color: red;"> not</span> available inside *that* dictionary. Given that you did not *touch* the `default` argument, its going to return `None`.
>
> Now, its going to **first** *insert* the 'key-value' pair ( *in our / this case, the value is `None`* ) into the dictionary **then** *returns* that key's value with is obviously `None` in this case!
>
> > Told you it was so *fucking* normie, common sense!
>

## Removal of Data

There are 3 **main** *methods* of to **remove** '*key-value*' pairs inside a dictionary, they are:

1. `dict_name.clear()`
2. `dict_name.pop(key)`
3. `dict_name.popitem()`

### Clear Method

I mean we have been talking about this for years now, right? Then, do I need to write something here?

> Yes, its basically the **same** thing as in [[Python - Lists#Clear Method | lists]], [[Python - Sets#Clear Method | sets]]!

```python
# dictionary containing hashable data types
general_dict: dict = {
    1: 1,
    2: "something",
    "some_nums": [69.69, 55, 27],
    "sets": {1, 2, 3, "A", "B", "C"},
    "a_dict": {1: "one", 2: "two", 3: "three"},
    ("Mazda", "BMW", "Porsche", "Lancia", "Lotus"): ["Car", "Brands"],
}


# output the general dictionary before removal
print(f"General Dictionary ( Before Removal ): {general_dict}")

# clear out the whole dictionary
general_dict.clear()

# output the general dictionary after removal
print(f"\nGeneral Dictionary ( After Removal ): {general_dict}")
```

Well, we should get an **empty** dictionary as output!

```console
General Dictionary ( Before Removal ): {1: 1, 2: 'something', 'some_nums': [69.69, 55, 27], 'sets': {1, 2, 3, 'A', 'B',
 'C'}, 'a_dict': {1: 'one', 2: 'two', 3: 'three'}, ('Mazda', 'BMW', 'Porsche', 'Lancia', 'Lotus'): ['Car', 'Brands']}

General Dictionary ( After Removal ): {}
```

### Pop Method

> [!NOTE]
> The `.pop()` method here is more similar to the `.pop()` method that are used with [[Python - Lists#Pop Method | lists]] than the `.pop()` method used with [[Python - Sets#Pop Method | sets]].

This is because compared to *sets*; the `.pop()` method here does take a parameter and that parameter is <span style="color: red;"> not</span> an **index** ( *obviously* ).

In this case, the *method* will take a **key** as argument and then **completely remove** that '*key-value*' pair.

In addition, to passing the **key** as parameter, we can also pass another *argument* called the `default` ( *kind of the same thing as in `.update()`* ). Whereby, we can provide a *default* value instead or raising a '*KeyError*'.

```python
# dictionary containing hashable data types
general_dict: dict = {
    1: 1,
    2: "something",
    "some_nums": [69.69, 55, 27],
    "sets": {1, 2, 3, "A", "B", "C"},
    "a_dict": {1: "one", 2: "two", 3: "three"},
    ("Mazda", "BMW", "Porsche", "Lancia", "Lotus"): ["Car", "Brands"],
}


# output the general dictionary before removal
print(f"General Dictionary ( Before Removal ): {general_dict}")

# remove the 'key-value' pair with key '1'
general_dict.pop(1)
# remove the 'key-value' pair with key 'a_dict'
general_dict.pop("a_dict")
# remove the 'key-value' pair with key '("Mazda", "BMW", "Porsche", "Lancia", "Lotus")'
general_dict.pop(("Mazda", "BMW", "Porsche", "Lancia", "Lotus"))

# output the general dictionary after removal
print(f"\nGeneral Dictionary ( After Removal ): {general_dict}")

# remove something that is not present
general_dict.pop("Joe Mama")
```

The output for the above code is going to look like this:

```console
General Dictionary ( Before Removal ): {1: 1, 2: 'something', 'some_nums': [69.69, 55, 27], 'sets': {1, 2, 3, 'C', 'A',
 'B'}, 'a_dict': {1: 'one', 2: 'two', 3: 'three'}, ('Mazda', 'BMW', 'Porsche', 'Lancia', 'Lotus'): ['Car', 'Brands']}

General Dictionary ( After Removal ): {2: 'something', 'some_nums': [69.69, 55, 27], 'sets': {1, 2, 3, 'C', 'A', 'B'}}
Traceback (most recent call last):
  File "/home/username/Desktop/test.py", line 26, in <module>
    general_dict.pop("Joe Mama")
    ~~~~~~~~~~~~~~~~^^^^^^^^^^^^
KeyError: 'Joe Mama'
```

> This is **good**!

> [!NOTE] Default Argument
> Taking the **same** code as above $\uparrow$; and modifying the last line to this $\Rightarrow$ `general_dict.pop("Joe Mama", "Not Found")`
>
> Instead of getting the error in the output, we should have this:
>
> ```console
> General Dictionary ( Before Removal ): {1: 1, 2: 'something', 'some_nums': [69.69, 55, 27], 'sets': {1, 2, 3, 'C', 'A',
 'B'}, 'a_dict': {1: 'one', 2: 'two', 3: 'three'}, ('Mazda', 'BMW', 'Porsche', 'Lancia', 'Lotus'): ['Car', 'Brands']}
>
> General Dictionary ( After Removal ): {2: 'something', 'some_nums': [69.69, 55, 27], 'sets': {1, 2, 3, 'C', 'A', 'B'}}
> ```
>
> If you wish to, you can add the `default` argument all the time... Because the `default` argument will *spring into action* only when the 'key-value' pair has **not** been found!

> [!TIP] Nevertheless!
> Similar to *list*, the `.pop()` method here, will also **keep track** of the *value* that has removed
>
> Yes, the **value** and not the 'key-value' *tuple* pair!
>
> > So in this way, it is completely alike to the `.pop()` used in lists!
>

> [!INFO]
> If we try to remove a 'key-value' pair that is either <strong> <span style="color: red;"> empty</span> </strong> or the **key** specified is <strong> <span style="color: red;"> not</span> </strong> found inside the dictionary and we have **not** provided passed any arguments as parameters for `default`.
>
> Therefore, the `.pop()` will **raise** a '*KeyError*'.
>
> > But passing `default` will obviously **not** *raise* any error
>

### Pop Item Method

Do you remember how the `pop()` method / function worked for [[Python - Sets#Pop Method | sets]]?

Do you remember how it was removing an "*arbitrary*" element from the set? This is because of their underlying "*technology*" which are '**Hash Tables**'. Therefore, they did **not** have *indices* and removed that *arbitrary* item based on the inner working of the Hash Tables.

> As you can read from this shitty paragraph above $\uparrow$, I still haven't learnt anything about **Hash Tables**!!!

The `.popitem()` method works similarly here whereby it removes, *what it seeems to be* a **random** element from the dictionary.

But fear not! As per the [documentation](https://docs.python.org/3/library/stdtypes.html#dict.popitem) the `.popitem()` method will **remove** and **return** a *tuple of 2 elements* containing the **key** and the corresponding **value**. But the removal process is <span style="color: red;"> not</span> **random**!

This method uses the 'LIFO' algorithm to remove data from that dictionary.

> [!TIP] What is 'LIFO'?
> Now, 'LIFO' means '*Last In First Out*'. As the simple English words tells you. The **last** items / 'key-value' pair that goes into the dictionary will be the one that will be *removed* **first**!

```python
# dictionary containing hashable data types
general_dict: dict = {
    1: 1,
    2: "something",
    "some_nums": [69.69, 55, 27],
    "sets": {1, 2, 3, "A", "B", "C"},
    "a_dict": {1: "one", 2: "two", 3: "three"},
    ("Mazda", "BMW", "Porsche", "Lancia", "Lotus"): ["Car", "Brands"],
}


# output the general dictionary before removal
print(f"General Dictionary ( Before Removal ): {general_dict}")

# the line below should remove the last 'key-value' pair
last_data = general_dict.popitem()
# the line below should remove the 5th 'key-value' pair
second_last_data = general_dict.popitem()

# output the general dictionary after removal
print(f"\nGeneral Dictionary ( After Removal ): {general_dict}")

# display the returned value of `.popitem()`
print("\n" + "-" * 90, "\n")
print(f"Variable 'last_data' Content: {last_data}")
print(f"Variable 'second_last_data' Content: {second_last_data}")
print("\n" + "-" * 90, "\n")
```

The output for the above $\uparrow$ code is going to look like this $\downarrow$:

```console
General Dictionary ( Before Removal ): {1: 1, 2: 'something', 'some_nums': [69.69, 55, 27], 'sets': {1, 2, 
3, 'C', 'B', 'A'}, 'a_dict': {1: 'one', 2: 'two', 3: 'three'}, ('Mazda', 'BMW', 'Porsche', 'Lancia', 'Lotus
'): ['Car', 'Brands']}

General Dictionary ( After Removal ): {1: 1, 2: 'something', 'some_nums': [69.69, 55, 27], 'sets': {1, 2, 3
, 'C', 'B', 'A'}}

------------------------------------------------------------------------------------------ 

Variable 'second_last_data' Content: (('Mazda', 'BMW', 'Porsche', 'Lancia', 'Lotus'), ['Car', 'Brands'])
Variable 'last_data' Content: ('a_dict', {1: 'one', 2: 'two', 3: 'three'})

------------------------------------------------------------------------------------------ 
```

> If you still **don't** understand this simple shit, there is an example code provided below!

## Miscellaneous Methods / Functions

### Copy Method

> I mean come on now! Its in the *fucking* word now!

```python
# dictionary containing hashable data types
general_dict: dict = {
    1: 1,
    2: "something",
    "some_nums": [69.69, 55, 27],
    "sets": {1, 2, 3, "A", "B", "C"},
    "a_dict": {1: "one", 2: "two", 3: "three"},
    ("Mazda", "BMW", "Porsche", "Lancia", "Lotus"): ["Car", "Brands"],
}

# create empty dictionary for "show-case" purposes
# INFO: this is Python, no need to declare anything
general_dict_copy = {}


# output the original general dictionary before removal
print(f"General Dictionary ( Before Removal ): {general_dict}")
# output the new general dictionary before removal
print(f"General Dictionary - Copy ( Before Removal ): {general_dict_copy}")

# copy the original dictionary
general_dict_copy = general_dict.copy()

# output the original general dictionary after removal
print(f"\nGeneral Dictionary ( After Removal ): {general_dict}")
# output the new general dictionary after removal
print(f"\nGeneral Dictionary - Copy ( After Removal ): {general_dict_copy}")
```

> I mean do I need to explain to you "*piece of shit*" what's going to happen here!

```console
General Dictionary ( Before Removal ): {1: 1, 2: 'something', 'some_nums': [69.69, 55, 27], 'sets': {'A', 1, 2, 3, 'B',
 'C'}, 'a_dict': {1: 'one', 2: 'two', 3: 'three'}, ('Mazda', 'BMW', 'Porsche', 'Lancia', 'Lotus'): ['Car', 'Brands']}
General Dictionary - Copy ( Before Removal ): {}

General Dictionary ( After Removal ): {1: 1, 2: 'something', 'some_nums': [69.69, 55, 27], 'sets': {'A', 1, 2, 3, 'B', 
'C'}, 'a_dict': {1: 'one', 2: 'two', 3: 'three'}, ('Mazda', 'BMW', 'Porsche', 'Lancia', 'Lotus'): ['Car', 'Brands']}

General Dictionary - Copy ( After Removal ): {1: 1, 2: 'something', 'some_nums': [69.69, 55, 27], 'sets': {'A', 1, 2, 3
, 'B', 'C'}, 'a_dict': {1: 'one', 2: 'two', 3: 'three'}, ('Mazda', 'BMW', 'Porsche', 'Lancia', 'Lotus'): ['Car', 'Brand
s']}
```

### Get Method

So the `.get()` method / function will allow one to return the **values** associated with key!

This method is normally used for displaying values of the *specific* **keys** found in the dictionary.

> For programs that required the use the enter the keys of "*things*"!

> [!NOTE]
> The `.get()` method is similar to the `.setdefault()` method / function whereby it has the `default` *parameter* / *argument*.
>
> But in this case, it will **not** *insert* anything inside the dictionary but instead; it will provide a default message instead of raising any **errors**!

> [!INFO] Speaking of Errors!!!
> If we **don't** provide the `default` *argument* / *parameter*; if we try to `.get()` a **key** that is <span style="color: red;"> <strong> not</strong> </span> present inside the dictionary...
>
> Our `.get()` method will **never** raise any errors!
>
> > I mean it kind of make sense as we are only retrieving the **value** of the *key* to be able to display it!
> >
>

```python
# dictionary containing hashable data types
general_dict: dict = {
    1: 1,
    2: "something",
    "some_nums": [69.69, 55, 27],
    "sets": {1, 2, 3, "A", "B", "C"},
    "a_dict": {1: "one", 2: "two", 3: "three"},
    ("Mazda", "BMW", "Porsche", "Lancia", "Lotus"): ["Car", "Brands"],
}


# get the value for the key '("Mazda", "BMW", "Porsche", "Lancia", "Lotus")'
print(
    f"\nValue for Key ( see code ): {general_dict.get(('Mazda', 'BMW', 'Porsche', 'Lancia', 'Lotus'))}"
)

# get the vaule for the key 'some_nums'
print(
    f"Value for Key 'some_nums': {general_dict.get('some_nums', 'Key is NOT Present Inside Dictionary!!!')}"
)

# get the balue for the key 'shitter'
print(
    f"Value for Key 'shitter': {general_dict.get('shitter', 'Key is NOT Present Inside Dictionary!!!')}"
)

# get the balue for the key 'shitter'
print(f"Value for Key 'shitter': {general_dict.get('shitter')}")
```

Running the above code will get us this output:

```console
Value for Key ( see code ): ['Car', 'Brands']
Value for Key 'some_nums': [69.69, 55, 27]
Value for Key 'shitter': Key is NOT Present Inside Dictionary!!!
Value for Key 'shitter': None
```

> [!SUCCESS] Well this is it!!!
> I think that we have completed the most and also the basics of these data structures!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!