# Testing LibMultiLabel Log

## Create a New Enviornment

```
(base) rnd@gpu:~$ conda create -n LibMultiLabel python=3.8
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 23.3.1

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/rnd/anaconda3/envs/LibMultiLabel

  added / updated specs:
    - python=3.8


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    libffi-3.4.4               |       h6a678d5_0         142 KB
    xz-5.4.2                   |       h5eee18b_0         642 KB
    ------------------------------------------------------------
                                           Total:         784 KB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-5.1-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2023.01.10-h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.38-h1181459_1
  libffi             pkgs/main/linux-64::libffi-3.4.4-h6a678d5_0
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-11.2.0-h1234567_1
  libgomp            pkgs/main/linux-64::libgomp-11.2.0-h1234567_1
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-11.2.0-h1234567_1
  ncurses            pkgs/main/linux-64::ncurses-6.4-h6a678d5_0
  openssl            pkgs/main/linux-64::openssl-1.1.1t-h7f8727e_0
  pip                pkgs/main/linux-64::pip-23.0.1-py38h06a4308_0
  python             pkgs/main/linux-64::python-3.8.16-h7a1cb2a_3
  readline           pkgs/main/linux-64::readline-8.2-h5eee18b_0
  setuptools         pkgs/main/linux-64::setuptools-66.0.0-py38h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.41.2-h5eee18b_0
  tk                 pkgs/main/linux-64::tk-8.6.12-h1ccaba5_0
  wheel              pkgs/main/linux-64::wheel-0.38.4-py38h06a4308_0
  xz                 pkgs/main/linux-64::xz-5.4.2-h5eee18b_0
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
libffi-3.4.4         | 142 KB    | ############################################################## | 100%
xz-5.4.2             | 642 KB    | ############################################################## | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate LibMultiLabel
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```

```
(base) rnd@gpu:~$ conda activate LibMultiLabel
(LibMultiLabel) rnd@gpu:~$
```

## Run git clone

```
(LibMultiLabel) rnd@gpu:~/tool$ git clone https://github.com/ASUS-AICS/LibMultiLabel.git
Cloning into 'LibMultiLabel'...
remote: Enumerating objects: 9424, done.
remote: Counting objects: 100% (1187/1187), done.
remote: Compressing objects: 100% (413/413), done.
remote: Total 9424 (delta 828), reused 1091 (delta 769), pack-reused 8237
Receiving objects: 100% (9424/9424), 1.49 MiB | 514.00 KiB/s, done.
Resolving deltas: 100% (6404/6404), done.
(LibMultiLabel) rnd@gpu:~/tool$ cd LibMultiLabel/
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel$ ls
docs            LICENSE            README.md                          search_params.py
example_config  linear_trainer.py  requirements_parameter_search.txt  setup.cfg
__init__.py     main.py            requirements.txt                   tests
libmultilabel   pyproject.toml     run_and_store_results.py           torch_trainer.py
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel$
```

## Install the Latest Version

