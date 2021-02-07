# Basics of HTML, CSS & JS
## Text

For the best appearance in our webpage and to make it easier for the visitor to read and understand the content there are some tags called ***markup*** tags, these tags are used for this purpose.
I am going to talk about two main types,
### 1. Structural markup:
They are the elements used to describe both headings and paragraphs.
Here are some examples about structural markup tags:
* Headings:
They are used to add heading to any content you want, and they are ranged from < h1 > < / h1 > to < h6 > < / h6 >, while *h1* is the most important and the *h6* is the least important.
* Paragraph:
For adding a paragraph, we use < p > < / p >.
* **Bold** and *italic*:
 * To make a word or a part of the text in **bold** we use < b > < / b > tag,
 * And to make them *italic* we use < I > < / I > tag.
* Superscript and Subscript:
 * Superscripts are used to add characters that should be raised above the text such as ( power of, and the suffix of the date ) and that is done by the < sup > < / sup > tag.
 * Subscripts are used when we need to add a character that is below the line of the text such as ( the foot of the chemical formulas ) and that is done by using < sub > < / sub > tag.
* White space:
When reading the HTML content, the browser considers the multiple spaces and the new lines as one space in the paragraph so authors benefit from this in making their code easier to read.
* Line breaks and Horizontal rules;
 * Line break in used to add a new line of content inside a paragraph and it is done by < br / > tag.
 * < hr / > tag is used to add a horizontal rule between sections.
### 2. Semantic markup:
They provide extra information about the content.
These include :
* < strong > indicates that the text has strong importance and the browser will show it as **bold**.
* < em > indicates emphasis that subtly changes the meaning of a sentence and the browser will show it as *italic*.
* Quotations:
 * < blockquote > is used for longer quotes that take up an entire paragraph, paragraph tags are contained inside it.
 * < q > is used for shorter quotes that are located inside a paragraph.
* < abbr > is used to add an abbreviation or an acronym to the text.
* < cite > is used to reference piece of work.
* < dfn > is used for the definition of new terms.
* < address > is used to include contact details of the author.
* Change of content, we can use two tags to show that some contents are changed:
 * < ins > to insert the new content and will be underlined in the browser.
 * < del > to remove an older content and the browser will put a line through it.

## Introducing CSS
**CSS** is used to add rules to **HTML** elements to tell how these elements will be shown, and a CSS rule has two parts :
1. Selectors, they indicate which elements we are applying the rule to.
2. Declarations, they indicate how the elements referred to in **selector** are styled, it sits inside curly brackets and they are made up of two parts:
 1.	Properties: Indicate the aspect of element to be changed.
 2.	Values: Specify the setting for the property.
There are many ways to add **CSS** to your **HTML** file :
* *Internal* CSS, a < style > tag is added to the head of the html contains the selector and declaration we want to add.
* *Inline* CSS, we add style inside the element we want.
* *External* CSS, we make a new file that is usually called style.css and the extension is always .css then we add a link of that css to the html file.
### Selectors 
There are many types of selectors that are used to indicate the element we want to modify, including:
* Universal Selector * {} 
It selects all the content in the html.
* Type Selector h1 {}, p {}, img{} 
Matches element names.
* Class Selector . class {} 
It modifies a class already classed by class attribute.
* ID selector # ID {} 
Modifies an ID 
### CSS Rule Cascade
1. Last Rule, if two selectors are identical, the last one will be applied.
2. Specificity, if one selector is more specific than the other, it will be applied
3. Important, you can add ! important to any element and will be considered more important than the other rules applied to the same element.

## Basic JavaScript Instructions
When making a script, some data should be stored inside a container; to deal with when making statements or operations, that container is called a variable.
Before using the variable we should announce that we want to use it, by creating a new variable and giving it a name, this process is called **declaration**.
e.g. var quantity
after creating and naming the variable we should assign them to a value, by typing the name of the variable followed by equal sign then the value we want.
e.g. quantity = 3;
 ### Data types:
There are three data types that JS can distinguish between including:
1. Numeric Data Type, numbers.
2. String Data types, anything inside quotes.
3. Boolean Data Types, True or false.
### Arrays:
Arrays are special type of variable that store a list of values instead of one.
To create an array we type var, followed by the name of the array and then we type the name of the array and the values we want will be contained in square brackets, and separated by commas.
e.g. var  colors;
colors = [ ‘white’, ‘black’, ‘custom’ ];
### Expressions:
There are two types of expressions that result in a single value.

