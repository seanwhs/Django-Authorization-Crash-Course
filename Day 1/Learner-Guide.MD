# **Day 1 Learner Guide – Foundations & User Management**

**Course:** Django Authorization Crash Course
**Day:** 1 – Foundations & User Management
**Duration:** ~4–5 hours

---

## **1. Introduction**

Welcome to Day 1! Today, you will learn the foundations of **Django authentication**, including the difference between authentication and authorization. By the end of this session, you’ll have a working Django project with a **custom user model** and basic user management functionality.

**Learning Objectives:**

* Understand **authentication vs authorization**
* Explore Django’s built-in **User model**
* Create a **Custom User model** with a `role` field
* Perform basic **CRUD operations** for users
* Manage **passwords securely**

---

## **2. Key Concepts**

### **Authentication vs Authorization**

* **Authentication:** Verifying who a user is (login, credentials)
* **Authorization:** Controlling what a user can do (permissions, roles)

**Example:**

* Authentication → “Is this user John?”
* Authorization → “Can John edit this page?”

### **Django User Model**

* Default fields: `username`, `email`, `password`, `first_name`, `last_name`
* Default permissions: `add`, `change`, `delete`, `view`
* Superuser has all permissions
* Groups allow grouping permissions for multiple users

---

## **3. Custom User Model**

**Why Use a Custom User?**

* Add fields like `role`, `bio`, `profile_picture`
* Flexibility for future features (e.g., API tokens)
* Best practice: create it **at the start of the project**

**Step 1: Create the `accounts` app**

```bash
django-admin startproject auth_crash_course
cd auth_crash_course
python manage.py startapp accounts
```

**Step 2: Define Custom User Model**

```python
from django.contrib.auth.models import AbstractUser
from django.db import models

class CustomUser(AbstractUser):
    ROLE_CHOICES = (
        ('admin', 'Admin'),
        ('editor', 'Editor'),
        ('viewer', 'Viewer'),
    )
    role = models.CharField(max_length=10, choices=ROLE_CHOICES, default='viewer')
```

**Step 3: Update `settings.py`**

```python
AUTH_USER_MODEL = 'accounts.CustomUser'
INSTALLED_APPS = [
    ...,
    'accounts',
]
```

---

## **4. Apply Migrations & Create Superuser**

```bash
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```

* Login to Django admin to verify your superuser
* Optional: Add sample users to test roles

---

## **5. Basic User CRUD**

**Step 1: Create a User List View**

```python
from django.contrib.auth import get_user_model
from django.shortcuts import render

User = get_user_model()

def user_list(request):
    users = User.objects.all()
    return render(request, 'accounts/user_list.html', {'users': users})
```

**Step 2: Create Template**

```html
<!-- accounts/templates/accounts/user_list.html -->
<h1>User List</h1>
<ul>
  {% for user in users %}
    <li>{{ user.username }} - {{ user.role }}</li>
  {% endfor %}
</ul>
```

**Step 3: Add URL**

```python
from django.urls import path
from .views import user_list

urlpatterns = [
    path('users/', user_list, name='user_list'),
]
```

---

## **6. Password Management**

* Use `set_password()` for secure passwords:

```python
user = User.objects.create(username='john')
user.set_password('securepassword123')
user.save()
```

* Never store plain-text passwords
* Django hashes passwords automatically

---

## **7. Lab Exercises**

**Mandatory Exercises:**

1. Set up Django project & `accounts` app
2. Implement **Custom User model** with `role` field
3. Apply migrations & create a superuser
4. Build a **user list view and template**
5. Test creating users programmatically with `set_password()`

**Optional Challenges:**

* Add extra fields like `bio` or `profile_picture`
* Create a simple registration form using `UserCreationForm`

---

## **8. Summary**

* Authentication vs Authorization
* Built-in Django User model
* Custom User model with roles
* CRUD operations for users
* Secure password handling

**Next:** Day 2 – Login, Logout, Password Management, and Role-Based Access

