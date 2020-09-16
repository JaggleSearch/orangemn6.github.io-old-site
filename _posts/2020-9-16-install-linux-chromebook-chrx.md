# How to install Linux on a chromebook with CHRX

**Note**: to do this, all your chromeOS data will be wiped. I recommend reading through all of this post before starting.

This post is about how I got my chromebook dual booting galliumOS.


### Step one: go into Developer mode.
Developer mode is a setting that lets you do development. It's not on by default because it also makes it easier to install a malicious package. (APKs, or android packages, can't be opened without developer mode.)

To turn on developer mode, hold down the esc and reload key, then tap the power key. You will be greeted by a very scary popup saying "CHROMEOS IS MISSING OR DAMAGED." Hit control-D, and then it will say something along the lines of "START DEVELOPER MODE? all your data will be wiped." press enter. It will start.

### Step two: login
Your computer will restart and say "OS VERIFICATION IS OFF." Press control-D.

since starting Developer mode wiped all your data, you will have to log in again, etc. If you don't want to that, you can just go into guest mode.

### Step two: install Chrx
You will have to install and run Chrx, which is really easy. Just one curl command:


```cd ; curl -Os https://chrx.org/go && sh go
```

Copy and paste that command in chrosh shell (ctrl-alt-T and then type shell.)

Go through the install script. At the bottom, it will have a "diagnosis." If it says it will only succeed if it has a firmware update keep that in mind. Reboot.

## Step two.two: Update firmware
If you need to update your firmware, you will have to download MrChromebox. Type this in the crosh shell:


```cd; curl -LO https://mrchromebox.tech/firmware-util.sh && sudo bash firmware-util.sh 
```
You will see a menu.


Press 1 to update the firmware. (When you do this, you will install BIOS [Basic Input/Output System]).

### Step three: repeat "step six"
Type this command in chrosh (again):


```cd ; curl -Os https://chrx.org/go && sh go 
```
That will install GaliumOS.

### Step four: Get into GalliumOS
Reboot. This time, when you have to type control-D, type control-L. It will go into BIOS, then GalliumOS. Username is chrx and password is chrx.


Chrx also accepts command line options.

Here they are:

```Usage: chrx [ option ... ]

Options
   -d DISTRIBUTION OS-specific distribution to install [galliumos]
                     galliumos, ubuntu, lubuntu, xubuntu, kubuntu, edubuntu,
                     fedora
   -e ENVIRONMENT  distribution-specific environment [desktop]
                     galliumos: desktop
                     ubuntu etc: desktop, minimal, standard, server
                     fedora: desktop, workstation, kde, xfce, lxde, mate,
                       cinnamon, sugar
   -r RELEASE      distribution release number or name [latest]
                     galliumos: latest, 3.0, bismuth, 2.0, xenon, nightly
                     ubuntu etc: latest, lts, dev, 16.04, 16.10, xenial, etc
                     fedora: latest, 23, 24, 25
   -a ARCH         processor architecture (i386, amd64) [amd64]
   -m MIRROR       distribution-specific download mirror [primary]
                     galliumos: ny1.us, va1.us, rb1.fr
   -t TARGETDISK   target disk (/dev/mmcblk1, /dev/sdb, etc) []
   -p PACKAGE      additional packages to install, may repeat []
                     kodi, minecraft, steam, etc, see chrx.org for more
                     (not yet supported on fedora)
   -H HOSTNAME     hostname for new system [chrx]
   -U USERNAME     username of first created user [chrx]
   -L LOCALE       locale for new system [en_US.UTF-8]
   -Z TIMEZONE     timezone for new system, Eggert convention [America/New_York]
                     America/San_Francisco, Europe/Amsterdam, Etc/UTC, etc
   -n              disable success/failure notifications
   -s              skip all customization, install stock OS only
   -y              run non-interactively, take defaults and do not confirm
   -v              increase output verbosity
   -h              show this help

Default values are shown in brackets, e.g.: [default].

If TARGETDISK is not specified, chrx will select the internal SSD.```
