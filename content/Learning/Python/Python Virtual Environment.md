---
id: Python Virtual Environment
aliases: Python Virtual Environment - venv
tags:
  - python
  - linux
author: S.Sunhaloo
date: 2025-08-21
status: Completed
---

## List of Contents

- [[#Creation and Usage of Python Virtual Environment]]
	- [[#Creation of Python Virtual Environment]]
	- [[#Activating The Python Virtual Environment]]
- [[#Playing With It!!!]]
- [[#Deactivate Python Virtual Environment]]

---

> [!INFO] Resources
> - https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/
> - https://docs.python.org/3/library/venv.html
> - https://medium.com/@lucasthedev/a-comprehensive-guide-to-python-virtual-environments-with-venv-cb76fea6a550
> - https://pip.pypa.io/en/stable/index.html
> - https://pypi.org/

> [!INFO] Python Version
> My version of Python that I have been using for this *learning* note was 'Python 3.13.7'
>
> > Which was basically the latest version of Python at the time of making this very note!
>


# Creation and Usage of Python Virtual Environment

## Creation of Python Virtual Environment

- Go ahead and create a "*testing*" folder

> In in my case, I created the `Testing` folder under the `~/Desktop` directory

```bash
# create the 'Testing' folder found inside the 'Desktop' directory
mkdir -p ~/Desktop/Testing

# change the current working directory to that 'Testing' folder
cd ~/Desktop/Testing
```

- **Create** the *Python Virtual Environment*:

```bash
python -m venv virtual_env
```

> [!INFO]
> The above command will go ahead an **create** ( *yes, only create* ) the Python Virtual Environment with the `virtual_env` name.
>
> > [!TIP] Common Convention To Naming Python Virtual Environment
> > The common *name* that programmers used to call their virtual environment is `.venv`!
>
> > [!WARNING] Using the `.venv` Name
> > The above command to **create** a Python Virtual Environment is going to actual create a **folder** with that name that you provided.
> >
> > In my case, as I used the *name* `virtual_env`. Python create a folder with *said* name in the `~/Desktop/Testing/` directory.
> >
> > Therefore, using the name that starts with the character `.`... "_Well its going to create a **hidden folder**_!!!"
>

## Activating The Python Virtual Environment

Now that we have *created* the virtual environment; we can't really do anything with it in its current state.

To be able to use that virtual environment, we first need to **activate** it.

### Steps To Activate Virtual Environment

- Head inside our `virtual_env` directory / *virtual environment*:

```bash
# head inside the virtual environment directory
cd virtual_env
```

> Windows Users

```powershell
# activate the python environment
.\Scripts\activate.bat
```

> Linux / MacOS Users

```bash
# activate the python environment
source /bin/activate
```

> [!NOTE]
> I mean, we can **activate** the Python Virtual Environment from **outside** the `virtual_env` folder...
>
> > But really what's the fucking point!
>
> We do have to go inside of it to be able to leverage the actual power of the Python Virtual Environment
>
> > [!WARNING] Arch Linux
> > As you might now, Arch Linux discourages the use of package managers like `pip`, which was previously **system-wide**.
> >
> > This was due to the fact that some packages from `pacman` were in *conflict* with `pip`.
> >
> > This means that you generally **cannot** install `pip` anymore!
> >
> > > From what I know of!
> >
> > But after **activating** the Python Virtual Environment, I can see that even if I go, for example, to my *home directory*. I still see that I am using the virtual environment. Therefore, I get do get the `pip` command.
> >
> > > But don't be fooled! _It is **system-wide**_
> >
> > Everything that you are going install with `pip` is going to get installed in the `virtual_env_name/lib` and `virtual_env_name/bin` folders!
> >
> > > As you can see not our `/bin` or `/usr/bin` folder found inside our system!
> >
>

---

# Playing With It!!!

## Installing Python Packages / Modules

To install Python modules or other Python packages, we can use `pip`!

> For more information about `pip`, see the link found above!

Now, let's go ahead and install some simple **modules** using `pip` in our *Python Virtual Environment*.

- Install the [numpy](https://pypi.org/project/numpy/) Module:

```bash
# install the famous 'numpy' module
pip install numpy
```

- Install the [requests](https://pypi.org/project/requests/) Module:

```bash
# install one of the other famous 'requests' module
pip install requests
```

- Install the [json5](https://pypi.org/project/json5/) Module:

```bash
# install the 'json5' module
pip install json5
```

> [!NOTE]
> For more information about using `pip` or installing other packages... Again please refer to the documentation

## Requirements File

Let' say that we have been locked in and we have been coding something that is super revolutionary to no one!

Let's say that we want to test it in **another** virtual environment... But there is a little problem...

> You have a lot of *modules* / *packages* installed!!!

Yes, you have installed a lot of *modules* / *packages* and other types of dependencies and you want to have an *easy* time **installing** these *modules*!

> Well Python has got you covered!

- Simply run the following command below to get all the "*packages*" installed!

```bash
# get all the modules / packages / dependencies installed
pip freeze > requirements.txt
```

> [!INFO]
> I mean you could use other names like `shitter.txt` or `bitch.txt` but `requirements.txt` is the **convention** for a reason right!

In my case the contents of the `requirements.txt` file looks like this:

```console
certifi==2025.8.3
charset-normalizer==3.4.3
idna==3.10
json5==0.12.1
requests==2.32.5
urllib3==2.5.0
```

### Using The `requirements.txt` File

- Create **another** *Virtual Environment* with the name `new_venv`:

```bash
# create another virtual environment
python -m venv new_venv
```

- Activate this new virtual environment:

```bash
# head inside the new virtual environment directory
# NOTE: I created the 'new_venv' folder inside the '~/Desktop/Testing' directory
cd new_venv

# activate the new python project
source /bin/activate
```

- Now move the `requirements.txt` file inside the **newly** created Python Virtual Environment

> I think you know how to use the `mv` command... If not "*Read The Fucking Manual*!!!"

#### Actual Install Modules / Packages / Dependencies

Again, now that we have the `requirements.txt` file inside our new Python Virtual Environment and we are now ready to install all the *modules* / *packages* that we are going to need.

- Check the contents of the `new_venv/lib/python3.13/site-packages/` directory / folder **before** installing anything

```console
-  pip
-  pip-25.2.dist-info
```

- Run the following command found below to install all the required *dependencies*:

```bash
# install all the required modules
python -m pip install -r requirements.txt
```

> This should install everything that we have in our `requirements.txt` file.

> [!INFO]
> You don't really need the `python -m` in the beginning of the line of the **command**!

> [!SUCCESS]
> Well here we have it! We have now **successfully** all the required "*modules*" on our **new** Python Virtual Environment!
>
> ```console
> -  certifi
> -  certifi-2025.8.3.dist-info
> -  charset_normalizer
> -  charset_normalizer-3.4.3.dist-info
> -  idna
> -  idna-3.10.dist-info
> -  json5
> -  json5-0.12.1.dist-info
> -  pip
> -  pip-25.2.dist-info
> -  requests
> -  requests-2.32.5.dist-info
> -  urllib3
> -  urllib3-2.5.0.dist-info
> ```

# Deactivate Python Virtual Environment

> [!INFO] Apparently You <em> <span style="color: orange;"> Don't</span> </em> Have To!!!
> > Its more of a "*discipline*" thing!
>

Now, that you have done your little coding session for the day... To **deactivate** the Python Virtual Environment... Simply run the following "*one-word*" command:

```bash
# deactivate the python virtual environment
deactivate
```

> Or you could just **close** and **re-open** your lovely terminal!

> [!SUCCESS]
> Therefore, in my case, if I try to run something like `pip install numpy`... I should **get** an *error*!
>
> ```console
> zsh: command not found: pip
> ```
>
> > Very Nice!
>

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!