# Berkeley Neural Parser Installation and Parsing

## git clone

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ git clone https://github.com/nikitakit/self-attentive-parser
Cloning into 'self-attentive-parser'...
remote: Enumerating objects: 190, done.
remote: Counting objects: 100% (190/190), done.
remote: Compressing objects: 100% (86/86), done.
remote: Total 541 (delta 103), reused 183 (delta 102), pack-reused 351
Receiving objects: 100% (541/541), 83.23 MiB | 695.00 KiB/s, done.
Resolving deltas: 100% (300/300), done.
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ cd self-attentive-parser/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ ls
data  EVALB  EVALB_SPMRL  EXPERIMENTS.md  LICENSE  README.md  setup.py  src
```

## Install Spacy and Download en_core_web_md

py3.6env အောက်ကိုဝင်တယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ conda activate py3.6env
```

Spacy က ဒီ python environment ထဲမှာ မရှိသေးတာကိုတွေ့ရ။ အဲဒါနဲ့ Spacy ကိုပါ installation လုပ်ခဲ့တယ်။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ python -m spacy download en_core_web_md
/home/ye/anaconda3/envs/py3.6env/bin/python: No module named spacy
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ pip install spacy
Collecting spacy
  Downloading spacy-3.0.5-cp36-cp36m-manylinux2014_x86_64.whl (12.8 MB)
     |████████████████████████████████| 12.8 MB 628 kB/s 
Requirement already satisfied: jinja2 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy) (2.11.3)
Requirement already satisfied: numpy>=1.15.0 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy) (1.19.4)
Requirement already satisfied: requests<3.0.0,>=2.13.0 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy) (2.25.1)
Requirement already satisfied: setuptools in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy) (51.0.0.post20201207)
Requirement already satisfied: tqdm<5.0.0,>=4.38.0 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy) (4.55.1)
Requirement already satisfied: importlib-metadata>=0.20 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy) (3.7.3)
Requirement already satisfied: typing-extensions<4.0.0.0,>=3.7.4 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy) (3.7.4.3)
Collecting blis<0.8.0,>=0.4.0
  Downloading blis-0.7.4-cp36-cp36m-manylinux2014_x86_64.whl (9.8 MB)
     |████████████████████████████████| 9.8 MB 823 kB/s 
Collecting catalogue<2.1.0,>=2.0.1
  Using cached catalogue-2.0.1-py3-none-any.whl (9.6 kB)
Collecting cymem<2.1.0,>=2.0.2
  Downloading cymem-2.0.5-cp36-cp36m-manylinux2014_x86_64.whl (35 kB)
Requirement already satisfied: zipp>=0.5 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from importlib-metadata>=0.20->spacy) (3.4.1)
Collecting murmurhash<1.1.0,>=0.28.0
  Downloading murmurhash-1.0.5-cp36-cp36m-manylinux2014_x86_64.whl (20 kB)
Collecting packaging>=20.0
  Downloading packaging-20.9-py2.py3-none-any.whl (40 kB)
     |████████████████████████████████| 40 kB 936 kB/s 
Collecting pathy>=0.3.5
  Using cached pathy-0.4.0-py3-none-any.whl (36 kB)
Requirement already satisfied: dataclasses<1.0,>=0.6 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from pathy>=0.3.5->spacy) (0.8)
Collecting preshed<3.1.0,>=3.0.2
  Downloading preshed-3.0.5-cp36-cp36m-manylinux2014_x86_64.whl (126 kB)
     |████████████████████████████████| 126 kB 819 kB/s 
Collecting pydantic<1.8.0,>=1.7.1
  Downloading pydantic-1.7.3-cp36-cp36m-manylinux2014_x86_64.whl (9.2 MB)
     |████████████████████████████████| 9.2 MB 472 kB/s 
Collecting pyparsing>=2.0.2
  Using cached pyparsing-2.4.7-py2.py3-none-any.whl (67 kB)
Requirement already satisfied: chardet<5,>=3.0.2 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from requests<3.0.0,>=2.13.0->spacy) (4.0.0)
Requirement already satisfied: idna<3,>=2.5 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from requests<3.0.0,>=2.13.0->spacy) (2.10)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from requests<3.0.0,>=2.13.0->spacy) (2020.12.5)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from requests<3.0.0,>=2.13.0->spacy) (1.26.4)
Collecting smart-open<4.0.0,>=2.2.0
  Using cached smart_open-3.0.0.tar.gz (113 kB)
Collecting spacy-legacy<3.1.0,>=3.0.0
  Using cached spacy_legacy-3.0.1-py2.py3-none-any.whl (7.0 kB)
Collecting srsly<3.0.0,>=2.4.0
  Downloading srsly-2.4.0-cp36-cp36m-manylinux2014_x86_64.whl (456 kB)
     |████████████████████████████████| 456 kB 541 kB/s 
