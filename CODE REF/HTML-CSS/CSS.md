## Linking External CSS

```css
<link rel="stylesheet" href="./css/main.css">
```
## Reset CSS

```scss
*{
    margin: 0px;
    padding: 0px;
    box-sizing: border-box;
}
```

## Fonts

```css
p{
    font-family: "Ink Free", sans-serif;
    font-style: italic;
    font-weight: bold;
    font-size: 18px;
    // text-decoration: underline wavy blue;
    text-decoration: none;
    color: [[00AA00]]
}
```

## Borders

```scss
h1{
    border-bottom-style: solid; //targeting specific side
    // border-top-style: solid;
    border-left-style: solid;
    border-left-width: 10px;
}

p{
    padding: 4px; //space between the border and the text
    border-style: inset; //solid | dashed | dotted | double | ridged | groove |inset | outset
    border-width: 2px;
    border-color: green;
    border-radius: 20px; //rounded border
}
```

## Gradients

```scss
html{
    background: linear-gradient(red,orange);
    background-attachment: fixed; // Background extends to full length of browser window
}
```

## Background Image

```scss
html{
    background-image: url('../img/shoe1.jpg');
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover; //cover the whole screen horizontal
    background-attachment: fixed; // stretches vertically
}
```

## Margins

```scss
h1{
    border: 1px solid;
    width: 600px;
    margin-left: 100px; //space between outside the border
    margin: 50px 20px 50px 20px; //top, right, bottom, left
    margin-left: -100px; //can be used to hide parts of the element
}
```

### Aligning

```scss
h1{
    border: 1px solid;
    width: 600px;
    // aligning
    margin-left: auto; //element will stick to the right hand side | right align
    margin: auto; // element will stay centered
}
```

## Shadows

```scss
h1{
    border: 1px solid;
    width: 500px;
    padding: 25px;
    font-size: 100px;
    margin: auto;
    color: white;
    background-color: black;
	
    /*  horizontal (px)
        vertical (px)
        blur (px)
        color (name, rgb, hexColor)
    */
    
    //text shadow
    text-shadow: 5px 5px 5px yellow, -3px -3px 5px red;//two shadows, yellow and red
    
    //border shadow
    box-shadow: 5px 5px 5px darkgray;
}
```

## Pseudo Class

### Links

```scss
a:link{ //unvisited
    color: lightgreen;
}
a:visited{
    color: darkgreen;
}
```

### Buttons

```scss
button:hover{
    background-color: lightcoral;
    color: white;
}
button:active{ //button clicked or pressed down
    background-color: blue;
}
```

### Lists

```scss
li:first-child{
    background-color: palegoldenrod;
}
li:last-child{
    background-color: palegreen;

}
//select specific child n| odd | even
li:nth-child(2){ 
    background-color: lightcyan;
}
//specific formula
/* nth-child(an+b)
    a = cycle size
    n = counter (starts from 0)
    b = offset value
*/
li:nth-child(2n+0){ //every second item
    background-color: chartreuse;
}
```

## Positioning

### Text alignment

```scss
p{ //container
    border: 1px solid;
    width: 250px;
}
[[p1]]{
    text-align: left;
    line-height: 100px; // align vertically | same as the container height in px
}
[[p2]]{
    text-align: center;
}
[[p3]]{
    text-align: right;
}
```

### Float property

