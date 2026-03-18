---
id: Java Language Basics
aliases: Java Language Basics
tags:
  - java
  - basics
author: S.Sunhaloo
date: 2025-08-11
status: Completed
---

## List of Contents

- [[#Installation of Java]]
	- [[#How it Works]]
- [[#Java Boiler Plate]]
- [[#Basic Data Types]]
- [[#Display Stuff to Screen]]
	- [[#Type Cast]]
	- [[#Find The Type Of Variable / Constant / Object]]
- [[#User Inputs]]
- [[#Conditions]]
- [[#Loops]]
- [[#Functions]]
- [[#Exception Handling]]

---

> [!INFO]
> I always had trouble using / reading the Official Java Documentation.
>
> Heck because I did not find anything what I actually needed... Back in the day I just use YouTube.
>
> > But this is going to be "*new*" me now and I want to learn the proper way!
>
> > [!NOTE]
> > Here are a few resources about how to read and understand the Official Java Documentation.
> >
> > - https://stackoverflow.com/questions/2576709/how-do-i-read-java-documentation
> > - https://web.archive.org/web/20181230191106/https://www.otherwise.com/Lessons/ReadingTheJavadoc.html
> > - https://www.reddit.com/r/javahelp/comments/vzmrcm/how_to_search_official_oracle_java_docs/
>
> - https://docs.oracle.com/en/
> 	- https://docs.oracle.com/en/java/
> - https://docs.oracle.com/javase/6/docs/api/
>
> - https://www.go4expert.com/articles/wrapper-class-java-t22183/

# Installation of Java

## Long Story Short

To install Java, i.e `java` and `javac`; refer to code block found below:

```bash
# debian / debian based distributions
# NOTE: as debian is "stable" ( hehe ) you guys are going to have to
# download the "version" '21' of openjdk
sudo apt-get install openjdk-21-jdk

# macos users - see homebrew package manager or xcode-select
#sorrynotsorry

# I use Arch BTW ( install the latest version of java )
sudo pacman -S jdk-openjdk

# fedora based distributions
sudo dnf install java-latest-openjdk-portable
```

> [!INFO] Windows Users
> Now, I don't think Window's official package manager `winget` has it...
>
> > I mean it does; but I don't think it allows to download *latest* version ( *more like "the version that I want"* )
>
> Therefore, I think I am going install another package manager!

### Windows Users

Now, I am going to use [scoop](https://scoop.sh/) but you could also you [chocolatey](https://chocolatey.org/)

> I just prefer the way that `scoop` works!

- Install scoop with the following command:

```powershell
# change the "permissions"
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
# actually run the script to install
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
```

- Restart the shell / terminal and then run the following command to add "*extra*" packages:

```powershell
# add the extras bucket
scoop bucket add extras

# additionally add the java bucket
scoop bucket add java
```

- Actually install the `java` package

```powershell
# actually install java / openjdk
scoop install java/openjdk
```

## How it Works

![[Java - JDK - JRE Diagram.png | 650]]

As you can see, Java is a **compiled** language similar to [[C Data View | C Data View]].

This means that we first have to run the `javac` command so that our `.java` file is **compiled to _bytecode_** thereby creating a `.class` file and its then that we can run the `java` command and provide it with the *class* file so that it can be run.

> [!INFO]
> You can think of it like this:
>
> - Running the command `javac` is like running the "*contents*" inside the 'JDK'
> - Running the command `java` is like running the "*contents*" inside the 'JRE'
>
> And in case if you don't know these acronyms:
>
> - 'JDK': Java Development Kit
> - 'JRE': Java Runtime Environment

> Well [let's get started](https://www.youtube.com/watch?v=IPFiKEm-oNI)

---

> [!WARNING]
> As you know every programming language has its own convention on how to *write* variables, functions, how the format of a code should look like...
>
> I come from Python; this means that I use `snake_case` for variables and function names.
>
> You are going to see me use *snake case* for some time before I realise that I need to use `camelCase` or `UpperCamelCase`.
>
> > Therefore, *please forgive me*!
>

# Java Boiler Plate

```java
public class Main {
  // our main function
  public static void main(String[] args) {
    System.out.println("Hello World");
  }
}
```

> [!WARNING] Careful With **File Names**
> Below you are going to see that on the first line of the boiler plate, we have this:
>
> ```java
> public class Main {
> ```
>
> The reason as to why its `Main`, its because the *actual* **file name** is also `Main.java`.
>
> So whenever you create a file... You <span style="color: red;"> have</span> make sure that the **same** *class* name.
>
> > [!INFO] Changing The Class Name
> > I am going to take the same boiler plate code above and **only change** the *class* name from `Main` to `Test` and then I am going to compile it.
> >
> >
> > ```console
> > Main.java:1: error: class Test is public,
> > should be declared in a file named Test.java
> > public class Test {
> >       ^
> > 1 error
> > ```
> >
> > > As we can see... Its does **not** compile at all!
> > >
> >
>

> [!INFO] How to **Compile** and **Run** `.java` Files
> 1. Firstly, **compile** the `.java` file with `javac FileName.java`
> 2. Secondly, **run** the `.class` file with `java FileName`
>
> > [!WARNING]
> > Yes, you **only** need to *type* the file name **without** the extension.
> >
> > So if you were going to run the file `Main.class` simply run:
> >
> > ```bash
> > # run the Main file
> > java Main
> > ```
> >
> > If you go ahead and run `java Main.class`, you are going to see something like this:
> >
> > ```console
> > Error: Could not find or load main class Main.class
> > Caused by: java.lang.ClassNotFoundException: Main.class
> > ```
>

# Basic Data Types

> [!INFO] Resource(s)
> - https://www.oracle.com/java/technologies/javase/codeconventions-codeexamples.html#182

```java
// single line comment

/*
* This is a multi-line
* comment. Very nice!
* Useful when you have to rage
* at someone
*/

/**
* this is a java-doc comment
* it is also multi-lined but can be used to
* explain variables and others.
* @author the author who wrote the code / function
* @param user_input passing the input of user to function
* @return that the function / program will return
* @throws IOException the error that the function with display
* there are so many refer to online documentation
*/
```

## Primitive Data Types

```java
int num = 69;
float floating_num = 6.9f;
double big_floating_num = 69.69;
char character_thingy = 'A';
boolean true_false = true;
```

## Wrapper - Referenced Data Types

```java
Integer w_num = 69;
Float w_floating_num = 6.9f;
Double w_big_floating_num = 69.69;
Character w_character_thingy = 'A';
Boolean w_true_false = true;
String some_text = "Some Text Here";
```

> [!INFO] Primitive V/S Wrapper - Referenced Data Types
> No need to complicate the matter for the moment.
>
> But there are a few things that we need to about them.
>
> 1. Primitive datatypes are **faster**, **more** *memory efficient* than Wrapper datatypes
> 2. Primitive datatypes are well... "*Primitive*"; therefore, the **cannot** be used with Objects
> 3. Primitive datatypes **cannot** be `null`
>
> > For more information please do check the link: https://www.go4expert.com/articles/wrapper-class-java-t22183/
>

> [!WARNING] Division in Java...
> Compared to Python who does **not** have *declaration*... The beloved character `//` does <span style="color: red;"> not</span> exists in Java!
>
> > Therefore, it depends on the context!
>
> - Returns **Integer** Values
>
> ```java
> System.out.println(1 / 2);
> System.out.println(-50 / 33);
> System.out.println(-9 / 11);
> System.out.println(5 / 2);
> ```
>
> - Returns **Float** / **Double** Values
>
> ```java
> System.out.println(1.0 / 2);
> System.out.println(-50 / 33.0);
> System.out.println(-9f / 11.0);
> System.out.println(5f / 2f);
> ```

# Display Stuff to Screen

As you know "*OOP People*" like to complicate things and that is why we have **3** types of `print` functions.

```java
public class Main {
  // our main function
  public static void main(String[] args) {
    // primitive datatypes
    int num = 69;
    double big_floating_num = 69.69;
    char character_thingy = 'A';

    // wrapper datatypes
    Integer w_num = 69;
    Double w_big_floating_num = 69.69;
    Character w_character_thingy = 'A';

    // using the `System.out.print()` function
    // NOTE: I suggest you that you stay away from `System.out.print()`
    System.out.print("Hello World");
    // INFO: this should be on the same line
    System.out.print(
	    "Primitive Datatype '" + num +
	    "' - Wrapper Datatype '"
	    + w_num
    );

    // output a blank line
    System.out.println();

    // using the `System.out.println();` function ==> "the standard"
    System.out.println(
	    "Primitive Datatype: " + character_thingy +
	    "\nWrapper Datatype: " + w_character_thingy
    );

    // using the lovely `System.out.printf();` function from C
    System.out.printf(
	    "Primitive Datatype: %.1f | Wrapper Datatype: .1%f\n"
	    , big_floating_num, w_big_floating_num
    );
  }
}
```

## Type Cast

This is going to be a little bit complex compared to what we learned in [[C Language Basics#Type Cast | C]] and [[Python Language Basics#Type Cast | Python]].

> As we have **both** *Primitive* and *Wrapper* data types!

### Converting Primitive to Primitive

```java
// primitive datatypes
int num = 69;
float floating_num = 6.9f;
char character_thingy = 'A';

// apply the type cast ==> change the data type
float decimal_int_number = (float) num;
int int_some_decimal_num = (int) floating_num;
int int_character_thingy = (int) character_thingy;
```

### Converting Primitive to Wrapper

```java
// primitive datatypes
int num = 69;
float floatingNum = 6.9f;
boolean booleanTrueFalse = true;

// manually converting the primitive datatypes to wrapper datatypes
Integer wNumManual = Integer.valueOf(num);
Float wFloatManual = Float.valueOf(floatingNum);
Boolean wBooleanManual = Boolean.valueOf(booleanTrueFalse);

// automatically converting the primitive datatypes to wrapper datatypes
Integer wNumAuto = num;
Float wFloatAuto = floatingNum;
Boolean wBooleanAuto = booleanTrueFalse;
```

> [!WARNING] The `.valueOf()` Method
> The `.valueOf()` method only accepts datatypes of "*type*" `int` and `String`.
>
> Therefore, we had to *cast* the 

### Converting Wrapper to Primitive - Unboxing

> [!NOTE] Wrapper **To** Primitive First!
> We first need to look at converting **Wrapper** datatypes to **Primitive** datatypes before going to learn to to *type cast* wrapper **to** wrapper.

```java
// wrapper datatypes
Integer num = 69;
Float floatingNum = 6.9f;
Boolean booleanTrueFalse = true;

// manually converting the wrapper datatypes to primitive datatypes
// NOTE: this step is called "unboxing"... remember Unbox Therapy
int pNumManual = num.intValue();
float pFloatNumManual = floatingNum.floatValue();
boolean pBooleanManual = booleanTrueFalse.booleanValue();

// automatically converting the wrapper datatypes to primitive datatypes
int pNumAuto = num;
float pFloatNumAuto = floatingNum;
boolean pBooleanAuto = booleanTrueFalse;
```

### Converting Wrapper to Wrapper

> [!NOTE] **Cannot** Directly *Type Cast* Wrapper Datatypes
> This is the reason as to why I said that we need to first learn how to convert the *wrapper* datatype **into** its *primitive* counterpart.
>
> Even though we **cannot** convert *directly*. This does not mean that we *have* to create another variable to hold the **primitive** *data* temporarily.
>
> > We can covert *wrapper* **to** *wrapper* in a single line

```java
    // wrapper datatypes
    Integer num = 69;
    Float floatingNum = 6.9f;
    Character characterThingy = 'A';

    // manually converting the wrapper datatypes to wrapper datatypes

    // NOTE: here we have to create another "placeholder" datatype
    // additiionally, I am going to "automatically" convert wrapper to primitive
    float placeholderFloat = num;
    // WARNING: not auto casting here... actually "assigning"
    int placeholderFloatingNum = (int) floatingNum.floatValue();
    int placeholderCharacter = characterThingy;

    // now we convert the primitive datatype to wrapper datatype
    Float wFloat = Float.valueOf(placeholderFloat);
    Integer wInteger = Integer.valueOf(placeholderFloatingNum);
    Integer wCharacter = Integer.valueOf(placeholderCharacter);

    // automatically converting the wrapper datatypes to wrapper datatypes
    Float wFloatDirect = Float.valueOf(num.intValue());
    // WARNING: similarly actually "assigning"...
    Integer wIntegerDirect = Integer.valueOf((int) floatingNum.floatValue());
    Integer wCharacterDirect = Integer.valueOf(characterThingy.charValue());

```

#### Find The Type Of Variable / Constant / Object

We know that [[Python Language Basics#Basic Data Types | Python]] has the `type()` function that can be used to check a *variable's* datatype.

But we know that Python is *weird* and we do **not** declare anything!

> What I am trying to say that the **datatypes** in Python are a bit "*special*" ( *I don't really know how it works in memory though* )

But in languages like C, as we **declare** our variables and functions ( *and all of the others* ), we don't really have the need to have a "`type()`" function!

But Java does have it and its called the `.getClass()` method! Nevertheless, *primitive* datatypes does **not** have / are **not** related to *classes* / *wrapper* datatypes.

Therefore, if you want to check the a *primitive* datatype "*type*". We need to convert them to an `Object` so that we can use that method.

```java
public class Test {
  // our main function
  public static void main(String[] args) {
    // primitive datatypes
    int num = 69;
    float floating_num = 69.69f;
    char character_thingy = 'A';

    // wrapper datatypes
    Integer w_num = 69;
    Float w_floating_num = 69.69f;
    Character w_character_thingy = 'A';
    String some_text = "Some Text Here";

    // display the datatypes of the wrapper variables
    System.out.println("Wrapper Integer: '" + w_num.getClass() + "'");
    System.out.println("Wrapper Float: '" + w_floating_num.getClass() + "'");
    System.out.println("Wrapper Character: '" + w_character_thingy.getClass() + "'");
    System.out.println("Wrapper String: '" + some_text.getClass() + "'");

    System.out.println();

    // display the datatypes of the primitive variables
    System.out.println("Primitive Integer: '" + ((Object) num).getClass() + "'");
    System.out.println("Primitive Float: '" + ((Object) floating_num).getClass() + "'");
    System.out.println("Primitive Character: '" + ((Object) character_thingy).getClass() + "'");
  }
}
```

> [!NOTE]
> If you try to use the `.getClass()` method **directly** with *primitive* datatypes... Then you are going get an error that looks something like this:
>
> ```console
> Test.java:10: error: int cannot be dereferenced
>    System.out.println("Primitive Integer: '" + num.getClass() + "'");
>                                                   ^
> 1 error
> ```

# User Inputs

Java user-inputs are very ( *in terms of syntax* ) to [Visual Basic](https://en.wikipedia.org/wiki/Visual_Basic_(classic)).

Nevertheless, Java does provide a few more tricks up it sleeves compared to *VB's* user-inputs. Below you are going to see how we are going to ask the to enter some data of **different** datatypes.

> [!NOTE]
> In java, we **need** to *import* a utility library which will give us access to the `Scanner` class.
>
> The scanner class is the one who is responsible for taking in user's input.

```java
// Import the `Scanner` class from the 'java.util' package
import java.util.Scanner;

public class Main {
  public static void main(String[] args) {

    // Declare a scanner object that reads input from 'stdin'
    Scanner scanner = new Scanner(System.in);

    // Display prompt the user to enter his name
    System.out.print("Enter Your Name: ");
    String user_name = scanner.nextLine();

    // Display prompt the user to enter his name
    System.out.print("Enter Your Age: ");
    int user_age = scanner.nextInt();

    // Display prompt the user to enter his mass
    System.out.print("Enter Your Mass: ");
    float user_mass = scanner.nextFloat();

    // Close the scanner for good practice
    scanner.close();
  }
}
```

> [!TIP] Tips and Tricks
> 1. The *datatype* which is going to hold our *value* can be **both** *Primitive* or *Wrapper*
> 2. **Close** the `scanner` *object* after usage so that we prevent any *memory leaks* and **free up** resources

# Conditions

## `if` Statements

```java
// Import the `Scanner` class from the 'java.util' package
import java.util.Scanner;

public class Main {
  public static void main(String[] args) {
    // Create scanner for input
    Scanner scanner = new Scanner(System.in);

    // Ask the user to input their age
    System.out.print("Please Enter Your Age: ");
    int userAge = scanner.nextInt();

    // As user's age between 18 and 100 (exclusive of 100)
    if (userAge > = 18 && userAge < 100) {
      System.out.println("You are an adult!");

      // If age entered is less than or equal to 0
    } else if (userAge <= 0) {
      System.out.println("Error!");

      // If user's age is greater than or equal to 100
    } else if (userAge > = 100) {
      System.out.println("Congratulations! You are about to die");

      // If user's age is between 1 and 18 (inclusive)
    } else if (userAge > = 1 && userAge <= 18) {
      System.out.println("Where is Your Guardian!");
    }

    // Close the scanner for good practice
    scanner.close();
  }
}
```

## `switch` Case Statements

```java
// Import the `Scanner` class from the 'java.util' package
import java.util.Scanner;

public class Main {

  public static void main(String[] args) {
    System.out.println("\nProgramming Language Choice Thing :)\n");

    // Asking the user to input their language of choice
    Scanner scanner = new Scanner(System.in);
    System.out.print("What's the programming language you want to learn? ");
    String lang = scanner.nextLine();

    // check the user's input / language entered
    switch (lang) {

      // If users entered 'JavaScript'
      case "JavaScript":
        System.out.println("You can become a Web Developer!");
        break;

      // If users entered 'Python'
      case "Python":
        System.out.println("You can become a Data Scientist!");
        break;

      // If users entered 'PHP'
      case "PHP":
        System.out.println("You can become a Backend Developer!");
        break;

      // If users entered 'Solidity'
      case "Solidity":
        System.out.println("You can become a Blockchain Developer!");
        break;

      // If users entered 'Java'
      case "Java":
        System.out.println("You can become a Mobile App Developer!");
        break;

      // If the users did not enter anything that if found above
      default:
        System.out.println("The language doesn't matter, what matters is solving problems!");
    }

    // Close the scanner for good practice
    scanner.close();
  }
}
```

# Loops

## `while` Loops

```java
// Import the `Scanner` class from the 'java.util' package
import java.util.Scanner;

public class Main {
  // Helper function to check if a string contains only digits
  public static boolean isDigitsOnly(String str) {
    // Iterate through the length of the string
    for (int i = 0; i < str.length(); i++) {
      // Check if each character if

      if (!Character.isDigit(str.charAt(i))) {
        // meaning string contains a character that is not a number
        return false;

      }
    }

    // Meaning that the string only contains "individual" numbers
    return true;
  }

  public static void main(String[] args) {
    // Declare a scanner object that read input from `stdin`
    Scanner scanner = new Scanner(System.in);
    String telNum;

    // Iterate through the `while` loop indefinitely
    while (true) {
      // Ask the user to enter their phone number
      System.out.print("Please Enter Telephone Number: ");
      telNum = scanner.nextLine();

      // Check length and call function to check if string consist only of numbers
      if (telNum.length() == 8 && isDigitsOnly(telNum)) {
        // Exit / break from the `while` loop
        break;

        // Meaning that the telephone number entered is not valid
      } else {
        // Output appropriate message
        System.out.println("\nPlease Enter Correct Telephone Number!\n");

      }
    }

    // Display the valid number
    System.out.println("\nYour Telephone Number is " + telNum);

    // Close the scanner for good practice
    scanner.close();
  }
}
```

### Regex Version

You might have notice that there is no functions such as `isdigit()` and we 

```java
// Import the `Scanner` class from the 'java.util' package
import java.util.Scanner;

public class Main {
  public static void main(String[] args) {
	// Declare a scanner object that read input from `stdin`
    Scanner scanner = new Scanner(System.in);
    String telNum;

    // Iterate through the `while` loop indefinitely
    while (true) {
      // Ask the user to enter their phone number
      System.out.print("Please Enter Telephone Number: ");
      telNum = scanner.nextLine();

      // Check if length is 8 and contains only digits
      if (telNum.matches("\\d{8}")) {
        // Exit / break from the `while` loop
        break;

      } else {
        // output appropriate message
        System.out.println("\nPlease Enter Correct Telephone Number!\n");

      }
    }

    // display the message after exiting `while` loop
    System.out.println("\nYour Telephone Number is " + telNum);

    // Close the scanner for good practice
    scanner.close();
  }
}
```

> [!TIP] *Parse* The Datatype
> Searching for how to do that *without* learning '**Regular Expressions**'... I came across this:
>
> - https://stackoverflow.com/a/1102916
>
> Hence, we can try *parsing* the string entered using things like:
>
> - `Integer.parseInt()`
> - `Float.parseFloat()`
> - `Double.parseDouble()`
>
> So that we can try to convert the string and check if it can be converted to a *numeric* value.
>
> > If we can convert, this means that the string is made of numbers!
>

## `for` Loops

```java
public class Main {

  public static void main(String[] args) {
    // Display 5 integer numbers from '0' to '4'
    for (int i = 0; i < 5; i++) {
      System.out.print(i + " ");

    }

    System.out.println("\n");

    // Display same 5 integer numbers from '4' to '0' in reverse
    for (int i = 4; i > = 0; i--) {
      System.out.print(i + " ");

    }

    System.out.println("\n");

    // Display numbers from '1' to '100' inclusive
    for (int i = 1; i <= 100; i++) {
      System.out.print(i + " ");

    }

    System.out.println("\n");

    // Display even numbers from '1' to '100' inclusive
    for (int i = 2; i <= 100; i += 2) {
      System.out.print(i + " ");

    }

    System.out.println("\n");

    // Display odd numbers from '1' to '100' inclusive
    for (int i = 1; i <= 100; i += 2) {
      System.out.print(i + " ");

    }

    System.out.println();
  }
}
```


## Keywords Related to Looping

# Functions

As this is an *Object Oriented Programming* language; therefore there are *many* **types** of function that is available to be used in Java.

Each function / method comes with its own "*security*" whereby it can be:

- Managed / Used by any other **classes** or **method**
- Managed by a **specific class**
- And *many others*

> Obviously I am **not** going to go over all of them!

Therefore I am going to include a table to show the "_**accessibility**_" of each functions throughout.

| Function Type | **Same** Class | **Different** Class ( **Same** Package ) | **Different** Class ( **Different** Package ) | Sub-Class ( **Same** Package ) | Sub-Class ( **Different** Package ) |
| ------------- | ---------- | ----------------------------- | ----------------------------------- | ------------------------ | ---------------------------- |
| `public` | Yes | Yes | Yes | Yes | Yes |
| `private` | Yes | *No* | *No* | *No* | *No* |
| `protected` | Yes | Yes | *No* | Yes | Yes |
| package-private | Yes | Yes | *No* | Yes | *No* |

> [!INFO] What is a **Package**?
> If you have a Project and you create a *main* folder and then make **sub-folders** inside that *root* project folder... The `.java` files inside each little *sub-folder* make up a **Package**!

> [!INFO] `static` Function
> Similar to something like `@staticmethod` in Python; whereby we do **not** need to create / *instantiate* a Object for **that** *class* to be able to use a function.

> [!WARNING]
> In Java, you **cannot** write a function *outside* of the `public class Main {}` ( *for example* ).
>
> If you are going to write a function you are going to have to write it in an **appropriate** class.

## Public - Static Method Example

```java
// Function that will allow the user to enter amount of dollars
public static float enterDollars() {
// Declare a scanner object that read input from `stdin`
Scanner scanner = new Scanner(System.in);
// Declare a variable which is going to hold the dollars entered
float user_dollars;

// Iterate through the `while` loop indefinitely
while (true) {
  // Exception Handling
  try {
	// Ask the user to amount of dollars
	System.out.print("\nPlease Enter Amount of Dollars: ");
	user_dollars = scanner.nextFloat();

	// Check if the user input is less than zero
	if (user_dollars < 0) {
	  // Output an appropriate message
	  System.out.println("\n<< Input Cannot Be Less Than 0.0!!! > > ");
	} else {
	  // Escape the `while` loop if the input is valid
	  break;
	}
  }

  // If the user does not enter a "float" value
  catch (InputMismatchException e) {
	// Ouput the error in question
	System.out.println("\n<< Error: '" + e + "' > > ");
	// Output appropriate message
	System.out.println("<< Please Enter A Decimal Number / Floating Value!!! > > ");

	// NOTE: need to consume the invalid input
	scanner.next();
  }
}

// Close the scanner object
// INFO: We cannot use `finally` block to close the scanner
// As if we close the `scanner`; we won't be able to take in user inputs again
scanner.close();

// Return the temperatere to the `main` function
return user_dollars;
}
```

# Exception Handling

Similar to Python, Java also does have its own *version* of the `try... except... else... finally` block.

Nevertheless, Java does **not** have the `else` block... Below you are going to find how we are going to implement our *Exception Handling*.

```java

// Import the `Scanner` class from the 'java.util' package
import java.util.InputMismatchException;
// Import the `Scanner` class from the 'java.util' package
import java.util.Scanner;

public class Main {
  public static void main(String[] args) {
    // Declare a scanner object that reads input from 'stdin'
    Scanner scanner = new Scanner(System.in);

    // Exception Handling --> open our scanner
    try {
      // Display prompt the user to enter his name
      System.out.print("Enter Your Name: ");
      String user_name = scanner.nextLine();

      // Display prompt the user to enter his name
      System.out.print("Enter Your Age: ");
      int user_age = scanner.nextInt();

      // Display prompt the user to enter his mass
      System.out.print("Enter Your Mass: ");
      float user_mass = scanner.nextFloat();

      // Try the divide by '0'
      System.out.println(1 / 0);

    }
    // If the user does not enter the correct datatype
    catch (InputMismatchException e) {
      // Display the error message with an appropriate messages to user
      System.out.println("\n\t<< Error: " + e.getMessage() + " > > \n");
      System.out.println("\n<< Please Enter The Appropriate Data Type!!! > > \n");

    }

    // If the programs trys to devide by '0' or something
    catch (ArithmeticException e) {
      // Display the error message with an appropriate messages to user
      System.out.println("\n\t<< Error: '" + e.getMessage() + "' > > ");
      System.out.println("\n<< You CANNOT Divide By 0... Fucking Idiot!!! > > \n");

    }

    // The code block that always run similar to 'finally' in Python
    finally {
      // Close scanner to free up resources and prevent memory leaks
      scanner.close();

      // Display the appropriate message
      System.out.println("<< Closing The Scanner Object... Exiting!!! > > \n");

    }
  }
}
```

> [!NOTE] Importing Java Utility Package
> Yes, if you are going to use `InputMismatchException`, you are going to **have** to `import` the Java utility package `java.util.InputMismatchException`.

> [!TIP]
> If you don't know the exception's name; just run the code!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!