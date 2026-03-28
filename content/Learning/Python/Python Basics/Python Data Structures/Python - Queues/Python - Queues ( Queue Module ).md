---
id: Python - Queues ( Queue Module )
aliases: Queue ( Abstract Data Type ) implemented using Python's Queue Module
tags:
  - data-structures
  - fifo
  - python
  - queue
author: S.Sunhaloo
date: 2026-03-07
status: Completed
---

## List Of Contents

- [[#Create A Queue]]
- [[#Function / Method Related To Queue]]
	- [[#Data Insertion Method]]
		- [[#Enqueuing And Waiting]]
		- [[#Enqueuing And Not Waiting]]
	- [[#Data Removal Method]]
		- [[#To Get Or To Get No Wait?]]
	- [[#Miscellaneous Methods]]
		- [[#Peek The Front Value]]
		- [[#Length Of Queue]]
		- [[#Check If Queue Is Empty Or Not]]
		- [[#Check If Queue Is Full Or Not]]
		- [[#Display Queue]]
- [[#Creation Of Queue and Usage]]

---

> [!INFO] Resource(s)
> - [[Python - Queues ( List )]]
> - [[Python - Queues ( Classes )]]
> - Python Queue Module: https://docs.python.org/3/library/queue.html#module-queue

> [!NOTE]
> I highly recommend you that you go to each one of the above **resources** and *in order* so as to get an idea of what we are actually trying to implement.

> [!WARNING]
> If you want a little, extremely naive introduction to what the `queue` module is all about.
> 
> Then, refer to my note: '[[Python - Stacks ( Queue Module )#The Queue Module | Python - Stacks ( Queue Module )]]' for just a tad bit more information.
> 
> > I am not going to repeat myself over here and there is [Google](https://google.com) and Large Language Models!

> [!WARNING] Another Warning!
> Do remember to **add** the following line at the top of the file if you want to create a "*Queue*" from the `queue` module
> 
> ```python
> # import the "queue" / FIFO abstract data type from the 'queue' module
> from queue import Queue
> ```
> 
> But I also recommended you to import the `Full` and `Empty` *error handling* from the `queue` module! Therefore, the import line is going to be updated to:
> 
> ```python
> from queue import Empty, Full, Queue
> ```

# Create A Queue

There are two main ways to create a "*queue*" through the `queue` module. The queue *could* have a **maximum size limit** or not!

```python
# create queue with no maximum size limit
large_queue: Queue = Queue()

# create queue with maximum size limit of 3
small_queue: Queue = Queue(maxsize=3)
```

> [!NOTE] Error Handling!
> - If the `Queue` is **empty**
> 	- It will raise a `queue.Empty` ( *or simply `Empty` ( see updated above import line )* ) error
> - If the `Queue` is **full**
> 	- It will raise a `queue.Full` ( *or simply `Full` ( see updated above import line )* ) error

---

> [!WARNING]
> I am going to *try* to keep it simple and only focus on the functions and methods related to **making** the 'Queue' abstract data type!
> 
> > I am not going to do in-depth and take notes on things like `.shutdown` and more!

# Function / Method Related To Queue

## Data Insertion Method

### Enqueuing And Waiting

> [!TIP]
> If you **don't** have time to read this; then simply use `.put_nowait()`!
> 
> See its explanation down [[#Enqueuing And Not Waiting | below]].

The `.put` method is going to allow the user to enter an element into the `Queue` but with some exceptions.

> I am going to be a `Queue` with a `maxsize` of 3

```python
# create queue with maximum size limit of 3
queue: Queue = Queue(maxsize=3)

# add elements using the `.put` method
queue.put(1)
queue.put(2)
queue.put(3)
```

Go ahead and run the above code, you are going to see that it does *run* **fine**.

> Then what's the problem you ask!

Let's try `put`ting another *item* inside the queue and see what happens:

```python
# create queue with maximum size limit of 3
queue: Queue = Queue(maxsize=3)

# add elements using the `.put` method
queue.put(1)
queue.put(2)
queue.put(3)

# add another element to a queue with a maximum size of 3
queue.put(4)
```

> [!BUG] It Just Hangs!
> Yes, *running* the above code is just going to hang **indefinitely**!
> 
> This is mainly due to the fact that we are trying to *conform* `queue` to work like a simple 'Queue'.
> 
> Like, these things are used when we, again, have **multi-processing** and / or **multi-threading**.
> 
> Hence, if you know a little bit about the 'consumer-producer' concept in multi-threading; then you are going to know that we **don't** have *any* type of **consumer** to consume the data found in that small queue.
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
# add another element to a queue and don't block if queue is already full
queue.put(4, block=False)
```

> [!SUCCESS] "SUCCESS"
> Hence, we should see that now the code is **not** going to hang *indefinitely*!
> 
> Instead the code is going to immediately *raise* the `queue.Full` error.

- Add a `timeout`:

```python
# add another element to a queue and add timeout if queue is already full
queue.put(4, timeout=2)
```

> [!SUCCESS] "SUCCESS"
> Here also, we should see that now the code is **not** going to hang *indefinitely*!
> 
> Instead the code is going to immediately *raise* the `queue.Full` error.

### Enqueuing And Not Waiting

> Its literally the **same** thing as `.put(item, block=False)`

This is the method that we should have been using from the beginning. But I wanted to understand the difference first as we know that the `.put_nowait` was using the `.put` under the hood!

```python
# create queue with maximum size limit of 3
queue: Queue = Queue(maxsize=3)

# add element using the `.put_nowait` method
queue.put_nowait(1)
queue.put_nowait(2)
queue.put_nowait(3)

# try adding another element into the size-limited queue
queue.put_nowait(4)
```

## Data Removal Method

### To Get Or To Get No Wait?

> My English is so exquisite!

> [!INFO] Resource(s)
> - Python Documentation ( `.get` ): https://docs.python.org/3/library/queue.html#queue.Queue.get
> 
> Please, do go ahead and read the documentation on what type of parameters that `.get` can accept

> [!NOTE] Difference between `.get` and `.get_nowait`
> 
> Its the **same** *principle* as `.put` and `.put_nowait`. But in this case, if a `Queue` is **empty** and we try to specifically use the `.get` method.
> 
> > Its going to **hang** *indefinitely*!
> 
> Again, this is because in our specific case, we **don't** have a *producer*.
> 
> > [!INFO]
> > In this case, its going to throw a `queue.Empty` error instead of a `queue.Full` error.
> > 
> > > It makes perfect sense to be honest...

#### Dequeuing Data From Queue

Here, given our use case; we are simply going to be using the `.get_nowait` method to **remove** data from the queue.

> The `.get_nowait()` function is equivalent to `.get(block=False)`!

```python
# remove element using the `.get_nowait` method
dequeued_element = queue.get_nowait()
```

## Miscellaneous Methods

### Peek The Front Value

> [!BUG] We **don't** have that here!
> 
> Yes, we **cannot** simply do something like `queue[0]` ( *see the value* ) or something like that here!

Therefore, to be able to check what value we have at the front, we are going to first have to **remove** it and then **add** it back again!

```python
# remove element using the `.get_nowait` method
front_element = queue.get_nowait()

# save all other elements
temp: list = []
while not queue.empty():
    temp.append(queue.get_nowait())

# put the front element back first
queue.put_nowait(front_element)

# put all other elements back in their original order
for item in temp:
    queue.put_nowait(item)
```

#### Simple Function To Peek Front Element

This is a simple function that I made to basically "*automate*" that process for us and return the `front_element`

```python
# function to be able to see / peek the front element
def peek_element(queue: Queue):
    # remove the front element
    front_element = queue.get_nowait()

    # save all other elements
    temp: list = []
    while not queue.empty():
        temp.append(queue.get_nowait())

    # put the front element back first
    queue.put_nowait(front_element)

    # put all other elements back in their original order
    for item in temp:
        queue.put_nowait(item)

    return front_element
```

### Length Of Queue

We have a built-in `.qsize` method that will allow us to display the length of the queue

```python
# find the length of the queue
print(f"Length Of Queue: {queue.qsize()}")
```

### Check If Queue Is Empty Or Not

Here, we have a specific `.empty` method that will allow to check if the "*queue*" is empty or not!

> No need for some `len(queue) == 0` or `not bool(queue)`...

```python
# check if the queue is empty
print(f"Queue Empty?: {queue.empty()}")
```

### Check If Queue Is Full Or Not

In this case, we have another check that we can perform on our `Queue`. And that is to check if its **full** or not!

```python
# check if the queue is full
print(f"Queue Full?: {queue.full()}")
```

### Display Queue

> [!WARNING]
> The following code was generated by [Claude](https://claude.ai)
> 
> > But it seems to follow the normal convention for this code after looking around!

```python
# function to display the elements in queue ( drain and restore technique )
def display_queue(queue: Queue):
    # initialise a temporary list
    temp: list = []

    # iterate through queue until it become empty --> add data to `temp` list
    while not queue.empty():
        temp.append(queue.get_nowait())

    print(temp)

    # restore the elements in correct order
    # WARNING: need to do this as we actually removed the value when we `get_nowait`
    for item in temp:
        queue.put_nowait(item)
```

> [!BUG] This is **not** recommended at all!
> 
> So let's say that you are working in the [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop) ( *for whatever reasons* ) and you quickly need to display the `Queue`.
> 
> Therefore, you can do the following:
> 
> ```python
> # display the queue by accessing the internal `deque` attribute
> print(list(queue.queue))
> ```
> 
> Nevertheless, this is **not** recommended at all as it by-passes everything and **not** *safe* to use when doing "*threading*" work.
> 
> > That is why in my lecturer sample code, she did not display the queue!

---

# Creation Of Queue and Usage

Here is simple, example of what we get when we combine all of these functions above.

> [!INFO]
> I hard-coded the input and deletion; but you can easily use a `for` loop to create another *simple* function if you want to allow for user input!

```python
from queue import Queue


# function to be able to see / peek the front element
def peek_element(queue: Queue):
    # remove the front element
    front_element = queue.get_nowait()

    # save all other elements
    temp: list = []
    while not queue.empty():
        temp.append(queue.get_nowait())

    # put the front element back first
    queue.put_nowait(front_element)

    # put all other elements back in their original order
    for item in temp:
        queue.put_nowait(item)

    return front_element


# function to display the elements in queue ( drain and restore technique )
def display_queue(queue: Queue):
    # initialise a temporary list
    temp: list = []

    # iterate through queue until it become empty --> add data to `temp` list
    while not queue.empty():
        temp.append(queue.get_nowait())

    print(temp)

    # restore the elements in correct order
    # WARNING: need to do this as we actually removed the value when we `get_nowait`
    for item in temp:
        queue.put_nowait(item)


# our main function
def main():
    # create queue with maximum size limit of 3
    queue: Queue = Queue(maxsize=3)

    # check if the queue is empty
    print(f"\nQueue Empty?: {queue.empty()}", "\n" + "-" * 50)

    # find the size of the queue
    print(f"\nSize Of Queue: {queue.qsize()}", "\n" + "-" * 50)

    # enqueue data onto the queue using `.put_nowait`
    queue.put_nowait(1)
    queue.put_nowait(2)
    queue.put_nowait(3)

    print("\nCurrent Contents Of Queue: ", end="")

    # display the queue by calling the function
    display_queue(queue)

    print("-" * 50)

    # check if the queue is full
    print(f"\nQueue Full?: {queue.full()}", "\n" + "-" * 50)

    # find the size of the queue
    print(f"\nSize Of Queue: {queue.qsize()}", "\n" + "-" * 50)

    # peek at the front value
    print(f"\nFront Element = {peek_element(queue)}", "\n" + "-" * 50)

    # dequeue data from the queue using `.get_nowait`
    dequeued_element = queue.get_nowait()
    print(f"\nDequeued Element = {dequeued_element}", "\n" + "-" * 50)

    print("\nCurrent Contents Of Queue: ", end="")

    # display the queue by calling the function
    display_queue(queue)

    print("-" * 50)

    # find the size of the queue
    print(f"\nSize Of Queue: {queue.qsize()}", "\n" + "-" * 50)

    # dequeue all remaining elements
    while not queue.empty():
        queue.get_nowait()

    # check if the queue is empty
    print(f"\nQueue Empty?: {queue.empty()}", "\n" + "-" * 50)


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