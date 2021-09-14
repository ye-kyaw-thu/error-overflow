# Deep Siamese Text Similarity Experiment Log

Siamese Network က စိတ်ဝင်စားတယ်။  
ဒါပေမဲ့ develop လုပ်ခဲ့တာတွေက Python2.7 တို့ လွန်ခဲ့တဲ့ ၃နှစ် ၄နှစ် ပတ်ဝန်းကျင်က source code တွေဖြစ်တာ များတော့ ကျောင်းသားတွေအနေနဲ့က ကိုယ်စက်ထဲမှာ download လုပ်ပြီး run ကြတဲ့အခါမှာ သိပ်အလွယ်ကြီး မဟုတ်ဘူး။ ကိုယ်တိုင်လည်း အတွေ့အကြုံက ရှိပေမဲ့ အတိုင်းအတာ တစ်ခုအထိ အချိန်ပေးရတာ များပါတယ်။  

ဒီတစ်ခါတော့ Deep Siamese ဆိုတာကို ကိုယ့်စက်ထဲမှာ run ဖို့ ပြင်ခဲ့စဉ်က log တစ်ခုလုံးကို တင်ပေးထားလိုက်တယ်။  
တင်ထားတာက debug လုပ်လိုက် run ကြည့်လိုက် တကယ့် raw log မို့လို့... ဒီ log ကို ဖတ်ကြည့်ပြီး လုပ်တဲ့သူတွေက မလိုအပ်တဲ့ အဆင့်တွေကို ကျော်ပြီးလုပ်သွားပါ။  

source code link: https://github.com/dhwajraj/deep-siamese-text-similarity

## Create a New Conda Env

conda create -n "paraphrase2" python=3.6

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ conda create -n "paraphrase2" python=3.6
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/anaconda3/envs/paraphrase2

  added / updated specs:
    - python=3.6


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    wheel-0.37.0               |     pyhd3eb1b0_1          33 KB
    ------------------------------------------------------------
                                           Total:          33 KB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-4.5-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2021.7.5-h06a4308_1
  certifi            pkgs/main/linux-64::certifi-2021.5.30-py36h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.35.1-h7274673_9
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_2
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.3.0-h5101ec6_17
  libgomp            pkgs/main/linux-64::libgomp-9.3.0-h5101ec6_17
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.3.0-hd4cf53a_17
  ncurses            pkgs/main/linux-64::ncurses-6.2-he6710b0_1
  openssl            pkgs/main/linux-64::openssl-1.1.1l-h7f8727e_0
  pip                pkgs/main/linux-64::pip-21.0.1-py36h06a4308_0
  python             pkgs/main/linux-64::python-3.6.13-h12debd9_1
  readline           pkgs/main/linux-64::readline-8.1-h27cfd23_0
  setuptools         pkgs/main/linux-64::setuptools-52.0.0-py36h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.36.0-hc218d9a_0
  tk                 pkgs/main/linux-64::tk-8.6.10-hbc83047_0
  wheel              pkgs/main/noarch::wheel-0.37.0-pyhd3eb1b0_1
  xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
  zlib               pkgs/main/linux-64::zlib-1.2.11-h7b6447c_3


Proceed ([y]/n)? y


Downloading and Extracting Packages
wheel-0.37.0         | 33 KB     | ############################################################################################################# | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate paraphrase2
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ conda activate paraphrase2
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ 
```

## Install Some Dependencies

Prepare requirements.txt file.  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ vi requirements.txt
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ cat ./requirements.txt 
numpy==1.11.0
tensorflow==1.2.1
gensim==1.0.1
nltk==3.2.2
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$
```

Installation with following command:  

```
pip install -r requirements.txt
```

Installation လုပ်တော့ အောက်ပါ error ဖြစ်တယ်။  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ cat ./requirements.txt 
numpy==1.11.0
tensorflow==1.2.1
gensim==1.0.1
nltk==3.2.2
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ 
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ pip install -r requirements.txt 
Collecting numpy==1.11.0
  Downloading numpy-1.11.0.zip (4.7 MB)
     |████████████████████████████████| 4.7 MB 1.7 MB/s 
Collecting tensorflow==1.2.1
  Downloading tensorflow-1.2.1-cp36-cp36m-manylinux1_x86_64.whl (35.0 MB)
     |████████████████████████████████| 35.0 MB 32.8 MB/s 
Collecting gensim==1.0.1
  Downloading gensim-1.0.1.tar.gz (13.9 MB)
     |████████████████████████████████| 13.9 MB 82.4 MB/s 
