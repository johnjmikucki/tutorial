# Getting Started with Django #

## What is it? ##

- A web framework written and manipulated in Python.
- Can be used to build scaffolding (basically mostly-empty starter files) for a new web application
- Invisibly handles a lot of the data movement that needs to happen to move and update stuff in the database.

## HowTo ##

- **NOTE** From here on out, anything you call from the command line must be called with the virtualenv running.  If you do not see `(myvenv)` (or `(whatever you named it)`) at the beginning of your command line prompt, go back and start virtualenv

- Install Django in virtualenv
  - Make sure your virtualenv is running (see [Introduction to Python](python_introduction/README.md) for a reminder)
  - Install Django using pip

*Example*

    (myvenv) student@adminuser-VirtualBox:~/workspace > pip install django==1.8
    Downloading/unpacking django==1.8
    Installing collected packages: django
    Successfully installed django
    Cleaning up...

- Start a new Django project
  - You can replace `mysite` with whatever you want to call it.  Just don't forget!
  - `(myvenv) student@adminuser-VirtualBox:~/workspace > django-admin startproject mysite .`
  - The `.` is **VERY IMPORTANT**.  It tells Django to make the new website in your current directory.

- Start a new Django app
  - You can replace `store` with whatever you want to call it.  Just don't forget!
  - `(myvenv) student@adminuser-VirtualBox:~/workspace > python manage.py startapp store`
  - Add your new app to the settings for your site, in `mysite/settings.py`
  
*Example*

    INSTALLED_APPS = (
      'django.contrib.admin',
      'django.contrib.auth',
      'django.contrib.contenttypes',
      'django.contrib.sessions',
      'django.contrib.messages',
      'django.contrib.staticfiles',
      'store',
    )

- Start the local server 
  - If you want, you can leave your server running in one tab and do other things in the terminal in a new/different tab!  Just make sure you're in the right directory and you have started virtualenv.
  - `(myvenv) student@adminuser-VirtualBox:~/workspace > python manage.py runserver`
  - You can look at your website at `http://127.0.0.1:8000/`
