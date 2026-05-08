---
id: C - Static Arrays
aliases: Static Arrays in C
tags:
  - C
  - data-structures
  - arrays
author: S.Sunhaloo
date: 2025-09-03
status: In-Progress
---

> [!INFO]
> I am going to try to **not** *write* as much as I used to and explain every single tiny detail!
>
> I will now only try to explain the thing that I need to explain ( *for example, things that I am not understanding* ) and focus on myself instead of making documentation notes for **everyone**.
>
> Even if I **share** these notes to people... I think the majority, will **not** be reading *every* single line and just <strong> <span style="color: orange;"> read the fucking code itself</span> </strong> !
>
> > This is how I am going to try to combat my [OCD](https://en.wikipedia.org/wiki/Obsessive%E2%80%93compulsive_disorder)!

## List of Contents

- [[#Learning Setup]]
- [[#Creation of Arrays]]
- [[#Displaying Arrays In C]]
	- [[#Displaying One Dimensional Arrays]]
	- [[#Displaying Multi Dimensional Arrays]]

---

# Arrays...

Yes, we talking about **arrays** here and <strong> <span style="color: orange;"> not</span> </strong> about *lists* or even *array lists* here!

By definition, we all know that an array can contains **only** 1 *type* of data.

This means that we are **not** going to be able to do something like this ( *from [[Python - Lists#Creation of Lists | Python]]* ):

```python
# list containing most data types
general_list = [
	44,
	5.5,
	"A",
	"Something",
	True,
	2 + 5j,
	None,
	[1, 2, 3],
	(4, 5, 6),
	{7, 8, 9},
	{"x": "nice", "y": "not nice"},
]
```

> Though we do have `malloc`!

# Learning Setup

As you know this is C... This means that we are going to have do to **everything** by ourselves. Therefore, I am going to create a *header file* and also `.c` file ( *for that header file* ) so that we can easily code and use **helper functions**!

> This is how my current directory structure looks like:

```console
 .
├──  helpers
│   ├──  helper_funcs.c
│   └──  helper_funcs.h
├──  main.c
└──  Makefile
```

- Current Contents of `helpers/helper_funcs.h` Header File:

```c
#ifndef HELPER_FUNCS_H
#define HELPER_FUNCS_H

/*
  INFO: again the following functions found below... the implementation is found
  inside the file: helper_funcs.c

  we are just making the compiler know that these functions does exists
*/

// include our standard input output library
#include <stdlib.h>

// define macro to find the length of any one dimensional array
#define LEN(arr) (sizeof(arr) / sizeof(arr[0]))

// "visual" function that is going to help us to display a horizontal rule
void display_rule(int num_of_chars);

// function that will help us to display integer array
void display_int_arr(int arr[], int size_arr);
// function that will help us to display float array
void display_float_arr(float arr[], int size_arr);
// function that will help us to display char array
void display_char_arr(char arr[], int size_arr);

#endif
```

- Current Contents of `helpers/helper_funcs.c` File:

```c
// include the header file that we just created
#include "helper_funcs.h"

// our standard I/O library
#include <stdio.h>

// visual function that will help us to draw a horizontal rule
void display_rule(int num_of_chars) {
  printf("\n");

  // iterate through the number of characters
  for (int i = 0; i < num_of_chars; i++) {
    // display the character on a single line
    printf("-");
  }

  printf("\n");
}

// function that will allow us to display an integer array of "any" size
void display_int_arr(int arr[], int size_arr) {
  // iterate through the length of the array
  for (int i = 0; i < size_arr; i++) {
    // dipslay the data at each index
    printf("Index: %d --> Value: %d\n", i, arr[i]);
  }
}

// function that will allow us to display a 'float' array of "any" size
void display_float_arr(float arr[], int size_arr) {
  // iterate through the length of the array
  for (int i = 0; i < size_arr; i++) {
    // dipslay the data at each index
    printf("Index: %d --> Value: %f\n", i, arr[i]);
  }
}

// function that will allow us to display a 'char' array of "any" size
void display_char_arr(char arr[], int size_arr) {
  // iterate through the length of the array
  for (int i = 0; i < size_arr; i++) {
    // dipslay the data at each index
    printf("Index: %d --> Value: %c\n", i, arr[i]);
  }
}
```

- My `main.c` File:

```c
// include the helper function that we defined and implemented
#include "helpers/helper_funcs.h"
#include <stdio.h>

// our main function
int main() {
  printf("\nHello World\n");

  return 0;
}
```

- My `Makefile` File:

```makefile
program:
	@rm -rf program
	@gcc main.c helpers/helper_funcs.c -Wall -Wextra -o program
	@echo
	@./program

compile:
	@gcc main.c -o program

clean:
	@rm -rf program
```

# Creation of Arrays

- The following code block below is going to show us how to create simple **one dimensional** arrays:

```c
  // declare and initialise array of integer
  int int_arr[5] = {1, 2, 3, 4, 5};

  // declare and initialise array of float
  float float_arr[5] = {0.001, .0002, 50.50, 69.6969, 0.0};

  // declare and initialise array of character
  char char_arr[5] = {'F', 'U', 'C', 'K', '!'};

  /*
  INFO: Array Of Characters!

  As string cannot be represented in memory "simply"... Therefore, we need to
  make an array of characters to be able to represent a string in C.
  */
  // create array of characters with "no" size limit
  char string[] = "This is how you make a string in C!!!";

  // create array of characters with size limit
  char greet[6] = "Hello";
 
  // create an array of string ==> array of characters of array of characters
  char strings[4][7] = {"The", "World", "Is", "Fucked"};
```

> [!INFO] Null Terminator and Newline Character
> When asking for "*character(s)*" user inputs... I would rather make the size of the *buffer* / **array of characters** 2 more than the required input.
>
> As you know if the use enters something like `Hello`... The array that holds this *string* is going to look something like this:
>
> ```console
> greet = {'H', 'e', 'l', 'l', 'o', '\0'}
> ```
>
> > This is why I have also used a size of '7' ( *instead of '6'* )  for the individual '*array of characters*' in our little one dimensional array of "*strings*".
> > BTW this is **not** a joke... If you are going to make an *string*, better to **not** define the length / size of the array of characters!

- In the following code block you are going to see me create some **multidimensional** arrays:

```c
// declare and initialise multi-dimensional array of integer
int int_marr[3][3] = {
  {1, 2, 3},
  {4, 5, 6},
  {7, 8, 9},
};

// declare and initialise multi-dimensional array of float
float float_marr[2][5] = {{1.1, 2.2}, {3.3, 4.4, 5.5, 6.9}};

// declare and initialise multi-dimensional array of character
char char_marr[3][4] = {{'A', 'B'}, {'C'}, {'X', 'Y'}};

// create an array of string ==> array of characters of array of characters
char strings[2][3][10] = {{"Hello", "World", "C"}, {"Shits", "Fun"}};

// having fun with a little bit of three dimensional array
int int_marrs[3][3][3] = {
    {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    },
    {
        {10, 11, 12},
        {13, 14, 15},
        {16, 17, 18}
    },
    {
        {19, 20, 21},
        {22, 23, 24},
        {25, 26, 27}
    }
};
```

## Arrays Of String

The following is a little endeavour about C "*strings*" and '*arrays of characters of characters*'.

### Static Arrays Of String

- If you know that you are going to **hardcode** each strings, use this

```c
// create array of characters with size limit
char greet[6] = "Hello";

// create one dimensional array of strings
char char_arr[6][12] = {"one", "dimensional", "array", "of", "size", "5"};

// create two dimensional array of strings
char char_marr[3][3][12] = {
  {"two", "dimensional"},
  {"array", "of"},
  {"size", "3 by 3", "nice"},
};
```

> [!NOTE] Array Of String In Memory
> In this case, as we have **hardcoded** the *lengths* of these arrays.
>
> C is going to create space of them in **memory** ( *or program's address space* ) for these.
>
> For example, if we take a look at the **two dimensional** array. We can see that I did **not** fill every *individual* **one dimensional** array completely
>
> > I only filled the `char_marr[2]` completely.
>
> But in memory **all** of them are <strong> <span style="color: orange;"> filled</span> </strong> . This is because, for **any** dimensional array of *string*, it fills the *empty* spaces with the `\0` or **null character**!
>
> > Therefore, we can use **pointers** instead!

### "Dynamic" Arrays Of String

- This basically is a better *string array* as we are using **pointers**

```c
// create array of characters with no size limit
char *greet = "Hello";

// create array of characters with "no" size limit
char *string = "This is how you make a string in C!!!";

// create one dimensional array of strings
char *char_arr[6] = {"In this case", "the",      "strings can be",
				   "of",           "any size", "!!!"};

// create two dimensional array of strings
char *char_marr[3][3] = {
  {"Here also", "the strings in here"},
  {"can", "be"},
  {"Of", "any size", "more nicer"},
};
```

> [!NOTE]
> The line `char *greet = "Hello"` is the same doing `char greet[] = "Hello"`!
> 
> > Passing by reference!

Compared to the "*static*" version. Here, we are creating **pointers** that is going to *point* to each of the **strings** found "*somewhere*" in memory!

> This does actually seems to be better!

---

# Displaying Arrays In C

## Displaying One Dimensional Arrays

- This is the function that we *implemented* in our `helper_funcs.c` file:

```c
// function that will allow us to display an integer array of "any" size
void display_int_arr(int arr[], int size_arr) {
  // iterate through the length of the array
  for (int i = 0; i < size_arr; i++) {
    // dipslay the data at each index
    printf("Index: %d --> Value: %d\n", i, arr[i]);
  }
}
```

> Where `size_arr` is the `#define LEN(arr) (sizeof(arr) / sizeof(arr[0]))` **macro** that we defined in `helper_funcs.h` file!

- Therefore, to display our *integer* array in our `main.c` file:

> I am just going to call the function, *in this case*!

```c
 // include the helper function that we defined and implemented
#include "helpers/helper_funcs.h"
#include <stdio.h>

// our main function
int main() {
  // declare and initialise array of integers
  int int_arr[5] = {1, 2, 3, 4, 5};

  // call the required function to display the integer array
  display_int_arr(int_arr, LEN(int_arr));

  return 0;
}
```

- Therefore, this is what I get as output:

```console
Index: 0 --> Value: 1
Index: 1 --> Value: 2
Index: 2 --> Value: 3
Index: 3 --> Value: 4
Index: 4 --> Value: 5
```

## Displaying Multi Dimensional Arrays

I **don't** have any functions in my `helper_funcs.h` and `helper_funcs.c` files to **display** a *two dimensional* array!

Therefore, let's go ahead and write the function in those "*helper*" files so that we can use them later on.

- **Declare** the function in the `helper_funcs.h`:

> Additionally, add the `COLS` macro to the file!

```c
// define macro to find the length of columns for two dimensional array
#define COLS(arr) (sizeof(arr[0]) / sizeof(arr[0][0]))

// function that will help us to display two dimensional array of integers
void display_int_matrix(int rows, int cols, int matrix[rows][cols]);
```

- **Implement** the function in the `helper_funcs.c` file:

> This function is **only** going to display *two dimensional integer arrays*!

```c
// function that will allow us to display an integer matrix of any size
void display_int_matrix(int rows, int cols, int matrix[rows][cols]) {
  // iterate through the rows of the matrix
  for (int i = 0; i < rows; i++) {
    // iterate through the columns of the matrix
    for (int j = 0; j < cols; j++) {
      // display the individual elements
      printf("Index: [%d][%d] --> Value: %d\n", i, j, matrix[i][j]);
    }
  }
}
```

### Therefore In Our Main File

```c
// include the helper function that we defined and implemented
#include "helpers/helper_funcs.h"
#include <stdio.h>

// our main function
int main() {
  // declare and initialise array of integers
  int matrix[2][2] = {{1, 2}, {3, 4}};

  // call the required function to display the two dimensional array
  display_int_matrix(LEN(matrix), COLS(matrix), matrix);

  return 0;
}
```

- This is the output that I get:

```console
Index: [0][0] --> Value: 1
Index: [0][1] --> Value: 2
Index: [1][0] --> Value: 3
Index: [1][1] --> Value: 4
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!
