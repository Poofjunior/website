---
layout: project_entry
year: 2015
title: Laser-Cut Laser Engraver
top_image_link: "/projects/laser_cut_laser_engraver/pics/laser_cutter_3_belts.png"
tagline: the laser-cut edition
---

#{{ page.title }}

##{{ page.tagline }}

<center>
<img src={{ page.top_image_link }}
vspace="15px"
>
</center>

I completely admit that I've been charmed by watching automated machines, and my third version of these [gantries](http://www.doublejumpelectric.com/projects/core_xy/2014-07-15-core_xy/) is yet another testament to just how much I really enjoy watching them move.
In the last year, I thought I'd give these machines one last look in the hopes of designing a version that can be fabbed without needing fancy tools or breaking the bank of the everyday hobbyist.
This round, I resorted to two methods for fabrication, laser cutting (classic) and, for the first time, sls-based 3D printing.
***

## 3D Printed Pulleys
I'm still skeptical of the practicality of low-cost 3D printing solutions for functional prototypes.
(Sadly, I've witnessed my pals 3D-printing too many plates of spaghetti....)
Nevertheless, this laser cutter needed 8 custom pulleys to guide the timing belt.
When it hit me that none of these pulleys were undergoing heavy loads, and when I discovered that 8 3D-printed pulleys from Shapeways was about three times cheaper than sourcing them from SDP/SI, I opted for printing.
### Getting around the Imprecision
Since I couldn't guarantee that each pulley would print with the correct inner-diameter to achieve a slip-fit, I press-fit a bushing into each pulley to guarantee a smooth ride along the shoulder screws.
<center>
<img src="/projects/laser_cut_laser_engraver/pics/pulleys.png"
vspace="15px"
>
</center>

The gantry motors also drive the timing belt with two smaller pulleys.
Again, since I couldn't guarantee that the inner diameter of the pulley would achieve a press-fit onto the motor shaft, I oversized the hole and added a set-screw clamp collar to ensure a tight grab on the shaft.
<center>
<img src="/projects/laser_cut_laser_engraver/pics/motor_pulley.png"
vspace="15px"
>
</center>
***

## Belt Tensioning
<center>
<img src="/projects/laser_cut_laser_engraver/pics/belt_tensioner.png"
vspace="15px"
>
</center>

I think I finally nailed it after 3 iterations.
Belts can now be tensioned by unscrewing the plate with teeth slots, tensioning the belt, and retightening the screws.


## Results
All-in-all, the gantry has been working consistently for engraving materials. (Alas, no cutting.)
On my todo list is better cable management and limit switches, but for now--it works!

<center>
<iframe width="560"
height="315"
src="https://www.youtube.com/embed/VxpdXk52prE"
frameborder="0"
allowfullscreen>
</iframe>
</center>


If you're interested, feel free to ping me for the laser cut vector files.
Otherwise, I'm looking to have another improved version of this gantry (one that includes limit switches) with an Instructable in the coming months.
***
