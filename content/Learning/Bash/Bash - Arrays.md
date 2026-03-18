---
id: Bash - Arrays
aliases: Arrays in BASH
tags:
  - bash
  - script
author: S.Sunhaloo
date: 2025-07-01
status: Completed
---

## List of Contents

- [[#Creation of Arrays]]
- [[#Displaying - Accessing Arrays]]
- [[#Insertion of Data]]
- [[#Removal of Data]]
- [[#Miscellaneous "Functions"]]
	- [[#Array Slicing]]

---

> [!WARNING]
> Similar to the way that we made '[[Bash Language Basics]]'... We are also going to **not** go into too much detail as we... I feel like with BASH; we actually need to go ahead and make something!
>
> > Instead of you know... Just reading shit out!
>

# Creation of Arrays

To create an array in BASH, we use the `()` characters

```bash
# array of integers numbers only
int_arr=(1 2 3 4 5)

# array containing most data types
general_arr=(
    44
    5.5
    "A"
    "Something"
    "1 2 3"
    "4 5 6"
    "7 8 9"
)
```

> [!NOTE] Accessing Elements
> BASH's arrays are "*zero-based*" indexing and therefore, the *first* element is found at *index* '**0**'.
>
> Now, they are also similar to Python's whereby we can access the **last element** with *negative indexing*!
>
> Nevertheless, is **not** as simple as doing `"$int_list[x]"` or `"$general_list[x]"` ( *where `x` is an integer number* ).
>
> To access and **single** element from an array in BASH, we need to follow this "*template*" $\downarrow$:
>
> ```bash
> # access and display the first element of integer array
> echo "${int_arr[0]}"
> # access and display the last element of integer array
> echo "${general_arr[-1]}"
> ```
>
> > Don't worry, I think you should be able to find more information below!
>

---

# Displaying - Accessing Arrays

## Length of Arrays

Now, there are no such thing as the `len()` or the `sizeof()` *function* here! Therefore, we are going to have to find another way to find the **length** of arrays in BASH.

```bash
#!/bin/env bash

# array of integers numbers only
int_arr=(1 2 3 4 5)

# array containing most data types
general_arr=(
    44
    5.5
    "A"
    "Something"
    "1 2 3"
    "4 5 6"
    "7 8 9"
)

# use the `echo` command with 'back slash'
echo -e "\nLength of Integer Array: ${#int_arr[@]}"
echo -e "Length of General Array: ${#general_arr[@]}\n"
```

This should return us something that looks like this:

```console
Length of Integer Array: 5
Length of General Array: 7
```

Now the thing that actually finds the length and keep track of "*the number of things*" is actually the `#` operator!

## Displaying Arrays and Array Values

This is going to me showcasing to you, some of the ways that we can display an ( */ the contents of an* ) array in BASH.

> [!NOTE]
> Even though I said that I am going to be *only* using the `printf` command.
>
> I need to stress that there are some advantages for using the `echo` command.
> Therefore, you might see me using the `echo` command when I need to!

> I am going to be writing these *ways* inside a single code block!

```bash
#!/bin/env bash

# array of integer numbers
int_arr=(1 2 3 4 5)

printf "\n== Simplest and Easiest Way ==\n"

# display all the contents of array at once
echo "${int_arr[@]}"

# NOTE: we could have also done something like this
printf "%s" "${int_arr[@]}"

printf "\n\n== Normal BASH Way ==\n"

# iterate through the array
for i in "${int_arr[@]}"; do
    # display the element
    printf "%d" "$i"
done

printf "\n\n== C-Style Version ==\n"

# iterate through the array
# NOTE: we could have created a variable to hold the length of array
for ((i=0; i < ${#int_arr[@]}; i++)); do
    printf "Index: %d | Value: %d\n" "$i" "${int_arr[$i]}"
done
```

# Insertion of Data

Well, this is BASH and again and again and *fucking* again. There are **no** such things like `.append()` or `.insert()`.

Therefore, we are going to have to use our simple *data manipulation* to be able to use it.

> [!INFO]
> Now there are some ways to *emulate* for example, the `.append()` or even the `.extend()` function from [[Python - Lists#Insertion of Data | Python]].
>
> But I would not really make an "*apples to apples*" comparision.

> Again, I am placing everything inside a single code block!

```bash
#!/bin/env bash

# array of integer numbers
int_arr=(0 2 3 4)

# output the integer array ( before insertion )
echo "Integer Array ( Before Insertion ): ${int_arr[@]}"

# Append
# append the element '5' to the array
int_arr+=(5)

# insert and element at a specific place
int_arr[1]=1

# Extend with another array
another_int_arr=(6 7 8)
int_arr+=( "${another_int_arr[@]}" )

# output the integer array ( after insertion )
echo "Integer Array ( After Insertion ): ${int_arr[@]}"
```

## Example Code: User Input

```bash
#!/bin/env bash

# array of integer numbers
int_arr=()

# output the integer array ( before insertion )
echo -e "Integer Array ( Before Insertion ): ${int_arr[@]}\n"

# iterate through the `while` loop indefinitely
while true; do
    # ask the user to enter amount of elements / integer numbers to add
    read -p "Please Enter Number of Integers to Add: " user_amount

    echo

    # check if the user's input is actually an integer number
    if [[ "$user_amount" =~ ^[0-9]+$ ]]; then
        # exit / break from the `while` loop
        break

    # if the user does not enter an integer number
    else
        # output appropriate message
        echo -e "Please Enter Integer Numbers Only!!!\n"

    fi
done

# iterate through that amount
# WARNING: for numeric iterations like we are doing now...
# USE C-Style `for` Loops!!! This is a command and NOT a suggestion
for ((i=0; i < user_amount; i++)); do
    # iterate through the `while` loop indefinitely
    while true; do
        # ask the user to enter the element / integer number
        read -p "Please Enter of Integer Number: " user_int

        # check if the user's input is actually an integer number
        if [[ "$user_amount" =~ ^[0-9]+$ ]]; then
            # add that integer entered by user to the array
            int_arr+=("$user_int")
            # exit / break from the `while` loop
            break

        # if the user does not enter an integer number
        else
            # output appropriate message
            echo -e "\nPlease Enter Integer Numbers Only!!!\n"

        fi
    done
done

# output the integer array ( after insertion )
echo -e "\nInteger Array ( After Insertion ): ${int_arr[@]}"
```

# Removal of Data

Similarly, we are going to have to learn about removing data from an *array* if we ever going to need to!

> Again, BASH is **not** really made for *computation*!!!

```bash
#!/bin/env bash

# array of integer numbers
int_arr=(1 2 3 4 5 6 7 8 9 10)

# output the integer array ( before removal )
echo "Integer Array ( Before Removal ): ${int_arr[@]}"

# remove element using its respective index
# remove the element '4' from the list
unset 'int_arr[4]'

# WARNING: this is the reason that we need to learn "low-level" languages like C!
# we are not going to have to "re-index" the whole array as we have removed a value
# this means that the elements inside the array will have to move to the left!
int_arr=( "${int_arr[@]}" )

echo "Integer Array ( During Removal ): ${int_arr[@]}"

# remove the first element using slicing
int_arr=( "${int_arr[@]:1}" )

echo "Integer Array ( During Removal ): ${int_arr[@]}"

# remove the last element using slicing
int_arr=( "${int_arr[@]:0:${#int_arr[@]}-1}" )

echo "Integer Array ( During Removal ): ${int_arr[@]}"

# remove elements from array using its actual value and not index
# NOTE: bash cannot simply "remove" an array, we are going to place
# that remove value inside another array

# variable that holds value we are going to remove
val_to_remove=7

# iterate through the array
for i in "${!int_arr[@]}"; do
    # check if element to be removed has been found
    if [[ "${int_arr[i]}" == "$val_to_remove" ]]; then
        # meaning that element has been found and we 
        unset 'int_arr[i]'
    fi
done

# as we have remove an element from the array
# we are going to have to "re-index" the array
int_arr=( "${int_arr[@]}" )

# output the integer array ( after removal )
echo "Integer Array ( Before Removal ): ${int_arr[@]}"
```

> [!TIP] No Errors!
> > I have a *Python Background*!
>
> So you know if you are going to *remove* an element from **empty** list in Python; we all know that we are going to get the *famous* `IndexError`!
>
> But BASH does **not** give you any errors... Instead it just... *Nothing* happens!
>
> Now, because I am still "*young*" ( *in terms of BASH scripting* ). I don't really know how it works under the hood and I need to ask my lecturer about this!

# Miscellaneous "Functions"

## Array Slicing

> Oh yes! *It kinda does*!

Now, again and *fucking* again; this is not a fully fledged programming language! Therefore, its going to be a dumb-down version of what we have in Python!

Here is what the template looks like for the **slicing** $\downarrow$:

```bash
"${array[@]:start:length}"
```

Below you are going go find some examples, *inside a single code block*, that you can experiment with:

```bash
#!/bin/env bash

# initialise our array containing some letters
str_arr=(a b c d e f g h i j)

# display the full string array
echo "Full String Array: ${str_arr[@]}"
echo

# display the array but skip the first 2
echo "Start From Second Index ( Third Element ):"
echo "${str_arr[@]:2}"
echo

# display the array but skip the first 3 elements and "take" only 4
echo "Start From Third Index ( Fourth Element ) and Retrieve 3 MORE:"
echo "${str_arr[@]:3:4}"
echo

# display the last 3 elements of array
echo "Start From Back and Retrieve 3 Elements:"
# WARNING: there as to be a space after the `:` character
echo "${str_arr[@]: -3}"
echo

# display the first 5 elements of array
echo "Start From Zeroth Index and Retrieve 4 MORE:"
echo "${str_arr[@]:0:5}"
echo
```

> I am going to also add its output just for this one!

```console
Full String Array: a b c d e f g h i j

Start From Second Index ( Third Element ):
c d e f g h i j

Start From Third Index ( Fourth Element ) and Retrieve 3 MORE:
d e f g

Start From Back and Retrieve 3 Elements:
h i j

Start From Zeroth Index and Retrieve 4 MORE:
a b c d e
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!