# Multihead Siamese Training for Myanmar Paraphrase

## Create a New Anaconda Environment

```
(base) yekyaw.thu@gpu:~/exp/siamese$ conda create --name siamese python=3.6
Collecting package metadata (current_repodata.json): done
Solving environment: failed with repodata from current_repodata.json, will retry with next repodata source.
Collecting package metadata (repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 22.9.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/siamese

  added / updated specs:
    - python=3.6


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    certifi-2021.5.30          |   py36h06a4308_0         139 KB
    pip-21.2.2                 |   py36h06a4308_0         1.8 MB
    python-3.6.13              |       h12debd9_1        32.5 MB
    setuptools-58.0.4          |   py36h06a4308_0         788 KB
    sqlite-3.40.0              |       h5082296_0         1.2 MB
    ------------------------------------------------------------
                                           Total:        36.4 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-5.1-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2022.10.11-h06a4308_0
  certifi            pkgs/main/linux-64::certifi-2021.5.30-py36h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.38-h1181459_1
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_2
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-11.2.0-h1234567_1
  libgomp            pkgs/main/linux-64::libgomp-11.2.0-h1234567_1
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-11.2.0-h1234567_1
  ncurses            pkgs/main/linux-64::ncurses-6.3-h5eee18b_3
  openssl            pkgs/main/linux-64::openssl-1.1.1s-h7f8727e_0
  pip                pkgs/main/linux-64::pip-21.2.2-py36h06a4308_0
  python             pkgs/main/linux-64::python-3.6.13-h12debd9_1
  readline           pkgs/main/linux-64::readline-8.2-h5eee18b_0
  setuptools         pkgs/main/linux-64::setuptools-58.0.4-py36h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.40.0-h5082296_0
  tk                 pkgs/main/linux-64::tk-8.6.12-h1ccaba5_0
  wheel              pkgs/main/noarch::wheel-0.37.1-pyhd3eb1b0_0
  xz                 pkgs/main/linux-64::xz-5.2.6-h5eee18b_0
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
pip-21.2.2           | 1.8 MB    | ################################################################################### | 100%
certifi-2021.5.30    | 139 KB    | ################################################################################### | 100%
setuptools-58.0.4    | 788 KB    | ################################################################################### | 100%
sqlite-3.40.0        | 1.2 MB    | ################################################################################### | 100%
python-3.6.13        | 32.5 MB   | ################################################################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate siamese
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) yekyaw.thu@gpu:~/exp/siamese$
```

Activate the Siamese...   

```
(base) yekyaw.thu@gpu:~/exp/siamese$ conda activate siamese
(siamese) yekyaw.thu@gpu:~/exp/siamese$
```

## Git Clone

```
(siamese) yekyaw.thu@gpu:~/exp/siamese$ git clone https://github.com/tlatkowski/multihead-siamese-nets
Cloning into 'multihead-siamese-nets'...
remote: Enumerating objects: 982, done.
remote: Counting objects: 100% (21/21), done.
remote: Compressing objects: 100% (21/21), done.
remote: Total 982 (delta 4), reused 3 (delta 0), pack-reused 961
Receiving objects: 100% (982/982), 1.47 MiB | 5.61 MiB/s, done.
Resolving deltas: 100% (557/557), done.
```

```
(siamese) yekyaw.thu@gpu:~/exp/siamese$ cd multihead-siamese-nets/
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ ls
bin  colab  config  data  gui_demo.py  layers  LICENSE  models  pics  README.md  requirements  run.py  tests  utils
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$
```

## Installation of the Requirement Libraries  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ pip install -r requirements/requirements-gpu.txt
Collecting tqdm==4.15.0
  Downloading tqdm-4.15.0-py2.py3-none-any.whl (46 kB)
     |████████████████████████████████| 46 kB 203 kB/s
Collecting pandas==0.22.0
  Downloading pandas-0.22.0-cp36-cp36m-manylinux1_x86_64.whl (26.2 MB)
     |████████████████████████████████| 26.2 MB 127.7 MB/s
Collecting tflearn==0.3.2
  Downloading tflearn-0.3.2.tar.gz (98 kB)
     |████████████████████████████████| 98 kB 619 kB/s
Collecting numpy==1.14.2
  Downloading numpy-1.14.2-cp36-cp36m-manylinux1_x86_64.whl (12.2 MB)
     |████████████████████████████████| 12.2 MB 73.9 MB/s
Collecting tensorflow-gpu==1.15.2
  Downloading tensorflow_gpu-1.15.2-cp36-cp36m-manylinux2010_x86_64.whl (411.0 MB)
     |████████████████████████████████| 411.0 MB 21 kB/s