```
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel$ pip3 install -r requirements.txt
Collecting nltk
  Using cached nltk-3.8.1-py3-none-any.whl (1.5 MB)
Collecting pandas>1.3.0
  Downloading pandas-2.0.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (12.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 12.3/12.3 MB 46.0 kB/s eta 0:00:00
Collecting PyYAML
  Using cached PyYAML-6.0-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_12_x86_64.manylinux2010_x86_64.whl (701 kB)
Collecting scikit-learn
  Using cached scikit_learn-1.2.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (9.8 MB)
Collecting torch>=1.13.1
  Downloading torch-2.0.1-cp38-cp38-manylinux1_x86_64.whl (619.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 619.9/619.9 MB 1.5 MB/s eta 0:00:00
Collecting torchmetrics==0.10.3
  Downloading torchmetrics-0.10.3-py3-none-any.whl (529 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 529.7/529.7 kB 2.7 MB/s eta 0:00:00
Collecting torchtext>=0.13.0
  Downloading torchtext-0.15.2-cp38-cp38-manylinux1_x86_64.whl (2.0 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.0/2.0 MB 4.8 MB/s eta 0:00:00
Collecting pytorch-lightning==1.7.7
  Downloading pytorch_lightning-1.7.7-py3-none-any.whl (708 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 708.1/708.1 kB 3.8 MB/s eta 0:00:00
Collecting tqdm
  Using cached tqdm-4.65.0-py3-none-any.whl (77 kB)
Collecting liblinear-multicore
  Downloading liblinear-multicore-2.46.1.tar.gz (48 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 48.9/48.9 kB 1.4 MB/s eta 0:00:00
  Preparing metadata (setup.py) ... done
Collecting numba
  Downloading numba-0.57.0-cp38-cp38-manylinux2014_x86_64.manylinux_2_17_x86_64.whl (3.6 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.6/3.6 MB 4.0 MB/s eta 0:00:00
Collecting scipy
  Using cached scipy-1.10.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (34.5 MB)
Collecting transformers
  Downloading transformers-4.29.2-py3-none-any.whl (7.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 7.1/7.1 MB 2.3 MB/s eta 0:00:00
Collecting packaging
  Using cached packaging-23.1-py3-none-any.whl (48 kB)
Collecting typing-extensions
  Using cached typing_extensions-4.5.0-py3-none-any.whl (27 kB)
Collecting numpy>=1.17.2
  Downloading numpy-1.24.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (17.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 17.3/17.3 MB 3.3 MB/s eta 0:00:00
Collecting tensorboard>=2.9.1
  Downloading tensorboard-2.13.0-py3-none-any.whl (5.6 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 5.6/5.6 MB 4.5 MB/s eta 0:00:00
Collecting fsspec[http]!=2021.06.0,>=2021.05.0
  Downloading fsspec-2023.5.0-py3-none-any.whl (160 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 160.1/160.1 kB 2.6 MB/s eta 0:00:00
Collecting pyDeprecate>=0.3.1
  Downloading pyDeprecate-0.3.2-py3-none-any.whl (10 kB)
Collecting joblib
  Using cached joblib-1.2.0-py3-none-any.whl (297 kB)
Collecting click
  Using cached click-8.1.3-py3-none-any.whl (96 kB)
Collecting regex>=2021.8.3
  Downloading regex-2023.5.5-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (771 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 771.9/771.9 kB 4.6 MB/s eta 0:00:00
Collecting python-dateutil>=2.8.2
  Using cached python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
Collecting pytz>=2020.1
  Using cached pytz-2023.3-py2.py3-none-any.whl (502 kB)
Collecting tzdata>=2022.1
  Using cached tzdata-2023.3-py2.py3-none-any.whl (341 kB)
Collecting threadpoolctl>=2.0.0
  Using cached threadpoolctl-3.1.0-py3-none-any.whl (14 kB)
Collecting triton==2.0.0
  Using cached triton-2.0.0-1-cp38-cp38-manylinux2014_x86_64.manylinux_2_17_x86_64.whl (63.2 MB)
Collecting nvidia-cusparse-cu11==11.7.4.91
  Using cached nvidia_cusparse_cu11-11.7.4.91-py3-none-manylinux1_x86_64.whl (173.2 MB)
Collecting jinja2
  Using cached Jinja2-3.1.2-py3-none-any.whl (133 kB)
Collecting nvidia-cudnn-cu11==8.5.0.96
  Using cached nvidia_cudnn_cu11-8.5.0.96-2-py3-none-manylinux1_x86_64.whl (557.1 MB)
Collecting nvidia-nccl-cu11==2.14.3
  Using cached nvidia_nccl_cu11-2.14.3-py3-none-manylinux1_x86_64.whl (177.1 MB)
Collecting nvidia-nvtx-cu11==11.7.91
  Using cached nvidia_nvtx_cu11-11.7.91-py3-none-manylinux1_x86_64.whl (98 kB)
Collecting nvidia-cuda-nvrtc-cu11==11.7.99
  Using cached nvidia_cuda_nvrtc_cu11-11.7.99-2-py3-none-manylinux1_x86_64.whl (21.0 MB)
Collecting nvidia-cusolver-cu11==11.4.0.1
  Using cached nvidia_cusolver_cu11-11.4.0.1-2-py3-none-manylinux1_x86_64.whl (102.6 MB)
Collecting nvidia-cuda-cupti-cu11==11.7.101
  Using cached nvidia_cuda_cupti_cu11-11.7.101-py3-none-manylinux1_x86_64.whl (11.8 MB)
Collecting nvidia-cuda-runtime-cu11==11.7.99
  Using cached nvidia_cuda_runtime_cu11-11.7.99-py3-none-manylinux1_x86_64.whl (849 kB)
Collecting nvidia-cufft-cu11==10.9.0.58
  Using cached nvidia_cufft_cu11-10.9.0.58-py3-none-manylinux1_x86_64.whl (168.4 MB)
Collecting networkx
  Using cached networkx-3.1-py3-none-any.whl (2.1 MB)
Collecting nvidia-curand-cu11==10.2.10.91
  Using cached nvidia_curand_cu11-10.2.10.91-py3-none-manylinux1_x86_64.whl (54.6 MB)
Collecting nvidia-cublas-cu11==11.10.3.66
  Using cached nvidia_cublas_cu11-11.10.3.66-py3-none-manylinux1_x86_64.whl (317.1 MB)
Collecting filelock
  Using cached filelock-3.12.0-py3-none-any.whl (10 kB)
Collecting sympy
  Downloading sympy-1.12-py3-none-any.whl (5.7 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 5.7/5.7 MB 4.2 MB/s eta 0:00:00
Requirement already satisfied: setuptools in /home/rnd/anaconda3/envs/LibMultiLabel/lib/python3.8/site-packages (from nvidia-cublas-cu11==11.10.3.66->torch>=1.13.1->-r requirements.txt (line 5)) (66.0.0)
Requirement already satisfied: wheel in /home/rnd/anaconda3/envs/LibMultiLabel/lib/python3.8/site-packages (from nvidia-cublas-cu11==11.10.3.66->torch>=1.13.1->-r requirements.txt (line 5)) (0.38.4)
Collecting cmake
  Using cached cmake-3.26.3-py2.py3-none-manylinux2014_x86_64.manylinux_2_17_x86_64.whl (24.0 MB)
Collecting lit
  Downloading lit-16.0.5.tar.gz (138 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 138.0/138.0 kB 3.5 MB/s eta 0:00:00
  Preparing metadata (setup.py) ... done
Collecting requests
  Downloading requests-2.30.0-py3-none-any.whl (62 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 62.5/62.5 kB 712.6 kB/s eta 0:00:00
Collecting torchdata==0.6.1
  Downloading torchdata-0.6.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.6 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.6/4.6 MB 5.8 MB/s eta 0:00:00
Collecting urllib3>=1.25
  Downloading urllib3-2.0.2-py3-none-any.whl (123 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 123.2/123.2 kB 3.0 MB/s eta 0:00:00
Collecting llvmlite<0.41,>=0.40.0dev0
  Downloading llvmlite-0.40.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (42.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42.1/42.1 MB 4.7 MB/s eta 0:00:00
Collecting importlib-metadata
  Downloading importlib_metadata-6.6.0-py3-none-any.whl (22 kB)
Collecting huggingface-hub<1.0,>=0.14.1
  Downloading huggingface_hub-0.14.1-py3-none-any.whl (224 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 224.5/224.5 kB 5.8 MB/s eta 0:00:00
Collecting tokenizers!=0.11.3,<0.14,>=0.11.1
  Using cached tokenizers-0.13.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (7.8 MB)
Collecting aiohttp!=4.0.0a0,!=4.0.0a1
  Using cached aiohttp-3.8.4-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.0 MB)
Collecting six>=1.5
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Collecting tensorboard-data-server<0.8.0,>=0.7.0
  Using cached tensorboard_data_server-0.7.0-py3-none-manylinux2014_x86_64.whl (6.6 MB)
Collecting protobuf>=3.19.6
  Downloading protobuf-4.23.1-cp37-abi3-manylinux2014_x86_64.whl (304 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 304.5/304.5 kB 6.4 MB/s eta 0:00:00
Collecting google-auth-oauthlib<1.1,>=0.5
  Downloading google_auth_oauthlib-1.0.0-py2.py3-none-any.whl (18 kB)
Collecting grpcio>=1.48.2
  Downloading grpcio-1.54.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (5.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 5.1/5.1 MB 10.0 MB/s eta 0:00:00
Collecting absl-py>=0.4
  Using cached absl_py-1.4.0-py3-none-any.whl (126 kB)
Collecting werkzeug>=1.0.1
  Downloading Werkzeug-2.3.4-py3-none-any.whl (242 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 242.5/242.5 kB 5.3 MB/s eta 0:00:00
Collecting markdown>=2.6.8
  Using cached Markdown-3.4.3-py3-none-any.whl (93 kB)
Collecting google-auth<3,>=1.6.3
  Downloading google_auth-2.18.1-py2.py3-none-any.whl (178 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 178.9/178.9 kB 2.0 MB/s eta 0:00:00
Collecting charset-normalizer<4,>=2
  Using cached charset_normalizer-3.1.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (195 kB)
Collecting idna<4,>=2.5
  Using cached idna-3.4-py3-none-any.whl (61 kB)
Collecting certifi>=2017.4.17
  Downloading certifi-2023.5.7-py3-none-any.whl (156 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 157.0/157.0 kB 2.6 MB/s eta 0:00:00
Collecting zipp>=0.5
  Using cached zipp-3.15.0-py3-none-any.whl (6.8 kB)
Collecting MarkupSafe>=2.0
  Using cached MarkupSafe-2.1.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (25 kB)
Collecting mpmath>=0.19
  Using cached mpmath-1.3.0-py3-none-any.whl (536 kB)
Collecting yarl<2.0,>=1.0
  Downloading yarl-1.9.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (266 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 266.9/266.9 kB 4.5 MB/s eta 0:00:00
Collecting aiosignal>=1.1.2
  Using cached aiosignal-1.3.1-py3-none-any.whl (7.6 kB)
Collecting attrs>=17.3.0
  Using cached attrs-23.1.0-py3-none-any.whl (61 kB)
Collecting multidict<7.0,>=4.5
  Using cached multidict-6.0.4-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (121 kB)
Collecting async-timeout<5.0,>=4.0.0a3
  Using cached async_timeout-4.0.2-py3-none-any.whl (5.8 kB)
Collecting frozenlist>=1.1.1
  Using cached frozenlist-1.3.3-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (161 kB)
Collecting urllib3>=1.25
  Using cached urllib3-1.26.15-py2.py3-none-any.whl (140 kB)
Collecting cachetools<6.0,>=2.0.0
  Using cached cachetools-5.3.0-py3-none-any.whl (9.3 kB)
Collecting rsa<5,>=3.1.4
  Using cached rsa-4.9-py3-none-any.whl (34 kB)
Collecting pyasn1-modules>=0.2.1
  Downloading pyasn1_modules-0.3.0-py2.py3-none-any.whl (181 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 181.3/181.3 kB 1.7 MB/s eta 0:00:00
Collecting requests-oauthlib>=0.7.0
  Using cached requests_oauthlib-1.3.1-py2.py3-none-any.whl (23 kB)
Collecting pyasn1<0.6.0,>=0.4.6
  Downloading pyasn1-0.5.0-py2.py3-none-any.whl (83 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 83.9/83.9 kB 1.4 MB/s eta 0:00:00
Collecting oauthlib>=3.0.0
  Using cached oauthlib-3.2.2-py3-none-any.whl (151 kB)
Building wheels for collected packages: liblinear-multicore, lit
  Building wheel for liblinear-multicore (setup.py) ... done
  Created wheel for liblinear-multicore: filename=liblinear_multicore-2.46.1-cp38-cp38-linux_x86_64.whl size=182196 sha256=60418c1aaf7084e668af36347ed7be1834c38230492a30b0c818db1548a371a6
  Stored in directory: /home/rnd/.cache/pip/wheels/aa/b5/74/9b0ab93681bfedff3d1447d7dcfd678010f896043f7c274e3b
  Building wheel for lit (setup.py) ... done
  Created wheel for lit: filename=lit-16.0.5-py3-none-any.whl size=88174 sha256=09b0c15167543e454b0077ce9e3c1182b15accb51fe512a47bb9bfd301a463d7
  Stored in directory: /home/rnd/.cache/pip/wheels/a6/05/82/bbf80d224f6ad6c764404f26aba7b644bfa77b45dcc1c17f5a
Successfully built liblinear-multicore lit
Installing collected packages: tokenizers, pytz, mpmath, lit, cmake, zipp, urllib3, tzdata, typing-extensions, tqdm, threadpoolctl, tensorboard-data-server, sympy, six, regex, PyYAML, pyDeprecate, pyasn1, protobuf, packaging, oauthlib, nvidia-nvtx-cu11, nvidia-nccl-cu11, nvidia-cusparse-cu11, nvidia-curand-cu11, nvidia-cufft-cu11, nvidia-cuda-runtime-cu11, nvidia-cuda-nvrtc-cu11, nvidia-cuda-cupti-cu11, nvidia-cublas-cu11, numpy, networkx, multidict, MarkupSafe, llvmlite, joblib, idna, grpcio, fsspec, frozenlist, filelock, click, charset-normalizer, certifi, cachetools, attrs, async-timeout, absl-py, yarl, werkzeug, scipy, rsa, requests, python-dateutil, pyasn1-modules, nvidia-cusolver-cu11, nvidia-cudnn-cu11, nltk, jinja2, importlib-metadata, aiosignal, scikit-learn, requests-oauthlib, pandas, numba, markdown, liblinear-multicore, huggingface-hub, google-auth, aiohttp, transformers, google-auth-oauthlib, tensorboard, triton, torch, torchmetrics, torchdata, torchtext, pytorch-lightning
Successfully installed MarkupSafe-2.1.2 PyYAML-6.0 absl-py-1.4.0 aiohttp-3.8.4 aiosignal-1.3.1 async-timeout-4.0.2 attrs-23.1.0 cachetools-5.3.0 certifi-2023.5.7 charset-normalizer-3.1.0 click-8.1.3 cmake-3.26.3 filelock-3.12.0 frozenlist-1.3.3 fsspec-2023.5.0 google-auth-2.18.1 google-auth-oauthlib-1.0.0 grpcio-1.54.2 huggingface-hub-0.14.1 idna-3.4 importlib-metadata-6.6.0 jinja2-3.1.2 joblib-1.2.0 liblinear-multicore-2.46.1 lit-16.0.5 llvmlite-0.40.0 markdown-3.4.3 mpmath-1.3.0 multidict-6.0.4 networkx-3.1 nltk-3.8.1 numba-0.57.0 numpy-1.24.3 nvidia-cublas-cu11-11.10.3.66 nvidia-cuda-cupti-cu11-11.7.101 nvidia-cuda-nvrtc-cu11-11.7.99 nvidia-cuda-runtime-cu11-11.7.99 nvidia-cudnn-cu11-8.5.0.96 nvidia-cufft-cu11-10.9.0.58 nvidia-curand-cu11-10.2.10.91 nvidia-cusolver-cu11-11.4.0.1 nvidia-cusparse-cu11-11.7.4.91 nvidia-nccl-cu11-2.14.3 nvidia-nvtx-cu11-11.7.91 oauthlib-3.2.2 packaging-23.1 pandas-2.0.1 protobuf-4.23.1 pyDeprecate-0.3.2 pyasn1-0.5.0 pyasn1-modules-0.3.0 python-dateutil-2.8.2 pytorch-lightning-1.7.7 pytz-2023.3 regex-2023.5.5 requests-2.30.0 requests-oauthlib-1.3.1 rsa-4.9 scikit-learn-1.2.2 scipy-1.10.1 six-1.16.0 sympy-1.12 tensorboard-2.13.0 tensorboard-data-server-0.7.0 threadpoolctl-3.1.0 tokenizers-0.13.3 torch-2.0.1 torchdata-0.6.1 torchmetrics-0.10.3 torchtext-0.15.2 tqdm-4.65.0 transformers-4.29.2 triton-2.0.0 typing-extensions-4.5.0 tzdata-2023.3 urllib3-1.26.15 werkzeug-2.3.4 yarl-1.9.2 zipp-3.15.0
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel$
```

