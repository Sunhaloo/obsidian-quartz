---
id: Javascript - Local Storage
aliases: Using The Local Storage Provided By The Browser
tags:
  - CSS
  - HTML
  - JS
  - basics
  - objects
author: S.Sunhaloo
date: 2025-10-29
status: Completed
---

## List of Contents

- [[#What Is Local Storage?]]
	- [[#Using The Local Storage]]

---

> [!INFO] Resource(s)
> - https://thelinuxcode.com/the-complete-guide-to-storing-data-in-browser-local-storage/
> - https://medium.com/@premodsuraweera1/how-to-work-with-local-storage-in-your-browser-8aebfe92c16d
> - https://www.freecodecamp.org/news/use-local-storage-in-modern-applications/
> - https://www.youtube.com/watch?v=GihQAC1I39Q

# What Is Local Storage?

> [!INFO]
> There are three ways to store data of a user ( *on the web* ). These are mainly:
>
> - [Cookies](https://en.wikipedia.org/wiki/HTTP_cookie)
> - [Sessions](https://en.wikipedia.org/wiki/Session_(web_analytics))
> - Local Storage
>
> From what I understand its that as compared to *cookies* and *sessions*... As the word "*local*" tells us.
>
> It's going to store the *data* / *contents* on the user's machine / system.
>
> This means that even if the user **closes** the website, the information ( *the things that the user interacted with* ) is **saved** on *his* system!
>
> This even works for *development servers* like in [[Django Data View | Django]] or [liver-server](https://www.npmjs.com/package/live-server) from [Node](https://nodejs.org/en).

# Using The Local Storage

- Consider the following code below that I wrote:

```js
// function to ask the user to enter his name
function enterName() {
  // declare the variable that is going to store the name of the user
  let userName;

  // iterate through the `while` loop indefinitely
  while (true) {
    // ask the user to enter his name
    userName = prompt("Enter Name: ");

    // check for conditions
    if (userName === "") {
      // meaning that the user did not enter a name ==> output appropriate message
      alert("\n\t<< Please Enter Name!!! > > \n");

      // continue to ask the user to enter his username
      continue;
    }

    // if everything is valid ==> exit the `while` loop
    break;
  }

  // return the username to the "main" program
  return userName;
}

// call the function to ask the user to enter name
let userName = enterName();

// check if the user pressed the `Cancel` button
if (userName !== null) {
  // display the username to the console ( for "show" purposes )
  console.log(`Hello User ${userName}!!!`);

  // if the user did press the `Cancel` button
} else {
  // display a little message to the console
  console.log("The User Has Cancelled The Name Input!!!");
}

// store the username `userName` to the local storage ( for persistancy )
localStorage.setItem("userName", userName);

// retrieve the data stored on the local storage
const localNameData = localStorage.getItem("userName");

// display the data retrieved from the local storage
console.log(`Username ( Data ) Retrieved From Local Storage: ${localNameData}`);
```

> [!INFO] What This Code Does?
> The above code is going to some things:
>
> 1. Function that asks the user to enter his name
> 2. Displays the name to the console
> 3. Saves that name to the local storage
> 4. Retrieves that name from local storage to display to the console.

## Saving The Username

The code that is doing the actual *saving* and *retrieving* is only this part of the code.

```js
// store the username `userName` to the local storage ( for persistancy )
localStorage.setItem("userName", userName);

// retrieve the data stored on the local storage
const localNameData = localStorage.getItem("userName");

// display the data retrieved from the local storage
console.log(`Username ( Data ) Retrieved From Local Storage: ${localNameData}`);
```

The function / method `.setItem` is going to **save** the *value* entered by the user and then keep it inside the key `"userName"`.

Then the function / method `.getItem`; is going to **retrieve** the username and keep it inside the variable `localNameData`.

> Finally, we simply display the *value* of the variable store to the console!

> [!INFO] The **Storage** Tab
> In the inspect itself, you are going to see a tab named 'Storage'. Then if you head over to the `Local Storage/http://127.0.0.1:8080`; you see something like this:
>
> | Key | Value |
> | --- | ----- |
> | userName | SS92 |
>
> - Clicking on that `userName` key you are going to see this:
>
> ```json
> userName:"SS92"
> ```

> [!TIP] Where Data Saved?
> Different web browsers is going to have their own little *hidden* folder where they are going to store that data!
>
> > [!INFO] Resource(s)
> > - https://stackoverflow.com/questions/8634058/where-the-sessionstorage-and-localstorage-stored
> > - https://stackoverflow.com/questions/7079075/where-does-firefox-store-javascript-html-localstorage
>
> Given that I am using [Zen](https://zen-browser.app/), the *database* where that data is stored is going to be ( *for me* ) here:
>
> ```console
> /home/username/.zen/4evptyc9.Default (release)/webappsstore.sqlite
> ```
>
> Therefore, if you have [SQLite](https://sqlite.org/); you should be able to do something like this:
>
> ```sql
> SQLite version 3.50.4 2025-07-30 19:33:53
> Enter ".help" for usage hints.
> sqlite> .tables
> webappsstore2
> sqlite> .schema webappsstore2 
> CREATE TABLE webappsstore2 (originAttributes TEXT, originKey TEXT, scope TEXT, key TEXT, value TEXT);
> CREATE UNIQUE INDEX origin_key_index ON webappsstore2(originAttributes, originKey, key);
> sqlite> SELECT * FROM webappsstore2;
> ```
>
> > [!BUG] I Don't Get Anything!
> > Compared to this guy right here: https://stackoverflow.com/a/14901354. I **don't** get anything!
> >
> > I don't know that reason as to why its that, maybe because of the `npx live-server` or...
> >
> > > I am actually lost for words!
> >
>
> > [!SUCCESS]
> > Nevertheless, talking to the people here at Rogers... They are telling me that if its loaded / *seen* in the 'Inspect/Storage' tab.
> >
> > > Then it should be fine!
> >
>

---

> [!INFO]
> The reason that I made this very note is because my mentor at Rogers was telling me about how I use the user's **system** theme to be able to automatically set the theme!
>
> I made this specific note is because of I *did* not understand how to use it.
>
> The thing that I am currently coding right now is the 'Theme Toggle Button With Local Storage'... Hence, please refer to the file / note '[[Javascript - Document Object Model ( DOM )#Example Code - Dark / Light Mode Button With Local Storage | Javascript - Document Object Model ( DOM )]]' for a *practical* example!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!