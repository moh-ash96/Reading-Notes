# 401 Introduction

## Pain and suffering

pain is bearable when it is linked to growth because without this pain we will never reach our goals, while suffering is the same pain but when it is for nothing; there is no outcome from this pain.

## A beginner's guide to Big O Notation

Big O is used in computer science to describe the performance or complexity of an algorithm, it describes the worst-case scenario, and can be used to describe the execution time required or the space used by an algorithm.

### Common orders of growth

* **O(1)**
it describes an algorithm that will always execute in the same time regardless of the size of the input data set.

```python
bool IsFirstElementNull(IList<string> elements)
{
    return elements[0] == null;
}
```

* **O(N)**
It describes an algorithm whose performance will grow linearly and in direct proportion to the size of the input of the data set. 

```python
bool ContainsValue(IEnumerable<string> elements, string value)
{
    foreach (var element in elements)
    {
        if (element == value) return true; 
    }     
    return false; 
}
```

* **O(N^2)**
It represents an algorithm whose performance is directly proportional to the square of the size of the input data set. This is common with the algorithms involving nested iterations over the data set, deeper nested iterations will result in **O(N^3)**, **O(N^4)**

* **O(2^N)**
It denotes an algorithm whose growth doubles with each addition to the input data set. The growth curve of an O(2^N) function is exponential — starting off very shallow, then rising meteorically. An example of an O(2^N) function is the recursive calculation of Fibonacci numbers:

```python
int Fibonacci(int number)
{
    if (number <= 1) return number;
       
    return Fibonacci(number - 2) + Fibonacci(number - 1); 
}
```

## Facts and Myths about python

### Facts

* Names refer to values.

* Many names can refer to one value.

* Names are reassigned independently.

* Values live until no references.

* Assignment never copies data.

* Changes are visible through all names.

* Immutable values such as *ints*, *floats* *strings* *tuples*, can't alias

* Types of changes:
    * Changing an int: **rebinding**
    * Changing a list: **mutating**

* Reference can be more than just names, they can be:
    * Object attributes.
    * List elements.
    * Dictionaries values(and Keys).
    * Anything on the left side of an assignment.

* Lots of things are assignments.

* Names have no types and Values have no scope.

### Myths

* Mutable and immutable are assigned the same.

* Python has no variables.
