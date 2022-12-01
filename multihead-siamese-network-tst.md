
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

```
(base) ye@ykt-pro:~/tool/multihead-siamese-nets/corpora/QQP$ wc *.csv
  2345806  49373483 314015127 test.csv
   404302   8540953  63399110 train.csv
  2750108  57914436 377414237 total
(base) ye@ykt-pro:~/tool/multihead-siamese-nets/corpora/QQP$
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

Installation of tqdm...  

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ pip install tqdm
Collecting tqdm
  Using cached tqdm-4.64.1-py2.py3-none-any.whl (78 kB)
Installing collected packages: tqdm
Successfully installed tqdm-4.64.1
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$
```

Installation of seaborn ...  

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ pip install seaborn
Collecting seaborn
  Using cached seaborn-0.12.1-py3-none-any.whl (288 kB)
Requirement already satisfied: pandas>=0.25 in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages (from seaborn) (1.5.2)
Requirement already satisfied: numpy>=1.17 in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages (from seaborn) (1.23.5)
Collecting matplotlib!=3.6.1,>=3.1
  Using cached matplotlib-3.6.2-cp38-cp38-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (9.4 MB)
Requirement already satisfied: packaging>=20.0 in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (21.3)
Requirement already satisfied: pyparsing>=2.2.1 in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (3.0.9)
Collecting kiwisolver>=1.0.1
  Using cached kiwisolver-1.4.4-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.whl (1.2 MB)
Collecting contourpy>=1.0.1
  Using cached contourpy-1.0.6-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (295 kB)
Collecting fonttools>=4.22.0
  Using cached fonttools-4.38.0-py3-none-any.whl (965 kB)
Collecting pillow>=6.2.0
  Using cached Pillow-9.3.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.2 MB)
Requirement already satisfied: python-dateutil>=2.7 in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (2.8.2)
Collecting cycler>=0.10
  Using cached cycler-0.11.0-py3-none-any.whl (6.4 kB)
Requirement already satisfied: pytz>=2020.1 in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages (from pandas>=0.25->seaborn) (2022.6)
Requirement already satisfied: six>=1.5 in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages (from python-dateutil>=2.7->matplotlib!=3.6.1,>=3.1->seaborn) (1.16.0)
Installing collected packages: pillow, kiwisolver, fonttools, cycler, contourpy, matplotlib, seaborn
Successfully installed contourpy-1.0.6 cycler-0.11.0 fonttools-4.38.0 kiwisolver-1.4.4 matplotlib-3.6.2 pillow-9.3.0 seaborn-0.12.1
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$
```

Installation of jsonlines ...  

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ pip install jsonlines
Collecting jsonlines
  Downloading jsonlines-3.1.0-py3-none-any.whl (8.6 kB)
Collecting attrs>=19.2.0
  Using cached attrs-22.1.0-py2.py3-none-any.whl (58 kB)
Installing collected packages: attrs, jsonlines
Successfully installed attrs-22.1.0 jsonlines-3.1.0
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$
```

