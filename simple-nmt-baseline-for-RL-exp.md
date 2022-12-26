# Preparing a Baseline for RL experiments

For this time, I wanna run for 100 epochs baselines ...  

## Preparing to Run

```
root@69b2889746d7:/# conda create --name simple-nmt
...
...
...
==> WARNING: A newer version of conda exists. <==
  current version: 4.5.11
  latest version: 22.11.1

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /root/anaconda3/envs/simple-nmt


Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate simple-nmt
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```

activate the new env ...  

```
root@69b2889746d7:/# conda activate simple-nmt
(simple-nmt) root@69b2889746d7:/#
```

installed torch ...  

```
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt# pip install torch
...
...
...

  Downloading https://files.pythonhosted.org/packages/36/92/89cf558b514125d2ebd8344dd2f0533404b416486ff681d5434a5832a019/nvidia_cuda_runtime_cu11-11.7.99-py3-none-manylinux1_x86_64.whl (849kB)
    100% |████████████████████████████████| 849kB 46.1MB/s
Collecting nvidia-cudnn-cu11==8.5.0.96; platform_system == "Linux" (from torch)
  Downloading https://files.pythonhosted.org/packages/dc/30/66d4347d6e864334da5bb1c7571305e501dcb11b9155971421bb7bb5315f/nvidia_cudnn_cu11-8.5.0.96-2-py3-none-manylinux1_x86_64.whl (557.1MB)
    100% |████████████████████████████████| 557.1MB 214kB/s
Collecting typing-extensions (from torch)
  Downloading https://files.pythonhosted.org/packages/0b/8e/f1a0a5a76cfef77e1eb6004cb49e5f8d72634da638420b9ea492ce8305e8/typing_extensions-4.4.0-py3-none-any.whl
Collecting nvidia-cublas-cu11==11.10.3.66; platform_system == "Linux" (from torch)
  Downloading https://files.pythonhosted.org/packages/ce/41/fdeb62b5437996e841d83d7d2714ca75b886547ee8017ee2fe6ea409d983/nvidia_cublas_cu11-11.10.3.66-py3-none-manylinux1_x86_64.whl (317.1MB)
    100% |████████████████████████████████| 317.1MB 376kB/s
Collecting nvidia-cuda-nvrtc-cu11==11.7.99; platform_system == "Linux" (from torch)
  Downloading https://files.pythonhosted.org/packages/ef/25/922c5996aada6611b79b53985af7999fc629aee1d5d001b6a22431e18fec/nvidia_cuda_nvrtc_cu11-11.7.99-2-py3-none-manylinux1_x86_64.whl (21.0MB)
    100% |████████████████████████████████| 21.0MB 4.4MB/s
Requirement already satisfied: setuptools in /root/anaconda3/lib/python3.7/site-packages (from nvidia-cuda-runtime-cu11==11.7.99; platform_system == "Linux"->torch) (40.2.0)
Requirement already satisfied: wheel in /root/anaconda3/lib/python3.7/site-packages (from nvidia-cuda-runtime-cu11==11.7.99; platform_system == "Linux"->torch) (0.31.1)
twisted 18.7.0 requires PyHamcrest>=1.9.0, which is not installed.
Installing collected packages: nvidia-cuda-runtime-cu11, nvidia-cublas-cu11, nvidia-cudnn-cu11, typing-extensions, nvidia-cuda-nvrtc-cu11, torch
Successfully installed nvidia-cublas-cu11-11.10.3.66 nvidia-cuda-nvrtc-cu11-11.7.99 nvidia-cuda-runtime-cu11-11.7.99 nvidia-cudnn-cu11-8.5.0.96 torch-1.13.1 typing-extensions-4.4.0
You are using pip version 10.0.1, however version 22.3.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
```

Installed torchtext library ...  

