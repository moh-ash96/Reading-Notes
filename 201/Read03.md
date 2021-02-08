# HTML Lists, Control Flow with JS, and the CSS Box Model
## Lists
Listing is needed in any type of websites we may make, and there are several uses for lists. In HTML we can add three types of lists:
1. Ordered list, here the items are numbered.
We can add them to HTML by the tag  < ol > and list items are added by the tag < li >.
2. Unordered lists, the items here are listed by bullet points.
We can add them to HTML by the tag < ul > and list items are added by < li >.
3. Definition list, they are made of set of terms with the definitions of each term.
The list is added by < dl >  tag and the term is added by < dt > while the definition is added by the tag < dd > .
Nested lists, they are lists added inside an element to create a sub list.
## Boxes
CSS deals with the elements of html as boxes, they have default height and width that is enough to fill the page, but we can modify these dimensions as we like using the *width* and *height* styles in CSS, we can also limit these dimensions by using *min-width*, *max-width*, *min-height*, *max-height*.
If the content of the box is larger than the area of the box itself, the browser need one of the two values to determine what to do with the excess content, so it will either:
* **Hide** the excess content using the value *hidden*.
* **Add** a scrollbar that will allow users to scroll down for the rest of the content using the value *scroll*.
### Border, Margin, and Padding
The boxes we mentioned above are made of:
* Border, it separates the edges of the boxes, it is usually invisible but we can show it at different styles, colors and control its width using *border-style*, *border-color* and *border-width* respectively. And we can use **shorthand** property that allows us to specify these three at once.
* Margins, they define the gap between boxes, and their value is usually given by pixels.
* Padding, it is the space between the borders of the box and the content inside it.
### Other styling properties of boxes
* We can change inline boxes to block vise versa using *display: block*, and *display:inline* respectively, and there is inline-block property that causes block-level element to flow like an inline, while retaining other features of block level element.
* Box content can be hidden using visibility property, as the following:
Visibility : hidden, will hide the element from the webpage.

## Switch statements
We talked about if statement before and that it is used when we have more than one option to follow and we must choose between them, and there must be a condition that helps us choose, the switch statement is similar to it and it is used for the same purpose, but it is better when we have so much conditions and here they are called cases.
So the switch statement consists of :
* Variable, which is called switch value, and this variable should be verified before typing the statement.
* Cases, they contain the possible values that will be added and we can determine what will happen if the value matches the case.
* Break, after every case there is a break statement that stops the rest of the switch statement if the match is found.
* Default, if no case matches the value then the option assigned at default statement will run.
so the switch statement will look like :
e.g. 
let userName= ' '
  switch(userName){
      case ' ':
      something to do;
      break;
      default:
      something to do;
      break:
  }
## Loops
The loop checks the condition, if it is *true* so the program will run, and then it will check again, if also *true* it will run, and so on until it checks *false* then the program will be stopped.
There are several types of loops including:
* *For*
When you need to run a code for a specific number of times, the loop *for* is here for you because it counts how many times the loop should run.
* *While*
Here the condition is something other than counter so it will keep running until the return is not *true*
* *Do while*
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
We include what will change in every loop.


