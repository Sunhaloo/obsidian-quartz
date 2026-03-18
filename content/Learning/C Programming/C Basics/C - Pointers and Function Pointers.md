---
id: C - Pointers and Function Pointers
aliases: Pointers and Function Pointers in C
tags:
  - C
  - basics
author: S.Sunhaloo
date: 2026-02-06
status: Completed
---

## List of Contents

- [[#Memory Address]]
	- [[#Passing By Value v/s Passing By Reference]]
	- [[#Example: Passing By Value]]
	- [[#Example: Passing By Reference]]
- [[#Using Pointers In C]]
	- [[#Type Casting - Dereferencing Pointers]]
		- [[#Cast Then Dereference]]
		- [[#Dereference Then Cast]]
	- [[#A Little Debate]]
- [[#Creating Pointers Of Pointers]]
- [[#Function Pointers]]

---

> [!NOTE]
> This note is basically inspired by these YouTube videos:
> - C Pointers: https://www.youtube.com/watch?v=2GDiXG5RfNE
> - C Function Pointers: https://www.youtube.com/watch?v=f_uWOWViYc0

---

## Our Makefile!

> [!NOTE] Before we get started with the learning about pointers and function pointers...
> 
> So the `Makefile` that I used for this "*learning session*" was like so:
> 
> ```makefile
> program: compile run clean
> 
> compile:
>	 @gcc main.c -Wall -Wextra -o program
>
> run:
> 	@./program
>
> clean:
> 	@rm program
> ```
> 
> In this case, if I just run the `make` command, the `main.c` file would get:
> 
> - Compile and the `program` file was created
> - The `program` file would run
> - Then the `program` file would be deleted leaving no binaries behind
> 
> > Ensuring that the `program` is always new!

# Memory Address

> [That's it you can stop reading!](https://www.youtube.com/watch?v=vyNqvjOdTi0) 

When we talk about **pointers** we are generally speaking about *memory*.

> Whereby the "*memory*" is your RAM!

When we run our program like `./a.out` or `./program`... Space is created in our RAM for that program to run.

> That *place* is called the '[stack](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)#Compile-time_memory_management)'!

This is basically where all the **variables** are stored in memory for our running program.

What I am trying to say its that all **variables** be it `int` or `double[]` or even a *function* has a memory address in RAM.

> [!NOTE] But how is that useful to us?
> If you been programming or paying attention in school. You might have come across the term '*Passing by value*' and '*Passing by reference*'.

## Passing By Value v/s Passing By Reference

> Yes! some actual coding...

Let's take a really simple example to showcase 'passing by value' v/s 'passing by reference'.

We are going to be making a simple `swap_int_numbers` function that will swap 2 numbers!

### Example: Passing By Value

```C
#include <stdio.h>

// function to swap the 2 numbers
// INFO: this is an example of passing by value
void swap_int_numbers(int num1, int num2) {
  // swap the 2 numbers using temporary buffer
  int temp = num1;
  num1 = num2;
  num2 = temp;

  printf("\n( In Function ) Number 1 `x`: %d\n", num1);
  printf("( In Function ) Number 2 `y`: %d\n", num2);
}

// our main little function
int main(int argc, char *argv[]) {
  // declare the 2 numbers to swap with
  int x = 0;
  int y = 1;

  printf("( Before Swapping ) `x`: %d\n", x);
  printf("( Before Swapping ) `y`: %d\n", y);

  // call the function and pass variables by values
  swap_int_numbers(x, y);

  printf("\n( After Swapping ) `x`: %d\n", x);
  printf("( After Swapping ) `y`: %d\n", y);

  return 0;
}
```

- The output of passing by **value**:

```console
( Before Swapping ) `x`: 0
( Before Swapping ) `y`: 1

( In Function ) Number 1 `x`: 1
( In Function ) Number 2 `y`: 0

( After Swapping ) `x`: 0
( After Swapping ) `y`: 1
```

> [!BUG] The values have **not** been swapped!!!
> 
> You’ll notice that simply passing `x` and `y` into `swap_int_numbers` doesn't actually change them in our `main` function.
> 
> > Wait, but didn't they swap inside the function?
> 
> Yes, they did! Here’s why: when we pass `x` and `y` as _arguments_, the program creates two brand-new variables, `num1` and `num2`, specifically for that function.
> 
> Think of it this way: when the function is called, it lives on the **stack**. The program allocates fresh memory for `num1` and `num2` and simply copies the _values_ of `x` and `y` into them. The function successfully swaps these local copies, but as soon as the function finishes, that stack frame is cleared and those variables are destroyed. The original `x` and `y` back in `main` never moved an inch!

### Example: Passing By Reference

```C
#include <stdio.h>

// function to swap the 2 numbers
// INFO: this is an example of passing by value
void swap_int_numbers(int *num1, int *num2) {
  // swap the 2 numbers using temporary buffer
  int temp = *num1;
  *num1 = *num2;
  *num2 = temp;

  printf("\n( In Function ) Number 1 `x`: %d\n", *num1);
  printf("( In Function ) Number 2 `y`: %d\n", *num2);
}

// our main little function
int main(int argc, char *argv[]) {
  // declare the 2 numbers to swap with
  int x = 0;
  int y = 1;

  printf("( Before Swapping ) `x`: %d\n", x);
  printf("( Before Swapping ) `y`: %d\n", y);

  // call the function and pass variables by values
  swap_int_numbers(&x, &y);

  printf("\n( After Swapping ) `x`: %d\n", x);
  printf("( After Swapping ) `y`: %d\n", y);

  return 0;
}
```

- The output of passing by **value**:

```console
( Before Swapping ) `x`: 0
( Before Swapping ) `y`: 1

( In Function ) Number 1 `x`: 1
( In Function ) Number 2 `y`: 0

( After Swapping ) `x`: 1
( After Swapping ) `y`: 0
```

> [!SUCCESS]
> As you can see here we are able to actually swap the value of the variable `x` with the value of the variable `y`.
> 
> Again, this swap happened because we *passed* the **addresses** ( *actual address in memory - RAM* ) of the integer variables instead of their actual values!

# Using Pointers In C

> You are already using it with `scanf`!

Now, let's go ahead and understand how to use *simple* pointers in C. The following code block is going to guide you through the basics of pointers in C.

```C
#include <stdio.h>

// function declaration and initialisation
void some_random_func() {};

int some_random_int_func() { return 0; };

float some_random_float_func(int first_num, int second_num) {
  return first_num + second_num;
}

int main(int argc, char *argv[]) {
  // declare some variables
  int num = 69;
  float floating_num = 6.9;
  double big_floating_num = 69.69;
  char character_thingy = 'A';
  char yes_this_is_a_string[11] = "Hello World";

  // declare and initialise pointer for these specific variables
  // NOTE: each datatype can be converted into its own little pointer

  // the `&` character is one that gets the address from memory and assigns it
  int *num_ptr = &num;
  float *floating_num_ptr = &floating_num;
  double *big_floating_num_ptr = &big_floating_num;
  char *character_thingy_ptr = &character_thingy;
  char *string_ptr = yes_this_is_a_string;

  void *func_ptr = &some_random_func;
  int (*int_func_ptr)() = &some_random_int_func;
  float (*float_func_ptr)(int, int) = &some_random_float_func;

  // display the address of each pointers
  printf("\nAddress Of Pointers\n");

  printf("Value of pointer `num_ptr`: %p\n", num_ptr);
  printf("Value of pointer `floating_num_ptr`: %p\n", floating_num_ptr);
  printf("Value of pointer `big_floating_num_ptr`: %p\n", big_floating_num_ptr);
  printf("Value of pointer `character_thingy_ptr`: %p\n", character_thingy_ptr);
  printf("Value of pointer `string_ptr`: %p\n", string_ptr);
  printf("Value of pointer `func_ptr`: %p\n", func_ptr);
  printf("Value of pointer `int_func_ptr`: %p\n", int_func_ptr);
  printf("Value of pointer `float_func_ptr`: %p\n", float_func_ptr);

  // display the actual value found at the address
  printf("\nValue Found At Addresses Of Pointers\n");

  // dereferencing "directly"
  printf("Value found at pointer `num_ptr`: %d\n", *num_ptr);

  // casting and then dereferencing
  printf("Value found at pointer `floating_num_ptr`: %0.2f\n",
         *(float *)floating_num_ptr);

  // dereferencing and then casting
  printf("Value found at pointer `big_floating_num_ptr`: %0.2lf\n",
         (double)*big_floating_num_ptr);

  printf("Value found at pointer `character_thingy_ptr`: %c\n",
         *character_thingy_ptr);

  // again no need to do anything here
  printf("Value found at pointer `string_ptr`: %s\n", string_ptr);

  // function pointers are a bit more different --> in this case void pointer
  // WARNING: because `void` is `void` ==> type casting to 'int' instead
  printf("Value found at pointer `func_ptr`: %d\n", ((int (*)())func_ptr)());

  // function pointers are a bit more different --> in this case int pointer
  // INFO: we know that an `int` pointer is going to return the 'int' datatype
  printf("Value found at pointer `int_func_ptr`: %d\n",
         ((int (*)())int_func_ptr)());

  // NOTE: as we need to get the "value", we need to actually "use" the function
  printf("Value found at pointer `float_func_ptr`: %0.2f\n",
         ((float (*)(int, int))float_func_ptr)(10, 10));

  return 0;
}
```

- The output of the above code will look something like this:

```console

Address Of Pointers
Value of pointer `num_ptr`: 0x7ffe9f49bae8
Value of pointer `floating_num_ptr`: 0x7ffe9f49baec
Value of pointer `big_floating_num_ptr`: 0x7ffe9f49baf0
Value of pointer `character_thingy_ptr`: 0x7ffe9f49bae7
Value of pointer `string_ptr`: 0x7ffe9f49bb3d
Value of pointer `func_ptr`: 0x55fd710b7159
Value of pointer `int_func_ptr`: 0x55fd710b7160
Value of pointer `float_func_ptr`: 0x55fd710b716b

Value Found At Addresses Of Pointers
Value found at pointer `num_ptr`: 69
Value found at pointer `floating_num_ptr`: 6.90
Value found at pointer `big_floating_num_ptr`: 69.69
Value found at pointer `character_thingy_ptr`: A
Value found at pointer `string_ptr`: Hello World
Value found at pointer `func_ptr`: 1896575321
Value found at pointer `int_func_ptr`: 0
Value found at pointer `float_func_ptr`: 20.00
```

In the above code we are **creating** pointers and **displaying** the actual memory addresses of these pointers. After that, we are dereferencing all of the above created pointer so display the **actual data** found inside of the memory address.

> [!NOTE] [[C Language Basics#Type Cast | Type Casting]] Resources
> - stackoverflow links:
> 	- https://stackoverflow.com/questions/4634252/in-c-if-i-cast-dereference-a-pointer-does-it-matter-which-one-i-do-first
> 	- https://stackoverflow.com/questions/51364499/pointer-type-casting-and-dereferencing
>
> > It's always the type casting syntax that's get me confused!

## Type Casting - Dereferencing Pointers

> I am going to be re-using the above code to create examples below!

So there are 2 ways to do that; we can either:

1. Cast First, then dereference
2. Dereference First, then cast

> [!NOTE]
> The first one is considered to be more *standard* way to get the actual value from a memory address.

> [!WARNING] What is the actual difference between the two?
> - Casting **first** and then dereferencing ( *the "standard" way* ) means that:
> 	1. Go to the address / ( *actual* ) pointer
> 	2. Cast *that* memory address / **pointer** into the proper datatype that we need
> 	3. Then the *outer* `*` character **dereferences** all of that to get the actual value!
> 
> > Use this when you just want to get the actual value from the address of the pointer **without** the need to convert it!
> 
> - Dereferencing **first** and then casting
> 	1. Go to the address / ( *actual* ) pointer
> 	2. Get the actual value found at *that* memory address / **pointer**
> 	3. Then the *outer* `(<insert_dataype_here>)` will convert the data found **in** pointer to another *format*
> 
> > Use this when you actually want to change the *datatype* of the value found **inside** the pointer!
> 
> > [!TIP]
> > - The first method ( *Cast --> Dereference* ) are a **reinterpretation** and is used to handle `void *` pointer in functions / data structures
> > - The second method ( *Dereference --> Cast* ) are **conversion** and is convert data at pointer to other datatype

## Cast Then Dereference

The following code block will show examples of *casting* and **then** *dereferencing*.

```C
// casting and then dereferencing the pointers syntax
// NOTE: see how our format specifiers are correctly "placed" to hold the actual datatype
printf("Value found at pointer `num_ptr`: %d\n", *(int *)num_ptr);

printf("Value found at pointer `floating_num_ptr`: %0.2f\n",
       *(float *)floating_num_ptr);
```

The above code is going to correctly display the data found inside the pointers!

```console
Value found at pointer `num_ptr`: 69
Value found at pointer `floating_num_ptr`: 6.90
```

> [!BUG] 'Casting Then Dereferencing' **Conversion** / **Type Casting** Error!
> 
> What is if we try **changing** the *datatype* when we are using this *method*?
> 
> ```C
> // casting and then dereferencing the pointers
> // NOTE: here we are trying to actually convert the pointer itself
> printf("Memory at `num_ptr` read as `float`: %f\n", *(float *)num_ptr);
> 
> printf("Memory at `floating_num_ptr` read as `int`: %d\n",
>        *(int *)floating_num_ptr);
> ```
> 
> - This is actually going to return "*nothing*"!
> 
> ```console
> Memory at `num_ptr` read as `float`: 0.000000
> Memory at `floating_num_ptr` read as `int`: 1088212173
> ```
> 
> > This is what we mean above when we are saying "*reinterpretation*" of bits!

## Dereference Then Cast

The following code block will show examples of *dereferencing* and **then** *casting*.

```C
// dereferencing and then casting the pointers syntax
// NOTE: here also we are keeping the format specificers the same as the actual datatype being held
printf("Value found at pointer `num_ptr`: %d\n", (int)*num_ptr);

printf("Value found at pointer `floating_num_ptr`: %0.2f\n",
         (float)*floating_num_ptr);
```

Therefore, we should see that we can correctly output the data found at those addresses!

```console
Value found at pointer `num_ptr`: 69
Value found at pointer `floating_num_ptr`: 6.90
```

> [!SUCCESS] We can actually *Type Cast* here!
> 
> Compared to the above ( *i.e 'Casting Then Dereferencing'* ), we can actually do that here!
> 
> ```C
> // dereferencing and then casting the pointers
> // NOTE: instead of trying to convert the pointer, we convert the actual data found in pointer!
> // it does make a huge difference!
> printf("Memory at `num_ptr` read as `float`: %f\n", (float)*num_ptr);
> printf("Memory at `floating_num_ptr` read as `int`: %d\n",
>        (int)*floating_num_ptr);
> ```
> 
> Therefore, we should see that our datatypes have been correctly converted.
> 
> ```console
> Memory at `num_ptr` read as `float`: 69.000000
> Memory at `floating_num_ptr` read as `int`: 6
> ```

## A Little Debate

> How to we *write* pointers? Do we write like this: `<datatype> *ptr` or this: `<datatype>* ptr`?

This is one of the never ending debates that... Well is *never* going to end!

### My Opinion, My Reasoning Compared To The Others!

- I like and will always use the following way:

```C
int *num_ptr = &num;
float *floating_num_ptr = &floating_num;
double *big_floating_num_ptr = &big_floating_num;
char *character_thingy_ptr = &character_thingy;
char *string_ptr = yes_this_is_a_string;

void *func_ptr = &some_random_func;
int (*int_func_ptr)() = &some_random_int_func;
float (*float_func_ptr)(int, int) = &some_random_float_func;
```

> [!NOTE] My Reasoning Of The Above Pointer Declaration Syntax
> Let's say that I create something like `int *num_ptr;` ( *like we did above* ). For me personally I read it like this:
> 
> > The `num_ptr` variable *points* to the *address* of an **integer** variable!
> 
> > [!SUCCESS] C's Standard
> > Yes, *my* way of writing it, unknowingly is C's standard way of *writing* / declaring pointers!
> > 
> > We associate the `*` character which is the "*dereferencing*" part to the actual value found inside that address that the pointer points to.

But there are people that strongly agrees to declaring pointers like so:

```C
// INFO: see how they associate the `*` characters to the datatype!
int* num_ptr = &num;
float* floating_num_ptr = &floating_num;
char* character_thingy_ptr = &character_thingy;
```

> [!NOTE] Their Reasoning!
> They say it like that:
> 
> > "*The pointer is a pointer to a specific datatype*"
> 
> Compared to **my** way of saying:
>
> > "*The pointer is a 'pointer' that points to this datatype*"

> [!SUCCESS] Use what you are currently using!
> 
> The difference is subtle but it's about **emphasis**:
> - `int* ptr` emphasises the **type**: "*`ptr` has type pointer-to-int*"
> - `int *ptr` emphasises the **relationship**: "*`ptr` is a pointer that happens to point to int*"

### But What Should We Use?

> "*Use what you are currently using*" I did say that right? Right?

Well let me show you how **_my_ way** is far, far **superior**! Why is it superior you ask? Because its my fucking way and you should listen to me!

> I am joking BTW!

No, for real, I think the way that I do it is better, because of the code block below:

```C
#include <stdio.h>

int main(int argc, char *argv[]) {
  // NOTE: declaring some pointers using "their" way ( associate `*` to datatype )
  int* int_pointer1, int_pointer2;
  float* float_pointer1, float_pointer2;
  char* char_pointer1, char_pointer2;

  // display the size of each pointers
  printf("\nSize Of Pointers\n");

  printf("Size of pointer `int_pointer1`: %ld\n", sizeof(int_pointer1));
  printf("Size of pointer `int_pointer2`: %ld\n", sizeof(int_pointer2));
  printf("Size of pointer `float_pointer1`: %ld\n", sizeof(float_pointer1));
  printf("Size of pointer `float_pointer2`: %ld\n", sizeof(float_pointer2));
  printf("Size of pointer `char_pointer1`: %ld\n", sizeof(char_pointer1));
  printf("Size of pointer `char_pointer2`: %ld\n", sizeof(char_pointer2));

  return 0;
}
```

Okay, I was asking [Gemini](https://gemini.google.com) ( *BTW Claude is the best!* ) as is there a **size** difference between a *simple* datatype to a *pointer* datatype.

And yes, there is! We know that "*simple*" variables has predefined sizes regardless of your architecture. By "*architecture*", I mean your actual hardware that you are running your C program on.

Pointers are **different**! They are based on your system! For example a modern, 64-bit system will return should return '8' for the size of a *pointer* variable.

> Now that we know that little thing; let's get back to our code above!

In the above code we declared two **pointers** therefore, given that I am on "*modern*" system with the 64-bit architecture, I should see that for both of these *variables*, I should get the value of '8'!

- Here is the output after running the above program:

```console

Size Of Pointers
Size of pointer `int_pointer1`: 8
Size of pointer `int_pointer2`: 4
Size of pointer `float_pointer1`: 8
Size of pointer `float_pointer2`: 4
Size of pointer `char_pointer1`: 8
Size of pointer `char_pointer2`: 1
```

> [!BUG] Yes, the second *pointers* are **not** pointers!
> 
> To be completely honest with you, I don't really know why it does that... I would need to actually ask someone that is more knowledgeable in this topic / debate that I am to found out for myself!
> 
> > [!TIP] The Fix?
> > 
> > Just simply declare variables and pointers on different lines each time! Problem solved!
> > 
> > > I mean already do the above *tip*. But I like "*my*" way of writing pointers because I feel its much more cleaner.

# Creating Pointers Of Pointers

The code block below is going to show you how to create **pointers of pointers**.

```C
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[]) {
  // declare and initialise integer variable
  int num = 5;

  // declare and intialise array of characters
  char word[] = "Hello World";

  // create a pointer that points to the value of integer variable
  int *first_int_pointer = &num;

  // create pointers of pointer ( integer )
  int **second_int_pointer = &first_int_pointer;
  int ***third_int_pointer = &second_int_pointer;

  // create a pointer that points to the value of "string" variable
  char *first_str_pointer = word;

  // create pointers of pointer ( array of characters )
  char **second_str_pointer = &first_str_pointer;
  char ***third_str_pointer = &second_str_pointer;

  // display the data found in the integer and 'array' variables before changing
  printf("\nDisplay Variables ( Before Data Manipulation )\n");

  printf("Value of `num`: %d\n", num);
  printf("Value of pointer `first_int_pointer`: %p\n", first_int_pointer);
  printf("Value of pointer `second_int_pointer`: %p\n", second_int_pointer);
  printf("Value of pointer `third_int_pointer`: %p\n", third_int_pointer);

  printf("Value of pointer `word`: %s\n", word);
  printf("Value of pointer `first_str_pointer`: %p\n", first_str_pointer);
  printf("Value of pointer `second_str_pointer`: %p\n", second_str_pointer);
  printf("Value of pointer `third_str_pointer`: %p\n", third_str_pointer);

  // change the data of variable using third pointer
  ***third_int_pointer = 10;
  strcpy(**third_str_pointer, "Very Nice");

  // WARNING: why use `strcpy`
  // this is due to the fact that `***third_str_pointer` pointers holds the data
  // 'H', like the actual character therefore, using `**third_str_pointer` as
  // first argument the the actual word as second arguement inside the `strcpy`
  // function is going to actually change our data inside

  printf("\nDisplay Variables ( After Data Manipulation )\n");

  printf("Value of `num`: %d\n", num);
  printf("Value of pointer `first_int_pointer`: %p\n", first_int_pointer);
  printf("Value of pointer `second_int_pointer`: %p\n", second_int_pointer);
  printf("Value of pointer `third_int_pointer`: %p\n", third_int_pointer);

  printf("Value of `word`: %s\n", word);
  printf("Value of pointer `first_str_pointer`: %p\n", first_str_pointer);
  printf("Value of pointer `second_str_pointer`: %p\n", second_str_pointer);
  printf("Value of pointer `third_str_pointer`: %p\n", third_str_pointer);

  printf("\nValue Found At Addresses Of Pointers\n");

  // dereferencing directly
  printf("Value found at pointer `third_int_pointer`: %d\n",
         ***third_int_pointer);

  // casting then dereferencing
  printf("Value found at pointer `third_int_pointer`: %d\n",
         *(int *)**third_int_pointer);

  // dereferencing then casting
  printf("Value found at pointer `third_int_pointer`: %d\n",
         (int)(***third_int_pointer));

  // again, because of array of character; no need to do anything here!
  printf("Value found at pointer `third_str_pointer`: %s\n",
         **third_str_pointer);

  return 0;
}
```

- Therefore running the above code block, we see that we get something like this:

```console

Display Variables ( Before Data Manipulation )
Value of `num`: 5
Value of pointer `first_int_pointer`: 0x7ffeb931b494
Value of pointer `second_int_pointer`: 0x7ffeb931b498
Value of pointer `third_int_pointer`: 0x7ffeb931b4a0
Value of pointer `word`: Hello World
Value of pointer `first_str_pointer`: 0x7ffeb931b4cc
Value of pointer `second_str_pointer`: 0x7ffeb931b4a8
Value of pointer `third_str_pointer`: 0x7ffeb931b4b0

Display Variables ( After Data Manipulation )
Value of `num`: 10
Value of pointer `first_int_pointer`: 0x7ffeb931b494
Value of pointer `second_int_pointer`: 0x7ffeb931b498
Value of pointer `third_int_pointer`: 0x7ffeb931b4a0
Value of `word`: Very Nice
Value of pointer `first_str_pointer`: 0x7ffeb931b4cc
Value of pointer `second_str_pointer`: 0x7ffeb931b4a8
Value of pointer `third_str_pointer`: 0x7ffeb931b4b0

Value Found At Addresses Of Pointers
Value found at pointer `third_int_pointer`: 10
Value found at pointer `third_int_pointer`: 10
Value found at pointer `third_int_pointer`: 10
Value found at pointer `third_str_pointer`: Very Nice
```

# Function Pointers

> A **function pointer** is a **pointer** that *points* to a **function**!

```C
#include <stdio.h>

// simple greet function
void greet() { printf("Hello World\n"); }

// function that displays and integer number of user's choice
int return_int_number(int number) { return number; }

// simple multiplication function
int multiply(int num1, int num2) { return num1 * num2; }

// simple recursive power function for integer numbers
int power_recursive_func(int base, int exponent) {
  if (exponent == 0) {
    return 1;

  } else if (exponent > 0) {
    return base * power_recursive_func(base, exponent - 1);
  } else {
    return 1 / power_recursive_func(base, exponent * -1);
  }
}

int main(int argc, char *argv[]) {
  // declare function pointers for our functions
  void (*greet_func_ptr)() = greet;
  int (*return_func_number_ptr)(int) = return_int_number;
  int (*power_recursive_func_ptr)(int, int) = power_recursive_func;
  int (*multiply_func_ptr)(int, int) = multiply;

  // declare array of pointers to hold functions
  int (*func_arrays_ptr[])(int, int) = {multiply, power_recursive_func};

  // display the address of the functions
  printf("\nAddress Of Pointers\n");

  printf("Value of pointer `greet_func_ptr`: %p\n", greet_func_ptr);
  printf("Value of pointer `return_func_number_ptr`: %p\n",
         return_func_number_ptr);
  printf("Value of pointer `power_recursive_func_ptr`: %p\n",
         power_recursive_func_ptr);
  printf("Value of pointer `multiply_func_ptr`: %p\n", multiply_func_ptr);
  printf("Value of pointer `func_arrays_ptr`: %p\n", func_arrays_ptr);

  // using function pointer `return_func_number_ptr` to run function
  int return_func_result = return_func_number_ptr(5);
  printf("\nValue of `return_func_result`: %d\n", return_func_result);

  // using array of pointer to calculate the power of a number
  int power_recursive_func_result = func_arrays_ptr[1](2, 3);

  printf("\nValue of `power_recursive_func_result`: %d\n",
         power_recursive_func_result);

  printf("\nValue Found At Address Of Pointers\n");

  printf("Value found at pointer `greet_func_ptr` ( execution of function ): ");

  // INFO: simply execute the `void` function ( without any parameter )
  (*greet_func_ptr)();

  printf("Value found at `return_func_number_ptr(10)`: %d\n",
         (*return_func_number_ptr)(10));
  printf("Value found at `multiply_func_ptr`: %d\n",
         (*multiply_func_ptr)(4, 5));
  printf("Value found at `func_arrays_ptr`: %d\n", (*func_arrays_ptr[0])(3, 3));

  return 0;
}
```

- Therefore compiling and running the above code block, we should see that we are able to get something like this:

```console
Address Of Pointers
Value of pointer `greet_func_ptr`: 0x562e4443c159
Value of pointer `return_func_number_ptr`: 0x562e4443c16f
Value of pointer `power_recursive_func_ptr`: 0x562e4443c18e
Value of pointer `multiply_func_ptr`: 0x562e4443c17b
Value of pointer `func_arrays_ptr`: 0x7ffdde9edc80

Value of `return_func_result`: 5

Value of `power_recursive_func_result`: 8

Value Found At Address Of Pointers
Value found at pointer `greet_func_ptr` ( execution of function ): Hello World
Value found at `return_func_number_ptr(10)`: 10
Value found at `multiply_func_ptr`: 20
Value found at `func_arrays_ptr`: 9
```

> [!TIP] No need to use the `&` character!
> 
> In the above code when I initially showed how to you pointers '[[#Using Pointers In C]]'. I did this:
> 
> ```C
> void *func_ptr = &some_random_func;
> ```
> 
> But apparently you could simply **omit** that `&` when it comes to, *again*, arrays and functions!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!