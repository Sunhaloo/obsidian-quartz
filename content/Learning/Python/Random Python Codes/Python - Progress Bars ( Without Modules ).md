---
id: Python - Progress Bars ( Without Modules )
aliases: Progress Bars in Python ( without installing any modules )
tags:
  - python
author: S.Sunhaloo
date: 2025-05-04
status: Completed
---

> [!INFO] Back Story
> Back around 2023... I wanted to learn how to make a progress bar that will display, well progress of stuff. But I never really got to doing it.
>
> On the 29th of March 2025, I restarted my [[Vanilla Arch - Environment Learning Process ( 29-04-2025 ) | Arch Linux]] journey.
>
> Therefore, I want to make a **progress bar** in *Bash* to be able to display the total progress of my install script like:
>
> - total progress of downloading and installing applications
> - progress of git setup
> - progress of moving folders and files into each place
>
> But because I don't even know where to start, I told myself that I just want to learn it with Python first.
>
> > Hence, here I am!
>

# Completely Shit

Instead of searching for a video or the code straight away... I instead tried doing it myself.

## Iteration 1 - For Loops

So I tried using `for` loops with our trusty `range()` function.

```python
# display the starting "character" of progress bar
print("[", end="")

# iterate through a number
for i in range(10):
	# display the progress
	print("#", end="")

# display the ending "character" of progress bar
print("]", end="")

# change cursor / pointer to new line
print()
```

Well, this is going to output:

```console
[##########]
```

The thing about the `range()` function, its **counting** number... We **don't** want to *count* numbers, but instead do it in a *period of time*.

## Iteration 2 - For Loops with Sleep Function

Therefore, I know that from the 'time' module, we have the `time.sleep()` function, whereby we can *sleep* the program for a desired amount of time.

> [!NOTE]
> For the *imports*, I will **not** be including them in the code, just know that I am doing something like this:
>
> ```console
> from module_name import function_name
> ```
>
> For example, importing the `sleep()` function from 'time' module
>
> ```python
> from time import sleep
> ```

```python
from time import sleep
# variable to hold second to sleep
sleep_seconds: float = 0.2

# display the starting "character" of progress bar
print("[", end="")

# iterate through a number
for i in range(10):
	# display the progress by flushing the stream buffer thing
	# INFO: see 'https://docs.python.org/3/library/functions.html#print'
	print("#", end="", flush=True)

	# sleep the program for desired "length"
	sleep(sleep_seconds)

# display the ending "character" of progress bar
print("]", end="")

# change cursor / pointer to new line
print()
```

> Well, I **beg you to run** the code and see for yourself.
> Nevertheless, the output at the end should be like so

```console
[##########]
```

---

> [!INFO]
> Well what about things like the percentage counter?
> What about finding the take taken for a *job* to complete and display its progress and percentage?
>
> Because I did **not** think enough! I looked for a video so that I can get the *logic* of how to do this.

# The Logic

> [!INFO] Resources
> Link to YouTube video: https://www.youtube.com/watch?v=x1eaT88vJUA

The logic was a simple *percentage calculator*! I think we all know how to calculate the percentage of something.

> But if you don't!

$$percentage = \frac{value}{total} \times 100 \%$$

Now, I know the logic, I think we can improve the *codes* found above $\uparrow$!

## Updated Iteration 2 - With Percentage Counter

```python
    # variable to hold amount of iterations
    iterations_amount: int = 30
    # variable to hold second to sleep
    sleep_seconds: float = 0.1

    # iterate through number of iterations
    for i in range(iterations_amount + 1):
        # calculate the percentage
        percentage = (i / iterations_amount) * 100

        # display the progress bar by flushing the stream buffer thing
        print(f"\r[{'#' * int(percentage)}] {percentage:.2f} %", end="\r")

        # sleep the program for desired "length"
        sleep(sleep_seconds)

    # change cursor / pointer to new line
    print()
```

> Again, do run the code by yourself

```console
[###################################################################################] 83.3
[######################################################################################] 8
[#########################################################################################
[#########################################################################################
[#########################################################################################
[#########################################################################################
###########] 100.00 %
```

> Well, this is **completely shit**. But we **do** have or *percentage counter*!

