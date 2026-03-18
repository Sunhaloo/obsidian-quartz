---
id: Python - Requests Module
aliases: ( API ) Web Requests in Python
tags:
  - python
  - api
author: S.Sunhaloo
date: 2025-10-15
status: In-Progress
---

## List of Contents

- [[#Installation of Python Requests Module]]
- [[#Bro Code's Video]]
	- [[#Making A Request]]
	- [[#What's A Request?]]
		- [[#Anatomy Of `GET` and `POST` Requests]]
	- [[#Retrieving Data From API]]
- [[#Corey Schafer's Video]]
	- [[#Get The Raw HTML Page]]
	- [[#Download Images]]
	- [[#Better Status Code Handling]]
	- [[#Making Requests - Getting Responses With 'httpbin.org']]
		- [[#The Correct Way To Do Parameters]]
		- [[#Using JSON Instead Of Text]]

---

> [!INFO] Resource(s)
> - YouTube Video(s):
> 	- https://www.youtube.com/watch?v=JVQNywo4AbU
> 	- https://www.youtube.com/watch?v=tb8gHvYlCFs
> 	- https://www.youtube.com/watch?v=Xi1F2ZMAZ7Q
> - *API* Website(s):
> 	- https://pokeapi.co/

# Installation of Python Requests Module

First of all, check if you already have the `requests` module installed. This can be done by running the following command:

```bash
python -c "import requests; print(requests.__version__)"
```

- This is the version of `requests` at the time of writing this note:

```console
2.32.5
```

> [!INFO]
> If you did **not** know... We can use the `-c` flag provided by Python to be able to *run* Python code **without** opening the [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop) or writing the code into a file first!

## Windows Users

Given that I have **not** used Windows in a long time, but I know that back in the day. I needed to **manually** install the `requests` module by myself using the `pip` package manager!

> [!INFO] I am right!
> Booting up a Python Virtual Environment running the above command is going to give me this:
>
> ```console
> Traceback (most recent call last):
>  File "<string> ", line 1, in <module>
>    import requests; print(requests.__version__)
>    ^^^^^^^^^^^^^^^
> ModuleNotFoundError: No module named 'requests'
> ```

> [!TIP] Installing The `requests` Module
> Hence, use the following command below to install the `requests` module that we need to:
>
> ```powershell
> python -m pip install requests
> ```
>
> Therefore, if you run the above command to check the version of `requests` that you have on your computer. You should see that you have it!

## Before We Start

<h4 align="center"> Learn By Doing</h4>

<p align="center">
	Instead of making complete "<em> documentation notes</em> " and then go and make something... I am going to try to build what I wanted since <strong> one</strong> and <strong> a half</strong> years ago!
<br>
	Hence, I am just going to follow <em> exactly</em> what they are showing and try to make an <a href="https://en.wikipedia.org/wiki/Minimum_viable_product" alt="MVP On Wikipedia"> MVP</a> for my thing!
</p>

---

# Bro Code's Video

> [!WARNING] JSON Format
> As the most websites uses [JSON](https://en.wikipedia.org/wiki/JSON) format for **returning** the data that we asked for.
>
> Therefore, I am going to create another note / file '[[Python - JSON Module]]'
>
> > Well, let's get started with the tutorials!
>

## Making A Request

- This it the code that we are going to use so that we can actually try to connect to to the API:

```python
# import the 'request' module to be able to connect to API
import requests

# global variable to hold the "base" URL of the API itself
# WARNING: this the website URL is 'https://pokeapi.co/' is the website itself
# but we are not iterested in the website... But instead in the API that it provides
BASE_URL: str = "https://pokeapi.co/api/v2/"


# function that is going to make the requests and test the URL
def test_url():
    # try to get the response object
    response = requests.get(BASE_URL)

    # display the response of the request ( if requests succeeded )
    print(f"\n\t-- Response Object: {response} --")
    # display the HTTP status code of the request itself
    print(f"\t   -- Response Status Code: {response.status_code} --\n")


# our main function
def main():
    # call the function to check if the URL is valid
    test_url()


# source the main function
if __name__ == "__main__":
    main()
```

- The above code is going to output something like this:

```console
        -- Response Object: <Response [200]> --
           -- Response Status Code: 200 --
```

## What's A Request?

> [!INFO] Resource(s)
> - https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Messages

A *request* is just that; the **client** ask making a "*request*" to ask the server to give him / her the data ( *or information or media* ) that the user wants. If the server finds or even does **not** found the data. A **response** is sent back to the **client**!

Below you are going to find about some diagram on how `GET` and `POST` requests are actually made.

- `GET` Request Diagram

```mermaid
sequenceDiagram
    participant Client as 🖥️ CLIENT<br/> (You)
    participant Server as 🌐 SERVER<br/> (YouTube)
    
    Note over Client,Server: GET Request - Retrieving Data
    Client-> > Server: GET /watch?v=dQw4w9WgXcQ<br/> "Give me video dQw4w9WgXcQ"
    Note right of Server: Server processes<br/> request and fetches<br/> video data
    Server-> > Client: 200 OK<br/> "Here's the video HTML + data"
    Note over Client: 📥 You RECEIVE data
```

- `POST` Request Diagram

```mermaid
sequenceDiagram
    participant Client as 🖥️ CLIENT<br/> (You)
    participant Server as 🌐 SERVER<br/> (YouTube)
    
    Note over Client,Server: POST Request - Sending Data
    Client-> > Server: POST /api/comments<br/> 📤 "Here's my comment, save it!"<br/> {comment: "Great song!"}
    Note right of Server: Server saves<br/> your comment to<br/> database
    Server-> > Client: 201 Created<br/> "Saved! Here's confirmation"
    Note over Client: ✅ Comment posted successfully
```

> [!TIP] What are `GET` and `POST` requests *methods*?
> > I finally understand it!
>
> Basically, let's say that you, the client, is **asking** for some data *from* the server. Therefore, you are going a `GET` <span style="color: orange;"> request</span> .
>
> But if you ( *again "the client"* ) is going to be **giving** ( *or 'writing'* ) some data *to* the server. Then you are going have a `POST` <span style="color: orange;"> request</span> .
>
> Now there are other HTTP methods that exists and here they are down in the table below:
>
> | Method | Purpose | Example Use Case |
> |--------|---------|------------------|
> | `GET` | **Retrieve** data from server | Loading a webpage, fetching user profile, searching |
> | `POST` | **Send** data to server | Posting a comment, submitting a form, creating account |
> | `PUT` | **Update** *entire* resource | Updating entire user profile, replacing a document |
> | `DELETE` | **Remove** data from server | Deleting a comment, removing a video, deleting account |
> | `PATCH` | **Update** *part* of a resource | Changing just username, updating email only |
> | `HEAD` | **Get** *headers only* | Checking if file exists, getting file size |
> | `OPTIONS` | **Get** *allowed* methods | Checking what operations are permitted on endpoint |
>
> > [!NOTE] Public APIs
> > Most *public* APIs only allow for `GET`, `HEAD` and `OPTIONS` methods!
>

### Anatomy Of `GET` and `POST` Requests

- `GET` HTTP Requests Anatomy:

```console
GET /api/v2/pokemon/pikachu HTTP/1.1
Host: pokeapi.co
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36
Accept: application/json, text/plain, */*
Accept-Language: en-US,en;q=0.9
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Referer: https://pokeapi.co/
Cookie: session_id=abc123xyz
```

- `POST` HTTP Requests Anatomy:

```console
POST /api/comments HTTP/1.1
Host: youtube.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
Accept: application/json
Content-Type: application/json
Content-Length: 89
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
Cookie: session_token=xyz789
Origin: https://youtube.com
Referer: https://youtube.com/watch?v=dQw4w9WgXcQ

{
  "video_id": "dQw4w9WgXcQ",
  "comment": "Great song! 🎵",
  "user_id": "12345",
  "timestamp": "2:30"
}
```

> [!TIP] Where Can You See This Data!
> Let's go to the famous, famous [YouTube](https://youtube.com/) website and right-click your mouse and open the '*inspect*' tab!
>
> Then upon opening; go to the '*Network*' tab and if you give it like 3 seconds... Its going to load all the **requests** that we are *using* ( *`GET`ing* ) and as this is YouTube and we can `POST` stuff... see all the `POST` requests that we are doing!

## Retrieving Data From API

> [!INFO] Resource(s)
> - https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status

> [!INFO]
> As you know, most websites return data in the JSON format!
>
> Therefore, if you need some help, I suggest you to take a look at the notes / files found below first:
>
> - [[Python - Dictionaries]]
> - [[Python - JSON Module]]
>
> After that, I think you should be ready to continue here!

- This code below is going to data that is found for a *specified* Pokemon, entered by the user:

```python
# import the 'request' module to be able to connect to API
import requests

# global variable to hold the "base" URL of the API itself
BASE_URL: str = "https://pokeapi.co/api/v2/"

# function that is going to make the requests and test the URL
def test_url():
    # try to get the response object
    response = requests.get(BASE_URL)

    # display the response of the request ( if requests succeeded )
    print(f"\n\t-- Response Object: {response} --")
    # display the HTTP status code of the request itself
    print(f"\t   -- Response Status Code: {response.status_code} --\n")


# function that is going to return the JSON data of a pokemon
def get_pokemon_information(pokemon_name: str):
    # create the new URL string that and pass the name of the pokemon
    POKEMON_URL = f"{BASE_URL}/pokemon/{pokemon_name}"

    # try to get a response from the server using 'GET' HTTP method
    response = requests.get(POKEMON_URL)

    # check if we have success with the 'GET' request
    if response.status_code == 200:
        # meaning that we do have a response from the server
        print("\n" + "-" * 50)
        print("\tData Retrieved From Server")
        print("-" * 50)

        # return the data into python's JSON object ==> dictionaries or lists
        return response.json()

    # if the data could not be retrieved from the server
    # INFO: for example, wrong pokemon name or something that does not exists, etc
    else:
        # meaning that the data could not be retrieved from the server
        print(
            f"<< Data For Pokemon '{pokemon_name}' Could Not Be Retrieved From Server!!! > > "
        )

        # exception handling
        try:
            # return the data into python's JSON object ==> dictionaries or lists
            return response.json()

        # if there are not data to return / convert to 'JSON' "Python object"
        except requests.exceptions.JSONDecodeError as e:
            # output appropriate message
            print(f"\n<< Error: {e} > > ")
            print(
                f"<< Failed To Retrieve Data --> Status Code: {response.status_code} > > \n"
            )

            # therefore, return `None` to the "main" program
            return None
```

> In this case, I use the famous 'Pikachu' as the pokemon name!

- This is out *updated* `main` function to be able to display the data **requested**:

```python
# our main function
def main():
    # call the function to check if the URL is valid
    # NOTE: refer to above ( notes ) as we did not change the implementation of this
    test_url()

    # display a horizontal rule
    print("  " + "-" * 50, "\n")

    # call the function that will return the data of the specific pokemon
    pokemon_data = get_pokemon_information("pikachu")

    # check if the return data is `None` or not
    if pokemon_data:
        # display the ID, name of 'pikachu'
        print(f"\n\t-- Pokemon ID: {pokemon_data["id"]}")
        print(f"\t-- Pokemon Name: {pokemon_data["name"]}")

        # find the abilities of 'pikachu' pokemon
        # --> iterate through the 'abilities' list "value"
        for ability in pokemon_data["abilities"]:
            # --> access the outer dictionary with `ability["ability"]`
            # --> access the innect dictionary with `ability["ability"]["name"]`
            # ==> get the value of the key of 'name'
            print(f"\t- Ability: {ability["ability"]["name"]}")

        print("\n" + "-" * 50)
        print("\t-- Using Range Function --")
        print("-" * 50)

        # same thing / principle as about but now just with `range` function
        # NOTE, we could have also used the `enumerate` function if we wanted to
        for i in range(len(pokemon_data["abilities"])):
            print(
                f"\t- Ability {i + 1}: {pokemon_data["abilities"][i]["ability"]["name"]}"
            )

    # if the data could not be retrieved from server
    else:
        # output an appropriate message
        print("   " + "-" * 44)
        print("   << Data Could NOT Be Retrieved From Server > > \n")


# source the main function
if __name__ == "__main__":
    main()
```

- Therefore, after running the above program; this is the output that I get:

```console
        -- Response Object: <Response [200]> --
           -- Response Status Code: 200 --

  --------------------------------------------------


        --------------------------------
           Data Retrieved From Server
        --------------------------------

        -- Pokemon ID: 25
        -- Pokemon Name: pikachu
        - Ability: static
        - Ability: lightning-rod

--------------------------------------------------
        -- Using Range Function --
--------------------------------------------------
        - Ability 1: static
        - Ability 2: lightning-rod
```

> [!INFO] What About Errors?
> Then, if we enter a Pokemon name such as '*Big Shitter*'... We are going to get this as output!
>
> ```console
>        -- Response Object: <Response [200]> --
>           -- Response Status Code: 200 --
>
>  --------------------------------------------------
>
> << Data For Pokemon 'Big Shitter' Could Not Be Retrieved From Server!!! > >
>
> << Error: Expecting value: line 1 column 1 (char 0) > >
> << Failed To Retrieve Data --> Status Code: 400 > >
>
>   --------------------------------------------
>   << Data Could NOT Be Retrieved From Server > >
> ```
>
> The *good* output above is from our `test` function. Nevertheless, I don't think that in the history of Pokemon we had one called "*Big Shitter*"!

# Corey Schafer's Video

> [!INFO] Resource(s)
> - 

> [!NOTE]
> As we now know the basics... *Thank You Bro Code For Teaching Millions Of Millions Of People*!!!
>
> I am now going to go and head straight in the *coding* / *implementation* part.

## Get The Raw HTML Page

Yes, we can use the `.text` method to be able to get the *raw data*, like the `.html` codes!

So there is a shitty website that I made for my friend Roy Paquiom... This is the link to the website ( *hosted on GitHub* )

> Link To Shitty Website ( *even if he got 'A' on it* ): https://zscary1403.github.io/RNT_Website

- Therefore, this is the code that we are going to use to output the *raw* HTML code:

> [!NOTE]
> <p align="center"> I just got carried away!!!</p>

```python
# import the 'request' module to be able connect to websites / APIs
import requests

# import the 'time' module to be able to use the `sleep` function
from time import sleep


# global variable that is going to hold the base URL for the website
BASE_URL: str = "https://zscary1403.github.io/RNT_Website/"


# function that is going to allow us to get the raw HTML codes from the website
def get_html_code(url: str = BASE_URL) -> str | None:
    # exception handling
    try:
        # use the `get` method to be able to get data from the server
        response = requests.get(url)

        # return the raw HTML codes to the "main" program
        return response.text

    # if we could not connect to the server
    except ConnectionError as e:
        # output appropriate message
        print(f"\n\t<< Error: {e} > > ")
        print("\t<< Could NOT Connect To The Server!!! > > \n")

        # therefore return `None` as we don't have any data
        return None

    # if we have a bad request to the server
    except requests.HTTPError as e:
        # output appropriate message
        print(f"\n\t<< Error: {e} > > ")
        print("\t<< Bad HTTP Status!!! > > \n")

        # therefore return `None` as we don't have any data
        return None

    # if we have a bad request to the server
    except requests.Timeout as e:
        # output appropriate message
        print(f"\n\t<< Error: {e} > > ")
        print("\t<< Took To Long To Connect!!! > > \n")

        # therefore return `None` as we don't have any data
        return None


# function to be able to write the HTML codes to an index file
def write_html_file(filename: str, html_code: str):
    # use the context manager to write data to the new file
    with open(f"{filename}.html", "w") as html_file:
        html_file.write(html_code)


# function to be able to display the content of the "freshly" created HTML file
def read_html_file(filename: str):
    # use the context manager to be able to read data from the file
    with open(f"{filename}.html", "r") as html_file:
        # read each line of the file instead of displaying the whole file
        for line in html_file:
            print(line.rstrip())
            sleep(0.1)


# our main function
def main():
    # declare and initalise variable that is going to hold the raw HTML codes
    raw_html_data = get_html_code()

    # check if we have data in the variable
    if raw_html_data:
        # meaning that we did retrieve the HTML code / data of the website
        # therefore as ask the user to enter the name of the HTML file
        user_filename: str = input("\nPlease Enter Name of HTML File: ")

        # call the function to be able to write the data to the file
        write_html_file(user_filename, raw_html_data)

        # call the function to display the data found inside the file
        read_html_file(user_filename)

    # else if some error occured above and `raw_html_data` is `None`
    else:
        # output appropriate message
        print("\n\t<< No HTML Codes Found... Error Occured When Fetching Data!!! > > \n")


# source the main function
if __name__ == "__main__":
    main()
```

> [!SUCCESS]
> If you were to run the above code, you are going to see that it output the *raw* HTML codes that the "*creator*" of that website coded himself / herself.
>
> It is also going to create a file in the **same** directory whereby the filename is entered by the user!
>
> > [!INFO]
> > The only thing that you should now its that we need to use the `response.text` *method*!
>

> [!WARNING] The **Exception Handling**
> Now, given that this is the **first** time that I am learning / using the `requests` module... I **don't** know anything about the *exceptions* / *errors* that can occur.
>
> Therefore, I asked [Claude](https://claude.ai) to list out a bunch of *errors* and how we can **handle** them!
>
> Therefore, I have added a some in the **above** code so that I can remember them and use them later on!

## Download Images

> Ouuhhh lala!!!

The `requests` *method* method that allows us to do that is the `.content` *function* / *method*. Therefore, let's find a "*good*" image on [Wallhaven](https://wallhaven.cc) and try to download it!

> Image that I am going to download: https://w.wallhaven.cc/full/1q/wallhaven-1qpqrw.jpg

> [!NOTE]
> The `.content` method is going to return us **binary** data... Therefore, we are going to have to write it into a `.jpg` file ( *in this case* ) using the `with` context manager.

- Therefore, this is the code that I wrote to be able to download the image ( *... I am not going to get carried now...* ):

```python
# import the 'request' module to be able connect to websites / APIs
import requests

# import the 'subprocess' module to be able run commands from Python
import subprocess

# global variable that is going to hold the URL for the actual image
IMG_URL: str = "https://w.wallhaven.cc/full/1q/wallhaven-1qpqrw.jpg"


# function to check if we have a response from the website itself
def response_status() -> requests.Response | None:
    # exception handling
    try:
        # use the `get` method to be able to requests and check website-server status
        response = requests.get(IMG_URL)

        # return the whole "reponse" data itself
        return response

    # if we could not connect to the server
    except ConnectionError as e:
        # output appropriate message
        print(f"\n\t<< Error: {e} > > ")
        print("\t<< Could NOT Connect To The Server!!! > > \n")

        # therefore return `None` as we don't have any data
        return None


# function that will write the binary data into an image file
def write_img_file(image_name: str, image_ext: str, server_response: requests.Response):
    # use the `with` context manager to write the image file
    with open(f"{image_name}{image_ext}", "wb") as img_file:
        # write the binary data to the file
        img_file.write(server_response.content)

    # in addition to writing the data to the "image" file ==> return the filename
    return f"{image_name}{image_ext}"


# our main function
def main():
    # call the function to check if server is "good"
    response_object = response_status()

    # check if the function did not return `None`
    if response_object:
        # check if the status code received is '200'
        if response_object.status_code == 200:
            # meaning that we can connect and retrieve data from the server
            # therefore, ask the user to enter the name of image file
            user_img_name = input("\nPlease Enter File Name Without Extension: ")

            # if the user enters the file name with the extension
            if user_img_name[-3::] == "jpg" or user_img_name[-3::] == "png":
                # then simply remove the extension from the file name
                user_img_name = user_img_name[:-4:]

            # therefore, write the data to image image file using the function
            image_filename = write_img_file(
                user_img_name, IMG_URL[-4::], response_object
            )

            # use the subprocess's `run` function / method to open my image viewer
            subprocess.run(["ristretto", image_filename])

        # if the status code is something else
        else:
            # output appropriate message
            print("\n\t<< Some Error Occurred Along The Way!!! > > \n")


# source the main function
if __name__ == "__main__":
    main()
```

> Fuck; I got carried away... *Its fucking fun*!!!

> [!SUCCESS]
> The above code is going to:
>
> 1. Check if the response from the `IMG_URL` is okay
> 2. If the `response_object` is **not** `None`
> 	- Check if the response's *status code* is `200`
> 	- Ask the user to enter the file name of the image that will be saved
> 	- Write the image to current the current directory ( *with appropriate image file extension* )
> 	- Open the image using my [Ristretto](https://gitlab.xfce.org/apps/ristretto) image file viewer
> 3. If the `response_object` **is** `None`
> 	- Display a little error message
>
> > [!INFO]
> > The only thing that you should know its that we need to use the *image*'s `response` itself with the `.content` *method* like so: `response.content`!
>

## Better Status Code Handling

> [!INFO] Resource(s)
> - API Testing: https://httpbin.org/
> - Mozilla Documentation: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status ( *added this again for reference purposes* )

Given that by now, we *kind-of* understand that to be able to work with the "*API*" ( *or website* ), we need to simply hope that the server returns a **response** of `200`!

Now, given that most of us is going to do something like this:

```python
# other codes above


# check if the response is '200' ==> "okay"
if response.status_code == 200:
	# other codes for working with response here


# more codes below
```

But as we are going to do this, or have something along the *lines* of the above code when working with the `requests` module... The `requests` module provides us with the `.ok` method to check if the *returned* **status code** is `200`!

```python
# import the 'request' module to be able connect to websites / APIs
import requests

# global variable that is going to hold the URL for the actual image
IMG_URL: str = "https://w.wallhaven.cc/full/1q/wallhaven-1qpqrw.jpg"


# function to check if the status response code is successfull ==> '200' returned status code
def status_code_success():
    # exception handling
    try:
        # use the `get` method to be able to requests and check website-server status
        response = requests.get(IMG_URL)

        # return the "ok" status code, i.e, 200
        return response.ok

    # if we could not connect to the server
    except ConnectionError as e:
        # output appropriate message
        print(f"\n\t<< Error: {e} > > ")
        print("\t<< Could NOT Connect To The Server!!! > > \n")

        # therefore return `None` as we don't have any data
        return None


# our main function
def main():
    # call the function to check if we can succuessfully connect to the API / website
    connection_success = status_code_success()

    # display is we have been able to successfully connected
    print(f"\n\tConnection Success Status: {connection_success}\n")


# source the main function
if __name__ == "__main__":
    main()
```

- Therefore, if we run the above code; the output is going to be like this;

```console
	Connection Success Status: True
```

> [!INFO] Testing Wrong URLs!
> What if we *alter* the `IMG_URL` so that is now looks like this:
>
> ```python
> # global variable that is going to hold the URL for the actual image
> IMG_URL: str = "https://w.wallhaven.cc/full/1q/wallhaven-1qpqrw.jpgniceonebrother"
> ```
>
> > Yes, I just added "*niceonebrother*" at the end of the URL!
>
> - Then running the above code, we are going to get something like this:
>
> ```console
> 	Connection Success Status: False
> ```

> [!TIP] My Chat With [Claude](https://claude.ai)
> - What actually `response.ok` do:
>
> ```python
> # response.ok is basically a shortcut for:
> response.ok == (200 <= response.status_code < 300)
> ```
>
> This is **way** better than just doing `200`, as looking at the *returned status codes*... We can see that we have a range of status code!
>
> For example the `GET` method is going to return '200' but the `DELETE` method is going / might return '204'.
>
> > [!TIP]
> > As from now on... Simply use the `.ok` *function* / *method*!
>

## HTTPS Headers

> [!INFO] Resource(s)
> - https://stackoverflow.com/questions/26745519/converting-dictionary-to-json

> Basically **meta-data** about the 'HTTPS' requests / response!

When using the `response.headers` *function* / *method*... Its going to return a [[Python - Dictionaries | Python Dictionary]].

```python
# import the 'request' module to be able connect to websites / APIs
import requests

# global variable that is going to hold the URL for the actual image
IMG_URL: str = "https://w.wallhaven.cc/full/1q/wallhaven-1qpqrw.jpg"


# our main function
def main():
    # variable to hold the entire reponse / request object
    response = requests.get(IMG_URL)

    # check if we have been able to connect to the API / website ( in this case image )
    if response.ok:
        # variable that will hold the 'HTTPS' metadata
        https_metadata = response.headers

        # display the key-pair value of the "dictionary" is a "asthetic" way
        print("\n{")

        # iterate through the dictionary and display the key-pair values
        for key, value in https_metadata.items():
            print(f"  {key}: {value},")

        print("}\n")

    # if the response was not successfull
    else:
        # output appropriate message
        print("\n\t<< Some Error Occurred On The Way!!! > > \n")


# source the main function
if __name__ == "__main__":
    main()
```

- Therefore, running the above code; I am going to get this as output:

> I am done some manually formatting as you can see!

```console
{
  Date: Sun, 19 Oct 2025 07:32:55 GMT,
  Content-Type: image/jpeg,
  Content-Length: 4505238,
  Connection: keep-alive,
  Server: cloudflare,
  Last-Modified: Sun, 28 Sep 2025 09:35:49 GMT,
  Nel: {"report_to":"cf-nel","success_fraction":0.0,"max_age":604800},
  ETag: "68d90175-44be96",
  Expires: Tue, 28 Oct 2025 09:37:53 GMT,
  Cache-Control: public, max-age=2592000,
  Pragma: public,
  Access-Control-Allow-Origin: *,
  Accept-Ranges: bytes,
  Age: 3061,
  cf-cache-status: HIT,
  Vary: accept-encoding,
  Report-To: {"group":"cf-nel","max_age":604800,"endpoints":[{"url":"https://a.nel.cloudflare.com/report/v4?s=8P2OOXNnVfOXKfLxJ0nrH7O1cEwGpGz1ZrydHMY08ixvQ2m4%2Fy%2FmXul5%2FhHyCJZbJD6%2B6WSktm7mLGSKYXq%2FszOIhMwfLooMZLej"}]},
  CF-RAY: 990e95949dc33876-MRU,
}
```

> [!TIP] I want more... But I don't know how to do it!
> Now, as you can see from the above output... We can see the **metadata** *fine* and *well*.
>
> But I wanted it too look like a '[[Python - JSON Module | JSON]]' output! Nevertheless, I don't know how to do that!
>
> > [!WARNING]
> > The variable `https_metadata = response.headers` is <strong> <span style="color: red;"> not</span> </strong> actually a *dictionary*!
> >
> > If we go ahead and use the `type` function on the `https_metadata` *variable*; we should see that we get and output that looks like so:
> >
> > ```console
> > <class 'requests.structures.CaseInsensitiveDict'>
> > ```
> >
> > > *Not something like*: `<class 'dict'> `!
> >
>
> What I am trying to say its that, if we want to display our "*dictionary*" with a pretty format using the 'JSON' module... Well, we are first going to have to convert `https_response` into an actual **Python Dictionary** with `dict()` **function**!
>
> Then as you know from '[[Python - JSON Module#Dumping / Creation Of New JSON Data | Python - JSON]]' *endeavour*; we can simply use the `.dumps` *function* / *method* with the argument `indent` passed through to **format** our dictionary into 'JSON' *format*!
>
> - The code below is just doing that:
>
> ```python
> # import the 'request' module to be able connect to websites / APIs
> import requests
>
> # import the 'json' module to be able display response data in 'JSON' format
> import json
>
>
> # global variable that is going to hold the URL for the actual image
> IMG_URL: str = "https://w.wallhaven.cc/full/1q/wallhaven-1qpqrw.jpg"
>
>
> # our main function
> def main():
>    # variable to hold the entire reponse / request object
>    response = requests.get(IMG_URL)
>
>    # check if we have been able to connect to the API / website ( in this case image )
>    if response.ok:
>        # variable that will hold the 'HTTPS' metadata
>        # NOTE: this is going to return a '<class 'requests.structures.CaseInsensitiveDict'> '
>        https_metadata = response.headers
>
>        # variable that holds the converted dictionary 'headers' data
>        https_metadata_dict = dict(https_metadata)
>
>        # iterate through the entire dictionary
>        for key, value in https_metadata_dict.items():
>            # check if the value of the key is a string
>            if isinstance(value, str):
>                # ( inner ) exception handling
>                try:
>                    # convert the data found at key into 'JSON' format and update key's value
>                    https_metadata_dict[key] = json.loads(value)
>
>                # if we cannot convert 'JSON' data
>                except json.JSONDecodeError:
>                    # leave it as be ==> not 'JSON' data --> therefore skip
>                    pass
>
>        # display the formatted string
>        print(json.dumps(https_metadata_dict, indent=2))
>
>    # if the response was not successfull
>    else:
>        # output appropriate message
>        print("\n\t<< Some Error Occurred On The Way!!! > > \n")
>
>
> # source the main function
> if __name__ == "__main__":
>    main()
> ```
>
> - Therefore, the output is going to look like this:
>
> ```console
> {
>  "Date": "Sun, 19 Oct 2025 08:01:32 GMT",
>  "Content-Type": "image/jpeg",
>  "Content-Length": 4505238,
>  "Connection": "keep-alive",
>  "Server": "cloudflare",
>  "Last-Modified": "Sun, 28 Sep 2025 09:35:49 GMT",
>  "Nel": {
>    "report_to": "cf-nel",
>    "success_fraction": 0.0,
>    "max_age": 604800
>  },
>  "ETag": "68d90175-44be96",
>  "Expires": "Tue, 28 Oct 2025 09:37:53 GMT",
>  "Cache-Control": "public, max-age=2592000",
>  "Pragma": "public",
>  "Access-Control-Allow-Origin": "*",
>  "Accept-Ranges": "bytes",
>  "Age": 4778,
>  "cf-cache-status": "HIT",
>  "Vary": "accept-encoding",
>  "Report-To": {
>    "group": "cf-nel",
>    "max_age": 604800,
>    "endpoints": [
>      {
>        "url": "https://a.nel.cloudflare.com/report/v4?s=GivvH2W4UkBYRo%2FkJsJP2qNZ%2FMSRSS%2B%2Fcyu%2BfmYpqmCFYYjx7xJgGeKYZ16NBJku75pF3fO5R8TJkXsz6P0om5z4m6mIVmUKaMZe"
>      }
>    ]
>  },
>  "CF-RAY": "990ebf805cf63874-MRU"
> }
> ```
>
> > [!NOTE]
> > The code that is used to convert the dictionary data is pretty much a standard... Therefore, I recommend to *learn it by heart*
> >
> > > Even though "*learning by heart*" is **fucked up**!!!
> >
>

## Making Requests - Getting Responses With 'httpbin.org'

Compared to the [PokeAPI](https://pokeapi.co/) that we used before when learning with [[#Bro Code's Video | Bro Code]]; the [httpbin.org](https://httpbin.org/) is going to allow us to use *all* the available methods to test with!

> [!TIP] Ohh My Fucking God!
> The guy who wrote the the [`requests`](https://requests.readthedocs.io/en/latest/) module for Python actually wrote the 'httpbin.org' *website*!

- Consider the following *simple* code found below:

```python
# import the 'request' module to be able connect to websites / APIs
import requests

# global variable that is going to hold the base URL for 'httpbin.org' website
BASE_URL: str = "https://httpbin.org/"


# our main function
def main():
    # variable initialise to hold the 'GET' method with "parameters"
    get_url: str = BASE_URL + "/get?name=John&age=30"

    # display the base URL and "get" URL ( URL with "search" parameters )
    print(f"\n  - Base URL: {BASE_URL}")
    print(f"  - 'GET' URL: {get_url}")

    print("\n" + "-" * 50, "\n")

    # get the response object from server
    response: requests.models.Response = requests.get(get_url)

    # display the output using the `.text` method
    print(response.text)


# source the main function
if __name__ == "__main__":
    main()
```

- This is going to output the <strong> <span style="color: orange;"> string</span> </strong> of:

```console
  - Base URL: https://httpbin.org/
  - 'GET' URL: https://httpbin.org//get?name=John&age=30

--------------------------------------------------

{
  "args": {
    "age": "30",
    "name": "John"
  },
  "headers": {
    "Accept": "*/*",
    "Accept-Encoding": "gzip, deflate",
    "Host": "httpbin.org",
    "User-Agent": "python-requests/2.32.5",
    "X-Amzn-Trace-Id": "Root=1-68f5d6dd-525ca4f2566aa68b06ad33c4"
  },
  "origin": "102.117.151.61",
  "url": "https://httpbin.org/get?name=John&age=30"
}
```

As you can see from the above output; after passing the *parameters* `/get?name=John&age=30`. You can clearly see that we have this also in the **string** ( *formatted to look like 'JSON'* ):

```console
  "args": {
    "age": "30",
    "name": "John"
  },
```

> [!INFO]
> If I go ahead and search for 'Mazda RX7 Feed' on [Google](https://google.com)... The **first** part of the URL is going to look like this:
>
> ```console
> https://www.google.com/search?q=Mazda+RX7+Feed
> ```
>
> > Again, this is *first* part of the URL; its much longer than that ( *that's what she said* )!
>

> [!WARNING] The `.text` Function / Method
> > Its actually so much more!
>
> In the above code whereby we used the `response.text` to be able *get* the '[[#Get The Raw HTML Page | HTML]]' codes!
>
> But man `.text` is so much **more** that just that... Let's change up the above code a bit and instead of using so that it now looks like this:
>
> ```python
> # import the 'request' module to be able connect to websites / APIs
> import requests
>
> # global variable that is going to hold the base URL for 'README.md' File
> BASE_URL: str = (
>    "https://raw.githubusercontent.com/Sunhaloo/archible/refs/heads/main/README.md"
> )
>
>
> # our main function
> def main():
>    # get the response object from server
>    response: requests.models.Response = requests.get(BASE_URL)
>
>    # use the `with` context manager to create a new file 'README.md'
>    with open("README.md", "w") as readme:
>        # write the contents found in 'README.md' file from server to local file
>        readme.write(response.text)
>
>
> # source the main function
> if __name__ == "__main__":
>    main()
> ```
>
> - Before running the above Python program, directory looked like this:
>
> ```console
>  .
> ├──  main.py
> └──  main.py.bak
> ```
>
> - After running my silly little Python program, I am going to get the `README.md` file inside my directory with all of its contents:
>
> ```console
>  .
> ├──  main.py
> ├──  main.py.bak
> └── 󰂺 README.md
> ```
>
> > Running a little `du -sh README.md`; you can clearly see that the file is **not** empty: `4.0K    README.md`!!!
>

### The Correct Way To Do Parameters

#### GET Method

From the above code, we used the variable `get_url` that **concatenates** the `BASE_URL` with `/get?name=John&age=30`; this is **dogshit**!

The *correct* or more safe way to do this is to use the `params` argument! Whereby `params` is going to look / *wants* a **dictionary**.

- Therefore, modifying the above code to work with dictionary:

```python
# import the 'request' module to be able connect to websites / APIs
import requests

# global variable that is going to hold the base URL for 'httpbin.org' website
BASE_URL: str = "https://httpbin.org/"


# our main function
def main():
    # ( dictionary ) parameters that we are going to use
    payload: dict[str, str | int] = {"name": "John", "age": 30}

    # pass the parameters get the response object from server
    # WARNING: don't forget to concatenate the `BASE_URL` with `/get`
    response = requests.get(BASE_URL + "/get", params=payload)

    # display the output using the `.text` method
    print(response.text)


# source the main function
if __name__ == "__main__":
    main()
```

> [!NOTE]
> This is simply going to return us the **same** output like above... Therefore, there is no need to paste it here again!
>
> > Additionally, I did *compare* the outputs and they are the **same**
>

#### POST Method

If we want to "*post*" some data to the server... Then the `requests.get` *function* / *method* `params` *argument* is **not** going to work!

We first have to change the `requests.get` method to the `requests.post` method. Then instead of using the `params` *argument*, we are going to have to use the `data` argument!

> Again the `data` argument is going to hold a `dict`ionary!

> [!WARNING] `GET` v/s `POST`
> Taking our example of the Google Search above, you can clearly see the *request* being made **directly** and the *parameters* that we are passing!
>
> > This is **not** the case with `POST`!
>
> Let's say that you are going to login to your [ClubPenguin](http://clubpenguin.com/) account... Do we want to "*show*" your **passwords** and other confidential data that you are entering.
>
> This means that we are **not** going to have something like this: `https://httpbin.org/get?name=John&age=30`. The actual **data** that is being sent / `POST`ed to the server is <span style="color: orange;"> hidden</span> in the *request* body itself.

- This is the code that will allow so to play with the `requests.post` method and *post* some data to the server:

```python
# import the 'request' module to be able connect to websites / APIs
import requests

# global variable that is going to hold the base URL for 'httpbin.org' website
BASE_URL: str = "https://httpbin.org/"


# our main function
def main():
    # data ( dictionary ) parameters that we are going to use
    payload: dict[str, str] = {
        "username": "JohnDoe6969",
        "email": "johndoe@email.com",
        "password": "your_mamaOn_me6969",
    }

    # use the `.post` method and pass our dictionary holding our data"
    # WARNING: in this case, instead of concatenating `/get` ==> use `/post`
    response = requests.post(BASE_URL + "/post", data=payload)

    # display the output using the `.text` method
    print(response.text)


# source the main function
if __name__ == "__main__":
    main()
```

- In my case, this is the output that I get:

```console
{
  "args": {},
  "data": "",
  "files": {},
  "form": {
    "email": "johndoe@email.com",
    "password": "your_mamaOn_me6969",
    "username": "JohnDoe6969"
  },
  "headers": {
    "Accept": "*/*",
    "Accept-Encoding": "gzip, deflate",
    "Content-Length": "74",
    "Content-Type": "application/x-www-form-urlencoded",
    "Host": "httpbin.org",
    "User-Agent": "python-requests/2.32.5",
    "X-Amzn-Trace-Id": "Root=1-68f5ec3f-71c931697cb9fad9399f1785"
  },
  "json": null,
  "origin": "102.117.151.61",
  "url": "https://httpbin.org/post"
}
```

> [!NOTE]
> But that does **not** means that the `requests.post` *function* / *method* does not have the `params` argument!
>
> > It Does!!!
>
> If I **replace** the line `response = requests.post(BASE_URL + "/post", data=payload)` with `response = requests.post(BASE_URL + "/post", data=payload, params=payload)`... You are going to see that the `args` *key* is going to have **values**.
>
> - This is the output that we should be expecting:
>
> ```console
> {
>  "args": {
>    "email": "johndoe@email.com",
>    "password": "your_mamaOn_me6969",
>    "username": "JohnDoe6969"
>  },
>  "data": "",
>  "files": {},
>  "form": {
>    "email": "johndoe@email.com",
>    "password": "your_mamaOn_me6969",
>    "username": "JohnDoe6969"
>  },
>  "headers": {
>    "Accept": "*/*",
>    "Accept-Encoding": "gzip, deflate",
>    "Content-Length": "74",
>    "Content-Type": "application/x-www-form-urlencoded",
>    "Host": "httpbin.org",
>    "User-Agent": "python-requests/2.32.5",
>    "X-Amzn-Trace-Id": "Root=1-68f5ee3d-48f627c7757867785a260deb"
>  },
>  "json": null,
>  "origin": "102.117.151.61",
>  "url": "https://httpbin.org/post?username=JohnDoe6969&email=johndoe%40email.com&password=your_mamaOn_me6969"
> }
> ```

### Using JSON Instead Of Text

Yes, we could also use 'JSON' instead of just using `.text`! Therefore, we are going to have more flexibility to *work* with the data!

- Updating the above code to work with 'JSON':

> By "*JSON*"... I meant to say **Python Dictionaries**!

```python
# import the 'request' module to be able connect to websites / APIs
import requests

# global variable that is going to hold the base URL for 'httpbin.org' website
BASE_URL: str = "https://httpbin.org/"


# our main function
def main():
    # data ( dictionary ) parameters that we are going to use
    payload: dict[str, str] = {
        "username": "JohnDoe6969",
        "email": "johndoe@email.com",
        "password": "your_mamaOn_me6969",
    }

    # use the `.post` method and pass our dictionary holding our data"
    # WARNING: in this case, instead of concatenating `/get` ==> use `/post`
    response = requests.post(BASE_URL + "/post", data=payload)

    # instead of using the `.text` method to display the `str` data ==> use `.json` method
    # place the output of the `response.json()` method inside a dictionary variable
    json_dict_data: dict = response.json()

    # display the value of the `form` key only
    print(json_dict_data["form"])


# source the main function
if __name__ == "__main__":
    main()
```

- Therefore, this is the output that we get after returning the 'JSON' data:

```console
{'email': 'johndoe@email.com', 'password': 'your_mamaOn_me6969', 'username': 'JohnDoe6969'}
```

### Singing Into httpbin.org

If we head back to our browser and type this URL:

```console
https://httpbin.org/basic-auth/JohnDoe6969/your_mamaOn_me6969
```

Then we are going to be prompted by the browser to ask us to input our **username** and **password**. If you enter any **other** username or password... Its going to ask you to enter the credential again.

- If you enter **your** username and password correctly... Then you are going to see this:

```json
{
  "authenticated": true,
  "user": "JohnDoe6969"
}
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!