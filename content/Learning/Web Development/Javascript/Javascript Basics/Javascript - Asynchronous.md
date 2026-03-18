---
id: Javascript - Asynchronous
aliases: Promises, Fetch, Async and Await in Javascript
tags:
  - CSS
  - HTML
  - JS
  - basics
  - node
author: S.Sunhaloo
date: 2025-11-05
status: Completed
---

## List of Contents

- [[#Callback Functions]]
- [[#Callback Hell!]]
- [[#Promises]]
- [[#The Actual Asynchronous Functions]]

---

> [!INFO] Resource(s)
> > Just search for 'Bro Code' video's about this... Its basically his code!
>

> [!INFO] What Do We Learn First?
>
> ```mermaid
> graph LR
>    A[Callbacks] --> B[Promises];
>    B --> C[Async / Await];
> ```
>
> Before we start learning about things like `async` and `await`... Let's look at it fundamentally.
>
> If you think about it in a *highly* abstracted way... Everything comes down to the `callback` functions which is the root of `async` and `await`!

> [!INFO] Resource(s)
> - https://www.youtube.com/watch?v=i2SPq-nb3NQ

# Callback Functions

> A function passed as **argument** to another function!

Yes, this is what callbacks are basically are! *Most* of the back-end work is **asynchronous**. And back in the day, there was no `async` keywords... We had to manually use the `setTimeout` function to *slow down* / **wait** for a another *process* to complete.

```js
// function to greet the user when entering building
const entering = () => {
  // greet the user
  console.log("Hello!");
};

// function to greet the user when leaving building
const leaving = () => {
  // greet the user
  console.log("GoodBye!");
};

// user entering the building
entering();

// user leaving the building
leaving();
```

If we were to run the above code, you are going to see that and *expect* that function `entering` is going to run **first** and then the `leaving` function is going to run. Hence we should and need to get an output like this:

```console
Hello!
GoodBye!
```

## Adding A Delay...

Let's say an elderly person like [Steven Hawking](https://en.wikipedia.org/wiki/Stephen_Hawking) is coming along slowly but surely... Therefore we **cannot** tell him 'GoodBye!' even *before* entering the building!

- If Steven is coming through:

```js
// function to greet the user when entering building
const entering = () => {
  // fucking steven hawking is coming through
  setTimeout(() => {
    console.log("Hello!");
  }, 3000);
};

// function to greet the user when leaving building
const leaving = () => {
  // greet the user
  console.log("GoodBye!");
};

// user entering the building
entering();

// user leaving the building
leaving();
```

> The `setTimeout` function is basically the `sleep` function from the 'time' module found in Python!

- This is a massive issue!

```console
GoodBye!
Hello!
```

### Fixing The Delay

Let's say that even if someone as fast as [Usain Bolt](https://en.wikipedia.org/wiki/Usain_Bolt) is coming through or *your mama* is coming through! We *always* want the `entering` function to execute **first** and then the `leaving` function.

- Hence, the code is going to look like this:

```js
// function to greet the user when leaving building
const leaving = () => {
  // greet the user
  console.log("GoodBye!");
};

// function to greet the user when entering building
const entering = (callback) => {
  // if someone that walks slowly comes through
  setTimeout(() => {
    console.log("Hello!");

    // call the `leaving` function to greet the user using `callback`
    callback();
	
  }, 3000);
};

// greet the user when entering the building and then leaving building
entering(leaving);
```

- Thus, this is going to always display the output of the `entering` function first:

```console
Hello!
GoodBye!
```

> [!WARNING]
> You need to use the `callback()` function **inside** the `setTimeout` function!
>
> > Else the `leaving` function will **never** be called!
>

### Example - Adding and Displaying Result Of Addition

- Here is another example of how to use `callback`:

```js
// function to display the addition of 2 numbers
const displaySum = (addResult) => {
  // display the result on the screen
  console.log(`\n\t<< Result Of Addition: ${addResult} > > \n`);
};

// function to add 2 numbers
const add = (callback, firstNum, secondNum) => {
  // add the 2 numbers together
  let addResult = firstNum + secondNum;

  // call the display function after performing calculation
  callback(addResult);
};

// add the 2 numbers and then display the
add(displaySum, 9, 10);
```

- Therefore, we are always going to *add* **first** and **then** *display*:

```console
	<< Result Of Addition: 19 > >
```

# Callback Hell!

Let's say that we have a lot of functions that are needed to run **sequentially**.

- Take a look at this code:

```js
// declare first function
const firstFunction = () => {
  console.log("Function 1 Completed!");
};

// declare second function
const secondFunction = () => {
  console.log("Function 2 Completed!");
};

// declare third function
const thirdFunction = () => {
  console.log("Function 3 Completed!");
};

// declare forth function
const forthFunction = () => {
  console.log("Function 4 Completed!");
};

// run the function sequentially and in order
firstFunction();
secondFunction();
thirdFunction();
forthFunction();

// display a little messate too show that all functions ran successfully
console.log("\n\tAll Functions Ran Successfully!!!\n");
```

- Therefore, if we go ahead and run the above code, we should expect something like this:

```console
Function 1 Completed!
Function 2 Completed!
Function 3 Completed!
Function 4 Completed!

	All Functions Ran Successfully!!!
```

## Adding The Delay

Let's say that if the functions takes different time to run. Go ahead and use the `setTimeout` function with **different** *timeouts* in the functions that we created.

```js
// declare first function
const firstFunction = () => {
  // add a delay of 2 seconds
  setTimeout(() => {
    console.log("Function 1 Completed!");
  }, 2000);
};

// declare second function
const secondFunction = () => {
  // add a delay of 4 seconds
  setTimeout(() => {
    console.log("Function 2 Completed!");
  }, 4000);
};

// declare third function
const thirdFunction = () => {
  // add a delay of 1 seconds
  setTimeout(() => {
    console.log("Function 3 Completed!");
  }, 1000);
};

// declare forth function
const forthFunction = () => {
  console.log("Function 4 Completed!");
};

// run the function sequentially and in order
firstFunction();
secondFunction();
thirdFunction();
forthFunction();

// display a little messate too show that all functions ran successfully
console.log("\n\tAll Functions Ran Successfully!!!\n");
```

- Hence, as we expect; the functions are **not** going to run in order:

```console
Function 4 Completed!

        All Functions Ran Successfully!!!

Function 3 Completed!
Function 1 Completed!
Function 2 Completed!
```

## Fixing The Delay

Let's say that we its **crucial** for the functions to work *sequentially*. Similarly, we are going to use `callback` function here to be able to make the *required* function run in **order**.

```js
// declare first function
const firstFunction = (callback) => {
  // add a delay of 2 seconds
  setTimeout(() => {
    console.log("Function 1 Completed!");

    // call the function that needs to run
    callback();
  }, 2000);
};

// declare second function
const secondFunction = (callback) => {
  // add a delay of 4 seconds
  setTimeout(() => {
    console.log("Function 2 Completed!");

    // call the function that needs to run
    callback();
  }, 4000);
};

// declare third function
const thirdFunction = (callback) => {
  // add a delay of 1 seconds
  setTimeout(() => {
    console.log("Function 3 Completed!");

    // call the function that needs to run
    callback();
  }, 1000);
};

// declare forth function
const forthFunction = (callback) => {
  console.log("Function 4 Completed!");

  // call the function that needs to run
  callback();
};

// run the function sequentially and in order even if there is a delay in between
// INFO: this is where the name 'Callback Hell' comes from
firstFunction(() => {
  secondFunction(() => {
    thirdFunction(() => {
      forthFunction(() => {
        console.log("\n\tAll Functions Ran Successfully!!!\n");
      });
    });
  });
});
```

- Hence, we should get the same output like we did when we did **not** have the delay:

```console
Function 1 Completed!
Function 2 Completed!
Function 3 Completed!
Function 4 Completed!

        All Functions Ran Successfully!!!
```

> [!INFO]
> Hence, to **not** have these issues; they then decided to create the `Promise` **object**!
>
> > This is what we are going to be looking at next!
>

# Promises

> "*Promise me that you are going to return a value*!"

The "`Promise`" is an [[Javascript - Objects | object]] that allows us to see ( *or tell us* ) when an **asynchronous** function ( *basically a long running task* ) is completed and if successfully *ran*... Its also going to **return** its resulting *value*.

> [!INFO] **States** of `Promise`
> A `Promise` function can be / always in **three** different states:
>
> - `pending`: The asynchronous function has **not** yet started or is currently running
> - `resolved`: The asynchronous function has **successfully** completed and **holds** the *resulting* value
> - `rejected`: The asynchronous function has **failed** and not **holds** an *error* object
>  
> When a `Promise` object has completed its `pending` state and *either* returns `resolved` / `rejected`... It <strong> <span style="color: orange;"> not</span> </strong> go back to `pending` state. Instead it moves on to a "*settled*" status and **never** changes again!

> [!TIP] Basically...
> Again, like I said above; the main goal of the `Promise` object was to basically eliminate the use of `callback`s and also **prevent** *Callback Hell*.
>
> Therefore, I am going to go straight into coding as its does basically function ( *conceptually* )!

Let's take the code that we written in the "*heading*" '[[#Callback Hell!]]'!

```js
// declare first function
const firstFunction = () => {
  // make our new promise object
  return new Promise((resolve, reject) => {
    // add a delay of 2 seconds
    setTimeout(() => {
      // message that is displayed when the 'async' function is successful in its operations
      resolve("Function 1 Completed!");
    }, 2000);
  });
};

// declare second function
const secondFunction = () => {
  // make our new promise object
  return new Promise((resolve, reject) => {
    // add a delay of 2 seconds
    setTimeout(() => {
      // message that is displayed when the 'async' function is successful in its operations
      resolve("Function 2 Completed!");
    }, 2000);
  });
};

// declare third function
const thirdFunction = () => {
  // make our new promise object
  return new Promise((resolve, reject) => {
    // add a delay of 2 seconds
    setTimeout(() => {
      // message that is displayed when the 'async' function is successful in its operations
      resolve("Function 3 Completed!");
    }, 2000);
  });
};

// declare forth function
const forthFunction = () => {
  // make our new promise object
  return new Promise((resolve, reject) => {
    // add a delay of 2 seconds
    setTimeout(() => {
      // message that is displayed when the 'async' function is successful in its operations
      resolve("Function 4 Completed!");
    }, 2000);
  });
};

// use the `.then` function to be able to run the function in order
firstFunction()
  .then((value) => {
    console.log(value);
    return secondFunction();
  })
  .then((value) => {
    console.log(value);
    return thirdFunction();
  })
  .then((value) => {
    console.log(value);
    return forthFunction();
  })
  .then((value) => {
    console.log(value);
    console.log("All Functions Ran Successfully!!!");
  });
```

> Bear with me for a second!

- Therefore, if everything is successful ( *which in this case; they are*! ):

```console
Function 1 Completed!
Function 2 Completed!
Function 3 Completed!
Function 4 Completed!
All Functions Ran Successfully!!!
```

> [!NOTE]
> But in *real life*... There are going to be times like and API **not** responding that is going to send and *error* back!
>
> Therefore, we need to make use of the `reject` variable that is going to hold the *error object*.

## Completed and "Corrected" Code

### First Case - Function 4 Does Not Run

> [!NOTE]
> In this case we only set `fourthFunction` to **not** run!

```js
// declare first function
const firstFunction = () => {
  // make our new promise object
  return new Promise((resolve, reject) => {
    // add a delay of 2 seconds
    setTimeout(() => {
      // variable to be able to change running state of `firstFunction`
      const firstFunctionRun = false;

      // check if the function has been ran
      if (firstFunctionRun) {
        // no error caught ==> display the "success" message
        resolve("Function 1 Completed!");

        // if 'async' function does not run ==> some error occurred
      } else {
        reject("Function 1 Did NOT Run!!!");
      }
    }, 2000);
  });
};

// declare second function
const secondFunction = () => {
  // make our new promise object
  return new Promise((resolve, reject) => {
    // add a delay of 2 seconds
    setTimeout(() => {
      // variable to be able to change running state of `firstFunction`
      const firstFunctionRun = true;

      // check if the function has been ran
      if (firstFunctionRun) {
        // no error caught ==> display the "success" message
        resolve("Function 2 Completed!");

        // if 'async' function does not run ==> some error occurred
      } else {
        reject("Function 2 Did NOT Run!!!");
      }
      // message that is displayed when the 'async' function is successful in its operations
      resolve("Function 2 Completed!");
    }, 2000);
  });
};

// declare third function
const thirdFunction = () => {
  // make our new promise object
  return new Promise((resolve, reject) => {
    // add a delay of 2 seconds
    setTimeout(() => {
      // variable to be able to change running state of `firstFunction`
      const firstFunctionRun = true;

      // check if the function has been ran
      if (firstFunctionRun) {
        // no error caught ==> display the "success" message
        resolve("Function 3 Completed!");

        // if 'async' function does not run ==> some error occurred
      } else {
        reject("Function 3 Did NOT Run!!!");
      }
    }, 2000);
  });
};

// declare forth function
const forthFunction = () => {
  // make our new promise object
  return new Promise((resolve, reject) => {
    // add a delay of 2 seconds
    setTimeout(() => {
      // variable to be able to change running state of `firstFunction`
      const firstFunctionRun = false;

      // check if the function has been ran
      if (firstFunctionRun) {
        // no error caught ==> display the "success" message
        resolve("Function 4 Completed!");

        // if 'async' function does not run ==> some error occurred
      } else {
        reject("Function 4 Did NOT Run!!!");
      }
      // message that is displayed when the 'async' function is successful in its operations
    }, 2000);
  });
};

// use the `.then` function to be able to run the function in order
firstFunction()
  .then((value) => {
    console.log(value);
    return secondFunction();
  })
  .then((value) => {
    console.log(value);
    return thirdFunction();
  })
  .then((value) => {
    console.log(value);
    return forthFunction();
  })
  .then((value) => {
    console.log(value);
    console.log("All Functions Ran Successfully!!!");
  })
  .catch((error) => {
    console.error(error);
  });
```

- As we modified the code to have "*errors*", we should see that the `.catch` function *catches* them:

```console
Function 1 Completed!
Function 2 Completed!
Function 3 Completed!
Function 4 Did NOT Run!!!
```

### Second Case - Function 2 Does Not Run

> [!NOTE]
> In this case we only set `firstFunction` to **not** run!

```js
// declare first function
const firstFunction = () => {
  // make our new promise object
  return new Promise((resolve, reject) => {
    // add a delay of 2 seconds
    setTimeout(() => {
      // variable to be able to change running state of `firstFunction`
      const firstFunctionRun = false;

      // check if the function has been ran
      if (firstFunctionRun) {
        // no error caught ==> display the "success" message
        resolve("Function 1 Completed!");

        // if 'async' function does not run ==> some error occurred
      } else {
        reject("Function 1 Did NOT Run!!!");
      }
    }, 2000);
  });
};

// declare second function
const secondFunction = () => {
  // make our new promise object
  return new Promise((resolve, reject) => {
    // add a delay of 2 seconds
    setTimeout(() => {
      // variable to be able to change running state of `firstFunction`
      const firstFunctionRun = true;

      // check if the function has been ran
      if (firstFunctionRun) {
        // no error caught ==> display the "success" message
        resolve("Function 2 Completed!");

        // if 'async' function does not run ==> some error occurred
      } else {
        reject("Function 2 Did NOT Run!!!");
      }
      // message that is displayed when the 'async' function is successful in its operations
      resolve("Function 2 Completed!");
    }, 2000);
  });
};

// declare third function
const thirdFunction = () => {
  // make our new promise object
  return new Promise((resolve, reject) => {
    // add a delay of 2 seconds
    setTimeout(() => {
      // variable to be able to change running state of `firstFunction`
      const firstFunctionRun = true;

      // check if the function has been ran
      if (firstFunctionRun) {
        // no error caught ==> display the "success" message
        resolve("Function 3 Completed!");

        // if 'async' function does not run ==> some error occurred
      } else {
        reject("Function 3 Did NOT Run!!!");
      }
    }, 2000);
  });
};

// declare forth function
const forthFunction = () => {
  // make our new promise object
  return new Promise((resolve, reject) => {
    // add a delay of 2 seconds
    setTimeout(() => {
      // variable to be able to change running state of `firstFunction`
      const firstFunctionRun = true;

      // check if the function has been ran
      if (firstFunctionRun) {
        // no error caught ==> display the "success" message
        resolve("Function 4 Completed!");

        // if 'async' function does not run ==> some error occurred
      } else {
        reject("Function 4 Did NOT Run!!!");
      }
      // message that is displayed when the 'async' function is successful in its operations
    }, 2000);
  });
};

// use the `.then` function to be able to run the function in order
firstFunction()
  .then((value) => {
    console.log(value);
    return secondFunction();
  })
  .then((value) => {
    console.log(value);
    return thirdFunction();
  })
  .then((value) => {
    console.log(value);
    return forthFunction();
  })
  .then((value) => {
    console.log(value);
    console.log("All Functions Ran Successfully!!!");
  })
  .catch((error) => {
    console.error(error);
  });
```

- As we modified the code to have "*errors*", we should see that the `.catch` function *catches* them:

```console
Function 1 Did NOT Run!!!
```

> [!WARNING]
> As you can see, it does **not** even bother to run the other functions!

# The Actual Asynchronous Functions

Given that we have seen that too *eliminate* 'Callback Hell', we used `Promise` but then we had to **chain** the *functions* using the `then` **method**.

> Its like we are *trading* 'Callback Hell' for 'Promise Hell'!

Hence, they decided to, again, make a better version that is going to handle **asynchronous** functions. Therefore, they came up with `async` and `await`.

> Using them will allow us to write asynchronous code in synchronous manner!

> [!INFO]
> - `async`: Going to make a function **return** a `Promise`
> - `await`: Make the `async` function **wait** for a `Promise`

Therefore, we are just going to copy the above [[#Completed and "Corrected" Code | code]] and then **remove** the `then` *method chaining* that we did!

> Also, set it so that all the functions run!

```js
// declare first function
const firstFunction = () => {
  // make our new promise object
  return new Promise((resolve, reject) => {
    // add a delay of 2 seconds
    setTimeout(() => {
      // variable to be able to change running state of `firstFunction`
      const firstFunctionRun = true;

      // check if the function has been ran
      if (firstFunctionRun) {
        // no error caught ==> display the "success" message
        resolve("Function 1 Completed!");

        // if 'async' function does not run ==> some error occurred
      } else {
        reject("Function 1 Did NOT Run!!!");
      }
    }, 2000);
  });
};

// declare second function
const secondFunction = () => {
  // make our new promise object
  return new Promise((resolve, reject) => {
    // add a delay of 2 seconds
    setTimeout(() => {
      // variable to be able to change running state of `firstFunction`
      const firstFunctionRun = false;

      // check if the function has been ran
      if (firstFunctionRun) {
        // no error caught ==> display the "success" message
        resolve("Function 2 Completed!");

        // if 'async' function does not run ==> some error occurred
      } else {
        reject("Function 2 Did NOT Run!!!");
      }
      // message that is displayed when the 'async' function is successful in its operations
      resolve("Function 2 Completed!");
    }, 2000);
  });
};

// declare third function
const thirdFunction = () => {
  // make our new promise object
  return new Promise((resolve, reject) => {
    // add a delay of 2 seconds
    setTimeout(() => {
      // variable to be able to change running state of `firstFunction`
      const firstFunctionRun = true;

      // check if the function has been ran
      if (firstFunctionRun) {
        // no error caught ==> display the "success" message
        resolve("Function 3 Completed!");

        // if 'async' function does not run ==> some error occurred
      } else {
        reject("Function 3 Did NOT Run!!!");
      }
    }, 2000);
  });
};

// declare forth function
const forthFunction = () => {
  // make our new promise object
  return new Promise((resolve, reject) => {
    // add a delay of 2 seconds
    setTimeout(() => {
      // variable to be able to change running state of `firstFunction`
      const firstFunctionRun = true;

      // check if the function has been ran
      if (firstFunctionRun) {
        // no error caught ==> display the "success" message
        resolve("Function 4 Completed!");

        // if 'async' function does not run ==> some error occurred
      } else {
        reject("Function 4 Did NOT Run!!!");
      }
      // message that is displayed when the 'async' function is successful in its operations
    }, 2000);
  });
};

/// asynchronous function that is going to run our code in order
const funcRunner = async () => {
  // exception handling
  try {
    // run the first function and wait for it to complete
    const firstFuncResult = await firstFunction();
    // display the result of the first Function
    console.log(firstFuncResult);

    // run the second function and wait for it to complete
    const secondFuncResult = await secondFunction();
    // display the result of the second Function
    console.log(secondFuncResult);

    // run the third function and wait for it to complete
    const thirdFuncResult = await thirdFunction();
    // display the result of the third Function
    console.log(thirdFuncResult);

    // run the forth function and wait for it to complete
    const forthFuncResult = await forthFunction();
    // display the result of the forth Function
    console.log(forthFuncResult);

    // display a little message after all functions ran
    console.log("All Functions Ran Successfully!!!");

    // if a function could not be ran
  } catch (error) {
    // display an error message give by `rejected` to the user
    console.error(error);
  }
};

// INFO: don't forget to call the `funcRunner` function
funcRunner();
```

- Therefore the above code is going to output the following:

```console
Function 1 Completed!
Function 2 Did NOT Run!!!
```

> [!SUCCESS]
> At least, now, we know that we can *write* asynchronous code in a "*synchronous*" way!
>
> As you can see, its basically the same thing as above but in terms of its **syntax**... Its far, far cleaner!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!