Collecting nltk==3.2.2
  Downloading nltk-3.2.2.tar.gz (1.2 MB)
     |████████████████████████████████| 1.2 MB 69.6 MB/s 
Collecting scipy>=0.7.0
  Using cached scipy-1.5.4-cp36-cp36m-manylinux1_x86_64.whl (25.9 MB)
Collecting six>=1.5.0
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Collecting smart_open>=1.2.1
  Downloading smart_open-5.2.1-py3-none-any.whl (58 kB)
     |████████████████████████████████| 58 kB 17.6 MB/s 
Collecting backports.weakref==1.0rc1
  Downloading backports.weakref-1.0rc1-py3-none-any.whl (4.3 kB)
Collecting bleach==1.5.0
  Downloading bleach-1.5.0-py2.py3-none-any.whl (17 kB)
Collecting protobuf>=3.2.0
  Using cached protobuf-3.17.3-cp36-cp36m-manylinux_2_5_x86_64.manylinux1_x86_64.whl (1.0 MB)
Collecting werkzeug>=0.11.10
  Using cached Werkzeug-2.0.1-py3-none-any.whl (288 kB)
Collecting markdown>=2.6.8
  Using cached Markdown-3.3.4-py3-none-any.whl (97 kB)
Requirement already satisfied: wheel>=0.26 in /home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages (from tensorflow==1.2.1->-r requirements.txt (line 2)) (0.37.0)
Collecting html5lib==0.9999999
  Downloading html5lib-0.9999999.tar.gz (889 kB)
     |████████████████████████████████| 889 kB 61.6 MB/s 
Collecting importlib-metadata
  Downloading importlib_metadata-4.8.1-py3-none-any.whl (17 kB)
Collecting scipy>=0.7.0
  Downloading scipy-1.5.3-cp36-cp36m-manylinux1_x86_64.whl (25.9 MB)
     |████████████████████████████████| 25.9 MB 21.9 MB/s 
  Downloading scipy-1.5.2-cp36-cp36m-manylinux1_x86_64.whl (25.9 MB)
     |████████████████████████████████| 25.9 MB 38.3 MB/s 
  Downloading scipy-1.5.1-cp36-cp36m-manylinux1_x86_64.whl (25.9 MB)
     |████████████████████████████████| 25.9 MB 31.8 MB/s 
  Downloading scipy-1.5.0-cp36-cp36m-manylinux1_x86_64.whl (25.9 MB)
     |████████████████████████████████| 25.9 MB 36.2 MB/s 
  Downloading scipy-1.4.1-cp36-cp36m-manylinux1_x86_64.whl (26.1 MB)
     |████████████████████████████████| 26.1 MB 72.0 MB/s 
  Downloading scipy-1.4.0-cp36-cp36m-manylinux1_x86_64.whl (26.1 MB)
     |████████████████████████████████| 26.1 MB 20.8 MB/s 
  Downloading scipy-1.3.3-cp36-cp36m-manylinux1_x86_64.whl (25.2 MB)
     |████████████████████████████████| 25.2 MB 29.6 MB/s 
  Downloading scipy-1.3.2-cp36-cp36m-manylinux1_x86_64.whl (25.2 MB)
     |████████████████████████████████| 25.2 MB 29.6 MB/s 
  Downloading scipy-1.3.1-cp36-cp36m-manylinux1_x86_64.whl (25.2 MB)
     |████████████████████████████████| 25.2 MB 83.1 MB/s 
  Downloading scipy-1.3.0-cp36-cp36m-manylinux1_x86_64.whl (25.2 MB)
     |████████████████████████████████| 25.2 MB 31.0 MB/s 
  Downloading scipy-1.2.3-cp36-cp36m-manylinux1_x86_64.whl (24.8 MB)
     |████████████████████████████████| 24.8 MB 23.8 MB/s 
Collecting dataclasses
  Using cached dataclasses-0.8-py3-none-any.whl (19 kB)
Collecting zipp>=0.5
  Using cached zipp-3.5.0-py3-none-any.whl (5.7 kB)
Collecting typing-extensions>=3.6.4
  Downloading typing_extensions-3.10.0.2-py3-none-any.whl (26 kB)
