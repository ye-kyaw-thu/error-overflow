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
