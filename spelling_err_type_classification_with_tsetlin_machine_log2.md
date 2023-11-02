## Spelling Error Type Classification with Tsetlin Log No. 2

ဒီတစ်ခါတော့ feature ဆွဲထုတ်တဲ့အပိုင်းကို fastText သုံးပြီး လုပ်ကြည့်မယ်။  

## Feature Extraction with FastText

လက်ရှိ စက်ထဲမှာ fastText python library ကတော့ ရှိပြီးသား ...  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$ pip install fasttext
Requirement already satisfied: fasttext in /home/ye/anaconda3/lib/python3.9/site-packages (0.9.2)
Requirement already satisfied: numpy in /home/ye/anaconda3/lib/python3.9/site-packages (from fasttext) (1.22.4)
Requirement already satisfied: pybind11>=2.2 in /home/ye/anaconda3/lib/python3.9/site-packages (from fasttext) (2.11.1)
Requirement already satisfied: setuptools>=0.7.0 in /home/ye/anaconda3/lib/python3.9/site-packages (from fasttext) (61.2.0)
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$
```

သို့သော် tsetlin code ကို update လုပ်ပြီး run ကြည့်တဲ့အခါမှာ error ပေးနေတယ်။ အဲဒါကြောင့် Python version ကိုလည်း နည်းနည်း လျှော့ပြီး Anaconda env အသစ်ဆောက်ပြီး စမ်းဖို့ ဆုံးဖြတ်ခဲ့တယ်။  

## Preparing New Environment

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$ conda create --name tsetlin_py3.8 python=3.8
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.12.0
  latest version: 23.9.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/ye/anaconda3/envs/tsetlin_py3.8

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
#     $ conda activate tsetlin_py3.8
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$
```

change to the new env:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$ conda activate tsetlin_py3.8
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$
```

လိုအပ်တဲ့ library တွေကို installation လုပ်ခဲ့ ...  

```
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$ pip install fasttext pyTsetlinMachine scikit-learn joblib
Collecting fasttext
  Using cached fasttext-0.9.2-cp38-cp38-linux_x86_64.whl
Collecting pyTsetlinMachine
  Downloading pyTsetlinMachine-0.6.4.tar.gz (24 kB)
  Preparing metadata (setup.py) ... done
Collecting scikit-learn
  Downloading scikit_learn-1.3.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (11 kB)
Collecting joblib
  Using cached joblib-1.3.2-py3-none-any.whl.metadata (5.4 kB)
Collecting pybind11>=2.2 (from fasttext)
  Downloading pybind11-2.11.1-py3-none-any.whl.metadata (9.5 kB)
Requirement already satisfied: setuptools>=0.7.0 in /home/ye/anaconda3/envs/tsetlin_py3.8/lib/python3.8/site-packages (from fasttext) (68.0.0)
Collecting numpy (from fasttext)
  Using cached numpy-1.24.4-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (5.6 kB)
Collecting scipy>=1.5.0 (from scikit-learn)
  Using cached scipy-1.10.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (34.5 MB)
Collecting threadpoolctl>=2.0.0 (from scikit-learn)
  Using cached threadpoolctl-3.2.0-py3-none-any.whl.metadata (10.0 kB)
