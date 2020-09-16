---
layout: post
title: Minecraft server guide
subtitle: bedrock
tags: [linux]
comments: true
---

# Minecraft BE server
## linux guide

**Part 1
Getting the software**

Go to the [minecraft BE server Download](minecraft.net/download/server/bedrock) and download the linux files.  Unzip the file and cd into the folder.  then run the following: 
```
LD_LIBRARY_PATH=. ./bedrock_server 
```
now your server is running! You can stop now or follow the rest of the guide to turn your server into a system service.

**Part 2
System Service**
run the following command in your terminal:
```
nano server
```
in nano type the following:
```
cd /path/to/server/folder
LD_LIBRARY_PATH=. ./bedrock_server
```
Then press ctrl+o then ctrl+x to exit. Next, type these commands:
```
sudo mv server /usr/bin/server
```
Good! Now when you type server in your terminal, it will start the server. Now we make the service.

Here comes the tricky part:
```
cd /etc/systemd/system
sudo nano server.service
```
In nano copy and paste this:
```
[Unit]
Description=<mcbe server>

[Service]
User=<your user name>
WorkingDirectory=<directory_of_script e.g. /root>
ExecStart=</usr/bin/server>
Restart=always

[Install]
WantedBy=multi-user.target
```
Exit nano by pressing ctrl+o and ctrl+x.
Now enter this in a terminal:
```
sudo systemctl daemon-reload
sudo systemctl start server.service
sudo systemctl enable server.service
```
And you are done! if you liked this tutorial please comment! Thanks!
