# Debugging
When writing codes in JS it seems impossible to make the right code from the first time, it is like a problem solving language and it can be dealt with like a puzzle, so whenever the code has a problem there are several methods to know what is wrong with it and how to solve it, so first we need to know the order of execution, some tasks cannot complete until another statement or function has been processed.
### Execution contexts 
* Global context 
It is the code that is in the script, and not inside a function, and can be accessed throughout the whole script.
* Function context 
The code that run only within the function
Scopes
* Global scope
It is a variable that is declared outside of a function and can be accessed everywhere.
* Function level scope
Any variable that is declared inside a function and only available inside this function; it will be undefined outside of it. 
The stack
The JS interpreter processes one line of code at a time , and when a statement needs data from another function, it stacks the new function on the top of the current task.
Once the task has been performed, the interpreter can go back to the task in hand.
### Errors
When an error happens, the interpreter stops and looks for exception-handling code .
*Errors* are usually found at the **console** in browsers, so if we have any problem we can *console log* the information we want, and the problem will appear at the **console** of the browser. 
**Consoles** are found in all browsers and they are very helpful tools for error solving and code debugging.
