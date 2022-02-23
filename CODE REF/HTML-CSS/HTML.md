## Comments
```html
<!-- this is a comment-->
```
## Text formatting

![[Screenshot 2022-02-19 195043.png]]

```html
<body>
    This is normal text <br>
    This is <b>bold</b> text <br>
    This is <i>italic</i> text <br>
    This is <sub>subcript</sub> text <br>
    This is <sup>supercript</sup> text <br>
    This is <small>text</small> text <br>
    This is <big>big</big> text <br>
    This is <ins>inserted</ins> text <br>
    This is <del>deleted</del> text <br>
    This is <mark>marked</mark> text <br>
</body>
```

## Links & Images

### Links

```html
<body>
    <!--this is a link-->
    <a href="http://www.google.co.nz">google</a>

    <!--open link in new tab-->
    <a target="blank" href="http://www.google.co.nz">google</a>

    <!--download-->
    <a href="./img/shoe1.jpg" download="download-name">download shoe img</a>
</body>
```

##### Images

```html
<body>
   <!--local image, use alt in case image fails to load--> 
   <img src="./img/shoe1.jpg" alt="incase image couldn't load" height="50%" width="50%">

   <!--link from a website-->
   <img src="https://images.unsplash.com/photo-1645161214666-ba24b9575a90?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=687&q=80" alt="">

   <!--image as a link-->
   <a href="https://en.wikipedia.org/wiki/The_Lord_of_the_Rings"><img src="./img/shoe2.jpg" alt="shoe" width="50%" height="50%"></a>  
</body>
```

#### Lists

##### Unordered List

```html
<!--un ordered list-->
<ul style="list-style: none;">
    <li>bread dough</li>
    <li>tomato sauce</li>
    <li>cheese</li>
    <li>pepper</li>
</ul>
```

##### Ordered List

```html
<h3>To do list</h3>
<!--type is what the list is incremented by. i.e numbers(1||100), abc(a|A), roman numerals(i|I)-->
<!-- start with b-->
<ol type="a" start="2">
    <li>step 1</li>
    <li>step 2</li>
    <li>step 3</li>
</ol>
```
##### Description List

```html
<!--a list with a item and its description-->
<dl>
    <dt>html</dt>
    <dd>- description</dd>
    <dt>css</dt>
    <dd>- Lorem ipsum dolor, sit amet consectetur adipisicing elit.</dd>
    <dt>javascript</dt>
    <dd>- Lorem ipsum dolor sit, amet consectetur adipisicing elit.</dd>
</dl>
```
##### Nested List

```html
<ul>
    <li>bread dough</li>
    <li>cheese</li>
    <li>extra toppings
        <ul>
            <li>cheese</li>
            <li>bacon</li>
            <li>shrimp</li>
        </ul>
    </li>
</ul>
```

#### Tables

```html
<h3>Personal finances :(</h3>

<table border="1" bgcolor="black">
    <tr bgcolor="grey"><!--table row-->
        <th>month</th><!--table heading-->
        <th>January</th>
        <th>February</th>
        <th>March</th>
    </tr>
    <tr bgcolor="yellow"><!--table row-->
        <th>income:</th><!--heading-->
        <td>$1500</td><!--table data-->
        <td>$800</td>
        <td>$500</td>
    </tr>
</table>
```

#### Add Video

```html
<!-- supported formats mp4, webm, ogg-->
<!--remove controls tag if u don't want user to interact with the video-->
<video width="50%" autoplay controls loop muted>
    <source src="./vids/vid1.mp4">
</video>
```

#### Buttons

```html
<button name="btn" type="button">click me</button>
<button name="submit" type="submit" value="Submit">submit</button>
<button name="reset" type="reset" value="Reset">reset</button>

<button disabled>disabled</button>
<button autofocus>autofocus</button>
<button onclick="alert('msg')">alert</button>
```

#### Forms

```html
<form action="do_something.php">
    <!--for name must match input id-->
    <label for="fname">First Name:</label><input placeholder="spongebob" type="text" name="fname" id="fname">
    <br><br>
    <label for="lname">Last Name:</label><input placeholder="squarepants" type="text" name="lname" id="lname">

    <input type="reset">
    <input type="submit">
</form>
```

##### Reset & submit buttons

```html
<!-- buttons-->
<input type="reset">
<input type="submit">
```

##### Radio buttons

```html
<label for="Mr.">Mr.</label>
<input type="radio" value="Mr." id="Mr." name="title">

<label for="Mrs.">Mrs.</label>
<input type="radio" value="Mrs." id="Mrs." name="title">
```

##### Selection Dropdowns

```html
<!--selection drop down-->
<label for="payment">Payment:</label>
<select name="payment" id="payment">
    <option value="visa">Visa</option>
    <option value="mastercard">Mastercard</option>
    <option value="giftcard">Gift Card</option>
</select>
```

##### Email

```html
<!-- email-->
<label for="email">Email:</label>
<input type="email" name="email" id="email" placeholder="s.squaroants@gmail.com">
```

##### Date

```html
<label for="data">Birth Date:</label>
<input type="date" name="date" id="date" min="2000-01-01">
```

##### Number

```html
<label for="number">Quantity</label>
<input type="number" id="number" name="number" min="0" max="99">
```

##### Telephone

```html
<!--telephone-->
<label for="tel">Telephone:</label>
<input type="tel" name="tel" id="tel">
```

##### Password

```html
<label for="password">Password</label>
<input type="password" name="password" id="password" maxlength="12">
```

