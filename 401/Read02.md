# Testing and Modules

## Unit tests

They are some pieces of code to exercise the input, the output, and the behavior of the code.

### Important aspects about unit tests

- Test file name should be the same as the tested file name but with *test_* before.

- Structure of the test should be in the **AAA** structure, which is:
  - Arrange: you need to organize data needed to execute the code (input).
  - Act: Execute the code being tested.
  - Assert: check if the result is same as the expected.
- Choosing test libraries, we will use ***pytest***.
- The Cycle:
We can use this approach in order to make a test :
  - Write a unit test and make it fail.
  - Write the feature that makes the test pass.
  - Refactor code to have the best solution.

## Recursion

It is the process with a function calls itself directly or indirectly, and the corresponding function is called a recursive function.
In recursive programs there something called *base case* , which is the simplist case of the problem and it's solution should be provided, and the bigger problems are expressed in terms of smaller problems, and if the base case is not reached or not defined, ***Stack over flow problem may arise***
There are two types of recursion, **Direct** which calls the same functions, and **Indirect** it calls another function, for example

```python
    # Direct recursion
    def directRecFun():

        # Some code....

        directRecFun()

        # Some code...
```

```python
    # An example of indirect recursion
    def indirectRecFun1():

        # Some code...

        indirectRecFun2()

        # Some code...

    def indirectRecFun2():

        # Some code...

        indirectRecFun1()

        # Some code...
```

### Example for recursion

``` python
# A Python 3 program to
# demonstrate working of
# recursion


def printFun(test):
    if (test < 1):
        return
    else:
        print(test, end=" ")
        printFun(test-1) # statement 2
        print(test, end=" ")
        return

# Driver Code
test = 3
printFun(test)
```

```python

# Python code to implement Fibonacci series
 
# Function for fibonacci
def fib(n):
 
    # Stop condition
    if (n == 0):
        return 0
 
    # Stop condition
    if (n == 1 or n == 2):
        return 1
 
    # Recursion function
    else:
        return (fib(n - 1) + fib(n - 2))
 
 
# Driver Code
 
# Initialize variable n.
n = 5;
print("Fibonacci series of 5 numbers is :",end=" ")
 
# for loop to print the fiboancci series.
for i in range(0,n):
    print(fib(i),end=" ")
```
