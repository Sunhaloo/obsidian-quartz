---
id: Python - Stacks ( Linked List )
aliases: Stack ( Abstract Data Type ) implemented using Linked List with Classes
tags:
  - data-structures
  - lifo
  - oop
  - python
  - stack
author: S.Sunhaloo
date: 2026-03-07
status: Completed
---

## List of Contents

- [[#Creation Of Class Node]]
- [[#Creation Of Stack Class]]
- [[#Function / Method Related To Stack ( Linked List )]]
	- [[#Data Insertion Method]]
	- [[#Data Removal Method]]
	- [[#Miscellaneous Methods]]
		- [[#Peek The Top Value]]
		- [[#Length Of Stack]]
		- [[#Check If Stack Empty Or Not]]
		- [[#Display / Print The Stack]]
- [[#Creation Of Stack and Usage]]

---

> [!INFO] Resource(s)
> - [[Python - Singly Linked Lists]]
> - Neural Nine Video: https://www.youtube.com/watch?v=RX3SB6pyXao

> [!INFO]
> To be honest, there is nothing much special here.
> 
> We are going to be basically coding a *minimal* singly linked list whereby we are just going to be appending and removing values at the end of the linked list.
> 
> Therefore, if you already understand singly linked list. This should be easy for you!

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

# Creation Of Stack Class

```python
# our stack class to allow for the 'LIFO' behaviour
class Stack:
    # our constructor
    def __init__(self) -> None:
        # our "head" in this case
        self.top = None

        # INFO: I plan to check for the length of the stack a lot of times
        self.size = 0
```

> [!INFO]
> As you can see I have also added the `self.size` attribute to the `Stack` class!
> 
> This is because simply because I plan **check** for the *length* / *size* stack  a **lot** of times. Therefore, instead of using the `len` function whereby we iterate through the **whole** linked list... I think keeping a single attribute for this is better!

---

# Function / Method Related To Stack ( Linked List )

## Data Insertion Method

> [!NOTE]
> Given that the following code uses the function to check if the stack is empty or not.
> 
> Please do refer to the heading: '[[#Check If Stack Empty Or Not]]' to see how we coded the `check_empty` method!

We are going to add / *push* a new element onto the *linked list* stack by:

- Creating a new node containing the data
- Then, new node **neighbour** should be the `top` pointer ( *as it holds the actual linked list* )
- Make the `top` **pointer** *become* the new node

```python
# method to add / push element onto the stack
def push(self, item):
	# create the new node
	new_node = Node(item)

	# link the new node to the linked list ( the `top` pointer holds last item )
	new_node.next = self.top

	# make the new node the `top` node
	self.top = new_node

	# INFO: don't forget to increment the size
	self.size += 1
```

## Data Removal Method

We are going to add / *push* a new element onto the *linked list* stack by:

- First of all, we check if the linked list **is** *empty*
	- If the linked **is** empty; we simply `raise` an `IndexError` 
- Else, we take the **element** found at the `top` pointer and **place** it into *variable*
- Then, we simply make the `top` pointer *points* to its **neighbour**
- Finally, we simply need to `return` the **popped element** like the actual `pop` function

```python
# method to remove / pop element from the stack
def pop(self):
	# if the linked list is empty
	if self.top is None:
		raise IndexError("\n\tError: Stack Empty ==> Cannot Remove / Pop Data!!!\n")

	# if the linked is not empty
	popped_element = self.top.data

	# move the current position of the `top` pointer to the new "top" element
	self.top = self.top.next

	# INFO: don't forget to decrement the size
	self.size -= 1

	# finally return the popped element
	return popped_element
```

## Miscellaneous Methods

### Peek The Top Value

> I think that this code is pretty self-explanatory

```python
# method to be able to see / peak the top value
def peek(self):
	# if the linked list is empty
	if self.top is None:
		raise ValueError("\n\tError: Stack Empty ==> Cannot Get Top Value!!!\n")

	# if the linked list is not empty
	return self.top.data
```

### Length Of Stack

#### Simply Use The `size` Attribute

```python
# find the length of the stack ( using the `size` attribute )
print(f"\nLength Of Stack: {stack.size}", "\n" + "-" * 50)
```

#### Iterate Through The Whole Linked List

```python
# ( dunder ) method to find the length of the stack through iteration
def __len__(self) -> int:
	# if the linked list is empty
	if self.top is None:
		return 0

	# if the linked lis is not empty ==> create a simple counter
	element_count: int = 0

	# create a simple pointer to iterate through the linked list
	current_ptr = self.top

	# iterate through the actual value until no more
	while current_ptr is not None:
		# increment the counter each time we encouter an element
		element_count += 1

		# move the pointer to its neighbour
		current_ptr = current_ptr.next

	return element_count
```

> [!NOTE]
> In this case, I do recommend that you simply just access the `size` attribute as its much more **efficient** and **faster** ( _O(1) **instead** of O(n)_ )!
> 
> > We simply don't have to iterate through the whole linked list ( *when using the `size` attribute* )!

### Check If Stack Empty Or Not

Here, is simple, as we can just use the `top` ( *or `head`* ) pointer to check if its `None` or not!

```python
# method to check if the stack is empty or not
def check_empty(self):
	return self.top is None
```

### Display / Print The Stack

In this case, I simply wanted to display it like a `list` would have been displayed through the `print` function.

> Nothing fancy here of actually showing the stack like in [[Python - Stacks ( Classes )#Display / Print The Stack | Python - Stacks ( Classes )]]

```python
# ( dunder ) method to display / print the "Stack"
def __repr__(self) -> str:
	# if the linked list is empty
	if self.top is None:
		return "\n\t== Stack Is Empty!!! ==\n"

	# initialise a temporary list ==> linked list is not empty
	temp: list = []

	# create a simple pointer to iterate through the linked list
	current_ptr = self.top

	# iterate through the actual value until no more
	while current_ptr is not None:
		# add the current element found at `current_ptr` to the list
		# NOTE: need to convert to `str`; because of `reversed` function
		temp.append(str(current_ptr.data))

		# move the pointer to its neighbour
		current_ptr = current_ptr.next

	return "[" + ", ".join(reversed(temp)) + "]"
```

---

# Creation Of Stack and Usage

Here is simple, example of what we get when we combine all of these functions above

> [!INFO]
> I hard-coded the input and deletion; but you can easily use a `for` loop to create another *simple* function if you want to allow for user input!
> 
> > Compared to '[[Python - Stacks ( List )]]'; you basically use *our* methods!

> [!WARNING]
> This stack implementation will work with **all** data types!
> 
> I just choose to use `int`eger numbers for this one...

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


# our stack class to allow for the 'LIFO' behaviour
class Stack:
    # our constructor
    def __init__(self) -> None:
        # our "head" in this case
        self.top = None

        # INFO: I plan to check for the length of the stack a lot of times
        self.size = 0

    # method to check if the stack is empty or not
    def check_empty(self):
        return self.top is None

    # method to add / push element onto the stack
    def push(self, item):
        # create the new node
        new_node = Node(item)

        # link the new node to the linked list ( the `top` pointer holds last item )
        new_node.next = self.top

        # make the new node the `top` node
        self.top = new_node

        # INFO: don't forget to increment the size
        self.size += 1

    # method to remove / pop element from the stack
    def pop(self):
        # if the linked list is empty
        if self.top is None:
            raise IndexError("\n\tError: Stack Empty ==> Cannot Remove / Pop Data!!!\n")

        # if the linked is not empty
        popped_element = self.top.data

        # move the current position of the `top` pointer to the new "top" element
        self.top = self.top.next

        # INFO: don't forget to decrement the size
        self.size -= 1

        # finally return the popped element
        return popped_element

    # method to be able to see / peak the top value
    def peek(self):
        # if the linked list is empty
        if self.top is None:
            raise ValueError("\n\tError: Stack Empty ==> Cannot Get Top Value!!!\n")

        # if the linked list is not empty
        return self.top.data

    # ( dunder ) method to find the length of the stack through iteration
    def __len__(self) -> int:
        # if the linked list is empty
        if self.top is None:
            return 0

        # if the linked lis is not empty ==> create a simple counter
        element_count: int = 0

        # create a simple pointer to iterate through the linked list
        current_ptr = self.top

        # iterate through the actual value until no more
        while current_ptr is not None:
            # increment the counter each time we encouter an element
            element_count += 1

            # move the pointer to its neighbour
            current_ptr = current_ptr.next

        return element_count

    # ( dunder ) method to display / print the "Stack"
    def __repr__(self) -> str:
        # if the linked list is empty
        if self.top is None:
            return "\n\t== Stack Is Empty!!! ==\n"

        # initialise a temporary list ==> linked list is not empty
        temp: list = []

        # create a simple pointer to iterate through the linked list
        current_ptr = self.top

        # iterate through the actual value until no more
        while current_ptr is not None:
            # add the current element found at `current_ptr` to the list
            # NOTE: need to convert to `str`; because of `reversed` function
            temp.append(str(current_ptr.data))

            # move the pointer to its neighbour
            current_ptr = current_ptr.next

        return "[" + ", ".join(reversed(temp)) + "]"


# our main function
def main():
    # create our stack
    stack: Stack = Stack()

    # check if the stack is empty
    print(f"\nStack Empty?: {stack.check_empty()}", "\n" + "-" * 50)

    # find the length of the stack ( using the `size` attribute )
    print(f"\nSize Of Stack: {stack.size}", "\n" + "-" * 50)

    # push data onto the stack
    stack.push(1)
    stack.push(2)
    stack.push(3)

    print("\nCurrent Contents Of Stack: ", end="")

    # display the stack using `print` ( because of `__repr__` )
    print(stack)

    print("-" * 50)

    # find the length of the stack ( using the `len` function )
    print(f"\nSize Of Stack: {len(stack)}", "\n" + "-" * 50)

    # peek at the top value
    print(f"\nTop Element = {stack.peek()}", "\n" + "-" * 50)

    # pop data from the stack
    popped_element = stack.pop()
    print(f"\nPopped Element = {popped_element}", "\n" + "-" * 50)

    print("\nCurrent Contents Of Stack: ", end="")

    # display the stack using `print` ( because of `__repr__` )
    print(stack)

    print("-" * 50)

    # find the length of the stack ( using the `len` function )
    print(f"\nSize Of Stack: {len(stack)}", "\n" + "-" * 50)

    # pop all remaining elements
    while not stack.check_empty():
        stack.pop()

    # check if the stack is empty
    print(f"\nStack Empty?: {stack.check_empty()}", "\n" + "-" * 50)

    # find the length of the stack ( using the `size` attribute )
    print(f"\nSize Of Stack: {stack.size}", "\n" + "-" * 50)

    # display the stack using `print` ( because of `__repr__` )
    print(stack)


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