---
id: Python - Maximum Heap ( Heap Module )
aliases: Max-Heap ( Priority Queue - Abstract Data Type  ) implemented using Python 'heapq' module
tags:
  - bifo
  - data-structures
  - heap
  - python
  - queue
author: S.Sunhaloo
date: 2026-03-28
status: Completed
---

## List of Contents

- [[#Create A Maximum Heap]]
- [[#Function / Method Related To Maximum Heap]]
	- [[#Maximum Heaps - Python Version 3.13 And Below]]
		- [[#Old Data Insertion Methods]]
			- [[#"Old" Heap Push ( Max ) Function]]
			- [[#"Old" Meld Function]]
		- [[#Old Data Removal Method]]
			- [[#"Old" Extract Maximum Function]]
	- [[#Maximum Heaps - Python Version 3.13 And Above]]
		- [[#Data Insertion Methods]]
			- [[#Heap Push ( Max ) Function]]
			- [[#Meld Function]]
		- [[#Data Removal Method]]
			- [[#Extract Maximum Function]]
	- [[#Miscellaneous Methods]]
		- [[#Length Of Heap]]
		- [[#Display / Print Heap]]
		- [[#Peek The Maximum Value / Root]]
		- [[#Parent Function]]
		- [[#Left Child Function]]
		- [[#Right Child Function]]
		- [[#Heapify Function]]

---

> [!INFO] Resource(s)
> 
> - [[Python - Maximum Heap ( Classes )]]
> - [[Python - Minimum Heap ( Heap Module )]]
> - Python Heap Module: https://docs.python.org/3/library/heapq.html#module-heapq

> [!NOTE]
> I highly recommend you that you go to each one of the above **resources** and *in order* so as to get an idea of what we are actually trying to implement.
> 
> > Specially the '[[Python - Minimum Heap ( Heap Module )]]' note!

> [!WARNING]
> Do remember to **add** the following line at the top of the file if you want to create a "*heap*" from the `heapq` module
> 
> ```python
> # import the "heap" / BIFO abstract data type from the 'heapq' module
> import heapq
> ```

# Create A Maximum Heap

To implement a *maximum* heap using the `heapq` module, we simply need to create / initialise an ( *empty* ) `list`!

```python
# create a maximum heap
max_heap: list = []
```

Yes, that's it! Like our [[Python - Maximum Heap ( Classes ) | `class`]] implementation which **does** also uses simple Python `list` / array.

> Here also, its the same thing!

---

> [!WARNING] Before We Start!
> 
> So **before** Python version `3.14`, there was **no** *functions* that would allows us to natively build a max-heap using `heapq` module.
> 
> Therefore, what programmers were doing; its that they were implementing a **min-heap** but used *negative elements* / "*keys*"... Which consequently made a **maximum heap**!
> 
> Given as of now, the 28 of March of 2026. [Debian](https://www.debian.org/)'s 'Trixie' which is the current **stable** version... Still ships Python with a version of `3.13` and the 'Bookworm' **old-stable** version still ships with `3.11`.
> 
> > [!INFO] Therefore...
> > 
> > I am going to basically split this note with a '*pre*' and '*post*' `3.14`.
> > 
> > This means that whatever your Python version is, you are still going to be able to **implement** your max-heap using the 'heapq' module!
> 
> > With that out of the way; let's get to the implementation!

---

# Function / Method Related To Maximum Heap

> [!WARNING]
> You are going to see `key` a lot! Don't worry about it for now.
> 
> Just know that the `key` can only be `int`, `float` or `str`. This is because our data ( *for this "learning session"* ) is going to look like this: `(key, actual_data )`.
> 
> > Yes a [[Python - Tuples | tuple]] containing 2 values!
> 
> We need `key` to *form part* of these 3 data types above because we are going to be using the `key` for **comparison**!

## Maximum Heaps - Python Version 3.13 And Below

### Old Data Insertion Methods

> Please do refer to the '[[Python - Minimum Heap ( Heap Module )]]' note so that you understand the **limitations** and **quirks** of inserting data!

#### "Old" Heap Push ( Max ) Function

Given that I am going to by using data of this format: `(key, value)`...

> There is something that needs to be said!

If we simply enter the `key` *normally* **without** any *pre-processing*. Well, we are just going to get a **minimum heap**

> [!TIP] The Solution!
> 
> The solution here is simple! Simply **negate** the *value* of the `key`.
> 
> Let's say that we have 2 numbers to add to our "**maximum heap**". We have to insert '-2' and '10'.
> 
> Hence, to create a **maximum** heap using *functions* use to create a minimum heap... Instead of inserting '-2', we *insert* '**2**' and similarly '**-10**' instead of '10'!

```python
# create a maximum heap
tuple_max_heap: list[tuple[int, str]] = []

# insert data in the following format: (-key, value)
heapq.heappush(tuple_max_heap, (-27, "Ayrton Senna"))
heapq.heappush(tuple_max_heap, (-44, "Lewis Hamilton"))
heapq.heappush(tuple_max_heap, (-5, "Sebastien Vettel"))

# create another maximum heap for simple integer numbers only
int_max_heap: list[int] = []

# insert simple integer data into the maximum heap
heapq.heappush(int_max_heap, -27)
heapq.heappush(int_max_heap, -44)
heapq.heappush(int_max_heap, -5)
```

#### "Old" Meld Function

```python
# "meld" the two maximum heaps together
# INFO: whereby `max_heap` and `other_max_heap` does not necessarily have to,
# originally, satisfy the max-heap property
combined_max_heaps = max_heap + other_max_heap

# "heapify" combined heap / list to satisfy max-heap property
heapq.heapify(combined_max_heaps)
```

### Old Data Removal Method

#### "Old" Extract Maximum Function

```python
# extract the maximum element / "root" node from heap
extracted = heapq.heappop(max_heap)
```

## Maximum Heaps - Python Version 3.13 And Above

### Data Insertion Methods

#### Heap Push ( Max ) Function

```python
# create a maximum heap
tuple_max_heap: list[tuple[int, str]] = []

# insert data in the following format: (key, value)
heapq.heappush_max(tuple_max_heap, (27, "Ayrton Senna"))
heapq.heappush_max(tuple_max_heap, (44, "Lewis Hamilton"))
heapq.heappush_max(tuple_max_heap, (5, "Sebastien Vettel"))

# create another maximum heap for simple integer numbers only
int_max_heap: list[int] = []

# insert simple integer data into the maximum heap
heapq.heappush_max(int_max_heap, 27)
heapq.heappush_max(int_max_heap, 44)
heapq.heappush_max(int_max_heap, 5)
```

#### Meld Function

```python
# "meld" the two maximum heaps together
# INFO: whereby `max_heap` and `other_max_heap` does not necessarily have to,
# originally, satisfy the max-heap property
combined_max_heaps = max_heap + other_max_heap

# "heapify" combined heap / list to satisfy max-heap property
heapq.heapify_max(combined_max_heaps)
```

### Data Removal Method

#### Extract Maximum Function

```python
# extract the maximum element / "root" node from heap
extracted = heapq.heappop_max(max_heap)
```

---

## Miscellaneous Methods

The functions / methods below are going to be the **same** regardless if you are trying to implement a *maximum heap* the old or new way!

### Length Of Heap

```python
# find the length of the maximum heap
print(f"Length of Maximum Heap: {len(max_heap)}")
```

### Display / Print Heap

```python
# display the maximum heap
print(f"Maximum Heap: {max_heap}")
```

### Peek The Maximum Value / Root

```python
# simply peek / see the maximum element / "root" node
print(f"Maximum Element ( Root Node ): {max_heap[0]}")
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
def left_child(index: int, heap: list) -> int | None:
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

```python
# heapify the list to satisfy the maximum heap property
heapq.heapify(other_max_heap)
```

---

# Creation Of Maximum Heap and Usage

> [!WARNING] New Version!
> 
> I am only going to be showing a full example code that uses the actual, newly implemented, `_max` *functions*.
> 
> Just go take a look at '[[Python - Minimum Heap ( Heap Module )#Creation Of Minimum Heap and Usage | Python - Minimum Heap ( Heap Module )]]' to see an example code if you are on an older Python version.
> 
> > With that out of the way...

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
    # create a drivers max-heap
    drivers_heap: list[tuple[int, str]] = []

    # insert data in the following format: (key, value)
    # NOTE: from Python 3.14 onwards we can use the native max-heap helpers
    heapq.heappush_max(drivers_heap, (27, "Ayrton Senna"))
    heapq.heappush_max(drivers_heap, (44, "Lewis Hamilton"))
    heapq.heappush_max(drivers_heap, (5, "Sebastien Vettel"))
    heapq.heappush_max(drivers_heap, (3, "Daniel Ricciardo"))
    heapq.heappush_max(drivers_heap, (4, "Lando Norris"))
    heapq.heappush_max(drivers_heap, (14, "Fernando Alonso"))

    # find the length of the heap
    print(f"\nLength of Drivers Max-Heap: {len(drivers_heap)}")

    # display the drivers heap after insertion of data
    print(f"\nDrivers Max-Heap After Insertion of Elements: {drivers_heap}")

    # simply peek / see the maximum element / "root" node
    print(f"\nMaximum Element ( Root Node ) In Drivers Heap: {drivers_heap[0]}")

    # extract the maximum element / "root" node from heap
    extracted = heapq.heappop_max(drivers_heap)

    # display the extracted value / "root" node of drivers heap
    print(f"\nExtracted Maximum Root From Drivers Heap: {extracted}")

    # display the drivers heap after extraction of "root" node
    print(f"\nDrivers Max-Heap After Extraction: {drivers_heap}")

    # find the parent of node with index '1' of the drivers heap
    print(f"\nParent of index 1 in Drivers Heap: {parent(1)}")

    # find the left child of node with index '1' of the drivers heap
    print(f"Left child of index 1 in Drivers Heap: {left_child(1, drivers_heap)}")

    # find the right child of node with index '1' of the drivers heap
    print(f"Right child of index 1 in Drivers Heap: {right_child(1, drivers_heap)}")

    # create a list of tuples of key-value pair to hold MotoGP riders
    # WARNING: this is just a simple list
    # it does not satisfy the max-heap property yet!
    riders_heap: list[tuple[int, str]] = [
        (46, "Valentino Rossi"),
        (93, "Marc Marquez"),
        (20, "Fabio Quartararo"),
        (4, "Andrea Dovizioso"),
        (25, "Maverick Vinales"),
        (12, "Brad Binder"),
    ]

    # heapify the list to satisfy the maximum heap property
    heapq.heapify_max(riders_heap)

    # display the riders heap after heapify
    print(f"\nRiders Heap After Heapify: {riders_heap}")

    # "meld" the two maximum heaps together
    # INFO: whereby `drivers_heap` and `riders_heap` do not necessarily have to,
    # originally, satisfy the max-heap property
    goated_racers_max_heap = drivers_heap + riders_heap

    # re-heapify the combined list to satisfy the max-heap property
    heapq.heapify_max(goated_racers_max_heap)

    # display the combined goated racers heap after melding
    print(f"\nGoated Racers Heap After Meld: {goated_racers_max_heap}")


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