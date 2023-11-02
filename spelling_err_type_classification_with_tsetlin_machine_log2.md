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
## Updated Python Code

Update လုပ်ထားတဲ့ code က အောက်ပါအတိုင်း။  
ရှေ့က experiment မှာရေးထားခဲ့တဲ့ code နဲ့က အခြေခံအားဖြင့် အတူတူပါပဲ။  
ဒီမှာက fastText ကို သုံးပြီးတော့ feature ထုတ်တဲ့အပိုင်းကို အဓိက update လုပ်ထားတာပါ။  

```python
## Written by Ye Kyaw Thu, LU Lab., Myanmar
## For this time, extract feature with FAIR fastText
## Last Updated: 2 Nov 2023


import fasttext
import numpy as np
import argparse
from pyTsetlinMachine.tm import MultiClassTsetlinMachine
from sklearn.preprocessing import MultiLabelBinarizer
from sklearn.metrics import accuracy_score, f1_score, precision_score, recall_score
import joblib

def save_model(filename, tm, mlb):
    joblib.dump({'tm': tm, 'mlb': mlb}, filename)

def load_model(filename):
    loaded_model = joblib.load(filename)
    return loaded_model['tm'], loaded_model['mlb']

def load_data(file_path):
    with open(file_path, 'r', encoding='utf-8') as f:
        lines = f.readlines()
    data, labels = [], []
    for line in lines:
        label, text = line.strip().split(' ', 1)
        data.append(text)
        labels.append(label.split())
    return data, labels

def train_fasttext(data):
    with open('temp_train.txt', 'w', encoding='utf-8') as f:
        for item in data:
            f.write(item + '\n')
    model = fasttext.train_unsupervised('temp_train.txt', minn=3, maxn=6, dim=100)
    return model

def transform_fasttext(model, data):
    return np.array([model.get_sentence_vector(item) for item in data])

def main():
    parser = argparse.ArgumentParser()
    parser.add_argument('--mode', help='train or test', default='train')
    parser.add_argument('--train_data', help='path to training data file', default='data/train.txt')
    parser.add_argument('--test_data', help='path to test data file', default='data/test.txt')
    parser.add_argument('--model_name', help='path to save/load model', default='model')
    parser.add_argument('--hypothesis_filename', help='path to save hypothesis file', default='hypothesis.txt')
    parser.add_argument('--clauses', help='number of clauses', type=int, default=20)
    parser.add_argument('--T', help='threshold', type=int, default=15)
    parser.add_argument('--s', help='s', type=float, default=3.9)
    parser.add_argument('--epoch', help='number of epochs', type=int, default=100)
    args = parser.parse_args()

    if args.mode == 'train':
        train_data, train_labels = load_data(args.train_data)
        ft_model = train_fasttext(train_data)
        train_data = transform_fasttext(ft_model, train_data)

        mlb = MultiLabelBinarizer()
        train_labels = mlb.fit_transform(train_labels)

        num_classes = len(mlb.classes_)
        tm = MultiClassTsetlinMachine(args.clauses, args.T, args.s)
        for epoch in range(args.epoch):
            tm.fit(train_data, np.argmax(train_labels, axis=1), epochs=1)  # Train for 1 epoch at a time
            # Calculate and display metrics after each epoch
            predictions = tm.predict(train_data)
            accuracy = accuracy_score(np.argmax(train_labels, axis=1), predictions)
            f1 = f1_score(np.argmax(train_labels, axis=1), predictions, average='weighted', zero_division=0)
            precision = precision_score(np.argmax(train_labels, axis=1), predictions, average='weighted', zero_division=0)
            recall = recall_score(np.argmax(train_labels, axis=1), predictions, average='weighted', zero_division=0)
            print(f'Epoch {epoch + 1}/{args.epoch}, Accuracy: {accuracy:.2f}, F1 Score: {f1:.2f}, Precision: {precision:.2f}, Recall: {recall:.2f}')

        # Save the fasttext and Tsetlin Machine model
        ft_model.save_model(args.model_name + '_ft.bin')
        save_model(args.model_name + '.joblib', tm, mlb)

    elif args.mode == 'test':
        if args.test_data is None:
            print('Please provide the testing data path using --test_data argument')
            return

        test_data, test_labels = load_data(args.test_data)
        ft_model = fasttext.load_model(args.model_name + '_ft.bin')
        test_data = transform_fasttext(ft_model, test_data)

        # Load the Tsetlin Machine and MultiLabelBinarizer
        tm, mlb = load_model(args.model_name + '.joblib')  # Updated line

        test_labels = mlb.transform(test_labels)

        predictions = tm.predict(test_data)
        # Convert numerical labels to binary matrix representation
        binarized_predictions = np.zeros((len(predictions), len(mlb.classes_)))
        for i, pred in enumerate(predictions):
            binarized_predictions[i, pred] = 1
        # Convert binary matrix representation to original labels
        original_labels = mlb.inverse_transform(binarized_predictions)
        # Calculate and display metrics
        accuracy = accuracy_score(np.argmax(test_labels, axis=1), predictions)
        f1 = f1_score(np.argmax(test_labels, axis=1), predictions, average='weighted', zero_division=0)
        precision = precision_score(np.argmax(test_labels, axis=1), predictions, average='weighted', zero_division=0)
        recall = recall_score(np.argmax(test_labels, axis=1), predictions, average='weighted', zero_division=0)
        print(f'Accuracy: {accuracy:.2f}, F1 Score: {f1:.2f}, Precision: {precision:.2f}, Recall: {recall:.2f}')

        # Save the hypothesis file
        with open(args.hypothesis_filename, 'w') as f:
            for label_set in original_labels:
                f.write(' '.join(label_set) + '\n')

        print(f'Test results saved as {args.hypothesis_filename}')
        # ... rest of your testing code ...

if __name__ == '__main__':
    main()
```

