---
id: Bash Language Basics
aliases: The Bourne Again Shell
tags:
  - bash
  - script
author: S.Sunhaloo
date: 2025-06-27
status: Completed
---

## List of Contents

- [[#How To Run Scripts?]]
- [[#The Shebang]]
- [[#Getting Started with BASH!]]
	- [[#Basic Data Types]]
- [[#Displaying Variables]]
	- [[#The `echo` Command]]
	- [[#The `printf` Command]]
- [[#User Inputs]]
- [[#Conditions]]
- [[#Loops]]
- [[#Positional Arguments]]
- [[#Functions]]

---

> [!WARNING]
> > This is going to be different!
>
> So, the actual reason that I am learning Bash it to make my `install.sh` script ( *for Linux* ) **better** and **simpler**!
>
> Therefore, instead of going to into the "*in's and out's*" of learning this language. I am going to apply the technique of:
>
> - See others and implement
> - Learn as I go and learn only what I need
> - Actually have fun and **fail** a lot
>
> What I am trying to say its that, this file / note is going to be really simple!

> Even if in my second year of University I am going to be learning about it!

# How To Run Scripts?

To be able to run a `.sh` script file; we are going to have to use the `chmod` command!

> [!TIP] Read The Friendly Manual
> I suggest that you do take a look at the *manual* ( *or man-pages* ) and other resources found online as I will **not** be explaining everything here.
>
> > This is due to the fact that I don't even really know the *in-and-outs* of the `chmod` command!
>

The primary usage ( *from what I have seen* ) of the `chmod` command is going to be *changing* the **permission** of the some files in your system, and if needed, allow other users to access these files.

```console
total 32
drwxr-xr-x  4 owner group 4096 Jul  3 11:40 .
drwx------ 38 owner group 4096 Jul  3 11:40 ..
drwxr-xr-x  4 owner group 4096 May 25 17:38 Algorithms
drwxr-xr-x  4 owner group 4096 Jun 26 21:25 learning_git
-rwxr-xr-x  1 owner group   24 Jul  3 11:40 main.sh
-rw-r--r--  1 owner group  888 Apr 19 14:22 mongodb_links.txt
-rw-r--r--  1 owner group 2821 May 24 22:11 test.c
-rw-r--r--  1 owner group 2276 Jun 25 17:45 user.json
```

The above $\uparrow$ output is my running the `ls -la` command inside my `~/Desktop` directory.

As you can clearly see, we get a lot of *information* about the **folders** and **files** that we created!

> But, [What are Thoooooseeee?](https://www.youtube.com/watch?v=HNtz05bhI1k) Things

```console
drwxr-xr-x
drwx------
drwxr-xr-x
drwxr-xr-x
-rwxr-xr-x
-rw-r--r--
-rw-r--r--
-rw-r--r--
```

There are the permission that an **owner**, **group** or **_other_** and each one of them can have the following permission:

1. Read
2. Write
3. Execute

If you take for example our `Algorithms` folders / directory we can break it down:

```console
d rwx r-x r-x  4 owner group 4096 May 25 17:38 Algorithms
```

> Let's go ahead and break down this thing!

- `d`: Meaning that the *thing* is a directory
- `rwx`: Referring to the **owner** and has permissions ( *in this case* )
	- read
	- write
	- execute
- `r-x`: Referring to the **group** and has permissions ( *in this case* )
	- read
	- execute
- `r-x`: Referring to the "**all users**" and has permissions ( *in this case* )
	- read
	- execute

> [!NOTE]
> Again, I am **not** going to be going over this as I actually want to go and write my *fucking* install script!

## Executing A `.sh` File

Copy the contents inside the code block below and then save it as `main.sh`

> *I use VIM BTW*

```bash
#!/bin/env bash

echo "Hello Motherfucker!"
```

To allow **everyone** to be able to execute the file, we are going to make it *executable* with the `chmod` command like so:

```bash
# make the file 'executable' for everyone
chmod +x main.sh
```

> [!SUCCESS]
> You can now go into your BASH ( *in my case, ZSH* ) shell and run the `main.sh` file like so $\downarrow$:
>
> ```bash
> # execute the script
> ./main.sh
> ```

> [!INFO]
> I suggest you go ahead and watch the following YouTube video; the link is just below:
>
> - https://www.youtube.com/watch?v=LnKoncbQBsM
>
> > You are going to get more of an idea of how it works!
>

---

# The Shebang

Now, scripts can be written in other languages also; one of these *other* languages is going to be [[Python Language Basics | Python]].

Here is practical example of where Python is used to make very nice *install* script: https://github.com/archlinux/archinstall

Therefore, there needs to be a way to make Linux ( *most if not any distribution* ) that we using the **Bourne Again Shell**
( *i.e BASH* ).

This is where the "**shebang**" comes it. This is the first line in the `.sh` file where it tell Linux what *language* that we are used to write our script!

## The Environment!

To specify the *language* that we are using for our script. We normally write something like this at the top of the file like so $\downarrow$:

```bash
#!/bin/bash
```

In this case, we are saying that we are going to be using *BASH* for this script.

> [!WARNING] It <strong> <span style="color: red;"> Needs</span> </strong> To Be The **First** Thing!
> Yes! the *shebang* needs to be on line number '1'. You cannot even have a *comment* above it.
>
> After specifying the *shebang* then you are going to be able to do whatever you want to do!

> I think you get the point!

Meaning that if you want to use another language for scripting; we could simply change `bash` to `that_language_name` like so:

```bash
#!/bin/python3
```

### `#!/bin/env language_name`

But what if its **not** your computer or you have different users?

As you know inside the `/bin` directory; we have packages that are *system-wide* **core packages** like `ls` and others.

If you are your own administrator user of your computer meaning that your user has access to `sudo`. The system-wide packages are going to be installed inside the `/usr/bin` directory.

But in my case, they also get installed inside of `/bin` directory; nevertheless, when I run, for example `which nvim`, I get the following output:

```console
/usr/bin/nvim
```

> Well... I don't know! Moving On!!!

Now, if your user does **not** even have access to the `sudo`
command then the packages should be installed inside of the `~/.local/share/` directory.

> This is where the `#/bin/env language_name` comes into play!

Because BASH is / *should be* installed on most, if not all Linux Systems / distribution; the `env` thing will go ahead and try to find if for us!

Now, this is going to add some **unnoticeable** *delay* to our script as it will first have to go and find where the *program* ( *meaning our language* ) is.

If it does <span style="color: red;"> not</span> see that *language*. It is going to scream something like this $\downarrow$:

```console
env: ‘joe_mama’: No such file or directory
```

> In this case, I tried to use the *programming language* `joe_mama`!

> [!TIP] Therefore!
> I will always be now using the `#!/bin/env bash` instead of specifying directly where our "*file*" / "*directory*".
>
> > I will also suggest you do to the same thing!
>

# Getting Started with BASH!

## Basic Data Types

```bash
# this is a single line comment

# bash does not really have multi-line comments
# but we can do something like this

: << "EOF"

this is the 'heredoc' type of comments
but again, BASH does not really have multi-line comments
this means that we can replace ':' the 'null' operator to
something like `echo` or others!

EOF

# back to single line comments
# just stick to single line comments for fuck sake
```

> [!NOTE]
> <p align="center"> <strong> Everything</strong> is a <strong> String</strong> until <strong> Evaluated</strong> !</p>
>
> BASH does **not** even *floating point numbers*!
>
> This is because its not really designed for heavy computation / calculation.
>
> Bash was designed to primarily work with files / directories first thereby keeping the number of data types to a minimal means that the user does **not** need to remember many things and can quickly proceed to do its things.
>
> > That is so true, as I do sometimes ( *rarely, but I did do it* ) will create a script just to move files and folders into specific directories!
>
> If you want to perform specific calculations with floating point numbers you are going to have to use another *scripting type* language called '[awk](https://en.wikipedia.org/wiki/AWK)'
>
> > We are also going to be learning this in second year of university!
>

> [!INFO] Regular Strings V/S Literal Strings
> *Regular Strings* are what you ( *might* ) already know and pretty much is used to represent **strings** in most ( *if not all* ) modern programming languages!
>
> But what about *Literal Strings*?
>
> Well as the name suggests. Its "*literally*" going to display what is inside **exactly as it is**!
>
> For example if we write something like:
>
> ```bash
> echo "Hello $name!!!"
> ```
>
> This will output the things that we already know. But if we instead use literal strings like so:
>
> ```bash
> echo 'Hello $name!!!'
> ```
>
> This is *literally* going to output `Hello $name!!!`
>
> > Therefore, you need to be careful with the character `'` and `"`!
>

### Integers, Characters and Strings

```bash
# initialisation of variables
num=69

# NOTE: can just create and `echo` it
# nevertheless, we are going to need `awk` or `bc` to compute
floating_num=6.9

character_thingy="A"
some_text="Some Text Here"
```

## Displaying Variables

There are two *main* ways to **display** *variables* onto the screen. In BASH, we can use the `echo` and `printf` command to display our *stuff* onto the screen!

### The `echo` Command

I think we all have, at some point in our life, run the following code found below $\downarrow$:

```bash
# "hello the fucking world"
echo "Sup Dickheads!"
```

- This should output the following in our BASH shell:

```console
Sup Dickheads!
```

#### Displaying Variables Using the `echo` Command

We are now going to display all the **variables** that we initialised above $\uparrow$:

```bash
# displaying integer number
echo "$num"

# displaying decimal / floating point number
echo "$floating_num"

# displaying characters
echo "$character_thingy"

# displaying strings
echo "$some_text"
```

- Running the above `echo` commands; we should therefore see something like this:

```console
69
6.9
A
Some Text Here
```

You see, to display a variable in BASH; we need to first **prefix** the *actual variable* with the `$` symbol. And then after that, we need to surround that resulting text with `"`.

This means that our final *text* should look similar to this $\rightarrow$ `"$variable_name"`!

### The `printf` Command

> People who program in [[C Language Basics | C]] should feel at home!

BASH does support the `printf` **command**! Yes, its a *command* because we just do `printf` and **not** `printf()`!

> Additionally, we can see it inside the `/bin` / `/usr/bin/` directory!

```bash
# find the `printf` command inside the system-wide coreutils directory
ls /bin | grep "printf"
```

But in terms of functionality of like using things like `%s`, `%d`, etc. Its basically the same thing!

> They are [same, same but different](https://www.youtube.com/watch?v=7tTfL-DtpXk)!

Now, if you have used the 'C' programming language. Then you know that we don't get things like automatic "*place cursor on the fucking next line or whatever its fucking called*" *thing*!

This is the reason why I said that people who program in C are going to be at ease as they have already been doing that.

> I suggest you to go take a look at some documentation / tutorials for `printf`!

Emulating the same thing that we did with our `echo` command above, we should therefore have the following code:

```bash
# displaying integer number
printf "%d\n" "$num"

# displaying decimal / floating point number
printf "%0.1f\n" "$floating_num"

# displaying characters
printf "%c\n" "$character_thingy"

# displaying strings
printf "%s\n" "$some_text"
```

- We should therefore have the same output as output like we did above!

```console
69
6.9
A
Some Text Here
```

> As you can see, we have the **same** output like we did we the above command!

> [!WARNING] What should we use?
> I am going to be using the `printf` command as we are going to have more control!
>
> I mean, you could use the `echo` command... But again, if you have ever *program* in C; then this should be no problem for you as you should already be familiar with the way that the `printf` function works!
>
> > Hence, `printf` it is!
>

# User Inputs

Now, if you want to make *safe* scripts and write actual usable scripts... I think that you **need** to spice things up by allowing the user to enter *data* / *select options*!

> What else can I say? *Go Fuck Yourself*?

The main thing that we are going to learn here is the `read` command whereby we are going to be able to **read** the user's input and do some *computation* or *logical* operation with it

Below you are going to find the simplest way to allow the user to enter data.

> I really mean it... Just *entering* some data and do **nothing** with it!

```bash
# simply use the `read` command
read
```

Now, if you simply run the `read` command in you BASH shell. You are going to find that it just keeps waiting.

This actually means that you can enter *something* and as soon as you press the <button style="border-radius: 10px; background-color: transparent;"> Return</button> key. It will return you to the *normal* shell like nothing ever happened before.

> [!TIP] The Template!
> The actual way to use the `read` command is going to be like this:
>
> ```bash
> read variable_name
> ```

This means that we should be able to do something like this $\downarrow$:

```bash
#!/bin/env bash

# ask the user to enter his name
echo -n "Please Enter Your Name: "

# use the `read` command --> add user input to variable `name`
read name

# display the name
printf "\nHello My Friend, %s!\n" "$name"
```

The above $\uparrow$ program simply means that:

- Use the `echo` to display / prompt the user to enter his name
	- the `-n` *flag* simply means that the cursor / caret will **not** be on the next line
- `read` that user's input and place that data into the variable `name`
- Finally, display a little message

> What if I told you that we can simplify that code into to lines or even one line?

This is the better and cleaner version of the above code.

> I am also going to add the *one line* version that should **not** be used inside the same code block

```bash
#!/bin/env bash

# ask the user to enter his name with the `read` command itself
read -p "Please Enter Your Name: " name

# display the name
printf "\nHello My Friend, %s!\n" "$name"

# display a blank line
echo

# WARNING: one-liner version of... NOT Recommended To DO THIS!!!
# this is only for 'show'
read -p "Please Enter Your Name: " name && printf "\nHello My Friend, %s!\n" "$name"
```

- This should output something that looks like this $\downarrow$:

> In this case the `name` that I entered was '*Joe Mama*'

```console
Please Enter Your Name: Joe Mama

Hello My Friend, Joe Mama!

Please Enter Your Name: Joe Mama

Hello My Friend, Joe Mama!
```

> [!TIP] The `;` and `&&` operators!
> > I know how to use them but I did **not** really know the difference between them... *But now I know*!
>
> Both of these operators allows you to *chain* commands together like so:
>
> ```bash
> # force refresh pacman's packages and then update
> sudo pacman -Syy && sudo pacman -Syu
>
> # again, force refresh pacman's packages and then update
> sudo pacman -Syy; sudo pacman -Syu
> ```
>
> Now both will refresh the packages and then update the system. Nevertheless, there is a *massive* difference ( *That's what she said* ); the `&&` operator will continue to run the other command(s) **if and only if** the first command return the exit code / status of '0'.
>
> > Meaning that the first command did run **successfully**!
>
> While our `;` operator will continue to *chug along* even if the first command returned the exit code / status '1'!

# Conditions

To execute something based on some **conditions** in BASH, we have *mighty* `if` statement and also the `case` statement!

> So its really similar to [[Python Language Basics#Conditions | Python]] in that way!

## `if` Statements

```bash
#!/bin/env bash

# ask the user to enter his age
read -p "Please Enter Your Age: " user_age

if [[ "$user_age" -le 0 ]]; then
    # output appropriate message
    echo "Error!"

# check if the user's age is between 18 and 100 ( inclusive )
elif [[ "$user_age" -ge 18 && "$user_age" -le 100 ]]; then
    # output appropriate message
    # INFO: using `echo` here because just a simple 'output'
    echo "You are an adult!"

# if the user's age is greater than '100'
elif [[ "$user_age" -ge 100 ]]; then
    # output appropriate message
    echo "Congratulations! You are about to die!"

# if the user's age is between 1 and 18
elif [[ "$user_age" -ge 1 && "$user_age" -le 18 ]]; then
    # output appropriate message
    # INFO: using `echo` here because just a simple 'output'
    echo "Where is your Guardian?"

fi
```

> [!WARNING]
> This is **not** Python! You are going to have to *close* the `if` statement with `fi` similar to something like *pseudo-code*

> [!INFO] You should go read about this!
> Link to StackOverflow Webpage: https://stackoverflow.com/questions/32320198/do-we-still-need-to-use-in-bash


## `case` Statements

```bash
#!/bin/env bash

# ask the user to enter his editor of choise
read -p "Enter your editor (nvim, emacs, vs c*de): " user_editor

# check the user's input
case "$user_editor" in
    # if the user entered 'nvim'
    nvim)
        # output appropriate message
        echo "You chose Neovim!"
        # end the case block... stop the `case` statement
        ;;

    # if the user entered 'nvim'
    emacs)
        # output appropriate message
        echo "You chose Emacs!"
        ;;

    # if the user entered 'nvim'
    "vs c*de")
        # output appropriate message
        echo "You chose VS C*de!"
        ;;

    # if the user entered something ridiculous like `nano` or `micro`
    *)
        # output appropriate message
        echo "Unknown editor."
        ;;
esac
```

> Again, don't forget to close the `case` statement with `asec`... *Which is 'case' written backwards*!

### `;;` and `;&` and `;;&`

As we have looked above... `;;` will stop the `case` statement *entirely* and the program will go run the next thing that comes after `asec`.

> But what about the others?

#### `;&` Operator

Study the following code found below $\downarrow$:

```bash
#!/bin/env bash

# ask the user to enter a number
read -p "Enter A Number: " user_editor

# check the user's input
case "$user_editor" in
    1)
        echo "This is first case '1' being executed!"
        # execute the next command just below
        ;&

    # if the user entered 'nvim'
    2)

        echo "This is first case '2' being executed!"
        # end the case block... stop the `case` statement
        ;;

    # if the user entered 'nvim'
    3)
        echo "This is first case '3' being executed!"
        # end the case block... stop the `case` statement
        ;;

    # if the user entered something ridiculous like `nano` or `micro`
    *)
        # output appropriate message
        echo "You Entered Something Else!"
        ;;
esac
```

Now, if the user is going to enter `1` as input... Then you are going to see that the `echo` command that is found in the **second** case is also going to run!

```console
This is first case '1' being executed!
This is first case '2' being executed!
```

> But everything else works just as fine!

#### `;;&` Operator

> But what will the `;;&` Operator Do?

Again, study the following code below:

> [!NOTE] I am Ashamed of Myself!!!
> So, the code that you are going to see below if provided by none other than [ChatGPT](https://chat.openai.com).
>
> I think that the example it provided is extremely good at showing what that `;;&` can do!
>
> > I am so sorry for copying a simple code to help me trying to understand something in Programming!
> > What I am trying to say is: "*I can do whatever the heck I want! This is my fucking notes and you are just living in it*!"
> > But I did modify the code!
>

```bash
#!/bin/env bash

# ask the user to enter a letter
read -p "Enter a letter: " user_letter

# check the user's input
case "$user_letter" in
    [aeiou] | [AEIOU])
        echo "Vowel detected"
        # DO NOT exit the `case` statement and continue to search throughout cases
        ;;&

    [a-z])
        echo "Lowercase letter"
        ;;


    [A-Z])
        echo "Uppercase letter"
        ;;

    *)
        echo "Other character or Multiple Characters Detected"
        ;;
esac
```

> I suggest you go and run the code found above!

> [!TIP]
> As you can see we **don't** use the `||` operator inside our *cases*. Instead we simply use a single *pipe* operator `|`!

# Loops

## `while` Loops

```bash
#!/bin/env bash

# iterate through the `while` loop indefinitely
while true; do
    # ask the user to enter his phone number
    read -p "Please Enter Telephone Number: " tel_num

    # check if the user's input is "digit" and has length of '8'
    # NOTE: we don't have `.isdigit()` function / method here
    # this means that we are going to actually write the regex ( regular expression )
    if [[ "$tel_num" =~ ^[0-9]+$ && ${#tel_num} -eq 8 ]]; then
        # exit / break from the `while` loop
        break

    # if the user string did not contain any number
    # or the length of string entered was not '8'
    else
        # output appropriate message
        echo -e "\nPlease Enter Correct Telephone Number!\n"
    fi
done

# display the following message after exiting the `while` loop
printf "\nYour Telephone Number is: %s" "$tel_num"
```

> [!NOTE]
> Don't forget about the `done` that **closes** the `while` loop

## `for` Loops

There are two version of `for` loops in BASH. There is the one that has a *syntax* that is specific to BASH and we also have **C-Style** `for` loops.

Again, if you know your `for` loops from [[C Language Basics | C]]; then you should be doing fine.

The code block that you are going to find below $\downarrow$ will contain **both** type!

```bash
#!/bin/env bash

# display 5 integer numbers from '0' to '4'
for i in {0..4}; do
    # display those numbers in a single line
    printf "%s " "$i"
done

printf "\n\n"

# display same 5 integer numbers ( from above ) in reverse
for (( i=4; i> =0; i-- )); do
    # display those numbers in a single line
    printf "%s " "$i"
done

printf "\n\n"

# display numbers from '1' to '100' ( inclusive )
for i in {1..100}; do
    # display those numbers in a single line
    printf "%s " "$i"
done

printf "\n\n"

# display even numbers from '1' to '100' ( inclusive )
for (( i=2; i<=100; i+=2 )); do
    # display those numbers in a single line
    printf "%s " "$i"
done


printf "\n\n"

# display odd numbers from '1' to '100' ( inclusive )
for (( i=1; i<=100; i+=2 )); do
    # display those numbers in a single line
    printf "%s " "$i"
done
```

> Similarly, **don't** forget about the `done` that closes the `for` loop!

## `until` Loops

This is basically the inverse of a `while` loop!

```bash
#!/bin/env bash

# iterate through the `until` loop indefinitely
# until user enters correct telephone number
until [[ "$tel_num" =~ ^[0-9]+$ && ${#tel_num} -eq 8 ]]; do
    # ask the user to enter the his telephone number
    read -p "Enter Your Telephone Number: " tel_num

    # check if the entered number is invalid
    if ! [[ "$tel_num" =~ ^[0-9]+$ && ${#tel_num} -eq 8 ]]; then
        printf "\nPlease Enter Correct Telephone Number!\n\n"
    fi

done

# display the user's telephone number
printf "\nYour Telephone Number: %s\n" "$tel_num"
```

> Again, **don't** forget the `done` keyword... *You little slut*!

## `select` Loops

> [!BUG]- Unique To BASH
> From what I have gathered... It *might* not work with ZSH...
>
> <p align="center"> <span style="color: lime";> But It Work on My Computer</span> !!!</p>

This is *kind-of* a combination of an **array** ( *we are going to get to later on* ) and the [[#`case` Statements | `case` Statement]]

```bash
#!/bin/env bash

# display the prompt to the user
# NOTE: this is going to be at the bottom of everything
PS3="Choose an option by entering its number: "

# use the `echo` command with `-e` to allow for `\n`
echo -e "\n=== Power Menu ===\n"

# display the items that the user can select
select choice in "Poweroff" "Restart" "Exit"; do
    # run a `case` statement to find correct user selection
    case $choice in
        # if the user wants to 'poweroff' the machine
        "Poweroff")
            # display appropriate message
            echo "Shutting down the system..."

            # turn of the machine using `systemctl`
            systemctl poweroff
            
            # escape the `select` loop
            break
            ;;

        # if the user wants to 'reboot' the machine
        "Restart")
            # display appropriate message
            echo "Rebooting the system..."

            # restart the machine using `systemctl`
            systemctl reboot

            # escape the `select` loop
            break
            ;;

        # if the user wants to exit the script / program
        "Exit")
            # display appropriate message
            echo "Exiting without shutting down."

            # escape the `select` loop
            break
            ;;

        # if the user entered something that is not found in selection
        *)
            # display appropriate message
            echo "Invalid option, please try again."
            ;;

    # close the `case` statement
    esac
done
```

> Similarly we should **not** forget the `done` for our `select` *loop*!
 
# Positional Arguments

> Let's get right into it! ( *Again, that's what she said!* )

Given the following code / command:

```bash
# display the following message using the echo command
echo "this    is  very     nice"
```

We all know that we **should** get this output right here!

```console
this    is  very     nice
```

But instead of the above $\uparrow$, we instead did something like this:

```bash
# display the following message using the echo command
echo this    is  very     nice
```

> Well, we did **remove** the `"` characters.

This is the output that we are going to *receive* in this case.

```console
this is very nice
```

> [!NOTE] This is what *Positional Arguments* Are!
> This is used extensively in other *command line* tools / utilities.

The *positional arguments* are in the template of `$x` where `x` is a **positive integer number**!.

This means that, in our case; it looks something like this:

- `$0`: The `echo` command itself
- `$1`: 'this'
- `$2`: 'is'
- `$3`: 'very'
- `$4`: 'nice'

Below you are going to find an example program that uses positional arguments to display the user's name.

```bash
#!/bin/env bash

# display the user's surname and name using positional arguments
printf "\nSurname: %s\nName: %s\n" "$1" "$2"
```

After running the *file* / script with `./main.sh JOE Mama`, we are going to get something like this as output $\downarrow$:

```console
Surname: JOE
Name: Mama
```

> Very Nice!

# Functions

## Function Templates

Below you are going to find the *template* for making a function in BASH or even something like [ZSH](https://github.com/zsh-users/zsh).

- Simple Function Template

```bash
# simple function in bash
foo() {
	# do nothing ==> "null"
	:
}
```

- Passing Parameters into Functions

> This is where [[#Positional Arguments | Positional Arguments]] comes into play!

```bash
# passing some arguments inside a function
foo() {
	# get the arguments
	# this means that we need to initialise local variables
	local var_1="$1"
	local var_2="$2"
	local var_3="$3"
}

# passing multiple arguments inside a function
# this is similar to something like `args` from C or Python
bar() {
    # initialise our counter ==> to emulate `enumerate` from Python
    local i=1

    # iterate through the arguments / items provided
    for file in "$@"; do
        # display the items together with its number
        echo "$i: - $file"

        # increment our counter
        i=$((i + 1))
    done

    # display the total number of items processed
    printf "\nTotal Items Processed: %d\n" "$#"
}
```

> This is how we are going to use it!

```bash
# NOTE: this should be inside the `.sh` script!
foo variable_1 variable_2 variable_3

bar item_1 item_2 item_3 item_4 item_5 item_6 item_7
```

- Exit Status

```bash
# simple status function to showcase `return`
status() {
    # check if some random fucking condition
    if [[ "$1" -eq 0 ]]; then
        # return a "success"
        return 0

    else
        # return a "failure"
        return 1
    fi
}
```

> This is how we are going to use these types of function

```bash
# NOTE: again, we are still in the `.sh` file
# call the function and pass any type of arguments
status 0

# check the condition
if [[ $? -eq 0 ]]; then
    # meaning that there was a success!
    echo "Success!"
else
    # meaning that there was a failure!
    echo "Failure"
fi
```

- Recursive Function

> [!NOTE] The *Simple* Recursive Function
> This is the same [[Python Language Basics#Recursive Function | factorial]] function that we wrote when we learnt about *functions* in Python.

```bash
#!/bin/bash

# our recursive factorial function
factorial() {
    # initialise our local variables
    local number="$1"
    local result

    # check if the argument provided is '0' or '1'
    if (( number == 0 || number == 1 )); then
        # display the factorial for these numbers
        echo 1

        # return the correct exit status code
        return 0
    fi

    # calculate the previous number ( argument )
    local prev_number=$((number - 1))

    # call the `factorial` function to calculate the factorial of the previous number
    local sub_factorial_result=$(factorial "$prev_number")

    # check if the exit status code for the above function is not '0'
    if [[ $? -ne 0 ]]; then
        # return the proper exit code
        return 1
    fi

    # calculate the final answer
    result=$((number * sub_factorial_result))

    # return the result to the main program
    echo "$result"

    # return the exit status code of '0'
    return 0
}
```

> Again still inside the script!

```bash
# call the function to calculate the factorial of '5'
fact_5=$(factorial 5)

# if the status code for function is '0'
if [[ $? -eq 0 ]]; then
    # output the factorial of that number
    echo "Factorial of 5 is: $fact_5"

# if the status code for function is '1'
else
    # output appropriate message
    echo "Failed to calculate factorial of 5."
fi
```

> It's so much bigger than I expected it to be!!! ( *that's what she fucking said* )

Again, it comes to the fact ( *get it! "fact" $\rightarrow$ factorial* ) its **not** really made for *computation*!

> Simply put... Its has **not** been designed for these types of tasks!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!