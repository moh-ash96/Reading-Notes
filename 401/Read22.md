# Django Forms

An HTML Form is a group of one or more fields on a web page, which can be used to collect information from users for submission to a server, they include text boxes, checkboxes, radio buttons, date pickers etc. they are also a relatively secure way of sharing data with the server, as they allow us to send data in POST requests with cross-site request forgery protection.

## HTML Forms

![form](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Forms/form_example_name_field.png)

the previous image is a form made by html, by the following code:

```html
<form action="/team_name_url/" method="post">
    <label for="team_name">Enter name: </label>
    <input id="team_name" type="text" name="name_field" value="Default name for team.">
    <input type="submit" value="OK">
</form>
```

### while

* **Action**: The resource/URL where data is to be sent for processing when the form is submitted. If this is not set (or set to an empty string), then the form will be submitted back to the current page URL.

* **Method**: The HTTP method used to send the data: post or get.
The POST method should always be used if the data is going to result in a change to the server's database because this can be made more resistant to cross-site forgery request attacks.
The GET method should only be used for forms that don't change user data (e.g. a search form). It is recommended for when you want to be able to bookmark or share the URL.

The role of the server is first to render the initial form state — either containing blank fields or pre-populated with initial values. After the user presses the submit button, the server will receive the form data with values from the web browser and must validate the information.

## Django form handling process

Django's form handling uses all of the same techniques that we learned about in previous tutorials (for displaying information about our models): the view gets a request, performs any actions required including reading data from the models, then generates and returns an HTML page (from a template, into which we pass a context containing the data to be displayed). What makes things more complicated is that the server also needs to be able to process data provided by the user, and redisplay the page if there are any errors.

![django chart](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Forms/form_handling_-_standard.png)

Based on the diagram above, the main things that Django's form handling does are:

1. Display the default form the first time it is requested by the user.
    * The form may contain blank fields (e.g. if you're creating a new record), or it may be pre-populated with initial values (e.g. if you are changing a record, or have useful default initial values).
    * The form is referred to as unbound at this point, because it isn't associated with any user-entered data (though it may have initial values).
2. Receive data from a submit request and bind it to the form.
    * Binding data to the form means that the user-entered data and any errors are available when we need to redisplay the form.
3. Clean and validate the data.
    * Cleaning the data performs sanitization of the input (e.g. removing invalid characters that might be used to send malicious content to the server) and converts them into consistent Python types.
    * Validation checks that the values are appropriate for the field (e.g. are in the right date range, aren't too short or too long, etc.)
4. If any data is invalid, re-display the form, this time with any user populated values and error messages for the problem fields.
5. If all data is valid, perform required actions (e.g. save the data, send an email, return the result of a search, upload a file, etc.)
6. Once all actions are complete, redirect the user to another page.

## Handling Forms

### Form

The Form class is the heart of Django's form handling system. It specifies the fields in the form, their layout, display widgets, labels, initial values, valid values, and (once validated) the error messages associated with invalid fields. The class also provides methods for rendering itself in templates using predefined formats (tables, lists, etc.) or for getting the value of any element (enabling fine-grained manual rendering).

### Declaring a Form

```python
from django import forms

class class_name(forms.Form):
    add the needed fields
```

### Form fields

* BooleanField
* CharField
* ChoiceField
* TypedChoiceField
* DateField
* DateTimeField
* DecimalField
* DurationField
* EmailField
* FileField
* FilePathField
* FloatField
* ImageField
* IntegerField
* GenericIPAddressField
* MultipleChoiceField
* TypedMultipleChoiceField
* NullBooleanField, RegexField, SlugField
* TimeField
* URLField
* UUIDField
* ComboField
* MultiValueField
* SplitDateTimeField
* ModelMultipleChoiceField
* ModelChoiceField

#### Arguments for the previous fields

* **required**: If True, the field may not be left blank or given a None value. Fields are required by default, so you would set required=False to allow blank values in the form.
* **label**: The label to use when rendering the field in HTML. If a label is not specified, Django will create one from the field name by capitalizing the first letter and replacing underscores with spaces (e.g. Renewal date).
* **label_suffix**: By default, a colon is displayed after the label (e.g. Renewal date:). This argument allows you to specify a different suffix containing other character(s).
* **initial**: The initial value for the field when the form is displayed.
* **widget**: The display widget to use.
* **help_text** (as seen in the example above): Additional text that can be displayed in forms to explain how to use the field.
* **error_messages**: A list of error messages for the field. You can override these with your own messages if needed.
* **validators**: A list of functions that will be called on the field when it is validated.
* **localize**: Enables the localization of form data input (see link for more information).
* **disabled**: The field is displayed but its value cannot be edited if this is True. The default is False.

### Validation

Django provides numerous places where you can validate your data. The easiest way to validate a single field is to override the method clean_<fieldname>() for the field you want to check.

### URL configuration

```python
urlpatterns += [
    path('put/the/path/here', add_the_view_here, name='view name')
]
```

### View

The view has to render the default form when it is first called and then either re-render it with error messages if the data is invalid, or process the data and redirect to a new page if the data is valid. In order to perform these different actions, the view has to be able to know whether it is being called for the first time to render the default form, or a subsequent time to validate data.
For forms that use a POST request to submit information to the server, the most common pattern is for the view to test against the POST request type (if request.method == 'POST') to identify form validation requests and GET (using an else condition) to identify the initial form creation request. If you want to submit your data using a GET request, then a typical approach for identifying whether this is the first or subsequent view invocation is to read the form data (e.g. to read a hidden value in the form).

### Templating

The last step is templating in an html file, and it is same to the previous labs, as it uses `{% this_type_of_templating %}` and we add the form and input tags inside this file.
