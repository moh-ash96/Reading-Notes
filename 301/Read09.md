# Refactoring Functions

Refactorin functions, means taking a function and modifying it to be more useful, more readable, and with less lines written.
## Pure functions:
 It is the function that returns the same result if given the same arguments, and doesn't cause any abservable side effects.
 ### What makes a function as impure:
 * **Reading externale files**, because the files contents can e changed as the following example:
 ```
 const charactersCounter = (text) => `Character count: ${text.length}`;

function analyzeFile(filename) {
  let fileContent = open(filename);
  return charactersCounter(fileContent);
}
```
* **Random number generation**
* **Modifyong a global Object or a parameter passed by referance**

### Pure function benefits
* **Immutability**, which is unchanging over time or unable to be changed.
* **Referential transparency**, Giving the same result for the same input.
* **Functions as firs class entities**, When the funvtion is pure, we can use it as a variable and we can cridict what the outcome would be, so we can call it in another func
### Examples of pure functions
* **Higher-order functions**, It is a function that takes one or more functions as arguments, or returns a function as a result.
* **Filter**, it expects *true* or *false* values to determine if the value should be included in the result collection.
* **Map**, it transformes a collection by applying a function to all of its elements and building a new collection from the returned values.
* **Reduce**, it recives a collection and returns a value created by combining the items.

