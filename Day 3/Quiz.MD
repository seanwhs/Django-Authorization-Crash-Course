# **Day 3 Quiz – Advanced Authorization & Security**

**Instructions:** Choose the correct answer or provide the requested response. Each question is worth **1 point**.

---

### **Multiple Choice Questions**

**1. Which mixin is used in a CBV to restrict access to authenticated users?**
A) `PermissionRequiredMixin`
B) `LoginRequiredMixin` ✅
C) `UserPassesTestMixin`
D) `AuthenticatedMixin`

**Answer:** B

---

**2. Which mixin is used in a CBV to enforce permission checks?**
A) `LoginRequiredMixin`
B) `PermissionRequiredMixin` ✅
C) `UserRoleMixin`
D) `AuthenticatedMixin`

**Answer:** B

---

**3. What is the purpose of object-level permissions?**
A) To assign permissions to models globally
B) To assign permissions to individual objects or records ✅
C) To enforce password policies
D) To group users automatically

**Answer:** B

---

**4. Which third-party package allows Django to implement object-level permissions?**
A) `django-rest-framework`
B) `django-guardian` ✅
C) `django-permissions`
D) `django-groups`

**Answer:** B

---

**5. Which Django REST Framework permission class restricts API access to authenticated users only?**
A) `AllowAny`
B) `IsAuthenticated` ✅
C) `IsAdminUser`
D) `DjangoModelPermissions`

**Answer:** B

---

### **True/False Questions**

**6. You can combine `LoginRequiredMixin` and `PermissionRequiredMixin` in a CBV to enforce both authentication and authorization.**

* True ✅
* False

**Answer:** True

---

**7. Checking a user’s role in a CBV’s `dispatch()` method is a valid way to implement role-based access control.**

* True ✅
* False

**Answer:** True

---

### **Short Answer Questions**

**8. Write a snippet of a CBV that only allows users with the role `editor` to access the view.**
**Answer Example:**

```python
from django.core.exceptions import PermissionDenied
from django.views.generic import ListView
from django.contrib.auth.mixins import LoginRequiredMixin

class EditorPageView(LoginRequiredMixin, ListView):
    template_name = 'accounts/editor_page.html'

    def dispatch(self, request, *args, **kwargs):
        if request.user.role != 'editor':
            raise PermissionDenied("Access denied")
        return super().dispatch(request, *args, **kwargs)
```

---

**9. How do you assign an object-level permission to a user using `django-guardian`?**
**Answer Example:**

```python
from guardian.shortcuts import assign_perm
assign_perm('change_customuser', request.user, target_user)
```

---

**10. Name three security best practices you should apply to a Django project.**
**Answer Example:**

* Enforce strong passwords with validators
* Use HTTPS (`SECURE_SSL_REDIRECT = True`)
* Configure secure session cookies (`SESSION_COOKIE_SECURE = True`)
* Limit login attempts using packages like `django-axes`

