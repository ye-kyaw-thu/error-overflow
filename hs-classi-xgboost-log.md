# Hate Speech Classification with XGBoost

Date: 6 April 2024  
By: Ye Kyaw Thu, LU Lab., Myanmar  

## Installation  

### Pip 21.3+ is required
pip install xgboost  

### CPU only
conda install -c conda-forge py-xgboost-cpu  

### Use NVIDIA GPU
conda install -c conda-forge py-xgboost-gpu  

### Install with Conda

```
(base) yekyaw.thu@gpu:~/exp$ conda activate py3.10.6
(py3.10.6) yekyaw.thu@gpu:~/exp$ conda install -c conda-forge py-xgboost-gpu
Collecting package metadata (current_repodata.json): done
Solving environment: |
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::binutils_impl_linux-64==2.38=h2a08ee3_1
  - defaults/linux-64::ncurses==6.3=h5eee18b_3
  - defaults/linux-64::setuptools==63.4.1=py310h06a4308_0
  - defaults/linux-64::libuuid==1.0.3=h7f8727e_2
  - defaults/linux-64::bzip2==1.0.8=h7b6447c_0
  - defaults/linux-64::xz==5.2.6=h5eee18b_0
  - defaults/linux-64::readline==8.1.2=h7f8727e_1
  - defaults/linux-64::openssl==1.1.1q=h7f8727e_0
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::python==3.10.6=haa1d7c7_0
  - defaults/linux-64::zlib==1.2.12=h5eee18b_3
  - defaults/linux-64::libgcc-devel_linux-64==11.2.0=h1234567_1
  - defaults/linux-64::pip==22.2.2=py310h06a4308_0
  - defaults/linux-64::certifi==2022.9.24=py310h06a4308_0
  - defaults/linux-64::gcc_impl_linux-64==11.2.0=h1234567_1
  - defaults/linux-64::libffi==3.3=he6710b0_2
  - defaults/linux-64::sqlite==3.39.3=h5082296_0
  - defaults/linux-64::binutils_linux-64==2.38.0=hc2dff05_0
  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
  - defaults/noarch::wheel==0.37.1=pyhd3eb1b0_0
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 24.3.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/py3.10.6

  added / updated specs:
    - py-xgboost-gpu


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    _libgcc_mutex-0.1          |      conda_forge           3 KB  conda-forge
    _openmp_mutex-4.5          |            2_gnu          23 KB  conda-forge
    _py-xgboost-mutex-2.0      |            gpu_0          12 KB  conda-forge
    joblib-1.3.2               |     pyhd8ed1ab_0         216 KB  conda-forge
    libblas-3.9.0              |21_linux64_openblas          14 KB  conda-forge
    libcblas-3.9.0             |21_linux64_openblas          14 KB  conda-forge
    libgfortran-ng-13.2.0      |       h69a702a_5          23 KB  conda-forge
    libgfortran5-13.2.0        |       ha4646dd_5         1.4 MB  conda-forge
    liblapack-3.9.0            |21_linux64_openblas          14 KB  conda-forge
    libopenblas-0.3.26         |pthreads_h413a1c8_0         5.3 MB  conda-forge
    libxgboost-2.0.3           |   cpu_hce603c2_3         5.0 MB  conda-forge
    numpy-1.26.4               |  py310hb13e2d6_0         6.7 MB  conda-forge
    py-xgboost-2.0.3           |cuda118_pyh103b7b7_3         130 KB  conda-forge
    py-xgboost-gpu-2.0.3       |     pyh7984362_3          16 KB  conda-forge
    python_abi-3.10            |          2_cp310           4 KB  conda-forge
    scikit-learn-1.4.1.post1   |  py310h1fdf081_0         8.8 MB  conda-forge
    scipy-1.13.0               |  py310hb13e2d6_0        15.6 MB  conda-forge
    threadpoolctl-3.4.0        |     pyhc1e730c_0          22 KB  conda-forge
    ------------------------------------------------------------
                                           Total:        43.2 MB

The following NEW packages will be INSTALLED:

  _py-xgboost-mutex  conda-forge/linux-64::_py-xgboost-mutex-2.0-gpu_0
  joblib             conda-forge/noarch::joblib-1.3.2-pyhd8ed1ab_0
  libblas            conda-forge/linux-64::libblas-3.9.0-21_linux64_openblas
  libcblas           conda-forge/linux-64::libcblas-3.9.0-21_linux64_openblas
  libgfortran-ng     conda-forge/linux-64::libgfortran-ng-13.2.0-h69a702a_5
  libgfortran5       conda-forge/linux-64::libgfortran5-13.2.0-ha4646dd_5
  liblapack          conda-forge/linux-64::liblapack-3.9.0-21_linux64_openblas
  libopenblas        conda-forge/linux-64::libopenblas-0.3.26-pthreads_h413a1c8_0
  libxgboost         conda-forge/linux-64::libxgboost-2.0.3-cpu_hce603c2_3
  numpy              conda-forge/linux-64::numpy-1.26.4-py310hb13e2d6_0
  py-xgboost         conda-forge/noarch::py-xgboost-2.0.3-cuda118_pyh103b7b7_3
  py-xgboost-gpu     conda-forge/noarch::py-xgboost-gpu-2.0.3-pyh7984362_3
  python_abi         conda-forge/linux-64::python_abi-3.10-2_cp310
  scikit-learn       conda-forge/linux-64::scikit-learn-1.4.1.post1-py310h1fdf081_0
  scipy              conda-forge/linux-64::scipy-1.13.0-py310hb13e2d6_0
  threadpoolctl      conda-forge/noarch::threadpoolctl-3.4.0-pyhc1e730c_0

The following packages will be UPDATED:

  ca-certificates    pkgs/main::ca-certificates-2022.07.19~ --> conda-forge::ca-certificates-2024.2.2-hbcca054_0
  libgcc-ng          pkgs/main::libgcc-ng-11.2.0-h1234567_1 --> conda-forge::libgcc-ng-13.2.0-h807b86a_5
  libgomp              pkgs/main::libgomp-11.2.0-h1234567_1 --> conda-forge::libgomp-13.2.0-h807b86a_5
  libstdcxx-ng       pkgs/main::libstdcxx-ng-11.2.0-h12345~ --> conda-forge::libstdcxx-ng-13.2.0-h7e041cc_5

The following packages will be SUPERSEDED by a higher-priority channel:

  _libgcc_mutex           pkgs/main::_libgcc_mutex-0.1-main --> conda-forge::_libgcc_mutex-0.1-conda_forge
  _openmp_mutex          pkgs/main::_openmp_mutex-5.1-1_gnu --> conda-forge::_openmp_mutex-4.5-2_gnu


Proceed ([y]/n)? y


Downloading and Extracting Packages
py-xgboost-gpu-2.0.3 | 16 KB     | ####################################### | 100%
numpy-1.26.4         | 6.7 MB    | ####################################### | 100%
_libgcc_mutex-0.1    | 3 KB      | ####################################### | 100%
libopenblas-0.3.26   | 5.3 MB    | ####################################### | 100%
_openmp_mutex-4.5    | 23 KB     | ####################################### | 100%
joblib-1.3.2         | 216 KB    | ####################################### | 100%
scipy-1.13.0         | 15.6 MB   | ####################################### | 100%
py-xgboost-2.0.3     | 130 KB    | ####################################### | 100%
libgfortran5-13.2.0  | 1.4 MB    | ####################################### | 100%
libxgboost-2.0.3     | 5.0 MB    | ####################################### | 100%
scikit-learn-1.4.1.p | 8.8 MB    | ####################################### | 100%
libblas-3.9.0        | 14 KB     | ####################################### | 100%
libgfortran-ng-13.2. | 23 KB     | ####################################### | 100%
liblapack-3.9.0      | 14 KB     | ####################################### | 100%
threadpoolctl-3.4.0  | 22 KB     | ####################################### | 100%
python_abi-3.10      | 4 KB      | ####################################### | 100%
_py-xgboost-mutex-2. | 12 KB     | ####################################### | 100%
libcblas-3.9.0       | 14 KB     | ####################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(py3.10.6) yekyaw.thu@gpu:~/exp$
```

## import test

```
(py3.10.6) yekyaw.thu@gpu:~/exp$ python
Python 3.10.6 (main, Oct  7 2022, 20:19:58) [GCC 11.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import xgboost as xgb
>>> print(xgb.__version__)
2.0.3
>>>
```

## Test Run with Python Interface

Folder and example file preparations:  

```
(py3.10.6) yekyaw.thu@gpu:~/exp$ mkdir xgboost
(py3.10.6) yekyaw.thu@gpu:~/exp$ cd xgboost/
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost$ mkdir test-run
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost$ cd test-run/
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost/test-run$ nano runexp.sh
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost/test-run$ nano train.py
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost/test-run$
```

Reference Link:
[https://github.com/dmlc/xgboost/tree/master/demo/multiclass_classification](https://github.com/dmlc/xgboost/tree/master/demo/multiclass_classification)  

train.py is as follows:  

```python
#!/usr/bin/python

from __future__ import division

import numpy as np

import xgboost as xgb

# label need to be 0 to num_class -1
data = np.loadtxt('./dermatology.data', delimiter=',',
        converters={33: lambda x:int(x == '?'), 34: lambda x:int(x) - 1})
sz = data.shape

train = data[:int(sz[0] * 0.7), :]
test = data[int(sz[0] * 0.7):, :]

train_X = train[:, :33]
train_Y = train[:, 34]

test_X = test[:, :33]
test_Y = test[:, 34]

xg_train = xgb.DMatrix(train_X, label=train_Y)
xg_test = xgb.DMatrix(test_X, label=test_Y)
# setup parameters for xgboost
param = {}
# use softmax multi-class classification
param['objective'] = 'multi:softmax'
# scale weight of positive examples
param['eta'] = 0.1
param['max_depth'] = 6
param['nthread'] = 4
param['num_class'] = 6

watchlist = [(xg_train, 'train'), (xg_test, 'test')]
num_round = 5
bst = xgb.train(param, xg_train, num_round, watchlist)
# get prediction
pred = bst.predict(xg_test)
error_rate = np.sum(pred != test_Y) / test_Y.shape[0]
print('Test error using softmax = {}'.format(error_rate))

# do the same thing again, but output probabilities
param['objective'] = 'multi:softprob'
bst = xgb.train(param, xg_train, num_round, watchlist)
# Note: this convention has been changed since xgboost-unity
# get prediction, this is in 1D array, need reshape to (ndata, nclass)
pred_prob = bst.predict(xg_test).reshape(test_Y.shape[0], 6)
pred_label = np.argmax(pred_prob, axis=1)
error_rate = np.sum(pred_label != test_Y) / test_Y.shape[0]
print('Test error using softprob = {}'.format(error_rate))
```

bash script is as follows:  

```bash
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost/test-run$ cat runexp.sh
#!/bin/bash
if [ -f dermatology.data ]
then
    echo "use existing data to run multi class classification"
else
    echo "getting data from uci, make sure you are connected to internet"
    wget https://archive.ics.uci.edu/ml/machine-learning-databases/dermatology/dermatology.data
fi
python train.py
```

test training/testing ...  

```
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost/test-run$ chmod +x ./runexp.sh
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost/test-run$ time ./runexp.sh | tee test-run.log
getting data from uci, make sure you are connected to internet
--2024-04-06 23:17:12--  https://archive.ics.uci.edu/ml/machine-learning-databases/dermatology/dermatology.data
Resolving archive.ics.uci.edu (archive.ics.uci.edu)... 128.195.10.252
Connecting to archive.ics.uci.edu (archive.ics.uci.edu)|128.195.10.252|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified
Saving to: ‘dermatology.data’

dermatology.data         [  <=>                ]  25.36K   123KB/s    in 0.2s

2024-04-06 23:17:14 (123 KB/s) - ‘dermatology.data’ saved [25964]

/home/yekyaw.thu/.conda/envs/py3.10.6/lib/python3.10/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:1.54662  test-mlogloss:1.57447
[1]     train-mlogloss:1.35498  test-mlogloss:1.39797
[2]     train-mlogloss:1.19883  test-mlogloss:1.25218
[3]     train-mlogloss:1.06734  test-mlogloss:1.13098
[4]     train-mlogloss:0.95564  test-mlogloss:1.03268
Test error using softmax = 0.09090909090909091
[0]     train-mlogloss:1.54662  test-mlogloss:1.57447
[1]     train-mlogloss:1.35498  test-mlogloss:1.39797
[2]     train-mlogloss:1.19883  test-mlogloss:1.25218
[3]     train-mlogloss:1.06734  test-mlogloss:1.13098
[4]     train-mlogloss:0.95564  test-mlogloss:1.03268
Test error using softprob = 0.09090909090909091

real    0m2.268s
user    0m1.276s
sys     0m1.377s
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost/test-run$
```

## Check Dermatology Data Format

```
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost/test-run$ wc dermatology.data
  366   366 25964 dermatology.data
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost/test-run$ head dermatology.data
2,2,0,3,0,0,0,0,1,0,0,0,0,0,0,3,2,0,0,0,0,0,0,0,0,0,0,3,0,0,0,1,0,55,2
3,3,3,2,1,0,0,0,1,1,1,0,0,1,0,1,2,0,2,2,2,2,2,1,0,0,0,0,0,0,0,1,0,8,1
2,1,2,3,1,3,0,3,0,0,0,1,0,0,0,1,2,0,2,0,0,0,0,0,2,0,2,3,2,0,0,2,3,26,3
2,2,2,0,0,0,0,0,3,2,0,0,0,3,0,0,2,0,3,2,2,2,2,0,0,3,0,0,0,0,0,3,0,40,1
2,3,2,2,2,2,0,2,0,0,0,1,0,0,0,1,2,0,0,0,0,0,0,0,2,2,3,2,3,0,0,2,3,45,3
2,3,2,0,0,0,0,0,0,0,0,0,2,1,0,2,2,0,2,0,0,0,1,0,0,0,0,2,0,0,0,1,0,41,2
2,1,0,2,0,0,0,0,0,0,0,0,0,0,3,1,3,0,0,0,2,0,0,0,0,0,0,0,0,0,0,2,0,18,5
2,2,3,3,3,3,0,2,0,0,0,2,0,0,0,2,3,0,0,0,0,0,0,0,0,2,2,3,2,0,0,3,3,57,3
2,2,1,0,2,0,0,0,0,0,0,0,0,0,0,2,1,0,1,0,0,0,0,0,0,0,0,2,0,0,0,2,0,22,4
2,2,1,0,1,0,0,0,0,0,0,0,0,0,0,3,2,0,2,0,0,0,0,0,0,0,0,2,0,0,0,2,0,30,4
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost/test-run$
```

## Library Installations

လိုအပ်မယ့် library တွေကို install လုပ်ခဲ့ ...  
အရင်ဆုံး gensim ကို installation လုပ်။  

```
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost$ pip install gensim
Collecting gensim
  Downloading gensim-4.3.2-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (8.4 kB)
Requirement already satisfied: numpy>=1.18.5 in /home/yekyaw.thu/.conda/envs/py3.10.6/lib/python3.10/site-packages (from gensim) (1.26.4)
Requirement already satisfied: scipy>=1.7.0 in /home/yekyaw.thu/.conda/envs/py3.10.6/lib/python3.10/site-packages (from gensim) (1.13.0)
Collecting smart-open>=1.8.1 (from gensim)
  Downloading smart_open-7.0.4-py3-none-any.whl.metadata (23 kB)
Requirement already satisfied: wrapt in /home/yekyaw.thu/.conda/envs/py3.10.6/lib/python3.10/site-packages (from smart-open>=1.8.1->gensim) (1.16.0)
Downloading gensim-4.3.2-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (26.5 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 26.5/26.5 MB 15.7 MB/s eta 0:00:00
Downloading smart_open-7.0.4-py3-none-any.whl (61 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 61.2/61.2 kB 625.8 kB/s eta 0:00:00
Installing collected packages: smart-open, gensim
Successfully installed gensim-4.3.2 smart-open-7.0.4
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost$
```

scipy installation ...  

```
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost$ pip install scipy
Collecting scipy
  Downloading scipy-1.13.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (60 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 60.6/60.6 kB 351.7 kB/s eta 0:00:00
Requirement already satisfied: numpy<2.3,>=1.22.4 in /home/yekyaw.thu/.conda/envs/py3.10.6/lib/python3.10/site-packages (from scipy) (1.26.4)
Downloading scipy-1.13.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (38.6 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 38.6/38.6 MB 12.4 MB/s eta 0:00:00
Installing collected packages: scipy
Successfully installed scipy-1.13.0
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost$
```

## Check with pipdeptree  

```
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost$ pip install pipdeptree
Collecting pipdeptree
  Downloading pipdeptree-2.17.0-py3-none-any.whl.metadata (15 kB)
Requirement already satisfied: packaging>=23.1 in /home/yekyaw.thu/.conda/envs/py3.10.6/lib/python3.10/site-packages (from pipdeptree) (24.0)
Requirement already satisfied: pip>=23.1.2 in /home/yekyaw.thu/.conda/envs/py3.10.6/lib/python3.10/site-packages (from pipdeptree) (24.0)
Downloading pipdeptree-2.17.0-py3-none-any.whl (28 kB)
Installing collected packages: pipdeptree
Successfully installed pipdeptree-2.17.0
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost$
```

```
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost$ pipdeptree
datasets==2.18.0
├── aiohttp [required: Any, installed: 3.9.3]
│   ├── aiosignal [required: >=1.1.2, installed: 1.3.1]
│   │   └── frozenlist [required: >=1.1.0, installed: 1.4.1]
│   ├── async-timeout [required: >=4.0,<5.0, installed: 4.0.3]
│   ├── attrs [required: >=17.3.0, installed: 23.2.0]
│   ├── frozenlist [required: >=1.1.1, installed: 1.4.1]
│   ├── multidict [required: >=4.5,<7.0, installed: 6.0.5]
│   └── yarl [required: >=1.0,<2.0, installed: 1.9.4]
│       ├── idna [required: >=2.0, installed: 3.6]
│       └── multidict [required: >=4.0, installed: 6.0.5]
├── dill [required: >=0.3.0,<0.3.9, installed: 0.3.8]
├── filelock [required: Any, installed: 3.13.3]
├── fsspec [required: >=2023.1.0,<=2024.2.0, installed: 2024.2.0]
├── huggingface-hub [required: >=0.19.4, installed: 0.22.2]
│   ├── filelock [required: Any, installed: 3.13.3]
│   ├── fsspec [required: >=2023.5.0, installed: 2024.2.0]
│   ├── packaging [required: >=20.9, installed: 24.0]
│   ├── PyYAML [required: >=5.1, installed: 6.0.1]
│   ├── requests [required: Any, installed: 2.31.0]
│   │   ├── certifi [required: >=2017.4.17, installed: 2022.9.24]
│   │   ├── charset-normalizer [required: >=2,<4, installed: 3.3.2]
│   │   ├── idna [required: >=2.5,<4, installed: 3.6]
│   │   └── urllib3 [required: >=1.21.1,<3, installed: 2.2.1]
│   ├── tqdm [required: >=4.42.1, installed: 4.66.2]
│   └── typing_extensions [required: >=3.7.4.3, installed: 4.10.0]
├── multiprocess [required: Any, installed: 0.70.16]
│   └── dill [required: >=0.3.8, installed: 0.3.8]
├── numpy [required: >=1.17, installed: 1.26.4]
├── packaging [required: Any, installed: 24.0]
├── pandas [required: Any, installed: 2.2.1]
│   ├── numpy [required: >=1.22.4,<2, installed: 1.26.4]
│   ├── python-dateutil [required: >=2.8.2, installed: 2.9.0.post0]
│   │   └── six [required: >=1.5, installed: 1.16.0]
│   ├── pytz [required: >=2020.1, installed: 2024.1]
│   └── tzdata [required: >=2022.7, installed: 2024.1]
├── pyarrow [required: >=12.0.0, installed: 15.0.2]
│   └── numpy [required: >=1.16.6,<2, installed: 1.26.4]
├── pyarrow-hotfix [required: Any, installed: 0.6]
├── PyYAML [required: >=5.1, installed: 6.0.1]
├── requests [required: >=2.19.0, installed: 2.31.0]
│   ├── certifi [required: >=2017.4.17, installed: 2022.9.24]
│   ├── charset-normalizer [required: >=2,<4, installed: 3.3.2]
│   ├── idna [required: >=2.5,<4, installed: 3.6]
│   └── urllib3 [required: >=1.21.1,<3, installed: 2.2.1]
├── tqdm [required: >=4.62.1, installed: 4.66.2]
└── xxhash [required: Any, installed: 3.4.1]
gensim==4.3.2
├── numpy [required: >=1.18.5, installed: 1.26.4]
├── scipy [required: >=1.7.0, installed: 1.13.0]
│   └── numpy [required: >=1.22.4,<2.3, installed: 1.26.4]
└── smart-open [required: >=1.8.1, installed: 7.0.4]
    └── wrapt [required: Any, installed: 1.16.0]
pipdeptree==2.17.0
├── packaging [required: >=23.1, installed: 24.0]
└── pip [required: >=23.1.2, installed: 24.0]
scikit-learn==1.4.1.post1
├── joblib [required: >=1.2.0, installed: 1.3.2]
├── numpy [required: >=1.19.5,<2.0, installed: 1.26.4]
├── scipy [required: >=1.6.0, installed: 1.13.0]
│   └── numpy [required: >=1.22.4,<2.3, installed: 1.26.4]
└── threadpoolctl [required: >=2.0.0, installed: 3.4.0]
tensorflow==2.16.1
├── absl-py [required: >=1.0.0, installed: 2.1.0]
├── astunparse [required: >=1.6.0, installed: 1.6.3]
│   ├── six [required: >=1.6.1,<2.0, installed: 1.16.0]
│   └── wheel [required: >=0.23.0,<1.0, installed: 0.37.1]
├── flatbuffers [required: >=23.5.26, installed: 24.3.7]
├── gast [required: >=0.2.1,!=0.5.2,!=0.5.1,!=0.5.0, installed: 0.5.4]
├── google-pasta [required: >=0.1.1, installed: 0.2.0]
│   └── six [required: Any, installed: 1.16.0]
├── grpcio [required: >=1.24.3,<2.0, installed: 1.62.1]
├── h5py [required: >=3.10.0, installed: 3.10.0]
│   └── numpy [required: >=1.17.3, installed: 1.26.4]
├── keras [required: >=3.0.0, installed: 3.0.5]
│   ├── absl-py [required: Any, installed: 2.1.0]
│   ├── dm-tree [required: Any, installed: 0.1.8]
│   ├── h5py [required: Any, installed: 3.10.0]
│   │   └── numpy [required: >=1.17.3, installed: 1.26.4]
│   ├── ml-dtypes [required: Any, installed: 0.3.2]
│   │   ├── numpy [required: >1.20, installed: 1.26.4]
│   │   └── numpy [required: >=1.21.2, installed: 1.26.4]
│   ├── namex [required: Any, installed: 0.0.7]
│   ├── numpy [required: Any, installed: 1.26.4]
│   └── rich [required: Any, installed: 13.7.1]
│       ├── markdown-it-py [required: >=2.2.0, installed: 3.0.0]
│       │   └── mdurl [required: ~=0.1, installed: 0.1.2]
│       └── Pygments [required: >=2.13.0,<3.0.0, installed: 2.17.2]
├── libclang [required: >=13.0.0, installed: 18.1.1]
├── ml-dtypes [required: ~=0.3.1, installed: 0.3.2]
│   ├── numpy [required: >1.20, installed: 1.26.4]
│   └── numpy [required: >=1.21.2, installed: 1.26.4]
├── numpy [required: >=1.23.5,<2.0.0, installed: 1.26.4]
├── opt-einsum [required: >=2.3.2, installed: 3.3.0]
│   └── numpy [required: >=1.7, installed: 1.26.4]
├── packaging [required: Any, installed: 24.0]
├── protobuf [required: >=3.20.3,<5.0.0dev,!=4.21.5,!=4.21.4,!=4.21.3,!=4.21.2,!=4.21.1,!=4.21.0, installed: 4.25.3]
├── requests [required: >=2.21.0,<3, installed: 2.31.0]
│   ├── certifi [required: >=2017.4.17, installed: 2022.9.24]
│   ├── charset-normalizer [required: >=2,<4, installed: 3.3.2]
│   ├── idna [required: >=2.5,<4, installed: 3.6]
│   └── urllib3 [required: >=1.21.1,<3, installed: 2.2.1]
├── setuptools [required: Any, installed: 63.4.1]
├── six [required: >=1.12.0, installed: 1.16.0]
├── tensorboard [required: >=2.16,<2.17, installed: 2.16.2]
│   ├── absl-py [required: >=0.4, installed: 2.1.0]
│   ├── grpcio [required: >=1.48.2, installed: 1.62.1]
│   ├── Markdown [required: >=2.6.8, installed: 3.6]
│   ├── numpy [required: >=1.12.0, installed: 1.26.4]
│   ├── protobuf [required: >=3.19.6,!=4.24.0, installed: 4.25.3]
│   ├── setuptools [required: >=41.0.0, installed: 63.4.1]
│   ├── six [required: >1.9, installed: 1.16.0]
│   ├── tensorboard-data-server [required: >=0.7.0,<0.8.0, installed: 0.7.2]
│   └── Werkzeug [required: >=1.0.1, installed: 3.0.1]
│       └── MarkupSafe [required: >=2.1.1, installed: 2.1.5]
├── tensorflow-io-gcs-filesystem [required: >=0.23.1, installed: 0.36.0]
├── termcolor [required: >=1.1.0, installed: 2.4.0]
├── typing_extensions [required: >=3.6.6, installed: 4.10.0]
└── wrapt [required: >=1.11.0, installed: 1.16.0]
transformers==4.39.3
├── filelock [required: Any, installed: 3.13.3]
├── huggingface-hub [required: >=0.19.3,<1.0, installed: 0.22.2]
│   ├── filelock [required: Any, installed: 3.13.3]
│   ├── fsspec [required: >=2023.5.0, installed: 2024.2.0]
│   ├── packaging [required: >=20.9, installed: 24.0]
│   ├── PyYAML [required: >=5.1, installed: 6.0.1]
│   ├── requests [required: Any, installed: 2.31.0]
│   │   ├── certifi [required: >=2017.4.17, installed: 2022.9.24]
│   │   ├── charset-normalizer [required: >=2,<4, installed: 3.3.2]
│   │   ├── idna [required: >=2.5,<4, installed: 3.6]
│   │   └── urllib3 [required: >=1.21.1,<3, installed: 2.2.1]
│   ├── tqdm [required: >=4.42.1, installed: 4.66.2]
│   └── typing_extensions [required: >=3.7.4.3, installed: 4.10.0]
├── numpy [required: >=1.17, installed: 1.26.4]
├── packaging [required: >=20.0, installed: 24.0]
├── PyYAML [required: >=5.1, installed: 6.0.1]
├── regex [required: !=2019.12.17, installed: 2023.12.25]
├── requests [required: Any, installed: 2.31.0]
│   ├── certifi [required: >=2017.4.17, installed: 2022.9.24]
│   ├── charset-normalizer [required: >=2,<4, installed: 3.3.2]
│   ├── idna [required: >=2.5,<4, installed: 3.6]
│   └── urllib3 [required: >=1.21.1,<3, installed: 2.2.1]
├── safetensors [required: >=0.4.1, installed: 0.4.2]
├── tokenizers [required: >=0.14,<0.19, installed: 0.15.2]
│   └── huggingface-hub [required: >=0.16.4,<1.0, installed: 0.22.2]
│       ├── filelock [required: Any, installed: 3.13.3]
│       ├── fsspec [required: >=2023.5.0, installed: 2024.2.0]
│       ├── packaging [required: >=20.9, installed: 24.0]
│       ├── PyYAML [required: >=5.1, installed: 6.0.1]
│       ├── requests [required: Any, installed: 2.31.0]
│       │   ├── certifi [required: >=2017.4.17, installed: 2022.9.24]
│       │   ├── charset-normalizer [required: >=2,<4, installed: 3.3.2]
│       │   ├── idna [required: >=2.5,<4, installed: 3.6]
│       │   └── urllib3 [required: >=1.21.1,<3, installed: 2.2.1]
│       ├── tqdm [required: >=4.42.1, installed: 4.66.2]
│       └── typing_extensions [required: >=3.7.4.3, installed: 4.10.0]
└── tqdm [required: >=4.27, installed: 4.66.2]
xgboost==2.0.3
├── numpy [required: Any, installed: 1.26.4]
└── scipy [required: Any, installed: 1.13.0]
    └── numpy [required: >=1.22.4,<2.3, installed: 1.26.4]
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost$
```

## Facing Error

```
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost$ python ./hs-xgboost.py --help
Traceback (most recent call last):
  File "/home/yekyaw.thu/exp/xgboost/./hs-xgboost.py", line 5, in <module>
    from gensim.models import Word2Vec, FastText
  File "/home/yekyaw.thu/.conda/envs/py3.10.6/lib/python3.10/site-packages/gensim/__init__.py", line 11, in <module>
    from gensim import parsing, corpora, matutils, interfaces, models, similarities, utils  # noqa:F401
  File "/home/yekyaw.thu/.conda/envs/py3.10.6/lib/python3.10/site-packages/gensim/corpora/__init__.py", line 6, in <module>
    from .indexedcorpus import IndexedCorpus  # noqa:F401 must appear before the other classes
  File "/home/yekyaw.thu/.conda/envs/py3.10.6/lib/python3.10/site-packages/gensim/corpora/indexedcorpus.py", line 14, in <module>
    from gensim import interfaces, utils
  File "/home/yekyaw.thu/.conda/envs/py3.10.6/lib/python3.10/site-packages/gensim/interfaces.py", line 19, in <module>
    from gensim import utils, matutils
  File "/home/yekyaw.thu/.conda/envs/py3.10.6/lib/python3.10/site-packages/gensim/matutils.py", line 20, in <module>
    from scipy.linalg import get_blas_funcs, triu
ImportError: cannot import name 'triu' from 'scipy.linalg' (/home/yekyaw.thu/.conda/envs/py3.10.6/lib/python3.10/site-packages/scipy/linalg/__init__.py)
(py3.10.6) yekyaw.thu@gpu:~/exp/xgboost$
```

numpy နဲ့ scipy ရဲ့ library နှစ်ခု version conflict ဖြစ်နေလို့ ...  

## Create a New Anaconda Environment

ဒီတစ်ခါတော့ python 3.8 နဲ့ပဲ သွားကြည့်မယ်...  

```
(base) yekyaw.thu@gpu:~/exp/xgboost$ conda create --name xgboost python=3.8 scipy numpy
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 24.3.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/xgboost

  added / updated specs:
    - numpy
    - python=3.8
    - scipy


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    certifi-2024.2.2           |   py38h06a4308_0         159 KB
    libgfortran-ng-11.2.0      |       h00389a5_1          20 KB
    libgfortran5-11.2.0        |       h1234567_1         2.0 MB
    numpy-1.24.3               |   py38hf6e8229_1          10 KB
    packaging-23.2             |   py38h06a4308_0         145 KB
    pooch-1.7.0                |   py38h06a4308_0          81 KB
    requests-2.31.0            |   py38h06a4308_1          96 KB
    scipy-1.10.1               |   py38hf6e8229_1        22.4 MB
    urllib3-2.1.0              |   py38h06a4308_1         156 KB
    ------------------------------------------------------------
                                           Total:        25.1 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-5.1-1_gnu
  blas               pkgs/main/linux-64::blas-1.0-mkl
  brotli-python      pkgs/main/linux-64::brotli-python-1.0.9-py38h6a678d5_7
  ca-certificates    pkgs/main/linux-64::ca-certificates-2024.3.11-h06a4308_0
  certifi            pkgs/main/linux-64::certifi-2024.2.2-py38h06a4308_0
  charset-normalizer pkgs/main/noarch::charset-normalizer-2.0.4-pyhd3eb1b0_0
  idna               pkgs/main/linux-64::idna-3.4-py38h06a4308_0
  intel-openmp       pkgs/main/linux-64::intel-openmp-2023.1.0-hdb19cb5_46306
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.38-h1181459_1
  libffi             pkgs/main/linux-64::libffi-3.4.4-h6a678d5_0
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-11.2.0-h1234567_1
  libgfortran-ng     pkgs/main/linux-64::libgfortran-ng-11.2.0-h00389a5_1
  libgfortran5       pkgs/main/linux-64::libgfortran5-11.2.0-h1234567_1
  libgomp            pkgs/main/linux-64::libgomp-11.2.0-h1234567_1
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-11.2.0-h1234567_1
  mkl                pkgs/main/linux-64::mkl-2023.1.0-h213fc3f_46344
  mkl-service        pkgs/main/linux-64::mkl-service-2.4.0-py38h5eee18b_1
  mkl_fft            pkgs/main/linux-64::mkl_fft-1.3.8-py38h5eee18b_0
  mkl_random         pkgs/main/linux-64::mkl_random-1.2.4-py38hdb19cb5_0
  ncurses            pkgs/main/linux-64::ncurses-6.4-h6a678d5_0
  numpy              pkgs/main/linux-64::numpy-1.24.3-py38hf6e8229_1
  numpy-base         pkgs/main/linux-64::numpy-base-1.24.3-py38h060ed82_1
  openssl            pkgs/main/linux-64::openssl-3.0.13-h7f8727e_0
  packaging          pkgs/main/linux-64::packaging-23.2-py38h06a4308_0
  pip                pkgs/main/linux-64::pip-23.3.1-py38h06a4308_0
  platformdirs       pkgs/main/linux-64::platformdirs-3.10.0-py38h06a4308_0
  pooch              pkgs/main/linux-64::pooch-1.7.0-py38h06a4308_0
  pysocks            pkgs/main/linux-64::pysocks-1.7.1-py38h06a4308_0
  python             pkgs/main/linux-64::python-3.8.19-h955ad1f_0
  readline           pkgs/main/linux-64::readline-8.2-h5eee18b_0
  requests           pkgs/main/linux-64::requests-2.31.0-py38h06a4308_1
  scipy              pkgs/main/linux-64::scipy-1.10.1-py38hf6e8229_1
  setuptools         pkgs/main/linux-64::setuptools-68.2.2-py38h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.41.2-h5eee18b_0
  tbb                pkgs/main/linux-64::tbb-2021.8.0-hdb19cb5_0
  tk                 pkgs/main/linux-64::tk-8.6.12-h1ccaba5_0
  urllib3            pkgs/main/linux-64::urllib3-2.1.0-py38h06a4308_1
  wheel              pkgs/main/linux-64::wheel-0.41.2-py38h06a4308_0
  xz                 pkgs/main/linux-64::xz-5.4.6-h5eee18b_0
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
numpy-1.24.3         | 10 KB     | ####################################### | 100%
pooch-1.7.0          | 81 KB     | ####################################### | 100%
requests-2.31.0      | 96 KB     | ####################################### | 100%
libgfortran-ng-11.2. | 20 KB     | ####################################### | 100%
libgfortran5-11.2.0  | 2.0 MB    | ####################################### | 100%
packaging-23.2       | 145 KB    | ####################################### | 100%
urllib3-2.1.0        | 156 KB    | ####################################### | 100%
scipy-1.10.1         | 22.4 MB   | ####################################### | 100%
certifi-2024.2.2     | 159 KB    | ####################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate xgboost
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) yekyaw.thu@gpu:~/exp/xgboost$
```

```
(base) yekyaw.thu@gpu:~/exp/xgboost$ conda activate xgboost
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

xgboost ကို install လုပ်ခဲ့ ...  

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ conda install -c conda-forge py-xgboost-gpu
Collecting package metadata (current_repodata.json): done
Solving environment: -
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::pysocks==1.7.1=py38h06a4308_0
  - defaults/linux-64::pip==23.3.1=py38h06a4308_0
  - defaults/linux-64::idna==3.4=py38h06a4308_0
  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::brotli-python==1.0.9=py38h6a678d5_7
  - defaults/linux-64::setuptools==68.2.2=py38h06a4308_0
  - defaults/linux-64::urllib3==2.1.0=py38h06a4308_1
  - defaults/linux-64::mkl_fft==1.3.8=py38h5eee18b_0
  - defaults/linux-64::scipy==1.10.1=py38hf6e8229_1
  - defaults/linux-64::xz==5.4.6=h5eee18b_0
  - defaults/linux-64::tbb==2021.8.0=hdb19cb5_0
  - defaults/linux-64::mkl_random==1.2.4=py38hdb19cb5_0
  - defaults/linux-64::numpy==1.24.3=py38hf6e8229_1
  - defaults/linux-64::ncurses==6.4=h6a678d5_0
  - defaults/linux-64::packaging==23.2=py38h06a4308_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::openssl==3.0.13=h7f8727e_0
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::libgfortran-ng==11.2.0=h00389a5_1
  - defaults/linux-64::intel-openmp==2023.1.0=hdb19cb5_46306
  - defaults/linux-64::wheel==0.41.2=py38h06a4308_0
  - defaults/linux-64::pooch==1.7.0=py38h06a4308_0
  - defaults/noarch::charset-normalizer==2.0.4=pyhd3eb1b0_0
  - defaults/linux-64::mkl-service==2.4.0=py38h5eee18b_1
  - defaults/linux-64::libffi==3.4.4=h6a678d5_0
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::platformdirs==3.10.0=py38h06a4308_0
  - defaults/linux-64::mkl==2023.1.0=h213fc3f_46344
  - defaults/linux-64::numpy-base==1.24.3=py38h060ed82_1
  - defaults/linux-64::certifi==2024.2.2=py38h06a4308_0
  - defaults/linux-64::requests==2.31.0=py38h06a4308_1
  - defaults/linux-64::sqlite==3.41.2=h5eee18b_0
  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
  - defaults/linux-64::python==3.8.19=h955ad1f_0
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 24.3.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/xgboost

  added / updated specs:
    - py-xgboost-gpu


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    _openmp_mutex-4.5          |       2_kmp_llvm           6 KB  conda-forge
    python_abi-3.8             |           2_cp38           4 KB  conda-forge
    scikit-learn-1.3.2         |   py38ha25d942_2         8.0 MB  conda-forge
    ------------------------------------------------------------
                                           Total:         8.1 MB

The following NEW packages will be INSTALLED:

  _py-xgboost-mutex  conda-forge/linux-64::_py-xgboost-mutex-2.0-gpu_0
  joblib             conda-forge/noarch::joblib-1.3.2-pyhd8ed1ab_0
  libxgboost         conda-forge/linux-64::libxgboost-2.0.3-cpu_hce603c2_3
  llvm-openmp        pkgs/main/linux-64::llvm-openmp-14.0.6-h9e868ea_0
  py-xgboost         conda-forge/noarch::py-xgboost-2.0.3-cuda118_pyh103b7b7_3
  py-xgboost-gpu     conda-forge/noarch::py-xgboost-gpu-2.0.3-pyh7984362_3
  python_abi         conda-forge/linux-64::python_abi-3.8-2_cp38
  scikit-learn       conda-forge/linux-64::scikit-learn-1.3.2-py38ha25d942_2
  threadpoolctl      conda-forge/noarch::threadpoolctl-3.4.0-pyhc1e730c_0

The following packages will be REMOVED:

  libgomp-11.2.0-h1234567_1

The following packages will be UPDATED:

  libgcc-ng          pkgs/main::libgcc-ng-11.2.0-h1234567_1 --> conda-forge::libgcc-ng-13.2.0-h807b86a_5
  libstdcxx-ng       pkgs/main::libstdcxx-ng-11.2.0-h12345~ --> conda-forge::libstdcxx-ng-13.2.0-h7e041cc_5

The following packages will be SUPERSEDED by a higher-priority channel:

  _libgcc_mutex           pkgs/main::_libgcc_mutex-0.1-main --> conda-forge::_libgcc_mutex-0.1-conda_forge
  _openmp_mutex          pkgs/main::_openmp_mutex-5.1-1_gnu --> conda-forge::_openmp_mutex-4.5-2_kmp_llvm
  ca-certificates    pkgs/main::ca-certificates-2024.3.11-~ --> conda-forge::ca-certificates-2024.2.2-hbcca054_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
python_abi-3.8       | 4 KB      | ####################################### | 100%
_openmp_mutex-4.5    | 6 KB      | ####################################### | 100%
scikit-learn-1.3.2   | 8.0 MB    | ####################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

gensim ကို install လုပ်ခဲ့...  

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ pip install gensim
Collecting gensim
  Downloading gensim-4.3.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (8.5 kB)
Requirement already satisfied: numpy>=1.18.5 in /home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages (from gensim) (1.24.3)
Requirement already satisfied: scipy>=1.7.0 in /home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages (from gensim) (1.10.1)
Collecting smart-open>=1.8.1 (from gensim)
  Downloading smart_open-7.0.4-py3-none-any.whl.metadata (23 kB)
Requirement already satisfied: wrapt in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from smart-open>=1.8.1->gensim) (1.14.1)
Downloading gensim-4.3.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (26.6 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 26.6/26.6 MB 17.1 MB/s eta 0:00:00
Downloading smart_open-7.0.4-py3-none-any.whl (61 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 61.2/61.2 kB 782.7 kB/s eta 0:00:00
Installing collected packages: smart-open, gensim
Successfully installed gensim-4.3.2 smart-open-7.0.4
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

## Data Preparation

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ cp -r ../hs-fasttext/long-data/ .
```

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ cp -r ../hs-fasttext/short-data/ .
```

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ tree ./long-data/
./long-data/
├── ltest.txt
└── ltrain.txt

0 directories, 2 files
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ tree ./short-data/
./short-data/
├── stest.txt
└── strain.txt

0 directories, 2 files
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

data size information:  

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ wc ./long-data/{ltrain,ltest}.txt
   9137  163390 2068583 ./long-data/ltrain.txt
   1000   17880  223453 ./long-data/ltest.txt
  10137  181270 2292036 total
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ wc ./short-data/{strain,stest}.txt
  9137  61854 901839 ./short-data/strain.txt
  1000   6725  96170 ./short-data/stest.txt
 10137  68579 998009 total
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

## Python Code Updating and Training for Long Hate Speech

ဒီအဆင့်မှာ coding လုပ်လိုက် run လိုက်ကို ၃နာရီခန့် လုပ်ခဲ့တယ်။  

```python
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ cat hs-xgboost.py
"""
for hate speech classification with XGBoost
Written by Ye Kyaw Thu, LU Lab., Myanmar.
Last updated: 7 April 2024
Usage:
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ python ./hs-xgboost.py --help
"""

import argparse
import numpy as np
import xgboost as xgb
from sklearn.feature_extraction.text import TfidfVectorizer
from gensim.models import Word2Vec, FastText
from sklearn.metrics import f1_score, precision_score, recall_score, log_loss, accuracy_score

# Function to load Burmese text data
def load_data(file_path):
    texts = []
    labels = []
    label_map = {}  # Dictionary to map text labels to integers
    with open(file_path, 'r', encoding='utf-8') as file:
        for line in file:
            parts = line.strip().split(' ', 1)
            label = parts[0]
            text = parts[1]
            texts.append(text)
            # Extract label from the first column
            label = label.split('__label__')[-1].strip()  # Extracting label after '__label__'
            if label == "":
                label = "BLANK"  # Assigning a special label for blanks
            if label not in label_map:
                label_map[label] = len(label_map)  # Assign a unique integer to each label
            labels.append(label_map[label])  # Append the integer label
    return texts, labels, label_map

# Function to load stop words from file
def load_stopwords(file_path):
    with open(file_path, 'r', encoding='utf-8') as file:
        stopwords = file.read().splitlines()
    return stopwords

# Function to calculate text features
def calculate_features(train_texts, test_texts, feature_type, stopwords=None):
    if feature_type == 'tfidf':
        vectorizer = TfidfVectorizer(stop_words=stopwords)
        train_features = vectorizer.fit_transform(train_texts)
        test_features = vectorizer.transform(test_texts)
    elif feature_type == 'word2vec':
        word2vec_model = Word2Vec(sentences=[text.split() for text in train_texts], vector_size=100, window=5, min_count=1, workers=4)
        train_features = np.array([np.mean([word2vec_model.wv[word] for word in text.split() if word in word2vec_model.wv] or [np.zeros(100)], axis=0) for text in train_texts])
        test_features = np.array([np.mean([word2vec_model.wv[word] for word in text.split() if word in word2vec_model.wv] or [np.zeros(100)], axis=0) for text in test_texts])
    elif feature_type == 'fasttext':
        fasttext_model = FastText(sentences=[text.split() for text in train_texts], vector_size=100, window=5, min_count=1, workers=4)
        train_features = np.array([np.mean([fasttext_model.wv[word] for word in text.split() if word in fasttext_model.wv] or [np.zeros(100)], axis=0) for text in train_texts])
        test_features = np.array([np.mean([fasttext_model.wv[word] for word in text.split() if word in fasttext_model.wv] or [np.zeros(100)], axis=0) for text in test_texts])
    else:
        raise ValueError("Invalid feature type. Choose from 'tfidf', 'word2vec', or 'fasttext'.")
    return train_features, test_features

def main(args):
    # Load data
    train_texts, train_labels, label_map = load_data(args.train_file)
    test_texts, test_labels, _ = load_data(args.test_file)

    # Load stop words if provided
    stopwords = None
    if args.stopword_file:
        stopwords = load_stopwords(args.stopword_file)

    # Calculate features
    train_features, test_features = calculate_features(train_texts, test_texts, args.feature, stopwords)

    # Train XGBoost model
    xg_train = xgb.DMatrix(train_features, label=train_labels)
    xg_test = xgb.DMatrix(test_features, label=test_labels)

    # Setup parameters for XGBoost
    param = {'objective': 'multi:softmax', 'eta': args.learning_rate, 'max_depth': args.max_depth, 'nthread': 4, 'num_class': len(label_map)}
    # Define the watchlist with the train and test sets
    watchlist = [(xg_train, 'train'), (xg_test, 'test')]
    num_round = args.num_round

    # Train XGBoost model
    bst = xgb.train(param, xg_train, num_round, watchlist)

    # Get predictions
    pred_prob = bst.predict(xg_test, output_margin=True)
    pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)

    # Get predicted numeric labels
    pred_numeric_labels = pred_prob.argmax(axis=1)

    # Evaluate model based on specified metric
    if args.eval == 'f1':
        # Convert numeric labels to text labels for F1 calculation
        pred_text_labels = [list(label_map.keys())[label] for label in pred_numeric_labels]
        f1 = f1_score([list(label_map.keys())[label] for label in test_labels], pred_text_labels, average='weighted')
        precision = precision_score([list(label_map.keys())[label] for label in test_labels], pred_text_labels, average='weighted', zero_division=1)
        recall = recall_score([list(label_map.keys())[label] for label in test_labels], pred_text_labels, average='weighted')
        print(f"F1 Score: {f1}")
        print(f"Precision: {precision}")
        print(f"Recall: {recall}")
    elif args.eval == 'logloss':
        metric_score = log_loss(test_labels, pred_prob)
        print(f"Log Loss: {metric_score}")
    elif args.eval == 'error':
        # Calculate error rate directly from numeric labels
        metric_score = 1.0 - accuracy_score(test_labels, pred_numeric_labels)
        print(f"Error Rate: {metric_score}")
    else:
        raise ValueError("Invalid evaluation metric. Choose from 'f1', 'logloss', or 'error'.")

    # Print numeric labels and original label text for better understanding
    print("\nNumeric Label - Original Label")
    for numeric_label, text_label in label_map.items():
        print(f"{numeric_label} - {text_label}")