![](app://obsidian.md/img/htmlcss/Screenshot%202022-02-20%20173704.png)

![](app://obsidian.md/img/htmlcss/Screenshot%202022-02-20%20173725.png)

```scss
img{
    width: 30%;
    height: 30%;

    //image is set to float
    //i.e. other elements will flow around the element like text
    float: left;
    margin: 5px;
}
```

### Position property

#### Fixed

```scss
h1{
    border: 1px solid;
    background-color: yellow;
    width: 200px;

    //fixed, nothing will move it
    //position h1 left bottom fixed
    position: fixed; 
    bottom: 0px;
    left: 0px;
}
```

#### Relative

```scss
h1{
    border: 1px solid;
    background-color: yellow;
    width: 200px;

    //relative to its normal position, i.e. from its original posistion
    position: relative;
    bottom: 50px;
    left: 50px; 
}
```

#### Sticky

```scss
h1{
    border: 1px solid;
    background-color: yellow;
    width: 200px;

    //sticks to the view port when scrolling
    position: sticky;
    top:0px //remember to add this | pos when being scrolled
}
```

#### Absolute

```scss
//box 1 is ancestor of box 2
[[box1]]{
    position: relative;
    background-color: lightgreen;
    width: 200px;
    height: 200px;
    border: 1px solid;

    top: 100px;
    margin: auto;
    
}

[[box2]]{
    position: absolute;
    background-color: lightblue;
    width: 100px;
    height: 100px;
    border: 1px solid; 

    top: 50px;
    left: 50px;
}
```

## Animations

### Transformations

```scss
p{
    border: 1px solid;
    background-color: lightblue;
    width: 50px;
    text-align: center;
    font-size: 50px;
    margin: 0px;
}

[[p2]]{
    // transform: translateY(-50px);
    // transform: translateX(50px);

    transform: translate(50px, -50px);
    transform: rotateY(180deg);
    // transform: rotateZ(40deg);
    transform: scaleY(.75,.75);
    // transform: skew(45deg);

    // scale, skewY, skewX, scaleY, translateX, translateY
    transform: matrix(1,0,0,1,0,0);
}
```

### Keyframes

```scss
[[p1]]{
    border: 1px solid;
    width: 100px;
    text-align: center;
    font-size: 40px;
    margin: 0px;
    background-color: aquamarine;

    //calling animation
    animation: myOpacityAnim;
    animation-duration: 5s;
    animation-iteration-count: infinite;
}

//defining animations
@keyframes myColorAnim{
    0%{background-color: aquamarine;}
    25%{background-color: blue;}
    50%{background-color: darkblue;}
    75%{background-color: pink;}
    100%{background-color: darkviolet;}
}

//rotation animation
@keyframes myRotateAnim {
    100%{transform: rotateY(720deg);}
}

//moving animation
@keyframes myTranslateAnim {
    50%{transform: translate(100px, 10px);}
}

//scaling animation
@keyframes myScaleAnim {
    50%{transform: scale(.5,.5);}
}

//opacity animation
@keyframes myOpacityAnim {
    0%{opacity: 0;}
    50%{opacity: 1;}
    100%{opacity: 0;}
}
```

## Flexbox

```html
<body>
    <h1>flexbox demo</h1>
    <div class="container">
        <div>1</div>
        <div>2</div>
        <div>3</div>
        <div>4</div>
        <div>5</div>
        <div>6</div>
    </div>
</body>
```

```scss
.container{
    background-color: #444444;

    height: 400px;
    display: flex;
    flex-wrap: wrap; // pushed down if no room

    flex-direction: column; //displaying vertically
    flex-direction: column-reverse; //show reverse order 

    //centering horizontally items inside flex box
    justify-content: flex-start;
    justify-content: space-around; // center

    //align vertically
    align-items: center; // flex-end | flex-start
}

.container div{
    color: black;
    background-color: #999999;
    border: 1px solid black;

    width: 100px;
    height: 100px;
    margin: 5px;

    text-align: center;
    line-height: 100px;
}
```

## Center div

```scss
.container{
    background-color: #444444;

    height: 400px;
    display: flex;
    flex-wrap: wrap; // pushed down if no room

    //center x and y using flex
    justify-content: center;
    align-items: center;
}

.container div{
    color: black;
    background-color: #999999;
    border: 1px solid black;

    width: 100px;
    height: 100px;
    margin: 5px;

    text-align: center;
    line-height: 100px;
}
```


## CSS Grid

![](app://obsidian.md/img/htmlcss/Screenshot%202022-02-22%20113725.png)

```scss
//Layout elements in rows & collumns
```

### Main Concepts

![](app://obsidian.md/img/htmlcss/Screenshot%202022-02-22%20113918.png)

### Sizing

```scss
*{
    margin: 0px;
    padding: 0px;
    box-sizing: border-box;
}
.container{
    background-color: lightblue;
    height: 80vh;
    width: 100vw;

    //css grid 
    display: grid;

    //columns & rows
    // col1 width,... coln width, auto = take what is left
    //better to use fractions | auto kinda breaks though
    grid-template-columns: 1fr 2fr 1fr;

    //can use minmax, so col-2 min-width is 200px max is 2fr
    grid-template-columns: 1fr minmax(200px, 2fr) 1fr;
    grid-template-rows: 200px minmax(200px, 2fr) 1fr;

    //auto fits the items
    grid-template-columns: repeat(auto-fit, minmax(300px,1fr));
    
    //named columns
    grid-template-columns: [col-1] 1fr [col-2] 1fr [col-3] 1fr;

    // set autos size
    //if u have auto sizing and want to them to have a certain size
    grid-auto-rows: 50px;
    grid-auto-columns: 100px;


    .mainblocks{
        background-color: orange;
        border: 1px solid gray;
        font-size: 68px;
        text-align: center;
    }
}
```

### Gaps

```scss
//add gaps/margin
grid-column-gap: 10px;
grid-row-gap: 10px;

grid-gap: 20px 30px;//row, col
grid-gap: 10px; //same on both
```

### Positioning

##### Align Items

```scss
//align items vertically
align-items: center; // default stretched
//align items horizonatlly
justify-items: center;

place-items: stretch;
```

#### Align content

```scss
//align content, i.e every items with the container
align-content: center; // y, space-between, space-between, space-around,  space-evenly, end, start
justify-content: space-between; // x 
place-content: center; //x & y
```

#### Grid Areas | Laying out 

![](app://obsidian.md/img/htmlcss/Screenshot%202022-02-22%20132813.png)

```html
<body>
    <div class="container">
        <!--content and footer-->
        <div class="item header">header</div>
        <div class="item main">main</div>
        <div class="item sidebar">sidebar</div>
        <div class="item footer">footer</div>
    </div>
</body>
```

```scss
* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}
.container {
  background-color: lightblue;
  height: 80vh;
  width: 90vw;
  margin: auto;
  margin-top: 100px;

  //css grid
  display: grid;

  //set 3 columns	
  grid-template-columns: [col-1] 1fr [col-2] 1fr [col-3] 1fr;
  
  //set 3 rows  
  grid-auto-rows: 60px auto 100px;

  //defining areas
  grid-template-areas: "header header header"  //1st row
                       "sidebar main main"     //2nd row
                       "footer footer footer"; //3rd row

  .item {
    background-color: orange;
    border: 1px solid gray;
    font-size: 28px;
    text-align: center;
    border-radius: 10px;
  }

  .header {
    background-color: lightcoral;

    //assigning names
    grid-area: header;
  }
  .main {
    background-color: lightcyan;

    //assigning names
    grid-area: main;
  }
  .sidebar {
    background-color: lightgreen;

    //assigning names
    grid-area: sidebar;
  }
  .footer {
    background-color: gray;

    //assigning names
    grid-area: footer;
  }
}
```

### Gaps

```scss
//add gaps/margin
grid-column-gap: 10px;
grid-row-gap: 10px;

grid-gap: 20px 30px;//row, col
grid-gap: 10px; //same on both
```

##### Gaps

```scss
//add gaps/margin
grid-column-gap: 10px;
grid-row-gap: 10px;

grid-gap: 20px 30px;//row, col
grid-gap: 10px; //same on both
```