```
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt# pip install torchtext
...
...
...
Requirement already satisfied: torch==1.13.1 in /root/anaconda3/lib/python3.7/site-packages (from torchtext) (1.13.1)
Requirement already satisfied: numpy in /root/anaconda3/lib/python3.7/site-packages (from torchtext) (1.15.1)
Requirement already satisfied: requests in /root/anaconda3/lib/python3.7/site-packages (from torchtext) (2.19.1)
Requirement already satisfied: tqdm in /root/anaconda3/lib/python3.7/site-packages (from torchtext) (4.26.0)
Requirement already satisfied: nvidia-cublas-cu11==11.10.3.66; platform_system == "Linux" in /root/anaconda3/lib/python3.7/site-packages (from torch==1.13.1->torchtext) (11.10.3.66)
Requirement already satisfied: typing-extensions in /root/anaconda3/lib/python3.7/site-packages (from torch==1.13.1->torchtext) (4.4.0)
Requirement already satisfied: nvidia-cudnn-cu11==8.5.0.96; platform_system == "Linux" in /root/anaconda3/lib/python3.7/site-packages (from torch==1.13.1->torchtext) (8.5.0.96)
Requirement already satisfied: nvidia-cuda-runtime-cu11==11.7.99; platform_system == "Linux" in /root/anaconda3/lib/python3.7/site-packages (from torch==1.13.1->torchtext) (11.7.99)
Requirement already satisfied: nvidia-cuda-nvrtc-cu11==11.7.99; platform_system == "Linux" in /root/anaconda3/lib/python3.7/site-packages (from torch==1.13.1->torchtext) (11.7.99)
Requirement already satisfied: chardet<3.1.0,>=3.0.2 in /root/anaconda3/lib/python3.7/site-packages (from requests->torchtext) (3.0.4)
Requirement already satisfied: urllib3<1.24,>=1.21.1 in /root/anaconda3/lib/python3.7/site-packages (from requests->torchtext) (1.23)
Requirement already satisfied: certifi>=2017.4.17 in /root/anaconda3/lib/python3.7/site-packages (from requests->torchtext) (2018.8.24)
Requirement already satisfied: idna<2.8,>=2.5 in /root/anaconda3/lib/python3.7/site-packages (from requests->torchtext) (2.7)
Requirement already satisfied: setuptools in /root/anaconda3/lib/python3.7/site-packages (from nvidia-cublas-cu11==11.10.3.66; platform_system == "Linux"->torch==1.13.1->torchtext) (40.2.0)
Requirement already satisfied: wheel in /root/anaconda3/lib/python3.7/site-packages (from nvidia-cublas-cu11==11.10.3.66; platform_system == "Linux"->torch==1.13.1->torchtext) (0.31.1)
twisted 18.7.0 requires PyHamcrest>=1.9.0, which is not installed.
Installing collected packages: torchtext
Successfully installed torchtext-0.14.1
You are using pip version 10.0.1, however version 22.3.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
```

Installed torch-optimizer ...  