## Experiment with All Data 


```
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$ ./run_fasttext_tsetlin.sh 300 | tee exp1_300epoch.log
Training with 97K data ...
Read 0M words
Number of words:  2578
Number of labels: 3
Progress: 100.0% words/sec/thread:  818398 lr: -0.000003 avg.loss:  2.801037 ETA:   0h 0m Progress: 100.0% words/sec/thread:  815709 lr:  0.000000 avg.loss:  2.801037 ETA:   0h 0m 0s
Epoch 1/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 2/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 3/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 4/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 5/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 6/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 7/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 8/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 9/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 10/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 11/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 12/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 13/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 14/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 15/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 16/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 17/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 18/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 19/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 20/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 21/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 22/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 23/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 24/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 25/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 26/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 27/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 28/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 29/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 30/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 31/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 32/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 33/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 34/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 35/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 36/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 37/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 38/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 39/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 40/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 41/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 42/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 43/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 44/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 45/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 46/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 47/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 48/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 49/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 50/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 51/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 52/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 53/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 54/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 55/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 56/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 57/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 58/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 59/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 60/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 61/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 62/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 63/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 64/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 65/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 66/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 67/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 68/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 69/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 70/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 71/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 72/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 73/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 74/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 75/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 76/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 77/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 78/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 79/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 80/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 81/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 82/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 83/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 84/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 85/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 86/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 87/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 88/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 89/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 90/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 91/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 92/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 93/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 94/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 95/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 96/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 97/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 98/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 99/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 100/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 101/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 102/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 103/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 104/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 105/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 106/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 107/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 108/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 109/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 110/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 111/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 112/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 113/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 114/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 115/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 116/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 117/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 118/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 119/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 120/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 121/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 122/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 123/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 124/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 125/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 126/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 127/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 128/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 129/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 130/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 131/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 132/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 133/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 134/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 135/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 136/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 137/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 138/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 139/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 140/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 141/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 142/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 143/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 144/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 145/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 146/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 147/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 148/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 149/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 150/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 151/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 152/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 153/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 154/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 155/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 156/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 157/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 158/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 159/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 160/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 161/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 162/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 163/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 164/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 165/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 166/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 167/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 168/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 169/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 170/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 171/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 172/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 173/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 174/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 175/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 176/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 177/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 178/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 179/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 180/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 181/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 182/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 183/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 184/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 185/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 186/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 187/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 188/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 189/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 190/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 191/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 192/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 193/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 194/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 195/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 196/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 197/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 198/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 199/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 200/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 201/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 202/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 203/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 204/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 205/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 206/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 207/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 208/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 209/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 210/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 211/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 212/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 213/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 214/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 215/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 216/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 217/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 218/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 219/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 220/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 221/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 222/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 223/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 224/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 225/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 226/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 227/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 228/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 229/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 230/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 231/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 232/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 233/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 234/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 235/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 236/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 237/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 238/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 239/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 240/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 241/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 242/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 243/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 244/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 245/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 246/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 247/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 248/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 249/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 250/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 251/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 252/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 253/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 254/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 255/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 256/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 257/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 258/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 259/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 260/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 261/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 262/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 263/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 264/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 265/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 266/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 267/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 268/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 269/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 270/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 271/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 272/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 273/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 274/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 275/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 276/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 277/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 278/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 279/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 280/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 281/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 282/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 283/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 284/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 285/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 286/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 287/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 288/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 289/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 290/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 291/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 292/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 293/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 294/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 295/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 296/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 297/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 298/300, Accuracy: 0.35, F1 Score: 0.18, Precision: 0.12, Recall: 0.35
Epoch 299/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 300/300, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46

real    3m27.247s
user    3m26.060s
sys     0m7.679s
===============
Testing with 10K errors ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Accuracy: 0.47, F1 Score: 0.30, Precision: 0.22, Recall: 0.47
Test results saved as ./error_type.epoch300.hyp

real    0m0.708s
user    0m1.443s
sys     0m3.424s
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$
```

