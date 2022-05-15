# Adapt MNMT Experiment No. 1

## Git Clone

```
(base) ye@ye-System-Product-Name:~/tool$ git clone https://github.com/surafelml/adapt-mnmt
Cloning into 'adapt-mnmt'...
remote: Enumerating objects: 272, done.
remote: Counting objects: 100% (21/21), done.
remote: Compressing objects: 100% (18/18), done.
remote: Total 272 (delta 1), reused 20 (delta 1), pack-reused 251
Receiving objects: 100% (272/272), 524.81 KiB | 4.23 MiB/s, done.
Resolving deltas: 100% (43/43), done.
(base) ye@ye-System-Product-Name:~/tool$ cd adapt-mnmt/
(base) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ ls
config_adapt.yml  config.yml  model_defn.py  OpenNMT  README.md  scripts  setup-env.sh  train-dynamic-tl.sh  train.sh
```

## Create a New Python Environment

```
(base) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ conda create --name adapt-mnmt python=3.6
Collecting package metadata (current_repodata.json): done
Solving environment: failed with repodata from current_repodata.json, will retry with next repodata source.
Collecting package metadata (repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/anaconda3/envs/adapt-mnmt

  added / updated specs:
    - python=3.6


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    ca-certificates-2022.4.26  |       h06a4308_0         124 KB
    openssl-1.1.1o             |       h7f8727e_0         2.5 MB
    sqlite-3.38.3              |       hc218d9a_0         1.0 MB
    tk-8.6.11                  |       h1ccaba5_1         3.0 MB
    xz-5.2.5                   |       h7f8727e_1         339 KB
    ------------------------------------------------------------
                                           Total:         7.0 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-4.5-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2022.4.26-h06a4308_0
  certifi            pkgs/main/linux-64::certifi-2021.5.30-py36h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.35.1-h7274673_9
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_2
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.3.0-h5101ec6_17
  libgomp            pkgs/main/linux-64::libgomp-9.3.0-h5101ec6_17
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.3.0-hd4cf53a_17
  ncurses            pkgs/main/linux-64::ncurses-6.3-h7f8727e_2
  openssl            pkgs/main/linux-64::openssl-1.1.1o-h7f8727e_0
  pip                pkgs/main/linux-64::pip-21.2.2-py36h06a4308_0
  python             pkgs/main/linux-64::python-3.6.13-h12debd9_1
  readline           pkgs/main/linux-64::readline-8.1.2-h7f8727e_1
  setuptools         pkgs/main/linux-64::setuptools-58.0.4-py36h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.38.3-hc218d9a_0
  tk                 pkgs/main/linux-64::tk-8.6.11-h1ccaba5_1
  wheel              pkgs/main/noarch::wheel-0.37.1-pyhd3eb1b0_0
  xz                 pkgs/main/linux-64::xz-5.2.5-h7f8727e_1
  zlib               pkgs/main/linux-64::zlib-1.2.12-h7f8727e_2


Proceed ([y]/n)? y


Downloading and Extracting Packages
sqlite-3.38.3        | 1.0 MB    | ############################################################################################ | 100%
ca-certificates-2022 | 124 KB    | ############################################################################################ | 100%
xz-5.2.5             | 339 KB    | ############################################################################################ | 100%
tk-8.6.11            | 3.0 MB    | ############################################################################################ | 100%
openssl-1.1.1o       | 2.5 MB    | ############################################################################################ | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate adapt-mnmt
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ conda activate adapt-mnmt
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

I updated the setup-env.sh as follows:  
```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ cat ./setup-env.sh
#!/bin/bash

#
# for library specific requiremtns, see README of each repo
#

EXPDIR=$PWD

# libraries
MOSES=https://github.com/moses-smt/mosesdecoder.git
SENT_PIECE='sentencepiece==0.1.8'
#TENSORFLOW='tensorflow-gpu==1.4.1'
#TENSORFLOW='tensorflow-gpu==2.7'
TENSORFLOW='tensorflow-gpu==2.6.2'
#OPENNMT=https://github.com/OpenNMT/OpenNMT-tf/tree/v1.15.0 # install updated version ./OpenNMT


# Data, Processing
if [ ! -d $EXPDIR/mosesdecoder ]
then
  echo "Cloning Mosesdecoder ..."
  git clone $MOSES
fi

echo "Installing SentencePiece ..."
pip install $SENT_PIECE


# NMT
echo "Install tensorflow.."
pip install $TENSORFLOW

if [ -d $EXPDIR/OpenNMT ]
then
  cd ./OpenNMT
  pip install -e ./
fi
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

## Run Setup-Env

Got ERROR at tensorflow installation ...  
(Version problem)  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ bash ./setup-env.sh | tee ./setup-env-running.log
bash: /home/ye/anaconda3/envs/xnmt/lib/libtinfo.so.6: no version information available (required by bash)
Cloning Mosesdecoder ...
Cloning into 'mosesdecoder'...
remote: Enumerating objects: 148097, done.
remote: Counting objects: 100% (525/525), done.
remote: Compressing objects: 100% (229/229), done.
remote: Total 148097 (delta 323), reused 441 (delta 292), pack-reused 147572
Receiving objects: 100% (148097/148097), 129.88 MiB | 15.40 MiB/s, done.
Resolving deltas: 100% (114349/114349), done.
Installing SentencePiece ...
Requirement already satisfied: sentencepiece==0.1.8 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (0.1.8)
Install tensorflow..
ERROR: Could not find a version that satisfies the requirement tensorflow-gpu==2.7 (from versions: 0.12.1, 1.0.0, 1.0.1, 1.1.0, 1.2.0, 1.2.1, 1.3.0, 1.4.0, 1.4.1, 1.5.0, 1.5.1, 1.6.0, 1.7.0, 1.7.1, 1.8.0, 1.9.0, 1.10.0, 1.10.1, 1.11.0, 1.12.0, 1.12.2, 1.12.3, 1.13.1, 1.13.2, 1.14.0, 1.15.0, 1.15.2, 1.15.3, 1.15.4, 1.15.5, 2.0.0, 2.0.1, 2.0.2, 2.0.3, 2.0.4, 2.1.0, 2.1.1, 2.1.2, 2.1.3, 2.1.4, 2.2.0, 2.2.1, 2.2.2, 2.2.3, 2.3.0, 2.3.1, 2.3.2, 2.3.3, 2.3.4, 2.4.0, 2.4.1, 2.4.2, 2.4.3, 2.4.4, 2.5.0, 2.5.1, 2.5.2, 2.6.0, 2.6.1, 2.6.2)
ERROR: No matching distribution found for tensorflow-gpu==2.7
Obtaining file:///home/ye/tool/adapt-mnmt/OpenNMT
Requirement already satisfied: pyyaml in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from OpenNMT-tf==1.15.0) (6.0)
Requirement already satisfied: rouge==0.3.1 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from OpenNMT-tf==1.15.0) (0.3.1)
Requirement already satisfied: pyonmttok<2,>=1.5.0 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from OpenNMT-tf==1.15.0) (1.31.0)
Installing collected packages: OpenNMT-tf
  Running setup.py develop for OpenNMT-tf
Successfully installed OpenNMT-tf-1.15.0
```

I updated the tensorflow version to 2.6.2 and then run setup-env.sh again:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ vi ./setup-env.sh
vi: /home/ye/anaconda3/envs/xnmt/lib/libtinfo.so.6: no version information available (required by vi)
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ bash ./setup-env.sh | tee ./setup-env-running.log
bash: /home/ye/anaconda3/envs/xnmt/lib/libtinfo.so.6: no version information available (required by bash)
Installing SentencePiece ...
Requirement already satisfied: sentencepiece==0.1.8 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (0.1.8)
Install tensorflow..
Collecting tensorflow-gpu==2.6.2
  Downloading tensorflow_gpu-2.6.2-cp36-cp36m-manylinux2010_x86_64.whl (458.3 MB)
Collecting keras-preprocessing~=1.1.2
  Using cached Keras_Preprocessing-1.1.2-py2.py3-none-any.whl (42 kB)
Collecting termcolor~=1.1.0
  Using cached termcolor-1.1.0-py3-none-any.whl
Collecting google-pasta~=0.2
  Using cached google_pasta-0.2.0-py3-none-any.whl (57 kB)
Collecting flatbuffers~=1.12.0
  Using cached flatbuffers-1.12-py2.py3-none-any.whl (15 kB)
Collecting gast==0.4.0
  Using cached gast-0.4.0-py3-none-any.whl (9.8 kB)
Collecting keras<2.7,>=2.6.0
  Using cached keras-2.6.0-py2.py3-none-any.whl (1.3 MB)
Collecting h5py~=3.1.0
  Using cached h5py-3.1.0-cp36-cp36m-manylinux1_x86_64.whl (4.0 MB)
Collecting absl-py~=0.10
  Using cached absl_py-0.15.0-py3-none-any.whl (132 kB)
Collecting numpy~=1.19.2
  Using cached numpy-1.19.5-cp36-cp36m-manylinux2010_x86_64.whl (14.8 MB)
Collecting opt-einsum~=3.3.0
  Using cached opt_einsum-3.3.0-py3-none-any.whl (65 kB)
Collecting six~=1.15.0
  Using cached six-1.15.0-py2.py3-none-any.whl (10 kB)
Collecting typing-extensions~=3.7.4
  Using cached typing_extensions-3.7.4.3-py3-none-any.whl (22 kB)
Collecting clang~=5.0
  Using cached clang-5.0-py3-none-any.whl
Collecting wrapt~=1.12.1
  Using cached wrapt-1.12.1-cp36-cp36m-linux_x86_64.whl
Collecting tensorboard<2.7,>=2.6.0
  Using cached tensorboard-2.6.0-py3-none-any.whl (5.6 MB)
Requirement already satisfied: wheel~=0.35 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from tensorflow-gpu==2.6.2) (0.37.1)
Collecting tensorflow-estimator<2.7,>=2.6.0
  Using cached tensorflow_estimator-2.6.0-py2.py3-none-any.whl (462 kB)
Collecting grpcio<2.0,>=1.37.0
  Downloading grpcio-1.46.1-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.4 MB)
Collecting protobuf>=3.9.2
  Using cached protobuf-3.19.4-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.1 MB)
Collecting astunparse~=1.6.3
  Using cached astunparse-1.6.3-py2.py3-none-any.whl (12 kB)
Collecting cached-property
  Using cached cached_property-1.5.2-py2.py3-none-any.whl (7.6 kB)
Collecting google-auth-oauthlib<0.5,>=0.4.1
  Using cached google_auth_oauthlib-0.4.6-py2.py3-none-any.whl (18 kB)
Collecting werkzeug>=0.11.15
  Using cached Werkzeug-2.0.3-py3-none-any.whl (289 kB)
Collecting tensorboard-plugin-wit>=1.6.0
  Using cached tensorboard_plugin_wit-1.8.1-py3-none-any.whl (781 kB)
Collecting tensorboard-data-server<0.7.0,>=0.6.0
  Using cached tensorboard_data_server-0.6.1-py3-none-manylinux2010_x86_64.whl (4.9 MB)
Collecting markdown>=2.6.8
  Downloading Markdown-3.3.7-py3-none-any.whl (97 kB)
Collecting google-auth<2,>=1.6.3
  Using cached google_auth-1.35.0-py2.py3-none-any.whl (152 kB)
Collecting requests<3,>=2.21.0
  Using cached requests-2.27.1-py2.py3-none-any.whl (63 kB)
Requirement already satisfied: setuptools>=41.0.0 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from tensorboard<2.7,>=2.6.0->tensorflow-gpu==2.6.2) (58.0.4)
Collecting rsa<5,>=3.1.4
  Using cached rsa-4.8-py3-none-any.whl (39 kB)
Collecting cachetools<5.0,>=2.0.0
  Using cached cachetools-4.2.4-py3-none-any.whl (10 kB)
Collecting pyasn1-modules>=0.2.1
  Using cached pyasn1_modules-0.2.8-py2.py3-none-any.whl (155 kB)
Collecting requests-oauthlib>=0.7.0
  Using cached requests_oauthlib-1.3.1-py2.py3-none-any.whl (23 kB)
Collecting importlib-metadata>=4.4
  Using cached importlib_metadata-4.8.3-py3-none-any.whl (17 kB)
Collecting zipp>=0.5
  Using cached zipp-3.6.0-py3-none-any.whl (5.3 kB)
Collecting pyasn1<0.5.0,>=0.4.6
  Using cached pyasn1-0.4.8-py2.py3-none-any.whl (77 kB)
Collecting urllib3<1.27,>=1.21.1
  Using cached urllib3-1.26.9-py2.py3-none-any.whl (138 kB)
Collecting charset-normalizer~=2.0.0
  Using cached charset_normalizer-2.0.12-py3-none-any.whl (39 kB)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from requests<3,>=2.21.0->tensorboard<2.7,>=2.6.0->tensorflow-gpu==2.6.2) (2021.5.30)
Collecting idna<4,>=2.5
  Using cached idna-3.3-py3-none-any.whl (61 kB)
Collecting oauthlib>=3.0.0
  Using cached oauthlib-3.2.0-py3-none-any.whl (151 kB)
Collecting dataclasses
  Using cached dataclasses-0.8-py3-none-any.whl (19 kB)
Installing collected packages: urllib3, pyasn1, idna, charset-normalizer, zipp, typing-extensions, six, rsa, requests, pyasn1-modules, oauthlib, cachetools, requests-oauthlib, importlib-metadata, google-auth, dataclasses, werkzeug, tensorboard-plugin-wit, tensorboard-data-server, protobuf, numpy, markdown, grpcio, google-auth-oauthlib, cached-property, absl-py, wrapt, termcolor, tensorflow-estimator, tensorboard, opt-einsum, keras-preprocessing, keras, h5py, google-pasta, gast, flatbuffers, clang, astunparse, tensorflow-gpu
Successfully installed absl-py-0.15.0 astunparse-1.6.3 cached-property-1.5.2 cachetools-4.2.4 charset-normalizer-2.0.12 clang-5.0 dataclasses-0.8 flatbuffers-1.12 gast-0.4.0 google-auth-1.35.0 google-auth-oauthlib-0.4.6 google-pasta-0.2.0 grpcio-1.46.1 h5py-3.1.0 idna-3.3 importlib-metadata-4.8.3 keras-2.6.0 keras-preprocessing-1.1.2 markdown-3.3.7 numpy-1.19.5 oauthlib-3.2.0 opt-einsum-3.3.0 protobuf-3.19.4 pyasn1-0.4.8 pyasn1-modules-0.2.8 requests-2.27.1 requests-oauthlib-1.3.1 rsa-4.8 six-1.15.0 tensorboard-2.6.0 tensorboard-data-server-0.6.1 tensorboard-plugin-wit-1.8.1 tensorflow-estimator-2.6.0 tensorflow-gpu-2.6.2 termcolor-1.1.0 typing-extensions-3.7.4.3 urllib3-1.26.9 werkzeug-2.0.3 wrapt-1.12.1 zipp-3.6.0
Obtaining file:///home/ye/tool/adapt-mnmt/OpenNMT
Requirement already satisfied: pyyaml in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from OpenNMT-tf==1.15.0) (6.0)
Requirement already satisfied: rouge==0.3.1 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from OpenNMT-tf==1.15.0) (0.3.1)
Requirement already satisfied: pyonmttok<2,>=1.5.0 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from OpenNMT-tf==1.15.0) (1.31.0)
Installing collected packages: OpenNMT-tf
  Attempting uninstall: OpenNMT-tf
    Found existing installation: OpenNMT-tf 1.15.0
    Uninstalling OpenNMT-tf-1.15.0:
      Successfully uninstalled OpenNMT-tf-1.15.0
  Running setup.py develop for OpenNMT-tf
Successfully installed OpenNMT-tf-1.15.0
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

## Download Data

run get-data.sh for getting TED corpus:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/scripts$ ./get-data.sh
/bin/bash: /home/ye/anaconda3/envs/xnmt/lib/libtinfo.so.6: no version information available (required by /bin/bash)
Loading and reading ted data ...
~/tool/adapt-mnmt/scripts/data/ted-data ~/tool/adapt-mnmt/scripts
wget: /home/ye/anaconda3/envs/xnmt/lib/libuuid.so.1: no version information available (required by wget)
--2022-05-12 17:13:07--  http://phontron.com/data/ted_talks.tar.gz
Resolving phontron.com (phontron.com)... 208.113.196.149
Connecting to phontron.com (phontron.com)|208.113.196.149|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 352222045 (336M) [application/gzip]
Saving to: ‘ted_talks.tar.gz’

ted_talks.tar.gz                  100%[============================================================>] 335.90M  9.19MB/s    in 33s

2022-05-12 17:13:41 (10.1 MB/s) - ‘ted_talks.tar.gz’ saved [352222045/352222045]

all_talks_dev.tsv
all_talks_test.tsv
all_talks_train.tsv
python: can't open file '/home/ye/tool/adapt-mnmt/scripts/scripts/ted_reader.py': [Errno 2] No such file or directory
~/tool/adapt-mnmt/scripts
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/scripts$
```

got ERROR as shown in the above and related to running "ted_reader.py"  
When I checked the ERROR, I found that is caused by running path. And thus, I move upper level folder and then run the "get-data.sh" again ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ ./scripts/get-data.sh
/bin/bash: /home/ye/anaconda3/envs/xnmt/lib/libtinfo.so.6: no version information available (required by /bin/bash)
Loading and reading ted data ...
~/tool/adapt-mnmt/data/ted-data ~/tool/adapt-mnmt
wget: /home/ye/anaconda3/envs/xnmt/lib/libuuid.so.1: no version information available (required by wget)
--2022-05-12 17:18:32--  http://phontron.com/data/ted_talks.tar.gz
Resolving phontron.com (phontron.com)... 208.113.196.149
Connecting to phontron.com (phontron.com)|208.113.196.149|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 352222045 (336M) [application/gzip]
Saving to: ‘ted_talks.tar.gz’

ted_talks.tar.gz                  100%[============================================================>] 335.90M  11.3MB/s    in 38s

2022-05-12 17:19:11 (8.80 MB/s) - ‘ted_talks.tar.gz’ saved [352222045/352222045]

all_talks_dev.tsv
all_talks_test.tsv
all_talks_train.tsv
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/scripts/ted_reader.py", line 139, in <module>
    with open("./ted_talks_langs.txt", 'r') as f:
FileNotFoundError: [Errno 2] No such file or directory: './ted_talks_langs.txt'
~/tool/adapt-mnmt
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

ERROR again as above ...  
added "./scripts/" for open function:  

```python
    # read ted_langs_list to extract [langs-en] pairs
    with open("./scripts/ted_talks_langs.txt", 'r') as f:
        langs = f.read().splitlines()
```

Run again ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ time ./scripts/get-data.sh
/bin/bash: /home/ye/anaconda3/envs/xnmt/lib/libtinfo.so.6: no version information available (required by /bin/bash)
Loading and reading ted data ...
~/tool/adapt-mnmt/data/ted-data ~/tool/adapt-mnmt
wget: /home/ye/anaconda3/envs/xnmt/lib/libuuid.so.1: no version information available (required by wget)
--2022-05-12 18:18:18--  http://phontron.com/data/ted_talks.tar.gz
Resolving phontron.com (phontron.com)... 208.113.196.149
Connecting to phontron.com (phontron.com)|208.113.196.149|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 352222045 (336M) [application/gzip]
Saving to: ‘ted_talks.tar.gz’

ted_talks.tar.gz                  100%[============================================================>] 335.90M  8.67MB/s    in 49s

2022-05-12 18:19:07 (6.91 MB/s) - ‘ted_talks.tar.gz’ saved [352222045/352222045]

all_talks_dev.tsv
all_talks_test.tsv
all_talks_train.tsv
en en
~/tool/adapt-mnmt

real    11m13.753s
user    10m16.927s
sys     0m9.416s
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

Check the downloaded data:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ tree ./data/
./data/
└── ted-data
    ├── ar_en
    │   ├── dev.ar
    │   ├── dev.en
    │   ├── test.ar
    │   ├── test.en
    │   ├── train.ar
    │   └── train.en
    ├── az_en
    │   ├── dev.az
    │   ├── dev.en
    │   ├── test.az
    │   ├── test.en
    │   ├── train.az
    │   └── train.en
    ├── be_en
    │   ├── dev.be
    │   ├── dev.en
    │   ├── test.be
    │   ├── test.en
    │   ├── train.be
    │   └── train.en
    ├── bg_en
    │   ├── dev.bg
    │   ├── dev.en
    │   ├── test.bg
    │   ├── test.en
    │   ├── train.bg
    │   └── train.en
    ├── bn_en
    │   ├── dev.bn
    │   ├── dev.en
    │   ├── test.bn
    │   ├── test.en
    │   ├── train.bn
    │   └── train.en
    ├── bs_en
    │   ├── dev.bs
    │   ├── dev.en
    │   ├── test.bs
    │   ├── test.en
    │   ├── train.bs
    │   └── train.en
    ├── calv_en
    │   ├── dev.calv
    │   ├── dev.en
    │   ├── test.calv
    │   ├── test.en
    │   ├── train.calv
    │   └── train.en
    ├── cs_en
    │   ├── dev.cs
    │   ├── dev.en
    │   ├── test.cs
    │   ├── test.en
    │   ├── train.cs
    │   └── train.en
    ├── da_en
    │   ├── dev.da
    │   ├── dev.en
    │   ├── test.da
    │   ├── test.en
    │   ├── train.da
    │   └── train.en
    ├── de_en
    │   ├── dev.de
    │   ├── dev.en
    │   ├── test.de
    │   ├── test.en
    │   ├── train.de
    │   └── train.en
    ├── el_en
    │   ├── dev.el
    │   ├── dev.en
    │   ├── test.el
    │   ├── test.en
    │   ├── train.el
    │   └── train.en
    ├── eo_en
    │   ├── dev.en
    │   ├── dev.eo
    │   ├── test.en
    │   ├── test.eo
    │   ├── train.en
    │   └── train.eo
    ├── es_en
    │   ├── dev.en
    │   ├── dev.es
    │   ├── test.en
    │   ├── test.es
    │   ├── train.en
    │   └── train.es
    ├── et_en
    │   ├── dev.en
    │   ├── dev.et
    │   ├── test.en
    │   ├── test.et
    │   ├── train.en
    │   └── train.et
    ├── eu_en
    │   ├── dev.en
    │   ├── dev.eu
    │   ├── test.en
    │   ├── test.eu
    │   ├── train.en
    │   └── train.eu
    ├── fa_en
    │   ├── dev.en
    │   ├── dev.fa
    │   ├── test.en
    │   ├── test.fa
    │   ├── train.en
    │   └── train.fa
    ├── fi_en
    │   ├── dev.en
    │   ├── dev.fi
    │   ├── test.en
    │   ├── test.fi
    │   ├── train.en
    │   └── train.fi
    ├── fr-ca_en
    │   ├── dev.en
    │   ├── dev.fr-ca
    │   ├── test.en
    │   ├── test.fr-ca
    │   ├── train.en
    │   └── train.fr-ca
    ├── fr_en
    │   ├── dev.en
    │   ├── dev.fr
    │   ├── test.en
    │   ├── test.fr
    │   ├── train.en
    │   └── train.fr
    ├── gl_en
    │   ├── dev.en
    │   ├── dev.gl
    │   ├── test.en
    │   ├── test.gl
    │   ├── train.en
    │   └── train.gl
    ├── he_en
    │   ├── dev.en
    │   ├── dev.he
    │   ├── test.en
    │   ├── test.he
    │   ├── train.en
    │   └── train.he
    ├── hi_en
    │   ├── dev.en
    │   ├── dev.hi
    │   ├── test.en
    │   ├── test.hi
    │   ├── train.en
    │   └── train.hi
    ├── hr_en
    │   ├── dev.en
    │   ├── dev.hr
    │   ├── test.en
    │   ├── test.hr
    │   ├── train.en
    │   └── train.hr
    ├── hu_en
    │   ├── dev.en
    │   ├── dev.hu
    │   ├── test.en
    │   ├── test.hu
    │   ├── train.en
    │   └── train.hu
    ├── hy_en
    │   ├── dev.en
    │   ├── dev.hy
    │   ├── test.en
    │   ├── test.hy
    │   ├── train.en
    │   └── train.hy
    ├── id_en
    │   ├── dev.en
    │   ├── dev.id
    │   ├── test.en
    │   ├── test.id
    │   ├── train.en
    │   └── train.id
    ├── it_en
    │   ├── dev.en
    │   ├── dev.it
    │   ├── test.en
    │   ├── test.it
    │   ├── train.en
    │   └── train.it
    ├── ja_en
    │   ├── dev.en
    │   ├── dev.ja
    │   ├── test.en
    │   ├── test.ja
    │   ├── train.en
    │   └── train.ja
    ├── ka_en
    │   ├── dev.en
    │   ├── dev.ka
    │   ├── test.en
    │   ├── test.ka
    │   ├── train.en
    │   └── train.ka
    ├── kk_en
    │   ├── dev.en
    │   ├── dev.kk
    │   ├── test.en
    │   ├── test.kk
    │   ├── train.en
    │   └── train.kk
    ├── ko_en
    │   ├── dev.en
    │   ├── dev.ko
    │   ├── test.en
    │   ├── test.ko
    │   ├── train.en
    │   └── train.ko
    ├── ku_en
    │   ├── dev.en
    │   ├── dev.ku
    │   ├── test.en
    │   ├── test.ku
    │   ├── train.en
    │   └── train.ku
    ├── lt_en
    │   ├── dev.en
    │   ├── dev.lt
    │   ├── test.en
    │   ├── test.lt
    │   ├── train.en
    │   └── train.lt
    ├── mk_en
    │   ├── dev.en
    │   ├── dev.mk
    │   ├── test.en
    │   ├── test.mk
    │   ├── train.en
    │   └── train.mk
    ├── mn_en
    │   ├── dev.en
    │   ├── dev.mn
    │   ├── test.en
    │   ├── test.mn
    │   ├── train.en
    │   └── train.mn
    ├── mr_en
    │   ├── dev.en
    │   ├── dev.mr
    │   ├── test.en
    │   ├── test.mr
    │   ├── train.en
    │   └── train.mr
    ├── ms_en
    │   ├── dev.en
    │   ├── dev.ms
    │   ├── test.en
    │   ├── test.ms
    │   ├── train.en
    │   └── train.ms
    ├── my_en
    │   ├── dev.en
    │   ├── dev.my
    │   ├── test.en
    │   ├── test.my
    │   ├── train.en
    │   └── train.my
    ├── nb_en
    │   ├── dev.en
    │   ├── dev.nb
    │   ├── test.en
    │   ├── test.nb
    │   ├── train.en
    │   └── train.nb
    ├── nl_en
    │   ├── dev.en
    │   ├── dev.nl
    │   ├── test.en
    │   ├── test.nl
    │   ├── train.en
    │   └── train.nl
    ├── pl_en
    │   ├── dev.en
    │   ├── dev.pl
    │   ├── test.en
    │   ├── test.pl
    │   ├── train.en
    │   └── train.pl
    ├── pt-br_en
    │   ├── dev.en
    │   ├── dev.pt-br
    │   ├── test.en
    │   ├── test.pt-br
    │   ├── train.en
    │   └── train.pt-br
    ├── pt_en
    │   ├── dev.en
    │   ├── dev.pt
    │   ├── test.en
    │   ├── test.pt
    │   ├── train.en
    │   └── train.pt
    ├── ro_en
    │   ├── dev.en
    │   ├── dev.ro
    │   ├── test.en
    │   ├── test.ro
    │   ├── train.en
    │   └── train.ro
    ├── ru_en
    │   ├── dev.en
    │   ├── dev.ru
    │   ├── test.en
    │   ├── test.ru
    │   ├── train.en
    │   └── train.ru
    ├── sk_en
    │   ├── dev.en
    │   ├── dev.sk
    │   ├── test.en
    │   ├── test.sk
    │   ├── train.en
    │   └── train.sk
    ├── sl_en
    │   ├── dev.en
    │   ├── dev.sl
    │   ├── test.en
    │   ├── test.sl
    │   ├── train.en
    │   └── train.sl
    ├── sq_en
    │   ├── dev.en
    │   ├── dev.sq
    │   ├── test.en
    │   ├── test.sq
    │   ├── train.en
    │   └── train.sq
    ├── sr_en
    │   ├── dev.en
    │   ├── dev.sr
    │   ├── test.en
    │   ├── test.sr
    │   ├── train.en
    │   └── train.sr
    ├── sv_en
    │   ├── dev.en
    │   ├── dev.sv
    │   ├── test.en
    │   ├── test.sv
    │   ├── train.en
    │   └── train.sv
    ├── ta_en
    │   ├── dev.en
    │   ├── dev.ta
    │   ├── test.en
    │   ├── test.ta
    │   ├── train.en
    │   └── train.ta
    ├── th_en
    │   ├── dev.en
    │   ├── dev.th
    │   ├── test.en
    │   ├── test.th
    │   ├── train.en
    │   └── train.th
    ├── tr_en
    │   ├── dev.en
    │   ├── dev.tr
    │   ├── test.en
    │   ├── test.tr
    │   ├── train.en
    │   └── train.tr
    ├── uk_en
    │   ├── dev.en
    │   ├── dev.uk
    │   ├── test.en
    │   ├── test.uk
    │   ├── train.en
    │   └── train.uk
    ├── ur_en
    │   ├── dev.en
    │   ├── dev.ur
    │   ├── test.en
    │   ├── test.ur
    │   ├── train.en
    │   └── train.ur
    ├── vi_en
    │   ├── dev.en
    │   ├── dev.vi
    │   ├── test.en
    │   ├── test.vi
    │   ├── train.en
    │   └── train.vi
    ├── zh-cn_en
    │   ├── dev.en
    │   ├── dev.zh-cn
    │   ├── test.en
    │   ├── test.zh-cn
    │   ├── train.en
    │   └── train.zh-cn
    ├── zh_en
    │   ├── dev.en
    │   ├── dev.zh
    │   ├── test.en
    │   ├── test.zh
    │   ├── train.en
    │   └── train.zh
    └── zh-tw_en
        ├── dev.en
        ├── dev.zh-tw
        ├── test.en
        ├── test.zh-tw
        ├── train.en
        └── train.zh-tw

