# Conda-Pytorch-Preparation

Conda environment အသစ်တစ်ခု create လုပ်ပြီးတော့ Pytorch CPU version ကို အဲဒီ environment ပေါ်မှာ installation လုပ်တာနဲ့ ပတ်သတ်တဲ့ note ဖိုင်ပါ။ Conda enviroment နဲ့ မရင်းနှီးတဲ့သူတွေအတွက် အသုံးဝင်ပါလိမ့်မယ်။  

## Creating a new environment with python=3.7

"--name" ဆိုတဲ့ option က ကိုယ်အသစ်ဖန်တီးမဲ့ enviroment ရဲ့ နာမည်ကိုပေးဖို့အတွက် သုံးတာပါ။ "pytorch1_py37" ဆိုတဲ့ နာမည်ကို ပေးထားပါတယ်။ ကိုယ်ကြိုက်တဲ့နာမည်ကို ပေးလို့ ရပါတယ်။ ပြီးတော့ installation လုပ်ချင်တဲ့ python ကိုလည်း ဗားရှင်းပါ သတ်မှတ်ပြီး install လုပ်ချင်လို့ "python=3.7" ဆိုပြီး ပေးခဲ့တာပါ။  

```
(base) ye@ykt-pro:/media/ye/project1/tool/Mask-Language-Model$ conda create --name pytorch1_py37 python=3.7
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/tool/anaconda3/envs/pytorch1_py37

  added / updated specs:
    - python=3.7


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    libedit-3.1.20191231       |       h14c3975_1         116 KB
    pip-20.2.2                 |           py37_0         1.8 MB
    python-3.7.9               |       h7579374_0        45.3 MB
    setuptools-49.6.0          |           py37_0         754 KB
    sqlite-3.33.0              |       h62c20be_0         1.1 MB
    wheel-0.35.1               |             py_0          37 KB
    ------------------------------------------------------------
                                           Total:        49.1 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  ca-certificates    pkgs/main/linux-64::ca-certificates-2020.7.22-0
  certifi            pkgs/main/linux-64::certifi-2020.6.20-py37_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.33.1-h53a641e_7
  libedit            pkgs/main/linux-64::libedit-3.1.20191231-h14c3975_1
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_2
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.1.0-hdf63c60_0
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.1.0-hdf63c60_0
  ncurses            pkgs/main/linux-64::ncurses-6.2-he6710b0_1
  openssl            pkgs/main/linux-64::openssl-1.1.1h-h7b6447c_0
  pip                pkgs/main/linux-64::pip-20.2.2-py37_0
  python             pkgs/main/linux-64::python-3.7.9-h7579374_0
  readline           pkgs/main/linux-64::readline-8.0-h7b6447c_0
  setuptools         pkgs/main/linux-64::setuptools-49.6.0-py37_0
  sqlite             pkgs/main/linux-64::sqlite-3.33.0-h62c20be_0
  tk                 pkgs/main/linux-64::tk-8.6.10-hbc83047_0
  wheel              pkgs/main/noarch::wheel-0.35.1-py_0
  xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
  zlib               pkgs/main/linux-64::zlib-1.2.11-h7b6447c_3


Proceed ([y]/n)? y


Downloading and Extracting Packages
libedit-3.1.20191231 | 116 KB    | ################################################################################### | 100% 
wheel-0.35.1         | 37 KB     | ################################################################################### | 100% 
pip-20.2.2           | 1.8 MB    | ################################################################################### | 100% 
sqlite-3.33.0        | 1.1 MB    | ################################################################################### | 100% 
python-3.7.9         | 45.3 MB   | ################################################################################### | 100% 
setuptools-49.6.0    | 754 KB    | ################################################################################### | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate pytorch1_py37
#
# To deactivate an active environment, use
#
#     $ conda deactivate
## Activate pytorch1_py37 environment and list env
(base) ye@ykt-pro:/media/ye/project1/tool/Mask-Language-Model$
```

အသစ် installation လုပ်ထားတဲ့ environment ထဲကို ဝင်မယ်ဆိုရင် "conda activate \<environment-name\>" ဆိုတဲ့ command ကို သုံးပါတယ်။  

```
(base) ye@ykt-pro:/media/ye/project1/tool/Mask-Language-Model$ conda activate pytorch1_py37
(pytorch1_py37) ye@ykt-pro:/media/ye/project1/tool/Mask-Language-Model$ conda env list
# conda environments:
#
base                     /home/ye/tool/anaconda3
conda3.6                 /home/ye/tool/anaconda3/envs/conda3.6
monoses                  /home/ye/tool/anaconda3/envs/monoses
persephone               /home/ye/tool/anaconda3/envs/persephone
py2.7                    /home/ye/tool/anaconda3/envs/py2.7
pytorch1_py37         *  /home/ye/tool/anaconda3/envs/pytorch1_py37
tensorflow               /home/ye/tool/anaconda3/envs/tensorflow
```


