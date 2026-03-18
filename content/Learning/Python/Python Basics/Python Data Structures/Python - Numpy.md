---
id: Python - Numpy
aliases: The Famous Numpy Module ( Python )
tags:
  - python
  - data-structures
  - arrays
author: S.Sunhaloo
date: 2025-09-15
status: HOLD
---

## List of Contents

- [[#Installation Of Numpy Module]]
- [[#Numpy Arrays]]
	- [[#Types and `dtype` Argument!]]
- [[#Functions / Methods Related To Numpy]]

---

> [!INFO] Resource(s)
> - https://numpy.org/
> 	- https://numpy.org/install/
> - https://numpy.org/doc/stable/
> 	- Absolute Basics: https://numpy.org/doc/stable/user/absolute_beginners.html
> 	- User Guide: https://numpy.org/doc/stable/user/index.html#user

# Installation Of Numpy Module

- This is how I installed the `numpy` module on my Arch ( *based* ) system:

```bash
# install numpy module globally
sudo pacman -S python-numpy
```

> [!SUCCESS] Verification Of Installation ( *as per documentation* )
> - I did this inside the Python 'REPL':
>
> ```python
> import numpy as np
> np.__version__
> ```
>
> Therefore, this is what I go as output:
>
> ```console
> '2.3.2'
> ```

---

# Numpy Arrays

- The following code block below is going to show us how to create simple **one dimensional** *numpy* arrays:

```python
# import the whole numpy library and alias it to `np`
import numpy as np

# numpy array of integer numbers
int_arr = np.array([1, 2, 3, 4])
# numpy array of float numbers
float_arr = np.array([5.0, 6.0, 6.9, 7.0])
# numpy array of double numbers
double_arr = np.array([69.69, 0.123567890])
# numpy array of characters
char_arr = np.array(["F", "u", "c", "k", " ", "Y", "o", "u", "!"])
```

- In the following code block you are going to see me create some **multidimensional** *numpy* arrays:

```python
# import the whole numpy library and alias it to `np`
import numpy as np

# two dimensional numpy integer arrays
int_2_arr = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

# three dimensional numpy float arrays
float_3_arr = np.array(
    # outer `[]` ==> three dimensional numpy array
    [
        # first two dimensional array
        [[1.1, 2.2], [3.3, 4.4]],
        # second two dimensional array
        [[5.5, 6.6], [7.7, 8.8]],
    ]
)

# four dimensional numpy character arrays
char_4_arr = np.array(
    # outer `[]` ==> four dimensional numpy array
    [
        # first three dimensional array
        [
            # first inner two dimensional array
            [["a", "b"], ["c", "d"]],
            # second inner two dimensional array
            [["e", "f"], ["g", "h"]],
        ],
        # second three dimensional array
        [
            # first inner two dimensional array
            [["i", "j"], ["k", "l"]],
            # second inner two dimensional array
            [["m", "n"], ["o", "p"]],
        ],
    ],
)
```

## Types and `dtype` Argument!

- Given the following python code:

```python
# import the whole numpy library and alias it to `np`
import numpy as np

# numpy array of integer numbers
int_arr = np.array([1, 2, 3, 4])
# numpy array of float numbers
float_arr = np.array([5.0, 6.0, 6.9, 7.0])
# numpy array of double numbers
double_arr = np.array([69.69, 0.123567890])
# numpy array of characters
char_arr = np.array(["F", "u", "c", "k", " ", "Y", "o", "u", "!"])
# numpy array of booleans
bool_arr = np.array([True, False, True, False])

# display the types of the following numpy arrays created above
print(f"\nType of Integer Numpy Array: {int_arr.dtype}")
print(f"Type of Float Numpy Array: {float_arr.dtype}")
print(f"Type of Double Numpy Array: {double_arr.dtype}")
print(f"Type of Character Numpy Array: {char_arr.dtype}")
print(f"Type of Boolean Numpy Array: {bool_arr.dtype}\n")
```

- This is the output after running the above code:

```console
Type of Integer Numpy Array: int64
Type of Float Numpy Array: float64
Type of Double Numpy Array: float64
Type of Character Numpy Array: <U1
Type of Boolean Numpy Array: bool
```

Numpy provides "*C-style*" data types whereby we can specify the **number of bytes** taken by each *element* inside the array.

For example; by default **integer** arrays in Numpy will be given the *datatype* of `int64`. But what if we know that we are only going to be using **single digit** integer numbers we could probably get away with `int8`!

```python
# import the whole numpy library and alias it to `np`
import numpy as np

# numpy array of integer numbers
int_arr = np.array([1, 2, 3, 4], dtype=np.int8)

# display the updated type of our integer array
print(f"\nType of Integer Numpy Array: {int_arr.dtype}")
```

- As you can see, in this case, we get `int8` as output:

```console
Type of Integer Numpy Array: int8
```

> [!NOTE]
> This could also be used for *security* purposes as if we are asking a user to enter a some elements inside a specific Numpy array.
>
> ```python
> # import the whole numpy library and alias it to `np`
> import numpy as np
>
> # numpy array of integer numbers
> new_int_arr = np.array([1, 2, 3, 4], dtype=np.int8)
>
> # display the updated type of our integer array
> print(f"\nType of Integer Numpy Array: {new_int_arr.dtype}")
>
> # WARNING: this is a reassignment and not a "direct" append
> # the `np.append` function creates a new array
> new_int_arr = np.append(new_int_arr, 5.5)
>
> print(f"Type of Integer Numpy Array: {new_int_arr.dtype}")
> ```
>
> - I think that is should give us an error:
>
> ```console
> Type of Integer Numpy Array: int8
> Type of Integer Numpy Array: float64
> ```
>
>
> > "*Okay...*"!
>
>
> > [!TIP] Oh Shit
> > When I try to add the '5.5' inside our `int_arr`... *You actually "<span style="color: orange;"> cannot</span> "*
> >
> > Compared to our lovely `.append` function that can be used with `list`s and `array`s in Python. Numpy arrays are **different** whereby we have a *specific* `numpy.append()` function whereby it does **not** do a "*in-place*" modification and instead it creates a **completely new** array with the correct data type!
> >
> > - This is what the *new* array looks like:
> >
> > ```console
> > [1.  2.  3.  4.  5.5]
> > ```
>

# Functions / Methods Related To Numpy

> [!INFO] Official List Of *Functions* / *Methods*
> - https://numpy.org/doc/stable/reference/arrays.ndarray.html
>
> > [!NOTE]
> > As I don't really need to learn about the `numpy` module and just wanted to *taste* it... I am **not** going to spend much time learning about it for now.
> >
> > I will be going slowly and learn *for fun* what it can do, at a very **slow** pace.
> >
> > > Therefore, I am going to the `status` of this file / note to `HOLD`!
> >
>


---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!