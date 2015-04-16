# Django Views #

## What is it? ##

- What you actually **see** when you visit a webpage
- Can be written in any of a combination of several things including html, javascript, CSS, etc.
- Can be static (always the same) or dynamic (changes based on other stuff, like what's in the database, or what you clicked on, or what time it is, etc.)
- A request comes into your site (`mysite`), your site forwards it to the proper application (`store`), and the application decides what the view/webpage should look like.

## HowTo ##

- Important regex things to know
  - `^` : the beginning
  - `$` : the end
  - `\d` : a digit
  - `+` : repeat one more times
  - `*` : repeat zero or more times
  - `?` : repeat zero or one times

- Add a reference to your **application** URLs in your **site** URLs
  - This means when certain kinds of requests come into your site (`mysite`), they will get sent to your application (`store`) for more instructions.
  - Open `mysite/urls.py`
  - Add a URL entry pointing to your store.urls.  Use `r` to specify when the site should use that app
    - Adding the store.urls using this `r` will forward **all** requests to your store app.  Basically saying "If I get any request, look for instructions `here`."
      - `url(r'', include('store.urls')),`
    - Adding the store.urls using this `r` will forward requests that start with `coolstore` to the store app. asically saying "If I get a request like <mywebsite>/coolstore/..., look for instructions `here`."
      - `url(r'^coolstore', include('store.urls')),`

*Example*

    from django.conf.urls import include, url
    from django.contrib import admin
    
    urlpatterns = [
      url(r'^admin/', include(admin.site.urls)),
      url(r'', include('blog.urls')),
    ]
    
- Add application-specific instructions into your **application** URLs
  - When the site `mysite` forwards requests to our application `store`, what should we do with them?
  - Open `store/urls.py`
  - Add a URL entry for your view.  Use `r` to specify when the application should use that view.
    - Adding the `inventory_list` using this `r` will use the `inventory_list` view for empty strings--when you specify no path in the request.
      - `url(r'^$', views.inventory_list),`
      - `r'^$'` : `^` is beginning and `$` is end so `^$` is "nothing between beginning and end"
    - Adding the `inventory_list` using this `r` will use the `inventory_list` view for the request `list`
       `url(r'^list$', views.inventory_list),`

*Example*

    from django.conf.urls import include, url
    from . import views
    
    urlpatterns = [
        url(r'^$', views.inventory_list),
    ]

- Create a function to call your view
  - Open `store/views.py`
    - Add a basic function corresponding to your view (such as `inventory_list`)

*Example*

    def inventory_list(request):
    
      return render(request, 'store/inventory_list.html', {})
      
- Create the view that your `store/views.py` function points at, in the indicated location
  - These views will be called "templates".  Create a "templates" directory in your `store` directory.
  - It is a convention in Django for some reason to create a directory inside the `templates` directory for your app (even though your templates directory is already inside a directory for your app.  Whatever.)
    - Under `templates` (which is under `store`) make another directory called `store`
  - For the example above, you will create a file named `inventory_list.html` in the `store/templates/store` directory.  You can leave it blank or [Add HTML](html/README.md)