Collecting thinc<8.1.0,>=8.0.2
  Downloading thinc-8.0.2-cp36-cp36m-manylinux2014_x86_64.whl (1.1 MB)
     |████████████████████████████████| 1.1 MB 740 kB/s 
Collecting contextvars<3,>=2.4
  Downloading contextvars-2.4.tar.gz (9.6 kB)
Collecting immutables>=0.9
  Downloading immutables-0.15-cp36-cp36m-manylinux1_x86_64.whl (100 kB)
     |████████████████████████████████| 100 kB 827 kB/s 
Collecting typer<0.4.0,>=0.3.0
  Using cached typer-0.3.2-py3-none-any.whl (21 kB)
Requirement already satisfied: click<7.2.0,>=7.1.1 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from typer<0.4.0,>=0.3.0->spacy) (7.1.2)
Collecting wasabi<1.1.0,>=0.8.1
  Using cached wasabi-0.8.2-py3-none-any.whl (23 kB)
Requirement already satisfied: MarkupSafe>=0.23 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from jinja2->spacy) (1.1.1)
Building wheels for collected packages: smart-open, contextvars
  Building wheel for smart-open (setup.py) ... done
  Created wheel for smart-open: filename=smart_open-3.0.0-py3-none-any.whl size=107097 sha256=dcf2d5f1bcc791ddad96dce140ecfde87d6b5ca18190973f2eaafc3503736228
  Stored in directory: /home/ye/.cache/pip/wheels/88/2a/d4/f2e9023989d4d4b3574f268657cb6cd23994665a038803f547
  Building wheel for contextvars (setup.py) ... done
  Created wheel for contextvars: filename=contextvars-2.4-py3-none-any.whl size=7665 sha256=545c1b1eede166f68a6e41cf5320faeb7604411ba3549bc80c2ad78c6856b1bf
  Stored in directory: /home/ye/.cache/pip/wheels/41/11/53/911724983aa48deb94792432e14e518447212dd6c5477d49d3
Successfully built smart-open contextvars
Installing collected packages: murmurhash, immutables, cymem, catalogue, wasabi, typer, srsly, smart-open, pyparsing, pydantic, preshed, contextvars, blis, thinc, spacy-legacy, pathy, packaging, spacy
  Attempting uninstall: smart-open
    Found existing installation: smart-open 4.1.0
    Uninstalling smart-open-4.1.0:
      Successfully uninstalled smart-open-4.1.0
Successfully installed blis-0.7.4 catalogue-2.0.1 contextvars-2.4 cymem-2.0.5 immutables-0.15 murmurhash-1.0.5 packaging-20.9 pathy-0.4.0 preshed-3.0.5 pydantic-1.7.3 pyparsing-2.4.7 smart-open-3.0.0 spacy-3.0.5 spacy-legacy-3.0.1 srsly-2.4.0 thinc-8.0.2 typer-0.3.2 wasabi-0.8.2
```

benepar (i.e. Berkeley Neural Parser) ကို installation မလုပ်ရသေးသူး... အဲဒါကြောင့် အောက်ပါ error ကို ပေးတာပါ။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ gedit download.py
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ cat ./download.py 
import benepar
benepar.download('benepar_en3')
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ python ./download.py 
Traceback (most recent call last):
  File "./download.py", line 1, in <module>
    import benepar
ModuleNotFoundError: No module named 'benepar'
```

## Installation of Self-Attentive-Parser of Berkeley Nerual Parser