Building wheels for collected packages: gensim, nltk, numpy, html5lib
  Building wheel for gensim (setup.py) ... done
  Created wheel for gensim: filename=gensim-1.0.1-cp36-cp36m-linux_x86_64.whl size=5541870 sha256=b1d11ff210a8f1d6022cca1060b9007f018adc9c15ba07c8bfa5dc789e321b29
  Stored in directory: /home/ye/.cache/pip/wheels/85/df/cc/cc4355dbb262291c0fd50ed277d3ad67843275dadf948b8288
  Building wheel for nltk (setup.py) ... done
  Created wheel for nltk: filename=nltk-3.2.2-py3-none-any.whl size=1353250 sha256=137252c77864ec1f530f15c5047e473dc13ae620534c50155d7e22d0372ba8a2
  Stored in directory: /home/ye/.cache/pip/wheels/67/d6/8c/5dda005acbc9a0d22c6199fdae187e7821c8e051a234628464
  Building wheel for numpy (setup.py) ... error
  ERROR: Command errored out with exit status 1:
   command: /home/ye/anaconda3/envs/paraphrase2/bin/python -u -c 'import sys, setuptools, tokenize; sys.argv[0] = '"'"'/tmp/pip-install-e8uqgu5p/numpy_3a01c5fb02e74d0397f2d7519f7d13a8/setup.py'"'"'; __file__='"'"'/tmp/pip-install-e8uqgu5p/numpy_3a01c5fb02e74d0397f2d7519f7d13a8/setup.py'"'"';f=getattr(tokenize, '"'"'open'"'"', open)(__file__);code=f.read().replace('"'"'\r\n'"'"', '"'"'\n'"'"');f.close();exec(compile(code, __file__, '"'"'exec'"'"'))' bdist_wheel -d /tmp/pip-wheel-rnfv7g73
       cwd: /tmp/pip-install-e8uqgu5p/numpy_3a01c5fb02e74d0397f2d7519f7d13a8/
  Complete output (2239 lines):
  Running from numpy source directory.
...
...
...
    gcc: numpy/core/src/multiarray/iterators.c
    gcc: build/src.linux-x86_64-3.6/numpy/core/src/multiarray/lowlevel_strided_loops.c
    gcc: numpy/core/src/multiarray/mapping.c
    gcc: numpy/core/src/multiarray/methods.c
    gcc: numpy/core/src/multiarray/multiarraymodule.c
    gcc: build/src.linux-x86_64-3.6/numpy/core/src/multiarray/nditer_templ.c
    gcc: numpy/core/src/multiarray/nditer_api.c
    gcc: numpy/core/src/multiarray/nditer_constr.c
    gcc: numpy/core/src/multiarray/nditer_pywrap.c
    gcc: numpy/core/src/multiarray/number.c
    gcc: numpy/core/src/multiarray/numpymemoryview.c
    gcc: numpy/core/src/multiarray/numpyos.c
    numpy/core/src/multiarray/numpyos.c:18:10: fatal error: xlocale.h: No such file or directory
     #include <xlocale.h>
              ^~~~~~~~~~~
    compilation terminated.
    numpy/core/src/multiarray/numpyos.c:18:10: fatal error: xlocale.h: No such file or directory
     #include <xlocale.h>
              ^~~~~~~~~~~
    compilation terminated.
    error: Command "gcc -pthread -B /home/ye/anaconda3/envs/paraphrase2/compiler_compat -Wl,--sysroot=/ -Wsign-compare -DNDEBUG -g -fwrapv -O3 -Wall -Wstrict-prototypes -fPIC -DHAVE_NPY_CONFIG_H=1 -D_FILE_OFFSET_BITS=64 -D_LARGEFILE_SOURCE=1 -D_LARGEFILE64_SOURCE=1 -Ibuild/src.linux-x86_64-3.6/numpy/core/src/private -Inumpy/core/include -Ibuild/src.linux-x86_64-3.6/numpy/core/include/numpy -Inumpy/core/src/private -Inumpy/core/src -Inumpy/core -Inumpy/core/src/npymath -Inumpy/core/src/multiarray -Inumpy/core/src/umath -Inumpy/core/src/npysort -I/home/ye/anaconda3/envs/paraphrase2/include/python3.6m -Ibuild/src.linux-x86_64-3.6/numpy/core/src/private -Ibuild/src.linux-x86_64-3.6/numpy/core/src/private -Ibuild/src.linux-x86_64-3.6/numpy/core/src/private -c numpy/core/src/multiarray/numpyos.c -o build/temp.linux-x86_64-3.6/numpy/core/src/multiarray/numpyos.o" failed with exit status 1
    ----------------------------------------
