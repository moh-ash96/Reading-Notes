# CSS Transforms, Transitions, and Animations



### Transform
It is a new property that makes positioning and sizing of elements easier, and it comes in two different settings 
1. *2D Transforms*
The 2D transform only includes  *X axis* and *Y axis*, and there are multiple properties that can be changed using the 2D transformation, including
* **2D Rotate**, it is used to rotate the element from 0 to 360 degrees, the has positive value for rotation clockwise, and negative value for counterclockwise.
* **2D Scale**, it is used to change the size of the element, the default value is *1*, so the value between *0.01* to *0.99* will reduce its size, and the value that equals or is above *1.01*, increases the element’s size, the change on *X-axes* will change the width, while the change on *Y-axes* will change the height.
* **2D Translate**, is used to change the position of the element on *X-axes* or *Y-axes* or both, using the pixels, or percentage units.
* **2D Skew**, it is used to distort element either on the *X-axes* or *Y-axes* and the unit here in degrees.
All elements have the origin value of *50%* vertically and *50%* horizontally ( at the center ), this can be changed using transform-origin property, and it can accept one value that will be applied on both directions, and when two values are added the first will affect the horizontal and the second will affect the vertical.
2. *3D Transforms*
It has the same properties as the *2D*, but with considering the *z-axes* and it includes 
* 3D Rotate.
* 3D Scale.
* 3D Translate.
* 3D Skew.

### Transitions
Transitions can be added using **CSS pseudo-classes** such as 
* :hover
* :focus
* :active
* :target
These pseudo-classes can have up to four transition related properties including:
1. Transition-Property, it determines exactly what properties will be altered in conjunction with the other transitional properties, and we can also use more than one property by typing them and separating them by commas.
2. Transition Duration, it sets the duration in which the transition property takes place, and its value is set using general timing value, and more than one duration can be added when we need to set different durations for different properties, and they will be added respectively.
3. Transition Timing, it is used to set the speed in which a transition will move.
4. Transition Delay, it determines how long a transition should be stalled before executing.
##### Shorthand Transitions
We use this property to combine the four properties inside one transition property by only typing; transition and following it with the four values in order of transition-property, transition-duration, transition-timing-function, transition-delay.

### Animations
Transitions do a great job of building out visual interactions from one state to another, and are perfect for these kinds of single state changes. However, when more control is required, transitions need to have multiple states. In return, this is where animations pick up where transitions leave off.
For an animation to be made we should start with a keyframe, that will contain the animation name, breakpoints, and properties.
Animations have similar properties to the transition such as duration, timing function, and delay. 
Other properties are:
* Animation iteration, here we set the times the animation will be repeated.
* Animation direction, we set the direction that the animation will go and it includes
    * Normal, it will go from beginning to end.
    * Reverse, from the end to the beginning.
    * Alternative, the animation will be played forwards then backwards.
    * Alternative-reverse, the animation will go backwards then forwards then backwards.
* Animation play state, it allows the play and pause of an animation, while the play will start where the animation was paused.
CSS3 Transitions:
* Fade in.
* Change color.
* Grow and Shrink.
* Rotate elements.
* Square to circle.
* 3D Shadow.
* Swing.
* Insert border.

