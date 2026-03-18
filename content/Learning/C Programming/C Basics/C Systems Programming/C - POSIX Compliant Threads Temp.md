---
id: C - POSIX Compliant Threads
aliases: Multi-threading in C using the `pthread` library
hags:
  - C
  - basics
author: S.Sunhaloo
date: 2026-02-12
status: In-Progress
---

## List of Contents



---

> [!NOTE]
> This note is basically inspired by these YouTube video(s):
> 
> - C Threads: https://www.youtube.com/watch?v=ldJ8WGZVXZk
> 
> > [!TIP] Additionally...
> > 
> > You could always use the `man pthreads` command to learn more about threads!
> > 
> > > You can even do things like `man pthread_create` or `man pthread_join` and more!

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
>	 @gcc main.c -Wall -Wextra -lpthread -o program
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

--- 

> [!BUG] Explain Here
> - Threads
> - Single V/S Multi Threading ( use web-server as example with the requests to show difference )
> - Concurrent V/S Parallel

# Using POSIX Threads

## Simple Multi-Threading Program

```C
#include <pthread.h>
#include <stdio.h>

// `void` function that returns a pointer
void *greet(void *args) {
  printf("Hello World from `greet` function!\n");

  // given that we are returning a `void` pointer
  return NULL;
}

// our main function executed by primary thread
int main(int argc, char *argv[]) {
  // declare a thread variable for `greet` function
  pthread_t greet_thread;

  // create a thread to run the `greet` function
  pthread_create(&greet_thread, NULL, greet, NULL);

  pthread_join(greet_thread, NULL);

  printf("Hello Word from `main` function!\n");

  return 0;
}
```

- The output:

```console
Hello World from `greet` function!
Hello Word from `main` function!
```

### Explanation Of Above Program Code

- Declare thread variable to run specific function:

```C
  // declare a thread variable for `greet` function
  pthread_t greet_thread;
```

- Create the function to run by the thread:

```C
// `void` function that returns a pointer
void *greet(void *args) {
  printf("Hello World from `greet` function!\n");

  // given that we are returning a `void` pointer
  return NULL;
}
```

> [!NOTE] Why created this way?
> 
> > [!WARNING] NOT A FUNCTION POINTER
> > 
> > Its **not** a *function pointer* but a function that **returns** a *pointer*!
> 
> - Function that returns a pointer to `void`
> - **Need** to pass `void *insert_anything_here` as argument because `pthread_create` expects that *syntax*
> - Run what we want
> - As `void *greet()`; need to return `NULL`!

- Create the thread:

```C
  // create a thread to run the `greet` function
  pthread_create(&greet_thread, NULL, greet, NULL);
```

> [!WARNING]
> The `pthread_create` function only takes `void` function that returns a pointer!
> 
> Meaning that we **cannot** pass a function that is declare like: `int *int_returning_ptr_func` or `char *char_returning_ptr_func`

