When you create a project using:

```bash
django-admin startproject myproject
```

Django automatically creates several **core files that control the whole framework**. Understanding these files is important to understand **how Django works internally**.

Typical structure:

```
myproject/
│
├── manage.py
│
└── myproject/
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    ├── asgi.py
    └── wsgi.py
```

Below is a **clear explanation of every important Django file**.

---

# 1️⃣ `manage.py`

### Purpose

`manage.py` is the **command-line utility used to control the Django project**.

It acts as a **wrapper around Django administrative commands**.

You use it to run commands like:

```
python manage.py runserver
python manage.py migrate
python manage.py makemigrations
python manage.py createsuperuser
```

### Example `manage.py`

```python
import os
import sys

def main():
    os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'myproject.settings')

    from django.core.management import execute_from_command_line
    execute_from_command_line(sys.argv)

if __name__ == '__main__':
    main()
```

### What happens internally

```
Command
   ↓
manage.py
   ↓
Django Management Framework
   ↓
Project Settings Loaded
   ↓
Command Executed
```

### Key Idea

`manage.py` = **entry point for all Django commands**

---

# 2️⃣ `settings.py`

### Purpose

`settings.py` contains **all configuration settings of the Django project**.

It defines:

* database
* installed apps
* middleware
* templates
* static files
* security settings

### Example Structure

```python
BASE_DIR = Path(__file__).resolve().parent.parent

SECRET_KEY = "django-secret-key"

DEBUG = True

ALLOWED_HOSTS = []
```

---

### Important Sections

| Setting          | Purpose                     |
| ---------------- | --------------------------- |
| `SECRET_KEY`     | Cryptographic security key  |
| `DEBUG`          | Debug mode                  |
| `ALLOWED_HOSTS`  | Allowed domains             |
| `INSTALLED_APPS` | Registered apps             |
| `MIDDLEWARE`     | Request/response processing |
| `DATABASES`      | Database configuration      |
| `STATIC_URL`     | Static file URL             |
| `MEDIA_ROOT`     | Uploaded files location     |

---

### Example Database Setting

```
DATABASES = {
 'default': {
   'ENGINE': 'django.db.backends.sqlite3',
   'NAME': BASE_DIR / 'db.sqlite3',
 }
}
```

If using MySQL:

```
ENGINE: django.db.backends.mysql
```

---

### Internally

```
Django Starts
     ↓
Load settings.py
     ↓
Configure Database
     ↓
Load Installed Apps
     ↓
Initialize Middleware
```

So **settings.py controls the entire Django environment**.

---

# 3️⃣ `urls.py`

### Purpose

`urls.py` defines **URL routing**.

It maps **URL → view function**.

Example:

```
User visits URL
       ↓
urls.py
       ↓
Correct View
       ↓
Response returned
```

---

### Example `urls.py`

```python
from django.contrib import admin
from django.urls import path
from blog import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.home),
]
```

---

### URL Routing Flow

```
Browser Request
       ↓
Django URL Dispatcher
       ↓
urls.py
       ↓
View Function
       ↓
Response
```

---

### Including App URLs

Large projects separate URLs per app.

```
myproject/
    urls.py
blog/
    urls.py
```

Project URLs:

```python
from django.urls import include, path

urlpatterns = [
    path('blog/', include('blog.urls')),
]
```

---

# 4️⃣ `wsgi.py`

### Purpose

`wsgi.py` allows Django to **communicate with web servers**.

WSGI = **Web Server Gateway Interface**

It connects Django with servers like:

* Gunicorn
* uWSGI
* Apache
* Nginx

---

### Example `wsgi.py`

```python
import os

from django.core.wsgi import get_wsgi_application

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'myproject.settings')

application = get_wsgi_application()
```

---

### Deployment Flow

```
Client Request
      ↓
Web Server (Nginx / Apache)
      ↓
WSGI Server (Gunicorn / uWSGI)
      ↓
wsgi.py
      ↓
Django Application
      ↓
Response
```

---

### Simple Idea

```
Browser → Server → WSGI → Django
```

---

# 5️⃣ `asgi.py`

### Purpose

`asgi.py` supports **asynchronous applications**.

ASGI = **Asynchronous Server Gateway Interface**

Used for:

* WebSockets
* Real-time chat
* async views
* long connections

---

### Example `asgi.py`

```python
import os
from django.core.asgi import get_asgi_application

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'myproject.settings')

application = get_asgi_application()
```

---

### Used With

* Daphne
* Uvicorn
* Hypercorn

---

# 6️⃣ `__init__.py`

### Purpose

Marks the directory as a **Python package**.

Usually empty.

Example:

```
__init__.py
```

---

# 🧠 Django File Responsibilities

| File          | Responsibility         |
| ------------- | ---------------------- |
| `manage.py`   | Run project commands   |
| `settings.py` | Project configuration  |
| `urls.py`     | URL routing            |
| `wsgi.py`     | Web server interface   |
| `asgi.py`     | Async server interface |
| `__init__.py` | Python package marker  |

---

# ⚙️ Complete Django Request Flow

```
Browser Request
       ↓
Web Server
       ↓
WSGI / ASGI
       ↓
Django
       ↓
urls.py
       ↓
View
       ↓
Model (Database)
       ↓
Template
       ↓
Response
```

---

✅ Since you are working on **Django ML projects (Arrhythmia detection + 3D visualization)**, understanding these files helps you know **where to place ML models, APIs, and prediction logic**.

For example:

```
views.py  → load ML model
models.py → database
urls.py   → prediction endpoint
templates → results
```

---

























