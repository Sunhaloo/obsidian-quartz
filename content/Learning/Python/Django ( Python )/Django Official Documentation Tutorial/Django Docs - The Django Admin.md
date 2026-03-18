---
id: Django Docs - The Django Admin
aliases: Python Django Documentation - Setting Up Database ( Django Administrator )
tags:
  - python
  - django
  - basics
author: S.Sunhaloo
date: 2025-09-25
status: Completed
---

## List of Contents

- [[#The Django Admin Site]]
	- [[#Creation Of Administrative User]]
	- [[#Login To Administrative Website]]
		- [[#Make Our Application / Table Appear In Admin Page]]
	- [[#Testing The Field Name]]

---

# The Django Admin Site

- This is what the documentation has to say about the **administrator** website:

Generating admin sites for your staff or clients to add, change, and delete content is tedious work that doesn’t require much creativity. For that reason, Django entirely automates creation of admin interfaces for models.

Django was written in a newsroom environment, with a very clear separation between “content publishers” and the “public” site. Site managers use the system to add news stories, events, sports scores, etc., and that content is displayed on the public site. Django solves the problem of creating a unified interface for site administrators to edit content.

> The admin isn’t intended to be used by site visitors. It’s for site managers.

> [!INFO]
> It basically makes our life **easier** but leaving the "*boring*" to Django itself and leaves us with the actual website that we are going to be displaying to the users!

## Creation Of Administrative User

- Create a '*superuser*' ( *just like in Linux* ) using the `createsuperuser` command:

```bash
# create an administrative "superuser" to login to website
python manage.py createsuperuser
```

> Therefore, we should be **prompted** to enter the *username* and *email address* of administrative user.

> [!WARNING] Username and Email
> Given that we are just *testing* and learning "*things*" out... There is **no** need to enter your *real* **credentials**.
>
> Therefore these are the following credentials that I entered:
>
> - Username: test_first_admin
> - Email: test_first@email.com
> - Password: 1234
> 	- **NOTE**: I am *bypassing* the password "*requirements*"!
>
> ```console
> Superuser created successfully.
> ```

> [!TIP]
> > The following *note* is the *answers* after a conversation with [ChatGPT](https://chat.openai.com).
>
> Similar to [[MongoDB Data View | MongoDB]], we can create our *superuser* **from** the *shell* itself!
>
> - Creation Of Superuser From "*Django*" shell:
>
> ```python
> from django.contrib.auth import get_user_model
> User = get_user_model()
> User.objects.create_superuser("testadmin", "fake@example.local", "S3cretP@ssw0rd")
> ```
>
> Another way of creating a superuser is going to be **non-interactively**. Similar to *logging in* to the MongoDB shell ( *with the proper credentials* ).
>
> ```bash
> # create the superuser directly from the terminal
> # NOTE: you are going to have to enter the password interactively
> python manage.py createsuperuser --username test_first_admin --email tests_first@email.com
> ```
>
> > As you can see, compared to the `--password` flag that MongoDB gives us... Django does <strong> <span style="color: red;"> not</span> </strong> allow us to do that for security reasons!
>

## Login To Administrative Website

Therefore, we simply need to reactivate / run the Django local, development server:

```bash
# run the server again
python manage.py runserver
```

Then head over to the URL `http://127.0.0.1:8000/admin` or simply `http://localhost:8000/admin` and you should see that we get an actual *website*.

> I am now going to enter the **username** and **password** for my newly created administrative user.

### Make Our Application / Table Appear In Admin Page

- I am going to head to my `DjangoLearning/FirstApp/admin.py` file and add the following code:

```python
from django.contrib import admin

# import our 'Question' class from `models.py` file ( found in current directory )
from .models import Question

# register the model to the administrator site
admin.site.register(Question)
```

> Basically copied from the [documentation](https://docs.djangoproject.com/en/5.2/intro/tutorial02/#make-the-poll-app-modifiable-in-the-admin)!

Therefore, we should be able to see that the 'FirstApp' app is shown together with the 'Questions' *class* / *table*.

#### Change List - Edit Question

In my case, I have just clicked on the 'Very Nice' question that I created when I played with the [[Django Docs - Database Setup#Playing With The API | API / Shell]].

- I have edited the 'Very Nice' text to 'New Text Question'

> [!NOTE] 'Question Text' and 'Date Published'!
> Remember how we added these *class variables* / **fields** to our 'Question' *class* / table in our `DjangoLearning/FirstApp/models.py` file?
>
> ```python
>    # class variables that will become our database fields
>    question_text = models.CharField(max_length=200)
>    # INFO: the actual field name is going to be `pub_date`
>    # but the user is going to see 'data published' and NOT `pub_date`
>    pub_date = models.DateTimeField("date published")
> ```
>
> As you can see the `question_text` **field** is being displayed as 'Question text' and `pub_date` is being displayed as 'Date published'
>
> From what I can see the 'date published'... Python ( *or Django* ) applied the `.capitalize()` function on it.

- Save the changes that we have done

> [!SUCCESS]
> We have been able to change the `question_text` for our first *record*.
>
> > [!INFO] Python Shell
> > Going into the `python manage.py shell`, importing `from django.db import models` and ( *in my case* ) `from FirstApp.models import Question`.
> >
> > When I run `Question.objects.all()`, I see that it gets **updated**!!!
>

#### Change List - Add Another Question

- Click on the <button> + Add</button> button to create another 'Question' record
- Add the 'Question text' and 'Date published'
- Finally, again, click on the <button> Save</button> button!

> [!SUCCESS]
> In my case, I do see that I have another record created and now I am going to **log out**!
>
> > [!INFO] Again Checking With Shell
> When I run the *query* `Question.objects.all()`, I can see that we have created the **new** record:
>
> ```console
> <QuerySet [<Question: New Text Question> , <Question: Newly Created Question> ]>
> ```

> [!TIP] So Basically...
> From what I see, instead of creating the *records* from the shell... We created them from the "*admin*" website!

## Testing The Field Name

> [!WARNING] Just Testing
> I am **not** going to be permanently switch it to the new one... After testing it am I doing to revert back to `"date published"`!

I want to test something out... Like I have said... I can see the `pub_date` display named had `.capitalise()` to it.

I will now change it so the **displayed** name inside the `DjangoLearning/FirstApp/models.py` file to this:

```python
# was originally 'date published'
pub_date = models.DateTimeField("Date Published")
```

> Therefore, I am expecting to see 'Date Published' instead of 'Date published'!

> [!SUCCESS] It Did Work!!!
> Therefore, I suggest if you to write what you **want** exactly to be displayed there.
>
> > I am now going to revert back to the original!
>

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!