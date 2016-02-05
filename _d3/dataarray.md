---
layout: page
title:  "Data Array: The ideal data for d3.js"
---

d3.js was designed to produce data driven documents, allowing for data to be
easily used in a visualization.  While d3.js has many ways to work with data,
providing d3.js data as an array greatly simplifies most tasks.


# A basic array

At a minimum, our data can be a simple array of numbers of strings.
If we want to plot grades along a line, our data may be as simple as:

<pre class="prettyprint">
var data = [100, 95, 85, 92, 74, 83, 91];
</pre>

As is the case with every d3 data accessor function, the data given from the
function is one element of the array.  In the first pass, that data would
be `100` (the first element of the array).



# An array of objects

More commonly, we want some form of structured data as our visualization.  For this,
we would us an array of dictionaries/objects.  That is, every element in our array is
a dictionary/object, as so:

<pre class="prettyprint">
var data = [
  { "fruit": "banana", "color": "yellow" },
  { "fruit": "orange", "color": "orange" },
  { "fruit": "apple", "color": "apple" }
];
</pre>

In a d3 accessor function, the data element would be the entire object.  In the
first pass, `d.fruit` would return `banana` and `d.color` would return `yellow`.
