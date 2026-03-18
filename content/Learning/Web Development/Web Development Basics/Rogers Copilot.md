---
id: Rogers Copilot
aliases: Rogers Capital own Large Language Model platform
tags:
  - CSS
  - HTML
  - JS
  - react
author: S.Sunhaloo
date: 2025-12-22
status: In-Progress
---

## List of Contents

- [[#Setup Project]]
	- [[#Tailwind Installation]]
	- [[#ShadCN Installation]]
	- [[#Setup Backend]]
- [[#Simple Database Setup]]

---

# Setup Project

- Setup private GitHub repository:

```bash
# use github-cli to create repository
gh repo create Rogers --private --add-readme --description "Rogers Copilot" --clone
```

- Create React's front-end folder:

```bash
# create the react project
npm create vite@latest client -- --template react
```

- Create React's back-end folder:

```bash
# create the back-end folder
mkdir backend

# switch to that folder
cd server
```

- Initialise the back-end folder using `npm`:

```bash
# initialise back-end with node
npm init -y
```

> I am going to get back to the back-end later on.

## Tailwind Installation

> [!NOTE] Resource(s)
> 
> - https://tailwindcss.com/docs
> 	- https://tailwindcss.com/docs/installation/using-vite

We are now going to install Tailwind in our React project and use Tailwind to style our components

> Additionally 'ShadCN' uses Tailwind CSS!

- Run the following command to install the 'tailwind' package(s):

```bash
# install tailwind in our front-end / client react project
npm install tailwindcss @tailwindcss/vite
```

- Configure the `client/vite.config.js` file to add 'tailwind':

```js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

// add tailwind styling
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  plugins: [react(), tailwindcss()],
});
```

- Update our `client/src/index.css` file to simply have this:

```css
@import "tailwindcss";
```

> Go ahead and also delete all the *codes* found inside `App.css` file.

> [!TIP] Success
> 
> We have been able to successfully install Tailwind into our project.

## ShadCN Installation

- Create the `client/jsonfig.json` file:

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

- Run ShadCN installation command using `npx`:

```bash
# install shadcn into our project
npx shadcn@latest init
```

> For the base colour; we choose 'Neutral'!

- You should see something like this after running the above command:

```console
✔ Preflight checks.
✔ Verifying framework. Found Vite.
✔ Validating Tailwind CSS config. Found v4.
✔ Validating import alias.
✔ Which color would you like to use as the base color? › Neutral
✔ Writing components.json.
✔ Checking registry.
✔ Updating CSS variables in src/index.css
✔ Installing dependencies.
✔ Created 1 file:
  - src/lib/utils.js

Success! Project initialization completed.
You may now add components.
```

### Testing Front-End React Project

We are now going to test if everything that we have installed in our front-end project has been setup correctly.

- Install / *Import* the `button` component from ShadCN:

```bash
# add the 'button' component from shadcn
npx shadcn@latest add button
```

- Update the `client/vite.config.js` file to this below:

```js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import path from "path";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  plugins: [react(), tailwindcss()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
});
```

- Update our `shadcn/client/src/App.jsx` file:

```jsx
import "./App.css";
import { Button } from "@/components/ui/button";

function App() {
  return (
    <>
      <div className="min-h-screen flex items-center justify-center">
        <Button> Click me!</Button>
      </div>
    </>
  );
}

export default App;
```

> [!TIP] Success
> 
> Therefore, running the front-end's development server using the `npm run dev` command. You should see that there is a button in the middle of our screen!

> [!WARNING] Copilot Kit ( Front-End )
> As we are going to be using Copilot Kit, we are going to have to install it. This can be done using the following command below:
> 
> ```bash
> # download the required packages to be able to work with copilot kit
> npm install @copilotkit/react-core @copilotkit/react-ui @copilotkit/runtime
> ```


## Back-end Setup

- Install the required dependencies in our `backend` folder:

```bash
# install the required dependencies in our back-end
npm install express knex pg cors dotenv jsonwebtoken
```

- Install `nodemon` package so that back-end is able to reload on changes:

```bash
# install what is essentially what's 'Vite' is doing
npm install --save-dev nodemon
```

- Create files and folders

```bash
# create the required files
touch index.js knexfile.js .env .gitignore

# create the required folders
mkdir db controllers routes middleware
```

- Update the `backend/.gitignore` file to be like this:

```bash
# Unccessary files and folders
node_modules/

# Environment Variables
.env
.env.development
.env.production
```

- Update our `backend/package.json` file to be like this:

```json
{
  "name": "backend",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "type": "commonjs",
  "devDependencies": {
    "nodemon": "^3.1.11"
  }
}
```

> [!NOTE]
> I have added a `temp.txt` file in all of these empty directories so that they can be pushed to remote repository!

> [!TIP] Success
> 
> I have been able to make an extremely simple and rudimentary test by adding `console.log("Hello World from Backend Folder!");` to the `backend/index.js` file.
> 
> Running the development server using the `npm run dev` command, I see that we do have the correct output:
> 
> ```console
> backend@1.0.0 dev
> nodemon server.js
> [nodemon] 3.1.11
> [nodemon] to restart at any time, enter `rs`
> [nodemon] watching path(s): *.*
> [nodemon] watching extensions: js,mjs,cjs,json
> [nodemon] starting `node server.js index.js`
> Hello World from Backend Folder!
> [nodemon] clean exit - waiting for changes before restart
> ```
> 
> > Very Nice!

> [!WARNING] Copilot Kit ( Back-End )
> As we are going to be using Copilot Kit, we are going to have to also install it inn our back-end. This can be done using the following command below:
> 
> ```bash
> # download the required packages to be able to work with copilot kit
> npm install @copilotkit/runtime body-parser
> ```

---

# Simple Database Setup

- Add the following code to the `backend/knexfile.js` file:

```js
require("dotenv").config();

module.exports = {
  development: {
    client: "postgresql",
    connection: process.env.DATABASE_URL,
    pool: {
      min: 2,
      max: 10,
    },
    migrations: {
      directory: "./db/migrations",
    },
    seeds: {
      directory: "./db/seeds",
    },
  },

  production: {
    client: "postgresql",
    connection: process.env.DATABASE_URL,
    pool: {
      min: 2,
      max: 10,
    },
    migrations: {
      directory: "./db/migrations",
    },
    seeds: {
      directory: "./db/seeds",
    },
  },
};
```

- Create the migration files using the following commands found in the code block below:

```bash
# create the employee table
npx knex migrate:make employees

# create the employee_absence table
npx knex migrate:make employees_absence
```

> You should see that 2 files have been created inside the `backend/db/migrations` file!

## Employees Table

- Modify the `backend/db/migrations/{datetime}_employees.js` file to this:

```js
/**
 * @param { import("knex").Knex } knex
 * @returns { Promise<void> }
 */
exports.up = function (knex) {
  return knex.schema.createTable("employees", (table) => {
    table.increments("id").primary();
    table.string("firstname", 50).notNullable().unique();
    table.string("lastname", 50).notNullable().unique();
    table.string("telephone").notNullable();
    table.string("address").notNullable();
    table.string("email", 100).notNullable().unique();
    table.string("password").notNullable();
    table.timestamps(true, true);
  });
};

/**
 * @param { import("knex").Knex } knex
 * @returns { Promise<void> }
 */
exports.down = function (knex) {
  return knex.schema.dropTable("employees");
};
```

## Employee's Absence Table

- Modify the `backend/db/migrations/{datetime}_employees_absence.js` file to this:

```js
/**
 * @param { import("knex").Knex } knex
 * @returns { Promise<void> }
 */
exports.up = function (knex) {
  return knex.schema.createTable("employees_absence", (table) => {
    table.increments("id").primary();
    table.date("date").notNullable();
    table.timestamps(true, true);
    table.integer("employee_id").unsigned().notNullable();
    table.foreign("employee_id").references("employees.id").onDelete("CASCADE");
  });
};

/**
 * @param { import("knex").Knex } knex
 * @returns { Promise<void> }
 */
exports.down = function (knex) {
  return knex.schema.dropTable("employees_absence");
};
```

> [!WARNING] No Migrations Have Been Ran
> I did **not** run the `npx knex migrate:latest` yet!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!