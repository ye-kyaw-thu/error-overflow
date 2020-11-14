# Installation of Old PyTorch CPU Version Example

PyTorch old version တွေက pip install နဲ့ လုပ်လို့ မရဘူး။  
link ပေးပြီး installation လုပ်တဲ့ ပုံစံနဲ့လုပ်လို့ ရတယ်။  
အဲဒါကို ဒီနေရာမှာ demo installation လုပ်ပြထားတာပါ။  

## Create Conda Environment  

ပထမဆုံး conda environment အသစ် တစ်ခုကို create လုပ်မယ်။  
python version ကိုတော့ 3.6 ပဲ ထားလိုက်ရအောင်။   

```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-crf-pytorch$ conda create --name pytorch1.5.1cpu_py36 python=3.6
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/tool/anaconda3/envs/pytorch1.5.1cpu_py36

  added / updated specs:
    - python=3.6


The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  ca-certificates    pkgs/main/linux-64::ca-certificates-2020.10.14-0
  certifi            pkgs/main/noarch::certifi-2020.6.20-pyhd3eb1b0_3
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.33.1-h53a641e_7
  libedit            pkgs/main/linux-64::libedit-3.1.20191231-h14c3975_1
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_2
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.1.0-hdf63c60_0
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.1.0-hdf63c60_0
  ncurses            pkgs/main/linux-64::ncurses-6.2-he6710b0_1
  openssl            pkgs/main/linux-64::openssl-1.1.1h-h7b6447c_0
  pip                pkgs/main/linux-64::pip-20.2.4-py36h06a4308_0
  python             pkgs/main/linux-64::python-3.6.12-hcff3b4d_2
  readline           pkgs/main/linux-64::readline-8.0-h7b6447c_0
  setuptools         pkgs/main/linux-64::setuptools-50.3.1-py36h06a4308_1
  sqlite             pkgs/main/linux-64::sqlite-3.33.0-h62c20be_0
  tk                 pkgs/main/linux-64::tk-8.6.10-hbc83047_0
  wheel              pkgs/main/noarch::wheel-0.35.1-pyhd3eb1b0_0
  xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
  zlib               pkgs/main/linux-64::zlib-1.2.11-h7b6447c_3


Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate pytorch1.5.1cpu_py36
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```

## Conda Activate

အသစ်ဆောက်ထားတဲ့ enviornment ဖြစ်တဲ့ pytorch1.5.1cpu_py36 ထဲဝင်မယ်။  

```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-crf-pytorch$ conda activate pytorch1.5.1cpu_py36
(pytorch1.5.1cpu_py36) ye@ykt-pro:/media/ye/project1/tool/lstm-crf-pytorch$
```

pip command ကို torch==1.5.1+cpu ဆိုတဲ့ option ပေးပြီး installation လုပ်ကြည့်ရင် အောက်ပါအတိုင်း error ပေးတာကို တွေ့ရပါလိမ့်မယ်။  
 
 ```
(pytorch1.5.1cpu_py36) ye@ykt-pro:/media/ye/project1/tool/lstm-crf-pytorch$pip install torch==1.5.1+cpu
ERROR: Could not find a version that satisfies the requirement torch==1.5.1+cpu (from versions: 0.1.2, 0.1.2.post1, 0.1.2.post2, 0.3.1, 0.4.0, 0.4.1, 1.0.0, 1.0.1, 1.0.1.post2, 1.1.0, 1.2.0, 1.3.0, 1.3.1, 1.4.0, 1.5.0, 1.5.1, 1.6.0, 1.7.0)
ERROR: No matching distribution found for torch==1.5.1+cpu
```

"-f" option နဲ့ သက်ဆိုင်တဲ့ link ကို ပေးပြီးတော့ installation လုပ်လို့ရပါတယ်။ အောက်ပါအတိုင်းပါ။  

```
(pytorch1.5.1cpu_py36) ye@ykt-pro:/media/ye/project1/tool/lstm-crf-pytorch$ pip install torch==1.5.1+cpu -f https://download.pytorch.org/whl/torch_stable.html
Looking in links: https://download.pytorch.org/whl/torch_stable.html
Collecting torch==1.5.1+cpu
  Downloading https://download.pytorch.org/whl/cpu/torch-1.5.1%2Bcpu-cp36-cp36m-linux_x86_64.whl (127.3 MB)
     |████████████████████████████████| 127.3 MB 115 kB/s 
Requirement already satisfied: numpy in /home/ye/.local/lib/python3.6/site-packages (from torch==1.5.1+cpu) (1.19.2)
WARNING: Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ProtocolError('Connection aborted.', ConnectionResetError(104, 'Connection reset by peer'))': /simple/future/
Collecting future
  Downloading future-0.18.2.tar.gz (829 kB)
     |████████████████████████████████| 829 kB 611 kB/s 
Building wheels for collected packages: future
  Building wheel for future (setup.py) ... done
  Created wheel for future: filename=future-0.18.2-py3-none-any.whl size=491059 sha256=8dbc2ca3011ba9f2910864f75d6f2bab402a074fda5fe1df5e87c5d9eb8d2720
  Stored in directory: /home/ye/.cache/pip/wheels/6e/9c/ed/4499c9865ac1002697793e0ae05ba6be33553d098f3347fb94
Successfully built future
Installing collected packages: future, torch
Successfully installed future-0.18.2 torch-1.5.1+cpu
```

Interactive Python ကို တင်လိုက်ပြီးတော့ torch ကို import လုပ်ပြီး installation လုပ်ထားတဲ့ version ကို confirm လုပ်ကြည့်ရအောင်...  

```
(pytorch1.5.1cpu_py36) ye@ykt-pro:/media/ye/project1/tool/lstm-crf-pytorch$ python
Python 3.6.12 |Anaconda, Inc.| (default, Sep  8 2020, 23:10:56) 
[GCC 7.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import torch
>>> print(torch.__version__)
1.5.1+cpu
```

## Reference

PyTorch old version တွေရဲ့ link တွေကို အောက်ပါလင့်ကနေ ရနိုင်ပါတယ်။  

[https://pytorch.org/get-started/previous-versions/](https://pytorch.org/get-started/previous-versions/)  
