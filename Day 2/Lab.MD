# **Day 2 Lab – Authentication & Permissions**

**Project Goal for Day 2:**
Enhance the Day 1 project with **login/logout functionality**, **password management**, and **role-based permissions**. By the end of the day, only authorized users can access certain pages.

---

## **Step 1: Set Up Authentication URLs**

In your `accounts/urls.py`, add Django’s built-in auth views:

```python
from django.urls import path
from django.contrib.auth import views as auth_views
from . import views

urlpatterns = [
    path('users/', views.user_list, name='user_list'),
    path('login/', auth_views.LoginView.as_view(template_name='accounts/login.html'), name='login'),
    path('logout/', auth_views.LogoutView.as_view(), name='logout'),
    path('password_change/', auth_views.PasswordChangeView.as_view(template_name='accounts/password_change.html'), name='password_change'),
    path('password_change/done/', auth_views.PasswordChangeDoneView.as_view(template_name='accounts/password_change_done.html'), name='password_change_done'),
]
```

---

## **Step 2: Create Login/Logout Templates**

Create `accounts/templates/accounts/login.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Login</title>
</head>
<body>
    <h2>Login</h2>
    <form method="post">
        {% csrf_token %}
        {{ form.as_p }}
        <button type="submit">Login</button>
    </form>
</body>
</html>
```

Create a logout template (optional, e.g., a redirect to login or home page).

---

## **Step 3: Protect Views**

Use the `@login_required` decorator to restrict access to authenticated users.

In `accounts/views.py`:

```python
from django.contrib.auth.decorators import login_required

@login_required
def user_list(request):
    users = User.objects.all()
    return render(request, 'accounts/user_list.html', {'users': users})
```

---

## **Step 4: Permissions & Groups**

1. **Create groups** in the admin panel (e.g., `Editors`, `Viewers`)

2. **Assign permissions** to the groups:

   * Editors: Can add/change users
   * Viewers: Can only view users

3. Assign users to these groups.

---

## **Step 5: Restrict Views by Permission**

In `views.py`, use the `@permission_required` decorator:

```python
from django.contrib.auth.decorators import permission_required

@permission_required('accounts.change_customuser', raise_exception=True)
def edit_user(request, user_id):
    # logic to edit a user
    pass
```

---

## **Step 6: Role-Based Access**

You can restrict views based on the `role` field of your custom user model:

```python
from django.http import HttpResponseForbidden

@login_required
def editor_page(request):
    if request.user.role != 'editor':
        return HttpResponseForbidden("You do not have access to this page.")
    return render(request, 'accounts/editor_page.html')
```

---

## **Step 7: Exercises**

1. Create a **password change form** and test it with an existing user.
2. Implement **role-based pages**:

   * Editor page → only `editor` role can access
   * Viewer page → all logged-in users can access
3. Create a **group-based permission page** (Editors can edit users).
4. Test `@login_required` and `@permission_required` decorators.
5. Add **navigation links** for login, logout, and protected pages in templates.

---

✅ **Day 2 Outcome:**

* Users can log in and log out.
* Password management flows are functional.
* Views are protected using `@login_required` and `@permission_required`.
* Groups and roles are implemented for role-based access control.

