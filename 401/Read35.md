# Pythonisms

In Python, special methods are a set of predefined methods you can use to enrich your classes. They are easy to recognize because they start and end with double underscores, for example `__init__` or `__str__`.

## Dunder Methods

### Object Initialization __init__

Right upon starting my class I already need a special method. To construct account objects from the Account class I need a constructor which in Python is the __init__ dunder:

```python
class Account:
    """A simple account class"""

    def __init__(self, owner, amount=0):
        """
        This is the constructor that lets us create
        objects from this class
        """
        self.owner = owner
        self.amount = amount
        self._transactions = []
```

The constructor takes care of setting up the object. In this case it receives the owner name, an optional start amount and defines an internal transactions list to keep track of deposits and withdrawals.

This allows us to create new accounts like this:

```python
>>> acc = Account('bob')  # default amount = 0
>>> acc = Account('bob', 10)
```

### Object Representation __str__,__repr__

It’s common practice in Python to provide a string representation of your object for the consumer of your class (a bit like API documentation.) There are two ways to do this using dunder methods:

1. `__repr__`: The “official” string representation of an object. This is how you would make an object of the class. The goal of __repr__ is to be unambiguous.

2. `__str__`: The “informal” or nicely printable string representation of an object. This is for the enduser.

Let’s implement these two methods on the Account class:

```python
class Account:
    # ... (see above)

    def __repr__(self):
        return 'Account({!r}, {!r})'.format(self.owner, self.amount)

    def __str__(self):
        return 'Account of {} with starting amount: {}'.format(
            self.owner, self.amount)
```

If you don’t want to hardcode "Account" as the name for the class you can also use `self.__class__.__name__` to access it programmatically.

If you wanted to implement just one of these to-string methods on a Python class, make sure it’s `__repr__`.

Now I can query the object in various ways and always get a nice string representation:

```python
>>> str(acc)
'Account of bob with starting amount: 10'

>>> print(acc)
"Account of bob with starting amount: 10"

>>> repr(acc)
"Account('bob', 10)"
```

### Iteration: __len__, __getitem__, __reversed__

In order to iterate over our account object I need to add some transactions. So first, I’ll define a simple method to add transactions. I’ll keep it simple because this is just setup code to explain dunder methods, and not a production-ready accounting system:

```python
def add_transaction(self, amount):
    if not isinstance(amount, int):
        raise ValueError('please use int for amount')
    self._transactions.append(amount)
```

I also defined a property to calculate the balance on the account so I can conveniently access it with account.balance. This method takes the start amount and adds a sum of all the transactions:

```python
@property
def balance(self):
    return self.amount + sum(self._transactions)
```

Let’s do some deposits and withdrawals on the account:

```python
>>> acc = Account('bob', 10)

>>> acc.add_transaction(20)
>>> acc.add_transaction(-10)
>>> acc.add_transaction(50)
>>> acc.add_transaction(-20)
>>> acc.add_transaction(30)

>>> acc.balance
80
```

Now I have some data and I want to know:

How many transactions were there?

Index the account object to get transaction number …

Loop over the transactions

With the class definition I have this is currently not possible. All of the following statements raise TypeError exceptions:

```python
>>> len(acc)
TypeError

>>> for t in acc:
...    print(t)
TypeError

>>> acc[1]
TypeError
```

Dunder methods to the rescue! It only takes a little bit of code to make the class iterable:

```python
class Account:
    # ... (see above)

    def __len__(self):
        return len(self._transactions)

    def __getitem__(self, position):
        return self._transactions[position]
```

Now the previous statements work:

```python

>>> len(acc)
5

>>> for t in acc:
...    print(t)
20
-10
50
-20
30

>>> acc[1]
-10
```

To iterate over transactions in reversed order you can implement the __reversed__ special method:

```python
def __reversed__(self):
    return self[::-1]

>>> list(reversed(acc))
[30, -20, 50, -10, 20]
```

