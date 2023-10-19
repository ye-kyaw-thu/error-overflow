# Myanmar HateSpeech GPT2 Experiment 1

## Create New Python Env

```
(base) yekyaw.thu@gpu:~/tool$ conda create --name nanoGPT python=3.8
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 23.9.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/nanoGPT

  added / updated specs:
    - python=3.8


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    ca-certificates-2023.08.22 |       h06a4308_0         123 KB
    libffi-3.4.4               |       h6a678d5_0         142 KB
    openssl-3.0.11             |       h7f8727e_2         5.2 MB
    pip-23.3                   |   py38h06a4308_0         2.6 MB
    python-3.8.18              |       h955ad1f_0        25.3 MB
    setuptools-68.0.0          |   py38h06a4308_0         927 KB
    sqlite-3.41.2              |       h5eee18b_0         1.2 MB
    wheel-0.41.2               |   py38h06a4308_0         108 KB
    xz-5.4.2                   |       h5eee18b_0         642 KB
    ------------------------------------------------------------
                                           Total:        36.1 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-5.1-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2023.08.22-h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.38-h1181459_1
  libffi             pkgs/main/linux-64::libffi-3.4.4-h6a678d5_0
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-11.2.0-h1234567_1
  libgomp            pkgs/main/linux-64::libgomp-11.2.0-h1234567_1
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-11.2.0-h1234567_1
  ncurses            pkgs/main/linux-64::ncurses-6.4-h6a678d5_0
  openssl            pkgs/main/linux-64::openssl-3.0.11-h7f8727e_2
  pip                pkgs/main/linux-64::pip-23.3-py38h06a4308_0
  python             pkgs/main/linux-64::python-3.8.18-h955ad1f_0
  readline           pkgs/main/linux-64::readline-8.2-h5eee18b_0
  setuptools         pkgs/main/linux-64::setuptools-68.0.0-py38h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.41.2-h5eee18b_0
  tk                 pkgs/main/linux-64::tk-8.6.12-h1ccaba5_0
  wheel              pkgs/main/linux-64::wheel-0.41.2-py38h06a4308_0
  xz                 pkgs/main/linux-64::xz-5.4.2-h5eee18b_0
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
ca-certificates-2023 | 123 KB    | ############################################### | 100%
setuptools-68.0.0    | 927 KB    | ############################################### | 100%
xz-5.4.2             | 642 KB    | ############################################### | 100%
python-3.8.18        | 25.3 MB   | ############################################### | 100%
pip-23.3             | 2.6 MB    | ############################################### | 100%
wheel-0.41.2         | 108 KB    | ############################################### | 100%
libffi-3.4.4         | 142 KB    | ############################################### | 100%
openssl-3.0.11       | 5.2 MB    | ############################################### | 100%
sqlite-3.41.2        | 1.2 MB    | ############################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate nanoGPT
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```

Activate the nanoGPT Anaconda environment ...  

```
(base) yekyaw.thu@gpu:~/tool$ conda activate nanoGPT
(nanoGPT) yekyaw.thu@gpu:~/tool$
```

## Installation of Python Libraries

