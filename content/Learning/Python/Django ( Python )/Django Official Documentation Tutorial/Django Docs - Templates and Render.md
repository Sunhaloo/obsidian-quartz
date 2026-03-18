---
id: Django Docs - Templates and Render
aliases: Python Django Documentation - More Views, HTML File and Rendering
tags:
  - python
  - django
  - basics
author: S.Sunhaloo
date: 2025-09-29
status: Completed
---

## List of Contents

- [[#Writing More Views]]
	- [[#Therefore, Write The Actual Views]]
	- [[#Map Out The Views Written]]
- [[#Modify Main View To Display Records]]
	- [[#Before We Start... Adding More Records]]
	- [[#Actually Updating Main View]]
- [[#Creation Of Templates]]
	- [[#Updating The Index / Main View Again]]
		- [[#The Render Shortcut]]
- [[#Raising and Displaying Famous Error]]
	- [[#The `get_object_or_404` Shortcut]]
	- [[#Update the HTML File For Details View]]
- [[#Removing Hardcoded URLs In Templates]]
	- [[#Hardcoded Code Written In Main Index Page]]
		- [[#Solving The Problem Of Hardcoding URLs]]

---

# Writing More Views

> [!INFO] What is a [[Django Docs - Getting Started#Writing Our View | view]]?
> A **view** is a "*type*" of **webpage** in your Django application that generally serves a **specific** *function* and has a **specific** *template*.
>
> For Example:
>
> - Homepage
> - Login Page
> - Comment / Rating Section

The documentation is telling us that we are going to be writing some views related to our application. These are going to be the following *views*:

- Question “index” page – displays the latest few questions.
- Question “detail” page – displays a question text, with no results but with a form to vote.
- Question “results” page – displays results for a particular question.
- Vote action – handles voting for a particular choice in a particular question.

> Straight from the documentation... *That is why its saying the 'Polls' application*!

> [!INFO] My Current `DjangoLearning/FirstApp/views.py` File
> You are going to see how my current `views.py` file looks like in the code block below.
>
> ```python
> from django.shortcuts import render
> from django.http import HttpResponse
>
>
> # Create your views here.
> def hello_motherfucker(request):
>    return HttpResponse("Hello World From FirstApp From Hello Motherfucker Function!")
>
>
> def something_wong(request):
>    return HttpResponse("Hello World From Something Wong")
> ```
>
> But going to back to *[Tutorial 1](https://docs.djangoproject.com/en/5.2/intro/tutorial01/#write-your-first-view)* of Official Documentation; you are going to see this:
>
> ```python
> from django.http import HttpResponse
>
>
> def index(request):
>    return HttpResponse("Hello, world. You're at the polls index.")
> ```
>
> > Therefore, I am going to change my `views.py` file so that it matches *their* `views.py` file!
>

## Therefore, Write The Actual Views

This is how our `views.py` file should look like after creating all of the required views!

```python
from django.http import HttpResponse


# main index page of the polls app
def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")


# detail page ==> shows the text for a specific question by ID
def detail(request, question_id):
    return HttpResponse("You're looking at question %s." % question_id)


# results page ==> shows the results for a specific question by ID
def results(request, question_id):
    response = "You're looking at the results of question %s."
    return HttpResponse(response % question_id)


# vote page ==> placeholder for voting on a specific question by ID
def vote(request, question_id):
    return HttpResponse("You're voting on question %s." % question_id)
```

## Map Out The Views Written

Hence, we are now going to **update** our `DjangoLearning/FirstApp/urls.py` file so that is looks like this:

```python
from django.urls import path

from . import views

urlpatterns = [
    # ex: /polls/
    path("", views.index, name="index"),
    # ex: /polls/5/
    path("<int:question_id> /", views.detail, name="detail"),
    # ex: /polls/5/results/
    path("<int:question_id> /results/", views.results, name="results"),
    # ex: /polls/5/vote/
    path("<int:question_id> /vote/", views.vote, name="vote"),
]
```

> Hot and Fresh from the documentation!

> [!TIP] We Have Already "*[[Django Docs - Getting Started#Map Out The View To The Project | Map Out The View To The Project]]*"
>
> As you can see, we have this inside our `DjangoLearning/urls.py` file:
>
> ```python
>    path("FirstApp/", include("FirstApp.urls")),
> ```

### Run The Server

- Go ahead and run the server with the `runserver` command to *test* some 'URLs'

```bash
# run the server again
python manage.py runserver
```

> [!TIP] Test The Following URLs
> Copy and paste these 'URLs' into your browser to check them out!
>
> - http://localhost:8000/FirstApp/1
> - http://localhost:8000/FirstApp/1/results
> - http://localhost:8000/FirstApp/1/vote
> - http://localhost:8000/FirstApp/1000
> - http://localhost:8000/FirstApp/1000/results
> - http://localhost:8000/FirstApp/1000/vote

# Writing Functional Views

> [!WARNING] What Django Wants!
> Django wants one of two things:
>
> - `HttpReponse`
> - Exception like the famous '404'
>
> > The rest is up to us!
>
> - If we want to make a **specific** *view* read **records** from a database; we can do so
> - If we want to use some kind of templates; we can do so
> - If we want to use it to create PDF, XML or ZIP files; we can do so
> - If we want to use some / any Python library to do anything we want; we can do so

# Modify Main View To Display Records

## Before We Start... Adding More Records

- Start the Python Interactive Shell:

```bash
python manage.py shell
```

- Add some more data / records into database:

```python
# import the "default" models functionalities
from django.db import models
# import our models that we created
from FirstApp.models import Question
# import the 'timezone' module from the django.utils
from django.utils import timezone

# create some more data / records to add
Question(question_text="Ayrton Senna", pub_date=timezone.now()).save()
Question(question_text="Lewis Hamilton", pub_date=timezone.now()).save()
Question(question_text="Sebastien Vettel", pub_date=timezone.now()).save()
Question(question_text="Max Verstappen", pub_date=timezone.now()).save()
Question(question_text="Nicholas Latifi", pub_date=timezone.now()).save()
Question(question_text="Logan Sargent", pub_date=timezone.now()).save()

# check if the data / records have been added successfully
Question.objects.all()

# iterate through records found inside
for record in Question.objects.all():
    print(record)

# iterate through records found inside ( again )
for record in Question.objects.all():
	# display each ID of each record
    print(record.id)
```

- This is the output that we got inside the 'REPL' itself!

```console
<QuerySet [
	<Question: New Text Question> ,
	<Question: Newly Created Question> ,
	<Question: Ayrton Senna> ,
	<Question: Lewis Hamilton> ,
	<Question: Sebastien Vettel> ,
	<Question: Max Verstappen> ,
	<Question: Nicholas Latifi> ,
	Question: Logan Sargent>
]>

New Text Question
Newly Created Question
Ayrton Senna
Lewis Hamilton
Sebastien Vettel
Max Verstappen
Nicholas Latifi

1
2
3
4
5
6
7
8
```

> [!INFO]
> I am doing this here because I am lazy and have already started the Python Shell.
>
> You could have simply started the development server and then head over to the [[Django Docs - The Django Admin | administrator]] website and then add the records there!
>
> > [!NOTE] I don't remember anything!
> > Link To Official Django Documentation For "*Playing With Shell*": https://docs.djangoproject.com/en/5.2/intro/tutorial02/#playing-with-the-api
>

> [!WARNING]
> I have formatted the output of `Question.objects.all()` for readability!

## Actually Updating Main View

- This is the code that was *ripped out* from the documentation:

```python
from django.http import HttpResponse

from .models import Question


def index(request):
    latest_question_list = Question.objects.order_by("-pub_date")[:5]
    output = ", ".join([q.question_text for q in latest_question_list])
    return HttpResponse(output)


# Leave the rest of the views (detail, results, vote) unchanged
```

### Understanding What Each Of These Lines Mean

- Start the Python Interactive Shell again!

```bash
python manage.py shell
```

- What does the **variable** `lastest_question_list` hold?

> Obviously the latest question**s** but like how?

```python
# get all the "question" record
Question.objects.all()

# get all the "question" record with `order_by` method
# but in this case, don't pass any arguments in `order_by`
Question.objects.order_by()

# similarly, now we are going to pass `id` but in reverse
Question.objects.order_by("-id")

# therefore, we can see that the line of code found below
# is getting all the records in the descending order of `pub_date`
Question.objects.order_by("-pub_date")

# finally apply list slicing to this output
# in this case, its going to get 5 first records
Question.objects.order_by("-pub_date")[:5]
```

> This is the output after running the following codes found above

```console
<QuerySet [
	<Question: New Text Question> ,
	<Question: Newly Created Question> ,
	<Question: Ayrton Senna> ,
	<Question: Lewis Hamilton> ,
	<Question: Sebastien Vettel> ,
	<Question: Max Verstappen> ,
	<Question: Nicholas Latifi> ,
	Question: Logan Sargent>
]>

# so its the same output... we need to pass an argument
<QuerySet [
	<Question: New Text Question> ,
	<Question: Newly Created Question> ,
	<Question: Ayrton Senna> ,
	<Question: Lewis Hamilton> ,
	<Question: Sebastien Vettel> ,
	<Question: Max Verstappen> ,
	<Question: Nicholas Latifi> ,
	Question: Logan Sargent>
]>

# in this case, we are "sorting" by `id` ( descending order )
<QuerySet [
	<Question: Logan Sargent> ,
	<Question: Nicholas Latifi> ,
	<Question: Max Verstappen> ,
	<Question: Sebastien Vettel> ,
	<Question: Lewis Hamilton> ,
	<Question: Ayrton Senna> ,
	<Question: Newly Created Question> ,
	<Question: New Text Question>
]>

# so in this very case, we are going to see that we have
# the exact same output as our `"-id"` argument passed in `order_by`
<QuerySet [
	<Question: Logan Sargent> ,
	<Question: Nicholas Latifi> ,
	<Question: Max Verstappen> ,
	<Question: Sebastien Vettel> ,
	<Question: Lewis Hamilton> ,
	<Question: Ayrton Senna> ,
	<Question: Newly Created Question> ,
	<Question: New Text Question>
]>

# finally, we can see that if only get the
# first data to the 5th data ==> 0th index to 4th index
<QuerySet [
	<Question: Logan Sargent> ,
	<Question: Nicholas Latifi> ,
	<Question: Max Verstappen> ,
	<Question: Sebastien Vettel> ,
	<Question: Lewis Hamilton> ,
]>
```

> [!SUCCESS] Therefore, `latest_question_list`
> We can see that the `latest_question_list` holds a *list* of records which a maximum size of '5'!

- What does the **variable** `output` holds?

```python
# that we know that `latest_queston` is just a list of records
# therefore, we can simply do something like this
latest_question_list = Question.objects.order_by("-pub_date")[:5]

# therefore if we run a little for loop to iterate through records
for record in latest_question_list:
	# display the records objects themselves
	print(record)
	
# now, let's get the `question_text` attribute of each record object
for record in latest_question_list:
	# display the `question_text` attribute of each object
	print(record.question_text)
	
# get all the `question_text` of each objects into a list
list_questions_text = [question.question_text for question in latest_question_list]

# finally, use the `join` method which works on strings and iterables
# to be able to join the data found in list with `, `
output = ', '.join(list_question_text)
```

> Again this is the output after running the codes from the above code block!

```console
# output of the first `for` loop
Logan Sargent
Nicholas Latifi
Max Verstappen
Sebastien Vettel
Lewis Hamilton

# output of the second `for` loop
Logan Sargent
Nicholas Latifi
Max Verstappen
Sebastien Vettel
Lewis Hamilton

# this the the `list_questions_text` list
['Logan Sargent', 'Nicholas Latifi', 'Max Verstappen', 'Sebastien Vettel', 'Lewis Hamilton']

# this is the final output that we want
'Logan Sargent, Nicholas Latifi, Max Verstappen, Sebastien Vettel, Lewis Hamilton'
```

> [!SUCCESS]
> Therefore, we what these `latest_question_list` and `output` variables do!

# Creation Of Templates

- Create the `templates/FirstApp` *folders* inside the `DjangoLearning/FirstApp` directory

```bash
# change directory to our first application
cd DjangoLearning/FirstApp

# create the `templates` folder inside
mkdir -p templates/FirstApp
```

- Head inside the `templates/FirstApp` directory and create an `index.html` HTML file

```bash
# change directory to proper directory
cd templates/FirstApp

# create a new HTML file
touch index.html
```

- Paste the following code inside the `index.html` file:

```html
<!doctype html>
<html lang="en-US">
  <head>
    <meta charset="utf-8" />
    <title> Django Templates and Render</title>
  </head>
  <body>

    {% if latest_question_list %}
    <ul>
      {% for question in latest_question_list %}
      <li> <a href="/FirstApp/{{ question.id }}/"> {{ question.question_text }}</a> </li>
      {% endfor %}
    </ul>
    {% else %}
    <p> No polls are available.</p>
    {% endif %}

  </body>
</html>
```

## Updating The Index / Main View Again

- Go ahead and update the `index` function with this code:

```python
from django.http import HttpResponse
from django.template import loader

from .models import Question


def index(request):
    latest_question_list = Question.objects.order_by("-pub_date")[:5]
    template = loader.get_template("FirstApp/index.html")
    context = {"latest_question_list": latest_question_list}
    return HttpResponse(template.render(context, request))
```

> This a modified code from the documentation!

- Therefore go ahead and start the development server:

```bash
# run the server again
python manage.py runserver
```

> [!SUCCESS]
> I can see that we have successfully displayed the `html` part of our applications

### The Render Shortcut

As **templates** are used pretty much in every *project* and / or *application*. There is a shortcut that Django gives us the `render` **function** from the `django.shortcuts` **module**.

- Therefore, updating the `index` *method* / *page* for last time ( *here* ):

```python
# INFO: remove the `from django.template import loader` import statement
# instead we are going to now use `render` ( see below )
from django.http import HttpResponse
from django.shortcuts import render
from .models import Question


# updated main index page of the polls app
def index(request):
    latest_question_list = Question.objects.order_by("-pub_date")[:5]
    context = {"latest_question_list": latest_question_list}
    return render(request, "FirstApp/index.html", context)
```

# Raising and Displaying Famous Error

- Go head and modify *this part* of our `DjangoLearning/FirstApp/views.py` file:

```python
# we also included the `Http404` "function"
from django.http import HttpResponse, Http404
from django.shortcuts import render
from .models import Question

# our modified 'details' page which is going to
# raise the '404' error is ID does not exists in database
# detail page ==> shows the text for a specific question by ID
def detail(request, question_id):
    # exception handling
    try:
        # get the record by its ID
        question = Question.objects.get(pk=question_id)

    # if the record's ID does not exists
    except Question.DoesNotExist:
        # raise the famous '404' ( not found ) error
        raise Http404("Question does not exist")

    # otherwise render the page
    return render(request, "FirstApp/detail.html", {"question": question})
```

- Create a **template** for our *details* page, add the following code found below in the `DjangoLearning/FirstApp/detail.html`:

```html
<!doctype html>
<html lang="en-US">
  <head>
    <meta charset="utf-8" />
    <title> Django Templates and Render</title>
  </head>

  <body>
    {{ question }}
  </body>
</html>
```

- Therefore go ahead and start the development server:

```bash
# run the server again
python manage.py runserver
```

> [!TIP] Testing URLs
> Given that I currently have eight records inside my 'Question' *table*. Therefore, we can go ahead and test these 2 different URLs.
>
> - http://127.0.0.1:8000/FirstApp/8
> 	- The above URL should be working fine
> - http://127.0.0.1:8000/FirstApp/9
> 	- The above URL should <strong> <span style="color: orange;"> NOT</span> </strong> be working
> 	- We should instead get a page saying something along the lines of '*Page not found (404)*'!
>
> > [!SUCCESS]
> > Therefore, we have been able to successfully been able to understand how to *implement* / *raise* the "*famous*" '404' error!
>

## The `get_object_or_404` Shortcut

Similar to how we need to **render** template frequently in Django... Django also knows that when using the `GET` / `get()` *method*... It is common to use **raise** the '404' error.

- Hence, we can update the `DjangoLearning/FirstApp/views.py` file again to this:

```python
from django.http import HttpResponse
from django.shortcuts import render, get_object_or_404
from .models import Question

# detail page ==> shows the text for a specific question by ID
def detail(request, question_id):
    # INFO: in this case, we can skip the exception handling block entirely
    question = get_object_or_404(Question, pk=question_id)
    return render(request, "polls/detail.html", {"question": question})
```

> [!NOTE]
> The only reason that I am **not** removing the `from django.https import HttpResponse` line is because my `result` and `vote` *function* are still using the `HttpReponse` *function*.

## Update the HTML File For Details View

- I am going to modify the `detail.html` file so that it looks like this:

```html
<!doctype html>
<html lang="en-US">
  <head>
    <meta charset="utf-8" />
    <title> Django Templates and Render</title>
  </head>

  <body>
    <h1> {{ question.question_text }}</h1>
    <ul>
      {% for choice in question.choice_set.all %}
      <li> {{ choice.choice_text }}</li>
      {% endfor %}
    </ul>
  </body>
</html>
```

# Removing Hardcoded URLs In Templates

## Hardcoded Code Written In Main Index Page

This is what where initially wrote inside the `DjangoLearning/FirstApp/templates/FirstApp/index.html` HTML file:

```html
      <li> <a href="/FirstApp/{{ question.id }}/"> {{ question.question_text }}</a> </li>
```

> This line of code is found on line **13** for me!

This is going to be difficult to manage as we get more and more *files*, *methods* and *classes* inside our Django application / project.

### Solving The Problem Of Hardcoding URLs

Remember how we wrote the following line inside our `DjangoLearning/FirstApp/urls.py` file?

> This is what we have, currently, inside our `urls.py` file!

```python
    path("<int:question_id> /", views.detail, name="detail"),
```

Well, you can see that we the `name` **argument** there! This is basically use for naming the actual *URL* itself. Therefore, this is going to allow us to use the `name` *variable* in other places **instead** of *hardcoding* the actual URL.

Therefore, replace the **above** *line* inside the `index.html` file to this:

```html
	<li> <a href="{% url 'detail' question.id %}"> {{ question.question_text }}</a> </li>
```

> [!SUCCESS]
> This means that if we go back to our `DjangoLearning/FirstApp/urls.py` file and change this specific line
>
> - From this:
>
> ```python
> path("<int:question_id> /", views.detail, name="detail"),
> ```
>
> - To something like this:
>
> ```python
> path("detail/<int:question_id> /", views.detail, name="detail"),
> ```
>
> This means that if you go ahead and *run* the development server and then go to our "*main*" / *root* link for our `FirstApp` application:
>
> - http://127.0.0.1:8000/FirstApp
>
> Then, as we currently have these *link lists* setup on the main index page; we can see that if we click on the link like 'Lewis Hamilton'... You are going to see that the page whereby we are redirected to is going to be:
>
> - http://127.0.0.1:8000/FirstApp/detail/4/
>
> > [!SUCCESS] Double Success
> > We can see that its being used in all of the other places as well!
>

# Namespacing URLs Names

> Basically giving *names* to 'URLs'!

Given that in a "*real*" Django **project**, we are going to have many, many and many **applications**!

This means that, let's say that another application can have the **same**, **exact** URL *definition*... Therefore, we got to let Django know that these URLs are *from* **different** applications.

Hence, this can easily done by providing an **application name** in our `<application_name> /urls.py` file.

- Thus, in our case, we are going **add** the `app_name` *variable* to our `DjangoLearning/FirstApp/urls.py` file:

```python
from django.urls import path

from . import views

# let Django know what application holds these specific URLs
app_name = "FirstApp"

urlpatterns = [
    # ex: /polls/
    path("", views.index, name="index"),
    # ex: /polls/5/
    path("detail/<int:question_id> /", views.detail, name="detail"),
    # ex: /polls/5/results/
    path("<int:question_id> /results/", views.results, name="results"),
    # ex: /polls/5/vote/
    path("<int:question_id> /vote/", views.vote, name="vote"),
]
```

## Updating Our Index Page

Finally, we are once again going to **update** our `index.html` HTML template found in our `FirstApp` application to this:

> Again, I am only changing the code at line **13**!

```html
      <li> <a href="{% url 'FirstApp:detail' question.id %}"> {{ question.question_text }}</a> </li>
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!