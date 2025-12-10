## ✅ **“Django Authorization in 3 Days Crash Course”**

This assessment validates:

* ✅ Real-world authorization skills
* ✅ Security awareness
* ✅ Practical Django implementation
* ✅ Role-based & object-level authorization

It includes:
✅ MCQs
✅ Scenario-based questions
✅ Hands-on coding
✅ **Answer Key**
✅ **Detailed Grading Rubric & Certification Rules**

---

# ✅ **POST-COURSE ASSESSMENT**

## *Django Authorization in 3 Days – Skills Validation Test*

**Duration:** 90 Minutes
**Total Marks:** 100
**Passing Mark:** 65
**Format:**

* Section A: MCQs (20 marks)
* Section B: Short Answer (30 marks)
* Section C: Practical Coding & Mini Project (50 marks)

---

# 🧠 **SECTION A: MCQs (20 Marks)**

**(2 marks × 10 questions)**

**1. What is the correct setting to define a custom user model?**
A. `USER_MODEL`
B. `CUSTOM_AUTH_USER`
C. `AUTH_USER_MODEL`
D. `DJANGO_USER`

✅ **Answer:** C

---

**2. Which class-based mixin enforces permission checking?**
A. `LoginRequiredMixin`
B. `AuthMixin`
C. `PermissionRequiredMixin`
D. `SecureMixin`

✅ **Answer:** C

---

**3. Which Django feature supports role-based access control?**
A. Middleware
B. Sessions
C. Groups
D. Tokens

✅ **Answer:** C

---

**4. Which permission is automatically created for every Django model?**
A. read
B. update
C. view
D. access

✅ **Answer:** C

---

**5. Which method checks if a user has a specific permission?**
A. `request.user.is_allowed()`
B. `request.user.has_perm()`
C. `request.user.check_permission()`
D. `request.user.validate_perm()`

✅ **Answer:** B

---

**6. Which decorator secures function-based views using permissions?**
A. `@user_passes_test`
B. `@login_required`
C. `@permission_required`
D. `@secure_view`

✅ **Answer:** C

---

**7. Which tool enables object-level permissions in Django?**
A. `django-police`
B. `django-guardian`
C. `django-security`
D. `django-shield`

✅ **Answer:** B

---

**8. Which view is used to log users out safely?**
A. `LogoutView`
B. `SignOutView`
C. `ExitView`
D. `EndSessionView`

✅ **Answer:** A

---

**9. Which Django setting ensures cookies are transmitted only over HTTPS?**
A. `SECURE_COOKIES`
B. `SESSION_COOKIE_SECURE`
C. `AUTH_COOKIE_SSL`
D. `COOKIE_SECURE_ONLY`

✅ **Answer:** B

---

**10. Which authentication method is recommended for APIs?**
A. Form Login
B. Token or JWT
C. Sessions only
D. Cookies only

✅ **Answer:** B

---

# ✍️ **SECTION B: Short Answer (30 Marks)**

**(6 marks × 5 questions)**

---

**11. Explain the difference between authentication and authorization with an example.**
✅ **Key Points Expected:**

* Authentication = identity verification
* Authorization = access control
* Example: Login vs editing admin data

---

**12. Explain the difference between `AbstractUser` and `AbstractBaseUser`.**
✅ **Key Points:**

* `AbstractUser` extends default user with minimal effort
* `AbstractBaseUser` provides full customization but requires full implementation

---

**13. Describe how Django Groups support role-based access control.**
✅ **Key Points:**

* Users assigned to groups
* Permissions assigned to groups
* Group permissions apply automatically

---

**14. What is middleware-based access control? Give one use case.**
✅ **Key Points:**

* Intercepts requests globally
* Applies access rules before views
* Example: Restrict admin access by IP or role

---

**15. List FOUR Django security best practices.**
✅ **Sample Answers (Any Four):**

* Use HTTPS
* Secure cookies
* Strong password validators
* CSRF protection
* Use environment variables
* Disable debug in production

---

# 💻 **SECTION C: Practical Coding & Mini Project (50 Marks)**

---

## ✅ **Part 1: Securing Views with Permissions (20 Marks)**

**16. You are given a model:**

```python
class Article(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
```

### a) Require users to be logged in to create articles (5 marks)

✅ Expected:

```python
from django.contrib.auth.decorators import login_required
```

```python
@login_required
def create_article(request):
```

---

### b) Require `add_article` permission (5 marks)

✅ Expected:

```python
from django.contrib.auth.decorators import permission_required
```

```python
@permission_required("app.add_article")
```

---

### c) Secure the same using class-based views (10 marks)

✅ Expected:

```python
from django.contrib.auth.mixins import LoginRequiredMixin, PermissionRequiredMixin

class ArticleCreateView(LoginRequiredMixin, PermissionRequiredMixin, CreateView):
    permission_required = "app.add_article"
```

---

## ✅ **Part 2: Object-Level Authorization (15 Marks)**

**17. Only the article author can edit the article. Explain how you would enforce this.**

✅ **Expected Concepts:**

* ForeignKey to user
* Filter by author
* `UserPassesTestMixin` or `django-guardian`
* Raise 403 if unauthorized

---

## ✅ **Part 3: Mini Project Design (15 Marks)**

**18. Design a secure Django system with:**

* Custom user model with roles
* Login/logout
* Role-based access
* Protected CRUD views
* Optional API token authentication

✅ **Must Include:**

* `AbstractUser` extension with role field
* Groups & permissions
* `@login_required`, `PermissionRequiredMixin`
* DRF token/JWT mention

---

# ✅ **FINAL GRADING RUBRIC**

| Section   | Marks   | Skill Area                     |
| --------- | ------- | ------------------------------ |
| A         | 20      | Core Concepts                  |
| B         | 30      | Architecture & Security        |
| C         | 50      | Practical Django Authorization |
| **Total** | **100** |                                |

---

# 🏆 **CERTIFICATION & READINESS LEVELS**

| Score        | Grade          | Meaning                                   |
| ------------ | -------------- | ----------------------------------------- |
| **85 – 100** | 🏆 Distinction | Production-ready authorization architect  |
| **70 – 84**  | 🟢 Proficient  | Can build secure role-based systems       |
| **65 – 69**  | 🟡 Pass        | Fundamental authorization skills achieved |
| **50 – 64**  | 🔴 Borderline  | Needs hands-on practice                   |
| **Below 50** | ❌ Fail         | Core authorization concepts not achieved  |