ERROR: Command errored out with exit status 1: /home/ye/anaconda3/envs/paraphrase2/bin/python -u -c 'import sys, setuptools, tokenize; sys.argv[0] = '"'"'/tmp/pip-install-e8uqgu5p/numpy_3a01c5fb02e74d0397f2d7519f7d13a8/setup.py'"'"'; __file__='"'"'/tmp/pip-install-e8uqgu5p/numpy_3a01c5fb02e74d0397f2d7519f7d13a8/setup.py'"'"';f=getattr(tokenize, '"'"'open'"'"', open)(__file__);code=f.read().replace('"'"'\r\n'"'"', '"'"'\n'"'"');f.close();exec(compile(code, __file__, '"'"'exec'"'"'))' install --record /tmp/pip-record-0dg78g5q/install-record.txt --single-version-externally-managed --compile --install-headers /home/ye/anaconda3/envs/paraphrase2/include/python3.6m/numpy Check the logs for full command output.
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ 
```

အဲဒါနဲ့ သပ်သပ်စီ လက်ရှိ Conda environment မှာ ပဲ version ကို မကန့်သတ်ပဲ installation လုပ်ကြည့်ခဲ့...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ pip install numpy
Collecting numpy
  Using cached numpy-1.19.5-cp36-cp36m-manylinux2010_x86_64.whl (14.8 MB)
Installing collected packages: numpy
Successfully installed numpy-1.19.5
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ python
Python 3.6.13 |Anaconda, Inc.| (default, Jun  4 2021, 14:25:59) 
[GCC 7.5.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import numpy
>>> print(numpy.__version__)
1.19.5
>>> exit()
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$
```

tensorflow ကို အောက်ပါအတိုင်း install လုပ်ခဲ့...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ pip install tensorflow

