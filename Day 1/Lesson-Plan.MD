# **Day 1 Lesson Plan – Foundations & User Management**

**Duration:** ~4–5 hours
**Target Audience:** Beginner to intermediate Django developers

---

## **Lesson Overview**

**Goal:** Introduce Django authentication concepts and implement a custom user model with basic user management functionality.

**Learning Objectives:**
By the end of Day 1, students will be able to:

1. Distinguish **authentication** from **authorization**
2. Understand Django’s built-in **User model**
3. Create a **Custom User model** with roles
4. Perform basic **CRUD operations** on users
5. Manage **passwords securely**

---

## **Session Breakdown**

| Time      | Topic                               | Method               | Notes / Resources                                                                                |
| --------- | ----------------------------------- | -------------------- | ------------------------------------------------------------------------------------------------ |
| 0:00–0:15 | **Introduction & Course Overview**  | Lecture / Discussion | Discuss course goals, 3-day roadmap, real-world applications                                     |
| 0:15–0:45 | **Authentication vs Authorization** | Lecture + Q&A        | Define both, use examples (login vs permission control), short discussion                        |
| 0:45–1:15 | **Django User Model Overview**      | Lecture + Demo       | Built-in fields (`username`, `email`, `password`), default permissions, groups                   |
| 1:15–1:45 | **Custom User Model**               | Lecture + Code Demo  | Show `AbstractUser`, `role` field, `AUTH_USER_MODEL` in `settings.py`                            |
| 1:45–2:15 | **Migrations & Superuser**          | Hands-On Lab         | Run `makemigrations` and `migrate`, create superuser, login to admin                             |
| 2:15–2:45 | **Break**                           | —                    | 15–20 minutes                                                                                    |
| 2:45–3:30 | **Basic User CRUD Operations**      | Hands-On Lab         | Create `user_list` view, template, test in browser                                               |
| 3:30–4:00 | **Password Management**             | Lecture + Lab        | Demonstrate `set_password()`, secure password storage, test creating users programmatically      |
| 4:00–4:30 | **Optional Lab: Registration Form** | Hands-On Lab         | Build a simple registration form using `UserCreationForm`                                        |
| 4:30–4:50 | **Review & Q&A**                    | Discussion           | Recap key points, answer questions                                                               |
| 4:50–5:00 | **Homework / Exercises**            | Assignment           | Extend user model (`bio`, `profile_picture`), implement registration form, experiment with roles |

---

## **Key Teaching Points**

* Always create a custom user model at the start of a project if you plan to extend it.
* Use `set_password()` instead of storing passwords in plain text.
* Roles are a simple way to implement access control.

---

## **Lab Exercises**

1. **Create Django Project & App**

```bash
django-admin startproject auth_crash_course
cd auth_crash_course
python manage.py startapp accounts
```

2. **Implement Custom User Model**

```python
from django.contrib.auth.models import AbstractUser
from django.db import models

class CustomUser(AbstractUser):
    ROLE_CHOICES = (('admin','Admin'),('editor','Editor'),('viewer','Viewer'))
    role = models.CharField(max_length=10, choices=ROLE_CHOICES, default='viewer')
```

3. **Migrate and create superuser**

```bash
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```

4. **User List View & Template**

```python
from django.contrib.auth import get_user_model
User = get_user_model()
# Render list of users in template
```

5. **Password Handling**

```python
user.set_password('securepassword123')
user.save()
```

**Optional Challenges:**

* Add `bio` or `profile_picture` field to `CustomUser`
* Build a registration form using `UserCreationForm`

---

## **Resources**

* [Django Custom User Model Documentation](https://docs.djangoproject.com/en/stable/topics/auth/customizing/)
* [Django Authentication Overview](https://docs.djangoproject.com/en/stable/topics/auth/)
* Example project structure and template snippets

