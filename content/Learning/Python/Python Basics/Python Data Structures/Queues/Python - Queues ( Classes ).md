---
id: Python - Queues ( Classes )
aliases: Queue ( Abstract Data Type ) implemented using Python Classes
tags:
  - arrays
  - data-structures
  - fifo
  - lists
  - oop
  - python
  - queue
author: S.Sunhaloo
date: 2026-03-07
status: Completed
---

## List of Contents

- [[#Creation Of Class Queue]]
- [[#Function / Method Related To Queue]]
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

> [!WARNING]
> Please do check the '[[Python - Queues ( List )]]' **first**!
> 
> This is because I wrote the above mentioned file **before** I wrote this one!
> 
> The reason as to why, I am telling you that you need to read the above note is because we are just going to *convert* those functions into their **classes** counterparts.

> [!INFO]
> Additionally, compared to the above note, I am **not** going to assume here.
> 
> I am just going to allow all types of data to go into the "*class*" ( *which basically initialises a `list`*! )

---

> [!NOTE]
> This note is going to be a fuss around, just going to show you the code!
> 
> Again, for more information; please do refer to the '[[Python - Queues ( List )]]' note!

# Creation Of Class Queue

```python
# our queue class
class Queue:
    # our constructor method
    def __init__(self) -> None:
        # initialise the actual list for our queue
        self.queue: list = []
```

- Therefore to create some Queues, we can simply create our objects of class `Queue`:

```python
# our main function
def main():
    # create our first Queue
    queue: Queue = Queue()

    # create a second queue
    second_queue: Queue = Queue()


if __name__ == "__main__":
    main()
```

> I mean pretty self-explanatory!

---

# Function / Method Related To Queue

## Data Insertion Method

### Enqueue Data Onto Queue

```python
# method that will be able to add / enqueue elements into queue
def enqueue(self, element):
	self.queue.append(element)
```

## Data Removal Method

### Dequeue Data From Queue

> [!NOTE]
> Given that the following code uses the function to check if the queue is empty or not.
> 
> Please do refer to the heading: '[[#Check If Queue Empty Or Not]]' to see how we coded the `check_empty` method!

```python
# method that will be able to remove / dequeue elements from queue
def dequeue(self):
	# check if the queue is already empty or not
	if self.check_empty_len():
		raise IndexError("\n\tError: Queue Empty ==> Cannot Remove / Dequeue Data!!!\n")

	return self.queue.pop(0)
```

## Miscellaneous Methods

### Peek The Front Value

```python
# method to be able to see / peek the front value
def peek(self):
	# check if the queue is already empty or not
	if self.check_empty_len():
		raise IndexError("\n\tError: Queue Empty!!!\n")

	return self.queue[0]
```

### Length Of Queue

```python
# ( dunder ) method to find the length of "Queue"
def __len__(self) -> int:
	return len(self.queue)
```

> Simply use the `len` function with the `Queue` class!

### Check If Queue Empty Or Not

#### Using Length Function

```python
# method to check if the queue is empty or not ( length implementation )
def check_empty(self) -> bool:
	return len(self.queue) == 0
```

#### Using Boolean Type Casting

```python
# method to check if the queue is empty or not ( type-cast implementation )
def check_empty_bool(self) -> bool:
	return not bool(self.queue)
```

### Display / Print The Queue

```python
# ( dunder ) method to display / print the "Queue"
def __repr__(self) -> str:
	# if the linked list is empty
	if self.check_empty_len():
		return "\n\t== Queue Is Empty!!! ==\n"

	# initialise a temporary list ==> linked list is not empty
	temp: list = []

	# iterate through every element
	for element in self.queue:
		temp.append(str(element))

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
# import the randint funtion
from random import randint


# our queue class
class Queue:
    # our constructor method
    def __init__(self) -> None:
        # initialise the actual list for our queue
        self.queue: list = []

    # method to check if the queue is empty or not ( length implementation )
    def check_empty_len(self) -> bool:
        return len(self.queue) == 0

    # method to check if the queue is empty or not ( type-cast implementation )
    def check_empty_bool(self) -> bool:
        return not bool(self.queue)

    # method that will be able to add / enqueue elements into queue
    def enqueue(self, element):
        self.queue.append(element)

    # method that will be able to remove / dequeue elements from queue
    def dequeue(self):
        # check if the queue is already empty or not
        if self.check_empty_len():
            raise IndexError(
                "\n\tError: Queue Empty ==> Cannot Remove / Dequeue Data!!!\n"
            )

        return self.queue.pop(0)

    # method to be able to see / peek the front value
    def peek(self):
        # check if the queue is already empty or not
        if self.check_empty_len():
            raise IndexError("\n\tError: Queue Empty!!!\n")

        return self.queue[0]

    # ( dunder ) method to find the length of "Queue"
    def __len__(self) -> int:
        return len(self.queue)

	# ( dunder ) method to display / print the "Queue"
	def __repr__(self) -> str:
		# if the linked list is empty
		if self.check_empty_len():
			return "\n\t== Queue Is Empty!!! ==\n"
	
		# initialise a temporary list ==> linked list is not empty
		temp: list = []
	
		# iterate through every element
		for element in self.queue:
			temp.append(str(element))
	
		return "[" + ", ".join(temp) + "]"


# our main function
def main():
    # create our first Queue
    queue: Queue = Queue()

    # check if the queue is empty ( using the length implementation )
    print(f"\nQueue Empty? {queue.check_empty_len()}", "\n" + "-" * 50)

    # find the length of queue
    print(f"\nLength Of Queue: {len(queue)}", "\n" + "-" * 50, "\n")

    # add data to the queue
    queue.enqueue(1)
    queue.enqueue(2)
    queue.enqueue(3)

    # add / enqueue data onto the queue and display queue each time
    for i in range(3):
        queue.enqueue(randint(0, 9))

        print(queue)

    print("\n" + "-" * 50)

    # find the length of queue
    print(f"\nLength Of Queue: {len(queue)}", "\n" + "-" * 50, "\n")

    # remove / dequeue data from the queue and display queue each time
    for i in range(3):
        dequeued_element = queue.dequeue()

        print(queue)

        print(f"\n  -- Dequeued Element: {dequeued_element} --\n")

    print("-" * 50)

    # find the length of queue
    print(f"\nLength Of Queue: {len(queue)}", "\n" + "-" * 50)

    # see / peek at the front value found
    print(f"\nFront Element = {queue.peek()}", "\n" + "-" * 50)

    # check if the queue is empty ( using the boolean implementation )
    print(f"\nQueue Empty? {queue.check_empty_bool()}", "\n" + "-" * 50)

    print("\n== Final Queue Representation ==\n")

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
