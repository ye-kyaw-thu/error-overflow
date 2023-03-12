## Installation of fbterm

```
(py3.8.10) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$ sudo apt-get install fbterm
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libopen-trace-format1 libotfaux0 linux-hwe-5.4-headers-5.4.0-122 linux-hwe-5.4-headers-5.4.0-124
  linux-hwe-5.4-headers-5.4.0-125 linux-hwe-5.4-headers-5.4.0-126 linux-hwe-5.4-headers-5.4.0-128
  linux-hwe-5.4-headers-5.4.0-131 linux-hwe-5.4-headers-5.4.0-132 linux-hwe-5.4-headers-5.4.0-135
  linux-hwe-5.4-headers-5.4.0-136 linux-hwe-5.4-headers-5.4.0-137
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  libx86-1
The following NEW packages will be installed:
  fbterm libx86-1
0 upgraded, 2 newly installed, 0 to remove and 146 not upgraded.
Need to get 131 kB of archives.
After this operation, 409 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 libx86-1 amd64 1.1+ds1-10.2 [75.2 kB]
Get:2 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 fbterm amd64 1.7-4 [55.9 kB]
Fetched 131 kB in 1s (87.6 kB/s)  
Selecting previously unselected package libx86-1:amd64.
(Reading database ... 665875 files and directories currently installed.)
Preparing to unpack .../libx86-1_1.1+ds1-10.2_amd64.deb ...
Unpacking libx86-1:amd64 (1.1+ds1-10.2) ...
Selecting previously unselected package fbterm.
Preparing to unpack .../fbterm_1.7-4_amd64.deb ...
Unpacking fbterm (1.7-4) ...
Setting up libx86-1:amd64 (1.1+ds1-10.2) ...
Setting up fbterm (1.7-4) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
Processing triggers for libc-bin (2.27-3ubuntu1.5) ...
/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_ribbon-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_html-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_adv-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_aui-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libpialign.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_richtext-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_xrc-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_qa-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_baseu_net-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_baseu_xml-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_core-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_stc-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_gl-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_propgrid-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/liboll.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_baseu-3.0.so.0 is not a symbolic link

(py3.8.10) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$
```

## Install Run getty

```
(py3.8.10) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$ sudo apt-get install rungetty
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libopen-trace-format1 libotfaux0 linux-hwe-5.4-headers-5.4.0-122 linux-hwe-5.4-headers-5.4.0-124
  linux-hwe-5.4-headers-5.4.0-125 linux-hwe-5.4-headers-5.4.0-126 linux-hwe-5.4-headers-5.4.0-128
  linux-hwe-5.4-headers-5.4.0-131 linux-hwe-5.4-headers-5.4.0-132 linux-hwe-5.4-headers-5.4.0-135
  linux-hwe-5.4-headers-5.4.0-136 linux-hwe-5.4-headers-5.4.0-137
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  rungetty
0 upgraded, 1 newly installed, 0 to remove and 146 not upgraded.
Need to get 12.7 kB of archives.
After this operation, 37.9 kB of additional disk space will be used.
Get:1 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 rungetty amd64 1.2-16build1 [12.7 kB]
Fetched 12.7 kB in 1s (8,938 B/s)   
Selecting previously unselected package rungetty.
(Reading database ... 665888 files and directories currently installed.)
Preparing to unpack .../rungetty_1.2-16build1_amd64.deb ...
Unpacking rungetty (1.2-16build1) ...
Setting up rungetty (1.2-16build1) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
(py3.8.10) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$
```

## Some Important Shortcut and Commands

sudo chvt 3 (Change to tty3)
Alt+F2 (return back to GUI)

Reference: https://superuser.com/questions/438950/how-do-i-make-ubuntu-start-fbterm-in-the-tty-on-startup  

```
/etc/inittab file  
```

rungetty allows you to run programs on a TTY as a particular user.  
fbterm requires you to be root to access the framebuffer, by the by. So you could run fbterm on TTY2 like so (double dashes signify the end of switches for rungetty):  

