# Canvas
Some websites need charts to display data, this can be done by Charts.js JavaScript plugin that uses HTML element (canvas).
This allows us to add either line, bar, and pie charts, by adding canvas element to the HTML add data to the chart using JavaScript.
In HTML the canvas element has only the id, height, and width attributes, and if the height, and width attributes are not added the canvas will have the size of 150*300 px, and it also needs a closing tag.
Some browsers don’t support canvas, so we add a fallback content for these browsers to display the information, so if the browser support canvas, it will ignore the fallback, and vice versa.
###  Drawing shapes with canvas
Canvas is considered a grid and each unit of the grid equals a pixel, and the origin of the grid is the top-left corner.
we can draw in canvas using either rectangle properties or using paths.
We have three rectangle properties:
1. fillRect(x, y, width, height), this will produce a filled rectangle.
2. strokeRect(x, y, width, height), this will produce an empty rectangle.
3. clearRect(x, y, width, height), this will erase an are in the shape of a rectangle.
Here x, y are used to specify the position if the rectangle, while width, and height are for its size.
In paths, we only connect points together using codes, and we can use this way of drawing to draw a lot of different shapes including:
* **Triangles.**
* **Lines**, using line to ()
* **Circles** and arcs using arc to () or arc()
* **Bezier** and **quadratic** curves, using quadratic curve to () or Bezier to ()
* **Rectangles**, using rect()
We start drawing using beginPath(), and we use other methods, such as:
* ClosePath, to add a straight line to the path going to the start of the sub path.
* Stroke(), is used to draw the outline of the shape.
* Fill(), it draws a solid shape.
We can also combine more than one shape to make a drawing.
There is a property called moving the pen which is made using, moveTo(x, y)and it is used to change the place of drawing.
### Colors
We can add colors to the shapes we draw either to change the fill color or the stroke color using:
fillStyle = color
strokeStyle = color
and the color here can be either by color name, RGB, or #000000.
We can add transparency to the color using globalAlpha = transparencyValue
We can change line styles using:
* lineWidth = value, to set the width of the line.
* lineCap = type, to set the appearance of the ends of lines.
* lineJoin = type, for the appearance of the corners.
* miterLimit = value, establishes a limit on the miter when two lines join at a sharp angle, to let you control how thick the junction becomes.
We also can add patterns to the shapes using:
* createLinearGradient(x1, y1, x2, y2), creates a linear gradient object with a starting point of (x1, y1) and an end point of (x2, y2).
* createRadialGradient(x1, y1, r1, x2, y2, r2), creates a radial gradient. The parameters represent two circles, one with its center at (x1, y1) and a radius of r1, and the other with its center at (x2, y2) with a radius of r2.
* createConicGradient(angle, x, y), creates a conic gradient object with a starting angle of angle in radians, at the position (x, y).
* gradient.addColorStop(position, color), creates a new color stop on the gradient object. The position is a number between 0.0 and 1.0 and defines the relative position of the color in the gradient, and the color argument must be a string representing a CSS < color >, indicating the color the gradient should reach at that offset into the transition.
We can add a pattern using an image and some properties:
* repeat, tiles the image in both vertical and horizontal directions.
* repeat-x, tiles the image horizontally but not vertically.
* repeat-y, tiles the image vertically but not horizontally.
* no-repeat, doesn't tile the image. It's used only once.
We can add shadows by one of these four properties:
1. shadowOffsetX = float, indicates the horizontal distance the shadow should extend from the object. This value isn't affected by the transformation matrix. The default is 0.
2. shadowOffsetY = float, indicates the vertical distance the shadow should extend from the object. This value isn't affected by the transformation matrix. The default is 0.
3. shadowBlur = float, indicates the size of the blurring effect; this value doesn't correspond to a number of pixels and is not affected by the current transformation matrix. The default value is 0.
4. shadowColor = color, a standard CSS color value indicating the color of the shadow effect; by default, it is fully-transparent black.


### Drawing text
We can render text using one of the following :
* fillText( text, x, y [ , maxWidth ] ), fills a given text at the given (x,y) position. Optionally with a maximum width to draw.
* strokeText( text, x, y [ , maxWidth ] ), strokes a given text at the given (x,y) position. Optionally with a maximum width to draw.
We can style text using:
* font = value, to indicate the font family.
* textAlign = value, to set the alignment of the text.
* textBaseline = value, to set the baseline alignment of the text.
* direction = value, for directionality.
We also can use measureText(), which returns a TextMetrics object containing the width, in pixels, that the specified text will be when drawn in the current text style.
