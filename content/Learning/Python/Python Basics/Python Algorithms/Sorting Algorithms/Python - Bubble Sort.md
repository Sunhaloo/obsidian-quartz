---
id: Python - Bubble Sort
aliases: Implementation of Bubble Sort in Python
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

- [[#Bubble Sort]]
	- [[#My Bubble Sort]]
	- [[#Optimised Bubble Sort]]
	- [[#Lecturer's Optimised Bubble Sort]]
	- [[#Categories Which Insertion Sort Falls Into]]
	- [[#Bubble Sort ( Optimised ) Full Example Code]]

---

> [!INFO] Resource(s)
> - Visualisation: https://visualgo.net/en/sorting
> - Big-Oh Cheat Sheet: https://www.bigocheatsheet.com/
> - Neural Nine: https://www.youtube.com/watch?v=Sr521jBTcto
> - Portfolio Courses: https://www.youtube.com/watch?v=YqzNgaFQEh8 ( *Its actually C code* )
> - Michael Sambol: https://www.youtube.com/watch?v=xli_FI7CuzA

> [!INFO] Summary
> If you don't have time to read all this shit... Head straight for the '[[#Optimised Bubble Sort]]' heading!

# Bubble Sort

## My Bubble Sort

Bubble sort is the only sorting algorithm that I by heart since Grade 10!

Therefore, I am going to show you how I code the _unoptmised_ version.

```python
# function to sort an array / list iteratively using my bubble sort
def my_bubble_sort(arr: list):
    # iterate through the whole list
    for i in range(len(arr) - 1):
        # at each iteration; iterate through the remaining element ( till end of array )
        for j in range(len(arr) - 1):
            # sort the array in ascending order
            if arr[j] > arr[j + 1]:
                # swap the elements using Python's tuple thingy
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
```

> Nice indentations!

> [!NOTE] Time Complexity = O(n^2) [ $O(n^{2})$ ]
> - The **overall** *running* time complexity for this function is going to be O(n^2) [ $O(n^{2})$ ]
> - Best Case: O(n^2) [ $O(n^{2})$ ]
> - Worst Case: O(n^2) [ $O(n^{2})$ ]
>
> > [!INFO] Recurrence Equation: T(n) = T(n - 1) + n
> > - The outer `for` loop iterates `n - 1` times
> > - The inner `for` loop **always** iterates `n - 1` times regardless of the current pass ( *until the end of array / list* )
> > - Thus the **running time complexity** ( *in terms of `T(n)`* ) becomes: T(n) = T(n - 1) + n

> [!TIP] The Swapping Part
> Normally, in a language like C or Java, you would do something like this:
> 
> > I am writing this in a way so that you can 'copy-paste' into the above code and run!
> 
> ```python
> 	# swap the current element with its neighbour to the right
> 
> 	# store current element temporarily
> 	temp = arr[j]
> 	# overwrite current position with the right neighbour
> 	arr[j] = arr[j + 1]
> 	# place the stored element into the right position
> 	arr[j + 1] = temp
> ```
> 
> But because we use Python and we are *snakes*, we can just **rattle** and **slither** our way and do the **same** thing like so:
> 
> ```python
> 	# swap the elements using Python's tuple thingy
> 	arr[j], arr[j + 1] = arr[j + 1], arr[j]
> ```
> 
> > Or you could use 'XOR' to swap the numbers like ThePrimeagen did here: https://www.youtube.com/shorts/DJxEYOC8IRc ( *mostly used in Low Level Languages and Integers data types* )
> 
> > **Don't** use the 'XOR' trick though... Its **not** has *efficient* as Python's [[Python - Tuples | tuple]] swapping!

## Optimised Bubble Sort

> This is the one that you are going to need to use and remember!

Here is the **bubble sort** *function* that is going to be able to sort Python's list.

```python
# optimised bubble sort function to sort an array / list iteratively
def bubble_sort_optimised(arr: list):
    # iterate through the whole list
    for i in range(len(arr) - 1):
        # create the flag to check if elements have been swapped or not
        swapped = False

        # at each iteration; iterate through the remaining unsorted elements
        for j in range(len(arr) - 1 - i):
            # sort the array in ascending order
            if arr[j] > arr[j + 1]:
                # swap the elements using Python's tuple thingy
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

                # mark that a swap has occurred
                swapped = True

        # check for swapping; if not swaps made ==> already sorted
        if not swapped:
            break
```

> [!NOTE] Time Complexity = O(n^2) [ $O(n^{2})$ ]
> - The **overall** *running* time complexity for this function is going to be O(n^2) [ $O(n^{2})$ ]
> - Best Case: O(n) - occurs when the list is already sorted ( `swapped` flag triggers early exit )
> - Worst Case: O(n^2) [ $O(n^{2})$ ] - occurs when the list is sorted in reverse order
>
> > [!INFO] Recurrence Equation: T(n) = T(n - 1) + n
> > - The outer `for` loop iterates `n - 1` times
> > - The inner `for` loop iterates `n - 1 - i` times at each pass
> > 	- *Shrinking* by one each time as the **largest** elements *bubble* to their correct position at the end
> > - The `swapped` flag provides an **early exit** if no swaps were made in a pass
> > - Thus the **running time complexity** ( *in terms of `T(n)`* ) becomes: T(n) = T(n - 1) + n
> > - Additionally, compared to the *unoptimised* version; here we do have a best case:
> > 	- Already sorted: O(n)
> > 	- Half sorted: Between O(n) and O(n^2) [ $O(n^{2})$ ]
> > 	- Fully reversed:  O(n^2) [ $O(n^{2})$ ]

> [!TIP] Return New List Instead
> 
> This above code / `bubble_sort` function is going to sort the list **in-place**.
> 
> > Meaning that we do *touch* the original list!
> 
> Therefore if you want to make this function `return` a **new** list instead of *sorting* the original...
> 
> - Create a new list like `new_arr: list` **inside** the function
> - Create a **copy** of the original list using either the `new_list = arr.copy()` method / function or the `new_list = arr[:]` trick!

### Lecturer's Optimised Bubble Sort

> [!NOTE]
> If you actually go ahead and compared the above ( "*actual*" ) optimised code that we wrote ( *which the world also write it this way* ).
> 
> My lecturer's code is practically the *same* thing!
> 
> > So what's the problem you ask...
> 
> It's the fucking `while` loops that bothers me... In Python the `for` loop is a **direct** C implementation under the hood. Compared to  `while` loops which needs to be translated into Python's byte code and that's really **slow**!
> 
> > No joke its so fucking slow compared to the `for` loop!
> 
> > [!INFO]
> > Again, I have *nothing* **against** this code; but given that we are learning about Data Structures and Algorithms, I think we **should** *care* about **optimising** things to the maximum!
> > 
> > > Nevertheless, if you want pure optimisations and speed; do switch to C or Rust!

```python
# lecturer's optimised version of bubble sort
def lecturer_bubble_sort(arr: list):
    # initialise variable to hold number of comparisons to perform
    num_of_comparisons = len(arr) - 1

    # create the flag to check if elements have been swapped or not
    # NOTE: again, given that we are going to be using `while` loop here
    # we have to make `swapped` have a "value" of `True` as we need to enter loop
    swapped = True

    # consider this our outer `for` loop to iterate though unsorted elements
    while (num_of_comparisons != 0) and (swapped):
        # create actual `index` pointer to be able to swap each elements
        index = 0

        # reset the flag
        swapped = False

        # at each iteration; iterate through the remaining elements until correct index
        while index < num_of_comparisons:
            # sort the array in ascending order
            if arr[index] > arr[index + 1]:
                # swap the elements using Python's tuple thingy
                arr[index], arr[index + 1] = arr[index + 1], arr[index]

                # change the flag to show swapping
                swapped = True

            # go to the next element to check if current element needs more sorting
            index += 1

        # decrease the number of comparision to go through
        num_of_comparisons -= 1
```

## Categories Which Insertion Sort Falls Into

| Terminology | Selection Sort Category |
| ----------- | ----------------------- |
| Storage Location | Internal |
| Access Method | Array-based |
| Logic Type | Comparison-based |
| Relative Order | Stable |
| Space Usage | In-place |

## Bubble Sort ( Optimised ) Full Example Code

```python
# import the `randint` function from the 'random' module
from random import randint


# optimised bubble sort function to sort an array / list iteratively
def bubble_sort_optimised(arr: list):
    # iterate through the whole list
    for i in range(len(arr) - 1):
        # create the flag to check if elements have been swapped or not
        swapped = False

        # at each iteration; iterate through the remaining unsorted elements
        for j in range(len(arr) - 1 - i):
            # sort the array in ascending order
            if arr[j] > arr[j + 1]:
                # swap the elements using Python's tuple thingy
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

                # mark that a swap has occurred
                swapped = True

        # check for swapping; if not swaps made ==> already sorted
        if not swapped:
            break


# our main function
def main():
    # initialise a list of integers
    list_int: list[int] = [randint(0, 9) for i in range(5)]

    # initialise a list of floats
    list_float: list[float] = [6.69, 69.67, 21.19, 44.27, 5.33]

    # initialise a list of characters
    list_chars: list[str] = ["T", "W", "A", "T"]

    # display list before sorting
    print(f"Integers List Before Sorting: {list_int}")
    print(f"'Float' List Before Sorting: {list_float}")
    print(f"Characters List Before Sorting: {list_chars}")

    # sort each of these list using selection sort
    bubble_sort_optimised(list_int)
    bubble_sort_optimised(list_float)
    bubble_sort_optimised(list_chars)

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