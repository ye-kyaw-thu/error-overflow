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

```

```

```

```


# Reference

- https://github.com/OpenNMT/OpenNMT-tf
- https://github.com/surafelml/adapt-mnmt 
- https://github.com/google/sentencepiece/issues/464
- 

















































