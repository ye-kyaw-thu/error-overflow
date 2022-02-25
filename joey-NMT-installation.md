# Joey NMT Installation

Reference: https://joeynmt.readthedocs.io/en/latest/install.html  
First install Python >= 3.5, PyTorch >=v.0.4.1 and git.  

## Check PyTorch Version

```
(base) ye@:/media/ye/project2/exp$ python
Python 3.7.6 (default, Jan  8 2020, 19:59:22) 
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import torch
>>> print(torch.__version__)
1.6.0
>>> 

```

## Create Virtual Environment

```
(base) ye@:/media/ye/project2/exp$ python3 -m venv jnmt
Error: [Errno 1] Operation not permitted: 'lib' -> '/media/ye/project2/exp/jnmt/lib64'
(base) ye@:/media/ye/project2/exp$ sudo python3 -m venv jnmt
[sudo] password for ye: 
Error: [Errno 1] Operation not permitted: 'lib' -> '/media/ye/project2/exp/jnmt/lib64'
(base) ye@:/media/ye/project2/exp$ 

```

portable HDD မှာမို့လို့လား?!  
လက်ရှိ စက်မှာက space သိပ်မရှိတာနဲ့ Joey-NMT က တကယ် minimal development လုပ်ထားတာမို့... virtual env မလုပ်ပဲ သွားလည်း အဆင်ပြေမယ်လို့ ယူဆ  

## git clone

```
(base) ye@:/media/ye/project2/exp$ git clone https://github.com/joeynmt/joeynmt.git
Cloning into 'joeynmt'...
remote: Enumerating objects: 3312, done.
remote: Counting objects: 100% (361/361), done.
remote: Compressing objects: 100% (208/208), done.
remote: Total 3312 (delta 210), reused 257 (delta 153), pack-reused 2951
Receiving objects: 100% (3312/3312), 8.22 MiB | 5.60 MiB/s, done.
Resolving deltas: 100% (2239/2239), done.
(base) ye@:/media/ye/project2/exp$
```

```
(base) ye@:/media/ye/project2/exp$ cd joeynmt/
(base) ye@:/media/ye/project2/exp/joeynmt$ pip install .
Processing /media/ye/project2/exp/joeynmt
  Preparing metadata (setup.py) ... done
Requirement already satisfied: future in /home/ye/anaconda3/lib/python3.7/site-packages (from joeynmt==1.5.1) (0.18.2)
Requirement already satisfied: pillow in /home/ye/anaconda3/lib/python3.7/site-packages (from joeynmt==1.5.1) (8.3.2)
Requirement already satisfied: numpy>=1.19.5 in /home/ye/anaconda3/lib/python3.7/site-packages (from joeynmt==1.5.1) (1.20.3)
Requirement already satisfied: setuptools>=41.0.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from joeynmt==1.5.1) (59.1.1)
Collecting torch>=1.9.0
  Downloading torch-1.10.2-cp37-cp37m-manylinux1_x86_64.whl (881.9 MB)
     |████████████████████████████████| 881.9 MB 5.8 kB/s             
Requirement already satisfied: tensorboard>=1.15 in /home/ye/anaconda3/lib/python3.7/site-packages (from joeynmt==1.5.1) (2.7.0)
Collecting torchtext>=0.10.0
  Downloading torchtext-0.11.2-cp37-cp37m-manylinux1_x86_64.whl (8.0 MB)
     |████████████████████████████████| 8.0 MB 22.0 MB/s            
Collecting sacrebleu>=2.0.0
  Downloading sacrebleu-2.0.0-py3-none-any.whl (90 kB)
     |████████████████████████████████| 90 kB 11.8 MB/s             
Requirement already satisfied: subword-nmt in /home/ye/anaconda3/lib/python3.7/site-packages/subword_nmt-0.3.7-py3.7.egg (from joeynmt==1.5.1) (0.3.7)
Requirement already satisfied: matplotlib in /home/ye/anaconda3/lib/python3.7/site-packages (from joeynmt==1.5.1) (3.1.1)
Requirement already satisfied: seaborn in /home/ye/anaconda3/lib/python3.7/site-packages (from joeynmt==1.5.1) (0.10.0)
Requirement already satisfied: pyyaml>=5.1 in /home/ye/anaconda3/lib/python3.7/site-packages (from joeynmt==1.5.1) (5.3)
Collecting pylint>=2.9.6
  Downloading pylint-2.12.2-py3-none-any.whl (414 kB)
     |████████████████████████████████| 414 kB 80.5 MB/s            
Requirement already satisfied: six>=1.12 in /home/ye/anaconda3/lib/python3.7/site-packages (from joeynmt==1.5.1) (1.14.0)
Collecting wrapt==1.11.1
  Downloading wrapt-1.11.1.tar.gz (27 kB)
  Preparing metadata (setup.py) ... done
Collecting platformdirs>=2.2.0
  Downloading platformdirs-2.5.1-py3-none-any.whl (14 kB)
Collecting astroid<2.10,>=2.9.0
  Downloading astroid-2.9.3-py3-none-any.whl (254 kB)
     |████████████████████████████████| 254 kB 43.4 MB/s            
Requirement already satisfied: toml>=0.9.2 in /home/ye/anaconda3/lib/python3.7/site-packages (from pylint>=2.9.6->joeynmt==1.5.1) (0.10.2)
Requirement already satisfied: typing-extensions>=3.10.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from pylint>=2.9.6->joeynmt==1.5.1) (3.10.0.2)
Requirement already satisfied: mccabe<0.7,>=0.6 in /home/ye/anaconda3/lib/python3.7/site-packages (from pylint>=2.9.6->joeynmt==1.5.1) (0.6.1)
Requirement already satisfied: isort<6,>=4.2.5 in /home/ye/anaconda3/lib/python3.7/site-packages (from pylint>=2.9.6->joeynmt==1.5.1) (4.3.21)
Requirement already satisfied: regex in /home/ye/anaconda3/lib/python3.7/site-packages (from sacrebleu>=2.0.0->joeynmt==1.5.1) (2020.11.13)
Collecting tabulate>=0.8.9
  Using cached tabulate-0.8.9-py3-none-any.whl (25 kB)
Requirement already satisfied: portalocker in /home/ye/anaconda3/lib/python3.7/site-packages (from sacrebleu>=2.0.0->joeynmt==1.5.1) (2.2.0)
Requirement already satisfied: colorama in /home/ye/anaconda3/lib/python3.7/site-packages (from sacrebleu>=2.0.0->joeynmt==1.5.1) (0.4.3)
Requirement already satisfied: protobuf>=3.6.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (3.19.1)
Requirement already satisfied: google-auth-oauthlib<0.5,>=0.4.1 in /home/ye/anaconda3/lib/python3.7/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (0.4.2)
Requirement already satisfied: absl-py>=0.4 in /home/ye/anaconda3/lib/python3.7/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (0.11.0)
Requirement already satisfied: tensorboard-data-server<0.7.0,>=0.6.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (0.6.1)
Requirement already satisfied: grpcio>=1.24.3 in /home/ye/anaconda3/lib/python3.7/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (1.35.0)
Requirement already satisfied: tensorboard-plugin-wit>=1.6.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (1.8.0)
Requirement already satisfied: wheel>=0.26 in /home/ye/anaconda3/lib/python3.7/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (0.37.0)
Requirement already satisfied: markdown>=2.6.8 in /home/ye/anaconda3/lib/python3.7/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (3.3.3)
Requirement already satisfied: google-auth<3,>=1.6.3 in /home/ye/anaconda3/lib/python3.7/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (1.35.0)
Requirement already satisfied: requests<3,>=2.21.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (2.26.0)
Requirement already satisfied: werkzeug>=0.11.15 in /home/ye/anaconda3/lib/python3.7/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (1.0.0)
Requirement already satisfied: tqdm in /home/ye/anaconda3/lib/python3.7/site-packages (from torchtext>=0.10.0->joeynmt==1.5.1) (4.62.3)
Requirement already satisfied: kiwisolver>=1.0.1 in /home/ye/anaconda3/lib/python3.7/site-packages (from matplotlib->joeynmt==1.5.1) (1.1.0)
Requirement already satisfied: python-dateutil>=2.1 in /home/ye/anaconda3/lib/python3.7/site-packages (from matplotlib->joeynmt==1.5.1) (2.8.1)
Requirement already satisfied: pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.1 in /home/ye/anaconda3/lib/python3.7/site-packages (from matplotlib->joeynmt==1.5.1) (2.4.6)
Requirement already satisfied: cycler>=0.10 in /home/ye/anaconda3/lib/python3.7/site-packages (from matplotlib->joeynmt==1.5.1) (0.10.0)
Requirement already satisfied: scipy>=1.0.1 in /home/ye/anaconda3/lib/python3.7/site-packages (from seaborn->joeynmt==1.5.1) (1.4.1)
Requirement already satisfied: pandas>=0.22.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from seaborn->joeynmt==1.5.1) (1.2.5)
Collecting typed-ast<2.0,>=1.4.0
  Downloading typed_ast-1.5.2-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_12_x86_64.manylinux2010_x86_64.whl (843 kB)
     |████████████████████████████████| 843 kB 65.9 MB/s            
Requirement already satisfied: lazy-object-proxy>=1.4.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from astroid<2.10,>=2.9.0->pylint>=2.9.6->joeynmt==1.5.1) (1.4.3)
Requirement already satisfied: pyasn1-modules>=0.2.1 in /home/ye/anaconda3/lib/python3.7/site-packages (from google-auth<3,>=1.6.3->tensorboard>=1.15->joeynmt==1.5.1) (0.2.8)
Requirement already satisfied: rsa<5,>=3.1.4 in /home/ye/anaconda3/lib/python3.7/site-packages (from google-auth<3,>=1.6.3->tensorboard>=1.15->joeynmt==1.5.1) (4.7)
Requirement already satisfied: cachetools<5.0,>=2.0.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from google-auth<3,>=1.6.3->tensorboard>=1.15->joeynmt==1.5.1) (4.2.1)
Requirement already satisfied: requests-oauthlib>=0.7.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from google-auth-oauthlib<0.5,>=0.4.1->tensorboard>=1.15->joeynmt==1.5.1) (1.3.0)
Requirement already satisfied: importlib-metadata in /home/ye/anaconda3/lib/python3.7/site-packages (from markdown>=2.6.8->tensorboard>=1.15->joeynmt==1.5.1) (4.8.2)
Requirement already satisfied: pytz>=2017.3 in /home/ye/anaconda3/lib/python3.7/site-packages (from pandas>=0.22.0->seaborn->joeynmt==1.5.1) (2019.3)
Requirement already satisfied: charset-normalizer~=2.0.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from requests<3,>=2.21.0->tensorboard>=1.15->joeynmt==1.5.1) (2.0.7)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /home/ye/anaconda3/lib/python3.7/site-packages (from requests<3,>=2.21.0->tensorboard>=1.15->joeynmt==1.5.1) (1.25.8)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/anaconda3/lib/python3.7/site-packages (from requests<3,>=2.21.0->tensorboard>=1.15->joeynmt==1.5.1) (2019.11.28)
Requirement already satisfied: idna<4,>=2.5 in /home/ye/anaconda3/lib/python3.7/site-packages (from requests<3,>=2.21.0->tensorboard>=1.15->joeynmt==1.5.1) (2.8)
Requirement already satisfied: pyasn1<0.5.0,>=0.4.6 in /home/ye/anaconda3/lib/python3.7/site-packages (from pyasn1-modules>=0.2.1->google-auth<3,>=1.6.3->tensorboard>=1.15->joeynmt==1.5.1) (0.4.8)
Requirement already satisfied: oauthlib>=3.0.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from requests-oauthlib>=0.7.0->google-auth-oauthlib<0.5,>=0.4.1->tensorboard>=1.15->joeynmt==1.5.1) (3.1.0)
Requirement already satisfied: zipp>=0.5 in /home/ye/anaconda3/lib/python3.7/site-packages (from importlib-metadata->markdown>=2.6.8->tensorboard>=1.15->joeynmt==1.5.1) (2.2.0)
Building wheels for collected packages: joeynmt, wrapt
  Building wheel for joeynmt (setup.py) ... done
  Created wheel for joeynmt: filename=joeynmt-1.5.1-py3-none-any.whl size=86000 sha256=fd4fbffa3f180ed602cb60384ac060f2ad885bb41f33b46498564fa699fc66db
  Stored in directory: /tmp/pip-ephem-wheel-cache-ede5u3x7/wheels/e9/51/7f/5fb996b2a0b8f05497c18d33ca907b35633abadd72647e3cdf
  Building wheel for wrapt (setup.py) ... done
  Created wheel for wrapt: filename=wrapt-1.11.1-cp37-cp37m-linux_x86_64.whl size=76514 sha256=f5cdb6671a5b291f017e2942530ee7dd5574ab9600c7eee2df936cd6a9b8ca45
  Stored in directory: /home/ye/.cache/pip/wheels/4e/58/9d/da8bad4545585ca52311498ff677647c95c7b690b3040171f8
Successfully built joeynmt wrapt
Installing collected packages: wrapt, typed-ast, torch, tabulate, platformdirs, astroid, torchtext, sacrebleu, pylint, joeynmt
  Attempting uninstall: wrapt
    Found existing installation: wrapt 1.11.2
    Uninstalling wrapt-1.11.2:
      Successfully uninstalled wrapt-1.11.2
  Attempting uninstall: torch
    Found existing installation: torch 1.6.0
    Uninstalling torch-1.6.0:
      Successfully uninstalled torch-1.6.0
  Attempting uninstall: tabulate
    Found existing installation: tabulate 0.8.7
    Uninstalling tabulate-0.8.7:
      Successfully uninstalled tabulate-0.8.7
  Attempting uninstall: astroid
    Found existing installation: astroid 2.3.3
    Uninstalling astroid-2.3.3:
      Successfully uninstalled astroid-2.3.3
  Attempting uninstall: torchtext
    Found existing installation: torchtext 0.5.0
    Uninstalling torchtext-0.5.0:
      Successfully uninstalled torchtext-0.5.0
  Attempting uninstall: sacrebleu
    Found existing installation: sacrebleu 1.5.0
    Uninstalling sacrebleu-1.5.0:
      Successfully uninstalled sacrebleu-1.5.0
  Attempting uninstall: pylint
    Found existing installation: pylint 2.4.4
    Uninstalling pylint-2.4.4:
      Successfully uninstalled pylint-2.4.4
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
spyder 4.0.1 requires pyqt5<5.13; python_version >= "3", which is not installed.
spyder 4.0.1 requires pyqtwebengine<5.13; python_version >= "3", which is not installed.
ersatz 1.0.0 requires tensorboard==2.4.1, but you have tensorboard 2.7.0 which is incompatible.
ersatz 1.0.0 requires torch==1.7.1, but you have torch 1.10.2 which is incompatible.
Successfully installed astroid-2.9.3 joeynmt-1.5.1 platformdirs-2.5.1 pylint-2.12.2 sacrebleu-2.0.0 tabulate-0.8.9 torch-1.10.2 torchtext-0.11.2 typed-ast-1.5.2 wrapt-1.11.1
WARNING: You are using pip version 21.3.1; however, version 22.0.3 is available.
You should consider upgrading via the '/home/ye/anaconda3/bin/python -m pip install --upgrade pip' command.
(base) ye@:/media/ye/project2/exp/joeynmt$ 

```

အထက်ပါအတိုင်း လက်ရှိစက်မှာရှိပြီးသား python library အများစုနဲ့ အဆင်ပြေပေမဲ့ spyder, ersatz တို့ကို install လုပ်မသွားတာကို တွေ့ရ...  

## Create a New Python Environment

Python environment ကို coda သုံးပြီး ဆောက်ဖို့ ဆုံးဖြတ်ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/joeynmt$ conda create --name joey
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/anaconda3/envs/joey



Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate joey
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) ye@:/media/ye/project2/exp/joeynmt$ conda activate joey
(joey) ye@:/media/ye/project2/exp/joeynmt$ 

```

## Install Joey-NMT Again

```
(joey) ye@:/media/ye/project2/exp/joeynmt$ pip install .
Processing /media/ye/project2/exp/joeynmt
Requirement already satisfied: future in /home/ye/.local/lib/python3.8/site-packages (from joeynmt==1.5.1) (0.18.2)
Requirement already satisfied: matplotlib in /home/ye/.local/lib/python3.8/site-packages (from joeynmt==1.5.1) (3.4.2)
Collecting numpy>=1.19.5
  Downloading numpy-1.22.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (16.8 MB)
     |████████████████████████████████| 16.8 MB 1.8 MB/s 
