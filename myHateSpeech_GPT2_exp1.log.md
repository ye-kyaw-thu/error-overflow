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