Berkeley Nerual Parser ကို git clone ပဲ လုပ်ထားပြီး installation မလုပ်ရသေးလို့ setup.py ကို အောက်ပါအတိုင်း run ခဲ့တယ်။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ ls
data  download.py  EVALB  EVALB_SPMRL  EXPERIMENTS.md  LICENSE  README.md  setup.py  src
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ python setup.py install
running install
running bdist_egg
running egg_info
creating src/benepar.egg-info
writing src/benepar.egg-info/PKG-INFO
writing dependency_links to src/benepar.egg-info/dependency_links.txt
writing requirements to src/benepar.egg-info/requires.txt
writing top-level names to src/benepar.egg-info/top_level.txt
writing manifest file 'src/benepar.egg-info/SOURCES.txt'
reading manifest file 'src/benepar.egg-info/SOURCES.txt'
writing manifest file 'src/benepar.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
creating build
creating build/lib
creating build/lib/benepar
copying src/benepar/subbatching.py -> build/lib/benepar
copying src/benepar/retokenization.py -> build/lib/benepar
copying src/benepar/parse_chart.py -> build/lib/benepar
copying src/benepar/partitioned_transformer.py -> build/lib/benepar
copying src/benepar/decode_chart.py -> build/lib/benepar
copying src/benepar/nkutil.py -> build/lib/benepar
copying src/benepar/char_lstm.py -> build/lib/benepar
copying src/benepar/parse_base.py -> build/lib/benepar
copying src/benepar/__init__.py -> build/lib/benepar
copying src/benepar/spacy_plugin.py -> build/lib/benepar
copying src/benepar/ptb_unescape.py -> build/lib/benepar
creating build/lib/benepar/integrations
copying src/benepar/integrations/nltk_plugin.py -> build/lib/benepar/integrations
copying src/benepar/integrations/downloader.py -> build/lib/benepar/integrations
copying src/benepar/integrations/__init__.py -> build/lib/benepar/integrations
copying src/benepar/integrations/spacy_extensions.py -> build/lib/benepar/integrations
copying src/benepar/integrations/spacy_plugin.py -> build/lib/benepar/integrations
creating build/bdist.linux-x86_64
creating build/bdist.linux-x86_64/egg
creating build/bdist.linux-x86_64/egg/benepar
copying build/lib/benepar/subbatching.py -> build/bdist.linux-x86_64/egg/benepar
copying build/lib/benepar/retokenization.py -> build/bdist.linux-x86_64/egg/benepar
copying build/lib/benepar/parse_chart.py -> build/bdist.linux-x86_64/egg/benepar
copying build/lib/benepar/partitioned_transformer.py -> build/bdist.linux-x86_64/egg/benepar
copying build/lib/benepar/decode_chart.py -> build/bdist.linux-x86_64/egg/benepar
copying build/lib/benepar/nkutil.py -> build/bdist.linux-x86_64/egg/benepar
copying build/lib/benepar/char_lstm.py -> build/bdist.linux-x86_64/egg/benepar
copying build/lib/benepar/parse_base.py -> build/bdist.linux-x86_64/egg/benepar
copying build/lib/benepar/__init__.py -> build/bdist.linux-x86_64/egg/benepar
copying build/lib/benepar/spacy_plugin.py -> build/bdist.linux-x86_64/egg/benepar
creating build/bdist.linux-x86_64/egg/benepar/integrations
copying build/lib/benepar/integrations/nltk_plugin.py -> build/bdist.linux-x86_64/egg/benepar/integrations
copying build/lib/benepar/integrations/downloader.py -> build/bdist.linux-x86_64/egg/benepar/integrations
copying build/lib/benepar/integrations/__init__.py -> build/bdist.linux-x86_64/egg/benepar/integrations
copying build/lib/benepar/integrations/spacy_extensions.py -> build/bdist.linux-x86_64/egg/benepar/integrations
copying build/lib/benepar/integrations/spacy_plugin.py -> build/bdist.linux-x86_64/egg/benepar/integrations
copying build/lib/benepar/ptb_unescape.py -> build/bdist.linux-x86_64/egg/benepar
byte-compiling build/bdist.linux-x86_64/egg/benepar/subbatching.py to subbatching.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/benepar/retokenization.py to retokenization.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/benepar/parse_chart.py to parse_chart.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/benepar/partitioned_transformer.py to partitioned_transformer.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/benepar/decode_chart.py to decode_chart.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/benepar/nkutil.py to nkutil.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/benepar/char_lstm.py to char_lstm.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/benepar/parse_base.py to parse_base.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/benepar/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/benepar/spacy_plugin.py to spacy_plugin.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/benepar/integrations/nltk_plugin.py to nltk_plugin.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/benepar/integrations/downloader.py to downloader.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/benepar/integrations/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/benepar/integrations/spacy_extensions.py to spacy_extensions.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/benepar/integrations/spacy_plugin.py to spacy_plugin.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/benepar/ptb_unescape.py to ptb_unescape.cpython-36.pyc
creating build/bdist.linux-x86_64/egg/EGG-INFO
copying src/benepar.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying src/benepar.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying src/benepar.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying src/benepar.egg-info/requires.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying src/benepar.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
zip_safe flag not set; analyzing archive contents...
creating dist
creating 'dist/benepar-0.2.0-py3.6.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing benepar-0.2.0-py3.6.egg
Copying benepar-0.2.0-py3.6.egg to /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Adding benepar 0.2.0 to easy-install.pth file

Installed /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/benepar-0.2.0-py3.6.egg
Processing dependencies for benepar==0.2.0
Searching for transformers[tokenizers,torch]>=4.2.2
Reading https://pypi.org/simple/transformers/
Downloading https://files.pythonhosted.org/packages/ed/d5/f4157a376b8a79489a76ce6cfe147f4f3be1e029b7144fa7b8432e8acb26/transformers-4.4.2-py3-none-any.whl#sha256=9826e4d5febc70d4ee6accd4d3f2a2a15e714e18c237ab82c95a6c0faaa001df
Best match: transformers 4.4.2
Processing transformers-4.4.2-py3-none-any.whl
Installing transformers-4.4.2-py3-none-any.whl to /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Adding transformers 4.4.2 to easy-install.pth file
Installing transformers-cli script to /home/ye/anaconda3/envs/py3.6env/bin

