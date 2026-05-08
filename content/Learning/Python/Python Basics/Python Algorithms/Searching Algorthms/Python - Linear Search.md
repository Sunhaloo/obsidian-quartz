---
id: Python - Linear Search
aliases: Linear Search in Python
tags:
  - algos
  - arrays
  - dsa
  - lists
  - python
  - searching
author: S.Sunhaloo
date: 2026-04-22
status: Completed
---

## List of Contents

- [[#Linear Search]]
	- [[#Simple Linear Search]]
	- [[#Find All Occurrences]]
- [[#Linear Search Full Example Code]]
	- [[#Finding One Specific Element]]
	- [[#Finding All Occurrences Of One Specific ELement]]

---

# Linear Search

One of, if not the **easiest** searching algorithm found in the whole world!

It also has a couple of **advantages** like:

- Simple and Easy to learn and implement
- Works on all type of arrays ( Sorted and Unsorted )

But its also the shittiest searching algorithm to ever exists as its **slow** as hell!

Given that nature of how it *moves* the pointer to search for an element inside the array... If the array / list has a **massive** size.

> Then you are basically going to be waiting forever for it to complete.

## Simple Linear Search

This is a simple Linear Search algorithm that is going to work on most arrays!

```python
# linear search function to find a specific element
def linear_search(arr: list, target) -> int:
    # iterate through the elements in the array
    for i in range(len(arr)):
        # check if current element is same as `target`
        if arr[i] == target:
            # meaning that element has been found ==> return the index
            return i

    # if target has not been found ==> simply return -1
    return -1
```

> [!TIP] Time Complexity = O(n)
> - The **overall** *running* time complexity is **O(n)**
> - Best Case: O(1) - Occurs when the `target` is found at the **first** index of array
> - Worst Case: O(n) - Occurs when the `target` is found at the **last** index of array

> [!WARNING] The Problem...
> 
> The above function is going to going *try* find the element / value that you input. But what is there are **many** *instances* / *occurrences* for that **target element / value**?
> 
> Because in the above code as soon as it finds the `target`... Its **not** going to bother continuing to search for more!
> 
> This is why we have some **variants** for the Linear Search algorithm.

## Find All Occurrences

The following code below is going to show you how to find **all** the *occurrences* of a `target` element.

```python
# linear search function to find all occurrences of a specific element
def linear_search_all(arr: list, target) -> list[int]:
    # create a list of integer ==> to hold indices for `target` value
    target_indices: list[int] = []

    # iterate through the elements in the array
    for i in range(len(arr)):
        # check if current element is same as `target`
        if arr[i] == target:
            # meaning that element has been found ==> add index to `target_indices`
            target_indices.append(i)

    # finally return the list of indices
    # NOTE: you could do a little check for `target_indices` is empty
    # where you are calling the function
    return target_indices
```

---

# Linear Search Full Example Code

## Finding One Specific Element

```python
# linear search function to find a specific value
def linear_search(arr: list, target) -> int:
    # iterate through the values in the array
    for i in range(len(arr)):
        # check if current value is same as `target`
        if arr[i] == target:
            # meaning that value has been found ==> return the index
            return i

    # if target has not been found ==> simply return -1
    return -1


# our main function
def main():
	# our integer list
    int_list: list[int] = [9, 8, 1, 6, 7, 4, 7, 1, 1, 0]

    print(f"`int_list` Array: {int_list}\n")

	# call the linear search function on different "target"
    print(f"Target Value: 0 --> {linear_search(int_list, 0)}")
    print(f"Target Value: 1 --> {linear_search(int_list, 1)}")
    print(f"Target Value: 7 --> {linear_search(int_list, 7)}")
    print(f"Target Value: 9 --> {linear_search(int_list, 9)}")
    print(f"Target Value: 10 --> {linear_search(int_list, 10)}")

    print("\n" + "-" * 60, "\n")

    # INFO: for the last one we could do something like
    if not linear_search(int_list, 10):
        print("\n\tTarget Value 10 Has Not Been Found!!!\n")


if __name__ == "__main__":
    main()
```

## Finding All Occurrences Of One Specific Element

```python
# linear search function to find all occurrences of a specific value
def linear_search_all(arr: list, target) -> list[int]:
    # create a list of integer ==> to hold indices for `target` value
    target_indices: list[int] = []

    # iterate through the values in the array
    for i in range(len(arr)):
        # check if current value is same as `target`
        if arr[i] == target:
            # meaning that value has been found ==> add index to `target_indices`
            target_indices.append(i)

    # finally return the list of indices
    # NOTE: you could do a little check for `target_indices` is empty
    # where you are calling the function
    return target_indices


# our main function
def main():
	# our integer list
    int_list: list[int] = [9, 8, 1, 6, 7, 4, 7, 1, 1, 0]

    print(f"`int_list` Array: {int_list}\n")

	# call the linear search function on different "target"
    print(f"Target Value: 0 --> {linear_search_all(int_list, 0)}")
    print(f"Target Value: 1 --> {linear_search_all(int_list, 1)}")
    print(f"Target Value: 7 --> {linear_search_all(int_list, 7)}")
    print(f"Target Value: 9 --> {linear_search_all(int_list, 9)}")
    print(f"Target Value: 10 --> {linear_search_all(int_list, 10)}")

    print("\n" + "-" * 60, "\n")

    # INFO: for the last one we could do something like
    if not linear_search_all(int_list, 10):
        print("\n\tTarget Value 10 Has Not Been Found!!!\n")


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