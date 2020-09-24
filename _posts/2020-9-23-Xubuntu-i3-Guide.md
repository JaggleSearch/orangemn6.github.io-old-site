---
title: i3 on Xfce
subtitle: another wm
comments: true
---

Xubuntu with i3 Tiling Windows Walkthrough

The idea of this setup is to achieve the best of both worlds from convenient desktop features and essential i3 features. This walkthrough assumes that you are already familiar with using i3, but you do not have to be in order to complete it. An altered default i3 config file is part of the walkthrough, which adapts default i3 keystrokes to XFCE components. (New and replaced sections of the config file are designated in the file.)





Use the familiar i3 keystrokes and config file for window tiling.
Utilize normal application names instead of binaries'. (dmenu still available)
Desktop notifications/indicators (not typically easy to find for i3)
Fixes the administrator authentication problem when using i3 in Ubuntu.
Software Center
Updater
Users and Groups
Elegant color scheme and icons



As usual, i3 is brought to you by the letter i and by the number 3 . . . and by Dexter.

For this guide, you will need to enter terminal commands, but you should not expect to remember them. Conversely, you will always want to understand the i3 config file. The last step will be to create a link to the i3 configuration file on you XFCE panel - to provide a visual reminder that it is central to your user experience, and conveniently available to open and edit.

The i3 site provides the best source about editing the configuration file.


#### I. Install Xubuntu on your system
Install the Xubuntu desktop in another Ubuntu variant by entering the following in a terminal:
```
sudo apt-get update
sudo apt-get install xubuntu-desktop
```

 





(The general idea of this walkthrough should work for XFCE and Mint XFCE as well.)

 
#### II. Create a Spare User
Especially if you are already using Xubuntu, creating a spare user account ensures that you can easily return to Xubuntu's default desktop.
Open 'Users and Groups'
Click button: 'Add'

Type in your current admin password

Enter a Name title
Enter the official username
Click button: 'OK'

Enter the new user's password
Click button: 'OK'

Click 'Change...', next to 'Account type'

Change the account type to 'Administrator' 
Click button: 'OK'

Click button: 'Close'
Log out
Select the Xubuntu desktop 
Log in to the new user





#### III. Install a new background image manager
Xubuntu's desktop settings manager will not work with this setup, but luckily you can install "nitrogen" to change background images. Only remove xfdesktop4 if you (Unfortunately wallch does not work with i3.)
```
sudo apt-get install nitrogen
```





Nitrogen is simple and plays well with i3. It has the ability to set different wallpapers for different monitors or to expand one wallpaper between them.

Open Nitrogen.
Click "Preferences"
Click "Add"
Add any folders you use for background images
/usr/share/backgrounds
/usr/share/xfce4/backdrop







#### IV. Install the i3 Window Manager
Enter the following in a terminal to install the i3 window manager: 
```
sudo apt-get update
sudo apt-get install i3
```











#### V. Install i3ipc-GLib and i3 Workspaces Plugin
This is a prerequisite for being able to switch between i3 workspaces in XFCE.


Open a terminal and enter the following:
```
sudo add-apt-repository ppa:aacebedo/libi3ipc-glib
sudo apt-get update
sudo apt-get install libi3ipc-glib
```

(The details of this source are found here.)
Installing individual sources like this should be done rarely. There is a slight security risk, and it can slow down apt updates 



 


This wonderful plugin allows you to place an i3-compatible workspace switcher on your XFCE panel.

Open a terminal and enter the following:
```
sudo add-apt-repository ppa:aacebedo/xfce4-i3-workspaces-plugin
sudo apt-get update
sudo apt-get install xfce4-i3-workspaces-plugin
```

Installing individual sources like this should be done rarely. There is a slight security risk, and it can slow down apt updates








#### VI. Deactivate Xubuntu's window manager

Open 'Session and Startup', and go to the 'Session' tab.

Note xfwm4 and xfdesktop. These processes will be replaced by the i3 Window Manager.
For xfwm4, click 'Immediately' and change it to the  'Never' option.
For xfdesktop, click 'Immediately' and change it to the 'Never' option.

Click the button: 'Save Session'.
Go to the 'Application Autostart' tab to activate the i3 window manager in the next stage.

Note that you leave the xfce4-panel and Xfsettingsd as they are.







#### VII. Activate the i3 window manager
 In the 'Session and Startup' window, make sure you are in the 'Application Autostart' tab.

Click the button 'Add' to add i3 to the list of startup applications.
Fill out the form:
Name: i3 (or whatever you want to call i3)
Description: Tiling Window Manager (or whatever you want)
Command: i3 (must be "i3", as below)