Reference link: [https://github.com/karpathy/nanoGPT](https://github.com/karpathy/nanoGPT)  

```
(nanoGPT) yekyaw.thu@gpu:~$ pip install torch numpy transformers datasets tiktoken wandb tqdm
Collecting torch
  Downloading torch-2.1.0-cp38-cp38-manylinux1_x86_64.whl.metadata (25 kB)
Requirement already satisfied: numpy in ./.local/lib/python3.8/site-packages (1.24.1)
Collecting transformers
  Downloading transformers-4.34.1-py3-none-any.whl.metadata (121 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 121.5/121.5 kB 952.3 kB/s eta 0:00:00
Collecting datasets
  Downloading datasets-2.14.5-py3-none-any.whl.metadata (19 kB)
Collecting tiktoken
  Downloading tiktoken-0.5.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (6.6 kB)
Collecting wandb
  Downloading wandb-0.15.12-py3-none-any.whl.metadata (9.8 kB)
Collecting tqdm
  Downloading tqdm-4.66.1-py3-none-any.whl.metadata (57 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 57.6/57.6 kB 557.5 kB/s eta 0:00:00
Collecting filelock (from torch)
  Downloading filelock-3.12.4-py3-none-any.whl.metadata (2.8 kB)
Requirement already satisfied: typing-extensions in ./.local/lib/python3.8/site-packages (from torch) (4.4.0)
Collecting sympy (from torch)
  Downloading sympy-1.12-py3-none-any.whl (5.7 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 5.7/5.7 MB 15.6 MB/s eta 0:00:00
Collecting networkx (from torch)
  Downloading networkx-3.1-py3-none-any.whl (2.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.1/2.1 MB 10.5 MB/s eta 0:00:00
Collecting jinja2 (from torch)
  Downloading Jinja2-3.1.2-py3-none-any.whl (133 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 133.1/133.1 kB 1.3 MB/s eta 0:00:00
Collecting fsspec (from torch)
  Downloading fsspec-2023.9.2-py3-none-any.whl.metadata (6.7 kB)
Collecting nvidia-cuda-nvrtc-cu12==12.1.105 (from torch)
  Downloading nvidia_cuda_nvrtc_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (23.7 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 23.7/23.7 MB 10.8 MB/s eta 0:00:00
Collecting nvidia-cuda-runtime-cu12==12.1.105 (from torch)
  Downloading nvidia_cuda_runtime_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (823 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 823.6/823.6 kB 4.9 MB/s eta 0:00:00
Collecting nvidia-cuda-cupti-cu12==12.1.105 (from torch)
  Downloading nvidia_cuda_cupti_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (14.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 14.1/14.1 MB 11.6 MB/s eta 0:00:00
Collecting nvidia-cudnn-cu12==8.9.2.26 (from torch)
  Downloading nvidia_cudnn_cu12-8.9.2.26-py3-none-manylinux1_x86_64.whl.metadata (1.6 kB)
Collecting nvidia-cublas-cu12==12.1.3.1 (from torch)
  Downloading nvidia_cublas_cu12-12.1.3.1-py3-none-manylinux1_x86_64.whl (410.6 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 410.6/410.6 MB 2.5 MB/s eta 0:00:00
Collecting nvidia-cufft-cu12==11.0.2.54 (from torch)
  Downloading nvidia_cufft_cu12-11.0.2.54-py3-none-manylinux1_x86_64.whl (121.6 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 121.6/121.6 MB 6.7 MB/s eta 0:00:00
Collecting nvidia-curand-cu12==10.3.2.106 (from torch)
  Downloading nvidia_curand_cu12-10.3.2.106-py3-none-manylinux1_x86_64.whl (56.5 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 56.5/56.5 MB 3.0 MB/s eta 0:00:00
Collecting nvidia-cusolver-cu12==11.4.5.107 (from torch)
  Downloading nvidia_cusolver_cu12-11.4.5.107-py3-none-manylinux1_x86_64.whl (124.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 124.2/124.2 MB 2.4 MB/s eta 0:00:00
Collecting nvidia-cusparse-cu12==12.1.0.106 (from torch)
  Downloading nvidia_cusparse_cu12-12.1.0.106-py3-none-manylinux1_x86_64.whl (196.0 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 196.0/196.0 MB 3.6 MB/s eta 0:00:00
Collecting nvidia-nccl-cu12==2.18.1 (from torch)
  Downloading nvidia_nccl_cu12-2.18.1-py3-none-manylinux1_x86_64.whl (209.8 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 209.8/209.8 MB 3.3 MB/s eta 0:00:00
Collecting nvidia-nvtx-cu12==12.1.105 (from torch)
  Downloading nvidia_nvtx_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (99 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 99.1/99.1 kB 1.4 MB/s eta 0:00:00
Collecting triton==2.1.0 (from torch)
  Downloading triton-2.1.0-0-cp38-cp38-manylinux2014_x86_64.manylinux_2_17_x86_64.whl.metadata (1.3 kB)
Collecting nvidia-nvjitlink-cu12 (from nvidia-cusolver-cu12==11.4.5.107->torch)
  Downloading nvidia_nvjitlink_cu12-12.2.140-py3-none-manylinux1_x86_64.whl.metadata (1.5 kB)
Collecting huggingface-hub<1.0,>=0.16.4 (from transformers)
  Downloading huggingface_hub-0.18.0-py3-none-any.whl.metadata (13 kB)
Requirement already satisfied: packaging>=20.0 in ./.local/lib/python3.8/site-packages (from transformers) (23.0)
Collecting pyyaml>=5.1 (from transformers)
  Downloading PyYAML-6.0.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (2.1 kB)
Collecting regex!=2019.12.17 (from transformers)
  Downloading regex-2023.10.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (40 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 40.9/40.9 kB 447.6 kB/s eta 0:00:00
Collecting requests (from transformers)
  Downloading requests-2.31.0-py3-none-any.whl.metadata (4.6 kB)
Collecting tokenizers<0.15,>=0.14 (from transformers)
  Downloading tokenizers-0.14.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (6.7 kB)
Collecting safetensors>=0.3.1 (from transformers)
  Downloading safetensors-0.4.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (3.8 kB)
Collecting pyarrow>=8.0.0 (from datasets)
  Downloading pyarrow-13.0.0-cp38-cp38-manylinux_2_28_x86_64.whl.metadata (3.0 kB)
Collecting dill<0.3.8,>=0.3.0 (from datasets)
  Downloading dill-0.3.7-py3-none-any.whl.metadata (9.9 kB)
Collecting pandas (from datasets)
  Downloading pandas-2.0.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (18 kB)
Collecting xxhash (from datasets)
  Downloading xxhash-3.4.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (12 kB)
Collecting multiprocess (from datasets)
  Downloading multiprocess-0.70.15-py38-none-any.whl.metadata (7.1 kB)
Collecting fsspec (from torch)
  Downloading fsspec-2023.6.0-py3-none-any.whl.metadata (6.7 kB)
Collecting aiohttp (from datasets)
  Downloading aiohttp-3.8.6-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (7.7 kB)
Collecting Click!=8.0.0,>=7.1 (from wandb)
  Downloading click-8.1.7-py3-none-any.whl.metadata (3.0 kB)
Collecting GitPython!=3.1.29,>=1.0.0 (from wandb)
  Downloading GitPython-3.1.40-py3-none-any.whl.metadata (12 kB)
Collecting psutil>=5.0.0 (from wandb)
  Downloading psutil-5.9.6-cp36-abi3-manylinux_2_12_x86_64.manylinux2010_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (21 kB)
Collecting sentry-sdk>=1.0.0 (from wandb)
  Downloading sentry_sdk-1.32.0-py2.py3-none-any.whl.metadata (9.8 kB)
Collecting docker-pycreds>=0.4.0 (from wandb)
  Downloading docker_pycreds-0.4.0-py2.py3-none-any.whl (9.0 kB)
Collecting pathtools (from wandb)
  Downloading pathtools-0.1.2.tar.gz (11 kB)
  Preparing metadata (setup.py) ... done
Collecting setproctitle (from wandb)
  Downloading setproctitle-1.3.3-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (9.9 kB)
Requirement already satisfied: setuptools in ./.conda/envs/nanoGPT/lib/python3.8/site-packages (from wandb) (68.0.0)
Collecting appdirs>=1.4.3 (from wandb)
  Downloading appdirs-1.4.4-py2.py3-none-any.whl (9.6 kB)
Requirement already satisfied: protobuf!=4.21.0,<5,>=3.12.0 in ./.local/lib/python3.8/site-packages (from wandb) (3.19.6)
Collecting six>=1.4.0 (from docker-pycreds>=0.4.0->wandb)
  Downloading six-1.16.0-py2.py3-none-any.whl (11 kB)
Collecting attrs>=17.3.0 (from aiohttp->datasets)
  Downloading attrs-23.1.0-py3-none-any.whl (61 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 61.2/61.2 kB 444.2 kB/s eta 0:00:00
Collecting charset-normalizer<4.0,>=2.0 (from aiohttp->datasets)
  Downloading charset_normalizer-3.3.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (32 kB)
Collecting multidict<7.0,>=4.5 (from aiohttp->datasets)
  Downloading multidict-6.0.4-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (121 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 121.3/121.3 kB 1.1 MB/s eta 0:00:00
Collecting async-timeout<5.0,>=4.0.0a3 (from aiohttp->datasets)
  Downloading async_timeout-4.0.3-py3-none-any.whl.metadata (4.2 kB)
Collecting yarl<2.0,>=1.0 (from aiohttp->datasets)
  Downloading yarl-1.9.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (266 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 266.9/266.9 kB 1.8 MB/s eta 0:00:00
Collecting frozenlist>=1.1.1 (from aiohttp->datasets)
  Downloading frozenlist-1.4.0-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (5.2 kB)
Collecting aiosignal>=1.1.2 (from aiohttp->datasets)
  Downloading aiosignal-1.3.1-py3-none-any.whl (7.6 kB)
Collecting gitdb<5,>=4.0.1 (from GitPython!=3.1.29,>=1.0.0->wandb)
  Downloading gitdb-4.0.10-py3-none-any.whl (62 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 62.7/62.7 kB 486.1 kB/s eta 0:00:00
Collecting idna<4,>=2.5 (from requests->transformers)
  Downloading idna-3.4-py3-none-any.whl (61 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 61.5/61.5 kB 420.2 kB/s eta 0:00:00
Collecting urllib3<3,>=1.21.1 (from requests->transformers)
  Downloading urllib3-2.0.7-py3-none-any.whl.metadata (6.6 kB)
Collecting certifi>=2017.4.17 (from requests->transformers)
  Downloading certifi-2023.7.22-py3-none-any.whl.metadata (2.2 kB)
Collecting huggingface-hub<1.0,>=0.16.4 (from transformers)
  Downloading huggingface_hub-0.17.3-py3-none-any.whl.metadata (13 kB)
Requirement already satisfied: MarkupSafe>=2.0 in ./.local/lib/python3.8/site-packages (from jinja2->torch) (2.1.1)
Requirement already satisfied: python-dateutil>=2.8.2 in ./.local/lib/python3.8/site-packages (from pandas->datasets) (2.8.2)
Requirement already satisfied: pytz>=2020.1 in ./.local/lib/python3.8/site-packages (from pandas->datasets) (2022.7.1)
Collecting tzdata>=2022.1 (from pandas->datasets)
  Downloading tzdata-2023.3-py2.py3-none-any.whl (341 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 341.8/341.8 kB 2.1 MB/s eta 0:00:00
Collecting mpmath>=0.19 (from sympy->torch)
  Downloading mpmath-1.3.0-py3-none-any.whl (536 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 536.2/536.2 kB 2.4 MB/s eta 0:00:00
Collecting smmap<6,>=3.0.1 (from gitdb<5,>=4.0.1->GitPython!=3.1.29,>=1.0.0->wandb)
  Downloading smmap-5.0.1-py3-none-any.whl.metadata (4.3 kB)
Downloading torch-2.1.0-cp38-cp38-manylinux1_x86_64.whl (670.2 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 670.2/670.2 MB 1.5 MB/s eta 0:00:00
Downloading nvidia_cudnn_cu12-8.9.2.26-py3-none-manylinux1_x86_64.whl (731.7 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 731.7/731.7 MB 1.1 MB/s eta 0:00:00
Downloading triton-2.1.0-0-cp38-cp38-manylinux2014_x86_64.manylinux_2_17_x86_64.whl (89.2 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 89.2/89.2 MB 1.6 MB/s eta 0:00:00
Downloading transformers-4.34.1-py3-none-any.whl (7.7 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 7.7/7.7 MB 2.0 MB/s eta 0:00:00
Downloading datasets-2.14.5-py3-none-any.whl (519 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 519.6/519.6 kB 1.4 MB/s eta 0:00:00
Downloading tiktoken-0.5.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (2.0 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.0/2.0 MB 1.5 MB/s eta 0:00:00
Downloading wandb-0.15.12-py3-none-any.whl (2.1 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.1/2.1 MB 1.8 MB/s eta 0:00:00
Downloading tqdm-4.66.1-py3-none-any.whl (78 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 78.3/78.3 kB 718.7 kB/s eta 0:00:00
Downloading click-8.1.7-py3-none-any.whl (97 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 97.9/97.9 kB 822.3 kB/s eta 0:00:00
Downloading dill-0.3.7-py3-none-any.whl (115 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 115.3/115.3 kB 741.1 kB/s eta 0:00:00
Downloading fsspec-2023.6.0-py3-none-any.whl (163 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 163.8/163.8 kB 868.0 kB/s eta 0:00:00
Downloading aiohttp-3.8.6-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.1 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.1/1.1 MB 1.3 MB/s eta 0:00:00
Downloading GitPython-3.1.40-py3-none-any.whl (190 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 190.6/190.6 kB 804.4 kB/s eta 0:00:00
Downloading psutil-5.9.6-cp36-abi3-manylinux_2_12_x86_64.manylinux2010_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (283 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 283.6/283.6 kB 831.9 kB/s eta 0:00:00
Downloading pyarrow-13.0.0-cp38-cp38-manylinux_2_28_x86_64.whl (40.1 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 40.1/40.1 MB 3.6 MB/s eta 0:00:00
Downloading PyYAML-6.0.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (736 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 736.6/736.6 kB 3.7 MB/s eta 0:00:00
Downloading regex-2023.10.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (776 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 777.0/777.0 kB 3.8 MB/s eta 0:00:00
Downloading requests-2.31.0-py3-none-any.whl (62 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 62.6/62.6 kB 909.5 kB/s eta 0:00:00
Downloading safetensors-0.4.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.3 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.3/1.3 MB 4.3 MB/s eta 0:00:00
Downloading sentry_sdk-1.32.0-py2.py3-none-any.whl (240 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 241.0/241.0 kB 2.4 MB/s eta 0:00:00
Downloading tokenizers-0.14.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.8 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.8/3.8 MB 4.7 MB/s eta 0:00:00
Downloading huggingface_hub-0.17.3-py3-none-any.whl (295 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 295.0/295.0 kB 2.2 MB/s eta 0:00:00
Downloading filelock-3.12.4-py3-none-any.whl (11 kB)
Downloading multiprocess-0.70.15-py38-none-any.whl (132 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 132.6/132.6 kB 1.4 MB/s eta 0:00:00
Downloading pandas-2.0.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (12.4 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 12.4/12.4 MB 3.4 MB/s eta 0:00:00
Downloading setproctitle-1.3.3-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (31 kB)
Downloading xxhash-3.4.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (194 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 194.6/194.6 kB 1.7 MB/s eta 0:00:00
Downloading async_timeout-4.0.3-py3-none-any.whl (5.7 kB)
Downloading certifi-2023.7.22-py3-none-any.whl (158 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 158.3/158.3 kB 1.5 MB/s eta 0:00:00
Downloading charset_normalizer-3.3.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (137 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 137.9/137.9 kB 1.3 MB/s eta 0:00:00
Downloading frozenlist-1.4.0-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (220 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 220.1/220.1 kB 1.7 MB/s eta 0:00:00
Downloading urllib3-2.0.7-py3-none-any.whl (124 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 124.2/124.2 kB 1.2 MB/s eta 0:00:00
Downloading nvidia_nvjitlink_cu12-12.2.140-py3-none-manylinux1_x86_64.whl (20.2 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 20.2/20.2 MB 2.2 MB/s eta 0:00:00
Downloading smmap-5.0.1-py3-none-any.whl (24 kB)
Building wheels for collected packages: pathtools
  Building wheel for pathtools (setup.py) ... done
  Created wheel for pathtools: filename=pathtools-0.1.2-py3-none-any.whl size=8791 sha256=433fdcc1b9ee670b782e345a687e53c933744c3704103e9830e7181aef53dfff
  Stored in directory: /home/yekyaw.thu/.cache/pip/wheels/4c/8e/7e/72fbc243e1aeecae64a96875432e70d4e92f3d2d18123be004
Successfully built pathtools
Installing collected packages: pathtools, mpmath, appdirs, xxhash, urllib3, tzdata, tqdm, sympy, smmap, six, setproctitle, safetensors, regex, pyyaml, pyarrow, psutil, nvidia-nvtx-cu12, nvidia-nvjitlink-cu12, nvidia-nccl-cu12, nvidia-curand-cu12, nvidia-cufft-cu12, nvidia-cuda-runtime-cu12, nvidia-cuda-nvrtc-cu12, nvidia-cuda-cupti-cu12, nvidia-cublas-cu12, networkx, multidict, jinja2, idna, fsspec, frozenlist, filelock, dill, Click, charset-normalizer, certifi, attrs, async-timeout, yarl, triton, sentry-sdk, requests, nvidia-cusparse-cu12, nvidia-cudnn-cu12, multiprocess, gitdb, docker-pycreds, aiosignal, tiktoken, pandas, nvidia-cusolver-cu12, huggingface-hub, GitPython, aiohttp, wandb, torch, tokenizers, transformers, datasets
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
google-auth 2.16.0 requires pyasn1-modules>=0.2.1, which is not installed.
requests-oauthlib 1.3.1 requires oauthlib>=3.0.0, which is not installed.
Successfully installed Click-8.1.7 GitPython-3.1.40 aiohttp-3.8.6 aiosignal-1.3.1 appdirs-1.4.4 async-timeout-4.0.3 attrs-23.1.0 certifi-2023.7.22 charset-normalizer-3.3.0 datasets-2.14.5 dill-0.3.7 docker-pycreds-0.4.0 filelock-3.12.4 frozenlist-1.4.0 fsspec-2023.6.0 gitdb-4.0.10 huggingface-hub-0.17.3 idna-3.4 jinja2-3.1.2 mpmath-1.3.0 multidict-6.0.4 multiprocess-0.70.15 networkx-3.1 nvidia-cublas-cu12-12.1.3.1 nvidia-cuda-cupti-cu12-12.1.105 nvidia-cuda-nvrtc-cu12-12.1.105 nvidia-cuda-runtime-cu12-12.1.105 nvidia-cudnn-cu12-8.9.2.26 nvidia-cufft-cu12-11.0.2.54 nvidia-curand-cu12-10.3.2.106 nvidia-cusolver-cu12-11.4.5.107 nvidia-cusparse-cu12-12.1.0.106 nvidia-nccl-cu12-2.18.1 nvidia-nvjitlink-cu12-12.2.140 nvidia-nvtx-cu12-12.1.105 pandas-2.0.3 pathtools-0.1.2 psutil-5.9.6 pyarrow-13.0.0 pyyaml-6.0.1 regex-2023.10.3 requests-2.31.0 safetensors-0.4.0 sentry-sdk-1.32.0 setproctitle-1.3.3 six-1.16.0 smmap-5.0.1 sympy-1.12 tiktoken-0.5.1 tokenizers-0.14.1 torch-2.1.0 tqdm-4.66.1 transformers-4.34.1 triton-2.1.0 tzdata-2023.3 urllib3-2.0.7 wandb-0.15.12 xxhash-3.4.1 yarl-1.9.2
(nanoGPT) yekyaw.thu@gpu:~$
```

## Cloning nanoGPT Repository 

GPT2 model training source code တွေကို ကိုယ့်စက်ထဲကို clone လုပ်ခဲ့ ...  

```
(nanoGPT) yekyaw.thu@gpu:~/tool$ git clone https://github.com/karpathy/nanoGPT
Cloning into 'nanoGPT'...
remote: Enumerating objects: 649, done.
remote: Total 649 (delta 0), reused 0 (delta 0), pack-reused 649
Receiving objects: 100% (649/649), 936.46 KiB | 3.32 MiB/s, done.
Resolving deltas: 100% (371/371), done.
(nanoGPT) yekyaw.thu@gpu:~/tool$ cd nanoGPT/
(nanoGPT) yekyaw.thu@gpu:~/tool/nanoGPT$ ls
assets    configurator.py  model.py   scaling_laws.ipynb
bench.py  data             README.md  train.py
config    LICENSE          sample.py  transformer_sizing.ipynb
(nanoGPT) yekyaw.thu@gpu:~/tool/nanoGPT$
```

## Cloning myPoetry Repository

အထက်ပါ nanoGPT repository ကို အခြေခံပြီးတော့ မြန်မာကဗျာအတွက် စမ်းထားတဲ့ repository ကိုလည်း ကိုယ့်လက်ရှိ run မယ့် server စက်ထဲကို clone လုပ်ခဲ့။ ဒီ ထဲမှာက မြန်မာစာကို run ဖို့အတွက် ရှေ့မှာ သုံးထားတဲ့ preprocessing code လည်း ရှိနေတာမို့လို့ ...  

```
(nanoGPT) yekyaw.thu@gpu:~/exp$ git clone https://github.com/ye-kyaw-thu/myPoetry
Cloning into 'myPoetry'...
remote: Enumerating objects: 188, done.
remote: Counting objects: 100% (74/74), done.
remote: Compressing objects: 100% (71/71), done.
remote: Total 188 (delta 20), reused 0 (delta 0), pack-reused 114
Receiving objects: 100% (188/188), 3.58 MiB | 12.64 MiB/s, done.
Resolving deltas: 100% (52/52), done.
(nanoGPT) yekyaw.thu@gpu:~/exp$
```

## Recalling myPoetry Experiment

myPoetry Link: [https://github.com/ye-kyaw-thu/myPoetry](https://github.com/ye-kyaw-thu/myPoetry)  
အရင် လုပ်ထားခဲ့တဲ့ myPoetry experiment နဲ့ ပတ်သက်ပြီး ပြန်စဉ်းစား၊ ဟိုဖိုင် ဝင်ကြည့်၊ ဒီဖိုင် ဝင်ကြည့် ... ဘာတွေ လုပ်ခဲ့တာလည်း ဆိုတာကို ပြန်နွှေး ...  

```
(nanoGPT) yekyaw.thu@gpu:~/exp$ cd myPoetry
(nanoGPT) yekyaw.thu@gpu:~/exp/myPoetry$ ls
corpus  notebooks  README.md
(nanoGPT) yekyaw.thu@gpu:~/exp/myPoetry$ cd corpus
(nanoGPT) yekyaw.thu@gpu:~/exp/myPoetry/corpus$ ls
version1.0
(nanoGPT) yekyaw.thu@gpu:~/exp/myPoetry/corpus$ cd version1.0/
(nanoGPT) yekyaw.thu@gpu:~/exp/myPoetry/corpus/version1.0$ ls
doc  mypoetry-corpus-notitle-ver1.0.txt  mypoetry-corpus-ver1.0.txt
(nanoGPT) yekyaw.thu@gpu:~/exp/myPoetry/corpus/version1.0$ head mypoetry-corpus-notitle-ver1.0.txt
ကြက်ဖ သာလျှင်
အာရုဏ်ရောင်လှ ၊ ဝင်းဝါကြ၏ ။
ဥဩ သာလျှင်
ရာသီနွေလ ၊ ဖူးပွင့်ကြ၏ ။
ဖားငယ် သာလျှင်
အာကာမိုးက ၊ မိုးရွာကြ၏ ။
တက်လူ သာလျှင်
မြန်မာပြည်လှ ၊ အားသစ်ရ၍
ဇေယျအောင်လံ ထူမည်တည်း ။

(nanoGPT) yekyaw.thu@gpu:~/exp/myPoetry/corpus/version1.0$
```

အဲဒီတုန်းက Jupyter Notebook နဲ့ run ခဲ့တာလို့ မှတ်မိနေတယ် ...  

```
(nanoGPT) yekyaw.thu@gpu:~/exp/myPoetry$ ls
corpus  notebooks  README.md
(nanoGPT) yekyaw.thu@gpu:~/exp/myPoetry$ cd notebooks/
(nanoGPT) yekyaw.thu@gpu:~/exp/myPoetry/notebooks$ ls
kabyarGPT2-building-experiment1.ipynb         srilm
kabyarGPT-notitle-building-experiment2.ipynb
(nanoGPT) yekyaw.thu@gpu:~/exp/myPoetry/notebooks$
```

## Jupyter Notebook Installation

ကိုယ်လက်ရှိ experiment လုပ်မယ့် python environment မှာ Jupyter notebook ကို run လို့ ရဖို့အတွက်က မရှိသေးရင် install လုပ်ရလိမ့်မယ်။  

```
(nanoGPT) yekyaw.thu@gpu:~$ conda install jupyter
Collecting package metadata (current_repodata.json): done
Solving environment: -
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::xz==5.4.2=h5eee18b_0
  - defaults/linux-64::openssl==3.0.11=h7f8727e_2
  - defaults/linux-64::python==3.8.18=h955ad1f_0
  - defaults/linux-64::ncurses==6.4=h6a678d5_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::pip==23.3=py38h06a4308_0
  - defaults/linux-64::setuptools==68.0.0=py38h06a4308_0
  - defaults/linux-64::wheel==0.41.2=py38h06a4308_0
  - defaults/linux-64::libffi==3.4.4=h6a678d5_0
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::sqlite==3.41.2=h5eee18b_0
  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 23.9.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/nanoGPT

  added / updated specs:
    - jupyter


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    aiofiles-22.1.0            |   py38h06a4308_0          24 KB
    aiosqlite-0.18.0           |   py38h06a4308_0          33 KB
    attrs-23.1.0               |   py38h06a4308_0         140 KB
    babel-2.11.0               |   py38h06a4308_0         6.8 MB
    beautifulsoup4-4.12.2      |   py38h06a4308_0         209 KB
    certifi-2023.7.22          |   py38h06a4308_0         153 KB
    cffi-1.15.1                |   py38h5eee18b_3         241 KB
    comm-0.1.2                 |   py38h06a4308_0          13 KB
    cryptography-41.0.3        |   py38hdda0065_0         2.0 MB
    cyrus-sasl-2.1.28          |       h52b45da_1         237 KB
    debugpy-1.6.7              |   py38h6a678d5_0         2.0 MB
    expat-2.5.0                |       h6a678d5_0         172 KB
    fontconfig-2.14.1          |       h4c34cd2_2         281 KB
    giflib-5.2.1               |       h5eee18b_3          80 KB
    glib-2.69.1                |       he621ea3_2         1.9 MB
    gst-plugins-base-1.14.1    |       h6a678d5_1         2.2 MB
    gstreamer-1.14.1           |       h5eee18b_1         1.7 MB
    importlib-metadata-6.0.0   |   py38h06a4308_0          38 KB
    importlib_metadata-6.0.0   |       hd3eb1b0_0           8 KB
    ipykernel-6.25.0           |   py38h2f386ee_0         228 KB
    ipython-8.12.2             |   py38h06a4308_0         1.1 MB
    ipywidgets-8.0.4           |   py38h06a4308_0         194 KB
    jpeg-9e                    |       h5eee18b_1         262 KB
    jsonschema-4.17.3          |   py38h06a4308_0         140 KB
    jupyter_client-7.4.9       |   py38h06a4308_0         205 KB
    jupyter_console-6.6.3      |   py38h06a4308_0          45 KB
    jupyter_core-5.3.0         |   py38h06a4308_0          89 KB
    jupyter_events-0.6.3       |   py38h06a4308_0          37 KB
    jupyter_server-1.23.4      |   py38h06a4308_0         382 KB
    jupyter_server_fileid-0.9.0|   py38h06a4308_0          29 KB
    jupyter_server_ydoc-0.8.0  |   py38h06a4308_1          21 KB
    jupyter_ydoc-0.2.4         |   py38h06a4308_0          15 KB
    jupyterlab-3.6.3           |   py38h06a4308_0         4.1 MB
    jupyterlab_server-2.22.0   |   py38h06a4308_0          82 KB
    jupyterlab_widgets-3.0.5   |   py38h06a4308_0         178 KB
    krb5-1.20.1                |       h143b758_1         1.3 MB
    libclang-14.0.6            |default_hc6dbbc7_1         137 KB
    libclang13-14.0.6          |default_he11475f_1         9.8 MB
    libcups-2.4.2              |       h2d74bed_1         4.5 MB
    libdeflate-1.17            |       h5eee18b_1          64 KB
    libevent-2.1.12            |       hdbd6064_1         453 KB
    libllvm14-14.0.6           |       hdb19cb5_3        33.4 MB
    libpng-1.6.39              |       h5eee18b_0         304 KB
    libpq-12.15                |       hdbd6064_1         2.4 MB
    libtiff-4.5.1              |       h6a678d5_0         533 KB
    libwebp-1.3.2              |       h11a3e52_0          87 KB
    libwebp-base-1.3.2         |       h5eee18b_0         387 KB
    libxkbcommon-1.0.1         |       h5eee18b_1         590 KB
    libxml2-2.10.4             |       hcbfbd50_0         755 KB
    libxslt-1.1.37             |       h2085143_0         266 KB
    lxml-4.9.3                 |   py38hdbbb534_0         1.5 MB
    lz4-c-1.9.4                |       h6a678d5_0         154 KB
    mysql-5.7.24               |       h721c034_2        60.0 MB
    nbclassic-0.5.5            |   py38h06a4308_0         6.1 MB
    nbformat-5.9.2             |   py38h06a4308_0         136 KB
    nest-asyncio-1.5.6         |   py38h06a4308_0          14 KB
    notebook-6.5.4             |   py38h06a4308_1         532 KB
    nspr-4.35                  |       h6a678d5_0         244 KB
    nss-3.89.1                 |       h6a678d5_0         2.1 MB
    packaging-23.1             |   py38h06a4308_0          77 KB
    platformdirs-3.10.0        |   py38h06a4308_0          33 KB
    prompt-toolkit-3.0.36      |   py38h06a4308_0         574 KB
    prompt_toolkit-3.0.36      |       hd3eb1b0_0           5 KB
    pygments-2.15.1            |   py38h06a4308_1         1.8 MB
    pyopenssl-23.2.0           |   py38h06a4308_0          96 KB
    python-json-logger-2.0.7   |   py38h06a4308_0          16 KB
    pytz-2023.3.post1          |   py38h06a4308_0         209 KB
    pyyaml-6.0                 |   py38h5eee18b_1         189 KB
    qt-main-5.15.2             |       h7358343_9        53.7 MB
    qt-webengine-5.15.9        |       h9ab4d14_7        53.8 MB
    qtconsole-5.4.2            |   py38h06a4308_0         191 KB
    qtwebkit-5.212             |       h3fafdc1_5        16.2 MB
    requests-2.31.0            |   py38h06a4308_0          96 KB
    rfc3339-validator-0.1.4    |   py38h06a4308_0           9 KB
    rfc3986-validator-0.1.1    |   py38h06a4308_0           9 KB
    soupsieve-2.5              |   py38h06a4308_0          69 KB
    terminado-0.17.1           |   py38h06a4308_0          31 KB
    tomli-2.0.1                |   py38h06a4308_0          24 KB
    tornado-6.3.3              |   py38h5eee18b_0         634 KB
    traitlets-5.7.1            |   py38h06a4308_0         200 KB
    typing-extensions-4.7.1    |   py38h06a4308_0           9 KB
    typing_extensions-4.7.1    |   py38h06a4308_0          55 KB
    urllib3-1.26.16            |   py38h06a4308_0         200 KB
    widgetsnbextension-4.0.5   |   py38h06a4308_0         875 KB
    y-py-0.5.9                 |   py38h52d8a92_0         1.3 MB
    yaml-0.2.5                 |       h7b6447c_0          75 KB
    ypy-websocket-0.8.2        |   py38h06a4308_0          26 KB
    zipp-3.11.0                |   py38h06a4308_0          19 KB
    zstd-1.5.5                 |       hc292b87_0         647 KB
    ------------------------------------------------------------
                                           Total:       281.7 MB

The following NEW packages will be INSTALLED:

  aiofiles           pkgs/main/linux-64::aiofiles-22.1.0-py38h06a4308_0
  aiosqlite          pkgs/main/linux-64::aiosqlite-0.18.0-py38h06a4308_0
  anyio              pkgs/main/linux-64::anyio-3.5.0-py38h06a4308_0
  argon2-cffi        pkgs/main/noarch::argon2-cffi-21.3.0-pyhd3eb1b0_0
  argon2-cffi-bindi~ pkgs/main/linux-64::argon2-cffi-bindings-21.2.0-py38h7f8727e_0
  asttokens          pkgs/main/noarch::asttokens-2.0.5-pyhd3eb1b0_0
  attrs              pkgs/main/linux-64::attrs-23.1.0-py38h06a4308_0
  babel              pkgs/main/linux-64::babel-2.11.0-py38h06a4308_0
  backcall           pkgs/main/noarch::backcall-0.2.0-pyhd3eb1b0_0
  beautifulsoup4     pkgs/main/linux-64::beautifulsoup4-4.12.2-py38h06a4308_0
  bleach             pkgs/main/noarch::bleach-4.1.0-pyhd3eb1b0_0
  brotlipy           pkgs/main/linux-64::brotlipy-0.7.0-py38h27cfd23_1003
  certifi            pkgs/main/linux-64::certifi-2023.7.22-py38h06a4308_0
  cffi               pkgs/main/linux-64::cffi-1.15.1-py38h5eee18b_3
  charset-normalizer pkgs/main/noarch::charset-normalizer-2.0.4-pyhd3eb1b0_0
  comm               pkgs/main/linux-64::comm-0.1.2-py38h06a4308_0
  cryptography       pkgs/main/linux-64::cryptography-41.0.3-py38hdda0065_0
  cyrus-sasl         pkgs/main/linux-64::cyrus-sasl-2.1.28-h52b45da_1
  dbus               pkgs/main/linux-64::dbus-1.13.18-hb2f20db_0
  debugpy            pkgs/main/linux-64::debugpy-1.6.7-py38h6a678d5_0
  decorator          pkgs/main/noarch::decorator-5.1.1-pyhd3eb1b0_0
  defusedxml         pkgs/main/noarch::defusedxml-0.7.1-pyhd3eb1b0_0
  entrypoints        pkgs/main/linux-64::entrypoints-0.4-py38h06a4308_0
  executing          pkgs/main/noarch::executing-0.8.3-pyhd3eb1b0_0
  expat              pkgs/main/linux-64::expat-2.5.0-h6a678d5_0
  fontconfig         pkgs/main/linux-64::fontconfig-2.14.1-h4c34cd2_2
  freetype           pkgs/main/linux-64::freetype-2.12.1-h4a9f257_0
  giflib             pkgs/main/linux-64::giflib-5.2.1-h5eee18b_3
  glib               pkgs/main/linux-64::glib-2.69.1-he621ea3_2
  gst-plugins-base   pkgs/main/linux-64::gst-plugins-base-1.14.1-h6a678d5_1
  gstreamer          pkgs/main/linux-64::gstreamer-1.14.1-h5eee18b_1
  icu                pkgs/main/linux-64::icu-58.2-he6710b0_3
  idna               pkgs/main/linux-64::idna-3.4-py38h06a4308_0
  importlib-metadata pkgs/main/linux-64::importlib-metadata-6.0.0-py38h06a4308_0
  importlib_metadata pkgs/main/noarch::importlib_metadata-6.0.0-hd3eb1b0_0
  importlib_resourc~ pkgs/main/noarch::importlib_resources-5.2.0-pyhd3eb1b0_1
  ipykernel          pkgs/main/linux-64::ipykernel-6.25.0-py38h2f386ee_0
  ipython            pkgs/main/linux-64::ipython-8.12.2-py38h06a4308_0
  ipython_genutils   pkgs/main/noarch::ipython_genutils-0.2.0-pyhd3eb1b0_1
  ipywidgets         pkgs/main/linux-64::ipywidgets-8.0.4-py38h06a4308_0
  jedi               pkgs/main/linux-64::jedi-0.18.1-py38h06a4308_1
  jinja2             pkgs/main/linux-64::jinja2-3.1.2-py38h06a4308_0
  jpeg               pkgs/main/linux-64::jpeg-9e-h5eee18b_1
  json5              pkgs/main/noarch::json5-0.9.6-pyhd3eb1b0_0
  jsonschema         pkgs/main/linux-64::jsonschema-4.17.3-py38h06a4308_0
  jupyter            pkgs/main/linux-64::jupyter-1.0.0-py38h06a4308_8
  jupyter_client     pkgs/main/linux-64::jupyter_client-7.4.9-py38h06a4308_0
  jupyter_console    pkgs/main/linux-64::jupyter_console-6.6.3-py38h06a4308_0
  jupyter_core       pkgs/main/linux-64::jupyter_core-5.3.0-py38h06a4308_0
  jupyter_events     pkgs/main/linux-64::jupyter_events-0.6.3-py38h06a4308_0
  jupyter_server     pkgs/main/linux-64::jupyter_server-1.23.4-py38h06a4308_0
  jupyter_server_fi~ pkgs/main/linux-64::jupyter_server_fileid-0.9.0-py38h06a4308_0
  jupyter_server_yd~ pkgs/main/linux-64::jupyter_server_ydoc-0.8.0-py38h06a4308_1
  jupyter_ydoc       pkgs/main/linux-64::jupyter_ydoc-0.2.4-py38h06a4308_0
  jupyterlab         pkgs/main/linux-64::jupyterlab-3.6.3-py38h06a4308_0
  jupyterlab_pygmen~ pkgs/main/noarch::jupyterlab_pygments-0.1.2-py_0
  jupyterlab_server  pkgs/main/linux-64::jupyterlab_server-2.22.0-py38h06a4308_0
  jupyterlab_widgets pkgs/main/linux-64::jupyterlab_widgets-3.0.5-py38h06a4308_0
  krb5               pkgs/main/linux-64::krb5-1.20.1-h143b758_1
  lerc               pkgs/main/linux-64::lerc-3.0-h295c915_0
  libclang           pkgs/main/linux-64::libclang-14.0.6-default_hc6dbbc7_1
  libclang13         pkgs/main/linux-64::libclang13-14.0.6-default_he11475f_1
  libcups            pkgs/main/linux-64::libcups-2.4.2-h2d74bed_1
  libdeflate         pkgs/main/linux-64::libdeflate-1.17-h5eee18b_1
  libedit            pkgs/main/linux-64::libedit-3.1.20221030-h5eee18b_0
  libevent           pkgs/main/linux-64::libevent-2.1.12-hdbd6064_1
  libllvm14          pkgs/main/linux-64::libllvm14-14.0.6-hdb19cb5_3
  libpng             pkgs/main/linux-64::libpng-1.6.39-h5eee18b_0
  libpq              pkgs/main/linux-64::libpq-12.15-hdbd6064_1
  libsodium          pkgs/main/linux-64::libsodium-1.0.18-h7b6447c_0
  libtiff            pkgs/main/linux-64::libtiff-4.5.1-h6a678d5_0
  libuuid            pkgs/main/linux-64::libuuid-1.41.5-h5eee18b_0
  libwebp            pkgs/main/linux-64::libwebp-1.3.2-h11a3e52_0
  libwebp-base       pkgs/main/linux-64::libwebp-base-1.3.2-h5eee18b_0
  libxcb             pkgs/main/linux-64::libxcb-1.15-h7f8727e_0
  libxkbcommon       pkgs/main/linux-64::libxkbcommon-1.0.1-h5eee18b_1
  libxml2            pkgs/main/linux-64::libxml2-2.10.4-hcbfbd50_0
  libxslt            pkgs/main/linux-64::libxslt-1.1.37-h2085143_0
  lxml               pkgs/main/linux-64::lxml-4.9.3-py38hdbbb534_0
  lz4-c              pkgs/main/linux-64::lz4-c-1.9.4-h6a678d5_0
  markupsafe         pkgs/main/linux-64::markupsafe-2.1.1-py38h7f8727e_0
  matplotlib-inline  pkgs/main/linux-64::matplotlib-inline-0.1.6-py38h06a4308_0
  mistune            pkgs/main/linux-64::mistune-0.8.4-py38h7b6447c_1000
  mysql              pkgs/main/linux-64::mysql-5.7.24-h721c034_2
  nbclassic          pkgs/main/linux-64::nbclassic-0.5.5-py38h06a4308_0
  nbclient           pkgs/main/linux-64::nbclient-0.5.13-py38h06a4308_0
  nbconvert          pkgs/main/linux-64::nbconvert-6.5.4-py38h06a4308_0
  nbformat           pkgs/main/linux-64::nbformat-5.9.2-py38h06a4308_0
  nest-asyncio       pkgs/main/linux-64::nest-asyncio-1.5.6-py38h06a4308_0
  notebook           pkgs/main/linux-64::notebook-6.5.4-py38h06a4308_1
  notebook-shim      pkgs/main/linux-64::notebook-shim-0.2.2-py38h06a4308_0
  nspr               pkgs/main/linux-64::nspr-4.35-h6a678d5_0
  nss                pkgs/main/linux-64::nss-3.89.1-h6a678d5_0
  packaging          pkgs/main/linux-64::packaging-23.1-py38h06a4308_0
  pandocfilters      pkgs/main/noarch::pandocfilters-1.5.0-pyhd3eb1b0_0
  parso              pkgs/main/noarch::parso-0.8.3-pyhd3eb1b0_0
  pcre               pkgs/main/linux-64::pcre-8.45-h295c915_0
  pexpect            pkgs/main/noarch::pexpect-4.8.0-pyhd3eb1b0_3
  pickleshare        pkgs/main/noarch::pickleshare-0.7.5-pyhd3eb1b0_1003
  pkgutil-resolve-n~ pkgs/main/linux-64::pkgutil-resolve-name-1.3.10-py38h06a4308_0
  platformdirs       pkgs/main/linux-64::platformdirs-3.10.0-py38h06a4308_0
  ply                pkgs/main/linux-64::ply-3.11-py38_0
  prometheus_client  pkgs/main/linux-64::prometheus_client-0.14.1-py38h06a4308_0
  prompt-toolkit     pkgs/main/linux-64::prompt-toolkit-3.0.36-py38h06a4308_0
  prompt_toolkit     pkgs/main/noarch::prompt_toolkit-3.0.36-hd3eb1b0_0
  psutil             pkgs/main/linux-64::psutil-5.9.0-py38h5eee18b_0
  ptyprocess         pkgs/main/noarch::ptyprocess-0.7.0-pyhd3eb1b0_2
  pure_eval          pkgs/main/noarch::pure_eval-0.2.2-pyhd3eb1b0_0
  pycparser          pkgs/main/noarch::pycparser-2.21-pyhd3eb1b0_0
  pygments           pkgs/main/linux-64::pygments-2.15.1-py38h06a4308_1
  pyopenssl          pkgs/main/linux-64::pyopenssl-23.2.0-py38h06a4308_0
  pyqt               pkgs/main/linux-64::pyqt-5.15.7-py38h6a678d5_1
  pyqt5-sip          pkgs/main/linux-64::pyqt5-sip-12.11.0-py38h6a678d5_1
  pyrsistent         pkgs/main/linux-64::pyrsistent-0.18.0-py38heee7806_0
  pysocks            pkgs/main/linux-64::pysocks-1.7.1-py38h06a4308_0
  python-dateutil    pkgs/main/noarch::python-dateutil-2.8.2-pyhd3eb1b0_0
  python-fastjsonsc~ pkgs/main/linux-64::python-fastjsonschema-2.16.2-py38h06a4308_0
  python-json-logger pkgs/main/linux-64::python-json-logger-2.0.7-py38h06a4308_0
  pytz               pkgs/main/linux-64::pytz-2023.3.post1-py38h06a4308_0
  pyyaml             pkgs/main/linux-64::pyyaml-6.0-py38h5eee18b_1
  pyzmq              pkgs/main/linux-64::pyzmq-23.2.0-py38h6a678d5_0
  qt-main            pkgs/main/linux-64::qt-main-5.15.2-h7358343_9
  qt-webengine       pkgs/main/linux-64::qt-webengine-5.15.9-h9ab4d14_7
  qtconsole          pkgs/main/linux-64::qtconsole-5.4.2-py38h06a4308_0
  qtpy               pkgs/main/linux-64::qtpy-2.2.0-py38h06a4308_0
  qtwebkit           pkgs/main/linux-64::qtwebkit-5.212-h3fafdc1_5
  requests           pkgs/main/linux-64::requests-2.31.0-py38h06a4308_0
  rfc3339-validator  pkgs/main/linux-64::rfc3339-validator-0.1.4-py38h06a4308_0
  rfc3986-validator  pkgs/main/linux-64::rfc3986-validator-0.1.1-py38h06a4308_0
  send2trash         pkgs/main/noarch::send2trash-1.8.0-pyhd3eb1b0_1
  sip                pkgs/main/linux-64::sip-6.6.2-py38h6a678d5_0
  six                pkgs/main/noarch::six-1.16.0-pyhd3eb1b0_1
  sniffio            pkgs/main/linux-64::sniffio-1.2.0-py38h06a4308_1
  soupsieve          pkgs/main/linux-64::soupsieve-2.5-py38h06a4308_0
  stack_data         pkgs/main/noarch::stack_data-0.2.0-pyhd3eb1b0_0
  terminado          pkgs/main/linux-64::terminado-0.17.1-py38h06a4308_0
  tinycss2           pkgs/main/linux-64::tinycss2-1.2.1-py38h06a4308_0
  toml               pkgs/main/noarch::toml-0.10.2-pyhd3eb1b0_0
  tomli              pkgs/main/linux-64::tomli-2.0.1-py38h06a4308_0
  tornado            pkgs/main/linux-64::tornado-6.3.3-py38h5eee18b_0
  traitlets          pkgs/main/linux-64::traitlets-5.7.1-py38h06a4308_0
  typing-extensions  pkgs/main/linux-64::typing-extensions-4.7.1-py38h06a4308_0
  typing_extensions  pkgs/main/linux-64::typing_extensions-4.7.1-py38h06a4308_0
  urllib3            pkgs/main/linux-64::urllib3-1.26.16-py38h06a4308_0
  wcwidth            pkgs/main/noarch::wcwidth-0.2.5-pyhd3eb1b0_0
  webencodings       pkgs/main/linux-64::webencodings-0.5.1-py38_1
  websocket-client   pkgs/main/linux-64::websocket-client-0.58.0-py38h06a4308_4
  widgetsnbextension pkgs/main/linux-64::widgetsnbextension-4.0.5-py38h06a4308_0
  y-py               pkgs/main/linux-64::y-py-0.5.9-py38h52d8a92_0
  yaml               pkgs/main/linux-64::yaml-0.2.5-h7b6447c_0
  ypy-websocket      pkgs/main/linux-64::ypy-websocket-0.8.2-py38h06a4308_0
  zeromq             pkgs/main/linux-64::zeromq-4.3.4-h2531618_0
  zipp               pkgs/main/linux-64::zipp-3.11.0-py38h06a4308_0
  zstd               pkgs/main/linux-64::zstd-1.5.5-hc292b87_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
tomli-2.0.1          | 24 KB     | ############################################### | 100%
ipython-8.12.2       | 1.1 MB    | ############################################### | 100%
pyyaml-6.0           | 189 KB    | ############################################### | 100%
aiofiles-22.1.0      | 24 KB     | ############################################### | 100%
libpng-1.6.39        | 304 KB    | ############################################### | 100%
ipykernel-6.25.0     | 228 KB    | ############################################### | 100%
cffi-1.15.1          | 241 KB    | ############################################### | 100%
libcups-2.4.2        | 4.5 MB    | ############################################### | 100%
jupyterlab-3.6.3     | 4.1 MB    | ############################################### | 100%
jpeg-9e              | 262 KB    | ############################################### | 100%
notebook-6.5.4       | 532 KB    | ############################################### | 100%
cryptography-41.0.3  | 2.0 MB    | ############################################### | 100%
pyopenssl-23.2.0     | 96 KB     | ############################################### | 100%
zstd-1.5.5           | 647 KB    | ############################################### | 100%
prompt-toolkit-3.0.3 | 574 KB    | ############################################### | 100%
pytz-2023.3.post1    | 209 KB    | ############################################### | 100%
jupyter_core-5.3.0   | 89 KB     | ############################################### | 100%
pygments-2.15.1      | 1.8 MB    | ############################################### | 100%
typing-extensions-4. | 9 KB      | ############################################### | 100%
gstreamer-1.14.1     | 1.7 MB    | ############################################### | 100%
aiosqlite-0.18.0     | 33 KB     | ############################################### | 100%
y-py-0.5.9           | 1.3 MB    | ############################################### | 100%
qtwebkit-5.212       | 16.2 MB   | ############################################### | 100%
libxml2-2.10.4       | 755 KB    | ############################################### | 100%
certifi-2023.7.22    | 153 KB    | ############################################### | 100%
libwebp-base-1.3.2   | 387 KB    | ############################################### | 100%
libclang13-14.0.6    | 9.8 MB    | ############################################### | 100%
importlib-metadata-6 | 38 KB     | ############################################### | 100%
libxslt-1.1.37       | 266 KB    | ############################################### | 100%
jupyter_server_ydoc- | 21 KB     | ############################################### | 100%
jupyterlab_widgets-3 | 178 KB    | ############################################### | 100%
rfc3339-validator-0. | 9 KB      | ############################################### | 100%
packaging-23.1       | 77 KB     | ############################################### | 100%
jupyter_server-1.23. | 382 KB    | ############################################### | 100%
libtiff-4.5.1        | 533 KB    | ############################################### | 100%
yaml-0.2.5           | 75 KB     | ############################################### | 100%
nbformat-5.9.2       | 136 KB    | ############################################### | 100%
libdeflate-1.17      | 64 KB     | ############################################### | 100%
widgetsnbextension-4 | 875 KB    | ############################################### | 100%
requests-2.31.0      | 96 KB     | ############################################### | 100%
fontconfig-2.14.1    | 281 KB    | ############################################### | 100%
glib-2.69.1          | 1.9 MB    | ############################################### | 100%
rfc3986-validator-0. | 9 KB      | ############################################### | 100%
qtconsole-5.4.2      | 191 KB    | ############################################### | 100%
cyrus-sasl-2.1.28    | 237 KB    | ############################################### | 100%
comm-0.1.2           | 13 KB     | ############################################### | 100%
urllib3-1.26.16      | 200 KB    | ############################################### | 100%
python-json-logger-2 | 16 KB     | ############################################### | 100%
nbclassic-0.5.5      | 6.1 MB    | ############################################### | 100%
libllvm14-14.0.6     | 33.4 MB   | ############################################### | 100%
platformdirs-3.10.0  | 33 KB     | ############################################### | 100%
jupyter_events-0.6.3 | 37 KB     | ############################################### | 100%
jupyter_ydoc-0.2.4   | 15 KB     | ############################################### | 100%
jsonschema-4.17.3    | 140 KB    | ############################################### | 100%
prompt_toolkit-3.0.3 | 5 KB      | ############################################### | 100%
krb5-1.20.1          | 1.3 MB    | ############################################### | 100%
libwebp-1.3.2        | 87 KB     | ############################################### | 100%
expat-2.5.0          | 172 KB    | ############################################### | 100%
libevent-2.1.12      | 453 KB    | ############################################### | 100%
jupyterlab_server-2. | 82 KB     | ############################################### | 100%
terminado-0.17.1     | 31 KB     | ############################################### | 100%
qt-main-5.15.2       | 53.7 MB   | ############################################### | 100%
lxml-4.9.3           | 1.5 MB    | ############################################### | 100%
qt-webengine-5.15.9  | 53.8 MB   | ############################################### | 100%
jupyter_server_filei | 29 KB     | ############################################### | 100%
ypy-websocket-0.8.2  | 26 KB     | ############################################### | 100%
traitlets-5.7.1      | 200 KB    | ############################################### | 100%
zipp-3.11.0          | 19 KB     | ############################################### | 100%
nspr-4.35            | 244 KB    | ############################################### | 100%
jupyter_console-6.6. | 45 KB     | ############################################### | 100%
mysql-5.7.24         | 60.0 MB   | ############################################### | 100%
nest-asyncio-1.5.6   | 14 KB     | ############################################### | 100%
attrs-23.1.0         | 140 KB    | ############################################### | 100%
gst-plugins-base-1.1 | 2.2 MB    | ############################################### | 100%
importlib_metadata-6 | 8 KB      | ############################################### | 100%
ipywidgets-8.0.4     | 194 KB    | ############################################### | 100%
debugpy-1.6.7        | 2.0 MB    | ############################################### | 100%
giflib-5.2.1         | 80 KB     | ############################################### | 100%
tornado-6.3.3        | 634 KB    | ############################################### | 100%
libclang-14.0.6      | 137 KB    | ############################################### | 100%
libxkbcommon-1.0.1   | 590 KB    | ############################################### | 100%
typing_extensions-4. | 55 KB     | ############################################### | 100%
libpq-12.15          | 2.4 MB    | ############################################### | 100%
jupyter_client-7.4.9 | 205 KB    | ############################################### | 100%
nss-3.89.1           | 2.1 MB    | ############################################### | 100%
babel-2.11.0         | 6.8 MB    | ############################################### | 100%
lz4-c-1.9.4          | 154 KB    | ############################################### | 100%
soupsieve-2.5        | 69 KB     | ############################################### | 100%
beautifulsoup4-4.12. | 209 KB    | ############################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(nanoGPT) yekyaw.thu@gpu:~$
```

Check the notebook version:  

```
(nanoGPT) yekyaw.thu@gpu:~$ jupyter notebook --version
6.5.4
(nanoGPT) yekyaw.thu@gpu:~$
```

## Relating to Port-forwarding

Server ပေါ်မှာ Jupyter notebook ကို run ထားပြီးတော့ အဲဒီ Jupyter notebook ကို ကိုယ့် local စက်ထဲက browser နဲ့ ခေါ်ကြည့်မယ်ဆိုရင်တော့ port-forwarding ကိစ္စကို သိဖို့ လိုအပ်တယ်။  

Explanation about port-forwarding: [https://github.com/ye-kyaw-thu/error-overflow/blob/master/running-jupyter-on-server-and-port-forwarding.md](https://github.com/ye-kyaw-thu/error-overflow/blob/master/running-jupyter-on-server-and-port-forwarding.md)  

## Preparation

kabyarGPT တုန်းက သုံးခဲ့တဲ့ notebook ကို copy ကူးယူပြီး rename လုပ် ...  

```
(nanoGPT) yekyaw.thu@gpu:~/exp$ cp ./myPoetry/notebooks/kabyarGPT-notitle-building-experiment2.ipynb ./myHatespeech/
(nanoGPT) yekyaw.thu@gpu:~/exp$ cd ./myHatespeech/
(nanoGPT) yekyaw.thu@gpu:~/exp/myHatespeech$ ls
kabyarGPT-notitle-building-experiment2.ipynb
(nanoGPT) yekyaw.thu@gpu:~/exp/myHatespeech$ mv kabyarGPT-notitle-building-experiment2.ipynb myHatespeech-GPT2-exp1.ipynb
(nanoGPT) yekyaw.thu@gpu:~/exp/myHatespeech$ ls
myHatespeech-GPT2-exp1.ipynb
(nanoGPT) yekyaw.thu@gpu:~/exp/myHatespeech$
```

Data ကိုလည်း local စက်ကနေ server ပေါ်ကို ကော်ပီကူယူခဲ့ ...  

```
C:\Users\ye>scp -P XXX -i C:\Users\801680\.ssh\xxxx Downloads\hs_data_4Oct2023.txt yekyaw.thu@xxx.xx.xx.xxx:/home/yekyaw.thu/exp/myHatespeech/data
Enter passphrase for key 'C:/Users/801680/.ssh/xxx':
hs_data_4Oct2023.txt                                    100% 2199KB   2.0MB/s   00:01

C:\Users\ye>
```

server ပေါ်မှာ ကူးခဲ့တဲ့ ဒေတာကို check လုပ် ...  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ ls
hs_data_4Oct2023.txt
```

filesize ကို စစ်ကြည့်ခဲ့ ...  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ wc hs_data_4Oct2023.txt
  10140  181428 2252181 hs_data_4Oct2023.txt
```

ဖိုင်ထဲက စာကြောင်းတွေကို check လုပ် ...  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ head hs_data_4Oct2023.txt
ဖော်လော်မော်/ab မ ဟုတ် လို့ ပေါ့ 🤣 🤣   ab
နား ကို မ လည် တာ   no
ဆောက်မြင်ကပ်/ab ထင် တာ ပဲ    ab
ကွမ်းယာ မှာ ထည့် စား တဲ့ စမုန်စပါး ထင် တယ် no
ဖလော်မော်/ab next version ab
ငါ လည်း သိ ချင် နေ တာ 😁 အဲ့လို စကား တွေ ကျ နားမလည် လို့ သင် ပေး ကြ ပါ ဦး 😂 no
ငါ မ သိ လို့ ကိုကို့ ကို မေး ကြည့် တာ ကိုကို က လည်း baby က လွဲ ရင် မ သိ ဘူး တဲ့ 🥺       no
ဖော်လော်မော်/ab နဲ့ ညီမ တော် တယ် လေ 😬  ab
sမွေး/ab ကြီး တဲ့ 😂        ab
$မွှေး/ab ပါ      ab
```

ဖိုင်ရဲ့ နောက်ဆုံးပိုင်းကိုလည်း tail command နဲ့ စစ်ကြည့်ခဲ့ ...  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ tail hs_data_4Oct2023.txt
သူ့ ကို ဘာ ကြည့် ပြီး vote ပေး ကြ တာ ပါ လိမ့် $ရူးမ/ab ဘာ မ ဟုတ် တဲ့ ကိစ္စ ကြောင့် ရွှေကြို အခွင့်အရေး ကို ဆုံးရှုံး မ ခံ နိုင် လို့ ဆို ပြီး ပြော တဲ့ $ရူးမ/ab       ab
ဖင်အရှည်ကြီးခံလိုက်/ab တစ်ခါတည်း အကုန် ကြို ပြီး သား ပဲ 🦭      ab
အိပ်မက် က အမ တစ် ယောက် ပဲ ရှိ တာ လား 🥲 no
SattPatt/ab !! ဘာ မ ဟုတ် တဲ့ ပြဿနာ တဲ့ PayloeeeMaaaGGG/ab     ab
စောက်ဆင့်မရှိ/ab တဲ့ ဟာ တွေ က လည်း အခုတလော ခပ်စိပ်စိပ် တွေ့ လာ ရ တယ် 🤣🤣🤣🤣🤣 ရေး ချင် လွန်း လို့ မ ဟုတ် ဘူး နော် ရှက် တတ် ဦး မ လား လို့ ဝင့် မန့် တာ       ab
ဘာ မ ဟုတ် တာ လေး တဲ့ အာ့ ဆို ဟုတ် တဲ့ ဟာ ဘောပဲမနေ/ab နော် အမကြီး      ab
ထမင်းစားတိုင်းလူမဖြစ်နိုင်ဘူး/ab ဆို တာ ခု မှ အရှင်လတ်လတ် မြင် ဖူး တော့ တယ် ကောင်မ/ab မွေးကတည်းကအသေလေးမွေးလာရမှာ/le        le
အော် ဘာ မ ဟုတ် တာ တဲ့ လား ပြောထွက်တဲ့ပါးစပ်လေးကိုအက်ဆစ်လေးနဲ့သွားဆေးစေချင်/ab     ab
ဗန်းကိုင် နဲ့ မအလ/ab|po ဘောကိုင်/ab      ab
စိတ်မပူ နဲ့ ရွှေကြို ပြီး ရင် ဖင်ခံ/ab ရ မှာ ညီမလေး fighting 22 နှစ် က ငါ 25 နှစ် ထက် အို/bo နေ တော့ အား တောင် နာ တယ် 😂 😂      bo
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$
```

## Change File Format

LLM ဆောက်ပြီးတော့ hatespeech generation လုပ်ကြည့်ချင်တာမို့လို့ tag တွေကို ဖြုတ်ဖို့ လိုအပ်တယ်။ file format ကို စာသားချည်းပဲ ဖြစ်အောင် ပြင်ဆင်ဖို့ လိုအပ်တယ်။  

Write a Python script:  

```python
## Writen by Ye Kyaw Thu, LU Lab., Myanmar
## for removing hatespeech tags
## last updated: 19 Oct 2023

import argparse
import re

def process_text(input_file, output_file=None):
    with open(input_file, 'r', encoding='utf-8') as file:
        lines = file.readlines()

    cleaned_lines = []
    for line in lines:
        # Split the line by tabs and take the first column
        sentence = line.split('\t')[0]
        # Use regex to remove the tags following "/"
        cleaned_sentence = re.sub(r'/[a-zA-Z|]*', '', sentence)
        cleaned_lines.append(cleaned_sentence)

    if output_file:
        with open(output_file, 'w', encoding='utf-8') as file:
            file.write('\n'.join(cleaned_lines))
    else:
        for cleaned_line in cleaned_lines:
            print(cleaned_line)

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description='Process a text file to remove tags.')
    parser.add_argument('-i', '--input_file', required=True, help='Path to the input file.')
    parser.add_argument('-o', '--output_file', help='Path to the output file. If not provided, result will be printed to the screen.')

    args = parser.parse_args()

    process_text(args.input_file, args.output_file)

```

အရင်ဆုံး ဖိုင်အသေးတစ်ဖိုင်ကို ဆောက်ပြီး python code နဲ့ testing လုပ်ခဲ့တယ်။  
အဲဒီဖိုင်ထဲမှာ pipe လည်း ပါအောင် ပြင်ဆင်ခဲ့ ...   

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ cat small.txt
စဥ်းစား ပြီး မင်း အမေ မင်း လိုး/ab|se လိုက် ပါ လား       ab
လာ ဟောင် စမ်း ခွေးမသား/ab နဲ့ ခွေးမသမီး/ab တွေ လူကြီး လူငယ် မရွေး မင်းမေလိုး/ab လိုက် တစ် ဖက် သား ကို အား နေ အာခြောင်/ab တဲ့ ဟာ တွေ အချိန် ပြည့် ငါ့ ဆီ က မင်း အမေ ကို လိုး/ab|se ပဲ 🤏🏻    ab
ကိုယ်လုံးတီး/ab|se နဲ့ ဆို ပို ပြီး နာမည်ကြီး သွား မယ်   ab
သီချင်း ရိုက် မ နေ နဲ့ ကွာ ဖူးကား/se ရိုက် လေ မအလ/ab|po ခေတ် ပဲ နော်   se
သီချင်း နဲ့ ကောင်မနို့/se နဲ့ ကောင်မဖင်/se နဲ့ ဘာ ဆိုင် လဲ ဟင် မအလ/ab|po အကြိုက် ရိုက် နေ ကြ တာ ကိုး မအလ/ab တွေ က ဆင်ဆာ မ ဖြတ် ဘူး နော် အိုးကြည့်ကောင်း/se နေ တာ ကိုး 🤣🤣🤣🤣       se
pornကားသာရိုက်/se|ab ကြ ပါ တော့ လား lee/ab အနုပညာ လား 😎     ab
ခွေးရုပ်ပေါက်/ab|bo နေ တာ မိမဆုံးမဖမဆုံးမ/ab သား သမီး တွေ မှန်း သိသာ တယ် 🖕🖕🖕 ဘောပဲ/ab        ab
စောက်ကျက်သရေတုံး/bo|ab ဖက်ရှင် နဲ့ ၊ အ မင်္ဂလာ သီချင်း တွေ ၊ -ီး/ab -ီး/ab -ီး(-=လ)/ab ပေါ့       ab
ဖင်ရိုက်/se လိုက် တာ ပရိတ်သတ် အားပေး မှု မ ရှိ ဘူး ဖင်ချ/se|ab လိုက် ရင် ပို အောင်မြင် နိုင် ပါ တယ် se
စောင်နိုင်ငံ/po|ab ရဲ့ မ ကောင်း တာ က တစ် မျိုး နင် တို့ အပြာကားမိသားစု/ab တွေ က တစ် မျိုး စောင်ကောင်/ab တွေ     ab
ဖော်လော်မော်/ab မ ဟုတ် လို့ ပေါ့ 🤣 🤣   ab
နား ကို မ လည် တာ   no
ဆောက်မြင်ကပ်/ab ထင် တာ ပဲ    ab
ကွမ်းယာ မှာ ထည့် စား တဲ့ စမုန်စပါး ထင် တယ် no
ဖလော်မော်/ab next version ab
ငါ လည်း သိ ချင် နေ တာ 😁 အဲ့လို စကား တွေ ကျ နားမလည် လို့ သင် ပေး ကြ ပါ ဦး 😂 no
ငါ မ သိ လို့ ကိုကို့ ကို မေး ကြည့် တာ ကိုကို က လည်း baby က လွဲ ရင် မ သိ ဘူး တဲ့ 🥺       no
ဖော်လော်မော်/ab နဲ့ ညီမ တော် တယ် လေ 😬  ab
sမွေး/ab ကြီး တဲ့ 😂        ab
$မွှေး/ab ပါ      ab
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$
```

test run start ...  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ python ./get_text.py -i small.txt -o small.clean.txt
```

input နဲ့ output ဖိုင်ပမာဏကို စစ်ကြည့်တော့ တစ်ကြောင်းကွာနေတာကို အောက်ပါအတိုင်း တွေ့ရ ...  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ wc {small,small.clean}.txt
  20  261 3316 small.txt
  19  241 3123 small.clean.txt
  39  502 6439 total
```

file type ကို စစ်ကြည့်တော့လည်း ပြဿနာ မတွေ့ရဘူး။  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ file small.txt
small.txt: UTF-8 Unicode text
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ file small.clean.txt
small.clean.txt: UTF-8 Unicode text
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$
```

output file ကို လည်း စစ်ကြည့်ခဲ့ ...  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ cat small.clean.txt
စဥ်းစား ပြီး မင်း အမေ မင်း လိုး လိုက် ပါ လား
လာ ဟောင် စမ်း ခွေးမသား နဲ့ ခွေးမသမီး တွေ လူကြီး လူငယ် မရွေး မင်းမေလိုး လိုက် တစ် ဖက် သား ကို အား နေ အာခြောင် တဲ့ ဟာ တွေ အချိန် ပြည့် ငါ့ ဆီ က မင်း အမေ ကို လိုး ပဲ 🤏🏻
ကိုယ်လုံးတီး နဲ့ ဆို ပို ပြီး နာမည်ကြီး သွား မယ်
သီချင်း ရိုက် မ နေ နဲ့ ကွာ ဖူးကား ရိုက် လေ မအလ ခေတ် ပဲ နော်
သီချင်း နဲ့ ကောင်မနို့ နဲ့ ကောင်မဖင် နဲ့ ဘာ ဆိုင် လဲ ဟင် မအလ အကြိုက် ရိုက် နေ ကြ တာ ကိုး မအလ တွေ က ဆင်ဆာ မ ဖြတ် ဘူး နော် အိုးကြည့်ကောင်း နေ တာ ကိုး 🤣🤣🤣🤣
pornကားသာရိုက် ကြ ပါ တော့ လား lee အနုပညာ လား 😎
ခွေးရုပ်ပေါက် နေ တာ မိမဆုံးမဖမဆုံးမ သား သမီး တွေ မှန်း သိသာ တယ် 🖕🖕🖕 ဘောပဲ
စောက်ကျက်သရေတုံး ဖက်ရှင် နဲ့ ၊ အ မင်္ဂလာ သီချင်း တွေ ၊ -ီး -ီး -ီး(-=လ) ပေါ့
ဖင်ရိုက် လိုက် တာ ပရိတ်သတ် အားပေး မှု မ ရှိ ဘူး ဖင်ချ လိုက် ရင် ပို အောင်မြင် နိုင် ပါ တယ်
စောင်နိုင်ငံ ရဲ့ မ ကောင်း တာ က တစ် မျိုး နင် တို့ အပြာကားမိသားစု တွေ က တစ် မျိုး စောင်ကောင် တွေ
ဖော်လော်မော် မ ဟုတ် လို့ ပေါ့ 🤣 🤣
နား ကို မ လည် တာ
ဆောက်မြင်ကပ် ထင် တာ ပဲ
ကွမ်းယာ မှာ ထည့် စား တဲ့ စမုန်စပါး ထင် တယ်
ဖလော်မော် next version
ငါ လည်း သိ ချင် နေ တာ 😁 အဲ့လို စကား တွေ ကျ နားမလည် လို့ သင် ပေး ကြ ပါ ဦး 😂
ငါ မ သိ လို့ ကိုကို့ ကို မေး ကြည့် တာ ကိုကို က လည်း baby က လွဲ ရင် မ သိ ဘူး တဲ့ 🥺
ဖော်လော်မော် နဲ့ ညီမ တော် တယ် လေ 😬
sမွေး ကြီး တဲ့ 😂
$မွှေး ပါ(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$
```

အထက်မှာ တွေ့ရတဲ့အတိုင်းပါပဲ။ မတူတာက နောက်ဆုံး တစ်ကြောင်းက enter မရိုက်ထားတာပဲမို့လို့ debug လုပ်ရတာ လွယ်ခဲ ...  
join လုပ်တဲ့ နေရာမှာ '\n' ကို ထည့်ပေးခဲ့ ...  

```
file.write('\n'.join(cleaned_lines) + '\n')
```

Remake test run ...

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ python ./get_text.py -i small.txt -o small.clean.txt
```

ဒီတခါတော့ filesize တူသွားပါပြီ။  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ wc ./small.txt
  20  261 3316 ./small.txt
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ wc ./small.clean.txt
  20  241 3124 ./small.clean.txt
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$
```

output ဖိုင် တစ်ဖိုင်လုံးကို ရိုက်ထုတ်ပြီး စစ်ကြည့်ခဲ့ ...  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ cat ./small.clean.txt
စဥ်းစား ပြီး မင်း အမေ မင်း လိုး လိုက် ပါ လား
လာ ဟောင် စမ်း ခွေးမသား နဲ့ ခွေးမသမီး တွေ လူကြီး လူငယ် မရွေး မင်းမေလိုး လိုက် တစ် ဖက် သား ကို အား နေ အာခြောင် တဲ့ ဟာ တွေ အချိန် ပြည့် ငါ့ ဆီ က မင်း အမေ ကို လိုး ပဲ 🤏🏻
ကိုယ်လုံးတီး နဲ့ ဆို ပို ပြီး နာမည်ကြီး သွား မယ်
သီချင်း ရိုက် မ နေ နဲ့ ကွာ ဖူးကား ရိုက် လေ မအလ ခေတ် ပဲ နော်
သီချင်း နဲ့ ကောင်မနို့ နဲ့ ကောင်မဖင် နဲ့ ဘာ ဆိုင် လဲ ဟင် မအလ အကြိုက် ရိုက် နေ ကြ တာ ကိုး မအလ တွေ က ဆင်ဆာ မ ဖြတ် ဘူး နော် အိုးကြည့်ကောင်း နေ တာ ကိုး 🤣🤣🤣🤣
pornကားသာရိုက် ကြ ပါ တော့ လား lee အနုပညာ လား 😎
ခွေးရုပ်ပေါက် နေ တာ မိမဆုံးမဖမဆုံးမ သား သမီး တွေ မှန်း သိသာ တယ် 🖕🖕🖕 ဘောပဲ
စောက်ကျက်သရေတုံး ဖက်ရှင် နဲ့ ၊ အ မင်္ဂလာ သီချင်း တွေ ၊ -ီး -ီး -ီး(-=လ) ပေါ့
ဖင်ရိုက် လိုက် တာ ပရိတ်သတ် အားပေး မှု မ ရှိ ဘူး ဖင်ချ လိုက် ရင် ပို အောင်မြင် နိုင် ပါ တယ်
စောင်နိုင်ငံ ရဲ့ မ ကောင်း တာ က တစ် မျိုး နင် တို့ အပြာကားမိသားစု တွေ က တစ် မျိုး စောင်ကောင် တွေ
ဖော်လော်မော် မ ဟုတ် လို့ ပေါ့ 🤣 🤣
နား ကို မ လည် တာ
ဆောက်မြင်ကပ် ထင် တာ ပဲ
ကွမ်းယာ မှာ ထည့် စား တဲ့ စမုန်စပါး ထင် တယ်
ဖလော်မော် next version
ငါ လည်း သိ ချင် နေ တာ 😁 အဲ့လို စကား တွေ ကျ နားမလည် လို့ သင် ပေး ကြ ပါ ဦး 😂
ငါ မ သိ လို့ ကိုကို့ ကို မေး ကြည့် တာ ကိုကို က လည်း baby က လွဲ ရင် မ သိ ဘူး တဲ့ 🥺
ဖော်လော်မော် နဲ့ ညီမ တော် တယ် လေ 😬
sမွေး ကြီး တဲ့ 😂
$မွှေး ပါ
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$
```

testing လုပ်ခဲ့တဲ့ ဖိုင်တွေကို backup ကူးထားခဲ့ ...  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ mkdir cleaning_test
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ mv small* ./cleaning_test/
```

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ ls
bk  cleaning_test  diff_line_identifier.py  get_text.py  hs_data_4Oct2023.txt  print-blank-lines.pl
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$
```

corpus မှာ blank line ရှိမရှိလည်း စစ်ခဲ့ ...  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ perl ./print-blank-lines.pl ./hs_data_4Oct2023.txt
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$
```

အဆင်ပြေမယ်လို့ ထင်တယ်။ corpus တစ်ခုလုံးကို cleaning လုပ်ခဲ့ ...  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ python ./get_text.py -i ./hs_data_4Oct2023.txt -o ./hs_data_4Oct2023.clean.txt
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$
```

Check filesize ...  
ထွက်တဲ့ output ဖိုင်ရဲ့ စာကြောင်းရေအတွက်က input ဖိုင်နဲ့ တူတယ်။ အိုကေတယ်။  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ wc ./{hs_data_4Oct2023,hs_data_4Oct2023.clean}.txt
  10140  181428 2252181 ./hs_data_4Oct2023.txt
  10140  171254 2172104 ./hs_data_4Oct2023.clean.txt
  20280  352682 4424285 total
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$
```
file content ကိုလည်း စစ်ကြည့်ခဲ့ ...  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ paste -d "\n" ./hs_data_4Oct2023.txt ./hs_data_4Oct2023.clean.txt | head
ဖော်လော်မော်/ab မ ဟုတ် လို့ ပေါ့ 🤣 🤣   ab
ဖော်လော်မော် မ ဟုတ် လို့ ပေါ့ 🤣 🤣
နား ကို မ လည် တာ   no
နား ကို မ လည် တာ
ဆောက်မြင်ကပ်/ab ထင် တာ ပဲ    ab
ဆောက်မြင်ကပ် ထင် တာ ပဲ
ကွမ်းယာ မှာ ထည့် စား တဲ့ စမုန်စပါး ထင် တယ် no
ကွမ်းယာ မှာ ထည့် စား တဲ့ စမုန်စပါး ထင် တယ်
ဖလော်မော်/ab next version ab
ဖလော်မော် next version
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$
```

tail command နဲ့ စာကြောင်းရေ တော်တော်များများကို print လုပ်ပြီး အကြမ်းစစ်ခဲ့ ...  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ paste -d "\n" ./hs_data_4Oct2023.txt ./hs_data_4Oct2023.clean.txt | tail -n 30 
အော် သူ က လူ လား ကျွန်/ab လား ဘောမ/ab လား 😁 ab
အော် သူ က လူ လား ကျွန် လား ဘောမ လား 😁
စပ/ab အဲ့ လောက် ပဲ ပြော မယ်  ab
စပ အဲ့ လောက် ပဲ ပြော မယ်
ဘာ မ ဟုတ် တာ နဲ့ တဲ့ လား zb/ab 🤌🏻 ကောင်မ/ab အသေလေးမွေးလာရမှာ/le 🖕 ထာ၀ရ ပေလိုးမ/ab ပါ လို့ 🖕 ခု လည်း ဆဲ/ab မှာ နောင် လည်း ဆက် ဆဲ/ab နေ ဦး မှာ ပါ 🤌🏻 ဖော်လော်မော်/ab သော်ဒေါ်စော်/ab အားတန်းစောက်မ/ab 🖕🖕🤬🤬  ab
ဘာ မ ဟုတ် တာ နဲ့ တဲ့ လား zb 🤌🏻 ကောင်မ အသေလေးမွေးလာရမှာ 🖕 ထာ၀ရ ပေလိုးမ ပါ လို့ 🖕 ခု လည်း ဆဲ မှာ နောင် လည်း ဆက် ဆဲ နေ ဦး မှာ ပါ 🤌🏻 ဖော်လော်မော် သော်ဒေါ်စော် အားတန်းစောက်မ 🖕🖕🤬🤬
ပြော လည်း နာ မှာ မ ဟုတ် ပါ ဘူး အရေထူ နေ တဲ့ စောက်ခွက်/ab|bo နဲ့      ab
ပြော လည်း နာ မှာ မ ဟုတ် ပါ ဘူး အရေထူ နေ တဲ့ စောက်ခွက် နဲ့
ဖြစ် နေ တဲ့ ပြဿနာ ကို နားမလည် ဘူး ဆို တဲ့ ဥာဏ်ရည်မမှီ/ed တဲ့ နင့် ကို တောင်ဘက်ပန်းခြံ/ab ပဲ လို ပြော ချင် တာ ပါ ပဲ    ed
ဖြစ် နေ တဲ့ ပြဿနာ ကို နားမလည် ဘူး ဆို တဲ့ ဥာဏ်ရည်မမှီ တဲ့ နင့် ကို တောင်ဘက်ပန်းခြံ ပဲ လို ပြော ချင် တာ ပါ ပဲ
သူ့ ကို ဘာ ကြည့် ပြီး vote ပေး ကြ တာ ပါ လိမ့် $ရူးမ/ab ဘာ မ ဟုတ် တဲ့ ကိစ္စ ကြောင့် ရွှေကြို အခွင့်အရေး ကို ဆုံးရှုံး မ ခံ နိုင် လို့ ဆို ပြီး ပြော တဲ့ $ရူးမ/ab       ab
သူ့ ကို ဘာ ကြည့် ပြီး vote ပေး ကြ တာ ပါ လိမ့် $ရူးမ ဘာ မ ဟုတ် တဲ့ ကိစ္စ ကြောင့် ရွှေကြို အခွင့်အရေး ကို ဆုံးရှုံး မ ခံ နိုင် လို့ ဆို ပြီး ပြော တဲ့ $ရူးမ
ဖင်အရှည်ကြီးခံလိုက်/ab တစ်ခါတည်း အကုန် ကြို ပြီး သား ပဲ 🦭      ab
ဖင်အရှည်ကြီးခံလိုက် တစ်ခါတည်း အကုန် ကြို ပြီး သား ပဲ 🦭
အိပ်မက် က အမ တစ် ယောက် ပဲ ရှိ တာ လား 🥲 no
အိပ်မက် က အမ တစ် ယောက် ပဲ ရှိ တာ လား 🥲
SattPatt/ab !! ဘာ မ ဟုတ် တဲ့ ပြဿနာ တဲ့ PayloeeeMaaaGGG/ab     ab
SattPatt !! ဘာ မ ဟုတ် တဲ့ ပြဿနာ တဲ့ PayloeeeMaaaGGG
စောက်ဆင့်မရှိ/ab တဲ့ ဟာ တွေ က လည်း အခုတလော ခပ်စိပ်စိပ် တွေ့ လာ ရ တယ် 🤣🤣🤣🤣🤣 ရေး ချင် လွန်း လို့ မ ဟုတ် ဘူး နော် ရှက် တတ် ဦး မ လား လို့ ဝင့် မန့် တာ       ab
စောက်ဆင့်မရှိ တဲ့ ဟာ တွေ က လည်း အခုတလော ခပ်စိပ်စိပ် တွေ့ လာ ရ တယ် 🤣🤣🤣🤣🤣 ရေး ချင် လွန်း လို့ မ ဟုတ် ဘူး နော် ရှက် တတ် ဦး မ လား လို့ ဝင့် မန့် တာ
ဘာ မ ဟုတ် တာ လေး တဲ့ အာ့ ဆို ဟုတ် တဲ့ ဟာ ဘောပဲမနေ/ab နော် အမကြီး      ab
ဘာ မ ဟုတ် တာ လေး တဲ့ အာ့ ဆို ဟုတ် တဲ့ ဟာ ဘောပဲမနေ နော် အမကြီး
ထမင်းစားတိုင်းလူမဖြစ်နိုင်ဘူး/ab ဆို တာ ခု မှ အရှင်လတ်လတ် မြင် ဖူး တော့ တယ် ကောင်မ/ab မွေးကတည်းကအသေလေးမွေးလာရမှာ/le        le
ထမင်းစားတိုင်းလူမဖြစ်နိုင်ဘူး ဆို တာ ခု မှ အရှင်လတ်လတ် မြင် ဖူး တော့ တယ် ကောင်မ မွေးကတည်းကအသေလေးမွေးလာရမှာ
အော် ဘာ မ ဟုတ် တာ တဲ့ လား ပြောထွက်တဲ့ပါးစပ်လေးကိုအက်ဆစ်လေးနဲ့သွားဆေးစေချင်/ab     ab
အော် ဘာ မ ဟုတ် တာ တဲ့ လား ပြောထွက်တဲ့ပါးစပ်လေးကိုအက်ဆစ်လေးနဲ့သွားဆေးစေချင်
ဗန်းကိုင် နဲ့ မအလ/ab|po ဘောကိုင်/ab      ab
ဗန်းကိုင် နဲ့ မအလ ဘောကိုင်
စိတ်မပူ နဲ့ ရွှေကြို ပြီး ရင် ဖင်ခံ/ab ရ မှာ ညီမလေး fighting 22 နှစ် က ငါ 25 နှစ် ထက် အို/bo နေ တော့ အား တောင် နာ တယ် 😂 😂      bo
စိတ်မပူ နဲ့ ရွှေကြို ပြီး ရင် ဖင်ခံ ရ မှာ ညီမလေး fighting 22 နှစ် က ငါ 25 နှစ် ထက် အို နေ တော့ အား တောင် နာ တယ် 😂 😂
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$
```

အထက်ပါ output ကို ကြည့်တော့ အမှားမတွေ့ရ ... 

egrep command နဲ့ hatespeech tag တွေကို ဆွဲထုတ်ပြီး confirmation လုပ်ခဲ့တော့လည်း အောက်ပါ output ကိုရတယ်။ ကြည့်ကြည့်သ၍တော့ cleaning process က အဆင်ပြေတယ်လို့ ယူဆပါတယ်။  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ egrep -E 'ab|ra|re|le|po|se|ed|co|bo|no' ./hs_data_4Oct2023.clean.txt | head   ငါ မ သိ လို့ ကိုကို့ ကို မေး ကြည့် တာ ကိုကို က လည်း baby က လွဲ ရင် မ သိ ဘူး တဲ့ 🥺
ရင် ထဲ က နေ နှစ်နှစ်ကာကာ ထာဝရ အားပေး နေ မှာ ပါ ဆဲ ကြ တဲ့ comment တွေ ကို
သူများ လောက် စောက်ဖြစ် မ ရှိ တဲ့ ကောင် တွေ ကောင်မ တွေ comment ထဲ မှာ တစ် ပုံ ကြီး ပဲ အား နေ ထိုင် blame နေ တယ် မင်း တို့ မ ကြိုက် ရင် မ ကြည့် နဲ့ ပေါ့ ရှင်းရှင်း လေး ရယ် ၊ မမစပ ငါလိုးမသား တွေ ငါလိုးမသမီး တွေ စောက်အာခြောင် တဲ့ ပါးစပ် တွေ တစ် နေ့ လူ စု ပြီး လီး နဲ့ ဖြဲထိုး ဦး မယ်
တော်တော် ကောင်း ပါ တယ် telegram ထဲ ရောက် သွား သလို ပဲ 😬
ဘာ သီချင်း ဆို သွား မှန်း မ သိ သလို ဘာ အတွက် ဘယ်လို ဘယ်လို သီကုံး ရေး စပ် ပြီး ဘယ်လို ပဲ သရုပ်ဆောင် လုပ် သွား ကြ ပါ စေ ကိုယ် တွေ အမြင် နဲ့ က တော့ သူ့ ရှေ့ က rapper ဘိုးအေ တွေ တောင် အဲ့ လောက် ထိ သရုပ်ဖော် မ ရိုင်းစိုင်း ခဲ့ ကြ ဘူး နိုင်ငံခြား က သရုပ်ဖော် ပုံ တွေ ကို တိုက်ရိုက် ခိုးချ တော့ မြန်မာ အမြင် နဲ့ ကြည့် ရင် မိမဆုံးမဖမဆုံးမ သား သမီး တွေ အထိန်းကွပ် မဲ့ နေ သလို ခံစား ရ တယ် ..
ဝတ် ထား တာ တွေ မိုက် တယ် Camera color ပဲ ကြောင်စီစီ ဖြစ် နေ တာ
pornကားသာရိုက် ကြ ပါ တော့ လား lee အနုပညာ လား 😎
ဟုတ်ကဲ့ ဒီ mv ထွက် ပြီး ၅၀၅ က နဲ့ အဖမ်းခံ ရ ပြီး ပါ ပြီ ပေးဆပ် ပြီး ပါ ပြီ ထောင် ထဲ မှာ လည်း ခွေးလိုနေ ခဲ့ ရ ပါ တယ် အခု ပြန် လွတ် လာ တာ မ ကြာ သေး လို့ အနုပညာ အလုပ် တွေ ပြန် လုပ် ပြီး စိတ် ကို relax လုပ် နေ တာ ပါ ပြန် အဖမ်းခံ စေ ချင် တာ လား ??? ကျွန်တော် တို့ ပေးဆပ် ရ တာ ကော တန် လား ????
lee ပဲ လုံးဝ ခံစား လို့ မ ရ ဘူး
ဖင်ကုန်းပြ ပြီး ပရိသတ် ကို respect ဖြစ် ရ သေး
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$
```

သေချာအောင် output file ကို shuffle လုပ်ပြီး head command နဲ့ ထပ်စစ်ကြည့်ခဲ့ ...  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ shuf ./hs_data_4Oct2023.clean.txt | head
Sp လန့် တာ mtm
အသံကိုကpharသံ 🤣🤣🤣
အမလေး စောက်ပြဿနာ က လည်း မ ပြီး တော့ ဘူး ဒိုင် ဆို တဲ့ ဟာ တွေ က လည်း ပြော လို့ ကို မ ပြီး နိုင် တော့ ဘူး
တောသား တွေ သောက်ပေါကား တွေ နဲ့ ပဲ တန် တယ်
မီး ပျက် ရင် ဝင် မ စား ကြ ပါ နဲ့ ဆိုင်ကြီး ဖြစ် ပြီး မီးစက် မ နှိုး ဘူး မေး တော့ ခဏ နေ နှုိး ပေး မှာ ဆို ပြီး လိမ် သေး တာ ပြီး တော့ သူ တို့ တောင် မ နေ နိုင် အပြင် ထွက် ထိုင် နေ တယ် ဆိုင် လာ စား တဲ့ သူ က ချွေးထုတ်ခန်း ရောက် နေ သလို ပဲ အဲ့ ကတည်းက မ စား တော့ တာ 🙂
ဗမာ ဗုဒ္ဓ ဟုတ် တယ် အဲ့ စကား ကြား တာ နဲ့ ဆောင့်ထိုး ချင် တာ
မသန္ဒာလှိုင် ပြော တာ ဘောင်ဝင် တယ် စကားလုံး တွေ က ဇင်အောင် ဂန်ဒူး မှ ဘာ တွေ ပြော နေ မှန်း မ သိ ဖြတ် ပြော မယ် ငါ မှန် တယ် ဆို တာ ချည်း ပဲ
လာ ကြည့် ဦး ပွဲ တွေ ဆို ss တွေ ဖတ် ပြီး စိတ်တို ရ တာ ဒါ က သူများ တော့ မ သိ ငါ နဲ့ တရုတ်ကြီး တော့ အူ တွေ တက် နေ ရော ကျပ်မပြည့် ဘူး လား မ သိ ဘူး ဟဲ့ 🤣
အာဆီယံ နိုင်ငံ မှန် သမျှ အာဏာရှင် စနစ် အမြစ်တွယ် နေ တုန်း ပဲ တော်တော် ဆိုး တာ နဲ့ သိပ် မ ဆိုး တာ ပဲ ရှိ တယ်
ရူး ခဲ့ တယ် အခု တော့ အချစ် က ဘဝ ကြီး မ ဟုတ် မှန်း နားလည် လာ ပြီ
```

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ shuf ./hs_data_4Oct2023.clean.txt | head
၇၂ နာရီ ပဲ စောင့် ပါ 😂
အေး သမီးလေး အပေါ် မှာ တစ် ပိုင်း ရှိ သေး တယ် 😊
ဗိုင်းဒါမ
ကျွန်တော့် ဆီ မှာ ပန်းတိမ် လာ သင် ပါ လား မင်းသမီး ရယ် အလုပ် မ ရှိ ဘူး ဆို တော့ သနား ပါ တယ် နော် စ သင် တဲ့ နေ့ အလုပ် စ ဝင် တာ နဲ့ တစ် ရက် ကို ၁၀၀၀၀ တော့ ပေး နိုင် ပါ တယ် နော် 😂 😂 😂
ဘယ် ဘုရား မှ မ ဟုတ် ဘူး အရူး တွေ သာသနာ မ ကုန် ဘဲ နဲ့ ဘုရားလောင်း မ ပေါ် ဘူး တဲ့
အင်တာဗျူး ဖြေ တာ နားထောင် ခါ မှ မြန်မာ မှန်း သိ တဲ့ ငါ့ အဖြစ် 😄 😄
နင့် sခွက် ကို မ ကြည့် ချင် ဘူး 😏
ဂေါပက ပါ ဝင် လုပ် ပြီး ဘုရား ငွေ လည်း နည်း ပေါင်းစုံ နဲ့ ခိုး တတ် ပါ တယ် ဗျ ၊ ဘုရားစောင်းတန်း က နှစ် ရာ တန် ပန်းစည်း ကို နှစ် ထောင် တင် ရောင်း နေ တာ လည်း ဒီ ကောင် တွေ သောက်မျိုး တွေ ချည်း ပဲ ဗျ
အမ က ရော အမ ပထွေး ထိ လို့ အောက်တန်းစား လို ရန် တွေ့ နေ တာ လား
လူ တွေ ရော ဟုတ် ကြ ရဲ့ လား မ သိ ထမင်း မ စား ဘဲ ချေးတွေစား နေ တဲ့ သူ တွေ ဖြစ် မယ် လာ ပါ ဦး မယ် ဖြေရှင်း ချက် တွေ မနာလို လို့ တိုက်ခိုက် တာ ပါ ဘာညာသာရကာ နေကြာ ၊ ကွာစိ ပေါ့
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$

```

လက်ရှိ ဒေတာမှာတော့ emoji တွေတော့ ပါတယ်။ အဲဒီအတိုင်းပဲ experiment လုပ်ဖို့ ဆုံးဖြတ်ခဲ့ ...  

## Preparing Training/Validation File

I made small modification of the original prepare-my-char.py code as follows:  

```python
"""
Prepare the Burmese hatespeech dataset for character-level language modeling.
So instead of encoding with GPT-2 BPE tokens, we just map characters to ints.
Will save train.bin, val.bin containing the ids, and meta.pkl containing the
encoder and decoder and some other related info.
"""
import os
import pickle
import requests
import numpy as np

# assign hatespeech corpus file
input_file_path = os.path.join(os.path.dirname(__file__), 'hs_data_4Oct2023.clean.txt')

# the following code is just for reference
#if not os.path.exists(input_file_path):
#    data_url = 'https://raw.githubusercontent.com/karpathy/char-rnn/master/data/tinyshakespeare/input.txt'
#    with open(input_file_path, 'w') as f:
#        f.write(requests.get(data_url).text)

with open(input_file_path, 'r') as f:
    data = f.read()
print(f"length of dataset in characters: {len(data):,}")

# get all the unique characters that occur in this text
chars = sorted(list(set(data)))
vocab_size = len(chars)
print("all the unique characters:", ''.join(chars))
print(f"vocab size: {vocab_size:,}")

# create a mapping from characters to integers
stoi = { ch:i for i,ch in enumerate(chars) }
itos = { i:ch for i,ch in enumerate(chars) }
def encode(s):
    return [stoi[c] for c in s] # encoder: take a string, output a list of integers
def decode(l):
    return ''.join([itos[i] for i in l]) # decoder: take a list of integers, output a string

# create the train and test splits
n = len(data)
train_data = data[:int(n*0.9)]
val_data = data[int(n*0.9):]

# encode both to integers
train_ids = encode(train_data)
val_ids = encode(val_data)
print(f"train has {len(train_ids):,} tokens")
print(f"val has {len(val_ids):,} tokens")

# export to bin files
train_ids = np.array(train_ids, dtype=np.uint16)
val_ids = np.array(val_ids, dtype=np.uint16)
train_ids.tofile(os.path.join(os.path.dirname(__file__), 'train.bin'))
val_ids.tofile(os.path.join(os.path.dirname(__file__), 'val.bin'))

# save the meta information as well, to help us encode/decode later
meta = {
    'vocab_size': vocab_size,
    'itos': itos,
    'stoi': stoi,
}
with open(os.path.join(os.path.dirname(__file__), 'meta.pkl'), 'wb') as f:
    pickle.dump(meta, f)

```

Running of prepare-my-char.py as follows ...  

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ time python ./prepare-my-char.py
length of dataset in characters: 844,288
all the unique characters:
 !"$%'()*+,-.0123456789:=?ABCDEFGHIJKLMNOPQRSTUVWXYZ_abcdefghijklmnopqrstuvwxyz§×ကခဂဃငစဆဇဈဉညဋဌဍဏတထဒဓနပဖဗဘမယရလဝသဟဠအဣဤဥဦဧဩဪါာိီုူေဲံ့း္်ျြွှဿ၀၁၂၃၄၅၆၇၈၉၊။၍၏​‌‍‘’“”…⁠☝☠☹☺♀♂♥⚽⛔✅✋✌✍❔❤️🌚🌝🌷🌹🍆🍑🍵🍺🎃🎵🏻🏼🏿🐄🐕🐮👀👂👈👉👊👋👌👍👎👏👐👣👲👹👺👻👽👿💀💔💗💛💜💡💣💥💦💨💩💪💿📦🔥🔪🔫🖐🖕🗿😀😁😂😃😄😅😆😇😈😉😊😋😌😍😎😏😐😑😒😓😔😕😖😗😘😙😚😛😜😝😞😟😠😡😢😣😤😥😦😧😩😪😫😬😭😮😯😰😱😳😵😶😷😹🙁🙂🙃🙄🙅🙈🙉🙊🙌🙏🤌🤍🤏🤐🤑🤒🤓🤔🤕🤖🤗🤝🤡🤢🤣🤥🤦🤧🤨🤩🤪🤫🤬🤭🤮🥰🥱🥲🥳🥴🥵🥶🥸🥹🥺🦭🦮🦴🦺🫠🫡🫢🫣🫤🫰🫶
vocab size: 343
train has 759,859 tokens
val has 84,429 tokens

real    0m0.431s
user    0m0.338s
sys     0m0.059s
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$
```

Check the bin files ... 

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ wc train.bin
    139     594 1519718 train.bin
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$
```
Check the val.bin file ... 

```
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$ wc val.bin
    11    100 168858 val.bin
(base) yekyaw.thu@gpu:~/exp/myHatespeech/data$
```

ဒေတာ ပြင်ဆင်တာတော့ ပြီးသွားပြီ၊ ပြီးရင် configuration ဖိုင်ကို ပြင်ရမယ်။ အရင်ဆုံး nanoGPT clone လုပ်ထားတဲ့ path ကိုသွားပြီး လေ့လာခဲ့ ...  

```
(base) yekyaw.thu@gpu:~/tool/nanoGPT$ ls
assets    config           data     model.py   sample.py           train.py
bench.py  configurator.py  LICENSE  README.md  scaling_laws.ipynb  transformer_sizing.ipynb
(base) yekyaw.thu@gpu:~/tool/nanoGPT$
```

data/ အောက်မှာ လက်ရှိ run ချင်တဲ့ hatespeech နဲ့ ဆိုင်တဲ့ ဖိုင်တွေအားလုံးကို ကူးယူခဲ့။ တကယ်က train.bin, val.bin, meta.pkl သုံးဖိုင်ကိုပဲ ကူးရင် လုံလောက်တယ်လို့ ထင်ပေမဲ့ ... နောက်ပိုင်း ပြန်ကြည့်ရင် လွယ်အောင်လို့ ကြိုပြင်ထားခဲ့ ...  

```
(base) yekyaw.thu@gpu:~/tool/nanoGPT/data$ mkdir myHatespeech_char
(base) yekyaw.thu@gpu:~/tool/nanoGPT/data$ cd myHatespeech_char/
(base) yekyaw.thu@gpu:~/tool/nanoGPT/data/myHatespeech_char$ cp ~/exp/myHatespeech/data/
bk/                         get_text.py                 meta.pkl                    train.bin
cleaning_test/              hs_data_4Oct2023.clean.txt  prepare-my-char.py          val.bin
diff_line_identifier.py     hs_data_4Oct2023.txt        print-blank-lines.pl
(base) yekyaw.thu@gpu:~/tool/nanoGPT/data/myHatespeech_char$ cp ~/exp/myHatespeech/data/*.bin .
(base) yekyaw.thu@gpu:~/tool/nanoGPT/data/myHatespeech_char$ cp ~/exp/myHatespeech/data/prepare-my-char.py .
(base) yekyaw.thu@gpu:~/tool/nanoGPT/data/myHatespeech_char$ cp ~/exp/myHatespeech/data/hs_data_4Oct2023.clean.txt .
(base) yekyaw.thu@gpu:~/tool/nanoGPT/data/myHatespeech_char$ cp ~/exp/myHatespeech/data/meta.pkl .
```

လက်ရှိ ကူးထည့်ထားတဲ့ ဖိုင်တွေကို ls လုပ်ကြည့်ခဲ့ ...  

```
(base) yekyaw.thu@gpu:~/tool/nanoGPT/data/myHatespeech_char$ ls
hs_data_4Oct2023.clean.txt  meta.pkl  prepare-my-char.py  train.bin  val.bin
(base) yekyaw.thu@gpu:~/tool/nanoGPT/data/myHatespeech_char$
```

Data path for our experiment:  

```
(base) yekyaw.thu@gpu:~/tool/nanoGPT/data/myHatespeech_char$ pwd
/home/yekyaw.thu/tool/nanoGPT/data/myHatespeech_char
```

## Preparing the Config File

Training မလုပ်ခင်မှာ configuration file (filename: train_myHatespeech_char.py) ကိုလည်း ပြင်ဆင်ဖို့ လိုအပ်လို့ ပြင်ခဲ့ ...  

```python
# train a miniature character-level Myanmar Hatepeech model

out_dir = 'out-myHatespeech-char'
eval_interval = 250 # keep frequent because we'll overfit
eval_iters = 200
log_interval = 10 # don't print too too often

# we expect to overfit on this small dataset, so only save when val improves
always_save_checkpoint = False

wandb_log = False # override via command line if you like
wandb_project = 'myHatespeech-char'
wandb_run_name = 'mini-gpt'

dataset = 'myHatespeech_char'
batch_size = 64
block_size = 256 # context of up to 256 previous characters

# baby GPT model :)
n_layer = 6
n_head = 6
n_embd = 384
dropout = 0.2

learning_rate = 1e-3 # with baby networks can afford to go a bit higher
max_iters = 5000
lr_decay_iters = 5000 # make equal to max_iters usually
min_lr = 1e-4 # learning_rate / 10 usually
beta2 = 0.99 # make a bit bigger because number of tokens per iter is small

warmup_iters = 100 # not super necessary potentially

# on macbook also add
# device = 'cpu'  # run on cpu only
# compile = False # do not torch compile the model
```

## Check the Current GPU Status

```
(base) yekyaw.thu@gpu:~/tool/nanoGPT/config$ nvidia-smi
Thu Oct 19 20:33:31 2023
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.199.02   Driver Version: 470.199.02   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:0A:00.0 Off |                  N/A |
| 29%   43C    P0    58W / 300W |      0MiB / 11019MiB |      1%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA GeForce ...  Off  | 00000000:42:00.0 Off |                  N/A |
| 62%   69C    P0    72W / 257W |      0MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  NVIDIA GeForce ...  Off  | 00000000:43:00.0 Off |                  N/A |
| 22%   64C    P0    72W / 250W |      0MiB / 11016MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
(base) yekyaw.thu@gpu:~/tool/nanoGPT/config$
```

လောလောဆယ် run နေတဲ့ process တစ်ခုမှ မရှိလို့ OK တယ်။  

## Training GPT-2 Model with myHatespeech Corpus

Note: I run with character unit ...  

Current Path:  

```
(base) yekyaw.thu@gpu:~/tool/nanoGPT$ pwd
/home/yekyaw.thu/tool/nanoGPT
```

Training command ပေးတော့ အောက်ပါအတိုင်း Error message ရခဲ့ ...  

```
(base) yekyaw.thu@gpu:~/tool/nanoGPT$ time python -m torch.distributed.launch --use-env train.py ./config/train_myHatespeech_char.py | tee train-myHatespeech-char.log
/home/yekyaw.thu/.local/lib/python3.7/site-packages/torch/distributed/launch.py:186: FutureWarning: The module torch.distributed.launch is deprecated
and will be removed in future. Use torchrun.
Note that --use_env is set by default in torchrun.
If your script expects `--local_rank` argument to be set, please
change it to read from `os.environ['LOCAL_RANK']` instead. See
https://pytorch.org/docs/stable/distributed.html#launch-utility for
further instructions

  FutureWarning,
usage: launch.py [-h] [--nnodes NNODES] [--nproc_per_node NPROC_PER_NODE]
                 [--rdzv_backend RDZV_BACKEND] [--rdzv_endpoint RDZV_ENDPOINT]
                 [--rdzv_id RDZV_ID] [--rdzv_conf RDZV_CONF] [--standalone]
                 [--max_restarts MAX_RESTARTS]
                 [--monitor_interval MONITOR_INTERVAL]
                 [--start_method {spawn,fork,forkserver}] [--role ROLE] [-m]
                 [--no_python] [--run_path] [--log_dir LOG_DIR] [-r REDIRECTS]
                 [-t TEE] [--node_rank NODE_RANK] [--master_addr MASTER_ADDR]
                 [--master_port MASTER_PORT] [--use_env]
                 training_script ...
launch.py: error: unrecognized arguments: --use-env

real    0m6.533s
user    0m1.593s
sys     0m0.281s
(base) yekyaw.thu@gpu:~/tool/nanoGPT$

```

Conda environment ကို activate လုပ်ဖို့ မေ့နေလို့ activate လုပ်ပြီး run ကြည့်တော့လည်း အောက်ပါအတိုင်း error message ရခဲ့ ...  

```
(nanoGPT) yekyaw.thu@gpu:~/tool/nanoGPT$ time python -m torch.distributed.launch --use-env train.py ./config/train_myHatespeech_char.py | tee train-myHatespeech-char.log
/home/yekyaw.thu/.conda/envs/nanoGPT/lib/python3.8/site-packages/torch/distributed/launch.py:181: FutureWarning: The module torch.distributed.launch is deprecated
and will be removed in future. Use torchrun.
Note that --use-env is set by default in torchrun.
If your script expects `--local-rank` argument to be set, please
change it to read from `os.environ['LOCAL_RANK']` instead. See
https://pytorch.org/docs/stable/distributed.html#launch-utility for
further instructions

  warnings.warn(
/home/yekyaw.thu/.conda/envs/nanoGPT/lib/python3.8/site-packages/torch/cuda/__init__.py:138: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
Overriding config with ./config/train_myHatespeech_char.py:
# train a miniature character-level Myanmar Hatepeech model

out_dir = 'out-myHatespeech-char'
eval_interval = 250 # keep frequent because we'll overfit
eval_iters = 200
log_interval = 10 # don't print too too often

# we expect to overfit on this small dataset, so only save when val improves
always_save_checkpoint = False

wandb_log = False # override via command line if you like
wandb_project = 'myHatespeech-char'
wandb_run_name = 'mini-gpt'

dataset = 'myHatespeech_char'
batch_size = 64
block_size = 256 # context of up to 256 previous characters

# baby GPT model :)
n_layer = 6
n_head = 6
n_embd = 384
dropout = 0.2

learning_rate = 1e-3 # with baby networks can afford to go a bit higher
max_iters = 5000
lr_decay_iters = 5000 # make equal to max_iters usually
min_lr = 1e-4 # learning_rate / 10 usually
beta2 = 0.99 # make a bit bigger because number of tokens per iter is small

warmup_iters = 100 # not super necessary potentially

# on macbook also add
# device = 'cpu'  # run on cpu only
# compile = False # do not torch compile the model

Traceback (most recent call last):
  File "train.py", line 84, in <module>
    init_process_group(backend=backend)
  File "/home/yekyaw.thu/.conda/envs/nanoGPT/lib/python3.8/site-packages/torch/distributed/c10d_logger.py", line 74, in wrapper
    func_return = func(*args, **kwargs)
  File "/home/yekyaw.thu/.conda/envs/nanoGPT/lib/python3.8/site-packages/torch/distributed/distributed_c10d.py", line 1148, in init_process_group
    default_pg, _ = _new_process_group_helper(
  File "/home/yekyaw.thu/.conda/envs/nanoGPT/lib/python3.8/site-packages/torch/distributed/distributed_c10d.py", line 1279, in _new_process_group_helper
    backend_class = ProcessGroupNCCL(backend_prefix_store, group_rank, group_size, pg_options)
RuntimeError: ProcessGroupNCCL is only supported with GPUs, no GPUs found!
[2023-10-19 20:45:35,890] torch.distributed.elastic.multiprocessing.api: [ERROR] failed (exitcode: 1) local_rank: 0 (pid: 2143781) of binary: /home/yekyaw.thu/.conda/envs/nanoGPT/bin/python
Traceback (most recent call last):
  File "/home/yekyaw.thu/.conda/envs/nanoGPT/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/home/yekyaw.thu/.conda/envs/nanoGPT/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/yekyaw.thu/.conda/envs/nanoGPT/lib/python3.8/site-packages/torch/distributed/launch.py", line 196, in <module>
    main()
  File "/home/yekyaw.thu/.conda/envs/nanoGPT/lib/python3.8/site-packages/torch/distributed/launch.py", line 192, in main
    launch(args)
  File "/home/yekyaw.thu/.conda/envs/nanoGPT/lib/python3.8/site-packages/torch/distributed/launch.py", line 177, in launch
    run(args)
  File "/home/yekyaw.thu/.conda/envs/nanoGPT/lib/python3.8/site-packages/torch/distributed/run.py", line 797, in run
    elastic_launch(
  File "/home/yekyaw.thu/.conda/envs/nanoGPT/lib/python3.8/site-packages/torch/distributed/launcher/api.py", line 134, in __call__
    return launch_agent(self._config, self._entrypoint, list(args))
  File "/home/yekyaw.thu/.conda/envs/nanoGPT/lib/python3.8/site-packages/torch/distributed/launcher/api.py", line 264, in launch_agent
    raise ChildFailedError(
torch.distributed.elastic.multiprocessing.errors.ChildFailedError:
============================================================
train.py FAILED
------------------------------------------------------------
Failures:
  <NO_OTHER_FAILURES>
------------------------------------------------------------
Root Cause (first observed failure):
[0]:
  time      : 2023-10-19_20:45:35
  host      : gpu.cadt.edu.kh
  rank      : 0 (local_rank: 0)
  exitcode  : 1 (pid: 2143781)
  error_file: <N/A>
  traceback : To enable traceback see: https://pytorch.org/docs/stable/elastic/errors.html
============================================================

real    0m8.606s
user    0m4.174s
sys     0m2.694s
(nanoGPT) yekyaw.thu@gpu:~/tool/nanoGPT$

```

## Check PyTorch

Check torch version ...  

```
(nanoGPT) yekyaw.thu@gpu:~/tool/nanoGPT$ python
Python 3.8.18 (default, Sep 11 2023, 13:40:15)
[GCC 11.2.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import torch
>>> print(torch.__version__)
2.1.0+cu121
>>> exit()
(nanoGPT) yekyaw.thu@gpu:~/tool/nanoGPT$
```

Check GPU is available or not ...  

```
(nanoGPT) yekyaw.thu@gpu:~/tool/nanoGPT$ python
Python 3.8.18 (default, Sep 11 2023, 13:40:15)
[GCC 11.2.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import torch
>>> torch.cuda.is_available()
/home/yekyaw.thu/.conda/envs/nanoGPT/lib/python3.8/site-packages/torch/cuda/__init__.py:138: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
False
>>>

```

Checked on LST Server:  

```
(base) ye@lst-gpu-3090:~$ python
Python 3.9.12 (main, Apr  5 2022, 06:56:58)
[GCC 7.5.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import torch
>>> torch.cuda.is_available()
True
```

## Preparation on LST Server

Create new env ...  

```
(base) ye@lst-gpu-3090:~$ conda create --name nanoGPT python=3.8
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.12.0
  latest version: 23.9.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/ye/anaconda3/envs/nanoGPT

  added / updated specs:
    - python=3.8


The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-5.1-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2023.08.22-h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.38-h1181459_1
  libffi             pkgs/main/linux-64::libffi-3.4.4-h6a678d5_0
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-11.2.0-h1234567_1
  libgomp            pkgs/main/linux-64::libgomp-11.2.0-h1234567_1
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-11.2.0-h1234567_1
  ncurses            pkgs/main/linux-64::ncurses-6.4-h6a678d5_0
  openssl            pkgs/main/linux-64::openssl-3.0.11-h7f8727e_2
  pip                pkgs/main/linux-64::pip-23.3-py38h06a4308_0
  python             pkgs/main/linux-64::python-3.8.18-h955ad1f_0
  readline           pkgs/main/linux-64::readline-8.2-h5eee18b_0
  setuptools         pkgs/main/linux-64::setuptools-68.0.0-py38h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.41.2-h5eee18b_0
  tk                 pkgs/main/linux-64::tk-8.6.12-h1ccaba5_0
  wheel              pkgs/main/linux-64::wheel-0.41.2-py38h06a4308_0
  xz                 pkgs/main/linux-64::xz-5.4.2-h5eee18b_0
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate nanoGPT
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) ye@lst-gpu-3090:~$ conda activate nanoGPT
(nanoGPT) ye@lst-gpu-3090:~$
```

nanoGPT နဲ့ run ဖို့အတွက် လိုအပ်တဲ့ python library တွေကို install လုပ်ခဲ့ ...  

```
(nanoGPT) ye@lst-gpu-3090:~/tool$ pip install torch numpy transformers datasets tiktoken wandb tqdm
Collecting torch
  Using cached torch-2.1.0-cp38-cp38-manylinux1_x86_64.whl.metadata (25 kB)
Collecting numpy
  Using cached numpy-1.24.4-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (5.6 kB)
Collecting transformers
  Downloading transformers-4.34.1-py3-none-any.whl.metadata (121 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 121.5/121.5 kB 664.9 kB/s eta 0:00:00
Collecting datasets
  Downloading datasets-2.14.5-py3-none-any.whl.metadata (19 kB)
Collecting tiktoken
  Downloading tiktoken-0.5.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (6.6 kB)
Collecting wandb
  Downloading wandb-0.15.12-py3-none-any.whl.metadata (9.8 kB)
Collecting tqdm
  Downloading tqdm-4.66.1-py3-none-any.whl.metadata (57 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 57.6/57.6 kB 852.3 kB/s eta 0:00:00
Collecting filelock (from torch)
  Using cached filelock-3.12.4-py3-none-any.whl.metadata (2.8 kB)
Collecting typing-extensions (from torch)
  Using cached typing_extensions-4.8.0-py3-none-any.whl.metadata (3.0 kB)
Collecting sympy (from torch)
  Using cached sympy-1.12-py3-none-any.whl (5.7 MB)
Collecting networkx (from torch)
  Using cached networkx-3.1-py3-none-any.whl (2.1 MB)
Collecting jinja2 (from torch)
  Using cached Jinja2-3.1.2-py3-none-any.whl (133 kB)
Collecting fsspec (from torch)
  Using cached fsspec-2023.9.2-py3-none-any.whl.metadata (6.7 kB)
Collecting nvidia-cuda-nvrtc-cu12==12.1.105 (from torch)
  Using cached nvidia_cuda_nvrtc_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (23.7 MB)
Collecting nvidia-cuda-runtime-cu12==12.1.105 (from torch)
  Using cached nvidia_cuda_runtime_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (823 kB)
Collecting nvidia-cuda-cupti-cu12==12.1.105 (from torch)
  Using cached nvidia_cuda_cupti_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (14.1 MB)
Collecting nvidia-cudnn-cu12==8.9.2.26 (from torch)
  Using cached nvidia_cudnn_cu12-8.9.2.26-py3-none-manylinux1_x86_64.whl.metadata (1.6 kB)
Collecting nvidia-cublas-cu12==12.1.3.1 (from torch)
  Using cached nvidia_cublas_cu12-12.1.3.1-py3-none-manylinux1_x86_64.whl (410.6 MB)
Collecting nvidia-cufft-cu12==11.0.2.54 (from torch)
  Using cached nvidia_cufft_cu12-11.0.2.54-py3-none-manylinux1_x86_64.whl (121.6 MB)
Collecting nvidia-curand-cu12==10.3.2.106 (from torch)
  Using cached nvidia_curand_cu12-10.3.2.106-py3-none-manylinux1_x86_64.whl (56.5 MB)
Collecting nvidia-cusolver-cu12==11.4.5.107 (from torch)
  Using cached nvidia_cusolver_cu12-11.4.5.107-py3-none-manylinux1_x86_64.whl (124.2 MB)
Collecting nvidia-cusparse-cu12==12.1.0.106 (from torch)
  Using cached nvidia_cusparse_cu12-12.1.0.106-py3-none-manylinux1_x86_64.whl (196.0 MB)
Collecting nvidia-nccl-cu12==2.18.1 (from torch)
  Using cached nvidia_nccl_cu12-2.18.1-py3-none-manylinux1_x86_64.whl (209.8 MB)
Collecting nvidia-nvtx-cu12==12.1.105 (from torch)
  Using cached nvidia_nvtx_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (99 kB)
Collecting triton==2.1.0 (from torch)
  Using cached triton-2.1.0-0-cp38-cp38-manylinux2014_x86_64.manylinux_2_17_x86_64.whl.metadata (1.3 kB)
Collecting nvidia-nvjitlink-cu12 (from nvidia-cusolver-cu12==11.4.5.107->torch)
  Using cached nvidia_nvjitlink_cu12-12.2.140-py3-none-manylinux1_x86_64.whl.metadata (1.5 kB)
Collecting huggingface-hub<1.0,>=0.16.4 (from transformers)
  Downloading huggingface_hub-0.18.0-py3-none-any.whl.metadata (13 kB)
Collecting packaging>=20.0 (from transformers)
  Using cached packaging-23.2-py3-none-any.whl.metadata (3.2 kB)
Collecting pyyaml>=5.1 (from transformers)
  Downloading PyYAML-6.0.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (2.1 kB)
Collecting regex!=2019.12.17 (from transformers)
  Downloading regex-2023.10.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (40 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 40.9/40.9 kB 328.6 kB/s eta 0:00:00
Collecting requests (from transformers)
  Downloading requests-2.31.0-py3-none-any.whl.metadata (4.6 kB)
Collecting tokenizers<0.15,>=0.14 (from transformers)
  Downloading tokenizers-0.14.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (6.7 kB)
Collecting safetensors>=0.3.1 (from transformers)
  Downloading safetensors-0.4.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (3.8 kB)
Collecting pyarrow>=8.0.0 (from datasets)
  Downloading pyarrow-13.0.0-cp38-cp38-manylinux_2_28_x86_64.whl.metadata (3.0 kB)
Collecting dill<0.3.8,>=0.3.0 (from datasets)
  Downloading dill-0.3.7-py3-none-any.whl.metadata (9.9 kB)
Collecting pandas (from datasets)
  Using cached pandas-2.0.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (18 kB)
Collecting xxhash (from datasets)
  Downloading xxhash-3.4.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (12 kB)
Collecting multiprocess (from datasets)
  Downloading multiprocess-0.70.15-py38-none-any.whl.metadata (7.1 kB)
Collecting fsspec (from torch)
  Downloading fsspec-2023.6.0-py3-none-any.whl.metadata (6.7 kB)
Collecting aiohttp (from datasets)
  Downloading aiohttp-3.8.6-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (7.7 kB)
Collecting Click!=8.0.0,>=7.1 (from wandb)
  Downloading click-8.1.7-py3-none-any.whl.metadata (3.0 kB)
Collecting GitPython!=3.1.29,>=1.0.0 (from wandb)
  Downloading GitPython-3.1.40-py3-none-any.whl.metadata (12 kB)
Collecting psutil>=5.0.0 (from wandb)
  Downloading psutil-5.9.6-cp36-abi3-manylinux_2_12_x86_64.manylinux2010_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (21 kB)
Collecting sentry-sdk>=1.0.0 (from wandb)
  Downloading sentry_sdk-1.32.0-py2.py3-none-any.whl.metadata (9.8 kB)
Collecting docker-pycreds>=0.4.0 (from wandb)
  Downloading docker_pycreds-0.4.0-py2.py3-none-any.whl (9.0 kB)
Collecting pathtools (from wandb)
  Downloading pathtools-0.1.2.tar.gz (11 kB)
  Preparing metadata (setup.py) ... done
Collecting setproctitle (from wandb)
  Downloading setproctitle-1.3.3-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (9.9 kB)
Requirement already satisfied: setuptools in /home/ye/anaconda3/envs/nanoGPT/lib/python3.8/site-packages (from wandb) (68.0.0)
Collecting appdirs>=1.4.3 (from wandb)
  Downloading appdirs-1.4.4-py2.py3-none-any.whl (9.6 kB)
Collecting protobuf!=4.21.0,<5,>=3.12.0 (from wandb)
  Downloading protobuf-4.24.4-cp37-abi3-manylinux2014_x86_64.whl.metadata (540 bytes)
Collecting six>=1.4.0 (from docker-pycreds>=0.4.0->wandb)
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Collecting attrs>=17.3.0 (from aiohttp->datasets)
  Downloading attrs-23.1.0-py3-none-any.whl (61 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 61.2/61.2 kB 915.1 kB/s eta 0:00:00
Collecting charset-normalizer<4.0,>=2.0 (from aiohttp->datasets)
  Downloading charset_normalizer-3.3.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (32 kB)
Collecting multidict<7.0,>=4.5 (from aiohttp->datasets)
  Downloading multidict-6.0.4-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (121 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 121.3/121.3 kB 1.7 MB/s eta 0:00:00
Collecting async-timeout<5.0,>=4.0.0a3 (from aiohttp->datasets)
  Downloading async_timeout-4.0.3-py3-none-any.whl.metadata (4.2 kB)
Collecting yarl<2.0,>=1.0 (from aiohttp->datasets)
  Downloading yarl-1.9.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (266 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 266.9/266.9 kB 2.0 MB/s eta 0:00:00
Collecting frozenlist>=1.1.1 (from aiohttp->datasets)
  Downloading frozenlist-1.4.0-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (5.2 kB)
Collecting aiosignal>=1.1.2 (from aiohttp->datasets)
  Downloading aiosignal-1.3.1-py3-none-any.whl (7.6 kB)
Collecting gitdb<5,>=4.0.1 (from GitPython!=3.1.29,>=1.0.0->wandb)
  Downloading gitdb-4.0.10-py3-none-any.whl (62 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 62.7/62.7 kB 626.6 kB/s eta 0:00:00
Collecting idna<4,>=2.5 (from requests->transformers)
  Downloading idna-3.4-py3-none-any.whl (61 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 61.5/61.5 kB 589.8 kB/s eta 0:00:00
Collecting urllib3<3,>=1.21.1 (from requests->transformers)
  Downloading urllib3-2.0.7-py3-none-any.whl.metadata (6.6 kB)
Collecting certifi>=2017.4.17 (from requests->transformers)
  Downloading certifi-2023.7.22-py3-none-any.whl.metadata (2.2 kB)
Collecting huggingface-hub<1.0,>=0.16.4 (from transformers)
  Downloading huggingface_hub-0.17.3-py3-none-any.whl.metadata (13 kB)
Collecting MarkupSafe>=2.0 (from jinja2->torch)
  Using cached MarkupSafe-2.1.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (3.0 kB)
Collecting python-dateutil>=2.8.2 (from pandas->datasets)
  Using cached python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
Collecting pytz>=2020.1 (from pandas->datasets)
  Using cached pytz-2023.3.post1-py2.py3-none-any.whl.metadata (22 kB)
Collecting tzdata>=2022.1 (from pandas->datasets)
  Using cached tzdata-2023.3-py2.py3-none-any.whl (341 kB)
Collecting mpmath>=0.19 (from sympy->torch)
  Using cached mpmath-1.3.0-py3-none-any.whl (536 kB)
Collecting smmap<6,>=3.0.1 (from gitdb<5,>=4.0.1->GitPython!=3.1.29,>=1.0.0->wandb)
  Downloading smmap-5.0.1-py3-none-any.whl.metadata (4.3 kB)
Using cached torch-2.1.0-cp38-cp38-manylinux1_x86_64.whl (670.2 MB)
Using cached nvidia_cudnn_cu12-8.9.2.26-py3-none-manylinux1_x86_64.whl (731.7 MB)
Using cached triton-2.1.0-0-cp38-cp38-manylinux2014_x86_64.manylinux_2_17_x86_64.whl (89.2 MB)
Using cached numpy-1.24.4-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (17.3 MB)
Downloading transformers-4.34.1-py3-none-any.whl (7.7 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 7.7/7.7 MB 22.7 MB/s eta 0:00:00
Downloading datasets-2.14.5-py3-none-any.whl (519 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 519.6/519.6 kB 2.7 MB/s eta 0:00:00
Downloading tiktoken-0.5.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (2.0 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.0/2.0 MB 3.6 MB/s eta 0:00:00
Downloading wandb-0.15.12-py3-none-any.whl (2.1 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.1/2.1 MB 20.4 MB/s eta 0:00:00
Downloading tqdm-4.66.1-py3-none-any.whl (78 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 78.3/78.3 kB 966.2 kB/s eta 0:00:00
Downloading click-8.1.7-py3-none-any.whl (97 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 97.9/97.9 kB 1.1 MB/s eta 0:00:00
Downloading dill-0.3.7-py3-none-any.whl (115 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 115.3/115.3 kB 1.3 MB/s eta 0:00:00
Downloading fsspec-2023.6.0-py3-none-any.whl (163 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 163.8/163.8 kB 1.9 MB/s eta 0:00:00
Downloading aiohttp-3.8.6-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.1 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.1/1.1 MB 13.8 MB/s eta 0:00:00
Downloading GitPython-3.1.40-py3-none-any.whl (190 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 190.6/190.6 kB 3.0 MB/s eta 0:00:00
Using cached packaging-23.2-py3-none-any.whl (53 kB)
Downloading protobuf-4.24.4-cp37-abi3-manylinux2014_x86_64.whl (311 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 311.6/311.6 kB 4.3 MB/s eta 0:00:00
Downloading psutil-5.9.6-cp36-abi3-manylinux_2_12_x86_64.manylinux2010_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (283 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 283.6/283.6 kB 3.8 MB/s eta 0:00:00
Downloading pyarrow-13.0.0-cp38-cp38-manylinux_2_28_x86_64.whl (40.1 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 40.1/40.1 MB 21.6 MB/s eta 0:00:00
Downloading PyYAML-6.0.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (736 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 736.6/736.6 kB 4.9 MB/s eta 0:00:00
Downloading regex-2023.10.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (776 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 777.0/777.0 kB 11.1 MB/s eta 0:00:00
Downloading requests-2.31.0-py3-none-any.whl (62 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 62.6/62.6 kB 957.5 kB/s eta 0:00:00
Downloading safetensors-0.4.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.3 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.3/1.3 MB 18.5 MB/s eta 0:00:00
Downloading sentry_sdk-1.32.0-py2.py3-none-any.whl (240 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 241.0/241.0 kB 4.3 MB/s eta 0:00:00
Downloading tokenizers-0.14.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.8 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.8/3.8 MB 21.7 MB/s eta 0:00:00
Downloading huggingface_hub-0.17.3-py3-none-any.whl (295 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 295.0/295.0 kB 4.1 MB/s eta 0:00:00
Using cached typing_extensions-4.8.0-py3-none-any.whl (31 kB)
Using cached filelock-3.12.4-py3-none-any.whl (11 kB)
Downloading multiprocess-0.70.15-py38-none-any.whl (132 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 132.6/132.6 kB 1.8 MB/s eta 0:00:00
Using cached pandas-2.0.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (12.4 MB)
Downloading setproctitle-1.3.3-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (31 kB)
Downloading xxhash-3.4.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (194 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 194.6/194.6 kB 2.3 MB/s eta 0:00:00
Downloading async_timeout-4.0.3-py3-none-any.whl (5.7 kB)
Downloading certifi-2023.7.22-py3-none-any.whl (158 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 158.3/158.3 kB 2.3 MB/s eta 0:00:00
Downloading charset_normalizer-3.3.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (137 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 137.9/137.9 kB 2.0 MB/s eta 0:00:00
Downloading frozenlist-1.4.0-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (220 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 220.1/220.1 kB 2.9 MB/s eta 0:00:00
Using cached MarkupSafe-2.1.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (25 kB)
Using cached pytz-2023.3.post1-py2.py3-none-any.whl (502 kB)
Downloading urllib3-2.0.7-py3-none-any.whl (124 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 124.2/124.2 kB 1.8 MB/s eta 0:00:00
Using cached nvidia_nvjitlink_cu12-12.2.140-py3-none-manylinux1_x86_64.whl (20.2 MB)
Downloading smmap-5.0.1-py3-none-any.whl (24 kB)
Building wheels for collected packages: pathtools
  Building wheel for pathtools (setup.py) ... done
  Created wheel for pathtools: filename=pathtools-0.1.2-py3-none-any.whl size=8791 sha256=79a081eb07be7390f6d7a7d0d272a8f747cd5aead38c57cdda69e120844b5209
  Stored in directory: /home/ye/.cache/pip/wheels/4c/8e/7e/72fbc243e1aeecae64a96875432e70d4e92f3d2d18123be004
Successfully built pathtools
Installing collected packages: pytz, pathtools, mpmath, appdirs, xxhash, urllib3, tzdata, typing-extensions, tqdm, sympy, smmap, six, setproctitle, safetensors, regex, pyyaml, psutil, protobuf, packaging, nvidia-nvtx-cu12, nvidia-nvjitlink-cu12, nvidia-nccl-cu12, nvidia-curand-cu12, nvidia-cufft-cu12, nvidia-cuda-runtime-cu12, nvidia-cuda-nvrtc-cu12, nvidia-cuda-cupti-cu12, nvidia-cublas-cu12, numpy, networkx, multidict, MarkupSafe, idna, fsspec, frozenlist, filelock, dill, Click, charset-normalizer, certifi, attrs, async-timeout, yarl, triton, sentry-sdk, requests, python-dateutil, pyarrow, nvidia-cusparse-cu12, nvidia-cudnn-cu12, multiprocess, jinja2, gitdb, docker-pycreds, aiosignal, tiktoken, pandas, nvidia-cusolver-cu12, huggingface-hub, GitPython, aiohttp, wandb, torch, tokenizers, transformers, datasets
Successfully installed Click-8.1.7 GitPython-3.1.40 MarkupSafe-2.1.3 aiohttp-3.8.6 aiosignal-1.3.1 appdirs-1.4.4 async-timeout-4.0.3 attrs-23.1.0 certifi-2023.7.22 charset-normalizer-3.3.0 datasets-2.14.5 dill-0.3.7 docker-pycreds-0.4.0 filelock-3.12.4 frozenlist-1.4.0 fsspec-2023.6.0 gitdb-4.0.10 huggingface-hub-0.17.3 idna-3.4 jinja2-3.1.2 mpmath-1.3.0 multidict-6.0.4 multiprocess-0.70.15 networkx-3.1 numpy-1.24.4 nvidia-cublas-cu12-12.1.3.1 nvidia-cuda-cupti-cu12-12.1.105 nvidia-cuda-nvrtc-cu12-12.1.105 nvidia-cuda-runtime-cu12-12.1.105 nvidia-cudnn-cu12-8.9.2.26 nvidia-cufft-cu12-11.0.2.54 nvidia-curand-cu12-10.3.2.106 nvidia-cusolver-cu12-11.4.5.107 nvidia-cusparse-cu12-12.1.0.106 nvidia-nccl-cu12-2.18.1 nvidia-nvjitlink-cu12-12.2.140 nvidia-nvtx-cu12-12.1.105 packaging-23.2 pandas-2.0.3 pathtools-0.1.2 protobuf-4.24.4 psutil-5.9.6 pyarrow-13.0.0 python-dateutil-2.8.2 pytz-2023.3.post1 pyyaml-6.0.1 regex-2023.10.3 requests-2.31.0 safetensors-0.4.0 sentry-sdk-1.32.0 setproctitle-1.3.3 six-1.16.0 smmap-5.0.1 sympy-1.12 tiktoken-0.5.1 tokenizers-0.14.1 torch-2.1.0 tqdm-4.66.1 transformers-4.34.1 triton-2.1.0 typing-extensions-4.8.0 tzdata-2023.3 urllib3-2.0.7 wandb-0.15.12 xxhash-3.4.1 yarl-1.9.2
(nanoGPT) ye@lst-gpu-3090:~/tool$
```

## Cloning nanoGPT on LST Server

```
(nanoGPT) ye@lst-gpu-3090:~/tool$ git clone https://github.com/karpathy/nanoGPT
Cloning into 'nanoGPT'...
remote: Enumerating objects: 649, done.
remote: Total 649 (delta 0), reused 0 (delta 0), pack-reused 649
Receiving objects: 100% (649/649), 936.46 KiB | 5.41 MiB/s, done.
Resolving deltas: 100% (371/371), done.
(nanoGPT) ye@lst-gpu-3090:~/tool$
```

## Copying Prepared Data/Scripts to LST Server

ဟိုးအထက်မှာ ပြင်ဆင်ခဲ့တဲ့ data တွေနဲ့ scripts တွေကို CADT GPU server ပေါ်ကနေ ကိုယ့် local စက်ထဲကို အရင်ဆုံး download လုပ်ခဲ့တယ်။ ပြီးတော့မှ ကိုယ့် local Windows OS စက်ကနေ LST GPU server ပေါ်ဆီကို အောက်ပါအတိုင်း copy ကူးယူခဲ့တယ်။ ip address စတာတွေကိုတော့ ဒီ note မှာ security reason အရ x နဲ့ အစားထိုးထားခဲ့တယ်။  

```
C:\Users\801680>scp Downloads\data.zip ye@xx.xxx.xx.xx:/home/ye/exp/myHatespeech/nanoGPT/
ye@xx.xxx.xx.xx's password:
data.zip                                                100% 1208KB 166.5KB/s   00:07
```

```
C:\Users\801680>scp Downloads\myHatespeech_char.zip ye@xx.xxx.xx.xx:/home/ye/exp/myHatespeech/nanoGPT/
ye@xx.xxx.xx.xx's password:
myHatespeech_char.zip                                   100%  775KB 276.1KB/s   00:02
```

```
C:\Users\801680>scp Downloads\train_myHatespeech_char.py ye@xx.xxx.xx.xx:/home/ye/exp/myHatespeech/nanoGPT/
ye@xx.xxx.xx.xx's password:
train_myHatespeech_char.py                              100% 1055    15.2KB/s   00:00

C:\Users\801680>
```

အရင်ဆုံး dummy ကူးထားခဲ့တဲ့ folder ကို ပြန်စစ်ခဲ့ ...  

```
(nanoGPT) ye@lst-gpu-3090:~/exp/myHatespeech/nanoGPT$ ls
data.zip  myHatespeech_char.zip  train_myHatespeech_char.py
(nanoGPT) ye@lst-gpu-3090:~/exp/myHatespeech/nanoGPT$
```

အဲဒီကနေ tool/nanoGPT/ folder အောက်ကို copy ပြန်ကူးပြီး ပြင်ဆင်ခဲ့တယ်။  

```
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT/data$ ls
openwebtext  shakespeare  shakespeare_char
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT/data$ cp -r /home/ye/exp/myHatespeech/nanoGPT/myHatespeech_char .
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT/data$ ls
myHatespeech_char  openwebtext  shakespeare  shakespeare_char
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT/data$ ls ./myHatespeech_char/
hs_data_4Oct2023.clean.txt  meta.pkl  prepare-my-char.py  train.bin  val.bin
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT/data$
```

```
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT/config$ cp /home/ye/exp/myHatespeech/nanoGPT/train_myHatespeech_char.py .
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT/config$
```

## Training myHatespeech GPT2 Model

check the config file again:  

```
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT/config$ cat ./train_myHatespeech_char.py
# train a miniature character-level Myanmar Hatepeech model

out_dir = 'out-myHatespeech-char'
eval_interval = 250 # keep frequent because we'll overfit
eval_iters = 200
log_interval = 10 # don't print too too often

# we expect to overfit on this small dataset, so only save when val improves
always_save_checkpoint = False

wandb_log = False # override via command line if you like
wandb_project = 'myHatespeech-char'
wandb_run_name = 'mini-gpt'

dataset = 'myHatespeech_char'
batch_size = 64
block_size = 256 # context of up to 256 previous characters

# baby GPT model :)
n_layer = 6
n_head = 6
n_embd = 384
dropout = 0.2

learning_rate = 1e-3 # with baby networks can afford to go a bit higher
max_iters = 5000
lr_decay_iters = 5000 # make equal to max_iters usually
min_lr = 1e-4 # learning_rate / 10 usually
beta2 = 0.99 # make a bit bigger because number of tokens per iter is small

warmup_iters = 100 # not super necessary potentially

# on macbook also add
# device = 'cpu'  # run on cpu only
# compile = False # do not torch compile the model
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT/config$
```

Start training GPT2 model with hatespeech data:  

```
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT$ time torchrun ./train.py ./config/train_myHatesp
eech_char.py | tee myHatespeech_char_exp1.log
Overriding config with ./config/train_myHatespeech_char.py:
# train a miniature character-level Myanmar Hatepeech model

out_dir = 'out-myHatespeech-char'
eval_interval = 250 # keep frequent because we'll overfit
eval_iters = 200
log_interval = 10 # don't print too too often

# we expect to overfit on this small dataset, so only save when val improves
always_save_checkpoint = False

wandb_log = False # override via command line if you like
wandb_project = 'myHatespeech-char'
wandb_run_name = 'mini-gpt'

dataset = 'myHatespeech_char'
batch_size = 64
block_size = 256 # context of up to 256 previous characters

# baby GPT model :)
n_layer = 6
n_head = 6
n_embd = 384
dropout = 0.2

learning_rate = 1e-3 # with baby networks can afford to go a bit higher
max_iters = 5000
lr_decay_iters = 5000 # make equal to max_iters usually
min_lr = 1e-4 # learning_rate / 10 usually
beta2 = 0.99 # make a bit bigger because number of tokens per iter is small

warmup_iters = 100 # not super necessary potentially

# on macbook also add
# device = 'cpu'  # run on cpu only
# compile = False # do not torch compile the model

tokens per iteration will be: 655,360
found vocab_size = 343 (inside data/myHatespeech_char/meta.pkl)
Initializing a new model from scratch
number of parameters: 10.75M
num decayed parameter tensors: 26, with 10,846,848 parameters
num non-decayed parameter tensors: 13, with 4,992 parameters
using fused AdamW: True
compiling the model... (takes a ~minute)
step 0: train loss 5.9544, val loss 5.9531
iter 0: loss 5.9471, time 1210102.02ms, mfu -100.00%
iter 10: loss 4.0368, time 17676.57ms, mfu 0.85%

```

training လုပ်တာ တအားနှေးနေလို့ GPU ကို စစ်ကြည့်တော့ ERR! ဖြစ်နေတာတွေ့ရလို့ GPU server စက်ကို reboot လုပ်ချလိုက်ပြီး ပြန် training လုပ်ခဲ့ ... 

```
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT$ time torchrun ./train.py ./config/train_myHatesp
eech_char.py | tee myHatespeech_char_exp1.log
Overriding config with ./config/train_myHatespeech_char.py:
# train a miniature character-level Myanmar Hatepeech model

out_dir = 'out-myHatespeech-char'
eval_interval = 250 # keep frequent because we'll overfit
eval_iters = 200
log_interval = 10 # don't print too too often

# we expect to overfit on this small dataset, so only save when val improves
always_save_checkpoint = False

wandb_log = False # override via command line if you like
wandb_project = 'myHatespeech-char'
wandb_run_name = 'mini-gpt'

dataset = 'myHatespeech_char'
batch_size = 64
block_size = 256 # context of up to 256 previous characters

# baby GPT model :)
n_layer = 6
n_head = 6
n_embd = 384
dropout = 0.2

learning_rate = 1e-3 # with baby networks can afford to go a bit higher
max_iters = 5000
lr_decay_iters = 5000 # make equal to max_iters usually
min_lr = 1e-4 # learning_rate / 10 usually
beta2 = 0.99 # make a bit bigger because number of tokens per iter is small

warmup_iters = 100 # not super necessary potentially

# on macbook also add
# device = 'cpu'  # run on cpu only
# compile = False # do not torch compile the model

tokens per iteration will be: 655,360
found vocab_size = 343 (inside data/myHatespeech_char/meta.pkl)
Initializing a new model from scratch
number of parameters: 10.75M
num decayed parameter tensors: 26, with 10,846,848 parameters
num non-decayed parameter tensors: 13, with 4,992 parameters
using fused AdamW: True
compiling the model... (takes a ~minute)
step 0: train loss 5.9544, val loss 5.9531
iter 0: loss 5.9471, time 31860.03ms, mfu -100.00%
iter 10: loss 4.0368, time 1113.83ms, mfu 13.50%
iter 20: loss 3.0333, time 1118.86ms, mfu 13.50%
iter 30: loss 2.5062, time 1118.83ms, mfu 13.49%
iter 40: loss 2.2987, time 1124.79ms, mfu 13.48%
iter 50: loss 2.1806, time 1124.80ms, mfu 13.47%
iter 60: loss 2.1559, time 1124.98ms, mfu 13.46%
iter 70: loss 2.1709, time 1125.21ms, mfu 13.45%
iter 80: loss 2.1324, time 1125.11ms, mfu 13.44%
iter 90: loss 2.1409, time 1131.22ms, mfu 13.43%
iter 100: loss 2.1276, time 1131.26ms, mfu 13.41%
iter 110: loss 2.0870, time 1130.97ms, mfu 13.40%
iter 120: loss 2.0193, time 1130.88ms, mfu 13.39%
iter 130: loss 1.9595, time 1130.92ms, mfu 13.38%
...
...
...
iter 1980: loss 0.1806, time 1125.56ms, mfu 13.26%
iter 1990: loss 0.1815, time 1125.58ms, mfu 13.27%
step 2000: train loss 0.0732, val loss 2.9034
iter 2000: loss 0.1770, time 4746.37ms, mfu 12.26%
iter 2010: loss 0.1691, time 1125.77ms, mfu 12.37%
iter 2020: loss 0.1690, time 1125.86ms, mfu 12.47%
iter 2030: loss 0.1679, time 1125.46ms, mfu 12.56%
iter 2040: loss 0.1796, time 1125.65ms, mfu 12.64%
iter 2050: loss 0.1694, time 1125.60ms, mfu 12.71%
iter 2060: loss 0.1784, time 1125.48ms, mfu 12.78%
iter 2070: loss 0.1704, time 1125.48ms, mfu 12.84%
iter 2080: loss 0.1764, time 1125.76ms, mfu 12.89%
iter 2090: loss 0.1791, time 1125.59ms, mfu 12.94%
iter 2100: loss 0.1631, time 1125.94ms, mfu 12.98%
iter 2110: loss 0.1603, time 1125.46ms, mfu 13.02%
iter 2120: loss 0.1738, time 1125.70ms, mfu 13.05%
iter 2130: loss 0.1721, time 1125.24ms, mfu 13.08%
iter 2140: loss 0.1683, time 1125.53ms, mfu 13.11%
iter 2150: loss 0.1585, time 1125.81ms, mfu 13.14%
iter 2160: loss 0.1761, time 1125.40ms, mfu 13.16%
iter 2170: loss 0.1677, time 1125.57ms, mfu 13.18%
...
...
...
iter 2440: loss 0.1465, time 1125.80ms, mfu 13.21%
iter 2450: loss 0.1433, time 1125.52ms, mfu 13.23%
iter 2460: loss 0.1464, time 1125.42ms, mfu 13.24%
iter 2470: loss 0.1494, time 1125.63ms, mfu 13.25%
iter 2480: loss 0.1460, time 1125.53ms, mfu 13.26%
iter 2490: loss 0.1499, time 1125.48ms, mfu 13.27%
step 2500: train loss 0.0681, val loss 3.1280
iter 2500: loss 0.1433, time 4743.42ms, mfu 12.26%
iter 2510: loss 0.1437, time 1125.56ms, mfu 12.37%
iter 2520: loss 0.1457, time 1125.79ms, mfu 12.47%
iter 2530: loss 0.1461, time 1125.47ms, mfu 12.56%
iter 2540: loss 0.1463, time 1125.77ms, mfu 12.64%
iter 2550: loss 0.1469, time 1125.45ms, mfu 12.71%
iter 2560: loss 0.1470, time 1125.59ms, mfu 12.78%
iter 2570: loss 0.1401, time 1125.66ms, mfu 12.84%
iter 2580: loss 0.1393, time 1125.77ms, mfu 12.89%
iter 2590: loss 0.1446, time 1125.55ms, mfu 12.94%
iter 2600: loss 0.1408, time 1125.60ms, mfu 12.98%
iter 2610: loss 0.1423, time 1125.52ms, mfu 13.02%
iter 2620: loss 0.1383, time 1125.69ms, mfu 13.05%
iter 2630: loss 0.1441, time 1125.77ms, mfu 13.08%
iter 2640: loss 0.1516, time 1125.48ms, mfu 13.11%
...
...
...
iter 2960: loss 0.1256, time 1125.61ms, mfu 13.24%
iter 2970: loss 0.1326, time 1125.72ms, mfu 13.25%
iter 2980: loss 0.1251, time 1125.53ms, mfu 13.26%
iter 2990: loss 0.1332, time 1125.78ms, mfu 13.27%
step 3000: train loss 0.0646, val loss 3.3001
iter 3000: loss 0.1231, time 4756.76ms, mfu 12.26%
iter 3010: loss 0.1280, time 1126.02ms, mfu 12.37%
iter 3020: loss 0.1291, time 1125.21ms, mfu 12.47%
iter 3030: loss 0.1308, time 1125.49ms, mfu 12.56%
iter 3040: loss 0.1249, time 1125.60ms, mfu 12.64%
iter 3050: loss 0.1247, time 1125.65ms, mfu 12.71%
...
...
...
iter 3720: loss 0.1129, time 1125.41ms, mfu 13.25%
iter 3730: loss 0.1069, time 1125.64ms, mfu 13.26%
iter 3740: loss 0.1107, time 1125.51ms, mfu 13.27%
step 3750: train loss 0.0616, val loss 3.4785
iter 3750: loss 0.1065, time 4728.09ms, mfu 12.26%
iter 3760: loss 0.1067, time 1125.68ms, mfu 12.37%
iter 3770: loss 0.1134, time 1125.63ms, mfu 12.47%
iter 3780: loss 0.1075, time 1125.70ms, mfu 12.56%
iter 3790: loss 0.1083, time 1125.69ms, mfu 12.64%
iter 3800: loss 0.1104, time 1125.53ms, mfu 12.71%
iter 3810: loss 0.1134, time 1125.57ms, mfu 12.78%
iter 3820: loss 0.1083, time 1125.62ms, mfu 12.84%
iter 3830: loss 0.1062, time 1125.15ms, mfu 12.89%
iter 3840: loss 0.1032, time 1125.74ms, mfu 12.94%
iter 3850: loss 0.1103, time 1125.66ms, mfu 12.98%
iter 3860: loss 0.1027, time 1125.94ms, mfu 13.02%
iter 3870: loss 0.1084, time 1125.26ms, mfu 13.05%
iter 3880: loss 0.1087, time 1125.57ms, mfu 13.08%
iter 3890: loss 0.1114, time 1125.45ms, mfu 13.11%
iter 3900: loss 0.1077, time 1125.39ms, mfu 13.14%
iter 3910: loss 0.1104, time 1125.42ms, mfu 13.16%
...
...
...
iter 4200: loss 0.1068, time 1126.03ms, mfu 13.23%
iter 4210: loss 0.1011, time 1125.61ms, mfu 13.24%
iter 4220: loss 0.0970, time 1125.76ms, mfu 13.25%
iter 4230: loss 0.1012, time 1125.38ms, mfu 13.26%
iter 4240: loss 0.1024, time 1125.39ms, mfu 13.27%
step 4250: train loss 0.0600, val loss 3.5678
iter 4250: loss 0.1014, time 4747.28ms, mfu 12.26%
iter 4260: loss 0.1043, time 1125.54ms, mfu 12.37%
iter 4270: loss 0.1029, time 1125.64ms, mfu 12.47%
iter 4280: loss 0.1039, time 1125.74ms, mfu 12.56%
iter 4290: loss 0.0969, time 1125.31ms, mfu 12.64%
iter 4300: loss 0.0993, time 1125.43ms, mfu 12.71%
iter 4310: loss 0.1030, time 1125.69ms, mfu 12.78%
iter 4320: loss 0.0983, time 1125.59ms, mfu 12.84%
iter 4330: loss 0.1025, time 1125.57ms, mfu 12.89%
iter 4340: loss 0.1023, time 1125.66ms, mfu 12.94%
iter 4350: loss 0.1033, time 1125.80ms, mfu 12.98%
iter 4360: loss 0.0998, time 1125.62ms, mfu 13.02%
iter 4370: loss 0.1066, time 1125.46ms, mfu 13.05%
iter 4380: loss 0.0955, time 1125.31ms, mfu 13.08%
iter 4390: loss 0.1031, time 1125.53ms, mfu 13.11%
iter 4400: loss 0.1000, time 1125.47ms, mfu 13.14%
...
...
...
iter 4840: loss 0.0975, time 1125.78ms, mfu 12.94%
iter 4850: loss 0.1012, time 1125.65ms, mfu 12.98%
iter 4860: loss 0.0944, time 1125.76ms, mfu 13.02%
iter 4870: loss 0.0976, time 1125.52ms, mfu 13.05%
iter 4880: loss 0.0924, time 1125.53ms, mfu 13.08%
iter 4890: loss 0.1005, time 1125.38ms, mfu 13.11%
iter 4900: loss 0.1001, time 1125.48ms, mfu 13.14%
iter 4910: loss 0.0951, time 1125.49ms, mfu 13.16%
iter 4920: loss 0.0995, time 1125.52ms, mfu 13.18%
iter 4930: loss 0.0998, time 1125.86ms, mfu 13.20%
iter 4940: loss 0.1007, time 1125.64ms, mfu 13.21%
iter 4950: loss 0.1005, time 1125.59ms, mfu 13.23%
iter 4960: loss 0.0966, time 1125.53ms, mfu 13.24%
iter 4970: loss 0.0942, time 1125.58ms, mfu 13.25%
iter 4980: loss 0.0982, time 1125.69ms, mfu 13.26%
iter 4990: loss 0.0937, time 1125.62ms, mfu 13.27%
step 5000: train loss 0.0585, val loss 3.6645
iter 5000: loss 0.0992, time 4749.53ms, mfu 12.26%

real    95m46.108s
user    53m32.433s
sys     42m14.771s
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT$
```

training လုပ်နေစဉ်မှာ nvidia-smi command နဲ့ စစ်ကြည့်တော့ GPU ကို သုံးနေတာကို အောက်ပါအတိုင်း တွေ့ခဲ့ရ ...  
သေချာသွားပြီး စောစောက training က multiple CPU ကို သုံးပြီး training လုပ်နေတာ...  

```
(base) ye@lst-gpu-3090:~$ (base) ye@lst-gpu-3090:~$ nvidia-smi
Thu Oct 19 23:28:28 2023
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 525.125.06   Driver Version: 525.125.06   CUDA Version: 12.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:01:00.0 Off |                  Off |
| 31%   67C    P2   416W / 480W |   5110MiB / 24564MiB |    100%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      1993      G   /usr/lib/xorg/Xorg                 59MiB |
|    0   N/A  N/A      2359      G   /usr/bin/gnome-shell              123MiB |
|    0   N/A  N/A      8378      C   python                           1716MiB |
|    0   N/A  N/A     10700      C   ...3/envs/nanoGPT/bin/python     3206MiB |
+-----------------------------------------------------------------------------+
(base) ye@lst-gpu-3090:~$
```

Check the model file:  

```
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT$ ls ./out-myHatespeech-char/
ckpt.pt
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT$
```

## Testing No. 1

```
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT$ torchrun ./sample.py --out_dir=out-myHatespeech-char | tee myHatespeech_char_test1.log


Overriding: out_dir = out-myHatespeech-char
number of parameters: 10.75M
Loading meta from data/myHatespeech_char/meta.pkl...
မနက် ၅ နာရီ ခု ထိ မ လာ ဘူး ၅ မိနစ် ၅ နာရီ ထိ ပျက် သွား အောင် ပေး တာ လား လီး ပဲ ဟေ့ မအေလိုး တွေပျက် သွား ပြီ ပြန် ဖျက် သလို ပဲောင် မ ပြည့် တော့ ဘူး မအေလိုး တွေ မီး နာရီ ပြန် ပျက် တယ် ဆို တော့ မ သိဝက် လည်း ပျက် ပြီ လီး ပဲ ဟေ့
မအေလိုး တွေ မီတာခ ကျတော့ ပြည်သူ တွေ အကုန်လုံး ခု မီး လာ မယ့် အချိန် မှန် အိပ် ပေး ပြီ နော် မီး ပျက် နေ တာေ ရေ
မအေလိုး တွေ တစ် နေကုန် ပျက် ၉ နာရီ လာ ပြီး ၉ နာရီ တော့ မှာ လာ ဖြတ် နေ တာ ပဲ
မအေလိုး တွေ အခု ထိ မ
---------------

နင့် လက်နက် တစ် ချောင်း ပါ တယ် နင် က ဖျက် နေ တာ လား စောက်ပြစ် ကျက်သရေတုံး တွေ
ဖင်ယား တယ် နော် လေ ယီး ပဲ လိ့ ကိုယ့် ပုံမှန် အောင် ပေး ပါ ဦး
အခွင့်အရေးယူ မှာ လား ဟင် မျက်နှာ ကို ကျက်သရေကိုတုံး တဲ့ ကောင် တွေ နောက် နေ ပြီ လီး ပဲ
မအေလိုး တွေ ရေ မီး ကို ၅ မိနစ် ပေး ပြီး လီး ပဲ လား ? မအေလိုး တွေ မြင် ရ အောင် မင်း တို့ တစ် နေ့ လုံး စောက်ပ                                                                        ပေါ တွေ ပေး မ နေ နဲ့ မ ေး နဲ့ လူကမွေးထားတာလား ဟ သူတောင်းစား တွေ နောက် လာ ရင် လည်း လူကြီး တွေ စောက်က                                                                                 ကလေး တွေ ရေ တင် ကြ လာ ပြီ ပေါ့ 🤌
လီး လား ရုပ် က တော့ လီး ပဲ
သူ တို့ ထုတ
---------------

တော်တော် ကို နှိပ်စက် လိုက် တာ မအေလိုး မျိုး
ကလေး က မြန်မာ နိုင်ငံ က လည်း သူ က ပါးရိုက် ချင် စရာ
ကျွန်မ အရင် က ဘယ်လောက် များ ပါ လဲ ဆိုရင် ကိုယ့် အစီအစဉ်
အစ မ သိ တာ ကျ အောင် က ပဲ ဘုရား ဆို တာ ပါ ပဲ ရီ ချင် တယ်
ရွံ စရာ ကြီး ရယ် နော် နှစ် ယောက် လုံး ကို သက်သက် မ ကြာ ဘဲ အမှား တာ မ ဟုတ် ဘူး မယားငယ်မ လူ တွေ သွား တ                                                                               တာ မ ဟုတ် ဘူး လေ နင့် ကို လည်း စောက်ချိုးမပြေ ဘူး
ခု မှ ကို ဘယ်လို အင်္ကျီ က သူများ လင် ယူ သွား လို့ လဲ ဟ 🙄
ခွေးသူတောင်းစား တွေ ပြော တာ ဘုရား စနစ် ကို လာ ပြီး စောက်ရူး စောက်သုံးမကျ တော့ ဘူး လာ
---------------

အခွင့် ရှိ တော့ မယ် ဘာ လုပ်လုပ် ပြ လဲ စောက်ရူး
အစ ကတည်းက မ ကြည့် ဘူး
အကြမ်းဖက် ကို ဖျက် စရာ ကောင်း လိုက် တာ ကို 😏 😏
အခု တော့ နော် ပွဲ က
ကလေး နဲ့ ကျပ်မပြည့် တဲ့ အချိန် ဆို ပြီး မှာ ကျေးဇူးတင် ပါ တယ် လူ က အခု တော့ ပရိတ်သတ် ချက် အဲ့လို မျိုး ကို ပျက်                                                                     ထား တော့ ရူး နေ လိုက် ရင် ပူလောင်နှမလို့ ကျ သလို တံတား ကျ နေ တာ လား မြန်မာ မ တုံး နဲ့ ကို နာမည်ကြီး နဲ့ နေရာ မ                                                                     မ ထူးဆန်း ဘူး လူပါးဝ တဲ့ ရေပေါ် ကို ဖျက်စီး အောင် လုပ် နေ တာ ကိုး မ ဟုတ် ဘူး အိမ်ထောင် ရင်း ရော ဘာ မှ မ ပ                                                                           ပြော နဲ့ စောက်ကျင့် သူတောင်းစား က သူ တွ
ြော နဲ့ စောက်ကျင့် သူတောင်းစား က သူ တွ
---------------

လီး လုပ် ပြီ လား
မိန်းမ တစ် လောက် မှ အား မ နေ နဲ့ ကိုမေကိုလိုး နေ ပြီ မီး က နေ ၅ နာရီ ခွဲ တည်းက ပျက် ချိန် တစ် နေကုန် ၁ နာ                                                                          ာရီ ခြား တစ် ခါ တည်း ပျက် တယ် ခု ထိ မ လာ သေး ဘူး လီး လုပ် နေ ကြ တာ လား မအေလိုး
လီး ပဲ မီး ပေး တဲ့ အချိန် လည်း ပျက် တဲ့ အချိန် မီး ပေး နေ တဲ့ အချိန် ကျ ပျက် တဲ့ အချိန် ဆို တာ က လည်း မ လာ ဘဲ                                                                      ဘဲ ခိုး ဖျက် တဲ့ အချိန် ကျ လို့ မီး က အခု ထိ ပေး နေ တာ မအေလိုး တွေ ငါလိုး တွေ ရ
မီး လာ ရ မယ့် အချိန် ပျက် တယ် 😡 မီး က ခု ထိ မ လာ ဘူး နော် မီး က တော့ ဖျက် နေ တယ် မီး က ပူ လွန်း လို့ သေ                                                                           ေး တယ် အချိ
---------------

နင် တို့ တွေ ပဲ ကောင်းကောင်း ပါ တယ် တွေ့ မယ် သူ တို့ က လည်း လည်း လူလိမ် ကလိမ် ခွေးကမာလားလား ရဲ့
ငါ တို့ က အဲ့ လောက် ဖျက် နေ တာ လား
မိဘ လုပ်စာ လေး ကို ဖန်တီး ပါ တယ် လီး ပဲ နော်
ရူး နေ သေး တယ် လီး လို ပဲ အက လီး ပဲ ကို မ ရ ဘူး လား ? မသာမ ရေ
စောက်ပေါ အမျိုးယုတ်
ကြိုက် လိုက် ကြ ပါ နဲ့ မနက် က
အမ ရယ် ဒီ လောက် ဆို ပြီး များ စား ပေး ချင် တယ် 🙂😆😆
ငါ လည်း လာ ပြီး 2 ယောက် က ပြန် မ လာ ဘူး နောက်ဆုံး မ လာ ရ မှာ လေ
တကယ့် အချိန် လည်း မ လာ ပါ နဲ့ 🙂 ကျေးဇူး ပါ ဆို ပြီး လည်း ငါ တို့ တုန်း က ပို ပေး ရ မှာ ပေါ့
မင်း
---------------

ဒိုင် တွေ ကို အပေါ်ယံ ကြည့် တာ ကို လူ့ စွတ် ကို မ မြင် ဖူး ဘူး လား ?
စောက်ချိုးမပြေ ဘူး
စောက်ခွက် ကို မျက်နှာ ထက် အထာ နဲ့ ပစ်သတ် နေ တာ ကို ဒုက္ခ ပေး မယ် အချိန် မှာ မ ပေး နိုင် ဘူး ကွာ ။
စောက်ပို တွေ ရ မှာ ပေါ့
ဒိုင် တွေ ပြော မ နေ နဲ့ မင်း တို့ ယောက်ျား တွေ က ဒီ လို အောကား လာ ပြီး ပြန် ပြီး အရေးယူ နေ တယ် ဒီ လောက်                                                                             ဖြစ် တော့ မယ် အချိန် ညှပ် မ ရှိ ဘူး နော်
အထက် ကြီး ပါ ပြီး မှာ မြန်မာ နိုင်ငံ သား သမီး တွေ ဆို တာ တောင် အရမ်း ရှည် ကြ ပါ တယ် သား သမီး တွေ သူ                                                                                 အများကြီး အသက် မှာ စိတ် မ ရှိ ပါ ဘူး အေးချမ်း
---------------

မင်း အမေ က ကြီး လာ တယ် အား မ လား အောင် ပြန် အိုင် နေ သေး တယ် မြန်မာ ပြည် မှာ တော့ ခု ထိ မီး ပေး ပ
လူ က ရော နင် တို့ တစ် ယောက် က အစား ဖူး တုန်း က ကိုယ့် အများကြီး လို့ ရ တယ် ရှင်း ပေါ် က နေ မြန်မာ လူမျိုး တွေ က သူ တို့ နိုင်ငံ လေး တွေ က လုပ် ခဲ့ ရ လေ နေ လို့ အမေ မ ဟုတ် ဘူး တဲ့ သူ တွေ သူ တို့ အတွက် တောင် မ စား လို့ လား နော်
အခု မှ သန့် တာ ပဲ မြန်မာ ပြည် မှာ ပဲ လေ မအလ ကြီး ရာ ချင် စရာ
ပြော ချက် ရ တာ ပေါ့ အရှက်မရှိ တဲ့ ချီးစား ကြီး ဘာ လေးစား ထား လဲ မ သိ ဘူး လေ ၊ ဖင်ခံ စား ခဲ့ ပြီး ရင် နင့် အသက် နဲ့
---------------
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT$
```

## Testing No. 2

```
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT$ torchrun ./sample.py --out_dir=out-myHatespeech-char | tee myHatespeech_char_test2.log
Overriding: out_dir = out-myHatespeech-char
number of parameters: 10.75M
Loading meta from data/myHatespeech_char/meta.pkl...

မနက် ၅ နာရီ ခု ထိ မ လာ ဘူး ၅ မိနစ် ၅ နာရီ ထိ ပျက် သွား အောင် ပေး တာ လား လီး ပဲ ဟေ့ မအေလိုး တွေ
မီး ပျက် သွား ပြီ ပြန် ဖျက် သလို ပဲ
မီး လာ ရ မှာ မီး ပေး ပြီး ၅ မိနစ် တောင် မ ပြည့် တော့ ဘူး မအေလိုး တွေ မီး နာရီ ပြန် ပျက် တယ် ဆို တော့ မ သိ ရင် လည်း နာရီဝက် လည်း ပျက် ပြီ လီး ပဲ ဟေ့
မအေလိုး တွေ မီတာခ ကျတော့ ပြည်သူ တွေ အကုန်လုံး ခု မီး လာ မယ့် အချိန် မှန် အိပ် ပေး ပြီ နော် မီး ပျက် နေ တာ လား မအေလိုး တွေ ရေ
မအေလိုး တွေ တစ် နေကုန် ပျက် ၉ နာရီ လာ ပြီး ၉ နာရီ တော့ မှာ လာ ဖြတ် နေ တာ ပဲ
မအေလိုး တွေ အခု ထိ မ
---------------

နင့် လက်နက် တစ် ချောင်း ပါ တယ် နင် က ဖျက် နေ တာ လား စောက်ပြစ် ကျက်သရေတုံး တွေ
ဖင်ယား တယ် နော် လေ ယီး ပဲ လိ့ ကိုယ့် ပုံမှန် အောင် ပေး ပါ ဦး
အခွင့်အရေးယူ မှာ လား ဟင် မျက်နှာ ကို ကျက်သရေကိုတုံး တဲ့ ကောင် တွေ နောက် နေ ပြီ လီး ပဲ
မအေလိုး တွေ ရေ မီး ကို ၅ မိနစ် ပေး ပြီး လီး ပဲ လား ? မအေလိုး တွေ မြင် ရ အောင် မင်း တို့ တစ် နေ့ လုံး စောက်ပေါ တွေ ပေး မ နေ နဲ့ မ ေး နဲ့ လူကမွေးထားတာလား ဟ သူတောင်းစား တွေ နောက် လာ ရင် လည်း လူကြီး တွေ စောက်ကလေး တွေ ရေ တင် ကြ လာ ပြီ ပေါ့ 🤌
လီး လား ရုပ် က တော့ လီး ပဲ
သူ တို့ ထုတ
---------------

တော်တော် ကို နှိပ်စက် လိုက် တာ မအေလိုး မျိုး
ကလေး က မြန်မာ နိုင်ငံ က လည်း သူ က ပါးရိုက် ချင် စရာ
ကျွန်မ အရင် က ဘယ်လောက် များ ပါ လဲ ဆိုရင် ကိုယ့် အစီအစဉ်
အစ မ သိ တာ ကျ အောင် က ပဲ ဘုရား ဆို တာ ပါ ပဲ ရီ ချင် တယ်
ရွံ စရာ ကြီး ရယ် နော် နှစ် ယောက် လုံး ကို သက်သက် မ ကြာ ဘဲ အမှား တာ မ ဟုတ် ဘူး မယားငယ်မ လူ တွေ သွား တာ မ ဟုတ် ဘူး လေ နင့် ကို လည်း စောက်ချိုးမပြေ ဘူး
ခု မှ ကို ဘယ်လို အင်္ကျီ က သူများ လင် ယူ သွား လို့ လဲ ဟ 🙄
ခွေးသူတောင်းစား တွေ ပြော တာ ဘုရား စနစ် ကို လာ ပြီး စောက်ရူး စောက်သုံးမကျ တော့ ဘူး လာ
---------------

အခွင့် ရှိ တော့ မယ် ဘာ လုပ်လုပ် ပြ လဲ စောက်ရူး
အစ ကတည်းက မ ကြည့် ဘူး
အကြမ်းဖက် ကို ဖျက် စရာ ကောင်း လိုက် တာ ကို 😏 😏
အခု တော့ နော် ပွဲ က
ကလေး နဲ့ ကျပ်မပြည့် တဲ့ အချိန် ဆို ပြီး မှာ ကျေးဇူးတင် ပါ တယ် လူ က အခု တော့ ပရိတ်သတ် ချက် အဲ့လို မျိုး ကို ပျက် ထား တော့ ရူး နေ လိုက် ရင် ပူလောင်နှမလို့ ကျ သလို တံတား ကျ နေ တာ လား မြန်မာ မ တုံး နဲ့ ကို နာမည်ကြီး နဲ့ နေရာ မ ထူးဆန်း ဘူး လူပါးဝ တဲ့ ရေပေါ် ကို ဖျက်စီး အောင် လုပ် နေ တာ ကိုး မ ဟုတ် ဘူး အိမ်ထောင် ရင်း ရော ဘာ မှ မ ပြော နဲ့ စောက်ကျင့် သူတောင်းစား က သူ တွ
---------------

လီး လုပ် ပြီ လား
မိန်းမ တစ် လောက် မှ အား မ နေ နဲ့ ကိုမေကိုလိုး နေ ပြီ မီး က နေ ၅ နာရီ ခွဲ တည်းက ပျက် ချိန် တစ် နေကုန် ၁ နာရီ ခြား တစ် ခါ တည်း ပျက် တယ် ခု ထိ မ လာ သေး ဘူး လီး လုပ် နေ ကြ တာ လား မအေလိုး
လီး ပဲ မီး ပေး တဲ့ အချိန် လည်း ပျက် တဲ့ အချိန် မီး ပေး နေ တဲ့ အချိန် ကျ ပျက် တဲ့ အချိန် ဆို တာ က လည်း မ လာ ဘဲ ခိုး ဖျက် တဲ့ အချိန် ကျ လို့ မီး က အခု ထိ ပေး နေ တာ မအေလိုး တွေ ငါလိုး တွေ ရ
မီး လာ ရ မယ့် အချိန် ပျက် တယ် 😡 မီး က ခု ထိ မ လာ ဘူး နော် မီး က တော့ ဖျက် နေ တယ် မီး က ပူ လွန်း လို့ သေး တယ် အချိ
---------------

နင် တို့ တွေ ပဲ ကောင်းကောင်း ပါ တယ် တွေ့ မယ် သူ တို့ က လည်း လည်း လူလိမ် ကလိမ် ခွေးကမာလားလား ရဲ့
ငါ တို့ က အဲ့ လောက် ဖျက် နေ တာ လား
မိဘ လုပ်စာ လေး ကို ဖန်တီး ပါ တယ် လီး ပဲ နော်
ရူး နေ သေး တယ် လီး လို ပဲ အက လီး ပဲ ကို မ ရ ဘူး လား ? မသာမ ရေ
စောက်ပေါ အမျိုးယုတ်
ကြိုက် လိုက် ကြ ပါ နဲ့ မနက် က
အမ ရယ် ဒီ လောက် ဆို ပြီး များ စား ပေး ချင် တယ် 🙂😆😆
ငါ လည်း လာ ပြီး 2 ယောက် က ပြန် မ လာ ဘူး နောက်ဆုံး မ လာ ရ မှာ လေ
တကယ့် အချိန် လည်း မ လာ ပါ နဲ့ 🙂 ကျေးဇူး ပါ ဆို ပြီး လည်း ငါ တို့ တုန်း က ပို ပေး ရ မှာ ပေါ့
မင်း
---------------

ဒိုင် တွေ ကို အပေါ်ယံ ကြည့် တာ ကို လူ့ စွတ် ကို မ မြင် ဖူး ဘူး လား ?
စောက်ချိုးမပြေ ဘူး
စောက်ခွက် ကို မျက်နှာ ထက် အထာ နဲ့ ပစ်သတ် နေ တာ ကို ဒုက္ခ ပေး မယ် အချိန် မှာ မ ပေး နိုင် ဘူး ကွာ ။
စောက်ပို တွေ ရ မှာ ပေါ့
ဒိုင် တွေ ပြော မ နေ နဲ့ မင်း တို့ ယောက်ျား တွေ က ဒီ လို အောကား လာ ပြီး ပြန် ပြီး အရေးယူ နေ တယ် ဒီ လောက် ဖြစ် တော့ မယ် အချိန် ညှပ် မ ရှိ ဘူး နော်
အထက် ကြီး ပါ ပြီး မှာ မြန်မာ နိုင်ငံ သား သမီး တွေ ဆို တာ တောင် အရမ်း ရှည် ကြ ပါ တယ် သား သမီး တွေ သူ အများကြီး အသက် မှာ စိတ် မ ရှိ ပါ ဘူး အေးချမ်း
---------------

မင်း အမေ က ကြီး လာ တယ် အား မ လား အောင် ပြန် အိုင် နေ သေး တယ် မြန်မာ ပြည် မှာ တော့ ခု ထိ မီး ပေး ပြီး မ လာ သေး ဘူး လား မ မှန် နေ တာ မီး ပျက် ရင် လည်း မ ပေး နဲ့ ချိန် တိုးတက် လုပ် နေ လိုက် ပျက် ၄ နာရီ ပဲ ပေး ပြီ
ပုံမှန် ပေး ပြီး တော့ လည်း တော့ ပျက် ချိန် မီး ပေး တာ လွန် လွန် လွန်း လို့ ပျက် တာ လား ဆောက်မီး က ချိန် လည်း ပျက် လိုက် နဲ့ အချိန် အိမ် ပြန် ပျက် လာ လိုက် ပျက် နေ ပြီ လာ ပျက် နေ တာ ၁ နာရီ လာ ပြီး ၅ နာရီ လောက် ပဲ ပေး ပြီး ၉ နာရီ ထိ ပြန် ပျက် တယ် ဖုန်း တောင် ခဏ ဖြတ် တယ် ၁ နာရီ လာ ပြီး ၁၀ မိန
---------------

တောင်ကြီးသား တယ်
ကိုယ့် ဘဘ တွေ မှာ မ သိ ဘူး လေ ဘာ ဖြစ် လို့ လဲ ဖာခံ မယ့် သူ တို့ ကို လည်း လှ ရ တာ ...
အားလုံး ဘုရင် စနစ် ထဲ ဘောမ အခွက် မ ဟုတ် တာ နော်
မ သိ တာ ကျ တော့ နင် တို့ အဖေ ပဲ ခွေးသူခိုး တွေ က ပို ကျွေး လိုက် တော့ ဒီ လောက် မ ရ တော့ ဘူး
စခ မျိုး စပ ဖြစ် နေ တာ အသေဆိုးနဲ့သေကြပါစေ
အကြမ်းဖက် နဲ့ မ တူ ရင် လည်း မ တူ ဘူး အသက် ခံ နေ ပြီ
လီး သတ်ပစ်
အမလေး တွေ ကို လည်း တရား ချ တယ် စောက်မြင်ကပ် လိုက် တာ ဆောက်မြင်ကပ် တယ် အရသာ ခံ ရ မယ် ဆို ပြီး ပြော သွား တာ ကို မ ပြော နဲ့ ဖော်လော်မော် ဖြစ် ချင် တာ ဟယ်
ခွ
---------------

ဘုန်းကြီး က တော့ မင်း တို့ က ဘယ်လို အဟုတ် မှာ လဲ ကျေနပ် မ ဆိုင် တာ နဲ့ တစ် ယောက် မှာ လေးစား ပါ တယ်
လူ က ရော နင် တို့ တစ် ယောက် က အစား ဖူး တုန်း က ကိုယ့် အများကြီး လို့ ရ တယ် ရှင်း ပေါ် က နေ မြန်မာ လူမျိုး တွေ က သူ တို့ နိုင်ငံ လေး တွေ က လုပ် ခဲ့ ရ လေ နေ လို့ အမေ မ ဟုတ် ဘူး တဲ့ သူ တွေ သူ တို့ အတွက် တောင် မ စား လို့ လား နော်
အခု မှ သန့် တာ ပဲ မြန်မာ ပြည် မှာ ပဲ လေ မအလ ကြီး ရာ ချင် စရာ
ပြော ချက် ရ တာ ပေါ့ အရှက်မရှိ တဲ့ ချီးစား ကြီး ဘာ လေးစား ထား လဲ မ သိ ဘူး လေ ၊ ဖင်ခံ စား ခဲ့ ပြီး ရင် နင့် အသက် နဲ့
---------------
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT$
```

## Testing No. 3

```
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT$ torchrun ./sample.py --out_dir=out-myHatespeech-char | tee myHatespeech_char_test3.log
Overriding: out_dir = out-myHatespeech-char
number of parameters: 10.75M
Loading meta from data/myHatespeech_char/meta.pkl...

မနက် ၅ နာရီ ခု ထိ မ လာ ဘူး ၅ မိနစ် ၅ နာရီ ထိ ပျက် သွား အောင် ပေး တာ လား လီး ပဲ ဟေ့ မအေလိုး တွေ
မီး ပျက် သွား ပြီ ပြန် ဖျက် သလို ပဲ
မီး လာ ရ မှာ မီး ပေး ပြီး ၅ မိနစ် တောင် မ ပြည့် တော့ ဘူး မအေလိုး တွေ မီး နာရီ ပြန် ပျက် တယ် ဆို တော့ မ သိ ရင် လည်း နာရီဝက် လည်း ပျက် ပြီ လီး ပဲ ဟေ့
မအေလိုး တွေ မီတာခ ကျတော့ ပြည်သူ တွေ အကုန်လုံး ခု မီး လာ မယ့် အချိန် မှန် အိပ် ပေး ပြီ နော် မီး ပျက် နေ တာ လား မအေလိုး တွေ ရေ
မအေလိုး တွေ တစ် နေကုန် ပျက် ၉ နာရီ လာ ပြီး ၉ နာရီ တော့ မှာ လာ ဖြတ် နေ တာ ပဲ
မအေလိုး တွေ အခု ထိ မ
---------------

နင့် လက်နက် တစ် ချောင်း ပါ တယ် နင် က ဖျက် နေ တာ လား စောက်ပြစ် ကျက်သရေတုံး တွေ
ဖင်ယား တယ် နော် လေ ယီး ပဲ လိ့ ကိုယ့် ပုံမှန် အောင် ပေး ပါ ဦး
အခွင့်အရေးယူ မှာ လား ဟင် မျက်နှာ ကို ကျက်သရေကိုတုံး တဲ့ ကောင် တွေ နောက် နေ ပြီ လီး ပဲ
မအေလိုး တွေ ရေ မီး ကို ၅ မိနစ် ပေး ပြီး လီး ပဲ လား ? မအေလိုး တွေ မြင် ရ အောင် မင်း တို့ တစ် နေ့ လုံး စောက်ပေါ တွေ ပေး မ နေ နဲ့ မ ေး နဲ့ လူကမွေးထားတာလား ဟ သူတောင်းစား တွေ နောက် လာ ရင် လည်း လူကြီး တွေ စောက်ကလေး တွေ ရေ တင် ကြ လာ ပြီ ပေါ့ 🤌
လီး လား ရုပ် က တော့ လီး ပဲ
သူ တို့ ထုတ
---------------

တော်တော် ကို နှိပ်စက် လိုက် တာ မအေလိုး မျိုး
ကလေး က မြန်မာ နိုင်ငံ က လည်း သူ က ပါးရိုက် ချင် စရာ
ကျွန်မ အရင် က ဘယ်လောက် များ ပါ လဲ ဆိုရင် ကိုယ့် အစီအစဉ်
အစ မ သိ တာ ကျ အောင် က ပဲ ဘုရား ဆို တာ ပါ ပဲ ရီ ချင် တယ်
ရွံ စရာ ကြီး ရယ် နော် နှစ် ယောက် လုံး ကို သက်သက် မ ကြာ ဘဲ အမှား တာ မ ဟုတ် ဘူး မယားငယ်မ လူ တွေ သွား တာ မ ဟုတ် ဘူး လေ နင့် ကို လည်း စောက်ချိုးမပြေ ဘူး
ခု မှ ကို ဘယ်လို အင်္ကျီ က သူများ လင် ယူ သွား လို့ လဲ ဟ 🙄
ခွေးသူတောင်းစား တွေ ပြော တာ ဘုရား စနစ် ကို လာ ပြီး စောက်ရူး စောက်သုံးမကျ တော့ ဘူး လာ
---------------

အခွင့် ရှိ တော့ မယ် ဘာ လုပ်လုပ် ပြ လဲ စောက်ရူး
အစ ကတည်းက မ ကြည့် ဘူး
အကြမ်းဖက် ကို ဖျက် စရာ ကောင်း လိုက် တာ ကို 😏 😏
အခု တော့ နော် ပွဲ က
ကလေး နဲ့ ကျပ်မပြည့် တဲ့ အချိန် ဆို ပြီး မှာ ကျေးဇူးတင် ပါ တယ် လူ က အခု တော့ ပရိတ်သတ် ချက် အဲ့လို မျိုး ကို ပျက် ထား တော့ ရူး နေ လိုက် ရင် ပူလောင်နှမလို့ ကျ သလို တံတား ကျ နေ တာ လား မြန်မာ မ တုံး နဲ့ ကို နာမည်ကြီး နဲ့ နေရာ မ ထူးဆန်း ဘူး လူပါးဝ တဲ့ ရေပေါ် ကို ဖျက်စီး အောင် လုပ် နေ တာ ကိုး မ ဟုတ် ဘူး အိမ်ထောင် ရင်း ရော ဘာ မှ မ ပြော နဲ့ စောက်ကျင့် သူတောင်းစား က သူ တွ
---------------

လီး လုပ် ပြီ လား
မိန်းမ တစ် လောက် မှ အား မ နေ နဲ့ ကိုမေကိုလိုး နေ ပြီ မီး က နေ ၅ နာရီ ခွဲ တည်းက ပျက် ချိန် တစ် နေကုန် ၁ နာရီ ခြား တစ် ခါ တည်း ပျက် တယ် ခု ထိ မ လာ သေး ဘူး လီး လုပ် နေ ကြ တာ လား မအေလိုး
လီး ပဲ မီး ပေး တဲ့ အချိန် လည်း ပျက် တဲ့ အချိန် မီး ပေး နေ တဲ့ အချိန် ကျ ပျက် တဲ့ အချိန် ဆို တာ က လည်း မ လာ ဘဲ ခိုး ဖျက် တဲ့ အချိန် ကျ လို့ မီး က အခု ထိ ပေး နေ တာ မအေလိုး တွေ ငါလိုး တွေ ရ
မီး လာ ရ မယ့် အချိန် ပျက် တယ် 😡 မီး က ခု ထိ မ လာ ဘူး နော် မီး က တော့ ဖျက် နေ တယ် မီး က ပူ လွန်း လို့ သေး တယ် အချိ
---------------

နင် တို့ တွေ ပဲ ကောင်းကောင်း ပါ တယ် တွေ့ မယ် သူ တို့ က လည်း လည်း လူလိမ် ကလိမ် ခွေးကမာလားလား ရဲ့
ငါ တို့ က အဲ့ လောက် ဖျက် နေ တာ လား
မိဘ လုပ်စာ လေး ကို ဖန်တီး ပါ တယ် လီး ပဲ နော်
ရူး နေ သေး တယ် လီး လို ပဲ အက လီး ပဲ ကို မ ရ ဘူး လား ? မသာမ ရေ
စောက်ပေါ အမျိုးယုတ်
ကြိုက် လိုက် ကြ ပါ နဲ့ မနက် က
အမ ရယ် ဒီ လောက် ဆို ပြီး များ စား ပေး ချင် တယ် 🙂😆😆
ငါ လည်း လာ ပြီး 2 ယောက် က ပြန် မ လာ ဘူး နောက်ဆုံး မ လာ ရ မှာ လေ
တကယ့် အချိန် လည်း မ လာ ပါ နဲ့ 🙂 ကျေးဇူး ပါ ဆို ပြီး လည်း ငါ တို့ တုန်း က ပို ပေး ရ မှာ ပေါ့
မင်း
---------------

ဒိုင် တွေ ကို အပေါ်ယံ ကြည့် တာ ကို လူ့ စွတ် ကို မ မြင် ဖူး ဘူး လား ?
စောက်ချိုးမပြေ ဘူး
စောက်ခွက် ကို မျက်နှာ ထက် အထာ နဲ့ ပစ်သတ် နေ တာ ကို ဒုက္ခ ပေး မယ် အချိန် မှာ မ ပေး နိုင် ဘူး ကွာ ။
စောက်ပို တွေ ရ မှာ ပေါ့
ဒိုင် တွေ ပြော မ နေ နဲ့ မင်း တို့ ယောက်ျား တွေ က ဒီ လို အောကား လာ ပြီး ပြန် ပြီး အရေးယူ နေ တယ် ဒီ လောက် ဖြစ် တော့ မယ် အချိန် ညှပ် မ ရှိ ဘူး နော်
အထက် ကြီး ပါ ပြီး မှာ မြန်မာ နိုင်ငံ သား သမီး တွေ ဆို တာ တောင် အရမ်း ရှည် ကြ ပါ တယ် သား သမီး တွေ သူ အများကြီး အသက် မှာ စိတ် မ ရှိ ပါ ဘူး အေးချမ်း
---------------

မင်း အမေ က ကြီး လာ တယ် အား မ လား အောင် ပြန် အိုင် နေ သေး တယ် မြန်မာ ပြည် မှာ တော့ ခု ထိ မီး ပေး ပြီး မ လာ သေး ဘူး လား မ မှန် နေ တာ မီး ပျက် ရင် လည်း မ ပေး နဲ့ ချိန် တိုးတက် လုပ် နေ လိုက် ပျက် ၄ နာရီ ပဲ ပေး ပြီ
ပုံမှန် ပေး ပြီး တော့ လည်း တော့ ပျက် ချိန် မီး ပေး တာ လွန် လွန် လွန်း လို့ ပျက် တာ လား ဆောက်မီး က ချိန် လည်း ပျက် လိုက် နဲ့ အချိန် အိမ် ပြန် ပျက် လာ လိုက် ပျက် နေ ပြီ လာ ပျက် နေ တာ ၁ နာရီ လာ ပြီး ၅ နာရီ လောက် ပဲ ပေး ပြီး ၉ နာရီ ထိ ပြန် ပျက် တယ် ဖုန်း တောင် ခဏ ဖြတ် တယ် ၁ နာရီ လာ ပြီး ၁၀ မိန
---------------

တောင်ကြီးသား တယ်
ကိုယ့် ဘဘ တွေ မှာ မ သိ ဘူး လေ ဘာ ဖြစ် လို့ လဲ ဖာခံ မယ့် သူ တို့ ကို လည်း လှ ရ တာ ...
အားလုံး ဘုရင် စနစ် ထဲ ဘောမ အခွက် မ ဟုတ် တာ နော်
မ သိ တာ ကျ တော့ နင် တို့ အဖေ ပဲ ခွေးသူခိုး တွေ က ပို ကျွေး လိုက် တော့ ဒီ လောက် မ ရ တော့ ဘူး
စခ မျိုး စပ ဖြစ် နေ တာ အသေဆိုးနဲ့သေကြပါစေ
အကြမ်းဖက် နဲ့ မ တူ ရင် လည်း မ တူ ဘူး အသက် ခံ နေ ပြီ
လီး သတ်ပစ်
အမလေး တွေ ကို လည်း တရား ချ တယ် စောက်မြင်ကပ် လိုက် တာ ဆောက်မြင်ကပ် တယ် အရသာ ခံ ရ မယ် ဆို ပြီး ပြော သွား တာ ကို မ ပြော နဲ့ ဖော်လော်မော် ဖြစ် ချင် တာ ဟယ်
ခွ
---------------

ဘုန်းကြီး က တော့ မင်း တို့ က ဘယ်လို အဟုတ် မှာ လဲ ကျေနပ် မ ဆိုင် တာ နဲ့ တစ် ယောက် မှာ လေးစား ပါ တယ်
လူ က ရော နင် တို့ တစ် ယောက် က အစား ဖူး တုန်း က ကိုယ့် အများကြီး လို့ ရ တယ် ရှင်း ပေါ် က နေ မြန်မာ လူမျိုး တွေ က သူ တို့ နိုင်ငံ လေး တွေ က လုပ် ခဲ့ ရ လေ နေ လို့ အမေ မ ဟုတ် ဘူး တဲ့ သူ တွေ သူ တို့ အတွက် တောင် မ စား လို့ လား နော်
အခု မှ သန့် တာ ပဲ မြန်မာ ပြည် မှာ ပဲ လေ မအလ ကြီး ရာ ချင် စရာ
ပြော ချက် ရ တာ ပေါ့ အရှက်မရှိ တဲ့ ချီးစား ကြီး ဘာ လေးစား ထား လဲ မ သိ ဘူး လေ ၊ ဖင်ခံ စား ခဲ့ ပြီး ရင် နင့် အသက် နဲ့
---------------
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT$
```

## Testing No. 4

```
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT$ torchrun ./sample.py --out_dir=out-myHatespeech-char | tee myHatespeech_char_test4.log
Overriding: out_dir = out-myHatespeech-char
number of parameters: 10.75M
Loading meta from data/myHatespeech_char/meta.pkl...

မနက် ၅ နာရီ ခု ထိ မ လာ ဘူး ၅ မိနစ် ၅ နာရီ ထိ ပျက် သွား အောင် ပေး တာ လား လီး ပဲ ဟေ့ မအေလိုး တွေ
မီး ပျက် သွား ပြီ ပြန် ဖျက် သလို ပဲ
မီး လာ ရ မှာ မီး ပေး ပြီး ၅ မိနစ် တောင် မ ပြည့် တော့ ဘူး မအေလိုး တွေ မီး နာရီ ပြန် ပျက် တယ် ဆို တော့ မ သိ ရင် လည်း နာရီဝက် လည်း ပျက် ပြီ လီး ပဲ ဟေ့
မအေလိုး တွေ မီတာခ ကျတော့ ပြည်သူ တွေ အကုန်လုံး ခု မီး လာ မယ့် အချိန် မှန် အိပ် ပေး ပြီ နော် မီး ပျက် နေ တာ လား မအေလိုး တွေ ရေ
မအေလိုး တွေ တစ် နေကုန် ပျက် ၉ နာရီ လာ ပြီး ၉ နာရီ တော့ မှာ လာ ဖြတ် နေ တာ ပဲ
မအေလိုး တွေ အခု ထိ မ
---------------

နင့် လက်နက် တစ် ချောင်း ပါ တယ် နင် က ဖျက် နေ တာ လား စောက်ပြစ် ကျက်သရေတုံး တွေ
ဖင်ယား တယ် နော် လေ ယီး ပဲ လိ့ ကိုယ့် ပုံမှန် အောင် ပေး ပါ ဦး
အခွင့်အရေးယူ မှာ လား ဟင် မျက်နှာ ကို ကျက်သရေကိုတုံး တဲ့ ကောင် တွေ နောက် နေ ပြီ လီး ပဲ
မအေလိုး တွေ ရေ မီး ကို ၅ မိနစ် ပေး ပြီး လီး ပဲ လား ? မအေလိုး တွေ မြင် ရ အောင် မင်း တို့ တစ် နေ့ လုံး စောက်ပေါ တွေ ပေး မ နေ နဲ့ မ ေး နဲ့ လူကမွေးထားတာလား ဟ သူတောင်းစား တွေ နောက် လာ ရင် လည်း လူကြီး တွေ စောက်ကလေး တွေ ရေ တင် ကြ လာ ပြီ ပေါ့ 🤌
လီး လား ရုပ် က တော့ လီး ပဲ
သူ တို့ ထုတ
---------------

တော်တော် ကို နှိပ်စက် လိုက် တာ မအေလိုး မျိုး
ကလေး က မြန်မာ နိုင်ငံ က လည်း သူ က ပါးရိုက် ချင် စရာ
ကျွန်မ အရင် က ဘယ်လောက် များ ပါ လဲ ဆိုရင် ကိုယ့် အစီအစဉ်
အစ မ သိ တာ ကျ အောင် က ပဲ ဘုရား ဆို တာ ပါ ပဲ ရီ ချင် တယ်
ရွံ စရာ ကြီး ရယ် နော် နှစ် ယောက် လုံး ကို သက်သက် မ ကြာ ဘဲ အမှား တာ မ ဟုတ် ဘူး မယားငယ်မ လူ တွေ သွား တာ မ ဟုတ် ဘူး လေ နင့် ကို လည်း စောက်ချိုးမပြေ ဘူး
ခု မှ ကို ဘယ်လို အင်္ကျီ က သူများ လင် ယူ သွား လို့ လဲ ဟ 🙄
ခွေးသူတောင်းစား တွေ ပြော တာ ဘုရား စနစ် ကို လာ ပြီး စောက်ရူး စောက်သုံးမကျ တော့ ဘူး လာ
---------------

အခွင့် ရှိ တော့ မယ် ဘာ လုပ်လုပ် ပြ လဲ စောက်ရူး
အစ ကတည်းက မ ကြည့် ဘူး
အကြမ်းဖက် ကို ဖျက် စရာ ကောင်း လိုက် တာ ကို 😏 😏
အခု တော့ နော် ပွဲ က
ကလေး နဲ့ ကျပ်မပြည့် တဲ့ အချိန် ဆို ပြီး မှာ ကျေးဇူးတင် ပါ တယ် လူ က အခု တော့ ပရိတ်သတ် ချက် အဲ့လို မျိုး ကို ပျက် ထား တော့ ရူး နေ လိုက် ရင် ပူလောင်နှမလို့ ကျ သလို တံတား ကျ နေ တာ လား မြန်မာ မ တုံး နဲ့ ကို နာမည်ကြီး နဲ့ နေရာ မ ထူးဆန်း ဘူး လူပါးဝ တဲ့ ရေပေါ် ကို ဖျက်စီး အောင် လုပ် နေ တာ ကိုး မ ဟုတ် ဘူး အိမ်ထောင် ရင်း ရော ဘာ မှ မ ပြော နဲ့ စောက်ကျင့် သူတောင်းစား က သူ တွ
---------------

လီး လုပ် ပြီ လား
မိန်းမ တစ် လောက် မှ အား မ နေ နဲ့ ကိုမေကိုလိုး နေ ပြီ မီး က နေ ၅ နာရီ ခွဲ တည်းက ပျက် ချိန် တစ် နေကုန် ၁ နာရီ ခြား တစ် ခါ တည်း ပျက် တယ် ခု ထိ မ လာ သေး ဘူး လီး လုပ် နေ ကြ တာ လား မအေလိုး
လီး ပဲ မီး ပေး တဲ့ အချိန် လည်း ပျက် တဲ့ အချိန် မီး ပေး နေ တဲ့ အချိန် ကျ ပျက် တဲ့ အချိန် ဆို တာ က လည်း မ လာ ဘဲ ခိုး ဖျက် တဲ့ အချိန် ကျ လို့ မီး က အခု ထိ ပေး နေ တာ မအေလိုး တွေ ငါလိုး တွေ ရ
မီး လာ ရ မယ့် အချိန် ပျက် တယ် 😡 မီး က ခု ထိ မ လာ ဘူး နော် မီး က တော့ ဖျက် နေ တယ် မီး က ပူ လွန်း လို့ သေး တယ် အချိ
---------------

နင် တို့ တွေ ပဲ ကောင်းကောင်း ပါ တယ် တွေ့ မယ် သူ တို့ က လည်း လည်း လူလိမ် ကလိမ် ခွေးကမာလားလား ရဲ့
ငါ တို့ က အဲ့ လောက် ဖျက် နေ တာ လား
မိဘ လုပ်စာ လေး ကို ဖန်တီး ပါ တယ် လီး ပဲ နော်
ရူး နေ သေး တယ် လီး လို ပဲ အက လီး ပဲ ကို မ ရ ဘူး လား ? မသာမ ရေ
စောက်ပေါ အမျိုးယုတ်
ကြိုက် လိုက် ကြ ပါ နဲ့ မနက် က
အမ ရယ် ဒီ လောက် ဆို ပြီး များ စား ပေး ချင် တယ် 🙂😆😆
ငါ လည်း လာ ပြီး 2 ယောက် က ပြန် မ လာ ဘူး နောက်ဆုံး မ လာ ရ မှာ လေ
တကယ့် အချိန် လည်း မ လာ ပါ နဲ့ 🙂 ကျေးဇူး ပါ ဆို ပြီး လည်း ငါ တို့ တုန်း က ပို ပေး ရ မှာ ပေါ့
မင်း
---------------

ဒိုင် တွေ ကို အပေါ်ယံ ကြည့် တာ ကို လူ့ စွတ် ကို မ မြင် ဖူး ဘူး လား ?
စောက်ချိုးမပြေ ဘူး
စောက်ခွက် ကို မျက်နှာ ထက် အထာ နဲ့ ပစ်သတ် နေ တာ ကို ဒုက္ခ ပေး မယ် အချိန် မှာ မ ပေး နိုင် ဘူး ကွာ ။
စောက်ပို တွေ ရ မှာ ပေါ့
ဒိုင် တွေ ပြော မ နေ နဲ့ မင်း တို့ ယောက်ျား တွေ က ဒီ လို အောကား လာ ပြီး ပြန် ပြီး အရေးယူ နေ တယ် ဒီ လောက် ဖြစ် တော့ မယ် အချိန် ညှပ် မ ရှိ ဘူး နော်
အထက် ကြီး ပါ ပြီး မှာ မြန်မာ နိုင်ငံ သား သမီး တွေ ဆို တာ တောင် အရမ်း ရှည် ကြ ပါ တယ် သား သမီး တွေ သူ အများကြီး အသက် မှာ စိတ် မ ရှိ ပါ ဘူး အေးချမ်း
---------------

မင်း အမေ က ကြီး လာ တယ် အား မ လား အောင် ပြန် အိုင် နေ သေး တယ် မြန်မာ ပြည် မှာ တော့ ခု ထိ မီး ပေး ပြီး မ လာ သေး ဘူး လား မ မှန် နေ တာ မီး ပျက် ရင် လည်း မ ပေး နဲ့ ချိန် တိုးတက် လုပ် နေ လိုက် ပျက် ၄ နာရီ ပဲ ပေး ပြီ
ပုံမှန် ပေး ပြီး တော့ လည်း တော့ ပျက် ချိန် မီး ပေး တာ လွန် လွန် လွန်း လို့ ပျက် တာ လား ဆောက်မီး က ချိန် လည်း ပျက် လိုက် နဲ့ အချိန် အိမ် ပြန် ပျက် လာ လိုက် ပျက် နေ ပြီ လာ ပျက် နေ တာ ၁ နာရီ လာ ပြီး ၅ နာရီ လောက် ပဲ ပေး ပြီး ၉ နာရီ ထိ ပြန် ပျက် တယ် ဖုန်း တောင် ခဏ ဖြတ် တယ် ၁ နာရီ လာ ပြီး ၁၀ မိန
---------------

တောင်ကြီးသား တယ်
ကိုယ့် ဘဘ တွေ မှာ မ သိ ဘူး လေ ဘာ ဖြစ် လို့ လဲ ဖာခံ မယ့် သူ တို့ ကို လည်း လှ ရ တာ ...
အားလုံး ဘုရင် စနစ် ထဲ ဘောမ အခွက် မ ဟုတ် တာ နော်
မ သိ တာ ကျ တော့ နင် တို့ အဖေ ပဲ ခွေးသူခိုး တွေ က ပို ကျွေး လိုက် တော့ ဒီ လောက် မ ရ တော့ ဘူး
စခ မျိုး စပ ဖြစ် နေ တာ အသေဆိုးနဲ့သေကြပါစေ
အကြမ်းဖက် နဲ့ မ တူ ရင် လည်း မ တူ ဘူး အသက် ခံ နေ ပြီ
လီး သတ်ပစ်
အမလေး တွေ ကို လည်း တရား ချ တယ် စောက်မြင်ကပ် လိုက် တာ ဆောက်မြင်ကပ် တယ် အရသာ ခံ ရ မယ် ဆို ပြီး ပြော သွား တာ ကို မ ပြော နဲ့ ဖော်လော်မော် ဖြစ် ချင် တာ ဟယ်
ခွ
---------------

ဘုန်းကြီး က တော့ မင်း တို့ က ဘယ်လို အဟုတ် မှာ လဲ ကျေနပ် မ ဆိုင် တာ နဲ့ တစ် ယောက် မှာ လေးစား ပါ တယ်
လူ က ရော နင် တို့ တစ် ယောက် က အစား ဖူး တုန်း က ကိုယ့် အများကြီး လို့ ရ တယ် ရှင်း ပေါ် က နေ မြန်မာ လူမျိုး တွေ က သူ တို့ နိုင်ငံ လေး တွေ က လုပ် ခဲ့ ရ လေ နေ လို့ အမေ မ ဟုတ် ဘူး တဲ့ သူ တွေ သူ တို့ အတွက် တောင် မ စား လို့ လား နော်
အခု မှ သန့် တာ ပဲ မြန်မာ ပြည် မှာ ပဲ လေ မအလ ကြီး ရာ ချင် စရာ
ပြော ချက် ရ တာ ပေါ့ အရှက်မရှိ တဲ့ ချီးစား ကြီး ဘာ လေးစား ထား လဲ မ သိ ဘူး လေ ၊ ဖင်ခံ စား ခဲ့ ပြီး ရင် နင့် အသက် နဲ့
---------------
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT$
```

## Testing No. 5

```
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT$ torchrun ./sample.py --out_dir=out-myHatespeech-char | tee myHatespeech_char_test5.log
Overriding: out_dir = out-myHatespeech-char
number of parameters: 10.75M
Loading meta from data/myHatespeech_char/meta.pkl...

မနက် ၅ နာရီ ခု ထိ မ လာ ဘူး ၅ မိနစ် ၅ နာရီ ထိ ပျက် သွား အောင် ပေး တာ လား လီး ပဲ ဟေ့ မအေလိုး တွေ
မီး ပျက် သွား ပြီ ပြန် ဖျက် သလို ပဲ
မီး လာ ရ မှာ မီး ပေး ပြီး ၅ မိနစ် တောင် မ ပြည့် တော့ ဘူး မအေလိုး တွေ မီး နာရီ ပြန် ပျက် တယ် ဆို တော့ မ သိ ရင် လည်း နာရီဝက် လည်း ပျက် ပြီ လီး ပဲ ဟေ့
မအေလိုး တွေ မီတာခ ကျတော့ ပြည်သူ တွေ အကုန်လုံး ခု မီး လာ မယ့် အချိန် မှန် အိပ် ပေး ပြီ နော် မီး ပျက် နေ တာ လား မအေလိုး တွေ ရေ
မအေလိုး တွေ တစ် နေကုန် ပျက် ၉ နာရီ လာ ပြီး ၉ နာရီ တော့ မှာ လာ ဖြတ် နေ တာ ပဲ
မအေလိုး တွေ အခု ထိ မ
---------------

နင့် လက်နက် တစ် ချောင်း ပါ တယ် နင် က ဖျက် နေ တာ လား စောက်ပြစ် ကျက်သရေတုံး တွေ
ဖင်ယား တယ် နော် လေ ယီး ပဲ လိ့ ကိုယ့် ပုံမှန် အောင် ပေး ပါ ဦး
အခွင့်အရေးယူ မှာ လား ဟင် မျက်နှာ ကို ကျက်သရေကိုတုံး တဲ့ ကောင် တွေ နောက် နေ ပြီ လီး ပဲ
မအေလိုး တွေ ရေ မီး ကို ၅ မိနစ် ပေး ပြီး လီး ပဲ လား ? မအေလိုး တွေ မြင် ရ အောင် မင်း တို့ တစ် နေ့ လုံး စောက်ပေါ တွေ ပေး မ နေ နဲ့ မ ေး နဲ့ လူကမွေးထားတာလား ဟ သူတောင်းစား တွေ နောက် လာ ရင် လည်း လူကြီး တွေ စောက်ကလေး တွေ ရေ တင် ကြ လာ ပြီ ပေါ့ 🤌
လီး လား ရုပ် က တော့ လီး ပဲ
သူ တို့ ထုတ
---------------

တော်တော် ကို နှိပ်စက် လိုက် တာ မအေလိုး မျိုး
ကလေး က မြန်မာ နိုင်ငံ က လည်း သူ က ပါးရိုက် ချင် စရာ
ကျွန်မ အရင် က ဘယ်လောက် များ ပါ လဲ ဆိုရင် ကိုယ့် အစီအစဉ်
အစ မ သိ တာ ကျ အောင် က ပဲ ဘုရား ဆို တာ ပါ ပဲ ရီ ချင် တယ်
ရွံ စရာ ကြီး ရယ် နော် နှစ် ယောက် လုံး ကို သက်သက် မ ကြာ ဘဲ အမှား တာ မ ဟုတ် ဘူး မယားငယ်မ လူ တွေ သွား တာ မ ဟုတ် ဘူး လေ နင့် ကို လည်း စောက်ချိုးမပြေ ဘူး
ခု မှ ကို ဘယ်လို အင်္ကျီ က သူများ လင် ယူ သွား လို့ လဲ ဟ 🙄
ခွေးသူတောင်းစား တွေ ပြော တာ ဘုရား စနစ် ကို လာ ပြီး စောက်ရူး စောက်သုံးမကျ တော့ ဘူး လာ
---------------

အခွင့် ရှိ တော့ မယ် ဘာ လုပ်လုပ် ပြ လဲ စောက်ရူး
အစ ကတည်းက မ ကြည့် ဘူး
အကြမ်းဖက် ကို ဖျက် စရာ ကောင်း လိုက် တာ ကို 😏 😏
အခု တော့ နော် ပွဲ က
ကလေး နဲ့ ကျပ်မပြည့် တဲ့ အချိန် ဆို ပြီး မှာ ကျေးဇူးတင် ပါ တယ် လူ က အခု တော့ ပရိတ်သတ် ချက် အဲ့လို မျိုး ကို ပျက် ထား တော့ ရူး နေ လိုက် ရင် ပူလောင်နှမလို့ ကျ သလို တံတား ကျ နေ တာ လား မြန်မာ မ တုံး နဲ့ ကို နာမည်ကြီး နဲ့ နေရာ မ ထူးဆန်း ဘူး လူပါးဝ တဲ့ ရေပေါ် ကို ဖျက်စီး အောင် လုပ် နေ တာ ကိုး မ ဟုတ် ဘူး အိမ်ထောင် ရင်း ရော ဘာ မှ မ ပြော နဲ့ စောက်ကျင့် သူတောင်းစား က သူ တွ
---------------

လီး လုပ် ပြီ လား
မိန်းမ တစ် လောက် မှ အား မ နေ နဲ့ ကိုမေကိုလိုး နေ ပြီ မီး က နေ ၅ နာရီ ခွဲ တည်းက ပျက် ချိန် တစ် နေကုန် ၁ နာရီ ခြား တစ် ခါ တည်း ပျက် တယ် ခု ထိ မ လာ သေး ဘူး လီး လုပ် နေ ကြ တာ လား မအေလိုး
လီး ပဲ မီး ပေး တဲ့ အချိန် လည်း ပျက် တဲ့ အချိန် မီး ပေး နေ တဲ့ အချိန် ကျ ပျက် တဲ့ အချိန် ဆို တာ က လည်း မ လာ ဘဲ ခိုး ဖျက် တဲ့ အချိန် ကျ လို့ မီး က အခု ထိ ပေး နေ တာ မအေလိုး တွေ ငါလိုး တွေ ရ
မီး လာ ရ မယ့် အချိန် ပျက် တယ် 😡 မီး က ခု ထိ မ လာ ဘူး နော် မီး က တော့ ဖျက် နေ တယ် မီး က ပူ လွန်း လို့ သေး တယ် အချိ
---------------

နင် တို့ တွေ ပဲ ကောင်းကောင်း ပါ တယ် တွေ့ မယ် သူ တို့ က လည်း လည်း လူလိမ် ကလိမ် ခွေးကမာလားလား ရဲ့
ငါ တို့ က အဲ့ လောက် ဖျက် နေ တာ လား
မိဘ လုပ်စာ လေး ကို ဖန်တီး ပါ တယ် လီး ပဲ နော်
ရူး နေ သေး တယ် လီး လို ပဲ အက လီး ပဲ ကို မ ရ ဘူး လား ? မသာမ ရေ
စောက်ပေါ အမျိုးယုတ်
ကြိုက် လိုက် ကြ ပါ နဲ့ မနက် က
အမ ရယ် ဒီ လောက် ဆို ပြီး များ စား ပေး ချင် တယ် 🙂😆😆
ငါ လည်း လာ ပြီး 2 ယောက် က ပြန် မ လာ ဘူး နောက်ဆုံး မ လာ ရ မှာ လေ
တကယ့် အချိန် လည်း မ လာ ပါ နဲ့ 🙂 ကျေးဇူး ပါ ဆို ပြီး လည်း ငါ တို့ တုန်း က ပို ပေး ရ မှာ ပေါ့
မင်း
---------------

ဒိုင် တွေ ကို အပေါ်ယံ ကြည့် တာ ကို လူ့ စွတ် ကို မ မြင် ဖူး ဘူး လား ?
စောက်ချိုးမပြေ ဘူး
စောက်ခွက် ကို မျက်နှာ ထက် အထာ နဲ့ ပစ်သတ် နေ တာ ကို ဒုက္ခ ပေး မယ် အချိန် မှာ မ ပေး နိုင် ဘူး ကွာ ။
စောက်ပို တွေ ရ မှာ ပေါ့
ဒိုင် တွေ ပြော မ နေ နဲ့ မင်း တို့ ယောက်ျား တွေ က ဒီ လို အောကား လာ ပြီး ပြန် ပြီး အရေးယူ နေ တယ် ဒီ လောက် ဖြစ် တော့ မယ် အချိန် ညှပ် မ ရှိ ဘူး နော်
အထက် ကြီး ပါ ပြီး မှာ မြန်မာ နိုင်ငံ သား သမီး တွေ ဆို တာ တောင် အရမ်း ရှည် ကြ ပါ တယ် သား သမီး တွေ သူ အများကြီး အသက် မှာ စိတ် မ ရှိ ပါ ဘူး အေးချမ်း
---------------

မင်း အမေ က ကြီး လာ တယ် အား မ လား အောင် ပြန် အိုင် နေ သေး တယ် မြန်မာ ပြည် မှာ တော့ ခု ထိ မီး ပေး ပြီး မ လာ သေး ဘူး လား မ မှန် နေ တာ မီး ပျက် ရင် လည်း မ ပေး နဲ့ ချိန် တိုးတက် လုပ် နေ လိုက် ပျက် ၄ နာရီ ပဲ ပေး ပြီ
ပုံမှန် ပေး ပြီး တော့ လည်း တော့ ပျက် ချိန် မီး ပေး တာ လွန် လွန် လွန်း လို့ ပျက် တာ လား ဆောက်မီး က ချိန် လည်း ပျက် လိုက် နဲ့ အချိန် အိမ် ပြန် ပျက် လာ လိုက် ပျက် နေ ပြီ လာ ပျက် နေ တာ ၁ နာရီ လာ ပြီး ၅ နာရီ လောက် ပဲ ပေး ပြီး ၉ နာရီ ထိ ပြန် ပျက် တယ် ဖုန်း တောင် ခဏ ဖြတ် တယ် ၁ နာရီ လာ ပြီး ၁၀ မိန
---------------

တောင်ကြီးသား တယ်
ကိုယ့် ဘဘ တွေ မှာ မ သိ ဘူး လေ ဘာ ဖြစ် လို့ လဲ ဖာခံ မယ့် သူ တို့ ကို လည်း လှ ရ တာ ...
အားလုံး ဘုရင် စနစ် ထဲ ဘောမ အခွက် မ ဟုတ် တာ နော်
မ သိ တာ ကျ တော့ နင် တို့ အဖေ ပဲ ခွေးသူခိုး တွေ က ပို ကျွေး လိုက် တော့ ဒီ လောက် မ ရ တော့ ဘူး
စခ မျိုး စပ ဖြစ် နေ တာ အသေဆိုးနဲ့သေကြပါစေ
အကြမ်းဖက် နဲ့ မ တူ ရင် လည်း မ တူ ဘူး အသက် ခံ နေ ပြီ
လီး သတ်ပစ်
အမလေး တွေ ကို လည်း တရား ချ တယ် စောက်မြင်ကပ် လိုက် တာ ဆောက်မြင်ကပ် တယ် အရသာ ခံ ရ မယ် ဆို ပြီး ပြော သွား တာ ကို မ ပြော နဲ့ ဖော်လော်မော် ဖြစ် ချင် တာ ဟယ်
ခွ
---------------

ဘုန်းကြီး က တော့ မင်း တို့ က ဘယ်လို အဟုတ် မှာ လဲ ကျေနပ် မ ဆိုင် တာ နဲ့ တစ် ယောက် မှာ လေးစား ပါ တယ်
လူ က ရော နင် တို့ တစ် ယောက် က အစား ဖူး တုန်း က ကိုယ့် အများကြီး လို့ ရ တယ် ရှင်း ပေါ် က နေ မြန်မာ လူမျိုး တွေ က သူ တို့ နိုင်ငံ လေး တွေ က လုပ် ခဲ့ ရ လေ နေ လို့ အမေ မ ဟုတ် ဘူး တဲ့ သူ တွေ သူ တို့ အတွက် တောင် မ စား လို့ လား နော်
အခု မှ သန့် တာ ပဲ မြန်မာ ပြည် မှာ ပဲ လေ မအလ ကြီး ရာ ချင် စရာ
ပြော ချက် ရ တာ ပေါ့ အရှက်မရှိ တဲ့ ချီးစား ကြီး ဘာ လေးစား ထား လဲ မ သိ ဘူး လေ ၊ ဖင်ခံ စား ခဲ့ ပြီး ရင် နင့် အသက် နဲ့
---------------
(nanoGPT) ye@lst-gpu-3090:~/tool/nanoGPT$
```

## To Do

- When I have time, preparing a Jupyter Notebook for some testing
- I also wish to do, manual evaluation
  
## Reference

1. [https://github.com/ye-kyaw-thu/myPoetry](https://github.com/ye-kyaw-thu/myPoetry)
2. [https://github.com/karpathy/nanoGPT](https://github.com/karpathy/nanoGPT)