```
2:23:respawn:/sbin/rungetty -u root tty2 -- fbterm
```

Only one problem; you have a beautiful framebuffer-based terminal, but you're logged in as root! Having an unautheticated root prompt is about as bad for security as it gets. That won't do.  

We can use a program called login to get around this by accepting another set of user credentials, and then starting bash or zsh or whatever your login shell happens to be. Luckily, fbterm can accept a command as its final argument (again, double dashes prevent fbterm and rungetty from getting arguments mixed up:  

```
2:23:respawn:/sbin/rungetty -u root tty2 -- fbterm -- login  
```

you can also update tty terminal with following command:  

``````

/etc/init/tty1.conf
```

Note: /etc/inittab is not anymore used in debian distro.  
inittab ဖိုင်ကို မသုံးတော့ဘူး။   

## fbterm setup file

~/.fbtermrc file content:  

# Configuration for FbTerm

```
# Lines starting with '#' are ignored.
# Note that end-of-line comments are NOT supported, comments must be on a line of their own.


# font family names/pixelsize used by fbterm, multiple font family names must be seperated by ','
# and using a fixed width font as the first is strongly recommended
font-names=mono
font-size=12

# force font width (and/or height), usually for non-fixed width fonts
# legal value format: n (fw_new = n), +n (fw_new = fw_old + n), -n (fw_new = fw_old - n)
#font-width=
#font-height=

# default color of foreground/background text
# available colors: 0 = black, 1 = red, 2 = green, 3 = brown, 4 = blue, 5 = magenta, 6 = cyan, 7 = white
color-foreground=7
color-background=0

# max scroll-back history lines of every window, value must be [0 - 65535], 0 means disable it
history-lines=1000

# up to 5 additional text encodings, multiple encodings must be seperated by ','
# run 'iconv --list' to get available encodings.
text-encodings=

# cursor shape: 0 = underline, 1 = block
# cursor flash interval in milliseconds, 0 means disable flashing
cursor-shape=0
cursor-interval=500

# additional ascii chars considered as part of a word while auto-selecting text, except ' ', 0-9, a-z, A-Z
word-chars=._-

# change the clockwise orientation angle of screen display
# available values: 0 = 0 degree, 1 = 90 degrees, 2 = 180 degrees, 3 = 270 degrees
screen-rotate=0

# specify the favorite input method program to run
input-method=

# treat ambiguous width characters as wide
#ambiguous-wide=yes
```

```
TERM="xterm-256color"
```

## Some Example of FrameBuffer


fbi xxx.jpg  
fbi xxx.png  
fbi xxx.gif (no animation but you can see the image at least)  

fbgs xxx.pdf (you can also view pdf file within terminal, resolution is not very good but you know it is great!)  

mplayer -vo fbdev (for playing videos)  
(fbdev for Facebook Developer)  
you can use arrow keys ...  
q for exit  

-vf scale=640:480 (scaling the video frame)  


## Final Note

fbterm မှာ Myanmar3 font နဲ့ display လုပ်လို့ ရတယ်။ terminal font ကို ttf font နဲ့ ပြောင်းလို့ ရတယ်။   
သို့သော် မြန်မာစာဖိုင်တွေကိုဖွင့်ကြည့်တဲ့အခါမှာတော့ အဆင်မပြေဘူး။ monofont လုပ်ဖို့ လိုအပ်တယ်။  

## Reference

- https://tldp.org/HOWTO/pdf/Framebuffer-HOWTO.pdf
- https://superuser.com/questions/438950/how-do-i-make-ubuntu-start-fbterm-in-the-tty-on-startup
- https://askubuntu.com/questions/34308/where-is-the-inittab-file
- https://bbs.archlinux.org/viewtopic.php?id=150473
- https://askubuntu.com/questions/278863/how-do-i-set-up-a-background-image-for-console
- https://www.kernel.org/doc/html/next/fb/fbcon.html