Installation of tflearn ...  

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ pip install tflearn
Collecting tflearn
  Downloading tflearn-0.5.0.tar.gz (107 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 107.3/107.3 kB 1.6 MB/s eta 0:00:00
  Preparing metadata (setup.py) ... done
Requirement already satisfied: numpy in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages (from tflearn) (1.23.5)
Requirement already satisfied: six in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages (from tflearn) (1.16.0)
Requirement already satisfied: Pillow in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages (from tflearn) (9.3.0)
Building wheels for collected packages: tflearn
  Building wheel for tflearn (setup.py) ... done
  Created wheel for tflearn: filename=tflearn-0.5.0-py3-none-any.whl size=127283 sha256=cffe2e504147a8c7e3e14d3bdbd70622847e32fbeaa51db4b64ab185ab1f86cf
  Stored in directory: /home/ye/.cache/pip/wheels/65/9b/15/cb1e6b279c14ed897530d15cfd7da8e3df8a947e593f5cfe59
Successfully built tflearn
Installing collected packages: tflearn
Successfully installed tflearn-0.5.0
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ 
```

## Training CNN model with QQP Dataset 

Got Some Errors because of the version conflict and some are as follows:  

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ time python3 run.py train cnn QQP
2022-11-30 16:22:53.037170: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/torch/install/lib:/usr/local/lib:/usr/local/lib/fst/
2022-11-30 16:22:53.037205: I tensorflow/compiler/xla/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
2022-11-30 16:22:53.870707: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer.so.7'; dlerror: libnvinfer.so.7: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/torch/install/lib:/usr/local/lib:/usr/local/lib/fst/
2022-11-30 16:22:53.870798: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer_plugin.so.7'; dlerror: libnvinfer_plugin.so.7: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/torch/install/lib:/usr/local/lib:/usr/local/lib/fst/
2022-11-30 16:22:53.870814: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Cannot dlopen some TensorRT libraries. If you would like to use Nvidia GPU with TensorRT, please make sure the missing libraries mentioned above are installed properly.
2022-11-30 16:22:54.675238: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcuda.so.1'; dlerror: libcuda.so.1: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/torch/install/lib:/usr/local/lib:/usr/local/lib/fst/
2022-11-30 16:22:54.675267: W tensorflow/compiler/xla/stream_executor/cuda/cuda_driver.cc:265] failed call to cuInit: UNKNOWN ERROR (303)
2022-11-30 16:22:54.675294: I tensorflow/compiler/xla/stream_executor/cuda/cuda_diagnostics.cc:156] kernel driver does not appear to be running on this host (ykt-pro): /proc/driver/nvidia/version does not exist
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages/tensorflow/python/compat/v2_compat.py:107: disable_resource_variables (from tensorflow.python.ops.variable_scope) is deprecated and will be removed in a future version.
Instructions for updating:
non-resource variables are not supported in the long term
Scipy not supported!
Traceback (most recent call last):
  File "run.py", line 17, in <module>
    from utils.other_utils import timer, set_visible_gpu, init_config
  File "/home/ye/tool/multihead-siamese-nets/utils/other_utils.py", line 12, in <module>
    tf.compat.v1.logging.set_verbosity(tf.logging.INFO)
AttributeError: module 'tensorflow' has no attribute 'logging'

real	0m2.347s
user	0m2.268s
sys	0m0.348s
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ time python3 run.py train cnn QQP
2022-11-30 16:23:17.958158: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/torch/install/lib:/usr/local/lib:/usr/local/lib/fst/
2022-11-30 16:23:17.958194: I tensorflow/compiler/xla/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
2022-11-30 16:23:18.744670: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer.so.7'; dlerror: libnvinfer.so.7: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/torch/install/lib:/usr/local/lib:/usr/local/lib/fst/
2022-11-30 16:23:18.744757: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer_plugin.so.7'; dlerror: libnvinfer_plugin.so.7: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/torch/install/lib:/usr/local/lib:/usr/local/lib/fst/
2022-11-30 16:23:18.744770: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Cannot dlopen some TensorRT libraries. If you would like to use Nvidia GPU with TensorRT, please make sure the missing libraries mentioned above are installed properly.
2022-11-30 16:23:19.603050: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcuda.so.1'; dlerror: libcuda.so.1: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/torch/install/lib:/usr/local/lib:/usr/local/lib/fst/
2022-11-30 16:23:19.603079: W tensorflow/compiler/xla/stream_executor/cuda/cuda_driver.cc:265] failed call to cuInit: UNKNOWN ERROR (303)
2022-11-30 16:23:19.603110: I tensorflow/compiler/xla/stream_executor/cuda/cuda_diagnostics.cc:156] kernel driver does not appear to be running on this host (ykt-pro): /proc/driver/nvidia/version does not exist
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages/tensorflow/python/compat/v2_compat.py:107: disable_resource_variables (from tensorflow.python.ops.variable_scope) is deprecated and will be removed in a future version.
Instructions for updating:
non-resource variables are not supported in the long term
Scipy not supported!
INFO:tensorflow:Setting visible GPU to 0
INFO:tensorflow:Reading main configuration.
INFO:tensorflow:Reading configuration for cnn model.
Traceback (most recent call last):
  File "run.py", line 280, in <module>
    main()
  File "run.py", line 274, in main
    train(main_config, model_config, args.model, experiment_name, args.dataset)
  File "run.py", line 43, in train
    train_data = dataset.train_set_pairs()
  File "/home/ye/tool/multihead-siamese-nets/data/qqp.py", line 28, in train_set_pairs
    return self.train[['question1', 'question2']].as_matrix()
  File "/home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages/pandas/core/generic.py", line 5902, in __getattr__
    return object.__getattribute__(self, name)
AttributeError: 'DataFrame' object has no attribute 'as_matrix'

real	0m3.819s
user	0m3.488s
sys	0m0.470s
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ gedit data/qqp.py 
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ time python3 run.py train cnn QQP
2022-11-30 16:26:26.196624: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/torch/install/lib:/usr/local/lib:/usr/local/lib/fst/
2022-11-30 16:26:26.196660: I tensorflow/compiler/xla/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
2022-11-30 16:26:26.956798: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer.so.7'; dlerror: libnvinfer.so.7: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/torch/install/lib:/usr/local/lib:/usr/local/lib/fst/
2022-11-30 16:26:26.956905: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer_plugin.so.7'; dlerror: libnvinfer_plugin.so.7: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/torch/install/lib:/usr/local/lib:/usr/local/lib/fst/
2022-11-30 16:26:26.956924: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Cannot dlopen some TensorRT libraries. If you would like to use Nvidia GPU with TensorRT, please make sure the missing libraries mentioned above are installed properly.
2022-11-30 16:26:27.775398: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcuda.so.1'; dlerror: libcuda.so.1: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/torch/install/lib:/usr/local/lib:/usr/local/lib/fst/
2022-11-30 16:26:27.775425: W tensorflow/compiler/xla/stream_executor/cuda/cuda_driver.cc:265] failed call to cuInit: UNKNOWN ERROR (303)
2022-11-30 16:26:27.775453: I tensorflow/compiler/xla/stream_executor/cuda/cuda_diagnostics.cc:156] kernel driver does not appear to be running on this host (ykt-pro): /proc/driver/nvidia/version does not exist
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages/tensorflow/python/compat/v2_compat.py:107: disable_resource_variables (from tensorflow.python.ops.variable_scope) is deprecated and will be removed in a future version.
Instructions for updating:
non-resource variables are not supported in the long term
Scipy not supported!
INFO:tensorflow:Setting visible GPU to 0
INFO:tensorflow:Reading main configuration.
INFO:tensorflow:Reading configuration for cnn model.
Traceback (most recent call last):
  File "run.py", line 280, in <module>
    main()
  File "run.py", line 274, in main
    train(main_config, model_config, args.model, experiment_name, args.dataset)
  File "run.py", line 43, in train
    train_data = dataset.train_set_pairs()
  File "/home/ye/tool/multihead-siamese-nets/data/qqp.py", line 29, in train_set_pairs
    return self.train[['question1', 'question2']].values()
TypeError: 'numpy.ndarray' object is not callable

real	0m3.582s
user	0m3.428s
sys	0m0.433s
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$
```

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ time python3 run.py train cnn QQP
2022-11-30 16:29:03.554555: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/torch/install/lib:/usr/local/lib:/usr/local/lib/fst/
2022-11-30 16:29:03.554612: I tensorflow/compiler/xla/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
2022-11-30 16:29:04.314476: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer.so.7'; dlerror: libnvinfer.so.7: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/torch/install/lib:/usr/local/lib:/usr/local/lib/fst/
2022-11-30 16:29:04.314580: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer_plugin.so.7'; dlerror: libnvinfer_plugin.so.7: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/torch/install/lib:/usr/local/lib:/usr/local/lib/fst/
2022-11-30 16:29:04.314598: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Cannot dlopen some TensorRT libraries. If you would like to use Nvidia GPU with TensorRT, please make sure the missing libraries mentioned above are installed properly.
2022-11-30 16:29:05.126233: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcuda.so.1'; dlerror: libcuda.so.1: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/torch/install/lib:/usr/local/lib:/usr/local/lib/fst/
2022-11-30 16:29:05.126265: W tensorflow/compiler/xla/stream_executor/cuda/cuda_driver.cc:265] failed call to cuInit: UNKNOWN ERROR (303)
2022-11-30 16:29:05.126304: I tensorflow/compiler/xla/stream_executor/cuda/cuda_diagnostics.cc:156] kernel driver does not appear to be running on this host (ykt-pro): /proc/driver/nvidia/version does not exist
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.8/site-packages/tensorflow/python/compat/v2_compat.py:107: disable_resource_variables (from tensorflow.python.ops.variable_scope) is deprecated and will be removed in a future version.
Instructions for updating:
non-resource variables are not supported in the long term
Scipy not supported!
INFO:tensorflow:Setting visible GPU to 0
INFO:tensorflow:Reading main configuration.
INFO:tensorflow:Reading configuration for cnn model.
Traceback (most recent call last):
  File "run.py", line 280, in <module>
    main()
  File "run.py", line 274, in main
    train(main_config, model_config, args.model, experiment_name, args.dataset)
  File "run.py", line 44, in train
    vectorizer = DatasetVectorizer(
  File "/home/ye/tool/multihead-siamese-nets/utils/data_utils.py", line 24, in __init__
    log('Chosen word embeddings.')
TypeError: 'module' object is not callable

real	0m3.853s
user	0m3.714s
sys	0m0.408s
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$
```

## Creating a New Enviornment with Python 3.6


```
(base) ye@ykt-pro:~/tool/multihead-siamese-nets$ conda env remove --name multihead-siamese

Remove all packages in environment /home/ye/tool/anaconda3/envs/multihead-siamese:

(base) ye@ykt-pro:~/tool/multihead-siamese-nets$ 
```

```
(base) ye@ykt-pro:~/tool/multihead-siamese-nets$ conda create --name multihead-siamese python=3.6
Collecting package metadata (current_repodata.json): done
Solving environment: failed with repodata from current_repodata.json, will retry with next repodata source.
Collecting package metadata (repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.14.0
  latest version: 22.9.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/ye/tool/anaconda3/envs/multihead-siamese

  added / updated specs:
    - python=3.6


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    python-3.6.13              |       h12debd9_1        32.5 MB
    ------------------------------------------------------------
                                           Total:        32.5 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-5.1-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2022.10.11-h06a4308_0
  certifi            pkgs/main/linux-64::certifi-2021.5.30-py36h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.38-h1181459_1
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_2
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-11.2.0-h1234567_1
  libgomp            pkgs/main/linux-64::libgomp-11.2.0-h1234567_1
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-11.2.0-h1234567_1
  ncurses            pkgs/main/linux-64::ncurses-6.3-h5eee18b_3
  openssl            pkgs/main/linux-64::openssl-1.1.1s-h7f8727e_0
  pip                pkgs/main/linux-64::pip-21.2.2-py36h06a4308_0
  python             pkgs/main/linux-64::python-3.6.13-h12debd9_1
  readline           pkgs/main/linux-64::readline-8.2-h5eee18b_0
  setuptools         pkgs/main/linux-64::setuptools-58.0.4-py36h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.40.0-h5082296_0
  tk                 pkgs/main/linux-64::tk-8.6.12-h1ccaba5_0
  wheel              pkgs/main/noarch::wheel-0.37.1-pyhd3eb1b0_0
  xz                 pkgs/main/linux-64::xz-5.2.6-h5eee18b_0
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
python-3.6.13        | 32.5 MB   | ########################################################## | 100% 
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
(base) ye@ykt-pro:~/tool/multihead-siamese-nets$ conda activate multihead-siamese
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$
```

## Installation of Requirements

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ pip install -r requirements/requirements-cpu.txt 
Collecting tqdm==4.15.0
  Using cached tqdm-4.15.0-py2.py3-none-any.whl (46 kB)
Collecting pandas==0.22.0
  Downloading pandas-0.22.0-cp36-cp36m-manylinux1_x86_64.whl (26.2 MB)
     |████████████████████████████████| 26.2 MB 7.4 MB/s 
Collecting tflearn==0.3.2
  Using cached tflearn-0.3.2.tar.gz (98 kB)
Collecting numpy==1.14.2
  Downloading numpy-1.14.2-cp36-cp36m-manylinux1_x86_64.whl (12.2 MB)
     |████████████████████████████████| 12.2 MB 16.1 MB/s 
Collecting tensorflow==1.15.2
  Downloading tensorflow-1.15.2-cp36-cp36m-manylinux2010_x86_64.whl (110.5 MB)
     |████████████████████████████████| 110.5 MB 11.0 MB/s 
Collecting seaborn==0.9.0
  Downloading seaborn-0.9.0-py3-none-any.whl (208 kB)
     |████████████████████████████████| 208 kB 4.6 MB/s 
Collecting jsonlines==1.2.0
  Downloading jsonlines-1.2.0-py2.py3-none-any.whl (7.6 kB)
Requirement already satisfied: python-dateutil>=2 in /home/ye/.local/lib/python3.6/site-packages (from pandas==0.22.0->-r requirements/requirements-cpu.txt (line 2)) (2.8.1)
Requirement already satisfied: pytz>=2011k in /home/ye/.local/lib/python3.6/site-packages (from pandas==0.22.0->-r requirements/requirements-cpu.txt (line 2)) (2020.1)
Requirement already satisfied: six in /home/ye/.local/lib/python3.6/site-packages (from tflearn==0.3.2->-r requirements/requirements-cpu.txt (line 3)) (1.15.0)
Collecting Pillow
  Using cached Pillow-8.4.0-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.1 MB)
Collecting tensorboard<1.16.0,>=1.15.0
  Using cached tensorboard-1.15.0-py3-none-any.whl (3.8 MB)
Collecting termcolor>=1.1.0
  Using cached termcolor-1.1.0-py3-none-any.whl
Collecting absl-py>=0.7.0
  Using cached absl_py-1.3.0-py3-none-any.whl (124 kB)
Requirement already satisfied: wheel>=0.26 in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.6/site-packages (from tensorflow==1.15.2->-r requirements/requirements-cpu.txt (line 5)) (0.37.1)
Collecting grpcio>=1.8.6
  Downloading grpcio-1.48.2-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.6 MB)
     |████████████████████████████████| 4.6 MB 14.7 MB/s 
Collecting astor>=0.6.0
  Using cached astor-0.8.1-py2.py3-none-any.whl (27 kB)
Collecting google-pasta>=0.1.6
  Using cached google_pasta-0.2.0-py3-none-any.whl (57 kB)
Collecting wrapt>=1.11.1
  Downloading wrapt-1.14.1-cp36-cp36m-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (74 kB)
     |████████████████████████████████| 74 kB 2.3 MB/s 
INFO: pip is looking at multiple versions of <Python from Requires-Python> to determine which version is compatible with other requirements. This could take a while.
INFO: pip is looking at multiple versions of numpy to determine which version is compatible with other requirements. This could take a while.
INFO: pip is looking at multiple versions of tflearn to determine which version is compatible with other requirements. This could take a while.
INFO: pip is looking at multiple versions of pandas to determine which version is compatible with other requirements. This could take a while.
INFO: pip is looking at multiple versions of tqdm to determine which version is compatible with other requirements. This could take a while.
ERROR: Cannot install -r requirements/requirements-cpu.txt (line 2), -r requirements/requirements-cpu.txt (line 3), -r requirements/requirements-cpu.txt (line 5) and numpy==1.14.2 because these package versions have conflicting dependencies.

The conflict is caused by:
    The user requested numpy==1.14.2
    pandas 0.22.0 depends on numpy>=1.9.0
    tflearn 0.3.2 depends on numpy
    tensorflow 1.15.2 depends on numpy<2.0 and >=1.16.0

To fix this you could try to:
1. loosen the range of package versions you've specified
2. remove package versions to allow pip attempt to solve the dependency conflict

ERROR: ResolutionImpossible: for help visit https://pip.pypa.io/en/latest/user_guide/#fixing-conflicting-dependencies
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$
```

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ pip install numpy==1.16.0
Collecting numpy==1.16.0
  Using cached numpy-1.16.0-cp36-cp36m-manylinux1_x86_64.whl (17.3 MB)
Installing collected packages: numpy
Successfully installed numpy-1.16.0
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ 
```

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ pip install tensorflow==1.15.2
Collecting tensorflow==1.15.2
  Using cached tensorflow-1.15.2-cp36-cp36m-manylinux2010_x86_64.whl (110.5 MB)
Collecting tensorflow-estimator==1.15.1
  Using cached tensorflow_estimator-1.15.1-py2.py3-none-any.whl (503 kB)
Requirement already satisfied: wheel>=0.26 in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.6/site-packages (from tensorflow==1.15.2) (0.37.1)
Collecting tensorboard<1.16.0,>=1.15.0
  Using cached tensorboard-1.15.0-py3-none-any.whl (3.8 MB)
Requirement already satisfied: numpy<2.0,>=1.16.0 in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.6/site-packages (from tensorflow==1.15.2) (1.16.0)
Collecting keras-applications>=1.0.8
  Using cached Keras_Applications-1.0.8-py3-none-any.whl (50 kB)
Collecting wrapt>=1.11.1
  Using cached wrapt-1.14.1-cp36-cp36m-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (74 kB)
Collecting absl-py>=0.7.0
  Using cached absl_py-1.3.0-py3-none-any.whl (124 kB)
Collecting keras-preprocessing>=1.0.5
  Using cached Keras_Preprocessing-1.1.2-py2.py3-none-any.whl (42 kB)
Collecting grpcio>=1.8.6
  Using cached grpcio-1.48.2-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.6 MB)
Collecting termcolor>=1.1.0
  Using cached termcolor-1.1.0-py3-none-any.whl
Collecting opt-einsum>=2.3.2
  Using cached opt_einsum-3.3.0-py3-none-any.whl (65 kB)
Collecting astor>=0.6.0
  Using cached astor-0.8.1-py2.py3-none-any.whl (27 kB)
Requirement already satisfied: six>=1.10.0 in /home/ye/.local/lib/python3.6/site-packages (from tensorflow==1.15.2) (1.15.0)
Collecting protobuf>=3.6.1
  Downloading protobuf-3.19.6-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.1 MB)
     |████████████████████████████████| 1.1 MB 1.6 MB/s 
Collecting google-pasta>=0.1.6
  Using cached google_pasta-0.2.0-py3-none-any.whl (57 kB)
Collecting gast==0.2.2
  Using cached gast-0.2.2-py3-none-any.whl
Collecting h5py
  Using cached h5py-3.1.0-cp36-cp36m-manylinux1_x86_64.whl (4.0 MB)
Requirement already satisfied: setuptools>=41.0.0 in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.6/site-packages (from tensorboard<1.16.0,>=1.15.0->tensorflow==1.15.2) (58.0.4)
Collecting werkzeug>=0.11.15
  Downloading Werkzeug-2.0.3-py3-none-any.whl (289 kB)
     |████████████████████████████████| 289 kB 14.6 MB/s 
Collecting markdown>=2.6.8
  Downloading Markdown-3.3.7-py3-none-any.whl (97 kB)
     |████████████████████████████████| 97 kB 2.3 MB/s 
Collecting importlib-metadata>=4.4
  Using cached importlib_metadata-4.8.3-py3-none-any.whl (17 kB)
Collecting typing-extensions>=3.6.4
  Using cached typing_extensions-4.1.1-py3-none-any.whl (26 kB)
Collecting zipp>=0.5
  Using cached zipp-3.6.0-py3-none-any.whl (5.3 kB)
Collecting dataclasses
  Using cached dataclasses-0.8-py3-none-any.whl (19 kB)
Collecting cached-property
  Using cached cached_property-1.5.2-py2.py3-none-any.whl (7.6 kB)
Installing collected packages: zipp, typing-extensions, importlib-metadata, dataclasses, cached-property, werkzeug, protobuf, markdown, h5py, grpcio, absl-py, wrapt, termcolor, tensorflow-estimator, tensorboard, opt-einsum, keras-preprocessing, keras-applications, google-pasta, gast, astor, tensorflow
Successfully installed absl-py-1.3.0 astor-0.8.1 cached-property-1.5.2 dataclasses-0.8 gast-0.2.2 google-pasta-0.2.0 grpcio-1.48.2 h5py-3.1.0 importlib-metadata-4.8.3 keras-applications-1.0.8 keras-preprocessing-1.1.2 markdown-3.3.7 opt-einsum-3.3.0 protobuf-3.19.6 tensorboard-1.15.0 tensorflow-1.15.2 tensorflow-estimator-1.15.1 termcolor-1.1.0 typing-extensions-4.1.1 werkzeug-2.0.3 wrapt-1.14.1 zipp-3.6.0
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$
```

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ pip install seaborn==0.9.0
Collecting seaborn==0.9.0
  Using cached seaborn-0.9.0-py3-none-any.whl (208 kB)
Collecting matplotlib>=1.4.3
  Using cached matplotlib-3.3.4-cp36-cp36m-manylinux1_x86_64.whl (11.5 MB)
Collecting pandas>=0.15.2
  Downloading pandas-1.1.5-cp36-cp36m-manylinux1_x86_64.whl (9.5 MB)
     |████████████████████████████████| 9.5 MB 8.0 MB/s 
Collecting scipy>=0.14.0
  Using cached scipy-1.5.4-cp36-cp36m-manylinux1_x86_64.whl (25.9 MB)
Requirement already satisfied: numpy>=1.9.3 in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.6/site-packages (from seaborn==0.9.0) (1.16.0)
Collecting cycler>=0.10
  Using cached cycler-0.11.0-py3-none-any.whl (6.4 kB)
Requirement already satisfied: python-dateutil>=2.1 in /home/ye/.local/lib/python3.6/site-packages (from matplotlib>=1.4.3->seaborn==0.9.0) (2.8.1)
Requirement already satisfied: pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.3 in /home/ye/.local/lib/python3.6/site-packages (from matplotlib>=1.4.3->seaborn==0.9.0) (2.4.7)
Collecting kiwisolver>=1.0.1
  Using cached kiwisolver-1.3.1-cp36-cp36m-manylinux1_x86_64.whl (1.1 MB)
Collecting pillow>=6.2.0
  Using cached Pillow-8.4.0-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.1 MB)
Requirement already satisfied: pytz>=2017.2 in /home/ye/.local/lib/python3.6/site-packages (from pandas>=0.15.2->seaborn==0.9.0) (2020.1)
Requirement already satisfied: six>=1.5 in /home/ye/.local/lib/python3.6/site-packages (from python-dateutil>=2.1->matplotlib>=1.4.3->seaborn==0.9.0) (1.15.0)
Installing collected packages: pillow, kiwisolver, cycler, scipy, pandas, matplotlib, seaborn
Successfully installed cycler-0.11.0 kiwisolver-1.3.1 matplotlib-3.3.4 pandas-1.1.5 pillow-8.4.0 scipy-1.5.4 seaborn-0.9.0
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$
```

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ pip install jsonlines==1.2.0
Collecting jsonlines==1.2.0
  Using cached jsonlines-1.2.0-py2.py3-none-any.whl (7.6 kB)
Requirement already satisfied: six in /home/ye/.local/lib/python3.6/site-packages (from jsonlines==1.2.0) (1.15.0)
Installing collected packages: jsonlines
Successfully installed jsonlines-1.2.0
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$
```

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ pip install tqdm
Collecting tqdm
  Using cached tqdm-4.64.1-py2.py3-none-any.whl (78 kB)
Collecting importlib-resources
  Downloading importlib_resources-5.4.0-py3-none-any.whl (28 kB)
Requirement already satisfied: zipp>=3.1.0 in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.6/site-packages (from importlib-resources->tqdm) (3.6.0)
Installing collected packages: importlib-resources, tqdm
Successfully installed importlib-resources-5.4.0 tqdm-4.64.1
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$
```

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ pip install tflearn
Collecting tflearn
  Using cached tflearn-0.5.0.tar.gz (107 kB)
Requirement already satisfied: numpy in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.6/site-packages (from tflearn) (1.16.0)
Requirement already satisfied: six in /home/ye/.local/lib/python3.6/site-packages (from tflearn) (1.15.0)
Requirement already satisfied: Pillow in /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.6/site-packages (from tflearn) (8.4.0)
Building wheels for collected packages: tflearn
  Building wheel for tflearn (setup.py) ... done
  Created wheel for tflearn: filename=tflearn-0.5.0-py3-none-any.whl size=127299 sha256=98b1aa90e0524e000039a88f51243e0fde4d91edc365b667e5a806ef4554e783
  Stored in directory: /home/ye/.cache/pip/wheels/b4/7f/53/2cc39cdcd4830aa8c962b88318a6d81b334fa00c9ef35b0923
Successfully built tflearn
Installing collected packages: tflearn
Successfully installed tflearn-0.5.0
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ 
```

## Training CNN Model on CPU  

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$ time python3 run.py train cnn QQP
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.6/site-packages/tensorflow_core/python/compat/v2_compat.py:68: disable_resource_variables (from tensorflow.python.ops.variable_scope) is deprecated and will be removed in a future version.
Instructions for updating:
non-resource variables are not supported in the long term
WARNING:tensorflow:From /home/ye/tool/multihead-siamese-nets/utils/data_utils.py:7: The name tf.logging.info is deprecated. Please use tf.compat.v1.logging.info instead.

WARNING:tensorflow:From /home/ye/tool/multihead-siamese-nets/utils/other_utils.py:11: The name tf.logging.set_verbosity is deprecated. Please use tf.compat.v1.logging.set_verbosity instead.

WARNING:tensorflow:From /home/ye/tool/multihead-siamese-nets/utils/other_utils.py:11: The name tf.logging.INFO is deprecated. Please use tf.compat.v1.logging.INFO instead.

INFO:tensorflow:Setting visible GPU to 0
INFO:tensorflow:Reading main configuration.
INFO:tensorflow:Reading configuration for cnn model.
INFO:tensorflow:Chosen word embeddings.
INFO:tensorflow:Maximum sentence length : 237
INFO:tensorflow:Processing sentences with word embeddings...
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.6/site-packages/tflearn/data_utils.py:211: VocabularyProcessor.__init__ (from tensorflow.contrib.learn.python.learn.preprocessing.text) is deprecated and will be removed in a future version.
Instructions for updating:
Please use tensorflow/transform or tf.data.
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.6/site-packages/tensorflow_core/contrib/learn/python/learn/preprocessing/text.py:154: CategoricalVocabulary.__init__ (from tensorflow.contrib.learn.python.learn.preprocessing.categorical_vocabulary) is deprecated and will be removed in a future version.
Instructions for updating:
Please use tensorflow/transform or tf.data.
INFO:tensorflow:Sentences have been successfully processed.
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.6/site-packages/tensorflow_core/contrib/learn/python/learn/preprocessing/text.py:170: tokenizer (from tensorflow.contrib.learn.python.learn.preprocessing.text) is deprecated and will be removed in a future version.
Instructions for updating:
Please use tensorflow/transform or tf.data.
WARNING:tensorflow:From /home/ye/tool/multihead-siamese-nets/models/base_model.py:15: The name tf.placeholder is deprecated. Please use tf.compat.v1.placeholder instead.

WARNING:tensorflow:From /home/ye/tool/multihead-siamese-nets/models/base_model.py:28: The name tf.variable_scope is deprecated. Please use tf.compat.v1.variable_scope instead.

WARNING:tensorflow:From /home/ye/tool/multihead-siamese-nets/models/base_model.py:29: The name tf.get_variable is deprecated. Please use tf.compat.v1.get_variable instead.

WARNING:tensorflow:From /home/ye/tool/multihead-siamese-nets/layers/convolution.py:21: conv2d (from tensorflow.python.layers.convolutional) is deprecated and will be removed in a future version.
Instructions for updating:
Use `tf.keras.layers.Conv2D` instead.
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.6/site-packages/tensorflow_core/python/layers/convolutional.py:424: Layer.apply (from tensorflow.python.keras.engine.base_layer) is deprecated and will be removed in a future version.
Instructions for updating:
Please use `layer.__call__` method instead.
WARNING:tensorflow:From /home/ye/tool/multihead-siamese-nets/layers/convolution.py:27: max_pooling2d (from tensorflow.python.layers.pooling) is deprecated and will be removed in a future version.
Instructions for updating:
Use keras.layers.MaxPooling2D instead.
WARNING:tensorflow:From /home/ye/tool/multihead-siamese-nets/layers/basics.py:32: dropout (from tensorflow.python.layers.core) is deprecated and will be removed in a future version.
Instructions for updating:
Use keras.layers.dropout instead.
WARNING:tensorflow:From /home/ye/tool/multihead-siamese-nets/layers/losses.py:55: The name tf.losses.mean_squared_error is deprecated. Please use tf.compat.v1.losses.mean_squared_error instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.6/site-packages/tensorflow_core/python/ops/losses/losses_impl.py:121: where (from tensorflow.python.ops.array_ops) is deprecated and will be removed in a future version.
Instructions for updating:
Use tf.where in 2.0, which has the same broadcast rule as np.where
WARNING:tensorflow:From /home/ye/tool/multihead-siamese-nets/layers/basics.py:66: The name tf.train.AdamOptimizer is deprecated. Please use tf.compat.v1.train.AdamOptimizer instead.

WARNING:tensorflow:From /home/ye/tool/multihead-siamese-nets/models/base_model.py:42: The name tf.rint is deprecated. Please use tf.math.rint instead.

WARNING:tensorflow:From /home/ye/tool/multihead-siamese-nets/models/base_model.py:43: to_float (from tensorflow.python.ops.math_ops) is deprecated and will be removed in a future version.
Instructions for updating:
Use `tf.cast` instead.
WARNING:tensorflow:From /home/ye/tool/multihead-siamese-nets/models/base_model.py:47: The name tf.summary.scalar is deprecated. Please use tf.compat.v1.summary.scalar instead.

WARNING:tensorflow:From /home/ye/tool/multihead-siamese-nets/models/base_model.py:49: The name tf.summary.merge_all is deprecated. Please use tf.compat.v1.summary.merge_all instead.

WARNING:tensorflow:From /home/ye/tool/multihead-siamese-nets/utils/model_saver.py:9: The name tf.train.Saver is deprecated. Please use tf.compat.v1.train.Saver instead.

WARNING:tensorflow:From run.py:73: The name tf.ConfigProto is deprecated. Please use tf.compat.v1.ConfigProto instead.

WARNING:tensorflow:From run.py:78: The name tf.Session is deprecated. Please use tf.compat.v1.Session instead.

2022-11-30 16:47:10.099051: I tensorflow/core/platform/profile_utils/cpu_utils.cc:94] CPU Frequency: 2893530000 Hz
2022-11-30 16:47:10.099818: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x55bfb332c530 initialized for platform Host (this does not guarantee that XLA will be used). Devices:
2022-11-30 16:47:10.099889: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): Host, Default Version
WARNING:tensorflow:From run.py:80: The name tf.global_variables_initializer is deprecated. Please use tf.compat.v1.global_variables_initializer instead.

