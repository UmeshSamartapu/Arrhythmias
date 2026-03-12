## Django — Complete Guide From Scratch

![Image](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Server-side/Django/Introduction/basic-django.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/0%2A8ZFh-CsrMi7bQG0O.jpg)

![Image](https://miro.medium.com/max/700/1%2AaICZBUzrgLgc5GoWuiFHcw.jpeg)

![Image](https://i.sstatic.net/QAxzh.png)

Django is a **high-level Python web framework** used to build **secure, scalable, and maintainable web applications quickly**.

It follows the principle:

> **“Don’t Repeat Yourself (DRY)”** and **“Batteries Included”**

Meaning Django already provides many built-in tools such as authentication, admin panel, ORM, and security.

---

# 1. What is Django?

**Django** is a backend framework written in **Python** that helps developers build web applications.

Examples of websites built with Django:

* Instagram
* Pinterest
* Mozilla
* Disqus
* NASA websites

Django helps create:

* Web applications
* APIs
* Data dashboards
* AI / ML web apps
* E-commerce systems
* Social networks

Since you work with **ML + Django projects**, it is commonly used to deploy ML models as **web applications**.

---

# 2. Why Django is Popular

Advantages:

### 1️⃣ Fast Development

Django provides built-in modules for:

* authentication
* database access
* sessions
* forms
* admin panel

So developers don't build everything from scratch.

---

### 2️⃣ Security

Django automatically protects against:

* SQL Injection
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Clickjacking

---

### 3️⃣ Scalable

Large platforms use Django.

Examples:

* Instagram handles millions of users
* Pinterest uses Django

---

### 4️⃣ Built-in Admin Panel

Django automatically creates an **admin dashboard** for database management.

Example:

```
http://127.0.0.1:8000/admin
```

You can:

* Add users
* Modify data
* Manage tables

---

# 3. Django Architecture

Django uses **MTV architecture**

```
Model
Template
View
```

It is similar to **MVC architecture**.

| MVC        | Django   |
| ---------- | -------- |
| Model      | Model    |
| View       | Template |
| Controller | View     |

---

## Model

Model represents **database structure**.

Example:

```python
class Student(models.Model):
    name = models.CharField(max_length=100)
    age = models.IntegerField()
```

Django converts this model into **SQL table automatically**.

---

## View

View contains **business logic**.

Example:

```python
from django.http import HttpResponse

def home(request):
    return HttpResponse("Hello World")
```

---

## Template

Template is **frontend HTML page**.

Example:

```html
<h1>Hello {{name}}</h1>
```

Django replaces variables dynamically.

---

# 4. Django Project Structure

When you create a project:

```
django-admin startproject myproject
```

Folder structure:

```
myproject
│
├── manage.py
│
├── myproject
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
```

Explanation:

| File        | Purpose                     |
| ----------- | --------------------------- |
| manage.py   | Command line utility        |
| settings.py | Project configuration       |
| urls.py     | URL routing                 |
| wsgi.py     | Deployment server interface |
| asgi.py     | Async server interface      |

---

# 5. Django Apps

A **project contains multiple apps**.

Example:

```
E-commerce Project
```

Apps inside:

```
accounts
products
orders
payments
```

Create app:

```
python manage.py startapp products
```

App structure:

```
products
│
├── models.py
├── views.py
├── admin.py
├── apps.py
├── tests.py
└── migrations
```

---

# 6. Django Request Response Cycle

How Django processes a request:

```
User
 ↓
Browser Request
 ↓
URL Dispatcher
 ↓
View
 ↓
Model (Database)
 ↓
Template
 ↓
Response
```

Step example:

User opens:

```
http://127.0.0.1:8000/home
```

Flow:

```
urls.py → view → model → template → response
```

---

# 7. Django Installation

### Step 1

Install Python

```
python --version
```

---

### Step 2

Create virtual environment

```
python -m venv env
```

Activate:

Windows

```
env\Scripts\activate
```

Linux / Mac

```
source env/bin/activate
```

---

### Step 3

Install Django

```
pip install django
```

Check version

```
django-admin --version
```

---

# 8. Creating First Django Project

```
django-admin startproject myproject
cd myproject
```

Run server

```
python manage.py runserver
```

Open browser

```
http://127.0.0.1:8000
```

You will see Django welcome page.

---

# 9. Creating First App

```
python manage.py startapp blog
```

Register app in **settings.py**

```python
INSTALLED_APPS = [
'blog',
]
```

---

# 10. URL Routing

File:

```
urls.py
```

Example:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home),
]
```

---

# 11. Views

Example:

```python
from django.shortcuts import render

