---
id: C - Type Function from Python
aliases: Implementation of `type()` Function in C
tags:
  - C
  - python
author: S.Sunhaloo
date: 2025-09-03
status: Completed
---

> [!INFO] Resources
> - https://en.cppreference.com/w/c/language/generic.html
> - https://stackoverflow.com/questions/64044070/how-to-make-an-output-function-similar-to-pythons-in-c
> 	- https://stackoverflow.com/a/64044782
>
> > [!WARNING] Refer To Link Only... **Code Does NOT Solve My Problem**!!!
> > The code in the above link is **not** trying to achieve the same *thing* that I am trying to achieve.
> >
> > The code in the link is, supposedly trying to make a *better* and *safer* `printf` function whereby if you use the **format specificier** `%f` to display and `int`eger
> >
> > You clearly know that your LSP will start to **scream** at you!
> >
> > The guy on [stackoverflow](https://stackoverflow.com) is trying to "*fix*" this by allowing you to use `printf` like Python's `print` function.
> >
> > > But I am **not** trying to achieve that "*goal*"!
> >
>

# Implementation of `type` From Python in C

## `type` Function In Python

```python
# our main function
def main():
    # find the "data types" of some "data"
    print(f"Integer Data Type: {type(69)}")
    print(f"Float Data Type: {type(69.69)}")
    print(f"String Data Type: {type("Joe Mama")}")
    print(f"Boolean Data Type: {type(True)}")
    print(f"Lists Data Type: {type([69, "fuck", 69.69, "Y"])}")
    print(f"Sets Data Type: {type({69, 69.69, True})}")
    print(f"Dictonaries Data Type: {type({'x': "big", 'y': "shitter"})}")


# source the main function
if __name__ == "__main__":
    main()
```

- Output something like this:

```console
Integer Data Type: <class 'int'>
Float Data Type: <class 'float'>
String Data Type: <class 'str'>
Boolean Data Type: <class 'bool'>
Lists Data Type: <class 'list'>
Sets Data Type: <class 'set'>
Dictonaries Data Type: <class 'dict'>
```

> [!WARNING] This is <strong> <span style="color: red;"> Not</span> </strong> Available in C!
>
> > Obviously!
>
> Therefore, I am going to try to "*replicate*" in C using 2 method that I found on the Internet!

## Version 1: Implementation in C using `_Generic`

### Macros Definition

This is the code that [Gemini](https://gemini.google.com) wrote for me!

```c
// My macro from a previous response
#define TYPE_NAME(X) _Generic((X), \
    int: "int", \
    float: "float", \
    double: "double", \
    char*: "char*", \
    default: "unknown type")
```

### Usage

```c
#include <stdio.h>

// define generic 'expression' for the "fake" type function
// WARNING: pay close attention the `\` character is still here!
// because of LSP and formatters( I use Neovim ) it automatically gets formatted
#define TYPE(X)                                                                \
  _Generic((X),                                                                \
      int: "int",                                                              \
      float: "float",                                                          \
      double: "double",                                                        \
      char *: "char*",                                                         \
      default: "unknown type")

// our main function
int main(int argc, char *argv[]) {
  // showcase the usage of the 'TYPE' macro
  printf("\nInteger Data Type: %s\n", TYPE(69));
  printf("Floating Data Type: %s\n", TYPE(69.69));
  printf("Double Data Type: %s\n", TYPE(69.69f));
  printf("String Data Type: %s\n", TYPE("Joe Mama"));

  return 0;
}
```

- The above code is going to output something like this:

```console
Integer Data Type: int
Floating Data Type: double
Double Data Type: float
String Data Type: char*
```

### Nevertheless, Limitations and Limitations

Now, is **not** going to handle other data types like `short int`, *functions* and *other* data types.

> [!INFO] I did **not** know that `type` from *Python* could do this
>
> ```python
> # simple addition function
> def add_two_nums(num_1: float, num_2: float) -> float:
>    return num_1 + num_2
>
>
> # our main function
> def main():
>    # find the "type" of the function
>    print(f"\nType Of Addition Function: {type(add_two_nums)}")
>
>
> # source the main function
> if __name__ == "__main__":
>    main()
> ```
>
> This simply returns the following output:
>
> ```console
> Type Of Addition Function: <class 'function'>
> ```

#### "Minimising The Damage"

Therefore, I am going to update our *macro* so that it can include **most** ( *not all... I think you fucking understand English* ) data types.

##### Checks For Most Data Types

```c
// define ( updated ) generic 'expression' for the "fake" type function
// WARNING: pay close attention the `\` character is still here!
// because of LSP and formatters( I use Neovim ) it automatically gets formatted
#define TYPE(X)                                                                \
  _Generic((X),                                                                \
      char: "char",                                                            \
      signed char: "signed char",                                              \
      unsigned char: "unsigned char",                                          \
      short: "short",                                                          \
      unsigned short: "unsigned short",                                        \
      int: "int",                                                              \
      unsigned int: "unsigned int",                                            \
      long: "long",                                                            \
      unsigned long: "unsigned long",                                          \
      long long: "long long",                                                  \
      unsigned long long: "unsigned long long",                                \
                                                                               \
      float: "float",                                                          \
      double: "double",                                                        \
      long double: "long double",                                              \
                                                                               \
      char *: "char*",                                                         \
      const char *: "const char*",                                             \
      void *: "void*",                                                         \
                                                                               \
      default: "unknown type")
```

Therefore, if we update our `main` function to include these:

```c
  // define some variables with different data types
  short short_int = 1;
  unsigned long unsigned_long_int = 100UL;
  long double long_double = 1234;

  // showcase the usage of the 'TYPE' macro
  printf("Short Integer Data Type: %s\n", TYPE(short_int));
  printf("Unsigned Long Data Type: %s\n", TYPE(unsigned_long_int));
  printf("Long Double Data Type: %s\n", TYPE(long_double));
```

- We should expect this as output:

```console
Short Integer Data Type: short
Unsigned Long Data Type: unsigned long
Long Double Data Type: long double
```

> [!INFO] Hence!
> This is what I am going to be using for most purposes as it includes most data types...

##### Checks For Functions

> When are you going to have to find the "*data type*" of a function?

```c
// define generic 'expression' for the "fake" type function
// WARNING: pay close attention the `\` character is still here!
// because of LSP and formatters( I use Neovim ) it automatically gets formatted
#define TYPE_FUNC(X)                                                           \
  _Generic((X),                                                                \
      int (*)(int): "integer fuction ( 1 param ) -> int",                      \
      int (*)(int, int): "integer fuction ( 2 param ) -> int",                 \
      float (*)(int, float, double): "float fuction ( 3 param ) -> float",     \
      void (*)(char[], char[]): "char fuction ( 2 param ) -> void",            \
      default: "unknown variable / function")
```

Therefore, if we go ahead and make some functions that we then apply the `TYPE_FUNC` macro to check there actual data type!

```c
#include <stdio.h>

// define generic 'expression' for the "fake" type function
// WARNING: pay close attention the `\` character is still here!
// because of LSP and formatters( I use Neovim ) it automatically gets formatted
#define TYPE_FUNC(X)                                                           \
  _Generic((X),                                                                \
      int (*)(int): "integer fuction ( 1 param ) -> int",                      \
      int (*)(int, int): "integer fuction ( 2 param ) -> int",                 \
      float (*)(int, float, double): "float fuction ( 3 param ) -> float",     \
      void (*)(char[], char[]): "char fuction ( 2 param ) -> void",            \
      default: "unknown variable / function")

// declare some functions to show our macro's "functionality"
int single_param_func_int(int x) { return x; }
int double_param_func_int(int x, int y) { return x + y; }
int triple_param_func_int(int x, int y, int z) { return x + y + z; }
float triple_param_func_float(int x, float y, double z) { return x + y + z; }
void double_param_func_void(char x[], char y[]) {
  printf("\nFull Name: %s, %s\n", x, y);
}

// our main function
int main(int argc, char *argv[]) {
  // showcase the usage of the 'TYPE_FUNC' macro
  printf("Integer Function ( Single Parameter ): %s\n",
         TYPE_FUNC(single_param_func_int));
  printf("Integer Function ( Double Parameter ): %s\n",
         TYPE_FUNC(double_param_func_int));
  printf("Float Function ( Triple Parameter ): %s\n",
         TYPE_FUNC(triple_param_func_float));
  printf("Void Function ( Double Parameter ): %s\n",
         TYPE_FUNC(double_param_func_void));
  printf("'Unknown' Function ( Triple Parameter ): %s\n",
         TYPE_FUNC(triple_param_func_int));

  return 0;
}
```

- This is the output after running the above code:

```console
Integer Function ( Single Parameter ): integer fuction ( 1 param ) -> int
Integer Function ( Double Parameter ): integer fuction ( 2 param ) -> int
Float Function ( Triple Parameter ): float fuction ( 3 param ) -> float
Void Function ( Double Parameter ): char fuction ( 2 param ) -> void
'Unknown' Function ( Triple Parameter ): unknown variable / function
```

## Version 2: `scanf`... So Fucking Simple!

```c
#include <stdio.h>

// our main function
int main(int argc, char *argv[]) {
  // declare some variables
  int num = 69;
  float floating_num = 6.9;
  double big_floating_num = 69.69;
  char character_thingy = 'A';
  char yes_this_is_a_string[11] = "Hello World";

  // display the size of each variable in bytes
  printf("Integer Variable Bytes Size = %ld\n", sizeof(num));
  printf("Float Variable Bytes Size = %ld\n", sizeof(floating_num));
  printf("Double Variable Bytes Size = %ld\n", sizeof(big_floating_num));
  printf("Character Variable Bytes Size = %ld\n", sizeof(character_thingy));
  printf("Array of Characters Variable Bytes Size = %ld\n",
         sizeof(yes_this_is_a_string));

  return 0;
}
```

If you don't want to complicate things and your entire existence... You can simply use the `sizeof()` function to check for the **size of the variable** ( *in bytes* ).

Therefore, based on the number that you get; you should be able to *judge* the **data type**!

### But Again Problems

To be honest with you. I **don't** think that we need such a thing in C!

We all know that C is a *declarative language* and well... You **need** to declare your variable or function with the "*correct*" datatype.

For example, **both** of these method shown above will never *satisfy* all the **edge cases**

> [!TIP] Nevertheless
> This was a good experience if finding out that I don't know anything about C... "*Yet*!"

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!