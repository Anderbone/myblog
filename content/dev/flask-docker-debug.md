+++ 
date = "2022-06-04"
title = "How to debug flask in docker with intellij on Linux"
tags = ["python", "flask", "docker"]
+++

Reference: https://blog.jetbrains.com/pycharm/2017/03/docker-compose-getting-flask-up-and-running/

Project to use in this page : https://github.com/wikimedia/analytics-quarry-web

I use intellij but PyCharm should be more or less the same.

Make sure your docker is configured correctly:
https://docs.docker.com/engine/install/linux-postinstall/

![](https://i.imgur.com/nFd9oSM.png)

Add remote interpreter
![](https://i.imgur.com/zYYqkAH.png)
![](https://i.imgur.com/p0jVyzJ.png)

First let's run by default to make sure it's working.
`docker-compose build && docker-compose up`

![](https://i.imgur.com/0SrwS5H.png)

Notice I changed the file name from quarry.wsgi to wsgi.py
![](https://i.imgur.com/MafdUxe.png)
Comment it out in dockerfile
![](https://i.imgur.com/N06shG9.png)

Run `docker-compose build` again.

Run debugger in intellij, hit debugger!

![](https://i.imgur.com/KA4ZU46.png)