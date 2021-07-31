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

This object is for rendering textures on the canvas. It is used in Grid backgrounds, [Cell](#Cell) Textures and, it later varsions, might be used even more! It is really helpful and it uses the Enum object (a deep-frozen object containing constant values to avoid useing strings). You can use colors or Images, and configure it in multiple ways!

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

## Part 3: All the classes properties and methods.

Now that we have covered all about class construction, let me show you all the properties and methods each object has. With the methods, you can execute commands on each object that would be hard and tiring to run without these methods and with propeties you can read stuff about each object's current state and information.

### 1: Grid class

- ### Methods:
  - #### <h4 id="#GridMethodSetCell"><code>setCell(<code>Cell: fromCell</code>, <code>Number (Int): x</code>, <code>Number (Int): y</code>)</code>:</h4>
    - <code><b>Cell</b> fromCell</code>: The cell to set the specific coordinates to.
    - <code><b>Number (Int)</b> x</code>: The x coordinate (from left to right) to select.
    - <code><b>Number (Int)</b> y</code>: The y coordinate (from top to bottom) to select.
    
    **Description:** Sets a cell at a specified position to the specified cell template.
  
  - #### <code>removeCell(<code>Number (Int): x</code>, <code>Number (Int): y</code>, <code>Boolean: thrown (=true)</code>)</code>:
    - <code><b>Number (Int)</b> x</code>: The x coordinate (from left to right) to select.
    - <code><b>Number (Int)</b> y</code>: The y coordinate (from top to bottom) to select.
    - <code><b>boolean</b> thrown</code>: Whether to throw an error when there is nothing in the coordinates you specified.
    
    **Description:** Removes the cell in the specified position no matter what, and if you want to, it throws an error if there is nothing
  
  - #### <code>clear()</code>
    **Description:** Just clears the entire canvas.
    
  - #### <code>renderSizes(<code>Grid: _this (=Grid the command is run on)</code>)</code>
    - <code><b>Grid</b> _this</code>: The grid to run the command on. It is mostly used because of the renderAll function to run this funtion after all the images and textures are loaded and rendered because the content of `this` is changed in that scope.
    
    **Description:** Renders the lines that separate the cells of the Grid.
  
  - #### <code>renderBackground()</code>
    **Description:** Renders the background that has been specified for the Grid using the <a href="#GridMethodApplyInfo">applyInfo</a> method.
  
  - #### <code>renderCells(<code>Function: after (=this.renderSides)</code>, <code>...Any: afterArgs</code>)</code>
    - <code><b>Function</b> after</code>: Because there can be multiple high-quality images to be rendered, we have to make a funtion to be run after them, as they are loaded asyncronously.
    - <code><b>Repeated Any</b> afterArgs</code>: Pass any arguments you want to the `after` function here.
    
    **Description:** Renders all the cells in the Grid, then runs the specified function with the specified arguments.
  
  - #### <code>fixAllPos()</code>
 
    **Description:** At first, both the name and the description might be a bit hard to understand, but if you read the <a href="#CellMethodFixPos">Cell's <code>fixPos</code> method</a>, you will possibly understand it better.
  
  - #### <code>renderAll()</code>
 
    **Description:** Renders the Grid with the new changes. In fact, it first renders tha background and then it renders all the cells with the `after` function set to default (`this.renderSides`) to render the lines separating each cell.
  
  - #### <h4 id="GridMethodApplyInfo"><code>applyInfo(<code><b>GridInfo</b> info</code>)</code></h4>
 
    **Description:** Applies a <a href="#GridInfo">Gridinfo</a> object to the grid, to change how the background and lines look.

- ### Properties:
  - ### canvas
    Contains the canvas element the grid is currently rendered on.
  
  - ### ctx
    A rendering context extrancted from the canvas.
  
  - ### cells
    - Contains all the cells that have been created on the Grid.
    - The coordinate system goes like this: this.cells = [[//cells here are in Y0 [//this cell is in Y0X0], [//this cell is in Y0X1]], [//Cells here are in Y1 [//This cell is in Y1X0], [//This cells is in Y1X1]]].
    - This is currently the only way to access a cell, but you can replace a cell using the <a href="#GridMethodSetCell">setCell()</a> method.
  
  - ### events
    - Here go all of the event listeners for internal end external use. Please do not change anything in here.
    - Each element syntax is like this: `{"args":[argument ...args], "event":argument event, "listener":argument once}`
 
  - ### instantRendering
    Controls whether the Grid will automatically re-render when things change like a cell is removed.
  
  - ### lineWidth
    - The width of the line separating the cells.
    - There are setters and getters for this property
  
  - ### <h3 id="GridPropSize">size</h3>
    - The width and height of the grid in cells.
    - There is a setter for this property.
    - When this changes (in setter), all the resize event listeners are triggered.
  
  - ### cellCount
    Additional property for `size`. This one is only for getting. If it changes without changing the `size` property, then the information for both of them will be incorrect until the next resize.
  
  - ### lineColor
    - The color of the lines separating the Cells.
    - This should be changed using the [GridInfo](#GridInfo) class and the [ApplyInfo](#GridMethodApplyInfo) method.
  
  - ### background
    - A `textureInfo` object containing the background texture of the grid.
    - As `lineColor`, his should be changed using the [GridInfo](#GridInfo) class and the [ApplyInfo](#GridMethodApplyInfo) method.
  
  ### 2: Grid.Cell class
  
  
- ### Methods:
  - #### <code>addEventListener(<code>String: event</code>, <code>Function: listener</code>, <code>boolean: once</code>, <code>...Any: args</code>)</code>
    - <code><b>String</b> event</code>: The listener only listens if the event is `click` or `resize`. When it is set to `click`, it will be triggered when the user clicks on the canvas. When it is `resize`, it will be triggered when the Grid <a href="#GridPropSize"><code>size</code> property</a> changes.
    - <code><b>Function</b> listener</code>: The function to be run when the listener is triggered
    - <code><b>boolean</b> once</code>: If it is true, then the listener can only be triggered once and then it gets removed.
    - <code><b>Repeated Any</b> args</code>: The arguments to pass to the listener.
    - 
    **Description:** Adds an event listener like in normal HTML elements. Currently, there is a great drawback with this one. **You can only ADD an event listener. You can't remove it in any way, as even after removing the event from the grid, you can only remove it from the canvas element itself in a very complicated and unsafe way that requires human supervision (e.g. Through the console)**. Let me show you how you can remove an event listener from a grid. **Never use this in an automated program.**:
    ```
    >>> var myG = new Grid(...);
    <<< Grid {canvas: ..., ctx: CanvasRenderingContext2D, cells: Array(0), events: Array(0), instantRendering: false, …}
    
    >>> var myCl = new myG.Cell(new Cell(new TextureInfo(Enum.textureType.Fill, "red")), 0, 0);
    <<< Grid.Cell {Grid: Grid, Cell: Cell, x: 0, y: 0, events: Array(0), …}
    
    >>> myG.addEventListener("click", (e)=>{console.log("I got clicked!!!")});
    <<< undefined
    
    >>> var evL = getEventListeners(myG.cells[0][0]);
    <<< {click: Array(1)} //This will return this if you have added only one event listener, if that's the case, then you had better use a newer version of CanvasGrid (like 1.2).
    
    >>> myG.canvas.removeEventListener("click", evL.click[0].listener);
    <<< undefined
    
    >>> myG.cells[0][0].events = []; //Hard removal, if you have more than one event listeners, better use cell.events.splice()
    <<< []
    ```
  - ### `fixPos`
    **Description:** Fixes the position of the cell so that it refreshes when the canvas resizes. It should be binded to a Grid's 
