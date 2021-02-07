# Process And Design
Websites should be designed for the target audience, not only for the site owner; so you need to know what audience to target, and that is determined by what your site contains.
You should ask  yourself, why would audience visit your site, is there a motivation or a specific goal, you also should create a list of reasons that make people visit your site.
After considering what people may need to see on your website, you should provide the information that they need and make your website relevant to them, then you can add any idea you think they might find helpful, and think of what would make them comeback when their goal or need are achieved.
Depending on what you deliver on your site and how often people visit it you should decide the frequency of the information updates on it.
## Site Map
After picking the content of your site, the next step is to have sections and pages ordered in a way that makes it easier for the viewers to find what they want and navigate the site, so there must be groups that gather related content and each group will be a page and a page that has all the links to the other pages is called a homepage.
## Wire Frame
It is a simple sketch that indicates what is the structure of the page and should be made before starting of the programming.
For the page to be organized the elements may be prioritized and ordered into blocks or chunks which is the simplest way to organize a page, also *visual hierarchy*; which is adding images to the website, or font editing and background modification, will make the website better looking and better idea presenting.
After we've done with the content and organization, we start working on the navigation, that will make it easier for the visitor to navigate and follow links on our website, the navigation should be at the heading and should contain the main links of the pages on that website, it is better not to exceed eight links and highlight the active link in order to tell the visitors where they are.

# HTML 5 layout
In the past, page authors used < div > elements to define elements on the pages such as (header, nav, sidebar, etc...), in HTML-5 the < div > is not needed anymore, there are new elements, each describing their contents; such as
* < Header >
which usually contains the name of the site and main navigation elements, which is presented by the tag < nav >.
* < footer >
it usually contains copyright and some links.
* < article >
it contains any section on the page and we can separate elements by putting them in different articles.
* < aside >
it can be inside or outside an article, if it is inside, it contains information related to the article but not essential to it's overall meaning, while if it is outside then article, it's contents are related to the entire page.
* < hgroup >
it contains multiple headings from < h1 > to < h6 > to be considered as one heading.
* < figure >
it contains any figure that is a reference from the main flow of an article.
* < div >
it is still used to group elements and also contains the elements that are not yet assigned with new tags.
* < a >
it is a linking element that can upload a link to the HTML file.
>since the HTML-5 is a new language, the old browsers can't read it, so the html file should be linked with **Java Script** or a **CSS**
line should be added for the page read by the elders of the internet.

# Extra Markup
* HTML-4
It an earlier release of HTML family and it contains almost all elements that are present now.
* XHTML1
It is the version that followed HTML-4 and it added some strict rules to the coding, such as:
  * every element needs a closing tag except for empty elements
  * Attribute name has to be in lowercase.
  * All attributes require value and values are placed inside double quotes.
  * Every element opened in another element should be closed inside it.
And there were more versions until they made HTML-5 which is not done completely yet but can be used anyway.
### Doctypes
Because there are multiple versions of HTML there must be < !DOCTYPE > declaration at the beginning of the page to tell the browser what version to read.
### Comments in HTML
When coding, we sometimes need to write a note or a comment inside the document that we don't want then viewer to see on the webpage and that is done by < !-- -- > 
### ID Attribute
It is a unique ID of any element in HTML, and it helps in the styling using CSS and also helps when dealing with Java Scrips, it can be done by < -the tag you want- id= " " >
### Class Attribute
Also can be added to any element but a single class can be assigned to more than one element, the aim here is to classify elements according to whatever class we want. It is done by < -the tag you want-  class= " ">
### Block elements
The elements that always start a line in the browser window, such as < h1 >, < p >, < ul >, and < li >
### Inline elements
The elements that always continue in the line of the neighboring elements eg. < a >, < b >, < em >, and < img >
### Iframe
It is used when you want to view another page as a small window inside your page, and it is done by < iframe src="link " >
