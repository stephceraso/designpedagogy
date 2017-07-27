---
layout: page
title: Collaboration
tag: Collaborative
d3: true
---

Collaborative practices are critical to design pedagogy. While many rhetoric and composition instructors already include opportunities for collaboration (in the form of small group work, peer review, and team projects), we found collaboration in design studio contexts to be more complex and layered than the ways that it typically figures into composition classrooms. During our research, we identified three primary kinds of collaboration: 1) student-student collaboration, 2) student-faculty collaboration, and 3) student-jury/clients collaboration. As writing and rhetoric instructors, student-student collaboration was the most familiar to us. Students worked in teams and often performed peer assessment. However, this kind of peer work went well beyond a single project or activity. Frequently, teams of students work together on multiple projects throughout the semester. In some cases, student collaborations span across time, continuing from one semester to the next (e.g. a student team might continue to work on the same or another student team’s project from a previous semester). The classes we observed presented a rigorous model of distributed authorship. Teamwork was a matter-of-fact practice that was necessary throughout each stage of project development—and it was frankly un-cite-able since this kind of collaboration often took place during late night design sessions. While teachers continue to provide guidance and mentorship in student-faculty collaboration, they also contribute to projects in ways that may not be recognizable to most humanities faculty. Sometimes, for instance, instructors contribute work to a student project. Also, jurors at crits are not merely critical evaluators, but often become collaborators, too. They push on and expand student ideas and offer new suggestions or possibilities. In this sense, they serve as unofficial team members; and they sometimes have multiple points of interaction, since the same jury will often make more than one appearance in a semester.

<script type="text/javascript">
  var w = 960,
      h = 500;

  var vertices = d3.range(100).map(function(d) {
    return [Math.random() * w, Math.random() * h];
  });

  var svg = d3.select("#graphic")
    .append("svg:svg")
      .attr("width", w)
      .attr("height", h);
  var paths, points, clips;
  clips = svg.append("svg:g").attr("id", "point-clips");
  points = svg.append("svg:g").attr("id", "points");
  paths = svg.append("svg:g").attr("id", "point-paths");
  
  clips.selectAll("clipPath")
      .data(vertices)
    .enter().append("svg:clipPath")
      .attr("id", function(d, i) { return "clip-"+i;})
    .append("svg:circle")
      .attr('cx', function(d) { return d[0]; })
      .attr('cy', function(d) { return d[1]; })
      .attr('r', 20);

  paths.selectAll("path")
      .data(d3.geom.voronoi(vertices))
    .enter().append("svg:path")
      .attr("d", function(d) { return "M" + d.join(",") + "Z"; })
      .attr("id", function(d,i) { 
        return "path-"+i; })
      .attr("clip-path", function(d,i) { return "url(#clip-"+i+")"; })
      .style("fill", d3.rgb(250, 250, 250))
      .style('fill-opacity', 0.5)
      .style("stroke", d3.rgb(190,230,230));

  points.selectAll("circle")
      .data(vertices)
    .enter().append("svg:circle")
      .attr("id", function(d, i) { 
        return "point-"+i; })
      .attr("transform", function(d) { return "translate(" + d + ")"; })
      .attr("r", 2)
      .attr('stroke', 'none');

  </script>