Requirement already satisfied: pillow in /usr/lib/python3/dist-packages (from joeynmt==1.5.1) (7.2.0)
Collecting pylint>=2.9.6
  Using cached pylint-2.12.2-py3-none-any.whl (414 kB)
Requirement already satisfied: pyyaml>=5.1 in /usr/lib/python3/dist-packages (from joeynmt==1.5.1) (5.3.1)
Collecting sacrebleu>=2.0.0
  Using cached sacrebleu-2.0.0-py3-none-any.whl (90 kB)
Requirement already satisfied: seaborn in /home/ye/.local/lib/python3.8/site-packages (from joeynmt==1.5.1) (0.11.1)
Requirement already satisfied: setuptools>=41.0.0 in /usr/lib/python3/dist-packages (from joeynmt==1.5.1) (49.3.1)
Requirement already satisfied: six>=1.12 in /usr/lib/python3/dist-packages (from joeynmt==1.5.1) (1.15.0)
Collecting subword-nmt
  Downloading subword_nmt-0.3.8-py3-none-any.whl (27 kB)
Requirement already satisfied: tensorboard>=1.15 in /home/ye/.local/lib/python3.8/site-packages (from joeynmt==1.5.1) (2.4.1)
Collecting torch>=1.9.0
  Downloading torch-1.10.2-cp38-cp38-manylinux1_x86_64.whl (881.9 MB)
     |████████████████████████████████| 881.9 MB 5.0 kB/s 
Collecting torchtext>=0.10.0
  Downloading torchtext-0.11.2-cp38-cp38-manylinux1_x86_64.whl (8.0 MB)
     |████████████████████████████████| 8.0 MB 18.3 MB/s 
Collecting wrapt==1.11.1
  Using cached wrapt-1.11.1.tar.gz (27 kB)
Requirement already satisfied: pyparsing>=2.2.1 in /home/ye/.local/lib/python3.8/site-packages (from matplotlib->joeynmt==1.5.1) (2.4.7)
Requirement already satisfied: cycler>=0.10 in /home/ye/.local/lib/python3.8/site-packages (from matplotlib->joeynmt==1.5.1) (0.10.0)
Requirement already satisfied: kiwisolver>=1.0.1 in /home/ye/.local/lib/python3.8/site-packages (from matplotlib->joeynmt==1.5.1) (1.3.1)
Requirement already satisfied: python-dateutil>=2.7 in /usr/lib/python3/dist-packages (from matplotlib->joeynmt==1.5.1) (2.8.1)
Collecting astroid<2.10,>=2.9.0
  Using cached astroid-2.9.3-py3-none-any.whl (254 kB)
Collecting mccabe<0.7,>=0.6
  Downloading mccabe-0.6.1-py2.py3-none-any.whl (8.6 kB)
Collecting typing-extensions>=3.10.0; python_version < "3.10"
  Downloading typing_extensions-4.1.1-py3-none-any.whl (26 kB)
Collecting toml>=0.9.2
  Using cached toml-0.10.2-py2.py3-none-any.whl (16 kB)
Collecting isort<6,>=4.2.5
  Downloading isort-5.10.1-py3-none-any.whl (103 kB)
     |████████████████████████████████| 103 kB 43.4 MB/s 
Collecting platformdirs>=2.2.0
  Using cached platformdirs-2.5.1-py3-none-any.whl (14 kB)
Requirement already satisfied: portalocker in /home/ye/.local/lib/python3.8/site-packages (from sacrebleu>=2.0.0->joeynmt==1.5.1) (2.0.0)
Requirement already satisfied: regex in /home/ye/.local/lib/python3.8/site-packages (from sacrebleu>=2.0.0->joeynmt==1.5.1) (2020.11.13)
Requirement already satisfied: tabulate>=0.8.9 in /home/ye/.local/lib/python3.8/site-packages (from sacrebleu>=2.0.0->joeynmt==1.5.1) (0.8.9)
Requirement already satisfied: colorama in /usr/lib/python3/dist-packages (from sacrebleu>=2.0.0->joeynmt==1.5.1) (0.4.3)
Requirement already satisfied: pandas>=0.23 in /home/ye/.local/lib/python3.8/site-packages (from seaborn->joeynmt==1.5.1) (1.3.0)
Requirement already satisfied: scipy>=1.0 in /home/ye/.local/lib/python3.8/site-packages (from seaborn->joeynmt==1.5.1) (1.6.0)
Requirement already satisfied: tqdm in /home/ye/.local/lib/python3.8/site-packages (from subword-nmt->joeynmt==1.5.1) (4.55.1)
Collecting mock
  Downloading mock-4.0.3-py3-none-any.whl (28 kB)
Requirement already satisfied: grpcio>=1.24.3 in /home/ye/.local/lib/python3.8/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (1.32.0)
Requirement already satisfied: requests<3,>=2.21.0 in /usr/lib/python3/dist-packages (from tensorboard>=1.15->joeynmt==1.5.1) (2.23.0)
Requirement already satisfied: google-auth<2,>=1.6.3 in /home/ye/.local/lib/python3.8/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (1.27.1)
Requirement already satisfied: markdown>=2.6.8 in /home/ye/.local/lib/python3.8/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (3.3.4)
Requirement already satisfied: tensorboard-plugin-wit>=1.6.0 in /home/ye/.local/lib/python3.8/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (1.8.0)
Requirement already satisfied: werkzeug>=0.11.15 in /home/ye/.local/lib/python3.8/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (1.0.1)
Requirement already satisfied: protobuf>=3.6.0 in /usr/lib/python3/dist-packages (from tensorboard>=1.15->joeynmt==1.5.1) (3.12.3)
Requirement already satisfied: wheel>=0.26; python_version >= "3" in /home/ye/.local/lib/python3.8/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (0.36.2)
Requirement already satisfied: absl-py>=0.4 in /home/ye/.local/lib/python3.8/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (0.12.0)
Requirement already satisfied: google-auth-oauthlib<0.5,>=0.4.1 in /home/ye/.local/lib/python3.8/site-packages (from tensorboard>=1.15->joeynmt==1.5.1) (0.4.3)
Collecting lazy-object-proxy>=1.4.0
  Downloading lazy_object_proxy-1.7.1-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (60 kB)
     |████████████████████████████████| 60 kB 9.3 MB/s 
Requirement already satisfied: pytz>=2017.3 in /usr/lib/python3/dist-packages (from pandas>=0.23->seaborn->joeynmt==1.5.1) (2020.1)
Requirement already satisfied: pyasn1-modules>=0.2.1 in /home/ye/.local/lib/python3.8/site-packages (from google-auth<2,>=1.6.3->tensorboard>=1.15->joeynmt==1.5.1) (0.2.8)
Requirement already satisfied: rsa<5,>=3.1.4; python_version >= "3.6" in /home/ye/.local/lib/python3.8/site-packages (from google-auth<2,>=1.6.3->tensorboard>=1.15->joeynmt==1.5.1) (4.7.2)
Requirement already satisfied: cachetools<5.0,>=2.0.0 in /home/ye/.local/lib/python3.8/site-packages (from google-auth<2,>=1.6.3->tensorboard>=1.15->joeynmt==1.5.1) (4.2.1)
Requirement already satisfied: requests-oauthlib>=0.7.0 in /home/ye/.local/lib/python3.8/site-packages (from google-auth-oauthlib<0.5,>=0.4.1->tensorboard>=1.15->joeynmt==1.5.1) (1.3.0)
Requirement already satisfied: pyasn1<0.5.0,>=0.4.6 in /home/ye/.local/lib/python3.8/site-packages (from pyasn1-modules>=0.2.1->google-auth<2,>=1.6.3->tensorboard>=1.15->joeynmt==1.5.1) (0.4.8)
Requirement already satisfied: oauthlib>=3.0.0 in /usr/lib/python3/dist-packages (from requests-oauthlib>=0.7.0->google-auth-oauthlib<0.5,>=0.4.1->tensorboard>=1.15->joeynmt==1.5.1) (3.1.0)
Building wheels for collected packages: joeynmt, wrapt
  Building wheel for joeynmt (setup.py) ... done
  Created wheel for joeynmt: filename=joeynmt-1.5.1-py3-none-any.whl size=85988 sha256=13bade9dc39cdb022d50528db5d91f4e0bcd06b193e8145a65e16bf522f3f8a8
  Stored in directory: /tmp/pip-ephem-wheel-cache-_6w7ijk_/wheels/33/00/5c/e266ab4e2514a7a25ca5302764936e1fb1633c152ba6f6b3b2
  Building wheel for wrapt (setup.py) ... done
  Created wheel for wrapt: filename=wrapt-1.11.1-cp38-cp38-linux_x86_64.whl size=73482 sha256=e10f7a4496d20058f8e115690d3ba9beba39766edce6bfa39a6fef4d15ed9c3a
  Stored in directory: /home/ye/.cache/pip/wheels/90/d4/83/58efda72eb47567053254faec24fe048dced315a0c3f11e8f8
Successfully built joeynmt wrapt
ERROR: tensorflow-gpu 2.4.1 has requirement numpy~=1.19.2, but you'll have numpy 1.22.2 which is incompatible.
ERROR: tensorflow-gpu 2.4.1 has requirement typing-extensions~=3.7.4, but you'll have typing-extensions 4.1.1 which is incompatible.
ERROR: tensorflow-gpu 2.4.1 has requirement wrapt~=1.12.1, but you'll have wrapt 1.11.1 which is incompatible.
ERROR: numba 0.54.0 has requirement numpy<1.21,>=1.17, but you'll have numpy 1.22.2 which is incompatible.
ERROR: huggingface-hub 0.0.12 has requirement packaging>=20.9, but you'll have packaging 20.8 which is incompatible.
Installing collected packages: numpy, typing-extensions, wrapt, lazy-object-proxy, astroid, mccabe, toml, isort, platformdirs, pylint, sacrebleu, mock, subword-nmt, torch, torchtext, joeynmt
  Attempting uninstall: numpy
    Found existing installation: numpy 1.19.4
    Uninstalling numpy-1.19.4:
      Successfully uninstalled numpy-1.19.4
  Attempting uninstall: typing-extensions
    Found existing installation: typing-extensions 3.7.4.3
    Uninstalling typing-extensions-3.7.4.3:
      Successfully uninstalled typing-extensions-3.7.4.3
  Attempting uninstall: wrapt
    Found existing installation: wrapt 1.12.1
    Uninstalling wrapt-1.12.1:
      Successfully uninstalled wrapt-1.12.1
  Attempting uninstall: sacrebleu
    Found existing installation: sacrebleu 1.4.14
    Uninstalling sacrebleu-1.4.14:
      Successfully uninstalled sacrebleu-1.4.14
  Attempting uninstall: torch
    Found existing installation: torch 1.7.1
    Uninstalling torch-1.7.1:
      Successfully uninstalled torch-1.7.1
Successfully installed astroid-2.9.3 isort-5.10.1 joeynmt-1.5.1 lazy-object-proxy-1.7.1 mccabe-0.6.1 mock-4.0.3 numpy-1.22.2 platformdirs-2.5.1 pylint-2.12.2 sacrebleu-2.0.0 subword-nmt-0.3.8 toml-0.10.2 torch-1.10.2 torchtext-0.11.2 typing-extensions-4.1.1 wrapt-1.11.1
(joey) ye@:/media/ye/project2/exp/joeynmt$ 

```

အဆင်ပြေပြေနဲ့ installation လုပ်လို့ ပြီးသွားပြီလို့ ယူဆခဲ့...   

## Run Unit Test

```
(joey) ye@:/media/ye/project2/exp/joeynmt$ python3 -m unittest
................................s.........................
----------------------------------------------------------------------
Ran 58 tests in 1.366s

OK (skipped=1)
(joey) ye@:/media/ye/project2/exp/joeynmt$ 
```

## Build a Toy RNN

Reference: https://joeynmt.readthedocs.io/en/latest/tutorial.html  

check current folder  

```
(joey) ye@:/media/ye/project2/exp/joeynmt$ ls
benchmarks.md  CODE_OF_CONDUCT.md  docs             joeynmt           joey-small.png  README.md         scripts   test
build          configs             joey_demo.ipynb  joeynmt.egg-info  LICENSE         requirements.txt  setup.py
```

data ကို generate လုပ်ခဲ့...  

```
(joey) ye@:/media/ye/project2/exp/joeynmt$ python3 scripts/generate_reverse_task.py
(joey) ye@:/media/ye/project2/exp/joeynmt$ ls
benchmarks.md       configs  docs             joeynmt.egg-info  README.md         setup.py  test.trg
build               dev.src  joey_demo.ipynb  joey-small.png    requirements.txt  test      train.src
CODE_OF_CONDUCT.md  dev.trg  joeynmt          LICENSE           scripts           test.src  train.trg
(joey) ye@:/media/ye/project2/exp/joeynmt$
```

```
(joey) ye@:/media/ye/project2/exp/joeynmt$ ls *.{src,trg}
dev.src  dev.trg  test.src  test.trg  train.src  train.trg
(joey) ye@:/media/ye/project2/exp/joeynmt$
```

reverse ဆိုတဲ့ နာမည်နဲ့ folder အသစ် တစ်ခု ဆောက်ပြီး အဲဒီအောက်ကို generate လုပ်ထားတဲ့ ဒေတာအကုန်ကို ရွှေ့...  

```
(joey) ye@:/media/ye/project2/exp/joeynmt$ mkdir test/data/reverse
(joey) ye@:/media/ye/project2/exp/joeynmt$ mv {train,test,dev}* ./test/data/reverse/
mv: cannot move 'test' to a subdirectory of itself, './test/data/reverse/test'
(joey) ye@:/media/ye/project2/exp/joeynmt$ ls ./test/data/reverse/
dev.src  dev.trg  test.src  test.trg  train.src  train.trg
(joey) ye@:/media/ye/project2/exp/joeynmt$ 
```

ဒီ Tutorial က Machine Translation ကို ပထမဆုံး စလုပ်တဲ့သူတွေအတွက် ရည်ရွယ်ထားတာမို့ preprocessing နဲ့ ပတ်သက်ပြီးတော့ အောက်ပါ SockEye စာတမ်းကိုဖတ်ဖို့ ညွှန်းထားတယ်...  

https://arxiv.org/pdf/1712.05690.pdf  

စာတမ်းထဲက ဖတ်စေချင်တာက အောက်ပါ စာကြောင်းတွေပါ။  

The preprocessing scheme was held constant over all models. It was constructed through four steps: normalization, tokenization, sentence-filtering, and byte-pair encoding.  

- Normalization. We used Moses’ normalize-punctuation.perl -l LANG and then removed non-printing characters with remove-non-printing-char.perl [Koehn et al., 2007].
- Tokenization. We used Moses’ tokenizer.perl with the following arguments:  -no-escape -l LANG -protected PATTERNS, where PATTERNS is the basic-protectedpatterns file included with the Moses tokenizer. Case was retained as found in the training data. No true-casing was applied.
- Filtering (training only). Sentences longer than 100 tokens on either side were removed using the Moses’ clean-corpus-n.perl with arguments 1 100.
- Byte-pair encoding. We trained a byte-pair encoding model with 32,000 split operations [Sennrich et al., 2016].

## Build Configuration File

Configuration file က YAML format ကို သုံးထားတယ်။  
example configuration ဖိုင်တွေက အောက်ပါ အတိုင်း...  

```
(joey) ye@:/media/ye/project2/exp/joeynmt$ cd configs/
(joey) ye@:/media/ye/project2/exp/joeynmt/configs$ ls
iwslt14_deen_bpe.yaml     reverse.yaml                       transformer_iwslt14_deen_sp.yaml     transformer_wmt17_ende.yaml  wmt_lven_best.yaml
iwslt_deen_bahdanau.yaml  small.yaml                         transformer_jparacrawl_enja_sp.yaml  transformer_wmt17_lven.yaml  wmt_lven_default.yaml
iwslt_envi_luong.yaml     transformer_copy.yaml              transformer_reverse.yaml             wmt_ende_best.yaml
iwslt_envi_xnmt.yaml      transformer_iwslt14_deen_bpe.yaml  transformer_small.yaml               wmt_ende_default.yaml
```

Toy RNN Model Build လုပ်ဖို့အတွက်က reverse.yaml ကို သုံးမှာ...  

```
(joey) ye@:/media/ye/project2/exp/joeynmt/configs$ cat reverse.yaml 
name: "reverse_experiment"