## Data Preparation

```
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel$ mkdir -p data/rcv1
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel$ cd data/rcv1/
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel/data/rcv1$
```

Download training data:  

```
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel/data/rcv1$ wget -O train.txt.bz2 https://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multilabel/rcv1_topics_train.txt.bz2
--2023-05-22 16:31:52--  https://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multilabel/rcv1_topics_train.txt.bz2
Resolving www.csie.ntu.edu.tw (www.csie.ntu.edu.tw)... 140.112.30.26
Connecting to www.csie.ntu.edu.tw (www.csie.ntu.edu.tw)|140.112.30.26|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3853819 (3.7M) [application/x-bzip2]
Saving to: ‘train.txt.bz2’

train.txt.bz2              100%[=====================================>]   3.67M  5.69MB/s    in 0.6s

2023-05-22 16:31:53 (5.69 MB/s) - ‘train.txt.bz2’ saved [3853819/3853819]

(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel/data/rcv1$
```

Download test data:  

```
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel/data/rcv1$ wget -O test.txt.bz2 https://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multilabel/rcv1_topics_test.txt.bz2
--2023-05-22 16:32:37--  https://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multilabel/rcv1_topics_test.txt.bz2
Resolving www.csie.ntu.edu.tw (www.csie.ntu.edu.tw)... 140.112.30.26
Connecting to www.csie.ntu.edu.tw (www.csie.ntu.edu.tw)|140.112.30.26|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 133089834 (127M) [application/x-bzip2]
Saving to: ‘test.txt.bz2’

test.txt.bz2               100%[=====================================>] 126.92M  13.4MB/s    in 9.5s

2023-05-22 16:32:47 (13.4 MB/s) - ‘test.txt.bz2’ saved [133089834/133089834]

(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel/data/rcv1$
```

