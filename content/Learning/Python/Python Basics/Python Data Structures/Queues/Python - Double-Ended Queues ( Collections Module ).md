---
id: Python - Double-Ended Queues ( Collections Module )
aliases: Queue ( Abstract Data Type ) implemented using Python's Collections Module
tags:
  - collections
  - data-structures
  - fifo
  - python
  - queue
author: S.Sunhaloo
date: 2026-03-08
status: Completed
---

## List of Contents

- [[#The Collections Module]]
- [[#Create A Double-Ended Queue]]
- [[#Function / Method Related To Queue]]
	- [[#Data Insertion Method]]
		- [[#Enqueuing To The Right Side]]
		- [[#Enqueuing To The Left Side]]
	- [[#Data Removal Method]]
		- [[#Dequeuing To The Right Side]]
		- [[#Dequeuing To The Left Side]]
	- [[#Miscellaneous Methods]]
		- [[#Peek Values?]]
		- [[#Length Of Queue]]
		- [[#Check If Queue Is Empty Or Not]]
		- [[#Display Queue]]
- [[#Creation Of Double-Ended Queue and Usage]]

---

> [!INFO] Resource(s)
> - [[Python - Queues ( List )]]
> - [[Python - Queues ( Classes )]]
> - [[Python - Queues ( Queue Module )]]
> - [[Python - Queues ( Linked List )]]
> - Python Collections Module: https://docs.python.org/3/library/collections.html

> [!NOTE]
> I highly recommend you that you go to each one of the above **resources** and *in order* so as to get an idea of what we are actually trying to implement.

> [!WARNING] Double-Ended Queues
> The `deque` from the `collections` module give us **double-ended** queue!
> 
> Compared to the single-ended queues that we have been learning ( *see above 'Resources'* ).
> 
> A *double-ended* could can allow the user to **enqueue** in data in **both** the "*`front`*" and the "*`rear`*" of the queue.
> 
> > Meaning that we also have two places whereby we can **dequeue** elements!

> [!WARNING]
> Do remember to **add** the following line at the top of the file if you want to create a "*Queue*" from the `collections` module
> 
> ```python
> # import the "queue" / FIFO abstract data type from the 'collections' module
> from collections import deque
> ```
> 
> > As for error handling, **no** need to *import* anything we are just going to be using simple `.append` and `.pop` function!

# The Collections Module

From what I can understand from the documentation and after chatting with [Claude](https://claude.ai).

The `collections` module provides with **specialised** "*container*" data types that leverages *general* data structures like `list`, `tuple`, `set`, `dict`.

> Its basically more efficient ways to manipulate specific data for specific use-cases!

# Create A Double-Ended Queue

There are two main ways to create a "*queue*" through the `collections` module. The queue *could* have a **maximum length limit** or not!

```python
# create queue with no maximum size limit
large_queue: deque = deque()

# create queue with maximum length limit of 3
small_queue: deque = deque(maxlen=3)
```

> [!INFO]
> - Python `deque` Function: https://docs.python.org/3/library/collections.html#collections.deque
> 
> Looking at the documentation about; I can see that we can pass an **iterable** as an argument!
> 
> This means that we can do something like this:
> 
> ```python
> # create a deque from a list
> list_queue: deque = deque([1, 2, 3])
> 
> # create a deque from a string
> string_queue: deque = deque("hello")
> ```
> 
> > [!WARNING]
> > If you pass something like `"hello"` like we did above in the code block...
> > 
> > This is actually going to be converted to `['h', 'e', 'l', 'l', 'o']`!
> > 
> > > Each *character* becomes an **element** inside a `list`!

---

# Function / Method Related To Queue

## Data Insertion Method

> I am going to be a `dequeu` with a `maxlen` of 3!

### Enqueuing To The Right Side

To be able to add / enqueue an element to the right side of our `queue`; we can simply use the `.append`.

```python
# create queue with maximum length limit of 3
queue: deque = deque(maxlen=3)

# add elements ( to the right ) using the `.append` method
queue.append(1)
queue.append(2)
queue.append(3)
```

> [!WARNING] Adding Elements Beyond `maxlen`!
> Compared to the `.put` method that we learned to use over at '[[Python - Stacks ( Queue Module )#Pushing And Waiting | Python - Stacks ( Queue Module )]]' and '[[Python - Queues ( Queue Module )#Enqueuing And Waiting | Python - Queues ( Queue Module )]]'.
> 
> If we add another item using the `.put` method, you know that its just going to **hang** the program *forever*!
> 
> But with the `dequeu` *data type*, its **not** the case!
> 
> The program simply *runs* **without** any errors but does **not** actually *add* the element to the `queue` ( *provided, again, that we do use `maxlen`* )

### Enqueuing To The Left Side

To be able to add / enqueue elements to the **left** of the `deque` data structure. We are going to use a special `.appendleft` method provided by that "*container*" / data structure

```python
# create queue with maximum length limit of 3
queue: deque = deque(maxlen=3)

# add elements ( to the left ) using the `.appendleft` method
queue.appendleft(1)
queue.appendleft(2)
queue.appendleft(3)
```

> [!NOTE] Adding Element Beyond `maxlen`
> We do have the **same** behaviour here whereby the element does **not** actually gets *inserted* into the `queue` and the program **continues** to *run* **without** any errors!

## Data Removal Method

> Do I need to say something here; I think you get the point!

### Dequeuing To The Right Side

```python
# remove element ( from the right ) using the `.pop` method
popped_element = queue.pop()
```

### Dequeuing To The Left Side

```python
# remove element ( from the left ) using the `.popleft` method
popped_element = queue.popleft()
```

## Miscellaneous Methods

### Peek Values?

Okay, given that this **double-ended** queue, there is no actual *top-value*...

Instead, I am going to use `[-1]` and `[0]` to get the **right-most** and **left-most** element respectively.

> I am going to simply write a function for both of them!

#### Peek The Right-most Value

```python
# function to be able to see / peek the right-most value
def peek_right_most(queue: deque):
    # simply return last / right-most element for queue
    return queue[-1]
```

#### Peek The Left-most Value

```python
# function to be able to see / peek the left-most value
def peek_left_most(queue: deque):
    # simply return first / left-most element for queue
    return queue[0]
```

### Length Of Queue

Well, you use the trusty `len` function provided by Python to find the **length** of the *list*!

```python
# find the length of the queue
print(f"Length Of Queue: {len(queue)}")
```

### Check If Queue Is Empty Or Not

#### Using the Length Function

Using the `len`gth function, we can use this simple function below to check if the queue is empty or not.

```python
# function to check if the queue is empty or not ( using length function )
def empty_check(queue: deque) -> bool:
    return len(queue) == 0
```

#### Using Boolean Type Casting

> Falsy and Truthy Value!

Here are are going to leverage **[[Python Language Basics#Type Cast | type casting]]** and '*truthy / falsy*' value to be able to check if the queue is empty or not!

```python
# function to check if the queue is empty or not ( using type casting )
def empty_check(queue: deque) -> bool:
    return not bool(queue)
```

### Display Queue

#### Using The Simple `print` Function

Yes! You can use the `print` statement to display the `deque`.

```python
# display the "deque" queue with our trusty little `print` statement
print(queue)
```

- But the output is absolutely shit!

```console
deque([1, 2, 3], maxlen=3)
```

> It also displays the fucking `maxlen` parameter with its value passed into it for some reason

#### Using Temporary Lists

Or we can create a simple function that just uses a temporary `list` to display the contents of the "*queue*".

```python
# function to display the elements in queue
def display_queue(queue: deque):
    # initialise a temporary list
    temp: list = []

    # iterate through the whole 'deque' queue
    for i in queue:
        temp.append(i)

    print(temp)
```

---

# Creation Of Double-Ended Queue and Usage

> [!INFO]
> I hard-coded the input and deletion; but you can easily use a `for` loop to create another *simple* function if you want to allow for user input!
>
> > Compared to '[[Python - Queues ( List )]]'; you basically use *our* functions!
>
> [!WARNING]
> This queue implementation will work with **all** data types!
>
> I just choose to use `int`eger numbers for this one...

```python
# import the "queue" / FIFO abstract data type from the 'collections' module
from collections import deque


# function to be able to see / peek the right-most value
def peek_right_most(queue: deque):
    # simply return last / right-most element for queue
    return queue[-1]


# function to be able to see / peek the left-most value
def peek_left_most(queue: deque):
    # simply return first / left-most element for queue
    return queue[0]


# function to check if the queue is empty or not ( using length function )
def empty_check(queue: deque) -> bool:
    return len(queue) == 0


# function to check if the queue is empty or not ( using type casting )
def empty_check_bool(queue: deque) -> bool:
    return not bool(queue)


# function to display the elements in queue
def display_queue(queue: deque):
    # initialise a temporary list
    temp: list = []

    # iterate through the whole 'deque' queue
    for i in queue:
        temp.append(i)

    print(temp)


# our main function
def main():
    # create queue with maximum length limit of 3
    queue: deque = deque(maxlen=3)

    # check if the queue is empty ( using the length implementation )
    print(f"\nQueue Empty?: {empty_check(queue)}", "\n" + "-" * 50)

    # find the length of queue
    print(f"\nLength Of Queue: {len(queue)}", "\n" + "-" * 50, "\n")

    # enqueue data onto the queue using `.append` ( right side )
    queue.append(1)
    queue.append(2)
    queue.append(3)

    print("Current Contents Of Queue ( after .append ): ", end="")
    display_queue(queue)

    print("\n" + "-" * 50)

    # enqueue data onto the queue using `.appendleft` ( left side )
    queue.appendleft(0)

    print("\nCurrent Contents Of Queue ( after .appendleft ): ", end="")

    # display the queue using my little function
    display_queue(queue)

    print("-" * 50)

    # find the length of queue
    print(f"\nLength Of Queue: {len(queue)}", "\n" + "-" * 50)

    # peek at the right-most value
    print(f"\nRight-Most Element = {peek_right_most(queue)}", "\n" + "-" * 50)

    # peek at the left-most value
    print(f"\nLeft-Most Element = {peek_left_most(queue)}", "\n" + "-" * 50)

    # check if the queue is empty ( using the boolean implementation )
    print(f"\nQueue Empty?: {empty_check_bool(queue)}", "\n" + "-" * 50)

    # dequeue data from the queue using `.popleft` ( left side )
    dequeued_element = queue.popleft()
    print(f"\nDequeued Element ( from left ) = {dequeued_element}", "\n" + "-" * 50)

    print("\nCurrent Contents Of Queue ( after .appendleft ): ", end="")

    # display the queue using my little function
    display_queue(queue)

    print("-" * 50)

    # dequeue data from the queue using `.pop` ( right side )
    dequeued_element = queue.pop()
    print(f"\nDequeued Element ( from right ) = {dequeued_element}", "\n" + "-" * 50)

    print("\nCurrent Contents Of Queue ( after .appendleft ): ", end="")

    # display the queue using my little function
    display_queue(queue)

    print("-" * 50)

    # find the length of queue
    print(f"\nLength Of Queue: {len(queue)}", "\n" + "-" * 50)

    # peek at the right-most value
    print(f"\nRight-Most Element = {peek_right_most(queue)}", "\n" + "-" * 50)

    # peek at the left-most value
    print(f"\nLeft-Most Element = {peek_left_most(queue)}", "\n" + "-" * 50)

    # check if the queue is empty ( using the length implementation )
    print(f"\nQueue Empty?: {empty_check(queue)}", "\n" + "-" * 50)

    # clear the whole `clear` method
    queue.clear()

    # check if the queue is empty ( using the boolean implementation )
    print(f"\nQueue Empty?: {empty_check_bool(queue)}", "\n" + "-" * 50)

    # find the length of queue
    print(f"\nLength Of Queue: {len(queue)}", "\n" + "-" * 50)

    print("\n== Final Queue Representation ==\n")

    # display the queue using our trusty little `print` function
    print(queue)


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