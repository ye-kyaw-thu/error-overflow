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

```

command:  

```

```

result:  

```

```