```
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt# pip install torch-optimizer
Collecting torch-optimizer
  Downloading https://files.pythonhosted.org/packages/f6/54/bbb1b4c15afc2dac525c8359c340ade685542113394fd4c6564ee3c71da3/torch_optimizer-0.3.0-py3-none-any.whl (61kB)
    100% |████████████████████████████████| 71kB 2.3MB/s
Requirement already satisfied: torch>=1.5.0 in /root/anaconda3/lib/python3.7/site-packages (from torch-optimizer) (1.13.1)
Collecting pytorch-ranger>=0.1.1 (from torch-optimizer)
  Downloading https://files.pythonhosted.org/packages/0d/70/12256257d861bbc3e176130d25be1de085ce7a9e60594064888a950f2154/pytorch_ranger-0.1.1-py3-none-any.whl
Requirement already satisfied: nvidia-cublas-cu11==11.10.3.66; platform_system == "Linux" in /root/anaconda3/lib/python3.7/site-packages (from torch>=1.5.0->torch-optimizer) (11.10.3.66)
Requirement already satisfied: nvidia-cudnn-cu11==8.5.0.96; platform_system == "Linux" in /root/anaconda3/lib/python3.7/site-packages (from torch>=1.5.0->torch-optimizer) (8.5.0.96)
Requirement already satisfied: typing-extensions in /root/anaconda3/lib/python3.7/site-packages (from torch>=1.5.0->torch-optimizer) (4.4.0)
Requirement already satisfied: nvidia-cuda-nvrtc-cu11==11.7.99; platform_system == "Linux" in /root/anaconda3/lib/python3.7/site-packages (from torch>=1.5.0->torch-optimizer) (11.7.99)
Requirement already satisfied: nvidia-cuda-runtime-cu11==11.7.99; platform_system == "Linux" in /root/anaconda3/lib/python3.7/site-packages (from torch>=1.5.0->torch-optimizer) (11.7.99)
Requirement already satisfied: setuptools in /root/anaconda3/lib/python3.7/site-packages (from nvidia-cublas-cu11==11.10.3.66; platform_system == "Linux"->torch>=1.5.0->torch-optimizer) (40.2.0)
Requirement already satisfied: wheel in /root/anaconda3/lib/python3.7/site-packages (from nvidia-cublas-cu11==11.10.3.66; platform_system == "Linux"->torch>=1.5.0->torch-optimizer) (0.31.1)
twisted 18.7.0 requires PyHamcrest>=1.9.0, which is not installed.
Installing collected packages: pytorch-ranger, torch-optimizer
Successfully installed pytorch-ranger-0.1.1 torch-optimizer-0.3.0
You are using pip version 10.0.1, however version 22.3.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt#
```

Installed pytorch-ignite ...  

```
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt# pip install pytorch-ignite
Collecting pytorch-ignite
  Downloading https://files.pythonhosted.org/packages/91/92/0a0f8c3cee2d837edd7521a6102e9913263d474de075dec207a10baff1c6/pytorch_ignite-0.4.10-py3-none-any.whl (264kB)
    100% |████████████████████████████████| 266kB 5.1MB/s
Requirement already satisfied: torch<2,>=1.3 in /root/anaconda3/lib/python3.7/site-packages (from pytorch-ignite) (1.13.1)
Requirement already satisfied: packaging in /root/anaconda3/lib/python3.7/site-packages (from pytorch-ignite) (17.1)
Requirement already satisfied: nvidia-cublas-cu11==11.10.3.66; platform_system == "Linux" in /root/anaconda3/lib/python3.7/site-packages (from torch<2,>=1.3->pytorch-ignite) (11.10.3.66)
Requirement already satisfied: nvidia-cuda-nvrtc-cu11==11.7.99; platform_system == "Linux" in /root/anaconda3/lib/python3.7/site-packages (from torch<2,>=1.3->pytorch-ignite) (11.7.99)
Requirement already satisfied: nvidia-cudnn-cu11==8.5.0.96; platform_system == "Linux" in /root/anaconda3/lib/python3.7/site-packages (from torch<2,>=1.3->pytorch-ignite) (8.5.0.96)
Requirement already satisfied: nvidia-cuda-runtime-cu11==11.7.99; platform_system == "Linux" in /root/anaconda3/lib/python3.7/site-packages (from torch<2,>=1.3->pytorch-ignite) (11.7.99)
Requirement already satisfied: typing-extensions in /root/anaconda3/lib/python3.7/site-packages (from torch<2,>=1.3->pytorch-ignite) (4.4.0)
Requirement already satisfied: pyparsing>=2.0.2 in /root/anaconda3/lib/python3.7/site-packages (from packaging->pytorch-ignite) (2.2.0)
Requirement already satisfied: six in /root/anaconda3/lib/python3.7/site-packages (from packaging->pytorch-ignite) (1.11.0)
Requirement already satisfied: wheel in /root/anaconda3/lib/python3.7/site-packages (from nvidia-cublas-cu11==11.10.3.66; platform_system == "Linux"->torch<2,>=1.3->pytorch-ignite) (0.31.1)
Requirement already satisfied: setuptools in /root/anaconda3/lib/python3.7/site-packages (from nvidia-cublas-cu11==11.10.3.66; platform_system == "Linux"->torch<2,>=1.3->pytorch-ignite) (40.2.0)
twisted 18.7.0 requires PyHamcrest>=1.9.0, which is not installed.
Installing collected packages: pytorch-ignite
Successfully installed pytorch-ignite-0.4.10
You are using pip version 10.0.1, however version 22.3.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt#
```

