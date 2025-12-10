# **Django Authorization Crash Course – Day 2: Authentication & Permissions**

## **Overview**

Day 2 focuses on **authentication workflows and permission management** in Django. You’ll learn how to control access to views and actions based on user roles, groups, and permissions. By the end of the day, your project will support login/logout, password management, and role-based access control.

---

## **Topics Covered**

1. Django built-in authentication views:

   * `LoginView`, `LogoutView`, `PasswordChangeView`, `PasswordResetView`
2. Redirects after login/logout
3. Model-level permissions: `add`, `change`, `delete`, `view`
4. Custom permissions
5. Groups and role-based access
6. Decorators: `@login_required`, `@permission_required`

---

## **Hands-On Exercises**

1. Implement login and logout using Django’s built-in views.
2. Implement password change and reset flows with templates.
3. Assign users to groups and set group permissions.
4. Restrict access to views using decorators:

   * Example: only users with a specific permission can access certain pages.
5. Implement role-based access control (e.g., editor vs viewer) for views.

---

## **Key Goals**

* Enable secure login, logout, and password management workflows.
* Understand and apply model-level and custom permissions.
* Use groups to simplify role-based access control.
* Protect views and templates based on user permissions.

