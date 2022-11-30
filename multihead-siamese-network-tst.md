
# Multihead Siamese Network Testing

## Creating a New Conda Environment

```
(base) ye@ykt-pro:~/exp$ conda create --name multihead-siamese python=3.8
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.14.0
  latest version: 22.9.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/ye/tool/anaconda3/envs/multihead-siamese

  added / updated specs:
    - python=3.8


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    libffi-3.4.2               |       h6a678d5_6         136 KB
    python-3.8.15              |       h7a1cb2a_2        20.1 MB
    sqlite-3.40.0              |       h5082296_0         1.2 MB
    ------------------------------------------------------------
                                           Total:        21.4 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-5.1-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2022.10.11-h06a4308_0
  certifi            pkgs/main/linux-64::certifi-2022.9.24-py38h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.38-h1181459_1
  libffi             pkgs/main/linux-64::libffi-3.4.2-h6a678d5_6
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-11.2.0-h1234567_1
  libgomp            pkgs/main/linux-64::libgomp-11.2.0-h1234567_1
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-11.2.0-h1234567_1
  ncurses            pkgs/main/linux-64::ncurses-6.3-h5eee18b_3
  openssl            pkgs/main/linux-64::openssl-1.1.1s-h7f8727e_0
  pip                pkgs/main/linux-64::pip-22.2.2-py38h06a4308_0
  python             pkgs/main/linux-64::python-3.8.15-h7a1cb2a_2
  readline           pkgs/main/linux-64::readline-8.2-h5eee18b_0
  setuptools         pkgs/main/linux-64::setuptools-65.5.0-py38h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.40.0-h5082296_0
  tk                 pkgs/main/linux-64::tk-8.6.12-h1ccaba5_0
  wheel              pkgs/main/noarch::wheel-0.37.1-pyhd3eb1b0_0
  xz                 pkgs/main/linux-64::xz-5.2.6-h5eee18b_0
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
sqlite-3.40.0        | 1.2 MB    | ########################################################## | 100% 
python-3.8.15        | 20.1 MB   | ########################################################## | 100% 
libffi-3.4.2         | 136 KB    | ########################################################## | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate multihead-siamese
#
# To deactivate an active environment, use
#
#     $ conda deactivate

Retrieving notices: ...working... done
(base) ye@ykt-pro:~/exp$ conda activate multihead-siamese
```

## Git Clone

```
(multihead-siamese) ye@ykt-pro:~/exp$ cd ..
(multihead-siamese) ye@ykt-pro:~$ cd tool
(multihead-siamese) ye@ykt-pro:~/tool$ git clone https://github.com/tlatkowski/multihead-siamese-netsCloning into 'multihead-siamese-nets'...
remote: Enumerating objects: 982, done.
remote: Counting objects: 100% (21/21), done.
remote: Compressing objects: 100% (21/21), done.
remote: Total 982 (delta 4), reused 3 (delta 0), pack-reused 961
Receiving objects: 100% (982/982), 1.47 MiB | 4.89 MiB/s, done.
Resolving deltas: 100% (557/557), done.
(multihead-siamese) ye@ykt-pro:~/tool$ cd multihead-siamese-nets/
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ ls
bin    config  gui_demo.py  LICENSE  pics       requirements  tests
colab  data    layers       models   README.md  run.py        utils
```