Installed /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/transformers-4.4.2-py3.6.egg
Searching for tokenizers>=0.9.4
Reading https://pypi.org/simple/tokenizers/
Downloading https://files.pythonhosted.org/packages/fd/5b/44baae602e0a30bcc53fbdbc60bd940c15e143d252d658dfdefce736ece5/tokenizers-0.10.1-cp36-cp36m-manylinux2010_x86_64.whl#sha256=fecfcb95c23ce6ebb4834156e78cb6a4cf883b37102c8dd46bc8bd3b5244c3d5
Best match: tokenizers 0.10.1
Processing tokenizers-0.10.1-cp36-cp36m-manylinux2010_x86_64.whl
Installing tokenizers-0.10.1-cp36-cp36m-manylinux2010_x86_64.whl to /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Adding tokenizers 0.10.1 to easy-install.pth file

Installed /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/tokenizers-0.10.1-py3.6-linux-x86_64.egg
Searching for torch-struct>=0.5
Reading https://pypi.org/simple/torch-struct/
Downloading https://files.pythonhosted.org/packages/b2/8c/775b7e141f11d509d59d0d2d801337ff3ad0203bc1a40335ea83e1161ba7/torch_struct-0.5-py3-none-any.whl#sha256=9e4c4e5a2317d01cef47bfb0786b4ece6aebe1fa23f5f8a6a91887a3aab3d020
Best match: torch-struct 0.5
Processing torch_struct-0.5-py3-none-any.whl
Installing torch_struct-0.5-py3-none-any.whl to /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Adding torch-struct 0.5 to easy-install.pth file

Installed /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch_struct-0.5-py3.6.egg
Searching for nltk>=3.2
Reading https://pypi.org/simple/nltk/
Downloading https://files.pythonhosted.org/packages/92/75/ce35194d8e3022203cca0d2f896dbb88689f9b3fce8e9f9cff942913519d/nltk-3.5.zip#sha256=845365449cd8c5f9731f7cb9f8bd6fd0767553b9d53af9eb1b3abf7700936b35
Best match: nltk 3.5
Processing nltk-3.5.zip
Writing /tmp/easy_install-c6la27ul/nltk-3.5/setup.cfg
Running nltk-3.5/setup.py -q bdist_egg --dist-dir /tmp/easy_install-c6la27ul/nltk-3.5/egg-dist-tmp-xs4337nn
warning: no files found matching 'README.txt'
warning: no files found matching 'Makefile' under directory '*.txt'
warning: no previously-included files matching '*~' found anywhere in distribution
creating /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/nltk-3.5-py3.6.egg
Extracting nltk-3.5-py3.6.egg to /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Adding nltk 3.5 to easy-install.pth file
Installing nltk script to /home/ye/anaconda3/envs/py3.6env/bin

Installed /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/nltk-3.5-py3.6.egg
Searching for sacremoses
Reading https://pypi.org/simple/sacremoses/
Downloading https://files.pythonhosted.org/packages/7d/34/09d19aff26edcc8eb2a01bed8e98f13a1537005d31e95233fd48216eed10/sacremoses-0.0.43.tar.gz#sha256=123c1bf2664351fb05e16f87d3786dbe44a050cfd7b85161c09ad9a63a8e2948
Best match: sacremoses 0.0.43
Processing sacremoses-0.0.43.tar.gz
Writing /tmp/easy_install-y3qts4a7/sacremoses-0.0.43/setup.cfg
Running sacremoses-0.0.43/setup.py -q bdist_egg --dist-dir /tmp/easy_install-y3qts4a7/sacremoses-0.0.43/egg-dist-tmp-xdf0kw37
zip_safe flag not set; analyzing archive contents...
sacremoses.__pycache__.corpus.cpython-36: module references __file__
creating /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/sacremoses-0.0.43-py3.6.egg
Extracting sacremoses-0.0.43-py3.6.egg to /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Adding sacremoses 0.0.43 to easy-install.pth file
Installing sacremoses script to /home/ye/anaconda3/envs/py3.6env/bin

Installed /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/sacremoses-0.0.43-py3.6.egg
Searching for filelock
Reading https://pypi.org/simple/filelock/
Downloading https://files.pythonhosted.org/packages/93/83/71a2ee6158bb9f39a90c0dea1637f81d5eef866e188e1971a1b1ab01a35a/filelock-3.0.12-py3-none-any.whl#sha256=929b7d63ec5b7d6b71b0fa5ac14e030b3f70b75747cef1b10da9b879fef15836
Best match: filelock 3.0.12
Processing filelock-3.0.12-py3-none-any.whl
Installing filelock-3.0.12-py3-none-any.whl to /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Adding filelock 3.0.12 to easy-install.pth file

