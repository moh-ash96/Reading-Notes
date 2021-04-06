# Sending Form Data
## Client server architecture
it is the request response between the client and the server and it is summarized as follows:
* A client usually sends request to the server using *HTTP* protocol.
* The server responds using the same protocol.
* The *HTML* form will serve as user friendly way to send that request to the server.
## Client side
The form element defines how data will be sent , we can use attributes to configure the request that will be sent when a user submits the form, attributes include:
* **action**, it defines where the data will be sent, so its value should be either a relative or an absolute URL.
* **method**, it defines how the data will be sent, the most common are:
    * **GET**, it is used to ask the server to send back a given resource, the data is appended to the URL as a series of name/value pairs, after the URL ends we add (**?**) followed by name/value pairs, each one separated by (**&**), in this case we are sending two pieces of data to the server.
    * **POST**, it is the method the browser use to talk to the server when asking for a response that takes into account the data provided in the body of the HTTP request, and here no data will be appended to the URL, this is good in two ways:
        1. If you need to send a password so it will not be displayed on the URL with PUT, but it will be in GET.
        2. If you need to send a large amount of data.
* **enctype**, it lets you specify the value of the content-type HTTP header included in the request generated when the form is submitted, this header tells the server what kind of data is being sent
## Server side
When using any HTTP method, the server receives a string that will be parsed to get the data as a list key/value pairs, the way we access this list depends on which development platform we're using.
## Security issues
HTML forms are the most common attack vectors, we should follow security rules to keep the attackers away, including:
* Never trust the user.
* All the data comes to your server must have be checked and sanitized.
* Escape potentially dangerous characters.
* Limit the incoming amount of data to allow only what's necessary.
* Sandbox uploaded files, the should be stored in a different server and the access will be allowed to the file only through different subdomain or even better through a completely different domain.