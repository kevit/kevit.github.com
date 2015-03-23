---
layout: post
title: "Setting video cam for Linux"
published: false
description: ""
category: 
tags: [linux]
---


fswebcam -d /dev/video1 --list-controls
--- Opening /dev/video1...
Trying source module v4l2...
/dev/video1 opened.
No input was specified, using the first.
Available Controls        Current Value   Range
------------------        -------------   -----
Brightness                127 (100%)      -128 - 127
Hue                       64 (50%)        1 - 127
Exposure                  700 (29%)       1 - 2372
Gain                      103 (40%)       0 - 255
Adjusting resolution from 384x288 to 352x288.
--- Capturing frame...
Captured frame in 0.00 seconds.
--- Processing captured image...
There are unsaved changes to the image.

fswebcam -S 5 -d /dev/video1 --save img12.jpg --resolution 640x480 -F 2  --set brightness=100%

nano ~/.fswebcam.conf

The contents of my config file are listed below...

device /dev/video0
input 0
loop 15
skip 20
background
resolution 320x240
set brightness=60%
set contrast=13%
top-banner
font /usr/share/fonts/truetype/msttcorefonts/arial.ttf
title "EvilEye cam-O-tron"
timestamp "%d-%m-%Y %H:%M:%S (%Z)"
jpeg 95
save /home/user/pictures/viewcam.jpg
palette MJPEG



http://manpages.ubuntu.com/manpages/natty/man1/fswebcam.1.html

