# presentation-canvas
Hello, everyone!
My name is Veronika Vasilchikova.
I want you to dive into very fascinating topic with me. This is canvas! *(Slide 1)*

The <canvas> is an HTML5 element which can be used to draw graphics via scripting (usually JavaScript) on the fly. *(Slide 1.1)*
  
For instance, it can be used to draw graphs, combine photos, or create animations. You can see examples of canvas implementations on this slide. *(Slide 1.2)*


I am sure that the best way to learn something is practice.
Let’s start! *(Slide 2)*

## Basic usage of canvas
To start a canvas project, we will need an HTML file and a Javascript file.

`<canvas id="first-canvas" width="300" height="150"></canvas>`

`<script src="script.js"></script>`

The canvas element has the following attributes: width, height, id. Width and height are both optional. When no width and height attributes are specified, the canvas will initially be 300 pixels wide and 150 pixels high. *(Slide 3)*
The canvas is initially blank, it creates a fixed-size drawing surface to display something. You do not see anything on the page because the canvas is an invisible element. *(Slide 3.1)*
Let’s add some style with CSS. We add border, positioning and background-color to our canvas. 

`#first-canvas {

   border: 1px solid lightblue;
   
   position: absolute;
   
   top: 30px;
   
   left: 0;
   
   right: 0;
   
   bottom: 0;
   
   background-color: lightblue;
   
}`
*(Slide 3.2)*
Here is a result. *(Slide 3.3)*



### Let’s go to JavaScript file. 

`const draw = () => {

   // Get canvas-element
   
   const canvas = document.getElementById('first-canvas');
   
   // Checking for support
   
   if(canvas.getContext) {
   
      // Get a context from the canvas
      
      const ctx = canvas.getContext('2d');
      
   } else {
   
      console.log('canvas is not supported');
      
   }
   
}

document.body.addEventListener('load', draw());`

To display something, a script first needs to access the rendering context and draw on it. The <canvas> element has a method called getContext(), used to obtain the rendering context and its drawing functions. getContext() takes one parameter, the type of context. We will use "2d" parameter for 2D graphics.
Also we have to check for browser support by simply testing for the presence of the getContext() method. On this slide you can see basic skeleton template. The script includes a function called draw(), which is executed once the page finishes loading, this is done by listening for the load event on the document. *(Slide 3.4)*

## The canvas grid
Before we start drawing I want to talk about the canvas grid or coordinate space. The origin of this grid is positioned in the top left corner. All elements are placed relative to this origin. *(Slide 4)*

## Draw elements to a canvas
With the context we can draw the following:
•	rectangles
•	lines
•	paths
•	text
•	images
•	animation
*(Slide 5)*

### Drawing rectangles
Let’s start with the simplest thing – a rectangle.
On this slide you can see methods which change a fill and stroke color and draw rectangles. Pay attention to that to draw a rectangle we have start from point with coordinates (x, y) and set a width and height to our future rectangle. 

`ctx.fillStyle = 'orange'; // property which change a fill color

ctx.fillRect(215, 190, 220, 220); // draw rectangle - x, y, width, height

ctx.fillStyle = 'violet';

ctx.fillRect(280, 250, 40, 40);

ctx.fillRect(325, 250, 40, 40);

ctx.fillRect(280, 295, 40, 40);

ctx.fillRect(325, 295, 40, 40);

ctx.strokeStyle = 'tomato'; // property which change a stroke color

ctx.strokeRect(280, 250, 85, 85);`

*(Slide 6)*
Here is a result of our code.
*(Slide 6.1)*

### Drawing a triangle
Then we will draw a triangle. Drawing a triangle is an example of drawing lines. First we create the path with beginPath() function,  then we set the first point from which we will start drawing using method moveTo(), then we draw two lines with lineTo() method and using fill() method we will draw a solid shape by filling the path’s content area.

`ctx.beginPath(); // create a new path

ctx.fillStyle = 'tomato'; // set a color

ctx.moveTo(215, 190); // set the first point

ctx.lineTo(325, 50); // draw the first line

ctx.lineTo(435, 190); // draw the second line

ctx.fill(); // draw a solid shape by filling the path's content area`

*(Slide 7)*
Here is a result
*(Slide 7.1)*

### Drawing quadratic curves
Quadratic curves are type of paths. There are also available cubic curves. They are both called Bezier curves. We draw quadratic curves using quadraticCurveTo() method where points 250 and 300 are control points, 800 and 500 are end points.

`ctx.beginPath();

ctx.fillStyle = 'green';

ctx.moveTo(0, 500); //start

ctx.quadraticCurveTo(250, 300, 800, 500); // 250, 300 - control point; 800, 500 - end point

ctx.fill(); // default color - black`

*(Slide 8)*
Here is a result
*(Slide 8.1)*

