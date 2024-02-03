# OpenNMT-tf Preparation Log

## Create a New Anaconda Environment

conda create --name opennmt-tf python=3.8
conda activate opennmt-tf

## OpenNMT-tf Installation

```
(opennmt-tf) ye@lst-gpu-3090:~/exp/myNLP$ pip install --upgrade pip
Requirement already satisfied: pip in /home/ye/anaconda3/envs/opennmt/lib/python3.8/site-packages (23.3.1)
Collecting pip
  Downloading pip-23.3.2-py3-none-any.whl.metadata (3.5 kB)
Downloading pip-23.3.2-py3-none-any.whl (2.1 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.1/2.1 MB 16.7 MB/s eta 0:00:00
Installing collected packages: pip
  Attempting uninstall: pip
    Found existing installation: pip 23.3.1
    Uninstalling pip-23.3.1:
      Successfully uninstalled pip-23.3.1
Successfully installed pip-23.3.2
(opennmt-tf) ye@lst-gpu-3090:~/exp/myNLP$ 
```

```
(opennmt-tf) ye@lst-gpu-3090:~/exp/myNLP$ pip install OpenNMT-tf
Collecting OpenNMT-tf
  Downloading OpenNMT_tf-2.32.0-py3-none-any.whl.metadata (11 kB)
Requirement already satisfied: ctranslate2<4,>=3.0 in /home/ye/anaconda3/envs/opennmt/lib/python3.8/site-packages (from OpenNMT-tf) (3.24.0)
Requirement already satisfied: packaging in /home/ye/anaconda3/envs/opennmt/lib/python3.8/site-packages (from OpenNMT-tf) (23.2)
Requirement already satisfied: pyonmttok<2,>=1.29.0 in /home/ye/anaconda3/envs/opennmt/lib/python3.8/site-packages (from OpenNMT-tf) (1.37.1)
Requirement already satisfied: pyyaml<7,>=5.3 in /home/ye/anaconda3/envs/opennmt/lib/python3.8/site-packages (from OpenNMT-tf) (6.0.1)
Collecting rouge<2,>=1.0 (from OpenNMT-tf)
  Downloading rouge-1.0.1-py3-none-any.whl (13 kB)
Requirement already satisfied: sacrebleu<3,>=1.5.0 in /home/ye/anaconda3/envs/opennmt/lib/python3.8/site-packages (from OpenNMT-tf) (2.4.0)
Collecting tensorflow-addons<0.22,>=0.16 (from OpenNMT-tf)
  Downloading tensorflow_addons-0.21.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (1.8 kB)
Requirement already satisfied: setuptools in /home/ye/anaconda3/envs/opennmt/lib/python3.8/site-packages (from ctranslate2<4,>=3.0->OpenNMT-tf) (68.2.2)
Requirement already satisfied: numpy in /home/ye/anaconda3/envs/opennmt/lib/python3.8/site-packages (from ctranslate2<4,>=3.0->OpenNMT-tf) (1.24.3)
Requirement already satisfied: six in /home/ye/anaconda3/envs/opennmt/lib/python3.8/site-packages (from rouge<2,>=1.0->OpenNMT-tf) (1.16.0)
Requirement already satisfied: portalocker in /home/ye/anaconda3/envs/opennmt/lib/python3.8/site-packages (from sacrebleu<3,>=1.5.0->OpenNMT-tf) (2.8.2)
Requirement already satisfied: regex in /home/ye/anaconda3/envs/opennmt/lib/python3.8/site-packages (from sacrebleu<3,>=1.5.0->OpenNMT-tf) (2023.12.25)
Requirement already satisfied: tabulate>=0.8.9 in /home/ye/anaconda3/envs/opennmt/lib/python3.8/site-packages (from sacrebleu<3,>=1.5.0->OpenNMT-tf) (0.9.0)
Requirement already satisfied: colorama in /home/ye/anaconda3/envs/opennmt/lib/python3.8/site-packages (from sacrebleu<3,>=1.5.0->OpenNMT-tf) (0.4.6)
Requirement already satisfied: lxml in /home/ye/anaconda3/envs/opennmt/lib/python3.8/site-packages (from sacrebleu<3,>=1.5.0->OpenNMT-tf) (5.1.0)
Collecting typeguard<3.0.0,>=2.7 (from tensorflow-addons<0.22,>=0.16->OpenNMT-tf)
  Downloading typeguard-2.13.3-py3-none-any.whl (17 kB)
Downloading OpenNMT_tf-2.32.0-py3-none-any.whl (162 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 162.0/162.0 kB 1.7 MB/s eta 0:00:00
Downloading tensorflow_addons-0.21.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (612 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 612.0/612.0 kB 2.8 MB/s eta 0:00:00
Installing collected packages: typeguard, rouge, tensorflow-addons, OpenNMT-tf
Successfully installed OpenNMT-tf-2.32.0 rouge-1.0.1 tensorflow-addons-0.21.0 typeguard-2.13.3
(opennmt-tf) ye@lst-gpu-3090:~/exp/myNLP$
```

## Check OpenNMT Commands

```
(opennmt-tf) ye@lst-gpu-3090:~/exp/myNLP$ onmt
onmt-ark-to-records     onmt_build_vocab        onmt-merge-config       onmt-tokenize-text      onmt_translate_dynamic
onmt_average_models     onmt-detokenize-text    onmt_release_model      onmt_train              
onmt-build-vocab        onmt-main               onmt_server             onmt_translate          
(opennmt-tf) ye@lst-gpu-3090:~/exp/myNLP$
```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
