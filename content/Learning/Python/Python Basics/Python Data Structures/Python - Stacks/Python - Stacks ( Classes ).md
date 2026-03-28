---
id: Python - Stacks ( Classes )
aliases: Stack ( Abstract Data Type ) implemented using Python Classes
tags:
  - arrays
  - data-structures
  - lifo
  - lists
  - oop
  - python
  - stack
author: S.Sunhaloo
date: 2026-03-06
status: Completed
---

## List of Contents

- [[#Creation Of Class Stack]]
- [[#Function / Method Related To Stack]]
	- [[#Data Insertion Method]]
		- [[#Pushing Data Onto Stack]]
	- [[#Data Removal Method]]
		- [[#Popping Data From Stack]]
	- [[#Miscellaneous Methods]]
		- [[#Peek The Top Value]]
		- [[#Length Of Stack]]
		- [[#Check If Stack Empty Or Not]]
		- [[#Display / Print The Stack]]
- [[#Creation Of Stack and Usage]]

---

> [!WARNING]
> Please do check the '[[Python - Stacks ( List )]]' **first**!
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
> Again, for more information; please do refer to the '[[Python - Stacks ( List )]]' note!

# Creation Of Class Stack

```python
# our stack class
class Stack:
    # our constructor method
    def __init__(self) -> None:
        # initialise the actual list for our stack
        self.stack: list = []
```

- Therefore to create some Stacks, we can simply create our objects of class `Stack`:

```python
# our main function
def main():
    # create our first Stack
    stack: Stack = Stack()

    # create a second stack
    second_stack: Stack = Stack()


if __name__ == "__main__":
    main()
```

> I mean pretty self-explanatory!

---

# Function / Method Related To Stack

## Data Insertion Method

### Pushing Data Onto Stack

```python
# method that will be able to add / push elements onto stack
def push(self, element):
	self.stack.append(element)
```

## Data Removal Method

### Popping Data From Stack

> [!NOTE]
> Given that the following code uses the function to check if the stack is empty or not.
> 
> Please do refer to the heading: '[[#Check If Stack Empty Or Not]]' to see how we coded the `check_empty` method!

```python
# method that will be able to remove / pop elements onto stack
def pop(self):
	# check if the stack is already empty or not
	if self.check_empty_len():
		raise IndexError("\n\tError: Stack Empty ==> Cannot Remove / Pop Data!!!\n")

	return self.stack.pop()
```

## Miscellaneous Methods

### Peek The Top Value

```python
# method to be able to see / peak the top value
def peek(self):
	# check if the stack is already empty or not
	if self.check_empty_len():
		raise IndexError("\n\tError: Stack Empty!!!\n")

	return self.stack[-1]
```

### Length Of Stack

```python
# ( dunder ) method to find the length of "Stack"
def __len__(self) -> int:
	return len(self.stack)
```

> Simply use the `len` function with the `Stack` class!

### Check If Stack Empty Or Not

#### Using Length Function

```python
# method to check if the stack is empty or not ( length implementation )
def check_empty(self) -> bool:
	return len(self.stack) == 0
```

#### Using Boolean Type Casting

```python
# method to check if the stack is empty or not ( type-cast implementation )
def check_empty_bool(self) -> bool:
	return not bool(self.stack)
```

### Display / Print The Stack

```python
# ( dunder ) method to display / print the "Stack"
def __repr__(self) -> str:
	if self.check_empty_len():
		return "\n\t== Stack Is Empty!!! ==\n"

	# initialise list that is going to hold all the strings
	lines = ["\n\t---------"]

	# iterate through every element in reversed ( so as to show the stack )
	for element in reversed(self.stack):
		lines.append(f"\t|   {element}   |")
		lines.append("\t---------")

	return "\n".join(lines)
```

---

# Creation Of Stack and Usage

Here is simple, example of what we get when we combine all of these functions above.

> [!INFO]
> I hard-coded the input and deletion; but you can easily use a `for` loop to create another *simple* function if you want to allow for user input!
> 
> > Compared to '[[Python - Stacks ( List )]]'; you basically use *our* methods!

> [!WARNING]
> This stack implementation will work with **all** data types!
> 
> I just chose to use `int`eger numbers for this one...

```python
# import the randint funtion
from random import randint


# our stack class
class Stack:
    # our constructor method
    def __init__(self) -> None:
        # initialise the actual list for our stack
        self.stack: list = []

    # method to check if the stack is empty or not ( length implementation )
    def check_empty_len(self) -> bool:
        return len(self.stack) == 0

    # method to check if the stack is empty or not ( type-cast implementation )
    def check_empty_bool(self) -> bool:
        return not bool(self.stack)

    # method that will be able to add / push elements onto stack
    def push(self, element):
        self.stack.append(element)

    # method that will be able to remove / pop elements onto stack
    def pop(self):
        # check if the stack is already empty or not
        if self.check_empty_len():
            raise IndexError("\n\tError: Stack Empty ==> Cannot Remove / Pop Data!!!\n")

        return self.stack.pop()

    # method to be able to see / peak the top value
    def peek(self):
        # check if the stack is already empty or not
        if self.check_empty_len():
            raise IndexError("\n\tError: Stack Empty!!!\n")

        return self.stack[-1]

    # ( dunder ) method to find the length of "Stack"
    def __len__(self) -> int:
        return len(self.stack)

    # ( dunder ) method to display / print the "Stack"
    def __repr__(self) -> str:
        if self.check_empty_len():
            return "\n\t== Stack Is Empty!!! ==\n"

        # initialise list that is going to hold all the strings
        lines = ["\n\t---------"]

        # iterate through every element in reversed ( so as to show the stack )
        for element in reversed(self.stack):
            lines.append(f"\t|   {element}   |")
            lines.append("\t---------")

        return "\n".join(lines)


# our main function
def main():
    # create our first Stack
    stack: Stack = Stack()

    # check if the stack is empty ( using the length implementation )
    print(f"\nStack Empty? {stack.check_empty_len()}", "\n" + "-" * 50)

    # find the length of stack
    print(f"\nLength Of Stack: {len(stack)}", "\n" + "-" * 50)

    # add data to the stack
    stack.push(1)
    stack.push(2)
    stack.push(3)

    # add / push data onto the stack and display stack each time
    for i in range(3):
        stack.push(randint(0, 9))

        print(stack)

    print("\n" + "-" * 50, "\n")

    # find the length of stack
    print(f"\nLength Of Stack: {len(stack)}", "\n" + "-" * 50)

    # add / push data onto the stack and display stack each time
    for i in range(3):
        popped_element = stack.pop()

        print(stack)

        print(f"\n  -- Popped Element: {popped_element} --\n")

    print("\n" + "-" * 50, "\n")

    # find the length of stack
    print(f"\nLength Of Stack: {len(stack)}", "\n" + "-" * 50)

    # see / peak at the top value found
    print(f"\nTop Element = {stack.peek()}", "\n" + "-" * 50)

    # check if the stack is empty ( using the boolean implementation )
    print(f"\nStack Empty? {stack.check_empty_bool()}", "\n" + "-" * 50)

    print("\n== Final Stack Representation ==\n")

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