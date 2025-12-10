# **Day 2 Learner Guide – Authentication & Permissions**

**Course:** Django Authorization Crash Course
**Day:** 2 – Authentication & Permissions
**Duration:** ~4–5 hours

---

## **1. Introduction**

Welcome to Day 2! Today, you’ll learn how to implement **login/logout**, manage **passwords**, and control access using **permissions and groups**. By the end of this session, your project will have fully functional authentication and role-based access.

**Learning Objectives:**

* Implement login and logout functionality
* Enable password change and reset flows
* Protect views with `@login_required` and `@permission_required`
* Create groups and assign permissions
* Implement role-based access control

---

## **2. Django Authentication Views**

Django provides built-in views for authentication:

| View                 | Purpose                            |
| -------------------- | ---------------------------------- |
| `LoginView`          | Handle user login                  |
| `LogoutView`         | Handle user logout                 |
| `PasswordChangeView` | Change password while logged in    |
| `PasswordResetView`  | Reset forgotten password via email |

**URL Example:**

```python
from django.contrib.auth import views as auth_views

urlpatterns = [
    path('login/', auth_views.LoginView.as_view(template_name='accounts/login.html'), name='login'),
    path('logout/', auth_views.LogoutView.as_view(next_page='/login/'), name='logout'),
    path('password_change/', auth_views.PasswordChangeView.as_view(template_name='accounts/password_change.html'), name='password_change'),
]
```

---

## **3. Implement Login & Logout**

**Login Template Example:**

```html
<form method="post">
  {% csrf_token %}
  {{ form.as_p }}
  <button type="submit">Login</button>
</form>
```

* Logout can redirect to login page or home page
* Test login/logout workflow in the browser

---

## **4. Protecting Views**

* Use **`@login_required`** to allow only authenticated users:

```python
from django.contrib.auth.decorators import login_required

@login_required
def user_list(request):
    ...
```

* Use **`@permission_required`** to enforce permissions:

```python
from django.contrib.auth.decorators import permission_required

@permission_required('accounts.change_customuser', raise_exception=True)
def edit_user(request, user_id):
    ...
```

---

## **5. Groups & Permissions**

* **Groups** simplify permission management:

  * Example: `Editors` → add/change users
  * Example: `Viewers` → view only

* Assign users to groups via **admin panel**

**Checking roles in views:**

```python
if request.user.role != 'editor':
    return HttpResponseForbidden("Access denied")
```

---

## **6. Role-Based Pages**

**Editor-Only Page Example:**

```python
from django.http import HttpResponseForbidden
from django.contrib.auth.decorators import login_required

@login_required
def editor_page(request):
    if request.user.role != 'editor':
        return HttpResponseForbidden("You do not have access")
    return render(request, 'accounts/editor_page.html')
```

* Ensures that only users with the `editor` role can access the page

---

## **7. Password Management**

* Change password while logged in:

```python
path('password_change/', auth_views.PasswordChangeView.as_view(template_name='accounts/password_change.html'), name='password_change')
```

* Reset password via email:

```python
path('password_reset/', auth_views.PasswordResetView.as_view(), name='password_reset')
```

* Always use secure password handling

---

## **8. Lab Exercises**

**Mandatory Exercises:**

1. Implement login/logout functionality
2. Add password change and password reset flows
3. Protect `user_list` and other views with `@login_required`
4. Implement `@permission_required` for edit views
5. Create groups (`Editors`, `Viewers`) and assign permissions
6. Build role-based pages (editor-only page)

**Optional Challenges:**

* Add navigation links for login/logout and role-based pages
* Test different combinations of roles, groups, and permissions

---

## **9. Summary**

* Users can log in and log out
* Password change/reset flows are functional
* Views can be protected with decorators
* Groups simplify role-based access control
* Roles and permissions form the foundation for **authorization**

**Next:** Day 3 – Class-Based View Mixins, Object-Level Permissions, and Security