## Data Downloading

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ cd bin
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/bin$ chmod a+x prepare_data.sh 
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/bin$ ls
prepare_data.sh
```

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/bin$ ./prepare_data.sh 
--2022-11-30 15:51:05--  https://drive.google.com/uc?export=download&id=1wkAjMu-Pqnm1l-92M7UEp5YEtT1cFgVz
Resolving drive.google.com (drive.google.com)... 74.125.24.138, 74.125.24.113, 74.125.24.102, ...
Connecting to drive.google.com (drive.google.com)|74.125.24.138|:443... connected.
HTTP request sent, awaiting response... 303 See Other
Location: https://doc-04-8o-docs.googleusercontent.com/docs/securesc/ha0ro937gcuc7l7deffksulhg5h7mbp1/793u61jbi7s647djbmdkhuhkm68trbe8/1669798200000/05563007606908372189/*/1wkAjMu-Pqnm1l-92M7UEp5YEtT1cFgVz?e=download&uuid=128b017c-0a42-4d7c-abc1-82476a4216cb [following]
Warning: wildcards not supported in HTTP.
--2022-11-30 15:51:13--  https://doc-04-8o-docs.googleusercontent.com/docs/securesc/ha0ro937gcuc7l7deffksulhg5h7mbp1/793u61jbi7s647djbmdkhuhkm68trbe8/1669798200000/05563007606908372189/*/1wkAjMu-Pqnm1l-92M7UEp5YEtT1cFgVz?e=download&uuid=128b017c-0a42-4d7c-abc1-82476a4216cb
Resolving doc-04-8o-docs.googleusercontent.com (doc-04-8o-docs.googleusercontent.com)... 142.250.4.132, 2404:6800:4003:c06::84
Connecting to doc-04-8o-docs.googleusercontent.com (doc-04-8o-docs.googleusercontent.com)|142.250.4.132|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 7735242 (7.4M) [application/x-compressed-tar]
Saving to: ‘SNLI/train_snli.tgz’

SNLI/train_snli.tgz       100%[==================================>]   7.38M  10.2MB/s    in 0.7s    

2022-11-30 15:51:15 (10.2 MB/s) - ‘SNLI/train_snli.tgz’ saved [7735242/7735242]

--2022-11-30 15:51:15--  https://drive.google.com/uc?export=download&id=1dnck-CCIyx8y2xg1vwFzcwXieZJB7ERC
Resolving drive.google.com (drive.google.com)... 74.125.24.101, 74.125.24.139, 74.125.24.100, ...
Connecting to drive.google.com (drive.google.com)|74.125.24.101|:443... connected.
HTTP request sent, awaiting response... 303 See Other
Location: https://doc-0o-8o-docs.googleusercontent.com/docs/securesc/ha0ro937gcuc7l7deffksulhg5h7mbp1/oghj7n477jc5chmfb3o47ojc594knpa0/1669798275000/05563007606908372189/*/1dnck-CCIyx8y2xg1vwFzcwXieZJB7ERC?e=download&uuid=f99efeed-eea9-4cd4-9a2f-b977b0f12084 [following]
Warning: wildcards not supported in HTTP.
--2022-11-30 15:51:19--  https://doc-0o-8o-docs.googleusercontent.com/docs/securesc/ha0ro937gcuc7l7deffksulhg5h7mbp1/oghj7n477jc5chmfb3o47ojc594knpa0/1669798275000/05563007606908372189/*/1dnck-CCIyx8y2xg1vwFzcwXieZJB7ERC?e=download&uuid=f99efeed-eea9-4cd4-9a2f-b977b0f12084
Resolving doc-0o-8o-docs.googleusercontent.com (doc-0o-8o-docs.googleusercontent.com)... 142.250.4.132, 2404:6800:4003:c06::84
Connecting to doc-0o-8o-docs.googleusercontent.com (doc-0o-8o-docs.googleusercontent.com)|142.250.4.132|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 22176174 (21M) [application/x-gtar]
Saving to: ‘QQP/qqp_train.tgz’

QQP/qqp_train.tgz         100%[==================================>]  21.15M  10.9MB/s    in 1.9s    

2022-11-30 15:51:22 (10.9 MB/s) - ‘QQP/qqp_train.tgz’ saved [22176174/22176174]

--2022-11-30 15:51:22--  https://docs.google.com/uc?export=download&confirm=t&id=1XD-HxzUCTHrzhfvIXOlgqN_MWiiAqM8h
Resolving docs.google.com (docs.google.com)... 74.125.24.100, 74.125.24.113, 74.125.24.139, ...
Connecting to docs.google.com (docs.google.com)|74.125.24.100|:443... connected.
HTTP request sent, awaiting response... 303 See Other
Location: https://doc-0g-8o-docs.googleusercontent.com/docs/securesc/ha0ro937gcuc7l7deffksulhg5h7mbp1/e778bg5b85c2m02o8752m9918r6666qp/1669798275000/05563007606908372189/*/1XD-HxzUCTHrzhfvIXOlgqN_MWiiAqM8h?e=download&uuid=85020c62-7d07-40ee-b393-ce77b5e85f15 [following]
Warning: wildcards not supported in HTTP.
--2022-11-30 15:51:23--  https://doc-0g-8o-docs.googleusercontent.com/docs/securesc/ha0ro937gcuc7l7deffksulhg5h7mbp1/e778bg5b85c2m02o8752m9918r6666qp/1669798275000/05563007606908372189/*/1XD-HxzUCTHrzhfvIXOlgqN_MWiiAqM8h?e=download&uuid=85020c62-7d07-40ee-b393-ce77b5e85f15
Resolving doc-0g-8o-docs.googleusercontent.com (doc-0g-8o-docs.googleusercontent.com)... 142.250.4.132, 2404:6800:4003:c06::84
Connecting to doc-0g-8o-docs.googleusercontent.com (doc-0g-8o-docs.googleusercontent.com)|142.250.4.132|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 117792766 (112M) [application/x-gtar]
Saving to: ‘QQP/qqp_test.tgz’

QQP/qqp_test.tgz          100%[==================================>] 112.33M  10.9MB/s    in 12s     

2022-11-30 15:51:35 (9.76 MB/s) - ‘QQP/qqp_test.tgz’ saved [117792766/117792766]

--2022-11-30 15:51:35--  https://dl.fbaipublicfiles.com/anli/anli_v0.1.zip
Resolving dl.fbaipublicfiles.com (dl.fbaipublicfiles.com)... 172.67.9.4, 104.22.75.142, 104.22.74.142, ...
Connecting to dl.fbaipublicfiles.com (dl.fbaipublicfiles.com)|172.67.9.4|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 18621352 (18M) [application/zip]
Saving to: ‘ANLI/anli_v0.1.zip’

ANLI/anli_v0.1.zip        100%[==================================>]  17.76M  6.28MB/s    in 2.8s    

2022-11-30 15:51:39 (6.28 MB/s) - ‘ANLI/anli_v0.1.zip’ saved [18621352/18621352]

train_snli.txt
train.csv
test.csv
Archive:  ANLI/anli_v0.1.zip
   creating: ANLI/anli_v0.1/
   creating: ANLI/anli_v0.1/R1/
  inflating: ANLI/anli_v0.1/R1/train.jsonl  
   creating: ANLI/__MACOSX/
   creating: ANLI/__MACOSX/anli_v0.1/
   creating: ANLI/__MACOSX/anli_v0.1/R1/
  inflating: ANLI/__MACOSX/anli_v0.1/R1/._train.jsonl  
  inflating: ANLI/anli_v0.1/R1/test.jsonl  
  inflating: ANLI/__MACOSX/anli_v0.1/R1/._test.jsonl  
  inflating: ANLI/anli_v0.1/R1/dev.jsonl  
  inflating: ANLI/__MACOSX/anli_v0.1/R1/._dev.jsonl  
  inflating: ANLI/__MACOSX/anli_v0.1/._R1  
  inflating: ANLI/anli_v0.1/README.txt  
  inflating: ANLI/__MACOSX/anli_v0.1/._README.txt  
   creating: ANLI/anli_v0.1/R3/
  inflating: ANLI/anli_v0.1/R3/train.jsonl  
   creating: ANLI/__MACOSX/anli_v0.1/R3/
  inflating: ANLI/__MACOSX/anli_v0.1/R3/._train.jsonl  
  inflating: ANLI/anli_v0.1/R3/test.jsonl  
  inflating: ANLI/__MACOSX/anli_v0.1/R3/._test.jsonl  
  inflating: ANLI/anli_v0.1/R3/dev.jsonl  
  inflating: ANLI/__MACOSX/anli_v0.1/R3/._dev.jsonl  
  inflating: ANLI/__MACOSX/anli_v0.1/._R3  
   creating: ANLI/anli_v0.1/R2/
  inflating: ANLI/anli_v0.1/R2/train.jsonl  
   creating: ANLI/__MACOSX/anli_v0.1/R2/
  inflating: ANLI/__MACOSX/anli_v0.1/R2/._train.jsonl  
  inflating: ANLI/anli_v0.1/R2/test.jsonl  
  inflating: ANLI/__MACOSX/anli_v0.1/R2/._test.jsonl  
  inflating: ANLI/anli_v0.1/R2/dev.jsonl  
  inflating: ANLI/__MACOSX/anli_v0.1/R2/._dev.jsonl  
  inflating: ANLI/__MACOSX/anli_v0.1/._R2  
  inflating: ANLI/__MACOSX/._anli_v0.1  
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/bin$ 
```

## Check Data Formats

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

```

```

```

```

```

```

```
