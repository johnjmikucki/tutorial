# Adding Another Page -- A Review #

- We made the cat names links in our view.  We will walk through adding a "details" page for each cat.
- This is intended to review what we have already covered.  There will be links back to the relevant chapters.  The new information is mostly just going to be how to make a route that goes to the details page of a specific cat, for every cat, without having to write them all.

## Next Steps ##

- We want the links in our view to go to a detail page about the cat we clicked on.
	- To review HTML links see [Introcuction to HTML](en/html/README.md)
	- We're going to change the line with `{{cat.name}}` to something that will call the detail page and also pass an identifier for the cat we're clicking on
		- Replace `<a href="">{{cat.name}}</a>` with `<a href="{% url 'cat_shelter.views.cat_detail' pk=cat.pk %}">{{ cat.name }}</a>`
		- "pk" is "primary key".  You could call this whatever you want (just don't forget!) but it is common practice to use "pk".
- Add the url for the detail page in your app's `urls.py` file
	- To review URLs see [Django Views](en/django_views/README.md)
	- The pk that gets returned is going to be a number.  We're going to want the url to look like `<mywebsite>/kitty/12345` where `12345` if `12345` was the pk for a particular kitty.
	- There is a special syntax for capturing a variable you passed from your html (in this case, pk)
		- In the regex, you want to start with `^kitty/`
		- To capture the pk, in the regex you will also include this special syntax
			- `(?P<pk>[0-9]+)`
		- End the regex with `/$` to say "that's all we want there to be from beginning to end

*Example*

	urlpatterns = [
	  url(r'^$', views.current_cats),
	  url(r'^kitty/(?P<pk>[0-9]+/$'), views.cat_detail),
	]

- Add the appropriate view function and catch the variable we passed in
	- In `cat_shelter/views.py` we need to add the `cat_detail` function, and it needs to catch the pk variable we passed
		- For a refresher check out [Django Views](en/django_views/README.md) for information about `views.py` 
		- Visit [Django ORM](en/django_orm/README.md) for a refresher on how we changed the view function to include objects from the database
	- We want to get the cat corresponding to the pk variable from the database
	- To protect the site from throwing a weird error if the user tries to select an item that doesn't exist (like, they type in a random number instead of clicking a link) replace the `get` function with the special function `get_object_or_404`. Instead of calling this on `Cat.object` you tell it you want to use it on `Cat`.  Looks like `get_object_or_404(Cat, pk=pk)`
		- To use it, you must add `get_object_or_404` to your `from django.shortcuts` line at the top of the page
		- `from django.shortcuts import render, get_object_or_404`
	- Get the value from the database and pass it to the view just like we did in current_cats

- Create a template for the detail page
	- Visit [Using Query Data in Templates](en/dynamic_data_in_templates/README.md) for a refresher on putting code into your HTML


