# **Django Authorization Crash Course – 3-Day Lab Guide**

**Project Goal:**
By the end of Day 3, you will have a Django project with:

* A **custom User model**
* User registration, login/logout, and password management
* Role-based and group-based permissions
* Object-level permissions and secure views
* Optional API endpoints

---

## **Day 1 – Foundations & User Management**

**Goal:** Set up a Django project and implement a custom user model with basic CRUD functionality.

### **Steps:**

1. **Set up project and app**

```bash
django-admin startproject auth_crash_course
cd auth_crash_course
python manage.py startapp accounts
```

Add `'accounts'` to `INSTALLED_APPS`.

2. **Create a custom user model** (`accounts/models.py`)

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

Set `AUTH_USER_MODEL = 'accounts.CustomUser'` in `settings.py`.

3. **Migrate and create superuser**

```bash
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```

4. **Create basic views** to list users (`accounts/views.py`) and templates (`accounts/templates/accounts/user_list.html`).

5. **Optional:** Implement a registration form with `UserCreationForm` for the custom user.

### **Exercises:**

* Add extra fields to the custom user model (e.g., `bio`, `profile_picture`).
* Implement user registration and test creating new users.
* Display user roles in the user list.

---

## **Day 2 – Authentication & Permissions**

**Goal:** Add login/logout, password management, groups, and role-based access.

### **Steps:**

1. **Add authentication URLs** (`accounts/urls.py`)

```python
from django.contrib.auth import views as auth_views
path('login/', auth_views.LoginView.as_view(template_name='accounts/login.html'), name='login'),
path('logout/', auth_views.LogoutView.as_view(), name='logout'),
path('password_change/', auth_views.PasswordChangeView.as_view(template_name='accounts/password_change.html'), name='password_change'),
```

2. **Create login/logout templates**.

3. **Protect views** with `@login_required`:

```python
from django.contrib.auth.decorators import login_required

@login_required
def user_list(request):
    ...
```

4. **Create groups and assign permissions** in admin:

* Example: Editors → add/change users, Viewers → view only

5. **Protect views with `@permission_required`**:

```python
@permission_required('accounts.change_customuser', raise_exception=True)
def edit_user(request, user_id):
    ...
```

6. **Role-based access** using the `role` field:

```python
@login_required
def editor_page(request):
    if request.user.role != 'editor':
        return HttpResponseForbidden()
```

### **Exercises:**

* Implement password change and test it.
* Create role-based pages for editors and viewers.
* Protect pages with decorators and test login/logout flow.

---

## **Day 3 – Advanced Authorization & Security**

**Goal:** Secure the project with CBVs, mixins, object-level permissions, and security best practices.

### **Steps:**

1. **Convert views to CBVs** and use `LoginRequiredMixin` and `PermissionRequiredMixin`:

```python
from django.views.generic import ListView
from django.contrib.auth.mixins import LoginRequiredMixin

class UserListView(LoginRequiredMixin, ListView):
    ...
```

2. **Object-level permissions** (optional) with `django-guardian`:

```bash
pip install django-guardian
```

Assign permissions:

```python
from guardian.shortcuts import assign_perm
assign_perm('change_customuser', request.user, target_user)
```

3. **Role-based CBVs**

```python
from django.core.exceptions import PermissionDenied

class EditorPageView(LoginRequiredMixin, ListView):
    def dispatch(self, request, *args, **kwargs):
        if request.user.role != 'editor':
            raise PermissionDenied()
        return super().dispatch(request, *args, **kwargs)
```

4. **Security best practices**

* Password validators in `settings.py`
* HTTPS enforcement (`SECURE_SSL_REDIRECT = True`)
* Secure sessions (`SESSION_COOKIE_SECURE = True`)
* Rate limiting login attempts (e.g., `django-axes`)

5. **Optional API endpoint** with Django REST Framework:

```python
from rest_framework.views import APIView
from rest_framework.permissions import IsAuthenticated
class UserListAPI(APIView):
    permission_classes = [IsAuthenticated]
    ...
```

### **Exercises:**

* Secure all CBVs with mixins.
* Implement object-level permission so users can only edit their own profiles.
* Create role-based pages and test access.
* Apply security settings and test login/logout, password change, and access restrictions.
* Optional: Add a protected API endpoint.

---

## **Final Project Outcome**

* Custom User model with roles
* User registration, login/logout, password management
* Group- and role-based access control
* Object-level permissions for secure editing
* Secure sessions and optional API endpoints

