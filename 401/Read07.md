# Game of Greed 2

## Python scope

### Scopes

The concept of scope rules how the **variables** and **Names** are looked up in the code, it determines the *visibility* of the **variable**, and it depends on the place of the **variable** in the code.
The python scope concept follows the **LEGB** rule, which stands for:

* Local (or function) scope, it is in the function code block. All the names defined in the local scope are **only visible** inside it, and these names and they are defines with the call of the function, and you can define them as many as you call the function.

* Enclosing (or non-local) scope, it is a special scope that only exists for **nested functions**. If the local scope is an inner or nested function, then the enclosing scope is the scope of the outer or enclosing function.

* Global (or module) scope, It is the top-most scope in the python program, script, or module. The names defined globally are **visible** everywhere in the code.

* Built-in scope, It is a special scope that is created whenever you run a script or open an interactive session.

#### Nested Functions: The Enclosing scope

It is observed when you nest a function inside the other. The names defined in the enclosing scope are commonly known as the non-local names.
For example:

```python
def outer_func():
    #This block is the Local scope of outer_func()
    var = 100  #a non-local variable
    # it is also the enclosing scope of inner_func()
    def inner_func():
        #this block is the Local scope of the inner_func()
        print(f"Printing {var} from inner_func()")

    inner_func()
    print(f"Printing {var} from outer_func()")

outer_func()
```

the result will be:

```shell
Printing var from inner_func(): 100
Printing var from outer_func(): 100
```

and here,

```python
inner_func()
```

the result will be:

```shell
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'inner_func' is not defined
```

When calling the `outer_func()`, that creates a local scope. and the local scope of the `outer_func()` is the enclosing scope of the `inner_func()`. Inside the `inner_func()` the variable is not local, neither global, it is a special one called **enclosing scope**.
All the names created in the enclosing scope are visible from inside `inner_func()`, except for those created after calling `inner_func()`.  For example:

```python
def outer_fun():
    var = 100
    def inner_func():
        print(f"Printing {var} from inner_func()")
        print(f"Printing {another_var} from inner_func()")
    
    inner_func()
    another_var = 200 # this is defined after calling inner_func()
    print(f"Printing {var} from outer_func()")

outer_func()
```

the result will be:

```shell
Printing var from inner_func(): 100
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
    outer_func()
  File "<stdin>", line 7, in outer_func
    inner_func()
  File "<stdin>", line 5, in inner_func
    print(f"Printing another_var from inner_func(): {another_var}")
NameError: free variable 'another_var' referenced before assignment in enclosing
 scope
 ```

#### Modules: The Global Scope

From the moment you start a Python program, you’re in the global Python scope. Internally, Python turns your program’s main script into a module called __main__ to hold the main program’s execution. The namespace of this module is the main global scope of your program.

To inspect the names within your main global scope, you can use dir(). If you call dir() without arguments, then you’ll get the list of names that live in your current global scope.

The global name is accessible from any place in the code, for example:

```python
var = 100
def func():
    return var
func()
```

result:

`100`

Inside func(), you can freely access or reference the value of var. This has no effect on your global name var, but it shows you that var can be freely accessed from within func(). On the other hand, you can’t assign global names inside functions unless you explicitly declare them as global names using a global statement, and whenever assigning a value to a name in python, one of two things can happen:

1. Create a new name.
2. Update an existing name.

If you try to assign a value to a global name inside a function, then you’ll be creating that name in the function’s local scope, shadowing or overriding the global name. This means that you won’t be able to change most variables that have been defined outside the function from within the function.

for example:

```python
var = 100  # A global variable
def increment():
    var = var + 1  # Try to update a global variable

increment()
```

the result:

```shell
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
    increment()
File "<stdin>", line 2, in increment
    var = var + 1
UnboundLocalError: local variable 'var' referenced before assignment
```

Within increment(), you try to increment the global variable, var. Since var isn’t declared global inside increment(), Python creates a new local variable with the same name, var, inside the function. In the process, Python realizes that you’re trying to use the local var before its first assignment (var + 1), so it raises an `UnboundLocalError`.

### Modifying Behavior of a Python scope

#### The Global Statement

when you try to assign a value to a global name inside a function, you create a new local name in the function scope. To modify this behavior, you can use a global statement. With this statement, you can define a list of names that are going to be treated as global names.

The statement consists of the global keyword followed by one or more names separated by commas. You can also use multiple global statements with a name (or a list of names). All the names that you list in a global statement will be mapped to the global or module scope in which you define them.

```python
counter = 0  # A global name

 def update_counter():
     counter = counter + 1  # Fail trying to update counter

update_counter()
```

Result:

```shell
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 2, in update_counter
UnboundLocalError: local variable 'counter' referenced before assignment
```

When you try to assign counter inside `update_counter()`, Python assumes that counter is local to `update_counter()` and raises an `UnboundLocalError` because you’re trying to access a name that isn’t defined yet.

To solve this problem, so the following:

```python
counter = 0  # A global name
def update_counter():
    global counter  # Declare counter as global
    counter = counter + 1  # Successfully update the counter

update_counte
```

The counter will be updated with each call of the function.

#### The non-local Statement

Non-local names can be accessed from inner functions, but not assigned or updated. If you want to modify them, then you need to use a non-local statement. With a non-local statement, you can define a list of names that are going to be treated as non-local.

The non-local statement consists of the non-local keyword followed by one or more names separated by commas. These names will refer to the same names in the enclosing Python scope.
For example:

```python
def func():
    var = 100  # A nonlocal variable
    def nested():
        nonlocal var  # Declare var as nonlocal
        var += 100
    nested()
    print(var)
```

the result will be *200* when calling that function.