Unzipping the downloaded data:  

```
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel/data/rcv1$ ls
test.txt.bz2  train.txt.bz2
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel/data/rcv1$
```

```
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel/data/rcv1$ bzip2 -d *.bz2
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel/data/rcv1$ ls
test.txt  train.txt
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel/data/rcv1$
```

## Check the Data Format

head of training data ...  

```
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel/data/rcv1$ head train.txt
2286    E11 ECAT M11 M12 MCAT   recov recov recov recov excit excit bring mexic mexic mexic mexic mexic mexic mexic mexic mexic mexic market market market market market market market life emerg evident evident econom econom econom econom back back back track buzz tuesday tuesday tuesday tuesday tuesday stock stock stock clos record record high high high interest interest interest interest rate rate rate rate rate rate rate month low low low stag begin year ahead term term term term fundament fundament fundament matthew hickm lehm brother york point point point hist hist fall fall fall view etch mind invest cris decemb free peso peso peso stubborn week week quart gross domest domest produc report percent percent percent strong strong strong anal anal expect expect expect expect expect govern treasur bill cete cete second second fell level jan main pric index rally volum frenz million shar confound strength end long long contract drop benchmark auction remain stead feder reserv refrain rais short attract off robust return foreign grow grow confid victim crumbl focus lar schonand head head research research santand city city continu declin inflat gdp growth figur lack upward move move fact play felix boni boni jame capel posit technic uncertain argentin put neighbor brazil risk south americ wary lot hyp export led patch consum venge corpor earn justif run
2287    C24 CCAT        uruguay uruguay compan compan compan bring limit limit mexic capac capac grab market market market market small small small portion emerg rival econom gener motor motor motor ford volkswagen ag tuesday tuesday tuesday stock stock target clos specif segment desir vehicl vehicl vehicl interest applic facil facil dakot dakot dakot low compact begin countr countr year year year year year cherok cherok cherok cherok cherok construc cordob provinc schedul build grand grand start start start york april output site select roll line mid modest invest invest invest invest invest invest invest ultimat unit unit unit unit unit annual annual annual free free employ peopl larg complet knock kit kit ship produc produc produc produc stat stat percent meet bloc local requir decid dodg brand brand brand name canad detroit italian design vm cylind turbocharg model instal miniv sold million million million million million million million million million europ support open dana end end johnson control lear lear techn ppg industr increas stead decad area polit stabl rise buy pow off venezuel neon car financ grow commit made rose cent exchang growth growth play play argentin argentin argentin argentin argentin argentin brazil brazil brazil brazil brazil brazil brazil brazil risk south south south americ americ americ americ americ consum chrysl chrysl chrysl chrysl chrysl chrysl chrysl chrysl chrysl chrysl chrysl chrysl chrysl chrysl chrysl chrysl chrysl plan latin latin corp corp corp corp corp corp corp announc announc includ includ includ includ assembl assembl assembl assembl assembl plant plant plant plant plant plant plant plant plant pickup pickup truck truck truck truck diesel diesel diesel diesel engin engin engin engin expand expand jeep jeep jeep jeep jeep jeep built built built caut rebuild intern intern present project worth worth rough total total total suppl suppl suppl suppl major major major role automak automak automak automak glob strateg chairm robert eaton eaton eaton eaton don don intend intend make risky add add thom gale execut execut vice presid operat content content pace region region region solid opportun boost sale sale sale mercosur mercosur mercosur mercosur mercosur trad trad trad zone zone group paraguay paraguay
2288    C151 C15 CCAT E41 ECAT GCAT GJOB        spun stak compan compan compan compan compan compan compan compan compan nasdaq early market market tuesday stock clos month month year year year year roll invest modest unit annual peopl larg quart quart quart quart quart quart quart quart quart produc produc produc stat report report report percent percent expect expect expect expect expect expect million million million million million million million million million million million shar shar shar shar end drop increas financ made cent cent cent cent cent cent compuserv compuserv compuserv compuserv compuserv compuserv compuserv compuserv compuserv compuserv compuserv compuserv loss loss loss loss loss loss loss loss cut cut cut cut work work forc forc continu surpris declin declin fisc fisc fisc fisc fisc blam blam numb numb numb numb subscrib subscrib subscrib subscrib subscrib subscrib subscrib onlin onlin onlin onlin servic servic servic servic servic servic servic servic spend fami fami orient orient improv improv improv improv predict half half take step revital chief bob massey massey massey job part part cost cost cost program save americ basi columbus ohio base sell sell spry web brows trail simil netscap earn commun microsoft july july compar profit result result corp corp corp announc pretax charg includ includ includ post actual great wall street revenu revenu expand prev comment cancel exceed flag inform memb memb worldw niftyserv niftyserv joint ventur total japan japan found wow wow infrastructur hit due late version softwar need access make releas releas featur teen parent forecast rosy execut coupl aggress campaign fourth top mark licens advert fee electron commerc trad subsid tax prepar block
2289    C151 C15 CCAT   spun stak compan compan compan compan compan compan compan compan compan nasdaq early market market tuesday stock clos month month year year year year roll invest modest unit annual peopl larg quart quart quart quart quart quart quart quart quart produc produc produc stat report report report percent percent expect expect expect expect expect expect million million million million million million million million million million million shar shar shar shar end drop increas financ made cent cent cent cent cent cent compuserv compuserv compuserv compuserv compuserv compuserv compuserv compuserv compuserv compuserv compuserv compuserv loss loss loss loss loss loss loss loss cut cut cut cut work work forc forc continu surpris declin declin fisc fisc fisc fisc fisc blam blam numb numb numb numb subscrib subscrib subscrib subscrib subscrib subscrib subscrib onlin onlin onlin onlin servic servic servic servic servic servic servic servic spend fami fami orient orient improv improv improv improv predict half half take step revital chief bob massey massey massey job part part cost cost cost program save americ basi columbus ohio base sell sell spry web brows trail simil netscap earn commun microsoft july july compar profit result result corp corp corp announc pretax charg includ includ includ post actual great wall street revenu revenu expand prev comment cancel exceed flag inform memb memb worldw niftyserv niftyserv joint ventur total japan japan found wow wow infrastructur hit due late version softwar need access make releas releas featur teen parent forecast rosy execut coupl aggress campaign fourth top mark licens advert fee electron commerc trad subsid tax prepar block
2290    C11 C22 CCAT    compan compan limit planet planet planet planet planet hollywood hollywood hollywood hollywood hollywood hollywood launch credit credit credit credit card card card card dine feel movie movie star money arnold schwarzeneg them restaur restaur rate applic chain fast outlet festoon kitsch memorabl team william mor talent agent mbna bank wilmington del perk prefer roll seat edition shirt discount food merchandis annual annual join pop cultur ston magazin issu debt fun usual stat percent percent approv pay special introduc balanc transf cash brand advanc check orland florid off grow made spend part americ base includ intern don make fee
2291    M14 MCAT        compan compan limit limit limit market market market small small small emerg tuesday tuesday tuesday clos clos clos clos clos clos clos high high high high high low low low low countr countr year york york york point decemb decemb decemb peopl larg week week produc produc report anal anal anal govern cash fell fell fell fell level level hog hog hog hog hog hog hog hog hog tumbl cocoa cocoa cocoa cocoa cocoa cocoa pric pric pric pric pric pric index gain slaught slaught slaught slaught show show futur futur futur futur futur anticip anticip crop crop crop crop crop overse overse shrink end end end deliv pull contract contract contract coffee coffee coffee coffee crud crud crud oil oil oil monday gold gold edg increas increas increas increas commod commod bureau chicag mercantil mercantil august august august august rise buy buy buy pork pork pork pork pork belly belly belly finish respect daily daily pressur weak worry side rose focus cent cent cent cent cent cent cent cent cent cent cent cent import pack pack exchang exchang exchang exchang freedom head margin doug research harp brock assoc senior livestock pinch meat quick figur bid agricultur depart ago fact near improv cme cme pound pound pound pound take sharp sharp sharp transl sugar specul buoy new new updat ivory ivory coast coast estimat rang settl settl basi metric metric ton ton base ivorian problem ghan prelimin peg factor bar revis burst session chart chart day wide profit profit watch break resist inspir driv wednesday refin septemb septemb septemb septemb unlead gasolin gallon gallon heat barrel ounc suppl suppl suppl suppl suppl late add add forecast forecast mark trad
2292    M11 M12 M132 M13 M14 MCAT       early credit market market market market market market econom econom back back tuesday stock stock stock clos clos clos clos record record fast high high high high interest interest interest interest interest rate rate rate rate rate rate year year year term bank prefer york york york york york point point point point merchandis invest invest ston issu week quart quart quart quart report percent percent percent strong expect expect advanc treasur second fell fell gain pric index index rally rally volum overse million deliv shar shar crud crud end end end end oil oil monday monday gold gold drop edg commod stead stead stead mercantil feder feder reserv short short pressur weak weak foreign foreign grow import declin inflat growth depart fact fact fact sharp new put settl lot export led inspir announc septemb septemb heat barrel ounc blu blu blu blu chip chip chip chip fed fed fed fed held dollar dollar dollar dollar dollar dollar dollar june june june deficit deficit deficit bond bond chang dow dow dow jone aver aver throw set set set broad strateg strateg moderat polic polic afternoon unchang unchang unchang allow hurdl make ling fear add add surpr neutral richard crip leg presid mason wood walk pace hold hold amid sign slow slow boost keep sale independ sought trad trad trad trad trad stay fire approach nov congress elect recent hous retail small stall pare look rumor hard find indic spectacul joseph barthel fahnestock way liquid visibl safet stud composit currenc currenc climb climb yen yen yen yen gap shrank petroleum shortfal billion trend decreas amount good greg pearm line deal commercial de franc unit huge today bought slight germ yield lost britain fts stat surpass meet nikkei local open techn techn industr increas polit rise buy buy commit rose rose rose rose cent cent cent exchang exchang exchang exchang numb numb chief chief chief sell sell wall street japan japan japan late late mark mark mark commerc nasdaq
2293    C22 CCAT        compan compan compan compan early market market credit rival rival card tuesday stock stock money high rate month year year start york site billion fall roll line good annual free free free larg larg lost local anal expect requir introduc sprint sprint sprint sprint sprint sprint sprint sprint sprint sprint sprint sprint bill internet internet internet internet internet internet internet internet internet internet internet jump home fell mci mci kans mo big chunk busi busi busi busi busi busi exist telephon custom custom choos million million flat support support support unlimit hour end minim long long long maxim usag nation techn dist dist ve ve industr jim dod dod dod time time time avoid glitch hurt short press bet massick off off off off off colomb bear stearn ground dub passport provid provid side cent clock exchang comput network phon call offer offer offer bell city city city entry spark flur numb compet shockwav initial onlin onlin onlin navigat navigat servic servic servic servic servic servic servic servic servic servic servic servic search search explor move won fact fact host propriet serv resid take take rebat certif speed speed modem new kilobit dedicat mail part direct toll americ base web brows brows consum consum consum consum consum simil netscap netscap commun microsoft microsoft compar plan profit wide corp corp corp announc includ includ includ revenu major glob softwar softwar don access access access access access access access access access access access releas make vice presid operat operat region commerc
2294    E14 ECAT        wear mom levi levi strauss popul popul market draw lure portion portion tommy hilfig retail retail retail retail retail retail ralph back back back back back back back back back back back laur polo calvin target klein slung find clos hip hug high high high high high high bottom chain retr peac march outlet low low hot own dayton dayton year year year year hudson hudson clay ring necklac reminisc spokeswom susan eich eich york backpack clog zip amount mind good shirt shirt shirt discount discount discount discount merchandis annual peopl larg larg percent percent percent percent percent percent percent percent percent percent percent percent percent special decid brand brand jump design big show increas short rise buy buy confid import import import network offer bell servic spend spend spend spend spend depart depart depart depart depart depart depart fact ago cost direct school school school school school school school school school school americ americ americ americ americ shop shop shop shop shop load lot peren base favourit sell sell sell sell jean jean jean jean jean jean sneak cloth cloth cloth cloth consum sort funny hasn pant thing basic andrea day plan kent kent kent kent express express express express express corp result travel relat includ includ child child child survey survey survey survey caus great emphas typic invent reduc item item item item textbook textbook textbook board account account account account budget budget budget budget element student student student student student student colleg colleg colleg colleg colleg colleg project demand expend curi boy suppl suppl suppl dramat found styl chang consc girl girl contr aver aver stor stor stor stor stor stor stor stor battl season season holiday access thanksgiv christm bang fight add add add add pur parent parent parent heart mall mall brat presid flex fashion fashion fashion muscl alan millstein millstein millstein consult captur locat offic electron sale sale sale sale left reveal influ kid kid kid group pick pick pick
2295    C12 CCAT GCAT GCRIM     recov recov compan compan compan compan bring early gener gener gener tuesday tuesday money month countr begin begin year year term mor mor york arizon arizon arizon arizon arizon amount suit suit suit suit suit suit suit suit tobacc tobacc tobacc tobacc tobacc tobacc tobacc tobacc tobacc tobacc tobacc tobacc tobacc tobacc tobacc firm firm firm firm file file file file file unit lawsuit lawsuit lawsuit lawsuit lawsuit list list join join seek seek seek hundred hundred hundred hundred week treat smok smok smok smok smok smok smok smok ill ill sourc sourc produc produc michig michig oklahom oklahom stat stat stat stat stat stat suing pay britain attorney attorney attorney carl expect stoval stoval stoval stoval decid decid leth warrant enorm name name name burd shift taxpay philip philip kans kans kans kans kans kans kans cos vigor big defend defend defend law aid frank kelley legal sold million million million million thursday thursday indianapol indianapol indianapol liabl challeng jury jury jury jury delib case case case roge roge roge lawy age age industr industr industr industr industr die lung lung time canc canc widow unspecif damag damag damag damag public public public public advocat advocat urg mayor rudolph giulian financ grow sue paid paid health health care green san francisc head research effort call obtain forc medicaid medicaid medicaid city city city city refund cigaret cigaret jacksonvill fla numb award figur man strick lucky strik defect brown brown williamson williamson plc neglig fail appeal excess discov ll finit claim grant cost cost cost cost program incur risk date americ aim basi educat hazard rjr nabisc rj reynold divid consum loew lorillard simil simil hill knowlton council run institut brook ligget corp corp corp relat relat relat child child actual wednesday wednesday inform dollar dollar dollar total broad make teen add richard mark wood hold group group group prepar sought
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel/data/rcv1$
```

