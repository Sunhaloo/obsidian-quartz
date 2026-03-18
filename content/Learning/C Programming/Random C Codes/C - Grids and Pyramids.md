---
id: C - Grids and Pyramids
aliases: Display Grids / Pyramids In C
tags:
  - C
  - basics
author: S.Sunhaloo
date: 2025-08-25
status: Completed
---

> [!INFO]
> If you want the Python version... Please look for the note '[[Python - Grids and Pyramids]]'

# Displaying Grids

## Simple $x \times x$ Grids

```c
#include <stdio.h>

// function to display a grid with required size
void display_grid(int size) {
  // iterate through the rows of the grid
  for (int i = 0; i < size; i++) {
    // iterate through the columns of the grid
    for (int j = 0; j < size; j++) {
      // display the character on the same line
      printf("#");
    }

    // change the position of the caret
    printf("\n");
  }
}

// our main function
int main(int argc, char *argv[]) {
  // declare variable that will hold the size of grid
  int grid_size;

  // ask the user to enter size of grid
  printf("\nPlease Enter Size of Grid: ");
  scanf("%d", &grid_size);

  // call the function to display the grid
  display_grid(grid_size);

  return 0;
}
```

- If we use a `grid_size` of 5, we should see something like this:

```console
#####
#####
#####
#####
#####
```

## Grids Of Custom Size

```c
#include <stdio.h>

// function to display a grid with required size
void display_grid(int rows, int cols) {
  // iterate through the rows of the grid
  for (int i = 0; i < rows; i++) {
    // iterate through the columns of the grid
    for (int j = 0; j < cols; j++) {
      // display the character on the same line
      printf("#");
    }

    // change the position of the caret
    printf("\n");
  }
}

// our main function
int main(int argc, char *argv[]) {
  // declare variables that will hold the rows and columns of grid
  int grid_rows;
  int grid_cols;

  // ask the user to enter number of rows
  printf("\nPlease Enter Number of Rows: ");
  scanf("%d", &grid_rows);

  // ask the user to enter number of columns
  printf("Please Enter Number of Columns: ");
  scanf("%d", &grid_cols);

  printf("\n");

  // call the function to display the grid
  display_grid(grid_rows, grid_cols);

  return 0;
}
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

```c
#include <stdio.h>

// function to display a grid with required size
void display_grid(int rows, int cols, int align_x, int align_y) {

  // iterate through the number of blank "align_y" rows
  for (int i = 0; i < align_y; i++) {
    // display a new line
    printf("\n");
  }

  // iterate through the rows of the grid
  for (int i = 0; i < rows; i++) {
    // iterate through the columns of grid ==> to print whitespaces
    for (int w = 0; w < align_x; w++) {
      // display the character on the same line
      printf(" ");
    }

    // iterate through the columns of the grid ==> to print characters
    for (int j = 0; j < cols; j++) {
      // display the character on the same line
      printf("#");
    }

    // change the position of the caret
    printf("\n");
  }

  // iterate through the number of blank "align_y" rows
  // INFO: doing this so that grid appears "centered"
  for (int i = 0; i < align_y; i++) {
    // display a new line
    printf("\n");
  }
}

// our main function
int main(int argc, char *argv[]) {
  // declare variables that will hold the rows and columns of grid
  int grid_rows;
  int grid_cols;
  // declare variable(s) that will hold the "size" / "width" of whitespace
  // NOTE: this is also going to determine how far we push down and to the right
  int alignment_x;
  int alignment_y;

  // ask the user to enter number of rows
  printf("\nPlease Enter Number of Rows: ");
  scanf("%d", &grid_rows);

  // ask the user to enter number of columns
  printf("Please Enter Number of Columns: ");
  scanf("%d", &grid_cols);

  // ask the user to enter number for the alignment ( x-axis )
  printf("Please Enter Number of Alignment ( X Position ): ");
  scanf("%d", &alignment_x);

  // ask the user to enter number for the alignment ( y-axis )
  printf("Please Enter Number of Alignment ( Y Position ): ");
  scanf("%d", &alignment_y);

  printf("\n");

  // call the function to display the grid
  display_grid(grid_rows, grid_cols, alignment_x, alignment_y);

  return 0;
}
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

```c
#include <stdio.h>

// function to display "left sided" right-angled triangle
void display_triangle_left(int num_of_rows) {
  // // iterate trough the amount of rows
  for (int rows = 0; rows < num_of_rows; rows++) {
    // iterate through the number of columns
    for (int cols = 0; cols <= rows; cols++) {
      printf("#");
    }

    // change the line / caret's position
    printf("\n");
  }
}

// our main function
int main(int argc, char *argv[]) {
  // declare variable that is going to hold the number of rows
  int num_of_rows;

  // ask the user to enter the number of rows
  printf("\nPlease Enter Number Of Rows: ");
  scanf("%d", &num_of_rows);

  printf("\n");

  // call the function to display the "left sided" right-angled triangle
  display_triangle_left(num_of_rows);

  return 0;
}
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

```c
#include <stdio.h>

