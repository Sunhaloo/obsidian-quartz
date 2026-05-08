---
id: MongoDB Introduction and Learning Setup
aliases: MongoDB Introduction and Setup Configuratation for notes
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

- [[#Preface]]
- [[#Setup Dummy User]]
	- [[#Steps To Create Development Account]]
	- [[#Login To New Development User]]

---

## Preface

Well, we are now going to **learn** about *functions* and *operations* so that we can actually use the flipping program!

Now, I hope that you ( *and I* ) have already follow the **comprehensive** guide that I made over at '[[MongoDB Document-Based Database Installation]]' and you have already created your "*admin-user*" as per the the documentation.

>[!INFO]
>Now I have **not** done an installation guide for Windows simply because its for normies!
>
>>Simple as that!
>

# Setup Dummy User

Before we start, we are now going to create a *dummy user* so that we can "*fuck around and find out*" thing about MongoDB.

Let's go ahead and create a **testing** user with the *username* `dev_user` and *password* `dev` that will be able to operate the database `dev_db`.

## Steps To Create Development Account

### Verify Development User Existence

Let's go ahead and check if the database `dev_db` and / or the user `dev_user` has already been created!

#### Check Presence of Development Database

```js
// show all the database that are currently available
show dbs

// alternatively, we could run the command
db.getMongo().getDBNames()
```

In my case, the output that I get is like so $\downarrow$:

- Using `show dbs`:

```console
admin   180.00 KiB
config   72.00 KiB
local    80.00 KiB
```

- Using `db.getMongo().getDBNames()`:

```console
[ 'admin', 'config', 'local' ]
```

>[!WARNING] "*Hidden*" Databases!!!
>Now, even if we go ahead and do:
>
>1. Switch / Create the database `dev_db` with the `use` command
>2. Create the user `dev_user` with the function `db.createUser()`
>
>After we **log-out** and login again; we are <strong><span style="color: red;">not</span></strong> going to see the database `dev_db` when we use the `show dbs` command / statement!
>
>>[!INFO] Why is that so???
>>This is because, MongoDB will only show the databases ( *with the `show dbs` command* ) that have actual *data* / **collections** in them!
>
>>*Then what should be do*?
>
>>[!TIP] Showing Hidden Databases - Placeholder Database and Data
>>
>>>[!INFO] Resource
>>>https://stackoverflow.com/questions/25947929/how-to-list-all-databases-in-the-mongo-shell
>>
>>>*Long Story Short; You Can't Directly See Hidden Database*!!!
>>
>>This means that we are going to have to create a *placeholder* collection, **with data inside**, the database so that we can actually see the database when we run the command `show dbs`
>>
>>```js
>>// switch to the required database
>>use dev_db
>>
>>// create the placeholder collection ( 'table' )
>>db.createCollection("placeholder")
>>
>>// insert a temporary data inside that 'placeholder' database
>>db.placeholder.insertOne({ temp: true })
>>```
>>
>>Instead of *creating* the collection and then *inserting* data into it... We can simply run the command:
>>
>>```js
>>// create the placeholder collection
>>// insert a temporary data inside that 'placeholder' database
>>// TIP: does both the creation and insertion
>>db.placeholder.insertOne({ temp: true })
>>```
>>
>>This is also **valid** as we know that there are no *collections* currently called `placeholder`. Therefore, MongoDB will **automatically** run the `db.createCollection()` function for us!
>>
>
>>[!TIP] Showing Hidden Databases - `db.stats()` Function
>>Like we have said, there are currently *no* **direct way** of showing "*hidden*" databases ( *that I know of* ). But we can definitely use the `db.stats()` command.
>>
>>>Well, guess from the name of the function what it will output? *Fucking Shitter*!
>>
>>Let's go ahead and check if our database `dev_db` is currently empty!
>>
>>```js
>>// switch to the required database
>>use dev_db
>>
>>// check if the database is has nothing in it
>>db.stats()
>>```
>>
>>We should all get an output that looks like this $\downarrow$. As we don't have `dev_db`!
>>
>>```console
>>{
>>  db: 'dev_db',
>>  collections: Long('0'),
>>  views: Long('0'),
>>  objects: Long('0'),
>>  avgObjSize: 0,
>>  dataSize: 0,
>>  storageSize: 0,
>>  indexes: Long('0'),
>>  indexSize: 0,
>>  totalSize: 0,
>>  scaleFactor: Long('1'),
>>  fsUsedSize: 0,
>>  fsTotalSize: 0,
>>  ok: 1
>>}
>>```
>>
>>Compare to running `db.stats()` inside the `admin` database, I get something like this:
>>
>>```console
>>{
>>  db: 'admin',
>>  collections: Long('2'),
>>  views: Long('0'),
>>  objects: Long('4'),
>>  avgObjSize: 314.5,
>>  dataSize: 1258,
>>  storageSize: 73728,
>>  indexes: Long('3'),
>>  indexSize: 110592,
>>  totalSize: 184320,
>>  scaleFactor: Long('1'),
>>  fsUsedSize: 32334225408,
>>  fsTotalSize: 52521566208,
>>  ok: 1
>>}
>>```
>

#### Check Presence of Development User

We are now going to check if `dev_user` has been created inside the `dev_db` database.

I usually run the following function `db.getUsers()`. But I am also going to run `db.getUser()`!

```js
// check if the 'dev_user' exists inside 'dev_db'
db.getUsers()

// check existence of 'dev_user' by passing its username
db.getUser("dev_user")
```

Again, in my case, I don't have the user `dev_user` created. Therefore my output should be `null`!

- Using the function `db.getUsers()`

```console
{ users: [], ok: 1 }
```

- Using the function `db.getUser("dev_user")`

```console
null
```

>[!INFO]
>As you can see; because `db.getUsers()` output all the users in *that specific* database... It returns a JSON output!

### Create Development User

If we don't have `dev_db` and `dev_user`. This means that we are going to actually create them, *right now and right here*!!!

1. Authenticate with the '*admin-user*' in my case, I am going to run:

>Again, I have expected you to have already read [[MongoDB Document-Based Database Installation#Setup Administrator User | this]] $\leftarrow$!

```bash
# login as the administrator user
# in my case, the administrator user is 'azmaan'
mongosh --username azmaan --authenticationDatabase admin
```

2. Create and Switch to the `dev_db` Database

```js
// switch to the required database
use dev_db
```

3. Actually create the new `dev_user`

```js
// run the function / method '.createUser'
// passing the correct arguments
db.createUser({
    // provide the username ==> 'dev_user'
    user: "dev_user",
    // provide the password for 'dev'
    pwd: "dev",
    // declare the array 'roles' to grant permission
    roles: [
        {
            // assign the 'dbOwner' role to user 'dev_user'
            // 'dbOwner' allows user to have
            // general functions for CRUD operations and more
            // NOTE: the user 'dev_user' only have permissions
            // for 'dev_db' database
            role: "dbOwner",  db: "dev_db"
        }
    ]
})
```

>[!SUCCESS] Verification of Creation of `dev_db`
>To verify if we successfully created the database `dev_db`, I am going to use the `db.stats()` function!
>
>```js
>// the 'dev_db' database should NOT be empty
>db.stats()
>```
>
>Again, the database should **not** be empty!!!
>
>```console
>{
> db: 'dev_db',
> collections: Long('0'),
> views: Long('0'),
> objects: Long('0'),
> avgObjSize: 0,
> dataSize: 0,
> storageSize: 0,
> indexes: Long('0'),
> indexSize: 0,
> totalSize: 0,
> scaleFactor: Long('1'),
> fsUsedSize: 0,
> fsTotalSize: 0,
> ok: 1
>}
>```
>
>>[!NOTE] Ohh, Its Empty!!!
>>>Well, fuck this shit!!!
>>
>>Nevertheless, I will be asking somebody about this!
>

>[!SUCCESS] Verification of Creation of `dev_user`
>To verify if we successfully created the user `dev_user`, we can use the function `db.getUser()` or `db.getUsers()`.
>
>```js
>// check if the 'dev_user' has been created
>db.getUser("dev_user")
>```
>
>This should output something like this:
>
>```console
>{
>  \_id: 'dev_db.dev_user',
>  userId: UUID('dcb0eb51-28c3-49b6-ba30-ceb53642566e'),
>  user: 'dev_user',
>  db: 'dev_db',
>  roles: [ { role: 'dbOwner', db: 'dev_db' } ],
>  mechanisms: [ 'SCRAM-SHA-1', 'SCRAM-SHA-256' ]
>}
>```


### Login To New Development User

Hence, we should be able to **login** with as our new *user* `dev_user` with the correct password!

```bash
# login as the development user
mongosh --username dev_user --authenticationDatabase dev_db
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/channel/UCMkQZsuW6eHMhdUObLPSpwg
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!