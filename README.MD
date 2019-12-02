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

8. More views
    A view is a “type” of Web page in your Django application that generally serves a specific function and has a specific template. In Django, web pages and other content are delivered by views. Each view is represented by a Python function (or method, in the case of class-based views). Django will choose a view by examining the URL that’s requested (to be precise, the part of the URL after the domain name).

    In URLconf, it use `<int:question_id>` to capture the remaining string and convert it into int type and name it as question_id.

    Each view is responsible for doing one of two things: returning an HttpResponse object containing the content for the requested page, or raising an exception such as Http404. The rest is up to you.

    Django's template system can separate the design from Python by creating a template that the view can use. Use render and map the variables to template in context.

    The render() function takes the request object as its first argument, a template name as its second argument and a dictionary as its optional third argument. It returns an HttpResponse object of the given template rendered with the given context

    Use `get_object_or_404()`， The get_object_or_404() function takes a Django model as its first argument and an arbitrary number of keyword arguments, which it passes to the get() function of the model’s manager. It raises Http404 if the object doesn’t exist There’s also a get_list_or_404() function, which works just as get_object_or_404() – except using filter() instead of get(). It raises Http404 if the list is empty.

    In `polls/urls.py`, change hard code url to `{% url 'polls:detail' question.id %}` can make it easy when change the urls. And remember to add `app_name='polls'` in `polls/urls.py`.
   

