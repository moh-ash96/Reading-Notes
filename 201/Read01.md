# Introductory HTML and JavaScript
## Introduction:
 Coding is not a very hard thing to do, it depends on learning, researching, and practicing; the more you read and do, the easier you see it in the next project.
So basically you will start at learning
* HTML, which holds the structure and all the content of your website.
* CSS, that is the style of the website.
* Java script, that one adds movements and functions to your website.
For accessing a website you need a *device*, an *internet connection* and a *browser* that can read webpages.
And in order to go to any website, some steps are followed, including:
* Connect to the web, via an Internet Service Provider (ISP). 
* Type a web address into the browser to visit a site.
* The computer will contact a network of servers called **Domain Name System**(DNS) servers. They tell your computer the IP address associated with the requested domain name.
***Which is a number of up to 12 digits separated
by periods / full stops.***
* The unique number that the DNS server returns to your computer allows your browser to contact the web server that hosts the website you requested.
* The web server then sends the page you requested back to your web browser.
## Structure
As I mentioned above, the structure of a webpage is made by HTML and HTML uses elements to describe the structure of the page, these elements include:
* Head, it has the title and external links and it’s contents don’t appear on the webpage.
* Body, that consists of:
 * header, it usually contains the (heading, and the navigation).
 * main: that has almost all the content of the website.
 * footer: that usually contains some links and copyright.
And many elements that carry our content such as headings (h1,h2,h3,h4,h5,h6), navigation, paragraphs, etc.
All elements are contained by *tags*, the name of each tag indicates the element inside it, almost each element has an *opening* and *closing* tags, and some don’t need closing tags.
We also can add more information about the elements using *attributes*, these attributes are places inside the opening tag and are made of two parts, 
* Attribute name: it indicates what type of extra information we are providing.
* Attribute value: it is the information or the setting of the attribute and should be placed in double quotes.
## Extra markup

At the beginning of the HTML page we must declare the version of HTML we are using by, <! DOCTYPE HTML > tag.
We also can add some text that we don’t want it to appear in the webpage; as a comment or a reminder or to recognize what are we doing in that element by using <!—anything inside those will not appear on the website -->  
There are some identification or classification attributes that we can sue in order to differentiate between elements in the structure, so we use ID attribute for the identification of one and unique element and CLASS attribute to indicate that elements in that class are different than other elements.
Some elements tend to go in the same line with other elements such as < a > < b > < em > < img > these are called Inline elements.
Other elements start a new line when added to the structure, such as < h1 > < p > < ul > < li > , these are called Block elements.
We can group a set of elements together in a block using < div > element, and in an Inline using < span > element.
There is an element called < iframe > this element allows you to put a window in your page that is another page.
The < meta > tag contains information about your page, this information are not visible to the visitor, they are only to tell search engines about your page.

## HTML 5 Layouts

There are many new elements added to the HTML5 that help organize the structure and make it easier to deal with, such as
* < header > it usually contains the titles and navigation
* < footer > usually contains external links and copyrights
* < nav > contains major navigation blocks on the site, such as primary site navigation.
* < article > can be a container of any section on the page 
* < aside > it is also a container and it can be inside or outside an article, if it is inside, it is related to that article but not essential to its overall meaning, and if it is outside, it is related to the whole document.
* < section > it divides the webpage into sections and each section can have their own heading.
## Process And Design
In order to start your website you should know what content to add and who are your target people you should start on planning for what content to add and where to add them, this is done by making a **site map** it contains all parts of your website organized by a block diagram. 
After the site map is made, you should make a wireframe that is the simple sketch of the key information that needs to go on each page of a site.
After that you will start the HTML structure building and then the ordering and visual hierarchy of the content.
## Java Script
For programing there are three main concepts to follow, these are,
1.	( A )
What is a script and how do I create one,
A script is a series of instructions that a computer can follow to achieve a goal To make a script there are some steps we have to follow including
###  1. *Define* the goal
First, you need to define the task you want to
achieve.
###  2. *Design* the script
To start the design you should split the goal into several tasks and arrange them in a flow chart.
###  3. *Code* each step
Now you must type the tasks you put in the chart is computer language i.e. JavaScript

2.	( B )
How would computers fit in with the world around them?
When you want to make the browser identify anything you add to your webpage, you shoul objectify that thing and tell the browser about it using java script; browsers can only read html, so if you want your website to interact with users you use javascript.

3.	( c )
How do I write script for a webpage?
First you made an HTML page then you will create a new file and call it app.js this is a java script file, it contains all java script codes that we want to apply on the page, then we link that JS file to the HTML page we created.




