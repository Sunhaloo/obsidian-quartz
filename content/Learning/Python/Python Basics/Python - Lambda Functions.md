---
id: Python - Lambda Functions
aliases: Lambda ( Anonymous ) Functions in Python
tags:
  - python
  - basics
author: S.Sunhaloo
date: 2025-10-06
status: Completed
---

## List of Contents

- [[#What Is The Point?]]
	- [[#The Better Way!]]
- [[#The Reason ( In My Case )!]]

---

# What Is The Point?

Let's say that we need to find to the **sum** of a *series* of numbers quickly and you don't have a calculator in your Linux Desktop Environment just like me ( *because its bloat*!!! ).

Therefore, you are going to open the Python [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop) and go ahead a write something like that:

```python
# quickly make a function that take a number of arguments
def add(*args):
    # use the in-built `sum` function
    return sum(args)


# therefore, we can simply do something like this:
print(add(1, 2, 69, 69.6969, 3, 4, 5))
```

> Therefore we do get our *correct* output of: 153.6969

## The Better Way!

As you know there is always a better way of doing something in Python and this also applies here!

- Using `lambda` function, the *above* `add` function is converted to this:

```python
# FOR REAL FOR REAL --> quickly make an actual quick add function
print((lambda *args: sum(args))(1, 2, 69, 69.6969, 3, 4, 5))
```

> [!INFO] The Fuck The Actual Difference!
> If you look in terms of memory and others... Using `lambda` is pretty much just the **same** as defining a function using the `def` keyword!
>
> The actual **difference** comes to how the *user* is going to use it!
>
> > If you only need to use a *function* <strong> <span style="color: orange;"> once</span> </strong> ! There is **no** point in *creating* a function using `def`!!!
>
> For example, if you just need a quick little calculation, or another function requires a parameter, we can simply use a `lambda` function **inline** *inside* the "*other*" function!

---

# The Reason ( In My Case )!

> [!NOTE]
> The reason as to why I am learning this is because of '[[DSA - Labsheet 4 ( L2S1 )]]'!
>
> The lecturer since the beginning was using the `timeit.timeit()` function to *time* stuff.
>
> > From what I can see, its a better `time.perf_counter()`!
>
> But using the `timeit.timeit()` function inside our *unofficial, official* Python Boilerplate, we get errors!
>
> > It does **not** let me!
>
> Nevertheless, I still wanted to know how this can be achieved and its by using `lambda` functions!
>
> Therefore, here is the *link* to the [[DSA - Labsheet 4 ( L2S1 )#Question 1| first question]] to use a **reference**!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!