To reverse the list of transactions I used Python’s reverse list slice syntax. I also had to wrapp the result of reversed(acc) in a list() call because reversed() returns a a reverse iterator, not a list object we can print nicely in the REPL. Check out this tutorial on iterators in Python if you’d like to learn more about how this approach works in detail.

All in all, this account class is starting to look quite Pythonic to me now.

Operator Overloading for Comparing Accounts: __eq__, __lt__
We all write dozens of statements daily to compare Python objects:

```python
>>> 2 > 1
True

>>> 'a' > 'b'
False
```

This feels completely natural, but it’s actually quite amazing what happens behind the scenes here. Why does > work equally well on integers, strings and other objects (as long as they are the same type)? This polymorphic behavior is possible because these objects implement one or more comparison dunder methods.

An easy way to verify this is to use the dir() builtin:

```python
>>> dir('a')
['__add__',
...
'__eq__',    <---------------
'__format__',
'__ge__',    <---------------
'__getattribute__',
'__getitem__',
'__getnewargs__',
'__gt__',    <---------------
...]
```

Let’s build a second account object and compare it to the first one (I am adding a couple of transactions for later use):

```python
>>> acc2 = Account('tim', 100)
>>> acc2.add_transaction(20)
>>> acc2.add_transaction(40)
>>> acc2.balance
160

>>> acc2 > acc
TypeError:
"'>' not supported between instances of 'Account' and 'Account'"
```

What happened here? We got a TypeError because I have not implemented any comparison dunders nor inherited them from a parent class.

Let’s add them. To not have to implement all of the comparison dunder methods, I use the functools.total_ordering decorator which allows me to take a shortcut, only implementing __eq__ and __lt__:

from functools import total_ordering

```python
@total_ordering
class Account:
    # ... (see above)

    def __eq__(self, other):
        return self.balance == other.balance

    def __lt__(self, other):
        return self.balance < other.balance
```

And now I can compare Account instances no problem:

```python
>>> acc2 > acc
True

>>> acc2 < acc
False

>>> acc == acc2
False
```

Operator Overloading for Merging Accounts: __add__
In Python, everything is an object. We are completely fine adding two integers or two strings with the + (plus) operator, it behaves in expected ways:

```python
>>> 1 + 2
3

>>> 'hello' + ' world'
'hello world'
```

Again, we see polymorphism at play: Did you notice how + behaves different depending the type of the object? For integers it sums, for strings it concatenates. Again doing a quick dir() on the object reveals the corresponding “dunder” interface into the data model:

```python
>>> dir(1)
[...
'__add__',
...
'__radd__',
...]
```

Our Account object does not support addition yet, so when you try to add two instances of it there’s a TypeError:

```shell
>>> acc + acc2
TypeError: "unsupported operand type(s) for +: 'Account' and 'Account'"
```

Let’s implement __add__ to be able to merge two accounts. The expected behavior would be to merge all attributes together: the owner name, as well as starting amounts and transactions. To do this we can benefit from the iteration support we implemented earlier:

```python
def __add__(self, other):
    owner = '{}&{}'.format(self.owner, other.owner)
    start_amount = self.amount + other.amount
    acc = Account(owner, start_amount)
    for t in list(self) + list(other):
        acc.add_transaction(t)
    return acc
```

Yes, it is a bit more involved than the other dunder implementations so far. It should show you though that you are in the driver’s seat. You can implement addition however you please. If we wanted to ignore historic transactions—fine, you can also implement it like this:

```python
def __add__(self, other):
    owner = self.owner + other.owner
    start_amount = self.balance + other.balance
    return Account(owner, start_amount)
```

I think the former implementation would be more realistic though, in terms of what a consumer of this class would expect to happen.

Now we have a new merged account with starting amount $110 (10 + 100) and balance of $240 (80 + 160):

```python
>>> acc3 = acc2 + acc
>>> acc3
Account('tim&bob', 110)

>>> acc3.amount
110
>>> acc3.balance
240
>>> acc3._transactions
[20, 40, 20, -10, 50, -20, 30]
```

