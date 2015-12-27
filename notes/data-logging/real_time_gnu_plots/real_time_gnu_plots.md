---
layout: notes_entry
note_category: data-logging
file_name: real_time_gnu_plots
title: Real-Time Plotting with GNU Plot
tagline:
---
# {{ page.title }}

Data Acquisition Units (DAQs) are expensive, and, in many simple cases,
overkill for plotting data in real-time to see changes. For simple plotting (i.e less than 30[hz]),
an Arduino with a serial connection can do the same trick. Of course, for
many situations, a DAQ really is the best bet, but this plotting trick (made possible by the folks at lysium.de) is handy nevertheless. You'll need their [perl script](http://www.lysium.de/sw/driveGnuPlotStreams.pl) (and a Perl installation) to make this trick work.

To stream data from the Arduino to the terminal, simply output the data via
serial connection in the following format as chars:
    
    <stream number>:<value>
    
Streaming one value over would be received as input looking like:

    0:10
    0:10
    0:10
    0:11
    0:12
    0:12
    0:12
    

A plugged-in Arduino appears in the Linux file system in the */dev* directory 
as */ttyUSBx* or */ttyACMx* where *x* is a positive integer. 

This data can be received and redirected directly to the Perl script like so:
    
    cat screen /dev/ttyACM0 115200 | ./driveGnuPlotStreams.pl 1 1 200 0 100 
    200x200+0+0 "phototransistor" 0
    
*Note: to open a connection, I sometimes need to first run the screen command,
kill the screen command, and then run the command above.*



### Resources

* [Source Code and Original Documentation](http://www.lysium.de/blog/index.php?/archives/234-Plotting-data-with-gnuplot-in-real-time.html)


