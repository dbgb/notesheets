# Working with Django: Notesheet

## Set up virtual environment and dependencies

```shell
mkdir <project_name> && cd $_

pipenv shell

pipenv install django <other_packages>

pipenv install --dev autopep8 <other_dev_packages>
```

## Initialize Django project and database

```shell
django-admin startproject <project_name>

cd <project_name>

vim <project_name>/settings.py

python manage.py migrate

python manage.py startapp <app_name>

python manage.py runserver <port>

python manage.py migrate
```

## Create and register models

```shell
vim <app_name>/models.py

vim <project_name>/settings.py

python manage.py makemigrations

python manage.py migrate
```

## Create data in the Django shell

```shell
python manage.py shell
```

```python
from <model_name>.models import <Model>

<Model>.objects.create(property_1="p1", property_2="p2") # etc...

exit()
```