head of test data ...  

```
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel/data/rcv1$ head test.txt
26151   GCAT GSPO       socc colomb colomb colomb colomb beat beat chil chil chil chil world world world cup cup cup qualif qualif qualif qualif halftim south south americ americ match sunday scor faustin asprill st minut minut jorg bermudez ivan zamoran penalt attend group stand tabulat play won draw lost goal goal point ecuador argentin boliv paraguay uruguay peru venezuel note top final franc brazil automat hold
26152   GCAT GSPO       world world world world qualif qualif sunday minut minut won hold athlet time time time time time lucky lucky komen komen komen komen break break record record record daniel keny keny keny keny keny keny made shat noureddin morcel morcel morcel morcel morcel morcel morcel met met met met met met second second second second intern meet year year fail fail atlant olymp olymp olymp olymp clock clock clock clock set set ago mont carl blist form grand grand prix prix circuit mark mark monac month brussel august fast fast hist hist finish finish back back sixth plac david kisang led field lead carry ahead ahead near rival shem koror italian gennar di napol champ champ young good deserv today result told report mean thing ve mile comfort burund venust niyongab born wilson kipket run denmark
26153   GCAT GSPO       hernandez socc jess colomb valient beat beat gabriel gabriel chil urdanet world world world vera cup cup cup mirand qualif juan juan socor south south hernndez americ americ sunday scor scor minut minut jorg ivan group play lost point point ecuador ecuador ecuador ecuador ecuador ecuador ecuador ecuador argentin venezuel venezuel top brazil record month finish david field good born step step quit sept win win game game game captain alex alex aguinag aguinag aguinag featur nation nation tourna prec jeer crowd expect high weak team team team snap rebound shot gilson gilson de de souz souz fourth unabl add tally coach boss francisc maturan home impress start chanc long quest ask defeat santiag ventur carlo moral wagn river hurtad hurtad maxim tenorio lui lui lui lui capur diaz alfons obregon hect carabal jose garcia garcia angel fernandez eduard rafael dudamel filos william gonzalez edson tortoler macintosh sergio
26154   GCAT GSPO       beat beat beat world world world world world world cup americ match cycl cycl sunday rousseau rousseau rousseau scor scor complet complet complet uniqu uniqu doubl doubl doubl florian sprint sprint sprint week take gold gold medal medal medal km trial day day marty marty nothstein nothstein nothstein unit unit stat stat won won frenchm didn bercy point point point point track track track pari appear drain race race race battl battl overcom defend defend darryn hill austral austral austral final final final final semifin franc franc franc hll cross line relegat rough time time ride ride ride ride rob bad record decid decid ll perth made lose felt keirin early early sery met met second find pow pow motor pure year year year year heart determin atlant marion olymp clignet clignet clignet clignet lucy tyl tyl ago sharm sharm women individual pursuit grand antonel prix bellut brok event adopt streamlin superm styl styl develop britain britain finish graem obree amaz differ plac move bike countback field need kms titl titl rossel llaner llaner llaner spain spain michael sandstod sandstod sandstod lap lap lap attack spent rest rest succeed champ champ champ champ champ champ champ gain advant good level award today span silvio martinel italy italy miss breakaway settl bronz arrear compet confirm status success russia denmark win win win win win win nation expect high home defeat
26155   GCAT GSPO       world world sunday day stand stand point point race race final final final franc franc champ champ result result italy motocross motocross cc cc round round stef evert evert evert evert belg belg belg hond hond marnicq bervoet bervoet bervoet bervoet suzuk suzuk freder bolley bolley bolley bolley kawasak kawasak pit beir beir beir german tallon vohland vohland yve demar demar demar demar yamah yamah wern dewit dewit provis andrea bartolin
26156   GCAT GSPO       open nick knight knight knight hit hit hundr provid backbon inn maid centur centur recent match match match pakistan sunday sunday sunday complet fine scor scor cap superb weekend bat brisk brisk assur take fall regul end push occas day day day left left left arm arm spin play play asif won mujtab lost midwicket punch air celebr includ four reply saeed saeed anwar anwar shahid put top singl pacem final final allan mull punish eventual ijaz ahm come remaind middl ord medium pace made lose sery sery sery intern finish back carry today run run run run round win win win game captain captain cricket rashid rashid rashid rashid rashid latif latif steer steer pakist pakist pakist pakist pakist pakist vict vict wicketkeep head wicket wicket wicket wicket wicket tumbl start england england england england england england england trent bridg test test calm squar cut adam hollioak hollioak hollioak hollioak ball ball ball ball chip surrey vacant territ spar threat steal quick chas over over pay tribut wasim akram saturday saturday edgbaston repeat perform control bowl pressur situat mike atherton drag warwickshir
26157   GCAT GSPO       knight beat beat sunday scor day day won final final ijaz ahm sery intern win cricket cricket pakist pakist pakist wicket england england england england trent bridg over over
26158   GCAT GSPO       world sunday minut put athlet komen record daniel keny keny keny keny keny keny keny riet men men men men men men men men men men alger noureddin laban morcel rotich met met met met met met met met met met met kiptoo second philip intern intern kibitok meet meet davi kamog ugand calvin har iwan thom osmons women women women women women ezinw ezinw ezinw niger niger niger niger niger davidson davidson deji aliu geir moen norway claus hirsbr hurdl tor zelln britain britain rusian mashchenk jon ridgeon pole david vault igor trandenkov tim lobing pyotr bochakaryov spain spain tripl michael jump jump shem yoelf koror quesad cuba cuba cuba gennar gennadiy di markov napol charl freidek paol dal soglio corrad result result fantin manuel martinez italy italy italy irin privalov juliet cuthbert jamaic burund chandr venust sturrup niyongab baham leah wilson pell russia russia russia russia russia russia kipket canad anna denmark denmark brezrezinsk poland mayt zunig sonia sulliv ireland sally barsosio paulin kong iness kravet ukrain german german chiom ajunw shan javelin xiomar oksan ovchinnikov shot isel lopez long river william
26159   GCAT GSPO       world world sunday minut week final athlet time time komen komen komen komen komen break break break record record record daniel keny keny keny keny shat alger noureddin morcel morcel morcel morcel met met met second second second intern meet year year atlant olymp clock clock clock clock grand grand prix prix event mark mark mark mark monac month brussel august fast fast hist hist finish finish back sixth plac david kisang field lead carry ahead near rival shem koror italian gennar di napol champ team fract make prev clos ethiop hail gebreselassie zurich
26160   GCAT GSPO       world sunday minut athlet komen komen break record record daniel keny men noureddin alger morcel met met second intern meet clock set set mont carl mark august prev
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel/data/rcv1$
```

