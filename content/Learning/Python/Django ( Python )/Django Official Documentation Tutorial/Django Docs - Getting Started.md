---
id: Django Docs - Getting Started
aliases: Python Django Documentation - Installation and Setup
tags:
  - python
  - django
  - basics
author: S.Sunhaloo
date: 2025-08-22
status: Completed
---

## List of Contents

- [[#What is Django?]]
- [[#The Setup]]
	- [[#Installing Django]]
- [[#Writing Our First Program]]
	- [[#Inspecting Files]]
- [[#Run The Local Development Server]]
- [[#Creation of Apps ( Web Pages )]]
	- [[#Setup The Application]]
		- [[#Register The Application]]
	- [[#Working With The Application]]
		- [[#Writing Our View]]
		- [[#Map Out The View]]
		- [[#Map Out The View To The Project]]

---

> [!INFO]
> - https://docs.djangoproject.com/en/5.2/
> - https://docs.djangoproject.com/en/5.2/topics/install/#installing-official-release
> 	- https://code.djangoproject.com/wiki/Distributions
> - https://docs.djangoproject.com/en/5.2/intro/tutorial01/

> [!WARNING]
> You might need to run `python3` **instead** of  `python`!
>
> I don't even have an *alias*, its just that I when I installed Arch, it was like this.

# What is Django?

Django is a **high-level Python web framework** that helps you build web applications **fast**, while handling a lot of the “hard stuff” for you.

A **web framework** is basically a toolkit of libraries, rules, and components that lets you build websites or web apps without reinventing the wheel every time.

# The Setup

## Requirements

- [Python](https://www.python.org/downloads/)
	- `pip` Python Package Manager
- Terminal Emulator
	- [Windows People](https://www.youtube.com/watch?v=bKcgfVCFKZU): [Windows Terminal](https://github.com/microsoft/terminal)
	- Linux People: [Kitty](https://github.com/kovidgoyal/kitty) $\leftarrow$ My Personal Favourite!

### Installing Django

The following code block below will show you how to install Django.

> Just look for you specific Operating System!

```console
# using `pip` python package manager
# NOTE: this should work for most Windows and MacOS users
python -m pip install Django

# debian / debian based distribution
sudo apt-get install python-django

# I use Arch BTW
sudo pacman -S python-django
```

> As I am on Arch Linux; I will be using `pacman` to install the `python-django` package!

> [!SUCCESS] Verification of Installation of Django
> To verify the installation of Django on our system, we can use the following command:
>
> ```bash
> # get the version of django installed on our system
> python -m django --version
> ```
>
> Therefore, at the time of making this note, I get the following output:
>
> ```console
> 5.1.11
> ```

---

# Writing Our First Program

I am going to use my Private [[Git Data View | Git]] Repository whereby I am going to create a folder with the name `django_testing` whereby I will then create the **project** inside.

```bash
# in my private repository's directory
# create and change directory to newly created folder
mkdir django_testing && cd django_testing
```

- Use the following command to **create** / **initialise** the *Django project*:

```bash
# create a new django project
django-admin startproject site_test
```

- After running the following command we should see that we get the `site_test` directory / folder inside our `django_testing` folder

```console
 .
├──  manage.py
└──  site_test
    ├──  __init__.py
    ├──  asgi.py
    ├──  settings.py
    ├──  urls.py
    └──  wsgi.py
```

## Inspecting Files

As I like to learn about programming and coding in general... I am going to *follow* the documentation so that I can learn what the **Python files** do!

### `manage.py` File

It is the one that provides us with the *command line utility* that allows us to **interact** with our Django project.

> Link: https://docs.djangoproject.com/en/5.2/ref/django-admin/

The `manage.py` does the **same** thing as the `django-admin` command. In addition to that, it also sets the `DJANGO_SETTINGS_MODULE` in our project's `<project-name> /settings.py`

> [!TIP] Tip: "*They are saying that...*"
> If you are working on a **single** Django project, they are saying that its easier to use the `manage.py` *Python file* instead of the `django-admin` command.
>
> > I thought that this was going to be fucking hard to do but its actually pretty simple...
> > I am going to show you how we can use the `manage.py` *file* **instead** of the `django-admin` command.
>

### `<project-name> /__init__.py` File

This is basically the way that Python "*sets*" packages or modules. For example, if you are working with a large Python project with many files and folders... I think you should see that they used the `__init__.py` file.

This is because *every time* that you have the `__init__.py` file inside a folder. Python will treat this folder as a **package**.

> Therefore, in our case, we can say that the `site_test` folder is a **package**!

> [!TIP] Python Folders and Packages
> This is purely a Python *thing*. If you were also making a "*pure*" Python program.
>
> You would also ( *optionally* ) use the `__init__.py` file to tell Python that that you have created a little packages.

> [!INFO]
> You can learn about them more here: https://docs.python.org/3/tutorial/modules.html#tut-packages
>
> > The above will go straight to the official Python documentation!
>

### `<project-name> /settings.py` File

> Think of this file as the **control panel** for our Django Project!

Its the file where we can configure things like:

- Basic Project Setup
	- Like: `ALLOWED_HOSTS` ( *localhost and others* ) and `DEBUG`ging
- Installed Django Applications
- Database Configuration
- Static and Media Files
	- What folder *name* to use to keep "*static*" data
- Authentication + Localisation

> Link: https://docs.djangoproject.com/en/5.2/topics/settings/

### `<project-name> /urls.py` File

> Think of the `urls.py` file as a *map* of the whole **website**.

As the name of the file suggests... It will keep track and allow us to **navigate** to our different webpages that we have inside our website.

> [!NOTE] Concepts of *Apps*, *URLs* and *Views*!
> So let's say that we are making a simple website **without** any *frameworks*. Given that we have the following files in our directory:
>
> ```console
>  .
> ├──  about.html
> ├──  index.html
> ├──  login.html
> └──  style.css
> ```
>
> > Let us now try to convert this into its "*Django Framework*" equivalent!
>
> Now, to actually make a *simple* website in Django, we are going to have to create an **app**!
>
> > The creation of said "*app*" is done using the command `startapp <app-name> `
>
> This is going to modify our `<project-name> ` directory to include the directory `<app-name> `
>
> ```console
>  .
> ├──  __init__.py
> ├──  admin.py
> ├──  apps.py
> ├──  migrations
> │   └──  __init__.py
> ├──  models.py
> ├──  tests.py
> └──  views.py
> ```
>
> All these files that has been created technically does <em> <span style="color: orange;"> not</span> </em> contain any code!
>
> > It's us who has to actual code things now!
>

### `<project-name> /asgi.py` and `<project-name> /wsgi.py` Files

These files are used to **deploy** our servers using '[ASGI](https://docs.djangoproject.com/en/5.2/howto/deployment/asgi/)' and '[WSGI](https://docs.djangoproject.com/en/5.2/howto/deployment/wsgi/)'

> I am **not** going to worry about them right now...

# Run The Local Development Server

- Execute the following command to **run** the Django's "*internal*" development server:

```bash
# run Django's development server
python manage.py runserver

# if you want to change the port, then run the this command
python manage.py runserver 8080
```

- Output after running the *second* command:

```console
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).

You have 18 unapplied migration(s). Your project may
not work properly until you apply the
migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.
August 23, 2025 - 11:25:34
Django version 5.1.11, using settings 'site_test.settings'
Starting development server at http://127.0.0.1:8080/
Quit the server with CONTROL-C.
```

Therefore, go ahead an open the "*localhost*" link `http://127.0.0.1:8080/` and you should see that the "*Congratulations*" page running!

> [!SUCCESS]
> We have successfully been able **start** and **run** the server!

> [!TIP] `manage.py` V/S `django-admin`
> This is what the documentation was saying!
>
> Instead of using something like `django-admin runserver`! We instead used the following:
>
> ```bash
> # using 'manage.py' instead of `django-admin`
> python manage.py runserver
> ```

---

> [!INFO] Difference Between **Project** and **App**
> In Django, the term '*Project*' can be considered as the whole [englobement](https://en.wiktionary.org/wiki/englobement) of the *webpages* and *configurations* of the website!
>
> While the term, '*app*', is considered to be **web application** that does *something*. That "*something*" can be anything from a simple blog to a fully developed website!
>
> > Think of the '*app*' as a "*mini webpage module*" that encompass its `.html` and `.css` and any other static or media related files.
> >
> > A **single _Project_** could contain **multiple _Apps_**!
>

---

# Creation of Apps ( Web Pages )

> [!WARNING]
> Before we go ahead and create our first application... Make sure that your *current working directory* contains the `manage.py` file.
>
> In my case this is going to be `django_testing/site_test`!

I am now going to create an *application* call 'test_app'. Hence, I am going to run the following command found below:

```bash
# create a new application with the name 'test_app'
python manage.py startapp test_app
```

Hence, we should see that we have a new directory with the **same** name as our application.

```console
.
├── manage.py
├── site_test
└── test_app
```

> [!INFO] Like I Mentioned Above
> This is what the contents of the directory `test_app` looks like:
>
> ```console
>  .
> ├──  __init__.py
> ├──  admin.py
> ├──  apps.py
> ├──  migrations
> │   └──  __init__.py
> ├──  models.py
> ├──  tests.py
> └──  views.py
> ```

## MVT Concept

'*MVT*' stands for:

- Models
- Views
- Templates

This is how Django's overall hierarchy works whereby we do have a `models.py` and `views.py` and we need to create the `templates` folder.

> [!TIP] Understanding What Each Does!
> - Models:
> 	- Responsible for **processing** our *data*
> 	- The `models.py` file is going to be *linked* to our **databases**!
> - Views:
> 	- Deals with the **logic** part of our application
> 	- Handling **user interactions** for our application
> 	- *Processing* of **user requests**
> - Templates:
> 	- Basically what the user will **see** / *front-end*
> 	- The '*UI / UX*' part of the website
> 	- How the user will primarily interact with the website

## Setup The Application

There is one more thing that we need to do before we are done with the "*setup*" stuff for 'Creation of Apps'.

> We need to **Register** the application!

### Register The Application

Go ahead and open the `site_test/settings.py` file and then search for the list with the identifier name `INSTALLED_APPS`. Hence, you should see something like this:

```python
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
]
```

Therefore, we need to make sure that we include **our** `test_app` application so that when we are going to use *databases* and other tools. Django will know about them!

- Therefore, add our application to the Python list `INSTALLED_APPS`:

```python
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
    
    # register our newly created `test_app` app
    "test_app",
]
```

## Working With The Application

### Writing Our View

To create our first, ever view... Ever! We are going to head into the Python File found over at `test_app/views.py`.

```bash
# change my working directory to the newly created app
cd test_app

# open the 'views.py' file
# INFO: use your preferred code editor
nvim views.py
```

#### Creation Of Front Page

We are now going to emulate the creation of our `index.html` file. Therefore, we are going to have to modify our `views.py` file so that Django know that is needs to **render** it.

```python
from django.http import HttpResponse


def index(request):
    return HttpResponse("'Hello World' from test's app index page")
```

### Map Out The View

Currently, Django does <span style="color: orange;"> not</span> know where that "`index.html`" file is stored.

> As we can have **multiple** *applications* inside a **single** *project*...

We need to tell Django where that "`index`" page is located at! Hence, we have to create a `urls.py` file **in the same `test_app` directory**

- Add the following contents to the `urls.py` file:

```python
from django.urls import path
from . import views

urlpatterns = [
	# as I don't want the user to type a specific URL
	# for example instead of 'test_app/something_here'
	# I just want to get access quickly therefore 'test_app'
    path("", views.index, name="index"),
    
    # NOTE: if wanted to do 'test_app/something'
    # would have typed 'something/' and passed that as
    # our first arguement in the `path` function
]
```

> Again, this is <span style="color: red;"> not</span> the `site_test/urls.py` file.
> This is a file that *we* **created** over at `test_app/urls.py`!

### Map Out The View To The Project

Now, we are going to have to tell the **main** Django `site_test` *project* that we are have created a **view** for the `test_app` app.

- Include the view path to the project's `urls.py` file

```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    # add the path to the URLconf file for 'test_app'
    path("test_app/", include("test_app.urls")),
    path("admin/", admin.site.urls),
]
```

> [!NOTE] When To Use `include()` Function?
> We need to use the `include()` function whenever we need to **add** URLs from *other* applications.

---

### Run The Server Again

If we go ahead and run the following command to run the *development server* again:

```bash
# run the server again
python manage.py runserver
```

> [!WARNING] Error!
> <p align="center"> <em> Page not found (404)</em> </p>
>
> This is because at the "*root*", i.e `http://127.0.0.1:8000/`; we have **not** yet defined anything!
>
> Therefore, to actually see our little message that we created in our `test_app` app. We need to head to this **URL**:
>
> ```console
> https://127.0.0.1:8000/test_app
> ```
>
> > [!SUCCESS]
> > Therefore, we should see that we get our little message that we have in our `index()` *page* for the `test_app` application.
>

> [!NOTE] If You Want To **Automatically** Open *View* Created
> If you want it to automatically enter the the URL `http://127.0.0.1:8000/test_app`. Therefore, we need to modify our `site_test/urls.py` file.
>
> ```python
> urlpatterns = [
>    # open the "index" page directly without manually enter in URL bar
>    path("", include("test_app.urls")),
>    path("admin/", admin.site.urls),
> ]
> ```
>
> Therefore, this means that to see our *page* that we just created... We imply need to enter the `http://127.0.0.1/8000` URL!

> [!TIP] Apparently it *live reloads*...
> So we don't need to **kill** and / or *restart* the server each time that we make a change.
>
> But in the documentation is it states that **adding** files is going to require a *full* **restart** of said development server.
>
> I tried modifying our `test_app/views.py` and modifying the message to just '*Hello World*'. When I **reloaded** the webpage, it did <span style="color: lime;"> updated</span> itself just fine!
>
> > [!INFO] Resource(s)
> > - https://docs.djangoproject.com/en/5.2/intro/tutorial01/#the-development-server
> > - https://stackoverflow.com/a/41429055
>

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!