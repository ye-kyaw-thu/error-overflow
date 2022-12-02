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
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ cd bin
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets/bin$ ls
prepare_data.sh
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets/bin$ chmod a+x prepare_data.sh
```

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets/bin$ ls -lh ./prepare_data.sh
-rwxr-xr-x 1 yekyaw.thu domain users 1.6K Dec  1 17:31 ./prepare_data.sh
```

run prepare_data.sh ...  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets/bin$ time ./prepare_data.sh
--2022-12-01 17:52:05--  https://drive.google.com/uc?export=download&id=1wkAjMu-Pqnm1l-92M7UEp5YEtT1cFgVz
Resolving drive.google.com (drive.google.com)... 172.217.194.101, 172.217.194.113, 172.217.194.138, ...
Connecting to drive.google.com (drive.google.com)|172.217.194.101|:443... connected.
HTTP request sent, awaiting response... 303 See Other
Location: https://doc-04-8o-docs.googleusercontent.com/docs/securesc/ha0ro937gcuc7l7deffksulhg5h7mbp1/0dld5bd6v9um84r3chu88r2lgo9te3rj/1669891875000/05563007606908372189/*/1wkAjMu-Pqnm1l-92M7UEp5YEtT1cFgVz?e=download&uuid=ae761366-7537-4b32-93c6-a297ec7f4dac [following]
Warning: wildcards not supported in HTTP.
--2022-12-01 17:52:15--  https://doc-04-8o-docs.googleusercontent.com/docs/securesc/ha0ro937gcuc7l7deffksulhg5h7mbp1/0dld5bd6v9um84r3chu88r2lgo9te3rj/1669891875000/05563007606908372189/*/1wkAjMu-Pqnm1l-92M7UEp5YEtT1cFgVz?e=download&uuid=ae761366-7537-4b32-93c6-a297ec7f4dac
Resolving doc-04-8o-docs.googleusercontent.com (doc-04-8o-docs.googleusercontent.com)... 74.125.130.132, 2404:6800:4003:c01::84
Connecting to doc-04-8o-docs.googleusercontent.com (doc-04-8o-docs.googleusercontent.com)|74.125.130.132|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 7735242 (7.4M) [application/x-compressed-tar]
Saving to: ‘SNLI/train_snli.tgz’

SNLI/train_snli.tgz             100%[=====================================================>]   7.38M  16.9MB/s    in 0.4s

2022-12-01 17:52:17 (16.9 MB/s) - ‘SNLI/train_snli.tgz’ saved [7735242/7735242]

--2022-12-01 17:52:17--  https://drive.google.com/uc?export=download&id=1dnck-CCIyx8y2xg1vwFzcwXieZJB7ERC
Resolving drive.google.com (drive.google.com)... 172.217.194.100, 172.217.194.139, 172.217.194.102, ...
Connecting to drive.google.com (drive.google.com)|172.217.194.100|:443... connected.
HTTP request sent, awaiting response... 303 See Other
Location: https://doc-0o-8o-docs.googleusercontent.com/docs/securesc/ha0ro937gcuc7l7deffksulhg5h7mbp1/jcc92is754h0ddrgeut03i1vonco8rqj/1669891875000/05563007606908372189/*/1dnck-CCIyx8y2xg1vwFzcwXieZJB7ERC?e=download&uuid=7792ecba-741d-4f70-85bf-515b61792b2f [following]
Warning: wildcards not supported in HTTP.
--2022-12-01 17:52:21--  https://doc-0o-8o-docs.googleusercontent.com/docs/securesc/ha0ro937gcuc7l7deffksulhg5h7mbp1/jcc92is754h0ddrgeut03i1vonco8rqj/1669891875000/05563007606908372189/*/1dnck-CCIyx8y2xg1vwFzcwXieZJB7ERC?e=download&uuid=7792ecba-741d-4f70-85bf-515b61792b2f
Resolving doc-0o-8o-docs.googleusercontent.com (doc-0o-8o-docs.googleusercontent.com)... 74.125.130.132, 2404:6800:4003:c01::84
Connecting to doc-0o-8o-docs.googleusercontent.com (doc-0o-8o-docs.googleusercontent.com)|74.125.130.132|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 22176174 (21M) [application/x-gtar]
Saving to: ‘QQP/qqp_train.tgz’

QQP/qqp_train.tgz               100%[=====================================================>]  21.15M  18.0MB/s    in 1.2s

2022-12-01 17:52:23 (18.0 MB/s) - ‘QQP/qqp_train.tgz’ saved [22176174/22176174]

--2022-12-01 17:52:24--  https://docs.google.com/uc?export=download&confirm=t&id=1XD-HxzUCTHrzhfvIXOlgqN_MWiiAqM8h
Resolving docs.google.com (docs.google.com)... 74.125.24.101, 74.125.24.113, 74.125.24.102, ...
Connecting to docs.google.com (docs.google.com)|74.125.24.101|:443... connected.
HTTP request sent, awaiting response... 303 See Other
Location: https://doc-0g-8o-docs.googleusercontent.com/docs/securesc/ha0ro937gcuc7l7deffksulhg5h7mbp1/3jnme6umnhm18to4i59gu2c8bbmlc329/1669891875000/05563007606908372189/*/1XD-HxzUCTHrzhfvIXOlgqN_MWiiAqM8h?e=download&uuid=3d776fdf-f37a-41f4-9eae-a6de7e0b71bc [following]
Warning: wildcards not supported in HTTP.
--2022-12-01 17:52:24--  https://doc-0g-8o-docs.googleusercontent.com/docs/securesc/ha0ro937gcuc7l7deffksulhg5h7mbp1/3jnme6umnhm18to4i59gu2c8bbmlc329/1669891875000/05563007606908372189/*/1XD-HxzUCTHrzhfvIXOlgqN_MWiiAqM8h?e=download&uuid=3d776fdf-f37a-41f4-9eae-a6de7e0b71bc
Resolving doc-0g-8o-docs.googleusercontent.com (doc-0g-8o-docs.googleusercontent.com)... 74.125.130.132, 2404:6800:4003:c01::84
Connecting to doc-0g-8o-docs.googleusercontent.com (doc-0g-8o-docs.googleusercontent.com)|74.125.130.132|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 117792766 (112M) [application/x-gtar]
Saving to: ‘QQP/qqp_test.tgz’

