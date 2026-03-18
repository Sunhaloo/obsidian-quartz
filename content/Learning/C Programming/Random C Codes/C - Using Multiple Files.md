---
id: C - Using Multiple Files
aliases: C - Importing and Using Multiple Files
tags:
  - C
  - files
author: S.Sunhaloo
date: 2025-09-04
status: Completed
---

## List of Contents

- [[#Single File]]
- [[#Splitting Into Multiple Files]]
	- [[#Creation of Header File]]
	- [[#Implementation of Helper Functions]]
	- [[#How To Import Multiple Files]]

---

> [!INFO] Resources
> - https://en.wikipedia.org/wiki/C_preprocessor
> - https://en.wikipedia.org/wiki/Include_guard

# Single File

Let's say that we have the following `main.c` file.

```c
#include <ctype.h>
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// define the macro to find the length of array
#define LEN(arr) (sizeof(arr) / sizeof(arr[0]))

// function that is going to display integer arrays
void display_int_arr(int arr[], int arr_length) {
  // iterate through the length of the array
  for (int i = 0; i < arr_length; i++) {
    printf("Index[%d]: %d\n", i, arr[i]);
  }
}

// function that is going to display the fullname of user
void display_names(char first_name[], char last_name[], int last_name_len) {
  // access the first character of the `first_name` variable and capitalise
  first_name[0] = toupper(first_name[0]);

  // iterate through the length of `last_name`
  for (int i = 0; i < last_name_len; i++) {
    // 'capitalise' each individual character in place
    last_name[i] = toupper(last_name[i]);
  }

  // display the full name of the user
  printf("\nUser's Full Name: %s %s\n", last_name, first_name);
}

// function to generate random telephone numbers
void gen_display_tels(int num_of_tels) {
  // set the seed for the random numbers
  srand(time(NULL));

  // iterate through the number of telephone numbers to be generated
  for (int i = 0; i < num_of_tels; i++) {
    // add the correct country code
    printf("+230 5");
    // iterate 7 times to generate some random numbers
    for (int j = 0; j < 7; j++) {
      // generate the random number from 0 to 9
      int rand_num = rand() % 10;

      printf("%d", rand_num);
    }

    // change the caret's position
    printf("\n");
  }
}

// function that will ask the user to enter a positive integer number
int enter_pos_num() {
  // declare variable that is going to hold the user's positive intege
  int user_int;

  // iterate through the `while` loop indefinitely
  while (1) {
    // ask the user to enter a positive integer number
    printf("\nPlease Enter A Positive Integer Number: ");
    scanf("%d", &user_int);

    // check if the input is invalide ==> negative integer number entered
    if (user_int < 0) {
      // output appropriate message
      printf("\n\t<< Please Enter Positive Integer Numbers Only!!! > > \n");

      // continue to ask the user to enter a positive integer number
      continue;
    }

    // if the user's input is valid ==> exit the `while` loop
    break;
  }

  // return user's positive integer input to the "main" function
  return user_int;
}

// our main function
int main() {
  // declare and initialise integer array
  int arr[5] = {1, 2, 3, 4, 5};

  // find the length of the integer array created
  printf("\nLength of Integer Array: %ld\n", LEN(arr));

  // call the function to display the element inside our integer array
  display_int_arr(arr, LEN(arr));

  // declare array of characters to keep user's name
  char f_name[] = "joe";
  char l_name[] = "mama";

  // call the function to display the user's full name
  display_names(f_name, l_name, LEN(l_name));

  // call the function to generate some random telephone numbers
  gen_display_tels(10);

  // declare variable that is going to hold the user's positive integer number
  int user_pos_num = enter_pos_num();

  // display that positive integer number entered
  printf("\n\t-- Positive Number Entered = %d --\n", user_pos_num);

  return 0;
}
```

As you can see writing C code can get pretty long ( *that's what she said* )! Therefore, I think its better for us to write "*helper*" files so that we can place these **helper functions** in another place and keep our `main.c` file clean and tidy!

# Splitting Into Multiple Files

## Creation of Header File

Now, dues to the way that C's '*preprocessor*' works. We must **first** create the *header* file for our "*helper*" functions.

> Basically the **program** ( *standalone or part of compiler* ) that's the one to **read** all of our files!

Therefore, we <strong> <span style="color: red;"> cannot</span> </strong> simply `include` or `import` our C files **directly** like we can in Python.

Additionally, C is a **declarative** language and therefore, we must first **declare** all the things that we are going to create **before** actually *implementing* / *coding* them.

### Creation Of Header File

- This is how my `void_helpers.h` file looks like:

```c
#ifndef VOID_HELPER_H
#define VOID_HELPER_H

// include these headers files so that these function can use them
// # NOTE: for safety's sake... at least include the standard library
#include <ctype.h>
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// define function prototype for `display_int_arr`
void display_int_arr(int arr[], int arr_length);

// define function prototype for `display_names`
void display_names(char first_name[], char last_name[], int last_name_len);

// define function prototype for `gen_display_tels`
void gen_display_tels(int num_of_tels);

#endif
```

- This is how my `function_helpers.h` file looks like:

```c
#ifndef FUNCTION_HELPER_H
#define FUNCTION_HELPER_H

// include these headers files so that these function can use them
// # NOTE: for safety's sake... at least include the standard library
#include <ctype.h>
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// define the macro to find the length of array
#define LEN(arr) (sizeof(arr) / sizeof(arr[0]))

// define function prototype for `enter_pos_num`
int enter_pos_num();

#endif
```

## Implementation of Helper Functions

In the above *header files*, we only **defined** the function prototypes... Hence, we still need to implement the above functions.

- Implementation of functions found in `void_helper.c`:

```c
#include "void_helper.h"
#include <stdio.h>

// function that is going to display integer arrays
void display_int_arr(int arr[], int arr_length) {
  // iterate through the length of the array
  for (int i = 0; i < arr_length; i++) {
    printf("Index[%d]: %d\n", i, arr[i]);
  }
}

// function that is going to display the fullname of user
void display_names(char first_name[], char last_name[], int last_name_len) {
  // access the first character of the `first_name` variable and capitalise
  first_name[0] = toupper(first_name[0]);

  // iterate through the length of `last_name`
  for (int i = 0; i < last_name_len; i++) {
    // 'capitalise' each individual character in place
    last_name[i] = toupper(last_name[i]);
  }

  // display the full name of the user
  printf("\nUser's Full Name: %s %s\n", last_name, first_name);
}

// function to generate random telephone numbers
void gen_display_tels(int num_of_tels) {
  // set the seed for the random numbers
  srand(time(NULL));

  // iterate through the number of telephone numbers to be generated
  for (int i = 0; i < num_of_tels; i++) {
    // add the correct country code
    printf("+230 5");
    // iterate 7 times to generate some random numbers
    for (int j = 0; j < 7; j++) {
      // generate the random number from 0 to 9
      int rand_num = rand() % 10;

      printf("%d", rand_num);
    }

    // change the caret's position
    printf("\n");
  }
}
```

- Implementation of functions found in `function_helper.c`:

```c
#include "function_helper.h"
#include <stdio.h>

// function that will ask the user to enter a positive integer number
int enter_pos_num() {
  // declare variable that is going to hold the user's positive intege rnumber
  int user_int;

  // iterate through the `while` loop indefinitely
  while (1) {
    // ask the user to enter a positive integer number
    printf("\nPlease Enter A Positive Integer Number: ");
    scanf("%d", &user_int);

    // check if the input is invalide ==> negative integer number entered
    if (user_int < 0) {
      // output appropriate message
      printf("\n\t<< Please Enter Positive Integer Numbers Only!!! > > \n");

      // continue to ask the user to enter a positive integer number
      continue;
    }

    // if the user's input is valid ==> exit the `while` loop
    break;
  }

  // return user's positive integer input to the "main" function
  return user_int;
}
```

## How To Import Other Files Into Main File

You see... We can **only** import the *header* files into our `main.c` file. Again this is due to how the '*preprocessor*' works.

Therefore, if you want to `include` and use these function that we created we simply need to add the `"void_helper.h"` and `"function_helper.h` files like so:

> The code below if the *final* modified code to show the **usage** of multiple files in C!

```c
#include "function_helper.h"
#include "void_helper.h"
#include <stdio.h>

// INFO: see how we don't have to include the previously required header files

// our main function
int main() {
  // declare and initialise integer array
  int arr[5] = {1, 2, 3, 4, 5};

  // find the length of the integer array created
  printf("\nLength of Integer Array: %ld\n", LEN(arr));

  // call the function to display the element inside our integer array
  display_int_arr(arr, LEN(arr));

  // declare array of characters to keep user's name
  char f_name[] = "joe";
  char l_name[] = "mama";

  // call the function to display the user's full name
  display_names(f_name, l_name, LEN(l_name));

  // call the function to generate some random telephone numbers
  gen_display_tels(10);

  // declare variable that is going to hold the user's positive integer number
  int user_pos_num = enter_pos_num();

  // display that positive integer number entered
  printf("\n\t-- Positive Number Entered = %d --\n", user_pos_num);

  return 0;
}
```

### How To Compile

Currently, if we go ahead and run our little `gcc` command like so:

```bash
# compile our updated `main.c` file
gcc main.c -o main
```

- This is the output that we get:

```console
/usr/sbin/ld: /tmp/cc8CrfeQ.o: in function `main':
test.c:(.text+0x60): undefined reference to `display_int_arr'
/usr/sbin/ld: main.c:(.text+0x8a): undefined reference to `display_names'
/usr/sbin/ld: main.c:(.text+0x94): undefined reference to `gen_display_tels'
/usr/sbin/ld: main.c:(.text+0x99): undefined reference to `enter_pos_num'
collect2: error: ld returned 1 exit status
```

> [!WARNING] As You Can See Errors!!!
> This is because the compiler does **not** currently know where the `void_helper.h` and `function_helper.h` is and what they actually are!
>
> Therefore we need to **update** our `gcc` compilation command to include their *associated* `.c` files

> [!SUCCESS]
> Hence, do also compile the required `.c` files:
>
> ```bash
> # compile the updated `main.c` file by adding "other" `.c` files
> gcc main.c void_helper.c function_helper.c -o program
> ```
>
> Thus, we have finally been able to learn how to *split* our `main.c` files into multiple ones!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!