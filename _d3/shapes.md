---
layout: page
title:  "Basic Shapes in d3.js"
---

At the core of most visualizations exists a few basic shapes: rectangles,
circles, lines, arcs, and similar shapes.  This section details the basics
of simple shapes in d3.js.


## Shapes

# Rectangle

A rectangle in d3 is defined by four attributes: `x`, `y`, `width`, and `height`.
The `x` and `y` define the position of the top-left corner of the rectangle
(relative to the area it is drawn on).

Rectangles are ideal for bar charts and any square or rectangle-based visualization.

Assuming that the `svg` variable has been setup from the [boilerplate code](boilerplate.html)
and `data` has been defined to be an [array of data](dataarray.html), the following code
will draw one rectangle for each data point:

<pre class="prettyprint">
svg.selectAll("group1")
   .data(data)
   .enter()
   .append("rect")
   .attr("x", function (d, i) { /* ... \*/ })
   .attr("y", function (d, i) { /* ... \*/ })
   .attr("width", function (d, i) { /* ... \*/ })
   .attr("height", function (d, i) { /* ... \*/ });
</pre>


# Circle

A circle in d3 is defined by three attributes: `cx`, `cy`, and `r`.
The `cx` and `cy` define the center of the circle (relative to the area it is drawn on).

Circles have a broad number of uses, including plots, trees, and graphs.

Assuming that the `svg` variable has been setup from the [boilerplate code](boilerplate.html)
and `data` has been defined to be an [array of data](dataarray.html), the following code
will draw one circle for each data point:

<pre class="prettyprint">
svg.selectAll("group2")
   .data(data)
   .enter()
   .append("circle")
   .attr("cx", function (d, i) { /* ... \*/ })
   .attr("cy", function (d, i) { /* ... \*/ })
   .attr("r", function (d, i) { /* ... \*/ });
</pre>


# Line

A line in d3 is similar to a rectangle and a circle, but defined by four attributes:
`x1`, `y1`, `x2`, and `y2`.  Lines default to having no width, so an Additional
`stroke-width` is needed for any line to show up.

<pre class="prettyprint">
svg.selectAll("group3")
   .data(data)
   .enter()
   .append("circle")
   .attr("x1", function (d, i) { /* ... \*/ })
   .attr("y1", function (d, i) { /* ... \*/ })
   .attr("x2", function (d, i) { /* ... \*/ })
   .attr("y2", function (d, i) { /* ... \*/ })
   .attr("stroke-width", 1);
</pre>
