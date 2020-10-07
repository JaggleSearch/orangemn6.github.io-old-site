---
title: 9 Evil Bash Commands Explained
subtitle: do not run these
comments: true
---

# 9 Evil Bash Commands Explained

I remember using **and** understanding a terminal for the first time: That feeling when you realize that you are able to reach every file, run every program and fully control the whole system by simply typing something into a black window. And I also remember the fear that came with it to make a mistake and lose or destroy something irrecoverably.

I'm not exactly a sysadmin, but over the years I worked with a lot of Linux/UNIX based systems and found myself more than once in a situation where I hesitated hitting the Enter key to rethink what I'm just about to execute.

In the following I want to share some commands you should not use at all or at least very carefully. If you're new to bash commands, I hope you can learn something new. If you're a bash pro, you can take this post as exercise to predict the result before reading the explanation.

_Note: Some of these commands I learned myself the hard way, but most of them I picked up once in a while, i.e. in [this old thread][1]._

Before we start, the last warning:  
⚠ **_Do not run any of these commands on a system you care about!_** ⚠

##  [ ][2] 1\. Destructive directory changing 

I decided not to start with the classic `rm -rf /`* but with a variation of it:  

###  [ ][3] 💡 That's what happens 

* `alias` declares a aliases/shortcuts for bash commands. The syntax is like `alias alias_name="command_to_run"`
* `cd` is the alias name and the same like the __c_hange _d_irectory_ command
* `rm -rf` is the command to run. This doesn't translate to "read mail, -realfast" rather than "remove the given directory with all its content without asking".

So if an evil person adds this alias to your open bash when you're afk and you want to `cd` through your file system, you will quickly notice a strange behavior...

Luckily `alias` will only be temporarily available throughout the current shell session, unless it's added to one of the files that are loaded on start of a terminal session, i.e. `~/.bashrc`.

###  [ ][4] 🛡 How to prevent possible damage 

Well, simply don't add this alias and double-check the command, when adding a new alias. You can always check which aliases exist with the `alias` command and remove an alias with `unalias alias_name`.

To prevent deleting files unknowingly, you can add the following alias to your `~/.bashrc`:  

This will make your bash always ask you before deleting something, even if the `rm` command is added as another alias.

_* In case you didn't know: this command cannot be executed this simply anymore—an additional flag `\--no-preserve-root` is required to execute it on the root directory._

##  [ ][5] 2\. Memory-eater 

In case you doubt it, the following is a valid bash command:  

###  [ ][3] 💡 That's what happens 

In short: Recursion without termination condition. A function is defined which is called `:`. It calls itself twice in its own definition. At the end of the command, the function is initially called. It becomes more clear, when we write it in separate lines and rename the function:  

    
    
    evil () {
      evil|evil &
    }
    evil
    

If this gets executed, it replicates itself quickly consuming all your memory and CPU resources (also known as _fork bomb_). It can freeze your whole system and is therefore an example of a denial-of-service attack. It's surprising how such an attack can be executed with a command of just 12 Bytes!

###  [ ][4] 🛡 How to prevent possible damage 

If you're using iterative or recursive bash functions, always double-check for proper termination condition and use a safe environment for testing purposes.

Since a fork bomb launches an unlimited number of processes, the only way to protect your system is limiting the number of processes a local user can run. You can do so by editing the `/etc/security/limits.conf` accordingly. A user could work with about 200-300 processes at the same time, so limiting to something like 2000 processes should shield your system from a fork bomb without limiting the corresponding user too much.

##  [ ][6] 3\. Zero memory 
    
    
    dd if=/dev/zero of=/dev/sda
    

###  [ ][3] 💡 That's what happens 

* `dd` is a command to copy data from one file or device to another
* `if=` specifies the source and `/dev/zero` is an unlimited source of zero bytes
* `of=` specifies the target and `/dev/sda` is a disk drive or volume

You see where this is going. It's an excellent way to erase the contents of a whole disk and a pretty quick way to lose a lot of data.

###  [ ][4] 🛡 How to prevent possible damage 

Unfortunately there is no `-i` flag as it is the case for `rm`, so my only advice is to double-check, if the devices you specified in your `dd` command are really the correct ones. Don't use the `dd` command at all, if it's to risky for you.

You can disable the whole `dd` command with the following alias:  

    
    
    alias dd='echo "no dd command available"'
    

If the `dd` command is now executed on your system, it only prints out _no dd command available_.

##  [ ][7] 4\. Zero recovery 

The following variation of the above command is also possible:  

    
    
    for i in {1..10};do dd if=/dev/urandom of=/dev/sda;done
    

###  [ ][3] 💡 That's what happens 

This overrides the whole disk ten times with random bytes and minimizes the probability of recovering data even more.

###  [ ][4] 🛡 How to prevent possible damage 

Since this is also using the `dd` command, see the advices from the preceding section 4.

##  [ ][8] 5\. Uncommitted and lost 

###  [ ][3] 💡 That's what happens 

