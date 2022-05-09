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

result for th-en ...  

```
Done packing batches.
[asean.baseline.nodropout.en-th] Epoch 25.0000 dev BLEU4: 0.34479153588229566, 0.568389/0.394797/0.284897/0.221065 (BP = 1.000000, ratio=1.05, hyp_len=7143, ref_len=6809) (time=0-00:20:44)
[asean.baseline.nodropout.en-th]              dev auxiliary GLEU: 0.345076
[asean.baseline.nodropout.en-th]              dev auxiliary Loss: 4.650 (ref_len=6809)
             checkpoint took 0-00:00:26
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.en and ./data/dev.th
Performing inference on ./data/test.en and ./data/test.th
Experiment                    | Final Scores
-----------------------------------------------------------------------
asean.baseline.nodropout.en-th| BLEU4: 0.3463192177550231, 0.573536/0.396025/0.286235/0.221259 (BP = 1.000000, ratio=1.05, hyp_len=7119, ref_len=6809)
                              | GLEU: 0.347426
                              | WER: 61.42% ( C/S/I/D: 3940/1866/1313/1003; hyp_len=7119, ref_len=6809 )
                              | CER: 48.98% ( C/S/I/D: 18797/7454/3075/4563; hyp_len=29326, ref_len=30814 )
                              | BLEU4: 0.37248305134650994, 0.603629/0.421736/0.310859/0.243793 (BP = 0.999442, ratio=1.00, hyp_len=7165, ref_len=7169)
                              | GLEU: 0.366892
                              | WER: 57.05% ( C/S/I/D: 4156/1932/1077/1081; hyp_len=7165, ref_len=7169 )
                              | CER: 48.25% ( C/S/I/D: 19004/7424/2941/4613; hyp_len=29369, ref_len=31041 )
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-baseline-nodropout$
```

result for en-th ...  

```
Done packing batches.
[asean.baseline.nodropout.th-en] Epoch 18.0000 dev BLEU4: 0.26889110653376486, 0.457166/0.302675/0.223567/0.168985 (BP = 1.000000, ratio=1.02, hyp_len=7424, ref_len=7245) (time=0-00:16:57)
[asean.baseline.nodropout.th-en]              dev auxiliary GLEU: 0.276516
[asean.baseline.nodropout.th-en]              dev auxiliary Loss: 5.106 (ref_len=7245)
             checkpoint took 0-00:00:29
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.th and ./data/dev.en
Performing inference on ./data/test.th and ./data/test.en
Experiment                    | Final Scores
-----------------------------------------------------------------------
asean.baseline.nodropout.th-en| BLEU4: 0.27064950622269823, 0.456802/0.304744/0.225172/0.171180 (BP = 1.000000, ratio=1.01, hyp_len=7292, ref_len=7245)
                              | GLEU: 0.276648
                              | WER: 67.08% ( C/S/I/D: 3267/3143/882/835; hyp_len=7292, ref_len=7245 )
                              | CER: 56.41% ( C/S/I/D: 17602/8121/4352/4672; hyp_len=30075, ref_len=30395 )
                              | BLEU4: 0.3007472883141158, 0.484179/0.334456/0.251953/0.200513 (BP = 1.000000, ratio=1.01, hyp_len=7237, ref_len=7176)
                              | GLEU: 0.306213
                              | WER: 62.64% ( C/S/I/D: 3458/3002/777/716; hyp_len=7237, ref_len=7176 )
                              | CER: 52.42% ( C/S/I/D: 18341/7671/3872/4396; hyp_len=29884, ref_len=30408 )
```