def home(request):
    return render(request,'home.html')
```

---

# 12. Templates

Folder structure:

```
templates
     home.html
```

Example:

```html
<h1>Welcome to Django</h1>
```

---

# 13. Django Models (Database)

Django supports:

* SQLite
* MySQL
* PostgreSQL
* Oracle

Example model:

```python
from django.db import models

class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.FloatField()
```

---

# 14. Migrations

Django converts models to SQL.

Commands:

```
python manage.py makemigrations
```

```
python manage.py migrate
```

This creates database tables.

---

# 15. Django Admin Panel

Create admin user:

```
python manage.py createsuperuser
```

Login:

```
http://127.0.0.1:8000/admin
```

Register model:

```python
from django.contrib import admin
from .models import Product

admin.site.register(Product)
```

---

# 16. Django ORM (Object Relational Mapper)

Instead of SQL queries you use Python.

Example:

Create object

```python
Product.objects.create(name="Laptop",price=50000)
```

Fetch data

```python
Product.objects.all()
```

Filter

```python
Product.objects.filter(price__gt=10000)
```

---

# 17. Django Forms

Used for user input.

Example:

```python
from django import forms

class ContactForm(forms.Form):
    name = forms.CharField()
    email = forms.EmailField()
```

---

# 18. Django Authentication System

Built-in features:

* login
* logout
* password reset
* user registration
* permissions

Example:

```python
from django.contrib.auth.models import User
```

---

# 19. Django Static Files

Used for:

* CSS
* JavaScript
* Images

Folder:

```
static
   css
   js
   images
```

Example:

```html
<link rel="stylesheet" href="{% static 'css/style.css' %}">
```

---

# 20. Django Deployment

Popular deployment platforms:

* Render
* AWS
* DigitalOcean
* Heroku
* Railway

Production stack example:

```
Client
 ↓
Nginx
 ↓
Gunicorn
 ↓
Django
 ↓
PostgreSQL
```

---

# 21. Django for AI / ML Projects

Since you work on **AI + ML projects**, Django is used to deploy models.

Example pipeline:

```
Dataset
 ↓
Model Training (Python)
 ↓
Save Model (.pkl)
 ↓
Django Backend
 ↓
User Upload Image / Video
 ↓
Model Prediction
 ↓
