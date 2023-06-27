---
layout: post
title: "A simple blog for my Django App"
categories: diary
tags: indie hacking
---

I wanted to make a blog page for datainternships.co the other day and started to look on the web, as I always do because I am a shitty programmer. The only thing I could find was the same flavor of post on how to set up a model, with blog post name, tags and description, then the template, slugs and whatnot. Sounded too complicated, I just wanted to have a page that listed all my blog posts and links to the page where each post was. Nothing fancy. So, I set up something and maybe it will be useful for you too.

As I said, I aimed at creating a single page, called `blog`. On this page, I wanted a list of my blog posts. My blog posts will live as HTML pages in some directory under my website. I figured out I could it in a few steps.

Create a new view for the blog post list in `views.py`. This will be some `BlogPageView(TemplateView)` that returns the `blog.html` template.

Create a view for the blog posts themselves. This will be a view that returns a different page according to which blog post the user selects. You just need to modify the `template_name` in `get_context_data`.

```
class ArticleView(TemplateView):

    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        self.template_name = f"blog/{self.kwargs['article']}.html"
        return context
```

Now, I need to pass the `article` parameter to the view from the url. I mododify the `urls.py` just by adding `path("blog/<str:article>/", ArticleView.as_view(), name="article")`.

That's it. In the `blog.html` template, I simply refer to the article with `href="/blog/article-name"`.

Hope it was useful. No models, no DB changes, migrations and other unnecessary stuff.
