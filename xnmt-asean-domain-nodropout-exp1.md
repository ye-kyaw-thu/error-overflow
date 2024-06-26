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

## Preparing for SwitchOut No-Dropout

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-switchout$ cp config.switchout.th-en-word.yaml ./config.switchout.nodropout.th-en-word.yaml
```

updated the experiment name and dropout value for en-th ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-switchout$ head ./config.switchout.nodropout.en-th-word.yaml
# standard settings
switchout.nodropout.asean.en-th: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.0           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
```

updated the experiment name and dropout value for th-en ...  

```
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-switchout$ head ./config.switchout.nodropout.th-en-word.yaml
# standard settings
switchout.nodropout.asean.th-en: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.0           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
(base) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-switchout$
```

## Training SwitchOut No-Dropout for ASEAN En-Th, Th-En

training for en-th language pair ...  

```
[switchout.nodropout.asean.en-th] Epoch 24.5633: train_loss/word=3.354674 (steps=10834, words/sec=10202.60, time=0-00:21:35)
[switchout.nodropout.asean.en-th] Epoch 24.6140: train_loss/word=2.736280 (steps=10862, words/sec=8028.96, time=0-00:21:37)
[switchout.nodropout.asean.en-th] Epoch 24.6666: train_loss/word=3.111305 (steps=10884, words/sec=8891.24, time=0-00:21:37)
[switchout.nodropout.asean.en-th] Epoch 24.7174: train_loss/word=3.186068 (steps=10903, words/sec=10302.89, time=0-00:21:38)
[switchout.nodropout.asean.en-th] Epoch 24.7694: train_loss/word=2.949471 (steps=10928, words/sec=8940.76, time=0-00:21:39)
[switchout.nodropout.asean.en-th] Epoch 24.8200: train_loss/word=2.857589 (steps=10954, words/sec=7556.43, time=0-00:21:40)
[switchout.nodropout.asean.en-th] Epoch 24.8719: train_loss/word=3.074174 (steps=10979, words/sec=8937.72, time=0-00:21:41)
[switchout.nodropout.asean.en-th] Epoch 24.9249: train_loss/word=3.004033 (steps=11002, words/sec=9951.02, time=0-00:21:42)
[switchout.nodropout.asean.en-th] Epoch 24.9755: train_loss/word=3.216816 (steps=11024, words/sec=9368.85, time=0-00:21:43)
[switchout.nodropout.asean.en-th] Epoch 25.0000: train_loss/word=3.241428 (steps=11034, words/sec=10119.01, time=0-00:21:43)
> Checkpoint [switchout.nodropout.asean.en-th]
Performing inference on ./data/dev.en and ./data/dev.th
Starting to read ./data/dev.en and ./data/dev.th
Done reading ./data/dev.en and ./data/dev.th. Packing into batches.
Done packing batches.
[switchout.nodropout.asean.en-th] Epoch 25.0000 dev BLEU4: 0.34160770057337403, 0.568507/0.392048/0.281373/0.217147 (BP = 1.000000, ratio=1.03, hyp_len=6992, ref_len=6809) (time=0-00:22:10)
[switchout.nodropout.asean.en-th]              dev auxiliary GLEU: 0.336515
[switchout.nodropout.asean.en-th]              dev auxiliary Loss: 4.043 (ref_len=6809)
             checkpoint took 0-00:00:26
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.en and ./data/dev.th
Performing inference on ./data/test.en and ./data/test.th
Experiment                    | Final Scores
-----------------------------------------------------------------------
switchout.nodropout.asean.en-th| BLEU4: 0.34756345881141265, 0.570658/0.398170/0.288971/0.222248 (BP = 1.000000, ratio=1.03, hyp_len=7041, ref_len=6809)
                              | GLEU: 0.342217
                              | WER: 61.98% ( C/S/I/D: 3880/1870/1291/1059; hyp_len=7041, ref_len=6809 )
                              | CER: 48.86% ( C/S/I/D: 18678/7277/2920/4859; hyp_len=28875, ref_len=30814 )
                              | BLEU4: 0.37081752511306093, 0.609105/0.423800/0.307131/0.238487 (BP = 1.000000, ratio=1.01, hyp_len=7227, ref_len=7169)
                              | GLEU: 0.368353
                              | WER: 56.10% ( C/S/I/D: 4249/1876/1102/1044; hyp_len=7227, ref_len=7169 )
                              | CER: 46.85% ( C/S/I/D: 19428/6918/2930/4695; hyp_len=29276, ref_len=31041 )

real    23m17.424s
user    23m15.745s
sys     0m2.875s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-switchout$
```

