+++ 
date = "2022-05-10"
title = "How to configure deft pro track ball on Linux"
tags = ["tool"]
+++
 Create a conf file, put it in
 `/usr/share/X11/xorg.conf.d/99-trackball.conf`

Notice the button mapping, instead of number 10, it's 1, which means I use Fn1 button as Left button;
then 2, means at 11 Fn2 button will be used as Middle button.

```conf
Section "InputClass"
        # DEFT PRO Buttons:
        #    1: Left button
        #    2: Middle button (wheel click)
        #    3: Right button
        #    4: Wheel scroll up
        #    5: Wheel scroll down
        #    6: Wheel tilt left
        #    7: Wheel tilt right
        #    8: Back button
        #    9: Forward button
        #   10: Fn1 (button on the left of the ball)
        #   11: Fn2 (button on right most)
        #   12: Fn3 (button on the above of the slide switch)
        Identifier      "Elecom DEFT Pro Trackball"
        MatchProduct    "DEFT Pro TrackBall"
	Driver          "libinput"
        Option          "ScrollMethod" "button"
        Option          "ScrollButton" "9"
        Option		"MiddleEmulation" "on"
        Option "ButtonMapping" "1 2 3 4 5 6 7 8 9 1 2 12"
EndSection