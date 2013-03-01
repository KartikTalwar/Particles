# Animations in JavaScript


##  D3.js

Library that uses HTML, CSS and SVG to bring data to life.

![](http://i.imgur.com/uEuFKRX.png)

## Setting Up


Open [http://jsfiddle.net/](http://jsfiddle.net/)

Click on  **External Resources** on the left and add this url:

```text
http://d3js.org/d3.v2.js
```

![](http://i.imgur.com/CPA7h4n.png)


## Getting Started


Add this in the **HTML** box

```html
<div id="frame"></div>
```

Add this in the **CSS** box

```css
#frame {
  background-color : #eee;
}
```

## Setting Up

Add this in **JavaScript** box

```js
var box = d3.select("#frame")
            .append("svg")
            .attr("width", 900)
            .attr("height", 600);
```


We created a variable **box** where we get **d3** to select the **#frame** and change its **width** and **height**

## Creating a Circle

Add this new code in the javascript box


```text
var box = d3.select("#frame")
            .append("svg")
            .attr("width", 900)
            .attr("height", 600);
```

```js
box.append("circle")         // make a circle
   .style("stroke", "white") // make the circle border white
   .attr("r", 40)            // radius 40. You can make it bigger
   .attr("cx", 150)          // position at x
   .attr("cy", 150);         // position at y
```


**Click Run!**

## Preview

![](http://i.imgur.com/GWW4jmf.png)

**Live Preview [here](http://jsfiddle.net/asr9Q/1/)**

## Our First Animation!

Modify the lines you just wrote: 

```js
box.append("circle")
   .style("stroke", "white")
   .attr("r", 40)
   .attr("cx", 150)
   .attr("cy", 150)   // no semicolon here
   .on("mouseover", bounce); // new line
```


We are telling it to **bounce** when we move our mouse over it.


## But What is Bounce?

```text
box.append("circle")
   .style("stroke", "white")
   .attr("r", 40)
   .attr("cx", 150)
   .attr("cy", 150)   // no semicolon here
   .on("mouseover", bounce); // new line
```
```js
function bounce()
{
  d3.select(this)     // we select our circle
    .transition()     // start changing the circle
    .attr("r", 100)   // change radius to 100
    .duration(1000)   // for 1 second
    .ease("elastic"); // like an elastic band
}
```


**Click Run!**

## Preview

![](http://i.imgur.com/TUveO1C.png)

**Live Preview [here](http://jsfiddle.net/asr9Q/2/)**

## Lets Make it Dance!

We add a new function **dance** right after the function **bounce**

```js
function dance()
{
  d3.select(this)          // select the circle
    .transition()          // start animating
    .attr("r", 50)         // change radius to 50
    .duration(1000)        // for 1 second
    .ease("elastic")       // like an elastic band
    .each("end", bounce);  // and then call bounce function
}
```
And change this line to call **dance** function

```js
.on("mouseover", dance); // dance instaed of bounce
```


## Preview


![](http://i.imgur.com/jICTqey.png)

**Live Preview [here](http://jsfiddle.net/asr9Q/3/)**


## The Fun Part

Lets create a new function **marker**

```js
function marker()
{
  var arrow = d3.mouse(this);
  
  box.append("circle")                // add new circle
     .attr("cx", arrow[0])            // new x coordinate
     .attr("cy", arrow[1])            // new y coordinate
     .style("stroke", "gray")         // make circle border gray
     .transition()                    // start animating
     .duration(1000)                  // for 1 second
     .attr("r", 80)                   // change radius to 80
     .style("stroke-opacity", 0.001)  // start fading previous circles
     .remove();                       // then remove older circles
}
```

## Modify these lines


**Change this**
```js
box.append("circle")
   .style("stroke", "white")
   .attr("r", 100)
   .attr("cx", 150)
   .attr("cy", 150)
   .on("mouseover", dance);
```

**To this**
```js
/*
box.append("circle")
   .style("stroke", "white")
   .attr("r", 100)
   .attr("cx", 150)
   .attr("cy", 150)
   .on("mouseover", dance);
*/
```

## Modify these lines

```js
var box = d3.select("#frame")
            .append("svg")
            .attr("width", 900)
            .attr("height", 600)      // no semicolon
            .on("mousemove", marker); // add this new line
```

**Click Run!**


## Preview

![](http://i.imgur.com/J7c0G78.png)


**Live Preview [here](http://jsfiddle.net/asr9Q/4/)**

## Bonus Points

Change the background-color of the frame to black and hit run!


```css
#frame {
  background-color : black;
}
```

## Preview

![](http://i.imgur.com/ptD6En0.jpg)


**Live Preview [here](http://jsfiddle.net/asr9Q/5/)**

## Double Bonus - Add Colors

```js

var i = 0;                          // new variable
var color = d3.scale.category20c(); // new variable

function marker() {
  var arrow = d3.mouse(this);

  box.append("circle")
     .attr("cx", arrow[0])
     .attr("cy", arrow[1])
     .attr("r", 1e-6)             // new line
     .style("stroke", color(++i)) // changed
     .transition()
     .duration(1000)
     .attr("r", 80)
     .style("stroke-opacity", 0.001)
     .remove();
}
```

## Preview

![](http://i.imgur.com/2Zd83N9.jpg)

**Live Preview [here](http://jsfiddle.net/asr9Q/6/)**

## Extra Credit

Convert the JSFiddle page to HTML, CSS and Javascript document