if __name__ == "__main__":
    parser = argparse.ArgumentParser(description='Hate Speech Classification with XGBoost')
    parser.add_argument('--train_file', type=str, help='Path to training data file', required=True)
    parser.add_argument('--test_file', type=str, help='Path to testing data file', required=True)
    parser.add_argument('--feature', type=str, help='Text feature type: tfidf, word2vec, or fasttext', choices=['tfidf', 'word2vec', 'fasttext'], required=True)
    parser.add_argument('--stopword_file', type=str, help='Path to stopword file (optional)', default=None)
    parser.add_argument('--learning_rate', type=float, help='Learning rate (eta)', default=0.1)
    parser.add_argument('--max_depth', type=int, help='Maximum depth of a tree', default=6)
    parser.add_argument('--num_round', type=int, help='Number of boosting rounds', default=5)
    parser.add_argument('--eval', type=str, help='Evaluation metric: f1, logloss, or error', choices=['f1', 'logloss', 'error'], default='f1')
    args = parser.parse_args()
    main(args)

```

called --help  

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ python ./hs-xgboost.py --help
usage: hs-xgboost.py [-h] --train_file TRAIN_FILE --test_file TEST_FILE
                     --feature {tfidf,word2vec,fasttext}
                     [--stopword_file STOPWORD_FILE]
                     [--learning_rate LEARNING_RATE] [--max_depth MAX_DEPTH]
                     [--num_round NUM_ROUND] [--eval {f1,logloss,error}]

Hate Speech Classification with XGBoost

optional arguments:
  -h, --help            show this help message and exit
  --train_file TRAIN_FILE
                        Path to training data file
  --test_file TEST_FILE
                        Path to testing data file
  --feature {tfidf,word2vec,fasttext}
                        Text feature type: tfidf, word2vec, or fasttext
  --stopword_file STOPWORD_FILE
                        Path to stopword file (optional)
  --learning_rate LEARNING_RATE
                        Learning rate (eta)
  --max_depth MAX_DEPTH
                        Maximum depth of a tree
  --num_round NUM_ROUND
                        Number of boosting rounds
  --eval {f1,logloss,error}
                        Evaluation metric: f1, logloss, or error
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

နောက်ဆုံး error မရှိတော့ပဲ run လို့ရတဲ့ အခြေအနေမို့လို့ အောက်ပါအတိုင်း shell script ရေးပြီး long hate speech အတွက် experiment လုပ်ခဲ့တယ်။  

```bash
$ cat run.sh
#!/bin/bash

## Written by Ye Kyaw Thu, LU Lab., Myanmar
## Last updated: 7 April 2024

set -x;

## Evaluation with F1, P and R
time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature tfidf --num_round 30 \
--eval f1 | tee tfidf-f1.log

time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature word2vec --num_round 30 \
--eval f1 | tee w2v-f1.log

time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature fasttext --num_round 30 \
--eval f1 | tee fasttext-f1.log

## Evaluation with Logloss
time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature tfidf --num_round 30 \
--eval logloss | tee tfidf-logloss.log

time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature word2vec --num_round 30 \
--eval logloss | tee w2v-logloss.log

time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature fasttext --num_round 30 \
--eval logloss | tee fasttext-logloss.log

## Evaluation with Error
time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature tfidf --num_round 30 \
--eval error | tee tfidf-error.log

time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature word2vec --num_round 30 \
--eval error | tee w2v-error.log

time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature fasttext --num_round 30 \
--eval error | tee fasttext-error.log

