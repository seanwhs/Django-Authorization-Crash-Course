# **Slide Deck – Day 1: Foundations & User Management**

---

## **Slide 1 – Title Slide**

**Title:** Django Authorization Crash Course – Day 1
**Subtitle:** Foundations & User Management
**Additional:** Your Name / Date / Course Logo

---

## **Slide 2 – Learning Objectives**

By the end of Day 1, you will be able to:

1. Understand **Authentication vs Authorization**
2. Describe Django’s built-in **User model**
3. Implement a **Custom User model**
4. Perform basic **CRUD operations** for users
5. Manage **passwords securely**
6. Lay the foundation for permissions and role-based access

---

## **Slide 3 – Authentication vs Authorization**

| Concept            | Definition                                          |
| ------------------ | --------------------------------------------------- |
| **Authentication** | Verifying who a user is (login, credentials)        |
| **Authorization**  | Controlling what a user can do (permissions, roles) |

**Example:**

* Authentication: User logs in with username/password
* Authorization: Only editors can edit articles

---

## **Slide 4 – Django User Model Overview**

* Built-in `User` model with fields:

  * `username`, `email`, `password`, `first_name`, `last_name`
* Default permissions:

  * `add`, `change`, `delete`, `view`
* Groups allow role-based access
* Superuser has all permissions

---

## **Slide 5 – Why a Custom User Model?**

* Add extra fields like:

  * `role` (admin/editor/viewer)
  * `profile_picture`
  * `bio`
* Flexibility for future features (e.g., API tokens)
* Best practice: **create custom user at the start of the project**

---

## **Slide 6 – Creating a Custom User Model**

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

**settings.py**

```python
AUTH_USER_MODEL = 'accounts.CustomUser'
```

---

## **Slide 7 – Apply Migrations & Create Superuser**

```bash
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```

* Verify in admin interface
* Test login functionality

---

## **Slide 8 – Basic User CRUD**

**List Users View:**

```python
from django.contrib.auth import get_user_model
from django.shortcuts import render

User = get_user_model()

def user_list(request):
    users = User.objects.all()
    return render(request, 'accounts/user_list.html', {'users': users})
```

**Template:**

```html
<ul>
  {% for user in users %}
    <li>{{ user.username }} - {{ user.role }}</li>
  {% endfor %}
</ul>
```

---

## **Slide 9 – Password Management**

* Use `set_password()` for secure password handling:

```python
user = User.objects.create(username='john')
user.set_password('securepassword123')
user.save()
```

* Never store plain text passwords
* Django handles hashing automatically

---

## **Slide 10 – Lab Exercise – Day 1**

**Goal:** Build a basic user management system with a custom user model

**Tasks:**

1. Create Django project & `accounts` app
2. Implement **Custom User model** with `role` field
3. Run migrations & create superuser
4. Build a **user list view** and template
5. Test creating users programmatically with `set_password()`

**Optional Challenges:**

* Add `bio` or `profile_picture` to user model
* Create a simple registration form

---

## **Slide 11 – Summary**

* Authentication vs Authorization
* Django’s built-in User model
* Custom User model: fields and roles
* CRUD operations for users
* Secure password handling

**Next:** Day 2 – Login, Logout, Password Management, and Role-Based Access

---

