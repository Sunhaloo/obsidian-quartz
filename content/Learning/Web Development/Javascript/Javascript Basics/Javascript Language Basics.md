---
id: Javascript Language Basics
aliases: Javascript Language Basics ( The Language Itself )
tags:
  - CSS
  - HTML
  - JS
  - basics
author: S.Sunhaloo
date: 2025-08-25
status: Completed
---

## List of Contents

- [[#Alert Me Up]]
- [[#Declaring Variables]]
- [[#Basic Data Types]]
	- [[#Type Cast]]
- [[#Display Stuff On Screen]]
- [[#User Inputs]]
- [[#Conditions]]
- [[#Loops]]
- [[#Functions]]
- [[#Arrow Functions]]
- [[#Exception Handling]]

---

> [!WARNING] [Web Browsers, Web Browsers and Web Browsers](https://www.youtube.com/watch?v=Vhh_GeBPOhs)
> > Use a fucking Web Browser... **Not** `node` or anything like that!
>
> There are somethings like *user inputs* and some other things that are **different** from the way that `node` does it.
>
> > Simply, stick to the **browser `console`**!!!
>

> [!INFO] Official Documentation
> - https://262.ecma-international.org/
> - https://javascript.info/
> - https://developer.mozilla.org/en-US/docs/Web/JavaScript
>
> > [!NOTE]
> > There are no **official** Javascript documentation... But the three links that I posted above are what people usually refers to.
>

# Alert Me Up

- Display Pop Message In Browser

```
// display greeting using browser pop-ups
alert("Hello World");
```

> You should see that you have a little **pop-up** saying 'Hello World'!

# Declaring Variables

The following code below will show how to *declare* variables in Javascript.

```js
// creating a variable without declaring ==> not recommended
someIntnum = 1;

// declaring and assigning values to variable using `var`
// NOTE: this is totally not recommended nowadays
var x = 1;

// re-assigning another value to the the variable `x`
x = 2;

// declaring and assigning values to variable in the modern day
let y = 3;

// re-assigning another value to the the variable `y`
// WARNING: you are not going to be able to do `let y = 4` now!!!
y = 4;

// declaring and assigning values to constant in the modern day
// INFO: yes, JS has constant and obviously we won't be able to change them
const z = 5;
```

> [!WARNING] Use `let` and `const`... **Forget** about `var`!
> If you are working with really **old** Javascript code... Then yes! You are going to have to work with `var`.
>
> But at the time of writing this... We are in modern era of Javascript; `let` and `const` gives us a lot of safety when it comes to declaring variables.
>
> > As working with `var` inside **functions** and things like **loops** is a sure-fire way to have problems!
>
> > [!TIP] `const` For Most Variables!
> > For most *one-time-use* variables like `message` and others. It is recommended to use `const`ants instead of `let`!
> >
> > That is why we see, for example, in an [Obsidian Plugin](https://github.com/cyanheads/obsidian-mcp-server/blob/main/src/mcp-server/transports/httpTransport.ts); we see that they use `const` for more than `let`!
>

- Below you are going to find an example of using `var` compared to using `let`:

```js
// to show how `var` acts when first declared inside a statement / function
if (true) {
  // declare and assign variable using `var`
  var someVarVariable = "Declare And Assigned Using `var`!!!";

  // display the values of `some_var_variable` inside the `if` statement
  console.log("`var` Content ( Inside `if` ): %s", someVarVariable);
}

// display the values of `some_var_variable`
console.log("`var` Content ( Outside `if` ): %s", someVarVariable);

// to show how `var` acts when first declared inside a statement / function
if (true) {
  // declare and assign variable using `let`
  let someLetVariable = "Declare And Assigned Using `var`!!!";

  // display the values of `some_let_variable` inside the `if` statement
  console.log("`let` Content ( Inside `if` ): %s", someLetVariable);
}

// display the values of `some_let_variable` outside the `if` statement
console.log("`let` Content ( Outside `if` ): %s", someLetVariable);
```

- This is the output of the above code:

```console
`var` Content ( Inside `if` ): Declare And Assigned Using `var`!!!
`var` Content ( Outside `if` ): Declare And Assigned Using `var`!!!
`let` Content ( Inside `if` ): Declare And Assigned Using `var`!!!

VM100:23 Uncaught ReferenceError: someLetVariable is not defined
    at <anonymous> :23:51
```

> [!BUG]
> As you can see `var` will cause many problems if, for example, *declared* **outside** a function and then *used* **inside** a function!
>
> Additionally, we can do something like this in Javascript which I think that this is totally crazy and unncessary!
>
> ```js
> // display variable even before declaring
> console.log(grettings);
>
> // its now that we are going to declare and assign value using `var`
> var grettings = "Hello World";
> ```
>
> Nevertheless, this just going to display `undefined` ( *but still...* )!
>
> > Not even Python let you so something like that!
>
>

> With that we can now move onto **Data Types**!

# Basic Data Types

```js
// single line comment

/*
This is a multi-line
comment. Very nice!
Useful for writing "documentation" for somethings
*/
```

```js
// initialisation of variables without 'type hinting' or 'type annotation'
let nullVar = null;
let num = 69;
let floatingNum = 6.9;
let characterThingy = "A";
let someText = "Some Text Here";
let trueFalse = false;

// "multiple assingment"
let [x, y, z] = ["What!", "What!", "What!"];
let [lewisHamilton, sebastienVettel, maxVerstappen] = [44, 5, 33];
```

- Using the `typeof` function:

```js
// display the data types of each of these variables
console.log(typeof nullVar);
console.log(typeof num);
console.log(typeof floatingNum);
console.log(typeof characterThingy);
console.log(typeof someText);
console.log(typeof trueFalse);
```

> That is the reason that I have added this because its **not** really *function*... More of a *keyword*!

- This is going to output something this:

```console
object
number
number
string
string
boolean
```

> [!NOTE]
> Look at how we **don't** have `int` or `float`... Instead we just have a "*generic*" data type called `number` for... Well *numbers*!

> [!WARNING] Double Equality and Triple Equality
> Now, let's say that we do something like this in Python:
>
> ```console
> print(5 == 5)
> print(5 == "5")
> print(5 == "5.00")
> ```
>
> Only the **first** one is going to *return* `True` while the **rest** is going to *return* `False`!
>
> Now, let's try to do the **same** exact thing in Javascript!
>
> ```js
> console.log(5 == 5);
> console.log(5 == "5");
> console.log(5 == "5.00");
> ```
>
> - This is the output of the above program:
>
> ```console
> true
> true
> true
> ```
>
> > [!BUG] All `true`!!!
> > Yes the **double** equality symbols is going to *return* `true` as it tries to **convert** both data into the same datatype!
> >
> > > This is why it give us `true` for **all** of them!
> >
> >
>
> > [!SUCCESS] The Solution?
> > Javascript has something called the "*triple equals*" that is going to check if two <strong> <span style="color: orange;"> values</span> </strong> .
> >
> > Therefore, if we replace the double equality with triple equality like so:
> >
> > ```js
> > console.log(5 === 5);
> > console.log(5 === "5");
> > console.log(5 === "5.00");
> > ```
> >
> > - This time... The output is going to look like this:
> >
> > ```console
> > true
> > false
> > false
> > ```

## Type Cast

The following code block below is going to show how we do *type casting* in Javascript.

```js
// declare some variables to covert to other data types
let number = 69;
let decimalNumber = 6.9;
let stringNumber = "1234";

// change the above variables to another data type
let floatNum = parseFloat(number);
let intNum = parseInt(decimalNumber);
let intStrNum = parseInt(stringNumber);

console.log(typeof floatNum);
console.log(typeof intNum);
console.log(typeof intStrNum);
```

# Display Stuff On Screen

The code block below is going to show ways that we can display *data* / variables on the console.

```js
// declare and assign data to integer variable
let racingNumber = 27;
// declare and assign data to string variable
let driverName = "Ayrton Senna";

// "normal" way of displayig data types
// this is pretty much available in most programming language
console.log(driverName + " racing number was " + racingNumber);

// this is similar to Python's way of displaying data using `printf`
// its actually more similar to something like Bash
console.log(`${driverName} racing number was ${racingNumber}`);

// basically C-style `printf` function
console.log("%s racing number was %d", driverName, racingNumber);
```

# User Inputs

The code block found below is basically the same as [[Python Language Basics#Convert At Input Function | converting at input function ( from Python )]] itself!

```js
// exception handling
try {
  // ask the user to enter an integer value ( base 10 number )
  let user_int = parseInt(prompt("\nPlease Enter Integer Value: "), 10);

  // manually check if the input is actually a number by conversion
  if (Number.isNaN(user_int)) {
    // meaning that the conversion has failed ==> not integer value
    // INFO: therefore, we have to manually raise the error ourselves
    throw new TypeError("Please Enter Integer Values Only!!!");
  }

  // if the user input is correct ( conversion correct ) ==> display the output
  console.log(
    `\n\tCurrent Input = ${user_int} | Data Type Of Input: ${typeof user_int}`,
  );
} catch (e) {
  // if the user did not enter integer values
  // output appropriate message
  console.log(`\n\t<< Error: ${e.message} > > `);
}
```

# Conditions

## `if` Statements

```js
// ask the user to enter an integer value ( base 10 number )
let user_age = parseInt(prompt("\nPlease Enter Your Age: "), 10);

// WARNING: as we trying to mimic the Python code... `int(input("..."))` is going
// to raise errors and terminate the program if the user does not enter an integer value
// therefore, we have to add the check with the `Number.isNaN` function
if (Number.isNaN(user_age)) {
  // display an little error message ( without any `try... catch`)
  console.error("\n\t<< Error! Please Enter Integer Numbers Only!!! > > \n");

  // check if the user is any adult
} else if (user_age > = 18 && user_age < 100) {
  // output appropriate message
  console.log("You Are An Adult");

  // if the user entered an age less than or equal to '0'
} else if (user_age <= 0) {
  // output appropriate message
  console.log("Error!");

  // if the user's age is greater or equal to '100'
} else if (user_age > = 100) {
  // output appropriate message
  console.log("Congratulations! You are about to die!!!");

  // if the user is just a child
} else if (user_age > = 1 && user_age <= 18) {
  // output appropriate message
  console.log("Where is your guardian?");
}
```

## `match` Case Statements

```js
// ask the user to enter their language of choice
let lang = prompt("What's the programming language you want to learn? ");

// check the user's input / language entered
switch (lang) {
  // if user entered 'JavaScript'
  case "JavaScript":
    console.log("You can become a Web Developer!");
    break;

  // if user entered 'Python'
  case "Python":
    console.log("You can become a Data Scientist!");
    break;

  // if user entered 'PHP'
  case "PHP":
    console.log("You can become a Backend Developer!");
    break;

  // if user entered 'Solidity'
  case "Solidity":
    console.log("You can become a Blockchain Developer!");
    break;

  // if user entered 'Java'
  case "Java":
    console.log("You can become a Mobile App Developer!");
    break;

  // if the user did not enter anything that is found above
  default:
    alert("The language doesn't matter, what matters is solving problems!");
}
```

# Loops

## `while` Loops

```js
// iterate through the while loop indefinitely
while (true) {
  // ask the user to enter their phone number
  let telNum = prompt("Please Enter Telephone Number: ");

  // check if the string contains only digits and has length of 8
  // NOTE: add `telNum` as it could be `null` or `undefined` or `""`
  if (telNum && /^\d{8}$/.test(telNum)) {
    // display the telephone number and exit the loop
    console.log(`\nYour Telephone Number is ${telNum}`);
    break;
  }
  // if the user string did not contain only numbers
  // or the length of string entered was not 8
  else {
    // output appropriate message
    console.log("\nPlease Enter Correct Telephone Number!\n");
  }
}
```

> [!WARNING]
> > There are no `isdigit` functions here!
>
> Yes, we are going to have to user [Regular Expression](https://en.wikipedia.org/wiki/Regular_expression)

## `do... while` Loops

```js
// declare variable to hold number of total items
let cartItems = 0;

// declare variable that will hold the user's input
let num;

// iterate through the do...while loop at least once
do {
  // ask the user to enter positive integer number
  num = parseInt(prompt("\nPlease Enter A Positive Integer Number: "), 10);

  // check if the user entered a negative number or invalid input
  if (Number.isNaN(num) || num <= 0) {
    // output appropriate message
    console.log("\n\t<< Please Enter Positive Numbers Only!!! > > \n");
  }

  // keep asking the user to enter positive number if negative/invalid input
} while (Number.isNaN(num) || num <= 0);

// display the number entered
console.log(`\n\t== You entered the positive number: ${num} ==\n`);
```

## `for` Loops

```js
// display 5 integer numbers from 0 to 4
let output1 = "";
for (let i = 0; i < 5; i++) {
  output1 += i + " ";
}
console.log(output1);

console.log();

// display same 5 integer numbers from 0 to 4 but in reverse
let output2 = "";
for (let i = 4; i > = 0; i--) {
  output2 += i + " ";
}
console.log(output2);

console.log();

// display numbers from 1 to 100 (inclusive)
let output3 = "";
for (let i = 1; i <= 100; i++) {
  output3 += i + " ";
}
console.log(output3);

console.log();

// display even numbers from 2 to 100 (inclusive)
let output4 = "";
for (let i = 2; i <= 100; i += 2) {
  output4 += i + " ";
}
console.log(output4);

console.log();

// display odd numbers from 1 to 100 (inclusive)
let output5 = "";
for (let i = 1; i <= 100; i += 2) {
  output5 += i + " ";
}
console.log(output5);
```

> [!INFO]
> See how we **declare** variables with the `let` keyword as they are going to be used in *loops*.

## Keywords Related to Looping

### The `break` Keyword

> [!INFO]
> This is basically the same code that if found in the [[#`while` Loops | `while`]] loop above!

```js
// iterate through the while loop indefinitely
while (true) {
  // ask the user to enter their phone number
  let telNum = prompt("Please Enter Telephone Number: ");

  // check if the string contains only digits and has length of 8
  // NOTE: add `telNum` as it could be `null` or `undefined` or `""`
  if (telNum && /^\d{8}$/.test(telNum)) {
    // display the telephone number and exit the loop
    console.log(`\nYour Telephone Number is ${telNum}`);
    break;
  }
  // if the user string did not contain only numbers
  // or the length of string entered was not 8
  else {
    // output appropriate message
    console.log("\nPlease Enter Correct Telephone Number!\n");
  }
}
```

### The `continue` Keyword

```js
// create output string that will hold the numbers
let str_nums = "";

// iterate from '0' to '10'
for (let i = 0; i < 11; i++) {
  // skip the following numbers found inside the list of numbers
  if ([2, 5, 8, 10].includes(i)) {
    continue;
  }

  // for numbers that are not inside the list --> add them to the string variable
  str_nums += i + " ";
}

// finally display the "completed" string
// INFO: use `trimEnd` function to remove the last ' ' character
console.log(str_nums.trimEnd());
```

> [!NOTE]
> Compared to Python's `print` function whereby we have the `end` parameter. The `console.log` *print* function does **not** have these *luxury*.
>
> Therefore, we are going to have to fill a `string` variable and then display its contents.

# Functions

As by now, you should be seeing that the *syntax* for Javascript is **similar** to that of [[C Language Basics | C]].

In the case of functions. The way that we write them is similar **but** given that *C* is a **declarative** language we declare the *return type* of the function.

Nevertheless, in our Javascript case, we just need to write `function` in front of the *function name*!

## Simple Addition Function

```js
// function that return the addition of 2 numbers
function add(a, b) {
  // return the result of the calculation
  return Number(a) + Number(b);
}

// call the function on its own
console.log(`\tRan directly From \`console.log\` Function: ${add(5, 5)}`);

// create a variable and call the function
let sum_2_nums = add(1, 1);

// output the result to the user
console.log(`\tFunction's Value Assigned to a Variable: ${sum_2_nums}`);
```

## Palindrome Function

```js
// function to check if a string is a palidrome
function palindromeChecker(str) {
  return (
    // convert the string to lowercase and replace all <Space> character
    str.toLowerCase().replaceAll(" ", "") ===
    // convert the string to lowercase and replace all <Space> character
    // WARNING: not Python ==> need to covert to array with `split`, reverse then join
    str.toLowerCase().replaceAll(" ", "").split("").reverse().join("")
  );
}

console.log(
  `\tRan Directly From 'print' Function: ${palindromeChecker("Nurses Run")}`,
);
console.log(`\n\tIs '1001' a Palindrome: ${palindromeChecker("1001")}`);
console.log(`\tIs 'Your Mama' a Palindrome: ${palindromeChecker("Your Mama")}`);
```

> [!WARNING] The `.split` Function In Javascript!
> How can we convert the following `text = "string"` into a *list* in Python?
>
> We just basically call the `list` function and **convert** the string *variable* into a list of characters
>
> Hence, if we do something like `list(text)`, we should get this very output right here:
>
> ```console
> ['s', 't', 'r', 'i', 'n', 'g']
> ```
>
> But what if we have something like this `text = "s,t,r,i,n,g"`; how can we convert the following into a list but *split* by the `,` characters!
>
> Therefore, we need to use the `.split` function like this: `text.split(",")`. This time the output that we should get should be like this:
>
> ```console
> ['s', 't', 'r', 'i', 'n', 'g']
> ```
>
> > **Same Output**!!!
>
> > [!INFO] What is *different* in Javascript?
> > There are **no** `list` datatype in Javascript! But `string` datatype is similar to the `str` datatype whereby we can, for example, iterate over it using a `for` loop!
> >
> > Hence, to be able to **convert** a `string` variable to a `list` / array like above with what we did in Python.
> >
> > ```js
> > // the string variable that needs to be splitted into its individual characters
> > const text = "string";
> >
> > // declare variable that is going to hold the array of characters
> > let char_arr = text.split("");
> >
> > // display the result on the browser console
> > console.log(char_arr);
> > ```
> >
> > Thus, we should see that we get the **same** output as our Python *code*
> >
> > ```console
> > ['s', 't', 'r', 'i', 'n', 'g']
> > ```

> [!WARNING] The `.replace` Function In Javascript!
> Compared to our `.replace` function in Python which is going to replace **all** instances of *that* word!
>
> The `.replace` function in Javscript is only going to replace a single time!
>
> ```js
> // our string variable that is going get replaced with some words
> const text = "hello world hello word";
>
> // replace the words and display the result on the browser console
> console.log(text.replace("hello", "REPLACED"));
> ```
>
> This is actually going to return the following output:
>
> ```console
> REPLACED world hello word
> ```
>
> > [!INFO] Using Regular Expression
> > Therefore, if we want to replace **all** instance of the word `hello`... We *could* use 'regex' to be able to replace **all** of them!
> >
> > ```js
> > // our string variable that is going get replaced with some words
> > const text = "hello world hello word";
> >
> > // replace the words and display the result on the browser console
> > console.log(text.replace(/hello/g, "REPLACED"));
> > ```
> >
> > Therefore after replacing the first argument with `/hello/g`, we should see that our output now have the word `hello` replaced **everywhere**!
> >
> > ```console
> > REPLACED world REPLACED word
> > ```
> >
>
> > [!INFO] Just Use The Fucking `.replaceAll` Function Instead!
> > - Hence, if we go ahead and use the `.replaceAll` instead of the `.replace` function:
> >
> >
> > ```js
> > // our string variable that is going get replaced with some words
> > const text = "hello world hello word";
> >
> > // replace the words and display the result on the browser console
> > console.log(text.replaceAll("hello", "REPLACED"));
> > ```
> >
> > Therefore after replacing the first argument with `/hello/g`, we should see that our output now have the word `hello` replaced **everywhere**!
> >
> > ```console
> > REPLACED world REPLACED word
> > ```

## Recursive Function

```js
// function to calculate the factorial of a positive integer number
function factorial(num) {
  // create new variable to try to convert the parameter into a number
  let int_num = parseInt(num);

  // check if convertion has been successful
  if (Number.isNaN(int_num)) {
    // throw a little error
    throw new TypeError(
      "\n\t<< Parameter Could Not Be Converted To Integer Datatype!!! > > \n",
    );
  }

  // check for the base case
  if (int_num === 1) {
    return 1;

    // if the number is greater than 1
  } else {
    // find the factorial of the number by solving sub-problems
    return int_num * factorial(int_num - 1);
  }
}

// ask the user to to enter a number ( no need to convert here )
const user_num_input = prompt("\nPlease Enter An Integer Number: ");

// call the function and assign the "returned" output to a variable
const factorial_ans = factorial(Math.abs(user_num_input));

// display the result of the factorial function
console.log(
  `\n\t<< The factorial of ${Math.abs(user_num_input)} = ${factorial_ans} > > \n`,
);
```

# Arrow Functions

Take a look at this simple function below:

```js
// function that is going to take a user's name as parameter
function sayHello(userName) {
  // check if the user correctly entered his username
  if (typeof userName === "string" && userName.trim().length > 0) {
    // actually greet the user
    console.log(`Hello ${userName.trim()}!`);
  } else if (userName === null) {
    console.log("Input canceled. No greeting provided.");
  } else {
    console.log("Hello, Mysterious User! Please provide a name.");
  }
}

// ask the user to enter his username
const usersName = prompt("Please enter your name:");

// call the function to greet the user
sayHello(usersName);
```

- This is going to display something like this:

> If the user does not **cancel** ( *meaning `userName == null`* ) and user does not enter `""` ( *runs the `else` code block* )...

```console
Hello S.Sunhaloo!
```

## Converting To Arrow Functions

This is the **same** exact code found above but just using **Arrow Functions**!

```js
// arrow function that is going take a user's name as parameter
const sayHello = (userName) => {
  // check if the user correctly entered his username
  if (typeof userName === "string" && userName.trim().length > 0) {
    // Using template literals for interpolation
    console.log(`Hello ${userName.trim()}!`);
  } else if (userName === null) {
    console.log("Input canceled. No greeting provided.");
  } else {
    console.log("Hello, mysterious user! Please provide a name.");
  }
};

// ask the user to enter their username
const usersName = prompt("Please enter your name:");

// call the function to greet the user
sayHello(usersName);
```

- Therefore, again, if everything goes well, you are should get the same thing as output:

```console
Hello S.Sunhaloo!
```

# Exception Handling

Compared to handling *errors* in Python, Javascript is **different** whereby it does <em> <span style="color: orange;"> not</span> </em> raise the error by itself!

## Python V/S Javascript Handling Errors

### The Way That Python Handles Errors

- Given this simple Python code:

```python
# ask the user to enter an integer number
user_num = int(input("\nPlease Enter An Integer Number: "))

# display the integer number entered by the user
print(f"\n\tNumber Entered By The User: '{user_num}'\n")
```

- After *inputting* the value `Hello World` into the prompt:

```console
Traceback (most recent call last):
  File "/home/username/Desktop/Web/JS-Learning/main.py", line 2, in <module>
    user_num = int(input("\nPlease Enter An Integer Number: "))
ValueError: invalid literal for int() with base 10: 'Hello World'
```

> This is what we should be expecting as 'Hello World' is a `str`ing!

### The Way That Javascript Handles Errors

- Mimic the above code in Javascript:

```js
// ask the user to enter an integer number
user_num = parseInt(prompt("\nPlease Enter An Integer Number: "));

// dislay the number entered by the user
console.log(`\n\tNumber Entered By The User: '${user_num}'\n`);
```

- After *inputting* the value `Hello World` into the prompt:

```console
Number Entered By The User: 'NaN'
```

> [!WARNING] You See **No** Errors
> As you can see, we *expected* that `parseInt` would **raise** an error as I entered 'Hello World' into the input box!
>
> But you see that how we have `NaN` as the *output*... This is because Javascript tries to covert the datatype and it cannot... In this case, it just returns a '*Not a Number*' "*value*"!
>
> > [!INFO] Raise The Error **Manually**!!!
> > In Javascript, we need to **manually** *raise* the error / do the *check* ourselves!
> >
> > > Javascript is **not** going to do it for us!
> >
>

## How To Do Exception Handling in Javascript

Therefore, if we modify the above code to something like this:

```js
// ask the user to enter an integer number
user_num = parseInt(prompt("\nPlease Enter An Integer Number: "));

// check if the value inside the variable `user_num` is an integer number
if (Number.isNaN(user_num)) {
  // meaning that the user did not enter an integer value ==> raise / throw an error
  // INFO: similar to how Python has things like `ValueError` and others
  // --> JS's is same same but different therefore, just google the apporpriate one
  throw new TypeError("\n\t<< Please Enter Integer Numbers Only!!! > > \n");
}

// dislay the number entered by the user
console.log(`\n\tNumber Entered By The User: '${user_num}'\n`);
```

- Hence, in this case, we can see that our *error* has been "*raised*":

```console
Uncaught TypeError: 
	<< Please Enter Integer Numbers Only!!! > >
```

> [!INFO]
> But that's **no** *exception handling*!
>
> This is where the syntax for [[Java Language Basics#Exception Handling | Java]] comes into play!
>
> Yes the way that Java does '*exception handling*' is the **same** as to how Javascript does it!

### The Actual Syntax For Exception Handling

```js
// exception handling
try {
  // ask the user to enter an integer number
  user_num = Math.abs(parseInt(prompt("\nPlease Enter An Integer Number: ")));

  // check if the value inside the variable `user_num` is an integer number
  if (Number.isNaN(user_num)) {
    // meaning that the user did not enter an integer value ==> raise / throw an error
    // INFO: similar to how Python has things like `ValueError` and others
    // --> JS's is same same but different therefore, just google the apporpriate one
    throw new TypeError("\n\t<< Please Enter Integer Numbers Only!!! > > \n");
  }

  // dislay the number entered by the user
  console.log(`\n\tNumber Entered By The User: '${user_num}'\n`);

  // if the user does not enter an integer value
} catch (error) {
  // output an appropriate message
  console.log(`\n\t<< Error: ${error.message} > > \n`);

  // the code block that is always executed regardless of error found or not
} finally {
  // display a little horizontal rule
  console.log("\n\t" + "-".repeat(50));
}
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!