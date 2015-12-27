---
layout: project_entry
year: 2015
title: Collapsing Delrin Desklamp
top_image_link: "https://farm1.staticflickr.com/260/20451926621_1257529888_z.jpg"
tagline: Homemade Illumination Equipment--2015 Edition!
---

# {{ page.title }}

## {{ page.tagline }}

I had the honor of meeting James Olander at this year's Maker Faire. This piece takes many leaps from V1 of his first laptop stand, dubbed **The Roost**. 

![]({{page.top_image_link}}){: .center-image}

***

## Another Lamp??

Ok, I completely admit that I have a staggering affection for desklamps.
Luckily, from a functional standpoint, they're undergoing some pretty light loads, so the choice of materials doesn't play a huge role in making a desklamp that doesn't collapse under its own weight!
In that sense, it's perfectly OK for lamps to come in all shapes and sizes, so they're a great chance to practice different types of fab techniques.
Desklamps are also **just practical enough** that I can feel justified making them over and over agin--and possibly handing out the previous models to my parents/pals.
("Really, Joshua? The one I had on my desk right now was fine already....")

Last year's desklamp was a challenge in parametrically "making things" with just a laser cutter and without the resources of a fully-blown machine shop.
Between that desklamp and GameCube-bot V2, I'd call it a success, though there were some growing pains.
It turns out that the laser cutter has its own vocabulary of techniques for predictably and repeatedly "making parts."
To that extent, I promise to document my findings in a later post.

<!--
Here's a quick recap of what I learned from using a 60[W] CO2 laser cutter last year with a promise now that I'll cover it further in-depth later.
-->

<!-- Frank and confident, but honest and convincing in a "trust-me" sort of way -->
<!--

### Materials

* Acrylic is clear, flat, and horribly brittle.
While it cuts better than almost any other material, it cannot be put under serious stresses of any kind without risking shattered parts.
By "cuts better," it turns out that the CO2 laser cutter's heat from the beam, quite literally, *undoes* the acrylic-forming reaction, which is why laser-cut acrylic edges are so darn smooth.
By "serious stresses," forget about trying to assemble anything with press-fits, tabs, and/or slots of any kind with acrylic.
It's so brittle that it's just not repeatable. Nevertheless, it's great for optically-clear surfaces, it etches well for displaying frosted images, and it can be glued together.
It also tends to be consistently sold flat, so it tends to lie flat on the laser cutter bed, rather than arching upwards with warped edges.
* Wood is strong, smelly, and knotted.
Hobby plywood is sold anywhere from 1/64th[in] to 3/8[in], and this entire range can be cut with a laser cutter.
The downside is that you'll have a smokin' burned edge since the laser is, of course, burning through.
Since the cellulose in wood isn't a perfectly uniform continuum like some other materials, some parts cut a bit more easily than others.
At the end of the day, just avoid the knots.
Wood can deform when it gets wet or under its own weight while it's waiting to jump into your arms off the store shelves, so you might have to hunt around for a nice flat piece that will rest in the cutting bed more uniformly and produce flat parts.
Wood also gets the added bonus in that it can serve as the base layer for composite layups for flat parts made from a sandwich of fiberglass-wood-fiberglass.
* Delrin is this strong, flexible, and **not-in-any-way** glueable stuff-of-the-gods.
OK, it was created by DuPont, but it has many properties that make it excellent for rapid prototypes, and it's my go-to material for lasing parts that need to hold tight tolerances between features and need to bear loads.
In the real world, people capitalize on just how-darned-slippery Delrin is to use it for bearings and bushings that will take a lot of wear.
We can lase out bushings too if we wanted, but Delrin has other uses. Under static loading, Delrin bends before it breaks, unless it receives a fast impact (in which case it shatters not unlike acrylic).
This bending characteristic give it a higher ultimate strength when compared to Delrin at the cost of some "flimsiness."
That said, the overall stength is sufficient enough to make structural components that can bear loads.
When I work with Delrin in a way where it needs to be flat, I generally add in extra reinforcement features to ensure that the flat parts stay flat.
Delrin lases very well with a laser cutter of sufficient power, although not quite as well as acrylic.
Delrin can accept press fits and slip fits very predictably, which means you can stick shafts into it, put threads in it, and join pieces together that have tabs and slots--no problem! You'll likely need a vise or arbor press to press-fit parts together.
This press-fitting detail is a godsend, since absolutely nothing sticks to Delrin via glue.
Long-story-short, Delrin is so chemically inert, smooth, and flexible that it simply breaks off of glue and epoxies, mostly because **(a)** the glues have nowhere to "seep in," and **(b)** Delrin is far less brittle than the brittle epoxies that it can be simply peeled off.
No gluing Delrin. Period. End-of-story. (Melting it together, however, is a different story.) Delrin warps under its own weight over time, so store it flat.

