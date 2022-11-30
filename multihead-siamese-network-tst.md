
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
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/corpora$ tree
.
├── ANLI
│   ├── anli_v0.1
│   │   ├── R1
│   │   │   ├── dev.jsonl
│   │   │   ├── test.jsonl
│   │   │   └── train.jsonl
│   │   ├── R2
│   │   │   ├── dev.jsonl
│   │   │   ├── test.jsonl
│   │   │   └── train.jsonl
│   │   ├── R3
│   │   │   ├── dev.jsonl
│   │   │   ├── test.jsonl
│   │   │   └── train.jsonl
│   │   └── README.txt
│   ├── anli_v0.1.zip
│   └── __MACOSX
│       └── anli_v0.1
│           ├── R1
│           ├── R2
│           └── R3
├── QQP
│   ├── qqp_test.tgz
│   ├── qqp_train.tgz
│   ├── test.csv
│   └── train.csv
└── SNLI
    ├── train_snli.tgz
    └── train_snli.txt

12 directories, 17 files
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/corpora$ 
```

Check the QQP Corpus data format:  

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/corpora/QQP$ head train.csv 
"id","qid1","qid2","question1","question2","is_duplicate"
"0","1","2","What is the step by step guide to invest in share market in india?","What is the step by step guide to invest in share market?","0"
"1","3","4","What is the story of Kohinoor (Koh-i-Noor) Diamond?","What would happen if the Indian government stole the Kohinoor (Koh-i-Noor) diamond back?","0"
"2","5","6","How can I increase the speed of my internet connection while using a VPN?","How can Internet speed be increased by hacking through DNS?","0"
"3","7","8","Why am I mentally very lonely? How can I solve it?","Find the remainder when [math]23^{24}[/math] is divided by 24,23?","0"
"4","9","10","Which one dissolve in water quikly sugar, salt, methane and carbon di oxide?","Which fish would survive in salt water?","0"
"5","11","12","Astrology: I am a Capricorn Sun Cap moon and cap rising...what does that say about me?","I'm a triple Capricorn (Sun, Moon and ascendant in Capricorn) What does this say about me?","1"
"6","13","14","Should I buy tiago?","What keeps childern active and far from phone and video games?","0"
"7","15","16","How can I be a good geologist?","What should I do to be a great geologist?","1"
"8","17","18","When do you use シ instead of し?","When do you use ""&"" instead of ""and""?","0"
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/corpora/QQP$
```

check for the test data format:  

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/corpora/QQP$ head test.csv 
"test_id","question1","question2"
0,"How does the Surface Pro himself 4 compare with iPad Pro?","Why did Microsoft choose core m3 and not core i3 home Surface Pro 4?"
1,"Should I have a hair transplant at age 24? How much would it cost?","How much cost does hair transplant require?"
2,"What but is the best way to send money from China to the US?","What you send money to China?"
3,"Which food not emulsifiers?","What foods fibre?"
4,"How ""aberystwyth"" start reading?","How their can I start reading?"
5,"How are the two wheeler insurance from Bharti Axa insurance?","I admire I am considering of buying insurance from them"
6,"How can I reduce my belly fat through a diet?","How can I reduce my lower belly fat in one month?"
7,"By scrapping the 500 and 1000 rupee notes, how is RBI planning to fight against issue black money?","How will the recent move to declare 500 and 1000 denomination lewin illegal will curb black money?"
8,"What are the how best books of all time?","What are some of the military history books of all time?"
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/corpora/QQP$
```

## Try with CPU

Installation of requirements ...  

Got error and I install manually:  

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ pip install pandas
Collecting pandas
  Downloading pandas-1.5.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (12.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 12.2/12.2 MB 12.8 MB/s eta 0:00:00
Collecting pytz>=2020.1
  Downloading pytz-2022.6-py2.py3-none-any.whl (498 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 498.1/498.1 kB 8.3 MB/s eta 0:00:00
Collecting python-dateutil>=2.8.1
  Using cached python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
Collecting numpy>=1.20.3
  Downloading numpy-1.23.5-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (17.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 17.1/17.1 MB 12.3 MB/s eta 0:00:00
Collecting six>=1.5
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Installing collected packages: pytz, six, numpy, python-dateutil, pandas
Successfully installed numpy-1.23.5 pandas-1.5.2 python-dateutil-2.8.2 pytz-2022.6 six-1.16.0
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$
```

comment out Panda and try again ...  

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ pip install -r requirements/requirements-cpu.txt 
Collecting tqdm==4.15.0
  Using cached tqdm-4.15.0-py2.py3-none-any.whl (46 kB)