## Installation of pytorch-cpu

pytorch ကို installation လုပ်တဲ့အခါ ပုံမှန်က GPU version နဲ့ သွားပါလိမ့်မယ်။ တကယ်လို့ ကိုယ်ရဲ့ notebook ထဲမှာ experiment အသေးတချို့ကို လုပ်ချင်တယ်ဆိုရင်တော့ pytorch-cpu ကို installation လုပ်မယ် ဆိုရင်တော့ "conda install" နဲ့ run တဲ့အခါမှာ pytorch-cpu ဆိုပြီး သတ်မှတ်ပေးမှ ရပါလိမ့်မယ်။ "-c" option ကတော့ install လုပ်မယ့် package ကို ရှာတဲ့အခါမှာ ရှာစေချင်တဲ့ channel ကိုသတ်မှတ်ပေးတာ ဖြစ်ပါတယ်။   

```
(pytorch1_py37) ye@ykt-pro:/media/ye/project1/tool/Mask-Language-Model$ conda install -c pytorch pytorch-cpu
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/tool/anaconda3/envs/pytorch1_py37

  added / updated specs:
    - pytorch-cpu


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    cffi-1.14.3                |   py37he30daa8_0         223 KB
    intel-openmp-2020.2        |              254         786 KB
    mkl-2020.2                 |              256       138.3 MB
    mkl_fft-1.2.0              |   py37h23d657b_0         148 KB
    ninja-1.10.1               |   py37hfd86e86_0         1.4 MB
    numpy-1.19.1               |   py37hbc911f0_0          21 KB
    numpy-base-1.19.1          |   py37hfa32c7d_0         4.1 MB
    pycparser-2.20             |             py_2          94 KB
    ------------------------------------------------------------
                                           Total:       145.1 MB

The following NEW packages will be INSTALLED:

  blas               pkgs/main/linux-64::blas-1.0-mkl
  cffi               pkgs/main/linux-64::cffi-1.14.3-py37he30daa8_0
  intel-openmp       pkgs/main/linux-64::intel-openmp-2020.2-254
  mkl                pkgs/main/linux-64::mkl-2020.2-256
  mkl-service        pkgs/main/linux-64::mkl-service-2.3.0-py37he904b0f_0
  mkl_fft            pkgs/main/linux-64::mkl_fft-1.2.0-py37h23d657b_0
  mkl_random         pkgs/main/linux-64::mkl_random-1.1.1-py37h0573a6f_0
  ninja              pkgs/main/linux-64::ninja-1.10.1-py37hfd86e86_0
  numpy              pkgs/main/linux-64::numpy-1.19.1-py37hbc911f0_0
  numpy-base         pkgs/main/linux-64::numpy-base-1.19.1-py37hfa32c7d_0
  pycparser          pkgs/main/noarch::pycparser-2.20-py_2
  pytorch-cpu        pytorch/linux-64::pytorch-cpu-1.1.0-py3.7_cpu_0
  six                pkgs/main/noarch::six-1.15.0-py_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
ninja-1.10.1         | 1.4 MB    | ################################################################################### | 100% 
mkl-2020.2           | 138.3 MB  | ################################################################################### | 100% 
cffi-1.14.3          | 223 KB    | ################################################################################### | 100% 
pycparser-2.20       | 94 KB     | ################################################################################### | 100% 
numpy-1.19.1         | 21 KB     | ################################################################################### | 100% 
mkl_fft-1.2.0        | 148 KB    | ################################################################################### | 100% 
intel-openmp-2020.2  | 786 KB    | ################################################################################### | 100% 
numpy-base-1.19.1    | 4.1 MB    | ################################################################################### | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
```

## Testing import torch framework

installation လုပ်ထားတဲ့ pytorch က import လုပ်လို့ ရမရ စမ်းသပ်တာဖို့အတွက် ပရိုဂရမ်အသေးလေး တပုဒ်ရေးထားပြီး run တာကို နမူနာ လုပ်ပြထားတာ ဖြစ်ပါတယ်။   
အရင်ဆုံး python code ကို ကြည့်ရအောင်။  

```
(pytorch1_py37) ye@ykt-pro:/media/ye/project1/tool/Mask-Language-Model$ cat ./pytorch-import-test.py 
from __future__ import print_function
import torch
x = torch.rand(2, 3, 4)
print(x)
```

