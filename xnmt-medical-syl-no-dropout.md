# XNMT Medical Syllable No-dropout

updated experiment name and the droupout=0.0 (i.e. no dropout)  
```yaml
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$ head ./config.medical.en-my-syl.nodorpout.yaml
# standard settings
medical.syl.nodropout.en-my: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.0           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
```

updated experiment name and the dropout=0.0 (i.e. no dropout)  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$ head ./config.medical.my-en-syl.nodropout.yaml
# standard settings
medical.syl.nodropout.my-en: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.0           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$
```

## Training

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$ time xnmt --backend torch --gpu ./config.medical.en-my-syl.nodorpout.yaml | tee en-my.syl.nodropout.log
```

result for en-my, syllable, no dropout:  

```
[medical.syl.nodropout.en-my] Epoch 17.3843: train_loss/word=1.401172 (steps=5289, words/sec=14426.48, time=0-00:20:07)
[medical.syl.nodropout.en-my] Epoch 17.4591: train_loss/word=1.410266 (steps=5311, words/sec=13735.18, time=0-00:20:09)
[medical.syl.nodropout.en-my] Epoch 17.5361: train_loss/word=1.411062 (steps=5334, words/sec=13584.78, time=0-00:20:11)
[medical.syl.nodropout.en-my] Epoch 17.6112: train_loss/word=1.412769 (steps=5358, words/sec=13124.23, time=0-00:20:13)
[medical.syl.nodropout.en-my] Epoch 17.6849: train_loss/word=1.430642 (steps=5380, words/sec=13810.25, time=0-00:20:15)
[medical.syl.nodropout.en-my] Epoch 17.7588: train_loss/word=1.410882 (steps=5403, words/sec=13965.12, time=0-00:20:17)
[medical.syl.nodropout.en-my] Epoch 17.8333: train_loss/word=1.431488 (steps=5426, words/sec=13362.55, time=0-00:20:19)
[medical.syl.nodropout.en-my] Epoch 17.9122: train_loss/word=1.431462 (steps=5451, words/sec=12526.75, time=0-00:20:22)
[medical.syl.nodropout.en-my] Epoch 17.9871: train_loss/word=1.445107 (steps=5473, words/sec=13428.68, time=0-00:20:24)
[medical.syl.nodropout.en-my] Epoch 18.0000: train_loss/word=1.359578 (steps=5476, words/sec=16992.09, time=0-00:20:24)
> Checkpoint [medical.syl.nodropout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.syl.nodropout.en-my] Epoch 18.0000 dev BLEU4: 0.3340348673826803, 0.626445/0.412531/0.275580/0.193890 (BP = 0.974442, ratio=0.97, hyp_len=12630, ref_len=12957) (time=0-00:21:00)
[medical.syl.nodropout.en-my]              dev auxiliary GLEU: 0.351087
[medical.syl.nodropout.en-my]              dev auxiliary Loss: 3.409 (ref_len=12957)
             checkpoint took 0-00:00:36
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.en and ./data/dev.my
Performing inference on ./data/test.en and ./data/test.my
Experiment                    | Final Scores
-----------------------------------------------------------------------
medical.syl.nodropout.en-my   | BLEU4: 0.33669193948309056, 0.627004/0.415701/0.278440/0.194178 (BP = 0.977208, ratio=0.98, hyp_len=12665, ref_len=12957)
                              | GLEU: 0.354006
                              | WER: 60.80% ( C/S/I/D: 6669/4406/1590/1882; hyp_len=12665, ref_len=12957 )
                              | CER: 55.10% ( C/S/I/D: 21391/9689/4716/6060; hyp_len=35796, ref_len=37140 )
                              | BLEU4: 0.3468145457361847, 0.624441/0.418801/0.287343/0.205372 (BP = 0.983982, ratio=0.98, hyp_len=13191, ref_len=13404)
                              | GLEU: 0.359365
                              | WER: 59.85% ( C/S/I/D: 7001/4571/1619/1832; hyp_len=13191, ref_len=13404 )
                              | CER: 54.42% ( C/S/I/D: 22355/9891/4906/6034; hyp_len=37152, ref_len=38280 )

real    22m25.292s
user    22m24.267s
sys     0m2.184s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$
```

