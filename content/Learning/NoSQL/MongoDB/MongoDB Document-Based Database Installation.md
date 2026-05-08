---
id: MongoDB Document-Based Database Installation
aliases: MongoDB NoSQL Database Management System
tags:
  - NoSQL
  - db
  - uni
  - uom
author: S.Sunhaloo
date: 2025-05-29
status: Completed
---

## List of Contents

- [[#Operating Systems]]
	- [[#Arch, Arch, Arch!!!]]
	- [[#Licensing Change]]
- [[#Installation Process]]
	- [[#AUR Helper]]
	- [[#MongoDB and MongoDB Compass]]
- [[#Configuration Process]]
	- [[#Services]]
	- [[#Setup Administrator User]]
		- [[#Steps To Setting Up Administrator User]]
- [[#MongoDB Compass]]
	- [[#Local Hosts]]

---

# Operating Systems

## Arch, Arch, Arch!!!

>I use Arch BTW!

MongoDB is available on Linux Systems; I am simply going to write the installation and configuration process for Arch Linux only!

>[!INFO] Why Arch Linux Only?
>Because Windows Systems are for [normies](https://www.urbandictionary.com/define.php?term=normies); the installation process is really really simple.
>
>"*Point and Click*" [Simply Lovely](https://www.youtube.com/watch?v=OtjsHokKUgI&t=9s)

## Licensing Change

Initially, MongoDB was **open-source** but then when *closed-source* and changed their license from '[GNU Affero General Public License](https://en.wikipedia.org/wiki/GNU_Affero_General_Public_License)' to '[Server Side Public License](https://en.wikipedia.org/wiki/Server_Side_Public_License)'.

If you want; you can have a read over here: https://www.zdnet.com/article/its-mongodbs-turn-to-change-its-open-source-license/

>Long story short; they changed their license because of companies like [AWS](https://en.wikipedia.org/wiki/Amazon_Web_Services) ( *from my understanding* )


>[!INFO] Hence, the [Arch User Repository ( AUR )](https://aur.archlinux.org/)!
>Because of this change, we don't have MongoDB inside the main Arch repositories... Heck, even distributions like Debian, Fedora all **removed** the "mongodb" package from their main repos.
>
>But as we are '*Arch Linux*' users... We don't have to worry about anything!
>
>>We can just use the beautiful 'AUR' baby!
>

---

# Installation Process

## AUR Helper

Now, to be able to download packages quickly and efficiently from the 'AUR', we are going to use '[yay](https://github.com/Jguer/yay)'.

Now some people like to use '[paru](https://github.com/Morganamilo/paru)' but I have never used it and don't plan on using it!
But if you use `paru`, then do your thing!

### Yaaaayyyy!!!

#### Installing Yay

To be able to use `yay`, we are going to run the following commands below $\downarrow$:

```bash
# download needed dependencies
sudo pacman -S --needed git base-devel
# clone the repository
git clone https://aur.archlinux.org/yay.git
# change directory to that repository / folder
cd yay
# compile the thing
makepkg -si

# ( if you want to ) delete all the unecessary files after
cd .. && rm -rf yay
```

>[!SUCCESS] Verification of Installation
>We can simply verify the installation of `yay` by just checking its version:
>
>```bash
>yay --version
>```
>
>If you want, we can also try to find it in our `/usr/bin` folder!
>
>```bash
>ls /usr/bin/ | grep "yay"
>```

## MongoDB and MongoDB Compass

To install [MongoDB](https://www.mongodb.com/), we download it from the 'Arch User Repository'!

>[!NOTE] What is MongoDB Compass?
>[MongoDB Compass](https://www.mongodb.com/products/tools/compass) is basically [[Microsoft SQL Server 2022 Introduction#SQL Server Management Studio Installation | SQL Server Management Studio]] whereby it the official GUI for the MongoDB Server!
>
>Therefore, we can say that its just the [[Database Management System ( DBMS )]] of MongoDB!
>
>>Now, I don't think that I will be using the GUI... But we never know what could happen.
>>
>>Additionally, if you try to use a Windows computer and they have it installed... I think its just better to use the GUI over there!
>

```bash
# download and install the MongoDB server binary
yay -S mongodb-bin

# download and install the MongoDB GUI binary
yay -S mongodb-compass-bin

# to download both at the same time
yay -S --noconfirm mongodb-bin mongodb-compass-bin
```

>[!WARNING] Building From Source!
><p align="center"><span style="color: orange;">I don't recommend this at all!!!</span></p>
>
>This is a massive waste of time and "*resources*" in my opinion!
>
>"*Why*" you ask. Because installing `mongodb` and `mongodb-compass` **instead** of `mongodb-bin` and `mongodb-compass-bin` means that you are going to '**build them from source**'!
>
>Now, if you wish, you can go with this route but it might take you 5+ hours!
>
>>You think I am joking right; take a look at this: https://bbs.archlinux.org/viewtopic.php?id=259365
>>If you have a pretty powerful computer and have the patience... *You can therefore GO FUCK YOURSELF*!

# Configuration Process

## Services

After the installing, try running `mongosh` into your terminal and see what *output* you get.

>Yes An Error!

You **need** to see an error that goes along the line of:

```console
Current Mongosh Log ID:	683833b1588e2cfd0ac59f34
Connecting to:		mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.5.1
MongoNetworkError: connect ECONNREFUSED 127.0.0.1:27017
```

>[!TIP] A Network Error!
>Similar to most databases... They have a *client-server* architecture. This means that if they *server* is **not** running.
>
>You won't be able to access anything ( *like your databases and more* ).
>
>But I think that Windows ( *again for normies its good* ) does that process automatically for you after a "*restart*".
>
>>Just checked, it **does do** that automatically during the installation process itself!
>

### Starting Services

>We are now going to use the `systemctl` command!

To start the service, we can simply run the following command:

```bash
# start the mongodb server / service
systemctl start mongodb.service
```

>[!NOTE]
>This will prompt you to enter your password. Hence, simply enter your *machine's* password ( *like your fucking user-login password for your PC* ).
>
>>Is that not simple enough?
>

>[!SUCCESS] Verification of Startup
>To check if the `mongodb.service` has actually started, we can simply run the command:
>
>```bash
># check the status of mongodb service
>systemctl status mongodb.service
>```

#### Therefore

We can now try to start `mongosh` again and now we should see something like this:

```console
Current Mongosh Log ID:	68383bc41c89386f84c59f34
Connecting to:		mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.5.1
Using MongoDB:		8.0.9
Using Mongosh:		2.5.1

For mongosh info see: https://www.mongodb.com/docs/mongodb-shell/

test> 
```

>[!SUCCESS] No Errors!!!
>

>[!NOTE] Enabling The Service On Boot
>Given that this is **not** Windows and I can simply run the above $\uparrow$ command to *start* or *stop* the `mongodb.service` as the speed of light.
>
>I personally will <span style="color: red;">not</span> be *enabling* the service to **start** on boot!
>
>Obviously, I will *lose* some **convenience** but what I will lose in convenience will be *gained* in terms of **performance**.
>
>But if you have a "*work machine*", I think its better of to enabled it on boot!
>
>Therefore, you can go ahead enabled the service with the command below:
>
>```bash
># enable mongodb service to start on boot
>systemctl enable mongodb.service
>```

## Setup Administrator User

Now, when working with [[Microsoft SQL Server 2022 Data View|MS SQL]], if you are working locally and using the "*Windows server*". You know that the administrator has a username of `dbo`.

In our case, we need to **create** one from scratch. Hence, please follow the steps found below $\downarrow$ carefully.

### Steps To Setting Up Administrator User

1. Setup the actual user inside `mongosh`

```json
// switch to the 'admin' database
use admin

// actually create administrator / admin-user
db.createUser(
  {
    // specify the admin's username
    user: "your_username",
    // specify the password for that admin
    pwd: "your_password",
    // allow this user to manage users on any database
    roles: [
        { role: "userAdminAnyDatabase", db: "admin"
        },
        // grant read and write access to all databases
        "readWriteAnyDatabase"
    ]
}
)
```

>[!SUCCESS] Should Receive `{ ok: 1 }` As Output!
>

- Explanation of above code using 'MS SQL Server 2022'

The above command basically translate to:

```SQL
-- create the actual login
-- which will 
CREATE LOGIN admin_login
WITH PASSWORD = 'your_password';

-- switch to the 'admin' database
USE master;

-- apply the login details to that admin-user
CREATE USER your_username
FOR LOGIN admin_login
WITH DEFAULT_SCHEMA = dbo;

-- give user 'your_username' all privileges
GRANT CONTROL
ON master
TO your_username
WITH GRANT OPTION;
```

2. Test the login created

>[!NOTE] No need to close original `mongosh` session
>Just open another terminal or TMUX window and then follow what I wrote below!

To be able to correctly enter the *database* using **authentication**; we need to first understand what *arguments* we can pass to `mongosh`.

>I mean just run `mongosh --help` to see everything

But we are interested in 2 main things; they are:

1. `--username`
2. `--authenticationDatabase`

Therefore, the *format* of our command to login as our 'admin' will be like so:

```bash
# login and authenticate as the administrator
mongosh --username your_username --authenticationDatabase database_name
```

Hence, our real command in this case would be something that looks like this:

```bash
# login and authenticate as the administrator
mongosh --username your_username --authenticationDatabase admin
```

What we just did above, in terms of '*MS SQL Server 2022*', is basically connecting the the specific login by choosing 'SQL Server Authentication'.

In this case, the username `your_username` has administrator access to the database 'admin'.

3. Verify the Login Created

After connecting with the correct credentials by first running the command above $\uparrow$ 

```js
// switch to the 'admin' database
use admin

// find all the users that are present in that database
db.getUsers()
```

>[!SUCCESS]
>In my case, the output looks like this:
>
>```json
>{
>  users: [
>    {
>      \_id: 'admin.azmaan',
>      userId: UUID('81fa7b2b-466f-403d-99df-55a45318c885'),
>      user: 'azmaan',
>      db: 'admin',
>      roles: [
>        { role: 'userAdminAnyDatabase', db: 'admin' },
>        { role: 'readWriteAnyDatabase', db: 'admin' }
>      ],
>      mechanisms: [ 'SCRAM-SHA-1', 'SCRAM-SHA-256' ]
>    }
>  ],
>  ok: 1
>}
>```
>
>>[!WARNING] Obsidian is Goated, but...
>>Given that we have `_id` in the output, obsidian will treat that `_` character as the start of *italics*.
>>
>>Therefore, if I don't prefix the character `\` which is the escape character for Obsidian's markdown syntax. All of the things that I am writing will be in *italic* and I **hate** this.
>>
>>As from now, instead of having this `_id` in the output ( *in code blocks not inline-code blocks* ). I will instead write this $\rightarrow$ `\_id`.
>>
>>But again that does not mean that the output contains that `\` character!
>

>[!INFO] Starting `mongosh` **Without** Authenticating!!!
>Now, if you just run `mongosh` instead of running it with the *arguments* required. You know what; I don't even know what happens, so let's find about it together!
>
>```js
>// after running 'mongosh' in the terminal
>
>// switch to the 'admin' database
>use admin
>
>// check if we the admin-user we created is here
>db.getUsers()
>```
>
>Well, as you can see we get the error:
>
>```console
>MongoServerError[Unauthorized]: Command usersInfo requires authentication
>```

4. Enable Authentication inside `/etc/mongodb.conf`.

Open the file with your favourite text editor... "*I use VIM BTW*"!

```bash
# open the file 'mongodb.conf' with a text editor
sudo nvim /etc/mongodb.conf
```

Add the following lines to that file

```yaml
security:
  authorization: "enabled"
```

Then, **restart** the `mongodb.service` with `systemctl`:

```bash
# restart the mongodb server / service
systemctl restart mongodb.service
```

>[!SUCCESS] That Should Be It!!!
>If you have follow everything '*step-by-step*', I think you should be fine!

---

# MongoDB Compass

Now, I have said that I won't be using it... But that does **not** mean that we cannot learn and understand how it works, just for the fun of it!

Actually, the reason why I need to do this ( *like write about 'MongoDB Compass'* ) is because of a problem that I get. That problem is:

```console
Compass cannot access credential storage.
You can still connect, but please note that
passwords will not be saved.
```

>This really annoys me! Nothing major just annoying!

>[!INFO] Use MongoDB Compass :LiCheck:
>>*I am not saying that you SHOULD ONLY use `mongosh`*!!!
>
>If you want convenience, I suggest you to use MongoDB Compass as we have things like *syntax highlighting* , *auto-completion* and general use improvements.
>
>Hence, please go ahead and use it. But as my workflow consists of using and staying in the terminal for most things ( *and I use VIM BTW* ).
>
>For me personally, it does not really make a difference!

>Therefore, let's get started!

## Fixing The Issue

Initially, I could **not** find the answer to this problem. Therefore, I ask people in the 'technology' section in the [Mauritius](https://discord.gg/X22J73HQ) Discord Server!

Then one of the GOAT himself, 'jeyoung' gave me this link: https://stackoverflow.com/questions/78604024/mongodb-compass-connection-password-missing-when-using-i3-wm

>I think I did not search well enough!

### `.desktop` Files

Now, if you have ever used Windows ( *looking at you, 'normies'* ). Then you must have come across `.ink` files found on your Desktop. They are like **shortcuts** on Windows, but here, its much, much more powerful!

#### The Actual Fix

##### `gnome-keyring`

First up, just download and enable `gnome-keyring`.

```bash
# download and install gnome-keyring
sudo pacman -S gnome-keyring
```

Now, it should be enabled by default. But if its not... Just use `systemctl` command; run the following command if you see that `gnome-keyring` is not '*active*' or '*enabled*'

```bash
# enable gnome-keyring
systemctl --user enable gnome-keyring-daemon.service

# start the gnome-keyring for this session
systemctl --user start gnome-keyring-daemon.service
```

##### `mongodb-compass.desktop`

We are now going to try to find the file `mongodb-compass.desktop` in our system using the `find`:

```bash
find / -name "*mongodb*compass*.desktop" 2> /dev/null

# NOTE: if the first command does not get you any output
sudo find / -type f -name "mongodb*compass*.desktop" 2> /dev/null
```

>[!TIP]- Explanation of the Above Command!
>1. Start finding files in the `/` directory
>2. Pass the argument `-name` to search for a "*name*" pattern
>3. Specify the pattern we are actually searching for
>	- In this case we are searching for `mongodb-compass.desktop`
>	- Let's say that we don't know the *full* file name
>		- Therefore, we use the `*` operator which acts like our "*all in*"
>4. Pass `2` before redirecting the output to the black hole of Linux ( *i.e `/dev/null`* )
>	- `2` is going to suppress any error messages

In my case, we find out that its found at:

```console
/usr/share/applications/
```

##### Modify the `.desktop` File

Again, using your favourite text editor ( *I use VIM BTW* ). Change this:

```console
Exec=env mongodb-compass %U
```

- To this:

```console
Exec=env XDG_CURRENT_DESKTOP=GNOME mongodb-compass %U
```

>[!SUCCESS]
>Now, we should have no errors 

## Local Hosts

When we use [[Microsoft SQL Server 2022 Introduction|MS SQL Server 2022 - Management Studio]], upon starting the program, we are going to see this very window:

![[SQL Server 2022 - Connect to Server Screen.png | 400]]

As you can clearly ( *or not* ) see that our 'Server name' is as follows: `DESKTOP-ND74V2\SQLEXPRESS`!

>Then, how can we find out about the server name here? How can we find that `DESKTOP` thing?

## `mongodb.conf` and `hosts`

>Just bear with me for a second and run the following commands!

```bash
# find the word 'network' in the file mongodb.conf
# output that line with 'network' and 3 lines below it
grep -A 3 'network' /etc/mongodb.conf
```

>[!SUCCESS] Output For `mongodb.conf` File
>```console
>18:# network interfaces
>19-net:
>20-  port: 27017
>21-  bindIp: 127.0.0.1
>```
>
>>[!NOTE]
>>The reason as to why I have *line numbers*; it because I was using 'ripgrep' `rg`!

```bash
# output all of the contents for hosts
cat /etc/hosts
```

My `hosts` file looks like this:

```console
# Standard host addresses
127.0.0.1  localhost
::1        localhost ip6-localhost ip6-loopback
ff02::1    ip6-allnodes
ff02::2    ip6-allrouters
# This host address
127.0.1.1  Arch_PC
```

>Now your might be different!

### Hence

We can clearly see that our `localhost` is '127.0.0.1' and the the default port for that *local host* is '27017'.

#### Therefore, the Server URL...

Therefore, the server URL for `localhost` is going to be of this format:

```console
mongodb://<mongodb_username>@localhost:<port-number>/
```

In our case, ( *following the administrator username we created above* ), the URL is going to look like this:

```console
mongodb://your_username@localhost:27017/
```

The above $\uparrow$ URL should work perfectly fine... But let's go ahead and try something!

>The URL below should also work!

```console
mongodb://your_username@127.0.0.1:27017/
```

>[!TIP]
>This is possible as from the `mongosh` help page, we can see that we the following output after running the command:
>
>```bash
>mongosh --help | rg -A 5 'DB Address Examples:'
>```
>
>This should churn out this very output:
>
>```console
>DB Address Examples:
>
>	foo                                    Foo database on local machine
>	192.168.0.5/foo                        Foo database on 192.168.0.5 machine
>	192.168.0.5:9999/foo                   Foo database on 192.168.0.5 machine on port 9999
>	mongodb://192.168.0.5:9999/foo         Connection string URI can also be used
>```
>
>As you can see from the last line, this is clearly possible!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/channel/UCMkQZsuW6eHMhdUObLPSpwg
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!