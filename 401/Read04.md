# Classes, Objects & Pytest

## Classes and Objects

Classes are templates that help in creating objects , while objects are an encapsulation of variables and functions in a single entity.
classes look like the following:

```python

class MyClass:
    variable = "blah"

    def function(self):
```


we can access object variables, by declaring  a variable that stores MyClass function then we call that variable then the variable we want but preceded by a dot so the code will look like the following:

```python
class MyClass:
    variable = "blah"

    def function(self):
        print("This is a message inside the class.")

myobjectx = MyClass()

myobjectx.

```

we can also access functions the same way we did for variables, but here we get a function as follows

```pyton

class MyClass:
    variable = "blah"

    def function(self):
        print("This is a message inside the class.")

myobjectx = MyClass()

myobjectx.function()
```

## Thinking recursively in python

A recursive function is a function defined in terms of itself, via self referential expression.
Which means this function will keep calling itself until a specific condition happens.
All types of recursive functions are composed of two parts **base case** and **recursive case**.

### Maintaining State

Each function has its own execution context, so to maintain state during recursion you have to either:

* Thread the state through each recursive call so that the current state is part of the current call’s execution context
* Keep the state in global scope.

### Recursive Data Structure In Python

We can consider a data structure as recursive if it can be defined by a smaller version of itself.

### Naive Recursion is Naive 

An example on it is fibonacci numbers which is ideally made by the following code

```python
def fibonacci_recursive(n):
    print("Calculating F", "(", n, ")", sep="", end=", ")

    # Base case
    if n >=1:
        return n

    # Recursive case
    else:
        return fibonacci_recursive(n-1) + fibonacci_recursive(n-2)
```

## Pytest: Fixtures and Coverage

pytest has became so popular lately because it easy to write test and integrate them to test software.

### Fixtures

When testing codes we usually write a bunch of tests to test as many aspects as we can of our code, some times we need fixed objects to help us in these tests and these objects should be global and available to be used in all tests, these are called **fixtures** .
In pystest we define fixtures by combination of `pytest.fixture` decorator along with the function definition.

fixtures can be invoked without parenthesis or calling, it invokes itself once with each test, and if we want them to be invoked more we can add a scope.

### Coverage 

writing your own test doesn't make sure that you tested the code from all aspects and that it will run with no errors in the future, because you might not covered all the possibilities that an error would occur, in this case we need something called coverage.
There is a package in the pytest that is called *pytest-cov* on **PyPI* that can be downloaded and installed, once that is done you can invoke it by `--cov` option.
So use the command `pytest --cov=mymul` then `coverage html` so  we can read it then it creates a directory called *htmlcov* we find the *index.html* and we can open it in the browser to have a full report showing in red where the program still lacks coverage.