(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ python
Python 3.6.13 |Anaconda, Inc.| (default, Jun  4 2021, 14:25:59) 
[GCC 7.5.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
>>> print(tf.__version__)
2.6.0
>>> exit()
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$
```

gensim ကို အောက်ပါ အတိုင်း install လုပ်ခဲ့တယ်...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ python
Python 3.6.13 |Anaconda, Inc.| (default, Jun  4 2021, 14:25:59) 
[GCC 7.5.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import gensim
>>> print(gensim.__version__)
4.1.0
>>> exit()
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ 
```

nltk ကိုလည်း အောက်ပါအတိုင်း install လုပ်ခဲ့...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ pip install nltk
Collecting nltk
  Using cached nltk-3.6.2-py3-none-any.whl (1.5 MB)
Collecting regex
  Downloading regex-2021.8.28-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (745 kB)
     |████████████████████████████████| 745 kB 1.7 MB/s 
Collecting joblib
  Using cached joblib-1.0.1-py3-none-any.whl (303 kB)
Collecting click
  Downloading click-8.0.1-py3-none-any.whl (97 kB)
     |████████████████████████████████| 97 kB 8.8 MB/s 
Collecting tqdm
  Downloading tqdm-4.62.2-py2.py3-none-any.whl (76 kB)
     |████████████████████████████████| 76 kB 5.6 MB/s 
Requirement already satisfied: importlib-metadata in /home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages (from click->nltk) (4.8.1)
Requirement already satisfied: typing-extensions>=3.6.4 in /home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages (from importlib-metadata->click->nltk) (3.7.4.3)
Requirement already satisfied: zipp>=0.5 in /home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages (from importlib-metadata->click->nltk) (3.5.0)
Installing collected packages: tqdm, regex, joblib, click, nltk
Successfully installed click-8.0.1 joblib-1.0.1 nltk-3.6.2 regex-2021.8.28 tqdm-4.62.2
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ python
Python 3.6.13 |Anaconda, Inc.| (default, Jun  4 2021, 14:25:59) 
[GCC 7.5.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import nltk
>>> print(nltk.__version__)
3.6.2
>>> exit()
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$
```

## git clone "Deep Siamese Text Similarity"

git clone ဆိုတဲ့ command နဲ့ ကိုယ့်စက်ထဲကို download လုပ်ယူခဲ့...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ git clone https://github.com/dhwajraj/deep-siamese-text-similarity
Cloning into 'deep-siamese-text-similarity'...
remote: Enumerating objects: 98, done.
remote: Total 98 (delta 0), reused 0 (delta 0), pack-reused 98
Unpacking objects: 100% (98/98), 1.37 MiB | 3.83 MiB/s, done.
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2$ cd deep-siamese-text-similarity/
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ ls
eval.py  input_helpers.py  LICENSE  person_match.train2  preprocess.py  README.md  siamese_network.py  siamese_network_semantic.py  train.py
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ 
```

## Call --help

train.py က python 2.7 version နဲ့ လား?!  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ python ./train.py 
Traceback (most recent call last):
  File "./train.py", line 10, in <module>
    from input_helpers import InputHelper
  File "/home/ye/exp/myPara2/deep-siamese-text-similarity/input_helpers.py", line 211
    print len(vocab_processor.vocabulary_)
            ^
SyntaxError: invalid syntax
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$
```

ဝင်ကြည့်တော့ train.py ကတော့ python3 နဲ့ ရေးထားတာ...  
input_helpers.py ကပဲ python2.7 နဲ့ ရေးထားတာ လား?!...  

ဒီတစ်ကြောင်းပဲ လို့ထင်တယ်။  

```
        print len(vocab_processor.vocabulary_)
```

အဲဒီ တစ်ကြောင်းကို bracket ခတ်ပြီး ထပ် run ကြည့်ခဲ့... အောက်ပါအတိုင်း error ပေးတယ်။  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ python ./train.py 
Traceback (most recent call last):
  File "./train.py", line 10, in <module>
    from input_helpers import InputHelper
  File "/home/ye/exp/myPara2/deep-siamese-text-similarity/input_helpers.py", line 8, in <module>
    from tensorflow.contrib import learn
ModuleNotFoundError: No module named 'tensorflow.contrib'
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$
```

tensorflow က မြင့်နေတယ် လျှော့ရမှာမို့ လက်ရှိ ရှိပြီးသား tensorflow ကို uninstall လုပ်ခဲ့...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ pip uninstall tensorflow
Found existing installation: tensorflow 2.6.0
Uninstalling tensorflow-2.6.0:
  Would remove:
    /home/ye/anaconda3/envs/paraphrase2/bin/estimator_ckpt_converter
    /home/ye/anaconda3/envs/paraphrase2/bin/import_pb_to_tensorboard
    /home/ye/anaconda3/envs/paraphrase2/bin/saved_model_cli
    /home/ye/anaconda3/envs/paraphrase2/bin/tensorboard
    /home/ye/anaconda3/envs/paraphrase2/bin/tf_upgrade_v2
    /home/ye/anaconda3/envs/paraphrase2/bin/tflite_convert
    /home/ye/anaconda3/envs/paraphrase2/bin/toco
    /home/ye/anaconda3/envs/paraphrase2/bin/toco_from_protos
    /home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow-2.6.0.dist-info/*
    /home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/*
Proceed (y/n)? y
  Successfully uninstalled tensorflow-2.6.0
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$
```

tensorflow==1.2.1 ကို install လုပ်ခဲ့...   

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ pip install tensorflow==1.2.1
Collecting tensorflow==1.2.1
  Using cached tensorflow-1.2.1-cp36-cp36m-manylinux1_x86_64.whl (35.0 MB)
Collecting html5lib==0.9999999
  Using cached html5lib-0.9999999-py3-none-any.whl
Requirement already satisfied: wheel>=0.26 in /home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages (from tensorflow==1.2.1) (0.37.0)
Requirement already satisfied: markdown>=2.6.8 in /home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages (from tensorflow==1.2.1) (3.3.4)
Requirement already satisfied: protobuf>=3.2.0 in /home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages (from tensorflow==1.2.1) (3.17.3)
Requirement already satisfied: six>=1.10.0 in /home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages (from tensorflow==1.2.1) (1.15.0)
Requirement already satisfied: werkzeug>=0.11.10 in /home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages (from tensorflow==1.2.1) (2.0.1)
Collecting bleach==1.5.0
  Using cached bleach-1.5.0-py2.py3-none-any.whl (17 kB)
Collecting backports.weakref==1.0rc1
  Using cached backports.weakref-1.0rc1-py3-none-any.whl (4.3 kB)
Requirement already satisfied: numpy>=1.11.0 in /home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages (from tensorflow==1.2.1) (1.19.5)
Requirement already satisfied: importlib-metadata in /home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages (from markdown>=2.6.8->tensorflow==1.2.1) (4.8.1)
Requirement already satisfied: dataclasses in /home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages (from werkzeug>=0.11.10->tensorflow==1.2.1) (0.8)
Requirement already satisfied: typing-extensions>=3.6.4 in /home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages (from importlib-metadata->markdown>=2.6.8->tensorflow==1.2.1) (3.7.4.3)
Requirement already satisfied: zipp>=0.5 in /home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages (from importlib-metadata->markdown>=2.6.8->tensorflow==1.2.1) (3.5.0)
Installing collected packages: html5lib, bleach, backports.weakref, tensorflow
Successfully installed backports.weakref-1.0rc1 bleach-1.5.0 html5lib-0.9999999 tensorflow-1.2.1
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$
```

install လုပ်ခဲ့တဲ့ tensorflow ကို import လုပ်ကြည့်ခဲ့...   

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ python
Python 3.6.13 |Anaconda, Inc.| (default, Jun  4 2021, 14:25:59) 
[GCC 7.5.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:458: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:459: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:460: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:461: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:462: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:465: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])
>>> print(tensorflow.__version__)
1.2.1
>>> 
```

train.py ကို ထပ် run ကြည့်ခဲ့...   

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ python ./train.py
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:458: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:459: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:460: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:461: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:462: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:465: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])
Traceback (most recent call last):
  File "./train.py", line 10, in <module>
    from input_helpers import InputHelper
  File "/home/ye/exp/myPara2/deep-siamese-text-similarity/input_helpers.py", line 14, in <module>
    reload(sys)
NameError: name 'reload' is not defined
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$
```

Trying to fix above error message!  
Ref: https://stackoverflow.com/questions/10142764/nameerror-name-reload-is-not-defined/10142772  

code ကို ဝင်ပြင်ခဲ့တယ်...   

```python
# added by Ye
from importlib import reload

#reload(sys)
#sys.setdefaultencoding("utf-8")

if sys.version[0] == '2':
    reload(sys)
    sys.setdefaultencoding("utf-8")
```

ထပ် error ရတယ်။  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ python ./train.py
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:458: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:459: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:460: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:461: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:462: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:465: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])
Traceback (most recent call last):
  File "./train.py", line 12, in <module>
    from siamese_network_semantic import SiameseLSTMw2v
  File "/home/ye/exp/myPara2/deep-siamese-text-similarity/siamese_network_semantic.py", line 55
    print self.embedded_words1
             ^
SyntaxError: Missing parentheses in call to 'print'. Did you mean print(self.embedded_words1)?
```


(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ gedit siamese_network_semantic.py  


```python
        print (self.embedded_words1)
```

ထပ် run ကြည့်တယ်...   
အောက်ပါ error ရတယ်...    

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ python ./train.py
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:458: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:459: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:460: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:461: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:462: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:465: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])

Parameters:
ALLOW_SOFT_PLACEMENT=True
BATCH_SIZE=64
CHECKPOINT_EVERY=1000
DROPOUT_KEEP_PROB=1.0
EMBEDDING_DIM=300
EVALUATE_EVERY=1000
HIDDEN_UNITS=50
IS_CHAR_BASED=True
L2_REG_LAMBDA=0.0
LOG_DEVICE_PLACEMENT=False
NUM_EPOCHS=300
TRAINING_FILES=person_match.train2
WORD2VEC_FORMAT=text
WORD2VEC_MODEL=wiki.simple.vec

Loading training data from person_match.train2
Traceback (most recent call last):
  File "./train.py", line 56, in <module>
    FLAGS.batch_size, FLAGS.is_char_based)
  File "/home/ye/exp/myPara2/deep-siamese-text-similarity/input_helpers.py", line 177, in getDataSets
    x1_text, x2_text, y=self.getTsvDataCharBased(training_paths)
  File "/home/ye/exp/myPara2/deep-siamese-text-similarity/input_helpers.py", line 111, in getTsvDataCharBased
    for i in xrange(len(combined)):
NameError: name 'xrange' is not defined

```

ဒီ error ကတော့ python 3 နဲ့ 2.7 ကြားမှာ ဖြစ်နေတဲ့ ပုံမှန်ကိစ္စပါ။   
ဖြေရှင်းရလွယ်ပါတယ်။   


input_helpers.py ဖိုင်မှာ အောက်ပါအတိုင်း ဝင်ပြင်ခဲ့...   

```python
#        for i in xrange(len(combined)):
        for i in range(len(combined)):
```

ထပ် run ကြည့်ခဲ့တယ်။  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ python ./train.py
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:458: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:459: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:460: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:461: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:462: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:465: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])

Parameters:
ALLOW_SOFT_PLACEMENT=True
BATCH_SIZE=64
CHECKPOINT_EVERY=1000
DROPOUT_KEEP_PROB=1.0
EMBEDDING_DIM=300
EVALUATE_EVERY=1000
HIDDEN_UNITS=50
IS_CHAR_BASED=True
L2_REG_LAMBDA=0.0
LOG_DEVICE_PLACEMENT=False
NUM_EPOCHS=300
TRAINING_FILES=person_match.train2
WORD2VEC_FORMAT=text
WORD2VEC_MODEL=wiki.simple.vec

Loading training data from person_match.train2
Building vocabulary
Length of loaded vocabulary =79
dumping validation 0
Train/Dev split for person_match.train2: 35634/3960
starting graph def
2021-09-14 11:05:33.801056: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.1 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 11:05:33.801071: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.2 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 11:05:33.801075: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 11:05:33.801078: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX2 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 11:05:33.801081: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use FMA instructions, but these are available on your machine and could speed up CPU computations.
started session
[<tf.Tensor 'output/unstack:0' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:1' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:2' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:3' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:4' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:5' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:6' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:7' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:8' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:9' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:10' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:11' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:12' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:13' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:14' shape=(?, 300) dtype=float32>]
[<tf.Tensor 'output/unstack_1:0' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:1' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:2' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:3' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:4' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:5' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:6' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:7' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:8' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:9' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:10' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:11' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:12' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:13' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:14' shape=(?, 300) dtype=float32>]
initialized siameseModel object
defined training_ops
defined gradient summaries
Writing to /home/ye/exp/myPara2/deep-siamese-text-similarity/runs/1631592338

init all variables
Traceback (most recent call last):
  File "./train.py", line 236, in <module>
    for nn in xrange(sum_no_of_batches*FLAGS.num_epochs):
NameError: name 'xrange' is not defined
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ 
```

xrange နဲ့ ပတ်သက်တဲ့ error ပါပဲ...   

gedit train.py နဲ့ အောက်ပါအတိုင်း ဝင်ပြင်ခဲ့...  

```python
#    for nn in xrange(sum_no_of_batches*FLAGS.num_epochs):
    for nn in range(sum_no_of_batches*FLAGS.num_epochs):    
```

ထပ် run ကြည့်ခဲ့...  
အောက်ပါအတိုင်း error အသစ် တစ်ခု ထပ်တွေ့ခဲ့...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ python ./train.py
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:458: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:459: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:460: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:461: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:462: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:465: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])

Parameters:
ALLOW_SOFT_PLACEMENT=True
BATCH_SIZE=64
CHECKPOINT_EVERY=1000
DROPOUT_KEEP_PROB=1.0
EMBEDDING_DIM=300
EVALUATE_EVERY=1000
HIDDEN_UNITS=50
IS_CHAR_BASED=True
L2_REG_LAMBDA=0.0
LOG_DEVICE_PLACEMENT=False
NUM_EPOCHS=300
TRAINING_FILES=person_match.train2
WORD2VEC_FORMAT=text
WORD2VEC_MODEL=wiki.simple.vec

Loading training data from person_match.train2
Building vocabulary
Length of loaded vocabulary =79
dumping validation 0
Train/Dev split for person_match.train2: 35634/3960
starting graph def
2021-09-14 11:10:30.444166: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.1 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 11:10:30.444182: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.2 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 11:10:30.444186: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 11:10:30.444189: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX2 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 11:10:30.444192: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use FMA instructions, but these are available on your machine and could speed up CPU computations.
started session
[<tf.Tensor 'output/unstack:0' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:1' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:2' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:3' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:4' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:5' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:6' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:7' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:8' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:9' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:10' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:11' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:12' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:13' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:14' shape=(?, 300) dtype=float32>]
[<tf.Tensor 'output/unstack_1:0' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:1' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:2' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:3' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:4' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:5' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:6' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:7' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:8' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:9' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:10' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:11' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:12' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:13' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:14' shape=(?, 300) dtype=float32>]
initialized siameseModel object
defined training_ops
defined gradient summaries
Writing to /home/ye/exp/myPara2/deep-siamese-text-similarity/runs/1631592634

init all variables
Traceback (most recent call last):
  File "./train.py", line 238, in <module>
    batch = batches.next()
AttributeError: 'generator' object has no attribute 'next'

```

Ref: https://stackoverflow.com/questions/21622193/python-3-2-coroutine-attributeerror-generator-object-has-no-attribute-next/21622696  
အောက်ပါအတိုင်း ဝင်ပြင်ဆင်ခဲ့...   

```
#        batch = batches.next()
        batch = next()        
```

အောက်ပါအတိုင်း Error ထပ် ရခဲ့...   

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ python ./train.py
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:458: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:459: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:460: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:461: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:462: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:465: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])

Parameters:
ALLOW_SOFT_PLACEMENT=True
BATCH_SIZE=64
CHECKPOINT_EVERY=1000
DROPOUT_KEEP_PROB=1.0
EMBEDDING_DIM=300
EVALUATE_EVERY=1000
HIDDEN_UNITS=50
IS_CHAR_BASED=True
L2_REG_LAMBDA=0.0
LOG_DEVICE_PLACEMENT=False
NUM_EPOCHS=300
TRAINING_FILES=person_match.train2
WORD2VEC_FORMAT=text
WORD2VEC_MODEL=wiki.simple.vec

Loading training data from person_match.train2
Building vocabulary
Length of loaded vocabulary =79
dumping validation 0
Train/Dev split for person_match.train2: 35634/3960
starting graph def
2021-09-14 11:13:18.382838: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.1 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 11:13:18.382854: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.2 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 11:13:18.382858: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 11:13:18.382861: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX2 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 11:13:18.382864: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use FMA instructions, but these are available on your machine and could speed up CPU computations.
started session
[<tf.Tensor 'output/unstack:0' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:1' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:2' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:3' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:4' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:5' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:6' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:7' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:8' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:9' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:10' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:11' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:12' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:13' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:14' shape=(?, 300) dtype=float32>]
[<tf.Tensor 'output/unstack_1:0' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:1' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:2' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:3' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:4' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:5' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:6' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:7' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:8' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:9' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:10' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:11' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:12' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:13' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:14' shape=(?, 300) dtype=float32>]
initialized siameseModel object
defined training_ops
defined gradient summaries
Writing to /home/ye/exp/myPara2/deep-siamese-text-similarity/runs/1631592802

init all variables
Traceback (most recent call last):
  File "./train.py", line 239, in <module>
    batch = next()        
TypeError: next expected at least 1 arguments, got 0

```

အောက်ပါအတိုင်း ပြင်ပြီး ထပ် run ကြည့်ခဲ့...  
Ref: https://stackoverflow.com/questions/31860030/typeerror-next-expected-at-least-1-arguments-got-0-i-am-trying-to-iterate-thro   

```
#        batch = batches.next()
        batch = reader.next()     
```

အောက်ပါအတိုင်း error ရခဲ့...   

```
tput/unstack_1:7' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:8' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:9' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:10' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:11' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:12' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:13' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:14' shape=(?, 300) dtype=float32>]
initialized siameseModel object
defined training_ops
defined gradient summaries
Writing to /home/ye/exp/myPara2/deep-siamese-text-similarity/runs/1631592933

init all variables
Traceback (most recent call last):
  File "./train.py", line 239, in <module>
    batch = reader.next()        
NameError: name 'reader' is not defined
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ 
```

အောက်ပါအတိုင်း error ပေးတယ်။  

```
k_1:14' shape=(?, 300) dtype=float32>]
initialized siameseModel object
defined training_ops
defined gradient summaries
Writing to /home/ye/exp/myPara2/deep-siamese-text-similarity/runs/1631593044

init all variables
Traceback (most recent call last):
  File "./train.py", line 240, in <module>
    batch = next(reader, None)
NameError: name 'reader' is not defined
```

Ref: https://community.dataquest.io/t/guided-project-1-name-error-name-reader-is-not-defined/363909  
အောက်ပါအတိုင်း update လုပ်ခဲ့...    

```
## added by Ye
from csv import reader
```

ဒီတစ်ခါ run ကြည့်တော့ အောက်ပါအတိုင်း error အသစ် ထပ်ရခဲ့...    

```
tput/unstack_1:7' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:8' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:9' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:10' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:11' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:12' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:13' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:14' shape=(?, 300) dtype=float32>]
initialized siameseModel object
defined training_ops
defined gradient summaries
Writing to /home/ye/exp/myPara2/deep-siamese-text-similarity/runs/1631593180

init all variables
Traceback (most recent call last):
  File "./train.py", line 244, in <module>
    batch = next(reader, None)
TypeError: 'builtin_function_or_method' object is not an iterator
```

ငါက သေချာ မကြည့်ပဲ ကမမ်းကတမ်း debugging လုပ်နေခဲ့....  
နည်းနည်း ပြန်စဉ်းစားကြည့်ပြီး လုပ်တော့ ရသွားခဲ့  

Ref: https://stackoverflow.com/questions/1073396/is-generator-next-visible-in-python-3  
ပြင်ခဲ့တာက အောက်ပါအတိုင်း  

```python
        batch = batches.__next__()
```

ဒီ တစ်ခေါက် run တော့ training လုပ်နေပြီ... ရလဒ်ကို ကြည့်ရအောင်...  



