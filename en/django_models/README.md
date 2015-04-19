# Django Models #

## What is it? ##

- Models represent things (called "objects") that we want to keep in the database.
- Models describe objects *attributes* -- information about the object (e.g. `name`, `date`, `description`)
- Models describe objects' *methods* -- behaviors related to the object (`print`, `set_name`, `buy`, `apply_discount`, etc)

## Next Steps ##

- Design a model

*Example*
Creating a model of a cat

        Cat
        ------------------------
        Name
        Age
        Color
        Fluffy?
        Description
        Adopted
    
- Add your newly created model to the application
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

- Set up the database
  - This command makes a basic (empty) database.  You only need to call it once per website
    - `(myvenv) student@adminuser-VirtualBox:~/workspace > python manage.py migrate`

- Add the model to the database
  - Creates the migration (basically a magical script that adds or removes stuff) for your application within your site.  You will need to call this any time you want to change or add a model to the `cat_shelter`
    - `(myvenv) student@adminuser-VirtualBox:~/workspace > python manage.py makemigrations cat_shelter`
- Perform that migration on the database
    - `(myvenv) student@adminuser-VirtualBox:~/workspace > python manage.py migrate cat_shelter`

- Create the admin user to allow for tinkering with models via the browser
  - This isn't required, but setting up the "admin" user and associated routes lets us modify and manipulate any models we register with the admin user in the browser instead of only via the console (which we'll learn about in a few chapters)
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
    - `http://127.0.0.1:8000/admin/`
  - Log in using the superuser username and password you just created
  - Add, edit, delete `Cat` entries to your heart's content!