Installed /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/filelock-3.0.12-py3.6.egg
Searching for dataclasses==0.8
Best match: dataclasses 0.8
Adding dataclasses 0.8 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for sentencepiece==0.1.94
Best match: sentencepiece 0.1.94
Adding sentencepiece 0.1.94 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for protobuf==3.15.6
Best match: protobuf 3.15.6
Adding protobuf 3.15.6 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for torch==1.8.1
Best match: torch 1.8.1
Adding torch 1.8.1 to easy-install.pth file
Installing convert-caffe2-to-onnx script to /home/ye/anaconda3/envs/py3.6env/bin
Installing convert-onnx-to-caffe2 script to /home/ye/anaconda3/envs/py3.6env/bin

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for spacy==3.0.5
Best match: spacy 3.0.5
Adding spacy 3.0.5 to easy-install.pth file
Installing spacy script to /home/ye/anaconda3/envs/py3.6env/bin

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for six==1.15.0
Best match: six 1.15.0
Adding six 1.15.0 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for tqdm==4.55.1
Best match: tqdm 4.55.1
Adding tqdm 4.55.1 to easy-install.pth file
Installing tqdm script to /home/ye/anaconda3/envs/py3.6env/bin

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for requests==2.25.1
Best match: requests 2.25.1
Adding requests 2.25.1 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for regex==2021.3.17
Best match: regex 2021.3.17
Adding regex 2021.3.17 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for packaging==20.9
Best match: packaging 20.9
Adding packaging 20.9 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for numpy==1.19.4
Best match: numpy 1.19.4
Adding numpy 1.19.4 to easy-install.pth file
Installing f2py script to /home/ye/anaconda3/envs/py3.6env/bin
Installing f2py3 script to /home/ye/anaconda3/envs/py3.6env/bin
Installing f2py3.6 script to /home/ye/anaconda3/envs/py3.6env/bin

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for importlib-metadata==3.7.3
Best match: importlib-metadata 3.7.3
Adding importlib-metadata 3.7.3 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for typing-extensions==3.7.4.3
Best match: typing-extensions 3.7.4.3
Adding typing-extensions 3.7.4.3 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for pydantic==1.7.3
Best match: pydantic 1.7.3
Adding pydantic 1.7.3 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for murmurhash==1.0.5
Best match: murmurhash 1.0.5
Adding murmurhash 1.0.5 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for pathy==0.4.0
Best match: pathy 0.4.0
Adding pathy 0.4.0 to easy-install.pth file
Installing pathy script to /home/ye/anaconda3/envs/py3.6env/bin

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for typer==0.3.2
Best match: typer 0.3.2
Adding typer 0.3.2 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for catalogue==2.0.1
Best match: catalogue 2.0.1
Adding catalogue 2.0.1 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for wasabi==0.8.2
Best match: wasabi 0.8.2
Adding wasabi 0.8.2 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for spacy-legacy==3.0.1
Best match: spacy-legacy 3.0.1
Adding spacy-legacy 3.0.1 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for thinc==8.0.2
Best match: thinc 8.0.2
Adding thinc 8.0.2 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for srsly==2.4.0
Best match: srsly 2.4.0
Adding srsly 2.4.0 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for Jinja2==2.11.3
Best match: Jinja2 2.11.3
Adding Jinja2 2.11.3 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for blis==0.7.4
Best match: blis 0.7.4
Adding blis 0.7.4 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for setuptools==51.0.0.post20201207
Best match: setuptools 51.0.0.post20201207
Adding setuptools 51.0.0.post20201207 to easy-install.pth file
Installing easy_install script to /home/ye/anaconda3/envs/py3.6env/bin

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for preshed==3.0.5
Best match: preshed 3.0.5
Adding preshed 3.0.5 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for cymem==2.0.5
Best match: cymem 2.0.5
Adding cymem 2.0.5 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for joblib==0.17.0
Best match: joblib 0.17.0
Adding joblib 0.17.0 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for click==7.1.2
Best match: click 7.1.2
Adding click 7.1.2 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for certifi==2020.12.5
Best match: certifi 2020.12.5
Adding certifi 2020.12.5 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for urllib3==1.26.4
Best match: urllib3 1.26.4
Adding urllib3 1.26.4 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for idna==2.10
Best match: idna 2.10
Adding idna 2.10 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for chardet==4.0.0
Best match: chardet 4.0.0
Adding chardet 4.0.0 to easy-install.pth file
Installing chardetect script to /home/ye/anaconda3/envs/py3.6env/bin

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for pyparsing==2.4.7
Best match: pyparsing 2.4.7
Adding pyparsing 2.4.7 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for zipp==3.4.1
Best match: zipp 3.4.1
Adding zipp 3.4.1 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for smart-open==3.0.0
Best match: smart-open 3.0.0
Adding smart-open 3.0.0 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for contextvars==2.4
Best match: contextvars 2.4
Adding contextvars 2.4 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for MarkupSafe==1.1.1
Best match: MarkupSafe 1.1.1
Adding MarkupSafe 1.1.1 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for immutables==0.15
Best match: immutables 0.15
Adding immutables 0.15 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Finished processing dependencies for benepar==0.2.0
```

ပြင်ထားတဲ့ download.py ပရိုဂရမ်ကို cat နဲ့ ကြည့်ရအောင်...  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ cat ./download.py 
import benepar
benepar.download('benepar_en3')
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ python ./download.py 
[nltk_data] Downloading package benepar_en3 to /home/ye/nltk_data...
[nltk_data]   Unzipping models/benepar_en3.zip.
```