set +x;
```

long hate speech အတွက် experiment result က အောက်ပါအတိုင်း ...  

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ ./run.sh
+ tee tfidf-f1.log
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --num_round 30 --eval f1
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.12946  test-mlogloss:2.17367
[1]     train-mlogloss:2.00021  test-mlogloss:2.08073
[2]     train-mlogloss:1.89729  test-mlogloss:2.01104
[3]     train-mlogloss:1.81263  test-mlogloss:1.95663
[4]     train-mlogloss:1.74133  test-mlogloss:1.91332
[5]     train-mlogloss:1.67966  test-mlogloss:1.87827
[6]     train-mlogloss:1.62641  test-mlogloss:1.85027
[7]     train-mlogloss:1.57942  test-mlogloss:1.82738
[8]     train-mlogloss:1.53793  test-mlogloss:1.80942
[9]     train-mlogloss:1.50116  test-mlogloss:1.79569
[10]    train-mlogloss:1.46858  test-mlogloss:1.78427
[11]    train-mlogloss:1.43915  test-mlogloss:1.77627
[12]    train-mlogloss:1.41194  test-mlogloss:1.77003
[13]    train-mlogloss:1.38762  test-mlogloss:1.76530
[14]    train-mlogloss:1.36513  test-mlogloss:1.76214
[15]    train-mlogloss:1.34535  test-mlogloss:1.76112
[16]    train-mlogloss:1.32705  test-mlogloss:1.76216
[17]    train-mlogloss:1.31008  test-mlogloss:1.76183
[18]    train-mlogloss:1.29418  test-mlogloss:1.76298
[19]    train-mlogloss:1.27949  test-mlogloss:1.76546
[20]    train-mlogloss:1.26622  test-mlogloss:1.76898
[21]    train-mlogloss:1.25395  test-mlogloss:1.77262
[22]    train-mlogloss:1.24196  test-mlogloss:1.77582
[23]    train-mlogloss:1.23125  test-mlogloss:1.78056
[24]    train-mlogloss:1.22111  test-mlogloss:1.78612
[25]    train-mlogloss:1.21133  test-mlogloss:1.79167
[26]    train-mlogloss:1.20282  test-mlogloss:1.79742
[27]    train-mlogloss:1.19390  test-mlogloss:1.80367
[28]    train-mlogloss:1.18614  test-mlogloss:1.80941
[29]    train-mlogloss:1.17850  test-mlogloss:1.81558
F1 Score: 0.4007500339443313
Precision: 0.3413717532467533
Recall: 0.534

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.289s
user    0m12.739s
sys     0m0.611s
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --num_round 30 --eval f1
+ tee w2v-f1.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.13041  test-mlogloss:2.17574
[1]     train-mlogloss:1.99837  test-mlogloss:2.08587
[2]     train-mlogloss:1.89066  test-mlogloss:2.01763
[3]     train-mlogloss:1.80154  test-mlogloss:1.96496
[4]     train-mlogloss:1.72546  test-mlogloss:1.92096
[5]     train-mlogloss:1.65894  test-mlogloss:1.88587
[6]     train-mlogloss:1.60067  test-mlogloss:1.85699
[7]     train-mlogloss:1.54849  test-mlogloss:1.83429
[8]     train-mlogloss:1.50075  test-mlogloss:1.81669
[9]     train-mlogloss:1.45806  test-mlogloss:1.80165
[10]    train-mlogloss:1.41988  test-mlogloss:1.78937
[11]    train-mlogloss:1.38433  test-mlogloss:1.78055
[12]    train-mlogloss:1.35227  test-mlogloss:1.77462
[13]    train-mlogloss:1.32214  test-mlogloss:1.76998
[14]    train-mlogloss:1.29528  test-mlogloss:1.76825
[15]    train-mlogloss:1.26960  test-mlogloss:1.76694
[16]    train-mlogloss:1.24553  test-mlogloss:1.76748
[17]    train-mlogloss:1.22358  test-mlogloss:1.76793
[18]    train-mlogloss:1.20311  test-mlogloss:1.76933
[19]    train-mlogloss:1.18375  test-mlogloss:1.77236
[20]    train-mlogloss:1.16585  test-mlogloss:1.77640
[21]    train-mlogloss:1.14763  test-mlogloss:1.78077
[22]    train-mlogloss:1.13081  test-mlogloss:1.78629
[23]    train-mlogloss:1.11486  test-mlogloss:1.79060
[24]    train-mlogloss:1.10011  test-mlogloss:1.79723
[25]    train-mlogloss:1.08507  test-mlogloss:1.80392
[26]    train-mlogloss:1.07165  test-mlogloss:1.81034
[27]    train-mlogloss:1.05853  test-mlogloss:1.81711
[28]    train-mlogloss:1.04615  test-mlogloss:1.82459
[29]    train-mlogloss:1.03481  test-mlogloss:1.83215
F1 Score: 0.3919937144088405
Precision: 0.6589524068041984
Recall: 0.523

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m3.549s
user    0m15.885s
sys     0m0.579s
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --num_round 30 --eval f1
+ tee fasttext-f1.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.13170  test-mlogloss:2.17422
[1]     train-mlogloss:2.00202  test-mlogloss:2.08113
[2]     train-mlogloss:1.89724  test-mlogloss:2.01159
[3]     train-mlogloss:1.81005  test-mlogloss:1.95655
[4]     train-mlogloss:1.73368  test-mlogloss:1.91155
[5]     train-mlogloss:1.66795  test-mlogloss:1.87540
[6]     train-mlogloss:1.60962  test-mlogloss:1.84631
[7]     train-mlogloss:1.55837  test-mlogloss:1.82284
[8]     train-mlogloss:1.51200  test-mlogloss:1.80290
[9]     train-mlogloss:1.47031  test-mlogloss:1.78789
[10]    train-mlogloss:1.43230  test-mlogloss:1.77547
[11]    train-mlogloss:1.39710  test-mlogloss:1.76513
[12]    train-mlogloss:1.36522  test-mlogloss:1.75792
[13]    train-mlogloss:1.33650  test-mlogloss:1.75266
[14]    train-mlogloss:1.30913  test-mlogloss:1.74946
[15]    train-mlogloss:1.28439  test-mlogloss:1.74741
[16]    train-mlogloss:1.26120  test-mlogloss:1.74672
[17]    train-mlogloss:1.23967  test-mlogloss:1.74629
[18]    train-mlogloss:1.21883  test-mlogloss:1.74811
[19]    train-mlogloss:1.20063  test-mlogloss:1.74925
[20]    train-mlogloss:1.18311  test-mlogloss:1.75159
[21]    train-mlogloss:1.16680  test-mlogloss:1.75474
[22]    train-mlogloss:1.15163  test-mlogloss:1.75745
[23]    train-mlogloss:1.13596  test-mlogloss:1.76077
[24]    train-mlogloss:1.12015  test-mlogloss:1.76522
[25]    train-mlogloss:1.10610  test-mlogloss:1.76941
[26]    train-mlogloss:1.09272  test-mlogloss:1.77413
[27]    train-mlogloss:1.07939  test-mlogloss:1.77953
[28]    train-mlogloss:1.06675  test-mlogloss:1.78538
[29]    train-mlogloss:1.05498  test-mlogloss:1.79161
F1 Score: 0.39730772499274547
Precision: 0.6373269975360788
Recall: 0.537

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m6.106s
user    0m20.472s
sys     0m0.599s
+ tee tfidf-logloss.log
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --num_round 30 --eval logloss
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.12946  test-mlogloss:2.17367
[1]     train-mlogloss:2.00021  test-mlogloss:2.08073
[2]     train-mlogloss:1.89729  test-mlogloss:2.01104
[3]     train-mlogloss:1.81263  test-mlogloss:1.95663
[4]     train-mlogloss:1.74133  test-mlogloss:1.91332
[5]     train-mlogloss:1.67966  test-mlogloss:1.87827
[6]     train-mlogloss:1.62641  test-mlogloss:1.85027
[7]     train-mlogloss:1.57942  test-mlogloss:1.82738
[8]     train-mlogloss:1.53793  test-mlogloss:1.80942
[9]     train-mlogloss:1.50116  test-mlogloss:1.79569
[10]    train-mlogloss:1.46858  test-mlogloss:1.78427
[11]    train-mlogloss:1.43915  test-mlogloss:1.77627
[12]    train-mlogloss:1.41194  test-mlogloss:1.77003
[13]    train-mlogloss:1.38762  test-mlogloss:1.76530
[14]    train-mlogloss:1.36513  test-mlogloss:1.76214
[15]    train-mlogloss:1.34535  test-mlogloss:1.76112
[16]    train-mlogloss:1.32705  test-mlogloss:1.76216
[17]    train-mlogloss:1.31008  test-mlogloss:1.76183
[18]    train-mlogloss:1.29418  test-mlogloss:1.76298
[19]    train-mlogloss:1.27949  test-mlogloss:1.76546
[20]    train-mlogloss:1.26622  test-mlogloss:1.76898
[21]    train-mlogloss:1.25395  test-mlogloss:1.77262
[22]    train-mlogloss:1.24196  test-mlogloss:1.77582
[23]    train-mlogloss:1.23125  test-mlogloss:1.78056
[24]    train-mlogloss:1.22111  test-mlogloss:1.78612
[25]    train-mlogloss:1.21133  test-mlogloss:1.79167
[26]    train-mlogloss:1.20282  test-mlogloss:1.79742
[27]    train-mlogloss:1.19390  test-mlogloss:1.80367
[28]    train-mlogloss:1.18614  test-mlogloss:1.80941
[29]    train-mlogloss:1.17850  test-mlogloss:1.81558
Log Loss: 1.8155840702084347

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.272s
user    0m12.310s
sys     0m0.533s
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --num_round 30 --eval logloss
+ tee w2v-logloss.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.13182  test-mlogloss:2.17732
[1]     train-mlogloss:2.00201  test-mlogloss:2.08835
[2]     train-mlogloss:1.89588  test-mlogloss:2.02107
[3]     train-mlogloss:1.80751  test-mlogloss:1.96648
[4]     train-mlogloss:1.73168  test-mlogloss:1.92440
[5]     train-mlogloss:1.66651  test-mlogloss:1.88922
[6]     train-mlogloss:1.60871  test-mlogloss:1.86069
[7]     train-mlogloss:1.55775  test-mlogloss:1.83994
[8]     train-mlogloss:1.51086  test-mlogloss:1.82222
[9]     train-mlogloss:1.47050  test-mlogloss:1.80745
[10]    train-mlogloss:1.43169  test-mlogloss:1.79673
[11]    train-mlogloss:1.39830  test-mlogloss:1.78788
[12]    train-mlogloss:1.36652  test-mlogloss:1.78151
[13]    train-mlogloss:1.33787  test-mlogloss:1.77722
[14]    train-mlogloss:1.31136  test-mlogloss:1.77398
[15]    train-mlogloss:1.28704  test-mlogloss:1.77100
[16]    train-mlogloss:1.26364  test-mlogloss:1.77053
[17]    train-mlogloss:1.24179  test-mlogloss:1.77007
[18]    train-mlogloss:1.22188  test-mlogloss:1.77136
[19]    train-mlogloss:1.20334  test-mlogloss:1.77359
[20]    train-mlogloss:1.18516  test-mlogloss:1.77652
[21]    train-mlogloss:1.16783  test-mlogloss:1.78192
[22]    train-mlogloss:1.15125  test-mlogloss:1.78591
[23]    train-mlogloss:1.13620  test-mlogloss:1.79108
[24]    train-mlogloss:1.12115  test-mlogloss:1.79685
[25]    train-mlogloss:1.10569  test-mlogloss:1.80428
[26]    train-mlogloss:1.09151  test-mlogloss:1.81132
[27]    train-mlogloss:1.07738  test-mlogloss:1.81730
[28]    train-mlogloss:1.06566  test-mlogloss:1.82430
[29]    train-mlogloss:1.05409  test-mlogloss:1.83161
Log Loss: 1.8316119095111993

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m3.592s
user    0m16.030s
sys     0m0.568s
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --num_round 30 --eval logloss
+ tee fasttext-logloss.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.13100  test-mlogloss:2.17601
[1]     train-mlogloss:2.00063  test-mlogloss:2.08446
[2]     train-mlogloss:1.89604  test-mlogloss:2.01446
[3]     train-mlogloss:1.80839  test-mlogloss:1.96028
[4]     train-mlogloss:1.73288  test-mlogloss:1.91668
[5]     train-mlogloss:1.66756  test-mlogloss:1.88075
[6]     train-mlogloss:1.60909  test-mlogloss:1.85217
[7]     train-mlogloss:1.55769  test-mlogloss:1.82867
[8]     train-mlogloss:1.51200  test-mlogloss:1.80987
[9]     train-mlogloss:1.46978  test-mlogloss:1.79513
[10]    train-mlogloss:1.43233  test-mlogloss:1.78330
[11]    train-mlogloss:1.39772  test-mlogloss:1.77328
[12]    train-mlogloss:1.36583  test-mlogloss:1.76508
[13]    train-mlogloss:1.33730  test-mlogloss:1.76019
[14]    train-mlogloss:1.31084  test-mlogloss:1.75693
[15]    train-mlogloss:1.28602  test-mlogloss:1.75533
[16]    train-mlogloss:1.26399  test-mlogloss:1.75420
[17]    train-mlogloss:1.24201  test-mlogloss:1.75482
[18]    train-mlogloss:1.22263  test-mlogloss:1.75640
[19]    train-mlogloss:1.20348  test-mlogloss:1.75855
[20]    train-mlogloss:1.18514  test-mlogloss:1.76207
[21]    train-mlogloss:1.16852  test-mlogloss:1.76523
[22]    train-mlogloss:1.15294  test-mlogloss:1.76945
[23]    train-mlogloss:1.13710  test-mlogloss:1.77349
[24]    train-mlogloss:1.12289  test-mlogloss:1.77808
[25]    train-mlogloss:1.10832  test-mlogloss:1.78309
[26]    train-mlogloss:1.09428  test-mlogloss:1.78809
[27]    train-mlogloss:1.08190  test-mlogloss:1.79441
[28]    train-mlogloss:1.07000  test-mlogloss:1.80084
[29]    train-mlogloss:1.05834  test-mlogloss:1.80638
Log Loss: 1.806377589567781

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m6.279s
user    0m20.845s
sys     0m0.608s
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --num_round 30 --eval error
+ tee tfidf-error.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.12946  test-mlogloss:2.17367
[1]     train-mlogloss:2.00021  test-mlogloss:2.08073
[2]     train-mlogloss:1.89729  test-mlogloss:2.01104
[3]     train-mlogloss:1.81263  test-mlogloss:1.95663
[4]     train-mlogloss:1.74133  test-mlogloss:1.91332
[5]     train-mlogloss:1.67966  test-mlogloss:1.87827
[6]     train-mlogloss:1.62641  test-mlogloss:1.85027
[7]     train-mlogloss:1.57942  test-mlogloss:1.82738
[8]     train-mlogloss:1.53793  test-mlogloss:1.80942
[9]     train-mlogloss:1.50116  test-mlogloss:1.79569
[10]    train-mlogloss:1.46858  test-mlogloss:1.78427
[11]    train-mlogloss:1.43915  test-mlogloss:1.77627
[12]    train-mlogloss:1.41194  test-mlogloss:1.77003
[13]    train-mlogloss:1.38762  test-mlogloss:1.76530
[14]    train-mlogloss:1.36513  test-mlogloss:1.76214
[15]    train-mlogloss:1.34535  test-mlogloss:1.76112
[16]    train-mlogloss:1.32705  test-mlogloss:1.76216
[17]    train-mlogloss:1.31008  test-mlogloss:1.76183
[18]    train-mlogloss:1.29418  test-mlogloss:1.76298
[19]    train-mlogloss:1.27949  test-mlogloss:1.76546
[20]    train-mlogloss:1.26622  test-mlogloss:1.76898
[21]    train-mlogloss:1.25395  test-mlogloss:1.77262
[22]    train-mlogloss:1.24196  test-mlogloss:1.77582
[23]    train-mlogloss:1.23125  test-mlogloss:1.78056
[24]    train-mlogloss:1.22111  test-mlogloss:1.78612
[25]    train-mlogloss:1.21133  test-mlogloss:1.79167
[26]    train-mlogloss:1.20282  test-mlogloss:1.79742
[27]    train-mlogloss:1.19390  test-mlogloss:1.80367
[28]    train-mlogloss:1.18614  test-mlogloss:1.80941
[29]    train-mlogloss:1.17850  test-mlogloss:1.81558
Error Rate: 0.46599999999999997

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.346s
user    0m13.247s
sys     0m0.507s
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --num_round 30 --eval error
+ tee w2v-error.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.13212  test-mlogloss:2.17986
[1]     train-mlogloss:2.00223  test-mlogloss:2.08857
[2]     train-mlogloss:1.89650  test-mlogloss:2.01996
[3]     train-mlogloss:1.80751  test-mlogloss:1.96752
[4]     train-mlogloss:1.73125  test-mlogloss:1.92425
[5]     train-mlogloss:1.66500  test-mlogloss:1.88991
[6]     train-mlogloss:1.60603  test-mlogloss:1.86119
[7]     train-mlogloss:1.55420  test-mlogloss:1.83799
[8]     train-mlogloss:1.50697  test-mlogloss:1.81972
[9]     train-mlogloss:1.46490  test-mlogloss:1.80619
[10]    train-mlogloss:1.42639  test-mlogloss:1.79468
[11]    train-mlogloss:1.39106  test-mlogloss:1.78587
[12]    train-mlogloss:1.35919  test-mlogloss:1.77860
[13]    train-mlogloss:1.32972  test-mlogloss:1.77378
[14]    train-mlogloss:1.30293  test-mlogloss:1.77100
[15]    train-mlogloss:1.27728  test-mlogloss:1.77019
[16]    train-mlogloss:1.25455  test-mlogloss:1.77004
[17]    train-mlogloss:1.23273  test-mlogloss:1.77188
[18]    train-mlogloss:1.21227  test-mlogloss:1.77476
[19]    train-mlogloss:1.19239  test-mlogloss:1.77665
[20]    train-mlogloss:1.17438  test-mlogloss:1.78157
[21]    train-mlogloss:1.15717  test-mlogloss:1.78589
[22]    train-mlogloss:1.14064  test-mlogloss:1.79171
[23]    train-mlogloss:1.12525  test-mlogloss:1.79745
[24]    train-mlogloss:1.11039  test-mlogloss:1.80318
[25]    train-mlogloss:1.09604  test-mlogloss:1.80930
[26]    train-mlogloss:1.08345  test-mlogloss:1.81588
[27]    train-mlogloss:1.07012  test-mlogloss:1.82306
[28]    train-mlogloss:1.05670  test-mlogloss:1.83059
[29]    train-mlogloss:1.04504  test-mlogloss:1.83874
Error Rate: 0.477

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m3.545s
user    0m15.694s
sys     0m0.571s
+ tee fasttext-error.log
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --num_round 30 --eval error
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.13152  test-mlogloss:2.17326
[1]     train-mlogloss:2.00141  test-mlogloss:2.08181
[2]     train-mlogloss:1.89651  test-mlogloss:2.01250
[3]     train-mlogloss:1.80897  test-mlogloss:1.95855
[4]     train-mlogloss:1.73359  test-mlogloss:1.91421
[5]     train-mlogloss:1.66812  test-mlogloss:1.87783
[6]     train-mlogloss:1.61008  test-mlogloss:1.84793
[7]     train-mlogloss:1.55928  test-mlogloss:1.82411
[8]     train-mlogloss:1.51317  test-mlogloss:1.80432
[9]     train-mlogloss:1.47160  test-mlogloss:1.78814
[10]    train-mlogloss:1.43449  test-mlogloss:1.77505
[11]    train-mlogloss:1.40073  test-mlogloss:1.76435
[12]    train-mlogloss:1.36933  test-mlogloss:1.75767
[13]    train-mlogloss:1.34006  test-mlogloss:1.75231
[14]    train-mlogloss:1.31373  test-mlogloss:1.74844
[15]    train-mlogloss:1.28880  test-mlogloss:1.74607
[16]    train-mlogloss:1.26570  test-mlogloss:1.74477
[17]    train-mlogloss:1.24442  test-mlogloss:1.74423
[18]    train-mlogloss:1.22432  test-mlogloss:1.74584
[19]    train-mlogloss:1.20492  test-mlogloss:1.74731
[20]    train-mlogloss:1.18658  test-mlogloss:1.74963
[21]    train-mlogloss:1.16888  test-mlogloss:1.75338
[22]    train-mlogloss:1.15140  test-mlogloss:1.75764
[23]    train-mlogloss:1.13520  test-mlogloss:1.76157
[24]    train-mlogloss:1.11930  test-mlogloss:1.76650
[25]    train-mlogloss:1.10570  test-mlogloss:1.77107
[26]    train-mlogloss:1.09253  test-mlogloss:1.77679
[27]    train-mlogloss:1.07991  test-mlogloss:1.78242
[28]    train-mlogloss:1.06717  test-mlogloss:1.78867
[29]    train-mlogloss:1.05506  test-mlogloss:1.79566
Error Rate: 0.475

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m6.140s
user    0m20.319s
sys     0m0.700s
+ set +x
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

## Experiment for short hate speech 

short hate speech data မှာ တချို့ စာကြောင်းတွေက blank field တွေ ပါနေတယ်။ 

```
3670 __label__no သက်ရှိ ဘုရား ဆို တာ အမှန် ရှိ ပါ တယ် ကိုယ် ရဲ့ ကျေဇူး ရှင် မွေ မိခင် နဲ့ ကျွ ဖခင် က ဘုရား အစစ် တွေ ပါ
3671 __label__ra
3672 __label__ab တုံလုံ ရိုက်
```

အဲဒါကြောင့် load_data function မှာ blank text field ပါတဲ့ ကိစ္စပါ ထည့်သွင်းစဉ်းစားပြီး တွေ့ရင် print ရိုက်ထုတ်ဖို့ပါ update လုပ်ခဲ့တယ်။   

```
# Function to load Burmese text data
def load_data(file_path):
    texts = []
    labels = []
    label_map = {}  # Dictionary to map text labels to integers
    with open(file_path, 'r', encoding='utf-8') as file:
        for line_no, line in enumerate(file, start=1):
            parts = line.strip().split(' ', 1)
            if len(parts) < 2:
                print(f"Error: Line {line_no} in the file '{file_path}' does not contain both label and text. Skipping...")
                continue
            label = parts[0]
            text = parts[1]
            texts.append(text)
            # Extract label from the first column
            label = label.split('__label__')[-1].strip()  # Extracting label after '__label__'
            if label == "":
                label = "BLANK"  # Assigning a special label for blanks
            if label not in label_map:
                label_map[label] = len(label_map)  # Assign a unique integer to each label
            labels.append(label_map[label])  # Append the integer label
    return texts, labels, label_map

