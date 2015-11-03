---
layout: post
title:  "GitHub多账户使用"
date:   2015-11-03
image: cover3.jpg
---

[source](http://www.blogjava.net/lishunli/archive/2012/03/08/371556.html)

在github托管了一些項目，其中包括三個`github pages`，需要通過不同的github賬號進行管理。

由於github使用ssh進行驗證連接，
我在本地創建了一個ssh key，等你切換到另一個賬號的話，添加ssh key，就會有「SSH 已經被使用」的出錯信息。
可能的解決方案是，使用多個SSH Key，然後通過配置位於`~/.ssh` 的 `config`文檔讓Github知道我所使用的多個key。

- 不需要使用ssh-add命令来添加ssh keys;


https://github.com/DasProjektZ/DasProjektZ.github.io.git