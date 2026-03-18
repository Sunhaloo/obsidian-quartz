---
id: Python - Quicksort
aliases: Implementation of Quicksort in Python
tags:
  - algos
  - arrays
  - divide-and-conquer
  - dsa
  - lists
  - python
  - sorting
author: S.Sunhaloo
date: 2026-03-12
status: Completed
---

## List of Contents

- [[#Quicksort - Hoare]]
	- [[#Lecturer's Quicksort]]
	- [[#Lecturer' Optimised Quicksort ( Median of Three )]]
- [[#Quicksort - Hoare Further Optimisation]]
	- [[#Median of Three and Insertion Sort]]
	- [[#Median of Three and Selection Sort]]
- [[#Quicksort - Lomuto]]
- [[#Categories Which Insertion Sort Falls Into]]
- [[#Quicksort Full Example Codes]]
	- [[#Lecturer's Quicksort Full Code]]
	- [[#Lecturer's Optimised ( Median of Three ) Quicksort Full Code]]
	- [[#Optimised ( Median Of Three + Insertion Sort ) Quicksort Full Code]]
	- [[#Optimised ( Median Of Three + Selection Sort ) Quicksort Full Code]]
	- [[#Lomuto's Quicksort Full Code]]

---

> [!INFO] Resource(s)
> - Visualisation: https://visualgo.net/en/sorting
> - Big-Oh Cheat Sheet: https://www.bigocheatsheet.com/
> - Neural Nine: https://www.youtube.com/watch?v=kLYqVGTKE20
> - Felix Tech Tips: https://www.youtube.com/watch?v=9KBwdDEwal8 ( **I understood trough this video** )
> - Portfolio Courses: https://www.youtube.com/watch?v=0jDiBM68NGU ( *Its actually C code* )
> - Michael Sambol: https://www.youtube.com/watch?v=Hoixgm4-P4M
> - Marie Elaine Califf: https://www.youtube.com/watch?v=1Vl2TB7DoAM

> [!NOTE] Difference Between **Hoare** and **Lumoto** Quicksort Algorithm
> 
> The main **difference** between these two algorithms is the *technique* that they use to sort the array.
> 
> What I mean by "*technique*"; is the way they **manipulate** / *move* data to sort the array.

> [!TIP] 
> Quicksort is just an "*expensive*" and **fast** version of [[Python - Selection Sort | Selection Sort]]!

# Quicksort - Hoare

## Lecturer's Quicksort

As you can see from the above heading; this code that I am going to provide is a direct Python *conversion* of the Pseudocode that my lecturer provided.

- Here is the Python code for sorting ( "*recursively*" ) an array / list using quicksort:

```python
# function to partition the array around a pivot ( last element as pivot )
def partition(arr: list, low: int, high: int) -> int:
    # choose the last element as the pivot
    pivot = arr[high]

    # initialise our pointers
    i = low
    j = high

    # iterate until the two pointers cross
    while i < j:
        # move `i` right until we find an element greater than or equal to pivot
        while arr[i] < pivot:
            i += 1

        # move `j` left until we find an element less than pivot
        while (i < j) and (arr[j] > = pivot):
            j -= 1

        # if pointers have not crossed, swap the elements
        if i < j:
            arr[i], arr[j] = arr[j], arr[i]

    # place the pivot in its correct position
    arr[i], arr[high] = arr[high], arr[i]

    # return the pivot's final position
    return i


# function to recursively sort the array using quicksort
def quicksort(arr: list, low: int, high: int):
    # base case --> subarray has 1 or 0 elements
    if low < high:
        # partition the array and get the pivot's final position
        partition_pos = partition(arr, low, high)

        # recursively sort the left subarray
        quicksort(arr, low, partition_pos - 1)

        # recursively sort the right subarray
        quicksort(arr, partition_pos + 1, high)
```

> [!NOTE]
> The `low` and `high` variable names are well, the **first** / **left-most element** / element found at the **start** of the array and the **last**

In the above code, we *assume* that the pivot is always going to be the element that is found at the **end** of the array / list.

> But is that actually efficient? Does using the *element* at the **end** actually good?

- The answer to the above question is going to be ( *drum-roll* ): Fuck **No**!

> There is always a better way to do something!

Selecting the *element* at the **end** of the array means that its **simple** to *implement* but that does **not** mean its going to yield the best results!

> [!NOTE] Time Complexity = O(n log n)
> - The **overall** *running* time complexity for this function is going to be O(n log n)
> - Best Case: O(n log n)
> - Worst Case: O(n^2) [ $O(n^{2})$ ]
>
> > [!INFO] Recurrence Equation: T(n) = 2T(n/2) + O(n)
> > - The `partition` function scans through the array once: O(n) work at **each** *level*
> > - In the **best** case, the `pivot` splits the array into two ( "*roughly*" ) equal halves
> > 	- Therefore, this means that we are going to have: T(n/2)
> > 	- Given that we also need to "*get*" these arrays *merged*; hence, we are going to get: 2T(n/2)
> > 	- Finally, we need to add O(n) due to the the way that the `partition` function scans and actually **partition** the array
> > - In the **worst case**, the pivot always ends up at one end ( _i.e: an **already** sorted array_ )
> > 	- One subarray has `n - 1` elements and the other has `0` elements
> > 	- Therefore; this means that we are going to have: T(n - 1) + O(n)
> > 	- Again, O(n) is added because of how the `partition` function works
> > - Thus the **running time complexity** ( *in terms of `T(n)`* ) becomes: T(n) = 2T(n/2) + O(n)

## Lecturer' Optimised Quicksort ( Median of Three )

> [!INFO] More Resource(s):
> - Dev Article: https://dev.to/pineapples/writing-a-median-of-three-pivot-helper-for-quicksort-289m

In this case, we are going to use something called 'Median of Three'!

Here, instead of simply using the **last** element as our *pivot* without much thought... We are going to instead do a calculation to find the middle of the array and based on our `low`, `mid` and `high` we are going to use it as our pivot.

This is simply because using an element *closer* to the **middle** of an array is going to sort the array **faster** as we have *less* number "*steps*" to do!

> [!NOTE]
> **Hoare** and **Lumoto** are the actual *partitioning* schemes whereby they are going to split the array accordingly.
> 
> But the 'Median of Three' is a **Pivot Selection Strategy**!
> 
> It has nothing to do with the actual sorting or anything like that... The `paritioning` algorithm is the one that is going to **benefit** from having a better *pivot*.
> 
> > I mean it does "*sort*" the the `low`, `mid` and `high` elements... But it does not sort the actual array ( *obviously* ).

> [!WARNING]
> If you have a sorted array and don't use 'Median of Three'... You are in big trouble!
> 
> The *quicksort* is definitely going to **crash**.
> 
> This is simply because if we have a sorted array, its going to get one *sub-array* **empty**!
> 
> > Its much more dangerous in *low-level* languages like C!

```python
# function to find the index of the median of three elements
def find_median(arr: list, low: int, mid: int, high: int) -> int:
    # get the three values
    a = arr[low]
    b = arr[mid]
    c = arr[high]

    # find the median index
    if (a <= b <= c) or (c <= b <= a):
        return mid
    elif (b <= a <= c) or (c <= a <= b):
        return low
    else:
        return high


# function to swap the median element with the last element ( pivot )
def swap_median(arr: list, median_idx: int, high: int):
    arr[median_idx], arr[high] = arr[high], arr[median_idx]


# function to partition the array around a pivot ( median of three )
def partition(arr: list, low: int, high: int) -> int:
    # find the middle index
    mid = (low + high) // 2

    # find the median index
    median_idx = find_median(arr, low, mid, high)

    # swap middle element with the last element
    swap_median(arr, median_idx, high)

    # choose the last element as the pivot ( now the median )
    pivot = arr[high]

    # initialise the two pointers
    i = low
    j = high

    # iterate until the two pointers cross
    while i < j:
        # move `i` right until we find an element greater than or equal to pivot
        while arr[i] < pivot:
            i += 1

        # move `j` left until we find an element less than pivot
        while (i < j) and (arr[j] > = pivot):
            j -= 1

        # if pointers have not crossed, swap the elements
        if i < j:
            arr[i], arr[j] = arr[j], arr[i]

    # place the pivot in its correct position
    arr[i], arr[high] = arr[high], arr[i]

    # return the pivot's final position
    return i


# function to recursively sort the array using quicksort
def quicksort(arr: list, low: int, high: int):
    # base case: if low > = high, subarray has 1 or 0 elements
    if low < high:
        # partition the array and get the pivot's final position
        partition_pos = partition(arr, low, high)

        # recursively sort the left subarray
        quicksort(arr, low, partition_pos - 1)

        # recursively sort the right subarray
        quicksort(arr, partition_pos + 1, high)
```

> [!NOTE] Time Complexity = O(n log n)
> - The **overall** *running* time complexity for this function is going to be O(n log n)
> - Best Case: O(n log n)
> - Average Case: O(n log n)
> - Worst Case: O(n^2) [ $O(n^{2})$ ]
>
> > [!INFO] Recurrence Equation: T(n) = 2T(n/2) + O(n)
> > - `find_median` looks at exactly 3 elements and performs a constant number of comparisons; therefore: O(1)
> > - `swap_median` performs a single swap, again: O(1)
> > - The `partition` function scans through the entire subarray once → O(n) work at each level
> > - Similarly, the `partition` function is going to result in O(n) because of the *scanning* and *splitting*
> > - In the **best** case, the *Median of Three* pivot produces balanced partitions
> > 	- This gives us: T(n) = 2T(n/2) + O(n)
> > 	- Which resolves to: O(n log n)
> > - In the **worst case**, even the median of three pivot could produce unbalanced partitions
> > 	- This gives us: T(n) = T(n - 1) + O(n)
> > 	- Which resolves to: O(n^2) [ $O(n^{2})$ ]
> > - Compared to the *unoptimised* version, the *Median of Three* **significantly reduces** the probability of *hitting* the worst case
> > 	- The *unoptimised* version hits O(n^2) [ $O(n^{2})$ ] on any already sorted array

# Quicksort - Hoare Further Optimisation

Given that we have the `partition` function that keeps on "*splitting*" our array even when we **little** or **two** elements in the *sub-array*.

This means that quicksort gets very *inefficient* for small array as it has to do a lot of computations just to sort 2 ( *or little* ) elements.

> [!WARNING] Shocker!
> 
> We just said that for little or 2 element array, quicksort becomes *slow*... Well the actually *slow* **bubble sort** function is actually **quicker** to sort 2 elements compared to quicksort!!!
> 
> > What a fucking shock!
> 
> Well, not really a shock, else we would not be waiting to see the codes down below...

## Median of Three and Insertion Sort

The following code is going to use a *modified* **insertion sort** to sort the smaller sub-arrays / sub-lists.

> For more information, you could refer to the '[[Python - Insertion Sort]]' note!

```python
# global variable to hold threshold for switching to insertion sort
THRESHOLD = 10


# modified insertion sort function to sort a sub-arrays created by quicksort
# INFO: "modified" as we are using `low` and `high` instead of array's length
def insertion_sort(arr: list, low: int, high: int):
    # iterate through the whole array / list
    # NOTE: starting with index '1' as a single element is considered to be sorted
    for i in range(low + 1, high + 1):
        # intialise the key at each iteration
        key = arr[i]

        # initialise "current" pointer ==> to track current position
        j = i

        # iterate through the rest of the array swapping as need be with "next" element
        # INFO: the main case for swapping is:
        # 1. pointer `j` should be greater than `low`
        # 2. previous element should be greater than current element `i`
        while (j > low) and (arr[j - 1] > key):
            # shift the two "current" elements
            arr[j] = arr[j - 1]

            # do also decrement the pointer
            j -= 1

        # finally place the key where it belongs
        arr[j] = key


# function to find the index of the median of three elements
def find_median(arr: list, low: int, mid: int, high: int) -> int:
    # get the three values
    a = arr[low]
    b = arr[mid]
    c = arr[high]

    # find the median index
    if (a <= b <= c) or (c <= b <= a):
        return mid
    elif (b <= a <= c) or (c <= a <= b):
        return low
    else:
        return high


# function to swap the median element with the last element ( pivot )
def swap_median(arr: list, median_idx: int, high: int):
    arr[median_idx], arr[high] = arr[high], arr[median_idx]


# function to partition the array around a pivot ( median of three )
def partition(arr: list, low: int, high: int) -> int:
    # find the middle index
    mid = (low + high) // 2

    # find the median index
    median_idx = find_median(arr, low, mid, high)

    # swap middle element with the last element
    swap_median(arr, median_idx, high)

    # choose the last element as the pivot ( now the median )
    pivot = arr[high]

    # initialise the two pointers
    i = low
    j = high

    # iterate until the two pointers cross
    while i < j:
        # move `i` right until we find an element greater than or equal to pivot
        while arr[i] < pivot:
            i += 1

        # move `j` left until we find an element less than pivot
        while (i < j) and (arr[j] > = pivot):
            j -= 1

        # if pointers have not crossed, swap the elements
        if i < j:
            arr[i], arr[j] = arr[j], arr[i]

    # place the pivot in its correct position
    arr[i], arr[high] = arr[high], arr[i]

    # return the pivot's final position
    return i


# function to recursively sort the array using quicksort
def quicksort(arr: list, low: int, high: int):
    # if subarray is small enough, use insertion sort
    if high - low + 1 <= THRESHOLD:
        insertion_sort(arr, low, high)
        return

    # base case: subarray has 1 or 0 elements
    if low < high:
        # partition the array and get the pivot's final position
        partition_pos = partition(arr, low, high)

        # recursively sort the left subarray
        quicksort(arr, low, partition_pos - 1)

        # recursively sort the right subarray
        quicksort(arr, partition_pos + 1, high)
```

## Median of Three and Selection Sort

The following code is going to use a *modified* **selection sort** to sort the smaller sub-arrays / sub-lists.

> For more information, you could refer to the '[[Python - Selection Sort]]' note!

```python
# global variable to hold threshold for switching to selection sort
THRESHOLD = 10


# modified selection sort function to sort sub-arrays created by quicksort
# INFO: "modified" as we are using `low` and `high` instead of array's length
def selection_sort(arr: list, low: int, high: int):
    # iterate through the subarray
    for i in range(low, high + 1):
        # initialise variable to hold index of minimum element at each iteration
        min_idx = i

        # iterate through the rest of the elements found in subarray
        for j in range(i + 1, high + 1):
            # check for minimum element at each iteration
            if arr[j] < arr[min_idx]:
                # new minimum element found ==> change `min_idx`
                min_idx = j

        # swap the required element
        if min_idx != i:
            # NOTE: using Python's tuple thingy to swap
            # else simply use `temp` for other languages
            arr[i], arr[min_idx] = arr[min_idx], arr[i]


# function to find the index of the median of three elements
def find_median(arr: list, low: int, mid: int, high: int) -> int:
    # get the three values
    a = arr[low]
    b = arr[mid]
    c = arr[high]

    # find the median index
    if (a <= b <= c) or (c <= b <= a):
        return mid
    elif (b <= a <= c) or (c <= a <= b):
        return low
    else:
        return high


# function to swap the median element with the last element ( pivot )
def swap_median(arr: list, median_idx: int, high: int):
    arr[median_idx], arr[high] = arr[high], arr[median_idx]


# function to partition the array around a pivot ( median of three )
def partition(arr: list, low: int, high: int) -> int:
    # find the middle index
    mid = (low + high) // 2

    # find the median index
    median_idx = find_median(arr, low, mid, high)

    # swap middle element with the last element
    swap_median(arr, median_idx, high)

    # choose the last element as the pivot ( now the median )
    pivot = arr[high]

    # initialise the two pointers
    i = low
    j = high

    # iterate until the two pointers cross
    while i < j:
        # move `i` right until we find an element greater than or equal to pivot
        while arr[i] < pivot:
            i += 1

        # move `j` left until we find an element less than pivot
        while (i < j) and (arr[j] > = pivot):
            j -= 1

        # if pointers have not crossed, swap the elements
        if i < j:
            arr[i], arr[j] = arr[j], arr[i]

    # place the pivot in its correct position
    arr[i], arr[high] = arr[high], arr[i]

    # return the pivot's final position
    return i


# function to recursively sort the array using quicksort
def quicksort(arr: list, low: int, high: int):
    # if subarray is small enough, use selection sort
    if high - low + 1 <= THRESHOLD:
        selection_sort(arr, low, high)
        return

    # base case: subarray has 1 or 0 elements
    if low < high:
        # partition the array and get the pivot's final position
        partition_pos = partition(arr, low, high)

        # recursively sort the left subarray
        quicksort(arr, low, partition_pos - 1)

        # recursively sort the right subarray
        quicksort(arr, partition_pos + 1, high)
```

# Quicksort - Lomuto

> [!INFO] More Resource(s)
> 
> - GeekForGeeks: https://www.geeksforgeeks.org/dsa/hoares-vs-lomuto-partition-scheme-quicksort/
> - GeekForGeeks: https://www.geeksforgeeks.org/javascript/quick-sortlomuto-partition-visualization-using-javascript/

> [!WARNING] I **don't** really care!
> 
> The only thing you need to know is how Lomuto **moves** / **manipulates** elements to sort them.
> 
> Unlike Hoare's two pointers moving towards each other, Lomuto uses:
> 
> - A **boundary pointer** `i` that *tracks* the last known small element
> - A **scanning pointer** `j` that *scans* left to right through the array
> 
> When `j` finds an element **smaller** than the *pivot*, `i` moves forward and they swap. Once `j` finishes *scanning*, the pivot is placed at its correct position at `i + 1`.
> 
> The key insight is:
> 
> - Hoare: `i` moves *right*, `j` moves *left* **towards** each other
> - Lomuto: `i` and `j` both move *right* **same** direction
> 
> > That's all I am going to say as I don't really care about this one!

```python
# function to partition the array around a pivot ( Lomuto partition scheme )
def partition(arr: list, low: int, high: int) -> int:
    # choose the last element as the pivot
    pivot = arr[high]

    # initialise the boundary pointer
    i = low - 1

    # iterate through the array from low to high
    for j in range(low, high):
        # if current element is smaller than or equal to pivot
        if arr[j] <= pivot:
            # move the boundary pointer forward
            i += 1
            # swap the elements
            arr[i], arr[j] = arr[j], arr[i]

    # place the pivot in its correct position
    arr[i + 1], arr[high] = arr[high], arr[i + 1]

    # return the pivot's final position
    return i + 1


# function to recursively sort the array using quicksort ( Lomuto )
def quicksort(arr: list, low: int, high: int):
    # base case: subarray has 1 or 0 elements
    if low < high:
        # partition the array and get the pivot's final position
        partition_pos = partition(arr, low, high)

        # recursively sort the left subarray
        quicksort(arr, low, partition_pos - 1)

        # recursively sort the right subarray
        quicksort(arr, partition_pos + 1, high)
```

---

# Categories Which Insertion Sort Falls Into

| Terminology | Standard Quick Sort | With Median of Three ( Only ) | Hybrid ( Median of Three + Insertion / Selection Sort ) |
| ----------- | ------------------- | -------------------- | -------------------------- |
| Storage Location | Internal | Internal | Internal |
| Access Method | Array-based ( Random ) | Array-based ( Random ) | Array-based ( Random ) |
| Logic Type | Comparison-based | Comparison-based | Comparison-based |
| Relative Order | Unstable | Unstable | Unstable |
| Space Usage | Out-of-place | Out-of-place | Out-of-place |

---

# Quicksort Full Example Codes

Well, what can I say apart that I am going to be writing "*full*" example codes from **each** of the above functions.

## Lecturer's Quicksort Full Code

```python
# import the `randint` function from the 'random' module
from random import randint


# function to partition the array around a pivot ( last element as pivot )
def partition(arr: list, low: int, high: int) -> int:
    # choose the last element as the pivot
    pivot = arr[high]

    # initialise our pointers
    i = low
    j = high

    # iterate until the two pointers cross
    while i < j:
        # move `i` right until we find an element greater than or equal to pivot
        while arr[i] < pivot:
            i += 1

        # move `j` left until we find an element less than pivot
        while (i < j) and (arr[j] > = pivot):
            j -= 1

        # if pointers have not crossed, swap the elements
        if i < j:
            arr[i], arr[j] = arr[j], arr[i]

    # place the pivot in its correct position
    arr[i], arr[high] = arr[high], arr[i]

    # return the pivot's final position
    return i


# function to recursively sort the array using quicksort
def quicksort(arr: list, low: int, high: int):
    # base case --> subarray has 1 or 0 elements
    if low < high:
        # partition the array and get the pivot's final position
        partition_pos = partition(arr, low, high)

        # recursively sort the left subarray
        quicksort(arr, low, partition_pos - 1)

        # recursively sort the right subarray
        quicksort(arr, partition_pos + 1, high)


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
    quicksort(list_int, 0, len(list_int) - 1)
    quicksort(list_float, 0, len(list_float) - 1)
    quicksort(list_chars, 0, len(list_chars) - 1)

    print("\n" + "-" * 50, "\n")

    # display list after sorting
    print(f"Integers List After Sorting: {list_int}")
    print(f"'Float' List After Sorting: {list_float}")
    print(f"Characters List After Sorting: {list_chars}")


if __name__ == "__main__":
    main()
```

## Lecturer's Optimised ( Median of Three ) Quicksort Full Code

```python
# import the `randint` function from the 'random' module
from random import randint


# function to find the index of the median of three elements
def find_median(arr: list, low: int, mid: int, high: int) -> int:
    # get the three values
    a = arr[low]
    b = arr[mid]
    c = arr[high]

    # find the median index
    if (a <= b <= c) or (c <= b <= a):
        return mid
    elif (b <= a <= c) or (c <= a <= b):
        return low
    else:
        return high


# function to swap the median element with the last element ( pivot )
def swap_median(arr: list, median_idx: int, high: int):
    arr[median_idx], arr[high] = arr[high], arr[median_idx]


# function to partition the array around a pivot ( median of three )
def partition(arr: list, low: int, high: int) -> int:
    # find the middle index
    mid = (low + high) // 2

    # find the median index
    median_idx = find_median(arr, low, mid, high)

    # swap middle element with the last element
    swap_median(arr, median_idx, high)

    # choose the last element as the pivot ( now the median )
    pivot = arr[high]

    # initialise the two pointers
    i = low
    j = high

    # iterate until the two pointers cross
    while i < j:
        # move `i` right until we find an element greater than or equal to pivot
        while arr[i] < pivot:
            i += 1

        # move `j` left until we find an element less than pivot
        while (i < j) and (arr[j] > = pivot):
            j -= 1

        # if pointers have not crossed, swap the elements
        if i < j:
            arr[i], arr[j] = arr[j], arr[i]

    # place the pivot in its correct position
    arr[i], arr[high] = arr[high], arr[i]

    # return the pivot's final position
    return i


# function to recursively sort the array using quicksort
def quicksort(arr: list, low: int, high: int):
    # base case: if low > = high, subarray has 1 or 0 elements
    if low < high:
        # partition the array and get the pivot's final position
        partition_pos = partition(arr, low, high)

        # recursively sort the left subarray
        quicksort(arr, low, partition_pos - 1)

        # recursively sort the right subarray
        quicksort(arr, partition_pos + 1, high)


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
    quicksort(list_int, 0, len(list_int) - 1)
    quicksort(list_float, 0, len(list_float) - 1)
    quicksort(list_chars, 0, len(list_chars) - 1)

    print("\n" + "-" * 50, "\n")

    # display list after sorting
    print(f"Integers List After Sorting: {list_int}")
    print(f"'Float' List After Sorting: {list_float}")
    print(f"Characters List After Sorting: {list_chars}")


if __name__ == "__main__":
    main()
```

## Optimised ( Median Of Three + Insertion Sort ) Quicksort Full Code

```python
# import the `randint` function from the 'random' module
from random import randint

# global variable to hold threshold for switching to insertion sort
THRESHOLD = 10


# modified insertion sort function to sort a sub-arrays created by quicksort
# INFO: "modified" as we are using `low` and `high` instead of array's length
def insertion_sort(arr: list, low: int, high: int):
    # iterate through the whole array / list
    # NOTE: starting with index '1' as a single element is considered to be sorted
    for i in range(low + 1, high + 1):
        # intialise the key at each iteration
        key = arr[i]

        # initialise "current" pointer ==> to track current position
        j = i

        # iterate through the rest of the array swapping as need be with "next" element
        # INFO: the main case for swapping is:
        # 1. pointer `j` should be greater than `low`
        # 2. previous element should be greater than current element `i`
        while (j > low) and (arr[j - 1] > key):
            # shift the two "current" elements
            arr[j] = arr[j - 1]

            # do also decrement the pointer
            j -= 1

        # finally place the key where it belongs
        arr[j] = key


# function to find the index of the median of three elements
def find_median(arr: list, low: int, mid: int, high: int) -> int:
    # get the three values
    a = arr[low]
    b = arr[mid]
    c = arr[high]

    # find the median index
    if (a <= b <= c) or (c <= b <= a):
        return mid
    elif (b <= a <= c) or (c <= a <= b):
        return low
    else:
        return high


# function to swap the median element with the last element ( pivot )
def swap_median(arr: list, median_idx: int, high: int):
    arr[median_idx], arr[high] = arr[high], arr[median_idx]


# function to partition the array around a pivot ( median of three )
def partition(arr: list, low: int, high: int) -> int:
    # find the middle index
    mid = (low + high) // 2

    # find the median index
    median_idx = find_median(arr, low, mid, high)

    # swap middle element with the last element
    swap_median(arr, median_idx, high)

    # choose the last element as the pivot ( now the median )
    pivot = arr[high]

    # initialise the two pointers
    i = low
    j = high

    # iterate until the two pointers cross
    while i < j:
        # move `i` right until we find an element greater than or equal to pivot
        while arr[i] < pivot:
            i += 1

        # move `j` left until we find an element less than pivot
        while (i < j) and (arr[j] > = pivot):
            j -= 1

        # if pointers have not crossed, swap the elements
        if i < j:
            arr[i], arr[j] = arr[j], arr[i]

    # place the pivot in its correct position
    arr[i], arr[high] = arr[high], arr[i]

    # return the pivot's final position
    return i


# function to recursively sort the array using quicksort
def quicksort(arr: list, low: int, high: int):
    # if subarray is small enough, use insertion sort
    if high - low + 1 <= THRESHOLD:
        insertion_sort(arr, low, high)
        return

    # base case: subarray has 1 or 0 elements
    if low < high:
        # partition the array and get the pivot's final position
        partition_pos = partition(arr, low, high)

        # recursively sort the left subarray
        quicksort(arr, low, partition_pos - 1)

        # recursively sort the right subarray
        quicksort(arr, partition_pos + 1, high)


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
    quicksort(list_int, 0, len(list_int) - 1)
    quicksort(list_float, 0, len(list_float) - 1)
    quicksort(list_chars, 0, len(list_chars) - 1)

    print("\n" + "-" * 50, "\n")

    # display list after sorting
    print(f"Integers List After Sorting: {list_int}")
    print(f"'Float' List After Sorting: {list_float}")
    print(f"Characters List After Sorting: {list_chars}")


if __name__ == "__main__":
    main()
```

## Optimised ( Median Of Three + Selection Sort ) Quicksort Full Code

```python
# import the `randint` function from the 'random' module
from random import randint

# global variable to hold threshold for switching to selection sort
THRESHOLD = 10


# modified selection sort function to sort sub-arrays created by quicksort
# INFO: "modified" as we are using `low` and `high` instead of array's length
def selection_sort(arr: list, low: int, high: int):
    # iterate through the subarray
    for i in range(low, high + 1):
        # initialise variable to hold index of minimum element at each iteration
        min_idx = i

        # iterate through the rest of the elements found in subarray
        for j in range(i + 1, high + 1):
            # check for minimum element at each iteration
            if arr[j] < arr[min_idx]:
                # new minimum element found ==> change `min_idx`
                min_idx = j

        # swap the required element
        if min_idx != i:
            # NOTE: using Python's tuple thingy to swap
            # else simply use `temp` for other languages
            arr[i], arr[min_idx] = arr[min_idx], arr[i]


# function to find the index of the median of three elements
def find_median(arr: list, low: int, mid: int, high: int) -> int:
    # get the three values
    a = arr[low]
    b = arr[mid]
    c = arr[high]

    # find the median index
    if (a <= b <= c) or (c <= b <= a):
        return mid
    elif (b <= a <= c) or (c <= a <= b):
        return low
    else:
        return high


# function to swap the median element with the last element ( pivot )
def swap_median(arr: list, median_idx: int, high: int):
    arr[median_idx], arr[high] = arr[high], arr[median_idx]


# function to partition the array around a pivot ( median of three )
def partition(arr: list, low: int, high: int) -> int:
    # find the middle index
    mid = (low + high) // 2

    # find the median index
    median_idx = find_median(arr, low, mid, high)

    # swap middle element with the last element
    swap_median(arr, median_idx, high)

    # choose the last element as the pivot ( now the median )
    pivot = arr[high]

    # initialise the two pointers
    i = low
    j = high

    # iterate until the two pointers cross
    while i < j:
        # move `i` right until we find an element greater than or equal to pivot
        while arr[i] < pivot:
            i += 1

        # move `j` left until we find an element less than pivot
        while (i < j) and (arr[j] > = pivot):
            j -= 1

        # if pointers have not crossed, swap the elements
        if i < j:
            arr[i], arr[j] = arr[j], arr[i]

    # place the pivot in its correct position
    arr[i], arr[high] = arr[high], arr[i]

    # return the pivot's final position
    return i


# function to recursively sort the array using quicksort
def quicksort(arr: list, low: int, high: int):
    # if subarray is small enough, use selection sort
    if high - low + 1 <= THRESHOLD:
        selection_sort(arr, low, high)
        return

    # base case: subarray has 1 or 0 elements
    if low < high:
        # partition the array and get the pivot's final position
        partition_pos = partition(arr, low, high)

        # recursively sort the left subarray
        quicksort(arr, low, partition_pos - 1)

        # recursively sort the right subarray
        quicksort(arr, partition_pos + 1, high)


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
    quicksort(list_int, 0, len(list_int) - 1)
    quicksort(list_float, 0, len(list_float) - 1)
    quicksort(list_chars, 0, len(list_chars) - 1)

    print("\n" + "-" * 50, "\n")

    # display list after sorting
    print(f"Integers List After Sorting: {list_int}")
    print(f"'Float' List After Sorting: {list_float}")
    print(f"Characters List After Sorting: {list_chars}")


if __name__ == "__main__":
    main()
```

## Lomuto's Quicksort Full Code

```python
# import the `randint` function from the 'random' module
from random import randint


# function to partition the array around a pivot ( Lomuto partition scheme )
def partition(arr: list, low: int, high: int) -> int:
    # choose the last element as the pivot
    pivot = arr[high]

    # initialise the boundary pointer
    i = low - 1

    # iterate through the array from low to high
    for j in range(low, high):
        # if current element is smaller than or equal to pivot
        if arr[j] <= pivot:
            # move the boundary pointer forward
            i += 1
            # swap the elements
            arr[i], arr[j] = arr[j], arr[i]

    # place the pivot in its correct position
    arr[i + 1], arr[high] = arr[high], arr[i + 1]

    # return the pivot's final position
    return i + 1


# function to recursively sort the array using quicksort ( Lomuto )
def quicksort(arr: list, low: int, high: int):
    # base case: subarray has 1 or 0 elements
    if low < high:
        # partition the array and get the pivot's final position
        partition_pos = partition(arr, low, high)

        # recursively sort the left subarray
        quicksort(arr, low, partition_pos - 1)

        # recursively sort the right subarray
        quicksort(arr, partition_pos + 1, high)


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
    quicksort(list_int, 0, len(list_int) - 1)
    quicksort(list_float, 0, len(list_float) - 1)
    quicksort(list_chars, 0, len(list_chars) - 1)

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