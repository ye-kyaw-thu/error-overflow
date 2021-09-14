# Deep Siamese Text Similarity Experiment Log

Siamese Network ကို စိတ်ဝင်စားတယ်။  
ဒါပေမဲ့ develop လုပ်ခဲ့တာတွေက Python2.7 တို့ လွန်ခဲ့တဲ့ ၃နှစ် ၄နှစ် ပတ်ဝန်းကျင်က source code တွေဖြစ်တာ များတော့ ကျောင်းသားတွေအနေနဲ့က ကိုယ်စက်ထဲမှာ download လုပ်ပြီး run ကြတဲ့အခါမှာ သိပ်အလွယ်ကြီး မဟုတ်ဘူး။ ကိုယ်တိုင်လည်း အတွေ့အကြုံက ရှိပေမဲ့ အတိုင်းအတာ တစ်ခုအထိ အချိန်ပေးရတာ များပါတယ်။  

ဒီတစ်ခါတော့ Deep Siamese ဆိုတာကို မြင့်မြင့်ဌေး (Ph.D. candidate, UTYCC) က ပြင်ဆင်ပေးထားတဲ့ မြန်မာစာ paraphrase ဒေတာတွေနဲ့ ကိုယ့်စက်ထဲမှာ run ဖို့ ပြင်ခဲ့စဉ်က log တစ်ခုလုံးကို လေ့လာနိုင်အောင်လို့ တင်ပေးထားလိုက်တာပါ။ တင်ထားတာက debug လုပ်လိုက် run ကြည့်လိုက်လုပ်ထားတဲ့ တကယ့် running/debugging log မို့လို့... ဒီ log ကို ဖတ်ကြည့်ပြီး လုပ်တဲ့သူတွေက မလိုအပ်တဲ့ အဆင့်တွေကို ကျော်ပြီးလုပ်သွားပါ။ ကြိုတော့ ပြောထားပါမယ် စက်တစ်လုံးနဲ့ တစ်လုံး ပေးတဲ့ error တွေက တသွေမသိမ်း တူချင်မှ တူပါလိမ့်မယ်။ reference တော့ ဖြစ်ပါလိမ့်မယ်။   

source code link: https://github.com/dhwajraj/deep-siamese-text-similarity

Enjoy! Debugging... :)  

y@Lab  
14 Sept 2021  


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

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ python ./train.py  
...  
...  
...  
```

![Deep-Siamese-Neural-Network](https://github.com/ye-kyaw-thu/error-overflow/blob/master/gif/after-the-debugging-deep-siamese-14Sept2021.gif)  

```
...
...
...
TRAIN 2021-09-14T12:52:53.163634: step 166792, loss 0.0172597, acc 0.96875
(1, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 1, 0, 1, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 1) [0.31412908 0.9472017  0.8342849  0.94143677 0.8847903  0.0454561
 0.3258683  0.91602916 0.962336   0.83891857 0.94244224 0.14618705
 0.92063123 0.25486535 0.98484814 0.7835809  0.98584193 0.05259424
 0.9898238  0.04903809 0.74376386 0.88932794 0.9891549  0.28035152
 0.0395739  0.91201115 0.76439553 0.9942868  0.91708815 0.904904
 0.81075585 0.22059423 0.9301315  0.7962086  0.7017909  0.08430753
 0.22638889 0.940203   0.5132914  0.88745373 0.9592978  0.97745895
 0.9950065  0.99586034 0.79326105 0.1892063  0.11887218 0.987077
 0.8930826  0.9856127  0.9870875  0.90667975 0.16764142 0.8836336
 0.9808654  0.92079264 0.99744445 0.07678524 0.9886437  0.73951566
 0.96967727 0.04719291 0.81923836 0.16062222] [1. 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 1. 0. 1. 0. 0. 0. 1. 0. 1. 0. 0. 0. 1.
 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 1. 0.
 0. 0. 0. 0. 1. 0. 0. 0. 0. 1. 0. 0. 0. 1. 0. 1.]
