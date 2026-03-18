---
id: React - Getting Started
aliases: Getting Started With React Library
tags:
  - HTML
  - CSS
  - JS
  - basics
  - react
author: S.Sunhaloo
date: 2025-11-05
status: Completed
---

## List of Contents

- [[#The React Library]]
	- [[#Create A React Project With Vite]]
	- [[#The Project Structure]]
- [[#Components]]
- [[#Getting Our Hands Dirty]]
- [[#Styling The Page and Components]]
	- [[#Style The Whole Page]]
- [[#Don't Style The Way That I Did!!!]]

---

> [!INFO] Resource(s):
> - Websites:
> 	- https://react.dev
> 		- https://react.dev/learn
> 		- https://react.dev/references
> - Videos:
> 	- https://www.youtube.com/watch?v=E8lXC2mR6-k

# The React Library

> [!INFO] Requirements
> - Terminal Emulator:
> 	- [Kitty](https://sw.kovidgoyal.net/kitty/)
> 	- [Ghostty](https://ghostty.org/)
> 	- [Windows Terminal](https://github.com/microsoft/terminal)
> - Text Editor:
> 	- [Neovim](https://github.com/neovim/neovim)
> 	- [Emacs](https://www.gnu.org/software/emacs/)
> 	- [VS C\*de](https://code.visualstudio.com/)
> - [Node](https://nodejs.org/en)
> - `git` ( *Please refer to: '[[Git - Introduction]]'* )

As the heading says, React is **not** a framework; its a **library** that is designed to make us developers *faster* at our works using *reuseable* **components**.

> [!INFO] What is a 'Component'?
> - React Documentation: https://react.dev/reference/react/Component
>
> In short, anything can be a component in React. A *component* is a **reusable**, piece of code and can be basically anything.

## Create A React Project With Vite

> [!INFO] Resource(s)
> - https://vite.dev/
> - https://react.dev/learn/build-a-react-app-from-scratch#vite
> - Deprecation Of 'Create My React App': https://react.dev/blog/2025/02/14/sunsetting-create-react-app#limitations-of-build-tools

> [!WARNING] Do **NOT** Use Create My React App
> If you follow the official React documentation, you are going to see that they have **deprecated** the following command:
>
> ```bash
> # this has been deprecated
> npx create-react-app my-app
> ```
>
> The reason is simple! There are **far** better ways and tools to do that and one of them is using 'Vite'

> "*Its a French word*!"

- Use the following command below to create a React project ( *with 'Vite'* ):

```bash
# create a 'my-app' React + Vite project using JSX
npm create vite@latest my-app -- --template react
```

> [!NOTE]
> The actual command that React is telling you to run is this:
>
> ```bash
> # create a 'my-app' React + Vite project using TSX
> npm create vite@latest my-app -- --template react-ts
> ```
>
> But this is going to make use 'Typescript XML' instead of the **default** 'Javascript XML'!

- Running the above command; I get the following:

```console
> npx
> "create-vite" my-app --template react

│
◇  Use rolldown-vite (Experimental)?:
│  No
│
◇  Install with npm and start now?
│  Yes
│
◇  Scaffolding project in /home/username/GitHub/University/Current-Learning/Web/my-app...
│
◇  Installing dependencies with npm...

added 152 packages, and audited 153 packages in 40s

32 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
│
◇  Starting dev server...

> my-app@0.0.0 dev
> vite


  VITE v7.2.1  ready in 314 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
  ➜  press h + enter to show help
```

> I basically went with the *recommended* options...

Hence, if you go the following URL in your browser, you are going to see the "*Welcome*" page for React + Vite!

## The Project Structure

Now, close the development server and heading into `my-app`! You should see that you have this project structure:

```console
 .
├──  eslint.config.js
├──  index.html
├──  node_modules
├──  package-lock.json
├──  package.json
├──  public
├── 󰂺 README.md
├── 󰣞 src
└──  vite.config.js
```

> [!TIP] What Does Each Means?
> - The Dependencies: `node_modules` folder
> - Static Assets: `public` folder
> 	- You can create other folders like `public/images` or `public/videos` inside!
> - Entry Point: `index.html` file
> - Source Folder: `src` folder ( *duh* )
> 	- Main "*coding*" file: `App.jsx` ( *initially renders the 'Welcome' page* )
> 	- React 'DOM': `main.jsx` --> `my-app/index.html`
> - [[Javascript - Node Version#The Package JSON File | Package JSON File]]: `package.json` ( *of-course* )
> - And many more!
>
> > These are the things that we need to know for now!
>
> The main this its that we are going to be working inside the `src` folder inside the `App.jsx` folder.

# Components

> [!INFO] Resource(s)
> - https://react.dev/reference/react-dom

## The Main Component

Again, as we know everything can become a "*component*" in React. Heck, even a **whole page** in React can become a component.

You are going to see the following code in our `src/App.jsx` *main* file:

```jsx
function App() {
  const [count, setCount] = useState(0)

  return (
    <>
      <div>
        <a href="https://vite.dev" target="_blank">
          <img src={viteLogo} className="logo" alt="Vite logo" />
        </a>
        <a href="https://react.dev" target="_blank">
          <img src={reactLogo} className="logo react" alt="React logo" />
        </a>
      </div>
      <h1> Vite + React</h1>
      <div className="card">
        <button onClick={() => setCount((count) => count + 1)}>
          count is {count}
        </button>
        <p>
          Edit <code> src/App.jsx</code> and save to test HMR
        </p>
      </div>
      <p className="read-the-docs">
        Click on the Vite and React logos to learn more
      </p>
    </>
  )
}
```

The `App` function ( *main component* ) is basically the "*entry point*" of our code. Then the `main.jsx` file is going to use something called the 'React DOM'.

- This is how the `main.jsx` file looks like:

```jsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import "./index.css";
import App from "./App.jsx";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <App />
  </StrictMode> ,
);
```

As you know, the "*browser*" only understands 'HTML', 'CSS' and 'JS' code! Therefore, React has to find a way to convert all of the 'JSX' code so the browser understand what we wrote!

- Therefore, this ( *the `my-app/index.html`* ) is what is actually being rendered out by our browser:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title> my-app</title>
  </head>
  <body>
    <div id="root"> </div>
    <script type="module" src="/src/main.jsx"> </script>
  </body>
</html>
```

> As you can see, `src="/src/main.jsx"` inside the `script` element!

# Getting Our Hands Dirty

> [!TIP] What To Code?
> As a first learning experience... I am going convert the 'Counter' *app* that I made in *pure* 'HTML', 'CSS' and 'JS'.
>
> Refer to the file / note: '[[Javascript - Document Object Model ( DOM )#Example Code - Counter Button | Javascript - Document Object Model ( DOM )]]'

- Remove the code found inside `App` function inside the `App.jsx` file:

```jsx
import "./App.css";

function App() {
  return <> </> ;
}

export default App;
```

> Also do remove every line of "*code*" from the `App.css` and `index.css` file!

- Head into the `src` folder and make a new folder with the name `components`
- Create two files:
	- `Button.jsx`
	- `Counter.jsx`

> [!INFO] First Letter Capitalised!
> When you create a component, what if it be a `.jsx` file or the actual component *function* that is **in** that file!
>
> We need to write the **first** *letter* of the *word* in 'CAPS'!

> BTW the `<> </> ` is called '*JSX Fragment*' tag!

## Create A Button Component

Let's go ahead and create a simple `button` *component*.

- Add the following code to the `components/Button.jsx` file:

```jsx
function Button() {
  return <button> A Button</button> ;
}

export default Button;
```

- Hence, to use the `Button` component, we need to update our `App.jsx` file to this:

```jsx
import Button from "./components/Button.jsx";
import "./App.css";

function App() {
  return (
    <>
      <Button />
    </>
  );
}

export default App;
```

## Update Button Component For Different Functionalities

> [!INFO] Resource(s)
> - https://react.dev/reference/react/useState

- This is our button component updated:

```jsx
function Button({ btnText, clickFunc }) {
  return <button onClick={clickFunc}> {btnText}</button> ;
}

export default Button;
```

- Create the required buttons inside the `App.jsx` file:

```jsx
import Button from "./components/Button.jsx";
import "./App.css";

function App() {
  return (
    <>
      <Button btnText={"Decrement Counter"} />
      <Button btnText={"Alert / Display Count"} />
      <Button btnText={"Increment Counter"} />
      <Button btnText={"Randomise Counter"} />
    </>
  );
}

export default App;
```

### Parent and Child Analogy

In our case, the `App` function ( *component* ) is called the '**Parent**' component. And the `Button` component that we created is called the '**Child**' component!

This is because the `App.jsx` / `App` component knows in what *state* the **data** is currently! Compared out our *child* components... They are just performing an **action** based on the data provided!

> [!TIP] What I Am Trying To Say?
> You need to:
>
> - Write the *wire-frame* in the **child** components ( *like `Button` in this case* )
> - Write the *functionalities* associated with **child** components inside the `App.jsx` file

## Implement The Button Functionalities

Therefore, update our `App.jsx` file and inside the main **parent** function we have the *implementation* of the button.

```jsx
import { useState } from "react";
import Button from "./components/Button.jsx";
import "./App.css";

function App() {
  // define the state for the count
  const [count, setCount] = useState(0);

  // function that is going to decrement the counter
  function handleDecrement() {
    setCount(count - 1);
  }

  // function that is going to diplay the counter using `alert` and `console`
  function handleDisplay() {
    // display a pop-up on the screen
    alert(`Current Count: ${count}`);

    // log the value of `count` to the console
    console.log(`Counter Value: ${count}`);
  }

  // function that is going to increment the counter
  function handleIncrement() {
    setCount(count + 1);
  }

  // function that is going to randomise the counter
  function handleRandomise() {
    setCount(Math.floor(Math.random() * 100));
  }

  return (
    <>
      <Button btnText={"Decrement Counter"} clickFunc={handleDecrement} />
      <Button btnText={"Alert / Display Count"} clickFunc={handleDisplay} />
      <Button btnText={"Increment Counter"} clickFunc={handleIncrement} h />
      <Button btnText={"Randomise Counter"} clickFunc={handleRandomise} />
    </>
  );
}

export default App;
```

## Create Counter Component

- Add this code inside our `src/components/Counter.jsx` file:

```jsx
function Counter({ countVal }) {
  return (
    <>
      <h4 className="counter-heading"> {countVal}</h4>
    </>
  );
}

export default Counter;
```

- Update our `count` function in our `App.jsx` file:

```jsx
  // define the state for the count
  const [count, setCount] = useState(Math.floor(Math.random() * 100));
```

> Now its also randomise at the start!

- Import and use the `Counter` component; therefore the full code is going to look like this:

```jsx
import { useState } from "react";
import Button from "./components/Button.jsx";
import Counter from "./components/Counter.jsx";
import "./App.css";

function App() {
  // define the state for the count
  const [count, setCount] = useState(Math.floor(Math.random() * 100));

  // function that is going to decrement the counter
  function handleDecrement() {
    setCount(count - 1);
  }

  // function that is going to diplay the counter using `alert` and `console`
  function handleDisplay() {
    // display a pop-up on the screen
    alert(`Current Count: ${count}`);

    // log the value of `count` to the console
    console.log(`Counter Value: ${count}`);
  }

  // function that is going to increment the counter
  function handleIncrement() {
    setCount(count + 1);
  }

  // function that is going to randomise the counter
  function handleRandomise() {
    setCount(Math.floor(Math.random() * 100));
  }

  return (
    <>
      <Counter countVal={count} />
      <Button btnText={"Decrement Counter"} clickFunc={handleDecrement} />
      <Button btnText={"Alert / Display Count"} clickFunc={handleDisplay} />
      <Button btnText={"Increment Counter"} clickFunc={handleIncrement} h />
      <Button btnText={"Randomise Counter"} clickFunc={handleRandomise} />
    </>
  );
}

export default App;
```

# Styling The Page and Components

As you know in *[[Javascript - Document Object Model ( DOM ) | pure]]* 'HTML', we have the **attribute** of `class` and `id`.

But in the case of React and more specifically, `.jsx`... We have something called `className`. Whereby you can use `className` on an 'HTML' *element* / *tag* and its going to basically do the **same** thing as `class`.

Nevertheless, there is a little quirk whereby you <strong> <span style="color: orange;"> cannot</span> </strong> use the attribute `className` *directly* with a **custom** component.

> But there is a something that we can do about it!

<p align=center> Simply pass it as an <strong> argument</strong> </p>

- Therefore, update our `Counter` component to have the `className` attribute:

```jsx
function Counter({ customClassName, countVal }) {
  return (
    <>
      <h4 className={customClassName}> {countVal}</h4>
    </>
  );
}

export default Counter;
```

> [!NOTE]
> Given that I want all my buttons to be of the **same** design... I think I don't need to add / pass a *custom* `className` variable to pass to the *component* itself!

> Therefore, let's go do something completely different!

## Style The Whole Page

Let's style the whole page first and then we style the individual components later!

- Go ahead and add the following code to the `src/index.css` file:

> This styling is for defining the overall layout of the **whole** page!

```css
/* default / "dark mode" colourscheme */
:root {
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
  --white: #1e1e1e;
  --dark-white: #2d2d2d;
  --primary: #4895ef;
  --secondary: #4361ee;
  --accent: #4cc9f0;
  --light-bg: #1e1e1e;
  --card-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  --card-shadow-hover: 0 8px 30px rgba(0, 0, 0, 0.4);
}

/* styling for the all the properties */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family:
    "Inter",
    -apple-system,
    BlinkMacSystemFont,
    "Segoe UI",
    Roboto,
    Oxygen,
    Ubuntu,
    Cantarell,
    sans-serif;
}

/* style the whole HTML tag ==> make everything in the middle */
html {
  max-width: 100%;
  margin: auto;
  scroll-behavior: smooth;
}
```

> [!NOTE]
> There are **many** ways to *style* a tag, component and other items.
>
> But I am going to set some rules for me, myself and I.
>
> - Define the styling for each **component** inside its respective *file* in `componentStyles`
> - Define the styling 'HTML' ( _**with `className`**_ ) tags inside the `App.css` file
> - Define the overall **layout** of the whole page using the `index.css` file
> 	- But if there are any "*global*" 'HTML' like `button` or `a` or whatever

## Using Ant Design

> That's the main goal of a library like React!

> [!INFO] Resource(s)
> - https://ant.design/

The thing that we want to do when using a library like React is to basically use / `import` as much stuff that we need to in order to go *faster* in the development!

If and only if there is something that has not yet been created... Then you are going to **make** it and then **post** it so that the whole world can use it.

The company that I am currently doing my internship is using something called 'Ant Design'!

> But the are going to be moving to [ShadCN](https://www.shadcndesign.com/)!

Hence, as I am bad at designing and making UIs look good; I think I am going to help myself and use their **premade** designs.

> You can also customise them to your liking...

### Installing Ant Design

- Go ahead and run the following command at the root of our project:

```bash
# install UI design from Ant Design
npm install antd
```

- Add the following line at the *top* of our `src/main.jsx` file:

```jsx
import "antd/dist/reset.css";
```

### Update Button Component To Use Ant Design

- Go ahead and modify the `components/Button.jsx` file so that it looks like this:

```jsx
import { Button as AntButton } from "antd";
import "../componentStyle/Button.css";

function Button({ btnText, clickFunc }) {
  return (
    <AntButton
      className="ant-button"
      onClick={clickFunc}
      color="primary"
      variant="solid"
    >
      {btnText}
    </AntButton>
  );
}

export default Button;
```

## Style Button Components

- This is what is in my `componentStyle/Button.css` file:

```css
.ant-button {
  margin: 0.5rem;
  padding: 0.5rem;
  border: none;
  transition: all 0.2s ease;
  box-shadow: 0 4px 10px rgba(67, 97, 238, 0.3);
}

.ant-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 15px rgba(67, 97, 238, 0.4);
  font-weight: 600;
}

.ant-button:active {
  transform: translateY(0);
}
```

## Style Counter Component

- I made some changes to the `components/Counter.jsx` file:

```jsx
import "../componentStyle/Counter.css";

function Counter({ customClassName, countVal }) {
  return <h4 className="main-counter"> {countVal}</h4> ;
}

export default Counter;
```

- Therefore this is how my `componentStyle/Counter.css` file looks like:

```css
.main-counter {
  padding: 1rem 2rem 1rem 2rem;
  margin-bottom: 2rem;
}
```

## Style The Main Container

- Update the 'JSX' fragment tag to a `div` tag in our `src/App.jsx` file:

```jsx
  return (
    <div className="main-container">
      <Counter countVal={count} />
      <Button btnText={"Decrement Counter"} clickFunc={handleDecrement} />
      <Button btnText={"Alert / Display Count"} clickFunc={handleDisplay} />
      <Button btnText={"Increment Counter"} clickFunc={handleIncrement} h />
      <Button btnText={"Randomise Counter"} clickFunc={handleRandomise} />
    </div>
  );

```

- This is my `src/App.css` file looks like:

```css
.main-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  max-width: 300px;
  margin: 5rem auto;
}
```

## Update The Main Styling For Whole Page

- Finally update the `src/index.css` file with these lines of code:

```css
/* default / "dark mode" colourscheme */
:root {
	/* other codes are the same */
  --border-radius: 12px;
  --transition: all 0.3s ease;
}


/* style the whole HTML tag ==> make everything in the middle */
html {
  max-width: 100%;
  margin: auto;
  background-color: var(--background);
  scroll-behavior: smooth;
}

/* style `div` found in our `App.jsx` file */
.main-container {
  background-color: var(--white);
  box-shadow: var(--card-shadow);
  border-radius: var(--border-radius);
}

/* style custom `Counter` component found in our `components/Counter.jsx` file */
.main-counter {
  color: var(--foreground);
  background-color: var(--white);
  box-shadow: var(--card-shadow);
  border-radius: var(--border-radius);
}
```

> [!SUCCESS]
> I think we has done a simple job now onto making a *mega* 'TODO' list application with React!

---

# Don't Style The Way That I Did!!!

Given that each company has its own coding standard which we have to follow... At my internship, the developers talked to me and said that my way ( *see above* ) is "**redundant**".

> It works but **not** optimal!

Therefore, this is how we should be actually styling our components and page.

- Leave the `src/index.css` file for the *whole* page ( *treat it like the `style.css` file* )
- All components created inside the `components` folder needs to have a `className` that can be passed
	- Style each `components/{compoentName}.jsx` inside the `.jsx` file itself
- If there are further styling that needs to be done to **one** specific component
	- Pass the `className` and style it in the `App.css` file


---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!