try running train.py ...  

```
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt# python ./train.py
Traceback (most recent call last):
  File "./train.py", line 10, in <module>
    from simple_nmt.data_loader import DataLoader
  File "/home/ye/tool/simple-nmt/simple_nmt/data_loader.py", line 92, in <module>
    class TranslationDataset(data.Dataset):
AttributeError: module 'torchtext.data' has no attribute 'Dataset'
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt#
```

Do I need to install nltk?! ...  

```
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt# pip install nltk
Requirement already satisfied: nltk in /root/anaconda3/lib/python3.7/site-packages (3.3)
Requirement already satisfied: six in /root/anaconda3/lib/python3.7/site-packages (from nltk) (1.11.0)
twisted 18.7.0 requires PyHamcrest>=1.9.0, which is not installed.
You are using pip version 10.0.1, however version 22.3.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt#
```

OK, I will upgrade pip itself ...  

```
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt# pip install --upgrade pip
Collecting pip
  Downloading https://files.pythonhosted.org/packages/09/bd/2410905c76ee14c62baf69e3f4aa780226c1bbfc9485731ad018e35b0cb5/pip-22.3.1-py3-none-any.whl (2.1MB)
    100% |████████████████████████████████| 2.1MB 23.9MB/s
twisted 18.7.0 requires PyHamcrest>=1.9.0, which is not installed.
Installing collected packages: pip
  Found existing installation: pip 10.0.1
    Uninstalling pip-10.0.1:
      Successfully uninstalled pip-10.0.1
Successfully installed pip-22.3.1
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt#
```

run train.py again ...  

```
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt# python ./train.py
Traceback (most recent call last):
  File "./train.py", line 10, in <module>
    from simple_nmt.data_loader import DataLoader
  File "/home/ye/tool/simple-nmt/simple_nmt/data_loader.py", line 92, in <module>
    class TranslationDataset(data.Dataset):
AttributeError: module 'torchtext.data' has no attribute 'Dataset'
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt#
```

Install DataLoader ...  

```
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt# pip install DataLoader
Collecting DataLoader
  Downloading dataloader-2.0.tar.gz (9.1 kB)
  Preparing metadata (setup.py) ... done
Building wheels for collected packages: DataLoader
  Building wheel for DataLoader (setup.py) ... done
  Created wheel for DataLoader: filename=dataloader-2.0-py3-none-any.whl size=10106 sha256=46d60e803e1b684fe7cf2e2013737776bd957e54ca950b926f74d61678e2fae3
  Stored in directory: /root/.cache/pip/wheels/12/9e/32/45562d8d8ef30f96d5406aeb03ae2b258f644274e2e93c9f27
Successfully built DataLoader
Installing collected packages: DataLoader
Successfully installed DataLoader-2.0
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt#
```

After installed DataLoader, run train.py again ...  

```
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt# python ./train.py
Traceback (most recent call last):
  File "./train.py", line 10, in <module>
    from simple_nmt.data_loader import DataLoader
  File "/home/ye/tool/simple-nmt/simple_nmt/data_loader.py", line 92, in <module>
    class TranslationDataset(data.Dataset):
AttributeError: module 'torchtext.data' has no attribute 'Dataset'
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt#
```

I removed the comment for checking version ... (I updated that code for the 1st time running error and thus ...)  

```python
  3 import torchtext
  4 version = list(map(int, torchtext.__version__.split('.')))
  5 if version[0] <= 0 and version[1] < 9:
  6     from torchtext import data
  7 else:
  8     from torchtext.legacy import data
  9
 10 #from torchtext import data
```

