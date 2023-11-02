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

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
