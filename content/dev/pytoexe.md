+++ 
date = "2020-08-16"
title = "Python to exe with win10 notification"
tags = ["python", "tool"]
+++

With this [auto-py-to-txe](https://pypi.org/project/auto-py-to-exe/), it's easily to convert your py to a self-contained exe.

I want to add a win10 notification, at first I tried win10toast.ToastNotifier(), it works fine in py but when I convert it to exe, it's no longer work anymore.

Then I tried plyer.notification, which works fine. 
Notince if you want to build a single exe file without folder, and you have resouce like pictures, you need to write a resouce_path function.

```python
def resource_path(relative_path):
    """ Get absolute path to resource, works for dev and for PyInstaller """
    try:
        # PyInstaller creates a temp folder and stores path in _MEIPASS
        base_path = sys._MEIPASS
    except Exception:
        base_path = os.path.abspath(".")
    return os.path.join(base_path, relative_path)

notification.notify("Test", "Successfully!",
app_icon=resource_path("xml.ico"))
```

