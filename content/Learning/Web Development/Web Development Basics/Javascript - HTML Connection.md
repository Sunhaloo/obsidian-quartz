---
id: Javascript - HTML Connection
aliases: Web Side Of Javascript
tags:
  - HTML
  - CSS
  - JS
author: S.Sunhaloo
date: 2025-09-28
status: Completed
---

## List of Contents

- [[#Simple Alert and Hello World]]
- [[#Buttons With Functions]]

---

> [!WARNING]
> This file has no structure!
>
> As Javascript is a *web scripting language*... This dilemma of how to structure these notes are going to be difficult.
>
> Therefore, instead of structuring... **Let's Not Structure Anything At All**!
>
> Additionally, I am following this very tutorial:
>
> - https://www.youtube.com/watch?v=EerdGm-ehJQ
>
> But then again, if there is something specific to the Javascript language itself... I am going to add it to the [[Javascript Language Basics]] file / note and any other *language* related note.

# Simple Alert and Hello World

- This is my `index.html` file that I created:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title> Hello World</title>
    <link href="style.css" rel="stylesheet" />
  </head>
  <body>
    <h1> Nice</h1>
    
    <button class="main_button" onclick="alert('Button Pressed!!!');">
      Greetings
    </button>

    <p>
      There is a
      <button class="inner_button" onclick="console.log('Hello World');">
        button
      </button>
      inside this <em> very</em> <strong> paragraph</strong> tag!!!
    </p>

    <script>
      console.log(Math.floor(68.69696969) + 1);
    </script>
  </body>
</html>
```

> [!WARNING] Using `<script> ` tags!
> I am going to fully follow the tutorial as I don't know how a `script.js` file is going to be linked and what to write in there!

- This is the stylesheet / `style.css` file that I created for the `index.html` file:

```css
html {
  background-color: black;
  color: white;
}

h1 {
  text-align: center;
}

.main_button {
  background-color: white;
  color: green;
  border: solid 2px transparent;
  border-radius: 5px;
}

.inner_button {
  background-color: #ff000050;
  color: white;
  border: none;
}
```

> [!INFO]
> The following code above has 2 buttons, button `main_button` and `inner_button`.
>
> When the webpage will start... It is going to *display* '69' in the console.
>
> Now, if the user presses the `main_button`... It going to *run* the `alert` function and then then use will see a **pop-up** with 'Button Pressed!!!' displayed as *message*.
>
> If the user presses the `inner_button`... Then instead of displaying 'Hello World' in a pop-up. The 'Hello World' *message* is going to be displayed inside the **console**.

# Buttons With Functions

- This is the `index.html` file:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title> Variables and Button</title>
    <link href="style.css" rel="stylesheet" />
  </head>
  <body>
    <h1> Shopping Cart Details</h1>

    <button onclick="alert(cartItems);"> Show Cart Quantity</button>
    <button
      onclick="cartItems += 1;
      console.log(`Cart Was Incremented To ${cartItems}`);"
    >
      Add To Cart
    </button>
    <button
      onclick="cartItems -= 1;
      console.log(`Cart Was Decremented To ${cartItems}`);"
    >
      Decrement Cart
    </button>
    <button
      onclick="cartItems = 0;
      console.log('Cart Was Reseted!!!');"
    >
      Reset Cart
    </button>
    <button onclick="console.log(`There are ${cartItems} Items In Cart!!!`);">
      Total Items
    </button>

    <script>
      // declare variable to hold number of total items
      let cartItems = 0;
    </script>
  </body>
</html>
```

> I think that pasting the `style.css` stylesheet is unncessary!

## Updating The Above Code

After playing and watching the video for a bit and using my *existing* programming knowledge ( *if there was something already* ). I updated the code a bit so that when you press the **decrement** button and if the number of items in the cart is already '0'... It **stays** zero!

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title> Variables and Button</title>
    <link href="style.css" rel="stylesheet" />
  </head>
  <body>
    <h1> Shopping Cart Details</h1>

    <button id="showCartQuantityBtn"> Show Cart Quantity</button>
    <button
      onclick="cartItems += 1;
      console.log(`Cart Was Incremented To ${cartItems}`);"
    >
      Add To Cart
    </button>
    <button
      onclick="
      if (cartItems <= 0) {
        console.log(`Cart Cannot Be Decremented Futher!!!`);
        cartItems = 0;
      } else {
        cartItems -= 1;
        console.log(`Cart Was Decremented To ${cartItems}`);
      }"
    >
      Decrement Cart
    </button>
    <button
      onclick="cartItems = 0;
      console.log('Cart Was Reseted!!!');"
    >
      Reset Cart
    </button>
    <button onclick="console.log(`There are ${cartItems} Items In Cart!!!`);">
      Total Items
    </button>

    <script src="script.js"> </script>
  </body>
</html>
```

### Additionally, "Tasting" 'Document Object Model'

```js
// declare variable to hold number of total items
let cartItems = 0;

// document object manipulation on the 'Show Cart Quantity' button

// get the button element by its ID
const showCartBtn = document.getElementById("showCartQuantityBtn");

// check if that button ( ID ) has been found on the page
if (showCartBtn) {
  // meaning that the button has been found ==> implement the code for showing cart
  showCartBtn.addEventListener("click", function () {
    // use the `alert` function to display the `cartItems`
    alert(cartItems);
  });

  // if the button ( ID ) has not been found ==> display an error message
} else {
  // output an appropriate message
  console.error("\n\t<< Button ID 'showCartQuantityBtn' Was NOT Found!!! > > \n");
}
```

> [!NOTE]
> I **don't** understand anything about '*Document Object Models*' but the video is going to show us how to use it and how it works!
>
> > So right now, I just have this!
>

> [!INFO]
> For more information about Document Object Model, please refer to the note '[[Javascript - Document Object Model ( DOM )]]'.
>
> I am now going to stop writing in this very file and start "*fresh*" over the the above mentioned note!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!