QQP/qqp_test.tgz                100%[=====================================================>] 112.33M  24.9MB/s    in 4.8s

2022-12-01 17:52:30 (23.6 MB/s) - ‘QQP/qqp_test.tgz’ saved [117792766/117792766]

--2022-12-01 17:52:30--  https://dl.fbaipublicfiles.com/anli/anli_v0.1.zip
Resolving dl.fbaipublicfiles.com (dl.fbaipublicfiles.com)... 104.22.75.142, 172.67.9.4, 104.22.74.142, ...
Connecting to dl.fbaipublicfiles.com (dl.fbaipublicfiles.com)|104.22.75.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 18621352 (18M) [application/zip]
Saving to: ‘ANLI/anli_v0.1.zip’

ANLI/anli_v0.1.zip              100%[=====================================================>]  17.76M  5.10MB/s    in 3.5s

2022-12-01 17:52:35 (5.10 MB/s) - ‘ANLI/anli_v0.1.zip’ saved [18621352/18621352]

train_snli.txt
train.csv
test.csv
Archive:  ANLI/anli_v0.1.zip
   creating: ANLI/anli_v0.1/
   creating: ANLI/anli_v0.1/R1/
  inflating: ANLI/anli_v0.1/R1/train.jsonl
   creating: ANLI/__MACOSX/
   creating: ANLI/__MACOSX/anli_v0.1/
   creating: ANLI/__MACOSX/anli_v0.1/R1/
  inflating: ANLI/__MACOSX/anli_v0.1/R1/._train.jsonl
  inflating: ANLI/anli_v0.1/R1/test.jsonl
  inflating: ANLI/__MACOSX/anli_v0.1/R1/._test.jsonl
  inflating: ANLI/anli_v0.1/R1/dev.jsonl
  inflating: ANLI/__MACOSX/anli_v0.1/R1/._dev.jsonl
  inflating: ANLI/__MACOSX/anli_v0.1/._R1
  inflating: ANLI/anli_v0.1/README.txt
  inflating: ANLI/__MACOSX/anli_v0.1/._README.txt
   creating: ANLI/anli_v0.1/R3/
  inflating: ANLI/anli_v0.1/R3/train.jsonl
   creating: ANLI/__MACOSX/anli_v0.1/R3/
  inflating: ANLI/__MACOSX/anli_v0.1/R3/._train.jsonl
  inflating: ANLI/anli_v0.1/R3/test.jsonl
  inflating: ANLI/__MACOSX/anli_v0.1/R3/._test.jsonl
  inflating: ANLI/anli_v0.1/R3/dev.jsonl
  inflating: ANLI/__MACOSX/anli_v0.1/R3/._dev.jsonl
  inflating: ANLI/__MACOSX/anli_v0.1/._R3
   creating: ANLI/anli_v0.1/R2/
  inflating: ANLI/anli_v0.1/R2/train.jsonl
   creating: ANLI/__MACOSX/anli_v0.1/R2/
  inflating: ANLI/__MACOSX/anli_v0.1/R2/._train.jsonl
  inflating: ANLI/anli_v0.1/R2/test.jsonl
  inflating: ANLI/__MACOSX/anli_v0.1/R2/._test.jsonl
  inflating: ANLI/anli_v0.1/R2/dev.jsonl
  inflating: ANLI/__MACOSX/anli_v0.1/R2/._dev.jsonl
  inflating: ANLI/__MACOSX/anli_v0.1/._R2
  inflating: ANLI/__MACOSX/._anli_v0.1

real    0m44.464s
user    0m4.553s
sys     0m2.959s
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets/bin$
```

Check the example data folder ...  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets/corpora$ ls
ANLI  QQP  SNLI
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets/corpora$ cd QQP/
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets/corpora/QQP$ ls
qqp_test.tgz  qqp_train.tgz  test.csv  train.csv
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets/corpora/QQP$ wc {train,test}.csv
   404302   8540953  63399110 train.csv
  2345806  49373483 314015127 test.csv
  2750108  57914436 377414237 total
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets/corpora/QQP$
```

## Training CNN Model with QQP Data

At first, check the GPU status ...  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ nvidia-smi
Thu Dec  1 17:56:59 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.141.03   Driver Version: 470.141.03   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:0A:00.0 Off |                  N/A |
| 26%   45C    P0    58W / 300W |      0MiB / 11019MiB |      1%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA GeForce ...  Off  | 00000000:42:00.0 Off |                  N/A |
| 68%   69C    P0    71W / 257W |      0MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  NVIDIA GeForce ...  Off  | 00000000:43:00.0 Off |                  N/A |
| 24%   64C    P0    83W / 250W |      0MiB / 11016MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$
```

When I train, I got an error ...  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ time python run.py train cnn QQP --experiment_name exp-CNN-QQP
Traceback (most recent call last):
  File "run.py", line 5, in <module>
    from tqdm import tqdm
ModuleNotFoundError: No module named 'tqdm'

real    0m14.550s
user    0m5.239s
sys     0m1.148s
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$
```

Installation of tqdm library ...  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ pip install tqdm==4.15.0
Collecting tqdm==4.15.0
  Using cached tqdm-4.15.0-py2.py3-none-any.whl (46 kB)
