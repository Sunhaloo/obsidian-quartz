---
id: Python - Emails
aliases: Sending emails in Python using 'Simple Mail Transfer Protocol'
tags:
  - python
  - emails
author: S.Sunhaloo
date: 2025-11-15
status: Completed
---

## List of Contents

- [[#Setup - Requirements]]
	- [[#Setup Google Account]]
- [[#Environment File]]
	- [[#Load The Dictionary]]
- [[#Client Connection]]
	- [[#Connecting To The Mail Server]]
	- [[#Sending Email(s) Using The 'SMTP' Class!]]
- [[#Using Local Debug Server]]
- [[#Formatting Email Message Correctly]]
- [[#Adding Attachments]]
	- [[#Image Attachments]]
- [[#PDF Attachments]]

---

> [!INFO] Resource(s)
> - https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol
> - https://docs.python.org/3/library/smtplib.html
> - https://www.youtube.com/watch?v=JRCJ6RtE3xU

# Setup - Requirements

These are the following things that we are going to need to before we even start writing some code.

- Email Address: My own 'Gmail' email address in this case
- External Python Modules:
	- [Python 'dot-env'](https://pypi.org/project/python-dotenv/)

> Refer to '[[Modrinth - Python API With Matplotlib#Loading Environment Variables]]' for more information.

## Setup Google Account

Google is **not** going to allow us to send emails from Python ( *due to security and other related reasons* ). Therefore, we are going to have to configure our **account** to let Google know that we are going to be doing some cool shit!

> [!INFO] Therefore... Create An App Specific Password
> - Enabled [2-Step Verification](https://support.google.com/accounts/answer/185839)
> - Head over to https://myaccount.google.com/apppasswords
> 	- App Name: Python - Email Learning
> 	- **Auto-Generated** Password: `<Your Password> `

> [!WARNING] Do Enable '2-Factor Verification' First!
> There is another way to be able to **allow** *external* programs, like Python in this case, to have access to your Google Account.
>
> > But that's fucked up!
>
> It requires you to toggle 'Less secure app access' which is going to make you **more** vulnerable to *attacks*.
>
> Hence, just do the right and proper thing and **enable** that *shit*!

> [!SUCCESS]
> We have completed this part and now the actual **fun** part comes!

# Environment File

Given that we are dealing with **passwords** and as I like to work on my GitHub repositories ( *which is 'Private' but still* )... We are going to make use of the famous, famous `.env` file!

> That is why I told you to download the 'dot-env' Python module!

- Create a `.gitignore` file at the **root** of our GitHub repository:

```gitignore
.env
__pycache__/
```

- Create our `.env` file in the **same** directory where you are going to have your `main.py` file:

```env

```

> [!NOTE] Wait... Its Fucking Empty!
> Yes, the `.env` file should and needs to be kept **private** at all times. That is why we **don't** *push*
>
> What I am trying to say is that I am keeping mine a secret from you!
>
> If you don't know how / what contents goes inside of the `.env` file; then you can read this: https://gist.github.com/ericelliott/4152984
>
> > [!INFO] Nevertheless...
> > I will be showing you what you need to add *further* in your `.env` file when its time to code!
>

## Load The Dictionary

The `dotenv` module provides us with a *function* that's going keep all those inside of a [[Python - Dictionaries | Python Dictionary]].

I have a little `NAME` and `URL` variable that is inside my `.env` file; let's see that if we can get their respective values.

- This is how we can **load** our `.env` variables into our Python code:

```python
# import the `dotenv_values` function from the 'dotenv' library only
from dotenv import dotenv_values


# load the environment variable into a global dictionary
ENV_DATA: dict = dotenv_values(".env")


def main():
    # display the `NAME` and `URL` variable
    print(f"Name Variable: {ENV_DATA["NAME"]}")
    print(f"URL Variable: {ENV_DATA["URL"]}")


if __name__ == "__main__":
    main()
```

- Therefore, *running* our `main.py` file, we should see that we have **values** for our *variables*:

```console
Name Variable: Joe Mama
URL Variable: https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

> You should really watch this YouTube video... Its about '*things*'!

# Client Connection

## Connecting To The Mail Server

Similar to something like **opening** a *file* is a programming language... After using it, we are going to have to **close** it so that it does **not** *consume* our precious resources.

> This is **also** the case for that "*connection*".

Hence, similar to how we **open** *files* in Python using the `with` ( *context manager* ) keyword; whereby we **don't** need to *manually* use the `.close()` function. Therefore, we are going to be using the `with` keyword to also open

## Sending Email(s) Using The 'SMTP' Class!

> [!INFO] Environment File - Update
> To be able to use / follow the codes below, make sure that you have these **environment variables** inside your `.env` file:
>
> - `GMAIL_SERVER`
> - `PORT`
> - `EMAIL_ADDRESS`
> - `APP_PASSWORD`

> [!INFO] What's the value of `GMAIL_SERVER`?
> Given that I am using 'Gmail' the variable `GMAIL_SERVER` has a value of `smtp.gmail.com`.
>
> > "*But I don't fucking use 'Gmail'!*" Some random guy named 'Toushal'!
>
> Here are some other email provider's "*value*":
>
> - `MICROHARD_SERVER="smtp.office365.com"`
> - `APPLEFANBOY_SERVER="smtp.mail.me.com"`
> - `YAHOO_SERVER="smtp.mail.yahoo.com"`

```python
# import the `dotenv_values` function from the 'dotenv' library only
from dotenv import dotenv_values

# import the 'smtplib' module to allow for client to send emails
import smtplib


# load the environment variable into a global dictionary
ENV_DATA: dict = dotenv_values(".env")


def main():
    # create 'client - server' connection
    with smtplib.SMTP(ENV_DATA["GMAIL_SERVER"], ENV_DATA["EMAIL_PORT"]) as smtp:
        # NOTE: optional ( already done in background ) --> authenticate with server
        smtp.ehlo()

        # encrypt the connection using 'TLS'
        smtp.starttls()

        # WARNING: required --> authenticate to email server to use encryption
        smtp.ehlo()

        print("\n" + "-" * 50, "\n")
        print("-- Authenticated --".center(25))
        print("\n" + "-" * 50, "\n")

        # login using your 'gmail' address and 'app' password
        smtp.login(ENV_DATA["EMAIL_ADDRESS"], ENV_DATA["APP_PASSWORD"])

        # create our subject header
        email_subject = "Python Email Test Message"

        # create our body ( our message to send )
        email_body = "This email has been sent using the 'SMTP' module from a simple Python script"

        # write our actual message
        email_message = f"Subject: {email_subject}\n\n{email_body}"

        # send the simple "plain text" email
        smtp.sendmail(
            ENV_DATA["EMAIL_ADDRESS"], "receiver@emial.com, email_message
        )

        print("\n" + "-" * 50, "\n")
        print("-- Email Sent --".center(25))
        print("\n" + "-" * 50, "\n")


if __name__ == "__main__":
    main()
```

> [!NOTE] Updated `receiver@email.com`!
> I have updated the **receiver**'s email to be my **own** email address, i.e `ENV_DATA["EMAIL_ADDRESS"]`.
>
> > I want to see if the code works right and I don't have any friend so...
>

- Therefore running the code:

```console
--------------------------------------------------

   -- Authenticated --

--------------------------------------------------


--------------------------------------------------

     -- Email Sent --

--------------------------------------------------
```

> [!SUCCESS]
> I see that I have received the email in my **inbox**...
>
> > So its actually a *valid* things! Because I expected it to go into my 'Spam' *folder*.
>
> OMG, it also shows that we sent the email in our 'Send' *folder*!

# Using Local Debug Server

> [!INFO] Resource(s)
> - https://aiosmtpd.aio-libs.org/en/latest/intro.html

In the above example, you can see that we did actually send *someone* an email. But let's say that you are testing things out and **don't** want to repeatedly send emails to someone or yourself and clutter your inbox.

> This is where the 'Local Debug Server' comes into play!

Instead of using something like `smtp.gmail.com` or some ( *actual* ) email server; we are going to simply use the `localhost` on a **default** port of `1025`. Hence, let's get started in running the local debug server.

- Install the proper *dependencies* / Python module:

```console
# windows users
pip install python-aiosmtpd

# macos users - see homebrew package manager or xcode-select
# sorry

# debian / debian based distribution
sudo apt-get install python3-aiosmtpd

# I use Arch BTW
sudo pacman -S python-aiosmtpd

# fedora based distributions
sudo dnf install python3-aiosmtpd
```

> [!NOTE]
> In Corey's video he is using something that looks like this:
>
> ```bash
> python -m smptd -c DebuggingServer -n localhost:1025
> ```
>
> But when I run the above Python command, I get the following error:
>
> ```console
> /usr/sbin/python: No module named smtp
> ```
>
> > Basically the `aiosmtpd` is basically a newer version of `smtpd` as the video was made **6** years ago at the time of writing this!
>

- Run the Python local ( *email* ) debug server:

```bash
# run the local debug ( email ) server by 'aiosmtpd'
python -m aiosmtpd -n -l localhost:1025
```

> [!TIP] Multiple Terminals / [TMUX](https://en.wikipedia.org/wiki/Tmux)
> As this is needs to be kept running in the background; I suggest that you **either** open multiple terminals ( *I use Neovim, i.e, I live inside the terminal* ) or simply learn how to use a **tool** like 'TMUX'.

> [!NOTE] What Does The Above Command Means?
> - `python -m aiosmptd`: Run the `aiosmptd` module as a **script**
> - `-n -l localhost:1025`: Run as a **foreground** ( *don't run as background service / daemon* ) and **listen** on `localhost:1025`

- Therefore modify the above code to this:

```python
# import the `dotenv_values` function from the 'dotenv' library only
from dotenv import dotenv_values

# import the 'smtplib' module to allow for client to send emails
import smtplib


# load the environment variable into a global dictionary
ENV_DATA: dict = dotenv_values(".env")


def main():
    # create 'client - server' connection to the local host ( 'aiosmtpd' module )
    with smtplib.SMTP("localhost", 1025) as smtp:
        # INFO: as you can see we are not authenticating or actually sending the email

        # create our subject header
        email_subject = "Python Email Test Message"

        # create our body ( our message to send )
        email_body = "https://www.youtube.com/watch?v=dQw4w9WgXcQ"

        # write our actual message
        email_message = f"Subject: {email_subject}\n\n{email_body}"

        smtp.sendmail(
            "random_sender@email.com", "random_receiver@email.com", email_message
        )

        print("\n" + "-" * 50, "\n")
        print("-- Email Sent To Localhost Debug Server --".center(50))
        print("\n" + "-" * 50, "\n")


if __name__ == "__main__":
    main()
```

- Running the `main.py` file using `python`, I get the following output:

```console
--------------------------------------------------

    -- Email Sent To Localhost Debug Server --

--------------------------------------------------
```

- On the TMUX pane that is running the local debug server, I see this:

```console
---------- MESSAGE FOLLOWS ----------
Subject: Python Email Test Message
X-Peer: ('::1', 45346, 0, 0)

https://www.youtube.com/watch?v=dQw4w9WgXcQ
------------ END MESSAGE ------------
```

> [!WARNING]
> Again, compared to Corey whereby he did **not** use the `.sendmail()` method; in our case do need to use it!
>
> Nevertheless, given that this is sending to the **local server**; there is no need to enter *real* email addresses!

# Formatting Email Message Correctly

> We are going to import another module!

Right now, the *look* of our message that we are sending is currently **dog water**. Therefore, we are going to try to fix that in this section!

> Proper formatting for emails can be achieved using the `email` _**package**_

> [!WARNING] But Before We Start...
> In this part of the tutorial, Corey used the `SMTP_SSL` *class* instead of the regular `SMTP`. Given that 'Secure Socket Layer' ( '*SSL*' ) is now **deprecated**. I am **not** going to use it!
>
> > I am just going to use 'TLS' like we did above!
>

- This is how we are going to be sending emails to have proper formatting:

```python
# import the `dotenv_values` function from the 'dotenv' library only
import email
from dotenv import dotenv_values

# import the 'smtplib' module to allow for client to send emails
import smtplib

# import the class `EmailMessage` from the package - module `email.message`
from email.message import EmailMessage


# load the environment variable into a global dictionary
ENV_DATA: dict = dotenv_values(".env")


def main():
    # create an object of the `EmailMessage` class
    email_message = EmailMessage()

    # add the proper data ( sender - receiever )
    email_message["From"] = ENV_DATA["EMAIL_ADDRESS"]
    email_message["To"] = ENV_DATA["EMAIL_ADDRESS"]

    # add the proper data ( the actual message )
    email_message["Subject"] = "Sending Properly Formatted Emails Using Python"
    email_message.set_content(
        "Dear Person,\n\nThe very email that you are reading should be properly formatted.\n\nRegards,\nYour Mama"
    )

    # create 'client - server' connection to the Gmail's server
    with smtplib.SMTP(ENV_DATA["GMAIL_SERVER"], ENV_DATA["EMAIL_PORT"]) as smtp:
        # encrypt the connection using 'TLS'
        smtp.starttls()

        # authenticate to server to now use encryption
        smtp.ehlo()

        # login using 'gmail' address and 'app' password
        smtp.login(ENV_DATA["EMAIL_ADDRESS"], ENV_DATA["APP_PASSWORD"])

        smtp.send_message(email_message)

        print("\n" + "-" * 50)
        print("-- Email Sent --".center(50))
        print("-" * 50, "\n")


if __name__ == "__main__":
    main()
```

- This is the output that I get after running the above Python file:

```console
--------------------------------------------------
                 -- Email Sent --
--------------------------------------------------
```

> [!SUCCESS]
> The email has been sent and it does seems to have **better** *formatting* compared to our previous one!

# Adding Attachments

## Image Attachments

So there are two ways that we can do this; one is by using the `splittext` function ( *or `.split()` see below* ) or using something like the [Pillow]() module.

> We are going to be using both here so that we can get a comparison!

### Using OS Module

- This is how we can use the `os` module to be able to **attach** an *image* to our email:

```python
# import the `dotenv_values` function from the 'dotenv' library only
from dotenv import dotenv_values

# import the 'smtplib' module to allow for client to send emails
import smtplib

# import the class `EmailMessage` from the package - module `email.message`
from email.message import EmailMessage

# for file path niceities
from os.path import expanduser, splitext


# load the environment variable into a global dictionary
ENV_DATA: dict = dotenv_values(".env")


def main():
    # create an object of the `EmailMessage` class
    email_message = EmailMessage()

    # add the proper data ( sender - receiever )
    email_message["From"] = ENV_DATA["EMAIL_ADDRESS"]
    email_message["To"] = ENV_DATA["EMAIL_ADDRESS"]

    # add the proper data ( the actual message )
    email_message["Subject"] = "Sending Properly Formatted Emails Using Python"
    email_message.set_content(
        "Dear Person,\n\nThe very email that you are reading should be properly formatted. Additionally, there is an image attached here.\n\nRegards,\nYour Mama"
    )


    # variable to hold the full path of the image
    img_path = expanduser("~/Wallpapers/MaoMao-Face.png")

    # open the image file to read binary contents and image file name
    with open(img_path, "rb") as img_file:
        # read all the contents of the image
        img_data = img_file.read()

    # get the image file name
    img_file_name = img_path.split("/")[4]

    # get image file's extension --> from the tuple returned by `splitext`
    img_file_ext = splitext(img_path)[1][1:]

    # add the image as attachment to the email
    email_message.add_attachment(
        img_data, maintype="image", subtype=img_file_ext, filename=img_file_name
    )

    # create 'client - server' connection to the Gmail's server
    with smtplib.SMTP(ENV_DATA["GMAIL_SERVER"], ENV_DATA["EMAIL_PORT"]) as smtp:
        # encrypt the connection using 'TLS'
        smtp.starttls()

        # authenticate to server to now use encryption
        smtp.ehlo()

        # login using 'gmail' address and 'app' password
        smtp.login(ENV_DATA["EMAIL_ADDRESS"], ENV_DATA["APP_PASSWORD"])

        smtp.send_message(email_message)

        print("\n" + "-" * 50)
        print("-- Email Sent --".center(50))
        print("-" * 50, "\n")


if __name__ == "__main__":
    main()
```

> [!TIP] Difference Between `.split()` and `os.path.splitext`
> The main thing its that `.split` is **general** and works on any string and you <strong> <span style="color: red;"> need</span> </strong> to pass in an **argument** that is going to act as the "*split character*".
>
> This is the **not** the case with `splitext`! This is due to the fact that the Python developers **only** intended it to be used with **file paths**. Below you are going to find a little example of getting the file extension from some file "*paths*".
>
> ```python
> # import the required functions from 'os' module
> from os.path import expanduser, splitext
>
> # image path
> img_path = expanduser("~/mnt/somewhere/in/hogwarts/voldemort_secrets.tar.gz")
>
> # split the image using `.split`
> img_split = img_path.split(".")
>
> # split the image using `splitext`
> img_splitext = splitext(img_path)
>
> # display the results
> print(f"Result of `.split()`: {img_split}")
> print(f"Result of `splitext()`: {img_splitext}")
> ```
>
> - This is the result after running the above code:
>
> ```console
> Result of `.split()`: ['/home/username/mnt/somewhere/in/hogwarts/voldemort_secrets', 'tar', 'gz']
> Result of `splitext()`: ('/home/username/mnt/somewhere/in/hogwarts/voldemort_secrets.tar', '.gz')
> ```
>
> > But as Mr Sathan tells us "*They are smarter than us... Use their functions and techniques*!!!"
>

### Using Pillow ( External ) Module

> [!NOTE]
> You are going to have to first install the 'Pillow' module **first** to be able to run the following code below.
>
> > In my case, I just did a `sudo pacman -S python-pillow --noconfirm`!
>

- So this is going to be basically the same thing but now with `PIL`:

```python
# import the `dotenv_values` function from the 'dotenv' library only
from dotenv import dotenv_values

# import the 'smtplib' module to allow for client to send emails
import smtplib

# import the class `EmailMessage` from the package - module `email.message`
from email.message import EmailMessage

# for file path niceities
from os.path import expanduser

# import the `Image` class from the 'pillow' module
from PIL import Image


# load the environment variable into a global dictionary
ENV_DATA: dict = dotenv_values(".env")


def main():
    # create an object of the `EmailMessage` class
    email_message = EmailMessage()

    # add the proper data ( sender - receiever )
    email_message["From"] = ENV_DATA["EMAIL_ADDRESS"]
    email_message["To"] = ENV_DATA["EMAIL_ADDRESS"]

    # add the proper data ( the actual message )
    email_message["Subject"] = "Sending Properly Formatted Emails Using Python"
    email_message.set_content(
        "Dear Person,\n\nThe very email that you are reading should be properly formatted. Additionally, there is an image attached here.\n\nRegards,\nYour Mama"
    )

    # variable to hold the full path of the image
    img_path = expanduser("~/Wallpapers/MaoMao-Face.png")

    # open the image file to read binary contents and image file name
    with open(img_path, "rb") as img_file:
        # read all the contents of the image
        img_data = img_file.read()

    # get the image file name
    img_file_name = img_path.split("/")[4]

    # get image file's extension --> from the class of `Image`
    with Image.open(img_path) as img_file:
        # check if the image path if valid
        if img_file.format is None:
            # raise a little error
            raise ValueError(f"Image ( Path: {img_path} ) Not Found")

        # get the extension directly
        img_file_ext = img_file.format.lower()

    # add the image as attachment to the email
    email_message.add_attachment(
        img_data, maintype="image", subtype=img_file_ext, filename=img_file_name
    )

    # create 'client - server' connection to the Gmail's server
    with smtplib.SMTP(ENV_DATA["GMAIL_SERVER"], ENV_DATA["EMAIL_PORT"]) as smtp:
        # encrypt the connection using 'TLS'
        smtp.starttls()

        # authenticate to server to now use encryption
        smtp.ehlo()

        # login using 'gmail' address and 'app' password
        smtp.login(ENV_DATA["EMAIL_ADDRESS"], ENV_DATA["APP_PASSWORD"])

        smtp.send_message(email_message)

        print("\n" + "-" * 50)
        print("-- Email Sent --".center(50))
        print("-" * 50, "\n")


if __name__ == "__main__":
    main()
```

> [!SUCCESS]
> We have now seen how to send images to someone via email!

### Sending Multiple Image Attachments

> What about sending multiple images?

I am now going to create a folder in the **same** directory as my `main.py` file and place some images inside of it!

- This is how my directory looks like currently:

```console
 .
├──  images
│   ├──  1.jpg
│   ├──  2.jpg
│   └──  3.jpg
└──  main.py
```

- Here is the code that is going to send **multiple** images to someone:

```python
# import the `dotenv_values` function from the 'dotenv' library only
from dotenv import dotenv_values

# import the 'smtplib' module to allow for client to send emails
import smtplib

# import the class `EmailMessage` from the package - module `email.message`
from email.message import EmailMessage

# for file path niceities
from os import listdir

# import the `Image` class from the 'pillow' module
from PIL import Image


# load the environment variable into a global dictionary
ENV_DATA: dict = dotenv_values(".env")


def main():
    # create an object of the `EmailMessage` class
    email_message = EmailMessage()

    # add the proper data ( sender - receiever )
    email_message["From"] = ENV_DATA["EMAIL_ADDRESS"]
    email_message["To"] = ENV_DATA["EMAIL_ADDRESS"]

    # add the proper data ( the actual message )
    email_message["Subject"] = "Sending Properly Formatted Emails Using Python"
    email_message.set_content(
        "Dear Person,\n\nThe very email that you are reading should be properly formatted. Additionally, there are images attached here.\n\nRegards,\nYour Mama"
    )

    # variable to hold the full path of the image
    image_dir = listdir("./images/")

    # iterate throught the images inside the `./images/` folder
    for image_file in image_dir:
        # get the full path of the image
        image = "./images/" + image_file

        # open the image file to read binary contents and image file name
        with open(image, "rb") as file:
            # read all the contents of the image
            img_data = file.read()

        # get image file's extension --> from the class of `Image`
        with Image.open(image) as file:
            # check if the image path if valid
            if file.format is None:
                # raise a little error
                raise ValueError(f"Image ( Path: {image} ) Not Found")

            # get the extension directly
            img_file_ext = file.format.lower()

        # add the image as attachment to the email
        email_message.add_attachment(
            img_data, maintype="image", subtype=img_file_ext, filename=image_file
        )

    # create 'client - server' connection to the Gmail's server
    with smtplib.SMTP(ENV_DATA["GMAIL_SERVER"], ENV_DATA["EMAIL_PORT"]) as smtp:
        # encrypt the connection using 'TLS'
        smtp.starttls()

        # authenticate to server to now use encryption
        smtp.ehlo()

        # login using 'gmail' address and 'app' password
        smtp.login(ENV_DATA["EMAIL_ADDRESS"], ENV_DATA["APP_PASSWORD"])

        smtp.send_message(email_message)

        print("\n" + "-" * 50)
        print("-- Email Sent --".center(50))
        print("-" * 50, "\n")


if __name__ == "__main__":
    main()
```

> [!TIP] No Need To Calculate Name Of File
> There is not need to calculate the image *file name* using things like `splitext` as we already are iterating through the **directory** which means that we **already** have the *name* of each file!

> [!WARNING] Full Path!
> Given that the `open` and `Image.open()` *methods* requires the full path. Instead of importing the whole 'os' library to get access to the `join` function from the `path` *module*.
>
> I decided it was best for me to just do this:
>
> ```python
> # get the full path of the image
> image = "./images/" + image_file
> ```

> [!SUCCESS]
> We have now learned how to send multiple, *not only images*, but this code is the "*boilerplate*" code for sending a **multiple** *data* all at once!

## PDF Attachments

We are now going to **attach** some 'PDF' files to our email! Therefore go ahead create a `pdfs` folder and add some 'PDF' files in it!

- This is how my current directory structure looks like:

```console
 .
├──  main.py
└──  pdfs
    ├──  'Introduction To DSA.pdf'
    └──  'PC Build.pdf'
```

> [!NOTE]
> This is going to be of the **same** principle as above but instead of `maintype="image"`, its `maintype="application"` and instead of `subtype="image"` we have `subtype="octet-stream"`. Additionally as we are dealing with 'PDF' files, we can simply **remove** the the '*pillow*' import!

```python
# import the `dotenv_values` function from the 'dotenv' library only
from dotenv import dotenv_values

# import the 'smtplib' module to allow for client to send emails
import smtplib

# import the class `EmailMessage` from the package - module `email.message`
from email.message import EmailMessage

# for file path niceities
from os import listdir


# load the environment variable into a global dictionary
ENV_DATA: dict = dotenv_values(".env")


def main():
    # create an object of the `EmailMessage` class
    email_message = EmailMessage()

    # add the proper data ( sender - receiever )
    email_message["From"] = ENV_DATA["EMAIL_ADDRESS"]
    email_message["To"] = ENV_DATA["EMAIL_ADDRESS"]

    # add the proper data ( the actual message )
    email_message["Subject"] = "Sending Properly Formatted Emails Using Python"
    email_message.set_content(
        "Dear Person,\n\nThe very email that you are reading should be properly formatted. Additionally, there are 'PDF' files attached here.\n\nRegards,\nYour Mama"
    )

    # variable to hold the full path of the image
    pdf_dir = listdir("./pdfs/")

    # iterate throught the 'PDF' files inside the `./pdfs/` folder
    for pdf_file in pdf_dir:
        # get the full path of the pdf
        pdf = "./pdfs/" + pdf_file

        # open the image file to read binary contents and image file name
        with open(pdf, "rb") as file:
            # read all the contents of the image
            img_data = file.read()

        # add the image as attachment to the email
        email_message.add_attachment(
            img_data,
            maintype="application",
            subtype="octet-stream",
            filename=pdf_file,
        )

    # create 'client - server' connection to the Gmail's server
    with smtplib.SMTP(ENV_DATA["GMAIL_SERVER"], ENV_DATA["EMAIL_PORT"]) as smtp:
        # encrypt the connection using 'TLS'
        smtp.starttls()

        # authenticate to server to now use encryption
        smtp.ehlo()

        # login using 'gmail' address and 'app' password
        smtp.login(ENV_DATA["EMAIL_ADDRESS"], ENV_DATA["APP_PASSWORD"])

        smtp.send_message(email_message)

        print("\n" + "-" * 50)
        print("-- Email Sent --".center(50))
        print("-" * 50, "\n")


if __name__ == "__main__":
    main()
```

> [!SUCCESS]
> We have now been able to send someone *a* / *multiple* 'PDF' file(s)!

# Sending Email To Multiple People

> Its actually very simple!

Let's take the original code found in the section '[[#Formatting Email Message Correctly]]' and modify it so that it now looks like this.

```python
# import the `dotenv_values` function from the 'dotenv' library only
import email
from dotenv import dotenv_values

# import the 'smtplib' module to allow for client to send emails
import smtplib

# import the class `EmailMessage` from the package - module `email.message`
from email.message import EmailMessage


# load the environment variable into a global dictionary
ENV_DATA: dict = dotenv_values(".env")


def main():
    # create list of recipients
    recipients = [
        "recipient1@email.com",
        "recipient2@email.com",
        "recipient3@email.com",
    ]

    # create list of "Cc" recipients
    cc_recipients = ["cc_recipients1@email.com", "cc_recipient2@email.com"]

    # create an object of the `EmailMessage` class
    email_message = EmailMessage()

    # add the proper data ( sender - receiever )
    email_message["From"] = ENV_DATA["EMAIL_ADDRESS"]
    email_message["To"] = ", ".join(recipients)

    # add "people" as "Cc"
    email_message["Cc"] = ", ".join(cc_recipients)

    # add the proper data ( the actual message )
    email_message["Subject"] = "Sending Properly Formatted Emails Using Python"
    email_message.set_content(
        "Dear Person,\n\nThis very email that you are reading has been written and send using a Python script.\n\nRegards,\nS.Sunhaloo"
    )

    # create 'client - server' connection to the Gmail's server
    with smtplib.SMTP(ENV_DATA["GMAIL_SERVER"], ENV_DATA["EMAIL_PORT"]) as smtp:
        # encrypt the connection using 'TLS'
        smtp.starttls()

        # authenticate to server to now use encryption
        smtp.ehlo()

        # login using 'gmail' address and 'app' password
        smtp.login(ENV_DATA["EMAIL_ADDRESS"], ENV_DATA["APP_PASSWORD"])

        smtp.send_message(email_message)

        print("\n" + "-" * 50)
        print("-- Email Sent --".center(50))
        print("-" * 50, "\n")


if __name__ == "__main__":
    main()
```

- This is the only "*part*" that we have changed:

```python
    # create list of recipients
    recipients = [
        "recipient1@email.com",
        "recipient2@email.com",
        "recipient3@email.com",
    ]

    # create list of "Cc" recipients
    cc_recipients = ["cc_recipients1@email.com", "cc_recipient2@email.com"]

    # create an object of the `EmailMessage` class
    email_message = EmailMessage()

    # add the proper data ( sender - receiever )
    email_message["From"] = ENV_DATA["EMAIL_ADDRESS"]
    email_message["To"] = ", ".join(recipients)

    # add "people" as "Cc"
    email_message["Cc"] = ", ".join(cc_recipients)
```

> [!SUCCESS]
> We have now seen how to send email to **multiple** people!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!