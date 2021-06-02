# Regular Expression and shutil

Regular Expressions (Regex) are a sequence of characters that checks whether a pattern exists in a specific string.

## Regular expressions in python

Regular expressions are supported by the `re` module in python, so in order to use it we should do:
`import re`

### Basic Patterns: Ordinary Characters

Ordinary characters are the simplest regular expressions. They match themselves exactly and do not have a special meaning in their regular expression syntax, e.g.

```python
pattern = r"Cookie"
sequence = "Cookie"
if re.match(pattern, sequence):
    print("Match!")
else: print("Not a match!")
```

here the result will be `Match!`
The `r` in the previous code is a **raw string literal**, It changes how the string literal is interpreted.

### Wild Card Characters: Special Characters

Special characters are characters that do not match themselves as seen but have a special meaning when used in a regular expression.

* . - A period. Matches any single character except the newline character.

* ^ - A caret. Matches the start of the string.

* $ - Matches the end of string.

* [abc] - Matches a or b or c.
[a-zA-Z0-9] - Matches any letter from (a to z) or (A to Z) or (0 to 9).

* \ - Backslash.
If the character following the backslash is a recognized escape character, then the special meaning of the term is taken,
Else if the character following the \ is not a recognized escape character, then the \ is treated like any other character and passed through.
\ can be used in front of all the metacharacters to remove their special meaning.

* \w - Lowercase 'w'. Matches any single letter, digit, or underscore.
\W - Uppercase 'W'. Matches any character not part of \w (lowercase w).

* \s - Lowercase 's'. Matches a single whitespace character like: space, newline, tab, return.
\S - Uppercase 'S'. Matches any character not part of \s (lowercase s).

* \d - Lowercase d. Matches decimal digit 0-9.
\D - Uppercase d. Matches any character that is not a decimal digit.

* \t - Lowercase t. Matches tab.

* \n - Lowercase n. Matches newline.

* \r - Lowercase r. Matches return.

* \A - Uppercase a. Matches only at the start of the string. Works across multiple lines as well.

* \Z - Uppercase z. Matches only at the end of the string.

* \b - Lowercase b. Matches only the beginning or end of the word.

### Repetitions

* + - Checks if the preceding character appears one or more times starting from that position.

* * - Checks if the preceding character appears zero or more times starting from that position.

* ? - Checks if the preceding character appears exactly zero or one time starting from that position.

* {x} - Repeat exactly x number of times.
{x,} - Repeat at least x times or more.
{x, y} - Repeat at least x times but no more than y times.

### Function provided by 're'

#### compile(pattern, flags=0)

With `compile()`, you can computer a regular expression pattern into a regular expression object.
When you need to use an expression several times in a single program, using compile() to save the resulting regular expression object for reuse is more efficient than saving it as a string. This is because the compiled versions of the most recent patterns passed to compile() and the module-level matching functions are cached.

#### search(pattern, string, flags=0)

With this function, you scan through the given string/sequence, looking for the first location where the regular expression produces a match. It returns a corresponding match object if found, else returns None if no position in the string matches the pattern. Note that None is different from finding a zero-length match at some point in the string.

#### match(pattern, string, flags=0)

Returns a corresponding match object if zero or more characters at the beginning of string match the pattern. Else it returns None, if the string does not match the given pattern.

#### findall(pattern, string, flags=0)

finds all the possible matches in the entire sequence and returns them as a list of strings. Each returned string represents one match.

#### finditer(string, [position, end_position])

similar to findall() - it finds all the possible matches in the entire sequence but returns regex match objects as an iterator.

#### sub(pattern, repl, string, count=0, flags=0)

sub() is the substitute function. It returns the string obtained by replacing or substituting the leftmost non-overlapping occurrences of pattern in string by the replacement repl. If the pattern is not found, then the string is returned unchanged.

#### subn(pattern, repl, string, count=0)

he subn() is similar to sub(). However, it returns a tuple containing the new string value and the number of replacements that were performed in the statement.

### split(string, [maxsplit = 0])

This splits the strings wherever the pattern matches and returns a list. If the optional argument maxsplit is nonzero, then the maximum 'maxsplit' number of splits are performed.

* start() - Returns the starting index of the match.
* end() - Returns the index where the match ends.
* span() - Return a tuple containing the (start, end) positions of the match.

### Compilation Flags

An expression's behavior can be modified by specifying a flag value. You can add flags as an extra argument to the different functions that you have seen in this tutorial. Some of the more useful ones are:

* IGNORECASE (I) - Allows case-insensitive matches.
* DOTALL (S) - Allows . to match any character, including newline.
* MULTILINE (M) - Allows start of string (^) and end of string ($) anchor to match newlines as well.
* VERBOSE (X) - Allows you to write whitespace and comments within a regular expression to make it more readable.

## Shutil-High-level File Operator

The shutil module includes high-level file operations such as copying and archiving.

### Copying Files

copyfile() copies the contents of the source to the destination and raises IOError if it does not have permission to write to the destination file.

