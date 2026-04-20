---
id: Python - Heap Sort
aliases: Implementation of Heap Sort in Python
tags:
  - algos
  - arrays
  - dsa
  - lists
  - python
  - sorting
author: S.Sunhaloo
date: 2026-03-31
status: Completed
---

## List of Contents

- [[#Heap Sort]]
	- [[#Sorting In Ascending Order]]
		- [[#Maximum Heap - NeetCode Implementation]]
		- [[#Minimum Heap - Heap Module Implementation]]
	- [[#Sorting In Descending Order]]
		- [[#Minimum Heap - NeetCode Implementation]]
		- [[#Maximum Heap - Heap Module Implementation]]

---

> [!INFO] Resource(s)
> 
> - NeetCode ( *see Heap Sort section* ): https://neetcode.io/solutions/sort-an-array
> - Big-Oh Cheat Sheet: https://www.bigocheatsheet.com/
> - Michael Sambol: https://www.youtube.com/watch?v=2DmK_H7IdTo
> - Medium Article: https://medium.com/@ishta.pal/heap-sort-explained-using-python-4f1466509521

> [!WARNING]
> <p align="center">You have to understand the <em>Heap</em> structure <strong>first</strong>!</p>
> 
> The "*heap*" is basically a **partially ordered** ( *not sorted* ) binary tree.
> 
> > It's **not** a [[Python - Binary Search Tree | binary search tree]]!
> 
> This is because the heapsort technique uses a function / method ( *depending on how you implement it in Python* ) called `heapify` that basically takes any ordinary array / `list` and turns **Minimum** or **Maximum** Heap.
> 
> The **heap sort** uses a 2 part process whereby its going to:
> 
> 1. Convert an *arbitrary* array / `lists` into a **minimum** or **maximum** *heap*
> 	- Depending on the method the *type* of heap; we can sort in **ascending** / **descending**
> 2. It does that conversion using the `heapify` method
> 	- Whereby we can either implement it using `class`es or simply using `heapq.heapify` function
> 3. Finally, create another array / list with the sorted element by using the "*pop*" method
> 	- Again, either implemented with `classes` or used `heapq.heappop` function
> 

> [!NOTE] Therefore
> 
> This note / *learning session* is going to be broken down into multiple categories whereby we are going to use the different implementation below and try to sort an *arbitrary* array using `heapsort`.
> 
> > Here are the notes that I took and we are going to be basically implementing `heapsort` based on these!
> 
> - [[Python - Minimum Heap ( Classes )]]
> - [[Python - Minimum Heap ( Heap Module )]]
> - [[Python - Maximum Heap ( Classes )]]
> - [[Python - Maximum Heap ( Heap Module )]]


---

# Heap Sort

> [!WARNING] The Problem!
> 
> When I learned about how to build a Minimum and Maximum heap through Neural Nine's [video](https://www.youtube.com/watch?v=wOouknH8RsY)... We used data that look like this: `(key, value)`.
> 
> > Yes a [[Python - Tuples | tuple]] of `int`eger and "*value*"!
> 
> 
> But given that we just want to use **heap sort** to sort a "*simple*" array / `list` of data... Well, we are going to have to "*modify*" the code!
> 
> But given that the heap sort implementation for NeetCode ( *see above link* ) is much much better than if I go and modify "*my*" class implementation of heap structure.
> 
> > [!INFO] 
> > This is simply because of the fact that Neural Nine's implementation of Minimum / Maximum Heap is *optimised* for **heap operations** while NeetCode's is *optimised* for **sorting** specifically!
> 
> > Given that we are learning about the **heap sort** ( *sorting* ) algorithm... I think we should look into the most optimised version for this case!

> [!TIP]
> If your **goal** is *pure performance* when sorting, consider to use Python’s *built-in* `sort` function ( *that uses the [Timsort](https://en.wikipedia.org/wiki/Timsort) algorithm* ), which is **highly optimised** in [[C Data View | C]] and typically outperforms heap-based approaches in practice.
> 
> The `heapq` module is better **suited** for *priority queue* operations.
> 
> > Well, consider switching to 'C' or even 'Rust' for better overall performance!

## Summary

Here is what you could implement based on if you had to use `class`es or the 'heapq' module found in Python!

| Heap Sort | Ascending Order | Descending Order |
| --------- | --------------- | ---------------- |
| Classes   | **Maximum**     | *Minimum*        |
| Heap      | *Minimum*       | **Maximum**      |

> [!NOTE] Time Complexity!
> 
> For all of the *function* / code found inside the '**ascending order**' and '**descending order**' sections ( *whether implemented using `class`es or the `heapq` module* ), they are all going to have the **same** overall *time complexity*!
> 
> > [!TIP] Time Complexity = O(n log n)
> > - The **overall** *running* time complexity for these `heapsort` functions is O(n log n).
> > - Best Case: O(n log n)
> > - Worst Case: O(n log n)
> >   - In every case, we:
> >     - First **build a heap** from the array / list in O(n) time using `heapify` / `heapify_min` / `heapify_max`.
> >     - Then perform **n heap operations** (either `sift_down` or `heappop` / `heappop_max`), each of which costs O(log n).
> >   - Therefore, the *dominant* cost is n × O(log n) = O(n log n) regardless of whether the input list already looks like a heap or is a completely arbitrary array.
> 
> > The explanation for the 'Worst Case' was provided by [ChatGPT](https://chatgpt.com) through [Opencode](https://opencode.ai/)!

## Sorting In Ascending Order

### Maximum Heap - NeetCode Implementation

```python
# sift down function ( max-heap ) -> to sift down smaller values found at root node
def sift_down(arr: list, arr_length: int, index: int) -> None:
    # iterate through the whole list until max-heap property is satisified
    while True:
        # get largest index ==> root node
        largest_idx = index

        # get the left child
        left_child = (2 * index) + 1
        # get the right child
        right_child = (2 * index) + 2

        # largest element found at left "branch"
        if left_child < arr_length and arr[left_child] > arr[largest_idx]:
            # update the largest index
            largest_idx = left_child

        # largest element found at right "branch"
        if right_child < arr_length and arr[right_child] > arr[largest_idx]:
            # update the largest index
            largest_idx = right_child

        # check if the max-heap property has been reached
        if largest_idx == index:
            break

        # actually swap the element if largest index is not root node
        arr[index], arr[largest_idx] = arr[largest_idx], arr[index]

        # update the index so as to continue sifting ( down )
        index = largest_idx


# function to order arbitrary array into max-heap
def heapify(arr: list) -> None:
    # find the length of the array
    arr_length = len(arr)

    # iterate through the whole "binary tree" / list
    # NOTE: start at the last parent node and iterate backwards
    for i in range((arr_length // 2) - 1, -1, -1):
        # simply call the `sift_down` function
        sift_down(arr, arr_length, i)


# function to sort array in ascending order using "custom" functions
def heapsort(arr: list) -> None:
    # find the length of the array
    arr_length = len(arr)

    # use the `heapify` to turn list into max-heap
    heapify(arr)

    # finally extract the element and order them in ascending order
    for i in range(arr_length - 1, 0, -1):
        # swap the first element with the "current" element
        # INFO: in a max-heap --> first element ==> biggest element
        arr[0], arr[i] = arr[i], arr[0]

        # call `sift_down` function to restore max-heap property
        sift_down(arr, i, 0)
```

### Minimum Heap - Heap Module Implementation

#### In-Place Sorting

```python
# import the "heap" / priority queue abstract data type from the 'heapq' module
import heapq


# function to sort array in ascending order using 'heapq' module
def heapsort(arr: list) -> None:
    # convert the arbitrary list into one that satisifies min-heap property
    heapq.heapify(arr)

    # create a new list to hold sorted elements
    sorted_elements: list = []

    # iterate through the array until its empty
    while arr:
        # pop / remove the smallest element ==> root node
        smallest = heapq.heappop(arr)

        # add / append smallest element to new list
        sorted_elements.append(smallest)

    # use the `extend` function to put the sorted element back into original `arr`
    # INFO: this is what allows us to sort array / list in-place
    arr.extend(sorted_elements)
```

#### Return A New List

```python
# import the "heap" / priority queue abstract data type from the 'heapq' module
import heapq


# function to sort array in ascending order using 'heapq' module
def heapsort(arr: list) -> list:
    # create a copy of the original list ==> so as not to modify it
    heap = list(arr)
	
    # convert the arbitrary list into one that satisifies min-heap property
    heapq.heapify(heap)
	
    # repeatedly pop the smallest element to build the sorted list
    # INFO: we are using list comprehension here...
    # you could have simply used `heapq.heappop` and `append` function also!
    return [heapq.heappop(heap) for _ in range(len(heap))]
```

## Sorting In Descending Order

### Minimum Heap - NeetCode Implementation

```python
# sift down function ( min-heap ) -> to sift down larger values found at root node
def sift_down(arr: list, arr_length: int, index: int) -> None:
    # iterate through the whole list until min-heap property is satisfied
    while True:
        # get smallest index ==> root node
        smallest_idx = index

        # get the left child
        left_child = (2 * index) + 1
        # get the right child
        right_child = (2 * index) + 2

        # smallest element found at left "branch"
        if left_child < arr_length and arr[left_child] < arr[smallest_idx]:
            # update the smallest index
            smallest_idx = left_child

        # smallest element found at right "branch"
        if right_child < arr_length and arr[right_child] < arr[smallest_idx]:
            # update the smallest index
            smallest_idx = right_child

        # check if the min-heap property has been reached
        if smallest_idx == index:
            break

        # actually swap the element if smallest index is not root node
        arr[index], arr[smallest_idx] = arr[smallest_idx], arr[index]

        # update the index so as to continue sifting ( down )
        index = smallest_idx


# function to order arbitrary array into min-heap
def heapify(arr: list) -> None:
    # find the length of the array
    arr_length = len(arr)

    # iterate through the whole "binary tree" / list
    # NOTE: start at the last parent node and iterate backwards
    for i in range((arr_length // 2) - 1, -1, -1):
        # simply call the `sift_down` function
        sift_down(arr, arr_length, i)


# function to sort array in descending order using "custom" functions
def heapsort(arr: list) -> None:
    # find the length of the array
    arr_length = len(arr)

    # use the `heapify` to turn list into min-heap
    heapify(arr)

    # finally extract the elements and order them in descending order
    for i in range(arr_length - 1, 0, -1):
        # swap the first element with the "current" element
        # INFO: in a min-heap --> first element ==> smallest element
        arr[0], arr[i] = arr[i], arr[0]

        # call `sift_down` function to restore min-heap property
        sift_down(arr, i, 0)
```

### Maximum Heap - Heap Module Implementation

If you read about '[[Python - Maximum Heap ( Heap Module )]]', then you are going to know that **before** Python `3.14` there was no *functions* that would allow one to natively build a max-heap using the `heapq` module!

Therefore what were programmers doing back then... They used *negative* elements to build a **maximum** heap using the "*minimum*" `heapq` functions.

Therefore, before we sort an array / list, in **descending order**, through the `heapq` module. I am going to first show you how one would sort and array using `heapsort` built from the `heapq` module **before** Python `3.14`

> As for right now ( 6/04/2026 ); the latest version of Python is `3.14.3`!

## Python Version 3.13 And Below

##### In-Place Sorting

```python
# import the "heap" / priority queue abstract data type from the 'heapq' module
import heapq


# function to sort array in descending order using 'heapq' module
# WARNING: we are assuming that you are using Python version 3.13 or below
def heapsort(arr: list[int]) -> None:
    # iterate through the array / list and negate every element
    for i in range(len(arr)):
        arr[i] = -arr[i]

    # convert the arbitrary list into one that satisifies min-heap property
    heapq.heapify(arr)

    # create a new list to hold sorted elements in descending order
    sorted_elements: list = []

    # iterate through the heap until its empty
    while arr:
        # pop / remove the smallest element ==> root node
        largest_neg = heapq.heappop(arr)

        # add / append largest element to new list
        sorted_elements.append(-largest_neg)

    # use the `extend` function to put the sorted element back into original `arr`
    # INFO: this is what allows us to sort array / list in-place
    arr.extend(sorted_elements)
```

##### Return A New List

```python
# import the "heap" / priority queue abstract data type from the 'heapq' module
import heapq


# function to sort array in descending order using 'heapq' module
# WARNING: we are assuming that you are using Python version 3.13 or below
def heapsort(arr: list[int]) -> list:
    # create a copy of the original list ==> so as not to modify it
    heap = list(arr)

    # negate all the values to simulate a maximum heap using a minimum heap
    # TIP: simply use list comprehension here...
    heap = [-value for value in heap]

    # convert the arbitrary list into one that satisifies min-heap property
    heapq.heapify(heap)

    # repeatedly pop the largest element to build the sorted list
    # INFO: we are using list comprehension here...
    # you could have simply used `heapq.heappop` and `append` function also!
    
    # WARNING: remember if you are using `.append`;
    # you need to append the positive elements by negating elements
    return [-heapq.heappop(heap) for _ in range(len(heap))]
```

> [!WARNING]
> From what I can see above, for the above two function... You are only going to be able to use then with arrays / lists that contains either, `int`egers, `float`s or `double` data types.

## Python Version 3.14 And Above

##### In-Place Sorting

```python
# import the "heap" / priority queue abstract data type from the 'heapq' module
import heapq


# function to sort array in descending order using 'heapq' module
# WARNING: this requires that you are using Python version 3.14 or above
def heapsort(arr: list) -> None:
    # convert the arbitrary list into one that satisifies max-heap property
    heapq.heapify_max(arr)

    # create a new list to hold sorted elements in descending order
    sorted_elements: list = []

    # iterate through the heap until its empty
    while arr:
        # pop / remove the largest element ==> root node
        largest = heapq.heappop_max(arr)

        # add / append largest element to new list
        sorted_elements.append(largest)

    # use the `extend` function to put the sorted elements back into original `arr`
    # INFO: this is what allows us to sort array / list in-place
    arr.extend(sorted_elements)
```

##### Return A New List

```python
# import the "heap" / priority queue abstract data type from the 'heapq' module
import heapq


# function to sort array in descending order using 'heapq' module
# WARNING: this requires that you are using Python version 3.14 or above
def heapsort(arr: list) -> list:
    # create a copy of the original list ==> so as not to modify it
    heap = list(arr)

    # convert the arbitrary list into one that satisifies max-heap property
    heapq.heapify_max(heap)

    # repeatedly pop the largest element to build the sorted list (descending)
    # INFO: we are using list comprehension here...
    # you could have simply used `heapq.heappop_max` and `append` function also!
    sorted_elements: list = [heapq.heappop_max(heap) for _ in range(len(heap))]

    # return the new sorted list (descending order)
    return sorted_elements
```

---

> [!INFO]
> For this note, I am **not** going to do a big section with *full example programs* like in the other notes.
>  
> It’s too much and would be overkill; this is a simple function that you can just *yoink* and drop into your own code.
>  
> > Therefore, there’s **no** need for *full code* implementations here!

---

# Socials

- **GitHub**: https://www.github.com/Sunhaloo
- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo

---

S.Sunhaloo
Thank You!