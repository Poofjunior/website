---
layout: project_entry
year: 2013
title: Machined Book Holders
top_image_link: http://farm4.staticflickr.com/3688/11476427756_dc00845716.jpg
tagline: parametric wire bending for crankin' out partz
---
#{{ page.title }}

##{{ page.tagline }}

I've been thrilled at the idea of making tools from tools. Just recently, I
was hoping to create a book-holder from bent wire. Since I wanted both the left
and right wings to be visibly identical, I needed some predictable and
repeatable manner to bend both wings. In the end, I created my first
wire-bending jig.

Wire-bending on the hobbyist level is definitely a realizable goal. I started
with a commonly available hand-crank like
[this one](http://www.amazon.com/K-S-Engineering-323-Bender/dp/B0006MZMH8/ref=sr_1_1?s=toys-and-games&ie=UTF8&qid=1387619102&sr=1-1&keywords=wire+bender).
To make the bends precise enough to form duplicates, though, I needed a
better solution.

## The Jig

At its core, the jig is  just a plate with precisely located holes drilled and
tapped using the cnc mill. What it outlines, though, are the contours of the
wire bends. By repeatedly moving the crank in and out of each shoulder screw,
the correct bend can be permanently fixed into the material.

![](http://farm4.staticflickr.com/3688/11476427756_dc00845716.jpg){: .center-image}

To make predictable bends, I first started with a Solidworks design of the
actual shape that I wanted to form.
Each of the bends has and identical bend radius. To choose that radius,
I first chose a hefty shoulder screw that could bear the load of the crank.
The radius of that shoulder screw defined the radius of the wire contours.

![](http://farm6.staticflickr.com/5546/11476976575_48d13a3ed8.jpg){: .center-image}

The bent shape was formed with the idea that
I could reproduce it from 1/8th [in.], 304-stainless steel rod.
Once the bent shape model was finished, I then super-imposed that model on the
back of a generic plate and located the hole locations using the radius of the
bends.

###Evading Those Toxic Elements

Many suppliers of different rod alloys include trace amounts of toxic species
in their metals (i.e: lead, and a few other culprits). Luckily, 304-stainless
steel didn't have any listing for trace elements of toxic metals. Since I was
intending to make many and send them to my friends, family, and professors, I
double-checked to ensure that no one would be harmed in the making of these
book-holders.

##Nylon Beams

![](http://farm3.staticflickr.com/2835/11429125645_4ab951bb3a.jpg){: center-image}

To hold the wire together, I created two nylon beams with 1/8th [in.]
holes drilled at the ends. This solution makes the  beam
fabrication much faster when compared to the original idea of
two separate plates per beam and milling a slot with a ball-endmill.

##The Output

{: style="text-align: center"}
![](http://farm6.staticflickr.com/5481/11428903836_5a72646e3d_n.jpg){: width="400px"} ![](http://farm3.staticflickr.com/2819/11428857295_1b9e3c6d82_n.jpg){: width="400px"}

The results are quite nice! The jig has stood the wear-and-tear of seven
book-holders so far, and each subsequent book holder emerges nearly identical
to the previous one. In the journey to make tools to make projects, I'm
excited to encourage others to give wire-bending a try.
