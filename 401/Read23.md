# Django Best Practices: Custom User Model

## Setup

Do the following steps in the terminal:

```shell
$ take accounts
$ poetry add django
$ poetry add --dev black flake8
$ poetry shell
(accounts) $ django-admin startproject config .
(accounts) $ python manage.py startapp accounts
(accounts) $ python manage.py runserver
```

we will see the following page after navigating to `http://127.0.0.0:8000`

![server](https://learndjango.com/static/images/django31_welcome.png)

press Ctrl + c to stop server.

We should not run `migrate` until we create our customer user model.

### Customer User Model

Creating our initial custom user model requires four steps:

* update config/settings.py
* create a new CustomUser model
* create new UserCreation and UserChangeForm
* update the admin

1. In `settings.py` we'll add the accounts app and use the **AUTH_USER_MODEL** config to tell Django to use our new custom user model in place of the built-in User model. We'll call our custom user model CustomUser.

2. Within **INSTALLED_APPS** add accounts at the bottom. Then at the bottom of the entire file, add the **AUTH_USER_MODEL** config.

    ```python
    # config/settings.py
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'accounts',
    ]
    ...
    AUTH_USER_MODEL = 'accounts.CustomUser'
    ```

3. update accounts/models.py with a new User model which we'll call CustomUser.

    ```python
    # accounts/models.py
    from django.contrib.auth.models import AbstractUser
    from django.db import models

    class CustomUser(AbstractUser):
        pass
        # add additional fields in here

        def __str__(self):
            return self.username
    ```

4. Create new file in the account called `forms.py`

    `(accounts) $ touch accounts/forms.py`

5. Update the file with the following code

    ```python
    # accounts/forms.py
    from django import forms
    from django.contrib.auth.forms import UserCreationForm, UserChangeForm
    from .models import CustomUser

    class CustomUserCreationForm(UserCreationForm):

        class Meta:
            model = CustomUser
            fields = ('username', 'email')

    class CustomUserChangeForm(UserChangeForm):

        class Meta:
            model = CustomUser
            fields = ('username', 'email')

    ```

6. Update `admin.py` since the Admin is highly coupled to the default User model.

    ```python
        # accounts/admin.py
    from django.contrib import admin
    from django.contrib.auth.admin import UserAdmin

    from .forms import CustomUserCreationForm, CustomUserChangeForm
    from .models import CustomUser

    class CustomUserAdmin(UserAdmin):
        add_form = CustomUserCreationForm
        form = CustomUserChangeForm
        model = CustomUser
        list_display = ['email', 'username',]

    admin.site.register(CustomUser, CustomUserAdmin)
    ```

7. Run the make migration and migrate commands.
  
    ```shell
    (accounts) $ python manage.py makemigrations accounts
    (accounts) $ python manage.py migrate
    ```

### Superuser

It's helpful to create a superuser that we can use to log in to the admin and test out log in/log out. On the command line type the following command and go through the prompts.

`(accounts) $ python manage.py createsuperuser`

### Templates/Views/URLs

We need a homepage with links to log in, log out, and sign up so follow these steps:

1. Update `settings.py` to use a project-level templates directory.

    ```python
    # config/settings.py
    TEMPLATES = [
        {
            ...
            'DIRS': [str(BASE_DIR.joinpath('templates'))], # new
            ...
        },
    ]
    ```

2. Set the redirect links for log in and log out, which will both go to our home template. Add these two lines at the bottom of the file.

    ```python
    # config/settings.py
    LOGIN_REDIRECT_URL = 'home'
    LOGOUT_REDIRECT_URL = 'home'
    ```

3. Create a new project-level templates folder and within it a registration folder as that's where Django will look for the log in template. We will also put our `signup.html` template in there.

    ```shell
    (accounts) $ mkdir templates
    (accounts) $ mkdir templates/registration
    ```

4. Create four templates

    ```shell
    (accounts) $ touch templates/registration/login.html
    (accounts) $ touch templates/registration/signup.html
    (accounts) $ touch templates/base.html
    (accounts) $ touch templates/home.html
    ```

5. Update the files as follows:

    ![base](https://i.ibb.co/n7yzg5z/base.png)

    ![home](https://i.ibb.co/wcxcF0H/home.png)

    ![login](https://i.ibb.co/YysJf8c/login.png)

    ![signup](https://i.ibb.co/6ZL1psz/signup.png)

6. Now for our `urls.py` files at the project and app level.

    ```python
    # config/urls.py
    from django.contrib import admin
    from django.urls import path, include
    from django.views.generic.base import TemplateView

    urlpatterns = [
        path('', TemplateView.as_view(template_name='home.html'), name='home'),
        path('admin/', admin.site.urls),
        path('accounts/', include('accounts.urls')),
        path('accounts/', include('django.contrib.auth.urls')),
    ]
    ```

7. Create a urls.py file in the accounts app.

    `(accounts) $ touch accounts/urls.py`

8. Fill in the following code:

    ```python

    # accounts/urls.py
    from django.urls import path
    from .views import SignUpView

    urlpatterns = [
        path('signup/', SignUpView.as_view(), name='signup'),
    ]
    ```

9. Last step is our `views.py` file in the accounts app which will contain our signup form.

    ```python
    # accounts/views.py
    from django.urls import reverse_lazy
    from django.views.generic.edit import CreateView

    from .forms import CustomUserCreationForm

    class SignUpView(CreateView):
        form_class = CustomUserCreationForm
        success_url = reverse_lazy('login')
        template_name = 'registration/signup.html'
    ```