60 directories, 354 files
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

## Check Myanmar Data

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ ls
dev.en  dev.my  test.en  test.my  train.en  train.my
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ wc *
    741   13293   66834 dev.en
    741   22491  212851 dev.my
   1504   30578  153883 test.en
   1504   49945  480504 test.my
  21497  430740 2160265 train.en
  21497  716879 6903838 train.my
  47484 1263926 9978175 total
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ head *
==> dev.en <==
First , a video .
Yes , it is a scrambled egg .
But as you look at it , I hope you &apos;ll begin to feel just slightly uneasy .
Because you may notice that what &apos;s actually happening is that the egg is unscrambling itself .
And you &apos;ll now see the yolk and the white have separated .
And now they &apos;re going to be poured back into the egg .
And we all know in our heart of hearts that this is not the way the universe works .
A scrambled egg is mush — tasty mush — but it &apos;s mush .
An egg is a beautiful , sophisticated thing that can create even more sophisticated things , such as chickens .
And we know in our heart of hearts that the universe does not travel from mush to complexity .

==> dev.my <==
ပထမဆုံး ၊ ဗီဒီယိုတစ ် ခု ။
ဟုတ ် ပါတယ ် ၊ ဒါက ကြက ် ဥမွှေကြော ် တစ ် လုံးပါ ။
ဒါပေမဲ ့ ကြည ့ ် လိုက ် စဉ ် မှာ ခင ် ဗျား နည ် းနည ် း စိတ ် မသက ် မသာဖြစ ် မိမယ ် လို ့ မျှော ် လင ့ ် ပါတယ ် ။
အကြောင ် းက တကယ ် ဖြစ ် နေတာက ကြက ် ဥဟာ သူ ့ ဘာသာ ဖော ် ထုတ ် နေတာ ခင ် ဗျားတို ့ သတိထားမိနိုင ် လို ့ ပါ ။
အခုဆို အနှစ ် နဲ ့ အကာဟာ ခွဲထွက ် သွားတာ မြင ် ရမှာပါ ။
အခု ဒါတွေကို ကြက ် ဥထဲကို ပြန ် လောင ် းထည ့ ် တော ့ မှာပါ ။
ကျွန ် တော ် တို ့ အားလုံးရဲ ့ ရင ် ထဲအသည ် းထဲမှာ သိနေတာက ဒါက စကြာဝဠာ အလုပ ် လုပ ် တဲ ့ ပုံ မဟုတ ် ဘူးပေါ ့ ။
ကြက ် ဥမွှေကြော ် က ပျော ့ ပြဲတယ ် ၊ အရသာရှိပေမဲ ့ ပျော ့ ပြဲတယ ် လေ ။
ကြက ် ဥတစ ် လုံးဟာ လှပ ၊ ဆန ် းပြားတဲ ့ အရာပါ ။ ကြက ် ကလေးတွေလို ပိုပြီးဆန ် းပြားတာတွေတောင ် ဖန ် တီးနိုင ် ပါတယ ် ။
ကျွန ် တော ် တို ့ ရင ် ထဲအသည ် းထဲက သိနေတာက စကြာဝဠာဟာ ပျော ့ ပြဲတာကနေ ရှုပ ် ထွေးမှုဆီ မသွားဘူးပေါ ့ ။

==> test.en <==
By the end of this year , there &apos;ll be nearly a billion people on this planet that actively use social networking sites .
The one thing that all of them have in common is that they &apos;re going to die .
While that might be a somewhat morbid thought , I think it has some really profound implications that are worth exploring .
What first got me thinking about this was a blog post authored earlier this year by Derek K. Miller , who was a science and technology journalist who died of cancer .
And what Miller did was have his family and friends write a post that went out shortly after he died .
Here &apos;s what he wrote in starting that out .
He said , &quot; &quot; Here it is . I &apos;m dead , and this is my last post to my blog .
In advance , I asked that once my body finally shut down from the punishments of my cancer , then my family and friends publish this prepared message I wrote — the first part of the process of turning this from an active website to an archive . &quot; &quot; Now , while as a journalist , Miller &apos;s archive may have been better written and more carefully curated than most , the fact of the matter is that all of us today are creating an archive that &apos;s something completely different than anything that &apos;s been created by any previous generation .
Consider a few stats for a moment .
Right now there are 48 hours of video being uploaded to YouTube every single minute .

==> test.my <==
ဒီနှစ ် ကုန ် လောက ် မှာ ဒီကမ ္ ဘာပေါ ် မှာ လူမှုရေးကွန ် ရက ် တွေကို စိတ ် ဝင ် တစားသုံးကြမယ ့ ် သူ သန ် း ၁ ထောင ် နီးပါးရှိလာလိမ ့ ် မယ ် ။
ဒီလူတွေအားလုံးမှာ တူနေတာတစ ် ခုက သူတို ့ တွေဟာ သေကြမှာပဲဖြစ ် ပါတယ ် ။
ဒါဟာ အနိဋ ္ ဌာရုံအတွေးလို ့ ဆိုနိုင ် ပေမဲ ့ စူးစမ ် းလေ ့ လာထိုက ် တဲ ့ တကယ ် ကို နက ် ရှိုင ် းတဲ ့ ဂယက ် ရိုက ် မှုတွေ ရှိတယ ် လို ့ ထင ် ပါတယ ် ။
ဒါကို ပထမဆုံး တွေးဖြစ ် မိတဲ ့ အကြောင ် းက ဒီနှစ ် အစောပိုင ် းက Derek Miller ရေးသားတဲ ့ ဘလော ့ ဂ ် ကြောင ့ ် ပါ ။ သူဟာ သိပ ္ ပံနဲ ့ နည ် းပညာ သတင ် းစာဆရာဖြစ ် ပြီး ကင ် ဆာနဲ ့ သေဆုံးခဲ ့ ပါတယ ် ။
Miller လုပ ် ခဲ ့ တာက သူ ့ မိသားစုနဲ ့ မိတ ် ဆွေတွေကို သူသေပြီးနောက ် မှာ ချက ် ချင ် းပဲ ပို ့ စ ် တစ ် ခုရေးတင ် ခိုင ် းတာပါ ။
ဒါက စစချင ် းမှာ သူရေးခဲ ့ တာပါ ။
သူပြောတာက &quot; &quot; ဟောဒီမှာ ၊ ကျုပ ် သေပြီ ၊ ဒါက ကျုပ ် ဘလော ့ ဂ ် ရဲ ့ နောက ် ဆုံး ပိုစ ့ ် ပါ ။
ကြိုတင ် ပြီး ကျုပ ် ရဲ ့ ခန ္ ဓာကိုယ ် ကို ကင ် ဆာရဲ ့ ဒဏ ် ခတ ် မှုတွေကနေ နောက ် ဆုံး တစ ် ခါတည ် းပိတ ် ချပစ ် လိုက ် တာနဲ ့ ဒီကြိုရေးထားတဲ ့ စာကိုတင ် ဖို ့ မိသားစု ၊ မိတ ် ဆွေတွေကို ပြောခဲ ့ တယ ် ။ လုပ ် ငန ် းစဉ ် ရဲ ့ ပထမပိုင ် းက ဒါကို သက ် ဝင ် တဲ ့ ဝက ် ဘ ် ဆိုဒ ် ကနေ မော ် ကွန ် းဘဏ ် ကို ပြောင ် းဖို ့ ပါ ။ ကဲ သတင ် းစာသမားတစ ် ယ ​ ောက ် ဆိုပေမည ့ ် လည ် း Miller ရဲ ့ မော ် ကွန ် းဘဏ ် ကိုရေးကာ အများစုထက ် ပိုဂရုစိုက ် ထိန ် းထားပါတယ ် ။ အမှန ် က ကျွန ် တော ် တို ့ အားလုံး ဒီနေ ့ မှာ အရင ် ကနဲ ့ မျိုးဆက ် တွေ ဖန ် တီးထားခဲ ့ တာတွေနဲ ့ ဘာမှမတူတဲ ့ မော ် ကွန ် းပြုစုခြင ် းကို ဖန ် တီးနေကြပါတယ ် ။
စာရင ် း တစ ် ချို ့ ကို တွေးကြည ့ ် လိုက ် ပါ ။
အခုအခါမှာ Youtube မှာ မိနစ ် တိုင ် းမှာ ဗီဒီယို ၄၈ နာရီကြာစာလောက ် ကို တင ် ဖြစ ် တယ ် ။

==> train.en <==
( Mechanical noises ) ( Music ) ( Applause )
This is about a place in London called Kiteflyer &apos;s Hill where I used to go and spend hours going &quot; &quot; When is he coming back ? When is he coming back ? &quot; &quot; So this is another one dedicated to that guy ...
who I &apos;ve got over .
But this is &quot; &quot; Kiteflyer &apos;s Hill . &quot; &quot; It &apos;s a beautiful song written by a guy called Martin Evan , actually , for me .
Boo Hewerdine , Thomas Dolby , thank you very much for inviting me . It &apos;s been a blessing singing for you .
Thank you very much .
♫ Do you remember when we used to go ♫ ♫ up to Kiteflyer &apos;s Hill ? ♫ ♫ Those summer nights , so still ♫ ♫ with all of the city beneath us ♫ ♫ and all of our lives ahead ♫ ♫ before cruel and foolish words ♫ ♫ were cruelly and foolishly said ♫ ♫ Some nights I think of you ♫ ♫ and then I go up ♫ ♫ on Kiteflyer &apos;s Hill ♫ ♫ wrapped up against the winter chill ♫ ♫ And somewhere in the city beneath me ♫ ♫ you lie asleep in your bed ♫ ♫ and I wonder if ever just briefly ♫
♫ do I creep in your dreams now and then ♫ ♫ Where are you now ? ♫ ♫ My wild summer love ♫ ♫ Where are you now ? ♫ ♫ Have the years been kind ? ♫ ♫ And do you think of me sometimes ♫ ♫ up on Kiteflyer &apos;s Hill ? ♫ ♫ Oh , I pray you one day will ♫ ♫ We won &apos;t say a word ♫ ♫ We won &apos;t need them ♫ ♫ Sometimes silence is best ♫ ♫ We &apos;ll just stand in the still of the evening ♫ ♫ and whisper farewell to loneliness ♫ ♫ Where are you now ? ♫ ♫ My wild summer love ♫ ♫ Where are you now ? ♫
♫ Do you think of me sometimes ? ♫ ♫ And do you ever make that climb ? ♫ ♫ Where are you now ? ♫ ♫ My wild summer love ♫ ♫ Where are you now ? ♫ ♫ Have the years been kind ? ♫ ♫ And do you ever make that climb ♫ ♫ up on Kiteflyer &apos;s Hill ? Kiteflyer &apos;s ... ♫ ♫ &#91; French &#93; ♫ ♫ Where are you ? Where are you now ? ♫ ♫ Where are you now ? ♫ ♫ Kiteflyer &apos;s ... ♫ ( Applause ) Gracias . Thank you very much .
I &apos;m actually here to make a challenge to people .

==> train.my <==
( စက ် ပိုင ် းဆိုင ် ရာ ဆူညံသံများ ) ( ဂီတသံ ) ( လက ် ခုပ ် သံများ )
ဒီအကြောင ် းက လန ် ဒန ် က &apos; စွန ် လွှတ ် သူရဲ ့ တောင ် ကုန ် း &quot; &quot; လို ့ ခေါ ် တဲ ့ နေရာပါ ။ သွားပြီး နာရီတွေကို ကုန ် ဆုံးလေ ့ ရှိတဲ ့ နေရာပါ &apos; သူဘယ ် တော ့ ပြန ် လာမလဲ &apos; &apos; သူဘယ ် တော ့ ပြန ် လာမလဲ &apos; လို ့ ဆိုရင ် း ဒီတော ့ ဒါဟာ အဲ ့ ဒီလူကိုရည ် စူးတဲ ့ နောက ် တစ ် ခုပေါ ့ ၊
ပြီးပျောက ် သွားတဲ ့ သူပါ ။
ဒါပေမဲ ့ ဒါက စွန ် လွှတ ် တဲ ့ သူရဲ ့ တောင ် ကုန ် းပါ ဒါက Martin Evan ဆိုတဲ ့ လူရေးစပ ် တဲ ့ လှပတဲ ့ သီချင ် းတစ ် ပုဒ ် ၊ တကယ ် က ကျွန ် မအတွက ် ပါ ။
Boo Hewerdine Thomas Dolby ဖိတ ် တဲ ့ အတွက ် ကျေးဇူးပါ ၊ ရှင ် တို ့ အတွက ် ကောင ် းချီးပေး သီဆိုခြင ် းပါ
ကျေးဇူးအများကြီး တင ် ပါတယ ် ။
စွန ် လွှတ ် သူတောင ် ကုန ် းဆီကို တက ် သွားခဲ ့ ဖူးတဲ ့ ​ အချိန ် ကို မှတ ် မိလား ။ ဒီနွေရာသီညတွေ ၊ ကိုယ ် တို ့ အောက ် ခြေက မြို ့ ရဲ ့ အားလုံးနဲ ့ အတူ ရှိနေဆဲပါ ။ ရှေ ့ ဆက ် မယ ့ ် ကိုယ ် တို ဘဝတွေ အားလုံးအတွက ် ၊ ရက ် စက ် ပြီး မိုက ် မဲတဲ ့ စကားလုံးတွေ ရက ် ရက ် စက ် စက ် မိုက ် မိုက ် မဲမဲ မပြောမီက တစ ် ချို ့ ညတွေ ကိုယ ် မင ် းကိုတွေးမိတယ ် ၊ ပြီးတော ့ စွန ် လွှတ ် သူရဲ ့ တောင ် ကုန ် းပေါ ် ကိုယ ် လှမ ် းခဲ ့ တာပေါ ့ ။ ဆောင ် းရာသီ အအေးဒဏ ် ကို အံတုထွေးပတ ် လို ့ လေ ။ ကိုယ ့ ် အောက ် ခြေက မြို ့ ရဲ ့ တစ ် နေရာရာမှာ မင ် းကတော ့ အိပ ် ခန ် းထဲ လဲလျောင ် းအိပ ် စက ် နေတာပေါ ့ ။ ပြီးတော ့ တွေးမိတာက တစ ် ခါတစ ် ခါမှာ မင ် းရဲ ့
အိပ ် မက ် တွေထဲ ခဏလေး ခိုးဝင ် လိုက ် ရရင ် များလို ့ လေ ။ အခုမင ် းဘယ ် မှာလဲ ။ ကိုယ ့ ် ရဲ ့ နွေရာသီ အချစ ် ရူးရေ အခုမင ် းဘယ ် မှာလဲ ။ နှစ ် ကာလတွေဖြတ ် သန ် းတာ ညင ် သာပါရဲ ့ လား ၊ ပြီးတော ့ စွန ် လွတ ် သူရဲ ့ တောင ် ကုန ် းပေါ ် က ကိုယ ့ ် ကို တစ ် ခါတစ ် လေ တွေးမိလား ။ အို တစ ် နေ ့ တော ့ မင ် းတွေးမိမှာ လို ့ ပဲ ဆုတောင ် းပါတယ ် ။ စကားတစ ် ခွန ် းမှ ကိုယ ် တို ့ ပြောမှာမဟုတ ် တော ့ ဘူးလေ ၊ ဒါတွေ လိုတော ့ မှာ မဟုတ ် ဘူးလေ ။ တစ ် ခါတစ ် လေကျတော ့ တိတ ် ဆိတ ် ခြင ် းက အကောင ် းဆုံးပါ ၊ ညနေခင ် းရဲ ့ ဆိတ ် ငြိမ ် မှုထဲ ကိုယ ် တို ့ ရပ ် နေရုံ ရပ ် နေပြီး အထီးကျန ် မှုကို နှုတ ် ဆက ် စကား တိုးတိုးလေးပြောကြမယ ် လေ ။ အခုမင ် းဘယ ် မှာလဲ ။ ကိုယ ့ ် ရဲ ့ နွေရာသီ အချစ ် ရူးရေ အခုမင ် းဘယ ် မှာလဲ ။
တစ ် ခါတစ ် လေ ကိုယ ့ ် အကြောင ် း တွေးမိလား ။ စွန ် လွှတ ် သူကုန ် းပေါ ် မင ် းတက ် တုန ် းလား ။ အခုမင ် းဘယ ် မှာလဲ ။ ကိုယ ့ ် ရဲ ့ နွေရာသီ အချစ ် ရူးရေ အခုမင ် းဘယ ် မှာလဲ ။ ပြီးတော ့ နှစ ် ကာလတွေ ဖြတ ် သန ် းတာ ညင ် သာပါရဲ ့ လား ၊ စွန ် လွှတ ် သူကုန ် းပေါ ် မင ် း တက ် ဖြစ ် တုန ် းလား ။ စွန ် လွှတ ် ကုန ် းရဲ ့ ..... စွန ် တွေဆီကိုပေါ ့ ... အခုမင ် းဘယ ် မှာလဲ ။ အခုမင ် းဘယ ် မှာလဲ ။ အခုမင ် းဘယ ် မှာလဲ ။ စွန ် လွှတ ် သူရဲ ့ .... ( လက ် ခုပ ် သံများ ) ကျေးဇူး ကျေးဇူး အများကြီးတင ် ပါတယ ် ရှင ် ။
တကယ ် က ကျွန ် မ ဒီကိုရောက ် လာတာက လူတွေကို စိမ ် ခေါ ် မှုတစ ် ခု လုပ ် ချင ် လို ့ ပါ ။
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$
```

## Check Japanese Data

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data$ cd ja_en
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ja_en$ ls
dev.en  dev.ja  test.en  test.ja  train.en  train.ja
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ja_en$ wc *
    4429    89107   442013 dev.en
    4429    19524   495770 dev.ja
    5565   110961   554462 test.en
    5565    22835   603768 test.ja
  204090  4263251 21431280 train.en
  204090   886227 23740455 train.ja
  428168  5391905 47267748 total
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ja_en$ head -n 3 *
==> dev.en <==
When I was 11 , I remember waking up one morning to the sound of joy in my house .
My father was listening to BBC News on his small , gray radio .
There was a big smile on his face which was unusual then , because the news mostly depressed him .

==> dev.ja <==
私が11才の時のことです ある朝 家中に湧き上がった 歓声に目を覚ましました
父はグレーの小型ラジオで BBCニュースを聞いていました
そして 珍しく 満面の笑みを浮かべていました 普段は暗いニュースに 落ち込んでばかりいましたから

==> test.en <==
By the end of this year , there &apos;ll be nearly a billion people on this planet that actively use social networking sites .
The one thing that all of them have in common is that they &apos;re going to die .
While that might be a somewhat morbid thought , I think it has some really profound implications that are worth exploring .

==> test.ja <==
今年の終わりには 世界中で 10億人近くがソーシャルネットワークのサイトを 活発に使っているでしょう
１つ全員に共通して言えるのは 皆いずれ死ぬということです
なんとなく陰気な考えである一方 これには検討に値する 実に深い意味があると思います

==> train.en <==
Amongst all the troubling deficits we struggle with today — we think of financial and economic primarily — the ones that concern me most is the deficit of political dialogue — our ability to address modern conflicts as they are , to go to the source of what they &apos;re all about and to understand the key players and to deal with them .
We who are diplomats , we are trained to deal with conflicts between states and issues between states .
There is trade , there is disarmament , there is cross-border relations .

==> train.ja <==
我々が今日直面している 様々な機能不全のなかで — 財政や経済が最初に思いつきますが — 私が一番 憂慮しているのは 政治的対話の欠乏です 我々 が 近年の紛争において 状況を把握し その根本原因を探り 中心人物を理解し 彼らと交渉をする能力です
我々外交官は 国家間の紛争や問題に対処するよう 訓練されています
貿易や軍縮の 国境を越えた問題などに 対処しなければなりません
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ja_en$
```

## Syllable Breaking for Myanmar Language