TRAIN 2021-09-14T12:52:53.192084: step 166793, loss 0.0126628, acc 0.96875
(0, 0, 0, 1, 0, 0, 0, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 1, 1, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 0, 1, 0, 1, 0, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1) [0.96866083 0.9500661  0.9600809  0.11584707 0.97335356 0.96794266
 0.9208151  0.19575799 0.93874717 0.07115714 0.3552479  0.9733194
 0.9950825  0.17129272 0.9336412  0.99230933 0.73479986 0.95657086
 0.07029311 0.16035047 0.23395155 0.91992366 0.1112964  0.84904605
 0.9988648  0.85323477 0.8998303  0.72136605 0.9867472  0.89994395
 0.96772164 0.9694394  0.36777526 0.9888469  0.28544316 0.10342429
 0.9987994  0.16361912 0.93631727 0.03067869 0.91499627 0.10124926
 0.5916933  0.95647424 0.90382844 0.9904221  0.5180281  0.9151575
 0.9326466  0.99763846 0.9603038  0.98879105 0.18480147 0.770629
 0.92313594 0.9984981  0.97045135 0.99002343 0.85486007 0.88244617
 0.9928645  0.921692   0.9039935  0.04515807] [0. 0. 0. 1. 0. 0. 0. 1. 0. 1. 1. 0. 0. 1. 0. 0. 0. 0. 1. 1. 1. 0. 1. 0.
 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 1. 0. 1. 0. 1. 0. 1. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1.]
TRAIN 2021-09-14T12:52:53.222235: step 166794, loss 0.0216152, acc 0.96875
(0, 0, 1, 0, 0, 1, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0) [0.9338377  0.9855416  0.07116676 0.8462816  0.9893753  0.19450073
 0.98013294 0.22659315 0.9682291  0.5984183  0.20403202 0.21405211
 0.1407054  0.9838736  0.9130343  0.5260561  0.88417923 0.8702493
 0.9677027  0.9130299  0.9989529  0.96173024 0.9935983  0.34404814
 0.89272827 0.8095023  0.6775013  0.8641295  0.97430915 0.93448544
 0.99505174 0.05725923 0.97179395 0.94586784 0.00906982 0.2045267
 0.08466621 0.99553156 0.93985546 0.9615806  0.10546374 0.9594052
 0.93827707 0.977727   0.77176636 0.8051426  0.3108686  0.99071145
 0.9986269  0.31569037 0.98801136 0.9272618  0.36308065 0.99658865
 0.7529656  0.8335037  0.85571885 0.02680121 0.89626575 0.16354796
 0.71365863 0.8485417  0.944978   0.5684366 ] [0. 0. 1. 0. 0. 1. 0. 1. 0. 0. 1. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1.
 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 0.
 0. 1. 0. 0. 1. 0. 0. 0. 0. 1. 0. 1. 0. 0. 0. 0.]
TRAIN 2021-09-14T12:52:53.250522: step 166795, loss 0.00914215, acc 1
(1, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 1, 0, 1, 0, 1, 0, 1, 1, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 1, 1, 0, 1, 0) [0.1302759  0.8943918  0.98038656 0.9377423  0.17209056 0.9986228
 0.22382711 0.9032577  0.9973197  0.9983012  0.94730586 0.9865154
 0.9978207  0.8481764  0.9354756  0.22823492 0.99887705 0.8472176
 0.8177258  0.9970969  0.17429706 0.04442819 0.1691791  0.8129638
 0.85300106 0.65399444 0.9814012  0.86128473 0.93420666 0.10305122
 0.23502143 0.85794646 0.06837418 0.83098257 0.20605631 0.90471035
 0.2010057  0.07091598 0.9422006  0.98841935 0.95584214 0.9327356
 0.0455367  0.93548715 0.97279245 0.9977002  0.06826435 0.8608919
 0.8242191  0.940601   0.06318019 0.99971205 0.9968645  0.9890988
 0.96283203 0.1895543  0.98454785 0.7958012  0.98335373 0.13120168
 0.46745148 0.874023   0.12290529 0.91805005] [1. 0. 0. 0. 1. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 1. 1. 1. 0.
 0. 0. 0. 0. 0. 1. 1. 0. 1. 0. 1. 0. 1. 1. 0. 0. 0. 0. 1. 0. 0. 0. 1. 0.
 0. 0. 1. 0. 0. 0. 0. 1. 0. 0. 0. 1. 1. 0. 1. 0.]
