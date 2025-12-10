# **Day 1 Quiz – Foundations & User Management**

**Instructions:** Choose the correct answer or provide the requested response. Each question is worth **1 point**.

---

### **Multiple Choice Questions**

**1. What is the main difference between authentication and authorization?**
A) Authentication checks what a user can do; authorization verifies who a user is
B) Authentication verifies who a user is; authorization checks what a user can do
C) Authentication stores passwords; authorization logs activity
D) Authentication and authorization are the same

**Answer:** B

---

**2. Which Django model is commonly used as the base for creating a custom user?**
A) `AbstractBaseUser`
B) `AbstractUser`
C) `UserProfile`
D) `BaseUser`

**Answer:** B

---

**3. When is it best to create a custom user model in Django?**
A) Anytime during development
B) At the start of a project
C) Only after deploying to production
D) Only if using Django REST Framework

**Answer:** B

---

**4. Which of the following is NOT a default field in Django’s built-in User model?**
A) `username`
B) `email`
C) `role`
D) `password`

**Answer:** C

---

**5. How should passwords be stored in Django?**
A) Plain text in the database
B) Hashed automatically by Django
C) Encrypted manually using base64
D) Stored in session cookies

**Answer:** B

---

### **True/False Questions**

**6. The `superuser` has all permissions by default.**

* True ✅
* False

**Answer:** True

---

**7. You can safely add extra fields to the built-in User model after starting a project without using a custom user model.**

* True
* False ✅

**Answer:** False

---

### **Short Answer Questions**

**8. Name two roles you might include in a custom user model.**
**Answer Example:** `admin`, `editor`, `viewer`

---

**9. What is the Django command to create a superuser?**
**Answer:** `python manage.py createsuperuser`

---

**10. Why is it a good practice to create a custom user model at the start of a project?**
**Answer Example:** To allow adding custom fields (like roles) and avoid migration issues later. It provides flexibility for authentication and authorization design.