data:
    src: "src"
    trg: "trg"
    # generate data with scripts/generate_reverse_task.py
    train: "test/data/reverse/train"
    dev: "test/data/reverse/dev"
    test: "test/data/reverse/test"
    level: "word"
    lowercase: False
    max_sent_length: 25
    src_voc_min_freq: 0
    src_voc_limit: 100
    trg_voc_min_freq: 0
    trg_voc_limit: 100
    #src_vocab: "reverse_model/src_vocab.txt"
    #trg_vocab: "reverse_model/trg_vocab.txt"

testing:
    beam_size: 1
    alpha: 1.0

training:
    random_seed: 42
    optimizer: "adam"
    learning_rate: 0.001
    learning_rate_min: 0.0002
    weight_decay: 0.0
    clip_grad_norm: 1.0
    batch_size: 10
    batch_type: "sentence"
    scheduling: "plateau"
    patience: 5
    decrease_factor: 0.5
    early_stopping_metric: "eval_metric"
    epochs: 1
    validation_freq: 1000
    logging_freq: 100
    eval_metric: "bleu"
    model_dir: "reverse_model"
    overwrite: True
    shuffle: True
    use_cuda: False
    max_output_length: 30
    print_valid_sents: [0, 3, 6]
    keep_best_ckpts: 2

model:
    initializer: "xavier"
    embed_initializer: "normal"
    embed_init_weight: 0.1
    bias_initializer: "zeros"
    init_rnn_orthogonal: False
    lstm_forget_gate: 0.
    encoder:
        rnn_type: "lstm"
        embeddings:
            embedding_dim: 16
            scale: False
        hidden_size: 64
        bidirectional: True
        dropout: 0.1
        num_layers: 1
    decoder:
        rnn_type: "lstm"
        embeddings:
            embedding_dim: 16
            scale: False
        hidden_size: 64
        dropout: 0.1
        hidden_dropout: 0.1
        num_layers: 1
        input_feeding: True
        init_hidden: "zero"
        attention: "luong"
(joey) ye@:/media/ye/project2/exp/joeynmt/configs$ 

```

## Training

ပထမဆုံး NMT စလုပ်ကြမယ့် သူတွေ ဆိုရင်တော့ configuration setting တွေနဲ့ ပတ်သက်ပြီးတော့ အသေးစိတ် လေ့လာသင့်ပါတယ်။  
toy model ကို training လုပ်ကြည့်ခဲ့တယ်...  

```
(joey) ye@:/media/ye/project2/exp/joeynmt$ time python3 -m joeynmt train configs/reverse.yaml
2022-02-25 16:01:46,491 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-25 16:01:46,516 - INFO - joeynmt.data - Loading training data...
2022-02-25 16:01:46,803 - INFO - joeynmt.data - Building vocabulary...
2022-02-25 16:01:46,913 - INFO - joeynmt.data - Loading dev data...
2022-02-25 16:01:46,919 - INFO - joeynmt.data - Loading test data...
2022-02-25 16:01:46,922 - INFO - joeynmt.data - Data loaded.
2022-02-25 16:01:46,922 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-25 16:01:46,925 - INFO - joeynmt.model - Enc-dec model built.
2022-02-25 16:01:47.173689: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.11.0
2022-02-25 16:01:48,284 - INFO - joeynmt.training - Total params: 105088
2022-02-25 16:01:48,285 - INFO - joeynmt.helpers -                           cfg.name : reverse_experiment
2022-02-25 16:01:48,285 - INFO - joeynmt.helpers -                       cfg.data.src : src
2022-02-25 16:01:48,285 - INFO - joeynmt.helpers -                       cfg.data.trg : trg
2022-02-25 16:01:48,285 - INFO - joeynmt.helpers -                     cfg.data.train : test/data/reverse/train
2022-02-25 16:01:48,285 - INFO - joeynmt.helpers -                       cfg.data.dev : test/data/reverse/dev
2022-02-25 16:01:48,285 - INFO - joeynmt.helpers -                      cfg.data.test : test/data/reverse/test
2022-02-25 16:01:48,285 - INFO - joeynmt.helpers -                     cfg.data.level : word
2022-02-25 16:01:48,285 - INFO - joeynmt.helpers -                 cfg.data.lowercase : False
2022-02-25 16:01:48,285 - INFO - joeynmt.helpers -           cfg.data.max_sent_length : 25
2022-02-25 16:01:48,285 - INFO - joeynmt.helpers -          cfg.data.src_voc_min_freq : 0
2022-02-25 16:01:48,285 - INFO - joeynmt.helpers -             cfg.data.src_voc_limit : 100
2022-02-25 16:01:48,285 - INFO - joeynmt.helpers -          cfg.data.trg_voc_min_freq : 0
2022-02-25 16:01:48,285 - INFO - joeynmt.helpers -             cfg.data.trg_voc_limit : 100
2022-02-25 16:01:48,285 - INFO - joeynmt.helpers -              cfg.testing.beam_size : 1
2022-02-25 16:01:48,285 - INFO - joeynmt.helpers -                  cfg.testing.alpha : 1.0
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -           cfg.training.random_seed : 42
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -             cfg.training.optimizer : adam
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -         cfg.training.learning_rate : 0.001
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -     cfg.training.learning_rate_min : 0.0002
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -          cfg.training.weight_decay : 0.0
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -        cfg.training.clip_grad_norm : 1.0
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -            cfg.training.batch_size : 10
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -            cfg.training.batch_type : sentence
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -            cfg.training.scheduling : plateau
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -              cfg.training.patience : 5
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -       cfg.training.decrease_factor : 0.5
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers - cfg.training.early_stopping_metric : eval_metric
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -                cfg.training.epochs : 1
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -       cfg.training.validation_freq : 1000
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -          cfg.training.logging_freq : 100
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -           cfg.training.eval_metric : bleu
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -             cfg.training.model_dir : reverse_model
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -             cfg.training.overwrite : True
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -               cfg.training.shuffle : True
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -              cfg.training.use_cuda : False
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -     cfg.training.max_output_length : 30
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -     cfg.training.print_valid_sents : [0, 3, 6]
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -       cfg.training.keep_best_ckpts : 2
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -              cfg.model.initializer : xavier
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -        cfg.model.embed_initializer : normal
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -        cfg.model.embed_init_weight : 0.1
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -         cfg.model.bias_initializer : zeros
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -      cfg.model.init_rnn_orthogonal : False
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -         cfg.model.lstm_forget_gate : 0.0
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -         cfg.model.encoder.rnn_type : lstm
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.embedding_dim : 16
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.scale : False
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -      cfg.model.encoder.hidden_size : 64
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -    cfg.model.encoder.bidirectional : True
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -          cfg.model.encoder.dropout : 0.1
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -       cfg.model.encoder.num_layers : 1
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers -         cfg.model.decoder.rnn_type : lstm
2022-02-25 16:01:48,286 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.embedding_dim : 16
2022-02-25 16:01:48,287 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.scale : False
2022-02-25 16:01:48,287 - INFO - joeynmt.helpers -      cfg.model.decoder.hidden_size : 64
2022-02-25 16:01:48,287 - INFO - joeynmt.helpers -          cfg.model.decoder.dropout : 0.1
2022-02-25 16:01:48,287 - INFO - joeynmt.helpers -   cfg.model.decoder.hidden_dropout : 0.1
2022-02-25 16:01:48,287 - INFO - joeynmt.helpers -       cfg.model.decoder.num_layers : 1
2022-02-25 16:01:48,287 - INFO - joeynmt.helpers -    cfg.model.decoder.input_feeding : True
2022-02-25 16:01:48,287 - INFO - joeynmt.helpers -      cfg.model.decoder.init_hidden : zero
2022-02-25 16:01:48,287 - INFO - joeynmt.helpers -        cfg.model.decoder.attention : luong
2022-02-25 16:01:48,287 - INFO - joeynmt.helpers - Data set sizes: 
	train 50000,
	valid 1000,
	test 1000
2022-02-25 16:01:48,287 - INFO - joeynmt.helpers - First training example:
	[SRC] 28 14 42 7 20 38 18
	[TRG] 18 38 20 7 42 14 28
2022-02-25 16:01:48,287 - INFO - joeynmt.helpers - First 10 words (src): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) 15 (5) 35 (6) 44 (7) 18 (8) 36 (9) 16
2022-02-25 16:01:48,287 - INFO - joeynmt.helpers - First 10 words (trg): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) 15 (5) 35 (6) 44 (7) 18 (8) 36 (9) 16
2022-02-25 16:01:48,287 - INFO - joeynmt.helpers - Number of Src words (types): 54
2022-02-25 16:01:48,287 - INFO - joeynmt.helpers - Number of Trg words (types): 54
2022-02-25 16:01:48,287 - INFO - joeynmt.training - Model(
	encoder=RecurrentEncoder(LSTM(16, 64, batch_first=True, bidirectional=True)),
	decoder=RecurrentDecoder(rnn=LSTM(80, 64, batch_first=True), attention=LuongAttention),
	src_embed=Embeddings(embedding_dim=16, vocab_size=54),
	trg_embed=Embeddings(embedding_dim=16, vocab_size=54))
2022-02-25 16:01:48,287 - INFO - joeynmt.training - Train stats:
	device: cpu
	n_gpu: 0
	16-bits training: False
	gradient accumulation: 1
	batch size per device: 10
	total batch size (w. parallel & accumulation): 10
2022-02-25 16:01:48,287 - INFO - joeynmt.training - EPOCH 1
2022-02-25 16:01:52,656 - INFO - joeynmt.training - Epoch   1, Step:      100, Batch Loss:    53.850666, Tokens per Sec:     3117, Lr: 0.001000
2022-02-25 16:01:56,663 - INFO - joeynmt.training - Epoch   1, Step:      200, Batch Loss:    66.041504, Tokens per Sec:     3530, Lr: 0.001000
2022-02-25 16:02:00,895 - INFO - joeynmt.training - Epoch   1, Step:      300, Batch Loss:    53.775745, Tokens per Sec:     3293, Lr: 0.001000
2022-02-25 16:02:05,522 - INFO - joeynmt.training - Epoch   1, Step:      400, Batch Loss:    46.204933, Tokens per Sec:     3074, Lr: 0.001000
2022-02-25 16:02:10,248 - INFO - joeynmt.training - Epoch   1, Step:      500, Batch Loss:    42.466156, Tokens per Sec:     2938, Lr: 0.001000
2022-02-25 16:02:14,502 - INFO - joeynmt.training - Epoch   1, Step:      600, Batch Loss:    47.798969, Tokens per Sec:     3306, Lr: 0.001000
2022-02-25 16:02:18,649 - INFO - joeynmt.training - Epoch   1, Step:      700, Batch Loss:    43.076118, Tokens per Sec:     3342, Lr: 0.001000
2022-02-25 16:02:22,820 - INFO - joeynmt.training - Epoch   1, Step:      800, Batch Loss:    32.452343, Tokens per Sec:     3317, Lr: 0.001000
2022-02-25 16:02:27,575 - INFO - joeynmt.training - Epoch   1, Step:      900, Batch Loss:    40.858349, Tokens per Sec:     2953, Lr: 0.001000
2022-02-25 16:02:32,450 - INFO - joeynmt.training - Epoch   1, Step:     1000, Batch Loss:    20.104404, Tokens per Sec:     2861, Lr: 0.001000
2022-02-25 16:02:35,558 - INFO - joeynmt.training - Hooray! New best validation result [eval_metric]!
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/media/ye/project2/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/media/ye/project2/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/media/ye/project2/exp/joeynmt/joeynmt/training.py", line 846, in train
    trainer.train_and_validate(train_data=train_data, valid_data=dev_data)
  File "/media/ye/project2/exp/joeynmt/joeynmt/training.py", line 497, in train_and_validate
    valid_duration = self._validate(valid_data, epoch_no)
  File "/media/ye/project2/exp/joeynmt/joeynmt/training.py", line 629, in _validate
    self._save_checkpoint(new_best, ckpt_score)
  File "/media/ye/project2/exp/joeynmt/joeynmt/training.py", line 268, in _save_checkpoint
    prev_path = symlink_update(symlink_target, last_path) # update always
  File "/media/ye/project2/exp/joeynmt/joeynmt/helpers.py", line 369, in symlink_update
    link_name.symlink_to(target)
  File "/usr/lib/python3.8/pathlib.py", line 1384, in symlink_to
    self._accessor.symlink(target, self, target_is_directory)
  File "/usr/lib/python3.8/pathlib.py", line 446, in symlink
    return os.symlink(a, b)
PermissionError: [Errno 1] Operation not permitted: '1000.ckpt' -> 'reverse_model/latest.ckpt'

real	0m50.760s
user	5m56.703s
sys	0m2.018s
(joey) ye@:/media/ye/project2/exp/joeynmt$
```

USB နဲ့ ချိတ်ထားတဲ့ Portable HDD ရဲ့ file system ကြောင့် ဖြစ်တဲ့ ပြဿနာလို့ နားလည်တယ်။  
အဲဒါနဲ့ နောက်ထပ် portable HDD တစ်ခုဆီကို joeynmt/ ဖိုလ်ဒါ တစ်ခုလုံးကို ရွှေ့ပလိုက်ပြီးတော့ training ထပ်လုပ်ခဲ့တယ်...  

```
(joey) ye@:/media/ye/project2/exp/joeynmt$ cd ..
(joey) ye@:/media/ye/project2/exp$ mv joeynmt /media/ye/project1/exp/
(joey) ye@:/media/ye/project2/exp$ cd ../../project1/exp/joeynmt/
(joey) ye@:/media/ye/project1/exp/joeynmt$ time python3 -m joeynmt train configs/reverse.yaml
2022-02-25 16:40:25,001 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-25 16:40:25,019 - INFO - joeynmt.data - Loading training data...
2022-02-25 16:40:25,308 - INFO - joeynmt.data - Building vocabulary...
2022-02-25 16:40:25,420 - INFO - joeynmt.data - Loading dev data...
2022-02-25 16:40:25,426 - INFO - joeynmt.data - Loading test data...
2022-02-25 16:40:25,429 - INFO - joeynmt.data - Data loaded.
2022-02-25 16:40:25,429 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-25 16:40:25,432 - INFO - joeynmt.model - Enc-dec model built.
2022-02-25 16:40:25.511604: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.11.0
2022-02-25 16:40:26,156 - INFO - joeynmt.training - Total params: 105088
2022-02-25 16:40:26,157 - INFO - joeynmt.helpers -                           cfg.name : reverse_experiment
2022-02-25 16:40:26,157 - INFO - joeynmt.helpers -                       cfg.data.src : src
2022-02-25 16:40:26,157 - INFO - joeynmt.helpers -                       cfg.data.trg : trg
2022-02-25 16:40:26,157 - INFO - joeynmt.helpers -                     cfg.data.train : test/data/reverse/train
2022-02-25 16:40:26,157 - INFO - joeynmt.helpers -                       cfg.data.dev : test/data/reverse/dev
2022-02-25 16:40:26,157 - INFO - joeynmt.helpers -                      cfg.data.test : test/data/reverse/test
2022-02-25 16:40:26,157 - INFO - joeynmt.helpers -                     cfg.data.level : word
2022-02-25 16:40:26,157 - INFO - joeynmt.helpers -                 cfg.data.lowercase : False
2022-02-25 16:40:26,157 - INFO - joeynmt.helpers -           cfg.data.max_sent_length : 25
2022-02-25 16:40:26,157 - INFO - joeynmt.helpers -          cfg.data.src_voc_min_freq : 0
2022-02-25 16:40:26,157 - INFO - joeynmt.helpers -             cfg.data.src_voc_limit : 100
2022-02-25 16:40:26,157 - INFO - joeynmt.helpers -          cfg.data.trg_voc_min_freq : 0
2022-02-25 16:40:26,157 - INFO - joeynmt.helpers -             cfg.data.trg_voc_limit : 100
2022-02-25 16:40:26,157 - INFO - joeynmt.helpers -              cfg.testing.beam_size : 1
2022-02-25 16:40:26,157 - INFO - joeynmt.helpers -                  cfg.testing.alpha : 1.0
2022-02-25 16:40:26,157 - INFO - joeynmt.helpers -           cfg.training.random_seed : 42
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -             cfg.training.optimizer : adam
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -         cfg.training.learning_rate : 0.001
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -     cfg.training.learning_rate_min : 0.0002
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -          cfg.training.weight_decay : 0.0
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -        cfg.training.clip_grad_norm : 1.0
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -            cfg.training.batch_size : 10
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -            cfg.training.batch_type : sentence
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -            cfg.training.scheduling : plateau
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -              cfg.training.patience : 5
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -       cfg.training.decrease_factor : 0.5
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers - cfg.training.early_stopping_metric : eval_metric
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -                cfg.training.epochs : 1
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -       cfg.training.validation_freq : 1000
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -          cfg.training.logging_freq : 100
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -           cfg.training.eval_metric : bleu
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -             cfg.training.model_dir : reverse_model
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -             cfg.training.overwrite : True
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -               cfg.training.shuffle : True
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -              cfg.training.use_cuda : False
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -     cfg.training.max_output_length : 30
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -     cfg.training.print_valid_sents : [0, 3, 6]
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -       cfg.training.keep_best_ckpts : 2
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -              cfg.model.initializer : xavier
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -        cfg.model.embed_initializer : normal
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -        cfg.model.embed_init_weight : 0.1
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -         cfg.model.bias_initializer : zeros
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -      cfg.model.init_rnn_orthogonal : False
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -         cfg.model.lstm_forget_gate : 0.0
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -         cfg.model.encoder.rnn_type : lstm
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.embedding_dim : 16
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.scale : False
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -      cfg.model.encoder.hidden_size : 64
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -    cfg.model.encoder.bidirectional : True
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -          cfg.model.encoder.dropout : 0.1
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -       cfg.model.encoder.num_layers : 1
2022-02-25 16:40:26,158 - INFO - joeynmt.helpers -         cfg.model.decoder.rnn_type : lstm
2022-02-25 16:40:26,159 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.embedding_dim : 16
2022-02-25 16:40:26,159 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.scale : False
2022-02-25 16:40:26,159 - INFO - joeynmt.helpers -      cfg.model.decoder.hidden_size : 64
2022-02-25 16:40:26,159 - INFO - joeynmt.helpers -          cfg.model.decoder.dropout : 0.1
2022-02-25 16:40:26,159 - INFO - joeynmt.helpers -   cfg.model.decoder.hidden_dropout : 0.1
2022-02-25 16:40:26,159 - INFO - joeynmt.helpers -       cfg.model.decoder.num_layers : 1
2022-02-25 16:40:26,159 - INFO - joeynmt.helpers -    cfg.model.decoder.input_feeding : True
2022-02-25 16:40:26,159 - INFO - joeynmt.helpers -      cfg.model.decoder.init_hidden : zero
2022-02-25 16:40:26,159 - INFO - joeynmt.helpers -        cfg.model.decoder.attention : luong
2022-02-25 16:40:26,159 - INFO - joeynmt.helpers - Data set sizes: 
	train 50000,
	valid 1000,
	test 1000