## Drawbacks of Lasing parts

* the dreaded taper
* pocket and edge dimensions aren't as good/repeatable as relative dimensions
* internal stresses in the cut material causes warping
-->

As much as I enjoy handicraft, when it comes to "making things," I'll kick myself into putting the most creative effort into the novelty of the design, the "easy of repeatability" across duplicates, and the type of interaction that the design has within its intended space.
In other words, my hands are pretty-much-crap at finesse and precise fingerwork, so I need to rely on machines to get the tricky parts done, *and*, hopefully, these darned widgets--which I now have 10 of--actually **do something** useful so that I can (get them off my desk) give them out to people without any raised eyebrows.

***

## The Design

Since I constantly seem to be moving, I wanted something collapseable enough to stuff somewhere into the back of my car for transit.


![](https://farm1.staticflickr.com/418/20257713610_9183dee97f_c.jpg){: .center-image}

This piece was a strange exercise in finding "stable" configurations of the joints in their final form.

![](https://farm1.staticflickr.com/478/20258990159_44677aecb0.jpg){: .center-image}

For the upper section I combined a prismatic and sliding joint so that I could rotate out the LED and then slide it out to lock.
The square tubing also resists torsional bending well enough such that the lamp doesn't continuously sway back and forth when it gets jostled by studious foreheads and elbows.


![](https://farm1.staticflickr.com/526/19824739413_463191ecee.jpg){: .center-image}


The center two joints of the lamp *would form* a *four-bar linkage* without additional modifications.
Four-bar linkages are pretty common when people design cranks and rockers where some of the joints will rotate freely.
I wanted to the arm joints to remain fixed, so I put extra material into the center piece to act as a "hard-stop" such that the four-bar linkage would remain rigid once the free bar was slotted into place.

![](/projects/collapsing_delrin_desklamp/pics/triangle_length_diagram.png){: .center-image}


For the sliding joint, I did some quick back-of-the-envelope checks with a Solidworks reference sketch to make sure that the sliding clip would freely slide down (to deploy the legs) and up (to retract them). The sliding clip and legs each form a truss-like triangle.
To get the sliding clip to fully retract from the open configuration, the sum of the lengths of the joint-to-joint leg distance and the leg supports needed to be equal to the same value.
**a<sub>1</sub> + b<sub>1</sub> = a<sub>2</sub> + b<sub>2</sub>**
(See image above.)


![](https://farm1.staticflickr.com/456/20445809035_1296b6efeb.jpg"){: .center-image}

The sliding clip that actually locks the legs in place hails from the design of [James Olander's] Roost.
In a nutshell, the pull-tab that releases the legs is springloaded, where the spring is directly embedded into the Delrin.
The partly-exposed version above exposes the spring.
All-in-all, this part needs a little work as the tab doesn't completely line up with the slot.

***


## Field Testing

Out on the desk, the lamp fares quite well! The wires tuck neatly into the square tubing, but I had to live with having them sticking out at the bends. (I borrowed the circuit from [last year's lamp]() to get this one up-and-running).

***
