# Django ORM and QuerySets #

## What is this? ##
- "Object-Relational Mapping" is how we turn records in the database into objects (sometimes called 'instances'), and vice versa.  Django does most of this work for us behind the scenes.
- To work with a set of one or more objects, we first *query* them from the database.  Queries get you a list of record whose attribtes meet your criteria-- all records with this name, created after that date, etc.
- A QuerySet is the result of a query.
- The Django console lets you create, add, query, look at, modify, or remove data from the database
- If we can query the database and get the output we want, we are one step closer to using those queries to put data about the database in the view!

## Next Steps ##

Why: Put objects in the database and learn how to work with them

How:

- Open the console
  - `(myvenv) student@adminuser-VirtualBox:~/workspace > python manage.py shell`
- Import any models you want to manipulate
    - `>>> from cat_shelter.models import Cat`
- Import timezone, so we can look up cats by adoption date
    - `>>> from django.utils import timezone`
- List all instances of a model
  - `Cat.objects.all()`
- Get a specific object and refer to it with a variable
  - `thiscat = Cat.objects.get(name="Zelda")`
- Create a new item in the database
  - `Cat.objects.create(name="Toothless", age=1, color="black", fluffy=True, desc="Toothless is made of snuggles and likes to knock things over")`
-  List all instances matching some criteria
  -  `Cat.objects.filter(adopted__lte=timezone.now())`
  -  `Cat.objects.filter(fluffy=True)`
- Sort Query Results
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
      mycats = Cat.objects.all().order_by('age')
      return render(request, 'cat_shelter/current_cats.html', {'mycats' : mycats})