Installing collected packages: tqdm
Successfully installed tqdm-4.15.0
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$
```

train again ...  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ time python run.py train cnn QQP --experiment_name exp-CNN-QQP
WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/helpers/summarizer.py:9: The name tf.summary.merge is deprecated. Please use tf.compat.v1.summary.merge instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/helpers/trainer.py:25: The name tf.summary.FileWriter is deprecated. Please use tf.compat.v1.summary.FileWriter instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/collections.py:13: The name tf.GraphKeys is deprecated. Please use tf.compat.v1.GraphKeys instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/config.py:123: The name tf.get_collection is deprecated. Please use tf.compat.v1.get_collection instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/config.py:129: The name tf.add_to_collection is deprecated. Please use tf.compat.v1.add_to_collection instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/config.py:131: The name tf.assign is deprecated. Please use tf.compat.v1.assign instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/utils/data_utils.py:7: The name tf.logging.info is deprecated. Please use tf.compat.v1.logging.info instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/utils/other_utils.py:10: The name tf.logging.set_verbosity is deprecated. Please use tf.compat.v1.logging.set_verbosity instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/utils/other_utils.py:10: The name tf.logging.INFO is deprecated. Please use tf.compat.v1.logging.INFO instead.

INFO:tensorflow:Setting visible GPU to 0
INFO:tensorflow:Reading main configuration.
INFO:tensorflow:Reading configuration for cnn model.
Traceback (most recent call last):
  File "run.py", line 280, in <module>
    main()
  File "run.py", line 274, in main
    train(main_config, model_config, args.model, experiment_name, args.dataset)
  File "run.py", line 43, in train
    train_data = dataset.train_set_pairs()
  File "/home/yekyaw.thu/exp/siamese/multihead-siamese-nets/data/qqp.py", line 28, in train_set_pairs
    return self.train[['question1', 'question2']].as_matrix()
  File "/home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/pandas/core/generic.py", line 5141, in __getattr__
    return object.__getattribute__(self, name)
AttributeError: 'DataFrame' object has no attribute 'as_matrix'

real    0m30.465s
user    0m10.760s
sys     0m1.526s
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$
```

I have to update data/qqp.py ...  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/as_matrix-to-to_numpy.png" alt="replaced \"as_matrix\" with \"to_numpy\"" width="800"/>  
</p>  
<div align="center">
  Fig.1 Replaced "as_matrix" with "to_numpy"   
</div> 

<br />

I train again and check the GPU usage and found that using only one GPU (i.e. 0) as follows:  


```
Every 2.0s: nvidia-smi                                                               gpu.cadt.edu.kh: Thu Dec  1 18:16:04 2022
Thu Dec  1 18:16:05 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.141.03   Driver Version: 470.141.03   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:0A:00.0 Off |                  N/A |
|  0%   47C    P8    14W / 300W |    154MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA GeForce ...  Off  | 00000000:42:00.0 Off |                  N/A |
| 46%   64C    P0    68W / 257W |      0MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  NVIDIA GeForce ...  Off  | 00000000:43:00.0 Off |                  N/A |
| 32%   62C    P0    82W / 250W |      0MiB / 11016MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A   2136404      C   python                            151MiB |
+-----------------------------------------------------------------------------+
```

And thus, I train with the parameter --gpu 0,1,2 for running on 3 GPUs and now, it looks using 3 GPUs, Great! ...  

```
Every 2.0s: nvidia-smi                                                               gpu.cadt.edu.kh: Thu Dec  1 18:29:22 2022
Thu Dec  1 18:29:22 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.141.03   Driver Version: 470.141.03   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:0A:00.0 Off |                  N/A |
|  0%   49C    P8    15W / 300W |    154MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA GeForce ...  Off  | 00000000:42:00.0 Off |                  N/A |
|  7%   56C    P8    23W / 257W |    154MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  NVIDIA GeForce ...  Off  | 00000000:43:00.0 Off |                  N/A |
| 33%   50C    P8    30W / 250W |    154MiB / 11016MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A   2738706      C   python                            151MiB |
|    1   N/A  N/A   2738706      C   python                            151MiB |
|    2   N/A  N/A   2738706      C   python                            151MiB |
+-----------------------------------------------------------------------------+
```

Training situation ...  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ time python run.py train cnn QQP --experiment_name exp-CNN-QQP --gpu 0,1,2
WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/helpers/summarizer.py:9: The name tf.summary.merge is deprecated. Please use tf.compat.v1.summary.merge instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/helpers/trainer.py:25: The name tf.summary.FileWriter is deprecated. Please use tf.compat.v1.summary.FileWriter instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/collections.py:13: The name tf.GraphKeys is deprecated. Please use tf.compat.v1.GraphKeys instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/config.py:123: The name tf.get_collection is deprecated. Please use tf.compat.v1.get_collection instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/config.py:129: The name tf.add_to_collection is deprecated. Please use tf.compat.v1.add_to_collection instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/config.py:131: The name tf.assign is deprecated. Please use tf.compat.v1.assign instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/utils/data_utils.py:7: The name tf.logging.info is deprecated. Please use tf.compat.v1.logging.info instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/utils/other_utils.py:10: The name tf.logging.set_verbosity is deprecated. Please use tf.compat.v1.logging.set_verbosity instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/utils/other_utils.py:10: The name tf.logging.INFO is deprecated. Please use tf.compat.v1.logging.INFO instead.

INFO:tensorflow:Setting visible GPU to 0,1,2
INFO:tensorflow:Reading main configuration.
INFO:tensorflow:Reading configuration for cnn model.
INFO:tensorflow:Chosen word embeddings.
INFO:tensorflow:Maximum sentence length : 237
INFO:tensorflow:Processing sentences with word embeddings...
WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/data_utils.py:201: VocabularyProcessor.__init__ (from tensorflow.contrib.learn.python.learn.preprocessing.text) is deprecated and will be removed in a future version.
Instructions for updating:
Please use tensorflow/transform or tf.data.
WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tensorflow_core/contrib/learn/python/learn/preprocessing/text.py:154: CategoricalVocabulary.__init__ (from tensorflow.contrib.learn.python.learn.preprocessing.categorical_vocabulary) is deprecated and will be removed in a future version.
Instructions for updating:
Please use tensorflow/transform or tf.data.
INFO:tensorflow:Sentences have been successfully processed.
WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tensorflow_core/contrib/learn/python/learn/preprocessing/text.py:170: tokenizer (from tensorflow.contrib.learn.python.learn.preprocessing.text) is deprecated and will be removed in a future version.
Instructions for updating:
Please use tensorflow/transform or tf.data.
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:15: The name tf.placeholder is deprecated. Please use tf.compat.v1.placeholder instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:28: The name tf.variable_scope is deprecated. Please use tf.compat.v1.variable_scope instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:29: The name tf.get_variable is deprecated. Please use tf.compat.v1.get_variable instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/layers/convolution.py:21: conv2d (from tensorflow.python.layers.convolutional) is deprecated and will be removed in a future version.
Instructions for updating:
Use `tf.keras.layers.Conv2D` instead.
WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tensorflow_core/python/layers/convolutional.py:424: Layer.apply (from tensorflow.python.keras.engine.base_layer) is deprecated and will be removed in a future version.
Instructions for updating:
Please use `layer.__call__` method instead.
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/layers/convolution.py:27: max_pooling2d (from tensorflow.python.layers.pooling) is deprecated and will be removed in a future version.
Instructions for updating:
Use keras.layers.MaxPooling2D instead.
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/layers/basics.py:32: dropout (from tensorflow.python.layers.core) is deprecated and will be removed in a future version.
Instructions for updating:
Use keras.layers.dropout instead.
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/layers/losses.py:55: The name tf.losses.mean_squared_error is deprecated. Please use tf.compat.v1.losses.mean_squared_error instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tensorflow_core/python/ops/losses/losses_impl.py:121: where (from tensorflow.python.ops.array_ops) is deprecated and will be removed in a future version.
Instructions for updating:
Use tf.where in 2.0, which has the same broadcast rule as np.where
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/layers/basics.py:66: The name tf.train.AdamOptimizer is deprecated. Please use tf.compat.v1.train.AdamOptimizer instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:42: The name tf.rint is deprecated. Please use tf.math.rint instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:43: to_float (from tensorflow.python.ops.math_ops) is deprecated and will be removed in a future version.
Instructions for updating:
Use `tf.cast` instead.
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:47: The name tf.summary.scalar is deprecated. Please use tf.compat.v1.summary.scalar instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:49: The name tf.summary.merge_all is deprecated. Please use tf.compat.v1.summary.merge_all instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/utils/model_saver.py:9: The name tf.train.Saver is deprecated. Please use tf.compat.v1.train.Saver instead.

