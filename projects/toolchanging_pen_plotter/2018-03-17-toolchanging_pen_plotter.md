---
layout: project_entry
year: 2019
title: A Tool-Changing Pen Plotter
top_image_link: "/projects/toolchanging_pen_plotter/pics/toolchanging_pen_plotter_small.jpg"
tagline: A toolchanger proof-of-concept that's eager to be your pen pal.
---

# {{ page.title }}

TODO: better picture here.
![](/projects/toolchanging_pen_plotter/pics/toolchanging_pen_plotter_pens.jpg){: .center-image}

3D printers have come a long way, but they're only scratching the surface of what's possible in small-scale manufacturing.
For instance: what if our 3D printers could do more than simply print? What if they could doodle with pens, decorate with frosting, or place electrical components on circuit boards?
My *Toolchanging Pen Plotter* proof-of-concept demonstrates the possibilities of an ecosystem where our 3D printers transform into general-purpose motion platforms.

In creating this project, I purposefully prevented myself from using conventional machining tools as much as possible for a resulting design that is fabricable for anyone with nearby access to a 3D printer and a laser cutter.

This project is the first of many during my time in grad school studying Human-Centered Design and Engineering.

## How it Works
For a toolchanging system, one of the main problems-to-solve is picking-up and putting-down tools in a consistent fashion.
Here's a breakdown of my version.

### Locating Tools
When the toolchanger head picks up a tool, it needs to do so in a consistent fashion such that tools lock into the same position each time they're picked up.
To do so, I opted for a three-groove kinematic coupling. In this coupling, three balls lock into three slots.
Each ball contacts the slot at exactly two points (in theory), for a total of 6 point of contact.
The conventional approach is to machine these grooves.
In my case, to avoid relying on machine-shop tools, I created an approximation to this groove using two shoulder screws. (Dowel pins would work too!)

After some preliminary testing, it turns out that the repeatability of my mating system is smaller than 0.001".
(Hey, that's not bad for a combination of "oozed" plastic parts and some shoulder screws.)

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/TebSZKkX770" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

### Locking Tools
The kinematic coupling locates the tool, but it does nothing to actually hold it in place.
To do so, I 3D-printed a wedge plate that mounts on each tool and interlocks with a "T-shaped" twisting lock.
To lock the tool, the tool-changer head simply contacts the kinematic copuling and then twists the lock.

Locking is a closed-loop system driven by stall detection.
Here, a stepper motor remotely twists the lock through a cable.
When the motor stalls, my stepper driver chip sends a signal to the microcontroller which halts the motor.
This stall-detection signal is part of what makes this stepper driver, the TMC2660, so special.
(In fact, the datasheet actually suggests using the feature as a replacement for limit switches.)
In my setup, the benefit of using stall detection, rather than twisting to a fixed angle, is that the applied locking torque is indifferent to the wear-and-tear of each wedge plate.
Locking the motor upon stall guarantees that the tool is connected to the head regardless of how much wear-and-tear the wedge has received.

Finally, odds are good that the wedge plate on each tool will wear out after thousands of tool-changes, so I made it a consumable.
These plates can be unscrewed and replaced *without* altering the locking position where the tool engages the toolchanger head.
This last part is especially important since we only want to calibrate tool offset once ever if possible.

### Parking Tools
We need a way to park tools such that we can pick them up again later.
To do that, I made a parking post consisting of two dowel pins.
All tools have two wedge features on the side ends of the tool holder.
Parking is just a matter of sliding the tool into the pins.
Im using two laser-cut flexures to apply a "squeezing" force that holds the tool in place once the end-effector lets go.

### A Parametric Tool Base Pattern
To capture all of the above features, I created a parametric tool base used by all tools in this ecosystem.
The locking pattern stays the same, but both the tool base and the parking post can grow in size.
The idea is that we can accomodate other light-load applications beyond plotting, like pipetting, and 3D printing.

## Fabricable Design

For the most part, all parts in this design are either 3D-printed, laser-cut, or off-the shelf.
The net result is that anyone with the building instructions, access to these fabrication tools, and some assembly know-how can reconstitute their own instance of this project!
Admittedly, there are two parts that require special tools, but this design is a step in the right direction in putting toolchanging machines in the hands of more people.

I call this trait of being reproducable easily *fabricability*.
It's the idea that we can embed particular aspects into the design that make it reproducible with common tools but without expert know-how.

Fabricability matters here because of the ecosystem of shared 3D printer designs.
I'm convinced that part of what makes an open-source design take flight in the community is how easy it is to reproduce.
When the RepRap project started back in 2008, the designers made an explicit choice to [make as many of the RepRap's constituent parts printable from another RepRap](https://reprap.org/wiki/Wealth_Without_Money).

For more on fabricability, stay tuned for some of the papers that our research lab is getting ready to publish.


## Preliminary Demos

<center>
<iframe width="720" height="405" src="https://www.youtube.com/embed/yCwlqF1J5I8?start=40" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

## Future Work
Admittedly, this project is still a work-in-progress, but this proof-of-concept is mature enough to share with the expectation that others can get similar results.
The design is now [open source](https://www.thingiverse.com/thing:3365456), and I'm eager to see what other folks will do with it.

In the meantime, I'll be adopting this idea into my own open-source *fabricable* 3D printer which I hope to release in a few months.
I also plan to start adding software support to a motion-control project like [Klipper](https://github.com/KevinOConnor/klipper) to make this ecosystem in software usable out-of-the-box.

Odds are good that I'll learn a few things in both hardware and software along the way, so be prepared for some changes!

## The Future of Ideas On-Demand
I can't wait to see a world where people lean on fabricable multi-tool motion platforms to solve odd one-off problems at home.
Getting there, though, is a matter of getting these designs out there first.
I've done a bit of the groundwork, and my hope is that the community responds by taking my designs on to the next step.


### Resources:
* [CAD Files](https://www.thingiverse.com/thing:3365456) for my toolchanging ecosystem

### References
* [The E3D Toolchanger Video](https://twitter.com/ioshea/status/1092815054641291268) that inspired this build
