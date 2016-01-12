---
layout: notes_entry
note_category: maths
file_name: quaternions
title: The Practical Boola Boola Guide to Quaternions
tagline: Rigid Body Transformations Made Easier!
---
# {{ page.title }}

## {{ page.tagline }}

![](/notes/embedded/rotary_encoder/pics/encoderIntro.jpg){: .center-image}

## The Short

Hey, quaternions are awesome!
They’re an efficient encoding of rotations in 3-space with a few nifty properties that make them far friendlier than their rotation matrix alternatives.
Since I can’t find a practical guide to using them for storing rotations, I decided: “hey–why not make one?”
Hence, this is it! By the end of this page, I hope to give you a sense of how they work and how to use them in your future 3D escapades.

## Getting a Grip on Rotations

### Rotations as Groups

First, we need a better grip on what it means to be a rotation, and that comes from from Euler’s Rotation Theorum.
We need to think about rotations a little bit differently; we need to think about them as groups.
Because rotations form a group, then the composition of two rotations is also a rotation.
In other words, let’s say I have a rigid body in three-space called a, and I rotate it some angle first about the x-axis and then some other angle about the y-axis.
It turns out that the resulting final orientation of a is the same as if I had only rotated it only once through some other angle about a different axis.
In this case, that axis is neither the x-axis nor the y-axis, but because rotations are a group, then we can guarantee that_there exists a single axis and angle such that if we were to rotate our rigid body through this angle and about this axis, it would land in the same orientation as if we had rotated it separately by the previous rotations about the x and y axes.
This is the essence of Euler’s formula.

### Folding Together Roll-Pitch-Yaw

If you've ever played with a 3D

## Quaternions--What do they look like?

In a nutshell, a quaternion is a collection of 4 numbers. We can think of them in various different ways. 

* a scalar plus a number
* a 4-tuple
* a 4-dimensional vector
* an extention of the complex numbers

All of these definitions are valid, but the authors usually pick one and stick with it.
Here's a quick breakdown of the various definitions:

* w x y z
* r i j k
* s + _v_

Ok, from this point on, I'll refer to them with the _i-j-k_ notation as I like to think of it as more explicit than the _w-x-y-z_ notation, plus it exposes the math a bit more than the scalar-plus-vector notation.

## Quaternions--What's inside that 4-tuple?

Take a look at what's inside a quaternion:
    
    <quaternion here>
    
This one encodes a rotation of 180 deg (2$\pi$ radians) about the x-axis.
Looking closely, can you tell?
Me neither!
In fact, spot-checking a quaternion that encodes a rotation isn't super easy because of _how_ that information gets encoded into the quaternion.

## Encode?

I say _encode_ because it isn't obvious at first glance to see where the scalar and number representation fit into the values of the 4-tuple.

### Unit Quaternions Only!

### Normalize!


## Resources

<a href='http://awtarlab3.engin.umich.edu/wiki/index.php/Arduino'>http://awtarlab3.engin.umich.edu/wiki/index.php/Arduino</a><br>
