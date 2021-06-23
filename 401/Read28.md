# API Deployment

## Managing Django Settings: Issues

* Different environments. Usually, you have several environments: local, dev, ci, qa, staging, production, etc. Each environment can have its own specific settings (for example: DEBUG = True, more verbose logging, additional apps, some mocked data, etc). You need an approach that allows you to keep all these Django setting configurations.

* Sensitive data. You have SECRET_KEY in each Django project. On top of this there can be DB passwords and tokens for third-party APIs like Amazon or Twitter. This data cannot be stored in VCS.

* Sharing settings between team members. You need a general approach to eliminate human error when working with the settings. For example, a developer may add a third-party app or some API integration and fail to add specific settings. On large (or even mid-size) projects, this can cause real issues.

* Django settings are a Python code. This is a curse and a blessing at the same time. It gives you a lot of flexibility, but can also be a problem – instead of key-value pairs, settings.py can have a very tricky logic.

### Setting Configuration

Separate settings file for each environment
This is an extension of the previous approach. It allows you to keep all configurations in VCS and to share default settings between developers.

In this case, you make a settings package with the following file structure:

```shell
settings/
   ├── __init__.py
   ├── base.py
   ├── ci.py
   ├── local.py
   ├── staging.py
   ├── production.py
   └── qa.py
```

settings/local.py:

```python
from .base import *


ALLOWED_HOSTS = ['localhost']
DEBUG = True
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'local_db',
        'HOST': '127.0.0.1',
        'PORT': '5432',
    }
}
```

`python manage.py runserver`

#### Pros

* All environments are in VCS.
* It’s easy to share settings between developers.

#### Cons

* You need to find a way to handle secret passwords and tokens.
* “Inheritance” of settings can be hard to trace and maintain.

### Environment variables

To solve the issue with sensitive data, you can use environment variables.

```python
import os


SECRET_KEY = os.environ['SECRET_KEY']
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.environ['DATABASE_NAME'],
        'HOST': os.environ['DATABASE_HOST'],
        'PORT': int(os.environ['DATABASE_PORT']),
    }
}
```

This is the simplest example using Python os.environ and it has several issues:

* You need to handle KeyError exceptions.
* You need to convert types manually.

To fix KeyError, you can write your own custom wrapper. For example:

```python
import os

from django.core.exceptions import ImproperlyConfigured


def get_env_value(env_variable):
    try:
      	return os.environ[env_variable]
    except KeyError:
        error_msg = 'Set the {} environment variable'.format(var_name)
        raise ImproperlyConfigured(error_msg)


SECRET_KEY = get_env_value('SECRET_KEY')
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': get_env_value('DATABASE_NAME'),
        'HOST': get_env_value('DATABASE_HOST'),
        'PORT': int(get_env_value('DATABASE_PORT')),
    }
}
```

Also, you can set default values for this wrapper and add type conversion. But actually there is no need to write this wrapper, because you can use a third-party library.

#### Pros

* Configuration is separated from code.
* Environment parity – you have the same code for all environments.
* No inheritance in settings, and cleaner and more consistent code.
* There is a theoretical grounding for using environment variables – 12 Factors.

#### Cons

You need to handle sharing default config between developers.

### 12 Factors

12 Factors is a collection of recommendations on how to build distributed web-apps that will be easy to deploy and scale in the Cloud. It was created by Heroku, a well-known Cloud hosting provider.

As the name suggests, the collection consists of twelve parts:

* Codebase
* Dependencies
* Config
* Backing services
* Build, release, run
* Processes
* Port binding
* Concurrency
* Disposability
* Dev/prod parity
* Logs
* Admin processes

Each point describes a recommended way to implement a specific aspect of the project. Some of these points are covered by instruments like Django, Python, pip. Some are covered by design patterns or the infrastructure setup. In the context of this article, we are interested in one part: the Configuration.

Its main rule is to store configuration in the environment. Following this recommendation will give us strict separation of config from code.

### django-environ

Environment variables are the perfect place to store settings.

Now it’s time to talk about the toolkit.

Writing code using os.environ could be tricky sometimes and require additional effort to handle errors. It’s better to use django-environ instead.

Technically it’s a merge of:

* envparse
* honcho
* dj-database-url
* dj-search-url
* dj-config-url
* django-cache-url

This app gives a well-functioning API for reading values from environment variables or text files, handful type conversion, etc. Let’s look at some examples.

`settings.py`