Current segmentation is wired ...  and thus, I made a syllable segmentation.  
1st, keep the original data under original/ folder, copied syllable breaking and space cleaning perl scripts to working folder ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ ls
dev.en  dev.my  test.en  test.my  train.en  train.my
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ mkdir original
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ cp *.my ./original/
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ mkdir mk-syl
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ mv *.my ./mk-syl/
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ cd mk-syl/
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ cp /home/ye/tool/xnmt/exp/asean-myth-syl/data/mk-syl/*.pl .
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ ls
clean-space.pl  dev.my  print-blank-lines.pl  sylbreak.pl  test.my  train.my
```
check file encoding ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ file *.my
dev.my:   Unicode text, UTF-8 text, with very long lines (432)
test.my:  Unicode text, UTF-8 text, with very long lines (614)
train.my: Unicode text, UTF-8 text, with very long lines (704)
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$
```

remove spaces ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ head ./test.my
ဒီနှစ ် ကုန ် လောက ် မှာ ဒီကမ ္ ဘာပေါ ် မှာ လူမှုရေးကွန ် ရက ် တွေကို စိတ ် ဝင ် တစားသုံးကြမယ ့ ် သူ သန ် း ၁ ထောင ် နီးပါးရှိလာလိမ ့ ် မယ ် ။
ဒီလူတွေအားလုံးမှာ တူနေတာတစ ် ခုက သူတို ့ တွေဟာ သေကြမှာပဲဖြစ ် ပါတယ ် ။
ဒါဟာ အနိဋ ္ ဌာရုံအတွေးလို ့ ဆိုနိုင ် ပေမဲ ့ စူးစမ ် းလေ ့ လာထိုက ် တဲ ့ တကယ ် ကို နက ် ရှိုင ် းတဲ ့ ဂယက ် ရိုက ် မှုတွေ ရှိတယ ် လို ့ ထင ် ပါတယ ် ။
ဒါကို ပထမဆုံး တွေးဖြစ ် မိတဲ ့ အကြောင ် းက ဒီနှစ ် အစောပိုင ် းက Derek Miller ရေးသားတဲ ့ ဘလော ့ ဂ ် ကြောင ့ ် ပါ ။ သူဟာ သိပ ္ ပံနဲ ့ နည ် းပညာ သတင ် းစာဆရာဖြစ ် ပြီး ကင ် ဆာနဲ ့ သေဆုံးခဲ ့ ပါတယ ် ။
Miller လုပ ် ခဲ ့ တာက သူ ့ မိသားစုနဲ ့ မိတ ် ဆွေတွေကို သူသေပြီးနောက ် မှာ ချက ် ချင ် းပဲ ပို ့ စ ် တစ ် ခုရေးတင ် ခိုင ် းတာပါ ။
ဒါက စစချင ် းမှာ သူရေးခဲ ့ တာပါ ။
သူပြောတာက &quot; &quot; ဟောဒီမှာ ၊ ကျုပ ် သေပြီ ၊ ဒါက ကျုပ ် ဘလော ့ ဂ ် ရဲ ့ နောက ် ဆုံး ပိုစ ့ ် ပါ ။
ကြိုတင ် ပြီး ကျုပ ် ရဲ ့ ခန ္ ဓာကိုယ ် ကို ကင ် ဆာရဲ ့ ဒဏ ် ခတ ် မှုတွေကနေ နောက ် ဆုံး တစ ် ခါတည ် းပိတ ် ချပစ ် လိုက ် တာနဲ ့ ဒီကြိုရေးထားတဲ ့ စာကိုတင ် ဖို ့ မိသားစု ၊ မိတ ် ဆွေတွေကို ပြောခဲ ့ တယ ် ။ လုပ ် ငန ် းစဉ ် ရဲ ့ ပထမပိုင ် းက ဒါကို သက ် ဝင ် တဲ ့ ဝက ် ဘ ် ဆိုဒ ် ကနေ မော ် ကွန ် းဘဏ ် ကို ပြောင ် းဖို ့ ပါ ။ ကဲ သတင ် းစာသမားတစ ် ယ ​ ောက ် ဆိုပေမည ့ ် လည ် း Miller ရဲ ့ မော ် ကွန ် းဘဏ ် ကိုရေးကာ အများစုထက ် ပိုဂရုစိုက ် ထိန ် းထားပါတယ ် ။ အမှန ် က ကျွန ် တော ် တို ့ အားလုံး ဒီနေ ့ မှာ အရင ် ကနဲ ့ မျိုးဆက ် တွေ ဖန ် တီးထားခဲ ့ တာတွေနဲ ့ ဘာမှမတူတဲ ့ မော ် ကွန ် းပြုစုခြင ် းကို ဖန ် တီးနေကြပါတယ ် ။
စာရင ် း တစ ် ချို ့ ကို တွေးကြည ့ ် လိုက ် ပါ ။
အခုအခါမှာ Youtube မှာ မိနစ ် တိုင ် းမှာ ဗီဒီယို ၄၈ နာရီကြာစာလောက ် ကို တင ် ဖြစ ် တယ ် ။
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ ```
>
> ```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ sed 's/[[:blank:]]//g' ./test.my > ./test.my.nospace
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ head ./test.my.nospace
ဒီနှစ်ကုန်လောက်မှာဒီကမ္ဘာပေါ်မှာလူမှုရေးကွန်ရက်တွေကိုစိတ်ဝင်တစားသုံးကြမယ့်သူသန်း၁ထောင်နီးပါးရှိလာလိမ့်မယ်။
ဒီလူတွေအားလုံးမှာတူနေတာတစ်ခုကသူတို့တွေဟာသေကြမှာပဲဖြစ်ပါတယ်။
ဒါဟာအနိဋ္ဌာရုံအတွေးလို့ဆိုနိုင်ပေမဲ့စူးစမ်းလေ့လာထိုက်တဲ့တကယ်ကိုနက်ရှိုင်းတဲ့ဂယက်ရိုက်မှုတွေရှိတယ်လို့ထင်ပါတယ်။
ဒါကိုပထမဆုံးတွေးဖြစ်မိတဲ့အကြောင်းကဒီနှစ်အစောပိုင်းကDerekMillerရေးသားတဲ့ဘလော့ဂ်ကြောင့်ပါ။သူဟာသိပ္ပံနဲ့နည်းပညာသတင်းစာဆရာဖြစ်ပြီးကင်ဆာနဲ့သေဆုံးခဲ့ပါတယ်။
Millerလုပ်ခဲ့တာကသူ့မိသားစုနဲ့မိတ်ဆွေတွေကိုသူသေပြီးနောက်မှာချက်ချင်းပဲပို့စ်တစ်ခုရေးတင်ခိုင်းတာပါ။
ဒါကစစချင်းမှာသူရေးခဲ့တာပါ။
သူပြောတာက&quot;&quot;ဟောဒီမှာ၊ကျုပ်သေပြီ၊ဒါကကျုပ်ဘလော့ဂ်ရဲ့နောက်ဆုံးပိုစ့်ပါ။
ကြိုတင်ပြီးကျုပ်ရဲ့ခန္ဓာကိုယ်ကိုကင်ဆာရဲ့ဒဏ်ခတ်မှုတွေကနေနောက်ဆုံးတစ်ခါတည်းပိတ်ချပစ်လိုက်တာနဲ့ဒီကြိုရေးထားတဲ့စာကိုတင်ဖို့မိသားစု၊မိတ်ဆွေတွေကိုပြောခဲ့တယ်။လုပ်ငန်းစဉ်ရဲ့ပထမပိုင်းကဒါကိုသက်ဝင်တဲ့ဝက်ဘ်ဆိုဒ်ကနေမော်ကွန်းဘဏ်ကိုပြောင်းဖို့ပါ။ကဲသတင်းစာသမားတစ်ယ​ောက်ဆိုပေမည့်လည်းMillerရဲ့မော်ကွန်းဘဏ်ကိုရေးကာအများစုထက်ပိုဂရုစိုက်ထိန်းထားပါတယ်။အမှန်ကကျွန်တော်တို့အားလုံးဒီနေ့မှာအရင်ကနဲ့မျိုးဆက်တွေဖန်တီးထားခဲ့တာတွေနဲ့ဘာမှမတူတဲ့မော်ကွန်းပြုစုခြင်းကိုဖန်တီးနေကြပါတယ်။
စာရင်းတစ်ချို့ကိုတွေးကြည့်လိုက်ပါ။
အခုအခါမှာYoutubeမှာမိနစ်တိုင်းမှာဗီဒီယို၄၈နာရီကြာစာလောက်ကိုတင်ဖြစ်တယ်။
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$
```

space removing for dev and train data also ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ sed 's/[[:blank:]]//g' ./dev.my > ./dev.my.nospace
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ sed 's/[[:blank:]]//g' ./train.my > ./train.my.nos
pace
```

check the output files:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ head -n 3 ./dev.my.nospace
ပထမဆုံး၊ဗီဒီယိုတစ်ခု။
ဟုတ်ပါတယ်၊ဒါကကြက်ဥမွှေကြော်တစ်လုံးပါ။
ဒါပေမဲ့ကြည့်လိုက်စဉ်မှာခင်ဗျားနည်းနည်းစိတ်မသက်မသာဖြစ်မိမယ်လို့မျှော်လင့်ပါတယ်။
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ head -n 3 ./train.my.nospace
(စက်ပိုင်းဆိုင်ရာဆူညံသံများ)(ဂီတသံ)(လက်ခုပ်သံများ)
ဒီအကြောင်းကလန်ဒန်က&apos;စွန်လွှတ်သူရဲ့တောင်ကုန်း&quot;&quot;လို့ခေါ်တဲ့နေရာပါ။သွားပြီးနာရီတွေကိုကုန်ဆုံးလေ့ရှိတဲ့နေရာပါ&apos;သူဘယ်တော့ပြန်လာမလဲ&apos;&apos;သူဘယ်တော့ပြန်လာမလဲ&apos;လို့ဆိုရင်းဒီတော့ဒါဟာအဲ့ဒီလူကိုရည်စူးတဲ့နောက်တစ်ခုပေါ့၊
ပြီးပျောက်သွားတဲ့သူပါ။
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$
```

syllable breaking ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ perl ./sylbreak.pl -i ./train.my.nospace -s " " > ./train.syl
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ perl ./sylbreak.pl -i ./dev.my.nospace -s " " > ./
dev.syl
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ perl ./sylbreak.pl -i ./test.my.nospace -s " " > .
/test.syl
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$
```

checking the syllable breaked Myanmar text files ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ head -n 3 {train,dev,test}.syl
==> train.syl <==
 ( စက် ပိုင်း ဆိုင် ရာ ဆူ ညံ သံ များ ) ( ဂီ တ သံ ) ( လက် ခုပ် သံ များ )
 ဒီ အ ကြောင်း က လန် ဒန် က & a p o s ; စွန် လွှတ် သူ ရဲ့ တောင် ကုန်း & q u o t ; & q u o t ; လို့ ခေါ် တဲ့ နေ ရာ ပါ ။ သွား ပြီး နာ ရီ တွေ ကို ကုန် ဆုံး လေ့ ရှိ တဲ့ နေ ရာ ပါ & a p o s ; သူ ဘယ် တော့ ပြန် လာ မ လဲ & a p o s ; & a p o s ; သူ ဘယ် တော့ ပြန် လာ မ လဲ & a p o s ; လို့ ဆို ရင်း ဒီ တော့ ဒါ ဟာ အဲ့ ဒီ လူ ကို ရည် စူး တဲ့ နောက် တစ် ခု ပေါ့ ၊
 ပြီး ပျောက် သွား တဲ့ သူ ပါ ။

==> dev.syl <==
 ပ ထ မ ဆုံး ၊ ဗီ ဒီ ယို တစ် ခု ။
 ဟုတ် ပါ တယ် ၊ ဒါ က ကြက် ဥ မွှေ ကြော် တစ် လုံး ပါ ။
 ဒါ ပေ မဲ့ ကြ ည့် လိုက် စဉ် မှာ ခင် ဗျား နည်း နည်း စိတ် မ သက် မ သာ ဖြစ် မိ မယ် လို့ မျှော် လ င့် ပါ တယ် ။

==> test.syl <==
 ဒီ နှစ် ကုန် လောက် မှာ ဒီ ကမ္ဘာ ပေါ် မှာ လူ မှု ရေး ကွန် ရက် တွေ ကို စိတ် ဝင် တ စား သုံး ကြ မ ယ့် သူ သန်း ၁ ထောင် နီး ပါး ရှိ လာ လိ မ့် မယ် ။
 ဒီ လူ တွေ အား လုံး မှာ တူ နေ တာ တစ် ခု က သူ တို့ တွေ ဟာ သေ ကြ မှာ ပဲ ဖြစ် ပါ တယ် ။
 ဒါ ဟာ အ နိဋ္ဌာ ရုံ အ တွေး လို့ ဆို နိုင် ပေ မဲ့ စူး စမ်း လေ့ လာ ထိုက် တဲ့ တ ကယ် ကို နက် ရှိုင်း တဲ့ ဂ ယက် ရိုက် မှု တွေ ရှိ တယ် လို့ ထင် ပါ တယ် ။
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$
```

I wanna change "& q u o t ;" to ```&quot;```   
and also for "& a p o s ;" ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ sed "s/\\& q u o t ;/\\&quot;/g" ./test.syl | sed "s/\\& a p o s ;/\\&apos;/g"> ./test.syl.clean
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ sed "s/\\& q u o t ;/\\&quot;/g" ./dev.syl | sed "
s/\\& a p o s ;/\\&apos;/g"> ./dev.syl.clean
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ sed "s/\\& q u o t ;/\\&quot;/g" ./train.syl | sed
 "s/\\& a p o s ;/\\&apos;/g"> ./train.syl.clean
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$
```

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$ head {train,dev,test}*.clean
==> train.syl.clean <==
 ( စက် ပိုင်း ဆိုင် ရာ ဆူ ညံ သံ များ ) ( ဂီ တ သံ ) ( လက် ခုပ် သံ များ )
 ဒီ အ ကြောင်း က လန် ဒန် က &apos; စွန် လွှတ် သူ ရဲ့ တောင် ကုန်း &quot; &quot; လို့ ခေါ် တဲ့ နေ ရာ ပါ ။ သွား ပြီး နာ ရီ တွေ ကို ကုန် ဆုံး လေ့ ရှိ တဲ့ နေ ရာ ပါ &apos; သူ ဘယ် တော့ ပြန် လာ မ လဲ &apos; &apos; သူ ဘယ် တော့ ပြန် လာ မ လဲ &apos; လို့ ဆို ရင်း ဒီ တော့ ဒါ ဟာ အဲ့ ဒီ လူ ကို ရည် စူး တဲ့ နောက် တစ် ခု ပေါ့ ၊
 ပြီး ပျောက် သွား တဲ့ သူ ပါ ။
 ဒါ ပေ မဲ့ ဒါ က စွန် လွှတ် တဲ့ သူ ရဲ့ တောင် ကုန်း ပါ ဒါ က M a r t i n E v a n ဆို တဲ့ လူ ရေး စပ် တဲ့ လှ ပ တဲ့ သီ ချင်း တစ် ပုဒ် ၊ တ ကယ် က ကျွန် မ အ တွက် ပါ ။
 B o o H e w e r d i n e T h o m a s D o l b y ဖိတ် တဲ့ အ တွက် ကျေး ဇူး ပါ ၊ ရှင် တို့ အ တွက် ကောင်း ချီး ပေး သီ ဆို ခြင်း ပါ
 ကျေး ဇူး အ များ ကြီး တင် ပါ တယ် ။
 စွန် လွှတ် သူ တောင် ကုန်း ဆီ ကို တက် သွား ခဲ့ ဖူး တဲ့​ အ ချိန် ကို မှတ် မိ လား ။ ဒီ နွေ ရာ သီ ည တွေ ၊ ကိုယ် တို့ အောက် ခြေ က မြို့ ရဲ့ အား လုံး နဲ့ အ တူ ရှိ နေ ဆဲ ပါ ။ ရှေ့ ဆက် မ ယ့် ကိုယ် တို ဘ ဝ တွေ အား လုံး အ တွက် ၊ ရက် စက် ပြီး မိုက် မဲ တဲ့ စ ကား လုံး တွေ ရက် ရက် စက် စက် မိုက် မိုက် မဲ မဲ မ ပြော မီ က တစ် ချို့ ည တွေ ကိုယ် မင်း ကို တွေး မိ တယ် ၊ ပြီး တော့ စွန် လွှတ် သူ ရဲ့ တောင် ကုန်း ပေါ် ကိုယ် လှမ်း ခဲ့ တာ ပေါ့ ။ ဆောင်း ရာ သီ အ အေး ဒဏ် ကို အံ တု ထွေး ပတ် လို့ လေ ။ ကို ယ့် အောက် ခြေ က မြို့ ရဲ့ တစ် နေ ရာ ရာ မှာ မင်း က တော့ အိပ် ခန်း ထဲ လဲ လျောင်း အိပ် စက် နေ တာ ပေါ့ ။ ပြီး တော့ တွေး မိ တာ က တစ် ခါ တစ် ခါ မှာ မင်း ရဲ့
 အိပ် မက် တွေ ထဲ ခ ဏ လေး ခိုး ဝင် လိုက် ရ ရင် များ လို့ လေ ။ အ ခု မင်း ဘယ် မှာ လဲ ။ ကို ယ့် ရဲ့ နွေ ရာ သီ အ ချစ် ရူး ရေ အ ခု မင်း ဘယ် မှာ လဲ ။ နှစ် ကာ လ တွေ ဖြတ် သန်း တာ ညင် သာ ပါ ရဲ့ လား ၊ ပြီး တော့ စွန် လွတ် သူ ရဲ့ တောင် ကုန်း ပေါ် က ကို ယ့် ကို တစ် ခါ တစ် လေ တွေး မိ လား ။ အို တစ် နေ့ တော့ မင်း တွေး မိ မှာ လို့ ပဲ ဆု တောင်း ပါ တယ် ။ စ ကား တစ် ခွန်း မှ ကိုယ် တို့ ပြော မှာ မ ဟုတ် တော့ ဘူး လေ ၊ ဒါ တွေ လို တော့ မှာ မ ဟုတ် ဘူး လေ ။ တစ် ခါ တစ် လေ ကျ တော့ တိတ် ဆိတ် ခြင်း က အ ကောင်း ဆုံး ပါ ၊ ည နေ ခင်း ရဲ့ ဆိတ် ငြိမ် မှု ထဲ ကိုယ် တို့ ရပ် နေ ရုံ ရပ် နေ ပြီး အ ထီး ကျန် မှု ကို နှုတ် ဆက် စ ကား တိုး တိုး လေး ပြော ကြ မယ် လေ ။ အ ခု မင်း ဘယ် မှာ လဲ ။ ကို ယ့် ရဲ့ နွေ ရာ သီ အ ချစ် ရူး ရေ အ ခု မင်း ဘယ် မှာ လဲ ။
 တစ် ခါ တစ် လေ ကို ယ့် အ ကြောင်း တွေး မိ လား ။ စွန် လွှတ် သူ ကုန်း ပေါ် မင်း တက် တုန်း လား ။ အ ခု မင်း ဘယ် မှာ လဲ ။ ကို ယ့် ရဲ့ နွေ ရာ သီ အ ချစ် ရူး ရေ အ ခု မင်း ဘယ် မှာ လဲ ။ ပြီး တော့ နှစ် ကာ လ တွေ ဖြတ် သန်း တာ ညင် သာ ပါ ရဲ့ လား ၊ စွန် လွှတ် သူ ကုန်း ပေါ် မင်း တက် ဖြစ် တုန်း လား ။ စွန် လွှတ် ကုန်း ရဲ့ . . . . . စွန် တွေ ဆီ ကို ပေါ့ . . . အ ခု မင်း ဘယ် မှာ လဲ ။ အ ခု မင်း ဘယ် မှာ လဲ ။ အ ခု မင်း ဘယ် မှာ လဲ ။ စွန် လွှတ် သူ ရဲ့ . . . . ( လက် ခုပ် သံ များ ) ကျေး ဇူး ကျေး ဇူး အ များ ကြီး တင် ပါ တယ် ရှင် ။
 တ ကယ် က ကျွန် မ ဒီ ကို ရောက် လာ တာ က လူ တွေ ကို စိမ် ခေါ် မှု တစ် ခု လုပ် ချင် လို့ ပါ ။

==> dev.syl.clean <==
 ပ ထ မ ဆုံး ၊ ဗီ ဒီ ယို တစ် ခု ။
 ဟုတ် ပါ တယ် ၊ ဒါ က ကြက် ဥ မွှေ ကြော် တစ် လုံး ပါ ။
 ဒါ ပေ မဲ့ ကြ ည့် လိုက် စဉ် မှာ ခင် ဗျား နည်း နည်း စိတ် မ သက် မ သာ ဖြစ် မိ မယ် လို့ မျှော် လ င့် ပါ တယ် ။
 အ ကြောင်း က တ ကယ် ဖြစ် နေ တာ က ကြက် ဥ ဟာ သူ့ ဘာ သာ ဖော် ထုတ် နေ တာ ခင် ဗျား တို့ သ တိ ထား မိ နိုင် လို့ ပါ ။
 အ ခု ဆို အ နှစ် နဲ့ အ ကာ ဟာ ခွဲ ထွက် သွား တာ မြင် ရ မှာ ပါ ။
 အ ခု ဒါ တွေ ကို ကြက် ဥ ထဲ ကို ပြန် လောင်း ထ ည့် တော့ မှာ ပါ ။
 ကျွန် တော် တို့ အား လုံး ရဲ့ ရင် ထဲ အ သည်း ထဲ မှာ သိ နေ တာ က ဒါ က စ ကြာ ဝ ဠာ အ လုပ် လုပ် တဲ့ ပုံ မ ဟုတ် ဘူး ပေါ့ ။
 ကြက် ဥ မွှေ ကြော် က ပျော့ ပြဲ တယ် ၊ အ ရ သာ ရှိ ပေ မဲ့ ပျော့ ပြဲ တယ် လေ ။
 ကြက် ဥ တစ် လုံး ဟာ လှ ပ ၊ ဆန်း ပြား တဲ့ အ ရာ ပါ ။ ကြက် က လေး တွေ လို ပို ပြီး ဆန်း ပြား တာ တွေ တောင် ဖန် တီး နိုင် ပါ တယ် ။
 ကျွန် တော် တို့ ရင် ထဲ အ သည်း ထဲ က သိ နေ တာ က စ ကြာ ဝ ဠာ ဟာ ပျော့ ပြဲ တာ က နေ ရှုပ် ထွေး မှု ဆီ မ သွား ဘူး ပေါ့ ။

==> test.syl.clean <==
 ဒီ နှစ် ကုန် လောက် မှာ ဒီ ကမ္ဘာ ပေါ် မှာ လူ မှု ရေး ကွန် ရက် တွေ ကို စိတ် ဝင် တ စား သုံး ကြ မ ယ့် သူ သန်း ၁ ထောင် နီး ပါး ရှိ လာ လိ မ့် မယ် ။
 ဒီ လူ တွေ အား လုံး မှာ တူ နေ တာ တစ် ခု က သူ တို့ တွေ ဟာ သေ ကြ မှာ ပဲ ဖြစ် ပါ တယ် ။
 ဒါ ဟာ အ နိဋ္ဌာ ရုံ အ တွေး လို့ ဆို နိုင် ပေ မဲ့ စူး စမ်း လေ့ လာ ထိုက် တဲ့ တ ကယ် ကို နက် ရှိုင်း တဲ့ ဂ ယက် ရိုက် မှု တွေ ရှိ တယ် လို့ ထင် ပါ တယ် ။
 ဒါ ကို ပ ထ မ ဆုံး တွေး ဖြစ် မိ တဲ့ အ ကြောင်း က ဒီ နှစ် အ စော ပိုင်း က D e r e k M i l l e r ရေး သား တဲ့ ဘ လော့ဂ် ကြော င့် ပါ ။ သူ ဟာ သိပ္ပံ နဲ့ နည်း ပ ညာ သ တင်း စာ ဆ ရာ ဖြစ် ပြီး ကင် ဆာ နဲ့ သေ ဆုံး ခဲ့ ပါ တယ် ။
 M i l l e r လုပ် ခဲ့ တာ က သူ့ မိ သား စု နဲ့ မိတ် ဆွေ တွေ ကို သူ သေ ပြီး နောက် မှာ ချက် ချင်း ပဲ ပို့စ် တစ် ခု ရေး တင် ခိုင်း တာ ပါ ။
 ဒါ က စ စ ချင်း မှာ သူ ရေး ခဲ့ တာ ပါ ။
 သူ ပြော တာ က &quot; &quot; ဟော ဒီ မှာ ၊ ကျုပ် သေ ပြီ ၊ ဒါ က ကျုပ် ဘ လော့ဂ် ရဲ့ နောက် ဆုံး ပို စ့် ပါ ။
 ကြို တင် ပြီး ကျုပ် ရဲ့ ခန္ဓာ ကိုယ် ကို ကင် ဆာ ရဲ့ ဒဏ် ခတ် မှု တွေ က နေ နောက် ဆုံး တစ် ခါ တည်း ပိတ် ချ ပစ် လိုက် တာ နဲ့ ဒီ ကြို ရေး ထား တဲ့ စာ ကို တင် ဖို့ မိ သား စု ၊ မိတ် ဆွေ တွေ ကို ပြော ခဲ့ တယ် ။ လုပ် ငန်း စဉ် ရဲ့ ပ ထ မ ပိုင်း က ဒါ ကို သက် ဝင် တဲ့ ဝက်ဘ် ဆိုဒ် က နေ မော် ကွန်း ဘဏ် ကို ပြောင်း ဖို့ ပါ ။ ကဲ သ တင်း စာ သ မား တစ် ယ​ောက် ဆို ပေ မ ည့် လည်း M i l l e r ရဲ့ မော် ကွန်း ဘဏ် ကို ရေး ကာ အ များ စု ထက် ပို ဂ ရု စိုက် ထိန်း ထား ပါ တယ် ။ အ မှန် က ကျွန် တော် တို့ အား လုံး ဒီ နေ့ မှာ အ ရင် က နဲ့ မျိုး ဆက် တွေ ဖန် တီး ထား ခဲ့ တာ တွေ နဲ့ ဘာ မှ မ တူ တဲ့ မော် ကွန်း ပြု စု ခြင်း ကို ဖန် တီး နေ ကြ ပါ တယ် ။
 စာ ရင်း တစ် ချို့ ကို တွေး ကြ ည့် လိုက် ပါ ။
 အ ခု အ ခါ မှာ Y o u t u b e မှာ မိ နစ် တိုင်း မှာ ဗီ ဒီ ယို ၄ ၈ နာ ရီ ကြာ စာ လောက် ကို တင် ဖြစ် တယ် ။
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en/mk-syl$
```

copy syllable breaked files to "ted-data/my_en/" path:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ ls
dev.en  mk-syl  original  test.en  train.en
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ cp ./mk-syl/*.clean .
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ ls
dev.en  dev.syl.clean  mk-syl  original  test.en  test.syl.clean  train.en  train.syl.clean
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ mv train.syl.clean train.my
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ mv dev.syl.clean dev.my
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ mv test.syl.clean test.my
```

confirm no of lines for both English and Myanmar side:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ wc *.en
    741   13293   66834 dev.en
   1504   30578  153883 test.en
  21497  430740 2160265 train.en
  23742  474611 2380982 total
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ wc *.my
    741   23984  215084 dev.my
   1504   54506  486569 test.my
  21497  775603 6983957 train.my
  23742  854093 7685610 total
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$
```

learning what is experiment-ID:  

```bash
#!/bin/bash

PARENT_EXPID=$1 # 'pt-en'
EXPID=$2        # 'gl-en_progadapt'
DEVICES=$3      # -1 for cpu
```

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ time bash ./scripts/build-training-data.sh 'ja-en ko-en' flag sov-1
bash: /home/ye/anaconda3/envs/xnmt/lib/libtinfo.so.6: no version information available (required by bash)
~/tool/adapt-mnmt/models/sov-1/data ~/tool/adapt-mnmt
DSTDIR: /home/ye/tool/adapt-mnmt/models/sov-1/data
DATADIR: /home/ye/tool/adapt-mnmt/data/ted-data
BUILDING: ja>en
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-train.orig.ja: No such file or directory
Warning: No built-in rules for language ja.
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-train.orig.ja: No such file or directory
Warning: No built-in rules for language ja.
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-dev.orig.ja: No such file or directory
Warning: No built-in rules for language ja.
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-dev.orig.ja: No such file or directory
Warning: No built-in rules for language ja.
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-test.orig.ja: No such file or directory
Warning: No built-in rules for language ja.
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-test.orig.ja: No such file or directory
Warning: No built-in rules for language ja.
./scripts/build-training-data.sh: line 79: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-test.orig.ja: No such file or directory
Warning: No built-in rules for language ja.
./scripts/build-training-data.sh: line 83: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-test.orig.en: No such file or directory
BUILDING: ko>en
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-train.orig.ko: No such file or directory
Warning: No built-in rules for language ko.
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-train.orig.ko: No such file or directory
Warning: No built-in rules for language ko.
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-dev.orig.ko: No such file or directory
Warning: No built-in rules for language ko.
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-dev.orig.ko: No such file or directory
Warning: No built-in rules for language ko.
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-test.orig.ko: No such file or directory
Warning: No built-in rules for language ko.
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-test.orig.ko: No such file or directory
Warning: No built-in rules for language ko.
./scripts/build-training-data.sh: line 79: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-test.orig.ko: No such file or directory
Warning: No built-in rules for language ko.
~/tool/adapt-mnmt
Done: /home/ye/tool/adapt-mnmt/models/sov-1/data
      0 /home/ye/tool/adapt-mnmt/models/sov-1/data/dev.src
      0 /home/ye/tool/adapt-mnmt/models/sov-1/data/dev.tgt
wc: /home/ye/tool/adapt-mnmt/models/sov-1/data/test-sets: Is a directory
      0 /home/ye/tool/adapt-mnmt/models/sov-1/data/test-sets
      0 /home/ye/tool/adapt-mnmt/models/sov-1/data/test.src
      0 /home/ye/tool/adapt-mnmt/models/sov-1/data/test.tgt
      0 /home/ye/tool/adapt-mnmt/models/sov-1/data/train.src
      0 /home/ye/tool/adapt-mnmt/models/sov-1/data/train.tgt
      0 total

real    0m0.077s
user    0m0.105s
sys     0m0.030s
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models$ tree
.
└── sov-1
    └── data
        ├── dev.src
        ├── dev.tgt
        ├── test-sets
        │   ├── test.en
        │   ├── test.ja
        │   └── test.ko
        ├── test.src
        ├── test.tgt
        ├── train.src
        └── train.tgt

3 directories, 9 files
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models$
```

got ERROR ...  
```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ time bash ./scripts/preprocess.sh sov-1 30000
bash: /home/ye/anaconda3/envs/xnmt/lib/libtinfo.so.6: no version information available (required by bash)

LEARNING SP MODEL ...
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 93, in <module>
    main()
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 69, in main
    train(args.spm_dir, args.in_file, args.src, args.tgt, args.spm_size)
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 18, in train
    spm_train(file_src, spm_src, spm_size)
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 7, in spm_train
    spm.SentencePieceTrainer.Train('--input={} --model_prefix={} --vocab_size={} '
AttributeError: module 'sentencepiece' has no attribute 'SentencePieceTrainer'
SP MODEL: [/home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel]

APPLYING SP MODEL ON [train] ...
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 93, in <module>
    main()
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 77, in main
    encode(args.spm_dir, args.in_file, args.src, args.op_file)
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 27, in encode
    spm_spp = spm.SentencePieceProcessor()
AttributeError: module 'sentencepiece' has no attribute 'SentencePieceProcessor'

APPLYING SP MODEL ON [dev] ...
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 93, in <module>
    main()
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 77, in main
    encode(args.spm_dir, args.in_file, args.src, args.op_file)
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 27, in encode
    spm_spp = spm.SentencePieceProcessor()
AttributeError: module 'sentencepiece' has no attribute 'SentencePieceProcessor'

APPLYING SP MODEL ON [test] ...
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 93, in <module>
    main()
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 77, in main
    encode(args.spm_dir, args.in_file, args.src, args.op_file)
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 27, in encode
    spm_spp = spm.SentencePieceProcessor()
AttributeError: module 'sentencepiece' has no attribute 'SentencePieceProcessor'
SP DATA: [ /home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel ]

real    0m0.088s
user    0m0.069s
sys     0m0.019s
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

The above error is caused by the version conflict of SentencePiece. And thus ... uninstall and install updated SentencePiece as follows:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~$ pip uninstall sentencepiece
Found existing installation: sentencepiece 0.1.8
Uninstalling sentencepiece-0.1.8:
  Would remove:
    /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/_sentencepiece.cpython-36m-x86_64-linux-gnu.so
    /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/sentencepiece-0.1.8.dist-info/*
    /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/sentencepiece.py
Proceed (Y/n)? Y
  Successfully uninstalled sentencepiece-0.1.8
(adapt-mnmt) ye@ye-System-Product-Name:~$ pip install sentencepiece
Collecting sentencepiece
  Using cached sentencepiece-0.1.96-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.2 MB)
Installing collected packages: sentencepiece
Successfully installed sentencepiece-0.1.96
(adapt-mnmt) ye@ye-System-Product-Name:~$
```

Then retry ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ time bash ./scripts/preprocess.sh sov-1 50000
bash: /home/ye/anaconda3/envs/xnmt/lib/libtinfo.so.6: no version information available (required by bash)

real    0m0.001s
user    0m0.001s
sys     0m0.000s
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

No error message and thus it looks OK and let me confirm by seeing some files ...  
I am not sure working well or not ... I just noticed that "spdata" and "spmodel" folders are built.  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models$ tree
.
└── sov-1
    └── data
        ├── dev.src
        ├── dev.tgt
        ├── spdata
        ├── spmodel
        ├── test-sets
        │   ├── test.en
        │   ├── test.ja
        │   └── test.ko
        ├── test.src
        ├── test.tgt
        ├── train.src
        └── train.tgt

5 directories, 9 files
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models$
```

When I checked the filesize, it looks not OK ... :(   

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data$ ls
dev.src  dev.tgt  spdata  spmodel  test-sets  test.src  test.tgt  train.src  train.tgt
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data$ head *.src
==> dev.src <==

==> test.src <==

==> train.src <==
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data$ head *.tgt
==> dev.tgt <==

==> test.tgt <==

==> train.tgt <==
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data$ wc *.src
0 0 0 dev.src
0 0 0 test.src
0 0 0 train.src
0 0 0 total
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data$ wc *.tgt
0 0 0 dev.tgt
0 0 0 test.tgt
0 0 0 train.tgt
0 0 0 total
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data$ cd test-sets/
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data/test-sets$ wc *
0 0 0 test.en
0 0 0 test.ja
0 0 0 test.ko
0 0 0 total
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data/test-sets$
```

## Trying to Fix the Error

```./scripts/build-training-data.sh ['src1-en en-src1 src2-en en-src2'] [flag] [exp-id]```

I found that I run the command for "build-training-data.sh" not exactly the same as example given (see above) and I haven't put for the reverse translation directions ... 
I run as follows:  

```
time bash ./scripts/build-training-data.sh 'ja-en ko-en' flag sov-1
```

And thus, I rerun as follows:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models$ rm -rf ./sov-1/
time bash ./scripts/build-training-data.sh 'ja-en en-ja ko-en en-ko' flag sov-1
```

Running log as follows:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ time bash ./scripts/build-training-data.sh 'ja-en en-ja ko-en en-ko' flag sov-1
bash: /home/ye/anaconda3/envs/xnmt/lib/libtinfo.so.6: no version information available (required by bash)
~/tool/adapt-mnmt/models/sov-1/data ~/tool/adapt-mnmt
DSTDIR: /home/ye/tool/adapt-mnmt/models/sov-1/data
DATADIR: /home/ye/tool/adapt-mnmt/data/ted-data
BUILDING: ja>en
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-train.orig.ja: No such file or directory
Warning: No built-in rules for language ja.
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-train.orig.ja: No such file or directory
Warning: No built-in rules for language ja.
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-dev.orig.ja: No such file or directory
Warning: No built-in rules for language ja.
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-dev.orig.ja: No such file or directory
Warning: No built-in rules for language ja.
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-test.orig.ja: No such file or directory
Warning: No built-in rules for language ja.
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-test.orig.ja: No such file or directory
Warning: No built-in rules for language ja.
./scripts/build-training-data.sh: line 79: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-test.orig.ja: No such file or directory
Warning: No built-in rules for language ja.
./scripts/build-training-data.sh: line 83: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-test.orig.en: No such file or directory
BUILDING: en>ja
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-train.orig.en: No such file or directory
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-train.orig.en: No such file or directory
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-dev.orig.en: No such file or directory
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-dev.orig.en: No such file or directory
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-test.orig.en: No such file or directory
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ja_en/ted-test.orig.en: No such file or directory
BUILDING: ko>en
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-train.orig.ko: No such file or directory
Warning: No built-in rules for language ko.
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-train.orig.ko: No such file or directory
Warning: No built-in rules for language ko.
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-dev.orig.ko: No such file or directory
Warning: No built-in rules for language ko.
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-dev.orig.ko: No such file or directory
Warning: No built-in rules for language ko.
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-test.orig.ko: No such file or directory
Warning: No built-in rules for language ko.
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-test.orig.ko: No such file or directory
Warning: No built-in rules for language ko.
./scripts/build-training-data.sh: line 79: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-test.orig.ko: No such file or directory
Warning: No built-in rules for language ko.
BUILDING: en>ko
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-train.orig.en: No such file or directory
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-train.orig.en: No such file or directory
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-dev.orig.en: No such file or directory
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-dev.orig.en: No such file or directory
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-test.orig.en: No such file or directory
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-test.orig.en: No such file or directory
~/tool/adapt-mnmt
Done: /home/ye/tool/adapt-mnmt/models/sov-1/data
      0 /home/ye/tool/adapt-mnmt/models/sov-1/data/dev.src
      0 /home/ye/tool/adapt-mnmt/models/sov-1/data/dev.tgt
wc: /home/ye/tool/adapt-mnmt/models/sov-1/data/test-sets: Is a directory
      0 /home/ye/tool/adapt-mnmt/models/sov-1/data/test-sets
      0 /home/ye/tool/adapt-mnmt/models/sov-1/data/test.src
      0 /home/ye/tool/adapt-mnmt/models/sov-1/data/test.tgt
      0 /home/ye/tool/adapt-mnmt/models/sov-1/data/train.src
      0 /home/ye/tool/adapt-mnmt/models/sov-1/data/train.tgt
      0 total

real    0m0.134s
user    0m0.175s
sys     0m0.064s
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

filesize for both src and tgt files are ZERO. I think there is a problem ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data$ wc *.src
0 0 0 dev.src
0 0 0 test.src
0 0 0 train.src
0 0 0 total
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data$ wc *.tgt
0 0 0 dev.tgt
0 0 0 test.tgt
0 0 0 train.tgt
0 0 0 total
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data$
```

TED-data filename changes?!   
See following messages:  

```
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-train.orig.en: No such file or directory
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-train.orig.en: No such file or directory
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-dev.orig.en: No such file or directory
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-dev.orig.en: No such file or directory
./scripts/build-training-data.sh: line 66: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-test.orig.en: No such file or directory
./scripts/build-training-data.sh: line 68: /home/ye/tool/adapt-mnmt/data/ted-data/ko_en/ted-test.orig.en: No such file or directory
```

I changed the filenames ...  :  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ko_en$ mv train.en ted-train.orig.en
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ko_en$ mv dev.en ted-dev.orig.en
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ko_en$ mv test.en ted-test.orig.en
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ko_en$
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ko_en$ mv train.ko ted-train.orig.ko
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ko_en$ mv dev.ko ted-dev.orig.ko
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ko_en$ mv test.ko ted-test.orig.ko
```

changed for Japanese-English parallel corpus also ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ja_en$ mv dev.en ted-dev.orig.en
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ja_en$ mv train.en ted-train.orig.en
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ja_en$ mv test.en ted-test.orig.en
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ja_en$
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ja_en$ mv dev.ja ted-dev.orig.ja
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ja_en$ mv train.ja ted-train.orig.ja
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/ja_en$ mv test.ja ted-test.orig.ja
```

Filename changes for Myanmar-English also ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ ls
dev.en  dev.my  mk-syl  original  test.en  test.my  train.en  train.my
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ mkdir bk
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ cp *.en ./bk
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ cp *.my ./bk
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ mv dev.en ted-dev.orig.en
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ mv test.en ted-test.orig.en
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ mv train.en ted-train.orig.en
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ mv dev.my ted-dev.orig.my
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ mv test.my ted-test.orig.my
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/data/ted-data/my_en$ mv train.my ted-train.orig.my
```

re-run the script "build-training-data.sh" :  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ time bash ./scripts/build-training-data.sh 'ja-en en-ja ko-en en-ko' flag sov
-1
bash: /home/ye/anaconda3/envs/xnmt/lib/libtinfo.so.6: no version information available (required by bash)
~/tool/adapt-mnmt/models/sov-1/data ~/tool/adapt-mnmt
DSTDIR: /home/ye/tool/adapt-mnmt/models/sov-1/data
DATADIR: /home/ye/tool/adapt-mnmt/data/ted-data
BUILDING: ja>en
Warning: No built-in rules for language ja.
Warning: No built-in rules for language ja.
Warning: No built-in rules for language ja.
Warning: No built-in rules for language ja.
Warning: No built-in rules for language ja.
Warning: No built-in rules for language ja.
Warning: No built-in rules for language ja.
BUILDING: en>ja
BUILDING: ko>en
Warning: No built-in rules for language ko.
Warning: No built-in rules for language ko.
Warning: No built-in rules for language ko.
Warning: No built-in rules for language ko.
Warning: No built-in rules for language ko.
Warning: No built-in rules for language ko.
Warning: No built-in rules for language ko.
BUILDING: en>ko
~/tool/adapt-mnmt
Done: /home/ye/tool/adapt-mnmt/models/sov-1/data
    17740 /home/ye/tool/adapt-mnmt/models/sov-1/data/dev.src
    17740 /home/ye/tool/adapt-mnmt/models/sov-1/data/dev.tgt
wc: /home/ye/tool/adapt-mnmt/models/sov-1/data/test-sets: Is a directory
        0 /home/ye/tool/adapt-mnmt/models/sov-1/data/test-sets
    22404 /home/ye/tool/adapt-mnmt/models/sov-1/data/test.src
    22404 /home/ye/tool/adapt-mnmt/models/sov-1/data/test.tgt
   819460 /home/ye/tool/adapt-mnmt/models/sov-1/data/train.src
   819460 /home/ye/tool/adapt-mnmt/models/sov-1/data/train.tgt
  1719208 total

real    1m41.567s
user    2m3.998s
sys     0m1.161s
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

As shown as above, for this time, it looks working ... :)  
Check the files:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1$ tree
.
└── data
    ├── dev.src
    ├── dev.tgt
    ├── test-sets
    │   ├── test.en
    │   ├── test.ja
    │   └── test.ko
    ├── test.src
    ├── test.tgt
    ├── train.src
    └── train.tgt

2 directories, 9 files
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1$ wc ./data/*.src
   17740   231315  1962874 ./data/dev.src
   22404   285295  2426802 ./data/test.src
  819460 10941469 93754627 ./data/train.src
  859604 11458079 98144303 total
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1$ wc ./data/*.tgt
   17740   213575  1856434 ./data/dev.tgt
   22404   262891  2292378 ./data/test.tgt
  819460 10122009 88837867 ./data/train.tgt
  859604 10598475 92986679 total
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1$ wc ./data/test-sets/*
   5565   93624  516341 ./data/test-sets/test.en
   5565    8511  589015 ./data/test-sets/test.ja
   5637   66301  666237 ./data/test-sets/test.ko
  16767  168436 1771593 total
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1$
```

I feel a little bit wired and check the contents ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data$ head -n 3 *.src
==> dev.src <==
<2en> 私が11才の時のことですある朝家中に湧き上がった歓声に目を覚ましました
<2en> 父はグレーの小型ラジオで BBCニュースを聞いていました
<2en> そして珍しく満面の笑みを浮かべていました普段は暗いニュースに落ち込んでばかりいましたから

==> test.src <==
<2en> 今年の終わりには世界中で 10億人近くがソーシャルネットワークのサイトを活発に使っているでしょう
<2en> １つ全員に共通して言えるのは皆いずれ死ぬということです
<2en> なんとなく陰気な考えである一方これには検討に値する実に深い意味があると思います

==> train.src <==
<2en> 我々が今日直面している様々な機能不全のなかで - 財政や経済が最初に思いつきますが - 私が一番憂慮しているのは政治的対話の欠乏です我 々が近年の紛争において状況を把握しその根本原因を探り中心人物を理解し彼らと交渉をする能力です
<2en> 我々外交官は国家間の紛争や問題に対処するよう訓練されています
<2en> 貿易や軍縮の国境を越えた問題などに対処しなければなりません
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data$ head -n 3 *.tgt
==> dev.tgt <==
私が11才の時のことですある朝家中に湧き上がった歓声に目を覚ましました
父はグレーの小型ラジオで BBCニュースを聞いていました
そして珍しく満面の笑みを浮かべていました普段は暗いニュースに落ち込んでばかりいましたから

==> test.tgt <==
今年の終わりには世界中で 10億人近くがソーシャルネットワークのサイトを活発に使っているでしょう
１つ全員に共通して言えるのは皆いずれ死ぬということです
なんとなく陰気な考えである一方これには検討に値する実に深い意味があると思います

==> train.tgt <==
我々が今日直面している様々な機能不全のなかで - 財政や経済が最初に思いつきますが - 私が一番憂慮しているのは政治的対話の欠乏です我々が近 年の紛争において状況を把握しその根本原因を探り中心人物を理解し彼らと交渉をする能力です
我々外交官は国家間の紛争や問題に対処するよう訓練されています
貿易や軍縮の国境を越えた問題などに対処しなければなりません
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data$
```

When I checked with tail command, I found English text as follows:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data$ tail -n 3 *.src
==> dev.src <==
<2ko> For you, it's your call.
<2ko> Thank you.
<2ko> (Applause)

==> test.src <==
<2ko> And all I could detect was this energy - energy.
<2ko> And I'm asking myself, "" What is wrong with me?
<2ko> And I felt lighter in my body.

==> train.src <==
<2ko> I have my own answer to that question, which comes from a great artist of the 19th century, Anton Chekhov, who said, "" Man will become better when you show him what he is like. "" And I think that the argument can't be put any more eloquently than that.
<2ko> Thank you very much.
<2ko> (Applause)
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data$
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data$ tail -n 3 *.tgt
==> dev.tgt <==
For you, it's your call.
Thank you.
(Applause)

==> test.tgt <==
And all I could detect was this energy - energy.
And I'm asking myself, "" What is wrong with me?
And I felt lighter in my body.

==> train.tgt <==
I have my own answer to that question, which comes from a great artist of the 19th century, Anton Chekhov, who said, "" Man will become better when you show him what he is like. "" And I think that the argument can't be put any more eloquently than that.
Thank you very much.
(Applause)
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data$
```

for the test data ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data/test-sets$ head -n 3 test.{en,ja,ko}
==> test.en <==
By the end of this year, there'll be nearly a billion people on this planet that actively use social networking sites.
The one thing that all of them have in common is that they're going to die.
While that might be a somewhat morbid thought, I think it has some really profound implications that are worth exploring.

==> test.ja <==
今年の終わりには世界中で 10億人近くがソーシャルネットワークのサイトを活発に使っているでしょう
１つ全員に共通して言えるのは皆いずれ死ぬということです
なんとなく陰気な考えである一方これには検討に値する実に深い意味があると思います

==> test.ko <==
올해 말쯤 되면 지구상에 약 10억 명의 사람들이 적극적으로 소셜 네트워킹 사이트를 이용할 것입니다.
이 사람들이 가지고 있는 단 하나의 공통점은 바로 언젠가 모두 다 죽는다는겁니다.
이게 약간 소름끼치는 생각일지도 모르지만 전 이게 연구해 볼 가치가 있는 심오한 뭔가가 있다고 생각합니다.
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data/test-sets$ tail -n 3 test.{en,ja,ko}
==> test.en <==
And all I could detect was this energy - energy.
And I'm asking myself, "" What is wrong with me?
And I felt lighter in my body.

==> test.ja <==
唯一感じ取れるのはエネルギーだけでした
そして自分に問いかけました
体が軽くなったのを感じました

==> test.ko <==
스스로에게 물어보았어요. "" 뭐가 잘못된 거지?
무슨 일이 일어나고 있는 거야? "" 그 순간, 뇌 수다장이가,
외부 세계의 모든 관계와 그 외부 세계에 관련된
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data/test-sets$
```

Let's go ahead for preprocess script running ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ time bash ./scripts/preprocess.sh sov-1 50000
bash: /home/ye/anaconda3/envs/xnmt/lib/libtinfo.so.6: no version information available (required by bash)

LEARNING SP MODEL ...
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 93, in <module>
    main()
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 69, in main
    train(args.spm_dir, args.in_file, args.src, args.tgt, args.spm_size)
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 18, in train
    spm_train(file_src, spm_src, spm_size)
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 7, in spm_train
    spm.SentencePieceTrainer.Train('--input={} --model_prefix={} --vocab_size={} '
AttributeError: module 'sentencepiece' has no attribute 'SentencePieceTrainer'
SP MODEL: [/home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel]

APPLYING SP MODEL ON [train] ...
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 93, in <module>
    main()
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 77, in main
    encode(args.spm_dir, args.in_file, args.src, args.op_file)
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 27, in encode
    spm_spp = spm.SentencePieceProcessor()
AttributeError: module 'sentencepiece' has no attribute 'SentencePieceProcessor'

APPLYING SP MODEL ON [dev] ...
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 93, in <module>
    main()
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 77, in main
    encode(args.spm_dir, args.in_file, args.src, args.op_file)
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 27, in encode
    spm_spp = spm.SentencePieceProcessor()
AttributeError: module 'sentencepiece' has no attribute 'SentencePieceProcessor'

APPLYING SP MODEL ON [test] ...
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 93, in <module>
    main()
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 77, in main
    encode(args.spm_dir, args.in_file, args.src, args.op_file)
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 27, in encode
    spm_spp = spm.SentencePieceProcessor()
AttributeError: module 'sentencepiece' has no attribute 'SentencePieceProcessor'
SP DATA: [ /home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel ]

real    0m0.088s
user    0m0.081s
sys     0m0.007s
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

I still got an error as above ...  
I tried uninstall current version of sentencepiece and then install the same version that adapt-mnmt used it ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ pip uninstall sentencepiece
Found existing installation: sentencepiece 0.1.96
Uninstalling sentencepiece-0.1.96:
  Would remove:
    /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/sentencepiece-0.1.96.dist-info/*
    /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/sentencepiece/*
Proceed (Y/n)? Y
  Successfully uninstalled sentencepiece-0.1.96
```

install 0.1.8 version as follows:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ pip install sentencepiece==0.1.8
Collecting sentencepiece==0.1.8
  Using cached sentencepiece-0.1.8-cp36-cp36m-manylinux1_x86_64.whl (1.0 MB)
Installing collected packages: sentencepiece
Successfully installed sentencepiece-0.1.8
```

run again and no error message however I am still doubt ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ time bash ./scripts/preprocess.sh sov-1 50000
bash: /home/ye/anaconda3/envs/xnmt/lib/libtinfo.so.6: no version information available (required by bash)

real    0m0.001s
user    0m0.001s
sys     0m0.000s
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ cd models/sov-1/
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1$ tree
.
└── data
    ├── dev.src
    ├── dev.tgt
    ├── spdata
    ├── spmodel
    ├── test-sets
    │   ├── test.en
    │   ├── test.ja
    │   └── test.ko
    ├── test.src
    ├── test.tgt
    ├── train.src
    └── train.tgt

4 directories, 9 files
```

spdata meaning might be sentencepiece-data and currently still a blank folder ...  ?! ?!   

libtinfo.so.6 error message as follows is caused by adding anaconda library path to ```LD_LIBRARY_PATH```:  
```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/OpenNMT/opennmt/bin$ vi build_vocab.py
vi: /home/ye/anaconda3/envs/xnmt/lib/libtinfo.so.6: no version information available (required by vi)
```

I removed anaconda library path of .bashrc as follows:  

```
#export LD_LIBRARY_PATH="/home/ye/anaconda3/envs/xnmt/lib/:/usr/local/cuda-11.6/lib64:$LD_LIBRARY_PATH"
export LD_LIBRARY_PATH="/usr/local/cuda-11.6/lib64:$LD_LIBRARY_PATH"
```

deactivate conda env, source /home/ye/.bashrc and then activate conda env and now that libtinfo.so.6 error already solved! :)  
Refer SentencePiece GitHub and install required libraries ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ sudo apt-get install cmake build-essential pkg-config libgoogle-perftools-dev
[sudo] password for ye:
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
build-essential is already the newest version (12.9ubuntu3).
cmake is already the newest version (3.22.1-1ubuntu1).
pkg-config is already the newest version (0.29.2-1ubuntu3).
The following NEW packages will be installed:
  libgoogle-perftools-dev libgoogle-perftools4 libtcmalloc-minimal4 libunwind-dev
0 upgraded, 4 newly installed, 0 to remove and 32 not upgraded.
Need to get 2,662 kB of archives.
After this operation, 11.3 MB of additional disk space will be used.
Get:1 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libtcmalloc-minimal4 amd64 2.9.1-0ubuntu3 [98.2 kB]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libgoogle-perftools4 amd64 2.9.1-0ubuntu3 [212 kB]
Get:3 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libunwind-dev amd64 1.3.2-2build2 [1,882 kB]
Get:4 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libgoogle-perftools-dev amd64 2.9.1-0ubuntu3 [470 kB]
Fetched 2,662 kB in 1s (5,110 kB/s)
Selecting previously unselected package libtcmalloc-minimal4:amd64.
(Reading database ... 230404 files and directories currently installed.)
Preparing to unpack .../libtcmalloc-minimal4_2.9.1-0ubuntu3_amd64.deb ...
Unpacking libtcmalloc-minimal4:amd64 (2.9.1-0ubuntu3) ...
Selecting previously unselected package libgoogle-perftools4:amd64.
Preparing to unpack .../libgoogle-perftools4_2.9.1-0ubuntu3_amd64.deb ...
Unpacking libgoogle-perftools4:amd64 (2.9.1-0ubuntu3) ...
Selecting previously unselected package libunwind-dev:amd64.
Preparing to unpack .../libunwind-dev_1.3.2-2build2_amd64.deb ...
Unpacking libunwind-dev:amd64 (1.3.2-2build2) ...
Selecting previously unselected package libgoogle-perftools-dev:amd64.
Preparing to unpack .../libgoogle-perftools-dev_2.9.1-0ubuntu3_amd64.deb ...
Unpacking libgoogle-perftools-dev:amd64 (2.9.1-0ubuntu3) ...
Setting up libunwind-dev:amd64 (1.3.2-2build2) ...
Setting up libtcmalloc-minimal4:amd64 (2.9.1-0ubuntu3) ...
Setting up libgoogle-perftools4:amd64 (2.9.1-0ubuntu3) ...
Setting up libgoogle-perftools-dev:amd64 (2.9.1-0ubuntu3) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

## Installation of SentencePiece

uninstall current sentencepiece ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool$ pip uninstall sentencepiece
Found existing installation: sentencepiece 0.1.8
Uninstalling sentencepiece-0.1.8:
  Would remove:
    /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/_sentencepiece.cpython-36m-x86_64-linux-gnu.so
    /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/sentencepiece-0.1.8.dist-info/*
    /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/sentencepiece.py
Proceed (Y/n)? Y
  Successfully uninstalled sentencepiece-0.1.8
```

git clone the updated sentencepiece ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool$ git clone https://github.com/google/sentencepiece.git
Cloning into 'sentencepiece'...
remote: Enumerating objects: 3870, done.
remote: Counting objects: 100% (179/179), done.
remote: Compressing objects: 100% (107/107), done.
remote: Total 3870 (delta 83), reused 133 (delta 71), pack-reused 3691
Receiving objects: 100% (3870/3870), 32.18 MiB | 10.65 MiB/s, done.
Resolving deltas: 100% (2675/2675), done.
```

Got error when I tried to compile ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool$ cd sentencepiece/
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece$ mkdir build
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece$ cd build
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ cmake ..
cmake: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by cmake)
cmake: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by /lib/x86_64-linux-gnu/libjsoncpp.so.25)
```

install libstdc++6 ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ sudo apt-get install libstdc++6
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
libstdc++6 is already the newest version (12-20220319-1ubuntu1).
0 upgraded, 0 newly installed, 0 to remove and 32 not upgraded.
```

I did the followings:  

```
sudo add-apt-repository ppa:ubuntu-toolchain-r/test 
sudo apt-get update
sudo apt-get upgrade
```

cmake again ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ cmake ..
cmake: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by cmake)
cmake: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by /lib/x86_64-linux-gnu/libjsoncpp.so.25)
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$
```

run ```sudo apt-get dist-upgrade``` also ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ sudo apt-get dist-upgrade
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Calculating upgrade... Done
The following NEW packages will be installed:
  linux-headers-5.15.0-30 linux-headers-5.15.0-30-generic linux-image-5.15.0-30-generic linux-modules-5.15.0-30-generic
  linux-modules-extra-5.15.0-30-generic
The following packages will be upgraded:
  linux-generic-hwe-22.04 linux-headers-generic-hwe-22.04 linux-image-generic-hwe-22.04
3 upgraded, 5 newly installed, 0 to remove and 0 not upgraded.
Need to get 110 MB of archives.
After this operation, 558 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-modules-5.15.0-30-generic amd64 5.15.0-30.31 [21.9 MB]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-image-5.15.0-30-generic amd64 5.15.0-30.31 [10.9 MB]
Get:3 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-modules-extra-5.15.0-30-generic amd64 5.15.0-30.31 [61.8 MB]
Get:4 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-generic-hwe-22.04 amd64 5.15.0.30.33 [1,670 B]
Get:5 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-image-generic-hwe-22.04 amd64 5.15.0.30.33 [2,476 B]
Get:6 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-headers-5.15.0-30 all 5.15.0-30.31 [12.3 MB]
Get:7 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-headers-5.15.0-30-generic amd64 5.15.0-30.31 [2,825 kB]
Get:8 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-headers-generic-hwe-22.04 amd64 5.15.0.30.33 [2,366 B]
Fetched 110 MB in 2s (45.4 MB/s)
Selecting previously unselected package linux-modules-5.15.0-30-generic.
(Reading database ... 230597 files and directories currently installed.)
Preparing to unpack .../0-linux-modules-5.15.0-30-generic_5.15.0-30.31_amd64.deb ...
Unpacking linux-modules-5.15.0-30-generic (5.15.0-30.31) ...
Selecting previously unselected package linux-image-5.15.0-30-generic.
Preparing to unpack .../1-linux-image-5.15.0-30-generic_5.15.0-30.31_amd64.deb ...
Unpacking linux-image-5.15.0-30-generic (5.15.0-30.31) ...
Selecting previously unselected package linux-modules-extra-5.15.0-30-generic.
Preparing to unpack .../2-linux-modules-extra-5.15.0-30-generic_5.15.0-30.31_amd64.deb ...
Unpacking linux-modules-extra-5.15.0-30-generic (5.15.0-30.31) ...
Preparing to unpack .../3-linux-generic-hwe-22.04_5.15.0.30.33_amd64.deb ...
Unpacking linux-generic-hwe-22.04 (5.15.0.30.33) over (5.15.0.27.30) ...
Preparing to unpack .../4-linux-image-generic-hwe-22.04_5.15.0.30.33_amd64.deb ...
Unpacking linux-image-generic-hwe-22.04 (5.15.0.30.33) over (5.15.0.27.30) ...
Selecting previously unselected package linux-headers-5.15.0-30.
Preparing to unpack .../5-linux-headers-5.15.0-30_5.15.0-30.31_all.deb ...
Unpacking linux-headers-5.15.0-30 (5.15.0-30.31) ...
Selecting previously unselected package linux-headers-5.15.0-30-generic.
Preparing to unpack .../6-linux-headers-5.15.0-30-generic_5.15.0-30.31_amd64.deb ...
Unpacking linux-headers-5.15.0-30-generic (5.15.0-30.31) ...
Preparing to unpack .../7-linux-headers-generic-hwe-22.04_5.15.0.30.33_amd64.deb ...
Unpacking linux-headers-generic-hwe-22.04 (5.15.0.30.33) over (5.15.0.27.30) ...
Setting up linux-headers-5.15.0-30 (5.15.0-30.31) ...
Setting up linux-headers-5.15.0-30-generic (5.15.0-30.31) ...
Setting up linux-headers-generic-hwe-22.04 (5.15.0.30.33) ...
Setting up linux-modules-5.15.0-30-generic (5.15.0-30.31) ...
Setting up linux-image-5.15.0-30-generic (5.15.0-30.31) ...
I: /boot/vmlinuz.old is now a symlink to vmlinuz-5.15.0-27-generic
I: /boot/initrd.img.old is now a symlink to initrd.img-5.15.0-27-generic
I: /boot/vmlinuz is now a symlink to vmlinuz-5.15.0-30-generic
I: /boot/initrd.img is now a symlink to initrd.img-5.15.0-30-generic
Setting up linux-modules-extra-5.15.0-30-generic (5.15.0-30.31) ...
Setting up linux-image-generic-hwe-22.04 (5.15.0.30.33) ...
Setting up linux-generic-hwe-22.04 (5.15.0.30.33) ...
Processing triggers for linux-image-5.15.0-30-generic (5.15.0-30.31) ...
/etc/kernel/postinst.d/initramfs-tools:
update-initramfs: Generating /boot/initrd.img-5.15.0-30-generic
/etc/kernel/postinst.d/zz-update-grub:
Sourcing file `/etc/default/grub'
Sourcing file `/etc/default/grub.d/init-select.cfg'
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-5.15.0-30-generic
Found initrd image: /boot/initrd.img-5.15.0-30-generic
Found linux image: /boot/vmlinuz-5.15.0-27-generic
Found initrd image: /boot/initrd.img-5.15.0-27-generic
Found linux image: /boot/vmlinuz-5.15.0-25-generic
Found initrd image: /boot/initrd.img-5.15.0-25-generic
Memtest86+ needs a 16-bit boot, that is not available on EFI, exiting
Warning: os-prober will not be executed to detect other bootable partitions.
Systems on them will not be added to the GRUB boot configuration.
Check GRUB_DISABLE_OS_PROBER documentation entry.
Adding boot menu entry for UEFI Firmware Settings ...
done
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$
```

cmake again and still got error as follows:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ cmake ..
cmake: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by cmake)
cmake: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by /lib/x86_64-linux-gnu/libjsoncpp.so.25)
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$
```

libgcc installation with conda ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ conda install libgcc
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/anaconda3/envs/adapt-mnmt

  added / updated specs:
    - libgcc


The following NEW packages will be INSTALLED:

  libgcc             pkgs/main/linux-64::libgcc-7.2.0-h69d50b8_2


Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$
```

cmake again and still got same error ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ cmake ..
cmake: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by cmake)
cmake: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by /lib/x86_64-linux-gnu/libjsoncpp.so.25)
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$
```

change filename of the libstdc library under anaconda3/lib/ and create a new soft link file with /usr/lib/x86_64-linux-gnu/libstdc++.so.6 as follows:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ cd /home/ye/anaconda3/lib
(adapt-mnmt) ye@ye-System-Product-Name:~/anaconda3/lib$ mv -vf libstdc++.so.6
libstdc++.so.6       libstdc++.so.6.0.26
(adapt-mnmt) ye@ye-System-Product-Name:~/anaconda3/lib$ mv -vf libstdc++.so.6
libstdc++.so.6       libstdc++.so.6.0.26
(adapt-mnmt) ye@ye-System-Product-Name:~/anaconda3/lib$ mv -vf libstdc++.so.6 libstdc++.so.6.old
renamed 'libstdc++.so.6' -> 'libstdc++.so.6.old'
(adapt-mnmt) ye@ye-System-Product-Name:~/anaconda3/lib$ ln -s /usr/lib/x86_64-linux-gnu/libstdc++.so.6 ./libstdc++.so.6
```

tried ```cmake ..``` again and still got ERROR ...  :(  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ conda deactivate
(base) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ source /home/ye/.bashrc
(base) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ conda activate adapt-mnmt
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ cmake ..
cmake: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by cmake)
cmake: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by /lib/x86_64-linux-gnu/libjsoncpp.so.25)
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$
```

check ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ strings /usr/lib/x86_64-linux-gnu/libstdc++.so.6 | grep GLIBCXX
GLIBCXX_3.4
GLIBCXX_3.4.1
GLIBCXX_3.4.2
GLIBCXX_3.4.3
GLIBCXX_3.4.4
GLIBCXX_3.4.5
GLIBCXX_3.4.6
GLIBCXX_3.4.7
GLIBCXX_3.4.8
GLIBCXX_3.4.9
GLIBCXX_3.4.10
GLIBCXX_3.4.11
GLIBCXX_3.4.12
GLIBCXX_3.4.13
GLIBCXX_3.4.14
GLIBCXX_3.4.15
GLIBCXX_3.4.16
GLIBCXX_3.4.17
GLIBCXX_3.4.18
GLIBCXX_3.4.19
GLIBCXX_3.4.20
GLIBCXX_3.4.21
GLIBCXX_3.4.22
GLIBCXX_3.4.23
GLIBCXX_3.4.24
GLIBCXX_3.4.25
GLIBCXX_3.4.26
GLIBCXX_3.4.27
GLIBCXX_3.4.28
GLIBCXX_3.4.29
GLIBCXX_3.4.30
GLIBCXX_DEBUG_MESSAGE_LENGTH
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$
```

update the link with lib64/xxx    

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ ll /usr/lib64/*
lrwxrwxrwx 1 root root       42 Mar  4 09:54 /usr/lib64/ld-linux-x86-64.so.2 -> /lib/x86_64-linux-gnu/ld-linux-x86-64.so.2*
lrwxrwxrwx 1 root root       21 Apr 30 18:33 /usr/lib64/libstdc++.so.6 -> ./libstdc++.so.6.0.28*
-rwxr-xr-x 1 root root 13121976 Apr 30 18:32 /usr/lib64/libstdc++.so.6.0.28*
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ cd /home/ye/anaconda3/lib/
(adapt-mnmt) ye@ye-System-Product-Name:~/anaconda3/lib$ ln -s /usr/lib64/libstdc++.so.6 ./libstdc++.so.6
ln: failed to create symbolic link './libstdc++.so.6': File exists
(adapt-mnmt) ye@ye-System-Product-Name:~/anaconda3/lib$ mv ./libstdc++.so.6 ./libstdc++.so.6.old-link
(adapt-mnmt) ye@ye-System-Product-Name:~/anaconda3/lib$ ln -s /usr/lib64/libstdc++.so.6 ./libstdc++.so.6
(adapt-mnmt) ye@ye-System-Product-Name:~/anaconda3/lib$ cd -
/home/ye/tool/sentencepiece/build
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ ldconfig
/sbin/ldconfig.real: Can't create temporary cache file /etc/ld.so.cache~: Permission denied
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ sudo ldconfig
[sudo] password for ye:
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ cmake ..
cmake: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by cmake)
cmake: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by /lib/x86_64-linux-gnu/libjsoncpp.so.25)
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$
```

```
(base) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ cmake ..
cmake: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by cmake)
cmake: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by /lib/x86_64-linux-gnu/libjsoncpp.so.25)
(base) ye@ye-System-Product-Name:~/tool/sentencepiece/build$
```

Not working yet ... ?! ?! ...  

```
(base) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ strings /usr/lib/x86_64-linux-gnu/libstdc++.so.6 | grep GLIBCXX
GLIBCXX_3.4
GLIBCXX_3.4.1
GLIBCXX_3.4.2
GLIBCXX_3.4.3
GLIBCXX_3.4.4
GLIBCXX_3.4.5
GLIBCXX_3.4.6
GLIBCXX_3.4.7
GLIBCXX_3.4.8
GLIBCXX_3.4.9
GLIBCXX_3.4.10
GLIBCXX_3.4.11
GLIBCXX_3.4.12
GLIBCXX_3.4.13
GLIBCXX_3.4.14
GLIBCXX_3.4.15
GLIBCXX_3.4.16
GLIBCXX_3.4.17
GLIBCXX_3.4.18
GLIBCXX_3.4.19
GLIBCXX_3.4.20
GLIBCXX_3.4.21
GLIBCXX_3.4.22
GLIBCXX_3.4.23
GLIBCXX_3.4.24
GLIBCXX_3.4.25
GLIBCXX_3.4.26
GLIBCXX_3.4.27
GLIBCXX_3.4.28
GLIBCXX_3.4.29
GLIBCXX_3.4.30
GLIBCXX_DEBUG_MESSAGE_LENGTH
```

I updated the $LD_LIBRARY_PATH path inside /home/ye/.bashrc and run source command ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ echo $LD_LIBRARY_PATH
/usr/lib/x86_64-linux-gnu/:/usr/local/cuda-11.6/lib64:/usr/local/lib:/usr/lib/:/lib:/lib64/
```

Finally, cmake OK ...  :)  

```
(base) ye@ye-System-Product-Name:~/anaconda3/lib$ vi /home/ye/.bashrc
(base) ye@ye-System-Product-Name:~/anaconda3/lib$ sudo ldconfig
(base) ye@ye-System-Product-Name:~/anaconda3/lib$ source /home/ye/.bashrc
(base) ye@ye-System-Product-Name:~/anaconda3/lib$ cd -
/home/ye/tool/sentencepiece/build
(base) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ conda activate adapt-mnmt
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ cmake ..
-- VERSION: 0.1.96
-- The C compiler identification is GNU 11.2.0
-- The CXX compiler identification is GNU 11.2.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Looking for pthread.h
-- Looking for pthread.h - found
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Found TCMalloc: /usr/lib/x86_64-linux-gnu/libtcmalloc_minimal.so
-- Configuring done
-- Generating done
-- Build files have been written to: /home/ye/tool/sentencepiece/build
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$
```

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ make -j 12
[  3%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/builder.cc.o
[  4%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/arena.cc.o
[  3%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/unicode_script.cc.o
[  3%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/trainer_factory.cc.o
[  5%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/trainer_interface.cc.o
[  5%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/arenastring.cc.o
[  5%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/arena.cc.o
[  6%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/unigram_model_trainer.cc.o
[  7%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/word_model_trainer.cc.o
[  8%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/arenastring.cc.o
[  9%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/bytestream.cc.o
[ 10%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/bytestream.cc.o
[ 12%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/coded_stream.cc.o
[ 12%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/coded_stream.cc.o
[ 13%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/extension_set.cc.o
[ 14%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/common.cc.o
[ 15%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/common.cc.o
[ 16%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/extension_set.cc.o
[ 16%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/char_model_trainer.cc.o
[ 17%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/bpe_model_trainer.cc.o
[ 18%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/generated_enum_util.cc.o
[ 19%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/generated_enum_util.cc.o
[ 20%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/generated_message_table_driven_lite.cc.o
[ 21%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/sentencepiece_trainer.cc.o
[ 21%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/generated_message_util.cc.o
[ 21%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/generated_message_table_driven_lite.cc.o
[ 22%] Building CXX object src/CMakeFiles/sentencepiece_train-static.dir/pretokenizer_for_training.cc.o
[ 24%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/implicit_weak_message.cc.o
[ 24%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/generated_message_util.cc.o
[ 25%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/implicit_weak_message.cc.o
[ 26%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/int128.cc.o
[ 27%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/int128.cc.o
[ 28%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/io_win32.cc.o
[ 29%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/message_lite.cc.o
[ 30%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/parse_context.cc.o
[ 31%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/io_win32.cc.o
[ 32%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/message_lite.cc.o
[ 33%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/parse_context.cc.o
[ 34%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/repeated_field.cc.o
[ 34%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/repeated_field.cc.o
[ 35%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/status.cc.o
[ 35%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/statusor.cc.o
[ 36%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/stringpiece.cc.o
[ 37%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/stringprintf.cc.o
[ 38%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/status.cc.o
In file included from /usr/include/string.h:535,
                 from /home/ye/tool/sentencepiece/src/../third_party/protobuf-lite/google/protobuf/stubs/port.h:39,
                 from /home/ye/tool/sentencepiece/src/../third_party/protobuf-lite/google/protobuf/stubs/macros.h:34,
                 from /home/ye/tool/sentencepiece/src/../third_party/protobuf-lite/google/protobuf/stubs/common.h:46,
                 from /home/ye/tool/sentencepiece/src/../third_party/protobuf-lite/google/protobuf/message_lite.h:45,
                 from /home/ye/tool/sentencepiece/third_party/protobuf-lite/message_lite.cc:36:
In function ‘void* memcpy(void*, const void*, size_t)’,
    inlined from ‘google::protobuf::uint8* google::protobuf::io::EpsCopyOutputStream::WriteRaw(const void*, int, google::protobuf::uint8*)’ at /home/ye/tool/sentencepiece/src/../third_party/protobuf-lite/google/protobuf/io/coded_stream.h:699:16,
    inlined from ‘virtual google::protobuf::uint8* google::protobuf::internal::ImplicitWeakMessage::_InternalSerialize(google::protobuf::uint8*, google::protobuf::io::EpsCopyOutputStream*) const’ at /home/ye/tool/sentencepiece/src/../third_party/protobuf-lite/google/protobuf/implicit_weak_message.h:85:28,
    inlined from ‘bool google::protobuf::MessageLite::SerializePartialToZeroCopyStream(google::protobuf::io::ZeroCopyOutputStream*) const’ at /home/ye/tool/sentencepiece/third_party/protobuf-lite/message_lite.cc:419:30:
/usr/include/x86_64-linux-gnu/bits/string_fortified.h:29:33: warning: ‘void* __builtin___memcpy_chk(void*, const void*, long unsigned int, long unsigned int)’ specified size between 18446744071562067968 and 18446744073709551615 exceeds maximum object size 9223372036854775807 [-Wstringop-overflow=]
   29 |   return __builtin___memcpy_chk (__dest, __src, __len,
      |          ~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~~
   30 |                                  __glibc_objsize0 (__dest));
      |                                  ~~~~~~~~~~~~~~~~~~~~~~~~~~
[ 39%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/structurally_valid.cc.o
In file included from /usr/include/string.h:535,
                 from /home/ye/tool/sentencepiece/src/../third_party/protobuf-lite/google/protobuf/stubs/port.h:39,
                 from /home/ye/tool/sentencepiece/src/../third_party/protobuf-lite/google/protobuf/stubs/macros.h:34,
                 from /home/ye/tool/sentencepiece/src/../third_party/protobuf-lite/google/protobuf/stubs/common.h:46,
                 from /home/ye/tool/sentencepiece/src/../third_party/protobuf-lite/google/protobuf/message_lite.h:45,
                 from /home/ye/tool/sentencepiece/third_party/protobuf-lite/message_lite.cc:36:
In function ‘void* memcpy(void*, const void*, size_t)’,
    inlined from ‘google::protobuf::uint8* google::protobuf::io::EpsCopyOutputStream::WriteRaw(const void*, int, google::protobuf::uint8*)’ at /home/ye/tool/sentencepiece/src/../third_party/protobuf-lite/google/protobuf/io/coded_stream.h:699:16,
    inlined from ‘virtual google::protobuf::uint8* google::protobuf::internal::ImplicitWeakMessage::_InternalSerialize(google::protobuf::uint8*, google::protobuf::io::EpsCopyOutputStream*) const’ at /home/ye/tool/sentencepiece/src/../third_party/protobuf-lite/google/protobuf/implicit_weak_message.h:85:28,
    inlined from ‘bool google::protobuf::MessageLite::SerializePartialToZeroCopyStream(google::protobuf::io::ZeroCopyOutputStream*) const’ at /home/ye/tool/sentencepiece/third_party/protobuf-lite/message_lite.cc:419:30:
/usr/include/x86_64-linux-gnu/bits/string_fortified.h:29:33: warning: ‘void* __builtin___memcpy_chk(void*, const void*, long unsigned int, long unsigned int)’ specified size between 18446744071562067968 and 18446744073709551615 exceeds maximum object size 9223372036854775807 [-Wstringop-overflow=]
   29 |   return __builtin___memcpy_chk (__dest, __src, __len,
      |          ~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~~
   30 |                                  __glibc_objsize0 (__dest));
      |                                  ~~~~~~~~~~~~~~~~~~~~~~~~~~
[ 40%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/strutil.cc.o
[ 41%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/time.cc.o
[ 42%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/statusor.cc.o
[ 43%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/stringpiece.cc.o
[ 44%] Linking CXX static library libsentencepiece_train.a
[ 44%] Built target sentencepiece_train-static
[ 45%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/stringprintf.cc.o
[ 46%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/wire_format_lite.cc.o
[ 47%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/structurally_valid.cc.o
[ 48%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/strutil.cc.o
[ 48%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/zero_copy_stream.cc.o
[ 48%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/time.cc.o
[ 49%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/wire_format_lite.cc.o
[ 50%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/zero_copy_stream.cc.o
[ 51%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/zero_copy_stream_impl.cc.o
[ 52%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/zero_copy_stream_impl.cc.o
[ 53%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/protobuf-lite/zero_copy_stream_impl_lite.cc.o
[ 54%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/protobuf-lite/zero_copy_stream_impl_lite.cc.o
[ 55%] Building CXX object src/CMakeFiles/sentencepiece.dir/builtin_pb/sentencepiece.pb.cc.o
[ 56%] Building CXX object src/CMakeFiles/sentencepiece.dir/builtin_pb/sentencepiece_model.pb.cc.o
[ 57%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/builtin_pb/sentencepiece.pb.cc.o
[ 58%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/builtin_pb/sentencepiece_model.pb.cc.o
[ 59%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/bpe_model.cc.o
[ 60%] Building CXX object src/CMakeFiles/sentencepiece.dir/bpe_model.cc.o
[ 61%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/char_model.cc.o
[ 61%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/error.cc.o
[ 61%] Building CXX object src/CMakeFiles/sentencepiece.dir/char_model.cc.o
[ 62%] Building CXX object src/CMakeFiles/sentencepiece.dir/error.cc.o
[ 63%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/filesystem.cc.o
[ 64%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/model_factory.cc.o
[ 65%] Building CXX object src/CMakeFiles/sentencepiece.dir/filesystem.cc.o
[ 66%] Building CXX object src/CMakeFiles/sentencepiece.dir/model_factory.cc.o
[ 67%] Building CXX object src/CMakeFiles/sentencepiece.dir/model_interface.cc.o
[ 68%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/model_interface.cc.o
[ 69%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/normalizer.cc.o
[ 70%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/sentencepiece_processor.cc.o
[ 71%] Building CXX object src/CMakeFiles/sentencepiece.dir/normalizer.cc.o
[ 72%] Building CXX object src/CMakeFiles/sentencepiece.dir/sentencepiece_processor.cc.o
[ 73%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/unigram_model.cc.o
[ 73%] Building CXX object src/CMakeFiles/sentencepiece.dir/unigram_model.cc.o
[ 73%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/util.cc.o
[ 74%] Building CXX object src/CMakeFiles/sentencepiece.dir/util.cc.o
[ 75%] Building CXX object src/CMakeFiles/sentencepiece.dir/word_model.cc.o
[ 76%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/word_model.cc.o
[ 77%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/absl/strings/string_view.cc.o
[ 78%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/absl/strings/string_view.cc.o
[ 79%] Building CXX object src/CMakeFiles/sentencepiece.dir/__/third_party/absl/flags/flag.cc.o
[ 80%] Building CXX object src/CMakeFiles/sentencepiece-static.dir/__/third_party/absl/flags/flag.cc.o
[ 81%] Linking CXX static library libsentencepiece.a
[ 82%] Linking CXX shared library libsentencepiece.so
[ 82%] Built target sentencepiece-static
[ 82%] Built target sentencepiece
[ 86%] Building CXX object src/CMakeFiles/spm_encode.dir/spm_encode_main.cc.o
[ 86%] Building CXX object src/CMakeFiles/spm_decode.dir/spm_decode_main.cc.o
[ 87%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/trainer_factory.cc.o
[ 87%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/builder.cc.o
[ 88%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/unigram_model_trainer.cc.o
[ 88%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/trainer_interface.cc.o
[ 89%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/char_model_trainer.cc.o
[ 86%] Building CXX object src/CMakeFiles/spm_export_vocab.dir/spm_export_vocab_main.cc.o
[ 86%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/unicode_script.cc.o
[ 91%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/bpe_model_trainer.cc.o
[ 91%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/word_model_trainer.cc.o
[ 92%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/sentencepiece_trainer.cc.o
[ 93%] Linking CXX executable spm_export_vocab
[ 93%] Built target spm_export_vocab
[ 94%] Building CXX object src/CMakeFiles/sentencepiece_train.dir/pretokenizer_for_training.cc.o
[ 95%] Linking CXX executable spm_decode
[ 95%] Built target spm_decode
[ 96%] Linking CXX executable spm_encode
[ 96%] Built target spm_encode
[ 96%] Linking CXX shared library libsentencepiece_train.so
[ 96%] Built target sentencepiece_train
[ 98%] Building CXX object src/CMakeFiles/spm_train.dir/spm_train_main.cc.o
[ 98%] Building CXX object src/CMakeFiles/spm_normalize.dir/spm_normalize_main.cc.o
[ 99%] Linking CXX executable spm_normalize
[100%] Linking CXX executable spm_train
[100%] Built target spm_normalize
[100%] Built target spm_train
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$
```

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$ sudo ldconfig -v
/sbin/ldconfig.real: Can't stat /usr/local/lib/x86_64-linux-gnu: No such file or directory
/sbin/ldconfig.real: Path `/usr/lib/x86_64-linux-gnu' given more than once
(from /etc/ld.so.conf.d/x86_64-linux-gnu.conf:4 and /etc/ld.so.conf.d/x86_64-linux-gnu.conf:3)
/sbin/ldconfig.real: Path `/lib/x86_64-linux-gnu' given more than once
(from <builtin>:0 and /etc/ld.so.conf.d/x86_64-linux-gnu.conf:3)
/sbin/ldconfig.real: Path `/usr/lib/x86_64-linux-gnu' given more than once
(from <builtin>:0 and /etc/ld.so.conf.d/x86_64-linux-gnu.conf:3)
/sbin/ldconfig.real: Path `/usr/lib' given more than once
(from <builtin>:0 and <builtin>:0)
/usr/local/cuda-11.6/targets/x86_64-linux/lib: (from /etc/ld.so.conf.d/cuda-11-6.conf:1)
        libcublas.so.11 -> libcublas.so.11.9.2.110
        libnppitc.so.11 -> libnppitc.so.11.6.3.9
        libcusolver.so.11 -> libcusolver.so.11.3.4.124
        libcufftw.so.10 -> libcufftw.so.10.7.2.124
...
...
...
        libGLU.so.1 -> libGLU.so.1.3.1
        libsensors.so.5 -> libsensors.so.5.0.0
        libnetsnmpmibs.so.40 -> libnetsnmpmibs.so.40.1.0
        libgpg-error.so.0 -> libgpg-error.so.0.32.1
        libhyphen.so.0 -> libhyphen.so.0.3.0
        libgexiv2.so.2 -> libgexiv2.so.2.14.0
        libabsl_random_internal_pool_urbg.so.20210324 -> libabsl_random_internal_pool_urbg.so.20210324.0.0
        libabsl_flags_program_name.so.20210324 -> libabsl_flags_program_name.so.20210324.0.0
        libtasn1.so.6 -> libtasn1.so.6.6.2
        libgssdp-1.2.so.0 -> libgssdp-1.2.so.0.104.0
/lib: (from <builtin>:0)
        libBLT.2.5.so.8.6 -> libBLT.2.5.so.8.6
        libBLTlite.2.5.so.8.6 -> libBLTlite.2.5.so.8.6
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/build$
```

test sentencepiece C++ commands ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/python$ spm_
spm_decode        spm_encode        spm_export_vocab  spm_normalize     spm_train
```

called --help for spm_train ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/python$ spm_train --help
sentencepiece

Usage: spm_train [options] files

   --help (show help)  type: bool default: false
   --version (show version)  type: bool default: false
   --minloglevel (Messages logged at a lower level than this don't actually get logged anywhere)  type: int default: 0
   --input (comma separated list of input sentences)  type: std::string default: ""
   --input_format (Input format. Supported format is `text` or `tsv`.)  type: std::string default: ""
   --model_prefix (output model prefix)  type: std::string default: ""
   --model_type (model algorithm: unigram, bpe, word or char)  type: std::string default: "unigram"
   --vocab_size (vocabulary size)  type: int32 default: 8000
   --accept_language (comma-separated list of languages this model can accept)  type: std::string default: ""
   --self_test_sample_size (the size of self test samples)  type: int32 default: 0
   --character_coverage (character coverage to determine the minimum symbols)  type: double default: 0.9995
   --input_sentence_size (maximum size of sentences the trainer loads)  type: std::uint64_t default: 0
   --shuffle_input_sentence (Randomly sample input sentences in advance. Valid when --input_sentence_size > 0)  type: bool default: true
   --seed_sentencepiece_size (the size of seed sentencepieces)  type: int32 default: 1000000
   --shrinking_factor (Keeps top shrinking_factor pieces with respect to the loss)  type: double default: 0.75
   --num_threads (number of threads for training)  type: int32 default: 16
   --num_sub_iterations (number of EM sub-iterations)  type: int32 default: 2
   --max_sentencepiece_length (maximum length of sentence piece)  type: int32 default: 16
   --max_sentence_length (maximum length of sentence in byte)  type: int32 default: 4192
   --split_by_unicode_script (use Unicode script to split sentence pieces)  type: bool default: true
   --split_by_number (split tokens by numbers (0-9))  type: bool default: true
   --split_by_whitespace (use a white space to split sentence pieces)  type: bool default: true
   --split_digits (split all digits (0-9) into separate pieces)  type: bool default: false
   --treat_whitespace_as_suffix (treat whitespace marker as suffix instead of prefix.)  type: bool default: false
   --allow_whitespace_only_pieces (allow pieces that only contain (consecutive) whitespace tokens)  type: bool default: false
   --control_symbols (comma separated list of control symbols)  type: std::string default: ""
   --control_symbols_file (load control_symbols from file.)  type: std::string default: ""
   --user_defined_symbols (comma separated list of user defined symbols)  type: std::string default: ""
   --user_defined_symbols_file (load user_defined_symbols from file.)  type: std::string default: ""
   --required_chars (UTF8 characters in this flag are always used in the character set regardless of --character_coverage)  type: std::string default: ""
   --required_chars_file (load required_chars from file.)  type: std::string default: ""
   --byte_fallback (decompose unknown pieces into UTF-8 byte pieces)  type: bool default: false
   --vocabulary_output_piece_score (Define score in vocab file)  type: bool default: true
   --normalization_rule_name (Normalization rule name. Choose from nfkc or identity)  type: std::string default: "nmt_nfkc"
   --normalization_rule_tsv (Normalization rule TSV file. )  type: std::string default: ""
   --denormalization_rule_tsv (Denormalization rule TSV file.)  type: std::string default: ""
   --add_dummy_prefix (Add dummy whitespace at the beginning of text)  type: bool default: true
   --remove_extra_whitespaces (Removes leading, trailing, and duplicate internal whitespace)  type: bool default: true
   --hard_vocab_limit (If set to false, --vocab_size is considered as a soft limit.)  type: bool default: true
   --use_all_vocab (If set to true, use all tokens as vocab. Valid for word/char models.)  type: bool default: false
   --unk_id (Override UNK (<unk>) id.)  type: int32 default: 0
   --bos_id (Override BOS (<s>) id. Set -1 to disable BOS.)  type: int32 default: 1
   --eos_id (Override EOS (</s>) id. Set -1 to disable EOS.)  type: int32 default: 2
   --pad_id (Override PAD (<pad>) id. Set -1 to disable PAD.)  type: int32 default: -1
   --unk_piece (Override UNK (<unk>) piece.)  type: std::string default: "<unk>"
   --bos_piece (Override BOS (<s>) piece.)  type: std::string default: "<s>"
   --eos_piece (Override EOS (</s>) piece.)  type: std::string default: "</s>"
   --pad_piece (Override PAD (<pad>) piece.)  type: std::string default: "<pad>"
   --unk_surface (Dummy surface string for <unk>. In decoding <unk> is decoded to `unk_surface`.)  type: std::string default: " ⁇ "
   --train_extremely_large_corpus (Increase bit depth for unigram tokenization.)  type: bool default: false
   --random_seed (Seed value for random generator.)  type: uint32 default: 4294967295


(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/python$
```

Run preprocessing script again ...  and still got an error ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ time bash ./scripts/preprocess.sh sov-1 36000

LEARNING SP MODEL ...
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 93, in <module>
    main()
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 69, in main
    train(args.spm_dir, args.in_file, args.src, args.tgt, args.spm_size)
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 18, in train
    spm_train(file_src, spm_src, spm_size)
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 7, in spm_train
    spm.SentencePieceTrainer.Train('--input={} --model_prefix={} --vocab_size={} '
AttributeError: module 'sentencepiece' has no attribute 'SentencePieceTrainer'
SP MODEL: [/home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel]

APPLYING SP MODEL ON [train] ...
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 93, in <module>
    main()
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 77, in main
    encode(args.spm_dir, args.in_file, args.src, args.op_file)
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 27, in encode
    spm_spp = spm.SentencePieceProcessor()
AttributeError: module 'sentencepiece' has no attribute 'SentencePieceProcessor'

APPLYING SP MODEL ON [dev] ...
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 93, in <module>
    main()
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 77, in main
    encode(args.spm_dir, args.in_file, args.src, args.op_file)
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 27, in encode
    spm_spp = spm.SentencePieceProcessor()
AttributeError: module 'sentencepiece' has no attribute 'SentencePieceProcessor'

APPLYING SP MODEL ON [test] ...
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 93, in <module>
    main()
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 77, in main
    encode(args.spm_dir, args.in_file, args.src, args.op_file)
  File "/home/ye/tool/adapt-mnmt/scripts/sentencepiece.py", line 27, in encode
    spm_spp = spm.SentencePieceProcessor()
AttributeError: module 'sentencepiece' has no attribute 'SentencePieceProcessor'
SP DATA: [ /home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel ]

real    0m0.122s
user    0m0.079s
sys     0m0.010s
```

Now, I noticed that sentencepiece didn't say anything, if "spdata" and "spmodel" folders already exist ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ time bash ./scripts/preprocess.sh sov-1 50000

real    0m0.001s
user    0m0.001s
sys     0m0.000s
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

## Install SentencePiece Python Module

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/python$ python ./setup.py build
/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/setuptools/dist.py:720: UserWarning: Usage of dash-separated 'description-file' will not be supported in future versions. Please use the underscore name 'description_file' instead
  % (opt, underscore_opt)
running build
running build_py
creating build
creating build/lib.linux-x86_64-3.6
creating build/lib.linux-x86_64-3.6/sentencepiece
copying src/sentencepiece/__init__.py -> build/lib.linux-x86_64-3.6/sentencepiece
copying src/sentencepiece/sentencepiece_model_pb2.py -> build/lib.linux-x86_64-3.6/sentencepiece
copying src/sentencepiece/sentencepiece_pb2.py -> build/lib.linux-x86_64-3.6/sentencepiece
running build_ext
-L/usr/local/lib -lsentencepiece -lsentencepiece_train
## cflags=-std=c++11 -I/usr/local/include
## libs=-L/usr/local/lib -lsentencepiece -lsentencepiece_train
building 'sentencepiece._sentencepiece' extension
creating build/temp.linux-x86_64-3.6
creating build/temp.linux-x86_64-3.6/src
creating build/temp.linux-x86_64-3.6/src/sentencepiece
gcc -pthread -B /home/ye/anaconda3/envs/adapt-mnmt/compiler_compat -Wl,--sysroot=/ -Wsign-compare -DNDEBUG -g -fwrapv -O3 -Wall -Wstrict-prototypes -fPIC -I/home/ye/anaconda3/envs/adapt-mnmt/include/python3.6m -c src/sentencepiece/sentencepiece_wrap.cxx -o build/temp.linux-x86_64-3.6/src/sentencepiece/sentencepiece_wrap.o -std=c++11 -I/usr/local/include
cc1plus: warning: command-line option ‘-Wstrict-prototypes’ is valid for C/ObjC but not for C++
g++ -pthread -shared -B /home/ye/anaconda3/envs/adapt-mnmt/compiler_compat -L/home/ye/anaconda3/envs/adapt-mnmt/lib -Wl,-rpath=/home/ye/anaconda3/envs/adapt-mnmt/lib -Wl,--no-as-needed -Wl,--sysroot=/ build/temp.linux-x86_64-3.6/src/sentencepiece/sentencepiece_wrap.o -o build/lib.linux-x86_64-3.6/sentencepiece/_sentencepiece.cpython-36m-x86_64-linux-gnu.so -L/usr/local/lib -lsentencepiece -lsentencepiece_train
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/python$
```

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/python$ sudo python3 ./setup.py install
/usr/lib/python3/dist-packages/setuptools/dist.py:723: UserWarning: Usage of dash-separated 'description-file' will not be supported in future versions. Please use the underscore name 'description_file' instead
  warnings.warn(
running install
/usr/lib/python3/dist-packages/setuptools/command/install.py:34: SetuptoolsDeprecationWarning: setup.py install is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
/usr/lib/python3/dist-packages/setuptools/command/easy_install.py:158: EasyInstallDeprecationWarning: easy_install command is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
/usr/lib/python3/dist-packages/pkg_resources/__init__.py:116: PkgResourcesDeprecationWarning: 0.1.43ubuntu1 is an invalid version and will not be supported in a future release
  warnings.warn(
/usr/lib/python3/dist-packages/pkg_resources/__init__.py:116: PkgResourcesDeprecationWarning: 1.1build1 is an invalid version and will not be supported in a future release
  warnings.warn(
running bdist_egg
running egg_info
creating src/sentencepiece.egg-info
writing src/sentencepiece.egg-info/PKG-INFO
writing dependency_links to src/sentencepiece.egg-info/dependency_links.txt
writing top-level names to src/sentencepiece.egg-info/top_level.txt
writing manifest file 'src/sentencepiece.egg-info/SOURCES.txt'
reading manifest file 'src/sentencepiece.egg-info/SOURCES.txt'
reading manifest template 'MANIFEST.in'
writing manifest file 'src/sentencepiece.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
creating build/lib.linux-x86_64-3.10
creating build/lib.linux-x86_64-3.10/sentencepiece
copying src/sentencepiece/__init__.py -> build/lib.linux-x86_64-3.10/sentencepiece
copying src/sentencepiece/sentencepiece_model_pb2.py -> build/lib.linux-x86_64-3.10/sentencepiece
copying src/sentencepiece/sentencepiece_pb2.py -> build/lib.linux-x86_64-3.10/sentencepiece
running build_ext
-L/usr/local/lib -lsentencepiece -lsentencepiece_train
## cflags=-std=c++11 -I/usr/local/include
## libs=-L/usr/local/lib -lsentencepiece -lsentencepiece_train
building 'sentencepiece._sentencepiece' extension
creating build/temp.linux-x86_64-3.10
creating build/temp.linux-x86_64-3.10/src
creating build/temp.linux-x86_64-3.10/src/sentencepiece
x86_64-linux-gnu-gcc -Wno-unused-result -Wsign-compare -DNDEBUG -g -fwrapv -O2 -Wall -g -fstack-protector-strong -Wformat -Werror=format-security -g -fwrapv -O2 -g -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -fPIC -I/usr/include/python3.10 -c src/sentencepiece/sentencepiece_wrap.cxx -o build/temp.linux-x86_64-3.10/src/sentencepiece/sentencepiece_wrap.o -std=c++11 -I/usr/local/include
src/sentencepiece/sentencepiece_wrap.cxx:178:11: fatal error: Python.h: No such file or directory
  178 | # include <Python.h>
      |           ^~~~~~~~~~
compilation terminated.
error: command '/usr/bin/x86_64-linux-gnu-gcc' failed with exit code 1
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/python$ sudo apt-get install python-dev
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Package python-dev is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source
However the following packages replace it:
  python2-dev:i386 python2:i386 python2-dev python2 python-dev-is-python3

E: Package 'python-dev' has no installation candidate
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/python$
```

Installation of header files and static libraries for python-dev ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/python$ sudo apt-get install python3-dev
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following packages were automatically installed and are no longer required:
  linux-headers-5.15.0-27 linux-headers-5.15.0-27-generic linux-image-5.15.0-27-generic linux-modules-5.15.0-27-generic
  linux-modules-extra-5.15.0-27-generic
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  javascript-common libexpat1-dev libjs-jquery libjs-sphinxdoc libjs-underscore libpython3-dev libpython3.10-dev python3.10-dev
Suggested packages:
  apache2 | lighttpd | httpd
The following NEW packages will be installed:
  javascript-common libexpat1-dev libjs-jquery libjs-sphinxdoc libjs-underscore libpython3-dev libpython3.10-dev python3-dev
  python3.10-dev
0 upgraded, 9 newly installed, 0 to remove and 0 not upgraded.
Need to get 6,029 kB of archives.
After this operation, 23.8 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 javascript-common all 11+nmu1 [5,936 B]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libexpat1-dev amd64 2.4.7-1 [147 kB]
Get:3 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libjs-jquery all 3.6.0+dfsg+~3.5.13-1 [321 kB]
Get:4 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libjs-underscore all 1.13.2~dfsg-2 [118 kB]
Get:5 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libjs-sphinxdoc all 4.3.2-1 [139 kB]
Get:6 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libpython3.10-dev amd64 3.10.4-3 [4,758 kB]
Get:7 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libpython3-dev amd64 3.10.4-0ubuntu2 [7,242 B]
Get:8 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 python3.10-dev amd64 3.10.4-3 [507 kB]
Get:9 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 python3-dev amd64 3.10.4-0ubuntu2 [26.0 kB]
Fetched 6,029 kB in 1s (6,791 kB/s)
Selecting previously unselected package javascript-common.
(Reading database ... 265979 files and directories currently installed.)
Preparing to unpack .../0-javascript-common_11+nmu1_all.deb ...
Unpacking javascript-common (11+nmu1) ...
Selecting previously unselected package libexpat1-dev:amd64.
Preparing to unpack .../1-libexpat1-dev_2.4.7-1_amd64.deb ...
Unpacking libexpat1-dev:amd64 (2.4.7-1) ...
Selecting previously unselected package libjs-jquery.
Preparing to unpack .../2-libjs-jquery_3.6.0+dfsg+~3.5.13-1_all.deb ...
Unpacking libjs-jquery (3.6.0+dfsg+~3.5.13-1) ...
Selecting previously unselected package libjs-underscore.
Preparing to unpack .../3-libjs-underscore_1.13.2~dfsg-2_all.deb ...
Unpacking libjs-underscore (1.13.2~dfsg-2) ...
Selecting previously unselected package libjs-sphinxdoc.
Preparing to unpack .../4-libjs-sphinxdoc_4.3.2-1_all.deb ...
Unpacking libjs-sphinxdoc (4.3.2-1) ...
Selecting previously unselected package libpython3.10-dev:amd64.
Preparing to unpack .../5-libpython3.10-dev_3.10.4-3_amd64.deb ...
Unpacking libpython3.10-dev:amd64 (3.10.4-3) ...
Selecting previously unselected package libpython3-dev:amd64.
Preparing to unpack .../6-libpython3-dev_3.10.4-0ubuntu2_amd64.deb ...
Unpacking libpython3-dev:amd64 (3.10.4-0ubuntu2) ...
Selecting previously unselected package python3.10-dev.
Preparing to unpack .../7-python3.10-dev_3.10.4-3_amd64.deb ...
Unpacking python3.10-dev (3.10.4-3) ...
Selecting previously unselected package python3-dev.
Preparing to unpack .../8-python3-dev_3.10.4-0ubuntu2_amd64.deb ...
Unpacking python3-dev (3.10.4-0ubuntu2) ...
Setting up javascript-common (11+nmu1) ...
Setting up libexpat1-dev:amd64 (2.4.7-1) ...
Setting up libpython3.10-dev:amd64 (3.10.4-3) ...
Setting up python3.10-dev (3.10.4-3) ...
Setting up libjs-jquery (3.6.0+dfsg+~3.5.13-1) ...
Setting up libjs-underscore (1.13.2~dfsg-2) ...
Setting up libpython3-dev:amd64 (3.10.4-0ubuntu2) ...
Setting up libjs-sphinxdoc (4.3.2-1) ...
Setting up python3-dev (3.10.4-0ubuntu2) ...
Processing triggers for man-db (2.10.2-1) ...
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/python$
```

After installation of python-dev for Python3, running sentencepiece python wrapper looks OK ...   

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/python$ sudo python3 ./setup.py install
/usr/lib/python3/dist-packages/setuptools/dist.py:723: UserWarning: Usage of dash-separated 'description-file' will not be supported in future versions. Please use the underscore name 'description_file' instead
  warnings.warn(
running install
/usr/lib/python3/dist-packages/setuptools/command/install.py:34: SetuptoolsDeprecationWarning: setup.py install is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
/usr/lib/python3/dist-packages/setuptools/command/easy_install.py:158: EasyInstallDeprecationWarning: easy_install command is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
/usr/lib/python3/dist-packages/pkg_resources/__init__.py:116: PkgResourcesDeprecationWarning: 0.1.43ubuntu1 is an invalid version and will not be supported in a future release
  warnings.warn(
/usr/lib/python3/dist-packages/pkg_resources/__init__.py:116: PkgResourcesDeprecationWarning: 1.1build1 is an invalid version and will not be supported in a future release
  warnings.warn(
running bdist_egg
running egg_info
writing src/sentencepiece.egg-info/PKG-INFO
writing dependency_links to src/sentencepiece.egg-info/dependency_links.txt
writing top-level names to src/sentencepiece.egg-info/top_level.txt
reading manifest file 'src/sentencepiece.egg-info/SOURCES.txt'
reading manifest template 'MANIFEST.in'
writing manifest file 'src/sentencepiece.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
running build_ext
-L/usr/local/lib -lsentencepiece -lsentencepiece_train
## cflags=-std=c++11 -I/usr/local/include
## libs=-L/usr/local/lib -lsentencepiece -lsentencepiece_train
building 'sentencepiece._sentencepiece' extension
x86_64-linux-gnu-gcc -Wno-unused-result -Wsign-compare -DNDEBUG -g -fwrapv -O2 -Wall -g -fstack-protector-strong -Wformat -Werror=format-security -g -fwrapv -O2 -g -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -fPIC -I/usr/include/python3.10 -c src/sentencepiece/sentencepiece_wrap.cxx -o build/temp.linux-x86_64-3.10/src/sentencepiece/sentencepiece_wrap.o -std=c++11 -I/usr/local/include
x86_64-linux-gnu-g++ -shared -Wl,-O1 -Wl,-Bsymbolic-functions -Wl,-Bsymbolic-functions -g -fwrapv -O2 -Wl,-Bsymbolic-functions -g -fwrapv -O2 -g -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 build/temp.linux-x86_64-3.10/src/sentencepiece/sentencepiece_wrap.o -o build/lib.linux-x86_64-3.10/sentencepiece/_sentencepiece.cpython-310-x86_64-linux-gnu.so -L/usr/local/lib -lsentencepiece -lsentencepiece_train
creating build/bdist.linux-x86_64
creating build/bdist.linux-x86_64/egg
creating build/bdist.linux-x86_64/egg/sentencepiece
copying build/lib.linux-x86_64-3.10/sentencepiece/_sentencepiece.cpython-310-x86_64-linux-gnu.so -> build/bdist.linux-x86_64/egg/sentencepiece
copying build/lib.linux-x86_64-3.10/sentencepiece/sentencepiece_pb2.py -> build/bdist.linux-x86_64/egg/sentencepiece
copying build/lib.linux-x86_64-3.10/sentencepiece/__init__.py -> build/bdist.linux-x86_64/egg/sentencepiece
copying build/lib.linux-x86_64-3.10/sentencepiece/sentencepiece_model_pb2.py -> build/bdist.linux-x86_64/egg/sentencepiece
byte-compiling build/bdist.linux-x86_64/egg/sentencepiece/sentencepiece_pb2.py to sentencepiece_pb2.cpython-310.pyc
byte-compiling build/bdist.linux-x86_64/egg/sentencepiece/__init__.py to __init__.cpython-310.pyc
byte-compiling build/bdist.linux-x86_64/egg/sentencepiece/sentencepiece_model_pb2.py to sentencepiece_model_pb2.cpython-310.pyc
creating stub loader for sentencepiece/_sentencepiece.cpython-310-x86_64-linux-gnu.so
byte-compiling build/bdist.linux-x86_64/egg/sentencepiece/_sentencepiece.py to _sentencepiece.cpython-310.pyc
creating build/bdist.linux-x86_64/egg/EGG-INFO
copying src/sentencepiece.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying src/sentencepiece.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying src/sentencepiece.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying src/sentencepiece.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
writing build/bdist.linux-x86_64/egg/EGG-INFO/native_libs.txt
zip_safe flag not set; analyzing archive contents...
sentencepiece.__pycache__._sentencepiece.cpython-310: module references __file__
creating dist
creating 'dist/sentencepiece-0.1.96-py3.10-linux-x86_64.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing sentencepiece-0.1.96-py3.10-linux-x86_64.egg
creating /usr/local/lib/python3.10/dist-packages/sentencepiece-0.1.96-py3.10-linux-x86_64.egg
Extracting sentencepiece-0.1.96-py3.10-linux-x86_64.egg to /usr/local/lib/python3.10/dist-packages
Adding sentencepiece 0.1.96 to easy-install.pth file

Installed /usr/local/lib/python3.10/dist-packages/sentencepiece-0.1.96-py3.10-linux-x86_64.egg
Processing dependencies for sentencepiece==0.1.96
Finished processing dependencies for sentencepiece==0.1.96
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/sentencepiece/python$
```

Check sentencepiece methods:  

```python 
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ python
Python 3.6.13 |Anaconda, Inc.| (default, Jun  4 2021, 14:25:59)
[GCC 7.5.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import sentencepiece as spm
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ python
Python 3.6.13 |Anaconda, Inc.| (default, Jun  4 2021, 14:25:59)
[GCC 7.5.0] on linuxystem-Product-Name:~/tool/adapt-mnmt$ vi ./scripts/sentencepiece.py
Type "help", "copyright", "credits" or "license" for more information.
>>> import sentencepiece as spm
>>> print(dir(spm))
['BytesIO', 'EncoderVersion_kOptimized', 'EncoderVersion_kOriginal', 'SentencePieceProcessor', 'SentencePieceTrainer', 'SentencePieceTrainer__TrainFromMap', 'SentencePieceTrainer__TrainFromMap2', 'SentencePieceTrainer__TrainFromMap3', 'SentencePieceTrainer__TrainFromMap4', 'SentencePieceTrainer__TrainFromString', 'SetRandomGeneratorSeed', 'StringIO', '_SwigNonDynamicMeta', '__builtin__', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__path__', '__spec__', '_add_snake_case', '_batchnize', '_sentencepiece', '_sentencepiece_processor_init_native', '_swig_add_metaclass', '_swig_python_version_info', '_swig_repr', '_swig_setattr_nondynamic_class_variable', '_swig_setattr_nondynamic_instance_variable', 'csv', 'm', 're', 'set_random_generator_seed', 'sys']
>>> print(dir(spm.SentencePieceTrainer))
['Train', '_TrainFromMap', '_TrainFromMap2', '_TrainFromMap3', '_TrainFromMap4', '_TrainFromString', '__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'thisown', 'train']
>>> print(dir(spm.SentencePieceProcessor))
['Decode', 'DecodeIds', 'DecodeIdsAsSerializedProto', 'DecodeIdsAsSerializedProtoWithCheck', 'DecodeIdsWithCheck', 'DecodePieces', 'DecodePiecesAsSerializedProto', 'Detokenize', 'Encode', 'EncodeAsIds', 'EncodeAsPieces', 'EncodeAsSerializedProto', 'GetEncoderVersion', 'GetPieceSize', 'GetScore', 'IdToPiece', 'Init', 'IsByte', 'IsControl', 'IsUnknown', 'IsUnused', 'Load', 'LoadFromFile', 'LoadFromSerializedProto', 'LoadVocabulary', 'NBestEncodeAsIds', 'NBestEncodeAsPieces', 'NBestEncodeAsSerializedProto', 'PieceToId', 'ResetVocabulary', 'SampleEncodeAsIds', 'SampleEncodeAsPieces', 'SampleEncodeAsSerializedProto', 'SetDecodeExtraOptions', 'SetEncodeExtraOptions', 'SetEncoderVersion', 'SetVocabulary', 'Tokenize', '__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getstate__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__len__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__setstate__', '__sizeof__', '__str__', '__subclasshook__', '__swig_destroy__', '__weakref__', 'bos_id', 'decode', 'decode_ids', 'decode_ids_as_serialized_proto', 'decode_ids_as_serialized_proto_with_check', 'decode_ids_with_check', 'decode_pieces', 'decode_pieces_as_serialized_proto', 'detokenize', 'encode', 'encode_as_ids', 'encode_as_pieces', 'encode_as_serialized_proto', 'eos_id', 'get_encoder_version', 'get_piece_size', 'get_score', 'id_to_piece', 'init', 'is_byte', 'is_control', 'is_unknown', 'is_unused', 'load', 'load_from_file', 'load_from_serialized_proto', 'load_vocabulary', 'nbest_encode_as_ids', 'nbest_encode_as_pieces', 'nbest_encode_as_serialized_proto', 'pad_id', 'piece_size', 'piece_to_id', 'reset_vocabulary', 'sample_encode_as_ids', 'sample_encode_as_pieces', 'sample_encode_as_serialized_proto', 'serialized_model_proto', 'set_decode_extra_options', 'set_encode_extra_options', 'set_encoder_version', 'set_vocabulary', 'thisown', 'tokenize', 'unk_id', 'vocab_size']
>>>
```

## Fixed One Error

Reference Link:  
https://stackoverflow.com/questions/59762996/how-to-fix-attributeerror-partially-initialized-module  

rename sentencepiece.py to sp.py and that solved the following errors:  

```
AttributeError: module 'sentencepiece' has no attribute 'SentencePieceTrainer'
...
...
...
AttributeError: module 'sentencepiece' has no attribute 'SentencePieceProcessor'
```

the following is the running log:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/scripts$ mv sentencepiece.py sp.py
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/scripts$ vi ./preprocess.sh
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/scripts$ cd ..
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ time bash ./scripts/preprocess.sh sov-1 32000

LEARNING SP MODEL ...
sentencepiece_trainer.cc(177) LOG(INFO) Running command: --input=/home/ye/tool/adapt-mnmt/models/sov-1/data/train.src --model_prefix=/home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel/spm.src --vocab_size=32000 --hard_vocab_limit=false --shuffle_input_sentence=true --input_sentence_size=6000000
sentencepiece_trainer.cc(77) LOG(INFO) Starts training with :
trainer_spec {
  input: /home/ye/tool/adapt-mnmt/models/sov-1/data/train.src
  input_format:
  model_prefix: /home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel/spm.src
  model_type: UNIGRAM
  vocab_size: 32000
  self_test_sample_size: 0
  character_coverage: 0.9995
  input_sentence_size: 6000000
  shuffle_input_sentence: 1
  seed_sentencepiece_size: 1000000
  shrinking_factor: 0.75
  max_sentence_length: 4192
  num_threads: 16
  num_sub_iterations: 2
  max_sentencepiece_length: 16
  split_by_unicode_script: 1
  split_by_number: 1
  split_by_whitespace: 1
  split_digits: 0
  treat_whitespace_as_suffix: 0
  allow_whitespace_only_pieces: 0
  required_chars:
  byte_fallback: 0
  vocabulary_output_piece_score: 1
  train_extremely_large_corpus: 0
  hard_vocab_limit: 0
  use_all_vocab: 0
  unk_id: 0
  bos_id: 1
  eos_id: 2
  pad_id: -1
  unk_piece: <unk>
  bos_piece: <s>
  eos_piece: </s>
  pad_piece: <pad>
  unk_surface:  ⁇
}
normalizer_spec {
  name: nmt_nfkc
  add_dummy_prefix: 1
  remove_extra_whitespaces: 1
  escape_whitespaces: 1
  normalization_rule_tsv:
}
denormalizer_spec {}
trainer_interface.cc(329) LOG(INFO) SentenceIterator is not specified. Using MultiFileSentenceIterator.
trainer_interface.cc(178) LOG(INFO) Loading corpus: /home/ye/tool/adapt-mnmt/models/sov-1/data/train.src
trainer_interface.cc(385) LOG(INFO) Loaded all 819460 sentences
trainer_interface.cc(400) LOG(INFO) Adding meta_piece: <unk>
trainer_interface.cc(400) LOG(INFO) Adding meta_piece: <s>
trainer_interface.cc(400) LOG(INFO) Adding meta_piece: </s>
trainer_interface.cc(405) LOG(INFO) Normalizing sentences...
trainer_interface.cc(466) LOG(INFO) all chars count=63686442
trainer_interface.cc(477) LOG(INFO) Done: 99.9501% characters are covered.
trainer_interface.cc(487) LOG(INFO) Alphabet size=2938
trainer_interface.cc(488) LOG(INFO) Final character coverage=0.999501
trainer_interface.cc(520) LOG(INFO) Done! preprocessed 819460 sentences.
unigram_model_trainer.cc(139) LOG(INFO) Making suffix array...
unigram_model_trainer.cc(143) LOG(INFO) Extracting frequent sub strings...
unigram_model_trainer.cc(194) LOG(INFO) Initialized 1000000 seed sentencepieces
trainer_interface.cc(526) LOG(INFO) Tokenizing input sentences with whitespace: 819460
trainer_interface.cc(537) LOG(INFO) Done! 736392
unigram_model_trainer.cc(489) LOG(INFO) Using 736392 sentences for EM training
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=509212 obj=15.0288 num_tokens=3111764 num_tokens/piece=6.11094
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=435847 obj=12.3973 num_tokens=3120396 num_tokens/piece=7.15938
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=325641 obj=12.3834 num_tokens=3194709 num_tokens/piece=9.81052
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=324540 obj=12.3649 num_tokens=3195281 num_tokens/piece=9.84557
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=243291 obj=12.4446 num_tokens=3329493 num_tokens/piece=13.6852
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=243182 obj=12.4225 num_tokens=3330065 num_tokens/piece=13.6937
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=182381 obj=12.5397 num_tokens=3497376 num_tokens/piece=19.1762
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=182376 obj=12.514 num_tokens=3497806 num_tokens/piece=19.1791
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=136780 obj=12.6623 num_tokens=3683168 num_tokens/piece=26.9277
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=136780 obj=12.6322 num_tokens=3684122 num_tokens/piece=26.9347
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=102585 obj=12.816 num_tokens=3883806 num_tokens/piece=37.8594
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=102585 obj=12.7834 num_tokens=3883968 num_tokens/piece=37.861
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=76938 obj=13 num_tokens=4101746 num_tokens/piece=53.3124
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=76938 obj=12.9644 num_tokens=4101873 num_tokens/piece=53.314
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=57703 obj=13.2158 num_tokens=4336752 num_tokens/piece=75.1564
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=57703 obj=13.1737 num_tokens=4336789 num_tokens/piece=75.1571
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=43277 obj=13.4633 num_tokens=4588785 num_tokens/piece=106.033
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=43277 obj=13.4142 num_tokens=4588799 num_tokens/piece=106.033
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=35200 obj=13.6451 num_tokens=4783159 num_tokens/piece=135.885
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=35200 obj=13.6068 num_tokens=4783173 num_tokens/piece=135.886
trainer_interface.cc(615) LOG(INFO) Saving model: /home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel/spm.src.model
trainer_interface.cc(626) LOG(INFO) Saving vocabs: /home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel/spm.src.vocab
sentencepiece_trainer.cc(177) LOG(INFO) Running command: --input=/home/ye/tool/adapt-mnmt/models/sov-1/data/train.tgt --model_prefix=/home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel/spm.tgt --vocab_size=32000 --hard_vocab_limit=false --shuffle_input_sentence=true --input_sentence_size=6000000
sentencepiece_trainer.cc(77) LOG(INFO) Starts training with :
trainer_spec {
  input: /home/ye/tool/adapt-mnmt/models/sov-1/data/train.tgt
  input_format:
  model_prefix: /home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel/spm.tgt
  model_type: UNIGRAM
  vocab_size: 32000
  self_test_sample_size: 0
  character_coverage: 0.9995
  input_sentence_size: 6000000
  shuffle_input_sentence: 1
  seed_sentencepiece_size: 1000000
  shrinking_factor: 0.75
  max_sentence_length: 4192
  num_threads: 16
  num_sub_iterations: 2
  max_sentencepiece_length: 16
  split_by_unicode_script: 1
  split_by_number: 1
  split_by_whitespace: 1
  split_digits: 0
  treat_whitespace_as_suffix: 0
  allow_whitespace_only_pieces: 0
  required_chars:
  byte_fallback: 0
  vocabulary_output_piece_score: 1
  train_extremely_large_corpus: 0
  hard_vocab_limit: 0
  use_all_vocab: 0
  unk_id: 0
  bos_id: 1
  eos_id: 2
  pad_id: -1
  unk_piece: <unk>
  bos_piece: <s>
  eos_piece: </s>
  pad_piece: <pad>
  unk_surface:  ⁇
}
normalizer_spec {
  name: nmt_nfkc
  add_dummy_prefix: 1
  remove_extra_whitespaces: 1
  escape_whitespaces: 1
  normalization_rule_tsv:
}
denormalizer_spec {}
trainer_interface.cc(329) LOG(INFO) SentenceIterator is not specified. Using MultiFileSentenceIterator.
trainer_interface.cc(178) LOG(INFO) Loading corpus: /home/ye/tool/adapt-mnmt/models/sov-1/data/train.tgt
trainer_interface.cc(385) LOG(INFO) Loaded all 819460 sentences
trainer_interface.cc(400) LOG(INFO) Adding meta_piece: <unk>
trainer_interface.cc(400) LOG(INFO) Adding meta_piece: <s>
trainer_interface.cc(400) LOG(INFO) Adding meta_piece: </s>
trainer_interface.cc(405) LOG(INFO) Normalizing sentences...
trainer_interface.cc(466) LOG(INFO) all chars count=58769682
trainer_interface.cc(477) LOG(INFO) Done: 99.9501% characters are covered.
trainer_interface.cc(487) LOG(INFO) Alphabet size=2977
trainer_interface.cc(488) LOG(INFO) Final character coverage=0.999501
trainer_interface.cc(520) LOG(INFO) Done! preprocessed 819460 sentences.
unigram_model_trainer.cc(139) LOG(INFO) Making suffix array...
unigram_model_trainer.cc(143) LOG(INFO) Extracting frequent sub strings...
unigram_model_trainer.cc(194) LOG(INFO) Initialized 1000000 seed sentencepieces
trainer_interface.cc(526) LOG(INFO) Tokenizing input sentences with whitespace: 819460
trainer_interface.cc(537) LOG(INFO) Done! 736466
unigram_model_trainer.cc(489) LOG(INFO) Using 736466 sentences for EM training
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=508844 obj=14.7287 num_tokens=3110126 num_tokens/piece=6.11214
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=435675 obj=12.3451 num_tokens=3119234 num_tokens/piece=7.15954
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=325531 obj=12.3337 num_tokens=3194804 num_tokens/piece=9.81413
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=324404 obj=12.3126 num_tokens=3195519 num_tokens/piece=9.85043
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=243182 obj=12.3974 num_tokens=3330606 num_tokens/piece=13.6959
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=243078 obj=12.374 num_tokens=3331058 num_tokens/piece=13.7037
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=182304 obj=12.4982 num_tokens=3498822 num_tokens/piece=19.1922
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=182299 obj=12.4701 num_tokens=3499418 num_tokens/piece=19.196
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=136722 obj=12.6279 num_tokens=3684963 num_tokens/piece=26.9522
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=136722 obj=12.5951 num_tokens=3685217 num_tokens/piece=26.9541
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=102541 obj=12.7904 num_tokens=3885320 num_tokens/piece=37.8904
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=102541 obj=12.7548 num_tokens=3885420 num_tokens/piece=37.8914
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=76905 obj=12.9848 num_tokens=4102762 num_tokens/piece=53.3484
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=76905 obj=12.9461 num_tokens=4105667 num_tokens/piece=53.3862
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=57678 obj=13.2141 num_tokens=4340283 num_tokens/piece=75.2502
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=57678 obj=13.1684 num_tokens=4340283 num_tokens/piece=75.2502
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=43258 obj=13.4767 num_tokens=4592496 num_tokens/piece=106.165
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=43258 obj=13.4233 num_tokens=4592840 num_tokens/piece=106.173
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=35200 obj=13.6685 num_tokens=4784977 num_tokens/piece=135.937
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=35200 obj=13.6272 num_tokens=4785014 num_tokens/piece=135.938
trainer_interface.cc(615) LOG(INFO) Saving model: /home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel/spm.tgt.model
trainer_interface.cc(626) LOG(INFO) Saving vocabs: /home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel/spm.tgt.vocab
SP MODEL: [/home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel]

APPLYING SP MODEL ON [train] ...

APPLYING SP MODEL ON [dev] ...

APPLYING SP MODEL ON [test] ...
SP DATA: [ /home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel ]

GENERATING VOCABULARY ...
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/bin/build_vocab.py", line 5, in <module>
    from opennmt import constants
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/__init__.py", line 5, in <module>
    from opennmt import decoders
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/decoders/__init__.py", line 3, in <module>
    from opennmt.decoders.rnn_decoder import RNNDecoder
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/decoders/rnn_decoder.py", line 12, in <module>
    from opennmt.utils.cell import build_cell
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/utils/cell.py", line 13, in <module>
    cell_class=tf.nn.rnn_cell.LSTMCell,
AttributeError: module 'tensorflow._api.v2.nn' has no attribute 'rnn_cell'
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/bin/build_vocab.py", line 5, in <module>
    from opennmt import constants
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/__init__.py", line 5, in <module>
    from opennmt import decoders
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/decoders/__init__.py", line 3, in <module>
    from opennmt.decoders.rnn_decoder import RNNDecoder
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/decoders/rnn_decoder.py", line 12, in <module>
    from opennmt.utils.cell import build_cell
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/utils/cell.py", line 13, in <module>
    cell_class=tf.nn.rnn_cell.LSTMCell,
AttributeError: module 'tensorflow._api.v2.nn' has no attribute 'rnn_cell'

real    2m49.997s
user    9m5.807s
sys     0m2.715s
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

Yes, I got a new ERROR as above ...  

The improvement is now some files under the spdata/ and spmodel/ folders:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ tree ./models/sov-1/data/
./models/sov-1/data/
├── dev.src
├── dev.tgt
├── spdata
│   ├── dev.src
│   ├── dev.tgt
│   ├── test.src
│   ├── test.tgt
│   ├── train.src
│   └── train.tgt
├── spmodel
│   ├── spm.src.model
│   ├── spm.src.vocab
│   ├── spm.tgt.model
│   └── spm.tgt.vocab
├── test-sets
│   ├── test.en
│   ├── test.ja
│   └── test.ko
├── test.src
├── test.tgt
├── train.src
└── train.tgt

3 directories, 19 files
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

I also checked the file size: 

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data/spdata$ wc *
    17740    423771   2846941 dev.src
    17740    370467   2651717 dev.tgt
    22404    522349   3516973 test.src
    22404    455109   3270501 test.tgt
   819460  19847625 135372221 train.src
   819460  17386979 126355895 train.tgt
  1719208  39006300 274014248 total
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data/spdata$ cd ../spmodel/
```

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data/spmodel$ wc *
  68964   35351  819556 spm.src.model
  32000   64000  609925 spm.src.vocab
  68994   35257  818959 spm.tgt.model
  32000   64000  610073 spm.tgt.vocab
 201958  198608 2858513 total
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data/spmodel$
```

## Fixing the Error Relating to Tensorflow

Currently, I have to fix the following error:  

```
GENERATING VOCABULARY ...
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/bin/build_vocab.py", line 5, in <module>
    from opennmt import constants
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/__init__.py", line 5, in <module>
    from opennmt import decoders
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/decoders/__init__.py", line 3, in <module>
    from opennmt.decoders.rnn_decoder import RNNDecoder
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/decoders/rnn_decoder.py", line 12, in <module>
    from opennmt.utils.cell import build_cell
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/utils/cell.py", line 13, in <module>
    cell_class=tf.nn.rnn_cell.LSTMCell,
AttributeError: module 'tensorflow._api.v2.nn' has no attribute 'rnn_cell'
...
...
...
```

I think this error is relating to tensorflow versions ...  
I updated the cell.py as follows:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data/spmodel$ vi /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/utils/cell.py

  1 """RNN cells helpers."""
  2
  3 import collections
  4
  5 import tensorflow as tf
  6
  7
  8 def build_cell(num_layers,
  9                num_units,
 10                mode,
 11                dropout=0.0,
 12                residual_connections=False,
 13 #               cell_class=tf.nn.rnn_cell.LSTMCell,
 14                cell_class=tf.contrib.rnn_cell.LSTMCell,
 15                attention_layers=None,
 16                attention_mechanisms=None):
```

After that, clean the folders "spdata/" and "spmodel/" and Re-run again and got following error:  

```
AttributeError: module 'tensorflow' has no attribute 'contrib'
```

Checked current tensorflow version:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ (adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ python
Python 3.6.13 |Anaconda, Inc.| (default, Jun  4 2021, 14:25:59)
[GCC 7.5.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
>>> print(tf.__version__)
2.6.2
>>>
```

I think I should downgrade the version of tensorflow based on the original running environment of adapt-mnmt:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ pip uninstall tensorflow
WARNING: Skipping tensorflow as it is not installed.
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ pip3 uninstall tensorflow
WARNING: Skipping tensorflow as it is not installed.
```

Oh! it should be "tensorflow-gpu" ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ pip uninstall tensorflow-gpu
Found existing installation: tensorflow-gpu 2.6.2
Uninstalling tensorflow-gpu-2.6.2:
  Would remove:
    /home/ye/anaconda3/envs/adapt-mnmt/bin/estimator_ckpt_converter
    /home/ye/anaconda3/envs/adapt-mnmt/bin/import_pb_to_tensorboard
    /home/ye/anaconda3/envs/adapt-mnmt/bin/saved_model_cli
    /home/ye/anaconda3/envs/adapt-mnmt/bin/tensorboard
    /home/ye/anaconda3/envs/adapt-mnmt/bin/tf_upgrade_v2
    /home/ye/anaconda3/envs/adapt-mnmt/bin/tflite_convert
    /home/ye/anaconda3/envs/adapt-mnmt/bin/toco
    /home/ye/anaconda3/envs/adapt-mnmt/bin/toco_from_protos
    /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/tensorflow/*
    /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/tensorflow_gpu-2.6.2.dist-info/*
Proceed (Y/n)? Y
  Successfully uninstalled tensorflow-gpu-2.6.2
```

After removing tensorflow-gpu version 2.6.2, I installed version 1.15 as follows:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ pip install tensorflow-gpu==1.15
Collecting tensorflow-gpu==1.15
  Downloading tensorflow_gpu-1.15.0-cp36-cp36m-manylinux2010_x86_64.whl (411.5 MB)
     |████████████████████████████████| 411.5 MB 18 kB/s
Requirement already satisfied: grpcio>=1.8.6 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from tensorflow-gpu==1.15) (1.46.1)
Requirement already satisfied: keras-preprocessing>=1.0.5 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from tensorflow-gpu==1.15) (1.1.2)
Collecting keras-applications>=1.0.8
  Downloading Keras_Applications-1.0.8-py3-none-any.whl (50 kB)
     |████████████████████████████████| 50 kB 954 kB/s
Requirement already satisfied: wrapt>=1.11.1 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from tensorflow-gpu==1.15) (1.12.1)
Collecting tensorboard<1.16.0,>=1.15.0
  Downloading tensorboard-1.15.0-py3-none-any.whl (3.8 MB)
     |████████████████████████████████| 3.8 MB 101.8 MB/s
Collecting gast==0.2.2
  Downloading gast-0.2.2.tar.gz (10 kB)
  Preparing metadata (setup.py) ... done
Requirement already satisfied: wheel>=0.26 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from tensorflow-gpu==1.15) (0.37.1)
Requirement already satisfied: absl-py>=0.7.0 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from tensorflow-gpu==1.15) (0.15.0)
Requirement already satisfied: six>=1.10.0 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from tensorflow-gpu==1.15) (1.15.0)
Collecting tensorflow-estimator==1.15.1
  Downloading tensorflow_estimator-1.15.1-py2.py3-none-any.whl (503 kB)
     |████████████████████████████████| 503 kB 91.3 MB/s
Requirement already satisfied: opt-einsum>=2.3.2 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from tensorflow-gpu==1.15) (3.3.0)
Requirement already satisfied: google-pasta>=0.1.6 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from tensorflow-gpu==1.15) (0.2.0)
Collecting astor>=0.6.0
  Downloading astor-0.8.1-py2.py3-none-any.whl (27 kB)
Requirement already satisfied: protobuf>=3.6.1 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from tensorflow-gpu==1.15) (3.19.4)
Requirement already satisfied: termcolor>=1.1.0 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from tensorflow-gpu==1.15) (1.1.0)
Requirement already satisfied: numpy<2.0,>=1.16.0 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from tensorflow-gpu==1.15) (1.19.5)
Requirement already satisfied: h5py in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from keras-applications>=1.0.8->tensorflow-gpu==1.15) (3.1.0)
Requirement already satisfied: setuptools>=41.0.0 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from tensorboard<1.16.0,>=1.15.0->tensorflow-gpu==1.15) (58.0.4)
Requirement already satisfied: markdown>=2.6.8 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from tensorboard<1.16.0,>=1.15.0->tensorflow-gpu==1.15) (3.3.7)
Requirement already satisfied: werkzeug>=0.11.15 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from tensorboard<1.16.0,>=1.15.0->tensorflow-gpu==1.15) (2.0.3)
Requirement already satisfied: importlib-metadata>=4.4 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from markdown>=2.6.8->tensorboard<1.16.0,>=1.15.0->tensorflow-gpu==1.15) (4.8.3)
Requirement already satisfied: dataclasses in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from werkzeug>=0.11.15->tensorboard<1.16.0,>=1.15.0->tensorflow-gpu==1.15) (0.8)
Requirement already satisfied: cached-property in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from h5py->keras-applications>=1.0.8->tensorflow-gpu==1.15) (1.5.2)
Requirement already satisfied: zipp>=0.5 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from importlib-metadata>=4.4->markdown>=2.6.8->tensorboard<1.16.0,>=1.15.0->tensorflow-gpu==1.15) (3.6.0)
Requirement already satisfied: typing-extensions>=3.6.4 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from importlib-metadata>=4.4->markdown>=2.6.8->tensorboard<1.16.0,>=1.15.0->tensorflow-gpu==1.15) (3.7.4.3)
Building wheels for collected packages: gast
  Building wheel for gast (setup.py) ... done
  Created wheel for gast: filename=gast-0.2.2-py3-none-any.whl size=7554 sha256=1f6697a3079bb446e7248f825f3dabc8036961cb204824bf4fdbbf5913f27406
  Stored in directory: /home/ye/.cache/pip/wheels/19/a7/b9/0740c7a3a7d1d348f04823339274b90de25fbcd217b2ee1fbe
Successfully built gast
Installing collected packages: tensorflow-estimator, tensorboard, keras-applications, gast, astor, tensorflow-gpu
  Attempting uninstall: tensorflow-estimator
    Found existing installation: tensorflow-estimator 2.6.0
    Uninstalling tensorflow-estimator-2.6.0:
      Successfully uninstalled tensorflow-estimator-2.6.0
  Attempting uninstall: tensorboard
    Found existing installation: tensorboard 2.6.0
    Uninstalling tensorboard-2.6.0:
      Successfully uninstalled tensorboard-2.6.0
  Attempting uninstall: gast
    Found existing installation: gast 0.4.0
    Uninstalling gast-0.4.0:
      Successfully uninstalled gast-0.4.0
Successfully installed astor-0.8.1 gast-0.2.2 keras-applications-1.0.8 tensorboard-1.15.0 tensorflow-estimator-1.15.1 tensorflow-gpu-1.15.0
```

confirm installation by importing tensorflow module and it looks OK ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ python
Python 3.6.13 |Anaconda, Inc.| (default, Jun  4 2021, 14:25:59)
[GCC 7.5.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
>>> print(tf.__version__)
1.15.0
>>>
```

Rerun again and got different type of error, for this time relating to one more argument ...  

```
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=43258 obj=13.4767 num_tokens=4592496 num_tokens/piece=106.165
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=43258 obj=13.4233 num_tokens=4592840 num_tokens/piece=106.173
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=0 size=35200 obj=13.6685 num_tokens=4784977 num_tokens/piece=135.937
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=35200 obj=13.6272 num_tokens=4785014 num_tokens/piece=135.938
trainer_interface.cc(615) LOG(INFO) Saving model: /home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel/spm.tgt.model
trainer_interface.cc(626) LOG(INFO) Saving vocabs: /home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel/spm.tgt.vocab
SP MODEL: [/home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel]

APPLYING SP MODEL ON [train] ...

APPLYING SP MODEL ON [dev] ...

APPLYING SP MODEL ON [test] ...
SP DATA: [ /home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel ]

GENERATING VOCABULARY ...
WARNING:tensorflow:
The TensorFlow contrib module will not be included in TensorFlow 2.0.
For more information, please see:
  * https://github.com/tensorflow/community/blob/master/rfcs/20180907-contrib-sunset.md
  * https://github.com/tensorflow/addons
  * https://github.com/tensorflow/io (for I/O related ops)
If you depend on functionality not listed there, please file an issue.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/decoders/rnn_decoder.py:428: The name tf.nn.rnn_cell.RNNCell is deprecated. Please use tf.compat.v1.nn.rnn_cell.RNNCell instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/utils/hooks.py:15: The name tf.train.SessionRunHook is deprecated. Please use tf.estimator.SessionRunHook instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/optimizers/adafactor.py:34: The name tf.train.Optimizer is deprecated. Please use tf.compat.v1.train.Optimizer instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/optimizers/multistep_adam.py:36: The name tf.train.AdamOptimizer is deprecated. Please use tf.compat.v1.train.AdamOptimizer instead.

usage: build_vocab.py [-h] [--from_vocab FROM_VOCAB]
                      [--from_format {default,sentencepiece}] --save_vocab
                      SAVE_VOCAB [--min_frequency MIN_FREQUENCY] [--size SIZE]
                      [--size_multiple SIZE_MULTIPLE]
                      [--without_sequence_tokens]
                      [--tokenizer {CharacterTokenizer,OpenNMTTokenizer,SpaceTokenizer}]
                      [--tokenizer_config TOKENIZER_CONFIG]
                      [data [data ...]]
build_vocab.py: error: argument --size: expected one argument
WARNING:tensorflow:
The TensorFlow contrib module will not be included in TensorFlow 2.0.
For more information, please see:
  * https://github.com/tensorflow/community/blob/master/rfcs/20180907-contrib-sunset.md
  * https://github.com/tensorflow/addons
  * https://github.com/tensorflow/io (for I/O related ops)
If you depend on functionality not listed there, please file an issue.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/decoders/rnn_decoder.py:428: The name tf.nn.rnn_cell.RNNCell is deprecated. Please use tf.compat.v1.nn.rnn_cell.RNNCell instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/utils/hooks.py:15: The name tf.train.SessionRunHook is deprecated. Please use tf.estimator.SessionRunHook instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/optimizers/adafactor.py:34: The name tf.train.Optimizer is deprecated. Please use tf.compat.v1.train.Optimizer instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/optimizers/multistep_adam.py:36: The name tf.train.AdamOptimizer is deprecated. Please use tf.compat.v1.train.AdamOptimizer instead.

usage: build_vocab.py [-h] [--from_vocab FROM_VOCAB]
                      [--from_format {default,sentencepiece}] --save_vocab
                      SAVE_VOCAB [--min_frequency MIN_FREQUENCY] [--size SIZE]
                      [--size_multiple SIZE_MULTIPLE]
                      [--without_sequence_tokens]
                      [--tokenizer {CharacterTokenizer,OpenNMTTokenizer,SpaceTokenizer}]
                      [--tokenizer_config TOKENIZER_CONFIG]
                      [data [data ...]]
build_vocab.py: error: argument --size: expected one argument

real    2m50.929s
user    9m19.784s
sys     0m2.591s
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

I found one error inside the "preprocess.sh" script, i.e. Although using $VOCABSIZE, there is no assignment for that variable ...  

```bash
         python $GEN_VOCAB --size $VOCABSIZE --save_vocab vocab.$SRC train.$SRC
         python $GEN_VOCAB --size $VOCABSIZE --save_vocab vocab.$TGT train.$TGT
```

And thus, I updated the "scripts/preprocess.sh" as follows:  

```bash
EXPID=$1        # pt-en, gl-en, gl-en_progadapt, ptgl-en_proggrow
SPMSIZE=$2      # 4000/single-pair/low-resource 8000/single-pair 16000/single-pair 32000/mnmt based on the model type
VOCABSIZE=$3
```

rerun scripts/preprocess.sh again and got following error:  

```
GENERATING VOCABULARY ...
WARNING:tensorflow:
The TensorFlow contrib module will not be included in TensorFlow 2.0.
For more information, please see:
  * https://github.com/tensorflow/community/blob/master/rfcs/20180907-contrib-sunset.md
  * https://github.com/tensorflow/addons
  * https://github.com/tensorflow/io (for I/O related ops)
If you depend on functionality not listed there, please file an issue.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/decoders/rnn_decoder.py:428: The name tf.nn.rnn_cell.RNNCell is deprecated. Please use tf.compat.v1.nn.rnn_cell.RNNCell instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/utils/hooks.py:15: The name tf.train.SessionRunHook is deprecated. Please use tf.estimator.SessionRunHook instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/optimizers/adafactor.py:34: The name tf.train.Optimizer is deprecated. Please use tf.compat.v1.train.Optimizer instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/optimizers/multistep_adam.py:36: The name tf.train.AdamOptimizer is deprecated. Please use tf.compat.v1.train.AdamOptimizer instead.

Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/bin/build_vocab.py", line 59, in <module>
    main()
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/bin/build_vocab.py", line 50, in main
    from_format=args.from_format)
TypeError: __init__() got an unexpected keyword argument 'from_format'
WARNING:tensorflow:
The TensorFlow contrib module will not be included in TensorFlow 2.0.
For more information, please see:
  * https://github.com/tensorflow/community/blob/master/rfcs/20180907-contrib-sunset.md
  * https://github.com/tensorflow/addons
  * https://github.com/tensorflow/io (for I/O related ops)
If you depend on functionality not listed there, please file an issue.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/decoders/rnn_decoder.py:428: The name tf.nn.rnn_cell.RNNCell is deprecated. Please use tf.compat.v1.nn.rnn_cell.RNNCell instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/utils/hooks.py:15: The name tf.train.SessionRunHook is deprecated. Please use tf.estimator.SessionRunHook instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/optimizers/adafactor.py:34: The name tf.train.Optimizer is deprecated. Please use tf.compat.v1.train.Optimizer instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/optimizers/multistep_adam.py:36: The name tf.train.AdamOptimizer is deprecated. Please use tf.compat.v1.train.AdamOptimizer instead.

Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/bin/build_vocab.py", line 59, in <module>
    main()
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/bin/build_vocab.py", line 50, in main
    from_format=args.from_format)
TypeError: __init__() got an unexpected keyword argument 'from_format'

real    2m51.479s
user    9m22.391s
sys     0m2.876s
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

check the commmand line argument of the build_vocab.py program:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ python ./OpenNMT/opennmt/bin/build_vocab.py --help
WARNING:tensorflow:
The TensorFlow contrib module will not be included in TensorFlow 2.0.
For more information, please see:
  * https://github.com/tensorflow/community/blob/master/rfcs/20180907-contrib-sunset.md
  * https://github.com/tensorflow/addons
  * https://github.com/tensorflow/io (for I/O related ops)
If you depend on functionality not listed there, please file an issue.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/decoders/rnn_decoder.py:428: The name tf.nn.rnn_cell.RNNCell is deprecated. Please use tf.compat.v1.nn.rnn_cell.RNNCell instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/utils/hooks.py:15: The name tf.train.SessionRunHook is deprecated. Please use tf.estimator.SessionRunHook instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/optimizers/adafactor.py:34: The name tf.train.Optimizer is deprecated. Please use tf.compat.v1.train.Optimizer instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/optimizers/multistep_adam.py:36: The name tf.train.AdamOptimizer is deprecated. Please use tf.compat.v1.train.AdamOptimizer instead.

usage: build_vocab.py [-h] [--from_vocab FROM_VOCAB]
                      [--from_format {default,sentencepiece}] --save_vocab
                      SAVE_VOCAB [--min_frequency MIN_FREQUENCY] [--size SIZE]
                      [--size_multiple SIZE_MULTIPLE]
                      [--without_sequence_tokens]
                      [--tokenizer {CharacterTokenizer,OpenNMTTokenizer,SpaceTokenizer}]
                      [--tokenizer_config TOKENIZER_CONFIG]
                      [data [data ...]]

positional arguments:
  data                  Source text file. (default: None)

optional arguments:
  -h, --help            show this help message and exit
  --from_vocab FROM_VOCAB
                        Build from a saved vocabulary (see also
                        --from_format). (default: None)
  --from_format {default,sentencepiece}
                        The format of the saved vocabulary (see also
                        --from_vocab). (default: default)
  --save_vocab SAVE_VOCAB
                        Output vocabulary file. (default: None)
  --min_frequency MIN_FREQUENCY
                        Minimum word frequency. (default: 1)
  --size SIZE           Maximum vocabulary size. If = 0, do not limit
                        vocabulary. (default: 0)
  --size_multiple SIZE_MULTIPLE
                        Ensure that the vocabulary size + 1 is a multiple of
                        this value (+ 1 represents the <unk> token that will
                        be added during the training. (default: 1)
  --without_sequence_tokens
                        If set, do not add special sequence tokens (start,
                        end) in the vocabulary. (default: False)
  --tokenizer {CharacterTokenizer,OpenNMTTokenizer,SpaceTokenizer}
                        Tokenizer class name. (default: SpaceTokenizer)
  --tokenizer_config TOKENIZER_CONFIG
                        Tokenization configuration file. (default: None)
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

command line running such as follows also giving the same error:  

```
python OpenNMT/opennmt/bin/build_vocab.py --save_vocab ./vocab.src ./models/sov-1/data/train.src
or
python OpenNMT/opennmt/bin/build_vocab.py --size 32000 --save_vocab ./vocab.src ./models/sov-1/data/train.src
```

And thus, check the train.src file format:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ head ./models/sov-1/data/train.src
<2en> 我々が今日直面している様々な機能不全のなかで - 財政や経済が最初に思いつきますが - 私が一番憂慮しているのは政治的対話の欠乏です我 々が近年の紛争において状況を把握しその根本原因を探り中心人物を理解し彼らと交渉をする能力です
<2en> 我々外交官は国家間の紛争や問題に対処するよう訓練されています
<2en> 貿易や軍縮の国境を越えた問題などに対処しなければなりません
<2en> しかし状況は変わりつつあり近年新しい中心人物達が登場してきました
<2en> 我々は彼らをおおまかに「集団」と呼んでいます彼らはそれぞれ社会 ､ 宗教政治 ､ 経済 ､ 軍事などの利害関係を代表していて
<2en> 我々は彼らの対処に苦慮しています
<2en> そしてこれらの紛争の中心的役割を果たしているのがこれらの国々の中にある様々な利害を代表する集団なのです
<2en> 彼らの行動いかんでは紛争が他国にも急速に広まります
<2en> 政治的な解決が必要となります
<2en> 9 ・ 11テロが起きた後は世界は敵と味方に二分されました
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

Checked under spdata/train.src also:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ head ./models/sov-1/data/spdata/train.src
▁<2 en > ▁我々が 今日 直面している 様々な 機能 不 全 のなかで ▁- ▁ 財政 や 経済 が 最初に 思い つき ますが ▁- ▁私が 一番 憂 慮 しているのは 政治的 対話 の 欠 乏 です 我々が 近年 の 紛争 において 状況 を把握し その 根本 原因 を探 り 中心 人物 を理解し 彼ら と 交渉 をする 能力 です
▁<2 en > ▁ 我々 外交官 は 国家 間の 紛争 や 問題 に対処する よう 訓練 されています
▁<2 en > ▁ 貿易 や 軍 縮 の 国境を越え た 問題 など に対処し なければなりません
▁<2 en > ▁しかし 状況は 変わり つつ あり 近年 新しい 中心 人物 達が 登場 してきました
▁<2 en > ▁我々は 彼らを お お ま かに 「 集団 」 と呼んでいます 彼らは それぞれ 社会 ▁、 ▁ 宗教 政治 ▁、 ▁ 経済 ▁、 ▁ 軍事 などの 利害 関係 を 代表 していて
▁<2 en > ▁我々は 彼らの 対処 に 苦 慮 しています
▁<2 en > ▁そして これらの 紛争 の中心 的 役割を果たし ているの が これらの 国々 の中にある 様々な 利害 を 代表 する 集団 なのです
▁<2 en > ▁彼らの 行動 いか んで は 紛争 が 他国 にも 急速に 広まり ます
▁<2 en > ▁ 政治的な 解決 が必要 となります
▁<2 en > ▁9 ▁ ・ ▁11 テロ が起きた 後 は 世界は 敵 と 味方 に 二 分 されました
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

check opennmt-tf version and I am using the same version with adapt-mnmt repo:  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt/models/sov-1/data$ python
Python 3.6.13 |Anaconda, Inc.| (default, Jun  4 2021, 14:25:59)
[GCC 7.5.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import opennmt as onmt
WARNING:tensorflow:
The TensorFlow contrib module will not be included in TensorFlow 2.0.
For more information, please see:
  * https://github.com/tensorflow/community/blob/master/rfcs/20180907-contrib-sunset.md
  * https://github.com/tensorflow/addons
  * https://github.com/tensorflow/io (for I/O related ops)
If you depend on functionality not listed there, please file an issue.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/decoders/rnn_decoder.py:428: The name tf.nn.rnn_cell.RNNCell is deprecated. Please use tf.compat.v1.nn.rnn_cell.RNNCell instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/utils/hooks.py:15: The name tf.train.SessionRunHook is deprecated. Please use tf.estimator.SessionRunHook instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/optimizers/adafactor.py:34: The name tf.train.Optimizer is deprecated. Please use tf.compat.v1.train.Optimizer instead.

WARNING:tensorflow:From /home/ye/tool/adapt-mnmt/OpenNMT/opennmt/optimizers/multistep_adam.py:36: The name tf.train.AdamOptimizer is deprecated. Please use tf.compat.v1.train.AdamOptimizer instead.

>>> print(onmt.__version__)
1.15.0
>>>
```

I upgraded the opennmt-tf version ...  

```
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$ pip install --upgrade OpenNMT-tf
Requirement already satisfied: OpenNMT-tf in ./OpenNMT (1.15.0)
Collecting OpenNMT-tf
  Downloading OpenNMT_tf-2.26.1-py3-none-any.whl (160 kB)
     |████████████████████████████████| 160 kB 1.8 MB/s
Collecting sacrebleu<2.1,>=1.5.0
  Downloading sacrebleu-2.0.0-py3-none-any.whl (90 kB)
     |████████████████████████████████| 90 kB 1.5 MB/s
Collecting ctranslate2<3,>=2.14.0
  Downloading ctranslate2-2.17.0-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (19.1 MB)
     |████████████████████████████████| 19.1 MB 10.9 MB/s
Requirement already satisfied: pyyaml<7,>=5.3 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from OpenNMT-tf) (6.0)
Collecting tensorflow-addons<0.17,>=0.14
  Downloading tensorflow_addons-0.14.0-cp36-cp36m-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (1.1 MB)
     |████████████████████████████████| 1.1 MB 78.6 MB/s
Requirement already satisfied: pyonmttok<2,>=1.29.0 in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from OpenNMT-tf) (1.31.0)
Collecting rouge<2,>=1.0
  Downloading rouge-1.0.1-py3-none-any.whl (13 kB)
Requirement already satisfied: numpy in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from ctranslate2<3,>=2.14.0->OpenNMT-tf) (1.19.5)
Requirement already satisfied: six in /home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages (from rouge<2,>=1.0->OpenNMT-tf) (1.15.0)
Collecting portalocker
  Downloading portalocker-2.4.0-py2.py3-none-any.whl (16 kB)
Collecting tabulate>=0.8.9
  Downloading tabulate-0.8.9-py3-none-any.whl (25 kB)
Collecting colorama
  Downloading colorama-0.4.4-py2.py3-none-any.whl (16 kB)
Collecting regex
  Using cached regex-2022.4.24-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (749 kB)
Collecting typeguard>=2.7
  Downloading typeguard-2.13.3-py3-none-any.whl (17 kB)
Installing collected packages: typeguard, tabulate, regex, portalocker, colorama, tensorflow-addons, sacrebleu, rouge, ctranslate2, OpenNMT-tf
  Attempting uninstall: rouge
    Found existing installation: rouge 0.3.1
    Uninstalling rouge-0.3.1:
      Successfully uninstalled rouge-0.3.1
  Attempting uninstall: OpenNMT-tf
    Found existing installation: OpenNMT-tf 1.15.0
    Uninstalling OpenNMT-tf-1.15.0:
      Successfully uninstalled OpenNMT-tf-1.15.0
Successfully installed OpenNMT-tf-2.26.1 colorama-0.4.4 ctranslate2-2.17.0 portalocker-2.4.0 regex-2022.4.24 rouge-1.0.1 sacrebleu-2.0.0 tabulate-0.8.9 tensorflow-addons-0.14.0 typeguard-2.13.3
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
```

try again and got different error ...  

```
unigram_model_trainer.cc(505) LOG(INFO) EM sub_iter=1 size=35200 obj=13.6272 num_tokens=4785014 num_tokens/piece=135.938
trainer_interface.cc(615) LOG(INFO) Saving model: /home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel/spm.tgt.model
trainer_interface.cc(626) LOG(INFO) Saving vocabs: /home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel/spm.tgt.vocab
SP MODEL: [/home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel]

APPLYING SP MODEL ON [train] ...

APPLYING SP MODEL ON [dev] ...

APPLYING SP MODEL ON [test] ...
SP DATA: [ /home/ye/tool/adapt-mnmt/models/sov-1/data/spmodel ]

GENERATING VOCABULARY ...
/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/opennmt/version.py:27: UserWarning: OpenNMT-tf supports TensorFlow versions 2.4.0 (included) to 2.9.0 (excluded), but you have TensorFlow 1.15.0 installed. Some features might not work properly.
  UserWarning,
/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/tensorflow_addons/utils/ensure_tf_install.py:67: UserWarning: Tensorflow Addons supports using Python ops for all Tensorflow versions above or equal to 2.4.0 and strictly below 2.7.0 (nightly versions are not supported).
 The versions of TensorFlow you are currently using is 1.15.0 and is not supported.
Some things might work, some things might not.
If you were to encounter a bug, do not file an issue.
If you want to make sure you're using a tested and supported configuration, either change the TensorFlow version or the TensorFlow Addons's version.
You can find the compatibility matrix in TensorFlow Addon's readme:
https://github.com/tensorflow/addons
  UserWarning,
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/bin/build_vocab.py", line 5, in <module>
    from opennmt import constants
  File "/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/opennmt/__init__.py", line 7, in <module>
    from opennmt.config import convert_to_v2_config, load_config, load_model, merge_config
  File "/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/opennmt/config.py", line 11, in <module>
    from opennmt.models import catalog
  File "/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/opennmt/models/__init__.py", line 3, in <module>
    from opennmt.models.catalog import (
  File "/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/opennmt/models/catalog.py", line 4, in <module>
    import tensorflow_addons as tfa
  File "/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/tensorflow_addons/__init__.py", line 21, in <module>
    from tensorflow_addons import activations
  File "/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/tensorflow_addons/activations/__init__.py", line 17, in <module>
    from tensorflow_addons.activations.gelu import gelu
  File "/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/tensorflow_addons/activations/gelu.py", line 19, in <module>
    from tensorflow_addons.utils.types import TensorLike
  File "/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/tensorflow_addons/utils/types.py", line 26, in <module>
    from tensorflow.python.keras.engine import keras_tensor
ImportError: cannot import name 'keras_tensor'
/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/opennmt/version.py:27: UserWarning: OpenNMT-tf supports TensorFlow versions 2.4.0 (included) to 2.9.0 (excluded), but you have TensorFlow 1.15.0 installed. Some features might not work properly.
  UserWarning,
/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/tensorflow_addons/utils/ensure_tf_install.py:67: UserWarning: Tensorflow Addons supports using Python ops for all Tensorflow versions above or equal to 2.4.0 and strictly below 2.7.0 (nightly versions are not supported).
 The versions of TensorFlow you are currently using is 1.15.0 and is not supported.
Some things might work, some things might not.
If you were to encounter a bug, do not file an issue.
If you want to make sure you're using a tested and supported configuration, either change the TensorFlow version or the TensorFlow Addons's version.
You can find the compatibility matrix in TensorFlow Addon's readme:
https://github.com/tensorflow/addons
  UserWarning,
Traceback (most recent call last):
  File "/home/ye/tool/adapt-mnmt/OpenNMT/opennmt/bin/build_vocab.py", line 5, in <module>
    from opennmt import constants
  File "/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/opennmt/__init__.py", line 7, in <module>
    from opennmt.config import convert_to_v2_config, load_config, load_model, merge_config
  File "/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/opennmt/config.py", line 11, in <module>
    from opennmt.models import catalog
  File "/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/opennmt/models/__init__.py", line 3, in <module>
    from opennmt.models.catalog import (
  File "/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/opennmt/models/catalog.py", line 4, in <module>
    import tensorflow_addons as tfa
  File "/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/tensorflow_addons/__init__.py", line 21, in <module>
    from tensorflow_addons import activations
  File "/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/tensorflow_addons/activations/__init__.py", line 17, in <module>
    from tensorflow_addons.activations.gelu import gelu
  File "/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/tensorflow_addons/activations/gelu.py", line 19, in <module>
    from tensorflow_addons.utils.types import TensorLike
  File "/home/ye/anaconda3/envs/adapt-mnmt/lib/python3.6/site-packages/tensorflow_addons/utils/types.py", line 26, in <module>
    from tensorflow.python.keras.engine import keras_tensor
ImportError: cannot import name 'keras_tensor'

real    2m48.715s
user    9m5.286s
sys     0m2.625s
(adapt-mnmt) ye@ye-System-Product-Name:~/tool/adapt-mnmt$
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

# Reference

- https://github.com/OpenNMT/OpenNMT-tf
- https://github.com/surafelml/adapt-mnmt 
- https://github.com/google/sentencepiece/issues/464
- https://github.com/rstudio/rstudio/issues/8278
- https://askubuntu.com/questions/575505/glibcxx-3-4-20-not-found-how-to-fix-this-error
- https://github.com/google/sentencepiece
- https://stackoverflow.com/questions/21530577/fatal-error-python-h-no-such-file-or-directory
- https://stackoverflow.com/questions/59762996/how-to-fix-attributeerror-partially-initialized-module
- https://github.com/tensorflow/nmt/issues/466
