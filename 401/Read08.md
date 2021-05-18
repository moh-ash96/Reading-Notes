# List Comprehensions

It is a concise way to create e a list, and it consists of brackets containing an expression, followed by for loop, then zero or more for, or if clauses. The expression can be anything.
The result will be a new list after evaluating the expression in the context of for and if clauses that follow it.
an example on the usual way to make a list:

```python
new_list = []
for i in old_list:
    if filter(i):
        new_list.append(expression(i))
```

but with list comprehensions it becomes as the following:

```python
new_list = [expression(i) for i in old_list if filter(i)]
```

## Syntax

The basic syntax is:

```python
[expression for item in list if conditional]
```

while:

* **new_list**, is the new list (result).

* **expression(i)**, Expression based on the variable used for each element in the old list.

* **for i in old_list**, the word *for* is followed by variable name to use, followed by the word in the old list.

* **if filter(i)**, Apply a filter with an if statement.

## Examples

### Create a simple list

```python
x= [i for i in range(10)]
print(x)
# expected output:[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Create a list using loops and list comprehension

```python
squares = [i**2 for i in range(10)]
print(squares)
# expected output:[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

### Multiplying parts of a list

```python
list1 = [3, 4, 5]

multiplied = [item*3 for item in list1]

print(multiplied)
# expected output: [9, 12, 15]
```

### Show the first letter of each word

```python
listOfWords = ["this", "is", "a", "list", "of", "words"]

items = [word[0] for word in listOfWords]
print(items)
# expected output: ['t', 'i', 'a', 'l', 'o', 'w']
```

### Lower/Upper case converter

```python
print([x.lower() for i in [A, B, C]])
# expected output: [a, b, c]

print([x.upper() for i in [a, b, c]])
# expected output: [A, B, C]
```

### Print numbers only from a given string

```python
string = "Hello 12345 world"
numbers = [x for x in string if x.isdigit()]
print(numbers)
# expected output: ['1', '2', '3', '4', '5']
```

if we want letter rather than numbers we can use `x.isalpha()` instead of `x.isdigit()`

### Parsing a file using list comprehension

In this example, we can see how to get specific lines out from a text file.

Create a text file and put in some text in it.

```txt
this is line1
this is line2
this is line3
this is line4
this is line5
```

Save the file as test.txt

```python
fh = open("test.txt", "r")

result = [i for i in fh if "line3" in i]
print(result)
# expected output: ['this is line3']
```

### Using list comprehension in functions

```python
def double(x):
    return x*2

print(double(10))
# output: 20
```

using list comprehension with it is like:

```python
double1 = [double(x) for x in range(10)]
print(double1)
# output: [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]

# we can put conditions:

double2 = [double(x) for x in range(10) if x%2==0]
print(double2)
# output: [0, 4, 8, 12, 16]

double3 = [x+y for x in [10, 30, 50] for y in [20, 40, 60]]
print(double3)
# output: [30, 50, 70, 50, 70, 90, 70, 90, 110]
```