1. Expression assigning a value to a variable:
Every variable has to be given a value in order to be useful, and we can do that using assignment operator “=” e.g. var color = ‘red’;

2. Expression that use two or more values to return a single value
Here we perform operation on more than one value to have a single value and an example is when we express the value by math, e.g var area = 3*2; and here the area will be 6.

### Operators:
Expressions rely on operators since they allow programmers to create a single value form one or more values. There are several types of operators, including:

* assignment operator
Assigns a value to a variable; color = ‘red’;

* Arithmetic operator
It performs basic mathematical operations using ( +,-,/,*,++,–,%) and follows order of execution.

* String operator
It is used to combine strings together using ( + ) symbol.

* Comparison operator
It is used to compare between two values and the return should be true or false, e.g. buy = 5 > 3; here the value will be false for buy.

* Logical operators
Combine expressions and return true or false e.g. buy = ( 5 > 3 ) && ( 2 < 4 ); here the value is true.

## Decisions and Loops
### Decision making
There are many places in the script that need making a decision to determine which line to run next, it is like reaching a junction and we have two paths ahead each path is made of a set of tasks, so to decide which path we should follow, we must put a condition that the path would be greater, equal, or less than that condition, if the outcome is true, we continue on that path, and if it returns false, we choose the other path. 
### Comparison operators
#### Evaluating conditions
This operator allows evaluating condition by comparing between one value in the script to something you expect might be the same, and the result will be Boolean, and these operators include:
* Equal to ( == ) This operator compares two values to see if they are the same. e.g. ‘Hello’ == ‘Goodbye’ will return false, because they are not the same, while ‘Hello’ == ‘Hello’ will return true.
* Strict equal to ( == ) This operator compares two values to see if they have the same type and data. e.g. ‘3’ === 3 will return false, because they are not the same type, while 3 === 3 will return true, they have the same type and data.
* Not equal to ( != ) This operation compares two values to see if they are not the same. e.g. ‘Hello’ != ‘Goodbye’ will return true, because they are not the same, while ‘Hello’ != ‘Hello’ are the same, so the return will be false.
* Strict not equal to ( !== ) It checks if both data and value are not the same. e.g. ‘3’ !== 3 will return true , because they are not the same in data and value, while ‘3’ !== ‘3’ are the same data and value, so the return will be false.
* Greater than ( > ) Checks if the number on the left is greater than the number on the right.
* 0Less than ( < ) Checks if the number on the left is less than the one on the right.
* Greater or equal ( >= ) Checks if the number on the left is greater or equal to number on the right.
* Less or equal ( <= ) Checks if the number on the left is less or equal to the number on the right.
### Logical operators
They are used to compare two comparison operators and the result will be either true , or false.

* Logical **and** ( && ) It check if both operators on it’s left and right are true; if they are, the result is true, if one or both are false, then the result will be false.
* Logical **or** ( || ) It checks if one pf the operators we are comparing is true; if one operator is true then the result will be true, and the false result will appear only if both operations are false.
* Logical **not** ( ! ) it takes a Boolean value and inverts it; if the value was true before adding the ! the return will be false, while if it was false before the ! the result will be true.
### Loops
The loop checks the condition, if it is true so the program will run, and then it will check again, if also true it will run, and so on until it checks false then the program will be stopped. There are three common types of loops:
1. ***For*** When you need to run a code for a specific number of times, the loop for is here for you because it counts how many times the loop should run.
2. ***While*** Here the condition is something other than counter so it will keep running until the return is not true
3. ***Do while*** It is similar to while but if you put a statement in {}, it will run it at least once, even if the return is false.     
We can do the **for** loop by following these steps:
* 'Initialization' Creating a variable and setting it as ZERO, and it is usually called i , it acts as a counter and it looks like this Var i = 0;
* 'Condition' We set a specific value for the counter to reach and stop counting e.g. i < 10; here the counter will continue until it reaches 10 we can give a variable to the condition using var and calling what we want e.g. var rounds = 3; the condition will be i < (rounds);
* 'Update' We put in it what will change in every loop. e.g. we can use i++ to add one at every loop, or i– to have the loop countdown. So the whole code will be for ( var i = 0; i < 10; i++) { the code will be here }

