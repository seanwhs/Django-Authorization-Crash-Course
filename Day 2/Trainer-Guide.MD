# **Day 2 Trainer Guide – Authentication & Permissions**

**Course:** Django Authorization Crash Course
**Day:** 2 – Authentication & Permissions
**Duration:** ~4–5 hours

---

## **1. Learning Objectives**

By the end of Day 2, learners should be able to:

1. Implement **login and logout** functionality
2. Enable **password change and reset** flows
3. Protect views using **`@login_required`** and **`@permission_required`**
4. Create **groups** and assign permissions
5. Implement **role-based access control** in views

---

## **2. Session Flow & Timing**

| Time      | Topic                              | Trainer Notes / Tips                                                                                                                       |
| --------- | ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| 0:00–0:15 | **Recap Day 1**                    | Quick discussion on custom user models, roles, and basic CRUD. Ask learners to share experiences or difficulties from Day 1 labs.          |
| 0:15–0:45 | **Django Authentication Views**    | Introduce `LoginView`, `LogoutView`, `PasswordChangeView`, `PasswordResetView`. Show demo in browser and explain URL patterns.             |
| 0:45–1:15 | **Implement Login & Logout**       | Guide learners to create login template. Emphasize CSRF tokens. Test login/logout workflow together.                                       |
| 1:15–1:45 | **Protecting Views**               | Explain `@login_required` and `@permission_required`. Demo protecting `user_list` and `edit_user` views. Highlight `raise_exception=True`. |
| 1:45–2:15 | **Groups & Permissions**           | Demonstrate creating groups (`Editors`, `Viewers`) in admin. Assign permissions. Ask learners to check access as different users.          |
| 2:15–2:45 | **Break**                          | 15–20 minutes                                                                                                                              |
| 2:45–3:30 | **Role-Based Access Control**      | Guide learners to create editor-only and viewer-only pages. Discuss how roles relate to permissions.                                       |
| 3:30–4:00 | **Password Management**            | Walk through password change/reset views. Show templates and forms. Emphasize security.                                                    |
| 4:00–4:30 | **Lab Exercise: Role-Based Pages** | Assist learners in building role-based pages and testing access control.                                                                   |
| 4:30–4:50 | **Review & Q&A**                   | Recap login/logout, decorators, groups, role-based pages. Answer questions.                                                                |
| 4:50–5:00 | **Homework / Assignment**          | Optional: Extend groups/permissions, experiment with `@permission_required` on new views.                                                  |

---

## **3. Trainer Tips**

* Emphasize the difference between **authentication** (login/logout) and **authorization** (permissions, groups, roles).
* Demonstrate **live testing**: log in as different users to verify access control.
* Encourage learners to use **Django admin** for experimenting with groups and permissions.
* Remind learners to include **CSRF tokens** in templates for forms.
* Use **real-world role examples** (editor, viewer, admin) to clarify abstract concepts.

---

## **4. Suggested Instructor Code Snippets**

* **Login URL**

```python
from django.contrib.auth import views as auth_views

urlpatterns = [
    path('login/', auth_views.LoginView.as_view(template_name='accounts/login.html'), name='login'),
    path('logout/', auth_views.LogoutView.as_view(next_page='/login/'), name='logout'),
]
```

* **Protecting Views**

```python
from django.contrib.auth.decorators import login_required, permission_required

@login_required
def user_list(request):
    ...

@permission_required('accounts.change_customuser', raise_exception=True)
def edit_user(request, user_id):
    ...
```

* **Role-Based Page**

```python
from django.http import HttpResponseForbidden

@login_required
def editor_page(request):
    if request.user.role != 'editor':
        return HttpResponseForbidden("You do not have access")
    return render(request, 'accounts/editor_page.html')
```

---

## **5. Learning Checks**

* Can learners log in and log out successfully?
* Can they change or reset passwords?
* Can they protect views with decorators and test access?
* Can they create groups and assign permissions to users?
* Can they implement a role-based page and restrict access correctly?

---

## **6. Resources for Trainer**

* [Django Authentication Documentation](https://docs.djangoproject.com/en/stable/topics/auth/)
* [Django Groups & Permissions](https://docs.djangoproject.com/en/stable/topics/auth/default/#groups)