> [!NOTE] Problems, Problems, Problems
> As you can, see its **not** become like in Linux where you have something like this:
>
> ```console
> [##################################] 100%
> ```
>
> With '[[#Iteration 1 - For Loops]]', it just simply output **everything** $\Rightarrow$ "*Completely Shit*"
>
> Then with '[[#Iteration 2 - For Loops with Sleep Function]]' it does *progress* nevertheless, it increment and the progress bar **size** changes dynamically as *progress* increases. Additionally, it does **not** have a *percentage counter*.
>
> Will '[[#Updated Iteration 2 - With Percentage Counter]]', it does **have** a *percentage counter*, but lacks the **fixed** progress bar **size**.
>
> > [!INFO] What We Want!
> > - Fixed Size ( *be it length of 'display' or like in Linux* )
> > - Progress fills up *empty* space in progress bar
> > - '*Percentage Counter*' to keep track of progress

# Good Versions

> What is the meaning of "*good*" anyways?

## Corrected "Updated" Iteration 2

> [!WARNING]
> When running the code as from here.
>
> <p align="center"> <br> <span style="color:orange;"> Make Sure To Use Small Font :CoTriangleWarning:</span> </p>

```python
# variable to hold amount of iterations
iterations_amount: int = 30
# variable to hold second to sleep
sleep_seconds: float = 0.1

# iterate through number of iterations
# NOTE: use `iterations_amount + 1` to go to 100%
for i in range(iterations_amount + 1):
	# variable to hold "filling up" character
	progress_char: str = "#"
	# variable to hold "incomplete" character
	incomplete_char: str = " "

	# calculate the percentage
	percentage = (i / iterations_amount) * 100

	# draw the progress bar first
	progress_bar = (progress_char * int(percentage)) + (
		incomplete_char * (100 - int(percentage))
	)

	# display the progress bar by flushing the stream buffer thing
	print(f"\r[{progress_bar}] {percentage:.2f} %", end="\r")

	# sleep the program for desired "length"
	sleep(sleep_seconds)

# change cursor / pointer to new line
print()
```

> Again and again... Do run the code

```console
[####################################################################################################] 100.00 %
```