TRAIN 2021-09-14T12:52:53.277998: step 166796, loss 0.00904333, acc 1
(1, 0, 1, 0, 0, 0, 1, 1, 1, 0, 0, 1, 1, 0, 1, 0, 1, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0) [0.12227681 0.8116232  0.09217805 0.97560054 0.8977865  0.90276307
 0.1935017  0.26807338 0.07407202 0.98802865 0.88194025 0.24649434
 0.4288236  0.9044529  0.08125094 0.78029066 0.12942277 0.94619685
 0.12885162 0.09826298 0.96782184 0.9941437  0.9984174  0.7788837
 0.99547064 0.1300075  0.9195392  0.96698457 0.9862306  0.07714777
 0.98422146 0.9805879  0.03804657 0.9926557  0.96505773 0.0349653
 0.9867777  0.1380071  0.2893066  0.8528502  0.9888131  0.82301927
 0.997276   0.9037222  0.9758819  0.9711453  0.8804366  0.21634263
 0.90749097 0.9945798  0.97932523 0.9701122  0.9914099  0.10112519
 0.9049202  0.79145014 0.9862884  0.95478725 0.8722545  0.93093777
 0.3718555  0.213921   0.96344966 0.98343253] [1. 0. 1. 0. 0. 0. 1. 1. 1. 0. 0. 1. 1. 0. 1. 0. 1. 0. 1. 1. 0. 0. 0. 0.
 0. 1. 0. 0. 0. 1. 0. 0. 1. 0. 0. 1. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1.
 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 1. 0. 0.]
TRAIN 2021-09-14T12:52:53.309479: step 166797, loss 0.0208972, acc 0.96875
(1, 1, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 0) [0.12732257 0.35728988 0.9173491  0.96426857 0.8982434  0.9852271
 0.08697479 0.19722879 0.14979061 0.9535493  0.91036344 0.7938481
 0.88814956 0.05657158 0.9813739  0.08493002 0.9967467  0.8612445
 0.92323625 0.46215793 0.92097825 0.97683424 0.99152905 0.11291496
 0.98803174 0.99843127 0.9940544  0.9292116  0.91171557 0.90190166
 0.89055043 0.9831246  0.27410284 0.9987327  0.98413724 0.1053162
 0.19793847 0.9520745  0.8668291  0.99564046 0.91075116 0.8980968
 0.8910242  0.9052935  0.9822527  0.9172132  0.03130032 0.9773395
 0.10921101 0.8852061  0.8457821  0.9567743  0.9802818  0.89701587
 0.9878813  0.98003095 0.8701394  0.49614704 0.95294863 0.8668566
 0.83354086 0.97073674 0.10056475 0.9442775 ] [1. 1. 0. 0. 0. 0. 1. 1. 1. 0. 0. 0. 0. 1. 0. 1. 0. 0. 0. 1. 0. 0. 0. 1.
 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0.
 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 1. 0.]
TRAIN 2021-09-14T12:52:53.336943: step 166798, loss 0.0129476, acc 1
(1, 0, 1, 1, 0, 1, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 1, 1, 1, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 1, 0, 1, 1, 1, 1, 1, 0, 0) [0.15025859 0.7975618  0.20289978 0.28746074 0.99740803 0.09125511
 0.7798001  0.92772144 0.9983357  0.21794708 0.9990825  0.12198178
 0.7365132  0.9328592  0.9732431  0.99559456 0.03753405 0.9732832
 0.8082658  0.9923464  0.19371419 0.20517662 0.07903683 0.98912156
 0.9108874  0.9863896  0.6296402  0.0401975  0.85804856 0.99232465
 0.9632527  0.43523917 0.9669493  0.9300102  0.86285365 0.97762257
 0.91020465 0.99888474 0.2610489  0.6877237  0.10831592 0.98858577
 0.9842223  0.8004281  0.9973269  0.9308928  0.9733901  0.9568678
 0.9318343  0.24797732 0.2940566  0.02882019 0.9118704  0.9181558
 0.8052859  0.24905929 0.8751881  0.02494277 0.03845597 0.4646816
 0.1553733  0.02478833 0.94183403 0.99069905] [1. 0. 1. 1. 0. 1. 0. 0. 0. 1. 0. 1. 0. 0. 0. 0. 1. 0. 0. 0. 1. 1. 1. 0.
 0. 0. 0. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0. 0. 0. 0. 0. 0. 0.
 0. 1. 1. 1. 0. 0. 0. 1. 0. 1. 1. 1. 1. 1. 0. 0.]
