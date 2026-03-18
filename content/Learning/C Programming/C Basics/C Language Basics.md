---
id: C Language Basics
aliases: C Language Basics
tags:
  - C
  - basics
author: S.Sunhaloo
date: 2024-11-05
status: Completed
---

## List of Contents

- [[#Requirements]]
- [[#C Boiler Plate]]
- [[#Basics Data Types]]
- [[#Display Stuff to Screen]]
	- [[#Type Cast]]
- [[#User Inputs]]
- [[#Conditions]]
- [[#Loops]]
- [[#Functions]]
- [[#Exception Handling]]

---

> [!INFO] Official Documentation
> Website: https://www.gnu.org/software/gnu-c-manual/gnu-c-manual.html

# Requirements

- `gcc` compiler
- `make`
- Code Editor of Choice

## C Boiler Plate

```C
#include <stdio.h>

int main() {
	printf("Hello World!\n");

	return 0;
}
```

### Simple Makefile Boiler Plate

This is the **contents** of the make file that I have used to compile the above boiler plate code...

```bash
program:
	gcc main.c -o program

clean:
	rm -rf *.o
	echo Done Cleaning
```

# Basics Data Types

```C
#include <stdio.h>

int main() {
	// this is a single line comment
	/*
	   This is a multi-line
	   comment. Very
	   Nice!
	*/

	// I like to declare and initialise at the same time for most simple things
	int num = 69;
	float floating_num = 6.9;
	double big_floating_num = 69.69;
	char character_thingy = 'A';
	char yes_this_is_a_string[11] = "Hello World";

	return 0;
}
```

> [!NOTE]
> C has so much fucking data types that its difficult to memorise them if you "*main*" other programming languages.
> Hence, here it the Wikipedia Link for *Datatypes in C*: https://en.wikipedia.org/wiki/C_data_types
> Additionally, we don't even have **boolean** data types without importing the header file `<bool.h> `!
>
> > In the above $\uparrow$ I only used the most common and simple datatypes.

> This is the reason why I like C so much. You *C*, you only import / use things that you really need. No shitty bloat things.

# Display Stuff to Screen

In C, to display "*things*" on our screen, we simply use the `printf()` function.

Compared to the `print()` function in programming languages like Python. The one in C is in a way better but really bad when it comes to actual flow when typing it in.

> The first appearance of `printf` in the gnu-c-manual is at chapter '1.3.4 String Constants'

```C
#include <stdio.h>

// create a function that will be able to emulate `print('-'*50)`
void print_dashed_lines(int amount) {
	for(int i = 0; i <= amount; i++){
		printf("-");
	}
	printf("\n");

}


int main() {
	// print a blank line above and below "Hello World"
	printf("\nHello World\n");
	// call the function to output 50 '-' characters.
	print_dashed_lines(50);
	// output the sentence whereby the number '5' is of type integer
	printf("\nI like the number %d\n\n", 5);

	// create and initialise variables
	char name[23] = "<Insert Your Name Here> ";
	int age = 20;

	// output these variables to the screen
	printf("My name is: %s\n", name);
	printf("My age is: %d\n\n", age);

	// again call the function to print a line '-'
	print_dashed_lines(50);

	// output a blank line
	printf("\n\n");
	
	return 0;

}
```

> Compared to Python, this has much more number of lines.

> [!NOTE]
> In Python, to output a blank line, you would just do `print()`. But here, its a bit different.
>
> You see, when you write something like `printf("Hello World\n");`. This will obviously output the words 'Hello World' but also move the **cursor** ( *or caret* ) on line below. But if you try to print something after that line. You will see that it will **not** place a blank line below 'Hello World'.
>
> Therefore, if you want to print a blank line or emulate the `print()` function from Python, we need to do:
>
> ```C
> printf("\n\n");
> ```

> [!WARNING]
> In Python we can do stuff like `print('-'*50)`. Well, this does not exist in C!
>
> > You have to manually do that with a `for` loop.

## Type Cast

> [!INFO]
> Here is a good read about Type Casting by [GeeksForGeeks](https://www.geeksforgeeks.org): https://www.geeksforgeeks.org/c-typecasting/
>
> > I know, I know, we should [not](https://www.reddit.com/r/learnprogramming/comments/lot6ah/geeksforgeeks_not_a_good_place_to_get_started/) be using GeekForGeeks as **beginners**!

Here are some simple example of Type Casting in C $\downarrow$:

```C
#include <stdbool.h>
#include <stdio.h>

int main() {
  // create an integer variable
  int number = 5;
  bool boolean_thing = true;
  float some_decimal_num = 69.69;
  char some_character = 'A';

  // output before conversion
  printf("\nVariables BEFORE Type Cast\n\n");
  printf("The Number is: %d\n", number);
  printf("The Number is: %d\n", boolean_thing);
  printf("The Number is: %f\n", some_decimal_num);
  printf("The Character is: %c\n", some_character);

  // apply the type cast ==> change the data type
  float decimal_int_number = (float)number;
  int int_boolean_thing = (int)boolean_thing;
  int int_some_decimal_num = (int)some_decimal_num;
  int int_some_character = (int)some_character;

  // output after conversion
  printf("\nVariables AFTER Type Cast\n\n");
  printf("The Number is: %f\n", decimal_int_number);
  printf("The Number is: %d\n", int_boolean_thing);
  printf("The Number is: %d\n", int_some_decimal_num);
  printf("The Number is: %d\n", int_some_character);
  
  return 0;
}
```

I suggest you that you have a read of the link that I provided above because there are lot of things that we have in C.

> [!INFO]
> In the program / code, we have use the data type 'boolean' by including the header file `#include <stdbool.h> `
>
> > [!NOTE]
> > Even if you do something like `bool something = true;` or `bool someone = false;`. When you are going to print this out. You are going to use the `%d` [Format Specifier](https://www.geeksforgeeks.org/format-specifiers-in-c/).
> >
> > This due to the fact that `true` is simply `1` and `false` is simply `0`!
>

> Then in my eyes, just use a constant of type integer or do use a 'enum' or something like that
> Yes, I don't understand 'enums'... *Yet*!

# User Inputs

Compared to the famous `input()` function from [[Python Language Basics#User Inputs | Python]]. Here we have 2 **main** input functions that we are going to be using in C.

## `scanf` Function

> If you have used / programmed with [Visual Shitty Basics]() or [[Learning/Java/Java Data View | Java]], the way we do it is similar...

```c
#include <stdio.h>

// our main function
int main(int argc, char *argv[]) {
  // declare a variety of variables of different data types
  int int_num;
  float float_num;
  double double_num;
  char character;
  char arr_str[10];

  // ask the user to enter an integer number
  printf("\nPlease Enter An Integer Number: ");
  scanf("%d", &int_num);

  // ask the user to enter an "float" / decimal number
  printf("\nPlease Enter A Float Number: ");
  scanf("%f", &float_num);

  // ask the user to enter an "double" / decimal number
  printf("\nPlease Enter A 'Double' Number: ");
  scanf("%lf", &double_num);

  // clean the buffer / remove the newline character
  getchar();

  // ask the user to enter an character
  printf("\nPlease Enter A Character: ");
  scanf("%c", &character);

  // ask the user to enter an string
  printf("\nPlease Enter A String: ");
  scanf("%s", arr_str);

  // display the "values" entered to the user
  printf("\nInteger Number: %d\n", int_num);
  printf("Float Number: %f\n", float_num);
  printf("Double Number: %lf\n", double_num);
  printf("Character: %c\n", character);
  printf("String: %s\n", arr_str);

  return 0;
}
```

> [!INFO] What is `%0.2f`?
> This is basically doing something like this *from* [[Learning/Python/Python Data View|Python Data View | Python]]:
>
> ```python
> # display only 2 to decimal places
> print(f"\nSum of Money = {money_sum:.2f}\n")
> ```
>
> Adding `0.2` in front means that its only going to display to **2 decimal places**.

> [!WARNING] The Problems With The `scanf` Function
> - Retrieves characters up to the first whitespace
> - Newline characters might stays inside the buffer
>
> Yes, using `scanf` will only grab your "*string*" up to the **first whitespace character**. This means that if you enter something like "Hello World"... Only the `Hello` part will actually be stored!
>
> There is also another problem of the `\n` character staying in the "*stream*" buffer whereby, let's say that you are **first** asking the user to *enter* a `double` number and then a `char`acter.
>
> The user will <strong> <span style="color: red;"> not</span> </strong> be able to enter anything!
>
> > Again due to that *pesky* `\n` character ( *our `<Enter> ` key BTW* )
>
> Therefore, we need to use a "*special*" function called `getchar` that is going to **consume** our `\n` character to allow the user to enter a value for *that* input.
>
> > See above code!
>
> > [!NOTE]
> > From what I can understand, if you have for example, `four_chars[3]`. This means that we can only enter **3** characters. If you go ahead and enter something like `1234`; then you are going to get this error message:
> >
> > ```console
> > Please Enter 3 Characters: 1234
> > String: 1234
> > *** stack smashing detected ***: terminated
> > [1]    4603 IOT instruction (core dumped)  ./test
> > ```
> >
> > > In this case, the *compiled* program is called `test`!
> >
>

## `fgets` Function

The `fgets` function is the typical function used to get a *string*. Compared to our `scanf` function; this function does *read* characters **after** whitespaces.

```c
#include <stdio.h>

int main(int argc, char *argv[]) {
  // declare array of characters of size 20 to hold the user's name
  char full_name[20];
  // declare array of characters of size 20 to hold the user's surname
  char address[40];

  // ask the user to enter his full name
  printf("\nPlease Enter Your Full Name: ");
  fgets(full_name, sizeof(full_name), stdin);

  // ask the user to enter his address
  printf("Please Enter Your Address: ");
  fgets(address, sizeof(address), stdin);

  // display the full name and address of the user
  printf("\nFull Name: %s\n", full_name);
  printf("Address: %s\n", address);

  return 0;
}
```

There are **3** parameters that we need to pass to the `fgets` function and they are:

1. Array / *Destination Buffer*
2. Maximum Buffer / Input Size ( *i.e number of characters allowed* )
3. Input Source Stream

> [!WARNING] The Null Terminator And `\n` Character
> Let's say that we **modified** the size of the *array of character* to `char full_name[5]` and `char address[10]`.
>
> Compared to the `scanf` function, if we enter `1234` ( *because full name's array size is '5'* )... We are <strong> <span style="color: red;"> not</span> </strong> going to be able to enter *data* for the `address`!
>
> This is due to the fact that we have the `\n` character is <span style="color: orange;"> not</span> stored inside the array!
>
> But we do have space for `\n` right? As we only entered *4* characters, we should have space of it...
>
> > **No**, we **don't** have space for `\n`!
>
> This is because of something called the **Null Terminator** ( `\0` ) or **Character** which is *special control character* that signifies the **end of a string**!
>
> It is a "*special*" character with the ASCII value of '0' and is **non-printable**!
>
> Modifying this part of the *above* code:
>
> ```c
>  // declare array of characters of size 20 to hold the user's name
>  char full_name[5];
>  // declare array of characters of size 20 to hold the user's surname
>  char address[10];
>
>  // ask the user to enter his full name
>  printf("\nPlease Enter Your Full Name ( 5 Characters ): ");
>  fgets(full_name, sizeof(full_name), stdin);
>
>  // INFO: in this case, to be able to actually allow the user to enter data
>  // into the `address` variable, we are going to have to:
>  // 1. get / remove the last character ==> '\n'
>  // 2. get / remove the null character ==> '5'
>  printf("\n%c\n", getchar());
>  printf("\n%c\n", getchar());
> ```
>
> Currently if you enter `12345`... The actual representation inside the array is going to be like this: `{'1', '2', '3', '4', '\0'}` ( *including the `<Enter> ` key*! ). This means that the "*garbage characters*" are `5` and `\n` respectively.
>
> This is why if you *remove* the 2 `getchar`s function, you are going to see that the program **terminate** and `address` gets the value of '5'. But you did **not** press the `<Return> ` key or anything like that!
>
> But remember that `\n` is part of the *garbage* input! Well we know that pressing `<Enter> ` keys means that we are "*printing*" `\n`. Well it just simply **emulates** the return key!
>

### Emulating `fgets` With `scanf`

> Yes, we can do that!

I have been seeing some code on [stackoverflow](https://www.stackoverflow.com) whereby instead of using `fgets` to get a *string* input... The simply used the `scanf` function.

But we know that it **cannot** read after *seeing* the first whitespace... *Or can it*?

Additionally, I saw that my lecturer was using it. Therefore, I have to include this in here!

#### Lecturer's Version

```c
#include <stdio.h>

// our main function
int main(int argc, char *argv[]) {
  // declare array of characters of size 20 to hold the user's name
  char user_name[5];
  // declare array of characters of size 20 to hold the user's surname
  char address[10];

  // INFO: asked Gemini about the lecturer's `scanf` version...
  // this is why I am using a small array of character size

  // ask the user to enter his username
  printf("\nPlease Enter Your 4 Character Username: ");
  // NOTE: look how we cannot make the user enter 5 characters
  scanf("%4[^\n]", user_name);

  // ask the user to enter his address
  printf("\nPlease Enter Your 9 Character Address: ");
  // similarly, we can only enter 9 actual characters
  scanf("%9[^\n]", address);

  // display the username and address of user
  printf("\nUsername: %s\n", user_name);
  printf("Address: %s\n", address);

  return 0;
}
```

> [!WARNING] Similar to `fgets`
> If you enter a 4 character username like `fuck`... The *newline character* will still be **inside** the buffer and therefore, the `address` variables is "*entered*" automatically!

#### Gemini's Version

Hence, [Gemini](https://gemini.google.com) tells me to update the `scanf` function so that the `\n` character does **not** stay in the *input buffer*!

> Only showing the code with changes made!

```c
  // ask the user to enter his username
  printf("\nPlease Enter Your 4 Character Username: ");
  // NOTE: look how we cannot make the user enter 5 characters
  scanf("%4[^\n]%*c", user_name);

  // ask the user to enter his address
  printf("\nPlease Enter Your 9 Character Address: ");
  // similarly, we can only enter 9 actual characters
  scanf("%9[^\n]%*c", address);
```

> But again the size of the *input buffer* inside the `scanf` function should be `array_size - 1`!

> [!SUCCESS]
> In this case, the program will allow us to input for the `address`!

# Conditions

## `if` Statements

```c
#include <stdio.h>

// our main function
int main() {
  // declare variable that will hold the user's age
  int user_age;

  // ask the user to input his age
  printf("Please Enter Your Age: ");
  scanf("%d", &user_age);

  // is user's age is between 18 and 100 ( inclusive )
  if (user_age > = 18 && user_age < 100) {
    // output appropriage
    printf("\n\t== You are an adult!!! ==\n");
  }

  // if age entered is less than '0'
  else if (user_age <= 0) {
    // output appropriage message
    printf("\n\t<< Error!!! > > \n");
  }

  // if user's age is greater than 100
  else if (user_age > = 100) {
    // output appropriage message
    printf("\n\t== Congratulations! You are about to die!!! ==\n");
  }

  // if the user's age is between 1 and 18
  else if (user_age > = 1 && user_age <= 18) {
    // output appropriage message
    printf("\n\t<< Where is Your Guardian!!! > > \n");
  }

  return 0;
}
```

## `switch` Case Statements

```c
#include <stdio.h>

// our main function
int main() {
  // declare variable that will store the user's grade
  char grade;

  // ask the user to enter his / her grade
  printf("Enter your grade (A, B, C, D, or F): ");
  scanf(" %c", &grade);

  // `switch` statement that will consider the `grade` variable
  switch (grade) {
	  // if the user enter the character 'A'
	  case 'A':
	    // output appropriate message
	    printf("Excellent! You've done an outstanding job.\n");
	    break;
	
	  // if the user enter the character 'B'
	  case 'B':
	    // output appropriate message
	    printf("Good! You've met the standards.\n");
	    // Exit the switch statement
	    break;
	
	  // if the user enter the character 'C'
	  case 'C':
	    // output appropriate message
	    printf("Satisfactory. You are on the right track.\n");
	    break;
	
	  // if the user enter the character 'D'
	  case 'D':
	    // output appropriate message
	    printf("Needs improvement. Let's work on getting a better grade.\n");
	    break;
	
	  // if the user enter the character 'F'
	  case 'F':
	    // output appropriate message
	    printf("Failure. Don't give up! Study hard for the next one.\n");
	    break;
	
	  // if the user did not enter anything that is found above
	  default:
	    // output appropriate message
	    printf("\n\t<< Invalid Grade!!! > > \n");
  }

  return 0;
}
```

### No Strings!

The `switch... case` statement in C is not like the one in [[Python Language Basics#`match` Case Statements | Python]] where it can also **compare** *strings*!

Therefore, if you want to *emulate* the `match... case` statement from Python, we simply need to use our lovely `if` statements!

```c
#include <stdio.h>
#include <string.h>

int main() {
  // variable that will store the user's input for programming language
  char lang[50];

  printf("\n\t== Programming Language Choice Thing :) ==\n\n");

  // ask the user to enter his programming language of choice
  printf("What's the programming language you want to learn? ");
  scanf("%s", lang);

  // NOTE: need to use `strcmp` from 'string.h'
  // as we cannot directly compare strings in C!

  // if the user's want to learn 'Javascript'
  if (strcmp(lang, "JavaScript") == 0) {
    printf("\n\t<< You can become a Web Developer!!! > > \n");

    // if the user's want to learn 'Python'
  } else if (strcmp(lang, "Python") == 0) {
    printf("\n\t<< You can become a Data Scientist!!! > > \n");
    // if the user's want to learn 'PHP'

  } else if (strcmp(lang, "PHP") == 0) {
    printf("\n\t<< You can become a Backend Developer!!! > > \n");

    // if the user's want to learn 'Solidity'
  } else if (strcmp(lang, "Solidity") == 0) {
    printf("\n\t<< You can become a Blockchain Developer!!! > > \n");

    // if the user's want to learn 'Java'
  } else if (strcmp(lang, "Java") == 0) {
    printf("\n\t<< You can become a Mobile App Developer!!! > > \n");

    // if the user's does not enter something that found above
  } else {
    printf("\n\t<< The language doesn't matter, what matters is solving problems!!! > > \n");
  }

  return 0;
}
```

> [!NOTE] `<string.h> ` Header And `strcmp` Function
> In Python, we can easily do something like this:
>
> ```python
> 	# python code to compare string with `if` statement
> if name == "fuck you":
> 	print("Its You!!!")
> ```
>
> Hence, to be able to do the *same*; we need to use the `strcmp` from the `string.h` header file!

# Loops

## `while` Loops

```c
#include <ctype.h>
#include <stdio.h>
#include <string.h>

// define a little macro that will help us to find the length of arrays
#define LEN(arr) (sizeof(arr) / sizeof(arr[0]))

// function to allow the user to enter this phone number
int enter_phone_number() {
  // declare variable that will hold the telephone number entered by user
  char telephone_num[10];

  // declare variable that will hold the converted "integer" telephone number
  int int_tel_num;

  // declare flag that will keep track if user's input it valid
  int is_valid = 1;

  // iterate through the `while` loop indefinitely
  while (1) {
    // ask the user to enter his telephone number
    printf("\nPlease Enter Your Telephone Number ( No Spaces ): ");
    scanf("%s", telephone_num);

    // check for the length of the user's telephone input
    if (strlen(telephone_num) != 8) {
      // output appropriate message
      printf("\n\t<< Length Of Telephone Number Needs To Be 8!!! > > \n");

      // continue to ask the user to enter telephone number
      continue;
    }

    // reset the `is_valid` flag to '1'
    is_valid = 1;

    // check if the phone number / string composes of all integer numbers
    // ==> iterate through the array of characters until null terminator
    for (int i = 0; telephone_num[i] != '\0'; i++) {
      // check if each character is actually an integer number
      if (!isdigit(telephone_num[i])) {
        // the input entered by the is not valid ==> change flag status
        is_valid = 0;

        // input not valid ==> exit the innermost `for` loop
      }
    }

    // check if `is_valid` flag's "status"
    if (is_valid) {
      // first convert the string into an actual number
      sscanf(telephone_num, "%d", &int_tel_num);
      // user input is valid ==> break from the outer `while`
      break;

      // it the user's input is not valid ==> ask the user to enter again
    } else {
      // output appropriate message
      printf("\n\t<< Please Enter Valid Phone Numbers Only!!! > > \n");

      // continue to ask the user to enter a telephone number until its valid
    }
  }

  // return the converted string to the main program
  return int_tel_num;
}
```

## `do ... while` Loops

```c
#include <stdio.h>

// our main function
int main() {
  // declare integer variable that will hold the user's input
  int num;

  // iterate throught the `do ... while` loop at least for 1 time
  do {
    // askt the user to enter positive integer number
    printf("\nPlease Enter A Positive Integer Number: ");
    scanf("%d", &num);

    // check if the user entered a negative number
    if (num <= 0) {
      // output appropriate message
      printf("\n\t<< Please Enter Positive Numbers Only!!! > > \n");
    }

    // keep asking the user to enter postive number if negative input
  } while (num <= 0);

  // display the number entered
  printf("\n\t== You entered the positive number: %d ==\n", num);

  return 0;
}
```

## `for` Loops

```c
#include <ctype.h>
#include <stdio.h>
#include <string.h>

// define a little macro that will help us to find the length of arrays
#define LEN(arr) (sizeof(arr) / sizeof(arr[0]))

// function to allow the user to enter this phone number
int enter_phone_number() {
  // declare variable that will hold the telephone number entered by user
  char telephone_num[10];

  // declare variable that will hold the converted "integer" telephone number
  int int_tel_num;

  // declare flag that will keep track if user's input it valid
  int is_valid = 1;

  // iterate through the `while` loop indefinitely
  while (1) {
    // ask the user to enter his telephone number
    printf("\nPlease Enter Your Telephone Number ( No Spaces ): ");
    scanf("%s", telephone_num);

    // check for the length of the user's telephone input
    if (strlen(telephone_num) != 8) {
      // output appropriate message
      printf("\n\t<< Length Of Telephone Number Needs To Be 8!!! > > \n");

      // continue to ask the user to enter telephone number
      continue;
    }

    // reset the `is_valid` flag to '1'
    is_valid = 1;

    // check if the phone number / string composes of all integer numbers
    // ==> iterate through the array of characters until null terminator
    for (int i = 0; telephone_num[i] != '\0'; i++) {
      // check if each character is actually an integer number
      if (!isdigit(telephone_num[i])) {
        // the input entered by the is not valid ==> change flag status
        is_valid = 0;

        // input not valid ==> exit the innermost `for` loop
      }
    }

    // check if `is_valid` flag's "status"
    if (is_valid) {
      // first convert the string into an actual number
      sscanf(telephone_num, "%d", &int_tel_num);
      // user input is valid ==> break from the outer `while`
      break;

      // it the user's input is not valid ==> ask the user to enter again
    } else {
      // output appropriate message
      printf("\n\t<< Please Enter Valid Phone Numbers Only!!! > > \n");

      // continue to ask the user to enter a telephone number until its valid
    }
  }

  // return the converted string to the main program
  return int_tel_num;
}

// our main function
int main(int argc, char *argv[]) {
  int num = enter_phone_number();

  printf("\nNumber = %d\n", num);

  return 0;
}
```

# Functions

As you already know by now, C is a **declarative** language. This means that we need to **declare** ( *i.e make "space" for that* ) variable(s) in order to use them.

Similarly, we can also apply the **same** *principle* to functions! Whereby one can simply declare a function and later *code* its actual functionality.

Additionally, you like how in Python, we would use *type hinting*... In this case, we need to actually declare the *function type* to what *type* its **returning**!

> See the code later to see what I am actually talking about!

> [!INFO] Anywhere!!!
> Compared to ( *"old"* ) Python which we know is an interpreted language.
>
> Therefore, to avoid any problems with any functions, we typically write our "*other*" functions before writing our `main` function.
>
> Hence, when the **interpreter** is going to each line... It will cannot say that a function has **not** been found!
>
> > But this is not the case in C!
>
> You could do something like:
>
> 1. Declare and / or Code required function **before** `main` function
> 2. Declare and / or Code required function **after** `main` function
>
> > "*C Does Not Really Care*!!!
>
> This is due to the fact that its a **compiled** language!


## Simple Addition Function

This is a simple addition function that is going to add 2 numbers!

In this case, I am going to simply **declare** the `addition` function and then *code* its functionality **after** the `main` function.

```c
#include <stdio.h>

// declare function to perform addition of 2 numbers
int add(int, int);

// our main fucntion
int main() {
  // declare variable that will hold the addition of '19' + '1'
  int add_result = add(19, 1);

  // display the result to the screen
  printf("== Addition Of Numbers: %d ==\n", add_result);

  return 0;
}

// implementation of addition function
int add(int num_1, int num_2) { return num_1 + num_2; }
```

> [!NOTE] My Opinion
> In my eyes... I think that this is totally *pointless*!
>
> Why *type* **more** and **increase** the number of lines in our file!
>
> > Even if you love *typing*... "*Why do something so un-optimised*?"
>

## Recursive Function

This function is going to calculate the power of a *floating* number raised to the power of an *integer* number.

In this case, I am going to code the function in the same way that I code functions in [[Python Language Basics#Functions | Python]]; i.e **above** the `main` function!

> [!WARNING]
> You <strong> <span style="color: red;"> cannot</span> </strong> code a function *directly* **below** the `main` function in C!
>
> > At least in the version of C that I am using.
>
> If I tried doing it, Neovim's `clang` *Language Server* tells me this:
>
> ```console
> ISO C99 and later do not support implicit function declarations
> ```
>
> > The more you know!
>
> This is how I like to do it as I come from Python!

```c
#include <stdio.h>

// function that will ask the user to enter the base and exponent
void enter_required_data(float *base, int *exponent) {
  // ask the user to enter a number floating number for base
  printf("\nPlease Enter A Number For Base: ");
  scanf("%f", base);

  // ask the user to enter a number integer number for exponent
  printf("Please Enter An Integer Number For Exponent: ");
  scanf("%d", exponent);
}

// function that will recursively find power of a number
float power_recursive(float base, int exponent) {
  // ( base case ) check if the exponent is '0'
  if (exponent == 0) {
    // any number to the power of '0' is equal to '1'
    return 1;

    // ( smaller case ) if the exponent is positive
  } else if (exponent > 0) {
    // calculate the power recursive for positive exponent numbers
    return base * power_recursive(base, exponent - 1);

    // ( smaller case ) if the exponent is negative
  } else {
    // calculate the power recursive for negative exponent numbers
    return 1 / power_recursive(base, exponent * -1);
  }
}

// our main fucntion
int main() {
  // declare variable that will hold the user's input for base and exponent
  float base;
  int exponent;

  // call the function to allow the user to enter required data
  enter_required_data(&base, &exponent);

  // call the function to find the power of required number
  float result = power_recursive(base, exponent);

  // display the answer to the screen
  printf("\nNumber '%0.2f' Raised To The Power Of '%d' = %0.2f ( 2 DP )\n",
         base, exponent, result);

  return 0;
}
```

> [!WARNING] Side Note ( 27/02/2026 @ 16:41 )
> So the above `power_recursive` does indeed show a *recursion* function but the code itself, which BTW I wrote myself; is one of the **worst** code that you are going to find on the internet!
> 
> It combines the O(n) from the `for` loop together with the overhead that comes with the actual recursion process.
> 
> > Found that out when I was learning about different algorithms to find the 'power of a number' over at '[[Python - Power of a Number]]'!

## `void` Functions

They are basically *normal* function but does **not** return anything!

What I am trying to say its that they **don't** have the `return` keyword inside them.

> Extremely simple example!

```c
// 'void' function that will display a horizontal rule
void display_rule(int num_of_chars) {
  printf("\n");

  // iterate through the number of characters
  for (int i = 0; i < num_of_chars; i++) {
    printf("-");
  }

  printf("\n\n");
}
```

### Nevertheless, They Are Powerful!

Consider this simple Python code below:

```python
# explanatory function that will return multiple values
def return_multiple_vals(a, b):
    return a, b, [1, a, b, 4], {1, a, b, 4}


# our main function
def main():
    # call the function that returns multiple values into specific variables
    num_1, num_2, int_list, int_set = return_multiple_vals(2, 3)

    # display the variables
    print(f"\nnum_1 = {num_1}")
    print(f"num_2 = {num_2}")
    print(f"int_list = {int_list}")
    print(f"int_set = {int_set}\n")


# source the main function
if __name__ == "__main__":
    main()
```

If we go ahead and run this simple little program... You are going to see that we have the following **variables** *populated* like so:

```console
num_1 = 2
num_2 = 3
int_list = [1, 2, 3, 4]
int_set = {1, 2, 3, 4}
```

> [!BUG] This Is **NOT** Possible in C!!!
>

You heard it. This is <strong> <span style="color: red;"> not</span> </strong> possible in C!

In order to be able to `return` **multiple** values in C... There are 2 main ways ( *of what I currently know of* ) to "*return*" multiple values to "*`main`*". And they are using:

- C Structures $\Rightarrow$ `struct`s
- C Pointers and Addresses

> [!INFO]
> I will be covering then in more detail later on whereby I will be making specific notes for these!
>
> > [!NOTE] But Yeah
> > To `return` **multiple** variables in C, we need to use the `void` function!
>

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!