```

Experiment with short hs dataset ...  

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ ./run-short.sh
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature tfidf --num_round 30 --eval f1
+ tee tfidf-f1-short.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:2.09079  test-mlogloss:2.15884
[1]     train-mlogloss:1.94046  test-mlogloss:2.05952
[2]     train-mlogloss:1.82384  test-mlogloss:1.98623
[3]     train-mlogloss:1.72935  test-mlogloss:1.92968
[4]     train-mlogloss:1.65100  test-mlogloss:1.88545
[5]     train-mlogloss:1.58398  test-mlogloss:1.85022
[6]     train-mlogloss:1.52700  test-mlogloss:1.82211
[7]     train-mlogloss:1.47666  test-mlogloss:1.80013
[8]     train-mlogloss:1.43294  test-mlogloss:1.78309
[9]     train-mlogloss:1.39452  test-mlogloss:1.76981
[10]    train-mlogloss:1.36074  test-mlogloss:1.75931
[11]    train-mlogloss:1.33002  test-mlogloss:1.75211
[12]    train-mlogloss:1.30311  test-mlogloss:1.74730
[13]    train-mlogloss:1.27872  test-mlogloss:1.74397
[14]    train-mlogloss:1.25684  test-mlogloss:1.74253
[15]    train-mlogloss:1.23687  test-mlogloss:1.74203
[16]    train-mlogloss:1.21925  test-mlogloss:1.74314
[17]    train-mlogloss:1.20303  test-mlogloss:1.74445
[18]    train-mlogloss:1.18831  test-mlogloss:1.74697
[19]    train-mlogloss:1.17487  test-mlogloss:1.75012
[20]    train-mlogloss:1.16231  test-mlogloss:1.75447
[21]    train-mlogloss:1.15115  test-mlogloss:1.75987
[22]    train-mlogloss:1.14079  test-mlogloss:1.76493
[23]    train-mlogloss:1.13132  test-mlogloss:1.77136
[24]    train-mlogloss:1.12234  test-mlogloss:1.77705
[25]    train-mlogloss:1.11408  test-mlogloss:1.78364
[26]    train-mlogloss:1.10634  test-mlogloss:1.79089
[27]    train-mlogloss:1.09935  test-mlogloss:1.79818
[28]    train-mlogloss:1.09269  test-mlogloss:1.80512
[29]    train-mlogloss:1.08656  test-mlogloss:1.81315
F1 Score: 0.44136648549575275
Precision: 0.5794780756442228
Recall: 0.539

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.561s
user    0m10.606s
sys     0m0.569s
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --num_round 30 --eval f1
+ tee w2v-f1-short.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:2.02865  test-mlogloss:2.15080
[1]     train-mlogloss:1.84207  test-mlogloss:2.05299
[2]     train-mlogloss:1.69934  test-mlogloss:1.98063
[3]     train-mlogloss:1.58361  test-mlogloss:1.92485
[4]     train-mlogloss:1.48858  test-mlogloss:1.88377
[5]     train-mlogloss:1.40704  test-mlogloss:1.85355
[6]     train-mlogloss:1.33784  test-mlogloss:1.83007
[7]     train-mlogloss:1.27705  test-mlogloss:1.81439
[8]     train-mlogloss:1.22310  test-mlogloss:1.80288
[9]     train-mlogloss:1.17594  test-mlogloss:1.79578
[10]    train-mlogloss:1.13326  test-mlogloss:1.79206
[11]    train-mlogloss:1.09490  test-mlogloss:1.79315
[12]    train-mlogloss:1.06004  test-mlogloss:1.79674
[13]    train-mlogloss:1.02924  test-mlogloss:1.80275
[14]    train-mlogloss:1.00139  test-mlogloss:1.81052
[15]    train-mlogloss:0.97536  test-mlogloss:1.81999
[16]    train-mlogloss:0.95192  test-mlogloss:1.83052
[17]    train-mlogloss:0.92998  test-mlogloss:1.84405
[18]    train-mlogloss:0.90946  test-mlogloss:1.85687
[19]    train-mlogloss:0.89121  test-mlogloss:1.87180
[20]    train-mlogloss:0.87460  test-mlogloss:1.88647
[21]    train-mlogloss:0.85817  test-mlogloss:1.90327
[22]    train-mlogloss:0.84342  test-mlogloss:1.92075
[23]    train-mlogloss:0.82989  test-mlogloss:1.93946
[24]    train-mlogloss:0.81703  test-mlogloss:1.95795
[25]    train-mlogloss:0.80485  test-mlogloss:1.97769
[26]    train-mlogloss:0.79203  test-mlogloss:1.99760
[27]    train-mlogloss:0.78170  test-mlogloss:2.01754
[28]    train-mlogloss:0.77112  test-mlogloss:2.03730
[29]    train-mlogloss:0.76110  test-mlogloss:2.05817
F1 Score: 0.4423163997596068
Precision: 0.6982201247800353
Recall: 0.543

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.628s
user    0m13.229s
sys     0m0.492s
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --num_round 30 --eval f1
+ tee fasttext-f1-short.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:2.03638  test-mlogloss:2.15118
[1]     train-mlogloss:1.85560  test-mlogloss:2.04953
[2]     train-mlogloss:1.71785  test-mlogloss:1.97645
[3]     train-mlogloss:1.60692  test-mlogloss:1.92113
[4]     train-mlogloss:1.51526  test-mlogloss:1.87885
[5]     train-mlogloss:1.43755  test-mlogloss:1.84659
[6]     train-mlogloss:1.37047  test-mlogloss:1.82246
[7]     train-mlogloss:1.31238  test-mlogloss:1.80504
[8]     train-mlogloss:1.26140  test-mlogloss:1.79265
[9]     train-mlogloss:1.21639  test-mlogloss:1.78425
[10]    train-mlogloss:1.17671  test-mlogloss:1.77902
[11]    train-mlogloss:1.14079  test-mlogloss:1.77759
[12]    train-mlogloss:1.10845  test-mlogloss:1.77929
[13]    train-mlogloss:1.07908  test-mlogloss:1.78323
[14]    train-mlogloss:1.05327  test-mlogloss:1.78942
[15]    train-mlogloss:1.02910  test-mlogloss:1.79704
[16]    train-mlogloss:1.00708  test-mlogloss:1.80671
[17]    train-mlogloss:0.98683  test-mlogloss:1.81806
[18]    train-mlogloss:0.96806  test-mlogloss:1.82984
[19]    train-mlogloss:0.95085  test-mlogloss:1.84228
[20]    train-mlogloss:0.93532  test-mlogloss:1.85605
[21]    train-mlogloss:0.92090  test-mlogloss:1.86969
[22]    train-mlogloss:0.90741  test-mlogloss:1.88394
[23]    train-mlogloss:0.89519  test-mlogloss:1.89911
[24]    train-mlogloss:0.88371  test-mlogloss:1.91598
[25]    train-mlogloss:0.87311  test-mlogloss:1.93334
[26]    train-mlogloss:0.86339  test-mlogloss:1.95064
[27]    train-mlogloss:0.85402  test-mlogloss:1.96834
[28]    train-mlogloss:0.84520  test-mlogloss:1.98592
[29]    train-mlogloss:0.83713  test-mlogloss:2.00375
F1 Score: 0.44245727534987955
Precision: 0.7401688262657588
Recall: 0.55

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.524s
user    0m16.166s
sys     0m0.603s
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature tfidf --num_round 30 --eval logloss
+ tee tfidf-logloss-short.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:2.09079  test-mlogloss:2.15884
[1]     train-mlogloss:1.94046  test-mlogloss:2.05952
[2]     train-mlogloss:1.82384  test-mlogloss:1.98623
[3]     train-mlogloss:1.72935  test-mlogloss:1.92968
[4]     train-mlogloss:1.65100  test-mlogloss:1.88545
[5]     train-mlogloss:1.58398  test-mlogloss:1.85022
[6]     train-mlogloss:1.52700  test-mlogloss:1.82211
[7]     train-mlogloss:1.47666  test-mlogloss:1.80013
[8]     train-mlogloss:1.43294  test-mlogloss:1.78309
[9]     train-mlogloss:1.39452  test-mlogloss:1.76981
[10]    train-mlogloss:1.36074  test-mlogloss:1.75931
[11]    train-mlogloss:1.33002  test-mlogloss:1.75211
[12]    train-mlogloss:1.30311  test-mlogloss:1.74730
[13]    train-mlogloss:1.27872  test-mlogloss:1.74397
[14]    train-mlogloss:1.25684  test-mlogloss:1.74253
[15]    train-mlogloss:1.23687  test-mlogloss:1.74203
[16]    train-mlogloss:1.21925  test-mlogloss:1.74314
[17]    train-mlogloss:1.20303  test-mlogloss:1.74445
[18]    train-mlogloss:1.18831  test-mlogloss:1.74697
[19]    train-mlogloss:1.17487  test-mlogloss:1.75012
[20]    train-mlogloss:1.16231  test-mlogloss:1.75447
[21]    train-mlogloss:1.15115  test-mlogloss:1.75987
[22]    train-mlogloss:1.14079  test-mlogloss:1.76493
[23]    train-mlogloss:1.13132  test-mlogloss:1.77136
[24]    train-mlogloss:1.12234  test-mlogloss:1.77705
[25]    train-mlogloss:1.11408  test-mlogloss:1.78364
[26]    train-mlogloss:1.10634  test-mlogloss:1.79089
[27]    train-mlogloss:1.09935  test-mlogloss:1.79818
[28]    train-mlogloss:1.09269  test-mlogloss:1.80512
[29]    train-mlogloss:1.08656  test-mlogloss:1.81315
Log Loss: 1.8131501831960344

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.551s
user    0m10.524s
sys     0m0.526s
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --num_round 30 --eval logloss
+ tee w2v-logloss-short.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:2.02826  test-mlogloss:2.15533
[1]     train-mlogloss:1.84198  test-mlogloss:2.05816
[2]     train-mlogloss:1.70000  test-mlogloss:1.98561
[3]     train-mlogloss:1.58576  test-mlogloss:1.93130
[4]     train-mlogloss:1.49045  test-mlogloss:1.89027
[5]     train-mlogloss:1.40904  test-mlogloss:1.85948
[6]     train-mlogloss:1.33944  test-mlogloss:1.83733
[7]     train-mlogloss:1.27804  test-mlogloss:1.82008
[8]     train-mlogloss:1.22450  test-mlogloss:1.80779
[9]     train-mlogloss:1.17734  test-mlogloss:1.80026
[10]    train-mlogloss:1.13468  test-mlogloss:1.79612
[11]    train-mlogloss:1.09715  test-mlogloss:1.79591
[12]    train-mlogloss:1.06223  test-mlogloss:1.79842
[13]    train-mlogloss:1.03074  test-mlogloss:1.80256
[14]    train-mlogloss:1.00232  test-mlogloss:1.80940
[15]    train-mlogloss:0.97654  test-mlogloss:1.81752
[16]    train-mlogloss:0.95301  test-mlogloss:1.82772
[17]    train-mlogloss:0.93057  test-mlogloss:1.83968
[18]    train-mlogloss:0.91021  test-mlogloss:1.85252
[19]    train-mlogloss:0.89171  test-mlogloss:1.86710
[20]    train-mlogloss:0.87544  test-mlogloss:1.88240
[21]    train-mlogloss:0.85953  test-mlogloss:1.89892
[22]    train-mlogloss:0.84489  test-mlogloss:1.91610
[23]    train-mlogloss:0.83026  test-mlogloss:1.93390
[24]    train-mlogloss:0.81768  test-mlogloss:1.95288
[25]    train-mlogloss:0.80590  test-mlogloss:1.97217
[26]    train-mlogloss:0.79502  test-mlogloss:1.99109
[27]    train-mlogloss:0.78456  test-mlogloss:2.01072
[28]    train-mlogloss:0.77359  test-mlogloss:2.03119
[29]    train-mlogloss:0.76362  test-mlogloss:2.05097
Log Loss: 2.0509737588539676

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.496s
user    0m12.115s
sys     0m0.467s
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --num_round 30 --eval logloss
+ tee fasttext-logloss-short.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:2.03557  test-mlogloss:2.14955
[1]     train-mlogloss:1.85433  test-mlogloss:2.04796
[2]     train-mlogloss:1.71651  test-mlogloss:1.97443
[3]     train-mlogloss:1.60545  test-mlogloss:1.91966
[4]     train-mlogloss:1.51317  test-mlogloss:1.87766
[5]     train-mlogloss:1.43513  test-mlogloss:1.84602
[6]     train-mlogloss:1.36789  test-mlogloss:1.82260
[7]     train-mlogloss:1.30947  test-mlogloss:1.80461
[8]     train-mlogloss:1.25842  test-mlogloss:1.79262
[9]     train-mlogloss:1.21254  test-mlogloss:1.78394
[10]    train-mlogloss:1.17206  test-mlogloss:1.77865
[11]    train-mlogloss:1.13576  test-mlogloss:1.77672
[12]    train-mlogloss:1.10287  test-mlogloss:1.77742
[13]    train-mlogloss:1.07349  test-mlogloss:1.78065
[14]    train-mlogloss:1.04701  test-mlogloss:1.78614
[15]    train-mlogloss:1.02287  test-mlogloss:1.79360
[16]    train-mlogloss:1.00051  test-mlogloss:1.80224
[17]    train-mlogloss:0.98046  test-mlogloss:1.81253
[18]    train-mlogloss:0.96224  test-mlogloss:1.82289
[19]    train-mlogloss:0.94521  test-mlogloss:1.83494
[20]    train-mlogloss:0.92898  test-mlogloss:1.84838
[21]    train-mlogloss:0.91440  test-mlogloss:1.86311
[22]    train-mlogloss:0.90107  test-mlogloss:1.87878
[23]    train-mlogloss:0.88852  test-mlogloss:1.89444
[24]    train-mlogloss:0.87686  test-mlogloss:1.91052
[25]    train-mlogloss:0.86619  test-mlogloss:1.92738
[26]    train-mlogloss:0.85585  test-mlogloss:1.94475
[27]    train-mlogloss:0.84629  test-mlogloss:1.96210
[28]    train-mlogloss:0.83721  test-mlogloss:1.98000
[29]    train-mlogloss:0.82884  test-mlogloss:1.99826
Log Loss: 1.9982596663641845

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.483s
user    0m14.997s
sys     0m0.635s
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature tfidf --num_round 30 --eval error
+ tee tfidf-error-short.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:2.09079  test-mlogloss:2.15884
[1]     train-mlogloss:1.94046  test-mlogloss:2.05952
[2]     train-mlogloss:1.82384  test-mlogloss:1.98623
[3]     train-mlogloss:1.72935  test-mlogloss:1.92968
[4]     train-mlogloss:1.65100  test-mlogloss:1.88545
[5]     train-mlogloss:1.58398  test-mlogloss:1.85022
[6]     train-mlogloss:1.52700  test-mlogloss:1.82211
[7]     train-mlogloss:1.47666  test-mlogloss:1.80013
[8]     train-mlogloss:1.43294  test-mlogloss:1.78309
[9]     train-mlogloss:1.39452  test-mlogloss:1.76981
[10]    train-mlogloss:1.36074  test-mlogloss:1.75931
[11]    train-mlogloss:1.33002  test-mlogloss:1.75211
[12]    train-mlogloss:1.30311  test-mlogloss:1.74730
[13]    train-mlogloss:1.27872  test-mlogloss:1.74397
[14]    train-mlogloss:1.25684  test-mlogloss:1.74253
[15]    train-mlogloss:1.23687  test-mlogloss:1.74203
[16]    train-mlogloss:1.21925  test-mlogloss:1.74314
[17]    train-mlogloss:1.20303  test-mlogloss:1.74445
[18]    train-mlogloss:1.18831  test-mlogloss:1.74697
[19]    train-mlogloss:1.17487  test-mlogloss:1.75012
[20]    train-mlogloss:1.16231  test-mlogloss:1.75447
[21]    train-mlogloss:1.15115  test-mlogloss:1.75987
[22]    train-mlogloss:1.14079  test-mlogloss:1.76493
[23]    train-mlogloss:1.13132  test-mlogloss:1.77136
[24]    train-mlogloss:1.12234  test-mlogloss:1.77705
[25]    train-mlogloss:1.11408  test-mlogloss:1.78364
[26]    train-mlogloss:1.10634  test-mlogloss:1.79089
[27]    train-mlogloss:1.09935  test-mlogloss:1.79818
[28]    train-mlogloss:1.09269  test-mlogloss:1.80512
[29]    train-mlogloss:1.08656  test-mlogloss:1.81315
Error Rate: 0.46099999999999997

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.540s
user    0m9.901s
sys     0m0.504s
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --num_round 30 --eval error
+ tee w2v-error-short.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:2.02919  test-mlogloss:2.15161
[1]     train-mlogloss:1.84294  test-mlogloss:2.05054
[2]     train-mlogloss:1.70003  test-mlogloss:1.97750
[3]     train-mlogloss:1.58520  test-mlogloss:1.92527
[4]     train-mlogloss:1.48946  test-mlogloss:1.88409
[5]     train-mlogloss:1.40788  test-mlogloss:1.85400
[6]     train-mlogloss:1.33772  test-mlogloss:1.83166
[7]     train-mlogloss:1.27606  test-mlogloss:1.81474
[8]     train-mlogloss:1.22203  test-mlogloss:1.80319
[9]     train-mlogloss:1.17375  test-mlogloss:1.79590
[10]    train-mlogloss:1.13119  test-mlogloss:1.79345
[11]    train-mlogloss:1.09281  test-mlogloss:1.79348
[12]    train-mlogloss:1.05827  test-mlogloss:1.79640
[13]    train-mlogloss:1.02726  test-mlogloss:1.80197
[14]    train-mlogloss:0.99824  test-mlogloss:1.80905
[15]    train-mlogloss:0.97193  test-mlogloss:1.81771
[16]    train-mlogloss:0.94784  test-mlogloss:1.82816
[17]    train-mlogloss:0.92578  test-mlogloss:1.84043
[18]    train-mlogloss:0.90559  test-mlogloss:1.85418
[19]    train-mlogloss:0.88694  test-mlogloss:1.86926
[20]    train-mlogloss:0.86976  test-mlogloss:1.88492
[21]    train-mlogloss:0.85379  test-mlogloss:1.90075
[22]    train-mlogloss:0.83861  test-mlogloss:1.91765
[23]    train-mlogloss:0.82532  test-mlogloss:1.93462
[24]    train-mlogloss:0.81277  test-mlogloss:1.95255
[25]    train-mlogloss:0.80076  test-mlogloss:1.97210
[26]    train-mlogloss:0.78945  test-mlogloss:1.99159
[27]    train-mlogloss:0.77897  test-mlogloss:2.01106
[28]    train-mlogloss:0.76811  test-mlogloss:2.03113
[29]    train-mlogloss:0.75876  test-mlogloss:2.05087
Error Rate: 0.45899999999999996

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.617s
user    0m12.611s
sys     0m0.574s
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --num_round 30 --eval error
+ tee fasttext-error-short.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:2.03610  test-mlogloss:2.15107
[1]     train-mlogloss:1.85479  test-mlogloss:2.04975
[2]     train-mlogloss:1.71650  test-mlogloss:1.97537
[3]     train-mlogloss:1.60530  test-mlogloss:1.91977
[4]     train-mlogloss:1.51318  test-mlogloss:1.87750
[5]     train-mlogloss:1.43497  test-mlogloss:1.84537
[6]     train-mlogloss:1.36784  test-mlogloss:1.82088
[7]     train-mlogloss:1.30930  test-mlogloss:1.80283
[8]     train-mlogloss:1.25795  test-mlogloss:1.78983
[9]     train-mlogloss:1.21235  test-mlogloss:1.78152
[10]    train-mlogloss:1.17143  test-mlogloss:1.77710
[11]    train-mlogloss:1.13541  test-mlogloss:1.77496
[12]    train-mlogloss:1.10320  test-mlogloss:1.77575
[13]    train-mlogloss:1.07419  test-mlogloss:1.77875
[14]    train-mlogloss:1.04768  test-mlogloss:1.78434
[15]    train-mlogloss:1.02391  test-mlogloss:1.79165
[16]    train-mlogloss:1.00244  test-mlogloss:1.80093
[17]    train-mlogloss:0.98209  test-mlogloss:1.81160
[18]    train-mlogloss:0.96359  test-mlogloss:1.82246
[19]    train-mlogloss:0.94691  test-mlogloss:1.83507
[20]    train-mlogloss:0.93170  test-mlogloss:1.84836
[21]    train-mlogloss:0.91757  test-mlogloss:1.86197
[22]    train-mlogloss:0.90478  test-mlogloss:1.87704
[23]    train-mlogloss:0.89254  test-mlogloss:1.89217
[24]    train-mlogloss:0.88127  test-mlogloss:1.90784
[25]    train-mlogloss:0.87039  test-mlogloss:1.92434
[26]    train-mlogloss:0.86066  test-mlogloss:1.94089
[27]    train-mlogloss:0.85136  test-mlogloss:1.95750
[28]    train-mlogloss:0.84288  test-mlogloss:1.97481
[29]    train-mlogloss:0.83527  test-mlogloss:1.99215
Error Rate: 0.44899999999999995

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.580s
user    0m15.685s
sys     0m0.576s
+ set +x
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

## Compare Results in Terms of F1, P, R

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ grep -l "F1\|Precision\|Recall" *f1*.log | xargs tail -n 20 | grep "==\|F1\|Precision\|Recall"
==> fasttext-f1.log <==
F1 Score: 0.3989795876822859
Precision: 0.5670872926093514
Recall: 0.542
==> fasttext-f1-short.log <==
F1 Score: 0.44245727534987955
Precision: 0.7401688262657588
Recall: 0.55
==> tfidf-f1.log <==
F1 Score: 0.4007500339443313
Precision: 0.3413717532467533
Recall: 0.534
==> tfidf-f1-short.log <==
F1 Score: 0.44136648549575275
Precision: 0.5794780756442228
Recall: 0.539
==> w2v-f1.log <==
F1 Score: 0.3963040975601391
Precision: 0.6681662337662337
Recall: 0.528
==> w2v-f1-short.log <==
F1 Score: 0.4423163997596068
Precision: 0.6982201247800353
Recall: 0.543
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

## Playing with --max_depth, --feature FastText for SHORT

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 5
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.03867  test-mlogloss:2.14963
[1]     train-mlogloss:1.85998  test-mlogloss:2.04750
[2]     train-mlogloss:1.72470  test-mlogloss:1.97395
[3]     train-mlogloss:1.61599  test-mlogloss:1.91873
[4]     train-mlogloss:1.52626  test-mlogloss:1.87683
[5]     train-mlogloss:1.45024  test-mlogloss:1.84442
[6]     train-mlogloss:1.38514  test-mlogloss:1.82036
[7]     train-mlogloss:1.32842  test-mlogloss:1.80234
[8]     train-mlogloss:1.27898  test-mlogloss:1.78945
[9]     train-mlogloss:1.23528  test-mlogloss:1.78090
[10]    train-mlogloss:1.19661  test-mlogloss:1.77630
[11]    train-mlogloss:1.16189  test-mlogloss:1.77465
[12]    train-mlogloss:1.13092  test-mlogloss:1.77557
[13]    train-mlogloss:1.10323  test-mlogloss:1.77916
[14]    train-mlogloss:1.07813  test-mlogloss:1.78460
[15]    train-mlogloss:1.05545  test-mlogloss:1.79222
[16]    train-mlogloss:1.03509  test-mlogloss:1.80105
[17]    train-mlogloss:1.01615  test-mlogloss:1.81136
[18]    train-mlogloss:0.99903  test-mlogloss:1.82273
[19]    train-mlogloss:0.98358  test-mlogloss:1.83508
[20]    train-mlogloss:0.96944  test-mlogloss:1.84853
[21]    train-mlogloss:0.95648  test-mlogloss:1.86323
[22]    train-mlogloss:0.94462  test-mlogloss:1.87856
[23]    train-mlogloss:0.93339  test-mlogloss:1.89345
[24]    train-mlogloss:0.92319  test-mlogloss:1.90931
[25]    train-mlogloss:0.91402  test-mlogloss:1.92592
[26]    train-mlogloss:0.90497  test-mlogloss:1.94319
[27]    train-mlogloss:0.89681  test-mlogloss:1.96022
[28]    train-mlogloss:0.88933  test-mlogloss:1.97807
[29]    train-mlogloss:0.88223  test-mlogloss:1.99649
F1 Score: 0.44313244749755826
Precision: 0.7411992810544534
Recall: 0.55

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.320s
user    0m15.078s
sys     0m0.601s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 6
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.03600  test-mlogloss:2.14901
[1]     train-mlogloss:1.85511  test-mlogloss:2.04646
[2]     train-mlogloss:1.71737  test-mlogloss:1.97247
[3]     train-mlogloss:1.60657  test-mlogloss:1.91706
[4]     train-mlogloss:1.51429  test-mlogloss:1.87421
[5]     train-mlogloss:1.43594  test-mlogloss:1.84165
[6]     train-mlogloss:1.36890  test-mlogloss:1.81716
[7]     train-mlogloss:1.31069  test-mlogloss:1.79891
[8]     train-mlogloss:1.25935  test-mlogloss:1.78633
[9]     train-mlogloss:1.21387  test-mlogloss:1.77833
[10]    train-mlogloss:1.17309  test-mlogloss:1.77342
[11]    train-mlogloss:1.13612  test-mlogloss:1.77149
[12]    train-mlogloss:1.10306  test-mlogloss:1.77325
[13]    train-mlogloss:1.07350  test-mlogloss:1.77724
[14]    train-mlogloss:1.04646  test-mlogloss:1.78328
[15]    train-mlogloss:1.02217  test-mlogloss:1.79044
[16]    train-mlogloss:0.99992  test-mlogloss:1.79935
[17]    train-mlogloss:0.97955  test-mlogloss:1.80998
[18]    train-mlogloss:0.96111  test-mlogloss:1.82153
[19]    train-mlogloss:0.94438  test-mlogloss:1.83412
[20]    train-mlogloss:0.92905  test-mlogloss:1.84789
[21]    train-mlogloss:0.91530  test-mlogloss:1.86275
[22]    train-mlogloss:0.90230  test-mlogloss:1.87719
[23]    train-mlogloss:0.89030  test-mlogloss:1.89327
[24]    train-mlogloss:0.87847  test-mlogloss:1.90981
[25]    train-mlogloss:0.86818  test-mlogloss:1.92652
[26]    train-mlogloss:0.85830  test-mlogloss:1.94353
[27]    train-mlogloss:0.84843  test-mlogloss:1.96127
[28]    train-mlogloss:0.83950  test-mlogloss:1.97921
[29]    train-mlogloss:0.83089  test-mlogloss:1.99709
F1 Score: 0.4427794071781406
Precision: 0.7406212255474551
Recall: 0.55

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.412s
user    0m15.012s
sys     0m0.596s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 7
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.03256  test-mlogloss:2.14911
[1]     train-mlogloss:1.84851  test-mlogloss:2.04672
[2]     train-mlogloss:1.70740  test-mlogloss:1.97396
[3]     train-mlogloss:1.59389  test-mlogloss:1.91869
[4]     train-mlogloss:1.49908  test-mlogloss:1.87702
[5]     train-mlogloss:1.41810  test-mlogloss:1.84554
[6]     train-mlogloss:1.34836  test-mlogloss:1.82113
[7]     train-mlogloss:1.28691  test-mlogloss:1.80357
[8]     train-mlogloss:1.23331  test-mlogloss:1.79040
[9]     train-mlogloss:1.18597  test-mlogloss:1.78115
[10]    train-mlogloss:1.14397  test-mlogloss:1.77660
[11]    train-mlogloss:1.10675  test-mlogloss:1.77470
[12]    train-mlogloss:1.07213  test-mlogloss:1.77539
[13]    train-mlogloss:1.04091  test-mlogloss:1.77848
[14]    train-mlogloss:1.01356  test-mlogloss:1.78374
[15]    train-mlogloss:0.98784  test-mlogloss:1.79177
[16]    train-mlogloss:0.96437  test-mlogloss:1.80075
[17]    train-mlogloss:0.94236  test-mlogloss:1.81116
[18]    train-mlogloss:0.92244  test-mlogloss:1.82256
[19]    train-mlogloss:0.90370  test-mlogloss:1.83532
[20]    train-mlogloss:0.88652  test-mlogloss:1.84995
[21]    train-mlogloss:0.87078  test-mlogloss:1.86450
[22]    train-mlogloss:0.85653  test-mlogloss:1.87987
[23]    train-mlogloss:0.84283  test-mlogloss:1.89554
[24]    train-mlogloss:0.82992  test-mlogloss:1.91134
[25]    train-mlogloss:0.81800  test-mlogloss:1.92820
[26]    train-mlogloss:0.80591  test-mlogloss:1.94575
[27]    train-mlogloss:0.79516  test-mlogloss:1.96334
[28]    train-mlogloss:0.78440  test-mlogloss:1.98181
[29]    train-mlogloss:0.77505  test-mlogloss:2.00005
F1 Score: 0.4452705132743363
Precision: 0.7228352320422113
Recall: 0.551

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.850s
user    0m17.121s
sys     0m0.780s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 8
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.02978  test-mlogloss:2.14987
[1]     train-mlogloss:1.84386  test-mlogloss:2.04854
[2]     train-mlogloss:1.70009  test-mlogloss:1.97532
[3]     train-mlogloss:1.58360  test-mlogloss:1.92017
[4]     train-mlogloss:1.48733  test-mlogloss:1.87906
[5]     train-mlogloss:1.40440  test-mlogloss:1.84716
[6]     train-mlogloss:1.33232  test-mlogloss:1.82272
[7]     train-mlogloss:1.26919  test-mlogloss:1.80485
[8]     train-mlogloss:1.21362  test-mlogloss:1.79210
[9]     train-mlogloss:1.16413  test-mlogloss:1.78347
[10]    train-mlogloss:1.11962  test-mlogloss:1.77884
[11]    train-mlogloss:1.07952  test-mlogloss:1.77815
[12]    train-mlogloss:1.04241  test-mlogloss:1.78035
[13]    train-mlogloss:1.00954  test-mlogloss:1.78463
[14]    train-mlogloss:0.97840  test-mlogloss:1.79025
[15]    train-mlogloss:0.95001  test-mlogloss:1.79747
[16]    train-mlogloss:0.92321  test-mlogloss:1.80588
[17]    train-mlogloss:0.89938  test-mlogloss:1.81661
[18]    train-mlogloss:0.87823  test-mlogloss:1.82864
[19]    train-mlogloss:0.85882  test-mlogloss:1.84175
[20]    train-mlogloss:0.84064  test-mlogloss:1.85622
[21]    train-mlogloss:0.82305  test-mlogloss:1.87120
[22]    train-mlogloss:0.80735  test-mlogloss:1.88714
[23]    train-mlogloss:0.79276  test-mlogloss:1.90317
[24]    train-mlogloss:0.77939  test-mlogloss:1.91881
[25]    train-mlogloss:0.76510  test-mlogloss:1.93591
[26]    train-mlogloss:0.75204  test-mlogloss:1.95280
[27]    train-mlogloss:0.74065  test-mlogloss:1.97019
[28]    train-mlogloss:0.73073  test-mlogloss:1.98797
[29]    train-mlogloss:0.72121  test-mlogloss:2.00659
F1 Score: 0.44276809453471194
Precision: 0.5833652173913043
Recall: 0.546

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m5.192s
user    0m18.318s
sys     0m0.629s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 9
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.02578  test-mlogloss:2.14812
[1]     train-mlogloss:1.83603  test-mlogloss:2.04630
[2]     train-mlogloss:1.68920  test-mlogloss:1.97043
[3]     train-mlogloss:1.57083  test-mlogloss:1.91556
[4]     train-mlogloss:1.47140  test-mlogloss:1.87365
[5]     train-mlogloss:1.38532  test-mlogloss:1.84148
[6]     train-mlogloss:1.31104  test-mlogloss:1.81624
[7]     train-mlogloss:1.24564  test-mlogloss:1.79806
[8]     train-mlogloss:1.18774  test-mlogloss:1.78527
[9]     train-mlogloss:1.13610  test-mlogloss:1.77592
[10]    train-mlogloss:1.08966  test-mlogloss:1.77049
[11]    train-mlogloss:1.04762  test-mlogloss:1.76910
[12]    train-mlogloss:1.00946  test-mlogloss:1.77000
[13]    train-mlogloss:0.97532  test-mlogloss:1.77329
[14]    train-mlogloss:0.94454  test-mlogloss:1.77908
[15]    train-mlogloss:0.91671  test-mlogloss:1.78652
[16]    train-mlogloss:0.89038  test-mlogloss:1.79565
[17]    train-mlogloss:0.86533  test-mlogloss:1.80602
[18]    train-mlogloss:0.84238  test-mlogloss:1.81886
[19]    train-mlogloss:0.82193  test-mlogloss:1.83184
[20]    train-mlogloss:0.80213  test-mlogloss:1.84564
[21]    train-mlogloss:0.78442  test-mlogloss:1.86049
[22]    train-mlogloss:0.76775  test-mlogloss:1.87588
[23]    train-mlogloss:0.75274  test-mlogloss:1.89243
[24]    train-mlogloss:0.73800  test-mlogloss:1.90864
[25]    train-mlogloss:0.72419  test-mlogloss:1.92622
[26]    train-mlogloss:0.70927  test-mlogloss:1.94420
[27]    train-mlogloss:0.69678  test-mlogloss:1.96223
[28]    train-mlogloss:0.68434  test-mlogloss:1.98091
[29]    train-mlogloss:0.67264  test-mlogloss:2.00046
F1 Score: 0.44134098940989414
Precision: 0.6298925912796881
Recall: 0.545

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m5.586s
user    0m19.568s
sys     0m0.743s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 10
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.02604  test-mlogloss:2.14891
[1]     train-mlogloss:1.83508  test-mlogloss:2.04739
[2]     train-mlogloss:1.68810  test-mlogloss:1.97422
[3]     train-mlogloss:1.56887  test-mlogloss:1.91934
[4]     train-mlogloss:1.46766  test-mlogloss:1.87618
[5]     train-mlogloss:1.38104  test-mlogloss:1.84525
[6]     train-mlogloss:1.30562  test-mlogloss:1.82127
[7]     train-mlogloss:1.23952  test-mlogloss:1.80384
[8]     train-mlogloss:1.18035  test-mlogloss:1.79166
[9]     train-mlogloss:1.12699  test-mlogloss:1.78327
[10]    train-mlogloss:1.07938  test-mlogloss:1.77906
[11]    train-mlogloss:1.03752  test-mlogloss:1.77764
[12]    train-mlogloss:0.99916  test-mlogloss:1.77849
[13]    train-mlogloss:0.96387  test-mlogloss:1.78245
[14]    train-mlogloss:0.93193  test-mlogloss:1.78834
[15]    train-mlogloss:0.90216  test-mlogloss:1.79507
[16]    train-mlogloss:0.87448  test-mlogloss:1.80395
[17]    train-mlogloss:0.84900  test-mlogloss:1.81376
[18]    train-mlogloss:0.82413  test-mlogloss:1.82586
[19]    train-mlogloss:0.80178  test-mlogloss:1.83777
[20]    train-mlogloss:0.78169  test-mlogloss:1.85163
[21]    train-mlogloss:0.76265  test-mlogloss:1.86607
[22]    train-mlogloss:0.74475  test-mlogloss:1.88123
[23]    train-mlogloss:0.72751  test-mlogloss:1.89762
[24]    train-mlogloss:0.71210  test-mlogloss:1.91473
[25]    train-mlogloss:0.69663  test-mlogloss:1.93232
[26]    train-mlogloss:0.68349  test-mlogloss:1.94886
[27]    train-mlogloss:0.66897  test-mlogloss:1.96668
[28]    train-mlogloss:0.65726  test-mlogloss:1.98488
[29]    train-mlogloss:0.64461  test-mlogloss:2.00394
F1 Score: 0.44362801090834825
Precision: 0.5961369608185094
Recall: 0.545

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m6.161s
user    0m22.207s
sys     0m0.723s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

## Playing with --max_depth, --feature tfidf for SHORT

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature tfidf --num_round 30 --eval f1 --max_depth 6
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.09079  test-mlogloss:2.15884
[1]     train-mlogloss:1.94046  test-mlogloss:2.05952
[2]     train-mlogloss:1.82384  test-mlogloss:1.98623
[3]     train-mlogloss:1.72935  test-mlogloss:1.92968
[4]     train-mlogloss:1.65100  test-mlogloss:1.88545
[5]     train-mlogloss:1.58398  test-mlogloss:1.85022
[6]     train-mlogloss:1.52700  test-mlogloss:1.82211
[7]     train-mlogloss:1.47666  test-mlogloss:1.80013
[8]     train-mlogloss:1.43294  test-mlogloss:1.78309
[9]     train-mlogloss:1.39452  test-mlogloss:1.76981
[10]    train-mlogloss:1.36074  test-mlogloss:1.75931
[11]    train-mlogloss:1.33002  test-mlogloss:1.75211
[12]    train-mlogloss:1.30311  test-mlogloss:1.74730
[13]    train-mlogloss:1.27872  test-mlogloss:1.74397
[14]    train-mlogloss:1.25684  test-mlogloss:1.74253
[15]    train-mlogloss:1.23687  test-mlogloss:1.74203
[16]    train-mlogloss:1.21925  test-mlogloss:1.74314
[17]    train-mlogloss:1.20303  test-mlogloss:1.74445
[18]    train-mlogloss:1.18831  test-mlogloss:1.74697
[19]    train-mlogloss:1.17487  test-mlogloss:1.75012
[20]    train-mlogloss:1.16231  test-mlogloss:1.75447
[21]    train-mlogloss:1.15115  test-mlogloss:1.75987
[22]    train-mlogloss:1.14079  test-mlogloss:1.76493
[23]    train-mlogloss:1.13132  test-mlogloss:1.77136
[24]    train-mlogloss:1.12234  test-mlogloss:1.77705
[25]    train-mlogloss:1.11408  test-mlogloss:1.78364
[26]    train-mlogloss:1.10634  test-mlogloss:1.79089
[27]    train-mlogloss:1.09935  test-mlogloss:1.79818
[28]    train-mlogloss:1.09269  test-mlogloss:1.80512
[29]    train-mlogloss:1.08656  test-mlogloss:1.81315
F1 Score: 0.44136648549575275
Precision: 0.5794780756442228
Recall: 0.539

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.557s
user    0m10.896s
sys     0m0.423s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature tfidf --num_round 30 --eval f1 --max_depth 7
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.08767  test-mlogloss:2.15687
[1]     train-mlogloss:1.93546  test-mlogloss:2.05742
[2]     train-mlogloss:1.81798  test-mlogloss:1.98435
[3]     train-mlogloss:1.72206  test-mlogloss:1.92838
[4]     train-mlogloss:1.64261  test-mlogloss:1.88452
[5]     train-mlogloss:1.57520  test-mlogloss:1.84980
[6]     train-mlogloss:1.51753  test-mlogloss:1.82222
[7]     train-mlogloss:1.46730  test-mlogloss:1.79999
[8]     train-mlogloss:1.42346  test-mlogloss:1.78221
[9]     train-mlogloss:1.38418  test-mlogloss:1.76894
[10]    train-mlogloss:1.34991  test-mlogloss:1.75900
[11]    train-mlogloss:1.31902  test-mlogloss:1.75167
[12]    train-mlogloss:1.29165  test-mlogloss:1.74678
[13]    train-mlogloss:1.26703  test-mlogloss:1.74424
[14]    train-mlogloss:1.24502  test-mlogloss:1.74213
[15]    train-mlogloss:1.22485  test-mlogloss:1.74166
[16]    train-mlogloss:1.20674  test-mlogloss:1.74286
[17]    train-mlogloss:1.19016  test-mlogloss:1.74494
[18]    train-mlogloss:1.17516  test-mlogloss:1.74816
[19]    train-mlogloss:1.16141  test-mlogloss:1.75260
[20]    train-mlogloss:1.14889  test-mlogloss:1.75724
[21]    train-mlogloss:1.13758  test-mlogloss:1.76257
[22]    train-mlogloss:1.12696  test-mlogloss:1.76856
[23]    train-mlogloss:1.11702  test-mlogloss:1.77502
[24]    train-mlogloss:1.10817  test-mlogloss:1.78101
[25]    train-mlogloss:1.09971  test-mlogloss:1.78749
[26]    train-mlogloss:1.09161  test-mlogloss:1.79465
[27]    train-mlogloss:1.08418  test-mlogloss:1.80196
[28]    train-mlogloss:1.07737  test-mlogloss:1.81012
[29]    train-mlogloss:1.07100  test-mlogloss:1.81779
F1 Score: 0.4406243977472294
Precision: 0.5793851831835248
Recall: 0.537

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.646s
user    0m10.327s
sys     0m0.498s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature tfidf --num_round 30 --eval f1 --max_depth 8
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.08546  test-mlogloss:2.15576
[1]     train-mlogloss:1.93159  test-mlogloss:2.05621
[2]     train-mlogloss:1.81267  test-mlogloss:1.98252
[3]     train-mlogloss:1.71663  test-mlogloss:1.92665
[4]     train-mlogloss:1.63655  test-mlogloss:1.88233
[5]     train-mlogloss:1.56834  test-mlogloss:1.84784
[6]     train-mlogloss:1.50975  test-mlogloss:1.81982
[7]     train-mlogloss:1.45850  test-mlogloss:1.79727
[8]     train-mlogloss:1.41373  test-mlogloss:1.78021
[9]     train-mlogloss:1.37439  test-mlogloss:1.76724
[10]    train-mlogloss:1.33951  test-mlogloss:1.75719
[11]    train-mlogloss:1.30825  test-mlogloss:1.75015
[12]    train-mlogloss:1.28033  test-mlogloss:1.74472
[13]    train-mlogloss:1.25521  test-mlogloss:1.74233
[14]    train-mlogloss:1.23287  test-mlogloss:1.74076
[15]    train-mlogloss:1.21245  test-mlogloss:1.74173
[16]    train-mlogloss:1.19430  test-mlogloss:1.74310
[17]    train-mlogloss:1.17763  test-mlogloss:1.74634
[18]    train-mlogloss:1.16214  test-mlogloss:1.74933
[19]    train-mlogloss:1.14805  test-mlogloss:1.75422
[20]    train-mlogloss:1.13519  test-mlogloss:1.75925
[21]    train-mlogloss:1.12354  test-mlogloss:1.76530
[22]    train-mlogloss:1.11254  test-mlogloss:1.77174
[23]    train-mlogloss:1.10248  test-mlogloss:1.77839
[24]    train-mlogloss:1.09335  test-mlogloss:1.78504
[25]    train-mlogloss:1.08475  test-mlogloss:1.79141
[26]    train-mlogloss:1.07634  test-mlogloss:1.79865
[27]    train-mlogloss:1.06875  test-mlogloss:1.80642
[28]    train-mlogloss:1.06163  test-mlogloss:1.81463
[29]    train-mlogloss:1.05506  test-mlogloss:1.82243
F1 Score: 0.43928133580705014
Precision: 0.5783720862470861
Recall: 0.533

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.826s
user    0m11.319s
sys     0m0.476s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature tfidf --num_round 30 --eval f1 --max_depth 9
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.08327  test-mlogloss:2.15538
[1]     train-mlogloss:1.92787  test-mlogloss:2.05538
[2]     train-mlogloss:1.80766  test-mlogloss:1.98208
[3]     train-mlogloss:1.71050  test-mlogloss:1.92559
[4]     train-mlogloss:1.62939  test-mlogloss:1.88106
[5]     train-mlogloss:1.56041  test-mlogloss:1.84578
[6]     train-mlogloss:1.50168  test-mlogloss:1.81822
[7]     train-mlogloss:1.45037  test-mlogloss:1.79627
[8]     train-mlogloss:1.40505  test-mlogloss:1.77935
[9]     train-mlogloss:1.36507  test-mlogloss:1.76586
[10]    train-mlogloss:1.32975  test-mlogloss:1.75631
[11]    train-mlogloss:1.29827  test-mlogloss:1.74957
[12]    train-mlogloss:1.27017  test-mlogloss:1.74482
[13]    train-mlogloss:1.24487  test-mlogloss:1.74266
[14]    train-mlogloss:1.22198  test-mlogloss:1.74239
[15]    train-mlogloss:1.20153  test-mlogloss:1.74273
[16]    train-mlogloss:1.18291  test-mlogloss:1.74480
[17]    train-mlogloss:1.16594  test-mlogloss:1.74833
[18]    train-mlogloss:1.15069  test-mlogloss:1.75208
[19]    train-mlogloss:1.13646  test-mlogloss:1.75743
[20]    train-mlogloss:1.12323  test-mlogloss:1.76233
[21]    train-mlogloss:1.11147  test-mlogloss:1.76793
[22]    train-mlogloss:1.10035  test-mlogloss:1.77476
[23]    train-mlogloss:1.09022  test-mlogloss:1.78100
[24]    train-mlogloss:1.08072  test-mlogloss:1.78858
[25]    train-mlogloss:1.07184  test-mlogloss:1.79600
[26]    train-mlogloss:1.06370  test-mlogloss:1.80362
[27]    train-mlogloss:1.05615  test-mlogloss:1.81139
[28]    train-mlogloss:1.04861  test-mlogloss:1.82004
[29]    train-mlogloss:1.04207  test-mlogloss:1.82837
F1 Score: 0.4375771440114212
Precision: 0.5759896878955348
Recall: 0.532

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.019s
user    0m12.556s
sys     0m0.541s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature tfidf --num_round 30 --eval f1 --max_depth 10
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.08144  test-mlogloss:2.15506
[1]     train-mlogloss:1.92455  test-mlogloss:2.05402
[2]     train-mlogloss:1.80352  test-mlogloss:1.98021
[3]     train-mlogloss:1.70510  test-mlogloss:1.92387
[4]     train-mlogloss:1.62348  test-mlogloss:1.87941
[5]     train-mlogloss:1.55399  test-mlogloss:1.84461
[6]     train-mlogloss:1.49470  test-mlogloss:1.81636
[7]     train-mlogloss:1.44261  test-mlogloss:1.79456
[8]     train-mlogloss:1.39743  test-mlogloss:1.77783
[9]     train-mlogloss:1.35697  test-mlogloss:1.76486
[10]    train-mlogloss:1.32094  test-mlogloss:1.75466
[11]    train-mlogloss:1.28926  test-mlogloss:1.74767
[12]    train-mlogloss:1.26062  test-mlogloss:1.74295
[13]    train-mlogloss:1.23514  test-mlogloss:1.74081
[14]    train-mlogloss:1.21214  test-mlogloss:1.74070
[15]    train-mlogloss:1.19143  test-mlogloss:1.74204
[16]    train-mlogloss:1.17246  test-mlogloss:1.74487
[17]    train-mlogloss:1.15540  test-mlogloss:1.74868
[18]    train-mlogloss:1.13983  test-mlogloss:1.75263
[19]    train-mlogloss:1.12556  test-mlogloss:1.75786
[20]    train-mlogloss:1.11228  test-mlogloss:1.76363
[21]    train-mlogloss:1.10043  test-mlogloss:1.76942
[22]    train-mlogloss:1.08930  test-mlogloss:1.77559
[23]    train-mlogloss:1.07911  test-mlogloss:1.78231
[24]    train-mlogloss:1.06944  test-mlogloss:1.79025
[25]    train-mlogloss:1.06056  test-mlogloss:1.79817
[26]    train-mlogloss:1.05210  test-mlogloss:1.80641
[27]    train-mlogloss:1.04459  test-mlogloss:1.81474
[28]    train-mlogloss:1.03727  test-mlogloss:1.82351
[29]    train-mlogloss:1.03044  test-mlogloss:1.83186
F1 Score: 0.43906122253056323
Precision: 0.5785504220378114
Recall: 0.532

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.107s
user    0m12.817s
sys     0m0.476s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

## Playing --max_dept, --feature word2vec for SHORT

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --num
_round 30 --eval f1 --max_depth 5
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.03234  test-mlogloss:2.15047
[1]     train-mlogloss:1.84940  test-mlogloss:2.04851
[2]     train-mlogloss:1.71034  test-mlogloss:1.97656
[3]     train-mlogloss:1.59865  test-mlogloss:1.92204
[4]     train-mlogloss:1.50597  test-mlogloss:1.88108
[5]     train-mlogloss:1.42728  test-mlogloss:1.85092
[6]     train-mlogloss:1.35989  test-mlogloss:1.82817
[7]     train-mlogloss:1.30143  test-mlogloss:1.81139
[8]     train-mlogloss:1.25038  test-mlogloss:1.80004
[9]     train-mlogloss:1.20499  test-mlogloss:1.79347
[10]    train-mlogloss:1.16393  test-mlogloss:1.79023
[11]    train-mlogloss:1.12727  test-mlogloss:1.78943
[12]    train-mlogloss:1.09442  test-mlogloss:1.79162
[13]    train-mlogloss:1.06489  test-mlogloss:1.79665
[14]    train-mlogloss:1.03841  test-mlogloss:1.80405
[15]    train-mlogloss:1.01432  test-mlogloss:1.81297
[16]    train-mlogloss:0.99223  test-mlogloss:1.82391
[17]    train-mlogloss:0.97223  test-mlogloss:1.83559
[18]    train-mlogloss:0.95433  test-mlogloss:1.84840
[19]    train-mlogloss:0.93784  test-mlogloss:1.86208
[20]    train-mlogloss:0.92268  test-mlogloss:1.87752
[21]    train-mlogloss:0.90847  test-mlogloss:1.89429
[22]    train-mlogloss:0.89487  test-mlogloss:1.91074
[23]    train-mlogloss:0.88227  test-mlogloss:1.92881
[24]    train-mlogloss:0.87118  test-mlogloss:1.94714
[25]    train-mlogloss:0.85990  test-mlogloss:1.96595
[26]    train-mlogloss:0.84894  test-mlogloss:1.98610
[27]    train-mlogloss:0.83981  test-mlogloss:2.00546
[28]    train-mlogloss:0.83088  test-mlogloss:2.02530
[29]    train-mlogloss:0.82266  test-mlogloss:2.04588
F1 Score: 0.43987248322147654
Precision: 0.7215454545454545
Recall: 0.537

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.332s
user    0m11.899s
sys     0m0.468s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --num_round 30 --eval f1 --max_depth 6
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.02867  test-mlogloss:2.15180
[1]     train-mlogloss:1.84285  test-mlogloss:2.05450
[2]     train-mlogloss:1.70034  test-mlogloss:1.98137
[3]     train-mlogloss:1.58602  test-mlogloss:1.92752
[4]     train-mlogloss:1.49100  test-mlogloss:1.88709
[5]     train-mlogloss:1.41032  test-mlogloss:1.85616
[6]     train-mlogloss:1.34037  test-mlogloss:1.83305
[7]     train-mlogloss:1.28043  test-mlogloss:1.81634
[8]     train-mlogloss:1.22753  test-mlogloss:1.80403
[9]     train-mlogloss:1.18010  test-mlogloss:1.79757
[10]    train-mlogloss:1.13877  test-mlogloss:1.79419
[11]    train-mlogloss:1.10033  test-mlogloss:1.79417
[12]    train-mlogloss:1.06601  test-mlogloss:1.79634
[13]    train-mlogloss:1.03542  test-mlogloss:1.80020
[14]    train-mlogloss:1.00783  test-mlogloss:1.80673
[15]    train-mlogloss:0.98233  test-mlogloss:1.81484
[16]    train-mlogloss:0.95872  test-mlogloss:1.82499
[17]    train-mlogloss:0.93712  test-mlogloss:1.83580
[18]    train-mlogloss:0.91733  test-mlogloss:1.84915
[19]    train-mlogloss:0.89956  test-mlogloss:1.86334
[20]    train-mlogloss:0.88243  test-mlogloss:1.87944
[21]    train-mlogloss:0.86687  test-mlogloss:1.89498
[22]    train-mlogloss:0.85234  test-mlogloss:1.91194
[23]    train-mlogloss:0.83812  test-mlogloss:1.92977
[24]    train-mlogloss:0.82555  test-mlogloss:1.94881
[25]    train-mlogloss:0.81387  test-mlogloss:1.96688
[26]    train-mlogloss:0.80207  test-mlogloss:1.98401
[27]    train-mlogloss:0.79130  test-mlogloss:2.00163
[28]    train-mlogloss:0.78085  test-mlogloss:2.02132
[29]    train-mlogloss:0.77194  test-mlogloss:2.04152
F1 Score: 0.44342364880811896
Precision: 0.690280921494073
Recall: 0.54

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.550s
user    0m12.798s
sys     0m0.580s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --num_round 30 --eval f1 --max_depth 7
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.02483  test-mlogloss:2.15228
[1]     train-mlogloss:1.83516  test-mlogloss:2.05041
[2]     train-mlogloss:1.69043  test-mlogloss:1.97920
[3]     train-mlogloss:1.57028  test-mlogloss:1.92560
[4]     train-mlogloss:1.47037  test-mlogloss:1.88501
[5]     train-mlogloss:1.38442  test-mlogloss:1.85083
[6]     train-mlogloss:1.31004  test-mlogloss:1.82835
[7]     train-mlogloss:1.24565  test-mlogloss:1.81252
[8]     train-mlogloss:1.18924  test-mlogloss:1.80185
[9]     train-mlogloss:1.13957  test-mlogloss:1.79525
[10]    train-mlogloss:1.09397  test-mlogloss:1.79145
[11]    train-mlogloss:1.05176  test-mlogloss:1.79026
[12]    train-mlogloss:1.01463  test-mlogloss:1.79283
[13]    train-mlogloss:0.98131  test-mlogloss:1.79772
[14]    train-mlogloss:0.95141  test-mlogloss:1.80493
[15]    train-mlogloss:0.92439  test-mlogloss:1.81391
[16]    train-mlogloss:0.89957  test-mlogloss:1.82546
[17]    train-mlogloss:0.87579  test-mlogloss:1.83800
[18]    train-mlogloss:0.85513  test-mlogloss:1.85161
[19]    train-mlogloss:0.83601  test-mlogloss:1.86715
[20]    train-mlogloss:0.81749  test-mlogloss:1.88262
[21]    train-mlogloss:0.79980  test-mlogloss:1.89957
[22]    train-mlogloss:0.78402  test-mlogloss:1.91754
[23]    train-mlogloss:0.76873  test-mlogloss:1.93585
[24]    train-mlogloss:0.75310  test-mlogloss:1.95557
[25]    train-mlogloss:0.73860  test-mlogloss:1.97483
[26]    train-mlogloss:0.72593  test-mlogloss:1.99425
[27]    train-mlogloss:0.71368  test-mlogloss:2.01411
[28]    train-mlogloss:0.70298  test-mlogloss:2.03449
[29]    train-mlogloss:0.69213  test-mlogloss:2.05485
F1 Score: 0.44280806572068715
Precision: 0.6102658227848101
Recall: 0.54

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.992s
user    0m14.560s
sys     0m0.651s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --num_round 30 --eval f1 --max_depth 8
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.02029  test-mlogloss:2.15389
[1]     train-mlogloss:1.82565  test-mlogloss:2.05370
[2]     train-mlogloss:1.67494  test-mlogloss:1.97987
[3]     train-mlogloss:1.55272  test-mlogloss:1.92820
[4]     train-mlogloss:1.45055  test-mlogloss:1.88852
[5]     train-mlogloss:1.36322  test-mlogloss:1.85934
[6]     train-mlogloss:1.28541  test-mlogloss:1.83777
[7]     train-mlogloss:1.21768  test-mlogloss:1.82025
[8]     train-mlogloss:1.15749  test-mlogloss:1.80827
[9]     train-mlogloss:1.10554  test-mlogloss:1.80173
[10]    train-mlogloss:1.05793  test-mlogloss:1.79795
[11]    train-mlogloss:1.01645  test-mlogloss:1.79790
[12]    train-mlogloss:0.97899  test-mlogloss:1.80054
[13]    train-mlogloss:0.94337  test-mlogloss:1.80529
[14]    train-mlogloss:0.91004  test-mlogloss:1.81357
[15]    train-mlogloss:0.88027  test-mlogloss:1.82307
[16]    train-mlogloss:0.85221  test-mlogloss:1.83305
[17]    train-mlogloss:0.82416  test-mlogloss:1.84511
[18]    train-mlogloss:0.79841  test-mlogloss:1.85780
[19]    train-mlogloss:0.77581  test-mlogloss:1.87255
[20]    train-mlogloss:0.75505  test-mlogloss:1.88914
[21]    train-mlogloss:0.73529  test-mlogloss:1.90505
[22]    train-mlogloss:0.71617  test-mlogloss:1.92242
[23]    train-mlogloss:0.69959  test-mlogloss:1.94019
[24]    train-mlogloss:0.68342  test-mlogloss:1.95805
[25]    train-mlogloss:0.66910  test-mlogloss:1.97749
[26]    train-mlogloss:0.65396  test-mlogloss:1.99719
[27]    train-mlogloss:0.64029  test-mlogloss:2.01744
[28]    train-mlogloss:0.62766  test-mlogloss:2.03706
[29]    train-mlogloss:0.61565  test-mlogloss:2.05773
F1 Score: 0.44487490494296583
Precision: 0.6057731070496084
Recall: 0.533

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m3.406s
user    0m15.915s
sys     0m0.642s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --num_round 30 --eval f1 --max_depth 9
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.01392  test-mlogloss:2.15356
[1]     train-mlogloss:1.81601  test-mlogloss:2.05312
[2]     train-mlogloss:1.66081  test-mlogloss:1.98192
[3]     train-mlogloss:1.53505  test-mlogloss:1.92841
[4]     train-mlogloss:1.42947  test-mlogloss:1.88574
[5]     train-mlogloss:1.33922  test-mlogloss:1.85431
[6]     train-mlogloss:1.26187  test-mlogloss:1.83090
[7]     train-mlogloss:1.19391  test-mlogloss:1.81406
[8]     train-mlogloss:1.13363  test-mlogloss:1.80213
[9]     train-mlogloss:1.07822  test-mlogloss:1.79483
[10]    train-mlogloss:1.02971  test-mlogloss:1.79092
[11]    train-mlogloss:0.98566  test-mlogloss:1.79139
[12]    train-mlogloss:0.94353  test-mlogloss:1.79361
[13]    train-mlogloss:0.90639  test-mlogloss:1.79994
[14]    train-mlogloss:0.87094  test-mlogloss:1.80803
[15]    train-mlogloss:0.83922  test-mlogloss:1.81687
[16]    train-mlogloss:0.81000  test-mlogloss:1.82747
[17]    train-mlogloss:0.78443  test-mlogloss:1.83997
[18]    train-mlogloss:0.76127  test-mlogloss:1.85435
[19]    train-mlogloss:0.73717  test-mlogloss:1.86897
[20]    train-mlogloss:0.71399  test-mlogloss:1.88356
[21]    train-mlogloss:0.69230  test-mlogloss:1.89973
[22]    train-mlogloss:0.67173  test-mlogloss:1.91620
[23]    train-mlogloss:0.65336  test-mlogloss:1.93360
[24]    train-mlogloss:0.63678  test-mlogloss:1.95116
[25]    train-mlogloss:0.62064  test-mlogloss:1.96956
[26]    train-mlogloss:0.60452  test-mlogloss:1.98847
[27]    train-mlogloss:0.59233  test-mlogloss:2.00710
[28]    train-mlogloss:0.57811  test-mlogloss:2.02590
[29]    train-mlogloss:0.56440  test-mlogloss:2.04678
F1 Score: 0.4430746124963897
Precision: 0.6021127116127115
Recall: 0.535

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m3.844s
user    0m18.014s
sys     0m0.611s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --num_round 30 --eval f1 --max_depth 10
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.01082  test-mlogloss:2.15640
[1]     train-mlogloss:1.80798  test-mlogloss:2.05802
[2]     train-mlogloss:1.65264  test-mlogloss:1.98868
[3]     train-mlogloss:1.52491  test-mlogloss:1.93623
[4]     train-mlogloss:1.41924  test-mlogloss:1.89396
[5]     train-mlogloss:1.32820  test-mlogloss:1.86114
[6]     train-mlogloss:1.24860  test-mlogloss:1.83844
[7]     train-mlogloss:1.17688  test-mlogloss:1.82078
[8]     train-mlogloss:1.11179  test-mlogloss:1.80923
[9]     train-mlogloss:1.05457  test-mlogloss:1.80368
[10]    train-mlogloss:1.00189  test-mlogloss:1.80093
[11]    train-mlogloss:0.95421  test-mlogloss:1.80270
[12]    train-mlogloss:0.91077  test-mlogloss:1.80700
[13]    train-mlogloss:0.87088  test-mlogloss:1.81207
[14]    train-mlogloss:0.83444  test-mlogloss:1.81690
[15]    train-mlogloss:0.80256  test-mlogloss:1.82650
[16]    train-mlogloss:0.77258  test-mlogloss:1.83852
[17]    train-mlogloss:0.74538  test-mlogloss:1.85293
[18]    train-mlogloss:0.71938  test-mlogloss:1.86808
[19]    train-mlogloss:0.69307  test-mlogloss:1.88159
[20]    train-mlogloss:0.66754  test-mlogloss:1.89953
[21]    train-mlogloss:0.64403  test-mlogloss:1.91761
[22]    train-mlogloss:0.62040  test-mlogloss:1.93479
[23]    train-mlogloss:0.60009  test-mlogloss:1.95450
[24]    train-mlogloss:0.58221  test-mlogloss:1.97391
[25]    train-mlogloss:0.56545  test-mlogloss:1.99272
[26]    train-mlogloss:0.55028  test-mlogloss:2.01293
[27]    train-mlogloss:0.53299  test-mlogloss:2.03562
[28]    train-mlogloss:0.51936  test-mlogloss:2.05476
[29]    train-mlogloss:0.50527  test-mlogloss:2.07691
F1 Score: 0.44452154195011334
Precision: 0.4178171697179614
Recall: 0.536

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.355s
user    0m19.921s
sys     0m0.629s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

## Playing --max_depth, --feature fasttext for LONG

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --num_r
ound 30 --eval f1 --max_depth 5
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.13843  test-mlogloss:2.17647
[1]     train-mlogloss:2.01418  test-mlogloss:2.08254
[2]     train-mlogloss:1.91370  test-mlogloss:2.01425
[3]     train-mlogloss:1.83033  test-mlogloss:1.96011
[4]     train-mlogloss:1.76027  test-mlogloss:1.91820
[5]     train-mlogloss:1.69962  test-mlogloss:1.88181
[6]     train-mlogloss:1.64683  test-mlogloss:1.85355
[7]     train-mlogloss:1.59965  test-mlogloss:1.83029
[8]     train-mlogloss:1.55804  test-mlogloss:1.81034
[9]     train-mlogloss:1.52065  test-mlogloss:1.79531
[10]    train-mlogloss:1.48708  test-mlogloss:1.78304
[11]    train-mlogloss:1.45691  test-mlogloss:1.77265
[12]    train-mlogloss:1.42849  test-mlogloss:1.76510
[13]    train-mlogloss:1.40315  test-mlogloss:1.75897
[14]    train-mlogloss:1.37950  test-mlogloss:1.75428
[15]    train-mlogloss:1.35786  test-mlogloss:1.75206
[16]    train-mlogloss:1.33737  test-mlogloss:1.75033
[17]    train-mlogloss:1.31871  test-mlogloss:1.75041
[18]    train-mlogloss:1.30090  test-mlogloss:1.75117
[19]    train-mlogloss:1.28449  test-mlogloss:1.75325
[20]    train-mlogloss:1.26875  test-mlogloss:1.75472
[21]    train-mlogloss:1.25469  test-mlogloss:1.75704
[22]    train-mlogloss:1.24125  test-mlogloss:1.76073
[23]    train-mlogloss:1.22805  test-mlogloss:1.76433
[24]    train-mlogloss:1.21607  test-mlogloss:1.76871
[25]    train-mlogloss:1.20439  test-mlogloss:1.77305
[26]    train-mlogloss:1.19305  test-mlogloss:1.77757
[27]    train-mlogloss:1.18200  test-mlogloss:1.78252
[28]    train-mlogloss:1.17193  test-mlogloss:1.78833
[29]    train-mlogloss:1.16179  test-mlogloss:1.79439
F1 Score: 0.393030255798548
Precision: 0.6740295106596079
Recall: 0.539

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m5.568s
user    0m18.524s
sys     0m0.584s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 6
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.12937  test-mlogloss:2.17341
[1]     train-mlogloss:2.00003  test-mlogloss:2.08011
[2]     train-mlogloss:1.89537  test-mlogloss:2.01125
[3]     train-mlogloss:1.80789  test-mlogloss:1.95821
[4]     train-mlogloss:1.73056  test-mlogloss:1.91564
[5]     train-mlogloss:1.66484  test-mlogloss:1.88011
[6]     train-mlogloss:1.60643  test-mlogloss:1.85153
[7]     train-mlogloss:1.55452  test-mlogloss:1.82876
[8]     train-mlogloss:1.50764  test-mlogloss:1.80899
[9]     train-mlogloss:1.46549  test-mlogloss:1.79382
[10]    train-mlogloss:1.42746  test-mlogloss:1.78143
[11]    train-mlogloss:1.39245  test-mlogloss:1.77215
[12]    train-mlogloss:1.36068  test-mlogloss:1.76572
[13]    train-mlogloss:1.33211  test-mlogloss:1.76035
[14]    train-mlogloss:1.30519  test-mlogloss:1.75709
[15]    train-mlogloss:1.27961  test-mlogloss:1.75421
[16]    train-mlogloss:1.25561  test-mlogloss:1.75346
[17]    train-mlogloss:1.23383  test-mlogloss:1.75335
[18]    train-mlogloss:1.21318  test-mlogloss:1.75503
[19]    train-mlogloss:1.19321  test-mlogloss:1.75743
[20]    train-mlogloss:1.17496  test-mlogloss:1.76077
[21]    train-mlogloss:1.15674  test-mlogloss:1.76432
[22]    train-mlogloss:1.14150  test-mlogloss:1.76786
[23]    train-mlogloss:1.12576  test-mlogloss:1.77296
[24]    train-mlogloss:1.11002  test-mlogloss:1.77879
[25]    train-mlogloss:1.09471  test-mlogloss:1.78394
[26]    train-mlogloss:1.08109  test-mlogloss:1.78993
[27]    train-mlogloss:1.06792  test-mlogloss:1.79558
[28]    train-mlogloss:1.05595  test-mlogloss:1.80189
[29]    train-mlogloss:1.04458  test-mlogloss:1.80831
F1 Score: 0.3935795259361044
Precision: 0.5473009554140127
Recall: 0.533

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m6.106s
user    0m20.456s
sys     0m0.623s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 7
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.12047  test-mlogloss:2.17467
[1]     train-mlogloss:1.98383  test-mlogloss:2.08303
[2]     train-mlogloss:1.87101  test-mlogloss:2.01438
[3]     train-mlogloss:1.77819  test-mlogloss:1.95895
[4]     train-mlogloss:1.69595  test-mlogloss:1.91638
[5]     train-mlogloss:1.62487  test-mlogloss:1.88128
[6]     train-mlogloss:1.56242  test-mlogloss:1.85178
[7]     train-mlogloss:1.50605  test-mlogloss:1.82778
[8]     train-mlogloss:1.45513  test-mlogloss:1.80808
[9]     train-mlogloss:1.40867  test-mlogloss:1.79144
[10]    train-mlogloss:1.36702  test-mlogloss:1.77807
[11]    train-mlogloss:1.32911  test-mlogloss:1.76787
[12]    train-mlogloss:1.29324  test-mlogloss:1.75958
[13]    train-mlogloss:1.25925  test-mlogloss:1.75402
[14]    train-mlogloss:1.22878  test-mlogloss:1.75028
[15]    train-mlogloss:1.19905  test-mlogloss:1.74733
[16]    train-mlogloss:1.17252  test-mlogloss:1.74643
[17]    train-mlogloss:1.14709  test-mlogloss:1.74713
[18]    train-mlogloss:1.12376  test-mlogloss:1.74807
[19]    train-mlogloss:1.10195  test-mlogloss:1.74919
[20]    train-mlogloss:1.07905  test-mlogloss:1.75223
[21]    train-mlogloss:1.05781  test-mlogloss:1.75596
[22]    train-mlogloss:1.03854  test-mlogloss:1.76054
[23]    train-mlogloss:1.01963  test-mlogloss:1.76425
[24]    train-mlogloss:1.00280  test-mlogloss:1.76881
[25]    train-mlogloss:0.98651  test-mlogloss:1.77403
[26]    train-mlogloss:0.97121  test-mlogloss:1.77958
[27]    train-mlogloss:0.95781  test-mlogloss:1.78544
[28]    train-mlogloss:0.94230  test-mlogloss:1.79216
[29]    train-mlogloss:0.92978  test-mlogloss:1.79899
F1 Score: 0.3948210781190264
Precision: 0.5492180993520518
Recall: 0.528

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m6.781s
user    0m23.331s
sys     0m0.765s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 8
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.11841  test-mlogloss:2.17562
[1]     train-mlogloss:1.97381  test-mlogloss:2.08301
[2]     train-mlogloss:1.85773  test-mlogloss:2.01478
[3]     train-mlogloss:1.75769  test-mlogloss:1.96346
[4]     train-mlogloss:1.67116  test-mlogloss:1.91950
[5]     train-mlogloss:1.59409  test-mlogloss:1.88517
[6]     train-mlogloss:1.52618  test-mlogloss:1.85621
[7]     train-mlogloss:1.46588  test-mlogloss:1.83358
[8]     train-mlogloss:1.40845  test-mlogloss:1.81423
[9]     train-mlogloss:1.35606  test-mlogloss:1.79944
[10]    train-mlogloss:1.30942  test-mlogloss:1.78724
[11]    train-mlogloss:1.26703  test-mlogloss:1.77620
[12]    train-mlogloss:1.22699  test-mlogloss:1.76684
[13]    train-mlogloss:1.18901  test-mlogloss:1.76087
[14]    train-mlogloss:1.15480  test-mlogloss:1.75714
[15]    train-mlogloss:1.12359  test-mlogloss:1.75532
[16]    train-mlogloss:1.09120  test-mlogloss:1.75445
[17]    train-mlogloss:1.06274  test-mlogloss:1.75404
[18]    train-mlogloss:1.03652  test-mlogloss:1.75524
[19]    train-mlogloss:1.01052  test-mlogloss:1.75749
[20]    train-mlogloss:0.98753  test-mlogloss:1.75916
[21]    train-mlogloss:0.96534  test-mlogloss:1.76399
[22]    train-mlogloss:0.94368  test-mlogloss:1.76751
[23]    train-mlogloss:0.92258  test-mlogloss:1.77170
[24]    train-mlogloss:0.90424  test-mlogloss:1.77549
[25]    train-mlogloss:0.88562  test-mlogloss:1.78168
[26]    train-mlogloss:0.86647  test-mlogloss:1.78775
[27]    train-mlogloss:0.85103  test-mlogloss:1.79382
[28]    train-mlogloss:0.83515  test-mlogloss:1.79997
[29]    train-mlogloss:0.82128  test-mlogloss:1.80671
F1 Score: 0.39418313204877187
Precision: 0.5487711543164587
Recall: 0.526

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m7.674s
user    0m27.052s
sys     0m0.772s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 9
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.10421  test-mlogloss:2.17173
[1]     train-mlogloss:1.94874  test-mlogloss:2.07918
[2]     train-mlogloss:1.82035  test-mlogloss:2.00978
[3]     train-mlogloss:1.70934  test-mlogloss:1.95541
[4]     train-mlogloss:1.61329  test-mlogloss:1.91341
[5]     train-mlogloss:1.52846  test-mlogloss:1.87748
[6]     train-mlogloss:1.45308  test-mlogloss:1.84833
[7]     train-mlogloss:1.38707  test-mlogloss:1.82484
[8]     train-mlogloss:1.32584  test-mlogloss:1.80544
[9]     train-mlogloss:1.27088  test-mlogloss:1.78991
[10]    train-mlogloss:1.22026  test-mlogloss:1.77845
[11]    train-mlogloss:1.17311  test-mlogloss:1.76928
[12]    train-mlogloss:1.12939  test-mlogloss:1.76370
[13]    train-mlogloss:1.09029  test-mlogloss:1.75933
[14]    train-mlogloss:1.05268  test-mlogloss:1.75490
[15]    train-mlogloss:1.01936  test-mlogloss:1.75297
[16]    train-mlogloss:0.98635  test-mlogloss:1.75325
[17]    train-mlogloss:0.95635  test-mlogloss:1.75376
[18]    train-mlogloss:0.92858  test-mlogloss:1.75509
[19]    train-mlogloss:0.90046  test-mlogloss:1.75544
[20]    train-mlogloss:0.87556  test-mlogloss:1.75924
[21]    train-mlogloss:0.85113  test-mlogloss:1.76233
[22]    train-mlogloss:0.82604  test-mlogloss:1.76678
[23]    train-mlogloss:0.80577  test-mlogloss:1.77159
[24]    train-mlogloss:0.78480  test-mlogloss:1.77744
[25]    train-mlogloss:0.76492  test-mlogloss:1.78377
[26]    train-mlogloss:0.74544  test-mlogloss:1.79068
[27]    train-mlogloss:0.72853  test-mlogloss:1.79682
[28]    train-mlogloss:0.71224  test-mlogloss:1.80182
[29]    train-mlogloss:0.69568  test-mlogloss:1.80817
F1 Score: 0.3966549392533828
Precision: 0.5618978262838511
Recall: 0.52

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m8.640s
user    0m30.632s
sys     0m0.801s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 10
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.09253  test-mlogloss:2.17666
[1]     train-mlogloss:1.93319  test-mlogloss:2.08807
[2]     train-mlogloss:1.79789  test-mlogloss:2.02193
[3]     train-mlogloss:1.68322  test-mlogloss:1.96819
[4]     train-mlogloss:1.58232  test-mlogloss:1.92383
[5]     train-mlogloss:1.49094  test-mlogloss:1.88849
[6]     train-mlogloss:1.41176  test-mlogloss:1.85864
[7]     train-mlogloss:1.34067  test-mlogloss:1.83448
[8]     train-mlogloss:1.27559  test-mlogloss:1.81466
[9]     train-mlogloss:1.21726  test-mlogloss:1.79886
[10]    train-mlogloss:1.16364  test-mlogloss:1.78503
[11]    train-mlogloss:1.11457  test-mlogloss:1.77555
[12]    train-mlogloss:1.06910  test-mlogloss:1.76784
[13]    train-mlogloss:1.02608  test-mlogloss:1.76170
[14]    train-mlogloss:0.98389  test-mlogloss:1.75818
[15]    train-mlogloss:0.94428  test-mlogloss:1.75689
[16]    train-mlogloss:0.90891  test-mlogloss:1.75488
[17]    train-mlogloss:0.87660  test-mlogloss:1.75333
[18]    train-mlogloss:0.84647  test-mlogloss:1.75573
[19]    train-mlogloss:0.81713  test-mlogloss:1.75752
[20]    train-mlogloss:0.79170  test-mlogloss:1.75987
[21]    train-mlogloss:0.76530  test-mlogloss:1.76270
[22]    train-mlogloss:0.74209  test-mlogloss:1.76599
[23]    train-mlogloss:0.71949  test-mlogloss:1.77090
[24]    train-mlogloss:0.69706  test-mlogloss:1.77509
[25]    train-mlogloss:0.67674  test-mlogloss:1.77955
[26]    train-mlogloss:0.65520  test-mlogloss:1.78406
[27]    train-mlogloss:0.63664  test-mlogloss:1.78995
[28]    train-mlogloss:0.61990  test-mlogloss:1.79487
[29]    train-mlogloss:0.60463  test-mlogloss:1.80072
F1 Score: 0.3965058347449652
Precision: 0.5465399999999999
Recall: 0.52

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m9.987s
user    0m36.231s
sys     0m0.856s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

## Playing with --max_depth, --feature tfidf for LONG

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --num_roun
d 30 --eval f1 --max_depth 5
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.13191  test-mlogloss:2.17430
[1]     train-mlogloss:2.00450  test-mlogloss:2.08176
[2]     train-mlogloss:1.90319  test-mlogloss:2.01157
[3]     train-mlogloss:1.81984  test-mlogloss:1.95633
[4]     train-mlogloss:1.74956  test-mlogloss:1.91303
[5]     train-mlogloss:1.68922  test-mlogloss:1.87829
[6]     train-mlogloss:1.63708  test-mlogloss:1.84984
[7]     train-mlogloss:1.59128  test-mlogloss:1.82776
[8]     train-mlogloss:1.55076  test-mlogloss:1.80936
[9]     train-mlogloss:1.51498  test-mlogloss:1.79510
[10]    train-mlogloss:1.48297  test-mlogloss:1.78307
[11]    train-mlogloss:1.45390  test-mlogloss:1.77439
[12]    train-mlogloss:1.42814  test-mlogloss:1.76795
[13]    train-mlogloss:1.40465  test-mlogloss:1.76376
[14]    train-mlogloss:1.38306  test-mlogloss:1.76124
[15]    train-mlogloss:1.36361  test-mlogloss:1.76014
[16]    train-mlogloss:1.34570  test-mlogloss:1.75985
[17]    train-mlogloss:1.32950  test-mlogloss:1.76037
[18]    train-mlogloss:1.31444  test-mlogloss:1.76268
[19]    train-mlogloss:1.30086  test-mlogloss:1.76512
[20]    train-mlogloss:1.28777  test-mlogloss:1.76675
[21]    train-mlogloss:1.27570  test-mlogloss:1.77008
[22]    train-mlogloss:1.26474  test-mlogloss:1.77448
[23]    train-mlogloss:1.25413  test-mlogloss:1.77897
[24]    train-mlogloss:1.24454  test-mlogloss:1.78340
[25]    train-mlogloss:1.23579  test-mlogloss:1.78873
[26]    train-mlogloss:1.22732  test-mlogloss:1.79413
[27]    train-mlogloss:1.21899  test-mlogloss:1.79922
[28]    train-mlogloss:1.21154  test-mlogloss:1.80487
[29]    train-mlogloss:1.20425  test-mlogloss:1.81065
F1 Score: 0.39860323791278685
Precision: 0.4283000715307582
Recall: 0.535

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.122s
user    0m13.602s
sys     0m0.580s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --num_round 30 --eval f1 --max_depth 6
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.12946  test-mlogloss:2.17367
[1]     train-mlogloss:2.00021  test-mlogloss:2.08073
[2]     train-mlogloss:1.89729  test-mlogloss:2.01104
[3]     train-mlogloss:1.81263  test-mlogloss:1.95663
[4]     train-mlogloss:1.74133  test-mlogloss:1.91332
[5]     train-mlogloss:1.67966  test-mlogloss:1.87827
[6]     train-mlogloss:1.62641  test-mlogloss:1.85027
[7]     train-mlogloss:1.57942  test-mlogloss:1.82738
[8]     train-mlogloss:1.53793  test-mlogloss:1.80942
[9]     train-mlogloss:1.50116  test-mlogloss:1.79569
[10]    train-mlogloss:1.46858  test-mlogloss:1.78427
[11]    train-mlogloss:1.43915  test-mlogloss:1.77627
[12]    train-mlogloss:1.41194  test-mlogloss:1.77003
[13]    train-mlogloss:1.38762  test-mlogloss:1.76530
[14]    train-mlogloss:1.36513  test-mlogloss:1.76214
[15]    train-mlogloss:1.34535  test-mlogloss:1.76112
[16]    train-mlogloss:1.32705  test-mlogloss:1.76216
[17]    train-mlogloss:1.31008  test-mlogloss:1.76183
[18]    train-mlogloss:1.29418  test-mlogloss:1.76298
[19]    train-mlogloss:1.27949  test-mlogloss:1.76546
[20]    train-mlogloss:1.26622  test-mlogloss:1.76898
[21]    train-mlogloss:1.25395  test-mlogloss:1.77262
[22]    train-mlogloss:1.24196  test-mlogloss:1.77582
[23]    train-mlogloss:1.23125  test-mlogloss:1.78056
[24]    train-mlogloss:1.22111  test-mlogloss:1.78612
[25]    train-mlogloss:1.21133  test-mlogloss:1.79167
[26]    train-mlogloss:1.20282  test-mlogloss:1.79742
[27]    train-mlogloss:1.19390  test-mlogloss:1.80367
[28]    train-mlogloss:1.18614  test-mlogloss:1.80941
[29]    train-mlogloss:1.17850  test-mlogloss:1.81558
F1 Score: 0.4007500339443313
Precision: 0.3413717532467533
Recall: 0.534

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.365s
user    0m12.939s
sys     0m0.580s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --num_round 30 --eval f1 --max_depth 7
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.12721  test-mlogloss:2.17320
[1]     train-mlogloss:1.99602  test-mlogloss:2.08052
[2]     train-mlogloss:1.89164  test-mlogloss:2.01043
[3]     train-mlogloss:1.80612  test-mlogloss:1.95598
[4]     train-mlogloss:1.73341  test-mlogloss:1.91242
[5]     train-mlogloss:1.67094  test-mlogloss:1.87818
[6]     train-mlogloss:1.61659  test-mlogloss:1.85012
[7]     train-mlogloss:1.56895  test-mlogloss:1.82816
[8]     train-mlogloss:1.52678  test-mlogloss:1.81017
[9]     train-mlogloss:1.48886  test-mlogloss:1.79636
[10]    train-mlogloss:1.45497  test-mlogloss:1.78544
[11]    train-mlogloss:1.42496  test-mlogloss:1.77721
[12]    train-mlogloss:1.39737  test-mlogloss:1.77080
[13]    train-mlogloss:1.37265  test-mlogloss:1.76662
[14]    train-mlogloss:1.35000  test-mlogloss:1.76342
[15]    train-mlogloss:1.32923  test-mlogloss:1.76190
[16]    train-mlogloss:1.31015  test-mlogloss:1.76251
[17]    train-mlogloss:1.29265  test-mlogloss:1.76363
[18]    train-mlogloss:1.27629  test-mlogloss:1.76546
[19]    train-mlogloss:1.26110  test-mlogloss:1.76846
[20]    train-mlogloss:1.24699  test-mlogloss:1.77183
[21]    train-mlogloss:1.23416  test-mlogloss:1.77566
[22]    train-mlogloss:1.22219  test-mlogloss:1.78009
[23]    train-mlogloss:1.21020  test-mlogloss:1.78481
[24]    train-mlogloss:1.19951  test-mlogloss:1.79016
[25]    train-mlogloss:1.18957  test-mlogloss:1.79550
[26]    train-mlogloss:1.17968  test-mlogloss:1.80089
[27]    train-mlogloss:1.17092  test-mlogloss:1.80772
[28]    train-mlogloss:1.16277  test-mlogloss:1.81485
[29]    train-mlogloss:1.15453  test-mlogloss:1.82130
F1 Score: 0.39943592769079495
Precision: 0.3265217391304348
Recall: 0.532

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.710s
user    0m15.597s
sys     0m0.608s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --num_round 30 --eval f1 --max_depth 8
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.12506  test-mlogloss:2.17200
[1]     train-mlogloss:1.99218  test-mlogloss:2.07936
[2]     train-mlogloss:1.88683  test-mlogloss:2.00953
[3]     train-mlogloss:1.79974  test-mlogloss:1.95513
[4]     train-mlogloss:1.72603  test-mlogloss:1.91173
[5]     train-mlogloss:1.66225  test-mlogloss:1.87809
[6]     train-mlogloss:1.60722  test-mlogloss:1.85018
[7]     train-mlogloss:1.55898  test-mlogloss:1.82838
[8]     train-mlogloss:1.51561  test-mlogloss:1.81045
[9]     train-mlogloss:1.47760  test-mlogloss:1.79656
[10]    train-mlogloss:1.44282  test-mlogloss:1.78533
[11]    train-mlogloss:1.41168  test-mlogloss:1.77727
[12]    train-mlogloss:1.38390  test-mlogloss:1.77151
[13]    train-mlogloss:1.35802  test-mlogloss:1.76796
[14]    train-mlogloss:1.33486  test-mlogloss:1.76557
[15]    train-mlogloss:1.31306  test-mlogloss:1.76388
[16]    train-mlogloss:1.29315  test-mlogloss:1.76401
[17]    train-mlogloss:1.27480  test-mlogloss:1.76557
[18]    train-mlogloss:1.25775  test-mlogloss:1.76775
[19]    train-mlogloss:1.24237  test-mlogloss:1.77099
[20]    train-mlogloss:1.22695  test-mlogloss:1.77428
[21]    train-mlogloss:1.21364  test-mlogloss:1.77858
[22]    train-mlogloss:1.20073  test-mlogloss:1.78394
[23]    train-mlogloss:1.18923  test-mlogloss:1.78921
[24]    train-mlogloss:1.17763  test-mlogloss:1.79514
[25]    train-mlogloss:1.16776  test-mlogloss:1.80093
[26]    train-mlogloss:1.15805  test-mlogloss:1.80673
[27]    train-mlogloss:1.14846  test-mlogloss:1.81293
[28]    train-mlogloss:1.13966  test-mlogloss:1.81996
[29]    train-mlogloss:1.13094  test-mlogloss:1.82671
F1 Score: 0.4014105208197363
Precision: 0.3290607843137255
Recall: 0.533

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m3.116s
user    0m16.128s
sys     0m0.671s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --num_round 30 --eval f1 --max_depth 9
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.12312  test-mlogloss:2.17244
[1]     train-mlogloss:1.98885  test-mlogloss:2.07945
[2]     train-mlogloss:1.88244  test-mlogloss:2.00904
[3]     train-mlogloss:1.79404  test-mlogloss:1.95541
[4]     train-mlogloss:1.71862  test-mlogloss:1.91225
[5]     train-mlogloss:1.65441  test-mlogloss:1.87744
[6]     train-mlogloss:1.59802  test-mlogloss:1.84988
[7]     train-mlogloss:1.54834  test-mlogloss:1.82791
[8]     train-mlogloss:1.50431  test-mlogloss:1.81037
[9]     train-mlogloss:1.46495  test-mlogloss:1.79675
[10]    train-mlogloss:1.42937  test-mlogloss:1.78649
[11]    train-mlogloss:1.39776  test-mlogloss:1.77850
[12]    train-mlogloss:1.36905  test-mlogloss:1.77321
[13]    train-mlogloss:1.34290  test-mlogloss:1.76909
[14]    train-mlogloss:1.31937  test-mlogloss:1.76686
[15]    train-mlogloss:1.29689  test-mlogloss:1.76564
[16]    train-mlogloss:1.27571  test-mlogloss:1.76666
[17]    train-mlogloss:1.25703  test-mlogloss:1.76830
[18]    train-mlogloss:1.24003  test-mlogloss:1.77111
[19]    train-mlogloss:1.22365  test-mlogloss:1.77401
[20]    train-mlogloss:1.20800  test-mlogloss:1.77745
[21]    train-mlogloss:1.19407  test-mlogloss:1.78266
[22]    train-mlogloss:1.18118  test-mlogloss:1.78775
[23]    train-mlogloss:1.16928  test-mlogloss:1.79373
[24]    train-mlogloss:1.15790  test-mlogloss:1.79967
[25]    train-mlogloss:1.14723  test-mlogloss:1.80568
[26]    train-mlogloss:1.13731  test-mlogloss:1.81207
[27]    train-mlogloss:1.12739  test-mlogloss:1.81855
[28]    train-mlogloss:1.11809  test-mlogloss:1.82495
[29]    train-mlogloss:1.10934  test-mlogloss:1.83273
F1 Score: 0.4009940809470485
Precision: 0.3292466083150985
Recall: 0.531

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m3.385s
user    0m17.625s
sys     0m0.659s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --num_round 30 --eval f1 --max_depth 10
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.12137  test-mlogloss:2.17346
[1]     train-mlogloss:1.98567  test-mlogloss:2.07978
[2]     train-mlogloss:1.87727  test-mlogloss:2.00907
[3]     train-mlogloss:1.78770  test-mlogloss:1.95417
[4]     train-mlogloss:1.71171  test-mlogloss:1.91107
[5]     train-mlogloss:1.64672  test-mlogloss:1.87625
[6]     train-mlogloss:1.58894  test-mlogloss:1.84873
[7]     train-mlogloss:1.53858  test-mlogloss:1.82731
[8]     train-mlogloss:1.49327  test-mlogloss:1.80946
[9]     train-mlogloss:1.45359  test-mlogloss:1.79563
[10]    train-mlogloss:1.41721  test-mlogloss:1.78547
[11]    train-mlogloss:1.38472  test-mlogloss:1.77757
[12]    train-mlogloss:1.35550  test-mlogloss:1.77244
[13]    train-mlogloss:1.32876  test-mlogloss:1.76937
[14]    train-mlogloss:1.30457  test-mlogloss:1.76740
[15]    train-mlogloss:1.28208  test-mlogloss:1.76773
[16]    train-mlogloss:1.26126  test-mlogloss:1.76782
[17]    train-mlogloss:1.24191  test-mlogloss:1.76912
[18]    train-mlogloss:1.22421  test-mlogloss:1.77182
[19]    train-mlogloss:1.20733  test-mlogloss:1.77458
[20]    train-mlogloss:1.19169  test-mlogloss:1.77890
[21]    train-mlogloss:1.17758  test-mlogloss:1.78406
[22]    train-mlogloss:1.16333  test-mlogloss:1.78965
[23]    train-mlogloss:1.15026  test-mlogloss:1.79523
[24]    train-mlogloss:1.13868  test-mlogloss:1.80107
[25]    train-mlogloss:1.12802  test-mlogloss:1.80798
[26]    train-mlogloss:1.11714  test-mlogloss:1.81420
[27]    train-mlogloss:1.10768  test-mlogloss:1.82034
[28]    train-mlogloss:1.09755  test-mlogloss:1.82730
[29]    train-mlogloss:1.08845  test-mlogloss:1.83396
F1 Score: 0.4019366092071761
Precision: 0.33118729281767956
Recall: 0.529

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m3.636s
user    0m18.601s
sys     0m0.752s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

## Playing with --max_depth, --feature word2vec for LONG 

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --num_r
ound 30 --eval f1 --max_depth 5
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.13745  test-mlogloss:2.17427
[1]     train-mlogloss:2.01362  test-mlogloss:2.08078
[2]     train-mlogloss:1.91307  test-mlogloss:2.01300
[3]     train-mlogloss:1.82895  test-mlogloss:1.95992
[4]     train-mlogloss:1.75785  test-mlogloss:1.91662
[5]     train-mlogloss:1.69584  test-mlogloss:1.88136
[6]     train-mlogloss:1.64141  test-mlogloss:1.85241
[7]     train-mlogloss:1.59341  test-mlogloss:1.82953
[8]     train-mlogloss:1.55035  test-mlogloss:1.81067
[9]     train-mlogloss:1.51263  test-mlogloss:1.79586
[10]    train-mlogloss:1.47854  test-mlogloss:1.78527
[11]    train-mlogloss:1.44749  test-mlogloss:1.77510
[12]    train-mlogloss:1.41883  test-mlogloss:1.76850
[13]    train-mlogloss:1.39264  test-mlogloss:1.76320
[14]    train-mlogloss:1.36851  test-mlogloss:1.75991
[15]    train-mlogloss:1.34690  test-mlogloss:1.75846
[16]    train-mlogloss:1.32628  test-mlogloss:1.75894
[17]    train-mlogloss:1.30748  test-mlogloss:1.76087
[18]    train-mlogloss:1.28998  test-mlogloss:1.76262
[19]    train-mlogloss:1.27304  test-mlogloss:1.76589
[20]    train-mlogloss:1.25761  test-mlogloss:1.76960
[21]    train-mlogloss:1.24224  test-mlogloss:1.77422
[22]    train-mlogloss:1.22854  test-mlogloss:1.77957
[23]    train-mlogloss:1.21544  test-mlogloss:1.78608
[24]    train-mlogloss:1.20274  test-mlogloss:1.79245
[25]    train-mlogloss:1.19124  test-mlogloss:1.79900
[26]    train-mlogloss:1.17953  test-mlogloss:1.80600
[27]    train-mlogloss:1.16955  test-mlogloss:1.81255
[28]    train-mlogloss:1.15856  test-mlogloss:1.81834
[29]    train-mlogloss:1.14959  test-mlogloss:1.82586
F1 Score: 0.3945659617691922
Precision: 0.6771237993051298
Recall: 0.528

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m3.080s
user    0m14.286s
sys     0m0.497s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --num_round 30 --eval f1 --max_depth 6
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.12767  test-mlogloss:2.17427
[1]     train-mlogloss:1.99570  test-mlogloss:2.08355
[2]     train-mlogloss:1.88886  test-mlogloss:2.01578
[3]     train-mlogloss:1.79849  test-mlogloss:1.96333
[4]     train-mlogloss:1.72196  test-mlogloss:1.92093
[5]     train-mlogloss:1.65380  test-mlogloss:1.88638
[6]     train-mlogloss:1.59535  test-mlogloss:1.85964
[7]     train-mlogloss:1.54254  test-mlogloss:1.83804
[8]     train-mlogloss:1.49574  test-mlogloss:1.82013
[9]     train-mlogloss:1.45381  test-mlogloss:1.80656
[10]    train-mlogloss:1.41557  test-mlogloss:1.79477
[11]    train-mlogloss:1.38138  test-mlogloss:1.78667
[12]    train-mlogloss:1.35015  test-mlogloss:1.78125
[13]    train-mlogloss:1.32132  test-mlogloss:1.77706
[14]    train-mlogloss:1.29404  test-mlogloss:1.77440
[15]    train-mlogloss:1.26975  test-mlogloss:1.77390
[16]    train-mlogloss:1.24663  test-mlogloss:1.77410
[17]    train-mlogloss:1.22515  test-mlogloss:1.77603
[18]    train-mlogloss:1.20520  test-mlogloss:1.77806
[19]    train-mlogloss:1.18566  test-mlogloss:1.78127
[20]    train-mlogloss:1.16843  test-mlogloss:1.78511
[21]    train-mlogloss:1.15152  test-mlogloss:1.78972
[22]    train-mlogloss:1.13514  test-mlogloss:1.79359
[23]    train-mlogloss:1.12046  test-mlogloss:1.79890
[24]    train-mlogloss:1.10563  test-mlogloss:1.80357
[25]    train-mlogloss:1.09108  test-mlogloss:1.81034
[26]    train-mlogloss:1.07747  test-mlogloss:1.81649
[27]    train-mlogloss:1.06511  test-mlogloss:1.82383
[28]    train-mlogloss:1.05118  test-mlogloss:1.83151
[29]    train-mlogloss:1.03932  test-mlogloss:1.83787
F1 Score: 0.39244559746473623
Precision: 0.6801268364710225
Recall: 0.517

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m3.580s
user    0m16.281s
sys     0m0.497s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --num_round 30 --eval f1 --max_depth 7
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.12355  test-mlogloss:2.17463
[1]     train-mlogloss:1.98504  test-mlogloss:2.08454
[2]     train-mlogloss:1.87190  test-mlogloss:2.01531
[3]     train-mlogloss:1.77578  test-mlogloss:1.96240
[4]     train-mlogloss:1.69284  test-mlogloss:1.92007
[5]     train-mlogloss:1.61997  test-mlogloss:1.88681
[6]     train-mlogloss:1.55536  test-mlogloss:1.86129
[7]     train-mlogloss:1.49896  test-mlogloss:1.83954
[8]     train-mlogloss:1.44711  test-mlogloss:1.82195
[9]     train-mlogloss:1.39977  test-mlogloss:1.80857
[10]    train-mlogloss:1.35706  test-mlogloss:1.79772
[11]    train-mlogloss:1.31835  test-mlogloss:1.79006
[12]    train-mlogloss:1.28363  test-mlogloss:1.78376
[13]    train-mlogloss:1.25061  test-mlogloss:1.77854
[14]    train-mlogloss:1.22009  test-mlogloss:1.77554
[15]    train-mlogloss:1.19166  test-mlogloss:1.77487
[16]    train-mlogloss:1.16338  test-mlogloss:1.77417
[17]    train-mlogloss:1.13767  test-mlogloss:1.77440
[18]    train-mlogloss:1.11377  test-mlogloss:1.77712
[19]    train-mlogloss:1.09074  test-mlogloss:1.78066
[20]    train-mlogloss:1.06984  test-mlogloss:1.78409
[21]    train-mlogloss:1.04995  test-mlogloss:1.78760
[22]    train-mlogloss:1.03099  test-mlogloss:1.79165
[23]    train-mlogloss:1.01200  test-mlogloss:1.79697
[24]    train-mlogloss:0.99434  test-mlogloss:1.80336
[25]    train-mlogloss:0.97768  test-mlogloss:1.80928
[26]    train-mlogloss:0.96092  test-mlogloss:1.81692
[27]    train-mlogloss:0.94657  test-mlogloss:1.82531
[28]    train-mlogloss:0.92944  test-mlogloss:1.83263
[29]    train-mlogloss:0.91540  test-mlogloss:1.84054
F1 Score: 0.3960560508827472
Precision: 0.5909617800620004
Recall: 0.522

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.282s
user    0m18.854s
sys     0m0.577s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --num_round 30 --eval f1 --max_depth 8
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.11427  test-mlogloss:2.17589
[1]     train-mlogloss:1.96828  test-mlogloss:2.08550
[2]     train-mlogloss:1.84742  test-mlogloss:2.01737
[3]     train-mlogloss:1.74715  test-mlogloss:1.96238
[4]     train-mlogloss:1.65942  test-mlogloss:1.91938
[5]     train-mlogloss:1.58332  test-mlogloss:1.88253
[6]     train-mlogloss:1.51411  test-mlogloss:1.85428
[7]     train-mlogloss:1.45237  test-mlogloss:1.83192
[8]     train-mlogloss:1.39670  test-mlogloss:1.81285
[9]     train-mlogloss:1.34640  test-mlogloss:1.79993
[10]    train-mlogloss:1.30068  test-mlogloss:1.78864
[11]    train-mlogloss:1.25850  test-mlogloss:1.77978
[12]    train-mlogloss:1.21901  test-mlogloss:1.77329
[13]    train-mlogloss:1.17954  test-mlogloss:1.76821
[14]    train-mlogloss:1.14557  test-mlogloss:1.76677
[15]    train-mlogloss:1.11352  test-mlogloss:1.76669
[16]    train-mlogloss:1.08413  test-mlogloss:1.76652
[17]    train-mlogloss:1.05556  test-mlogloss:1.76682
[18]    train-mlogloss:1.03022  test-mlogloss:1.76837
[19]    train-mlogloss:1.00703  test-mlogloss:1.77183
[20]    train-mlogloss:0.98353  test-mlogloss:1.77504
[21]    train-mlogloss:0.96132  test-mlogloss:1.77855
[22]    train-mlogloss:0.93901  test-mlogloss:1.78393
[23]    train-mlogloss:0.92034  test-mlogloss:1.78838
[24]    train-mlogloss:0.90033  test-mlogloss:1.79332
[25]    train-mlogloss:0.88333  test-mlogloss:1.80089
[26]    train-mlogloss:0.86463  test-mlogloss:1.80883
[27]    train-mlogloss:0.84895  test-mlogloss:1.81630
[28]    train-mlogloss:0.83249  test-mlogloss:1.82414
[29]    train-mlogloss:0.81816  test-mlogloss:1.83159
F1 Score: 0.39728501121848925
Precision: 0.593852885525071
Recall: 0.524

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m5.039s
user    0m21.636s
sys     0m0.569s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --num_round 30 --eval f1 --max_depth 9
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.09877  test-mlogloss:2.18136
[1]     train-mlogloss:1.94197  test-mlogloss:2.09264
[2]     train-mlogloss:1.81043  test-mlogloss:2.02389
[3]     train-mlogloss:1.69867  test-mlogloss:1.96978
[4]     train-mlogloss:1.60368  test-mlogloss:1.92831
[5]     train-mlogloss:1.51769  test-mlogloss:1.89574
[6]     train-mlogloss:1.44109  test-mlogloss:1.86714
[7]     train-mlogloss:1.37458  test-mlogloss:1.84473
[8]     train-mlogloss:1.31347  test-mlogloss:1.82787
[9]     train-mlogloss:1.25837  test-mlogloss:1.81570
[10]    train-mlogloss:1.20716  test-mlogloss:1.80517
[11]    train-mlogloss:1.15674  test-mlogloss:1.79572
[12]    train-mlogloss:1.11145  test-mlogloss:1.79004
[13]    train-mlogloss:1.07239  test-mlogloss:1.78573
[14]    train-mlogloss:1.03589  test-mlogloss:1.78274
[15]    train-mlogloss:1.00054  test-mlogloss:1.78090
[16]    train-mlogloss:0.97058  test-mlogloss:1.78117
[17]    train-mlogloss:0.93980  test-mlogloss:1.78223
[18]    train-mlogloss:0.91040  test-mlogloss:1.78407
[19]    train-mlogloss:0.88315  test-mlogloss:1.78788
[20]    train-mlogloss:0.85800  test-mlogloss:1.79181
[21]    train-mlogloss:0.83431  test-mlogloss:1.79680
[22]    train-mlogloss:0.81087  test-mlogloss:1.80229
[23]    train-mlogloss:0.78835  test-mlogloss:1.80806
[24]    train-mlogloss:0.76822  test-mlogloss:1.81550
[25]    train-mlogloss:0.74828  test-mlogloss:1.82270
[26]    train-mlogloss:0.72932  test-mlogloss:1.82976
[27]    train-mlogloss:0.71169  test-mlogloss:1.83803
[28]    train-mlogloss:0.69423  test-mlogloss:1.84559
[29]    train-mlogloss:0.67837  test-mlogloss:1.85390
F1 Score: 0.39108373664346385
Precision: 0.6575750480788998
Recall: 0.508

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m6.039s
user    0m25.860s
sys     0m0.591s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --num_round 30 --eval f1 --max_depth 10
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.09078  test-mlogloss:2.18234
[1]     train-mlogloss:1.92595  test-mlogloss:2.09505
[2]     train-mlogloss:1.78909  test-mlogloss:2.02686
[3]     train-mlogloss:1.67183  test-mlogloss:1.97210
[4]     train-mlogloss:1.57235  test-mlogloss:1.93068
[5]     train-mlogloss:1.48414  test-mlogloss:1.89527
[6]     train-mlogloss:1.40345  test-mlogloss:1.86759
[7]     train-mlogloss:1.32839  test-mlogloss:1.84595
[8]     train-mlogloss:1.26248  test-mlogloss:1.82746
[9]     train-mlogloss:1.20353  test-mlogloss:1.81294
[10]    train-mlogloss:1.15013  test-mlogloss:1.80156
[11]    train-mlogloss:1.10118  test-mlogloss:1.79140
[12]    train-mlogloss:1.05577  test-mlogloss:1.78470
[13]    train-mlogloss:1.01330  test-mlogloss:1.78017
[14]    train-mlogloss:0.97324  test-mlogloss:1.77722
[15]    train-mlogloss:0.93461  test-mlogloss:1.77637
[16]    train-mlogloss:0.90066  test-mlogloss:1.77509
[17]    train-mlogloss:0.86681  test-mlogloss:1.77544
[18]    train-mlogloss:0.83641  test-mlogloss:1.77707
[19]    train-mlogloss:0.80628  test-mlogloss:1.77806
[20]    train-mlogloss:0.77693  test-mlogloss:1.78117
[21]    train-mlogloss:0.75086  test-mlogloss:1.78617
[22]    train-mlogloss:0.72537  test-mlogloss:1.79054
[23]    train-mlogloss:0.70155  test-mlogloss:1.79652
[24]    train-mlogloss:0.67733  test-mlogloss:1.80292
[25]    train-mlogloss:0.65480  test-mlogloss:1.80939
[26]    train-mlogloss:0.63357  test-mlogloss:1.81578
[27]    train-mlogloss:0.61396  test-mlogloss:1.82477
[28]    train-mlogloss:0.59548  test-mlogloss:1.83324
[29]    train-mlogloss:0.57966  test-mlogloss:1.84275
F1 Score: 0.39134705558036437
Precision: 0.6632175794860627
Recall: 0.513

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m7.199s
user    0m31.112s
sys     0m0.725s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

## Playing with --learning_rate, --feature fasttext for LONG

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --num_r
ound 30 --eval f1 --max_depth 5 --learning_rate 1
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:1.37821  test-mlogloss:1.76909
[1]     train-mlogloss:1.21337  test-mlogloss:1.92748
[2]     train-mlogloss:1.13071  test-mlogloss:2.01079
[3]     train-mlogloss:1.07293  test-mlogloss:2.07527
[4]     train-mlogloss:1.00931  test-mlogloss:2.12408
[5]     train-mlogloss:0.96631  test-mlogloss:2.18636
[6]     train-mlogloss:0.92114  test-mlogloss:2.23268
[7]     train-mlogloss:0.87301  test-mlogloss:2.28086
[8]     train-mlogloss:0.82664  test-mlogloss:2.31965
[9]     train-mlogloss:0.78937  test-mlogloss:2.35039
[10]    train-mlogloss:0.74870  test-mlogloss:2.39125
[11]    train-mlogloss:0.71325  test-mlogloss:2.42634
[12]    train-mlogloss:0.68284  test-mlogloss:2.47501
[13]    train-mlogloss:0.65474  test-mlogloss:2.52175
[14]    train-mlogloss:0.63038  test-mlogloss:2.53910
[15]    train-mlogloss:0.59680  test-mlogloss:2.56402
[16]    train-mlogloss:0.56882  test-mlogloss:2.60435
[17]    train-mlogloss:0.54103  test-mlogloss:2.64505
[18]    train-mlogloss:0.51934  test-mlogloss:2.68053
[19]    train-mlogloss:0.49688  test-mlogloss:2.70299
[20]    train-mlogloss:0.48030  test-mlogloss:2.71996
[21]    train-mlogloss:0.45483  test-mlogloss:2.73830
[22]    train-mlogloss:0.43297  test-mlogloss:2.77615
[23]    train-mlogloss:0.41370  test-mlogloss:2.80024
[24]    train-mlogloss:0.39639  test-mlogloss:2.80926
[25]    train-mlogloss:0.38030  test-mlogloss:2.81793
[26]    train-mlogloss:0.36723  test-mlogloss:2.83001
[27]    train-mlogloss:0.35171  test-mlogloss:2.84990
[28]    train-mlogloss:0.33942  test-mlogloss:2.88471
[29]    train-mlogloss:0.32903  test-mlogloss:2.90190
F1 Score: 0.3951004497603237
Precision: 0.3665202995323913
Recall: 0.472

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m5.668s
user    0m18.549s
sys     0m0.583s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 5 --learning_rate 2
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:1.84158  test-mlogloss:2.51927
[1]     train-mlogloss:10.84782 test-mlogloss:12.40324
[2]     train-mlogloss:13.28325 test-mlogloss:14.14012
[3]     train-mlogloss:30.13175 test-mlogloss:33.12038
[4]     train-mlogloss:17.03211 test-mlogloss:17.58765
[5]     train-mlogloss:31.35119 test-mlogloss:33.93096
[6]     train-mlogloss:28.25452 test-mlogloss:27.85303
[7]     train-mlogloss:17.26610 test-mlogloss:17.27860
[8]     train-mlogloss:17.27628 test-mlogloss:17.31671
[9]     train-mlogloss:17.26706 test-mlogloss:17.17723
[10]    train-mlogloss:17.39294 test-mlogloss:17.72622
[11]    train-mlogloss:17.37133 test-mlogloss:17.72070
[12]    train-mlogloss:19.43767 test-mlogloss:19.97604
[13]    train-mlogloss:29.25858 test-mlogloss:29.51506
[14]    train-mlogloss:17.88091 test-mlogloss:18.25012
[15]    train-mlogloss:23.23587 test-mlogloss:22.88461
[16]    train-mlogloss:21.96703 test-mlogloss:22.38505
[17]    train-mlogloss:24.82061 test-mlogloss:25.02862
[18]    train-mlogloss:23.10106 test-mlogloss:24.26482
[19]    train-mlogloss:22.70320 test-mlogloss:22.93467
[20]    train-mlogloss:23.31413 test-mlogloss:24.69524
[21]    train-mlogloss:21.07594 test-mlogloss:21.76952
[22]    train-mlogloss:27.53195 test-mlogloss:29.01885
[23]    train-mlogloss:20.51909 test-mlogloss:21.41724
[24]    train-mlogloss:26.58934 test-mlogloss:27.69962
[25]    train-mlogloss:20.61078 test-mlogloss:21.68769
[26]    train-mlogloss:25.95382 test-mlogloss:26.96131
[27]    train-mlogloss:21.00123 test-mlogloss:22.01609
[28]    train-mlogloss:22.84211 test-mlogloss:24.12767
[29]    train-mlogloss:22.13761 test-mlogloss:23.28390
./hs-xgboost.py:91: RuntimeWarning: overflow encountered in exp
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
./hs-xgboost.py:91: RuntimeWarning: invalid value encountered in divide
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
F1 Score: 0.3651233299081165
Precision: 0.35210400191861824
Recall: 0.432

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m5.051s
user    0m17.423s
sys     0m0.675s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 5 --learning_rate 3
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.60503  test-mlogloss:3.76636
[1]     train-mlogloss:30.81171 test-mlogloss:32.46745
[2]     train-mlogloss:29.30493 test-mlogloss:34.16004
[3]     train-mlogloss:16.22520 test-mlogloss:16.61545
[4]     train-mlogloss:16.22520 test-mlogloss:16.61545
[5]     train-mlogloss:16.22520 test-mlogloss:16.61545
[6]     train-mlogloss:16.22520 test-mlogloss:16.61545
[7]     train-mlogloss:16.22520 test-mlogloss:16.61545
[8]     train-mlogloss:16.22520 test-mlogloss:16.61545
[9]     train-mlogloss:16.22520 test-mlogloss:16.61545
[10]    train-mlogloss:16.22520 test-mlogloss:16.61545
[11]    train-mlogloss:16.22520 test-mlogloss:16.61545
[12]    train-mlogloss:16.22520 test-mlogloss:16.61545
[13]    train-mlogloss:16.22520 test-mlogloss:16.61545
[14]    train-mlogloss:16.22520 test-mlogloss:16.61545
[15]    train-mlogloss:16.22520 test-mlogloss:16.61545
[16]    train-mlogloss:16.22520 test-mlogloss:16.61545
[17]    train-mlogloss:16.22520 test-mlogloss:16.61545
[18]    train-mlogloss:16.22520 test-mlogloss:16.61545
[19]    train-mlogloss:16.22520 test-mlogloss:16.61545
[20]    train-mlogloss:16.22520 test-mlogloss:16.61545
[21]    train-mlogloss:16.22520 test-mlogloss:16.61545
[22]    train-mlogloss:16.22520 test-mlogloss:16.61545
[23]    train-mlogloss:16.22520 test-mlogloss:16.61545
[24]    train-mlogloss:16.22520 test-mlogloss:16.61545
[25]    train-mlogloss:16.22520 test-mlogloss:16.61545
[26]    train-mlogloss:16.22520 test-mlogloss:16.61545
[27]    train-mlogloss:16.22520 test-mlogloss:16.61545
[28]    train-mlogloss:16.22520 test-mlogloss:16.61545
[29]    train-mlogloss:16.22520 test-mlogloss:16.61545
./hs-xgboost.py:91: RuntimeWarning: overflow encountered in exp
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
./hs-xgboost.py:91: RuntimeWarning: invalid value encountered in divide
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
F1 Score: 0.3891555842479019
Precision: 0.7524010000000001
Recall: 0.549

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.934s
user    0m16.057s
sys     0m0.609s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 5 --learning_rate 4
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:3.44993  test-mlogloss:4.96936
[1]     train-mlogloss:34.28008 test-mlogloss:34.37594
[2]     train-mlogloss:31.37025 test-mlogloss:34.69940
[3]     train-mlogloss:34.36473 test-mlogloss:34.61781
[4]     train-mlogloss:33.70192 test-mlogloss:34.49271
[5]     train-mlogloss:16.22520 test-mlogloss:16.61545
[6]     train-mlogloss:16.22520 test-mlogloss:16.61545
[7]     train-mlogloss:16.22520 test-mlogloss:16.61545
[8]     train-mlogloss:16.22520 test-mlogloss:16.61545
[9]     train-mlogloss:16.22520 test-mlogloss:16.61545
[10]    train-mlogloss:16.22520 test-mlogloss:16.61545
[11]    train-mlogloss:16.22520 test-mlogloss:16.61545
[12]    train-mlogloss:16.22520 test-mlogloss:16.61545
[13]    train-mlogloss:16.22520 test-mlogloss:16.61545
[14]    train-mlogloss:16.22520 test-mlogloss:16.61545
[15]    train-mlogloss:16.22520 test-mlogloss:16.61545
[16]    train-mlogloss:16.22520 test-mlogloss:16.61545
[17]    train-mlogloss:16.22520 test-mlogloss:16.61545
[18]    train-mlogloss:16.22520 test-mlogloss:16.61545
[19]    train-mlogloss:16.22520 test-mlogloss:16.61545
[20]    train-mlogloss:16.22520 test-mlogloss:16.61545
[21]    train-mlogloss:16.22520 test-mlogloss:16.61545
[22]    train-mlogloss:16.22520 test-mlogloss:16.61545
[23]    train-mlogloss:16.22520 test-mlogloss:16.61545
[24]    train-mlogloss:16.22520 test-mlogloss:16.61545
[25]    train-mlogloss:16.22520 test-mlogloss:16.61545
[26]    train-mlogloss:16.22520 test-mlogloss:16.61545
[27]    train-mlogloss:16.22520 test-mlogloss:16.61545
[28]    train-mlogloss:16.22520 test-mlogloss:16.61545
[29]    train-mlogloss:16.22520 test-mlogloss:16.61545
./hs-xgboost.py:91: RuntimeWarning: overflow encountered in exp
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
./hs-xgboost.py:91: RuntimeWarning: invalid value encountered in divide
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
F1 Score: 0.3891555842479019
Precision: 0.7524010000000001
Recall: 0.549

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.805s
user    0m15.453s
sys     0m0.675s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 5 --learning_rate 5
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:4.37374  test-mlogloss:6.06265
[1]     train-mlogloss:34.96640 test-mlogloss:33.50482
[2]     train-mlogloss:34.96640 test-mlogloss:33.50482
[3]     train-mlogloss:34.96640 test-mlogloss:33.50482
[4]     train-mlogloss:34.96640 test-mlogloss:33.50482
[5]     train-mlogloss:34.96640 test-mlogloss:33.50482
[6]     train-mlogloss:34.96640 test-mlogloss:33.50482
[7]     train-mlogloss:34.96640 test-mlogloss:33.50482
[8]     train-mlogloss:34.96640 test-mlogloss:33.50482
[9]     train-mlogloss:34.96640 test-mlogloss:33.50482
[10]    train-mlogloss:34.96640 test-mlogloss:33.50482
[11]    train-mlogloss:34.96640 test-mlogloss:33.50482
[12]    train-mlogloss:34.96640 test-mlogloss:33.50482
[13]    train-mlogloss:34.96640 test-mlogloss:33.50482
[14]    train-mlogloss:34.96640 test-mlogloss:33.50482
[15]    train-mlogloss:34.96640 test-mlogloss:33.50482
[16]    train-mlogloss:34.96640 test-mlogloss:33.50482
[17]    train-mlogloss:34.96640 test-mlogloss:33.50482
[18]    train-mlogloss:34.96640 test-mlogloss:33.50482
[19]    train-mlogloss:34.96640 test-mlogloss:33.50482
[20]    train-mlogloss:34.96640 test-mlogloss:33.50482
[21]    train-mlogloss:34.96640 test-mlogloss:33.50482
[22]    train-mlogloss:34.96640 test-mlogloss:33.50482
[23]    train-mlogloss:34.96640 test-mlogloss:33.50482
[24]    train-mlogloss:34.96640 test-mlogloss:33.50482
[25]    train-mlogloss:34.96640 test-mlogloss:33.50482
[26]    train-mlogloss:34.96640 test-mlogloss:33.50482
[27]    train-mlogloss:34.96640 test-mlogloss:33.50482
[28]    train-mlogloss:34.96640 test-mlogloss:33.50482
[29]    train-mlogloss:34.96640 test-mlogloss:33.50482
./hs-xgboost.py:91: RuntimeWarning: overflow encountered in exp
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
./hs-xgboost.py:91: RuntimeWarning: invalid value encountered in divide
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
F1 Score: 0.021285525791713517
Precision: 0.8014058197358198
Recall: 0.068

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.693s
user    0m14.724s
sys     0m0.587s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 5 --learning_rate 6
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:5.12828  test-mlogloss:7.23679
[1]     train-mlogloss:34.83291 test-mlogloss:33.70225
[2]     train-mlogloss:33.26851 test-mlogloss:35.93599
[3]     train-mlogloss:33.37328 test-mlogloss:35.92401
[4]     train-mlogloss:34.86875 test-mlogloss:33.71367
[5]     train-mlogloss:30.19645 test-mlogloss:34.48351
[6]     train-mlogloss:30.19645 test-mlogloss:34.48351
[7]     train-mlogloss:30.19645 test-mlogloss:34.48351
[8]     train-mlogloss:30.19645 test-mlogloss:34.48351
[9]     train-mlogloss:30.19645 test-mlogloss:34.48351
[10]    train-mlogloss:30.19645 test-mlogloss:34.48351
[11]    train-mlogloss:30.19645 test-mlogloss:34.48351
[12]    train-mlogloss:30.19645 test-mlogloss:34.48351
[13]    train-mlogloss:30.19645 test-mlogloss:34.48351
[14]    train-mlogloss:30.19645 test-mlogloss:34.48351
[15]    train-mlogloss:30.19645 test-mlogloss:34.48351
[16]    train-mlogloss:30.19645 test-mlogloss:34.48351
[17]    train-mlogloss:30.19645 test-mlogloss:34.48351
[18]    train-mlogloss:30.19645 test-mlogloss:34.48351
[19]    train-mlogloss:30.19645 test-mlogloss:34.48351
[20]    train-mlogloss:30.19645 test-mlogloss:34.48351
[21]    train-mlogloss:30.19645 test-mlogloss:34.48351
[22]    train-mlogloss:30.19645 test-mlogloss:34.48351
[23]    train-mlogloss:30.19645 test-mlogloss:34.48351
[24]    train-mlogloss:30.19645 test-mlogloss:34.48351
[25]    train-mlogloss:30.19645 test-mlogloss:34.48351
[26]    train-mlogloss:30.19645 test-mlogloss:34.48351
[27]    train-mlogloss:30.19645 test-mlogloss:34.48351
[28]    train-mlogloss:30.19645 test-mlogloss:34.48351
[29]    train-mlogloss:30.19645 test-mlogloss:34.48351
./hs-xgboost.py:91: RuntimeWarning: overflow encountered in exp
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
./hs-xgboost.py:91: RuntimeWarning: invalid value encountered in divide
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
F1 Score: 0.007699248120300752
Precision: 0.940096
Recall: 0.064

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.765s
user    0m15.217s
sys     0m0.604s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 5 --learning_rate 9
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:7.69040  test-mlogloss:11.04058
[1]     train-mlogloss:35.02892 test-mlogloss:33.56248
[2]     train-mlogloss:30.25141 test-mlogloss:34.55720
[3]     train-mlogloss:30.25141 test-mlogloss:34.55720
[4]     train-mlogloss:30.25141 test-mlogloss:34.55720
[5]     train-mlogloss:30.25141 test-mlogloss:34.55720
[6]     train-mlogloss:30.25141 test-mlogloss:34.55720
[7]     train-mlogloss:30.25141 test-mlogloss:34.55720
[8]     train-mlogloss:30.25141 test-mlogloss:34.55720
[9]     train-mlogloss:30.25141 test-mlogloss:34.55720
[10]    train-mlogloss:30.25141 test-mlogloss:34.55720
[11]    train-mlogloss:30.25141 test-mlogloss:34.55720
[12]    train-mlogloss:30.25141 test-mlogloss:34.55720
[13]    train-mlogloss:30.25141 test-mlogloss:34.55720
[14]    train-mlogloss:30.25141 test-mlogloss:34.55720
[15]    train-mlogloss:30.25141 test-mlogloss:34.55720
[16]    train-mlogloss:30.25141 test-mlogloss:34.55720
[17]    train-mlogloss:30.25141 test-mlogloss:34.55720
[18]    train-mlogloss:30.25141 test-mlogloss:34.55720
[19]    train-mlogloss:30.25141 test-mlogloss:34.55720
[20]    train-mlogloss:30.25141 test-mlogloss:34.55720
[21]    train-mlogloss:30.25141 test-mlogloss:34.55720
[22]    train-mlogloss:30.25141 test-mlogloss:34.55720
[23]    train-mlogloss:30.25141 test-mlogloss:34.55720
[24]    train-mlogloss:30.25141 test-mlogloss:34.55720
[25]    train-mlogloss:30.25141 test-mlogloss:34.55720
[26]    train-mlogloss:30.25141 test-mlogloss:34.55720
[27]    train-mlogloss:30.25141 test-mlogloss:34.55720
[28]    train-mlogloss:30.25141 test-mlogloss:34.55720
[29]    train-mlogloss:30.25141 test-mlogloss:34.55720
./hs-xgboost.py:91: RuntimeWarning: overflow encountered in exp
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
./hs-xgboost.py:91: RuntimeWarning: invalid value encountered in divide
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
F1 Score: 0.007706491063029164
Precision: 0.8501001001001002
Recall: 0.064

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.763s
user    0m15.075s
sys     0m0.597s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --num_round 30 --eval f1 --max_depth 5 --learning_rate 10
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:8.49532  test-mlogloss:12.19518
[1]     train-mlogloss:33.01107 test-mlogloss:33.93232
[2]     train-mlogloss:32.85254 test-mlogloss:35.92033
[3]     train-mlogloss:32.85254 test-mlogloss:35.92033
[4]     train-mlogloss:32.85254 test-mlogloss:35.92033
[5]     train-mlogloss:32.85254 test-mlogloss:35.92033
[6]     train-mlogloss:32.85254 test-mlogloss:35.92033
[7]     train-mlogloss:32.85254 test-mlogloss:35.92033
[8]     train-mlogloss:32.85254 test-mlogloss:35.92033
[9]     train-mlogloss:32.85254 test-mlogloss:35.92033
[10]    train-mlogloss:32.85254 test-mlogloss:35.92033
[11]    train-mlogloss:32.85254 test-mlogloss:35.92033
[12]    train-mlogloss:32.85254 test-mlogloss:35.92033
[13]    train-mlogloss:32.85254 test-mlogloss:35.92033
[14]    train-mlogloss:32.85254 test-mlogloss:35.92033
[15]    train-mlogloss:32.85254 test-mlogloss:35.92033
[16]    train-mlogloss:32.85254 test-mlogloss:35.92033
[17]    train-mlogloss:32.85254 test-mlogloss:35.92033
[18]    train-mlogloss:32.85254 test-mlogloss:35.92033
[19]    train-mlogloss:32.85254 test-mlogloss:35.92033
[20]    train-mlogloss:32.85254 test-mlogloss:35.92033
[21]    train-mlogloss:32.85254 test-mlogloss:35.92033
[22]    train-mlogloss:32.85254 test-mlogloss:35.92033
[23]    train-mlogloss:32.85254 test-mlogloss:35.92033
[24]    train-mlogloss:32.85254 test-mlogloss:35.92033
[25]    train-mlogloss:32.85254 test-mlogloss:35.92033
[26]    train-mlogloss:32.85254 test-mlogloss:35.92033
[27]    train-mlogloss:32.85254 test-mlogloss:35.92033
[28]    train-mlogloss:32.85254 test-mlogloss:35.92033
[29]    train-mlogloss:32.85254 test-mlogloss:35.92033
./hs-xgboost.py:91: RuntimeWarning: overflow encountered in exp
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
./hs-xgboost.py:91: RuntimeWarning: invalid value encountered in divide
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
F1 Score: 0.008308537999899137
Precision: 0.8295152604548789
Recall: 0.062

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.793s
user    0m15.109s
sys     0m0.613s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

## Playing with --learning_rate, --feature tfidf for LONG

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --num_roun
d 30 --eval f1 --max_depth 5 --learning_rate 1
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:1.36140  test-mlogloss:1.77783
[1]     train-mlogloss:1.21652  test-mlogloss:1.90282
[2]     train-mlogloss:1.16594  test-mlogloss:1.96832
[3]     train-mlogloss:1.12600  test-mlogloss:2.02145
[4]     train-mlogloss:1.09260  test-mlogloss:2.06358
[5]     train-mlogloss:1.06928  test-mlogloss:2.09177
[6]     train-mlogloss:1.04587  test-mlogloss:2.12117
[7]     train-mlogloss:1.02853  test-mlogloss:2.12786
[8]     train-mlogloss:1.01250  test-mlogloss:2.12789
[9]     train-mlogloss:0.99731  test-mlogloss:2.14488
[10]    train-mlogloss:0.98436  test-mlogloss:2.16153
[11]    train-mlogloss:0.97041  test-mlogloss:2.16870
[12]    train-mlogloss:0.95713  test-mlogloss:2.17786
[13]    train-mlogloss:0.94554  test-mlogloss:2.19233
[14]    train-mlogloss:0.93577  test-mlogloss:2.20224
[15]    train-mlogloss:0.92534  test-mlogloss:2.20765
[16]    train-mlogloss:0.91539  test-mlogloss:2.21481
[17]    train-mlogloss:0.90665  test-mlogloss:2.22309
[18]    train-mlogloss:0.89519  test-mlogloss:2.23627
[19]    train-mlogloss:0.88637  test-mlogloss:2.23847
[20]    train-mlogloss:0.87829  test-mlogloss:2.24438
[21]    train-mlogloss:0.87098  test-mlogloss:2.25488
[22]    train-mlogloss:0.86390  test-mlogloss:2.26104
[23]    train-mlogloss:0.85595  test-mlogloss:2.27129
[24]    train-mlogloss:0.84891  test-mlogloss:2.28490
[25]    train-mlogloss:0.84283  test-mlogloss:2.28884
[26]    train-mlogloss:0.83715  test-mlogloss:2.30530
[27]    train-mlogloss:0.83095  test-mlogloss:2.31042
[28]    train-mlogloss:0.82274  test-mlogloss:2.31596
[29]    train-mlogloss:0.81633  test-mlogloss:2.32448
F1 Score: 0.41051406833610543
Precision: 0.3647756812420786
Recall: 0.496

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.844s
user    0m11.637s
sys     0m0.574s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --num_round 30 --eval f1 --max_depth 5 --learning_rate 2
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:1.92212  test-mlogloss:2.74234
[1]     train-mlogloss:13.73217 test-mlogloss:15.70318
[2]     train-mlogloss:14.96458 test-mlogloss:16.05898
[3]     train-mlogloss:17.46709 test-mlogloss:19.08383
[4]     train-mlogloss:17.46709 test-mlogloss:19.08383
[5]     train-mlogloss:17.46709 test-mlogloss:19.08383
[6]     train-mlogloss:17.46709 test-mlogloss:19.08383
[7]     train-mlogloss:17.46709 test-mlogloss:19.08383
[8]     train-mlogloss:17.46709 test-mlogloss:19.08383
[9]     train-mlogloss:17.46709 test-mlogloss:19.08383
[10]    train-mlogloss:17.46709 test-mlogloss:19.08383
[11]    train-mlogloss:17.46709 test-mlogloss:19.08383
[12]    train-mlogloss:17.46709 test-mlogloss:19.08383
[13]    train-mlogloss:17.46709 test-mlogloss:19.08383
[14]    train-mlogloss:17.46709 test-mlogloss:19.08383
[15]    train-mlogloss:17.46709 test-mlogloss:19.08383
[16]    train-mlogloss:17.46709 test-mlogloss:19.08383
[17]    train-mlogloss:17.46709 test-mlogloss:19.08383
[18]    train-mlogloss:17.46709 test-mlogloss:19.08383
[19]    train-mlogloss:17.46709 test-mlogloss:19.08383
[20]    train-mlogloss:17.46709 test-mlogloss:19.08383
[21]    train-mlogloss:17.46709 test-mlogloss:19.08383
[22]    train-mlogloss:17.46709 test-mlogloss:19.08383
[23]    train-mlogloss:17.46709 test-mlogloss:19.08383
[24]    train-mlogloss:17.46709 test-mlogloss:19.08383
[25]    train-mlogloss:17.46709 test-mlogloss:19.08383
[26]    train-mlogloss:17.46709 test-mlogloss:19.08383
[27]    train-mlogloss:17.46709 test-mlogloss:19.08383
[28]    train-mlogloss:17.46709 test-mlogloss:19.08383
[29]    train-mlogloss:17.46709 test-mlogloss:19.08383
./hs-xgboost.py:91: RuntimeWarning: overflow encountered in exp
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
./hs-xgboost.py:91: RuntimeWarning: invalid value encountered in divide
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
F1 Score: 0.4013666507350199
Precision: 0.42589333333333335
Recall: 0.542

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.045s
user    0m8.059s
sys     0m0.540s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --num_round 30 --eval f1 --max_depth 5 --learning_rate 3
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.80265  test-mlogloss:4.02577
[1]     train-mlogloss:33.39800 test-mlogloss:32.91058
[2]     train-mlogloss:16.58002 test-mlogloss:16.87370
[3]     train-mlogloss:16.58002 test-mlogloss:16.87370
[4]     train-mlogloss:16.58002 test-mlogloss:16.87370
[5]     train-mlogloss:16.58002 test-mlogloss:16.87370
[6]     train-mlogloss:16.58002 test-mlogloss:16.87370
[7]     train-mlogloss:16.58002 test-mlogloss:16.87370
[8]     train-mlogloss:16.58002 test-mlogloss:16.87370
[9]     train-mlogloss:16.58002 test-mlogloss:16.87370
[10]    train-mlogloss:16.58002 test-mlogloss:16.87370
[11]    train-mlogloss:16.58002 test-mlogloss:16.87370
[12]    train-mlogloss:16.58002 test-mlogloss:16.87370
[13]    train-mlogloss:16.58002 test-mlogloss:16.87370
[14]    train-mlogloss:16.58002 test-mlogloss:16.87370
[15]    train-mlogloss:16.58002 test-mlogloss:16.87370
[16]    train-mlogloss:16.58002 test-mlogloss:16.87370
[17]    train-mlogloss:16.58002 test-mlogloss:16.87370
[18]    train-mlogloss:16.58002 test-mlogloss:16.87370
[19]    train-mlogloss:16.58002 test-mlogloss:16.87370
[20]    train-mlogloss:16.58002 test-mlogloss:16.87370
[21]    train-mlogloss:16.58002 test-mlogloss:16.87370
[22]    train-mlogloss:16.58002 test-mlogloss:16.87370
[23]    train-mlogloss:16.58002 test-mlogloss:16.87370
[24]    train-mlogloss:16.58002 test-mlogloss:16.87370
[25]    train-mlogloss:16.58002 test-mlogloss:16.87370
[26]    train-mlogloss:16.58002 test-mlogloss:16.87370
[27]    train-mlogloss:16.58002 test-mlogloss:16.87370
[28]    train-mlogloss:16.58002 test-mlogloss:16.87370
[29]    train-mlogloss:16.58002 test-mlogloss:16.87370
./hs-xgboost.py:91: RuntimeWarning: overflow encountered in exp
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
./hs-xgboost.py:91: RuntimeWarning: invalid value encountered in divide
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
F1 Score: 0.3955024138687734
Precision: 0.5892288659793814
Recall: 0.543

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.032s
user    0m8.397s
sys     0m0.505s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --num_round 30 --eval f1 --max_depth 5 --learning_rate 4
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:3.71554  test-mlogloss:5.34255
[1]     train-mlogloss:31.72684 test-mlogloss:33.91974
[2]     train-mlogloss:31.72684 test-mlogloss:33.91974
[3]     train-mlogloss:31.72684 test-mlogloss:33.91974
[4]     train-mlogloss:31.72684 test-mlogloss:33.91974
[5]     train-mlogloss:31.72684 test-mlogloss:33.91974
[6]     train-mlogloss:31.72684 test-mlogloss:33.91974
[7]     train-mlogloss:31.72684 test-mlogloss:33.91974
[8]     train-mlogloss:31.72684 test-mlogloss:33.91974
[9]     train-mlogloss:31.72684 test-mlogloss:33.91974
[10]    train-mlogloss:31.72684 test-mlogloss:33.91974
[11]    train-mlogloss:31.72684 test-mlogloss:33.91974
[12]    train-mlogloss:31.72684 test-mlogloss:33.91974
[13]    train-mlogloss:31.72684 test-mlogloss:33.91974
[14]    train-mlogloss:31.72684 test-mlogloss:33.91974
[15]    train-mlogloss:31.72684 test-mlogloss:33.91974
[16]    train-mlogloss:31.72684 test-mlogloss:33.91974
[17]    train-mlogloss:31.72684 test-mlogloss:33.91974
[18]    train-mlogloss:31.72684 test-mlogloss:33.91974
[19]    train-mlogloss:31.72684 test-mlogloss:33.91974
[20]    train-mlogloss:31.72684 test-mlogloss:33.91974
[21]    train-mlogloss:31.72684 test-mlogloss:33.91974
[22]    train-mlogloss:31.72684 test-mlogloss:33.91974
[23]    train-mlogloss:31.72684 test-mlogloss:33.91974
[24]    train-mlogloss:31.72684 test-mlogloss:33.91974
[25]    train-mlogloss:31.72684 test-mlogloss:33.91974
[26]    train-mlogloss:31.72684 test-mlogloss:33.91974
[27]    train-mlogloss:31.72684 test-mlogloss:33.91974
[28]    train-mlogloss:31.72684 test-mlogloss:33.91974
[29]    train-mlogloss:31.72684 test-mlogloss:33.91974
./hs-xgboost.py:91: RuntimeWarning: overflow encountered in exp
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
./hs-xgboost.py:91: RuntimeWarning: invalid value encountered in divide
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
F1 Score: 0.03505955097534045
Precision: 0.7196312706900944
Recall: 0.07

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m0.972s
user    0m8.041s
sys     0m0.406s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --num_round 30 --eval f1 --max_depth 5 --learning_rate 5
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:4.63415  test-mlogloss:6.66568
[1]     train-mlogloss:31.26899 test-mlogloss:34.18878
[2]     train-mlogloss:31.26899 test-mlogloss:34.18878
[3]     train-mlogloss:31.26899 test-mlogloss:34.18878
[4]     train-mlogloss:31.26899 test-mlogloss:34.18878
[5]     train-mlogloss:31.26899 test-mlogloss:34.18878
[6]     train-mlogloss:31.26899 test-mlogloss:34.18878
[7]     train-mlogloss:31.26899 test-mlogloss:34.18878
[8]     train-mlogloss:31.26899 test-mlogloss:34.18878
[9]     train-mlogloss:31.26899 test-mlogloss:34.18878
[10]    train-mlogloss:31.26899 test-mlogloss:34.18878
[11]    train-mlogloss:31.26899 test-mlogloss:34.18878
[12]    train-mlogloss:31.26899 test-mlogloss:34.18878
[13]    train-mlogloss:31.26899 test-mlogloss:34.18878
[14]    train-mlogloss:31.26899 test-mlogloss:34.18878
[15]    train-mlogloss:31.26899 test-mlogloss:34.18878
[16]    train-mlogloss:31.26899 test-mlogloss:34.18878
[17]    train-mlogloss:31.26899 test-mlogloss:34.18878
[18]    train-mlogloss:31.26899 test-mlogloss:34.18878
[19]    train-mlogloss:31.26899 test-mlogloss:34.18878
[20]    train-mlogloss:31.26899 test-mlogloss:34.18878
[21]    train-mlogloss:31.26899 test-mlogloss:34.18878
[22]    train-mlogloss:31.26899 test-mlogloss:34.18878
[23]    train-mlogloss:31.26899 test-mlogloss:34.18878
[24]    train-mlogloss:31.26899 test-mlogloss:34.18878
[25]    train-mlogloss:31.26899 test-mlogloss:34.18878
[26]    train-mlogloss:31.26899 test-mlogloss:34.18878
[27]    train-mlogloss:31.26899 test-mlogloss:34.18878
[28]    train-mlogloss:31.26899 test-mlogloss:34.18878
[29]    train-mlogloss:31.26899 test-mlogloss:34.18878
./hs-xgboost.py:91: RuntimeWarning: overflow encountered in exp
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
./hs-xgboost.py:91: RuntimeWarning: invalid value encountered in divide
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
F1 Score: 0.03663945786090771
Precision: 0.7244785880785881
Recall: 0.072

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m0.992s
user    0m8.220s
sys     0m0.477s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --num_round 30 --eval f1 --max_depth 5 --learning_rate 6
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:5.55474  test-mlogloss:7.99115
[1]     train-mlogloss:30.53514 test-mlogloss:34.29931
[2]     train-mlogloss:30.53514 test-mlogloss:34.29931
[3]     train-mlogloss:30.53514 test-mlogloss:34.29931
[4]     train-mlogloss:30.53514 test-mlogloss:34.29931
[5]     train-mlogloss:30.53514 test-mlogloss:34.29931
[6]     train-mlogloss:30.53514 test-mlogloss:34.29931
[7]     train-mlogloss:30.53514 test-mlogloss:34.29931
[8]     train-mlogloss:30.53514 test-mlogloss:34.29931
[9]     train-mlogloss:30.53514 test-mlogloss:34.29931
[10]    train-mlogloss:30.53514 test-mlogloss:34.29931
[11]    train-mlogloss:30.53514 test-mlogloss:34.29931
[12]    train-mlogloss:30.53514 test-mlogloss:34.29931
[13]    train-mlogloss:30.53514 test-mlogloss:34.29931
[14]    train-mlogloss:30.53514 test-mlogloss:34.29931
[15]    train-mlogloss:30.53514 test-mlogloss:34.29931
[16]    train-mlogloss:30.53514 test-mlogloss:34.29931
[17]    train-mlogloss:30.53514 test-mlogloss:34.29931
[18]    train-mlogloss:30.53514 test-mlogloss:34.29931
[19]    train-mlogloss:30.53514 test-mlogloss:34.29931
[20]    train-mlogloss:30.53514 test-mlogloss:34.29931
[21]    train-mlogloss:30.53514 test-mlogloss:34.29931
[22]    train-mlogloss:30.53514 test-mlogloss:34.29931
[23]    train-mlogloss:30.53514 test-mlogloss:34.29931
[24]    train-mlogloss:30.53514 test-mlogloss:34.29931
[25]    train-mlogloss:30.53514 test-mlogloss:34.29931
[26]    train-mlogloss:30.53514 test-mlogloss:34.29931
[27]    train-mlogloss:30.53514 test-mlogloss:34.29931
[28]    train-mlogloss:30.53514 test-mlogloss:34.29931
[29]    train-mlogloss:30.53514 test-mlogloss:34.29931
./hs-xgboost.py:91: RuntimeWarning: overflow encountered in exp
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
./hs-xgboost.py:91: RuntimeWarning: invalid value encountered in divide
  pred_prob = np.apply_along_axis(lambda x: np.exp(x) / np.sum(np.exp(x)), 1, pred_prob)
F1 Score: 0.032573198022378354
Precision: 0.7261504237288137
Recall: 0.069

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m0.940s
user    0m7.505s
sys     0m0.513s
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

## Experiment-1 for both LONG, SHORT with Default Parameters  

shell script ကို အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့တယ်။  

```bash
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ cat exp1-for-JCSSE2024.sh
#!/bin/bash

