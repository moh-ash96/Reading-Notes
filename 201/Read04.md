# HTML Links, JS Functions, and Intro to CSS Layout
## Links
Links are very important in a webpage, because they allow you to go from a page to another and navigate in the page you are in and that defines surfing.
In HTML, links are added using:
* < a >  tag , the link text will be between the opening and closing *a* tags.
* *href* attribute , that will contain the link of the page the user is going to.
* Link text, is the place where the user will click on to follow the link, and it is better to be named as the page name, and has different color than the entire text.
* The link address.
So the link will look like this :
< a href = “ link address “ > link text < / a >
### Types of links we can include in our page 
* Linking to other sites, here the link will take us to other sites and the link address should be absolute URL.
* Linking to pages of the same site, here we use relative URL, that will be the name of the file, if it is at the same folder, or the folder name / file name, if they are in different folders.
* We can add another attribute to the href attribute called *mailto* and this will be followed by an email address, when clicked on; will start an email to that address.
* Linking to a part of the same page, is done by giving an *id* to the element we want and the href will start with #then the id of the element.
* Linking to a specific element at another page is done by, href =” link of the page / #id “ and it works either in the same website or another wesite.
* If we want the clicked link to be opened in a new window, we can use the attribute *target*, but it is better to avoid new window, but when needed; user should be informed that this link opens in a new window.
 ### Directories:
In HTML the *folders* are called *directories* they are used to contain and organize the all the files in the website.
As a usual structure a top level folder which is called the **root** folder will contain all files and folders in the website, we can see the relations between directories using the family tree, which relates every child file or folder to their parent folder.
Every page shown to the use on the website is index.html file, so at the root level there is index.html that has the homepage, and the other pages are made as index.html each in separate folder.
## Layout
CSS deals with the HTML elements as boxes, they can be **inline elements**, that start at the same line of the other box, and **block-level elements**, these start another line.
In HTML some elements have another elements inside them, these are referred as containing elements.
### Elements positioning
There are several positioning schemes that allow us to position the elements we want the way we want, including:
* Normal flow, it is the default in almost all browsers and here every element added will below the one before the syntax for that is *position: static;* .
* Relative positioning, here we can move the element to the top, bottom, right, and left, and so on the syntax here is *position: relative;* then we add the directions we want to move the element to.
* Absolute positioning, here we position the element in relation to its containing element, and the absolutely positioned elements move when the user scrolls up and down, we use the syntax *position: absolute;* then we add dimensions. 
* Fixed positioning, it is absolute positioning but it is related to the window area, and elements don’t move when the user scrolls, here the syntax is *position: fixed;* then the dimensions are added.
* Floating elements, it positions the element to the far left of the far right of the page, we use here *float: right* or *float: left*.
When moving the element from normal flow some elements may overlap another elements, to control which element will be on the top; we use z-index the it is followed by a number, the elements then are arranged by the ordered numbers.
## Functions
We use functions to group a series of statement to perform a specific task, and we can reuse it if we need to perform that task again in another place in the script.
Also we use functions to store information to use them when needed, because functions will not run until we declare them.
When functions are to be used we should name them, and the *name* should describe the task that the function is performing. The name of the functions is used to *call* it; when we want it to appear in our code. The statement we need should be written in curly braces {} that is function declaration.
Some functions need more information about the task, such as the ( height and width in box function ) these information are called **parameters** .
When a function returns an answer, the answer is called **return value** .
There is a type of functions that are called **anonymous functions**, they don’t have a name and can’t be called, they are executed as soon as the interpreter comes across them.
To make a function we should do the following:
* Name the function.
* Declare the function using the keyword **function** then state the *name* of the function, then put the statement inside curly braces {} . 
* Call the function by typing the name of the function followed by empty parenthesis () .
We can get either single value from a function using a variable, or multiple values using an array.
# Pair programming
Working alone on the code is good, and the one that can run a whole complicated code alone is a skied person, but it takes them so much time to write the code, detect errors and fix them, and so on.
Pair programming has so much benefits, because here the load of work will be on several people, and I’m going to mention 6 benefits of pair programming:
1.	Greater efficiency, when more than one person work on one program and everyone knows their job, gives us more sophisticated, error free code.
2.	Engaged collaboration, when more than one are  using and looking at the same code, a better outcome will be expected, and also the cheer each other to have them  continue.
3.	Learning from fellow students, when one of the primers is stuck at something, or doesn’t know any part of the code, their fellows will offer to help them solve the conflict .
4.	Social skills, with pair programming, the social skills will be improved, considering the communication between the fellow students even if they don’t know each other.
5.	Job interview readiness.
6.	Work environment readiness, at work, almost every code is done by many partners, so working like this right now will help us adapt in the work  more quickly.