##### Range

```html
<br><br>
<!--range | star rating | steps = 100/25 = 4 + 1 -->
<label for="slider">Rate us</label>
1<input type="range" step="25" value="75">5
```

##### Checkbox

```html
<!--checkbox -->
<label for="checkbox">Checkbox</label>
<input type="checkbox" name="checkbox" id="checkbox">
```

##### Checkbox

```html
<!--upload file-->
<label for="myfile">Upload file:</label>
<input type="file" name="myfile" id="myfile" accept=".txt">
```

#### Meta Tags

```html
<title>Document</title>
<!--meta tags-->
<meta charset="UTF-8">
<meta name="keyword" content="html, tutorial, youtube">
<meta name="description" content="this is html tutorial">
<meta name="author" content="dylan">
<!--more readable in mobile-->
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<!--refresh after 3 seconds-->
<meta http-equiv = "refresh" content="3">
```

#### Navigation

```html
<body>
    <h1>nav bar demo</h1>
    <nav>
        <ul>
            <li><a href="">Home</a></li>
            <li><a href="">About</a></li>
            <li><a href="">Contact</a></li>
        </ul>
    </nav>
</body>
```

````scss
nav{
    ul{
        list-style: none;
        padding: 0px;
        margin: 0px;
        overflow: hidden;
        background-color: #444444;
        border-radius: 2px;

        li a{
            float: left;
            display: block;
            color: wheat;
            text-align: center;
            padding: 2px 15px;
            border-right: 1px solid black;
            text-decoration: none;
        }
        li a:hover{
            background-color: #222222;

            animation: glow;
            animation-duration: 1s;
            animation-iteration-count: infinite;
        }
    }
}

@keyframes glow {
    50%{text-shadow: 0px 0px 10px yellow;}
}
````



## ::: CSS :::

#### Linking External CSS

````css
<link rel="stylesheet" href="./css/main.css">
````

#### Fonts

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

#### Borders

````scss
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
````

#### Gradients

````scss
html{
    background: linear-gradient(red,orange);
    background-attachment: fixed; // Background extends to full length of browser window
}
````

#### Background Image

````scss
html{
    background-image: url('../img/shoe1.jpg');
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover; //cover the whole screen horizontal
    background-attachment: fixed; // stretches vertically
}
````

#### Margins

````scss
h1{
    border: 1px solid;
    width: 600px;
    margin-left: 100px; //space between outside the border
    margin: 50px 20px 50px 20px; //top, right, bottom, left
    margin-left: -100px; //can be used to hide parts of the element
}
````

##### Aligning

````scss
h1{
    border: 1px solid;
    width: 600px;
    // aligning
    margin-left: auto; //element will stick to the right hand side | right align
    margin: auto; // element will stay centered
}
````

#### Shadows

````scss
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
````

#### Pseudo Class

##### Links

````scss
a:link{ //unvisited
    color: lightgreen;
}
a:visited{
    color: darkgreen;
}
````
##### Buttons

````scss
button:hover{
    background-color: lightcoral;
    color: white;
}
button:active{ //button clicked or pressed down
    background-color: blue;
}
````

##### Lists

````scss
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
````

#### Positioning

##### Text alignment

````scss
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
````
##### Float property

<img src="img/htmlcss/Screenshot 2022-02-20 173704.png" style="zoom: 50%;" />

<img src="img/htmlcss/Screenshot 2022-02-20 173725.png" style="zoom:50%;" />

````scss
img{
    width: 30%;
    height: 30%;

    //image is set to float
    //i.e. other elements will flow around the element like text
    float: left;
    margin: 5px;
}
````
##### Position property

###### Fixed

````scss
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
````

###### Relative

````scss
h1{
    border: 1px solid;
    background-color: yellow;
    width: 200px;

    //relative to its normal position, i.e. from its original posistion
    position: relative;
    bottom: 50px;
    left: 50px; 
}
````

###### Sticky

````scss
h1{
    border: 1px solid;
    background-color: yellow;
    width: 200px;

    //sticks to the view port when scrolling
    position: sticky;
    top:0px //remember to add this | pos when being scrolled
}
````

###### Absolute

````scss
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
````

#### Animations

##### Transformations

````scss
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
````

#### Keyframes

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

#### Flexbox

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

#### Center div

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

#### RESET CSS

```scss
*{
    margin: 0px;
    padding: 0px;
    box-sizing: border-box;
}
```

#### CSS Grid

<img src="img/htmlcss/Screenshot 2022-02-22 113725.png" style="zoom: 67%;" />

```scss
//Layout elements in rows & collumns
```

##### Main Concepts

<img src="img/htmlcss/Screenshot 2022-02-22 113918.png" style="zoom:67%;" />

##### Sizing

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

##### Gaps

```scss
//add gaps/margin
grid-column-gap: 10px;
grid-row-gap: 10px;

grid-gap: 20px 30px;//row, col
grid-gap: 10px; //same on both
```

##### Positioning

###### Align Items

```scss
//align items vertically
align-items: center; // default stretched
//align items horizonatlly
justify-items: center;

place-items: stretch;
```

###### Align content

```scss
//align content, i.e every items with the container
align-content: center; // y, space-between, space-between, space-around,  space-evenly, end, start
justify-content: space-between; // x 
place-content: center; //x & y
```

###### ** Grid Areas **

<img src="img/htmlcss/Screenshot 2022-02-22 132813.png" style="zoom:50%;" />

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

##### Gaps

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











