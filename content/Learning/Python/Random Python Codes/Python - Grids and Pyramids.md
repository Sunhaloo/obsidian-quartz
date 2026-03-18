---
id: Python - Grids and Pyramids
aliases: Display Grids / Pyramids in Python
tags:
  - C
author: S.Sunhaloo
date: 2025-08-25
status: Completed
---

> [!INFO]
> If you want the C version... Please look for the note '[[C - Grids and Pyramids]]'

# Display Grids

## Simple $x \times x$ Grids

```python
# function to display the grid with the required size
def display_grid(size: int):
    # iterate through the rows of the grid
    for i in range(size):
        # iterate through the columns of the grid
        for j in range(size):
            # display the characters ( for columns ) on a single line
            print("#", end="")

        # display a "newline" characters ==> move the caret
        print()


# our main function
def main():
    # ask the user to enter the number of rows and columns for grid
    size = int(input("\nPlease Enter Size of Grid: "))
    
    print()
    
    # call the function to display the grid of size `size`
    display_grid(size)


# source the main function
if __name__ == "__main__":
    main()
```

- If we use a `size` of 5, we should see something like this:

```console
#####
#####
#####
#####
#####
```

## Grids Of Custom Size

```python
# function to display the grid with the required size
def display_grid(rows: int, cols: int):
    # iterate through the rows of the grid
    for i in range(rows):
        # iterate through the columns of the grid
        for j in range(cols):
            # display the characters ( for columns ) on a single line
            print("#", end="")

        # display a "newline" characters ==> move the caret
        print()


# our main function
def main():
    # ask the user to enter the number of rows and columns for grid
    rows = int(input("\nPlease Enter Number of Rows: "))
    cols = int(input("Please Enter Number of Columns: "))

    print()

    # call the function to display the grid of size `size`
    display_grid(rows, cols)


# source the main function
if __name__ == "__main__":
    main()
```

- If we used a value of 5 for `rows` and 10 for `cols`:

```console
##########
##########
##########
##########
##########
```

### Custom Alignment With Grid Of Custom Size

```python
# function to display the grid with the required size
def display_grid(rows: int, cols: int, align_x: int, align_y: int):

    # iterate through the number of blank "align_y" rows
    for i in range(align_y):
        print()

    # iterate through the rows of the grid
    for i in range(rows):
        # iterate through the columns of the grid ==> display whitespaces
        for w in range(align_x):
            print(" ", end="")

        # iterate through the columns of the grid ==> display characters
        for j in range(cols):
            # display the characters ( for columns ) on a single line
            print("#", end="")

        # display a "newline" characters ==> move the caret
        print()

    # iterate through the number of blank "align_y" rows
    # INFO: doing this again to appear "centered"
    for i in range(align_y):
        print()


# our main function
def main():
    # ask the user to enter the number of rows and columns for grid
    rows = int(input("\nPlease Enter Number of Rows: "))
    cols = int(input("Please Enter Number of Columns: "))

    # ask the user to enter to hold size and width of whitespace
    alignment_x = int(input("Please Enter Number of Alignment ( X Position ): "))
    alignment_y = int(input("Please Enter Number of Alignment ( Y Position ): "))

    print()

    # call the function to display the grid of size `size`
    display_grid(rows, cols, alignment_x, alignment_y)


# source the main function
if __name__ == "__main__":
    main()
```

This is the output after running the above code with these inputs:

- `rows` = 5
- `cols` = 5
- `alignment_x` = 20
- `alignment_y` = 4

```console




                    #####
                    #####
                    #####
                    #####
                    #####




```

---

# Displaying Triangle and Pyramids

> [!NOTE]
> Instead of remembering the *inner loops*... Think in terms of **rows** itself

## Triangle Starting From Left

```python
# function to display our "left-sided" right-angled triangle
def display_triangle_left(num_of_rows: int):
    # iterate through the number of rows
    for rows in range(num_of_rows):
        # iterate through the number of columns
        for cols in range(rows + 1):
            print("#", end="")

        # change the line / caret's position
        print()


# our main function
def main():
    # ask the user to enter the number of rows
    num_of_rows = int(input("\nPlease Enter Number Of Rows: "))

    print()

    # call the function to display "left-sided" right-angled triangle
    display_triangle_left(num_of_rows)


# source the main function
if __name__ == "__main__":
    main()
```