Note this works in both directions because we’re adding objects of the same type. In general, if you would add your object to a builtin (int, str, …) the __add__ method of the builtin wouldn’t know anything about your object. In that case you need to implement the reverse add method (__radd__) as well. You can see an example for that here.

### Callable Python Objects: __call__

You can make an object callable like a regular function by adding the __call__ dunder method. For our account class we could print a nice report of all the transactions that make up its balance:

```python
class Account:
    # ... (see above)

    def __call__(self):
        print('Start amount: {}'.format(self.amount))
        print('Transactions: ')
        for transaction in self:
            print(transaction)
        print('\nBalance: {}'.format(self.balance))
```

Now when I call the object with the double-parentheses acc() syntax, I get a nice account statement with an overview of all transactions and the current balance:

```python
>>> acc = Account('bob', 10)
>>> acc.add_transaction(20)
>>> acc.add_transaction(-10)
>>> acc.add_transaction(50)
>>> acc.add_transaction(-20)
>>> acc.add_transaction(30)

>>> acc()
Start amount: 10
Transactions:
20
-10
50
-20
30
Balance: 80
```

Please keep in mind that this is just a toy example. A “real” account class probably wouldn’t print to the console when you use the function call syntax on one of its instances. In general, the downside of having a __call__ method on your objects is that it can be hard to see what the purpose of calling the object is.

Most of the time it’s therefore better to add an explicit method to the class. In this case it probably would’ve been more transparent to have a separate Account.print_statement() method.

Context Manager Support and the With Statement: __enter__, __exit__
My final example in this tutorial is about a slightly more advanced concept in Python: Context managers and adding support for the with statement.

Now, what is a “context manager” in Python? Here’s a quick overview:

A context manager is a simple “protocol” (or interface) that your object needs to follow so it can be used with the with statement. Basically all you need to do is add __enter__ and __exit__ methods to an object if you want it to function as a context manager.

Let’s use context manager support to add a rollback mechanism to our Account class. If the balance goes negative upon adding another transaction we rollback to the previous state.

We can leverage the Pythonic with statement by adding two more dunder methods. I’m also adding some print calls to make the example clearer when we demo it:

```python
class Account:
    # ... (see above)

    def __enter__(self):
        print('ENTER WITH: Making backup of transactions for rollback')
        self._copy_transactions = list(self._transactions)
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        print('EXIT WITH:', end=' ')
        if exc_type:
            self._transactions = self._copy_transactions
            print('Rolling back to previous transactions')
            print('Transaction resulted in {} ({})'.format(
                exc_type.__name__, exc_val))
        else:
            print('Transaction OK')
```

As an exception has to be raised to trigger a rollback, I define a quick helper method to validate the transactions in an account:

```python
def validate_transaction(acc, amount_to_add):
    with acc as a:
        print('Adding {} to account'.format(amount_to_add))
        a.add_transaction(amount_to_add)
        print('New balance would be: {}'.format(a.balance))
        if a.balance < 0:
            raise ValueError('sorry cannot go in debt!')
```

Now I can use an Account object with the with statement. When I make a transaction to add a positive amount, all is good:

```python
acc4 = Account('sue', 10)

print('\nBalance start: {}'.format(acc4.balance))
validate_transaction(acc4, 20)

print('\nBalance end: {}'.format(acc4.balance))
```

Executing the above Python snippet produces the following printout:

Balance start: 10
ENTER WITH: Making backup of transactions for rollback
Adding 20 to account
New balance would be: 30
EXIT WITH: Transaction OK
Balance end: 30
However when I try to withdraw too much money, the code in __exit__ kicks in and rolls back the transaction:

```python
acc4 = Account('sue', 10)

print('\nBalance start: {}'.format(acc4.balance))
try:
    validate_transaction(acc4, -50)
except ValueError as exc:
    print(exc)

print('\nBalance end: {}'.format(acc4.balance))
```

In this case we get a different result:

