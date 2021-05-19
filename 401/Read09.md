# Dunder Methods & Probability

## Dunder Methods

Dunder are special methods that used to enrich calsses, and they are sometimes called magic methods. They lest you emulate the behavior of built in types.

We can use Dunder methods to do the following:

### Object initialization: __init__

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

it allows us to create a new class instance.

### Object Representation: __str__, __repr__

They provide a string representation of the object

1. __repr__: it is the official representation of the objects.

2. __str__(): The informal or nicely printable string representation of an object.

### Iteration: __len__, __getitem__, __reversed__

#### __len__

it is used to get the length of an object

#### __reversed__

to iterates over an object by reverse

### Operator Overloading for Comparing Accounts: __eq__, __lt__

### Operator Overloading for Merging Accounts: __add__

### Callable Python Objects: __call__

### Context Manager Support and the With Statement: __enter__, __exit__


## probability

An event is some outcome of interest.
Probability seeks to answer the question "What is the chance of an event happening?"

### From statistics to probability

we can have an example of tossing a coin 10 times and counting how many times we get heads, we can use the following function:

```python
import random
def coin_trial():
heads = 0
for i in range(100):
    if random.random() <= 0.5:
        heads +=1
    return heads
def simulate(n):
    trials = []
    for i in range(n):
        trials.append(coin_trial())
    return(sum(trials)/n)
simulate(10)
>>> 5.4
simulate(100)
>>> 4.83
simulate(1000)
>>> 5.055
simulate(1000000)
>>> 4.999781
```

### Revisiting the normal

The normal distribution is significant to probability and statistic thanking to some factors factors:

* Central limit theorem, which indicates that for larger the assumption count, the more normal the probability becomes.

* Three Sigma Rule, it is an expression of how many of our observations fall within a certain distance of the mean.

* Z-score, it is a simple calculation that answers the question, “**Given a data point, how many standard deviations is it away from the mean?**”, and it can be shown by the following equation:

![z-score](https://i.imgur.com/3TuDF4G.jpeg)