- This is the output that we are going to get if we use a value of 5 for `num_of_rows`

```console
#
##
###
####
#####
```


### Same Triangle But Upside Down

```python
# function to display our "left-sided" right-angled triangle
def display_triangle_left(num_of_rows: int):
    # iterate through the number of rows
    for rows in range(num_of_rows):
        # iterate through the number of columns
        for cols in range(rows, num_of_rows):
            print("#", end="")

        # change the line / caret's position
        print()


# our main function
def main():
    # ask the user to enter the number of rows
    num_of_rows = int(input("\nPlease Enter Number Of Rows: "))

    print()

    # call the function to display "left-sided" right-angled triangle
    display_triangle_left(num_of_rows)


# source the main function
if __name__ == "__main__":
    main()
```

- Again, this is the output that we get when using the `num_of_row` with a value of 5

```console
#####
####
###
##
#
```

## Triangle Starting Right

```python
# function to display our "right-sided" right-angled triangle
def display_triangle_right(num_of_rows: int):
    # iterate through the number of rows
    for rows in range(num_of_rows):
        # iterate through the number of columns
        for cols in range(rows, num_of_rows - 1):
            print(" ", end="")

        for chars in range(rows + 1):
            print("#", end="")

        # change the line / caret's position
        print()


# our main function
def main():
    # ask the user to enter the number of rows
    num_of_rows = int(input("\nPlease Enter Number Of Rows: "))

    print()

    # call the function to display "left-sided" right-angled triangle
    display_triangle_left(num_of_rows)


# source the main function
if __name__ == "__main__":
    main()
```

- Using a value of 5 for `num_of_rows`:

```console
    #
   ##
  ###
 ####
#####
```

### Same Triangle But Upside Down

```python
# function to display our "right-sided" right-angled triangle
def display_triangle_right(num_of_rows: int):
    # iterate through the number of rows
    for rows in range(num_of_rows):
        # iterate through the number of columns
        for cols in range(rows, num_of_rows):
            print("#", end="")

        # change the line / caret's position
        print()
```

- Using the value of 5 with `num_of_rows`:

```console
#####
####
###
##
#
```

### Same Triangle But Mirrored

```python
# function to display lower half ( left-side ) of triangle
def display_triangle_left(num_of_rows: int):
    # iterate through the number of rows ==> lower half
    for rows in range(num_of_rows, 0, -1):
        # iterate through the number of columns ==> to print lower left whitespaces
        for cols in range(num_of_rows - rows):
            print(" ", end="")

        # iterate through the number of columns ==> to print lower left characters
        for chars in range(rows):
            print("#", end="")

        # change the line / caret's position
        print()
```

- This is the output that we get after using a value of 5 for `num_of_rows`

```console
#####
 ####
  ###
   ##
    #
```

---

# Display A Pyramid

Therefore, its just a case of combining the individual "*modules*" to make "*any*" shape that we want.

```python
# function to display pyramid
def display_pyramid(num_of_rows: int):
    # iterate through the number of rows
    for rows in range(num_of_rows):
        # iterate through the number of columns ==> to print left corner whitespaces
        for cols in range(rows, num_of_rows - 1):
            print(" ", end="")

        # iterate through the number of columns ==> to print left corner characters
        for cols in range(rows + 1):
            print("#", end="")

        # iterate through the number of columns ==> to print right corner characters
        for cols in range(rows):
            print("#", end="")

        # change the line / caret's position
        print()


# our main function
def main():
    # ask the user to enter the number of rows
    num_of_rows = int(input("\nPlease Enter Number Of Rows: "))

    print()

    # call the function to display the pyramid
    display_pyramid(num_of_rows)


# source the main function
if __name__ == "__main__":
    main()
```

- Using a value of 10 for `num_of_rows`

```console
         #
        ###
       #####
      #######
     #########
    ###########
   #############
  ###############
 #################
###################
```

## With Custom Alignment

