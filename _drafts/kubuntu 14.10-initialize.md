---
layout: post
title:  "Kubuntu Initialization"
date:   2015-04-05
category: "Linux"
tags: [Linux, Kubuntu]
---

###Make a USB Installation Stick
First, downlaod the linux image file and burn image with **unetbootin**

>Missing Operation System Error
http://www.syslinux.org/wiki/index.php/Common_Problems#Missing_Operating_System_.28mbr.bin.29

###Common Tools

Install development tools.

    $ sudo apt-get install -y autoconf automake autotools-dev binutils build-essential fakeroot exuberant-ctags g++ gcc libc-dev-bin libc6-dev libltdl-dev libc++-dev libtool linux-libc-dev m4 manpages-dev patch xz-utils git-core meld giggle

Install personal usful tools.

    sudo apt-get install -y filezilla sakura vim openssh-server screen wget curl w3m htop

####bash environment

####vim

####git


###Install Individually
> google-chrome
> dropbox ()

####Multiple dropbox instances

> (http://www.dropboxwiki.com/tips-and-tricks/run-multiple-instances-of-dropbox-simultaneously-on-linux-or-mac-os-x)

Here is my script. Before we re-login
Add this script with "System Settings" -> "Startup and Shutdown"(Autostart)
Remove the origin dropbox initialation program.

```
#!/bin/bash
dropboxes=".dropbox-dist .dropbox-alt/.dropbox-dist"
for dropbox in $dropboxes
do
    HOME=/home/$USER
    if ! [ -d "$HOME/$dropbox" ]
    then
        mkdir "$HOME/$dropbox" 2> /dev/null
        ln -s "$HOME/.Xauthority" "$HOME/$dropbox/" 2> /dev/null
    fi
    HOME="$HOME/$dropbox"
    $HOME/dropboxd 2> /dev/null &
done
```
Logout and Login again, got two dropbox login windows.
