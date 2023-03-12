# tmux Installation Example

server နဲ့ ချိတ်ပြီး အလုပ်လုပ်တဲ့အခါမှာ tmux က အသုံးဝင်တယ်။  
built-in terminal တွေနဲ့ မတူတာက tmux က platform မျိုးစုံမှာ support လုပ်ပါတယ်။ အဲဒါကြောင့် mac OS မှာပဲ ဖြစ်ဖြစ် Linux မှာပဲ ဖြစ်ဖြစ် servers တွေပေါ်မှာ... ပြီးတော့  Raspberry Pi တွေပေါ်မှာပါ tmux က သုံးလို့ ရပါတယ်။  
tmux enviroment က configuration မျိုးစုံလုပ်ပြီး ကိုယ်ကြိုက်တဲ့ environment ကိုပြင်ပြီး သုံးလို့ ရတယ်။ dot file ကို သုံးပြီး ကိုယ်ပြင်ထားတဲ့ environment ကို sync လုပ်လို့ ရတာမို့ အရမ်းအဆင်ပြေပါတယ်။  

##  tmux Installation

```
(base) ye@ykt-pro:~/tool/fbv-1.0b$ sudo apt-get install tmux
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libopen-trace-format1 libotfaux0 linux-hwe-5.4-headers-5.4.0-122
  linux-hwe-5.4-headers-5.4.0-124 linux-hwe-5.4-headers-5.4.0-125
  linux-hwe-5.4-headers-5.4.0-126 linux-hwe-5.4-headers-5.4.0-128
  linux-hwe-5.4-headers-5.4.0-131 linux-hwe-5.4-headers-5.4.0-132
  linux-hwe-5.4-headers-5.4.0-135 linux-hwe-5.4-headers-5.4.0-136
  linux-hwe-5.4-headers-5.4.0-137
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  tmux
0 upgraded, 1 newly installed, 0 to remove and 146 not upgraded.
Need to get 249 kB of archives.
After this operation, 647 kB of additional disk space will be used.
Get:1 http://mm.archive.ubuntu.com/ubuntu bionic-updates/main amd64 tmux amd64 2.6-3ubuntu0.3 [249 kB]
Fetched 249 kB in 2s (148 kB/s)                          
Selecting previously unselected package tmux.
(Reading database ... 665896 files and directories currently installed.)
Preparing to unpack .../tmux_2.6-3ubuntu0.3_amd64.deb ...
Unpacking tmux (2.6-3ubuntu0.3) ...
Setting up tmux (2.6-3ubuntu0.3) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
(base) ye@ykt-pro:~/tool/fbv-1.0b$
```

## git clone gpakosz

configuration ကို reference အနေနဲ့ gpakosz ဆိုတဲ့ အကောင့်က တင်ထားတဲ့ config ဖိုင်ကို refer လုပ်နိုင်တယ် ...  

home folder အောက်မှာ လုပ်ဖို့ လိုအပ်တယ် ...  

```
(base) ye@ykt-pro:~$ git clone https://github.com/gpakosz/.tmux.git
Cloning into '.tmux'...
remote: Enumerating objects: 1053, done.
remote: Counting objects: 100% (41/41), done.
remote: Compressing objects: 100% (17/17), done.
remote: Total 1053 (delta 26), reused 35 (delta 24), pack-reused 1012
Receiving objects: 100% (1053/1053), 541.86 KiB | 4.33 MiB/s, done.
Resolving deltas: 100% (574/574), done.
(base) ye@ykt-pro:~$ ln -s -f .tmux/.tmux.conf
(base) ye@ykt-pro:~$ cp .tmux/.tmux.conf.local .
(base) ye@ykt-pro:~$ 
```

## Setting


setting တချို့ကို အောက်ပါအတိုင်း ဝင် update လုပ်ခဲ့ ...  

```
338 # on macOS, this requires installing reattach-to-user-namespace, see README.md
339 # on Linux, this requires xsel, xclip or wl-copy
340 tmux_conf_copy_to_os_clipboard=true
```

