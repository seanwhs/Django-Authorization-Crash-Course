# **Day 1 Lab – Foundations & User Management**

**Project Goal for Day 1:**
Create a Django project with a **custom User model** and basic user management features. By the end of the day, users should be able to register, view a list of users, and have role-based fields attached to them.

---

## **Step 1: Set Up the Project**

1. Create a new Django project:

```bash
django-admin startproject auth_crash_course
cd auth_crash_course
```

2. Create a new app for accounts:

```bash
python manage.py startapp accounts
```

3. Add the app to `INSTALLED_APPS` in `settings.py`:

```python
INSTALLED_APPS = [
    ...
    'accounts',
]
```

---

## **Step 2: Create a Custom User Model**

In `accounts/models.py`:

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

    def __str__(self):
        return self.username
```

Update `settings.py`:

```python
AUTH_USER_MODEL = 'accounts.CustomUser'
```

---

## **Step 3: Apply Migrations**

```bash
python manage.py makemigrations
python manage.py migrate
```

---

## **Step 4: Create Superuser**

```bash
python manage.py createsuperuser
```

Test login at `/admin` to ensure the custom user model works.

---

## **Step 5: Basic Views for Users**

Create `accounts/views.py`:

```python
from django.contrib.auth import get_user_model
from django.shortcuts import render

User = get_user_model()

def user_list(request):
    users = User.objects.all()
    return render(request, 'accounts/user_list.html', {'users': users})
```

Create `accounts/urls.py`:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('users/', views.user_list, name='user_list'),
]
```

Include in `project urls.py`:

```python
from django.urls import include, path

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('accounts.urls')),
]
```

---

## **Step 6: Templates**

Create `accounts/templates/accounts/user_list.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>User List</title>
</head>
<body>
    <h1>Users</h1>
    <ul>
        {% for user in users %}
            <li>{{ user.username }} - {{ user.role }}</li>
        {% endfor %}
    </ul>
</body>
</html>
```

---

## **Step 7: Optional – User Registration Form**

You can create a simple registration form using `forms.py`:

```python
from django import forms
from django.contrib.auth.forms import UserCreationForm
from .models import CustomUser

class CustomUserCreationForm(UserCreationForm):
    class Meta:
        model = CustomUser
        fields = ('username', 'email', 'role')
```

Create a registration view and template as homework.

---

## **Step 8: Exercises**

1. Add **more fields** to your custom user model, like `bio` or `profile_picture`.
2. Implement a **user registration form** and test creating new users.
3. Display **user roles** in the user list.
4. Experiment with `set_password()` programmatically to create new users with secure passwords.

---

✅ **Day 1 Outcome:**

* Django project running
* Custom User model implemented
* Superuser created
* User list page showing username and role
* Foundation ready for authentication and permissions on Day 2