WARNING:tensorflow:From run.py:73: The name tf.ConfigProto is deprecated. Please use tf.compat.v1.ConfigProto instead.

WARNING:tensorflow:From run.py:78: The name tf.Session is deprecated. Please use tf.compat.v1.Session instead.

2022-12-01 18:28:42.120766: I tensorflow/core/platform/cpu_feature_guard.cc:142] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
2022-12-01 18:28:42.151368: I tensorflow/core/platform/profile_utils/cpu_utils.cc:94] CPU Frequency: 3499560000 Hz
2022-12-01 18:28:42.154728: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x55a7cf2005d0 initialized for platform Host (this does not guarantee that XLA will be used). Devices:
2022-12-01 18:28:42.154880: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): Host, Default Version
2022-12-01 18:28:42.159292: I tensorflow/stream_executor/platform/default/dso_loader.cc:44] Successfully opened dynamic library libcuda.so.1
2022-12-01 18:28:44.470564: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:983] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2022-12-01 18:28:44.470846: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:983] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2022-12-01 18:28:44.479470: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x55a7cdfe7dd0 initialized for platform CUDA (this does not guarantee that XLA will be used). Devices:
2022-12-01 18:28:44.479611: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): NVIDIA GeForce RTX 2080 Ti, Compute Capability 7.5
2022-12-01 18:28:44.479663: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (1): NVIDIA GeForce RTX 2080 Ti, Compute Capability 7.5
2022-12-01 18:28:44.479682: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (2): NVIDIA GeForce RTX 2080 Ti, Compute Capability 7.5
2022-12-01 18:28:44.482153: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1639] Found device 0 with properties:
name: NVIDIA GeForce RTX 2080 Ti major: 7 minor: 5 memoryClockRate(GHz): 1.65
pciBusID: 0000:0a:00.0
2022-12-01 18:28:44.482718: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:983] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2022-12-01 18:28:44.483842: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1639] Found device 1 with properties:
name: NVIDIA GeForce RTX 2080 Ti major: 7 minor: 5 memoryClockRate(GHz): 1.545
pciBusID: 0000:42:00.0
2022-12-01 18:28:44.484603: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:983] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2022-12-01 18:28:44.486797: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1639] Found device 2 with properties:
name: NVIDIA GeForce RTX 2080 Ti major: 7 minor: 5 memoryClockRate(GHz): 1.545
pciBusID: 0000:43:00.0
2022-12-01 18:28:44.487445: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcudart.so.10.0'; dlerror: libcudart.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 18:28:44.487535: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcublas.so.10.0'; dlerror: libcublas.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 18:28:44.487607: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcufft.so.10.0'; dlerror: libcufft.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 18:28:44.487675: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcurand.so.10.0'; dlerror: libcurand.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 18:28:44.487739: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcusolver.so.10.0'; dlerror: libcusolver.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 18:28:44.487804: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcusparse.so.10.0'; dlerror: libcusparse.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 18:28:44.487881: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcudnn.so.7'; dlerror: libcudnn.so.7: cannot open shared object file: No such file or directory
2022-12-01 18:28:44.487909: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1662] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2022-12-01 18:28:44.488029: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1180] Device interconnect StreamExecutor with strength 1 edge matrix:
2022-12-01 18:28:44.488063: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1186]      0 1 2
2022-12-01 18:28:44.488080: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1199] 0:   N N N
2022-12-01 18:28:44.488093: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1199] 1:   N N N
2022-12-01 18:28:44.488105: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1199] 2:   N N N
WARNING:tensorflow:From run.py:80: The name tf.global_variables_initializer is deprecated. Please use tf.compat.v1.global_variables_initializer instead.

