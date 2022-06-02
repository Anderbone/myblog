+++ 
date = "2022-06-02"
title = "How to set up a shortcut to open/track/minimise an app on Linux"
tags = ["tool","linux"]
+++
For e.g. with yakuake, by default the shortcut is F12, you can open it or track it anywhere, just the same window. If it's focused, press F12 again gonna minimize it.

Now let's learn how to set up such a shortcut for our own whatever apps on Linux.

You need to have xorg-xprop, xdotool, wmctrl, procps-ng installed.

You'd want to set the terminal variable to your app's launch command, and set the wm_class variable based on what you see when you run xprop WM_CLASS and click on your app window. Set process to the process name of your app.

My app here is eudic. Create such a sh file somewhere:

`starter.sh`
```bash
#!/bin/zsh

terminal="/home/jiyu/Applications/eudic_3607f62f9b8228131f9f4b0f97be4cbf.AppImage"
wm_class=eudic
process=eudic

if [[ $(xprop -id $(xdotool getactivewindow) WM_CLASS) =~ \"$wm_class\" ]] {
  xdotool getactivewindow windowminimize
} else {
  wmctrl -xR $wm_class
}

pgrep -u $USER -x $process || exec $terminal &
```
Set up a customer shortcut to execute this script.