```python
# function to display pyramid
def display_pyramid(num_of_rows: int, align_x: int, align_y: int):
    # iterate through the number of blank "align_y" rows
    for i in range(align_y):
        print()

    # iterate through the number of rows
    for rows in range(num_of_rows):
        # iterate through the number of columns ==> display whitespaces
        for w in range(align_x):
            print(" ", end="")

        # iterate through the number of columns ==> to print left corner whitespaces
        for cols in range(rows, num_of_rows - 1):
            print(" ", end="")

        # iterate through the number of columns ==> to print left corner characters
        for cols in range(rows + 1):
            print("#", end="")

        # iterate through the number of columns ==> to print right corner characters
        for cols in range(rows):
            print("#", end="")

        # change the line / caret's position
        print()

    # iterate through the number of blank "align_y" rows
    for i in range(align_y):
        print()
```

This is the output after running the above code with these inputs:

- `num_of_rows` = 10
- `alignment_x` = 5
- `alignment_y` = 5

```console





              #
             ###
            #####
           #######
          #########
         ###########
        #############
       ###############
      #################
     ###################






```

---

# Display a Diamond

```python
# fucntion to display a diamond
def display_diamond(num_of_rows: int):
    # iterate through the number of rows ==> for upper diamond
    for rows in range(num_of_rows):
        # iterate through the number of columns ==> to print upper left whitespaces
        for cols in range(rows, num_of_rows - 1):
            print(" ", end="")

        # iterate through the number of columns ==> to print upper left characters
        for chars in range(rows + 1):
            print("#", end="")

        # iterate through the number of columns ==> to print upper right characters
        for chars in range(rows):
            print("#", end="")

        # change the line / caret's position
        print()

    # iterate through the number of rows ==> for lower diamond
    for rows in range(num_of_rows - 1, 0, -1):
        # iterate through the number of columns ==> to print lower left whitespaces
        for cols in range(rows, num_of_rows):
            print(" ", end="")

        # iterate through the number of columns ==> to print lower left characters
        for chars in range(rows):
            print("#", end="")

        # iterate through the number of columns ==> to print lower right characters
        for chars in range(rows - 1):
            print("#", end="")

        # change the line / caret's position
        print()


# our main function
def main():
    # ask the user to enter the number of rows
    num_of_rows = int(input("\nPlease Enter Number Of Rows: "))

    print()

    # call the function to display the diamond
    display_diamond(num_of_rows)


# source the main function
if __name__ == "__main__":
    main()
```

- This is the output that I am going see when I use a value of 10 for `num_of_rows`

```console
         #
        ###
       #####
      #######
     #########
    ###########
   #############
  ###############
 #################
###################
 #################
  ###############
   #############
    ###########
     #########
      #######
       #####
        ###
         #
```

## With Custom Alignment

```python
# fucntion to display a diamond
def display_diamond(num_of_rows: int, align_x: int, align_y: int):
    # iterate through the number of blank "align_y" rows
    for i in range(align_y):
        print()

    # iterate through the number of rows ==> for upper diamond
    for rows in range(num_of_rows):
        # iterate through the columns of the grid ==> display whitespaces
        for w in range(align_x):
            print(" ", end="")

        # iterate through the number of columns ==> to print upper left whitespaces
        for cols in range(rows, num_of_rows - 1):
            print(" ", end="")

        # iterate through the number of columns ==> to print upper left characters
        for chars in range(rows + 1):
            print("#", end="")

        # iterate through the number of columns ==> to print upper right characters
        for chars in range(rows):
            print("#", end="")

        # change the line / caret's position
        print()

    # iterate through the number of rows ==> for lower diamond
    for rows in range(num_of_rows - 1, 0, -1):
        # iterate through the columns of the grid ==> display whitespaces
        for w in range(align_x):
            print(" ", end="")

        # iterate through the number of columns ==> to print lower left whitespaces
        for cols in range(rows, num_of_rows):
            print(" ", end="")

        # iterate through the number of columns ==> to print lower left characters
        for chars in range(rows):
            print("#", end="")

        # iterate through the number of columns ==> to print lower right characters
        for chars in range(rows - 1):
            print("#", end="")

        # change the line / caret's position
        print()

    # iterate through the number of blank "align_y" rows
    for i in range(align_y):
        print()
```

This is the output after running the above code with these inputs:

- `num_of_rows` = 10
- `alignment_x` = 5
- `alignment_y` = 5

```console





              #
             ###
            #####
           #######
          #########
         ###########
        #############
       ###############
      #################
     ###################
      #################
       ###############
        #############
         ###########
          #########
           #######
            #####
             ###
              #





```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!