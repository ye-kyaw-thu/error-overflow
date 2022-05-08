# XNMT ASEAN Domain No Dropout Experiment No. 1

English-Thai, Thai-English no dropout experiment log file

## Prepare Config File and Data Folder for No-Dropout Experiment

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline-nodropout$ ls
config.baseline.en-th-word-nodropout.yaml  config.baseline.th-en-word-nodropout.yaml  data
```

just update experiment name and dropout.  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline-nodropout$ head ./config.baseline.en-th-word-nodropout.yaml
# standard settings
asean.baseline.nodropout.en-th: !Experiment
  exp_global: !ExpGlobal
  default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.0           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
```

for th-en direction ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline-nodropout$ head ./config.baseline.th-en-word-nodropout.yaml
# standard settings
asean.baseline.nodropout.th-en: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.0           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline-nodropout$
```

## Prepare a Shell Script for Training

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline-nodropout$ chmod +x ./train.sh
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline-nodropout$ cat ./train.sh
#!/bin/bash

time xnmt --backend torch --gpu ./config.baseline.en-th-word-nodropout.yaml | tee no-dropout.en-th.log1
time xnmt --backend torch --gpu ./config.baseline.th-en-word-nodropout.yaml | tee no-dropout.th-en.log1
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline-nodropout$
```

## Prepare screen command

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline-nodropout$ sudo apt-get install screen
[sudo] password for ye:
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libutempter0
Suggested packages:
  byobu | screenie | iselect
The following NEW packages will be installed:
  libutempter0 screen
0 upgraded, 2 newly installed, 0 to remove and 22 not upgraded.
Need to get 680 kB of archives.
After this operation, 1,081 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libutempter0 amd64 1.2.1-2build2 [8,848 B]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 screen amd64 4.9.0-1 [672 kB]
Fetched 680 kB in 1s (1,005 kB/s)
Selecting previously unselected package libutempter0:amd64.
(Reading database ... 230336 files and directories currently installed.)
Preparing to unpack .../libutempter0_1.2.1-2build2_amd64.deb ...
Unpacking libutempter0:amd64 (1.2.1-2build2) ...
Selecting previously unselected package screen.
Preparing to unpack .../screen_4.9.0-1_amd64.deb ...
Unpacking screen (4.9.0-1) ...
Setting up libutempter0:amd64 (1.2.1-2build2) ...
Setting up screen (4.9.0-1) ...
Processing triggers for install-info (6.8-4build1) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
Processing triggers for man-db (2.10.2-1) ...
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline-nodropout$
```

call --help  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline-nodropout$ screen --help
screen: /home/ye/anaconda3/envs/xnmt/lib/libtinfo.so.6: no version information available (required by screen)
Use: screen [-opts] [cmd [args]]
 or: screen -r [host.tty]

Options:
-4            Resolve hostnames only to IPv4 addresses.
-6            Resolve hostnames only to IPv6 addresses.
-a            Force all capabilities into each window's termcap.
-A -[r|R]     Adapt all windows to the new display width & height.
-c file       Read configuration file instead of '.screenrc'.
-d (-r)       Detach the elsewhere running screen (and reattach here).
-dmS name     Start as daemon: Screen session in detached mode.
-D (-r)       Detach and logout remote (and reattach here).
-D -RR        Do whatever is needed to get a screen session.
-e xy         Change command characters.
-f            Flow control on, -fn = off, -fa = auto.
-h lines      Set the size of the scrollback history buffer.
-i            Interrupt output sooner when flow control is on.
-l            Login mode on (update /var/run/utmp), -ln = off.
-ls [match]   or
-list         Do nothing, just list our SockDir [on possible matches].
-L            Turn on output logging.
-Logfile file Set logfile name.
-m            ignore $STY variable, do create a new screen session.
-O            Choose optimal output rather than exact vt100 emulation.
-p window     Preselect the named window if it exists.
-q            Quiet startup. Exits with non-zero return code if unsuccessful.
-Q            Commands will send the response to the stdout of the querying process.
-r [session]  Reattach to a detached screen process.
-R            Reattach if possible, otherwise start a new session.
-s shell      Shell to execute rather than $SHELL.
-S sockname   Name this session <pid>.sockname instead of <pid>.<tty>.<host>.
-t title      Set title. (window's name).
-T term       Use term as $TERM for windows, rather than "screen".
-U            Tell screen to use UTF-8 encoding.
-v            Print "Screen version 4.09.00 (GNU) 30-Jan-22".
-wipe [match] Do nothing, just clean up SockDir [on possible matches].
-x            Attach to a not detached screen. (Multi display mode).
-X            Execute <cmd> as a screen command in the specified session.
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline-nodropout$
```



## Training

```

```

```

```
