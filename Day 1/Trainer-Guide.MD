# **Day 1 Trainer Guide – Foundations & User Management**

**Course:** Django Authorization Crash Course
**Day:** 1 – Foundations & User Management
**Duration:** ~4–5 hours

---

## **1. Learning Objectives**

By the end of this session, learners should be able to:

1. Distinguish **authentication** vs **authorization**
2. Understand Django’s **built-in User model**
3. Create a **Custom User model** with roles
4. Perform basic **CRUD operations** on users
5. Manage **passwords securely**

---

## **2. Session Flow & Timing**

| Time      | Topic                               | Trainer Notes / Tips                                                                                                                                          |
| --------- | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0:00–0:15 | **Introduction & Course Overview**  | Introduce yourself, explain 3-day plan, discuss real-world applications of authentication & authorization. Ask learners if they have used Django auth before. |
| 0:15–0:45 | **Authentication vs Authorization** | Explain the difference with simple examples. Encourage discussion: “Who can log in? Who can access which pages?”                                              |
| 0:45–1:15 | **Django User Model Overview**      | Show built-in fields and permissions. Demo in Django shell or admin. Highlight superuser and groups.                                                          |
| 1:15–1:45 | **Custom User Model**               | Explain `AbstractUser` vs `AbstractBaseUser`. Show how to add `role` field. Emphasize best practice: create custom user model at the start.                   |
| 1:45–2:15 | **Migrations & Superuser**          | Demonstrate `makemigrations`, `migrate`, and `createsuperuser`. Encourage learners to log in to admin.                                                        |
| 2:15–2:45 | **Break**                           | 15–20 minutes                                                                                                                                                 |
| 2:45–3:30 | **Basic User CRUD**                 | Hands-on: create a `user_list` view and template. Guide learners step by step.                                                                                |
| 3:30–4:00 | **Password Management**             | Demo `set_password()` and saving users programmatically. Emphasize never storing plain-text passwords.                                                        |
| 4:00–4:30 | **Optional Lab: Registration Form** | Encourage learners to create a simple registration form using `UserCreationForm`. Walk around to assist.                                                      |
| 4:30–4:50 | **Review & Q&A**                    | Recap key concepts: authentication vs authorization, custom user, roles. Answer questions.                                                                    |
| 4:50–5:00 | **Homework / Assignment**           | Assign adding extra fields (`bio`, `profile_picture`) or experimenting with registration forms.                                                               |

---

## **3. Trainer Tips**

* Use **live coding demos** to illustrate key points.
* Encourage learners to **experiment** in the shell (`python manage.py shell`).
* Stress **best practices**:

  * Always create a custom user model at project start
  * Never store passwords in plain text
* Make comparisons to **real-world roles** (editor, admin, viewer) to clarify concepts.
* Check learner progress frequently and address issues immediately.

---

## **4. Suggested Instructor Code Snippets**

* **Custom User Model**

```python
from django.contrib.auth.models import AbstractUser
from django.db import models

class CustomUser(AbstractUser):
    ROLE_CHOICES = (
        ('admin', 'Admin'),
        ('editor', 'Editor'),
        ('viewer', 'Viewer'),
    )
    role = models.CharField(max_length=10, choices=ROLE_CHOICES, default='viewer')
```

* **Creating superuser**

```bash
python manage.py createsuperuser
```

* **Basic user list view**

```python
from django.contrib.auth import get_user_model
from django.shortcuts import render

User = get_user_model()

def user_list(request):
    users = User.objects.all()
    return render(request, 'accounts/user_list.html', {'users': users})
```

---

## **5. Learning Checks**

* Ask learners to **explain the difference between authentication and authorization**.
* Verify they can **create a superuser** and log in to admin.
* Check that learners can **list users** in a template and use `set_password()` securely.

---

## **6. Resources for Trainer**

* [Django Custom User Model Documentation](https://docs.djangoproject.com/en/stable/topics/auth/customizing/)
* [Django Authentication Overview](https://docs.djangoproject.com/en/stable/topics/auth/)

