# Deep Siamese Text Similarity Experiment Log

Siamese Network ကို စိတ်ဝင်စားတယ်။  
ဒါပေမဲ့ develop လုပ်ခဲ့တာတွေက Python2.7 တို့ လွန်ခဲ့တဲ့ ၃နှစ် ၄နှစ် ပတ်ဝန်းကျင်က source code တွေဖြစ်တာ များတော့ ကျောင်းသားတွေအနေနဲ့က ကိုယ်စက်ထဲမှာ download လုပ်ပြီး run ကြတဲ့အခါမှာ သိပ်အလွယ်ကြီး မဟုတ်ဘူး။ ကိုယ်တိုင်လည်း အတွေ့အကြုံက ရှိပေမဲ့ အတိုင်းအတာ တစ်ခုအထိ အချိန်ပေးရတာ များပါတယ်။  

ဒီတစ်ခါတော့ Deep Siamese ဆိုတာကို မြင့်မြင့်ဌေး (Ph.D. candidate, UTYCC) က ပြင်ဆင်ပေးထားတဲ့ မြန်မာစာ paraphrase ဒေတာတွေနဲ့ ကိုယ့်စက်ထဲမှာ run ဖို့ ပြင်ခဲ့စဉ်က log တစ်ခုလုံးကို လေ့လာနိုင်အောင်လို့ တင်ပေးထားလိုက်တာပါ။ တင်ထားတာက debug လုပ်လိုက် run ကြည့်လိုက်လုပ်ထားတဲ့ တကယ့် running/debugging log မို့လို့... ဒီ log ကို ဖတ်ကြည့်ပြီး လုပ်တဲ့သူတွေက မလိုအပ်တဲ့ အဆင့်တွေကို ကျော်ပြီးလုပ်သွားပါ။ ကြိုတော့ ပြောထားပါမယ် စက်တစ်လုံးနဲ့ တစ်လုံး ပေးတဲ့ error တွေက တသွေမသိမ်း တူချင်မှ တူပါလိမ့်မယ်။ reference တော့ ဖြစ်ပါလိမ့်မယ်။   

source code link: https://github.com/dhwajraj/deep-siamese-text-similarity

Enjoy! Debugging & Hacking Deep Siamese Model... :)  

y@Lab  
14-21 Sept 2021  


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

ပြောရရင်တော့ evaluation ကို ဘယ်လို လုပ်ရတယ် ဆိုတာကိုလည်း တိတိကျကျ run ပြမထားဘူး...  
ကိုယ့်ဖာသာကိုယ် hack လုပ်ရင် နောက်ဆုံး evaluation လုပ်လို့ ရသွားတယ်။  
ပေးခဲ့တဲ့ command က အောက်ပါအတိုင်း...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ python ./eval.py --model ./runs/1631593567/checkpoints/model-13000 --vocab_filepath ./runs/1631593567/checkpoints/vocab 
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
MODEL=./runs/1631593567/checkpoints/model-13000
VOCAB_FILEPATH=./runs/1631593567/checkpoints/vocab

Loading testing/labelled data from validation.txt0
79

Evaluating...

./runs/1631593567/checkpoints/model-13000
2021-09-14 14:34:33.573920: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.1 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 14:34:33.573939: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.2 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 14:34:33.573943: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 14:34:33.573946: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX2 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 14:34:33.573949: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use FMA instructions, but these are available on your machine and could speed up CPU computations.
WARNING:tensorflow:From /home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/util/tf_should_use.py:170: initialize_all_variables (from tensorflow.python.ops.variables) is deprecated and will be removed after 2017-03-02.
Instructions for updating:
Use `tf.global_variables_initializer` instead.
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/numpy/core/_asarray.py:83: VisibleDeprecationWarning: Creating an ndarray from ragged nested sequences (which is a list-or-tuple of lists-or-tuples-or ndarrays with different lengths or shapes) is deprecated. If you meant to do this, you must specify 'dtype=object' when creating the ndarray
  return array(a, dtype, copy=False, order=order)
[[array([26,  7,  1, 20, 12,  3,  0,  0,  0,  0,  0,  0,  0,  0,  0])
  array([ 8, 14,  5, 26,  2, 13,  4, 16, 26,  7,  1, 20, 12,  3, 16]) 1]
 [array([30, 14, 12, 13,  4, 16, 26, 14,  8, 17, 14,  3,  4, 16,  3])
  array([30, 14, 12, 13,  4, 16, 26, 14,  8, 17, 14,  3,  4,  0,  0]) 1]
 [array([19,  5,  7, 20, 21,  4, 30, 17,  2,  5, 16, 31, 14, 15, 16])
  array([31, 14, 15, 16, 31, 14,  5,  2, 15, 27,  2,  5, 10,  0,  0]) 1]
 ...
 [array([17,  2, 15,  5, 32, 16,  5,  4, 18, 27, 32, 16, 27,  2, 15])
  array([10,  2,  5, 14,  5,  3, 16, 13, 14, 16, 30, 12,  8,  2, 13]) 0]
 [array([19,  2, 15, 21, 16, 17, 12, 10, 17,  2, 20,  0,  0,  0,  0])
  array([14, 27,  3, 12, 13, 16, 14, 17, 14,  3,  0,  0,  0,  0,  0]) 0]
 [array([20,  7,  5, 16,  5,  7,  8, 17, 14,  5,  3, 16, 10, 13, 32])
  array([31, 14, 15, 16,  8, 14, 26, 30,  2, 15,  0,  0,  0,  0,  0]) 0]]
(3960, 3)
[0.48051894 0.11134904 0.15258537 0.7697163  0.0696125  0.87505776
 0.34775648 0.84484607 0.84156024 0.25541663 0.45018306 0.9276639
 0.8588505  0.10373925 0.25809535 0.829069   0.9014754  0.3874177
 0.931582   0.8640543  0.53605944 0.8160944  0.90925324 0.98244625
 0.86023    0.8273528  0.6396485  0.8740547  0.8570869  0.9634491
 0.4846367  0.8188962  0.80158556 0.42632192 0.29289934 0.46139133
 0.59343356 0.3886755  0.25678825 0.25288665 0.18385643 0.6398447
 0.14113942 0.79824036 0.27164763 0.63877755 0.7744924  0.13190815
 0.8305942  0.9375213  0.55820745 0.09367575 0.84264743 0.7852408
 0.93713546 0.84100986 0.6631142  0.8599447  0.78172016 0.7812325
 0.8978783  0.6283619  0.9054264  0.92028683 0.21720225 0.9316196
 0.14823997 0.85767025 0.93312055 0.16351505 0.78072757 0.82527053
 0.7020502  0.5713685  0.2301845  0.65169305 0.5405332  0.7864149
 0.7405968  0.8773768  0.6099557  0.95185816 0.9294704  0.3592625
 0.4895674  0.35303137 0.14132403 0.44698346 0.64555603 0.83869654
 0.8340916  0.2255398  0.21403314 0.8650171  0.62657565 0.7684638
 0.43415007 0.78368187 0.89564157 0.7489605  0.83786595 0.468486
 0.90813476 0.66140026 0.7990641  0.8605188  0.7656862  0.97035235
 0.13441287 0.17562373 0.82581407 0.16445178 0.6182474  0.87445325
 0.13715796 0.23939237 0.8922461  0.8675207  0.846599   0.5280631
 0.8464384  0.5945585  0.1486523  0.09214944 0.79281336 0.83066046
 0.2560978  0.9583661 ]
DEV acc 0.8828125
[0.9755     0.19461726 0.835866   0.7594421  0.39340064 0.7631643
 0.7573837  0.77263474 0.35451734 0.9303884  0.09532365 0.7262197
 0.9200206  0.7052126  0.8722166  0.8114673  0.89015865 0.66902566
 0.24330233 0.6901295  0.18609518 0.3236155  0.83077455 0.893309
 0.7651193  0.81558937 0.8003434  0.86193377 0.7299626  0.5487027
 0.8483336  0.73139733 0.7621548  0.84510374 0.47026336 0.12956257
 0.551719   0.170433   0.8669925  0.29510263 0.6779065  0.94104064
 0.29814607 0.7479773  0.60581124 0.20047289 0.9024934  0.7376424
 0.5419169  0.3573726  0.1945846  0.6134591  0.3494092  0.8688659
 0.7913153  0.21187618 0.95152646 0.8353385  0.8166604  0.7286643
 0.4252748  0.28371325 0.3178186  0.9424079  0.17993969 0.4842985
 0.85404986 0.17751585 0.8304757  0.7534187  0.9765113  0.7950901
 0.7388128  0.853298   0.13332441 0.6460604  0.91460294 0.15531307
 0.83708763 0.41470402 0.95186967 0.9156639  0.9138113  0.24061309
 0.8869199  0.9052033  0.68316144 0.9431843  0.94497824 0.88665134
 0.6311262  0.7483303  0.7283564  0.8386759  0.7026322  0.12282453
 0.83167577 0.29675242 0.8670999  0.82671225 0.87358826 0.8342904
 0.24250157 0.9327047  0.82464963 0.8519388  0.66966647 0.498218
 0.8494306  0.93589324 0.68974173 0.68862534 0.17979579 0.84488505
 0.9666872  0.8227533  0.83127224 0.14260317 0.5165744  0.8055586
 0.4616744  0.56815547 0.6833526  0.759102   0.9476213  0.27432793
 0.14658232 0.6932883 ]
DEV acc 0.859375
...
...
...
...
...
0.7531898021697998
0.7812643051147461
0.9171555042266846
0.8714993000030518
0.8629871010780334
0.8651865720748901
0.14436538517475128
0.8010897040367126
0.3041492700576782
0.8359568119049072
0.8607620596885681
0.953765332698822
0.6105573773384094
0.41982027888298035
0.22305311262607574
0.95859295129776
0.7022679448127747
0.8070364594459534
0.8831055760383606
0.7331452965736389
0.8412736058235168
0.591589093208313
0.8378694653511047
0.28716591000556946
0.8234173655509949
0.926723837852478
0.6341679692268372
0.9080979228019714
0.8508889675140381
0.9194278120994568
Accuracy: 0.865909
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ 
```

## Check Original Taining Data Format

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ head person_match.train2 
Taras Fedorovych	Fedorowicz	y
Alan Rodger, Baron Rodger of Earlsferry	Rodger	y
Juliana Carneiro da Cunha	Carneiro	y
Tommy de la Cruz	De la Cruz	y
Alexander Walker Scott	Alexander Walker	y
Robert Conroy	1862	y
Guillermo Iberio Ortiz Mayagoitia	Guillermo Ortiz	y
Les AuCoin	Aucoin	y
Charles Robinson, Jr.	Charles Robinson	y
Bill Baggs	Bagg	y
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ tail ./person_match.train2 
Mohammed Fazle Baki	Md. Fazle Baki	y
Shensheng Zhang	Shen-sheng Zhang	y
James B. D. Joshi	James Joshi	y
Thomas A. Down	Thomas Down	y
Frank Hung-Fat Leung	Frank H. Leung	y
Geoffrey W. Hill	G. W. Hill	y
Simon L. Harding	Simon Harding	y
Antonio Fernández	Antonio Fernández Anta	y
Argyrios Zymnis	Argyris Zymnis	y
N. R. Achuthan	Nirmala Achuthan	y
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ head ./validation.txt0 
1	mifsud	carmelo mifsud bonnici
1	paulo machado de carvalho filho	paulo machado
1	kristopher van varenberg	van varenberg
0	philip iv of france	van der hoeven
1	charles gordon-lennox	charles gordon-lennox, 5th duke of richmond
0	charles manners-sutton, 1st viscount canterbury	guy haworth
0	alda bandeira	s. p. balasubrahmanyam
0	t. patrick martin	jetsun
0	sir robert munro, 6th baronet	reesor
1	kate ter horst	ter horst
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ tail ./validation.txt0 
0	f. jay taylor	meinoud rost van tonningen
0	thomas w. sneddon, jr.	cagdas e. gerede
0	diego hidalgo schnur	tatanka
1	den uyl	jan den uyl
0	emilio pasquale mancini	renee elio
0	hanns	f. g. l. chester
1	henry howard, 13th duke of norfolk	henry fitzalan-howard
0	henry roxby benson	gerard la pucelle
0	kent hughes	abdul ahad
0	sir richard glyn, 9th baronet	van campen
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$
```

## Check Our Data

```
(paraphrase1) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara/data3$ head train.csv
id,senid1,senid2,sentence1,sentence2,is_duplicate
0,1,2,ကျွန်တော် စီး ဖို့ ချစ်စရာ ဖိနပ် တစ် ရံ ကို ရှာ မတွေ့လို့ပါ ။,တစ်ခါတစ်ခါ ကျွန်တော်က ခင်ဗျား ကို အရမ်း အပြောင်းအလဲများတဲ့လူ လို့ ထင်မိတယ် ။,0
1,3,4,​ ကျေးဇူး ပဲ ၊ ကျွန်တော် ဘယ်လောက် ပေး ရ မလဲ ။,ကျေးဇူး နော် ၊ ဘယ်တော့ ပြန် တွေ့ ကြ မလဲ ။,0
2,5,6,​ ကျေးဇူး အများကြီး တင် ပါ တယ် ။,ကျေးဇူးတင် တယ် လို့ မ ပြော သွား ဘူး ။,0
3,7,8,​ ကျောင်းအုပ်ကြီး က တော် တဲ့ ကျောင်းသား တွေ ကို ချီးကျူး ကြ တယ် ။,ကျောင်းအုပ်ကြီး က ဆိုး တဲ့ ကျောင်းသား တွေ ကို ဒဏ်ပေး ကြ တယ် ။,0
4,9,10,​ ကောင်း ပြီ ကျွန်တော် လုပ် ပါ့ မယ် ။,ကောင်း ပြီ ကျွန်တော် ဒီ အလုပ် ကို လက်မခံ တော့ ဘူး ။,0
5,11,12,​ ကောင်း သော ည ပါ ။,ကောင်း သော နေ့ ပါ ။,0
6,13,14, ကောင်လေး က လူကြီး ကို ရှင်းရှင်းလင်းလင်း မြင် နေ တယ် ။,သာယာတဲ့ နေ့ကလေး ပါပဲ ။,0
7,15,16, ခဏအကြာမှာ ကျွန်တော် ခင်ဗျား ကို  ပြန်ဆက် ပါရစေ ။,ခဏ ကြာတော့ သူမ တည်ငြိမ် စပြုလာ ပြီး သူ ပြောတာကို နားထောင် နေတော့တယ် ။,0
8,17,18, ခေါင်မိုး ပေါ်မှာ ကြောင် တစ်ကောင် ရှိ တယ် ။,အတန်း လွတ်သွားမှာ စိုးတယ် ။,0
(paraphrase1) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara/data3$ head test.csv 
id,senid1,senid2,sentence1,sentence2,is_duplicate
0,1,2,ကောင်း လိုက် တဲ့ သတင်း လေး ပါ,ကောင်း သော သတင်း ပါ ပဲ,1
1,3,4,ခု ဒီ တံဆိပ် က ဈေးလိုက် နေ တယ် ။,ဒီ တံဆိပ် က ဈေး အရမ်း တက် နေ တယ် ။,0
2,5,6,ကျွန်မ ဘက် က စ ပြီး ကျေအေး ပေး တယ် နော်,ကျွန်မ ဘက် က စ ပြီး ကျေလည် တာ နော်,1
3,7,8,တကယ် ကို လေးစား သွား ပြီ,ငါ သူ့ ကို သဘောမကျ ဘူး,0
4,9,10,ဂုဏ်ယူ တယ် မြန်မာ အတွက်,ဂုဏ်ယူ ပါ တယ် မြန်မာ,1
5,11,12,မင်း ဘယ် ကို ရောက် နေ တာ လဲ ။,မင်း ဘာတွေ ကို လုပ် နေ တာ လဲ ။,0
6,13,14,ဆရာတော် ကြီး များ သက်တော် ရာ ကျော် ရှည် ပါစေ,ဆရာတော် အသက် ရာ ကျော် ရှည် ပါစေ ဘေးရန်ကင်း ပါစေ,1
7,15,16,ရှိခိုး လျက် ပါ,ရှိခိုး ကန်တော့ ဦးခိုက် ပါ ၏,1
8,17,18,အောင်မြင် ပါစေ အမြဲ အားပေး လျက်,အားပေး လိုက် လို့ အောင်မြင် တာ လား,0
(paraphrase1) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara/data3$
```

## Data Preparation

မြန်မာစာ ဒေတာနဲ့ (သို့) လက်ရှိ ငါတို့ ပြင်ထားတဲ့ format နဲ့က run လို့ မရဘူး။ အဲဒါကြောင့် Deep Siamese ပရိုဂရမ်က သုံးထားတဲ့ format ကို အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့...   

```
(paraphrase1) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara/data3$ cp {train,test,open-test}.csv /home/ye/exp/myPara2/deep-siamese-text-similarity/my-para/
(paraphrase1) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara/data3$ 
```

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ cut -f 4-6 -d"," ./test.csv > test.4-6
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ cut -f 4-6 -d"," ./train.csv > train.4-6
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ cut -f 4-6 -d"," ./open-test.csv > open-test.4-6
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ wc *.4-6
   1001   10731  138637 open-test.4-6
   1001   14907  202268 test.4-6
  40462  591508 8350847 train.4-6
  42464  617146 8691752 total
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ wc *.csv
   1001   10731  151440 open-test.csv
   1001   14907  215068 test.csv
  40462  591517 9056946 train.csv
  42464  617155 9423454 total
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$
```

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ sed 's/\,/\t/g' ./test.4-6 > ./test.4-6.tab
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ sed 's/\,/\t/g' ./train.4-6 > ./train.4-6.tab
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ sed 's/\,/\t/g' ./open-test.4-6 > ./open-test.4-6.tab
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ head -n 3 *.tab
==> open-test.4-6.tab <==
sentence1	sentence2	is_duplicate
၁၁ ဒေါ်လာ ကျ ပါ တယ် ။	၁၁ နာရီ လာ ခေါ် မယ် ။	0
၁၁ နာရီ ခွဲ အိမ် ပြန် မယ် ။	၁၁ နာရီ ခွဲ အရောက် လာ ပါ ။	0

==> test.4-6.tab <==
sentence1	sentence2	is_duplicate
ကောင်း လိုက် တဲ့ သတင်း လေး ပါ	ကောင်း သော သတင်း ပါ ပဲ	1
ခု ဒီ တံဆိပ် က ဈေးလိုက် နေ တယ် ။	ဒီ တံဆိပ် က ဈေး အရမ်း တက် နေ တယ် ။	0

==> train.4-6.tab <==
sentence1	sentence2	is_duplicate
ကျွန်တော် စီး ဖို့ ချစ်စရာ ဖိနပ် တစ် ရံ ကို ရှာ မတွေ့လို့ပါ ။	တစ်ခါတစ်ခါ ကျွန်တော်က ခင်ဗျား ကို အရမ်း အပြောင်းအလဲများတဲ့လူ လို့ ထင်မိတယ် ။	0
 ကျေးဇူး ပဲ ၊ ကျွန်တော် ဘယ်လောက် ပေး ရ မလဲ ။	ကျေးဇူး နော် ၊ ဘယ်တော့ ပြန် တွေ့ ကြ မလဲ ။	0
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$
```

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ cut -f 3 ./test.4-6.tab > test.4-6.tab.col3
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ head test.4-6.tab.col3 
is_duplicate
1
0
1
0
1
0
1
1
0
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$
```

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ cut -f 3 ./train.4-6.tab > train.4-6.tab.col3
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ cut -f 3 ./open-test.4-6.tab > open-test.4-6.tab.col3
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ wc *.col3
 1001  1000  2012 open-test.4-6.tab.col3
 1001  1001  2013 test.4-6.tab.col3
40462 40462 80935 train.4-6.tab.col3
42464 42463 84960 total
```

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ sed -i 'y/10/yn/' ./test.4-6.tab.col3
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ head ./test.4-6.tab.col3 
is_duplicate
y
n
y
n
y
n
y
y
n
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$
```

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ sed -i 'y/10/yn/' ./train.4-6.tab.col3 
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ sed -i 'y/10/yn/' ./open-test.4-6.tab.col3 
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ wc *.col3
 1001  1000  2012 open-test.4-6.tab.col3
 1001  1001  2013 test.4-6.tab.col3
40462 40462 80935 train.4-6.tab.col3
42464 42463 84960 total
```

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ cut -f1,2 train.4-6.tab > ./train.col12
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ head ./train.col12 
sentence1	sentence2
ကျွန်တော် စီး ဖို့ ချစ်စရာ ဖိနပ် တစ် ရံ ကို ရှာ မတွေ့လို့ပါ ။	တစ်ခါတစ်ခါ ကျွန်တော်က ခင်ဗျား ကို အရမ်း အပြောင်းအလဲများတဲ့လူ လို့ ထင်မိတယ် ။
 ကျေးဇူး ပဲ ၊ ကျွန်တော် ဘယ်လောက် ပေး ရ မလဲ ။	ကျေးဇူး နော် ၊ ဘယ်တော့ ပြန် တွေ့ ကြ မလဲ ။
 ကျေးဇူး အများကြီး တင် ပါ တယ် ။	ကျေးဇူးတင် တယ် လို့ မ ပြော သွား ဘူး ။
 ကျောင်းအုပ်ကြီး က တော် တဲ့ ကျောင်းသား တွေ ကို ချီးကျူး ကြ တယ် ။	ကျောင်းအုပ်ကြီး က ဆိုး တဲ့ ကျောင်းသား တွေ ကို ဒဏ်ပေး ကြ တယ် ။
 ကောင်း ပြီ ကျွန်တော် လုပ် ပါ့ မယ် ။	ကောင်း ပြီ ကျွန်တော် ဒီ အလုပ် ကို လက်မခံ တော့ ဘူး ။
 ကောင်း သော ည ပါ ။	ကောင်း သော နေ့ ပါ ။
 ကောင်လေး က လူကြီး ကို ရှင်းရှင်းလင်းလင်း မြင် နေ တယ် ။	သာယာတဲ့ နေ့ကလေး ပါပဲ ။
 ခဏအကြာမှာ ကျွန်တော် ခင်ဗျား ကို  ပြန်ဆက် ပါရစေ ။	ခဏ ကြာတော့ သူမ တည်ငြိမ် စပြုလာ ပြီး သူ ပြောတာကို နားထောင် နေတော့တယ် ။
 ခေါင်မိုး ပေါ်မှာ ကြောင် တစ်ကောင် ရှိ တယ် ။	အတန်း လွတ်သွားမှာ စိုးတယ် ။
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$
```

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ cut -f1,2 test.4-6.tab > ./test.col12
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ cut -f1,2 open-test.4-6.tab > ./open-test.col12
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ wc *.col12
   1001   11677  136625 open-test.col12
   1001   15907  200255 test.col12
  40462  631911 8269912 train.col12
  42464  659495 8606792 total
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$
```

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ wc *.col3
 1001  1000  2012 open-test.4-6.tab.col3
 1001  1001  2013 test.4-6.tab.col3
40462 40462 80935 train.4-6.tab.col3
42464 42463 84960 total
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$
```

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ paste ./test.col12 ./test.4-6.tab.col3 > valid
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ paste ./train.col12 ./train.4-6.tab.col3 > train
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ paste ./open-test.col12 ./open-test.4-6.tab.col3 > open-test
```

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ wc {train,valid,open-test}
  40462  672373 8350847 train
   1001   16908  202268 valid
   1001   12677  138637 open-test
  42464  701958 8691752 total
```

check the content:  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ head ./train
sentence1	sentence2	is_duplicate
ကျွန်တော် စီး ဖို့ ချစ်စရာ ဖိနပ် တစ် ရံ ကို ရှာ မတွေ့လို့ပါ ။	တစ်ခါတစ်ခါ ကျွန်တော်က ခင်ဗျား ကို အရမ်း အပြောင်းအလဲများတဲ့လူ လို့ ထင်မိတယ် ။	n
 ကျေးဇူး ပဲ ၊ ကျွန်တော် ဘယ်လောက် ပေး ရ မလဲ ။	ကျေးဇူး နော် ၊ ဘယ်တော့ ပြန် တွေ့ ကြ မလဲ ။	n
 ကျေးဇူး အများကြီး တင် ပါ တယ် ။	ကျေးဇူးတင် တယ် လို့ မ ပြော သွား ဘူး ။	n
 ကျောင်းအုပ်ကြီး က တော် တဲ့ ကျောင်းသား တွေ ကို ချီးကျူး ကြ တယ် ။	ကျောင်းအုပ်ကြီး က ဆိုး တဲ့ ကျောင်းသား တွေ ကို ဒဏ်ပေး ကြ တယ် ။	n
 ကောင်း ပြီ ကျွန်တော် လုပ် ပါ့ မယ် ။	ကောင်း ပြီ ကျွန်တော် ဒီ အလုပ် ကို လက်မခံ တော့ ဘူး ။	n
 ကောင်း သော ည ပါ ။	ကောင်း သော နေ့ ပါ ။	n
 ကောင်လေး က လူကြီး ကို ရှင်းရှင်းလင်းလင်း မြင် နေ တယ် ။	သာယာတဲ့ နေ့ကလေး ပါပဲ ။	n
 ခဏအကြာမှာ ကျွန်တော် ခင်ဗျား ကို  ပြန်ဆက် ပါရစေ ။	ခဏ ကြာတော့ သူမ တည်ငြိမ် စပြုလာ ပြီး သူ ပြောတာကို နားထောင် နေတော့တယ် ။	n
 ခေါင်မိုး ပေါ်မှာ ကြောင် တစ်ကောင် ရှိ တယ် ။	အတန်း လွတ်သွားမှာ စိုးတယ် ။	n
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ head ./valid
sentence1	sentence2	is_duplicate
ကောင်း လိုက် တဲ့ သတင်း လေး ပါ	ကောင်း သော သတင်း ပါ ပဲ	y
ခု ဒီ တံဆိပ် က ဈေးလိုက် နေ တယ် ။	ဒီ တံဆိပ် က ဈေး အရမ်း တက် နေ တယ် ။	n
ကျွန်မ ဘက် က စ ပြီး ကျေအေး ပေး တယ် နော်	ကျွန်မ ဘက် က စ ပြီး ကျေလည် တာ နော်	y
တကယ် ကို လေးစား သွား ပြီ	ငါ သူ့ ကို သဘောမကျ ဘူး	n
ဂုဏ်ယူ တယ် မြန်မာ အတွက်	ဂုဏ်ယူ ပါ တယ် မြန်မာ	y
မင်း ဘယ် ကို ရောက် နေ တာ လဲ ။	မင်း ဘာတွေ ကို လုပ် နေ တာ လဲ ။	n
ဆရာတော် ကြီး များ သက်တော် ရာ ကျော် ရှည် ပါစေ	ဆရာတော် အသက် ရာ ကျော် ရှည် ပါစေ ဘေးရန်ကင်း ပါစေ	y
ရှိခိုး လျက် ပါ	ရှိခိုး ကန်တော့ ဦးခိုက် ပါ ၏	y
အောင်မြင် ပါစေ အမြဲ အားပေး လျက်	အားပေး လိုက် လို့ အောင်မြင် တာ လား	n
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ head ./open-test
sentence1	sentence2	is_duplicate
၁၁ ဒေါ်လာ ကျ ပါ တယ် ။	၁၁ နာရီ လာ ခေါ် မယ် ။	n
၁၁ နာရီ ခွဲ အိမ် ပြန် မယ် ။	၁၁ နာရီ ခွဲ အရောက် လာ ပါ ။	n
၁၁:၃၀ ပြန်ရောက် မယ် လို့ ထင် သလား ။	၁၁:၃၀ အတိ မှာ ပြန်ရောက် လာ ခဲ့ တယ် ။	n
၂ မိုင် ထက် ပို ရှည် တယ် ။	၂ မိုင် လောက် သွား ရ တယ် ။	n
၄ ရက် အတွင်း အိမ် ပြန် မယ် ။	၄ ရက် လောက် နေ ရင် ပြန် လာ ပါ ။	n
၅ ဒေါ်လာ ထက် ပို ပါ တယ် ။	၅ ဒေါ်လာ လောက် ကျ သင့် တယ် ။	n
၅ ဒေါ်လာ ထက် နဲ ပါ တယ် ။	၅ ဒေါ်လာ ဆို နဲ ပါ တယ် ။	n
၅ ဒေါ်လာ ပဲ ရှိ တယ် ။	၅ ဒေါ်လာ လောက် ရှိ လား ။	n
၅ လမ်းက စားသောက်ဆိုင် မှာ စား ချင် တယ် ။	၅ လမ်း မှာ စားသောက်ဆိုင် ရှိ လား ။	n
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$
```

အထက်ပါ format က တခြား training process တွေ အတွက်လည်း သုံးလိုရလို ဒီအတိုင်းပဲ သိမ်းထားချင်တယ်။  

Deep Siamese နဲ့ run ဖို့ က column header ကိုဖြုတ်ရမယ်။ ပြီးတော့ validation နဲ့ open-test အတွက်က label ကို 1st column မှာ ထားပေးရမယ်။  0,1 နဲ့ ပြောင်းပေးရမယ်။  
အဲဒါတွေအတွက် အောက်ပါအတိုင်း လုပ်ခဲ့...  

Folder အသစ်ဆောက်ပြီး အဲဒီထဲမှာ လုပ်မယ်။  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ mkdir data
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ mv train ./data/
```

အရင်ဆုံး train ဖိုင်ထဲက ထိပ်ဆုံး column header ကို gedit နဲ့ ဝင်ဖြုတ်ခဲ့ပြီးတော့ awk နဲ့ column 3 က y ဖြစ်နေတာတွေပဲ ဆွဲထုတ်ခဲ့... 

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/data$ awk -F "[\t]" '$3 == "y" {print;}' ./train | head
 ပျော် စရာ ကြီး ပါ	ပျော် စရာ ပဲ နော်	y
 ပျော် စရာ ကြီး ပါ	ပျော် စရာ လို့ ပဲ မြင် တယ်	y
 ပျော် စရာ ကြီး ပါ	ပျော်ရွှင် စရာ ပါ	y
 ပျော် စရာ ကြီး ပါ	ပျော် စရာ လေး ပေါ့	y
 ပျော် စရာ ကြီး ပါ	ပျော် စရာ ပဲ	y
 ပျော် စရာ ကြီး ပါ	ပျော် တယ် ကြည်နူး တယ်	y
၎င်း ဓူဝံ ကြယ် သည် ကမ္ဘာ ၏ မြောက် ဝင်ရိုးစွန်း တွင် တည်ရှိ ပြီး မြောက် အရပ် ကို အမြဲ ညွှန်ပြ ပေး သည် ။	၎င်း ဓူဝံ ကြယ် သည် ကမ္ဘာ ၏ မြောက် ဝင်ရိုးစွန်း တွင် တည်ရှိ ပြီး မြောက် အရပ် ကို အမြဲ ညွှန် ပေး သည် ။	y
၅၀၀ ကီလိုမီတာ မိုင် ၉၀၀၀ ရှည်မျော သည် ။	ကမ်းရိုးတန်း အလျား ၁၄	y
Apple ကုန်တံဆိပ် ဖုန်း များ သည် အရည်အသွေး ကောင်းမွန် ကြ သည် ။	Apple ကုန်အမှတ်တံဆိပ် ဖုန်း များ သည် အရည်အသွေး ကောင်းမွန် ကြ သည် ။	y
Delivery ပို့ရန် ကောင်လေး လိုအပ် ပါ တယ် ။	Delivery ပို့ ရန် ကောင်းကလေး လိုအပ် ပါ တယ် ။	y
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/data$
```

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/data$ awk -F "[\t]" '$3 == "y" {print;}' ./train > train.final
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/data$ wc train.final 
  15640  233644 2893579 train.final
```

for Validation and Open-test data:  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ cut -d "," -f 6 ./test.csv > ./data/test.col6
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ cut -d "," -f 6 ./open-test.csv > ./data/open-test.col6
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$
```

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ paste ./data/test.col6 ./test.col12 > ./data/test.col123
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para$ paste ./data/open-test.col6 ./open-test.col12 > ./data/open-test.col123
```

gedit နဲ့ ထိပ်ဆုံးလိုင်းကို ဝင်ဖျက်ရင် ဒေတာပြင်ပြီးသွားပြီ။  
backup ကူးပြီး final naming လုပ်။  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/data$ ls
open-test.col123  test.col123  train.final
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/data$ mkdir bk
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/data$ cp * ./bk
cp: -r not specified; omitting directory 'bk'
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/data$ ls
bk  open-test.col123  test.col123  train.final
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/data$ mv test.col123 valid.final
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/data$ mv open-test.col123 open-test.final
```

filename တွေကို ဘယ်လို ပေးရမလဲ ဆိုတာကို coding ကို ဝင်ကြည့်မှ အဆင်ပြေတယ်။  
training data အတွက်က program argument အနေနဲ့ ပေးလို့ ရပေမဲ့ validation အတွက်က coding ထဲမှာ filename ကို အောက်ပါအတိုင်း အသေပေးထားတာတွေ့ရ...  

```python
        with open('validation.txt'+str(i),'w') as f:
            for text1,text2,label in zip(x1_dev,x2_dev,y_dev):
                f.write(str(label)+"\t"+text1+"\t"+text2+"\n")
            f.close()
        del x1_dev
        del y_dev
        
```

validation.txt0, validation.txt1 ဆိုပြီး ဖိုင်နာမည်ကို ပေးသွားလို့ ရတယ်လို့ နားလည်တယ်။  

original training ဒေတာနဲ့ validation ဒေတာတွေကို နေရာရွှေ့ခဲ့...  
နောက်ဆုံး သုံးမယ့် file တွေက အောက်ပါအတိုင်း   

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ head train.txt
 ပျော် စရာ ကြီး ပါ	ပျော် စရာ ပဲ နော်	y
 ပျော် စရာ ကြီး ပါ	ပျော် စရာ လို့ ပဲ မြင် တယ်	y
 ပျော် စရာ ကြီး ပါ	ပျော်ရွှင် စရာ ပါ	y
 ပျော် စရာ ကြီး ပါ	ပျော် စရာ လေး ပေါ့	y
 ပျော် စရာ ကြီး ပါ	ပျော် စရာ ပဲ	y
 ပျော် စရာ ကြီး ပါ	ပျော် တယ် ကြည်နူး တယ်	y
၎င်း ဓူဝံ ကြယ် သည် ကမ္ဘာ ၏ မြောက် ဝင်ရိုးစွန်း တွင် တည်ရှိ ပြီး မြောက် အရပ် ကို အမြဲ ညွှန်ပြ ပေး သည် ။	၎င်း ဓူဝံ ကြယ် သည် ကမ္ဘာ ၏ မြောက် ဝင်ရိုးစွန်း တွင် တည်ရှိ ပြီး မြောက် အရပ် ကို အမြဲ ညွှန် ပေး သည် ။	y
၅၀၀ ကီလိုမီတာ မိုင် ၉၀၀၀ ရှည်မျော သည် ။	ကမ်းရိုးတန်း အလျား ၁၄	y
Apple ကုန်တံဆိပ် ဖုန်း များ သည် အရည်အသွေး ကောင်းမွန် ကြ သည် ။	Apple ကုန်အမှတ်တံဆိပ် ဖုန်း များ သည် အရည်အသွေး ကောင်းမွန် ကြ သည် ။	y
Delivery ပို့ရန် ကောင်လေး လိုအပ် ပါ တယ် ။	Delivery ပို့ ရန် ကောင်းကလေး လိုအပ် ပါ တယ် ။	y
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ head validation.txt0
0	တော် ပါ တယ် လေးစား တယ်	နှမြော စရာ ကြီး ကွယ်
1	ဒိုင် က ညစ် တာ	ဒိုင် ညစ် တယ်
0	ကူညီ ပေး စေ ချင် ပါ တယ်	ကြည့် ချင် လိုက် တာ ဘယ် က လွှင့် မလဲ
0	တရားမျှတ မှု ရှိ နိုင် ကြ ပါစေ	ကျွန်မ စကား ကြောင့် မူယာ တစ် ချက် မျက်နှာ မ ကောင်း ဖြစ် သွား ၏
0	အဖိတ်နေ့ မှာ မယ်သီလ တို့ ဆွမ်းဆန်ခံ ကြွ လိမ့် မယ် ။	ကြိုဆို နေ ပါ တယ်
0	ထည့်ပေး ထား သော ထမင်း ကို ကုန်စင်အောင် စား ပါ ။	ကောင်း နေ ရော
0	ခြင်ပေါက်ဖွား ခြင်း ကို ဘယ်လို တားဆီး မလဲ	ဒီ ကလေး အရမ်း ဆင်ခြေပေး တယ်
0	အောင်မြင် ပါစေ အမြဲ အားပေး လျက်	ဝမ်းမြောက် ဝမ်းသာ သာဓု ၃ ကြိမ် ခေါ် ပါ တယ်
0	ဂိုးသမား ကောင်း ပါ တယ်	ဆက် ကြိုးစား ပါ အားပေး မယ်
0	ကျန်းမာ ပြီး ဘေးကင်း ပါစေ	သူ စောဒကတက် နေ တယ် ။
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ head validation.txt1
0	၁၁ ဒေါ်လာ ကျ ပါ တယ် ။	၁၁ နာရီ လာ ခေါ် မယ် ။
0	၁၁ နာရီ ခွဲ အိမ် ပြန် မယ် ။	၁၁ နာရီ ခွဲ အရောက် လာ ပါ ။
0	၁၁:၃၀ ပြန်ရောက် မယ် လို့ ထင် သလား ။	၁၁:၃၀ အတိ မှာ ပြန်ရောက် လာ ခဲ့ တယ် ။
0	၂ မိုင် ထက် ပို ရှည် တယ် ။	၂ မိုင် လောက် သွား ရ တယ် ။
0	၄ ရက် အတွင်း အိမ် ပြန် မယ် ။	၄ ရက် လောက် နေ ရင် ပြန် လာ ပါ ။
0	၅ ဒေါ်လာ ထက် ပို ပါ တယ် ။	၅ ဒေါ်လာ လောက် ကျ သင့် တယ် ။
0	၅ ဒေါ်လာ ထက် နဲ ပါ တယ် ။	၅ ဒေါ်လာ ဆို နဲ ပါ တယ် ။
0	၅ ဒေါ်လာ ပဲ ရှိ တယ် ။	၅ ဒေါ်လာ လောက် ရှိ လား ။
0	၅ လမ်းက စားသောက်ဆိုင် မှာ စား ချင် တယ် ။	၅ လမ်း မှာ စားသောက်ဆိုင် ရှိ လား ။
0	ကျေးဇူးပြုပြီး မီနူးရ နိုင် မလား ။	ကျေးဇူးပြုပြီး မီနူး ထဲ က အတိုင်း ရ နိုင် မလား ။
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ 
```

file size တွေရဲ့ information က အောက်ပါအတိုင်း...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ wc train.txt 
  15640  233644 2893579 train.txt
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ wc validation.txt0
  4692  69876 869662 validation.txt0
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ wc validation.txt1
  1000  12674 138604 validation.txt1
```

## Training with Myanmar Paraphrase Data

အရင်ဆုံး epoch ကို 1 ပဲ ထားပြီး run ကြည့်ခဲ့...  
အလုပ် လုပ်မလုပ် သိချင်တာနဲ့... log ဖိုင်ကို ဝင်ကြည့်ချင်တာနဲ့...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --num_epochs 1 2>&1 | tee train-epoch1.log
```

runs ဖိုလ်ဒါက HDD size တော့ ယူလိမ့်မယ်။
လက်ရှိ runs ဖိုလ်ဒါက 140 items, totalling 11.9 GB ယူထားတယ်။  
original text နဲ့ train ထားတာလည်း ရှိလို့...   


character နဲ့ run ခဲ့ ...

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --num_epochs 50 2>&1 | tee train-char-epoch50.log
2021-09-14 17:22:27.291395: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.1 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 17:22:27.291416: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.2 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 17:22:27.291420: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 17:22:27.291422: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX2 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-14 17:22:27.291424: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use FMA instructions, but these are available on your machine and could speed up CPU computations.

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
NUM_EPOCHS=50
TRAINING_FILES=train.txt
WORD2VEC_FORMAT=text
WORD2VEC_MODEL=wiki.simple.vec

Loading training data from train.txt
Building vocabulary
Length of loaded vocabulary =98
dumping validation 0
Train/Dev split for train.txt: 42228/4692
starting graph def
started session
[<tf.Tensor 'output/unstack:0' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:1' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:2' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:3' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:4' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:5' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:6' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:7' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:8' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:9' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:10' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:11' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:12' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:13' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack:14' shape=(?, 300) dtype=float32>]
[<tf.Tensor 'output/unstack_1:0' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:1' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:2' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:3' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:4' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:5' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:6' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:7' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:8' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:9' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:10' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:11' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:12' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:13' shape=(?, 300) dtype=float32>, <tf.Tensor 'output/unstack_1:14' shape=(?, 300) dtype=float32>]
initialized siameseModel object
defined training_ops
defined gradient summaries
Writing to /home/ye/exp/myPara2/deep-siamese-text-similarity/runs/1631614951

init all variables
[[array([19,  5,  6, 10,  7,  4,  6, 13,  2,  3, 12, 27,  2, 18, 35])
  array([34, 35, 62, 12,  2, 34, 37, 33,  3,  7,  2, 10, 32, 33,  2]) 0]
 [array([37, 10,  7,  2, 28, 16,  6,  2, 62, 21,  7, 13,  2,  9, 20])
  array([10,  4,  5, 13, 59, 22, 13, 18, 17,  7,  2,  3, 14,  2, 18]) 0]
 [array([ 9, 16, 32, 60, 32, 33, 13,  2,  3, 14,  2, 31,  2, 30, 33])
  array([61, 13, 60, 32, 33, 10,  7,  2, 45, 22, 13, 28, 11,  5,  6]) 1]
 ...
 [array([28, 17,  7, 13, 10, 11, 20,  7, 51,  2,  9,  2, 18,  6,  2])
  array([28, 17,  7, 13, 10, 11, 20,  7, 51,  2,  9,  2, 18,  6,  2]) 1]
 [array([34, 32, 28,  7,  2, 56, 35,  2,  8, 12, 13,  2, 45, 32, 33])
  array([34, 32, 28,  7,  2, 56, 35,  2,  8, 12, 13,  2, 45, 32, 33]) 1]
 [array([44, 10,  7,  2, 10, 11, 32, 33, 13,  8,  6, 13,  2, 21, 32])
  array([27, 22,  2, 10,  2, 18, 10, 19,  7,  2, 37,  4, 17,  7, 28]) 0]]
(42228, 3)
TRAIN 2021-09-14T17:22:34.467969: step 1, loss 0.104869, acc 0.703125
(1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 1, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 1) [0.7228426  0.70311946 0.6689437  0.74712044 0.7588836  0.7367509
 0.7423743  0.70503914 0.7097842  0.7233885  0.7015295  0.72005475
 0.68342423 0.75234264 0.66156316 0.72910476 0.63605756 0.71473706
 0.71906424 0.6476928  0.6368718  0.74751556 0.739291   0.71910137
 0.7178705  0.73053616 0.7658531  0.7020739  0.7006539  0.75535154
 0.6397792  0.6719798  0.6946104  0.63752306 0.7432048  0.6868644
 0.673546   0.75386614 0.7485469  0.7748737  0.7433629  0.6583958
 0.6983609  0.6466102  0.70500195 0.62406594 0.629249   0.7356372
 0.7205792  0.7019439  0.75504035 0.69082147 0.7238766  0.7279587
 0.75519866 0.7009046  0.73951507 0.7181911  0.6846975  0.7252145
 0.7332474  0.69621295 0.6613988  0.69604206] [0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
TRAIN 2021-09-14T17:22:34.523919: step 2, loss 0.117165, acc 0.640625
(1, 0, 0, 1, 0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 1, 0, 1, 0, 1, 1, 0, 0, 1, 0, 1, 0, 0, 0, 1, 0, 1, 0, 0, 0, 1, 0, 1) [0.6403134  0.699832   0.7184507  0.6897673  0.6099598  0.7621312
 0.752492   0.5123035  0.58121604 0.552051   0.66513413 0.7217747
 0.7151997  0.68314177 0.7104632  0.7413689  0.6846424  0.63214844
 0.7569284  0.6269265  0.65527844 0.68405277 0.719569   0.67128974
 0.64879596 0.7018228  0.85006934 0.7008645  0.67306525 0.70108455
 0.7433712  0.70727587 0.70731866 0.7159384  0.68623745 0.6692966
 0.79595685 0.7077783  0.65152055 0.62030697 0.7397595  0.6895023
 0.68711716 0.70094234 0.68051136 0.54211134 0.6925647  0.5966107
 0.6281844  0.7278306  0.756788   0.70443463 0.69034183 0.7566798
 0.6648226  0.7280827  0.7273223  0.72308725 0.7292816  0.7299788
 0.7888011  0.6733662  0.671531   0.70622325] [0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
TRAIN 2021-09-14T17:22:34.556643: step 3, loss 0.103037, acc 0.703125
...
...
...
...
...
...
 0.8603376  0.17818424 0.07762048 0.10578492] [0. 0. 0. 0. 1. 0. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 0. 1. 0. 1. 0. 1.
 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 1. 1. 0. 0. 0. 0. 0. 1. 0. 1. 0.
 0. 0. 0. 0. 0. 1. 1. 1. 0. 0. 1. 1. 0. 1. 1. 1.]
TRAIN 2021-09-14T17:41:42.082900: step 32949, loss 0.0122488, acc 0.984375
(1, 1, 1, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 1, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 1, 1, 0, 0, 1, 0, 1, 1, 0, 0, 0, 1, 1, 0, 1, 1, 0, 0, 1, 0, 0, 1, 1, 0, 1, 0, 1, 0) [0.01759469 0.0346491  0.01773486 0.9999344  0.99939954 0.99634296
 0.985249   0.99885213 0.99210066 0.23745357 0.94950384 0.19063194
 0.9998161  0.9998979  0.06118951 0.04668707 0.99996763 0.96335
 0.04441455 0.9999776  0.12334152 0.9050146  0.99954176 0.9999964
 0.98700446 0.7966908  0.99973184 0.02240145 0.99587125 0.9999227
 0.04773209 0.7282799  0.99998575 0.05638697 0.9970182  0.04685412
 0.03273954 0.10128768 0.7594312  0.88697624 0.14179127 0.99745476
 0.0894561  0.1224346  0.99968207 0.6746357  0.99970984 0.03490018
 0.11313327 0.84791106 0.09020269 0.02863695 0.99985415 0.99994534
 0.05367226 0.984751   0.9207436  0.06163626 0.04649518 0.9820613
 0.07533711 0.99915206 0.13171151 0.9989518 ] [1. 1. 1. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0. 0. 1. 1. 0. 0. 1. 0. 1. 0. 0. 0.
 0. 0. 0. 1. 0. 0. 1. 0. 0. 1. 0. 1. 1. 1. 0. 0. 1. 0. 1. 1. 0. 0. 0. 1.
 1. 0. 1. 1. 0. 0. 1. 0. 0. 1. 1. 0. 1. 0. 1. 0.]
TRAIN 2021-09-14T17:41:42.120989: step 32950, loss 0.00925516, acc 0.984375
(0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 1, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 1, 1, 0, 1, 1, 0, 1, 0, 1, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0)/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:458: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
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
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/numpy/core/_asarray.py:83: VisibleDeprecationWarning: Creating an ndarray from ragged nested sequences (which is a list-or-tuple of lists-or-tuples-or ndarrays with different lengths or shapes) is deprecated. If you meant to do this, you must specify 'dtype=object' when creating the ndarray
  return array(a, dtype, copy=False, order=order)
 [0.99253154 0.19331038 0.9574837  0.98238796 0.05297118 0.99984115
 0.5796681  0.27019942 0.99538493 0.9976765  0.8289619  0.07189957
 0.04746499 0.15106255 0.9999968  0.10152893 0.9998525  0.11503272
 0.933221   0.89964664 0.80016875 0.99743956 0.9999647  0.99998844
 0.09476809 0.999969   0.99998236 0.99949366 0.9771544  0.99999034
 0.12532079 0.1068604  0.8388157  0.9781501  0.8506993  0.98022735
 0.03307126 0.08057828 0.9933547  0.24445897 0.08390144 0.97213584
 0.2044727  0.79894054 0.05971796 0.05905108 0.99733734 0.9165366
 0.99729794 0.98179424 0.3736628  0.21080233 0.07405753 0.10773523
 0.90384406 0.07302347 0.99441576 0.9426707  0.10396013 0.97811204
 0.11866362 0.99994695 0.97931874 0.99997073] [0. 1. 0. 0. 1. 0. 0. 1. 0. 0. 0. 1. 1. 1. 0. 1. 0. 1. 0. 0. 0. 0. 0. 0.
 1. 0. 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 1. 1. 0. 1. 1. 0. 1. 0. 1. 1. 0. 0.
 0. 0. 1. 1. 1. 1. 0. 1. 0. 0. 1. 0. 1. 0. 0. 0.]

real	19m20.078s
user	84m42.974s
sys	10m6.671s
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ 
```


for checking the log:  

```
tensorboard --logdir ./runs/1631593567/
```

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/training-with-myPara-epoch50-tensorboard-eg.png" alt="checking Acc/Loss with Tensorboard"/>  
</p>  
<div align="center">
  Fig. Checking accuracy and loss with tensorboard for character model with epoch 50
</div> 

<br />

## Testing with 100 Epoch, Character Model

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --num_epochs 100 2>&1 | tee train-char-epoch100.log
...
...
...
TRAIN 2021-09-14T18:56:20.256182: step 65899, loss 0.0099119, acc 0.984375
(1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 1, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 1, 0, 0, 1, 0) [0.16064101 0.9960499  0.06751609 0.9992422  0.9996971  0.99947983
 0.9999647  0.99997497 0.96139574 0.85451084 0.8754424  0.02957441
 0.92741996 0.99977666 0.0115665  0.8949488  0.9978316  0.99999994
 0.01608626 0.99994856 0.99989474 0.9999935  0.98232895 0.9999032
 0.98447365 0.99558955 0.92766976 0.9999844  0.97869277 0.11665272
 0.10537347 0.99999094 0.99999994 0.9977801  0.9999723  0.13152637
 0.8578336  0.02459399 0.12613334 0.92083573 0.99999934 0.09517364
 0.17424114 0.9872209  0.09404152 0.06587148 0.95393926 0.24111326
 0.9964343  0.99999994 0.99966735 0.9981149  0.91042507 0.03897988
 0.999971   0.2839204  0.04269813 0.92717016 0.99998486 0.08691422
 0.9997049  0.9984812  0.03077045 0.9348178 ] [1. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 1. 0. 1. 1. 0. 0. 1. 1. 0. 1. 1. 0. 1.
 0. 0. 0. 0. 0. 1. 0. 1. 1. 0. 0. 1. 0. 0. 1. 0.]
TRAIN 2021-09-14T18:56:20.285867: step 65900, loss 0.0189417, acc 0.96875
(1, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 1, 1, 0, 1, 0, 1, 1, 0, 1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 1, 0, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0) [0.0581731  0.03400388 0.9986798  0.07306936 0.9999965  0.99999875
 1.         0.98091894 0.9715222  0.99999917 0.99999523 0.83911306
 0.03431511 0.7464771  0.7715236  0.94724643 0.999999   0.99863523
 0.1263301  0.15799901 0.9933539  0.99990803 0.86561984 0.07145077
 0.17120437 0.04553419 0.97824675 0.16044396 0.98224133 0.9999824
 0.0950496  0.9851802  0.05744882 0.99998885 0.04026607 0.9994575
 0.9475584  0.9999773  0.98211443 0.10332731 0.9962923  0.9995471
 0.07347064 0.08722373 0.99960655 0.07217398 0.23213333 0.04031973
 0.99316967 0.99710387 0.99997187 0.9999707  0.8961683  0.9999
 0.9699691  0.03565321 0.99831307 0.99999905 0.9999798  0.9999996
 0.12812302 0.9856524  0.8827942  0.9876295 ] [1. 1. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 1. 0. 0. 0. 1.
 1. 1. 0. 1. 0. 0. 1. 0. 1. 0. 1. 0. 0. 0. 0. 1. 0. 0. 1. 1. 0. 1. 1. 1.
 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 1. 0. 0. 0.]

real	38m3.608s
user	168m52.596s
sys	20m17.571s
```

အထက်ပါ Myanmar paraphrase classification with character model, epoch 100 ရဲ့ training/validation ရလဒ်တွေက အောက်ပါအတိုင်းပါ...  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myPara-char-epoch100-accuracy.png" alt="checking Acc/Loss with Tensorboard" width="800"/>  
</p>  
<div align="center">
  Fig. The accuracy graph of character model with epoch 100
</div> 

<br />

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myPara-char-epoch100-loss.png" alt="checking Acc/Loss with Tensorboard" width="800"/>  
</p>  
<div align="center">
  Fig. The loss graph of character model with epoch 100
</div> 

<br />

## Evaluation with Validation.txt0

ဒီဒေတာက program က validation လုပ်ဖို့အတွက် training data ထဲက ဆွဲထုတ်ထားတဲ့ ဒေတာပါ။  
အဲဒါကိုပဲ သုံးပြီး ပြန် evaluation လုပ်ကြည့်တာ...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ python ./eval.py --model ./runs/1631618306/checkpoints/model-32000 --vocab_filepath ./runs/1631618306/checkpoints/vocab --eval_filepath ./validation.txt0
...
...
...
0.9001823663711548
0.8666810393333435
0.9979985356330872
0.11115581542253494
0.05955391749739647
0.977220892906189
0.9973459243774414
0.14262501895427704
0.9983453750610352
0.973921000957489
0.7028488516807556
0.9999891519546509
0.9970781803131104
0.9920246601104736
0.06250093132257462
0.9981074929237366
0.7910733819007874
0.08610323071479797
0.7639585137367249
0.9994668960571289
0.9160317182540894
Accuracy: 0.966539
```

## Evaluation with Open Test Data

ဒီဒေတာက လုံးဝ open-test ဒေတာပါ  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ python ./eval.py --model ./runs/1631618306/checkpoints/model-32000 --vocab_filepath ./runs/1631618306/checkpoints/vocab --eval_filepath ./validation.txt1
...
...
...
0.33295318484306335
0.7900525331497192
0.21132522821426392
0.5631528496742249
0.1898920238018036
0.49018043279647827
0.7191677093505859
0.29480621218681335
0.10198315978050232
0.1400306522846222
0.9661251306533813
0.28176015615463257
0.30746933817863464
0.2912597060203552
0.07379546761512756
0.3612543046474457
0.6867332458496094
Accuracy: 0.543544
```

## Evaluation with Closed-Test Data

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ python ./eval.py --model ./runs/1631618306/checkpoints/model-32000 --vocab_filepath ./runs/1631618306/checkpoints/vocab --eval_filepath ./my-para/data/closed-test.final
...
...
...
0.06834502518177032
0.1330200433731079
0.09447325021028519
0.10914053022861481
0.199232280254364
0.024631556123495102
0.5442995429039001
0.09711595624685287
0.5433968305587769
0.0807630717754364
0.05371960252523422
0.2358183115720749
0.9972859621047974
0.10500875115394592
0.040762852877378464
0.07162264734506607
0.02737630344927311
0.560492992401123
0.030253712087869644
0.1330290585756302
0.1289135217666626
Accuracy: 0.671
```

## Char, epoch 200 Training

```
TRAIN 2021-09-14T21:27:11.167425: step 131799, loss 0.00803139, acc 0.96875
(0, 0, 1, 0, 1, 1, 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0) [0.9998082  0.9640413  0.04790479 0.9999997  0.01406619 0.03604193
 0.47977725 0.99961776 0.9843824  0.9999993  0.02484133 0.99999917
 0.01383992 0.03669196 0.95883846 0.97135824 0.99974024 0.03899364
 0.03178833 0.99194974 0.9920721  0.99915045 0.9733629  0.9881744
 0.9965433  0.33839834 0.03103029 0.033379   0.00782603 0.06816801
 0.7863452  0.0301777  0.9999838  0.9991821  0.09934568 0.97987276
 0.8647701  0.71886253 0.05248119 1.         0.93319297 0.05668609
 0.0673655  0.05602337 0.9999999  0.9968679  0.96542156 0.99922776
 0.9965267  0.99999994 0.9999996  0.9389753  0.80356556 0.07132067
 0.99999994 0.9711472  0.99979764 0.8672038  0.9999532  0.9030611
 0.02672092 0.9924076  0.04271268 0.78086215] [0. 0. 1. 0. 1. 1. 1. 0. 0. 0. 1. 0. 1. 1. 0. 0. 0. 1. 1. 0. 0. 0. 0. 0.
 0. 1. 1. 1. 1. 1. 0. 1. 0. 0. 1. 0. 0. 0. 1. 0. 0. 1. 1. 1. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0.]
TRAIN 2021-09-14T21:27:11.197048: step 131800, loss 0.00861455, acc 0.984375
(1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 1, 1, 1, 0, 1, 0, 1) [0.0666633  0.09248008 0.00494913 0.99996763 0.9998624  0.98887694
 0.9996415  0.9119651  0.9994628  0.06643134 0.89237493 0.99994755
 0.9998723  0.81035614 0.69418985 0.13685837 0.99995244 0.8851657
 0.9962895  0.9999992  0.9893723  0.997094   0.9593931  0.99998605
 0.9999568  0.16513367 0.9999987  0.9313098  0.99953485 0.08055323
 0.9554062  0.99998915 0.02059137 1.         0.8096035  0.10196403
 0.01721132 0.94323486 0.01994065 1.         0.97065514 0.8656875
 0.9999491  0.02141003 0.99289167 0.06201737 0.9999993  0.9942093
 0.99858814 0.99238396 0.97881705 0.12349763 0.9996444  0.998489
 0.9999993  0.10759059 0.9999993  0.04221566 0.0343822  0.16774084
 0.9940543  0.02479621 0.99989855 0.04969526] [1. 1. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 1. 0. 0. 0. 1. 0. 0. 1. 0. 0. 1. 1. 0. 1. 0. 0. 0. 0. 1. 0. 1. 0. 0.
 0. 0. 0. 1. 0. 0. 0. 1. 0. 1. 1. 1. 0. 1. 0. 1.]

real	69m10.247s
user	331m17.438s
sys	39m50.935s
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --num_epochs 200 2>&1 | tee train-char-epoch200.log
```

## Char, 200 epoch, Evaluation with Open Test Data

```
0.41817140579223633
0.8039582371711731
0.11771837621927261
0.8368899822235107
0.08196800947189331
0.13802488148212433
0.4074195921421051
0.2630413770675659
0.3123328387737274
0.26409921050071716
0.2526575028896332
0.061000481247901917
0.9993323683738708
0.9883047342300415
0.6661810874938965
0.09748351573944092
0.26076817512512207
0.4817509949207306
0.566023588180542
Accuracy: 0.557558

real	0m7.403s
user	0m7.896s
sys	0m1.094s
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631625490/checkpoints/model-60000 --vocab_filepath ./runs/1631625490/checkpoints/vocab --eval_filepath ./validation.txt1
```

## Char, 200 epoch, Evaluation with Closed-test Data

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631625490/checkpoints/model-60000 --vocab_filepath ./runs/1631625490/checkpoints/vocab --eval_filepath ./my-para/data/closed-test.final 
...
...
...
0.18231897056102753
0.9920779466629028
0.441364049911499
0.013013259507715702
0.3906610906124115
0.02960198186337948
0.9086000323295593
0.029317649081349373
0.056800492107868195
0.09450982511043549
Accuracy: 0.697

real	0m7.476s
user	0m8.000s
sys	0m1.134s
```

အထက်ပါ ရလဒ်တွေ၊ run ခဲ့တာတွေက manual segmentation လုပ်ထားတဲ့ paraphrase data ကို သုံးခဲ့တယ်။ လက်ရှိ setting အရ character setting နဲ့ run ထားခဲ့တယ်လို့ ယူဆထား...  


## Data Preparation for Syllable Segmentation

myWord Segmentation Tool ကို သုံးပြီးတော့ အောက်ပါအတိုင်း syllable segmentation လုပ်ခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main$ python ./myword.py syllable ./my-para/train.txt ./my-para/train.txt.syl
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main$ python ./myword.py syllable ./my-para/validation.txt0 ./my-para/validation.txt0.syl
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main$ python ./myword.py syllable ./my-para/validation.txt1 ./my-para/validation.txt1.syl
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main$ python ./myword.py syllable ./my-para/open-test.final ./my-para/open-test.final.syl 
```

တစ်ခုရှိတာက အခု syllable ဖြတ်တာက "label\<TAB\>string1\<TAB\>string2" ဆိုတဲ့ format နဲ့ "string1\<TAB\>string2\<TAB\>label" ဆိုတဲ့ format နှစ်မျိုးနဲ့ ရိုက်ထားတဲ့ စာကြောင်းတွေကို တန်းပြီးတော့ myWord ကို parse လုပ်ပြီး ဖြတ်ခဲ့တာမို့ ထွက်လာတဲ့ output က အောက်က ဥပမာ စာကြောင်းတွေမှာ ဖြစ်နေသလိုပါပဲ (မျက်စိနဲ့ကြည့်ရင်တော့ မသိသာ) "label\<SPACE\>\<TAB\>\<SPACE\>string1\<SPACE\>\<TAB\>\<SPACE\>sring2" ဆိုတဲ့ ပုံစံ မျိုး output တွေ ထွက်လာလိမ့်မယ်။  
  
```
0 	 ၁ ၁ ဒေါ် လာ ကျ ပါ တယ် ။ 	 ၁ ၁ နာ ရီ လာ ခေါ် မယ် ။
0 	 ၁ ၁ နာ ရီ ခွဲ အိမ် ပြန် မယ် ။ 	 ၁ ၁ နာ ရီ ခွဲ အ ရောက် လာ ပါ ။
0 	 ၁ ၁ : ၃ ၀ ပြန် ရောက် မယ် လို့ ထင် သ လား ။ 	 ၁ ၁ : ၃ ၀ အ တိ မှာ ပြန် ရောက် လာ ခဲ့ တယ် ။
0 	 ၂ မိုင် ထက် ပို ရှည် တယ် ။ 	 ၂ မိုင် လောက် သွား ရ တယ် ။
0 	 ၄ ရက် အ တွင်း အိမ် ပြန် မယ် ။ 	 ၄ ရက် လောက် နေ ရင် ပြန် လာ ပါ ။
```

အဲဒီ ကိစ္စကို ရှင်းဖိုအတွက် အောက်ပါအတိုင်း sed command ကို သုံးခဲ့တယ်။  
  
```
$ sed -i $'s/ \t /\t/g' ./open-test.final.syl
```
  
Deep Siamese experiment လုပ်မယ့် folder အောက်ကို ကော်ပြီကူးယူခဲ့...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ cp /media/ye/SP\ PHD\ U3/test-myWord/myWord-main/my-para/*.syl .
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ wc *.syl
   1000   16435  142309 open-test.final.syl
  15640  314485 2974426 train.txt.syl
   4692   94009  890123 validation.txt0.syl
   1000   16435  142309 validation.txt1.syl
  22332  441364 4149167 total
```

ပထမ run ခဲ့တဲ့ manual Segmentation နဲ့ ဒေတာကို အောက်ပါအတိုင်း .manual file extension တွေနဲ့ နာမည်ပြောင်း သိမ်းထားခဲ့...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ wc *.manual
   1000   12674  138604 open-test.final.manual
  15640  233644 2893579 train.txt.manual
   4692   69654  865752 validation.txt0.manual
   1000   12674  138604 validation.txt1.manual
  22332  328646 4036539 total
```

Deep Siamese ကို run ဖို့အတွက်... code ထဲကို ဝင်မပြင်ချင်လို့ command prompt ကနေပဲ ဖိုင်နာမည်တွေကို အောက်ပါအတိုင်း ပြောင်းခဲ့တယ်။  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ mv open-test.final.syl open-test.final
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ mv train.txt.syl ./train.txt
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ mv validation.txt0.syl validation.txt0
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ mv validation.txt1.syl validation.txt1
```
## Training with Syllable Unit, 200 Epoch

syllable ဖြတ်ထားတဲ့ word2vec မော်ဒယ်ကို သပ်သပ် မဆောက်ပဲ သူ့လက်ရှိ code နဲ့ပဲ syllble ဖြတ်ထားတဲ့ ဒေတာနဲ့ အလုပ်လုပ်သလားဆိုတာကို သိချင်လို့.... run ပြီး ရလဒ်တွေကို အကြမ်း ကြည့်ဖို့ အောက်ပါအတိုင်း run ခဲ့တယ်။  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --num_epochs 200 2>&1 | tee train-syl-epoch200.log
...
...
...
DEV 2021-09-15T09:54:16.125044: step 38000, loss 0.0410759, acc 0.890625
(1, 0, 1, 1, 1, 1, 0, 0, 0, 1, 0, 0, 1, 1, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 1, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0) [1. 0. 1. 1. 1. 1. 0. 0. 0. 0. 0. 0. 1. 1. 1. 0. 1. 0. 0. 0. 1. 0. 0. 0.
 1. 1. 0. 1. 1. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 1. 0.
 0. 1. 1. 0. 0. 0. 0. 1. 0. 0. 0. 1. 0. 1. 0. 0.]
DEV 2021-09-15T09:54:16.132673: step 38000, loss 0.00826754, acc 0.96875
(0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 1, 1, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 1, 1, 1, 1, 0, 0, 1, 1, 0, 0, 1, 0, 1, 1, 0, 0, 1, 0, 1, 1, 0, 1, 0, 0, 0) [0. 0. 0. 0. 1. 0. 0. 0. 0. 1. 0. 0. 0. 0. 1. 0. 0. 0. 1. 1. 1. 1. 0. 0.
 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 1. 1. 1. 1. 0. 0. 0. 1. 1. 0.
 0. 1. 1. 1. 1. 0. 0. 1. 0. 1. 1. 0. 1. 0. 0. 0.]
DEV 2021-09-15T09:54:16.140162: step 38000, loss 0.0243361, acc 0.953125
(0, 1, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 0, 0, 0) [0. 1. 0. 0. 0. 1. 1. 1. 1. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0. 0. 0. 0. 0.
 1. 0. 0. 0. 0. 0. 1. 0. 1. 1. 0. 1. 1. 1. 0. 0. 0. 0. 0. 0. 0. 1. 1. 0.
 0. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 1. 1. 0. 0. 0.]
DEV 2021-09-15T09:54:16.148006: step 38000, loss 0.00969854, acc 1
(0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0) [0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 1. 0. 0. 1. 0. 0.
 0. 0. 0. 1. 0. 0. 0. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1.
 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0.]
DEV 2021-09-15T09:54:16.156613: step 38000, loss 0.0111736, acc 0.984375
(0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 0, 1, 0, 1, 1, 0, 1, 0, 1) [0. 0. 1. 0. 0. 1. 0. 1. 0. 0. 1. 0. 1. 0. 1. 0. 0. 0. 1. 0. 1. 0. 1. 0.
 0. 0. 0. 0. 1. 1. 0. 0. 1. 1. 1. 0. 0. 1. 0. 1. 0. 0. 0. 1. 0. 0. 0. 0.
 0. 0. 1. 0. 0. 1. 1. 0. 1. 0. 1. 1. 0. 1. 0. 1.]
DEV 2021-09-15T09:54:16.165721: step 38000, loss 0.0297975, acc 0.953125
(0, 0, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0) [0. 0. 0. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 1. 0. 1. 0. 0. 1.
 1. 0. 0. 0. 0. 0. 0. 1. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 1. 0. 0. 0. 0. 1.
 1. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
DEV 2021-09-15T09:54:16.174362: step 38000, loss 0.0131426, acc 0.984375
(1, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 1) [1. 1. 0. 0. 1. 0. 1. 0. 0. 0. 0. 0. 1. 0. 1. 1. 0. 1. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 1. 0. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 1.
 0. 0. 0. 0. 1. 0. 1. 0. 0. 0. 0. 0. 1. 1. 0. 1.]/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:458: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
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
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/numpy/core/_asarray.py:83: VisibleDeprecationWarning: Creating an ndarray from ragged nested sequences (which is a list-or-tuple of lists-or-tuples-or ndarrays with different lengths or shapes) is deprecated. If you meant to do this, you must specify 'dtype=object' when creating the ndarray
  return array(a, dtype, copy=False, order=order)

DEV 2021-09-15T09:54:16.183969: step 38000, loss 0.0086205, acc 1
(0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 1, 0, 1, 0, 0, 1, 1, 0, 0, 1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 1, 0, 1, 0, 1, 0, 1, 1) [0. 1. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 1. 0. 1. 0. 0. 1. 1. 0. 0. 1. 1. 0.
 0. 1. 0. 1. 0. 0. 1. 0. 0. 0. 0. 0. 1. 1. 1. 0. 0. 1. 0. 1. 0. 0. 0. 0.
 0. 0. 1. 0. 1. 1. 0. 0. 1. 0. 1. 0. 1. 0. 1. 1.]
DEV 2021-09-15T09:54:16.193565: step 38000, loss 0.0173112, acc 0.984375
(0, 0, 0, 1, 1, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 1, 0, 1, 0, 0, 1, 1, 1, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1, 1, 0, 0) [0. 0. 1. 1. 1. 0. 0. 0. 1. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 0. 1. 0.
 1. 0. 1. 0. 1. 1. 0. 1. 0. 0. 1. 1. 1. 0. 1. 0. 0. 1. 0. 0. 1. 0. 0. 0.
 0. 0. 1. 0. 1. 0. 0. 0. 0. 1. 1. 0. 1. 1. 0. 0.]
DEV 2021-09-15T09:54:16.203770: step 38000, loss 0.0213961, acc 0.953125
(0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 0, 1, 0, 1, 1, 0, 0, 0, 0, 1, 0, 1, 1, 0, 1, 0, 1, 1, 0, 1, 1, 1, 1, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0) [0. 0. 0. 0. 0. 1. 0. 1. 0. 0. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0.
 1. 1. 0. 0. 1. 0. 1. 1. 0. 0. 0. 0. 1. 0. 1. 1. 0. 1. 0. 1. 1. 0. 1. 1.
 0. 1. 0. 0. 1. 0. 0. 0. 0. 1. 0. 1. 1. 0. 1. 0.]
DEV 2021-09-15T09:54:16.212314: step 38000, loss 0.0107806, acc 0.984375
(0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 1, 1, 0, 0, 1, 0, 0, 1, 0, 1, 1, 0, 0, 1, 0, 0, 1) [0. 0. 0. 0. 0. 1. 0. 0. 1. 0. 1. 0. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 0.
 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 1. 1. 0. 0. 0. 1.
 1. 0. 0. 1. 0. 0. 1. 0. 0. 1. 0. 0. 1. 0. 0. 1.]
DEV 2021-09-15T09:54:16.220745: step 38000, loss 0.0122867, acc 0.984375
(0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 1, 1, 0, 0, 0, 1, 1, 1, 0, 0, 1, 1, 0, 0, 0, 1, 1, 1, 0, 1, 0, 0, 1, 1, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 1) [0. 0. 0. 0. 0. 0. 0. 0. 1. 1. 1. 0. 0. 0. 1. 1. 0. 0. 0. 1. 1. 1. 0. 0.
 1. 1. 0. 0. 0. 1. 1. 1. 0. 1. 0. 0. 1. 1. 0. 0. 1. 0. 0. 1. 0. 0. 1. 0.
 1. 1. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 1.]
DEV 2021-09-15T09:54:16.229206: step 38000, loss 0.0187725, acc 0.96875
(1, 0, 0, 1, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 1, 1, 1, 0, 1, 1, 0, 0, 1, 0, 0, 1, 1, 1, 1, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1) [1. 0. 0. 1. 1. 0. 0. 0. 0. 1. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1.
 0. 0. 0. 1. 1. 1. 1. 0. 1. 1. 0. 0. 1. 0. 1. 1. 1. 1. 1. 0. 0. 1. 0. 0.
 0. 0. 1. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 1. 1. 1.]
DEV 2021-09-15T09:54:16.233908: step 38000, loss 0.00149831, acc 1
(0, 1, 0, 1, 1, 1, 1, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 1, 1, 0) [0. 1. 0. 1. 1. 1. 1. 0. 0. 1. 0. 0. 1. 1. 0. 0. 0. 1. 1. 0.]

tee: train-syl-epoch200.log: No space left on device
Traceback (most recent call last):
  File "./train.py", line 269, in <module>
    saver.save(sess, checkpoint_prefix, global_step=current_step)
  File "/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/training/saver.py", line 1494, in save
    self.export_meta_graph(meta_graph_filename)
  File "/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/training/saver.py", line 1527, in export_meta_graph
    clear_devices=clear_devices)
  File "/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/training/saver.py", line 1750, in export_meta_graph
    **kwargs)
  File "/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/meta_graph.py", line 658, in export_scoped_meta_graph
    as_text=as_text)
  File "/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/graph_io.py", line 69, in write_graph
    file_io.atomic_write_string_to_file(path, graph_def.SerializeToString())
  File "/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/lib/io/file_io.py", line 418, in atomic_write_string_to_file
    write_string_to_file(temp_pathname, contents)
  File "/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/lib/io/file_io.py", line 305, in write_string_to_file
    f.write(file_content)
  File "/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/lib/io/file_io.py", line 104, in write
    compat.as_bytes(file_content), self._writable_file, status)
  File "/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/contextlib.py", line 88, in __exit__
    next(self.gen)
  File "/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/errors_impl.py", line 466, in raise_exception_on_not_ok_status
    pywrap_tensorflow.TF_GetCode(status))
tensorflow.python.framework.errors_impl.ResourceExhaustedError: /home/ye/exp/myPara2/deep-siamese-text-similarity/runs/1631673267/checkpoints/model-38000.meta.tmpf7236d70b7874ec298219b2c9413efcb

real	19m58.564s
user	95m53.243s
sys	11m28.893s
```

HDD space က 10MB ပဲ ကျန်တော့လို့ ပေးတဲ့ error!  

HDD space ကို ထွက်လာအောင် ရှေ့က run ထားခဲ့တဲ့ folder တွေကို တခြား portable HDD ဆီကို ရွှေ့ပြီး ပြန် run ကြည့်ခဲ့...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --num_epochs 200 2>&1 | tee train-syl-epoch200.log
...
...
...
 1. 1. 1. 0. 1. 1. 0. 0. 0. 1. 0. 1. 1. 0. 1. 1.]
TRAIN 2021-09-15T11:19:54.159213: step 131793, loss 0.0051682, acc 0.984375
(0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 1, 1, 1, 1, 0, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 1, 1, 0) [0.99998516 1.         0.937862   0.93402785 0.99650383 0.03971712
 0.9998484  1.         0.9825678  0.99999714 0.43163714 0.9996955
 0.9404271  0.03886712 0.9997964  0.03971712 0.10183023 0.99966615
 0.85627794 0.03368897 0.9019434  0.95260906 0.9999998  0.06745468
 0.01690558 0.21458769 0.10640638 0.9999982  0.99999255 0.11359121
 0.97739875 0.99983525 1.         0.9342618  0.07023177 0.08810733
 0.9999999  0.7938566  0.9710799  0.8994255  0.05233868 0.99995565
 0.998826   0.9840871  0.05474536 0.99995804 0.07632899 1.
 0.9913338  0.99999124 0.04175986 0.99999857 0.9814682  0.9999997
 0.0204247  0.99995697 1.         0.9999951  0.99855787 0.0984255
 0.09804264 0.08111872 0.30226403 0.99890924] [0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 1. 0. 0. 1. 0. 1. 1. 0. 0. 1. 0. 0. 0. 1.
 1. 1. 1. 0. 0. 1. 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 1. 0. 0. 0. 1. 0. 1. 0.
 0. 0. 1. 0. 0. 0. 1. 0. 0. 0. 0. 1. 1. 1. 1. 0.]
TRAIN 2021-09-15T11:19:54.192922: step 131794, loss 0.00981904, acc 0.984375
(0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 1, 0, 0, 1, 0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 1, 0, 1, 1, 1, 0, 0, 1, 0, 0, 1, 0, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0) [0.986989   0.9999629  0.9959353  0.97052985 0.98749155 0.9994624
 0.99975556 0.87390095 0.99995834 0.9999937  0.9999997  0.00970273
 0.02798182 0.99999946 0.05327806 0.9998352  0.9999999  0.05594131
 0.9999754  0.99754333 0.99999964 0.16277774 0.07887408 0.9286348
 0.85760653 0.01934318 0.9999981  0.9999983  0.9862598  0.99131197
 0.03647797 0.9987471  0.01187856 0.94532245 0.06461124 0.01858894
 0.81961185 0.12678027 0.05823305 0.0840304  0.7773534  0.9567414
 0.15049846 1.         0.9916963  0.02443344 0.9999995  0.04998657
 0.06857833 0.9999974  0.99999976 0.9991478  0.01928862 0.9999917
 0.9999999  0.99958026 0.99991983 1.         0.96221703 0.86741114
 0.06325322 0.9999912  0.02756709 0.998279  ] [0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 1. 0. 1. 0. 0. 1. 0. 0. 0. 1. 1. 0.
 0. 1. 0. 0. 0. 0. 1. 0. 1. 0. 1. 1. 0. 1. 1. 1. 0. 0. 1. 0. 0. 1. 0. 1.
 1. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0.]
TRAIN 2021-09-15T11:19:54.225614: step 131795, loss 0.00836769, acc 0.96875
(0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0)/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:458: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
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
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/numpy/core/_asarray.py:83: VisibleDeprecationWarning: Creating an ndarray from ragged nested sequences (which is a list-or-tuple of lists-or-tuples-or ndarrays with different lengths or shapes) is deprecated. If you meant to do this, you must specify 'dtype=object' when creating the ndarray
  return array(a, dtype, copy=False, order=order)
 [0.70262873 0.8825639  0.97493213 0.99952906 0.05576891 0.9934624
 0.9999802  0.07952492 0.9999855  0.13619912 1.         0.9999576
 0.02857307 1.         0.99998236 0.9977072  0.947191   0.9995704
 0.07485552 0.9662322  0.9991987  0.9999949  0.9670943  0.9999994
 0.9999998  1.         0.0807156  1.         0.7092956  0.82743996
 0.01449107 1.         0.88978857 1.         0.9839174  0.9999999
 1.         0.99994266 0.9948607  0.04813676 0.10856461 0.0765016
 0.9903368  1.         0.99939346 0.8866861  0.0903827  0.9985856
 0.99998695 0.8062292  0.98903704 0.88105005 0.9999977  0.49064693
 0.9970016  0.04216099 0.9996086  0.9583801  0.9522927  0.9998589
 0.86979765 0.04062203 0.9997664  0.999989  ] [0. 0. 0. 0. 1. 0. 0. 1. 0. 1. 0. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0.
 0. 0. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 1. 1. 0. 0. 0. 0. 1. 0.
 0. 0. 0. 0. 0. 1. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0.]
TRAIN 2021-09-15T11:19:54.262655: step 131796, loss 0.02074, acc 0.96875
(1, 1, 1, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 1, 0, 1, 1, 0, 1, 1, 1, 0, 1, 0, 0, 0, 0, 0, 1, 1) [0.12568706 0.04201827 0.03086819 0.99969035 0.05373971 0.94110864
 0.99993116 0.95568687 0.04761579 0.7721839  0.7493745  0.9999647
 0.9999913  0.99846774 0.99999994 0.9999626  0.9989488  0.87255245
 1.         0.9994301  0.99999666 0.8256018  0.95672894 0.03900048
 1.         0.9999879  0.08963507 0.99970424 0.99999994 0.9963513
 0.9984763  1.         0.03380157 0.8284018  0.9086743  0.99999994
 0.69758594 0.99999994 0.9725588  1.         0.9999983  0.87700725
 0.99982935 0.9985767  0.05280105 0.2494033  0.99984145 0.03519296
 0.9456786  0.4074406  0.23284441 0.9960382  0.0577459  0.071107
 0.03698673 0.9962464  0.03921128 0.9999149  0.9935477  0.99949706
 0.9396751  0.9999809  0.01261483 0.05638208] [1. 1. 1. 0. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1.
 0. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 1. 0. 1.
 0. 1. 1. 0. 1. 1. 1. 0. 1. 0. 0. 0. 0. 0. 1. 1.]
TRAIN 2021-09-15T11:19:54.297128: step 131797, loss 0.00287009, acc 1
(0, 0, 1, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0) [0.9999985  0.9708165  0.07747564 0.95262486 0.9999994  0.8485772
 0.04563139 0.98893154 0.01449087 0.9999975  0.05807064 0.9999536
 0.9022308  1.         0.9867289  0.9450925  0.1973297  0.1482283
 0.7776127  0.94643676 0.9998791  0.9992713  0.80474716 0.93295753
 0.9936826  0.9999917  0.92702067 0.9999917  0.99999934 0.9999621
 0.99963146 0.96110064 0.9411735  0.8585914  0.92905676 0.91286993
 0.07696564 0.14186282 0.99999994 0.04666561 0.99355614 0.99746996
 0.9720633  0.99438256 0.99995685 0.9999976  0.9946785  0.99998605
 0.9991848  0.11130433 0.11702996 0.9999791  0.97989786 0.05608746
 0.98911446 0.03474864 1.         0.03330117 0.80443484 0.9994811
 0.08572456 0.9991206  0.10588799 0.99987555] [0. 0. 1. 0. 0. 0. 1. 0. 1. 0. 1. 0. 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 1. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 1. 1. 0. 0. 1. 0. 1. 0. 1. 0. 0. 1. 0. 1. 0.]
TRAIN 2021-09-15T11:19:54.327356: step 131798, loss 0.00276665, acc 1
(0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 1, 1, 1, 1, 1, 0, 0, 0, 1, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0) [0.9860582  1.         0.07808739 0.906906   0.9999761  0.01243269
 0.9993784  0.99468744 0.83274424 0.9999961  0.07717638 0.05315494
 0.28447977 0.0491781  0.03617941 0.9999961  1.         0.89795476
 0.06473207 0.05106451 0.9926943  0.07582235 0.9999992  0.9158415
 0.02501248 0.9999686  0.9896145  0.99733955 1.         1.
 0.99995905 0.9592621  0.99996775 0.9981041  0.999999   0.97535723
 0.93019795 0.83783025 0.05481643 0.9999995  0.8389096  0.91179496
 0.9999969  0.05029936 0.87603694 1.         0.02423264 0.99999994
 0.08046148 0.9937046  0.7891175  0.97761583 0.9998183  0.99995995
 1.         0.9926588  0.99973345 1.         0.9999824  0.21561198
 0.9985427  0.99998957 0.99305785 0.9998764 ] [0. 0. 1. 0. 0. 1. 0. 0. 0. 0. 1. 1. 1. 1. 1. 0. 0. 0. 1. 1. 0. 1. 0. 0.
 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 1. 0. 0. 1. 0.
 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0.]
TRAIN 2021-09-15T11:19:54.357324: step 131799, loss 0.0107237, acc 0.984375
(0, 0, 1, 0, 1, 1, 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0) [0.94847864 0.99988943 0.0965892  1.         0.01518003 0.00599404
 0.80823624 0.9943989  0.9817049  0.99998504 0.04447979 0.9995345
 0.04193787 0.07619037 0.9975098  0.78545076 0.87678987 0.05382669
 0.0429753  0.99999964 0.9509113  0.9999357  0.9987072  0.8631615
 0.8523336  0.8300784  0.04888918 0.08776858 0.05049271 0.07060391
 0.99990225 0.14373559 0.98942906 0.9999929  0.03633241 0.99996525
 0.99999964 0.99999917 0.2574068  0.9635168  0.9999925  0.05342663
 0.09490681 0.06292736 0.9884941  0.9997024  0.8498587  0.99741197
 0.9977506  0.9648455  0.99995834 0.99999946 0.828186   0.05815978
 0.99998605 0.90151626 0.9962096  0.8874124  0.99994916 0.01648023
 0.06058297 0.9999835  0.05096401 0.99999493] [0. 0. 1. 0. 1. 1. 0. 0. 0. 0. 1. 0. 1. 1. 0. 0. 0. 1. 1. 0. 0. 0. 0. 0.
 0. 0. 1. 1. 1. 1. 0. 1. 0. 0. 1. 0. 0. 0. 1. 0. 0. 1. 1. 1. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 1. 0. 1. 0.]
TRAIN 2021-09-15T11:19:54.385139: step 131800, loss 0.00349722, acc 1
(1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 1, 1, 1, 0, 1, 0, 1) [0.06003136 0.13051483 0.03910718 0.99973303 0.9998992  0.9309996
 0.9232491  0.51570153 0.9913921  0.02769632 0.9981377  0.99179095
 0.93011636 0.9999616  0.9999994  0.9999959  0.9998623  0.9996069
 0.8352393  0.99992573 0.88245654 0.9999987  0.9999659  0.95959836
 0.9706326  0.07979309 0.8623219  0.999968   0.95721173 0.08853591
 0.99954844 0.9999983  0.04026754 0.9996513  0.9520687  0.135224
 0.03849297 1.         0.02305199 0.9996644  0.90170056 0.9999959
 0.99837273 0.04442282 0.9654944  0.06389835 0.99966526 0.9999971
 0.9537398  0.9705463  0.9867478  0.04378152 0.95737284 0.89382356
 0.9979386  0.13407075 0.94454664 0.04582701 0.02990569 0.04253847
 0.9886646  0.08190372 0.9999982  0.06339355] [1. 1. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 1. 0. 0. 0. 1. 0. 0. 1. 0. 0. 1. 1. 0. 1. 0. 0. 0. 0. 1. 0. 1. 0. 0.
 0. 0. 0. 1. 0. 0. 0. 1. 0. 1. 1. 1. 0. 1. 0. 1.]

real	67m36.242s
user	330m51.890s
sys	39m51.585s
```

## Evaluation of syl, 200 Epoch with Validation Data

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631675547/checkpoints/model-54000 --vocab_filepath ./runs/1631675547/checkpoints/vocab --eval_filepath ./validation.txt0
...
...
...
0.28562480211257935
0.9872654676437378
0.9858872294425964
0.9592834711074829
0.8704239130020142
0.9990317225456238
0.06222686916589737
0.9410238862037659
0.889403760433197
0.019395597279071808
0.8360447883605957
0.9982960224151611
0.9993011951446533
Accuracy: 0.972293

real	0m7.727s
user	0m10.069s
sys	0m1.363s
```

## Evaluation of syl, 200 Epoch with Open Test Data

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631675547/checkpoints/model-54000 --vocab_filepath ./runs/1631675547/checkpoints/vocab --eval_filepath ./validation.txt1
...
...
...
0.9887449741363525
0.4452979266643524
0.8528821468353271
0.04653041064739227
0.46165546774864197
0.13421422243118286
0.28732728958129883
0.3616258502006531
0.17452344298362732
0.9672794342041016
0.14735110104084015
0.11531607806682587
0.30584394931793213
0.1961718201637268
0.07260091602802277
0.9969580173492432
Accuracy: 0.541542

real	0m7.585s
user	0m7.887s
sys	0m1.296s
```

Note: open-test.final.syl နဲ့ validation.txt1 က ဖိုင် အတူတူပဲ  
closed test ကို ကော်ပီကူး...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/data/syl$ cp closed-test.final.syl ../../../
```

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631675547/checkpoints/model-54000 --vocab_filepath ./runs/1631675547/checkpoints/vocab --eval_filepath ./closed-test.final.syl
...
...
...
0.3602466583251953
0.9215807318687439
0.12304315716028214
0.027029892429709435
0.17889904975891113
0.06955845654010773
0.974432110786438
0.024845167994499207
0.06749435514211655
0.09339363127946854
Accuracy: 0.693

real	0m7.392s
user	0m8.042s
sys	0m1.202s
```
char နဲ့တုန်းက open test: 557, closed-test: 697  မို့လို့... 
ရလဒ်မှာ char နဲ့ syl က သိပ်မကွာသလိုပဲ word2vec မော်ဒယ်ကို သပ်သပ်ဆောက်ပြီး command line argument ကနေ ပေးရမယ်လို့ ယူဆခဲ့...  

## Preprocessing, Cutting Only Myanmar Text Columns

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/data/4word2vec/syl$ head -n 3 *
==> closed-test.final.syl <==
1	ကောင်း လိုက် တဲ့ သ တင်း လေး ပါ	ကောင်း သော သ တင်း ပါ ပဲ
0	ခု ဒီ တံ ဆိပ် က ဈေး လိုက် နေ တယ် ။	ဒီ တံ ဆိပ် က ဈေး အ ရမ်း တက် နေ တယ် ။
1	ကျွန် မ ဘက် က စ ပြီး ကျေ အေး ပေး တယ် နော်	ကျွန် မ ဘက် က စ ပြီး ကျေ လည် တာ နော်

==> open-test.final.syl <==
0	၁ ၁ ဒေါ် လာ ကျ ပါ တယ် ။	၁ ၁ နာ ရီ လာ ခေါ် မယ် ။
0	၁ ၁ နာ ရီ ခွဲ အိမ် ပြန် မယ် ။	၁ ၁ နာ ရီ ခွဲ အ ရောက် လာ ပါ ။
0	၁ ၁ : ၃ ၀ ပြန် ရောက် မယ် လို့ ထင် သ လား ။	၁ ၁ : ၃ ၀ အ တိ မှာ ပြန် ရောက် လာ ခဲ့ တယ် ။

==> train.txt.syl <==
 ပျော် စ ရာ ကြီး ပါ	ပျော် စ ရာ ပဲ နော်	y
 ပျော် စ ရာ ကြီး ပါ	ပျော် စ ရာ လို့ ပဲ မြင် တယ်	y
 ပျော် စ ရာ ကြီး ပါ	ပျော် ရွှင် စ ရာ ပါ	y

==> validation.txt0.syl <==
0	တော် ပါ ပေ တယ် လေး စား ဂုဏ် ယူ မိ ပါ တယ်	ထိ ထိ ရောက် ရောက် အ ရေး ယူ ပေး ပါ
1	ဒိုင် ညစ် တယ်	ဒိုင် က ညစ် တာ
0	ကူ ညီ ပေး စေ ချင် ပါ တယ်	ကျွန် တော် တို့ မ လှ လို့ ရ တယ်
```

format က အထက်ပါအတိုင်း training data နဲ့ test data က မတူဘူး။ အဲဒါကြောင့် training အတွက်က col1, col2 ကို ဖြတ်ထုတ်ရမယ်။  
test ဒေတာတွေအတွက်က col2 နဲ့ col3 ကို ဖြတ်ထုတ်ရမယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para$ cat ./print-myanmar-text-columns.sh 
#!/bin/bash

#Note validation.txt1 နဲ့ open-test.final နဲ့က အတူတူပဲ

cut -f1 train.txt > train.f1
cut -f2 train.txt > train.f2

cut -f2 closed-test.final > closed.f2
cut -f3 closed-test.final > closed.f3

cut -f2 open-test.final > open.f2
cut -f3 open-test.final > open.f3
```

အထက်က shell script နဲ့ အောက်ပါအတိုင်း မြန်မာစာ စာကြောင်းပါတဲ့ column တွေကို ဆွဲထုတ်ခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para$ bash ./print-myanmar-text-columns.sh 
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para$ ls *.f{1..3}
closed.f2  closed.f3  open.f2  open.f3  train.f1  train.f2
```

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para$ mv *.f{1..3} ./manual-my/
```
combind all  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my$ head -3 *
==> closed.f2 <==
ကောင်း လိုက် တဲ့ သတင်း လေး ပါ
ခု ဒီ တံဆိပ် က ဈေးလိုက် နေ တယ် ။
ကျွန်မ ဘက် က စ ပြီး ကျေအေး ပေး တယ် နော်

==> closed.f3 <==
ကောင်း သော သတင်း ပါ ပဲ
ဒီ တံဆိပ် က ဈေး အရမ်း တက် နေ တယ် ။
ကျွန်မ ဘက် က စ ပြီး ကျေလည် တာ နော်

==> open.f2 <==
၁၁ ဒေါ်လာ ကျ ပါ တယ် ။
၁၁ နာရီ ခွဲ အိမ် ပြန် မယ် ။
၁၁:၃၀ ပြန်ရောက် မယ် လို့ ထင် သလား ။

==> open.f3 <==
၁၁ နာရီ လာ ခေါ် မယ် ။
၁၁ နာရီ ခွဲ အရောက် လာ ပါ ။
၁၁:၃၀ အတိ မှာ ပြန်ရောက် လာ ခဲ့ တယ် ။

==> train.f1 <==
 ပျော် စရာ ကြီး ပါ
 ပျော် စရာ ကြီး ပါ
 ပျော် စရာ ကြီး ပါ

==> train.f2 <==
ပျော် စရာ ပဲ နော်
ပျော် စရာ လို့ ပဲ မြင် တယ်
ပျော်ရွှင် စရာ ပါ
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my$ cat train.f1 train.f2 closed.f2 closed.f3 open.f2 open.f3 > mypara-all.manual
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my$ wc mypara-all.manual 
  35280  245584 3199139 mypara-all.manual
```
အခု ဖြတ်ပြီးသွားတာက manual ဖြတ်ထားတဲ့ ဒေတာအတွက်...  

Syllable အတွက်လည်း အောက်ပါအတိုင်း လုပ်ခဲ့တယ်။   
အရင်ဆုံး shell script ကို ပြင်ဆင်ခဲ့တယ်။   

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para$ cat ./print-myanmar-text-columns-syl.sh 
#!/bin/bash

#Note validation.txt1 နဲ့ open-test.final နဲ့က အတူတူပဲ

cut -f1 train.txt.syl > ./syl-my/train.f1
cut -f2 train.txt.syl > ./syl-my/train.f2

cut -f2 closed-test.final.syl > ./syl-my/closed.f2
cut -f3 closed-test.final.syl > ./syl-my/closed.f3

cut -f2 open-test.final.syl > ./syl-my/open.f2
cut -f3 open-test.final.syl > ./syl-my/open.f3

```

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para$ bash ./print-myanmar-text-columns-syl.sh 
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para$ cd syl-my/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/syl-my$ head -n 3 *
==> closed.f2 <==
ကောင်း လိုက် တဲ့ သ တင်း လေး ပါ
ခု ဒီ တံ ဆိပ် က ဈေး လိုက် နေ တယ် ။
ကျွန် မ ဘက် က စ ပြီး ကျေ အေး ပေး တယ် နော်

==> closed.f3 <==
ကောင်း သော သ တင်း ပါ ပဲ
ဒီ တံ ဆိပ် က ဈေး အ ရမ်း တက် နေ တယ် ။
ကျွန် မ ဘက် က စ ပြီး ကျေ လည် တာ နော်

==> open.f2 <==
၁ ၁ ဒေါ် လာ ကျ ပါ တယ် ။
၁ ၁ နာ ရီ ခွဲ အိမ် ပြန် မယ် ။
၁ ၁ : ၃ ၀ ပြန် ရောက် မယ် လို့ ထင် သ လား ။

==> open.f3 <==
၁ ၁ နာ ရီ လာ ခေါ် မယ် ။
၁ ၁ နာ ရီ ခွဲ အ ရောက် လာ ပါ ။
၁ ၁ : ၃ ၀ အ တိ မှာ ပြန် ရောက် လာ ခဲ့ တယ် ။

==> train.f1 <==
 ပျော် စ ရာ ကြီး ပါ
 ပျော် စ ရာ ကြီး ပါ
 ပျော် စ ရာ ကြီး ပါ

==> train.f2 <==
ပျော် စ ရာ ပဲ နော်
ပျော် စ ရာ လို့ ပဲ မြင် တယ်
ပျော် ရွှင် စ ရာ ပါ
```

combind all Myanmar text...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/syl-my$ ls
closed.f2  closed.f3  open.f2  open.f3  train.f1  train.f2

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/syl-my$ cat train.f1 train.f2 closed.f2 closed.f3 open.f2 open.f3 > ./mypara-all.syl

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/syl-my$ wc ./mypara-all.syl 
  35280  335561 3288936 ./mypara-all.syl

```

ဒီတစ်ခါတော့ myWord နဲ့ ဖြတ်ထားတာအတွက်ကို ပြင်ဆင်မယ်...  
word segmentation ကို myWord ကိုသုံးခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main$ time python ./myword.py word ./my-para/manual-my/mypara-all.manual ./my-para/word-my/mypara-all.word

real	3m40.834s
user	3m40.691s
sys	0m0.128s
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main$ 
```

check the no. of sentences ...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my$ wc mypara-all.word 
  35280  271501 3224985 mypara-all.word
```


## Building Word2Vec, fasttext Models for Syllable

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/data/4word2vec/syl$ cp all-para.txt /home/ye/4github/syl-ngram/ref/playing_with_fasttext/
```

word2vec နဲ့ fasttext မော်ဒယ် နှစ်ခုကို အောက်ပါအတိုင်း program တစ်ပုဒ်ကို refer/update လုပ်ပြီး ဆောက်ခဲ့တယ်။  
ကိုယ့်စက်ထဲမှာက command line နဲ့ word2vec ကို ဆောက်တာ၊ fasttext command နဲ့ ဆောက်တာလည်း လုပ်လို့ ရတယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ python ./Sherlock_Holmes_fasttext.py ./all-para.txt
[nltk_data] Downloading package punkt to /home/ye/nltk_data...
[nltk_data]   Package punkt is already up-to-date!
[nltk_data] Downloading package vader_lexicon to /home/ye/nltk_data...
[nltk_data]   Package vader_lexicon is already up-to-date!
[nltk_data] Downloading package stopwords to /home/ye/nltk_data...
[nltk_data]   Package stopwords is already up-to-date!
[nltk_data] Downloading package wordnet to /home/ye/nltk_data...
[nltk_data]   Package wordnet is already up-to-date!
Read 0M words
Number of words:  1327
Number of labels: 0
Progress: 100.0% words/sec/thread:  121556 lr:  0.000000 avg.loss:  2.530337 ETA:   0h 0m 0s
print(w2v_model.wv.most_similar('ကျောင်း', topn = 20)):
[('ပွား', 0.8231478929519653), ('ပ', 0.8066482543945312), ('ကပ်', 0.7989271283149719), ('ပေါင်း', 0.7834250926971436), ('သော်', 0.7466834783554077), ('ပြည်', 0.7398074865341187), ('ကမ္ဘာ', 0.7311006784439087), ('ငဉ်', 0.7295233011245728), ('မော်', 0.7273308634757996), ('ပွဲ', 0.7215660214424133), ('ခိုင်', 0.7213265299797058), ('ဇာ', 0.7209988236427307), ('ရန်', 0.7161328792572021), ('စည်း', 0.7160824537277222), ('တိုး', 0.706506073474884), ('ဩ', 0.7056975364685059), ('သတ်', 0.7045521140098572), ('များ', 0.704490065574646), ('မြိုင့်', 0.7007927894592285), ('သင်္ကန်း', 0.699887752532959)] 

print(ft_model.get_nearest_neighbors('ကျောင်း', k = 20))
[(0.8953080177307129, 'ဟောင်း'), (0.8905119895935059, 'ညောင်း'), (0.8808940052986145, 'ဘောင်း'), (0.8607454299926758, 'ယောင်း'), (0.8558489084243774, 'အောင်း'), (0.8547207117080688, 'ဆောင်း'), (0.8530898690223694, 'လောင်း'), (0.8524867296218872, 'သောင်း'), (0.8471701741218567, 'မောင်း'), (0.8411751985549927, 'ချောင်း'), (0.8342663049697876, 'ရောင်း'), (0.8330811262130737, 'ထောင်း'), (0.8247120380401611, 'စောင်း'), (0.8135457038879395, 'နှောင်း'), (0.7960479855537415, 'ဖောင်း'), (0.7959949374198914, 'ကောင်း'), (0.7523844838142395, 'ပြောင်း'), (0.7491981387138367, 'ကြောင်း'), (0.7450031042098999, 'ကျင်း'), (0.7447229623794556, 'နောင်း')] 

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ 
```

ပထမ မြင်ရတာက word2vec မော်ဒယ်ရဲ့ "ကျောင်း" ဆိုတဲ့ syllable နဲ့ similar ဖြစ်တဲ့ syllable တွေကို ဆွဲထုတ်ထားတာ။   
ဒုတိယ မြင်ရတာက fasttext မော်ဒယ်ရဲ့ "ကျောင်း" ဆိုတဲ့ syllable နဲ့ similar ဖြစ်တဲ့ syllable တွေကို ဆွဲထုတ်ထားတာ။    

ခု ဆောက်ခဲ့တာက myPara Corpus ထဲမှာ ရှိတဲ့ စာလုံးတွေ ကို syllable ဖြတ်ထားတာနဲ့ပဲ ဆောက်ထားတာ။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ head -n 2 ./all-para.word2vec 
1784 500
ပါ 0.37244356 0.56611603 0.48474115 0.6031777 -0.4505382 -0.2746808 0.12651987 0.12649426 0.045680463 0.26101395 0.21693195 0.12225574 0.067934416 0.2673442 0.15868858 -0.24570772 -0.38072526 -0.06830177 -0.5683561 0.19374624 0.17118008 0.016827634 0.11786197 -0.16147865 0.08785961 -0.46517852 -0.35112914 0.068276875 0.020713389 0.041030068 -0.035507496 0.43896672 0.3029661 0.15723917 -0.03690397 0.020477975 0.21211721 -0.03776245 -0.14975749 -0.532014
...
...
```

fasttext ရဲ့ output ကတော့ လောလောဆယ် binary format နဲ့ပဲ ရှိသေးတယ်။  


## Convert fasttext bin to vec Format

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ cat fasttext_bin-to-vec.py 
import sys
from fasttext import load_model
#import tensorflow as tf
#from fasttext import load_word2vec_format

# Ye, LST
# I updated this code: https://stackoverflow.com/questions/58337469/how-to-save-fasttext-model-in-vec-format
#Ref: https://stackoverflow.com/questions/48017343/how-to-convert-gensim-word2vec-model-to-fasttext-model


# original BIN model loading
f = load_model(sys.argv[1])
lines=[]

# get all words from model
words = f.get_words()

with open(sys.argv[2],'w') as file_out:
    
    # the first line must contain number of total words and vector dimension
    file_out.write(str(len(words)) + " " + str(f.get_dimension()) + "\n")

    # line by line, you append vectors to VEC file
    for w in words:
        v = f.get_word_vector(w)
        vstr = ""
        for vi in v:
            #config = tf.ConfigProto( device_count = {'GPU': 1 , 'CPU': 56} ) 
            vstr += " " + str(vi)
        try:
            file_out.write(w + vstr+'\n')
        except:
            pass
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$
```

fasttext bin ဖိုင်ကနေ vec ကို ပြောင်းထားခဲ့... လိုအပ်ရင် သုံးဖို့.... Deep Siamese မှာက text format သို့မဟုတ် vec format ရော binary format ကိုရော ခွင့်ပြုထားလို့....  
ပြီးတော့ လူအနေနဲ့က ကိုယ်ဆောက်ထားတဲ့ word2vec, fasttext မော်ဒယ်တွေကိုလည်း မျက်လုံးနဲ့ ကြည့်ပြီး confirmation လုပ်တာက ကောင်းလို့...  

အောက်ပါအတိုင်း command ပေးပြီး run ခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ python ./fasttext_bin-to-vec.py ./all-para.fasttext.bin all-para.fasttext.vector
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
```

output vector ဖိုင်ကို confirm လုပ်ခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ head -n 3 ./all-para.fasttext.vector 
1327 500
y 0.11803807 -0.0059538484 -0.039868176 0.06798492 -0.04294115 -0.04061252 0.038582884 -0.045880213 0.17151836 -0.049289834 -0.08403759 0.0075357365 0.013414924 -0.015835846 -0.029434219 0.04345471 0.044386454 -0.053039677 0.0034440125 0.048566647 -0.08146793 0.019674815 0.21577293 -0.0076261684 -0.06369582 -0.10587478 0.058592193 0.06362913 0.05232598 0.033913843 0.10804905 -0.03561741 0.04159803 -0.012685538 0.0046959985 -0.028543212 -0.002129108 -0.03172332 0.04909301 -0.018985532 0.077273086 0.022501929 -0.02081753 -0.03644567 -0.0767379 0.029325014 0.010480709 0.13495953 0.020376649 -0.00395286 0.12773803 0.018018143 0.06888831 -0.014275079 0.030391939 -0.10680618 -0.054560322 -0.01206048 -0.025071673 0.059077114 0.020614766 0.0019675284 0.016606526 -0.06658499 0.05477988 -0.027976317 0.012254027 0.050258808 0.046026204 -0.11615581 -0.08595513 -0.04720106 -0.02644769 0.029198378 0.08464057 -0.0
```


## word2vec, fasttext Preparation for Word Unit (i.e. manually segmented)

လုပ်လက်စနဲ့ တခါတည်း Word Unit အတွက်လည်း word2vec နဲ့ fasttext မော်ဒယ်တွေကို myPara Corpus နဲ့ ဆောက်ထားခဲ့။  
Note: အချိန်မှီရင် myWord corpus နဲ့ myPara ကို ပေါင်းပြီး word2vec မော်ဒယ် အကြီး ဆောက်ပြီးတော့ experiment လုပ်ကြည့်ရန်။  
တစ်ခုရှိတာက အဲဒီလို လုပ်လိုက်ရင် character နဲ့ run ထားတဲ့ မော်ဒယ်နဲ့တော့ direct comparison လုပ်ဖို့ ခက်လိမ့်မယ်။  

လောလောဆယ်တော့ Word Unit အတွက်လည်း myPara Corpus နဲ့ အောက်ပါအတိုင်း word2vec, fasttext တွေကို ပြင်ဆင်ခဲ့...  
final Output အနေနဲ့ က အောက်ပါသုံးဖိုင် ရမယ်။  

- all-para.word2vec
- all-para.fasttext.bin
- all-para.fasttext.vector

အလုပ်လုပ်မယ့် folder ဆီကို mypara corpus manual segmentation ဒေတာကို ကော်ပီကူး...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my$ cp mypara-all.manual /home/ye/4github/syl-ngram/ref/playing_with_fasttext/
```

word2vec နဲ့ fasttext မော်ဒယ်ဆောက်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ python ./Sherlock_Holmes_fasttext.py ./mypara-all.manual 
[nltk_data] Downloading package punkt to /home/ye/nltk_data...
[nltk_data]   Package punkt is already up-to-date!
[nltk_data] Downloading package vader_lexicon to /home/ye/nltk_data...
[nltk_data]   Package vader_lexicon is already up-to-date!
[nltk_data] Downloading package stopwords to /home/ye/nltk_data...
[nltk_data]   Package stopwords is already up-to-date!
[nltk_data] Downloading package wordnet to /home/ye/nltk_data...
[nltk_data]   Package wordnet is already up-to-date!
Read 0M words
Number of words:  2524
Number of labels: 0
Progress: 100.0% words/sec/thread:  166157 lr:  0.000000 avg.loss:  2.373572 ETA:   0h 0m 0s
print(w2v_model.wv.most_similar('ကျောင်း', topn = 20)):
[('ပေါ်ထွန်း', 0.9712773561477661), ('စိုက်ပျိုး', 0.9701921343803406), ('သော်လည်း', 0.9683841466903687), ('ကျမ်းဂန်', 0.966464102268219), ('သစ်ပင်', 0.9655385613441467), ('ပြေး', 0.9643632769584656), ('ယောင်', 0.9635617136955261), ('အားနည်းသူ', 0.9624178409576416), ('အမှာစကား', 0.96114182472229), ('အတွင်း', 0.9610957503318787), ('ဒုတိယ', 0.9609416723251343), ('ကိုး', 0.9603080153465271), ('ကာလ', 0.9600256681442261), ('မြွက်ကြား', 0.9593163728713989), ('ကယုကယ', 0.9589902758598328), ('စစ်ပွဲ', 0.9579262137413025), ('ပွတ်', 0.9576618075370789), ('ကိုယ်ဝန်', 0.9568699598312378), ('ချေ', 0.9567964673042297), ('ကျောင်းအုပ်ကြီး', 0.9552498459815979)] 

print(ft_model.get_nearest_neighbors('ကျောင်း', k = 20))
[(0.9846287965774536, 'ဟောင်း'), (0.9821839928627014, 'ရောင်း'), (0.9801282286643982, 'လောင်း'), (0.9791935682296753, 'ဖောင်း'), (0.9789695739746094, 'ချောင်း'), (0.9788998961448669, 'ရလဒ်ကောင်း'), (0.9776743054389954, 'ကံကောင်း'), (0.9726752042770386, 'လည်းကောင်း'), (0.9718174934387207, 'ဆောင်း'), (0.971022367477417, 'စုဆောင်း'), (0.9681249260902405, 'မောင်း'), (0.966025710105896, 'စောင်း'), (0.9654709696769714, 'နေကောင်း'), (0.964064359664917, 'တောင်း'), (0.9635544419288635, 'ကားမောင်း'), (0.9628528356552124, 'နေမကောင်း'), (0.9599199295043945, 'ကောင်း'), (0.9592843055725098, 'အကောင်း'), (0.9579277634620667, 'ကောင်းကောင်း'), (0.9559436440467834, 'ရောင်ဆင်း')] 

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ 
```

fasttest မော်ဒယ်က bin ပဲ လက်ရှိ output အနေနဲ့ ရသေးတာမို့ အောက်ပါအတိုင်း vec (normal text file format) ကို ပြောင်းခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ python ./fasttext_bin-to-vec.py ./all-para.fasttext.bin all-para.fasttext.vector
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.


(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ ls ./mypara-manual/
all-para.fasttext.bin  all-para.fasttext.vector  all-para.word2vec  mypara-all.manual
```

## word2vec, fasttext Preparation for Word Unit Segmented with myWord Segmentation Tool

ဒီတစ်ခါတော့ myWord Segmentation Tool နဲ့ ဖြတ်ထားတဲ့ ဒေတာကိုလည်း word2vec နဲ့ fasttext တွေဆောက်မယ်။  

အရင်ဆုံး စာလုံးဖြတ်ထားတဲ့ file ကို အလုပ်လုပ်မယ့် folder ဆီကို ကော်ပီကူး...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my$ cp mypara-all.word /home/ye/4github/syl-ngram/ref/playing_with_fasttext/
```

word2vec (text file format) နဲ့ fasttext (binary file) ကို ရဖို့အတွက် အောက်ပါအတိုင်း run ခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ python ./Sherlock_Holmes_fasttext.py ./mypara-all.word 
[nltk_data] Downloading package punkt to /home/ye/nltk_data...
[nltk_data]   Package punkt is already up-to-date!
[nltk_data] Downloading package vader_lexicon to /home/ye/nltk_data...
[nltk_data]   Package vader_lexicon is already up-to-date!
[nltk_data] Downloading package stopwords to /home/ye/nltk_data...
[nltk_data]   Package stopwords is already up-to-date!
[nltk_data] Downloading package wordnet to /home/ye/nltk_data...
[nltk_data]   Package wordnet is already up-to-date!
Read 0M words
Number of words:  2270
Number of labels: 0
Progress: 100.0% words/sec/thread:  165331 lr:  0.000000 avg.loss:  2.473827 ETA:   0h 0m 0s
print(w2v_model.wv.most_similar('ကျောင်း', topn = 20)):
[('ဝင်', 0.9266782999038696), ('ကြီးပြင်း', 0.9038617610931396), ('ပြေး', 0.8990140557289124), ('ထွန်း', 0.89654141664505), ('ပွဲ', 0.8948243856430054), ('ပန်း', 0.8947284817695618), ('ခိုင်', 0.8942050933837891), ('ကပ်', 0.8937804698944092), ('ရပ်နား', 0.8883771896362305), ('ဘျမ်း', 0.8875871300697327), ('၄', 0.886764645576477), ('စီးပွား', 0.8851052522659302), ('ဇကာ', 0.8846842646598816), ('ဝင်ရောက်', 0.8842604756355286), ('သနည်း', 0.882266104221344), ('အိမ်', 0.8776984810829163), ('ပွား', 0.8749026656150818), ('တံကဲ', 0.8732095956802368), ('ပျောက်ပျက်', 0.8730794787406921), ('မောင်း', 0.8730676770210266)] 

print(ft_model.get_nearest_neighbors('ကျောင်း', k = 20))
[(0.9544370770454407, 'သရဖူဆောင်း'), (0.9521687030792236, 'စုဆောင်း'), (0.9521067142486572, 'ရောင်း'), (0.9479786157608032, 'ဖောင်း'), (0.9418590068817139, 'ကံကောင်း'), (0.9414095878601074, 'ဟောင်း'), (0.9406473636627197, 'ချောင်း'), (0.937873363494873, 'မောင်း'), (0.9377909898757935, 'ဆောင်းပါး'), (0.9377263188362122, 'လောင်း'), (0.9371371865272522, 'ကြိမ်းမောင်း'), (0.9367919564247131, 'ဆောင်း'), (0.9364582300186157, 'ရှေးဟောင်း'), (0.9305664300918579, 'အောင်း'), (0.9292629957199097, 'ကျောင်းသား'), (0.9214203953742981, 'အကောင်း'), (0.9205161929130554, 'ဖျောင်းဖျ'), (0.9190094470977783, 'ဘုန်းကြီးကျောင်း'), (0.9188613891601562, 'ကူးပြောင်း'), (0.9045475721359253, 'ကောင်း')] 

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$
```

fasttext bin ကနေ vector plain text format ရအောင် အောက်ပါအတိုင်း လုပ်ခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ python ./fasttext_bin-to-vec.py ./all-para.fasttext.bin all-para.fasttext.vector
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ mv all-para.* ./mypara-word/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ cd mypara-word/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext/mypara-word$ ls
all-para.fasttext.bin  all-para.fasttext.vector  all-para.word2vec
```

Deep Siamese run မယ့် folder အောက်ကို ဆောက်ထားတဲ့ word2vec, fasttext တွေကို ကော်ပီကူးခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ cp -r mypara-manual /home/ye/exp/myPara2/deep-siamese-text-similarity/my-para/data/w2v_fasttext/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ cp -r mypara-syl /home/ye/exp/myPara2/deep-siamese-text-similarity/my-para/data/w2v_fasttext/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ cp -r mypara-word /home/ye/exp/myPara2/deep-siamese-text-similarity/my-para/data/w2v_fasttext/
```

## Retraining with Syllable Unit, 200 Epoch (for this time, I will use word2vec)

word2vec နဲ့ fasttest folder က အောက်ပါ path မှာ...  

```
/home/ye/exp/myPara2/deep-siamese-text-similarity/my-para/data/w2v_fasttext
```

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./my-para/data/w2v_fasttext/mypara-syl/all-para.word2vec --embedding_dim 500 --num_epochs 200 2>&1 | tee train-syl-epoch200-w2v.log1
```

အောက်ပါအတိုင်း error ပေးနေ...  

```
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:465: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])

Parameters:
ALLOW_SOFT_PLACEMENT=True
BATCH_SIZE=64
CHECKPOINT_EVERY=1000
DROPOUT_KEEP_PROB=1.0
EMBEDDING_DIM=500
EVALUATE_EVERY=1000
HIDDEN_UNITS=50
IS_CHAR_BASED=False
L2_REG_LAMBDA=0.0
LOG_DEVICE_PLACEMENT=False
NUM_EPOCHS=200
TRAINING_FILES=train.txt
WORD2VEC_FORMAT=text
WORD2VEC_MODEL=./my-para/data/w2v_fasttext/mypara-syl/all-para.word2vec

Loading training data from train.txt
Traceback (most recent call last):
  File "./train.py", line 61, in <module>
    FLAGS.batch_size, FLAGS.is_char_based)
  File "/home/ye/exp/myPara2/deep-siamese-text-similarity/input_helpers.py", line 180, in getDataSets
    x1_text, x2_text, y=self.getTsvData(training_paths)
  File "/home/ye/exp/myPara2/deep-siamese-text-similarity/input_helpers.py", line 87, in getTsvData
    y.append(int(l[2]))
ValueError: invalid literal for int() with base 10: 'y'

real	0m2.519s
user	0m2.666s
sys	0m0.998s
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ 

getTsvData  y.append(int(l[2])) ValueError: invalid literal for int() with base 10: 'y'
```

Debug လုပ်ကြည့်တော့ သူက sentence level training လုပ်တဲ့အခါမှာ label ကို 0, 1 ထားတယ်။  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/sent-data$ head train_snli.txt
A person on a horse jumps over a broken down airplane.	A person is at a diner, ordering an omelette.	0
A person on a horse jumps over a broken down airplane.	A person is outdoors, on a horse.	1
Children smiling and waving at camera	There are children present	1
Children smiling and waving at camera	The kids are frowning	0
A boy is jumping on skateboard in the middle of a red bridge.	The boy skates down the sidewalk.	0
A boy is jumping on skateboard in the middle of a red bridge.	The boy does a skateboarding trick.	1
An older man sits with his orange juice at a small table in a coffee shop while employees in bright colored shirts smile in the background.	A boy flips a burger.	0
Two blond women are hugging one another.	The women are sleeping.	0
Two blond women are hugging one another.	There are women showing affection.	1
A few people in a restaurant setting, one of them is drinking orange juice.	The people are sitting at desks in school.	0
```

ပြီးတော့ နာမည် သို့မဟုတ် phrase အနေနဲ့ training လုပ်တဲ့အခါမှာက label အားလုံးကို y ပဲ ထားထားတာ...  
အထက်မှာ ငါရခဲ့တဲ့ ရလဒ်တွေက အဲဒီလို y တွေကိုပဲ ရွေးထုတ်ထားပြီး training လုပ်ခဲ့တဲ့ ရလဒ်တွေ...  

လောလောဆယ် ပြင်ဆင်ထားတဲ့ ဒေတာတွေက y တွေချည်းပဲ မို့ အဲဒါနဲ့ပဲ အရင် training လုပ်ကြည့်မယ်။ အဲဒါနဲ့ ရလဒ်ကောင်းရင်လည်း အဲဒါကို ယူလို့ရတယ်။ သုံးလို့ ရတယ်။  
"y" တွေကို "1" အဖြစ် ပြောင်းတာကို အောက်ပါအတိုင်း လုပ်ခဲ့...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ mv train.txt train.syl.txt
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ cp train.syl.txt train.sent.txt
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ cut -f 3 ./train.sent.txt > f3
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ sed -i 'y/y/1^C
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ wc f3
15640 15640 31280 f3
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ grep -c "y" ./f3
15640
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ sed -i 'y/y/1/' ./f3

(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ cut -f 1,2 ./train.sent.txt > f12
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ head -n 3 ./f12
 ပျော် စ ရာ ကြီး ပါ	ပျော် စ ရာ ပဲ နော်
 ပျော် စ ရာ ကြီး ပါ	ပျော် စ ရာ လို့ ပဲ မြင် တယ်
 ပျော် စ ရာ ကြီး ပါ	ပျော် ရွှင် စ ရာ ပါ
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ paste ./f12 ./f3 > train.txt
```

ဖိုင်ကို confirm လုပ်ခဲ့...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ head train.txt
 ပျော် စ ရာ ကြီး ပါ	ပျော် စ ရာ ပဲ နော်	1
 ပျော် စ ရာ ကြီး ပါ	ပျော် စ ရာ လို့ ပဲ မြင် တယ်	1
 ပျော် စ ရာ ကြီး ပါ	ပျော် ရွှင် စ ရာ ပါ	1
 ပျော် စ ရာ ကြီး ပါ	ပျော် စ ရာ လေး ပေါ့	1
 ပျော် စ ရာ ကြီး ပါ	ပျော် စ ရာ ပဲ	1
 ပျော် စ ရာ ကြီး ပါ	ပျော် တယ် ကြည် နူး တယ်	1
၎င်း ဓူ ဝံ ကြယ် သည် ကမ္ဘာ ၏ မြောက် ဝင် ရိုး စွန်း တွင် တည် ရှိ ပြီး မြောက် အ ရပ် ကို အ မြဲ ညွှန် ပြ ပေး သည် ။ 	၎င်း ဓူ ဝံ ကြယ် သည် ကမ္ဘာ ၏ မြောက် ဝင် ရိုး စွန်း တွင် တည် ရှိ ပြီး မြောက် အ ရပ် ကို အ မြဲ ညွှန် ပေး သည် ။	1
၅ ၀ ၀ ကီ လို မီ တာ မိုင် ၉ ၀ ၀ ၀ ရှည် မျော သည် ။	ကမ်း ရိုး တန်း အ လျား ၁ ၄	1
A p p l e ကုန် တံ ဆိပ် ဖုန်း များ သည် အ ရည် အ သွေး ကောင်း မွန် ကြ သည် ။	A p p l e ကုန် အ မှတ် တံ ဆိပ် ဖုန်း များ သည် အ ရည် အ သွေး ကောင်း မွန် ကြ သည် ။	1
D e l i v e r y ပို့ ရန် ကောင် လေး လို အပ် ပါ တယ် ။	D e l i v e r y ပို့ ရန် ကောင်း က လေး လို အပ် ပါ တယ် ။	1
```

လက်ရှိ 1 အဖြစ် ပြောင်းထားတဲ့ train.txt ဖိုင်ကို သုံးပြီးတော့ Training ကို လုပ်ကြည့်မယ်... I hope it will be OK...  

```
time python ./train.py --nois_char_based --word2vec_model ./my-para/data/w2v_fasttext/mypara-syl/all-para.word2vec --embedding_dim 500 --num_epochs 200 2>&1 | tee train-syl-epoch200-w2v.log1
...
...
...
TRAIN 2021-09-15T20:43:04.179927: step 6557, loss 1.51727e-07, acc 1
(1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1) [0.00093147 0.00042711 0.0005228  0.00044483 0.00049942 0.00051216
 0.00052045 0.00048873 0.00091181 0.0005256  0.00047738 0.0004586
 0.00042555 0.00065418 0.00044551 0.000524   0.000528   0.00052869
 0.00056297 0.00056543 0.00041463 0.00048667 0.0004517  0.00092714
 0.00046745 0.00056901 0.00043226 0.00046505 0.00058091 0.00077819
 0.00057027 0.00051216 0.00048898 0.00047999 0.00055656 0.00061859
 0.00052392 0.0004631  0.00045861 0.000539   0.00047649 0.00043771
 0.00088843 0.00047158 0.00053376 0.0004067  0.00041591 0.00055387
 0.00052797 0.00056037 0.00047961 0.00048259 0.00042492 0.00071588
 0.000446   0.00041927 0.00045816 0.0008268  0.00054773 0.00054284
 0.00057137 0.0004619  0.00051865 0.00041787] [1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
TRAIN 2021-09-15T20:43:04.211167: step 6558, loss 1.67676e-07, acc 1
(1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1) [0.00049145 0.00062057 0.0004825  0.00043573 0.00054301 0.00052593
 0.00049798 0.00056848 0.00054202 0.00050205 0.00047748 0.00049263
 0.00050483 0.00075437 0.00048613 0.0004414  0.0005491  0.00066889
 0.00063032 0.00052558 0.00072708 0.00049604 0.00051932 0.00048036
 0.00047906 0.00048809 0.00070174 0.00044759 0.00051752 0.00113679
 0.00048045 0.00045944 0.00050589 0.00049568 0.00047283 0.00050124
 0.00045815 0.00058478 0.00062569 0.00048911 0.00052419 0.00052815
 0.00051044 0.00059683 0.00052092 0.00046898 0.00053534 0.0007372
 0.0006818  0.00063921 0.00064887 0.00062363 0.00101212 0.00055969
 0.00047876 0.00048444 0.00055878 0.0008085  0.00049886 0.00056041
 0.00061951 0.00060025 0.00067865 0.0005192 ] [1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
TRAIN 2021-09-15T20:43:04.243188: step 6559, loss 1.72278e-07, acc 1
(1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1) [0.00049148 0.00057423 0.00043417 0.0006967  0.00050643 0.00046657
 0.00043974 0.00055412 0.00054206 0.00042516 0.00045239 0.00106311
 0.00042485 0.00107465 0.00052645 0.00045527 0.00044861 0.0007013
 0.00052359 0.00047954 0.00048973 0.00048094 0.00055912 0.00049338
 0.00047097 0.00057534 0.00086696 0.00075234 0.00078004 0.00044411
 0.00123036 0.00052502 0.00046861 0.00043324 0.0008151  0.00048613
 0.00075791 0.00058069 0.00044432 0.00048145 0.0004449  0.00059619
 0.00047606 0.00044804 0.00079869 0.00047976 0.00062161 0.00047342
 0.00061542 0.00057792 0.00059646 0.00046125 0.00052386 0.00042936
 0.00055044 0.00046241 0.00046702 0.00072433 0.00046072 0.00046382
 0.00061338 0.00043443 0.00044343 0.00046455] [1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
TRAIN 2021-09-15T20:43:04.277116: step 6560, loss 1.34307e-07, acc 1
(1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1) [0.00049893 0.00054702 0.00041434 0.0005583  0.00041548 0.00055647
 0.00041752 0.00039115 0.00069056 0.00051018 0.00050029 0.0004127
 0.00041983 0.00069836 0.00042262 0.0004546  0.00064617 0.00048319
 0.00042125 0.00038625 0.00078884 0.00112098 0.00042642 0.00043826
 0.00044677 0.00043877 0.00044942 0.00043135 0.0005487  0.00049054
 0.00044882 0.00045643 0.00035084 0.00042276 0.0004565  0.00045952
 0.00037289 0.00053607 0.00041958 0.00043149 0.00066635 0.00046217
 0.00041007 0.00080464 0.00038748 0.00040799 0.00040651 0.00039697
 0.00044382 0.00056813 0.00039275 0.00060866 0.00076602 0.00096006
 0.00051577 0.00050519 0.00041016 0.0003673  0.00044682 0.00052095
 0.00036719 0.00050229 0.00040498 0.0003987 ] [1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
TRAIN 2021-09-15T20:43:04.309978: step 6561, loss 1.85199e-07, acc 1
...
...
Ctrl+C နဲ့ ရပ်ခဲ့....  
```

Training ကတော့ လုပ်သွားပြီ။   
သို့သော် အထက်မှာ တွေ့ရတဲ့အတိုင်းပဲ training data ထဲမှာက 1 တွေချည်းပဲ ရှိတော့ တနည်းအားဖြင့် y ဆိုတဲ့ label တွေချည်းပဲ ရှိလို့ အဆင်မပြေဘူး။   
phrase အနေနဲ့ run တဲ့အခါမှာ သူက validation set ဆိုပြီး auto ထုတ်တယ်။ အဲဒီမှာ 0, 1 ဒေတာကို ပြင်ထားတာတွေ့ရအောက်ပါအတိုင်း...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ wc validation.txt0.manual 
  4692  69654 865752 validation.txt0.manual
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ tail validation.txt0.manual 
0	သူ့ အပြစ် က ကြီး လွန်း လို့ ကြိုးမိန့်ပေး ခံ လိုက် ရ တာ	စိတ်ပျက် ဖို့ အရမ်း ကောင်း တယ်
0	သူမ ပြန်ရောက် ဖို့ အချိန် တန်ပြီ ။	မတူကွဲပြား မှု တွေ အမြဲတမ်း ရှိ နေ တယ် ။
0	အလုပ် ရ သွား တာ နဲ့ စိတ် ကြီး ဝင် နေ ပြီ ။	စိန် ဘယက် တစ် ခု ဝတ်ဆင် လာ ခဲ့ တယ် ။
1	ဆောင်း ရာသီ ဟာ အရမ်း အရောင်းအဝယ် ပါး လို့ ငါ တို့ တွေ ဆိုင် ကို ပိတ် ပြီး အားလပ်ရက် ခရီးထွက် ကြ တယ် ။	ဆောင်း ရာသီ ဟာ အရမ်း အရောင်းအဝယ် ပါး လို့ ငါ တို့ တွေ ဆိုင် ကို နား ပြီး အားလပ်ရက် ခရီးထွက် ကြ တယ် ။
0	မ တွေ့ ချင် တဲ့ လူ ကို ခပ်ခွာခွာ မ နေ ပါ ဘူး ။	လွဲ မှာ စိုးလို့ တိုက် ထား ရ တယ် ။
0	တော် လိုက် တာ အားပေး တယ် ဆက် လုပ်	တစ်သက်တစ်ကျွန်း ချ လိုက်
1	ဂုဏ်ယူ စရာ မြန်မာ ဟေ့	ဂုဏ်ယူ စရာ ဒို့ မြန်မာ ပါ ကွာ
0	ဂရု တောင် မ စိုက် ဘူး	ပြော စရာ က တော့ တစ် ခု ပဲ ရှိ တော့ တယ်
0	ရှေးဘုရင် များ တွင် ကိုယ်လုပ် များ ရှိ ကြ သည် ။	ဒီ ကောင်မလေး က လူနုံ ရယ် သေချာ ခေါ် သွား ဦး ။
0	အလံ ကို လွှင့်တင် ချင် သောအခါ ၎င်း ကို ဘယ် မှာ စည်းနှောင် ရ မလဲ ။	ချီးကျူး ဂုဏ်ပြု ပါ တယ်
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ 
```

**To Do

အဲဒါကြောင့် အောက်ပါ အချက်တွေကို ငါ ပြင်ဆင်ရမယ်...  
- 0,1 label နှစ်ခုလုံးပါတဲ့ training ဒေတာကို ပြင်ရမယ် (ရှိပြီးသား... နဂို original ကို ယူလိုက်ယုံပါပဲ)  
- အခု အချိန်ထိ phrase နဲ့ ငါစမ်းခဲ့တာက တကယ်က y သို့မဟုတ် 1 နဲ့ပဲ စမ်းခဲ့တာ မို့ word2vec, fasttext တွေကိုလည်း ဖယ်ထားတဲ့ စာကြောင်းတွေပါ ပြန်ထည့်ပြီး ဆောက်ရန်
- sentence ကိုပဲ experiment setting ထားပြီး သွားမယ်ဆိုရင်၊ character, syllable, word အားလုံးကိုလည်း word2vec နဲ့ experiment လုပ်ရန်
- ပြီးရင် fasttext နဲ့လည်း လုပ်ပြီး ရလဒ်ကို ကြည့်ရန်...  
- Word Embedding ကိုလည်း myPara Corpus တစ်ခုတည်း သုံးတာနဲ့ myPara Corpus + myWord Corpus နှစ်မျိုးရောပြီး သုံးတာကိုလည်း စမ်းကြည့်လို့ ရနိုင်တယ်

-------------

**ပြောရရင်တော့ တကယ် စာတမ်းမှာ သုံးလို့ ရမယ့် Experiment က ဒီကနေ စတာပါ...**


## Preprocessing


wor2vec နဲ့ fasttext တွေကို သိမ်ထားမယ့် folder path:
/home/ye/exp/myPara2/deep-siamese-text-similarity/w2v_fasttext

Prepare Training Data (containing both 0 and 1):

Original CSV ဖိုင်ကို final-prepare ဆိုတဲ့ folder အသစ်အောက်မှာ ကော်ပီကူးသိမ်းပြီး အဲဒီအောက်မှာ training data ကို Deep Siamese ရဲ့ format နဲ့ ကိုက်အောင်ပြင်တဲ့ အလုပ်ကို လုပ်သွားမယ်။   

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/preprocess/final-prepare$ wc train.csv 
  40462  591517 9056946 train.csv
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/preprocess/final-prepare$ head train.csv 
id,senid1,senid2,sentence1,sentence2,is_duplicate
0,1,2,ကျွန်တော် စီး ဖို့ ချစ်စရာ ဖိနပ် တစ် ရံ ကို ရှာ မတွေ့လို့ပါ ။,တစ်ခါတစ်ခါ ကျွန်တော်က ခင်ဗျား ကို အရမ်း အပြောင်းအလဲများတဲ့လူ လို့ ထင်မိတယ် ။,0
1,3,4,​ ကျေးဇူး ပဲ ၊ ကျွန်တော် ဘယ်လောက် ပေး ရ မလဲ ။,ကျေးဇူး နော် ၊ ဘယ်တော့ ပြန် တွေ့ ကြ မလဲ ။,0
2,5,6,​ ကျေးဇူး အများကြီး တင် ပါ တယ် ။,ကျေးဇူးတင် တယ် လို့ မ ပြော သွား ဘူး ။,0
3,7,8,​ ကျောင်းအုပ်ကြီး က တော် တဲ့ ကျောင်းသား တွေ ကို ချီးကျူး ကြ တယ် ။,ကျောင်းအုပ်ကြီး က ဆိုး တဲ့ ကျောင်းသား တွေ ကို ဒဏ်ပေး ကြ တယ် ။,0
4,9,10,​ ကောင်း ပြီ ကျွန်တော် လုပ် ပါ့ မယ် ။,ကောင်း ပြီ ကျွန်တော် ဒီ အလုပ် ကို လက်မခံ တော့ ဘူး ။,0
5,11,12,​ ကောင်း သော ည ပါ ။,ကောင်း သော နေ့ ပါ ။,0
6,13,14, ကောင်လေး က လူကြီး ကို ရှင်းရှင်းလင်းလင်း မြင် နေ တယ် ။,သာယာတဲ့ နေ့ကလေး ပါပဲ ။,0
7,15,16, ခဏအကြာမှာ ကျွန်တော် ခင်ဗျား ကို  ပြန်ဆက် ပါရစေ ။,ခဏ ကြာတော့ သူမ တည်ငြိမ် စပြုလာ ပြီး သူ ပြောတာကို နားထောင် နေတော့တယ် ။,0
8,17,18, ခေါင်မိုး ပေါ်မှာ ကြောင် တစ်ကောင် ရှိ တယ် ။,အတန်း လွတ်သွားမှာ စိုးတယ် ။,0
```

Column နံပါတ် ၄ ၅ ၆ ကို ပဲ ဖြတ်ထုတ်ယူ...   

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/preprocess/final-prepare$ cut -d"," -f4,5,6 ./train.csv > train.csv.col456
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/preprocess/final-prepare$ head ./train.csv.col456 
sentence1,sentence2,is_duplicate
ကျွန်တော် စီး ဖို့ ချစ်စရာ ဖိနပ် တစ် ရံ ကို ရှာ မတွေ့လို့ပါ ။,တစ်ခါတစ်ခါ ကျွန်တော်က ခင်ဗျား ကို အရမ်း အပြောင်းအလဲများတဲ့လူ လို့ ထင်မိတယ် ။,0
 ကျေးဇူး ပဲ ၊ ကျွန်တော် ဘယ်လောက် ပေး ရ မလဲ ။,ကျေးဇူး နော် ၊ ဘယ်တော့ ပြန် တွေ့ ကြ မလဲ ။,0
 ကျေးဇူး အများကြီး တင် ပါ တယ် ။,ကျေးဇူးတင် တယ် လို့ မ ပြော သွား ဘူး ။,0
 ကျောင်းအုပ်ကြီး က တော် တဲ့ ကျောင်းသား တွေ ကို ချီးကျူး ကြ တယ် ။,ကျောင်းအုပ်ကြီး က ဆိုး တဲ့ ကျောင်းသား တွေ ကို ဒဏ်ပေး ကြ တယ် ။,0
 ကောင်း ပြီ ကျွန်တော် လုပ် ပါ့ မယ် ။,ကောင်း ပြီ ကျွန်တော် ဒီ အလုပ် ကို လက်မခံ တော့ ဘူး ။,0
 ကောင်း သော ည ပါ ။,ကောင်း သော နေ့ ပါ ။,0
 ကောင်လေး က လူကြီး ကို ရှင်းရှင်းလင်းလင်း မြင် နေ တယ် ။,သာယာတဲ့ နေ့ကလေး ပါပဲ ။,0
 ခဏအကြာမှာ ကျွန်တော် ခင်ဗျား ကို  ပြန်ဆက် ပါရစေ ။,ခဏ ကြာတော့ သူမ တည်ငြိမ် စပြုလာ ပြီး သူ ပြောတာကို နားထောင် နေတော့တယ် ။,0
 ခေါင်မိုး ပေါ်မှာ ကြောင် တစ်ကောင် ရှိ တယ် ။,အတန်း လွတ်သွားမှာ စိုးတယ် ။,0
```

CSV ကနေ TAB delimiter အဖြစ် အောက်ပါအတိုင်း ပြောင်းခဲ့။ sed နဲ့ အစားထိုးတာထက် အခုလို field တစ်ခုချင်းစီ ဖြတ်ထုတ်ပြီးမှ paste နဲ့ ပေါင်းတာက ပို အန္တရာယ်ကင်းလို့....   

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/preprocess/final-prepare$ cut -d"," -f 1 ./train.csv.col456 > f1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/preprocess/final-prepare$ cut -d"," -f 2 ./train.csv.col456 > f2
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/preprocess/final-prepare$ cut -d"," -f 3 ./train.csv.col456 > f3
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/preprocess/final-prepare$ paste f1 f2 f3 > train.txt
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/preprocess/final-prepare$ rm f1 f2 f3
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/preprocess/final-prepare$ head ./train.txt
sentence1	sentence2	is_duplicate
ကျွန်တော် စီး ဖို့ ချစ်စရာ ဖိနပ် တစ် ရံ ကို ရှာ မတွေ့လို့ပါ ။	တစ်ခါတစ်ခါ ကျွန်တော်က ခင်ဗျား ကို အရမ်း အပြောင်းအလဲများတဲ့လူ လို့ ထင်မိတယ် ။	0
 ကျေးဇူး ပဲ ၊ ကျွန်တော် ဘယ်လောက် ပေး ရ မလဲ ။	ကျေးဇူး နော် ၊ ဘယ်တော့ ပြန် တွေ့ ကြ မလဲ ။	0
 ကျေးဇူး အများကြီး တင် ပါ တယ် ။	ကျေးဇူးတင် တယ် လို့ မ ပြော သွား ဘူး ။	0
 ကျောင်းအုပ်ကြီး က တော် တဲ့ ကျောင်းသား တွေ ကို ချီးကျူး ကြ တယ် ။	ကျောင်းအုပ်ကြီး က ဆိုး တဲ့ ကျောင်းသား တွေ ကို ဒဏ်ပေး ကြ တယ် ။	0
 ကောင်း ပြီ ကျွန်တော် လုပ် ပါ့ မယ် ။	ကောင်း ပြီ ကျွန်တော် ဒီ အလုပ် ကို လက်မခံ တော့ ဘူး ။	0
 ကောင်း သော ည ပါ ။	ကောင်း သော နေ့ ပါ ။	0
 ကောင်လေး က လူကြီး ကို ရှင်းရှင်းလင်းလင်း မြင် နေ တယ် ။	သာယာတဲ့ နေ့ကလေး ပါပဲ ။	0
 ခဏအကြာမှာ ကျွန်တော် ခင်ဗျား ကို  ပြန်ဆက် ပါရစေ ။	ခဏ ကြာတော့ သူမ တည်ငြိမ် စပြုလာ ပြီး သူ ပြောတာကို နားထောင် နေတော့တယ် ။	0
 ခေါင်မိုး ပေါ်မှာ ကြောင် တစ်ကောင် ရှိ တယ် ။	အတန်း လွတ်သွားမှာ စိုးတယ် ။	0
```

check file:  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/preprocess/final-prepare$ wc train.txt
  40462  672373 8350847 train.txt
```

copy to experiment folder:  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/my-para/preprocess/final-prepare$ cp ./train.txt ../../../
```

Final manual word segmented data:  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/w2v_fasttext/mypara-manual$ wc *
   1000   16905  202235 closed-test
   1000   12674  138604 open-test.final.manual
  40461  672370 8350814 train.txt
  42461  701949 8691653 total
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/w2v_fasttext/mypara-manual$ head -n 3 *
==> closed-test <==
1	ကောင်း လိုက် တဲ့ သတင်း လေး ပါ	ကောင်း သော သတင်း ပါ ပဲ
0	ခု ဒီ တံဆိပ် က ဈေးလိုက် နေ တယ် ။	ဒီ တံဆိပ် က ဈေး အရမ်း တက် နေ တယ် ။
1	ကျွန်မ ဘက် က စ ပြီး ကျေအေး ပေး တယ် နော်	ကျွန်မ ဘက် က စ ပြီး ကျေလည် တာ နော်

==> open-test.final.manual <==
0	၁၁ ဒေါ်လာ ကျ ပါ တယ် ။	၁၁ နာရီ လာ ခေါ် မယ် ။
0	၁၁ နာရီ ခွဲ အိမ် ပြန် မယ် ။	၁၁ နာရီ ခွဲ အရောက် လာ ပါ ။
0	၁၁:၃၀ ပြန်ရောက် မယ် လို့ ထင် သလား ။	၁၁:၃၀ အတိ မှာ ပြန်ရောက် လာ ခဲ့ တယ် ။

==> train.txt <==
ကျွန်တော် စီး ဖို့ ချစ်စရာ ဖိနပ် တစ် ရံ ကို ရှာ မတွေ့လို့ပါ ။	တစ်ခါတစ်ခါ ကျွန်တော်က ခင်ဗျား ကို အရမ်း အပြောင်းအလဲများတဲ့လူ လို့ ထင်မိတယ် ။	0
 ကျေးဇူး ပဲ ၊ ကျွန်တော် ဘယ်လောက် ပေး ရ မလဲ ။	ကျေးဇူး နော် ၊ ဘယ်တော့ ပြန် တွေ့ ကြ မလဲ ။	0
 ကျေးဇူး အများကြီး တင် ပါ တယ် ။	ကျေးဇူးတင် တယ် လို့ မ ပြော သွား ဘူး ။	0

```

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/w2v_fasttext/mypara-manual$ cut -f 1 ./train.txt > train.f1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/w2v_fasttext/mypara-manual$ cut -f 2 ./train.txt > train.f2
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/w2v_fasttext/mypara-manual$ cut -f 2 ./closed-test > closed-test.f2
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/w2v_fasttext/mypara-manual$ cut -f 3 ./closed-test > closed-test.f3
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/w2v_fasttext/mypara-manual$ cut -f 2 ./open-test.final.manual > open-test.f2
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/w2v_fasttext/mypara-manual$ cut -f 3 ./open-test.final.manual > open-test.f3
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/w2v_fasttext/mypara-manual$ cat ./train.f1 ./train.f2 ./closed-test.f2 ./closed-test.f3 ./open-test.f2 ./open-test.f3 > mypara-all.manual
```

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/w2v_fasttext/mypara-manual$ wc *
    1000    16905   202235 closed-test
   84922   659489  8606732 mypara-all.manual
    1000    12674   138604 open-test.final.manual
   40461   672370  8350814 train.txt
  127383  1361438 17298385 total
```

**syllable အတွက် စပြင်ခဲ့...**  

syllable segmentation ကို အောက်ပါအတိုင်း လုပ်ခဲ့...  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main$ python ./myword.py syllable ./my-para/syl-my2/closed-test ./my-para/syl-my2/closed-test.syl1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main$ python ./myword.py syllable ./my-para/syl-my2/mypara-all.manual ./my-para/syl-my2/mypara-all.manual.syl1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main$ python ./myword.py syllable ./my-para/syl-my2/open-test.final.manual ./my-para/syl-my2/open-test.final.manual.syl1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main$ python ./myword.py syllable ./my-para/syl-my2/train.txt ./my-para/syl-my2/train.txt.syl1
```

Column ခွဲထားတဲ့ ဖိုင်တွေကို syllable ဝင်ဖြတ်ရတာဖြစ်လို့ \<Space\>\<TAB\>\<Space\> ဆိုပြီး space ပိုတာမျိုးတွေရှိလို့အောက်ပါအတိုင်း space cleaning လုပ်ခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/syl-my2$ bash ./space-tab-space-to-tab.sh ./closed-test.syl1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/syl-my2$ perl ./clean-space.pl ./closed-test.syl1 > closed-test.syl
```

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/syl-my2$ perl ./clean-space.pl ./mypara-all.manual.syl1 > ./mypara-all.manual.syl 
```

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/syl-my2$ bash ./space-tab-space-to-tab.sh ./open-test.final.manual.syl1 
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/syl-my2$ perl ./clean-space.pl ./open-test.final.manual.syl1 > ./open-test.final.manual.syl
```

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/syl-my2$ bash ./space-tab-space-to-tab.sh ./train.txt.syl1 
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/syl-my2$ perl ./clean-space.pl ./train.txt.syl1 > ./train.txt.syl
```

syl1 တွေက dummy file တွေမို့ အဲဒါတွေကို နောက်ပိုင်းမှာ မရှုပ်အောင် ဖျက်ခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/syl-my2$ rm *.syl1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/syl-my2$ wc *.syl
    1000    22293   207626 closed-test.syl
   84921   928148  8874942 mypara-all.manual.syl
    1000    16435   142309 open-test.final.manual.syl
   40461   931880  8610117 train.txt.syl
  127382  1898756 17834994 total
```

ခုထဲက manual word အတွက်နဲ့ syllable ဒေတာပြင်ဆင်တာ ပြီးသွားပြီ...  

**word segmentation with myWord ကို စလုပ်မယ်...**

အရင်ဆုံး manual word segmentation လုပ်ထားတဲ့ ဖိုင်တွေကို ကော်ပီကူးမယ်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para$ cp ./manual-my2/* ./word-my2/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para$ cd word-my2
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ ls
closed-test  mypara-all.manual  open-test.final.manual  train.txt
```

word-my2/ အောက်ထဲမှာ word-segmentation လုပ်မယ်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ cd ../..
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main$ python ./myword.py word ./my-para/word-my2/closed-test ./my-para/word-my2/closed-test.word1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main$ python ./myword.py word ./my-para/word-my2/mypara-all.manual ./my-para/word-my2/mypara-all.manual.word1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main$ python ./myword.py word ./my-para/word-my2/open-test.final.manual ./my-para/word-my2/open-test.final.manual.word1

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main$ time python ./myword.py word ./my-para/word-my2/train.txt ./my-para/word-my2/train.txt.word1

real	22m52.376s
user	22m49.658s
sys	0m0.596s
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main$
```

space cleaning...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ bash ./space-tab-space-to-tab.sh ./closed-test.word1 
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ bash ./space-tab-space-to-tab.sh ./train.txt.word1 
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ bash ./space-tab-space-to-tab.sh ./open-test.final.manual.word1 
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$
```

နောက်ထပ် ပရိုဂရမ် တပုဒ်နဲ့ စာကြောင်းအစ၊ စာကြောင်းအဆုံးနဲ့ စာလုံး တစ်လုံးနဲ့ တစ်လုံးကြားမှာ မလိုတဲ့ <space> အပိုတွေကို ရှင်းထုတ်ခဲ့...  
  
```
 (base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ perl ./clean-space.pl ./closed-test.word1 > ./closed-test.word
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ perl ./clean-space.pl ./mypara-all.manual.word1 > ./mypara-all.manual.word
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ perl ./clean-space.pl ./open-test.final.manual.word1 > ./open-test.final.manual.word
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ perl ./clean-space.pl ./train.txt.word1 > ./train.txt.word
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ 
```

cleaning လုပ်စဉ်မှာ ခဏသုံးခဲ့တဲ့ dummy file တွေဖြစ်တဲ့ ".word1" ဖိုင်တွေကို ဖျက်ခဲ့...  
  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ rm *.word1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ wc *.word
    1000    18272   203625 closed-test.word
   84921   753196  8699990 mypara-all.manual.word
    1000    13766   139640 open-test.final.manual.word
   40461   764288  8442342 train.txt.word
  127382  1549522 17485597 total
```
  
ဖိုင်ထဲက content တွေကို မျက်လုံးနဲ့ confirm လုပ်ခဲ့...  
  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ head -n 3 *.word
==> closed-test.word <==
1	ကောင်း လိုက် တဲ့ သတင်း လေး ပါ	ကောင်း သော သတင်း ပါ ပဲ
0	ခု ဒီ တံဆိပ် က ဈေး လိုက် နေ တယ် ။	ဒီ တံဆိပ် က ဈေး အရမ်း တက် နေ တယ် ။
1	ကျွန်မ ဘက် က စ ပြီး ကျေအေး ပေး တယ် နော်	ကျွန်မ ဘက် က စ ပြီး ကျေလည် တာ နော်

==> mypara-all.manual.word <==
ကျွန်တော် စီး ဖို့ ချစ် စရာ ဖိနပ် တစ် ရံ ကို ရှာ မ တွေ့ လို့ ပါ ။
ကျေးဇူး ပဲ ၊ ကျွန်တော် ဘယ်လောက် ပေး ရ မ လဲ ။
ကျေးဇူး အများကြီး တင် ပါ တယ် ။

==> open-test.final.manual.word <==
0	၁၁ ဒေါ်လာ ကျ ပါ တယ် ။	၁၁ နာရီ လာ ခေါ် မယ် ။
0	၁၁ နာရီ ခွဲ အိမ် ပြန် မယ် ။	၁၁ နာရီ ခွဲ အရောက် လာ ပါ ။
0	၁၁:၃၀ ပြန် ရောက် မယ် လို့ ထင် သလား ။	၁၁:၃၀ အတိ မှာ ပြန် ရောက် လာ ခဲ့ တယ် ။

==> train.txt.word <==
ကျွန်တော် စီး ဖို့ ချစ် စရာ ဖိနပ် တစ် ရံ ကို ရှာ မ တွေ့ လို့ ပါ ။	တစ်ခါတစ်ခါ ကျွန်တော် က ခင်ဗျား ကို အရမ်း အပြောင်းအလဲ များ တဲ့ လူ လို့ ထင် မိ တယ် ။	0
ကျေးဇူး ပဲ ၊ ကျွန်တော် ဘယ်လောက် ပေး ရ မ လဲ ။	ကျေးဇူး နော် ၊ ဘယ် တော့ ပြန် တွေ့ ကြ မ လဲ ။	0
ကျေးဇူး အများကြီး တင် ပါ တယ် ။	ကျေးဇူးတင် တယ် လို့ မ ပြော သွား ဘူး ။	0
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$
```
                              
သတိရတာနဲ့ manual ဖြတ်ထားတဲ့ original corpus ကိုလည်း အောက်ပါအတိုင်း space cleaning လုပ်ခဲ့...  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ ls
clean-space.pl  closed-test  mypara-all.manual  open-test.final.manual  train.txt
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ perl ./clean-space.pl ./mypara-all.manual > ./mypara-all.manual.1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ rm ./mypara-all.manual
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ mv ./mypara-all.manual.1 ./mypara-all.manual
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ perl ./clean-space.pl ./closed-test > closed-test.1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ diff ./closed-test ./closed-test.1 | wc
      0       0       0
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ rm ./closed-test.1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ perl ./clean-space.pl ./train.txt > ./train.txt.1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ wc train.txt train.txt.1 | wc
      3      12     109
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ rm ./train.txt
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ mv train.txt.1 train.txt
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ perl ./clean-space.pl ./open-test.final.manual > ./open-test.final.manual.1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ diff ./open-test.final.manual ./open-test.final.manual.1 | wc
     92     548    6377
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ rm ./open-test.final.manual
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ mv ./open-test.final.manual.1 ./open-test.final.manual
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$                           
```

diff နဲ့ စစ်ကြည့်လို့ wc count က > 0 ဆိုရင် သေချာတယ် ပိုရိုက်ထားတဲ့ space တွေရှိနေခဲ့လို့...  
  
## Preparing word2vec and fasttext

word2vec နဲ့ fasttext ကို ပြောင်းဖို့အတွက်က မြန်မာစာ paraphrase corpus တစ်ခုလုံးကို စုထားတဲ့ (ဆိုလိုတာ့ 0,1, y,n စတဲ့ label မပါတဲ့) ဖိုင်တစ်ဖိုင်တည်းကို ပြောင်းရင် ရပြီ။   
for manual word Unit:  

ပြင်ထားတဲ့ paraphrase မြန်မာစာကြောင်းအားလုံးပါတဲ့ စုထားတဲ့ ဖိုင်တွေကို word2vec, fasttext ပြောင်းဖို့အလုပ်လုပ်မယ့် ပရိုဂရမ်ရှိတဲ့ဆီကို ကော်ပီကူးခဲ့တယ်...  
  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ cp ./mypara-all.manual /home/ye/4github/syl-ngram/ref/playing_with_fasttext/mypara-manual/
  
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/syl-my2$ cp mypara-all.manual.syl /home/ye/4github/syl-ngram/ref/playing_with_fasttext/mypara-syl/
  
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ cp ./mypara-all.manual.word /home/ye/4github/syl-ngram/ref/playing_with_fasttext/mypara-word/

```
                              
ကော်ပီကူးပြီးသွားတဲ့အခါမှာ အမှားအယွင်းမရှိအောင် ဖိုင်တွေကို စစ်ကြည့်ခဲ့...  
  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ tree ./mypara-{manual,syl,word}
./mypara-manual
└── mypara-all.manual
./mypara-syl
└── mypara-all.manual.syl
./mypara-word
└── mypara-all.manual.word

0 directories, 3 files
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ wc ./mypara-{manual,syl,word}/*
   84921   659489  8606282 ./mypara-manual/mypara-all.manual
   84921   928148  8874942 ./mypara-syl/mypara-all.manual.syl
   84921   753196  8699990 ./mypara-word/mypara-all.manual.word
  254763  2340833 26181214 total
```
  
syl, manual-word, word ဖြတ်ထားတဲ့ ဖိုင်တွေအကြား word-count ကွာတာကို လေ့လာခဲ့...  

### wor2vec, fasttext creation for "manual-word"
  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ python ./Sherlock_Holmes_fasttext.py ./mypara-manual/mypara-all.manual 
[nltk_data] Downloading package punkt to /home/ye/nltk_data...
[nltk_data]   Package punkt is already up-to-date!
[nltk_data] Downloading package vader_lexicon to /home/ye/nltk_data...
[nltk_data]   Package vader_lexicon is already up-to-date!
[nltk_data] Downloading package stopwords to /home/ye/nltk_data...
[nltk_data]   Package stopwords is already up-to-date!
[nltk_data] Downloading package wordnet to /home/ye/nltk_data...
[nltk_data]   Package wordnet is already up-to-date!
Read 0M words
Number of words:  5589
Number of labels: 0
Progress: 100.0% words/sec/thread:  117601 lr:  0.000000 avg.loss:  2.214699 ETA:   0h 0m 0s
print(w2v_model.wv.most_similar('ကျောင်း', topn = 20)):
[('လမ်း', 0.9358484148979187), ('ပြေး', 0.9177197217941284), ('၉', 0.9083137512207031), ('သစ်ပင်', 0.9031364917755127), ('ပိုင်း', 0.8975261449813843), ('ကဗျာစာပေ', 0.8899070024490356), ('ရထား', 0.8897032737731934), ('ဦးဘ', 0.8862273097038269), ('၆', 0.8817196488380432), ('နေမင်း', 0.8805981278419495), ('အောက်', 0.880402684211731), ('လေဆိပ်', 0.879432201385498), ('မြို့', 0.8792335987091064), ('စသည်', 0.8785279393196106), ('တော', 0.8784735202789307), ('မနက်', 0.8765276670455933), ('ထောင်', 0.8763911128044128), ('၈', 0.8751877546310425), ('အလည်', 0.8742582201957703), ('စတိုး', 0.8731852769851685)] 

print(ft_model.get_nearest_neighbors('ကျောင်း', k = 20))
[(0.9173595309257507, 'ချောင်း'), (0.9170924425125122, 'ကျောင်းထွက်'), (0.914071798324585, 'ရွာဦးကျောင်း'), (0.9108685255050659, 'ကျောင်းဆရာ'), (0.9106876850128174, 'ယာဉ်မောင်း'), (0.9096049070358276, 'ကားမောင်း'), (0.9030694961547852, 'လည်ချောင်း'), (0.8952051997184753, 'ကြာညောင်း'), (0.8913081288337708, 'မောင်း'), (0.8908674716949463, 'ကျောင်းသူ'), (0.8906762003898621, 'ကျောင်းတက်'), (0.890514612197876, 'ဟောင်း'), (0.8890510201454163, 'ရောင်း'), (0.8887304067611694, 'ဘောင်းဘီ'), (0.8873381018638611, 'ညောင်း'), (0.8857645988464355, 'အုန်းမောင်း'), (0.8834129571914673, 'ကျောင်းအပ်'), (0.8831270933151245, 'ရေလောင်း'), (0.8785563111305237, 'ဖောင်း'), (0.8780372738838196, 'ရောင်ဆင်း')] 

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$
```

fasttext binary ဖိုင် ကနေ text vector ဖိုင်အဖြစ် အောက်ပါအတိုင်း convert လုပ်ခဲ့...  
  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ python ./fasttext_bin-to-vec.py ./all-para.fasttext.bin all-para.fasttext.vector
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
```
  
output ထွက်လာတဲ့ word2vec နဲ့ fasttext ဖိုင်တွေက python ပရိုဂရမ် run တဲ့ folder အောက်မှာပဲ ရှိလို့ ...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ ll -h ./all-para.word2vec 
-rw-rw-r-- 1 ye ye 158M စက်   16 11:00 ./all-para.word2vec
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ ll -h ./all-para.fasttext.bin 
-rw-rw-r-- 1 ye ye 3.8G စက်   16 11:00 ./all-para.fasttext.bin
  
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ ll -h ./all-para.fasttext.vector 
-rw-rw-r-- 1 ye ye 32M စက်   16 11:03 ./all-para.fasttext.vector

```
 
move လုပ်ခဲ့ ...   

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ mv ./all-para.{word2vec,fasttext.bin,fasttext.vector} ./mypara-manual/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ ls ./mypara-manual/
all-para.fasttext.bin  all-para.fasttext.vector  all-para.word2vec  mypara-all.manual
```

wc count လုပ်ပြီး စာလုံးအရေအတွက်ကို confirmation လုပ်ခဲ့....   
  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ wc ./mypara-manual/*
   7430223   43125790 4022529962 ./mypara-manual/all-para.fasttext.bin
      5590    2800091   33139857 ./mypara-manual/all-para.fasttext.vector
     25465   12757465  165233108 ./mypara-manual/all-para.word2vec
     84921     659489    8606282 ./mypara-manual/mypara-all.manual
   7546199   59342835 4229509209 total
```

### wor2vec, fasttext creation for "syllable"
  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ python ./Sherlock_Holmes_fasttext.py ./mypara-syl/mypara-all.manual.syl 
[nltk_data] Downloading package punkt to /home/ye/nltk_data...
[nltk_data]   Package punkt is already up-to-date!
[nltk_data] Downloading package vader_lexicon to /home/ye/nltk_data...
[nltk_data]   Package vader_lexicon is already up-to-date!
[nltk_data] Downloading package stopwords to /home/ye/nltk_data...
[nltk_data]   Package stopwords is already up-to-date!
[nltk_data] Downloading package wordnet to /home/ye/nltk_data...
[nltk_data]   Package wordnet is already up-to-date!
Read 1M words
Number of words:  1698
Number of labels: 0
Progress: 100.0% words/sec/thread:  171847 lr:  0.000000 avg.loss:  2.285939 ETA:   0h 0m 0s
print(w2v_model.wv.most_similar('ကျောင်း', topn = 20)):
[('ပဉ္စ', 0.5370543599128723), ('ဘုန်း', 0.5247331857681274), ('မြို့', 0.5121671557426453), ('ကြွ', 0.5113822817802429), ('စု', 0.4787759780883789), ('တန်း', 0.47199782729148865), ('ပွား', 0.44916942715644836), ('လိမ္မာ', 0.41200706362724304), ('မှူး', 0.41169601678848267), ('အုပ်', 0.4100281894207001), ('သား', 0.4082058370113373), ('ဂန်', 0.4068843722343445), ('စုန်း', 0.39872241020202637), ('ဇင်း', 0.39803269505500793), ('ဖွား', 0.3973041772842407), ('မန်း', 0.39071279764175415), ('နွား', 0.38369205594062805), ('မဂ္ဂ', 0.38261133432388306), ('ရွာ', 0.37912026047706604), ('ရိုး', 0.3771994709968567)] 

print(ft_model.get_nearest_neighbors('ကျောင်း', k = 20))
[(0.7989024519920349, 'လျောင်း'), (0.7456591129302979, 'ပျောင်း'), (0.7406554222106934, 'ဖျောင်း'), (0.7350637316703796, 'ချောင်း'), (0.7133853435516357, 'သောင်း'), (0.6981094479560852, 'ကျော'), (0.6794184446334839, 'ကျော့'), (0.6780442595481873, 'ဘောင်း'), (0.6744620203971863, 'မောင်း'), (0.6675193309783936, 'ညောင်း'), (0.6367529034614563, 'ဟောင်း'), (0.6356250643730164, 'ထောင်း'), (0.6198782920837402, 'ဖောင်း'), (0.6182639598846436, 'ယောင်း'), (0.6182332634925842, 'အောင်း'), (0.6042153239250183, 'ကျော်'), (0.5988919138908386, 'စောင်း'), (0.5975959300994873, '/'), (0.5973014235496521, 'လောင်း'), (0.5396040678024292, 'နောင်း')] 

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$
```
  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ python ./fasttext_bin-to-vec.py ./all-para.fasttext.bin all-para.fasttext.vector
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
```

mv လုပ်ခဲ့...  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ mv ./all-para.{word2vec,fasttext.bin,fasttext.vector} ./mypara-syl/
```
  
wc နဲ့ count လုပ်ကြည့်ခဲ့...  
  
```
  (base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ wc ./mypara-syl/*
   7313171   42466874 4006828598 ./mypara-syl/all-para.fasttext.bin
      1699     850700   10071849 ./mypara-syl/all-para.fasttext.vector
      2265    1134265   13722059 ./mypara-syl/all-para.word2vec
     84921     928148    8874942 ./mypara-syl/mypara-all.manual.syl
   7402056   45379987 4039497448 total
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$
```
  
### wor2vec, fasttext creation for "word segmented with myWord"
  
word2vec နဲ့ fastext bin ဖိုင် အရင်ထုတ်...  
  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ python ./Sherlock_Holmes_fasttext.py ./mypara-word/mypara-all.manual.word
[nltk_data] Downloading package punkt to /home/ye/nltk_data...
[nltk_data]   Package punkt is already up-to-date!
[nltk_data] Downloading package vader_lexicon to /home/ye/nltk_data...
[nltk_data]   Package vader_lexicon is already up-to-date!
[nltk_data] Downloading package stopwords to /home/ye/nltk_data...
[nltk_data]   Package stopwords is already up-to-date!
[nltk_data] Downloading package wordnet to /home/ye/nltk_data...
[nltk_data]   Package wordnet is already up-to-date!
Read 0M words
Number of words:  3892
Number of labels: 0
Progress: 100.0% words/sec/thread:  145675 lr:  0.000000 avg.loss:  2.283026 ETA:   0h 0m 0s
print(w2v_model.wv.most_similar('ကျောင်း', topn = 20)):
[('ပြေး', 0.7961063981056213), ('ခွဲ', 0.7723153829574585), ('၉', 0.7554347515106201), ('အိုးစည်', 0.7439748644828796), ('အိမ်', 0.7432504892349243), ('မနက်', 0.73084557056427), ('သစ်ပင်', 0.7282942533493042), ('ချင်း', 0.7281666994094849), ('ခြောက်', 0.7259509563446045), ('ရွာ', 0.7217157483100891), ('မိုး', 0.7168434858322144), ('ကိုး', 0.7160293459892273), ('ခရီး', 0.7147096395492554), ('တက်', 0.7122154831886292), ('အတွင်း', 0.7082696557044983), ('ဆောက်', 0.7070903182029724), ('6', 0.7063080668449402), ('လမ်း', 0.7039904594421387), ('ဒယီးဒယိုင်', 0.7018947005271912), ('ရှစ်', 0.6975663304328918)] 

print(ft_model.get_nearest_neighbors('ကျောင်း', k = 20))
[(0.9004136323928833, 'လဲလျောင်း'), (0.8921953439712524, 'ဟောင်း'), (0.8709333539009094, 'မောင်း'), (0.8656821250915527, 'ညောင်း'), (0.8641787767410278, 'ယာဉ်မောင်း'), (0.856418788433075, 'လည်ချောင်း'), (0.8552566170692444, 'ချောင်း'), (0.8549490571022034, 'အဟောင်း'), (0.850272536277771, 'ဇနီးလောင်း'), (0.849738359451294, 'ကြာညောင်း'), (0.8468860387802124, 'ကျောင်းအုပ်ကြီး'), (0.8459020256996155, 'ဖောင်း'), (0.8434823751449585, 'ပျော့ပျောင်း'), (0.8413714170455933, 'လောင်း'), (0.8298735618591309, 'ဖြားယောင်း'), (0.8275929689407349, 'ကြိမ်းမောင်း'), (0.8272570371627808, 'ကျောင်းသား'), (0.8240382075309753, 'ဘောင်းဘီတို'), (0.8207239508628845, 'ငရုတ်ကောင်း'), (0.8204129338264465, 'ပြတ်တောင်းတောင်း')] 

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$  
```
  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ python ./fasttext_bin-to-vec.py ./all-para.fasttext.bin all-para.fasttext.vector
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ 
```
  
ပြီးသွားတဲ့ word2vec, fasttext ဖိုင်တွေကို 
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ mv ./all-para.{word2vec,fasttext.bin,fasttext.vector} ./mypara-word/
```
  
wc နဲ့ စာလုံးတွေကို ရေတွက်ကြည့်ခဲ့...  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ wc ./mypara-word/*
   7389827   42894550 4015683697 ./mypara-word/all-para.fasttext.bin
      3893    1949894   23149133 ./mypara-word/all-para.fasttext.vector
      8493    4254493   53833877 ./mypara-word/all-para.word2vec
     84921     753196    8699990 ./mypara-word/mypara-all.manual.word
   7487134   49852133 4101366697 total
```
  
## Training with Manual Word Unit, 200 Epoch 

အထက်မှာ ပြင်ဆင်ထားခဲ့တဲ့ training, closed test, open test ဒေတာတွေက အောက်ပါအတိုင်းရှိ...  
(syllable မဖြတ်ခင်၊ word မဖြတ်ခင်က original manual-word ဖိုင်တွေကိုလည်း ရှင်းပြီးသား အခြေအနေ...)  
  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para$ tree ./{manual,syl,word}-my2/
./manual-my2/
├── clean-space.pl
├── closed-test
├── mypara-all.manual
├── open-test.final.manual
└── train.txt
./syl-my2/
├── clean-space.pl
├── closed-test.syl
├── mypara-all.manual.syl
├── open-test.final.manual.syl
├── space-tab-space-to-tab.sh
└── train.txt.syl
./word-my2/
├── clean-space.pl
├── closed-test.word
├── mypara-all.manual.word
├── open-test.final.manual.word
├── space-tab-space-to-tab.sh
└── train.txt.word

0 directories, 17 files
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para$ 
```

အထက်မှာ ပြင်ထားခဲ့တဲ့ word2vec, fasttext တွေက အောက်ပါအတိုင်းရှိ...  
  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$ tree ./mypara-{manual,syl,word}/
./mypara-manual/
├── all-para.fasttext.bin
├── all-para.fasttext.vector
├── all-para.word2vec
└── mypara-all.manual
./mypara-syl/
├── all-para.fasttext.bin
├── all-para.fasttext.vector
├── all-para.word2vec
└── mypara-all.manual.syl
./mypara-word/
├── all-para.fasttext.bin
├── all-para.fasttext.vector
├── all-para.word2vec
└── mypara-all.manual.word

0 directories, 12 files
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/syl-ngram/ref/playing_with_fasttext$
```

နောက်ပိုင်း ပြန်ကြည့်တဲ့အခါမှာ experiment လုပ်ခဲ့တဲ့ Deep Siamese folder အောက်မှာပဲ training/test ဒေတာရော, word2vec, fasttext တို့ရော အတူတူ ရှိနေစေချင်လို့ Deep Siamese NN experiment လုပ်နေတဲ့ folder အောက်ကိုလည်း ကော်ပီကူး သိမ်းထားခဲ့။ copy ကူးနေရင်းနဲ့ HDD မှာ space တွေက မကျန်တော့လို့ ... file/forder တွေအတွက် space ပါ ထွက်လာအောင် လုပ်ခဲ့ရ့...
  
word2vec, fasttext တွေက HDD space နေရာ တော်တော်ယူတယ်။ tensorflow နဲ့ မော်ဒယ်ဆောက်တဲ့အခါမှာလည်း မော်ဒယ်ဖိုင်က size ကြီးတယ်။ အထူးသဖြင့် bin ဖိုင်တွေက...  
  
```
 (base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity/w2v_fasttext$ ll -h ./mypara-{manual,syl,word}
./mypara-manual:
total 4.0G
drwxrwxr-x 3 ye ye 4.0K စက်   16 12:12 ./
drwxrwxr-x 7 ye ye 4.0K စက်   15 23:18 ../
-rw-rw-r-- 1 ye ye 3.8G စက်   16 12:12 all-para.fasttext.bin
-rw-rw-r-- 1 ye ye  32M စက်   16 12:12 all-para.fasttext.vector
-rw-rw-r-- 1 ye ye 158M စက်   16 12:12 all-para.word2vec
-rw-rw-r-- 1 ye ye 8.3M စက်   16 12:12 mypara-all.manual
drwxrwxr-x 2 ye ye 4.0K စက်   16 12:10 tmp/

./mypara-syl:
total 3.8G
drwxrwxr-x 2 ye ye 4.0K စက်   16 12:13 ./
drwxrwxr-x 7 ye ye 4.0K စက်   15 23:18 ../
-rw-rw-r-- 1 ye ye 3.8G စက်   16 12:13 all-para.fasttext.bin
-rw-rw-r-- 1 ye ye 9.7M စက်   16 12:13 all-para.fasttext.vector
-rw-rw-r-- 1 ye ye  14M စက်   16 12:13 all-para.word2vec
-rwxr-xr-x 1 ye ye 8.5M စက်   16 12:13 mypara-all.manual.syl*

./mypara-word:
total 3.9G
drwxrwxr-x 2 ye ye 4.0K စက်   16 12:14 ./
drwxrwxr-x 7 ye ye 4.0K စက်   15 23:18 ../
-rw-rw-r-- 1 ye ye 3.8G စက်   16 12:27 all-para.fasttext.bin
-rw-rw-r-- 1 ye ye  23M စက်   16 12:27 all-para.fasttext.vector
-rw-rw-r-- 1 ye ye  52M စက်   16 12:27 all-para.word2vec
-rwxr-xr-x 1 ye ye 8.3M စက်   16 12:27 mypara-all.manual.word*
```
  
### word2vec embedding
  
Training မလုပ်ခင်မှာ training data ကို run မယ့် path အောက်ကို copy ကူးခဲ့...   
ခု run မှာက manual word segmentation (i.e. original myPara Corpus data) နဲ့...  
  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ cp train.txt /home/ye/exp/myPara2/deep-siamese-text-similarity/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ cp ./closed-test /home/ye/exp/myPara2/deep-siamese-text-similarity/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ cp ./open-test.final.manual /home/ye/exp/myPara2/deep-siamese-text-similarity/
```
  
Start training ...  
Working under following path with "paraphrase2" conda environment:  
    (paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity  
  
```
$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-manual/all-para.word2vec --embedding_dim 500 --num_epochs 200 2>&1 | tee train-manual-epoch200-w2v.16sept2021.log1
  ...
  ...
  ...
TRAIN 2021-09-16T13:45:58.460771: step 113598, loss 0.0164377, acc 0.96875
(0, 0, 1, 0, 0, 0, 1, 1, 1, 1, 0, 0, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 1, 1, 1, 0, 0, 1, 0, 0, 1, 1, 0, 1, 0, 1, 0, 1, 0, 1, 1, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 1) [0.9419964  0.9909818  0.03355075 0.9520038  0.985154   0.98097736
 0.04736961 0.06299996 0.02146125 0.04941377 0.9315572  0.9936179
 0.98336387 0.01307698 0.19319095 0.9956813  0.03895702 0.00616257
 0.9859238  0.9874242  0.9878587  0.98022336 0.9877094  0.05571805
 0.97808695 0.0608202  0.99026346 0.90719754 0.1894708  0.9809522
 0.00761485 0.8945809  0.21627101 0.03647421 0.04645642 0.02929282
 0.9931745  0.85217273 0.02578556 0.9927515  0.1353821  0.02260694
 0.01082476 0.90786713 0.04211792 0.74116445 0.09564605 0.9941705
 0.26394233 0.83126986 0.00944646 0.02681115 0.11433662 0.9963453
 0.99385935 0.876727   0.05314198 0.99081814 0.8899707  0.03243851
 0.9952672  0.99259424 0.06914932 0.0164423 ] [0. 0. 1. 0. 0. 0. 1. 1. 1. 1. 0. 0. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 0. 1.
 0. 1. 0. 0. 1. 0. 1. 0. 1. 1. 1. 1. 0. 0. 1. 0. 1. 1. 1. 0. 1. 0. 1. 0.
 1. 0. 1. 1. 1. 0. 0. 0. 1. 0. 0. 1. 0. 0. 1. 1.]
TRAIN 2021-09-16T13:45:58.492594: step 113599, loss 0.0114836, acc 0.984375
(0, 0, 1, 1, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 1, 0, 0, 1, 1, 0, 1, 0, 0, 0, 1, 1, 1, 0, 1, 1, 1, 0, 1, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0) [0.79993486 0.992949   0.06948991 0.05092521 0.03792386 0.91978157
 0.02029573 0.71337444 0.91844106 0.17576876 0.9746574  0.8667417
 0.9050173  0.9465583  0.99242526 0.9912101  0.93995774 0.04787563
 0.02709529 0.98775923 0.9947058  0.99531883 0.9826074  0.96631557
 0.95957094 0.9319243  0.03641484 0.9755334  0.00654725 0.02921274
 0.8235116  0.8792676  0.01477309 0.9838968  0.00803334 0.01066745
 0.99425125 0.98887813 0.24063577 0.31871438 0.81006485 0.0809553
 0.9903365  0.9939361  0.98814297 0.10051856 0.05503315 0.01802728
 0.98636484 0.0078872  0.02045328 0.05821494 0.87361485 0.09010669
 0.9739269  0.02070081 0.15535516 0.99492806 0.9641502  0.9930214
 0.9756709  0.9941101  0.99529564 0.9588737 ] [0. 0. 1. 1. 1. 0. 1. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 0.
 0. 0. 1. 0. 1. 1. 0. 0. 1. 0. 1. 1. 0. 0. 1. 1. 0. 1. 0. 0. 0. 1. 1. 1.
 0. 1. 1. 1. 0. 1. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0.]
TRAIN 2021-09-16T13:45:58.525368: step 113600, loss 0.00698656, acc 0.984375
(1, 0, 0, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 1, 0, 1, 0, 1) [0.02720496 0.9852954  0.98378694 0.9973933  0.91634786 0.06061707
 0.04017207 0.9767052  0.92036635 0.03009795 0.05432156 0.04535866
 0.79143333 0.9295048  0.9250981  0.03223426 0.0148273  0.9574951
 0.9031704  0.97588176 0.02884737 0.9878285  0.9943944  0.9934299
 0.99659365 0.1079848  0.98559237 0.8866228  0.9876645  0.99414647
 0.913203   0.9364064  0.9441828  0.03129002 0.96649086 0.99488336
 0.99453557 0.8283133  0.9891788  0.0415177  0.9855306  0.07026331
 0.04727738 0.0393959  0.01999033 0.18869656 0.07366163 0.8585527
 0.99243706 0.982875   0.9490559  0.03244815 0.0427594  0.9697372
 0.9604285  0.9625252  0.96492845 0.98167986 0.01314194 0.11413096
 0.9780259  0.08663671 0.9871331  0.78975767] [1. 0. 0. 0. 0. 1. 1. 0. 0. 1. 1. 1. 0. 0. 0. 1. 1. 0. 0. 0. 1. 0. 0. 0.
 0. 1. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 0. 1. 1. 1. 1. 1. 1. 0.
 0. 0. 0. 1. 1. 0. 0. 0. 0. 0. 1. 1. 0. 1. 0. 0.]

real	63m55.843s
user	302m5.470s
sys	35m5.831s
```
  
Closed-test နဲ့ Evaluation ရလဒ်က...  
  
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631770932/checkpoints/model-97000 --vocab_filepath ./runs/1631770932/checkpoints/vocab --eval_filepath ./closed-test
...
...
...
0.02291765995323658
0.962419867515564
0.017590908333659172
0.016503769904375076
0.17908570170402527
0.9913085103034973
0.0086247269064188
0.05625711381435394
0.9947324991226196
0.9085485339164734
0.9825022220611572
0.024478977546095848
0.02972199022769928
0.02680038847029209
Accuracy: 0.969

real	0m6.462s
user	0m6.960s
sys	0m1.242s
```

Open test နဲ့ Evaluation ရလဒ်...  
  
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631770932/checkpoints/model-97000 --vocab_filepath ./runs/1631770932/checkpoints/vocab --eval_filepath ./open-test.final.manual
...
...
...
0.7002002000808716
0.9887453317642212
0.9927669167518616
0.9894479513168335
0.9788118004798889
0.9657342433929443
0.9853591322898865
0.9841658473014832
0.9000328183174133
0.043093930929899216
Accuracy: 0.447447

real	0m6.261s
user	0m6.960s
sys	0m1.261s
```
  
<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/word-manual-200epoch-w2v-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/word-manual-200epoch-w2v-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with Manual-Word, word2vec, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>
  
**open test data နဲ့ ရလဒ်တွေက နည်းတယ်...  fasttext embedding မှာ ရလဒ်ပိုကောင်းလာဖို့ မျှော်လင့်တယ်...  
  
### with fasttext embedding

  to do ...  
  
## Training with Syllable Unit, 200 Epoch
  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/syl-my2$ cp train.txt.syl /home/ye/exp/myPara2/deep-siamese-text-similarity/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/syl-my2$ cp ./closed-test.syl /home/ye/exp/myPara2/deep-siamese-text-similarity/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/syl-my2$ cp ./open-test.final.manual.syl /home/ye/exp/myPara2/deep-siamese-text-similarity/

(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ mv train.txt.syl train.txt
```

### with word2vec embedding
  
Training...  
  
```
 (paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-syl/all-para.word2vec --embedding_dim 500 --num_epochs 200 2>&1 | tee train-syl-epoch200-w2v.16sept2021.log1
...
...
...
 0.02091654 0.9663267  0.90700865 0.04371732 0.8961842  0.00296073
 0.02215976 0.9899095  0.95406896 0.9793343 ] [0. 0. 0. 0. 1. 1. 1. 0. 0. 1. 1. 1. 0. 0. 0. 1. 1. 0. 1. 0. 0. 1. 1. 1.
 0. 0. 0. 1. 1. 1. 0. 1. 0. 1. 1. 1. 0. 0. 0. 1. 0. 1. 0. 0. 1. 0. 0. 1.
 1. 0. 0. 1. 0. 0. 1. 0. 0. 1. 0. 1. 1. 0. 0. 0.]
TRAIN 2021-09-16T16:52:31.345629: step 113597, loss 0.0152269, acc 0.96875
(1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 1, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 1, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 1, 1, 1, 1) [0.01455327 0.9870814  0.97746    0.89777565 0.98396546 0.79817986
 0.97968453 0.8180441  0.04095497 0.9475394  0.98304874 0.1846217
 0.98348427 0.9900868  0.99144804 0.7470401  0.96919894 0.69581765
 0.0300861  0.837663   0.9907724  0.93667954 0.00896425 0.00537071
 0.78860366 0.879115   0.24495238 0.9916818  0.98600805 0.99128544
 0.98098963 0.02455625 0.02071692 0.98255116 0.0159982  0.9348165
 0.9500329  0.9874977  0.98482704 0.9903666  0.04137152 0.05610597
 0.9798864  0.02006133 0.9931502  0.01306872 0.02230313 0.9845925
 0.01289491 0.10466327 0.98278373 0.98818314 0.9677835  0.8517117
 0.94684416 0.98614323 0.7966163  0.07903998 0.02673028 0.81548256
 0.08668354 0.00731071 0.06214686 0.01715842] [1. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 1. 1.
 0. 0. 1. 0. 0. 0. 0. 1. 1. 0. 1. 0. 0. 0. 0. 0. 1. 1. 0. 1. 0. 1. 1. 0.
 1. 1. 0. 0. 0. 0. 0. 0. 0. 1. 1. 0. 1. 1. 1. 1.]
TRAIN 2021-09-16T16:52:31.378339: step 113598, loss 0.00246232, acc 1
(0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 1, 0, 0, 1, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 1, 1, 0, 0, 1, 1, 0) [0.9851777  0.9911565  0.00414244 0.9724044  0.9699916  0.85211194
 0.97888607 0.9501937  0.09561642 0.97362673 0.9806172  0.96781343
 0.90781885 0.00816202 0.9413196  0.99725777 0.21034437 0.01093046
 0.94182307 0.9494229  0.0994199  0.05172439 0.9798627  0.01242599
 0.01314907 0.98836374 0.98557526 0.07227623 0.9346365  0.8334887
 0.98978895 0.9114609  0.15247263 0.98825127 0.0172944  0.14457922
 0.98715407 0.9391851  0.0461673  0.9902375  0.98141754 0.8572563
 0.00651553 0.96711093 0.9926239  0.98899114 0.94974506 0.9800238
 0.8942215  0.95001954 0.9817894  0.9644184  0.05566928 0.8785487
 0.05999915 0.9694745  0.93233126 0.05348293 0.14041512 0.9896282
 0.96250725 0.06997442 0.09076206 0.96941084] [0. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 1. 0. 0. 1. 1. 0. 0. 1. 1. 0. 1.
 1. 0. 0. 1. 0. 0. 0. 0. 1. 0. 1. 1. 0. 0. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 1. 0. 1. 0. 0. 1. 1. 0. 0. 1. 1. 0.]
TRAIN 2021-09-16T16:52:31.412571: step 113599, loss 0.0106745, acc 0.984375
(1, 1, 1, 0, 1, 0, 0, 1, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0) [0.07511511 0.00992862 0.09383474 0.9845103  0.42750978 0.9885962
 0.9737026  0.03921494 0.9897507  0.01142494 0.28653    0.99063355
 0.93259156 0.81163394 0.9111803  0.84107625 0.10002489 0.9631664
 0.00950325 0.03967316 0.8516903  0.9900489  0.02514343 0.11052439
 0.8007279  0.99114406 0.92940557 0.01485086 0.01612651 0.91075027
 0.98484623 0.9650639  0.01353214 0.00924495 0.98925036 0.9865781
 0.9861669  0.12311102 0.97243387 0.85635215 0.88017154 0.9690309
 0.98886216 0.01519664 0.02136359 0.95893246 0.91234    0.9921954
 0.04504061 0.9822806  0.03222006 0.9835961  0.99060905 0.04959264
 0.9323055  0.84680355 0.9873483  0.9832903  0.9295842  0.98844165
 0.01231659 0.16103679 0.97759914 0.99631435] [1. 1. 1. 0. 1. 0. 0. 1. 0. 1. 1. 0. 0. 0. 0. 0. 1. 0. 1. 1. 0. 0. 1. 1.
 0. 0. 0. 1. 1. 0. 0. 0. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 1. 0. 0. 0.
 1. 0. 1. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 1. 0. 0.]/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:458: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
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
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/numpy/core/_asarray.py:83: VisibleDeprecationWarning: Creating an ndarray from ragged nested sequences (which is a list-or-tuple of lists-or-tuples-or ndarrays with different lengths or shapes) is deprecated. If you meant to do this, you must specify 'dtype=object' when creating the ndarray
  return array(a, dtype, copy=False, order=order)

TRAIN 2021-09-16T16:52:31.447157: step 113600, loss 0.00366657, acc 1
(0, 1, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 1, 0, 0, 0, 1, 1, 1, 0, 0, 1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 0) [0.8490067  0.01250746 0.00801008 0.01475833 0.93831295 0.7886718
 0.9162655  0.01692229 0.9873203  0.9800165  0.9525264  0.97410685
 0.01648008 0.86701304 0.985644   0.9863476  0.793619   0.06214541
 0.97326267 0.03008804 0.96568096 0.0487156  0.9885504  0.98825496
 0.12289882 0.99012816 0.02196589 0.89089894 0.98969877 0.17093301
 0.0271644  0.9822771  0.8341764  0.99178284 0.01329917 0.01756735
 0.04102688 0.79551387 0.9314474  0.02096893 0.26229507 0.98347366
 0.85389024 0.01125636 0.97005534 0.15467514 0.92432976 0.9734198
 0.03029069 0.98420954 0.99407595 0.0479748  0.9730881  0.9876717
 0.89958215 0.05553504 0.88420814 0.00268378 0.86370724 0.01418513
 0.9902393  0.01337512 0.9036564  0.9709314 ] [0. 1. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 1. 0. 0. 0. 0. 1. 0. 1. 0. 1. 0. 0.
 1. 0. 1. 0. 0. 1. 1. 0. 0. 0. 1. 1. 1. 0. 0. 1. 1. 0. 0. 1. 0. 1. 0. 0.
 1. 0. 0. 1. 0. 0. 0. 1. 0. 1. 0. 1. 0. 1. 0. 0.]

real	64m32.060s
user	300m59.195s
sys	36m45.968s
```

Evaluation with open test data...  
  
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631782087/checkpoints/model-48000 --vocab_filepath ./runs/1631782087/checkpoints/vocab --eval_filepath ./open-test.final.manual.syl
...
...
...
0.9907528162002563
0.9839120507240295
0.9847670197486877
0.9224840402603149
0.9677222967147827
0.9731126427650452
0.9694141149520874
0.08521928638219833
Accuracy: 0.44044

real	0m6.388s
user	0m6.941s
sys	0m1.198s 
```
  
Evaluation with closed test data...  
  
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631782087/checkpoints/model-48000 --vocab_filepath ./runs/1631782087/checkpoints/vocab --eval_filepath ./closed-test.syl 
...
...
...
0.2634804844856262
0.8883613348007202
0.06093858927488327
0.8401598334312439
0.016606930643320084
0.06594143062829971
0.11839007586240768
0.9407025575637817
0.04454350098967552
0.11671852320432663
0.9733070135116577
0.8989876508712769
0.9675915241241455
0.08163182437419891
0.03284897282719612
0.015808621421456337
Accuracy: 0.964

real	0m6.290s
user	0m7.001s
sys	0m1.251s
```
  
<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/syl-200epoch-w2v-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/syl-200epoch-w2v-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with Syllable Unit, word2vec, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>
  
**open test data နဲ့ ရလဒ်တွေက နည်းတယ်...  fasttext embedding မှာ ရလဒ်ပိုကောင်းလာဖို့ မျှော်လင့်တယ်...  
  
### with fasttext embedding

to do...  
  
## Training with Word Unit Segmented with myWord Segmentation Tool, 200 Epoch

Training မလုပ်ခင်မှာ training data ကို run မယ့် path အောက်ကို copy ကူးခဲ့...   
ခု run မှာက "word segmentation with myWord" နဲ့...  
  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ ls
clean-space.pl  closed-test.word  mypara-all.manual.word  open-test.final.manual.word  space-tab-space-to-tab.sh  train.txt.word
```
  
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ cp train.txt.word /home/ye/exp/myPara2/deep-siamese-text-similarity/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ cp ./closed-test.word /home/ye/exp/myPara2/deep-siamese-text-similarity/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$ cp ./open-test.final.manual.word /home/ye/exp/myPara2/deep-siamese-text-similarity/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/word-my2$
```
  
train.py က ယူသုံးမှာက train.txt ဖိုင်မို့လို့ train.txt.word ကို train.txt အဖြစ် နာမည်ပြောင်းပေးခဲ့...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ mv train.txt.word train.txt
```
  
### with word2vec embedding
  
Start training ...  
  
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-word/all-para.word2vec --embedding_dim 500 --num_epochs 200 2>&1 | tee train-myWord-epoch200-w2v.16sept2021.log1
...
...
...
TRAIN 2021-09-16T22:29:24.619464: step 113597, loss 0.00265531, acc 1
(0, 1, 0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 1, 0, 0, 0, 1, 0, 1, 1, 0, 0, 0, 1, 1, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 1, 0, 1, 1, 1, 0, 1, 0, 1, 0, 1, 0, 0, 1, 1, 0, 0) [0.9850662  0.00879405 0.88440835 0.05313137 0.9688384  0.95900524
 0.2709356  0.98392254 0.9844128  0.03006384 0.97595656 0.13284539
 0.00268415 0.97408813 0.9471427  0.9660672  0.1607805  0.94651824
 0.06383909 0.01886019 0.99257773 0.9954775  0.852071   0.02334686
 0.1434339  0.01201858 0.95887965 0.94713104 0.07107159 0.95804334
 0.9982065  0.03837465 0.9866807  0.03026451 0.9302049  0.9927166
 0.03563291 0.9545246  0.9911042  0.03209935 0.90917605 0.03427913
 0.9643064  0.830687   0.04606726 0.9955016  0.02075966 0.09254609
 0.9907924  0.04575163 0.13259092 0.04475972 0.97399265 0.05944297
 0.97562736 0.18986687 0.93324214 0.03005751 0.9679934  0.99646586
 0.05618291 0.02735716 0.99419653 0.9948907 ] [0. 1. 0. 1. 0. 0. 1. 0. 0. 1. 0. 1. 1. 0. 0. 0. 1. 0. 1. 1. 0. 0. 0. 1.
 1. 1. 0. 0. 1. 0. 0. 1. 0. 1. 0. 0. 1. 0. 0. 1. 0. 1. 0. 0. 1. 0. 1. 1.
 0. 1. 1. 1. 0. 1. 0. 1. 0. 1. 0. 0. 1. 1. 0. 0.]
TRAIN 2021-09-16T22:29:24.653275: step 113598, loss 0.00271718, acc 1
(0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 1, 1, 1, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 1, 1, 0, 1, 0, 0) [0.949876   0.99576133 0.98642087 0.9695648  0.9895049  0.9758769
 0.8850004  0.9160057  0.04041297 0.9765084  0.99484813 0.00992112
 0.1212589  0.8923535  0.97863036 0.9533763  0.03723662 0.06007402
 0.07296715 0.02726118 0.87807906 0.9495408  0.0352279  0.08962715
 0.9534285  0.99601376 0.07681897 0.08117759 0.01949989 0.995418
 0.02420102 0.07956555 0.03698553 0.94706136 0.9791973  0.10253704
 0.99059325 0.9947502  0.89953357 0.8917115  0.9964431  0.97180307
 0.9876075  0.9898226  0.99233794 0.9822397  0.1741165  0.9951472
 0.9788798  0.02381705 0.9327281  0.9594176  0.32997692 0.97155994
 0.9611574  0.00798038 0.9490846  0.04287683 0.03966755 0.07784478
 0.9220738  0.01653555 0.8412575  0.9636669 ] [0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 1. 0. 0. 0. 1. 1. 1. 1. 0. 0. 1. 1.
 0. 0. 1. 1. 1. 0. 1. 1. 1. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0.
 0. 1. 0. 0. 1. 0. 0. 1. 0. 1. 1. 1. 0. 1. 0. 0.]
TRAIN 2021-09-16T22:29:24.685580: step 113599, loss 0.0124779, acc 0.984375
(0, 1, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 1, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 1, 0, 1, 1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 1) [0.9089788  0.10335294 0.05535833 0.9641084  0.984347   0.9956428
 0.01737725 0.9824617  0.9111592  0.01741187 0.96804607 0.8826667
 0.06341025 0.96089303 0.94698614 0.9872213  0.04567855 0.10100064
 0.9821623  0.9480066  0.32334182 0.16479255 0.9454978  0.9401492
 0.01186842 0.14180285 0.15474096 0.05359622 0.98796976 0.88560826
 0.8695659  0.75225425 0.9175623  0.98482704 0.8507125  0.99403775
 0.9827479  0.9894304  0.94528985 0.02310562 0.9791361  0.01040859
 0.9132292  0.02285045 0.01931922 0.8133418  0.03051075 0.01788426
 0.9965208  0.41708893 0.93525636 0.9462767  0.9007239  0.9401036
 0.03356254 0.98747414 0.8815259  0.9957233  0.9743943  0.9511638
 0.02205978 0.22141515 0.8915794  0.05244731]/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:458: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
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
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/numpy/core/_asarray.py:83: VisibleDeprecationWarning: Creating an ndarray from ragged nested sequences (which is a list-or-tuple of lists-or-tuples-or ndarrays with different lengths or shapes) is deprecated. If you meant to do this, you must specify 'dtype=object' when creating the ndarray
  return array(a, dtype, copy=False, order=order)
 [0. 1. 1. 0. 0. 0. 1. 0. 0. 1. 0. 0. 1. 0. 0. 0. 1. 1. 0. 0. 1. 1. 0. 0.
 1. 1. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0. 1. 1. 0. 1. 1.
 0. 1. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 1. 0. 1.]
TRAIN 2021-09-16T22:29:24.720883: step 113600, loss 0.00398123, acc 1
(1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 1, 1, 0, 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 1) [0.00700924 0.01974106 0.9644851  0.9479363  0.9134623  0.07460944
 0.9497177  0.9906787  0.9586223  0.9581748  0.0276198  0.03787733
 0.02507436 0.9916055  0.07310243 0.03522433 0.78171974 0.0124846
 0.0794319  0.8522914  0.20754345 0.02846266 0.8723001  0.9738412
 0.01350101 0.9621868  0.01790376 0.03560381 0.2098181  0.987656
 0.9880347  0.98566204 0.04464159 0.9617633  0.98133373 0.91524345
 0.9428236  0.03154174 0.12129259 0.9866109  0.9604344  0.95209914
 0.2890827  0.92596334 0.92799103 0.99370915 0.98004067 0.02385005
 0.9769717  0.8417644  0.13906741 0.9692392  0.78598285 0.06859816
 0.9953218  0.99608994 0.990479   0.9877418  0.1757418  0.9861319
 0.07057042 0.99606776 0.8272302  0.01530872] [1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 1. 1. 1. 0. 1. 1. 0. 1. 1. 0. 1. 1. 0. 0.
 1. 0. 1. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 1.
 0. 0. 1. 0. 0. 1. 0. 0. 0. 0. 1. 0. 1. 0. 0. 1.]

real	63m46.110s
user	300m46.858s
sys	36m11.341s
```
  
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631802346/checkpoints/model-97000 --vocab_filepath ./runs/1631802346/checkpoints/vocab --eval_filepath ./open-test.final.manual.word 
...
...
...
0.46157094836235046
0.9662734866142273
0.9818298816680908
0.9758252501487732
0.9846404790878296
0.9772659540176392
0.9684680104255676
0.9769710302352905
0.982317328453064
0.08774643391370773
Accuracy: 0.444444

real	0m6.427s
user	0m7.003s
sys	0m1.126s
```
  
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631802346/checkpoints/model-97000 --vocab_filepath ./runs/1631802346/checkpoints/vocab --eval_filepath ./closed-test.word 
...
...
...
0.8838050365447998
0.8108258843421936
0.017134888097643852
0.9742394685745239
0.9144530892372131
0.8724464178085327
0.14075440168380737
0.060980163514614105
0.025890707969665527
Accuracy: 0.96

real	0m6.303s
user	0m6.980s
sys	0m1.317s
```
  
<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-200epoch-w2v-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-200epoch-w2v-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "Word Unit Segmented with myWord", word2vec, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>
  
### with fasttext embedding

  
 
## Training with character Embedding, 200 Epoch

### with Manual Segmented Word

```
  (base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ cp train.txt /home/ye/exp/myPara2/deep-siamese-text-similarity/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ cp closed-test /home/ye/exp/myPara2/deep-siamese-text-similarity/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my2$ cp open-test.final.manual /home/ye/exp/myPara2/deep-siamese-text-similarity/
```
  
Training...  
  
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --num_epochs 200 2>&1 | tee train-manualWord-epoch200-char.17sept2021.log1
...
...
...
TRAIN 2021-09-17T08:33:40.437386: step 113599, loss 0.0176852, acc 0.96875
(1, 1, 1, 1, 0, 0, 0, 0, 1, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 1, 1, 1, 1, 0, 1, 0, 0, 1, 0, 1, 1, 0, 1, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 1) [0.01710249 0.02088132 0.49095032 0.9991442  0.9999758  0.99992573
 0.95847493 0.9984738  0.06186721 0.9999667  0.10709501 0.01128071
 0.99907947 0.03544362 0.02262182 0.9594318  0.9400406  0.9662051
 0.9996135  0.05338364 0.99991    0.9810591  0.80223364 0.9999611
 0.9916298  0.1145042  0.94660133 0.9462263  0.98968065 0.99939805
 0.03688958 0.9594914  0.9973829  0.12264115 0.140586   0.02213434
 0.02216515 0.06106067 0.9997547  0.13217804 0.92550236 0.9999489
 0.02034801 0.9971149  0.01402947 0.0475621  0.9546379  0.14907146
 0.35601988 0.99997973 0.03583423 0.042423   0.9942232  0.2184124
 0.02563166 0.99722993 0.84842104 0.9992327  0.9998519  0.9911397
 0.131085   0.2497375  0.9999235  0.01674522] [1. 1. 1. 0. 0. 0. 0. 0. 1. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 1. 0. 0. 0. 0.
 0. 1. 0. 0. 0. 0. 1. 0. 0. 1. 1. 1. 1. 1. 0. 1. 0. 0. 1. 0. 1. 1. 0. 1.
 1. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 0. 1. 1. 0. 1.]
TRAIN 2021-09-17T08:33:40.470940: step 113600, loss 0.00688723, acc 0.984375
(0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1, 1, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0) [0.98606527 0.9880705  0.99935925 0.02286364 0.0189631  0.86225116
 0.91923463 0.99816185 0.99751365 0.9987128  0.03547265 0.91534126
 0.14326613 0.93578094 0.43920103 0.99994385 0.9747022  0.9870132
 0.03487771 0.49595645 0.99516356 0.02786031 0.21102893 0.13855019
 0.9690649  0.99436605 0.9999864  0.9195651  0.01294936 0.0185043
 0.9934532  0.99892604 0.99970025 0.9999463  0.02631062 0.04114269
 0.9999871  0.99993694 0.04113905 0.9999525  0.14205377 0.01648929
 0.12497853 0.91579515 0.02329412 0.20557167 0.9999837  0.08783047
 0.14494622 0.21899173 0.03457058 0.99919385 0.9948132  0.7303538
 0.11688264 0.9931345  0.99962676 0.99112314 0.79970384 0.04410025
 0.0113913  0.9975709  0.9978006  0.94006103] [0. 0. 0. 1. 1. 0. 0. 0. 0. 0. 1. 0. 1. 0. 1. 0. 0. 0. 1. 1. 0. 1. 1. 1.
 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 1. 1. 0. 0. 1. 0. 1. 1. 1. 0. 1. 1. 0. 1.
 1. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 1. 1. 0. 0. 0.]

real	58m54.268s
user	286m47.183s
sys	34m45.287s
```

Evaluation with Open Test...   
  
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631838895/checkpoints/model-79000 --vocab_filepath ./runs/1631838895/checkpoints/vocab --eval_filepath ./open-test.final.manual.syl
...
...
...
0.9446943402290344
0.983420729637146
0.9538199305534363
0.9711295366287231
0.9995074272155762
0.99341881275177
0.21550516784191132
0.9981439709663391
0.9975602626800537
0.9822693467140198
0.7379894852638245
0.8074220418930054
0.9981020092964172
0.797886848449707
0.9995074272155762
0.9907914996147156
0.9994357228279114
0.996101438999176
0.9993839263916016
0.9193836450576782
0.9951070547103882
0.7995368838310242
Accuracy: 0.437437

real	0m7.580s
user	0m7.759s
sys	0m1.296s
```
  
Evaluation with Closed Test...   
  
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631838895/checkpoints/model-79000 --vocab_filepath ./runs/1631838895/checkpoints/vocab --eval_filepath ./closed-test
...
...
...
0.8203821182250977
0.07618311792612076
0.08052340894937515
0.10361530631780624
0.9595077633857727
0.030501002445816994
0.47866925597190857
0.999776303768158
0.9998214840888977
0.9912829995155334
0.3728065490722656
0.014010102488100529
0.030996309593319893
Accuracy: 0.941

real	0m7.319s
user	0m7.852s
sys	0m1.321s
```
  
<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/manualWord-200epoch-char-nosimu-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/manualWord-200epoch-char-nosimu-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "Manual Word Segmentation", char, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>  

### with Syllable Unit  

Syllable segmentation လုပ်ထားတဲ့ training ဖိုင်၊ open test data ဖိုင်၊ closed-test data ဖိုင်တွေကို Deep Siamese ပရိုဂရမ် run မယ့် ဖိုလ်ဒါအောက်ကို ကူးပြီးတော့...  
Training...  
  
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --num_epochs 200 2>&1 | tee train-syllable-epoch200-char.17sept2021.log1
...
...
...
 0. 0. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0.]
TRAIN 2021-09-17T03:27:45.698857: step 113599, loss 0.0151053, acc 0.96875
(1, 1, 1, 1, 0, 0, 0, 0, 1, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 1, 1, 1, 1, 0, 1, 0, 0, 1, 0, 1, 1, 0, 1, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 1) [0.01244726 0.05930466 0.52322394 0.14285411 0.9999475  0.9997004
 0.9778462  0.99735653 0.20036602 0.99254894 0.05704248 0.03587206
 0.9802339  0.05712055 0.06057943 0.99722415 0.928086   0.8984999
 0.998682   0.04652771 0.9998792  0.98051095 0.9575911  0.9999521
 0.9683923  0.1251368  0.79908717 0.70171845 0.97755516 0.7949107
 0.06328318 0.97031224 0.9997542  0.05919214 0.3735775  0.04111467
 0.06268573 0.09404915 0.99807936 0.28363353 0.9939709  0.9929386
 0.09345161 0.99650466 0.02310976 0.0987618  0.9493103  0.10939773
 0.4642903  0.9620684  0.05345828 0.02731799 0.99941707 0.12383053
 0.06630751 0.985526   0.9820592  0.9980037  0.9998971  0.9991964
 0.15190373 0.2856892  0.98948646 0.01193938] [1. 1. 0. 1. 0. 0. 0. 0. 1. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 1. 0. 0. 0. 0.
 0. 1. 0. 0. 0. 0. 1. 0. 0. 1. 1. 1. 1. 1. 0. 1. 0. 0. 1. 0. 1. 1. 0. 1.
 1. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 0. 1. 1. 0. 1.]
TRAIN 2021-09-17T03:27:45.729125: step 113600, loss 0.0192622, acc 0.96875
(0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1, 1, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0) [0.99701834 0.99960726 0.947118   0.0634083  0.05877936 0.8282125
 0.9972906  0.74603134 0.96146196 0.99630105 0.0898889  0.91051716
 0.03797238 0.763806   0.29922253 0.9999772  0.94923866 0.99860877
 0.04185865 0.5229606  0.9993906  0.03580802 0.15488438 0.15347345
 0.95345455 0.9992983  0.89077234 0.97280717 0.03480324 0.01513536
 0.9447719  0.95918524 0.9993739  0.9181629  0.0279074  0.3687679
 0.9998054  0.993611   0.06327686 0.9980404  0.14335655 0.0341741
 0.05541288 0.98687106 0.01099566 0.295234   0.99130446 0.13808285
 0.05508539 0.07567084 0.05212153 0.99935484 0.99882317 0.1237691
 0.06947734 0.946094   0.9992038  0.95013994 0.9371162  0.8944203
 0.01671701 0.9981475  0.99937534 0.84970325] [0. 0. 0. 1. 1. 0. 0. 0. 0. 0. 1. 0. 1. 0. 1. 0. 0. 0. 1. 0. 0. 1. 1. 1.
 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 1. 1. 0. 0. 1. 0. 1. 1. 1. 0. 1. 1. 0. 1.
 1. 1. 1. 0. 0. 1. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0.]

real	58m52.449s
user	287m49.006s
sys	34m30.836s
```
  
Evaluation with Open Test...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631820543/checkpoints/model-82000 --vocab_filepath ./runs/1631820543/checkpoints/vocab --eval_filepath ./open-test.final.manual.syl 
...
...
...
0.9570709466934204
0.9942687749862671
0.8381921052932739
0.9008236527442932
0.9921364784240723
0.9986552596092224
0.9997888207435608
0.9983261227607727
0.9993004202842712
0.9994852542877197
0.999622106552124
0.9715873599052429
0.998479425907135
0.9661536812782288
Accuracy: 0.428428

real	0m7.631s
user	0m7.906s
sys	0m1.398s
```
  
Evaluation with Closed Test...  
  
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631820543/checkpoints/model-82000 --vocab_filepath ./runs/1631820543/checkpoints/vocab --eval_filepath ./closed-test.syl 
...
...
...
0.17807729542255402
0.8669766187667847
0.05581562593579292
0.9736708998680115
0.9992751479148865
0.9468411207199097
0.997136652469635
0.6256596446037292
0.08919131010770798
0.10025789588689804
Accuracy: 0.922

real	0m7.382s
user	0m7.971s
sys	0m1.272s
```
  
<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/syllable-200epoch-char-nosimu-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/syllable-200epoch-char-nosimu-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "Syllable", char, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>  

### with Word (segmented with myWord)

myWord နဲ့ segmentation လုပ်ထားတဲ့ training ဖိုင်၊ open test data ဖိုင်၊ closed-test data ဖိုင်တွေကို Deep Siamese ပရိုဂရမ် run မယ့် ဖိုလ်ဒါအောက်ကို ကူးပြီးတော့...  
Training...  
  
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --num_epochs 200 2>&1 | tee train-myWord-epoch200-char.17sept2021.log1
...
...
...
TRAIN 2021-09-17T02:16:11.807057: step 113599, loss 0.0110288, acc 0.984375
(1, 1, 1, 1, 0, 0, 0, 0, 1, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 1, 1, 1, 1, 0, 1, 0, 0, 1, 0, 1, 1, 0, 1, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 1) [0.03989657 0.02682988 0.39383897 0.1915212  0.9860914  0.9903423
 0.85367876 0.99820644 0.10371912 0.9544347  0.10991197 0.02838761
 0.97933185 0.01987699 0.07285393 0.99956274 0.9934865  0.93414015
 0.8427608  0.01826372 0.9791876  0.9481497  0.96179736 0.98475325
 0.9230137  0.12304137 0.99962646 0.97813594 0.98622394 0.9985329
 0.05658104 0.98762125 0.97758645 0.19862963 0.33726496 0.01119247
 0.01947715 0.09853523 0.96921617 0.3223927  0.9037315  0.99655503
 0.06173862 0.98966575 0.01818539 0.05283776 0.97668236 0.15290992
 0.39469957 0.9491836  0.06483429 0.04708945 0.99888504 0.29172167
 0.08881769 0.95779717 0.95472103 0.987724   0.9176121  0.9917869
 0.16548954 0.28660333 0.97811604 0.0215688 ] [1. 1. 1. 1. 0. 0. 0. 0. 1. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 1. 0. 0. 0. 0.
 0. 1. 0. 0. 0. 0. 1. 0. 0. 1. 1. 1. 1. 1. 0. 1. 0. 0. 1. 0. 1. 1. 0. 1.
 1. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 0. 1. 1. 0. 1.]
TRAIN 2021-09-17T02:16:11.837667: step 113600, loss 0.00795127, acc 0.96875
(0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1, 1, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0) [0.97486573 0.9763054  0.9238184  0.03463613 0.06548369 0.9837549
 0.9880085  0.7797943  0.93543947 0.97447747 0.15969199 0.8858988
 0.09098587 0.9584585  0.5139087  0.9785594  0.9842352  0.981734
 0.0301457  0.45745763 0.98850375 0.03458148 0.23927824 0.0982235
 0.9606329  0.996049   0.9509183  0.9665665  0.1064872  0.01467092
 0.83456874 0.9938178  0.980774   0.9355007  0.03297447 0.08123428
 0.93980485 0.986335   0.02482973 0.98618096 0.10677867 0.0216668
 0.04363763 0.9412012  0.0370629  0.26737562 0.9787755  0.18109982
 0.14164561 0.15257561 0.05249614 0.9987908  0.942929   0.97283506
 0.0916484  0.98466206 0.98943305 0.9368821  0.99554557 0.16027772
 0.03504372 0.9841427  0.9907694  0.99152714] [0. 0. 0. 1. 1. 0. 0. 0. 0. 0. 1. 0. 1. 0. 0. 0. 0. 0. 1. 1. 0. 1. 1. 1.
 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 1. 1. 0. 0. 1. 0. 1. 1. 1. 0. 1. 1. 0. 1.
 1. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 1. 1. 0. 0. 0.]

real	58m30.308s
user	286m21.230s
sys	34m25.437s
```

Evaluation with Open Test Data...  
  
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631816270/checkpoints/model-89000 --vocab_filepath ./runs/1631816270/checkpoints/vocab --eval_filepath ./open-test.final.manual.word 
...
...
...
0.9373813271522522
0.723473846912384
0.9477940201759338
0.9427857995033264
0.9797320365905762
0.9321064352989197
0.9682533740997314
0.722674548625946
0.9753073453903198
0.9798092842102051
Accuracy: 0.437437

real	0m7.645s
user	0m7.942s
sys	0m1.276s

```
  
Evaluation with Closed Test Data...  
  
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631816270/checkpoints/model-89000 --vocab_filepath ./runs/1631816270/checkpoints/vocab --eval_filepath ./closed-test.word 
...
...
...
0.08742140978574753
0.17588753998279572
0.03499225899577141
0.9809699058532715
0.20026858150959015
0.5987406373023987
0.9703155755996704
0.27455997467041016
0.9868044853210449
0.18742233514785767
0.04543688893318176
0.08513258397579193
Accuracy: 0.932

real	0m7.339s
user	0m7.923s
sys	0m1.236s 
```
  
<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-200epoch-char-nosimu-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-200epoch-char-nosimu-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "Word Unit Segmented with myWord", char, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>  


----------------
  
## Training Only with Paraphrase, Validation and Testing with (Para + Non-Pra)

traditional ML မှာ data နည်းတဲ့အခါ လုပ်ခဲ့တဲ့ နည်းလမ်းတစ်ခု... model အနေနဲ့ကတော့ intelligent မရှိဖြစ်သွားပေမဲ့....
NN မှာ လည်း စမ်းကြည့်ချင်ခဲ့...  

အဲဒီလို Run ဖို့အတွက်ဆိုရင် coding ကို ဝင်ပြင်ရလိမ့်မယ်။  

ပထမဆုံး run ခဲ့တဲ့ experiment နဲ့ အကြမ်းမျဉ်း တူသလိုလို ထင်ရပေမဲ့... တကယ်တမ်းက မတူဘူး။ ဘာကြောင့်လဲ ဆိုတော့ ပထမဆုံး run ခဲ့တဲ့ char approach မှာက training data က Para ကိုပဲ ပေးပေမဲ့ coding ထဲကနေ simulation လုပ်ပြီး nagetive label ပါ ပါတဲ့ validation ဖိုင်ကို auto ထုတ်တာမို့။   
တကယ်က အဲဒီလို auto ထုတ်တဲ့ validation ဖိုင်ကို မသုံးစေချင်လို့ ကိုယ့်ဖာသာကိုယ် validation ဖိုင်ကို assignment လုပ်ပြီးတော့ run လို့ ရတဲ့ ပုံစံနဲ့ လိုချင်တာမို့....  
ပြီးတော့ ဒီတစ်ခါက word2vec မော်ဒယ်ကို ကြိုဆောက်ထားပြီးမှ သွားကြည့်ချင်တာ။ ဆိုလိုတာက --nois_char_based option နဲ့ ပေးပြီး run ကြည့်ချင်တာ...  
အဲဒီလို လုပ်ရင် ဘာတွေကောင်းလာမှာမို့လို့လဲ လို့ဆိုရင်တော့ char embedding မဟုတ်တာကြောင့် ငါတို့မြန်မာစာအတွက်က အထက်မှာ စမ်းခဲ့သလို syllable, manual-word, word with segmenter စသည်ဖြင့် အမျိုးမျိုး segmentation လုပ်ကြည့်ပြီး expeirment လုပ်လို့ ရတယ်။ အဲဒီအပြင် word2vec ကို မော်ဒယ်အကြီး (ဆိုလိုတာက myWord corpus လို စာကြောင်းရေ ငါသိန်းနဲ့ ဆောက်ထားပြီးတော့) experiment လုပ်တာမျိုးလည်း လုပ်လို့ ရတယ်။ theory အရကတော့ ကောင်းတဲ့ အချက်တွေရှိတယ် သို့သော် လက်တွေ့ ရလဒ်တွေအပေါ် ဘယ်လောက် သက်ရောက်သလဲ ဆိုတာကတော့ experiment လုပ်ကြည့်ပြီးမှပဲ အသေအချာ ပြောနိုင်လိမ့်မယ်....   


Coding information of input_helpers.py:  

```python
    def dumpValidation(self,x1_text,x2_text,y,shuffled_index,dev_idx,i):
        print("dumping validation "+str(i))
        x1_shuffled=x1_text[shuffled_index]
        x2_shuffled=x2_text[shuffled_index]
        y_shuffled=y[shuffled_index]
        x1_dev=x1_shuffled[dev_idx:]
        x2_dev=x2_shuffled[dev_idx:]
        y_dev=y_shuffled[dev_idx:]
        del x1_shuffled
        del y_shuffled
        with open('validation.txt'+str(i),'w') as f:
            for text1,text2,label in zip(x1_dev,x2_dev,y_dev):
                f.write(str(label)+"\t"+text1+"\t"+text2+"\n")
            f.close()
        del x1_dev
        del y_dev
```

အထက်ပါ input_helpers.py ဖိုင်ရဲ့ dumpValidation() function အထဲက statement တွေကို ပိတ်လိုက်ရင် အိုကေပြီလို့ ထင်တယ်။  
training ဒေတာထဲမှာ positive label တွေချည်းပဲကို ပြင်ဆင်ထားပြီးတော့ validation.txt0 ဆိုတဲ့ ဖိုင်ကို ကိုယ့်ဖာသာကိုယ် ကြိုပြင်ထားပြီးတော့ run ရင် ရပြီလို့ ယူဆ...  


### Preprocessing

လက်ရှိ path ```/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/``` က Deep Siamese NN အတွက် ပြင်ခဲ့တဲ့ training, validation, test ဒေတာတွေကို သိမ်းထားတဲ့ folder ပါ။
အဲဒီအောက်မှာရှိတဲ့...  manual-my1, syl-1, word-1 က Deep Siamese ကို စစမ်းတုန်းက သုံးခဲ့တဲ့ ဒေတာတွေ...    

တကယ် formal experiment က manual-my2, syl-my2 နဲ့ word-my2 ကို သုံးပြီး လုပ်ခဲ့တယ်။  
စာတမ်းအတွက် အသုံးဝင်လိမ့်မယ်။  

ပြီးတော့ training data ကို positive label (ဆိုလိုတာက paraphrase တွေချည်းပဲ) ထားပြီး validation နဲ့ testing ကျမှပဲ both positive and negative label တွေနဲ့ train လုပ်ဖို့အတွက်  
အောက်ပါအတိုင်း manual-my2, syl-my2 နဲ့ word-my2 ဖိုလ်ဒါတွေကို ကော်ပီကူးခဲ့တယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para$ cp -r manual-my2 manual-my3
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para$ cp -r syl-my2 syl-my3
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para$ cp -r word-my2 word-my3
```

ပြီးမှ နံပါတ် 3 ဖိုလ်ဒါတွေအထဲမှာ positive only training data ဖြစ်အောင်နဲ့ validation set တွေကို ဝင်ပြင်ခဲ့တယ်။  
အောက်ပါအတိုင်း ...    

ဖိုင်နာမည်တွေ နဲ့ file size ကို အရင်ဆုံး စစ်ဆေး...    

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my3$ wc *
      32       91      686 clean-space.pl
    1000    16905   202235 closed-test
   84921   659489  8606282 mypara-all.manual
    1000    12674   138579 open-test.final.manual
   40461   672370  8350480 train.txt
  127414  1361529 17298262 total
```

train.txt ဖိုင်ကို shuffle လုပ်ခဲ့...  
```
$ shuf ./train.txt > train.txt.shuf
```

နဂို train.txt ဖိုင်ကိုလည်း train.txt.original ဆိုတဲ့ ဖိုင်နာမည်အဖြစ် နာမည်ပြောင်းသိမ်းခဲ့...  
```
$ mv train.txt train.txt.original
```

training ဖိုင် 
```
$ head -n 36415 ./train.txt.shuf > train.txt
```
validation or development ဖိုင်ကို ဆောက် (10%)
```
$ tail -n 4046 ./train.txt.shuf > validation.txt0
```

training ဖိုင်ကို ပြင်ဆင်...  
```
$ head -n 36415 ./train.txt.shuf > train.yn
$ head ./train.yn
ခင်ဗျား ဇနီး ဖြစ်မယ် ။	မင်း ရဲ့ ယောက်ျားလေး မိတ်ဆွေ က ဘယ်နှစ်ခါလောက် ဖုန်းဆက် တတ်သလဲ ။	0
အားပေး နေ မယ် ။	စောင့်မျှော် နေ မယ် နော် ။	0
ဒီထက်မက လှူနိုင်တန်းနိုင် ပါစေ	ဒီထက် လှူ နိုင် ဒီထက် ချမ်းသာ ပါစေ	1
ခင်ဗျား တို့ သူ တို့ ကို ဘယ်မှာ စောင့် ခဲ့ တာ လဲ ။	ခင်ဗျား က ကျွန်တော် တို့ ကို ဘယ် နေရာ မှာ စောင့် နေ တာ လဲ ။	0
သူ ပြော နေ တာ တွေ က အဲ လို လား ။	သူ ပြော နေ တာ တွေ ကြား မိ လား ။	0
သန်းခေါင်ကျော် မှ အိမ် ကို ဘာ လာ လုပ် တာ လဲ ။	သန်းခေါင်သန်းလွဲ မှ အိမ် ကို ဘာ လာ လုပ် တာ လဲ ။	1
ဒါဆို ဘာကြောင့် ခင်ဗျား ကိစ္စမပြတ် နိုင် သလဲ ဆိုတာ ကျွန်တော် နားမလည် နိုင်ဘူး ။	သူ ဒေါသတကြီး နဲ့ ကျွန်တော့် ကို မေးတယ် ။	0
ကိုယ် အလုပ် များ လို့ သတိမရ လိုက် ဘူး ။	ကိုယ် အလုပ် များ လို့ ပင်ပန်း နေ တယ် ။	0
ကောင်း လိုက် တဲ့ စာသား လေး	ကောင်း လိုက် တဲ့ စာသား တွေ ပါ လား	1
ရှိခိုး ပါ ၏ ဘုရား	ရှိခိုး ဦးတိုက် ပါ တယ်	1
```

train.yn ဖိုင်ထဲကနေ 1 or y or positive လေဘယ် ပါတဲ့ စာကြောင်းတွဲတွေကိုပဲ ဆွဲထုတ်ခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my3$ awk -F "[\t]" '$3 == "1" {print;}' ./train.yn > train.txt
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my3$ head train.txt
ဒီထက်မက လှူနိုင်တန်းနိုင် ပါစေ	ဒီထက် လှူ နိုင် ဒီထက် ချမ်းသာ ပါစေ	1
သန်းခေါင်ကျော် မှ အိမ် ကို ဘာ လာ လုပ် တာ လဲ ။	သန်းခေါင်သန်းလွဲ မှ အိမ် ကို ဘာ လာ လုပ် တာ လဲ ။	1
ကောင်း လိုက် တဲ့ စာသား လေး	ကောင်း လိုက် တဲ့ စာသား တွေ ပါ လား	1
ရှိခိုး ပါ ၏ ဘုရား	ရှိခိုး ဦးတိုက် ပါ တယ်	1
ကိုယ် လည်း လိုက် မယ် နော် ။	ကျွန်မ လည်း လိုက် မယ် နော် ။	1
သူ့ မျက်နှာသုန့် လို့ ဘာဖြစ် နေ လဲ မေး ဦး ။	သူ့ မျက်နှာ မ ကောင်း ဘူး ဘာဖြစ် နေ လဲ မေး ဦး ။	1
ဘာ တွေ ရှိ လို့ ဒီ လောက် မာန ကြီး နေ တာ လဲ ။	ဘာ တွေ ရှိ လို့ ဒီ လောက် စိတ် ကြီး ဝင်နေ တာ လဲ ။	1
ဝမ်းသာ စရာ ကောင်း ပါ တယ် သူ့ မှာ ကိုယ်ဝန်ရှိ နေ ပြီ လေ	ဝမ်းသာ စရာ ပါ သူ့ မှာ ကလေးရှိ နေ ပြီ	1
ဦးခိုက် ပါ ၏	ရှိခိုး ပူဇော် ပါ ၏	1
ငွေ တစ် ခု တည်း မ ကြည့် နဲ့	ငွေ နောက် ပဲ ကောက်ကောက် လိုက် နေ လို့ မ ရ ပါ ဘူး	1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my3$
```

manual-word အတွက် ပြင်ပြီးသွားပြီမို့ manual-word အတွက် အရင်ဆုံး စမ်း run ကြည့်မယ်။ အိုကေရင် syllable နဲ့ myWord အတွက် ဆက် run ကြည့်မယ်။  


### Manual-Word, word2vec

မ run ခင်မှာ လိုအပ်တဲ့ manual-word ဖိုင်တွေကို (ဒီတစ်ခါတော့ training က only positive label) experiment လုပ်မယ့် path အောက်ကို ကော်ပီကူးယူခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my3$ cp train.txt /home/ye/exp/myPara2/deep-siamese-text-similarity/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my3$ cp validation.txt0 /home/ye/exp/myPara2/deep-siamese-text-similarity/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my3$ cp open-test.final.manual /home/ye/exp/myPara2/deep-siamese-text-similarity/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my3$ cp closed-test /home/ye/exp/myPara2/deep-siamese-text-similarity/
```

training မလုပ်ခင်မှာ validation.txt0 ရဲ့ time-stamp ကို ကြိုမှတ်ထားခဲ့...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ ll validation.txt0 -h
-rw-rw-r-- 1 ye ye 813K စက်   17 17:12 validation.txt0
```

training...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-manual/all-para.word2vec --embedding_dim 500 --num_epochs 200 2>&1 | tee train-manual-only-positive-epoch200-w2v.17sept2021.log1
...
...
...
TRAIN 2021-09-17T17:39:46.564761: step 39399, loss 3.05481e-08, acc 1
(1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1) [0.00024865 0.0002466  0.00027224 0.00024572 0.00024855 0.00024488
 0.00024766 0.00024721 0.00024948 0.00024328 0.00024351 0.00025074
 0.0002478  0.00025212 0.00024574 0.00024964 0.0002552  0.00024587
 0.00024412 0.00025052 0.00024961 0.00024165 0.0002428  0.00025267
 0.00024398 0.00022844 0.00025545 0.00024173 0.00024751 0.00024321
 0.00026098 0.00024543 0.00024847 0.00024023 0.00024641 0.00024678
 0.00024533 0.00023933 0.00024738 0.0002454  0.00025541 0.00024143
 0.00024669 0.00024291 0.00024548 0.00024699 0.00024032 0.00025411
 0.00024528 0.00024482 0.00025943 0.0002474  0.00023909 0.00024442
 0.00024392 0.00025083 0.00025068 0.00024896 0.00024297 0.00024476
 0.00024731 0.00024893 0.00024602 0.00024437] [1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
TRAIN 2021-09-17T17:39:46.602548: step 39400, loss 2.98827e-08, acc 1
(1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1) [0.00024309 0.00024326 0.00024617 0.00024327 0.00024798 0.00024657
 0.00022552 0.00024243 0.0002439  0.00024508 0.00024084 0.00024378
 0.00024425 0.00024513 0.00024652 0.00024542 0.00025015 0.00028745
 0.00023983 0.00024876 0.00024366 0.00024354 0.00024649 0.00024516
 0.00025758 0.00024797 0.00024604 0.00021853 0.00024458 0.00024531
 0.00024567 0.00024418 0.00024477 0.00024508 0.00024197 0.00024472
 0.00024928 0.0002412  0.00023928 0.00023908 0.00024712 0.00024558
 0.00022134 0.00024482 0.00024461 0.00024224 0.00024842 0.00024513
 0.00023626 0.00024697 0.00024672 0.0002539  0.00024741 0.00023437
 0.00023487 0.00024628 0.00024363 0.00024572 0.00024528 0.00022636
 0.00025647 0.00024542 0.00024412 0.00024982] [1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]

real	22m7.099s
user	103m25.454s
sys	11m39.175s
```

လက်ရှိ training, validation ရလဒ်ကို ကြည့်လိုက်ရင် char mode ရဲ့ run တဲ့ ပုံစံနဲ့ မတူဘူး?! ငါမျှော်လင့်ခဲ့တာက word2vec ကိုသုံးထားပြီး char mode နဲ့ run ခဲ့သလို ရလဒ်ကောင်းချင်တာ... အခုက training/validation ရလဒ်တွေက တအားကောင်းနေတယ်?! အကောင်းလွန် နေတယ်...   
Evaluation with open test...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631873868/checkpoints/model-39000 --vocab_filepath ./runs/1631873868/checkpoints/vocab --eval_filepath ./open-test.final.manual
...
...
...
0.00016263683210127056
0.0001614336360944435
0.0001669142220634967
0.00016816060815472156
0.00016702391440048814
0.00016422268527094275
0.0001679160341154784
0.000170883780810982
0.0001652077044127509
0.00016829701780807227
0.00016728548507671803
0.0001456546742701903
Accuracy: 0.58959

real	0m6.342s
user	0m6.787s
sys	0m1.299s
```

closed-test နဲ့ စမ်းကြည့်ခဲ့...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631873868/checkpoints/model-39000 --vocab_filepath ./runs/1631873868/checkpoints/vocab --eval_filepath ./closed-test
...
...
...
0.00016925446107052267
0.00018451933283358812
0.00016786772175692022
0.00016849656822159886
0.00019232940394431353
0.00017138884868472815
0.0001668633340159431
0.0001695984392426908
0.0001692506775725633
0.00017815759929362684
0.00017650517111178488
0.00016840800526551902
0.00018453771190252155
0.00018454436212778091
Accuracy: 0.487

real	0m6.082s
user	0m6.783s
sys	0m1.306s
```

တစ်ခုခုတော့ လွဲနေပြီလား ?!...  

  
<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/train-manual-only-positive-epoch200-w2v.17sept2021-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/train-manual-only-positive-epoch200-w2v.17sept2021-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "Word Unit Segmented with myWord", char, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>  

ဒီ ဂရဖ်ကို ငါ မကြိုက်ဘူး...  ပြန်သုံးသပ်ရမယ်...   

ဖိုင်တွေကို ပြန်စစ်ကြည့်တော့ အထက်က preprocessing မှာ တစ်ခု အမှား လုပ်မိခဲ့တာကိုတော့ တွေ့သွားပြီ။  
validation.txt0 ရဲ့ format က train.txt ထဲကနေပဲ ငါက ယူထားခဲ့တာဆိုတော့ format က အောက်ပါအတိုင်း ရှိနေ....  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/media/ye/SP PHD U3/test-myWord/myWord-main/my-para/manual-my3$ head validation.txt0 
အရည်အသွေး ကောင်း လွန်း လို့ ဒီ ကျောက် က တန်ဖိုး ကြီး ပါ တယ်	အရည်အသွေး ကောင်း လွန်း လို့ ဒီ ကျောက် က ဈေးကြီး ပေး ရ ပါ တယ်	1
ဒီ ပုစ္ဆာ က တွက် ရ တာ လွယ် တယ် ။	ဒီ ပုစ္ဆာ က တွက် ရ တာ ခက်ခဲ လိုက် တာ ။	0
တစ်ချိန်လုံး ဆူဆူပူပူ လုပ် နေ တော့ ဘယ်သူ က ပျော် မှာ လဲ ။	တစ်ချိန်လုံး ပျော်ပျော်ရွှင်ရွှင် နေ ကြ တယ် မ ဆူပူ ကြ တော့ ဘူး ။	0
ကြိုးစား ကြ စမ်း ပါ ကွာ	ကြိုးစား ကြ ပါ ဦး	1
အဲ့ဒါ ကို တွက်ချက် လိုက်ပါ ။	သူ လိမ် ပြောတဲ့ အတွက် သူ့ ဖခင်က သူ့ကို ပြစ်တင်ကြိမ်းမောင်း လိမ့် မယ် ။	0
ကောင်လေးတွေ က ဟိုမှာ ပါ ။	ခင်ဗျား ဘောလ်ပင် ကို မ ကောက် ဘူး လား ။	0
ခင်ဗျား အသံ က အရမ်း ပျော် တတ် တဲ့ လူ တစ် ယောက် အသံ ပဲ ။	ခင်ဗျား အသံ က ပျော် တတ် တဲ့ လူ လို့ မ ထင် ရ ဘူး ။	0
ဒို့ မြန်မာ နိုင် ရ မည် ဟေ့	ဒို့ မြန်မာ ပဲ နိုင် ရ မှာ	1
ကလေး ကို ကြည့် ရ တာ ထွားကျိုင်း လိုက် တာ	ကလေး ရဲ့ အသား လေး ကို ကိုင်ကြည့် ပါ ဦး သန်မာ လိုက် တာ	1
ဟင့်အင်း ၊ သူ မရှိဘူး ။	သူတို့လေးတွေ ချစ်စရာကောင်းတာ အမှန်ဘဲ ။	0
```

တကယ် ရှိသင့်တာက label\<TAB\>string1\<TAB\>string2 ဆိုတဲ့ ပုံစံ ရှိရမယ်။ ဆိုလိုတာက test data နဲ့ format တူရမယ်။ မေ့သွားတာ...   
validation.txt0 ရဲ့ format ကို ပြန်ပြောင်းပြီး ထပ် training လုပ်ကြည်မယ်...  

training ထပ်လုပ်ကြည့်ခဲ့... training/validation graph က မကောင်းဘူး။  
char model run တာကို ငါကြည့်ခဲ့စဉ်က တိုက်တိုက်ဆိုင် head, tail က true တွေချည်းဖြစ်နေတာဖြစ်ရမယ်...  
ပုံမှန် training data ကိုပဲ char နဲ့ အစအဆုံး ပြန် run ကြည့်ပြီး confirmation လုပ်မယ်။   



## Experiment with Char Embedding  

ပြန် confirm လုပ်ကြည့်ချင်တယ်။ ပြီးတော့ input or training data ကို y only နဲ့ both y,n နဲ့ ပါ စမ်းကြည့်ချင်တယ်။  

ပထမဆုံး y,n နှစ်မျိုးလုံးနဲ့ training လုပ်ခဲ့...  (dumpValidation function ကို comment ပိတ်ထားခဲ့)

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --num_epochs 200 2>&1 | tee train-char-unit-both-yesno-label-17-char-embedding-sept2021.log1
...
...
...
TRAIN 2021-09-17T22:22:18.248597: step 113599, loss 0.00928952, acc 0.984375
(1, 1, 1, 1, 0, 0, 0, 0, 1, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 1, 1, 1, 1, 0, 1, 0, 0, 1, 0, 1, 1, 0, 1, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 1) [0.01583512 0.06545042 0.37487823 0.07334331 0.98481566 0.9740973
 0.974744   0.9652304  0.09076369 0.9896482  0.12312228 0.02727517
 0.98638755 0.04705433 0.08167117 0.97999895 0.9898183  0.97636753
 0.95561546 0.05246364 0.98295873 0.8372066  0.98276806 0.9833687
 0.9777756  0.093307   0.97506404 0.8909358  0.9865072  0.9115684
 0.09104723 0.9962457  0.9865118  0.03514251 0.2996722  0.03784204
 0.02731801 0.07383046 0.97171247 0.1874643  0.9962971  0.982813
 0.05788892 0.9276825  0.01508454 0.03422804 0.9770363  0.1244453
 0.44767073 0.9860132  0.02653803 0.11011203 0.98442316 0.33210924
 0.12903947 0.9484946  0.99129593 0.97842336 0.8778358  0.9797766
 0.1262571  0.24051821 0.9791967  0.03347741] [1. 1. 1. 1. 0. 0. 0. 0. 1. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 1. 0. 0. 0. 0.
 0. 1. 0. 0. 0. 0. 1. 0. 0. 1. 1. 1. 1. 1. 0. 1. 0. 0. 1. 0. 1. 1. 0. 1.
 1. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 0. 1. 1. 0. 1.]
TRAIN 2021-09-17T22:22:18.278195: step 113600, loss 0.00638196, acc 1
(0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1, 1, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0) [0.9676406  0.9735173  0.9864515  0.07358615 0.10179903 0.854159
 0.99009025 0.828539   0.9505731  0.9968247  0.19306809 0.87070763
 0.07031751 0.9572122  0.32572377 0.98357785 0.9852664  0.9476204
 0.08844588 0.6895189  0.9843316  0.07024514 0.2564101  0.15791814
 0.98962396 0.9902072  0.9165808  0.96080804 0.05438793 0.01829758
 0.97909534 0.9505146  0.9791351  0.81307983 0.01006282 0.03290852
 0.9836465  0.98008686 0.02286414 0.97633314 0.07824443 0.02048856
 0.05361512 0.9961693  0.01350765 0.2939456  0.9657806  0.14757979
 0.16511376 0.0479538  0.04747514 0.962947   0.98747456 0.8794633
 0.04419978 0.90134275 0.98610556 0.9122985  0.93501055 0.34254825
 0.02727869 0.9402128  0.9854962  0.8995379 ] [0. 0. 0. 1. 1. 0. 0. 0. 0. 0. 1. 0. 1. 0. 1. 0. 0. 0. 1. 0. 0. 1. 1. 1.
 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 1. 1. 0. 0. 1. 0. 1. 1. 1. 0. 1. 1. 0. 1.
 1. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 1. 1. 0. 0. 0.]

real	58m41.145s
user	287m43.696s
sys	34m48.652s
```

Evaluation with open test data

```
0.9655413031578064
0.4054034650325775
0.886533260345459
0.9968680143356323
0.9820180535316467
0.8720901012420654
0.97926926612854
0.9793165922164917
0.9786327481269836
0.93329918384552
0.9489979147911072
0.6613661646842957
0.9922716617584229
0.9060789346694946
Accuracy: 0.443443

real	0m7.625s
user	0m7.768s
sys	0m1.366s
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631888626/checkpoints/model-75000 --vocab_filepath ./runs/1631888626/checkpoints/vocab --eval_filepath ./open-test.final.manual
```

Evaluation with closed-test...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631888626/checkpoints/model-75000 --vocab_filepath ./runs/1631888626/checkpoints/vocab --eval_filepath ./closed-test
...
...
...
0.030810397118330002
0.9287165403366089
0.0818067416548729
0.10326208919286728
0.05379047617316246
0.9919763803482056
0.06349574029445648
0.44059285521507263
0.9803009033203125
0.8286778330802917
0.981559693813324
0.1632755994796753
0.04561747610569
0.02362591214478016
Accuracy: 0.941

real	0m7.306s
user	0m7.886s
sys	0m1.279s
```

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/train-char-unit-both-yesno-label-char-embedding-17Sept2021-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/train-char-unit-both-yesno-label-char-embedding-17Sept2021-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "Manual-Word", char, training with both yes-no label, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>  
  

ဒုတိယ experiment အနေနဲ့ y,n နှစ်မျိုးလုံးနဲ့ training လုပ်ခဲ့...  (dumpValidation function ကို သုံးခဲ့)

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --num_epochs 200 2>&1 | tee train-char-unit-both-yesno-label-char-embedding-sampling-17sept2021.log
TRAIN 2021-09-17T23:57:05.920913: step 113599, loss 0.0162398, acc 0.953125
(1, 1, 1, 1, 0, 0, 0, 0, 1, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 1, 1, 1, 1, 0, 1, 0, 0, 1, 0, 1, 1, 0, 1, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 1) [0.02081363 0.03449002 0.82673    0.09592614 0.9982565  0.98387957
 0.9996308  0.9961138  0.10704955 0.9996726  0.06616928 0.03162305
 0.9549085  0.0188218  0.01711525 0.9996527  0.999814   0.9025748
 0.9998829  0.03703678 0.9998511  0.9595919  0.99452    0.9202664
 0.999416   0.1056829  0.93871397 0.41157252 0.9938623  0.97253543
 0.05765578 0.9986325  0.99972    0.11090621 0.2526931  0.06680547
 0.05833242 0.03654693 0.9957481  0.10322494 0.9985233  0.99978423
 0.09156062 0.9996627  0.01227115 0.04067817 0.9280618  0.11467165
 0.42437798 0.9993128  0.03402987 0.04864617 0.99811167 0.24129371
 0.03925733 0.9993104  0.9292444  0.9375286  0.923653   0.99985147
 0.12542243 0.25134814 0.9929733  0.03702257] [1. 1. 0. 1. 0. 0. 0. 0. 1. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 1. 0. 0. 0. 0.
 0. 1. 0. 1. 0. 0. 1. 0. 0. 1. 1. 1. 1. 1. 0. 1. 0. 0. 1. 0. 1. 1. 0. 1.
 1. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 0. 1. 1. 0. 1.]
TRAIN 2021-09-17T23:57:05.949352: step 113600, loss 0.0126378, acc 0.96875
(0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1, 1, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0) [0.99626815 0.9919621  0.986952   0.04145057 0.1027806  0.9858794
 0.88951945 0.9483123  0.95531964 0.9834236  0.25624168 0.9172375
 0.0216     0.8799821  0.3487399  0.99979377 0.99921197 0.9589786
 0.08500715 0.42028752 0.9997605  0.01462506 0.28582984 0.15615787
 0.9015118  0.9997736  0.9993481  0.8619546  0.06575771 0.01073423
 0.9926888  0.9998429  0.99931574 0.956278   0.02624244 0.11792202
 0.99992424 0.99959815 0.03039122 0.99955136 0.04039368 0.01261356
 0.09214533 0.895682   0.02944429 0.26197252 0.9999166  0.05360898
 0.46668753 0.14071992 0.0560796  0.9633307  0.99469745 0.9406887
 0.07704298 0.8803524  0.9843426  0.8371126  0.9596928  0.6989547
 0.01665139 0.9998339  0.9982314  0.98731333] [0. 0. 0. 1. 1. 0. 0. 0. 0. 0. 1. 0. 1. 0. 1. 0. 0. 0. 1. 1. 0. 1. 1. 1.
 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 1. 1. 0. 0. 1. 0. 1. 1. 1. 0. 1. 1. 0. 1.
 1. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0.]

real	58m19.037s
user	286m39.591s
sys	34m49.366s
```

Evaluation with open test...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631894336/checkpoints/model-112000 --vocab_filepath ./runs/1631894336/checkpoints/vocab --eval_filepath ./open-test.final.manual
...
...
...
0.9996175765991211
0.9957304000854492
0.9979681372642517
0.9912671446800232
0.9929057359695435
0.9039397239685059
0.9628039598464966
0.3023703396320343
0.999755859375
0.9968329668045044
0.9972761273384094
0.9998899102210999
0.9995104670524597
0.9931474924087524
0.9576190710067749
0.9842780232429504
0.9990139603614807
Accuracy: 0.442442

real	0m7.648s
user	0m7.691s
sys	0m1.471s
```

Evaluation with closed test...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631894336/checkpoints/model-112000 --vocab_filepath ./runs/1631894336/checkpoints/vocab --eval_filepath ./closed-test
...
...
...
0.9005180597305298
0.08478938788175583
0.9961918592453003
0.11164321005344391
0.9996281266212463
0.04861947521567345
0.9683501720428467
0.0714702308177948
0.06173016130924225
0.04371044412255287
0.9674890041351318
0.05456890910863876
0.5070134997367859
0.9997949004173279
0.9545276761054993
0.9997859597206116
0.21628829836845398
0.04192781075835228
0.06079230457544327
Accuracy: 0.933

real	0m7.424s
user	0m7.803s
sys	0m1.298s
```

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/train-char-unit-both-yesno-label-char-embedding-sampling-17sept2021-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/train-char-unit-both-yesno-label-char-embedding-sampling-17sept2021-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "Manual-Word", char, training with both yes-no label, allow sampling, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>  


## Summary of Experiments

အထက်မှာ အမျိုးမျိုး Experiment လုပ်ခဲ့တာတွေထဲက သုံးလို့ ရနိုင်တဲ့ ရလဒ်တွေကို summary လုပ်ကြည့်ရင် အောက်ပါအတိုင်း ရခဲ့တယ်...  

|Method|Closed-test|open test|  
|:-------|------------:|----------:|
|Manual (word2vec)| **0.969**| **0.447447**|  
|Syllable (word2vec)| 0.964| 0.44044|  
|Word (word2vec)| 0.96| 0.444444|  
|Manual (char-embedding)| 0.941| 0.437437|  
|Syllable(char-embedding)| 0.922| 0.428428|  
|Word (char-embedding)| 0.932| 0.437437|  

အောက်ပါ အချက်တွေ တွေ့ရ  
- word2vec က char-embedding ထက် ရလဒ် ပိုကောင်းတယ်
- closed-test မှာ ရလဒ်တွေက 0.969 အထိ ရပေမဲ့၊ open test မှာတော့ 0.447 က အများဆုံးပဲ

 
  
## Thinking

လက်ရှိ အချိန်ထိ run ခဲ့တဲ့ အခြေအနေပေါ်ကို မူတည်ပြီးတော့ ရလဒ်ပိုကောင်းလာနိုင်မယ့် သို့မဟုတ် လုပ်လို့ ရမယ့် training ကို စဉ်းစားကြည့်ရင်...  
  
- တကယ်လို့ ရလဒ်က မကောင်းရင် training လုပ်တဲ့ ပုံစံကို ပထမဆုံး run ခဲ့တဲ့ char မှာလုပ်ခဲ့သလိုပဲ...  training ကို paraphrase စာကြောင်းတွေနဲ့ပဲ ပြင်ထားတဲ့ training data ကို သုံးပြီးတော့ validation, testing ကိုပဲ para+no-para ရောထားတဲ့ ဒေတာနဲ့ လုပ်သွားတဲ့ ပုံစံနဲ့ ဆိုရင်ကော... ?!
- fasttext   (လောလောဆယ် run ကြည့်တော့ error တက်နေတယ်... embedding အပိုင်းကို ပြင်ရေးရမယ်)
- universal sentence ကို သုံးကြည့်ရမလား?!  
- လက်ရှိ wordvec က မြန်မာစာ paraphrase ဒေတာနဲ့ပဲ ဆောက်ထားတာ အဲဒါကြောင့် word2vec အနေနဲ့ ကြည့်မယ်ဆိုရင် language model နဲ့ တူလို့ data များများနဲ့ ဆောက်ဖို့လိုအပ်တယ်။ myWord data ပါ ပေါင်းပြီး word2vec ဆောက်ပြီး run ရင်တော့ theory အရ ရလဒ်က ပိုကောင်းလာနိုင်တယ်...  

## Embedding with FastText

ပထမ စ run တော့ပေးနေတဲ့ error က အောက်ပါအတိုင်း...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-manual/all-para.fasttext.vector --embedding_dim 500 --num_epochs 200 2>&1 | tee train-manual-epoch200-fasttext.18sept2021.log1
2021-09-18 03:18:40.025300: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.1 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-18 03:18:40.025320: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.2 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-18 03:18:40.025323: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX instructions, but these are available on your machine and could speed up CPU computations.
2021-09-18 03:18:40.025325: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX2 instructions, but these are available on your machine and could speed up CPU computations.
2021-09-18 03:18:40.025327: W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use FMA instructions, but these are available on your machine and could speed up CPU computations.
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
EMBEDDING_DIM=500
EVALUATE_EVERY=1000
HIDDEN_UNITS=50
IS_CHAR_BASED=False
L2_REG_LAMBDA=0.0
LOG_DEVICE_PLACEMENT=False
NUM_EPOCHS=200
TRAINING_FILES=train.txt
WORD2VEC_FORMAT=text
WORD2VEC_MODEL=./w2v_fasttext/mypara-manual/all-para.fasttext.vector

Loading training data from train.txt
Building vocabulary
Length of loaded vocabulary =1141
dumping validation 0
Train/Dev split for train.txt: 36414/4047
Loading W2V data...
loaded word2vec len  5590
starting graph def
started session
Tensor("embedding/embedding_lookup:0", shape=(?, 15, 500), dtype=float32)
initialized siameseModel object
defined training_ops
defined gradient summaries
Writing to /home/ye/exp/myPara2/deep-siamese-text-similarity/runs/1631909923

init all variables
initializing initW with pre-trained word2vec embeddings
Traceback (most recent call last):
  File "./train.py", line 180, in <module>
    arr=inpH.pre_emb["zero"]
KeyError: 'zero'

real	0m9.696s
user	0m9.723s
sys	0m1.212s
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$
```

train.py ဖိုင်ကို ဝင်စစ်ပြီး print ထုတ်ကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရ...  

```
Error ဖြစ်တာကိုတော့ တွေ့သွားပြီ...  

w: apple
s: apple
w: အရည
s: 
w: အသ
s: 
w: covid
s: covid
w: 19
s: 19
Traceback (most recent call last):
  File "./train.py", line 180, in <module>
    arr=inpH.pre_emb["zero"]
KeyError: 'zero'

real	0m9.601s
user	0m9.494s
sys	0m1.273s
```

စာကြောင်းထဲမှာ နံပါတ်ပါရင် zero လုပ်ထားတာကိုတွေ့ရ...  
အဲဒါကြောင့် အောက်ပါအတိုင်း train.py ဖိုင်ရဲ့ coding ကို ဝင်ပြင်တော့ fasttext vector နဲ့ run လို့ ရသွားခဲ့...  

```python
        for w in vocab_processor.vocabulary_._mapping:
            arr=[]
            #print("w:", w)
            s = re.sub('[^0-9a-zA-Z]+', '', w)
            #print("s:", s)            
            #s = re.sub('[၊။]', '', w)
            if w in inpH.pre_emb:
                arr=inpH.pre_emb[w]
            elif w.lower() in inpH.pre_emb:
                arr=inpH.pre_emb[w.lower()]
            elif s in inpH.pre_emb:
                arr=inpH.pre_emb[s]
#            elif s.isdigit():
#                arr=inpH.pre_emb["zero"]
```

### with manual word
ပထမဆုံး manual word နဲ့ စ run ခဲ့...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-manual/all-para.fasttext.vector --embedding_dim 500 --num_epochs 200 2>&1 | tee train-manual-epoch200-fasttext.18sept2021.log1
...
...
...
TRAIN 2021-09-18T04:28:12.625177: step 113598, loss 0.0117705, acc 0.96875
(0, 0, 1, 0, 0, 0, 1, 1, 1, 1, 0, 0, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 1, 1, 1, 0, 0, 1, 0, 0, 1, 1, 0, 1, 0, 1, 0, 1, 0, 1, 1, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 1) [0.96330327 0.9897576  0.03248395 0.87518585 0.9602844  0.9892118
 0.02200038 0.01657733 0.06715383 0.03885545 0.8360112  0.89606434
 0.9144302  0.01893772 0.2390241  0.99429023 0.40074584 0.02470012
 0.98928285 0.9917732  0.9804681  0.9572804  0.9833475  0.02146463
 0.982263   0.01153532 0.9130529  0.9134238  0.34108347 0.9927607
 0.0270608  0.92322975 0.04178759 0.05246258 0.10937169 0.02129744
 0.8475863  0.99147683 0.01814317 0.9900588  0.18709005 0.01207976
 0.01405868 0.84859973 0.15559523 0.9372698  0.13935675 0.919362
 0.0398486  0.9254618  0.01362888 0.0340601  0.00752221 0.9903806
 0.9906022  0.8827947  0.03947177 0.99158543 0.76256603 0.0252838
 0.9519909  0.8841865  0.01419877 0.01819706] [0. 0. 1. 0. 0. 0. 1. 1. 1. 1. 0. 0. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 0. 1.
 0. 1. 0. 0. 1. 0. 1. 0. 1. 1. 1. 1. 0. 0. 1. 0. 1. 1. 1. 0. 1. 0. 1. 0.
 1. 0. 1. 1. 1. 0. 0. 0. 1. 0. 0. 1. 0. 0. 1. 1.]
TRAIN 2021-09-18T04:28:12.660875: step 113599, loss 0.00394277, acc 1
(0, 0, 1, 1, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 1, 0, 0, 1, 1, 0, 1, 0, 0, 0, 1, 1, 1, 0, 1, 1, 1, 0, 1, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0) [0.9465181  0.9927966  0.04634272 0.1351826  0.05867341 0.84448636
 0.12367037 0.98070955 0.9781645  0.03462579 0.9382891  0.9967606
 0.85604125 0.994116   0.9909656  0.98437864 0.9945791  0.34562686
 0.03253374 0.8408504  0.98860246 0.990277   0.98872405 0.7977991
 0.84663516 0.9892206  0.93669087 0.95425355 0.01060134 0.04627833
 0.99059206 0.82678944 0.05680316 0.9765498  0.01011628 0.01370191
 0.8976815  0.985971   0.11559405 0.27936274 0.87047416 0.10465913
 0.98961645 0.9456868  0.9718608  0.0984633  0.01084607 0.02197323
 0.91211236 0.01517926 0.01176044 0.00853918 0.98829323 0.00811042
 0.98910254 0.00444985 0.03033165 0.9427287  0.9896305  0.9899108
 0.990984   0.9676688  0.9879092  0.9915178 ] [0. 0. 1. 1. 1. 0. 1. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 1. 1. 0. 0. 1. 0. 1. 1. 0. 0. 1. 1. 0. 1. 0. 0. 0. 1. 1. 1.
 0. 1. 1. 1. 0. 1. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0.]
TRAIN 2021-09-18T04:28:12.693494: step 113600, loss 0.00344966, acc 1
(1, 0, 0, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 1, 0, 1, 0, 1) [0.04881577 0.7519182  0.98596644 0.83828145 0.9642996  0.03056869
 0.04174186 0.98906946 0.8289109  0.03660227 0.01602329 0.04754157
 0.96371675 0.7958222  0.95542586 0.02174286 0.01397285 0.72020644
 0.8920336  0.9789656  0.02261902 0.9777455  0.9883589  0.9325011
 0.9893896  0.02545586 0.99029976 0.9918712  0.9871542  0.9141936
 0.92663646 0.9961489  0.93387    0.0167546  0.8937534  0.98899776
 0.96096313 0.946808   0.99239075 0.06863283 0.889855   0.07105798
 0.17116182 0.03441466 0.02929268 0.0520981  0.0488636  0.97301245
 0.9805799  0.99347913 0.99414337 0.07184369 0.01244048 0.99182755
 0.99462944 0.9580038  0.9732214  0.92741865 0.20374665 0.11401034
 0.9811393  0.02641292 0.98182744 0.09720048] [1. 0. 0. 0. 0. 1. 1. 0. 0. 1. 1. 1. 0. 0. 0. 1. 1. 0. 0. 0. 1. 0. 0. 0.
 0. 1. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 0. 1. 1. 1. 1. 1. 1. 0.
 0. 0. 0. 1. 1. 0. 0. 0. 0. 0. 1. 1. 0. 1. 0. 1.]

real	67m19.544s
user	303m38.149s
sys	36m1.240s
```

Evaluation with open test...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631910061/checkpoints/model-74000 --vocab_filepath ./runs/1631910061/checkpoints/vocab --eval_filepath ./open-test.final.manual
...
...
...
0.9507440328598022
0.9617266058921814
0.24795784056186676
0.6320780515670776
0.016683245077729225
0.9772344827651978
0.9840661287307739
0.8515365123748779
0.943259596824646
0.9835275411605835
0.981746256351471
0.9879975914955139
0.9781875014305115
0.9695249795913696
0.9891492128372192
0.2674834132194519
Accuracy: 0.439439

real	0m6.551s
user	0m6.976s
sys	0m1.190s
```

Evaluation with closed test...

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631910061/checkpoints/model-74000 --vocab_filepath ./runs/1631910061/checkpoints/vocab --eval_filepath ./closed-test
...
...
...
0.9872598052024841
0.02754240483045578
0.08470219373703003
0.9896406531333923
0.7571049928665161
0.9871442317962646
0.8559340834617615
0.016688302159309387
0.02593778818845749
Accuracy: 0.965

real	0m6.234s
user	0m6.991s
sys	0m1.231s
```

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/manual-word-200epoch-fasttext-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/manual-word-200epoch-fasttext-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "Manual-Word", fasttext, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>  

### with syllable

training...  
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-syl/all-para.fasttext.vector --embedding_dim 500 --num_epochs 200 2>&1 | tee train-syl-epoch200-fasttext.18sept2021.log1
...
...
...
 [1. 1. 1. 0. 1. 0. 0. 1. 0. 1. 1. 0. 0. 0. 0. 0. 1. 0. 1. 1. 0. 0. 1. 1.
 0. 0. 0. 1. 1. 0. 0. 0. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 1. 0. 0. 0.
 1. 0. 1. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 1. 0. 0.]
TRAIN 2021-09-18T05:58:39.531721: step 113600, loss 0.00447952, acc 0.984375
(0, 1, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 1, 0, 0, 0, 1, 1, 1, 0, 0, 1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 0) [0.98402315 0.00180838 0.01070712 0.0154055  0.98705846 0.9853515
 0.95092505 0.02980232 0.99272627 0.98217225 0.94084054 0.98908705
 0.00423985 0.96129864 0.98890257 0.96572787 0.98351836 0.01490581
 0.98165065 0.03652248 0.9688797  0.5547371  0.964869   0.93653595
 0.09941081 0.9785712  0.02613369 0.9069237  0.9493511  0.34883094
 0.04002983 0.97117645 0.87285954 0.9725491  0.03783482 0.02630803
 0.06692225 0.9041588  0.98872745 0.03097629 0.06559272 0.9921083
 0.9481784  0.02409441 0.96886575 0.01070136 0.9915045  0.97494423
 0.01829547 0.9943721  0.9853153  0.02161155 0.9348786  0.99144703
 0.98526984 0.12195244 0.9571868  0.04699932 0.8520498  0.02437799
 0.99258953 0.04464612 0.9140488  0.98703146] [0. 1. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 1. 0. 0. 0. 0. 1. 0. 1. 0. 0. 0. 0.
 1. 0. 1. 0. 0. 1. 1. 0. 0. 0. 1. 1. 1. 0. 0. 1. 1. 0. 0. 1. 0. 1. 0. 0.
 1. 0. 0. 1. 0. 0. 0. 1. 0. 1. 0. 1. 0. 1. 0. 0.]

real	63m41.558s
user	300m25.522s
sys	37m9.517s
```

Evaluation with open test...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631915705/checkpoints/model-23000 --vocab_filepath ./runs/1631915705/checkpoints/vocab --eval_filepath ./open-test.final.manual.syl 
...
...
...
0.9436487555503845
0.5453405380249023
0.9636836647987366
0.9735085368156433
0.8837988376617432
0.9472755789756775
0.9272462129592896
0.9751208424568176
0.812988817691803
Accuracy: 0.458458

real	0m6.057s
user	0m6.904s
sys	0m1.157s
```

Evaluation with closed test...

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631915705/checkpoints/model-23000 --vocab_filepath ./runs/1631915705/checkpoints/vocab --eval_filepath ./closed-test.syl 
...
...
0.08440058678388596
0.6090917587280273
0.017645984888076782
0.2214645892381668
0.05666700750589371
0.8263212442398071
0.138916477560997
0.32509809732437134
0.8845736980438232
0.7855257987976074
0.8029919862747192
0.16575828194618225
0.1529986411333084
0.021857550367712975
Accuracy: 0.935

real	0m6.085s
user	0m6.777s
sys	0m1.282s
```

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/syllable-200epoch-fasttext-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/syllable-200epoch-fasttext-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "Syllable", fasttext, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>  
  

### with myWord-Word

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-word/all-para.fasttext.vector --embedding_dim 500 --num_epochs 200 2>&1 | tee train-myWord-epoch200-fasttext.18sept2021.log1
...
...
...
TRAIN 2021-09-18T08:03:55.987094: step 113599, loss 0.00793565, acc 0.984375
(0, 1, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 1, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 1, 0, 1, 1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 1) [0.82764393 0.03556161 0.02789695 0.99163294 0.97693527 0.9539127
 0.02244745 0.9932332  0.95334905 0.02169408 0.99329734 0.80185753
 0.02667648 0.9936891  0.8925737  0.996175   0.02180221 0.04734171
 0.9634545  0.943511   0.12730259 0.03243406 0.98198503 0.9935275
 0.05879339 0.11034941 0.01933953 0.04633586 0.9902289  0.9437852
 0.9340833  0.98713166 0.9936486  0.9499433  0.92865956 0.97957975
 0.9893893  0.9957551  0.88447046 0.02398767 0.9939847  0.09456157
 0.9941129  0.01157092 0.01559823 0.9839165  0.01484902 0.02442652
 0.96511036 0.07712807 0.9056795  0.8848276  0.98618144 0.9912563
 0.03232694 0.91025984 0.94287425 0.99019814 0.93301797 0.987511
 0.01330403 0.0414805  0.9421609  0.07767771] [0. 1. 1. 0. 0. 0. 1. 0. 0. 1. 0. 0. 1. 0. 0. 0. 1. 1. 0. 0. 1. 1. 0. 0.
 1. 1. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0. 1. 1. 0. 1. 1.
 0. 1. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 1. 0. 1.]
TRAIN 2021-09-18T08:03:56.019713: step 113600, loss 0.00688716, acc 0.984375
(1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 1, 1, 0, 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 1) [0.01434837 0.01653426 0.9923921  0.9909915  0.99146897 0.00673319
 0.9948768  0.88798946 0.98213786 0.9887646  0.03249896 0.01965207
 0.0247782  0.9930346  0.02923042 0.04901762 0.9260369  0.01213083
 0.02076924 0.1848216  0.15186372 0.06963076 0.98957896 0.9931711
 0.14079256 0.9923005  0.01027369 0.02117962 0.07929119 0.99123794
 0.9906705  0.9817085  0.05727641 0.98987967 0.90546757 0.9916885
 0.8754084  0.00629362 0.01937794 0.8383126  0.87017554 0.93303996
 0.0985159  0.9679212  0.95394295 0.96070194 0.9919226  0.02892021
 0.99173665 0.9440813  0.08768374 0.98349965 0.99369156 0.01015645
 0.9680928  0.9930324  0.9906569  0.9955355  0.17570198 0.9863978
 0.03614085 0.9907422  0.97773033 0.00789372] [1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 1. 1. 1. 0. 1. 1. 0. 1. 1. 1. 1. 1. 0. 0.
 1. 0. 1. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 1.
 0. 0. 1. 0. 0. 1. 0. 0. 0. 0. 1. 0. 1. 0. 0. 1.]

real	63m0.563s
user	300m16.738s
sys	35m20.849s
```

Evaluation with open test...   

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631923263/checkpoints/model-25000 --vocab_filepath ./runs/1631923263/checkpoints/vocab --eval_filepath ./open-test.final.manual.word 
...
...
...
0.9543828964233398
0.29838594794273376
0.8570796847343445
0.9770405888557434
0.9763622283935547
0.9702016115188599
0.971348762512207
0.9883525371551514
0.9759397506713867
0.9921869039535522
0.8496887683868408
Accuracy: 0.488488

real	0m6.365s
user	0m7.122s
sys	0m1.215s
```

Evaluation with closed test...  
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631923263/checkpoints/model-25000 --vocab_filepath ./runs/1631923263/checkpoints/vocab --eval_filepath ./closed-test.word 
...
...
...
0.7471199035644531
0.07436402142047882
0.9202162623405457
0.05158622935414314
0.974510133266449
0.1326059103012085
0.9690447449684143
0.026856355369091034
0.08524863421916962
0.3267844319343567
0.9688017964363098
0.09938966482877731
0.2276495099067688
0.8332359194755554
0.8445929288864136
0.9091323614120483
0.09535416215658188
0.04002465307712555
0.022362658753991127
Accuracy: 0.94

real	0m6.529s
user	0m6.944s
sys	0m1.237s
```

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-200epoch-fasttext-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-200epoch-fasttext-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "myWord-word", fasttext, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>  

--------------

လက်ရှိအချိန်ထိ ရလဒ်တွေကို ပြန် သုံးသပ်နိုင်ဖို့ အထက်မှာ ဆောက်ခဲ့တဲ့ ရလဒ်ဇယားကို update လုပ်ခဲ့တယ်။  

|Method|Closed-test|open test|  
|:-------|------------:|----------:|
|Manual (word2vec)| **0.969**| 0.447447|  
|Syllable (word2vec)| 0.964| 0.44044|  
|Word (word2vec)| 0.96| 0.444444|  
|Manual (char-embedding)| 0.941| 0.437437|  
|Syllable(char-embedding)| 0.922| 0.428428|  
|Word (char-embedding)| 0.932| 0.437437|  
|Manual (fasttext embedding)| 0.965 | 0.439439 |
|Syllable (fasttext embedding)|0.935 | 0.458458 |
|Word (fasttext embedding)|0.94 | **0.488488** |


- open test နဲ့မှာ fasttext နဲ့ရတဲ့ Accuracy: 48 က အများဆုံးလို့ ထင်တယ်။
- universal sentence နဲ့ run လိုရအောင် ပြင်ကြည့်ပြီး run ကြည့်ရန်
- လက်ရှိ သုံးနေတဲ့ Siamese Network ကို parameter tuning လုပ်ကြည့်ရန်...  အလွယ်ဆုံးကတော့ batch size ကို ကစားကြည့်တာ...  hidden unit, max_document_length=15
- Distance ကို ပြောင်းတဲ့ ကိစ္စ ရနိုင်မလား?!
- word2vec, fasttext ကို မော်ဒယ် အကြီးကြီးနဲ့ ဆောက်ကြည့်ပြီးတော့ အဲဒါနဲ့ paraphrase classification လုပ်ကြည့်ရင်ကော...?! 
(ဒါကတော့ လုပ်နိုင်တယ်)

----------------------

လက်ရှိ myWord-200epoch-fasttext က open-test နဲ့မှာ အကောင်းဆုံး ရလဒ်ကို ပေးတာမို့ အဲဒီ မော်ဒယ်ကိုပဲ parameter tuning လုပ်ကြည့်မယ်...  
max_document_length ကို နဂို author က ထားထားတဲ့ 15 ကနေ 30 အထိ ကစားကြည့်ခဲ့...  

```python
max_document_length= 30 # 15 (original setting)
```

ဘာကြောင့်လဲ ဆိုတော့ အဲဒီ max_document_length ဆိုတာက ခေါ်သုံးထားတဲ့ မော်ဒယ် setting မှာ အောက်ပါအတိုင်း sequence length ဆိုတာကို တွေ့ရလို့...  
သိတဲ့အတိုင်း sequene length ကလည်း LSTM မှာ အရေးကြီးတယ်လေ...  

```python
            siameseModel = SiameseLSTMw2v(
                sequence_length=max_document_length,
                vocab_size=len(vocab_processor.vocabulary_),
                embedding_size=FLAGS.embedding_dim,
                hidden_units=FLAGS.hidden_units,
                l2_reg_lambda=FLAGS.l2_reg_lambda,
                batch_size=FLAGS.batch_size,
                trainableEmbeddings=trainableEmbeddings
            )
```

Training...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-word/all-para.fasttext.vector --embedding_dim 500 --num_epochs 200 2>&1 | tee train-myWord-epoch200-fasttext-max-doc-length30.18sept2021.log
...
...
...
TRAIN 2021-09-18T13:01:12.629787: step 113599, loss 0.00746483, acc 0.96875
(0, 1, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 1, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 1, 0, 1, 1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 1) [0.92624086 0.01805103 0.02975548 0.9999996  0.99974865 0.97255623
 0.00431878 0.8791241  0.8657474  0.00779783 0.99999857 0.9999856
 0.0170119  0.99492633 0.01417147 0.9467506  0.00785836 0.03103591
 0.9999893  0.9894357  0.04877776 0.12333237 0.99999696 0.99372876
 0.00837848 0.5674289  0.05084061 0.02308893 0.84453577 0.94361484
 0.94509786 0.995537   0.89373064 0.93880534 0.96907246 0.9998304
 0.9999997  0.85306334 0.90601975 0.07775357 0.9949044  0.10171027
 0.9948656  0.0041138  0.00520389 0.99851644 0.01871002 0.0085987
 0.91654474 0.01629934 0.92316455 0.9457384  0.95441914 0.9999999
 0.0072884  0.9973446  0.9992435  0.8981512  0.34368148 0.9932806
 0.02914722 0.08751538 0.94355834 0.05746603] [0. 1. 1. 0. 0. 0. 1. 0. 0. 1. 0. 0. 1. 0. 1. 0. 1. 1. 0. 0. 1. 1. 0. 0.
 1. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0. 1. 1. 0. 1. 1.
 0. 1. 0. 0. 0. 0. 1. 0. 0. 0. 1. 0. 1. 1. 0. 1.]
TRAIN 2021-09-18T13:01:12.692920: step 113600, loss 0.0134646, acc 0.96875
(1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 1, 1, 0, 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 1) [0.07296225 0.01897413 0.9999999  0.9990921  0.9939167  0.00918471
 0.83494526 0.91333646 0.99990577 0.9999996  0.00511401 0.02215979
 0.01287346 0.9300575  0.0124837  0.06613448 0.92949784 0.0326583
 0.5767586  0.105673   0.0230297  0.01420715 0.83782053 0.7262092
 0.01155026 0.9999999  0.02192598 0.05949882 0.05879025 0.9999952
 0.99997276 0.9414     0.45732307 0.9916099  0.9013649  0.8095589
 0.9905467  0.01032792 0.00418146 0.9999994  0.9868192  0.73679656
 0.01711435 0.94987375 0.9712678  0.99998623 0.9999885  0.0462269
 0.9999962  0.9647083  0.20447707 0.9894155  0.8792689  0.00626593
 0.99999124 0.999994   0.9961439  0.9895958  0.10424    0.8786488
 0.02196177 0.99959594 0.91943884 0.01193227] [1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 1. 1. 1. 0. 1. 1. 0. 1. 0. 1. 1. 1. 0. 0.
 1. 0. 1. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 1.
 0. 0. 1. 0. 0. 1. 0. 0. 0. 0. 1. 0. 1. 0. 0. 1.]

real	118m52.270s
user	574m49.760s
sys	72m0.524s
```

Evaluation with open test data...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631937752/checkpoints/model-71000 --vocab_filepath ./runs/1631937752/checkpoints/vocab --eval_filepath ./open-test.final.manual.word 
...
...
...
0.28249916434288025
0.9759529232978821
0.04650973901152611
0.8494864106178284
0.9016193151473999
0.9893068671226501
0.9910531640052795
0.9620731472969055
0.9922521710395813
0.9402870535850525
0.9999063014984131
0.99468994140625
0.9999648928642273
0.20834650099277496
Accuracy: 0.474474

real	0m10.578s
user	0m11.288s
sys	0m1.423s
```

Evaluation with closed test data...

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631937752/checkpoints/model-71000 --vocab_filepath ./runs/1631937752/checkpoints/vocab --eval_filepath ./closed-test.word 
...
...
...
0.13001085817813873
0.03301911801099777
0.9999862313270569
0.023909352719783783
0.04856507107615471
0.9843346476554871
0.8013219833374023
0.9865438938140869
0.022901752963662148
0.02608126774430275
0.019091874361038208
Accuracy: 0.95

real	0m10.110s
user	0m11.129s
sys	0m1.209s
```

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-200epoch-fasttext-max_document_length30-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-200epoch-fasttext-max_document_length30-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "myWord-word", fasttext, max_document_length=30, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>  
  
## Playing with Batch Size (32, 16, 128, 8)  

### Training and Evaluation with Batch Size 32

ဒီ တစ်ခါ Batch Size ကို 32 ထားပြီး run ကြည့်မယ်...  
default က 64 မို့လို့...  

```python
  --batch_size BATCH_SIZE
                        Batch Size (default: 64)
```

Training...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-word/all-para.fasttext.vector --embedding_dim 500 --num_epochs 200 --batch_size 32 2>&1 | tee train-myWord-epoch200-fasttext-max-doc-length14-batch_size32.18sept2021.log
...
...
...
TRAIN 2021-09-18T16:19:11.458035: step 227398, loss 0.00352363, acc 1
(1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0) [0.02403889 0.03176647 0.87205195 0.92525536 0.9969638  0.02394373
 0.9920563  0.9904885  0.9876254  0.94473547 0.9852069  0.00982478
 0.8949047  0.9602766  0.00804671 0.97471666 0.9632204  0.9190069
 0.24604355 0.9909947  0.85339123 0.8582644  0.9864661  0.01477041
 0.0346037  0.98619115 0.00882425 0.04613937 0.84483206 0.9704118
 0.78715104 0.99619526] [1. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 1. 0. 0. 0. 1. 0. 0. 0. 0. 1.
 1. 0. 1. 1. 0. 0. 0. 0.]
TRAIN 2021-09-18T16:19:11.482025: step 227399, loss 0.0128122, acc 0.96875
(0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 0) [0.9978148  0.9965245  0.97438765 0.9292312  0.6161585  0.20763494
 0.6639417  0.9981818  0.9242246  0.9807221  0.91263074 0.8772597
 0.09045552 0.94843405 0.98379785 0.0315199  0.00575078 0.98440033
 0.0289392  0.84323245 0.98678446 0.98094934 0.9925442  0.03066472
 0.01921155 0.913031   0.9033415  0.97622824 0.00129642 0.68945867
 0.98128664 0.9835823 ] [0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 1. 0. 1. 0. 0. 0. 0. 1.
 1. 0. 0. 0. 1. 0. 0. 0.]
TRAIN 2021-09-18T16:19:11.506678: step 227400, loss 0.00220552, acc 1
(0, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 1, 1, 0, 1, 0, 1, 1) [0.9973903  0.03724901 0.99495596 0.23391274 0.0321546  0.02022237
 0.9308554  0.01154507 0.05858197 0.99165326 0.0257774  0.9980095
 0.88196665 0.08046707 0.98483795 0.9900811  0.07103508 0.96788657
 0.03840635 0.9151216  0.98907954 0.9859412  0.9656631  0.9859979
 0.9893176  0.02294798 0.10577742 0.97785014 0.04226098 0.97624576
 0.14351536 0.04517284] [0. 1. 0. 1. 1. 1. 0. 1. 1. 0. 1. 0. 0. 1. 0. 0. 1. 0. 1. 0. 0. 0. 0. 0.
 0. 1. 1. 0. 1. 0. 1. 1.]

real	96m40.769s
user	408m55.347s
sys	49m57.117s
```

Evaluation with open test data...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631950958/checkpoints/model-74000 --vocab_filepath ./runs/1631950958/checkpoints/vocab --eval_filepath ./open-test.final.manual.word
...
...
...
0.9617986679077148
0.3559138774871826
0.9680095911026001
0.3147951364517212
0.9473056793212891
0.9830624461174011
0.986249566078186
0.9767338037490845
0.9748944640159607
0.9086078405380249
0.947942316532135
0.9724734425544739
0.7812961935997009
Accuracy: 0.47047

real	0m6.692s
user	0m7.027s
sys	0m1.199s
```

Evaluation with closed test data...   

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631950958/checkpoints/model-74000 --vocab_filepath ./runs/1631950958/checkpoints/vocab --eval_filepath ./closed-test.word 
...
...
...
0.05136781558394432
0.6581233739852905
0.9145849943161011
0.0513664111495018
0.0388374850153923
0.8176277279853821
0.8050743937492371
0.9768770933151245
0.03486732393503189
0.058863189071416855
0.026790976524353027
Accuracy: 0.96

real	0m6.582s
user	0m7.119s
sys	0m1.238s
```

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-200epoch-fasttext-max_document_length15-batch32-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-200epoch-fasttext-max_document_length15-batch32-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "myWord-word", fasttext, max_document_length=15, Batch Size = 32, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br> 

### Training and Evaluation with Batch Size 16

ဒီ တစ်ခါ Batch Size ကို 16 ထားပြီး run ကြည့်မယ်...  
(default က 64 မို့လို့)  

Training...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-word/all-para.fasttext.vector --embedding_dim 500 --num_epochs 200 --batch_size 16 2>&1 | tee train-myWord-epoch200-fasttext-max-doc-length14-batch_size16.18sept2021.log
...
...
...
DEV 2021-09-18T19:12:46.483289: step 455000, loss 0.0389468, acc 0.9375
(0, 0, 1, 0, 0, 0, 1, 1, 1, 0, 0, 0, 1, 0, 0, 1) [0. 0. 0. 0. 0. 0. 1. 1. 1. 0. 0. 0. 1. 0. 0. 1.]
DEV 2021-09-18T19:12:46.487393: step 455000, loss 0.0320925, acc 0.9375
(0, 0, 1, 0, 0, 1, 1, 1, 0, 0, 1, 1, 0, 1, 1, 0) [1. 0. 1. 0. 0. 1. 1. 1. 0. 0. 1. 1. 0. 1. 1. 0.]
DEV 2021-09-18T19:12:46.491122: step 455000, loss 0.0552768, acc 0.8125
(0, 1, 0, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0) [1. 0. 0. 0. 1. 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 1.]
DEV 2021-09-18T19:12:46.495124: step 455000, loss 0.0377479, acc 0.9375
(1, 0, 0, 0, 0, 1, 1, 0, 1, 1, 0, 0, 1, 1, 0, 0) [1. 0. 0. 0. 0. 1. 0. 0. 1. 1. 0. 0. 1. 1. 0. 0.]
DEV 2021-09-18T19:12:46.498875: step 455000, loss 0.0927998, acc 0.8125
(1, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0) [1. 1. 0. 1. 1. 0. 0. 0. 0. 1. 1. 0. 1. 1. 0. 0.]
DEV 2021-09-18T19:12:46.502812: step 455000, loss 0.146016, acc 0.5625
(1, 1, 0, 1, 1, 1, 1, 0, 1, 0, 0, 1, 1, 0, 0, 0) [1. 0. 1. 0. 1. 1. 0. 0. 1. 0. 0. 0. 1. 1. 1. 0.]
DEV 2021-09-18T19:12:46.506540: step 455000, loss 0.0244976, acc 0.9375
(1, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0) [0. 0. 0. 1. 0. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0.]
DEV 2021-09-18T19:12:46.510490: step 455000, loss 0.033423, acc 0.9375
(0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 1, 1, 0) [0. 1. 1. 0. 1. 0. 0. 0. 0. 1. 1. 0. 0. 1. 1. 0.]
DEV 2021-09-18T19:12:46.514506: step 455000, loss 0.0279166, acc 0.9375
(1, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1) [0. 0. 1. 1. 0. 1. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1.]
DEV 2021-09-18T19:12:46.518644: step 455000, loss 0.0283468, acc 0.9375
(0, 0, 1, 1, 0, 1, 0, 0, 1, 1, 0, 1, 0, 1, 0, 0) [0. 0. 1. 0. 0. 1. 0. 0. 1. 1. 0. 1. 0. 1. 0. 0.]
DEV 2021-09-18T19:12:46.522548: step 455000, loss 0.0354156, acc 0.9375
(0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 1, 0, 0) [0. 0. 1. 0. 0. 0. 1. 0. 0. 0. 0. 1. 0. 1. 0. 0.]
DEV 2021-09-18T19:12:46.528270: step 455000, loss 0.0582881, acc 0.875
(1, 0, 1, 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0) [0. 0. 1. 0. 0. 1. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0.]
DEV 2021-09-18T19:12:46.531930: step 455000, loss 0.149407, acc 0.625
(0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0) [0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 0. 0. 0. 1. 0.]
DEV 2021-09-18T19:12:46.535854: step 455000, loss 0.118709, acc 0.625
(1, 1, 0, 0, 0, 0, 0, 1, 1, 0, 1, 0, 1, 0, 0, 1) [1. 0. 0. 1. 0. 0. 0. 0. 1. 1. 1. 1. 0. 0. 0. 1.]
DEV 2021-09-18T19:12:46.539667: step 455000, loss 0.0687233, acc 0.8125
(1, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0) [0. 1. 1. 0. 0. 1. 0. 0. 0. 0. 1. 0. 1. 0. 0. 0.]
DEV 2021-09-18T19:12:46.543621: step 455000, loss 0.0851983, acc 0.8125
(1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1) [1. 0. 0. 1. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1.]
DEV 2021-09-18T19:12:46.547409: step 455000, loss 0.0851138, acc 0.8125
(1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0) [0. 1. 1. 0. 0. 0. 1. 0. 0. 1. 0. 0. 1. 0. 0. 0.]
DEV 2021-09-18T19:12:46.551519: step 455000, loss 0.117828, acc 0.75
(1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 1, 0, 0) [0. 0. 0. 1. 0. 0. 0. 0. 1. 0. 1. 0. 0. 0. 0. 0.]
DEV 2021-09-18T19:12:46.555381: step 455000, loss 0.114029, acc 0.6875
(0, 1, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0) [0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1.]
DEV 2021-09-18T19:12:46.559446: step 455000, loss 0.0994599, acc 0.75
(1, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0) [0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1.]
DEV 2021-09-18T19:12:46.563273: step 455000, loss 0.0536064, acc 0.8125
(0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0) [0. 1. 0. 1. 0. 0. 0. 1. 0. 1. 1. 1. 0. 0. 0. 0.]
DEV 2021-09-18T19:12:46.567221: step 455000, loss 0.0642047, acc 0.8125
(1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1) [1. 1. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 1.]
DEV 2021-09-18T19:12:46.571231: step 455000, loss 0.053512, acc 0.8
(1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 1, 0, 0) [0. 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 0. 1. 0. 0.]


real	158m14.640s
user	631m53.678s
sys	87m43.462s
```

Evaluation with open test data...

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631957680/checkpoints/model-278000 --vocab_filepath ./runs/1631957680/checkpoints/vocab --eval_filepath ./open-test.final.manual.word 
...
...
...
0.09737103432416916
0.8349100351333618
0.5718583464622498
0.9539714455604553
0.4346398711204529
0.9829984903335571
0.9852316975593567
0.9641343951225281
0.9493564963340759
0.9835594296455383
0.5822402238845825
0.9708181619644165
0.9960183501243591
0.8996568322181702
Accuracy: 0.48048

real	0m6.845s
user	0m7.109s
sys	0m1.289s
```

Evaluation with closed test data...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631957680/checkpoints/model-278000 --vocab_filepath ./runs/1631957680/checkpoints/vocab --eval_filepath ./closed-test.word 
...
...
...
0.035546641796827316
0.12186361849308014
0.9597530961036682
0.19731087982654572
0.1664719432592392
0.9887048602104187
0.7238930463790894
0.9657279253005981
0.09512090682983398
0.013249056413769722
0.014574057422578335
Accuracy: 0.96

real	0m6.545s
user	0m7.002s
sys	0m1.308s
```  

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-epoch200-fasttext-max-doc-length15-batch_size16.18sept2021-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-epoch200-fasttext-max-doc-length15-batch_size16.18sept2021-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "myWord-word", fasttext, max_document_length=15, Batch Size = 16, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br> 

### Training and Evaluation with Batch Size 128

- သိသိသာသာကြီးတော့ ပြောင်းလဲတာ မဟုတ်ပေမဲ့ open test မှာ top အထိတော့ ရောက်လာတယ်။  
- လုပ်လက်စနဲ့ batch size ကို လျှောတာ မဟုတ်ပဲ တိုးကြည့်မယ်။ 128 ထားပြီး run ကြည့်မယ်။ memory မနိုင်ရင်တော့ down သွားလိမ့်မယ်။ အချိန်ကတော့ ပိုမြန်လာမှာမို့...  

train  

```
TRAIN 2021-09-18T20:34:56.437872: step 56800, loss 0.00715417, acc 0.992188
(0, 1, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 1, 1, 1, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 1, 1) [0.98893255 0.04449805 0.98516876 0.07384958 0.97653365 0.9931233
 0.3426403  0.01499568 0.9397142  0.00985243 0.00662157 0.9584093
 0.98401266 0.87091655 0.9953214  0.93349475 0.99410987 0.96460116
 0.98955965 0.9570942  0.02024418 0.96880436 0.03979622 0.95159936
 0.044512   0.9640463  0.02205688 0.9082739  0.9885286  0.9603047
 0.9011498  0.99171436 0.01024971 0.9504751  0.9854933  0.846394
 0.9813922  0.9721602  0.9541315  0.01142997 0.9819446  0.17845133
 0.21813504 0.01233266 0.00725548 0.96160334 0.9610414  0.9936095
 0.8899325  0.02497481 0.00916614 0.9837413  0.9530923  0.9932352
 0.96732694 0.9495125  0.9939361  0.9928263  0.9542634  0.14402986
 0.94129723 0.8928191  0.9788322  0.9803882  0.98578113 0.9932462
 0.03488638 0.8921952  0.98482245 0.03730138 0.03869322 0.01120798
 0.9810165  0.8638478  0.21271087 0.95851743 0.9717313  0.9961764
 0.01163011 0.90928155 0.9498315  0.94930935 0.09413309 0.97967654
 0.9732036  0.36746678 0.9869391  0.80561626 0.874806   0.02922652
 0.9036345  0.01338273 0.10194791 0.05944632 0.98735    0.9796173
 0.9929584  0.9705825  0.01127431 0.9877322  0.07522707 0.00522548
 0.11014822 0.14123897 0.8416569  0.98357    0.9813028  0.9608407
 0.99267644 0.99129474 0.09957607 0.9632983  0.98458886 0.99183136
 0.9599739  0.9567542  0.8290281  0.99606895 0.21069199 0.98182315
 0.00839156 0.023146   0.02095954 0.9956263  0.16148451 0.01145996
 0.05812779 0.00761131] [0. 1. 0. 1. 0. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0.
 1. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 1. 1. 1. 1. 0. 0. 0.
 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 1. 1.
 0. 0. 1. 0. 0. 0. 1. 0. 0. 0. 1. 0. 0. 1. 0. 0. 0. 1. 0. 1. 1. 1. 0. 0.
 0. 0. 1. 0. 1. 1. 1. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 1. 0.
 1. 1. 1. 0. 1. 1. 1. 1.]

real	53m43.064s
user	252m3.097s
sys	27m4.489s
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-word/all-para.fasttext.vector --embedding_dim 500 --num_epochs 200 --batch_size 128 2>&1 | tee train-myWord-epoch200-fasttext-max-doc-length15-batch_size128.18sept2021.log

```

```
0.9859036207199097
0.9564060568809509
0.9937774538993835
0.98033207654953
0.9909590482711792
0.9629113078117371
0.9839295148849487
0.9901171922683716
0.04866617172956467
Accuracy: 0.465465

real	0m6.390s
user	0m6.711s
sys	0m1.308s
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631968881/checkpoints/model-44000 --vocab_filepath ./runs/1631968881/checkpoints/vocab --eval_filepath ./open-test.final.manual.word 

```

```
0.9858622550964355
0.10395412147045135
0.957053005695343
0.011664217337965965
0.8435176610946655
0.00354763213545084
0.01141747459769249
0.03913850709795952
0.9706794619560242
0.04380450397729874
0.08448033779859543
0.9894874095916748
0.3476203680038452
0.9513115286827087
0.035035908222198486
0.03613768517971039
0.02633647434413433
Accuracy: 0.958

real	0m6.089s
user	0m6.831s
sys	0m1.246s
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631968881/checkpoints/model-44000 --vocab_filepath ./runs/1631968881/checkpoints/vocab --eval_filepath ./closed-test.word 

```

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-epoch200-fasttext-max-doc-length15-batch_size128-18sept2021-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-epoch200-fasttext-max-doc-length15-batch_size128-18sept2021-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "myWord-word", fasttext, max_document_length=15, Batch Size = 128, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br> 
  
### Training and Evaluation with Batch Size 8

with batch 8  

Training...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-word/all-para.fasttext.vector --embedding_dim 500 --num_epochs 200 --batch_size 8 2>&1 | tee train-myWord-epoch200-fasttext-max-doc-length15-batch_size8.18sept2021.log
...
...
...
TRAIN 2021-09-19T02:08:46.656488: step 910191, loss 0.00185777, acc 1
(1, 0, 0, 0, 0, 1, 1, 0) [0.03990608 0.9727256  0.9108535  0.98155093 0.991791   0.00314731
 0.02321241 0.86404294] [1. 0. 0. 0. 0. 1. 1. 0.]
TRAIN 2021-09-19T02:08:46.673584: step 910192, loss 0.000753155, acc 1
(0, 0, 1, 0, 1, 0, 0, 1) [0.9626929  0.9809996  0.00982593 0.9717767  0.06024733 0.98469794
 0.92683154 0.01367546] [0. 0. 1. 0. 1. 0. 0. 1.]
TRAIN 2021-09-19T02:08:46.689704: step 910193, loss 0.000927542, acc 1
(0, 0, 1, 0, 0, 0, 1, 0) [0.99994725 0.9568301  0.00745048 0.9834818  0.97518104 0.9610638
 0.01131944 0.8980759 ] [0. 0. 1. 0. 0. 0. 1. 0.]
TRAIN 2021-09-19T02:08:46.705339: step 910194, loss 0.00461476, acc 1
(0, 0, 1, 0, 0, 0, 1, 0) [0.99264836 0.9474799  0.18195926 0.99416876 0.9921323  0.89002246
 0.15813509 0.97322494] [0. 0. 1. 0. 0. 0. 1. 0.]
TRAIN 2021-09-19T02:08:46.720925: step 910195, loss 0.0423163, acc 0.875
(1, 0, 1, 1, 1, 0, 0, 0) [0.08362851 0.9847577  0.03967705 0.00427338 0.8165049  0.97688437
 0.9999979  0.96794695] [1. 0. 1. 1. 0. 0. 0. 0.]
TRAIN 2021-09-19T02:08:46.736587: step 910196, loss 0.0034488, acc 1
(0, 0, 1, 0, 1, 1, 0, 1) [0.7889347  0.98449343 0.01578695 0.99186873 0.06425839 0.04289431
 0.93838656 0.01764195] [0. 0. 1. 0. 1. 1. 0. 1.]
TRAIN 2021-09-19T02:08:46.752479: step 910197, loss 0.00449611, acc 1
(0, 0, 1, 0, 0, 0, 0, 0) [0.92676604 0.9490532  0.0845099  0.979378   0.9269593  0.82777774
 0.85508394 0.97961104] [0. 0. 1. 0. 0. 0. 0. 0.]
TRAIN 2021-09-19T02:08:46.769228: step 910198, loss 0.000954758, acc 1
(0, 1, 0, 0, 0, 0, 0, 1) [0.96779895 0.04902476 0.99210054 0.9724558  0.94113284 0.9848764
 0.96279484 0.07704815] [0. 1. 0. 0. 0. 0. 0. 1.]
TRAIN 2021-09-19T02:08:46.789875: step 910199, loss 0.0024396, acc 1
(0, 0, 0, 0, 1, 0, 1, 1) [0.99512535 0.99994266 0.9134737  0.98314166 0.00388219 0.96048754
 0.17221716 0.0019391 ] [0. 0. 0. 0. 1. 0. 1. 1.]
TRAIN 2021-09-19T02:08:46.809164: step 910200, loss 0.00270052, acc 1
(0, 0, 0, 0, 1, 0, 1, 0) [0.8398588  0.99466497 0.8910279  0.99643314 0.02904102 0.9897509
 0.06704266 0.9857204 ] [0. 0. 0. 0. 1. 0. 1. 0.]

real	268m2.130s
user	1062m24.119s
sys	174m36.510s
```

Evaluation with open test data...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631976052/checkpoints/model-305000 --vocab_filepath ./runs/1631976052/checkpoints/vocab --eval_filepath ./open-test.final.manual.word 
...
...
...
0.9653648138046265
0.9659691452980042
0.9999502897262573
0.9781660437583923
0.10993435233831406
0.35477980971336365
0.996107280254364
0.016683556139469147
0.8212568163871765
0.8039032816886902
0.9736127853393555
0.9613524675369263
0.9766113758087158
0.9746643900871277
0.986161470413208
0.9969761371612549
0.9809455871582031
0.961876392364502
0.8280744552612305
Accuracy: 0.459459

real	0m6.674s
user	0m6.912s
sys	0m1.295s
```

Evaluation with closed test data...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1631976052/checkpoints/model-305000 --vocab_filepath ./runs/1631976052/checkpoints/vocab --eval_filepath ./closed-test.word 
...
...
...
0.048089444637298584
0.12703701853752136
0.7452284693717957
0.08231732249259949
0.2024417519569397
0.9374021887779236
0.9588937759399414
0.9569810628890991
0.8017306327819824
0.0364222526550293
0.011395945213735104
Accuracy: 0.95

real	0m6.398s
user	0m6.943s
sys	0m1.208s
```

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-epoch200-fasttext-max-doc-length15-batch_size8-18sept2021-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-epoch200-fasttext-max-doc-length15-batch_size8-18sept2021-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "myWord-word", fasttext, max_document_length=15, Batch Size = 8, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br> 
  
  

## Playing Hidden Units (80, 100)


Default က အောက်ပါအတိုင်း "50" ...  

```
tf.flags.DEFINE_integer("hidden_units", 50, "Number of hidden units (default:50)")
```

Training with hidden_units 80 ...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-word/all-para.fasttext.vector --embedding_dim 500 --hidden_units 80 --num_epochs 200 --batch_size 128 2>&1 | tee train-myWord-epoch200-fasttext-max-doc-length15-batch_size128-hidden-units80.19sept2021.log
...
...
...
TRAIN 2021-09-19T10:02:55.863663: step 56799, loss 0.00689599, acc 0.984375
(0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 0, 1, 1, 0, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1) [0.96008354 0.0434795  0.9986391  0.98858666 0.9976284  0.98758584
 0.9232492  0.14415649 0.4472968  0.98634696 0.9759302  0.9863774
 0.8323816  0.97134674 0.9770409  0.03988861 0.03634576 0.03353406
 0.9921223  0.16000226 0.9971628  0.8743508  0.98248994 0.08092334
 0.9827864  0.99543494 0.99816936 0.9957076  0.014832   0.98790413
 0.98294383 0.06613919 0.993161   0.07126638 0.99093556 0.9701534
 0.97346306 0.98717755 0.03050734 0.11752249 0.99716693 0.03040678
 0.98701215 0.9957608  0.9850543  0.13585424 0.99914366 0.15214063
 0.98482066 0.9937763  0.70550424 0.9893158  0.06888399 0.98782736
 0.03042401 0.9952615  0.9898806  0.00895595 0.85931456 0.01982016
 0.91180605 0.00979323 0.9827573  0.98701155 0.9260039  0.9946595
 0.9915597  0.0693153  0.9932875  0.9542401  0.9931093  0.9134049
 0.95425117 0.04747902 0.34215227 0.02538054 0.9696489  0.9730643
 0.03463023 0.8927941  0.00786105 0.99598265 0.9885221  0.03059609
 0.00453156 0.9887551  0.9884313  0.00798033 0.04365558 0.08577233
 0.91247946 0.01550312 0.94499916 0.00525763 0.03607941 0.9482978
 0.9625405  0.00706136 0.11116144 0.9861198  0.24926907 0.10305783
 0.9512727  0.99236715 0.8719931  0.9672973  0.9875881  0.95850825
 0.0439466  0.9822282  0.9970254  0.08973045 0.9932222  0.05092913
 0.01743638 0.998573   0.9195819  0.03242508 0.99150914 0.99336225
 0.93763286 0.99604845 0.9919478  0.7025144  0.945805   0.8899602
 0.9145456  0.01873425]/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:458: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
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
/home/ye/anaconda3/envs/paraphrase2/lib/python3.6/site-packages/numpy/core/_asarray.py:83: VisibleDeprecationWarning: Creating an ndarray from ragged nested sequences (which is a list-or-tuple of lists-or-tuples-or ndarrays with different lengths or shapes) is deprecated. If you meant to do this, you must specify 'dtype=object' when creating the ndarray
  return array(a, dtype, copy=False, order=order)
 [0. 1. 0. 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 0. 0. 1. 1. 1. 0. 1. 0. 0. 0. 1.
 0. 0. 0. 0. 1. 0. 0. 1. 0. 1. 0. 0. 0. 0. 1. 1. 0. 1. 0. 0. 0. 1. 0. 1.
 0. 0. 0. 0. 1. 0. 1. 0. 0. 1. 0. 1. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0.
 0. 1. 1. 1. 0. 0. 1. 0. 1. 0. 0. 1. 1. 0. 0. 1. 1. 1. 0. 1. 0. 1. 1. 0.
 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 0. 1. 1. 0. 0. 1. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 1.]
TRAIN 2021-09-19T10:02:55.941556: step 56800, loss 0.00579812, acc 0.992188
(0, 1, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 1, 1, 1, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 1, 1) [0.99748445 0.01503942 0.9898642  0.15090016 0.86168087 0.9936443
 0.08638985 0.02358826 0.9621086  0.02887449 0.00678937 0.89907265
 0.9901975  0.85304344 0.9403376  0.97265744 0.99490917 0.99342513
 0.9953361  0.95977736 0.08203688 0.99145955 0.01279815 0.9907073
 0.01576171 0.9978994  0.03229469 0.954032   0.9926211  0.9890453
 0.9992834  0.99696845 0.0343316  0.9925628  0.9643927  0.96918684
 0.95750827 0.98180866 0.98071283 0.04687326 0.6771118  0.17804745
 0.01696016 0.01207962 0.02415025 0.9765256  0.98819256 0.97640246
 0.9715343  0.04416689 0.04139017 0.995106   0.9906807  0.99568444
 0.9973935  0.9651161  0.993226   0.8807839  0.99451464 0.07823469
 0.9523315  0.940349   0.99738294 0.99059856 0.9978822  0.9888982
 0.06245081 0.99738896 0.9871685  0.02338487 0.00663392 0.00771589
 0.9847533  0.9806138  0.03064734 0.9697826  0.78268665 0.99860924
 0.04582025 0.891179   0.9963223  0.9487666  0.08691469 0.9969385
 0.98065555 0.0336427  0.9883983  0.9770088  0.8983085  0.08947548
 0.9983189  0.0067191  0.07282192 0.0038964  0.96572596 0.9907323
 0.9929252  0.98927766 0.00225778 0.9868995  0.01068619 0.00401066
 0.01132973 0.05257326 0.88213736 0.9778928  0.9905981  0.97720385
 0.9836171  0.97089106 0.06440663 0.9813887  0.9960412  0.9786449
 0.9978182  0.9370796  0.9927651  0.94601494 0.05418006 0.9927412
 0.01273309 0.04517234 0.05684408 0.99879956 0.31007898 0.00820068
 0.09405867 0.03351604] [0. 1. 0. 1. 0. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0.
 1. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 1. 1. 1. 1. 0. 0. 0.
 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 1. 1.
 0. 0. 1. 0. 0. 0. 1. 0. 0. 0. 1. 0. 0. 1. 0. 0. 0. 1. 0. 1. 1. 1. 0. 0.
 0. 0. 1. 0. 1. 1. 1. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 1. 0.
 1. 1. 1. 0. 1. 1. 1. 1.]

real	77m21.227s
user	410m16.650s
sys	41m1.093s
```

Evaluation with open test data...

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1632015943/checkpoints/model-24000 --vocab_filepath ./runs/1632015943/checkpoints/vocab --eval_filepath ./open-test.final.manual.word
...
...
...
0.9903789758682251
0.6760683059692383
0.9890448451042175
0.9636557102203369
0.4964662790298462
0.8603502511978149
0.9946073889732361
0.6331019997596741
0.9895495772361755
0.958094596862793
0.9703750610351562
0.8610476851463318
0.9976627230644226
0.1999111920595169
0.9953885674476624
0.8401797413825989
0.9313542246818542
0.9136837124824524
0.9679527282714844
0.9364022612571716
0.9885643124580383
0.9834272861480713
0.9702487587928772
0.9908196330070496
0.9933100938796997
0.9908649325370789
0.9543254375457764
Accuracy: 0.457457

real	0m6.670s
user	0m7.299s
sys	0m1.320s
```

Evaluation with closed test data...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1632015943/checkpoints/model-24000 --vocab_filepath ./runs/1632015943/checkpoints/vocab --eval_filepath ./closed-test.word
...
...
...
0.057475633919239044
0.8561100363731384
0.016477342694997787
0.10651938617229462
0.04892006143927574
0.9846063852310181
0.18044225871562958
0.2706989645957947
0.9808452725410461
0.6464325785636902
0.9958001375198364
0.03720360994338989
0.03238968923687935
0.0183793306350708
Accuracy: 0.966

real	0m6.091s
user	0m7.165s
sys	0m1.245s
```

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-fasttext-max_doc-length15-batch_size128-hidden_units80-epoch200-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-fasttext-max_doc-length15-batch_size128-hidden_units80-epoch200-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "myWord-word", fasttext, max_document_length=15, Batch Size = 8, **hidden_units = 80**, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>  
  
Training with hidden_units 100 ...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/163/checkpoints/model-24000 --vocab_filepath ./runs/1632015943/checkpoints/vocab --eval_filepath ./open-test.final.manual.word 
1631968881/ 1632015943/ 1632021038/
...
...
...
TRAIN 2021-09-19T11:49:02.326422: step 56799, loss 0.00150294, acc 1
(0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 0, 1, 1, 0, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1) [0.98797727 0.05778217 0.99342036 0.9601727  0.9933479  0.991539
 0.9753987  0.05447035 0.97502923 0.97931    0.9815827  0.97747177
 0.9729986  0.9792168  0.9946935  0.0056797  0.04524836 0.07936098
 0.9948534  0.0415458  0.9807506  0.7140992  0.99924207 0.08280636
 0.99795324 0.9928986  0.998295   0.99725884 0.00305175 0.99372107
 0.97544295 0.01429896 0.99087006 0.00747938 0.988577   0.9977412
 0.9974732  0.99072266 0.00958685 0.13701275 0.99680144 0.00363376
 0.94161665 0.9926777  0.98645395 0.90532595 0.9929393  0.03315252
 0.97899055 0.9862539  0.994164   0.99141324 0.02435222 0.9902621
 0.07970246 0.9874631  0.9907539  0.06953542 0.9957651  0.055096
 0.9876097  0.0657955  0.9920751  0.96194685 0.9523996  0.99508125
 0.972728   0.13344015 0.9915283  0.92335534 0.9902977  0.9559341
 0.9908542  0.01363836 0.0295854  0.04093583 0.99908364 0.98541117
 0.0114614  0.99527866 0.04804048 0.9203682  0.9945875  0.14982776
 0.00411682 0.98884106 0.9924598  0.00790326 0.01463957 0.15807448
 0.9794528  0.01265432 0.95693415 0.01050018 0.04349682 0.94245964
 0.9581554  0.00897688 0.2592739  0.9686135  0.05681589 0.03622668
 0.9977888  0.98067355 0.9857632  0.87094516 0.98971635 0.92219794
 0.03559797 0.981656   0.95321417 0.07744087 0.9915528  0.07137285
 0.0150079  0.9986768  0.992164   0.00991364 0.97362477 0.9908045
 0.99823403 0.98918676 0.9923736  0.98040414 0.9647025  0.99687296
 0.9493618  0.05567533] [0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 1. 1. 1. 0. 1. 0. 0. 0. 1.
 0. 0. 0. 0. 1. 0. 0. 1. 0. 1. 0. 0. 0. 0. 1. 1. 0. 1. 0. 0. 0. 0. 0. 1.
 0. 0. 0. 0. 1. 0. 1. 0. 0. 1. 0. 1. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0.
 0. 1. 1. 1. 0. 0. 1. 0. 1. 0. 0. 1. 1. 0. 0. 1. 1. 1. 0. 1. 0. 1. 1. 0.
 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 0. 1. 1. 0. 0. 1. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 1.]
TRAIN 2021-09-19T11:49:02.426032: step 56800, loss 0.00135911, acc 1
(0, 1, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 1, 1, 1, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 1, 1) [0.9980315  0.10397734 0.9910403  0.05654317 0.949212   0.9971089
 0.19390854 0.9157792  0.95188534 0.02068768 0.00811281 0.96526563
 0.980101   0.9351864  0.9835696  0.9917342  0.9841047  0.9932216
 0.9897279  0.9541875  0.00811666 0.99188244 0.04410606 0.99834687
 0.00353435 0.9859713  0.00929413 0.9839156  0.9984199  0.9917065
 0.96359813 0.99682057 0.02267849 0.9778394  0.9970043  0.882563
 0.99482006 0.98515075 0.9719909  0.03518144 0.898184   0.02797582
 0.15798363 0.00406762 0.01897743 0.98863304 0.97043276 0.9970629
 0.9537353  0.10292603 0.0050393  0.99129426 0.98991936 0.9927889
 0.99805325 0.96599174 0.982835   0.9500324  0.9861721  0.01419633
 0.9926889  0.9439796  0.9879151  0.99178916 0.9905796  0.9948835
 0.00626121 0.9832788  0.98631454 0.04928223 0.00314159 0.00414913
 0.98833275 0.9044731  0.040857   0.9860908  0.9898924  0.99652034
 0.00553263 0.9311647  0.99601495 0.9857431  0.02189248 0.9932194
 0.8958931  0.17683871 0.9913646  0.9959405  0.99683493 0.16864623
 0.9903987  0.00646073 0.09054842 0.01288416 0.9923628  0.9866678
 0.99014294 0.991337   0.0150082  0.9933805  0.0541211  0.01630788
 0.25464663 0.01981673 0.9840162  0.97837746 0.99571544 0.9766202
 0.9867341  0.9899967  0.0256057  0.9714582  0.9915846  0.99289644
 0.97180533 0.9830732  0.99172884 0.863391   0.05341799 0.99032056
 0.00250714 0.00723718 0.0142429  0.99037373 0.0360524  0.0028002
 0.00789937 0.00485939] [0. 1. 0. 1. 0. 0. 1. 0. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0.
 1. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 1. 1. 1. 1. 0. 0. 0.
 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 1. 1.
 0. 0. 1. 0. 0. 0. 1. 0. 0. 0. 1. 0. 0. 1. 0. 0. 0. 1. 0. 1. 1. 1. 0. 0.
 0. 0. 1. 0. 1. 1. 1. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 1. 0.
 1. 1. 1. 0. 1. 1. 1. 1.]

real	98m32.292s
user	548m16.703s
sys	52m3.512s
 ```

Evaluation with open test data...

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1632021038/checkpoints/model-12000 --vocab_filepath ./runs/1632021038/checkpoints/vocab --eval_filepath ./open-test.final.manual.word 
...
...
...
0.8836311101913452
0.9877339601516724
0.9811812043190002
0.9612742066383362
0.9585511684417725
0.9627130031585693
0.9890472292900085
0.9888907074928284
0.20945025980472565
Accuracy: 0.472472

real	0m6.858s
user	0m7.774s
sys	0m1.288s
```

Evaluation with closed test data...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1632021038/checkpoints/model-12000 --vocab_filepath ./runs/1632021038/checkpoints/vocab --eval_filepath ./closed-test.word
...
...
...
0.027162594720721245
0.08747516572475433
0.3960792124271393
0.5358574986457825
0.013986693695187569
0.1506965160369873
0.8232517242431641
0.590276300907135
0.9166087508201599
0.10452276468276978
0.022880397737026215
0.013701611198484898
Accuracy: 0.962

real	0m6.412s
user	0m7.549s
sys	0m1.304s
```

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-fasttext-max_doc-length15-batch_size128-hidden_units100-epoch200-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-fasttext-max_doc-length15-batch_size128-hidden_units100-epoch200-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "myWord-word", fasttext, max_document_length=15, Batch Size = 8, **hidden_units = 100**, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>  
  
### Experiment with Hidden Units 200

Hidden unit ကို တိုးကြည့်ခြင်းအားဖြင့် ရလဒ်မှာ ဘယ်လို သက်ရောက်မှုရှိသလဲ ဆိုတာကို ကြည့်ချင်တယ်...  

Training...  
```
TRAIN 2021-09-19T16:24:39.201050: step 56799, loss 0.00568583, acc 0.992188
(0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 0, 1, 1, 0, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1) [0.9999995  0.06600956 0.99999475 0.98780465 0.99967945 0.99996686
 0.98924893 0.02328436 0.9733005  0.99999857 0.99998873 0.8206937
 0.9714638  0.870831   0.9991422  0.02600494 0.05080863 0.02253476
 0.9999908  0.05320882 0.99999845 0.7404357  0.8638974  0.07006209
 0.99949235 0.9999981  0.9984778  0.52130437 0.04144137 0.988197
 0.94312394 0.02899923 0.97678465 0.02522051 0.9999966  0.9999987
 0.7307124  0.99997413 0.01459773 0.01974709 0.99779075 0.00248542
 0.9332421  0.99998945 0.99922603 0.22997421 0.9999987  0.05651654
 0.9335722  0.9984346  0.9956376  0.999961   0.01630518 0.99999094
 0.01405815 0.99999917 0.9977108  0.00507964 0.85111153 0.03910892
 0.94987184 0.04076211 0.99881727 0.9721893  0.9723979  0.999996
 0.99999875 0.02623825 0.9999891  0.99999607 0.9869323  0.97260857
 0.87837356 0.00878605 0.01613044 0.0257945  0.9999873  0.98923266
 0.00471694 0.9995036  0.00145971 0.9086946  0.9999375  0.03463826
 0.00338798 0.9734288  0.97058785 0.13827273 0.06347995 0.15024957
 0.999997   0.01091347 0.9836654  0.00158742 0.00714629 0.9626525
 0.97959775 0.00124933 0.11589885 0.97515    0.21206637 0.04680314
 0.9761969  0.9813297  0.9420918  0.57160515 0.99997735 0.86775625
 0.00493999 0.9972329  0.99342465 0.03504947 0.99999636 0.0375863
 0.01109098 0.99894536 0.9999981  0.00365695 0.9956921  0.9999367
 0.9106621  0.99999934 0.9999967  0.999816   0.9617652  0.9470359
 0.99753606 0.0080701 ] [0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 1. 1. 1. 0. 1. 0. 0. 0. 1.
 0. 0. 0. 0. 1. 0. 0. 1. 0. 1. 0. 0. 0. 0. 1. 1. 0. 1. 0. 0. 0. 1. 0. 1.
 0. 0. 0. 0. 1. 0. 1. 0. 0. 1. 0. 1. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0.
 0. 1. 1. 1. 0. 0. 1. 0. 1. 0. 0. 1. 1. 0. 0. 1. 1. 1. 0. 1. 0. 1. 1. 0.
 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 0. 1. 1. 0. 0. 1. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 1.]
TRAIN 2021-09-19T16:24:39.515780: step 56800, loss 0.00153731, acc 1
(0, 1, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 1, 1, 1, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 1, 1) [0.99999034 0.01554931 0.99999815 0.03362669 0.9817217  0.9974437
 0.02928895 0.6423491  0.99998266 0.02569702 0.0148371  0.9744598
 0.99999785 0.9667639  0.9999938  0.96646166 0.9999988  0.9999991
 0.99999905 0.9996529  0.04704428 0.99995774 0.03932017 0.96651864
 0.00148254 0.9999934  0.02251011 0.89405984 0.9771394  0.99999756
 0.87672603 0.9997829  0.00214819 0.9516075  0.9999662  0.8366784
 0.99759674 0.99957615 0.99840164 0.02642784 0.999987   0.07493971
 0.0241367  0.00451633 0.01327371 0.99992305 0.99795276 0.9997678
 0.99516124 0.00301333 0.0040026  0.9999993  0.9999987  0.9999845
 0.9988173  0.9877183  0.9999987  0.9669281  0.9747639  0.03180455
 0.99985254 0.9815787  0.99996233 0.9999936  0.9750637  0.9999702
 0.00542689 0.9859162  0.9998819  0.00555981 0.00439281 0.00655893
 0.99999434 0.81347495 0.10591505 0.9999472  0.9472466  0.9787277
 0.04138113 0.997298   0.92989796 0.99981153 0.05069036 0.9799033
 0.9999281  0.02159362 0.9999957  0.99998945 0.9775107  0.05746001
 0.8929381  0.00377445 0.0320724  0.00348737 0.98658687 0.9999988
 0.9999961  0.9999786  0.01533161 0.9973322  0.06113447 0.01367223
 0.00295958 0.02943331 0.94270897 0.9783589  0.87702376 0.99981403
 0.99998    0.99911255 0.0431125  0.9879038  0.99999565 0.99998224
 0.99976844 0.986218   0.9989184  0.82382184 0.21614008 0.99990463
 0.01358469 0.02658643 0.00543392 0.95229834 0.05745857 0.00384571
 0.02026095 0.00229271] [0. 1. 0. 1. 0. 0. 1. 0. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0.
 1. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 1. 1. 1. 1. 0. 0. 0.
 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 1. 1.
 0. 0. 1. 0. 0. 0. 1. 0. 0. 0. 1. 0. 0. 1. 0. 0. 0. 1. 0. 1. 1. 1. 0. 0.
 0. 0. 1. 0. 1. 1. 1. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 1. 0.
 1. 1. 1. 0. 1. 1. 1. 1.]

real	245m50.179s
user	1524m4.884s
sys	127m47.910s
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-word/all-para.fasttext.vector --embedding_dim 500 --hidden_units 200 --num_epochs 200 --batch_size 128 2>&1 | tee train-myWord-epoch200-fasttext-max-doc-length15-batch_size128-hidden-units200.19sept2021.log

```

Evaluation with Open Test...    

```
0.021944165229797363
0.4867711365222931
0.7697957158088684
0.9989840984344482
0.9999575018882751
0.9998946189880371
0.9999101758003235
0.9941884875297546
0.9978181719779968
0.9999339580535889
0.9999669790267944
0.9999174475669861
Accuracy: 0.454454

real	0m6.970s
user	0m9.964s
sys	0m1.513s
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1632028737/checkpoints/model-15000 --vocab_filepath ./runs/1632028737/checkpoints/vocab --eval_filepath ./open-test.final.manual.word 
```

Evaluation with Closed Test...   

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1632028737/checkpoints/model-15000 --vocab_filepath ./runs/1632028737/checkpoints/vocab --eval_filepath ./closed-test.word 

0.07809671014547348
0.9977867007255554
0.03831274062395096
0.9056090116500854
0.01958031766116619
0.03582420200109482
0.06769813597202301
0.9758111834526062
0.2538534104824066
0.09882841259241104
0.9510629773139954
0.9232838153839111
0.9997376203536987
0.07959375530481339
0.02659495919942856
0.01065360102802515
Accuracy: 0.97

real	0m6.775s
user	0m10.231s
sys	0m1.350s
```

Training time ကတော့ အရမ်းကြာသွားတယ်။ graph နဲ့ ကြည့်ရင် အောက်ပါအတိုင်း...  
(ပုံမှန်အားဖြင့်က 1နာရီ ဝန်းကျင်နဲ့ ပြီးပေမဲ့ ဒီတစ်ခေါက်ကတော့ ...  )


<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-fasttext-max_doc-length15-batch_size128-hidden_units200-epoch200-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-fasttext-max_doc-length15-batch_size128-hidden_units200-epoch200-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "myWord-word", fasttext, max_document_length=15, Batch Size = 8, **hidden_units = 200**, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>  

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-fasttext-max_doc-length15-batch_size128-hidden_units200-epoch200-accuracy-time.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-fasttext-max_doc-length15-batch_size128-hidden_units200-epoch200-loss-time.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "myWord-word", fasttext, max_document_length=15, Batch Size = 8, **hidden_units = 200**, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>  

အခုချိန်ထိ လုပ်ခဲ့တဲ့ parameter tuning ရလဒ်တွေကို ဇယားဆောက်ကြည့်ရင် အောက်ပါအတိုင်း...   




-----------

## Evaluation with "checkpoint_dir"

checkpoint_dir ကိုပဲ ပေးပြီး Run ကြည့်ခဲ့ပေမဲ့ Run လို့ မရဘူး...
Vocab ဖိုင်path ကို တောင်းတယ်။ vocab filepath ကိုဖြည့်လည်း မရဘူး။
အောက်ပါအတိုင်း model က fixed လုပ်ထားတဲ့ ပုံစံဖြစ်နေလို့ coding ကို ဝင်ပြင်မှ ရလိမ့်မယ်။
လက်ရှိအတိုင်း မော်ဒယ် path ကို အတိအကျပေး၊ vocab path ကိုပေးပြီး run တာက ပြဿနာမရှိဘူးလို့ ယုံကြည်တယ်။   

```python
Parameters:
ALLOW_SOFT_PLACEMENT=True
BATCH_SIZE=64
CHECKPOINT_DIR=./runs/1632028737/checkpoints/
EVAL_FILEPATH=./closed-test.word
LOG_DEVICE_PLACEMENT=False
MODEL=runs/1512222837/checkpoints/model-5000
VOCAB_FILEPATH=./runs/1632028737/checkpoints/vocab

Loading testing/labelled data from ./closed-test.word
792
```

## Playing with Misc Parameters

train.py မှာရော eval.py မှာရော အောက်ပါ command line argument နှစ်ခု ကို support လုပ်ထားတယ်...  

```python
tf.flags.DEFINE_boolean("allow_soft_placement", True, "Allow device soft device placement")
tf.flags.DEFINE_boolean("log_device_placement", False, "Log placement of ops on devices")
```

training မှာ ငါ မလုပ်ကြည့်ခဲ့ပေမဲ့ evaluation မှာတော့ မြန်တော့ ဒီ option နှစ်ခုကို True/False လုပ်ကြည့်ခဲ့...  
closed-test, open test နှစ်ခုလုံးနဲ့ စမ်းကြည့်ခဲ့...  ရလဒ်မှာ ဘာအပြောင်းအလဲမှ မရှိ  

------------

## Playing Dropout

Default dropout က အောက်ပါအတိုင်း...  

```
tf.flags.DEFINE_float("dropout_keep_prob", 1.0, "Dropout keep probability (default: 1.0)")
```

### training/validation with dropout 0.3

Training
```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-word/all-para.fasttext.vector --embedding_dim 500 --dropout_keep_prob 0.3 --num_epochs 200 --batch_size 128 2>&1 | tee train-myWord-epoch200-fasttext-max-doc-length15-batch_size128-dropout0.3.19-sept2021.log
...
...
...
TRAIN 2021-09-19T17:51:28.978016: step 56798, loss 0.0858131, acc 0.617188
(0, 0, 0, 1, 1, 1, 0, 1, 0, 1, 0, 0, 0, 1, 1, 1, 0, 1, 0, 1, 1, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 1, 1, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 1, 1, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 1, 0, 1, 1, 0) [0.89831084 0.542138   0.99880433 0.578645   0.6126059  0.64776236
 0.54780245 0.54222846 0.7089221  0.6526236  0.9999983  0.97700876
 0.9286358  0.57373464 0.6220245  0.5983121  0.6480494  0.57309467
 0.62909263 0.6069158  0.63225853 0.6220263  0.99988484 0.87719876
 0.997969   0.96151    0.999645   0.9900018  0.5421874  0.63319945
 0.9918734  0.5722605  0.53798443 0.96635085 0.59025025 0.9458008
 0.67696744 0.5414472  0.61236674 0.6204126  0.9911351  0.6763898
 0.99833906 0.60738087 0.9823729  0.96962756 0.93259835 0.63636076
 0.98658204 0.589055   0.91043067 0.63904166 0.6416887  0.5563491
 0.9991617  0.93826306 0.9900399  0.53809917 0.9879628  0.9979794
 0.6127442  0.653643   0.99287164 0.5331615  0.99172556 0.787013
 0.63724124 0.61859095 0.9197604  0.65487856 0.6131347  0.6584891
 0.9883598  0.63112706 0.5432596  0.9999203  0.61303765 0.53962153
 0.999911   0.55518204 0.98883504 0.570349   0.6010823  0.69245744
 0.93629074 0.6396006  0.8173982  0.99290615 0.9440498  0.91307026
 0.64573544 0.98960125 0.51474035 0.6332445  0.5188722  0.99255615
 0.5639217  0.98784435 0.5744801  0.60252    0.4929012  0.92339015
 0.54146415 0.8901703  0.95555466 0.57617104 0.57873446 0.9929294
 0.98459065 0.99459004 0.61290234 0.99974716 0.6271622  0.6135975
 0.9926899  0.9916548  0.9997774  0.6208076  0.99124163 0.8447508
 0.9205384  0.5979728  0.9075466  0.642849   0.94614995 0.70959365
 0.5619504  0.52517414] [0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 0.]
TRAIN 2021-09-19T17:51:29.025483: step 56799, loss 0.0758093, acc 0.6875
(0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 0, 1, 1, 0, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1) [0.62837595 0.66786945 0.9409178  0.6504329  0.9951757  0.9423084
 0.9999427  0.56691074 0.60179883 0.9999936  0.99587476 0.61380917
 0.9407665  0.9988139  0.6253218  0.58605564 0.5927695  0.60554785
 0.9809914  0.63387126 0.98498553 0.56109846 0.99384606 0.55511206
 0.626834   0.98816985 0.99935246 0.965482   0.56181085 0.98696136
 0.6614471  0.595754   0.7455434  0.60621834 0.95737314 0.9899798
 0.92694    0.99651223 0.6019958  0.6498344  0.5766129  0.57766634
 0.5841511  0.9999829  0.9999302  0.6220276  0.999996   0.64544505
 0.59592605 0.99946344 0.58371794 0.9940447  0.52946866 0.9785271
 0.57446164 0.9356654  0.92156494 0.60191005 0.57765466 0.6440612
 0.94812995 0.49325836 0.9612229  0.938627   0.6165704  0.98878026
 0.98962474 0.6521884  0.9999946  0.9999998  0.9952852  0.9471761
 0.8841055  0.69203174 0.5841444  0.63492453 0.99979776 0.91498375
 0.5778863  0.9999191  0.61755717 0.9773974  0.9997129  0.57744074
 0.5189336  0.9996531  0.99945694 0.6327173  0.6092066  0.58522916
 0.9999028  0.62754875 0.9394281  0.5302863  0.68313825 0.5887845
 0.8456903  0.56730163 0.5487114  0.9196736  0.99027884 0.48332512
 0.5553816  0.99226046 0.6701823  0.6419401  0.98573434 0.6546533
 0.61320096 0.9910201  0.9722635  0.5711428  0.94347215 0.43600112
 0.6356748  0.98834467 0.8857932  0.6732016  0.99895203 0.9954401
 0.67923    0.9932044  0.95279825 0.9110846  0.9998289  0.5590291
 0.99285    0.5778808 ] [0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 0.]
TRAIN 2021-09-19T17:51:29.073658: step 56800, loss 0.0785956, acc 0.664062
(0, 1, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 1, 1, 1, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 1, 1) [0.7471598  0.5007721  0.5959633  0.6004416  0.60179555 0.9999889
 0.59816176 0.5826911  0.6804864  0.51644146 0.56211394 0.62457466
 0.8518688  0.9184734  0.90748346 0.94489765 0.9854465  0.998637
 0.9845774  0.51205486 0.61451846 0.99022144 0.6155286  0.99485236
 0.61738205 0.5478599  0.47404492 0.9215802  0.97219443 0.98978174
 0.8892868  0.94411254 0.63389134 0.9932962  0.904045   0.6172168
 0.9514726  0.9997882  0.9887644  0.61751795 0.9951047  0.47186154
 0.6125823  0.5345218  0.6428533  0.9893989  0.9556926  0.5370387
 0.9198501  0.67095697 0.5776941  0.9928134  0.9994396  0.98057884
 0.9978897  0.799027   0.9998023  0.62786955 0.90950114 0.6162969
 0.95511854 0.6068848  0.99998826 0.6267434  0.9460645  0.980438
 0.61459345 0.7653887  0.9998982  0.58254087 0.54195666 0.59420574
 0.99913883 0.5536601  0.68900156 0.91917163 0.6451798  0.99005175
 0.6062162  0.5933077  0.98682487 0.9999999  0.611791   0.98958874
 0.97841054 0.5773082  0.95594925 0.9896814  0.56643915 0.6018867
 0.4771903  0.64656496 0.67155844 0.6357456  0.9851021  0.9992453
 0.9999318  0.994236   0.62816757 0.9879931  0.64805096 0.630453
 0.55572057 0.6360917  0.9328173  0.9909787  0.55105615 0.99135214
 0.9971061  0.9795627  0.50090563 0.5349686  0.9756878  0.9892739
 0.99988306 0.5359101  0.9228017  0.99999994 0.6363865  0.8452608
 0.6716614  0.5419618  0.55051744 0.99031955 0.5505009  0.5983485
 0.9455715  0.6056997 ] [0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 0.]

real	48m5.260s
user	248m38.320s
sys	25m57.861s
```

Evaluation with open test

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1632045811/checkpoints/model-49000 --vocab_filepath ./runs/1632045811/checkpoints/vocab --eval_filepath ./open-test.final.manual.word
...
...
...
0.9902514815330505
0.9974169731140137
0.9975934624671936
0.9050056338310242
0.9977385997772217
0.9853681921958923
0.00011787795665441081
0.9979106187820435
0.9998983144760132
0.9906489253044128
0.9902304410934448
0.990393877029419
0.9908090233802795
0.9907548427581787
0.9899232983589172
0.9906142950057983
0.9907415509223938
0.00011730215919669718
Accuracy: 0.504505

real	0m6.574s
user	0m6.885s
sys	0m1.295s
```

Evaluatin with closed-test

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1632045811/checkpoints/model-49000 --vocab_filepath ./runs/1632045811/checkpoints/vocab --eval_filepath ./closed-test.word
...
...
...
0.9908466339111328
0.006372394971549511
0.9985648989677429
0.00011611670925049111
0.0006372779607772827
0.00011605738836806267
0.01888386718928814
0.00011835629993584007
0.00011541764251887798
0.00011536699457792565
0.00016449691611342132
0.9979623556137085
0.08503350615501404
0.18771852552890778
0.00011470980825833976
0.00012022916052956134
0.00011555595847312361
Accuracy: 0.839

real	0m6.406s
user	0m6.940s
sys	0m1.247s
```

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-fasttext-max_doc-length15-batch_size128-hidden_units200-dropout0.3-epoch200-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-fasttext-max_doc-length15-batch_size128-hidden_units200-dropout0.3-epoch200-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "myWord-word", fasttext, max_document_length=15, Batch Size = 8, **--dropout_keep_prob 0.3**, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br>  
  
Note: အခုချိန်ထိ လုပ်ခဲ့တဲ့ training နဲ့ validation နှစ်ခုအကြားရဲ့ learning rate မှာ ပြောင်းလဲမှု သိသိသာသာ ဖြစ်စေတာက dropout ပဲ  

### training/validation with dropout 0.6

Training...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-word/all-para.fasttext.vector --embedding_dim 500 --dropout_keep_prob 0.6 --num_epochs 200 --batch_size 128 2>&1 | tee train-myWord-epoch200-fasttext-max-doc-length15-batch_size128-dropout0.6.19-sept2021.log
...
...
...
TRAIN 2021-09-19T20:12:59.443781: step 56798, loss 0.0590359, acc 0.851562
(0, 0, 0, 1, 1, 1, 0, 1, 0, 1, 0, 0, 0, 1, 1, 1, 0, 1, 0, 1, 1, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 1, 1, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 1, 1, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 1, 0, 1, 1, 0) [0.9428333  0.49043295 0.9977025  0.5105157  0.4572112  0.40907958
 0.9569281  0.4440592  0.4437955  0.5480318  0.9765081  0.99999803
 0.9650765  0.44958788 0.4534829  0.49638602 0.9999337  0.43039307
 0.43338045 0.531424   0.5336742  0.41593978 0.9999507  0.47333875
 0.99999475 0.999966   0.99999964 0.99854106 0.47233552 0.41936108
 0.9998733  0.46986762 0.44323266 0.9999965  0.6425158  0.9968083
 0.51119006 0.36523023 0.41524026 0.52518123 0.88987345 0.42452228
 0.9998587  0.95437324 0.99782133 0.9288572  0.87096286 0.4858694
 0.6493997  0.52971697 0.94562024 0.9980808  0.4694354  0.36007482
 0.97523785 0.961917   0.99998224 0.4825918  0.9645845  0.9999628
 0.49412122 0.31109682 0.99431103 0.46015146 0.97429955 0.9999816
 0.4315792  0.8834134  0.9997361  0.43878958 0.69167215 0.9471349
 0.9803159  0.97473866 0.38812476 0.9999939  0.37813684 0.9835328
 0.9990475  0.5107082  0.9999471  0.4913239  0.9998203  0.99384737
 0.31644323 0.9765501  0.99563307 0.99992937 0.8534014  0.97566944
 0.47273633 0.99999    0.4671243  0.87601113 0.41567507 0.9998909
 0.9884433  0.99999887 0.45362377 0.38109273 0.45641223 0.6796058
 0.45735636 0.9999311  0.99998784 0.49793732 0.4711444  0.99999547
 0.9999959  0.9453358  0.97653675 0.9999876  0.43206358 0.4161449
 0.9999886  0.9999835  0.9998397  0.52268803 0.87452084 0.9999725
 0.9996154  0.8541897  0.7708078  0.95985353 0.78952324 0.49170494
 0.38740715 0.57919437] [0. 1. 0. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 1. 1. 1. 0. 1. 1. 0. 0. 1. 0. 1.
 0. 0. 0. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 1. 1. 0. 0. 1. 0. 0. 0. 0. 0. 1.
 0. 0. 0. 0. 1. 1. 0. 0. 0. 1. 0. 0. 1. 1. 0. 1. 0. 0. 1. 0. 0. 1. 0. 0.
 0. 0. 1. 0. 1. 0. 0. 0. 0. 1. 0. 0. 1. 0. 0. 0. 0. 0. 1. 0. 1. 0. 1. 0.
 0. 0. 1. 1. 1. 0. 1. 0. 0. 1. 1. 0. 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 0. 0.
 0. 0. 0. 0. 0. 1. 1. 0.]
TRAIN 2021-09-19T20:12:59.494734: step 56799, loss 0.0460168, acc 0.890625
(0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 0, 1, 1, 0, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1) [0.9639286  0.3816652  0.99995255 0.9736398  0.9999941  0.99994594
 0.94882    0.39229122 0.49460754 0.9473358  0.9999807  0.8812573
 0.9713771  0.8802114  0.8798587  0.40145966 0.45261347 0.45356315
 0.99998605 0.5021822  0.99998176 0.9118507  0.9961207  0.44250882
 0.9526726  0.99984324 0.9006224  0.499809   0.447026   0.9991294
 0.80658925 0.3773477  0.9997088  0.44729486 0.9999404  0.9999858
 0.9995417  0.99995816 0.41566607 0.49865326 0.9554986  0.4434284
 0.38203433 0.999918   0.9999841  0.4495573  0.99999505 0.4295671
 0.9898091  0.99871975 0.9993184  0.99736655 0.52075875 0.99997544
 0.51513404 0.9999755  0.9999897  0.5047913  0.861278   0.39515468
 0.8920846  0.38053396 0.9979121  0.9756198  0.43207976 0.93996704
 0.9999527  0.44068956 0.9999983  0.9110893  0.9999837  0.97420454
 0.9994351  0.36814982 0.5207922  0.4720887  0.999996   0.99995714
 0.44321546 0.9998084  0.37345025 0.9999697  0.9792648  0.37596995
 0.4303156  0.9998034  0.8266549  0.48945454 0.48772153 0.41724226
 0.97758174 0.37798294 0.946606   0.44892925 0.4528625  0.4080135
 0.9864005  0.47868308 0.4947556  0.97442925 0.7441282  0.41769406
 0.9099068  0.54879254 0.9999448  0.4290502  0.99998236 0.43697938
 0.366292   0.8850466  0.96946645 0.41570675 0.9892543  0.46446204
 0.4998545  0.99979556 0.9232507  0.48889688 0.89270455 0.9999463
 0.9784005  0.99997234 0.999791   0.9999005  0.9189638  0.89739746
 0.99975383 0.40818354] [0. 1. 0. 0. 0. 0. 0. 1. 1. 0. 0. 0. 0. 0. 0. 1. 1. 1. 0. 0. 0. 0. 0. 1.
 0. 0. 0. 1. 1. 0. 0. 1. 0. 1. 0. 0. 0. 0. 1. 1. 0. 1. 1. 0. 0. 1. 0. 1.
 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0. 0. 1. 0. 0. 1. 0. 0. 0. 0.
 0. 1. 0. 1. 0. 0. 1. 0. 1. 0. 0. 1. 1. 0. 0. 1. 1. 1. 0. 1. 0. 1. 1. 1.
 0. 1. 1. 0. 0. 1. 0. 0. 0. 1. 0. 1. 1. 0. 0. 1. 0. 1. 1. 0. 0. 1. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 1.]
TRAIN 2021-09-19T20:12:59.546805: step 56800, loss 0.0451508, acc 0.921875
(0, 1, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 1, 1, 1, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 1, 1) [0.99997234 0.49534392 0.9999806  0.47268686 0.9422643  0.9382324
 0.5153953  0.47796285 0.5637852  0.5054728  0.4020668  0.47587752
 0.99993145 0.98172426 0.9883846  0.99912834 0.9999886  0.99999607
 0.99997467 0.95237964 0.45795846 0.9998294  0.42489606 0.9828798
 0.4081045  0.95271206 0.4583293  0.9593662  0.9999911  0.9999427
 0.9767794  0.999417   0.4474861  0.9999973  0.9992465  0.8821031
 0.99969816 0.9997933  0.999921   0.4292514  0.9999842  0.45342594
 0.43776384 0.4701893  0.3869383  0.9999578  0.99978054 0.9644568
 0.9995203  0.45009503 0.4672625  0.9999576  0.9999939  0.9103861
 0.99971896 0.9444025  0.9999638  0.51980186 0.8832062  0.4463673
 0.9980975  0.85435116 0.99208677 0.9929407  0.9999434  0.9999917
 0.445087   0.67918473 0.6658756  0.37369984 0.48470888 0.4655623
 0.9982626  0.51204216 0.42774132 0.999082   0.5376607  0.9404863
 0.41573066 0.91313136 0.7992074  0.9996425  0.5528397  0.99992204
 0.9999914  0.49133366 0.999958   0.9999313  0.94684106 0.7454152
 0.9997879  0.36981022 0.41256973 0.5395518  0.99616843 0.9999998
 0.999989   0.99993515 0.45297822 0.9999941  0.44980583 0.40849188
 0.55640364 0.41834244 0.9700262  0.9180224  0.9973495  0.949857
 0.94243354 0.9999955  0.39542085 0.81459284 0.99929494 0.9972109
 0.97524995 0.9998297  0.999401   0.99992853 0.5109101  0.98390615
 0.41705707 0.44592607 0.47862104 0.99999696 0.41607487 0.3776465
 0.8046052  0.40832713] [0. 1. 0. 1. 0. 0. 0. 1. 0. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0.
 1. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 1. 1. 1. 1. 0. 0. 0.
 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 1. 1.
 0. 0. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 1. 0. 0. 0.
 0. 0. 1. 0. 1. 1. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0.
 1. 1. 1. 0. 1. 1. 0. 1.]

real	48m41.867s
user	248m42.052s
sys	26m10.386s
```

Evaluation with open test...

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1632054265/checkpoints/model-56000 --vocab_filepath ./runs/1632054265/checkpoints/vocab --eval_filepath ./open-test.final.manual.word
...
...
...
0.9973602890968323
0.0019538868218660355
0.0011032548500224948
0.9993106126785278
0.015413553453981876
0.9994139671325684
0.9996687769889832
0.9999812841415405
0.9999819397926331
0.9999824166297913
0.9999828338623047
0.9999765753746033
0.9551821351051331
0.999980092048645
0.9999822378158569
0.9772554636001587
Accuracy: 0.486486

real	0m6.659s
user	0m6.869s
sys	0m1.290s
```

Evaluation with closed test...

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1632054265/checkpoints/model-56000 --vocab_filepath ./runs/1632054265/checkpoints/vocab --eval_filepath ./closed-test.word 
...
...
0.0010986969573423266
0.9970912337303162
0.0012275318149477243
0.024728016927838326
0.08713027089834213
0.0010856621665880084
0.0010486117098480463
0.022984491661190987
0.9361893534660339
0.04294361174106598
0.9948735237121582
0.000990169239230454
0.005071983207017183
0.00110618828330189
0.0031332301441580057
0.0013495823368430138
0.9438773393630981
0.0011586268665269017
0.0012747757136821747
0.9960055351257324
0.9999815821647644
0.9992577433586121
0.0012822076678276062
0.00120147957932204
0.0010955269681289792
Accuracy: 0.915

real	0m6.565s
user	0m6.961s
sys	0m1.298s
```

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-fasttext-max_doc-length15-batch_size128-hidden_units200-dropout0.6-epoch200-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-fasttext-max_doc-length15-batch_size128-hidden_units200-dropout0.6-epoch200-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "myWord-word", fasttext, max_document_length=15, Batch Size = 8, **--dropout_keep_prob 0.6**, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br> 
  
### training/validation with dropout 0.8

Training...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-word/all-para.fasttext.vector --embedding_dim 500 --dropout_keep_prob 0.8 --num_epochs 200 --batch_size 128 2>&1 | tee train-myWord-epoch200-fasttext-max-doc-length15-batch_size128-dropout0.8.19-sept2021.log
...
...
...
TRAIN 2021-09-19T21:57:59.301689: step 56799, loss 0.0350333, acc 0.945312
(0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 0, 1, 1, 0, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1) [0.8774608  0.44746765 0.9883107  0.9999027  0.9007726  0.9999232
 0.9924808  0.8885927  0.9895336  0.9799488  0.999994   0.938076
 0.9071175  0.8611088  0.9678341  0.35016742 0.48649937 0.3587404
 0.9623205  0.26708746 0.9998428  0.8871987  0.99890757 0.2876297
 0.9473133  0.9998266  0.9844121  0.2959227  0.3931273  0.99972993
 0.89269066 0.3284538  0.99997115 0.3443117  0.99995255 0.99995965
 0.9618344  0.99990034 0.31135347 0.36924332 0.9715765  0.3169097
 0.3110325  0.9997955  0.999454   0.36005813 0.99970436 0.28030285
 0.9998981  0.9648272  0.9091898  0.99981123 0.22953205 0.9999594
 0.27821705 0.99948436 0.9998181  0.27611056 0.9099229  0.37069738
 0.8928184  0.32204714 0.9999619  0.9687531  0.75299376 0.94023603
 0.9998167  0.2821813  0.99971396 0.9786713  0.9998146  0.9703577
 0.7765221  0.3951021  0.7967614  0.29331753 0.8679043  0.98341495
 0.35115153 0.9979647  0.33218265 0.89117795 0.9992612  0.38262963
 0.32616192 0.99897283 0.98161143 0.32572424 0.27940345 0.31261048
 0.9111179  0.36674014 0.99988335 0.30483177 0.27431616 0.813441
 0.98474634 0.28013554 0.31658486 0.9403555  0.8304533  0.3421268
 0.85822135 0.99737793 0.9512419  0.2598712  0.9997451  0.8248395
 0.3425826  0.9991504  0.8639615  0.4428084  0.98834133 0.28062367
 0.32704604 0.9614185  0.9027042  0.3485019  0.9988712  0.9698261
 0.9795596  0.9999441  0.999911   0.99891645 0.94362557 0.90777516
 0.9874103  0.3564288 ] [0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 1. 1. 0. 1. 0. 0. 0. 1.
 0. 0. 0. 1. 1. 0. 0. 1. 0. 1. 0. 0. 0. 0. 1. 1. 0. 1. 1. 0. 0. 1. 0. 1.
 0. 0. 0. 0. 1. 0. 1. 0. 0. 1. 0. 1. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0.
 0. 1. 0. 1. 0. 0. 1. 0. 1. 0. 0. 1. 1. 0. 0. 1. 1. 1. 0. 1. 0. 1. 1. 0.
 0. 1. 1. 0. 0. 1. 0. 0. 0. 1. 0. 0. 1. 0. 0. 1. 0. 1. 1. 0. 0. 1. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 1.]
TRAIN 2021-09-19T21:57:59.350807: step 56800, loss 0.0317684, acc 0.960938
(0, 1, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 1, 1, 1, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 1, 1) [0.99985665 0.27808684 0.9985655  0.30450964 0.8079662  0.99998415
 0.8788951  0.27573398 0.9258697  0.34792677 0.27251703 0.98507833
 0.9999877  0.9692795  0.99678564 0.968687   0.9997095  0.9998369
 0.999931   0.9388367  0.305751   0.99535525 0.33532017 0.9510985
 0.28795213 0.9629085  0.32703322 0.83118165 0.99974257 0.9998947
 0.9935075  0.9280968  0.32164636 0.93998814 0.99997723 0.85936844
 0.9697481  0.9999793  0.95087135 0.31131268 0.99994916 0.22292042
 0.4641393  0.35376084 0.8848051  0.9998466  0.97644037 0.85150504
 0.9719926  0.16909951 0.3112048  0.99936545 0.9996232  0.9997694
 0.99980485 0.84718996 0.99966633 0.8871662  0.9345399  0.27814993
 0.8632771  0.76879627 0.9378128  0.9984224  0.9978619  0.9999364
 0.3777619  0.9368904  0.9995374  0.3215669  0.2937857  0.33658645
 0.9955708  0.29619697 0.31126374 0.9455262  0.8836761  0.8199639
 0.37024814 0.9816995  0.8560109  0.9961681  0.3998207  0.9662595
 0.99967706 0.8850215  0.9998142  0.9998672  0.9023668  0.36091998
 0.9999185  0.28465164 0.39303884 0.32645267 0.99767864 0.99799675
 0.99994105 0.99971646 0.33505252 0.9982224  0.262892   0.32663053
 0.30073345 0.27840343 0.91447943 0.97083884 0.9986408  0.981179
 0.9768253  0.9997958  0.27518392 0.9977484  0.999865   0.9985462
 0.89961153 0.89474756 0.99715763 0.82340723 0.38651672 0.9795397
 0.3634785  0.3369148  0.4014937  0.9998737  0.29597372 0.35633108
 0.29960176 0.34156635] [0. 1. 0. 1. 0. 0. 0. 1. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0.
 1. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 1. 1. 1. 0. 0. 0. 0.
 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 1. 1.
 0. 1. 1. 0. 0. 0. 1. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 1. 1. 1. 0. 0.
 0. 0. 1. 0. 1. 1. 1. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 1. 0.
 1. 1. 1. 0. 1. 1. 1. 1.]

real	54m34.623s
user	248m39.200s
sys	31m33.550s
```

Evaluation with open test...

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1632060213/checkpoints/model-20000 --vocab_filepath ./runs/1632060213/checkpoints/vocab --eval_filepath ./open-test.final.manual.word 
...
...
...
0.9989233016967773
0.9991495013237
0.9991986155509949
0.9991160035133362
0.999006450176239
0.9991082549095154
0.9991894364356995
0.9992244839668274
0.8654000163078308
Accuracy: 0.47047

real	0m6.433s
user	0m6.985s
sys	0m1.214s
```

Evaluation with closed test...

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1632060213/checkpoints/model-20000 --vocab_filepath ./runs/1632060213/checkpoints/vocab --eval_filepath ./closed-test.word 
...
...
...
0.015915270894765854
0.8373597860336304
0.006046591326594353
0.006051730830222368
0.07427341490983963
0.9571735858917236
0.003378618974238634
0.44886720180511475
0.9922441840171814
0.9988714456558228
0.9862053990364075
0.005022414028644562
0.004893637262284756
0.003538074903190136
Accuracy: 0.94

real	0m6.650s
user	0m6.795s
sys	0m1.391s
```

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-fasttext-max_doc-length15-batch_size128-hidden_units200-dropout0.8-epoch200-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myWord-fasttext-max_doc-length15-batch_size128-hidden_units200-dropout0.8-epoch200-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "myWord-word", fasttext, max_document_length=15, Batch Size = 8, **--dropout_keep_prob 0.8**, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br> 

## Playing Hidden Layer

siamese_network_semantic.py ဖိုင်မှာ...  

```python
class SiameseLSTMw2v(object):
    """
    A LSTM based deep Siamese network for text similarity.
    Uses an word embedding layer (looks up in pre-trained w2v), followed by a biLSTM and Energy Loss layer.
    """
    
    def stackedRNN(self, x, dropout, scope, embedding_size, sequence_length, hidden_units):
        n_hidden=hidden_units
        n_layers=3
 ```

n_layers=6 ထားပြီး run ကြည့်ခဲ့...  

Training...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./train.py --nois_char_based --word2vec_model ./w2v_fasttext/mypara-word/all-para.fasttext.vector --embedding_dim 500 --num_epochs 200 --batch_size 128 2>&1 | tee train-myWord-epoch200-fasttext-max-doc-length15-batch_size128-n_layers6.20-sept2021.log
...
...
...
TRAIN 2021-09-20T01:47:31.012995: step 56799, loss 0.0175684, acc 0.960938
(0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 0, 1, 1, 0, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1) [0.9755353  0.02710504 0.99950075 0.99240553 0.9995317  0.9980001
 0.9914314  0.01404302 0.9620266  0.98563576 0.9994877  0.9191051
 0.9677719  0.99965405 0.9602045  0.02660101 0.05178836 0.04379741
 0.9994751  0.01585458 0.9996354  0.11637741 0.99143416 0.03155239
 0.9891281  0.99956685 0.9994327  0.9565669  0.01579263 0.9995635
 0.9969269  0.08028337 0.9913726  0.01997571 0.9994037  0.9996255
 0.99289006 0.9994721  0.00831199 0.02912706 0.9486243  0.01419155
 0.83953273 0.99956906 0.999459   0.01603404 0.99960726 0.99954575
 0.9875011  0.928913   0.9897533  0.9849492  0.01646035 0.99947035
 0.17379273 0.9996384  0.9995201  0.14994353 0.9670049  0.02899335
 0.83929014 0.03459416 0.99912727 0.97401035 0.96391714 0.9995891
 0.9844213  0.0263519  0.99942625 0.9982247  0.95575    0.9371042
 0.94848716 0.01352229 0.02858366 0.08552025 0.92958695 0.9129604
 0.01849387 0.9932805  0.09669479 0.9866546  0.93755966 0.020669
 0.01329142 0.9931194  0.9569492  0.01770849 0.03607322 0.14314564
 0.9307828  0.01030943 0.9741033  0.01733695 0.08779465 0.9871403
 0.98587656 0.03068013 0.0277773  0.9489542  0.9717834  0.01352115
 0.9871335  0.9885586  0.9996408  0.26877478 0.9995453  0.8472594
 0.00791825 0.99810404 0.96376234 0.02585378 0.9994085  0.01926701
 0.01709304 0.9635301  0.99918973 0.01694571 0.999529   0.9994869
 0.9343804  0.999637   0.9993037  0.9508317  0.99940234 0.96898407
 0.9995622  0.01500639] [0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 1. 1. 1. 0. 1. 0. 1. 0. 1.
 0. 0. 0. 0. 1. 0. 0. 1. 0. 1. 0. 0. 0. 0. 1. 1. 0. 1. 0. 0. 0. 1. 0. 0.
 0. 0. 0. 0. 1. 0. 1. 0. 0. 1. 0. 1. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0.
 0. 1. 1. 1. 0. 0. 1. 0. 1. 0. 0. 1. 1. 0. 0. 1. 1. 1. 0. 1. 0. 1. 1. 0.
 0. 1. 1. 0. 0. 1. 0. 0. 0. 1. 0. 0. 1. 0. 0. 1. 0. 1. 1. 0. 0. 1. 0. 0.
 0. 0. 0. 0. 0. 0. 0. 1.]
TRAIN 2021-09-20T01:47:31.077663: step 56800, loss 0.00952607, acc 0.976562
(0, 1, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 1, 1, 1, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 1, 1) [0.9996474  0.00534535 0.98989505 0.08177954 0.94818527 0.8557705
 0.21713915 0.01399366 0.92808354 0.02219464 0.01883885 0.92580146
 0.9995505  0.9156494  0.9811772  0.9996237  0.96283174 0.99965566
 0.999585   0.9543137  0.03173688 0.9994653  0.01063691 0.9657915
 0.01566869 0.9995456  0.02685113 0.999637   0.99967575 0.9995228
 0.95105606 0.9562811  0.03149823 0.9796914  0.9893623  0.8547356
 0.9994683  0.9387166  0.957204   0.00942579 0.99944925 0.05955359
 0.04420103 0.01740686 0.01935516 0.99927384 0.9997087  0.9752822
 0.97677296 0.50743043 0.01505104 0.9994601  0.9995073  0.97765505
 0.9716313  0.96188116 0.9995452  0.955208   0.99063957 0.07297046
 0.7335115  0.9209876  0.98790646 0.99924296 0.929541   0.9995002
 0.01675273 0.90384656 0.85249114 0.03177572 0.01493693 0.01798517
 0.9313957  0.840215   0.02443171 0.9747293  0.87406665 0.98972595
 0.01720359 0.9424642  0.98652494 0.9552945  0.02035582 0.999548
 0.9927863  0.0370243  0.95587885 0.986975   0.94922596 0.8884724
 0.94853914 0.01584998 0.10820074 0.01608972 0.99947864 0.9995707
 0.99950266 0.99948096 0.01528186 0.9609339  0.02275314 0.01614167
 0.06011584 0.0196424  0.8973115  0.93557507 0.99233794 0.9995645
 0.9995159  0.96503544 0.03633498 0.9709156  0.9994899  0.99382097
 0.98988545 0.8403808  0.91443497 0.96518993 0.02461713 0.9906137
 0.01671949 0.02192536 0.05545646 0.9996245  0.07933193 0.01614936
 0.07781927 0.0166619 ] [0. 1. 0. 1. 0. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0.
 1. 0. 1. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 1. 1. 1. 1. 0. 0. 0.
 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 1. 1.
 0. 0. 1. 0. 0. 0. 1. 0. 0. 0. 1. 0. 0. 1. 0. 0. 0. 0. 0. 1. 1. 1. 0. 0.
 0. 0. 1. 0. 1. 1. 1. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 1. 0.
 1. 1. 1. 0. 1. 1. 1. 1.]

real	68m1.208s
user	356m26.522s
sys	43m50.782s
```

Evaluation with open test data...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1632073182/checkpoints/model-55000 --vocab_filepath ./runs/1632073182/checkpoints/vocab --eval_filepath ./open-test.final.manual.word 
...
...
...
0.9998568892478943
0.01668265275657177
0.9998795390129089
0.9988184571266174
0.999839723110199
0.9998583793640137
0.9998182058334351
0.9996994733810425
0.546632707118988
0.997288703918457
0.9998788833618164
0.917654812335968
0.03667210787534714
Accuracy: 0.455455

real	0m10.309s
user	0m11.010s
sys	0m1.353s
```

Evaluation with closed test data...  

```
(paraphrase2) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara2/deep-siamese-text-similarity$ time python ./eval.py --model ./runs/1632073182/checkpoints/model-55000 --vocab_filepath ./runs/1632073182/checkpoints/vocab --eval_filepath ./closed-test.word
...
...
...
0.01367015391588211
0.029039530083537102
0.026714330539107323
0.9998959302902222
0.027314158156514168
0.047084990888834
0.9956732392311096
0.9999219179153442
0.9874526262283325
0.06668917834758759
0.02529512345790863
0.018707364797592163
Accuracy: 0.958

real	0m10.558s
user	0m11.061s
sys	0m1.365s
```

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/nlayers6-accuracy.png" width="300" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/nlayers6-loss.png" width="300" /> 
</p>
<div align="center">
  Fig. Training and Validation Result with "myWord-word", fasttext, max_document_length=15, Batch Size = 8, **--dropout_keep_prob 0.6**, 200 epoch. Left: Accuracy, Right: Loss
</div>   
  </br> 
  
## Hack eval.py and Thinking

model တွေကို training လုပ်ရင်း စဉ်းစားမိတာတွေကို ချရေးထားခဲ့...  

eval.py မှာက coding က အောက်ပါအတိုင်း...   

```python
        # Collect the predictions here
        all_predictions = []
        all_d=[]
        for db in batches:
            x1_dev_b,x2_dev_b,y_dev_b = zip(*db)
            batch_predictions, batch_acc, batch_sim = sess.run([predictions,accuracy,sim], {input_x1: x1_dev_b, input_x2: x2_dev_b, input_y:y_dev_b, dropout_keep_prob: 1.0})
            all_predictions = np.concatenate([all_predictions, batch_predictions])
            print(batch_predictions)
```
            
"batch_sim" ကို print ထုတ်ကြည့်ပြီး လေ့လာရန်။  

training တုန်းက coding က အောက်ပါအတိုင်း  

```python
            feed_dict = {
                siameseModel.input_x1: x2_batch,
                siameseModel.input_x2: x1_batch,
                siameseModel.input_y: y_batch,
                siameseModel.dropout_keep_prob: FLAGS.dropout_keep_prob,
            }
        _, step, loss, accuracy, dist, sim, summaries = sess.run([tr_op_set, global_step, siameseModel.loss, siameseModel.accuracy, siameseModel.distance, siameseModel.temp_sim, train_summary_op],  feed_dict)
        time_str = datetime.datetime.now().isoformat()
        print("TRAIN {}: step {}, loss {:g}, acc {:g}".format(time_str, step, loss, accuracy))
        train_summary_writer.add_summary(summaries, step)
        print(y_batch, dist, sim)
```

output ကို ကြည့်ရင် အောက်ပါအတိုင်း...   

```
TRAIN 2021-09-19T14:34:42.147274: step 31429, loss 0.00459611, acc 0.992188
(1, 1, 1, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 1, 1, 1, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 1, 0, 0, 0, 1, 1, 0, 0, 0, 1, 1, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 1, 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 1, 0, 0, 1, 1, 1) [0.13571483 0.15750377 0.01232103 0.99774694 0.9999297  0.99999523
 0.0186371  0.01254055 0.99997187 0.99972963 0.9399145  0.9999453
 0.9946073  0.985404   0.98289347 0.999998   0.01486034 0.9999639
 0.98403805 0.03449004 0.02151816 0.9586517  0.9995968  0.00482136
 0.00630763 0.03047854 0.980725   0.01996006 0.9991037  0.9813261
 0.9999416  0.9999971  0.9710663  0.99999815 0.00386708 0.89505875
 0.9998986  0.9735444  0.05214329 0.9908545  0.9999967  0.01630748
 0.00926793 0.00325864 0.04387594 0.99957997 0.03695309 0.98522085
 0.9617969  0.99993134 0.01108018 0.92042726 0.9994914  0.9995199
 0.9283887  0.01761526 0.9745685  0.99999595 0.93862104 0.00776012
 0.02091951 0.99998873 0.96473116 0.99869454 0.05147315 0.01240575
 0.02433388 0.01989828 0.9999977  0.9999955  0.99910563 0.0090289
 0.999955   0.9951485  0.99995303 0.9861572  0.02171431 0.9999884
 0.00434535 0.99996036 0.999919   0.9675294  0.9999974  0.01992809
 0.9986063  0.02074391 0.99966615 0.9700154  0.9286931  0.06214102
 0.9683462  0.9981848  0.9837354  0.07322868 0.98861104 0.99998575
 0.9999896  0.02857984 0.05907594 0.9999755  0.00731123 0.99999726
 0.9731104  0.15855333 0.00484825 0.9999951  0.99999213 0.98983485
 0.9756117  0.9982806  0.02623191 0.00690353 0.9999961  0.999958
 0.03110681 0.9998352  0.01771471 0.00406088 0.01756511 0.08012437
 0.9999616  0.9642646  0.01661208 0.9600833  0.8737765  0.01750395
 0.04282009 0.00349833] [1. 1. 1. 0. 0. 0. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 1. 1. 0. 0. 1.
 1. 1. 0. 1. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 1. 0. 0. 1. 1. 1. 1. 0. 1. 0.
 0. 0. 1. 0. 0. 0. 0. 1. 0. 0. 0. 1. 1. 0. 0. 0. 1. 1. 1. 1. 0. 0. 0. 1.
 0. 0. 0. 0. 1. 0. 1. 0. 0. 0. 0. 1. 0. 1. 0. 0. 0. 1. 0. 0. 0. 1. 0. 0.
 0. 1. 1. 0. 1. 0. 0. 1. 1. 0. 0. 0. 0. 0. 1. 1. 0. 0. 1. 0. 1. 1. 1. 1.
 0. 0. 1. 0. 0. 1. 1. 1.]
```

ဒီ code  ```print("TRAIN {}: step {}, loss {:g}, acc {:g}".format(time_str, step, loss, accuracy))```python ရဲ့ output က    
```TRAIN 2021-09-19T14:34:42.147274: step 31429, loss 0.00459611, acc 0.992188```  

ဒီ code  ```print(y_batch, dist, sim)```python ရဲ့ output က အထက်မှာ မြင်နေရတဲ့ တသီတတန်း list တွေ...  
အဲဒါကြောင့် ငါနားလည်တာက distance က သိပ်မကွာရင် (i.e. တန်ဖိုးငယ်ရင်) similarity က 1 အနေနဲ့ decision လုပ်ပြီးတော့၊ distance က အရမ်းကွာရင် similarity ကို 0 အနေနဲ့ decision လုပ်သွားတာ...   

တကယ်က paraphrase က distance တစ်ခုတည်းနဲ့တော့ တိုင်းလို့ မရဘူး...   
လက်ရှိ Deep Siamese NN မှာ သူတို့ သုံးပြထားတဲ့ ဒေတာက paraphrase အတွက် မဟုတ်ဘူး... 
README ဖိုင်ထဲမှာ ရေးထားတာတွေကို ပြန်ဖတ်ကြည့်ရင် အောက်ပါအတိုင်း ရေးထားတယ်...  

```
Given adequate training pairs, this model can learn Semantic as well as structural similarity. For eg:  

Phrases :

International Business Machines = I.B.M
Synergy Telecom = SynTel
Beam inc = Beam Incorporate
Sir J J Smith = Johnson Smith
Alex, Julia = J Alex
James B. D. Joshi = James Joshi
James Beaty, Jr. = Beaty
For phrases, the model learns character based embeddings to identify structural/syntactic similarities.

Sentences :

He is smart = He is a wise man.
Someone is travelling countryside = He is travelling to a village.
She is cooking a dessert = Pudding is being cooked.
Microsoft to acquire Linkedin ≠ Linkedin to acquire microsoft
(More examples Ref: semEval dataset)

For Sentences, the model uses pre-trained word embeddings to identify semantic similarities.
```

သူတို့ သုံးထားတဲ့ စာကြောင်းတွေက string similarity နဲ့တင်လုံလောက်နိုင်တယ်။ အထူးသဖြင့် Phrase level မှာ...   
သူတို့ရဲ့ README ဖိုင်မှာလည်း အောက်ပါအတိုင်း mention လုပ်ထားတယ်။   

```
Categories of pairs, it can learn as similar:

Annotations
Abbreviations
Extra words
Similar semantics
Typos
Compositions
Summaries
```

ငါတို့ရဲ့ မြန်မာစာ paraphrase စာကြောင်း ဒေတာကို ပြန်ကြည့်ကြည့်ရအောင်။  validation.txt0 ဖိုင်ကနေ ယူလာခဲ့...    

```
0	ဒီ အပတ် ထဲ မှာ လျှော် မှာ ပါ ကွ ။	ကျွန်​​တော် ဘတ်စ်ကား စီး သင့် သလား ။
1	ယခု ကာလ ခြစ်ခြုတ် သုံးစွဲ ခြင်း မ ရှိ ကြ ၍ အခက်အခဲ ဖြစ် ကြ သည် ။	ယခု ကာလ ခြိုးခြံ သုံးစွဲ ခြင်း မ ရှိ ကြ ၍ အခက်အခဲ ဖြစ် ကြ သည် ။
0	ကျွန်တော့် အတွက် ဂုဏ်ပကာသန တွေ ဟာ အရေး မ ပါ ပါ ဘူး ။	ကျွန်တော့် မိဘ တွေ က ဂုဏ်ပကာသန တွေ ပြ တာ မ ကြိုက် ဘူး ။
0	မင်း ဒီ မှာ ရှိ တာ ငါ ဝမ်းသာ တယ် ။	သူ မ ငါ့ ကို သတိ မ ရ ခဲ့ ဘူး လား ။
0	ဆရာ ကြီး သဘောကျ ဖို့ သူ ကြိုးစား နေ တယ် ။	ဆရာ ကြီး က တော့ တော်တော် သဘောကျ သွား ပြီ ။
0	ကျွန်တော့် ကို ပုံစံ အမှား တွေ ပေး လိုက် လို့ ။	ဘယ် ရ ထား စီး ခဲ့ သလဲ ။
1	သူ တို့ တွေ ဟာ အသွင်အပြင် ၊ အသွင်သဏ္ဌာန် အတော် တူ ပါ တယ် ။	သူ တို့ တွေ ဟာ အသွင်အပြင် ၊ ပုံပန်းသဏ္ဌာန် အတော် တူ ပါ တယ် ။
0	ဒီ လို မ ကြာ မ ကြာ အတူ စား ကြ ရ အောင် ။	ငါ တို့ မင်း ကို ကျေးဇူးတင် တယ် ။
0	လိုအပ် တဲ့ နေ ရာ မှာ ကော်မာ တစ် ခု ထည့် ရ မယ် ။	ကော် တွေ က ကြာ တော့ မာ သွား ပြီ ။
1	ကုသိုလ် လုပ် ဖို့ မ တွန့်ဆုတ် ကြ ပါ နဲ့	ကုသိုလ် လုပ် ရ မှာ မ ကြောက် ကြ နဲ့
1	လျှပ်စစ်မီး အိမ် သည် ဖယောင်းတိုင် ထက် ပို ၍ လင်းလက် သည် ။	လျှပ်စစ်မီး အိမ် သည် ဖယောင်းတိုင် ထက် ပို ၍ လင်း သည် ။
1	ငါ ဈေး ရင်း ပေး ပါ့ မယ် ။	ငါ ရင်းနှီး ပေး ပါ့ မယ် ။
1	တစ်ဖက်ကမ်း သို့ လှ ေသမ္ဗန် လှော် သွား သည် ။	တစ်ဖက်ကမ်း သို့ လှ ေသမ္ဗန် လှော်ခတ် သွား သည် ။
1	ရှိ ခိုး ဖူးမြော် ကန် တော့ ပါ ၏	ကန် တော့ ဝန် ချ ပါ ၏
0	သူ မ က မ ဆင်ခြင် မ စဉ်းစား ဘူး ။	သူ တို့ ဘာ တွေ များ ကျေနပ် နေ ကြ သလဲ ။
0	တစ် ခု တော့ ဆိုးဆိုးရွားရွား ဖြစ် နေ ပြီ ထင် တယ် ။	ကိုယ် မင်း ကို ဒုက္ခ ပေး လိုက် လား ။
0	ကျ ပန်း အလုပ် တစ် ရက် လောက် လုပ် ပြီး ရင် နှစ် ရက် လောက် အလုပ် ပြန် ရှာ ရ တယ် ။	ကျွန်တော့် အဖေ နဲ့ ကျွန်တော် ဟာ ပို ပြီး စိုးရိမ် လာ ပါ တယ် ။
0	အသံ လေး ချဲ့ ပေး လိုက် ပါ ဦး ။	ကျေးဇူးပြုပြီး မင်း ရဲ့ လေယာဉ် တက် လက်မှတ် ကြည့် ပါ ရ စေ ။
0	ကျွန်တော် ကျွန်တော့် သူငယ်ချင်း တွေ ကို မ တွေ့ ရဲ ဘူး ။	ကျွန်တော် ကျွန်တော့် သူငယ်ချင်း တွေ ကို သွား တွေ့ မ လို့ ။
0	ကျွန်တော့် ဆီ လာ တဲ့ မှာ ကြား စာ ရှိ ပါ သလား ။	ကျွန်တော် မှာ ကြား စာ ပို့ လိုက် ပါ မယ် ။
...
...
1	အားပေး နေ ပါ တယ်	အားပေး မယ်
0	သူ က လူ ကြီး သူ မ ရှေ့ ဆို စကား ကို ယဉ်ကျေး စွာ အမြဲ ပြော တယ်	လူ ကြီး သူ မ ရှေ့ စကား ကို ယဉ်ကျေး စွာ ပြော ဖို့ သူ့ ကို ဖျောင်းဖျ ပါ
0	အဲ့ဒါ ကို ကျွန်တော် ယူ ခဲ့ မိ သလား ။	မင်း ဒုက္ခ တွေ ကို သည်းမခံ နိုင် ဘူး လား ။
1	ကျွန်မ ရင် ထဲ မှာ စူးနစ် သွား သည် ။	ကျွန်မ ရင် ထဲ မှာ နာကျင် သွား သည်
0	ဆက် ပြီး ကြိုးစား ချင် စိတ် မ ရှိ တော့ ဘူး	ဆက် ပြီး ကြိုးစား လိုက် ကြ ပါ ဦး
0	ဒီ အဖု လေး ကွာ နိုင် လား ။	ဘယ် မှာ ခင်ဗျား ထား ခဲ့ လို့ လဲ ။
1	ဘယ် လား ညာ လား ။	ဘယ် ဘက် လား ညာ ဘက် လား ။
1	ကြည့် ရ တာ ဝမ်းသာ စရာ ပါ	ကြည့် ရ တာ ပျော် စရာ ပါ
0	ဒိုင် အရမ်း ညစ် တယ်	ဒိုင် က အရမ်း မှား တယ်
0	အလှဆင် ထား တဲ့ အိမ် တွေ ။	သိပ် ကို ကောင်း မယ့် အကြံ ပဲ ။
...
...
1	ရှိ ခိုး ပူဇော် ဖူးမြော် ပါ ၏	ရှိ ခိုး ပူဇော် ကန် တော့ ပါ ၏
0	ဒီ အရ သာ က ဖရဲသီး နဲ့ အရ သာ တူ တယ် ။	တစ် ကြိမ် ဘယ်လို ဆို တာ သိ သွား ရင် အလွယ် လေး ပေါ့ ။
1	ရှိ ခိုး ဖူးမြော် ကန် တော့ ပါ ၏	ဦး ခိုက် ပါ တယ်
1	အရာရာ တော့ မ ကောင်း နိုင် ဘူး လေ ။	အရာ အားလုံး တော့ မ ကောင်း နိုင် ဘူး လေ ။
0	အရမ်း ဆိုး တယ်	အရမ်း ကောင်း တယ်
```

**meaning of word:**  

```
0	အလှဆင် ထား တဲ့ အိမ် တွေ ။	သိပ် ကို ကောင်း မယ့် အကြံ ပဲ ။
0	ဒိုင် အရမ်း ညစ် တယ်	ဒိုင် က အရမ်း မှား တယ်
0	သူ က လူ ကြီး သူ မ ရှေ့ ဆို စကား ကို ယဉ်ကျေး စွာ အမြဲ ပြော တယ်	လူ ကြီး သူ မ ရှေ့ စကား ကို ယဉ်ကျေး စွာ ပြော ဖို့ သူ့ ကို ဖျောင်းဖျ ပါ
1	ရှိ ခိုး ဖူးမြော် ကန် တော့ ပါ ၏	ဦး ခိုက် ပါ တ
```

**word overlapping:**  

```
1	ကုသိုလ် လုပ် ဖို့ မ တွန့်ဆုတ် ကြ ပါ နဲ့	ကုသိုလ် လုပ် ရ မှာ မ ကြောက် ကြ နဲ့
1	ငါ ဈေး ရင်း ပေး ပါ့ မယ် ။	ငါ ရင်းနှီး ပေး ပါ့ မယ် ။
1	တစ်ဖက်ကမ်း သို့ လှ ေသမ္ဗန် လှော် သွား သည် ။	တစ်ဖက်ကမ်း သို့ လှ ေသမ္ဗန် လှော်ခတ် သွား သည် ။
1	ယခု ကာလ ခြစ်ခြုတ် သုံးစွဲ ခြင်း မ ရှိ ကြ ၍ အခက်အခဲ ဖြစ် ကြ သည် ။	ယခု ကာလ ခြိုးခြံ သုံးစွဲ ခြင်း မ ရှိ ကြ ၍ အခက်အခဲ ဖြစ် ကြ သည် ။
1	ဘယ် လား ညာ လား ။	ဘယ် ဘက် လား ညာ ဘက် လား ။
1	အားပေး နေ ပါ တယ်	အားပေး မယ်
1	ကျွန်မ ရင် ထဲ မှာ စူးနစ် သွား သည် ။	ကျွန်မ ရင် ထဲ မှာ နာကျင် သွား သည်
```

**ending:**

```
0	ကျွန်တော့် ဆီ လာ တဲ့ မှာ ကြား စာ ရှိ ပါ သလား ။	ကျွန်တော် မှာ ကြား စာ ပို့ လိုက် ပါ မယ် ။
0	အရမ်း ဆိုး တယ်	အရမ်း ကောင်း တယ်
```

တကယ်က word overlapping တစ်ခုတည်းနဲ့တောင် တော်တော်များများသော မြန်မာစာကြောင်းတွေကို paraphrase or not ဆုံးဖြတ်လို့ ရတယ်။  
*** တကယ်ကတော့ word2vec, fasttext တွေက usage, frequency, corpus ပေါ်မူတည်ပြီး အဓိပ္ပါယ်ဆွဲထုတ်နိုင်တယ်ဆိုတာကို သက်သေပြထားတယ်။ ငါတို့ လက်ရှိ word2vec, fasttext မော်ဒယ်တွေက myPara corpus နဲ့ ပဲ ဆောက်ထားတာဆိုတော့ ဒေတာပမာဏ အားဖြင့်က နည်းတော့ အဓိပ္ပါယ်ကို ဘယ်လောက်ထိ ဆွဲထုတ်နိုင်သလဲ ဆိုတာကလည်း ပြဿနာဖြစ်နေတယ်။ myWord corpus ပါ ပေါင်းလိုက်ရင်တော့ အပြောင်းအလဲ ရှိနိုင်တယ်။ အဲဒါကတော့ လုပ်ကို လုပ်ရမယ်...  

**နောက်တစ်ခုက Siamese Network နဲ့ meaning ဆိုတာကို ယူပြီးတော့ ကျန်တဲ့ factor တွေကို rule နဲ့ ထပ်ဖြည့်ပြီး final decision လုပ်တာမျိုး...** 

paraphrae အပေါ်မှာ ရှိနေတဲ့... word2vec နဲ့ fasttext နှစ်ခုအကြား distance ကို နှိုင်းယှဉ်ကြည့်ရင်ကော... ?!  

Ensemble method တစ်ခုဖြစ်တဲ့ Random Forest (from sklearn.ensemble import RandomForestClassifier) လို traditional classifier က အောက်ပါအတိုင်း ဒေတာကို ပြင်ဆင်ဖို့ လိုအပ်...   

```
X=[[165,19],[175,32],[136,35],[174,65],[141,28],[176,15],[131,32],[166,6],[128,
32],[179,10],[136,34],[186,2],[126,25],[176,28],[112,38],[169,9],[171,36],[116,
25],[196,25]]
Y =
['Man','Woman','Woman','Man','Woman','Man','Woman','Man','Woman','Man','Woman',
'Man','Woman','Woman','Woman','Man','Woman','Woman','Man']
data_feature_names = ['height','length of hair']
X_train, X_test, Y_train, Y_test = cross_validation.train_test_split(X, Y,
test_size=0.40, random_state=5)
```

Feature တွေကို လူက လုပ်ပေးတာ မဟုတ်ပဲနဲ့ pattern တစ်ခု သတ်မှတ်ပြီး auto ဆွဲထုတ်ပြီး paraphrase အနေနဲ့ training လုပ်ကြည့်ရင်ကော?!  
ဥပမာ feature တွေအနေနဲ့ အထက်မှာ စဉ်းစားခဲ့သလို    

  - no. of. overlap words, 
  - lev distance, 
  - cosine distance, 
  - extended edit distance, 
  - BLEU, 
  - RIBES, 
  - chrF++
  - WER
  - word2vec similarity
  - fasttext similarity
 
စတဲ့ feature အမျိုးမျိုး combination လုပ်ပြီး traditional classifier ဆောက်ကြည့်ရင်ကော.... ?!   
အောက်ပါ လိုမျိုး calculation ကတော့ အလွယ်ဆုံးပေါ့လေ...   

  - sentence length difference (i.e. char),
  - no. of syllable difference 
  - no. of myWord difference
  
Random Forest ရဲ့ "feature_importance module" ကိုသုံးပြီးတော့ visualization graph ထုတ်ကြည့်ရင် ဘယ် feature တွေက paraphrase ဖြစ်တယ် မဖြစ်ဘူး ဆိုတဲ့ decision အတွက် အသုံးဝင်ကြောင်းပါ ရှင်းရှင်းလင်းလင်း မြင်ရနိုင်တယ်။   

အဲဒါနဲ့ ရလဒ်ကောင်းရင် အဲဒီ ဒေတာကို သုံးပြီးမှ Siamese NN နဲ့ training လုပ်တာက လက်ရှိအတိုင်း မြန်မာစာစာကြောင်းကို ထည့်ပြီး word2vec, fasttext စတဲ့ word representation တွေအပေါ်ကို မူတည်ပြီးတော့  ပိုတောင်ကောင်းမလား?!  
paper ရေးဖို့လည်း ပိုကောင်းသွားလိမ့်မယ်။    

-----------

## write a shell script

အထက်မှာ စဉ်းစားထားခဲ့တာကို အကောင်အထည်ဖော်တဲ့ အနေနဲ့ string similarity distance တွေနဲ့ပဲ ဖြည့်ထားပြီး forest tree နဲ့ classification လုပ်တာကို စမ်းကြည့်ပြီး ရလဒ်တွေကို ကြည့်ချင်တယ်။  
အဲဒီအတွက် harry string similarity တိုင်းတဲ့ tool ကို သုံးခဲ့တယ်။  
ထုံးစံအတိုင်းပဲ preprocessing, formatting ကိစ္စတွေ လုပ်ဖို့ လိုအပ်လို့ bash script ကို အောက်ပါအတိုင်း ရေးခဲ့...  

ဖိုင်နာမည်က "mk-distance-csv.sh"  

```bash
#!/bin/bash

# for getting all distances of "harry string similarity tool"
# written by Ye, LST, NECTEC, Thailand
# 20 Sept 2021

cut -f3 $1 > label.txt

cut -f1,2 $1 | sed -e 'y/\t/\n/' > ./para.tmp

count=($(wc ./para.tmp));

# clean previous calculated files
rm {dist_,sim_,kern}*.txt;

for distance in {dist_bag,dist_compression,dist_damerau,dist_hamming,dist_jaro,\
dist_jarowinkler,dist_kernel,dist_lee,dist_levenshtein,dist_osa,\
kern_distance,kern_spectrum,kern_subsequence,kern_wdegree,sim_braun,\
sim_dice,sim_jaccard,sim_kulczynski,sim_otsuka,sim_simpson,sim_sokal}
do
    # bash ပုံမှန် တွန့်ကွင်းနဲ့ looping ပတ်တဲ့အခါမှာ eval တို့ seq တို့ကို သုံးရတာမို့ C style နဲ့ပဲ သုံးခဲ့
    for (( i = 0; i < $count-1; i+=2 )) 
    do 
        # harry -x 0:1 -y 1:2
        #echo "$i:$(( $i+1 )) -y $(( $i+1 )):$(( $i+2 )):";
        harry -q -m $distance -x $i:$(( $i+1 )) -y $(( $i+1 )):$(( $i+2 )) ./para.tmp - | grep -v "#" >> $distance.txt
    done
done

paste {dist_bag,dist_compression,dist_damerau,dist_hamming,dist_jaro,\
dist_jarowinkler,dist_kernel,dist_lee,dist_levenshtein,dist_osa,\
kern_distance,kern_spectrum,kern_subsequence,kern_wdegree,sim_braun,\
sim_dice,sim_jaccard,sim_kulczynski,sim_otsuka,sim_simpson,sim_sokal}.txt ./label.txt -d "," > all_distance.txt

echo "wc all_distance.txt:"
wc all_distance.txt

echo "head all_distance.txt:"
head all_distance.txt

rm ./label.txt;
rm ./para.tmp;
```

## make features CSV file

အထက်ပါ bash script နဲ့ labeled paraphrase စာကြောင်း ၁၀ ကြောင်းဖိုင်ကို သုံးပြီး feature CSV ဖိုင်တာကို run ကြည့်ခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ bash ./mk-distance-csv.sh ./mypara-10lines.txt 
wc all_distance.txt:
  10   10 1455 all_distance.txt
head all_distance.txt:
16,0.146341,16,89,0.166014,0.0996083,164.333,6000,16,16,11918.5,243,0.000263601,26.6667,0.956522,0.956522,0.916667,0.956522,0.956522,0.956522,0.846154,1
23,0.506944,38,61,0.289805,0.231844,129.667,3508,38,38,7598,98,0.000111681,23,0.73913,0.755556,0.607143,0.755929,0.755742,0.772727,0.435897,0
17,0.463918,43,115,0.216625,0.1733,255,7241,43,43,23726,387,0.000447501,26.3333,0.777778,0.807692,0.677419,0.808889,0.80829,0.84,0.512195,0
17,0.188119,20,41,0.0711534,0.0426921,71.3333,3053,20,20,23607.5,509,0.000551857,117.667,0.892857,0.925926,0.862069,0.927198,0.926562,0.961538,0.757576,0
9,0.288136,9,31,0.14945,0.0896699,62,2047,9,9,3563.5,77,8.4394e-05,28.3333,0.777778,0.848485,0.736842,0.855556,0.852013,0.933333,0.583333,1
16,0.393617,16,26,0.218734,0.13124,44.3333,1799,16,16,1396.5,30,3.23094e-05,15.6667,0.785714,0.785714,0.647059,0.785714,0.785714,0.785714,0.478261,0
11,0.230769,12,17,0.0807298,0.0484379,30.3333,1206,12,12,6189.5,157,0.000178442,63.1667,0.777778,0.823529,0.7,0.826389,0.824958,0.875,0.538462,1
16,0.4375,18,46,0.240478,0.168335,80.3333,3365,18,18,1946,50,5.94379e-05,4.16667,0.769231,0.833333,0.714286,0.839161,0.836242,0.909091,0.555556,0
44,0.346591,46,114,0.21214,0.127284,194.333,8106,46,46,16482.5,361,0.000420554,32.6667,0.857143,0.878049,0.782609,0.878571,0.87831,0.9,0.642857,1
13,0.358824,37,81,0.161302,0.0967811,166,5205,37,37,12700.5,218,0.000258249,29.3333,0.8,0.869565,0.769231,0.87619,0.872872,0.952381,0.625,0
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$
```

တကယ် run ဖို့အတွက်ကတော့ myPara corpus တစ်ခုလုံးနဲ့ ဆောက်ဖို့ လိုအပ်တယ်။  

## Building String Similarity Feature File with the Whole Corpus

အကြမ်းမျဉ်းအားဖြင့် အလုပ်လုပ်မလုပ် သိချင်တော့ training ဖိုင်နဲ့ open-test ဖိုင်နှစ်ခုကို ပေါင်းလိုက်ပြီး test run လုပ်ကြည့်မယ်။
အဲဒီအတွက် myWord segmentation ဖြတ်ထားတဲ့ myPara corpus ဖိုင်တွေကို ပြင်ဆင်ခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara3/data/original$ wc *
   1000   18272  203625 closed-test.word
   1000   13766  139640 open-test.final.manual.word
  40461  764288 8442342 train.txt
  42461  796326 8785607 total
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara3/data/original$ head -3 *
==> closed-test.word <==
1	ကောင်း လိုက် တဲ့ သတင်း လေး ပါ	ကောင်း သော သတင်း ပါ ပဲ
0	ခု ဒီ တံဆိပ် က ဈေး လိုက် နေ တယ် ။	ဒီ တံဆိပ် က ဈေး အရမ်း တက် နေ တယ် ။
1	ကျွန်မ ဘက် က စ ပြီး ကျေအေး ပေး တယ် နော်	ကျွန်မ ဘက် က စ ပြီး ကျေလည် တာ နော်

==> open-test.final.manual.word <==
0	၁၁ ဒေါ်လာ ကျ ပါ တယ် ။	၁၁ နာရီ လာ ခေါ် မယ် ။
0	၁၁ နာရီ ခွဲ အိမ် ပြန် မယ် ။	၁၁ နာရီ ခွဲ အရောက် လာ ပါ ။
0	၁၁:၃၀ ပြန် ရောက် မယ် လို့ ထင် သလား ။	၁၁:၃၀ အတိ မှာ ပြန် ရောက် လာ ခဲ့ တယ် ။

==> train.txt <==
ကျွန်တော် စီး ဖို့ ချစ် စရာ ဖိနပ် တစ် ရံ ကို ရှာ မ တွေ့ လို့ ပါ ။	တစ်ခါတစ်ခါ ကျွန်တော် က ခင်ဗျား ကို အရမ်း အပြောင်းအလဲ များ တဲ့ လူ လို့ ထင် မိ တယ် ။	0
ကျေးဇူး ပဲ ၊ ကျွန်တော် ဘယ်လောက် ပေး ရ မ လဲ ။	ကျေးဇူး နော် ၊ ဘယ် တော့ ပြန် တွေ့ ကြ မ လဲ ။	0
ကျေးဇူး အများကြီး တင် ပါ တယ် ။	ကျေးဇူးတင် တယ် လို့ မ ပြော သွား ဘူး ။	0
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara3/data/original$ 
```

open-test ဒေတာရဲ့ format ကို training data ရဲ့ format နဲ့ တူအောင်အောက်ပါအတိုင်း ညှိခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara3/data/original$ cut -f1 open-test.final.manual.word > f1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara3/data/original$ cut -f2,3 ./open-test.final.manual.word > f23
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara3/data/original$ paste f23 f1 > open-test.formatted
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara3/data/original$ rm f23 f1
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara3/data/original$ head open-test.formatted 
၁၁ ဒေါ်လာ ကျ ပါ တယ် ။	၁၁ နာရီ လာ ခေါ် မယ် ။	0
၁၁ နာရီ ခွဲ အိမ် ပြန် မယ် ။	၁၁ နာရီ ခွဲ အရောက် လာ ပါ ။	0
၁၁:၃၀ ပြန် ရောက် မယ် လို့ ထင် သလား ။	၁၁:၃၀ အတိ မှာ ပြန် ရောက် လာ ခဲ့ တယ် ။	0
၂ မိုင် ထက် ပို ရှည် တယ် ။	၂ မိုင် လောက် သွား ရ တယ် ။	0
၄ ရက် အတွင်း အိမ် ပြန် မယ် ။	၄ ရက် လောက် နေ ရင် ပြန် လာ ပါ ။	0
၅ ဒေါ်လာ ထက် ပို ပါ တယ် ။	၅ ဒေါ်လာ လောက် ကျ သင့် တယ် ။	0
၅ ဒေါ်လာ ထက် နဲ ပါ တယ် ။	၅ ဒေါ်လာ ဆို နဲ ပါ တယ် ။	0
၅ ဒေါ်လာ ပဲ ရှိ တယ် ။	၅ ဒေါ်လာ လောက် ရှိ လား ။	0
၅ လမ်း က စားသောက်ဆိုင် မှာ စား ချင် တယ် ။	၅ လမ်း မှာ စားသောက်ဆိုင် ရှိ လား ။	0
ကျေးဇူးပြုပြီး မီနူး ရ နိုင် မ လား ။	ကျေးဇူးပြုပြီး မီနူး ထဲ က အတိုင်း ရ နိုင် မ လား ။	0
```

all.txt ဆိုပြီးတော့ train.txt ဖိုင်နဲ့ format ညှိထားတဲ့ open-test ဒေတာဖိုင် နှစ်ဖိုင်ကို ပေါင်းခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara3/data/original$ cat ./train.txt open-test.formatted > all.txt
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara3/data/original$ wc train.txt
  40461  764288 8442342 train.txt
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara3/data/original$ wc open-test.formatted 
  1000  13766 139640 open-test.formatted
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara3/data/original$ wc all.txt 
  41461  778054 8581982 all.txt
```

အဲဒီ all.txt ဖိုင် (the whole paraphrase corpus) ကို harry string similarity tool ရှိတဲ့ ဖိုလ်ဒါအောက်ကို ရွှေ့ပြီးတော့ string similarity distance တွေ အားလုံးကို တိုင်းခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ time bash mk-distance-csv.sh ./all.txt 
```

ညဘက် run ထားခဲ့ပြီးတော့ နောက်နေ့ မနက်ရောက်တော့ စုစုပေါင်း လေးသောင်းကျော်ရှိတဲ့ (တကယ်ကတော့ နှစ်သောင်းကျော် para, no-para အတွဲ) corpus ကို distance တွက်တာက ၅မျိုးပြီးနေခဲ့... ကျန်တာတွေကတော့ ဆက်တွက်နေဆဲ...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry$ wc *.txt
       2        9      111 2lines.txt
      10       10     1455 all_distance.txt
   41461   778054  8581982 all.txt
   41461    41461   118314 dist_bag.txt
   41461    41461   357386 dist_compression.txt
   41461    41461   121785 dist_damerau.txt
   41461    41461   132294 dist_hamming.txt
   41461    41461   373345 dist_jaro.txt
   30136    30136   278879 dist_jarowinkler.txt
   41461    41460    82921 label.txt
      11       19      396 matrix.txt
      10      187     1985 mypara-10lines.txt
  320396  1057180 10050853 total
```

အထက်ပါ wc ရလဒ်အရဆိုရင် လက်ရှိမှာ dist_jarowinkler ကို တွက်နေတယ်လို့ နားလည်တယ်။  
အဲဒါကြောင့် distance အကုန်တွက်တာကို စောင့်မနေတော့ပဲ လက်ရှိ output ရလာတဲ့ distance ၅မျိုးကိုပဲ ယူလိုက်ပြီး လေဘယ်နဲ့ တွဲပေးလိုက်ပြီးရင် Random Forest နဲ့ training လုပ်ဖို့ ဆုံးဖြတ်ခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry/tmp$ paste -d"," ./dist_bag.txt ./dist_compression.txt ./dist_damerau.txt ./dist_hamming.txt ./dist_jaro.txt ./label.txt > ./5dist.para.csv
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry/tmp$ head ./5dist.para.csv 
66,0.541322,95,183,0.287804,0
15,0.377907,35,88,0.217737,0
20,0.448718,37,74,0.2494,0
15,0.227723,18,100,0.196164,0
45,0.425532,53,120,0.28428,0
6,0.183673,11,44,0.216472,0
93,0.639535,98,123,0.443955,0
72,0.590909,90,142,0.303462,0
50,0.5,57,108,0.322201,0
16,0.574627,26,54,0.263832,0
```

တစ်ခုရှိတာက တကယ့် CSV format အမှန်က ထိပ်ဆုံးအကြောင်းက column header တပ်ထားရတယ်။ အဲဒါမှလည်း Python library တွေဖြစ်တဲ့ csv တို့ panda တို့နဲ့ တွဲအလုပ်လုပ်ရင် အဆင်ပြေမှာမို့ ထိပ်ဆုံး ကော်လံခေါင်းစဉ်ကိုလည်း အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့...  

ဒီနေရာမှာ သုံးထားတဲ့ header.txt ဖိုင်ဆိုတာက column header တစ်ကြောင်းတည်းကိုပဲ ရိုက်ထည့်ထားတဲ့ ဖိုင်ပါ။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry/tmp$ cat header.txt 5dist.para.csv > para.train
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry/tmp$ head para.train 
dist_bag,dist_compression,dist_damerau,dist_hamming,dist_jaro,label
66,0.541322,95,183,0.287804,0
15,0.377907,35,88,0.217737,0
20,0.448718,37,74,0.2494,0
15,0.227723,18,100,0.196164,0
45,0.425532,53,120,0.28428,0
6,0.183673,11,44,0.216472,0
93,0.639535,98,123,0.443955,0
72,0.590909,90,142,0.303462,0
50,0.5,57,108,0.322201,0
```

para.train ဖိုင်ကို သုံးပြီးတော့ model ဆောက်မှာမို့ အဲဒီဖိုင်ကို paraphrase modeling with traditional ML approach လုပ်ဖို့ ရည်ရွယ်ထားတဲ့ ဖိုလ်ဒါအောက်ကို ကော်ပီကူးခဲ့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/harry/tmp$ cp para.train /home/ye/exp/myPara3/data/
```


## Prepare a Python Script for Random Forest Classifier

ပြင်ဆင်ခဲ့တဲ့ Python script က အောက်ပါအတိုင်း...  

```python
# for Myanmar language paraphrase experiment with Forest-tree 
# We used our inhouse myPara corpus mainly develped by Myint Myint Htay (UTYCC)
# Features were extracted with harry string similary tool
# This code is written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Date: 21 Sept 2021

from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import time
import matplotlib.pyplot as plt

para_data=pd.read_csv('/home/ye/exp/myPara3/data/para.train')
print("head:")
print(para_data.head())

para_data.replace([np.inf, -np.inf], np.nan, inplace=True)
para_data.fillna(999, inplace=True)

y=para_data.label
x=para_data.drop('label',axis=1)

#x = x.values.astype(np.float)
#y = y.values.astype(np.float)

X_train, X_test, y_train, y_test = train_test_split(x,y,test_size=0.2)
print("X_train.head()")
print(X_train.head())

forest = RandomForestClassifier(n_estimators=50, random_state=0)
forest.fit(X_train,y_train)

print('Accuracy on the training:',format(forest.score(X_train,y_train)))
print('Accuracy on the testing:',format(forest.score(X_test,y_test)))


feature_names = x.columns

start_time = time.time()
importances = forest.feature_importances_
std = np.std([
    tree.feature_importances_ for tree in forest.estimators_], axis=0)
elapsed_time = time.time() - start_time

print(f"Elapsed time to compute the importances: "
      f"{elapsed_time:.3f} seconds")
      
forest_importances = pd.Series(importances, index=feature_names)

fig, ax = plt.subplots()
forest_importances.plot.bar(yerr=std, ax=ax)
ax.set_title("Feature importances using MDI")
ax.set_ylabel("Mean decrease in impurity")
fig.tight_layout()
plt.show()

from sklearn.inspection import permutation_importance

start_time = time.time()
result = permutation_importance(
    forest, X_test, y_test, n_repeats=10, random_state=42, n_jobs=2)
elapsed_time = time.time() - start_time
print(f"Elapsed time to compute the importances: "
      f"{elapsed_time:.3f} seconds")

forest_importances = pd.Series(result.importances_mean, index=feature_names)


fig, ax = plt.subplots()
forest_importances.plot.bar(yerr=result.importances_std, ax=ax)
ax.set_title("Feature importances using permutation on full model")
ax.set_ylabel("Mean accuracy decrease")
fig.tight_layout()
plt.show()


```

coding က run လို့ အိုကေသွားပြီး နောက်ပိုင်း အချိန်ရတော့မှာ input ဖိုင်ကို argument နဲ့ ပေးတာမျိုး၊ train, test data ကို သတ်မှတ်ပြီး ဖိုင်အနေနဲ့ pass လုပ်တာမျိုး၊ graph တွေကိုလည်း ဖိုင်နာမည်ပေးသိမ်းတာမျိုး ဖြည့်ရေးဖို့ စိတ်ကူးထားတယ်။ လောလောဆယ်က အချိန်မရှိလို့ run ကြည့်ပြီး ရလဒ်ကို အမြန်ကြည့်ဖို့ ကြိုးစားနေတာမို့...  

ပြီးတော့ အထက်ပါ python program ကို run မလုပ်ခင်မှာ လိုအပ်တဲ့ panda, time စတဲ့ library က ကြိုတင် installation လုပ်ခဲ့ပါတယ်။   

### Training Paraphrase Classification with Random-Forest (used only 5 string similarity distance features)

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/myPara3$ time python ./para_foresttree.py 
head:
   dist_bag  dist_compression  dist_damerau  dist_hamming  dist_jaro  label
0        66          0.541322            95           183   0.287804    0.0
1        15          0.377907            35            88   0.217737    0.0
2        20          0.448718            37            74   0.249400    0.0
3        15          0.227723            18           100   0.196164    0.0
4        45          0.425532            53           120   0.284280    0.0
X_train.head()
       dist_bag  dist_compression  dist_damerau  dist_hamming  dist_jaro
39938        32          0.549383            44            75   0.294668
39205        28          0.359649            28            40   0.215399
18687        11          0.367347            11            30   0.182359
21622        26          0.477941            26            31   0.200418
7835          7          0.166667             7            14   0.070937
Accuracy on the training: 0.9994874577906416
Accuracy on the testing: 0.818762812010129
Elapsed time to compute the importances: 0.010 seconds
Elapsed time to compute the importances: 2.987 seconds

real	0m28.195s
user	0m7.161s
sys	0m1.217s
```

Run time က 28 Sec ပဲ ကြာတယ်။
ရလဒ်ကလည်း ကောင်းတယ်။ training ဒေတာနဲ့က 0.99 Accuracy ရပြီးတော့၊ test data နဲ့က 0.82 ရတယ်။  
အထက်မှာ ဆက်တိုက် လုပ်လာခဲ့တဲ့ distance တစ်ခုတည်းနဲ့ Siamese Network training result တွေနဲ့ ယှဉ်လိုက်ရင် လုံးဝ တခြားစီပါပဲ....  
အဲဒါကြောင့် အထက်က Python code ကို ပြင်ဆင်ပြီးတော့ Siamese Network တုန်းက သုံးခဲ့တဲ့ training, test data နဲ့ ထပ်တူ လုပ်ကြည့်ပြီး result ထုတ်ကြည့်မယ်။
ပြီးတော့ Siamese Network ကိုလည်း word2vec, fasttext တို့နဲ့ မဟုတ်ပဲ အခု python code နဲ့ random forest နဲ့ စမ်းခဲ့တဲ့ training, test ဒေတာ (i.e. features with 5 distances) တို့နဲ့ training/testing လုပ်ကြည့်ပြီး ရလဒ်တွေကို compare လုပ်ကြည့်မယ်။  

## Checking the Feature Importance Graphs  

Tree, Forest-Tree နဲ့ training လုပ်ထားတဲ့ မော်ဒယ်မို့လို့ လွယ်လွယ်ကူကူ ဘယ် feature တွေက မြန်မာစာ paraphrase classification task အတွက် အလုပ်ကောင်းကောင်းလုပ်တယ်ဆိုတာကို feature importance graph ထုတ်ကြည့်လို့ ရပါတယ်။ Feature importance ကို ဆုံးဖြတ်တဲ့ approach နှစ်ခု ဖြစ်တဲ့ MDI (Mean Decrease in Impurity) နည်းလမ်းနဲ့ Feature Permutation နည်းလမ်းနှစ်မျိုးတို့ကို သုံးထားပါတယ်။  

<p float="left"  align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/feature_importance-with-MDI-for-5dists.png" width="460" />
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/feature_importance-with-feature-permutation-for-5dists.png" width="460" /> 
</p>
<div align="center">
  Fig. Important feature graph for five string similarity measures. Left: with MDI, Right: with Feature Permutation
</div>   
  </br> 
  
  

## Building a Big Word2Vec and FastText Models

  
### Validation.txt0

Deep Siamese NN ပရိုဂရမ်မှာက default char နဲ့ run ရင် training data ကို label ထိုးထားတာက တမျိုးပဲ လို့ ယူဆပြီးတော့ validation.txt0 ဆိုတဲ့ ဖိုင်ကို function တစ်ခုနဲ့ negative label ကို simulation လုပ်သွားတယ်။ အဲဒါကြောင့် အဲဒီတိုင်း run ရင် result က မကောင်းနိုင်ဘူး။ ဥပမာ အောက်က ပုံက myWord ကို character training default နဲ့ run နေစဉ်မှာ မြင်ရတဲ့ accuracy နဲ့ loss ရဲ့ အခြေအနေ... ဒီ အနေအထားကနေ Accuracy က 90 အထက် တက်လာဖို့က မလွယ်ကူဘူး...  
  
<p align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/with-default-char-accuracy-is-low.png" width="600" />
</p>
<div align="center">
  Fig. Accuracy and Loss Status of Training and Validation  with "Word Unit Segmented with myWord", character, 200 epoch.
</div>   
  </br>
  
အဲဒါကြောင့် coding ကို ဝင်ပြင်ဖို့ လိုအပ်တယ်။  

input_helpers.py ဖိုင်ကို အောက်ပါအတိုင်း ဝင်ပြင်ဆင်ခဲ့...  
  
```python
    def getDataSets(self, training_paths, max_document_length, percent_dev, batch_size, is_char_based):
        if is_char_based:
            #x1_text, x2_text, y=self.getTsvDataCharBased(training_paths)
            x1_text, x2_text, y=self.getTsvData(training_paths)
        else:
            x1_text, x2_text, y=self.getTsvData(training_paths)
```
  
### Check Your HDD Space

အခု လက်ရှိ training လုပ်ပြီးရလာတဲ့ NN model တွေရဲ့ file size တွေက တအားကြီးပါတယ်။ အထူးသဖြင့် batch size ကို small no. ထားတဲ့အခါမျိုး၊ hidden units တွေကို တိုးတဲ့အခါမျိုးတွေမှာ...  
ဥပမာ အနေနဲ့ word (segmented with myWord Segmentation Tool), fasttext embedding, batch size 8, epoch 200 (ထားထားပေမဲ့ early stop လုပ်ပါတယ်) နဲ့ ဆောက်ထားတဲ့ မော်ဒယ်တွေကို သိမ်းထားတဲ့ ဖိုလ်ဒါရဲ့ size က အောက်ပါပုံမှာ ပြထားတဲ့အတိုင်းပါပဲ... 41.8 GB ယူပါတယ်။ အဲဒါတွေကို ဖြေရှင်းတဲ့နည်းကတော့ ဖိုလ်ဒါအလိုက် external HDD မှာ ရွှေ့သိမ်းထားတာမျိုး၊ သို့မဟုတ် checkpoint လုပ်ထားတဲ့ တခြား မော်ဒယ်ဖိုင်တွေကို ဖျက်ပစ်ပြီးတော့ နောက်ဆုံးမော်ဒယ်ကိုပဲ သိမ်းထားတာမျိုးတွေ လုပ်ပါလို့ အကြံပေးချင်ပါတယ်။   

<p align="center">
  <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/siameseNN-training-model-folder-with-batch8.png" width="300" />
</p>
<div align="center">
  Fig. An Example HDD space usage of the Folder that Saved Trained Deep Siamese NN Models
</div>   
  </br>
  
## Links
  - https://arxiv.org/pdf/1803.11175.pdf
  - https://tfhub.dev/google/universal-sentence-encoder/4
  - https://colab.research.google.com/github/tensorflow/hub/blob/master/examples/colab/semantic_similarity_with_tf_hub_universal_encoder.ipynb#scrollTo=BnvjATdy64eR
  
  
