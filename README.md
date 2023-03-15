# Lab5_202001027
## Static Analysis using Mypy tool.

- MyPy tool is used to analyze static code i.e. static functions of the code will be analyzed and errors will be reflected
- While dynamic functions of python (where return variable type is not defined) will not be analyzed for error-checking
- We checked our dummy repository of the project using Mypy tool with command 'py -m mypy ./'

```sh
#!/usr/bin/env python
"""Django's command-line utility for administrative tasks."""
import os
import sys


def main():
    """Run administrative tasks."""
    os.environ.setdefault("DJANGO_SETTINGS_MODULE", "auto_attendance.settings")
    try:
        from django.core.management import execute_from_command_line
    except ImportError as exc:
        raise ImportError(
            "Couldn't import Django. Are you sure it's installed and "
            "available on your PYTHONPATH environment variable? Did you "
            "forget to activate a virtual environment?"
        ) from exc
    execute_from_command_line(sys.argv)


if __name__ == "__main__":
    main()
```

```sh
from django.contrib import admin
from django.urls import path

from . import views

urlpatterns = [
    path("admin/", admin.site.urls),
    path('',views.home_page,name = "home_page"),
    path('student_login',views.student_login,name = "student_login"),
    path('instructor_login',views.instructor_login,name = "instructor_login"),
    path('register_instructor',views.create_new_instructor_account,name = "register_instructor"),
    path('register_student',views.create_new_student_account,name = "register_student")
]
```

```sh
##########################################################################
from django.shortcuts import render,redirect
from django.contrib.auth.models import User
from django.contrib.auth import authenticate
from django.contrib import messages
from django.contrib.auth import authenticate,login,logout
##########################################################################



#################Home Page##############

def home_page(request):
    if request.user.is_authenticated:
        user = request.user
        # redirect to main page
    else:
        return render(request,'account_credentials/index.html')

#####################################3

###################Login###########################

###########INSTRUCTOR LOGIN#######################
def instructor_login(request):
    if request.method == 'POST':
        user_name = request.POST.get("user_name")
        password = request.POST.get("password")
        user = authenticate(username=user_name, password=password)
        if user is not None:
            # login successfull
            login(request,user)
            # redirect to main instructor page
        else:
            messages.success(request,"Invalid Username/password")
            return render("account_credentials/login_instructor.html")
    else:
        return render(request,"account_credentials/login_instructor.html")

################################################

#################STUDENT LOGIN#####################
def student_login(request):
    if request.method == 'POST':
        user_name = request.POST["user_name"]
        password = request.POST["password"]
        user = authenticate(username=user_name, password=password)
        if user is not None:
            # login successfull
            login(request,user)
            # redirect to main instructor page
        else:
            messages.success(request,"Invalid Username/password")
            return render("account_credentials/login_student.html")
    else:
        return render(request,"account_credentials/login_student.html")
##################################################


###################################################

##################CREATE NEW ACCOUNT################################################################

################INSTRUCTOR CREATE NEW ACCOUNT###############################

def create_new_instructor_account(request):
    if request.method == 'POST':
        username = request.POST['username']
        password = request.POST['password']
        first_name = request.POST['first_name']
        last_name = request.POST['last_name']
        email = request.POST['email']
        user = User.objects.create_user(firstname = first_name,lastname = last_name,email = email,username = username,password = password)
        user.save()
        # is instructor
        login(request,user)
        # redirect to main instructor page
    else:
        # create_new_account_page for student
        return render(request,"account_credentials/register_instructor.html")

############################################################################

#################STUDENT CREATE NEW ACCOUNT###################################
def create_new_student_account(request):
    if request.method == 'POST':
        username = request.POST['username']
        password = request.POST['password']
        first_name = request.POST['first_name']
        last_name = request.POST['last_name']
        email = request.POST['email']
        user = User.objects.create_user(firstname = first_name,lastname = last_name,email = email,username = username,password = password)
        user.save()
        login(request,user)
        # redirect to main student page
    else:
        # create_new_account_page for student
        return render(request,"account_credentials/register_student.html")

###########################################################################3

####################################################################################################

##################################LOGOUT#########################################################
def general_logout(request):
    logout(request)
    return redirect("home_page")
#################################################################################################
```

### Error 1:

- auto_attendance\urls.py:13: error: unmatched ']'  [syntax]
Found 1 error in 1 file (errors prevented further checking)
- After recognizing the error, mypy will stop looking for errors beyond that point.

![Screenshot (42)](https://user-images.githubusercontent.com/123458372/225282103-94239692-2da4-4dce-a71c-ab3072926c1e.png)

- All the syntax errors are found and solved one by one in this way.

### Error 2:

![Screenshot (41)](https://user-images.githubusercontent.com/123458372/225283535-69497938-16eb-461a-b407-b23220298116.png)

- After solving the syntax errors we got these errors at the end.

### Types of Errors:

- Syntax Errors 
- Import Errors
- Variable annotated errors

#### Syntax Errors:
Syntax errors are mistakes in the source code, such as spelling and punctuation errors, incorrect labels, and so on, which cause an error message to be generated by the compiler. These appear in a separate error window, with the error type and line number indicated so that it can be corrected in the edit window.

#### Import Errors:
This error generally occurs when a class cannot be imported due to one of the following reasons: The imported class is in a circular dependency. The imported class is unavailable or was not created. The imported class name is misspelled. The imported class from a module is misplaced.

#### Var Annotated Error:
This error occurs at the time of declaring the variable when variable type is not defined perfectly and consistently.