## Written by Ye Kyaw Thu, LU Lab., Myanmar
## Experiment with long/short hate speech dataset
## for JCSSE 2024 Baseline
## Last updated: 7 April 2024

set -x;

## Evaluation with F1, P and R, Default Parameters for LONG HS
time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature tfidf \
--eval f1 | tee -a exp1.log

time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature word2vec \
--eval f1 | tee -a exp1.log

time python ./hs-xgboost.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature fasttext  \
--eval f1 | tee -a exp1.log

## Evaluation with F1, P and R, Default Parameters for SHORT HS
time python ./hs-xgboost.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature tfidf \
--eval f1 | tee -a exp1.log

time python ./hs-xgboost.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature word2vec \
--eval f1 | tee -a exp1.log

time python ./hs-xgboost.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature fasttext \
--eval f1 | tee -a exp1.log

set +x;
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

Experiment-1 Result...  

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ ./exp1-for-JCSSE2024.sh
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --eval f1
+ tee -a exp1.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.12946  test-mlogloss:2.17367
[1]     train-mlogloss:2.00021  test-mlogloss:2.08073
[2]     train-mlogloss:1.89729  test-mlogloss:2.01104
[3]     train-mlogloss:1.81263  test-mlogloss:1.95663
[4]     train-mlogloss:1.74133  test-mlogloss:1.91332
F1 Score: 0.40082636302582586
Precision: 0.3543703647416413
Recall: 0.541

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.023s
user    0m7.780s
sys     0m0.481s
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --eval f1
+ tee -a exp1.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.13212  test-mlogloss:2.17589
[1]     train-mlogloss:2.00247  test-mlogloss:2.08521
[2]     train-mlogloss:1.89629  test-mlogloss:2.01647
[3]     train-mlogloss:1.80896  test-mlogloss:1.96403
[4]     train-mlogloss:1.73342  test-mlogloss:1.92057
F1 Score: 0.38937196569484755
Precision: 0.6736459126539753
Recall: 0.531

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.140s
user    0m10.495s
sys     0m0.533s
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --eval f1
+ tee -a exp1.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.12986  test-mlogloss:2.17020
[1]     train-mlogloss:2.00038  test-mlogloss:2.07867
[2]     train-mlogloss:1.89502  test-mlogloss:2.00890
[3]     train-mlogloss:1.80787  test-mlogloss:1.95525
[4]     train-mlogloss:1.73270  test-mlogloss:1.91043
F1 Score: 0.3969942482789251
Precision: 0.5646141456582634
Recall: 0.538

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.755s
user    0m15.031s
sys     0m0.576s
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature tfidf --eval f1
+ tee -a exp1.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:2.09079  test-mlogloss:2.15884
[1]     train-mlogloss:1.94046  test-mlogloss:2.05952
[2]     train-mlogloss:1.82384  test-mlogloss:1.98623
[3]     train-mlogloss:1.72935  test-mlogloss:1.92968
[4]     train-mlogloss:1.65100  test-mlogloss:1.88545
F1 Score: 0.4412957516022528
Precision: 0.6042834620576556
Recall: 0.54

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m0.868s
user    0m7.246s
sys     0m0.489s
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --eval f1
+ tee -a exp1.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:2.02779  test-mlogloss:2.15351
[1]     train-mlogloss:1.84104  test-mlogloss:2.05598
[2]     train-mlogloss:1.69882  test-mlogloss:1.98478
[3]     train-mlogloss:1.58378  test-mlogloss:1.93085
[4]     train-mlogloss:1.48841  test-mlogloss:1.89088
F1 Score: 0.4414807121661721
Precision: 0.6844130162703379
Recall: 0.542

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.597s
user    0m8.912s
sys     0m0.580s
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --eval f1
+ tee -a exp1.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:2.03602  test-mlogloss:2.15003
[1]     train-mlogloss:1.85498  test-mlogloss:2.04697
[2]     train-mlogloss:1.71728  test-mlogloss:1.97403
[3]     train-mlogloss:1.60647  test-mlogloss:1.91917
[4]     train-mlogloss:1.51397  test-mlogloss:1.87692
F1 Score: 0.44245727534987955
Precision: 0.7401688262657588
Recall: 0.55

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m3.478s
user    0m11.949s
sys     0m0.636s
+ set +x
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