Display Result
```

Example:

* Deepfake detection
* Crop detection
* ECG classification
* Traffic forecasting

Exactly like the projects you are building.

---

# 22. Advanced Django Topics

Important advanced concepts:

* Django REST Framework (APIs)
* Middleware
* Signals
* Celery (background tasks)
* WebSockets
* Django Channels
* Caching
* Async Django
* Microservices architecture

---

# 23. Common Django Commands

| Command         | Purpose           |
| --------------- | ----------------- |
| startproject    | create project    |
| startapp        | create app        |
| runserver       | start server      |
| makemigrations  | create migration  |
| migrate         | apply migration   |
| createsuperuser | create admin user |
| shell           | open Django shell |

---

# 24. Real Django Project Example

Example project architecture:

```
AI Deepfake Detector
│
├── frontend (templates)
├── upload video
├── extract frames
├── CNN model prediction
├── database storage
└── result visualization
```

This is very similar to your **Arrhythmia + 3D Heart visualization project**.

---

# 25. Django vs Other Frameworks

| Feature        | Django     | Flask      | Node.js        |
| -------------- | ---------- | ---------- | -------------- |
| Language       | Python     | Python     | JavaScript     |
| Complexity     | Medium     | Simple     | Medium         |
| Built-in tools | Many       | Few        | Few            |
| Best for       | Large apps | Small apps | Real-time apps |

---

# 26. When to Use Django

Use Django for:

* AI web apps
* ML dashboards
* E-commerce
* CMS
* enterprise apps
* REST APIs
* admin dashboards

---

✅ **In simple words**

Django is a **complete backend framework** that manages:

```
URL routing
Database
User authentication
Templates
Security
Admin panel
Deployment
```

---



































## How Django Works Internally (Step-by-Step)

![Image](https://miro.medium.com/0%2AsKcHbUZUKssndJKp)

![Image](https://i.sstatic.net/r91Zn.png)

![Image](https://learndjango.com/static/images/django_architecture.jpg)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1054/0%2A5B0GwJEN3zVhqnUn.png)

When a user opens a Django website, many internal components work together to process the request and return a response. Understanding this **request–response lifecycle** is important for backend development.

---

# 1. High-Level Flow

The basic Django workflow:

```
User (Browser)
      ↓
Web Server (Gunicorn / uWSGI)
      ↓
WSGI / ASGI Interface
      ↓
Django Framework
      ↓
Middleware
      ↓
URL Dispatcher
      ↓
View
      ↓
Model (Database via ORM)
      ↓
Template
      ↓
HttpResponse
      ↓
Browser
```

---

# 2. Step 1 — User Sends HTTP Request

A user types a URL:

```
http://example.com/products
```

The browser sends an **HTTP request** to the server.

Example request:

```
GET /products HTTP/1.1
Host: example.com
```

The request contains:

* HTTP method (GET, POST)
* headers
* cookies
* request body
* URL

---

# 3. Step 2 — Web Server Receives Request

A **web server** receives the request.

Common servers:

* **Nginx**
* **Apache**

In production architecture:

```
Browser
   ↓
Nginx
   ↓
Gunicorn
   ↓
Django
```

Role of Nginx:

* handle static files
* reverse proxy
* load balancing
* security

---

# 4. Step 3 — WSGI / ASGI Interface

The request is passed to Django through:

### WSGI (Web Server Gateway Interface)

Used for **synchronous applications**.

File:

```
wsgi.py
```

Example:

```python
application = get_wsgi_application()
```

---

### ASGI (Asynchronous Server Gateway Interface)

Used for **async features** like:

* WebSockets
* real-time chat
* async views

File:

```
asgi.py
```

Example:

```python
application = get_asgi_application()
```

---

# 5. Step 4 — Django Loads Settings

Django loads configuration from:

```
settings.py
```

Important settings:

* installed apps
* database configuration
* middleware
* templates
* static files

Example:

```python
INSTALLED_APPS = [
'django.contrib.admin',
'django.contrib.auth',
'myapp'
]
```

---

# 6. Step 5 — Middleware Processing

Before the request reaches the view, **middleware layers process it**.

Middleware acts like **filters**.

Example flow:

```
Request
 ↓
Security Middleware
 ↓
Session Middleware
 ↓
Authentication Middleware
 ↓
View
```

Example middleware list:

```python
MIDDLEWARE = [
'django.middleware.security.SecurityMiddleware',
'django.contrib.sessions.middleware.SessionMiddleware',
'django.middleware.common.CommonMiddleware',
]
```

Middleware tasks:

* authentication
* sessions
* CSRF protection
* request modification
* logging

---

# 7. Step 6 — URL Dispatcher

Django checks **URL patterns** to find which view should handle the request.

File:

```
urls.py
```

Example:

```python
urlpatterns = [
    path('products/', views.product_list),
]
```

If user requests:

```
/products
```

Django maps it to:

```
views.product_list
```

This process is called **URL routing**.

---

# 8. Step 7 — View Function Executes

The view contains **business logic**.

Example:

```python
def product_list(request):
    products = Product.objects.all()
    return render(request,'products.html',{'products':products})
