# **Day 2 Lesson Plan – Authentication & Permissions**

**Duration:** ~4–5 hours
**Target Audience:** Beginner to intermediate Django developers

---

## **Lesson Overview**

**Goal:** Implement user login/logout, password management, and role/group-based permissions in the project.

**Learning Objectives:**
By the end of Day 2, students will be able to:

1. Implement **login and logout** functionality
2. Enable **password change and reset** flows
3. Protect views using **`@login_required`** and **`@permission_required`**
4. Create **groups and assign permissions**
5. Implement **role-based access control** in views

---

## **Session Breakdown**

| Time      | Topic                              | Method               | Notes / Resources                                                                 |
| --------- | ---------------------------------- | -------------------- | --------------------------------------------------------------------------------- |
| 0:00–0:15 | **Recap Day 1**                    | Lecture / Discussion | Review custom user model and user list view                                       |
| 0:15–0:45 | **Django Authentication Views**    | Lecture + Demo       | `LoginView`, `LogoutView`, `PasswordChangeView`, `PasswordResetView`              |
| 0:45–1:15 | **Implement Login & Logout**       | Hands-On Lab         | Create login template, configure URLs, test login/logout workflow                 |
| 1:15–1:45 | **Protecting Views**               | Lecture + Lab        | Use `@login_required` and `@permission_required` decorators                       |
| 1:45–2:15 | **Groups & Permissions**           | Lecture + Demo       | Create groups in admin, assign permissions, test access                           |
| 2:15–2:45 | **Break**                          | —                    | 15–20 minutes                                                                     |
| 2:45–3:30 | **Role-Based Access Control**      | Lecture + Lab        | Restrict pages based on user role (`editor`, `viewer`)                            |
| 3:30–4:00 | **Password Management**            | Lecture + Lab        | Implement password change, reset flows, test functionality                        |
| 4:00–4:30 | **Lab Exercise: Role-Based Pages** | Hands-On Lab         | Create editor-only page, viewer page, protect views                               |
| 4:30–4:50 | **Review & Q&A**                   | Discussion           | Recap login/logout, permissions, groups, role-based access                        |
| 4:50–5:00 | **Homework / Exercises**           | Assignment           | Experiment with group-based access, try `@permission_required` on different views |

---

## **Key Teaching Points**

* `@login_required` ensures only authenticated users can access views
* `@permission_required` enforces permission-level access control
* Groups simplify role-based access management
* Roles can be stored in the custom user model for easy checks

---

## **Lab Exercises**

1. **Add Authentication URLs** (`accounts/urls.py`)

```python
from django.contrib.auth import views as auth_views
path('login/', auth_views.LoginView.as_view(template_name='accounts/login.html'), name='login'),
path('logout/', auth_views.LogoutView.as_view(), name='logout'),
path('password_change/', auth_views.PasswordChangeView.as_view(template_name='accounts/password_change.html'), name='password_change'),
```

2. **Create Login & Logout Templates**

```html
<form method="post">
  {% csrf_token %}
  {{ form.as_p }}
  <button type="submit">Login</button>
</form>
```

3. **Protect Views**

```python
from django.contrib.auth.decorators import login_required, permission_required

@login_required
def user_list(request):
    ...

@permission_required('accounts.change_customuser', raise_exception=True)
def edit_user(request, user_id):
    ...
```

4. **Create Groups and Assign Permissions**

* Example groups: `Editors`, `Viewers`
* Assign permissions in admin panel
* Test login as different users

5. **Role-Based Pages**

```python
from django.http import HttpResponseForbidden

@login_required
def editor_page(request):
    if request.user.role != 'editor':
        return HttpResponseForbidden("You do not have access")
    return render(request, 'accounts/editor_page.html')
```

---

## **Optional Challenges**

* Add navigation links for login/logout and role-based pages
* Test different combinations of roles and permissions
* Extend permissions using `@permission_required` on custom actions

---

## **Resources**

* [Django Authentication Docs](https://docs.djangoproject.com/en/stable/topics/auth/)
* [Django Groups & Permissions](https://docs.djangoproject.com/en/stable/topics/auth/default/#groups)

