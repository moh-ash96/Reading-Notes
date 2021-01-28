# Operators and Loops
## Comparison operators
### Evaluating conditions 
This operator allows evaluating condition by comparing between one value in the script to something you expect might be the same, and the result will be Boolean, and these operators include:
* ==  **Equal to**
This operator compares two values to see if they are the same.
e.g. ‘Hello’ == ‘Goodbye’ will return *false*, because they are not the same,
while ‘Hello’ == ‘Hello’ will return *true*
* === **Strict equal to**
This operator compares two values to see if they have the same type and data.
e.g. ‘3’ === 3 will return *false*, because they are not the same type,
while 3 === 3 will return *true*, they have the same type and data.
* != **Not equal to**
This operation compares two values to see if they are not the same.
e.g. ‘Hello’ != ‘Goodbye’ will return *true*, because they are not the same,
while ‘Hello’ != ‘Hello’ are the same, so the return will be *false*
* !== **Strict not equal to**
It checks if both data and value are not the same.
e.g. ‘3’ !== 3 will return *true* , because they are not the same in data and value,
while ‘3’ !== ‘3’ are the same data and value, so the return will be *false*
* ">" **Greater than**
Check if the number on the left is greater than the number on the right.
* "<" **Less than**
Checks if the number on the left is less than the one on the right.
* ">=" **Greater or equal**
Checks if the number on the left is greater or equal to number on the right.
* "<=" **Less or equal**
Checks if the number on the left is less or equal to the number on the right.

## Logical operators
They are used to compare two comparison operators and the result will be either *true* , or *false*
* && **Logical and**
It check if both operators on it’s left and right are true; if they are, the result is *true*, if one or both are false, then the result will be *false*,
* || **Logical or**
It checks if one pf the operators we are comparing is true; if one operator is *true* then the result will be true, and the *false* result will appear only if both operations are *false*
* ! **Logical not**
it takes a Boolean value and inverts it; if the value was *true* before adding the ! the return will be *false*, while if it was *false* before the ! the result will be *true*

## Loops
The loop checks the condition, if it is *true* so the program will run, and then it will check again, if also *true* it will run, and so on until it checks *false* then the program will be stopped.
There are three common types of loops:
1. For
When you need to run a code for a specific number of times, the loop *for* is here for you because it counts how many times the loop should run.
2. While
Here the condition is something other than counter so it will keep running until the return is not *true*
3. Do while
It is similar to **while** but if you put a statement in {} , it will run it at least once, even if the return is false.
We can do the **for** loop by following these steps
* Initialization
Creating a variable and setting it as *ZERO*, and it is usually called **i** , it acts as a counter and it looks like this
Var i = 0;
* Condition
We set a specific value for the counter to reach and stop counting 
e.g. i < 10; here the counter will continue until it reaches 10
we can give a variable to the condition using *var* and calling what we want 
e.g. var rounds = 3;
the condition will be i < (rounds);
* Update
We put in it what will change in every loop.
e.g. we can use **i++** to add one at every loop, or **i--** to have the loop countdown.
So the whole code will be 
for ***( var i = 0; i < 10; i++) { the code will be here }***
