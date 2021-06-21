# JSON Web Token

## What is JSON Web Token

JSON Web Token (JWT) is an open standard that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed, they can be signed using a secret (with the **HMAC** algorithm) or a public/private key pair using **RSA** or **ECDSA**.
Although **JWTs** can be encrypted to also provide secrecy between parties, using signed tokens, these can verify the integrity of the claims contained within it, while encrypted tokens hide those claims from other parties. When tokens are signed using public/private key pairs, the signature also certifies that only the party holding the private key is the one that signed it.

## When to use JWTs

* Authorization
* Information exchange

## JWTs Structure

* ### Header

    The header typically consists of two parts: the type of the token, which is JWT, and the signing algorithm being used, such as HMAC SHA256 or RSA.
    For example:

    ```python
    {
        "alg": "HS256",
        "typ": "JWT"
    }
    ```

* ### Payload

    The second part of the token is the payload, which contains the claims. Claims are statements about an entity (typically, the user) and additional data. There are three types of claims: *registered*, *public*, and *private* claims.

  * Registered claims: These are a set of predefined claims which are not mandatory but recommended, to provide a set of useful, interoperable claims. Some of them are: iss (issuer), exp (expiration time), sub (subject), aud (audience), and others.

  Notice that the claim names are only three characters long as JWT is meant to be compact.

  * Public claims: These can be defined at will by those using JWTs. But to avoid collisions they should be defined in the IANA JSON Web Token Registry or be defined as a URI that contains a collision resistant namespace.

  * Private claims: These are the custom claims created to share information between parties that agree on using them and are neither registered or public claims.

    For example:

    ```python
    {
        "sub": "1234567890",
        "name": "John Doe",
        "admin": true
    }
    ```

    The payload is then Base64Url encoded to form the second part of the JSON Web Token.

* ### Signature

    The signature is issued by the JWT backend, using the header base64 + payload base64 + SECRET_KEY. Upon each request this signature is verified. If any information in the header or in the payload was changed by the client it will invalidate the signature. The only way of checking and validating the signature is by using your application’s SECRET_KEY.
    To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

    For example if you want to use the HMAC SHA256 algorithm, the signature will be created in the following way:

    ```python
    HMACSHA256(
        base64UrlEncode(header) + "." +
        base64UrlEncode(payload),
        secret)
    ```

  The signature is used to verify the message wasn't changed along the way, and, in the case of tokens signed with a private key, it can also verify that the sender of the JWT is who it says it is.

## Putting them all together

The result will be as the following:
![encoded](https://cdn.auth0.com/content/jwt/encoded-jwt3.png)

## How JWT Work

The JWT is just an authorization token that should be included in all requests:

`curl http://127.0.0.1:8000/hello/ -H 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQzODI4NDMxLCJqdGkiOiI3ZjU5OTdiNzE1MGQ0NjU3OWRjMmI0OTE2NzA5N2U3YiIsInVzZXJfaWQiOjF9.Ju70kdcaHKn1Qaz8H42zrOYk0Jx9kIckTn9Xx7vhikY'`

The JWT is acquired by exchanging an username + password for an access token and an refresh token, this access token is usually short-lived (expires in 5 min or so, can be customized though), while the refresh token lives a little bit longer (expires in 24 hours, also customizable). It is comparable to an authentication session, after it expires, you need a full login with username + password again.

## Installation & Setup

* Install django_rest_framework_simple_jwt -> `poetry add djangorestframework_simplejwt`
* Add the following in the **settings.py** file

    ```python
    REST_FRAMEWORK = {
        'DEFAULT_AUTHENTICATION_CLASSES': [
            'rest_framework_simplejwt.authentication.JWTAuthentication',
        ],
    }
    ```

* Add the following to **urls.py** file in project

    ```python
    from django.urls import path
    from rest_framework_simplejwt import views as jwt_views

    urlpatterns = [
    # Your URLs...
    path('api/token/', jwt_views.TokenObtainPairView.as_view(), name='token_obtain_pair'),
    path('api/token/refresh/', jwt_views.TokenRefreshView.as_view(), name='token_refresh'),
    ]
    ```

* Add the following to **views.py** as an example

    ```python
    from rest_framework.views import APIView
    from rest_framework.response import Response
    from rest_framework.permissions import IsAuthenticated


    class HelloView(APIView):
    permission_classes = (IsAuthenticated,)

    def get(self, request):
        content = {'message': 'Hello, World!'}
        return Response(content)
    ```

* The **urls** in the app

    ```python
    from django.urls import path
    from myapi.core import views

    urlpatterns = [
    path('hello/', views.HelloView.as_view(), name='hello'),
    ]
    ```

### Obtain Token

First step is to authenticate and obtain the token. The endpoint is /api/token/ and it only accepts POST requests.

`http post http://127.0.0.1:8000/api/token/ username=vitor password=123`

![obtain](https://simpleisbetterthancomplex.com/media/2018/12/jwt-obtain-token.png)

After that you are going to store both the access token and the refresh token on the client side, usually in the localStorage.

In order to access the protected views on the backend (i.e., the API endpoints that require authentication), you should include the access token in the header of all requests, like this:

`http http://127.0.0.1:8000/hello/ "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQ1MjI0MjAwLCJqdGkiOiJlMGQxZDY2MjE5ODc0ZTY3OWY0NjM0ZWU2NTQ2YTIwMCIsInVzZXJfaWQiOjF9.9eHat3CvRQYnb5EdcgYFzUyMobXzxlAVh_IAgqyvzCE"`

![use token](https://simpleisbetterthancomplex.com/media/2018/12/jwt-bearer.png)

This token is available for five minutes, after that an error will occur when trying to use it.

### Refresh Token

To get a new access token, you should use the refresh token endpoint /api/token/refresh/ posting the refresh token:

`http post http://127.0.0.1:8000/api/token/refresh/ refresh=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTU0NTMwODIyMiwianRpIjoiNzAyOGFlNjc0ZTdjNDZlMDlmMzUwYjg3MjU1NGUxODQiLCJ1c2VyX2lkIjoxfQ.Md8AO3dDrQBvWYWeZsd_A1J39z6b6HEwWIUZ7ilOiPE`

![refresh](https://simpleisbetterthancomplex.com/media/2018/12/jwt-refresh-token.png)

The return is a new access token that you should use in the subsequent requests.

The refresh token is valid for the next 24 hours. When it finally expires too, the user will need to perform a full authentication again using their username and password to get a new set of access token + refresh token.
