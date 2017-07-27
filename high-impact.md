---
layout: page
title: High Impact
tag: High Impact
d3: true
---


Learning in studio environments is different from learning in other classroom spaces in large part because it is high impact. The sites we visited were all designed to include an element of risk; design pedagogy is necessarily risky and disorienting. As Randall Bass suggests, productive disorientation entails perching students at “the porous boundaries between the classroom and life experience,” where they benefit from the combined force of “social learning, authentic audiences, and integrative contexts” (“Disrupting”). Variations of each of these forces were present in every studio we visited. What Bass calls “authentic audiences,” we tend to think of in terms of varying degrees of publicness. Studio students worked publicly in a variety of ways: attempting to impact issues of importance to publics of varying sizes and compositions, defending their work in critiques (“crits”) that were often open to the public and attended by practicing professionals, engaging directly with communities and performing research in communities, and creating work for eventual public circulation. Students also encountered high impact learning practices in that studio work seems to require constantly juggling knowledge at different levels of scale, from the foundation/conceptual to the detailed nitty-gritty. This toggling generates impact because, as Casey Boyle puts it in his exploration of glitch, “when we are positioned to pay attention to in-betweens, especially the mediation work of interfaces and infrastructures, we often come to better understand how those in-betweens help configure our personal, academic, professional, and civic practices” (13). Once students find themselves navigating the public beyond a traditional classroom environment, and actively toggling between the conceptual and the applied, most studio heads hold students’ work to high, even professional standards of production. Patricia Andrasik does so with her LEEDlab by adhering to the LEED certification standards; likewise, Neil Rothman does so with his mechanical engineering students, relying on his experience as a former ASME (American Society of Mechanical Engineers) judge. Both public engagement and professional standards are vital to high impact learning.

<script type="text/javascript">

var w = 1280,
    h = 200;

var nodes = d3.range(2000).map(function() { return {radius:
Math.random() * 12 + 4}; });

var force = d3.layout.force()
    .gravity(0.05)
    .charge(function(d, i) { return i ? 0 : -1000; })
    .nodes(nodes)
    .size([w, h]);

var root = nodes[0];
root.radius = 0;
root.fixed = true;

force.start();

var svg = d3.select("#graphic").append("svg:svg")
    .attr("width", w)
    .attr("height", h);

svg.selectAll("circle")
    .data(nodes.slice(1))
  .enter().append("svg:circle")
    .attr("r", function(d) { return d.radius - 2; })
    .style("fill", d3.rgb(250, 250, 250))
    .style('fill-opacity', 0.5)
    .style("stroke", d3.rgb(190,230,230));

force.on("tick", function(e) {
  var q = d3.geom.quadtree(nodes),
      i = 0,
      n = nodes.length;

  while (++i < n) {
    q.visit(collide(nodes[i]));
  }

  svg.selectAll("circle")
      .attr("cx", function(d) { return d.x; })
      .attr("cy", function(d) { return d.y; });
});

svg.on("mousemove", function() {
  var p1 = d3.svg.mouse(this);
  root.px = p1[0];
  root.py = p1[1];
  force.resume();
});

function collide(node) {
  var r = node.radius + 16,
      nx1 = node.x - r,
      nx2 = node.x + r,
      ny1 = node.y - r,
      ny2 = node.y + r;
  return function(quad, x1, y1, x2, y2) {
    if (quad.point && (quad.point !== node)) {
      var x = node.x - quad.point.x,
          y = node.y - quad.point.y,
          l = Math.sqrt(x * x + y * y),
          r = node.radius + quad.point.radius;
      if (l < r) {
        l = (l - r) / l * .5;
        node.x -= x *= l;
        node.y -= y *= l;
        quad.point.x += x;
        quad.point.y += y;
      }
    }
    return x1 > nx2
        || x2 < nx1
        || y1 > ny2
        || y2 < ny1;
  };
}

    </script>
