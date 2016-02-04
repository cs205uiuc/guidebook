---
layout: page
title:  "Axes in d3.js"
---

Using an axis to label your visualization is helpful in many forms of visualization
to inform the user of the data they're viewing.  By using [d3.js scales](scales.html),
one can add an axis in very few lines of code.


# Defining an axis

Given a variable that is a [d3.js scale](scales.html), an axis variable can be created
with the following code:

<pre class="prettyprint">
var yourAxisVariable = d3.svg.axis()
                             .scale( yourScaleVariable )
                             .orient("top");
</pre>

The `orient` parameter accepts `"top"`, `"left"`, `"right"`, and `"bottom"` and
denotes the direction the text labels and tick marks should extend from the axis.


# Drawing the axis

Using the `svg` variable created in the [d3.js boilerplate code](boilerplate.html),
an axis is drawn with the following code:

<pre class="prettyprint">
svg.append("g")
   .attr("class", "axis")
   .call( yourAxisVariable );
</pre>



Additionally, if your axis should not sit at the top-left, you can translate the axis.
The most common case is to move the axis to the bottom of the visualization, which
can be completed with the following code:

<pre class="prettyprint">
svg.append("g")
   .attr("class", "axis")
   .attr("transform", "translate(0," + height + ")");
   .call( yourAxisVariable );
</pre>


Similarly, translating the axis to the right is a slight modification to the translate function:

<pre class="prettyprint">
svg.append("g")
   .attr("class", "axis")
   .attr("transform", "translate(" + width + ", 0)");
   .call( yourAxisVariable );
</pre>
