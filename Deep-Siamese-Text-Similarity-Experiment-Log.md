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




