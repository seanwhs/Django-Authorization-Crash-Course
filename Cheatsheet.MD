# ✅ DJANGO AUTHORIZATION – MASTER CHEATSHEET

---

## 🔐 1. AUTHENTICATION vs AUTHORIZATION (CORE THEORY)

| Concept        | Meaning          | Django Tools                      |
| -------------- | ---------------- | --------------------------------- |
| Authentication | WHO the user is  | `authenticate()`, `login()`       |
| Authorization  | WHAT user can do | `has_perm()`, Groups, Permissions |

✅ Rule: **AuthN → AuthZ → Access**

---

## 👤 2. DEFAULT USER MODEL

```python
from django.contrib.auth.models import User
```

Core Fields:

* username, password (hashed)
* email, first_name, last_name
* is_staff, is_superuser, is_active

DB Table: `auth_user`

---

## 🏗️ 3. CUSTOM USER MODEL (MANDATORY KNOWLEDGE)

### ✅ Using `AbstractUser` (BEST CHOICE)

```python
class CustomUser(AbstractUser):
    role = models.CharField(max_length=20)
    phone = models.CharField(max_length=15)
```

```python
AUTH_USER_MODEL = "accounts.CustomUser"   # settings.py
```

✅ Use when extending default user

---

### ✅ Using `AbstractBaseUser` (ADVANCED ONLY)

* You build everything manually
* Requires custom manager + admin

---

## 👥 4. GROUPS = ROLES

| Group   | Meaning         |
| ------- | --------------- |
| Admins  | Full Access     |
| Editors | Create / Update |
| Viewers | Read Only       |

```python
from django.contrib.auth.models import Group

editors = Group.objects.get(name="Editors")
user.groups.add(editors)
```

---

## 🔑 5. PERMISSIONS SYSTEM

Every Model Gets:

```
add_model
change_model
delete_model
view_model
```

Check:

```python
request.user.has_perm("blog.add_post")
```

### ✅ Custom Permission

```python
class Report(models.Model):
    class Meta:
        permissions = [
            ("approve_report", "Can approve report")
        ]
```

---

## 🧭 6. FUNCTION-BASED VIEW SECURITY

### ✅ Login Required

```python
@login_required
```

---

### ✅ Permission Required

```python
@permission_required("blog.add_post")
```

---

### ✅ Group Restriction

```python
request.user.groups.filter(name="Editors").exists()
```

---

## 🧱 7. CLASS-BASED VIEW SECURITY

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

### ✅ Object-Level Check (UserPassesTestMixin)

```python
class PostUpdateView(UserPassesTestMixin, UpdateView):
    def test_func(self):
        return self.get_object().author == self.request.user
```

---

## 🎯 8. TEMPLATE AUTHORIZATION

```html
{% if user.is_authenticated %}
```

```html
{% if perms.blog.delete_post %}
```

---

## 🔐 9. PASSWORD SECURITY

Enable Validators:

```python
AUTH_PASSWORD_VALIDATORS = [...]
```

Never store raw passwords ❌
Always:

```python
user.set_password("1234")
```

---

## 🔁 10. LOGIN / LOGOUT VIEWS

```python
from django.contrib.auth.views import LoginView, LogoutView
```

```python
LOGIN_REDIRECT_URL = "/dashboard/"
LOGOUT_REDIRECT_URL = "/login/"
```

---

## 🧬 11. OBJECT-LEVEL PERMISSIONS

| Method              | Use               |
| ------------------- | ----------------- |
| Filter by owner     | Simple cases      |
| UserPassesTestMixin | Web apps          |
| django-guardian     | True object perms |

---

## 🧰 12. MIDDLEWARE AUTHORIZATION

Use when:

* Blocking IP addresses
* Restricting routes based on role
* Forcing logout

---

## 🔒 13. ENTERPRISE SECURITY SETTINGS

```python
DEBUG = False
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
SECURE_SSL_REDIRECT = True
```

---

## 🌐 14. API AUTHENTICATION (DRF)

| Method      | Best For      |
| ----------- | ------------- |
| SessionAuth | Web           |
| TokenAuth   | Mobile        |
| JWT         | Microservices |

---

## ✅ 15. COMPLETE AUTH FLOW (END-TO-END)

1️⃣ Register User
2️⃣ Hash Password
3️⃣ Assign Group
4️⃣ Check Permission
5️⃣ Grant Access
6️⃣ Audit Security

---

## ✅ 16. INTERVIEW POWER Q&A

**Q:** Difference between permission & group?
✅ Permission = single action
✅ Group = collection of permissions

---

**Q:** Why use `AbstractUser`?
✅ To extend default user safely with minimal risk

---

**Q:** Best way to secure object-level edits?
✅ `UserPassesTestMixin` or `django-guardian`

---

## ✅ 17. DAILY DEVELOPER COMMANDS

```
python manage.py createsuperuser
python manage.py makemigrations
python manage.py migrate
```