benepar paerser ကို test လုပ်ကြည့်ရအောင်။  
Package 'en_core_web_md' က ဒီ pyton environment မှာ download မလုပ်ရသေးဘူးဆိုတာကို တွေ့ရ...    

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ python ./benepar-test.py 
[nltk_data] Error loading en_core_web_md: Package 'en_core_web_md' not
[nltk_data]     found in index
Traceback (most recent call last):
  File "./benepar-test.py", line 4, in <module>
    nlp = spacy.load('en_core_web_md')
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/spacy/__init__.py", line 47, in load
    return util.load_model(name, disable=disable, exclude=exclude, config=config)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/spacy/util.py", line 329, in load_model
    raise IOError(Errors.E050.format(name=name))
OSError: [E050] Can't find model 'en_core_web_md'. It doesn't seem to be a Python package or a valid path to a data directory.
```

spacy ကို သုံးပြီးတော့ en_core_web_md မော်ဒယ်ကို ဒေါင်းလုပ် လုပ်ရအောင်...  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ python3 -m spacy download en_core_web_md
Collecting en-core-web-md==3.0.0
  Downloading https://github.com/explosion/spacy-models/releases/download/en_core_web_md-3.0.0/en_core_web_md-3.0.0-py3-none-any.whl (47.1 MB)
     |████████████████████████████████| 47.1 MB 440 kB/s 
Requirement already satisfied: spacy<3.1.0,>=3.0.0 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from en-core-web-md==3.0.0) (3.0.5)
Requirement already satisfied: packaging>=20.0 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (20.9)
Requirement already satisfied: wasabi<1.1.0,>=0.8.1 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (0.8.2)
Requirement already satisfied: murmurhash<1.1.0,>=0.28.0 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (1.0.5)
Requirement already satisfied: srsly<3.0.0,>=2.4.0 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (2.4.0)
Requirement already satisfied: typing-extensions<4.0.0.0,>=3.7.4 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (3.7.4.3)
Requirement already satisfied: thinc<8.1.0,>=8.0.2 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (8.0.2)
Requirement already satisfied: setuptools in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (51.0.0.post20201207)
Requirement already satisfied: pathy>=0.3.5 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (0.4.0)
Requirement already satisfied: cymem<2.1.0,>=2.0.2 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (2.0.5)
Requirement already satisfied: typer<0.4.0,>=0.3.0 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (0.3.2)
Requirement already satisfied: blis<0.8.0,>=0.4.0 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (0.7.4)
Requirement already satisfied: tqdm<5.0.0,>=4.38.0 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (4.55.1)
Requirement already satisfied: numpy>=1.15.0 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (1.19.4)
Requirement already satisfied: requests<3.0.0,>=2.13.0 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (2.25.1)
Requirement already satisfied: pydantic<1.8.0,>=1.7.1 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (1.7.3)
Requirement already satisfied: preshed<3.1.0,>=3.0.2 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (3.0.5)
Requirement already satisfied: jinja2 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (2.11.3)
Requirement already satisfied: catalogue<2.1.0,>=2.0.1 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (2.0.1)
Requirement already satisfied: importlib-metadata>=0.20 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (3.7.3)
Requirement already satisfied: spacy-legacy<3.1.0,>=3.0.0 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (3.0.1)
Requirement already satisfied: zipp>=0.5 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from importlib-metadata>=0.20->spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (3.4.1)
Requirement already satisfied: pyparsing>=2.0.2 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from packaging>=20.0->spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (2.4.7)
Requirement already satisfied: smart-open<4.0.0,>=2.2.0 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from pathy>=0.3.5->spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (3.0.0)
Requirement already satisfied: dataclasses<1.0,>=0.6 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from pathy>=0.3.5->spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (0.8)
Requirement already satisfied: idna<3,>=2.5 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (2.10)
Requirement already satisfied: chardet<5,>=3.0.2 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (4.0.0)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (2020.12.5)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (1.26.4)
Requirement already satisfied: contextvars<3,>=2.4 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from thinc<8.1.0,>=8.0.2->spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (2.4)
Requirement already satisfied: immutables>=0.9 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from contextvars<3,>=2.4->thinc<8.1.0,>=8.0.2->spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (0.15)
Requirement already satisfied: click<7.2.0,>=7.1.1 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from typer<0.4.0,>=0.3.0->spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (7.1.2)
Requirement already satisfied: MarkupSafe>=0.23 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from jinja2->spacy<3.1.0,>=3.0.0->en-core-web-md==3.0.0) (1.1.1)
Installing collected packages: en-core-web-md
Successfully installed en-core-web-md-3.0.0
✔ Download and installation successful
You can now load the package via spacy.load('en_core_web_md')
```

