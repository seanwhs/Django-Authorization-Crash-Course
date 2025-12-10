# **Day 3 Learner Guide – Advanced Authorization & Security**

**Course:** Django Authorization Crash Course
**Day:** 3 – Advanced Authorization & Security
**Duration:** ~4–5 hours

---

## **1. Introduction**

Welcome to Day 3! Today, you will learn how to secure your Django project using **class-based view mixins**, **object-level permissions**, **role-based access**, and **security best practices**. By the end of the session, your project will be **fully secure and role-aware**.

**Learning Objectives:**

* Use CBV mixins (`LoginRequiredMixin`, `PermissionRequiredMixin`)
* Implement **object-level permissions** with `django-guardian`
* Secure views based on **roles and groups**
* Apply **security best practices**: passwords, HTTPS, sessions
* Optionally, secure **API endpoints** with Django REST Framework
* Consolidate all skills into a secure project

---

## **2. Class-Based View Mixins**

* **LoginRequiredMixin** → restricts access to authenticated users
* **PermissionRequiredMixin** → restricts access based on permissions

**Example – ListView:**

```python
from django.views.generic import ListView
from django.contrib.auth.mixins import LoginRequiredMixin, PermissionRequiredMixin
from django.contrib.auth import get_user_model

User = get_user_model()

class UserListView(LoginRequiredMixin, PermissionRequiredMixin, ListView):
    model = User
    template_name = 'accounts/user_list.html'
    permission_required = 'accounts.view_customuser'
```

* CBVs simplify access control and reduce repetitive code

---

## **3. Object-Level Permissions**

* Fine-grained control for individual objects
* Use **django-guardian**:

```bash
pip install django-guardian
```

**Assign object permission:**

```python
from guardian.shortcuts import assign_perm
assign_perm('change_customuser', request.user, target_user)
```

* Users can only edit objects they have permissions for

---

## **4. Role-Based CBVs**

**Example – Editor-Only Page:**

```python
from django.views.generic import ListView
from django.contrib.auth.mixins import LoginRequiredMixin
from django.core.exceptions import PermissionDenied

class EditorPageView(LoginRequiredMixin, ListView):
    template_name = 'accounts/editor_page.html'

    def dispatch(self, request, *args, **kwargs):
        if request.user.role != 'editor':
            raise PermissionDenied("Access denied")
        return super().dispatch(request, *args, **kwargs)
```

* Combines **login required** and **role check** in a single CBV

---

## **5. Security Best Practices**

1. **Password Policies** – enforce strong passwords with validators
2. **HTTPS** – `SECURE_SSL_REDIRECT = True` in production
3. **Sessions** –

   * `SESSION_COOKIE_SECURE = True`
   * `SESSION_EXPIRE_AT_BROWSER_CLOSE = True`
4. **Limit Login Attempts** – use packages like `django-axes`

---

## **6. Optional API Endpoint**

* Use Django REST Framework (DRF) for protected APIs

**Example – Protected APIView:**

```python
from rest_framework.views import APIView
from rest_framework.permissions import IsAuthenticated
from rest_framework.response import Response
from django.contrib.auth import get_user_model

User = get_user_model()

class UserListAPI(APIView):
    permission_classes = [IsAuthenticated]

    def get(self, request):
        users = User.objects.values('id', 'username', 'role')
        return Response(users)
```

* Protects endpoints using **token authentication** or **JWT**

---

## **7. Lab Exercises**

**Mandatory Exercises:**

1. Convert function-based views to CBVs with mixins
2. Implement object-level permissions using `django-guardian`
3. Build role-based pages and test access control
4. Apply security best practices (HTTPS, sessions, password validators)
5. Test full workflow: login, password change, role access, object permissions

**Optional Challenges:**

* Users can only edit their own profiles
* Add custom permissions and extend CBVs
* Create secure API endpoints using DRF

---

## **8. Summary**

* CBVs with `LoginRequiredMixin` and `PermissionRequiredMixin` simplify access control
* Object-level permissions allow fine-grained authorization
* Role-based access control ensures proper authorization in CBVs
* Security best practices make your project production-ready
* Optional API endpoints can be secured with DRF

**Next Steps:** Your Django project is now secure, role-aware, and ready for real-world use. You can expand it further with custom permissions, APIs, or multi-level roles.