After updating the python code as shown in above, I run train.py again and for this time got following new error:  

```
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt# python ./train.py -h
Traceback (most recent call last):
  File "./train.py", line 10, in <module>
    from simple_nmt.data_loader import DataLoader
  File "/home/ye/tool/simple-nmt/simple_nmt/data_loader.py", line 8, in <module>
    from torchtext.legacy import data
ModuleNotFoundError: No module named 'torchtext.legacy'
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt#
```

I updated the code as follows:  

```
if version[0] <= 0 and version[1] < 9:
    from torchtext import data
else:
    #from torchtext.legacy import data
    from torchtext import data, datasets
```

run python code again ...  

```
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt# python ./train.py -h
Traceback (most recent call last):
  File "./train.py", line 10, in <module>
    from simple_nmt.data_loader import DataLoader
  File "/home/ye/tool/simple-nmt/simple_nmt/data_loader.py", line 93, in <module>
    class TranslationDataset(data.Dataset):
AttributeError: module 'torchtext.data' has no attribute 'Dataset'
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt#
```

I will downgrade the torchtext version ...  

```
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt# pip install torchtext==0.10.0
...
...
...
Collecting torchtext==0.10.0
  Downloading torchtext-0.10.0-cp37-cp37m-manylinux1_x86_64.whl (7.6 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 7.6/7.6 MB 2.3 MB/s eta 0:00:00
Requirement already satisfied: numpy in /root/anaconda3/lib/python3.7/site-packages (from torchtext==0.10.0) (1.15.1)
Collecting torch==1.9.0
  Downloading torch-1.9.0-cp37-cp37m-manylinux1_x86_64.whl (831.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 831.4/831.4 MB 9.2 MB/s eta 0:00:00
Requirement already satisfied: requests in /root/anaconda3/lib/python3.7/site-packages (from torchtext==0.10.0) (2.19.1)
Requirement already satisfied: tqdm in /root/anaconda3/lib/python3.7/site-packages (from torchtext==0.10.0) (4.26.0)
Requirement already satisfied: typing-extensions in /root/anaconda3/lib/python3.7/site-packages (from torch==1.9.0->torchtext==0.10.0) (4.4.0)
Requirement already satisfied: certifi>=2017.4.17 in /root/anaconda3/lib/python3.7/site-packages (from requests->torchtext==0.10.0) (2018.8.24)
Requirement already satisfied: urllib3<1.24,>=1.21.1 in /root/anaconda3/lib/python3.7/site-packages (from requests->torchtext==0.10.0) (1.23)
Requirement already satisfied: chardet<3.1.0,>=3.0.2 in /root/anaconda3/lib/python3.7/site-packages (from requests->torchtext==0.10.0) (3.0.4)
Requirement already satisfied: idna<2.8,>=2.5 in /root/anaconda3/lib/python3.7/site-packages (from requests->torchtext==0.10.0) (2.7)
Installing collected packages: torch, torchtext
  Attempting uninstall: torch
    Found existing installation: torch 1.13.1
    Uninstalling torch-1.13.1:
      Successfully uninstalled torch-1.13.1
  Attempting uninstall: torchtext
    Found existing installation: torchtext 0.14.1
    Uninstalling torchtext-0.14.1:
      Successfully uninstalled torchtext-0.14.1
Successfully installed torch-1.9.0 torchtext-0.10.0
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
```

run python code again ...  Do Hope OK! ...  

```
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt# python ./train.py -h
Traceback (most recent call last):
  File "./train.py", line 10, in <module>
    from simple_nmt.data_loader import DataLoader
  File "/home/ye/tool/simple-nmt/simple_nmt/data_loader.py", line 93, in <module>
    class TranslationDataset(data.Dataset):
AttributeError: module 'torchtext.data' has no attribute 'Dataset'
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt#
```

Yes I need to change the source code also ...  