2022-02-25 16:40:26,159 - INFO - joeynmt.helpers - First training example:
	[SRC] 28 14 42 7 20 38 18
	[TRG] 18 38 20 7 42 14 28
2022-02-25 16:40:26,159 - INFO - joeynmt.helpers - First 10 words (src): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) 15 (5) 35 (6) 44 (7) 18 (8) 36 (9) 16
2022-02-25 16:40:26,159 - INFO - joeynmt.helpers - First 10 words (trg): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) 15 (5) 35 (6) 44 (7) 18 (8) 36 (9) 16
2022-02-25 16:40:26,159 - INFO - joeynmt.helpers - Number of Src words (types): 54
2022-02-25 16:40:26,159 - INFO - joeynmt.helpers - Number of Trg words (types): 54
2022-02-25 16:40:26,160 - INFO - joeynmt.training - Model(
	encoder=RecurrentEncoder(LSTM(16, 64, batch_first=True, bidirectional=True)),
	decoder=RecurrentDecoder(rnn=LSTM(80, 64, batch_first=True), attention=LuongAttention),
	src_embed=Embeddings(embedding_dim=16, vocab_size=54),
	trg_embed=Embeddings(embedding_dim=16, vocab_size=54))
2022-02-25 16:40:26,160 - INFO - joeynmt.training - Train stats:
	device: cpu
	n_gpu: 0
	16-bits training: False
	gradient accumulation: 1
	batch size per device: 10
	total batch size (w. parallel & accumulation): 10
2022-02-25 16:40:26,160 - INFO - joeynmt.training - EPOCH 1
2022-02-25 16:40:30,275 - INFO - joeynmt.training - Epoch   1, Step:      100, Batch Loss:    53.850666, Tokens per Sec:     3310, Lr: 0.001000
2022-02-25 16:40:34,317 - INFO - joeynmt.training - Epoch   1, Step:      200, Batch Loss:    66.041504, Tokens per Sec:     3499, Lr: 0.001000
2022-02-25 16:40:38,439 - INFO - joeynmt.training - Epoch   1, Step:      300, Batch Loss:    53.775745, Tokens per Sec:     3382, Lr: 0.001000
2022-02-25 16:40:43,070 - INFO - joeynmt.training - Epoch   1, Step:      400, Batch Loss:    46.204933, Tokens per Sec:     3072, Lr: 0.001000
2022-02-25 16:40:48,750 - INFO - joeynmt.training - Epoch   1, Step:      500, Batch Loss:    42.466156, Tokens per Sec:     2444, Lr: 0.001000
2022-02-25 16:40:53,218 - INFO - joeynmt.training - Epoch   1, Step:      600, Batch Loss:    47.798969, Tokens per Sec:     3147, Lr: 0.001000
2022-02-25 16:40:57,379 - INFO - joeynmt.training - Epoch   1, Step:      700, Batch Loss:    43.076118, Tokens per Sec:     3331, Lr: 0.001000
2022-02-25 16:41:01,513 - INFO - joeynmt.training - Epoch   1, Step:      800, Batch Loss:    32.452343, Tokens per Sec:     3346, Lr: 0.001000
2022-02-25 16:41:05,556 - INFO - joeynmt.training - Epoch   1, Step:      900, Batch Loss:    40.858349, Tokens per Sec:     3473, Lr: 0.001000
2022-02-25 16:41:09,967 - INFO - joeynmt.training - Epoch   1, Step:     1000, Batch Loss:    20.104404, Tokens per Sec:     3162, Lr: 0.001000
2022-02-25 16:41:13,499 - INFO - joeynmt.training - Hooray! New best validation result [eval_metric]!
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/media/ye/project1/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/media/ye/project1/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/media/ye/project1/exp/joeynmt/joeynmt/training.py", line 846, in train
    trainer.train_and_validate(train_data=train_data, valid_data=dev_data)
  File "/media/ye/project1/exp/joeynmt/joeynmt/training.py", line 497, in train_and_validate
    valid_duration = self._validate(valid_data, epoch_no)
  File "/media/ye/project1/exp/joeynmt/joeynmt/training.py", line 629, in _validate
    self._save_checkpoint(new_best, ckpt_score)
  File "/media/ye/project1/exp/joeynmt/joeynmt/training.py", line 268, in _save_checkpoint
    prev_path = symlink_update(symlink_target, last_path) # update always
  File "/media/ye/project1/exp/joeynmt/joeynmt/helpers.py", line 369, in symlink_update
    link_name.symlink_to(target)
  File "/usr/lib/python3.8/pathlib.py", line 1384, in symlink_to
    self._accessor.symlink(target, self, target_is_directory)
  File "/usr/lib/python3.8/pathlib.py", line 446, in symlink
    return os.symlink(a, b)
PermissionError: [Errno 1] Operation not permitted: '1000.ckpt' -> 'reverse_model/latest.ckpt'