INFO:tensorflow:Training model for 10 epochs
Epochs:   0%|                                                                                          | 0/10 [00:00<?, ?it/sWARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tensorflow_core/python/training/saver.py:963: remove_checkpoint (from tensorflow.python.training.checkpoint_management) is deprecated and will be removed in a future version.
Instructions for updating:
Use standard file APIs to delete files with this prefix.
Epochs: 100%|████████████████████████████████████████████████████████████████████████████████| 10/10 [54:37<00:00, 296.58s/it]

real    56m24.891s
user    591m39.440s
sys     23m20.703s
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$
```

## Testing

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ python run.py predict cnn
WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/helpers/summarizer.py:9: The name tf.summary.merge is deprecated. Please use tf.compat.v1.summary.merge instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/helpers/trainer.py:25: The name tf.summary.FileWriter is deprecated. Please use tf.compat.v1.summary.FileWriter instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/collections.py:13: The name tf.GraphKeys is deprecated. Please use tf.compat.v1.GraphKeys instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/config.py:123: The name tf.get_collection is deprecated. Please use tf.compat.v1.get_collection instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/config.py:129: The name tf.add_to_collection is deprecated. Please use tf.compat.v1.add_to_collection instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/config.py:131: The name tf.assign is deprecated. Please use tf.compat.v1.assign instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/utils/data_utils.py:7: The name tf.logging.info is deprecated. Please use tf.compat.v1.logging.info instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/utils/other_utils.py:10: The name tf.logging.set_verbosity is deprecated. Please use tf.compat.v1.logging.set_verbosity instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/utils/other_utils.py:10: The name tf.logging.INFO is deprecated. Please use tf.compat.v1.logging.INFO instead.

INFO:tensorflow:Setting visible GPU to 0
INFO:tensorflow:Reading main configuration.
INFO:tensorflow:Reading configuration for cnn model.
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:15: The name tf.placeholder is deprecated. Please use tf.compat.v1.placeholder instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:28: The name tf.variable_scope is deprecated. Please use tf.compat.v1.variable_scope instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:29: The name tf.get_variable is deprecated. Please use tf.compat.v1.get_variable instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/layers/convolution.py:21: conv2d (from tensorflow.python.layers.convolutional) is deprecated and will be removed in a future version.
Instructions for updating:
Use `tf.keras.layers.Conv2D` instead.
WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tensorflow_core/python/layers/convolutional.py:424: Layer.apply (from tensorflow.python.keras.engine.base_layer) is deprecated and will be removed in a future version.
Instructions for updating:
Please use `layer.__call__` method instead.
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/layers/convolution.py:27: max_pooling2d (from tensorflow.python.layers.pooling) is deprecated and will be removed in a future version.
Instructions for updating:
Use keras.layers.MaxPooling2D instead.
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/layers/basics.py:32: dropout (from tensorflow.python.layers.core) is deprecated and will be removed in a future version.
Instructions for updating:
Use keras.layers.dropout instead.
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/layers/losses.py:55: The name tf.losses.mean_squared_error is deprecated. Please use tf.compat.v1.losses.mean_squared_error instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tensorflow_core/python/ops/losses/losses_impl.py:121: where (from tensorflow.python.ops.array_ops) is deprecated and will be removed in a future version.
Instructions for updating:
Use tf.where in 2.0, which has the same broadcast rule as np.where
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/layers/basics.py:66: The name tf.train.AdamOptimizer is deprecated. Please use tf.compat.v1.train.AdamOptimizer instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:42: The name tf.rint is deprecated. Please use tf.math.rint instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:43: to_float (from tensorflow.python.ops.math_ops) is deprecated and will be removed in a future version.
Instructions for updating:
Use `tf.cast` instead.
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:47: The name tf.summary.scalar is deprecated. Please use tf.compat.v1.summary.scalar instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:49: The name tf.summary.merge_all is deprecated. Please use tf.compat.v1.summary.merge_all instead.

WARNING:tensorflow:From run.py:204: The name tf.Session is deprecated. Please use tf.compat.v1.Session instead.

2022-12-01 19:55:34.667316: I tensorflow/stream_executor/platform/default/dso_loader.cc:44] Successfully opened dynamic library libcuda.so.1
2022-12-01 19:55:35.803538: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1639] Found device 0 with properties:
name: NVIDIA GeForce RTX 2080 Ti major: 7 minor: 5 memoryClockRate(GHz): 1.65
pciBusID: 0000:0a:00.0
2022-12-01 19:55:35.803648: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcudart.so.10.0'; dlerror: libcudart.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 19:55:35.803689: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcublas.so.10.0'; dlerror: libcublas.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 19:55:35.803740: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcufft.so.10.0'; dlerror: libcufft.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 19:55:35.803796: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcurand.so.10.0'; dlerror: libcurand.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 19:55:35.803843: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcusolver.so.10.0'; dlerror: libcusolver.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 19:55:35.803884: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcusparse.so.10.0'; dlerror: libcusparse.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 19:55:35.803923: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcudnn.so.7'; dlerror: libcudnn.so.7: cannot open shared object file: No such file or directory
2022-12-01 19:55:35.803932: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1662] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2022-12-01 19:55:35.822020: I tensorflow/core/platform/cpu_feature_guard.cc:142] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
2022-12-01 19:55:35.848950: I tensorflow/core/platform/profile_utils/cpu_utils.cc:94] CPU Frequency: 3499560000 Hz
2022-12-01 19:55:35.850100: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x55a9213c1150 initialized for platform Host (this does not guarantee that XLA will be used). Devices:
2022-12-01 19:55:35.850138: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): Host, Default Version
2022-12-01 19:55:36.094616: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x55a91f4aff00 initialized for platform CUDA (this does not guarantee that XLA will be used). Devices:
2022-12-01 19:55:36.094668: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): NVIDIA GeForce RTX 2080 Ti, Compute Capability 7.5
2022-12-01 19:55:36.094789: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1180] Device interconnect StreamExecutor with strength 1 edge matrix:
2022-12-01 19:55:36.094803: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1186]
WARNING:tensorflow:From run.py:205: The name tf.train.Saver is deprecated. Please use tf.compat.v1.train.Saver instead.

Traceback (most recent call last):
  File "run.py", line 280, in <module>
    main()
  File "run.py", line 276, in main
    predict(main_config, model_config, args.model, experiment_name)
  File "run.py", line 212, in predict
    saver.restore(session, last_checkpoint)
  File "/home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tensorflow_core/python/training/saver.py", line 1277, in restore
    raise ValueError("Can't load save_path when it is None.")
ValueError: Can't load save_path when it is None.
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$
```

I updated the run.py, line no. 205 with tf.compat.v1.train.Saver and run again ...  

```
orm Host (this does not guarantee that XLA will be used). Devices:
2022-12-01 19:59:34.042432: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): Host, Default Version
2022-12-01 19:59:34.293683: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x557923918df0 initialized for platform CUDA (this does not guarantee that XLA will be used). Devices:
2022-12-01 19:59:34.293735: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): NVIDIA GeForce RTX 2080 Ti, Compute Capability 7.5
2022-12-01 19:59:34.293858: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1180] Device interconnect StreamExecutor with strength 1 edge matrix:
2022-12-01 19:59:34.293872: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1186]
Traceback (most recent call last):
  File "run.py", line 281, in <module>
    main()
  File "run.py", line 277, in main
    predict(main_config, model_config, args.model, experiment_name)
  File "run.py", line 213, in predict
    saver.restore(session, last_checkpoint)
  File "/home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tensorflow_core/python/training/saver.py", line 1277, in restore
    raise ValueError("Can't load save_path when it is None.")
ValueError: Can't load save_path when it is None.
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$
```

I can solve or run by adding one more command line argument as follows:  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ python run.py predict cnn --experiment_name exp-CNN-QQP
WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/helpers/summarizer.py:9: The name tf.summary.merge is deprecated. Please use tf.compat.v1.summary.merge instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/helpers/trainer.py:25: The name tf.summary.FileWriter is deprecated. Please use tf.compat.v1.summary.FileWriter instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/collections.py:13: The name tf.GraphKeys is deprecated. Please use tf.compat.v1.GraphKeys instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/config.py:123: The name tf.get_collection is deprecated. Please use tf.compat.v1.get_collection instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/config.py:129: The name tf.add_to_collection is deprecated. Please use tf.compat.v1.add_to_collection instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/config.py:131: The name tf.assign is deprecated. Please use tf.compat.v1.assign instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/utils/data_utils.py:7: The name tf.logging.info is deprecated. Please use tf.compat.v1.logging.info instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/utils/other_utils.py:10: The name tf.logging.set_verbosity is deprecated. Please use tf.compat.v1.logging.set_verbosity instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/utils/other_utils.py:10: The name tf.logging.INFO is deprecated. Please use tf.compat.v1.logging.INFO instead.

INFO:tensorflow:Setting visible GPU to 0
INFO:tensorflow:Reading main configuration.
INFO:tensorflow:Reading configuration for cnn model.
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:15: The name tf.placeholder is deprecated. Please use tf.compat.v1.placeholder instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:28: The name tf.variable_scope is deprecated. Please use tf.compat.v1.variable_scope instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:29: The name tf.get_variable is deprecated. Please use tf.compat.v1.get_variable instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/layers/convolution.py:21: conv2d (from tensorflow.python.layers.convolutional) is deprecated and will be removed in a future version.
Instructions for updating:
Use `tf.keras.layers.Conv2D` instead.
WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tensorflow_core/python/layers/convolutional.py:424: Layer.apply (from tensorflow.python.keras.engine.base_layer) is deprecated and will be removed in a future version.
Instructions for updating:
Please use `layer.__call__` method instead.
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/layers/convolution.py:27: max_pooling2d (from tensorflow.python.layers.pooling) is deprecated and will be removed in a future version.
Instructions for updating:
Use keras.layers.MaxPooling2D instead.
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/layers/basics.py:32: dropout (from tensorflow.python.layers.core) is deprecated and will be removed in a future version.
Instructions for updating:
Use keras.layers.dropout instead.
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/layers/losses.py:55: The name tf.losses.mean_squared_error is deprecated. Please use tf.compat.v1.losses.mean_squared_error instead.

WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tensorflow_core/python/ops/losses/losses_impl.py:121: where (from tensorflow.python.ops.array_ops) is deprecated and will be removed in a future version.
Instructions for updating:
Use tf.where in 2.0, which has the same broadcast rule as np.where
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/layers/basics.py:66: The name tf.train.AdamOptimizer is deprecated. Please use tf.compat.v1.train.AdamOptimizer instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:42: The name tf.rint is deprecated. Please use tf.math.rint instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:43: to_float (from tensorflow.python.ops.math_ops) is deprecated and will be removed in a future version.
Instructions for updating:
Use `tf.cast` instead.
WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:47: The name tf.summary.scalar is deprecated. Please use tf.compat.v1.summary.scalar instead.

WARNING:tensorflow:From /home/yekyaw.thu/exp/siamese/multihead-siamese-nets/models/base_model.py:49: The name tf.summary.merge_all is deprecated. Please use tf.compat.v1.summary.merge_all instead.

WARNING:tensorflow:From run.py:204: The name tf.Session is deprecated. Please use tf.compat.v1.Session instead.

2022-12-01 22:01:52.960524: I tensorflow/stream_executor/platform/default/dso_loader.cc:44] Successfully opened dynamic library libcuda.so.1
2022-12-01 22:01:53.152543: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1639] Found device 0 with properties:
name: NVIDIA GeForce RTX 2080 Ti major: 7 minor: 5 memoryClockRate(GHz): 1.65
pciBusID: 0000:0a:00.0
2022-12-01 22:01:53.152624: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcudart.so.10.0'; dlerror: libcudart.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 22:01:53.152665: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcublas.so.10.0'; dlerror: libcublas.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 22:01:53.152698: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcufft.so.10.0'; dlerror: libcufft.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 22:01:53.152738: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcurand.so.10.0'; dlerror: libcurand.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 22:01:53.152773: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcusolver.so.10.0'; dlerror: libcusolver.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 22:01:53.152805: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcusparse.so.10.0'; dlerror: libcusparse.so.10.0: cannot open shared object file: No such file or directory
2022-12-01 22:01:53.152838: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcudnn.so.7'; dlerror: libcudnn.so.7: cannot open shared object file: No such file or directory
2022-12-01 22:01:53.152846: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1662] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2022-12-01 22:01:53.153132: I tensorflow/core/platform/cpu_feature_guard.cc:142] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
2022-12-01 22:01:53.158453: I tensorflow/core/platform/profile_utils/cpu_utils.cc:94] CPU Frequency: 3499560000 Hz
2022-12-01 22:01:53.159136: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x555a80ff7060 initialized for platform Host (this does not guarantee that XLA will be used). Devices:
2022-12-01 22:01:53.159165: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): Host, Default Version
2022-12-01 22:01:53.422502: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x555a7fc9ad70 initialized for platform CUDA (this does not guarantee that XLA will be used). Devices:
2022-12-01 22:01:53.422537: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): NVIDIA GeForce RTX 2080 Ti, Compute Capability 7.5
2022-12-01 22:01:53.422633: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1180] Device interconnect StreamExecutor with strength 1 edge matrix:
2022-12-01 22:01:53.422647: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1186]
INFO:tensorflow:Restoring parameters from model_dir/exp-CNN-QQP/model-7020
First sentence:
```

## Interactive Testing

1st I checked the data:  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets/corpora/QQP$ head test.csv
"test_id","question1","question2"
0,"How does the Surface Pro himself 4 compare with iPad Pro?","Why did Microsoft choose core m3 and not core i3 home Surface Pro 4?"
1,"Should I have a hair transplant at age 24? How much would it cost?","How much cost does hair transplant require?"
2,"What but is the best way to send money from China to the US?","What you send money to China?"
3,"Which food not emulsifiers?","What foods fibre?"
4,"How ""aberystwyth"" start reading?","How their can I start reading?"
5,"How are the two wheeler insurance from Bharti Axa insurance?","I admire I am considering of buying insurance from them"
6,"How can I reduce my belly fat through a diet?","How can I reduce my lower belly fat in one month?"
7,"By scrapping the 500 and 1000 rupee notes, how is RBI planning to fight against issue black money?","How will the recent move to declare 500 and 1000 denomination lewin illegal will curb black money?"
8,"What are the how best books of all time?","What are some of the military history books of all time?"
```

