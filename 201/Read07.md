# Object-Oriented Programming, HTML Tables

## Tables
They are used in most websites, because they make it easier to present complex information.
The tags used to form a table are:
* < table >, it states that we are going to make a table.
* < tr >, indicates the start of each row in the table.
* < th >. it is the heading of the table.
* < td >, every **tr** is followed by several **td**s the **td** indicates the data cell of the table.
We can get a cell along more than one column using *colspan* which is an attribute that usually comes inside a **td**.
We can also have a cell along more than one raw using *rowspan* attribute.
If we have a long table, we can distinguish between its content using < thead >, it will contain the heading of the table, < tbody >, that contains the main data of the table, and < tfoot > has the footer element.
We can modify the appearance of the table we made using CSS.

## Functions
We talked before a lot about functions, here are some points to remember:
* Functions are composed of:
    * The word *function*.
    * The *name* of that function.
    * *Parenthesis* that can be empty, or carry parameters to be used when the function is called.
    * *Curly brackets* that contain the code of the function.
* The function can contain any element or operation inside the JS.
* They are usually used when the operation needs to be applied more than once in the code.
* I n order for the function to run it should be called by; typing the *name* of the *function*, and either empty or valuable  parenthesis.

## Objects
We learned about object with literal notation, and now we are going to talk about ***Constructor Notation***.
Constructor Object is made by naming a variable and adding the word *new*, followed by **Object ()** constructor function.
And the properties are added by typing the name of the object, then period, after that the property we want to add, and it works the same way with methods.
<pre><code>Let hotel = new Object();
                Hotel.name = ‘Quay’;
                Hotel.rooms = 40;
                Hotel.checkAvailability = function() {
	                Return this.rooms – this.booked;
                };</code></pre>
We can leave the object empty the time we form it, because we can update its contents after that only by typing the name of the object followed by *period* then the property we want to add or update, the system will check the content of that object, if there is a value of that property, it will be updated according to the new input, if there is no property, then the new input will be added as new property.
We can delete from the object using the keyword, *delete* followed by the name of the object.the property we want to delete.
Inside an object we can refer to its content using the keyword **this** instead of typing the name of the object.
### Arrays are objects
Arrays can be considered as a special type of an object, because they carry a set of key/value pairs, but the keys are the index number of these values.
An object can carry an array, and an array can carry an object.
### Built in objects
Browsers come with a set of built-in objects that do some default stuff for creating interactive webpages.
There are three groups of built is objects:
#### 1.	Browser Object Model
It creates a model for browser tab or window, and they are the objects that are usually present in all browsers such as *print* property.
#### 2.	Document Object Model
It is the model of the webpage structure that carries the documents type and all the elements in that webpage.
#### 3.	Global JavaScript Objects
They are a group of individual objects that relate to different types of JavaScript language, and they can be *datatypes* or objects that deal with real world concepts.

