# CanvasGrid
A little JavaScript module that helps you render a proper and pixel-perfect grid on HTML5 canvas. You can add cells, images with CSS, add event listeners and more in just a few steps!!!

# Full tutorial (for version v.1)

## Part 1: A brief explanation

One day, I wanted to make a minesweeper game in JavaScript, so, I started making it! I always want compatibility and ease of use in my projects, so I used a ton of classes and configurations that sometimes I just didn't need. That's when the first version of CanvasGrid was made!!! CanvasGrid works using classes and by binding objects together. Every class has a bunch of methods to help you handle your program as if it was using HTML elements.

## Part 2: All the classes constructors

So, I told you that there are classes in my project to help you manage and handle stuff easier. It's about time to tell you everything about them. Here is a list of all the **constructors** of these classes.

#### 1: Grid class

This is the main class you need in order to use CanvasGrid. As every JavaScript class, it is construction by typing `new Grid()`, the constructor arguments are the following:

 - `HTMLCanvasElement: Canvas` Here's where you specify which canvas element you want your Grid to be rendered on. It has to be a canvas and it doesn't need any constructed contexts. Note that the canvas should be square (as of the `width` and `height` attributes, but you can change them using CSS, I warn you that there are no fixes for this and you should keep the canvas square all the time).
 - `Number (Int): CellCount` In the current version of CanvasGrid, your Grid, canvas and Cells have to be square. I don't know if this will be changed in later versions, but currently, you have to specify a single number for both width and height.
 - `Number: lineWidth` This just specifies the initial width of the lines dragged between cells. It can be changed along with multiple other possible customizations using [GridInfo](#GridInfo).

<h4 id="GridInfo">2: GridInfo class</h4>

This object applies info to a Grid. You can customize stuff like line color and width.

- `Color String: lineColor` The color of the lines separating cells.
- <code><a href="#TextureInfo">TextureInfo</a>: Background</code> Now here is where it gets a little bit confusing. For now, let's just focus on the fact that this can modify our background.

<h4 id="TextureInfo">3: TextureInfo class</h4>

This object is for rendering textures on the canvas. It is used in Grid backgrounds, [Cell Textures](#Cell) and, it later varsions, might be used even more! It is really helpful and it uses the Enum object (a deep-frozen object containing constant values to avoid useing strings). You can use colors or Images, and configure it in multiple ways!

- <code><a href="#Enum">Enum</a>.<a href="#EnumTextureType">textureType</a>: textureType</code> It has to be included in `Enum.textureType`, so it can be either `Enum.textureType.Image` to use images or `Enum.textureType.Fill` to use colors.
- <code>String/<a href="#ImageInfo">ImageInfo</a>: textureInfo</code> When it is a string, if the `textureType` argument is set to be an image, then it will specify the source of that image. If it is a string and the `textureType` is set to color, then it will just define the color to be rendered, like `"red"`, `"#ff0000"`, `"rgb(255, 0, 0)"`, `"rgba(255, 0, 0, 1)"`, `hsl(0, 100%, 50%)`, `hsla(0, 100%, 50%, 1)` and any CSS/JS-supported color!!!

<h4 id="ImageInfo">4: ImageInfo class</h4>

This is used to describe an image, hich is mostly used in a textureInfo object. You have multiple choises such as:

- `String: src` The source of the image, for example `myimg.png`, `/myimg.png`, `http://www.example.com/myimg.png`, `../myimg.png`.
- `Bool: pixelatedRender` Whether to render the image pixelated or normal. Would be useful for low resolution images such as 16x16.

<h4 id="Cell">5: Cell class</h4>

This class is used in order to create a "template" for a Cell, to place in a grid. This is helpful to if you want to copy multiple cells without reconstructing and passing information.

- <code><a href="#TextureInfo">TextureInfo</a>: textureInfo</code> All you have to do is tell the program what you want your Cell to look like when you render it. Then, to actually construct a visible cell, just use the <a href="#GridCell">following class</a>.

<h4 id="GridCell">6: new Grid(...).Cell class</h4>

This class can be constructed only if you already have a Grid object constructed. First, construct a Grid. Then, make a Cell with a specificc texture you like. And last but not least, construct a `<your grid>.Cell` object in order to use it properly.

- <code><a href="#Cell">Cell</a>: fromCell</code> The cell template you want to use for that cell.
- `Number (Int): X` The X coordinate (left to right) you want you cell to be onto the grid. It starts from 0 (first cell to the left) and ends on the last cell to the right.
- `Number (Int): Y` The Y coordinate (up to down) you want you cell to be onto the grid. As in X, it starts from 0 (first cell to the top) and ends on the last cell to the bottom.

Sometimes, this can get confusing, so here is some piece of code to help you:

```
var myG = new Grid(...); //Construct a Grid, no matter what dimensions it has.
var myCellTemp = new Cell(new TextureInfo(Enum.TextureType.Image, "myImg.png")); //Then, make a cell template constining an image in the same folder as the file and named "myImg.png"
var myCell = new myG.Cell(myCellTemp, 0, 0); //Finally, construct a cell into the Grid at position 0x0 using the "myImg" texture
```

### Part 3: All the classes properties and methods.

Now that we have covered all about class construction, let me show you all the properties and methods each object has. With the methods, you can execute commands on each object that would be hard and tiring to run without these methods and with propeties you can read stuff about each object's current state and information.

#### 1: Grid class

- #### Methods:
  - #### setCell(`Cell: fromCell`, `Number (Int): x`, `Number (Int): y`):
    Sets a cell at a specified position to the specified template cell.
