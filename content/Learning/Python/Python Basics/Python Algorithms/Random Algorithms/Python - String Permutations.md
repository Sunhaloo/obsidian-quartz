---
id: Python - String Permutations
aliases: Using brute-force and backtracking apporaches to find string permutations
tags:
  - algos
  - backtracking
  - brute-force
  - dsa
  - python
author: S.Sunhaloo
date: 2026-03-03
status: Completed
---

## List of Contents

- [[#Brute Force]]
- [[#Backtracking]]

---

> [!WARNING] 
> Please go give little look at the note for '[[Python - Subset Generation#Before We Start | Python - Subset Generation]]' as I wrote that note first.
> 
> There, I gave a little "*note*" about 'Brute Force' and 'Backtracking'

# Brute Force

> [!INFO] Resource(s)
> 
> - Medium Article: https://medium.com/swlh/step-by-step-guide-to-solving-string-permutation-using-recursion-in-javascript-a11d098d5b83

```python
# function to generate all the permutations of a strings through "brute force" recursion
def generate_permutations(string: str) -> list[str]:
    # check for the base cases ==> length of the strings
    if len(string) == 0:
        return [""]

    elif len(string) == 1:
        return [string]

    # initialise result list
    result: list[str] = []

    # iterate through the length of the string
    for i in range(len(string)):
        # get the current character at `i`
        current_char = string[i]

        # get all the remaining characters ==> everything except `string[i]`
        remaining_characters = string[:i] + string[i + 1 :]

        # run the function again on the remaining characters of the string
        remaining_char_permutations = generate_permutations(remaining_characters)

        # add the current character `current_char` to the front of every permutations
        for j in remaining_char_permutations:
            # add the newly created string to the `result` list
            result.append(current_char + j)

    return result
```

> [!NOTE] Time Complexity = O(n * n!) [ $O(n \cdot n!)$ ]
> 
> - The **overall** *running* time complexity for this function is going to be O(n * n!) [ $O(n \cdot n!)$ ]
> - Best Case: O(1)
> - Worst Case: O(n * n!) / $O(n \cdot n!)$
> 
> > [!INFO] Recurrence Equation: nT(n - 1) + O(n)
> >
> > - In this case, we know that the **inner** `for` loop is going to run `n` times; therefore: O(n)
> > - Additionally, we know that the **string slicing**
> > 	- Hence, we are going to have O(n^2) [ $O(n^{2})$ ]
> > - Now, we know that we are calling the function again but with *one* **less** characters
> > 	- This means that we are going to get: T(n - 1)
> > - Since the outer loop runs `n` times and each iteration makes a recursive call on a *sub-problem* of size `n - 1`, we get: n x T(n - 1)
> > - Thus the **running time complexity** ( *in terms of `T(n)`* ) becomes: nT(n - 1) + O(n^2)

## What does the code actually do?

> I would actually do *this* if I were to do this with *pen* and *paper*!

Let's go ahead and take an example with the string of `"ABC"`.

- Take the `A` out and permute with the other remaining characters
	- This means we get `A + BC` and `A + CB`
- Then, take the `B` out and permute with the other remaining characters
	- This means we get `B + AC` and `B + CA`
- Finally, take the `C` out and permute with the other remaining characters
	- This means we get `C + AB` and `C + BA`

Hence, at the end, we should have this:

```console
ABC ACB BAC BCA CAB CBA
```

> [!SUCCESS]
> As you can see, it a really simple, *actual* brute force approach!

---

> [!NOTE]
> There is one thing that I want to say about the above code!
> 
> Running the code and passing the string `"CAR"` as the argument; we see that our output look like this:
> 
> ```console
> ['CAR', 'CRA', 'ACR', 'ARC', 'RCA', 'RAC']
> ```
> 
> As you can clearly see, the function returns a **list of strings** ( *with the different possibilities* ).
> 
> Speaking with [Claude](https://claude.ai); it tells me that this is totally fine and its how its should be. Therefore, we could use something like the `.join()` *method* to be able to "*stringify*" it!
> 
> But I asked [Gemini](https://gemini.google.com) to adapt the above code so that we instead get an output like this:
> 
> ```console
> CAR CRA ACR ARC RCA RAC
> ```
> 
> Nevertheless, Claude told, me that the "*correct*" ( *unofficial official* ) way to write this type of basic code is to actually `return` a **list of strings**
> 
> > Therefore I am giving up on the idea of adapting the program to return a `str`ing ( *as Gemini's code was shit...* )!

---

# Backtracking

> [!INFO] Resource(s)
> 
> - YouTube Video: https://www.youtube.com/watch?v=s7AvT7cGdSo

> Well this is basically a 'copy-paste' of [NeetCode](https://www.youtube.com/@NeetCode)'s code!

```python
# function to generate all the permutations of a strings using backtracking and recursion
def generate_permutations_backtracking(data: list) -> list:
    # initialise result list
    result = []

    # check for the base cases ==> length of the strings
    if len(data) == 1:
        # NOTE: in Python `data[:]` is the same as `data.copy()`
        # `list[:]` is slightly ( in terms of nanoseconds ) faster than `list.copy()`
        # again, as they shared same memory... need to work with copy
        return [data[:]]

    # iterate through the length of the array
    for i in range(len(data)):
        # remove the first element from the array
        n = data.pop(0)

        # run the function again on the remaining data of the list
        perms = generate_permutations_backtracking(data)

        # add the element remove at the top, back to each sub-permutation
        for perm in perms:
            # add the remove element to the "individual" list
            perm.append(n)

        # add remaining "permutated" elements to our `result` list
        result.extend(perms)

        # backtrack; restore the list for the next iteration and move up the tree
        data.append(n)

    return result
```

> [!NOTE] Time Complexity = O(n * n!) [ $O(n \cdot n!)$ ]
> 
> - The **overall** *running* time complexity for this function is going to be O(n * n!) [ $O(n \cdot n!)$ ]
> - Best Case: O(1)
> - Worst Case: O(n * n!) / $O(n \cdot n!)$
> 
> > [!INFO] Recurrence Equation: nT(n - 1) + O(n)
> >
> > - The **outer** `for` loop runs `n` times, and each iteration makes a recursive call on a *sub-problem* of size `n - 1`, giving us: n x T(n - 1)
> > - Unlike the brute force version, there is **no** *string slicing* here
> > 	- Nevertheless, `.pop()` function oes *costs* O(n) as Python has to **shift** every element left after removal
> > 	- The **inner** `for` loop also runs O(n) times
> > 	- Combined, the work at each level is O(n) not O(n^2)
> > - Thus the **running time complexity** ( *in terms of `T(n)`* ) becomes: nT(n - 1) + O(n)

> [!WARNING] The Output!
> 
> If we go ahead and run the above program with the input *argument* of `["A", "B", "C"]`. We should see that we get and **output** that looks like this:
> 
> ```console
> [['C', 'B', 'A'], ['B', 'C', 'A'], ['A', 'C', 'B'], ['C', 'A', 'B'], ['B', 'A', 'C'], ['A', 'B', 'C']]
> ```
> 
> > List of list of *element' datatype*!
> 
> Therefore, if we want to have a cleaner output for some `str`ing datatypes, then we could use this *wrapper* function that Claude gave me.
> 
> ```python
> # wrapper function to return a list with actual elements itself
> def permutations_as_strings(data: list) -> list:
>     # call the function on the input "data" / lists
>     perms = generate_permutations_backtracking(data)
> 
>     # simply use the `.join` method inside a string to build the "return" list
>     return ["".join(perm) for perm in perms]
> ```
> 
> > [!SUCCESS]
> > 
> > Therefore using the above wrapper function of **input** like: `["A", "B", "C"]`
> > 
> > - We are going to get these as output:
> > 
> > ```console
> > ["A", "B", "C"]`: ['CBA', 'BCA', 'ACB', 'CAB', 'BAC', 'ABC']
> > ```
> 
> > Nevertheless, the above function only works for **list of strings**!

## The Principle

Here is a little diagram for you to understand how it actually works!

![[String Permutations - Backtracking ( NeetCode ).png | 600]]

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!