## Experiment-2 for both LONG, SHORT with --num_round 10

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ ./exp2-for-JCSSE2024.sh
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --eval f1 --num_round 10
+ tee -a exp2.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.12946  test-mlogloss:2.17367
[1]     train-mlogloss:2.00021  test-mlogloss:2.08073
[2]     train-mlogloss:1.89729  test-mlogloss:2.01104
[3]     train-mlogloss:1.81263  test-mlogloss:1.95663
[4]     train-mlogloss:1.74133  test-mlogloss:1.91332
[5]     train-mlogloss:1.67966  test-mlogloss:1.87827
[6]     train-mlogloss:1.62641  test-mlogloss:1.85027
[7]     train-mlogloss:1.57942  test-mlogloss:1.82738
[8]     train-mlogloss:1.53793  test-mlogloss:1.80942
[9]     train-mlogloss:1.50116  test-mlogloss:1.79569
F1 Score: 0.4025752666212844
Precision: 0.36034021739130434
Recall: 0.535

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.282s
user    0m8.833s
sys     0m0.508s
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --eval f1 --num_round 10
+ tee -a exp2.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.13061  test-mlogloss:2.17293
[1]     train-mlogloss:2.00051  test-mlogloss:2.08288
[2]     train-mlogloss:1.89458  test-mlogloss:2.01378
[3]     train-mlogloss:1.80641  test-mlogloss:1.96018
[4]     train-mlogloss:1.72989  test-mlogloss:1.91860
[5]     train-mlogloss:1.66305  test-mlogloss:1.88485
[6]     train-mlogloss:1.60415  test-mlogloss:1.85755
[7]     train-mlogloss:1.55276  test-mlogloss:1.83528
[8]     train-mlogloss:1.50647  test-mlogloss:1.81602
[9]     train-mlogloss:1.46502  test-mlogloss:1.80234
F1 Score: 0.39612066717707073
Precision: 0.678390729932843
Recall: 0.536

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.462s
user    0m12.341s
sys     0m0.519s
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --eval f1 --num_round 10
+ tee -a exp2.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:2.13138  test-mlogloss:2.17503
[1]     train-mlogloss:2.00141  test-mlogloss:2.08249
[2]     train-mlogloss:1.89588  test-mlogloss:2.01340
[3]     train-mlogloss:1.80833  test-mlogloss:1.95885
[4]     train-mlogloss:1.73416  test-mlogloss:1.91478
[5]     train-mlogloss:1.66797  test-mlogloss:1.87993
[6]     train-mlogloss:1.60969  test-mlogloss:1.85144
[7]     train-mlogloss:1.55865  test-mlogloss:1.82859
[8]     train-mlogloss:1.51228  test-mlogloss:1.81077
[9]     train-mlogloss:1.46995  test-mlogloss:1.79469
F1 Score: 0.39803761292291717
Precision: 0.6780144099378881
Recall: 0.544

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m5.122s
user    0m16.546s
sys     0m0.621s
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature tfidf --eval f1 --num_round 10
+ tee -a exp2.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:2.09079  test-mlogloss:2.15884
[1]     train-mlogloss:1.94046  test-mlogloss:2.05952
[2]     train-mlogloss:1.82384  test-mlogloss:1.98623
[3]     train-mlogloss:1.72935  test-mlogloss:1.92968
[4]     train-mlogloss:1.65100  test-mlogloss:1.88545
[5]     train-mlogloss:1.58398  test-mlogloss:1.85022
[6]     train-mlogloss:1.52700  test-mlogloss:1.82211
[7]     train-mlogloss:1.47666  test-mlogloss:1.80013
[8]     train-mlogloss:1.43294  test-mlogloss:1.78309
[9]     train-mlogloss:1.39452  test-mlogloss:1.76981
F1 Score: 0.4398949340807641
Precision: 0.5775848504615627
Recall: 0.538

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.018s
user    0m8.375s
sys     0m0.444s
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --eval f1 --num_round 10
+ tee -a exp2.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:2.02923  test-mlogloss:2.15253
[1]     train-mlogloss:1.84366  test-mlogloss:2.05165
[2]     train-mlogloss:1.70247  test-mlogloss:1.97892
[3]     train-mlogloss:1.58809  test-mlogloss:1.92616
[4]     train-mlogloss:1.49327  test-mlogloss:1.88560
[5]     train-mlogloss:1.41235  test-mlogloss:1.85466
[6]     train-mlogloss:1.34313  test-mlogloss:1.83138
[7]     train-mlogloss:1.28204  test-mlogloss:1.81534
[8]     train-mlogloss:1.22850  test-mlogloss:1.80325
[9]     train-mlogloss:1.18082  test-mlogloss:1.79616
F1 Score: 0.4414807121661721
Precision: 0.7214130162703379
Recall: 0.542

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.755s
user    0m9.936s
sys     0m0.429s
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --eval f1 --num_round 10
+ tee -a exp2.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:2.03732  test-mlogloss:2.14945
[1]     train-mlogloss:1.85669  test-mlogloss:2.04687
[2]     train-mlogloss:1.71937  test-mlogloss:1.97364
[3]     train-mlogloss:1.60779  test-mlogloss:1.91861
[4]     train-mlogloss:1.51607  test-mlogloss:1.87664
[5]     train-mlogloss:1.43822  test-mlogloss:1.84475
[6]     train-mlogloss:1.37163  test-mlogloss:1.82108
[7]     train-mlogloss:1.31342  test-mlogloss:1.80246
[8]     train-mlogloss:1.26199  test-mlogloss:1.79003
[9]     train-mlogloss:1.21716  test-mlogloss:1.78189
F1 Score: 0.44299778129392114
Precision: 0.7406348894348895
Recall: 0.551

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m3.695s
user    0m12.374s
sys     0m0.610s
+ set +x
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

