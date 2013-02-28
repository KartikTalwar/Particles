# Animations in JavaScript

##  D3.js

Library that uses HTML, CSS and SVG to bring data to life.

![](http://i.imgur.com/uEuFKRX.png)

## Setting Up

#### Windows

- Download and install Notepad++ [http://tinyurl.com/notepadwin](http://tinyurl.com/notepadwin)

#### Mac

- Download and install Text Wrangler [http://tinyurl.com/textwranglermac](http://tinyurl.com/textwranglermac)

Download and install Google Chrome  [http://google.com/chrome](http://google.com/chrome)


## Downloading the Template

Copy the contents into a new html file **particles.html** in your text editor!

http://tinyurl.com/particlesSetup

## Getting Started


```html
<script type="text/javascript">
```

```js
var box = d3.select("#frame")
          .append("svg")
          .attr("width", 900)
          .attr("height", 600);
```

```html
</script>
```

We create a variable **box** where we get **d3** to select the **#frame** and change its **width** and **height**

## Creating a Circle

```text
<script type="text/javascript">
```
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
```text
</script>
```

**Save Changes!**

## Preview

![](http://i.imgur.com/tSAA9Lv.png)


## Our First Animation!

Modify the lines you just wrote: 

```text
<script type="text/javascript">
  ...
```
```js
box.append("circle")
    .style("stroke", "white")
    .attr("r", 40)
    .attr("cx", 150)
    .attr("cy", 150)   // no semicolon here
    .on("mouseover", bounce); // new line
```
```text
</script>
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
```text
</script>
```

**Save Changes!**

## Preview

![](http://i.imgur.com/aCFAChO.jpg)


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

## Everything looks like this:

```html
<script type="text/javascript">

var box = d3.select("#frame")
          .append("svg")
          .attr("width", 900)
          .attr("height", 600);

box.append("circle")
    .attr("r", 100)
    .attr("cx", 150)
    .attr("cy", 150)
    .on("mouseover", dance);

function bounce()
{
  d3.select(this)
  .transition()
  .attr("r", 40)
  .duration(1000)
  .ease("elastic");
}

function dance()
{
  d3.select(this)
  .transition()
  .attr("r", 40)
  .duration(1000)
  .ease("elastic")
  .each("end", bounce);
}

</script>

```

## Preview

### See the live preview [here!](http://jsfiddle.net/kuwxT/4/embedded/result/)