Collecting jsonlines==1.2.0
  Downloading jsonlines-1.2.0-py2.py3-none-any.whl (7.6 kB)
Collecting seaborn==0.9.0
  Downloading seaborn-0.9.0-py3-none-any.whl (208 kB)
     |████████████████████████████████| 208 kB 53.3 MB/s
Collecting pytz>=2011k
  Downloading pytz-2022.6-py2.py3-none-any.whl (498 kB)
     |████████████████████████████████| 498 kB 48.1 MB/s
Collecting python-dateutil>=2
  Using cached python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
Collecting six
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Collecting Pillow
  Downloading Pillow-8.4.0-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.1 MB)
     |████████████████████████████████| 3.1 MB 49.6 MB/s
Collecting gast==0.2.2
  Downloading gast-0.2.2.tar.gz (10 kB)
Collecting opt-einsum>=2.3.2
  Using cached opt_einsum-3.3.0-py3-none-any.whl (65 kB)
Collecting astor>=0.6.0
  Downloading astor-0.8.1-py2.py3-none-any.whl (27 kB)
Collecting google-pasta>=0.1.6
  Using cached google_pasta-0.2.0-py3-none-any.whl (57 kB)
Collecting wrapt>=1.11.1
  Downloading wrapt-1.14.1-cp36-cp36m-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (74 kB)
     |████████████████████████████████| 74 kB 237 kB/s
Collecting tensorboard<1.16.0,>=1.15.0
  Downloading tensorboard-1.15.0-py3-none-any.whl (3.8 MB)
     |████████████████████████████████| 3.8 MB 47.0 MB/s
Collecting tensorflow-estimator==1.15.1
  Downloading tensorflow_estimator-1.15.1-py2.py3-none-any.whl (503 kB)
     |████████████████████████████████| 503 kB 47.9 MB/s
Collecting protobuf>=3.6.1
  Downloading protobuf-3.19.6-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.1 MB)
     |████████████████████████████████| 1.1 MB 49.0 MB/s
INFO: pip is looking at multiple versions of <Python from Requires-Python> to determine which version is compatible with other requirements. This could take a while.
INFO: pip is looking at multiple versions of numpy to determine which version is compatible with other requirements. This could take a while.
INFO: pip is looking at multiple versions of tflearn to determine which version is compatible with other requirements. This could take a while.
INFO: pip is looking at multiple versions of pandas to determine which version is compatible with other requirements. This could take a while.
INFO: pip is looking at multiple versions of tqdm to determine which version is compatible with other requirements. This could take a while.
ERROR: Cannot install -r requirements/requirements-gpu.txt (line 2), -r requirements/requirements-gpu.txt (line 3), -r requirements/requirements-gpu.txt (line 5) and numpy==1.14.2 because these package versions have conflicting dependencies.

The conflict is caused by:
    The user requested numpy==1.14.2
    pandas 0.22.0 depends on numpy>=1.9.0
    tflearn 0.3.2 depends on numpy
    tensorflow-gpu 1.15.2 depends on numpy<2.0 and >=1.16.0

To fix this you could try to:
1. loosen the range of package versions you've specified
2. remove package versions to allow pip attempt to solve the dependency conflict

ERROR: ResolutionImpossible: for help visit https://pip.pypa.io/en/latest/user_guide/#fixing-conflicting-dependencies
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$
```

I got some errors as you can see above ...  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ pip install numpy>=1.16.0
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ python
Python 3.6.13 |Anaconda, Inc.| (default, Jun  4 2021, 14:25:59)
[GCC 7.5.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import numpy as np
>>> print(np.__version__)
1.19.5
>>>
```

install pandas library ...  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ pip install pandas
Collecting pandas
  Downloading pandas-1.1.5-cp36-cp36m-manylinux1_x86_64.whl (9.5 MB)
     |████████████████████████████████| 9.5 MB 6.7 kB/s
Collecting python-dateutil>=2.7.3
  Using cached python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
Requirement already satisfied: numpy>=1.15.4 in /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages (from pandas) (1.19.5)
Collecting pytz>=2017.2
  Using cached pytz-2022.6-py2.py3-none-any.whl (498 kB)
