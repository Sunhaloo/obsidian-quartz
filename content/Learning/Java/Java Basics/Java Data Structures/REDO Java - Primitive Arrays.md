---
id: Java - Primitive Arrays
aliases: Arrays in Java
tags:
  - java
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
>

## List of Contents

- [[#Learning Setup]]
- [[#Creation of Arrays]]
- [[#Displaying Arrays In Java]]

---

# C Arrays!

If we are talking about implementation of **primitive arrays** in Java... You can definitely think of it like they are in [[REDO C - Static Arrays| C]]!

Basically they are the **same** thing but as Java is an actual *High Level Language* it does provides things like:

- Safety
- Garbage Collection
- Exception Handling

> [!NOTE]
> I think the *note* that I am for *C arrays* are going to be pretty much the same thing here but then again... "_**Its Fucking Java**_!!!"

# Learning Setup

This is how I configured / setup my Project structure to be able to use multiple files ( *via packages* ).

- This is how the current **project** structure looks like:

```console
 .
├──  helpers
│   └──  HelperFuncs.java
├──  Main.java
└──  Makefile
```

- Contents of our `src/helpers/HelperFuncs.java` file:

```java
// Mark this file as a package
package helpers;

// Class implementation of `HelperFuncs.java` file
public class HelperFuncs {
  // Function to help us draw a horizontal rule
  public static void displayRule(int numChar) {
    // Iterate through the number of characters
    for (int i = 0; i < numChar; i++) {
      System.out.printf("-");
    }

    System.out.printf("\n");
  }

  // Function that will allow us to display an integer array of "any" size
  public static void displayIntArr(int[] arr) {
    // Iterate through the length of the array
    for (int i = 0; i < arr.length; i++) {
      // Display the data at each index
      System.out.printf("Index: %d --> Value: %d\n", i, arr[i]);
    }
  }

  // Function that will allow us to display an double array of "any" size
  public static void displayDoubleArr(double[] arr) {
    // Iterate through the length of the array
    for (int i = 0; i < arr.length; i++) {
      // Display the data at each index
      System.out.printf("Index: %d --> Value: %.2f\n", i, arr[i]);
    }
  }

  // Function that will allow us to display an character array of "any" size
  public static void displayCharArr(char[] arr) {
    // Iterate through the length of the array
    for (int i = 0; i < arr.length; i++) {
      // Display the data at each index
      System.out.printf("Index: %d --> Value: %c\n", i, arr[i]);
    }
  }

  // Function that will allow us to display an string array of "any" size
  public static void displayStringArr(String[] arr) {
    // Iterate through the length of the array
    for (int i = 0; i < arr.length; i++) {
      // Display the data at each index
      System.out.printf("Index: %d --> Value: %s\n", i, arr[i]);
    }
  }

}
```

- Current contents of the `src/Main.java` file:

```java
// Import the `helpers/HelperFuncs.java` file
import helpers.HelperFuncs;

// Our main class
public class Main {
  // Our main static function
  public static void main(String[] args) {
    System.out.println("\nHello World\n");
  }
}
```

- This is how I am compiling and running the program with my `Makefile`:

```makefile
program:
	@rm -rf Main.class helpers/*.class
	@javac helpers/*.java Main.java
	@echo
	@java Main

compile:
	@javac helpers/*.java Main.java

clean:
	@rm -rf Main.class helpers/*.class
```

# Creation of Arrays

- The following code block below is going to show us how to create simple **one dimensional** arrays:

```java
// Declare and initialise array of integer
int[] intArr = { 1, 2, 3, 4, 5 };

// Declare and initialise array of double
double[] doubleArr = { 0.001, 0.0002, 50.50, 69.6969, 0.0 };

// Declare and initialise array of character
char[] charArr = { 'F', 'U', 'C', 'K', '!' };

// Declare and initialise array of strings
String[] strArr = { "Ayrton Senna", "Lewis Hamilton", "Sebastien Vettel", "Max Verstappen", "Nicholas Latifi" };
```

- In the following code block you are going to see me create some **multidimensional** arrays:

```java
    // Declare and initialise multi-dimensional array of integer
    int[][] intMarr = {
        { 1, 2, 3 },
        { 4, 5, 6 },
        { 7, 8, 9 }
    };

    // Declare and initialise multi-dimensional array of float
    float[][] floatMarr = {
        { 1.1f, 2.2f },
        { 3.3f, 4.4f, 5.5f, 6.9f }
    };

    // Declare and initialise multi-dimensional array of character
    char[][] charMarr = {
        { 'A', 'B' },
        { 'C' },
        { 'X', 'Y' }
    };

    // Declare and initialise two dimensional array of string
    String[][] strings = {
        { "Hello", "World", "C" },
        { "Shits", "Fun" }
    };

    // Declare and initialise three dimensional array of string
    int[][][] intMarrs = {
        {
            { 1, 2, 3 },
            { 4, 5, 6 },
            { 7, 8, 9 }
        },
        {
            { 10, 11, 12 },
            { 13, 14, 15 },
            { 16, 17, 18 }
        },
        {
            { 19, 20, 21 },
            { 22, 23, 24 },
            { 25, 26, 27 }
        }
    };
```

---

# Displaying Arrays In Java

## Displaying One Dimensional Arrays

- This is the function that we *implemented* in our `HelperFuncs.java` file:

```java
  // Function that will allow us to display an integer array of "any" size
  public static void displayIntArr(int[] arr) {
    // Iterate through the length of the array
    for (int i = 0; i < arr.length; i++) {
      // Display the data at each index
      System.out.printf("Index: %d --> Value: %d\n", i, arr[i]);
    }
  }
```

- Therefore, to display our *integer* array in our `Main.java` file:

> I am just going to call the function, *in this case*!

```java

// Import the `helpers/HelperFuncs.java` file
import helpers.HelperFuncs;

// Our main class
public class Main {
  // Our main static function
  public static void main(String[] args) {
    // declare and initialise array of integers
    int[] int_arr = { 1, 2, 3, 4, 5 };

    // call the required function to display the integer array
    HelperFuncs.displayIntArr(int_arr);
  }
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

I **don't** have any functions in my `HelperFuncs.java` file to **display** a *two dimensional* array!

Therefore, I am going to go and write a little function that will allow us to display a *two dimensional* array!

- **Declare** the function in the `HelperFuncs.java`:

```java

```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!