```
if version[0] <= 0 and version[1] < 9:
    from torchtext import data
else:
    from torchtext.legacy import data
    #from torchtext import data, datasets
```

Run train.py again ...  

```
(simple-nmt) root@69b2889746d7:/home/ye/tool/simple-nmt# python ./train.py -h
...
...
...
  --max_grad_norm MAX_GRAD_NORM
                        Threshold for gradient clipping. Default=5.0
  --iteration_per_update ITERATION_PER_UPDATE
                        Number of feed-forward iterations for one parameter
                        update. Default=1
  --lr LR               Initial learning rate. Default=1.0
  --lr_step LR_STEP     Number of epochs for each learning rate decay.
                        Default=1
  --lr_gamma LR_GAMMA   Learning rate decay rate. Default=0.5
  --lr_decay_start LR_DECAY_START
                        Learning rate decay start at. Default=10
  --use_adam            Use Adam as optimizer instead of SGD. Other lr
                        arguments should be changed.
  --use_radam           Use rectified Adam as optimizer. Other lr arguments
                        should be changed.
  --rl_lr RL_LR         Learning rate for reinforcement learning. Default=0.01
  --rl_n_samples RL_N_SAMPLES
                        Number of samples to get baseline. Default=1
  --rl_n_epochs RL_N_EPOCHS
                        Number of epochs for reinforcement learning.
                        Default=10
  --rl_n_gram RL_N_GRAM
                        Maximum number of tokens to calculate BLEU for
                        reinforcement learning. Default=6
  --rl_reward RL_REWARD
                        Method name to use as reward function for RL training.
                        Default=gleu
  --use_transformer     Set model architecture as Transformer.
  --n_splits N_SPLITS   Number of heads in multi-head attention in
                        Transformer. Default=8

```

```
root@341956fcb949:/home/ye/tool/simple-nmt# python train.py
/root/anaconda3/lib/python3.7/site-packages/sklearn/feature_extraction/text.py:17: DeprecationWarning: Using or importing the ABCs from 'collections' instead of from 'collections.abc' is deprecated, and in 3.8 it will stop working
  from collections import Mapping, defaultdict
usage: train.py [-h] --model_fn MODEL_FN --train TRAIN --valid VALID --lang
                LANG [--gpu_id GPU_ID] [--off_autocast]
                [--batch_size BATCH_SIZE] [--n_epochs N_EPOCHS]
                [--verbose VERBOSE] [--init_epoch INIT_EPOCH]
                [--max_length MAX_LENGTH] [--dropout DROPOUT]
                [--word_vec_size WORD_VEC_SIZE] [--hidden_size HIDDEN_SIZE]
                [--n_layers N_LAYERS] [--max_grad_norm MAX_GRAD_NORM]
                [--iteration_per_update ITERATION_PER_UPDATE] [--lr LR]
                [--lr_step LR_STEP] [--lr_gamma LR_GAMMA]
                [--lr_decay_start LR_DECAY_START] [--use_adam] [--use_radam]
                [--rl_lr RL_LR] [--rl_n_samples RL_N_SAMPLES]
                [--rl_n_epochs RL_N_EPOCHS] [--rl_n_gram RL_N_GRAM]
                [--rl_reward RL_REWARD] [--use_transformer]
                [--n_splits N_SPLITS]
train.py: error: the following arguments are required: --model_fn, --train, --valid, --lang
root@341956fcb949:/home/ye/tool/simple-nmt#
```

## Commit the Current Container Environment for Future Usages

