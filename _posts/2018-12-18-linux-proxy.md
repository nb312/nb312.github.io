---
layout: post
title: Linux| Layout
subtitle: Recordings about the base layout.
tags: [linux]
---

This tutorial is going to show you how to set up Shadowsocks proxy on Ubuntu 16.04 and Ubuntu 17.10. Shadowsocks is a lightweight, fast and secure Socks5 proxy to bypass Internet censorship. We will learn how to set up the server side and how to configure the desktop client on Ubuntu. There are many implementations of Shadowsocks, this tutorial shows you how to use Shadowsocks-libev, because


It’s written in C, very fast even on low end machine.
It’s well-maintained.
It’s the most feature-rich implementation. TCP fast open, multiuser, management API, redirect mode, tunnel mode, UDP relay, AEAD ciphers and plugins are all supported.
Prerequisites
To complete this tutorial, you will need:

A VPS (Virtual Private Server). I recommend Vultr. They offer 512M memory high performance VPS for just $2.5 per month, which is perfect for your private proxy server.
Then install Ubuntu 16.04 or 17.10 on your VPS.
Install Shadowsocks-libev Server on Ubuntu 16.04/17.10
SSH into your remote Ubuntu server. Shadowsocks-libev is included in Ubuntu repository since 17.04. So Ubuntu 17.10 users can install it with:

sudo apt update

sudo apt install shadowsocks-libev
Ubuntu 16.04 users can install it from PPA by running the following commands. software-properties-common is needed if you want to install software from PPA. It may be missing on your Ubuntu server.

sudo apt install software-properties-common -y

sudo add-apt-repository ppa:max-c-lv/shadowsocks-libev -y

sudo apt update

sudo apt install shadowsocks-libev
The sodium crypto library (libsodium) will be installed along with shadowsocks-libev. It’s a requirement if you want to use the secure and fast ChaCha20-Poly1305 encryption method. Once it’s installed, edit the configuration file.

 sudo nano /etc/shadowsocks-libev/config.json
Default contents of the file are as follows.

{
 "server":"127.0.0.1",
 "server_port":8388,
 "local_port":1080,
 "password":"focobguph",
 "timeout":60,
 "method":"chacha20-ietf-poly1305"
}
Replace 127.0.0.1 with your Ubuntu server public IP address. You can change server_port to other port number, but don’t use port 8388. Then set your preferred password, which is used to encrypt traffic. You can leave the encryption method to default.

Save and close the file. Then start shadowsocks-libev service.

sudo systemctl start shadowsocks-libev.service
Enable auto-start at boot time.

sudo systemctl enable shadowsocks-libev.service
Check its status. Make sure it’s running.

systemctl status shadowsocks-libev.service
Note: On Ubuntu 17.10, Shadowsocks-libev will automatically start with the default configuration file. You need to restart it for your configurations to take effect.

sudo systemctl restart shadowsocks-libev
Sometimes you can see the following error.


This system doesn't provide enough entropy to quickly generate high-quality random numbers. The service will not start until enough entropy has been collected.
You can fix this error by installing rng-tools.

sudo apt-get install rng-tools
Then run

sudo rngd -r /dev/urandom
Now you can start Shadowsocks-libev service.

Configure Firewall
If you are using iptables firewall on your server, then you need to allow traffic to the TCP and UDP port Shadowsocks is listening on. For example, if port 8888 is being used by Shadowsocks, then run the following command:

sudo iptables -I INPUT -p tcp --dport 8888 -j ACCEPT

sudo iptables -I INPUT -p udp --dport 8888 -j ACCEPT
If you are using UFW firewall, then run the following commands:

sudo ufw allow 8888
If you are using AWS or Google Cloud, then you need to configure firewall at the web-based control panel.


Install and Configure Shadowsocks-libev on Ubuntu 16.04/17.10 Desktop
The shadowsocks-libev package contains both the server software and client software. So on Ubuntu 16.04/17.10 desktop, you can install shadowsocks-libev from repository or PPA to get the client software.

On Ubuntu 17.10 desktop, run the following commands to install Shadowsocks-libev.

sudo apt update

sudo apt install shadowsocks-libev
Note: On Ubuntu 17.10, Shadowsocks-libev (the server) will automatically start after being installed. You need to stop Shadowsocks server on Ubuntu desktop.

sudo systemctl stop shadowsocks-libev
Also disable auto-start at boot time.

sudo systemctl disable shadowsocks-libev
On Ubuntu 16.04 desktop, run the following commands to install Shadowsocks-libev.

sudo add-apt-repository ppa:max-c-lv/shadowsocks-libev -y

sudo apt update

sudo apt install shadowsocks-libev
The Shadowsocks client binary is named ss-local. There’s a template systemd service unit for it: /lib/systemd/system/shadowsocks-libev-local@.service. Before starting the client, we need to create the client side configuration file.

sudo nano /etc/shadowsocks-libev/location-of-your-server.json
You can replace location-of-your-server with something like SFO, LAX. Copy the Shadowsocks-libev server config to the client config file, then add the following line to tell the client to listen on 127.0.0.1.


 "local_address":"127.0.0.1",
So the client config file will look like this:

{
 "server":"your-server-ip-address",
 "server_port":8388,
 "local_address":"127.0.0.1",
 "local_port":1080,
 "password":"focobguph",
 "timeout":60,
 "method":"chacha20-ietf-poly1305"
}
Save and close the file. Then we can start the client with:

sudo systemctl start shadowsocks-libev-local@location-of-your-server.service
And enable auto-start at boot time.

