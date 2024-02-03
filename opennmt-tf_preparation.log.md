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
(opennmt-tf) ye@lst-gpu-3090:~/exp/myNLP$ onmt-main --help
2024-02-03 11:52:28.083699: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2024-02-03 11:52:30.914587: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2024-02-03 11:52:35.900117: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
/home/ye/anaconda3/envs/opennmt/lib/python3.8/site-packages/tensorflow_addons/utils/tfa_eol_msg.py:23: UserWarning: 

TensorFlow Addons (TFA) has ended development and introduction of new features.
TFA has entered a minimal maintenance and release mode until a planned end of life in May 2024.
Please modify downstream libraries to take dependencies from other repositories in our TensorFlow community (e.g. Keras, Keras-CV, and Keras-NLP). 

For more information see: https://github.com/tensorflow/addons/issues/2807 

  warnings.warn(
usage: onmt-main [-h] [-v] --config CONFIG [CONFIG ...] [--model_dir MODEL_DIR] [--auto_config]
                 [--model_type {GPT2Small,ListenAttendSpell,LstmCnnCrfTagger,LuongAttention,NMTBigV1,NMTMediumV1,NMTSmallV1,ScalingNmtEnDe,ScalingNmtEnFr,Transformer,TransformerBase,TransformerBaseRelative,TransformerBaseSharedEmbeddings,TransformerBig,TransformerBigRelative,TransformerBigSharedEmbeddings,TransformerRelative,TransformerTiny}]
                 [--model MODEL] [--run_dir RUN_DIR] [--data_dir DATA_DIR] [--checkpoint_path CHECKPOINT_PATH]
                 [--log_level {CRITICAL,ERROR,WARNING,INFO,DEBUG,NOTSET}] [--seed SEED] [--gpu_allow_growth]
                 [--intra_op_parallelism_threads INTRA_OP_PARALLELISM_THREADS]
                 [--inter_op_parallelism_threads INTER_OP_PARALLELISM_THREADS] [--mixed_precision] [--jit_compile]
                 [--eager_execution]
                 {train,eval,infer,export,score,average_checkpoints,update_vocab} ...

positional arguments:
  {train,eval,infer,export,score,average_checkpoints,update_vocab}
                        Run type.
    train               Training.
    eval                Evaluation.
    infer               Inference.
    export              Model export.
    score               Scoring.
    average_checkpoints
                        Checkpoint averaging.
    update_vocab        Update model vocabularies in checkpoint.

optional arguments:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit
  --config CONFIG [CONFIG ...]
                        List of configuration files. (default: None)
  --model_dir MODEL_DIR
                        Path to the model directory. If not set, the model directory is read from the field 'model_dir' in
                        the configuration. (default: None)
  --auto_config         Enable automatic configuration values. (default: None)
  --model_type {GPT2Small,ListenAttendSpell,LstmCnnCrfTagger,LuongAttention,NMTBigV1,NMTMediumV1,NMTSmallV1,ScalingNmtEnDe,ScalingNmtEnFr,Transformer,TransformerBase,TransformerBaseRelative,TransformerBaseSharedEmbeddings,TransformerBig,TransformerBigRelative,TransformerBigSharedEmbeddings,TransformerRelative,TransformerTiny}
                        Model type from the catalog. (default: )
  --model MODEL         Custom model configuration file. (default: )
  --run_dir RUN_DIR     If set, model_dir will be created relative to this location. (default: )
  --data_dir DATA_DIR   If set, data files are expected to be relative to this location. (default: )
  --checkpoint_path CHECKPOINT_PATH
                        Path to the checkpoint or checkpoint directory to load. If not set, the latest checkpoint from the
                        model directory is loaded. (default: None)
  --log_level {CRITICAL,ERROR,WARNING,INFO,DEBUG,NOTSET}
                        Logs verbosity. (default: INFO)
  --seed SEED           Random seed. (default: None)
  --gpu_allow_growth    Allocate GPU memory dynamically. (default: False)
  --intra_op_parallelism_threads INTRA_OP_PARALLELISM_THREADS
                        Number of intra op threads (0 means the system picks an appropriate number). (default: 0)
  --inter_op_parallelism_threads INTER_OP_PARALLELISM_THREADS
                        Number of inter op threads (0 means the system picks an appropriate number). (default: 0)
  --mixed_precision     Enable mixed precision. (default: False)
  --jit_compile         Compile the model with XLA when possible. (default: False)
  --eager_execution     Enable TensorFlow eager execution. (default: False)
(opennmt-tf) ye@lst-gpu-3090:~/exp/myNLP$ 
```

## Check Tensorflow Version

```
(opennmt-tf) ye@lst-gpu-3090:~/exp/myNLP$ python
Python 3.8.18 (default, Sep 11 2023, 13:40:15) 
[GCC 11.2.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
2024-02-03 11:54:03.357070: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2024-02-03 11:54:03.379965: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2024-02-03 11:54:03.755345: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
>>> print(tf.__version__)
2.13.1
>>> 

```

## Check GPU Status

```
(opennmt-tf) ye@lst-gpu-3090:~/exp/myNLP$ nvidia-smi
Sat Feb  3 11:54:56 2024       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 525.147.05   Driver Version: 525.147.05   CUDA Version: 12.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:01:00.0  On |                  Off |
|  0%   45C    P8    35W / 480W |    484MiB / 24564MiB |      6%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      2013      G   /usr/lib/xorg/Xorg                 29MiB |
|    0   N/A  N/A     60384      G   /usr/lib/xorg/Xorg                215MiB |
|    0   N/A  N/A     60667      G   /usr/bin/gnome-shell              116MiB |
|    0   N/A  N/A     64126      G   ...on=20240126-130123.803000       41MiB |
+-----------------------------------------------------------------------------+
(opennmt-tf) ye@lst-gpu-3090:~/exp/myNLP$ 
```

## JupyterLab Installation

```
pip install jupyterlab
```

Test Jupyter Lab ...  

```
(opennmt-tf) ye@lst-gpu-3090:~/exp/opennmt/notebook$ jupyter lab
```

Now, you can run OpenNMT-TF.  
