---
id: Python - Arrays
aliases: Arrays in Python
tags:
  - python
  - data-structures
  - arrays
  - lists
author: S.Sunhaloo
date: 2025-09-15
status: Completed
---

## List of Contents

- [[#Creation Of Arrays]]
- [[#Cool Functions / Methods Of Arrays]]
	- [[#Information About Buffer]]
	- [[#From Bytes]]
	- [[#To Bytes]]
	- [[#To Unicode]]
	- [[#To Lists and From Lists]]
	- [[#To File and From Files]]

---

> [!INFO] Back Story
> I have been using Python for 3 to 4 years now and I did **not** know that Python had "*arrays*" similar to something like in [[REDO C - Static Arrays| C]]!
>
> Additionally, I am also going to look at Numpy arrays which is going to be really exiting!
>
> Link To Numpy Documentation: https://numpy.org/

# Creation Of Arrays

To create "*primitive*" array in Python, refer to that following code block below:

```python
import array

# array of integer numbers
int_arr = array.array("i", [1, 2, 3, 4, 5])

# array of float numbers
float_arr = array.array("f", [5.0, 6.0, 6.9, 7.0])

# array of double numbers
double_arr = array.array("f", [69.69, 0.123567890])

# array of characters
char_arr = array.array("w", ["F", "u", "c", "k", " ", "Y", "o", "u", "!"])
```

## Functions Related To Arrays

- Use the `dir` function to check what *functions* / *methods* are associated with `array.array`:

```python
# import the required 'array' module
import array

# filter out all the unncessary things that we don't really need
funcs = [function for function in dir(array.array) if not function.startswith("__")]

# display all the functions / methods associated with `array.array`
print("\nFunctions / Methods Associated With Arrays:")

# iterate through the array and display the functions / methods
for func in funcs:
    print(func)
```

- This is the output after running the above code:

```console
Functions / Methods Associated With Arrays:
append
buffer_info
byteswap
clear
count
extend
frombytes
fromfile
fromlist
fromunicode
index
insert
itemsize
pop
remove
reverse
tobytes
tofile
tolist
tounicode
typecode
```

> [!TIP] Pretty Much The Same Thing As `list`!
> As you can see, for the most important functionality like **insertion**, **removal** and **searching** for elements is basically the same thing!
>
> Therefore, refer to the file / note '[[Python - Lists]]' for more information about them.
>
> > But there are some cool stuff that I found!
>

# Cool Functions / Methods Of Arrays

## Information About Buffer

> Link To Python's `.buffer_info()` documentation: https://docs.python.org/3/library/array.html#array.array.buffer_info

```python
# import arrays from the 'array' module
from array import array

# declare and initalise array of characters
char_arr = array("w", ["F", "u", "c", "k", " ", "Y", "o", "u", "!"])

# find the memory address / location and number of elements from character array
memory_address, number_of_elements = char_arr.buffer_info()

# calculate the buffer "memory" size in megabytes
memory_size = (number_of_elements * char_arr.itemsize) / (1024 * 1024)

# display the information
print(f"\nMemory Address: {memory_address}")
print(f"Memory Buffer Size: {memory_size:.8f} Megabytes")
print(f"Number Of Elements: {number_of_elements}\n")
```

- Therefore, we should see something like this:

```console
Memory Address: 140096736683920
Memory Buffer Size: 0.00003433 Megabytes
Number Of Elements: 9
```

## From Bytes

> *So... There is `struct` in Python*!?!

```python
# import arrays from the 'array' module
from array import array

# import the 'struct' module to be able to use `pack` function
# NOTE: doing `import struct` instead of `from struct import pack` to see "struct"
import struct

# declare array of integers
int_arr = array("i")

# declare and initialise structure of integers
int_struct: bytes = struct.pack("5i", 1, 2, 3, 4, 5)

# sends those "bytes" ( using the `frombytes`function ) to populate the integer array
int_arr.frombytes(int_struct)

# display the array of integers
print(f"\nArray Of Integers: {int_arr}\n")
```

- This is the output after running the above code:

```console
Array Of Integers: array('i', [1, 2, 3, 4, 5])
```

## To Bytes

Similarly, we could convert the individual data inside the array into its *bytes* component.

```python
# import arrays from the 'array' module
from array import array

# import the `unpack` function from the 'struct' module
from struct import unpack


# declare and initialise array of integers
int_arr = array("i", [1, 2, 3, 4, 5])

# convert the integer array into its "bytes" component
int_arr_bytes: bytes = int_arr.tobytes()

# unpack the "bytes" into a struct
int_struct = unpack("5i", int_arr_bytes)


print(f"\n'Struct' / Tuple After Unpacking Integer Array: {int_struct}")
```

- Therefore, at the end we should get the **readable** numbers:

```console
'Struct' / Tuple After Unpacking Integer Array: (1, 2, 3, 4, 5)
```

## To Unicode

> Link To Wikipedia: https://en.wikipedia.org/wiki/Unicode

```python
# import arrays from the 'array' module
from array import array

# declare and initalise array of characters
char_arr = array("w", ["F", "u", "c", "k", " ", "Y", "o", "u", "!"])

# combine the characters found inside character array to a string
text: str = char_arr.tounicode()

# display the string on the screen
print(f"\nString From Character Array: {text}\n")
```

- This is the output that we get after running the simple code above:

```console
String From Character Array: Fuck You!
```

## To Lists and From Lists

```python
# import arrays from the 'array' module
from array import array

# declare and intialise an integer array
int_arr = array("i", [1, 2, 3, 4, 5])

# convert the integer array into a list
int_list: list[int] = int_arr.tolist()

# display the list and its type
print(f"\nInteger Array Coverted To List: {int_list}")

# NOTE: removing the last element from the list to show that list can be coverted back
int_list.pop()

# declare new array of integers
new_int_arr = array("i")

# call the function to convert integer list back into array of integers
new_int_arr.fromlist(int_list)

print(f"Integer List Coverted Back To Array Of Integers: {new_int_arr}")
```

- This is the output that we should get after running the above code:

```console
Integer Array Coverted To List: [1, 2, 3, 4, 5]
Integer List Coverted Back To Array Of Integers: array('i', [1, 2, 3, 4])
```

## To File and From Files

> [!WARNING] Binary Data Files!
> Yes, the files that we are going to be using are **not** going to be *human readable*!
>
> The code block will show us how to use both the `.tofile` and `.fromfile` functions... I created a little function for each of them.

```python
# import arrays from the 'array' module
from array import array, typecodes

# import `getsize` function from the 'os' sub-module "path"
from os.path import getsize


# function to read data from a binary file
def write_binary_file(binary_file_name: str, arr: array):
    # open the binary file for reading
    with open(binary_file_name, "wb") as binary_file:
        # write the binary "bytes" to the file
        arr.tofile(binary_file)


# function to read data from a binary file
def read_binary_file(binary_file_name: str):
    # open the binary file for reading
    with open(binary_file_name, "rb") as binary_file:
        # read each line of the file until EOF
        for line in binary_file:
            print(line)


# function to create array of integers from binary data found in file
def create_int_arr(binary_file_name: str, file_size: int, type_size: int) -> array:
    # NOTE: need to delcare array... in this case declaring it here itself
    int_arr: array = array("i")

    # calculate the total number of elements to add to array
    # INFO: in this case, I am adding all elements found inside the array
    # NOTE: here we are doing something similar to our `scanf` function from C
    # to find the length / number of elements inside an array... same principle here
    num_of_data = file_size // type_size

    # open the file for reading
    with open(binary_file_name, "rb") as binary_file:
        # use the `fromfile` function to convert binary data to integer array
        int_arr.fromfile(binary_file, num_of_data)

    # return the populated integer array from to the main program
    return int_arr


# our main function
def main():
    # variable to hold the name of the binary file to write to
    file_name = "binary_arr.bin"
    # declare and intialise array of integers
    int_arr = array("i", [1, 2, 3, 4, 5])

    # call the function to write data to the file
    write_binary_file(file_name, int_arr)

    # call the function to read the data from the file
    read_binary_file(file_name)

    # declare new array of integers
    new_int_arr: array = array("i")

    # call the function and pass the required parameters
    new_int_arr = create_int_arr(file_name, getsize(file_name), array("i").itemsize)

    # display the new array created
    print(f"\nInteger Array Created From File: {new_int_arr}\n")


# source the main function
if __name__ == "__main__":
    main()
```

- Below you are going to find the output after running the above code:

```console
b'\x01\x00\x00\x00\x02\x00\x00\x00\x03\x00\x00\x00\x04\x00\x00\x00\x05\x00\x00\x00'

Integer Array Created From File: array('i', [1, 2, 3, 4, 5])
```

---

> [!TIP] **Limitations** With `array.array`!!!
> - We can only create array for a *small* amount of **data types** and actually be able to use them
> 	- For example, we cannot really use "*string arrays*" like in C
> - No multidimensional support – it’s strictly one-dimensional; you’d need nested arrays or switch to numpy for matrices
> - **Cannot** create *multidimensional* array
> 	- Would have to "**_nest_**" array below one another
> 	- Which is clearly not what we want
>
> > [!INFO]
> > > Therefore, Numpy Arrays!
> >
> > Yes, Numpy Arrays apparently add *support* for multidimensional arrays and pretty much all the good stuff!
> >
> > > Also, I just want to try it out! *Famous, Famous Numpy*!!!
> >
> > Here is the file / note that I created for Numpy: '[[Python - Numpy]]'
>

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!