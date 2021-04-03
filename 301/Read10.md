# Call stack & Error Messages
## Call Stack
Call stack is a mechanism for the interpreter to keep track for all the functions that that are being run and and what functions are being called from inside a function, it runs as follows:
* When the interpreter goes across a function, it adds that function to the call stack then starts carrying it out.
* Any function called inside this function is added to the stack and run where it's call is reached.
* When the current function is finished, the interpreter takes it off the stack and resumes execution where it left off in the last code listing.
* If the stack takes up more space than it had assigned to it, it results in a "stack overflow" error.
Call stack follows **LIFO** principle *Last in* is *First out* which means when the interpreter adds a function to the stack, it adds it to the top the then the functions are processed from the top to the button, and in the stack, the parameters are added to the call stack, and form a *stack frame*; which is a temporary memory location that will be cleared when the function returns.
### Stack overflow 
Stack overflow happens when a recursive function (a function that calls itself) runs without exit point; here the browser will keep calling it until the stack limit is reached, then it will throw a stack overflow error, as the following example:

```
function callMyself(){
    callMyself();
}
callMyself();
```
the result will be :

![](https://i.ibb.co/0ZX83ck/stack-overflow.png)

## Error Messages
### Types of errors:
* Reference error, this error comes when a variable is used but not declared, or is declared after the use when declared by *const* and *let*.
* Syntax error, when you have something that cannot be parsed in terms of syntax, such as when trying to JSON.parse, invalid object.
* Range errors, when trying to manipulate object with some kind of length and give it invalid length.
* Type errors, when the types you are trying to access or use are incompatible.
    


