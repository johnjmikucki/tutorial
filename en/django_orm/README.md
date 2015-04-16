# Django ORM and QuerySets #

## What is it? ##

- One way to look at, add, modify, or remove data from the database
- Allows you to get a list of database entries based on lots of different characteristics, like name, or the date in the object
- If we can query the database and get the output we want, we are one step closer to using those queries to put data about the database in the view!

## HowTo ##

- Open the console
  - `(myvenv) student@adminuser-VirtualBox:~/workspace > python manage.py shell`
  - Don't forget to import any models you want to manipulate
    - `>>> from store.models import Item`
- List all of a model object
  - `<MODEL NAME>.objects.all()`
    - `>>> Item.objects.all()`
- Get a specific object and save it to a variable
  - `<VARIABLE> = <MODEL NAME>.objects.get(<ATTRIBUTE>=<value>)`
  - `>>> myItem = Item.objects.get(name="banana")`
- Create a new item in the database
  - `<MODEL>.objects.create(<LIST OF ATTRIBUTES>)`
  -  //TODO need to figure the model out first...
-  Filtering queries
  -  `<MODEL>.objects.filter(<CRITERIA>)`
  -  //Figure out the model first...
-Change the order of query results
  - `<MODEL>.objects.order_by(<CRITERIA>)`
  - //Figure out the model
- Make query results available to your view
  - Open `store/views.py`
  - In the function for the view you are interested in:
    - Add the query and save it to a variable
      - //Figure out the model sigh.
    - Give the variable a name and pass it to the html like a dictionary
      - //Figure out model

*Example*

//TODO
