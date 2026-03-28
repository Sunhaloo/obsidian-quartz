---
id: Python - Stacks ( List )
aliases: Stack ( Abstract Data Type ) implemented using Python Lists
tags:
  - arrays
  - data-structures
  - lifo
  - lists
  - python
  - stack
author: S.Sunhaloo
date: 2026-03-06
status: Completed
---

## List of Contents

- [[#Create A Stack]]
- [[#Function / Method Related To Stack]]
	- [[#Data Insertion Method]]
		- [[#Pushing Data Onto Stack]]
	- [[#Data Removal Method]]
		- [[#Popping Data From Stack]]
	- [[#Miscellaneous Methods]]
		- [[#Peek The Top Value]]
		- [[#Length Of Stack]]
		- [[#Check If Stack Empty Or Not]]
- [[#Creation Of Stack And Usage]]

---

> [!NOTE]
> This is note is only going to show about the implementation of the **stack** *abstract datatype* using Python `list`s.
> 
> Please refer to online resources or even use Large Language Models to learn more about 'Stack'.

> [!WARNING]
> In this learning session, I am going to *[assume](https://www.youtube.com/watch?v=5ksV4nnXOsQ)* that our stack are going to only hold `int`eger numbers!
> 
> > [!TIP] Abstract Data Types... Data Types!
> > As the word "*abstract*" tell you, it does **not** really care about what kind of data goes into the stack!
> > 
> > In reality, the stack does **not** really know what data its holding. The main objective of the stack is to provide the '**Last-In-First-Out**' behaviour!
> > 
> > Again, in this learning session, I am simply **assuming** that `stack: list[int]` which in *reality* should simply be `stack: list`!!!

> [!INFO] Resource(s)
> - [[Python - Lists]]

# Create A Stack

To create a *stack* in this case, we can simply create a Python `list`.

```python
# create an empty stack
empty_stack: list[int] = []

# create a stack containing some integer numbers
stack: list[int] = [1, 2, 3, 4, 5]
```

---

# Function / Method Related To Stack

## Data Insertion Method

### Pushing Data Onto Stack

The main way to **add** ( */ or "push"* ) data onto the stack, can be done by simply appending the new data to the list.

```python
# our stack variable
stack: list[int] = []

# push / append data onto the stack
stack.append(1)
stack.append(2)
stack.append(3)
```

The above is the most simplest way to add data to a stack; i.e, using the `.append` method to *push* data onto the stack.

#### Simple Function To Push Data ( User Input )

The following function below is a simple function that is going to allow the *user* to **add** an `amount` of data to the stack!

```python
# function to allow the user to push a number of integer data onto the stack
def push_data(amount: int, stack: list[int]):
    # iterate through the amount of data to add
    for i in range(amount):
        # ask the user to add data and append to "stack" / list
        user_data = int(input("Please Enter Data To Push: "))

        stack.append(user_data)
```

## Data Removal Method

### Popping Data From Stack

Well, we can simply use the `.pop` method to **remove** the most *recent* element added to the stack.

```python
# our stack variable
stack: list[int] = [1, 2, 3, 4, 5]

# pop / remove data from the stack
popped_data = stack.pop()
popped_data = stack.pop()
```

> [!TIP]
> Remember that the `.pop` method will **return** the *element* that it has just removed from the `list`!

#### Simple Function To Pop Data ( User Input )

The following function below is a simple function that is going to allow the *user* to remove an `amount` of data from the stack!

```python
# function to allow the user to pop a number of integer data from the stack
def pop_data(amount: int, stack: list[int]):
    # iterate through the amount of data to remove
    for i in range(amount):
        # remove the most "recent" value added
        stack.pop()
```

> [!INFO] Improvements
> For the above function, you could:
> 
> - Create a list **before** the `for` loop and call that list `popped_elements`
> - Instead of simply calling `stack.pop()`; we instead get the *popped* value like so: `popped_element = stack.pop()`
> - Then use the `.append` function to **add** these `popped_element` to the `popped_elements` list
> - Hence, **return** the `popped_elements`
> 
> > Then for aesthetic purposes you add `-> list` at the "*function definition*"!
> 
> The reason as to why I am saying all of this is because I did **not** do something like `popped_element = stack.pop()` and `return popped_element` above!

## Miscellaneous Methods

### Peek The Top Value

This is just a one liner in Python because of the way that Python `list`'s **indexing** works!

> I am going to simply write the function itself

```python
# function to be able to see / peek the top value
def peek_data(stack: list[int]) -> int:
    # simply return top / last value for stack / list
    return stack[-1]
```

### Length Of Stack

Well, you use the trusty `len` function provided by Python to find the **length** of the *list*!

```python
# find the length of the stack
print(f"Length Of Stack: {len(stack)}")
```

> I mean what else can I say?

### Check If Stack Empty Or Not

#### Using the Length Function

Using the `len`gth function, we can use this simple function below to check if the stack is empty or not.

```python
# function to check if the stack is empty or not ( using length function )
def empty_check(stack: list[int]) -> bool:
    return len(stack) == 0
```

#### Using Boolean Type Casting

> Falsy and Truthy Value!

Here are are going to leverage **[[Python Language Basics#Type Cast | type casting]]** and '*truthy / falsy*' value to be able to check if the stack is empty or not!

```python
# function to check if the stack is empty or not ( using type casting )
def empty_check(stack: list[int]) -> bool:
    return not bool(stack)
```

> My lecturer did this when she provided us some extremely simple and bare sample code!

> [!NOTE] We need the `not`!
> 
> If you go ahead an create an **empty** list called `x` and do something like this: `bool(x)`
> 
> This is actually going to return **`False`** as "*nothing*" / an **empty** list is 'Falsy' value! While doing the above with a **non-emtpy** list. You should see that we do get **`True`**, simply because "*something*" / a **non-empty** is a 'Truthy' value!
> 
> Therefore as we want to check if the stack is **empty** or **not**, We are going to have to *reverse* that statement use the `not` keyword found in Python!

> [!TIP] Which is **faster**?
> 
> The one using the `len`gth function is going to be **faster**!
> 
> This is due to the fact that we **don't** need to apply the `not` operator before it!
> 
> > Nevertheless, we are talking about nanoseconds here!

---

# Creation Of Stack And Usage

The code below is going to be show the *whole* usage and behaviour of using a Stack!

> [!NOTE]
> In this specific case, I am **not** assuming that my stack is only going to contain `int`eger data types!

```python
# function to allow the user to push a number of elements onto the stack
def push_element(amount: int, stack: list):
    # iterate through the amount of data to add
    for i in range(amount):
        # ask the user to add data and append to "stack" / list
        user_data = input("Please Enter Data To Push: ")

        stack.append(user_data)


# function to allow the user to pop a number of elements from the stack
def pop_element(amount: int, stack: list) -> list:
    # create a list of hold the popped elements
    popped_elements: list = []

    # iterate through the amount of data to remove
    for i in range(amount):
        # remove the most "recent" value added and get return value
        popped_element = stack.pop()

        # finally add the popped element to the `popped_elements` list
        popped_elements.append(popped_element)

    return popped_elements


# function to be able to see / peak the top value
def peek_element(stack: list[int]) -> int:
    # simply return top / last value for stack / list
    return stack[-1]


# function to check if the stack is empty or not ( using length function )
def empty_check_length(stack: list) -> bool:
    return len(stack) == 0


# function to check if the stack is empty or not ( using type casting )
def empty_check_bool(stack: list) -> bool:
    return not bool(stack)


# our main function
def main():
    # intialise list for our stack
    stack: list = []

    # append / push elements using the `.append` method
    stack.append(1)
    stack.append(2)
    stack.append(3)

    print(f"\nCurrent Data In Stack: {stack}", "\n" + "-" * 50)

    # ask the user to enter amount of elements to push
    user_push_amount = int(input("\nPlease Enter Amount Of Elements To Push: "))

    # call the function to allow user to add elements to stack
    push_element(user_push_amount, stack)

    print(f"\nCurrent Data In Stack: {stack}", "\n" + "-" * 50)

    # remove / pop element using the `.pop` method
    popped_element = stack.pop()

    print(f"\nPopped Element = {popped_element}", "\n" + "-" * 50)

    print(f"\nCurrent Data In Stack: {stack}", "\n" + "-" * 50)

    # ask the user to enter amount of elements to pop
    user_pop_amount = int(input("\nPlease Enter Amount Of Elements To Pop: "))

    # call the function to allow user to add elements to stack
    pop_element(user_pop_amount, stack)

    print(f"\nCurrent Data In Stack: {stack}", "\n" + "-" * 50)

    # peek / take a look at the top value
    top_element = peek_element(stack)

    print(f"\nTop Element = {top_element}", "\n" + "-" * 50)

    # find the length of stack
    print(f"\nLength Of Stack: {len(stack)}", "\n" + "-" * 50)

    # check if the stack is empty ( length `check_emtpy` function )
    print(f"\nStack Empty?: {empty_check_length(stack)}", "\n" + "-" * 50)

    # NOTE: delete all the data from the stack
    pop_element(len(stack), stack)

    # check if the stack is empty ( boolean `check_emtpy` function )
    print(f"\nStack Empty?: {empty_check_length(stack)}", "\n" + "-" * 50)

    print(f"\nCurrent Data In Stack: {stack}", "\n" + "-" * 50)


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