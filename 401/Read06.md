# Game of Greed

## Random module

Random module provides access to functions that support many operations, and it is used when we want the computer to pick a random number in a given range, pick a random element from a list, pick a random card from a deck, flip a coin, or when making password database more secure or powering a random page on your website.

### Random functions

#### Randit

It is used to generate a random integer, and it accepts two parameters: a lowest and a highest number, the first value should be less than the second.

```python
import random
print(random.randint(0, 5))
```

it will print a number between 0 and 5

#### Random

To get a larger number we multiply it.

```python
import random
print(random.random()*100)
```

here we will get a number between 0 and 100

#### Choice

It generates a random value from a given list.

```python
import random
my_list = [2, 109, False, 10, "Lorem", 482]
random.choice(my_list)
```

#### Shuffle

It shuffles the elements in list in place, so they are in a random order.

```python
from random import shuffle
x = [[i] for i in range(10)]
shuffle(x)
```

it will generate a list of numbers from 0 to 9 sorted in random order.

#### Randrange

Generate a randomly selected element from range (start, stop, step)

```python
import random
print(random.randrange(0, 101, 5))
```

It will generate a number between 0 and 101 with 5 numbers difference.

## Risk Analysis in Software Testing

Risk is the probability of any unwanted incident, and risk analysis is the process of identifying the risks in applications or software that you built and prioritizing them to test.

### Why Risk Analysis

Using software analysis at the beginning of a project highlights the potential problem areas,so it helps the developer and the manager to mitigate the risks.

#### Possible risks one could encounter

1. Use of new hardware.

2. Use of new technology.

3. Use of new automation tool.

4. The sequence of code.

5. Availability of test resources for the application.

#### Unavoidable risks

1. The time allocated for testing.

2. A defect leakage due to the complexity or size of the application.

3. Urgency from the clients to deliver the project.

4. Incomplete requirements.

##### Points to be taken of to tackle the previous situations

* Conduct Risk Assessment review meeting.

* Use maximum resources to work on high-risk areas.

* Create Risk Assessment database for future use.

* Identify and notice the risk magnitude indicators, which are:
    * High, means the effect of the risk would be very high and non-tolerable. The company might face loss.

    * Medium: it is tolerable but not desirable. The company may suffer financially but there is a limited risk.

    * Low: it is tolerable. There lies little or no external exposure or no financial loss.

### Risk Identification

1. Business Risk, it is the most common risk, and it is the risk that comes from the company or the customer rather than the project itself.

2. Testing Risk, you should be well acquainted with the platform you are working on, along with the software testing tools being used.

3. Premature Release Risk, a fair amount of knowledge to analyze the risk associated with releasing unsatisfactory or untested software is required.

4. Software Risks, you should be well versed with the risks associated with the software development process.

### Risk Assessment

![Risk Assessment](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2019/08/Picture1-528x290.png)

#### The perspective of Risk Assessment

There are three perspectives of Risk Assessments:

1. Effect, to assess risk by Effect. In case you identify a condition, event or action and try to determine its impact.

2. Cause, to assess risk by Cause is opposite of by Effect. Initialize scanning the problem and reach to the point that could be the most probable reason behind that.

3. Likelihood, to assess risk by Likelihood is to say that there is a probability that a requirement won’t be satisfied.

### Steps for Risk Analysis

1. Search the risk.

2. Analyze the impact of each individual risk.

3. Measures for the risk identified.

## Big O Notation

It represents how the runtime scales with respect to some input variables.

* If the function checks for a particular value it will be O(N) while N is the size of the array.

```python
for i in list:
    if i == x:
        return True
```

* If the function prints pairs of values in the array, will br O(N^2) while N is the size of the array.

```python
for i in list:
    for j in list:
        print(i, j)
```

We have four important rules to know with Big O:

1. If you have two different steps in you algorithm, you add up those steps.

2. Drop constants, which means that if we have more than one function that has the same big O notation => O(n) + O(n) + O(n) will turn into O(3n) but it will be expressed as O(n) because we shall not include constants.

3. Different variables represent different inputs.

4. Drop non-dominate terms, if we have a function that has O(n) and O(n^2) we drop the O(n) and the Big O notation is O(n^2).