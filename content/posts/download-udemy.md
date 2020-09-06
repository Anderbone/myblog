+++ 
date = "2020-07-01"
title = "How to download all videos (resources) on Udemy at once"
tags = ["tools"]
+++

> This article will teach you how to download all videos or whatever resources on udemy you want, for e.g. all zip files in a specific course.

The tool we use: https://github.com/r0oth3x49/udemy-dl

Suppose we want to download all zip files in a course:
1. run the following command:
```python
python udemy-dl.py https://www.udemy.com/course/xxx/  --save
```
![](https://i.imgur.com/F6uG3ER.png)

2. We get a txt file with all downloadable links, open it with [ VSCode ](https://code.visualstudio.com/)

![](https://i.imgur.com/xcExhIY.png)

3. Suppose we only want all zip files, we just need to search __https.*zip__ with regex opened (the third button):

![](https://i.imgur.com/WnGuTpY.png)

Then Alt+Enter to select all lines, then Ctrl+C, open a new file, Ctrl+V. Bingo! We get all links we want:

![](https://i.imgur.com/fa5I4Ce.png)

4. With some download managers such as [Free Download Manager](https://www.freedownloadmanager.org/), you can download all files you want at once finally!

![](https://i.imgur.com/iVoszbx.png)