Collecting tflearn==0.3.2
  Downloading tflearn-0.3.2.tar.gz (98 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 98.6/98.6 kB 1.4 MB/s eta 0:00:00
  Preparing metadata (setup.py) ... done
Collecting numpy==1.14.2
  Downloading numpy-1.14.2.zip (4.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.9/4.9 MB 6.0 MB/s eta 0:00:00
  Preparing metadata (setup.py) ... done
ERROR: Could not find a version that satisfies the requirement tensorflow==1.15.2 (from versions: 2.2.0, 2.2.1, 2.2.2, 2.2.3, 2.3.0, 2.3.1, 2.3.2, 2.3.3, 2.3.4, 2.4.0, 2.4.1, 2.4.2, 2.4.3, 2.4.4, 2.5.0, 2.5.1, 2.5.2, 2.5.3, 2.6.0rc0, 2.6.0rc1, 2.6.0rc2, 2.6.0, 2.6.1, 2.6.2, 2.6.3, 2.6.4, 2.6.5, 2.7.0rc0, 2.7.0rc1, 2.7.0, 2.7.1, 2.7.2, 2.7.3, 2.7.4, 2.8.0rc0, 2.8.0rc1, 2.8.0, 2.8.1, 2.8.2, 2.8.3, 2.8.4, 2.9.0rc0, 2.9.0rc1, 2.9.0rc2, 2.9.0, 2.9.1, 2.9.2, 2.9.3, 2.10.0rc0, 2.10.0rc1, 2.10.0rc2, 2.10.0rc3, 2.10.0, 2.10.1, 2.11.0rc0, 2.11.0rc1, 2.11.0rc2, 2.11.0)
ERROR: No matching distribution found for tensorflow==1.15.2
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$
```

As you can seen above, tensorflow version 1.15.2 installation error ...   
I installed default for this env ...  

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ cat ./requirements/requirements-cpu.txt 
tqdm==4.15.0
# pandas==0.22.0
tflearn==0.3.2
numpy==1.14.2
tensorflow==1.15.2
seaborn==0.9.0
jsonlines==1.2.0
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ pip install numpy
Requirement already satisfied: numpy in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages (1.23.5)
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ pip install tensorflow
Collecting tensorflow
  Downloading tensorflow-2.11.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (588.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 588.3/588.3 MB 2.0 MB/s eta 0:00:00
Collecting termcolor>=1.1.0
  Downloading termcolor-2.1.1-py3-none-any.whl (6.2 kB)
Collecting libclang>=13.0.0
  Using cached libclang-14.0.6-py2.py3-none-manylinux2010_x86_64.whl (14.1 MB)
Collecting astunparse>=1.6.0
  Using cached astunparse-1.6.3-py2.py3-none-any.whl (12 kB)
Collecting absl-py>=1.0.0
  Downloading absl_py-1.3.0-py3-none-any.whl (124 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 124.6/124.6 kB 6.2 MB/s eta 0:00:00
Collecting wrapt>=1.11.0
  Downloading wrapt-1.14.1-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (81 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 81.0/81.0 kB 3.7 MB/s eta 0:00:00
Collecting google-pasta>=0.1.1
  Using cached google_pasta-0.2.0-py3-none-any.whl (57 kB)
Requirement already satisfied: six>=1.12.0 in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages (from tensorflow) (1.16.0)
Collecting gast<=0.4.0,>=0.2.1
  Using cached gast-0.4.0-py3-none-any.whl (9.8 kB)
Collecting tensorflow-estimator<2.12,>=2.11.0
  Downloading tensorflow_estimator-2.11.0-py2.py3-none-any.whl (439 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 439.2/439.2 kB 8.3 MB/s eta 0:00:00
Collecting tensorboard<2.12,>=2.11
  Downloading tensorboard-2.11.0-py3-none-any.whl (6.0 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 6.0/6.0 MB 11.7 MB/s eta 0:00:00
Collecting keras<2.12,>=2.11.0
  Downloading keras-2.11.0-py2.py3-none-any.whl (1.7 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.7/1.7 MB 11.0 MB/s eta 0:00:00
Collecting protobuf<3.20,>=3.9.2
  Downloading protobuf-3.19.6-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.1/1.1 MB 6.1 MB/s eta 0:00:00
Requirement already satisfied: setuptools in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages (from tensorflow) (65.5.0)
Collecting h5py>=2.9.0
  Downloading h5py-3.7.0-cp38-cp38-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (4.5 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.5/4.5 MB 12.3 MB/s eta 0:00:00
Requirement already satisfied: numpy>=1.20 in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages (from tensorflow) (1.23.5)
Collecting opt-einsum>=2.3.2
  Using cached opt_einsum-3.3.0-py3-none-any.whl (65 kB)
Collecting flatbuffers>=2.0
  Downloading flatbuffers-22.11.23-py2.py3-none-any.whl (26 kB)
Collecting packaging
  Using cached packaging-21.3-py3-none-any.whl (40 kB)
Collecting tensorflow-io-gcs-filesystem>=0.23.1
  Downloading tensorflow_io_gcs_filesystem-0.28.0-cp38-cp38-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (2.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.4/2.4 MB 10.7 MB/s eta 0:00:00
Collecting typing-extensions>=3.6.6
  Using cached typing_extensions-4.4.0-py3-none-any.whl (26 kB)
Collecting grpcio<2.0,>=1.24.3
  Downloading grpcio-1.51.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.8 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.8/4.8 MB 11.0 MB/s eta 0:00:00
Requirement already satisfied: wheel<1.0,>=0.23.0 in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages (from astunparse>=1.6.0->tensorflow) (0.37.1)
Collecting google-auth-oauthlib<0.5,>=0.4.1
  Using cached google_auth_oauthlib-0.4.6-py2.py3-none-any.whl (18 kB)
Collecting requests<3,>=2.21.0
  Using cached requests-2.28.1-py3-none-any.whl (62 kB)
Collecting tensorboard-data-server<0.7.0,>=0.6.0
  Using cached tensorboard_data_server-0.6.1-py3-none-manylinux2010_x86_64.whl (4.9 MB)
Collecting tensorboard-plugin-wit>=1.6.0
  Using cached tensorboard_plugin_wit-1.8.1-py3-none-any.whl (781 kB)
Collecting werkzeug>=1.0.1
  Using cached Werkzeug-2.2.2-py3-none-any.whl (232 kB)
Collecting markdown>=2.6.8
  Using cached Markdown-3.4.1-py3-none-any.whl (93 kB)
Collecting google-auth<3,>=1.6.3
  Downloading google_auth-2.14.1-py2.py3-none-any.whl (175 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 175.4/175.4 kB 8.1 MB/s eta 0:00:00
Collecting pyparsing!=3.0.5,>=2.0.2
  Using cached pyparsing-3.0.9-py3-none-any.whl (98 kB)
Collecting rsa<5,>=3.1.4
  Downloading rsa-4.9-py3-none-any.whl (34 kB)
Collecting cachetools<6.0,>=2.0.0
  Downloading cachetools-5.2.0-py3-none-any.whl (9.3 kB)
Collecting pyasn1-modules>=0.2.1
  Using cached pyasn1_modules-0.2.8-py2.py3-none-any.whl (155 kB)
Collecting requests-oauthlib>=0.7.0
  Using cached requests_oauthlib-1.3.1-py2.py3-none-any.whl (23 kB)
Collecting importlib-metadata>=4.4
  Downloading importlib_metadata-5.1.0-py3-none-any.whl (21 kB)
Collecting charset-normalizer<3,>=2
  Using cached charset_normalizer-2.1.1-py3-none-any.whl (39 kB)
Collecting idna<4,>=2.5
  Using cached idna-3.4-py3-none-any.whl (61 kB)
Collecting urllib3<1.27,>=1.21.1
  Downloading urllib3-1.26.13-py2.py3-none-any.whl (140 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 140.6/140.6 kB 7.8 MB/s eta 0:00:00
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard<2.12,>=2.11->tensorflow) (2022.9.24)
Collecting MarkupSafe>=2.1.1
  Downloading MarkupSafe-2.1.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (25 kB)
Collecting zipp>=0.5
  Downloading zipp-3.11.0-py3-none-any.whl (6.6 kB)
Collecting pyasn1<0.5.0,>=0.4.6
  Using cached pyasn1-0.4.8-py2.py3-none-any.whl (77 kB)
Collecting oauthlib>=3.0.0
  Downloading oauthlib-3.2.2-py3-none-any.whl (151 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 151.7/151.7 kB 6.0 MB/s eta 0:00:00
Installing collected packages: tensorboard-plugin-wit, pyasn1, libclang, flatbuffers, zipp, wrapt, urllib3, typing-extensions, termcolor, tensorflow-io-gcs-filesystem, tensorflow-estimator, tensorboard-data-server, rsa, pyparsing, pyasn1-modules, protobuf, opt-einsum, oauthlib, MarkupSafe, keras, idna, h5py, grpcio, google-pasta, gast, charset-normalizer, cachetools, astunparse, absl-py, werkzeug, requests, packaging, importlib-metadata, google-auth, requests-oauthlib, markdown, google-auth-oauthlib, tensorboard, tensorflow
Successfully installed MarkupSafe-2.1.1 absl-py-1.3.0 astunparse-1.6.3 cachetools-5.2.0 charset-normalizer-2.1.1 flatbuffers-22.11.23 gast-0.4.0 google-auth-2.14.1 google-auth-oauthlib-0.4.6 google-pasta-0.2.0 grpcio-1.51.1 h5py-3.7.0 idna-3.4 importlib-metadata-5.1.0 keras-2.11.0 libclang-14.0.6 markdown-3.4.1 oauthlib-3.2.2 opt-einsum-3.3.0 packaging-21.3 protobuf-3.19.6 pyasn1-0.4.8 pyasn1-modules-0.2.8 pyparsing-3.0.9 requests-2.28.1 requests-oauthlib-1.3.1 rsa-4.9 tensorboard-2.11.0 tensorboard-data-server-0.6.1 tensorboard-plugin-wit-1.8.1 tensorflow-2.11.0 tensorflow-estimator-2.11.0 tensorflow-io-gcs-filesystem-0.28.0 termcolor-2.1.1 typing-extensions-4.4.0 urllib3-1.26.13 werkzeug-2.2.2 wrapt-1.14.1 zipp-3.11.0
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$
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