### Drawing a circle
To draw arcs or circles we use the arc() or arcTo() methods.
We draw a circle which is centered at position with coordinates (650, 80) with radius 50 pixels starting at startAngle (0) ending at endAngle (360) going in the given direction indicated by anticlockwise. And after that we draw some lines to finish our picture

`// draw circle

ctx.beginPath();

ctx.fillStyle = 'yellow';

ctx.arc(650, 80, 50, 0, 360, false); // arc(x, y, radius, startAngle, endAngle, anticlockwise)

ctx.fill();

// draw lines

ctx.beginPath();

ctx.strokeStyle = 'yellow';

ctx.lineWidth = 5;

ctx.lineCap = 'round';

ctx.moveTo(590, 80);

ctx.lineTo(540, 80);

ctx.stroke();

ctx.moveTo(600, 130);

ctx.lineTo(540, 160);

ctx.stroke();

ctx.moveTo(650, 150);

ctx.lineTo(650, 200);

ctx.stroke();

ctx.moveTo(700, 120);

ctx.lineTo(750, 150);

ctx.stroke();

ctx.moveTo(720, 80);

ctx.lineTo(770, 80);

ctx.stroke();`

*(Slide 9)*
Here is a result
*(Slide 9.1)*

## Text
Drawing text is similar to rectangles. 
We have 2 methods:
-	fillText(text, x, y)
-	strokeText(text, x, y)
which let us write text on the canvas.
Where x and y refer to the bottom-left corner.
Before we draw text we have to clear our canvas using method clearRect().
You can change the font family and size using the font property.
*(Slide 10)*

`ctx.clearRect(0, 0, 800, 500);

ctx.font = '148px Courier New';

ctx.fillStyle = "red";

ctx.fillText('Canvas', 100, 150);

ctx.strokeStyle = "violet";

ctx.strokeText('Canvas', 150, 300);`

*(Slide 10.2)*
Here is a result
*(Slide 10.3)*

## Work with images
We will use drawImage() method.

`ctx.drawImage(image, dx, dy);

ctx.drawImage(image, dx, dy, dWidth, dHeight);

ctx.drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight);`

*(Slide 11)*
I want to show you how we can crop images using canvas.
*(Slide 11.1)*
*(Slide 11.2)*

First we will draw the whole image on the canvas. 

`const ctx = canvas.getContext('2d');

const image = new Image();

image.src = '../pictures/image-with-girl.jpg';

image.onload = () => {

 context.drawImage(image, 0, 0);
 
};`

*(Slide 11.3)*
*(Slide 11.4)*

Then we will select a portion of the image based on the following parameters:
-	0 and 100 mark the point on the image from where the selection is to begin;
-	187 and 336 are the width and height of the selection rectangle;
-	300 and 90 are coordinates of where to start drawing on the canvas;
-	187 and 336 show how wide and high to draw the image.

`const ctx = canvas.getContext('2d');

const image = new Image();

image.src = './pictures/image-with-girl.jpg';

image.onload = () => {

ctx.drawImage(image, 0, 100, 187, 336, 300, 90, 187, 336);
};`

*(Slide 11.5)*
Here is a result
*(Slide 11.6)*

## Animation
Let’s go to animation with canvas. I will show my example of animation – moving Mario using drawImage() method.
To execute an animation, instead of loading a new image every millisecond a portion of the same image is shown through a viewport just at different positions.
*(Slide 12)*
We have a row of Mario images. Every Mario has height is equal to 32 pixels and width is equal to 32 pixels.
*(Slide 12.1)*


We need to animate Mario or in other words show different frames of the same location in succession and make illusion of movement happen.

`const canvas = document.getElementById('first-canvas');

const ctx = canvas.getContext('2d');

const MARIO_WIDTH = 32;

const MARIO_HEIGHT = 32;

const mario = new Image();

mario.src = './pictures/mario.png';`

*(Slide 12.2)*
We use requestAnimationFrame() method which tells the browser that you wish to perform an animation and requests that the browser call a specified function to update an animation before the next repaint.

`let currentFrame = 0;

const update = () => {

   ctx.clearRect(0, 0, 800, 500);
   
   ctx.drawImage(
   
     mario,
     
     (MARIO_WIDTH * (Math.floor(currentFrame) % 8)),
     
     0,
     
     MARIO_WIDTH,
     
     MARIO_HEIGHT,
     
     350,
     
     250,
     
     MARIO_WIDTH,
     
     MARIO_HEIGHT
     
   );
   
   currentFrame += 0.2;
   
   requestAnimationFrame(update);
   
};

update();`

*(Slide 12.3)*
Here is a result
*(Slide 12.4)*

## Further you can see more examples of using canvas. 
*(Slides 13, 13.1, 13.2, 13.3)*

## Today all modern browsers support canvas. 
*(Slide 14)*

Unfortunately, this is a little part of examples of using canvas. But I hope you are interested in this topic.
Thank you for your attention! *(Slide 14)*
