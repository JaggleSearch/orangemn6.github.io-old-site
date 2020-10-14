---
Title: Nativefier is Bonkers
subtitle: electron apps the easy way
comments: true
---


[Source](https://dev.to/daveparr/nativefire-is-bonkers-4m43 "Permalink to Nativefier is bonkers - DEV")

# Nativefier is bonkers - DEV

I made an electron app in 4 lines...  

    
    
    nativefier "http://musicforprogramming.net/" -n "musicforprogramming"
    cd musicforprogramming-linux-x64/
    sudo chmod +x musicforprogramming
    ./musicforprogramming
    

I like music, but don't like music in browser tabs. Basically because i have it open all the time, I want to find and control it easily, and I don't want it cluttering up an area that might be soley focused on work. 

I discovered some neat apps for google play, and wanted to see if there was one for my other go to, [musicforprogramming][1]. There wasn't, so I just casually googled how to convert a page into an electron app and OMFG!

###  Make any web page a desktop application 

![Build Status][2] ![npm version][3]

![Dock][4]

You want to make a native wrapper for WhatsApp Web (or any web page).
    
    
    nativefier web.whatsapp.com

![Walkthrough animation][5]

You're done.

##  Table of Contents

##  Introduction

Nativefier is a command-line tool to easily create a desktop application for any web site with succinct and minimal configuration. Apps are wrapped by [Electron][6] in an OS executable (`.app`, `.exe`, etc.) for use on Windows, macOS and Linux.

I did this because I was tired of having to `⌘-tab` or `alt-tab` to my browser and then search through the numerous open tabs when I was using [Facebook Messenger][7] or [Whatsapp Web][8] ([relevant Hacker News thread][9]).

[Changelog][10]. [Developer docs][11].

Features:

* Automatically retrieves the correct icon and app name.
* JavaScript and CSS injection.
* Many more, see the [API docs][12] or `nativefier --help`

##  Installation

* macOS 10.9+ / Windows / Linux
* [Node.js][13] `>= 10`
* Optional dependencies 

[This post][14] and [this one][15] helped iron out some kinks and now I can launch programming music right from my VS code terminal!

![vs code and an electron app of musicforprogramming made with nativefier][16]
    
    
    alias musicforprogramming="~/Dev/musicforprogramming-linux-x64/musicforprogramming
    

[1]: http://musicforprogramming.net/
[2]: https://camo.githubusercontent.com/ad85e0e99331276be88ac58d52766711e18f2334/68747470733a2f2f7472617669732d63692e6f72672f6a696168616f672f6e6174697665666965722e737667
[3]: https://camo.githubusercontent.com/738dc95632651a1cc6744eae10d51799e2e6a985/68747470733a2f2f62616467652e667572792e696f2f6a732f6e6174697665666965722e737667
[4]: https://res.cloudinary.com/practicaldev/image/fetch/s--az94tTn6--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://raw.githubusercontent.com/jiahaog/nativefier/master/docs/dock.png
[5]: https://res.cloudinary.com/practicaldev/image/fetch/s--JfLlSUl_--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://raw.githubusercontent.com/jiahaog/nativefier/master/docs/walkthrough.gif
[6]: https://www.electronjs.org/
[7]: https://messenger.com
[8]: https://web.whatsapp.com
[9]: https://news.ycombinator.com/item?id=10930718
[10]: https://github.com/jiahaog/nativefier/blob/master/CHANGELOG.md
[11]: https://github.com/jiahaog/nativefier/blob/master/docs/development.md
[12]: https://raw.githubusercontent.com/jiahaog/nativefier/master/docs/api.md
[13]: https://nodejs.org/
[14]: https://www.todesktop.com/guides/nativefier
[15]: https://www.addictivetips.com/ubuntu-linux-tips/nativefier-turn-websites-into-linux-apps/
[16]: https://res.cloudinary.com/practicaldev/image/fetch/s--JPtMrtuL--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/7dh4uokd2pt0zxgeye0n.png

  