// function to display "left sided" right-angled triangle
void display_triangle_left(int num_of_rows) {
  // // iterate trough the amount of rows
  for (int rows = 0; rows <= num_of_rows; rows++) {
    // iterate through the number of columns
    for (int cols = num_of_rows; cols > rows; cols--) {
      printf("#");
    }

    // change the line / caret's position
    printf("\n");
  }
}

// our main function
int main(int argc, char *argv[]) {
  // declare variable that is going to hold the number of rows
  int num_of_rows;

  // ask the user to enter the number of rows
  printf("\nPlease Enter Number Of Rows: ");
  scanf("%d", &num_of_rows);

  printf("\n");

  // call the function to display the "left sided" right-angled triangle
  display_triangle_left(num_of_rows);

  return 0;
}
```

- Again, this is the output that we get when using the `num_of_row` with a value of 5

```console
#####
####
###
##
#
```

## Triangle Starting From Right

> [!NOTE]
> This was made entirely in C.

```c
#include <stdio.h>

// function to display "right sided" right-angled triangle
void display_triangle_right(int num_of_rows) {
  // // iterate trough the amount of rows
  for (int rows = 0; rows < num_of_rows; rows++) {
    // iterate through the number of columns ==> to print whitespaces
    for (int cols = num_of_rows - 1; cols > rows; cols--) {
      printf(" ");
    }

    // iterate through the number of columns ==> to print characters
    for (int chars = 0; chars < rows + 1; chars++) {
      printf("#");
    }

    // change the line / caret's position
    printf("\n");
  }
}

// our main function
int main(int argc, char *argv[]) {
  // declare variable that is going to hold the number of rows
  int num_of_rows;

  // ask the user to enter the number of rows
  printf("\nPlease Enter Number Of Rows: ");
  scanf("%d", &num_of_rows);

  printf("\n");

  // call the function to display the "right sided" right-angled triangle
  display_triangle_right(num_of_rows);

  return 0;
}
```

> [!NOTE]
> This was an adaptation from our [[Python - Grids and Pyramids#Triangle Starting Right | Python code]].

> The `main` function is the same, just the `for` loop inside the *displaying* function is different.

```c
// function to display "left sided" right-angled triangle
void display_triangle_left(int num_of_rows) {
  // // iterate trough the amount of rows
  for (int rows = 0; rows < num_of_rows; rows++) {
    // iterate through the number of columns ==> to print whitespaces
    for (int cols = rows; cols < num_of_rows - 1; cols++) {
      printf(" ");
    }

    // iterate through the number of columns ==> to print characters
    for (int chars = 0; chars < rows + 1; chars++) {
      printf("#");
    }

    // change the line / caret's position
    printf("\n");
  }
}


```

Again, using the value of 5 for `num_of_rows` for both of these code found above, we are going to see and output that looks like this.

```console
    #
   ##
  ###
 ####
#####
```


### Same Triangle But Upside Down

> Again, our `main` program is the same!

```c
// function to display "right sided" right-angled triangle
void display_triangle_right(int num_of_rows) {
  // // iterate trough the amount of rows
  for (int rows = 0; rows < num_of_rows; rows++) {
    // iterate through the number of columns ==> to print whitespaces
    for (int chars = num_of_rows; chars > rows; chars--) {
      printf("#");
    }

    // change the line / caret's position
    printf("\n");
  }
}
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

```c
// function to display lower half ( left-side ) of triangle
void display_triangle_left(int num_of_rows) {
  // iterate through the number of rows ==> lower half
  for (int rows = num_of_rows; rows > 0; rows--) {
    // iterate through the number of columns ==> to print lower left corner
    // whitespaces
    for (int cols = 0; cols < num_of_rows - rows; cols++) {
      printf(" ");
    }

    // iterate through the number of columns ==> to print lower left corner
    // characters
    for (int chars = 0; chars < rows; chars++) {
      printf("#");
    }

    // change the line / caret's position
    printf("\n");
  }
}
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

```c
#include <stdio.h>

// function to display a pyramid
void display_pyramid(int num_of_rows) {
  // iterate through the number of rows
  for (int rows = 0; rows < num_of_rows; rows++) {
    // iterate through the number of columns ==> to print left corner
    // whitespaces
    for (int cols = num_of_rows - 1; cols > rows; cols--) {
      printf(" ");
    }

    // iterate through the number of columns ==> to print left corner characters
    for (int chars = 0; chars < rows + 1; chars++) {
      printf("#");
    }

    // iterate through the number of columns ==> to print right corner
    // whitespaces
    for (int chars = 0; chars < rows; chars++) {
      printf("#");
    }

    // change the line / caret's position
    printf("\n");
  }
}

// our main function
int main(int argc, char *argv[]) {
  // declare variable that is going to hold the number of rows
  int num_of_rows;

  // ask the user to enter the number of rows
  printf("\nPlease Enter Number Of Rows: ");
  scanf("%d", &num_of_rows);

  printf("\n");

  // call the function to display the diamond
  display_pyramid(num_of_rows);

  return 0;
}
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

