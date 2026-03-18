---
id: Python - Selection Sort
aliases: Implementation of Selection Sort in Python
tags:
  - algos
  - arrays
  - dsa
  - lists
  - python
  - sorting
author: S.Sunhaloo
date: 2026-03-11
status: Completed
---

## List of Contents

- [[#Selection Sort]]
	- [[#Categories Which Selection Sort Falls Into]]
	- [[#Selection Sort Full Example Code]]

---

> [!INFO] Resource(s)
> - Visualisation: https://visualgo.net/en/sorting
> - Big-Oh Cheat Sheet: https://www.bigocheatsheet.com/
> - Neural Nine: https://www.youtube.com/watch?v=0MdfSjSnPe0
> - Portfolio Courses: https://www.youtube.com/watch?v=YepJ7fDmyjI ( *Its actually C code* )
> - Michael Sambol: https://www.youtube.com/watch?v=g-PGLbMth_g

> [!WARNING]
> Please do refer to the resources above to see how the sorting algorithm actually works ( *in terms of movement of elements* ).

# Selection Sort

Here is the **selection sort** *function* that is going to be able to sort Python's list.

> But this implementation is going to work in most if not all programming languages!

```python
# function to sort an array / list iteratively using selection sort
def selection_sort(arr: list):
    # iterate through the whole array / list
    for i in range(len(arr)):
        # initialise variable to hold index of minimum element at each iteration
        min_idx = i

        # iterate through the rest of the elements found in array / list
        for j in range(i + 1, len(arr)):
            # check for minimum element at each iteration
            if arr[j] < arr[min_idx]:
                # new minimum element found ==> change `min_idx`
                min_idx = j

        # swap the required element
        if min_idx != i:
            # NOTE: using Python's tuple thingy to swap
            # else simply use `temp` for other languages
            arr[i], arr[min_idx] = arr[min_idx], arr[i]
```

> [!INFO]
> The line of code `if min_idx != i` just **before** the actual swap is; you could say a little optimisation.
> 
> **During** swapping there will be some elements that are **already** going to be in their *correct* position. Hence, we simply make sure that we swap only when `i` is **not** `min_idx`.

> [!NOTE] Time Complexity = O(n^2) [ $O(n^{2})$ ]
> - The **overall** *running* time complexity for this function is going to be O(n^2) [ $O(n^{2})$ ]
> - Best Case: O(n^2) [ $O(n^{2})$ ]
> - Worst Case: O(n^2) [ $O(n^{2})$ ]
>
> > [!INFO] Time Complexity Equation: T(n) = T(n - 1) + n
> > - Iterate through an array of size `n`; this means that we are going to have an outer loop that runs `n` times
> > - At each iteration of the outer loop, we search the **remaining unsorted** portion of the array for the minimum element
> > 	- On the first pass, we search `n - 1` elements
> > 	- On the second pass, we search `n - 2` elements
> > 	- And so on...
> > - Thus the **running time complexity** ( *in terms of `T(n)`* ) becomes: T(n) = T(n - 1) + n

> [!TIP] Return New List Instead
> 
> This above code / `selection_sort` function is going to sort the list **in-place**.
> 
> > Meaning that we do *touch* the original list!
> 
> Therefore if you want to make this function `return` a **new** list instead of *sorting* the original...
> 
> - Create a new list like `new_arr: list` **inside** the function
> - Create a **copy** of the original list using either the `new_list = arr.copy()` method / function or the `new_list = arr[:]` trick!

## Categories Which Selection Sort Falls Into

| Terminology | Selection Sort Category |
| ----------- | ----------------------- |
| Storage Location | Internal |
| Access Method | Array-based |
| Logic Type | Comparison-based |
| Relative Order | Unstable |
| Space Usage | In-place |

## Selection Sort Full Example Code

```python
# import the `randint` function from the 'random' module
from random import randint


# function to sort an array / list iteratively using selection sort
def selection_sort(arr: list):
    # iterate through the whole array / list
    for i in range(len(arr)):
        # initialise variable to hold index of minimum element at each iteration
        min_idx = i

        # iterate through the rest of the elements found in array / list
        for j in range(i + 1, len(arr)):
            # check for minimum element at each iteration
            if arr[j] < arr[min_idx]:
                # new minimum element found ==> change `min_idx`
                min_idx = j

        # swap the required element
        if min_idx != i:
            # NOTE: using Python's tuple thingy to swap
            # else simply use `temp` for other languages
            arr[i], arr[min_idx] = arr[min_idx], arr[i]


# our main function
def main():
    # initialise a list of integers
    list_int: list[int] = [randint(0, 9) for i in range(5)]

    # initialise a list of floats
    list_float: list[float] = [6.69, 69.67, 21.19, 44.27, 5.33]

    # initialise a list of characters
    list_chars: list[str] = ["F", "U", "C", "K"]

    # display list before sorting
    print(f"Integers List Before Sorting: {list_int}")
    print(f"'Float' List Before Sorting: {list_float}")
    print(f"Characters List Before Sorting: {list_chars}")

    # sort each of these list using selection sort
    selection_sort(list_int)
    selection_sort(list_float)
    selection_sort(list_chars)

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