---
id: Python - Sets
aliases: Sets in Python
tags:
  - python
  - data-structures
  - sets
author: S.Sunhaloo
date: 2025-04-24
status: Completed
---

## List of Contents

- [[#What are Sets?]]
- [[#Creation of Sets]]
- [[#Displaying - Accessing Sets]]
	- [[#Displaying Sets and Sets Value(s)]]
	- [[#Accessing Sets Value(s)]]
- [[#Unpacking of Sets]]
- [[#Functions and Methods of Sets]]
	- [[#Insertion of Data]]
		- [[#Add Method]]
		- [[#Update Method]]
		- [[#Set Comprehension - Insertion of Elements]]
	- [[#Removal of Data]]
		- [[#Clear Method]]
		- [[#Pop Method]]
		- [[#Remove Method]]
		- [[#Discard Method]]
		- [[#Set Comprehension - Removal of Elements]]
	- [[#Miscellaneous Methods / Functions]]
		- [[#Set Equality and Inequality]]
		- [[#Copy Method]]
		- [[#Difference Update Method]]
		- [[#Difference Method]]
		- [[#Intersection Method]]
		- [[#Intersection Update Method]]
		- [[#Disjoint Method]]
		- [[#Subset Method]]
		- [[#Superset Method]]
		- [[#Symmetric Difference Method]]
		- [[#Symmetric Difference Update Method]]
		- [[#Union Method]]
- [[#Summary of Operators]]

---

> [!NOTE]
> I expect you to have **already** read the notes / files '[[Python - Lists]]', '[[Python - Two Dimensional Lists]]' and '[[Python - Tuples]]' before coming here!
>

# What are Sets?

> [!TIP] Definition of Sets
> Similar to *list* and *tuples*; sets stores a collection of items and has the following properties:
>
> - No Duplicate Items
> - Unordered Collection
> 	- No **indexes** ( *i.e cannot do something like `set_name[0]`* )
> - Uses [Hashing](https://en.wikipedia.org/wiki/Hash_function) to allow efficient *insert*, *remove* and *search* operations
> - Allows for *insertion* and *removal* of **new elements**
> 	- Elements already present at creation <span style="color: red;"> cannot</span> be changed directly
> 	- Implies for elements **already** inside... They *cannot* be **modified**.
> 		- Meaning that we cannot change the element at an index in a set

> [!WARNING]
> Compared to *tuples*; Sets do **enforce uniqueness**!!!

> [!NOTE] That's the Thing!!!
> I have **never** used *sets* in my life in Python!
>
> Therefore, both me and you, we are going to learn *sets* with actually coding and not just simple regurgitation or learning by heart!
>
> > Let's get to coding!
>

---

# Creation of Sets

To create a set in Python, we use the `{}` characters!

```python
# set of integer numbers only
int_set: set[int] = {1, 1, 2, 3, 4, 4, 5}

# set containing most data types
general_set: set = {
    44,
    5.5,
    "A",
    "Something",
    True,
    2 + 5j,
    None,
}
```

> [!INFO]
> 2D-Sets does not really exists!
>
> Additionally, compared to 2D-Lists or even multi-dimensional lists... 2D-Sets are used for very specific reasons.
>
> I will make another note called '[[Python - Sets ( Frozen Sets )]]' going over how we can make 2D-Sets.
>
> > Hence, I will only be focusing on 1D-Sets in this very note!
>

> [!INFO] `type()` of Set
> If we run `print(type(int_set))` or `print(type(general_set))` we should see that we get:
>
> ```console
> <class 'set'>
> ```
>
> Nevertheless, the word '*set*' is **not** a reserved word in Python and you can create a set called `set` like so:
>
> ```python
> set = {1, "shitter", 'A', 69.69}
> ```
>
> > Nevertheless, this is **not** recommended!

> [!WARNING]
> Sets **cannot** store elements such as *lists*, *dictionaries*, *sets* and *tuples* ( *if elements in tuples are non-hashable* ).
>
> Data types that are *hashable* are things like:
>
> 1. Numeric Types ( `int`, `float`, `complex` )
> 2. Boolean
> 3. None Type ( `None` )
> 4. Strings
> 5. Tuples ( _**if and only if** elements found in tuples are hashable_ )
>
> ```python
> # set containing list and dictionary, set and tuple ( with non-hashable elements )
> bad_set: set = {[1, 2, 3], {"x": "nice", "y": "not nice"}, {1, 1, 2, 3, 4}, ([1, 2, 3])}
> ```
>
> The above code will return a '*TypeError*'!
>
> ```console
> Traceback (most recent call last):
>  File "/home/username/Desktop/main.py", line 2, in module
>    bad_set: set = {[1, 2, 3], {"x": "nice", "y": "not nice"}, {1, 1, 2, 3, 4}, ([1, 2, 3])}
>                   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
> TypeError: unhashable type: 'list'
> ```
>
> > [!SUCCESS] But We Can Do This!!!
> > ```python
> > # set containing hashable elements ( with tuple containing hashable elements )
> > good_set: set = {
> >    44,
> >    5.5,
> >    "A",
> >    "Something",
> >    True,
> >    2 + 5j,
> >    None,
> >    (44, 5.5, "A", "Something", True, 2 + 5j, None),
> > }
> >
> > # display the set
> > print(f"Good Set: {good_set}")
> > ```
> >
> > This is completely fine!
> >
> > ```console
> > Good Set: {None, True, 5.5, 44, 'A', (2+5j), 'Something', (44, 5.5, 'A', 'Something', True, (2+5j), None)}
> > ```

> [!INFO] Type Annotation / Hinting
> I am **not** going to explain things again as its literally the **same** as [[Python - Lists#Type Annotation / Hinting | lists]]!

---

# Displaying - Accessing Sets

## Length of Sets

> I am tired of saying things!

Well, the code block below will show you how we can get the length of sets using the very famous `len()` function!

```python
# create a set of integers ==> has 5 items
int_set: set[int] = {1, 2, 3, 4, 5}
# create a set of boolean values ==> has 4 items
bool_set: set[bool] = {True, False, False, True}
# create a set of strings ==> has 4 items
str_set: set[str] = {"Carlos Sainz", "Charles Leclerc", "", "Pierre Gasly"}


# output the size of each set
print("\n<< Size of Sets > > \n")

print(f"Size of Integer Set = {len(int_set)}")
print(f"Size of Boolean Set = {len(bool_set)}")
print(f"Size of String Set = {len(str_set)}")
```

Therefore, we should receive the output below

```console

<< Size of 1D-Set > >

Size of Integer Set = 5
Size of Boolean Set = 2
Size of String Set = 4
```

## Displaying Sets and Sets Value(s)

Again, here also I am just going to *copy-paste* the code found in '[[Python - Lists#Displaying List and List Value(s) | Python - Lists]]' and '[[Python - Tuples#Displaying Tuples and Tuples Value(s) | Python - Tuples]]'

> Because I fucking can!

```python
# set of integer numbers
int_set = {1, 2, 3, 4, 5}

print("\nPythonic Version\n")

# the pythonic way of displaying set
# "unpack" the values
print(*int_set)

print("\n'Normal' Version\n")

# "normal" way to display values of set
# interate through the set
for num in int_set:
    # output the value at each index
    print(num)

print("\n'C' - Python Version\n")

# doing the same thing above but using 'enumerate' function
for index, num in enumerate(int_set):
    # output the index and its corresponding value
    print(f"Index = {index} | Value: {num}")
```

Then again, we should have the following code:

```console

Pythonic Version

1 2 3 4 5

'Normal' Version

1
2
3
4
5

'C' - Python Version

Index = 0 | Value: 1
Index = 1 | Value: 2
Index = 2 | Value: 3
Index = 3 | Value: 4
Index = 4 | Value: 5
```

> [!WARNING]
> <p align="center"> "<em> Implies for elements already inside... They cannot be modified</em> "</p>
>
> We all know and love this ( *IDK how to call it* ):
>
> ```python
> # import the random module
> import random
>
> # iterate through the list or tuple
> for i in range(len(list_tuple)):
>    # change each element in the list / tuple
>    list_tuple[i] = random.randint(0, 9)
> ```
>
> > [!BUG] Well, Its **Not** Available Here!!!
>
> It all relates back the the *quote* above!
>
> Heck this `set_name[0]` give me an error in my IDE ( *I use VIM BTW* ).
> This is why we cannot do the '*C*' way of displaying sets.

## Accessing Sets Value(s)

> Well, Well, Well... *Its The Same As Tuples*!!!

Again, simply because of the "*definition*" of Sets; we **cannot** *modify* the individual elements of sets!

Therefore, this leaves us with only *one method* to **access** these elements.

```python
# our main function
def main():
    # empty integer set
    none_duplicated_set: set[int] = set()

    # output the integer set ( before insertion )
    print(f"Integer Set ( Before Insertion ): {none_duplicated_set}")

    # set of integer numbers
    int_set: set[int] = {1, 2, 3, 4, 5}

    # iterate through the integer set
    for num in int_set:
        # calculate the square of each number and append to the set
        # NOTE: functions / methods are found below
        none_duplicated_set.add(pow(num, 2))

    # output the integer set ( after insertion )
    print(f"Integer Set ( After Insertion ): {none_duplicated_set}")


# source the main function
if __name__ == "__main__":
    main()
```

We should have something like this!

```console
Integer Set ( Before Insertion ): set()
Integer Set ( After Insertion ): {1, 4, 9, 16, 25}
```

> [!WARNING] Sets $\neq$ [[Python - Dictionaries#Creation of Dictionaries | Dictionaries]]!
> This means **only and only** for *Sets*; to create an **empty** set, we need to use `set()` instead of `{}`.
>
> This is because `{}` is also the *syntax* for **Dictionaries**!

# Unpacking of Sets

To be honest with you; it is literally the **same** as [[Python - Tuples#Unpacking of Tuples | unpacking of tuples]]!

Whereby if you unpack with the actual *unpacking* `*` operator... You are going to get a **list** and again, you need to continue to use *sets*. You can simply *type cast* that **list** with `set()` onto another variable!

---

# Functions and Methods of Sets

> [!INFO]
> I am **not** going to write about every and all the *functions* and *methods* that can be used with sets.
>
> If you take a look at the list of contents for '[[Python - Lists#List of Contents | Python - Lists]]'.
> You will find that I have *documented* most of the *functions* and *methods* that works with **iterables**
>
> Therefore, I suggest you that you yourself put in some work and use them yourself!
>
> Hence, I will only be writing about the *functions* and *methods* found when you run `dir(set)`!
>
> > Additionally, its taking to much time to write all of this now :)!
>

## Insertion of Data

Compared to **lists**, there are <span style="color: red;"> no</span> such things as `.insert()` and `.append()`.

But we do have these:

1. `set_name.add(element)`
2. `set_name.update(iterable)`

### Add Method

As the word "*add*" tells us; this method will be used to add **elements** into our *sets*!

But it has a little quirk. So you remember how I was talking about how **sets** can only hold *hashable data types* and therefore, **cannot** hold elements such a *lists* and others!

> [!NOTE]
> Well, from what I can understand, the `.add()` method will only *add* that element in the "*last*" position like the `.append()` method.
>
> > [!WARNING]
> > When I say "*last position*"; I am referring how it will **place** the *element* into the set.
> >
> > Remember kids! we **cannot** access a **specific** *element* from a set with something like this `set_name[index]`
> >
> > > Let us get to coding and I will show you what I really mean!
> >

> [!INFO]
> With the `.add()` method, we are going to pass the **actual** *element* as **parameter**.

```python
# empty set
general_set: set = set()

# output the general set ( before insertion )
print(f"General Set ( Before Insertion ): {general_set}")

# append 'hello', 44, 'SS92', True to `general_list`
general_set.add("hello")
general_set.add(44)
general_set.add("SS92")
general_set.add(True)

# output the general set ( after insertion )
print(f"General Set ( After Insertion ): {general_set}")
```

This is the output that we [shall](https://www.youtube.com/watch?v=3xYXUeSmb-Y) receive for the about code block:

```console
General List ( Before Insertion ): set()
General Set ( After Insertion ): {True, 'SS92', 44, 'hello'}
```

> [!INFO] <span style="color: red;"> Ohh Fuck!!!</span>
>
> <p align="center"> "<em> I was Completely Wrong</em> "</p>
>
> Well, based on what I see above, its **not** like the `.append()` function whereby it will place the element at that "*last position*".
>
> See how we inserted the 'True' at the **end** in our code block but in the set its the **first** thing!
>
> > [!TIP] The Answer - Hash Tables
> > So, they way that a **set** where to place a specific element is based on [Hash Tables](https://en.wikipedia.org/wiki/Hash_table); which is basically another type of **data structure** that is *implemented* with **sets** and **[[Python - Dictionaries | dictionaries]]**
> >
> > This *Hash Table* will then use **Hash Function(s)** to calculate an **index** ( *or 'Hash Code'* ).
>
> > [!NOTE]
> > I have to confess something... As of now, I don't know anything about '*Hash Tables*', '*Hash Maps*'. Heck, even the definition of the work '*hash*' I don't know.
> >
> > But I do plan to learn it and after I create its own note / file... I will be placing its wiki-link here!
>

### Update Method

> A Dramatic Start!

> [!WARNING]
> The `.update()` method wears two faces. The reason as to why I am saying this is that; it **works differently** if we used it on a *set* or *dictionary*.
>
> > If you want to see how `.update()` work for dictionaries; head over to '[[Python - Dictionaries#Update Method | Python - Dictionaries]]'
>
> This is why ( *from my perspective* ) the `.update()` method has a **shorthand** version; whereby the *operator* `|=` does the exact **same** thing as the `.update()` method!
>
> In this, case we are **not** going to *confuse* it with the one used with dictionaries!
>
> > [!BUG] Drawback!
> > The drawback of using `|=` its that our **iterable** that we are trying to add **must** be of *data-type* `set`!
> >
> > > Hahaha "*Typeset*"; I am losing it!
> >
>

The `.update()` method can take **iterable(s)** like a *list(s)*, *tuple(s)* or *set(s)* and inserts their respective elements into the desired set!

> [!NOTE]
> This does **not** create a 2D-Set. Instead think of it like the `.extend()` [[Python - Lists#Extend Method | method]] that are used with **lists**!
>
> > [!INFO]
> > Additionally, the `.update()` method can have **multiple** *elements* as **parameters** and these "*elements*" can **must** be an *iterable*!

```python
# empty general set
general_set: set = set()

# output the general set ( before insertion )
print(f"General Set ( Before Insertion ): {general_set}")

# list of strings containing some elements
str_list: list[str] = ["The", "World", "Is", "Small"]

# tuple of integers containing some elements
int_tuple: tuple[int, ...] = tuple(num for num in range(1, 5))

# set of floating numbers containing some elements
float_set: set[float] = {12.23, 34.45, 45.56, 69.69}

# update general set with list of string
general_set.update(str_list)

# update general set with other iterables found above
general_set.update(int_tuple, float_set)

# list of integer containing some elements
int_list: list[int] = [even for even in range(25, 36) if even % 2 == 0]

# update general set with list of integers
general_set.update(int_list)

# output the general set ( after insertion )
print(f"General Set ( After Insertion ): {general_set}")

# update general set with list of string again
general_set.update(str_list)

# output the general set ( after final insertion )
print(f"\nGeneral Set ( After Final Insertion ): {general_set}")
```

Therefore, we should have *updated* ( *more like 'added'* ) these elements into the desired set:

```console
General Set ( Before Insertion ): set()
General Set ( After Insertion ): {1, 2, 3, 4, 'o', 'd', 12.23, 'r', 'Is', 26, 28, 30, 32, 34.45, 34, 45.56, 'w', 'World
', 69.69, 'l', 'Small', 'The'}

General Set ( After Final Insertion ): {1, 2, 3, 4, 'o', 'd', 12.23, 'r', 'Is', 26, 28, 30, 32, 34.45, 34, 45.56, 'w', 
'World', 69.69, 'l', 'Small', 'The'}
```

> [!NOTE] String Datatypes
> In Python, "*strings*" are also considered as **iterables**. Therefore, the `.update()` method does accept it. Very Nice!
>
> But one thing to consider is that how it "*expands*" the string `world` and places **each** character into the specified *set*.
>
> Whereby a *string* element found in a list; its just going place that **whole** string into the set!
>
> > See how we have `Is`, `'World'`, `Small` and `The`!
>

> [!INFO]
> Again, because sets does **not** hold *duplicate* elements... Even after *updating* the set again to add the list of string. Nothing happens and no warnings are raised!

#### Using the `|=` Operator

Here is how we can *mimic* the code above using the `|=` operator! 

> [!INFO]
> - Our *iterable* should be of type `set()`
> - To add multiple *iterable* at the same time just *pipe* `|` it

```python
# empty general set
general_set: set = set()

# output the general set ( before insertion )
print(f"General Set ( Before Insertion ): {general_set}")

# list of strings containing some elements
str_list: list[str] = ["The", "World", "Is", "Small"]

# tuple of integers containing some elements
int_tuple: tuple[int, ...] = tuple(num for num in range(1, 5))

# set of floating numbers containing some elements
float_set: set[float] = {12.23, 34.45, 45.56, 69.69}

# update general set with list of string
general_set |= set(str_list)

# update general set with other iterables found above
general_set |= set(int_tuple) | float_set

# list of integer containing some elements
int_list: list[int] = [even for even in range(25, 36) if even % 2 == 0]

# update general set with list of integers
general_set |= set(int_list)

# output the general set ( after insertion )
print(f"General Set ( After Insertion ): {general_set}")

# update general set with list of string again
general_set |= set(str_list)

# output the general set ( after final insertion )
print(f"\nGeneral Set ( After Final Insertion ): {general_set}")
```

We should get basically the same output as above:

```console
General Set ( Before Insertion ): set()
General Set ( After Insertion ): {32, 1, 2, 3, 4, 34.45, 'Small', 69.69, 34, 'The', 12.23, 45.56, 'Is', 'World', 26, 28
, 30}

General Set ( After Final Insertion ): {1, 2, 3, 4, 69.69, 'Small', 12.23, 'World', 26, 28, 30, 32, 34.45, 34, 'The', 4
5.56, 'Is'}
```

> Well, beoause of said *Hash Tables*... The **order** of the output will be different

> [!INFO]
> And yes! In this case the *iterable* that we are trying to "*update*" our set with **should** be type `set`.
>
> > Now, if we are trying to use `|=` with another *set*. Then **no** need to convert ( *obvious-fucking-ly* )!

### Set Comprehension - Insertion of Elements

I think you are a professional now when it comes to the *bulk* inserts using **list comprehension**.

Basically, its the **same** stuff that I should you in '[[Python - Lists#List Comprehension - Insertion of Elements | Python - Lists]]'.

> I am going to just 'copy-paste' the code because I fucking can!

```python
# integer set containing integer numbers starting from 500 to 550
int_set: set[int] = {(num + 500) for num in range(51)}

# output the integer set ( after insertion )
print(f"Integer Set ( After Insertion ): {int_set}")
```

> [!SUCCESS]
> Because of the *nature* of sets; we **cannot** *insert* data using [[Python - Lists#Insertion of Data in Other Ways | through other ways]] like the lovely 'Concatenation Operator' and / or the 'Slice *Operator*'.
>
> Therefore, consider this section done!

## Removal of Data

To remove **elements** from inside a *Set*, these *method* are available for us to use:

1. `set_name.clear()`
2. `set_name.pop()`
3. `set_name.remove(element)`
4. `set_name.discard(element)`

### Clear Method

> [Well, Well, Well](https://www.youtube.com/watch?v=XFagogEOZz8&t=15s)

I mean you should be a professional by now with the "*ultra*, *mega*, *famous*" `.clear()` method...

> Please just refer to '[[Python - Lists#Clear Method | Python - Lists]]' for more information!

```python
# set containing most data types
general_set: set = {
    44,
    5.5,
    "A",
    "Something",
    True,
    2 + 5j,
    None,
}

# output the general set ( before clearing )
print(f"General Set ( Before Clearing ): {general_set}")

# clear the set
general_set.clear()

# output the general set ( after clearing )
print(f"General Set ( After Clearing ): {general_set}")
```

> Do I even need to write this?

```console
General Set ( Before Clearing ): {None, True, (2+5j), 'A', 5.5, 'Something', 44}
General Set ( After Clearing ): set()
```

> [!NOTE] I Do Have To Write Something
> As you can see from the above output. It did correctly return an *empty* **set** with `set()` and not `{}`!

### Pop Method

You would think that I would have said that same thing above about being a "*professional*".

> Sike!

From our notes for `.pop()` for [[Python - Lists#Pop Method | Python lists]], we know that we have to *pass* in an **index** of the element as our *parameter*.

But *sets* does <span style="color: red;"> not</span> have **indices**!

Well, from the [official documentation](https://docs.python.org/3/library/stdtypes.html#frozenset.pop) it states that the `.pop()` method for *sets* is going to "_remove and return an **arbitrary**_" value from the set.

Nevertheless, you must **not** think that with *sets*, the `.pop()` method just *randomly* choose what element to remove. No! Here also we are going to use those lovely **Hash Table** to figure out what element should be removed.


> [!INFO]
> The `.pop()` method with *sets* will raise a '*KeyError*' if we are trying to remove data from an <strong> <span style="color: red;"> empty</span> </strong> set.
>
> I did notice something about the '*KeyError*', lets say that we have an empty set like so `empty_set: set = set()`. If we try to remove the **element** ( *or string* ) 'try to remove this'. Then we are going to get something that looks like this:
>
> ```console4
> # other error message here
>
> KeyError: 'try to remove this'
> ```
>
> This means if we had tried to remove another value for example '1'... Then *that* message would take it.
>
> > Just something that I noticed!
>
> > [!NOTE] Important Note!!!
> > Additionally, the `.pop()` method here does **not** take any *parameters*.
> > If a *parameter* is provided; then a '*TypeError*' will be raised!
>

```python
# set containing most data types
general_set: set = {
    44,
    5.5,
    "A",
    "Something",
    True,
    2 + 5j,
    None,
}

# output the general set ( before removal )
print(f"General Set ( Before Removal ): {general_set}\n")

# "arbitrary" removal of elements ( using hash tables )
general_set.pop()
print(f"General Set ( During Removal ): {general_set}")
general_set.pop()
print(f"General Set ( During Removal ): {general_set}")
general_set.pop()
print(f"General Set ( During Removal ): {general_set}")

# output the general set ( after popping )
print(f"\nGeneral Set ( After Popping ): {general_set}")
```

In this case, we are going to have this:

```console
General Set ( Before Removal ): {None, True, (2+5j), 5.5, 'A', 44, 'Something'}

General Set ( During Removal ): {True, (2+5j), 5.5, 'A', 44, 'Something'}
General Set ( During Removal ): {(2+5j), 5.5, 'A', 44, 'Something'}
General Set ( During Removal ): {5.5, 'A', 44, 'Something'}

General Set ( After Popping ): {5.5, 'A', 44, 'Something'}
```

Running the exact same code yields different results!

- Second Run

```console
General Set ( Before Removal ): {None, True, (2+5j), 5.5, 'Something', 44, 'A'}

General Set ( During Removal ): {True, (2+5j), 5.5, 'Something', 44, 'A'}
General Set ( During Removal ): {(2+5j), 5.5, 'Something', 44, 'A'}
General Set ( During Removal ): {5.5, 'Something', 44, 'A'}

General Set ( After Popping ): {5.5, 'Something', 44, 'A'}
```

- Third Run

```console
General Set ( Before Removal ): {'Something', True, None, (2+5j), 5.5, 44, 'A'}

General Set ( During Removal ): {True, None, (2+5j), 5.5, 44, 'A'}
General Set ( During Removal ): {None, (2+5j), 5.5, 44, 'A'}
General Set ( During Removal ): {(2+5j), 5.5, 44, 'A'}

General Set ( After Popping ): {(2+5j), 5.5, 44, 'A'}
```

> [!NOTE]
> **Both** outputs of the set, *before* and *after* changes due to the nature / "*un-orderedness*" of sets as it uses **Hash Tables**.

### Remove Method

In terms of **usage** and **execution**; the `.remove()` method works just as we expect it to work.

Again, with the `.remove()` method, we are going to pass the **actual** *element* as **parameter**.

> Where's the catch?!?

> [!INFO]
> As you know if we try to **remove** an element that does **not** exists in a *list*... The error '*ValueError*' will be raised!
>
> Well, if we try to remove an element that does <span style="color: red;"> not</span> exists from a set. The `.remove()` function will, instead, throw a '*KeyError*'
>
> > That's the only difference between *Sets* and *Lists* with the `.remove()` method!
>

```python
# set containing most data types
general_set: set = {
    44,
    5.5,
    "A",
    "Something",
    True,
    2 + 5j,
    None,
}

# output the general set ( before removal )
print(f"General Set ( Before Removal ): {general_set}\n")

# remove the element 'A' from the set
general_set.remove("A")
print(f"General Set ( During Removal ): {general_set}")

# remove the element 'None' from the set
general_set.remove(None)
print(f"General Set ( During Removal ): {general_set}")

# remove the element '2 + 5j' from the set
general_set.remove(2 + 5j)
print(f"General Set ( During Removal ): {general_set}")

# output the general set ( after removal )
print(f"\nGeneral Set ( After Removal ): {general_set}")
```

Therefore, the output for the above program will be:

```console
General Set ( Before Removal ): {None, True, (2+5j), 5.5, 'A', 44, 'Something'}

General Set ( During Removal ): {None, True, (2+5j), 5.5, 44, 'Something'}
General Set ( During Removal ): {True, (2+5j), 5.5, 44, 'Something'}
General Set ( During Removal ): {True, 5.5, 44, 'Something'}

General Set ( After Removal ): {True, 5.5, 44, 'Something'}
```

> The output for the *before* and *after* ( *insertion-removal* ) will change if we run the code above **multiple** times.

### Discard Method

> Ahh! A new method that we have not looked before!

> [!TIP] Interview, Interview, Interview
> "*Sir ( or Madam ), do you know how to use the `.remove()` method?*"... If **not**, just go fuck yourself with a toothbrush!
>

Well, the discard method is literally the **same** thing as the `.remove()` method.

> [!NOTE] "*What the fuck? No Difference?*"
> Well you see, with the `.discard()` method. When you try to remove that does <span style="color: red;"> not</span> exist in the set... **No errors will be raised**!!!
>
> > The `.discard()` method is like a ninja!
>

> I am just going to copy the same *structure* of the code above

```python
# set containing most data types
general_set: set = {
    44,
    5.5,
    "A",
    "Something",
    True,
    2 + 5j,
    None,
}

# output the general set ( before removal )
print(f"General Set ( Before Removal ): {general_set}\n")

# discard the element 'jezza' from the set
general_set.discard("jezza")
print(f"General Set ( During Discard ): {general_set}")

# discard the element 'its a jaaaaggg' from the set
general_set.discard("its a jaaaaggg")
print(f"General Set ( During Discard ): {general_set}")

# discard the element 'the chicken was still warm' from the set
general_set.discard("the chicken was still warm")
print(f"General Set ( During Discard ): {general_set}")

# output the general set ( after discarding )
print(f"\nGeneral Set ( After Discarding ): {general_set}")
```

In this case, we should **not** raise any '*KeyError*' and we should have the **same** set before the removal of elements:

```console
General Set ( Before Removal ): {None, True, (2+5j), 5.5, 'A', 'Something', 44}

General Set ( During Discard ): {None, True, (2+5j), 5.5, 'A', 'Something', 44}
General Set ( During Discard ): {None, True, (2+5j), 5.5, 'A', 'Something', 44}
General Set ( During Discard ): {None, True, (2+5j), 5.5, 'A', 'Something', 44}

General Set ( After Discarding ): {None, True, (2+5j), 5.5, 'A', 'Something', 44}
```

> As you can, see **no** errors were *raised*!

### Set Comprehension - Removal of Elements

Similarly, we can use the *list comprehension* to **remove** elements from our sets.

```python
# integer set containing some elements
int_set: set[int] = {1, 1, 2, 3, 4, 4, 5}

# output the integer set ( before removal )
print(f"Integer Set ( Before Removal  ): {int_set}")

# remove the all element '1' from the integer set
int_set: set[int] = {element for element in int_set if element != 1}

# output the integer set ( after removal )
print(f"Integer Set ( After Removal  ): {int_set}")
```

We should be able to remove all '1' elements from the set

```console
Integer Set ( Before Removal  ): {1, 2, 3, 4, 5}
Integer Set ( After Removal  ): {2, 3, 4, 5}
```

> [!NOTE]
> Again, the thing about *reassignment* here also applies as I am **not** using different *variable name* for the set.
>
> But if we did used something like [`massive_rat`](https://www.youtube.com/watch?v=7BqLKGJZ9lI) then it would be called '**Removal of Element**'!
>
> For full story / rant, head over to '[[Python - Lists#List Comprehension - Removal of Elements | Python - Lists]]'

## Miscellaneous Methods / Functions

> [!NOTE]
> These *functions* / *method* found below are in not particular order.

### Set Equality and Inequality

> Here comes the *stealing*!

I am just going to copy the code from 'List Equality - Inequality' from our lovely [[Python - Lists#List Equality - Inequality | Python Lists]] note!

```python
# import the 'randint' function from the random module
from random import randint

# integer set containing some elements
int_set: set[int] = {1, 2, 3, 4, 5}
# character set containing some elements
char_set: set[str] = {chr(num) for num in range(65, 70)}


# check if sets are equal to each other

# << integer set > >
print(f"Integer Set Equal? {int_set == {randint(0, 9) for i in range(5)}}")
print(f"Integer Set Equal? {int_set != {num for num in range(5, 0, -1)}}")
print(f"Integer Set Equal? {int_set == {1, 2, 3, 4, 5}} <---\n")

print("-" * 50, "\n")

# << character set > >
print(f"Character Set Equal? {char_set == {randint(0, 9) for i in range(5)}}")
print(f"Character Set Equal? {char_set != {chr(num) for num in range(69, 64, -1)}}")
print(f"Character Set Equal? {char_set == {chr(num) for num in range(65, 70)}} <---")
```

Therefore, we can see that:

```console
Integer Set Equal? False
Integer Set Equal? False
Integer Set Equal? True <---

-------------------------------------------------- 

Character Set Equal? False
Character Set Equal? False
Character Set Equal? True <---
```

> [!NOTE]
> Given that *sets* are **unordered** and contains **no duplicates**; the *second* and *fifth* output will therefore become `False` as they are still **equal**!
>
> > I was initially confused as to why it was becoming `False`!
>

### Copy Method

I mean we have already done this one, therefore we **code**!

```python
# character set containing 5 elements
char_set: set[str] = {chr(num) for num in range(30, 35)}

# create a copy of the set containing the characters
char_set_copy: set[str] = char_set.copy()
```

### Difference Update Method

> [!NOTE]
> I initially thought that placing this *heading* in the 'Removal of Elements' category would make better sense...
>
> But I changed my mind and here we are. But just for this one, we are going to look at `.difference_update()` first and then `.difference()`.
>
> What am saying is that we should have done `.difference()` first and then `.difference_update()`.

Again this is a new method that is **specific** to *sets*.

This method will be able to **remove** elements from the specified set!

> [!INFO]
> With the `.difference_update()` method, we can pass *as many iterables* **as we like**, to our hearts' content.
>
> > And yes, a '*string*' is considered as **iterable** in Python!
>
> > [!NOTE] Additionally,
> > It does behave a little bit like our `.discard()` method as it does **not** raise any '*KeyError*' when an *element* has <span style="color:red"> not</span> been found in the set!
>

```python
# set of integer of random numbers only
int_set: set[int] = {int_num for int_num in range(20)}

# output the integer set ( before removal )
print(f"Integer Set ( Before Removal ): {int_set}")

# remove multiple elements from the set
int_set.difference_update({0, 1, 2}, "something", [19, 18, 17], (9, 10, 11))

# output the integer set ( after removal )
print(f"Integer Set ( After Removal ): {int_set}")
```

This is the output that we should get for the above code block:

```console
Integer Set ( Before Removal ): {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19}
Integer Set ( After Removal ): {3, 4, 5, 6, 7, 8, 12, 13, 14, 15, 16}
```

#### Using the `-=` Operator

> Basically, `.difference_update()` **equals** to `-=`!

> [!INFO] Again things to consider!
> - Our *iterable* should be of type `set()`
> - To add multiple *iterables* at the same time just *pipe* `|` it

We are going to use the same code found above and we are going to instead use `-=` instead of `.difference_update()`

```python
# set of integer of random numbers only
int_set: set[int] = {int_num for int_num in range(20)}

# output the integer set ( before removal )
print(f"Integer Set ( Before Removal ): {int_set}")

# remove multiple elements from the set
int_set -= {0, 1, 2} | set("something") | set([19, 18, 17]) | set((9, 10, 11))

# output the integer set ( after removal )
print(f"Integer Set ( After Removal ): {int_set}")
```

Therefore, we should get  the same output ( *in this case* ):

```console
Integer Set ( Before Removal ): {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19}
Integer Set ( After Removal ): {3, 4, 5, 6, 7, 8, 12, 13, 14, 15, 16}
```

### Difference Method

> "*Its like removal of element but not really because its 'Sets Difference'.*
> *Leave uncommon in place...*"

Given that we know that the `.difference_update()` method will **remove** elements found inside a specific set.

> "*But what does `.difference()` do then*?" You ask!

Its basically the **same** thing in terms of *working* but this time... Its going to create **another** set and **keep** the *original* **intact**!

> [!INFO]
> Additionally, the `.difference()` method can **multiple** *elements* as **parameters** and these "*elements*" can **should** be an *iterable*!

```python
# set containing most data types
general_set: set = {
    44,
    5.5,
    "A",
    "Something",
    True,
    2 + 5j,
    None,
}

# empty set
general_set_update: set = set()

# output the general set ( before removal )
print(f"General Set ( Before Removal ): {general_set}")
# output the general set "updated" ( before insertion )
print(f"Updated General Set ( Before Insertion ): {general_set_update}")

# updated should only contain the element '44'
general_set_update = general_set.difference(
    "Not Found", [5.5, "A"], ("Something", True), {2 + 5j, None}
)

# output the general set ( after removal )
print(f"\nGeneral Set ( After Removal ): {general_set}")
# output the general set ( after insertion )
print(f"General Set Update ( After Insertion ): {general_set_update}")
```

Therefore, the above program should return us with:

```console
General Set ( Before Removal ): {None, 'A', True, (2+5j), 5.5, 'Something', 44}
Updated General Set ( Before Insertion ): set()

General Set ( After Removal ): {None, 'A', True, (2+5j), 5.5, 'Something', 44}
General Set Update ( After Insertion ): {44}
```

> [!INFO]
> As you can see, it behave in the **exact same** way ( *just that it acts on other sets* ) as `.difference_update()`. Where it will **not** raise any '*KeyError*' when the *element* trying to be removed does <span style="color: red;"> not</span> exist in the set!

#### Using the `-` Operator

> [!INFO] Again, things to keep in mind
> - Our *iterable* should be of type `set()`
> - To add multiple *iterables* at the same time just continue to use `-`
>
> > [!WARNING]
> > You should be careful, where you place the `-` character.
> >
> > > It does <span style="color: red;"> not</span> follow the  [Associative](https://www.onlinemath4all.com/associative-property-of-sets.html) Law!
> >
> > As $A - ( B - C ) \neq A - ( B - C )$
>

Mimicking the above code, we should get something that looks like this:

```python
# set containing most data types
general_set: set = {
    44,
    5.5,
    "A",
    "Something",
    True,
    2 + 5j,
    None,
}

# empty set
general_set_update: set = set()

# output the general set ( before removal )
print(f"General Set ( Before Removal ): {general_set}")
# output the general set "updated" ( before insertion )
print(f"Updated General Set ( Before Insertion ): {general_set_update}")

# updated should only contain the element '44'
general_set_update = (
    general_set
    - set("Not Found")
    - set([5.5, "A"])
    - set(("Something", True))
    - {2 + 5j, None}
)

# output the general set ( after removal )
print(f"\nGeneral Set ( After Removal ): {general_set}")
# output the general set ( after insertion )
print(f"General Set Update ( After Insertion ): {general_set_update}")
```

The output should be the **same** thing as above:

```console
General Set ( Before Removal ): {None, True, (2+5j), 5.5, 'Something', 'A', 44}
Updated General Set ( Before Insertion ): set()

General Set ( After Removal ): {None, True, (2+5j), 5.5, 'Something', 'A', 44}
General Set Update ( After Insertion ): {44}
```

> [!INFO]
> In the code above, I did *declare* the set `general_set_update` so that I can show you that is was **empty** at the beginning.
>
> Obviously, we don't need to do that as Python does **not** have any declaration ( *obviously* ).

### Intersection Method

> "*Do you know you maths, son*?"

If so, then this is really simple. But if you don't know what the *fuck* does **intersection** of a set means. You can stay.

> [!TIP] Intersection Explanation
> Its just takes the **common** value!
>
> > Back to our regular schedule, Yeeaahhhh!
>

> [!INFO]
> Similarly, the `.intersection()` method can have **multiple** *elements* as **parameters** and these "*elements*" can **should** be an *iterable*!
>
> > [!NOTE]
> > Additionally, it **creates** a new set instead of *modifying* ( *reassigning* ) the set itself.

> I don't think that its appropriate to output *aesthetically* here!

```python
# set of characters containing some elements
char_set: set[str] = {"A", "B", "C", "D", "E"}

# set of integer of random numbers only
int_set: set[int] = {int_num for int_num in range(20)}

# find the intersection of some elements with the `char_set` set
# NOTE: in this case, we want to have 'A' and 'B'
# therefore, we need to have 'A' and 'B' present ( all places )
char_result_1 = char_set.intersection({"B", "y", "A"}, ["A", "B", "Q"], ("A", "X", "B"))

# find the intersection of some elements with the `int_set` set
# NOTE: in this case, want to have '1', '2', '3'
# therefore, we need to have '1', '2' and '3' present ( all places )
int_result_1 = int_set.intersection(
    {1, 2, 3, 4, 5},
    [2, 5, 3, 1, 11, 17],
    ("not found", 2, 3, 1),
)

# display the intersection for `char_result_1`
print(f"First Intersection ( `char_result_1` ): {char_result_1}")
# display the intersection for `int_result_1`
print(f"First Intersection ( `int_result_1` ): {int_result_1}")

# find the intersection of some elements with the `char_result_1` set
# NOTE: in this case, we only want 'A'
# therefore, we need to have 'A' present ( all places )
char_result_2 = char_result_1.intersection(
    {"A", "found", "B"}, [1, "A", 5], ("E", "A", 3)
)

# find the intersection of some elements with the `int_result_1` set
# NOTE: in this case, we only want '1'
# therefore, we need to have '1' present ( all places )
int_result_2 = int_result_1.intersection(
    {1, 19, "really"}, ["fine", 0, 1], (1, 200, "some")
)

# display the intersection for `char_result_2`
print(f"Second Intersection ( `char_result_2` ): {char_result_2}")
# display the intersection for `int_result_2`
print(f"Second Intersection ( `int_result_2` ): {int_result_2}")
```

Therefore, we should have get the intersection of these sets.

```console
First Intersection ( `char_result_1` ): {'A', 'B'}
First Intersection ( `int_result_1` ): {1, 2, 3}
Second Intersection ( `char_result_2` ): {'A'}
Second Intersection ( `int_result_2` ): {1}
```

> [!WARNING] Learning
> So as you can see, we passed multiple *iterables* as parameter inside the `.intersection()` method.
>
> Given that *intersections* of sets are **associative** meaning that we can have these:
>
> $( A \cap B \cap C ) = ((A \cap B) \cap C ) = (A \cap (B \cap C)) = ((A \cap C) \cap B)$
>
> Well, I first wrote this code ( *showing you only for `char_result_1` as I did the same logic with others* ):
>
> ```python
> char_result_1 = char_set.intersection(
> 	{1, "y", 0}, ["D", 6.9, "Q"], ("E", "X", "Z")
> )
> ```
>
> I just thought that its going to *take* whatever it finds... For example in the *list* we have 'D' and in the *tuple* we have 'E'.
> Therefore, I thought that its going to populate `char_result_1` with `{'E', 'D'}` ( *order does not matter* ).
>
> But instead I got `set()`?!?
>
> > [!NOTE]
> > Therefore that **associative** law does apply here whereby we <strong> <span style="color: red;"> need</span> </strong> to have the **elements** present in **all** the *iterables* that we passed in as **parameters**.
>
> Therefore, we would get the desired output like in the above output!

#### Using the `&` Operator

> [!INFO] A few things to consider!
> - Our *iterable* should be of type `set()`
> - To add multiple *iterables* at the same time just continue to use `&`

Therefore, if we try to mimic the above code, we should get something that looks like this:

```python
# set of characters containing some elements
char_set: set[str] = {"A", "B", "C", "D", "E"}

# set of integer of random numbers only
int_set: set[int] = {int_num for int_num in range(20)}

# find the intersection of some elements with the `char_set` set
char_result_1 = char_set & {"B", "y", "A"} & set(["A", "B", "Q"]) & set(("A", "X", "B"))

# find the intersection of some elements with the `int_set` set
int_result_1 = (
    int_set & {1, 2, 3, 4, 5} & set([2, 5, 3, 1, 11, 17]) & set(("not found", 2, 3, 1))
)

# display the intersection for `char_result_1`
print(f"First Intersection ( `char_result_1` ): {char_result_1}")
# display the intersection for `int_result_1`
print(f"First Intersection ( `int_result_1` ): {int_result_1}")

# find the intersection of some elements with the `char_result_1` set
char_result_2 = (
    char_result_1 & {"A", "found", "B"} & set([1, "A", 5]) & set(("E", "A", 3))
)

# find the intersection of some elements with the `int_result_1` set
int_result_2 = (
    int_result_1 & {1, 19, "really"} & set(["fine", 0, 1]) & set((1, 200, "some"))
)

# display the intersection for `char_result_2`
print(f"Second Intersection ( `char_result_2` ): {char_result_2}")
# display the intersection for `int_result_2`
print(f"Second Intersection ( `int_result_2` ): {int_result_2}")
```

We should have the **same** *elements* at the end:

```console
First Intersection ( `char_result_1` ): {'A', 'B'}
First Intersection ( `int_result_1` ): {1, 2, 3}
Second Intersection ( `char_result_2` ): {'A'}
Second Intersection ( `int_result_2` ): {1}
```

### Intersection Update Method

> I think you know where we are getting to with this!

Compared to `.intersection()` whereby we needed to create **other** sets and it did **not** touch the original set. In this case, the `.intersection_update()` is going to actually *modify* the **original** set instead of creating new ones.

```python
# set of characters containing some elements
char_set: set[str] = {"A", "B", "C", "D", "E"}

# set of integer of random numbers only
int_set: set[int] = {int_num for int_num in range(20)}

# find the intersection of some elements with the `char_set` set
# NOTE: in this case, we want to have 'A' and 'B'
# therefore, we need to have 'A' and 'B' present ( all places )
char_set.intersection_update({"B", "y", "A"}, ["A", "B", "Q"], ("A", "X", "B"))

# find the intersection of some elements with the `int_set` set
# NOTE: in this case, want to have '1', '2', '3'
# therefore, we need to have '1', '2' and '3' present ( all places )
int_set.intersection_update(
    {1, 2, 3, 4, 5},
    [2, 5, 3, 1, 11, 17],
    ("not found", 2, 3, 1),
)

# display output for the first intersection
print(f"First Intersection: {char_set}")
# display output for the first intersection
print(f"First Intersection: {int_set}")

# find the intersection of some elements with the `char_result_1` set
# NOTE: in this case, we only want 'A'
# therefore, we need to have 'A' present ( all places )
char_set.intersection_update({"A", "found", "B"}, [1, "A", 5], ("E", "A", 3))

# find the intersection of some elements with the `int_result_1` set
# NOTE: in this case, we only want '1'
# therefore, we need to have '1' present ( all places )
int_set.intersection_update({1, 19, "really"}, ["fine", 0, 1], (1, 200, "some"))

# display output for the second intersection
print(f"Second Intersection: {char_set}")
# display output for the second intersection
print(f"Second Intersection: {int_set}")
```

This should be output of the above program code:

```console
First Intersection: {'A', 'B'}
First Intersection: {1, 2, 3}
Second Intersection: {'A'}
Second Intersection: {1}
```

> Therefore, instead of **making** other sets... We just change this one itself!

#### Using the `&=` Operator

> [!INFO] A few things to consider!
> - Our *iterable* should be of type `set()`
> - To add multiple *iterables* at the same time just continue to use `&` but **remember** to *start* with `&=` to indicate to Python that this is `.intersection_update()`.

```python
# set of characters containing some elements
char_set: set[str] = {"A", "B", "C", "D", "E"}

# set of integer of random numbers only
int_set: set[int] = {int_num for int_num in range(20)}

# find the intersection of some elements with the `char_set` set
# NOTE: in this case, we want to have 'A' and 'B'
# therefore, we need to have 'A' and 'B' present ( all places )
char_set &= {"B", "y", "A"} & set(["A", "B", "Q"]) & set(("A", "X", "B"))

# find the intersection of some elements with the `int_set` set
# NOTE: in this case, want to have '1', '2', '3'
# therefore, we need to have '1', '2' and '3' present ( all places )
int_set &= {1, 2, 3, 4, 5} & set([2, 5, 3, 1, 11, 17]) & set(("not found", 2, 3, 1))

# display output for the first intersection
print(f"First Intersection: {char_set}")
# display output for the first intersection
print(f"First Intersection: {int_set}")

# find the intersection of some elements with the `char_result_1` set
# NOTE: in this case, we only want 'A'
# therefore, we need to have 'A' present ( all places )
char_set &= {"A", "found", "B"} & set([1, "A", 5]) & set(("E", "A", 3))

# find the intersection of some elements with the `int_result_1` set
# NOTE: in this case, we only want '1'
# therefore, we need to have '1' present ( all places )
int_set &= {1, 19, "really"} & set(["fine", 0, 1]) & set((1, 200, "some"))

# display output for the second intersection
print(f"Second Intersection: {char_set}")
# display output for the second intersection
print(f"Second Intersection: {int_set}")
```

So we should have the *same* output in this case:

```console
First Intersection: {'A', 'B'}
First Intersection: {1, 2, 3}
Second Intersection: {'A'}
Second Intersection: {1}
```

### Disjoint Method

> I know that the "*heading name*" looks trash!

> [!TIP] What is a **Disjoint** Set?
> These [pesky](https://www.youtube.com/watch?v=6mcgCxAe2Cg) Disjoint Sets are also called **non-intersecting** sets as... Well, they **don't** fucking *intersects*!
>
> Long story short, the **don't** contain the **same** elements found in each sets.
>
> > In terms of a Venn Diagram, they are completely "*disjoint*" ( *hihi, they are "spreaded" far apart* )
> >
> > "*That's what I say to here in bed*"!
>

> [!INFO]
> Compared to all of the other *method* above whereby they can take **other** types of data likes *lists*, *tuples* and *strings* **simultaneously**.
>
> The `.isdisjoint()` method can take these "*other*" types of data but we can *only* pass a **single** data item at a time.

```python
# set of characters containing some elements
char_set: set[str] = {"A", "B", "C", "D", "E"}

# set of integer of random numbers only
int_set: set[int] = {int_num for int_num in range(20)}

# find if the `char_set` is disjointed from the set passed in as argument
print(f"Character Set Disjoint? {char_set.isdisjoint(['F', 'G', 'H', 'I', 'J'])}")
print(f"Character Set Disjoint? {char_set.isdisjoint((1, 2, 3, 4, 5))}")
print(f"Character Set Disjoint? {char_set.isdisjoint({'A', 'B', 'C', 'D', 'E'})} <---")

print("\n" + "-" * 50, "\n")

# find if the `int_set` is disjointed from the set passed in as argument
print(f"Integer Set Disjoint? {int_set.isdisjoint([num for num in range(20, 31)])}")
print(f"Integer Set Disjoint? {int_set.isdisjoint(('A', 'B', 'C', 'D', 'E'))}")
print(f"Integer Set Disjoint? {int_set.isdisjoint({1, 2, 3, 4, 5})} <---")
```

Therefore, our output should be like so:

```console
Character Set Disjoint? True
Character Set Disjoint? True
Character Set Disjoint? False <---

-------------------------------------------------- 

Integer Set Disjoint? True
Integer Set Disjoint? True
Integer Set Disjoint? False <---
```

> [!NOTE] No Operators for `isdisjoint()` :(
> There are **no** shortcut operators for the `isdisjoint()` function.
>
> Therefore, we have completed the *method* `isdisjoint()`!
>
> > "*Or have we*?"
>

#### Intersection Operator `&` As The `isdisjoint()` Operator

My brain when <span style="color: yellow;"> :BoBxsBulb:</span> when I ( *just recently, like about 5 minutes ago* ) learned that Disjoint Sets are also known as "**non-intersecting**" sets!

Therefore, my 2 brains cells that are alive, thought of 2 things:

- `if` statement
- `&` of 2 sets

```python
# function to replicate the `isdisjoint` method with '&' operator
def disjointed_set(main_set: set, comparing_set: set):
    # if both sets intersects ==> not disjointed
    if main_set & comparing_set:
        # output boolean value of 'False' like the method
        return False
    # if sets does NOT intersects ==> disjointed
    else:
        # output boolean value of 'True' like the method
        return True
```

> [!INFO] Again, We should keep this in mind
> - Our *iterable* should be of type `set()`

##### Therefore,

Mimicking the same code found above with *our* function!

```python
# set of characters containing some elements
char_set: set[str] = {"A", "B", "C", "D", "E"}

# set of integer of random numbers only
int_set: set[int] = {int_num for int_num in range(20)}

# find if the `char_set` is disjointed from the set passed in as argument
print(
    f"Character Set Disjoint? {disjointed_set(char_set, set(['F', 'G', 'H', 'I', 'J']))}"
)
print(f"Character Set Disjoint? {disjointed_set(char_set, set((1, 2, 3, 4, 5)))}")
print(
    f"Character Set Disjoint? {disjointed_set(char_set, {'A', 'B', 'C', 'D', 'E'})} <---"
)

print("\n" + "-" * 50, "\n")

# find if the `int_set` is disjointed from the set passed in as argument
print(
    f"Integer Set Disjoint? {disjointed_set(int_set, set([num for num in range(20, 31)]))}"
)
print(
    f"Integer Set Disjoint? {disjointed_set(int_set, set(('A', 'B', 'C', 'D', 'E')))}"
)
print(f"Integer Set Disjoint? {disjointed_set(int_set, {1, 2, 3, 4, 5})} <---")
```

> Remember to **include** the function `disjointed_set()` to be able to run the code above in your IDE.
> "*I use VIM BTW*!"

We should get the same output!

```console
Character Set Disjoint? True
Character Set Disjoint? True
Character Set Disjoint? False <---

-------------------------------------------------- 

Integer Set Disjoint? True
Integer Set Disjoint? True
Integer Set Disjoint? False <---
```

#### Improving My Disjoint Function

```python
# updated function that accepts multiple parameters
# whereby these parameters can either be lists, tuples or sets
def disjointed_set_updated(*args: list | tuple | set) -> bool:
    # check if the number of arguments passed is either '0' or '1'
    if len(args) > = 0 and len(args) <= 1:
        # '0' arguments passed ==> we are not comparing with anything
        # '1' argument passed ==> argument has nothing to be compared with
        return True

    # iterate through the "arguments" passed in
    # INFO: doing some pair comparision
    for i in range(len(args) - 1):
        # again, compare the first argument to the second one and so on
        for j in range(i + 1, len(args)):
            # convert the arguments at each position into sets
            if set(args[i]) & set(args[j]):
                # meaning intersection happens ==> set being compared are NOT disjointed
                return False

    # after all comparision no intersection has been found ==> all arguments are disjointed
    return True

```

##### Hence,

> Just a little example for you to *taste*!

```python

print(f"Output of Disjointed Set: {disjointed_set_updated()}")
print(f"Output of Disjointed Set: {disjointed_set_updated({1, 2, 3, 4})}")
print(f"Output of Disjointed Set: {disjointed_set_updated({1, 2, 3, 4}, [5, 6, 7, 8])}")
print(
    f"Output of Disjointed Set: {disjointed_set_updated({1, 2, 3, 4}, [5, 6, 7, 8], (1, 2, 3, 4))} <---"
)
print(
    f"Output of Disjointed Set: {disjointed_set_updated({1, 2, 3, 4}, {1, 2, 3, 4})} <---"
)
```

In this case, we should be able to correctly identify the "*disjointed*" set!

```console
Output of Disjointed Set: True
Output of Disjointed Set: True
Output of Disjointed Set: True
Output of Disjointed Set: False <---
Output of Disjointed Set: False <---
```

> [!SUCCESS]
> We fucking did it boys!!!
>
> > [!INFO] I am getting emotional...
> > This is the very first time that I use and implemented `*args` **without watching** any specific Python Video or **reading** something like [stackoverflow](https://stackoverflow.com).
> >
> > > I just simply found it *logical* by just looking the at [official documentation](https://docs.python.org)!
> >
>

---

> I think the explanation should go together for '*Subsets*' and '*Supersets*'!

### Subset and Superset Explanation

> This one is going to be really simple in terms of explanation and code running!

> [!TIP] What is a 'Superset' or 'Subset'?
> Picture a Venn Diagram with one "*circle*" **inside** another "*circle*". In short, we have a *set* inside another *set*!
>
> > I think of it in this way!
>
> This means that the set **inside** does *not* really know about the other *set* <strong> <span style="color: orange;"> but</span> </strong> the **outer** set knows about that **inner** set.
>
> Hence, the **outer** set is the '*Superset*' and the **inner** set is called the '*Subset*'.
>
> In terms of Mathematics, given:
>
> $A = \{1, 2, 3, 4, 5\}$
> $B = \{2, 3, 4\}$
>
> Therefore, we are going to have:
>
> 1. $B \subseteq A \} \Rightarrow$ $B$ is a **subset** of $A$
> 2. $A \supseteq B \Rightarrow$ $A$ is a **superset** of $B$
>
> > In this case $B$ is also a proper **subset** ( *$\subset$* ) $A$ and $A$ is a proper **superset** ( *$\supseteq$* ) of $B$; as $A$ and $B$ are <span style="color: red;"> not</span> **equal**.

---

### Subset Method

> [!INFO]
> > I will need to write this for `.issubset()`.
>
> > [!TIP] Usage
> > Here is how the subset *method* is supposed to use:
> >
> > ```python
> > inner_set.issubset(outer_set)
> > ```
> >
> > > We **always** pass in the `outer_set` as a **parameter**.
>
> Similar to our `.isdisjoint()` *method*; the `.issubset()` method can *only* handle a **single** argument at a time.

```python
# set of integer containing some elements
inner_int_set: set[int] = {1, 2, 3}

# in this case, we want to show that our `inner_int_set`
# is a subset of other "outer" sets
print(
    f"Inner Integer Set a Subset of '[1, 2, 3, 4, 5]'?: {inner_int_set.issubset([1, 2, 3, 4, 5])}"
)
print(
    f"Inner Integer Set a Subset of '(2, 3, 1)'?: {inner_int_set.issubset((2, 3, 1))}"
)
print(
    "Inner Integer Set a Subset of '{5, 4, 3, 2, 1}'?: "
    + str(inner_int_set.issubset({5, 4, 3, 2, 1}))
)

print("\n" + "-" * 50, "\n")

# in this case, we want to show that our `inner_int_set`
# is NOT a subset of other "outer" sets
print(
    f"Inner Integer Set a Subset of '[5, 6, 7, 8, 9]'?: {inner_int_set.issubset([5, 6, 7, 8, 9])}"
)
print(f"Inner Integer Set a Subset of '(1, 2)'?: {inner_int_set.issubset((1, 2))}")
print(
    "Inner Integer Set a Subset of '{4, 69.69, 1}'?: "
    + str(inner_int_set.issubset({4, 69.69, 1}))
)
```

Therefore, we should happily have this:

```console
Inner Integer Set a Subset of '[1, 2, 3, 4, 5]'?: True
Inner Integer Set a Subset of '(2, 3, 1)'?: True
Inner Integer Set a Subset of '{5, 4, 3, 2, 1}'?: True

-------------------------------------------------- 

Inner Integer Set a Subset of '[5, 6, 7, 8, 9]'?: False
Inner Integer Set a Subset of '(1, 2)'?: False
Inner Integer Set a Subset of '{4, 69.69, 1}'?: False
```

#### Using the `<=` And `<` Operator

##### Difference Between `<=` and `<`

> [!TIP] Meaning of `<=`
> It checks whether one iterable object on the **left** side is a *subset* of another iterable on the **right** side.
>
> > Like we said: `inner_set.issubset(outer_set)`!
>

> [!TIP] Meaning of `<`
> It does the **same** exact operations as `<=` but it also checks for if the subset is a "*proper*" subset.
>
> This means that:
>
> 1. All *elements* in *first* set are **in** *second* set
> 2. *Second* set has *at least* **one** more element
> 3. *Identical* sets are **not** allowed

> [!WARNING]
> <p align="center"> Sets <code> &lt;=</code> or <code> &lt;</code> Sets = Subset</p>
> <p align="center"> Integers <code> &lt;=</code> or <code> &lt;</code> Integers = Comparison</p>

In terms of usage, its the same thing whereby the `inner_set` is on the **left hand side** and the `outer_set` is on the **right hand side**.

> [!INFO] Again, things to keep inside the mind!
> - Our *iterable* should be of type `set()`

```python
# set of integer containing some elements
inner_int_set: set[int] = {1, 2, 3}

# in this case, we want to show that our `inner_int_set`
# is a subset of other "outer" sets
print(
    f"Inner Integer Set a Subset of '[1, 2, 3, 4, 5]'?: {inner_int_set <= set([1, 2, 3, 4, 5])}"
)
print(f"Inner Integer Set a Subset of '(2, 3, 1)'?: {inner_int_set <= set((2, 3, 1))}")
print(
    "Inner Integer Set a Subset of '{5, 6}'?: " + str(inner_int_set <= {5, 6}) + " <---"
)

print("\n" + "-" * 50, "\n")

# in this case, we want to show that our `inner_int_set`
# is a "proper" subset of other "outer" sets
print(
    f"Inner Integer Set a 'Proper' Subset of '[5, 4, 3, 2, 1]'?: {inner_int_set < set([5, 4, 3, 2, 1])}"
)
print(
    f"Inner Integer Set a 'Proper' Subset of '(1, 2 , 3, 4, 5, 6, 7)'?: {inner_int_set < set((1, 2, 3, 4, 5, 6, 7))}"
)
print(
    "Inner Integer Set a 'Proper' Subset of '{1, 2, 3}'?: "
    + str(inner_int_set < {1, 2, 3})
    + " <---"
)
```

```console
Inner Integer Set a Subset of '[1, 2, 3, 4, 5]'?: True
Inner Integer Set a Subset of '(2, 3, 1)'?: True
Inner Integer Set a Subset of '{5, 6}'?: False <---

-------------------------------------------------- 

Inner Integer Set a 'Proper' Subset of '[5, 4, 3, 2, 1]'?: True
Inner Integer Set a 'Proper' Subset of '(1, 2 , 3, 4, 5, 6, 7)'?: True
Inner Integer Set a 'Proper' Subset of '{1, 2, 3}'?: False <---
```

### Superset Method

From the "*cOmpHrenSive*" explanation and the knowledge ( *because I still don't quite understand them* ) gain with the `.issubset()` method. We can simply **reverse** the "*sentences*".

> Nevertheless, I will still write this down

> [!TIP] Using The `.issuperset()` Method
> Here is how the super-set *method* is supposed to be used:
>
> ```python
> outer_set.issuperset(inner_set)
> ```
>
> > We **always** pass in the `inner_set` as a **parameter**
>

> As you can see, its the **opposite** of `.issubset()`!

```python
# set of integer containing some elements
outer_int_set: set[int] = {1, 2, 3, 4, 5, 6, 7, 8}

# in this case, we want to show that our `outer_int_set`
# is a super-set of other "inner" sets
print(
    f"Outer Integer Set a Super Set of '[1, 2, 3, 4, 5]'?: {outer_int_set.issuperset([1, 2, 3, 4, 5])}"
)
print(
    f"Outer Integer Set a Super Set of '(2, 3, 1)'?: {outer_int_set.issuperset((2, 3, 1))}"
)
print(
    "Outer Integer Set a Super Set of '{5, 4, 3, 2, 1}'?: "
    + str(outer_int_set.issuperset({5, 4, 3, 2, 1}))
)

print("\n" + "-" * 50, "\n")

# in this case, we want to show that our `outer_int_set`
# is NOT a super-set of other "inner" sets
print(
    f"Outer Integer Set a Super Set of '[5, 6, 7, 8, 9]'?: {outer_int_set.issuperset([5, 6, 7, 8, 9])}"
)
print(
    f"Outer Integer Set a Super Set of '(0, -1, -2)'?: {outer_int_set.issuperset((0, -1, -2))}"
)
print(
    "Outer Integer Set a Super Set of '{4, 69.69, 1}'?: "
    + str(outer_int_set.issuperset({4, 69.69, 1}))
)
```

```console
Outer Integer Set a Super Set of '[1, 2, 3, 4, 5]'?: True
Outer Integer Set a Super Set of '(2, 3, 1)'?: True
Outer Integer Set a Super Set of '{5, 4, 3, 2, 1}'?: True

-------------------------------------------------- 

Outer Integer Set a Super Set of '[5, 6, 7, 8, 9]'?: False
Outer Integer Set a Super Set of '(0, -1, -2)'?: False
Outer Integer Set a Super Set of '{4, 69.69, 1}'?: False
```

#### Using the `> =` And `> ` Operator

##### Difference Between `> =` and `> `

> [!TIP] Meaning of `> =`
> It checks whether one iterable object on the **left** side is a *super-set* of another iterable on the **right** side.
>
> > Like we said: `outer_set.issuperset(inner_set)`
>

> [!TIP] Meaning of `> `
> It does the **same** exact operations as `> =` but it also checks for if the the super-set is a "*proper*" super-set.
>
> This means that:
>
> 1. All *elements* of the *second* set are **in** the *first* set
> 2. *First* set has *at least* **one** more element
> 3. *Identical* sets are **not** allowed

> [!WARNING] Again!
> <p align="center"> Sets <code> &gt;=</code> or <code> &gt;</code> Sets = Subset</p>
> <p align="center"> Integers <code> &gt;=</code> or <code> &gt;</code> Integers = Comparison</p>

In terms of usage, its the same thing whereby the `outer_set` is on the **left hand side** and the `inner_set` is on the **right hand side**.

> [!INFO] Again, things to keep inside the mind!
> - Our *iterable* should be of type `set()`

```python
# set of integer containing some elements
outer_int_set: set[int] = {1, 2, 3, 4, 5, 6, 7, 8}

# in this case, we want to show that our `outer_int_set`
# is a super-set of other "inner" sets
print(
    f"Outer Integer Set a Super Set of '[1, 2, 3, 4, 5]'?: {outer_int_set > = set([1, 2, 3, 4, 5])}"
)
print(
    f"Outer Integer Set a Super Set of '(2, 3, 1)'?: {outer_int_set > = set((2, 3, 1))}"
)
print(
    "Outer Integer Set a Super Set of '{10, 11, 12, 13, 14, 15}'?: "
    + str(outer_int_set.issuperset({10, 11, 12, 13, 14, 15}))
    + " <---"
)

print("\n" + "-" * 50, "\n")

# in this case, we want to show that our `outer_int_set`
# is a "proper" super-set of other "inner" sets
print(
    f"Outer Integer Set a 'Proper' Super Set of '[8, 7, 6, 5]'?: {outer_int_set > set([8, 7, 6, 5])}"
)
print(
    f"Outer Integer Set a 'Proper' Super Set of '(0, -1, -2)'?: {outer_int_set > set((1, 2, 3, 4, 5))}"
)
print(
    "Outer Integer Set a 'Proper' Super Set of '{4, 69.69, 1}'?: "
    + str(outer_int_set.issuperset({1, 2, 3, 4, 5, 6, 7, 8, 9, 0}))
    + " <---"
)
```

```console
Outer Integer Set a Super Set of '[1, 2, 3, 4, 5]'?: True
Outer Integer Set a Super Set of '(2, 3, 1)'?: True
Outer Integer Set a Super Set of '{10, 11, 12, 13, 14, 15}'?: False <---

-------------------------------------------------- 

Outer Integer Set a 'Proper' Super Set of '[8, 7, 6, 5]'?: True
Outer Integer Set a 'Proper' Super Set of '(0, -1, -2)'?: True
Outer Integer Set a 'Proper' Super Set of '{4, 69.69, 1}'?: False <---
```

> [!TIP] Tips, Tips, Tits, Tips and Tips
> - The `.issubset()` *method* is the **same** as the `<=`
> - The `.ssuperset()` *method* is the **same** as the `> =`

### Symmetric Difference Method

> [!NOTE]
> Given that I have never heard of '*Symmetric Difference*', I am going to learn it right here and right now!
>
> > I mean, I could have known it in the past but...
>

> [!TIP] What is Symmetric Difference?
> As per the [Wikipedia](https://en.wikipedia.org/wiki/Symmetric_difference) the *symmetric difference* of two sets is equivalent to the **union** of *both* **relative complements**.
>
> This mean that we are going to have:
>
> $$A \oplus B = ( A - B ) \cup ( B - A )$$

Therefore, in terms of actual *sets with numbers*:

Let's say that you have 2 sets, $A$ and $B$, whereby:

- $A = \{1, 2, 3, 4, 5, 6, 7, 8\}$
- $B = \{1, 3, 5, 6, 7, 8, 9\}$

Therefore, the *Symmetric Difference* will be calculated as follows:

1. $( A - B ) = \{2, 4\}$
2. $( B - A ) = \{9\}$
3. $( A - B ) \cup ( B - A ) = \{2, 4\} \cup \{9\}$
4. $\therefore A \oplus B = \{2, 4, 9\} \leftarrow$

If you do that in Python, we should get the **same** answer as above:

> Writing in the Python Interpreter directly!

Here, I am just going the `^` operator:

```python
> > > {1, 2, 3, 4, 5, 6, 7, 8} ^ {1, 3, 5, 6, 7, 8, 9}
{2, 4, 9}
```

But as you can see, we do get literally the **same** answer.

> [!SUCCESS] Well, Let's Get Started

> [!INFO]
> Similar to our favourite `.isdisjoint()`, `.issubset()` and `.issuperset()` *methods*. The `.symmetric_difference()` will *only* accept a **single** data item as **parameter** at a time.
>
> Additionally, we can pass other iterables like *list*, *tuples*.

```python
# set of integer containing some elements
int_set: set[int] = {1, 2, 3}

# performing some "symmetric difference" on some sets
print(f"Symmetric Difference with [1, 4, 5]: {int_set.symmetric_difference([1, 4, 5])}")
print(f"Symmetric Difference with (3, 5, 6): {int_set.symmetric_difference((3, 5, 6))}")
print(
    "Symmetric Difference with {1, 2, 5, 7, 9}: "
    + str(int_set.symmetric_difference({2, 5, 7, 1, 9}))
)
```

Hence, we should get an output that looks like this:

```console
Symmetric Difference with [1, 4, 5]: {2, 3, 4, 5}
Symmetric Difference with (3, 5, 6): {1, 2, 5, 6}
Symmetric Difference with {1, 2, 5, 7, 9}: {3, 5, 7, 9}
```

> [!NOTE] From What I Can See!
>
> <p align="center"> <span style="color: #8ebd6b;"> You Just Take All <strong> Common</strong> Out!</span> </p>

#### Using the `^` Operator

> [!INFO] Again, things to keep in mind
> - Our *iterable* should be of type `set()`
> - To add multiple *iterables* at the same time just continue to use `^`
>
> > Yes compared `.symmetric_difference()` *method*, We can "**chain**" multiple sets!

```python
# set of integer containing some elements
int_set: set[int] = {1, 2, 3, 5}

# performing some "symmetric difference" on some sets
print(
    f"Symmetric Difference: {int_set ^ set([1, 4, 5]) ^ set((3, 5, 6)) ^ {1, 2, 5, 7, 9}}"
)
```

Hence, we should get an output that looks like this:

```console
Symmetric Difference: {1, 4, 6, 7, 9}
```

### Symmetric Difference Update Method

> Does it need an introduction?

Well, similar to the *difference* between the `.difference()` and `.difference_update()` or `.intersection()` and `.intersection_update()`.

Thus, in this case, the *first* set is going to get modified.

```python
# set of integer containing some elements
int_set: set[int] = {1, 2, 3, 5}

# output the integer set ( before symmetric difference )
print(f"Integer Set ( Before Symmetric Difference ): {int_set}")

# performing some "symmetric difference" on some sets
int_set.symmetric_difference_update([1, 4, 5])
int_set.symmetric_difference_update((3, 5, 6))
int_set.symmetric_difference_update({1, 2, 5, 7, 9})

# output the integer set ( after symmetric difference )
print(f"Integer Set ( After Symmetric Difference ): {int_set}")
```

Hence, we should get and updated set:

```console
Integer Set ( Before Symmetric Difference ): {1, 2, 3, 5}
Integer Set ( After Symmetric Difference ): {1, 4, 6, 7, 9}
```

#### Using `^=` Operator

> [!INFO] Again, things to keep in mind
> - Our *iterable* should be of type `set()`
> - To add multiple *iterables* at the same time just continue to use `^`

Mimicking our code above, we should therefore have this.

```python
# set of integer containing some elements
int_set: set[int] = {1, 2, 3, 5}

# output the integer set ( before symmetric difference )
print(f"Integer Set ( Before Symmetric Difference ): {int_set}")

# performing some "symmetric difference" on some sets
int_set ^= set([1, 4, 5]) ^ set((3, 5, 6)) ^ {1, 2, 5, 7, 9}

# output the integer set ( after symmetric difference )
print(f"Integer Set ( After Symmetric Difference ): {int_set}")
```

Thus, we should get something that looks like this:

```console
Integer Set ( Before Symmetric Difference ): {1, 2, 3, 5}
Integer Set ( After Symmetric Difference ): {1, 4, 6, 7, 9}
```

### Union Method

Because we have clearly been using the *union* operator `|` in *methods* like the [[#Difference Update Method]]. I am not going to bother writing any explanation... *Wasting my time and stuff*.

> "*Even if I wasted my time writing the above paragraph*"


> [!INFO]
> The `.union()` method can have **multiple** *elements* as **parameters** and these "*elements*" can **must** be an *iterable*!

```python
# empty general set
general_set: set = {1, 2, 3, "A", "B", "C"}

# output the general set ( before union )
print(f"General Set ( Before Union ): {general_set}")

# perform some union operations on the set
general_set.union([1, 2, 3], [4, 5, 6], ("A", "B", "C"), {"D", "E", "F"})
general_set.union([4, 5, 6], ("D", "E", "F"))

# output the general set ( after union )
print(f"General Set ( After Union ): {general_set}")
```

Therefore the outputs should be:

```console
General Set ( Before Union ): {1, 2, 3, 'A', 'C', 'B'}
General Set ( After Union ): {1, 2, 3, 'A', 'C', 'B'}
```

> No Change! But did do its job.

> [!NOTE]
> As you can see, its takes whatever is in **between** the "*intersection*" of the Venn Diagram.
>
> > If you know what I am trying to say!
>

#### Using the `|` Operator

> [!INFO] Again, things to keep in mind
> - Our *iterable* should be of type `set()`
> - To add multiple *iterables* at the same time just continue to use `|`

> [!WARNING]
> <p align="center"> <strong> <span style="color: red;"> It Creates A New Set</span> </strong> !!!</p>
>
> > "*So there is a fucking difference between `.union()` method and `|` operator*"
>
> Yes, we are going to have to **create** *another* variable to store the result of the union operation.
>
> > This also means that the *original* set does **not** get modified! 
>

```python
# general set containing some elements
general_set_unioned: set = {1, "A"}

# general set containing some elements
general_set: set = {1, 2, 3, "A", "B", "C"}

# output the general set ( before union )
print(f"General Set ( Before Union ): {general_set_unioned}")

# perform some union operations on the set
general_set_unioned = (
    general_set
    | set([1, 2, 3])
    | set([4, 5, 6])
    | set(("A", "B", "C"))
    | {"D", "E", "F"}
)

# output the general set ( after union )
print(f"General Set ( After Union ): {general_set_unioned}")

general_set_unioned = general_set | {4, 5, 6} | set(("D", "E", "F"))

# output the general set ( after union )
print(f"Final General Set ( After Union ): {general_set_unioned}")
```

Therefore, we should get the result of:

```console
General Set ( Before Union ): {1, 'A'}
General Set ( After Union ): {1, 2, 3, 4, 'B', 5, 6, 'F', 'C', 'E', 'A', 'D'}
Final General Set ( After Union ): {1, 2, 3, 4, 'B', 5, 6, 'F', 'C', 'E', 'A', 'D'}
```

---

# Summary of Operators

In now particular order, here is the summary of each method ( *that has an operator equivalent* ) and its corresponding operator.

| Function - Method Name   | Operator |
| ------------------------ | -------- |
| Equality Function        | ==       |
| Inequality Function      | !=       |
| `.union()`               | \|       |
| `.update()`              | \|=      |
| `.difference()`          | `-`      |
| `.difference_update()`   | `-=`     |
| `.intersection()`        | `&`      |
| `.intersection_update()` | `&=`     |
| `.issubset()`            | `<=`     |
| `.issuperset()`          | `> =`     |
| `.symmetric_difference()`| `^`      |
| `.symmetric_difference_update()`| `^=` |

> [!SUCCESS]
> After many long hours and nights, 11,222 words and 69,956 characters.
>
> > **We are done**!!!
>

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!