Check the hyp file output/filesize:  

```
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$ head error_type.epoch300.hyp
__label__pho
__label__pho
__label__pho
__label__pho
__label__pho
__label__pho
__label__pho
__label__pho
__label__pho
__label__pho
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$
```

```
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$ wc error_type.epoch300.hyp
 10794  10794 140322 error_type.epoch300.hyp
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$
```

Result ကို သုံးသပ်ကြည့်တော့ FastText နဲ့ feature ထုတ်ပြီး Tsetlin ကို run တာက ရလဒ်က ပိုတောင် ကျသွားတယ်။  
ဖြစ်နိုင်တဲ့ reason က syllable 5 လုံးရဲ့ အမှားတွေကိုပဲ fasttext embedding လုပ်ခဲ့တာမို့လို့ embedding အတွက် မလုံလောက်တာလဲ ဖြစ်နိုင်တယ်။  



## Playing with T values

Reference from ChatGPT:

In a Tsetlin Machine, the hyperparameters `T` and `s` play crucial roles, although the specifics of their functions are not always straightforwardly explained in the literature. However, a practical example can provide some insight. In one study, a Tsetlin Machine was configured with a threshold value (`T`) of 15 and an `s`-value of 3.9 for binary classification tasks, but for multi-class classification, a higher `T` value of 800 was used, likely due to the increased complexity of the task. However, the `s` value was not mentioned for the multi-class scenario, which leaves some uncertainty.

