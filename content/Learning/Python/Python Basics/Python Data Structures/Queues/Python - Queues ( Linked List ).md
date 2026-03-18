---
id: Python - Queues ( Linked List )
aliases: Queue ( Abstract Data Type ) implemented using Linked List with Classes
tags:
  - data-structures
  - fifo
  - oop
  - python
  - queue
author: S.Sunhaloo
date: 2026-03-07
status: Completed
---

## List Of Contents

- [[#Creation Of Class Node]]
- [[#Creation Of Queue Class]]
- [[#Function / Method Related To Queue ( Linked List )]]
	- [[#Data Insertion Method]]
		- [[#Enqueue Data Onto Queue]]
	- [[#Data Removal Method]]
		- [[#Dequeue Data From Queue]]
	- [[#Miscellaneous Methods]]
		- [[#Peek The Front Value]]
		- [[#Length Of Queue]]
		- [[#Check If Queue Empty Or Not]]
		- [[#Display / Print The Queue]]
- [[#Creation Of Queue and Usage]]

---

> [!INFO] Resource(s)
> - [[Python - Singly Linked Lists]]
> - Neural Nine Video: https://www.youtube.com/watch?v=9FvlBQQ_gfY

> [!INFO]
> To be honest, there is nothing much special here.
> 
> We are going to be basically coding a *minimal* singly linked list whereby we are just going to be appending and removing values at the end of the linked list.
> 
> Therefore, if you already understand singly linked list. This should be easy for you!

> [!WARNING] Two Pointers!
> Implementing a queue using *linked list* is going to require **two** pointers!
> 
> Whereby the `front` pointer is going to keep track of the **first** element that got *into* the queue.
> 
> And the `rear` pointer is going to keep track of the **last** element that that *into* the queue.

# Creation Of Class Node

Below you are going to find the *class* implementation of a **node**.

> This is literally a 'copy-paste' of the node class from our [[Python - Singly Linked Lists#Creation Of Class Node | linked list]] note!

```python
# our linked list nodes
class Node:
    # our constructor method
    def __init__(self, data) -> None:
        # the actual node data / element inside node
        # INFO: in this case, head cannot start without any data
        self.data = data

        # class variable to "point" to the next node
        self.next = None
```

# Creation Of Queue Class

```python
# our queue class to allow for the 'FIFO' behaviour
class Queue:
    # our constructor
    def __init__(self) -> None:
        # our "front" pointer ( first in )
        self.front = None

        # our "rear" pointer ( last in )
        self.rear = None

        # INFO: I plan to check for the length of the queue a lot of times
        self.size = 0
```

> [!INFO]
> As you can see I have also added the `self.size` attribute to the `Queue` class!
> 
> This is because I plan **check** for the *length* / *size* of the queue a **lot** of times. Therefore, instead of using the `len` function whereby we iterate through the **whole** linked list... I think keeping a single attribute for this is better!

---

# Function / Method Related To Queue ( Linked List )

## Data Insertion Method

> [!NOTE]
> Given that the following code uses the function to check if the queue is empty or not.
> 
> Please do refer to the heading: '[[#Check If Queue Empty Or Not]]' to see how we coded the `check_empty` method!

We are going to add / *enqueue* a new element onto the *linked list* queue by:

- Creating a new node containing the data
- Then, we check if the queue is **empty**
	- If the queue **is** empty: both `front` and `rear` point to the new node
	- If the queue is **not** empty: link the current `rear` to the new node, then update `rear` to the new node

### Enqueue Data Onto Queue

```python
# method to add / enqueue element onto the queue
def enqueue(self, item):
	# create the new node
	new_node = Node(item)

	# if the queue is empty
	if self.rear is None:
		# both front and rear point to the new node
		self.front = new_node
		self.rear = new_node
	else:
		# link the current rear to the new node
		self.rear.next = new_node

		# make the new node the rear
		self.rear = new_node

	# INFO: don't forget to increment the size
	self.size += 1
```

## Data Removal Method

We are going to remove / *dequeue* an element from the *linked list* queue by:

- First of all, we check if the linked list **is** *empty*
	- If the linked **is** empty; we simply `raise` an `IndexError` 
- Else, we take the **element** found at the `front` pointer and **place** it into *variable*
- Then, we simply make the `front` pointer *point* to its **neighbour**
- If the queue becomes empty after removal, we also set `rear` to `None`
- Finally, we simply need to `return` the **dequeued element**

### Dequeue Data From Queue

```python
# method to remove / dequeue element from the queue
def dequeue(self):
	# if the linked list is empty
	if self.front is None:
		raise IndexError("\n\tError: Queue Empty ==> Cannot Remove / Dequeue Data!!!\n")

	# if the queue is not empty
	dequeued_element = self.front.data

	# move the front pointer to the next element
	self.front = self.front.next

	# if the queue becomes empty after removal
	if self.front is None:
		self.rear = None

	# INFO: don't forget to decrement the size
	self.size -= 1

	# finally return the dequeued element
	return dequeued_element
```

## Miscellaneous Methods

### Peek The Front Value

> I think that this code is pretty self-explanatory

```python
# method to be able to see / peek the front value
def peek(self):
	# if the queue is empty
	if self.front is None:
		raise ValueError("\n\tError: Queue Empty!!!\n")

	# if the queue is not empty
	return self.front.data
```

### Length Of Queue

#### Simply Use The `size` Attribute

```python
# find the length of the queue ( using the `size` attribute )
print(f"\nLength Of Queue: {queue.size}", "\n" + "-" * 50)
```

#### Iterate Through The Whole Linked List

```python
# ( dunder ) method to find the length of the queue through iteration
def __len__(self) -> int:
	# if the linked list is empty
	if self.front is None:
		return 0

	# if the linked list is not empty ==> create a simple counter
	element_count: int = 0

	# create a simple pointer to iterate through the linked list
	current_ptr = self.front

	# iterate through the actual value until no more
	while current_ptr is not None:
		# increment the counter each time we encounter an element
		element_count += 1

		# move the pointer to its neighbour
		current_ptr = current_ptr.next

	return element_count
```

> [!NOTE]
> In this case, I do recommend that you simply just access the `size` attribute as its much more **efficient** and **faster** ( _O(1) **instead** of O(n)_ )!
> 
> > We simply don't have to iterate through the whole linked list ( *when using the `size` attribute* )!

### Check If Queue Empty Or Not

Here, is simple, as we can just use the `front` pointer to check if its `None` or not!

```python
# method to check if the queue is empty or not
def check_empty(self):
	return self.front is None
```

### Display / Print The Queue

In this case, I simply wanted to display it like a `list` would have been displayed through the `print` function.

> Nothing fancy here of actually showing the queue like in [[Python - Queues ( Classes )#Display / Print The Queue | Python - Queues ( Classes )]]

```python
# ( dunder ) method to display / print the "Queue"
def __repr__(self) -> str:
	# if the linked list is empty
	if self.front is None:
		return "\n\t== Queue Is Empty!!! ==\n"

	# initialise a temporary list ==> linked list is not empty
	temp: list = []

	# create a simple pointer to iterate through the linked list
	current_ptr = self.front

	# iterate through the actual value until no more
	while current_ptr is not None:
		# add the current element found at `current_ptr` to the list
		temp.append(str(current_ptr.data))

		# move the pointer to its neighbour
		current_ptr = current_ptr.next

	return "[" + ", ".join(temp) + "]"
```

---

# Creation Of Queue and Usage

Here is simple, example of what we get when we combine all of these functions above

> [!INFO]
> I hard-coded the input and deletion; but you can easily use a `for` loop to create another *simple* function if you want to allow for user input!
> 
> > Compared to '[[Python - Queues ( List )]]'; you basically use *our* methods!

> [!WARNING]
> This queue implementation will work with **all** data types!
> 
> I just choose to use `int`eger numbers for this one...

> [!NOTE]
> For simplicity sake and to *conform* to the "*unofficial-official*" standards...
> 
> I am simply going to use `.append` and `.pop(0)` to **enqueue** and **dequeue** elements!

```python
# our linked list nodes
class Node:
    # our constructor method
    def __init__(self, data) -> None:
        # the actual node data / element inside node
        self.data = data

        # class variable to "point" to the next node
        self.next = None


# our queue class to allow for the 'FIFO' behaviour
class Queue:
    # our constructor
    def __init__(self) -> None:
        # our "front" pointer (first in)
        self.front = None

        # our "rear" pointer (last in)
        self.rear = None

        # INFO: I plan to check for the length of the queue a lot of times
        self.size = 0

    # method to check if the queue is empty or not
    def check_empty(self):
        return self.front is None

    # method to add / enqueue element onto the queue
    def enqueue(self, item):
        # create the new node
        new_node = Node(item)

        # if the queue is empty
        if self.rear is None:
            # both front and rear point to the new node
            self.front = new_node
            self.rear = new_node
        else:
            # link the current rear to the new node
            self.rear.next = new_node

            # make the new node the rear
            self.rear = new_node

        # INFO: don't forget to increment the size
        self.size += 1

    # method to remove / dequeue element from the queue
    def dequeue(self):
        # if the linked list is empty
        if self.front is None:
            raise IndexError("\n\tError: Queue Empty ==> Cannot Remove / Dequeue Data!!!\n")

        # if the queue is not empty
        dequeued_element = self.front.data

        # move the front pointer to the next element
        self.front = self.front.next

        # if the queue becomes empty after removal
        if self.front is None:
            self.rear = None

        # INFO: don't forget to decrement the size
        self.size -= 1

        # finally return the dequeued element
        return dequeued_element

    # method to be able to see / peek the front value
    def peek(self):
        # if the queue is empty
        if self.front is None:
            raise ValueError("\n\tError: Queue Empty!!!\n")

        # if the queue is not empty
        return self.front.data

    # ( dunder ) method to find the length of the queue through iteration
    def __len__(self) -> int:
        # if the linked list is empty
        if self.front is None:
            return 0

        # if the linked list is not empty ==> create a simple counter
        element_count: int = 0

        # create a simple pointer to iterate through the linked list
        current_ptr = self.front

        # iterate through the actual value until no more
        while current_ptr is not None:
            # increment the counter each time we encounter an element
            element_count += 1

            # move the pointer to its neighbour
            current_ptr = current_ptr.next

        return element_count

    # ( dunder ) method to display / print the "Queue"
    def __repr__(self) -> str:
        # if the linked list is empty
        if self.front is None:
            return "\n\t== Queue Is Empty!!! ==\n"

        # initialise a temporary list ==> linked list is not empty
        temp: list = []

        # create a simple pointer to iterate through the linked list
        current_ptr = self.front

        # iterate through the actual value until no more
        while current_ptr is not None:
            # add the current element found at `current_ptr` to the list
            temp.append(str(current_ptr.data))

            # move the pointer to its neighbour
            current_ptr = current_ptr.next

        return "[" + ", ".join(temp) + "]"


# our main function
def main():
    # create our queue
    queue: Queue = Queue()

    # check if the queue is empty
    print(f"\nQueue Empty?: {queue.check_empty()}", "\n" + "-" * 50)

    # find the length of the queue ( using the `size` attribute )
    print(f"\nSize Of Queue: {queue.size}", "\n" + "-" * 50)

    # enqueue data onto the queue
    queue.enqueue(1)
    queue.enqueue(2)
    queue.enqueue(3)

    print("\nCurrent Contents Of Queue: ", end="")

    # display the queue using `print` ( because of `__repr__` )
    print(queue)

    print("-" * 50)

    # find the length of the queue ( using the `len` function )
    print(f"\nSize Of Queue: {len(queue)}", "\n" + "-" * 50)

    # peek at the front value
    print(f"\nFront Element = {queue.peek()}", "\n" + "-" * 50)

    # dequeue data from the queue
    dequeued_element = queue.dequeue()
    print(f"\nDequeued Element = {dequeued_element}", "\n" + "-" * 50)

    print("\nCurrent Contents Of Queue: ", end="")

    # display the queue using `print` ( because of `__repr__` )
    print(queue)

    print("-" * 50)

    # find the length of the queue ( using the `len` function )
    print(f"\nSize Of Queue: {len(queue)}", "\n" + "-" * 50)

    # dequeue all remaining elements
    while not queue.check_empty():
        queue.dequeue()

    # check if the queue is empty
    print(f"\nQueue Empty?: {queue.check_empty()}", "\n" + "-" * 50)

    # find the length of the queue ( using the `size` attribute )
    print(f"\nSize Of Queue: {queue.size}", "\n" + "-" * 50)

    # display the queue using `print` ( because of `__repr__` )
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