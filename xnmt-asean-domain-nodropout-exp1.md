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

```

```
