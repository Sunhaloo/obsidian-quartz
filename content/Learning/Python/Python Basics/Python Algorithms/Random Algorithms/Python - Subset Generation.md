---
id: Python - Subset Generation
aliases: Using brute-force and backtracking apporaches to generate subsets
tags:
  - algos
  - backtracking
  - brute-force
  - dsa
  - python
author: S.Sunhaloo
date: 2026-03-02
status: Completed
---

## List of Contents

- [[#Brute Force]]
	- [[#Bitmasking Approach]]
- [[#Backtracking]]
	- [[#Depth First Search Recursive Approach]]
		- [[#Lecturer's Version Of Subset Generation Using Backtracking]]
		- [[#NeetCode's Implementation Of Subset Generation ( Adaptation Of LeetCode Solution )]]

---

## Before We Start

> [!WARNING] Brute Force **and** Backtracking
> 
> > They are [same, same but different](https://www.youtube.com/watch?v=7tTfL-DtpXk)!
> 
> From our lecture notes / slides, we are first taught about 'Brute Force' which, in simple terms, is going to check all the possibilities and normally results in a **running time complexity** of O(n).
> 
> After that, we are also taught about 'Backtracking'... But remember something! *Backtracking* is just a "*better*" version of Brute Force as we have **pruning**; therefore it will stop the recursion process instead *when found* instead of checking all and every possible *combinations*!
> 
> > [!INFO] What am I trying to say?
> > 
> > This note is divided into 2 sections whereby we have the 'Brute Force' approach and also the 'Backtracking' approach.
> > 
> > But then again, we show that the 'Brute Force' approach "*is*" the 'Backtracking' and vice-versa!
> > 
> 
> > Therefore take these with a *grain of salt*... Nevertheless, the all the code below works and was done with the help of all looking at articles, videos and more before asking [Claude](https://claude.ai) and mainly [Gemini](https://gemini.google.com) for more help and clarification!

> [!NOTE]
> I am **not** going to explain everything... This is note is mainly for the actual *code*!
> 
> Please do refer to the resource(s) resources in this note; and for *me*, do also refer to the lecture slides.

# Brute Force

> [!INFO] Resource(s)
> 
> - Medium Article: https://jyotiguptaofficial.medium.com/js-recursion-part-2-generate-all-subsets-of-a-set-in-javascript-from-brute-force-to-optimal-3263a211c2f7
> - YouTube Video: https://www.youtube.com/watch?v=GLm0aLsoRtY

## Bitmasking Approach

```python
# function to use bitmasking / bit manipulation to generate subsets
def subset_generation(nums: list[int]) -> list[list[int]]:
    # find the length of the array
    arr_length = len(nums)

    # check for the length
    if arr_length == 0:
        return []

    elif arr_length == 1:
        return [[], [nums[0]]]

    # our overall result set containing each subsets
    result: list[list[int]] = []

    # iterate through the (2^n - 1) combinations ( refer to notes )
    for i in range(1 << arr_length):
        # create the individual subsets
        subset: list[int] = []

        # iterate through the length of the array and apply bit masking
        for j in range(arr_length):
            if i & (1 << j):
                subset.append(nums[j])

        # add that subset to the overall result
        result.append(subset)

    return result
```

> [!NOTE] Time Complexity = O(n * 2^n) [ $O(n \cdot 2^{n})$ ]
> 
> - The **overall** *running* time complexity for this function is going to be O(n * 2^n) [ $O(n \cdot 2^{n})$ ]
> - Best Case: O(1)
> - Worst Case: O(n * 2^n) / $O(n \cdot 2^{n})$
> 	- We have the inner `for` loop which iterate through `n` times
> 	- We have the outer `for` loop which iterate through `2 ^ n` times

### Tracking The Bitmasking Program

I am going going to trace the program above because for this I think its necessary!

> [!TIP]
> 
> > A little guide to **Bit Shifting**!
> 
> - Shifting Left: `n << x`
> 	- This simply means in *multiplying* in terms of **powers of 2**
> 	- In short, we are doing: `n * 2^x` [ $n \times 2^{x}$ ]
> - Shifting Right: `n > > x`
> 	- This simply means that *dividing* in terms of **powers of 2**
> 	- In short, we are doing: `n // 2^x` [ $\frac{n}{2^{x}}$ ]
> 
> - Table Example Of Shifting Bits Left ( *i.e `<<`* ):
> 	- `n`: 1
> 
> | Expression | Movement | Final Binary | Decimal Value |
> | ---------- | -------- | ------------ | ------------- |
> | 1 << 0 | `0001` -> `0001` | `0001` | 1 |
> | 1 << 1 | `0001` -> `0010` | `0010` | 2 |
> | 1 << 2 | `0001` -> `0100` | `0100` | 4 |
> | 1 << 3 | `0001` -> `1000` | `1000` | 8 |
> 
> - Table Example Of Shifting Bits Left ( *i.e `<<`* ):
> 	- `n`: 8
>
> | Expression | Movement | Final Binary | Decimal Value |
> | ---------- | -------- | ------------ | ------------- |
> | 8 << 0 | `1000` -> `1000` | `1000` | 8 |
> | 8 << 1 | `1000` -> `0100` | `0100` | 4 |
> | 8 << 2 | `1000` -> `0010` | `0010` | 2 |
> | 8 << 3 | `1000` -> `0001` | `0001` | 1 |
> | 8 << 4 | `1000` -> `0000` | `0000` | 0 |

- The `console` code block below will show the "*tracing*" of the above bitmasking program:

```console
[1, 2, 3]

# length = 3 ==> n = 3
# total number of combinations ==> 2^3 = 8

# the bitmasking formula

# first iteration
i = 0
j = 0

0 & ( 1 << 0 )
0000 & 0001 = 0000

==> first iteration = []

# second iteration
i = 0
j = 1

0 & ( 1 << 1 )
0000 & 0010 = 0000

==> second iteration = []
```

> Basically this *pattern* keeps repeating and therefore, we get each of the subsets!

# Backtracking

> [!INFO] Resource(s)
> 
> - LeetCode Doocs: https://leetcode.doocs.org/en/lc/78/
> 	- The code here puts the "*include*" branch **first** *they* put the "*exclude*" branch **first**
> - YouTube Video: https://www.youtube.com/watch?v=REOH22Xwdkk

## Depth First Search Recursive Approach

### Lecturer's Version Of Subset Generation Using Backtracking

```python
# ( lecturer ) function to use recursion and backtracking to generate subsets
def subset_generation_recursive(
    i: int, nums: list[int], result: list[list[int]], subset: list[int]
):
    # check for base case ==> no more elements
    if i == len(nums):
        # NOTE: need to do `list(subset)` as its being manipulated in memory else we crash
        result.append(list(subset))

        # move back up the tree
        return

    # include part of the branch
    subset.append(nums[i])

    # move down into the tree
    subset_generation_recursive(i + 1, nums, result, subset)

    # exclude part of the branch
    subset.pop()

    # move down into the tree ( again )
    subset_generation_recursive(i + 1, nums, result, subset)


# function "main" ( wrapper ) function to call the recursive function to return all subsets
def generate_all_subsets(nums: list[int]):
    subset = []
    result = []

    # call the recursive function and pass required arguments
    subset_generation_recursive(0, nums, result, subset)

    # return the list of subsets for that "set"
    return result
```


### NeetCode's Implementation Of Subset Generation ( Adaptation Of LeetCode Solution )

```python
# function to generate subsets in a more elegant fashion ( NeetCode version )
def subset_generation_backtracking(nums: list[int]) -> list[list[int]]:
    # initialise our lists
    result: list[list[int]] = []
    subset: list[int] = []

    # check for the length
    if len(nums) == 0:
        return []

    elif len(nums) == 1:
        return [[], [nums[0]]]

    # function to recursively include / exclude the numbers into each subset
    # INFO: this is basically the backtracking recursive algorithm
    def depth_first_search(i: int):
        if i == len(nums):
            # NOTE: in Python `subset[:]` is the same as `subset.copy()`
            # `list[:]` is slightly ( in terms of nanoseconds ) faster than `list.copy()`
            # again, as they shared same memory... need to work with copy
            result.append(subset[:])

            # move back up the tree
            return

        # include part of the branch
        subset.append(nums[i])

        # move down into the tree
        depth_first_search(i + 1)

        # exclude part of the branch
        subset.pop()

        # move down into the tree
        depth_first_search(i + 1)

    # call the recursive `depth_first_search` function to find each subset
    depth_first_search(0)

    # return the list of subsets for that "set"
    return result
```

As you can see, its basically doing the **same** thing as my lecturer's code.

> I found this one more *elegant* and more *pythonic*!

> [!NOTE] Time Complexity = O(n * 2^n) [ $O(n \cdot 2^{n})$ ]
> 
> - The **overall** *running* time complexity for this function is going to be O(n * 2^n) [ $O(n \cdot 2^{n})$ ]
> - Best Case: O(1)
> - Worst Case: O(n * 2^n) / $O(n \cdot 2^{n})$
> 
> > [!INFO] Recurrence Equation: 2T(n - 1) + O(1)
> > 
> > - In this case, at each step the algorithm makes 2 recursive calls
> > 	- *include* and *exclude* at each sub-problem of size `n - 1`
> > - Additionally, we are doing `append` and `pop`
> > 	- Therefore we are going to have: O(1)
> > - At the base case / leaf node ( *when we have to move back up* )
> > 	- The we `append` a **copy** of the `subset` list which has a running time of O(n)
> > 	- We are also performing this action for `2^n` times which means that we are going to have: O(n) * O(2^n)
> > - Thus the **running time complexity** ( *in terms of `T(n)`* ) becomes: 2T(n - 1) + O(1)

#### The Principle

Here is a little diagram for you to understand how it actually works!

![[Subset Generation - Backtracking ( NeetCode ).png | 1000]]

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!