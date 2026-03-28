---
id: Python - Queues ( List )
aliases: Queue ( Abstract Data Type ) implemented using Python Lists
tags:
  - arrays
  - data-structures
  - fifo
  - lists
  - python
  - queue
author: S.Sunhaloo
date: 2026-03-07
status: Completed
---

## List of Contents

- [[#Create A Queue]]
- [[#Function / Method Related To Queue]]
	- [[#Data Insertion Method]]
		- [[#Enqueue Data Into Queue]]
	- [[#Data Removal Method]]
		- [[#Dequeue Data From Queue]]
	- [[#Miscellaneous Methods]]
		- [[#Peek The Top Value]]
		- [[#Length Of Queue]]
		- [[#Check If Queue Empty Or Not]]
- [[#Creation Of Queue And Usage]]

---

> [!NOTE]
> This is note is only going to show about the implementation of the **queue** *abstract datatype* using Python `list`s.
> 
> Please refer to online resources or even use Large Language Models to learn more about 'Queue'.

> [!INFO]
> Compared to my little *blunder* which I did in the '[[Python - Stacks ( List )]]' whereby I assumed that the datatype was going to be `int`eger data types ( *supposedly for simpler data manipulation* ).
> 
> > Well it did not made a **difference**!
> 
> Therefore, again, we all know that abstract data types like 'Stacks' and 'Queues' are implemented because of their *input-output* behaviour instead of the actual data type that they store.
> 
> > I am **not** going to repeat that silly mistake here!

> [!INFO] Resource(s)
> - [[Python - Lists]]
> - [[Python - Stacks ( List )]]

> [!WARNING] Hear Me Out!
> 
> What is the main difference between a 'Queue' and a 'Stack'?
> 
> > Its the way that they manipulate, especially in terms of *input-output*!
> 
> But if you take a closer look at both of them; most of their *functions* are practically the **same**
> 
> > Obviously with the **massive exception** of the `enqueue` / `push` and `dequeue` / `pop` methods!
> 
> What I am trying to say; its that most of things that we learned during the "*Stack*" notes will *pretty much* be the same here!
> 
> > Nevertheless, I will still continue to use integer numbers as example!

# Create A Queue

To create a *queue* in this case, we can simply create a Python `list`.

```python
# create an empty queue
empty_queue: list = []

# create a queue containing some elements
queue: list = ["Hello World", 67, 6.9, True, [1, 2, 3]]
```

---

# Function / Method Related To Queue

## Data Insertion Method

### Enqueue Data Into Queue

The main way to **add** ( *or "enqueue"* ) data into the queue, can be done by simply appending the new data to the list.

```python
# our queue variable
queue: list = []

# enqueue / append data into the queue
queue.append(1)
queue.append(2)
queue.append(3)
```

The above is the most simplest way to add data to a queue; i.e, using the `.append` method to *enqueue* data into the queue.

#### Simple Function To Enqueue Data ( User Input )

The following function below is a simple function that is going to allow the *user* to **add** an `amount` of data to the queue!

```python
# function to allow the user to enqueue a number of integer data into the queue
def enqueue_data(amount: int, queue: list):
    # iterate through the amount of data to add
    for i in range(amount):
        # ask the user to add data and append to "queue" / list
        user_data = input("Please Enter Data To Enqueue: ")

        queue.append(user_data)
```

## Data Removal Method

### Dequeue Data From Queue

Well, we can simply use the `.pop` method but this time with the index of `0` to **remove** the *oldest* element added to the queue.

```python
# our queue variable
queue: list = [1, 2, 3, 4, 5]

# dequeue / remove data from the queue
dequeued_data = queue.pop(0)
dequeued_data = queue.pop(0)
```

> [!TIP]
> Remember that the `.pop(0)` method will **return** the *element* that it has just removed from the `list`!

> [!WARNING] Index 0!
> Unlike the stack whereby we just did `.pop()` to remove the last element, in a queue we have to specifically tell Python that we want to remove the **first** element!
> 
> This is done by passing in the index of `0` to the `.pop()` method!

#### Simple Function To Dequeue Data ( User Input )

The following function below is a simple function that is going to allow the *user* to remove an `amount` of data from the queue!

```python
# function to allow the user to dequeue a number of integer data from the queue
def dequeue_data(amount: int, queue: list[int]):
    # iterate through the amount of data to remove
    for i in range(amount):
        # remove the "oldest" value added
        queue.pop(0)
```

> [!INFO] Improvements
> For the above function, you could:
> 
> - Create a list **before** the `for` loop and call that list `dequeued_elements`
> - Instead of simply calling `queue.pop(0)`; we instead get the *dequeued* value like so: `dequeued_element = queue.pop(0)`
> - Then use the `.append` function to **add** these `dequeued_element` to the `dequeued_elements` list
> - Hence, **return** the `dequeued_elements`
> 
> > Then for aesthetic purposes you add `-> list` at the "*function definition*"!
> 
> The reason as to why I am saying all of this is because I did **not** do something like `popped_element = stack.pop()` and `return popped_element` above!

---

## Before We Continue

I would like to say something about the `.append` / `.pop(0)` and `.insert(0, element)` / `.pop()` methods!

In the code above for **enqueue** and **dequeue**, we are adding new data at the **end** of the list and then using `.pop(0)` to **remove** the *first* value that was added to the list.

> Makes perfect sense!

In the above case, you should see that your list is going to look something like this if you **append** and then **pop**:

> Consider this little "*diagrammatical*" representation of the movement:
```console
# enqueueing / appending data to the list / queue
[]
[1]
[1, 2]
[1, 2, 3]

# dequeueing / removing data from the list / queue ( following FIFO )
[1, 2, 3]
[2, 3]
[3]
[]
```

> But what if I told you that we could use `.insert` and simply `.pop` ( *without passing any parameters* )?

So basically, if you **add** at index `0` using `.insert(0, element)`, then to **remove** you simply call `.pop()` ( *without passing any index as a parameter* ).

> Therefore, you are going to get this "*movement*":
```console
# enqueueing / inserting data to the list / queue
# this is done using the `.insert` method
[]
[1]
[2, 1]
[3, 2, 1]

# dequeueing / removing data from the list / queue ( following FIFO )
# this is done using the `.pop` method
[3, 2, 1]
[3, 2]
[3]
[]
```

> I much prefer this way over the former!

> [!INFO] Summary
> - If you are using `.append(element)` to **enqueue** elements into the list:
> 	- You need to use `.pop(0)` ( *pass index `0` as the argument* ) to **dequeue**
> - If you are using `.insert(0, element)` to **enqueue** elements into the list:
> 	- You need to use `.pop()` ( *without passing any parameter* ) to **dequeue**

---

## Miscellaneous Methods

### Peek The Top Value

This is just a one liner in Python because of the way that Python `list`'s **indexing** works!

> I am going to simply write the function itself

```python
# function to be able to see / peak the front value
def peek_data(queue: list):
    # simply return front / first value for queue / list
    return queue[0]
```

> [!WARNING] Wait, its `[0]` not `[-1]`!
> Remember for a **queue**, the "top" is actually the **front** of the queue ( the first element that was added! )
> 
> Therefore we access it using `[0]` not `[-1]` like we did with the stack!

### Length Of Queue

Well, you use the trusty `len` function provided by Python to find the **length** of the *list*!

```python
# find the length of the queue
print(f"Length Of Queue: {len(queue)}")
```

> I mean what else can I say?

### Check If Queue Empty Or Not

#### Using the Length Function

Using the `len`gth function, we can use this simple function below to check if the queue is empty or not.

```python
# function to check if the queue is empty or not ( using length function )
def empty_check(queue: list) -> bool:
    return len(queue) == 0
```

#### Using Boolean Type Casting

> Falsy and Truthy Value!

Here are are going to leverage **[[Python Language Basics#Type Cast | type casting]]** and '*truthy / falsy*' value to be able to check if the queue is empty or not!

```python
# function to check if the queue is empty or not ( using type casting )
def empty_check(queue: list) -> bool:
    return not bool(queue)
```

> My lecturer did this when she provided us some extremely simple and bare sample code!

> [!NOTE] We need the `not`!
> 
> If you go ahead an create an **empty** list called `x` and do something like this: `bool(x)`
> 
> This is actually going to return **`False`** as "*nothing*" / an **empty** list is 'Falsy' value! While doing the above with a **non-empty** list. You should see that we do get **`True`**, simply because "*something*" / a **non-empty** is a 'Truthy' value!
> 
> Therefore as we want to check if the queue is **empty** or **not**, We are going to have to *reverse* that statement use the `not` keyword found in Python!

> [!TIP] Which is **faster**?
> 
> The one using the `len`gth function is going to be **faster**!
> 
> This is due to the fact that we **don't** need to apply the `not` operator before it!
> 
> > Nevertheless, we are talking about nanoseconds here!

---

# Creation Of Queue And Usage

The code below is going to be show the *whole* usage and behaviour of using a Queue!

> [!NOTE]
> For simplicity sake and to *conform* to the "*unofficial-official*" standards...
> 
> I am simply going to use `.append` and `.pop(0)` to **enqueue** and **dequeue** elements!

```python
# function to allow the user to enqueue a number of elements into the queue
def enqueue_element(amount: int, queue: list):
    # iterate through the amount of data to add
    for i in range(amount):
        # ask the user to add data and append to "queue" / list
        user_data = input("Please Enter Data To Enqueue: ")

        queue.append(user_data)


# function to allow the user to dequeue a number of elements from the queue
def dequeue_element(amount: int, queue: list) -> list:
    # create a list to hold the dequeued elements
    dequeued_elements: list = []

    # iterate through the amount of data to remove
    for i in range(amount):
        # remove the "oldest" value added and get return value
        dequeued_element = queue.pop(0)

        # finally add the dequeued element to the `dequeued_elements` list
        dequeued_elements.append(dequeued_element)

    return dequeued_elements


# function to be able to see / peak the front value
def peek_element(queue: list[int]) -> int:
    # simply return front / first value for queue / list
    return queue[0]


# function to check if the queue is empty or not ( using length function )
def empty_check_length(queue: list) -> bool:
    return len(queue) == 0


# function to check if the queue is empty or not ( using type casting )
def empty_check_bool(queue: list) -> bool:
    return not bool(queue)


# our main function
def main():
    # intialise list for our queue
    queue: list = []

    # append / enqueue elements using the `.append` method
    queue.append(1)
    queue.append(2)
    queue.append(3)

    print(f"\nCurrent Data In Queue: {queue}", "\n" + "-" * 50)

    # ask the user to enter amount of elements to enqueue
    user_enqueue_amount = int(input("\nPlease Enter Amount Of Elements To Enqueue: "))

    # call the function to allow user to add elements to queue
    enqueue_element(user_enqueue_amount, queue)

    print(f"\nCurrent Data In Queue: {queue}", "\n" + "-" * 50)

    # remove / dequeue element using the `.pop(0)` method
    dequeued_element = queue.pop(0)

    print(f"\nDequeued Element = {dequeued_element}", "\n" + "-" * 50)

    print(f"\nCurrent Data In Queue: {queue}", "\n" + "-" * 50)

    # ask the user to enter amount of elements to dequeue
    user_dequeue_amount = int(input("\nPlease Enter Amount Of Elements To Dequeue: "))

    # call the function to allow user to remove elements from queue
    dequeue_element(user_dequeue_amount, queue)

    print(f"\nCurrent Data In Queue: {queue}", "\n" + "-" * 50)

    # peek / take a look at the front value
    front_element = peek_element(queue)

    print(f"\nFront Element = {front_element}", "\n" + "-" * 50)

    # find the length of queue
    print(f"\nLength Of Queue: {len(queue)}", "\n" + "-" * 50)

    # check if the queue is empty ( length `empty_check` function )
    print(f"\nQueue Empty?: {empty_check_length(queue)}", "\n" + "-" * 50)

    # NOTE: delete all the data from the queue
    dequeue_element(len(queue), queue)

    # check if the queue is empty ( boolean `empty_check` function )
    print(f"\nQueue Empty?: {empty_check_length(queue)}", "\n" + "-" * 50)

    print(f"\nCurrent Data In Queue: {queue}", "\n" + "-" * 50)


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