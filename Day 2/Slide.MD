# **Slide Deck – Day 2: Authentication & Permissions**

---

## **Slide 1 – Title Slide**

**Title:** Django Authorization Crash Course – Day 2
**Subtitle:** Authentication & Permissions
**Additional:** Your Name / Date / Course Logo

---

## **Slide 2 – Learning Objectives**

By the end of Day 2, you will be able to:

1. Implement **login/logout** functionality
2. Handle **password change and reset** flows
3. Protect views with **`@login_required`** and **`@permission_required`**
4. Create **groups and assign permissions**
5. Implement **role-based access control**
6. Understand **Django’s permissions system**

---

## **Slide 3 – Django Authentication Views**

Django provides built-in class-based views:

| View                 | Purpose                            |
| -------------------- | ---------------------------------- |
| `LoginView`          | Handle user login                  |
| `LogoutView`         | Handle user logout                 |
| `PasswordChangeView` | Change password while logged in    |
| `PasswordResetView`  | Reset forgotten password via email |

**Example – URL mapping:**

```python
from django.contrib.auth import views as auth_views
path('login/', auth_views.LoginView.as_view(template_name='accounts/login.html'), name='login')
```

---

## **Slide 4 – Login / Logout Templates**

**Login Template Example:**

```html
<form method="post">
  {% csrf_token %}
  {{ form.as_p }}
  <button type="submit">Login</button>
</form>
```

**Logout:**

* Can redirect to login or home page
* Optionally show message: “You have logged out successfully.”

---

## **Slide 5 – Protecting Views**

**Function-based views:**

```python
from django.contrib.auth.decorators import login_required, permission_required

@login_required
def user_list(request):
    ...
    
@permission_required('accounts.change_customuser', raise_exception=True)
def edit_user(request, user_id):
    ...
```

* `@login_required`: Only authenticated users can access
* `@permission_required`: Only users with specific permissions can access

---

## **Slide 6 – Django Permissions Overview**

* Each model automatically has permissions:

  * `add`, `change`, `delete`, `view`
* Custom permissions can be added:

```python
class Meta:
    permissions = [
        ("can_publish", "Can publish articles"),
    ]
```

* Permissions can be assigned to **users or groups**

---

## **Slide 7 – Groups & Role-Based Access**

* Groups simplify permissions management
* Example roles:

  * **Editors:** add/change users
  * **Viewers:** view only
* Assign users to groups in **admin panel**

**Code Example – Check role:**

```python
if request.user.role != 'editor':
    return HttpResponseForbidden("Access denied")
```

---

## **Slide 8 – Role-Based Page Example**

```python
from django.http import HttpResponseForbidden

@login_required
def editor_page(request):
    if request.user.role != 'editor':
        return HttpResponseForbidden("You do not have access")
    return render(request, 'accounts/editor_page.html')
```

* Ensures only users with the `editor` role can access page

---

## **Slide 9 – Password Management**

* Changing password while logged in:

```python
path('password_change/', auth_views.PasswordChangeView.as_view(template_name='accounts/password_change.html'), name='password_change')
```

* Password reset via email:

```python
path('password_reset/', auth_views.PasswordResetView.as_view(), name='password_reset')
```

* Always ensure **secure password handling**

---

## **Slide 10 – Lab Exercise – Day 2**

**Goal:** Add authentication and role-based access to the project

**Tasks:**

1. Implement login/logout functionality
2. Add password change and password reset flows
3. Protect `user_list` and other views with `@login_required`
4. Implement `@permission_required` for edit views
5. Create groups (`Editors`, `Viewers`) and assign permissions
6. Build role-based pages (e.g., editor-only page)

**Optional Challenges:**

* Add navigation links for login/logout and protected pages
* Test combinations of roles, groups, and permissions

---

## **Slide 11 – Summary**

* Users can **log in and log out**
* Password change/reset flows are functional
* Views can be protected using decorators
* Groups simplify **role-based access control**
* Permissions are the foundation for **authorization**

**Next:** Day 3 – Class-Based View Mixins, Object-Level Permissions, and Security

---

