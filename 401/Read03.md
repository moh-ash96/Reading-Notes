# FileIO & Exceptions

## Reading and Writing files in python

### Files

a file is a set of bytes used to stored data that is organized in a specific format, and they are composed of three main parts:

1. Header, which has the file information.
2. Data, the content written by the creator.
3. End of file, a special character that indicates the end of the file.

To get into a file, we need to find its path which is also of three parts:

1. Folder path.
2. File name.
3. Extension.

### Opening and closing files in python

In order to use a file, first, we need to open it using `.open(<filepath>)`, and closing by `close()`
Anytime you open a file, you need to close it, and this can be assured by using

```python
reader = open('filename.txt')
try:
    # Further file processing goes here
finally:
    reader.close()
```

this will ensure closing the file after use

There is also another arguments that can be added to the open file function including the following:

* 'r', open file reading mode (default value)
* 'w', open file writing mode
* 'rb' or 'wb', raw binary and buffered binary, respectively

### Reading and writing opened files

we can read an write to files using the following functions:

* .read(size=-1), This reads from the file based on the number of size bytes. If no argument is passed or None or -1 is passed, then the entire file is read.

* .readline(size= -1), This reads at most size number of characters from the line. This continues to the end of the line and then wraps back around. If no argument is passed or None or -1 is passed, then the entire line (or rest of the line) is read.

* .readlines(), This reads the remaining lines from the file object and returns them as a list.

* .write(string), This writes the string to the file.

* .writelines(seq), This writes the sequence to the file. No line endings are appended to each sequence item. It’s up to you to add the appropriate line ending(s).

## Exceptions

The difference between **syntax error** and **exception** error is that syntax error comes when there is something wrong with the code itself and when the wrong thing is fixed the error goes away, but with **exception** error the code is all correct but there is an error, and python figures out what class of errors is it and and the error pops, such as when dividing by zero, an error called *ZeroDivisionError* pops.

### Raising an exception

Exceptions can be raised if we want an error to appear when specific thing happens in the code such as in the following example:

```python
x = 10
if x > 5:
    raise Exception('x should not exceed 5. The value of x was: {}'.format(x))
```

and the output will be the following:

```Python Traceback
Traceback (most recent call last):
  File "<input>", line 4, in <module>
Exception: x should not exceed 5. The value of x was: 10
```

### The AssertionError Exception

We can use assert to test a part of the code and if it goes good, continue, if something is wrong we can add what the error should include as follows:

```python
import sys
assert ('linux' in sys.platform), "This code runs ln Linux only."
```

```python
Traceback (most recent call last):
  File "<input>", line 2, in <module>
AssertionError: This code runs on Linux only.
```

### try and except Block: handling Exceptions

Here it is like we try executing a code and if it goes wrong instead of crashing the code with exception error, we can provide an *except* followed by a code to follow if the error happens, and we can add more than one excepts for different types of errors as the following:

```python
try:
    linux_interaction()
    with open('file.log') as file:
        read_data = file.read()
except FileNotFoundError as fnf_error:
    print(fnf_error)
except AssertionError as error:
    print(error)
    print('Linux linux_interaction() function was not executed')
```

if the file doesn't exist, the return will be:

```shell
Function can only run on Linux systems.
Linux linux_interaction() function was not executed
```

if the code is run on linux the return will be:

```shell
[Errno 2] No such file or directory: 'file.log'
```

We can add an else statement to the code, when it runs good and the exception is not popped the else statement will be called.
At the end of the statement we can add another condition called finally, that will always run after the code is executed, so the final result will be:

```python
try:
    linux_interaction()
except AssertionError as error:
    print(error)
else:
    try:
        with open('file.log') as file:
            read_data = file.read()
    except FileNotFoundError as fnf_error:
        print(fnf_error)
finally:
    print('Cleaning up, irrespective of any exceptions.')
```

running it on windows will produce the following:

```shell
Function can only run on Linux systems.
Cleaning up, irrespective of any exceptions.
```

