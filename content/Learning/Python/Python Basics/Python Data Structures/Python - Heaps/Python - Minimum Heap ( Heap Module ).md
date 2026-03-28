---
id: Python - Minimum Heap ( Heap Module )
aliases: Min-Heap ( Priority Queue - Abstract Data Type  ) implemented using Python 'heapq' module
tags:
  - bifo
  - data-structures
  - heap
  - python
  - queue
author: S.Sunhaloo
date: 2026-03-25
status: Completed
---

## List of Contents

- [[#The Heap Module]]
- [[#Create A Minimum Heap]]
- [[#Function / Method Related To Minimum Heap]]
	- [[#Data Insertion Methods]]
		- [[#Heap Push Function]]
		- [[#Meld Function]]
	- [[#Data Removal]]
		- [[#Extract Minimum Function]]
	- [[#Miscellaneous Methods]]
		- [[#Length Of Heap]]
		- [[#Display / Print Heap]]
		- [[#Peek The Minimum Value / Root]]
		- [[#Parent Function]]
		- [[#Left Child Function]]
		- [[#Right Child Function]]
		- [[#Heapify Function]]

---

> [!INFO] Resource(s)
> 
> - [[Python - Minimum Heap ( Classes )]]
> - Python Heap Module: https://docs.python.org/3/library/heapq.html#module-heapq

> [!NOTE]
> I highly recommend you that you go to each one of the above **resources** and *in order* so as to get an idea of what we are actually trying to implement.

# The Heap Module

Compared to the [[Python - Stacks ( Queue Module ) | `queue`]] module; this is actually a *simple* module that basically allows us to create a **priority queue**

This is a *lightweight* tool that provides a **collection of functions** to transform a *standard* Python `list` into a **min-heap**!

Because it uses a highly optimised [[C Data View | C]] implementation of the 'Binary Heap' algorithms ( *sift-up and sift-down* ).

It is an **efficient** way of *creating* and *handling* priority based data structures in Python. We use this primarily for '*Heapsort*' and for any situation where we need $O(1)$ **access** to the *smallest* element.

> [!WARNING]
> Do remember to **add** the following line at the top of the file if you want to create a "*heap*" from the `heapq` module
> 
> ```python
> # import the "heap" / BIFO abstract data type from the 'heapq' module
> import heapq
> ```

# Create A Minimum Heap

To implement a *minimum* heap using the `heapq` module, we simply need to create / initialise an ( *empty* ) `list`!

```python
# create a minimum heap
min_heap: list = []
```

Yes, that's it! Like our [[Python - Minimum Heap ( Classes ) | `class`]] implementation which **does** also uses simple Python `list` / array.

> Here also, its the same thing!

---

# Function / Method Related To Minimum Heap

> [!WARNING]
> You are going to see `key` a lot! Don't worry about it for now.
> 
> Just know that the `key` can only be `int`, `float` or `str`. This is because our data ( *for this "learning session"* ) is going to look like this: `(key, actual_data )`.
> 
> > Yes a [[Python - Tuples | tuple]] containing 2 values!
> 
> We need `key` to *form part* of these 3 data types above because we are going to be using the `key` for **comparison**!

## Data Insertion Methods

### Heap Push Function

Do you still remember the [[Python - Minimum Heap ( Classes )#Insert Method | insert]] method that we implemented in our `class` implementation of `MinHeap`?

> I am just asking you to remember the **format** of the *data* that we were inserting!

Well, if you **don't**... We were inserting data that was in the following *format*:

```console
(key, value)
```

> But there is a "*problem*" here!

> [!INFO] "*All Data Types But Of Single Type*"
> 
> What is the *definition* of an array?
> 
> Basically an array is a data structure that holds **multiple** items of the **same** *data type*.
> 
> Now, given that we are working with Python `list`s; therefore, we are able to insert *any* type of data!
> 
> The thing about `heapq` module is that it compares with the **same** *type* of data. Therefore, if we insert data with the format of: `(key, value)`.
> 
> > Hence, we are **not** going to be able to enter *other* types of data!
> 
> Let' us actually insert some data for you to see...

```python
# create a minimum heap
tuple_min_heap: list[tuple[int, str]] = []

# insert data in the following format: (key, value)
heapq.heappush(tuple_min_heap, (27, "Ayrton Senna"))
heapq.heappush(tuple_min_heap, (44, "Lewis Hamilton"))
heapq.heappush(tuple_min_heap, (5, "Sebastien Vettel"))

# create another minimum heap for simple integer numbers only
int_min_heap: list[int] = []

# insert simple integer data into the minimum heap
heapq.heappush(int_min_heap, 27)
heapq.heappush(int_min_heap, 44)
heapq.heappush(int_min_heap, 5)
```

> [!SUCCESS]
> The above code block is going to be working fine. Again, "*show me the problem*" I hear you groan...
> 
> > Well, here it is!
> 
> > [!BUG]
> > If you try doing something like this:
> > 
> >```python
> ># create a heap to hold different data types
> >mult_type_heap: list = []
> >
> ># insert simple integer numbers and also tuples of key-value pair
> >heapq.heappush(mult_type_heap, 27)
> >heapq.heappush(mult_type_heap, (44, "Lewis Hamilton"))
> > ```
> > 
> > - If we try to run this, we should see that we get an error:
> > 
> > ```console
> > TypeError: '<' not supported between instances of 'tuple' and 'int'
> > ```
> 
> > As long as you stick to "*the format*" you decided upon from the **start**, everything will work fine. In addition, given that we are going to be basically **inserting** [[Python - Tuples | tuples]], we are going do something like `heap[heap_list_index][1]` if you want to access the *value* or `heap[heap_list_index][0]` to access the *key*!

> [!WARNING] I am grabbing your attention!
> 
> Given that I have been able to grab your attention; this means that you have not been take by the '*shorts*' / '*reels*' overlords.
> 
> Yes, for this **learning session** I am going to be *inserting* / *using* the data format, tuple thingy that we talked above above!

### Meld Function

> Heapify to meld!

There are **no** built-in functions provided by 'heapq' to *merge* two ( *or more* ) heap.

> It does **not** provide a way to *merge* heaps that **preserve** the heap structure!

Hence, we are going to make use of the `heapq.heapify` method to **combine** multiple *minimum heaps*.

> For more information, head below and you should see the '[[#Heapify Method]]' heading.

> [!TIP] They **don't** have to *satisfy* the **min-heap** *property*!
> 
> Yes, given that we are simply using `heapq.heapify` to "*merge*" them together.
> 
>  The function will **first** treat the combined list as a *flat* list and *then*, apply the 'bottom-up' sift down method.
> 
> The resulting structure **satisfies** the min-heap *property*.

```python
# "meld" the two minimum heaps together
# INFO: whereby `min_heap` and `other_min_heap` does not necessarily have to,
# originally, satisfy the min-heap property
combined_min_heaps = min_heap + other_min_heap

# "heapify" combined heap / list to satisfy min-heap property
heapq.heapify(combined_min_heaps)
```

> [!NOTE]
> 
> Similar to our `meld_min_heap` [[Python - Minimum Heap ( Classes )#Meld | method]]; the above code is **not** an *incremental merge operation*... It **rebuilds** the heap from *scratch*.

## Data Removal Method

### Extract Minimum Function

```python
# extract the minimum element / "root" node from heap
extracted = heapq.heappop(min_heap)
```

## Miscellaneous Methods

### Length Of Heap

> Do I need to say something?

```python
# find the length of the minimum heap
print(f"Length of Minimum Heap: {len(min_heap)}")
```

### Display / Print Heap

> Again, do I need to say something?

```python
# display the minimum heap
print(f"Minimum Heap: {min_heap}")
```

### Peek The Minimum Value / Root

Well, in this case, we **don't** need to write the *error handling* ourselves, and therefore, we simply have this!

```python
# simply peek / see the minimum element / "root" node
print(f"Minimum Element ( Root Node ): {min_heap[0]}")
```

### Parent Function

```python
# function to find the parent of a "node"
def parent(index: int) -> int | None:
    # find the parent of a "node" while the index is greater than '0'
    return ((index - 1) // 2) if index > 0 else None
```

### Left Child Function

```python
# function to find the left child of a "node"
def left_child(index, heap: list) -> int | None:
    # calculate the index of the left child
    left_child_idx = (2 * index) + 1

    # return the correct index ==> depending of `index` provided
    return left_child_idx if left_child_idx < len(heap) else None
```

### Right Child Function

```python
# function to find the right child of a "node"
def right_child(index: int, heap: list) -> int | None:
    # calculate the index of the right child
    right_child_idx = (2 * index) + 2

    # return the correct index ==> depending of `index` provided
    return right_child_idx if right_child_idx < len(heap) else None
```

### Heapify Function

Compared to our heapify method that we implemented in '[[Python - Minimum Heap ( Classes )#Heapify Method | Python - Minimum Heap ( Classes )]]'; the `heapq.heapify` function is here going to simple work **in-place** and does **not** create a *copy*.

```python
# heapify the list to satisfy the minimum heap property
heapq.heapify(other_min_heap)
```

> [!WARNING]
> What I am trying to day its that, originally the `other_min_heap` was just a *simple* Python `list`.
> 
> > Initially, `other_min_heap` did **not** satisfy the min-heap property... *Well that is why we use `heapq.heapify`*!

---

# Creation Of Minimum Heap and Usage

Here is simple, example of what we get when we combine all of these functions above.

> [!INFO]
> I hard-coded the input and deletion; but you can easily use a `for` loop to create another *simple* function if you want to allow for user input!

> [!NOTE]
> I said above that for this *learning session*, I am going to be using data that is in this format: `(key, value)`.
> 
> Well, here also, its going to be the **same** thing!

```python
# import the "heap" / BIFO abstract data type from the 'heapq' module
import heapq


# function to find the parent of a "node"
def parent(index: int) -> int | None:
    # find the parent of a "node" while the index is greater than '0'
    return ((index - 1) // 2) if index > 0 else None


# function to find the left child of a "node"
def left_child(index: int, heap: list) -> int | None:
    # calculate the index of the left child
    left_child_idx = (2 * index) + 1

    # return the correct index ==> depending of `index` provided
    return left_child_idx if left_child_idx < len(heap) else None


# function to find the right child of a "node"
def right_child(index: int, heap: list) -> int | None:
    # calculate the index of the right child
    right_child_idx = (2 * index) + 2

    # return the correct index ==> depending of `index` provided
    return right_child_idx if right_child_idx < len(heap) else None


# our main function
def main():
    # create a drivers min-heap
    drivers_heap: list[tuple[int, str]] = []

    # insert data in the following format: (key, value)
    heapq.heappush(drivers_heap, (27, "Ayrton Senna"))
    heapq.heappush(drivers_heap, (44, "Lewis Hamilton"))
    heapq.heappush(drivers_heap, (5, "Sebastien Vettel"))
    heapq.heappush(drivers_heap, (3, "Daniel Ricciardo"))
    heapq.heappush(drivers_heap, (4, "Lando Norris"))
    heapq.heappush(drivers_heap, (14, "Fernando Alonso"))

    # find the length of the heap
    print(f"\nLength of Drivers Heap: {len(drivers_heap)}")

    # display the drivers heap after insertion of data
    print(f"\nDrivers Heap After Insertion of Elements: {drivers_heap}")

    # simply peek / see the minimum element / "root" node
    print(f"\nMinimum Element ( Root Node ) In Drivers Heap: {drivers_heap[0]}")

    # extract the minimum element / "root" node from heap
    extracted = heapq.heappop(drivers_heap)

    # display the extracted value / "root" node of drivers heap
    print(f"\nExtracted Minimum Root From Drivers Heap: {extracted}")

    # display the drivers heap after extraction of "root" node
    print(f"\nDrivers Heap After Extraction: {drivers_heap}")

    # find the parent of node with index '1' of the drivers heap
    print(f"\nParent of index 1 in Drivers Heap: {parent(1)}")

    # find the left child of node with index '1' of the drivers heap
    print(f"Left child of index 1 in Drivers Heap: {left_child(1, drivers_heap)}")

    # find the right child of node with index '1' of the drivers heap
    print(f"Right child of index 1 in Drivers Heap: {right_child(1, drivers_heap)}")

    # create a list of tuples of key-value pair to hold MotoGP riders
    # WARNING: this is just a simple list
    # it does not satisfy the min-heap property yet!
    riders_heap: list[tuple[int, str]] = [
        (46, "Valentino Rossi"),
        (93, "Marc Marquez"),
        (20, "Fabio Quartararo"),
        (4, "Andrea Dovizioso"),
        (25, "Maverick Vinales"),
        (12, "Brad Binder"),
    ]

    # heapify the list to satisfy the minimum heap property
    heapq.heapify(riders_heap)

    # display the riders heap after heapify
    print(f"\nRiders Heap After Heapify: {riders_heap}")

    # "meld" the two minimum heaps together ==> original heaps size increases
    # INFO: whereby `drivers_heap` and `riders_heap` do not necessarily have to,
    # originally, satisfy the min-heap property
    goated_racers_min_heap = drivers_heap + riders_heap

    # "heapify" combined heap / list to satisfy min-heap property
    heapq.heapify(goated_racers_min_heap)

    # display the combined goated racers heap after melding
    print(f"\nGoated Racers Heap After Meld: {goated_racers_min_heap}")


if __name__ == "__main__":
    main()
```

---

# Socials

- **GitHub**: https://www.github.com/Sunhaloo
- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo

---

S.Sunhaloo
Thank You!