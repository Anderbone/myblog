+++ 
date = "2020-05-04"
title = "Autohotkey/Autokey scripts for Dynalist"
tags = ["tool", "dynalist"]

+++
#### Autohotkey 
##### Picture

Suppose the picture link is in your clipboard, to put a picture in Dynalist(or any markdown editor)
In your clipboard you have a picture link like https://i.imgur.com/XH472FR.png

Click Alt+P, you got 
```markdown
![](https://i.imgur.com/XH472FR.png)
```
```markdown
!p::
Send, {!}[]()
Sleep, 50
Send, {Left 1}
Sleep, 50
Send ^v
return
```

##### Code
In your clipboard, you have print('Hello').
Click win+` in dynalist next to test, you got this nice result.

![](https://i.imgur.com/sLA06FM.png)
```markdown
#`::
Send {Enter}
Send {Tab}
Send, code
Send +{Enter}
Send, ````````````
Sleep, 50
Send, {Left 3}
Send ^v
return

```

#### Autokey 
It's similar as above, just on Linux.
##### Picture
```markdown
# Enter script code
keyboard.send_keys("![]()")
keyboard.send_key("<left>")
```
##### Code
```python
# Enter script code
import time

keyboard.send_keys("<enter>")
keyboard.send_keys("code")
keyboard.send_key("<tab>")
keyboard.send_keys("<shift>+<enter>")
time.sleep(0.2)
keyboard.send_keys("```py```")
time.sleep(0.2)
keyboard.send_key("<left>", 3)
keyboard.send_keys("<enter>")
keyboard.send_keys("<ctrl>+v")
keyboard.send_keys("<enter>")
keyboard.send_keys("<shift>+<enter>")
```