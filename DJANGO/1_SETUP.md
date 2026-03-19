Here are the **most important Django commands** (clean + simple 🔥):

---

# 🚀 **1. Project Setup Commands**

### 👉 Install Django

```bash
pip install django
```

### 👉 Create Project

```bash
django-admin startproject myproject
```

### 👉 Move into project

```bash
cd myproject
```

### 👉 Run Server

```bash
python manage.py runserver
```

---

# 📦 **2. App Management**

### 👉 Create App

```bash
python manage.py startapp myapp
```

### 👉 Register App

(Add in `settings.py`)

```python
INSTALLED_APPS = ['myapp']
```

---

# 🧠 **3. Database Commands**

### 👉 Make Migrations

```bash
python manage.py makemigrations
```

### 👉 Apply Migrations

```bash
python manage.py migrate
```

### 👉 Show Migrations

```bash
python manage.py showmigrations
```

---

# 👤 **4. Admin & Users**

### 👉 Create Superuser

```bash
python manage.py createsuperuser
```

### 👉 Access Admin Panel

```
http://127.0.0.1:8000/admin/
```

---

# 🔍 **5. Debug & Shell**

### 👉 Open Django Shell

```bash
python manage.py shell
```

### 👉 Check SQL Queries

```bash
python manage.py dbshell
```

---

# 📁 **6. Static & Media**

### 👉 Collect Static Files

```bash
python manage.py collectstatic
```

---

# ⚡ **7. Useful Development Commands**

### 👉 Run Specific Port

```bash
python manage.py runserver 8001
```

### 👉 Run on Network (for mobile testing)

```bash
python manage.py runserver 0.0.0.0:8000
```

---

# 🧹 **8. Reset / Cleanup**

### 👉 Delete all migrations (manual)

```bash
rm -rf migrations/
```

### 👉 Flush Database

```bash
python manage.py flush
```

---

# 🧪 **9. Testing**

### 👉 Run Tests

```bash
python manage.py test
```

---

# 🧠 **Pro Tip (Important for You 🚀)**

For your **AI + Django projects**, you’ll mostly use:

* `runserver`
* `makemigrations`
* `migrate`
* `createsuperuser`
* `shell`

---

If you want, I can give you a **“Level-wise Django command roadmap” (Beginner → Advanced → Deployment)** 🔥

















