# Images, Color, Text
## Images
I almost every website there are Images added in different sizes and locations so, here are some tags and syntax that help us add images and modify them:
### Add an Image:
To add an image to our website we need the following elements:
* < *img* / >  tag.
* *Src* attribute, here we either but the relative path or the absolute URL of the image we want.
* *Alt* attribute, it contains a description about the image and will appear when that image is not available.
* *Title* attribute, it adds title to the image that usually appears when the user hovers on it.
### Image dimensions and position:
First t we should figure where to put the image in the code, we have three options:
1. Before the paragraph, here the paragraph will start a new line after the image.
2. Inside the start of the paragraph, here the first row of the text aligns with the bottom of the image.
3. In the middle of the paragraph, the image comes between the words of the paragraph.
We can change the width and the height of the image by adding, height = ‘ ’ and width = ‘ ‘.
### Creating an Image
We should follow three rules:
1. Save the image in the correct format.
 #### image formats can be:
 * *JPEG*, used with the images that have so many colors.
 * *PNG*, used in images that have an area filled with the exact same color.
 * **GIF*, it is an animated type of images and usually used when the page loads, and some other places.
2. Save the image at the right size.
Images we download should have the right height and width that we need to put in our website, because a lot of issues might come if we chose to resize them, such as, lower quality, and inappropriate shape of the photo content.
3. Use the correct resolution.
*JEPG*, *PNG*, and *GIF* images use **Bitmap** format, the best resolution that browsers display is 72 pixels per inch.
There is another type for photos called **Vector images** these images are not composed of pixels, they are composed of dots on a grid and then lines will be drawn between these dots and the spaces are filled with colors, these images are usually used for logos and increasing their size won’t change their resolution.
## Colors
CSS allows us to change the color of the text or it's background, and deals with each element separatly, there are several ways to include colors in your webpage using CSS, including:
* Color property, that allows us to change the text color.
* background-color property, that changes the color of the background of an element.
CSS understands colors as sets of values, each set define a different color, such as: 
* RGB, how much Red,Green,Blue are in the color we want ( 000,000,000 ).
* Hex, six-digit code for how much red, green, blue in the color we want ( #ee3e80 ).
* Color name, there are 147 predefined color names in the browsers.
* HSL, which has three parts:
 1. HUE, the degree of the color.
 2. Saturation, shades of gray.
 3. Light, amount of light ( brightness ).
There is another symbol that can be added to RGB and HSL which is ***a*** ( Alpha ), that symbol indicates the opacity of the color, it ranges from 0.0 to 1.0; while 0.0 transparent and 1.0 fully visible.
### Contrast
In webpages, especially the ones with a lot of text, *contrast* helps readers to see and understand the text more easily and leaves less tension on their eyes, and contrast can be made by modifying the text and the background colors.


## Text
CSS allows us to modify text to have the best appearance of our webpage and the modification is done by:
* Font-size, can be in pixels, ems, or percentage.
* Font-family, that specifies the family of the font.
* Font-weight, which is bold or normal.
* Font-style, styles are, normal, italic, oblique.
* Text-transform, for uppercase and lowercase transformation.
* Text-decoration, underline, line-through, overline, and blink ** animates the text**.
* Line-height, which is called leading, sets the vertical spaces between lines.
* Letter-spacing, sets the spaces between letter in the words.
* Word-spacing, sets spaces between words in the text.
* Text-align, to align text to the left, right, center, or justify.
* Text-shadow, add shadow behind text.
* Link, to style the links that are not visited.
* Visited, to style the links that was clicked.
* Hover, what happens when the user hovers over the text.

