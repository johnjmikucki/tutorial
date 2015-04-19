# Django Views #

## What is a View? ##

- What you actually **see** when you visit a webpage
- Can be written in any of a combination of several things including html, javascript, CSS, etc.
- Can be static (always the same) or dynamic (changes based on other stuff, like what's in the database, or what you clicked on, or what time it is, etc.)
- A request comes into your site (`critters_site`), your site forwards it to the proper application (`cat_shelter`), and the application decides what the view/webpage should look like.

## Notes ##

- Important regex things to know
  - What's a Regex?  A Regular Expression - matches strings against patterns.
  - `^` : the beginning
  - `$` : the end
  - `\d` : a digit
  - `+` : repeat one more times
  - `*` : repeat zero or more times
  - `?` : repeat zero or one times

## Next Steps ##

- Add a reference to your **application** URLs in your **site** URLs
  - This means when certain kinds of requests come into your site (`critters_site`), they will get sent to your application (`cat_shelter`) for more instructions.
  - Open `critters_site/urls.py`
  - Add a URL entry pointing to your cat_shelter.urls.  Use `r` to specify when the site should use that app
    - Adding the cat_shelter.urls using this `r` will forward **all** requests to your store app.  Basically saying "If I get any request, look for instructions `here`."
      - `url(r'', include('cat_shelter.urls')),`
    - Adding the `cat_shelter.urls` using this `r` will forward requests that start with `kitties` to the `cat_shelter` app. Basically saying "If I get a request like `http://127.0.0.1:8000/kitties/...`, look for instructions `here`."
      - `url(r'^kitties/', include('cat_shelter.urls')),`

*Example*

    from django.conf.urls import include, url
    from django.contrib import admin
    
    urlpatterns = [
      url(r'^admin/', include(admin.site.urls)),
      url(r'', include('cat_shelter.urls')),
    ]
    
- Add application-specific instructions into your **application** URLs
  - When the site `critters_site` forwards requests to our application `cat_shelter`, what should we do with them?
  - Open `cat_shelter/urls.py`
  - Add a URL entry for your view.  Use `r` to specify when the application should use that view.
    - Adding the `current_cats` using this `r` will use the `current_cats` view for empty strings--when you specify no path in the request.
      - `url(r'^$', views.current_cats),`
      - `r'^$'` : `^` is beginning and `$` is end so `^$` is "nothing between beginning and end"
    - Adding the `current_cats` using this `r` will use the `current_cats` view for the request `current`
       `url(r'^current$', views.current_cats),`

*Example*

    from django.conf.urls import include, url
    from . import views
    
    urlpatterns = [
        url(r'^$', views.current_cats),
    ]

- Create a function to call your view
  - Open `cat_shelter/views.py`
    - Add a basic function corresponding to your view (such as `current_cats`)

*Example*

    def current_cats(request):
    
      return render(request, 'cat_shelter/current_cats.html', {})
      
- Create the view that your `cat_shelter/views.py` function points at, in the indicated location
  - Create `cat_shelter/templates` and `cat_shelter/templates/cat_shelter` directories. 
  - Django convention is to create a directory inside the `templates` directory for your app (even though your templates directory is already inside a directory for your app.  Whatever.)
  - For the example above, you will create a file named `current_cats.html` in the `cat_shelter/templates/cat_shelter` directory.  You can leave it blank or [Add HTML](html/README.md)
