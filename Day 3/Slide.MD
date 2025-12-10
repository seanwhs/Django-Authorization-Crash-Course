# **Slide Deck – Day 3: Advanced Authorization & Security**

---

## **Slide 1 – Title Slide**

**Title:** Django Authorization Crash Course – Day 3
**Subtitle:** Advanced Authorization & Security
**Additional:** Your Name / Date / Course Logo

---

## **Slide 2 – Learning Objectives**

By the end of Day 3, you will be able to:

1. Use **class-based view mixins** (`LoginRequiredMixin`, `PermissionRequiredMixin`)
2. Implement **object-level permissions**
3. Secure views based on **user roles and groups**
4. Apply **security best practices** for passwords, sessions, and HTTPS
5. Optionally, protect **API endpoints** using Django REST Framework
6. Consolidate all skills into a **secure, role-aware project**

---

## **Slide 3 – Class-Based View Mixins**

* **LoginRequiredMixin** → restricts access to logged-in users
* **PermissionRequiredMixin** → restricts access based on permissions

**Example – ListView:**

```python
from django.views.generic import ListView
from django.contrib.auth.mixins import LoginRequiredMixin, PermissionRequiredMixin

class UserListView(LoginRequiredMixin, PermissionRequiredMixin, ListView):
    model = User
    template_name = 'accounts/user_list.html'
    permission_required = 'accounts.view_customuser'
```

---

## **Slide 4 – Object-Level Permissions**

* Fine-grained permissions for individual objects
* Use **django-guardian**:

```bash
pip install django-guardian
```

**Example – Assign permission:**

```python
from guardian.shortcuts import assign_perm
assign_perm('change_customuser', request.user, target_user)
```

* Users can only edit objects they have permissions for

---

## **Slide 5 – Role-Based CBVs**

```python
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

## **Slide 6 – Security Best Practices**

1. **Password policies:** enforce strong passwords via validators
2. **HTTPS:** `SECURE_SSL_REDIRECT = True` in production
3. **Sessions:**

   * `SESSION_COOKIE_SECURE = True`
   * `SESSION_EXPIRE_AT_BROWSER_CLOSE = True`
4. **Limit login attempts:** use packages like `django-axes`

---

## **Slide 7 – Optional API Authentication**

* Use Django REST Framework (DRF)
* Example endpoint:

```python
from rest_framework.views import APIView
from rest_framework.permissions import IsAuthenticated
from rest_framework.response import Response

class UserListAPI(APIView):
    permission_classes = [IsAuthenticated]

    def get(self, request):
        users = User.objects.values('id', 'username', 'role')
        return Response(users)
```

* Protects endpoints using **token authentication** or **JWT**

---

## **Slide 8 – Lab Exercise – Day 3**

**Goal:** Secure the project with advanced authorization and security features

**Tasks:**

1. Convert function-based views to **CBVs** with mixins
2. Implement **object-level permissions** using `django-guardian`
3. Build **role-based pages** and test access control
4. Apply **security best practices**: HTTPS, secure sessions, password validators
5. Optional: Create a **protected API endpoint**

**Optional Challenges:**

* Users can only edit their own profiles
* Test full workflow: login, password change, role access, object permissions

---

## **Slide 9 – Summary**

* CBVs with **LoginRequiredMixin** and **PermissionRequiredMixin**
* Object-level permissions for fine-grained control
* Role-based access integrated in CBVs
* Security best practices applied
* Optional API endpoints protected

**Outcome:** Fully secure, role-aware Django application ready for real-world use