run ကြည့်ရအောင်။ coding မှာမြင်ရတဲ့အတိုင်း "torch.rand(2, 3, 4)" ဆိုပြီး tensor ရဲ့ shape ကို 2, 3, 4 ဆိုပြီးထားခဲ့လို့ အဲဒီ shape မှာ random value နဲ့ ဖြည့်ပြီးပြပေးပါလိမ့်မယ်။  

```
(pytorch1_py37) ye@ykt-pro:/media/ye/project1/tool/Mask-Language-Model$ python ./pytorch-import-test.py 
tensor([[[0.8172, 0.8915, 0.3025, 0.3595],
         [0.2715, 0.7749, 0.4014, 0.8265],
         [0.4307, 0.1273, 0.4391, 0.3232]],

        [[0.3288, 0.7164, 0.3346, 0.8309],
         [0.0037, 0.1166, 0.7883, 0.0706],
         [0.8236, 0.7092, 0.0606, 0.3490]]])

```

## Installation of tqdm library

"tqdm" library ကတော့လိုအပ်မှ installation လုပ်ပါ။ pytorch-cpu installation နဲ့ မဆိုင်ပါဘူး။ progress bar ပြဖို့အတွက် အသုံးဝင်လို့ ဥပမာအနေနဲ့ ထည့်ထားတာပဲ ဖြစ်ပါတယ်။  

```
(pytorch1_py37) ye@ykt-pro:/media/ye/project1/tool/Mask-Language-Model$ pip install tqdm
Collecting tqdm
  Downloading tqdm-4.50.0-py2.py3-none-any.whl (70 kB)
     |████████████████████████████████| 70 kB 402 kB/s 
Installing collected packages: tqdm
ERROR: After October 2020 you may experience errors when installing or updating packages. This is because pip will change the way that it resolves dependency conflicts.

We recommend you use --use-feature=2020-resolver to test your packages with the new resolver before it becomes the default.

nltk 3.5 requires click, which is not installed.
nltk 3.5 requires joblib, which is not installed.
Successfully installed tqdm-4.50.0
```

tqdm ကို library ကို input လုပ်ပြီး test လုပ်ကြည့်ရအောင်။  

```
(pytorch1_py37) ye@ykt-pro:/media/ye/project1/tool/Mask-Language-Model$ cat ./tqdm-demo.py 
from tqdm import tqdm
for i in tqdm(range(9000000)):
    pass

(pytorch1_py37) ye@ykt-pro:/media/ye/project1/tool/Mask-Language-Model$ python ./tqdm-demo.py 
100%|██████████████████████████████████████████████████████████████████████████| 9000000/9000000 [00:01<00:00, 4674827.43it/s]
```

## For the above ERROR

အထက်မှာ tqdm installation လုပ်စဉ်မှာ မြင်ရတဲ့ error က pip နဲ့ ဆိုင်တဲ့ error ပါ။   

```
(pytorch1_py37) ye@ykt-pro:/media/ye/project1/tool/Mask-Language-Model$ python -m pip install --upgrade pip
Collecting pip
  Downloading pip-20.2.3-py2.py3-none-any.whl (1.5 MB)
     |████████████████████████████████| 1.5 MB 557 kB/s 
Installing collected packages: pip
  Attempting uninstall: pip
    Found existing installation: pip 20.2.2
    Uninstalling pip-20.2.2:
      Successfully uninstalled pip-20.2.2
Successfully installed pip-20.2.3
(pytorch1_py37) ye@ykt-pro:/media/ye/project1/tool/Mask-Language-Model$ pip install example --use-feature=2020-resolver
Collecting example
  Downloading example-0.1.0.tar.gz (860 bytes)
Requirement already satisfied: six in /home/ye/tool/anaconda3/envs/pytorch1_py37/lib/python3.7/site-packages (from example) (1.15.0)
Building wheels for collected packages: example
  Building wheel for example (setup.py) ... done
  Created wheel for example: filename=example-0.1.0-py3-none-any.whl size=1239 sha256=4960ba43fd0630d2c983ecaab6b9764fdf4fddfe7237e408d6ad0a432524f691
  Stored in directory: /home/ye/.cache/pip/wheels/8d/ea/09/d4642cabc2ea6d60ab48ecabea4f62d604108571d1a059d6d9
Successfully built example
Installing collected packages: example
Successfully installed example-0.1.0
```

## Reference

[https://tqdm.github.io/](https://tqdm.github.io/)  
[https://stackoverflow.com/questions/63277123/what-is-use-feature-2020-resolver-error-message-with-jupyter-installation-on](https://stackoverflow.com/questions/63277123/what-is-use-feature-2020-resolver-error-message-with-jupyter-installation-on)  
