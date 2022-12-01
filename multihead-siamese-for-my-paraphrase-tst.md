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

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
