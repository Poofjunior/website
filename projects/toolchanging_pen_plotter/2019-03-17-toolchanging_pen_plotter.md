---
layout: project_entry
year: 2019
title: A Tool-Changing Pen Plotter
top_image_link: "/projects/toolchanging_pen_plotter/pics/toolchanging_pen_plotter_small.jpg"
tagline: A toolchanger proof-of-concept that's eager to be your pen pal.
---

# {{ page.title }}


<!--![](/projects/toolchanging_pen_plotter/pics/toolchanging_pen_plotter_pens.jpg){: .center-image}-->
<div class="video">
<figure>
<iframe width="560" height="315" src="https://www.youtube.com/embed/yCwlqF1J5I8?start=48&rel=0&version=3&autohide=1&showinfo=0&controls=0&mute=1&autoplay=1&loop=1&playlist=yCwlqF1J5I8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</figure>
</div>

<!--
<video src="https://i.giphy.com/media/4QFqEqtTz0mTh1jaW3/source.mp4" autoplay="" loop="" muted="" playsinline="" onerror="this.onerror=()=>{};this.src='https://i.giphy.com/4QFqEqtTz0mTh1jaW3.mp4';">
</video>
-->

<!--
<center>
<video controls autoplay name="media">
<source src="/projects/toolchanging_pen_plotter/pics/source.mp4" type="video/mp4">
</video>
</center>
-->

3D printers have come a long way, but they're only scratching the surface of what's possible with rapid-prototyping.
What if our 3D printers could do more than simply print? What if they could doodle with pens, decorate with frosting, or place electrical components on circuit boards?
My *Toolchanging Pen Plotter* proof-of-concept demonstrates the beginnings of an ecosystem where our 3D printers transform into general-purpose motion platforms.

