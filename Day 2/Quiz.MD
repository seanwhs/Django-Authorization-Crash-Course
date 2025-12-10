# **Day 2 Quiz – Authentication & Permissions**

**Instructions:** Choose the correct answer or provide the requested response. Each question is worth **1 point**.

---

### **Multiple Choice Questions**

**1. Which decorator is used to restrict a view to authenticated users only?**
A) `@permission_required`
B) `@login_required` ✅
C) `@user_passes_test`
D) `@authenticated_user`

**Answer:** B

---

**2. Which decorator is used to enforce specific permissions on a view?**
A) `@login_required`
B) `@user_passes_test`
C) `@permission_required` ✅
D) `@group_required`

**Answer:** C

---

**3. In Django, what is the purpose of groups?**
A) To group HTML templates
B) To organize users and assign permissions collectively ✅
C) To encrypt passwords
D) To store session data

**Answer:** B

---

**4. Which Django view handles user logout by default?**
A) `LogoutView` ✅
B) `LoginView`
C) `PasswordResetView`
D) `UserView`

**Answer:** A

---

**5. What will happen if a user without the required permission accesses a view decorated with `@permission_required(..., raise_exception=True)`?**
A) The user will be redirected to login page
B) The view will render normally
C) A `PermissionDenied` exception is raised ✅
D) The user will be logged out

**Answer:** C

---

### **True/False Questions**

**6. Users in the same group automatically share the same permissions.**

* True ✅
* False

**Answer:** True

---

**7. Role-based access control in Django can be implemented by checking a custom field (like `role`) in views.**

* True ✅
* False

**Answer:** True

---

### **Short Answer Questions**

**8. Name two built-in Django views used for password management.**
**Answer Example:** `PasswordChangeView`, `PasswordResetView`

---

**9. How would you restrict a view to allow access only to users in the “Editor” role?**
**Answer Example:**

```python
@login_required
def editor_page(request):
    if request.user.role != 'editor':
        return HttpResponseForbidden("Access denied")
    ...
```

---

**10. Explain the difference between a user’s role and a group in Django.**
**Answer Example:**

* **Role:** A custom field in the user model defining the user’s function (e.g., editor, viewer).
* **Group:** A collection of users with shared permissions, managed through Django admin.

