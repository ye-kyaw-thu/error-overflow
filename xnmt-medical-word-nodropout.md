# Medical Domain Word Unit No-Dropout Experiment Log

## Preparing config files for Seq2Seq No-Dropout

```yaml
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$ head ./config.medical.en-my-word.nodropout.yaml
# standard settings
medical.word.nodropout.en-my: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.0           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
```

```yaml
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$ head ./config.medical.my-en-word.nodropout.yaml
# standard settings
medical.word.nodropout.my-en: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.0           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$
```

## Training

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$ time xnmt --backend torch --gpu ./config.medical.en-my-word.nodropout.yaml | tee switchout.nodropout.en-my-word.log
```

result  

```
[medical.word.nodropout.en-my] Epoch 19.5323: train_loss/word=1.646143 (steps=5635, words/sec=11333.98, time=0-00:19:34)
[medical.word.nodropout.en-my] Epoch 19.6084: train_loss/word=1.638700 (steps=5654, words/sec=12151.21, time=0-00:19:36)
[medical.word.nodropout.en-my] Epoch 19.6845: train_loss/word=1.639620 (steps=5676, words/sec=11626.72, time=0-00:19:37)
[medical.word.nodropout.en-my] Epoch 19.7598: train_loss/word=1.660359 (steps=5698, words/sec=11316.18, time=0-00:19:39)
[medical.word.nodropout.en-my] Epoch 19.8378: train_loss/word=1.635920 (steps=5719, words/sec=12378.49, time=0-00:19:41)
[medical.word.nodropout.en-my] Epoch 19.9120: train_loss/word=1.654850 (steps=5738, words/sec=12075.13, time=0-00:19:42)
[medical.word.nodropout.en-my] Epoch 19.9872: train_loss/word=1.635910 (steps=5760, words/sec=11215.02, time=0-00:19:44)
[medical.word.nodropout.en-my] Epoch 20.0000: train_loss/word=1.636023 (steps=5764, words/sec=11033.63, time=0-00:19:44)
> Checkpoint [medical.word.nodropout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[medical.word.nodropout.en-my] Epoch 20.0000 dev BLEU4: 0.16784699369385003, 0.479447/0.228441/0.116093/0.062680 (BP = 0.998966, ratio=1.00, hyp_len=7736, ref_len=7744) (time=0-00:20:13)
[medical.word.nodropout.en-my]              dev auxiliary GLEU: 0.213870
[medical.word.nodropout.en-my]              dev auxiliary Loss: 5.330 (ref_len=7744)
             checkpoint took 0-00:00:29
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.en and ./data/dev.my
Performing inference on ./data/test.en and ./data/test.my
Experiment                    | Final Scores
-----------------------------------------------------------------------
medical.word.nodropout.en-my  | BLEU4: 0.17013665018799728, 0.473316/0.229363/0.117411/0.066559 (BP = 0.996896, ratio=1.00, hyp_len=7720, ref_len=7744)
                              | GLEU: 0.212399
                              | WER: 72.16% ( C/S/I/D: 3164/3548/1008/1032; hyp_len=7720, ref_len=7744 )
                              | CER: 59.01% ( C/S/I/D: 19558/10787/4335/6795; hyp_len=34680, ref_len=37140 )
                              | BLEU4: 0.1705199688299613, 0.485771/0.237886/0.116800/0.062797 (BP = 0.999376, ratio=1.00, hyp_len=8012, ref_len=8017)
                              | GLEU: 0.216813
                              | WER: 71.36% ( C/S/I/D: 3349/3610/1053/1058; hyp_len=8012, ref_len=8017 )
                              | CER: 59.11% ( C/S/I/D: 20410/10742/4756/7128; hyp_len=35908, ref_len=38280 )

real    21m30.843s
user    21m21.981s
sys     0m10.017s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$
```

command    

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$ time xnmt --backend torch --gpu ./config.medical.my-en-word.nodropout.yaml | tee switcho
ut.nodropout.my-en-word.log
```

result  

```
[medical.word.nodropout.my-en] Epoch 28.9099: train_loss/word=1.438401 (steps=7835, words/sec=13384.34, time=0-00:23:15)
[medical.word.nodropout.my-en] Epoch 28.9835: train_loss/word=1.438354 (steps=7855, words/sec=11533.41, time=0-00:23:17)
[medical.word.nodropout.my-en] Epoch 29.0000: train_loss/word=1.438122 (steps=7859, words/sec=13505.72, time=0-00:23:17)
> Checkpoint [medical.word.nodropout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[medical.word.nodropout.my-en] Epoch 29.0000 dev BLEU4: 0.24470525213426483, 0.545013/0.296705/0.195846/0.134164 (BP = 0.958458, ratio=0.96, hyp_len=6387, ref_len=6658) (time=0-00:23:40)
[medical.word.nodropout.my-en]              dev auxiliary GLEU: 0.274967
[medical.word.nodropout.my-en]              dev auxiliary Loss: 4.970 (ref_len=6658)
             checkpoint took 0-00:00:23
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.my and ./data/dev.en
Performing inference on ./data/test.my and ./data/test.en
Experiment                    | Final Scores
-----------------------------------------------------------------------
medical.word.nodropout.my-en  | BLEU4: 0.24562800715957595, 0.535422/0.291639/0.193290/0.134696 (BP = 0.972750, ratio=0.97, hyp_len=6479, ref_len=6658)
                              | GLEU: 0.273092
                              | WER: 63.04% ( C/S/I/D: 3157/2626/696/875; hyp_len=6479, ref_len=6658 )
                              | CER: 56.71% ( C/S/I/D: 14402/7515/2806/4869; hyp_len=24723, ref_len=26786 )
                              | BLEU4: 0.2426041985359957, 0.528529/0.286035/0.189288/0.136173 (BP = 0.971008, ratio=0.97, hyp_len=6730, ref_len=6928)
                              | GLEU: 0.271245
                              | WER: 63.05% ( C/S/I/D: 3230/2830/670/868; hyp_len=6730, ref_len=6928 )
                              | CER: 56.86% ( C/S/I/D: 14697/7868/2817/4976; hyp_len=25382, ref_len=27541 )

real    24m45.212s
user    24m43.493s
sys     0m2.945s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word$
```

## Preparing Config Files for Word Unit Switchout with No-Dropout

```yaml
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word_switchout$ head ./config.switchout.nodropout.en-my-word.yaml
# standard settings
switchout.nodropout.en-my: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.0           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
```

```yaml
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word_switchout$ head ./config.switchout.nodropout.my-en-word.yaml
# standard settings
switchout.nodropout.my-en: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.0           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word_switchout$
```

## Training Word Switchout No-Dropout

command:  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word_switchout$ time xnmt --backend torch --gpu ./config.switchout.nodropout.en-my-word.yaml | tee switchout.nodropout.en-my-word.log
```

result:  

```
[switchout.nodropout.en-my] Epoch 22.3791: train_loss/word=2.907220 (steps=6437, words/sec=10788.76, time=0-00:23:50)
[switchout.nodropout.en-my] Epoch 22.4556: train_loss/word=2.983515 (steps=6455, words/sec=13534.28, time=0-00:23:51)
[switchout.nodropout.en-my] Epoch 22.5310: train_loss/word=2.802518 (steps=6477, words/sec=11435.54, time=0-00:23:53)
[switchout.nodropout.en-my] Epoch 22.6068: train_loss/word=2.887820 (steps=6498, words/sec=11447.73, time=0-00:23:55)
[switchout.nodropout.en-my] Epoch 22.6854: train_loss/word=2.817711 (steps=6523, words/sec=9899.16, time=0-00:23:57)
[switchout.nodropout.en-my] Epoch 22.7595: train_loss/word=2.773578 (steps=6544, words/sec=11079.28, time=0-00:23:58)
[switchout.nodropout.en-my] Epoch 22.8356: train_loss/word=2.886686 (steps=6564, words/sec=12696.19, time=0-00:24:00)
[switchout.nodropout.en-my] Epoch 22.9100: train_loss/word=2.718673 (steps=6590, words/sec=9688.55, time=0-00:24:02)
[switchout.nodropout.en-my] Epoch 22.9888: train_loss/word=2.806439 (steps=6612, words/sec=11484.12, time=0-00:24:04)
[switchout.nodropout.en-my] Epoch 23.0000: train_loss/word=2.888503 (steps=6615, words/sec=12417.11, time=0-00:24:04)
> Checkpoint [switchout.nodropout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.nodropout.en-my] Epoch 23.0000 dev BLEU4: 0.14293925006627745, 0.460311/0.208479/0.097036/0.047162 (BP = 0.987395, ratio=0.99, hyp_len=7647, ref_len=7744) (time=0-00:24:34)
[switchout.nodropout.en-my]              dev auxiliary GLEU: 0.194230
[switchout.nodropout.en-my]              dev auxiliary Loss: 4.989 (ref_len=7744)
             checkpoint took 0-00:00:29
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.en and ./data/dev.my
Performing inference on ./data/test.en and ./data/test.my
Experiment                    | Final Scores
-----------------------------------------------------------------------
switchout.nodropout.en-my     | BLEU4: 0.1478841963800444, 0.462133/0.210881/0.100724/0.051671 (BP = 0.985432, ratio=0.99, hyp_len=7632, ref_len=7744)
                              | GLEU: 0.196319
                              | WER: 73.66% ( C/S/I/D: 3032/3608/992/1104; hyp_len=7632, ref_len=7744 )
                              | CER: 60.89% ( C/S/I/D: 18379/11078/3852/7683; hyp_len=33309, ref_len=37140 )
                              | BLEU4: 0.155386772206501, 0.470128/0.217339/0.104381/0.057495 (BP = 0.987448, ratio=0.99, hyp_len=7917, ref_len=8017)
                              | GLEU: 0.202573
                              | WER: 72.78% ( C/S/I/D: 3177/3745/995/1095; hyp_len=7917, ref_len=8017 )
                              | CER: 60.35% ( C/S/I/D: 19271/11483/4093/7526; hyp_len=34847, ref_len=38280 )

real    25m51.062s
user    25m42.239s
sys     0m10.042s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word_switchout$
```

command:  

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word_switchout$ time xnmt --backend torch --gpu ./config.switchout.nodropout.my-en-word.yaml |
 tee switchout.nodropout.my-en-word.log
```

result:  

```
[switchout.nodropout.my-en] Epoch 21.3774: train_loss/word=2.459924 (steps=5797, words/sec=10109.57, time=0-00:18:02)
[switchout.nodropout.my-en] Epoch 21.4537: train_loss/word=2.592933 (steps=5818, words/sec=12251.98, time=0-00:18:04)
[switchout.nodropout.my-en] Epoch 21.5316: train_loss/word=2.619566 (steps=5839, words/sec=11396.96, time=0-00:18:05)
[switchout.nodropout.my-en] Epoch 21.6069: train_loss/word=2.712008 (steps=5857, words/sec=12122.32, time=0-00:18:06)
[switchout.nodropout.my-en] Epoch 21.6865: train_loss/word=2.560473 (steps=5879, words/sec=11877.93, time=0-00:18:08)
[switchout.nodropout.my-en] Epoch 21.7607: train_loss/word=2.604162 (steps=5900, words/sec=12322.16, time=0-00:18:09)
[switchout.nodropout.my-en] Epoch 21.8381: train_loss/word=2.662415 (steps=5920, words/sec=12520.39, time=0-00:18:10)
[switchout.nodropout.my-en] Epoch 21.9142: train_loss/word=2.780188 (steps=5938, words/sec=12509.37, time=0-00:18:11)
[switchout.nodropout.my-en] Epoch 21.9934: train_loss/word=2.796579 (steps=5957, words/sec=11231.97, time=0-00:18:13)
[switchout.nodropout.my-en] Epoch 22.0000: train_loss/word=2.410786 (steps=5959, words/sec=10769.35, time=0-00:18:13)
> Checkpoint [switchout.nodropout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.nodropout.my-en] Epoch 22.0000 dev BLEU4: 0.23903233195905252, 0.536012/0.290014/0.196037/0.139280 (BP = 0.936486, ratio=0.94, hyp_len=6248, ref_len=6658) (time=0-00:18:36)
[switchout.nodropout.my-en]              dev auxiliary GLEU: 0.268645
[switchout.nodropout.my-en]              dev auxiliary Loss: 4.371 (ref_len=6658)
             checkpoint took 0-00:00:22
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.my and ./data/dev.en
Performing inference on ./data/test.my and ./data/test.en
Experiment                    | Final Scores
-----------------------------------------------------------------------
switchout.nodropout.my-en     | BLEU4: 0.2422414517829107, 0.537393/0.290682/0.195542/0.137960 (BP = 0.950764, ratio=0.95, hyp_len=6338, ref_len=6658)
                              | GLEU: 0.271590
                              | WER: 62.41% ( C/S/I/D: 3094/2653/591/911; hyp_len=6338, ref_len=6658 )
                              | CER: 57.08% ( C/S/I/D: 13940/7230/2444/5616; hyp_len=23614, ref_len=26786 )
                              | BLEU4: 0.2399637231543298, 0.527824/0.286087/0.192048/0.136770 (BP = 0.956199, ratio=0.96, hyp_len=6631, ref_len=6928)
                              | GLEU: 0.267928
                              | WER: 63.18% ( C/S/I/D: 3203/2776/652/949; hyp_len=6631, ref_len=6928 )
                              | CER: 57.93% ( C/S/I/D: 14179/7608/2592/5754; hyp_len=24379, ref_len=27541 )

real    19m40.130s
user    19m38.498s
sys     0m2.772s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word_switchout$
```
