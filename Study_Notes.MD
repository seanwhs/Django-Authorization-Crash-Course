# ✅ **Django Authorization in 3 Days Crash Course**

*(Trainer-ready, enterprise-grade notes with deep explanations, best practices, and examples)*

These notes are written so they can be used as:

* ✅ Student handbook
* ✅ Trainer slides reference
* ✅ Self-study material
* ✅ Post-course revision guide

---

# 🗓️ **DAY 1: Foundations & User Management**

> *Goal: Understand how identity works in Django and how users are created, stored, and secured.*

---

## ✅ 1. Authentication vs Authorization (CRITICAL CONCEPT)

### 🔹 Authentication = WHO you are

* Verifies the identity of the user
* Example:

  * Username + Password
  * Email + OTP
  * Token-based login

**In Django:**

* Managed using:

  * `django.contrib.auth`
  * `authenticate()`
  * `login()`

✅ Example:

```python
from django.contrib.auth import authenticate, login

user = authenticate(username='admin', password='1234')
if user:
    login(request, user)
```

---

### 🔹 Authorization = WHAT you are allowed to do

* Determines access rights after authentication
* Example:

  * Can user access admin panel?
  * Can user delete records?
  * Can user edit someone else's post?

**In Django:**

* Roles → implemented via Groups
* Permissions → add, change, delete, view

✅ Example:

```python
request.user.has_perm("blog.delete_post")
```

---

### ✅ Key Exam Difference:

| Feature | Authentication | Authorization  |
| ------- | -------------- | -------------- |
| Purpose | Identity       | Access Control |
| Happens | First          | After login    |
| Example | Login          | Edit/Delete    |

---

## ✅ 2. Django Default User Model

Django ships with:

```python
django.contrib.auth.models.User
```

### 🔹 Default Fields:

* username
* password (hashed)
* email
* first_name
* last_name
* is_staff
* is_superuser
* is_active
* last_login
* date_joined

✅ Stored in:

```sql
auth_user
```

---

## ✅ 3. Why Custom User Model is Important

### ❌ Problems with Default User:

* Username is mandatory
* Cannot replace with email easily
* Hard to add business-specific fields

---

### ✅ Use Custom User When:

* You want email login instead of username
* You need roles (admin, editor, member)
* You need phone numbers, departments, etc.

---

## ✅ 4. Custom User Model Options

### ✅ Option 1: `AbstractUser` (Recommended for Most Use Cases)

Extends full Django User with customization

✅ Example:

```python
from django.contrib.auth.models import AbstractUser
from django.db import models

class CustomUser(AbstractUser):
    role = models.CharField(max_length=20, choices=[
        ("ADMIN", "Admin"),
        ("EDITOR", "Editor"),
        ("VIEWER", "Viewer"),
    ])
    phone_number = models.CharField(max_length=15)
```

✅ Best for:

* 90% of business applications
* When you want username + password + extra fields

---

### ✅ Option 2: `AbstractBaseUser` (Advanced & Risky)

* Only provides password & authentication logic
* You must implement:

  * username field
  * email
  * manager
  * permissions
  * admin support

✅ Only use if:

* You fully understand Django internals
* You want email-only login with no username

---

## ✅ 5. Activating a Custom User Model

Inside `settings.py`:

```python
AUTH_USER_MODEL = "accounts.CustomUser"
```

⚠️ MUST be set before first migration
⚠️ Cannot change after db tables exist without data migration

---

## ✅ 6. Creating Users Programmatically

### ✅ Create Superuser:

```bash
python manage.py createsuperuser
```

---

### ✅ Create User in Code:

```python
from django.contrib.auth import get_user_model

User = get_user_model()
user = User.objects.create_user(
    username="john",
    password="pass1234",
    role="EDITOR"
)
```

---

## ✅ 7. Password Management & Validators

Django stores:
✅ Hashed passwords only
❌ Never stores raw passwords

---

### ✅ Default Password Validators:

* Similarity to username
* Minimum length
* Common passwords
* Numeric-only passwords

Enable in `settings.py`:

```python
AUTH_PASSWORD_VALIDATORS = [
    {"NAME": "django.contrib.auth.password_validation.UserAttributeSimilarityValidator"},
    {"NAME": "django.contrib.auth.password_validation.MinimumLengthValidator"},
    {"NAME": "django.contrib.auth.password_validation.CommonPasswordValidator"},
    {"NAME": "django.contrib.auth.password_validation.NumericPasswordValidator"},
]
```

---

