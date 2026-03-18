---
id: TODO Application - Pure HTML, CSS and JS
aliases: Building A Simple TODO Application in Pure HTML, CSS and JS
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

- [[#Display Random Greetings]]
- [[#Get The Current Date]]
- [[#Write A TODO]]
- [[#Displaying The TODO]]
- [[#Styling]]
	- [[#Implementation Of The Toggle Theme Button]]
	- [[#CSS Syntax]]
	- [[#Colour Shifting Text Logo]]
- [[#The Actual Main Javascript]]
	- [[#Display, Username And TODO Item Code]]
	- [[#The Display Function]]
	- [[#Displaying Categories]]

---

> [!WARNING]
> For the styling, don't focus on it too much as I told [Qwen Code](https://github.com/QwenLM/qwen-code) to do it for me.
>
> This is due to the fact, that I don't really have a taste and don't know the proper *properties* and *syntax* for 'CSS'.

> [!INFO] Resource(s)
> - This file is going to referring to the note / file called '[[Javascript - Document Object Model ( DOM )]]'
> - https://www.youtube.com/watch?v=6eFwtaZf6zc
> - https://www.youtube.com/watch?v=SeKQSQDUMDQ

# Display Random Greetings

I wanted to implement this Python code into my HTML page so that it displays **different** greetings *randomly*.

- This is the Python code that I was talking about:

```python
# import the `choice` function from the 'random' module
from random import choice

# initalise list of strings that holds some greetings
greetings: list[str] = ["Hello", "Hi", "What's Up", "How's Going"]

# display a random "greet"
print(f"\n\t<< Random Greet: {choice(greetings)}! > > \n")
```

Therefore, the following code in 'JS' and 'HTML' is going to look something like this:

```js
// create an array that is going to hold some greetings that will be displayed
const greetings = ["Hello", "Hi", "What's Up", "How's Going"];

// get a random index from the `greetings` array
const randomGreetingIndex = Math.floor(Math.random() * greetings.length);

// get the `span` tag as an object
let spanHeadingGreet = document.getElementById("greetings-heading");

// display the "random" greeting on the 'HTML' page
spanHeadingGreet.innerHTML = greetings[randomGreetingIndex];
```

Hence, the above code is going to:

1. Get a random **index** using the `Math.random()` function
2. Get the `<span> ` tag / element into a Javascript object
3. Display the *random* greeting using the `.innerHTML` method

# Get The Current Date

Well as the title suggests, we are going to try to get the current date in this format `dd mm yyyy`.

- This is how the `index.html` file looks like for *this* implementation:

```html
        <h4> <span id="current-date" class="date-heading"> </span> </h4>
```

- This is the code that is going to display the current date in a specific format:

```js
// function that is going to be able to display the current date
function getCurrentDate() {
  // initalise variable that is going to hold the current date
  let currentDate = new Date();

  // split the current date into an array
  // INFO: need to convert the data object to string then use `.split`
  currentDate = currentDate.toString().split(" ");

  // get only the date, month and year
  document.getElementById("current-date").innerHTML =
    currentDate[2] + " " + currentDate[1] + " " + currentDate[3];
}

// function to display the date on the current page
window.onload = function () {
  // call the function to display the current date
  getCurrentDate();
};
```

The above code is going to work like this:

1. Create a new `currentDate` **object** from `new Date()`
2. Change the data **object** to a **string** so that we can apply the `split` function on it
3. Display on only the day number, month and year number
4. Use the `.onload` function to be able to display the *whole* function to the 'HTML' page

# Write A TODO

I am going to show you the whole `<section> ` that is going to be used for adding 'TODO'.

```html
      <section class="create-todo-section">
        <h3> Create A TODO</h3>

        <!-- our main `form` that is going to handle the user input for TODO -->
        <form class="new-todo-form">
          <h4> What Do You Want To Add?</h4>

          <!-- the actual input bar that the user is going to write TODOs -->
          <input
            id="input-todo"
            type="type"
            name="todo-content"
            placeholder="Implement AI in workflow"
          />

          <h4> TODO Category</h4>

          <!-- use the drop down menu to select TODO category -->
          <div class="category-options">
            <select class="drop-down-category" name="category" required>
              <!-- this value is already selected by default -->
              <option value="miscellaneous" selected hidden>
                ❓ Miscellaneous
              </option>

              <!-- these are the selectables category -->
              <option value="coding"> 💻 Coding</option>
              <option value="debugging"> 🐛 Debugging</option>
              <option value="testing"> ✅ Testing</option>
              <option value="documentation"> 📄 Documentation</option>
              <option value="meeting"> 👥 Meeting</option>
              <option value="learning"> 📚 Learning</option>
              <option value="refactoring"> 🔧 Refactoring</option>
              <option value="deployment"> ☁️ Deployment</option>
              <option value="code-review"> 📝 Code Review</option>
              <option value="planning"> 📅 Planning</option>
              <option value="miscellaneous"> ❓Miscellaneous</option>

            </select>
          </div>

          <!-- create a new button that is going to handle the TODO submission -->
          <button class="form-submit-button" type="sumbit">
            Add TODO
            <i class="material-icons"> check</i>
          </button>
        </form>
      </section>
```

This is how the `<form> ` is structured:

- The `<input> ` tag is going to allow the user to enter a 'TODO' that the user has to do
	- The user is **not** going to be able to submit until he / she write something
	- **NOTE**: This is going to be implemented inside the `script.js` file!
- The user is then going to be able to select from the *drop down* menu; a list of **different** categories that is available.
	- By default, the category is set to '*Miscellaneous*'
	- Therefore, the user is going to have to set another category manually if 'TODO' being added does **not** match '*Miscellaneous*'
- Finally, the user is going to able to **press** the *Submit Button* that is going to allow the TODO to be added

# Displaying The TODO

This is a **rudimentary** code that is going to display some *dumb* 'TODO'.

> [!WARNING]
> You should **not** really focus on this code below... This is going to be changed as we implement it *inside* the `script.js` file!

```html
      <!-- section of the form that is going to be displaying our TODOs -->
      <section class="todo-form-section">
        <h3> TODO List</h3>

        <!-- part of the section that is going to display the individual TODOs -->
        <div class="list" id="todo-list">
          <!-- an individual todo item -->
          <div class="todo-item">
            <label>
              <input type="checkbox" />
              <span class="bubble business"> </span>
            </label>
          </div>

          <!-- the content for the individual todo -->
          <div class="todo-content">
            <input type="text" value="Todo Item 1" readonly />
          </div>

          <!-- the actions buttons that are going to be associated with each TODO -->
          <div class="todo-action">
            <button class="todo-edit-button"> Edit</button>
            <button class="todo-delete-button"> Delete</button>
          </div>
        </div>

        <!-- part of the section that is going to display the individual TODOs -->
        <div class="list" id="todo-list">
          <!-- an individual todo item -->
          <div class="todo-item">
            <label>
              <input type="checkbox" />
              <span class="bubble business"> </span>
            </label>
          </div>

          <!-- the content for the individual todo -->
          <div class="todo-content">
            <input type="text" value="Todo Item 2" readonly />
          </div>

          <!-- the actions buttons that are going to be associated with each TODO -->
          <div class="todo-action">
            <button class="todo-edit-button"> Edit</button>
            <button class="todo-delete-button"> Delete</button>
          </div>
        </div>
      </section>
```

## The Actual TODO Display Section

This is how the actual 'TODO' display section is going to look like, in terms of code **after** we have written the `displayTodos` function inn our `main.js` file.

```html
      <!-- section of the form that is going to be displaying our TODOs -->
      <section class="todo-form-section">
        <h3> TODO List</h3>

        <!-- container for the list of todos -->
        <div id="todo-list"> </div>
      </section>
```

> [!NOTE]
> <p align="center"> Why is that like this?</p>
>
> You are going to see that in our `main.js` file when we go to explain it later on... You will see a function like `document.createElement`... What this will actually is create an "*HTML tag*" that we need / want to into our 'HTML' page!
>
> > I did **not** know that we could do something like that!
>

# Styling

Given that you know from [[Javascript - Document Object Model ( DOM )#Example Code - Dark / Light Mode Button With Local Storage | Javascript - Document Object Model]] code example, that to be able to actually switch the colours; you have to have *two* separate colourschemes.

> Makes sense, one for 'Dark' mode and one for 'Light' mode!

In the above example code, we were doing it like so:

```css
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
```

As you can see, we have a styling for when the user is in 'Light' mode and another one for when the user is in 'Dark' mode.

But given that in our case, we have something more "*complex*" here.

> There are more elements and tags on the page!

Therefore, doing using the above way is going to be a *pain in the ass*. This is where the `:root` comes into play!

```css
/* colours for the light theme */
:root {
  --background: #f8f9fa;
  --foreground: #212529;
  --cursor: #0d6efd;
  --cursor-text-color: #ffffff;
  --selection-background: #e9ecef;
  --selection-foreground: #495057;
  --black: #000000;
  --dark-grey: #6c757d;
  --red: #dc3545;
  --dark-red: #a71e2a;
  --green: #28a745;
  --dark-green: #1e7e34;
  --yellow: #ffc107;
  --dark-yellow: #d39e00;
  --blue: #0d6efd;
  --dark-blue: #0056b3;
  --magenta: #6f42c1;
  --dark-magenta: #5a32a3;
  --cyan: #17a2b8;
  --dark-cyan: #117a8b;
  --white: #e9ecef;
  --dark-white: #dee2e6;
}

/* colours for the dark theme */
:root.dark-mode {
  --background: #121212;
  --foreground: #e9ecef;
  --selection-background: #495057;
  --selection-foreground: #f8f9fa;
  --cursor: #0d6efd;
  --cursor-text-color: #000000;
  --black: #212529;
  --dark-grey: #495057;
  --red: #ea4343;
  --dark-red: #c82333;
  --green: #28a745;
  --dark-green: #1e7e34;
  --yellow: #ffc107;
  --dark-yellow: #d39e00;
  --blue: #6ea8fe;
  --dark-blue: #3d73c5;
  --magenta: #b19cd9;
  --dark-magenta: #9e7fcc;
  --cyan: #6edff6;
  --dark-cyan: #4bb5d7;
  --white: #ced4da;
  --dark-white: #adb5bd;
}
```

In this way, we only need to have something like this:

```css
/* style the `body` tag / element for the 'light' and 'dark' mode */
body {
  /* set the background color */
  background-color: var(--background);
  /* set the text colour when in light mode */
  color: var(--foreground);
}
```

Due to the way that I implemented the 'Toggle Theme' function; The above CSS, is going to use the colours of the '*Light*' mode and when / if the user decides to switch to the '*Dark*' mode. Then the colours from the `:root.dark-mode {}` are going to be **automatically** sourced.

> [!INFO]
> Given that we are already taking about the 'Toggle Theme' button; I am going to show you, how I implemented the it, right here, right now!

> [!TIP]
> Additionally, if you want to still style something that is "*found*" inside the 'Dark' mode; then you could totally do something like this to be able to achieve the styling that you want to.
>
> - The code found below is *styling* the 'Toggle Theme' button when **dark mode** is applied:
>
> ```css
> /* style the toggle theme button when in dark mode specifically */
> :root.dark-mode .theme-toggle-button {
>  /* change the background colour */
>  background-color: var(--dark-grey);
>  /* change the text colour */
>  color: var(--foreground);
> }
> ```

## Implementation Of The Toggle Theme Button

> I am going to break down the code little by little instead of showing me, myself and I the full thing!

```js
// get the button that is going to change the theme
let themeToggleButtonElement = document.getElementById("theme-button");

// get the "material" icons that of the theme button
let themeToggleIconElement = document.querySelector(".material-symbols-outlined");

// get the `theme` key from the local storage
let systemTheme = localStorage.getItem("theme");
```

- Get the 'HTML' elements from the `index.html` page and make them a Javascript object
- Get the `theme` *key's* value from the `localStorage`

```js
// set the default key-value pair for `theme` key if not already set
if (systemTheme === null) {
  // INFO: meaning that the page is using the light theme by default
  systemTheme = "light";
  // thus, set the key-value pair for 'theme' to 'light'
  localStorage.setItem("theme", systemTheme);
}

// Apply the theme based on the systemTheme
if (systemTheme === "dark") {
  // change the whole page to the 'dark' mode
  document.documentElement.classList.add("dark-mode");
  // change the button theme to the 'dark' mode
  themeToggleButtonElement.classList.add("dark-mode");
  // change the icon of the button ( toggling the theme )
  themeToggleIconElement.textContent = "dark_mode";
} else {
  // meaning that the user is actually using the light theme

  // change the whole page to the 'light' mode
  document.documentElement.classList.remove("dark-mode");
  // change the button theme to the 'light' mode
  themeToggleButtonElement.classList.remove("dark-mode");
  // change the icon of the button ( toggling the theme )
  themeToggleIconElement.textContent = "light_mode";
}
```

- The above code checks if the `theme` key does exists or not inside the `localStorage`
	- If the `theme` key does not have a value ==> set it to `Light` theme by default
- If the `theme` key has a **value** of `"dark"`
	- Switch all the element to use the `dark-mode` *style* variant from our `style.css`
- If the `theme` key has a **value** of `"light"`
	- Simply remove the `dark-mode` colorscheme applied on the 'HTML' elements

```js
// add the "click" implementation for the button
themeToggleButtonElement.addEventListener("click", () => {
  // switch the whole page to the 'dark' mode
  document.documentElement.classList.toggle("dark-mode");
  // switch the button to the 'dark' mode
  themeToggleButtonElement.classList.toggle("dark-mode");

  // check if the current theme is the dark theme
  const isDarkMode = document.documentElement.classList.contains("dark-mode");

  // change the icon of the button depending on the theme
  themeToggleIconElement.textContent = isDarkMode ? "dark_mode" : "light_mode";

  // change the 'theme' key to `dark` in the local storage
  localStorage.setItem("theme", isDarkMode ? "dark" : "light");
});
```

- The actual implementation of the 'Toggle Theme' button
- When the user *toggles* the button
	- The whole page and the button is going to switch to `dark-mode`
	- Check if the current theme is set to the 'Dark' variant
		- Switch the icon to dark variant
		- Update the `theme` key to `dark`
	- Else if the current theme is set to 'Light' variant
		- Switch the icon to light variant
		- Update the `theme` key to `light`

## CSS Syntax

Following the tutorial I came across this bit of 'CSS' code:

```css
/* select the `input:checked` and `bubble-business` together */
input:checked ~ .bubble-business {
  /* change the background colour */
  background-color: var(--green);
  /* change the border colour */
  border-color: var(--green);
}
```

> [!INFO] What is that `~` syntax?
>
> > [!INFO] Resource(s)
> > - https://www.w3schools.com/Css/css_combinators.asp
>
> The `~` is part of the '**General Sibling Combinator**' and it defines a *relationship* between two or more "*selectors*".
>
> The actual `~` is called a '**Subsequent Sibling Combinator**'.
>
> The *syntax* is going to select all the *siblings* of a **single** *parent*!
>
> In our *development* code above; you are going to see something like this:
>
> ```html
>          <!-- an individual todo item -->
>          <div class="todo-item">
>            <label>
>              <input type="checkbox" />
>              <span class="bubble business"> </span>
>            </label>
>          </div>
> ```
>
> As you can clearly see, we have `<input> ` and also the `<span> ` tag under the same `<label> ` ( *and `<div> `* )
>
> Therefore, the above syntax is going to select both of them and apply the corresponding settings.

- In this case, when the `<input> ` is "*checked*"
	- Select the `<span> `'s *checkbox* ( *our custom checkbox* )
	- Therefore, simply apply the *styling* to **both** of them

## Colour Shifting Text Logo

> [!INFO] Resource(s)
> - https://www.joshwcomeau.com/animation/color-shifting/

I now want to implement some sort of 'RGB' colour "*rotate*" when I hover on the *text logo* found inside the `<navbar> `.

From the first link found in the '*Resource(s)*' callout above; I have managed to make this:

```css
/* create a custom 'hue' property */
@property --hue {
  /* user defined 'HSL' angle / degree */
  syntax: "<angle> ";
  /* each element needs to have the 'hue' property added to it */
  inherits: false;
  /* if user does not provide a angle ==> default to '0' */
  initial-value: 0deg;
}

/* styling for the main logo's heading */
.main-heading {
  /* set the custom 'hue' propery to desired angle */
  /* --hue: 229.47deg; */
  --hue: 237deg;
  /* define the intial colour of the text logo */
  color: hsl(var(--hue), 100%, 75%);
  /* add a little "linear" animation to the 'hue' property only */
  transition: --hue 1.5s linear;
}

/* when the cursor / pointer hovers above the text logo */
.main-heading:hover,
.main-heading:focus-visible {
  /* change the angle on the colour wheel to desired angle */
  --hue: 720deg;
}
```

This code will and is going to allow for **colour shifting** when the user hovers on the '*Text Logo*'.

> [!NOTE]
> This is okay, but **not** the thing that I really want. I want the colour to basically **cycle** and **keep** cycling until the user does not / stops the hover.

### RGB Cycle On Text Logo!

> Talking with [Claude](https://claude.ai), I now understand how we are able to do that!

The **updated** ( *because I did write most of the initial parts* ) `style.css`'s code generated by 'Qwen'... I saw something like this:

```css
/* custom animation called `fadeIn` */
@keyframes fadeIn {
  /* element starts out with '0' opacity */
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  /* then gradually shows itself */
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

This is basically a **custom** animation that you can define. In this case, this custom animation is basically changing the opacity and moving the element '10' pixels up.

> We are also going to use something like this!

Therefore, updating the above code, we are going to implement this custom 'RGB-Cycle' animation like so still using the `--hue` 'CSS' property:

```css
/* define a custom animation called `rgb-cycle` */
@keyframes rgb-cycle {
  /* initial state */
  from {
    --hue: 0deg;
  }
  /* final state */
  to {
    --hue: 360deg;
  }
}
```

If you don't understand 'HSL' colours at all, then I suggest that you take a look at this YouTube video:

> Link to YouTube Video: https://www.youtube.com/watch?v=EJLrssH1ip0

Basically, this *custom animation* is going to start from the **colour** *red* and **cycles** through the whole colours of the colour wheel and goes back to *red*.

- Therefore, applying the custom animation to the '*text logo*':

```css
/* styling for the main logo's heading */
.main-heading {
  /* define the intial colour of the text logo */
  color: var(--foreground);
  /* add a little "linear" animation to the 'color' property only */
  transition: color 1.5s ease-out;
}

/* when the cursor / pointer hovers above the text logo */
.main-heading:hover,
.main-heading:focus-visible {
  /* define the intial colour of the text logo */
  color: hsl(var(--hue), 100%, 75%);
  /* the actual animation that will cycle infinitely */
  animation: rgb-cycle 2s linear infinite;
  /* remove all the transition animation to smoothly display cycling */
  transition: none;
}

/* when the cursor is not hovering on the text logo */
.main-heading:hover:not(:active) {
  /* stop the animation even when not hovering */
  animation-play-state: running;
}
```

Here are basically the **last** part of the 'CSS' code is basically saying that; to **stop** the animation from continuing.

> [!SUCCESS]
> We are able to implement the 'RGB-Cycle' effect / animation when we hover of the *text logo*!

### RGB Cycle On Username!

Now, what about keeping the 'RGB' cycle on while on the **username**. I have a section / `<input> ` whereby the user can input his / her username.

Therefore, let's implement this same, little "*subtle*" animation on username!

```css
/* add an infinite, always on RGB cycle to the user's name */
#username {
  /* define the intial colour of the text logo */
  color: hsl(var(--hue), 100%, 75%);
  /* the actual animation that will cycle infinitely */
  animation: rgb-cycle 2s linear infinite;
  /* change the font weight to be a little more bold */
  font-weight: 700;
}
```

> [!SUCCESS]
> Therefore, we should see that we have an *always-on* 'RGB' cycle on our page... Making it more *hip*?!?

---

# The Actual Main Javascript

I am now going to talk about the `main.js` file and how we are actually able to:

1. Write our 'TODO' item and display it
2. Add a category to it and store it in `localStorage`
3. Display the actual 'TODO' list and individual 'TODO' items
4. Allow the user to able to delete and edit each of the 'TODO' item

## Display, Username And TODO Item Code

> [!NOTE]
> I am going to look at this very code **before** I show me, myself and I look at the `displayTodos` function!

The code that we are going to look at is going to do three main things:

1. Initialises the whole page and also *calls* the `displayTodos` function to **show** the 'TODO' items
2. Allow the user enter a 'TODO' item and *connect* a category to it
3. Store the 'TODO' item added to the `localStorage`

```js
// when the whole thing ( HTML pages and objects ) is loaded
window.addEventListener("load", () => {
  // variable for the user's name for the "welcome" heading ( as a JS object )
  const nameInput = document.getElementById("username");

  // variable for whole TODO "creation" form itself ( as a JS object )
  const newTodoForm = document.getElementsByClassName("new-todo-form")[0];

  // variable to store the user's name from the local storage
  // if there are no 'username' key ==> default to a 'string'
  const username = localStorage.getItem("username") || "";

  // after the user enters the username ==> get that username "values"
  nameInput.value = username;

  // check for changes made at the input for username
  nameInput.addEventListener("change", (e) => {
    // if there is a name entered there or username has changed ==> save to local storage
    localStorage.setItem("username", e.target.value);
  });

  // check for any submission of TODOs
  newTodoForm.addEventListener("submit", (e) => {
    // stop the browser from executing its default action
    e.preventDefault();

    // get the content from the input field
    const content = e.target.elements.content.value;

    // if the content is empty or just whitespace, prevent adding the todo
    if (!content.trim()) {
      return;
    }

    // create a `todo` object
    const todo = {
      // use the variable `content` from above to save the actual content user entered
      content,
      // use the variable name `category` to save the category selected for each TODO item
      category: e.target.elements.category.value,
      // new TODO item created ==> not done yet
      done: false,
      // specify the current time at which the TODO item was created
      createdAt: new Date().getTime(),
    };

    // add new todo to the global array `todos`
    todos.push(todo);

    // save the new TODO item created to the local storage
    // use `JSON.stringify()` to convert the JS object to "JSON" string
    localStorage.setItem("todos", JSON.stringify(todos));

    // reset the TODO input and categories
    e.target.reset();

    // call the display function after creation of TODO item
    displayTodos();
  });

  // call the function ( "all the time" ) to display the TODO items
  displayTodos();
});
```

- The `load` event is... As the *word* suggests, its going to be *sourced* / "*activated*" when the page is **loaded**
- Check if there is a change on the page; Then use the *event system* to:
	- Store the changed **username** into the `localStorage`

```js
  // check for any submission of TODOs
  newTodoForm.addEventListener("submit", (e) => {
    // stop the browser from executing its default action
    e.preventDefault();

    // get the content from the input field
    const content = e.target.elements.content.value;

    // if the content is empty or just whitespace, prevent adding the todo
    if (!content.trim()) {
      return;
    }

    // create a `todo` object
    const todo = {
      // use the variable `content` from above to save the actual content user entered
      content,
      // use the variable name `category` to save the category selected for each TODO item
      category: e.target.elements.category.value,
      // new TODO item created ==> not done yet
      done: false,
      // specify the current time at which the TODO item was created
      createdAt: new Date().getTime(),
    };

    // add new todo to the global array `todos`
    todos.push(todo);

    // save the new TODO item created to the local storage
    // use `JSON.stringify()` to convert the JS object to "JSON" string
    localStorage.setItem("todos", JSON.stringify(todos));

    // reset the TODO input and categories
    e.target.reset();

    // call the display function after creation of TODO item
    displayTodos();
  });
```

The **part** of the code is responsible to allow us to enter the 'TODO' item and submit it to the `localStorage`.

- The `e.preventDefault()` is a function that will allow the browser to **stop** executing its normal behaviour
- If the `content` / 'TODO' item **cannot** be *trimmed*
	- This means that we **don't** have anything written in the 'TODO' `<input> `
	- This allows for the *category* to **not** be sent alone
- When we have *content* inside the `<input> ` for the 'TODO' item
	- Then we add that to the `todos` *global* array
	- Convert that *array* / *object* into its 'JSON' format
	- So that it can be saved to the `localStorage`
- Reset the `<input> ` and `<select> ` elements with `e.target.reset()`

## The Display Function

Below you are going to find the full code for the `displayTodos` function.

```js
// function that is going to be responsible for displaying our TODO items
function displayTodos() {
  // variable to get our using the query selector
  const todoList = document.querySelector("#todo-list");

  // "reset" all the HTML page for the display part
  todoList.innerHTML = "";

  todos.forEach((todo) => {
    // create a new `div` HTML tag on the page to show TODO item
    const todoItem = document.createElement("div");

    // add the styling of the todo item using the class 'todo-form-section'
    todoItem.classList.add("list");

    // create a new `label` HTML tag on the page to show TODO description
    const label = document.createElement("label");
    // create a new `input` HTML tag on the page to show TODO checkbox "clickable" area
    const input = document.createElement("input");
    // create a new `span` HTML tag on the page to show TODO customised checkbox
    const span = document.createElement("span");

    // create `div` tags for 'content', 'actions', 'edit', 'delete'
    const content = document.createElement("div");
    const actions = document.createElement("div");
    const editButton = document.createElement("button");
    const deleteButton = document.createElement("button");

    // change the type of the `input` tag
    input.type = "checkbox";
    // check if the TODO item has been completed / done
    input.checked = todo.done;

    input.addEventListener("change", (e) => {
      todo.done = e.target.checked;
      localStorage.setItem("todos", JSON.stringify(todos));
      displayTodos();
    });

    // add the styling of the todo item using the class 'bubble-business'
    span.classList.add("bubble-business");
    // add the styling of the todo item using the class 'bubble-business'
    content.classList.add("todo-content");
    // add the styling of the todo item using the class 'todo-action'
    actions.classList.add("todo-action");
    // add the styling of the todo item using the class 'todo-edit-button'
    editButton.classList.add("todo-edit-button");
    // add the styling of the todo item using the class 'todo-delete-button'
    deleteButton.classList.add("todo-delete-button");

    // change the content to show the actual content for the TODO item
    content.innerHTML = `<input type="text" value="${todo.content}" readonly> `;

    // display the 'edit' and 'delete' texts button according on the page
    editButton.innerHTML = "Edit";
    deleteButton.innerHTML = "Delete";

    // actually add all the elements to be shown on the HTML page
    // this is for the checkbox and text of todo item
    label.appendChild(input);
    label.appendChild(span);

    // this is for the buttons
    actions.appendChild(editButton);
    actions.appendChild(deleteButton);

    // so that the whole thing is displayed on the page
    todoItem.appendChild(label);
    todoItem.appendChild(content);
    todoItem.appendChild(actions);

    // finally add everything to the list
    todoList.appendChild(todoItem);

    // check if the TODO item has been checked off
    if (todo.done) {
      // add the styling of the todo item using the class 'done'
      todoItem.classList.add("done");
    }

    // check if the TODO item has been checked or not
    input.addEventListener("click", (e) => {
      // checked if the TODO item has been checked off
      todo.done = e.target.checked;

      // update the JSON data found inside the local storage
      localStorage.setItem("todos", JSON.stringify(todos));

      // check if the condition is the TODO item has been checked
      if (todo.done) {
        // if TODO item has actually been checked ==> apply the styling
        todoItem.classList.add("done");

        // but if the TODO item has not been checked off
      } else {
        // if TODO item has NOT been checked ==> remove the styling
        todoItem.classList.remove("done");
      }
    });

    // implement the 'Edit' button
    editButton.addEventListener("click", (e) => {
      // get the content of the TODO item
      const input = content.querySelector("input");

      // remove the `readonly` attribute from the `<input> ` taga completely
      input.removeAttribute("readonly");

      // WARNING: what does this actually means?
      input.focus();

      // check if the user clicks somewhere else when editing TODO item
      input.addEventListener("blur", (e) => {
        // re-apply the `readonly` attribute to the `<input> ` tag
        input.setAttribute("readonly", true);

        // update the todo item's content
        todo.content = input.value;

        // if change did occur ==> update the local storage
        localStorage.setItem("todos", JSON.stringify(todos));

        // refresh - display the update on the page
        displayTodos();
      });
    });

    // implement the 'Delete' button
    deleteButton.addEventListener("click", (e) => {
      // the actual code that is going to allow us to remove the TODO item
      todos = todos.filter((t) => t != todo);

      // update the local storage
      localStorage.setItem("todos", JSON.stringify(todos));

      // refresh - display the update on the page
      displayTodos();
    });
  });
}
```

### Displaying Each TODO Item

```js
  // iterate through each of the TODO objects found in the global array
  todos.forEach((todo) => {
    // create a new `div` HTML tag on the page to show TODO item
    const todoItem = document.createElement("div");

    // add the styling of the todo item using the class 'todo-form-section'
    todoItem.classList.add("list");

    // create a new `label` HTML tag on the page to show TODO description
    const label = document.createElement("label");
    // create a new `input` HTML tag on the page to show TODO checkbox "clickable" area
    const input = document.createElement("input");
    // create a new `span` HTML tag on the page to show TODO customised checkbox
    const span = document.createElement("span");

    // create `div` tags for 'content', 'actions', 'edit', 'delete'
    const content = document.createElement("div");
    const actions = document.createElement("div");
    const editButton = document.createElement("button");
    const deleteButton = document.createElement("button");

    // change the type of the `input` tag
    input.type = "checkbox";
    // check if the TODO item has been completed / done
    input.checked = todo.done;

    // check for changes made at the input for checkboxes
    input.addEventListener("change", (e) => {
      // checked if the todo item is done
      todo.done = e.target.checked;

      // update the local storage to modify the global array
      localStorage.setItem("todos", JSON.stringify(todos));

      // call the function "resursively" to show the change
      displayTodos();
    });

    // add the styling of the todo item using the class 'bubble-business'
    span.classList.add("bubble-business");
    // add the styling of the todo item using the class 'bubble-business'
    content.classList.add("todo-content");
    // add the styling of the todo item using the class 'todo-action'
    actions.classList.add("todo-action");
    // add the styling of the todo item using the class 'todo-edit-button'
    editButton.classList.add("todo-edit-button");
    // add the styling of the todo item using the class 'todo-delete-button'
    deleteButton.classList.add("todo-delete-button");

    // change the content to show the actual content for the TODO item
    content.innerHTML = `<input type="text" value="${todo.content}" readonly> `;

    // display the 'edit' and 'delete' texts button according on the page
    editButton.innerHTML = "Edit";
    deleteButton.innerHTML = "Delete";

    // actually add all the elements to be shown on the HTML page
    // this is for the checkbox and text of todo item
    label.appendChild(input);
    label.appendChild(span);

    // this is for the buttons
    actions.appendChild(editButton);
    actions.appendChild(deleteButton);

    // so that the whole thing is displayed on the page
    todoItem.appendChild(label);
    todoItem.appendChild(content);
    todoItem.appendChild(actions);

    // finally add everything to the list
    todoList.appendChild(todoItem);
```

The code above is going to iterate through the *global* `todos` variable and get each 'TODO' item so that it can be displayed inside the `<div> ` element with and `id` of `todo-list`.

The code is going to create each to the 'HTML' elements like `<input> `, `<span> `, `<button> ` and more!

### Checking For Completed TODO Item

```js
    // check if the TODO item has been checked off
    if (todo.done) {
      // add the styling of the todo item using the class 'done'
      todoItem.classList.add("done");
    }

    // check if the TODO item has been checked or not
    input.addEventListener("click", (e) => {
      // checked if the TODO item has been checked off
      todo.done = e.target.checked;

      // update the JSON data found inside the local storage
      localStorage.setItem("todos", JSON.stringify(todos));

      // check if the condition is the TODO item has been checked
      if (todo.done) {
        // if TODO item has actually been checked ==> apply the styling
        todoItem.classList.add("done");

        // but if the TODO item has not been checked off
      } else {
        // if TODO item has NOT been checked ==> remove the styling
        todoItem.classList.remove("done");
      }
    });
```

The above code is going to add the correct styling options from the `style.css` file for when the `<input> ` has been checked-off!

If there has been a `'click'` event on the checkbox associated with the `<input> ` tag. Hence, updated the `localStorage`.

> [!NOTE]
> Given that this is a *toggleable* thing, we have to have conditions for when it checked-off and **not** checked-off.
>
> That is the reason as to why we have that `if` statement.

### Implementation Of The Edit Button

```js
    // implement the 'Edit' button
    editButton.addEventListener("click", (e) => {
      // get the content of the TODO item
      const input = content.querySelector("input");

      // remove the `readonly` attribute from the `<input> ` taga completely
      input.removeAttribute("readonly");

      // set the input element to be active to be able to receive changes
      input.focus();

      // check if the user clicks somewhere else when editing TODO item
      input.addEventListener("blur", (e) => {
        // re-apply the `readonly` attribute to the `<input> ` tag
        input.setAttribute("readonly", true);

        // update the todo item's content
        todo.content = input.value;

        // if change did occur ==> update the local storage
        localStorage.setItem("todos", JSON.stringify(todos));

        // refresh - display the update on the page
        displayTodos();
      });
    });
```

- Check if the 'Edit' button has been clicked
	- Remove the `readonly` attribute applied to the `<input> ` tag *normally*
	- Use the `input.focus()` to set the *focus* to the `<input> ` on the 'TODO' item
- When the use has finished editing the 'TODO' item
	- He just need to click somewhere else and the `'blur'` event listener is going to take into action
		- Its going to re-add the `readonly` property to the the `<input> ` tag so it **cannot** be changed
		- Update the *value* changed to the `localStorage`'s `todos` array
- Finally call the `displayTodos` function to *refresh* the page

### Implementation Of The Delete Button

```js
    // implement the 'Delete' button
    deleteButton.addEventListener("click", (e) => {
      // the actual code that is going to allow us to remove the TODO item
      todos = todos.filter((t) => t != todo);

      // update the local storage
      localStorage.setItem("todos", JSON.stringify(todos));

      // refresh - display the update on the page
      displayTodos();
    });
```

The above code is pretty simple as it going to:

- Listen when the 'Delete' button has been clicked
- The line of code `todos = todos.filter((t) => t != todo);` is going to:
	- Find the specific 'TODO' item that the 'Delete' button has just been pressed
	- Create a new `todos` list whereby the 'TODO' item to be *removed* is **not** present
	- Return the new, updated `todos` global array
- Save that new `todos` array to the `localStorage`
- Finally refresh the page to show the changes made

## Displaying Categories

I now want to display the `category` in **between** the *checkbox* and the 'TODO' *content*.

Therefore, I first tried doing this in my `main.js` file to see if I am able to display a single `category`.

- Update the `index.html`; add the following code just after `</main> `:

```html
    <!-- WARNING: test the category display -->
    <p> Content <span class="todo-category-view"> </span> </p>
```

- Update the `main.js` file so that it can display the `category`:

```js
// WARNING: testing
// get the `<span> ` tag as a JS object
const category = document.querySelector(".todo-category-view");

// get the first object found inside the `todos` array
const firstObj = todos[0];

// display the category of that first TODO item
category.innerHTML = firstObj.category;
```

> [!SUCCESS]
> I can see that the *category* has been displayed!

### Updating The `displayTodos` Function To Display Category

I am now going to show bits of code in the `main.js` file and specifically inside the `displayTodos` function.

- Actually create the `div` element on the page to display category:

```js
    // create `div` tags for 'category', 'content', 'actions', 'edit', 'delete' const category = document.createElement("div");
	const category = document.createElement("div");
    const content = document.createElement("div");
    const actions = document.createElement("div");
    const editButton = document.createElement("button");
    const deleteButton = document.createElement("button");
```

- Create the styling inside our `style.css` file:

```css
/* style each category found in between the checkbox and TODO content */
.todo-category {
  /* change the padding */
  padding: 0.5rem;
  /* change the margin */
  margin: 0.2rem;
  /* change the border radius */
  border-radius: 0.5rem;
  /* change the background colour */
  background-color: var(--foreground);
  /* change the text colour */
  color: var(--background);
}
```

- Associate the styling `.todo-category` to the `category` element / `<div> `:

```js
    // add the styling of the todo item using the class 'bubble-business'
    span.classList.add("bubble-business");
    // add the styling of the category using the class 'todo-category'
    category.classList.add("todo-category");
    // add the styling of the todo item using the class 'bubble-business'
    content.classList.add("todo-content");
    // add the styling of the todo item using the class 'todo-action'
    actions.classList.add("todo-action");
    // add the styling of the todo item using the class 'todo-edit-button'
    editButton.classList.add("todo-edit-button");
    // add the styling of the todo item using the class 'todo-delete-button'
    deleteButton.classList.add("todo-delete-button");
```

- Actually display the `category` for each 'TODO' item:

```js
    // display the `category` for each TODO item
    category.innerHTML = "#" + todo.category;
    // display the actual content for the TODO item
    content.innerHTML = `<input type="text" value="${todo.content}" readonly> `;

    // display the 'edit' and 'delete' texts button according on the page
    editButton.innerHTML = "Edit";
    deleteButton.innerHTML = "Delete";
```

- Add the *whole* TODO *list* item:

```js
    // actually add all the elements to be shown on the HTML page
    // this is for the checkbox and text of todo item
    label.appendChild(input);
    label.appendChild(span);

    // this is for the buttons
    actions.appendChild(editButton);
    actions.appendChild(deleteButton);

    // so that the whole thing is displayed on the page
    todoItem.appendChild(label);
    todoItem.appendChild(category);
    todoItem.appendChild(content);
    todoItem.appendChild(actions);

    // finally add everything to the list
    todoList.appendChild(todoItem);
```

> [!SUCCESS]
> Therefore, you should be able to see that we have the `category` displayed in *between* the checkbox and the 'TODO' content!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!