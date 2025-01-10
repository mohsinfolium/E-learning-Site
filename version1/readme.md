# E-learning-Site

A Django-based web application with user authentication (signup, login, logout) and admin panel functionality, designed for creating and managing e-learning content.

## Version 1

### Project Workflow

In Version 1 of the project, the focus is on setting up the basic user authentication system, integrating Bootstrap templates for a polished frontend, and enabling navigation between multiple pages using URL dispatching.

### Steps to Run the Project

#### 1. Initialize Virtual Environment

First, create a virtual environment for the project to manage dependencies:

```bash
python -m venv venv
```

Activate the virtual environment:

- For Windows:

  ```bash
  venv\Scripts\activate
  ```

- For macOS/Linux:
  ```bash
  source venv/bin/activate
  ```

#### 2. Install Django

With the virtual environment activated, install Django using pip:

```bash
pip install django
```

#### 3. Create a Django Project

Create a new Django project by running the following command:

```bash
django-admin startproject elearning_site
```

Navigate into the project directory:

```bash
cd elearning_site
```

#### 4. Create a Django App

Create an app within the project for user authentication (login, logout, signup):

```bash
python manage.py startapp login
```

#### 5. Configure Settings

In the `settings.py` file, add the `'login'` app to the `INSTALLED_APPS` list:

```python
INSTALLED_APPS = [
    ...
    'login',
]
```

Also, configure static files (for Bootstrap) and templates directories in the `settings.py` file:

```python
STATIC_URL = '/static/'
STATICFILES_DIRS = [
    BASE_DIR / "static",
]

TEMPLATES = [
    {
        ...
        'DIRS': [BASE_DIR / 'templates'],
    },
]
```

#### 6. Set Up URLs

Create a `urls.py` file in the `login` app and configure URL patterns for the login, logout, and signup views. Also, include these URLs in the main project’s `urls.py` file.

**In `login/urls.py`:**

```python
from django.urls import path
from . import views

urlpatterns = [
    path('login/', views.login_view, name='login'),
    path('logout/', views.logout_view, name='logout'),
    path('signup/', views.signup_view, name='signup'),
]
```

**In `elearning_site/urls.py`:**

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('login.urls')),
]
```

#### 7. Create Views

Define the views for handling login, logout, and signup in `login/views.py`:

```python
from django.shortcuts import render, redirect
from django.contrib.auth import login, logout
from django.contrib.auth.forms import UserCreationForm
from django.contrib.auth.views import LoginView

def signup_view(request):
    if request.method == 'POST':
        form = UserCreationForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('login')
    else:
        form = UserCreationForm()
    return render(request, 'signup.html', {'form': form})

def login_view(request):
    return render(request, 'login.html')

def logout_view(request):
    logout(request)
    return redirect('login')
```

#### 8. Create Templates

Create the following HTML templates in the `templates` directory for the login, logout, and signup views:

**In `templates/login.html`:**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Login</title>
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css"
      rel="stylesheet"
    />
  </head>
  <body>
    <div class="container">
      <h2>Login</h2>
      <form method="POST">
        {% csrf_token %}
        <div class="mb-3">
          <label for="username" class="form-label">Username</label>
          <input
            type="text"
            name="username"
            class="form-control"
            id="username"
          />
        </div>
        <div class="mb-3">
          <label for="password" class="form-label">Password</label>
          <input
            type="password"
            name="password"
            class="form-control"
            id="password"
          />
        </div>
        <button type="submit" class="btn btn-primary">Login</button>
      </form>
      <p>Don't have an account? <a href="{% url 'signup' %}">Sign up</a></p>
    </div>
  </body>
</html>
```

**In `templates/signup.html`:**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Sign Up</title>
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css"
      rel="stylesheet"
    />
  </head>
  <body>
    <div class="container">
      <h2>Sign Up</h2>
      <form method="POST">
        {% csrf_token %} {{ form.as_p }}
        <button type="submit" class="btn btn-primary">Sign Up</button>
      </form>
      <p>Already have an account? <a href="{% url 'login' %}">Login</a></p>
    </div>
  </body>
</html>
```

#### 9. Run the Project

Finally, run the Django development server to test the application:

```bash
python manage.py migrate
python manage.py runserver
```

You can now visit the application in your browser at `http://127.0.0.1:8000/` and test the login, logout, and signup functionality.

### Screenshots

Here are the screenshots of the login and signup pages:

**Login Page**
![Login Page Screenshot](https://github.com/mohsinfolium/E-learning-Site/blob/e11503c80fe5651593b809bafca7f577ac9813c9/version1/Screenshot%20from%202025-01-10%2019-47-46.png)

**Signup Page**
![Signup Page Screenshot](https://github.com/mohsinfolium/E-learning-Site/blob/e11503c80fe5651593b809bafca7f577ac9813c9/version1/Screenshot%20from%202025-01-10%2019-47-59.png)

**Logout Page**
![Logout Page Screenshot](https://github.com/mohsinfolium/E-learning-Site/blob/e11503c80fe5651593b809bafca7f577ac9813c9/version1/Screenshot%20from%202025-01-10%2019-48-17.png)

This version of the `README.md` includes all the necessary instructions and detailed steps to set up and run the project for Version 1, including setting up the virtual environment, Django installation, views, templates, and screenshots.