I also checked the training data:  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets/corpora/QQP$ head train.csv
"id","qid1","qid2","question1","question2","is_duplicate"
"0","1","2","What is the step by step guide to invest in share market in india?","What is the step by step guide to invest in share market?","0"
"1","3","4","What is the story of Kohinoor (Koh-i-Noor) Diamond?","What would happen if the Indian government stole the Kohinoor (Koh-i-Noor) diamond back?","0"
"2","5","6","How can I increase the speed of my internet connection while using a VPN?","How can Internet speed be increased by hacking through DNS?","0"
"3","7","8","Why am I mentally very lonely? How can I solve it?","Find the remainder when [math]23^{24}[/math] is divided by 24,23?","0"
"4","9","10","Which one dissolve in water quikly sugar, salt, methane and carbon di oxide?","Which fish would survive in salt water?","0"
"5","11","12","Astrology: I am a Capricorn Sun Cap moon and cap rising...what does that say about me?","I'm a triple Capricorn (Sun, Moon and ascendant in Capricorn) What does this say about me?","1"
"6","13","14","Should I buy tiago?","What keeps childern active and far from phone and video games?","0"
"7","15","16","How can I be a good geologist?","What should I do to be a great geologist?","1"
"8","17","18","When do you use シ instead of し?","When do you use ""&"" instead of ""and""?","0"
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets/corpora/QQP$
```

testing ...  

```
(siamese) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets$ python run.py predict cnn --experiment_name exp-CNN-QQP
WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tflearn/helpers/summarizer.py:9: The name tf.summary.merge is deprecated. Please use tf.compat.v1.summary.merge instead.
...
...
...
2022-12-01 22:01:53.422502: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x555a7fc9ad70 initialized for platform CUDA (this does not guarantee that XLA will be used). Devices:
2022-12-01 22:01:53.422537: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): NVIDIA GeForce RTX 2080 Ti, Compute Capability 7.5
2022-12-01 22:01:53.422633: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1180] Device interconnect StreamExecutor with strength 1 edge matrix:
2022-12-01 22:01:53.422647: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1186]
INFO:tensorflow:Restoring parameters from model_dir/exp-CNN-QQP/model-7020
First sentence:What is the step by step guide to invest in share market in india?
Second sentence:What is the step by step guide to invest in share market?
WARNING:tensorflow:From /home/yekyaw.thu/.conda/envs/siamese/lib/python3.6/site-packages/tensorflow_core/contrib/learn/python/learn/preprocessing/text.py:203: tokenizer (from tensorflow.contrib.learn.python.learn.preprocessing.text) is deprecated and will be removed in a future version.
Instructions for updating:
Please use tensorflow/transform or tf.data.
[array([[0.]], dtype=float32)]
First sentence:Astrology: I am a Capricorn Sun Cap moon and cap rising...what does that say about me?
Second sentence:I'm a triple Capricorn (Sun, Moon and ascendant in Capricorn) What does this say about me?
[array([[0.]], dtype=float32)]
First sentence:How can I be a good geologist?
Second sentence:What should I do to be a great geologist?
[array([[1.]], dtype=float32)]
First sentence:
```

## Installation of Jupyter

Jupyter notebook နဲ့ run ဖို့အတွက် ပြင်ဆင်ခဲ့တာပါ။  

pip3 install --upgrade pip  

pip3 install jupyter  

## Testing with Port Forwarding

နောက်ထပ် terminal တစ်ခု ဖွင့်ပြီး ကိုယ့် local စက်ကနေ run တာလည်း အဆင်ပြေပါတယ်။  

## Datapreparation for Myanmar Data

အရင် run ခဲ့တဲ့ Siamese မှာက TSV (Tab Separated Values) ဖိုင်ကို သုံးခဲ့တာမို့လို့ လက်ရှိ run ဖို့ ပြင်နေတဲ့ code မှာက CSV (Comma Separated Values) ဖိုင်မို့လို့ CSV ဖိုင် ပြောင်းဖို့အတွက် shell script တစ်ပုဒ် ရေးခဲ့တယ်။  

```bash
(multihead-siamese) ye@ykt-pro:~/Downloads/2mmt/manual-my2/4release/csv$ cat ./tsv2csv.sh 
#!/bin/bash

