---
id: Python - Merge Sort
aliases: Implementation of Merge Sort on Dynamic Arrays in Python
tags:
  - algos
  - arrays
  - dsa
  - lists
  - python
  - sorting
author: S.Sunhaloo
date: 2025-10-09
status: Completed
---

## List of Contents

- [[#Different Ways Of Doing Merge Sort]]
	- [[#Sorting Lists In-Place]]
		- [[#Neural Nine / NeetCode Version]]
		- [[#Single Function Merge Sort]]
	- [[#Return New Sorted List]]

---

> [!INFO] Resource(s)
> - Visualisation: https://visualgo.net/en/sorting?slide=1
> - Big-Oh Cheat Sheet: https://www.bigocheatsheet.com/
> - Neural Nine: https://www.youtube.com/watch?v=LGiEYu6SkgE
> - NeetCode: https://www.youtube.com/watch?v=MsYZSinhuFo
> - Michael Sambol: https://www.youtube.com/watch?v=4VqmGXwpLqc

> [!WARNING]
> Please do refer to the resources above to see how the sorting algorithm actually works ( *in terms of movement of elements* ).

# Different Ways Of Doing Merge Sort

The **Merge Sort** algorithm will always have a *Time Complexity* of $O(n \cdot log(n))$. But there are several ways of doing it. Some just returns a **new** *sorted* array / list or some simply sorts the array / list **in-place**.

> [!TIP]- Time Complexity = O(n log n)
> The **worst**, **average** and also **best** *Time Complexity* is actually $O(n \cdot log(n))$
>
> > *Yes... They are all the same*!!!
>

> [!NOTE]
> As I don't know what the fuck I am doing anymore... I will be just learning them as I go!
>
> I am going to include all the resources that I *watched* and *read* and simply learn and understand them.

## Sorting Lists In-Place

### Neural Nine / NeetCode Version

In this version they have 2 **different** functions; one that does the *divide* / *splitting* part and another one that "*conquer*" / *combines* the individual ( *lists* ) data!

- The `merge_sort` function is the *main* function responsible for **splitting** and **calling** the `merge` function
- The `merge` function is the function that is going to **sort** and *replace* our data in an *ordered* manner

```python
# conquer "merge" function to combine individual list / values in sorted manner
def merge(list_nums, left_index, right_index, mid_index):
    # create a copy of the left and right part of the list `list_nums`
    left_part_cpy = list_nums[left_index : mid_index + 1]
    right_part_cpy = list_nums[mid_index + 1 : right_index + 1]

    # create pointers that will iterate through the left and right parts
    left_ptr = right_ptr = 0

    # create pointer that will iterate through the original `list_nums`
    main_ptr = left_index

    # check for the ( part of ) list which has the minimum length
    while left_ptr < len(left_part_cpy) and right_ptr < len(right_part_cpy):
        # check if value of index at left part if smaller or equals than right part
        if left_part_cpy[left_ptr] <= right_part_cpy[right_ptr]:
            # if smaller value found ==> replace original list's value
            list_nums[main_ptr] = left_part_cpy[left_ptr]

            # increment the pointer found at left part of list
            left_ptr += 1

        # else if the value of the index at right part is smaller
        else:
            list_nums[main_ptr] = right_part_cpy[right_ptr]

            # increment the pointer found at right part of list
            right_ptr += 1

        # increment the main list pointer to move it to next value
        main_ptr += 1

    # if the left part has more data left
    while left_ptr < len(left_part_cpy):
        # add the remaining data ( which have already been sorted ) to the list
        list_nums[main_ptr] = left_part_cpy[left_ptr]

        # increment the main pointer and also the left pointer
        left_ptr += 1
        main_ptr += 1

    # if the right part has more data left
    while right_ptr < len(right_part_cpy):
        # add the remaining data ( which have already been sorted ) to the list
        list_nums[main_ptr] = right_part_cpy[right_ptr]

        # increment the main pointer and also the right pointer
        right_ptr += 1
        main_ptr += 1


# divide "merge_sort" function that is going to divide the list
# NOTE: the `merge_sort` function is going to call the `merge` helper function
# therefore, we can definitely say that the `merge_sort` function also sorts it
def merge_sort(list_nums, left, right):
    # check if the we have only 1 data that is returned ( upon recursion )
    if left > = right:
        # therefore our base case has been reached
        return list_nums

    # if not calculate our middle index of "main" array
    mid = (left + right) // 2

    # call the function again to split the left part of the array again
    merge_sort(list_nums, left, mid)

    # call the function again to split the right part of the array again
    merge_sort(list_nums, mid + 1, right)

    # finally call the helper function to merge individuals lists / values
    merge(list_nums, left, right, mid)
```

### Single Function Merge Sort

> [!INFO]
> This code was written / found in NeetCode's video whereby the *commenter* '[alexsimons3804](https://www.youtube.com/@alexsimons3804)' wrote the following code shown below!
>
> In this code, he / she combined **both** the `merge` and `merge_sort` function to then only have the `merge_sort` function **without**, *again*, the `merge` function.

> [!TIP] Actually!!!
> > *Its The Fucking Same*!!!
>
> Instead of creating a *helper* `merge` function. He / She simply coded the code found inside the `merge` function **without** the need to **call** the *helper* function!
>
> But instead of having a **base case** of `left > = right`... We instead have `len(list_nums) > 1` ( *the condition to basically keep splitting...* )
>

```python
# merge sort function to recursively sort lists using divide and conquer method
def merge_sort(list_nums):
    # check if the list can be splitted further
    if len(list_nums) > 1:
        # INFO: in this case, instead of using "user" create pointers
        # the coder chooses to simply use the "length" itself to find the indices

        # therefore calculate the middle of the list
        mid = len(list_nums) // 2

        # create a copy of the left and right part of the list `list_nums`
        # NOTE: `mid` is non-inclusive in this case
        left_part = list_nums[:mid]
        # NOTE: `mid` is inclusive in this case
        right_part = list_nums[mid:]

        # call the function again on the left part of the array
        merge_sort(left_part)

        # call the function again on the right part of the array
        merge_sort(right_part)

        # INFO: therefore code the `merge` function directly here

        # create pointers that will iterate through main and copies of list
        main_ptr = left_ptr = right_ptr = 0

        # check for the ( part of ) list which has the minimum length
        while left_ptr < len(left_part) and right_ptr < len(right_part):
            # check if value of index at left part if smaller than right part
            if left_part[left_ptr] <= right_part[right_ptr]:
                # if smaller value found ==> replace original list's value
                list_nums[main_ptr] = left_part[left_ptr]

                # increment the pointer found at left part of list
                left_ptr += 1

            # else if the value of the index at right part is smaller
            else:
                list_nums[main_ptr] = right_part[right_ptr]

                # increment the pointer found at right part of list
                right_ptr += 1

            # increment the main list pointer to move it to next value
            main_ptr += 1

        # if the left part has more data left
        while left_ptr < len(left_part):
            # add the remaining data ( which have already been sorted ) to the list
            list_nums[main_ptr] = left_part[left_ptr]

            # increment the main pointer and also the left pointer
            left_ptr += 1
            main_ptr += 1

        # if the right part has more data left
        while right_ptr < len(right_part):
            # add the remaining data ( which have already been sorted ) to the list
            list_nums[main_ptr] = right_part[right_ptr]

            # increment the main pointer and also the right pointer
            right_ptr += 1
            main_ptr += 1
```

## Return New Sorted List

> [!INFO] I **Don't** Know Where I Found This Code!!!
> Yes, I think I found it someone's YouTube comment section and its working nicely for all I know and its actually really easy to understand.
>
> > Its even more simply than than the above code!
>

```python
# conquer "merge" function to combine individual list / values in sorted manner
def merge(left_part, right_part):
    # create a new list that will be returned
    result_list = []

    # create pointers that will iterate through the left and right parts
    left_ptr = right_ptr = 0

    # check for the ( part of ) list which has the minimum length
    while left_ptr < len(left_part) and right_ptr < len(right_part):
        # check if value of index at left part if smaller than right part
        if left_part[left_ptr] <= right_part[right_ptr]:
            # if smaller value found ==> add / 'append' the value to the new list
            result_list.append(left_part[left_ptr])

            # increment the pointer found at left part of list
            left_ptr += 1

        # else if smaller value found on right part
        else:
            # ==> add / 'append' the value to the new list
            result_list.append(right_part[right_ptr])

            # increment the pointer found at right part of list
            right_ptr += 1

    # if the left part has more data left
    result_list.extend(left_part[left_ptr:])

    # if the right part has more data right
    result_list.extend(right_part[right_ptr:])

    # finally return the new sorted list
    return result_list


# divide "merge_sort" function that is going to divide the list
# NOTE: the `merge_sort` function is going to call the `merge` helper function
# therefore, we can definitely say that the `merge_sort` function also sorts it
def merge_sort(list_nums):
    # check if we only have less than 2 data ==> one data left ( upon recursion )
    if len(list_nums) < 2:
        # therefore our base case has been reached
        return list_nums

    # if not calculate the middle index of the list
    mid = len(list_nums) // 2

    # call the function again to split the left part of the array again
    # NOTE: `mid` is non-inclusive in this case
    left_part = merge_sort(list_nums[:mid])

    # call the function again to split the right part of the array again
    # NOTE: `mid` is inclusive in this case
    right_part = merge_sort(list_nums[mid:])

    # finally call the helper function to merge individuals lists / values
    return merge(left_part, right_part)
```

> [!TIP] **Don't** Use The Above For Pure Performance!
> As you can see we are **inserting** data into a new list for the "*conquer*" part of 'Merge Sort' function.
>
>

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!