## ✅ 8. User Registration Flow (Full Architecture)

Steps:

1. Show registration form
2. Validate input
3. Create user
4. Hash password
5. Auto login OR redirect to login

✅ Example:

```python
from django.contrib.auth.forms import UserCreationForm

class RegisterForm(UserCreationForm):
    class Meta:
        model = CustomUser
        fields = ["username", "role", "password1", "password2"]
```

---

## ✅ 9. Profile Editing

Two models:

* User → authentication
* Profile → additional info

✅ Relation:

```python
user = models.OneToOneField(settings.AUTH_USER_MODEL)
```

---

# 🗓️ **DAY 2: Authentication & Permissions**

> *Goal: Control who can access what using permissions & roles.*

---

## ✅ 1. Login & Logout Views

### ✅ Login:

```python
from django.contrib.auth.views import LoginView
```

### ✅ Logout:

```python
from django.contrib.auth.views import LogoutView
```

---

## ✅ 2. Redirect After Login

In `settings.py`:

```python
LOGIN_REDIRECT_URL = "/dashboard/"
LOGOUT_REDIRECT_URL = "/login/"
```

---

## ✅ 3. Django Model Permissions

For every model Django auto-creates:

| Permission | Meaning       |
| ---------- | ------------- |
| add        | Insert record |
| change     | Edit record   |
| delete     | Remove record |
| view       | Read/view     |

Shown in:

```bash
python manage.py migrate
```

---

## ✅ 4. Custom Permissions

Inside model:

```python
class Report(models.Model):
    class Meta:
        permissions = [
            ("approve_report", "Can approve report"),
        ]
```

✅ Use:

```python
user.has_perm("app.approve_report")
```

---

## ✅ 5. Groups (Django Roles)

Groups = Role Containers

### ✅ Example:

| Group   | Permissions |
| ------- | ----------- |
| Editors | add, change |
| Viewers | view only   |
| Admins  | full        |

✅ Assign user:

```python
editors = Group.objects.get(name="Editors")
user.groups.add(editors)
```

---

## ✅ 6. View Protection

### ✅ Login Required:

```python
@login_required
```

---

### ✅ Permission Required:

```python
@permission_required("blog.add_post")
```

---

## ✅ 7. Template Authorization

```html
{% if perms.blog.delete_post %}
   <button>Delete</button>
{% endif %}
```

---

# 🗓️ **DAY 3: Advanced Authorization & Security**

> *Goal: Enforce enterprise-grade security and object-level control.*

---

## ✅ 1. Class-Based View Security

### ✅ LoginRequiredMixin

```python
class DashboardView(LoginRequiredMixin, View):
```

---

### ✅ PermissionRequiredMixin

```python
class PostCreateView(PermissionRequiredMixin, CreateView):
    permission_required = "blog.add_post"
```

---

## ✅ 2. Object-Level Permissions

Example Rule:

> Only the author can edit the post

✅ Using Query Filtering:

```python
Post.objects.filter(author=request.user)
```

✅ Using Mixin:

```python
class PostUpdateView(UserPassesTestMixin, UpdateView):
    def test_func(self):
        return self.get_object().author == self.request.user
```

---

## ✅ 3. Middleware for Access Control

Middleware intercepts every request:

Use cases:

* Block users by IP
* Restrict admin routes by role
* Force logout suspicious sessions

---

## ✅ 4. Security Best Practices (ENTERPRISE LEVEL)

| Practice               | Why                      |
| ---------------------- | ------------------------ |
| HTTPS                  | Prevent credential theft |
| Secure Cookies         | Prevent session hijack   |
| CSRF Protection        | Prevent form attacks     |
| Disable Debug          | Prevent data leaks       |
| Strong Password Policy | Prevent brute-force      |
| Session Expiry         | Prevent stale logins     |

---

## ✅ 5. DRF Authentication (Optional API Section)

| Type        | Use Case      |
| ----------- | ------------- |
| TokenAuth   | Mobile apps   |
| JWT         | Microservices |
| SessionAuth | Browser APIs  |

---

# ✅ FINAL MINI PROJECT ARCHITECTURE

✅ Registration/Login
✅ Custom User with Role
✅ Groups & Permissions
✅ Protected Views
✅ Object-Level Security
✅ Optional JWT API

---

# ✅ WHAT YOU NOW MASTER

✔ Authentication & Authorization
✔ Custom User Models
✔ Role-Based Access
✔ Django Permissions
✔ Class-Based Security
✔ Object-Level Permissions
✔ Enterprise Security Standards

