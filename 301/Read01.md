# Responsive Web Design And Floats

## Responsive Web Design

Internet is used in different types of devices, so when the website is designed on a computer it will not be displayed properly on a mobile screen, or on a larger computer screen.
To overcome this situation, we can use **Responsive Web Design**, which is the practice of building a website suitable to work on every device and every screen size.
Another ways of web design are *Adaptive Web Design* and *Mobile Web Design*.
*Responsive* and *Adaptive* web design are closely related. *Responsive* generally means to react quickly and positively to any change, while *Adaptive* means to be easily modified for a new purpose or situation, such as change. With responsive design websites continually and fluidly change based on different factors, such as viewport width, while adaptive websites are built to a group of preset factors. A combination of the two is ideal, providing the perfect formula for functional websites. Which term is used specifically doesn’t make a huge difference.

Mobile, on the other hand, generally means to build a separate website commonly on a new domain solely for mobile users. While this does occasionally have its place, it normally isn’t a great idea. Mobile websites can be extremely light but they do come with the dependencies of a new code base and browser sniffing, all of which can become an obstacle for both developers and users.

Currently the most popular technique lies within responsive web design, favoring design that dynamically adapts to different browser and device viewports, changing layout and content along the way. This solution has the benefits of being all three, responsive, adaptive, and mobile.


**Responsive Web Design** is composed of three main components:
### 1. Flexible layouts:
It is building the layout of a website with a flexible grid, capable of dynamically resizing to any width, this is done by putting any element within a parent element and making the size of that element relative to the parent by relative positioning in *CSS*, here the best practice is using the percentages or the ***em*** units rather than fixed units such as pixles.
Em units include:
* ***vw***, Viewports width.
* ***vh***, Viewports height.
* ***vmin***, Minimum of the viewport’s height and width.
* ***vmax***, Maximum of the viewport’s height and width.

And there is an easy formula to find out the right relative value which is:
```
Target width of the element / width of the parent element = result relative element
```
But sometimes flexible layout isn’t enough, for example: when the width of a browser viewport is too small that even scaling the layout proportionally will create too small element to effectively display content, and when the layout gets too small, or too large, text may become illegible and the layout may begin to break. For that we can use media queries.
### 2. Media queries:
It is an extension to media types that is used when we are targeting and including styles (the ability to specify different styles for individual browser and device circumstances).
It is initialized by:
* Using the ***@media*** rule inside the stylesheet, or
* Importing new stylesheet using ***@import***, or
* Linking to a separate stylesheet in *HTML*.
But ***@media*** is the best choice.
After initializing the media query we follow it by media type, that can be *all*, *screen*, *print*, or *tv*. And when media type is not specified the default type will be set as *screen*.
Following the media type comes the **expression** that will contain different media features and values, which allocate to be *true* or *false*. If it allocates to *true*, the styles will be applied. If it allocates to *false*, the styles will not be applied.
We can use specific logical operators in media queries, including:
* **and**, which allows us to add extra condition so if the browser has all of the conditions the style will be applied.
* **not**, when added, the style will not be applied to the browser having the condition mentioned.
* **only**, the style will be applied when the condition mentioned is present.
Examples of media features:
* *Height & Width*, they also can be used with minimum and maximum prefixes.
* *Orientation*, such as portrait, and landscape.
* *Aspect Ratio*.
* *Resolution*.
 #### Mobile first
