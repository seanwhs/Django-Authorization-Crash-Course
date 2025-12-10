# **Day 3 Lesson Plan – Advanced Authorization & Security**

**Duration:** ~4–5 hours
**Target Audience:** Beginner to intermediate Django developers

---

## **Lesson Overview**

**Goal:** Secure the Django project using **class-based view mixins**, **object-level permissions**, **role-based access**, and **security best practices**.

**Learning Objectives:**
By the end of Day 3, students will be able to:

1. Use **class-based view mixins** (`LoginRequiredMixin`, `PermissionRequiredMixin`)
2. Implement **object-level permissions** using `django-guardian`
3. Secure views based on **roles and groups**
4. Apply **security best practices**: password policies, HTTPS, sessions
5. Optionally, create **secure API endpoints** with Django REST Framework
6. Consolidate all skills into a **secure, role-aware project**

---

## **Session Breakdown**

| Time      | Topic                                       | Method               | Notes / Resources                                                                             |
| --------- | ------------------------------------------- | -------------------- | --------------------------------------------------------------------------------------------- |
| 0:00–0:15 | **Recap Day 2**                             | Lecture / Discussion | Review login/logout, groups, permissions, role-based pages                                    |
| 0:15–0:45 | **Class-Based Views & Mixins**              | Lecture + Demo       | `LoginRequiredMixin`, `PermissionRequiredMixin`, converting function-based views to CBVs      |
| 0:45–1:15 | **Object-Level Permissions**                | Lecture + Demo       | Introduce `django-guardian`, assign object-level permissions, test access                     |
| 1:15–2:00 | **Hands-On Lab: CBVs & Object Permissions** | Lab                  | Convert `user_list` and `edit_user` views to CBVs, apply object-level permissions             |
| 2:00–2:15 | **Break**                                   | —                    | 15 minutes                                                                                    |
| 2:15–3:00 | **Role-Based CBVs**                         | Lecture + Lab        | Restrict access in CBVs using `role` field, handle PermissionDenied                           |
| 3:00–3:30 | **Security Best Practices**                 | Lecture + Demo       | Password validators, HTTPS, secure sessions, login attempt limits                             |
| 3:30–4:00 | **Optional API Endpoint**                   | Lecture + Lab        | DRF APIView example with `IsAuthenticated`, token/JWT auth                                    |
| 4:00–4:30 | **Lab Exercise: Secure Project**            | Lab                  | Combine CBVs, object-level permissions, role-based pages, secure sessions, test full workflow |
| 4:30–4:50 | **Review & Q&A**                            | Discussion           | Recap CBVs, mixins, object-level permissions, security practices                              |
| 4:50–5:00 | **Homework / Assignment**                   | Assignment           | Optional: Add more roles, custom permissions, secure API endpoints                            |

---

## **Key Teaching Points**

* **CBVs with Mixins** simplify access control and reduce repeated code
* **Object-level permissions** allow per-object authorization
* **Role-based CBVs** enforce user roles in class-based views
* **Security best practices** ensure production readiness (passwords, HTTPS, sessions)
* DRF integration allows secure API endpoints

---

## **Lab Exercises**

1. **Convert Views to CBVs**

```python
from django.views.generic import ListView, DetailView
from django.contrib.auth.mixins import LoginRequiredMixin, PermissionRequiredMixin

class UserListView(LoginRequiredMixin, PermissionRequiredMixin, ListView):
    model = User
    template_name = 'accounts/user_list.html'
    permission_required = 'accounts.view_customuser'
```

2. **Object-Level Permissions**

```python
from guardian.shortcuts import assign_perm

# Assign permission to a specific user object
assign_perm('change_customuser', request.user, target_user)
```

3. **Role-Based CBVs**

```python
from django.core.exceptions import PermissionDenied

class EditorPageView(LoginRequiredMixin, ListView):
    def dispatch(self, request, *args, **kwargs):
        if request.user.role != 'editor':
            raise PermissionDenied("Access denied")
        return super().dispatch(request, *args, **kwargs)
```

4. **Apply Security Best Practices**

* Password validators: `AUTH_PASSWORD_VALIDATORS` in `settings.py`
* Secure sessions: `SESSION_COOKIE_SECURE = True`, `SESSION_EXPIRE_AT_BROWSER_CLOSE = True`
* HTTPS: `SECURE_SSL_REDIRECT = True`

5. **Optional API Endpoint**

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

---

## **Optional Challenges**

* Users can only edit their own profiles
* Test full workflow: login, password change, role-based pages, object-level permissions
* Add custom permissions and extend CBVs
* Secure multiple API endpoints

---

## **Resources**

* [Django CBV Mixins](https://docs.djangoproject.com/en/stable/topics/class-based-views/)
* [django-guardian Documentation](https://django-guardian.readthedocs.io/en/stable/)
* [Django Security Best Practices](https://docs.djangoproject.com/en/stable/topics/security/)
* [Django REST Framework Authentication](https://www.django-rest-framework.org/api-guide/authentication/)

