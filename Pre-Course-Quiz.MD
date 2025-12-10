# ✅ **Pre-Course Quiz**

## *Django Authorization in 3 Days – Readiness Assessment*

**Purpose:**
To evaluate participants’ baseline understanding of Django authentication, authorization, and security before the course begins.

**Time:** 30 Minutes
**Total Marks:** 50
**Instructions:**

* Attempt **all questions**
* No IDE or internet required
* Write clearly for short answers

---

# 🧠 **Section A: Core Concepts (MCQs – 20 Marks)**

**(2 marks × 10 questions)**

**1. Authentication refers to:**
A. Granting user permissions
B. Verifying user identity
C. Managing sessions
D. Assigning user roles

---

**2. Which Django model is used by default to store users?**
A. `Account`
B. `BaseUser`
C. `auth.User`
D. `UserProfile`

---

**3. Which command correctly creates a superuser in Django?**
A. `django-admin adduser`
B. `python manage.py createsuperuser`
C. `python manage.py makeadmin`
D. `django-admin createsuperuser`

---

**4. Which decorator restricts a function-based view to authenticated users only?**
A. `@secure`
B. `@auth_required`
C. `@login_required`
D. `@permission_only`

---

**5. Which Django setting enables a custom user model?**
A. `CUSTOM_AUTH_MODEL`
B. `USER_MODEL`
C. `AUTH_USER_MODEL`
D. `DJANGO_USER`

---

**6. Which permission is automatically created by Django for models?**
A. publish
B. approve
C. view
D. assign

---

**7. What is Django’s built-in method for role-based access control?**
A. Teams
B. Policies
C. Groups
D. Roles

---

**8. What does `request.user.is_authenticated` return?**
A. User ID
B. Username
C. Boolean (True/False)
D. Session token

---

**9. Which class-based view mixin enforces user login?**
A. `AuthRequiredMixin`
B. `LoginRequiredMixin`
C. `SecureAccessMixin`
D. `PermissionOnlyMixin`

---

**10. Which technology is required to secure login credentials during transmission?**
A. HTTP
B. FTP
C. HTTPS
D. SMTP

---

# ✍️ **Section B: Short Answer (20 Marks)**

**(4 marks × 5 questions)**

**11. In your own words, define authentication.**

---

**12. Why would you use a custom user model instead of Django’s default one?**

---

**13. Name any TWO built-in Django authentication views.**

---

**14. What is a Django permission and where can it be enforced?**

---

**15. What is object-level authorization? Give one real-world example.**

---

# 💻 **Section C: Practical Logic & Mini Coding (10 Marks)**

**(5 marks × 2 questions)**

### **16. Protecting a View with Login**

Complete the code so that only authenticated users can access the dashboard.

```python
from django.shortcuts import render

def dashboard(request):
    return render(request, "dashboard.html")
```

---

### **17. Group-Based Access Control**

Write the Python condition that checks whether a user belongs to the **"Editors"** group.

---

---

# ✅ **ANSWER KEY**

---

## ✅ **Section A – MCQ Answers (20 Marks)**

| Q  | Answer |
| -- | ------ |
| 1  | ✅ B    |
| 2  | ✅ C    |
| 3  | ✅ B    |
| 4  | ✅ C    |
| 5  | ✅ C    |
| 6  | ✅ C    |
| 7  | ✅ C    |
| 8  | ✅ C    |
| 9  | ✅ B    |
| 10 | ✅ C    |

---

## ✅ **Section B – Model Answers (20 Marks)**

**11. Authentication**

> Authentication is the process of verifying a user’s identity before allowing access to a system.

---

**12. Purpose of Custom User Model**

> It allows developers to add or modify user attributes such as role, phone number, or username structure.

---

**13. Built-in Authentication Views (Any Two):**

* `LoginView`
* `LogoutView`
* `PasswordChangeView`
* `PasswordResetView`

---

**14. Django Permission**

> A permission defines what actions a user can perform on a model and is enforced in views, templates, and APIs.

---

**15. Object-Level Authorization Example**

> Only the author of a blog post can edit or delete that specific post.

---

## ✅ **Section C – Practical Answers (10 Marks)**

---

### **16. View Protection**

✅ **Correct Implementation:**

```python
from django.contrib.auth.decorators import login_required

@login_required
def dashboard(request):
    return render(request, "dashboard.html")
```

---

### **17. Group Check Condition**

✅ **Correct Answer:**

```python
request.user.groups.filter(name="Editors").exists()
```

✅ **Alternative Acceptable Answer:**

```python
"Editors" in request.user.groups.values_list("name", flat=True)
```

---

# 📊 **GRADING & READINESS INTERPRETATION**

| Score       | Level           | Interpretation                                                    |
| ----------- | --------------- | ----------------------------------------------------------------- |
| **0 – 19**  | 🔴 Beginner     | Participant strongly needs Django fundamentals before proceeding  |
| **20 – 34** | 🟡 Intermediate | Participant can follow the course with some guidance              |
| **35 – 44** | 🟢 Ready        | Participant is well-prepared for all 3 days                       |
| **45 – 50** | 🔵 Advanced     | Participant may be suitable for advanced tasks or mentoring roles |

