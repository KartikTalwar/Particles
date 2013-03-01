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
box.append("circle")
      .style("stroke", "white")
      .attr("r", 40)    // radius 40. You can make it bigger
      .attr("cx", 150)  // position at x
      .attr("cy", 150); // position at y
```


**Click Run!**

## Preview

![](http://i.imgur.com/ks91VST.png)


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
  d3.select(this)   // we select our circle
  .transition()     // start changing the circle
  .attr("r", 100)   // change radius to 100
  .duration(1000)   // for 1 second
  .ease("elastic"); // like an elastic band
}
```


**Click Run!**

## Preview

![](http://i.imgur.com/TUveO1C.png)


## Lets Make it Dance!

We add a new function **dance** right after the function **bounce**

```js
function dance()
{
  d3.select(this)        // select the circle
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

### See the live preview [here!](http://jsfiddle.net/kuwxT/4/embedded/result/)


## The Fun Part

Lets create a new function **marker**

```js
function marker()
{
  var arrow = d3.mouse(this);
  
  box.append("circle")             // add new circle
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
   .attr("r", 100)
   .attr("cx", 150)
   .attr("cy", 150)
   .on("mouseover", dance);
```

**To this**
```js
/*
box.append("circle")
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
    .attr("height", 600)    // no semicolon
    .on("mousemove", marker); // add this new line
```

**Save and refresh!**


## Preview

![](http://i.imgur.com/IS87E4i.jpg)


## Bonus Points

Change the background-color of the frame to black and hit refresh!

**particles.html**

```html
<style type="text/css">
#frame {
  background-color : black;
}
</style>
```

## Preview

![](http://i.imgur.com/ptD6En0.jpg)

## Extra Credit - Add Colors

```js

var i = 0;                          // new variable
var color = d3.scale.category20c(); // new variable

function marker() {
  var m = d3.mouse(this);

  box.append("circle")
     .attr("cx", m[0])
     .attr("cy", m[1])
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

View it [Live] (http://jsfiddle.net/kuwxT/10/embedded/result/)
