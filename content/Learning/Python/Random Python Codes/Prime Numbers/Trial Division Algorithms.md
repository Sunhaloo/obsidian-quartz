---
id: Trial Division Algorithms
aliases: Deterministic Primality Tests - Trial Divison Algorithms
tags:
  - python
  - C
author: S.Sunhaloo
date: 2025-05-22
status: Completed
---

## List of Contents

- [[#What is Trial Division?]]
	- [[#Trial Division Method]]
- [[#Wikipedia's Algorithms]]
	- [[#Pseudo-code]]
- [[#GeekForGeeks - Wikipedia Algorithms]]
	- [[#Not Stopping At Square Root of 'n']]
	- [[#Stopping At Square Root of 'n']]
- [[#The Main Algorithm]]
	- [[#Are You For or While?]]
- [[#Optimised Solution]]
	- [[#Optimised Implementation in Python]]
	- [[#Optimised Implementation in C]]

---

> [!WARNING]
> As you know, when a *CLI* program or application return `1`... This usually means that we have an <span style="color: red;"> error</span> !
>
> But you are going to see that I did the **inverse**... "*Why you ask*?" **Skill Issue**!
>
> Therefore, only and only for this one:
>
> - `0` means **composite**
> - `1` means **prime**

# What is Trial Division?

As per the [Wiki](https://en.wikipedia.org/wiki/Trial_division); **Trial Division** is the easiest way to understand *integer factorisation* algorithms.

Again what is '*integer factorisation*' you ask! Its the "*decomposition*" of larger number into their smaller numbers like we did over at [[Prime Number Analysis#Example of Prime and Composite Numbers | Prime Number Analysis]].

The method for **Trial Division** was first described by [Fibonacci](https://en.wikipedia.org/wiki/Fibonacci) ( *WTF, he is an actual fucking person?!?* ) in his book [Liber Abaci](https://en.wikipedia.org/wiki/Liber_Abaci)!

## Duh, Duh, Duh!!!

So the actual definition of *trial division* from the Wikipedia is **not** to check if a number $n$ is actually **prime** or **composite**. But instead to again, find the <strong> <span style="color: orange;"> Prime Factors</span> </strong> of $n$.

> [!INFO] Therefore...
> This first part is going to be just about the algorithm that Wikipedia is talking about and then we are going to move on to what *I* came here for!

## Trial Division Method

- Systematically tests whether $n$ is **divisible** by any *smaller* number
	- It is worthwhile to test *candidate factors* less than $n$ in order from 2 to $n -1$
- There is **no** point in testing for divisibility by *all the numbers* in the range of 2 to $n -1$ as number $n$ should already be determined at that point
	- Hence, just need to test **from 2 to $\sqrt{n}$** to reduce the number of *iterations*

> The last one is the most important part!

---

# Wikipedia's Algorithms

## Pseudo-code

Here is the pseudo-code that Wikipedia provides for the **Trial Division**.

```console
algorithm trial-division is
	input: Integer n to be factored
	output: List of F of primes factors of n

    P <- set of all primes <= int(sqrt(N))
    F <- empty list of factors

    for each prime p in P do
        while n mod p is 0
            add factor p to list F
            n <- n / p

    if F is empty ( Original n is prime? )
        add factor n to list F
```

> [!NOTE]
> Now, this is complete **bullshit**, why? Because:
>
> 1. Its not solving our problem ( *check if a number is prime* )
> 2. We are going to have to **generate** a list of prime!!!
>
> In this case, I am not going to be implementing this code... *Not right now*!

---

## GeeksForGeeks

> [!BUG] Don't Use GeekForGeeks!
> Yes **don't** use [GeeksForGeeks](), see these Reddit posts below as to why we, **especially _beginners_** should **not** be using it!
>
> - https://www.reddit.com/r/learnprogramming/comments/lot6ah/geeksforgeeks_not_a_good_place_to_get_started/
> - https://www.reddit.com/r/UoPeople/comments/16fgbhl/geeksforgeeksorg_article_reputable/

> Then why am I using it?

Well, because this is a pretty basic algorithm whereby the code is pretty much "*boilerplate*" code.

Therefore, we can initially take this code that I am about to explain just below $\downarrow$!

> [!TIP] Remember Definition of Prime!
> As we have been saying in [[Prime Number Analysis#What is a Prime Number? | Prime Number Analysis]], a **Prime Number** is a natural number that is *greater* than 1 and **not** a *product* of 2 smaller numbers.

# GeekForGeeks - Wikipedia Algorithms

This is a *mix* between the algorithm that Wikipedia provides and [GeeksForGeeks's](https://www.geeksforgeeks.org/trial-division-algorithm-for-prime-factorization/) code.

> [!INFO] Going Forwards!
> > Literally!
>
> So, instead of giving me and you the **optimised** / final version of *this* specific code... I rather make you and I *read* and *understand* each unoptimised code so that we know how to optimise it!
>
> > Additionally if will be *beautiful* to see it go from *slow* to *fast*!
>

## Not Stopping At Square Root of 'n'

### Implementation in Python

```python
# algorithm 1: trial division ( unoptimised )
# unoptimised ==> without stopping at sqrt(n)
def trial_division_1(n: int) -> int:
    # initialise and declare counter
    i = 2

    # iterate through the 'while' loop
    while n > i:
        # check if 'n' divided by 'i' has remainder(s) or not
        if (n % i) == 0:
            # number 'n' is composite
            return 0

        # increment the counter 'i' by 1
        i += 1

    # if number 'n' has no remainder(s) ==> 'n' is prime
    return 1
```

### Implementation in C

```C
// algorithm 1: trial division --> unoptimised ( without stopping at sqrt(n) )
int trial_division_1(int n) {
    // declare and initialise counter
    int i = 2;

    // start iterating with `while` loop
    while (n > i) {
        // check when does 'n' has no remainder when divided by 'i'
        if ((n % i) == 0) {
            // number 'n' is composite
            return 0;
        }
        
        // incremenent counter 'i' by 1
        i = i + 1;
    }

    // number 'n' is prime as `(n % i) != 0`
    return 1;
}
```

### Testing Validity of Functions

> [!NOTE]
> I am **not** going to write the timings, as it depends on the user's hardware and other factors.
>
> I know I just betrayed you and even myself... Buts as I am a lazy motherfucker. I won't waste my fucking time on copying and pasting the *elapsed times*!
>
> > Nevertheless, I am going to just say what version was the fastest at the *end* of the **file** / **note**.
>

Let's now check if the *output(s)* of the functions that we wrote above $\uparrow$.

| Test Number | Python Version | C Version |
| ----------- | -------------- | --------- |
| 0 | 1 | 1 |
| 1 | 1 | 1 |
| 2 | 1 | 1 |
| 3 | 1 | 1 |
| 4 | 0 | 0 |
| 5 | 1 | 1 |
| 7 | 1 | 1 |
| 10 | 0 | 0 |
| 12 | 0 | 0 |

> [!BUG] The Problem
> By definition, '0' and '1' **cannot** be *Prime Numbers*; and with this function, we do get them as **primes**.
>
> Simply, it because we currently **don't** have a *check* for number that are **less than 0 or equal to 1**. Hence, as we have `n > i` as condition for the `while` loop... It will never iterate through it and thus, number less than 1 or equal to becomes *primes*!
>
> We **cannot** use this function!
>
> > Its good as garbage!!!
>

## Stopping At Square Root of 'n'

### Implementation in Python

```python
# algorithm 2: trial division --> optimised ( stopping at sqrt(n) )
# optimised ==> stopping at sqrt(n)
def trial_division_2(n: int):
    # initialise and declare counter
    i = 2

    # iterate through the 'while' loop
    while sqrt(n) > = i:
        # check if 'n' divided by 'i' has a remainder(s) or not
        if (n % i) == 0:
            # number 'n' is composite
            return 0

        # increment the counter 'i' by 1
        i += 1

    # if number 'n' has no remainder(s) ==> 'n' is prime
    return 1
```

### Implementation in C

```C
// algorithm 2: trial division --> optimised ( stopping at sqrt(n) )
int trial_division_1(int n) {
    // declare and initialise counter
    int i = 2;

    // start iterating with `while` loop
    while (sqrt((double) n) > = i) {
        // check when does 'n' has no remainder when divided by 'i'
        if ((n % i) == 0) {
            // number 'n' is composite
            return 0;
        }
        
        // incremenent counter 'i' by 1
        i = i + 1;
    }

    // number 'n' is prime as `(n % i) != 0`
    return 1;
}
```

### Testing Validity of Functions

Let's also check *output(s)* the "*updated*" version of the functions with "**stopping at square root of $n$**"!

| Test Number | Python Version | C Version |
| ----------- | -------------- | --------- |
| 0 | 1 | 1 |
| 1 | 1 | 1 |
| 2 | 1 | 1 |
| 3 | 1 | 1 |
| 4 | 0 | 0 |
| 5 | 1 | 1 |
| 7 | 1 | 1 |
| 10 | 0 | 0 |
| 12 | 0 | 0 |


> [!BUG] Again, Similar Problems!!!
> The number '0' and '1' are still considered as *prime* numbers here which its obviously **fake**.
>
> Again, we have **no** checks for numbers that are less than '1' ( *even though negative prime numbers does exists* ).

> [!SUCCESS] Nevertheless, We Did Optimise Garbage!
> > Yet, its still garbage!
>
> So instead of iterating from '2' to $n$, we are iterating from '2' to $\sqrt{n}$.
>
> For example, if we take $n = 5$; below you are going to find the number of iterations that each of the function ( *one with square root and one without* ) took to find if that number $n$ is a **prime** or **composite**.
>
> - Function **Without** Square Root
>
> | Iteration Number | `n` | `i` |
> | ---------------- | --- | --- |
> | 0 | 5 | 2 |
> | 1 | 5 | 3 |
> | 2 | 5 | 4 |
> | 3 | 5 | 5 |
>
> - Function **With** Square Root
>
> | Iteration Number | `n` | `i` |
> | ---------------- | --- | --- |
> | 0 | 5 | 2 |
>
> On average, I saw that the *Elapsed Time* was slightly... Soooooo slightly faster **on average** for the one **with** the *square root* added to it.


---

# The Main Algorithm

> [!TIP]
> This is the one that we need to actually know!
>
> > [!NOTE]
> > When I say "*know*", I don't need "*learning by heart / regurgitate*"; because that fucked up or you have a *photographic memory*.
> >
> > What I really mean, is that we need to try to **understand** the code so that we do have the **knowledge** to be *implement* it again in the future!
> >
> > > [Because Knowledge $\neq$ Understanding](https://www.youtube.com/watch?v=MFzDaBzBlL0&t=404s)
> >
>

## Are You For or While?

Now, you see how we used `while` loops for the above $\uparrow$ algorithms?

> Now, let me hit you with some [knhaawwledge](https://www.youtube.com/watch?v=UgNH8q4D0Z4)!

As you know ( *which you should* ), Python is basically [[C Data View V2 | C]] and Python itself, under the hood.

Nevertheless, the version of *C* is, from what I am reading about, is a modified version of it.

Cutting to the chase; the `for` loop with the `range()` iterator, is going to be **faster** than a its `while` loop counter-part in <span style="color: orange;"> most</span> cases.

### The Reason!

As you know, in **Python** ( *and in most other languages* ); to be able to use a `while` loop without it getting **infinitely stuck**, we need to first *declare* and *increment* a **variable**.

> Like we have been doing for our counter / variable `i` above $\uparrow$

Additionally, the `while` loop, compared to the "*extremely*" faster **iterator** `range()`, which was implemented in *C*.
Needs to first be translated by the *Python's Interpreter* before being converted into *machine code*.

While ( *get it? "while"* ) using a `for` loop with the `range()` function; as its implemented in C, there is not need for *Python's Interpreter* to convert it and therefore is extremely faster.

Additionally, we also have to increment the variable / counter that will keep the `while` loop from going *rogue*. And as you know, there is no declaration in Python. Meaning that each time, that **variable** gets *re-initialised*!

### Concrete Example



## First Iteration of Trial Division Using For Loops

### Implementation in Python

```python
# algorithm 1: trial division --> unoptimised
def trial_division_1(n: int):
    # iterate through the `for` loop until we reach the threshold
    for i in range(2, n):
        # check if 'n' divided by 'i' has remainder(s) or not
        if n % i == 0:
            # number 'n' is composite
            return 0

    # if the number 'n' has no remainder(s) ==> 'n' is prime
    return 1
```

### Implementation in C

```C
// algorithm 1: trial division --> unoptimised
int trial_division_1(int n) {
    // iterate through the `for` loop until we reach the threshold
    for (int i = 2; i < n; i++) {
        // check if 'n' divided by 'i' has remainder(s) or not
        if (n % i == 0) {
            // number 'n' is composite
            return 0;
        }
    }

    // if the number 'n' has no remainder(s) ==> 'n' is prime
    return 1;
}
```

---

> [!WARNING]
> We need to start iterating **from** '2'!
>
> Well, all monkeys know that we <span style="color: red;"> cannot</span> divide a number by '0'.
>
> Furthermore, instead of iterating from '*1*' to `n`. We can start with '2' as, again, all monkeys know that whatever number we try to divide by the number one is going to return the number itself.
>
> Additionally, we know that the "*stop*" part ( *where `n` is* ) in our `range()` function.
> The simple reason as to why we **don't** do `n + 1` here is. If you had an actual **prime number**... Dividing that number by itself will, as all fucking monkeys know it; is going to return **no** *remainders*.
>
> This means that any **prime** number will become *composite*!
>
> > We don't want that... Or do we?
>

---

### Testing Validity of Functions

Let's now check if the *output(s)* of the functions that we wrote above $\uparrow$.

| Test Number | Python Version | C Version |
| ----------- | -------------- | --------- |
| 0 | 1 | 1 |
| 1 | 1 | 1 |
| 2 | 1 | 1 |
| 3 | 1 | 1 |
| 4 | 0 | 0 |
| 5 | 1 | 1 |
| 7 | 1 | 1 |
| 10 | 0 | 0 |
| 12 | 0 | 0 |

## Second Iteration of Trial Division Using For Loops

> [!NOTE]
> I am currently testing and using [LazyVim](). This is why the indentation is **not** going to be set to '4' spaces.
>
> > I think am starting to prefer '2' spaces for `<Tab> ` as the code does not need to go to the right as much!
>

### Implementation in Python

```python
# algorithm 2: trial division
# similarly 'unoptimised' but "proper" definition of number '1'
def trial_division_2(n: int):
    # fail early method
    if n <= 1:
        # prime numbers cannot be less or equal to 1
        return -1

    # if the number is greater than 1
    else:
        # iterate through the `for` loop until we reach the threshold ( with square root )
        for i in range(2, int(sqrt(n) + 1)):
            # check if 'n' divided by 'i' has remainders or not
            if n % i == 0:
                # number 'n' is composite
                return 0

        # if the number 'n' has no remainder(s) ==> 'n' is prime
        return 1
```

### Implementation in C

```c
// algorithm 2: trial division
// similarly 'unoptimised' but "proper" definition of number '1'
int trial_division_2(int n) {
  // fail early method
  if (n <= 1) {
    // prime numbers cannot be less or equal to 1
    return -1;
    
  } else {
    // iterate through `for` loop until we reach the threshold
    for (int i = 2; i < n; i++) {
      // check if 'n' divided 'i' has remainders or not
      if (n % i == 0) {
        // number 'n' is composite
        return 0;
      }
    }
	
    // if the number 'n' has not remainder(s) ==> 'n' is prime
    return 1;
  }
}
```

### Testing Validity of Functions

Let's now check if the *output(s)* of the functions that we wrote above $\uparrow$.

| Test Number | Python Version | C Version |
| ----------- | -------------- | --------- |
| 0 | -1 | -1 |
| 1 | -1 | -1 |
| 2 | 1 | 1 |
| 3 | 1 | 1 |
| 4 | 0 | 0 |
| 5 | 1 | 1 |
| 7 | 1 | 1 |
| 10 | 0 | 0 |
| 12 | 0 | 0 |

> [!SUCCESS]
> To be honest, this is "*complete*". Most numbers that you throw at it... Its going to give the **correct** answer obviously!
>
> But I mean... "*We can always try to optimise it much much more*!"

---

# Optimised Solution

> [!INFO] Resources
> - https://github.com/NakerTheFirst/Trial-division/blob/main/trial_division.py

While learning / researching about the "*most*" optimised solution for this. I came across the above **GitHub Link**.

Its pretty simple with our *second iteration* and it also uses the "_**superior**_" `for` loop. Below, you are going to find the complete code implement in Python and also C.

## Optimised Implementation in Python

```python
# our supposedly "opimised" trial division function
def optimised_trial_division(n: int):
    # fail early method
    if n <= 1:
        # prime numbers cannot be less or equal to 1
        return -1

    # if the number 'n' is the first prime number ( i.e '2' )
    if n == 2:
        # return '1' as we know that '2' is a prime number
        return 1

    # we know that all even numbers are / can be divided by 2
    if n % 2 == 0:
        # number 'n' is an even number and therefore composite
        return 0

    # iterate through the `for` loop until we reach the threshold ( with square root )
    # skip every even numbers as we cannot test 'primality' with even numbers
    for i in range(3, int(sqrt(n) + 1), 2):
        # check if 'n' divided by 'i' has remainders or not
        if n % i == 0:
            # number 'n' is composite
            return 0

    # if the number 'n' has no remainder(s) ==> 'n' is prime
    return 1
```

## Optimised Implementation in C

```c
// our supposedly "optimised" trial division function
int trial_division_2(int n) {
  // fail early method
  if (n <= 1) {
    // prime numbers cannot be less or equal to 1
    return -1;
  }

  // if the number 'n' is the first prime number ( i.e '2' )
  if (n == 2) {
    // return '1' as we know that '2' is a prime number
    return 1;
  }

  // we know that all even numbers are / can be devided by 2
  if (n % 2 == 0) {
    // number 'n' is an even and therefore composite
    return 0;
  }

  // iterate through `for` loop until we reach the threshold
  for (int i = 3; i <= sqrt((double)n) + 1; i += 2) {
    // check if 'n' divided 'i' has remainders or not
    if (n % i == 0) {
      // number 'n' is composite
      return 0;
    }
  }

  // if the number 'n' has not remainder(s) ==> 'n' is prime
  return 1;
}
```

### Why It's Considered "Optimised"

> Let's get started!

By definition, we know that a **negative** number <strong> <span style="color: red;"> cannot</span> </strong> be classified as a *prime number*. Therefore, we have the little `if` statement:

> I am going to explain using Python code snippets!

```python
# fail early method
if n <= 1:
	# prime numbers cannot be less or equal to 1
	return -1
```

Now, we know that after every **odd** number there going to be an **even** numbers ( *obviously* ). Additionally, we know that we <span style="color: red;"> cannot</span> ( *or more likely "would not"* ) use **even** numbers to test for *primality*!

Therefore, let's just make a little check to see if our number `n` is actually `2` or a **multiple** of 2; hence, we are going to get these 2 little `if` statements.

```python
# if the number 'n' is the first prime number ( i.e '2' )
if n == 2:
	# return '1' as we know that '2' is a prime number
	return 1

# we know that all even numbers are / can be divided by 2
if n % 2 == 0:
	# number 'n' is an even number and therefore composite
	return 0
```

This means that if we enter `2` or any other **even** number, which we know is obviously going to "*fail early*" ( *in this code its a success, you know what I mean* ). Therefore, this is going to be to improve the **performance**.

Now what about the `for` loop? Like I have been saying, and we know that we are already handling the case for `2` and **multiples** of 2. Therefore, we start at `3` and then we are going to **skip** each *even* number.

Now, the reason as to why we skip these **even** numbers. Its just because of the thing I told you above. There is no point in checking for *primality* with **even** numbers.

> Therefore, let's just completely skip them!

### Testing the Validity of the Above Function

Let's now check if the *output(s)* of the functions that we wrote above $\uparrow$.

| Test Number | Python Version | C Version |
| ----------- | -------------- | --------- |
| 0 | -1 | -1 |
| 1 | -1 | -1 |
| 2 | 1 | 1 |
| 3 | 1 | 1 |
| 4 | 0 | 0 |
| 5 | 1 | 1 |
| 7 | 1 | 1 |
| 10 | 0 | 0 |
| 12 | 0 | 0 |
| 7756935 | 0 | 0 |
| 7756937 | 1 | 1 |

> [!SUCCESS]
> Well, we have completed what our little Trial Division journey "*scientist roleplay*". Its now time to start [[Basic Sieve of Eratosthenes]]!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!