training for my-en ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$ time xnmt --backend torch --gpu ./config.medical.my-en-syl.nodropout.yaml | tee my-en.syl.nodropout.log
```

result for my-en, syllable, no dropout ...  

```
[medical.syl.nodropout.my-en] Epoch 18.3800: train_loss/word=2.012662 (steps=4685, words/sec=9574.99, time=0-00:14:48)
[medical.syl.nodropout.my-en] Epoch 18.4539: train_loss/word=1.980176 (steps=4702, words/sec=10768.71, time=0-00:14:49)
[medical.syl.nodropout.my-en] Epoch 18.5294: train_loss/word=2.051752 (steps=4722, words/sec=9717.09, time=0-00:14:51)
[medical.syl.nodropout.my-en] Epoch 18.6053: train_loss/word=1.999263 (steps=4742, words/sec=9816.82, time=0-00:14:52)
[medical.syl.nodropout.my-en] Epoch 18.6805: train_loss/word=1.999332 (steps=4761, words/sec=10127.90, time=0-00:14:54)
[medical.syl.nodropout.my-en] Epoch 18.7548: train_loss/word=1.998372 (steps=4779, words/sec=10233.81, time=0-00:14:55)
[medical.syl.nodropout.my-en] Epoch 18.8286: train_loss/word=2.003607 (steps=4796, words/sec=9150.63, time=0-00:14:57)
[medical.syl.nodropout.my-en] Epoch 18.9042: train_loss/word=1.965679 (steps=4812, words/sec=11630.88, time=0-00:14:58)
[medical.syl.nodropout.my-en] Epoch 18.9819: train_loss/word=2.080426 (steps=4836, words/sec=8842.12, time=0-00:15:00)
[medical.syl.nodropout.my-en] Epoch 19.0000: train_loss/word=2.088435 (steps=4842, words/sec=9446.26, time=0-00:15:00)
> Checkpoint [medical.syl.nodropout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[medical.syl.nodropout.my-en] Epoch 19.0000 dev BLEU4: 0.15340692164834868, 0.390150/0.168082/0.110550/0.076396 (BP = 1.000000, ratio=1.01, hyp_len=6741, ref_len=6658) (time=0-00:15:27)
[medical.syl.nodropout.my-en]              dev auxiliary GLEU: 0.178869
[medical.syl.nodropout.my-en]              dev auxiliary Loss: 5.082 (ref_len=6658)
             checkpoint took 0-00:00:26
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.my and ./data/dev.en
Performing inference on ./data/test.my and ./data/test.en
Experiment                    | Final Scores
-----------------------------------------------------------------------
medical.syl.nodropout.my-en   | BLEU4: 0.15895698309835926, 0.396994/0.177099/0.117552/0.080651 (BP = 0.989279, ratio=0.99, hyp_len=6587, ref_len=6658)
                              | GLEU: 0.183193
                              | WER: 76.79% ( C/S/I/D: 2289/3554/744/815; hyp_len=6587, ref_len=6658 )
                              | CER: 68.47% ( C/S/I/D: 11712/9949/3267/5125; hyp_len=24928, ref_len=26786 )
                              | BLEU4: 0.14823426256716127, 0.388848/0.165803/0.105756/0.073289 (BP = 0.991447, ratio=0.99, hyp_len=6869, ref_len=6928)
                              | GLEU: 0.175279
                              | WER: 77.66% ( C/S/I/D: 2343/3731/795/854; hyp_len=6869, ref_len=6928 )
                              | CER: 69.50% ( C/S/I/D: 11834/10679/3434/5028; hyp_len=25947, ref_len=27541 )

real    16m30.376s
user    16m29.297s
sys     0m2.184s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl$
```

## Medical Domain Syllable SwitchOut and No-Dropout

preparing config files ...  
for en-my, syllable, no-dropout, switchout:  

```yaml
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl_switchout$ head ./config.switchout.nodropout.en-my-syl.yaml
# standard settings
switchout.nodropout.syl.en-my: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.0           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
```

for my-en, syllable, no-dropout, switchout:  

```yaml
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl_switchout$ head ./config.switchout.nodropout.en-my-syl.yaml
# standard settings
switchout.nodropout.syl.en-my: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.0           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
```

## Training

command ...  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl_switchout$ time xnmt --backend torch --gpu ./config.switchout.nodropout.en-my-syl.yaml | tee switchout.nodropout.en-my-syl.log
```

result for en-my, switchout, nodropout, syllable unit ...  

```
[switchout.nodropout.syl.en-my] Epoch 20.3807: train_loss/word=1.955596 (steps=6211, words/sec=13331.20, time=0-00:23:17)
[switchout.nodropout.syl.en-my] Epoch 20.4549: train_loss/word=2.035654 (steps=6232, words/sec=14799.07, time=0-00:23:19)
[switchout.nodropout.syl.en-my] Epoch 20.5306: train_loss/word=1.993931 (steps=6253, words/sec=15394.95, time=0-00:23:21)
[switchout.nodropout.syl.en-my] Epoch 20.6076: train_loss/word=2.007725 (steps=6276, words/sec=13835.60, time=0-00:23:23)
[switchout.nodropout.syl.en-my] Epoch 20.6850: train_loss/word=2.022797 (steps=6300, words/sec=13295.64, time=0-00:23:25)
[switchout.nodropout.syl.en-my] Epoch 20.7603: train_loss/word=2.015961 (steps=6324, words/sec=11770.73, time=0-00:23:28)
[switchout.nodropout.syl.en-my] Epoch 20.8355: train_loss/word=1.983724 (steps=6349, words/sec=13092.45, time=0-00:23:30)
[switchout.nodropout.syl.en-my] Epoch 20.9100: train_loss/word=2.081794 (steps=6371, words/sec=13441.40, time=0-00:23:32)
[switchout.nodropout.syl.en-my] Epoch 20.9851: train_loss/word=1.987199 (steps=6394, words/sec=14009.17, time=0-00:23:34)
[switchout.nodropout.syl.en-my] Epoch 21.0000: train_loss/word=2.046443 (steps=6398, words/sec=16853.24, time=0-00:23:34)
> Checkpoint [switchout.nodropout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.nodropout.syl.en-my] Epoch 21.0000 dev BLEU4: 0.3435070829692638, 0.649184/0.439618/0.299209/0.214474 (BP = 0.933765, ratio=0.94, hyp_len=12126, ref_len=12957) (time=0-00:24:08)
[switchout.nodropout.syl.en-my]              dev auxiliary GLEU: 0.360906
[switchout.nodropout.syl.en-my]              dev auxiliary Loss: 2.979 (ref_len=12957)
             checkpoint took 0-00:00:33
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.en and ./data/dev.my
Performing inference on ./data/test.en and ./data/test.my
Experiment                    | Final Scores
-----------------------------------------------------------------------
switchout.nodropout.syl.en-my | BLEU4: 0.34540814958202326, 0.649653/0.436271/0.298266/0.212471 (BP = 0.943512, ratio=0.95, hyp_len=12245, ref_len=12957)
                              | GLEU: 0.360589
                              | WER: 58.38% ( C/S/I/D: 6885/3868/1492/2204; hyp_len=12245, ref_len=12957 )
                              | CER: 52.61% ( C/S/I/D: 21971/8493/4372/6676; hyp_len=34836, ref_len=37140 )
                              | BLEU4: 0.35348586236960633, 0.650419/0.442342/0.307085/0.223696 (BP = 0.942768, ratio=0.94, hyp_len=12658, ref_len=13404)
                              | GLEU: 0.367651
                              | WER: 58.42% ( C/S/I/D: 7059/4114/1485/2231; hyp_len=12658, ref_len=13404 )
                              | CER: 53.04% ( C/S/I/D: 22302/9143/4324/6835; hyp_len=35769, ref_len=38280 )

real    25m28.034s
user    25m26.861s
sys     0m2.393s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl_switchout$
```

command ...  

```

```

result for en-my, switchout, nodropout, syllable unit ...  

```

```
