---
id: Python - Stacks ( Queue Module )
aliases: Stack ( Abstract Data Type ) implemented using Python's Queue Module
tags:
  - data-structures
  - lifo
  - python
  - queue
  - stack
author: S.Sunhaloo
date: 2026-03-07
status: HOLD
---

## List of Contents

- [[#The Queue Module]]
- [[#Create A Stack]]
- [[#Function / Method Related To Stack]]
	- [[#Data Insertion Method ( Pushing Data )]]
		- [[#Pushing And Waiting]]
		- [[#Pushing And Not Waiting]]
	- [[#Data Removal Method]]
		- [[#To Get Or TO Get No Wait?]]
	- [[#Miscellaneous Methods]]
		- [[#Peek The Top Value]]
		- [[#Length Of Stack]]
		- [[#Check If Stack Is Empty Or Not]]
		- [[#Check If Stack Is Full Or Not]]
		- [[#Display Stack]]
- [[#Creation Of Stack and Usage]]

---

> [!INFO] Resource(s)
> - [[Python - Stacks ( List )]]
> - [[Python - Stacks ( Classes )]]
> - Python Queue Module: https://docs.python.org/3/library/queue.html

> [!NOTE]
> I highly recommend you that you go to each one of the above **resources** and *in order* so as to get an idea of what we are actually trying to implement.

# The Queue Module

This module is **not** just a simple module that exists to just allow us to create *abstract data type*.

Its actually use for things like [Multi-processing](https://en.wikipedia.org/wiki/Multiprocessing) and [Multi-threading](https://en.wikipedia.org/wiki/Multithreading_(computer_architecture)) due to its **speed** and **thread-safety**!

Nevertheless, we are not going to be doing all of that and instead focus of the movement of data / elements instead.

> [!WARNING]
> Do remember to **add** the following line at the top of the file if you want to create a "*Stack*" from the `queue` module
> 
> ```python
> # import the "stack" / LIFO abstract data type from the 'queue' module
> from queue import LifoQueue
> ```
> 
> But I also recommended you to import the `Full` and `Empty` *error handling* from the `queue` module! Therefore, the import line is going to be updated to:
> 
> ```python
> from queue import Empty, Full, LifoQueue
> ```
> 
> > I *might* show you later why we might need them!

> [!BUG]
> Remember to link C's multi-threading ( *coding* ) file **down below**!

> [!INFO]
> You could trying checking C programming notes on Posix compliant threads: ''

# Create A Stack

There are two main ways to creating a "*stack*" through the `queue` module. The stack *could* have a **maximum size limit** or not!

```python
# create stack with no maximum size limit
large_stack: LifoQueue = LifoQueue()

# create stack with maximum size limit of 3
small_stack: LifoQueue = LifoQueue(maxsize=3)
```

> [!NOTE] Error Handling!
> - If the `LifoQueue` stack is **empty**
> 	- It will raise a `queue.Empty` ( *or simply `Empty` ( see updated above import line )* ) error
> - If the `LifoQueue` stack is **full**
> 	- It will raise a `queue.Full` ( *or simply `Full` ( see updated above import line )* ) error

---

> [!WARNING]
> I am going to *try* to keep it simply and only focus on the functions and methods related to **making** the 'Stack' abstract data type!
> 
> > I am not going to do in-depth and take notes on thing like `.shutdown` and more!

# Function / Method Related To Stack

## Data Insertion Method ( Pushing Data )

### Pushing And Waiting

> [!TIP]
> If you **don't** have time to read this; then simply use `.put_nowait()`!
> 
> See it explanation down [[#Putting And Not Waiting | below]].

The `.put` method is going to allow the user to enter an element into the `LifoQueue` but with some exceptions.

> I am going to be a `LifoQueue` with a `maxsize` of 3!

```python
# create stack with maximum size limit of 3
stack: LifoQueue = LifoQueue(maxsize=3)

# add elements using the `.put` method
stack.put(1)
stack.put(2)
stack.put(3)
```

Go ahead and run the above code, you are going to see that it does *run* **fine**.

> Then what's the problem you ask!

Let's try `put`ting another *item* inside the stack see run the code again:

```python
# create stack with maximum size limit of 3
stack: LifoQueue = LifoQueue(maxsize=3)

# add elements using the `.put` method
stack.put(1)
stack.put(2)
stack.put(3)

# add another element to a stack with a maximum size of 3
stack.put(4)
```

> [!BUG] It Just Hangs!
> Yes, *running* the above code is just going to hang **indefinitely**!
> 
> This is mainly due to the fact that we are trying to *conform* `queue` to work like a simple 'Stack'.
> 
> Like, these things are used when we, again, have **multi-processing** and / or **multi-threading**.
> 
> Hence, if you know a little bit about the 'consumer-producer' concept in multi-threading; then you are going to know that we **don't** have *any* type of **consumer** to consume the data found in that small stack.
> 
> > Thus it's going to hang indefinitely!

#### Change The Parameters

> [!INFO] Resource(s)
> - Python Documentation ( `.put` ): https://docs.python.org/3/library/queue.html#queue.Queue.put
> 
> Go ahead and read the above documentation; there you are going to find the parameters that the `.put` method accepts.

> The following code below will need the above code to run!

- Don't `block` for input:

```python
# add another element to a stack and don't block if stack if already full
stack.put(4, block=False)
```

> [!SUCCESS] "SUCCESS"
> Hence, we should see that now the code is **not** going to hang *indefinitely*!
> 
> Instead the code is going to immediately *raise* the `queue.Full` error.

- Add a `timeout`:

```python
# add another element to a stack and add timeout if stack if already full
stack.put(4, timeout=2)
```

> [!SUCCESS] "SUCCESS"
> Here also, we should see that now the code is **not** going to hang *indefinitely*!
> 
> Instead the code is going to immediately *raise* the `queue.Full` error.

### Pushing And Not Waiting

> Its literally the **same** thing as `.put(item, block=False)`

This is the method that we should have been using from the beginning. But I wanted to understand the difference first as we know that the `.put_nowait` was using the `.put` under the hood!

```python
# create stack with maximum size limit of 3
stack: LifoQueue = LifoQueue(maxsize=3)

# add element using the `.put_nowait_nowait` method
stack.put_nowait(1)
stack.put_nowait(2)
stack.put_nowait(3)

# try adding another element into the size-limited stack
stack.put_nowait(4)
```

## Data Removal Method

### To Get Or TO Get No Wait?

> My English is so exquisite!

> [!INFO] Resource(s)
> - Python Documentation ( `.get` ): https://docs.python.org/3/library/queue.html#queue.Queue.get
> 
> Please, do a and go head the documentation on what type of parameters that `.get` can accept

> [!NOTE] Difference between `.get` and `.get_nowait`
> 
> Its the **same** *principle* as `.put` and `.put_nowait`. But in this case, if a `LifoQueue` stack is **empty** and we try to specifically use the `.get` method.
> 
> > Its going to **hang** *indefinitely*!
> 
> Again, this is because in our specific case, we **don't** have a *producer*.
> 
> > [!INFO]
> > In this case, its going to throw a `queue.Empty` error instead of a `queue.Full` error.
> > 
> > > It makes perfect sense to be honest...

#### Popping Data From Stack

Here, given our use case; we are simply going to be using the `.get_nowait` method to **remove** data from the stack.

> The `.get_notwait()` function is equivalent to `.get(block=False)`!

```python
# remove element using the `.get_nowait` method
popped_element = stack.get_nowait()
```

## Miscellaneous Methods

### Peek The Top Value

> [!BUG] We **don't** have that here!
> 
> Yes, we **cannot** simply do something like `stack[-1]` ( *see the value* ) or something like that here!

Therefore, to be able to check what value we have at the top, we are going to first have to **remove** it and then **add** it back again!

```python
# remove element using the `.get_nowait` method
top_element = stack.get_nowait()

# WARNING: make sure that we add the "top" element back into the stack
stack.put_nowait(top_element)
```

#### Simple Function To Peek Top Element

This is a simple function that I made to basically "*automate*" that process for us and return the `top_element`

```python
# function to be able to see / peak the top element
def peek_element(stack: LifoQueue):
    # remove the top element
    top_element = stack.get_nowait()

    # add the top element back into the stack
    stack.put_nowait(top_element)

    return top_element
```

### Length Of Stack

We have a built-in `.qsize` method that will allow us to display the length of the stack

```python
# find the length of the stack
print(f"Length Of Stack: {stack.qsize()}")
```

### Check If Stack Is Empty Or Not

Here, we have a specific `.empty` method that will allow to check if the "*stack*" is empty or not!

> No need for some `len(stack) == 0` or `not bool(stack)`...

```python
# check if the stack is empty
print(f"Stack Empty?: {stack.empty()}")
```

### Check If Stack Is Full Or Not

In this case, we have another check that we can perform on our `LifoQueue` stack. And that is to check if its **full** or not!

```python
# check if the stack is full
print(f"Stack Empty?: {stack.full()}")
```

### Display Stack

> [!WARNING]
> The following code was generated by [Claude](https://claude.ai)
> 
> > But it seems to follow the normal convention for this code after looking around!

```python
# function to display the elements in stack ( drain and restore technique )
def display_stack(stack: LifoQueue):
    # initialise a temporary list
    temp: list = []

    # iterate through stack until it become empty --> add data to `temp` list
    while not stack.empty():
        temp.append(stack.get_nowait())

    # INFO: I like when the latest / top value is found on the right-most index
    print(list(reversed(temp)))

    # restore the elements in correct order using `reversed`
    # WARNING: need to do this as we actually removed the value when we `get_nowait`
    for item in reversed(temp):
        stack.put_nowait(item)
```

> [!BUG] This is **not** recommended at all!
> 
> So let's say that you are working in the [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop) ( *for whatever reasons* ) and you quickly need to display the `LifoQueue`.
> 
> Therefore, you can do the following:
> 
> ```python
> # display the stack by accessing the internal `deque` attribute
> print(list(stack.queue))
> ```
> 
> Nevertheless, this is **not** recommended at all as it by-passes everything and **not** *safe* to use when doing "*threading*" work.
> 
> > That is why in my lecturer sample code, she did not display the stack!

---

# Creation Of Stack and Usage

Here is simple, example of what we get when we combine all of these functions above

> [!INFO]
> I hard-coded the input and deletion; but you can easily use a `for` loop to create another *simple* function if you want to allow for user input!

```python
from queue import LifoQueue


# function to be able to see / peak the top element
def peek_element(stack: LifoQueue):
    # remove the top element
    top_element = stack.get_nowait()

    # add the top element back into the stack
    stack.put_nowait(top_element)

    return top_element


# function to display the elements in stack ( drain and restore technique )
def display_stack(stack: LifoQueue):
    # initialise a temporary list
    temp: list = []

    # iterate through stack until it become empty --> add data to `temp` list
    while not stack.empty():
        temp.append(stack.get_nowait())

    # INFO: I like when the latest / top value is found on the right-most index
    print(list(reversed(temp)))

    # restore the elements in correct order using `reversed`
    # WARNING: need to do this as we actually removed the value when we `get_nowait`
    for item in reversed(temp):
        stack.put_nowait(item)


# our main function
def main():
    # create stack with maximum size limit of 3
    stack: LifoQueue = LifoQueue(maxsize=3)

    # check if the stack is empty
    print(f"\nStack Empty?: {stack.empty()}", "\n" + "-" * 50)

    # find the size of the stack
    print(f"\nSize Of Stack: {stack.qsize()}", "\n" + "-" * 50)

    # push data onto the stack using `.put_nowait`
    stack.put_nowait(1)
    stack.put_nowait(2)
    stack.put_nowait(3)

    print("\nCurrent Contents Of Stack: ", end="")

    # display the stack by calling the function
    display_stack(stack)

    print("-" * 50)

    # check if the stack is full
    print(f"\nStack Full?: {stack.full()}", "\n" + "-" * 50)

    # find the size of the stack
    print(f"\nSize Of Stack: {stack.qsize()}", "\n" + "-" * 50)

    # peek at the top value
    print(f"\nTop Element = {peek_element(stack)}", "\n" + "-" * 50)

    # pop data from the stack using `.get_nowait`
    popped_element = stack.get_nowait()
    print(f"\nPopped Element = {popped_element}", "\n" + "-" * 50)

    print("\nCurrent Contents Of Stack: ", end="")

    # display the stack by calling the function
    display_stack(stack)

    print("-" * 50)

    # find the size of the stack
    print(f"\nSize Of Stack: {stack.qsize()}", "\n" + "-" * 50)

    # pop all remaining elements
    while not stack.empty():
        stack.get_nowait()

    # check if the stack is empty
    print(f"\nStack Empty?: {stack.empty()}", "\n" + "-" * 50)


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