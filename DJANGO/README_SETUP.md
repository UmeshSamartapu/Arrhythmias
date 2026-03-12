Setting up **Django from scratch in a structured and organized way** is very important for real projects. Below is a **clean professional workflow used in industry**. 🚀

---

# 1️⃣ Install Python and Check Version

Django requires Python.

```bash
python --version
```

Recommended: **Python 3.10+**

If Python is not installed → download from
[https://python.org](https://python.org)

---

# 2️⃣ Create a Project Folder

Create a dedicated workspace.

```bash
mkdir django_projects
cd django_projects
```

Example structure:

```
django_projects/
```

---

# 3️⃣ Create Virtual Environment (VERY IMPORTANT) 🧠

Virtual environments isolate dependencies.

```bash
python -m venv env
```

Activate it:

### Windows

```bash
env\Scripts\activate
```

### Linux / Mac

```bash
source env/bin/activate
```

You will see:

```
(env) C:\django_projects>
```

---

# 4️⃣ Install Django

```bash
pip install django
```

Check installation:

```bash
django-admin --version
```

Example:

```
5.0.3
```

---

# 5️⃣ Create Django Project

```bash
django-admin startproject myproject
```

Move inside project:

```bash
cd myproject
```

Project structure:

```
myproject/
│
├── manage.py
│
└── myproject/
    │
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    ├── asgi.py
    └── wsgi.py
```

---

# 6️⃣ Create Django App

A **project contains multiple apps**.

Example:

```bash
python manage.py startapp blog
```

Structure becomes:

```
myproject/
│
├── manage.py
│
├── myproject/
│
└── blog/
    │
    ├── admin.py
    ├── apps.py
    ├── models.py
    ├── views.py
    ├── tests.py
    └── migrations/
```

---

# 7️⃣ Register App in Django

Open:

```
settings.py
```

Add the app:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    'blog',   # add this
]
```

---

# 8️⃣ Run Initial Database Migrations

Django automatically creates database tables.

```bash
python manage.py migrate
```

Tables created:

```
auth_user
django_admin_log
django_session
django_content_type
```

---

# 9️⃣ Create Superuser

Admin login account.

```bash
python manage.py createsuperuser
```

Example:

```
Username: admin
Email: admin@gmail.com
Password: ********
```

---

# 🔟 Run Development Server

```bash
python manage.py runserver
```

Open browser:

```
http://127.0.0.1:8000
```

Admin panel:

```
http://127.0.0.1:8000/admin
```

---

# 1️⃣1️⃣ Proper Production-Level Project Structure

For **organized Django projects**, use this structure.

```
myproject/
│
├── env/
│
├── manage.py
│
├── requirements.txt
│
├── README.md
│
├── .gitignore
│
├── config/
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
│
├── apps/
│   ├── users/
│   ├── blog/
│   └── payments/
│
├── templates/
│
├── static/
│
├── media/
│
└── scripts/
```

Explanation:

| Folder    | Purpose             |
| --------- | ------------------- |
| env       | virtual environment |
| apps      | all Django apps     |
| templates | HTML templates      |
| static    | CSS, JS             |
| media     | uploaded files      |
| scripts   | utility scripts     |

---

# 1️⃣2️⃣ Create Requirements File

Save dependencies:

```bash
pip freeze > requirements.txt
```

Example:

```
Django==5.0
mysqlclient==2.2
pillow==10.0
```

---

# 1️⃣3️⃣ Setup Git (Recommended)

Initialize git:

```bash
git init
```

Create `.gitignore`

```
env/
__pycache__/
*.pyc
db.sqlite3
```

---

# 1️⃣4️⃣ Django Development Workflow

Real development flow:

```
Create Model
      ↓
Run makemigrations
      ↓
Run migrate
      ↓
Create View
      ↓
Create URL
      ↓
Create Template
      ↓
Test in browser
```

Commands:

```bash
python manage.py makemigrations
python manage.py migrate
python manage.py runserver
```

---

# 1️⃣5️⃣ Example Minimal Django App

### Model

`models.py`

```python
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
```

---

### View

`views.py`

```python
from django.http import HttpResponse

def home(request):
    return HttpResponse("Hello Django")
```

---

### URL

`urls.py`

```python
from django.urls import path
from blog import views

urlpatterns = [
    path('', views.home),
]
```

---

# ⚙️ Internally What Happens When You Run Django

When you run:

```
python manage.py runserver
```

Flow:

```
Browser Request
      ↓
URL Dispatcher
      ↓
View Function
      ↓
Model (Database Query)
      ↓
Template Rendering
      ↓
HTTP Response
```

This is called **MTV Architecture**.

```
Model
Template
View
```

---

# 🧠 Professional Django Setup (Used by Experts)

```
Python
   ↓
Virtual Environment
   ↓
Install Django
   ↓
Create Project
   ↓
Create Apps
   ↓
Define Models
   ↓
Run Migrations
   ↓
Create Views
   ↓
Create URLs
   ↓
Create Templates
   ↓
Run Server
```

---


























