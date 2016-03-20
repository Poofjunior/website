---
layout: project_entry
year: 2016
title: 60 Watt CO2 Laser Cutter
top_image_link: "/projects/60w_laser_cutter/pics/end_effector.jpeg"
tagline: a pipeline from CAD to cuts
---

# {{ page.title }}

![](/projects/60w_laser_cutter/pics/end_effector.jpeg){: .center-image}

CO2 Laser Cutters are marvelous digital fabrication tools.
If you can abstract your design away to an implementation that suits thin sheets of wood, paper, unlaminated composite, or plastic, you can realize it... mostly.
Unfortunately, off-the-shelf laser cutters are expensive, as in--20K expensive!
Yes, there are some thriftier options from overseas.
There are also some great companies in the US building low-cost versions.
Nevertheless, given that most of my design work lives in software these days, I couldn't resist tackling a mechanical challenge one more time.

***

## Designing for Calibration
Designing parts to fit together perfectly is hard.
Whether it's the coarseness of our fabrication tools or those of the vendor who's making us parts, nothing is perfect.

To design a machine that's supposed to be precise and accurate, I'm using a trick that I discovered earlier with previous gantires: make parts with adustable set points.
If the majority of my parts can be slid back-and-forth between a range of positions, one of which minimizes error, then I can just keep adjusting them until I'm satisfied.
This design concept actually gives me a bit of "wiggle room," literally, in that I can machine/chop/3D-print parts, make a few mistakes, and still get a precise machine at the end of the day.

This idea isn't anything novel. In fact, it's exactly why "alignment" of any metalworking machine is necessary before cutting parts with it.
What I'm doing is essentially pushing the responsibility of holding tight tolerances off to my measurement equipment, which is far more accurate than any of my messy garage processes for making parts.
Luckily, machinists have been operating under this idea too, so good-quality, measurement equipment is actually pretty widespread.

I'm almost certain that there's a name for this procedure; I just don't know it. For now, I'll call it "tunable design" since I can keep adjusting the positions of my parts and measuring them with my measuring tools until I'm satisfied.

This idea of "tunable design" shines in the belt tensioners.
(I'm really happy with how well these turned out.)
The Y-axis is driven with 2 open belts that are cut to length and then clamped to the moving axis with clamping plates.
Since these are timing belts, the entire length of the belt can only be shortened/lengthened in discrete steps, about one belt tooth long.
I could calculate the correct number of teeth needed to fix the belt in its final location on the gantry with the proper tension, but there are wayy too many other parts that will also need to measured and cut to exact lengths for the belt to truly fit correctly.
Furthermore, the belt length might change ever-so-slightly with age, and my entire design is hosed if it can't accommodate for a belt that becomes marginally looser over time.
Ok, it's "tunable design" to the rescue here!

![](/projects/60w_laser_cutter/pics/tuneable_design_1.jpg){: .center-image}

Pulleys are installed in their own pulley blocks, but their final placement can be slid back and forth to accommodate for both the actual number of belt teeth and the amount of tension that I want to tighten them to.
On these pulley blocks, I've affixed an aluminum plate to the back with threaded holes where I can install screws.
Adjusting the tension is just a matter of rotating these screws from the back.

![](/projects/60w_laser_cutter/pics/tuneable_design_2.jpg){: .center-image}

Now that my machine can be calibrated, it's starting to stray out of the world of hacks and into the world of engineering design! I'm pretty jazzed.
Don't worry, though. There are plenty of hot-fix and hot-glue moments up ahead that'll keep this baby from being mass-produced and sold to the masses.


***

## the Grammar of the Nuts and Bolts

***

## The Occasional Tape and Glue

***

## Breathing Freely

***

## Optics Alignment

***

## The Software Pipeline

***




![](/projects/linear_time_parallel_sorter/pics/insert_fourth_element.png){: .center-image width="430px"}



## The Takeaway

Back in college, I dreamed about cutting everything from composite costumes to modular robotics with a homebrew laser cutter.
Time flew.
Reality settled in.
Now, almost three years later, I set aside many nights over the last six months to make it happen. Three iterations later, I'm just about ready to sign off on this fellow.
This project has been a beloved exercise in CAD, machining, and software, all in efforts to assemble a pipeline from CAD to cuts.

For me, taking an idea out of my head and giving it the chance to have life in the real world is about as close as I can get to magic.

***
