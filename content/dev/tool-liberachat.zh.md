+++ 
date = "2022-05-08"
title = "快速入门Liber chat"
tags = ["分享推荐"]
toc = true
+++

官网：[Libera Chat | A next-generation IRC network for FOSS projects collaboration!](https://libera.chat/)

IRC一大特点，坏处也是好处，大部分IRC服务器不会记录任何聊天记录。所以想和小伙伴聊天时，两个人必须同时在线。每次登陆后聊天记录都是空白的。

我们先需要一个客户端，第一次尝试直接用这个在线的即可：[Libera Chat](https://web.libera.chat/)

其他客户端参考：[Choosing an IRC client | Libera Chat](https://libera.chat/guides/clients)

第一次登录，Nick随便给自己起个英文名字，password和channel不用填，点击Start。
![](https://i.imgur.com/VRU3Bil.png)

你已经进入Libera世界了。

如果你知道小伙伴在哪个Channel，也不在意一定要保留一个自己的用户名，那根本无需注册，随便输入个用户名，Channel里输入频道名字(一般以#或者##开头)，就可以畅快使用了，后面都不用看了。
![](https://i.imgur.com/shzsEdO.png)

## 注册一个可以保留的用户名
无需密码登录的话，用户名也不会为你保留，重复名字会自动在后面加数字。先找个可以注册的名字，使用/nick + 你想要的用户名，看看能否注册。  
`/nick Yournick`
![](https://i.imgur.com/aLgOdXO.png)

/nick到自己满意的名字后，注册使用  
`/msg NickServ REGISTER YourPassword youremail@example.com`  
YourPassword是你的密码，后面是邮箱。

不出意外你会收到一封邮件，包含指令
`/msg  NickServ VERIFY REGISTER youname xxxxx`

复制这条指令，回到网页上运行，这时候你就有了自己的用户名和密码了。

## 进入频道
网页左边的CHANNELS右边，点击加号，可以输入你想去的频道。
查找包含linux关键字的频道使用 ：
`/msg alis LIST *linux*`  
查找500人以上的频道：
`/msg alis LIST * -min 500`

## 创建自己的频道
输入`/msg ChanServ INFO ##yourChannelName`，如果显示not registerd未注册，可以
`/join ##yourChannelName`加入了。

`/msg ChanServ REGISTER ##yourChannelName`会注册`##yourChannelName`这个名字的频道。

## Android客户端
推荐下载Revolution IRC。点击加号添加Server，信息如下，Server password留空，Username, Password以及Nicknames请填自己的用户名和密码，Auto-join channels可以添些自己常去的频道，勾选上Rejoin opened channels，这样每次打开会自动进入上次打开了的频道。
![](https://i.imgur.com/nNU3Z47.png)

当然如果你不想注册的话，只需要第一行的Name，Server address和Port，Authetication mode选None，随便输入个Nicknames，Auto-join channels里输入想去的频道，就可以开始玩耍了。


