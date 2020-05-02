---
layout: post
title: "4 reasons why I love Django"
categories: webapp
tags: webapp django
---

# Intro

I have always been using Flask to develop little web apps but I have recently switched to [Django][django] for a bigger project.

I definitely felt more comfortable with Flask so why change? Many makers I admire use Django and are happy with it but I didn't really get why one should use Django instead of Flask and I could not find a good explanation online about the differences. I decided to find out by myself.

I read the official tutorial and it seemed to make sense, but it was only when I starter to build my app that I fell in love. These are the 4 reasons why I love Django.

## The Class Based Views

The views are so easy to build. Most of them require 3 lines of code, everything else is done inside the templates.

For example you want to build a view that shows an entry in your Database table. Just do:

```
class DetailView(generic.DetailView):
    model = YourModel
    template_name = 'detail.html'
```

## The Django user authentication system

The `contrib.auth` package has all the functionality to add a mechanism to register and login users. You don't even need to wirte a view!

To make a view available only for registered users you just add `LoginRequiredMixin` as argument to the view:

```
class DetailView(LoginRequiredMixin, generic.DetailView):
    model = YourModel
    template_name = 'detail.html'
```

## The Django Models (or Django ORM)

How easy it is to add a model and migrate the DB! First of all your Database ground truth is in the code (all Models have a corresponding Table defined in the DB). Every time you change the Models (add a new table, add a column to the DB, link tables with a key...) you just need to run the migration:

```
python manage.py makemigrations
python manage.py migrate
```

The first command creates the statements to be applied to your DB and the second one will apply them, modifying your DB schema. Just do this everytime you deploy and you will never run into troubles even for the most complex DB schemas.

Bonus: you can create a wonderful UML diagram following [these instructions][django-uml]

## The Django built-in filters

There are so many useful filters available to use (in addition to Jinja ones). The `truncatewords` for example. The text you want to display is too long to stay in one line so you can only afford 10 words? Do

```
{{ "{{ table.text|truncatewords:10 " }}}}
```

Or the `humanize`, to make easily readable numbers. Instead of displaying 100000000 you can simply display 100 Million by doing:

```
{{ "{{ 100000000|intword " }}}}
```

I am sure I just scratched the surface of the advantages of Django, I hope those above will make you see how easy is to do very important things when developing a web app.
Just head to the [documentation][django-docs] and follow the tutorial if you wanna get started.

[django]: https://www.djangoproject.com
[django-uml]: https://simpleit.rocks/python/django/generate-uml-class-diagrams-from-django-models/
[django-docs]: https://docs.djangoproject.com/en/3.0/
