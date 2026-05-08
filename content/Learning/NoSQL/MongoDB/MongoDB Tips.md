---
id: MongoDB - Structure Defining Operations
aliases: MongoDB Data Definition "Language" Functions and Keywords
tags:
  - NoSQL
  - db
  - uni
  - uom
author: S.Sunhaloo
date: 2025-05-30
status: In-Progress
---

# 30/05/2025 - Creation of Users

## Using Admin Itself

1. Authenticate as admin user
2. `use admin` --> switch to the 'admin' database
3. Create the user inside 'admin'

This means that the argument `--authenticationDatabase` should be 'admin' as that user's credentials are stored inside the 'admin' database.

Nevertheless, when we do login as *that* user... We are going to be dropped into the 'test' database by default (  basically how MongoDB works ).

Hence, we therefore, need to actually switch / create the database ( *like the database that we want to use* ) by using the `use` keyword.

>[!NOTE]
>We normally use 'admin' database to create "administration" users!

## Using Specific Database

1. Authenticate as admin user
2. `use x` --> switch to the specific database
3. Create the user inside that database

This now means we are going to have to authenticate with `--authenticationDatabase specific_database`. Now, we are going to be dropped, again, into the 'test' database by default. We therefore, **need to switch** to that specific database.

For example, lets say that we created the user with database 'x'. Therefore, we authenticate with database 'x'. But when we login we do:

```js
use fuck_you
```

And then we try to create collection... This is what's going to happen:

```js
fuck_you> db.createCollection("fuck_you")
MongoServerError[Unauthorized]: not authorized on
fuck_you to execute command 
```

# 25/06/2025 - Clearing The MongoDB Shell

To clear the MongoDB Shell. we can simply use the following command $\downarrow$:

```js
// clear the mongodb shell
cls
```

This is very useful when you **don't** have access to the `<Ctrl> + L` keyboard shortcut, when for example, you are in [TMUX](https://github.com/tmux/tmux/wiki)

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/channel/UCMkQZsuW6eHMhdUObLPSpwg
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!