Collecting six>=1.5
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Installing collected packages: six, pytz, python-dateutil, pandas
Successfully installed pandas-1.1.5 python-dateutil-2.8.2 pytz-2022.6 six-1.16.0
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$
```

Install tflearn or make confirmation ...  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ pip install tflearn==0.3.2
Collecting tflearn==0.3.2
  Using cached tflearn-0.3.2.tar.gz (98 kB)
Requirement already satisfied: numpy in /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages (from tflearn==0.3.2) (1.19.5)
Requirement already satisfied: six in /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages (from tflearn==0.3.2) (1.16.0)
Collecting Pillow
  Using cached Pillow-8.4.0-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.1 MB)
Building wheels for collected packages: tflearn
  Building wheel for tflearn (setup.py) ... done
  Created wheel for tflearn: filename=tflearn-0.3.2-py3-none-any.whl size=128207 sha256=ed2a25985463f608a150270cb9258b61d25b53167128cbc58483c9f0df583bd3
  Stored in directory: /home/yekyaw.thu/.cache/pip/wheels/14/e9/35/ac682b1d18f932dc39cf86f25b22bb70df2e80e45851e4f9f3
Successfully built tflearn
Installing collected packages: Pillow, tflearn
Successfully installed Pillow-8.4.0 tflearn-0.3.2
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$
```

Installation of tensorflow-gpu==1.15.2  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ pip install tensorflow-gpu==1.15.2
Collecting tensorflow-gpu==1.15.2
  Using cached tensorflow_gpu-1.15.2-cp36-cp36m-manylinux2010_x86_64.whl (411.0 MB)
Collecting gast==0.2.2
  Using cached gast-0.2.2.tar.gz (10 kB)
Collecting google-pasta>=0.1.6
  Using cached google_pasta-0.2.0-py3-none-any.whl (57 kB)
Collecting grpcio>=1.8.6
  Downloading grpcio-1.48.2-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.6 MB)
     |████████████████████████████████| 4.6 MB 528 kB/s
Requirement already satisfied: six>=1.10.0 in /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages (from tensorflow-gpu==1.15.2) (1.16.0)
Collecting opt-einsum>=2.3.2
  Using cached opt_einsum-3.3.0-py3-none-any.whl (65 kB)
Collecting keras-preprocessing>=1.0.5
  Using cached Keras_Preprocessing-1.1.2-py2.py3-none-any.whl (42 kB)
Collecting tensorflow-estimator==1.15.1
  Using cached tensorflow_estimator-1.15.1-py2.py3-none-any.whl (503 kB)
Collecting termcolor>=1.1.0
  Downloading termcolor-1.1.0.tar.gz (3.9 kB)
Collecting wrapt>=1.11.1
  Using cached wrapt-1.14.1-cp36-cp36m-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (74 kB)
Collecting keras-applications>=1.0.8
  Downloading Keras_Applications-1.0.8-py3-none-any.whl (50 kB)
     |████████████████████████████████| 50 kB 952 kB/s
Requirement already satisfied: wheel>=0.26 in /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages (from tensorflow-gpu==1.15.2) (0.37.1)
Collecting astor>=0.6.0
  Using cached astor-0.8.1-py2.py3-none-any.whl (27 kB)
Collecting tensorboard<1.16.0,>=1.15.0
  Using cached tensorboard-1.15.0-py3-none-any.whl (3.8 MB)
Collecting absl-py>=0.7.0
  Using cached absl_py-1.3.0-py3-none-any.whl (124 kB)
Requirement already satisfied: numpy<2.0,>=1.16.0 in /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages (from tensorflow-gpu==1.15.2) (1.19.5)
Collecting protobuf>=3.6.1
  Using cached protobuf-3.19.6-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.1 MB)
Collecting h5py
  Downloading h5py-3.1.0-cp36-cp36m-manylinux1_x86_64.whl (4.0 MB)
     |████████████████████████████████| 4.0 MB 53.2 MB/s
Requirement already satisfied: setuptools>=41.0.0 in /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages (from tensorboard<1.16.0,>=1.15.0->tensorflow-gpu==1.15.2) (58.0.4)
Collecting werkzeug>=0.11.15
  Downloading Werkzeug-2.0.3-py3-none-any.whl (289 kB)
     |████████████████████████████████| 289 kB 88.9 MB/s
Collecting markdown>=2.6.8
  Downloading Markdown-3.3.7-py3-none-any.whl (97 kB)
     |████████████████████████████████| 97 kB 1.3 MB/s
Collecting importlib-metadata>=4.4
  Downloading importlib_metadata-4.8.3-py3-none-any.whl (17 kB)
Collecting zipp>=0.5
  Downloading zipp-3.6.0-py3-none-any.whl (5.3 kB)
Collecting typing-extensions>=3.6.4
  Downloading typing_extensions-4.1.1-py3-none-any.whl (26 kB)
Collecting dataclasses
  Downloading dataclasses-0.8-py3-none-any.whl (19 kB)
Collecting cached-property
  Downloading cached_property-1.5.2-py2.py3-none-any.whl (7.6 kB)
