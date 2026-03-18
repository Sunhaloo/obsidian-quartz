---
id: Git - Getting Started
aliases: Getting Started and Setup with Git
tags:
  - GitHub
  - bootdev
  - git
  - linux
author: S.Sunhaloo
date: 2025-06-23
status: Completed
---

## List of Contents

- [[#Git, Directories and General Setup]]
	- [[#My Learning Setup]]
	- [[#Reading The Friendly Manual]]
- [[#Git Configuration]]
- [[#Git Commands]]

---

> [!INFO]
> I have expected you to read the short introduction that I wrote for `git` in the note / file '[[Git - Introduction]]'
>
> Therefore, I am thinking that you should already have your setup; meaning that you have **downloaded** `git` and also have all the tools that you require to work... Code / Text Editor and others.

# Git, Directories and General Setup

## My Learning Setup

```console
├──  Git_Learning
│   └──  git_dir
```

The folder that will contain my *main* `.git` hidden folder is going to be `git_dir`.

> I created the directory above $\uparrow$ inside the `Desktop` folder.

## Reading The Friendly Manual

As people **cannot** remember everything all at once... People therefore create *Manuals* or, what we programmer call "**Documentation**".

To read the *Friendly Manual* simply run the following command below:

```bash
# open the manual pages for git
man git
```

> [!WARNING] Windows Users
> In Powershell, the `man` command is just an **alias** to the `help` or `HELP` command. And we all know that its **definitely not** the same as our `man` command from Linux / Unix based machines.
>
> Therefore, to *emulate* the manual pages for `git` on Windows; simply run the following to get the **same** *output*.
>
> ```powershell
> # another way of opening manual pages for git
> git help git
> ```

### Further Help

Now simply running the command `git`, we know that we are going to get an output that looks something like this $\downarrow$:

```console
usage: git [-v | --version] [-h | --help] [-C <path> ] [-c <name> =<value> ]
           [--exec-path[=<path> ]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--no-lazy-fetch]
           [--no-optional-locks] [--no-advice] [--bare] [--git-dir=<path> ]
           [--work-tree=<path> ] [--namespace=<name> ] [--config-env=<name> =<envvar> ]
           <command> [<args> ]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone      Clone a repository into a new directory
   init       Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add        Add file contents to the index
   mv         Move or rename a file, a directory, or a symlink
   restore    Restore working tree files
   rm         Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect     Use binary search to find the commit that introduced a bug
   diff       Show changes between commits, commit and working tree, etc
   grep       Print lines matching a pattern
   log        Show commit logs
   show       Show various types of objects
   status     Show the working tree status

grow, mark and tweak your common history
   backfill   Download missing objects in a partial clone
   branch     List, create, or delete branches
   commit     Record changes to the repository
   merge      Join two or more development histories together
   rebase     Reapply commits on top of another base tip
   reset      Reset current HEAD to the specified state
   switch     Switch branches
   tag        Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch      Download objects and refs from another repository
   pull       Fetch from and integrate with another repository or a local branch
   push       Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command> ' or 'git help <concept> '
to read about a specific subcommand or concept.
See 'git help git' for an overview of the system.
```

Reading the last *paragraph* tells you that we can learn / refer to the *manual pages* for specific commands.

Therefore, we can do something like this:

```bash
# help guides for specific commands

# help page for the `merge` command
git help merge

# help page for the `diff` command
git help diff

# help page for the `fetch` command
git help fetch
```

> [!NOTE] Windows Users
>
> > Hahh... Hahh... Hahh
>
> When you run these command above... Its going to **open** up your *browser* like a fucking peasant and then send you straight to the **online documentation** for that *sub-command* because why fucking not Micro fucking Soft!

# Git Configuration

Before, we start using our lovely `git`... We first need to **configure** some things. This is done using the `config` *sub-command*.

Let us first go ahead and see what our current configuration looks like.

Run the following command to see how our current configuration looks like:

```bash
# see all you git configurations
git config list

# you can also run the following commands
git config --list
```

> [!TIP] Newer Version of Git!
> I am currently using the version `2.49.0`.
>
> Back when I was learning `git` ( *meaning before `2.44`* ), we <span style="color: red;"> needed</span> to use the **second** command as shown above!
>
> But now, we don't need to! Its even inside the manual pages.
>
> > Go and take a look at `git help config` and see for yourself!
>

Depending on your platform / Operating System, you might see that it **completely empty** or does contain some information.

> [!WARNING] Learn the Older Commands ( *For The Moment* )!
> The format is going to be like this as from now.
>
> Inside the **code block**; I will first show you the *new* commands and below it you are going to get the *older* / **deprecated** equivalent of that command / function!
>
> > I will tell you the reason later on!
>
> Additionally, the new command opens the **output** with `less` and I don't really like opening things with `less` where you only have a *one liner* output.
>
> > Does **not** make any sense at all in my opinion
>

## Checking and Setting Up User

Now, if this is your first time ( *[that's what she said](https://www.youtube.com/watch?v=dBUGfs9rwms)* ) then you are not going to have any **username** or **email** or any other configuration for that matter, setup.

> Nevertheless, let's go ahead and run the following commands to verify ourselves.

### Checking User

```bash
# new command - verify username
git config get user.name

# deprecated equivalent - verify username
git config user.name


# new command - verify email
git config get user.email

# deprecated equivalent - verify email
git config user.email
```

> Or we could have simply run the `git config list` command!

### Setting Up the User

If this is your first time working with `git`. Therefore, `git` currently does not *know* you and we set it up!

#### Creation of GitHub Account

> [!NOTE] Again and Again!
> [GitHub](https://github.com) is <strong> <span style="color: red;"> not</span> </strong> `git`.
>
> > We have already covered this in the '[[Git - Introduction#Confusion, Confusion and Confusion! | Git - Introduction]]' file / note!
>

I think if you know how to create a motherfucking, fucking shitty ass, TikTok account. I think you should be able to create a simple little GitHub Account.

> Additionally, there is always Search Engines / AI if you need any help!

#### Back to `git`

Now that you have created you GitHub account with your email and provided a new username.

We are going to be using these data to tell `git` that you are who you are.

> [!WARNING]
> We have not yet connected or even touched **remote** repositories!!!

##### Setup `git`

Please use the code block found below $\downarrow$ as a guide to help you setup your username, email and other settings.

> I will also be writing the old commands together with it!

```bash
# new command - setup username
git config set --global user.name "github_username"

# deprecated equivalent - setup username
git config --global user.name "github_username"

# new command - setup email
git config set --global user.email "github_email"

# deprecated equivalent - setup email
git config --global user.email "github_email"

# new command - change default branch
git config set --global init.defaultBranch main

# deprecated equivalent - change default branch
git config --global init.defaultBranch main

# new command - setup code editor
# NOTE: if you use VS C*de / Sumblime Text, you need to add the `--wait`
# so that git will stop doing / running other commands
# until you close the editor, i.e
git config set --global core.editor "code --wait"

# INFO: I use VIM BTW!!!
# WARNING: choose only one!
git config set --global core.editor "nvim"

# deprecated equivalent - setup code editor
git config --global core.editor "code-- wait"
```

### The Configuration File

Now, `git` does not *magically* absorbs these "*setup commands*" by itself.

Almost, all systems have a configuration files! These configuration files could be stored **locally** or **remotely**; for the case of *some* games.

Git also comes with this **configuration file** and that file is called the `.gitconfig` config file.

> English is **not** my first language!

This configuration file is normally found in our **home directory**.

> [!INFO]
> Again, if this is your first time... Then the configuration file is probably stored inside the home directory $\Rightarrow$ `~/.gitconfig`!

> But let's try to find it!

```bash
# try to find the `.gitconfig` command
# which is supposed to be inside the home directory
find / -type f -iname ".gitconfig" 2> /dev/null
```

The above $\uparrow$ command is basically saying something like this:

- start searching inside the root directory $\rightarrow$ `/`
- only search of the *type of file* "**file**"
- find the file with the **exact** name of `.gitconfig`
	- whereby `-iname` is *case-sensitive*
- suppress any errors found by redirecting `stderr` to the Linux *black hole*

Therefore, in my case, I get the following output:

```console
/home/username/.gitconfig
/home/username/.vscode/extensions/miguelsolorio.symbols-0.0.24/file-types/.gitconfig
```

> [!WARNING] Windows People... :)
> Sooooooo... Do we even have a `find` command on Windows???

#### Contents of `.gitconfig`

The current contents of my `.gitconfig` file is as follows:

```bash
# run the command to display the contents of file
cat ~/.gitconfig
```

- Contents of my `.gitconfig` configuration file

```console
[user]
	email = username@email.com
	name = username
[init]
	defaultBranch = main
```

# Git Commands

So, `git` commands are divided into **two** categories. They are the:

1. Porcelain Commands
2. Plumbing Commands

The command that 99% of developers use is going to be the **Porcelain** commands. These are "*basics*" things like:

- `git status`
- `git push`
- `git pull`
- `git log`

While the rarer used commands are going to be called **Plumbing** commands

> Because they allow you to fix the massive leakage that you have caused :)
>
> "*Car trace jaune fanner partout*!"

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!