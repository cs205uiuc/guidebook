---
layout: page
title:  "Pie Charts in D3.js"
---

# Getting Started

First, open web/vis.js in the project's directory. Set up the file as follows if it is not already set up:

```javascript
function main() {
  $.getJSON("res/counts.json",
    function (jsonData){

    })
    .fail(function(d) {alert("Failed to load JSON!");})
  ;
}
```
# Preprocessing the data to be plotted

Let's jump back to the example of extracting links from Reddit posts. You may find
that you wound up with a large number of different domains but that some domains
have a very small number of links counted. This can pose a problem when trying to visualize
in a pie chart. So perhaps we should combine the smaller counts into an "Other" category.
To do this, we need to find domains with less than some arbitrary threshold and combine them together.
We can do this using a for loop.

```javascript
var other_count = 0;
var data = []
for(var i = 0; i < Object.keys(jsonData).length; i++){
  var key = Object.keys(jsonData)[i];
  // Change the number in the line below as needed. You should look at the counts to pick this number
  if(jsonData[key] < 75){
    other_count += jsonData[key];
  }
  else{
    var cur = {"label": key, "count": jsonData[key]};
    data.push(cur);
  }
}
var other = {"label": "Other", "count": other_count};
data.push(other);
```

The for loop checks if the count for each domain is below a certain threshold. If it
is, then its count gets added to the other category. If it isn't, an object is created
with its label and count and is pushed to an array.

# The Pie Chart

Then you will want to look at [the boilerplate code](boilerplate.md) and from there, take the
code to set up the svg canvas but modify it such that there are no margins for the width
and height attributes and so that the transform attribute uses the radius in place of
margin.left and margin.top. There is also a .data that provides the data array
we created above. Make sure you set the variables width, height, and r to some
appropriate value! Here is an example, including the code from above to show where
you should put your code.

```javascript
function main() {
  $.getJSON("res/counts.json",
    function (jsonData){
      var width = 1280;
      var height = 720;
      var r = height / 2;
      var color = d3.scale.category20c();
      var svg = d3.select("#chart")
            .append("svg")
            .data([data])
            .attr("width", width)
            .attr("height", height)
            .style("width", width)
            .style("height", height)
            .append("g")
            .attr("transform", "translate(" + r + "," + r + ")");
    })
    .fail(function(d) {alert("Failed to load JSON!");})
  ;
}
```

Now that we've set up the canvas, we can now set up the code for the actual pie chart.
To do that, we will use d3.layout.pie and d3.svg.arc. You want to do this after
setting up the canvas in the code.

```javascript
var pie = d3.layout.pie().value(function(d) {return d.count;});
var arc = d3.svg.arc().outerRadius(r);
// This selects and draws the paths
var arcs = vis.selectAll("g.slice").data(pie).enter().append("g").attr("class", "slice");
//This sets colors for the segments
arcs.append("path")
    .attr("fill", function(d, i){
        return color(i);
    })
    .attr("d", function (d) {
        return arc(d);
    });
```

# Labelling the sections of the chart

A pie chart isn't necessarily useful if we don't have a way of telling what segments
of the chart represents what. Let's jump to the example of links from Reddit posts.
To label the segments, we use the data as we processed it above. We append text to the
arcs.

```javascript
arcs.append("text").attr("transform", function(d){
      d.innerRadius = 0;
      d.outerRadius = r;
    return "translate(" + arc.centroid(d) + ")";}).attr("text-anchor", "middle").text( function(d, i) {
    return data[i].label;}
  ).attr("dy", ".35em");
```

The innerRadius in the above code is set to 0 because we want a full circle, not a donut.
We have the function inside .text return the label at position i in the array and the label
is aligned to the middle using the text-anchor attribute. The dy attribute rotates around the center of the text.
