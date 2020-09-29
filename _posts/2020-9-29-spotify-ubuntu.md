---
layout: post
title: How to install spotify on ubuntu
subtitle: This is fun
tags: [linux]
comments: true
---



# HOW TO INSTALL SPOTIFY ON UBUNTU 20.04

Spotify is a well-versed platform for streaming music. You can easily access millions of distinctive songs on this very platform. Spotify makes it unchallenging to listen to your favorite music with ease. You can conveniently upgrade this software to relish whatever category of music suits your taste. The application encompasses a wide range of songs from classic to modern hip-hop. It offers the feature of listening offline music track after synchronization. It's not only a music application but also offers the contours of radio, audiobook, along with featuring videos and postcards. The Spotify app is highly compatible with Ubuntu and is very easy to download on Ubuntu 20.04. There are two primary methods for installing Spotify on your operating system. This guide directs the most appropriate and quick way to download Spotify using the root account. 

### Installation Process

To install Spotify on ubuntu 20.04 you just undergo 3 vital processes assuming the prerequisite that you are either logged in to the server using the root account. If not then use the user encompassing the sudo privileges. The three fundamental steps for installation are;

Step# 1: Initial package updating

Step# 2: Installation of Spotify on server

Step# 3: Start-up application

### Initial Package Updating

Always keep in mind to update the existing packages before installing any new application or software on your Linux server. Use these commands to update system packages.

$ sudo apt update && upgrade

![][1]

### Installation of Spotify on Server

Once you have updated all the packages then you can move towards installing the application. You can install Spotify app via the APT command on you Ubuntu 20.04 machine

### APT Command for Installation

In this procedure you are required to extract the GPG key of depository, using this command.

$ sudo apt-key adv \--keyserver hkp://keyserver.ubuntu.com:80  
 \--recv-keys 4773BD5E130D1D45

![][2]

You could use the below given command for the transfer of depository to server.

$ echo "deb http://repository.spotify.com stable non-free" |   
sudo tee /etc/apt/sources.list.d/spotify.list

![][3]

Now it's done. You have added the source in your Ubuntu system. As a final step, you just need to update your system and you are good to go.

![][4]

$ sudo apt install spotify-client

![][5]

### Start-Up Application

After using the above commands, you will see the output screen showing the successful installation of Spotify. You can ingress the Spotify in the search bar to find and start the application. After starting Spotify, you can access all of its features and enjoy listening to the songs on it.

![][6]

### CONCLUSION

This guide helps you in installing Spotify on ubuntu 20.04 proficiently. Updating the system package before and after the installation will result in effective e output in the form of the installation of the latest version of the application. 

[1]: https://linuxhint.com/wp-content/uploads/2020/09/word-image-1185.png
[2]: https://linuxhint.com/wp-content/uploads/2020/09/word-image-1186.png
[3]: https://linuxhint.com/wp-content/uploads/2020/09/word-image-1187.png
[4]: https://linuxhint.com/wp-content/uploads/2020/09/word-image-1188.png
[5]: https://linuxhint.com/wp-content/uploads/2020/09/word-image-1189.png
[6]: https://linuxhint.com/wp-content/uploads/2020/09/word-image-1190.png

  
