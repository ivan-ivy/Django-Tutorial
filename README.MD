# Django Tutorial

Follow the tutorial on Django website, and create my first Django App.
The app consist of two parts:

A public site that lets people view polls and vote in them.
An admin site that lets you add, change, and delete polls.


Steps:

1. initial steps
   ```
   django-admin startproject mysite
   ```
    Avoid naming projects after built-in Python or Django components. In particular, this means you should avoid using names like django (which will conflict with Django itself) or test (which conflicts with a built-in Python package).
    
    manage.py: command-line utility that lets you interact with Django project.
    inner mysite directory is the python package for the whole project,e.g. in other file use import mysite.urls.

2. development server `python manage.py runserver`

   create app: `python manage.py startapp polls`

    write views in view.py, and then map the views into a URL in urls.py. And point the root URLconf at the urls.py in root directory.

    use include to allows referencing other URLconf. path use two key word argument: route and view.

3. Database setup
   use migrate command to create necessary database tables `python manage.py migrate`

4. Create models
   models are database layout with additional metadata.
    Each model is represented by a class that subclasses django.db.models.Model. Each model has a number of class variables, each of which represents a database field in the model.
    Each field is represented by an instance of a Field class.
    The name of each Field instance (e.g. question_text or pub_date) is the field’s name, in machine-friendly format. You’ll use this value in your Python code, and your database will use it as the column name

5. Activate models
   To include app in project, add a reference to its configuration class in the INSTALL_APPS setting.
   Use makemigrations to let django know your changes. `python manage.py makemigrations polls`
   Use migration to apply the changes to database. `python manage.py migrate`

6. Shell
   `python manage.py shell` manage.py sets the DJANGO_SETTINGS_MODULE environment variable, which gives Django the Python import path to your mysite/settings.py file.

    It’s important to add __str__() methods to your models, not only for your own convenience when dealing with the interactive prompt, but also because objects’ representations are used throughout Django’s automatically-generated admin.

    Django provide shortcut for primary-key exact lookups.The following is identical to Question.objects.get(id=1).`Question.objects.get(pk=1)`

7. Create Admin
    Use `python manage.py createsuperuser` to create users. To make the admin can manage polls, register polls in `polls/admin.py`
   