TRAIN 2021-09-14T12:52:53.364905: step 166799, loss 0.0110675, acc 1
(1, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 1, 0, 0, 1, 0) [0.14208236 0.89500153 0.25742823 0.98619974 0.86474043 0.04040703
 0.9120324  0.8766869  0.11459201 0.8894361  0.87493914 0.18864411
 0.9624623  0.18748328 0.9518787  0.4001624  0.85122526 0.99514496
 0.1495677  0.05406529 0.7549388  0.83928347 0.98854953 0.7996011
 0.7732091  0.9792835  0.77746826 0.94324124 0.88399595 0.9958147
 0.96391195 0.18343858 0.96885276 0.217565   0.78878266 0.9548478
 0.94569546 0.83042747 0.1935929  0.9549087  0.9916679  0.9852316
 0.8680228  0.8040159  0.11863542 0.99648863 0.832604   0.9020687
 0.16454029 0.8841151  0.8587238  0.98409504 0.8475404  0.04677882
 0.4148259  0.70900404 0.916675   0.89931756 0.11098508 0.15137528
 0.9735436  0.9478729  0.02937397 0.9808598 ] [1. 0. 1. 0. 0. 1. 0. 0. 1. 0. 0. 1. 0. 1. 0. 1. 0. 0. 1. 1. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0.
 1. 0. 0. 0. 0. 1. 1. 0. 0. 0. 1. 1. 0. 0. 1. 0.]