real	0m49.913s
user	5m55.748s
sys	0m1.797s
```

အထက်ပါအတိုင်းပါပဲ။ နောက်  HDD မှာလည်း error ပေးနေပြန်ပါတယ်။  
အဲဒါနဲ့ main HDD ဆီကို ရွှေ့ပြီး run ကြည့်ခဲ့ပါတယ်။ အောက်ပါအတိုင်းပါ...  

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/reverse.yaml
2022-02-25 16:50:40,603 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-25 16:50:40,620 - INFO - joeynmt.data - Loading training data...
2022-02-25 16:50:40,907 - INFO - joeynmt.data - Building vocabulary...
2022-02-25 16:50:41,017 - INFO - joeynmt.data - Loading dev data...
2022-02-25 16:50:41,023 - INFO - joeynmt.data - Loading test data...
2022-02-25 16:50:41,026 - INFO - joeynmt.data - Data loaded.
2022-02-25 16:50:41,026 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-25 16:50:41,029 - INFO - joeynmt.model - Enc-dec model built.
2022-02-25 16:50:41.103183: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.11.0
2022-02-25 16:50:41,748 - INFO - joeynmt.training - Total params: 105088
2022-02-25 16:50:41,749 - INFO - joeynmt.helpers -                           cfg.name : reverse_experiment
2022-02-25 16:50:41,749 - INFO - joeynmt.helpers -                       cfg.data.src : src
2022-02-25 16:50:41,749 - INFO - joeynmt.helpers -                       cfg.data.trg : trg
2022-02-25 16:50:41,749 - INFO - joeynmt.helpers -                     cfg.data.train : test/data/reverse/train
2022-02-25 16:50:41,749 - INFO - joeynmt.helpers -                       cfg.data.dev : test/data/reverse/dev
2022-02-25 16:50:41,749 - INFO - joeynmt.helpers -                      cfg.data.test : test/data/reverse/test
2022-02-25 16:50:41,749 - INFO - joeynmt.helpers -                     cfg.data.level : word
2022-02-25 16:50:41,749 - INFO - joeynmt.helpers -                 cfg.data.lowercase : False
2022-02-25 16:50:41,749 - INFO - joeynmt.helpers -           cfg.data.max_sent_length : 25
2022-02-25 16:50:41,749 - INFO - joeynmt.helpers -          cfg.data.src_voc_min_freq : 0
2022-02-25 16:50:41,749 - INFO - joeynmt.helpers -             cfg.data.src_voc_limit : 100
2022-02-25 16:50:41,749 - INFO - joeynmt.helpers -          cfg.data.trg_voc_min_freq : 0
2022-02-25 16:50:41,750 - INFO - joeynmt.helpers -             cfg.data.trg_voc_limit : 100
2022-02-25 16:50:41,750 - INFO - joeynmt.helpers -              cfg.testing.beam_size : 1
2022-02-25 16:50:41,750 - INFO - joeynmt.helpers -                  cfg.testing.alpha : 1.0
2022-02-25 16:50:41,750 - INFO - joeynmt.helpers -           cfg.training.random_seed : 42
2022-02-25 16:50:41,750 - INFO - joeynmt.helpers -             cfg.training.optimizer : adam
2022-02-25 16:50:41,750 - INFO - joeynmt.helpers -         cfg.training.learning_rate : 0.001
2022-02-25 16:50:41,750 - INFO - joeynmt.helpers -     cfg.training.learning_rate_min : 0.0002
2022-02-25 16:50:41,750 - INFO - joeynmt.helpers -          cfg.training.weight_decay : 0.0
2022-02-25 16:50:41,750 - INFO - joeynmt.helpers -        cfg.training.clip_grad_norm : 1.0
2022-02-25 16:50:41,750 - INFO - joeynmt.helpers -            cfg.training.batch_size : 10
2022-02-25 16:50:41,750 - INFO - joeynmt.helpers -            cfg.training.batch_type : sentence
2022-02-25 16:50:41,750 - INFO - joeynmt.helpers -            cfg.training.scheduling : plateau
2022-02-25 16:50:41,750 - INFO - joeynmt.helpers -              cfg.training.patience : 5
2022-02-25 16:50:41,750 - INFO - joeynmt.helpers -       cfg.training.decrease_factor : 0.5
2022-02-25 16:50:41,750 - INFO - joeynmt.helpers - cfg.training.early_stopping_metric : eval_metric
2022-02-25 16:50:41,750 - INFO - joeynmt.helpers -                cfg.training.epochs : 1
2022-02-25 16:50:41,750 - INFO - joeynmt.helpers -       cfg.training.validation_freq : 1000
2022-02-25 16:50:41,751 - INFO - joeynmt.helpers -          cfg.training.logging_freq : 100
2022-02-25 16:50:41,751 - INFO - joeynmt.helpers -           cfg.training.eval_metric : bleu
2022-02-25 16:50:41,751 - INFO - joeynmt.helpers -             cfg.training.model_dir : reverse_model
2022-02-25 16:50:41,751 - INFO - joeynmt.helpers -             cfg.training.overwrite : True
2022-02-25 16:50:41,751 - INFO - joeynmt.helpers -               cfg.training.shuffle : True
2022-02-25 16:50:41,751 - INFO - joeynmt.helpers -              cfg.training.use_cuda : False
2022-02-25 16:50:41,751 - INFO - joeynmt.helpers -     cfg.training.max_output_length : 30
2022-02-25 16:50:41,751 - INFO - joeynmt.helpers -     cfg.training.print_valid_sents : [0, 3, 6]
2022-02-25 16:50:41,751 - INFO - joeynmt.helpers -       cfg.training.keep_best_ckpts : 2
2022-02-25 16:50:41,751 - INFO - joeynmt.helpers -              cfg.model.initializer : xavier
2022-02-25 16:50:41,751 - INFO - joeynmt.helpers -        cfg.model.embed_initializer : normal
2022-02-25 16:50:41,751 - INFO - joeynmt.helpers -        cfg.model.embed_init_weight : 0.1
2022-02-25 16:50:41,751 - INFO - joeynmt.helpers -         cfg.model.bias_initializer : zeros
2022-02-25 16:50:41,751 - INFO - joeynmt.helpers -      cfg.model.init_rnn_orthogonal : False
2022-02-25 16:50:41,751 - INFO - joeynmt.helpers -         cfg.model.lstm_forget_gate : 0.0
2022-02-25 16:50:41,751 - INFO - joeynmt.helpers -         cfg.model.encoder.rnn_type : lstm
2022-02-25 16:50:41,752 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.embedding_dim : 16
2022-02-25 16:50:41,752 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.scale : False
2022-02-25 16:50:41,752 - INFO - joeynmt.helpers -      cfg.model.encoder.hidden_size : 64
2022-02-25 16:50:41,752 - INFO - joeynmt.helpers -    cfg.model.encoder.bidirectional : True
2022-02-25 16:50:41,752 - INFO - joeynmt.helpers -          cfg.model.encoder.dropout : 0.1
2022-02-25 16:50:41,752 - INFO - joeynmt.helpers -       cfg.model.encoder.num_layers : 1
2022-02-25 16:50:41,752 - INFO - joeynmt.helpers -         cfg.model.decoder.rnn_type : lstm
2022-02-25 16:50:41,752 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.embedding_dim : 16
2022-02-25 16:50:41,752 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.scale : False
2022-02-25 16:50:41,752 - INFO - joeynmt.helpers -      cfg.model.decoder.hidden_size : 64
2022-02-25 16:50:41,752 - INFO - joeynmt.helpers -          cfg.model.decoder.dropout : 0.1
2022-02-25 16:50:41,752 - INFO - joeynmt.helpers -   cfg.model.decoder.hidden_dropout : 0.1
2022-02-25 16:50:41,752 - INFO - joeynmt.helpers -       cfg.model.decoder.num_layers : 1
2022-02-25 16:50:41,752 - INFO - joeynmt.helpers -    cfg.model.decoder.input_feeding : True
2022-02-25 16:50:41,752 - INFO - joeynmt.helpers -      cfg.model.decoder.init_hidden : zero
2022-02-25 16:50:41,752 - INFO - joeynmt.helpers -        cfg.model.decoder.attention : luong
2022-02-25 16:50:41,753 - INFO - joeynmt.helpers - Data set sizes: 
	train 50000,
	valid 1000,
	test 1000
2022-02-25 16:50:41,753 - INFO - joeynmt.helpers - First training example:
	[SRC] 28 14 42 7 20 38 18
	[TRG] 18 38 20 7 42 14 28
2022-02-25 16:50:41,753 - INFO - joeynmt.helpers - First 10 words (src): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) 15 (5) 35 (6) 44 (7) 18 (8) 36 (9) 16
2022-02-25 16:50:41,753 - INFO - joeynmt.helpers - First 10 words (trg): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) 15 (5) 35 (6) 44 (7) 18 (8) 36 (9) 16
2022-02-25 16:50:41,753 - INFO - joeynmt.helpers - Number of Src words (types): 54
2022-02-25 16:50:41,753 - INFO - joeynmt.helpers - Number of Trg words (types): 54
2022-02-25 16:50:41,753 - INFO - joeynmt.training - Model(
	encoder=RecurrentEncoder(LSTM(16, 64, batch_first=True, bidirectional=True)),
	decoder=RecurrentDecoder(rnn=LSTM(80, 64, batch_first=True), attention=LuongAttention),
	src_embed=Embeddings(embedding_dim=16, vocab_size=54),
	trg_embed=Embeddings(embedding_dim=16, vocab_size=54))
2022-02-25 16:50:41,754 - INFO - joeynmt.training - Train stats:
	device: cpu
	n_gpu: 0
	16-bits training: False
	gradient accumulation: 1
	batch size per device: 10
	total batch size (w. parallel & accumulation): 10
2022-02-25 16:50:41,754 - INFO - joeynmt.training - EPOCH 1
2022-02-25 16:50:45,669 - INFO - joeynmt.training - Epoch   1, Step:      100, Batch Loss:    53.850666, Tokens per Sec:     3478, Lr: 0.001000
2022-02-25 16:50:49,586 - INFO - joeynmt.training - Epoch   1, Step:      200, Batch Loss:    66.041504, Tokens per Sec:     3611, Lr: 0.001000
2022-02-25 16:50:54,495 - INFO - joeynmt.training - Epoch   1, Step:      300, Batch Loss:    53.775745, Tokens per Sec:     2839, Lr: 0.001000
2022-02-25 16:50:59,814 - INFO - joeynmt.training - Epoch   1, Step:      400, Batch Loss:    46.204933, Tokens per Sec:     2674, Lr: 0.001000
2022-02-25 16:51:03,973 - INFO - joeynmt.training - Epoch   1, Step:      500, Batch Loss:    42.466156, Tokens per Sec:     3338, Lr: 0.001000
2022-02-25 16:51:07,892 - INFO - joeynmt.training - Epoch   1, Step:      600, Batch Loss:    47.798969, Tokens per Sec:     3588, Lr: 0.001000
2022-02-25 16:51:11,937 - INFO - joeynmt.training - Epoch   1, Step:      700, Batch Loss:    43.076118, Tokens per Sec:     3426, Lr: 0.001000
2022-02-25 16:51:15,870 - INFO - joeynmt.training - Epoch   1, Step:      800, Batch Loss:    32.452343, Tokens per Sec:     3517, Lr: 0.001000
2022-02-25 16:51:19,817 - INFO - joeynmt.training - Epoch   1, Step:      900, Batch Loss:    40.858349, Tokens per Sec:     3558, Lr: 0.001000
2022-02-25 16:51:23,974 - INFO - joeynmt.training - Epoch   1, Step:     1000, Batch Loss:    20.104404, Tokens per Sec:     3355, Lr: 0.001000
2022-02-25 16:51:27,195 - INFO - joeynmt.training - Hooray! New best validation result [eval_metric]!
2022-02-25 16:51:27,198 - INFO - joeynmt.training - Example #0
2022-02-25 16:51:27,198 - INFO - joeynmt.training - 	Source:     33 9 15 3 14 33 32 42 23 12 14 17 4 35 0 48 46 36 46 27 2 34 35 17 36 39 7 14 9 0
2022-02-25 16:51:27,198 - INFO - joeynmt.training - 	Reference:  0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 4 17 14 12 23 42 32 33 14 3 15 9 33
2022-02-25 16:51:27,198 - INFO - joeynmt.training - 	Hypothesis: 0 9 14 33 39 36 17 35 10 2 27 27 22 46 46 48 7 8 4 14 42 32 9 9 9 9 33 33 33 33
2022-02-25 16:51:27,198 - INFO - joeynmt.training - Example #3
2022-02-25 16:51:27,198 - INFO - joeynmt.training - 	Source:     10 43 37 32 6 9 25 36 21 29 16 7 18 27 30 46 37 15 7 48 18
2022-02-25 16:51:27,198 - INFO - joeynmt.training - 	Reference:  18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
2022-02-25 16:51:27,198 - INFO - joeynmt.training - 	Hypothesis: 18 48 9 15 37 46 30 27 18 18 16 29 21 22 25 25 9 41 2 43 43 43
2022-02-25 16:51:27,198 - INFO - joeynmt.training - Example #6
2022-02-25 16:51:27,198 - INFO - joeynmt.training - 	Source:     0 38 14 26 20 34 10 36 11 32 29 21
2022-02-25 16:51:27,198 - INFO - joeynmt.training - 	Reference:  21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 16:51:27,198 - INFO - joeynmt.training - 	Hypothesis: 21 29 32 11 36 10 10 20 26 14 40
2022-02-25 16:51:27,198 - INFO - joeynmt.training - Validation result (greedy) at epoch   1, step     1000: bleu:  50.36, loss: 29904.3535, ppl:   6.2480, duration: 3.2240s
2022-02-25 16:51:32,384 - INFO - joeynmt.training - Epoch   1, Step:     1100, Batch Loss:    22.845684, Tokens per Sec:     2660, Lr: 0.001000
2022-02-25 16:51:36,414 - INFO - joeynmt.training - Epoch   1, Step:     1200, Batch Loss:    22.456341, Tokens per Sec:     3503, Lr: 0.001000
2022-02-25 16:51:40,418 - INFO - joeynmt.training - Epoch   1, Step:     1300, Batch Loss:    22.778179, Tokens per Sec:     3527, Lr: 0.001000
2022-02-25 16:51:44,488 - INFO - joeynmt.training - Epoch   1, Step:     1400, Batch Loss:    15.911810, Tokens per Sec:     3421, Lr: 0.001000
2022-02-25 16:51:49,615 - INFO - joeynmt.training - Epoch   1, Step:     1500, Batch Loss:    17.996113, Tokens per Sec:     2750, Lr: 0.001000
2022-02-25 16:51:55,084 - INFO - joeynmt.training - Epoch   1, Step:     1600, Batch Loss:    26.362797, Tokens per Sec:     2577, Lr: 0.001000
2022-02-25 16:51:59,893 - INFO - joeynmt.training - Epoch   1, Step:     1700, Batch Loss:     2.797748, Tokens per Sec:     2832, Lr: 0.001000
2022-02-25 16:52:04,855 - INFO - joeynmt.training - Epoch   1, Step:     1800, Batch Loss:    10.014632, Tokens per Sec:     2810, Lr: 0.001000
2022-02-25 16:52:09,370 - INFO - joeynmt.training - Epoch   1, Step:     1900, Batch Loss:     5.577150, Tokens per Sec:     3097, Lr: 0.001000
2022-02-25 16:52:14,141 - INFO - joeynmt.training - Epoch   1, Step:     2000, Batch Loss:     7.863119, Tokens per Sec:     3004, Lr: 0.001000
2022-02-25 16:52:18,395 - INFO - joeynmt.training - Hooray! New best validation result [eval_metric]!
2022-02-25 16:52:18,399 - INFO - joeynmt.training - Example #0
2022-02-25 16:52:18,399 - INFO - joeynmt.training - 	Source:     33 9 15 3 14 33 32 42 23 12 14 17 4 35 0 48 46 36 46 27 2 34 35 17 36 39 7 14 9 0
2022-02-25 16:52:18,399 - INFO - joeynmt.training - 	Reference:  0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 4 17 14 12 23 42 32 33 14 3 15 9 33
2022-02-25 16:52:18,399 - INFO - joeynmt.training - 	Hypothesis: 0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 17 17 12 12 23 7 39 39 36 17 35 2 2
2022-02-25 16:52:18,399 - INFO - joeynmt.training - Example #3
2022-02-25 16:52:18,399 - INFO - joeynmt.training - 	Source:     10 43 37 32 6 9 25 36 21 29 16 7 18 27 30 46 37 15 7 48 18
2022-02-25 16:52:18,399 - INFO - joeynmt.training - 	Reference:  18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
2022-02-25 16:52:18,399 - INFO - joeynmt.training - 	Hypothesis: 18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
2022-02-25 16:52:18,399 - INFO - joeynmt.training - Example #6
2022-02-25 16:52:18,399 - INFO - joeynmt.training - 	Source:     0 38 14 26 20 34 10 36 11 32 29 21
2022-02-25 16:52:18,399 - INFO - joeynmt.training - 	Reference:  21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 16:52:18,399 - INFO - joeynmt.training - 	Hypothesis: 21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 16:52:18,399 - INFO - joeynmt.training - Validation result (greedy) at epoch   1, step     2000: bleu:  83.59, loss: 25864.3789, ppl:   4.8780, duration: 4.2582s
2022-02-25 16:52:25,245 - INFO - joeynmt.training - Epoch   1, Step:     2100, Batch Loss:     2.236318, Tokens per Sec:     2042, Lr: 0.001000
2022-02-25 16:52:29,824 - INFO - joeynmt.training - Epoch   1, Step:     2200, Batch Loss:    22.793039, Tokens per Sec:     3031, Lr: 0.001000
2022-02-25 16:52:35,279 - INFO - joeynmt.training - Epoch   1, Step:     2300, Batch Loss:     5.545212, Tokens per Sec:     2578, Lr: 0.001000
2022-02-25 16:52:40,838 - INFO - joeynmt.training - Epoch   1, Step:     2400, Batch Loss:     4.159322, Tokens per Sec:     2572, Lr: 0.001000
2022-02-25 16:52:46,092 - INFO - joeynmt.training - Epoch   1, Step:     2500, Batch Loss:     1.014469, Tokens per Sec:     2636, Lr: 0.001000
2022-02-25 16:52:50,254 - INFO - joeynmt.training - Epoch   1, Step:     2600, Batch Loss:     7.540004, Tokens per Sec:     3346, Lr: 0.001000
2022-02-25 16:52:54,676 - INFO - joeynmt.training - Epoch   1, Step:     2700, Batch Loss:     0.495534, Tokens per Sec:     3087, Lr: 0.001000
2022-02-25 16:52:59,025 - INFO - joeynmt.training - Epoch   1, Step:     2800, Batch Loss:     1.346067, Tokens per Sec:     3219, Lr: 0.001000
2022-02-25 16:53:03,204 - INFO - joeynmt.training - Epoch   1, Step:     2900, Batch Loss:     0.313974, Tokens per Sec:     3365, Lr: 0.001000
2022-02-25 16:53:08,480 - INFO - joeynmt.training - Epoch   1, Step:     3000, Batch Loss:     0.621481, Tokens per Sec:     2672, Lr: 0.001000
2022-02-25 16:53:12,642 - INFO - joeynmt.training - Hooray! New best validation result [eval_metric]!
2022-02-25 16:53:12,645 - INFO - joeynmt.helpers - delete reverse_model/1000.ckpt
2022-02-25 16:53:12,645 - INFO - joeynmt.training - Example #0
2022-02-25 16:53:12,645 - INFO - joeynmt.training - 	Source:     33 9 15 3 14 33 32 42 23 12 14 17 4 35 0 48 46 36 46 27 2 34 35 17 36 39 7 14 9 0
2022-02-25 16:53:12,645 - INFO - joeynmt.training - 	Reference:  0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 4 17 14 12 23 42 32 33 14 3 15 9 33
2022-02-25 16:53:12,645 - INFO - joeynmt.training - 	Hypothesis: 0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 4 17 14 12 12 23 32 38 34 2 27 9 33
2022-02-25 16:53:12,645 - INFO - joeynmt.training - Example #3
2022-02-25 16:53:12,645 - INFO - joeynmt.training - 	Source:     10 43 37 32 6 9 25 36 21 29 16 7 18 27 30 46 37 15 7 48 18
2022-02-25 16:53:12,645 - INFO - joeynmt.training - 	Reference:  18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
2022-02-25 16:53:12,645 - INFO - joeynmt.training - 	Hypothesis: 18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
2022-02-25 16:53:12,645 - INFO - joeynmt.training - Example #6
2022-02-25 16:53:12,646 - INFO - joeynmt.training - 	Source:     0 38 14 26 20 34 10 36 11 32 29 21
2022-02-25 16:53:12,646 - INFO - joeynmt.training - 	Reference:  21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 16:53:12,646 - INFO - joeynmt.training - 	Hypothesis: 21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 16:53:12,646 - INFO - joeynmt.training - Validation result (greedy) at epoch   1, step     3000: bleu:  91.19, loss: 18124.3750, ppl:   3.0359, duration: 4.1657s
2022-02-25 16:53:17,971 - INFO - joeynmt.training - Epoch   1, Step:     3100, Batch Loss:     5.290173, Tokens per Sec:     2601, Lr: 0.001000
2022-02-25 16:53:21,989 - INFO - joeynmt.training - Epoch   1, Step:     3200, Batch Loss:     0.257176, Tokens per Sec:     3399, Lr: 0.001000
2022-02-25 16:53:28,302 - INFO - joeynmt.training - Epoch   1, Step:     3300, Batch Loss:     0.815733, Tokens per Sec:     2183, Lr: 0.001000
2022-02-25 16:53:33,818 - INFO - joeynmt.training - Epoch   1, Step:     3400, Batch Loss:     5.961339, Tokens per Sec:     2546, Lr: 0.001000
2022-02-25 16:53:39,416 - INFO - joeynmt.training - Epoch   1, Step:     3500, Batch Loss:     1.077253, Tokens per Sec:     2551, Lr: 0.001000
2022-02-25 16:53:43,474 - INFO - joeynmt.training - Epoch   1, Step:     3600, Batch Loss:     0.124250, Tokens per Sec:     3458, Lr: 0.001000
2022-02-25 16:53:48,927 - INFO - joeynmt.training - Epoch   1, Step:     3700, Batch Loss:     0.544841, Tokens per Sec:     2606, Lr: 0.001000
2022-02-25 16:53:55,126 - INFO - joeynmt.training - Epoch   1, Step:     3800, Batch Loss:     0.043265, Tokens per Sec:     2230, Lr: 0.001000
2022-02-25 16:53:59,352 - INFO - joeynmt.training - Epoch   1, Step:     3900, Batch Loss:     2.352964, Tokens per Sec:     3325, Lr: 0.001000
2022-02-25 16:54:03,654 - INFO - joeynmt.training - Epoch   1, Step:     4000, Batch Loss:     0.063842, Tokens per Sec:     3269, Lr: 0.001000
2022-02-25 16:54:06,600 - INFO - joeynmt.helpers - delete reverse_model/2000.ckpt
2022-02-25 16:54:06,601 - INFO - joeynmt.training - Example #0
2022-02-25 16:54:06,601 - INFO - joeynmt.training - 	Source:     33 9 15 3 14 33 32 42 23 12 14 17 4 35 0 48 46 36 46 27 2 34 35 17 36 39 7 14 9 0
2022-02-25 16:54:06,601 - INFO - joeynmt.training - 	Reference:  0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 4 17 14 12 23 42 32 33 14 3 15 9 33
2022-02-25 16:54:06,601 - INFO - joeynmt.training - 	Hypothesis: 0 9 14 7 39 36 17 35 34 2 33 46 36 46 48 0 35 4 17 14 12 23 42 32 33 14 46 36 46 48
2022-02-25 16:54:06,601 - INFO - joeynmt.training - Example #3
2022-02-25 16:54:06,601 - INFO - joeynmt.training - 	Source:     10 43 37 32 6 9 25 36 21 29 16 7 18 27 30 46 37 15 7 48 18
2022-02-25 16:54:06,601 - INFO - joeynmt.training - 	Reference:  18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
2022-02-25 16:54:06,601 - INFO - joeynmt.training - 	Hypothesis: 18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
2022-02-25 16:54:06,601 - INFO - joeynmt.training - Example #6
2022-02-25 16:54:06,601 - INFO - joeynmt.training - 	Source:     0 38 14 26 20 34 10 36 11 32 29 21
2022-02-25 16:54:06,601 - INFO - joeynmt.training - 	Reference:  21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 16:54:06,601 - INFO - joeynmt.training - 	Hypothesis: 21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 16:54:06,601 - INFO - joeynmt.training - Validation result (greedy) at epoch   1, step     4000: bleu:  86.92, loss: 31391.9785, ppl:   6.8443, duration: 2.9473s
2022-02-25 16:54:12,384 - INFO - joeynmt.training - Epoch   1, Step:     4100, Batch Loss:     0.054932, Tokens per Sec:     2415, Lr: 0.001000
2022-02-25 16:54:17,980 - INFO - joeynmt.training - Epoch   1, Step:     4200, Batch Loss:     2.978068, Tokens per Sec:     2444, Lr: 0.001000
2022-02-25 16:54:22,839 - INFO - joeynmt.training - Epoch   1, Step:     4300, Batch Loss:     0.074170, Tokens per Sec:     2903, Lr: 0.001000
2022-02-25 16:54:28,040 - INFO - joeynmt.training - Epoch   1, Step:     4400, Batch Loss:     0.025495, Tokens per Sec:     2576, Lr: 0.001000
2022-02-25 16:54:32,767 - INFO - joeynmt.training - Epoch   1, Step:     4500, Batch Loss:     1.219658, Tokens per Sec:     2951, Lr: 0.001000
2022-02-25 16:54:37,771 - INFO - joeynmt.training - Epoch   1, Step:     4600, Batch Loss:     7.716228, Tokens per Sec:     2726, Lr: 0.001000
2022-02-25 16:54:45,087 - INFO - joeynmt.training - Epoch   1, Step:     4700, Batch Loss:     0.053380, Tokens per Sec:     1905, Lr: 0.001000
2022-02-25 16:54:49,580 - INFO - joeynmt.training - Epoch   1, Step:     4800, Batch Loss:    22.972399, Tokens per Sec:     3115, Lr: 0.001000
2022-02-25 16:54:53,999 - INFO - joeynmt.training - Epoch   1, Step:     4900, Batch Loss:     0.012751, Tokens per Sec:     3234, Lr: 0.001000
2022-02-25 16:54:58,220 - INFO - joeynmt.training - Epoch   1, Step:     5000, Batch Loss:     0.094934, Tokens per Sec:     3340, Lr: 0.001000
2022-02-25 16:55:01,566 - INFO - joeynmt.training - Hooray! New best validation result [eval_metric]!
2022-02-25 16:55:01,569 - INFO - joeynmt.helpers - delete reverse_model/4000.ckpt
2022-02-25 16:55:01,569 - INFO - joeynmt.training - Example #0
2022-02-25 16:55:01,570 - INFO - joeynmt.training - 	Source:     33 9 15 3 14 33 32 42 23 12 14 17 4 35 0 48 46 36 46 27 2 34 35 17 36 39 7 14 9 0
2022-02-25 16:55:01,570 - INFO - joeynmt.training - 	Reference:  0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 4 17 14 12 23 42 32 33 14 3 15 9 33
2022-02-25 16:55:01,570 - INFO - joeynmt.training - 	Hypothesis: 0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 4 17 14 12 23 42 32 33 14 3 15 46 33
2022-02-25 16:55:01,570 - INFO - joeynmt.training - Example #3
2022-02-25 16:55:01,570 - INFO - joeynmt.training - 	Source:     10 43 37 32 6 9 25 36 21 29 16 7 18 27 30 46 37 15 7 48 18
2022-02-25 16:55:01,570 - INFO - joeynmt.training - 	Reference:  18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
2022-02-25 16:55:01,570 - INFO - joeynmt.training - 	Hypothesis: 18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
2022-02-25 16:55:01,570 - INFO - joeynmt.training - Example #6
2022-02-25 16:55:01,570 - INFO - joeynmt.training - 	Source:     0 38 14 26 20 34 10 36 11 32 29 21
2022-02-25 16:55:01,570 - INFO - joeynmt.training - 	Reference:  21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 16:55:01,570 - INFO - joeynmt.training - 	Hypothesis: 21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 16:55:01,570 - INFO - joeynmt.training - Validation result (greedy) at epoch   1, step     5000: bleu:  96.32, loss: 9381.9082, ppl:   1.7768, duration: 3.3498s
2022-02-25 16:55:02,403 - INFO - joeynmt.training - Epoch   1: total training loss 71639.21
2022-02-25 16:55:02,405 - INFO - joeynmt.training - Training ended after   1 epochs.
2022-02-25 16:55:02,405 - INFO - joeynmt.training - Best validation result (greedy) at step     5000:  96.32 eval_metric.
2022-02-25 16:55:02,413 - INFO - joeynmt.prediction - Process device: cpu, n_gpu: 0, batch_size per device: 10
2022-02-25 16:55:02,413 - INFO - joeynmt.prediction - Loading model from reverse_model/5000.ckpt
2022-02-25 16:55:02,414 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-25 16:55:02,416 - INFO - joeynmt.model - Enc-dec model built.
2022-02-25 16:55:02,417 - INFO - joeynmt.prediction - Decoding on dev set (test/data/reverse/dev.trg)...
2022-02-25 16:55:04,433 - INFO - joeynmt.prediction -  dev bleu[13a]:  96.32 [Greedy decoding]
2022-02-25 16:55:04,433 - INFO - joeynmt.prediction - Translations saved to: reverse_model/00005000.hyps.dev
2022-02-25 16:55:04,433 - INFO - joeynmt.prediction - Decoding on test set (test/data/reverse/test.trg)...
2022-02-25 16:55:06,579 - INFO - joeynmt.prediction - test bleu[13a]:  96.04 [Greedy decoding]
2022-02-25 16:55:06,579 - INFO - joeynmt.prediction - Translations saved to: reverse_model/00005000.hyps.test

real	4m27.385s
user	32m11.147s
sys	0m10.875s
(joey) ye@:~/exp/joeynmt$ 
```

