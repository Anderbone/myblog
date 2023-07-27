+++ 
date = "2022-05-02"
title = "Kobo升级版本后如何更新Koreader"
tags = ["软件"]
+++
Koreader比Kobo本身的阅读器好用太多，翻页速度，各种快捷键，pdf裁边等等。我入了Kobo sage后没多久就装了Koreader。

安装参考链接：https://www.mobileread.com/forums/showthread.php?t=314220

最近想试试Kobo自带的Pocket，Koreader上的read it later插件wallabag还要自己找服务器配置实在麻烦，就退出了Koreader连上Wifi更新Pocket的list，没想到Kobo自动更新了。自动更新后，右下角NickelMenu点开没有了KOReader，显示Error。

这可怎么办，搜了一圈4.32 + Koreader没找到什么结果，还以为是不支持新版本，后来才发现是每次官方固件升级后的必备操作：

NOTE: Something that bears repeating from KFMon's FAQ: a FW update will disable it, so you'll have to reinstall it after a FW update in order to be able to launch stuff again, which is why there's a package dedicated to that listed at the bottom of this post.

要做的也很简单，下载KFMon这个zip后，直接解压缩到Kobo的根目录比如E盘下，点击替换文件夹，然后弹出即可。
![](https://i.imgur.com/7JfsR6Q.png)

Kobo会自动安装和重启，如果有弹窗，点击确定升级即可，熟悉的KOReader又回到右下角的NickelMenu里啦！