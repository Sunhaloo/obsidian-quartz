---
id: Linux - File Permissions
aliases: File Permsissions For Different "Users" In Linux
tags:
  - C
  - linux
  - theory
author: S.Sunhaloo
date: 2025-09-21
status: Completed
---

## List of Contents

- [[#How To Read File Permission]]
	- [[#Breaking Down The Gibberish]]
- [[#Changing File Permission]]
	- [[#Change File Permission Directly In Shell!]]
		- [[#All People Have All Permissions]]
		- [[#Changing Permissions Using "Words"]]
	- [[#Special Permissions Access Control Bits]]
		- [[#Sticky Bits]]
		- [[#Set User ID ( SUID ) and Set Group ID ( SGID )]]
	- [[#Change File Permission Using C Programming Language]]
		- [[#Example Of Using Octal Numbers]]
		- [[#Example Of Using Macros]]

---

> [!INFO] Resource(s)
> - https://www.youtube.com/watch?v=LnKoncbQBsM

> [!TIP] Breaking Down Of Permission
> 1. Owner
> 2. Group
> 3. Others
>
> All of them has **three** types of *permissions*:
>
> - read `r`
> - write `w`
> - execute `x`

# How To Read File Permission

The following output after running the `ls -la` command ( *from the video* ):

```console
drwxrwxr-x 2 ubuntu ubuntu 4096 Oct 2 11:55 files
```

## Breaking Down The Gibberish

```console
drwxrwxr-x

# breaking it down / seperating them
d rwx rwx r-x
```

I am going to refer them as "*part 'x'*"... If I say something like "*part 1*"; this would mean `d` while "*part 4*" would mean `r-x`!

### Part 1 - Directory Or File?

```console
d
```

> This means that the *thing* is a **directory**!

```console
-
```

> This means that the *thing* is a **file**!

### Part 2 - Owner Permissions

```console
rwx
```

> In this case, the **owner** has *all* of the **3** permissions... That is, `read`, `write` and `execute`!

> [!TIP] The *First* `ubuntu`!
> The **first** `ubuntu` shows the *name* of the **owner**

### Part 3 - Group Permission

```console
rwx
```

> Here also, the **group** has the **same** permission as the owner! That is, `read`, `write` and `execute`!

> [!TIP] The *Second* `ubuntu`!
> The **second** `ubuntu` shows the *name* of the **group**

### Part 4 - All Users / Others

```console
r-w
```

> In this case, "_**other**_" users will only have these **2** permissions. That is, `read` and `write`

> [!INFO] Indication Of **No** Permission
> As you can see to indicate that a *someone* does **not** have a particular permission, we use the `-` symbol to represent it!

# Changing File Permission

## Change File Permission Directly In Shell!

Given the following `test.txt` file:

```console
-rw-rw-r--  1 owner group     0 Sep 21 12:05 test.txt
```

> [!WARNING] Using Google Cloud Console
> As I *alias* my `ls` to `ls='eza --no-user --no-time --no-permissions --icons=always'` and `-la` to `la='ls -lAh'`.
>
> Therefore if I create the `test.txt` file on my computer, I get this instead:
>
> ```console
> 0  test.txt
> ```
>
> Okay, I could also try to run `eza -la --icons=always` and this would return me something like this:
>
> ```console
> .rw-r--r--    0 owner 21 Sep 16:07  test.txt
> ```
>
> > [!INFO] The `.` **instead** of `-`!
> > Compared to the regular *linux* `ls -la` command... The *indication* of a **file** is different!
>
> > Therefore [Google Cloud Console](https://console.cloud.google.com)!
> 
> > [!NOTE] 16/02/2026
> > 
> > Reading this today ( *@ 9:52* ); I am such a dumb motherfucker! I could have just `unalias` the `ls` alias and simply use the *normal* `ls` command.
> > 
> > If that was not good enough... I could simply **switch** to the `bash` shell temporarily, and simply use it from there as I already have my `zsh` configured!
> > 
> > > Dumb Fuck!

```console
-rw-rw-r--
```

### Breaking It Down Again!

```
-rw- rw- r--
```

> **Binary Numbers**!!!

Each part is basically from $2^{0}$ to $2^{2}$. Therefore if we take a look at each *part*; we can see that we have something like this:

- Part 1: `rw-` = 6
- Part 2: `rw-` = 6
- Part 3: `r--` = 4

### All People Have All Permissions

To allow **everyone** to have **every** *permission*, we can use the `chmod` command like so:

```bash
# allow all "users" to have every permission
chmod 777 test.txt
```

Therefore, now we should see that the **file permission** has changed for this particular file:

```console
-rwxrwxrwx 1 owner group 0 Sep 21 12:05 test.txt
```

> [!SUCCESS]
> We have managed to **change** the file permissions!

---

### Changing Permissions Using "Words"

> Today is the 11/03/2026 @ 13:25!

So we have looked at how we can change file permissions using those **octal** numbers.

But do you expect Linux users ( *specially beginners* ) to use this?

> I **don't** think so!

Therefore, instead of using these octal numbers; we are going to be using *letters* and *symbols* instead!

> [!NOTE]
> I am going to be creating an empty `script.sh` file for demonstrating the process of changing the file permissions.
> 
> - This what the script file permissions looks like upon creation:
> 
> ```console
> -rw-r--r-- 1 owner group    0 Mar 11 13:28  script.sh
> ```

> [!WARNING]
> The reason as to why I am writing that right now is because of my Operating System module lab sheets!
> 
> The thing is that, I already understood the **octal** numbers *system*; but if I were you and using Linux as my daily drivers ( *which I have been doing for the past 6 years now* ).
> 
> I would instead prefer to use the following ( *see below* ) **instead** of the *octal numbers*.
> 
> > Therefore the following *notes* below till [[#Change File Permission Using C Programming Language]] are just for "*me*" sake!

#### Changing Permission For All

The easiest way to add execute permission for *everyone* (owner, group, and others):

```bash
# add executable permission to everyone
chmod +x script.sh
```

- After running this command, our `script.sh` file permissions now looks like this:

```console
-rwxr-xr-x 1 owner group 0 Mar 11 13:28 script.sh
```

- To add **all** permissions at once:

```bash
# add all permission to everyone
chmod a+rwx script.sh
```

- After running this command, our `script.sh` file permissions now looks like this:

```console
-rwxrwxrwx 1 owner group    0 Mar 11 13:28  script.sh
```

- Add **specific** permissions to *some* people:

```bash
# add specific permissions to specific people
chmod u=r,g=rw,o=x script.sh
```

- After running this command, our `script.sh` file permissions now looks like this:

```console
-r--rw---x 1 owner group    0 Mar 11 14:07  script.sh
```

- To **remove** all permissions from *everyone*:

```bash
# remove all permission from everyone
chmod a-rwx script.sh
```

- After running this command, our `script.sh` file permissions now looks like this:

```console
---------- 1 owner group    0 Mar 11 13:28  script.sh
```

#### Changing Permission For Owner / User Only

To **add** execute permission **only** for the *owner*:

```bash
# add executable permission to owner only
chmod u+x script.sh
```

- After running this command, our `script.sh` file permissions now looks like this:

```console
-rwxr--r-- 1 owner group    0 Mar 11 14:02  script.sh
```

- To **remove** write permission from the *owner*:

```bash
# remove write permission from owner
chmod u-w script.sh
```

- After running this command, our `script.sh` file permissions now looks like this:

```console
-r--r--r-- 1 owner group    0 Mar 11 14:03  script.sh
```

- To set **exactly** what permissions the *owner* should have:

```bash
# set no permissions for owner
chmod u= script.sh
```

- After running this command, our `script.sh` file permissions now looks like this:

```console
----r--r-- 1 owner group    0 Mar 11 14:06  script.sh
```

#### Changing Permission For Group Only

To **add** write permission **only** for the *group*:

```bash
# add write permission to group
chmod g+w script.sh
```

- After running this command, our `script.sh` file permissions now looks like this:

```console
-rw-rw-r-- 1 owner group    0 Mar 11 14:10  script.sh
```

- To **remove** read permission from the *group*:

```bash
# remove read permission from group
chmod g-r script.sh
```

- After running this command, our `script.sh` file permissions now looks like this:

```console
-rw----r-- 1 owner group    0 Mar 11 14:11  script.sh
```

- To set **exactly** what permissions the *group* should have:

```bash
# set exactly execute permission for group
chmod g=x script.sh
```

- After running this command, our `script.sh` file permissions now looks like this:

```console
-rw---xr-- 1 owner group    0 Mar 11 14:12  script.sh
```

#### Changing Permission For 'Others' Only

To **add** read permission **only** for *others*:

```bash
# add execute permission to others
chmod o+x script.sh
```

- After running this command, our `script.sh` file permissions now looks like this:

```console
-rw-r--r-x 1 owner group    0 Mar 11 14:13  script.sh
```

- To **remove** write permission from *others*:

```bash
# remove read permission from others
chmod o-r script.sh
```

- After running this command, our `script.sh` file permissions now looks like this:

```console
-rw-r----- 1 owner group    0 Mar 11 14:13  script.sh
```

- To **add** only write permissions to *other*:

```bash
# add only write permissions to others
chmod o=w script.sh
```

- After running this command, our `script.sh` file permissions now looks like this:

```console
-rw-r---w- 1 owner group    0 Mar 11 14:14  script.sh
```

## Special Permissions Access Control Bits

> This was also written on 11/03/2026 @ 14:39!

### Sticky Bits

> Restriction... Yes "*Restrictions*"!

Basically, we are going to be restricting the user to his / her own files.

For example, let's say that you have a user 'A' and a user 'B' whereby they *both* share the **same** *directory*.

Well, you could say if the A wants to mess with 'B', he / she could simply **delete** B's file.

Therefore, how can we stop other people from messing with someone else's stuff.

> Sticky Bits!

> [!WARNING]
> Sticky Bits are used to restrict *deletion* and *renaming* **only**!
> 
> Additionally, setting up sticky bits means that the:
> 
> - Root / `root` user will be able to delete / rename **everything**
> - The user who created the directory ( *i.e directory owner* ) will be able to delete / rename everything
> 
> > Nevertheless, users are able to *delete* / *rename* their **own** files but **not** for others!

#### How Setup Sticky Bits

##### Using Octal Numbers

- Create a directory with sticky bits applied:

```bash
# create a directory with "default" permissions
mkdir directory

# add sticky bit to directory so deletion is restricted to me
chmod 1755 directory/
```

> [!INFO]
> Now, if you ran an `ls -la` command just **after** you *created* the directory; you should see that the file permission was like so:
> 
> ```console
> drwxr-xr-x 1 owner group   0 Mar 15 21:16 directory
> ```
> 
> Now, if we run the same `ls -la` command again, we should see that it has **changed** to this:
> 
> ```console
> drwxr-xr-t 1 owner group   0 Mar 15 21:16 directory
> ```
> 
> > Very nice!

> [!NOTE] I think you get the point!
> 
> To add sticky bits using **octal numbers**, we simply need to add `1` in *front* when we are setting the file permissions ( *using octal numbers* ).
> 
> > Do I need to say something more!

##### Using "Words"

> I am basically going to be "*doing*" the same thing as above!

- Create a directory with sticky bits applied:

```bash
# create a directory with "default" permissions
mkdir directory

# add sticky bit to directory so deletion is restricted to me
chmod +t directory/
```

> Given that I needed the directory with *default* file permissions... Using `+t` was enough!

> [!WARNING]
> Applying sticky bits to a **regular** files ( *i.e `.txt`, `.py` or any other file* ) on a *modern* Linux system does absolutely **nothing**!
> 
> > The kernel simply **ignores** it!
>
> Sticky bits are only *meaningful* when applied to a **directory**. The directory is what gets the sticky bit, and that is what protects the files **inside** it from being *deleted* or *renamed* by others.

> [!INFO]
> Given that above, the table below shows who can delete **what** when a sticky bit is applied to a **directory**.
>
> | User Type | Can Delete? | Reason |
> | --------- | ----------- | ------ |
> | root | Yes | Always bypasses permission checks |
> | Directory Owner | Yes | Owns the directory |
> | File Owner | Yes | Owns the file |
> | Group Member | No | Sticky bit blocks this, regardless of directory write permission |
> | Others | No | Sticky bit blocks this, regardless of directory write permission |

### Set User ID ( SUID ) and Set Group ID ( SGID )

> Run **executable** files with the *permissions* of the **file owner** instead of the user that *launched* it!

Here, we are going to talk about how we can *escalate* the **privileges** of a file / directory. Let's say that you are a *normal* / *simple* user and he / she wants to do something that requires `root` privileges.

Let's take an example of a "*normal*" user trying to change his / her password; therefore the user simply needs to run the `passwd` command and enter the **current** and **new** password.

> Simple as that!

But the actual file that the **new** password you just added to; where do it go? Given that we do know that in Linux, everything is a *file*.

All the **passwords** goes into the `/etc/shadow` file... But that file is **only** own `root` user. So how come we, a simpleton user was able to change the password?

> [!TIP] The Irony...
> 
> **Not** to be confused with `/etc/passwd` which just keep a *general* information about users!
> 
> > The irony of `passwd` file simply storing "*general*" information instead of actual ( *encrypted* ) passwords!

> [!INFO]
> What I am trying to say is that; instead of the **administrator** of *that* machine going into the `root` user ( *maybe with something like `sudo su`* ).
> 
> And then to change that **specific** user's `user` password, he would then run something like: `passwd user`.
> 
> Therefore, what I was saying its that... *How come that "simple" user is able to change his / her password*?

The *answer* to the above question is simply because we ( *Linux* ) have set a '*SUID*' on that `passwd` binary!

So if you go ahead and run the following command below:

```bash
ls -la /usr/bin/passwd
```

- You should see that we have an `s` character for the **owner**:

```console
-rwsr-xr-x 1 root root 84952 Jun 28  2025 /usr/bin/passwd
```

> That is why a "*simple*" user is able change his / her password **without** being the `root` user!

#### Set User ID ( SUID )

##### Using Octal Numbers

- Create an **excecutable** `script.sh` and then apply 'SUID' to that file:

```bash
# create script file
touch script.sh

# make the script file executable ( for the owner only )
# NOTE: additionally, add 'SUID' to the file
chmod 4755 script.sh
```

> [!INFO]
> Now, if you ran an `ls -la` command just **after** you *created* the script file; you should see that the file permission was like so:
> 
> ```console
> -rw-r--r-- 1 owner group   0 Mar 16 21:10 script.sh
> ```
> 
> Now, if we run the same `ls -la` command again, we should see that it has **changed** to this:
> 
> ```console
> -rwsr-xr-x 1 owner group   0 Mar 16 21:10 script.sh
> ```
> 
> > Very nice!

##### Using "Words"

> Basically repeating the same thing that was done above...

- Create an **excecutable** `script.sh` and then apply 'SUID' to that file:

```bash
# create script file
touch script.sh

# make the script file executable ( for the owner only )
# NOTE: additionally, add 'SUID' to the file
chmod +s script.sh
```

> [!WARNING] Wait a second!
> 
> > Its different!
> 
> If I run the `ls -la` command after applying the `+s` ( *using `+s` as its the same thing as `u+s`* ), I see that we get something "*different*":
> 
> ```console
> -rwSr--r-- 1 owner group   0 Mar 16 21:15 script.sh
> ```
> 
> Its now `-rwSr--r--` compared to using `4755` / *octal numbers* which gives us `-rwsr-xr-x` instead!

> [!BUG]
> Using *symbolic* ( *what I have been saying "words"* ) is **different** compared to simply our *octal numbers*!
> 
> Using the `chmod +s filename.sh` command will **only** set the '*SUID*' and it will **not** set the `x` / executable!
> 
> > [!TIP] The Fix ( *In Our Case* )
> > 
> > Given that we want to to make `script.sh` actually executable, we are going to instead use `+sx` like so:
> > 
> > ```bash
> > # add 'SUID' and actually make the script executable
> > # NOTE: similarly to above... apply excutable flag to owner only!
> > chmod +sx script.sh
> > ```
> > 
> > Therefore, if we now run a little `ls -la` command, we should get the **same** thing that we did for `4755`:
> > 
> > ```console
> > -rwsr-sr-x 1 owner group   0 Mar 16 21:20 script.sh
> > ```
> 
> > [!WARNING]
> > Its still **different** whereby the *group* also has the `s` applied to it!
> > 
> > Therefore, if you really want it to be `755`; then you are going to have to **manually** setup it up for the "*others*".

> [!TIP]
> Applying 'SUID' to *directories* has **no** effect and the kernel simply **ignores** it!

#### Set Group ID ( SGID )

This is the **same** thing as above but here we are going to apply it to *directories*! As you know, similar to [[#Sticky Bits]]; when you are going to apply it to a **directory** all the *files* **inside** are going to *inherit* the "*file permissions*" of that directory.

> Meaning that they are going to have *group*'s **ownership** applied to them ( *the files and folders inside* )!

> [!NOTE]
> See how I only said: "but here we are going to apply it to directories".
> 
> This is because 'SGID' **also** works on **executable** files. And we apply 'SGID' to a *file*; we are going to run that file with the *group*'s thingy.
> 
> But in modern times, 'SGID' is mostly applied to **directories**!
> 
> > Nevertheless, there are files that we have / need to apply 'SGID' in some systems.

##### Using Octal Numbers

- Create a `shared` directory and apply 'SGID' to that directory:

```bash
# create a directory
mkdir shared

# add SGID to directory
chmod 2755 shared/
```

> [!INFO]
> Now, if you ran an `ls -la` command just **after** you *created* the directory; you should see that the file permission was like so:
> 
> ```console
> drwxr-xr-x 1 owner group   0 Mar 16 21:54 shared
> ```
> 
> Now, if we run the same `ls -la` command again, we should see that it has **changed** to this:
> 
> ```console
> drwxr-sr-x 1 owner group   0 Mar 16 21:54 shared
> ```
> 
> Its correct as we have `s` in the *group*'s file permissions!
> 
> > Very nice!

##### Using "Words"

> Basically repeating the same thing that was done above...

- Create a `shared` directory and apply 'SGID' to that directory:

```bash
# create a directory
mkdir shared

# add SGID to directory
# NOTE: that here we need to specify that we are applying to 'group'
# else its going to default to 'owner'
chmod g+s shared/
```

> [!SUCCESS]
> We have finally completed this section about **Sticky Bits** and **Special File Permissions**!

---

## Change File Permission Using C Programming Language

When doing my '[[OS - Labsheet 4 ( L2S1 )]]' whereby we need to use **system calls** like `open` and others. We needed to understand **file permission**.

Therefore there are 2 possible ways of *setting* our "*created*" file's permission!

- Directly setting the file permission using **octal numbers**
- Use *macros* already defined in `<sys/stat.h> `

### Example Of Using Octal Numbers

Let's write a simple C code that is going to create the `test.txt` file whereby the:

- **Owner** will be able to `read`, `write`
- **Group** will be able to `read` **only**
- _**Others**_ will be able to `read` **only**

Therefore, we know that we need to use the *number* `644` if we were, for example, using the `chmod` command.

> Translating the `644` number... *Just add a '0' at the front*!

```c
// to be able to use the wrapper system call function `open`
#include <fcntl.h>
// to be able to use the wrapper system call function `close`
#include <unistd.h>

int main() {
  // create the `test.txt` file
  int file_descriptor = open("test.txt", O_CREAT, 0644);

  // close the file to free up memory
  close(file_descriptor);

  return 0;
}
```

> [!SUCCESS]
> After running and compiling this code, we can see that the `test.txt` file has the *proper* permission that we wanted!
>
> ```console
> .rw-r--r--    0 username 21 Sep 16:34  test.txt
> ```
>
> > Yes I am using `eza` here!
>

### Example Of Using Macros

Now the `<sys/stat.h> ` *header file* basically gives us **macros** that simply *represents* these **octal** numbers!

Let's say that we want to do the same thing by as above, whereby the **owner** has `read` and `write`, **group** and **others** both having `read` only.

```c
// to be able to use the wrapper system call function `open`
#include <fcntl.h>
// to be able to use the wrapper system call function `close`
#include <unistd.h>
// to be able to use the proper macros for file permissions
#include <sys/stat.h>

int main() {
  // create the `test.txt` file
  int file_descriptor =
      open("test.txt", O_CREAT, S_IRUSR | S_IWUSR | S_IRGRP | S_IROTH);

  // close the file to free up memory
  close(file_descriptor);

  return 0;
}
```

> [!SUCCESS]
> We **do** get the *proper* file permission that we wanted to set:
>
> ```console
> .rw-r--r--    0 owner 21 Sep 16:34  test.txt
> ```
>
> > Again, using `eza -la --icons=always`!
>

#### The `touch` Command

- Try creating the `test.txt` file using the `touch` command:

```bash
# create the 'test.txt' file using the `touch` command
touch test.txt
```

- Running my little `eza` command, we get this:

```console
.rw-r--r--    0 owner 21 Sep 17:59  test.txt
```

> Basically the same thing:

#### Therefore,

> The **tables** below were created by [claude](https://claude.ai)! *Seems Good*!

##### Common Permission Combinations

| Octal | Symbolic | Description |
|-------|----------|-------------|
| 0755 | rwxr-xr-x | Executable files (owner: rwx, group/other: rx) |
| 0644 | rw-r--r-- | Regular files (owner: rw, group/other: r) |
| 0600 | rw------- | Private files (owner: rw, group/other: none) |
| 0777 | rwxrwxrwx | Full permissions for all |
| 0666 | rw-rw-rw- | Read/write for all (no execute) |

##### Individual Permission Bits

| Macro | Octal | Description |
|-------|-------|-------------|
| `S_IRUSR` | 0400 | User (owner) read permission |
| `S_IWUSR` | 0200 | User (owner) write permission |
| `S_IXUSR` | 0100 | User (owner) execute permission |
| `S_IRGRP` | 0040 | Group read permission |
| `S_IWGRP` | 0020 | Group write permission |
| `S_IXGRP` | 0010 | Group execute permission |
| `S_IROTH` | 0004 | Other read permission |
| `S_IWOTH` | 0002 | Other write permission |
| `S_IXOTH` | 0001 | Other execute permission |

##### Combined Permission Macros

| Macro | Octal | Description |
|-------|-------|-------------|
| `S_IRWXU` | 0700 | User (owner) read, write, and execute |
| `S_IRWXG` | 0070 | Group read, write, and execute |
| `S_IRWXO` | 0007 | Other read, write, and execute |

##### Special Permission Bits

| Macro | Octal | Description |
|-------|-------|-------------|
| `S_ISUID` | 04000 | Set user ID on execution |
| `S_ISGID` | 02000 | Set group ID on execution |
| `S_ISVTX` | 01000 | Sticky bit (restricted deletion) |

##### File Type Macros

| Macro | Octal | Description |
|-------|-------|-------------|
| `S_IFMT` | 0170000 | Bit mask for file type |
| `S_IFREG` | 0100000 | Regular file |
| `S_IFDIR` | 0040000 | Directory |
| `S_IFCHR` | 0020000 | Character special file |
| `S_IFBLK` | 0060000 | Block special file |
| `S_IFIFO` | 0010000 | FIFO (named pipe) |
| `S_IFLNK` | 0120000 | Symbolic link |
| `S_IFSOCK` | 0140000 | Socket |

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!