I've been inspired by some of [E3D's early work creating their toolchanger system](https://e3d-online.com/blog/2018/03/21/tool-changer-q/).
Since the pricetag looks like it'll be out of my range, I thought: why not build my own and release it for others to enjoy too?
I'm eager to see a world where toolchanging systems become the norm, but getting there will be a matter of getting these machines in to the hands of more people first.
In my mind, kicking things off with an open-source system is critical to catalyzing the development of other areas of this ecosystem, like software support and tool types.

In designing this project, I purposefully prevented myself from using expensive machine-shop tools as much as possible.
The result is a system that is *fabricable* by anyone with access to a 3D printer, laser cutter, and some light hand tools.

This project is the first (of many!) during my time in grad school studying Human-Centered Design and Engineering.

***

## How it Works: Changing Tools
For a toolchanging system, one of the main problems-to-solve is picking-up and putting-down tools in a consistent fashion.
Here's a breakdown of my version.

### Locating Tools
When the toolchanger head picks up a tool, it needs to do so in a consistent fashion such that tools lock into the same position each time they're picked up.
To do so, I opted for a [three-groove kinematic coupling](https://dspace.mit.edu/openaccess-disseminate/1721.1/69013). In this coupling, three balls lock into three slots.
Each ball contacts the slot at exactly two points (in theory), for a total of 6 point of contact.
The conventional approach is to machine these grooves from a stiff material like steel.
In my case, to avoid relying on machine-shop tools, I created an approximation to this groove using two shoulder screws. (Dowel pins would work too!)

Here's an early proof-of-concept...

![](/projects/toolchanging_pen_plotter/pics/coupling_proof_of_concept.jpg "Early Coupling Proof-of-Concept"){: .center-image}

...followed by the latest version split across both the machine end-effector and its tool rack.

<!--
{: style="text-align: center"}
![](/projects/toolchanging_pen_plotter/pics/three_groove_coupling.jpg){: height="300px"}
![](/projects/toolchanging_pen_plotter/pics/parked_tool.jpg){:height="300px"}
-->

<div style="display:flex;">
<div style="flex:0.5; padding:0 3% 0 0">
<img src="/projects/toolchanging_pen_plotter/pics/three_groove_coupling.jpg">
</div>
<div style="flex:0.56; padding:0 3% 0 0">
<img src="/projects/toolchanging_pen_plotter/pics/parked_tool.jpg">
</div>
</div>

### Locking Tools
The kinematic coupling locates the tool, but it does nothing to actually hold it in place.
To do so, I 3D-printed a wedge plate that mounts on each tool and interlocks with a "T-shaped" twisting lock.
To lock the tool, the tool-changer head simply contacts the kinematic copuling and then twists the lock.

<!-- GIF OR GRAPHIC HERE -->

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
To hold the tool in place once parked, two laser-cut flexures apply a "squeezing" force.
These flexures are cut from Delrin, making them slippy and flexible, yet sturdy enough to take repeated cycles.

![](/projects/toolchanging_pen_plotter/pics/parking_post_flexure.gif){:.center-image}

### A Parametric Tool Base Pattern
To capture all of the above features, I created a parametric tool base used by all tools in this ecosystem.
The locking pattern stays the same, but both the tool base and the parking post can grow in size.
The idea is that we can accomodate other light-load applications beyond plotting, like pipetting, and 3D printing.

***

## How it Works: the Pen Tool

To doodle with pens and sharpies, I designed a one-size-fits-most pen holder that can hold any cylindrical tool from 5-to-10mm in diameter.

### Even More Cable Drives

To actuate the pen up-and-down, I opted for another cable drive.
Here, the "curtain work" is done by a stepper motor pulling a stretchy nylon fishing wire.
Stretchy wire is generally avoided in cable-driven systems, but here it's desirable as it puts a preload on the pen when actuated, allowing it to compensate for a not-perfectly-flat drawing surface.

<div class="video">
<figure>
<iframe width="560" height="315" src="https://www.youtube.com/embed/INWYEUltPPw?rel=0&version=3&autohide=1&showinfo=0&controls=0&mute=1&autoplay=1&loop=1&playlist=INWYEUltPPw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</figure>
</div>

A cable-driven design also keeps my tools compact and lightweight by relocating the active elements off the moving system to a stationary position.
The net result is that I can drive my system around at wicked-fast speeds without wobbling the machine.

### Handling Many Pens

My pen tool "collet" features a v-groove that accommodates cylindrical pens between 5 and 10mm.
The disadvantage of such a collet is that all pens need a software offset since each of them seat at a different spot.
Nevertheless, this problem is easily handled with most GCode interpreter boards that support the G92 command.

### Flexures Revisited

As I've recently discovered, flexures are absolutely wonderful bits of mechanical engineering theory.
By embedding a specific pattern into a material we can cause it to flex with very specific degrees of freedom.

![](/projects/toolchanging_pen_plotter/pics/pen_tool_actuating.gif){:.center-image}

I'm using two double parallelogram flexures to enable my pen tool to actuate up-and-down.
Mounting each flexure perpedicular to each other also prevents the pen collet from twisting in response to side loads as the pen drags along the paper.
(Admittedly, getting this right took a few revs, but it works well enough for a proof-of-concept.)

***

## Preliminary Demos

Ok, words aside. Let's see some plotting!

<div class="video">
<figure>
<iframe width="720" height="405" src="https://www.youtube.com/embed/yCwlqF1J5I8?start=40" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</figure>
</div>


### Coupling Tests
After some preliminary testing, it turns out that the repeatability of my mating system is *less* than 0.001".
(It actually blows my mind that a combination of "oozed" plastic parts and some shoulder screws can compete with precision that we'd normally only imagine coming from metal machined parts.)

<div class="video">
<figure>
<iframe width="640" height="360" src="https://www.youtube.com/embed/TebSZKkX770?rel=0&version=3&autohide=1&showinfo=0&controls=0&mute=1&autoplay=1&loop=1&playlist=TebSZKkX770" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</figure>
</div>

***
## Fabricable Design

For the most part, all parts in this design are either 3D-printed, laser-cut, or available off-the shelf. (Those threaded steel balls are actually [Delta-style 3D printer replacement parts](https://www.google.com/search?q=kossel+3d+printer+threaded+balls&oq=kossel+3d+printer+threaded+balls&aqs=chrome..69i57.5231j0j7&sourceid=chrome&ie=UTF-8)!)
The net result is that anyone with the building instructions, access to these fabrication tools, and some assembly know-how can reconstitute their own instance of this project!
Admittedly, there are two parts that require special tools.
The coupling's "T-lock" requires a lathe, and the carbon-fiber crossbar piece requires a cnc router (or you could [get it fabricated for ≈$50 here](http://www.cncmadness.com/home.html)).
Nevertheless, this design is a step in the right direction in putting toolchanging machines in the hands of more people.

I call this trait of being easily reproducable *fabricability*.
It's the idea that designs can be fabricated and assembled with common tools but without expert know-how.
As an extension, designs that have this property are *fabricable*, and designing with this intent can be referred-to as *design-for-fabricability*.

Fabricability matters because of the ecosystem of shared 3D printer designs.
I'm convinced that part of what makes an open-source design take flight in the community is how easily it can be reproduced.
When the RepRap open-source 3D Printer launched in 2008, the designers made an explicit choice to [maximize the number of RepRap parts that could be printable from another RepRap](https://reprap.org/wiki/Wealth_Without_Money).
In doing so, they made the design easy to reproduce, since one machine could create parts for the next.
RepRap was special in that it was a machine that could create most of its constituent parts, but most machine designs can't do this.
For those machines, fabricability fills in the gap.
It's a reminder to the designer that they design with the fabricator in mind, this character who will try to build the design, as well as the fabricator's existing knowledge and available tools.

For more on fabricability, stay tuned for some of the upcoming papers from our research lab!

### Go Forth and Build your Own
Speaking of fabricability, don't let me have all the fun.
All design files and assembly docs for the tool-changer hardware are open source and [ready-for-download](https://www.thingiverse.com/thing:3365456) with the gantry design coming in behind shortly.
May you go forth and confidently build your own! (And feel free to write to me with questions.)

![](/projects/toolchanging_pen_plotter/pics/assembly_instructions.svg){:width="640px" .center-image}

Admittedly, this project is still a work-in-progress, but this proof-of-concept is mature enough to share with the expectation that others can get similar results.
I'm eager to see more folks riff off this solution for their own tool-changing needs.

### Future Work
In the coming months, I'll be adopting this idea into my own open-source *fabricable* 3D printer which I hope to release in a few months.
I also plan to start adding software support to a motion-control project like [Klipper](https://github.com/KevinOConnor/klipper) to make this ecosystem in software usable out-of-the-box.

Odds are good that I'll learn a few things in both hardware and software along the way, so be prepared for some changes!

### Tomorrow's Ideas On-Demand
I can't wait to see a world where people lean on multi-tool motion platforms to solve odd one-off problems at home.
Getting there, though, is a matter of getting these designs out there first in a way that people can build them now.
I've done a bit of the groundwork, and my hope is that the community responds by taking my designs on to the next step.


### Resources:
* [CAD Files](https://www.thingiverse.com/thing:3365456) for my toolchanging ecosystem
* [Tool Changer Head Building Instructions](https://cdn.thingiverse.com/assets/fb/45/2a/0d/64/assembly_instructions.pdf)

### References
* [The E3D Toolchanger Video](https://twitter.com/ioshea/status/1092815054641291268) that inspired this build
