---
layout: page
title: Material Test
description: Optical system that detect the strain in material
img: assets/img/3.jpg
importance: 2
category: work
---

This was a fun project that I worked on during my time at 4D sensor, I got to build from scratch the software for an optical system that will allow the user to visualize the strain in object in real time 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include youtubePlayer.html path="assets/vid/mt.mp4" %}
    </div>

</div>
<div class="caption">
  You can see in this sample video the system in use
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
   Me testing the software, looking serious.
</div>

This projects is special form e cause it was the first ever project that I lead ( with the support and help from my senior Sasa Seles).
This application that i created had touched many aspect in coding so it was a blast creating it. These were the Technologies involved in this project:
- DotNet, C#, WPF
- Data pipelines 
- GUI Processing
- Parallel programming
- Computer vision
- Image analysis 

 <h3 class="title">The technology that inspired the project </h3>
 this project was based upon the sampling moire technique to calculate the displacement in a material. You can find more material in the paper below
<div class="publications">
  <h2 class="year">2022</h2>
  {% bibliography -f {{ site.scholar.bibliography }} -q @*[abbr= SM]* %}
</div>