```

Tasks performed in views:

* fetch data from database
* process user input
* call machine learning models
* render templates

For example in your projects:

```
upload ECG
 ↓
CNN model prediction
 ↓
return classification
```

---

# 9. Step 8 — Model Interaction (Database)

Views interact with database through **Django ORM**.

Instead of SQL queries:

```
SELECT * FROM products;
```

You write Python code:

```python
Product.objects.all()
```

Django ORM converts it internally into SQL queries.

Example:

```
Python ORM
     ↓
SQL Query
     ↓
Database
```

Supported databases:

* SQLite
* MySQL
* PostgreSQL
* Oracle

---

# 10. Step 9 — Template Rendering

If the view returns a template:

Example:

```python
return render(request,'products.html',context)
```

Django loads HTML template.

Example template:

```html
<h1>Products</h1>

{% for product in products %}
<p>{{product.name}}</p>
{% endfor %}
```

Template engine replaces variables.

Output becomes:

```html
<h1>Products</h1>
<p>Laptop</p>
<p>Phone</p>
```

---

# 11. Step 10 — Response Creation

The final output is converted into **HttpResponse**.

Example:

```python
from django.http import HttpResponse

return HttpResponse("Hello World")
```

Or HTML response.

---

# 12. Step 11 — Middleware Response Processing

Before sending response to the browser, middleware runs again.

Flow:

```
View Response
 ↓
Middleware
 ↓
Final Response
```

Tasks:

* modify response
* add headers
* compress data

---

# 13. Step 12 — Response Sent to Browser

Finally:

```
Django → Web Server → Browser
```

Browser renders:

* HTML
* CSS
* JavaScript

User sees the webpage.

---

# 14. Full Internal Django Flow (Simplified)

```
1 Browser Request
2 Web Server (Nginx)
3 WSGI / ASGI
4 Django Settings Loaded
5 Middleware (request processing)
6 URL Dispatcher
7 View Function
8 ORM → Database
9 Template Rendering
10 HttpResponse
11 Middleware (response processing)
12 Response to Browser
```

---

# 15. Real Example (Your ML Project)

Example for your **Arrhythmia Detection Project**:

```
User Upload ECG
        ↓
Django View receives file
        ↓
Preprocess ECG signal
        ↓
CNN Model Prediction
        ↓
Result (Normal / Arrhythmia)
        ↓
3D Heart Visualization
        ↓
Template renders result
        ↓
Browser displays output
```

---

# 16. Django Internally Uses Many Components

Core internal modules:

| Component             | Purpose                     |
| --------------------- | --------------------------- |
| URL Resolver          | routes requests             |
| ORM                   | database abstraction        |
| Template Engine       | HTML rendering              |
| Middleware            | request/response processing |
| Authentication System | login system                |
| Admin Interface       | database management         |

---

# 17. Why Django is Fast for Development

Because Django already includes:

* authentication
* ORM
* admin panel
* form handling
* security
* caching

So developers focus only on **business logic**.

---

✅ **In one sentence**

Django works by receiving a request, routing it through middleware and URL patterns, executing a view that interacts with models and templates, and returning a response back to the browser.

---
































## Complete Django Internal Architecture (Deep Dive)

![Image](https://se.ewi.tudelft.nl/desosa2019/chapters/django/images/django/Django_modules.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/0%2Ar7ALulxaXPSboehX.jpg)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/0%2A8ZFh-CsrMi7bQG0O.jpg)

![Image](https://www.tutorjoes.in/img/python_django/work.jpg)

Django is built as a **layered framework** where many internal components work together to handle web requests, interact with databases, render templates, and send responses.

At a high level Django architecture contains these layers:

```
Client (Browser)
       ↓
Web Server
       ↓
WSGI / ASGI Interface
       ↓
Django Core Framework
       ↓
Middleware Layer
       ↓
