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