sudo systemctl enable shadowsocks-libev-local@location-of-your-server.service
Check its status. Make sure it’s running.

systemctl status shadowsocks-libev-local@location-of-your-server.service
Now the ss-local process listens on 127.0.0.1:1080 on your Ubuntu desktop and it’s connected to your Shadowsocks server.

Configure Web Browser to Use the Socks Proxy
To let your program use a socks proxy, the program must support socks proxy. Programs like Firefox, Google Chrome and Dropbox allows users to use proxy. I will show you how to configure Firefox and Google Chrome.

Firefox
In Firefox, go to Edit > Preferences > General. Then scroll down to the bottom and click Settings in Network Proxy. In the Connection Settings window, select manual proxy configuration. Then select SOCKS v5 because Shadowsocks is a Socks5 proxy. Enter 127.0.0.1 in the SOCKS Host field and 1080 in the port field. Make sure Proxy DNS when using SOCKS v5 is enabled. Click OK to apply these modifications.

shadowsocks-libev ubuntu 16.04

Google Chrome
Google Chrome and Chromium Linux version don’t have a GUI to configure proxy, but you can use command line options like below.

google-chrome --proxy-server="socks5://127.0.0.1:1080"
or

chromium-browser --proxy-server="socks5://127.0.0.1:1080"
You can also install and use the SwitchOmega extension configure proxy.

DNS Leak Test
Go to dnsleaktest.com. You will see your Shadowsocks server’s IP address, which indicates that your proxy is working.

shadowsocks-libev ubuntu install

Click Standardard test. Make sure your local ISP isn’t in the test results.

shadowsocks-libev ubuntu 17.10

Proxy in Command Line
To let your command line programs use the proxy, you can install tsocks.

sudo apt install tsocks
Then edit the configuration file.


sudo nano /etc/tsocks.conf
Find the following line:

server = 192.168.0.1
Change it to

server = 127.0.0.1
Save and close the file. Now you can allow you command line program to use Shadowsocks proxy like this:

sudo tsocks apt update
There’s also a similar program called proxychains.

Enable TCP Fast Open
You can speed up Shadowsocks by enabling TCP fast open. TCP is connection-oriented protocol, which means data can only be exchanged after a connection is established, which is done via the three way handshake. In other words, traditionally, data can only be exchanged after the three way handshake is complete. TCP fast open (TFO) is a mechanism that allows data to be exchanged before three way handshake is complete, saving up to 1 round-trip time (RTT).

TCP fast open support is merged to Linux kernel since version 3.7 and enabled by default since version 3.13. You can check your kernel version by running:

uname -r
To check TCP fast open configuration on your Ubuntu server, run

cat /proc/sys/net/ipv4/tcp_fastopen
It can return 4 values.

0 means disabled.
1 means it’s enabled for outgoing connection (as a client).
2 means it’s enabled for incoming connection (as a server).
3 means it’s enabled for both outgoing and incoming connection.
All my Ubuntu 16.04/17.10 VPS (Virtual Private Server) returned 1 after running the above command. We want tcp_fastopen set to 3 on our server. To achieve that, we can edit the sysctl configuration file.

sudo nano /etc/sysctl.conf
Then paste the following line at the end of the file.

net.ipv4.tcp_fastopen=3
Reload sysctl settings for the change to take effect.

sudo sysctl -p
Then you will also need to enable TCP fast open in Shadowsocks configuration file.

sudo nano /etc/shadowsocks-libev/config.json
Add the following line.

"fast_open": true
So your Shadowsocks server configuration file will look like this:

{
 "server":"your-server-ip-address",
 "server_port":8388,
 "local_port":1080,
 "password":"focobguph",
 "timeout":60,
 "method":"chacha20-ietf-poly1305",
 "fast_open": true
}
Note that last config line has not comma. Save and close the file. Then restart Shadowsocks server.

sudo systemctl restart shadowsocks-libev
Check if it’s running. (An error in configuration file can prevent it from restarting.)

systemctl status shadowsocks-libev
You also need to edit the Shadowsocks client configuration file and restart it to enable TCP fast open on Ubuntu desktop.

Enable TCP BBR
TCP BBR is a TCP congestion control algorithm that can drastically improve connection speed. Check out the following tutorial.

How to Easily Boost Ubuntu Network Performance by Enabling TCP BBR
For more usage on Shadowsocks, check the manual.

man shadowsocks-libev
Troubleshooting
Every now and then, my Shadowsocks-libev proxy stops working and the following error is displayed on the server side when I check the status with systemctl.

ERROR: server recv: Connection reset by peer
On the client side, the error returned by systemctl is:

ERROR: remote_recv_cb_recv: Connection reset by peer
I don’t know why it happens, but restarting the shadowsocks-libev service on the server can fix this issue.

sudo systemctl restart shadowsocks-libev
I don’t want to manually restart the service every time, so I add a cron job to do it for me periodically.

sudo crontab -e
Put the following line at the end of the file.

0 */3 * * * /bin/systemctl restart shadowsocks-libev
This will restart the service every 3 hours. That is to say, restart happens at 12am, 3am, 6am, 9am and so forth. Note that the time is determined by cron. It is not determined by calculating how long the service has been running.

That’s it! I hope this tutorial helped you install Shadowsocks-libev proxy on Ubuntu 16.04 and Ubuntu 17.10. As always, if you found this post useful, then subscribe to our free newsletter or follow us on Google+, Twitter or like our Facebook page. Thanks for visiting!