Click the button: OK
You should scroll down to the bottom of the list and verify that i3 is listed and checked.
(Yes, the intimidating terminal command to start i3 is . . . i3.)
Click the button: Close








#### VIII. Remove non-i3 Keyboard Shortcuts
Disabling the shortcuts here is about letting i3 take over in this regard, utilizing the i3 config file. Although my general philosophy is to avoid getting technical wherever possible (ie: avoid using a config file when a GUI is available), managing keyboard shortcuts through the i3 config file is inevitable if you want to use i3 at all. For the sake of peace-of-mind, as well as avoiding strange conflicts, I say avoid using 2 different applications for managing keyboard shortcuts. In this guide, ALL keyboard shortcuts are defined by the i3 config, rather than some here and some there. bleh.

Open the 'Keyboard' dialogue.

Go to the 'Application Shortcuts' tab as above.
Remove all keyboard shortcuts
You can shift-select all of them and click the button: 'Remove' 
Click the button: Close









#### IX. Paste i3 config
Let's get down to brass tacks and just do this thing.
Create a directory in your user's home directory named '.i3'
The file path will be like: /home/<yourusername>/.i3/
Create a new file in the .i3 directory named 'config'
the file path will be like: /home/<yourusername>/.i3/config
Open the config file in a text editor and save the following in the file:


```
# This file has been auto-generated by i3-config-wizard(1).
# It will not be overwritten, so edit it as you like.
#
# Should you change your keyboard layout some time, delete
# this file and re-run i3-config-wizard(1).
#

# i3 config file (v4)
#
# Please see http://i3wm.org/docs/userguide.html for a complete reference!

set $mod Mod4

# Font for window titles. Will also be used by the bar unless a different font
# is used in the bar {} block below.
font pango:monospace 8

# This font is widely installed, provides lots of unicode glyphs, right-to-left
# text rendering and scalability on retina/hidpi displays (thanks to pango).
#font pango:DejaVu Sans Mono 8

# Before i3 v4.8, we used to recommend this one as the default:
# font -misc-fixed-medium-r-normal--13-120-75-75-C-70-iso10646-1
# The font above is very space-efficient, that is, it looks good, sharp and
# clear in small sizes. However, its unicode glyph coverage is limited, the old
# X core fonts rendering does not support right-to-left and this being a bitmap
# font, it doesn’t scale on retina/hidpi displays.

# Use Mouse+$mod to drag floating windows to their wanted position
floating_modifier $mod

# start a terminal
bindsym $mod+Return exec xfce4-terminal

# kill focused window
bindsym $mod+Shift+q kill

# start dmenu (a program launcher)
bindsym $mod+d exec dmenu_run

# For use with xfce4 whisker popup menu in Mint XFCE:
# bindsym $mod+Shift+d exec dmenu_run
# bindsym $mod+d exec --no-startup-id xfce4-popup-whiskermenu


# There also is the (new) i3-dmenu-desktop which only displays applications
# shipping a .desktop file. It is a wrapper around dmenu, so you need that
# installed.
# bindsym $mod+d exec --no-startup-id i3-dmenu-desktop

# change focus
bindsym $mod+j focus left
bindsym $mod+k focus down
bindsym $mod+l focus up
bindsym $mod+semicolon focus right

# alternatively, you can use the cursor keys:
bindsym $mod+Left focus left
bindsym $mod+Down focus down
bindsym $mod+Up focus up
bindsym $mod+Right focus right

# move focused window
bindsym $mod+Shift+j move left
bindsym $mod+Shift+k move down
bindsym $mod+Shift+l move up
bindsym $mod+Shift+semicolon move right

# alternatively, you can use the cursor keys:
bindsym $mod+Shift+Left move left
bindsym $mod+Shift+Down move down
bindsym $mod+Shift+Up move up
bindsym $mod+Shift+Right move right

# split in horizontal orientation
bindsym $mod+h split h

# split in vertical orientation
bindsym $mod+v split v

# enter fullscreen mode for the focused container
bindsym $mod+f fullscreen toggle

# change container layout (stacked, tabbed, toggle split)
bindsym $mod+s layout stacking
bindsym $mod+w layout tabbed
bindsym $mod+e layout toggle split

# toggle tiling / floating
bindsym $mod+Shift+space floating toggle

# change focus between tiling / floating windows
bindsym $mod+space focus mode_toggle

# focus the parent container
bindsym $mod+a focus parent

# focus the child container
#bindsym $mod+d focus child

# switch to workspace
bindsym $mod+1 workspace 1
bindsym $mod+2 workspace 2
bindsym $mod+3 workspace 3
bindsym $mod+4 workspace 4
bindsym $mod+5 workspace 5
bindsym $mod+6 workspace 6
bindsym $mod+7 workspace 7
bindsym $mod+8 workspace 8
bindsym $mod+9 workspace 9
bindsym $mod+0 workspace 10

# move focused container to workspace
bindsym $mod+Shift+1 move container to workspace 1
bindsym $mod+Shift+2 move container to workspace 2
bindsym $mod+Shift+3 move container to workspace 3
bindsym $mod+Shift+4 move container to workspace 4
bindsym $mod+Shift+5 move container to workspace 5
bindsym $mod+Shift+6 move container to workspace 6
bindsym $mod+Shift+7 move container to workspace 7
bindsym $mod+Shift+8 move container to workspace 8
bindsym $mod+Shift+9 move container to workspace 9
bindsym $mod+Shift+0 move container to workspace 10

# reload the configuration file
bindsym $mod+Shift+c reload
# restart i3 inplace (preserves your layout/session, can be used to upgrade i3)
bindsym $mod+Shift+r restart
# exit i3 (logs you out of your X session)
#-old-#bindsym $mod+Shift+e exec "i3-nagbar -t warning -m 'You pressed the exit shortcut. Do you really want to exit i3? This will end your X session.' -b 'Yes, exit i3' 'i3-msg exit'"
bindsym $mod+Shift+e exec xfce4-session-logout

# resize window (you can also use the mouse for that)
mode "resize" {
        # These bindings trigger as soon as you enter the resize mode

        # Pressing left will shrink the window’s width.
        # Pressing right will grow the window’s width.
        # Pressing up will shrink the window’s height.
        # Pressing down will grow the window’s height.
        bindsym j resize shrink width 10 px or 10 ppt
        bindsym k resize grow height 10 px or 10 ppt
        bindsym l resize shrink height 10 px or 10 ppt
        bindsym semicolon resize grow width 10 px or 10 ppt

        # same bindings, but for the arrow keys
        bindsym Left resize shrink width 10 px or 10 ppt
        bindsym Down resize grow height 10 px or 10 ppt
        bindsym Up resize shrink height 10 px or 10 ppt
        bindsym Right resize grow width 10 px or 10 ppt

        # back to normal: Enter or Escape
        bindsym Return mode "default"
        bindsym Escape mode "default"
}

bindsym $mod+r mode "resize"

# Start i3bar to display a workspace bar (plus the system information i3status
# finds out, if available)


#-old-#bar {
#-old-#       status_command i3status
#-old-#}
exec --no-startup-id nitrogen --restore
exec --no-startup-id synergy
```