WARNING:tensorflow:From /home/ye/tool/multihead-siamese-nets/utils/log_saver.py:12: The name tf.summary.FileWriter is deprecated. Please use tf.compat.v1.summary.FileWriter instead.

INFO:tensorflow:Training model for 10 epochs
Epochs:   0%|                                                                 | 0/10 [00:00<?, ?it/s2022-11-30 16:47:12.962526: W tensorflow/core/framework/cpu_allocator_impl.cc:81] Allocation of 62128128 exceeds 10% of system memory.
2022-11-30 16:47:13.073528: W tensorflow/core/framework/cpu_allocator_impl.cc:81] Allocation of 245296896 exceeds 10% of system memory.
2022-11-30 16:47:13.073534: W tensorflow/core/framework/cpu_allocator_impl.cc:81] Allocation of 245296896 exceeds 10% of system memory.
2022-11-30 16:47:13.140362: W tensorflow/core/framework/cpu_allocator_impl.cc:81] Allocation of 190829600 exceeds 10% of system memory.
2022-11-30 16:47:13.140362: W tensorflow/core/framework/cpu_allocator_impl.cc:81] Allocation of 189212400 exceeds 10% of system memory.
                                                                                                    WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/multihead-siamese/lib/python3.6/site-packages/tensorflow_core/python/training/saver.py:963: remove_checkpoint (from tensorflow.python.training.checkpoint_management) is deprecated and will be removed in a future version.
