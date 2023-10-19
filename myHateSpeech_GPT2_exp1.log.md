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

လိုအပ်ရင် ပြန် refer လုပ်ဖို့အတွက် ...  

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

တကယ်တမ်းက အထက်ပါ nanoGPT repository ကို အခြေခံပြီးတော့ မြန်မာကဗျာအတွက် စမ်းထားတဲ့ repository က ရှိပြီးသားမို့ အဲဒါပဲ clone လုပ်တာနဲ့တင် အိုကေမယ်လို့ ထင်တယ်။  

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

အဆင်ပြေမယ်လို့ ထင်တယ်။ corpus တစ်ခုလုံးကို cleaning လုပ်ခဲ့ ...  

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

