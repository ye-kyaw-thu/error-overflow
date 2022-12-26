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