## Experiment-3 for both LONG, SHORT with --num_round 10, --learning_rate 0.3

```
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$ ./exp3-for-JCSSE2024.sh
+ tee -a exp2.log
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --eval f1 --num_round 10 --learning_rate 0.3
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:1.82156  test-mlogloss:1.95389
[1]     train-mlogloss:1.61823  test-mlogloss:1.84050
[2]     train-mlogloss:1.48913  test-mlogloss:1.78497
[3]     train-mlogloss:1.40066  test-mlogloss:1.76264
[4]     train-mlogloss:1.33550  test-mlogloss:1.75496
[5]     train-mlogloss:1.28569  test-mlogloss:1.75967
[6]     train-mlogloss:1.24587  test-mlogloss:1.77318
[7]     train-mlogloss:1.21524  test-mlogloss:1.78714
[8]     train-mlogloss:1.18832  test-mlogloss:1.80582
[9]     train-mlogloss:1.16586  test-mlogloss:1.82397
F1 Score: 0.39911079779481656
Precision: 0.3293518317011244
Recall: 0.531

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.304s
user    0m9.360s
sys     0m0.449s
+ tee -a exp2.log
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --eval f1 --num_round 10 --learning_rate 0.3
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:1.81953  test-mlogloss:1.96265
[1]     train-mlogloss:1.59823  test-mlogloss:1.84746
[2]     train-mlogloss:1.45229  test-mlogloss:1.79200
[3]     train-mlogloss:1.34771  test-mlogloss:1.77262
[4]     train-mlogloss:1.26659  test-mlogloss:1.76673
[5]     train-mlogloss:1.20294  test-mlogloss:1.77499
[6]     train-mlogloss:1.14765  test-mlogloss:1.79031
[7]     train-mlogloss:1.09926  test-mlogloss:1.80424
[8]     train-mlogloss:1.06250  test-mlogloss:1.82337
[9]     train-mlogloss:1.02648  test-mlogloss:1.84402
F1 Score: 0.3950963823009053
Precision: 0.5897403722721437
Recall: 0.522

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.402s
user    0m11.569s
sys     0m0.442s
+ python ./hs-xgboost.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --eval f1 --num_round 10 --learning_rate 0.3
+ tee -a exp2.log
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
[0]     train-mlogloss:1.82314  test-mlogloss:1.95080
[1]     train-mlogloss:1.60592  test-mlogloss:1.83646
[2]     train-mlogloss:1.46126  test-mlogloss:1.78244
[3]     train-mlogloss:1.35502  test-mlogloss:1.76046
[4]     train-mlogloss:1.27432  test-mlogloss:1.75526
[5]     train-mlogloss:1.20793  test-mlogloss:1.75985
[6]     train-mlogloss:1.15210  test-mlogloss:1.76948
[7]     train-mlogloss:1.10414  test-mlogloss:1.78685
[8]     train-mlogloss:1.06689  test-mlogloss:1.80287
[9]     train-mlogloss:1.02929  test-mlogloss:1.82007
F1 Score: 0.39425890688259113
Precision: 0.5544793140407289
Recall: 0.528

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m5.014s
user    0m16.152s
sys     0m0.601s
+ tee -a exp2.log
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature tfidf --eval f1 --num_round 10 --learning_rate 0.3
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:1.71758  test-mlogloss:1.92185
[1]     train-mlogloss:1.50149  test-mlogloss:1.81112
[2]     train-mlogloss:1.37225  test-mlogloss:1.76191
[3]     train-mlogloss:1.28391  test-mlogloss:1.74446
[4]     train-mlogloss:1.22148  test-mlogloss:1.74398
[5]     train-mlogloss:1.17573  test-mlogloss:1.75140
[6]     train-mlogloss:1.14074  test-mlogloss:1.76668
[7]     train-mlogloss:1.11404  test-mlogloss:1.78563
[8]     train-mlogloss:1.09233  test-mlogloss:1.80607
[9]     train-mlogloss:1.07441  test-mlogloss:1.82895
F1 Score: 0.4418083743437946
Precision: 0.5805824371976452
Recall: 0.538

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m0.977s
user    0m8.166s
sys     0m0.464s
+ tee -a exp2.log
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --eval f1 --num_round 10 --learning_rate 0.3
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:1.54734  test-mlogloss:1.92270
[1]     train-mlogloss:1.29816  test-mlogloss:1.83385
[2]     train-mlogloss:1.13983  test-mlogloss:1.80421
[3]     train-mlogloss:1.03094  test-mlogloss:1.81219
[4]     train-mlogloss:0.95235  test-mlogloss:1.83729
[5]     train-mlogloss:0.89106  test-mlogloss:1.87931
[6]     train-mlogloss:0.84638  test-mlogloss:1.93052
[7]     train-mlogloss:0.80799  test-mlogloss:1.98773
[8]     train-mlogloss:0.77718  test-mlogloss:2.04543
[9]     train-mlogloss:0.74891  test-mlogloss:2.11075
F1 Score: 0.44299474079639367
Precision: 0.6249987212276215
Recall: 0.537

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.730s
user    0m9.857s
sys     0m0.470s
+ tee -a exp2.log
+ python ./hs-xgboost.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --eval f1 --num_round 10 --learning_rate 0.3
/home/yekyaw.thu/.conda/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py:727: FutureWarning: Pass `evals` as keyword args.
  warnings.warn(msg, FutureWarning)
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
[0]     train-mlogloss:1.57014  test-mlogloss:1.91016
[1]     train-mlogloss:1.33085  test-mlogloss:1.81332
[2]     train-mlogloss:1.18178  test-mlogloss:1.78082
[3]     train-mlogloss:1.07990  test-mlogloss:1.78336
[4]     train-mlogloss:1.00481  test-mlogloss:1.80612
[5]     train-mlogloss:0.94802  test-mlogloss:1.84106
[6]     train-mlogloss:0.90285  test-mlogloss:1.88466
[7]     train-mlogloss:0.86922  test-mlogloss:1.93474
[8]     train-mlogloss:0.84112  test-mlogloss:1.99122
[9]     train-mlogloss:0.81902  test-mlogloss:2.04780
F1 Score: 0.4426204640800171
Precision: 0.7298552152495181
Recall: 0.549

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m3.675s
user    0m12.346s
sys     0m0.637s
+ set +x
(xgboost) yekyaw.thu@gpu:~/exp/xgboost$
```

---
