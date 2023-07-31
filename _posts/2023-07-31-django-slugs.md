---
layout: post
title: "Django slugs - Easily explained"
categories: django
tags: indie hacking
---

I wrote about my job board the other day, one of the 2 experiments I am trying to get off the ground. The idea is to build a business without having a large audience. For SEO the URL is very important and you don't want to mess them up. From [Google's own documents][google-seo-starter] you want to `use words in URLs. URLs with words that are relevant to your site's content and structure are friendlier for visitors navigating your site`. And also, you want to `avoid using lengthy URLs with unnecessary parameters and session IDs`. So, for example, `https://datainternships.co/internships/data-scientist-italy-ferrari` is a much more SEO-friendly choice than `https://datainternships.co/internships/italy/12281726`, where we use some random id to identify the job opening.

But how can you write SEO-friendly URLs in Django? That's where `slugs` come into play. Let's look at an example on how to implement slugs in Django.

## The model

Let's take an example of a recipe website. Even better, international recipes. You have categories for vegetarian, meat, pasta dishes and so on. You probably want to have `/italian-vegetarian-dishes` or `/french-meat-dishes` as your URL.

You probably have a model that looks something like this

```{python}
class Recipe(models.Model):
    type = models.CharField(default="")
    nationality = models.CharField(default="")
    recipe = models.CharField(default="")
```

You have the ingredients to create a slug, but you do not have the slug yet. So first of all, you need to add the slug to your database. Add an attribute recipe_slug to the `class Recipe`.

```{python}
class Recipe(models.Model):
    ...
    recipe_slug = models.SlugField(null=True, blank=True, unique=True, max_length=100)
```

## The view

Now that the field is there we need a way to automatically populate it when we add a new recipe to our database. For this, you just need to add a function to the `class Recipe`. It will look like this

```{python}
class Recipe(models.Model):
    ...
    def save(self, *args, **kwargs):
        self.recipe_slug = slugify(self.nationality + "-" + self.type)
        super().save(*args, **kwargs)
```

That's it. Now every time you add a new recipe to the database, the slug field will get populated.

Now, we need to tell Django to use the slug just created in the URL. Let's just create the corresponding row in `urls.py`.

```{python}
path("recipe/<str:recipe_slug>/", RecipeDetailView.as_view(), name="recipe_detail")
```

Where `RecipeDetailView` is the view where you show your recipe. It now probably looks something like this.

```{python}
class RecipeDetailView(DetailView):
    model = RecipeDetail
    template_name = "recipe/recipe_detail.html"
```

We have just the Model and the template name. Here we have the template under `recipe/recipe_detail.html`, but it can be anywhere. To make the slugs work, we need to add `slug_field` and `slug_url_kwarg` to properly parse them.

```{python}
class RecipeDetailView(DetailView):
    model = RecipeDetail
    slug_field = "recipe_slug"
    slug_url_kwarg = "recipe_slug"
    template_name = "recipe/recipe_detail.html"
```

Now that you have a link to the recipe, you can use the slug to link directly to the `RecipeDetailView` in the usual way

```{python}
href="{% url 'recipe_detail' recipe_slug=recipe.recipe_slug %}"
```

Once you run a migration with `python manage.py makemigrations` and `python manage.py migrate`, each time you insert a new recipe in the database a slug will be automatically created.

## Add slugs for previous data

Something that I didn't notice when I inserted slugs is that SLUGS WILL WORK ONLY FOR NEW DATA. As it modifies the database schema, it will only work from the moment you have included them. For old data, you need to find a way to populate your database with the expected input. In our case, it could be something that mimics the `slugify` function. We could run an SQL statement like this:

```{sql}
update recipe set recipe_slug=lower(concat(nationality, '-', type, '-dishes'));
```

This will create exactly the same pattern as our `slugify` function above. For example, if the nationality is `chinese`, and the type is `dumpling`, the field `recipe_slug`will be`chinese-dumpling-dishes`.

[google-seo-starter]: https://developers.google.com/search/docs/fundamentals/seo-starter-guide
[full_code]: https://github.com/appliku