TRAIN 2021-09-14T12:52:53.396726: step 166800, loss 0.0193407, acc 0.984375
(0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 1, 0, 0) [0.97265303 0.90968597 0.7356576  0.9816575  0.9785298  0.9242283
 0.8648083  0.09064282 0.834709   0.08185707 0.87201065 0.14452232
 0.01487786 0.95256877 0.97152925 0.29146734 0.72330135 0.98881656
 0.9769335  0.99313    0.781817   0.8398587  0.9987803  0.29737073
 0.33694202 0.9956376  0.81225866 0.8556662  0.962738   0.9802147
 0.42173705 0.9571966  0.11559749 0.96374327 0.05562472 0.98252845
 0.99796015 0.42668512 0.81573313 0.21335216 0.8759703  0.96754676
 0.8951805  0.16922542 0.18484795 0.2921868  0.22007763 0.9510128
 0.99874353 0.8721868  0.8879849  0.73691744 0.85864466 0.83461595
 0.12708123 0.9321396  0.07160352 0.9487504  0.16775413 0.84878516
 0.26673597 0.90002215 0.9702678  0.966103  ] [0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0. 1. 1. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 1.
 1. 0. 0. 0. 0. 0. 1. 0. 1. 0. 1. 0. 0. 1. 0. 1. 0. 0. 0. 1. 1. 1. 1. 0.
 0. 0. 0. 0. 0. 0. 1. 0. 1. 0. 1. 0. 1. 0. 0. 0.]
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$
```

အဆင်ပြေပြေနဲ့ training လုပ်တာ ပြီးသွားတယ်။   
CPU ရှစ်လုံးနဲ့ စက်မှာ ၁နာရီခွဲလောက်တော့ ကြာတယ်။  

## Check Trained Models

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/runs$ tree
.
├── 1631592338
│   ├── checkpoints
│   │   ├── graphpb.txt
│   │   └── vocab
│   └── summaries
│       ├── dev
│       │   └── events.out.tfevents.1631592339.administrator-HP-Z2-Tower-G4-Workstation
│       └── train
│           └── events.out.tfevents.1631592338.administrator-HP-Z2-Tower-G4-Workstation
├── 1631592634
│   ├── checkpoints
│   │   ├── graphpb.txt
│   │   └── vocab
│   └── summaries
│       ├── dev
│       │   └── events.out.tfevents.1631592635.administrator-HP-Z2-Tower-G4-Workstation
│       └── train
│           └── events.out.tfevents.1631592635.administrator-HP-Z2-Tower-G4-Workstation
├── 1631592802
│   ├── checkpoints
│   │   ├── graphpb.txt
│   │   └── vocab
│   └── summaries
│       ├── dev
│       │   └── events.out.tfevents.1631592803.administrator-HP-Z2-Tower-G4-Workstation
│       └── train
│           └── events.out.tfevents.1631592803.administrator-HP-Z2-Tower-G4-Workstation
├── 1631592933
│   ├── checkpoints
│   │   ├── graphpb.txt
│   │   └── vocab
│   └── summaries
│       ├── dev
│       │   └── events.out.tfevents.1631592935.administrator-HP-Z2-Tower-G4-Workstation
│       └── train
│           └── events.out.tfevents.1631592934.administrator-HP-Z2-Tower-G4-Workstation
├── 1631593044
│   ├── checkpoints
│   │   ├── graphpb.txt
│   │   └── vocab
│   └── summaries
│       ├── dev
│       │   └── events.out.tfevents.1631593045.administrator-HP-Z2-Tower-G4-Workstation
│       └── train
│           └── events.out.tfevents.1631593044.administrator-HP-Z2-Tower-G4-Workstation
├── 1631593180
│   ├── checkpoints
│   │   ├── graphpb.txt
│   │   └── vocab
│   └── summaries
│       ├── dev
│       │   └── events.out.tfevents.1631593181.administrator-HP-Z2-Tower-G4-Workstation
│       └── train
│           └── events.out.tfevents.1631593180.administrator-HP-Z2-Tower-G4-Workstation
├── 1631593513
│   ├── checkpoints
│   │   ├── graphpb.txt
│   │   └── vocab
│   └── summaries
│       ├── dev
│       │   └── events.out.tfevents.1631593514.administrator-HP-Z2-Tower-G4-Workstation
│       └── train
│           └── events.out.tfevents.1631593513.administrator-HP-Z2-Tower-G4-Workstation
└── 1631593567
    ├── checkpoints
    │   ├── checkpoint
    │   ├── graphpb.txt
    │   ├── model
    │   │   ├── graph12999.pb
    │   │   ├── graph1999.pb
    │   │   ├── graph2999.pb
    │   │   ├── graph4999.pb
    │   │   ├── graph6999.pb
    │   │   ├── graph9999.pb
    │   │   └── graph999.pb
    │   ├── model-10000.data-00000-of-00001
    │   ├── model-10000.index
    │   ├── model-10000.meta
    │   ├── model-1000.data-00000-of-00001
    │   ├── model-1000.index
    │   ├── model-1000.meta
    │   ├── model-13000.data-00000-of-00001
    │   ├── model-13000.index
    │   ├── model-13000.meta
    │   ├── model-2000.data-00000-of-00001
    │   ├── model-2000.index
    │   ├── model-2000.meta
    │   ├── model-3000.data-00000-of-00001
    │   ├── model-3000.index
    │   ├── model-3000.meta
    │   ├── model-5000.data-00000-of-00001
    │   ├── model-5000.index
    │   ├── model-5000.meta
    │   ├── model-7000.data-00000-of-00001
    │   ├── model-7000.index
    │   ├── model-7000.meta
    │   └── vocab
    └── summaries
        ├── dev
        │   └── events.out.tfevents.1631593568.administrator-HP-Z2-Tower-G4-Workstation
        └── train
            └── events.out.tfevents.1631593567.administrator-HP-Z2-Tower-G4-Workstation

41 directories, 61 files
```
## Learn Command-line Arguments Through --help

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ python ./train.py -h
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
usage: train.py [-h] [--is_char_based [IS_CHAR_BASED]] [--nois_char_based]
                [--word2vec_model WORD2VEC_MODEL]
                [--word2vec_format WORD2VEC_FORMAT]
                [--embedding_dim EMBEDDING_DIM]
                [--dropout_keep_prob DROPOUT_KEEP_PROB]
                [--l2_reg_lambda L2_REG_LAMBDA]
                [--training_files TRAINING_FILES]
                [--hidden_units HIDDEN_UNITS] [--batch_size BATCH_SIZE]
                [--num_epochs NUM_EPOCHS] [--evaluate_every EVALUATE_EVERY]
                [--checkpoint_every CHECKPOINT_EVERY]
                [--allow_soft_placement [ALLOW_SOFT_PLACEMENT]]
                [--noallow_soft_placement]
                [--log_device_placement [LOG_DEVICE_PLACEMENT]]
                [--nolog_device_placement]