URL Dispatcher
       ↓
Views
       ↓
Models / ORM
       ↓
Database
       ↓
Template Engine
       ↓
Response
```

Let's break down each internal component.

---

# 1. Client Layer

The **client** is usually:

* Web browser
* Mobile application
* API client (Postman)
* Frontend frameworks (React / Angular)

Example request:

```
GET /predict HTTP/1.1
Host: example.com
```

The client sends:

* HTTP request
* headers
* cookies
* request body

---

# 2. Web Server Layer

Before Django receives a request, a **web server** handles it.

Common servers:

* **Nginx**
* **Apache**

Typical architecture:

```
Client
   ↓
Nginx
   ↓
Gunicorn / uWSGI
   ↓
Django
```

Responsibilities:

* reverse proxy
* load balancing
* SSL termination
* serving static files

---

# 3. WSGI / ASGI Interface

Django communicates with web servers using interfaces.

## WSGI (Web Server Gateway Interface)

Used for **synchronous applications**.

File:

```
wsgi.py
```

Example:

```python
from django.core.wsgi import get_wsgi_application

application = get_wsgi_application()
```

---

## ASGI (Asynchronous Server Gateway Interface)

Used for:

* WebSockets
* async views
* real-time applications

File:

```
asgi.py
```

Example:

```python
from django.core.asgi import get_asgi_application

application = get_asgi_application()
```

---

# 4. Django Core Framework

The Django core framework contains internal modules:

```
django/
 ├── http
 ├── urls
 ├── views
 ├── middleware
 ├── template
 ├── db
 ├── forms
 └── auth
```

These modules handle:

* HTTP processing
* routing
* templates
* authentication
* database operations

---

# 5. Settings System

The **settings module** configures the entire Django project.

File:

```
settings.py
```

Important configurations:

```
INSTALLED_APPS
DATABASES
MIDDLEWARE
TEMPLATES
STATICFILES
AUTHENTICATION
```

Example:

```python
DATABASES = {
 'default': {
   'ENGINE': 'django.db.backends.mysql',
   'NAME': 'mydb'
 }
}
```

Django loads settings **once when the server starts**.

---

# 6. Middleware Layer

Middleware acts like a **pipeline** between request and response.

Request Flow:

```
Request
   ↓
Middleware 1
   ↓
Middleware 2
   ↓
View
```

Response Flow:

```
View
   ↓
Middleware 2
   ↓
Middleware 1
   ↓
Response
```

Examples:

| Middleware               | Purpose           |
| ------------------------ | ----------------- |
| SecurityMiddleware       | security headers  |
| SessionMiddleware        | session handling  |
| AuthenticationMiddleware | user login system |
| CsrfViewMiddleware       | CSRF protection   |

Example configuration:

```python
MIDDLEWARE = [
 'django.middleware.security.SecurityMiddleware',
 'django.contrib.sessions.middleware.SessionMiddleware',
 'django.middleware.csrf.CsrfViewMiddleware'
]
```

---

# 7. URL Dispatcher

The **URL resolver** maps URLs to views.

File:

```
urls.py
```

Example:

```python
urlpatterns = [
 path('predict/', views.predict),
 path('login/', views.login)
]
```

Internal process:

```
Incoming URL
     ↓
Regex matching
     ↓
Corresponding view selected
```

Django uses **pattern matching** to find the correct view.

---

# 8. Views Layer

Views contain the **application logic**.

Example:

```python
def predict(request):

    result = model.predict(data)

    return render(request,"result.html",{'result':result})
```

Responsibilities:

* handle requests
* process data
* call models
* return response

Types of views:

1. Function-Based Views (FBV)

```
def home(request)
```

2. Class-Based Views (CBV)

```
class HomeView(View)
```

---

# 9. Models Layer

Models represent **database tables**.

Example:

```python
class Product(models.Model):

    name = models.CharField(max_length=100)

    price = models.FloatField()
