---
id: Django Docs - Writing Forms
aliases: Python Django Documentation - Writing Forms
tags:
  - python
  - django
  - basics
author: S.Sunhaloo
date: 2025-10-14
status: Completed
---

## List of Contents

- [[#Forms In Django]]
	- [[#Updating Our HTML Template]]
	- [[#Update Our View For The Vote]]
	- [[#Update The Result View]]

---

# Forms In Django

> [!INFO]
> This tutorial requires us to fully complete the previous tutorial which was about the '[[Django Docs - Templates and Render]]' systems.

## Updating Our HTML Template

- Go ahead and update our current `FirstApp/templates/FirstApp/detail.html` so that now its looks like this:

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

    <form action="{% url 'polls:vote' question.id %}" method="post">
    {% csrf_token %}
    <fieldset>
        <legend> <h1> {{ question.question_text }}</h1> </legend>
        {% if error_message %}<p> <strong> {{ error_message }}</strong> </p> {% endif %}
        {% for choice in question.choice_set.all %}
            <input type="radio" name="choice" id="choice{{ forloop.counter }}" value="{{ choice.id }}">
            <label for="choice{{ forloop.counter }}"> {{ choice.choice_text }}</label> <br>
        {% endfor %}
    </fieldset>
    <input type="submit" value="Vote">
    </form>

  </body>
</html>
```

> As you can see, we have added a `<form> `!

### What is this all about?

- The way that we making the API request is **not** by `GET` but by `POST`
	- Meaning that the data is hidden and does **not** *show* in the URL
- The above form will provide the user with 2 radio buttons and a <input type="submit" value="something">

## Update Our View For The Vote

> [!INFO]
> As the `FirstApp/views.py` file is getting pretty long... I am going to only show the changes that I made in the code block found below.

```python
# make sure that you have imported all of these "things"
from django.db.models import F
from django.http import HttpResponse, HttpsResponseRedirect
from django.shortcuts import render, get_object_or_404
from django.urls import reverse
from .models import Question, Choice

# vote page ==> placeholder for voting on a specific question by ID
def vote(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    try:
        selected_choice = question.choice_set.get(pk=request.POST["choice"])
    except (KeyError, Choice.DoesNotExist):
        # Redisplay the question voting form.
        return render(
            request,
            "FirstApp/detail.html",
            {
                "question": question,
                "error_message": "You didn't select a choice.",
            },
        )
    else:
        selected_choice.votes = F("votes") + 1
        selected_choice.save()
        # Always return an HttpResponseRedirect after successfully dealing
        # with POST data. This prevents data from being posted twice if a
        # user hits the Back button.
        return HttpResponseRedirect(reverse("FirstApp:results", args=(question.id,)))
```

> [!NOTE]
> From what we can understand with the above `vote` function. It is the one that is going to be responsible for **incrementing** the *vote* count for each of the question that we have!
>

## Update The Result View

Update the `result` *view* / function so that it now looks like this:

```python
# results page ==> shows the results for a specific question by ID
def results(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    return render(request, "FirstApp/results.html", {"question": question})
```

## Create The Template For The Result View

Go ahead and create the `FirstApp/templates/FirstApp/results.html` file:

```html
<h1> {{ question.question_text }}</h1>

<ul>
  {% for choice in question.choice_set.all %}
  <li>
    {{ choice.choice_text }} -- {{ choice.votes }} vote{{ choice.votes | pluralize }}
  </li>
  {% endfor %}
</ul>

<a href="{% url 'FirstApp:detail' question.id %}"> Vote again?</a>
```

### Vote For Question

Run development server and head over to the link 'http://localhost:8000/FirstApp/detail/1/' and then select a _**choice**_ and then press the <button> vote</button> button!

It will then redirect you to the 'http://localhost:8000/FirstApp/1/results/' webpage and you should be able to see that what you voted for has been **incremented**!

# Generic View Shortcut

Because the following is common:

- Send data to the database
- Update the database
- Update the view

Therefore, Django gives us a **shortcut** that we can do the above *steps* in less lines of codes!

## Converting To Use Generic Views

### Update Our URL Configuration

- Update the `FirstApp/urls.py` file so that it now looks like this:

```python
from django.urls import path

from . import views

# let Django know what application holds these specific URLs
app_name = "FirstApp"

urlpatterns = [
    # ex: /FirstApp/
    path("", views.IndexView.as_view(), name="index"),
    # ex: /FirstApp/5/
    path("<int:pk> /", views.DetailView.as_view(), name="detail"),
    # ex: /FirstApp/5/results/
    path("<int:pk> /results/", views.ResultsView.as_view(), name="results"),
    # ex: /FirstApp/5/vote/
    path("<int:question_id> /vote/", views.vote, name="vote"),
]
```

### Update The Actual Views

- Head over to the `FirstApp/views.py` file and add the following generic view "*classes*" before the "*functions*":

```python
from django.db.models import F
from django.http import HttpResponseRedirect
from django.shortcuts import render, get_object_or_404
from django.urls import reverse
from django.views import generic
from .models import Question, Choice


class IndexView(generic.ListView):
    template_name = "FirstApp/index.html"
    context_object_name = "latest_question_list"

    def get_queryset(self):
        """Return the last five published questions."""
        return Question.objects.order_by("-pub_date")[:5]


class DetailView(generic.DetailView):
    model = Question
    template_name = "FirstApp/detail.html"


class ResultsView(generic.DetailView):
    model = Question
    template_name = "FirstApp/results.html"
```

> [!WARNING]
> We should now <strong> <span style="color: orange;"> remove</span> </strong> the old `def index`, `def detail` and `def result` views!
>
> This is because the **generic views** are now handling them for us!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!