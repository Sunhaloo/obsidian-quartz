---
id: Shutdown Computer Prank
aliases: Turning of Computer with Python
tags:
  - python
  - windows
author: S.Sunhaloo
date: 2024-11-08
status: Completed
---

This code was created to prank Mr Hayyan a.k.a "*Boombang*"!

There are 2 parts for this code:

1. Blanking the screen
2. Shutting down the computer

The first part, I told [ChatGPT](https://chat.openai.com) to write because I don't fucking know how to...
The second part, I did write it by myself, just need to learn the syntax to shutdown the computer

```python
import ctypes
import time
import os

# display text in slow motion
def slow_mo_text():
    sentence = "\nSayonara :)\n"

    for ch in sentence:
        print(ch, end="", flush=True)
        time.sleep(0.5)

    time.sleep(5)


def blank_screen():
    HWND_BROADCAST = 0xFFFF
    WM_SYSCOMMAND = 0x0112
    SC_MONITORPOWER = 0xF170
    TURN_OFF = 2
    TURN_ON = -1

    # IDK some sort of Dynamic Link Libraries ( DLL )
    user32 = ctypes.windll.user32

    # turn off
    user32.SendMessageW(HWND_BROADCAST, WM_SYSCOMMAND, SC_MONITORPOWER, TURN_OFF)
    time.sleep(2)
    # turn on
    user32.SendMessageW(HWND_BROADCAST, WM_SYSCOMMAND, SC_MONITORPOWER, TURN_ON)
    # turn off
    user32.SendMessageW(HWND_BROADCAST, WM_SYSCOMMAND, SC_MONITORPOWER, TURN_OFF)


# create a function to display the options to user
def display_options():
    print("\nWelcome to TO DO Application\n")
    print("Select an Option")

    print("\nOption [1]: Insert Tasks")
    print("Option [2]: Display Tasks")


# conditions based on user options
def choice(user_choice: str):
    if user_choice == "1":
        # call the function to output text in slow motion
        slow_mo_text()
        # call the function to blank the screen
        blank_screen()
        # shutdown the computer
        os.system("shutdown /s /t 0")

    elif user_choice == "2":
        # call the function to output text in slow motion
        slow_mo_text()
        # call the function to blank the screen
        blank_screen()
        # shutdown the computer
        os.system("shutdown /s /t 0")
    else:
        # call the function to output text in slow motion
        slow_mo_text()
        # call the function to blank the screen
        blank_screen()
        # shutdown the computer
        os.system("shutdown /s /t 0")


def main():
    # call the function to display options
    display_options()

    # ask the user for a choice
    user_choice = input("\nPlease Enter An Option: ")

    # call the function to evaluate choice
    choice(user_choice)


# run the main function
if __name__ == '__main__':
	main()
```

> [![NOTE]]
> If you don't want the computer to shutdown, you can change `os.system("shutdown /s /t 0)` to `os.system("shutdown /r /t 0)` to **restart** the computer!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!