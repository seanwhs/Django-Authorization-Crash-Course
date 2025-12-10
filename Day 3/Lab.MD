# **Day 3 Lab – Advanced Authorization & Security**

**Project Goal for Day 3:**
Enhance the project with **class-based view mixins**, **object-level permissions**, and **security best practices**. By the end of the day, your application will be fully secure, role-aware, and ready for real-world use.

---

## **Step 1: Convert Views to Class-Based Views (CBVs)**

In `accounts/views.py`:

```python
from django.views.generic import ListView, DetailView
from django.contrib.auth.mixins import LoginRequiredMixin, PermissionRequiredMixin
from django.contrib.auth import get_user_model

User = get_user_model()

class UserListView(LoginRequiredMixin, ListView):
    model = User
    template_name = 'accounts/user_list.html'
    context_object_name = 'users'

class UserDetailView(LoginRequiredMixin, PermissionRequiredMixin, DetailView):
    model = User
    template_name = 'accounts/user_detail.html'
    context_object_name = 'user'
    permission_required = 'accounts.view_customuser'
```

Update `urls.py`:

```python
from django.urls import path
from .views import UserListView, UserDetailView

urlpatterns = [
    path('users/', UserListView.as_view(), name='user_list'),
    path('users/<int:pk>/', UserDetailView.as_view(), name='user_detail'),
]
```

---

## **Step 2: Implement Object-Level Permissions (Optional)**

For fine-grained control, use `django-guardian`:

```bash
pip install django-guardian
```

In `settings.py`:

```python
INSTALLED_APPS += ['guardian']
AUTHENTICATION_BACKENDS = (
    'django.contrib.auth.backends.ModelBackend', 
    'guardian.backends.ObjectPermissionBackend',
)
```

Example usage in views:

```python
from guardian.shortcuts import assign_perm

# Assign object-level permission
assign_perm('change_customuser', request.user, target_user)
```

---

## **Step 3: Secure Views with Role Checks**

Even with CBVs, you can enforce role-based access:

```python
from django.core.exceptions import PermissionDenied

class EditorPageView(LoginRequiredMixin, ListView):
    template_name = 'accounts/editor_page.html'

    def dispatch(self, request, *args, **kwargs):
        if request.user.role != 'editor':
            raise PermissionDenied("You are not allowed to access this page.")
        return super().dispatch(request, *args, **kwargs)
```

---

## **Step 4: Security Best Practices**

1. **Password policies:** Ensure strong passwords using Django validators.
2. **HTTPS:** Set `SECURE_SSL_REDIRECT = True` in production.
3. **Sessions:** Set `SESSION_COOKIE_SECURE = True` and `SESSION_EXPIRE_AT_BROWSER_CLOSE = True`.
4. **Limit login attempts:** Use `django-axes` or a custom solution to prevent brute-force attacks.

---

## **Step 5: Optional API Authentication**

If you’re using Django REST Framework (DRF):

1. Install DRF: `pip install djangorestframework`
2. Create a simple API endpoint:

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.permissions import IsAuthenticated

class UserListAPI(APIView):
    permission_classes = [IsAuthenticated]

    def get(self, request):
        users = User.objects.values('id', 'username', 'role')
        return Response(users)
```

3. Secure with **TokenAuthentication** or **JWT**.

---

## **Step 6: Final Project Exercises**

1. Protect all CBVs with `LoginRequiredMixin` and `PermissionRequiredMixin`.
2. Implement an **object-level permission system** where users can only edit their own profile.
3. Add a **role-based page** for editors or admins.
4. Apply **security settings**: secure sessions, HTTPS, password validators.
5. Optional: Create a **protected API endpoint** with DRF.
6. Test the full workflow:

   * User login/logout
   * Role-based access to pages
   * Password change
   * Object-level editing

---

✅ **Day 3 Outcome:**

* All views are secured with CBVs and mixins.
* Object-level permissions restrict editing to authorized users.
* Security best practices are applied for passwords, sessions, and HTTPS.
* Optional API endpoints are protected with token-based authentication.

