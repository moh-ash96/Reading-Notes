# Pandas

It is a fast, flexible, and expressive data structures designed to make working with relational or labeled data both easy and intuitive.

In order for us to use panda, we should first import it using:
`import pandas as pd`

## Object creation

we can create a series by passing a list of values, letting panda create a default integer index.

We also can Create a DataFrame by passing a NumPy array, with a datetime index and labeled columns.

And we can create data frame by passing a dict of objects that can be converted to series-like.

## Viewing data

`DataFrame.to_numpy()` gives a NumPy representation of the underlying data. Note that this can be an expensive operation when your DataFrame has columns with different data types, which comes down to a fundamental difference between pandas and NumPy: NumPy arrays have one *dtype* for the entire array, while pandas DataFrames have one *dtype* per column. When you call `DataFrame.to_numpy()`, pandas will find the NumPy *dtype* that can hold all of the *dtypes* in the DataFrame. This may end up being object, which requires casting every value to a Python object.

For df, our DataFrame of all floating-point values, DataFrame.to_numpy() is fast and doesn’t require copying data.

For df2, the DataFrame with multiple *dtype*s, DataFrame.to_numpy() is relatively expensive.

DataFrame.to_numpy() does not include the index or column labels in the output.

## Selection

### Getting

* Selecting a single column.

### Selection by label

* getting a cross section using a label

* Selecting on a multi-axis by label

* Showing label slicing, both endpoints are included

* Reduction in the dimensions of the returned object

### Selection by position

* Select via the position of the passed integers

* getting a value explicitly.

### Boolean indexing

* Using a single column’s values to select data.

* Selecting values from a DataFrame where a boolean condition is met.

* Using the isin() method for filtering

### Setting

* Setting a new column automatically aligns the data by the indexes.

* Setting values by label.

* Setting values by position.

* Setting by assigning with a NumPy array.

* The result of the prior setting operations.

* A **where** operation with setting.

## Missing data

pandas primarily uses the value `np.nan` to represent missing data. It is by default not included in computations. See the Missing Data section.

*Reindexing* allows you to change/add/delete the index on a specified axis. This returns a copy of the data.

* drop any rows that have missing data.

* Filling missing data.

* get the boolean mask where values are nan.

## Operations

### Stats

Operations in general exclude missing data.

* Performing a descriptive statistic

* Same operation on the other axis

* Operating with objects that have different dimensionality and need alignment. In addition, pandas automatically broadcasts along the specified dimension.

### Apply

* Applying functions to the data

### String Methods

Series is equipped with a set of string processing methods in the str attribute that make it easy to operate on each element of the array, as in the code snippet below. Note that pattern-matching in str generally uses regular expressions by default (and in some cases always uses them). See more at Vectorized String Methods.

## Merge

### Concat

pandas provides various facilities for easily combining together Series and DataFrame objects with various kinds of set logic for the indexes and relational algebra functionality in the case of join / merge-type operations.

* Concatenating pandas objects together with `concat()`

> Adding a column to a DataFrame is relatively fast. However, adding a row requires a copy, and may be expensive. We recommend passing a pre-built list of records to the DataFrame constructor instead of building a DataFrame by iteratively appending records to it. See Appending to dataframe for more.

### Join

SQL style merges.

## Grouping

By “group by” we are referring to a process involving one or more of the following steps:

* Splitting the data into groups based on some criteria

* Applying a function to each group independently

* Combining the results into a data structure

## Reshaping

### Stack

* The stack() method “compresses” a level in the DataFrame’s columns.

With a “stacked” DataFrame or Series (having a MultiIndex as the index), the inverse operation of stack() is unstack(), which by default unstacks the last level:

### Pivot tables

* We can produce pivot tables from this data very easily:

## Time series

pandas has simple, powerful, and efficient functionality for performing resampling operations during frequency conversion (e.g., converting secondly data into 5-minutely data). This is extremely common in, but not limited to, financial applications. See the Time Series section.

* Time zone representation:

* Converting to another time zone:

* Converting between time span representations:

* Converting between period and timestamp enables some convenient arithmetic functions to be used.

## Categoricals

pandas can include categorical data in a DataFrame. For full docs, see the categorical introduction and the API documentation.

* Convert the raw grades to a categorical data type.

* Name: grade, dtype: category

* Rename the categories to more meaningful names (assigning to `Series.cat.categories()` is in place!).

* Reorder the categories and simultaneously add the missing categories (methods under Series.cat() return a new Series by default).

* Name: grade, dtype: category

* Sorting is per order in the categories, not lexical order.

* Grouping by a categorical column also shows empty categories.

## Plotting

We use the standard convention for referencing the matplotlib API

## Getting data in/out

### CSV

* Writing to a csv file.

* Reading from a csv file.

* Reading and writing to HDFStores.

### HDF Files

* Writing to a HDF5 Store.

* Reading from a HDF5 Store.

### Excel

* Reading and writing to MS Excel.

* Writing to an excel file.

* Reading from an excel file.
