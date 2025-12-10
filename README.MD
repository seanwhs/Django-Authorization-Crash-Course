## **Django Authorization in 3 Days Crash Course **

---

### **Day 1: Foundations & User Management**

**Topics:**

* Authentication vs Authorization
* Overview of Django User model
* Custom User model (`AbstractUser` vs `AbstractBaseUser`)
* CRUD operations for users
* Password management and validators

**Hands-On:**

* Set up Django project and app
* Implement a **custom User model** (e.g., adding `role` or `profile fields`)
* Create a superuser and regular users programmatically
* Implement user registration and profile editing

---

### **Day 2: Authentication & Permissions**

**Topics:**

* Login, logout, and password management (`LoginView`, `LogoutView`, `PasswordChangeView`)
* Redirects after login/logout
* Model-level permissions (`add`, `change`, `delete`, `view`)
* Custom permissions and `@permission_required` decorator
* Groups and role-based access

**Hands-On:**

* Implement login/logout flow with templates
* Implement password reset and change flow
* Assign users to **groups** and set group permissions
* Protect views using `@login_required` and `@permission_required`
* Restrict access based on roles (e.g., editor vs viewer)

---

### **Day 3: Advanced Authorization & Security**

**Topics:**

* Class-based view mixins: `LoginRequiredMixin`, `PermissionRequiredMixin`
* Object-level permissions (optional: `django-guardian`)
* Middleware for access control
* Security best practices: secure sessions, password policies, HTTPS
* Optional: API authentication using DRF (Token/JWT)

**Hands-On:**

* Secure class-based views using permission mixins
* Implement object-level permissions for custom user objects (e.g., only authors can edit their posts)
* Final mini-project:

  * User registration/login/logout with custom user
  * Role-based access control
  * Protected views and optional API endpoint

---

💡 **Tip:**

* **Day 1** is mostly setup and user handling.
* **Day 2** focuses on permissions and roles.
* **Day 3** is advanced authorization and security, ending with a small project to consolidate learning.

