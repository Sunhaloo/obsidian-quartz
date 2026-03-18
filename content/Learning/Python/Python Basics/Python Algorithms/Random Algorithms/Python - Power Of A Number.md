---
id: Python - Power Of A Number
aliases: Different ways to find the power of a number using different algorithms
tags:
  - algos
  - divide-and-conquer
  - dsa
  - python
author: S.Sunhaloo
date: 2026-02-23
status: Completed
---

## List of Contents

- [[#Naive Inefficient Approach]]
- [[#Divide and Conquer Approach]]
	- [[#Naive Divide and Conquer Approach]]
- [[#Divide and Conquer Sub-Optimal Approach]]
- [[#Bit-Wise Optimal Approach]]

---

> [!NOTE] Summary: What You Actually Need To Learn!
> 
> - [[#Naive Inefficient Approach]]
> - [[#Divide and Conquer Sub-Optimal Approach]]

> [!WARNING] You just need to know the algorithms!
> 
> Therefore, compared to what I did over at the note '[[Python - Maximum and Minimum Of Array]]' whereby I wrote the *function* and then also provided a full example, *running* code.
> 
> > I am **not** going to do that here!
> 
> > [!TIP] Nevertheless
> > 
> > The actual algorithm / *function* that I am going to provide has been tested and run multiple times!

> [!NOTE] Base and Exponent
> In this case, I am going to *[assume](https://www.youtube.com/watch?v=5ksV4nnXOsQ)* that **both** the *base* and *exponent* to be `int`eger numbers!
> 
> > Okay, okay, the **base** could be of *type* `float`...
> 
> Because I don't really care, if you are going to find the power of a number, use the power method that the ( *high level* ) programming language gives you!
> 
> > ( *In this case* ) The guy that coded the `pow` function for Python is probably smarter than everyone here!

# Naive Inefficient Approach

Well, this is pure logic and a sheer iteration process that anybody can do. There is nothing special about it!

> I think a 3 year old can code this!

```python
# function to find the power of a number
def power(base: float, exponent: int) -> float:
    # initialise variable to hold our end result
    result = 1

    # check if the exponent is positive or negative
    if exponent > = 0:
        # find the power of that `base` number using `exponent`
        for i in range(exponent):
            result *= base

        # return the result
        return result

    else:
        # find the power of that `base` number `-exponent`
        for i in range(-exponent):
            result *= base

        # return the correct answer
        return 1 / result
```

> I mean if a 3 year old child can play Chess; he / she should probably be able to code the above code!

> [!NOTE] Time Complexity = O()
> - The **overall** *running* time complexity for this function is going to be O(n)
> - Best Case: O(1)
> - Worst Case: O(n)

---

# Divide and Conquer Approach

## Naive Divide and Conquer Approach

### My Naive Divide and Conquer Approach

> [!BUG] **Don't Use This!!!**
> 
> This is **complete** *shit* and *unoptimise*!

> [!WARNING]
> This was not provided by anybody nor anyone! ( *pErFecT ENgLisH* ) One day, I just decided to simply code the following code that you are about to see below.
> 
> > I mean there should be other people that have done this **before** me!

> [!NOTE]
> The only reason that I am adding this here is; even though its a [[#Naive Inefficient Approach | naive]] approach to finding the power of a number.
> 
> It uses **recursion** which is *part* of the **divide and conquer** technique.

```python
# function to find the power of a number that uses recursion ( but still "naive" )
def power(base: float, exponent: int) -> float:
    # check for the base case ==> exponent = 0
    if exponent == 0:
        return 1

    # check if the exponent is positive or negative
    elif exponent > 0:
        # calculate and return the power of that `base` number
        return base * power(base, exponent - 1)

    else:
        # calculate and return the power of that `base` number after "reversing"
        return 1 / power(base, exponent * -1)
```

> Again, there is nothing special about this code, forget about it!

> [!NOTE] Time Complexity = O(n)
> - The **overall** *running* time complexity for this code is going to be O(n)
> - Best Case: O(1)
> - Worst Case: O(n)
> 
> > [!INFO] Time Complexity Equation: T(n) = T(n - 1) + c
> > 
> > - We know that we have our `exponent` which is going to be used to iterate `n` times
> > 	- Whereby the value of `n` is going to be **dependent** on the value of `exponent`
> > - Each time we find the *next* function call, we instead use `exponent - 1`
> > - Therefore, we are going to have: T(n - 1)
> > - Additionally, given that we are checking for the base-case above; we are going to add `c` for the *cost* of going into the `if` statement
> > - Hence, the final **running time complexity** equation is going to be: T(n - 1) + c

### Lecturer's Divide and Conquer Approach

> [!BUG] **Don't Use This!!!**
> 
> Similarly, this is also a **complete** piece of *shit* and *unoptimise*!

Now, this is a version of the 'power of a number' algorithm that the lecturer provided.

```python
# function provided by lecturer to find power of a number that uses recursion
def power(base: float, exponent: int) -> float:
    # check if the exponent is positive or negative
    if exponent < 0:
        # calculate and return the power of that `base` number after "reversing"
        return 1 / power(base, -exponent)

    # check for the base case
    if exponent == 0:
        return 1

    # if we are trying to find `base` to the power of '1'
    elif exponent == 1:
        return base

    # check if the exponent is even or odd
    if exponent % 2 == 0:
        return power(base, exponent // 2) * power(base, exponent // 2)

    else:
        return base * power(base, exponent // 2) * power(base, exponent // 2)
```

The above code basically divides the component by '2' at each recursion "*level*" and simply waits to return either the `base` or `1`

```python
    # check for the base case
    if exponent == 0:
        return 1

    # if we are trying to find `base` to the power of '1'
    elif exponent == 1:
        return base
```

Basically the lecturer's code is going to wait until the `exponent` satisfy the above conditions!

> Additionally I added a little 'positive-negative' exponent checker at the top!

> [!NOTE] Time Complexity: O(n)
> - The **overall** *running* time complexity for this code is going to be O(n)
> - Best Case: O(1)
> - Worst Case: O(n)
> 
> > [!INFO] Recurrence Equation: 2T(n/2) + c
> > 
> > - In this case, the `exponent` is be divided into 2 at each function *call*
> > - Therefore we are going to get: T(n/2)
> > - But remember even if `exponent` is *even* or *odd*
> > 	- For both of these conditions, we are calling the `power` function **twice**
> > - Hence, the updated running time is going to be: 2T(n/2)
> > - Furthermore, as we are also checking using the `if` statement
> > - Thus the **running time complexity** becomes: 2T(n/2) + c

#### Image Representation

##### Even Exponent

![[Power - Naive DC Even Exponent ( Lecturer ).png | 350]]

##### Odd Exponent

![[Power - Naive DC Odd Exponent ( Lecturer ).png | 450]]

## Divide and Conquer Sub-Optimal Approach

> [!SUCCESS] **Do You This One!**
> 
> This is a great *recursive* way to find the power of a number!

This is the approach that we should learn if we are going to try to use **divide and conquer** to find the *power of a number*.

```python
# function to find the power of a number that uses recursion ( optimised divide and conquer )
def power(base: float, exponent: int) -> float:
    # check if the base is '0' and the exponent is negative
    if base == 0 and exponent < 0:
        raise ValueError("\nUndefined: Cannot raise '0' to a negative exponent!\n")

    # check if the exponent is positive or negative
    if exponent < 0:
        # calculate and return the power of that `base` number after "reversing"
        return 1 / power(base, -exponent)

    # check for the base case
    if exponent == 0:
        return 1

    # if we are trying to find `base` to the power of '1'
    elif exponent == 1:
        return base

    # create temporary variable that calls the function again
    # INFO: as you can see, we don't
    # do something like `power(base, exponent) * power(base, exponent)`
    temp = power(base, exponent // 2)

    # check if the exponent is even or odd
    if exponent % 2 == 0:
        return temp * temp

    else:
        return base * temp * temp
```

> [!NOTE] Time Complexity: O(log n)
> - The **overall** *running* time complexity for this code is going to be O(log n)
> - Best Case: O(1)
> - Worst Case: O(log n)
> 
> > [!INFO] Recurrence Equation: T(n/2) + c
> > 
> > - In this case, the `exponent` is be divided into 2 at each function *call* and the result is placed in `temp`
> > - Therefore we are going to get: T(n/2)
> > - Hence, we check if `exponent` is *even* or *odd*
> > 	- We multiply `base` and `temp` accordingly and return the answer
> > - Given that we are also using `if` statements to check above
> > - Thus the **running time complexity** becomes: T(n/2) + c

#### Simple Image Representation

![[Power - DC ( Odd and Even ) Exponent.png | 175]]

---

# Exponentiation By Squaring Optimal Approach

> [!INFO] Resource(s)
> 
> - Wikipedia: https://en.wikipedia.org/wiki/Exponentiation_by_squaring

```python
# function to find the power of a number that uses an iterative and bitwise approach
def power(base: float, exponent: int) -> float:
    # check if the base is '0' and the exponent is negative
    if base == 0 and exponent < 0:
        raise ValueError("\nUndefined: Cannot raise '0' to a negative power!\n")

    # check if the exponent is positive or negative
    if exponent < 0:
        # prepare "values" for later
        base = 1 / base
        exponent = -exponent

    # check for the "base case" ( not really in this case )
    if exponent == 0:
        return 1

    # declare and initialise "answer" variable
    result = 1.0

    # start iterating until exponent becomes '0'
    while exponent > 0:
        # check for even or odd exponent using 'AND' gate
        # NOTE: if last bit is '1' ==> odd exponent found
        if exponent & 1:
            result *= base

        # square the base
        base *= base

        # the line below is simply doing: exponent // 2
        exponent > > = 1  # move to next bit

    return result
```

> [!NOTE] **Same** Time Complexity
> 
> Yes, the above "*better*" and "*more-optimised*" code has the **same** *running time complexity* of O(log n) as our '[[#Divide and Conquer Sub-Optimal Approach]]'.
> 
> - Best Case: O(1)
> - Worst Case: O(log n)
> 
> The reason that this code actually **faster** is because:
> 
> 1. It uses **iteration** instead of recursion
> 2. It does **not** get slower as the values of the `exponent` increases
> 
> This is because of the [Space Complexity](https://en.wikipedia.org/wiki/Space_complexity) whereby we only use and manipulate **three** variables in memory!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!