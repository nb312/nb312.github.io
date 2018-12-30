---
layout: post
title: Aliyun Config
subtitle: How to config the web server with the Aliyun.
tags: [linux]
---
# 一. 解析域名
### 1. 购买服务器
首先根据自己的需要购买服务器，我现在选择的是2G的，宽带是不定常，这主要个人需求了
### 2.购买域名
这个不用多说，大家都是会的，只要现在没有注册的域名，基本价格都是固定的，买你觉得喜欢或者和你的业务相关的就ok
### 3. 解析
当这两者都购买好以后，你就可以进行域名解析了，找到解析入口，一般在阿里云控制台中，域名产品下，找到你的域名就可以看见域名解析入口了，域名解析的本质就是将域名和ip进行绑定，注意，如果是域名和ESC服务器都是阿里云的，解析只需要这一步就可以了，不需要在主机上配置任何东西，配置如图
![Hell](https://github.com/nb312/nb312.github.io/blob/master/doc/aliyun1.png)
<img src="https://github.com/nb312/nb312.github.io/blob/master/doc/aliyun1.png" />
### 4. 验证解析
当配置好解析信息后，需要等大约10分钟才会生效，使用耐心一点，
在另一台主机上输入ping [你的域名]  
看是否成功,如果成功会类似下面的信息
```
C:\Users\nb>ping flutteropen.com

正在 Ping flutteropen.com [47.254.21.19] 具有 32 字节的数据:
来自 47.254.21.19 的回复: 字节=32 时间=182ms TTL=53
来自 47.254.21.19 的回复: 字节=32 时间=182ms TTL=53
来自 47.254.21.19 的回复: 字节=32 时间=181ms TTL=53
来自 47.254.21.19 的回复: 字节=32 时间=183ms TTL=53

47.254.21.19 的 Ping 统计信息:
    数据包: 已发送 = 4，已接收 = 4，丢失 = 0 (0% 丢失)，
往返行程的估计时间(以毫秒为单位):
    最短 = 181ms，最长 = 183ms，平均 = 182ms
```
### 注意事项
1. 我设置的境外服务器，所以可以不做备案也能解析，如果国内要使域名得到成功解析，还需要进行备案申请
2. 我现在使用的都是阿里云的产品，可能其他的供应商会有一定的不同

# 二. 80 端口 映射到8080

### 1. 安全组
阿里云并没有默认讲所有端口都开启，如果你想进行web开发，那么你就需要开启80/80端口，以及8080/8080 端口，具体如图，这一步是必不可少的，如果没有这个设置，你将无法通过浏览器进行ip的http 请求，当然443也一起开通，如你这样做了，你就可以对ip直接访问了，在浏览器中输入```http://ip```是什么反应
![Hell](https://github.com/nb312/nb312.github.io/blob/master/doc/aliyun2.png)
![Hell](https://github.com/nb312/nb312.github.io/blob/master/doc/aliyun3.png)

### 2. 80 端口 映射到8080 需求
系统的默认是80端口，也就是说我们在浏览器中输入域名（如http://flutteropen.com/）或者ip(```http://47.254.21.19```)时，我们实际调用的是(```http://47.254.21.19:80```),那怎么才能实现，当我们输入```http://flutteropen.com```时，直接调用监听在8080端口的应用程序呢，这就是我们的需求，这里我需要用到一个很好的工具，**nginx**

### 3. nginx 基本使用
> 我使用的是ubuntu 16,所以直接使用命令进行安装

[基本使用教程](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-16-04)，注意这里少了一些东西，把里面的命令看看把使用一下吧，额外的你需要这些命令
```
sudo ufw allow http
sudo ufw allow 80
sudo ufw allow https
sudo ufw allow 443
```
安装nginx并做一些初始化工作以后,我们现在可以通过``http://flutteropen.com``进行直接访问，但是出现的网页不是我们想要的，他是一个默认网页，一般是``/var/www/html/index.html``,这个文件是通过```/etc/nginx/sites-enabled/default```进行配置的，自己没事多看看
### 4.80 端口 映射到8080 配置
我们有了nginx工具后，我们就可以对我们的环境为所欲为了，就是我们刚才提到的文件```/etc/nginx/sites-enabled/default```
打开它，没有别人修改的情况下，你会看见很多注释以及有一个
```
#很多注释

server {
  #内部有很多代码配置
}
# Virtual Host configuration for example.com
#
# You can move that to a different file under sites-available/ and symlink that
# to sites-enabled/ to enable it.
#
#server {
#       listen 80;
#       listen [::]:80;
#
#       server_name example.com;
#
#       root /var/www/example.com;
#       index index.html;
#
#       location / {
#               try_files $uri $uri/ =404;
#       }


```

然后我们需要加入以下内容
```
server {
    listen       80;
    listen [::]:80;
    server_name  flutteropen.com;

    location / {
        proxy_set_header    Host $host:$server_port;
        proxy_set_header    X-Real-IP $remote_addr;
        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header    X-Forwarded-Proto $scheme;

        proxy_pass          http://127.0.0.1:8080;
        proxy_read_timeout  90;

        proxy_redirect      http://127.0.0.1:8080 http://flutteropen.com;
    }
}
```
注意，这里的端口8080是你应用监听端口，你可以修改的，还有
```flutteropen.com``` 是自己的域名，也是可以改的，其他的不懂就不要瞎改了,加入的时候，请注意是和另一个server{}是同级的，中间不用任何符号隔开，在前面一个server{}的下面粘贴进去就ok了，是不是很简单呢.
[配置指导](https://gist.github.com/zulhfreelancer/87bfb2ffeb937bd2fa38215cad9b9509)

### 5. 验证

现在是时候见证奇迹了，输入命令``` sudo service nginx restart ```,但前提是你的应用可能已经跑起来，并在8080做了监听，然后在浏览器中输入自己的域名(http://flutteropen.com)，你就能看见你想要的了，实在没有得到也不要气馁，重头再来一遍，看看究竟哪里没跟上，走错了方向。