- Explanation of `pthread_create` from [Claude](https://claude.ai):

```C
pthread_create(
    &greet_thread,  // 1st: where to store thread ID
    NULL,           // 2nd: thread attributes (NULL = use defaults)
    greet,          // 3rd: function pointer to run
    NULL            // 4th: argument to pass to greet (void* arg)
);
```

> [!NOTE]
> As soon as we use the `pthread_create` function, the threads starts running **immediately**

- Join the thread to the main program:

```C
  pthread_join(greet_thread, NULL);
```

- Explanation of `pthread_create` from [Claude](https://claude.ai):

```C
pthread_join(
    greet_thread,   // 1st: which thread to wait for
    NULL            // 2nd: where to store return value from thread
);
```

> [!TIP] This is basically `async` / `await` from [[Javascript - Asynchronous | Javascript]]!
> 
> The `pthread_join` is basically here so that the `main` function that is the main thread executioner does not simply forget about the `greet_thread` thread!
> 
> It allows the `greet_thread` to actually run!

## Simple Thread Program ( With Arguments Passed )

```C
#include <pthread.h>
#include <stdio.h>

// `void` function that returns a pointer
void *greet(void *args) {
  printf("Hello World from `greet` function!\n");

  // given that we are returning a `void` pointer
  return NULL;
}

// `void` function that returns a pointer and takes argument
void *display_number(void *args) {
  // get the integer number from the pointer into a pointer
  long int *long_num_ptr = (long int *)args;

  printf("The integer number is %ld\n", *long_num_ptr);

  return NULL;
}

// `void` function that takes arguments, computes and display sum
void *sum_computation(void *args) {
  // get the number from the argument
  int *number = (int *)args;

  // declare sum variable
  int sum = 0;

  // compute the sum for 1000 times
  for (int i = 0; i < 1000; i++) {
    sum += *number;
  }

  // display the sum of the number
  printf("Sum after adding '%d' 1000x: %d\n", *number, sum);

  return NULL;
}

// our main function executed by primary thread
int main(int argc, char *argv[]) {
  // declare a thread variable for `greet` function
  pthread_t greet_thread;
  pthread_t display_num_thread;
  pthread_t sum_thread;

  // create long integer variables
  long int num_to_display = 5;
  int num_to_sum = 10;

  // create and run threads immediately
  pthread_create(&greet_thread, NULL, greet, NULL);
  pthread_create(&display_num_thread, NULL, display_number,
                 (void *)&num_to_display);
  pthread_create(&sum_thread, NULL, sum_computation, (void *)&num_to_sum);

  // wait for the threads before ending main process / main executioner test
  pthread_join(greet_thread, NULL);
  pthread_join(display_num_thread, NULL);
  pthread_join(sum_thread, NULL);

  printf("Hello Word from `main` function!\n");

  return 0;
}
```

- Running the above code we get something like:

```console
The integer number is 5
Sum after adding '10' 1000x: 10000
Hello World from `greet` function!
Hello Word from `main` function!
```

> This is how we pass in and use arguments in these types of functions!

## Capture Return Value

```C
#include <pthread.h>
#include <stdio.h>

// `void` fucntion that returns a pointer
void *return_int(void *args) {
  // get the integer value passed from the user
  int *number = (int *)args;

  return number;
}

// our main function ( main thread executioner )
int main(int argc, char *argv[]) {
  // declare the thread
  pthread_t return_num_thread;

  // declare the `void` return variable
  void *returned_value_from_thread;

  // declare and initialise to pass to function
  int arg_num = 5;

  // create and run the thread immediately
  pthread_create(&return_num_thread, NULL, return_int, (void *)&arg_num);

  // wait for the function to run before exiting main program
  pthread_join(return_num_thread, &returned_value_from_thread);

  // display the return value to the user
  printf("\nReturn value from thread: %d\n",
         *(int *)returned_value_from_thread);

  return 0;
}
```

- Therefore the above code is going to return something like this:

```console
Return value from thread: 5
```

## Single-Threading V/S Multi-Threading

### Single Threading

```C
#include <pthread.h>
#include <stdio.h>

// `void` function that will keep adding a number for 999999999
void *summation(void *args) {
  long int sum = 0;
  long int *num_to_sum = (long int *)args;

  for (long int i = 0; i < 999999999; i++) {
    sum += *num_to_sum;
  }

  return NULL;
}

int main(int argc, char *argv[]) {
  long int first_num = 1;
  long int second_num = 10;

  // call the function ( two times ) directly
  summation((void *)&first_num);
  summation((void *)&second_num);

  return 0;
}
```

- Using the `time` command to find the time taken to run the above code

```console
./program  0.40s user 0.00s system 99% cpu 0.406 total
```

### Multi-Threading

> [!NOTE]
> **Same** code but now using *threads*!

```C
#include <pthread.h>
#include <stdio.h>

// `void` function that will keep adding a number for 999999999
void *summation(void *args) {
  long int sum = 0;
  long int *num_to_sum = (long int *)args;

  for (long int i = 0; i < 999999999; i++) {
    sum += *num_to_sum;
  }

  return NULL;
}

int main(int argc, char *argv[]) {
  long int first_num = 1;
  long int second_num = 10;

  // create thread
  pthread_t first_thread;
  pthread_t second_thread;

  // create and run the threads immediately
  pthread_create(&first_thread, NULL, summation, (void *)&first_num);
  pthread_create(&second_thread, NULL, summation, (void *)&second_num);

  // make the main executioner thread wait for the two threads to complete run
  pthread_join(first_thread, NULL);
  pthread_join(second_thread, NULL);

  return 0;
}
```

- Again using the `time` command to find time taken to run multi-threaded code:

```console
./program  3.91s user 0.00s system 198% cpu 1.968 total
```

> [!BUG]
> I **cannot** seem to make a program that is going to show that using threads are *faster* than simply using the single-threaded ones

# TODO

- How to pass multiple values to the **last** argument of `pthread_create` using `struct`
- Thread locking with mutexes `pthread_mutex_t`

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!