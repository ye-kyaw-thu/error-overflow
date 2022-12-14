# Log of using NCRF++ for Burmese Sentence Tokenization

## git clone

```
(ncrfpp) yekyaw.thu@gpu:~/tool$ git clone https://github.com/jiesutd/NCRFpp
Cloning into 'NCRFpp'...
remote: Enumerating objects: 768, done.
remote: Total 768 (delta 0), reused 0 (delta 0), pack-reused 768
Receiving objects: 100% (768/768), 6.89 MiB | 12.92 MiB/s, done.
Resolving deltas: 100% (484/484), done.
(ncrfpp) yekyaw.thu@gpu:~/tool$
```

checked the cloned files:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ ls
demo.clf.config     demo.train.config  main_parse.py  model   README.md    utils
demo.decode.config  LICENCE            main.py        readme  sample_data
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

## Prepare a New Conda Environment

I create an Anaconda new environment with Python version 3.8 as follows:  

```
(base) yekyaw.thu@gpu:~/tool/NCRFpp$ conda create --name ncrfpp python==3.8
...
...
...
  wheel              pkgs/main/noarch::wheel-0.37.1-pyhd3eb1b0_0
  xz                 pkgs/main/linux-64::xz-5.2.8-h5eee18b_0
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
libedit-3.1.20221030 | 181 KB    | ################################################################################### | 100%
xz-5.2.8             | 429 KB    | ################################################################################### | 100%
sqlite-3.33.0        | 1.1 MB    | ################################################################################### | 100%
libffi-3.2.1         | 48 KB     | ################################################################################### | 100%
python-3.8.0         | 34.9 MB   | ################################################################################### | 100%
pip-22.3.1           | 2.7 MB    | ################################################################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate ncrfpp
#
# To deactivate an active environment, use
#
#     $ conda deactivate

```

When I try to install torch==1.0, I got an error as follows:  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ pip install torch==1.0
ERROR: Could not find a version that satisfies the requirement torch==1.0 (from versions: 1.4.0, 1.5.0, 1.5.1, 1.6.0, 1.7.0, 1.7.1, 1.8.0, 1.8.1, 1.9.0, 1.9.1, 1.10.0, 1.10.1, 1.10.2, 1.11.0, 1.12.0, 1.12.1, 1.13.0)
ERROR: No matching distribution found for torch==1.0
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
```

How about trying with 1.4.0 ?!  

```
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ pip install torch==1.0
ERROR: Could not find a version that satisfies the requirement torch==1.0 (from versions: 1.4.0, 1.5.0, 1.5.1, 1.6.0, 1.7.0, 1.7.1, 1.8.0, 1.8.1, 1.9.0, 1.9.1, 1.10.0, 1.10.1, 1.10.2, 1.11.0, 1.12.0, 1.12.1, 1.13.0)
ERROR: No matching distribution found for torch==1.0
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ pip install --upgrade pip
Requirement already satisfied: pip in /home/yekyaw.thu/.conda/envs/ncrfpp/lib/python3.8/site-packages (22.3.1)
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$ pip install torch==1.4.0
Collecting torch==1.4.0
  Downloading torch-1.4.0-cp38-cp38-manylinux1_x86_64.whl (753.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 753.4/753.4 MB 1.9 MB/s eta 0:00:00
Installing collected packages: torch
Successfully installed torch-1.4.0
(ncrfpp) yekyaw.thu@gpu:~/tool/NCRFpp$
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