## Learn the Example Configuration File

```
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel/data/rcv1$ cd ../..
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel$ cat example_config/rcv1/l2svm.yml
# data
training_file: data/rcv1/train.txt
test_file: data/rcv1/test.txt
data_name: rcv1

# train
seed: 1337
linear: true
liblinear_options: "-s 2 -B 1 -e 0.0001 -q"
linear_technique: 1vsrest

# eval
eval_batch_size: 256
monitor_metrics: [Macro-F1, Micro-F1, P@1, P@3, P@5]
metric_threshold: 0

data_format: txt
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel$
```

## Training and Prediction

Running command:  
time python3 main.py --config example_config/rcv1/l2svm.yml | tee train-predict-rcv1.log


```
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel$ time python3 main.py --config example_config/rcv1/l2svm.yml | tee train-predict-rcv1.log
2023-05-22 16:40:50,464 INFO:Run name: rcv1_l2svm_20230522164050
/home/rnd/anaconda3/envs/LibMultiLabel/lib/python3.8/site-packages/liblinear/liblinear.py:135: NumbaDeprecationWarning: The 'nopython' keyword argument was not supplied to the 'numba.jit' decorator. The implicit default value for this argument is currently False, but it will be changed to True in Numba 0.59.0. See https://numba.readthedocs.io/en/stable/reference/deprecation.html#deprecation-of-object-mode-fall-back-behaviour-when-using-jit for details.
  def csr_to_problem_jit(l, x_val, x_ind, x_rowptr, prob_val, prob_ind, prob_rowptr):
/home/rnd/anaconda3/envs/LibMultiLabel/lib/python3.8/site-packages/sklearn/preprocessing/_label.py:895: UserWarning: unknown class(es) ['E312', 'GMIL'] will be ignored
  warnings.warn(
2023-05-22 16:41:57,447 INFO:Training one-vs-rest model on 101 labels
100%|██████████████████████████████████████████████████████████████████| 101/101 [00:13<00:00,  7.68it/s]
100%|████████████████████████████████████████████████████████████████| 3052/3052 [00:48<00:00, 62.73it/s]
2023-05-22 16:42:59,327 INFO:Finish writing log to ./runs/rcv1_l2svm_20230522164050/logs.json.
====== test dataset evaluation result =======
|     Macro-F1     |     Micro-F1     |       P@1        |       P@3        |       P@5        |
|-----------------:|-----------------:|-----------------:|-----------------:|-----------------:|
|      0.5189      |      0.8030      |      0.9587      |      0.7992      |      0.5577      |

Wall time: 129.30 (s)

real    2m9.880s
user    3m49.180s
sys     0m5.295s
(LibMultiLabel) rnd@gpu:~/tool/LibMultiLabel$
```



## Reference

1. https://www.csie.ntu.edu.tw/~cjlin/libmultilabel/cli/linear.html#cli-quickstart
2. https://www.csie.ntu.edu.tw/~cjlin/papers/libsvm.pdf  

