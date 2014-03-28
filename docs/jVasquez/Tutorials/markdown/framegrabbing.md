##Framegrabbing 
###Turn a webcam and computer into a visual logging instrument

Need a simple way to log camera image data over time? Two command-line 
programs, when combined, will do just that. 
[Streamer](http://linux.die.net/man/1/streamer) can capture images 
through strictly a command-line interface. 
[FFmpeg](http://www.ffmpeg.org/about.html) will fuse images together to
form a single video file.

To log images at a specified frame rate:

    streamer -o 0000.jpeg -s 320x240 -j 100 -t 2000 -r 1 -c /dev/video1

The above command logs images beginning at 0000.jpeg and incrementing 
with a size of 320x240, for 2000 frames at a rate of 1 frame per second. 

    ffmpeg -r 30 -i %04d.jpeg -s hd480 -vcodec libx264 -vpre medium time-lapse.mp4
    
FFmpeg looks for images files with a four-place decimal at the end of the name 
and compiles it in sequential order into time-lapse.mp4 at 852x480 (hd480) 
using libx264 and the medium preset file.  