```python
import glob
import shutil

print('BEFORE:', glob.glob('shutil_copyfile.*'))

shutil.copyfile('shutil_copyfile.py', 'shutil_copyfile.py.copy')

print('AFTER:', glob.glob('shutil_copyfile.*'))
```

Result:

```shell
$ python3 shutil_copyfile.py

BEFORE: ['shutil_copyfile.py']
AFTER: ['shutil_copyfile.py', 'shutil_copyfile.py.copy']
```

## Copying File Metadata

By default when a new file is created under Unix, it receives permissions based on the umask of the current user. To copy the permissions from one file to another, use copymode().

```python

import os
import shutil
import subprocess

with open('file_to_change.txt', 'wt') as f:
    f.write('content')
os.chmod('file_to_change.txt', 0o444)

print('BEFORE:', oct(os.stat('file_to_change.txt').st_mode))

shutil.copymode('shutil_copymode.py', 'file_to_change.txt')

print('AFTER :', oct(os.stat('file_to_change.txt').st_mode))
```

result: 

```shell
$ python3 shutil_copymode.py

BEFORE: 0o100444
AFTER : 0o100644
```

## Working With Directory Trees

shutil includes three functions for working with directory trees. To copy a directory from one place to another, use copytree(). It recurses through the source directory tree, copying files to the destination. The destination directory must not exist in advance.

```python
import glob
import pprint
import shutil

print('BEFORE:')
pprint.pprint(glob.glob('/tmp/example/*'))

shutil.copytree('../shutil', '/tmp/example')

print('\nAFTER:')
pprint.pprint(glob.glob('/tmp/example/*'))
```

## Finding Files

The which() function scans a search path looking for a named file. The typical use case is to find an executable program on the shell’s search path defined in the environment variable PATH.

```python
import shutil

print(shutil.which('virtualenv'))
print(shutil.which('tox'))
print(shutil.which('no-such-program'))
```

result:

```shell
$ python3 shutil_which.py

/Users/dhellmann/Library/Python/3.5/bin/virtualenv
/Users/dhellmann/Library/Python/3.5/bin/tox
None
```

## Archives

Python’s standard library includes many modules for managing archive files such as tarfile and zipfile. There are also several higher-level functions for creating and extracting archives in shutil. get_archive_formats() returns a sequence of names and descriptions for formats supported on the current system.

```python
import shutil

for format, description in shutil.get_archive_formats():
    print('{:<5}: {}'.format(format, description))
```

result:

```shell
$ python3 shutil_get_archive_formats.py

bztar: bzip2'ed tar-file
gztar: gzip'ed tar-file
tar  : uncompressed tar file
xztar: xz'ed tar-file
zip  : ZIP file
```

```python
shutil_make_archive.py
import logging
import shutil
import sys
import tarfile

logging.basicConfig(
    format='%(message)s',
    stream=sys.stdout,
    level=logging.DEBUG,
)
logger = logging.getLogger('pymotw')

print('Creating archive:')
shutil.make_archive(
    'example', 'gztar',
    root_dir='..',
    base_dir='shutil',
    logger=logger,
)

print('\nArchive contents:')
with tarfile.open('example.tar.gz', 'r') as t:
    for n in t.getnames():
        print(n)
```

result:

```shell
$ python3 shutil_make_archive.py

Creating archive:
changing into '..'
Creating tar archive
changing back to '...'

Archive contents:
shutil
shutil/config.ini
shutil/example.out
shutil/file_to_change.txt
shutil/index.rst
shutil/shutil_copy.py
shutil/shutil_copy2.py
shutil/shutil_copyfile.py
shutil/shutil_copyfileobj.py
shutil/shutil_copymode.py
shutil/shutil_copystat.py
shutil/shutil_copytree.py
shutil/shutil_copytree_verbose.py
shutil/shutil_disk_usage.py
shutil/shutil_get_archive_formats.py
shutil/shutil_get_unpack_formats.py
shutil/shutil_make_archive.py
shutil/shutil_move.py
shutil/shutil_rmtree.py
shutil/shutil_unpack_archive.py
shutil/shutil_which.py
shutil/shutil_which_regular_file.py
```

## File System Space

It can be useful to examine the local file system to see how much space is available before performing a long running operation that may exhaust that space. disk_usage() returns a tuple with the total space, the amount currently being used, and the amount remaining free.

```python
import shutil

total_b, used_b, free_b = shutil.disk_usage('.')

gib = 2 ** 30  # GiB == gibibyte
gb = 10 ** 9   # GB == gigabyte

print('Total: {:6.2f} GB  {:6.2f} GiB'.format(
    total_b / gb, total_b / gib))
print('Used : {:6.2f} GB  {:6.2f} GiB'.format(
    used_b / gb, used_b / gib))
print('Free : {:6.2f} GB  {:6.2f} GiB'.format(
    free_b / gb, free_b / gib))
```

Result:

```shell
$ python3 shutil_disk_usage.py

Total: 499.42 GB  465.12 GiB
Used : 246.68 GB  229.73 GiB
Free : 252.48 GB  235.14 GiB
```