baseName=`basename "$1"`

cut -f1 $1 > col1.tmp
cut -f2 $1 > col2.tmp
cut -f3 $1 > col3.tmp

paste -d "," col2.tmp col3.tmp col1.tmp > csv.tmp
awk 'BEGIN{i=0} /.*/{printf "%d,% s\n",i,$0; i++}'  csv.tmp > $baseName.csv
rm *.tmp;
(multihead-siamese) ye@ykt-pro:~/Downloads/2mmt/manual-my2/4release/csv$
```

Run as follows:  

```
(multihead-siamese) ye@ykt-pro:~/Downloads/2mmt/manual-my2/4release/csv$ ./tsv2csv.sh ./closed-test 
(multihead-siamese) ye@ykt-pro:~/Downloads/2mmt/manual-my2/4release/csv$ ./tsv2csv.sh ./open-test.final.manual 
```

check the output file format and I found error on train.txt.csv file ...  

```
(multihead-siamese) ye@ykt-pro:~/Downloads/2mmt/manual-my2/4release/csv$ head -3 *.csv
==> closed-test.csv <==
0,ကောင်း လိုက် တဲ့ သတင်း လေး ပါ,ကောင်း သော သတင်း ပါ ပဲ,1
1,ခု ဒီ တံဆိပ် က ဈေးလိုက် နေ တယ် ။,ဒီ တံဆိပ် က ဈေး အရမ်း တက် နေ တယ် ။,0
2,ကျွန်မ ဘက် က စ ပြီး ကျေအေး ပေး တယ် နော်,ကျွန်မ ဘက် က စ ပြီး ကျေလည် တာ နော်,1

