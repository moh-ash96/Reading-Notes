# Docker

## Linux Containers

Docker is a Linux containers which are a type of virtualization.

Virtualization has its roots at the beginning of computer science when large, expensive mainframe computers were the norm.

### The downside to a virtual machine

* Size.
* speed.
A typical guest operating system can easily take up 700MB of size. So if one physical server supports three virtual machines, that’s at least 2.1GB of disk space taken up along with separate needs for CPU and memory resources.

Most computers rely on the same Linux operating system, so what if we virtualized from that level up instead? Wouldn’t that provide a lightweight, faster way to duplicate much of the same functionality?

The answer is yes. And in recent years Linux containers, also known as **containerization** has become increasingly popular. For most applications, a virtual machine provides far more resources than are needed and a container is more than sufficient.

This, fundamentally, is what Docker is. A way to implement Linux containers!

An analogy we can use here is that of homes and apartments. Virtual Machines are like homes: stand-alone buildings with their own infrastructure including plumbing and heating, as well as a kitchen, bathrooms, bedrooms, and so on. Docker containers are like apartments: they share common infrastructure like plumbing and heating, but come in various sizes that match the exact needs of an owner.

## Containers vs Virtual Environments

Virtual environments are used to isolate Python software packages locally. We can create an isolated box for individual projects so one can use Python 2.7 and Django 1.5 while another can use Python 3.5 and Django 2.1 on the same computer. Virtual environments are great.

But virtual environments can only isolate Python packages. They still rely on a global, system-level installation of Python albeit they can refer to the proper version. So when we use Python 2.7 in a project, we’re pointing to an installation of Python 2.7 on the computer itself, not actually within the virtual environment.

Also we can’t run a production database or other services within virtual environments so compared to Docker containers they are far more limited.

## Install Docker

1. Install desktop app package.
2. Create a free account.
3. Ensure that te version is at least 19.
4. Run `sudo pip install docker-compose`.
5. Ensure that its version is at least 1.24.x.
6. To confirm Docker installed correctly we can run our first command `docker run hello-world`, this will download an official image and then run the container, and the following will show in your terminal:

    ```shell
    Unable to find image 'hello-world:latest' locally
    latest: Pulling from library/hello-world
    1b930d010525: Pull complete
    Digest: sha256:9572f7cdcee8591948c2963463447a53466950b3fc15a247fcad1917ca215a2f
    Status: Downloaded newer image for hello-world:latest

    Hello from Docker!
    ```

7. Run `docker info` to inspect docker, the result is:

    ```shell
    Containers: 1
    Running: 0
    Paused: 0
    Stopped: 1
    Images: 1
    ```

## Images and Containers

### Images

To create an image, follow these steps:

1. Create a local directory on your computer for our code.
2. Define the image with a Dockerfile.
3. Run `FROM python:3.7-alpine

### Containers

Now that we have our Python image how do we run it? Well just as a Dockerfile is a list of image instructions there is also a docker-compose.yml file that is a list of container instructions.

To demonstrate a real-world image and container example we will now “Dockerize” a basic Django web app.

## Dockerized Django

* Create django app from scratch.
* Create docker file and docker-compose.yml:

    ```shell
    touch Dockerfile
    touch docker-compose.yml
    ```

 This Dockerfile has several commands. RUN, COPY, and ADD each create a new layer.

* Add the following code to Dockerfile:

    ```python
    #python version
    FROM python:3.7-alpine

    # set environment variables
    ENV PTHONDONTWRITEBYTECODE 1
    ENV PYTHONUNBUFFERED 1

    # Set work directory
    WORKDIR/code

    #Install dependencies
    COPY Pipfile Pipfile.lock /code/
    RUN pip install pipenv && pipenv install --system

    # Copy project
    COPY . /code/
    ```

    First we use FROM to install python:3.7-alpine as our base image and set two environment variables with ENV. The first, PYTHONDONTWRITEBYTECODE will remove .pyc files from our container which is a good optimization. The second, PYTHONUNBUFFERED will buffer our output so it will look “normal” within Docker for us.

    Then we used the WORKDIR command to create and set /code as our default directory within Docker. That means if in the future we want to run a command like python manage.py runserver we don’t have to also specify it should be run in the /code folder.

    The Pipfile contains information on our software packages so we copy that over, too. (Technically we could use COPY Pipfile . and because of the WORKDIR setting it would still go in the /code folder!)

    And then we install Pipenv itself via pip and then run pipenv install to install the software packages in our Pipfile. Note that we added the --system tag so that software packages are available throughout the entire container, not within a virtual environment which is Pipenv’s default but doesn’t make sense here since the entire Docker container is a virtual environment.

* Add the following code to the docker-compose.yml:

    ```python
    version: '3.7'

    services:
        web:
            bulid: .
            command: python/code/manage.py runserver 0.0.0.0:8000
            volumes:
            -.:/code
            ports:
            - 8000:8000
    ```

    At the top we specify we’re using the 3.7 version of Docker Compose and then set up a service, which is running within our container.

Multiple services can run within a Docker host–for example, we might add a db service for a running PostgreSQL database in the future–but for now we have a single web service.

We tell it to build the current directory, execute runserver on startup which will start the Django server. Then volumes will sync our local directory to the Docker container. And as a final step we expose port 8000 which is Django’s default so the container will expose it, too.

## Library Website and API

### Django REST Framework

Django REST Framework is added just like any other third-party app, we do that by :

1. Install django framework library by `$ pipenv install djangorestframework~=3.11.0`
2. Add it to the `INSTALLED APPS` inside `settings.py`.
3. Create api app: `$ python manage.py startapp api`.
4. Add it to `INSTALLED_APPS`, The api app will not have its own database models so there is no need to create a migration file and run migrate to update the database.
5. Add api path in the urls of the project:

    ```python
    # config/urls.py
    from django.contrib import admin
    from django.urls import path, include

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('api/', include('api.urls')), # new
        path('', include('books.urls')),
    ]
    ```

6. Create `urls.py` inside the api.
7. Update it as follows:

    ```python
    from django.urls import path
    from .views import BookAPIView

    urlpatterns = [
        path('', BookAPIView.as_view()),
    ]
    ```

8. In the views file, add the following:

    ```python
    from rest_framework import generics

    from books.models import Book
    from .serializers import BookSerializer


    class BookAPIView(generics.ListAPIView):
        queryset = Book.objects.all()
        serializer_class = BookSerializer
    ```

9. Make a api/serializers.py file, and add the following code to it:

    ```python
    from rest_framework import serializers

    from books.models import Book


    class BookSerializer(serializers.ModelSerializer):
    class Meta:
        model = Book
        fields = ('title', 'subtitle', 'author', 'isbn')
    ```

10. Use the popular cURL program to execute HTTP requests via the command line. All we need for a basic GET request it to specify curl and the URL we want to call.

    ```shell
    $ curl http://127.0.0.1:8000/api/
    [  
    {  
        "title":"Django for Beginners",
        "subtitle":"Build websites with Python and Django",
        "author":"William S. Vincent",
        "isbn":"978-198317266"
    }
    ]
    ```
