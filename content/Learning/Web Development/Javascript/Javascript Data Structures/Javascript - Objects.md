---
id: Javascript - Objects
aliases: Dictionaries in Javascript ( Basically JSON Data )
tags:
  - JS
  - basics
  - data-structures
  - dictionaries
  - objects
author: S.Sunhaloo
date: 2025-10-28
status: Completed
---

## List of Contents

- [[#Javascript Objects V/S JSON]]
- [[#Creation Of Objects]]
- [[#Displaying - Accessing Objects]]
- [[#Functions And Methods Of Dictionaries]]
	- [[#Insertion Of Data]]
		- [[#Direct Assignment]]
		- [[#The Assign Method]]
		- [[#Using Spreading]]
	- [[#Removal Of Data]]
		- [[#Using The Delete Operator]]
		- [[#Remove Last Data From Object]]
		- [[#Clear An Object]]

---

> [!INFO] Dictionaries = Objects
> In this case, I am going to say that a *dictionary* is an *object* and **vice versa**!
>
> Additionally, I a '*key*' in JS is called an **Object**. I will also be using that interchangeably!

> [!WARNING] `let` and `const`
> You are going to see that most of the time, I just used `let` where I should be using `consts`!
>
> > "*I know that I am a `let`down...*"
>
> But just know that we should be using `const` for "*single use*" variables!

# Javascript Objects V/S JSON

> [!WARNING]
> They are **not** the same!

## Example Of Javascript Object

```js
// javascript object ( dictionary )
const item = {
  name: "shirt",
  "delivery-time": "1 day",
  rating: {
    stars: 4.5,
    count: 87,
  },
  fun: function function1() {
    console.log("function inside object");
  },
};
```

## Example of JSON

```json
{
  "name": "shirt",
  "delivery-time": "1 day",
  "rating": {
    "stars": 4.5,
    "count": 87
  }
}
```

Comparing both of them, you can see that in a **Javascript Object** you don't need to have the *keys* / *properties* as **string** datatype. Also we can have full fledge *functions* inside of our **object**

> While our 'JSON' file is just for storing data!

# Creation Of Objects

To create an object in Javascript, we use the `{}` characters!

```js
// objects containing some data items
let generalObj = {
  1: 1,
  2: "something",
  someNums: [69.69, 55, 27],
  set: new Set([1, 2, 3, "A", "B", "C"]),
  anObj: {
    1: "one",
    2: "two",
    3: "three",
  },
};
```

> [!NOTE] The Data Type Of Javascript Objects
> If we go ahead and run the following code:
>
> ```js
> // display the datatype of the `generalObj` object
> console.log(typeof generalObj);
> ```
>
> Then you are going to see that we get this as output:
>
> ```console
> object
> ```

> [!INFO] WTF Functions?!?
> We can even have functions inside of objects and function inside of *keys*!
>
> ```js
> // object containing functions and functions as values
> const greeter = {
>  // a simple function without any key / property
>  helloWorld() {
>    // display a message
>    console.log("\n\tHello World From Greeter Object!!!\n");
>  },
>
>  // key that hold a function as a value
>  sayHello: function greeterHello() {
>    // display a message
>    console.log("Hello World From Inside Of The Object Property!");
>  },
>
>  // just a regular property-value
>  message: "I hold a greeting function.",
> };
>
> // run the `helloWorld` function found inside the `greeter`
> greeter.helloWorld();
> // run the `greeterHello` function found inside the `greeter` object "on a property"
> greeter.sayHello();
> ```
>
> - Therefore, if we run the above code, we get the following output:
>
> ```console
>
> Hello World From Greeter Object!!!
> Hello World From Inside Of The Object Property!
> ```
>
> > [!INFO] Actually...
> > Things like `console.log` whereby the `console` is literally just and object the the `log` is the **function** of that *property*!
> >
> > ```js
> > console.log(typeof console, typeof console.log);
> > ```
> >
> > - The above is going to output:
> >
> > ```console
> > object function
> > ```

# Displaying - Accessing Objects

## Length Of Dictionaries

Take a look at the code below to find the length of our `generalObj` object!

```js
// objects containing some data items
let generalObj = {
  1: 1,
  2: "something",
  someNums: [69.69, 55, 27],
  set: new Set([1, 2, 3, "A", "B", "C"]),
  anObj: {
    1: "one",
    2: "two",
    3: "three",
  },
};

// find the length of the whole `generalObj` object
console.log(
  `Size Of Entire \`generalObj\` Object: ${Object.keys(generalObj).length}`,
);

// find the length of the inner `anObj` object found inside the `generalObj`
console.log(
  `Size Of Inner \`anObj\` Object: ${Object.keys(generalObj.anObj).length}`,
);
```

- Therefore, this is the output that we should get after *running* the above code:

```console
Size Of Entire `generalObj` Object: 5
Size Of Inner `anObj` Object: 3
```

> [!TIP]
> Like I said in my notes for '[[Python - Dictionaries#Length of Dictionaries | Python - Dictionaries]]'... The length of the *keys* should be the **same** as the length of the *values*.
>
> This is because we have a *key-value* pair(s)!

## Displaying Objects ( Key - Value )

### Displaying Whole Object

To display the **whole** object all at once, we can simply use the `console.log()` function.

```js
// object containing number-string 'key-pair' values
let intStrObj = { 1: "one", 2: "two", 3: "three" };

// display the entire object
console.log(intStrObj);
```

Therefore, we should see that we get the **whole** thing displayed to us:

```console
Object { 1: "one", 2: "two", 3: "three" }
```

### Displaying All Values Of Object

To display all the **values** *associated* with each **keys**. We can use the `Object.values` *static method*!

```js
// object containing number-string 'key-pair' values
let intStrObj = { 1: "one", 2: "two", 3: "three" };

// display all the values of the object
console.log(Object.values(intStrObj));
```

- This is what is returned to us when we output **all** the *values* of an object:

```console
Array(3) [ "one", "two", "three" ]
```

> Something similar to what we got in '[[Python - Dictionaries#Displaying All Values of Dictionary | Python - Dictionaries]]'

### Displaying Specific Values Of Object

Given that in Python I can do something like this: `int_str_dict[1]` to be able **display** the *value* of that *key*, we can also do this in Javascript!

But here there are a couple of ways to be able to do this!

> The are basically the *same* as in Python... "*Just different syntax*"!

#### Dot Notation

This is similar to doing something like `int_str_dict.get(1)` but **better** in my opinion!

```js
// object containing number-string 'key-pair' values
let intStrObj = { 1: "one", 2: "two", 3: "three" };

// display a specific value of a key using the 'dot notation'
console.log(
  `Value of Key \`1\` ( Using Dot Notation ) = '${intStrObj.1}'`,
);
```

> Ohh!!!

```console
Uncaught SyntaxError: missing } in template string
```

> [!WARNING]
> The 'Dot Notation' is <strong> <span style="color: orange;"> not</span> </strong> going to work with **numbers**!
>
> It requires something like `name`, or `id` or anything that is **not** a *number*!
>
> - Here is a little example of what I mean:
>
> ```js
> // object containing number-string 'key-pair' values
> let newIntStrObj = { one: 1, two: 2, three: 3 };
>
> // display a specific value of a key using the 'dot notation'
> console.log(
>  `Value of Key \`"one"\` ( Using Dot Notation ) = '${newIntStrObj.one}'`,
> );
> ```
>
> - Therefore, you should see that we do get the output that using the *Dot Notation*:
>
> ```console
> Value of Key `"one"` ( Using Dot Notation ) = '1'
> ```

> [!TIP] That's Why
> This is why I consider the '**Bracket Notation**' to be superior!
>
> As I can do the thing that I wanted with the **number**!

#### Bracket Notation

> The best in the business!

Given that we are still using our `intStrObj`... We can have *pass in* our "_**number keys**_" and basically use it like what we know in Python.

```js
// object containing number-string 'key-pair' values
let intStrObj = { 1: "one", 2: "two", 3: "three" };


// display a specific value of a key using the 'bracket notation'
console.log(
  `Value of Key \`1\` ( Using Bracket Notation ) = '${intStrObj[1]}'`,
);
```

- Therefore, we should **successfully** get our *value* found in that key!

```console
Value of Key `1` ( Using Bracket Notation ) = 'one'
```

> [!WARNING] What Do We Use?
> We, *by default*, use the **Dot Notation** because it is shorter and easier to use / *type*!
>
> But when something that the above happens when the *type* is **not** compatible with the 'Dot Notation' then we simply use the *more powerful* **Bracket Notation**!

### Displaying All Keys Of Object

Similarly, if we need to display all the **keys** of our object, we can simply use the `Object.keys` *static method*!

```js
// object containing number-string 'key-pair' values
let intStrObj = { 1: "one", 2: "two", 3: "three" };

// display all the keys of the object
console.log(Object.keys(intStrObj));
```

- Hence, we should get something like this:

```console
Array(3) [ "1", "2", "3" ]
```

### Displaying All Key-Value Item Of Dictionary

Similar to how we have something like `.items` method in [[Python - Dictionaries#Displaying All Key-Value Item of Dictionary | Python]]. Here the same thing is called `Object.entries`!

```js
// object containing number-string 'key-pair' values
let intStrObj = { 1: "one", 2: "two", 3: "three" };

// display all the 'key-value' pair of the dictionary
console.log(Object.entries(intStrObj));
```

- Therefore, this is what is going to be displayed:

```console
Array(3) [ (2) […], (2) […], (2) […] ]
```

> I mean... You *cannot* say that it did *not* display!


> [!WARNING] But The *Actual* Usage Is A Bit Different!
> In Python, we are used to doing something like this:
>
> ```python
> # dictionary of numbers-string ( key-value )
> int_str_dict: dict[int, str] = {1: "one", 2: "two", 3: "three"}
>
> # display all key-value pairs of the dictionary
> for key, value in int_str_dict.items():
>    # display the key and value in a nice way
>    print(f"Key: {key} | Value: {value}")
> ```
>
> - Therefore, if we were to go ahead and run the above code, you should see that we get something like this:
>  
> ```console
> Key: 1 | Value: one
> Key: 2 | Value: two
> Key: 3 | Value: three
> ```
>
> But in JS, if we were to *replicate* the above code, we should get something like this:
>
> ```js
> // display all the key-value pairs of the dictionary
> for (let [key, value] of Object.entries(intStrObj)) {
>  // display the key and value in a nice way
>  console.log(`Key: ${key} | Value: ${value}`);
> }
> ```
>
> - Hence, we should see the exact **same** thing:
>
> ```console
> Key: 1 | Value: one
> Key: 2 | Value: two
> Key: 3 | Value: three
> ```

# Functions And Methods Of Dictionaries

## Insertion Of Data

To show the insertion of data, I have created a `car` **object** that will be filled with *data* as we do along!

```js
// empty object that is going to hold data about some car
const car = {};
```

### Direct Assignment

#### Using Dot Notation

```js
// insert the following details into the `car` object ( using dot notation )
car.make = "Mazda";
car.model = "RX-7";

// display the `car` object after inserting any data into it
console.log("`car` Object AFTER Insertion Of Data: %o", car);
```

```console
Object { make: "Mazda", model: "RX-7" }
```

> I don't really know how to display this!

#### Using Bracket Notation

```js
// insert the following details into the `car` object ( using bracket notation )
car["horsepower"] = 255;
car["wheel-horsepower"] = 220;
car["crank-horsepower"] = 276;

// display the `car` object after inserting any data into it
for (let [key, value] of Object.entries(car)) {
  console.log(`Key: ${key} --> Value: ${value}`);
}
```

```console
Key: make --> Value: Mazda
Key: model --> Value: RX-7
Key: horsepower --> Value: 255
Key: wheel-horsepower --> Value: 220
Key: crank-horsepower --> Value: 276
```

> [!WARNING]
> You **cannot** do something like this here:
>
> ```js
> console.log(`\`car\` Object BEFORE Insertion Of Data: ${car}`);
> ```
>
> This is actually going to return us something like that:
>
> ```console
> `car` Object BEFORE Insertion Of Data: [object Object]
> ```
>
> This is because using `${car}` is basically doing / using the concatenate *operator* like so:
>
> ```js
> // this code will display the same thing as above
> console.log("\`car\` Object BEFORE Insertion Of Data: " + car);
> ```
>
> If you really wanted to use "*C-Style*", we can use the `%o` **format specifier** to be able to display those values!
>
> ```js
> console.log("`car` Object AFTER Insertion Of Data: %o", car);
> ```

> Here also, the 'Dot Notation' is favoured as its more simpler to work with!

### The Assign Method

This is similar to something like the [[Python - Dictionaries#Update Method | `update`]] method!

Additionally, similar to Python again, its the **first** object that is going to be *receiving* all the other data from the **other** objects.

> Yes, there can be **multiple** objects!

```js
// create another dictionary with the following key-pair values
const carBooleanData = {
  isManual: true,
  isConvertible: false,
  hasNavigation: false,
  isDailyDriver: false,
};

// use the `assign` method from `Object` to add the data found inside the `carBooleanData` to `car`
Object.assign(car, carBooleanData);

// display the `car` object after inserting any data into it
for (let [key, value] of Object.entries(car)) {
  console.log(`Key: ${key} --> Value: ${value}`);
}
```

```console
Key: make --> Value: Mazda
Key: model --> Value: RX-7
Key: horsepower --> Value: 255
Key: wheel-horsepower --> Value: 220
Key: crank-horsepower --> Value: 276
Key: isManual --> Value: true
Key: isConvertible --> Value: false
Key: hasNavigation --> Value: false
Key: isDailyDriver --> Value: false
```

### Using Spreading

> [!WARNING] Changing `const car` to `let car`!
> To be able to modify the **original** `car` object, we need to first change the way we are declaring our `car` object!

> I don't really like this one!

```js
// update our original `car` method to be able to insert more data using "spread" operator
car = {
  // spread the old data for our `car` object here
  ...car,
  // add the new data that needs to be added
  modifications: [
    "Single Turbo Conversion",
    "Aftermarket ECU",
    "Adjustable Coilover Suspension",
    "Upgraded Fuel System",
  ],
};

// display the `car` object after inserting any data into it
for (let [key, value] of Object.entries(car)) {
  console.log(`Key: ${key} --> Value: ${value}`);
}
```

- This is what we get after running that above code:

```console
Key: make --> Value: Mazda
Key: model --> Value: RX-7
Key: horsepower --> Value: 255
Key: wheel-horsepower --> Value: 220
Key: crank-horsepower --> Value: 276
Key: isManual --> Value: true
Key: isConvertible --> Value: false
Key: hasNavigation --> Value: false
Key: isDailyDriver --> Value: false
Key: modifications --> Value: Single Turbo Conversion,Aftermarket ECU,Adjustable Coilover Suspension,Upgraded Fuel System
```

## Removal Of Data

### Using The Delete Operator

This is similar to using the `pop` *method* or `del` operator from Python.

> Nevertheless, compared to the `pop` *method*... The `delete` *operator* here is **not** going to return the "*popped*" data!

```js
// Using the delete operator (mutating the original `car` object)
delete car.modifications;
delete car["horsepower"];

// display the `car` object after deleting any data from it
for (let [key, value] of Object.entries(car)) {
  console.log(`Key: ${key} --> Value: ${value}`);
}
```

- Therefore this is what we should be expecting when we use the `delete` operator:

```console
Key: make --> Value: Mazda
Key: model --> Value: RX-7
Key: wheel-horsepower --> Value: 220
Key: crank-horsepower --> Value: 276
Key: isManual --> Value: true
Key: isConvertible --> Value: false
Key: hasNavigation --> Value: false
Key: isDailyDriver --> Value: false
```

### Remove Last Data From Object

Okay, I **don't** know what I am doing and I am just going remove the last data from the object similar to what `popitem` method does from [[Python - Dictionaries#Pop Item Method | Python]]!

```js
// get all the keys into an array of keys ( of the `car` object )
const carObjKeys = Object.keys(car);

// get the last element from the array ==> meaning that its the last key of `car`
const lastKeyCarObj = carObjKeys.pop();

// if there is data present inside the `lastKeyCarObj` constant
if (lastKeyCarObj) {
  // get the value of the last key
  const lastValue = car[lastKeyCarObj];

  // delete the last key-value pair of the `car` object using `delete`
  delete car[lastKeyCarObj];

  // display the key-value paired removed
  console.log(`'Pop Item' Result: ${lastKeyCarObj} --> ${lastValue}`);

  // display the `car` object after deleting any data from it
  for (let [key, value] of Object.entries(car)) {
    console.log(`Key: ${key} --> Value: ${value}`);
  }
}
```

- Therefore, we can see that the last value is removed:

```console
'Pop Item' Result: isDailyDriver --> false

Key: make --> Value: Mazda
Key: model --> Value: RX-7
Key: wheel-horsepower --> Value: 220
Key: crank-horsepower --> Value: 276
Key: isManual --> Value: true
Key: isConvertible --> Value: false
Key: hasNavigation --> Value: false
```

### Clear An Object

Well, there are **no** `clear` *function* or *methods* here!

> The what are we going to do?

- Simply reassign the object!

```js
// clear / remove all the data from the list by reassignment
car = {};

// display the `car` object after clearing all data from it
console.log("`car` Object AFTER Clearing Of Data: %o", car);
```

- Therefore, we should see something like this:

```console
`car` Object AFTER Clearing Of Data:

Object { }
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!