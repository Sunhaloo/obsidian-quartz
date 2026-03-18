---
id: Python - Insertion Sort
aliases: Implementation of Insertion Sort in Python
tags:
  - algos
  - arrays
  - dsa
  - lists
  - python
  - sorting
author: S.Sunhaloo
date: 2026-03-12
status: Completed
---

## List of Contents

- [[#Insertion Sort]]
	- [[#Categories Which Insertion Sort Falls Into]]
	- [[#Insertion Sort Full Example Code]]

---

> [!INFO] Resource(s)
> - Visualisation: https://visualgo.net/en/sorting
> - Big-Oh Cheat Sheet: https://www.bigocheatsheet.com/
> - Neural Nine: https://www.youtube.com/watch?v=GzyOEmu_Jv8
> - Portfolio Courses: https://www.youtube.com/watch?v=Tz7vBodZqo8 ( *Its actually C code* )
> - Michael Sambol: https://www.youtube.com/watch?v=JU767SDMDvA


> [!WARNING]
> Please do refer to the resources above to see how the sorting algorithm actually works ( *in terms of movement of elements* ).

# Insertion Sort

Here is the **insertion sort** *function* that is going to be able to sort Python's list.

> But this implementation is going to work in most if not all programming languages!

```python
# function to sort an array / list iteratively using insertion sort
def insertion_sort(arr: list):
    # iterate through the whole array / list
    # NOTE: starting with index '1' as a single element is considered to be sorted
    for i in range(1, len(arr)):
        # intialise the key at each iteration
        key = arr[i]

        # initialise "current" pointer ==> to track current position
        j = i

        # iterate through the rest of the array swapping as need be with "next" element
        # INFO: the main case for swapping is:
        # 1. pointer `j` should be greater than '0'
        # 2. previous element should be greater than current element `i`
        while (j > 0) and (arr[j - 1] > key):
            # shift the two "current" elements
            arr[j] = arr[j - 1]

            # do also decrement the pointer
            j -= 1

        # finally place the key where it belongs
        arr[j] = key
```

> [!NOTE] Time Complexity = O(n^2) [ $O(n^{2})$ ]
> - The **overall** *running* time complexity for this function is going to be O(n^2) [ $O(n^{2})$ ]
> - Best Case: O(n)
> - Worst Case: O(n^2) [ $O(n^{2})$ ]
>
> > [!INFO] Recurrence Equation: T(n) = T(n - 1) + n
> > - The outer `for` loop iterates through the array from index `1` to `n`, giving us `T(n - 1)`
> > - At each iteration, the inner `while` loop **shifts** elements to the right to find the correct position for the `key`
> > 	- Best Case: the `while` loop never executes ( array already sorted ) thus, O(1) inner work
> > 	- Worst Case: the `while` loop shifts every element therefore, O(n) inner work
> > - Thus the **running time complexity** ( *in terms of `T(n)`* ) becomes: T(n) = T(n - 1) + n
> > 
> > - Additionally, compared to [[Python - Selection Sort | Selection Sort]] which is only O(n^2) [ $O(n^{2})$ ]... Here we can have
> > 	- **Fully** sorted: O(n)
> > 	- **Half** sorted: Between O(n) and O(n^2) [ $O(n^{2})$ ]
> > 	- **Fully** reversed: O(n^2) [ $O(n^{2})$ ]

> [!TIP] Return New List Instead
> 
> This above code / `insertion_sort` function is going to sort the list **in-place**.
> 
> > Meaning that we do *touch* the original list!
> 
> Therefore if you want to make this function `return` a **new** list instead of *sorting* the original...
> 
> - Create a new list like `new_arr: list` **inside** the function
> - Create a **copy** of the original list using either the `new_list = arr.copy()` method / function or the `new_list = arr[:]` trick!

## Categories Which Insertion Sort Falls Into

| Terminology | Selection Sort Category |
| ----------- | ----------------------- |
| Storage Location | Internal |
| Access Method | Array-based |
| Logic Type | Comparison-based |
| Relative Order | Stable |
| Space Usage | In-place |

## Insertion Sort Full Example Code

```python
# import the `randint` function from the 'random' module
from random import randint


# function to sort an array / list iteratively using insertion sort
def insertion_sort(arr: list):
    # iterate through the whole array / list
    # NOTE: starting with index '1' as a single element is considered to be sorted
    for i in range(1, len(arr)):
        # intialise the key at each iteration
        key = arr[i]

        # initialise "current" pointer ==> to track current position
        j = i

        # iterate through the rest of the array swapping as need be with "next" element
        # INFO: the main case for swapping is:
        # 1. pointer `j` should be greater than '0'
        # 2. previous element should be greater than current element `i`
        while (j > 0) and (arr[j - 1] > key):
            # shift the two "current" elements
            arr[j] = arr[j - 1]

            # do also decrement the pointer
            j -= 1

        # finally place the key where it belongs
        arr[j] = key


# our main function
def main():
    # initialise a list of integers
    list_int: list[int] = [randint(0, 9) for i in range(5)]

    # initialise a list of floats
    list_float: list[float] = [6.69, 69.67, 21.19, 44.27, 5.33]

    # initialise a list of characters
    list_chars: list[str] = ["S", "H", "I", "T"]

    # display list before sorting
    print(f"Integers List Before Sorting: {list_int}")
    print(f"'Float' List Before Sorting: {list_float}")
    print(f"Characters List Before Sorting: {list_chars}")

    # sort each of these list using selection sort
    insertion_sort(list_int)
    insertion_sort(list_float)
    insertion_sort(list_chars)

    print("\n" + "-" * 50, "\n")

    # display list after sorting
    print(f"Integers List After Sorting: {list_int}")
    print(f"'Float' List After Sorting: {list_float}")
    print(f"Characters List After Sorting: {list_chars}")


if __name__ == "__main__":
    main()
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!