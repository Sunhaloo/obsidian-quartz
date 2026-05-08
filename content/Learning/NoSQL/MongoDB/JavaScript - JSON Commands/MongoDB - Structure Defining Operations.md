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

## List of Contents

- [[#Login]]
- [[#Writing Comments]]
- [[#Creation of Databases]]
	- [[#Display All Databases]]
	- [[#Create - Switch Databases]]
	- [[#Verification of Creation of Databases]]
- [[#Deletion of Databases]]
	- [[#Making Database and Assigning User]]
	- [[#Actually Deleting Databases]]
- [[#Creation of Collections - Tables]]
	- [[#Displaying All Collections]]

---

## Resources

- User Defined Roles:
	- https://www.mongodb.com/docs/manual/core/security-user-defined-roles/
	- Create Role Function: https://www.mongodb.com/docs/manual/reference/method/db.createrole/
- Deletion of Databases:
	- Drop Database Function: https://www.mongodb.com/docs/manual/reference/method/db.dropDatabase/
	- `readWritAnyDatabase` Role: https://www.mongodb.com/docs/manual/reference/built-in-roles/#mongodb-authrole-readWriteAnyDatabase
	- `userAdminAnyDatabase` Role: https://www.mongodb.com/docs/manual/reference/built-in-roles/#mongodb-authrole-userAdminAnyDatabase
	- `dbOwner` Role: https://www.mongodb.com/docs/manual/reference/built-in-roles/#mongodb-authrole-dbOwner

## Login

If you have followed the note '[[MongoDB Document-Based Database Installation]]' and '[[MongoDB Introduction and Learning Setup]]' ( *in order* ) respectively. Then you know that our login credentials is going to be:

```console
username: dev_user
password: dev
database: dev_db
```

Therefore, the login for that user is going to be:

```bash
# login to 'mongosh' as the 'dev_user'
mongosh --username dev_user --password dev --authenticationDatabase dev_db
```

>[!WARNING] Security Risk: Password!
><p align="center"><span style="color: orange;">Don't Use <code>--password</code> Directly!!!</span></p>
>
>>But I am using it!?!
>
>Look, because are going and following this ( *what I like to call* ) "*tutorial documentation*"... I mean we all know that the password is `dev`. But if going to log into the **administrator** account whereby we **don't** want other people to see our password. We therefore, only use this command:
>
>```bash
># my administrator account --> see no password in "plain text"!
>mongosh --username azmaan --authenticationDatabase admin
>```
>
>This means that when I run the above $\uparrow$ command... MongoDB will then prompt me to enter the password and it looks something like this:
>
>```console
>Enter password: 
>```
>
>>[!NOTE]
>>The reason that we **don't** use the `--password` parameter is because of tools like '[zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions?tab=readme-ov-file)', '[fzf](https://github.com/junegunn/fzf)' and also reverse search!
>>
>>I know that most people that I am friends with don't even know Linux and don't understand the way Window Managers work... But still!
>

### MongoDB Compass

Now, if you are using [[MongoDB Document-Based Database Installation#MongoDB Compass | MongoDB Compass]]; when creating a new connection, use `localhost` and `dev_user`. Meaning that the *URL* / *URI* will look something like this $\downarrow$:

```console
mongodb://dev_user:dev@localhost:27017/
```

>[!WARNING] Add **Credentials** and Specify **Authentication Database**
>Yes! Not only do we have to specify the *username* and *password* ( *which we have already done with the URL $\uparrow$* ).
>
>But we also **need** to specify the *authentication database*. Else, MongoDB will scream as you!
>
>>I mean it makes completely sense if you look at it like so:
>>
>>```bash
>>mongosh --username dev_user --password dev --authenticationDatabase dev_db
>>```
>

>[!TIP] The Final URL
>After we have **successfully** established a connection... If we go ahead and check on the connection string ( *i.e the URL* ), we can see that it becomes like so:
>
>```console
>mongodb://dev_user:dev@localhost:27017/?authSource=dev_db
>```
>
>>Therefore, I now know how to connect directly **without** going into the 'Advanced' tab!
>

# Writing Comments

## Single Line Comments

```js
// this is a comment
// this is the same as our lovely C Programming Language
```

## Multi-Line Comments

```js
/*
This is a multi-line comment
It's similar to C and Java's multi-line comment.
*/
```

---

# Creation of Databases

## Display All Databases

There are a couple of ways that we can list out the database present in our "*session*"!

>You are going to find these command below!

```js
// most famous "show database" command
// --> returns a readable list database name + size
show databases
// or simply
show dbs
// or even
// --> returns an array containing all the collections found
db.getMongo().getDBNames()

// in my opinion, better version of 'show dbs'
// or 'db.getMongo().getDBNames()' as we get more information
db.adminCommand({ listDatabases: 1 })
// or simply
db.getMongo().getDBs()
```

>[!WARNING] Permissions, Permissions and Persmissions!
>For you to be able to actually run the `show dbs` or any other *equivalent* command... The user **must** have the `readAnyDatabase` *built-in* role or the `listDatabases` "*custom*" role.
>
>The `listDatabases` "*custom*" is more **low-level** than `readAnyDatabase`. Therefore, we can really fine-tune a user's permission.
>
>>Kindly refer to the [[#Resources]] section and search for '*User Defined Roles and ...*'
>

>I will be placing the output for each of the following command inside the **same** code block

```console
// 'show dbs' / 'show databases' output
admin   180.00 KiB
config   72.00 KiB
local    80.00 KiB

// 'db.getMongo().getDBNames()' output
[ 'admin', 'config', 'local' ]

// 'db.adminCommand({ listDatabases: 1 })' or
// 'db.getMongo().getDBs()' output
{
  databases: [
    { name: 'admin', sizeOnDisk: Long('184320'), empty: false },
    { name: 'config', sizeOnDisk: Long('73728'), empty: false },
    { name: 'local', sizeOnDisk: Long('81920'), empty: false }
  ],
  totalSize: Long('339968'),
  totalSizeMb: Long('0'),
  ok: 1
}
```

>[!NOTE]
>I had to do this in my `azmaan` administrator database as we actually have databases to list out!

### Display Current Database



## Create - Switch Databases

>Its so much easier than [[SQL Commands - Data Definition Language ( DDL )#Create Database | "traditional" SQL]]!

The command that we use to **create** and **switch** to that database in MongoDB is the `use` command.

```js
// create - switch to specified database
use db_name
```

In our case, as we authenticated as `dev_user` and we only have access to `dev_db`. We are going to **switch** to that database $\downarrow$:

```js
// "create" and switch to 'dev_db'
use dev_db
```

## Verification of Creation of Databases

>In short... We can't?!?

As you know, we created our `dev_user` inside the `dev_db` database.

>Refer to it [[MongoDB Introduction and Learning Setup#Create Development User | here]]!

Meaning that we should see our `dev_db` database, when we run these "*show database*" commands that we learned [[#Display All Databases | above]] $\uparrow$...

>I am currently back using the `dev_user` "*session*".

```js
// display all the database present
show dbs
```

- Output of `show dbs`:

```console

```

>Ahh nothing, let's try another method of displaying these pesky databases

```js
// this should clearly display all the database
db.adminCommand({ listDatabases: 1 })
```

```console

```

>Ahh nothing, let's try another method of displaying these pesky databases

```js
// this should clearly display all the database
db.adminCommand({ listDatabases: 1 })
```

- Output of `db.adminCommand({ listDatabases: 1 })`:

```console
{ databases: [], totalSize: Long('0'), totalSizeMb: Long('0'), ok: 1 }
```

>[!BUG] We don't see the Database
>Yes, this is **not** a bug, we actually don't see the database we created *until* we start **creating collections** ( *basically tables* ).
>
>Even if we currently have the user `dev_user` "**inside**" the `dev_db` database; here is proof ( *again, still on `dev_user` "session"* )
>
>```console
>dev_db> db.getUsers()
>{
>  users: [
>    {
>      \_id: 'dev_db.dev_user',
>      userId: UUID('e7c27569-7378-4a95-b968-5b30da0fa903'),
>      user: 'dev_user',
>      db: 'dev_db',
>      roles: [ { role: 'dbOwner', db: 'dev_db' } ],
>      mechanisms: [ 'SCRAM-SHA-1', 'SCRAM-SHA-256' ]
>    }
>  ],
>  ok: 1
>}
>```
>
>This tells me ( *and you* ) that MongoDB will only show us the database *if and only if* we have actual **data** inside that database.

### The "Fix"

>"*The Fix???*" You Ask...

Simply create a "`placeholder`" collection **inside** ( *obviously* ) the specific database that we want to show...

```js
// in our case, we need to display 'dev_db'
// switch to `dev_db`
use dev_db

// create the "placeholder" collection ( or table )
db.createCollection("placeholder")
```

>[!SUCCESS] [Success](https://www.youtube.com/watch?v=r13riaRKGo0)
>Now, when we run our "*show databases*" command, we do see that `dev_db` is actually fucking present!
>
>```console
>// inside administrator user
>// using 'show dbs' command
>admin   180.00 KiB
>config   72.00 KiB
>dev_db    8.00 KiB <--
>local    80.00 KiB
>
>// using 'db.adminCommand({ listDatabases: 1 })' command
>{
>  databases: [
>    { name: 'admin', sizeOnDisk: Long('184320'), empty: false },
>    { name: 'config', sizeOnDisk: Long('73728'), empty: false },
>    { name: 'dev_db', sizeOnDisk: Long('8192'), empty: false }, <--
>    { name: 'local', sizeOnDisk: Long('81920'), empty: false }
>  ],
>  totalSize: Long('348160'),
>  totalSizeMb: Long('0'),
>  ok: 1
>}
>```
>
>Doing the same thing inside the `dev_user` "*session*":
>
>```console
>// inside 'dev_user'
>// using 'show dbs' command
>dev_db  8.00 KiB
>
>// using 'db.adminCommand({ listDatabases: 1 })' command
>{
>  databases: [ { name: 'dev_db', sizeOnDisk: Long('8192'), empty: false } ],
>  totalSize: Long('8192'),
>  totalSizeMb: Long('0'),
>  ok: 1
>}
>```

# Deletion of Databases

To delete database, we simply need to run the `db.dropDatabase()` function. To show this... Let's make a database called `to_be_deleted` so that we can see *the function* in action

## Making Database and Assigning User

In our case, our `dev_user` has only one role `dbOwner` and that to, on the database `dev_db`!

Therefore, we are going to make some changes so that the user `dev_user` can create and add data to another database.

1. First, go ahead and log into you **administrator** account

```bash
# in my case, I do this
mongosh --username azmaan --authenticationDatabase admin
```

2. Grant role for `to_be_deleted` database to `dev_user`

```js
// switch to the 'dev_db' database
// as the user 'dev_user' is created inside 'dev_db'
use dev_db

// grant more roles to 'dev_user'
db.grantRolesToUser("dev",
[
    { role: "dbOwner", db: "to_be_deleted" }
])

// verify the "update" to role
db.getUser("dev_user")
```

Therefore, the `dev_user` should have the following roles:

```console
{
  _id: 'dev_db.dev_user',
  userId: UUID('e7c27569-7378-4a95-b968-5b30da0fa903'),
  user: 'dev_user',
  db: 'dev_db',
  roles: [
    { role: 'dbOwner', db: 'dev_db' },
    { role: 'dbOwner', db: 'to_be_deleted' }
  ],
  mechanisms: [ 'SCRAM-SHA-1', 'SCRAM-SHA-256' ]
```

3. Login as `dev_user` and create a *placeholder* collection inside `to_be_deleted`

```bash
# login into the development user
mongosh --username dev_user --password dev --authenticationDatabase dev_db
```

- Create the *placeholder* collection

```js
// switch to 'to_be_deleted' database
use to_be_deleted

// create the placeholder collection
db.createCollection("placeholder")
```

Now, go ahead and **log out** from the `dev_user` session and log **back in**!

>[!NOTE] You Don't Need To!!!
>Yes, we **don't** need to logout!
>
>I just do it because I want to... *Go Fuck Yourself*!!!

- Then run the following:

```js
// display the all the databases
show dbs
```

We should now have the following databases $\downarrow$:

```console
dev_db         8.00 KiB
to_be_deleted  8.00 KiB
```

## Actually Deleting Databases

>Now, "*its so simple to be happy but so difficult to be simple*"...

```js
// display all the availble databases
show dbs

// switch to the required database
use to_be_deleted

// verify that we actually are inside the 'to_be_deleted'
db

// delete the database
db.dropDatabase()

// verify that the database has been dropped
show dbs
```


After running the `db.dropDatabase()` command **inside** the `to_be_deleted` database, we should see something like this $\downarrow$:

```console
{ ok: 1, dropped: 'to_be_deleted' }
```

>[!WARNING] `dbOwner` / `dbAdmin` Needed!!!
>If you take the case of `azmaan` which is currently my administrator for MongoDB.
>
>This account <span style="color: red;">won't</span> be able to use the `db.dropDatabase()` function as the `userAdminAnyDatabase` and `readWriteAnyDatabase` does **not** provide this function to be used!
>
>Take a look at this; this was done **inside** the administrator account!
>
>```js
>// create - switch to 'to_be_deleted' database
>use to_be_deleted
>
>// create the placeholder collection
>db.createCollection("placeholder")
>
>// check if we are in the database 'to_be_deleted'
>db
>
>// delete the database 'to_be_deleted'
>db.dropDatabase()
>```
>
>But we don't get something like: `{ ok: 1, dropped: 'to_be_deleted' }`, but we get **an error**!
>
>```console
>MongoServerError[Unauthorized]: not authorized on to_be_deleted to execute
>command { dropDatabase: 1, lsid: { id:
>UUID("956ef77f-8a5f-499b-8256-db23d2a7e9a0") }, $db: "to_be_deleted" }
>```

>[!INFO] If you want to...
>As we ran the `db.grantRolesToUser()` function on the user `dev_user`, we can see that, `dev_user` has this role:
>
>```console
>{ role: 'dbOwner', db: 'to_be_deleted' }
>```
>
>But as, we have already deleted the database `to_be_deleted`... *If you want to*, you can remove this role!
>
>Simply run the following function below $\downarrow$:
>
>```js
>// remove the desired role from the user 'dev_user'
>db.revokeRolesFromUser("dev_user", [
>  { role: "dbOwner", db: "to_be_deleted" }
>])
>```
>
>If you run this function, we can see that we are back to where we started!
>
>```console
>{
>  users: [
>    {
>      \_id: 'dev_db.dev_user',
>      userId: UUID('e7c27569-7378-4a95-b968-5b30da0fa903'),
>      user: 'dev_user',
>      db: 'dev_db',
>      roles: [ { role: 'dbOwner', db: 'dev_db' } ],
>      mechanisms: [ 'SCRAM-SHA-1', 'SCRAM-SHA-256' ]
>    }
>  ],
>  ok: 1
>}
>```

# Creation of Collections - Tables

>We have been doing it already!

As you know; there are <strong><span style="color: red;">no</span></strong> **Structure Tables** when it comes to [[NoSQL Data View | NoSQL]] Databases.

This is what we NoSQL can be so great! You **don't** need to conform to a specific amount of *attributes* and can "*mix and match*" however you like.

Therefore, most '*Document-Based*' Stores ( *or simply 'Databases'* ) call this so-called "*tables*"... '**Collections**'.

>**Collections**

Yes, if you are coming from the realm of "*[[Microsoft SQL Server 2022 Data View | SQL Land]]*", the term 'table' here is going to be '**Collections**'.

>[!INFO]
>Now, not all of the NoSQL, i.e *Document-Based* stores are going to call these "*collections*".
>
>Now, the idea of when someone talks about '**table**' in *SQL* database, we know what they mean.
>
>>This is similar here!
>
>Whereby most people even if their *NoSQL Database Management System* does not use the actual term '**collection**'. Will know what you are talking about!

>[!NOTE] The Beauty of NoSQL
>So as you already know, they *structured table* found in SQL databases each have a series of **columns** / **fields**, whereby we store the *attributes* and also we have **rows** / tuples; where we keep all the data attached to an [[Entity Relationship Diagram ( ERD ) and Relationships | entity]].
>
>Therefore, we can saw that each *entity* is limited to that **amount** of *attributes* that the table is keeping track.
>
>>[!TIP] Solving The Problem
>>Compared to **tables**; *collections* only have **rows** which are known as '**Document(s)**' in the '[[NoSQL Data View | NoSQL land]]'.
>>
>>This means that we can keep on *adding* or *removing* attributes to our heart's content. This then solves the problem of some *entities* having more "*attributes*" that some others.
>

## Displaying All Collections

Similar to *listing out* all the [[#Display All Databases | databases]]. There are a couple of ways on how we can go about displaying all the collections found inside a database.

Below you are going to find most of them inside the code block $\downarrow$:

```js
// most famous "show collections" command
// --> returns a readable list database name + size
show collections

// --> returns an array containing all the collections found
db.getCollectionNames()

// if you want full details about all collections
db.getCollectionInfos()

// TIP: get full details about a single collection
// what I am trying to say is we can pass arguements inside!
db.getCollectionInfos({ name: "specific_collection_name" })
```

>[!WARNING] Permissions, Permissions and Permissions!
>To be able run the above *commands* and *functions*. The ( *or your "user"* ) needs to have the *minimal* **built-in** role of `read`!

>Below $\downarrow$ you are going to find the output for the above $\uparrow$ code block

```console
// 'show collections' output
system.users
system.version

// 'db.getCollectionNames()' output
[ 'system.version', 'system.users' ]


// 'db.getCollectionInfos()' output
[
  {
    name: 'system.version',
    type: 'collection',
    options: {},
    info: {
      readOnly: false,
      uuid: UUID('a7bd1604-49ba-4559-96fb-8b1fbbd6db7a')
    },
    idIndex: { v: 2, key: { _id: 1 }, name: '_id_' }
  },
  {
    name: 'system.users',
    type: 'collection',
    options: {},
    info: {
      readOnly: false,
      uuid: UUID('d20ba921-800d-40ea-869a-cc910ec1e9b2')
    },
    idIndex: { v: 2, key: { _id: 1 }, name: '_id_' }
  }
]

// NOTE: I did not show the last one...
// it either returns the details of said database
// if not found, its just returns 'null'
```

>[!INFO]
>In this case, I logged into my **administrator** *account*, `azmaan` as there ( *should be /* ) are more collections inside each databases.

## Create Collections

The command that we are going to use to **create** our *collection* is going to be done using the `db.createCollection()` function.

```js
// create the collection ( "table" ) 'collection_name'
db.createCollection("collection_name")
```

Therefore, let's go ahead and create the collection called `cars`.

```js
// create the collection 'cars'
db.createCollection("cars")
```

>[!SUCCESS] Verification of Creation of Collection `cars`
>To verify the creation of the collection; we can simply use the *command* and *functions* that displays all the collections inside a database.
>
>```js
>// using the 'show collections' command
>show collections
>
>// using the 'db.getCollectionInfos()' function
>db.getCollectionInfos({ name: "cars" })
>```
>
>Therefore, we should get an output that looks like this $\downarrow$:
>
>>Placing both outputs inside the same code block!
>
>```js
>// output using the 'show collections' command
>cars
>placeholder
>
>// output using the 'db.getCollectionInfos("cars")'
>[
>  {
>    name: 'cars',
>    type: 'collection',
>    options: {},
>    info: {
>      readOnly: false,
>      uuid: UUID('afe13ba6-e272-4f87-8dc7-6eb7adecb697')
>    },
>    idIndex: { v: 2, key: { _id: 1 }, name: '_id_' }
>  }
>]
>```
>You can also see that our `placeholder` collections does appear when we use the `show collections` databases!

### Permissions to use `db.createCollections()`

In mine ( *or "our"* ) case, you know that my administrator user has the following permissions:

```js
// display the permission of 'azmaan' administrator user
// INFO: the function below was executed inside `admin` database
// while being logged in as 'azmaan' and authenticated with `admin`
db.getUser("azmaan")
```

- This is going to output the permissions that my current administrator user has

```console
{
  _id: 'admin.azmaan',
  userId: UUID('81fa7b2b-466f-403d-99df-55a45318c885'),
  user: 'azmaan',
  db: 'admin',
  roles: [
    { role: 'readWriteAnyDatabase', db: 'admin' },
    { role: 'userAdminAnyDatabase', db: 'admin' }
  ],
  mechanisms: [ 'SCRAM-SHA-1', 'SCRAM-SHA-256' ]
}
```

>[!INFO] Permission for Administrator Account
>As you can see, my administrator *account* has these **built-in** roles:
>
>1. `readWriteAnyDatabase`
>2. `userAdminAnyDatabase`

---

Switching to our `dev_db` database while still being authenticated as our **administrator user**, we can clearly see that our `dev_user` only have 1 **built-in** role and that should be the `dbOwner` role!

```js
// display the permission of 'dev_user' administrator user
db.getUser("dev_user")
```

- This is the output after executing the above command:

```console
{
  _id: 'dev_db.dev_user',
  userId: UUID('e7c27569-7378-4a95-b968-5b30da0fa903'),
  user: 'dev_user',
  db: 'dev_db',
  roles: [ { role: 'dbOwner', db: 'dev_db' } ],
  mechanisms: [ 'SCRAM-SHA-1', 'SCRAM-SHA-256' ]
}
```


#### Using the `db.createCollection()` Function

Now, to be able to use the create collection function, `db.createCollection()`. You <strong><span style="color: red;"></span></strong> to have the `readWrite` **built-in** role!

Now, the above mentioned *users*, currently have these roles:

- `readWriteAnyDatabase`
- `userAdminAnyDatabase`
- `dbOwner`

Below you are going to find a *Mermaid Diagram* / flowchart to see as to why we can use the `db.createCollection()` function.

```mermaid
flowchart TD
	A([Start]) --> B
	A([Start]) --> D
	B[userAdminAnyDatabase] --> C[ X ]
	D[readWriteAnyDatabase] --> E[readWrite]
	E[readWrite] --> F[createCollection Function]
	G[dbOwner] --> F
```

>As you can see both of our users in this case, have the `readWrite` role!

#### Making a Point

Now the `read` **built-in** should **not** let us use the `db.createCollection()` function.

Let's us try to make another `testing_user` to check what minimal role should be assigned to a user to be able to **create** collections inside a database.

- Create the following user inside the `dev_db` database

```bash
# login as the administrator user
# in my case, the administrator user is 'azmaan'
mongosh --username azmaan --authenticationDatabase admin
```

```js
// run the function / method '.createUser'
// passing the correct arguments
db.createUser({
    // provide the username ==> 'dev_user'
    user: "testing_user",
    // provide the password for 'dev'
    pwd: "test",
    // declare the array 'roles' to grant permission
    roles: [
        {
            // assign a minimal role without being able to
            // create collections inside the database
            role: "read",  db: "dev_db"
        }
    ]
})
```

- Login into `dev_db` as `testing_user`

```bash
# login as the testing user
mongosh --username testing_user --password dev --authenticationDatabase dev_db
```

- Try to create a collection called `test` inside the `dev_db` database

```js
// display all the available database
show dbs

// switch into the 'dev_db' database
use dev_db

// check that we are in the correct database
db

// try to create a collection called `test`
db.createCollection("test")

// check if the collection has been created successfully
db.getCollectionInfos({ name: "test" })
```

- This is the output after running the above $\downarrow$ code block inside of `mongosh`

>I am going to place all the outputs into a single code block

```console
dev_db  16.00 KiB


switched to db dev_db


dev_db


MongoServerError[Unauthorized]: not authorized on dev_db to execute command { create: "test", lsid: { id: UUID("087ce483-6485-4dbf-ba73-8ba818aeddb5") }, $db: "dev_db" }
```

#### Grant Test User `readWrite` Permission

Now, we are going to grant the `testing_user` the `readWrite` permission.

This should be the most *minimal* **built-in** role that will allow any user to be able to **use** the `db.createCollection()` function.

- Grant the `readWrite` permission to `testing_user`

```js
db.grantRolesToUser("testing_user",
	[
		{
			role: "readWrite", db: "dev_db"
		}
	])
```

- Therefore, we should see that our `testing_user` now has **two** roles!

```console
{
  _id: 'dev_db.testing_user',
  userId: UUID('cbc08d9a-3b35-43b9-8bc2-a2ff0ab820f9'),
  user: 'testing_user',
  db: 'dev_db',
  roles: [
    { role: 'readWrite', db: 'dev_db' },
    { role: 'read', db: 'dev_db' }
  ],
  mechanisms: [ 'SCRAM-SHA-1', 'SCRAM-SHA-256' ]
}
```

- Retry the above commands $\uparrow$

>I am going to *log out* and then *log back in*!

```console
dev_db  16.00 KiB


switched to db dev_db


dev_db


{ ok: 1 }


[
  {
    name: 'test',
    type: 'collection',
    options: {},
    info: {
      readOnly: false,
      uuid: UUID('bde0c398-cb4b-402d-8ca3-dd276d9f6c04')
    },
    idIndex: { v: 2, key: { _id: 1 }, name: '_id_' }
  }
]
```

>In this case, we should be able to see that we created the `test` collection!

>[!SUCCESS]
>We now see that we have successfully created our **collection**!
>
>>[!TIP] Cleaning Up
>>- Remove the `test` collection created in `dev_db` database
>>
>>```js
>>// remove the `test` collection
>>// we are going to get to deletion just after this
>>db.test.drop()
>>
>>// check if the collection has actually been deleted
>>show collections
>>```
>>
>>
>>- Remove the `testing_user` created by administrator user
>>
>>
>>```js
>>// remove the `testing_user`
>>db.dropUser("testing_user")
>>
>>// check if the deletion of the user
>>db.getUser("testing_user")
>>```
>

# Deletion of Collections - Tables



---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/channel/UCMkQZsuW6eHMhdUObLPSpwg
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!