---
id: Prime Number Analysis
aliases: Prime Number Checking and Generation
tags:
  - C
  - python
  - theory
author: S.Sunhaloo
date: 2025-05-20
status: HOLD
---

## List of Contents

- [[#What is a Prime Number?]]
- [[#Algorithms for Prime Number]]
	- [[#Primality Testing Algorithms]]
		- [[#Types of Primality Tests]]
	- [[#Prime Generation Algorithms]]
		- [[#Types of Prime Generation Algorithms]]
	- [[#Implementation of These Algorithms]]
		- [[#Python]]
			- [[#Python Boilerplate]]
		- [[#C Language]]
			- [[#The Actual C Boilerplate Code | C Boilerplate]]

---

> [!WARNING] To be removed
> 0. **Simple trial division** (from 2 to _n_)  
> 1. **√n trial division** (verify the simplest factor-test)  
> 2. **Basic Sieve of Eratosthenes** (list primes up to _N_)  
> 3. **Wheel optimisation** (apply to both trial-division and sieve)  
> 4. **Segmented sieve** (handle very large _N_ with limited RAM)  
> 5. **Miller–Rabin** (fast probabilistic primality test)  
> 6. **Deterministic Miller–Rabin** (guaranteed correctness for _n_ < 2⁶⁴)  

# What is a Prime Number?

From the [Wikipedia](https://en.wikipedia.org/wiki/Prime_number), we know that a **Prime Number** is a [natural number](https://en.wikipedia.org/wiki/Natural_number) is **greater** than '1' and **not** a *product* of '2' smaller numbers.

> [!INFO] What is the **Opposite** of a Prime Number?
> The *opposite* of a Prime Number is called a '**[Composite Number](https://en.wikipedia.org/wiki/Composite_number)**'!
>
> This means that a Composite number is a **positive integer number** that is **greater** than '1' and is a *product* of '2' smaller numbers!

> [!TIP] Therefore, we can say that
> > $n$ is **prime** if $n$ is **greater** than $1$ and numbers from $2$ to $n - 1$ **must have** *remainders*.
>
> > [!NOTE]- Pay close attention to $n - 1$!
> > We all know that '$2$' is a **prime number**. But what if instead of dividing from '$n - 1$'; we divided to '$n$'?
> >
> > Well, you are going to make '$2$' become a *composite* number. As $\frac{2}{2} = 1$
> > This is why we need to *stop* **before** the value of '$n$'!
>

## Example of Prime and Composite Numbers

An example of a **Prime Number** would be $5$ as we can see its **only** made up of $1$ and $5$:

$$
5 = 1 \times 5 \ \longleftrightarrow \ 5 = 5 \times 1
$$

Whereas an example of a **Composite Number** would be something like $12$ whereby its made up of:

$$
12 = 1 \times 2 \times 2 \times 3
$$

> From this $\uparrow$, we can say that; every number **greater** than 1 is either *prime* or can be **factorised** as a *product of primes*.

Further breakdown of the number '$12$' would be:

- $12 = 1 \times 12 \ \longleftrightarrow \ 12 = 12 \times 1$
- $12 = 2 \times 6 \ \longleftrightarrow \ 12 = 6 \times 2$
- $12 = 3 \times 4 \ \longleftrightarrow \ 12 = 4 \times 3$

> [!TIP] Some General Tips
> - **No** *even numbers* **greater** than '$2$' is prime
> 	- As that *even* number, $n$, can be expressed as $2 \times \frac{n}{2}$
> - Every prime number other than '$2$' is **odd** $\Rightarrow$ "*Odd Prime*"
> - *Prime numbers* **greater** than '$5$' ends in $1, 5, 7, 9$
> - *Composite numbers* ends with other digits $\Rightarrow 0, 2, 3, 4, 5, 6, 8$
> - *Decimal Numbers* ending with '$0$' or $5$ are **divisible** by $5$
> - Set of **all primes** is denoted by:
> 	- Either '$\mathbf{P}$' or '$\mathbb{P}$'

> [!WARNING] Why is '$1$' <span style="color: red;"> Not</span> a Prime Number?
> This is because of the *history* of it and because of its *characteristics*... '$1$' is considered as a [unit](https://en.wikipedia.org/wiki/Unit_(ring_theory))!
>
> > That pesky "*unit*" thing is beyond my understanding!
>
> **Before** the *Renaissance* and *Middle Ages*; mathematicians did **not** consider '1' to be a number!
>
> > Yes, they did **not** think that '0' and '1' as actual numbers 🤯!

---

# Algorithms for Prime Number

> Onto the spicy parts!

There are 2 main types of *algorithms* for Prime Numbers, they are called:

1. Primality Testing Algorithms
2. Prime Generation Algorithms

Looking at the *second* one you can see that we are going to look at algorithms that will be **generating** a list of *prime numbers*. But what about the *first* one?

The *first* one is about **checking** if a number, '$n$', is either **prime** or **composite**.

## Primality Testing Algorithms

### What is Primality Testing?

All **prime numbers** share a property called '*Primality*', which means they are **only** *divisible* by **1** and **themselves**.

**Primality Testing** is the process of checking whether a given number, $n$, is **prime** or **composite**.

This is a fundamental task in number theory and has real-world applications in *cryptography*, *random number generation*, and *computer security*.

#### Why it matters:

Prime numbers are essential in:
- 'RSA' encryption and other public-key cryptography
- Hashing algorithms
- Random number generation
- Procedural content generation ( *chunk generation like in [Minecraft](https://en.wikipedia.org/wiki/Minecraft_(franchise))* )

#### What makes it challenging:

As numbers get **larger** ( *hundreds or thousands of digits* ), checking for primality becomes increasingly *computationally expensive*.  
Efficient algorithms are crucial to handle large inputs, especially in real-world systems like *secure messaging* and *digital signatures*.

#### Types of Primality Tests:

- Deterministic Tests $\Rightarrow$ **Always** return the *correct result*.
- Examples:
  - Trial Division Algorithms
  - AKS Primality Test
  - Deterministic Miller–Rabin ( *for $n < 2^{64}$* )

- Probabilistic Tests $\Rightarrow$ **Extremely fast**, but have a ( *very small* ) chance of *error* $\Rightarrow$ "*Erroneous*".
- Examples:
  - Fermat Test
  - Miller–Rabin ( *'Probabilistic' version* )
  - Baillie–PSW

> [!INFO] When to use which?
> The '*Probabilistic*' Test's Algorithms are the now that are usually use in **real-world** scenarios.
>
> Even if they do have a ( *small* ) chance of producing and error; they are still preferred due to to their extreme rapidity!
>
> Nevertheless, if are creating the "*next big thing*" and you need to **guarantee 100% accuracy**. Go with the *Deterministic* route!

---

## Prime Generation Algorithms

As the name suggests, **prime generation** is the process of *creating a list of prime numbers* up to a given number, $n$ ( *'threshold' / 'upper bound' if you prefer* ).

This is different from '[[#What is Primality Testing? | Primality Testing]]', which checks if a **single** number, $n$ is prime or not. Prime generation produces **all primes** in a range typically from 2 to $n$.

### Types of Prime Generation Algorithms

- Naive trial-division for each number
  - Very slow; checks each number up to $n$ individually.
- Sieve of Eratosthenes
  - Classic and practical sieve; efficient up to $10^9$.

- Wheel-optimised sieve
  - Skips multiples of small primes (e.g. 2, 3, 5); improves speed and memory.
- Segmented Sieve of Eratosthenes
  - Divides the range into chunks; good for generating primes up to $10^{12}$+.
- FFT-based sieves (theoretical)
  - Uses number-theoretic transforms; mostly academic or used in massive-scale computations.

---

# Implementation of These Algorithms

I will now try and learn how to implement these algorithms! But before we start, there are some few information that I am going to give out about.

## Specifications

- CPU: Intel(R) Core(TM) i5-8500T (6) @ 3.50 GHz
- GPU: NVIDIA GeForce GTX 1650 [Discrete]
- Memory:
	- Memory Size: 16 GB ( Single Stick )
	- Memory Speed: 3200 MT/s
	- Swap: Disabled / 0 GB
- Operating System: Arch Linux
	- Kernel: Linux 6.14.4-arch1-1
- Terminal Emulator: kitty
- Shell: zsh
- Python Version: Python 3.13.3
- GCC Version: gcc (GCC) 14.2.1 20250207
- MAKE Version: make 4.4.1-2

## Python

### Python Boilerplate

This is the *boilerplate code* that I am going to be using:

```python
# our imports
from time import perf_counter
from math import sqrt


# function description
def func_name():
    # code goes here
    pass


# our main function
def main():
    # call the function `func_name()`
    func_name()


# source the main function
if __name__ == "__main__":
    # initialise sum / total variable
    sum_times = 0

    # run the main function 10 times
    for iterations in range(10):
        # start time for performance measurement
        start_time = perf_counter()

        # call and run the actual main function
        main()

        # end time for performance measurement
        end_time = perf_counter()

        # variable that will keep track of current elapsed time
        elapsed_time = end_time - start_time

        # increment the variable `sum_times` by the `elapsed_time`
        sum_times += elapsed_time

    # calculate and display the average times.
    print(
        "\n" + "-" * 50 + "\n",
        f"\n\t== Average Time: {(sum_times / 10):.8f} s <-- ==",
        "\n\n" + "-" * 50,
    )
```

Now, obviously when it comes to actually writing the code, I might need to import other things like `sqrt()` from the `math` module and others.

> Speaking of **modules**!

#### Importing Modules

We all know that the **Square Root** of $x$ where $x$ in this case; will be a **positive integer number** is going to be:

$$
\sqrt{x} = x^{\frac{1}{2}}
$$

Hence, there are 2 ways we can go about this in Python, either we use the `math.sqrt()` function or we use `**` ( *which stand for 'to the power of' in Python* ).

Thus, I want to check what type of performance that we get when using each of them

> [!NOTE]
> There should **not** be much difference between them!

##### Using `math.sqrt()`

Now, instead of importing the whole `math` module, we can simply import the specific `sqrt()` function only. Therefore, we don't need to load all of the other functions in memory

Using the *boilerplate code* found above $\uparrow$ and importing `sqrt()` function from that `math` module. Whereby we create a variable `x` which is going to be initialised with `sqrt(pow(9999, 77))`. In my case, I get these *timings*:

> [!WARNING]
> As you can see from the *boilerplate*; we are running the `main()` function **10 times** whereby we calculate the **average time** at the end and display *it*.
>
> The table below $\downarrow$ shows **individual average times**!
>
> To achieve **greater** statistical confidence and mitigate external factors results, we are going to **combine** each of these *averages* and then calculate, again, its average.

| Iteration | `import math` | `from math import sqrt` |
| --------- | ------------- | ----------------------- |
| 1 | 0.00000287 s | 0.00000587 s |
| 2 | 0.00000287 s | 0.00000286 s |
| 3 | 0.00000380 s | 0.00000248 s |
| 4 | 0.00000212 s | 0.00000281 s |
| 5 | 0.00000346 s | 0.00000332 s |
| Average Time | 0.00000302 s <-- | 0.00000347 s |

> [!SUCCESS] Using `from math import sqrt`!
> Like I said, there should **not** be much difference between the two *method* of doing `math.sqrt()` or `sqrt()`.
>
> Therefore, I am going to use the one that I like and what most considered to be "*more*" readable as we are only importing **one** function from that module.
>
> > [!WARNING] Specific to Computer
> > The timings are based on each computer system... What I am trying to say is that; my computer ran the codes in these *times* $\uparrow$ that does not mean that it will run about the same for you!
> >
> > > Let me give you an example!
> >
> > Running a simple `for` loop, from '0' to '1000000000' in Python on my **laptop** yield about '*81.xxx s*' while the **same** yields about '*5*' seconds!
> >
> > > "*That's massive*" [that's what she said](https://www.youtube.com/watch?v=dBUGfs9rwms)
> >
>

##### Difference between `sqrt()` and `**`

Let's see what's the difference between `sqrt()` and `** 0.5`. We are going to find the **square root** of `sys.float_info.max`

> [!TIP] I did not know this!
> This `sys.float_info.max` is the **largest finite float number** in Python!
>
> This means that we are going to be able to find the *square root* of this number successfully **without** any of those pesky `OverflowError`.

| Iteration | `from math import sqrt` | `float_info.max ** 0.5` |
| --------- | ------------- | ----------------------- |
| 1 | 0.00000071 s | 0.00000155 s |
| 2 | 0.00000116 s | 0.00000150 s |
| 3 | 0.00000119 s | 0.00000177 s |
| 4 | 0.00000099 s | 0.00000159 s |
| 5 | 0.00000102 s | 0.00000107 s |
| Average Time | 0.00000101 s <-- | 0.00000150 s |

> [!NOTE]
> I kept running the version that was using the `**` operator and it was *consistently* **slower** than using `sqrt()` function!
>
> Now, we know what we should be using to be able to squeeze as much performance out of our algorithms when using Python!


> [!BUG] Nevertheless
> If we are thinking too much about **optimisation** and other "*efficiency management*" *stuff*. Then, we should first ask the following question:
>
> <p align="center"> "<em> <strong> Should we use 'X' to code?</strong> </em> "</p>
>
> Yes, if we are thinking about optimisation and stuff, we should first consider the **programming language** we are going to be using...
>
> This is the reason why I, *even though I don't know shit and don't understand shit*... I like programming languages such as 'C' or 'Rust'!
>
> > Because they are really ziiiiiiiioooooooouuuuuuuummmmm!!!
>

> With that said... Let's get started!

---

## C Language

> You C, I like [[C Data View | C]]!

I am also going to implement all the algorithms that I am going to cover in C.

### C Boilerplate

Below, you are going to find the *boilerplate code* that I am going to be using:

#### Time Header and Performance Counter

> [!INFO] Resources
> - https://www.youtube.com/watch?v=Qoed2uBwF_o
> - https://www.youtube.com/watch?v=mSUChCEE-rs
>
> > [!NOTE] Man Pages!
> > In most [linux](https://en.wikipedia.org/wiki/Linux) or [unix](https://en.wikipedia.org/wiki/Unix) based system, we are going to have the `man` command.
> >
> > For example running the command `man man` will give you something like this:
> >
> > ```console
> > MAN(1)                  Manual pager utils                  MAN(1)
> >
> > NAME
> >       man - an interface to the system reference manuals
> >
> > SYNOPSIS
> >       man [man options] [[section] page ...] ...
> >       man -k [apropos options] regexp ...
> >       man -K [man options] [section] term ...
> >       man -f [whatis options] page ...
> >       man -l [man options] file ...
> >       man -w|-W [man options] page ...
> > ```
> >
> > What I am trying to say is that, I am not **smart** enough to just look at the *manpages* for `time.h` and understand it!
> >
> > This is the reason why I have included these awesome video. I hope that with time, patient, *head bashing*... I will be able to someday, read and understand the *manpages*.
>

```C

```

> [!WARNING] About Time!
> > Get it $\uparrow$... "*About Time*"
>
> So as you can see, we use use the `clock()` function to be able to measure the **elapsed time** of our `main()` function.
>
> Nevertheless, this is not really a good implementation of the `time.perf_counter()` function from *Python*.
>
> The difference comes when you have a lot of **inputs** and **outputs** in your program. The `clock()` function will <strong> <span style="color: red;"> not</span> </strong> take these into account.
>
> For example, let's say that the user took a 10 seconds to enter something... `time.perf_counter()` will take that *10 seconds* in **consideration** whereas the `clock()` or `time.time()` will **not**!
>
> > Additionally, I think there are is a difference between the `clock()` function on Windows compare to on Linux
> > Check this out: https://learn.microsoft.com/en-us/cpp/c-runtime-library/reference/clock?view=msvc-170&viewFallbackFrom=msvc-170
>

##### Gemini Code

After chatting with [Gemini](https://gemini.google.com) about the above problem, it gave me this function so that we can *emulate* the `time.perf_counter()` function from Python

```C
// function to emulate `time.perf_counter()` in Python ==> high resoultion monotonic clock
double perf_time_count() {
    // standard C struct to hold seconds and nanoseconds
    struct timespec time_ts;

    // call function `clock_gettime()` to get the current time-stamp
    // NOTE: the `clock_gettime()` function is versatile ==> we are going to pass `CLOCK_MONOTONIC`
    clock_gettime(CLOCK_MONOTONIC, &time_ts);

    // convert seconds and nano-seconds into "total" seconds
    // NOTE: '1e9' = 1 x 10^9, whereby 1 seconds = 1e9 nano-seconds
    return (double) time_ts.tv_sec + (double) time_ts.tv_nsec / 1e9;
}
```

###### "Explanation" of the Above Code

The code above first creates a *user-defined datatype* or `struct` with the variable name `time_ts`.

Then we are going to call the function `clock_gettime()` to get the **current timestamp** from `CLOCK_MONOTONIC`.

> What is `CLOCK_MONOTONIC`?

From the `man time.h`, we see that `CLOCK_MONTONIC` is described as:

```console
The  identifier for the system-wide monotonic clock,
which is defined as a  clock  measuring  real  time,
whose  value  cannot  be set via clock_settime() and
which cannot have negative clock jumps. The  maximum
possible clock jump shall be implementation-defined.
```

> [!WARNING] I **Don't** Know C Enough!
> I know that there are things called [pointers](https://www.youtube.com/watch?v=JFO_HLa0UMc).
>
> Whereby we are going to *point* to a specific **address** in memory ( *like the RAM* ) and access it for later use!
>
> Therefore, the symbol `&` is used to be able to access that **memory address**!
>
> > [!BUG] **Memory Address**
> > Yes, we **don't** get the *actual value* of that memory location. But instead we <span style="color: green;"> get</span> the **memory address**!
>

Therefore, we are going to return the "*current timestamp*" by first converting it into seconds!

#### The Actual C Boilerplate Code

> [!NOTE]
> Our file that we will be writing our program will be called / named `main.c`!

```C
#include <stdio.h>
#include <time.h>


// function to emulate `time.perf_counter()` in Python ==> high resoultion monotonic clock
double perf_time_count() {
    // standard C struct to hold seconds and nanoseconds
    struct timespec time_ts;

    // call function `clock_gettime()` to get the current time-stamp
    // NOTE: the `clock_gettime()` function is versatile ==> we are going to pass `CLOCK_MONOTONIC`
    clock_gettime(CLOCK_MONOTONIC, &time_ts);

    // convert seconds and nano-seconds into "total" seconds
    // NOTE: '1e9' = 1 x 10^9, whereby 1 seconds = 1e9 nano-seconds
    return (double) time_ts.tv_sec + (double) time_ts.tv_nsec / 1e9;
}


// function description
int func_name() {
    // code goes here
    return 0;
}

// our main function
int main(int argc, char *argv[]) {
    // declare and initialise sum / total variable
    double sum_times = 0;

    // declare variables related to performance counter
    double start_time;
    double end_time;


    for (int i = 0; i < 10; i++) {
        // initialise the start timer
        start_time = perf_time_count();

        // WARNING: don't forget to call required function
        // and run computation here!!!

        // initialise the start timer
        end_time = perf_time_count();

        // declare and initialise the variable to hold elapsed time
        double elapsed_time = end_time - start_time;

        // increment the variable `sum_times` by `elapsed_time`
        sum_times += elapsed_time;
    }

    // display the average time taken
    // for the program to run 10 iterations
    printf("\nAverage Time: %0.8f s <--\n", sum_times / 10);

    // return '0' --> 'EXIT_STATUS' as `int main()`
    return 0;
}
```

##### Make File for Above Template

As you know, compared to Python; C is a **compiled language**. This means that we are going to file need to run `gcc`, and in this case, specify some flags as we are using the `time.h` header with the `clock_gettime()` function.

```makefile
# specify the compiler to use
# INFO: in our case, we are going to be using 'gcc'
CC = gcc

# specify the compiler flags to use
# the flags `-Wall` and `-Wextra` will provide warnings
# if something goes wrong during the compilation process
CFLAGS = -Wall -Wextra

# specify the linker flags
# these are the flags that "header" dependent
# INFO: in our case, we are going to be using the
# 'time.h' header and `clock_gettime()` function ==> -lrt
# 'math.h' header and `sqrt()` function ==> -lm
LDFLAGS = -lrt -lm

# specify the source file ( file that needs to be compiled )
SRC = main.c

# specify the target / output file ( file that needs to be run )
TARGET = program

# make the 'Makefile' to compile what we need
all: $(TARGET)
$(TARGET): $(SRC)
	$(CC) $(SRC) -o $(TARGET) $(CFLAGS) $(LDFLAGS)

# clean / remove the unwanted files
clean:
	rm -r $(TARGET)
```

> [!NOTE]
> Our output file is going to be called `program`!

> [!TIP] `make` The Program
> In our Makefile, we have 2 *targets* and they are `all` and `clean`. Therefore, we can either do:
>
> 1. `make` $\Rightarrow$ To **build** the `program` *output* file
> 2. `make clean` $\Rightarrow$ To **remove** the `program` *output* file

> [!WARNING] Side Rant
> <p align="center"> Fuck all of you for using the "play" button!!!</p>
>
> I have when I see my friend use the fucking mouse, then click on the play button and then *watch* their code run. Nah, **fuck that mate**!
>
> When I ask them ( *we use Python BTW* ), do you know what is happening when you press that *motherfucking shitty as button with your fucking ass mouse*?
>
> > "No, I don't!"
>
> Hence, **fuck you all**. When we hit year 2 and start C, we'll have to compile it ourselves!
>
> > Now I know that using some *extension*; one can easily still use the *play* button to run C code.
> > But again... **FUCK THAT**!!!
>

---

# Link to Algorithms

## Primality Testing Algorithms

### Deterministic Primality Testing Algorithms

- [[Trial Division Algorithms]]

### Propabilistic Primality Testing Algorithms

- [[Basic Sieve of Eratosthenes]]

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!