Downloading scikit_learn-1.3.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (11.1 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 11.1/11.1 MB 41.9 MB/s eta 0:00:00
Using cached joblib-1.3.2-py3-none-any.whl (302 kB)
Using cached numpy-1.24.4-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (17.3 MB)
Downloading pybind11-2.11.1-py3-none-any.whl (227 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 227.7/227.7 kB 3.5 MB/s eta 0:00:00
Using cached threadpoolctl-3.2.0-py3-none-any.whl (15 kB)
Building wheels for collected packages: pyTsetlinMachine
  Building wheel for pyTsetlinMachine (setup.py) ... done
  Created wheel for pyTsetlinMachine: filename=pyTsetlinMachine-0.6.4-cp38-cp38-linux_x86_64.whl size=66369 sha256=f1cfb46a4cd839922280f81b6aae282cd619189c2bae86e74a52c845bfce4258
  Stored in directory: /home/ye/.cache/pip/wheels/49/e2/3d/371ca19e9f98d827e9d8898530bdffc49c7dab8cebd5aab77c
Successfully built pyTsetlinMachine
Installing collected packages: pyTsetlinMachine, threadpoolctl, pybind11, numpy, joblib, scipy, fasttext, scikit-learn
Successfully installed fasttext-0.9.2 joblib-1.3.2 numpy-1.24.4 pyTsetlinMachine-0.6.4 pybind11-2.11.1 scikit-learn-1.3.2 scipy-1.10.1 threadpoolctl-3.2.0
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$
```

## Prepare test_run.sh

အရင်ဆုံး ဒေတာဆိုက် သေးသေးနဲ့ပဲ test run လုပ်ဖို့အတွက် shell script ကို အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့တယ်။ 

```bash
#!/bin/bash

## Written by Ye, LU Lab., Myanmar
## for running tsetlin machine with several epoch values
## last updated: 2 Nov 2023

# Check if epoch argument is provided
if [ "$#" -ne 1 ]; then
    echo "Usage: $0 <epoch>"
    exit 1
fi

EPOCH=$1

echo "Training with 97K data ..."
time python ./fasttext_tsetlin.py --mode train --train_data ./error_type.5k.train --model_name tsetlin.epoch${EPOCH}.model --epoch ${EPOCH}

echo "==============="
echo "Testing with 10K errors ..."
time python ./fasttext_tsetlin.py --mode test --model_name tsetlin.epoch${EPOCH}.model --test_data ./error_type.100.valid --hypothesis_filename ./error_type.epoch${EPOCH}.hyp
```

When I made test run, I got following error:  

```
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Traceback (most recent call last):
  File "./fasttext_tsetlin.py", line 107, in <module>
    main()
  File "./fasttext_tsetlin.py", line 80, in main
    test_labels = mlb.transform(test_labels)
  File "/home/ye/anaconda3/envs/tsetlin_py3.8/lib/python3.8/site-packages/sklearn/preprocessing/_label.py", line 853, in transform
    check_is_fitted(self)
  File "/home/ye/anaconda3/envs/tsetlin_py3.8/lib/python3.8/site-packages/sklearn/utils/validation.py", line 1461, in check_is_fitted
    raise NotFittedError(msg % {"name": type(estimator).__name__})
sklearn.exceptions.NotFittedError: This MultiLabelBinarizer instance is not fitted yet. Call 'fit' with appropriate arguments before using this estimator.
```

Code debugging and run again ...  

```
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$ ./test_run.sh 100 | tee test.log1
Training with 97K data ...
Read 0M words
Number of words:  561
Number of labels: 3
Progress: 100.1% words/sec/thread:   42344 lr: -0.000027 avg.loss:  4.126272 ETA:   0h 0m Progress: 100.0% words/sec/thread:   42128 lr:  0.000000 avg.loss:  4.126272 ETA:   0h 0m 0s
Epoch 1/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 2/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 3/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 4/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 5/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 6/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 7/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 8/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 9/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 10/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 11/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 12/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 13/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 14/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 15/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 16/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 17/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 18/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 19/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 20/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 21/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 22/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 23/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 24/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 25/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 26/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 27/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 28/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 29/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 30/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 31/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 32/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 33/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 34/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 35/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 36/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 37/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 38/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 39/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 40/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 41/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 42/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 43/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 44/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 45/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 46/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 47/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 48/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 49/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 50/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 51/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 52/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 53/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 54/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 55/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 56/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 57/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 58/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 59/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 60/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 61/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 62/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 63/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 64/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 65/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 66/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 67/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 68/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 69/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 70/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 71/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 72/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 73/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 74/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 75/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 76/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 77/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 78/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 79/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 80/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 81/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 82/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 83/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 84/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 85/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 86/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 87/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 88/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 89/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 90/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 91/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 92/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 93/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 94/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 95/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 96/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 97/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 98/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 99/100, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 100/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46

real    0m9.511s
user    0m6.626s
sys     0m3.940s
===============
Testing with 10K errors ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Accuracy: 0.50, F1 Score: 0.33, Precision: 0.25, Recall: 0.50
Test results saved as ./error_type.epoch100.hyp

real    0m0.618s
user    0m1.285s
sys     0m3.494s
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$
```

the 1st test run with fasttext feature successs! :)

## 2nd Test Run with More Epochs

Test run with 200 epochs ...  

```
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$ ./test_run.sh 200 | tee test.log3
...
...
...
Epoch 194/200, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 195/200, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 196/200, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 197/200, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 198/200, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 199/200, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 200/200, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46

real    0m8.742s
user    0m10.355s
sys     0m3.696s
===============
Testing with 10K errors ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Accuracy: 0.50, F1 Score: 0.33, Precision: 0.25, Recall: 0.50
Test results saved as ./error_type.epoch200.hyp

real    0m0.613s
user    0m1.354s
sys     0m3.424s
```

Test run with 500 epochs ...  

```
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$ ./test_run.sh 500 | tee test.log2
...
...
...
Epoch 494/500, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 495/500, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 496/500, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 497/500, Accuracy: 0.34, F1 Score: 0.17, Precision: 0.11, Recall: 0.34
Epoch 498/500, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 499/500, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 500/500, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46

real    0m20.146s
user    0m21.922s
sys     0m3.596s
===============
Testing with 10K errors ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Accuracy: 0.50, F1 Score: 0.33, Precision: 0.25, Recall: 0.50
Test results saved as ./error_type.epoch500.hyp

real    0m0.615s
user    0m1.392s
sys     0m3.385s
```

## Experiment with All Data 


```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