In this case, it does do what we tell it to do ( *to do do do do... Lots of do's* )

> Check this line ( *of code* ) out:

```python
# draw the progress bar first
progress_bar = (progress_char * int(percentage)) + (incomplete_char * (100 - int(percentage)))
```

In this case, we are saying to output `progress_char` ( *which is `#`* ) for `percentage` amount and output `incomplete_char` ( *which is just ` `* ) for `100 - int(percentage)`

We know that we calculated the **percentage** with this:

```python
# calculate the percentage
percentage = (i / iterations_amount) * 100
```

Initially, the *value* of `i` will be '**0**'; therefore $percentage = \frac{0}{30} \times 100 \%$ which is going to equal to '**0**'!

Hence, our `progress_bar` will contain **zero** `#` and `100 - int(percentage)` $\Rightarrow 100 - 0 = 100$ ` ` characters.

After each iteration as `i` **increases**, the `percentage` increases. Thus, we know that the number of `#` will **increase** and ` ` will **decrease**!

# NeuralNine's Code

> "*Its so simple to be happy but so difficult to be simple*!"

## Progress Bar Function

Here is how [NeuralNine](https://www.youtube.com/c/NeuralNine) made the function!

```python
# our progress bar function
def progress_bar(progress: int, total: float):
    # variable to hold "filling up" character
    progress_char: str = "#"
    # variable to hold "incomplete" character
    incomplete_char: str = " "

    # calculate the percentage
    percentage: float = (progress / total) * 100

    # draw the progress bar ( using same logic )
    draw_bar = (progress_char * int(percentage)) + (
        incomplete_char * (100 - int(percentage))
    )

    # display the bar on screen
    print(f"\r[{draw_bar}] {percentage:.2f}%", end="\r")
```

> Simple as that!

### Running the Function

Here, you will find an example code on how you can use the `progress_bar()` function!

```python
# import the 'randint' function from the random module
from random import randint

# import the 'factorial' function from the math module
from math import factorial

# import the 'time' function from the time module
from time import time


# our progress bar function
def progress_bar(progress: int, total: float):
    # variable to hold "filling up" character
    progress_char: str = "#"
    # variable to hold "incomplete" character
    incomplete_char: str = " "

    # calculate the percentage
    percentage: float = (progress / total) * 100

    # draw the progress bar ( using same logic )
    draw_bar = (progress_char * int(percentage)) + (
        incomplete_char * (100 - int(percentage))
    )

    # display the bar on screen
    print(f"\r[{draw_bar}] {percentage:.2f}%", end="\r")


# our main function
def main():
    # varaible to hold number of iterations
    iterations_amount: int = 9999

    # declare and initialise sum variables
    sum_in: int = 0
    sum_out: int = 0

    # call function for progress bar and initialise
    progress_bar(0, iterations_amount)

    # variable hold the start time of program ( for performance )
    start_time = time()

    # iterate through amount of iterations
    # NOTE: use `iterations_amount + 1` to go to 100%
    for i in range(iterations_amount + 1):
        # start making ways to slow down the code
        if i % iterations_amount == 0:
            # increment the sum with random power
            sum_in += pow(i, randint(0, 9))

        # increment the sum varaible with "things"
        sum_out *= factorial(i)

        # update the progress bar
        progress_bar(i, iterations_amount)

    # variable hold the end time of program ( for performance )
    end_time = time()

    # calculate and display the elapsed time
    print(f"\n\nElapsed Time: {(end_time - start_time):.2f} Second(s) <---")


# source the main function
if __name__ == "__main__":
    main()
```

In my case, I get the output of:

```console
[####################################################################################################] 100.00%

Elapsed Time: 9.62 Second <---
```

## My Spin on NeuralNine's Code

> More like [Gemini's Code](https://gemini.google.com)

You know how when you do a full system update with something like `sudo pacman -Syy; sudo pacman -Syu`.

> <p style="color: #1792CF; font-family: 'MonaspiceRn Nerd Font';"> I use Arch BTW!!!</p>

You are going to see that the initially the progress bar are off to the right side of the screen taking up **minimal** space.

> *So how can we do that?*... **By adding a Bar Width**!

```python
# our updated progress bar function ( with bar size )
def progress_bar(progress: int, total: float):
    # variable to hold "filling up" character
    progress_char: str = "#"
    # variable to hold "incomplete" character
    incomplete_char: str = " "

    # integer variable that will hold "total size" of progress bar
    bar_width: int = 50

    # calculate the percentage
    percentage: float = (progress / total) * 100

    # calculate the number of character to fill progress bar
    char_fill_length = int((progress / total) * bar_width)
    # calculate the number of "white-space"
    char_remain_length = bar_width - char_fill_length

    # draw the progress bar ( using same logic )
    draw_bar = (progress_char * char_fill_length) + (
        incomplete_char * char_remain_length
    )

    # display the bar on screen
    print(f"\r[{draw_bar}] {percentage:.2f}%", end="\r")
```

We added 3 more lines of code:

```python
# integer variable that will hold "total size" of progress bar
bar_width: int = 50

# calculate the number of character to fill progress bar
char_fill_length = int((progress / total) * bar_width)
# calculate the number of "white-space"
char_remain_length = bar_width - char_fill_length
```

Initially, we were only doing this;

```python
# draw the progress bar ( using same logic )
draw_bar = (progress_char * int(percentage)) + (
	incomplete_char * (100 - int(percentage))
)
```

As explained above $\uparrow$... Its going to, *with iterations / time*, increment the number of character to output and decrement the number of *white-space*.

But now, we have the bar function... We **need** to convert the *amount / progress* to conform with the desired **bar length**!

This is done with something like this:

$$Filled \ Amount = \frac{Progress}{Total} \times Bar's \ Width$$

In this case, we know that [all the time](https://www.youtube.com/watch?v=7hyNoSz-UvM&t=60s) the **initial** *total length* of the progress bar is going to be '100'. Therefore we need to find the number of character to fit into the updated bar's width so that it carries over.

> [!TIP] Improvement and Optimisation
> Actually Gemini gave me this code:
>
> ```python
> # integer variable that will hold "total size" of progress bar
> bar_width: int = 50
>
> # calculate the number of character to fill progress bar
> char_fill_length = int((percentage / 100) * bar_width)
>
> # calculate the number of "white-space"
> char_remain_length = bar_width - char_fill_length
> ```
>
> Now, let me explain ( _I need to defend myself like my life depends on it; because I tell people that I use AI to learn and **not** copy! :LiSkull:_ ). Yesterday ( *so 03/05/2025* ), I learned the 'NeuralNine' code... Like I have said... I need to learn actually how to make it in Bash and **not** Python... But as I was learning it and proficient enough in Python.
>
> I thought that: "*Yeah, let's do it in Python first!*".. Then in the morning ( *currently @22:36* ), I tried doing it in C.
>
> Now because we cannot do things like `print('-' * 50)` in C and we need to actually use a `for` loop. I learned from Gemini that we need to create the "`bar_width`" to make things happen...
>
> > You can find the 'C' version for this Progress Bar in the note / file '[[C - Progress Bar ( Python )]]'.
>
> I then tried converting the C code into Python whereby, I realised that we can change the length of the **entire** progress bar.
>
> Long story short... I realised that instead of doing $\frac{percentage}{100} \times bar's \ width$. We could simply do $\frac{progress}{total} \times bar's \ width$.
>
> I then asked Gemini to check if this so called "**optimisation**" would actually benefit the code; it gave me this code to run and check:
>
> ```python
> import timeit
>
>
> def calculate_filled_direct(progress, total, bar_width):
>    return int((progress / total) * bar_width)
>
>
> def calculate_filled_two_step(progress, total, bar_width):
>    percentage = (progress / total) * 100
>    return int((percentage / 100) * bar_width)
>
>
> progress_val = 50
> total_val = 100
> bar_width_val = 20
> num_runs = 1000000
>
> time_direct = timeit.timeit(
>    lambda: calculate_filled_direct(progress_val, total_val, bar_width_val),
>    number=num_runs,
> )
> time_two_step = timeit.timeit(
>    lambda: calculate_filled_two_step(progress_val, total_val, bar_width_val),
>    number=num_runs,
> )
>
> print(f"Time for direct calculation ({num_runs} runs): {time_direct:.6f} seconds")
> print(f"Time for two-step calculation ({num_runs} runs): {time_two_step:.6f} seconds")
> ```
>
> Running the above code block, we can see that **we have clearly optimised the code by a lot**!
>
> ```console
> Time for direct calculation (1000000 runs): 0.143641 seconds
> Time for two-step calculation (1000000 runs): 0.210460 seconds
> ```
>
> > [!WARNING] But Again
> > If you are really *optimising* things... <span style="color: orange;"> Then consider switch to a completely different language like C and Rust</span> !!!

### Updated Full Code

```python
# import the 'randint' function from the random module
from random import randint

# import the 'factorial' function from the math module
from math import factorial

# import the 'time' function from the time module
from time import time


# our updated progress bar function ( with bar size )
def progress_bar(progress: int, total: float):
    # variable to hold "filling up" character
    progress_char: str = "#"
    # variable to hold "incomplete" character
    incomplete_char: str = " "

    # integer variable that will hold "total size" of progress bar
    bar_width: int = 50

    # calculate the percentage
    percentage: float = (progress / total) * 100

    # calculate the number of character to fill progress bar
    char_fill_length = int((progress / total) * bar_width)
    # calculate the number of "white-space"
    char_remain_length = bar_width - char_fill_length

    # draw the progress bar ( using same logic )
    draw_bar = (progress_char * char_fill_length) + (
        incomplete_char * char_remain_length
    )

    # display the bar on screen
    print(f"\r Iterations: \t\t\t\t\t\t[{draw_bar}] {percentage:.2f}%", end="\r")


# our main function
def main():
    # varaible to hold number of iterations
    iterations_amount: int = 9999

    # declare and initialise sum variables
    sum_in: int = 0
    sum_out: int = 0

    # call function for progress bar and initialise
    progress_bar(0, iterations_amount)

    # variable hold the start time of program ( for performance )
    start_time = time()

    # iterate through amount of iterations
    # NOTE: use `iterations_amount + 1` to go to 100%
    for i in range(iterations_amount + 1):
        # start making ways to slow down the code
        if i % iterations_amount == 0:
            # increment the sum with random power
            sum_in += pow(i, randint(0, 9))

        # increment the sum varaible with "things"
        sum_out *= factorial(i)

        # update the progress bar
        progress_bar(i, iterations_amount)

    # variable hold the end time of program ( for performance )
    end_time = time()

    # calculate and display the elapsed time
    print(f"\n\nElapsed Time: {(end_time - start_time):.2f} Second(s) <---")


# source the main function
if __name__ == "__main__":
    main()
```

Therefore, we should see that the progress bar's width has decreased and we have a description for the progress bar to the side of it:

```console
 Iterations:                                            [##################################################] 100.00%

Elapsed Time: 9.51 Second(s) <---
```

Well, again from a calculation point-of-view... We know that `int(9999/2)` is going to give us '4999'.

This means that when the `i` reaches that number, we should see that we have 50 *filled characters* and 50 *white-spaces* for a **100 bar's width** progress bar!

Well, is the half-way point for the same *value* by with the **50 bar's width**?

Therefore the "*Filled Characters Amount*" for a bar's width of **50** is:

$$Filled \ Amount = \frac{4999}{9999} \times 50 \approx 24.9974$$

This means for a **bar's width** of '50'... There is going to be '25' *filled characters* and '25' *white-spaces*!

> **Obvious-Fuckingly**

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!