```
404 # to enable a plugin, use the 'set -g @plugin' syntax:
405 # visit https://github.com/tmux-plugins for available plugins
406 set -g @plugin 'tmux-plugins/tmux-copycat'
407 set -g @plugin 'tmux-plugins/tmux-cpu'
#408 set -g @plugin 'tmux-plugins/tmux-resurrect'
409 set -g @plugin 'tmux-plugins/tmux-continuum'
410 set -g @continuum-restore 'on'
```

ဖိုင်ရဲ့ နောက်ဆုံး နေရာမှာ အောက်ပါလိုင်းကို ဝင်ရိုက်ထည့်ခဲ့ ...  

```
# if run as "tmux attach", create a session if one does not already exist
new-session -n $HOST 
```

tumx ကို run လိုက်လိုက်ရင် အောက်ပါအတိုင်း မြင်ရလိမ့်မယ်။  


 ❐ 0  ↑ 3h 33m   1 bash                                                         ↑ ◼◼◼◼◼◼◼◼◼◻ 88% | 16:01 | 12 မတ်  ye  ykt-pro

## xclip Installation

command line နဲ့ X selections (the clipboard) အကြား copy/paste လုပ်လို့ ရဖို့အတွက် ကိုယ့်စက်ထဲမှာ xclip library ကို installation လုပ်ထားဖို့ လိုအပ်တယ်။  

```
(base) ye@ykt-pro:~$ sudo apt install xclip
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
The following NEW packages will be installed:
  xclip
0 upgraded, 1 newly installed, 0 to remove and 146 not upgraded.
Need to get 17.5 kB of archives.
After this operation, 52.2 kB of additional disk space will be used.
Get:1 http://mm.archive.ubuntu.com/ubuntu bionic/main amd64 xclip amd64 0.12+svn84-4build1 [17.5 kB]
Fetched 17.5 kB in 1s (18.9 kB/s)                        
Selecting previously unselected package xclip.
(Reading database ... 665905 files and directories currently installed.)
Preparing to unpack .../xclip_0.12+svn84-4build1_amd64.deb ...
Unpacking xclip (0.12+svn84-4build1) ...
Setting up xclip (0.12+svn84-4build1) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
(base) ye@ykt-pro:~$
```

## Shortcuts

Ctrl-b; % = screen ကို vertically နှစ်ခြမ်းခွဲဖို့  
Ctrl-b; " = screen ကို horizontally နှစ်ခြမ်းခွဲဖို့  
exit or Ctrl-d = လက်ရှိ ရောက်နေတဲ့ terminal ကနေ ထွက်ဖို့  

Ctrl-b;left-arrow key = vertically ခွဲထားတဲ့ screen နှစ်ခုကြား ရွှေ့ဖို့  
Ctrl-b; up-arrow or down-arrow = horizontally နှစ်ခြမ်းခွဲထားတဲ့ screen အကြား အပေါ်အောက် ရွှေ့ဖို့  

Ctrl-b; c = new window တစ်ခု ထပ်ဖွင့်တာ   
Ctrl-b; number = ဖွင့်ထားတဲ့ window တွေအကြား ကိုယ်သွားချင်တဲ့ window ရဲ့ နံပါတ်ကို ရိုက်ထည့်ပြီး ရွှေ့တာ  

## Session Handling

tmux ရဲ့ နောက်ထပ် အသုံးဝင်တဲ့ အပိုင်းက GNU ရဲ့ screen command လိုပဲ session တွေ ဖွင့်ပြီး terminal တွေကို သုံးလို့ ရတာပါ။ Detach, Re-attach လုပ်ပြီး ကိုယ်အရင် run ထားခဲ့တဲ့ session တွေဆီကို ပြန်သွားလို့ ရတဲ့ အပိုင်းပါ။ 

လက်ရှိ run နေတဲ့ session တွေကို ကြည့်ချင်ရင် ...  

```
(base) ye@ykt-pro:~$ tmux ls
0: 2 windows (created Sun Mar 12 17:19:39 2023) [126x34] (attached)
```

ဖွင့်ထားတဲ့ screen တွေကို attach ပြန်လုပ်မယ် ဆိုရင် ...  

```
tmux attach -t 0  
tmux attach -t 1  
```