Building wheels for collected packages: gast, termcolor
  Building wheel for gast (setup.py) ... done
  Created wheel for gast: filename=gast-0.2.2-py3-none-any.whl size=7554 sha256=010e9d6b30d1a24aa3a5fbb07c93dd1b693c7b2fe7c32e5db1c6203addb2ee3f
  Stored in directory: /home/yekyaw.thu/.cache/pip/wheels/19/a7/b9/0740c7a3a7d1d348f04823339274b90de25fbcd217b2ee1fbe
  Building wheel for termcolor (setup.py) ... done
  Created wheel for termcolor: filename=termcolor-1.1.0-py3-none-any.whl size=4848 sha256=ba32648f946b916d56239f5cb96a5310cce677e7d7b19d166df9de15b38785cc
  Stored in directory: /home/yekyaw.thu/.cache/pip/wheels/93/2a/eb/e58dbcbc963549ee4f065ff80a59f274cc7210b6eab962acdc
Successfully built gast termcolor
Installing collected packages: zipp, typing-extensions, importlib-metadata, dataclasses, cached-property, werkzeug, protobuf, markdown, h5py, grpcio, absl-py, wrapt, termcolor, tensorflow-estimator, tensorboard, opt-einsum, keras-preprocessing, keras-applications, google-pasta, gast, astor, tensorflow-gpu
Successfully installed absl-py-1.3.0 astor-0.8.1 cached-property-1.5.2 dataclasses-0.8 gast-0.2.2 google-pasta-0.2.0 grpcio-1.48.2 h5py-3.1.0 importlib-metadata-4.8.3 keras-applications-1.0.8 keras-preprocessing-1.1.2 markdown-3.3.7 opt-einsum-3.3.0 protobuf-3.19.6 tensorboard-1.15.0 tensorflow-estimator-1.15.1 tensorflow-gpu-1.15.2 termcolor-1.1.0 typing-extensions-4.1.1 werkzeug-2.0.3 wrapt-1.14.1 zipp-3.6.0
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$
```

Install jsonlines ...  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ pip install jsonlines==1.2.0
Collecting jsonlines==1.2.0
  Using cached jsonlines-1.2.0-py2.py3-none-any.whl (7.6 kB)
Requirement already satisfied: six in /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages (from jsonlines==1.2.0) (1.16.0)
Installing collected packages: jsonlines
Successfully installed jsonlines-1.2.0
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$
```

Installation of seaborn ...  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ pip install seaborn==0.9.0
Collecting seaborn==0.9.0
  Using cached seaborn-0.9.0-py3-none-any.whl (208 kB)
Collecting scipy>=0.14.0
  Downloading scipy-1.5.4-cp36-cp36m-manylinux1_x86_64.whl (25.9 MB)
     |████████████████████████████████| 25.9 MB 2.9 MB/s
Requirement already satisfied: pandas>=0.15.2 in /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages (from seaborn==0.9.0) (1.1.5)
Requirement already satisfied: numpy>=1.9.3 in /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages (from seaborn==0.9.0) (1.19.5)
Collecting matplotlib>=1.4.3
  Downloading matplotlib-3.3.4-cp36-cp36m-manylinux1_x86_64.whl (11.5 MB)
     |████████████████████████████████| 11.5 MB 142 kB/s
Collecting cycler>=0.10
  Using cached cycler-0.11.0-py3-none-any.whl (6.4 kB)
Collecting pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.3
  Using cached pyparsing-3.0.9-py3-none-any.whl (98 kB)
Requirement already satisfied: pillow>=6.2.0 in /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages (from matplotlib>=1.4.3->seaborn==0.9.0) (8.4.0)
Requirement already satisfied: python-dateutil>=2.1 in /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages (from matplotlib>=1.4.3->seaborn==0.9.0) (2.8.2)
Collecting kiwisolver>=1.0.1
  Downloading kiwisolver-1.3.1-cp36-cp36m-manylinux1_x86_64.whl (1.1 MB)
     |████████████████████████████████| 1.1 MB 26.1 MB/s
Requirement already satisfied: pytz>=2017.2 in /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages (from pandas>=0.15.2->seaborn==0.9.0) (2022.6)
Requirement already satisfied: six>=1.5 in /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages (from python-dateutil>=2.1->matplotlib>=1.4.3->seaborn==0.9.0) (1.16.0)
Installing collected packages: pyparsing, kiwisolver, cycler, scipy, matplotlib, seaborn
Successfully installed cycler-0.11.0 kiwisolver-1.3.1 matplotlib-3.3.4 pyparsing-3.0.9 scipy-1.5.4 seaborn-0.9.0
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$
```

## Data Preparation 

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