It is an approach includes using styles targeting smaller viewports as default styles for a website, then use media quires to add styles as the viewport grows. It is used to only apply necessary styles to the website when used on mobile to not waste bandwidth and to save battery life, and also this makes the website run faster.
It can be done by putting the default styles as usual and adding the desktop view style using media queries like the following:
```
@media screen and (min-width: 400px) {styling}
@media screen and (min-width: 600px) {styling}
@media screen and (min-width: 1000px) {styling}
@media screen and (min-width: 1400px) {styling}
```
#### Viewport
View port is used to assist the view of the website using the devices *size*, *scale*, and *resolution*, for that we can use the **meta** tag to identify these 
* *Viewport Height & Width*, that should be the device defaults by applying device-height and device-width values.
* *Viewport scale*, it controls how a website is scaled on a mobile device, and how user can continue to scale a website using:
	* *initial-scale*, it should be set to **1** as this defines the ratio between the device height, while in a portrait orientation, and the viewport size. Should a device be in landscape mode this would be the ratio between the device width and the viewport size. Values for initial-scale should always be a positive integer between 0 and 10.
	* *minimum-scale*, it is used to determine how small is the viewport scaled, and its value should be positive integer lower than or equal the initial-scale.
	* *maximum-scale*, it is used to determine how large is the viewport, and its value should be greater than or equal to the initial-scale.
	* *user-scalable*, it is used to set the ability of the user to zoom in or out  and its value can be either *yes*, or *no*. 
### 3. Flexible Media:
When using viewport to change the size of elements, some media types don’t follow. Images, videos, and other media types need to be scalable, changing their size as the size of the viewport changes. So we can set the max-width: 100% and this will fix the problem.
But some types of media such as the ones embedded inside iframe the max-width property doesn’t work, they can become responsive by doing like the following:

```
HTML
<figure>
  <iframe src="videoLink"></iframe>
</figure>
```
```              
CSS
figure {
  height: 0;
  padding-bottom: 56.25%; /* 16:9 */
  position: relative;
  width: 100%;
}
iframe {
  height: 100%;
  left: 0;
  position: absolute;
  top: 0;
  width: 100%;
}
```
While the padding is calculating using the aspect ratio which is here 16:9 and the formula is 

```
9 / 16 * 100% = 56.25% 
```

## Floats
Floats are used to wrap text with a specific element the way you want; we can use either:
* float: right; to put the element on the right and the text on the left.
* float: left; to put the element on the left and the text on the right.
* float: none; to ensure there is no float for that element.
* float: inherit; float value will be taken from the parent element.

### Techniques for Clearing Floats
When floating an element, the other elements will be affected and might not be displayed the way we want, so we need to clear float, that will ensure the floating element won’t affect the non-floating elements, and this is done by:
* #### Clear method:
    which has these values:
    * Both, will clear the right and left floats.
	* left, will clear the left float.
	* right, will clear the right float.
	* none, default.
	* Inherit, the same as the parent.
* #### The Empty Div Method
It is quite literally, an empty div. It is the most common because it has no browser default styling, doesn’t have any special function, and is unlikely to be generically styled with CSS.
* #### The Overflow Method
It relies on setting the overflow CSS property on a parent element. If this property is set to auto or hidden on the parent element, the parent will expand to contain the floats, effectively clearing it for succeeding elements.
* #### The Easy Clearing Method
It uses *CSS* pseudo selector *(:after)* to clear floats. Rather than setting the overflow on the parent, you apply an additional class like *“clearfix”* to it. Then apply this *CSS*:

```
.clearfix:after { 
   content: "."; 
   visibility: hidden; 
   display: block; 
   height: 0; 
   clear: both;
}
```

### Problems with floats
* **Pushdown** is a symptom of an element inside a floated item being wider than the float itself (typically an image). Most browsers will render the image outside the float, but not have the part sticking out affect other layout. IE will expand the float to contain the image, often drastically affecting layout, *Quick fix*: Make sure you don’t have any images that do this, use **overflow: hidden** to cut off excess.
* **Double Margin Bug** – Another thing to remember when dealing with IE 6 is that if you apply a margin in the same direction as the float, it will double the margin. *Quick fix*: set display: inline on the float, and don’t worry it will remain a block-level element.
* **The 3px Jog** is when text that is up next to a floated element is mysteriously kicked away by **3px** like a weird forcefield around the float. *Quick fix*: set a width or height on the affected text.
* In IE 7, **the Bottom Margin Bug** is when a floated parent has floated children inside it, bottom margin on those children is ignored by the parent. *Quick fix*: using bottom padding on the parent instead.
