# Adding Another Page -- A Review #

## Notes ##
- In our view, we hyperlinked the cat names, but they aren't fun to click.  Let's add a "details" page for each cat.
- This exercise reviews what we already covered.  The only new trick we'll show you is how to add a single route that handles the detail pages for every cat, without having to write them all.

## Next Steps ##


### Update the URL patterns ###

Note: - To review HTML links see [Introduction to HTML](../html/README.md)

Why: So when we click a cat's name, we go to a detail page about that cat.

How: 

- Hyperlink `{{cat.name}}` to a URL that will call the detail page and pass an identifier for the cat we clicked.
    Generating URLs like these is pretty common so Django provides a shortcut for it.
	- Replace `<a href="">{{cat.name}}</a>` with `<a href="{% url 'cat_shelter.views.cat_detail' pk=cat.pk %}">{{ cat.name }}</a>`
	- "pk" stands for "primary key".  You could use whatever name you want (just don't forget!) but "pk" is convention.


### Route the URL for the detail page ###

Note: To review URLs see [Django Views](../django_views/README.md)

Note: The pk that gets passed via the URL is going to be a number.  We want the url to look like `<mywebsite>/kitty/12345` where `12345` was the pk for a particular kitty.

Why: So our app knows what to do when we ask for that URL

How:

In your app's `urls.py` file...
- There is a special syntax for capturing a variable you passed from your html (in this case, `pk`)
	- In the regex, you start with `^kitty/`
	- To capture the pk parameter, you include this special syntax
		- `(?P<pk>[0-9]+)`
	- To not match urls with trailing stuff, end the regex with `/$` 
	
*Example*

	urlpatterns = [
	  url(r'^$', views.current_cats),
	  url(r'^kitty/(?P<pk>[0-9]+/$'), views.cat_detail),
	]

### Add the appropriate view function ##

Note: For a refresher check out [Django Views](../django_views/README.md) for information about `views.py` 

Note: Visit [Django ORM](../django_orm/README.md) for a refresher on how we changed the view function to include objects from the database

Why: We need to tell Django what to do when cat_detail is called!

How:
- In `cat_shelter/views.py` we need to add the `cat_detail` function, and it needs to receive the pk variable we passed
	- We want to query for the cat whose ID matches the pk variable 
	- But what if no such cat is found?  Normally, `get` would throw a weird error.  Fortunately, Django includes a handy `get_object_or_404` function which either populates the object or returns a friendlier '404' - page not found - error.  
	- Replace the `get` function with `get_object_or_404`, passing in `Cat` instead of `Cat.object`.  Thus: `get_object_or_404(Cat, pk=pk)`
		- To use the special function, add `get_object_or_404` to your `from django.shortcuts` line at the top of the page
		- `from django.shortcuts import render, get_object_or_404`
	- Get the value from the database and pass it to the view just like we did in current_cats

### Create a template for the detail page ###
Why: Now that we have a `Cat` object, we need a template in which to display its data!

How: 

	- Visit [Using Query Data in Templates](../dynamic_data_in_templates/README.md) for a refresher on putting code into your HTML

### Optional: Add another attribute (or more) to your model ###
Why: Why Not?

How: 
	- Make changes to your `models.py`
	- Create and run the migrations
		- Check out [Django Models](../django_models/README.md) for a reminder
	- Work these new things into your view!