## Training with GPU

config ဖိုင်မှာ cuda သုံးမယ် ဆိုတာကို on ပေးလိုက်တယ်...  

```
    model_dir: "reverse_model"
    overwrite: True
    shuffle: True
    use_cuda: True
```

ပြီးတော့ run ကြည့်ခဲ့တယ်...  

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/reverse.yaml
2022-02-25 16:57:38,568 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-25 16:57:38,584 - INFO - joeynmt.data - Loading training data...
2022-02-25 16:57:38,871 - INFO - joeynmt.data - Building vocabulary...
2022-02-25 16:57:38,983 - INFO - joeynmt.data - Loading dev data...
2022-02-25 16:57:38,989 - INFO - joeynmt.data - Loading test data...
2022-02-25 16:57:38,992 - INFO - joeynmt.data - Data loaded.
2022-02-25 16:57:38,992 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-25 16:57:38,995 - INFO - joeynmt.model - Enc-dec model built.
2022-02-25 16:57:39.069187: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.11.0
2022-02-25 16:57:39,716 - INFO - joeynmt.training - Total params: 105088
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -                           cfg.name : reverse_experiment
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -                       cfg.data.src : src
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -                       cfg.data.trg : trg
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -                     cfg.data.train : test/data/reverse/train
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -                       cfg.data.dev : test/data/reverse/dev
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -                      cfg.data.test : test/data/reverse/test
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -                     cfg.data.level : word
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -                 cfg.data.lowercase : False
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -           cfg.data.max_sent_length : 25
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -          cfg.data.src_voc_min_freq : 0
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -             cfg.data.src_voc_limit : 100
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -          cfg.data.trg_voc_min_freq : 0
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -             cfg.data.trg_voc_limit : 100
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -              cfg.testing.beam_size : 1
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -                  cfg.testing.alpha : 1.0
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -           cfg.training.random_seed : 42
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -             cfg.training.optimizer : adam
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -         cfg.training.learning_rate : 0.001
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -     cfg.training.learning_rate_min : 0.0002
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -          cfg.training.weight_decay : 0.0
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -        cfg.training.clip_grad_norm : 1.0
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -            cfg.training.batch_size : 10
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -            cfg.training.batch_type : sentence
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -            cfg.training.scheduling : plateau
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -              cfg.training.patience : 5
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers -       cfg.training.decrease_factor : 0.5
2022-02-25 16:57:41,941 - INFO - joeynmt.helpers - cfg.training.early_stopping_metric : eval_metric
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -                cfg.training.epochs : 1
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -       cfg.training.validation_freq : 1000
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -          cfg.training.logging_freq : 100
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -           cfg.training.eval_metric : bleu
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -             cfg.training.model_dir : reverse_model
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -             cfg.training.overwrite : True
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -               cfg.training.shuffle : True
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -              cfg.training.use_cuda : True
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -     cfg.training.max_output_length : 30
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -     cfg.training.print_valid_sents : [0, 3, 6]
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -       cfg.training.keep_best_ckpts : 2
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -              cfg.model.initializer : xavier
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -        cfg.model.embed_initializer : normal
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -        cfg.model.embed_init_weight : 0.1
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -         cfg.model.bias_initializer : zeros
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -      cfg.model.init_rnn_orthogonal : False
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -         cfg.model.lstm_forget_gate : 0.0
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -         cfg.model.encoder.rnn_type : lstm
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.embedding_dim : 16
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.scale : False
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -      cfg.model.encoder.hidden_size : 64
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -    cfg.model.encoder.bidirectional : True
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -          cfg.model.encoder.dropout : 0.1
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -       cfg.model.encoder.num_layers : 1
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -         cfg.model.decoder.rnn_type : lstm
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.embedding_dim : 16
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.scale : False
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -      cfg.model.decoder.hidden_size : 64
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -          cfg.model.decoder.dropout : 0.1
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -   cfg.model.decoder.hidden_dropout : 0.1
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -       cfg.model.decoder.num_layers : 1
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -    cfg.model.decoder.input_feeding : True
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -      cfg.model.decoder.init_hidden : zero
2022-02-25 16:57:41,942 - INFO - joeynmt.helpers -        cfg.model.decoder.attention : luong
2022-02-25 16:57:41,943 - INFO - joeynmt.helpers - Data set sizes: 
	train 50000,
	valid 1000,
	test 1000
2022-02-25 16:57:41,943 - INFO - joeynmt.helpers - First training example:
	[SRC] 28 14 42 7 20 38 18
	[TRG] 18 38 20 7 42 14 28
2022-02-25 16:57:41,943 - INFO - joeynmt.helpers - First 10 words (src): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) 15 (5) 35 (6) 44 (7) 18 (8) 36 (9) 16
2022-02-25 16:57:41,943 - INFO - joeynmt.helpers - First 10 words (trg): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) 15 (5) 35 (6) 44 (7) 18 (8) 36 (9) 16
2022-02-25 16:57:41,943 - INFO - joeynmt.helpers - Number of Src words (types): 54
2022-02-25 16:57:41,943 - INFO - joeynmt.helpers - Number of Trg words (types): 54
2022-02-25 16:57:41,943 - INFO - joeynmt.training - Model(
	encoder=RecurrentEncoder(LSTM(16, 64, batch_first=True, bidirectional=True)),
	decoder=RecurrentDecoder(rnn=LSTM(80, 64, batch_first=True), attention=LuongAttention),
	src_embed=Embeddings(embedding_dim=16, vocab_size=54),
	trg_embed=Embeddings(embedding_dim=16, vocab_size=54))
2022-02-25 16:57:41,943 - INFO - joeynmt.training - Train stats:
	device: cuda
	n_gpu: 2
	16-bits training: False
	gradient accumulation: 1
	batch size per device: 5
	total batch size (w. parallel & accumulation): 10