```python
import environ


root = environ.Path(__file__) - 3  # get root of the project
env = environ.Env()
environ.Env.read_env()  # reading .env file

SITE_ROOT = root()

DEBUG = env.bool('DEBUG', default=False)
TEMPLATE_DEBUG = DEBUG

DATABASES = {'default': env.db('DATABASE_URL')}

public_root = root.path('public/')
MEDIA_ROOT = public_root('media')
MEDIA_URL = env.str('MEDIA_URL', default='media/')
STATIC_ROOT = public_root('static')
STATIC_URL = env.str('STATIC_URL', default='static/')

SECRET_KEY = env.str('SECRET_KEY')

CACHES = {'default': env.cache('REDIS_CACHE_URL')}
```

`.env file`

```envDjango Settings: Best practices
Keep settings in environment variables.
Write default values for production configuration (excluding secret keys and tokens).
Don’t hardcode sensitive settings, and don’t put them in VCS.
Split settings into groups: Django, third-party, project.
Follow naming conventions for custom (project) settings.
DEBUG=True
DATABASE_URL=postgres://user:password@db.example.com:5432/production_db?sslmode=require
REDIS_CACHE_URL=redis://user:password@cache.example.com:6379/1
SECRET_KEY=Some-Autogenerated-Secret-Key
```

### Setting structure

Instead of splitting settings by environments, you can split them by the source: Django, third- party apps (Celery, DRF, etc.), and your custom settings.

File structure:

project/
├── apps/
├── settings/
│   ├── __init__.py
│   ├── djano.py
│   ├── project.py
│   └── third_party.py
└── manage.py

__init__.py file:

```python
from .django import *       # All Django related settings
from .third_party import *  # Celery, Django REST Framework & other 3rd parties
from .project import *      # You custom settings
```

Each module could be done as a package, and you can split it more granularly:

project/
├── apps/
├── settings/
│   ├── project
│   │   ├── __init__.py
│   │   ├── custom_module_foo.py
│   │   ├── custom_module_bar.py
│   │   └── custom_module_xyz.py
│   ├── third_party
│   │   ├── __init__.py
│   │   ├── celery.py
│   │   ├── email.py
│   │   └── rest_framework.py
│   ├── __init__.py
│   └── djano.py
└── manage.py

### Naming Conventions

Naming of variables is one of the most complex parts of development. So is naming of settings. We can’t imply on Django or third-party applications, but we can follow these simple rules for our custom (project) settings:

* Give meaningful names to your settings.
* Always use the prefix with the project name for your custom (project) settings.
* Write descriptions for your settings in comments.

### Django Settings: Best practices

* Keep settings in environment variables.
* Write default values for production configuration (excluding secret keys and tokens).
* Don’t hardcode sensitive settings, and don’t put them in VCS.
* Split settings into groups: Django, third-party, project.
* Follow naming conventions for custom (project) settings.

## SSH

SSH, or Secure Shell, is a remote administration protocol that allows users to control and modify their remote servers over the Internet. The service was created as a secure replacement for the unencrypted Telnet and uses cryptographic techniques to ensure that all communication to and from the remote server happens in an encrypted manner. It provides a mechanism for authenticating a remote user, transferring inputs from the client to the host, and relaying the output back to the client.

### How does it work

If you’re using Linux or Mac, then using SSH is very simple. If you use Windows, you will need to utilize an SSH client to open SSH connections. The most popular SSH client is PuTTY, which you can learn more about here.

For Mac and Linux users, head over to your terminal program and then follow the procedure below:

The SSH command consists of 3 distinct parts:

ssh {user}@{host}
The SSH key command instructs your system that you want to open an encrypted Secure Shell Connection. {user} represents the account you want to access. For example, you may want to access the root user, which is basically synonymous for system administrator with complete rights to modify anything on the system. {host} refers to the computer you want to access. This can be an IP Address (e.g. 244.235.23.19) or a domain name (e.g. www.xyzdomain.com).

When you hit enter, you will be prompted to enter the password for the requested account. When you type it in, nothing will appear on the screen, but your password is, in fact being transmitted. Once you’re done typing, hit enter once again. If your password is correct, you will be greeted with a remote terminal window.

### Encryption techniques

1. Symmetrical Encryption
    Symmetric encryption is a form of encryption where a secret key is used for both encryption and decryption of a message by both the client and the host. Effectively, any one possessing the key can decrypt the message being transferred.

2. Asymmetrical encryption
    Unlike symmetrical encryption, asymmetrical encryption uses two separate keys for encryption and decryption. These two keys are known as the public key and the private key. Together, both these keys form a public-private key pair.

3. Hashing
    One-way hashing is another form of cryptography used in Secure Shell Connections. One-way-hash functions differ from the above two forms of encryption in the sense that they are never meant to be decrypted. They generate a unique value of a fixed length for each input that shows no clear trend which can exploited. This makes them practically impossible to reverse.