==> open-test.final.manual.csv <==
0,၁၁ ဒေါ်လာ ကျ ပါ တယ် ။,၁၁ နာရီ လာ ခေါ် မယ် ။,0
1,၁၁ နာရီ ခွဲ အိမ် ပြန် မယ် ။,၁၁ နာရီ ခွဲ အရောက် လာ ပါ ။,0
2,၁၁:၃၀ ပြန်ရောက် မယ် လို့ ထင် သလား ။,၁၁:၃၀ အတိ မှာ ပြန်ရောက် လာ ခဲ့ တယ် ။,0
```

Prepare a code for the training data ...  

```
(multihead-siamese) ye@ykt-pro:~/Downloads/2mmt/manual-my2/4release/csv$ cat tsv2csv4train.sh 
#!/bin/bash
# this script is for the training data (i.e. different with test data tsv file format)  

baseName=`basename "$1"`

cut -f1 $1 > col1.tmp
cut -f2 $1 > col2.tmp
cut -f3 $1 > col3.tmp

paste -d "," col1.tmp col2.tmp col3.tmp > csv.tmp
awk 'BEGIN{i=0} /.*/{printf "%d,% s\n",i,$0; i++}'  csv.tmp > $baseName.csv
rm *.tmp;
(multihead-siamese) ye@ykt-pro:~/Downloads/2mmt/manual-my2/4release/csv$
```

running as follows:  

```
(multihead-siamese) ye@ykt-pro:~/Downloads/2mmt/manual-my2/4release/csv$ ./tsv2csv4train.sh train 
(multihead-siamese) ye@ykt-pro:~/Downloads/2mmt/manual-my2/4release/csv$ ls
closed-test.csv  open-test.final.manual.csv  train  train.csv  tsv2csv4train.sh  tsv2csv.sh
```

head command နဲ့ စစ်ကြည့်တဲ့အခါမှာ <200b> တွေ ရောပါနေသေးတယ် ဆိုတာကို တွေ့ရတယ်။  

```
(multihead-siamese) ye@ykt-pro:~/Downloads/2mmt/manual-my2/4release/csv$ head train.csv
0,ကျွန်တော် စီး ဖို့ ချစ်စရာ ဖိနပ် တစ် ရံ ကို ရှာ မတွေ့လို့ပါ ။,တစ်ခါတစ်ခါ ကျွန်တော်က ခင်ဗျား ကို အရမ်း အပြောင်းအလဲများတဲ့လူ လို့ ထင်မိတယ် ။,0
1,​ ကျေးဇူး ပဲ ၊ ကျွန်တော် ဘယ်လောက် ပေး ရ မလဲ ။,ကျေးဇူး နော် ၊ ဘယ်တော့ ပြန် တွေ့ ကြ မလဲ ။,0
2,​ ကျေးဇူး အများကြီး တင် ပါ တယ် ။,ကျေးဇူးတင် တယ် လို့ မ ပြော သွား ဘူး ။,0
3,​ ကျောင်းအုပ်ကြီး က တော် တဲ့ ကျောင်းသား တွေ ကို ချီးကျူး ကြ တယ် ။,ကျောင်းအုပ်ကြီး က ဆိုး တဲ့ ကျောင်းသား တွေ ကို ဒဏ်ပေး ကြ တယ် ။,0
4,​ ကောင်း ပြီ ကျွန်တော် လုပ် ပါ့ မယ် ။,ကောင်း ပြီ ကျွန်တော် ဒီ အလုပ် ကို လက်မခံ တော့ ဘူး ။,0
5,​ ကောင်း သော ည ပါ ။,ကောင်း သော နေ့ ပါ ။,0
6,ကောင်လေး က လူကြီး ကို ရှင်းရှင်းလင်းလင်း မြင် နေ တယ် ။,သာယာတဲ့ နေ့ကလေး ပါပဲ ။,0
7,ခဏအကြာမှာ ကျွန်တော် ခင်ဗျား ကို ပြန်ဆက် ပါရစေ ။,ခဏ ကြာတော့ သူမ တည်ငြိမ် စပြုလာ ပြီး သူ ပြောတာကို နားထောင် နေတော့တယ် ။,0
8,ခေါင်မိုး ပေါ်မှာ ကြောင် တစ်ကောင် ရှိ တယ် ။,အတန်း လွတ်သွားမှာ စိုးတယ် ။,0
9,ငါ ခိုင်းတာ မင်း လုပ် ခဲ့လား ။,ဒါက အသစ် တပ်ဆင်မှာ ဖြစ် တယ် ။,0
```

I removed 200b from train.csv file ...  

```
(multihead-siamese) ye@ykt-pro:~/Downloads/2mmt/manual-my2/4release/csv$ cat rm-200b-200d.sh 
#!/bin/bash

# for removing "\u200b" and "\u200d" characters

sed -i -e "s/$(echo -ne '\u200b')//g; s/$(echo -ne '\u200d')//g;" $1;
(multihead-siamese) ye@ykt-pro:~/Downloads/2mmt/manual-my2/4release/csv$ ./rm-200b-200d.sh train.csv
```

Check the number of sentences ...  

```
(multihead-siamese) ye@ykt-pro:~/Downloads/2mmt/manual-my2/4release/csv$ wc *.csv
   1000   14906  206125 closed-test.csv
   1000   10706  142470 open-test.final.manual.csv
  40461  591452 8580488 train.csv
  42461  617064 8929083 total
```

## Training with Myanmar Data  


I copied Myanmar paraphrase data to the GPU server ...  
Here, test.csv file is the open test data.  

```
(base) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets/corpora/MYPARA$ ls
closed-test.csv  test.csv  train.csv
(base) yekyaw.thu@gpu:~/exp/siamese/multihead-siamese-nets/corpora/MYPARA$
```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