optional arguments:
  -h, --help            show this help message and exit
  --is_char_based [IS_CHAR_BASED]
                        is character based syntactic similarity. if false then
                        word embedding based semantic similarity is
                        used.(default: True)
  --nois_char_based
  --word2vec_model WORD2VEC_MODEL
                        word2vec pre-trained embeddings file (default: None)
  --word2vec_format WORD2VEC_FORMAT
                        word2vec pre-trained embeddings file format
                        (bin/text/textgz)(default: None)
  --embedding_dim EMBEDDING_DIM
                        Dimensionality of character embedding (default: 300)
  --dropout_keep_prob DROPOUT_KEEP_PROB
                        Dropout keep probability (default: 1.0)
  --l2_reg_lambda L2_REG_LAMBDA
                        L2 regularizaion lambda (default: 0.0)
  --training_files TRAINING_FILES
                        training file (default: None)
  --hidden_units HIDDEN_UNITS
                        Number of hidden units (default:50)
  --batch_size BATCH_SIZE
                        Batch Size (default: 64)
  --num_epochs NUM_EPOCHS
                        Number of training epochs (default: 200)
  --evaluate_every EVALUATE_EVERY
                        Evaluate model on dev set after this many steps
                        (default: 100)
  --checkpoint_every CHECKPOINT_EVERY
                        Save model after this many steps (default: 100)
  --allow_soft_placement [ALLOW_SOFT_PLACEMENT]
                        Allow device soft device placement
  --noallow_soft_placement
  --log_device_placement [LOG_DEVICE_PLACEMENT]
                        Log placement of ops on devices
  --nolog_device_placement
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$
```

## Evaluation

Evaluation ကို မော်ဒယ် တစ်ခုနဲ့ လုပ်ကြည့်တော့ အောက်ပါအတိုင်း python version error ပေး...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python eval.py --model ./runs/1631593567/checkpoints/model/graph9999.pb 
  File "eval.py", line 45
    print checkpoint_file
                        ^
SyntaxError: Missing parentheses in call to 'print'. Did you mean print(checkpoint_file)?

real	0m0.038s
user	0m0.027s
sys	0m0.012s
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$
```

Fixed followings:   

```
print (checkpoint_file)
...
...
        for ex in all_predictions:
            print (ex)
```

eval လုပ်ကြည့်တော့...  
အောက်ပါအတိုင်း vocab ဖိုင်ရှာမတွေ့ကြောင်း error ပေးတယ်...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python eval.py --model ./runs/1631593567/checkpoints/model/graph9999.pb 
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
CHECKPOINT_DIR=
EVAL_FILEPATH=validation.txt0
LOG_DEVICE_PLACEMENT=False
MODEL=./runs/1631593567/checkpoints/model/graph9999.pb
VOCAB_FILEPATH=runs/1512222837/checkpoints/vocab

Loading testing/labelled data from validation.txt0
Traceback (most recent call last):
  File "eval.py", line 38, in <module>
    x1_test,x2_test,y_test = inpH.getTestDataSet(FLAGS.eval_filepath, FLAGS.vocab_filepath, 30)
  File "/home/ye/exp/myPara2/deep-siamese-text-similarity/input_helpers.py", line 219, in getTestDataSet
    vocab_processor = vocab_processor.restore(vocab_path)
  File "/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/contrib/learn/python/learn/preprocessing/text.py", line 226, in restore
    return pickle.loads(f.read())
  File "/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/lib/io/file_io.py", line 118, in read
    self._preread_check()
  File "/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/lib/io/file_io.py", line 78, in _preread_check
    compat.as_bytes(self.__name), 1024 * 512, status)
  File "/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/contextlib.py", line 88, in __exit__
    next(self.gen)
  File "/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/errors_impl.py", line 466, in raise_exception_on_not_ok_status
    pywrap_tensorflow.TF_GetCode(status))
tensorflow.python.framework.errors_impl.NotFoundError: runs/1512222837/checkpoints/vocab

real	0m2.462s
user	0m2.623s
sys	0m1.066s
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$
```

အဲဒါနဲ့ help ခေါ်ကြည့်...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ python ./eval.py -h
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
usage: eval.py [-h] [--batch_size BATCH_SIZE]
               [--checkpoint_dir CHECKPOINT_DIR]
               [--eval_filepath EVAL_FILEPATH]
               [--vocab_filepath VOCAB_FILEPATH] [--model MODEL]
               [--allow_soft_placement [ALLOW_SOFT_PLACEMENT]]
               [--noallow_soft_placement]
               [--log_device_placement [LOG_DEVICE_PLACEMENT]]
               [--nolog_device_placement]

optional arguments:
  -h, --help            show this help message and exit
  --batch_size BATCH_SIZE
                        Batch Size (default: 64)
  --checkpoint_dir CHECKPOINT_DIR
                        Checkpoint directory from training run
  --eval_filepath EVAL_FILEPATH
                        Evaluate on this data (Default: None)
  --vocab_filepath VOCAB_FILEPATH
                        Load training time vocabulary (Default: None)
  --model MODEL         Load trained model checkpoint (Default: None)
  --allow_soft_placement [ALLOW_SOFT_PLACEMENT]
                        Allow device soft device placement
  --noallow_soft_placement
  --log_device_placement [LOG_DEVICE_PLACEMENT]
                        Log placement of ops on devices
  --nolog_device_placement
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$
```