training for th-en language pair ...  

```
[switchout.nodropout.asean.th-en] Epoch 25.5653: train_loss/word=3.059163 (steps=11699, words/sec=10825.24, time=0-00:26:49)
[switchout.nodropout.asean.th-en] Epoch 25.6168: train_loss/word=3.118423 (steps=11722, words/sec=8900.61, time=0-00:26:50)
[switchout.nodropout.asean.th-en] Epoch 25.6695: train_loss/word=3.253051 (steps=11745, words/sec=10562.02, time=0-00:26:51)
[switchout.nodropout.asean.th-en] Epoch 25.7198: train_loss/word=3.223706 (steps=11769, words/sec=8041.08, time=0-00:26:52)
[switchout.nodropout.asean.th-en] Epoch 25.7709: train_loss/word=3.043218 (steps=11793, words/sec=8674.13, time=0-00:26:53)
[switchout.nodropout.asean.th-en] Epoch 25.8229: train_loss/word=3.220041 (steps=11817, words/sec=9965.41, time=0-00:26:54)
[switchout.nodropout.asean.th-en] Epoch 25.8752: train_loss/word=3.128776 (steps=11842, words/sec=9473.52, time=0-00:26:55)
[switchout.nodropout.asean.th-en] Epoch 25.9267: train_loss/word=3.019609 (steps=11865, words/sec=9157.80, time=0-00:26:56)
[switchout.nodropout.asean.th-en] Epoch 25.9789: train_loss/word=3.026770 (steps=11890, words/sec=9226.58, time=0-00:26:57)
[switchout.nodropout.asean.th-en] Epoch 26.0000: train_loss/word=2.978781 (steps=11902, words/sec=7268.18, time=0-00:26:57)
> Checkpoint [switchout.nodropout.asean.th-en]
Performing inference on ./data/dev.th and ./data/dev.en
Starting to read ./data/dev.th and ./data/dev.en
Done reading ./data/dev.th and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.nodropout.asean.th-en] Epoch 26.0000 dev BLEU4: 0.28248944660060127, 0.512647/0.351733/0.267599/0.211047 (BP = 0.889260, ratio=0.89, hyp_len=6484, ref_len=7245) (time=0-00:27:22)
[switchout.nodropout.asean.th-en]              dev auxiliary GLEU: 0.293425
[switchout.nodropout.asean.th-en]              dev auxiliary Loss: 4.706 (ref_len=7245)
             checkpoint took 0-00:00:24
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.th and ./data/dev.en
Performing inference on ./data/test.th and ./data/test.en
Experiment                    | Final Scores
-----------------------------------------------------------------------
switchout.nodropout.asean.th-en| BLEU4: 0.28460356510539947, 0.513756/0.353374/0.270154/0.215995 (BP = 0.887112, ratio=0.89, hyp_len=6470, ref_len=7245)
                              | GLEU: 0.294741
                              | WER: 61.67% ( C/S/I/D: 3288/2671/511/1286; hyp_len=6470, ref_len=7245 )
                              | CER: 50.87% ( C/S/I/D: 16974/6438/2041/6983; hyp_len=25453, ref_len=30395 )
                              | BLEU4: 0.30344751118300956, 0.531399/0.375295/0.283031/0.225707 (BP = 0.903213, ratio=0.91, hyp_len=6513, ref_len=7176)
                              | GLEU: 0.314479
                              | WER: 59.18% ( C/S/I/D: 3419/2604/490/1153; hyp_len=6513, ref_len=7176 )
                              | CER: 49.39% ( C/S/I/D: 17429/6473/2039/6506; hyp_len=25941, ref_len=30408 )

real    28m27.820s
user    28m26.188s
sys     0m2.905s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/asean-mt-switchout$
```