Instructions for updating:
Use standard file APIs to delete files with this prefix.
Epochs: 100%|████████████████████████████████████████████████████| 10/10 [3:31:57<00:00, 1271.76s/it]
                                                                                                     
real	212m50.967s
user	789m10.450s
sys	14m46.168s
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets$
```

## Model Information

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/logs$ tree
.
└── QQP
    └── cnn_64_MSE
        ├── dev
        │   └── events.out.tfevents.1669801630.ykt-pro
        └── train
            └── events.out.tfevents.1669801630.ykt-pro

4 directories, 2 files
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/logs$
```

## Config Files

for CNN model ...  

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/config/model$ ls
cnn.ini  multihead.ini  rnn.ini
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/config/model$ cat cnn.ini
[PARAMS]
num_filters = 50,50,50
filter_sizes = 2,3,4
dropout_rate = 0.0
```

for Multihead Model ...  

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/config/model$ cat multihead.ini 
[PARAMS]
num_blocks = 2
num_heads = 8
use_residual = False
```

For RNN Model ...  

```
dropout_rate = 0.0(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/config/model$ cat rnn.ini 
[PARAMS]
hidden_size = 128
cell_type = GRU
bidirectional = True(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/config/model$ 
```

```
(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/config$ cat main.ini 
[TRAINING]
num_epochs = 10
batch_size = 512
eval_every = 20
learning_rate = 0.001
checkpoints_to_keep = 5
save_every = 100
log_device_placement = False

[DATA]
logs_path = logs
model_dir = model_dir

[PARAMS]
embedding_size = 64
loss_function = MSE
char_embeddings = False(multihead-siamese) ye@ykt-pro:~/tool/multihead-siamese-nets/config$
```