The i3 site provides the best source for editing the configuration file.




Here is the magic moment when you can restart your computer and log in with i3 as your window manager.


#### i3 cheat sheet
The mod key is the 'super key', also called the 'windows key' (left of the space-bar.)

mod+Enter opens a terminal
mod+d opens Xubuntu's whisker menu (in place of the dmenu)
mod+Shift+d opens the dmenu
mod+Shift+q closes the current window tile
mod+r initiates resize-tile mode
mod+1, mod+2, etc. (1-0) switches to a different workspace
mod+Shift+1, mod+Shift+2, etc. (1-0) moves the current window tile to a different workspace
mod+Shift+` (` is left of '1') Moves a window tile to the scratch-pad workspace
mod+Shift+e initiates Xubuntu's session logout dialogue






#### X. Configure the XFCE Panel

Right-click the XFCE Panel at the top of the screen.
Select the menu option 'Panel >' and then 'Panel Preferences'
The panel preferences dialogue should open
This looks different in Xubuntu 16.04.

Click on the plus button to add the i3 workspaces plugin you installed earlier.
Use the arrows to place the i3 workspaces plugin where you want it on the panel.
Click the gear button, and configure the i3 workspaces plugin with colors that will show up on the panel.

I like to incorporate the i3 window color, which is #285577
Remove the 'Window Buttons' from the panel items by selecting it and clicking the minus button.
You can change the icon on the 'Whisker Menu' so that it is not an infantile mouse icon.
Add or remove any application launchers to the panel.







#### XI. Create a launcher for i3's config file
In the XFCE Panel items list, add a launcher next to the clock in order to create convenient access to the i3 config file.

Edit the launcher details to be as below
Click the icon to change it. (The icon above is included with xubuntu-desktop)
Name: i3 Config
Command: mousepad config
Working Directory: /home/<yourusername>/.i3
