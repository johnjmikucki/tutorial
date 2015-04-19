# Django ORM and QuerySets #

## What is it? ##

- One way to look at, add, modify, or remove data from the database
- Allows you to get a list of database entries based on lots of different characteristics, like name, or the date in the object
- If we can query the database and get the output we want, we are one step closer to using those queries to put data about the database in the view!

## HowTo ##

- Open the console
  - `(myvenv) student@adminuser-VirtualBox:~/workspace > python manage.py shell`
  - Don't forget to import any models you want to manipulate
    - `>>> from cat_shelter.models import Cat`
  - Add this also so we can look up cats by adoption date
    - `>>> from django.utils import timezone`
- List all of a model object
  - `Cat.objects.all()`
- Get a specific object and save it to a variable
  - `thiscat = Cat.objects.get(name="Zelda")`
- Create a new item in the database
  - `Cat.objects.create(name="Toothless", age=1, color="black", fluffy=True, desc="Toothless is made of snuggles and likes to knock things over")`
-  Filtering queries
  -  `Cat.objects.filter(adopted__lte=timezone.now())`
  -  `Cat.objects.filter(fluffy=True)`
-Change the order of query results
  - `Cat.objects.order_by('name')`
  - `Cat.objects.order_by('-age')`
- Make query results available to your view
  - Open `cat_shelter/views.py`
  - Include the new model at the top
    - `from .models import Cat`
  - In the function for the view you are interested in:
    - Add the query and save it to a variable
      - `mycats = Cat.objects.all().order_by('age')`
    - Give the variable a name and pass it to the html like a dictionary
      - `'mycats' : mycats`

*Example*

    def current_cats(request):
      theCats = Cat.objects.all().order_by('age')
      return render(request, 'cat_shelter/current_cats.html', {'mycats' : mycats})
