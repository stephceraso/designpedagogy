---
layout: page
title: DIY Learning
tag: DIY
d3: true
---

Self-propelled learning is one of the most crucial aspects of design pedagogy. DIY (do-it-yourself) approaches to teaching encourage students to become responsible for their own learning without heavy-handed instruction. The main features of DIY learning environments are experimentation and productive failure. It is also highly collaborative, which we discuss in detail in the “Collaboration” section of this project. We want to stress that DIY learning is not only about students doing conceptual research on their own. Rather, it is an embodied practice in which students are given opportunities to physically tinker with materials—in both screen-based and non-screen-based contexts—in order to try out different possibilities for their projects. When an idea or material design fails during the experimentation process, students learn what does not work in order to get closer to what does work (hence, productive failure). However, it is important to recognize that students are not starting from scratch. DIY approaches rely on the fact that students have already acquired what Jenny Rice calls “para-expertise.” Rice defines “para-expertise” as “the experiential, embodied, tacit knowledge that does not translate into the vocabulary or skills of disciplinary expertise” (119). DIY draws on students’ “para-expertise,” or the knowledge they have accumulated from lived experiences, and encourages them to leverage or articulate that knowledge—to put it into practice. In other words, “para-expertise” is the engine of DIY; it is the reason why DIY approaches work. We also want to point out that while students’ independence is central to DIY learning, the teacher is not absent from this approach. Instead of providing constant direction and authority, however, the role of the teacher is to guide from a distance, and to zoom in closer when asked or needed. That is, teachers often point students to resources or research, or check in on the progress of developing projects without telling students the “right” way to do things. However, we want to be clear that DIY does not diminish the value of expert knowledge. Rather, it offers something more akin to an apprenticeship in which teachers design guided opportunities for students to learn on their own through instinctual and practical knowledge.

<script type="text/javascript">
(function() {
    var paper, circs, i, nowX, nowY, timer, props = {}, toggler = 0, elie, dx, dy, rad, cur, opa;
    // Returns a random integer between min and max
    // Using Math.round() will give you a non-uniform distribution!
    function ran(min, max)
    {
        return Math.floor(Math.random() * (max - min + 1)) + min;
    }

    function moveIt()
    {
        for(i = 0; i < circs.length; ++i)
        {
              // Reset when time is at zero
            if (! circs[i].time)
            {
                circs[i].time  = ran(30, 100);
                circs[i].deg   = ran(-179, 180);
                circs[i].vel   = ran(1, 5);
                circs[i].curve = ran(0, 1);
                circs[i].fade  = ran(0, 1);
                circs[i].grow  = ran(-2, 2);
            }
                // Get position
            nowX = circs[i].attr("cx");
            nowY = circs[i].attr("cy");
               // Calc movement
            dx = circs[i].vel * Math.cos(circs[i].deg * Math.PI/180);
            dy = circs[i].vel * Math.sin(circs[i].deg * Math.PI/180);
                // Calc new position
            nowX += dx;
            nowY += dy;
                // Calc wrap around
            if (nowX < 0) nowX = 490 + nowX;
            else          nowX = nowX % 490;
            if (nowY < 0) nowY = 490 + nowY;
            else          nowY = nowY % 490;

                // Render moved particle
            circs[i].attr({cx: nowX, cy: nowY});

                // Calc growth
            rad = circs[i].attr("r");
            if (circs[i].grow > 0) circs[i].attr("r", Math.min(30, rad +  .1));
            else                   circs[i].attr("r", Math.max(10,  rad -  .1));

                // Calc curve
            if (circs[i].curve > 0) circs[i].deg = circs[i].deg + 2;
            else                    circs[i].deg = circs[i].deg - 2;

                // Calc opacity
            opa = circs[i].attr("fill-opacity");
            if (circs[i].fade > 0) {
                circs[i].attr("fill-opacity", Math.max(.3, opa -  .01));
                circs[i].attr("stroke-opacity", Math.max(.3, opa -  .01)); }
            else {
                circs[i].attr("fill-opacity", Math.min(1, opa +  .01));
                circs[i].attr("stroke-opacity", Math.min(1, opa +  .01)); }

            // Progress timer for particle
            circs[i].time = circs[i].time - 1;

                // Calc damping
            if (circs[i].vel < 1) circs[i].time = 0;
            else circs[i].vel = circs[i].vel - .05;

        }
        timer = setTimeout(moveIt, 60);
    }

    window.onload = function () {
        paper = Raphael("graphic", 1000, 1000);
        circs = paper.set();
        for (i = 0; i < 30; ++i)
        {
            opa = ran(3,10)/10;
            circs.push(paper.circle(ran(0,1000), ran(0,1000), ran(10,30)).attr({"fill-opacity": opa,
                                                                           "stroke-opacity": opa}));
        }
        circs.attr({fill: "#00DDAA", stroke: "#00DDAA"});
        moveIt();
        elie = document.getElementById("toggle");
        elie.onclick = function() {
            (toggler++ % 2) ? (function(){
                    moveIt();
                    elie.value = " Stop ";
                }()) : (function(){
                    clearTimeout(timer);
                    elie.value = " Start ";
                }());
        }
    };
}());
</script>
