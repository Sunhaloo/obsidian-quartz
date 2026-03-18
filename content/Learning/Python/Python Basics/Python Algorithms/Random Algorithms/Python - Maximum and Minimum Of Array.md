---
id: Python - Maximum and Minimum Of Array
aliases: Find the maximum and minimum element / value from an array
tags:
  - algos
  - arrays
  - brute-force
  - divide-and-conquer
  - dsa
  - lists
  - python
author: S.Sunhaloo
date: 2026-02-20
status: Completed
---

## List of Contents

- [[#Naive Inefficient Approach]]
- [[#Divide and Conquer Sub-Optimal Approach]]
- [[#Pairwise Optimal Approach]]

---

> [!NOTE] Summary: What You Actually Need To Learn!
> 
> - [[#Naive Inefficient Approach]]
> - [[#Divide and Conquer Sub-Optimal Approach]]

# Naive Inefficient Approach

> [!INFO] Resource(s)
> 
> - LeetCode Discussions: https://leetcode.com/discuss/post/3593060/maximum-and-minimum-element-in-an-array-2n6ud/

Here is a simple, "*normal*" algorithm to find the **minimum** and the **maximum** element / value of an integer array!

```python
# function to find the maximum and minimum value of array
def min_max_arr(arr: list[int]):
    # intialise variables
    min = arr[0]
    max = arr[0]

    # find the minimum and maximum value from array through iteration
    for i in range(len(arr)):
        if arr[i] < min:
            # get the new minimum value into the variable
            min = arr[i]

        elif arr[i] > max:
            # get the new maximum value into the variable
            max = arr[i]

    # return the required values
    return max, min
```

> We could also have returned something like `[min, max]` ( *a list / tuple* )!

> [!NOTE] Time Complexity = O(n)
> 
> - The **overall** *running* time complexity for this function is going to be O(n)
> - Best Case: O(n)
> - Worst Case: O(n)
> 	- Both O(n) in this case as algorithm **needs** to iterate through `for` loop at least once to check for values!

> [!NOTE] Number of Comparisons = 2n - 2
> 
> - We have 1 `for` loop that runs `n - 1` times
> - We are doing 2 comparisons with `if arr[i] < min` and `elif arr[i] > max`
> 
> > Therefore we have $2 \times (n -1)$ = 2n - 1 <--

## Naive Approach: Full Example Code

This is a full example code using the 'Naive Approach' to find the maximum and minimum element in an array!

> [!TIP]
> I have updated the above code to optimise it just of *tad bit* for extremely **rare** cases!
> 
> > Its "*rare*" but **not** "*impossible*"!

```python
from random import randint


# function to find the maximum and minimum value of array
def max_min_arr(arr: list[int]):
    # check if length of array is '0'
    if len(arr) == 0:
        return None, None

    # intialise variables
    min = arr[0]
    max = arr[0]

    # check if the length of the array is '1'
    if len(arr) == 1:
        return max, min

    # find the minimum and maximum value from array through iteration
    for i in range(1, len(arr)):
        if arr[i] < min:
            # get the new minimum value into the variable
            min = arr[i]

        elif arr[i] > max:
            # get the new maximum value into the variable
            max = arr[i]

    # return the required values
    return max, min


# our main function
def main():
    # find the minimum and maximum number for different numbers in array / list
    for i in range(5):
        # create list of integers of random numbers
        int_nums: list[int] = [randint(0, 9) for i in range(randint(0, 10))]

        print("\n" + "-" * 50, "\n")

        # display the rray to the user
        print(f"Array / List: {int_nums}")

        # call the function to find the maximum and minimum value
        maximum_arr_value, minimum_arr_value = max_min_arr(int_nums)

        # display the minimum and maximum value from the array / list
        print(f"\nMaximum Value: {maximum_arr_value}")
        print(f"Minimum Value: {minimum_arr_value}")


if __name__ == "__main__":
    main()
```

- The output after running the above "*naive*" code:

```console
-------------------------------------------------- 

Array / List: []

Maximum Value: None
Minimum Value: None

-------------------------------------------------- 

Array / List: [8, 3, 3, 1, 4]

Maximum Value: 8
Minimum Value: 1

-------------------------------------------------- 

Array / List: [3]

Maximum Value: 3
Minimum Value: 3

-------------------------------------------------- 

Array / List: [7, 2, 3, 9, 9]

Maximum Value: 9
Minimum Value: 2

-------------------------------------------------- 

Array / List: [0, 6, 1, 6, 1, 1, 3, 5, 0, 3]

Maximum Value: 6
Minimum Value: 0
```

---

# Divide and Conquer Sub-Optimal Approach

> [!INFO] Resource(s)
> 
> - Medium Article: https://medium.com/@t.sampathkumar/finding-maximum-and-minimum-using-divide-and-conquer-43bbae7636c3

As the name of the *technique* suggests; we are going to be dividing / splitting the problem into smaller problems until we cannot further divide anymore!

```python
def max_min_arr(arr: list[int], left: int, right: int):
    # check if the length of the array is '0'
    if len(arr) == 0:
        return (None, None)

    # check if we have only 1 element in array
    if left == right:
        return (arr[left], arr[left])

    # check if we have only 2 elements in array
    if (right - left) == 1:
        # check for maximum and minimum value by comparing those 2 elements
        if arr[left] > arr[right]:
            return (arr[left], arr[right])

        else:
            return (arr[right], arr[left])

    # if the array contains `n` terms
    else:
        # lower split of array
        max1, min1 = max_min_arr(arr, left, (left + right) // 2)

        # upper split of array
        max2, min2 = max_min_arr(arr, (((left + right) // 2) + 1), right)

    # finally return the correct maximum and minimum values
    return (max(max1, max2), min(min1, min2))
```

> [!NOTE] Time Complexity = O(n)
> 
> - The **overall** *running* time complexity for this function is going to be O(n)
> - Best Case: O(n)
> - Worst Case: O(n)
> 
> > [!INFO] Recurrence Equation: T(n) = 2T(n/2) + 2
> > 
> > - An array with `n` terms is broken down into 2 parts
> > 	- Therefore we are going to have an 2 arrays each with `n / 2` elements
> > 	- This process keeps on repeating as until we only have 2 elements in the *last function call*
> > - Therefore, we are going to have: T(n/2)
> > - But then as we have 2 arrays we are going to do everything twice!
> > - Hence, the updated running time complexity is going to be: 2T(n/2)
> > - Furthermore, at the `return` statement we are comparing to find the actual maximum and minimum
> > - Thus the **running time complexity** ( *in terms of `T(n)`* ) becomes: 2T(n/2) + 2

> [!NOTE] Number of Comparisons = (3n/2) - 2
> 
> Simply solved the above **recurrence relation**; T(n) = 2T(n/2) + 2 to get the above number of *equation*!

> [!SUCCESS]
> Let's say that we have an array with 100 terms ( *meaning that `n = 100`* ). Calculating the number of comparison with the different approaches:
> 
> - Naive Approach: 2(100) - 2 = 198
> - Divide and Conquer: (3(100) / 2) - 2 = 148
> 
> > That's a massive reduction of the number of comparisons made!
> 
> This shows that even though, *in general*, recursion is "*heavier*" in terms of hardware resources; in this case its going to be much **faster** that the iterative approach simply because we have **less** *comparing* to do!
> 
> > The benefits gets bigger when the number of terms increases in the array!

## Divide and Conquer Approach: Full Example Code

This is a full example code using the 'Divide and Conquer Approach' to find the maximum and minimum element in an array!

```python
from random import randint


# function to find the maximum and minimum value of array
def max_min_arr(arr: list[int], left: int, right: int):
    # check if the length of the array is '0'
    if len(arr) == 0:
        return (None, None)

    # check if we have only 1 element in array
    if left == right:
        return (arr[left], arr[left])

    # check if we have only 2 elements in array
    if (right - left) == 1:
        # check for maximum and minimum value by comparing those 2 elements
        if arr[left] > arr[right]:
            return (arr[left], arr[right])

        else:
            return (arr[right], arr[left])

    # if the array contains `n` terms
    else:
        # lower split of array
        max1, min1 = max_min_arr(arr, left, (left + right) // 2)

        # upper split of array
        max2, min2 = max_min_arr(arr, (((left + right) // 2) + 1), right)

    # finally return the correct maximum and minimum values
    return (max(max1, max2), min(min1, min2))


# our main function
def main():
    # find the minimum and maximum number for different numbers in array / list
    for i in range(5):
        # create list of integers of random numbers
        int_nums: list[int] = [randint(0, 9) for i in range(randint(0, 10))]

        print("\n" + "-" * 50, "\n")

        # display the rray to the user
        print(f"Array / List: {int_nums}")

        # call the function to find the maximum and minimum value
        maximum_arr_value, minimum_arr_value = max_min_arr(
            int_nums, 0, len(int_nums) - 1
        )

        # display the minimum and maximum value from the array / list
        print(f"\nMaximum Value: {maximum_arr_value}")
        print(f"Minimum Value: {minimum_arr_value}")


if __name__ == "__main__":
    main()
```

- This is the output that we got when we ran the above code:

```console
--------------------------------------------------

Array / List: [2, 1, 4, 3, 8]

Maximum Value: 8
Minimum Value: 1

--------------------------------------------------

Array / List: [6]

Maximum Value: 6
Minimum Value: 6

--------------------------------------------------

Array / List: []

Maximum Value: None
Minimum Value: None

--------------------------------------------------

Array / List: [3, 8]

Maximum Value: 8
Minimum Value: 3

--------------------------------------------------

Array / List: [1]

Maximum Value: 1
Minimum Value: 1
```

---

# Pairwise Optimal Approach

> [!INFO] Resource(s)
> 
> - Enjoy Algorithms: https://www.enjoyalgorithms.com/blog/find-the-minimum-and-maximum-value-in-an-array
> - Chier Hu YouTube Video: https://www.youtube.com/watch?v=rsJTZgRqqZQ

```python
# function to find the maximum and minimum value of array
def max_min_arr(arr: list[int]):
    # get the length of the array
    arr_length = len(arr)

    # check for length
    if arr_length == 0:
        return None, None

    elif arr_length == 1:
        return arr[0], arr[0]

    # initialise the overall minimum and maximum
    if arr[0] > arr[1]:
        current_max = arr[0]
        current_min = arr[1]

    else:
        current_max = arr[1]
        current_min = arr[0]

    # get the `start` and `end` index
    # TIP: no need to start from first 2 elements
    start = 2

    # WARNING: for the `end` index, we HAVE to check if array length is odd / even
    if arr_length % 2 != 0:
        current_max = max(current_max, arr[-1])
        current_min = min(current_min, arr[-1])

        # therefore remove last element from pair comparison as we already compared!
        end = arr_length - 1

    else:
        end = arr_length

    # perform pairwise comparison operation
    for i in range(start, end, 2):
        if arr[i] > arr[i + 1]:
            local_max, local_min = arr[i], arr[i + 1]

        else:
            local_max, local_min = arr[i + 1], arr[i]

        # compare with actual current maximum and minimum from local pairs
        if local_max > current_max:
            current_max = local_max

        if local_min < current_min:
            current_min = local_min

    return current_max, current_min
```

> [!INFO] Same Time Complexity and Number Of Comparison
> The *pairwise* approach has the **same** *time complexity* and *number of comparison* as our **divide and conquer** approach!
> 
> Therefore, please refer to the [[#Divide and Conquer Sub-Optimal Approach | above]] explanation for the time complexity and how to get the number of comparison!
> 
> > [!NOTE] Again...
> > The only possible different that *I* can see its that the way that *pairwise* approach is much **better** than our *recursive* method is because of the **lack** of *recursion*.

## Pairwise Approach: Full Example Code

```python
from random import randint


# function to find the maximum and minimum value of array
def max_min_arr(arr: list[int]):
    # get the length of the array
    arr_length = len(arr)

    # check for length
    if arr_length == 0:
        return None, None

    elif arr_length == 1:
        return arr[0], arr[0]

    # initialise the overall minimum and maximum
    if arr[0] > arr[1]:
        current_max = arr[0]
        current_min = arr[1]

    else:
        current_max = arr[1]
        current_min = arr[0]

    # get the `start` and `end` index
    # TIP: no need to start from first 2 elements
    start = 2

    # WARNING: for the `end` index, we HAVE to check if array length is odd / even
    if arr_length % 2 != 0:
        current_max = max(current_max, arr[-1])
        current_min = min(current_min, arr[-1])

        # therefore remove last element from pair comparison as we already compared!
        end = arr_length - 1

    else:
        end = arr_length

    # perform pairwise comparison operation
    for i in range(start, end, 2):
        if arr[i] > arr[i + 1]:
            local_max, local_min = arr[i], arr[i + 1]

        else:
            local_max, local_min = arr[i + 1], arr[i]

        # compare with actual current maximum and minimum from local pairs
        if local_max > current_max:
            current_max = local_max

        if local_min < current_min:
            current_min = local_min

    return current_max, current_min


# our main function
def main():
    # find the minimum and maximum number for different numbers in array / list
    for i in range(5):
        # create list of integers of random numbers
        int_nums: list[int] = [randint(0, 9) for i in range(randint(0, 10))]

        print("\n" + "-" * 50, "\n")

        # display the rray to the user
        print(f"Array / List: {int_nums}")

        # call the function to find the maximum and minimum value
        maximum_arr_value, minimum_arr_value = max_min_arr(int_nums)

        # display the minimum and maximum value from the array / list
        print(f"\nMaximum Value: {maximum_arr_value}")
        print(f"Minimum Value: {minimum_arr_value}")


if __name__ == "__main__":
    main()
```

- This is the output for the above program:

```console
--------------------------------------------------

Array / List: [6]

Maximum Value: 6
Minimum Value: 6

--------------------------------------------------

Array / List: [8, 8, 2]

Maximum Value: 8
Minimum Value: 2

--------------------------------------------------

Array / List: [7, 7, 0, 2, 0]

Maximum Value: 7
Minimum Value: 0

--------------------------------------------------

Array / List: []

Maximum Value: None
Minimum Value: None

--------------------------------------------------

Array / List: [6, 4, 7, 4, 8, 4, 2, 5]

Maximum Value: 8
Minimum Value: 2
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!