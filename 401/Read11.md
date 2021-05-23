# NumPy

It is a data analysis package that allows us to speed up our workflow and interface with other packages in python ecosystem.

## Lists of lists for CSV data

### CSV files

The CSV (Comma Separated Values) format is the most common import and export format for spreadsheets and databases.
We can read in this file format using `csv.read` object which will allow us to read in and split up all the content from *ssv* file.
For that, we do the following:

* import *csv* library.

* Open the winequality-red.csv file.
    * With the file open, create a new csv.reader object.
        * Pass in the keyword argument delimiter=";" to make sure that the records are split up on the semicolon character instead of the default comma character.
    * Call the list type to get all the rows from the file.
    * Assign the result to wines.

```python
import csv
with open('winequality-red.py', 'r) as f:
    wines = list(csv.reader(f, delimitera = ';'))
```

The data will be read into list of lists, each inner list ia a row from the *ssv* file, and each item inside the inner list is a string, which will make it harder for computation, we can use the following code to calculate the average quality of wines:

```python
qualities =
[float(item[-1]) for item in wines[1:]]
sum(qualities / len(qualities))
```

and we can do any calculation we want, but this way is complex, to make it simpler, we use NumPy.

### NumPy 2-Dimensional Arrays

a 2-dimensional array, which is also known as matrix, which is a different way of thinking about a lists of lists that it has rows and columns.
In NUmPy array, the number of dimensions is called the rank, and each dimension is called an axis, So the rows are first axis and the columns are the second axis.

#### Creating a NUmPy Array

We can create a NumPy array using the `numpy.array` function. If we pass in a list of lists, it will automatically create a NumPy array with the same number of rows and columns. Because we want all of the elements in the array to be float elements for easy computation, we’ll leave off the header row, which contains strings. One of the limitations of *NumPy* is that all the elements in an array have to be of the same type, so if we include the header row, all the elements in the array will be read in as strings. Because we want to be able to do computations like find the average quality of the wines, we need the elements to all be floats.
It is done using thd following code:

```python
import csv
with open("winequality-rd.csv", 'r') as f:
    wines = list(csv.reader(f, delimiter=";"))
import numpy as np
wines = np.array(wines[1:], dtype=np.float)
```

##### Alternative NumPy Array Creation Methods

We can also create NumPy arrays by creating an array where every element is zero using `numpy.zeros((3,4))`, This will create an array with 3 rows and 4 columns, where every element is 0, or create an array where every element is a random number by `numpy.random.rand`.

#### Using NumPy To Read In Files

We can use NumPy to directly read *csv* or other file types into arrays, using `numpy.genfromtxt` function, as the following code:

```python
wines = np.genfromtxt("winequality-red.csv", delimiter=";", skip_header=1)
```

wines will end up looking the same as if we read it into a list then converted it to an array of floats. NumPy will automatically pick a data type for the elements in an array based on their format.

#### Indexing NumPy Arrays

To select an item inside the NumPy array, we should use indexing, and the index starts from zero, and because the array is 2-dimensional, we pick an index for row number and an index for column number.
E.G. if we want the 3rd row and the 4th column we select :
`wines[2,3]`

#### Slicing NumPy Arrays

If we want to pick multiple elements in a range, we can use slicing method as for example:

* `wines[0:3,3]` or `wines[:3,3]` => this will pick the elements ranging from index 0 to 2 on the rows at column of index 3.

* `wines[:,3]` => This will pick the entire column of index 3.

* `wines[3,:]` => This will pick the entire row of index 3.

* `wines[:,:]` => This will show the entire array.

#### Assigning Values To NumPy Arrays

We can use indexes to assign values to any element in the array,
e.g. `wines[1,5] = 10` => This will change the value of the elements at row **1**, column **5** into **10**.
`wines[:,10] = 50` => This will change all the elements on column **10** into **50**.

### 1-Dimensional NumPy Arrays

One dimensional array is a vector and it needs only a single index to retrieve an element.

### N-Dimensional NumPy Arrays

For example, if we need the 3-Dimensional array. it will return a list of lists of lists of elements.

### NumPy Data Types

Data Types in NumPy include the following:

* float — numeric floating point data.

* int — integer data.

* string — character data.

* object — Python objects.

#### Converting Data Types

We can convert between data types inside the array using `numpy.astype(<datatype>)` => e.g. `wines.astype(int)` to convert the type into integer.

### NumPy Array Operations

#### Single Array Math

This will apply basic math operations on elements of one array.

#### Multiple Array Math

This will apply operations between two arrays.

#### Broadcasting

Unless the arrays that you’re operating on are the exact same size, it’s not possible to do elementwise operations. In cases like this, NumPy performs broadcasting to try to match up elements. Essentially, broadcasting involves a few steps:

* The last dimension of each array is compared.
    * If the dimension lengths are equal, or one of the dimensions is of length 1, then we keep going.
    * If the dimension lengths aren’t equal, and none of the dimensions have length 1, then there’s an error.
* Continue checking dimensions until the shortest array is out of dimensions.

### NumPy Array Methods

There are some methods used for complex operations such as:

* `numpy.ndarray.sum` => this will give us the sum of all elements in the array, and if we pass (axis=0) argument, it will sum the columns of the array, while (axis=1) argument will sum the rows of the array.

* `numpy.ndarray.mean` => finds the mean of the array.

* `numpy.ndarray.std` => finds the standard value of an array.

* `numpy.ndarray.min` => finds the minimum value of an array.

* `numpy.ndarray.max` => finds the maximum value of an array.

### NumPy Array Comparisons

We can use comparison operations between arrays, such as:
`<, >, <=, >=, ==`
and it will return a boolean array for all the elements in the range we are comparing.

#### Subsetting

Using the boolean array, we can select only certain columns and rows in the NumPy array, and this makes it easier to filter arrays for certain criteria.

### Reshaping NumPy Arrays

We have multiple functions for reshaping arrays, including:

* `numpy.transpose` => It will flip the axis, so rows become columns and vise versa.

* `numpy.ravel` => It will turn an array to one dimensional array, by merging the elements.

* `numpy.reshape` => It will reshape an array to a certain shape we specify.

### Combining NumPy Arrays

* `numpy.vstack` => It will combine multiple arrays vertically.

* `numpy.hstack` => It will combine multiple arrays horizontally.

* `numpy.concatenate` => It is a general purpose of hstack and vstack and we can pass the (axis=0) or (axis=1) arguments and the will correspond to vstack and hstack respectively. 