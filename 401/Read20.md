# Intro to Django

## Working with Django

### What is Django

Django is a high-level python framework that enables rapid development of secure and maintainable websites.

### Object-relational mapper

We can define our data models entirely in python, and get a data-base access API for free.

```python
class Band(models.Model):
    '''A model of a rock band'''
    name = models.CharField(max_length=200)
    can_rock = models.BooleanField(default=True)

class Me,ber(models.Model):
    '''A model of a rock band member'''
    name =  models.CharField('Member\'s name', max_length=200)
    instrument = models.CharField(choices=(
        ('g', 'Guitar'),
        ('b', 'Bass'),
        ('d', 'Drums'),
    ),
    max_length=1
    )
    band = models.ForeignKey('Band')
```

### URLs and Views

Using Django, we can design a beautiful URL scheme by creating a Python module called `URLconf`. It contains simple mapping between URL patterns and our views.

```python
from django.urls import path

from . import views

urlpatterns = [
    path('bands/', views.band_listing, name='band-list'),
    path('bands/<int:band_id>/', views.band_detail, name='band-detail'),
    path('bands/search/', views.band_search, name='band-search'),
]
```

```python
from django.shortcuts import render

def band_listing(request):
    '''A view of all bands'''
    bands = models.Band.objects.all()
    return render(request, 'bands/band_listing.html', {'bands': bands})
```

### Templates

The template language in Django uses HTML, and it is flexible and easy to use.

```html
<html>
    <head>
        <title>Band Listing</title>
    </head>
    <body>
        <h1>All Bands</h1>
        <ul>
        {% for band in bands %}
            <li>
                <h2><a href="{{ band.get_absolute_url }}">{{ band.name }}</a></h2>
                {% if band.can_rock %}<p>This band can rock!</p>{% endif %}
            </li>
            {% endfor %}
        </ul>
    </body>
</html>
```

### Forms

Django has a powerful form library that handles rendering forms as HTML, validating user-submitted data, and converting that data to native Python types, it also provides a way to generate forms from your existing models and use those forms to create and update data.

```python
from django import forms

class BandContactForm(forms.Form):
    subject = forms.CharField(max_length=100)
    message = forms.CharField()
    sender = forms.EmailField()
    cc_myself = forms.BooleanField(required=False)
```

### Authentication

Django comes with a full-featured and secure authentication system. It handles user accounts, groups, permissions and cookie-based user sessions. This lets you easily build sites that allow users to create accounts and safely log in/out.

```python
from django.contrib.auth.decorators import login_required
from django.shortcuts import render

@login_required
def my_protected_view(request):
    '''A view can only be accessed by logged-in users'''
    return render(request, 'protected.html', {'current_user': request,user})
```

## Admin

Django offers an admin interface that content procedures can immediatly use to start managing content on your site.

```python
from django.contrib import admin
from bands.models import Band, Member

class MemberAdmin(admit.ModelAdmin):
    '''Customize the look of the auto-generated admin for the member model'''
    list_display = ('name', 'instrument')
    list_filter = ('band',)

admin.site.register(Band)
admit.site.register(Member, MemberAdmin)
```

### Internationalization

Django offers full support for translating text into different languages, plus locale-specific formatting of dates, times, numbers, and time zones. It lets developers and template authors specify which parts of their apps should be translated or formatted for local languages and cultures, and it uses these hooks to localize Web applications for particular users according to their preferences.

```python
from django.shortcuts import render
from django.utils.translation import gettext

def homepage(request):
    '''
    shows the homepage with a welcome message that is translated in the user's language
    '''
    message = gettext('Welcome to our site!')
    return render(request, 'homepage.html', {'message': message})
```

```html
<!-- {% load i18n %} <== It should not be commented, but it is not recognized -->
<html>
    <head>
        <title>{% trans 'Homepage - Hall of Fame' %}</title>
    </head>
    <body>
        <h1>{{ message }}</h1>
        <p>
            {% blocktrans count member_count=bands.count %}
            Here is the only band in the hall of fame:
            {{% plural %}}
            Here are all the {{ member_count }} bands in the hall of fame:
            {% endblocktrans %}
        </p>
        <ul>
            {% for band in bands %}
            <li>
                <h2><a href="{{ band.get_absolute_url }}">{{ band.name }}</a></h2>
                {% if band.can_rock %}<p>{% trans 'This band can rock!' %}</p>{% endif %}
            </li>
            {% endfor %}
        </ul>
    </body>
</html>
```

### Security

#### Django provides multiple protections against:

* Clickjacking.
* Cross-site scripting.
* Cross Site Request Forgery (CSRF).
* SQL injection.
* Remote code execution.

## How Django works behind the scene

Django’s code is open source and available to all. It's organization is managed by a non-profit, the **DSF**, with a miniscule budget. And Django code is lead by a core team of volunteers, two paid Django Fellows, and a larger group of contributors.
