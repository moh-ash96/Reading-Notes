# Pair Programming and jQuery
## jQuery
*jQuery* is a JavaScript file that is added to the webpage and uses *CSS* selectors to select elements and add methods to them.
Frist, we should find elements using *CSS* style selectors.
This is done by using **jQuery ()** function or the shortcut ***$()*** and the selector is added inside the parenthesis inside quotes.  
After the **jQuery ()** function there will be **‘.’** Added and followed by the method and every method has parameter that provides details about how to update the element.
Why use *jQuery*?
* It has simple selectors, as it uses *CSS* selectors so it is easier to use it to get element from the *HTML* than using the **DOM**.
* Common tasks in less code, it has almost all tasks used in JS but simpler such as:
	* loop through elements.
	* Add / remove elements from the DOM tree.
	* Handle events.
	* Fade elements into / out of view.
	* Handle Ajax requests.
* Cross browser compatibility.
Using jQuery, we can select single element as in selecting ‘ul’ element or multiple elements as in selecting ‘li’ elements, and we also can get and set element data from HTML using 
```
let content = $(‘li’).html();
$(‘li’).html(‘’updated);
```
,respectively 

Sometimes in the *JS* if we want to use a function for more than one element we need to use loops, but with **jQuery** we can put a *class* on the elements we want to modify and use it to apply on all of them.
And we also can add several methods to one selection using by calling the selector and adding the methods separated by dot notation.
There are some handy methods is jQuery such as:
* The *load event* that lets the page load then the *JS* applies and it is replace by .on.
* The *.ready ()* method, that checks if the browser supports **DOMContentLoaded**.


### Ways to include *jQuery*:
* Downloading it to the files of the websites.
* Getting it as a link from Content Delivery Network (**CDN**), that is powered by Max CDN, Microsoft, and Google.
After getting the link of jQuery, we need to add it to the HTML, and the best place is before the closing </ body > tag, because it waits for the whole HTML to load then the *JS* will work, and that makes it faster.

## 6 Reasons for Pair Programming:
**Pair programming** is working on the code by two people as one is the driver which writes the code and the other is the navigator that only navigates the driver on how to deal with the code.
### Reasons:
1. *Greater efficiency*
That is getting work done quickly with high quality, and that is achieved when more than one mind focuses on the same problem.
2. *Engaged collaboration*
Working with someone looking at your screen make it harder to lose focus on what you are doing and also it makes it easier to get help when needed.
3. *Learning from fellow students*
When coding with others you will learn new things that was concerning you and preventing the perfection of your code and you will help the other person on the aspects they are not strong in.
4. *Social skills*
Of course working with another person will improve your social skills and communication.
5. *Job interview readiness*
In some interview there is a test when you use pair programing with the one interviewing you and practicing it now will increase your opportunity in passing that exam.
6. *Work environment readiness*
Many companies that utilize pair programing expect to train fresh hires from CS-degree programs on how they operate to actually deliver a product.
