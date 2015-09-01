# Common Getting Started Problems #

In order of most frequent, the following are common issues:
  1. The Kinect is not plugged in! Believe it or not!
  1. The Kinect SDK needs to be version 1.6 (http://www.microsoft.com/en-gb/download/details.aspx?id=34808)
  1. The Kinect is too far away too work.  1.0m -> 1.2m works well.
  1. Touch doesn't work but the Like button does?  Download the Touch Fix (https://code.google.com/p/ubidisplays/downloads/detail?name=UbiDisplays.exe)
  1. It crashes when I close it and try to run it again.  In this case, make sure the Ubi Displays.exe process is not running in the task manager.
  1. You are on a MacBook with a retina display.  Set your system font size to Small (100%) and drop the screen resolution down too 1080p.

# Common Usage Problems #

Once you are up and running:
  1. Plug in a mouse.  Everything is much easier to use.
  1. Touch doesn't work on websites like Bing Maps.  You will need to enable the experimental mode.  Do this by clicking the surface name i.e. "Surface 0" and checking the tick box.  _Keep in mind that not all websites support touch!_
  1. The debug inspector doesn't work!  Edit the "UbiDisplays.exe.config" file and change this bit _"%AppData%\..\Local\Google\Chrome\Application\chrome.exe"_ to your Google Chrome exe file.

# Showcase and Community Support #

We are really interested in projects which blur the line between physical objects and digital information!  Please take the time to share things you have created here: http://highwire-dtc.com/ubidisplays/community/ :-)

If you have any problems or design questions which are not addressed in this (admittedly) brief guide, please tell us here: http://highwire-dtc.com/ubidisplays/community/

Please submit bugs and issues here: https://code.google.com/p/ubidisplays/issues/list