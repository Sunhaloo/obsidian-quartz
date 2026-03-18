---
id: Python Language Basics
aliases: Python Language Basics
tags:
  - python
  - basics
author: S.Sunhaloo
date: 2024-11-05
status: Completed
---

## List of Contents

- [[#Requirements]]
- [[#Python Boiler Plate]]
- [[#Basic Data Types]]
- [[#Display Stuff On Screen]]
	- [[#Type Cast]]
- [[#User Inputs]]
- [[#Conditions]]
- [[#Loops]]
- [[#Functions]]
- [[#Exception Handling]]

---

> [!INFO] Official Documentation
> Website: https://docs.python.org/3/

# Requirements

- Python 3.10.0 or above $\uparrow$
- Code Editor of Choice

## Python Boiler Plate

```python
# our main function
def main():
    print("Hello World!")


# source the main function
if __name__ == '__main__':
    main()
```

> [!NOTE]
> Most people ( *in my country* ) will tell you that: "*Oh!, you don't need to put that... Just run the main function*".
> My response, "*Why do people online include it?*".
>
> Its main purpose is to distinguish between a file **directly** or **importing** a file as a *module*.
> In this case we are going to have:
>
> - Unintended Execution
> - Reusability and Modularity
> 	- File can be run as a standalone program or as a module
>
> > Basically, you are going to have control over how code blocks are executed.
> > You can either run them ( *code blocks* ) directly from that file or import that file as a **module**.

# Basic Data Types

```python
# single line comment

"""
This is a multi-line
comment. Very nice!
Useful for writing "documentation" for somethings
"""
```

```python
# initialisation of variables without 'type hinting' or 'type annotation'
num = 69
floating_num = 6.9
character_thingy = "A"
some_text = "Some Text Here"
true_false = False
complex_num = 1 + 2j

# multiple assingment ( languages like Go and Lua also supports this )
x = y = z = "What!"
lewis_hamilton, sebastien_vettel, max_verstappen = 44, 5, 33
```

```python
# initialisation of variables with 'type hinting' or 'type annotation'
num: int = 69
floating_num: float = 6.9
character_thingy: str = "A"
some_text: str = "Some Text Here"
true_false: bool = False
complex_num: complex = 1 + 2j
```

> [!WARNING]
> Even though you might think that, "*oh yes, we have added specifically what data type a variable can take*". Well think again!
>
> In Python, there are not declaration of variables... Meaning that we can totally do this: `num = 5.5`.
>
> From what I can understand, if you are using 'Type Hinting' in Python, its for your **readability** sake and your IDE's sake ( *I use VIM BTW* ).

> [!NOTE]
> To find the "*type*" of the data type; you can use the `type()` function.
> In addition, there are more data types like `bytes`, `bytearray` and more!

# Display Stuff On Screen

In Python, to display stuff on our "*terminal*" screen ( *because we are not learning GUI here... For now!* ).
We can simply use the `print()` function.

```python
def main():
    # this will print a blank line above and below 'Hello World'
    print("\nHello World\n")
	
    # prints the character '-' 50 times in a straight line
    print("-" * 50)
	
    # need to "type cast"...
    print("\nI like the number" + str(5) + "\n")
    # create a variables
    name = "<Insert Your Name Here> "
    age = 20

    # this is how my lecturer does it because years of using 'C'
    print("My name is:" + name)
    print("My age is:", age, "\n")

    print("-" * 50)

    # this is how people in Python normally do this ==> using `f` strings / function
    print(f"\nMy name is: {name}")
    print(f"My age is: {age}")

	# outputs a blank like
	print()


if __name__ == '__main__':
    main()
```

> Python Documentation for `print()` function: https://docs.python.org/3/library/functions.html#print

> [!NOTE]
> We can only output / print variables of **string** datatypes with the `print()` function.
> This where Type Casting comes into play!s

## Type Cast

This is a fancy term for "*converting data types*"...

```python
def main():
    # let's say that
    number = 5
    boolean_thing = True
    some_decimal_num = 69.69

    # INFO: well the line below will return an error
    # print("\nNumber: " + number)

    # nevertheless, if we convert to to string just for the sake of "printing"
    print("\nNumber: " + str(number))
    print("True / False: " + str(boolean_thing))
    print("Decimal Number: " + str(some_decimal_num))


if __name__ == '__main__':
    main()
```

Hence, this is why I recommend using my lecturer's method or better ( *the best* ); use the `f` function.

> The above then simply becomes $\downarrow$:

```python
def main():
    # let's say that
    number = 5
    boolean_thing = True
    some_decimal_num = 69.69

    # using 'f' function
    print(f"\nNumber: {number}")
    print(f"True / False: {boolean_thing}")
    print(f"Decimal Number: {some_decimal_num}")


if __name__ == '__main__':
    main()
```

> This also improves the **readability** of the code!

# User Inputs

The only thing that you need to know is how to `input`!

Yes, in this programming language, we use the `input` function to accept input from a user.

> Below $\downarrow$ is a simple program that will ask the name of a user!

```python
# our main function
def main():
    # ask the user to enter his name
    user_name = input("\nPlease Enter Your Name: ")

    # display the user's name
    print(f"\n\t Your Name is: {user_name}")


# source the main function
if __name__ == "__main__":
    main()
```

## Input Data Types

Now, there **will** be a place whereby you need to ask the user to enter an **integer** or **float** value ( *and more IDK* ) and do some computation on that value.

But the only problem ( *that can be easily fixed!* ) is that our trusty `input()` function will always "*output*" in the **string** datatype!

Therefore, we are going to have to **convert** our string input into the desired data type that we want using [[#Type Cast]]!

> Here are some of the methods that I know on top of my head that can do that $\downarrow$

### Convert After User Input

> I don't like this method!

```python
# our main function
def main():
    # ask the user to enter an integer value
    user_int = input("\nPlease Enter An Integer Value: ")

    # output the value and 'type' of the user intput before conversion
    print(f"\n\tCurrent Input = '{user_int}' | Data Type of Input: {type(user_int)}")

    # verify that the user did enter a numerical value
    if user_int.isdigit():
        # convert the user input into integer
        user_int = int(user_int)

        # output the value and 'type' of the user intput after conversion
        print(
            f"\n\tCurrent Input = '{user_int}' | Data Type of Input: {type(user_int)}"
        )

    # else if the user did not enter a numerical value
    else:
        # output an appropriate message
        print("\n\t<< Please Enter Integer Values Only!!! > > ")


# source the main function
if __name__ == "__main__":
    main()
```

In this case, we are going to convert the user input into an **integer** data type. Therefore, we are going to **first** check if the user input is actually a *bunch of numbers* and then **convert** that *correct*, *bunch of numbers* into the required data type.

### Convert At Input Function

> [!NOTE]
> Here we are going to have to use **Exception Handling**. Its not difficult at all and we are going to get to that later on!

```python
# our main function
def main():
    # exception handling
    try:
        # ask the user to enter an integer value
        user_int = int(input("\nPlease Enter An Integer Value: "))

        # output the value and 'type' of the user intput before conversion
        print(
            f"\n\tCurrent Input = '{user_int}' | Data Type of Input: {type(user_int)}"
        )

    # if the user does not enter the correct data type
    except ValueError as e:
        # output appropriate message
        print(f"\n\t<< Error: {e} > > ")
        print("\t<< Please Enter Integer Values Only!!! > > ")


# source the main function
if __name__ == "__main__":
    main()
```

Similarly, we are trying to convert the user input to **integer**. But this time we are going to use [[#Exception Handling]] which is a way to catch errors in Python.

> Well, most *modern* languages have this feature to catch errors during the execution of the program!

# Conditions

Here is what you are going to need if you want to ask the do *something* based on some **conditions**.

## `if` Statements

```python
# our main function
def main():
    # ask the user to input his age
    user_age = int(input("Please Enter Your Age: "))

    # is user's age is between 18 and 100 ( inclusive )
    if user_age > = 18 and user_age < 100:
        # output appropriage
        print("You are an adult!")

    # if age entered is less and '0'
    elif user_age <= 0:
        # output appropriage message
        print("Error!")

    # if user's age is greater than 100
    elif user_age > = 100:
        # output appropriage message
        print("Congratulations! You are about to die!!!")

    # if the user's age is between 1 and 18
    elif user_age > = 1 and user_age <= 18:
        # output appropriage message
        print("Where is your guardian?")


# source the main function
if __name__ == "__main__":
    main()
```


## `match` Case Statements

```python
# our main function
def main():
	print("\nProgramming Language Choice Thing :)\n")
	
	# Asking the user to input his language of choice
	# ask the user to enter his language of choice
	lang = input("What's the programming language you want to learn? ")
	
	# check the user's input / language entered
	match lang:
	
	    # if users entered 'Javascript'
	    case "JavaScript":
	        # output appropriate message
	        print("You can become a Web Developer!")
	
	    # if users entered 'Python'
	    case "Python":
	        # output appropriate message
	        print("You can become a Data Scientist!")
	
	    # if users entered 'PHP'
	    case "PHP":
	        # output appropriate message
	        print("You can become a Backend Developer!")
	
	    # if users entered 'Solidity'
	    case "Solidity":
	        # output appropriate message
	        print("You can become a Blockchain Developer!")
	
	    # if users entered 'Java'
	    case "Java":
	        # output appropriate message
	        print("You can become a Mobile App Developer!")
	
	    # if the users did not enter anything that is found above
	    case _:
	        # output appropriate message
	        print("The language doesn't matter, what matters is solving problems!")


# source the main function
if __name__ == "__main__":
    main()
```

# Loops

If you ever need to iterate over *something* **repeatedly**... Well, you are going to need is a **loop**.

Below you are going to find how we do *loops* in Python!

## `while` Loops

```python
# our main function
def main():
    # iterate through the `while` loop indefinitely
    while True:
        # ask the user to enter his phone number
        tel_num = input("Please Enter Telephone Number: ")

        # check if the length of the variable is '8'
        # and that the string variable contains numbers only
        if tel_num.isdigit() and len(tel_num) == 8:
            # exit / break from the `while` loop
            break

        # if the user string did not contain any number
        # or the length of string entered was not '8'
        else:
            # output appropriate message
            print("\nPlease Enter Correct Telephone Number!\n")

    # display the following message after exiting `while` loop
    print(f"\nYour Telephone Number is {tel_num}")


# source the main function
if __name__ == "__main__":
    main()
```


## `for` Loops

```python
# our main function
def main():
    # display 5 integer numbers from '0' to '4'
    for i in range(5):
        # display those numbers in a single line
        print(i, end=" ")

    print()
    print()

    # display same 5 integer numbers from '0' to '4' but in reverse
    for i in range(4, -1, -1):
        # display those numbers in a single line
        print(i, end=" ")

    print()
    print()

    # display numbers from '1' to '100' ( inclusive )
    for i in range(1, 101):
        # display those numbers in a single line
        print(i, end=" ")

    print()
    print()

    # display even numbers from '1' to '100' ( inclusive )
    for i in range(2, 101, 2):
        # display those numbers in a single line
        print(i, end=" ")

    print()
    print()

    # display even numbers from '1' to '100' ( inclusive )
    for i in range(1, 101, 2):
        # display those numbers in a single line
        print(i, end=" ")

    print()


# source the main function
if __name__ == "__main__":
    main()
```

## Keywords Related to Looping

### The `break` Keyword

As the word "*break*" suggests... We are going to be *breaking* from the loop

> I am going to be re-using the same example as the `while` loop!

```python
# our main function
def main():
    # iterate through the `while` loop indefinitely
    while True:
        # ask the user to enter his phone number
        tel_num = input("Please Enter Telephone Number: ")

        # check if the length of the variable is
        if tel_num.isdigit() and len(tel_num) > 8:
            # exit / break from the `while` loop
            break

        # if the user string did not contain any number
        else:
            # output appropriate message
            print("\nPlease Enter Correct Telephone Number!\n")

    # display the following message after exiting `while` loop
    print(f"\nYour Telephone Number is {tel_num}")


# source the main function
if __name__ == "__main__":
    main()
```

### The `continue` Keyword

If you want to **skip** something for example, in a `for` loop with numbers... We can easily do so with the `continue` keyword!

```python
def main():
    # iterate from '0' to '10'
    for i in range(11):
        # skip the following numbers found inside the list of numbers
        if i in [2, 5, 8, 10]:
            # skip the number and don't display that number
            continue

        # if the number is not in the list
		# display the numbers / output in a single line
		print(i, end=" ")

    print()


if __name__ == "__main__":
    main()
```

### The `pass` Keyword

<p align="center"> <strong> Just Don't Do Anything</strong> </p>

Its the equivalent of `null` found in some other languages!

For example, if you need to skip, for example an `if` statement, we can simply use it to **avoid** any errors


```python
def main():
    pass


if __name__ == "__main__":
    main()
```

> If you remove the `pass` keyword... You are going to encounter an error!

# Functions

> Yes, I already have been using it in the examples above :)

Well to create a function in Python, we use the `def` keyword.

Python is **not** like shitty programming languages like [Visual Basic ( .NET Fucker )](https://en.wikipedia.org/wiki/Visual_Basic_(.NET)).

Whereby Python does not have things like *procedures* and also *functions*. We just have the simple the `def` here!

But the only theoretical thing that you *might* need to know is that a **Procedure** typically does **not** return a value but can **modify** *data* or *output* **multiple** values via parameters. A **Function**, on the other hand, **always** returns a *single* value.

## Simple Addition Function

```python
# function that return the addition of 2 numbers
def addition(a: int, b: int) -> int:
	# return the result of the calculation
	return int(a) + int(b)

# our main function
def main():
	# call the function on its own
	print(f"\tRan Directly From 'print' Function: {addition(5, 5)}")
	
	# create a variable and call the function
	sum_2_nums = addition(1, 1)
	
	# output result to the user
	print(f"\tFunction's Value Assigned to a Variable: {sum_2_nums}")

# source the main function
if __name__ == '__main__':
	main()
```

> [!INFO]
> The `return` keyword can only be used **with** / **inside** of functions and / or methods!

## Palindrome Function

If you don't know what a '*Palindrome*' is; I suggest to go kill yourself. Nah mate! I am joking else I would **not** have been here writing this after 7 years.

```python
# function to check if a string is a palidrome
def palindrome_checker(string: str):
	# verify and return the result
	return string.lower().replace(" ", "") == string.lower().replace(" ", "")[::-1]


# our main function
def main():
	# call the function on its own
	print(f"\tRan Directly From 'print' Function: {palindrome_checker("Nurses Run")}")
	print(f"\n\tIs '1001' a Palindrome: {palindrome_checker("1001")}")
	print(f"\tIs 'Your Mama' a Palindrome: {palindrome_checker("Your Mama")}")
	
	
# source the main function
if __name__ == '__main__':
	main()
```

## Recursive Function

This is a recursive function that will calculate the **factorial** of a number entered by a user.

```python
# function to calculate the factorial of a positive integer number
def factorial(number: int):
    # our base case
    if number == 1:
        # meaning that we go '1' as argument
        return 1

    # if the arguement passed is not '1'
    else:
        # find the factorial by multiplication
        return number * factorial(number - 1)


# our main function
def main():
    # exception handling
    # NOTE: again, we are going to get to that later on!
    try:
        # ask the user to enter a positive integer number
        user_num = int(input("\nPlease Enter A Number: "))

        # call the function to factorial function and assign to a variable
        factorial_result = factorial(abs(user_num))

        # output the required result
        print(f"\n\t<< The factorial of '{abs(user_num)}' = {factorial_result} > > \n")

    # if the user does not enter the correct data type
    except ValueError as e:
        print(f"\n\tError: {e}")
        print("\tPlease Enter Integer Numbers Only!!!\n")

        # output a horizontal rule in the middle of the screen
        print("\t", end="")
        print("-" * 53)

        # call the main function again
        main()


# source the main function
if __name__ == "__main__":
    main()
```

> Well, the factorial function is only 5 lines of actual code!

# Exception Handling

In Python, to catch an error during runtime... We use the `try... except... else... finally` *statement*. For example, if you have not yet **implemented** a function, we can **raise** and error to indicate that the function has not been implemented yet!

> The example below is not really related to Exception Handling... But I think that its good to know this!
>
> "*A little more knowledge and UNDERSTANDING does not hurt the brain*"

```python
# some big function
def big_ass_function():
    # raise the error
    raise NotImplementedError


# our main function
def main():
    # call the function `big_ass_function`
    big_ass_function()


# source the main function
if __name__ == "__main__":
    main()
```

In this case, the output is going to look something like this $\downarrow$

```console
Traceback (most recent call last):
  File "/home/username/Desktop/main.py", line 15, in <module>
    main()
    ~~~~^^
  File "/home/username/Desktop/main.py", line 10, in main
    big_ass_function()
    ~~~~~~~~~~~~~~~~^^
  File "/home/username/Desktop/main.py", line 4, in big_ass_function
    raise NotImplementedError
NotImplementedError
```

> [!TIP] Output A Message With `raise` Keyword
> As you can see, we have `raise NotImplementedError` at line 4. But we can change that to `raise NotImplementedError("This Function Has Yet To Been Implemented!!!")`
>
> And hence, in the *error message*, we are going to see that we have *the* message that we wrote!
>
> ```console
> NotImplementedError: This Function Has Yet To Been Implemented!!!
> ```

## Format of Exception Handling

This is how the general format for `try... except... else... finally` is written

```python
# our main function
def main():
    # exception handling
    try:
        # ask the user to enter a positive integer number
        user_num = abs(int(input("\n\tPlease Enter A Positive Integer Number: ")))

        # output the number together with the 'type'
        print(
            f"\n\tCurrent Input = '{user_num}' | Data Type of Input: {type(user_num)}"
        )

    # if the user does not enter a integer value
    except ValueError as e:
        # output appropriate message
        print(f"\n\t<< Error: {e} > > ")
        print("\t<< Please Enter Integer Values Only!!! > > ")

    # condition that runs if not error has been raised
    else:
        # output appropriate message
        print("\n\t<< No Error Has Been Raised!!! > > ")

        # condition that will always run whether if error was raised or not
    finally:
        # output a horizontal rule
		print("\n\t" + "-" * 50, "\n")       

        # output appropriate message
        print("\n\t<< I ALWAYS RUN... HAHAHAHAHAHHHH!!! > > ")


# source the main function
if __name__ == "__main__":
    main()
```

Okay, now you might be asking the question of how to find things like `ValueError` or `NotImplmentedErrorr`...

1. There is always the [official](https://docs.python.org) and unofficial ones!
2. Simply fucking run your program and see what error it outputs!

---

> [!INFO] Confession Time
> To be honest, with you... Just watch a lot of people on YouTube / Twitch like "*live code*". I know its kinda boring and maybe un-productive.
>
> But who needs to be 100 % productive all the time! In today's world, every one in their mother on social media platforms tell you to keep fucking grinding. But I want to live my fucking also!
>
> No, but really! I do get inspired when I see these people code and I recently got really inspired by [Nikilov Lazar](https://www.youtube.com/watch?v=e8w_PJLKHuM) when he was building a Full Stack Resume web application. Just play these types of videos in the background and do some work. When you hear them say a word or things that you never heard of. Then you can go watch that bit!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!