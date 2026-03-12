Here is a **structured table of the most important Django commands from scratch**. This covers the **complete development workflow used in Django projects**. 🚀

---

# 1️⃣ Django Project Creation Commands

| Command                                  | Purpose                      | Example                               |
| ---------------------------------------- | ---------------------------- | ------------------------------------- |
| `django-admin startproject project_name` | Create a new Django project  | `django-admin startproject myproject` |
| `cd project_name`                        | Move into the project folder | `cd myproject`                        |
| `python manage.py startapp app_name`     | Create a Django app          | `python manage.py startapp blog`      |

---

# 2️⃣ Server Commands

| Command                                   | Purpose                   | Example                                   |
| ----------------------------------------- | ------------------------- | ----------------------------------------- |
| `python manage.py runserver`              | Start development server  | `python manage.py runserver`              |
| `python manage.py runserver 8001`         | Run server on custom port | `python manage.py runserver 8001`         |
| `python manage.py runserver 0.0.0.0:8000` | Allow external access     | `python manage.py runserver 0.0.0.0:8000` |

---

# 3️⃣ Database Commands

| Command                                                 | Purpose                   |
| ------------------------------------------------------- | ------------------------- |
| `python manage.py migrate`                              | Apply database migrations |
| `python manage.py makemigrations`                       | Create migration files    |
| `python manage.py sqlmigrate app_name migration_number` | Show SQL for a migration  |
| `python manage.py showmigrations`                       | Show migration status     |
| `python manage.py dbshell`                              | Open database shell       |

Example:

```bash
python manage.py makemigrations
python manage.py migrate
```

---

# 4️⃣ Admin Commands

| Command                                    | Purpose              |
| ------------------------------------------ | -------------------- |
| `python manage.py createsuperuser`         | Create admin user    |
| `python manage.py changepassword username` | Change user password |

Example:

```bash
python manage.py createsuperuser
```

---

# 5️⃣ App Management Commands

| Command                              | Purpose                  |
| ------------------------------------ | ------------------------ |
| `python manage.py startapp app_name` | Create new app           |
| `python manage.py check`             | Check project for issues |

---

# 6️⃣ Development Utility Commands

| Command                         | Purpose                            |
| ------------------------------- | ---------------------------------- |
| `python manage.py shell`        | Open Django Python shell           |
| `python manage.py shell_plus`   | Enhanced shell (django-extensions) |
| `python manage.py diffsettings` | Show modified settings             |
| `python manage.py help`         | List all commands                  |

---

# 7️⃣ Static Files Commands

| Command                                 | Purpose                             |
| --------------------------------------- | ----------------------------------- |
| `python manage.py collectstatic`        | Collect static files for deployment |
| `python manage.py findstatic file_name` | Find static file location           |

---

# 8️⃣ Testing Commands

| Command                          | Purpose                    |
| -------------------------------- | -------------------------- |
| `python manage.py test`          | Run tests                  |
| `python manage.py test app_name` | Run tests for specific app |

Example:

```bash
python manage.py test blog
```

---

# 9️⃣ Database Reset Commands

| Command                     | Purpose                            |
| --------------------------- | ---------------------------------- |
| `python manage.py flush`    | Remove all data from database      |
| `python manage.py reset_db` | Reset database (django-extensions) |

---

# 🔟 Deployment Commands

| Command                           | Purpose                             |
| --------------------------------- | ----------------------------------- |
| `python manage.py collectstatic`  | Prepare static files for production |
| `python manage.py check --deploy` | Check deployment settings           |

---

# 1️⃣1️⃣ Migration Workflow Commands

Typical workflow:

| Step             | Command                           |
| ---------------- | --------------------------------- |
| Create model     | edit `models.py`                  |
| Create migration | `python manage.py makemigrations` |
| Apply migration  | `python manage.py migrate`        |

---

# 1️⃣2️⃣ Django Project Lifecycle Commands

Complete development cycle:

| Step             | Command                                  |
| ---------------- | ---------------------------------------- |
| Create project   | `django-admin startproject project_name` |
| Create app       | `python manage.py startapp app_name`     |
| Make migrations  | `python manage.py makemigrations`        |
| Apply migrations | `python manage.py migrate`               |
| Create admin     | `python manage.py createsuperuser`       |
| Run server       | `python manage.py runserver`             |

---

# 1️⃣3️⃣ Django Help Command (Very Useful)

List all Django commands:

```bash
python manage.py help
```

Example output:

```text
Available commands:

[auth]
    changepassword
    createsuperuser

[django]
    check
    migrate
    runserver
    shell
    startapp
```

---

# 🧠 Most Important Commands (Top 10)

| Command                            | Importance |
| ---------------------------------- | ---------- |
| `django-admin startproject`        | ⭐⭐⭐⭐⭐      |
| `python manage.py startapp`        | ⭐⭐⭐⭐⭐      |
| `python manage.py runserver`       | ⭐⭐⭐⭐⭐      |
| `python manage.py makemigrations`  | ⭐⭐⭐⭐⭐      |
| `python manage.py migrate`         | ⭐⭐⭐⭐⭐      |
| `python manage.py createsuperuser` | ⭐⭐⭐⭐⭐      |
| `python manage.py shell`           | ⭐⭐⭐⭐       |
| `python manage.py collectstatic`   | ⭐⭐⭐⭐       |
| `python manage.py test`            | ⭐⭐⭐        |
| `python manage.py check`           | ⭐⭐⭐        |

---

✅ Since you are building **Django ML projects (Arrhythmia detection + 3D heart visualization)**, the **most used commands for you will be:**

```bash
python manage.py runserver
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
python manage.py shell
```

---
































