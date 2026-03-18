---
id: Django Docs - Commands Used
aliases: Django Commands Used When Following Django Official Tutorial
tags:
  - python 
  - django
  - basics
author: S.Sunhaloo
date: 2025-09-09
status: In-Progress
---

- [[Django Docs - Getting Started#Installing Django]]

```bash
# install django on my arch-based system
sudo pacman -S python-django --noconfirm
```

- Verify Installation of Django

```bash
# verify the installation of django on system
python -m django --version
```

- [[Django Docs - Getting Started#Writing Our First Program]]

```bash
# create new django project with the name 'site_test'
django-admin startproject site_test
```

- [[Django Docs - Getting Started#Run The Local Development Server]]

```bash
# run the local development server to check intial project setup
# run the development server on the default port
python manage.py runserver

# run the development server on a specific port
python manage.py runserver 5555
```

- [[Django Docs - Getting Started#Creation of Apps ( Web Pages )]]

```bash
# create new app with the name 'test_app'
python manager.py startapp test_app
```

- [[Django Docs - Getting Started#Run The Server Again]]

```bash
# run the server again
python manage.py runserver
```

- [[Django Docs - Database Setup#Running The `migrate` Command]]

```bash
# run the migrate command to supposedly create our tables ( for required apps )
python manage.py migrate
```

- [[Django Docs - Database Setup#Therefore Making The Migrations]]

```bash
# run the `makemigrations` command for Django create "plan"
python manage.py makemigrations
```

- [[Django Docs - Database Setup#How The SQL Looks Like]]

```bash
# run the `sqlmigrate` command to see the SQL "literals"
python manage.py sqlmigrate FirstApp 0001
```

- To check for errors:

```bash
# run this command to check for any errors
python manage.py check
```

- [[Django Docs - Database Setup#Playing With The API]]

```bash
# open the interactive python 'Django'
# this shell compared to `python` command has
# automatically imported all models from `INSTALLED_APPS`
python manage.py shell
```

- [[Django Docs - The Django Admin#Creation Of Administrative User]]

```bash
# create an administrative "superuser" to login to website
python manage.py createsuperuser
```

- [[Django Docs - Templates and Render#Run The Server]]

```bash
# run the server again
python manage.py runserver
```

- [[Django Docs - Templates and Render#Modify Main View To Display Records]]

```bash
python manage.py shell
```

- [[Django Docs - Templates and Render#Understanding What Each Of These Lines Mean]]

```bash
python manage.py shell
```

- [[Django Docs - Templates and Render#]]

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!