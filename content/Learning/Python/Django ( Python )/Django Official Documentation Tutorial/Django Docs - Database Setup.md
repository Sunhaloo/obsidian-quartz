---
id: Django Docs - Database Setup
aliases: Python Django Documentation - Setting Up Database
tags:
  - python
  - django
  - basics
author: S.Sunhaloo
date: 2025-08-29
status: Completed
---

## List of Contents

- [[#Choosing A Database]]
- [[#The Migrate Command]]
- [[#Creation Of Models]]
	- [[#Creation Of Database In First Application]]
		- [[#Code Pasted Inside File]]
	- [[#Activating Models]]
- [[#Making The Migrations]]
	- [[#But First I Want To Test Somethings]]
	- [[#Make The Migrations Continued]]
		- [[#Creation Of Tables In Database]]
- [[#Playing With The API]]


---

> [!WARNING]
> <p align="center"> I Have Created A New Project!!!</p>
>
> Yes, I am **not** working on the `site_test` project and `test_app` app... Instead I created a **new** project from scratch, so that I can help and do the documentation together with a friend.
>
> Here are some details about the new project:
>
> - Project Name: DjangoLearning
> - Apps Created:
> 	- FirstApp
> 	- SecondApp
>
> > Additionally, I am working *inside* a Python **virtual environment** meaning that I had to run `pip` to install `Django` / `django` module again!
>

> [!INFO] Resource(s)
> - https://docs.djangoproject.com/en/5.2/intro/tutorial02/

# Choosing A Database

The default and **easiest** option is going to be [SQLite](https://www.sqlite.org/)!

If you look at the `settings.py` file and search for `DATABASES`; you should see that it has already been "*configured*".

```python
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.sqlite3",
        "NAME": BASE_DIR / "db.sqlite3",
    }
}
```

> [!INFO] Information About SQLite
> This is a fully open-sourced Relational Database *program* that is can be used out of the box!
>
> Yes, it requires **no configuration**, its **serverless** ( *compared to something like [[Microsoft SQL Server 2022 Data View|MS SQL Server]] or [[MongoDB Data View | MongoDB]]* )
>
> Its also the most widely adopted Database in the whole world... Therefore there is not need to be ashamed of using such a "*simple*" tool!
>
> > As you get older, you realise that **simple** is so much **better**!
>
> Additionally, check out this video made by one of the GOATs '[DevOps Toolbox](https://www.youtube.com/@devopstoolbox)' about SQLite: https://www.youtube.com/watch?v=9RArbqGOvsw

> [!TIP] Set Up The [Time Zone](https://docs.djangoproject.com/en/5.2/ref/settings/#std-setting-TIME_ZONE)
> As we are already inside the `settings.py` file... Let's change the time zone from '*UTC*' to '*Indian/Mauritius*' as I live in piece of shit country!

> [!TIP] Packaging Applications
> From what I can see from the documentation, we know that whenever we create a project; inside our `settings.py` file, we have the following [[Python - Lists | list]].
>
> ```python
> INSTALLED_APPS = [
> 	# the administrator site ( for superusers, etc )
>    "django.contrib.admin",
>    # the authentication system
>    "django.contrib.auth",
>    # something related to models and "contenttypes"
>    "django.contrib.contenttypes",
>    # think of it like cookies on a website
>    "django.contrib.sessions",
>    # for one time "flash" notifications
>    "django.contrib.messages",
>    # our static files like HTML, CSS and JS
>    "django.contrib.staticfiles",
> ]
> ```
>
> But let's say that we really like to use '*AppX*' in most of our Projects that we create.
>
> Therefore, we can **package** this app and hence be able to "*import*" it to another project.

# The Migrate Command

> [!INFO] Resource(s)
> - https://docs.djangoproject.com/en/5.2/ref/django-admin/#django-admin-migrate

Given that we have all these `INSTALLED_APPS`; some of them make use of a database. Therefore, the `migrate` command is going **create** the required database **tables**.

> [!NOTE] Addition / Removal Of Applications
> As you **don't** know, my *current* `INSTALLED_APPS` list looks like this:
>
> ```python
> INSTALLED_APPS = [
>    "django.contrib.admin",
>    "django.contrib.auth",
>    "django.contrib.contenttypes",
>    "django.contrib.sessions",
>    "django.contrib.messages",
>    "django.contrib.staticfiles",
>    # our `FirstApp` application
>    "FirstApp",
>    # our `SecondApp` application
>    "SecondApp",
> ]
> ```
>
> I have my `DjangoLearning/FirstApp` and `DjangoLearning/SecondApp`... But I don't really know if its going to create any **tables** for *these* applications. As I currently have **not** setup any "*models*" inside my `models.py` files for **both** of these applications.
>
> > But this means that if you **don't** need an application, you can just *comment* it out or *completely* **remove** it from the the Python list.
>

## Running The `migrate` Command

- Run the following `migrate` command:

```bash
# run the migrate command to supposedly create our tables ( for required apps )
python manage.py migrate
```

- This is the following output that I get after I run this command:

```console
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying auth.0010_alter_group_name_max_length... OK
  Applying auth.0011_update_proxy_permissions... OK
  Applying auth.0012_alter_user_first_name_max_length... OK
  Applying sessions.0001_initial... OK
```

> [!INFO] Ohh!
> From what I can see, it *applies the migrations* for:
>
> - `admin`
> - `auth`
> - `contenttypes`
> - `sessions`
>
> Now, when I did **not** even run the `migrate` command... I saw that the `db.sqlite3` file was being created. Nevertheless, when I did `cat` out the file; I saw that it was simply **empty**.
>
> But now, **after** applying the migrations with the above command, I can see that it added a lot of things into that **database file** ( `db.sqlite3` ).
>
> > [!INFO]
> > Again, notice like, even if we have the `FirstApp` and `SecondApp` *apps* inside of this `INSTALLED_APPS` **lists**.
> >
> > As we have **no code** inside each `models.py` file... It's **not** going to *show up* using the migration process.
>

# Creation Of Models

> This is basically us **defining** our database **fields**!!!

Let's say that we are simply using something like [[Microsoft SQL Server 2022 Data View|MS SQL Server]]. This means that we would need to *use* the `CREATE` command and **specify** our *fields* so that our **[[SQL Commands - Data Definition Language ( DDL )#Create Tables | database tables]]** are created correctly.

> Django allows us to "<em> <span style="color: orange;"> skip</span> </em> " all of this by just writing Python "*codes*"!

This is were the `models.py` file comes into play. You are going to see that in our *main* **project** folder `DjangoLearning`. We **don't** have that `models.py` file there!

But if you go into our **applications** ( *i.e `FirstApp` and `SecondApp`* ), you **are** going to see that these `models.py` file are present and they currently looks like this:

```python
from django.db import models

# Create your models here.
```

## Creation Of Database In First Application

> [!WARNING]
> As I don't really know what to implement and what I am actually doing... I am just going to follow the documentation.

```python
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField("date published")


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

One thing that I immediately see when I pasted that code in my `model.py` file... I get *errors*!

[Pyright](https://github.com/microsoft/pyright) is telling me that the line of code:

```python
votes = models.IntegerField(default=0)
```

- The error message for the `default=0` is something like this:

```console
Argument of type "Literal[0]" cannot be assigned to parameter "default"...
```

> I am just going to **leave** it *as is*!

### Explanation Of Above Documentation Code

- Each **model** is represented by a `class` ( that *subclasses* `django.db.models.Model` )
	- Example of "*model class*": `Question` and `Choice`
	- Each **model** has a number of *class variables*
- Each **class variable** is represented as a *database field*
	- Each database **field** is represented by the `Field` *class*
		- `Field` class will hold **datatype** of each *database field*
- **Relationship** is defined using `ForeignKey`
	- Supports for *one-to-one*, *many-to-one* and *many-to-many*

### Code Pasted Inside File

- The code block below is the actual code that I pasted inside my `DjangoLearning/FirstApp/models.py` file:

```python
from django.db import models


# create the 'Question' database table
class Question(models.Model):
    # class variables that will become our database fields
    question_text = models.CharField(max_length=200)
    # INFO: the actual field name is going to be `pub_date`
    # but the user is going to see 'data published' and NOT `pub_date`
    pub_date = models.DateTimeField("date published")


# create the 'Choice' database table
class Choice(models.Model):
    # class variables that will become our database fields
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

This is what is going to have happen in this case:

- Creates **two** database *table*: `Question` and `Choice`
- `Question` table:
	- Creates the following database *fields*:
		- `id`
		- `question_text`
		- `pub_date` ( *which is represented as 'date published'* )
- `Choice` table:
	- Creates the following database *fields*:
		- `id`
		- `question` ( _**references** the `id` of `Question` table_ )
		- `choice_text`
		- `votes`

> [!TIP] Creation Of `id` Database **Field**
> Yes! Django is going to **automatically create** the `id` field for you.
>
> Taking a look at the `db.sqlite3` database file... Remember I have already ran the `migrate` command and I can see that for the **all** of the *tables* created, we have something like this:
>
> ```sql
> "id" integer NOT NULL PRIMARY KEY AUTOINCREMENT
> ```
>
> > [!INFO] The **Foreign Key**
> > As you can, see we have this line of code in our `Choice` class ( *or database table* )
> >
> > From '[[Microsoft SQL Server 2022 Data View|MS SQL Server 2022]]' we know that if we want to make a *relation* with a **foreign key**. In the other table... We are going to have to make a *field* strictly for that "*relationship*".
> >
> > > But that *other* table still has its own **primary key**!
> >
> > From what [ChatGPT](https://chat.openai.com), it's going to create / *execute* something like this:
> >
> > ```sql
> > CREATE TABLE Choice (
> >    id integer PRIMARY KEY AUTOINCREMENT,
> >    question_id integer NOT NULL,
> >    choice_text varchar(200) NOT NULL,
> >    votes integer NOT NULL DEFAULT 0,
> >    FOREIGN KEY(question_id) REFERENCES Question(id) ON DELETE CASCADE
> > );
> > ```
> >
> > > I will check the `db.sqlite3` file after we run the `migrate` command!
> >
>

## Activating Models

In the '[[#The Migrate Command]]' heading / section... I had **already** added my applications inside the `INSTALLED_APPS` list found in the `settings.py` file.

> "_But we are going to **remove** / **update** it_!"

- Update the `INSTALLED_APPS` inside the `settings.py` file to *this*:

```python
INSTALLED_APPS = [
    # add the dotted path to `FirstApp` configuration
    "FirstApp.apps.FirstappConfig",
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
]
```

> As you can see, I have also **removed** the `SecondApp` app from the list!

The thing that we have added, that is, `"FirstApp.apps.FirstAppConfig"` is basically the *dotted* path to `DjangoLearning/FirstApp/apps.py` and points to the `FirstappConfig` **class**!

- This is the contents found inside the `apps.py` in the `FirstApp` folder:

```python
from django.apps import AppConfig


class FirstappConfig(AppConfig):
    default_auto_field = "django.db.models.BigAutoField"
    name = "FirstApp"
```

> [!SUCCESS]
> Similarly to what I have been saying from above... Now Django will know that it has to **include** the `FirstApp` when using the *proper* commands!

# Making The Migrations

Now the *documentation* is asking us to the run the `makemigrations` command that is going to create the actual database **tables** and **fields**.

---

## But First I Want To Test Somethings

> [!WARNING]
> <h4 align="center"> You Can Skip This!!!</h4>

Given that I just updated the `INSTALLED_LIST` to add the *dotted* path to the `FirstApp/apps.py` "*configuration*" class.

> But Why?

Why do I have to add `"FirstApp.apps.FirstappConfig"` instead of simply adding the **whole** `FirstApp` directory

> This is what I am going to test!

- Revert the `INSTALLED_APPS` list to what I had before and run the "*required*" command to **make** the *migrations*

```python
# reverting back to what I had originally
INSTALLED_APPS = [
   "django.contrib.admin",
   "django.contrib.auth",
   "django.contrib.contenttypes",
   "django.contrib.sessions",
   "django.contrib.messages",
   "django.contrib.staticfiles",
   # our `FirstApp` application
   "FirstApp",
   # our `SecondApp` application
   "SecondApp",
]
```

- Run the `makemigrations` command to actually **create** of database *tables* and *fields*:

```bash
# "make migrations" to create the "proper" database tables and fields
python manage.py makemigrations
```

> [!INFO] Before I Run This Command!
> If you are following the documentation, then you are going to see that they expect you to *see* something like this:
>
> ```console
> Migrations for 'polls':
>  polls/migrations/0001_initial.py
>    + Create model Question
>    + Create model Choice
> ```
>
> Our are **not** going to be the same thing but `'polls'` should be **replaced** for us!

- This is what I get after running the above command where I have my **original** `INSTALLED_APP` list:

```console
  FirstApp/migrations/0001_initial.py
    + Create model Question
    + Create model Choice
```

> A File!

From what I can see that it **created** the `0001_initial.py` file and this is where the "*implementation*" of the **tables** and **fields** are stored.

- Here is a little *extract* from the file:

```python
    operations = [
        migrations.CreateModel(
            name="Question",
            fields=[
                (
                    "id",
                    models.BigAutoField(
                        auto_created=True,
                        primary_key=True,
                        serialize=False,
                        verbose_name="ID",
                    ),
                ),
                ("question_text", models.CharField(max_length=200)),
                ("pub_date", models.DateTimeField(verbose_name="date published")),
            ],
        ),
	# more code found below
```

> [!WARNING]
> > "*It Has NOT Yet Created The Tables*"
>
> From what I can understand the `makemigrations` command is going to only create a **plan** ( *i.e the `FirstApp/migrations/0001_initial.py` file* ) for Django to then, when running the `migrate` command is going to *then* write things like `CREATE TABLE ...` inside the `db.sqlite3` file!

- Hence to **create** the *tables* inside the `db.sqlite3` file:

```bash
# create the actual tables inside the sqlite file
python manage.py migrate
```

- This is the output that I get after running the above `migrate` command:

```console
Operations to perform:
  Apply all migrations: FirstApp, admin, auth, contenttypes, sessions
Running migrations:
  Applying FirstApp.0001_initial... OK
```

> [!WARNING] Binary File Ouput!
> The `db.sqlite3` file is a **binary** file... *Well its not human readable*.
>
> Nevertheless, when I do use the `cat` command to display its contents... I can see that I do have the following:
>
> ```console
> CREATE TABLE "FirstApp_question" (
> 	"id" integer NOT NULL PRIMARY KEY AUTOINCREMENT,
> 	"question_text" varchar(200) NOT NULL,
> 	"pub_date" datetime NOT NULL
> )
> ```
>
> ```console
> CREATE TABLE "FirstApp_choice" (
> 	"id" integer NOT NULL PRIMARY KEY AUTOINCREMENT,
> 	"choice_text" varchar(200) NOT NULL,
> 	"votes" integer NOT NULL,
> 	"question_id" bigint NOT NULL REFERENCES "FirstApp_question" ("id") DEFERRABLE INITIALLY DEFERRED
> )
> ```
>
> > "*I have formatted the output for readability*"
>

> [!SUCCESS] So It Does Work!
> > I mean it just did right!
>

### Difference Between Short Hand Path and Full Dotted Path

> [!NOTE]
> > This answer is coming from 'ChatGPT'.
>
> - Using `FirstApp`:
> 	- Check for the `apps.py` file inside
> 	- Which has the `AppConfig` subclass
> 	- No `apps.py`; then Django just uses a *generic* **default** configuration
> - Using `FirstApp.apps.FirstappConfig`
> 	- Django does **not** have to guess
> 	- More precise if we have **multiple** configurations or app *names* conflicts
>
> Why Django's documentation shows the "*long form*" version? Because it wants us, beginners to know that is exactly being *sourced*!

#### But What Is Exactly `apps.py` Or These "Configurations"?

From what I can see and understand, when we **add** our applications into the `INSTALLED_APPS` list. Django does straight to look at the `apps.py` file for *that* application.

> This is why, for beginners the *long form* is used!

Django uses this `apps.py` file to basically keep track of the "*things*" and *metadata* about our applications.

---

## Make The Migrations Continued

> [!TIP] Reminder...
> We are back to following the documentations; this means that my `INSTALLED_APPS` lists looks *back* like this:
>
> ```python
> INSTALLED_APPS = [
>    # add the dotted path to `FirstApp` configuration
>    "FirstApp.apps.FirstappConfig",
>    "django.contrib.admin",
>    "django.contrib.auth",
>    "django.contrib.contenttypes",
>    "django.contrib.sessions",
>    "django.contrib.messages",
>    "django.contrib.staticfiles",
> ]
> ```
>
> Its **now** that I am going to run the `makemigrations` and `migrate` commands.
>
> Here is proof that I **don't** have the `0001_initial.py` file:
>
> ```console
>  migrations
> ├──  __init__.py
> └──  __pycache__
>    ├──  0001_initial.cpython-313.pyc
>    └──  __init__.cpython-313.pyc
> ```

### Therefore Making The Migrations

- Hence, run the following command to tell Django how to **create** the *tables*:

```bash
# run the `makemigrations` command for Django create "plan"
python manage.py makemigrations
```

- This is the output that I get after running the `makemigrations` command:

```console
Migrations for 'FirstApp':
  FirstApp/migrations/0001_initial.py
    + Create model Question
    + Create model Choice
```

- Therefore we should see that its **now** that we have the `migrations/0001_initial.py`:

```console
 migrations
├──  0001_initial.py
├──  __init__.py
└──  __pycache__
    ├──  0001_initial.cpython-313.pyc
    └──  __init__.cpython-313.pyc
```

> [!INFO] Everything is going to plan!
> If I `cat` out the `db.sqlite3` **binary** file and search for `FirstApp`... **I don't see it**!
>
> > Very Nice!
>

### Creation Of Tables In Database

- Thus to **create** the *tables* inside of `db.sqlite3` run the `migrate` command:

```bash
# actually create the tables inside the database
python manage.py migrate
```

- This is the output that I get after running the above command:

```bash
Operations to perform:
  Apply all migrations: FirstApp, admin, auth, contenttypes, sessions
Running migrations:
  Applying FirstApp.0001_initial... OK
```

> [!SUCCESS]
> > Fucking Succ-Fucking-Cess!
>
> I can basically see the **same** thing as above, that is:
>
> ```console
> CREATE TABLE "FirstApp_question" (
> 	"id" integer NOT NULL PRIMARY KEY AUTOINCREMENT,
> 	"question_text" varchar(200) NOT NULL,
> 	"pub_date" datetime NOT NULL
> )
> ```
>
> ```console
> CREATE TABLE "FirstApp_choice" (
> 	"id" integer NOT NULL PRIMARY KEY AUTOINCREMENT,
> 	"choice_text" varchar(200) NOT NULL,
> 	"votes" integer NOT NULL,
> 	"question_id" bigint NOT NULL REFERENCES "FirstApp_question" ("id") DEFERRABLE INITIALLY DEFERRED
> )
> ```
>
> > "*Again; formatted the output for readability*"
>

> [!INFO] From The Documentation
> > "You can read the migration for your new model if you like; it’s the file `polls/migrations/0001_initial.py`. Don’t worry, you’re not expected to read them every time Django makes one, but they’re designed to be human-editable in case you want to manually tweak how Django changes things."
>

# How The SQL Looks Like:

As you know we have the `db.sqlite3` file which is a **binary** file. This means that its not human readable.

> Even though the `cat` command could "*kind of*" read it!

Therefore, we have a the `sqlmigrate` command; which when provided with our *applications* is going to show us what the 'SQL' actually looks like:

- Therefore, run the following command and provide our `FirstApp` app as *argument*:

```bash
# run the `sqlmigrate` command to see the SQL "literals"
python manage.py sqlmigrate FirstApp 0001
```

- In my case, I see an output like this:

```console
BEGIN;
--
-- Create model Question
--
CREATE TABLE "FirstApp_question" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "question_text" varchar(200) NOT NULL, "pub_date" datetime NOT NULL);
--
-- Create model Choice
--
CREATE TABLE "FirstApp_choice" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "choice_text" varchar(200) NOT NULL, "votes" integer NOT NULL, "question_id" bigint NOT NULL REFERENCES "FirstApp_question" ("id") DEFERRABLE INITIALLY DEFERRED);
CREATE INDEX "FirstApp_choice_question_id_738d62d9" ON "FirstApp_choice" ("question_id");
COMMIT;
```

> [!WARNING] But The Documentation Shows Us Something Like This:
> ```console
> BEGIN;
> --
> -- Create model Question
> --
> CREATE TABLE "polls_question" (
>    "id" bigint NOT NULL PRIMARY KEY GENERATED BY DEFAULT AS IDENTITY,
>    "question_text" varchar(200) NOT NULL,
>    "pub_date" timestamp with time zone NOT NULL
> );
> --
> -- Create model Choice
> --
> CREATE TABLE "polls_choice" (
>    "id" bigint NOT NULL PRIMARY KEY GENERATED BY DEFAULT AS IDENTITY,
>    "choice_text" varchar(200) NOT NULL,
>    "votes" integer NOT NULL,
>    "question_id" bigint NOT NULL
> );
> ALTER TABLE "polls_choice"
>  ADD CONSTRAINT "polls_choice_question_id_c5b4b260_fk_polls_question_id"
>    FOREIGN KEY ("question_id")
>    REFERENCES "polls_question" ("id")
>    DEFERRABLE INITIALLY DEFERRED;
> CREATE INDEX "polls_choice_question_id_c5b4b260" ON "polls_choice" ("question_id");
>
> COMMIT;
> ```

> [!TIP] Check For Any Errors
> We can use the following command to check for any errors:
>
> ```bash
> # run this command to check for any errors
> python manage.py check
> ```
>
> - This is the output that I get after running the `check` command:
>
> ```console
> System check identified no issues (0 silenced).
> ```

## Remake The Migrations And Migrate To Database

At this point, the documentations ask us to run the `makemigrations` and `migrate` commands... As I have already run it a couple of times.

My output is going to be **different** than what they have in the documentation... Again, as I have already **ran** these commands.

- Running the "*required*" commands again:

```bash
# make the migrations
python manage.py makemigrations

# make Django write the actual "SQL" to the 'db.sqlite3' file
python manage.py migrate
```

---

# Playing With The API

- Open the **interactive** Python shell with the following command:

```bash
# open the interactive python 'Django'
# this shell compared to `python` command has
# automatically imported all models from `INSTALLED_APPS`
python manage.py shell
```

> Therefore we are going to be thrown into the [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop)

> [!INFO] Follow The Official Documentation
> I think its best to just follow the documentation for this part.
>
> - Link To Documentation: https://docs.djangoproject.com/en/5.2/intro/tutorial02/#playing-with-the-api

## My Playing With It

- `Question.objects.all()` does **not** work!!! We need to import?

```python
# import everything inside the `models.py` file
from FirstApp.models import *
```

> Therefore, it should work!

> [!INFO]
> I have now *played* with the first part and now its telling us to modify the `FirstApp/models.py` file again to better "*return*" data.
>
> From this `<QuerySet [<Question: Question object (1)> ]> ` to something like this `<QuerySet [<Question: What's up?> ]> `
>
> > Therefore, I am now going to exit the interactive shell and will have to run the `import` command again!
>

### Modifying My `models.py` File

#### Get Better Return Results

> I am now going to modify the `models.py` file to look like this!

```python
from django.db import models


# create the 'Question' database table
class Question(models.Model):
    # class variables that will become our database fields
    question_text = models.CharField(max_length=200)
    # INFO: the actual field name is going to be `pub_date`
    # but the user is going to see 'data published' and NOT `pub_date`
    pub_date = models.DateTimeField("date published")

    # method to allow us to get better return results in 'RPEL'
    def __str__(self):
        # return the 'question_text' field instead of just showing object
        return self.question_text


# create the 'Choice' database table
class Choice(models.Model):
    # class variables that will become our database fields
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)

    # method to allow us to get better return results in 'RPEL'
    def __str__(self):
        # return the 'question_text' field instead of just showing object
        return self.choice_text
```

#### Add The Following Custom Method To `Question` Class

```python
# this method is found inside the `Question` class and below the `__str__` dunder method
    # custom method to check if question was published recently
    def was_published_recently(self):
        return self.pub_date > = timezone.now() - datetime.timedelta(days=1)
```

### Going Back To Play With Interactive Shell

> Again, restart the the shell and `import` our *required* models again!



---

> [!SUCCESS]
> I think I am done in here.
>
> Now there is another part to this "*database*" thing and its the 'Django Admin'. I think its more fitting that I create a separate note for it as this one is becoming to much!
>
> > Please visit the '[[Django Docs - The Django Admin]]' file / note next> !
>

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!