BBC News ကနေ အင်္ဂလိပ်လို ရေးထားတဲ့ စာကြောင်းတစ်ကြောင်းကို ကော်ပီကူးယူပြီး parsing လုပ်ကြည့်တော့ အိုကေသွားတာကို တွေ့ရတယ်။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ python ./benepar-test.py 
/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/distributions/distribution.py:46: UserWarning: <class 'torch_struct.distributions.TreeCRF'> does not define `arg_constraints`. Please set `arg_constraints = {}` or initialize the distribution with `validate_args=False` to turn off validation.
  'with `validate_args=False` to turn off validation.')
(S (NP (NNP State) (NNP TV)) (VP (VBD had) (VP (VBN warned) (PP (IN in) (NP (DT a) (JJ separate) (NN broadcast))) (PP (IN on) (NP (NNP Friday))) (SBAR (IN that) (S (NP (NNS people)) (`` ") (VP (MD should) (VP (VB learn) (PP (IN from) (NP (NP (DT the) (NN tragedy)) (PP (IN of) (NP (JJR earlier) (JJ ugly) (NNS deaths))))) (SBAR (IN that) (S (NP (PRP you)) (VP (MD can) (VP (VB be) (PP (IN in) (NP (NP (NN danger)) (PP (IN of) (S (VP (VBG getting) (VP (VBN shot) (PP (IN to) (NP (DT the) (NN head) (CC and) (RB back))))))))))))))))))) (. ") ('' .))
('S',)
State TV
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$
```
## Parsing a Corpus

ဒီတစ်ခါတော့ အင်္ဂလိပ်စာ စာကြောင်းရေ ၂သိန်းကျော်ရှိတဲ့ WAT2021 share MT Task ရဲ့ အင်္ဂလိပ်စာ corpus ကို parsing လုပ်ကြည့်ပါမယ်။  
program ကို အောက်ပါအတိုင်းရေးခဲ့ပါတယ်။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ cat benepar-file.py 
import benepar, spacy
import sys

filename = sys.argv[1]
nlp = spacy.load('en_core_web_md')

if spacy.__version__.startswith('2'):
   nlp.add_pipe(benepar.BeneparComponent("benepar_en3"))
else:
   nlp.add_pipe("benepar", config={"model": "benepar_en3"})

r_file = open(filename, "r")
with open(filename+".parse.txt","a") as w_file:
    for line in r_file:
       doc = nlp(line)
       sent = list(doc.sents)[0]
       #print(sent._.parse_string)
       w_file.write(sent._.parse_string+"\n")

(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$
```

parsing လုပ်တာ ဘယ်လောက်ကြာသလဲ ဆိုတာကိုလည်း သိချင်လို့ python command ရဲ့ ရှေ့မှာ time command ကို ခံထားခဲ့ပါတယ်။  
input file က train.en ဖိုင်ပါ။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ time python ./benepar-file.py ./train.en
/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/distributions/distribution.py:46: UserWarning: <class 'torch_struct.distributions.TreeCRF'> does not define `arg_constraints`. Please set `arg_constraints = {}` or initialize the distribution with `validate_args=False` to turn off validation.
  'with `validate_args=False` to turn off validation.')
Token indices sequence length is longer than the specified maximum sequence length for this model (537 > 512). Running this sequence through the model will result in indexing errors
Traceback (most recent call last):
  File "./benepar-file.py", line 15, in <module>
    doc = nlp(line)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/spacy/language.py", line 995, in __call__
    error_handler(name, proc, [doc], e)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/spacy/util.py", line 1498, in raise_error
    raise e
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/spacy/language.py", line 990, in __call__
    doc = proc(doc, **component_cfg.get(name, {}))
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/benepar-0.2.0-py3.6.egg/benepar/integrations/spacy_plugin.py", line 154, in __call__
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/benepar-0.2.0-py3.6.egg/benepar/parse_chart.py", line 414, in parse
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/benepar-0.2.0-py3.6.egg/benepar/parse_chart.py", line 414, in <listcomp>
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/benepar-0.2.0-py3.6.egg/benepar/parse_chart.py", line 193, in encode
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/benepar-0.2.0-py3.6.egg/benepar/retokenization.py", line 179, in __call__
ValueError: Sentence of length 538 (in sub-word tokens) exceeds the maximum supported length of 512

real	4m16.785s
user	4m20.542s
sys	0m6.267s
```
parsing time က မြန်ပါတယ်။ သို့သော် အထက်မှာ မြင်ရတဲ့အတိုင်း parser က လုပ်ပေးနိုင်တာက sentence length က 512 အထိက maximum လို့ ထင်တယ်။   
input လုပ်လိုက်တဲ့ corpus ဖိုင်နဲ့ parse လုပ်ပြီး ထွက်လာတဲ့ output ဖိုင်ရဲ့ စာကြောင်းရေ အရေအတွက်ကို နှိုင်းယှဉ်ကြည့်တော့ အောက်ပါအတိုင်း 8263 ကြောင်းကိုပဲ parsing လုပ်ပေးနိုင်တာကို တွေ့ရပါလိမ့်မယ်။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ wc ./train.en
  238014  3357260 17186660 ./train.en
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ wc ./train.en.parse.txt 
   8263  472855 2521622 ./train.en.parse.txt
```
parsed လုပ်ထားတဲ့ စာကြောင်းတချို့ကို ကြည့်ကြည့်ရအောင်။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/self-attentive-parser$ head ./train.en.parse.txt 
(S (NP (DT A) (NN murder) (NN case)) (VP (VBZ has) (VP (VBN been) (VP (VBN opened) (PP (IN at) (NP (DT the) (NNP Kyeikgyaung) (NN police) (NN station)))))) (. .))
(S (NP (NNS Police)) (VP (VBP are) (VP (VBG investigating))) (. .))
(S (NP (NNP Tatmadaw) (NNS troops)) (VP (VBD seized) (NP (NP (NNS arms)) (CC and) (NP (JJ illegal) (NN timber))) (PP (IN from) (NP (DT a) (NN vehicle))) (PP (IN during) (NP (NP (NP (DT a) (JJ surprise) (NN check)) (PP (IN in) (NP (NP (NNP Tarmoenyae)) (PP (IN in) (NP (JJ northern) (NNP Shan) (NN state)))))) (NP (NN yesterday))))) (. .))
(S (NP (DT The) (NNS police)) (VP (VBD intercepted) (CC and) (VBD searched) (NP (DT a) (NNP Mitsubishi) (NNP Pajero))) (. .))
(S (NP (DT The) (NNS police)) (VP (VBD discovered) (NP (NP (CD one) (NN pistol)) (VP (VBN loaded) (PP (IN with) (NP (NP (CD seven) (NNS bullets)) (CC and) (NP (NP (CD 740) (NNS pieces)) (PP (IN of) (NP (JJ sawed) (NN timber))))))))) (. .))
(S (NP (DT The) (NNS troops)) (VP (MD will) (VP (VB hand) (PRT (RP over)) (NP (NP (NP (NNP U) (NNP Sai) (NNP Kyaw) (NNP Win)) (, ,) (NP (NP (DT the) (NN driver)) (PP (IN of) (NP (DT the) (NN car))))) (, ,) (CC and) (NP (NP (NNP U) (NNP Than) (NNP Maung)) (, ,) (SBAR (WHNP (WP who)) (S (VP (VBD was) (NP (NP (NP (DT a) (NN passenger)) (PP (IN on) (NP (NN board)))) (VP (VBG carrying) (NP (DT the) (NN pistol))))))) (, ,))) (PP (IN to) (NP (NNP Tarmoenyae) (NN police) (NN station))) (, ,) (PP (VBG according) (PP (IN to) (NP (DT the) (JJ local) (NNS authorities)))))) (. .))
(S (NP (NN Fighting)) (VP (VBD happened) (PP (IN between) (NP (NP (NP (NNP Tatmadaw) (CC &) (CD amp) (SYM ;) (NNP apos) (-RRB- ;) (POS s)) (NNS troops)) (CC and) (NP (NNP KIA) (JJ armed) (NN group))))) (. .))
(S (NP (NP (DT An) (JJ armed) (NN clash)) (PP (IN between) (NP (NP (DT the) (NNS troops)) (PP (IN of) (NP (DT the) (NML (NNP Tatmadaw) (CC and) (NNP KIA)) (JJ armed) (NN group)))))) (VP (VBD happened) (NP (NN yesterday)) (PP (IN in) (NP (NP (NNP Muse) (NN township)) (PP (IN in) (NP (JJ northern) (NNP Shan) (NN state)))))) (. .))
(S (NP (NP (DT The) (NNS troops)) (PP (IN of) (NP (DT the) (NNP Tatmadaw)))) (VP (VBD returned) (NP (NN fire)) (PP (IN to) (NP (DT the) (JJ armed) (NN group))) (SBAR (IN after) (S (NP (PRP they)) (VP (VBD were) (VP (VBN attacked) (PP (IN by) (NP (DT the) (NN group))) (ADVP (ADVP (NP (QP (RB about) (CD four)) (NNS miles)) (RB east) (PP (IN of) (NP (NNP Mawtaung) (NN village)))) (SBAR (IN while) (S (VP (VBG conducting) (NP (NN area) (NN clearance) (NN operation))))))))))) (. .))
(S (NP (DT The) (JJ armed) (NN group)) (VP (VBD withdrew) (PP (IN to) (NP (NML (JJ south) (HYPH -) (NN west)) (NN direction)))) (. .))
```

## Reference

https://github.com/explosion/spaCy/issues/4577  
https://github.com/nikitakit/self-attentive-parser   


