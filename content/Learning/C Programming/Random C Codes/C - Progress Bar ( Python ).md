---
id: C - Progress Bar ( Python )
aliases: Progress Bars in C ( emulating Python Code )
tags:
  - C
  - python
author: S.Sunhaloo
date: 2025-05-04
status: Completed
---

# Simple Implementation of Progress Bar in C

Now, that we know how the **logic** of the *Progress Bar* code from first making it in [[Python - Progress Bars ( Without Modules )#Updated Iteration 2 - With Percentage Counter | Python]]. I am now going to implement it in C!

## The Print Function

> "*Well, Well, Well, Let's 'C' this*!"

Given this simple function written in Python:

```python
def display_bar(char_amount: int = 50):
    print("\n" + "-" * char_amount, "\n")
```

Running this function will output something like this:

```console

-------------------------------------------------- 

```

> [!WARNING] Butt ))💨
> <p align="center"> <span style="color: orange;"> We Cannot Do That in C!</span> </p>

Therefore, the line of code found in the function `progress_bar`:

```python
print(f"\r[{bar}] {percentage:0.2f}%", end="\r")
```

We simply **cannot** perform this operation in C!

### The Mighty `for` Loop!

> Fear Not! The mighty `for` loop will definitely save our asses.

Well, this is just a case of converting Python's *Syntactic-Sugar* into a "*normal*" thing that every programming language can do even if you don't understand the language as much!

```C
void display_bar() {
    // NOTE: default values are not a thing in C!
    int char_amount = 50;

    printf("\n");

    for (int i = 0; i < char_amount; i++) {
        printf("-");
    }

    printf("\n");
}
```

> We go from '2' lines of code to '12' lines of code!

Therefore, running this `display_bar()` in the `main()` function and compiling, we should get the **same** as above $\uparrow$:

```console

--------------------------------------------------

```

> [!WARNING] The Bar's Width!
> We **need** to make the `bar_width` variable here!
>
> Compared to the code:
>
> ```python
> draw_bar = (progress_char * int(percentage)) + (
> 	incomplete_char - (100 - int(percentage))
> )
> ```
>
> In this case, this means that we *iterate* through that '100 %' itself... *If you know what I am trying to say*.
>
> But when we are going to implement this in C; we need to use the [[Python - Progress Bars ( Without Modules )#My Spin on NeuralNine's Code | code]] where we can change the `bar_width`.

# Let's Get Started!

## Python Progress Bar Function Implemented in C

```C
// our progress bar function
void progress_bar(float progress, float total) {
    // variable to hold "filling up" character
    char progress_char = '#';
    // variable to hold "incomplete" character
    char incomplete_char = ' ';

    // calculate the percentage
    float percentage = ( progress / total ) * 100;

    // integer variable that will hold the "total size" of the progress bar
    int bar_width = 100;

    // calculate the number of characters to fill progress bar
    int char_fill_length = (int) (( progress / total ) * bar_width);
    // calculate the number of "white-spaces"
    int char_remain_length = bar_width - char_fill_length;

    // start displaying the progress bar
    printf("\r[");

    // display the characters being fill up
    for (int i = 0; i < char_fill_length; i++) {
        // output the amount of characters
        printf("%c", progress_char);
    }

    // display the "white-spaces" being removed
    for (int i = 0; i < char_remain_length; i++) {
        // remove the amount of 'white-space' characters
        printf("%c", incomplete_char);
    }

    // display the percentage at the end
    printf("] %0.2f %%\r", percentage);

    // display the progress bar by flushing the stream buffer
    fflush(stdout);
}
```

> Well, there we have it!

### Running the Function

```C
#include <stdio.h>

// our factorial function
int my_factorial(int input_num) {
    if (input_num == 1 || input_num == 0) {
        return 1;
    }
    else {
        return input_num * my_factorial(input_num - 1);
    }
}

// our progress bar function
void progress_bar(float progress, float total) {
    // variable to hold "filling up" character
    char progress_char = '#';
    // variable to hold "incomplete" character
    char incomplete_char = ' ';

    // calculate the percentage
    float percentage = ( progress / total ) * 100;

    // integer variable that will hold the "total size" of the progress bar
    int bar_width = 100;

    // calculate the number of characters to fill progress bar
    int char_fill_length = (int) (( progress / total ) * bar_width);
    // calculate the number of "white-spaces"
    int char_remain_length = bar_width - char_fill_length;

    // start displaying the progress bar
    printf("\r[");

    // display the characters being fille up
    for (int i = 0; i < char_fill_length; i++) {
        // output the amount of characters
        printf("%c", progress_char);
    }

    // display the "white-spaces" being removed
    for (int i = 0; i < char_remain_length; i++) {
        // remove the amount of 'white-space' characters
        printf("%c", incomplete_char);
    }

    // display the percentage at the end
    printf("] %0.2f %%\r", percentage);

    // display the progress bar by flushing the stream buffer
    fflush(stdout);
}

int main(int argc, char *argv[]) {
    // variable that will hold number of iterations
    long int iterations = 20000;

    // declare and initialise sum variables
    int sum_in = 0;
    int sum_out = 0;

    // initialise our progress bar
    progress_bar(0, iterations);

    // iterate through the number of iterations
    for (int i = 0; i <= iterations; i++) {
        // find ways to slow down the program
        if (i % iterations == 0) {
            // increment the sum variable
            sum_in = sum_in + ( i * 50 );
        }

        // call the function 'my_factorial' to calculate factorial of numbers
        sum_out = sum_out + my_factorial(i);
        // update the progress bar
        progress_bar(i, iterations);
    }

    // display a new line at the end to provide a cleaner output
    printf("\n");

    return 0;
}
```

> [!NOTE]
> Do you a high number of `iterations`!
>
> Why because "*C Go Fast*!!!". Yes, if you use a really *low* ( *what is "low" anyways* ) number like '100'. That thing will just zoom straight pass you like lighting McQueen!
>
> > Kachow!
>

In *my* case... I should get some output that resembles like this:

```console
[####################################################################################################] 100.00 %
```

> [!INFO] Terminal and Font Size
> The `bar_width` variable here is **different** to the `bar_width` variable found in Python???
>
> Nevertheless, I was using the [Kitty](https://sw.kovidgoyal.net/kitty/) terminal emulator with a *monospaced* font with size '15.0'.
>
> Therefore, you need to **adjust** the `bar_width` variable for your desired length depending on your:
>
> - Monitor Size
> - Font Size
> - Font Family

---

> [!SUCCESS]
> Therefore, I can say that I know how to make a **basic** *Progress Bar* in Python and C; and you could say in pretty much every language ever as we do have the **logic** now!
>
> > [!NOTE] BTW
> > If you want to make the progress bar a bit smaller or bigger; just change the `bar_width` variable accordingly!
>
> Peace Out Motherfuckers!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!