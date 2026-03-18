---
id: Javascript - Node Version
aliases: Using Node Version Of Javascript
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

- [[#Browser V/S Node]]
	- [[#The Package Manager and Package Runner]]
- [[#Writing Some Code]]

---

> [!INFO]
>
> - https://www.youtube.com/watch?v=klen07C1M-c
>
> As you know the *Javascript* version found in the browser is **different** from the version that '[Node](https://nodejs.org/en)' uses.
>
> Both are **interpreted** languages; Node was designed for the [Chrome](https://www.google.com/chrome/) Browser built on Google's *V8* engine ( *not the actual engine with 'pistons', 'cams'* ); The engine is a Javascript engine written with 'C++'.
>
> If you think about it... Javascript is a *browser language* and you are going to **need** the browser "*engine*" to be able to write the Javascript code.
>
> > The 'Console' that all the browser in the world offers!
>
> Therefore, similar to something like '[[Learning/Python/Python Data View|`python`]]' that allows us to *run* Python code on our machine. `node` does the **same** thing whereby it allows you to write Javascript code and run it on your machine using its 'Runtime Environment'.
>
> > Hence, let's actually get started with some code writing!
>

# Browser V/S Node

> [!NOTE] My Browser!
> Instead of using Chromium based browsers, I use a version / *flavour* of Firefox called [Zen](https://zen-browser.app/)
>
> > Really cool 'Arc' rip-off!
> >

Go ahead and open the 'Console' found in your browser and also the `node` [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop) in your terminal.

> [!INFO] Some **Similarities**
> look at the code given below, you are going to see that in **both** the browser version and the `node` version... We get the **same** output!
>
> ```js
> // declare and intialise an integer number
> let someNum = 69;
>
> // display a little message
> console.log(`Never Gonna ${someNum} You! Never Gonna Give You Up!`);
> ```
>
> > [!SUCCESS] Browser Output
> >
> > ```console
> > Never Gonna 69 You! Never Gonna Give You Up!
> > ```
>
> > [!SUCCESS] Node Ouptut
> >
> > ```console
> > Never Gonna 69 You! Never Gonna Give You Up!
> > ```
>
> > As you can see **both** the *outputs* are the **same**!
>

> [!INFO] Some **Differences**
> As you know, in the Javascript "*browser*" version; we have access to something called the '*DOM*'. There we have the `window` [[Javascript - Objects | object]]. Let's try to run the following code found below:
>
> ```js
> window
> ```
>
> > The output is going to be long ( *that's what she said* )... Going to only display the *first* output!
>
> > [!SUCCESS] Browser Output
> >
> > ```console
> > Window
> > ```
>
> > [!BUG] Node Ouptut
> >
> > ```console
> > Uncaught ReferenceError: window is not defined
> > ```
>

## The Package Manager and Package Runner

> [!INFO] Resource(s)
> - https://www.npmjs.com/package/npm
> - https://docs.npmjs.com/
> - https://www.youtube.com/watch?v=UYz-9UaUp2E

Node comes with the `npm` package *manager* and also the `npx` package *runner*.

### Package Manager

- Example: Install [Typescript](https://www.typescriptlang.org/) *inside* a **project**

```bash
npm install typescript --save-dev
```

> [!SUCCESS]
> In this case, I *ran* the above command in my `~/Desktop/node_test` folder and this is the output that I get after I use the `npm list` command.
>
> ```console
> testing@ /home/username/Desktop/node_test
> └── typescript@5.
> ```
>
> Additionally, I now have the following *directory* and *files* in that `~/Desktop/node_test` folder:
>
> ```console
> ──  node_modules
> ├──  package-lock.json
> └──  package.json
> ```

- Example: Install [Typescript](https://www.typescriptlang.org/) *inside* a **globally** on our system:

```bash
sudo npm install -g typescript
```

> [!SUCCESS]
> In this case, I *ran* the above command in my `~/Desktop/node_test` folder and this is the output that I get after I use the `npm ls -g` command.
>
> ```console
> /usr/lib
> ├── @qwen-code/qwen-code@0.1.2
> ├── node-gyp@11.5.0
> ├── nopt@7.2.1
> ├── npm@11.6.2
> ├── pnpm@10.19.0
> ├── semver@7.7.3
> └── typescript@5.9.3
> ```
>
> As you can clearly see, I have all of these packages installed **globally** on my system using the `npm` package manager.
>

### Package Runner

The package runner allows us to *use* a package **without** installing it!

> Actually so helpful!

I currently **don't** have the 'cowsay' installed on my system:

```console
cowsay not found
```

Therefore, let's **temporarily** install the `cowsay` *command* and display a little message.

- Run the following command:

```bash
npx cowsay "Mooo World"
```

- The output after running the above command is going to be:

```console
 ____________
< Mooo World >
 ------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

> I get the **same** output as *above* if I run the `which` command again!

## Initialising A Project

To initialise a project with 'Node', we can run the following command:

```bash
# initialise a project ( faster way )
npm init -y
```

> [!NOTE] The Interactive Way!
> If you want an interactive version that will fill out some of *values* for you. Then you should run it with the `npm init` command only ( _**without** the `-y` flag_ )!

```console
Wrote to /home/username/Desktop/testing/package.json:

{
  "name": "testing",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "type": "commonjs"
}
```

- This is the file that it created inside the *project*:

```console
 .
└──  package.json
```

### The Package JSON File

The `package.json` file is the heart of the a 'Node' project. It defines the:

- Project Metadata
- Dependencies
- Scripts

- I am now going to go ahead fill out some of the details in my `package.json` file:

```json
{
  "name": "testing",
  "version": "1.0.0",
  "description": "This is a testing space for learning about 'Node'",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [
    "test",
    "testing",
    "learning",
    "basics"
  ],
  "author": "S.Sunhaloo",
  "license": "ISC",
  "type": "commonjs"
}
```

#### Javascript Version

> [!INFO] Resource(s)
> - https://en.wikipedia.org/wiki/CommonJS
> - https://en.wikipedia.org/wiki/ECMAScript

There are *two* version of *node syntax* the `commonjs` and `module`. The *old* way is 'CommonJS' and the new way is 'ECMAScript'!

> As with everything with Software Engineering and Computer Science. There are **no** *good* or *bad*!

The company that I am currently doing my internship at is using `commonjs` / 'CJS' in the **back-end** due to its *scalability*, *stability* and *maintainability*. Then for the **front-end** they use `module` / 'ECMAScript' as most ( *if all not* ) **browsers** uses that!

> Hence, I am just going to let the *key-value* pair `type` be `commonjs`.

---

# Writing Some Code

Let's go ahead and write some code that is going to emulate this Python code:

```python
# ask the user to enter some ID of some users
def enter_ids():
    # declare list to hold ID's of users
    user_ids: list[str] = []

    # loop through the `while` loop indefinitely
    while True:
        # exception handling
        try:
            # ask the user to enter the amount of ID's to add
            user_amount = int(input("\nPlease Enter Amount Of Users: "))

            # validate the user input
            if user_amount <= 0:
                # output appropriate message
                print("\n\t<< Please Enter A Value Greater Than 0! > > ")

                # continue to ask the user to enter amount of user's ID to add
                continue

            # if the amount is valid ==> exit the `while` loop
            break

        # if the user does not enter an integer number for the amount
        except ValueError:
            # output appropriate message
            print("\n\t<< Please Enter Integer Number Only For The Amount!!! > > ")

    # iterate through the amount of user's ID to add
    for i in range(user_amount):
        # ask the user to enter the ID of user
        user_id = input("\nPlease Enter User's ID: ")

        # add / append that ID to the list
        user_ids.append(user_id)

    # finally return the list of IDs
    return user_ids


# our main function
def main():
    # call the function to get thee list of IDs
    id_list: list[str] = enter_ids()

    # display horizontal rule using the `center` function
    print("\n\t" + "-" * 50, "\n")

    # display all the IDs
    for index, value in enumerate(id_list, start=1):
        print(f"Index: {index} ==> ID: {value}")


# source the main function
if __name__ == "__main__":
    main()
```

## Converting To Javascript Node's Version

This is how I implemented the above Python code in Javscript with the Node version

> [!WARNING]
> <p align="center"> I could <strong> <span style="color: orange;"> not</span> </strong> do it!</p>
>
> The reason that I could **not** do it because I don't understand `async` and `await`.
>
> > My complete mistake!
>
> Therefore, as soon as I complete this note. I will go back and learn about `async` functions and the other good stuff.
>
> > But for now, here is my Python code *converted* to 'JS' using [Claude](https://claude.ai).
>

```js
// import the 'readline' package to allow input from the command line
const readline = require("node:readline/promises");

// process the input / output stream
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

// ask the user to enter some ID of some users
const enterIds = async () => {
  // declare variable to hold user amount of ID
  let userAmount;
  // declare list to hold ID's of users
  const userIds = [];

  // iterate through the `while` loop indefinitely
  while (true) {
    // exception handling
    try {
      // ask the user data ==> notice the `await` keyword
      userAmount = parseInt(
        await rl.question("\nPlease Enter Amount Of Users: "),
      );

      // validate the user input for amount of users
      if (userAmount <= 0) {
        // throw / raise if user enter a number less than or equal to '0'
        throw new Error("\n<< Please Enter A Value Greater Than 0!");
      }

      // check if input is actually a number
      if (isNaN(userAmount)) {
        // throw / raise an error if user entered a 'string'
        throw new TypeError(
          "\n<< Please Enter Integer Number Only For The Amount!!! > > \n",
        );
      }

      // if amount is valid ==> exit the `while` loop
      break;

      // if the user does not enter an integer number for amount
    } catch (error) {
      // output appropriate message
      console.error(`\n\t<< ${error.message} > > \n`);
    }
  }

  // iterate through the amount of user's ID to add
  for (let i = 0; i < userAmount; i++) {
    // ask the user to enter the ID of user
    const userId = await rl.question("\nPlease Enter User's ID: ");

    // add / append the ID to the list
    userIds.push(userId);
  }

  // finally return the list of IDs
  return userIds;
};

// INFO: the "main" function

// async function to be able to call the `enterIds` function with `await`
(async () => {
  const idList = await enterIds();

  // display horizontal rule
  console.log("\n\t" + "-".repeat(50) + "\n");

  // display all the IDs
  idList.forEach((value, index) => {
    console.log(`Index: ${index + 1} ==> ID: ${value}`);
  });

  // similar to Java ==> close the realine scanner
  rl.close();
})();
```

> IDK why but this took me two fucking whole hours?!?

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!