Balance start: 10
ENTER WITH: Making backup of transactions for rollback
Adding -50 to account
New balance would be: -40
EXIT WITH: Rolling back to previous transactions
ValueError: sorry cannot go in debt!
Balance end: 10

## Iteration

### Python Iterators That Iterate Forever

Create a class that demonstrates the bare-bones iterator protocol in Python.

```python
class Repeater:
    def __init__(self, value):
        self.value = value

    def __iter__(self):
        return RepeaterIterator(self)
```

RepeaterIterator object is a helper class we also need to define for our for-in iteration example to work

```python
class RepeaterIterator:
    def __init__(self, source):
        self.source = source

    def __next__(self):
        return self.source.value
```

### How do for-in loops work in Python

Now, what does this for-in loop really do behind the scenes? How does it communicate with the repeater object to fetch new elements from it?

To dispel some of that “magic” we can expand this loop into a slightly longer code snippet that gives the same result:

```python
repeater = Repeater('Hello')
iterator = repeater.__iter__()
while True:
    item = iterator.__next__()
    print(item)
```

As you can see, the for-in was just syntactic sugar for a simple while loop:

* It first prepared the repeater object for iteration by calling its __iter__ method. This returned the actual iterator object.
* After that, the loop repeatedly calls the iterator object’s __next__ method to retrieve values from it.

### A Simpler Iterator Class

```python
class Repeater:
    def __init__(self, value):
        self.value = value

    def __iter__(self):
        return self

    def __next__(self):
        return self.value
```

We just went from two separate classes and 10 lines of code to to just one class and 7 lines of code.

## Python generators

### Python Generators 101 – The Basics

Let’s start by looking again at the Repeater example that I previously used to introduce the idea of iterators. It implemented a class-based iterator cycling through an infinite sequence of values.

This is what the class looked like in its second (simplified) version:

```python
class Repeater:
    def __init__(self, value):
        self.value = value

    def __iter__(self):
        return self

    def __next__(self):
        return self.value
```

If you’re thinking, “that’s quite a lot of code for such a simple iterator,” you’re absolutely right. Parts of this class seem rather formulaic, as if they would be written in exactly the same way from one class-based iterator to the next.

This is where Python’s generators enter the scene. If I rewrite this iterator class as a generator, it looks like this:

```python
def repeater(value):
    while True:
        yield value
```

We just went from seven lines of code to three.

Not bad, eh? As you can see, generators look like regular functions but instead of using the return statement, they use yield to pass data back to the caller.

Will this new generator implementation still work the same way as our class-based iterator did? Let’s bust out the for-in loop test to find out:

```python
>>> for x in repeater('Hi'):
...    print(x)
'Hi'
'Hi'
'Hi'
'Hi'
'Hi'
...
```

Yep! We’re still looping through our greetings forever. This much shorter generator implementation seems to perform the same way that the Repeater class did.

(Remember to hit Ctrl+C if you want out of the infinite loop in an interpreter session.)

Now, how do these generators work? They look like normal functions, but their behavior is quite different. For starters, calling a generator function doesn’t even run the function. It merely creates and returns a generator object:

```python
>>> repeater('Hey')
<generator object repeater at 0x107bcdbf8>
```

The code in the generator function only executes when next() is called on the generator object:

```python
>>> generator_obj = repeater('Hey')
>>> next(generator_obj)
'Hey'
```

If you read the code of the repeater function again, it looks like the yield keyword in there somehow stops this generator function in mid-execution and then resumes it at a later point in time:

```python
def repeater(value):
    while True:
        yield value
```

And that’s quite a fitting mental model for what happens here. You see, when a return statement is invoked inside a function, it permanently passes control back to the caller of the function. When a yield is invoked, it also passes control back to the caller of the function—but it only does so temporarily.

Whereas a return statement disposes of a function’s local state, a yield statement suspends the function and retains its local state.

In practical terms, this means local variables and the execution state of the generator function are only stashed away temporarily and not thrown out completely.

Execution can be resumed at any time by calling next() on the generator:

```python
>>> iterator = repeater('Hi')
>>> next(iterator)
'Hi'
>>> next(iterator)
'Hi'
>>> next(iterator)
'Hi'
```

This makes generators fully compatible with the iterator protocol. For this reason, I like to think of them primarily as syntactic sugar for implementing iterators.

You’ll find that for most types of iterators, writing a generator function will be easier and more readable than defining a long-winded class-based iterator.

### Python Generators That Stop Generating

In this tutorial we started out by writing an infinite generator once again. By now you’re probably wondering how to write a generator that stops producing values after a while, instead of going on and on forever.

Remember, in our class-based iterator we were able to signal the end of iteration by manually raising a StopIteration exception. Because generators are fully compatible with class-based iterators, that’s still what happens behind the scenes.

Thankfully, as programmers we get to work with a nicer interface this time around. Generators stop generating values as soon as control flow returns from the generator function by any means other than a yield statement. This means you no longer have to worry about raising StopIteration at all!

Here’s an example:

```python
def repeat_three_times(value):
    yield value
    yield value
    yield value
```

Notice how this generator function doesn’t include any kind of loop. In fact it’s dead simple and only consists of three yield statements. If a yield temporarily suspends execution of the function and passes back a value to the caller, what will happen when we reach the end of this generator?

Let’s find out:

```python
>>> for x in repeat_three_times('Hey there'):
...     print(x)
'Hey there'
'Hey there'
'Hey there'
```

As you may have expected, this generator stopped producing new values after three iterations. We can assume that it did so by raising a StopIteration exception when execution reached the end of the function.

But to be sure, let’s confirm that with another experiment:

```python
>>> iterator = repeat_three_times('Hey there')
>>> next(iterator)
'Hey there'
>>> next(iterator)
'Hey there'
>>> next(iterator)
'Hey there'
>>> next(iterator)
StopIteration
>>> next(iterator)
StopIteration
```

This iterator behaved just like we expected. As soon as we reach the end of the generator function, it keeps raising StopIteration to signal that it has no more values to provide.

Let’s come back to another example from my Python iterators tutorials. The BoundedIterator class implemented an iterator that would only repeat a value a set number of times:

```python
class BoundedRepeater:
    def __init__(self, value, max_repeats):
        self.value = value
        self.max_repeats = max_repeats
        self.count = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.count >= self.max_repeats:
            raise StopIteration
        self.count += 1
        return self.value
```

Why don’t we try to re-implement this BoundedRepeater class as a generator function. Here’s my first take on it:

```python
def bounded_repeater(value, max_repeats):
    count = 0
    while True:
        if count >= max_repeats:
            return
        count += 1
        yield value
```

I intentionally made the while loop in this function a little unwieldy. I wanted to demonstrate how invoking a return statement from a generator causes iteration to stop with a StopIteration exception. We’ll soon clean up and simplify this generator function some more, but first let’s try out what we’ve got so far:

```python
>>> for x in bounded_repeater('Hi', 4):
...     print(x)
'Hi'
'Hi'
'Hi'
'Hi'
```

Great! Now we have a generator that stops producing values after a configurable number of repetitions. It uses the yield statement to pass back values until it finally hits the return statement and iteration stops.

Like I promised you, we can further simplify this generator. We’ll take advantage of the fact that Python adds an implicit return None statement to the end of every function. This is what our final implementation looks like:

```python
def bounded_repeater(value, max_repeats):
    for i in range(max_repeats):
        yield value
```

Feel free to confirm that this simplified generator still works the same way. All things considered, we went from a 12-line iterator in the BoundedRepeater class to a three-line generator-based implementation providing the same functionality.

That’s a 75% reduction in the number of lines of code—not too shabby!

Generator functions are a great feature in Python, and you shouldn’t hesitate to use them in your own programs.

As you just saw, generators help you “abstract away” most of the boilerplate code otherwise needed when writing class-based iterators. Generators can make your life as a Pythonista much easier and allow you to write cleaner, shorter, and more maintainable iterators.
