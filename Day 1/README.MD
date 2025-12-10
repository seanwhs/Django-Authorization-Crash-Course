# **Django Authorization Crash Course – Day 1: Foundations & User Management**

## **Overview**

Day 1 introduces the foundations of Django authentication and user management. You will learn the difference between **authentication** (verifying who a user is) and **authorization** (controlling what a user can do). The main focus is on understanding Django’s built-in User model and creating a **custom User model** to extend functionality with fields like roles or profiles.

By the end of the day, you will have:

* A working Django project
* A custom User model
* User registration and profile functionality

---

## **Topics Covered**

1. Authentication vs Authorization
2. Django User model overview
3. Custom User model (`AbstractUser` vs `AbstractBaseUser`)
4. CRUD operations for users
5. Password management and validators

---

## **Hands-On Goals**

1. Set up a new Django project and app.
2. Implement a custom User model with additional fields (e.g., `role`).
3. Create a superuser and test login via the Django admin.
4. Perform basic CRUD operations for users programmatically.
5. Explore password management securely using `set_password()`.

---

## **Key Concepts**

* **Custom User Model:** Extending `AbstractUser` to add extra fields such as role, profile info, or permissions.
* **Roles:** Simple way to implement access control based on user types (e.g., admin, editor, viewer).
* **Password Management:** Never store plain-text passwords; always use Django’s password hashing utilities.

---

## **References**

* [Django Custom User Model](https://docs.djangoproject.com/en/stable/topics/auth/customizing/)
* [Django Authentication Overview](https://docs.djangoproject.com/en/stable/topics/auth/)

