---
id: Python - JSON Module
aliases: Javascript Object Notation ( JSON ) Module In Python
tags:
  - python
  - api
  - data-structures
  - dictionaries
author: S.Sunhaloo
date: 2025-10-15
status: HOLD
---

## List of Contents

- [[#Using The JSON Library]]
	- [[#Doing Everything On A Single File]]
		- [[#Loading The JSON Data]]
		- [[#Getting And Using Some Data]]
		- [[#Dumping / Creation Of New JSON Data]]
	- [[#Using A Separate File For JSON Data]]
		- [[#Opening JSON File For Reading]]
		- [[#Displaying Some Specific Data]]
		- [[#Dumping New Data Into Another File]]

---

> [!WARNING]
> This very file / note was created because of my notes on `requests` module
>
> > This is the note / file for my notes `requests`: '[[Python - Requests Module]]'
>
> I don't really know how to write this note / file... The `json` format is literally just a *dictionary*!
>
> Therefore, for you to be able to understand and work with `json`, you have to first understand how the `dict` datatype works in Python.
>
> > Please refer to the file / note '[[Python - Dictionaries]]' for more information!
>
> > [!INFO] Additionally...
> > The `json` module is part of Python's *standard library* therefore, we are **not** going to have to *install* anything here!
>

> Well Let's Get Started With It

> [!INFO] Resource(s)
> - Python Documentation: https://docs.python.org/3/library/json.html#module-json
> - Corey Schafer: https://www.youtube.com/watch?v=9N6a-VLBa2I

# Using The JSON Library

Here is a sample JSON *code* that I found on the [Mozilla Developer Website](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/JSON#json_structure):

```json
{
  "squadName": "Super hero squad",
  "homeTown": "Metro City",
  "formed": 2016,
  "secretBase": "Super tower",
  "active": true,
  "members": [
    {
      "name": "Molecule Man",
      "age": 29,
      "secretIdentity": "Dan Jukes",
      "powers": ["Radiation resistance", "Turning tiny", "Radiation blast"]
    },
    {
      "name": "Madame Uppercut",
      "age": 39,
      "secretIdentity": "Jane Wilson",
      "powers": [
        "Million tonne punch",
        "Damage resistance",
        "Superhuman reflexes"
      ]
    },
    {
      "name": "Eternal Flame",
      "age": 1000000,
      "secretIdentity": "Unknown",
      "powers": [
        "Immortality",
        "Heat Immunity",
        "Inferno",
        "Teleportation",
        "Interdimensional travel"
      ]
    }
  ]
}
```

In the above data, you can see that we have many *keys* and for the `members` key.

You are going to see that its *value* is a Python `list` containing more **dictionaries**!

> The `list` "*value*" contains 3 more `dicts`!

## Doing Everything On A Single File

Create our `main.py` Python file and then copy paste the above JSON *code* into a Python String ( *with the `"""` multiple-line string* ).

- I have created the `sample_json` variable that stores the entire thing like so:

```python
# import the 'json' entire module
import json

# variable to store the JSON data
sample_json: str = """
{
  "squadName": "Super hero squad",
  "homeTown": "Metro City",
  "formed": 2016,
  "secretBase": "Super tower",
  "active": true,
  "members": [
    {
      "name": "Molecule Man",
      "age": 29,
      "secretIdentity": "Dan Jukes",
      "powers": ["Radiation resistance", "Turning tiny", "Radiation blast"]
    },
    {
      "name": "Madame Uppercut",
      "age": 39,
      "secretIdentity": "Jane Wilson",
      "powers": [
        "Million tonne punch",
        "Damage resistance",
        "Superhuman reflexes"
      ]
    },
    {
      "name": "Eternal Flame",
      "age": 1000000,
      "secretIdentity": "Unknown",
      "powers": [
        "Immortality",
        "Heat Immunity",
        "Inferno",
        "Teleportation",
        "Interdimensional travel"
      ]
    }
  ]
}
"""
```

> [!WARNING] Friendly Warning
> **Don't** forget to import the `json` module at the top of our Python file!
> 
> > [!TIP]
> > The `json` module is part of the Python's *default* module library!
> > 
> > Therefore, no need to download anything with a package manager!

### Loading The JSON Data

To be able to use the data that is found inside the JSON "*string*" ( *in this case* ). We are going to make use of the `loads` function.

- Updating the `main.py` file like so:

```python
# load the JSON data into a variable called `json_data`
json_data = json.loads(sample_json)
```

Therefore, if we go ahead and use the `print` and `type` functions on the variable `json_data`.

```python
# display the "data" that is found inside the `json_data` variable
print(json_data)

# display the datatype of the data for our `json_data` variable
print(f"\n\t<< Data Type: {type(json_data)} > > \n")
```

> [!INFO] What does it returned?
> If you ran the above code, you should see that we basically get the same "*string*" that we created in `sample_json`.
> 
> But the real thing is... Its a **Python Dictionary**!!! Therefore, we could do some data manipulation on this `json` data!

### Getting And Using Some Data

Now that we have successfully loaded this data, we can use `dict` *functions* and *methods* to be able to **retrieve** the data that we want to.

Below you are going to find the code block of me retrieving some data from the `json_data`.

```python
# find the value associated with the key of `secretBase`
print(json_data["secretBase"], "\n")

# display all the key and the value of the 'json' data using the `item` method
for key, value in json_data.items():
    # check if the key is 'members'
    if key == "members":
        # display a horizontal rule
        print("\n" + "-" * 50, "\n")

        # iterate through the list of dictionaries of the 'members' value
        for members in value:
            # display the key and the associated value of each "members" key
            for mkey, mvalue in members.items():
                print(f"Members Key: {mkey} | Value: {mvalue}")

        # display a horizontal rule
        print("\n" + "-" * 50, "\n")

    # if the key was not a 'member'
    else:
        # display the data normally
        print(f"Key: {key} --> Value: {value}")
        
# get the names of the members
# INFO: we could have used `json_data.get("members")` but the docs says this method first
for member in json_data["members"]:
    # display the name of the members
    print(member["name"])
```

> [!INFO]
> The above code is a piece of shit code that I just wrote

- Running the above code, we should see that we get something like this:

```console
Super tower

Key: squadName --> Value: Super hero squad
Key: homeTown --> Value: Metro City
Key: formed --> Value: 2016
Key: secretBase --> Value: Super tower
Key: active --> Value: True

--------------------------------------------------

Members Key: name | Value: Molecule Man
Members Key: age | Value: 29
Members Key: secretIdentity | Value: Dan Jukes
Members Key: powers | Value: ['Radiation resistance', 'Turning tiny', 'Radiation blast']
Members Key: name | Value: Madame Uppercut
Members Key: age | Value: 39
Members Key: secretIdentity | Value: Jane Wilson
Members Key: powers | Value: ['Million tonne punch', 'Damage resistance', 'Superhuman reflexes']
Members Key: name | Value: Eternal Flame
Members Key: age | Value: 1000000
Members Key: secretIdentity | Value: Unknown
Members Key: powers | Value: ['Immortality', 'Heat Immunity', 'Inferno', 'Teleportation', 'Interdimensional travel']

--------------------------------------------------

Molecule Man
Madame Uppercut
Eternal Flame
```

### Dumping / Creation Of New JSON Data

But before, we "*dump*" that data somewhere else! Let us first go ahead and **remove** some data ( *key-value pair* ) found in our current JSON Python variable `json_data`!

#### Deleting Data From Our JSON Variable

This is the code that I wrote that is going to delete the *key-value* `secretBase` and the `powers` of the `members` *key*.

```python
# display the data before deleting anything
print("\n\t -- Data Before Deletion Of Key-Value Pairs --\n\n", json_data)

# delete the key-value pair for the key 'secretBase'
del json_data["secretBase"]

# iterate through the values of the 'members' key
for member in json_data["members"]:
    # delete all the 'powers' key-value pair of the members data
    # delete all the key-value pair for the key 'powers'
    del member["powers"]


# display the data after deleting anything
print("\n\t -- Data After Deletion Of Key-Value Pairs --\n\n", json_data)
```

> [!INFO]
> I am **not** going to be showing you the result of the output. Simply because the output is quite long ( *that's what she said* ).
> 
> But I think to give you proof that *data* has been **deleted** from `json_data`... Finding the length of the data, *before* and *after* deletion!
> 
> - Therefore, we if we run the following `len` code:
> 
> ```python
> # display the data before deleting anything
> print(f"Length Of Whole Dictionary Before Deletion: {len(json_data)}")
> # NOTE: we can simply do `['members'][0]` as the key's ( 'member' ) value is just a `list`
> print(
>     f"Length Of Inner 'members' `powers` Key-Value Dictionary Before Deletion: {len(json_data['members'][0])}"
> )
> 
> # display the data after deleting
> print(f"Length Of Whole Dictionary After Deletion: {len(json_data)}")
> # NOTE: we can simply do `['members'][0]` as the key's ( 'member' ) value is just a `list`
> print(
>     f"Length Of Inner 'members' `powers` Key-Value Dictionary After Deletion: {len(json_data['members'][0])}\n"
> )
> ```
> 
> - Therefore, we are going to have something like this:
> 
> ```console
> Length Of Whole Dictionary Before Deletion: 6
> Length Of Inner 'members' Dictionary Before Deletion: 4
> Length Of Whole Dictionary Before Deletion: 5
> Length Of Inner 'members' Dictionary Before Deletion: 3
> ```

#### Create A New JSON Data Thing

Now that we have *updated* our `json_data` variable... Let's create a new variable that is going to hold the actual `json` *thing* instead of that Python dictionary.

```python
# create a new string that is going to hold the new data
new_json_data = json.dumps(json_data)

# display the new JSON data created from `dumps`
print(new_json_data)
```

- Therefore, we are going to get this very ( *ugly* ) output right here:

```console
{"squadName": "Super hero squad", "homeTown": "Metro City", "formed": 2016, "active": true, "members": [{"name": "Molecule Man", "age": 29, "secretIdentity": "Dan Jukes"}, {"name": "Madame Uppercut", "age": 39, "secretIdentity": "Jane Wilson"}, {"name": "Eternal Flame", "age": 1000000, "secretIdentity": "Unknown"}]}
```

##### Beautify The Output!

But this is complete shit... No one has the time to go to online and find a JSON **formatter**!

> This is why I really, really recommend code formatters! Your 'IDE' should have it or download some extensions!

Therefore the `dumps` *function* / *method* comes with some arguments that we can use to make the output **prettier**!

> That is the [formatter](https://github.com/prettier/prettier) that I use in Neovim!

```python
# create a new string that is going to hold the new data
# pass the additional parameters to be able to have good JSON formatting
new_json_data = json.dumps(json_data, indent=2, sort_keys=True)

# display the new JSON data created from `dumps`
print(new_json_data)
```

> [!INFO] What is the above code going to do?
> The above code is going to make the JSON output **not** simply on a single line and actually like provides good indentation.
>
> Then its going to sort the keys in **alphabetical** order; after all of that, it is now that `dumps` is going to *put* that *new* data into the variable `new_json_data`.

- Hence, we should now see a **beautiful** output just like this:

```console
{
  "active": true,
  "formed": 2016,
  "homeTown": "Metro City",
  "members": [
    {
      "age": 29,
      "name": "Molecule Man",
      "secretIdentity": "Dan Jukes"
    },
    {
      "age": 39,
      "name": "Madame Uppercut",
      "secretIdentity": "Jane Wilson"
    },
    {
      "age": 1000000,
      "name": "Eternal Flame",
      "secretIdentity": "Unknown"
    }
  ],
  "squadName": "Super hero squad"
}
```

## Using A Separate File For JSON Data

In the above section, we have seen how we can deal with the JSON data if it was in a Python `str`ing variable!

But a *small* JSON file could have over 1000 lines of code! We would definitely **not** want that to be stored in a single `str`ing variable!

Therefore, we can simply use the `with` *context* to simply open the file and use some *functions* / *methods* that are found inside the `json` module to be able to **get** our data!

### Opening JSON File For Reading

> Basically file handling in Python!

To open *any* file in Python, the best and most Pythonic way is to use the `with` *context*. Therefore, we are going to have this code below that is going to open the file for us!

> [!INFO]
> My current directory structure looks like this:
>
> ```python
>  .
> ├──  api.json
> └──  main.py
> ```
>
> Now, the `api.json` file is a file that I just downloaded from the internet and it's '4 KB' in size and has '43' line of *data*!
>
> > To put it simply, the *data* inside the **variable** `sample_json` is **not** the same at the `api.json` *data*
>

```python
# import the 'json' module to be able to handle `json` files
import json


# function that will be able to open the `.json` file and get its data
def load_json_data(file: str):
    # exception handling
    try:
        # open the file for reading
        with open(file, "r") as json_file:
            # use the `load` function to load the data
            # WARNING: we are using `json.load` instead of `json.loads`
            json_data = json.load(json_file)

        # finally return the data to the "main" program
        return json_data

    # if the file has not been found
    except FileNotFoundError as e:
        # output appropriate message
        print(f"\n\t<< Error: {e} > > ")
        print("\t<< File Has Not Been Found!!! > > \n")

    # if the `.json` file contains some syntax errors or is not really a `.json` file
    except json.JSONDecodeError as e:
        # output appropriate message
        print(f"\n\t<< Error: {e} > > ")
        print(
            f"\t<< Invalid JSON Syntax Found: Line = {e.lineno} - Column {e.colno}!!! > > \n"
        )


# our main function
def main():
    # initialise a variable that will hold the JSON data of the file
    data = load_json_data("api.json")

    # therefore, display the data found inside the 'api.json' file
    print(data)


# source the main function
if __name__ == "__main__":
    main()
```

> [!WARNING] Difference Between `json.loads` and `json.load`!
> If you look at the official Python documentation, over at:
>
> - https://docs.python.org/3/library/json.html#json.loads
> - https://docs.python.org/3/library/json.html#json.load
>
> Yes, there are two "*load*" `json` functions / methods! This is because we have have our JSON data in a `str`ing variable or we have have our JSON data inside an actual `.json` file.
>
> Therefore, Python gives us the two *methods* found above!
>
> - The `json.loads` ( *with 's'* ) will load data from a **string** variable
> - The `json.load` will load data from a file
>
> > That is the **only** difference that I can personally seen from these two!
>

### Displaying Some Specific Data

> [!INFO] How my `api.json` files look like?
> This is how the contents inside my `api.json` file looks like:
>
> ```json
> {
>  "name": "Richard",
>  "age": "33",
>  "hobbies": ["Biking", "Gaming", "Squash"],
>  "city": "Port Land",
>  "friends": [
>    {
>      "name": "Chris",
>      "age": 23,
>      "city": "New York"
>    },
>    {
>      "name": "Emily",
>      "age": 19,
>      "city": "Atlanta"
>    },
>    {
>      "name": "Joe",
>      "age": 32,
>      "city": "New York"
>    },
>    {
>      "name": "Kevin",
>      "age": 19,
>      "city": "Atlanta"
>    },
>    {
>      "name": "Michelle",
>      "age": 27,
>      "city": "Los Angeles"
>    },
>    {
>      "name": "Robert",
>      "age": 45,
>      "city": "Manhattan"
>    },
>    {
>      "name": "Sarah",
>      "age": 31,
>      "city": "New York"
>    }
>  ]
> }
> ```

As you can see from my `api.json` file, I have a `friend` **key** that has a "*value*" ( *or datatype* ) of `list[dict]`!

Therefore, for us to be able to access the **value of the `name` _key_**; we are first going to have to:

- Iterate through the Python `list` itself
- Access each `dict`ionaries `name` key and display their corresponding value

> In the code below, I show the "*Pythonic Method*" and also using the `range` function!

```python
# our main function
def main():
    # initialise a variable that will hold the JSON data of the file
    data = load_json_data("api.json")

    # iterate through the list of dictionary objects
    for friend in data["friends"]:
        # not that our `friend` variable is going to hold each dictionary
        # we can therefore use the "index" of dictionary to access the names!
        print(f"Name: {friend["name"]}")

    print("\n" + "-" * 50, "\n")

    # if we were to use the `range` function to iterate through
    # then the above code is going to look something like this

    # get the length of the "friends" list
    for i in range(len(data["friends"])):
        # 1. `data["friends"]` ==> get the whole "friends" list itself
        # 2. `data["friends"][i]` ==> access each dictionary inside the list
        # 2. `data["friends"][i]["name"]` ==> access the values of the 'name' key
        print(f"Name {i + 1}: {data["friends"][i]["name"]}")


# source the main function
if __name__ == "__main__":
    main()
```

> I am only showing you our `main` function as the above function is still the **same**!

- Therefore the output that we are going to have for this program is going to be like so:

```console
Name: Chris
Name: Emily
Name: Joe
Name: Kevin
Name: Michelle
Name: Robert
Name: Sarah

--------------------------------------------------

Name 1: Chris
Name 2: Emily
Name 3: Joe
Name 4: Kevin
Name 5: Michelle
Name 6: Robert
Name 7: Sarah
```

### Dumping New Data Into Another File

> [!INFO] Same situation as `loads` and `load`!
> We also have the same situation here whereby we are going to use:
>
> - The `dumps` *method* for dumping data to a **string** variable
> - The `dump` *method* for dumping data to a **file**
>
> > Simply put, we are going to be using `json.dump` instead!
>

- This it the function that is going to create another file called `new_json.json` and add our **new** data

```python
# function that will be able to create a new file with updated JSON data
def write_json_data(new_data, filename: str):
    # open the new file for writing
    with open(filename, "w") as new_json_file:
        # dump the new data to the new file
        json.dump(new_data, new_json_file, indent=2)
```

#### Delete Some Data Before Writing New File!!!

> I am simply going to show you the `main` function that I wrote!

```python
# our main function
def main():
    # initialise a variable that will hold the JSON data of the file
    data = load_json_data("api.json")

    # iterate through the list of dictionary objects
    for friend in data["friends"]:
        # not that our `friend` variable is going to hold each dictionary
        # we can therefore use the "index" of dictionary to delete the age!
        del friend["age"]

    # call the function to write the new data to a "new" file
    write_json_data(data, "new_file.json")


# source the main function
if __name__ == "__main__":
    main()
```

- Therefore, this is what the new file, `new_file.json` looks like:

```json
{
  "name": "Richard",
  "age": "33",
  "hobbies": [
    "Biking",
    "Gaming",
    "Squash"
  ],
  "city": "Port Land",
  "friends": [
    {
      "name": "Chris",
      "city": "New York"
    },
    {
      "name": "Emily",
      "city": "Atlanta"
    },
    {
      "name": "Joe",
      "city": "New York"
    },
    {
      "name": "Kevin",
      "city": "Atlanta"
    },
    {
      "name": "Michelle",
      "city": "Los Angeles"
    },
    {
      "name": "Robert",
      "city": "Manhattan"
    },
    {
      "name": "Sarah",
      "city": "New York"
    }
  ]
}
```

> [!SUCCESS]
> As you can see, we **don't** have our `age` *key-value* pair in our new JSON file!
>
> Additionally, I did use the `indent=2` argument inside the `json.dump` function / method to be able to get this formatting!
---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!