* `git reset` resets the current HEAD of a git repository to the last committed (or specified) state
* `\--hard` resets the index and working tree. Any changes to tracked files in the working tree since the last commit are discarded.

In other words: it discards all uncommitted changes. Since these aren't tracked by git, there's no way to restore them.

###  [ ][4] 🛡 How to prevent possible damage 

Simply don't use the `\--hard` flag. And if you have to: double-check if there are any local changes you want to keep before resetting it. I would recommend to do a hard reset only if the output of `git status` is empty or you're absolutely sure to wipe all uncommitted data.

##  [ ][9] 6\. Demolition by compression 
    
    
    tar -czvf /path/to/file archive.tgz
    # instead of
    tar -czvf archive.tgz /path/to/file
    

###  [ ][3] 💡 That's what happens 

* `tar -czvf` is the command to _c_reate a new archive, use g_z_ip, show a _v_erbose list of all files and use the given archive _f_ile
* `archive.tgz` the name of the archive file to create
* `/path/to/file` the path of the file to be compressed

The order of the files here is crucial. If the first file is the file you want to compress, it gets completely destroyed, because `tar` starts creating the archive by overwriting the first given file and realizes only afterwards, that the second given file doesn't exist. This is especially annoying if you wanted to make a backup of a file and used the wrong order of arguments...

###  [ ][4] 🛡 How to prevent possible damage 

Instead of grouping all flags together, you could separate the `-f` flag and use the longer version to remind yourself, which file the archive file is, e.g. like this:  

    
    
    tar -czv --file archive.tgz /path/to/file/to/compress
    

##  [ ][10] 7\. Too many rights 
    
    
    chmod -R 777 /
    # instead of
    chmod -R 777 ./
    

###  [ ][3] 💡 That's what happens 

* `chmod -R` applies file permissions recursively
* `777` permission mode to set (permit everything)
* `./` the directory or file which should be changed

If you don't pay attention which directory you want to target and accidentally take the root directory instead of the current directory, you will mess up all permissions of your whole system, making it impossible to use anymore.

###  [ ][4] 🛡 How to prevent possible damage 

To prevent the result of the typo above, you can add the following alias:  

    
    
    alias chmod='chmod --preserve-root'
    

This will always decline a recursive change on the root directory.

##  [ ][11] 8\. The root of all evil 

The same applies to owner changes:  

    
    
    chown -R root:root /
    # instead of
    chown -R root:root ./
    

###  [ ][3] 💡 That's what happens 

* `chown -R` applies new owner recursively
* `root:root` the owner:group to set
* `./` the directory or file which should be changed

This will mess up all files in a similar way that you would most likely need to reinstall your system.

###  [ ][4] 🛡 How to prevent possible damage 

As we already did with `chmod`, you can add the following alias for `chown` too:  

    
    
    alias chown='chown --preserve-root'
    

This will also in this case always decline a recursive change on the root directory.

##  [ ][12] 9\. Encrypted and destroyed 

###  [ ][3] 💡 That's what happens 

* `fsck` perform a _f_ile_s_ystem _c_hec_k_
* `-y` the flag to always attempt to fix any detected filesystem corruption automatically
* `/dev/sda` the volume to check

This is normally a good thing, except your volume is encrypted. In this case, the attempt of `fsck` fixing it would destroy it completely. A filesystem can only be checked after it is unlocked.

###  [ ][4] 🛡 How to prevent possible damage 

Only use the `fsck` command if you're absolutely sure, that you're using it on a normal, unencrypted volume. To prevent damage caused by an attempt of automatically fixing errors, don't use the `-y` flag at all.

* * *

##  [ ][13] Wrap it up 

We saw that it's incredibly easy to destroy data or make a whole system unusable by typing a simple command.

I found that in the end the best protection is **knowing what you type** and **double check** for typos before executing something! Never just copy and paste code—that's especially true for bash commands! And: always keep a good set of backups.

Most of the commands above need root privileges to be executed. So always be careful what you do as root!

If you know another evil command, please share it with us in the comments below.

_Disclaimer: I'm not responsible for any damage you do to your system by trying the above commands. Please use a safe environment like a virtual machine for testing. You have been warned._



[1]: https://www.cyberciti.biz/tips/my-10-unix-command-line-mistakes.html
[2]: https://dev.to#1-destructive-directory-changing
[3]: https://dev.to#thats-what-happens
[4]: https://dev.to#%F0%9F%9B%A1-how-to-prevent-possible-damage
[5]: https://dev.to#2-memoryeater
[6]: https://dev.to#3-zero-memory
[7]: https://dev.to#4-zero-recovery
[8]: https://dev.to#5-uncommitted-and-lost
[9]: https://dev.to#6-demolition-by-compression
[10]: https://dev.to#7-too-many-rights
[11]: https://dev.to#8-the-root-of-all-evil
[12]: https://dev.to#9-encrypted-and-destroyed
[13]: https://dev.to#wrap-it-up
