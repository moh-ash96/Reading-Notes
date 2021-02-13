# Objects, and the DOM
## Objects:
An object is a set of variables and functions that create a model to be used in the real world.
In objects we have two elements:
1.	Variable, which is called here a **Property** and it can be string, number, Boolean, array, or another object.
2.	Function, which is called here a **Method**.
Each property and method should be named like other variables and each name is called, a ***Key***, the object can’t have two keys with the same name.
To create an object we have to give it a name, considering it a variable, and its contents are contained in curly brackets, then we put the *property name* followed by a colon followed by a method and each property and method are separated by a comma.
To access a property or method of any object, we call the name of the object followed by a period, then the name of the property or method we want to diplay.
## Document Object Model ( DOM )
The document object model specifies how browser should create a model for HTML PAGE AND HOW JavaScript should reach its content an update it.
The DOM tree consists of:
* Document Node, which carries the whole document.
* Element Node, it has the elements of HTML.
* Attribute Node, access the attribute of any element.
* Text Node, to access the text content of the element.
We can access any element by:
*   <pre><code>getElementById()</code></pre>
*   <pre><code>querySelector()</code></pre>, it uses CSSselector.
* Or by going from an element to another upon the DOM tree.
And we can select multiple elements by:
*   <pre><code>getElementByClassName()</code></pre>
*   <pre><code>getElementByTagName()</code></pre>
*   <pre><code>querySelectorAll()</code></pre>
And we can move from element to another using:
*   <pre><code>parentNode</code></pre>
*   <pre><code>previousSibling /nextSibling</code></pre>
*   <pre><code>firstChild / lastChild</code></pre>

If we want to access an element more than once, we should store the reference of that element in a variable, and this variable will access the location of that element not the content.
We also can select an element from a node list by one of these two methods:
1. Item () method, but here we have to be sure that there is at least one element in the node list before executing the code.
So the item() method is done by:
 * Selecting the elements that have a class attribute and storing the node list in a variable.
 * Ensure there is at least one element in the list using 	element.length inside **if** statement.
 * Store the element in a variable, and use	elements.item() putting the index inside the parenthesis.
It will look like :
    <pre><code>let elements = document.getElementByClassName(‘class name’)
        if(elements.length >=1){
            let firstItem = elements.item(put the index here);
}</code></pre>
2. Array syntax.
It looks like the following:
    <pre><code>let elements = document.getElementByClassName(‘class name’)
    	    if(elements.length >=1){
      	    let firstItem = elements [put the index here];
}</code></pre>
We can apply a statement to an entire node list elements one by one, using the for loop,
Here we want to change the class of all hot items in the list to cold items by 
    <pre><code>let hotItems = document.querySelectorAll(‘li.hot’);
    	for (let i = 0; i < hotItems.length; i++){
            hotItems[i].className = ‘cool’;
}</code></pre>
### adding or removing HTML content 
We can use either one of these methods:
* The innerHTML property
We add content by:
1. Store a new content as a string in a variable.
2. Select the element that you want to replace.
3. Set the element’s innerHTML property to be the new string.
We can remove all content of an element by providing the entire fragment minus that element.
* DOM manipulation methods
We add content by using a DOM method for creating new content, one node at a time and storing it in a variable, then another DOM method is used to attach it to the right place in the DOM tree.
### Attribute nodes
We have several methods to work with attributes of any elements in the HTML by:
Select the element node that carries an attribute and follow it by a period, then use one of the following methods or properties:
##### Methods include:
*   <pre><code>getAttribute()   “that gets a value of an attribute”.</code></pre>
*   <pre><code>hasAttribute()   “that checks if the element has an attribute or not”.</code></pre>
*   <pre><code>SetAttribute()   “that sets the value of the attribute”.</code></pre>
*   <pre><code>removeAttribute()    “that removes an attribute form an element’s node.</code></pre> 
##### Properties include:
* *className* “gets or sets the value of the *class* attribute”.
* *id* “gets or sets the value of an id atteibute”.
And the syntax will look like the following:
   <pre><code>document.getElementById(‘one’).getAttribute(‘class’)</code></pre>


