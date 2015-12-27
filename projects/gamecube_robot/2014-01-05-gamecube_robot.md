---
layout: project_entry
year: 2014
title: GameCube Robot
top_image_link: "/projects/gamecube_robot/pics/gamecubeBot.png"
tagline: a differential drive train packed into a classic console
---
# {{ page.title }}

##{{ page.tagline }}

![](/projects/gamecube_robot/pics/GameCubeSideBySide.jpg){: .center-image}

### Update:

Building instructions for version 2 can be found online at
[instructables](http://www.instructables.com/id/RC-Nintendo-GameCube-Robot/)
and can be built without specialized equipment (i.e: a machine shop).

##Introduction

With yet another generation of game consoles on the horzion, what on earth will
we do with all of our previous consoles?  Now backlogged by two generations,
the good ol' Nintendo Gamecube sits patiently in many closets. I decided that
it deserved some fresh air, so I took mine apart and turned it into a robot.

Lacking artificial intelligence of any kind, Gamecube-Bot is
actually slightly more of an rc toy than a robot in its current state. However,
with its differential drivetrain and the ease-of-reproducability added in with
version 2, it's just begging to be loaded down with sensors for multi-robot
research problems.

##The Design

<center>
<a href="http://www.flickr.com/photos/77947059@N05/12022025236/" title="driveTrain4 by Poofjunior, on Flickr"><img src="http://farm8.staticflickr.com/7371/12022025236_feb0a83655_m.jpg" width="225" height="240" alt="driveTrain4"></a>
<a href="http://www.flickr.com/photos/77947059@N05/12021298405/" title="TransmissionsDone by Poofjunior, on Flickr"><img src="http://farm3.staticflickr.com/2811/12021298405_a9a8344367_n.jpg" width="428"  alt="TransmissionsDone"></a>
</center>

Design a high-end research-worthy robot platform on-the-cheap? Challenge
accepted. As many of us bot-designers over at
[Harvey Mudd College](http://www.cs.hmc.edu/~adobke/hmc_crl/index.html) are
learning, designing a drive train transmission takes time. Why? For us, our
biggest hump was choosing the gears needed for an acceptable gear ratio. With
brushless motors revving up to 10000[rpm], a transmission is vital to slow
down that motor to an acceptable driving speed.

###A Servo Replacement Gear Transmission (SRGT)
Choosing each gear separately from a supplier like McMaster-Carr
or SDP-SI can send us digging deep into our wallets. The solution? Find an
already-existing set of gears. In our case, a few of us have found that
the HS-815/805BB servo replacement gears work shockingly well as a full
transmission for 8-to-12[lb] differential-drive bots.
(I owe this trick to JB at the
[Secret Underwater Base / Machine Shop](http://projectsbyjb.blogspot.com/2013/07/new-project-mini-combat-robot.html)
who gave it a shot first and sent me the gear CAD files!)

This is my first shot at seriously working with gears, apart from the classic
LEGOs of my past. The main principles are like so:


* Gears of identical diametrical pitch can mesh together
* Gear ratios are given by the ratio of teeth between the driving and driven gears
* Gears mesh by mating their pitch circles tangent to each other. (Plus a wee-bit more space for added backlash)
* Common gears generally have the  worldwide-accepted pressure angle of 20 degrees
* Gears often come in standard Metric and US sizes. This is reflected in their pitch diameters

Gears mesh at the imaginary circles called their pitch circles, a property
derived from tooth count and pitch.

![](/projects/gamecube_robot/pics/meshingGears.png){:.center-image}

To make the gear stage shape a bit easier to design, I created a Solidworks
Assembly using the gear files. I resized them to their pitch diameters and
mated them tangent to each other so that I could freely position them while
ensuring that each stage touched the next. (One quick note: I actually made the
gears a wee-bit bigger than their pitch diameters, adding some backlash, to
permit the gears to spin more smoothly.)

![](http://farm4.staticflickr.com/3678/11915172665_2529be3f5b_n.jpg){: .center-image}

The pinion gear was a bit tricky to find. The servo replacement gears are
metric, and finding metric pinion gears with the right inner shaft diameter
became another hunting game that I didn't want to play--especially if I
happened to find the right gear from a limited line of one vendor's rc car.
Luckily, 64-pitch US gears can mate with their metric cousins of comparable
pitch, a feature that expanded the gear-selection wide enough to find the right
pinion gear.

###Replacement Gear Mods
<center>
<a href="http://www.flickr.com/photos/77947059@N05/12021757884/" title="HotTweezers by Poofjunior, on Flickr"><img src="http://farm8.staticflickr.com/7446/12021757884_383370071c_m.jpg" width="278"  alt="HotTweezers"></a>
<a href="http://www.flickr.com/photos/77947059@N05/12021731743/" title="TabbedServoGear by Poofjunior, on Flickr"><img src="http://farm3.staticflickr.com/2855/12021731743_6234094802_m.jpg" width="240" height="160" alt="TabbedServoGear"></a>
<a href="http://www.flickr.com/photos/77947059@N05/12022265296/" title="TabRemoved by Poofjunior, on Flickr"><img src="http://farm3.staticflickr.com/2832/12022265296_45ef3d175d_m.jpg" width="240" height="160" alt="TabRemoved"></a>
</center>

To prep the gears for continuous rotation, I had to clip off the limiting nylon
tab feature on the output gear with the spline feature. Taking a great tip from JB once more, hot 
tweezers did the trick just fine.

###Wheels and Hubs
<center>
<a href="http://www.flickr.com/photos/77947059@N05/11896808754/" title="Hubs by Poofjunior, on Flickr"><img src="http://farm4.staticflickr.com/3798/11896808754_1cca5d5355_n.jpg" width="320" height="180" alt="Hubs"></a>
<a href="http://www.flickr.com/photos/77947059@N05/11896863004/" title="HubsFinished by Poofjunior, on Flickr"><img src="http://farm8.staticflickr.com/7359/11896863004_f48ce946d6_n.jpg" width="320" height="180" alt="HubsFinished"></a>
</center>

Once again, in choosing wheels, I opted not to rip wheels out of a
vendor-specific rc car. Since LEGO wheels will (hopefully!) be around for years
to come, I designed hubs around a set of four 56145 LEGO Technic wheels from my 
old sets. (There's something special about using the old LEGO Mindstorms wheels
on a bold new robot!) An aluminum hub and 32-pitch gear from servocity.com
sandwich the wheel together (held together wih long 4-40 button-head screws).


##Machining
To ensure that the CAD files for the gear offsets would work, I made a quick
test-plate with matching gear offets in the actual design. I was fortunate to
catch small misalignment errors here, rather than in the actual part.

<center>
<a href="http://www.flickr.com/photos/77947059@N05/11850479963/" title="TestPlate by Poofjunior, on Flickr"><img src="http://farm6.staticflickr.com/5524/11850479963_a0549783f3_n.jpg" width="320" height="180" alt="TestPlate"></a>
</center>

My first shot at press-fitting the servo gear shafts resulted in a crooked 
pin. Consequently, I made a second thicker plate with matching offsets but slip-fit
holes to hold the pins as I press-fit them into the frame.

<center>
<a href="http://www.flickr.com/photos/77947059@N05/11998238204/" title="PressFitAlignment by Poofjunior, on Flickr"><img src="http://farm4.staticflickr.com/3820/11998238204_06c419aa49.jpg" width="500" height="281" alt="PressFitAlignment"></a>
</center>

Following the first transmission's completion and lubrication with silicone
spray, we gave it a spin down in the shops.

###Drive Train Initial Test
<center>
<iframe width="320" height="180" src="//www.youtube.com/embed/p8CYwb18Eh8" frameborder="0" allowfullscreen></iframe>
</center>
(That jiggly spacer was replaced!)

##Implementation
Once the two transmissions were created (correctly this time!), I zippy-tied
them together with a steel plate from an old hard drive. (Ah, having a scrap
pile is a lovely thing!) Following the crude assembly, we spun some initial
outdoor tests:

<center>
<h4> Skeletal Drive Train Outdoor Testing</h4>
<iframe width="640" height="360" src="//www.youtube.com/embed/AJMVFgwLAJs" frameborder="0" allowfullscreen></iframe>
</center>

<center>
<h4> Fully-shelled Gamecube Living Room Test</h4>
<iframe width="560" height="315" src="//www.youtube.com/embed/rBZQmiqKuV0" frameborder="0" allowfullscreen></iframe>
</center>

###Signal Mixing for Differential Drive Control
The differential drive train is driven with two brushless motors, one per side.
Each of these brushless motors is driven by a brushless motor controller that
accepts PWM input signals from the rc receiver. Since each motor is controlled
by a separate channel, these channels must be mapped to a control-stick scheme
that makes sense; otherwise, the controls are
offset by 45-degrees, making the driving experience a bit strange.
Rather than remapping the channel output signals with an
embedded board like an Arduino, it's much cheaper
to place in a V-tail mixer cable between the two channels. (They're only $3.)
(The video above is actually before I snagged a mixer.)

##Outlooks
I'm thrilled that the srg-transmission works so well, and I'd really encourage
others to take the leap! With some
more effort, I'm convinced that a cheaper laser-cuttable edition is on its way
in the near future. For the budding Arduino hobbyist, this could be the
beginning of an awesome new development platform with brushless motors.
Alas, only time will tell.

Finally, now that I've got a hardware platform to work with outside the labs, I'd like
to give some budget mouse odometry a shot to see how well I can get it to track
it's position for future state-estimation projects.

### References
* [Source Code and Original Documentation](http://www.lysium.de/blog/index.php?/archives/234-Plotting-data-with-gnuplot-in-real-time.html)
* Side-By-Side image credit to [Ben Chasnov](http://www.bchasnov.com/)
* [The Flickr Picture Feed](http://www.flickr.com/photos/77947059@N05/sets/72157639670192223/)
* [SDP/SI Notes on Metric Gears](http://www.sdp-si.com/D805/D805_PDFS/Technical/8050T007.pdf)
* [The Secret Underwater Base / Machine Shop](http://projectsbyjb.blogspot.com/), lair of the machining guru JB.
* [Harvey Mudd College Combat Robot Club Facebook Page](https://www.facebook.com/pages/Harvey-Mudd-Combat-Robot-Club/134567813384420)
