---
layout: page
title: Mine Note.
subtitle: This is my note,which is the bug I fix or the problem I confer.
---

#  Cause: dl.google.com:443 failed to respond
这个问题是由于代理问题引起的

[注销gradle中的https代理](https://blog.csdn.net/linweidong/article/details/80879798)

linux 路经 ～\.gradle\gradle.properties 文件下
window C:\Users\Administrator\.gradle\gradle.properties文件下
路径主要是gradle 运行是的路径 然后修改为下面类似的内容 如果没有代理 可以直接把  http 代理也注释掉
```
#systemProp.https.proxyPort=1080
systemProp.http.proxyHost=127.0.0.1  
#systemProp.https.proxyHost=127.0.0.1  
systemProp.http.proxyPort=1080
```
