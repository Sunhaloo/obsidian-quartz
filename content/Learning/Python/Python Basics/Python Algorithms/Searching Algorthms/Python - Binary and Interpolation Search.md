---
id: Python - Binary and Interpolation Search
aliases: Binary and Interpolation Search in Python
tags:
  - algos
  - arrays
  - divide-and-conquer
  - dsa
  - lists
  - python
  - searching
author: S.Sunhaloo
date: 2026-04-24
status: Completed
---

## List of Contents

- [[#Binary Search]]
	- [[#Iterative Version - Binary Search]]
	- [[#Recursive Version - Binary Search]]
- [[#Interpolation Search]]
	- [[#Iterative Version - Interpolation Search]]
	- [[#Recursive Version - Interpolation Search]]
- [[#Binary Search Full Example Code]]
	- [[#Iterative Binary Search]]
	- [[#Recursive Binary Search]]
- [[#Interpolation Search Full Example Code]]
	- [[#Iterative Interpolation Search]]
	- [[#Recursive Interpolation Search]]

---

> [!INFO] Resource(s)
> - NeetCode: https://www.youtube.com/watch?v=s4DPM8ct1pI

# Binary Search

Compared to our [[Python - Linear Search | Linear Search]] algorithm; the Binary Search algorithm is much, much faster compared to our Linear Search!

This is because it **divides** the whole array in **half** each time that it does **not** find the *target* element.

But the catch is that the array needs to be **sorted first** in order to split the array into a "*high*" and "*low*" sub-arrays.

> Where the "*low*" sub-array's elements is smaller then the "*high*" sub-arrays's elements.

This ways, the algorithms know where to check if the *target* is **not** found in the *middle* at the first check.

## Iterative Version - Binary Search

> [!WARNING] Sort the array / list first!
> 
> Again, like we have been saying; the array / list needs to be **sorted first** in order to be able to use the Binary Search algorithm.

```python
# binary search function to find a specific element
def binary_search(arr: list, target) -> int:
    # intialise our left - low and right - high pointers
    low = 0
    high = len(arr) - 1

    # iterate through search space while valid
    while low <= high:
        # find the middle index of array / list
        # NOTE: `(low + high) // 2` works extremely well in Python,
        # but can cause 'Integer Overflow' in languages like Java or C
        # therefore, simply remember this following below
        middle_idx = low + (high - low) // 2

        # check if the middle element is the target
        if arr[middle_idx] == target:
            return middle_idx

        # if the `target` element if found greater than middle element
        elif arr[middle_idx] < target:
            # completely eliminate the bottom - left part of array
            low = middle_idx + 1

        # if the `target` element if found less than middle element
        else:
            # completely eliminate the top - right part of array
            high = middle_idx - 1

    # if the `target` was not found
    return -1
```

> [!TIP] Time Complexity = O(log n)
> - The **overall** *running* time complexity is **O(log n)**
> - Best Case: O(1) - Occurs when the `target` is found in the **middle** on first check
> - Worst Case: O(log n) - Occurs when we keep halving the search range until the target is not found

## Recursive Version - Binary Search

As you are already know, most of the algorithms which have a *recursive* version are normally **slower** than their *iterative* counter-parts!

This is due to the way that *recursive* functions use **memory** as they have to call the function again and again!

> It basically has an O(log n) space complexity compared to O(1) space complexity for the iterative version.

```python
# recursive binary search function to find a specific element
def binary_search_recursive(arr: list[int], target: int, low: int, high: int) -> int:
    # base case --> search space is exhausted ==> `target` has not been found
    if low > high:
        return -1

    # calculate the middle index
    middle_idx = low + (high - low) // 2

    # check if the middle element is the target
    if arr[middle_idx] == target:
        return middle_idx

	# if the `target` element if found greater than middle element
    elif arr[middle_idx] < target:
        # completely eliminate the bottom - left part of array
        return binary_search_recursive(arr, target, middle_idx + 1, high)

	# if the `target` element if found less than middle element
    else:
        # completely eliminate the top - right part of array
        return binary_search_recursive(arr, target, low, middle_idx - 1)
```

---

# Interpolation Search

> What is 'Interpolation Search' doing here?

What you simply should know its that Interpolation Search is simply a **better** Binary Search!

If the values **evenly spaced out**; meaning that the *difference* between the elements ( *or values in our case* ) are similar across the array; then Interpolation Search is best used here.

From what I see and understand the way the we *move* our pointers and other things is the **exact same** as our Binary Search. The **difference** is the way that we are calculating the `mid` value!

```console
# binary search - middle value calculation
mid = (low + high) // 2
-----------------------------
mid = low + (high - low) // 2

# interpolation search - middle value calculation
mid = low + ((target - arr[low]) * (high - low) // (arr[high] - arr[low]))
```

## Iterative Version - Interpolation Search

```python
# interpolation search function to find a specific element
def interpolation_search(arr: list, target) -> int:
    # intialise our left - low and right - high pointers
    low = 0
    high = len(arr) - 1

    # iterate through search space while valid
    while low <= high and arr[low] <= target <= arr[high]:
        # WARNING: guard against division by zero error
        if arr[low] == arr[high]:
            if arr[low] == target:
                return low
            return -1

        # find the middle index of array / list
        # INFO: as you can see we have updated the `middle_idx` calculation to
        # use the interpolation search's "formula"
        middle_idx = low + (
            (target - arr[low]) * (high - low) // (arr[high] - arr[low])
        )

        # check if the middle element is the target
        if arr[middle_idx] == target:
            return middle_idx

        # if the `target` element if found greater than middle element
        elif arr[middle_idx] < target:
            # completely eliminate the bottom - left part of array
            low = middle_idx + 1

        # if the `target` element if found less than middle element
        else:
            # completely eliminate the top - right part of array
            high = middle_idx - 1

    # if the `target` was not found
    return -1
```

> [!TIP] Time Complexity = O(log log n) average
> - The **overall** *running* time complexity is **O(log log n)** on uniform data
> - Best Case: O(1) - Occurs when target estimated exactly on first *probe*
> - Worst Case: O(n) - Occurs when elements / data is skewed, formula gives poor estimates

## Recursive Version - Interpolation Search

Again, this is basically the *recursive* function of the above *iterative* Interpolation Search function.

```python
# recursive interpolation search function to find a specific element
def interpolation_search_recursive(
    arr: list[int], target: int, low: int, high: int
) -> int:
    # base case --> search space is exhausted / target out of bounds
    if low > high or not arr[low] <= target <= arr[high]:
        return -1

    # WARNING: guard against division by zero error
    if arr[low] == arr[high]:
        if arr[low] == target:
            return low
        return -1

    # interpolation formula to estimate position of target
    middle_idx = low + ((target - arr[low]) * (high - low) // (arr[high] - arr[low]))

    # check if the middle value is the target
    if arr[middle_idx] == target:
        return middle_idx

    # if the `target` value is found greater than middle value
    elif arr[middle_idx] < target:
        # completely eliminate the bottom - left part of array
        return interpolation_search_recursive(arr, target, middle_idx + 1, high)

    # if the `target` value is found less than middle value
    else:
        # completely eliminate the top - right part of array
        return interpolation_search_recursive(arr, target, low, middle_idx - 1)
```

---

# Binary Search Full Example Code

## Iterative Binary Search

> Here I simply used `middle_idx = (low + high) // 2` because its more *Pythonic*!

```python
# binary search function to find a specific value
def binary_search(arr: list, target) -> int:
    # intialise our left - low and right - high pointers
    low = 0
    high = len(arr) - 1

    # iterate through search space while valid
    while low <= high:
        # find the middle index of array / list
        # NOTE: `(low + high) // 2` works extremely well in Python,
        # but can cause 'Integer Overflow' in languages like Java or C
        # therefore, simply remember this following below
        middle_idx = low + (high - low) // 2

        # check if the middle value is the target
        if arr[middle_idx] == target:
            return middle_idx

        # if the `target` value is found greater than middle value
        elif arr[middle_idx] < target:
            # completely eliminate the bottom - left part of array
            low = middle_idx + 1

        # if the `target` value is found less than middle value
        else:
            # completely eliminate the top - right part of array
            high = middle_idx - 1

    # if the `target` was not found
    return -1


# our main function
def main():
    # our integer list
    int_list: list[int] = [1, 4, 11, 16, 44, 55, 63]

    print(f"`int_list` Array: {int_list}\n")

    # call the binary search function on different target
    print(f"Target Value: 0 --> {binary_search(int_list, 0)}")
    print(f"Target Value: 1 --> {binary_search(int_list, 1)}")
    print(f"Target Value: 16 --> {binary_search(int_list, 16)}")
    print(f"Target Value: 63 --> {binary_search(int_list, 63)}")
    print(f"Target Value: 77 --> {binary_search(int_list, 77)}")


if __name__ == "__main__":
    main()
```

## Recursive Binary Search

```python
# recursive binary search function to find a specific value
def binary_search_recursive(arr: list[int], target: int, low: int, high: int) -> int:
    # base case --> search space is exhausted ==> `target` has not been found
    if low > high:
        return -1

    # calculate the middle index
    middle_idx = low + (high - low) // 2

    # check if the middle value is the target
    if arr[middle_idx] == target:
        return middle_idx

	# if the `target` element if found greater than middle element
    elif arr[middle_idx] < target:
        # completely eliminate the bottom - left part of array
        return binary_search_recursive(arr, target, middle_idx + 1, high)

	# if the `target` element if found less than middle element
    else:
        # completely eliminate the top - right part of array
        return binary_search_recursive(arr, target, low, middle_idx - 1)


# our main function
def main():
    # our integer list
    int_list: list[int] = [1, 4, 11, 16, 44, 55, 63]

    print(f"`int_list` Array: {int_list}\n")

    # call the binary search recursive function on different target
    print(
        f"Target Value: 0 --> {binary_search_recursive(int_list, 0, 0, len(int_list) - 1)}"
    )

    print(
        f"Target Value: 1 --> {binary_search_recursive(int_list, 1, 0, len(int_list) - 1)}"
    )
    print(
        f"Target Value: 16 --> {binary_search_recursive(int_list, 16, 0, len(int_list) - 1)}"
    )
    print(
        f"Target Value: 63 --> {binary_search_recursive(int_list, 63, 0, len(int_list) - 1)}"
    )
    print(
        f"Target Value: 77 --> {binary_search_recursive(int_list, 77, 0, len(int_list) - 1)}"
    )


if __name__ == "__main__":
    main()
```

---

# Interpolation Search Full Example Code

## Iterative Interpolation Search

```python
# interpolation search function to find a specific value
def interpolation_search(arr: list, target) -> int:
    # intialise our left - low and right - high pointers
    low = 0
    high = len(arr) - 1

    # iterate through search space while valid
    while low <= high and arr[low] <= target <= arr[high]:
        # WARNING: guard against division by zero error
        if arr[low] == arr[high]:
            if arr[low] == target:
                return low
            return -1

        # find the middle index of array / list
        # INFO: as you can see we have updated the `middle_idx` calculation to
        # use the interpolation search's "formula"
        middle_idx = low + (
            (target - arr[low]) * (high - low) // (arr[high] - arr[low])
        )

        # check if the middle value is the target
        if arr[middle_idx] == target:
            return middle_idx

        # if the `target` value is found greater than middle value
        elif arr[middle_idx] < target:
            # completely eliminate the bottom - left part of array
            low = middle_idx + 1

        # if the `target` value is found less than middle value
        else:
            # completely eliminate the top - right part of array
            high = middle_idx - 1

    # if the `target` was not found
    return -1


# our main function
def main():
    # our integer list
    int_list: list[int] = [1, 4, 11, 16, 44, 55, 63]

    print(f"`int_list` Array: {int_list}\n")

    # call the interpolation search function on different target
    print(f"Target Value: 0 --> {interpolation_search(int_list, 0)}")
    print(f"Target Value: 1 --> {interpolation_search(int_list, 1)}")
    print(f"Target Value: 16 --> {interpolation_search(int_list, 16)}")
    print(f"Target Value: 63 --> {interpolation_search(int_list, 63)}")
    print(f"Target Value: 77 --> {interpolation_search(int_list, 77)}")


if __name__ == "__main__":
    main()
```

## Recursive Interpolation Search

```python
# recursive interpolation search function to find a specific value
def interpolation_search_recursive(
    arr: list[int], target: int, low: int, high: int
) -> int:
    # base case --> search space is exhausted / target out of bounds
    if low > high or not arr[low] <= target <= arr[high]:
        return -1

    # WARNING: guard against division by zero error
    if arr[low] == arr[high]:
        if arr[low] == target:
            return low
        return -1

    # interpolation formula to estimate position of target
    middle_idx = low + ((target - arr[low]) * (high - low) // (arr[high] - arr[low]))

    # check if the middle value is the target
    if arr[middle_idx] == target:
        return middle_idx

    # if the `target` value is found greater than middle value
    elif arr[middle_idx] < target:
        # completely eliminate the bottom - left part of array
        return interpolation_search_recursive(arr, target, middle_idx + 1, high)

    # if the `target` value is found less than middle value
    else:
        # completely eliminate the top - right part of array
        return interpolation_search_recursive(arr, target, low, middle_idx - 1)


# our main function
def main():
    # our integer list
    int_list: list[int] = [1, 4, 11, 16, 44, 55, 63]

    print(f"`int_list` Array: {int_list}\n")

    # call the interpolation search recursive function on different target
    print(
        f"Target Value: 0 --> {interpolation_search_recursive(int_list, 0, 0, len(int_list) - 1)}"
    )
    print(
        f"Target Value: 1 --> {interpolation_search_recursive(int_list, 1, 0, len(int_list) - 1)}"
    )
    print(
        f"Target Value: 16 --> {interpolation_search_recursive(int_list, 16, 0, len(int_list) - 1)}"
    )
    print(
        f"Target Value: 63 --> {interpolation_search_recursive(int_list, 63, 0, len(int_list) - 1)}"
    )
    print(
        f"Target Value: 77 --> {interpolation_search_recursive(int_list, 77, 0, len(int_list) - 1)}"
    )


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