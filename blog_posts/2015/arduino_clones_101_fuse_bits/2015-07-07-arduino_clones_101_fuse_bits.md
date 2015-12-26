---
layout: blog_post_entry
date: Jul
day: 7
year: 2015
title: "Arduino Clones 101: Fuse Bits"
top_image_link: "/blog_posts/2015/arduino_clones_101_fuse_bits/pics/avr_programming.png"
---

<center>
<img src="{{ page.top_image_link }}"
vspace="15px">
</center>

# {{ page.title }}


<p align="right">
{{page.date}} {{page.day}}, {{page.year}}
</p>
***
The Arduino toolchain does a wonderful job of hiding away unnecessary complexity that would otherwise prevent us from building up projects quickly. The compilation procedure with avr-g++, the uploading process with an ISP (in-system programmer), and the pre-configuration of the chip via its fuse bits are all hidden parts of this process. But what happens when you need to “go off the deep end” and build an Arduino-compatible circuit board from scratch? In these cases we need to dig down to the level of embedded systems engineers and understand how things work at the low level so that we can put together a working system.

In this post, I thought I’d get started introducing the Arduino toolchain and then drop down a few notes about the fuse bits.

## What are these Fuse Bits? Why do they matter?
Fuse bits are a concept hidden to us if we’re programming Arduino Boards through the IDE. If we’re making our own Arduino-compatible PCB, though, we need to know what they are and how they affect our board.

Fuse bits refer to programmable settings for the microcontroller that tell it information about its hardware configuration. While they’re not one-time-programmable it is possible to (more-or-less) brick your setup if you upload the wrong fuse bits. Put another way, since these fuse bits tell the microcontroller important things such as: “what is my clock source?” and “should I disable reprogramming?”–it is possible to tell the microcontroller that it’s configured in a way that doesn’t match its actual configuration, in which case it may or may not listen to you.

Rest assured, there are calculators, forums, and blog posts that can give us an idea of what fuse bits we want to set before we actually write them over.

## Which Fuse Bits do I set?
Which fuse bits you'll want to set depends on your configuration. Fuse bits give the chip information as to

* what clock source
* disable programming
* enable/disable clock prescaling for a slower processor speed
* enable/disable brownout detection to reset the device below certain input voltage supply thresholds
* set the starting address of program memory

Which features to enable/disable are up to your particular scenario. Here are some general guidelines:

* Disable brown-out detection unless you need it
* Keep the starting address of program memory at the default value unless you want to squeeze out more/less program space for some purpose
* Enable Programming __Otherwise you won't be able to reprogram the chip after writing the fuse bits!__
* Disable clock prescaling (unless you need to save power)
* __Choose the clock source that you're actually using, and give it a 65[ms] delay time unless you can be sure that the oscillator (internal or external) is stable and ready before that window when the system boots up!__

__Careful!__ If you either disabled programming or your chosen clock source is incorrect, it may be very difficult to get your system back into a working state where you can talk to it again.

## Writing over the Fuse Bits
Before going any further, make sure you’ve got avrdude, the flash utility, installed. Luckily, if the Arduino IDE is installed, then you get avrdude with it for free. I’m using the command line on Linux for this one. (You can do this on Mac and Windows, also.) It’s a three-line incantation, one for each group of fuse bits. Assuming our desired lfuse, hfuse, and efuse are 0xe2, 0xd9, and 0xff respectively, our command-line input would look like this:
    
    avrdude -c usbtiny -p atmega328p -U lfuse:w:0xe2:m
    avrdude -c usbtiny -p atmega328p -U hfuse:w:0xd9:m
    avrdude -c usbtiny -p atmega328p  -U efuse:w:0xff:m
    
As each line is written, you’ll get a verification from avrdude. If you get something that says rc=-1, then avrdude can’t connect to your board for some reason. Either the power isn’t connected, the fuse bits are misconfigured to begin with, or there’s something wrong with the pcb design.

Keep in mind that these fuse bits are specific to the microcontroller. (i.e: An atmega32u4, the chip one on the Leonardo, will have different fuse bits from an atmega328p, the chip on the Uno.)

## ATMega328P with the Internal Oscillator
For an 8-bit Arduino Clone using the internall oscillator (instead of an external crystal or clock reference), the fuse bits for a typical use case are likely:
    
* lfuse: 0xe2
* hfuse: 0xd9
* efuse: 0xff

Specifically, these settings are:

* Internal Oscillator as clock source with 65[ms] startup delay [(What's startup Delay?)](http://www.ladyada.net/learn/avr/fuses.html)
* No clock division
* default starting address
* enable programming over SPI
* disable brown-out detection

Need something slightly different? Check out this wonderful [AVR Fuse Calculator](http://www.engbedded.com/fusecalc/)
