# Testing with TabPFN

## Create a New Conda Environment

```
conda create --name tabPFN python=3.7
...
...
...
Downloading and Extracting Packages
pip-22.2.2           | 2.3 MB    | ######################################### | 100% 
zlib-1.2.13          | 103 KB    | ######################################### | 100% 
python-3.7.13        | 40.7 MB   | ######################################### | 100% 
setuptools-63.4.1    | 1.1 MB    | ######################################### | 100% 
readline-8.2         | 357 KB    | ######################################### | 100% 
certifi-2022.9.24    | 154 KB    | ######################################### | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate tabPFN
#
# To deactivate an active environment, use
#
#     $ conda deactivate

Retrieving notices: ...working... done
```

## Entering into the New Environment

conda activate tabPFN

## Install TabPFN

(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/data/test/neg$ pip install tabpfn
Collecting tabpfn
  Downloading tabpfn-0.1.3-py3-none-any.whl (136 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 136.1/136.1 kB 1.7 MB/s eta 0:00:00
Collecting configspace>=0.4.21
  Downloading ConfigSpace-0.6.0-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.9/4.9 MB 3.0 MB/s eta 0:00:00
Collecting seaborn>=0.11.2
  Downloading seaborn-0.12.1-py3-none-any.whl (288 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 288.2/288.2 kB 3.7 MB/s eta 0:00:00
Collecting openml>=0.12.2
  Downloading openml-0.12.2.tar.gz (119 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 119.9/119.9 kB 9.2 MB/s eta 0:00:00
  Preparing metadata (setup.py) ... done
Collecting hyperopt>=0.2.5
  Downloading hyperopt-0.2.7-py2.py3-none-any.whl (1.6 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.6/1.6 MB 5.9 MB/s eta 0:00:00
Collecting torch>=1.9.0
  Downloading torch-1.12.1-cp37-cp37m-manylinux1_x86_64.whl (776.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 776.3/776.3 MB 1.0 MB/s eta 0:00:00
Collecting numpy>=1.21.2
  Using cached numpy-1.21.6-cp37-cp37m-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (15.7 MB)
Collecting scikit-learn>=0.24.2
  Downloading scikit_learn-1.0.2-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (24.8 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 24.8/24.8 MB 2.5 MB/s eta 0:00:00
Collecting gpytorch>=1.5.0
  Downloading gpytorch-1.8.1-py2.py3-none-any.whl (361 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 361.8/361.8 kB 4.4 MB/s eta 0:00:00
Collecting pyyaml>=5.4.1
  Downloading PyYAML-6.0-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_12_x86_64.manylinux2010_x86_64.whl (596 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 596.3/596.3 kB 5.8 MB/s eta 0:00:00
Collecting tqdm>=4.62.1
  Using cached tqdm-4.64.1-py2.py3-none-any.whl (78 kB)
Collecting cython
  Downloading Cython-0.29.32-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_24_x86_64.whl (1.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.9/1.9 MB 4.8 MB/s eta 0:00:00
Collecting pyparsing
  Using cached pyparsing-3.0.9-py3-none-any.whl (98 kB)
Collecting scipy
  Using cached scipy-1.7.3-cp37-cp37m-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (38.1 MB)
Collecting typing-extensions
  Using cached typing_extensions-4.4.0-py3-none-any.whl (26 kB)
Collecting networkx>=2.2
  Downloading networkx-2.6.3-py3-none-any.whl (1.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.9/1.9 MB 4.9 MB/s eta 0:00:00
Collecting py4j
  Downloading py4j-0.10.9.7-py2.py3-none-any.whl (200 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 200.5/200.5 kB 3.5 MB/s eta 0:00:00
Collecting future
  Using cached future-0.18.2-py3-none-any.whl
Collecting six
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Collecting cloudpickle
  Downloading cloudpickle-2.2.0-py3-none-any.whl (25 kB)
Collecting liac-arff>=2.4.0
  Downloading liac-arff-2.5.0.tar.gz (13 kB)
  Preparing metadata (setup.py) ... done
Collecting xmltodict
  Downloading xmltodict-0.13.0-py2.py3-none-any.whl (10.0 kB)
Collecting requests
  Using cached requests-2.28.1-py3-none-any.whl (62 kB)
Collecting python-dateutil
  Using cached python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
Collecting pandas>=1.0.0
  Downloading pandas-1.3.5-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (11.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 11.3/11.3 MB 2.6 MB/s eta 0:00:00
Collecting minio
  Downloading minio-7.1.12-py3-none-any.whl (76 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 76.2/76.2 kB 1.8 MB/s eta 0:00:00
Collecting pyarrow
  Downloading pyarrow-9.0.0-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (35.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 35.3/35.3 MB 2.5 MB/s eta 0:00:00
Collecting threadpoolctl>=2.0.0
  Using cached threadpoolctl-3.1.0-py3-none-any.whl (14 kB)
Collecting joblib>=0.11
  Using cached joblib-1.2.0-py3-none-any.whl (297 kB)
Collecting matplotlib!=3.6.1,>=3.1
  Downloading matplotlib-3.5.3-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.whl (11.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 11.2/11.2 MB 2.7 MB/s eta 0:00:00
Collecting kiwisolver>=1.0.1
  Downloading kiwisolver-1.4.4-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.whl (1.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.1/1.1 MB 4.8 MB/s eta 0:00:00
Collecting fonttools>=4.22.0
  Downloading fonttools-4.38.0-py3-none-any.whl (965 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 965.4/965.4 kB 4.6 MB/s eta 0:00:00
Collecting packaging>=20.0
  Using cached packaging-21.3-py3-none-any.whl (40 kB)
Collecting pillow>=6.2.0
  Downloading Pillow-9.2.0-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.1/3.1 MB 3.6 MB/s eta 0:00:00
Collecting cycler>=0.10
  Using cached cycler-0.11.0-py3-none-any.whl (6.4 kB)
Collecting pytz>=2017.3
  Downloading pytz-2022.5-py2.py3-none-any.whl (500 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 500.7/500.7 kB 3.9 MB/s eta 0:00:00
Requirement already satisfied: certifi in /home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages (from minio->openml>=0.12.2->tabpfn) (2022.9.24)
Collecting urllib3
  Using cached urllib3-1.26.12-py2.py3-none-any.whl (140 kB)
Collecting charset-normalizer<3,>=2
  Using cached charset_normalizer-2.1.1-py3-none-any.whl (39 kB)
Collecting idna<4,>=2.5
  Using cached idna-3.4-py3-none-any.whl (61 kB)
Building wheels for collected packages: openml, liac-arff
  Building wheel for openml (setup.py) ... done
  Created wheel for openml: filename=openml-0.12.2-py3-none-any.whl size=137310 sha256=6ae472b3c822b049900d8ddf8d892f664fa68dda0dc874e3d19c31b9a19a0348
  Stored in directory: /home/ye/.cache/pip/wheels/6a/20/88/cf4ac86aa18e2cd647ed16ebe274a5dacee9d0075fa02af250
  Building wheel for liac-arff (setup.py) ... done
  Created wheel for liac-arff: filename=liac_arff-2.5.0-py3-none-any.whl size=11716 sha256=2d852ef410d28cf1c943ae78408f94625e45ce7bfe97be04100d73f3aadaccb2
  Stored in directory: /home/ye/.cache/pip/wheels/1f/0f/15/332ca86cbebf25ddf98518caaf887945fbe1712b97a0f2493b
Successfully built openml liac-arff
Installing collected packages: pytz, py4j, xmltodict, urllib3, typing-extensions, tqdm, threadpoolctl, six, pyyaml, pyparsing, pillow, numpy, networkx, liac-arff, joblib, idna, future, fonttools, cython, cycler, cloudpickle, charset-normalizer, torch, scipy, requests, python-dateutil, pyarrow, packaging, minio, kiwisolver, scikit-learn, pandas, matplotlib, hyperopt, configspace, seaborn, openml, gpytorch, tabpfn
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
nltk 3.5 requires click, which is not installed.
mchmm 0.4.1 requires graphviz, which is not installed.
Successfully installed charset-normalizer-2.1.1 cloudpickle-2.2.0 configspace-0.6.0 cycler-0.11.0 cython-0.29.32 fonttools-4.38.0 future-0.18.2 gpytorch-1.8.1 hyperopt-0.2.7 idna-3.4 joblib-1.2.0 kiwisolver-1.4.4 liac-arff-2.5.0 matplotlib-3.5.3 minio-7.1.12 networkx-2.6.3 numpy-1.21.6 openml-0.12.2 packaging-21.3 pandas-1.3.5 pillow-9.2.0 py4j-0.10.9.7 pyarrow-9.0.0 pyparsing-3.0.9 python-dateutil-2.8.2 pytz-2022.5 pyyaml-6.0 requests-2.28.1 scikit-learn-1.0.2 scipy-1.7.3 seaborn-0.12.1 six-1.16.0 tabpfn-0.1.3 threadpoolctl-3.1.0 torch-1.12.1 tqdm-4.64.1 typing-extensions-4.4.0 urllib3-1.26.12 xmltodict-0.13.0
(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/data/test/neg$ 
```

## Install Two More Libraries 

```
(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/data/test/neg$ pip install graphviz
Collecting graphviz
  Using cached graphviz-0.20.1-py3-none-any.whl (47 kB)
Installing collected packages: graphviz
Successfully installed graphviz-0.20.1
(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/data/test/neg$ 
```

```
(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/data/test/neg$ pip install click
Collecting click
  Using cached click-8.1.3-py3-none-any.whl (96 kB)
Collecting importlib-metadata
  Downloading importlib_metadata-5.0.0-py3-none-any.whl (21 kB)
Requirement already satisfied: typing-extensions>=3.6.4 in /home/ye/tool/anaconda3/envs/tabPFN/lib/python3.7/site-packages (from importlib-metadata->click) (4.4.0)
Collecting zipp>=0.5
  Downloading zipp-3.10.0-py3-none-any.whl (6.2 kB)
Installing collected packages: zipp, importlib-metadata, click
Successfully installed click-8.1.3 importlib-metadata-5.0.0 zipp-3.10.0
(tabPFN) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/data/test/neg$ 
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
