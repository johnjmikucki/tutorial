# Django Models #

## What Are They? ##
- A description of a class ("Cat") of objects ("Fluffy", "Fuzzbucket", "Patches", "Lady Yarnsbury") 
- Most web apps have many objects to manage and relate to each other.  Doing so manually is a pain.  Instead, Django can help keep track of objects in our database.
- Before we can manage objects in the databse, we must *model* the objects' classes in Django.
- Models describe objects' *attributes* (e.g. `name`, `date`, `description`)
- Additionally, we often use Models to describe *methods* / or *behaviors* (`print`, `set_name`, `buy`, `apply_discount`, etc) that make sense in the context of an object.  So, Fluffy's meow() might sound different from that of the Lady Yarnsbury...


## Next Steps ##

### Understand your Objects ###

Why: We need to manage lots of 'somethings'.  Here, it's cats.

How: Think about your objects.  What attributes do they share that you care about?  What sort of values do they have?

*Example*
A cat

        Cat
        ------------------------
        Name
        Age
        Color
        Fluffy?
        Description
        Adopted
    
### Model your object in Django
Why:  So Django can help us herd our cats.

How:
  - Open `cat_shelter/models.py`
  - Add a new `class` to the `models.py` file that describes your model!

*Example*

    from django.db import models
    from django.utils import timezone
    
    class Cat(models.Model):
      name = models.CharField(max_length=200)
      age = models.IntegerField()
      color = models.CharField(max_length=200)
      desc = models.TextField()
      adopted = models.DateTimeField( blank=True, null=True )
      fluffy = models.BooleanField()
    
      def adopt(self):
        self.adopted = timezone.now()
        self.save()
    
      def __str__(self):
        return self.name

### Create a database ###
Why: We need a place to put all our cat information!

How: 
This command makes a basic (empty) database.  You only need to call it once per website.
- `(myvenv) student@adminuser-VirtualBox:~/workspace > python manage.py migrate`

### Add the model to the database ###
Why: So Django and the database are ready to store our cat info!

How:

- Create the migration-- instructions on how to change the database when you change your models' attributes.  The migration script is basically a magical script that adds or removes stuff for your application within your site.  You will need to call this any time you want to change or add a model to the `cat_shelter`
    - `(myvenv) student@adminuser-VirtualBox:~/workspace > python manage.py makemigrations cat_shelter`

- Perform that migration on the database
    - `(myvenv) student@adminuser-VirtualBox:~/workspace > python manage.py migrate cat_shelter`

### Optional: Create an admin user for your app ###
**Note** This isn't required, but sometimes it's more convenient to modify and manipulate Cats in a browser than instead via the console (which we'll learn about in a few chapters).

Why: Allows you to tinker with models via the browser instead of by hand

How:

- Register your model with the application admin
    - Open `cat_shelter/admin.py`
    - Under `from django.contrib import admin` add an import statement for your model
    - `from .models import Cat`
- Register `Cat` with the admin
    - `admin.site.register(Cat)`
- Create a superuser/admin user
    - `(myvenv) student@adminuser-VirtualBox:~/workspace > python manage.py createsuperuser`
    - `Username: ` (pick one you'll remember!  I suggest `admin`)
    - `Email address: ` (you can make this up if you want or use your real one)
    - `Password: ` (don't forget your password!  You'll need it later)
    - `Password (again): ` (make sure you typed your password correctly
    - `Superuser created successfully.`
- Request the `admin` page on your website
    - Visit `http://127.0.0.1:8000/admin/`
    - Log in using the superuser username and password you just created
- Add, edit, delete `Cat` entries to your heart's content!
