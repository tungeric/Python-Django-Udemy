# Django-Python-Full-Stack-Web-Developer
Notes and files for the Python full stack developer course!

# SET UP APPLICATION!

## create environment
`conda create --name myEnv django`

## activate environment
`source activate myEnv`
  * (deactivate to deactivate)

## Create a django project command
`django-admin startproject first_project`

## Run server
`python manage.py runserver`

## Initialize django application (not the same as the full application!)
`python manage.py startapp first_app`

## Add the django application into your project `settings.py` file under "INSTALLED_APPS"
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'first_app' # <----- add this!
]
```

## In `views.py` in your application:
`from django.http import HttpResponse`
```python
def index(request):
  return HttpResponse("Trust the Process.")
```

* Each view should return an HttpResponse object


## In `urls.py` in your project:
```python
from django.conf.urls import include #Allows you to include urls.py from within your app!
from first_app import views

urlpatterns = [
    url(r'^$', views.index), # Add view to your server
    url(r'^first_app/', include('first_app.urls')), # Gets views from a urls.py file that you create in your app!
    url(r'^admin/', admin.site.urls),
]
```
  * this imports views from each application you create

## In `urls.py` in your APP:
(similar setup to urls.py in project)
```python
from django.conf.urls import url
from first_app import views

urlpatterns = [
  url(r'^$', views.index, name='index'),
]
```

## In your base project directory, add a `templates` folder.

## In `settings.py`, add a reference to the folder you just made
(right below BASE_DIR)
`TEMPLATE_DIR = os.path.join(BASE_DIR,"templates")`

Add `TEMPLATE_DIR` to `DIRS` section of `TEMPLATES` in `settings.py`

## In templates folder, create a file `index.html` where you just put your basic HTML starter stuff.
### Add a line `{{ insert_me }}` to input your template

# Add to views.py
Your `views.py` should now look like this:

```python
from django.shortcuts import render # <---- important!
from django.http import HttpResponse

# Create your views here.

def index(request):
  my_dict = {'insert_me':"Now I am from first_app/index.html!"}
  return render(request,'first_app/index.html',context=my_dict)
```