Paper Link:  [https://link.springer.com/chapter/10.1007/978-3-030-63799-6_5#:~:text=For%20experiments%20involving%20binary%20classification,with%20a%20T%20of%20800](https://link.springer.com/chapter/10.1007/978-3-030-63799-6_5#:~:text=For%20experiments%20involving%20binary%20classification,with%20a%20T%20of%20800)  

လက်ရှိ ငါတို့ လုပ်နေတာက multiclass classification မို့လို့ T-value ကို မြှင့်ကြည့်မယ်။

```
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$ python ./fasttext_tsetlin.py --help
usage: fasttext_tsetlin.py [-h] [--mode MODE] [--train_data TRAIN_DATA]
                           [--test_data TEST_DATA] [--model_name MODEL_NAME]
                           [--hypothesis_filename HYPOTHESIS_FILENAME]
                           [--clauses CLAUSES] [--T T] [--s S] [--epoch EPOCH]

optional arguments:
  -h, --help            show this help message and exit
  --mode MODE           train or test
  --train_data TRAIN_DATA
                        path to training data file
  --test_data TEST_DATA
                        path to test data file
  --model_name MODEL_NAME
                        path to save/load model
  --hypothesis_filename HYPOTHESIS_FILENAME
                        path to save hypothesis file
  --clauses CLAUSES     number of clauses
  --T T                 threshold
  --s S                 s
  --epoch EPOCH         number of epochs
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$
```

Updating bash shell script for playing with T value:  

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
time python ./fasttext_tsetlin.py --mode train --T 800 --train_data ./error_type.train --model_name tsetlin.epoch${EPOCH}.T800.model --epoch ${EPOCH}

echo "==============="
echo "Testing with 10K errors ..."
time python ./fasttext_tsetlin.py --mode test --model_name tsetlin.epoch${EPOCH}.T800.model --test_data ./error_type.valid --hypothesis_filename ./error_type.epoch${EPOCH}.T800.hyp

```

အထက်က shell script မှာက T value ကို 800 ထားခဲ့တယ်။ ပြီးတော့ မော်ဒယ်ဖိုင်နာမည်ကိုလည်း ခွဲခြားပြီး ထားချင်လို့ T800.model ဆိုပြီး extension ကို ပြင်ခဲ့တယ်။ Testing output ကိုလည်း T800.hyp ဆိုတဲ့ extension နဲ့ ထားခဲ့တယ်။  

Training/Testing results are as follows:  

```
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$ ./run_play_Tvalue.sh 100 | tee exp2_100epoch_T800.log
Training with 97K data ...
Read 0M words
Number of words:  2578
Number of labels: 3
Progress: 100.0% words/sec/thread:  817049 lr: -0.000006 avg.loss:  2.806322 ETA:   0h 0m Progress: 100.0% words/sec/thread:  813267 lr:  0.000000 avg.loss:  2.806322 ETA:   0h 0m 0s
Epoch 1/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 2/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 3/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 4/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 5/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 6/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 7/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 8/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 9/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 10/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 11/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 12/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 13/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 14/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 15/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 16/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 17/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 18/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 19/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 20/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 21/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 22/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 23/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 24/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 25/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 26/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 27/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 28/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 29/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 30/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 31/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 32/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 33/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 34/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 35/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 36/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 37/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 38/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 39/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 40/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 41/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 42/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 43/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 44/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 45/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 46/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 47/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 48/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 49/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 50/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 51/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 52/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 53/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 54/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 55/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 56/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 57/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 58/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 59/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 60/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 61/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 62/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 63/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 64/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 65/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 66/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 67/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 68/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 69/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 70/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 71/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 72/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 73/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 74/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 75/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 76/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 77/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 78/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 79/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
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
Epoch 92/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 93/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 94/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 95/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 96/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 97/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 98/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 99/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 100/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46

real    1m19.034s
user    1m20.660s
sys     0m5.327s
===============
Testing with 10K errors ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Accuracy: 0.47, F1 Score: 0.30, Precision: 0.22, Recall: 0.47
Test results saved as ./error_type.epoch100.T800.hyp

real    0m0.705s
user    0m1.440s
sys     0m3.429s
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$
```

For this time, I wanna try with T=50. The updated bash shell script is as follows:  

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
#time python ./fasttext_tsetlin.py --mode train --T 800 --train_data ./error_type.train --model_name tsetlin.epoch${EPOCH}.T800.model --epoch ${EPOCH}
time python ./fasttext_tsetlin.py --mode train --T 50 --train_data ./error_type.train --model_name tsetlin.epoch${EPOCH}.T50.model --epoch ${EPOCH}

echo "==============="
echo "Testing with 10K errors ..."
#time python ./fasttext_tsetlin.py --mode test --model_name tsetlin.epoch${EPOCH}.T800.model --test_data ./error_type.valid --hypothesis_filename ./error_type.epoch${EPOCH}.T800.hyp
time python ./fasttext_tsetlin.py --mode test --model_name tsetlin.epoch${EPOCH}.T50.model --test_data ./error_type.valid --hypothesis_filename ./error_type.epoch${EPOCH}.T50.hyp
```

running result with T=50 is as follows:  

```
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$ ./run_play_Tvalue.sh 100 | tee exp3_100epoch_T50.log
Training with 97K data ...
Read 0M words
Number of words:  2578
Number of labels: 3
Progress: 100.0% words/sec/thread:  816588 lr: -0.000005 avg.loss:  2.807577 ETA:   0h 0m Progress: 100.0% words/sec/thread:  812965 lr:  0.000000 avg.loss:  2.807577 ETA:   0h 0m 0s
Epoch 1/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 2/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 3/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 4/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 5/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 6/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 7/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 8/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 9/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 10/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 11/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 12/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 13/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 14/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 15/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 16/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 17/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 18/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 19/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 20/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 21/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 22/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 23/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 24/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 25/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 26/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 27/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 28/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 29/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 30/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 31/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 32/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 33/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 34/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 35/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 36/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 37/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 38/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 39/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 40/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 41/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 42/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 43/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 44/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 45/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 46/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 47/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 48/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 49/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 50/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 51/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 52/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 53/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 54/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 55/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 56/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 57/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 58/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 59/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 60/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 61/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 62/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 63/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 64/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 65/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 66/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 67/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 68/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 69/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 70/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 71/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 72/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 73/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 74/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 75/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 76/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 77/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 78/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 79/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
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
Epoch 92/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 93/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 94/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 95/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 96/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 97/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 98/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 99/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46
Epoch 100/100, Accuracy: 0.46, F1 Score: 0.29, Precision: 0.21, Recall: 0.46

real    1m15.999s
user    1m17.594s
sys     0m4.909s
===============
Testing with 10K errors ...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Accuracy: 0.47, F1 Score: 0.30, Precision: 0.22, Recall: 0.47
Test results saved as ./error_type.epoch100.T50.hyp

real    0m0.724s
user    0m1.504s
sys     0m3.830s
(tsetlin_py3.8) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/fasttext_feature$
```

ရလဒ်က အပြောင်းအလဲ မရှီဘူး ...   

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
