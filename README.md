# Woof
*The canvas' best friend*

Woof is a small JavaScript library inspired by Scratch for making interactive canvas games.

## Getting Started

1) Include the Woof library in your code between the `<head>` tags.
```html
<script src="https://cdn.rawgit.com/stevekrouse/WoofJS/22feaa07aacb174a93b8d545f19a9cf14aaea7dc/woof.js"></script>
```

2) Add a canvas tag between the `<body>` tags. Give it an ID, width and height.
```html
<canvas id="project" width="350" height="500"></canvas>
```
3) Set up your Woof project by referencing the ID of your canvas.
```javascript
var project = new Woof.Project("project"); 
```
4) Add a backdrop URL (preferably of similar dimensions to your canvas).
```javascript
project.addBackdropURL("http://cdn.mysitemyway.com/etc-mysitemyway/webtreats/assets/posts/857/thumbs/tileable-classic-nebula-space-patterns-6.jpg");
```
5) Add an image.
```javascript
var rectangle = project.addImage({url: "http://www.urdu-english.com/images/lessons/beginner/shapes/shapes-pics/rectangle.png"});
```
6) Make it move with the arrow keys.
```javascript
project.every(40, "milliseconds", () => {
  if (project.keysDown.includes("LEFT")){
    rectangle.xPosition -= 5; 
  }
  if (project.keysDown.includes("RIGHT")){
    rectangle.xPosition +=5; 
  }
  if (project.keysDown.includes("UP")){
    rectangle.yPosition -= 5; 
  }
  if (project.keysDown.includes("DOWN")){
    rectangle.yPosition += 5; 
  }
});
```
7) Add a timer.
```javascript
var timer = 20;
var timerSprite = project.addText({xPosition: project.width / 2, yPosition: project.height / 2, fontSize: 20, fontColor: "white"});
project.every("1", "second", () => {
  timerSprite.text = "Timer: " + timer;
  if (timer === 0){
    project.stopAll();
  }
  timer--;
});
```

## Woof.Project

  - Create a project: `var project = new Woof.Project('canvasID');`
  - Add a backdrop: `project.addBackDropURL("http://example.com/img.jpg");`
  - Change the backdrop: `project.backdrop = 0;`
  - Create a sprite: `var sprite = project.addSprite();`
  - Stop all: `project.stopAll();`
  - Mouse X: `project.mouseX`
  - Mouse Y: `project.mouseY`
  - Mouse down?: `project.mouseDown`
  - List of keys currently pressed: `project.keysDown`
  - Is 'A' pressed?: `project.keysDown.includes('A')`
  - Do this every second: `project.every(1, "second", () => {...});`
  - Do this after one second: `project.after(1, "second", () => {...});`

## Woof.Sprite

`Woof.Sprite` represents all of the commonalities between `Woof.Image`, `Woof.Text`, and `Woof.Circle`.

When creating a new `Woof.Image`, `Woof.Text`, or `Woof.Circle`, you may use the following parameters as so:
```javascript
  // notice how we can use the same parameters for the different types
  var image = project.addImageSprite({xPosition = 0, yPosition = 0, angle = 0, rotationStyle = "ROTATE", showing = true});
  var text = project.addTextSprite({xPosition = 0, yPosition = 0, angle = 0, rotationStyle = "ROTATE", showing = true});
  var circle = project.addCircleSprite({xPosition = 0, yPosition = 0, angle = 0, rotationStyle = "ROTATE", showing = true});
```

  - Set the X position: `sprite.xPosition = 200;`
  - Change the Y position: `sprite.yPosition += 10;`
  - Set the angle: `sprite.angle = 30;`
  - Don't rotate the sprites costume when the angle changes: `sprite.setRotationStyle("NO ROTATE");`
  - Hide the sprite: `sprite.showing = false;`
  - Move the sprite in the direction of the angle: `sprite.move(10);`
  - Touching another sprite?: `if (sprite.touching(sprite2)) { ... }`
  - Mouse over this sprite?: `if (sprite.mouseOver()) { ... }`
  - Clicking on this sprite?: `if (project.mouseDown && sprite.mouseOver()) { ... }`
  - Send this sprite to the back layer: `sprite.sendToBack();`
  - Send this sprite to the front layer: `sprite.sendToFront();`
  - Point the sprite towards another sprite: `sprite.pointTowards(sprite2)`
  - Point the sprite towards an X,Y position: `sprite.pointTowards(project.mouseX, project.mouseY)`
  - Delete this sprite: `sprite.delete();`
  - Get the width: `sprite.width()`
  - Get the height: `sprite.height()`

## Woof.Image

  - Create a new image: `var image = project.addImage({url: "http://www.loveyourdog.com/image3.gif", imageWidth: 30, imageHeight: 30});`
  - Add a costume: `image.addCostumeURL("http://www.urdu-english.com/images/lessons/beginner/shapes/shapes-pics/rectangle.png");`
  - Change the costume: `image.costume = 0;`
  - Set the width: `image.imageWidth = 10;`
  - Set the height `image.imageHeight = 20;`

## Woof.Circle

  - Create a new circle: `var circle = project.addCircle({radius: 10, color: "black"});`
  - Change the radius: `circle.radius = 15;`
  - Change the color: `circle.color = "blue";`

## Woof.Text

  - Create a new text: `var text = project.addText({text: "Text", fontSize: 12, fontColor: "black", fontFamily: "arial", textAlign: "center"});`
  - Set the text value: `text.text = "Sample Text";`
  - Set the font size: `text.fontSize = 20;`
  - Set the font color: `text.fontColor = "white";`
  - Set the font color to a hex value: `text.fontColor = "#32CD32";`
  - Set the font family: `text.fontFamily = "arial";`
  - Set the text-align: `text.textAlign: "center";`

## Helper Functions

1) Get a random integer between any two numbers
```javascript
var number = Woof.randomInt(10, 20);
```
