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