```
ye@lst-gpu-3090:~$ sudo docker ps -a | head
CONTAINER ID   IMAGE                                    COMMAND                  CREATED         STATUS                      PORTS                                       NAMES
341956fcb949   ye_conda                                 "/bin/bash"              3 minutes ago   Exited (2) 11 seconds ago                                               loving_almeida
0d441b235700   ye_conda                                 "/bin/bash"              4 days ago      Up 4 days                                                               nice_yalow
36ae92f960d5   ye_conda                                 "/bin/bash"              4 days ago      Up 4 days                                                               hardcore_clarke
56c7c2fbf383   tgowda/rtg-model:600toEng-v2.0           "/bin/sh -c 'uwsgi -…"   8 days ago      Up 8 days                   0.0.0.0:6060->6060/tcp, :::6060->6060/tcp   frosty_lumiere
5d94c7834a47   ye_conda                                 "/bin/bash"              10 days ago     Up 10 days                                                              nervous_shirley
4476a2a898d1   ye_marian                                "/bin/bash"              3 weeks ago     Created                                                                 admiring_faraday
4a41a9061b50   ye_marian                                "/bin/bash"              3 weeks ago     Created                                                                 trusting_ishizaka
ab54cf38cc53   nvidia/cuda:11.5.2-base-ubuntu20.04      "nvidia-smi"             7 weeks ago     Exited (0) 7 weeks ago                                                  vigilant_knuth
195c8c6864b4   peerachet_cuda_image                     "/bin/bash"              2 months ago    Exited (137) 7 weeks ago                                                peerachet_machine
ye@lst-gpu-3090:~$
```

Commit Changes to Image and give the new name "ye_simple" ...  

```
ye@lst-gpu-3090:~$ sudo docker commit 341956fcb949 ye_simple
sha256:a77e96fff51fc5f9a7450f1775ccd9aaadd3fcccd6779467881e2692629f6b0e
ye@lst-gpu-3090:~$
```

Check the docker images and find "ye_simple" image and I found as follows:  

```
ye@lst-gpu-3090:~$ sudo docker images
REPOSITORY             TAG                          IMAGE ID       CREATED         SIZE
ye_simple              latest                       a77e96fff51f   2 minutes ago   21GB
peerachet_cuda_image   latest                       2edb58a4de97   2 months ago    4.86GB
demo_image             latest                       50cafb379077   2 months ago    20.5GB
<none>                 <none>                       eeedbfa8fd48   2 months ago    18.5GB
ye_conda               latest                       b17c659462c6   2 months ago    18.3GB
ye_marian              latest                       2d6589b91c5e   2 months ago    15GB
<none>                 <none>                       9a48ab016bc3   2 months ago    15GB
nvidia/cuda            11.8.0-runtime-ubuntu22.04   8f435f3366df   2 months ago    2.38GB
nvidia/cuda            11.8.0-base-ubuntu22.04      87e1b9a6df85   2 months ago    239MB
nvidia/cuda            11.7.0-devel-ubuntu22.04     bdb394791d83   4 months ago    4.86GB
nvidia/cuda            11.5.2-base-ubuntu20.04      20e5014a14c9   7 months ago    153MB
tgowda/rtg-model       600toEng-v2.0                70954713b8a4   9 months ago    8.53GB
nvidia/cuda            11.4.0-devel-centos8         bb61b346cd33   11 months ago   5.23GB
ye@lst-gpu-3090:~$
```

I updated the login shell script:  

```
#!/bin/bash

sudo docker start ye_conda
#sudo docker run -it --gpus 1 -v /home/ye:/home/ye ye_marian /bin/bash -c "nvidia-smi; cd home/ye/; pwd"
#sudo docker run --rm -it --gpus 1 -v /home/ye:/home/ye ye_marian /bin/bash
sudo docker run -it --gpus 1 -v /home/ye:/home/ye ye_simple /bin/bash
```

Entering to the new container env again:  

```
ye@lst-gpu-3090:~$ ./start-ye_conda.sh
ye_conda
root@822ee7bdb9c8:/#
```

Check the prepared Anaconda environment for running simple-nmt:  

```
root@822ee7bdb9c8:/# conda info --envs
# conda environments:
#
base                  *  /root/anaconda3
simple-nmt               /root/anaconda3/envs/simple-nmt

root@822ee7bdb9c8:/#
```

It looks everythings OK!  

## Prepare data

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
