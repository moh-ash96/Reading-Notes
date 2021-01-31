# JavaScript Functions
 **Functions** let you group a series of statements together to do a
specific task. They are used when different parts of the code need to be reused, When functions are to be used we should name them, and the *name* should describe the task that the function is performing. The name of the functions is used to *call* it; when we want it to appear in our code. The statement we need should be written in curly braces {} that is function declaration.
Some functions need more information about the task, such as the ( height and width in box function ) these information are called **parameters** .
When a functions returns an answer, the answer is called **return value** .
There is a type of functions that are called **anonymous functions**, they don’t have a name and can’t be called, they are executed as soon as the interpreter comes across them.
To make a function we should do the following:
* Name the function.
* Declare the function using the keyword **function** then state the *name* of the function, then put the statement inside curly braces {} . 
* Call the function by typing the name of the function followed by empty parenthesis () .
e.g.  function sayHello! () {document.write(‘Hello!’);
this function is called by typing :
sayHello! ();

# CSS
*Cascading Style Sheet.*
It is used to style HTML sheet,
It has three ways to handle its job:
1. Inline, here we put the styling inside the tag we want to modify inside the HTML sheet.
2. Internal, here we put the styling in the head portion of the HTML sheet.
3. External, we make a new CSS file and make the style there, and put a link of that file in the head of the HTML sheet.
## Colors 
There are several ways to include colors in your webpage using CSS, including:
* RGB, how much Red,Green,Blue are in the color we want ( 000,000,000 ).
* Hex, six-digit code for how much red, green, blue in the color we want ( #ee3e80 ).
* Color name, there are 147 predefined color names in the browsers.
* HSL, which has three parts:
1. HUE, the degree of the color.
2. Saturation, shades of gray.
3. Light, amount of light ( brightness ).
There is another symbol that can be added to RGB and HSL which is ***a*** ( Alpha ), that symbol indicates the opacity of the color, it ranges from 0.0 to 1.0; while 0.0 transparent and 1.0 fully visible.
## Contrast
In webpages, especially the ones with a lot of text, *contrast* helps readers to see and understand the text more easily and leaves less tension on their eyes, and contrast can be made by modifying the text and the background colors, and this modification can be done by:
* Foreground color, which indicates text color, can easily be modified using { color: the color we want *we can use here name, hex, or rgb* } .
* For background, we use { background-color : the color we want } .
