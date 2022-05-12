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