2022-02-25 16:57:41,943 - INFO - joeynmt.training - EPOCH 1
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:694: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, batch_sizes, hx, self._flat_weights, self.bias,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:691: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/_functions.py:68: UserWarning: Was asked to gather along dimension 0, but all input tensors were scalars; will instead unsqueeze and return a vector.
  warnings.warn('Was asked to gather along dimension 0, but all '
2022-02-25 16:57:47,155 - INFO - joeynmt.training - Epoch   1, Step:      100, Batch Loss:    26.863581, Tokens per Sec:     2613, Lr: 0.001000
2022-02-25 16:57:50,605 - INFO - joeynmt.training - Epoch   1, Step:      200, Batch Loss:    32.623943, Tokens per Sec:     4100, Lr: 0.001000
2022-02-25 16:57:54,155 - INFO - joeynmt.training - Epoch   1, Step:      300, Batch Loss:    26.875950, Tokens per Sec:     3926, Lr: 0.001000
2022-02-25 16:57:57,682 - INFO - joeynmt.training - Epoch   1, Step:      400, Batch Loss:    23.177490, Tokens per Sec:     4033, Lr: 0.001000
2022-02-25 16:58:01,303 - INFO - joeynmt.training - Epoch   1, Step:      500, Batch Loss:    21.018108, Tokens per Sec:     3835, Lr: 0.001000
2022-02-25 16:58:04,838 - INFO - joeynmt.training - Epoch   1, Step:      600, Batch Loss:    23.882730, Tokens per Sec:     3978, Lr: 0.001000
2022-02-25 16:58:08,306 - INFO - joeynmt.training - Epoch   1, Step:      700, Batch Loss:    19.991211, Tokens per Sec:     3996, Lr: 0.001000
2022-02-25 16:58:11,761 - INFO - joeynmt.training - Epoch   1, Step:      800, Batch Loss:    13.857175, Tokens per Sec:     4004, Lr: 0.001000
2022-02-25 16:58:15,212 - INFO - joeynmt.training - Epoch   1, Step:      900, Batch Loss:    17.809200, Tokens per Sec:     4069, Lr: 0.001000
2022-02-25 16:58:18,733 - INFO - joeynmt.training - Epoch   1, Step:     1000, Batch Loss:     9.078739, Tokens per Sec:     3962, Lr: 0.001000
2022-02-25 16:58:29,036 - INFO - joeynmt.training - Hooray! New best validation result [eval_metric]!
2022-02-25 16:58:29,042 - INFO - joeynmt.training - Example #0
2022-02-25 16:58:29,043 - INFO - joeynmt.training - 	Source:     33 9 15 3 14 33 32 42 23 12 14 17 4 35 0 48 46 36 46 27 2 34 35 17 36 39 7 14 9 0
2022-02-25 16:58:29,043 - INFO - joeynmt.training - 	Reference:  0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 4 17 14 12 23 42 32 33 14 3 15 9 33
2022-02-25 16:58:29,043 - INFO - joeynmt.training - 	Hypothesis: 0 9 14 7 39 36 17 35 34 2 27 46 22 46 46 0 0 0 18 16 16 16 16 9 9 9 9 9 9 33
2022-02-25 16:58:29,043 - INFO - joeynmt.training - Example #3
2022-02-25 16:58:29,043 - INFO - joeynmt.training - 	Source:     10 43 37 32 6 9 25 36 21 29 16 7 18 27 30 46 37 15 7 48 18
2022-02-25 16:58:29,043 - INFO - joeynmt.training - 	Reference:  18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
2022-02-25 16:58:29,043 - INFO - joeynmt.training - 	Hypothesis: 18 48 7 15 37 46 30 27 18 18 16 29 21 25 25 25 41 41 0 43
2022-02-25 16:58:29,043 - INFO - joeynmt.training - Example #6
2022-02-25 16:58:29,043 - INFO - joeynmt.training - 	Source:     0 38 14 26 20 34 10 36 11 32 29 21
2022-02-25 16:58:29,043 - INFO - joeynmt.training - 	Reference:  21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 16:58:29,043 - INFO - joeynmt.training - 	Hypothesis: 21 29 32 11 36 10 34 20 26 14 14 0
2022-02-25 16:58:29,043 - INFO - joeynmt.training - Validation result (greedy) at epoch   1, step     1000: bleu:  58.32, loss: 13479.4971, ppl:   2.2839, duration: 10.3099s
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:694: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, batch_sizes, hx, self._flat_weights, self.bias,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:691: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/_functions.py:68: UserWarning: Was asked to gather along dimension 0, but all input tensors were scalars; will instead unsqueeze and return a vector.
  warnings.warn('Was asked to gather along dimension 0, but all '
2022-02-25 16:58:33,521 - INFO - joeynmt.training - Epoch   1, Step:     1100, Batch Loss:    11.696822, Tokens per Sec:     3081, Lr: 0.001000
2022-02-25 16:58:37,012 - INFO - joeynmt.training - Epoch   1, Step:     1200, Batch Loss:    15.892814, Tokens per Sec:     4043, Lr: 0.001000
2022-02-25 16:58:40,629 - INFO - joeynmt.training - Epoch   1, Step:     1300, Batch Loss:    13.630435, Tokens per Sec:     3904, Lr: 0.001000
2022-02-25 16:58:44,093 - INFO - joeynmt.training - Epoch   1, Step:     1400, Batch Loss:     7.677674, Tokens per Sec:     4020, Lr: 0.001000
2022-02-25 16:58:47,622 - INFO - joeynmt.training - Epoch   1, Step:     1500, Batch Loss:     6.754305, Tokens per Sec:     3996, Lr: 0.001000
2022-02-25 16:58:51,115 - INFO - joeynmt.training - Epoch   1, Step:     1600, Batch Loss:    16.463957, Tokens per Sec:     4036, Lr: 0.001000
2022-02-25 16:58:54,623 - INFO - joeynmt.training - Epoch   1, Step:     1700, Batch Loss:     2.009682, Tokens per Sec:     3882, Lr: 0.001000
2022-02-25 16:58:58,114 - INFO - joeynmt.training - Epoch   1, Step:     1800, Batch Loss:     2.418900, Tokens per Sec:     3994, Lr: 0.001000
2022-02-25 16:59:01,598 - INFO - joeynmt.training - Epoch   1, Step:     1900, Batch Loss:     1.804115, Tokens per Sec:     4013, Lr: 0.001000
2022-02-25 16:59:05,115 - INFO - joeynmt.training - Epoch   1, Step:     2000, Batch Loss:     1.457934, Tokens per Sec:     4075, Lr: 0.001000
2022-02-25 16:59:16,287 - INFO - joeynmt.training - Hooray! New best validation result [eval_metric]!
2022-02-25 16:59:16,292 - INFO - joeynmt.training - Example #0
2022-02-25 16:59:16,292 - INFO - joeynmt.training - 	Source:     33 9 15 3 14 33 32 42 23 12 14 17 4 35 0 48 46 36 46 27 2 34 35 17 36 39 7 14 9 0
2022-02-25 16:59:16,292 - INFO - joeynmt.training - 	Reference:  0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 4 17 14 12 23 42 32 33 14 3 15 9 33
2022-02-25 16:59:16,292 - INFO - joeynmt.training - 	Hypothesis: 0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 4 17 14 12 23 42 15 24 33 33
2022-02-25 16:59:16,292 - INFO - joeynmt.training - Example #3
2022-02-25 16:59:16,292 - INFO - joeynmt.training - 	Source:     10 43 37 32 6 9 25 36 21 29 16 7 18 27 30 46 37 15 7 48 18
2022-02-25 16:59:16,292 - INFO - joeynmt.training - 	Reference:  18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
2022-02-25 16:59:16,292 - INFO - joeynmt.training - 	Hypothesis: 18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
2022-02-25 16:59:16,292 - INFO - joeynmt.training - Example #6
2022-02-25 16:59:16,292 - INFO - joeynmt.training - 	Source:     0 38 14 26 20 34 10 36 11 32 29 21
2022-02-25 16:59:16,292 - INFO - joeynmt.training - 	Reference:  21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 16:59:16,292 - INFO - joeynmt.training - 	Hypothesis: 21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 16:59:16,292 - INFO - joeynmt.training - Validation result (greedy) at epoch   1, step     2000: bleu:  88.28, loss: 4554.0200, ppl:   1.3218, duration: 11.1767s
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:694: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, batch_sizes, hx, self._flat_weights, self.bias,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:691: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/_functions.py:68: UserWarning: Was asked to gather along dimension 0, but all input tensors were scalars; will instead unsqueeze and return a vector.
  warnings.warn('Was asked to gather along dimension 0, but all '
2022-02-25 16:59:20,690 - INFO - joeynmt.training - Epoch   1, Step:     2100, Batch Loss:     1.533344, Tokens per Sec:     3179, Lr: 0.001000
2022-02-25 16:59:24,235 - INFO - joeynmt.training - Epoch   1, Step:     2200, Batch Loss:     2.824706, Tokens per Sec:     3915, Lr: 0.001000
2022-02-25 16:59:27,762 - INFO - joeynmt.training - Epoch   1, Step:     2300, Batch Loss:     2.699212, Tokens per Sec:     3987, Lr: 0.001000
2022-02-25 16:59:31,290 - INFO - joeynmt.training - Epoch   1, Step:     2400, Batch Loss:     7.115499, Tokens per Sec:     4051, Lr: 0.001000
2022-02-25 16:59:34,804 - INFO - joeynmt.training - Epoch   1, Step:     2500, Batch Loss:     2.194516, Tokens per Sec:     3941, Lr: 0.001000
2022-02-25 16:59:38,322 - INFO - joeynmt.training - Epoch   1, Step:     2600, Batch Loss:     0.918128, Tokens per Sec:     3959, Lr: 0.001000
2022-02-25 16:59:41,870 - INFO - joeynmt.training - Epoch   1, Step:     2700, Batch Loss:     2.113064, Tokens per Sec:     3848, Lr: 0.001000
2022-02-25 16:59:45,399 - INFO - joeynmt.training - Epoch   1, Step:     2800, Batch Loss:     0.980278, Tokens per Sec:     3968, Lr: 0.001000
2022-02-25 16:59:48,938 - INFO - joeynmt.training - Epoch   1, Step:     2900, Batch Loss:     0.330842, Tokens per Sec:     3973, Lr: 0.001000
2022-02-25 16:59:52,552 - INFO - joeynmt.training - Epoch   1, Step:     3000, Batch Loss:     8.710308, Tokens per Sec:     3900, Lr: 0.001000
2022-02-25 17:00:03,729 - INFO - joeynmt.helpers - delete reverse_model/1000.ckpt
2022-02-25 17:00:03,729 - INFO - joeynmt.training - Example #0
2022-02-25 17:00:03,729 - INFO - joeynmt.training - 	Source:     33 9 15 3 14 33 32 42 23 12 14 17 4 35 0 48 46 36 46 27 2 34 35 17 36 39 7 14 9 0
2022-02-25 17:00:03,729 - INFO - joeynmt.training - 	Reference:  0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 4 17 14 12 23 42 32 33 14 3 15 9 33
2022-02-25 17:00:03,729 - INFO - joeynmt.training - 	Hypothesis: 0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 17 35 4 4 17 14 12 23 42 14 14 7 39 39 36
2022-02-25 17:00:03,729 - INFO - joeynmt.training - Example #3
2022-02-25 17:00:03,730 - INFO - joeynmt.training - 	Source:     10 43 37 32 6 9 25 36 21 29 16 7 18 27 30 46 37 15 7 48 18
2022-02-25 17:00:03,730 - INFO - joeynmt.training - 	Reference:  18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
2022-02-25 17:00:03,730 - INFO - joeynmt.training - 	Hypothesis: 18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
2022-02-25 17:00:03,730 - INFO - joeynmt.training - Example #6
2022-02-25 17:00:03,730 - INFO - joeynmt.training - 	Source:     0 38 14 26 20 34 10 36 11 32 29 21
2022-02-25 17:00:03,730 - INFO - joeynmt.training - 	Reference:  21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 17:00:03,730 - INFO - joeynmt.training - 	Hypothesis: 21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 17:00:03,730 - INFO - joeynmt.training - Validation result (greedy) at epoch   1, step     3000: bleu:  87.46, loss: 10863.2754, ppl:   1.9457, duration: 11.1780s
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:694: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, batch_sizes, hx, self._flat_weights, self.bias,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:691: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/_functions.py:68: UserWarning: Was asked to gather along dimension 0, but all input tensors were scalars; will instead unsqueeze and return a vector.
  warnings.warn('Was asked to gather along dimension 0, but all '
2022-02-25 17:00:08,300 - INFO - joeynmt.training - Epoch   1, Step:     3100, Batch Loss:     1.407775, Tokens per Sec:     3031, Lr: 0.001000
2022-02-25 17:00:11,793 - INFO - joeynmt.training - Epoch   1, Step:     3200, Batch Loss:     0.513544, Tokens per Sec:     3910, Lr: 0.001000
2022-02-25 17:00:15,309 - INFO - joeynmt.training - Epoch   1, Step:     3300, Batch Loss:     2.213034, Tokens per Sec:     3920, Lr: 0.001000
2022-02-25 17:00:18,841 - INFO - joeynmt.training - Epoch   1, Step:     3400, Batch Loss:     0.949318, Tokens per Sec:     3976, Lr: 0.001000
2022-02-25 17:00:22,419 - INFO - joeynmt.training - Epoch   1, Step:     3500, Batch Loss:    13.880915, Tokens per Sec:     3990, Lr: 0.001000
2022-02-25 17:00:26,052 - INFO - joeynmt.training - Epoch   1, Step:     3600, Batch Loss:     0.289540, Tokens per Sec:     3863, Lr: 0.001000
2022-02-25 17:00:29,670 - INFO - joeynmt.training - Epoch   1, Step:     3700, Batch Loss:     4.061685, Tokens per Sec:     3928, Lr: 0.001000
2022-02-25 17:00:33,217 - INFO - joeynmt.training - Epoch   1, Step:     3800, Batch Loss:     0.866066, Tokens per Sec:     3898, Lr: 0.001000
2022-02-25 17:00:36,758 - INFO - joeynmt.training - Epoch   1, Step:     3900, Batch Loss:     4.546507, Tokens per Sec:     3968, Lr: 0.001000
2022-02-25 17:00:40,336 - INFO - joeynmt.training - Epoch   1, Step:     4000, Batch Loss:     0.158080, Tokens per Sec:     3931, Lr: 0.001000
2022-02-25 17:00:49,926 - INFO - joeynmt.training - Hooray! New best validation result [eval_metric]!
2022-02-25 17:00:49,930 - INFO - joeynmt.helpers - delete reverse_model/3000.ckpt
2022-02-25 17:00:49,931 - INFO - joeynmt.training - Example #0
2022-02-25 17:00:49,931 - INFO - joeynmt.training - 	Source:     33 9 15 3 14 33 32 42 23 12 14 17 4 35 0 48 46 36 46 27 2 34 35 17 36 39 7 14 9 0
2022-02-25 17:00:49,931 - INFO - joeynmt.training - 	Reference:  0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 4 17 14 12 23 42 32 33 14 3 15 9 33
2022-02-25 17:00:49,931 - INFO - joeynmt.training - 	Hypothesis: 0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 4 4 17 14 12 23 9 9
2022-02-25 17:00:49,931 - INFO - joeynmt.training - Example #3
2022-02-25 17:00:49,931 - INFO - joeynmt.training - 	Source:     10 43 37 32 6 9 25 36 21 29 16 7 18 27 30 46 37 15 7 48 18
2022-02-25 17:00:49,931 - INFO - joeynmt.training - 	Reference:  18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
2022-02-25 17:00:49,931 - INFO - joeynmt.training - 	Hypothesis: 18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
2022-02-25 17:00:49,931 - INFO - joeynmt.training - Example #6
2022-02-25 17:00:49,931 - INFO - joeynmt.training - 	Source:     0 38 14 26 20 34 10 36 11 32 29 21
2022-02-25 17:00:49,931 - INFO - joeynmt.training - 	Reference:  21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 17:00:49,931 - INFO - joeynmt.training - 	Hypothesis: 21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 17:00:49,931 - INFO - joeynmt.training - Validation result (greedy) at epoch   1, step     4000: bleu:  89.62, loss: 11126.6250, ppl:   1.9773, duration: 9.5946s
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:694: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, batch_sizes, hx, self._flat_weights, self.bias,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:691: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/_functions.py:68: UserWarning: Was asked to gather along dimension 0, but all input tensors were scalars; will instead unsqueeze and return a vector.
  warnings.warn('Was asked to gather along dimension 0, but all '
2022-02-25 17:00:54,387 - INFO - joeynmt.training - Epoch   1, Step:     4100, Batch Loss:     0.169919, Tokens per Sec:     3134, Lr: 0.001000
2022-02-25 17:00:57,932 - INFO - joeynmt.training - Epoch   1, Step:     4200, Batch Loss:     1.314063, Tokens per Sec:     3858, Lr: 0.001000
2022-02-25 17:01:01,498 - INFO - joeynmt.training - Epoch   1, Step:     4300, Batch Loss:     3.430106, Tokens per Sec:     3955, Lr: 0.001000
2022-02-25 17:01:05,008 - INFO - joeynmt.training - Epoch   1, Step:     4400, Batch Loss:     0.299303, Tokens per Sec:     3818, Lr: 0.001000
2022-02-25 17:01:08,526 - INFO - joeynmt.training - Epoch   1, Step:     4500, Batch Loss:     0.613354, Tokens per Sec:     3965, Lr: 0.001000
2022-02-25 17:01:12,065 - INFO - joeynmt.training - Epoch   1, Step:     4600, Batch Loss:     9.175688, Tokens per Sec:     3854, Lr: 0.001000
2022-02-25 17:01:15,741 - INFO - joeynmt.training - Epoch   1, Step:     4700, Batch Loss:     0.056693, Tokens per Sec:     3791, Lr: 0.001000
2022-02-25 17:01:19,278 - INFO - joeynmt.training - Epoch   1, Step:     4800, Batch Loss:     0.073095, Tokens per Sec:     3957, Lr: 0.001000
2022-02-25 17:01:22,831 - INFO - joeynmt.training - Epoch   1, Step:     4900, Batch Loss:     0.042638, Tokens per Sec:     4022, Lr: 0.001000
2022-02-25 17:01:26,357 - INFO - joeynmt.training - Epoch   1, Step:     5000, Batch Loss:     0.056767, Tokens per Sec:     3997, Lr: 0.001000
2022-02-25 17:01:36,444 - INFO - joeynmt.training - Hooray! New best validation result [eval_metric]!
2022-02-25 17:01:36,448 - INFO - joeynmt.helpers - delete reverse_model/2000.ckpt
2022-02-25 17:01:36,448 - INFO - joeynmt.training - Example #0
2022-02-25 17:01:36,449 - INFO - joeynmt.training - 	Source:     33 9 15 3 14 33 32 42 23 12 14 17 4 35 0 48 46 36 46 27 2 34 35 17 36 39 7 14 9 0
2022-02-25 17:01:36,449 - INFO - joeynmt.training - 	Reference:  0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 4 17 14 12 23 42 32 33 14 3 15 9 33
2022-02-25 17:01:36,449 - INFO - joeynmt.training - 	Hypothesis: 0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 4 17 14 14 23 42 32 33 33
2022-02-25 17:01:36,449 - INFO - joeynmt.training - Example #3
2022-02-25 17:01:36,449 - INFO - joeynmt.training - 	Source:     10 43 37 32 6 9 25 36 21 29 16 7 18 27 30 46 37 15 7 48 18
2022-02-25 17:01:36,449 - INFO - joeynmt.training - 	Reference:  18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
2022-02-25 17:01:36,449 - INFO - joeynmt.training - 	Hypothesis: 18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 37 43 10
2022-02-25 17:01:36,449 - INFO - joeynmt.training - Example #6
2022-02-25 17:01:36,449 - INFO - joeynmt.training - 	Source:     0 38 14 26 20 34 10 36 11 32 29 21
2022-02-25 17:01:36,449 - INFO - joeynmt.training - 	Reference:  21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 17:01:36,449 - INFO - joeynmt.training - 	Hypothesis: 21 29 32 11 36 10 34 20 26 14 38 0
2022-02-25 17:01:36,449 - INFO - joeynmt.training - Validation result (greedy) at epoch   1, step     5000: bleu:  94.86, loss: 4660.0898, ppl:   1.3305, duration: 10.0916s
2022-02-25 17:01:37,316 - INFO - joeynmt.training - Epoch   1: total training loss 37273.51
2022-02-25 17:01:37,316 - INFO - joeynmt.training - Training ended after   1 epochs.
2022-02-25 17:01:37,317 - INFO - joeynmt.training - Best validation result (greedy) at step     5000:  94.86 eval_metric.
2022-02-25 17:01:37,325 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 5
2022-02-25 17:01:37,325 - INFO - joeynmt.prediction - Loading model from reverse_model/5000.ckpt
2022-02-25 17:01:37,332 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-25 17:01:37,334 - INFO - joeynmt.model - Enc-dec model built.
2022-02-25 17:01:37,335 - INFO - joeynmt.prediction - Decoding on dev set (test/data/reverse/dev.trg)...
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:694: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, batch_sizes, hx, self._flat_weights, self.bias,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:691: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
2022-02-25 17:01:46,730 - INFO - joeynmt.prediction -  dev bleu[13a]:  94.86 [Greedy decoding]
2022-02-25 17:01:46,731 - INFO - joeynmt.prediction - Translations saved to: reverse_model/00005000.hyps.dev
2022-02-25 17:01:46,731 - INFO - joeynmt.prediction - Decoding on test set (test/data/reverse/test.trg)...
2022-02-25 17:01:54,415 - INFO - joeynmt.prediction - test bleu[13a]:  94.88 [Greedy decoding]
2022-02-25 17:01:54,415 - INFO - joeynmt.prediction - Translations saved to: reverse_model/00005000.hyps.test

real	4m17.721s
user	6m23.591s
sys	0m24.168s
(joey) ye@:~/exp/joeynmt$ 
```

GPU မသုံးပဲ run ခဲ့တုန်းက 4m27 ဖြစ်ပြီး GPU သုံးပြီး run တော့ 4m17 ...  
learning လုပ်ရတာကလည်း အရမ်းလွယ်တဲ့ toy model ကြောင့် လို့ ယူဆ...  

## Process Tracking

```
(joey) ye@:~/exp/joeynmt/reverse_model$ ls
00005000.hyps.dev   3000.hyps  5000.hyps       att.2000.0.pdf  att.3000.3.pdf  att.4000.6.pdf  best.ckpt      tensorboard
00005000.hyps.test  4000.ckpt  att.1000.0.pdf  att.2000.3.pdf  att.3000.6.pdf  att.5000.0.pdf  config.yaml    train.log
1000.hyps           4000.hyps  att.1000.3.pdf  att.2000.6.pdf  att.4000.0.pdf  att.5000.3.pdf  latest.ckpt    trg_vocab.txt
2000.hyps           5000.ckpt  att.1000.6.pdf  att.3000.0.pdf  att.4000.3.pdf  att.5000.6.pdf  src_vocab.txt  validations.txt
(joey) ye@:~/exp/joeynmt/reverse_model$ 
```

log file ကို လေ့လာခဲ့...  

```
(joey) ye@:~/exp/joeynmt/reverse_model$ head ./train.log
2022-02-25 16:57:38,568 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-25 16:57:38,584 - INFO - joeynmt.data - Loading training data...
2022-02-25 16:57:38,871 - INFO - joeynmt.data - Building vocabulary...
2022-02-25 16:57:38,983 - INFO - joeynmt.data - Loading dev data...
2022-02-25 16:57:38,989 - INFO - joeynmt.data - Loading test data...
2022-02-25 16:57:38,992 - INFO - joeynmt.data - Data loaded.
2022-02-25 16:57:38,992 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-25 16:57:38,995 - INFO - joeynmt.model - Enc-dec model built.
2022-02-25 16:57:39,435 - DEBUG - tensorflow - Falling back to TensorFlow client; we recommended you install the Cloud TPU client directly with pip install cloud-tpu-client.
2022-02-25 16:57:39,716 - INFO - joeynmt.training - Total params: 105088
(joey) ye@:~/exp/joeynmt/reverse_model$ tail ./train.log
2022-02-25 17:01:37,325 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 5
2022-02-25 17:01:37,325 - INFO - joeynmt.prediction - Loading model from reverse_model/5000.ckpt
2022-02-25 17:01:37,332 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-25 17:01:37,334 - INFO - joeynmt.model - Enc-dec model built.
2022-02-25 17:01:37,335 - INFO - joeynmt.prediction - Decoding on dev set (test/data/reverse/dev.trg)...
2022-02-25 17:01:46,730 - INFO - joeynmt.prediction -  dev bleu[13a]:  94.86 [Greedy decoding]
2022-02-25 17:01:46,731 - INFO - joeynmt.prediction - Translations saved to: reverse_model/00005000.hyps.dev
2022-02-25 17:01:46,731 - INFO - joeynmt.prediction - Decoding on test set (test/data/reverse/test.trg)...
2022-02-25 17:01:54,415 - INFO - joeynmt.prediction - test bleu[13a]:  94.88 [Greedy decoding]
2022-02-25 17:01:54,415 - INFO - joeynmt.prediction - Translations saved to: reverse_model/00005000.hyps.test
(joey) ye@:~/exp/joeynmt/reverse_model$
```

validation report ဖိုင်က validations.txt ဆိုတဲ့ ဖိုင်မှာ သိမ်းထားတယ်...  

```
(joey) ye@:~/exp/joeynmt/reverse_model$ cat ./validations.txt 
Steps: 1000	Loss: 13479.49707	PPL: 2.28393	bleu: 58.32355	LR: 0.00100000	*
Steps: 2000	Loss: 4554.02002	PPL: 1.32184	bleu: 88.27667	LR: 0.00100000	*
Steps: 3000	Loss: 10863.27539	PPL: 1.94566	bleu: 87.45886	LR: 0.00100000	
Steps: 4000	Loss: 11126.62500	PPL: 1.97731	bleu: 89.61592	LR: 0.00100000	*
Steps: 5000	Loss: 4660.08984	PPL: 1.33046	bleu: 94.85863	LR: 0.00100000	*
(joey) ye@:~/exp/joeynmt/reverse_model$
```

validation result တွေကို အထက်ပါအတိုင်း တွေ့ရလိမ့်မယ်...  

## Check Learning Curves

```
(joey) ye@:~/exp/joeynmt$ python3 scripts/plot_validations.py reverse_model --plot_values bleu PPL  --output_path reverse_model/bleu-ppl.png
(joey) ye@:~/exp/joeynmt$ display ./reverse_model/bleu-ppl.png 
```


## Check TensorBoard

```
(joey) ye@:~/exp/joeynmt$ tensorboard --logdir reverse_model/tensorboard
2022-02-25 17:11:40.025636: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.11.0
Serving TensorBoard on localhost; to expose to the network, use a proxy or pass --bind_all
TensorBoard 2.4.1 at http://localhost:6006/ (Press CTRL+C to quit)
```
http://localhost:6006/ ကို ဖွင့်ကြည့်ရင် browser မှာ အောက်ပါအတိုင်း Tensorboard ကို မြင်ရပါလိမ့်မယ်။  

## Attention Visualization

JoeyNMT မှာက facility တစ်ခုအနေနဲ့ Attention Visualization ဆိုတာကိုလည်း ထည့်ပေးထားတယ်။  

## Check Validation Hypothesis Files

```
(joey) ye@:~/exp/joeynmt/reverse_model$ head 5000.hyps 
0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 4 17 14 14 23 42 32 33 33
43 41 2 47 32 34 1 20 46
10 49 27 6 25 2 35 6 49 9 36 6 0 17 11 24 0 6 46 38 49 5 9 9 8 22
18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 37 43 10
38 49 7 40 2 30 3 43 39 33 0 34 8 31 19 16 47 3 5 5 31 43 38 28 17 48 24
37 12 6 45 22 2 9 48 10 18 46 1 28 0 44 0 41 44 27 15 4 4 24 3 4 37
21 29 32 11 36 10 34 20 26 14 38 0
25 9 8 12 26 10 16 49 20 2 4 42 25 31 12 0 22 39
35 20 31 41 22
23 9 14 23 8 38 35 11 22 9 47 14 3 13 46 30 49 34
```

```
(joey) ye@:~/exp/joeynmt/reverse_model$ head 4000.hyps 
0 9 14 7 39 36 17 35 34 2 27 46 36 46 48 0 35 4 4 17 14 12 23 9 9
43 41 2 47 32 34 1 20 46
10 49 27 6 25 2 35 6 49 9 36 6 0 17 11 24 0 6 6 46 38 49 5 4 9
18 48 7 15 37 46 30 27 18 7 16 29 21 36 25 9 6 32 37 43 10
38 49 7 40 2 30 3 43 39 33 0 34 8 31 19 16 47 3 5 31 31 43 38 28 24
37 12 6 45 22 2 9 48 10 18 46 1 28 0 44 0 41 44 27 15 15 4 24 3 37
21 29 32 11 36 10 34 20 26 14 38 0
25 9 8 12 26 10 16 49 20 2 4 42 25 31 12 0 22 39
35 20 31 41 22
23 9 14 23 8 38 35 11 22 9 47 14 3 13 46 30 49 34
(joey) ye@:~/exp/joeynmt/reverse_model$ 
```

## Testing

```
(joey) ye@:~/exp/joeynmt$ python3 -m joeynmt test reverse_model/config.yaml --output_path reverse_model/predictions
2022-02-25 17:23:39,489 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-25 17:23:39,489 - INFO - joeynmt.data - Building vocabulary...
2022-02-25 17:23:39,489 - INFO - joeynmt.data - Loading dev data...
2022-02-25 17:23:39,493 - INFO - joeynmt.data - Loading test data...
2022-02-25 17:23:39,497 - INFO - joeynmt.data - Data loaded.
2022-02-25 17:23:39,514 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 5
2022-02-25 17:23:39,514 - INFO - joeynmt.prediction - Loading model from reverse_model/latest.ckpt
2022-02-25 17:23:41,087 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-25 17:23:41,107 - INFO - joeynmt.model - Enc-dec model built.
2022-02-25 17:23:41,110 - INFO - joeynmt.prediction - Decoding on dev set (test/data/reverse/dev.trg)...
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:694: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, batch_sizes, hx, self._flat_weights, self.bias,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:691: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
2022-02-25 17:23:50,880 - INFO - joeynmt.prediction -  dev bleu[13a]:  94.86 [Greedy decoding]
2022-02-25 17:23:50,880 - INFO - joeynmt.prediction - Translations saved to: reverse_model/predictions.dev
2022-02-25 17:23:50,880 - INFO - joeynmt.prediction - Decoding on test set (test/data/reverse/test.trg)...
2022-02-25 17:23:58,966 - INFO - joeynmt.prediction - test bleu[13a]:  94.88 [Greedy decoding]
2022-02-25 17:23:58,966 - INFO - joeynmt.prediction - Translations saved to: reverse_model/predictions.test
(joey) ye@:~/exp/joeynmt$
```

Evaluation ရလဒ်တွေက အထက်ပါ output ရဲ့ နောက်ဆုံးပိုင်းမှာ ရှိတဲ့ အပိုင်းကိုပဲ လေ့လာရင် dev BLEU နဲ့ test BLEU တွေကို တွေ့ရမှာ ဖြစ်ပါတယ်။  

```
2022-02-25 17:23:50,880 - INFO - joeynmt.prediction -  dev bleu[13a]:  94.86 [Greedy decoding]
2022-02-25 17:23:50,880 - INFO - joeynmt.prediction - Translations saved to: reverse_model/predictions.dev
2022-02-25 17:23:50,880 - INFO - joeynmt.prediction - Decoding on test set (test/data/reverse/test.trg)...
2022-02-25 17:23:58,966 - INFO - joeynmt.prediction - test bleu[13a]:  94.88 [Greedy decoding]
2022-02-25 17:23:58,966 - INFO - joeynmt.prediction - Translations saved to: reverse_model/predictions.test

```

dev BLEU က 94.86 နဲ့ test BLEU က 94.88 ရတယ်။  

output ဖိုင်တွေကိုလည်း ကြည့်ကြည့် ရအောင်...  

```
(joey) ye@:~/exp/joeynmt/reverse_model$ ls predictions.*
predictions.dev  predictions.test
(joey) ye@:~/exp/joeynmt/reverse_model$ 
```

reference ဖိုင်ရဲ့ head က အောက်ပါအတိုင်း...  

```
(joey) ye@:~/exp/joeynmt/test/data/reverse$ head test.trg 
11 42 37 25 39 33 46 40 8 21 24 14 25 12 47 2 17
29 29 12 22 35 9 36 43 11 47 7 24 8 37 44 5 2 14 28 3
14 23 15 5 31 34 14 49 48 34 4 47 47
37 28 10 38 23 23 47 21 25 18 39 45
29 13 18 38 5 41 8
20 42 5 8 25 25 42
48 49 17 26 10 25 4 34 25
48 31 36 41 45 39 30 1 25 4 3 24 17
35 8 45 26 7 49 1 14 13 7 15 5 27 42 26 31 22 23 31 2
38 30 1 28
(joey) ye@:~/exp/joeynmt/test/data/reverse$
```

ဆောက်ထားတဲ့ မော်ဒယ်ကို သုံးပြီးတော့ prediction လုပ်ထားတဲ့ output က အောက်ပါအတိုင်း...  

```
(joey) ye@:~/exp/joeynmt/reverse_model$ head ./predictions.test
11 42 37 25 39 33 46 40 8 21 24 14 25 12 47 2 17
29 29 12 22 35 9 36 43 11 47 7 24 8 37 44 5 2 14 28 3
14 23 15 5 31 34 14 49 48 34 4 47 47 47
37 28 10 38 23 23 47 21 25 18 39 45
29 13 18 38 5 41 8
20 42 5 8 25 25 42
48 49 17 26 10 25 4 34 25
48 31 36 41 45 39 30 1 25 4 3 24 17
35 8 45 26 7 49 1 14 13 7 15 5 27 42 26 31 22 23 31 2
38 30 1 28
(joey) ye@:~/exp/joeynmt/reverse_model$
```

## Translation with Input File

configuration ဖိုင်ထဲမှာ setting လုပ်ထားတဲ့ test ဖိုင် မဟုတ်ပဲ ပြင်ပက test ဖိုင်နဲ့လည်း testing လုပ်လို့ ရပါတယ်။  

စာကြောင်း နှစ်ကြောင်းပဲ ပါတဲ့ test ဖိုင် ကို အောက်ပါအတိုင်း ဆောက်ခဲ့...  

```
echo $'2 34 43 21 2 \n3 4 5 6 7 8 9 10 11 12' > my_input.txt
```

ပြီးရင် testing လုပ်ကြည့်ရအောင်...  
"--output_path" option ကို မပေးထားလို့ ဘာသာပြန်ပြီးရလာတဲ့ ရလဒ်ကို စကရင်ပေါ်မှာပဲ ရိုက်ထုတ်ပြလိမ့်မယ်...  

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt translate reverse_model/config.yaml < my_input.txt
2022-02-25 17:38:49,546 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-25 17:38:49,563 - INFO - joeynmt.prediction - Loading model from reverse_model/latest.ckpt
2022-02-25 17:38:51,125 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-25 17:38:51,149 - INFO - joeynmt.model - Enc-dec model built.
2 21 43 34 2
12 11 10 9 8 7 6 5 4 3

real	0m2.875s
user	0m2.102s
sys	0m0.762s
(joey) ye@:~/exp/joeynmt$
```

## Interactive Translation with JoeyNMT

```
(joey) ye@:~/exp/joeynmt$ python3 -m joeynmt translate reverse_model/config.yaml
2022-02-25 17:41:19,531 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-25 17:41:19,548 - INFO - joeynmt.prediction - Loading model from reverse_model/latest.ckpt
2022-02-25 17:41:21,122 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-25 17:41:21,149 - INFO - joeynmt.model - Enc-dec model built.

Please enter a source sentence (pre-processed): 
1 3 5 7 9
JoeyNMT: Hypotheses ranked by score
JoeyNMT #1: 9 7 5 3 1

Please enter a source sentence (pre-processed): 
၁ ၂ ၃ ၄ ၅ ၆ ၇ ၈ ၉
JoeyNMT: Hypotheses ranked by score
JoeyNMT #1: 36 36 36 36 36 43 40 40
```

အထက်ပါအတိုင်း အလုပ်ကောင်းကောင်းလုပ်ပေးပါတယ်။ training မလုပ်ထားတဲ့ မြန်မာစာ ဂဏန်းတွေကို ထည့်ကြည့်တဲ့ အခါမှာတော့ အလုပ် မလုပ်ပေးတာကို တွေ့ရတယ်။  
ထိုနည်းလည်းကောင်း ဒဿမ ပါတဲ့ ဂဏန်းတွေကို translate လုပ်ခိုင်းရင်လည်း ဘာသာပြန်ပေးနိုင်မှာ မဟုတ်ပါဘူး။ အောက်ပါအတိုင်းပါ...  

```
Please enter a source sentence (pre-processed): 
0.1 1 2 3.0
JoeyNMT: Hypotheses ranked by score
JoeyNMT #1: 23 2 1 36
```


အဲဒါက ဘာကို ပြနေတာလဲ ဆိုရင် လက်ရှိ Neural Network Model တွေက တကယ့်ကို specific task အတွက်ပဲ အလုပ်လုပ်နိုင်ပြီးတော့ intelligent ဆိုတဲ့ အပိုင်းမှာ ပြောစရာတွေရှိနေသေးတယ် ဆိုတဲ့ အချက်ပါ...  

## Tuning

တကယ်တမ်းက လက်တွေ့မှာတော့ hyperparameter တွေကို အမျိုးမျိုး ကစားပြီး tuning လုပ်ကြရပါတယ်။ ဥပမာ batch size, learning rate, hidden layer, optimizing function, dropout rate စသည်တို့ကို အဓိက ထား ကစားကြပါတယ်။  အဲဒီအပေါ်ကို မူတည်ပြီး learning curve က အပြောင်းအလဲဖြစ်တာ၊ training time အပြောင်းအလဲဖြစ်တာ... translation performance ကလည်း တက်တာ၊ ကျတာတွေ ဖြစ်နိုင်ပါတယ်။ ဒီနေရာမှာ လုပ်မပြတော့ပါဘူး...  

လေ့လာချင်တဲ့သူက configuration ဖိုင်မှာ setting ကို ဝင်ပြောင်းတာလုပ်ပြီးရင် model output folder သိမ်းမယ့် path ကိုလည်း အသစ်ပေးပြီး training လုပ်ပြီးတော့ comparison လုပ်တာတွေကို လုပ်ကြည့်ကြပါ။  

JoeyNMT ရဲ့ framework တွေကို အသေးစိတ် သိချင်တယ်၊ ဝင်ပြင်ချင်တယ်ဆိုရင်တော့ အောက်ပါ link တွေကို မွှေနှောက်ဖတ်ရလိမ့်မယ်။  

- https://joeynmt.readthedocs.io/en/latest/overview.html#overview
- https://joeynmt.readthedocs.io/en/latest/modules.html#modules