နာမည် တစ်ခုပေးပြီး session အသစ် တစ်ခုကို စမယ် ဆိုရင်အောက်ပါအတိုင်း ...  

```
tmux new -s demo
```

session တွေကို rename လုပ်မယ် ဆိုရင် ...  

```
tmux rename-session -t demo demo1  
```

```
tmux rename-session -t 0 demo-session  

```

## List of All Tmux Commands

Ctrl-b; ? နဲ့ ရိုက်ပြီး ရှိသမျှ tmux command အားလုံးကို လေ့လာလို့ ရပါတယ်။  

```
bind-key    -T copy-mode    C-Space           send-keys -X begin-selection                                           [254/254]
bind-key    -T copy-mode    C-a               send-keys -X start-of-line
bind-key    -T copy-mode    C-b               send-keys -X cursor-left
bind-key    -T copy-mode    C-c               run-shell "tmux     send-keys -X cancel; /home/ye/.tmux/plugins/tmux-copycat/scr
ipts/copycat_mode_quit.sh; true"
bind-key    -T copy-mode    C-e               send-keys -X end-of-line
bind-key    -T copy-mode    C-f               send-keys -X cursor-right
bind-key    -T copy-mode    C-g               send-keys -X clear-selection
bind-key    -T copy-mode    C-k               send-keys -X copy-end-of-line
bind-key    -T copy-mode    C-n               send-keys -X cursor-down
bind-key    -T copy-mode    C-p               send-keys -X cursor-up
bind-key    -T copy-mode    C-r               command-prompt -i -I "#{pane_search_string}" -p "(search up)" "send -X search-ba
ckward-incremental \"%%%\""
bind-key    -T copy-mode    C-s               command-prompt -i -I "#{pane_search_string}" -p "(search down)" "send -X search-
forward-incremental \"%%%\""
bind-key    -T copy-mode    C-v               send-keys -X page-down
bind-key    -T copy-mode    C-w               run-shell "tmux     send-keys -X copy-pipe-and-cancel \"xclip -i -selection clip
board > /dev/null 2>&1\"; /home/ye/.tmux/plugins/tmux-copycat/scripts/copycat_mode_quit.sh; true"
bind-key    -T copy-mode    Escape            run-shell "tmux     send-keys -X cancel; /home/ye/.tmux/plugins/tmux-copycat/scr
ipts/copycat_mode_quit.sh; true"
bind-key    -T copy-mode    Space             send-keys -X page-down
bind-key    -T copy-mode    ,                 send-keys -X jump-reverse
bind-key    -T copy-mode    ;                 send-keys -X jump-again
bind-key    -T copy-mode    F                 command-prompt -1 -p "(jump backward)" "send -X jump-backward \"%%%\""
bind-key    -T copy-mode    N                 run-shell "tmux     send-keys -X search-reverse; /home/ye/.tmux/plugins/tmux-cop
ycat/scripts/copycat_jump.sh 'prev'; true"
bind-key    -T copy-mode    R                 send-keys -X rectangle-toggle
bind-key    -T copy-mode    T                 command-prompt -1 -p "(jump to backward)" "send -X jump-to-backward \"%%%\""
bind-key    -T copy-mode    f                 command-prompt -1 -p "(jump forward)" "send -X jump-forward \"%%%\""
bind-key    -T copy-mode    g                 command-prompt -p "(goto line)" "send -X goto-line \"%%%\""
bind-key    -T copy-mode    n                 run-shell "tmux     send-keys -X search-again; /home/ye/.tmux/plugins/tmux-copyc
at/scripts/copycat_jump.sh 'next'; true"
bind-key    -T copy-mode    q                 run-shell "tmux     send-keys -X cancel; /home/ye/.tmux/plugins/tmux-copycat/scr
ipts/copycat_mode_quit.sh; true"
bind-key    -T copy-mode    t                 command-prompt -1 -p "(jump to forward)" "send -X jump-to-forward \"%%%\""
bind-key    -T copy-mode    MouseDown1Pane    select-pane
bind-key    -T copy-mode    MouseDrag1Pane    select-pane ; send-keys -X begin-selection
bind-key    -T copy-mode    MouseDragEnd1Pane run-shell "tmux     send-keys -X copy-pipe-and-cancel \"xclip -i -selection clip
board > /dev/null 2>&1\"; /home/ye/.tmux/plugins/tmux-copycat/scripts/copycat_mode_quit.sh; true"
bind-key    -T copy-mode    WheelUpPane       select-pane ; send-keys -X -N 5 scroll-up
bind-key    -T copy-mode    WheelDownPane     select-pane ; send-keys -X -N 5 scroll-down
bind-key    -T copy-mode    DoubleClick1Pane  select-pane ; send-keys -X select-word
bind-key    -T copy-mode    TripleClick1Pane  select-pane ; send-keys -X select-line
bind-key    -T copy-mode    Home              send-keys -X start-of-line
bind-key    -T copy-mode    End               send-keys -X end-of-line
bind-key    -T copy-mode    NPage             send-keys -X page-down
bind-key    -T copy-mode    PPage             send-keys -X page-up
bind-key    -T copy-mode    Up                send-keys -X cursor-up
bind-key    -T copy-mode    Down              send-keys -X cursor-down
bind-key    -T copy-mode    Left              send-keys -X cursor-left
bind-key    -T copy-mode    Right             send-keys -X cursor-right
bind-key    -T copy-mode    M-1               command-prompt -N -I 1 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode    M-2               command-prompt -N -I 2 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode    M-3               command-prompt -N -I 3 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode    M-4               command-prompt -N -I 4 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode    M-5               command-prompt -N -I 5 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode    M-6               command-prompt -N -I 6 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode    M-7               command-prompt -N -I 7 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode    M-8               command-prompt -N -I 8 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode    M-9               command-prompt -N -I 9 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode    M-<               send-keys -X history-top
bind-key    -T copy-mode    M->               send-keys -X history-bottom
bind-key    -T copy-mode    M-R               send-keys -X top-line
bind-key    -T copy-mode    M-b               send-keys -X previous-word
bind-key    -T copy-mode    M-f               send-keys -X next-word-end
bind-key    -T copy-mode    M-m               send-keys -X back-to-indentation
bind-key    -T copy-mode    M-r               send-keys -X middle-line
bind-key    -T copy-mode    M-v               send-keys -X page-up
bind-key    -T copy-mode    M-w               run-shell "tmux     send-keys -X copy-pipe-and-cancel \"xclip -i -selection clip
board > /dev/null 2>&1\"; /home/ye/.tmux/plugins/tmux-copycat/scripts/copycat_mode_quit.sh; true"
bind-key    -T copy-mode    M-{               send-keys -X previous-paragraph
bind-key    -T copy-mode    M-}               send-keys -X next-paragraph
bind-key    -T copy-mode    M-Up              send-keys -X halfpage-up
bind-key    -T copy-mode    M-Down            send-keys -X halfpage-down
bind-key    -T copy-mode    C-Up              send-keys -X scroll-up
bind-key    -T copy-mode    C-Down            send-keys -X scroll-down
bind-key    -T copy-mode-vi C-b               send-keys -X page-up
bind-key    -T copy-mode-vi C-c               send-keys -X cancel
bind-key    -T copy-mode-vi C-d               send-keys -X halfpage-down
bind-key    -T copy-mode-vi C-e               send-keys -X scroll-down
bind-key    -T copy-mode-vi C-f               send-keys -X page-down
bind-key    -T copy-mode-vi C-h               send-keys -X cursor-left
bind-key    -T copy-mode-vi C-j               send-keys -X copy-pipe-and-cancel "xclip -i -selection clipboard > /dev/null 2>&
1"
bind-key    -T copy-mode-vi Enter             send-keys -X copy-pipe-and-cancel "xclip -i -selection clipboard > /dev/null 2>&
1"
bind-key    -T copy-mode-vi C-u               send-keys -X halfpage-up
bind-key    -T copy-mode-vi C-v               send-keys -X rectangle-toggle
bind-key    -T copy-mode-vi C-y               send-keys -X scroll-up
bind-key    -T copy-mode-vi Escape            send-keys -X cancel
bind-key    -T copy-mode-vi Space             send-keys -X begin-selection
bind-key    -T copy-mode-vi $                 send-keys -X end-of-line
bind-key    -T copy-mode-vi ,                 send-keys -X jump-reverse
bind-key    -T copy-mode-vi /                 command-prompt -p "(search down)" "send -X search-forward \"%%%\""
bind-key    -T copy-mode-vi 0                 send-keys -X start-of-line
bind-key    -T copy-mode-vi 1                 command-prompt -N -I 1 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode-vi 2                 command-prompt -N -I 2 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode-vi 3                 command-prompt -N -I 3 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode-vi 4                 command-prompt -N -I 4 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode-vi 5                 command-prompt -N -I 5 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode-vi 6                 command-prompt -N -I 6 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode-vi 7                 command-prompt -N -I 7 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode-vi 8                 command-prompt -N -I 8 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode-vi 9                 command-prompt -N -I 9 -p (repeat) "send -N \"%%%\""
bind-key    -T copy-mode-vi :                 command-prompt -p "(goto line)" "send -X goto-line \"%%%\""
bind-key    -T copy-mode-vi ;                 send-keys -X jump-again
bind-key    -T copy-mode-vi ?                 command-prompt -p "(search up)" "send -X search-backward \"%%%\""
bind-key    -T copy-mode-vi A                 send-keys -X append-selection-and-cancel
bind-key    -T copy-mode-vi B                 send-keys -X previous-space
bind-key    -T copy-mode-vi D                 send-keys -X copy-end-of-line
bind-key    -T copy-mode-vi E                 send-keys -X next-space-end
bind-key    -T copy-mode-vi F                 command-prompt -1 -p "(jump backward)" "send -X jump-backward \"%%%\""
bind-key    -T copy-mode-vi G                 send-keys -X history-bottom
bind-key    -T copy-mode-vi H                 send-keys -X start-of-line
bind-key    -T copy-mode-vi J                 send-keys -X scroll-down
bind-key    -T copy-mode-vi K                 send-keys -X scroll-up
bind-key    -T copy-mode-vi L                 send-keys -X end-of-line
bind-key    -T copy-mode-vi M                 send-keys -X middle-line
bind-key    -T copy-mode-vi N                 send-keys -X search-reverse
bind-key    -T copy-mode-vi T                 command-prompt -1 -p "(jump to backward)" "send -X jump-to-backward \"%%%\""
bind-key    -T copy-mode-vi V                 send-keys -X select-line
bind-key    -T copy-mode-vi W                 send-keys -X next-space
bind-key    -T copy-mode-vi ^                 send-keys -X back-to-indentation
bind-key    -T copy-mode-vi b                 send-keys -X previous-word
bind-key    -T copy-mode-vi e                 send-keys -X next-word-end
bind-key    -T copy-mode-vi f                 command-prompt -1 -p "(jump forward)" "send -X jump-forward \"%%%\""
bind-key    -T copy-mode-vi g                 send-keys -X history-top
bind-key    -T copy-mode-vi h                 send-keys -X cursor-left
bind-key    -T copy-mode-vi j                 send-keys -X cursor-down
bind-key    -T copy-mode-vi k                 send-keys -X cursor-up
bind-key    -T copy-mode-vi l                 send-keys -X cursor-right
bind-key    -T copy-mode-vi n                 send-keys -X search-again
bind-key    -T copy-mode-vi o                 send-keys -X other-end
bind-key    -T copy-mode-vi q                 send-keys -X cancel
bind-key    -T copy-mode-vi t                 command-prompt -1 -p "(jump to forward)" "send -X jump-to-forward \"%%%\""
bind-key    -T copy-mode-vi v                 send-keys -X begin-selection
bind-key    -T copy-mode-vi w                 send-keys -X next-word
bind-key    -T copy-mode-vi y                 send-keys -X copy-pipe-and-cancel "xclip -i -selection clipboard > /dev/null 2>&
1"
bind-key    -T copy-mode-vi {                 send-keys -X previous-paragraph
bind-key    -T copy-mode-vi }                 send-keys -X next-paragraph
bind-key    -T copy-mode-vi MouseDown1Pane    select-pane
bind-key    -T copy-mode-vi MouseDrag1Pane    select-pane ; send-keys -X begin-selection
bind-key    -T copy-mode-vi MouseDragEnd1Pane send-keys -X copy-pipe-and-cancel "xclip -i -selection clipboard > /dev/null 2>&
1"
bind-key    -T copy-mode-vi WheelUpPane       select-pane ; send-keys -X -N 5 scroll-up
bind-key    -T copy-mode-vi WheelDownPane     select-pane ; send-keys -X -N 5 scroll-down
bind-key    -T copy-mode-vi DoubleClick1Pane  select-pane ; send-keys -X select-word
bind-key    -T copy-mode-vi TripleClick1Pane  select-pane ; send-keys -X select-line
bind-key    -T copy-mode-vi BSpace            send-keys -X cursor-left
bind-key    -T copy-mode-vi NPage             send-keys -X page-down
bind-key    -T copy-mode-vi PPage             send-keys -X page-up
bind-key    -T copy-mode-vi Up                send-keys -X cursor-up
bind-key    -T copy-mode-vi Down              send-keys -X cursor-down
bind-key    -T copy-mode-vi Left              send-keys -X cursor-left
bind-key    -T copy-mode-vi Right             send-keys -X cursor-right
bind-key    -T copy-mode-vi C-Up              send-keys -X scroll-up
bind-key    -T copy-mode-vi C-Down            send-keys -X scroll-down
bind-key    -T prefix       C-a               send-prefix -2
bind-key    -T prefix       C-b               send-prefix
bind-key    -T prefix       C-c               new-session
bind-key    -T prefix       C-d               run-shell "/home/ye/.tmux/plugins/tmux-copycat/scripts/copycat_mode_start.sh '[[
:digit:]]+'"
bind-key    -T prefix       C-f               run-shell "/home/ye/.tmux/plugins/tmux-copycat/scripts/copycat_mode_start.sh '(^
|^\\.|[[:space:]]|[[:space:]]\\.|[[:space:]]\\.\\.|^\\.\\.)[[:alnum:]~_-]*/[][[:alnum:]_.#$%&+=/@-]*'"
bind-key    -T prefix       C-g               run-shell "/home/ye/.tmux/plugins/tmux-copycat/scripts/copycat_git_special.sh #{
pane_current_path}"
bind-key -r -T prefix       C-h               previous-window
bind-key    -T prefix       Tab               last-window
bind-key -r -T prefix       C-l               next-window
bind-key    -T prefix       Enter             copy-mode
bind-key    -T prefix       C-o               rotate-window
bind-key    -T prefix       C-u               run-shell "/home/ye/.tmux/plugins/tmux-copycat/scripts/copycat_mode_start.sh '(h
ttps?://|git@|git://|ssh://|ftp://|file:///)[[:alnum:]?=%/_.:,;~@!#$&()*+-]*'"
bind-key    -T prefix       C-z               suspend-client
bind-key    -T prefix       Space             next-layout
bind-key    -T prefix       !                 break-pane
bind-key    -T prefix       "                 split-window -c "#{pane_current_path}"
bind-key    -T prefix       #                 list-buffers
bind-key    -T prefix       $                 command-prompt -I "#S" "rename-session '%%'"
bind-key    -T prefix       %                 split-window -h -c "#{pane_current_path}"
bind-key    -T prefix       &                 confirm-before -p "kill-window #W? (y/n)" kill-window
bind-key    -T prefix       '                 command-prompt -p index "select-window -t ':%%'"
bind-key    -T prefix       (                 switch-client -p
bind-key    -T prefix       )                 switch-client -n
bind-key    -T prefix       +                 run-shell "cut -c3- '#{TMUX_CONF}' | sh -s _maximize_pane '#{session_name}' '#D'
"
bind-key    -T prefix       ,                 command-prompt -I "#W" "rename-window '%%'"
bind-key    -T prefix       -                 split-window -v -c "#{pane_current_path}"
bind-key    -T prefix       .                 command-prompt "move-window -t '%%'"
bind-key    -T prefix       /                 run-shell /home/ye/.tmux/plugins/tmux-copycat/scripts/copycat_search.sh
bind-key    -T prefix       0                 select-window -t :=0
bind-key    -T prefix       1                 select-window -t :=1
bind-key    -T prefix       2                 select-window -t :=2
bind-key    -T prefix       3                 select-window -t :=3
bind-key    -T prefix       4                 select-window -t :=4
bind-key    -T prefix       5                 select-window -t :=5
bind-key    -T prefix       6                 select-window -t :=6
bind-key    -T prefix       7                 select-window -t :=7
bind-key    -T prefix       8                 select-window -t :=8
bind-key    -T prefix       9                 select-window -t :=9
bind-key    -T prefix       :                 command-prompt
bind-key    -T prefix       ;                 last-pane
bind-key    -T prefix       <                 swap-pane -U
bind-key    -T prefix       =                 choose-buffer
bind-key    -T prefix       >                 swap-pane -D
bind-key    -T prefix       ?                 list-keys
bind-key    -T prefix       D                 choose-client
bind-key    -T prefix       F                 run-shell "cut -c3- '#{TMUX_CONF}' | sh -s _fpp '#{pane_id}' '#{pane_current_pat
h}'"
bind-key -r -T prefix       H                 resize-pane -L 2
bind-key    -T prefix       I                 run-shell /home/ye/.tmux/plugins/tpm/bindings/install_plugins
bind-key -r -T prefix       J                 resize-pane -D 2
bind-key -r -T prefix       K                 resize-pane -U 2
bind-key -r -T prefix       L                 resize-pane -R 2
bind-key    -T prefix       M                 select-pane -M
bind-key    -T prefix       P                 choose-buffer
bind-key    -T prefix       U                 run-shell "cut -c3- '#{TMUX_CONF}' | sh -s _urlview '#{pane_id}'"
bind-key    -T prefix       [                 copy-mode
bind-key    -T prefix       ]                 paste-buffer
bind-key    -T prefix       _                 split-window -h -c "#{pane_current_path}"
bind-key    -T prefix       b                 list-buffers
bind-key    -T prefix       c                 new-window
bind-key    -T prefix       d                 detach-client
bind-key    -T prefix       e                 new-window -n "#{TMUX_CONF_LOCAL}" sh -c "${EDITOR:-vim} \"$TMUX_CONF_LOCAL\" &&
 \"$TMUX_PROGRAM\" ${TMUX_SOCKET:+-S \"$TMUX_SOCKET\"} source \"$TMUX_CONF\" \\; display \"$TMUX_CONF_LOCAL sourced\""
bind-key    -T prefix       f                 command-prompt "find-window '%%'"
bind-key -r -T prefix       h                 select-pane -L
bind-key    -T prefix       i                 display-message
bind-key -r -T prefix       j                 select-pane -D
bind-key -r -T prefix       k                 select-pane -U
bind-key -r -T prefix       l                 select-pane -R
bind-key    -T prefix       m                 run-shell "cut -c3- '#{TMUX_CONF}' | sh -s _toggle_mouse"
bind-key    -T prefix       o                 select-pane -t :.+
bind-key    -T prefix       p                 paste-buffer -p
bind-key    -T prefix       q                 display-panes
bind-key    -T prefix       r                 run-shell "\"$TMUX_PROGRAM\" ${TMUX_SOCKET:+-S \"$TMUX_SOCKET\"} source \"$TMUX_
CONF\"" ; display-message "#{TMUX_CONF} sourced"
bind-key    -T prefix       s                 choose-tree -s
bind-key    -T prefix       t                 clock-mode
bind-key    -T prefix       u                 run-shell /home/ye/.tmux/plugins/tpm/bindings/update_plugins
bind-key    -T prefix       w                 choose-tree -w
bind-key    -T prefix       x                 confirm-before -p "kill-pane #P? (y/n)" kill-pane
bind-key    -T prefix       y                 run-shell -b "\"$TMUX_PROGRAM\" ${TMUX_SOCKET:+-S \"$TMUX_SOCKET\"} save-buffer
- | xclip -i -selection clipboard >/dev/null 2>&1"
bind-key    -T prefix       z                 resize-pane -Z
bind-key    -T prefix       {                 swap-pane -U
bind-key    -T prefix       }                 swap-pane -D
bind-key    -T prefix       ~                 show-messages
bind-key    -T prefix       PPage             copy-mode -u
bind-key    -T prefix       BTab              switch-client -l
bind-key -r -T prefix       Up                select-pane -U
bind-key -r -T prefix       Down              select-pane -D
bind-key -r -T prefix       Left              select-pane -L
bind-key -r -T prefix       Right             select-pane -R
bind-key    -T prefix       M-1               select-layout even-horizontal
bind-key    -T prefix       M-2               select-layout even-vertical
bind-key    -T prefix       M-3               select-layout main-horizontal
bind-key    -T prefix       M-4               select-layout main-vertical
bind-key    -T prefix       M-5               select-layout tiled
bind-key    -T prefix       M-h               run-shell "/home/ye/.tmux/plugins/tmux-copycat/scripts/copycat_mode_start.sh '\\
b([0-9a-f]{7,40}|[[:alnum:]]{52}|[0-9a-f]{64})\\b'"
bind-key    -T prefix       M-i               run-shell "/home/ye/.tmux/plugins/tmux-copycat/scripts/copycat_mode_start.sh '[[
:digit:]]{1,3}\\.[[:digit:]]{1,3}\\.[[:digit:]]{1,3}\\.[[:digit:]]{1,3}'"
bind-key    -T prefix       M-n               next-window -a
bind-key    -T prefix       M-o               rotate-window -D
bind-key    -T prefix       M-p               previous-window -a
bind-key    -T prefix       M-u               run-shell /home/ye/.tmux/plugins/tpm/bindings/clean_plugins
bind-key -r -T prefix       M-Up              resize-pane -U 5
bind-key -r -T prefix       M-Down            resize-pane -D 5
bind-key -r -T prefix       M-Left            resize-pane -L 5
bind-key -r -T prefix       M-Right           resize-pane -R 5
bind-key -r -T prefix       C-Up              resize-pane -U
bind-key -r -T prefix       C-Down            resize-pane -D
bind-key -r -T prefix       C-Left            resize-pane -L
bind-key -r -T prefix       C-Right           resize-pane -R
bind-key    -T root         C-l               send-keys C-l ; run-shell "sleep 0.2" ; clear-history
bind-key    -T root         MouseDown1Pane    select-pane -t = ; send-keys -M
bind-key    -T root         MouseDown1Status  select-window -t =
bind-key    -T root         MouseDown3Pane    if-shell -F -t = "#{mouse_any_flag}" "select-pane -t=; send-keys -M" "select-pan
e -mt="
bind-key    -T root         MouseDrag1Pane    if-shell -F -t = "#{mouse_any_flag}" "if -Ft= \"#{pane_in_mode}\" \"copy-mode -M
\" \"send-keys -M\"" "copy-mode -M"
bind-key    -T root         MouseDrag1Border  resize-pane -M
bind-key    -T root         WheelUpPane       if-shell -F -t = "#{mouse_any_flag}" "send-keys -M" "if -Ft= \"#{pane_in_mode}\"
 \"send-keys -M\" \"copy-mode -et=\""
bind-key    -T root         WheelUpStatus     previous-window
bind-key    -T root         WheelDownStatus   next-window
```

## Reference

- tmux shortcuts & cheatsheet: [https://gist.github.com/MohamedAlaa/2961058](https://gist.github.com/MohamedAlaa/2961058)  
- [https://github.com/rothgar/awesome-tmux](https://github.com/rothgar/awesome-tmux)  
- [https://www.hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/](https://www.hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/)
- [https://www.hamvocke.com/blog/a-guide-to-customizing-your-tmux-conf/](https://www.hamvocke.com/blog/a-guide-to-customizing-your-tmux-conf/)  
- [useful configurations for tmux](https://github.com/gpakosz/.tmux.git)
- [https://www.reddit.com/r/unixporn/](https://www.reddit.com/r/unixporn/)

