# **Django Authorization Crash Course – Day 3: Advanced Authorization & Security**

## **Overview**

Day 3 focuses on **advanced authorization techniques and security best practices**. You will learn how to protect class-based views, implement object-level permissions, and ensure your application follows secure practices. By the end of the day, you’ll have a fully secure, role-aware Django application with both frontend and optional API protection.

---

## **Topics Covered**

1. Class-based view mixins:

   * `LoginRequiredMixin`
   * `PermissionRequiredMixin`
2. Object-level permissions (optional: `django-guardian`)
3. Middleware for access control
4. Security best practices:

   * Secure sessions
   * Password policies
   * HTTPS enforcement
   * Rate-limiting login attempts
5. Optional: API authentication using Django REST Framework (Token/JWT)

---

## **Hands-On Exercises**

1. Protect class-based views using permission mixins.
2. Implement object-level permissions so that, for example, users can edit only their own posts.
3. Apply security settings for sessions, passwords, and HTTPS.
4. Optionally, secure API endpoints with token-based authentication.
5. Final mini-project:

   * User registration/login/logout with custom user model
   * Role-based access control
   * Protected views and optional API endpoint

---

## **Key Goals**

* Secure both function-based and class-based views using permissions.
* Understand and apply object-level authorization.
* Follow Django security best practices.
* Consolidate knowledge from Days 1 and 2 into a working, secure application.

