# **Day 3 Trainer Guide – Advanced Authorization & Security**

**Course:** Django Authorization Crash Course
**Day:** 3 – Advanced Authorization & Security
**Duration:** ~4–5 hours

---

## **1. Learning Objectives**

By the end of Day 3, learners should be able to:

1. Use **class-based view mixins** (`LoginRequiredMixin`, `PermissionRequiredMixin`)
2. Implement **object-level permissions** using `django-guardian`
3. Secure views based on **roles and groups**
4. Apply **security best practices** (passwords, HTTPS, sessions)
5. Optionally, create **secure API endpoints** using Django REST Framework
6. Consolidate all skills into a fully secure, role-aware project

---

## **2. Session Flow & Timing**

| Time      | Topic                                       | Trainer Notes / Tips                                                                                                        |
| --------- | ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| 0:00–0:15 | **Recap Day 2**                             | Review login/logout, groups, role-based pages, and `@permission_required`. Ask learners about challenges from Day 2 labs.   |
| 0:15–0:45 | **Class-Based Views & Mixins**              | Introduce `LoginRequiredMixin` and `PermissionRequiredMixin`. Demonstrate converting a function-based view to CBV.          |
| 0:45–1:15 | **Object-Level Permissions**                | Introduce `django-guardian`. Show how to assign object permissions and check them in views. Emphasize fine-grained control. |
| 1:15–2:00 | **Hands-On Lab: CBVs & Object Permissions** | Guide learners to convert `user_list` and `edit_user` views to CBVs with object-level permissions.                          |
| 2:00–2:15 | **Break**                                   | 15 minutes                                                                                                                  |
| 2:15–3:00 | **Role-Based CBVs**                         | Demonstrate role checks in CBVs using `dispatch()` and raising `PermissionDenied`. Learners implement editor/viewer pages.  |
| 3:00–3:30 | **Security Best Practices**                 | Discuss password validators, HTTPS, session settings, limiting login attempts. Highlight production readiness.              |
| 3:30–4:00 | **Optional API Endpoint**                   | Demonstrate DRF APIView with `IsAuthenticated` permission. Optional token/JWT authentication.                               |
| 4:00–4:30 | **Lab Exercise: Secure Project**            | Learners consolidate CBVs, object permissions, role-based pages, and security best practices into the project.              |
| 4:30–4:50 | **Review & Q&A**                            | Recap CBVs, mixins, object-level permissions, role-based access, and security.                                              |
| 4:50–5:00 | **Homework / Assignment**                   | Optional: Extend object-level permissions, add custom permissions, or secure API endpoints.                                 |

---

## **3. Trainer Tips**

* Stress **CBVs with mixins** for cleaner, maintainable code.
* Highlight **object-level permissions** as a way to control access per resource.
* Demonstrate **role-based CBVs** to combine authentication, permissions, and roles.
* Emphasize **security best practices**—password policies, HTTPS, session handling.
* Encourage learners to **test full workflows**: login, password change, role access, object-level permissions.
* Optional: Show API endpoints only if learners are comfortable with DRF basics.

---

## **4. Suggested Instructor Code Snippets**

* **CBV with PermissionRequiredMixin**

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

* **Object-Level Permission Assignment**

```python
from guardian.shortcuts import assign_perm

assign_perm('change_customuser', request.user, target_user)
```

* **Role-Based CBV**

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

* **DRF Protected API Example**

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

---

## **5. Learning Checks**

* Can learners convert function-based views to CBVs with mixins?
* Can they assign and enforce object-level permissions?
* Can learners implement role-based access in CBVs?
* Are security best practices applied (password validators, HTTPS, sessions)?
* Can learners test secure API endpoints?

---

## **6. Resources for Trainer**

* [Django Class-Based Views](https://docs.djangoproject.com/en/stable/topics/class-based-views/)
* [django-guardian Documentation](https://django-guardian.readthedocs.io/en/stable/)
* [Django Security Best Practices](https://docs.djangoproject.com/en/stable/topics/security/)
* [Django REST Framework Authentication](https://www.django-rest-framework.org/api-guide/authentication/)