```c
// function to display a pyramid
void display_pyramid(int num_of_rows, int align_x, int align_y) {
  // iterate through the number of 'align_y' to print blank spaces
  for (int i = 0; i < align_y; i++) {
    printf("\n");
  }

  // iterate through the number of rows
  for (int rows = 0; rows < num_of_rows; rows++) {
    // iterate through the number of 'align_x' to print blank spaces
    for (int i = 0; i < align_x; i++) {
      printf(" ");
    }

    // iterate through the number of columns ==> to print left corner
    // whitespaces
    for (int cols = num_of_rows - 1; cols > rows; cols--) {
      printf(" ");
    }

    // iterate through the number of columns ==> to print left corner characters
    for (int chars = 0; chars < rows + 1; chars++) {
      printf("#");
    }

    // iterate through the number of columns ==> to print right corner
    // whitespaces
    for (int chars = 0; chars < rows; chars++) {
      printf("#");
    }

    // change the line / caret's position
    printf("\n");
  }

  // iterate through the number of 'align_y' to print blank spaces again
  for (int i = 0; i < align_y; i++) {
    printf("\n");
  }
}
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

# Display A Diamond

```c
#include <stdio.h>

// function to display a diamond
void display_diamond(int num_of_rows) {
  // iterate through the number of rows ==> upper half
  for (int rows = 0; rows < num_of_rows; rows++) {
    // iterate through the number of columns ==> to print upper left corner
    // whitespaces
    for (int cols = num_of_rows - 1; cols > rows; cols--) {
      printf(" ");
    }

    // iterate through the number of columns ==> to print upper left corner
    // characters
    for (int chars = 0; chars < rows + 1; chars++) {
      printf("#");
    }

    // iterate through the number of columns ==> to print upper right corner
    // whitespaces
    for (int chars = 0; chars < rows; chars++) {
      printf("#");
    }

    // change the line / caret's position
    printf("\n");
  }

  // iterate through the number of rows ==> lower half
  for (int rows = num_of_rows - 1; rows > 0; rows--) {
    // iterate through the number of colums ==> to print lower left corner
    // whitespaces
    for (int cols = 0; cols < num_of_rows - rows; cols++) {
      printf(" ");
    }

    // iterate through the number of colums ==> to print lower left corner
    // characters
    for (int chars = 0; chars < rows; chars++) {
      printf("#");
    }

    // iterate through the number of colums ==> to print lower right corner
    // characters
    for (int chars = num_of_rows - 1; chars > num_of_rows - rows; chars--) {
      printf("#");
    }

    // change the line / caret's position
    printf("\n");
  }
}

// our main function
int main(int argc, char *argv[]) {
  // declare variable that is going to hold the number of rows
  int num_of_rows;

  // ask the user to enter the number of rows
  printf("\nPlease Enter Number Of Rows: ");
  scanf("%d", &num_of_rows);

  printf("\n");

  // call the function to display the diamond
  display_diamond(num_of_rows);

  return 0;
}
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

```c
// function to display a diamond
void display_diamond(int num_of_rows, int align_x, int align_y) {
  // iterate through the number of 'align_y' to print blank spaces
  for (int i = 0; i < align_y; i++) {
    printf("\n");
  }

  // iterate through the number of rows ==> upper half
  for (int rows = 0; rows < num_of_rows; rows++) {
    // iterate through the number of 'align_x' to print blank spaces
    for (int i = 0; i < align_x; i++) {
      printf(" ");
    }

    // iterate through the number of columns ==> to print upper left corner
    // whitespaces
    for (int cols = num_of_rows - 1; cols > rows; cols--) {
      printf(" ");
    }

    // iterate through the number of columns ==> to print upper left corner
    // characters
    for (int chars = 0; chars < rows + 1; chars++) {
      printf("#");
    }

    // iterate through the number of columns ==> to print upper right corner
    // whitespaces
    for (int chars = 0; chars < rows; chars++) {
      printf("#");
    }

    // change the line / caret's position
    printf("\n");
  }

  // iterate through the number of rows ==> lower half
  for (int rows = num_of_rows - 1; rows > 0; rows--) {
    // iterate through the number of 'align_x' to print blank spaces
    for (int i = 0; i < align_x; i++) {
      printf(" ");
    }

    // iterate through the number of colums ==> to print lower left corner
    // whitespaces
    for (int cols = 0; cols < num_of_rows - rows; cols++) {
      printf(" ");
    }

    // iterate through the number of colums ==> to print lower left corner
    // characters
    for (int chars = 0; chars < rows; chars++) {
      printf("#");
    }

    // iterate through the number of colums ==> to print lower right corner
    // characters
    for (int chars = num_of_rows - 1; chars > num_of_rows - rows; chars--) {
      printf("#");
    }

    // change the line / caret's position
    printf("\n");
  }

  // iterate through the number of 'align_y' to print blank spaces
  for (int i = 0; i < align_y; i++) {
    printf("\n");
  }
}
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