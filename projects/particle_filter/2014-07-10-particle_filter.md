---
layout: project_entry
year: 2014
title: Particle Filter Implementation
top_image_link: "/projects/particle_filter/pics/particle_filter_export.png"
tagline: a C++ Implementation of a localization algorithm with graphics rendered in OpenFrameworks
---
#{{ page.title }}

##{{ page.tagline }}

![]({{ page.top_image_link }}){: .center-image}

***

##Introduction

In robotics, answering the question "Where am I?" in a known environment is
tricky. Fortunately, a number of techniques have been developed to answer this
question, and the particle filter is one of these techniques.

Below is a quick video of my implementaton. When I started to wrap my head
around this algorithm, I realized that there aren't many bare-bones
implementations out there that expose the guts of what the particle filter is
actually doing, so I wrote one to get a better understanding of how they work.
This is the second time I code one up, so I've done my best to keep this
version clean to best expose what's going on in case I need to build off of it
later.

This was also my first foray into using OpenFrameworks, a C++ frameworks, for
visualization. I neglected to use ROS to keep the code as clean and
straightforward as possible, requiring as little external downloads as possible
to get it up and running on another machine. Here, OpenFrameworks is just
visualizing the data.

<center>
<iframe width="560" height="315" src="//www.youtube.com/embed/DY-l30yNMYU?list=UUc8qYIxKs4CkRFSN7Vdn-lw" frameborder="0" allowfullscreen></iframe>
</center>

One last note: at the time of video capture, I didn't evenly distribute the
particles throughout the map. (I've changed that in the latest version.)

Feel free to download the source code on
[Github](https://github.com/Poofjunior/ParticleFilter)

In the context of navigation on a 2D map, a particle filter can estimate
the robot's **most likely** pose (position and orientation) in that
map. Within the map, the robot's distribution of all possible poses is
messy and very difficult to model mathematically with an equation. Rather than
trying to model this distribution of poses mathematically, however, a
particle filter, instead, attempts to capture this distribution by sampling the 
it many many times. The more times we sample this distribution, the
better picture we can capture of the robot's possible distribution of poses
over the map and, ultimately, the better chance we have at estimating the
robot's true pose in the map.

In a nutshell, the particle filter tries numerous possible poses on the map,
each pose estimating how likely it is to be the particle's true pose. As the
particle filter tries more poses, some are more likely than others, and the
more likely poses are kept, while the less-likely poses are thrown out.
Eventually, as the robot contiues to sample the environment with its sensors,
only the most likely poses are kept, and they generally converge on poses
that are very likely for the actual robot.

Unfortunately, there's a catch. That is, the particle filter is
nondeterministic. Because we can't possibly span the distribution with only a
handful of possibilities, we don't know for sure if the estimate returned by
the particle filter is the true pose of the robot. Regardless, with some
tuning and sufficient computational resources, the particle filter can
converge fairly often.

##References

* [The Probabilistic Robotics Text](http://www.probabilistic-robotics.org/)
* [Prof Clark's Lecture Notes](http://www.hmc.edu/lair/E190Q/E190Q-Lecture10-PFLocalization.pdf) from HMC's Autonomous Robot Navigation Class
