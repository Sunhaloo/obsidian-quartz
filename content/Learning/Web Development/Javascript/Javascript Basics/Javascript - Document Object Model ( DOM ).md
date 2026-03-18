---
id: Javascript - Document Object Model ( DOM )
aliases: Document Object Models ( Web Development )
tags:
  - CSS
  - HTML
  - JS
  - basics
  - objects
author: S.Sunhaloo
date: 2025-10-28
status: Completed
---

## List of Contents

- [[#How HTML Tags Are Converted Into JS's Objects]]
- [[#Getting Practical]]
	- [[#Setting Up The Files]]
	- [[#Playing With Body Object]]
	- [[#Playing With Query Selector Function]]
- [[#Class Selectors]]
- [[#Identifier Selectors]]
	- [[#Example Code - Counter Button]]
	- [[#Example Code - Dark / Light Mode Button With Local Storage]]

---

> [!INFO]
> From what I see and understand its that 'Document Object Models' are the **bridge** between the HTML document and the Javascript Code!
>
> 'DOM' will allow us to HTML *tags* that are found inside our HTML tags. In the case of these *tags*... They are just Javascript **objects**.

# How HTML Tags Are Converted Into JS's Objects

> [!INFO] Resource(s)
> - https://www.w3schools.com/js/js_htmldom.asp
> - For more information about Javascript Objects; please refer to the file / note '[[Javascript - Objects]]'

- Take a look at the following heading that we created in *an* HTML file

```html
<h1 id="title"> Welcome To This Piece Of Garbage!!!</h1>
```

What JS is now going to do **internally**... Its going to create an **object** for that HTML tag. Therefore, this is going to look something this:

```js
{
  tagName: "H1",
  id: "title",
  textContent: "Welcome!",
  style: { color: "black", fontSize: "32px" },
  onclick: null,
  // ...plus lots of hidden methods & properties
}
```

> [!NOTE]
> The above explanation was given by [ChatGPT](https://chat.openai.com)... Therefore, this needs to be verified!

# Getting Practical

> [!INFO] What is the type of `document`?
> If we go ahead and run the following code, we are going to see that its going to be an `object`!
>
> ```js
> console.log(typeof document);
> ```
>
> - Therefore, we should see that we do get `object` as output:
>
> ```console
> object
> ```

## Setting Up The Files

I am now going to create an `index.html` file and its going to be basically the boilerplate.

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title> </title>
    <link href="style.css" rel="stylesheet" />
  </head>
  <body>
    <script src="script.js"> </script>
  </body>
</html>
```

For now, I am just going to `touch style.css` and leave that stylesheet empty. But create a `script.js` file and add the following content to the Javascript file.

```js
// display a little "hello world" on the `index.html` page
document.body.innerHTML = "Hello World From DOM";
```

> [!INFO] Explanation Of The Above Code!
> As you know, we have the `document` **object** and then the `body` is going to be the **property** or the *key* ( *from [[Learning/Python/Python Data View | Python]]* ).
>
> > [!WARNING]
> > The `body` is also considered as an **object**!
>
> Therefore, the `innerHTML` is going to be a **property** of the `body` object!

## Playing With Body Object

### Change The Title In The Browser

Currently the **title** that is shown inside the browser is this fucking shit `http://127.0.0.1:8080`.

Therefore, add the following line in our `script.js` file so that the title is going to change to 'Nice One Brother'.

```js
// change the title found in the tab above in the browser
document.title = "Nice One Brother";

// display the title inside the console
console.log(document.title);
```

- This is going to display the title that we just set to the browser console

```console
Nice One Brother
```

### Display The HTML Code Found Inside Body

If you want to display the "*raw*" HTML code that is found inside the `<body> ` tag, then we simply need to display the `document.body` object inside our `console.log`.

```js
// display the "raw" HTML tag of the body
console.log(document.body);
```

> [!NOTE]
> Given that I am currently using the [Zen Browser](https://zen-browser.app/), the way that the console inside this *Firefox* based browser is going to be a little **different** from the way that *Chrome* or something similar!
>
> Basically, what I am trying to say its that, it works! But I am **not** going to display the output here!

### Display The Text Found Inside Body Tag

```js
// display the "text" found inside the `body` tag
console.log(document.body.innerHTML);
```

- As we have `Hello World From DOM`; we should see that we have this very text as output:

```console
Hello World From DOM
```

### Create A Button Using Javascript

We are going to use the `innerHTML` property to create a <button> Button</button> on our HTML page.

```js
// create a button to be displayed in our HTML page
document.body.innerHTML =
  '<button> <a href="https://github.com/Sunhaloo" target="_blank"> GitHub</a> </button> ';
```

> [!SUCCESS]
> You should see a button named '*GitHub*' and when you click that button, you are going to be redirected to my GitHub page.

## Playing With Query Selector Function

The `document.querySelector` is a `function` that is going to allow us to get any **element** from the page and place it inside our Javascript!

- Go ahead and create a little button inside our `index.html` page:

```html
<button> Hello World</button>
```

- In our `script.js` file we are going to add this line of code:

```js
// get the button created on our HTML page
console.log(document.querySelector("button"));
```

- Therefore, this is going to display something our *newly* created button element

```console
<button> Hello World</button>
```

> [!WARNING] The Order Matters!
> When writing the above 2 lines in each of their respective files... I see that instead of simply having our button being displayed... I see that we still have `Hello World From DOM` text!
>
> From what I can clearly see; it that the *Javascript* `document.body` object has **precedence** over the *HTML* `button` tags!
>
> > [!SUCCESS] The Solution
> > Simply *delete* or *comment out* ( *what I did* ) the line that are actually **interacting** with our HTML page!
>

### Get The Content / Text Found Inside Button

In the above section we looked at how we were able to display the **whole** `<button> Hello World</button> ` HTML tag.

But what if we wanted to only display the *content* or *text* that is found **in between** the HTML tag!

```js
// get the content / text of the button created on our HTML page
console.log(document.querySelector("button").innerHTML);
```

- Hence, we should see that we get the text `Hello World` as output!

```console
Hello World
```

### Change The Content / Data Found Between Button HTML Tag

> I think that that thing that we are trying to achieve is self-explanatory!

```js
// change the content / text of the button created on our HTML page
document.querySelector("button").innerHTML = "Nice Button";

// then display the newly changed content to the console again
console.log(document.querySelector("button").innerHTML);
```

- Therefore this is the output that we should be receiving after that change above:

```console
Nice Button
```

# Class Selectors

Currently, we only have **one** little button in our `index.html` page. But what if we add another one? What is going to actually happen?

> [!TIP] The Answer?
> <p align="center"> <strong> Nothing</strong> </p>

From what I know and understand, its only going to *get* / *see* the first button that we created! Any other button created after our **first** button is not going to be "*selected*" by our `document.querySelector`!

> [!TIP] The Solution?
> We are going to be using **classes** ( `class` ) or **identifiers** ( `id` ) to able to *target* each specific **element** on our page!
>
> > In this heading, we are going to be focusing on using `class`es in order to *select* our target!
>

- Therefore, go ahead and create another <button> button</button> on our `index.html` file:

```html
  <!-- this is what my body looks like -->
  <body>
    <button> Hello World</button>
    <button class="second-button"> Second Button Created</button>

    <script src="script.js"> </script>
  </body>
```

- Hence, in our `script.js` file, we are going to create a variable and *play* with it:

```js
// get the second button found on our HTML page in a variable
const secondButtonElement = document.querySelector(".second-button");

// change the content / text found inside the `secondButtonElement` HTML element
secondButtonElement.innerHTML = "What A Second Button!";

// finally display the content / text inside the console
console.log(secondButtonElement.innerHTML);
```

- Thus, in our console, we should see the **correct** output and our button should be updated on our page:

```console
What A Second Button!
```

# Identifier Selectors

Similarly to [[#Class Selectors]], instead of using `class`es, we are instead going to use `id`entifiers!

> But the logic / process stays the same!

```js
// get the third button found on our HTML page in a variable
const thirdButtonElement = document.querySelector("#third-button");

// change the content / text found inside the `thirdButtonElement` HTML element
thirdButtonElement.innerHTML = "What A Third Button!";

// finally display the content / text inside the console
console.log(thirdButtonElement.innerHTML);
```

- Therefore, you should see that the button has been updated and the console display the new *value* accordingly

```console
What A Third Button!
```

## Example Code - Counter Button

This code is going to display a counter on the main 'HTML' page and there are going to be four buttons:

1. Decrement Button ( *decrement the counter* )
2. Alert / Display Button ( *use the `alert()` function to display value* )
3. Increment Button ( *increment the counter* )
4. Random Button ( *re-initialise the counter to another random value* )

- This is how my `index.html` file looks like:

```html
<!doctype html>
<html lang="en-GB">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title> Counter - Button</title>
    <link href="style.css" rel="stylesheet" />
  </head>
  <body>
    <!-- the main container that is going to contain everything -->
    <div class="main-container">
      <p class="counter"> Counter Value: <span class="counter-value"> </span> </p>

      <!-- container that is going to "hold" all of the buttons -->
      <div class="button-container">
        <button class="decrement-button"> Decrement Counter</button>
        <button class="alert-button"> Alert / Display Count</button>
        <button class="increment-button"> Increment Counter</button>
      </div>

      <!-- another button that is just going to be re-intialising the counter -->
      <div class="random-button-container">
        <button class="random-button"> Random Button</button>
      </div>
    </div>

    <!-- import the external 'script.js' file -->
    <script src="script.js"> </script>
  </body>
</html>
```

- This is how my `style.css` file looks like:

```css
/* main outer `div` tag */
.main-container {
  /* change the display the `flex` */
  display: flex;
  /* change from "main" axis to "cross" axis */
  flex-direction: column;
  /* apply a spacing between all the elements found in main container ==> everything */
  justify-content: space-evenly;
  /* center the items in the middle */
  /* NOTE: this one is used for centering the background colour of `.counter` class */
  align-items: center;
}

/* the paragraph tag inside the main `div` container */
.counter {
  /* change to `inline-block` so that background colour does not expand across */
  display: inline-block;
  /* change the background colour of the counter */
  background-color: #d6eea4;
  /* add a bit of padding around the whole counter */
  padding: 18px;
  /* change the border radius of the border */
  border-radius: 10px;
}

/* main button `div` containing the 3 buttons */
.button-container {
  /* change the display the `flex` */
  display: flex;
  /* space the buttons evenly between each other */
  justify-content: space-evenly;
}

/* button that can reset / re-initialise the counter */
.random-button-container {
  /* change the display the `flex` */
  display: flex;
  /* change from "main" axis to "cross" axis */
  flex-direction: column;
  /* apply a spacing between all the elements found in main container ==> everything */
  justify-content: space-evenly;
  /* center the items in the middle */
  align-items: center;
}

/* change the styling of the all the buttons */
button {
  /* change the background colour to black */
  background-color: black;
  /* change the border to of the button */
  border: 2px solid grey;
  /* change the border radius of the border */
  border-radius: 5px;
  /* change the colour of the text of the text */
  color: white;
  /* change the pointer of the cursor to "hand" pointer */
  cursor: pointer;
  /* change the padding of the button */
  padding: 10px;
  /* change the spacing between the buttons */
  margin: 50px;
}

/* change the styling of the all the buttons on cursor hover */
button:hover {
  /* change the background colour to black */
  background-color: grey;
  /* change the colour of the text of the text */
  color: black;
}
```

> [!INFO] Understanding Flexbox Little By Little!
> Man this video is so good at explaining `display: flexbox` is a good and clear way with practical "*show and tell*"!
>
> - Link to YouTube Video: https://www.youtube.com/watch?v=phWxA89Dy94

- This is how my `script.js` file looks like:

```js
// create a counter that is going hold a random number
let counter = Math.floor(Math.random() * 100) + 1;

// implementation of the counter on the HTML page
const spanCountElement = document.querySelector(".counter-value");

// display the counter to the main page
spanCountElement.innerHTML = counter;

// implementation of the 'alert' button
const alertBtnElement = document.querySelector(".alert-button");

// display the current count of `counter` when the user clicks the button
alertBtnElement.addEventListener("click", function () {
  // display the value of the counter `counter` to the user using `alert` function
  alert(`Current Count: ${counter}`);

  // also display the data to the console
  console.log(counter);
});

// implementation of the 'increment' button
const incrementBtnElement = document.querySelector(".increment-button");

// allow the user to increment the counter when pressing the increment button
incrementBtnElement.addEventListener("click", function () {
  // increment the counter `count`
  counter += 1;

  // update the counter on the HTML page
  spanCountElement.textContent = counter;
});

// implementation of the 'decrement' button
const decrementBtnElement = document.querySelector(".decrement-button");

// allow the user to increment the counter when pressing the increment button
decrementBtnElement.addEventListener("click", function () {
  // increment the counter `count`
  counter -= 1;

  // update the counter on the HTML page
  spanCountElement.textContent = counter;
});

// implementation of the random button
const randomBtnElement = document.querySelector(".random-button");

// allow the user to get another random number to be displayed on the page
randomBtnElement.addEventListener("click", function () {
  // get another random number
  counter = Math.floor(Math.random() * 100) + 1;

  // update the counter on the HTML page
  spanCountElement.textContent = counter;
});
```

## Example Code - Dark / Light Mode Button With Local Storage

> [!NOTE]
> There are two ways that I am came across on how to implement this. The first one is a *rudimentary* version **without** any *saving* local storage or anything like that.
>
> > Basically uses the `.innerHTML` of the button tag to check what theme we are on!
>
> Then I am going to try to code the other version with **icons**, **local storage**.

### Rudimentary Version

In this version, the page is **always** going to start on the *light mode* and then the button which is going to be *toggle-able* will allow the user to switch the theme.

- This is how my `index.html` page is going to look like:

```html
<!doctype html>
<html lang="en-GB">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title> Rudimentary Theme</title>
    <link href="style.css" rel="stylesheet" />
  </head>
  <body>
    <!-- the main container that is going to contain everything -->
    <div class="main-container">
      <button type="button" class="main-button" id="theme-button">
        Toggle Theme
      </button>
    </div>

    <!-- import the external 'script.js' file -->
    <script src="script.js"> </script>
  </body>
</html>
```

- This is how my `style.css` file is going to look like:

```css
/* setup the whole page for displaying the button in the middle of screen */
html,
body {
  /* remove all margin from the page */
  margin: 0;
  /* remove all padding from the page */
  padding: 0;
}

/* main outer `div` tag */
.main-container {
  /* change the display "rendering" to `flex` */
  display: flex;
  /* center the content of container to the center ( horizontally - main axis ) */
  justify-content: center;
  /* center the content of container to the center ( vertically - cross axis ) */
  align-items: center;
  /* move the contents of the container to the dead center ( using the viewport ) */
  min-height: 100vh;
}

/* main toggleable button that is going to switch from 'light' mode to 'dark' mode */
.main-button {
  /* add some padding around the button itself */
  padding: 10px;
  /* add a smaller border around the button */
  border: 2px solid #e29024;
  /* change the radius of the border to something appealing */
  border-radius: 10px;
  /* change the background colour of the button */
  background-color: #2476e2;
  /* change the text colour of the button */
  color: white;
  /* change the cursor to the "pointing hand" */
  cursor: pointer;
  /* add "animations" when the user is going interact with the code */
  transition: 0.22s ease;
}

/* main button but styling upon cursor 'hover' */
.main-button:hover {
  /* move the button a bit up on the page */
  transform: translate(0, -5px);
}

/* main button but styling upon cursor being 'clicked' */
.main-button:active {
  /* move the button a bit up on the page */
  transform: translate(0, 1px);
  /* change the background colour to 'white' */
  background-color: white;
  /* change the text colour to black */
  color: black;
  /* change the border colour to red */
  border-color: red;
}
```

- This is how my `script.js` file is going to look like:

```js
// get the theme button as an object
const themeBtnElement = document.getElementById("theme-button");

// add click listener event to allow button to respond on click
themeBtnElement.addEventListener("click", function () {
  // get the styling objects for the body
  const bodyStyles = window.getComputedStyle(document.body);
  // get the value of the `background-colour` property set
  const bodyBGColour = bodyStyles.getPropertyValue("background-color");

  // check if the current background colour is 'white'
  // NOTE: given that we are using `"black"` ==> use 'RGB'
  if (bodyBGColour !== "rgb(0, 0, 0)") {
    // user currently on 'light mode' ==> switch to 'dark mode'
    document.body.style.backgroundColor = "black";
    document.body.style.color = "white";

    // check if the current background colour is 'black'
  } else {
    // user currently on 'dark mode' ==> switch to 'light mode'
    document.body.style.backgroundColor = "white";
    document.body.style.color = "black";
  }
});
```

### Version With Icons And Local Storage

> [!INFO] Resource(s)
> - For more information about Local Storage; please refer to '[[Javascript - Local Storage]]'

This code is going to display a button in the middle of the page and then allow the user to be able to change from *light* mode to *dark* mode.

Compared to the above code, this one is going to have access to the *local storage*; this means that the previous *state* is going to be **saved**!

- This is how my `index.html` page is going to look like:

```html
<!doctype html>
<html lang="en-GB">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title> Local Storage</title>
    <link href="style.css" rel="stylesheet" />
    <!-- link all the material icons to be able to use icons from Google -->
    <link
      rel="stylesheet"
      href="https://fonts.googleapis.com/icon?family=Material+Icons"
    />
  </head>
  <body>
    <div class="main-container">
      <!-- create main button that is going to allow the user to toggle themes -->
      <!-- this button is also going to react to current theme of webpage -->
      <button type="button" class="main-theme-button" id="main-button">
        <i class="material-icons"> toggle_off</i>
      </button>
    </div>

    <!-- source the external JS file -->
    <script src="script.js"> </script>
  </body>
</html>
```

- This is how my `style.css` file is going to look like:

```css
/* define variables for colours */
:root {
  --light-background: #ebebeb;
  --light-text: #333333;
  --dark-background: #0d0e11;
  --dark-text: #dee4df;

  --button-background: #b1aeae;
  --button-border-colour: #268c93;
}

/* setup the whole page for displaying button in dead center */
html,
body {
  /* remove all the margin */
  margin: 0;
  /* remove all the padding */
  padding: 0;
}

/* styling for the 'light mode' version */
body {
  /* change the background colour */
  background-color: var(--light-background);
  /* add a little animation to the background colour */
  transform: 0.2s ease-in-out;
}

/* styling for the 'dark mode' version */
body.dark-mode {
  /* change the background colour */
  background-color: var(--dark-background);
}

/* style the main `div` tag */
.main-container {
  /* change the display type to `flex` */
  display: flex;
  /* center the item to the middle of the page ( horizontally ==> main axis ) */
  justify-content: center;
  /* center the item to the middle of the page ( vertically ==> cross axis ) */
  align-items: center;
  /* move the contents of the main container to the middle of the screen --> using viewport */
  min-height: 100vh;
}

/* style the main button that is going to be used to change the theme */
.main-theme-button {
  /* add some padding around the button */
  padding: 10px 28px 10px 28px;
  /* add border around the button */
  border: 2px solid var(--button-border-colour);
  /* add border radius to the button */
  border-radius: 10px;
  /* change the background colour */
  background-color: var(--button-background);
  /* change the text colour */
  color: var(--light-text);
  /* change the cursor to 'hand' */
  cursor: pointer;
  /* add a smooth animation on all property to the button */
  transition: 0.15s ease-in-out;
}

/* style the main button upon cursor 'hover' */
.main-theme-button:hover {
  /* move the button just a little bit up */
  transform: translate(0, -5px);
  /* add "more" border around the button */
  border: 3px solid var(--button-border-colour);
}

/* style the main button when clicked */
.main-theme-button:active {
  /* move the button a bit down */
  transform: translate(0, 10px);
}
```

- This is how my `script.js` file is going to look like:

```js
// get the main button that is going to handle theme change
const themeBtnElement = document.getElementById("main-button");

// get the icon of the button using `querySelector` and using the class name of `i` tag
const themeIcon = themeBtnElement.querySelector(".material-icons");

// get the theme from the local storage
let systemTheme = localStorage.getItem("theme");

// set the theme key-value pair to be 'light' in the beginning
if (systemTheme === null) {
  // default to the light theme
  systemTheme = "light";
  // set the local theme in the storage
  localStorage.setItem("theme", systemTheme);
}

// according to the user's system theme ==> set it accordingly
if (systemTheme == "dark") {
  // then change the theme on the page to dark mode
  document.body.classList.add("dark-mode");
  // then change the theme of the button to dark-mode
  themeBtnElement.classList.add("dark-mode");
  // set the icon to toggle_on for dark mode
  themeIcon.textContent = "toggle_off";

  // if the current system system is set to 'light'
} else {
  // set the icon to toggle_off for light mode
  themeIcon.textContent = "toggle_on";
}

// log / display the local theme to the console
console.log(`System Theme: '${systemTheme}'`);

// add a click event on that button
themeBtnElement.addEventListener("click", function () {
  // switch to the dark mode / version using the styling found in `style.css` file
  document.body.classList.toggle("dark-mode");

  // change the button to use the `dark-mode` styling
  themeBtnElement.classList.toggle("dark-mode");

  // get the current theme that is being used
  const isDarkMode = document.body.classList.contains("dark-mode");

  // change the icon based on the theme
  themeIcon.textContent = isDarkMode ? "toggle_off" : "toggle_on";

  // save the theme ==> when use presses the button ( using JS's ternary syntax )
  localStorage.setItem("theme", isDarkMode ? "dark" : "light");
});
```

#### Explanation Of The Above Javascript Code

- Get the *data* items that we need to be able to work with:

```js
// get the main button that is going to handle theme change
const themeBtnElement = document.getElementById("main-button");

// get the icon of the button using `querySelector` and using the class name of `i` tag
const themeIcon = themeBtnElement.querySelector(".material-icons");

// get the theme from the local storage
let systemTheme = localStorage.getItem("theme");
```

- Check if the system theme is `null` ( *meaning not 'theme' key has been stored* ) if so ==> Set the default theme to *light theme*:

```js
// set the theme key-value pair to be 'light' in the beginning
if (systemTheme === null) {
  // default to the light theme
  systemTheme = "light";
  // set the local theme in the storage
  localStorage.setItem("theme", systemTheme);
}
```

- Check if we already have a `"theme"` *key-value* **pair** ==> Setup the *whole page*, *button* and *button icon* to use the **dark** variant:

```js
// according to the user's system theme ==> set it accordingly
if (systemTheme == "dark") {
  // then change the theme on the page to dark mode
  document.body.classList.add("dark-mode");
  // then change the theme of the button to dark-mode
  themeBtnElement.classList.add("dark-mode");
  // set the icon to toggle_on for dark mode
  themeIcon.textContent = "toggle_off";

  // if the current system system is set to 'light'
} else {
  // set the icon to toggle_off for light mode
  themeIcon.textContent = "toggle_on";
}
```

- Add the functionality to the actual / *main* button:

```js
// add a click event on that button
themeBtnElement.addEventListener("click", function () {
  // switch to the dark mode / version using the styling found in `style.css` file
  document.body.classList.toggle("dark-mode");

  // change the button to use the `dark-mode` styling
  themeBtnElement.classList.toggle("dark-mode");

  // get the current theme that is being used
  const isDarkMode = document.body.classList.contains("dark-mode");

  // change the icon based on the theme
  themeIcon.textContent = isDarkMode ? "toggle_off" : "toggle_on";

  // save the theme ==> when use presses the button ( using JS's ternary syntax )
  localStorage.setItem("theme", isDarkMode ? "dark" : "light");
});
```

1. Use the `toggle` function to **toggle** between `body` and `body.dark-mode` for the **body** / whole page
2. Use the `toggle` function to **toggle** between `.main-theme-button` and `.main-theme-button.dark-mode` for the **button**
3. Check if the current theme is set / using the *dark* variant, i.e, `.dark-mode`
4. Change the **icon** of the button using the `.textContent` and ternary operation
5. Change the `"theme"` *key* of the `localStorage` using the `.setItem` and ternary operation

## Example Code - Input Text With Local Storage

> [!NOTE]
> This is going to be me learning how the `<input> ` and `<form> ` tags works together and how we can use it to actually save the data somewhere!

### Simple Form Page That Is Going To Search Google

- This is how the `index.html` file looks like:

```html
<!doctype html>
<html lang="en-GB">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title> Forms And Inputs</title>
    <link href="style.css" rel="stylesheet" />
    <!-- link / add "material" icons from Google -->
    <link
      rel="stylesheet"
      href="https://fonts.googleapis.com/icon?family=Material+Icons"
    />
    <!-- link / add 'Fira Code' font from Google -->
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@300..700&family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&display=swap"
      rel="stylesheet"
    />
  </head>
  <body>
    <!-- add a simple little heading to the page outside of the `div` tag -->

    <!-- main container that is going to contain the form and the inputs -->
    <div class="main-container">
      <h2 class="para-heading"> Giggle Search</h2>
      <!-- main form for the webpage -->
      <form
        class="main-form"
        id="main-search-form"
        action="https://google.com/search"
        target="_blank"
      >
        <!-- main input bar / box -->
        <input
          class="main-input"
          id="main-input-field"
          type="text"
          placeholder="Enter A Question"
          name="q"
        />

        <!-- the actual button that will allow use to submit name -->
        <button class="main-submit-btn" type="submit">
          <i class="material-icons"> check</i>
        </button>
      </form>
    </div>

    <!-- link the javascript file to the HTML page -->
    <script src="script.js"> </script>
  </body>
</html>
```

- This is how the `style.css` file looks like:

```css
/* setup the whole page to display the input bar at top middle of page */
html,
body {
  /* remove all the margin from the page */
  margin: 0;
  /* remove all the padding from the page */
  padding: 0;
}

/* style the main container that holds the form - input box */
.main-container {
  /* change the display method to `flex` */
  display: flex;
  /* change the direction of the "flex" to be along the cross axis */
  flex-direction: column;
  /* center the elements inside container ( horizontally ==> main axis ) */
  justify-content: center;
  /* center the elements inside container ( vertically ==> cross axis ) */
  align-items: center;
}

/* style the heading that is found .para-heading { */
.para-heading {
  /* change the display method to `flex` */
  display: inline-block;
  /* change the padding */
  padding: 8px;
  /* change the background colour to some black */
  background-color: #333333;
  /* change the text / icon colour of the button */
  color: #ebebeb;
  /* add some border radius to the button */
  border-radius: 0.8rem;
}

/* style the main form found on the page */
.main-form {
  /* change the display method to `flex` */
  display: flex;
  /* change the margin and add space at the top only */
  margin-top: 80px;
  /* center the elements inside container ( vertically ==> cross axis ) */
  align-items: center;
}

/* style the input bar */
.main-input {
  /* change the padding */
  padding: 8px;
  /* change the margin to the right ==> add some space between button */
  margin-right: 10px;
  /* remove all the border from the button */
  border: 0.1rem solid #333333;
  /* add some border radius to the button */
  border-radius: 0.2rem;
  /* change the font of the user's input */
  font-family: "Fira Code", monospace;
}

/* style the submit button */
.main-submit-btn {
  /* change the margin and add space to the left only */
  margin-left: 10px;
  /* change the padding 2px solid transparent */
  padding: 0.18rem;
  /* change the background colour to some black */
  background-color: #333333;
  /* change the text / icon colour of the button */
  color: #ebebeb;
  /* remove all the border from the button */
  border: 2px solid transparent;
  /* add some border radius to the button */
  border-radius: 0.2rem;
  /* add a little transition / animation on all the button property */
  transition: 0.1s ease-in-out;
}

/* style the submit button on cursor 'hover' */
.main-submit-btn:hover {
  /* change the background colour to some black */
  background-color: #ebebeb;
  /* change the text / icon colour of the button */
  color: #333333;
  /* add a simple border */
  border: 2px solid #333333;
}

/* style the submit button on 'click' */
.main-submit-btn:active {
  /* change the background colour to some black */
  background-color: #ebebeb;
  /* change the text / icon colour of the button */
  color: green;
  /* add a simple border */
  border: 2px solid #333333;
}
```

- This is how the `script.js` file looks like:

```js
// get the form element as a object
const formElement = document.getElementById("main-search-form");

// get the input element as an object
const inputElement = document.getElementById("main-input-field");

// check if whether the user has submitted something using and event listener
formElement.addEventListener("submit", function () {
  // get the search value from the input element / object
  const questionSearch = inputElement.value;

  // store the question asked to the local storage
  localStorage.setItem("lastQuestionSearch", questionSearch);

  // display the question entered by user to the console
  console.log(`User Entered: ${questionSearch}`);

  // finally remove the question entered from the local storage
  localStorage.removeItem("lastQuestionSearch");
});
```

> [!INFO]
> Given that the `<form> ` is the one that is responsible in **submitting** the data to *wherever* we want to.
>
> > What I am trying to say its that the `<input> ` is just for the user to enter *data*!
>
> Therefore, this is the reason as to why we add use the `addEventListener` function on the **form** itself *rather* than the `<input> ` tag!
>
> > Also you can see how we have `submit` instead of `click`!
>
> Finally, we simply get the **value** using the `.value` method from the input box and therefore, store and also remove the data from local storage after the question has been displayed to the console!


---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!j