```

Django converts this into SQL table:

```
CREATE TABLE product(
id INT,
name VARCHAR(100),
price FLOAT
)
```

Models contain:

* fields
* relationships
* validation rules

---

# 10. Django ORM (Object Relational Mapper)

ORM converts **Python code → SQL queries**.

Example:

Python:

```python
Product.objects.filter(price__gt=1000)
```

Generated SQL:

```
SELECT * FROM product WHERE price > 1000;
```

Advantages:

* no raw SQL required
* database abstraction
* easier migrations

Supported databases:

* SQLite
* MySQL
* PostgreSQL
* Oracle

---

# 11. Template Engine

Templates generate **dynamic HTML pages**.

Example template:

```html
<h1>{{title}}</h1>

{% for item in products %}
<p>{{item.name}}</p>
{% endfor %}
```

Django replaces variables dynamically.

Template engine components:

```
Templates
Template tags
Template filters
Context variables
```

---

# 12. Forms System

Django forms manage:

* user input
* validation
* HTML form rendering

Example:

```python
class ContactForm(forms.Form):

    name = forms.CharField()

    email = forms.EmailField()
```

Django automatically validates input.

---

# 13. Authentication System

Django provides a built-in authentication system.

Features:

* login
* logout
* password hashing
* user permissions
* user groups

Example:

```python
from django.contrib.auth.models import User
```

---

# 14. Admin Interface

Django automatically generates an **admin dashboard**.

URL:

```
/admin
```

Register models:

```python
admin.site.register(Product)
```

Admin features:

* CRUD operations
* filtering
* search
* authentication

---

# 15. Static Files System

Handles:

* CSS
* JavaScript
* Images

Structure:

```
static/
   css/
   js/
   images/
```

Example:

```html
<link rel="stylesheet" href="{% static 'css/style.css' %}">
```

---

# 16. Caching System

Caching improves performance.

Types:

* database cache
* memory cache
* Redis cache
* Memcached

Example:

```python
from django.core.cache import cache
```

---

# 17. Signals System

Signals allow components to **communicate automatically**.

Example:

```
User created
     ↓
Send welcome email
```

Example code:

```python
post_save.connect(create_profile, sender=User)
```

---

# 18. Django Management Commands

Commands executed using:

```
python manage.py
```

Examples:

```
runserver
makemigrations
migrate
createsuperuser
shell
```

`manage.py` acts as **project control interface**.

---

# 19. Django Migration System

Migrations convert models into database schema.

Steps:

```
models.py
     ↓
makemigrations
     ↓
migration files
     ↓
migrate
     ↓
database tables created
```

Migration file example:

```
0001_initial.py
```

---

# 20. Complete Django Internal Workflow

```
Browser
   ↓
Web Server (Nginx)
   ↓
WSGI / ASGI
   ↓
Django Settings Loaded
   ↓
Middleware (request processing)
   ↓
URL Resolver
   ↓
View
   ↓
Model / ORM
   ↓
Database
   ↓
Template Engine
   ↓
HttpResponse
   ↓
Middleware (response processing)
   ↓
Browser
```

---

# 21. Example: ML Project with Django Architecture

Example pipeline for your **ECG Arrhythmia project**:

```
User uploads ECG signal
         ↓
Django view receives file
         ↓
Signal preprocessing
         ↓
CNN model prediction
         ↓
Result classification
         ↓
3D heart visualization
         ↓
Template renders result
         ↓
Browser shows output
```

---

# 22. Major Django Internal Components

| Component       | Role                       |
| --------------- | -------------------------- |
| URL Resolver    | route URLs                 |
| Middleware      | request/response filtering |
| Views           | business logic             |
| Models          | database schema            |
| ORM             | SQL generation             |
| Template Engine | HTML rendering             |
| Authentication  | user management            |
| Admin           | database interface         |
| Forms           | user input validation      |

---

✅ **In simple terms**

Django architecture is a **layered system** where:

```
Request → Middleware → URL Router → View → ORM → Database → Template → Response
```

---
