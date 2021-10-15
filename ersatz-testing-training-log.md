# ersatz Testing Log

## git clone

pip နဲ့ install လုပ်ပြီး သုံးတာမျိုးလည်း လုပ်လို့ ရပေမဲ့... source code ကိုပဲ git clone လုပ်ပြီး ကိုယ်စက်ထဲမှာပဲ setup run ဖို့ ဆုံးဖြတ်ခဲ့...  

```
(base) ye@:~/exp/sentence-seg$ git clone https://github.com/rewicks/ersatz
Cloning into 'ersatz'...
remote: Enumerating objects: 627, done.
remote: Counting objects: 100% (627/627), done.
remote: Compressing objects: 100% (385/385), done.
remote: Total 627 (delta 382), reused 470 (delta 227), pack-reused 0
Receiving objects: 100% (627/627), 8.76 MiB | 13.89 MiB/s, done.
Resolving deltas: 100% (382/382), done.
(base) ye@:~/exp/sentence-seg$ cd ersatz/
(base) ye@:~/exp/sentence-seg/ersatz$ ls
environment.yml  ersatz  LICENSE  README.md  scripts  setup.py  tapes
```

## Run setup.py

python ပရိုဂရမ်တွေကို install လုပ်နေကျပုံစံအတိုင်း setup.py ကို run ပြီး အောက်ပါအတိုင်း installation လုပ်ခဲ့တယ်။  

```
(base) ye@:~/exp/sentence-seg/ersatz$ python setup.py install
running install
running bdist_egg
running egg_info
creating ersatz.egg-info
writing ersatz.egg-info/PKG-INFO
writing dependency_links to ersatz.egg-info/dependency_links.txt
writing entry points to ersatz.egg-info/entry_points.txt
writing requirements to ersatz.egg-info/requires.txt
writing top-level names to ersatz.egg-info/top_level.txt
writing manifest file 'ersatz.egg-info/SOURCES.txt'
reading manifest file 'ersatz.egg-info/SOURCES.txt'
adding license file 'LICENSE'
writing manifest file 'ersatz.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
creating build
creating build/lib
creating build/lib/ersatz
copying ersatz/split.py -> build/lib/ersatz
copying ersatz/utils.py -> build/lib/ersatz
copying ersatz/__init__.py -> build/lib/ersatz
copying ersatz/trainer.py -> build/lib/ersatz
copying ersatz/dataset.py -> build/lib/ersatz
copying ersatz/score.py -> build/lib/ersatz
copying ersatz/candidates.py -> build/lib/ersatz
copying ersatz/subword.py -> build/lib/ersatz
copying ersatz/model.py -> build/lib/ersatz
creating build/bdist.linux-x86_64
creating build/bdist.linux-x86_64/egg
creating build/bdist.linux-x86_64/egg/ersatz
copying build/lib/ersatz/split.py -> build/bdist.linux-x86_64/egg/ersatz
copying build/lib/ersatz/utils.py -> build/bdist.linux-x86_64/egg/ersatz
copying build/lib/ersatz/__init__.py -> build/bdist.linux-x86_64/egg/ersatz
copying build/lib/ersatz/trainer.py -> build/bdist.linux-x86_64/egg/ersatz
copying build/lib/ersatz/dataset.py -> build/bdist.linux-x86_64/egg/ersatz
copying build/lib/ersatz/score.py -> build/bdist.linux-x86_64/egg/ersatz
copying build/lib/ersatz/candidates.py -> build/bdist.linux-x86_64/egg/ersatz
copying build/lib/ersatz/subword.py -> build/bdist.linux-x86_64/egg/ersatz
copying build/lib/ersatz/model.py -> build/bdist.linux-x86_64/egg/ersatz
byte-compiling build/bdist.linux-x86_64/egg/ersatz/split.py to split.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/ersatz/utils.py to utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/ersatz/__init__.py to __init__.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/ersatz/trainer.py to trainer.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/ersatz/dataset.py to dataset.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/ersatz/score.py to score.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/ersatz/candidates.py to candidates.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/ersatz/subword.py to subword.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/ersatz/model.py to model.cpython-37.pyc
creating build/bdist.linux-x86_64/egg/EGG-INFO
copying ersatz.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying ersatz.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying ersatz.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying ersatz.egg-info/entry_points.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying ersatz.egg-info/requires.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying ersatz.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
zip_safe flag not set; analyzing archive contents...
ersatz.__pycache__.dataset.cpython-37: module references __file__
ersatz.__pycache__.score.cpython-37: module references __file__
ersatz.__pycache__.split.cpython-37: module references __file__
ersatz.__pycache__.trainer.cpython-37: module references __file__
creating dist
creating 'dist/ersatz-1.0.0-py3.7.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing ersatz-1.0.0-py3.7.egg
creating /home/ye/anaconda3/lib/python3.7/site-packages/ersatz-1.0.0-py3.7.egg
Extracting ersatz-1.0.0-py3.7.egg to /home/ye/anaconda3/lib/python3.7/site-packages
Adding ersatz 1.0.0 to easy-install.pth file
Installing ersatz script to /home/ye/anaconda3/bin
Installing ersatz_preprocess script to /home/ye/anaconda3/bin
Installing ersatz_score script to /home/ye/anaconda3/bin
Installing ersatz_train script to /home/ye/anaconda3/bin

Installed /home/ye/anaconda3/lib/python3.7/site-packages/ersatz-1.0.0-py3.7.egg
Processing dependencies for ersatz==1.0.0
Searching for progressbar2
Reading https://pypi.org/simple/progressbar2/
Downloading https://files.pythonhosted.org/packages/48/3d/705d2101f918e227cd039f567cd150b6ae5fe492c8850fc5b741106abb35/progressbar2-3.53.3-py2.py3-none-any.whl#sha256=6610fe393a4591967ecf9062d42c0663c8862092245c490e5971ec5f348755ca
Best match: progressbar2 3.53.3
Processing progressbar2-3.53.3-py2.py3-none-any.whl
Installing progressbar2-3.53.3-py2.py3-none-any.whl to /home/ye/anaconda3/lib/python3.7/site-packages
Adding progressbar2 3.53.3 to easy-install.pth file

Installed /home/ye/anaconda3/lib/python3.7/site-packages/progressbar2-3.53.3-py3.7.egg
Searching for sentencepiece==0.1.95
Reading https://pypi.org/simple/sentencepiece/
Downloading https://files.pythonhosted.org/packages/f5/99/e0808cb947ba10f575839c43e8fafc9cc44e4a7a2c8f79c60db48220a577/sentencepiece-0.1.95-cp37-cp37m-manylinux2014_x86_64.whl#sha256=ad2866aebdf702b0d6a992b2b3b46c2de3739ca8a92bce17f24cf51c29fa4f3e
Best match: sentencepiece 0.1.95
Processing sentencepiece-0.1.95-cp37-cp37m-manylinux2014_x86_64.whl
Installing sentencepiece-0.1.95-cp37-cp37m-manylinux2014_x86_64.whl to /home/ye/anaconda3/lib/python3.7/site-packages
Adding sentencepiece 0.1.95 to easy-install.pth file

Installed /home/ye/anaconda3/lib/python3.7/site-packages/sentencepiece-0.1.95-py3.7-linux-x86_64.egg
Searching for torch==1.7.1
Reading https://pypi.org/simple/torch/
Downloading https://files.pythonhosted.org/packages/90/5d/095ddddc91c8a769a68c791c019c5793f9c4456a688ddd235d6670924ecb/torch-1.7.1-cp37-cp37m-manylinux1_x86_64.whl#sha256=5d76c255a41484c1d41a9ff570b9c9f36cb85df9428aa15a58ae16ac7cfc2ea6
Best match: torch 1.7.1
Processing torch-1.7.1-cp37-cp37m-manylinux1_x86_64.whl
Installing torch-1.7.1-cp37-cp37m-manylinux1_x86_64.whl to /home/ye/anaconda3/lib/python3.7/site-packages
Adding torch 1.7.1 to easy-install.pth file
Installing convert-caffe2-to-onnx script to /home/ye/anaconda3/bin
Installing convert-onnx-to-caffe2 script to /home/ye/anaconda3/bin

Installed /home/ye/anaconda3/lib/python3.7/site-packages/torch-1.7.1-py3.7-linux-x86_64.egg
Searching for python-utils>=2.3.0
Reading https://pypi.org/simple/python-utils/
Downloading https://files.pythonhosted.org/packages/62/47/974eb168d5012bc8841d4b5be10e345f3e706e25fa1661b68f193e16ca67/python_utils-2.5.6-py2.py3-none-any.whl#sha256=18fbc1a1df9a9061e3059a48ebe5c8a66b654d688b0e3ecca8b339a7f168f208
Best match: python-utils 2.5.6
Processing python_utils-2.5.6-py2.py3-none-any.whl
Installing python_utils-2.5.6-py2.py3-none-any.whl to /home/ye/anaconda3/lib/python3.7/site-packages
Adding python-utils 2.5.6 to easy-install.pth file

Installed /home/ye/anaconda3/lib/python3.7/site-packages/python_utils-2.5.6-py3.7.egg
Searching for tensorboard==2.4.1
Best match: tensorboard 2.4.1
Adding tensorboard 2.4.1 to easy-install.pth file
Installing tensorboard script to /home/ye/anaconda3/bin

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for six==1.14.0
Best match: six 1.14.0
Adding six 1.14.0 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for setuptools==57.2.0
Best match: setuptools 57.2.0
Adding setuptools 57.2.0 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for requests==2.22.0
Best match: requests 2.22.0
Adding requests 2.22.0 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for tensorboard-plugin-wit==1.8.0
Best match: tensorboard-plugin-wit 1.8.0
Adding tensorboard-plugin-wit 1.8.0 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for Werkzeug==1.0.0
Best match: Werkzeug 1.0.0
Adding Werkzeug 1.0.0 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for grpcio==1.35.0
Best match: grpcio 1.35.0
Adding grpcio 1.35.0 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for absl-py==0.11.0
Best match: absl-py 0.11.0
Adding absl-py 0.11.0 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for protobuf==3.14.0
Best match: protobuf 3.14.0
Adding protobuf 3.14.0 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for google-auth-oauthlib==0.4.2
Best match: google-auth-oauthlib 0.4.2
Adding google-auth-oauthlib 0.4.2 to easy-install.pth file
Installing google-oauthlib-tool script to /home/ye/anaconda3/bin

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for wheel==0.34.2
Best match: wheel 0.34.2
Adding wheel 0.34.2 to easy-install.pth file
Installing wheel script to /home/ye/anaconda3/bin

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for Markdown==3.3.3
Best match: Markdown 3.3.3
Adding Markdown 3.3.3 to easy-install.pth file
Installing markdown_py script to /home/ye/anaconda3/bin

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for google-auth==1.24.0
Best match: google-auth 1.24.0
Adding google-auth 1.24.0 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for numpy==1.18.1
Best match: numpy 1.18.1
Adding numpy 1.18.1 to easy-install.pth file
Installing f2py script to /home/ye/anaconda3/bin
Installing f2py3 script to /home/ye/anaconda3/bin
Installing f2py3.7 script to /home/ye/anaconda3/bin

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for typing-extensions==3.7.4.3
Best match: typing-extensions 3.7.4.3
Adding typing-extensions 3.7.4.3 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for urllib3==1.25.8
Best match: urllib3 1.25.8
Adding urllib3 1.25.8 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for idna==2.8
Best match: idna 2.8
Adding idna 2.8 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for certifi==2019.11.28
Best match: certifi 2019.11.28
Adding certifi 2019.11.28 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for chardet==3.0.4
Best match: chardet 3.0.4
Adding chardet 3.0.4 to easy-install.pth file
Installing chardetect script to /home/ye/anaconda3/bin

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for requests-oauthlib==1.3.0
Best match: requests-oauthlib 1.3.0
Adding requests-oauthlib 1.3.0 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for importlib-metadata==1.5.0
Best match: importlib-metadata 1.5.0
Adding importlib-metadata 1.5.0 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for pyasn1-modules==0.2.8
Best match: pyasn1-modules 0.2.8
Adding pyasn1-modules 0.2.8 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for cachetools==4.2.1
Best match: cachetools 4.2.1
Adding cachetools 4.2.1 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for rsa==4.7
Best match: rsa 4.7
Adding rsa 4.7 to easy-install.pth file
Installing pyrsa-decrypt script to /home/ye/anaconda3/bin
Installing pyrsa-encrypt script to /home/ye/anaconda3/bin
Installing pyrsa-keygen script to /home/ye/anaconda3/bin
Installing pyrsa-priv2pub script to /home/ye/anaconda3/bin
Installing pyrsa-sign script to /home/ye/anaconda3/bin
Installing pyrsa-verify script to /home/ye/anaconda3/bin

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for oauthlib==3.1.0
Best match: oauthlib 3.1.0
Adding oauthlib 3.1.0 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for zipp==2.2.0
Best match: zipp 2.2.0
Adding zipp 2.2.0 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for pyasn1==0.4.8
Best match: pyasn1 0.4.8
Adding pyasn1 0.4.8 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Finished processing dependencies for ersatz==1.0.0
(base) ye@:~/exp/sentence-seg/ersatz$ 
```

## call --help

```
(base) ye@:~/exp/sentence-seg/ersatz$ ersatz --help
usage: ersatz [-h] [--model MODEL] [--input INPUT] [--output OUTPUT] [OPTIONS]

ERSATZ SEGMENTER: Segments input text into sentences.
      Example: ersatz --model fr --input wikipedia.fr --output output.fr

optional arguments:
  -h, --help            show this help message and exit

arguments:
  --model MODEL, -m MODEL
                        Either name of or path to a pre-trained ersatz model
  --input INPUT, -i INPUT
                        Input file. None means stdin
  --output OUTPUT, -o OUTPUT
                        Output file. None means stdout
  --batch-size BATCH_SIZE, -b BATCH_SIZE
                        Batch size--predictions to make at once
  --candidates {multilingual,en,all}, -c {multilingual,en,all}
                        Criteria for selecting candidate sites. Defaults to 'multilingual'
                           * multilingual: [EOS punctuation][!number] (sentence-ending punctuation followed by a non-digit)
                           * en: [EOS punctuation][any_punctuation]*[space] (sentence-ending punctuation followed by a space)
                           * all: all possible contexts
  --cpu                 Uses CPU (GPU is default if available)

tsv options:
  Used for splitting .csv/.tsv/etc files. This mode triggered by '--columns'

  --delimiter DELIMITER, -d DELIMITER
                        Delimiter character (default is \t)
                          * '--columns' must be set
  --columns [COLUMNS [COLUMNS ...]], -C [COLUMNS [COLUMNS ...]]
                        Columns to split (0-indexed). If empty, plain-text

additional options:
  --version, -V         Prints ersatz version
  --download, -D        Downloads model selected via '--model'
  --list, -l            Lists available models.
  --quiet, -q           Disables logging.
(base) ye@:~/exp/sentence-seg/ersatz$
```

## Run with --list Option

```
(base) ye@:~/exp/sentence-seg/ersatz$ ersatz --list
	- en (monolingual/en) : An English monolingual model trained on English News Commentary
	- ar (monolingual-ar) : An Arabic monolingual model trained on Arabic News Commentary and Wikipedia data
	- cs (monolingual-cs) : A Czech monolingual model trained on Czech News Commentary and Wikipedia data
	- de (monolingual-de) : A German monolingual model trained on German News Commentary and Wikipedia data
	- es (monolingual-es) : A Spanish monolingual model trained on Spanish News Commentary data
	- et (monolingual-et) : A Estonian monolingual model trained on Estonian News Crawl data
	- fi (monolingual-fi) : A Finnish monolingual model trained on Finnish News Crawl and Wikipedia data
	- fr (monolingual-fr) : A French monolingual model trained on French News Commentary and Wikipedia data
	- gu (monolingual-gu) : A Gujarti monolingual model trained on Gujarti News Crawl and Common Crawl data
	- hi (monolingual-hi) : A Hindi monolingual model trained on Hindi News Commentary, News Crawl, and Wikipeda data
	- iu (monolingual-iu) : A Inuktitut monolingual model trained on Inuktitut data from the Nunavut-Hansard-Inuktitut-English Parallel Corpus 3.0
	- ja (monolingual-ja) : A Japanese monolingual model trained on Japanese News Commentary and News Crawl data
	- kk (monolingual-kk) : A Kazakh monolingual model trained on Kazakh News Commentary and News Crawl data
	- km (monolingual-km) : A Khmer monolingual model trained on Khmer JW300 Corpus and Common Crawl data
	- lt (monolingual-lt) : A Lithuanian monolingual model trained on Lithuanian News Crawl and Wikipedia data
	- lv (monolingual-lv) : A Latvian monolingual model trained on Latvian News Crawl data
	- pl (monolingual-pl) : A Polish monolingual model trained on Polish News Crawl, Global Voices, and Wikipedia data
	- ps (monolingual-ps) : A Pashto monolingual model trained on Pashto News Crawl, SADA, SYSTRAN, and TRANSTAC data
	- ro (monolingual-ro) : A Romanian monolingual model trained on Romanian News Crawl, Global Voices, and Wikipedia data
	- ru (monolingual-ru) : A Russian monolingual model trained on Russian News Commentary and Wikipedia data
	- ta (monolingual-ta) : A Tamil monolingual model trained on Tamil Wikipedia and News Crawl data
	- tr (monolingual-tr) : A Turkish monolingual model trained on Turkish Global Voices, Wikipedia, and News Crawl data
	- zh (monolingual-zh) : A Chinese monolingual model trained on Chinese News Commentary and Wikipedia data
	- default-multilingual (multilingual/wmtlangs) : A multilingual model, including languages commonly associated with WMT tasks and datasets
(base) ye@:~/exp/sentence-seg/ersatz$ 
```

## 1st Time Running

ပထမဆုံး ဂျပန်စာကြောင်း တချို့ကို ပြင်ဆင်ပြီး pre-trained model နဲ့ sentence segmentation လုပ်ကြည့်တော့ အောက်ပါအတိုင်း error ပေးတယ်...  

```
(base) ye@:~/exp/sentence-seg/ersatz$ ersatz --input ./jp.txt --output ./output.txt
2021-10-11 00:33:18 | INFO | ersatz | Segmentation model: "default-multilingual"
2021-10-11 00:33:18 | INFO | ersatz | Model description: "multilingual/wmtlangs"
2021-10-11 00:33:18 | INFO | ersatz | Release Date: "01 June 2021"
2021-10-11 00:33:18 | INFO | ersatz | USING "default-multilingual" model found at /home/ye/.ersatz/multilingual/wmtlangs/01.Jun.21.multilingual
Traceback (most recent call last):
  File "/home/ye/anaconda3/bin/ersatz", line 33, in <module>
    sys.exit(load_entry_point('ersatz==1.0.0', 'console_scripts', 'ersatz')())
  File "/home/ye/anaconda3/lib/python3.7/site-packages/ersatz-1.0.0-py3.7.egg/ersatz/split.py", line 317, in main
    split(args)
  File "/home/ye/anaconda3/lib/python3.7/site-packages/ersatz-1.0.0-py3.7.egg/ersatz/split.py", line 283, in split
    model = EvalModel(model_path)
  File "/home/ye/anaconda3/lib/python3.7/site-packages/ersatz-1.0.0-py3.7.egg/ersatz/split.py", line 62, in __init__
    self.model = load_model(model_path)
  File "/home/ye/anaconda3/lib/python3.7/site-packages/ersatz-1.0.0-py3.7.egg/ersatz/split.py", line 49, in load_model
    tokenizer = SentencePiece(serialization=model_dict['tokenizer'])
  File "/home/ye/anaconda3/lib/python3.7/site-packages/ersatz-1.0.0-py3.7.egg/ersatz/subword.py", line 96, in __init__
    self.model = spm.SentencePieceProcessor(model_proto=serialization)
TypeError: __init__() got an unexpected keyword argument 'model_proto'
(base) ye@:~/exp/sentence-seg/ersatz$
```

မော်ဒယ်က မရှိသေးရင် ersatz က auto download လုပ်ပေးတယ်။  
မော်ဒယ်ဖိုင်ရဲ့ path ကို ပေးကြည့်ပြီး run ရင်လည်း error ပေးနေတယ်။   

```
(base) ye@:~/exp/sentence-seg/ersatz$ ersatz --input ./input.ja --output ./output.ja --model ./model/01.Jun.21.ja 
Traceback (most recent call last):
  File "/home/ye/anaconda3/bin/ersatz", line 33, in <module>
    sys.exit(load_entry_point('ersatz==1.0.0', 'console_scripts', 'ersatz')())
  File "/home/ye/anaconda3/lib/python3.7/site-packages/ersatz-1.0.0-py3.7.egg/ersatz/split.py", line 317, in main
    split(args)
  File "/home/ye/anaconda3/lib/python3.7/site-packages/ersatz-1.0.0-py3.7.egg/ersatz/split.py", line 280, in split
    model = EvalModel(args.model)
  File "/home/ye/anaconda3/lib/python3.7/site-packages/ersatz-1.0.0-py3.7.egg/ersatz/split.py", line 62, in __init__
    self.model = load_model(model_path)
  File "/home/ye/anaconda3/lib/python3.7/site-packages/ersatz-1.0.0-py3.7.egg/ersatz/split.py", line 49, in load_model
    tokenizer = SentencePiece(serialization=model_dict['tokenizer'])
  File "/home/ye/anaconda3/lib/python3.7/site-packages/ersatz-1.0.0-py3.7.egg/ersatz/subword.py", line 96, in __init__
    self.model = spm.SentencePieceProcessor(model_proto=serialization)
TypeError: __init__() got an unexpected keyword argument 'model_proto'
(base) ye@:~/exp/sentence-seg/ersatz$ pip3 show sentencepiece
Name: sentencepiece
Version: 0.1.8
Summary: SentencePiece python wrapper
Home-page: https://github.com/google/sentencepiece
Author: Taku Kudo
Author-email: taku@google.com
License: Apache
Location: /home/ye/anaconda3/lib/python3.7/site-packages
Requires: 
Required-by: torchtext, ersatz
(base) ye@:~/exp/sentence-seg/ersatz$
```

sentencepiece နဲ့ vocab ဆောက်တဲ့အခါမှာ ပေးနေတဲ့ error လို့ နားလည်တယ်။   
အဲဒါကြောင့် uninstall လုပ်ပြီး အသစ် install ပြန်လုပ်ခဲ့တယ်။  

```
(base) ye@:~/exp/sentence-seg/ersatz$ pip uninstall sentencepiece
Found existing installation: sentencepiece 0.1.8
Uninstalling sentencepiece-0.1.8:
  Would remove:
    /home/ye/anaconda3/lib/python3.7/site-packages/_sentencepiece.cpython-37m-x86_64-linux-gnu.so
    /home/ye/anaconda3/lib/python3.7/site-packages/sentencepiece-0.1.8.dist-info/*
    /home/ye/anaconda3/lib/python3.7/site-packages/sentencepiece.py
Proceed (Y/n)? Y
  Successfully uninstalled sentencepiece-0.1.8
(base) ye@:~/exp/sentence-seg/ersatz$ pip install sentencepiece
Requirement already satisfied: sentencepiece in /home/ye/anaconda3/lib/python3.7/site-packages/sentencepiece-0.1.95-py3.7-linux-x86_64.egg (0.1.95)
```

ဒီတစ်ခါ run ကြည့်တော့ ရသွားပြီ...  

```
(base) ye@:~/exp/sentence-seg/ersatz$ ersatz --input ./input.ja --output ./output.ja --model ./model/01.Jun.21.ja 
(base) ye@:~/exp/sentence-seg/ersatz$ cat output.ja 
私の名前はイェです。
現在は自然言語処理の研究を一所懸命行っています。
具体的には機械翻訳、音声認識、音声合成などです。
(base) ye@:~/exp/sentence-seg/ersatz$ 
```

input ဂျပန်ဖိုင်က အောက်ပါလိုမျိုး ရိုက်ထားတာ...  

```
(base) ye@:~/exp/sentence-seg/ersatz$ cat ./input.ja
私の名前はイェです。現在は自然言語処理の研究を一所懸命行っています。具体的には機械翻訳、音声認識、音声合成などです。
```

### Testing with English

အင်္ဂလိပ်စာနဲ့ စမ်းကြည့်တော့လည်း အလုပ်လုပ်ပေးတယ်။  

```
(base) ye@:~/exp/sentence-seg/ersatz$ cat ./input.en 
Tea is an evil substance! Tea is much more dangerous then beer. Please avoid drinking tea. I discovered this last night. I had drunk 14. I discovered this last night. I had drunk 14 beers up until 3.00 am at the pub while my wife was just drinking  tea at home. You should have seen how angry and violent she was when I got home. I was peaceful, silent and headed to bed as she shouted at me, all night long and even into the next morning. Please ladies, if you can't handle your tea, just don't drink it....
(base) ye@:~/exp/sentence-seg/ersatz$ ersatz --input ./input.en --output ./output.en
2021-10-11 01:17:29 | INFO | ersatz | Segmentation model: "default-multilingual"
2021-10-11 01:17:29 | INFO | ersatz | Model description: "multilingual/wmtlangs"
2021-10-11 01:17:29 | INFO | ersatz | Release Date: "01 June 2021"
2021-10-11 01:17:29 | INFO | ersatz | USING "default-multilingual" model found at /home/ye/.ersatz/multilingual/wmtlangs/01.Jun.21.multilingual
(base) ye@:~/exp/sentence-seg/ersatz$ cat ./output.en 
Tea is an evil substance!
Tea is much more dangerous then beer.
Please avoid drinking tea.
I discovered this last night.
I had drunk 14.
I discovered this last night.
I had drunk 14 beers up until 3.00 am at the pub while my wife was just drinking tea at home.
You should have seen how angry and violent she was when I got home.
I was peaceful, silent and headed to bed as she shouted at me, all night long and even into the next morning.
Please ladies, if you can't handle your tea, just don't drink it....
(base) ye@:~/exp/sentence-seg/ersatz$ 
```

## Testing with Python Script

Testing for Japanese...  

```
(base) ye@:~/exp/sentence-seg/ersatz/ersatz$ cat ../input.ja | python ./split.py 
2021-10-11 09:55:36 | INFO | ersatz | Segmentation model: "default-multilingual"
2021-10-11 09:55:36 | INFO | ersatz | Model description: "multilingual/wmtlangs"
2021-10-11 09:55:36 | INFO | ersatz | Release Date: "01 June 2021"
2021-10-11 09:55:36 | INFO | ersatz | USING "default-multilingual" model found at /home/ye/.ersatz/multilingual/wmtlangs/01.Jun.21.multilingual
私の名前はイェです。
現在は自然言語処理の研究を一所懸命行っています。
具体的には機械翻訳、音声認識、音声合成などです。
```

Testing for English...  

```
(base) ye@:~/exp/sentence-seg/ersatz/ersatz$ cat ../input.en | python ./split.py 
2021-10-11 09:55:47 | INFO | ersatz | Segmentation model: "default-multilingual"
2021-10-11 09:55:47 | INFO | ersatz | Model description: "multilingual/wmtlangs"
2021-10-11 09:55:47 | INFO | ersatz | Release Date: "01 June 2021"
2021-10-11 09:55:47 | INFO | ersatz | USING "default-multilingual" model found at /home/ye/.ersatz/multilingual/wmtlangs/01.Jun.21.multilingual
Tea is an evil substance!
Tea is much more dangerous then beer.
Please avoid drinking tea.
I discovered this last night.
I had drunk 14.
I discovered this last night.
I had drunk 14 beers up until 3.00 am at the pub while my wife was just drinking tea at home.
You should have seen how angry and violent she was when I got home.
I was peaceful, silent and headed to bed as she shouted at me, all night long and even into the next morning.
Please ladies, if you can't handle your tea, just don't drink it....
(base) ye@:~/exp/sentence-seg/ersatz/ersatz$ 
```

## Scoring on Sentence Segmentation

```
(base) ye@:~/exp/sentence-seg/ersatz/ersatz$ python ./score.py ../output.ja ../output.ja 
Accuracy 100.00
Recall 100.00
Precision 100.00
F1 100.00
0
(base) ye@:~/exp/sentence-seg/ersatz/ersatz$
```

အင်္ဂလိပ်စာ input ဖိုင် အသစ်တစ်ခုနဲ့ reference ဖိုင်ကို ပြင်ဆင်ပြီး scoring လုပ်ကြည့်ခဲ့...  
input ဖိုင်က အောက်ပါအတိုင်း...  

```
(base) ye@:~/exp/sentence-seg/ersatz/ersatz$ cat ./casual-eng.input 
Hiya, how ya doing? Not bad ya know, what about you? What’ve you been up to lately? Okay? Okay, coding sentence segmentation program till morning 3 am ... and thus, couldn't get up as normal ... 
```

sentence segmentation လုပ်ကြည့်ခဲ့...  

```
(base) ye@:~/exp/sentence-seg/ersatz/ersatz$ cat ./casual-eng.input | python ./split.py > ./casual-eng.sent-seg
2021-10-11 10:44:23 | INFO | ersatz | Segmentation model: "default-multilingual"
2021-10-11 10:44:23 | INFO | ersatz | Model description: "multilingual/wmtlangs"
2021-10-11 10:44:23 | INFO | ersatz | Release Date: "01 June 2021"
2021-10-11 10:44:23 | INFO | ersatz | USING "default-multilingual" model found at /home/ye/.ersatz/multilingual/wmtlangs/01.Jun.21.multilingual
```

sentence segmentation လုပ်ပြီးထွက်လာတဲ့ output က အောက်ပါအတိုင်း...  

```
(base) ye@:~/exp/sentence-seg/ersatz/ersatz$ cat ./casual-eng.sent-seg 
Hiya, how ya doing?
Not bad ya know, what about you?
What’ve you been up to lately? Okay?
Okay, coding sentence segmentation program till morning 3 am ... and thus, couldn't get up as normal ...
(base) ye@:~/exp/sentence-seg/ersatz/ersatz$ gedit casual-eng.ref
```

score.py ကို သုံးပြီး evaluation လုပ်ကြည့်ခဲ့...  

```
(base) ye@:~/exp/sentence-seg/ersatz/ersatz$ python ./score.py ./casual-eng.ref ./casual-eng.sent-seg 
till morning 3 am ... <mos>    and thus, couldn't get
Accuracy 99.37
Recall 75.00
Precision 100.00
F1 85.71
0
(base) ye@:~/exp/sentence-seg/ersatz/ersatz$
```

## Training a New Model

training data ကို myWord corpus ရဲ့ တစိတ်တပိုင်းကိုပဲ သုံးခဲ့...  

```
(base) ye@:/media/ye/project1/exp/word-segmentation$ cp segmentation-data-updated2.txt /home/ye/exp/sentence-seg/ersatz/my-data/
```

```
(base) ye@:~/exp/sentence-seg/ersatz/my-data$ wc ./segmentation-data-updated2.txt 
  213104  5342354 69130416 ./segmentation-data-updated2.txt
```

### Building Sentencepiece Vocab

မြန်မာစာ ဒေတာနဲ့ sentence segmentation ကို လုပ်ကြည့်ဖို့အတွက် အရင်ဆုံး sentencepiece vocab ဆောက်ရမယ်။  


```
(base) ye@:~/exp/sentence-seg/ersatz$ time spm_train --input ./my-data/segmentation-data-updated2.txt \
>    --model_prefix ersatz \
>    --bos_piece "<mos>" \
>    --eos_piece "<eos>"
sentencepiece_trainer.cc(77) LOG(INFO) Starts training with : 
trainer_spec {
  input: ./my-data/segmentation-data-updated2.txt
  input_format: 
  model_prefix: ersatz
  model_type: UNIGRAM
  vocab_size: 8000
  self_test_sample_size: 0
  character_coverage: 0.9995
  input_sentence_size: 0
  shuffle_input_sentence: 1
  seed_sentencepiece_size: 1000000
  shrinking_factor: 0.75
  max_sentence_length: 4192
  num_threads: 16
  num_sub_iterations: 2
  max_sentencepiece_length: 16
  split_by_unicode_script: 1
  split_by_number: 1
  split_by_whitespace: 1
  split_digits: 0
  treat_whitespace_as_suffix: 0
  required_chars: 
  byte_fallback: 0
  vocabulary_output_piece_score: 1
  train_extremely_large_corpus: 0
  hard_vocab_limit: 1
  use_all_vocab: 0
  unk_id: 0
  bos_id: 1
  eos_id: 2
  pad_id: -1
  unk_piece: <unk>
  bos_piece: <mos>
  eos_piece: <eos>
  pad_piece: <pad>
  unk_surface:  ⁇ 
}
normalizer_spec {
  name: nmt_nfkc
  add_dummy_prefix: 1
  remove_extra_whitespaces: 1
  escape_whitespaces: 1
  normalization_rule_tsv: 
}
denormalizer_spec {}
trainer_interface.cc(319) LOG(INFO) SentenceIterator is not specified. Using MultiFileSentenceIterator.
trainer_interface.cc(174) LOG(INFO) Loading corpus: ./my-data/segmentation-data-updated2.txt
trainer_interface.cc(346) LOG(WARNING) Found too long line (9461 > 4192).
trainer_interface.cc(348) LOG(WARNING) Too long lines are skipped in the training.
trainer_interface.cc(349) LOG(WARNING) The maximum length can be changed with --max_sentence_length=<size> flag.
trainer_interface.cc(375) LOG(INFO) Loaded all 212778 sentences
trainer_interface.cc(381) LOG(INFO) Skipped 326 too long sentences.
trainer_interface.cc(390) LOG(INFO) Adding meta_piece: <unk>
trainer_interface.cc(390) LOG(INFO) Adding meta_piece: <mos>
trainer_interface.cc(390) LOG(INFO) Adding meta_piece: <eos>
trainer_interface.cc(395) LOG(INFO) Normalizing sentences...
trainer_interface.cc(456) LOG(INFO) all chars count=25965548
trainer_interface.cc(467) LOG(INFO) Done: 99.9504% characters are covered.
trainer_interface.cc(477) LOG(INFO) Alphabet size=222
trainer_interface.cc(478) LOG(INFO) Final character coverage=0.999504
trainer_interface.cc(510) LOG(INFO) Done! preprocessed 212777 sentences.
unigram_model_trainer.cc(138) LOG(INFO) Making suffix array...
unigram_model_trainer.cc(142) LOG(INFO) Extracting frequent sub strings...
unigram_model_trainer.cc(193) LOG(INFO) Initialized 174811 seed sentencepieces
trainer_interface.cc(516) LOG(INFO) Tokenizing input sentences with whitespace: 212777
trainer_interface.cc(526) LOG(INFO) Done! 98011
unigram_model_trainer.cc(488) LOG(INFO) Using 98011 sentences for EM training
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=0 size=63988 obj=9.37692 num_tokens=202253 num_tokens/piece=3.1608
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=1 size=48524 obj=7.66725 num_tokens=201920 num_tokens/piece=4.16124
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=0 size=36337 obj=7.62021 num_tokens=208142 num_tokens/piece=5.7281
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=1 size=36188 obj=7.60807 num_tokens=208173 num_tokens/piece=5.75254
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=0 size=27126 obj=7.62654 num_tokens=220854 num_tokens/piece=8.14178
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=1 size=27114 obj=7.62057 num_tokens=220866 num_tokens/piece=8.14583
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=0 size=20331 obj=7.65236 num_tokens=235889 num_tokens/piece=11.6024
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=1 size=20330 obj=7.64464 num_tokens=235899 num_tokens/piece=11.6035
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=0 size=15247 obj=7.69706 num_tokens=252323 num_tokens/piece=16.549
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=1 size=15247 obj=7.68693 num_tokens=252325 num_tokens/piece=16.5492
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=0 size=11435 obj=7.75846 num_tokens=269322 num_tokens/piece=23.5524
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=1 size=11432 obj=7.74631 num_tokens=269326 num_tokens/piece=23.559
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=0 size=8799 obj=7.83273 num_tokens=285463 num_tokens/piece=32.4427
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=1 size=8799 obj=7.81626 num_tokens=285465 num_tokens/piece=32.4429
trainer_interface.cc(604) LOG(INFO) Saving model: ersatz.model
trainer_interface.cc(615) LOG(INFO) Saving vocabs: ersatz.vocab

real	0m26.343s
user	0m33.230s
sys	0m0.224s
(base) ye@:~/exp/sentence-seg/ersatz$
```

check the output model...  

```
(base) ye@:~/exp/sentence-seg/ersatz$ wc ./ersatz.model 
 16576  11485 449195 ./ersatz.model
(base) ye@:~/exp/sentence-seg/ersatz$ file ./ersatz.model 
./ersatz.model: data
```

### Create a Training Data

```
(base) ye@:~/exp/sentence-seg/ersatz$ time python ./ersatz/dataset.py --sentencepiece_path ./ersatz.model  --left-size 3 --right-size 3 --output_path ./my-data/model/dataset.out --input_paths ./my-data/segmentation-data-updated2.txt 

real	0m23.790s
user	0m23.401s
sys	0m0.353s
(base) ye@:~/exp/sentence-seg/ersatz$
```

```
(base) ye@:~/exp/sentence-seg/ersatz/my-data/model$ wc dataset.out 
  18693  168237 1536691 dataset.out
(base) ye@:~/exp/sentence-seg/ersatz/my-data/model$ head dataset.out 
▁နိုင် ▁မှာ ▁? ||| ▁စိတ် မကောင်း ▁ဘူး ||| <eos>
▁ပေး ▁ပါ ▁. ||| : - ▁) ||| <mos>
▁ပါ ▁က ▁? ||| ▁ဖုန်း ▁ကို ▁အရမ်း ||| <eos>
▁နော် ▁- ▁? ||| ▁ဦးကျော် ဟိန်း ▁လည်း ||| <mos>
▁😂 ▁😂 . ||| ▁မေး ▁ထား ▁တာ ||| <eos>
▁ကြောင်း ▁ပေါ့ ▁. ||| ▁အဆင်ပြေ ▁တယ် ▁မြန် ||| <eos>
▁လိုက် ▁တာ ▁! ||| ▁မနေ့ ▁ည ▁က ||| <eos>
▁ပါ ▁ရှင် ▁.... ||| ▁ရောင်းချ ▁တဲ့ ▁ဆိုင် ||| <mos>
▁တယ် ▁နော် ▁... ||| ▁မင်္ဂလာ ▁အပေါင်း ▁နဲ့ ||| <eos>
▁သင့် ▁ဘူး ▁... ||| ▁ဘယ်လို ▁ဆိုးကျိုး ▁ကို ||| <mos>
(base) ye@:~/exp/sentence-seg/ersatz/my-data/model$
```

output ထွက်လာတဲ့ ဖိုင်ကို shuffle လုပ်ခဲ့...  

```
(base) ye@:~/exp/sentence-seg/ersatz/my-data/model$ shuf ./dataset.out > ./dataset.out.shuf
(base) ye@:~/exp/sentence-seg/ersatz/my-data/model$ head ./dataset.out.shuf 
ကြည့် ▁ရင်း ▁... ||| ▁ရင် ▁တွေ ▁ခုန် ||| <mos>
▁လဲ ▁ဟင် ▁? ||| ▁ချစ် ▁တဲ့ ▁သူ ||| <mos>
▁ဩဝါဒ ▁အရ ▁... ||| ▁လူ ▁ဟာ ▁သူ့ ||| <mos>
o o ! ||| ! ! ▁တော် ||| <mos>
▁နှစ် ▁၂ . ||| ၅ ▁သန်း ▁ဝေး ||| <mos>
▁.. ▁ဒါ ▁.. ||| ▁ခိုက လေး ▁က ||| <eos>
▁... ▁ဪ ▁... ||| ▁ခင်ဗျား ▁ကို ▁... ||| <mos>
▁ဆို ▁ရင် ▁... ||| ▁ငါ ▁သေ ▁မှာ ||| <mos>
▁။ ▁ဟင် ... ||| ▁ဘာ ▁လဲ ▁ ||| <mos>
▁နေ ▁သလား ▁... ||| ▁အင်နီ ▁။ ▁ဟုတ်ကဲ့ ||| <mos>
(base) ye@:~/exp/sentence-seg/ersatz/my-data/model$
```

### Preparing Validation Dataset

mypos data ကို download လုပ်ခဲ့...  

```
(base) ye@:~/exp/sentence-seg/ersatz/my-data$ wget https://raw.githubusercontent.com/ye-kyaw-thu/myPOS/master/corpus-ver-3.0/corpus/mypos-ver.3.0.txt
--2021-10-11 12:27:43--  https://raw.githubusercontent.com/ye-kyaw-thu/myPOS/master/corpus-ver-3.0/corpus/mypos-ver.3.0.txt
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.108.133, 185.199.109.133, 185.199.111.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.108.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 9581543 (9.1M) [text/plain]
Saving to: ‘mypos-ver.3.0.txt’

mypos-ver.3.0.txt                     100%[=========================================================================>]   9.14M  17.3MB/s    in 0.5s    

2021-10-11 12:27:47 (17.3 MB/s) - ‘mypos-ver.3.0.txt’ saved [9581543/9581543]
```

mypos (version 3) ဒေတာမှာက pos-tag တွေပါ ပါနေတော့ အဲဒါတွေကို ဖြုတ်ဖို့အတွက် ရေးထားတဲ့ perl script ကို download လုပ်ယူခဲ့...  

```
(base) ye@:~/exp/sentence-seg/ersatz/my-data$ wget https://raw.githubusercontent.com/ye-kyaw-thu/myPOS/master/corpus-draft-ver-1.0/mk-wordtag.pl
--2021-10-11 12:28:23--  https://raw.githubusercontent.com/ye-kyaw-thu/myPOS/master/corpus-draft-ver-1.0/mk-wordtag.pl
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.108.133, 185.199.109.133, 185.199.111.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.108.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3967 (3.9K) [text/plain]
Saving to: ‘mk-wordtag.pl’

mk-wordtag.pl                         100%[=========================================================================>]   3.87K  --.-KB/s    in 0s      

2021-10-11 12:28:23 (120 MB/s) - ‘mk-wordtag.pl’ saved [3967/3967]
```

"word/pos word/pos" ဖြစ်နေတာကနေ "word word" ဖြစ်ဖို့ အောက်ပါအတိုင်း perl script ကို run ခဲ့...  

```
(base) ye@:~/exp/sentence-seg/ersatz/my-data$ perl ./mk-wordtag.pl ./mypos-ver.3.0.txt "\/" w > mypos-ver3.validation-data
```

pos tag ဖြုတ်ထားပြီးသား output validation ဖိုင်ကို check လုပ်ခဲ့။   

```
(base) ye@:~/exp/sentence-seg/ersatz/my-data$ head ./mypos-ver3.validation-data 
ဒီ ဆေး က ၁၀၀ ရာခိုင်နှုန်း ဆေးဘက်ဝင် အပင် များ မှ ဖော်စပ် ထား တာ ဖြစ် တယ် ။
အသစ် ဝယ် ထား တဲ့ ဆွယ်တာ က အသီး ထ နေ ပါ ပေါ့ ။
မ ကျန်းမာ လျှင် နတ် ဆရာ ထံ မေးမြန်း ၍ သက်ဆိုင်ရာ နတ် တို့ အား ပူဇော်ပသ ရ သည် ။
ပေဟိုင် ဥယျာဉ် ။
နဝမ အိပ်မက် ကောသလ မင်း အိပ်မက် ၉ နက်ရှိုင်း ကျယ်ဝန်း သော ရေကန် ကြီး တစ် ခု တွင် သတ္တဝါ တို့ ဆင်း ၍ ရေသောက် ကြ ၏ ။
အပြင်ပန်း ကြည့် ရင် ခက် သလို ထင် ရ ပေမယ့် တကယ့် လက်တွေ့ အခြေအနေ က တော့ အဲဒီ လို မ ဟုတ် ပါ ဘူး ။
8 bit ပုံရိပ် တစ် ခု သည် 256 color သို့မဟုတ် gray scale များ ကို အထောက်အကူ ပြု သည် ။
ကိုရီးယား ဝတ်စုံ မှာ ပန်း ဒီဇိုင်း နဲ့ အဝါရောင် က လိုက်ဖက် လိမ့် မယ် ထင် တယ် ။
သို့နှင့် မဂ္ဂဇင်း မှ တစ်ဆင့် သတင်းစာ ကို ပါ တိုးချဲ့ လိုက် သောအခါ တွင် ဘက်ပတစ် ကျောင်း သို့ မ ပြန် တော့ ဘဲ ထို မဂ္ဂဇင်း ၊ သတင်းစာ နှစ် ခု စလုံး တွင် ပင် တည်းဖြတ် သည့် ဘက် မှ ဆက်လက် လုပ်ကိုင် လေ တော့ သည် ။
တစ် ကျပ်သား ။
(base) ye@:~/exp/sentence-seg/ersatz/my-data$
```

sentencepiece လည်း ပြင်ရမှာမို့ ပြီးတော့ တကယ်က training ရော validation ရော နှစ်မျိုးစလုံးကို cover ဖြစ်ရမှာမို့ sentencepiece ကိုလည်း ပြန်ဆောက်ခဲ့...  
ပထမဆုံး training ဒေတာနဲ့ validation ဒေတာကို ပေါင်းခဲ့...  

```
(base) ye@:~/exp/sentence-seg/ersatz/my-data$ cat ./segmentation-data-updated2.txt ./mypos-ver3.validation-data > train-valid.txt
(base) ye@:~/exp/sentence-seg/ersatz/my-data$ wc ./train-valid.txt 
  256300  5906871 76649248 ./train-valid.txt
(base) ye@:~/exp/sentence-seg/ersatz/my-data$
```

sentencepiece ပြန်ဆောက်ခဲ့...  

```
(base) ye@:~/exp/sentence-seg/ersatz$ time spm_train --input ./my-data/train-valid.txt --model_prefix train-valid-sentencepiece --bos_piece "<mos>" --eos_piece "<eos>"
sentencepiece_trainer.cc(77) LOG(INFO) Starts training with : 
trainer_spec {
  input: ./my-data/train-valid.txt
  input_format: 
  model_prefix: train-valid-sentencepiece
  model_type: UNIGRAM
  vocab_size: 8000
  self_test_sample_size: 0
  character_coverage: 0.9995
  input_sentence_size: 0
  shuffle_input_sentence: 1
  seed_sentencepiece_size: 1000000
  shrinking_factor: 0.75
  max_sentence_length: 4192
  num_threads: 16
  num_sub_iterations: 2
  max_sentencepiece_length: 16
  split_by_unicode_script: 1
  split_by_number: 1
  split_by_whitespace: 1
  split_digits: 0
  treat_whitespace_as_suffix: 0
  required_chars: 
  byte_fallback: 0
  vocabulary_output_piece_score: 1
  train_extremely_large_corpus: 0
  hard_vocab_limit: 1
  use_all_vocab: 0
  unk_id: 0
  bos_id: 1
  eos_id: 2
  pad_id: -1
  unk_piece: <unk>
  bos_piece: <mos>
  eos_piece: <eos>
  pad_piece: <pad>
  unk_surface:  ⁇ 
}
normalizer_spec {
  name: nmt_nfkc
  add_dummy_prefix: 1
  remove_extra_whitespaces: 1
  escape_whitespaces: 1
  normalization_rule_tsv: 
}
denormalizer_spec {}
trainer_interface.cc(319) LOG(INFO) SentenceIterator is not specified. Using MultiFileSentenceIterator.
trainer_interface.cc(174) LOG(INFO) Loading corpus: ./my-data/train-valid.txt
trainer_interface.cc(346) LOG(WARNING) Found too long line (9461 > 4192).
trainer_interface.cc(348) LOG(WARNING) Too long lines are skipped in the training.
trainer_interface.cc(349) LOG(WARNING) The maximum length can be changed with --max_sentence_length=<size> flag.
trainer_interface.cc(375) LOG(INFO) Loaded all 255973 sentences
trainer_interface.cc(381) LOG(INFO) Skipped 327 too long sentences.
trainer_interface.cc(390) LOG(INFO) Adding meta_piece: <unk>
trainer_interface.cc(390) LOG(INFO) Adding meta_piece: <mos>
trainer_interface.cc(390) LOG(INFO) Adding meta_piece: <eos>
trainer_interface.cc(395) LOG(INFO) Normalizing sentences...
trainer_interface.cc(456) LOG(INFO) all chars count=28858856
trainer_interface.cc(467) LOG(INFO) Done: 99.9503% characters are covered.
trainer_interface.cc(477) LOG(INFO) Alphabet size=215
trainer_interface.cc(478) LOG(INFO) Final character coverage=0.999503
trainer_interface.cc(510) LOG(INFO) Done! preprocessed 255972 sentences.
unigram_model_trainer.cc(138) LOG(INFO) Making suffix array...
unigram_model_trainer.cc(142) LOG(INFO) Extracting frequent sub strings...
unigram_model_trainer.cc(193) LOG(INFO) Initialized 195958 seed sentencepieces
trainer_interface.cc(516) LOG(INFO) Tokenizing input sentences with whitespace: 255972
trainer_interface.cc(526) LOG(INFO) Done! 108356
unigram_model_trainer.cc(488) LOG(INFO) Using 108356 sentences for EM training
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=0 size=70288 obj=9.36946 num_tokens=223783 num_tokens/piece=3.1838
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=1 size=53470 obj=7.6401 num_tokens=223447 num_tokens/piece=4.17892
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=0 size=40060 obj=7.59438 num_tokens=230651 num_tokens/piece=5.75764
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=1 size=39899 obj=7.58286 num_tokens=230666 num_tokens/piece=5.78125
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=0 size=29914 obj=7.60065 num_tokens=244527 num_tokens/piece=8.17433
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=1 size=29897 obj=7.59553 num_tokens=244553 num_tokens/piece=8.17985
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=0 size=22419 obj=7.62585 num_tokens=261120 num_tokens/piece=11.6473
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=1 size=22418 obj=7.62121 num_tokens=261131 num_tokens/piece=11.6483
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=0 size=16811 obj=7.66867 num_tokens=279106 num_tokens/piece=16.6026
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=1 size=16808 obj=7.66017 num_tokens=279107 num_tokens/piece=16.6056
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=0 size=12606 obj=7.72713 num_tokens=297311 num_tokens/piece=23.5849
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=1 size=12605 obj=7.71443 num_tokens=297311 num_tokens/piece=23.5868
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=0 size=9452 obj=7.80778 num_tokens=315959 num_tokens/piece=33.4277
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=1 size=9452 obj=7.79042 num_tokens=315961 num_tokens/piece=33.428
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=0 size=8800 obj=7.81591 num_tokens=320511 num_tokens/piece=36.4217
unigram_model_trainer.cc(504) LOG(INFO) EM sub_iter=1 size=8800 obj=7.81119 num_tokens=320511 num_tokens/piece=36.4217
trainer_interface.cc(604) LOG(INFO) Saving model: train-valid-sentencepiece.model
trainer_interface.cc(615) LOG(INFO) Saving vocabs: train-valid-sentencepiece.vocab

real	0m28.399s
user	0m36.936s
sys	0m0.229s
(base) ye@:~/exp/sentence-seg/ersatz$
```

ထွက်လာတဲ့ sentencepiece model နဲ့ vocab ဖိုင်တွေကို စစ်ကြည့်ခဲ့...  

```
(base) ye@:~/exp/sentence-seg/ersatz$ ls train-valid*
train-valid-sentencepiece.model  train-valid-sentencepiece.vocab
(base) ye@:~/exp/sentence-seg/ersatz$ wc train-valid*
 16585  11593 450855 train-valid-sentencepiece.model
  8000  16000 220144 train-valid-sentencepiece.vocab
 24585  27593 670999 total
(base) ye@:~/exp/sentence-seg/ersatz$
```

```
(base) ye@:~/exp/sentence-seg/ersatz$ head ./train-valid-sentencepiece.vocab 
<unk>	0
<mos>	0
<eos>	0
▁။	-3.47204
▁	-3.82072
▁ပါ	-3.82271
▁က	-3.92084
▁ကို	-3.9694
▁တယ်	-4.04095
▁မ	-4.19039
(base) ye@:~/exp/sentence-seg/ersatz$ tail ./train-valid-sentencepiece.vocab 
‘	-16.257
😗	-16.2571
💦	-16.2571
ဪ	-16.2571
😭	-16.2571
💙	-16.8566
😬	-16.8567
😚	-16.8568
၎	-16.8569
ဉ	-16.857
(base) ye@:~/exp/sentence-seg/ersatz$
```

validation data ကိုလည်း သတ်မှတ်ထားတဲ့ format အတိုင်း ရဖို့ ပြင်ဆင်ခဲ့...  

```
(base) ye@:~/exp/sentence-seg/ersatz$ time python ./ersatz/dataset.py --sentencepiece_path ./train-valid-sentencepiece.model  --left-size 3 --right-size 3 --output_path ./my-data/model/validation.out --input_paths ./my-data/mypos-ver3.validation-data

real	0m3.091s
user	0m2.867s
sys	0m0.141s
```

validation နဲ့ ဆိုင်တဲ့ output ဖိုင်ကို စစ်ကြည့်ခဲ့...  

```
(base) ye@:~/exp/sentence-seg/ersatz$ wc ./my-data/model/validation.out 
  291  2619 17991 ./my-data/model/validation.out
(base) ye@:~/exp/sentence-seg/ersatz$ head ./my-data/model/validation.out 
▁အဖေ ▁J . ||| W . M ||| <mos>
. W . ||| M ax w ||| <mos>
▁ ၆၆ . ||| ၇ ▁ ၊ ||| <mos>
▁ ၇၆ . ||| ၇ ▁နှင့် ▁၄၀၀ ||| <mos>
▁ ၈၆ . ||| ၂ ▁% ▁ကိုးကွယ် ||| <mos>
▁ဘာသာ ▁၆ . ||| ၀ ▁% ▁ ||| <mos>
▁ဘာသာ ▁၄ . ||| ၁ ▁% ▁ကိုးကွယ် ||| <mos>
▁ဒေါ်လာ ▁၁ . ||| ၂ ▁သန်း ▁နီးပါး ||| <mos>
▁ပါ ▁ရှင် ▁! ||| ▁၁ ▁နာရီ ▁ထိုး ||| <eos>
▁ခရီးသည် ▁၃ . ||| ၅ ▁သန်း ▁ဝင် ||| <mos>
(base) ye@:~/exp/sentence-seg/ersatz$ tail ./my-data/model/validation.out 
▁နေ ▁၁ . ||| ၄ ▁မီတာ ▁ထိ ||| <mos>
ငွေ ▁၇ . ||| ၅၀ ▁ဒေါ်လာ ▁ပါ ||| <mos>
▁အရပ် ▁၁ . ||| ၄ ▁မီတာ ▁ထက် ||| <mos>
▁ဟာ ▁၁ . ||| ၁ ▁မီတာ ▁ထက် ||| <mos>
ပေါင်း ▁၁၇ . ||| ၉၅ ▁ဒေါ်လာ ▁ပါ ||| <mos>
▁။ ▁N . ||| W . 5 ||| <mos>
▁အရပ် ▁၁ . ||| ၁ ▁မီတာ ▁ထက် ||| <mos>
▁အရပ် ▁၁ . ||| ၁ ▁မီတာ ▁ထက် ||| <mos>
▁က ▁၁ . ||| ၁ ▁မီတာ ▁ထက် ||| <mos>
▁က ▁၁ . ||| ၄ ▁မီတာ ▁ထက် ||| <mos>
(base) ye@:~/exp/sentence-seg/ersatz$
```

### Training

training လုပ်ဖို့အတွက် trainer.py ဖိုင်ကို ဘယ်လို parameter တွေပေး run ရမလဲ ဆိုတာကို --help ခေါ်ကြည့်ခဲ့...  

```
(base) ye@:~/exp/sentence-seg/ersatz$ python ./ersatz/trainer.py --help
usage: trainer.py [-h] [--train_path TRAIN_PATH] [--valid_path VALID_PATH]
                  [--sentencepiece_path SENTENCEPIECE_PATH]
                  [--determiner_type {en,multilingual,all}]
                  [--left_size LEFT_SIZE] [--right_size RIGHT_SIZE]
                  [--batch_size BATCH_SIZE] [--min-epochs MIN_EPOCHS]
                  [--max-epochs MAX_EPOCHS] [--output_path OUTPUT_PATH]
                  [--checkpoint_path CHECKPOINT_PATH] [--lr LR]
                  [--dropout DROPOUT] [--embed_size EMBED_SIZE]
                  [--source_factors] [--factor_embed_size FACTOR_EMBED_SIZE]
                  [--transformer_nlayers TRANSFORMER_NLAYERS]
                  [--linear_nlayers LINEAR_NLAYERS] [--activation_type {tanh}]
                  [--nhead NHEAD] [--log_interval LOG_INTERVAL]
                  [--validation_interval VALIDATION_INTERVAL]
                  [--early_stopping EARLY_STOPPING] [--cpu]
                  [--eos_weight EOS_WEIGHT] [--seed SEED] [--tb_dir TB_DIR]

optional arguments:
  -h, --help            show this help message and exit
  --train_path TRAIN_PATH
  --valid_path VALID_PATH
  --sentencepiece_path SENTENCEPIECE_PATH
  --determiner_type {en,multilingual,all}
  --left_size LEFT_SIZE
  --right_size RIGHT_SIZE
  --batch_size BATCH_SIZE
  --min-epochs MIN_EPOCHS
  --max-epochs MAX_EPOCHS
  --output_path OUTPUT_PATH
  --checkpoint_path CHECKPOINT_PATH
  --lr LR
  --dropout DROPOUT
  --embed_size EMBED_SIZE
  --source_factors
  --factor_embed_size FACTOR_EMBED_SIZE
  --transformer_nlayers TRANSFORMER_NLAYERS
  --linear_nlayers LINEAR_NLAYERS
  --activation_type {tanh}
  --nhead NHEAD
  --log_interval LOG_INTERVAL
  --validation_interval VALIDATION_INTERVAL
  --early_stopping EARLY_STOPPING
  --cpu
  --eos_weight EOS_WEIGHT
  --seed SEED
  --tb_dir TB_DIR
(base) ye@:~/exp/sentence-seg/ersatz$ 
```

Example အနေနဲ့ training ဒါမျိုး command နဲ့ လုပ်တယ်ဆိုတဲ့ command ကတကယ် အကြမ်းပဲ ပြထားတာမို့... အသေးစိတ်သိနိုင်ဖို့ trainer.py ဖိုင်ကို ဝင်ကြည့်ဖို့လိုအပ်တယ်။  
အောက်ပါ setting နဲ့ training လုပ်ခဲ့...  

```
time python /home/ye/exp/sentence-seg/ersatz/ersatz/trainer.py \
        --sentencepiece_path=/home/ye/exp/sentence-seg/ersatz/train-valid-sentencepiece.vocab \
        --left_size=3 \
        --right_size=3 \
        --output_path=/home/ye/exp/sentence-seg/ersatz/my-data/model/ \
        --transformer_nlayers=2 \
        --activation_type=tanh \
        --linear_nlayers=0 \
        --min-epochs=25 \
        --max-epochs=100 \
        --lr=0.0001 \
        --dropout=0.1 \
        --embed_size=256 \
        --factor_embed_size=8 \
        --source_factors \
        --nhead=8 \
        --log_interval=1000 \
        --validation_interval=25000 \
        --eos_weight=1.0 \
        --early_stopping=25 \
        --train_path /home/ye/exp/sentence-seg/ersatz/my-data/dataset.out.shuf \
        --valid_path /home/ye/exp/sentence-seg/ersatz/my-data/validation.out
```

training လုပ်ကြည့်တော့ အောက်ပါအတိုင်း error ပေးတယ်...  

```
(base) ye@:~/exp/sentence-seg/ersatz$ time python /home/ye/exp/sentence-seg/ersatz/ersatz/trainer.py \
>         --sentencepiece_path=/home/ye/exp/sentence-seg/ersatz/train-valid-sentencepiece.vocab \
>         --left_size=3 \
>         --right_size=3 \
>         --output_path=/home/ye/exp/sentence-seg/ersatz/my-data/model/ \
>         --transformer_nlayers=2 \
>         --activation_type=tanh \
>         --linear_nlayers=0 \
>         --min-epochs=25 \
>         --max-epochs=100 \
>         --lr=0.0001 \
>         --dropout=0.1 \
>         --embed_size=256 \
>         --factor_embed_size=8 \
>         --source_factors \
>         --nhead=8 \
>         --log_interval=1000 \
>         --validation_interval=25000 \
>         --eos_weight=1.0 \
>         --early_stopping=25 \
>         --train_path /home/ye/exp/sentence-seg/ersatz/my-data/dataset.out.shuf \
>         --valid_path /home/ye/exp/sentence-seg/ersatz/my-data/validation.out
Starting trainer...
Traceback (most recent call last):
  File "/home/ye/exp/sentence-seg/ersatz/ersatz/trainer.py", line 100, in <module>
    main()
  File "/home/ye/exp/sentence-seg/ersatz/ersatz/trainer.py", line 72, in main
    trainer = ErsatzTrainer(args)
NameError: name 'ErsatzTrainer' is not defined

real	0m0.427s
user	0m0.347s
sys	0m0.028s
(base) ye@:~/exp/sentence-seg/ersatz$
```

main() ကို call လုပ်ထားတဲ့ အပိုင်းကို trainer.py ဖိုင်ရဲ့ အောက်ဆုံးကို ရွှေ့ခဲ့...  

```python
if __name__ == '__main__':
    main()
```

ထပ် run ကြည့်ခဲ့...  

```
(base) ye@:~/exp/sentence-seg/ersatz$ time python /home/ye/exp/sentence-seg/ersatz/ersatz/trainer.py         --sentencepiece_path=/home/ye/exp/sentence-seg/ersatz/train-valid-sentencepiece.vocab         --left_size=3         --right_size=3         --output_path=/home/ye/exp/sentence-seg/ersatz/my-data/model/         --transformer_nlayers=2         --activation_type=tanh         --linear_nlayers=0         --min-epochs=25         --max-epochs=100         --lr=0.0001         --dropout=0.1         --embed_size=256         --factor_embed_size=8         --source_factors         --nhead=8         --log_interval=1000         --validation_interval=25000         --eos_weight=1.0         --early_stopping=25         --train_path /home/ye/exp/sentence-seg/ersatz/my-data/dataset.out.shuf         --valid_path /home/ye/exp/sentence-seg/ersatz/my-data/validation.out
Starting trainer...
Traceback (most recent call last):
  File "/home/ye/exp/sentence-seg/ersatz/ersatz/trainer.py", line 413, in <module>
    main()
  File "/home/ye/exp/sentence-seg/ersatz/ersatz/trainer.py", line 72, in main
    trainer = ErsatzTrainer(args)
  File "/home/ye/exp/sentence-seg/ersatz/ersatz/trainer.py", line 209, in __init__
    right_context_size=args.right_size)
  File "/home/ye/exp/sentence-seg/ersatz/ersatz/dataset.py", line 166, in __init__
    self.tokenizer = SentencePiece(model_path=sentencepiece_path)
  File "/home/ye/exp/sentence-seg/ersatz/ersatz/subword.py", line 91, in __init__
    self.model.Load(model_path)
  File "/home/ye/anaconda3/lib/python3.7/site-packages/sentencepiece-0.1.95-py3.7-linux-x86_64.egg/sentencepiece/__init__.py", line 367, in Load
    return self.LoadFromFile(model_file)
  File "/home/ye/anaconda3/lib/python3.7/site-packages/sentencepiece-0.1.95-py3.7-linux-x86_64.egg/sentencepiece/__init__.py", line 171, in LoadFromFile
    return _sentencepiece.SentencePieceProcessor_LoadFromFile(self, arg)
RuntimeError: Internal: /sentencepiece/python/bundled/sentencepiece/src/sentencepiece_processor.cc(848) [model_proto->ParseFromArray(serialized.data(), serialized.size())] 

real	0m0.456s
user	0m0.336s
sys	0m0.057s
(base) ye@:~/exp/sentence-seg/ersatz$
```

Ref: https://github.com/google/sentencepiece/issues/296  
Sentencepiece နဲ့ ပတ်သက်တဲ့ error ဆိုတာတော့ သိတယ်။ အထက်ပါ reference link ကို ဖတ်ကြည့်ခဲ့...  

command line argument တွေကို အောက်ပါအတိုင်း update လုပ်ခဲ့...  

```
time python /home/ye/exp/sentence-seg/ersatz/ersatz/trainer.py \
--sentencepiece_path=/home/ye/exp/sentence-seg/ersatz/train-valid-sentencepiece.model  \
--left_size=3  \
--right_size=3  \
--output_path=/home/ye/exp/sentence-seg/ersatz/my-data/model/ \
--transformer_nlayers=2 \
--activation_type=tanh \
--linear_nlayers=0   \
--min-epochs=25 \
--max-epochs=100 \
--lr=0.0001 \
--dropout=0.1  \
--embed_size=256 \
--factor_embed_size=8 \
--source_factors \
--nhead=8 \
--log_interval=1000 \
--validation_interval=25000 \
--eos_weight=1.0 \
--early_stopping=25 \
--train_path /home/ye/exp/sentence-seg/ersatz/my-data/model/dataset.out.shuf \
--valid_path /home/ye/exp/sentence-seg/ersatz/my-data/model/validation.out
```

အောက်ပါအတိုင်း Error ရခဲ့...  

```
(base) ye@:~/exp/sentence-seg/ersatz$ time python /home/ye/exp/sentence-seg/ersatz/ersatz/trainer.py \
> --sentencepiece_path=/home/ye/exp/sentence-seg/ersatz/train-valid-sentencepiece.model  \
> --left_size=3  \
> --right_size=3  \
> --output_path=/home/ye/exp/sentence-seg/ersatz/my-data/model/ \
> --transformer_nlayers=2 \
> --activation_type=tanh \
> --linear_nlayers=0   \
> --min-epochs=25 \
> --max-epochs=100 \
> --lr=0.0001 \
> --dropout=0.1  \
> --embed_size=256 \
> --factor_embed_size=8 \
> --source_factors \
> --nhead=8 \
> --log_interval=1000 \
> --validation_interval=25000 \
> --eos_weight=1.0 \
> --early_stopping=25 \
> --train_path /home/ye/exp/sentence-seg/ersatz/my-data/model/dataset.out.shuf \
> --valid_path /home/ye/exp/sentence-seg/ersatz/my-data/model/validation.out
Starting trainer...
cuda:0
Training with: 4780322
Using 2 GPUSs for ET
DataParallel(
  (module): ErsatzTransformer(
    (fact_emb): Embedding(6, 8)
    (encoder): TransformerEncoder(
      (layers): ModuleList(
        (0): TransformerEncoderLayer(
          (self_attn): MultiheadAttention(
            (out_proj): _LinearWithBias(in_features=264, out_features=264, bias=True)
          )
          (linear1): Linear(in_features=264, out_features=2048, bias=True)
          (dropout): Dropout(p=0.1, inplace=False)
          (linear2): Linear(in_features=2048, out_features=264, bias=True)
          (norm1): LayerNorm((264,), eps=1e-05, elementwise_affine=True)
          (norm2): LayerNorm((264,), eps=1e-05, elementwise_affine=True)
          (dropout1): Dropout(p=0.1, inplace=False)
          (dropout2): Dropout(p=0.1, inplace=False)
        )
        (1): TransformerEncoderLayer(
          (self_attn): MultiheadAttention(
            (out_proj): _LinearWithBias(in_features=264, out_features=264, bias=True)
          )
          (linear1): Linear(in_features=264, out_features=2048, bias=True)
          (dropout): Dropout(p=0.1, inplace=False)
          (linear2): Linear(in_features=2048, out_features=264, bias=True)
          (norm1): LayerNorm((264,), eps=1e-05, elementwise_affine=True)
          (norm2): LayerNorm((264,), eps=1e-05, elementwise_affine=True)
          (dropout1): Dropout(p=0.1, inplace=False)
          (dropout2): Dropout(p=0.1, inplace=False)
        )
      )
    )
    (pos_embed): PositionalEncoding(
      (dropout): Dropout(p=0.1, inplace=False)
    )
    (src_emb): Embedding(8000, 256)
    (embed_dropout): Dropout(p=0.1, inplace=False)
    (generator): Generator(
      (proj): Linear(in_features=1584, out_features=2, bias=True)
    )
  )
)
Namespace(activation_type='tanh', batch_size=256, checkpoint_path=None, cpu=False, determiner_type='multilingual', dropout=0.1, early_stopping=25, embed_size=256, eos_weight=1.0, factor_embed_size=8, left_size=3, linear_nlayers=0, log_interval=1000, lr=0.0001, max_epochs=100, min_epochs=25, nhead=8, output_path='/home/ye/exp/sentence-seg/ersatz/my-data/model/', right_size=3, seed=14, sentencepiece_path='/home/ye/exp/sentence-seg/ersatz/train-valid-sentencepiece.model', source_factors=True, tb_dir=None, train_path='/home/ye/exp/sentence-seg/ersatz/my-data/model/dataset.out.shuf', transformer_nlayers=2, valid_path='/home/ye/exp/sentence-seg/ersatz/my-data/model/validation.out', validation_interval=25000)
{"type": "TRAINING", "update_num": 0, "prec": 0.15862068965517243, "recall": 0.6216216216216216, "acc": 0.46875, "f1": 0.2527472527472528, "lr": 0.0001, "total_loss": 0.7809608578681946, "average_loss": 0.003050628351047635, "ppl_per_pred": 0.008529567159712315, "time_since_last_update": 1.2554638385772705, "predictions_per_second": 203.908700620248, "time_passed": 1.2554645538330078, "correct_eos": 23, "correct_mos": 97, "num_pred_eos": 145, "num_obs_eos": 37, "validations": 0, "num_pred": 256}
Traceback (most recent call last):
  File "/home/ye/exp/sentence-seg/ersatz/ersatz/trainer.py", line 413, in <module>
    main()
  File "/home/ye/exp/sentence-seg/ersatz/ersatz/trainer.py", line 93, in main
    determiner=determiner)
  File "/home/ye/exp/sentence-seg/ersatz/ersatz/trainer.py", line 368, in run_epoch
    stats = self.validate(batch_size, determiner, use_factors=use_factors)
  File "/home/ye/exp/sentence-seg/ersatz/ersatz/trainer.py", line 289, in validate
    left_context = self.model.tokenizer.merge(context_item[0])
  File "/home/ye/anaconda3/lib/python3.7/site-packages/torch/nn/modules/module.py", line 772, in __getattr__
    type(self).__name__, name))
torch.nn.modules.module.ModuleAttributeError: 'DataParallel' object has no attribute 'tokenizer'

real	0m3.139s
user	0m2.573s
sys	0m1.226s
(base) ye@:~/exp/sentence-seg/ersatz$
```

--cpu option နဲ့ပဲ run ကြည့်တော့ ရတယ်။  

```
(base) ye@:~/exp/sentence-seg/ersatz$ time python /home/ye/exp/sentence-seg/ersatz/ersatz/trainer.py --sentencepiece_path=/home/ye/exp/sentence-seg/ersatz/train-valid-sentencepiece.model  --left_size=3  --right_size=3  --output_path=/home/ye/exp/sentence-seg/ersatz/my-data/model/ --transformer_nlayers=2 --activation_type=tanh --linear_nlayers=0   --min-epochs=25 --max-epochs=100 --lr=0.0001 --dropout=0.1  --embed_size=256 --factor_embed_size=8 --source_factors --nhead=8 --log_interval=1000 --validation_interval=25000 --eos_weight=1.0 --early_stopping=25 --train_path /home/ye/exp/sentence-seg/ersatz/my-data/model/dataset.out.shuf --valid_path /home/ye/exp/sentence-seg/ersatz/my-data/model/validation.out --cpu
Starting trainer...
cpu
Training with: 4780322
ErsatzTransformer(
  (fact_emb): Embedding(6, 8)
  (encoder): TransformerEncoder(
    (layers): ModuleList(
      (0): TransformerEncoderLayer(
        (self_attn): MultiheadAttention(
          (out_proj): _LinearWithBias(in_features=264, out_features=264, bias=True)
        )
        (linear1): Linear(in_features=264, out_features=2048, bias=True)
        (dropout): Dropout(p=0.1, inplace=False)
        (linear2): Linear(in_features=2048, out_features=264, bias=True)
        (norm1): LayerNorm((264,), eps=1e-05, elementwise_affine=True)
        (norm2): LayerNorm((264,), eps=1e-05, elementwise_affine=True)
        (dropout1): Dropout(p=0.1, inplace=False)
        (dropout2): Dropout(p=0.1, inplace=False)
      )
      (1): TransformerEncoderLayer(
        (self_attn): MultiheadAttention(
          (out_proj): _LinearWithBias(in_features=264, out_features=264, bias=True)
        )
        (linear1): Linear(in_features=264, out_features=2048, bias=True)
        (dropout): Dropout(p=0.1, inplace=False)
        (linear2): Linear(in_features=2048, out_features=264, bias=True)
        (norm1): LayerNorm((264,), eps=1e-05, elementwise_affine=True)
        (norm2): LayerNorm((264,), eps=1e-05, elementwise_affine=True)
        (dropout1): Dropout(p=0.1, inplace=False)
        (dropout2): Dropout(p=0.1, inplace=False)
      )
    )
  )
  (pos_embed): PositionalEncoding(
    (dropout): Dropout(p=0.1, inplace=False)
  )
  (src_emb): Embedding(8000, 256)
  (embed_dropout): Dropout(p=0.1, inplace=False)
  (generator): Generator(
    (proj): Linear(in_features=1584, out_features=2, bias=True)
  )
)
Namespace(activation_type='tanh', batch_size=256, checkpoint_path=None, cpu=True, determiner_type='multilingual', dropout=0.1, early_stopping=25, embed_size=256, eos_weight=1.0, factor_embed_size=8, left_size=3, linear_nlayers=0, log_interval=1000, lr=0.0001, max_epochs=100, min_epochs=25, nhead=8, output_path='/home/ye/exp/sentence-seg/ersatz/my-data/model/', right_size=3, seed=14, sentencepiece_path='/home/ye/exp/sentence-seg/ersatz/train-valid-sentencepiece.model', source_factors=True, tb_dir=None, train_path='/home/ye/exp/sentence-seg/ersatz/my-data/model/dataset.out.shuf', transformer_nlayers=2, valid_path='/home/ye/exp/sentence-seg/ersatz/my-data/model/validation.out', validation_interval=25000)
{"type": "TRAINING", "update_num": 0, "prec": 0.16447368421052633, "recall": 0.6756756756756757, "acc": 0.45703125, "f1": 0.2645502645502646, "lr": 0.0001, "total_loss": 0.7893432974815369, "average_loss": 0.0030833722557872534, "ppl_per_pred": 0.00860136654227972, "time_since_last_update": 0.21313953399658203, "predictions_per_second": 1201.0911124733213, "time_passed": 0.21314048767089844, "correct_eos": 25, "correct_mos": 92, "num_pred_eos": 152, "num_obs_eos": 37, "validations": 0, "num_pred": 256}
{"num_obs_eos": 7, "num_pred_eos": 26, "correct_eos": 1, "correct_mos": 259, "total_loss": 0.8075444102287292, "ppl": 2.9950203895568848, "num_pred": 291, "inference_correct_eos": 1, "inference_incorrect_eos": 6, "inference_correct_mos": 259, "inference_incorrect_mos": 25, "average_loss": 0.002775066701816939, "ppl_per_pred": 0.01029216628713706, "inference_prec": 0.038461538461538464, "inference_recall": 0.14285714285714285, "inference_f1": 0.060606060606060615, "inference_acc": 0.8934707903780069, "type": "VALIDATION", "acc": 0.8934707903780069, "prec": 0.038461538461538464, "recall": 0.14285714285714285, "f1": 0.060606060606060615}
SAVING MODEL: {"num_obs_eos": 7, "num_pred_eos": 26, "correct_eos": 1, "correct_mos": 259, "total_loss": 0.8075444102287292, "ppl": 2.9950203895568848, "num_pred": 291, "inference_correct_eos": 1, "inference_incorrect_eos": 6, "inference_correct_mos": 259, "inference_incorrect_mos": 25, "average_loss": 0.002775066701816939, "ppl_per_pred": 0.01029216628713706, "inference_prec": 0.038461538461538464, "inference_recall": 0.14285714285714285, "inference_f1": 0.060606060606060615, "inference_acc": 0.8934707903780069, "type": "VALIDATION", "acc": 0.8934707903780069, "prec": 0.038461538461538464, "recall": 0.14285714285714285, "f1": 0.060606060606060615}
SAVING MODEL: End of epoch 0
SAVING MODEL: End of epoch 1
SAVING MODEL: End of epoch 2
SAVING MODEL: End of epoch 3
SAVING MODEL: End of epoch 4
SAVING MODEL: End of epoch 5
SAVING MODEL: End of epoch 6
SAVING MODEL: End of epoch 7
SAVING MODEL: End of epoch 8
SAVING MODEL: End of epoch 9
SAVING MODEL: End of epoch 10
SAVING MODEL: End of epoch 11
SAVING MODEL: End of epoch 12
{"type": "TRAINING", "update_num": 1, "prec": 0.735791848822451, "recall": 0.3442644584474283, "acc": 0.9065312953781994, "f1": 0.4690625491650372, "lr": 5.133420832795048e-05, "total_loss": 227.69105940160807, "average_loss": 0.0009009011715799747, "ppl_per_pred": 0.0049782181140642446, "time_since_last_update": 203.44786977767944, "predictions_per_second": 1242.2690897485531, "time_passed": 203.66192054748535, "correct_eos": 10435, "correct_mos": 218679, "num_pred_eos": 14182, "num_obs_eos": 30311, "validations": 1, "num_pred": 252737}
SAVING MODEL: End of epoch 13
SAVING MODEL: End of epoch 14
SAVING MODEL: End of epoch 15
SAVING MODEL: End of epoch 16
SAVING MODEL: End of epoch 17
SAVING MODEL: End of epoch 18
SAVING MODEL: End of epoch 19
SAVING MODEL: End of epoch 20
SAVING MODEL: End of epoch 21
SAVING MODEL: End of epoch 22
SAVING MODEL: End of epoch 23
SAVING MODEL: End of epoch 24
SAVING MODEL: End of epoch 25
SAVING MODEL: End of epoch 26
{"type": "TRAINING", "update_num": 2, "prec": 0.8645922659153089, "recall": 0.7002116542099345, "acc": 0.9509636177847485, "f1": 0.7737679755879181, "lr": 2.5034408974245492e-05, "total_loss": 123.45839448920742, "average_loss": 0.00048897124786803, "ppl_per_pred": 0.004484550061960205, "time_since_last_update": 197.5932583808899, "predictions_per_second": 1277.806753473827, "time_passed": 401.2557101249695, "correct_eos": 21173, "correct_mos": 218932, "num_pred_eos": 24489, "num_obs_eos": 30238, "validations": 1, "num_pred": 252486}
SAVING MODEL: End of epoch 27
SAVING MODEL: End of epoch 28
SAVING MODEL: End of epoch 29
SAVING MODEL: End of epoch 30
SAVING MODEL: End of epoch 31
SAVING MODEL: End of epoch 32
SAVING MODEL: End of epoch 33
SAVING MODEL: End of epoch 34
SAVING MODEL: End of epoch 35
SAVING MODEL: End of epoch 36
SAVING MODEL: End of epoch 37
SAVING MODEL: End of epoch 38
SAVING MODEL: End of epoch 39
{"type": "TRAINING", "update_num": 3, "prec": 0.9178402910348306, "recall": 0.8407681140292992, "acc": 0.9718798593003795, "f1": 0.8776153329544867, "lr": 1.2851215656510312e-05, "total_loss": 76.06256667077287, "average_loss": 0.0003009554068884764, "ppl_per_pred": 0.004271032437240253, "time_since_last_update": 198.81293416023254, "predictions_per_second": 1271.2301695437359, "time_passed": 600.069611787796, "correct_eos": 25482, "correct_mos": 220148, "num_pred_eos": 27763, "num_obs_eos": 30308, "validations": 1, "num_pred": 252737}
SAVING MODEL: End of epoch 40
SAVING MODEL: End of epoch 41
SAVING MODEL: End of epoch 42
SAVING MODEL: End of epoch 43
SAVING MODEL: End of epoch 44
SAVING MODEL: End of epoch 45
SAVING MODEL: End of epoch 46
SAVING MODEL: End of epoch 47
SAVING MODEL: End of epoch 48
SAVING MODEL: End of epoch 49
SAVING MODEL: End of epoch 50
SAVING MODEL: End of epoch 51
SAVING MODEL: End of epoch 52
SAVING MODEL: End of epoch 53
{"type": "TRAINING", "update_num": 4, "prec": 0.9412898703119523, "recall": 0.8882677868554228, "acc": 0.979987009180707, "f1": 0.9140105168218097, "lr": 6.267216326897833e-06, "total_loss": 56.7133055922709, "average_loss": 0.00022461960501679658, "ppl_per_pred": 0.004192749144113263, "time_since_last_update": 198.6365065574646, "predictions_per_second": 1271.0956529380817, "time_passed": 798.7070555686951, "correct_eos": 26855, "correct_mos": 220578, "num_pred_eos": 28530, "num_obs_eos": 30233, "validations": 1, "num_pred": 252486}
SAVING MODEL: End of epoch 54
SAVING MODEL: End of epoch 55
SAVING MODEL: End of epoch 56
SAVING MODEL: End of epoch 57
SAVING MODEL: End of epoch 58
SAVING MODEL: End of epoch 59
SAVING MODEL: End of epoch 60
SAVING MODEL: End of epoch 61
SAVING MODEL: End of epoch 62
SAVING MODEL: End of epoch 63
SAVING MODEL: End of epoch 64
SAVING MODEL: End of epoch 65
SAVING MODEL: End of epoch 66
{"type": "TRAINING", "update_num": 5, "prec": 0.9467798716090288, "recall": 0.9046001648804617, "acc": 0.9824521142531565, "f1": 0.9252095313580331, "lr": 3.2172258856130596e-06, "total_loss": 49.61838071345255, "average_loss": 0.00019632416588569364, "ppl_per_pred": 0.004158772665752739, "time_since_last_update": 201.37443590164185, "predictions_per_second": 1255.0600023701388, "time_passed": 1000.0826570987701, "correct_eos": 27432, "correct_mos": 220870, "num_pred_eos": 28974, "num_obs_eos": 30325, "validations": 1, "num_pred": 252737}
SAVING MODEL: End of epoch 67
SAVING MODEL: End of epoch 68
SAVING MODEL: End of epoch 69
SAVING MODEL: End of epoch 70
SAVING MODEL: End of epoch 71
SAVING MODEL: End of epoch 72
SAVING MODEL: End of epoch 73
SAVING MODEL: End of epoch 74
SAVING MODEL: End of epoch 75
SAVING MODEL: End of epoch 76
SAVING MODEL: End of epoch 77
SAVING MODEL: End of epoch 78
SAVING MODEL: End of epoch 79
SAVING MODEL: End of epoch 80
{"type": "TRAINING", "update_num": 6, "prec": 0.9506432587176215, "recall": 0.9123469049983449, "acc": 0.9838446488122113, "f1": 0.9311014644528148, "lr": 1.5689605665762901e-06, "total_loss": 45.94255206669641, "average_loss": 0.0001819607901693417, "ppl_per_pred": 0.004147615054591146, "time_since_last_update": 211.8176507949829, "predictions_per_second": 1191.996979724696, "time_passed": 1211.9008955955505, "correct_eos": 27562, "correct_mos": 220845, "num_pred_eos": 28993, "num_obs_eos": 30210, "validations": 1, "num_pred": 252486}
SAVING MODEL: End of epoch 81
SAVING MODEL: End of epoch 82
SAVING MODEL: End of epoch 83
SAVING MODEL: End of epoch 84
SAVING MODEL: End of epoch 85
SAVING MODEL: End of epoch 86
SAVING MODEL: End of epoch 87
SAVING MODEL: End of epoch 88
SAVING MODEL: End of epoch 89
SAVING MODEL: End of epoch 90
SAVING MODEL: End of epoch 91
SAVING MODEL: End of epoch 92
SAVING MODEL: End of epoch 93
{"type": "TRAINING", "update_num": 7, "prec": 0.95255562030784, "recall": 0.9159744198312236, "acc": 0.9844383687390449, "f1": 0.933906935318534, "lr": 8.054134858296649e-07, "total_loss": 44.246400838966, "average_loss": 0.00017506894850760274, "ppl_per_pred": 0.004136426016854199, "time_since_last_update": 210.94285202026367, "predictions_per_second": 1198.1301929857357, "time_passed": 1422.8446853160858, "correct_eos": 27787, "correct_mos": 221017, "num_pred_eos": 29171, "num_obs_eos": 30336, "validations": 1, "num_pred": 252737}
SAVING MODEL: End of epoch 94
SAVING MODEL: End of epoch 95
SAVING MODEL: End of epoch 96
SAVING MODEL: End of epoch 97
SAVING MODEL: End of epoch 98
SAVING MODEL: End of epoch 99

real	25m2.066s
user	190m9.729s
sys	1m27.408s
```

### Thinking ...

မော်ဒယ်က ကို ersatx ရဲ့ site မှာ ပြထားတဲ့အတိုင်း training လုပ်ခဲ့တယ်။ မြန်မာစာ ဒေတာနဲ့ ပြောင်းသုံးပြီး လုပ်ခဲ့တယ်။  
အဆင်ပြေတယ်။ သို့သော် မြန်မာစာအတွက် segmentation က ဒီအတိုင်း သွားလို့ မရဘူး။ training data, validation data, test data ကို ကိုယ်ဖာသာကိုယ် script ရေးပြီး ပြင်ဆင်ရလိမ့်မယ်။  

ဘာဖြစ်လို့လဲ ဆိုရင် သူ့ preprocessing အတိုင်း သွားရင် အင်္ဂလိပ်စာကို အကြေခံပြီးသွားတာကြောင့် အောက်ပါလို ပုံစံမျိုး ဖြစ်နေတာကို တွေ့ရလိမ့်မယ်။   

```
(base) ye@:~/exp/sentence-seg/ersatz/my-data/model$ head validation.out 
▁အဖေ ▁J . ||| W . M ||| <mos>
. W . ||| M ax w ||| <mos>
▁ ၆၆ . ||| ၇ ▁ ၊ ||| <mos>
▁ ၇၆ . ||| ၇ ▁နှင့် ▁၄၀၀ ||| <mos>
▁ ၈၆ . ||| ၂ ▁% ▁ကိုးကွယ် ||| <mos>
▁ဘာသာ ▁၆ . ||| ၀ ▁% ▁ ||| <mos>
▁ဘာသာ ▁၄ . ||| ၁ ▁% ▁ကိုးကွယ် ||| <mos>
▁ဒေါ်လာ ▁၁ . ||| ၂ ▁သန်း ▁နီးပါး ||| <mos>
▁ပါ ▁ရှင် ▁! ||| ▁၁ ▁နာရီ ▁ထိုး ||| <eos>
▁ခရီးသည် ▁၃ . ||| ၅ ▁သန်း ▁ဝင် ||| <mos>
(base) ye@:~/exp/sentence-seg/ersatz/my-data/model$ tail validation.out 
▁နေ ▁၁ . ||| ၄ ▁မီတာ ▁ထိ ||| <mos>
ငွေ ▁၇ . ||| ၅၀ ▁ဒေါ်လာ ▁ပါ ||| <mos>
▁အရပ် ▁၁ . ||| ၄ ▁မီတာ ▁ထက် ||| <mos>
▁ဟာ ▁၁ . ||| ၁ ▁မီတာ ▁ထက် ||| <mos>
ပေါင်း ▁၁၇ . ||| ၉၅ ▁ဒေါ်လာ ▁ပါ ||| <mos>
▁။ ▁N . ||| W . 5 ||| <mos>
▁အရပ် ▁၁ . ||| ၁ ▁မီတာ ▁ထက် ||| <mos>
▁အရပ် ▁၁ . ||| ၁ ▁မီတာ ▁ထက် ||| <mos>
▁က ▁၁ . ||| ၁ ▁မီတာ ▁ထက် ||| <mos>
▁က ▁၁ . ||| ၄ ▁မီတာ ▁ထက် ||| <mos>

```

ဆိုလိုတာက အောက်ပါ အဆင့်ကို ကိုယ့်ဖာသာကိုယ် လုပ်ယူရလိမ့်မယ့်...  

```
time python ./ersatz/dataset.py --sentencepiece_path ./ersatz.model  --left-size 3 --right-size 3 --output_path ./my-data/model/dataset.out --input_paths ./my-data/segmentation-data-updated2.txt 
```

dataset.py ရဲ့ တချို့ အရေးကြီးတဲ့ အပိုင်းတွေ...  

```python
                # potentially add a marker for truncated words in left context
                if len(word) > 0:
                    untok = ''.join(word).replace('\u2581', '')
                    if untok.istitle():
                        out = [self.codes['TITLE'] for w in word]
                    elif untok.isupper():
                        out = [self.codes['CAP'] for w in word]
                    elif untok.islower():
                        out = [self.codes['LOWER'] for w in word]
                    elif untok in string.punctuation:
                        out = [self.codes['PUNC'] for w in word]
                    else:
                        for w in untok:
                            if w in string.digits:
                                out = [self.codes['NUMBER'] for w in word]
                                break
                        if not out:
                            out = [self.codes['UNMARK'] for w in word]
                    output_stream += out
                word = []
```

## Data Preparation by Myself

sentencepiece ကို သုံးပြီး segmentation ဖြတ်တာကို အရင် လုပ်ရမယ်..  

```
(base) ye@:~/exp/sentence-seg/ersatz/my-data$ cat ./segmentation-data-updated2.txt | spm_encode --model ../ersatz.model > ./segmentation-data-updated2.txt.sentencepiece
(base) ye@:~/exp/sentence-seg/ersatz/my-data$ head ./segmentation-data-updated2.txt.sentencepiece 
▁လု ▁သာ ▁မောင်း ▁ပြိုင် ▁သာ ▁ပြိုင် ▁ကိုယ့် ▁ကိုယ်ပိုင် ▁ကား ▁မ ▁ဟုတ် ▁ပြဿနာ ▁ဖြစ် ▁ရင် ▁ထွက် ▁ပြေး ▁အေးအေးဆေးဆေး ▁ဖြစ် ▁သွား ▁ရင် ▁ပြန် ▁မောင်း ▁လု ▁သာ ▁မောင်း ▁။
▁သမ္မတ ▁ဦးထင်ကျော်
▁အင်းလေး ▁သူ ▁ဆို ▁လည်း ▁ကောင်း ▁တာ ▁ပဲ ▁ ၊ ▁ကစ်ကစ် ▁က ▁ဖြူဖြူ ▁ဖွေးဖွေး လေး ▁ဆို ▁တော့ ▁ ၊ ▁ရှမ်း မလေး ▁တွေ ▁တော့ ▁ထိုင် ▁ငို ▁နေ ▁တော့ ▁မှာ ▁ပဲ ▁အင်းလေး ▁ကို ▁အရမ်း ▁ချစ် ▁တယ် ▁အင်းလေး ▁နဲ့ ▁ကစ် ▁နဲ့ ▁လိုက် ▁ပါ ▁တယ် ▁တသက် လုံး ▁တကယ် ▁လာ ▁နေ ▁ရင် ▁အရမ်း ▁ကောင်း ▁မှာ ▁ပဲ ▁ချစ် ▁တယ် ▁မကစ် ▁ဇင် ဇင် ▁တို့ ▁မွန် ▁ပြည်နယ် ▁လာ လည် ▁ပါ ▁လား ▁ဖိတ် ခေါ် ▁ပါ ▁တယ် ▁ကျိုက် ထီးရိုး ▁ဘုရား ▁ဖူး ▁ရင် ▁မော်လ မြိုင် ▁မြို့ ▁ကို ▁လာ လည် ▁ပါ ▁ရှမ်း ▁က ▁မဲ ▁တာ ▁လား ▁အင်း သူ မ ▁က ▁မဲ ▁တာ ▁လား ▁မူ ကြို ▁ကလေး ▁မေး ▁တောင် ▁သိ ▁တယ် ▁အင်း သူ မ ▁က ▁ဘယ် လောက် ▁ပဲ ▁ပိုက်ဆံ ▁ရှိ ▁ပါစေ ▁အလောင်း စည်သူ မင်း ▁ကျိန်စာ ▁တိုက် ▁ခဲ့ ▁လို့ ▁ရေ ▁ခြံ ▁ရော ▁ကုန်း ▁ခြံ ▁ရော ▁ကုန်း ▁နေ ▁အောင် ▁လုပ် ▁ရ ▁တာ ▁ဖြူ ▁နေ ▁ဦး ▁မယ် ▁အသား ▁က ▁ကြည့် ▁ပြော ▁အင်း သူ မ ▁လုပ် ▁ရင် ▁ရေ ▁ကူး ▁တတ် ▁ရ ▁မယ် ▁နော် ▁ရေ ▁မ ▁ကူး ▁တတ် ▁ရင် ▁အလောင်း ▁တွေ ▁ခု ▁ချိန် ▁ထိ ▁ဆယ် ▁မ ▁ကုန် ▁သေး ▁ဘူး ▁အသဲ ▁😍 ▁😍 ▁😍 ▁😍 ▁မမ ▁ကစ် ▁ချစ် ▁လိုက် ▁တာ ▁ကောင်း ▁တယ် ▁လုပ် ▁ပစ် ▁လိုက် ▁အမ ▁😁 ▁😁 ▁😁 ▁😁 ▁ကစ် ▁သာ ▁နေ ▁ရင် ▁ရှမ်း ▁ပြည် ▁အပြီး ▁ပြန် ▁လာ ▁မယ် ▁နေ ▁နိုင် ▁လား ▁ဘဝ ▁ကို ▁ဖြတ်သန်း ▁တဲ့ ▁အခါ ▁အရိုး ဆုံး ▁က ▁အကောင်းဆုံး ▁ပါ ▁ပဲ ▁မ ▁လုပ် ▁ပါ ▁နဲ့ ▁ကစ်လေး ▁ရယ် ▁ရန်ကုန် ▁ကို ▁အမြန် ▁ပြန် ▁လာ ▁ပါ ▁ကိုယ် ▁အရမ်း ▁သတိရ ▁လို့ ▁ပါ ▁ကွာ ▁ချစ် ▁တာ ▁😍 ▁😍 ▁😘 ▁😘 ▁ချစ် ▁စရာ ▁လေး ▁အရမ်း ▁ကြိုက် ▁မမ ▁နေ ▁ပါ ▁ကစ်လေး ▁ရယ် ▁သာယာ ▁လိုက် ▁တာ ▁အဲ့ ▁နား ▁မှာ ▁အိမ် ▁တစ် ▁လုံး ▁သွား ▁ဝယ် ▁လိုက် ▁မှာ ▁ပေါ့ ▁။
▁အင်း သား ▁ဖြစ် ▁ချင် ▁လို့ ▁အင်း သူ မ ▁ပဲ ▁လုပ် ▁တော့ ▁မကစ် ▁ ค ุณ น ่ า รั ก เส ม อ ▁ 💟 ▁ကြည့် ▁လို့ ▁မ ▁ရ ▁တော့ ▁ဘူး ▁နော် ▁ကိုကြီး ▁နေ ▁ဖို့ ▁လည်း ▁မ ▁ကောင်း ▁ပဲ ▁ရေ ▁ထဲ ▁မှာ ▁ငါ ▁မ ▁ကြိုက် ▁ဘူး ▁ကောင်း ▁သား ▁ပဲ ▁အင်း သူ မလေး ▁ဆို ▁တော့ ▁အေးအေးချမ်းချမ် း ▁လေး ▁ပေါ့ ▁နော် ▁မကစ် ▁ကို ▁က ▁အင်း သား ▁ဖြစ် ▁ပါရစေ ▁ကောင်း ▁တာ ▁ပေါ့ ▁ကစ် ▁ရဲ့ ▁အင်း သူ လေး ▁တွေ ▁က ▁ဖြူစင် ▁တယ် ▁အင်း သူ မလေး ▁ဖြစ် ▁တော့ ▁မယ် ▁ရွှေ ▁ကစ်လေး ▁: - ▁* ▁ကောင်း ▁သလိုလို ▁တော့ ▁ရှိ ▁သား ▁နော်
▁ရွှေ ▁ကစ်လေး ▁ရဲ့ ▁ကုသိုလ် ▁ကြောင့် ▁အစစအရာ ရာ ▁ပြီး ပြည့် စုံ ▁မှာ ▁ပါ ▁ရွှေ ▁ကစ်လေး ▁ကို ▁လည်း ▁သေ ▁တဲ့ ▁ထိ ▁အားပေး ▁မှာ ▁ပါ ▁အရမ်း ▁ချစ် ▁တယ် ▁သာဓု ▁ပါ ▁သာဓု ▁ပါ ▁သာဓု ▁ပါ ▁ဒီ ▁ထက် ▁မက ▁လှူ ▁နိုင် ▁ပါစေ ▁နော် ▁👏 ▁👏 ▁👏 ▁👏 ▁👏 ▁👍 ▁👍 ▁👍 ▁အခု ▁လို ▁ပြု ▁ရ ▁သော ▁ကုသိုလ် ▁ကောင်း ▁မှု ▁တွေ ▁ကြောင့် ▁ဘဝ ▁မှာ ▁တောင်း တ ▁ခြင်း ▁နဲ့ ▁ကြောက် ▁ရ ▁ခြင်း ▁ကင်း ဝေး ▁ပြီး ▁တော့ ▁မနက်ဖြန် ▁တွေ ▁တိုင်း ▁မှာ ▁ချစ် ▁တဲ့ ▁မိသားစု ▁နဲ့ ▁ပျော်ရွှင် ▁စွာ ▁ဖြတ်သန်း ▁နိုင် ▁ပါစေ ▁မကစ် ▁😍 ▁😍 ▁😍 ▁😍 ▁😍
▁အနိုင် ရ ▁မည့် ▁အသင်း ▁= ▁ပြင်သစ် ▁ဂိုး ▁ရလဒ် ▁= ▁ပြင်သစ် ▁၂ ▁- ▁၀ ▁ခရို အေးရှား
▁မွန် ▁ရခိုင် ▁ရခိုင် ▁ရခိုင် ▁ရခိုင်
▁ည ▁အရမ်း ▁တိုးတက် ▁လို့ ▁ပါ ▁လား ▁ခြင်္သေ့ ▁အက ▁တွေ ▁နဲ့ ▁တော့ ▁ပြန် ▁ကြည့် ▁ချင် ▁တယ် ▁ယား ▁နေ ▁ရော ▁ပဲ ▁ဝမ်း စာ ရေး ▁က ▁အဓိက ▁ပါ ▁လေ ▁ပြန် ▁တော့ ▁ဘူး ▁တော် ▁ပါ ▁ပေ ▁တယ် ▁ဗျာ ▁လေးစား ▁တယ် ▁ဝိုး ▁လီး ▁ဘဲ ့ ▁စောက် ▁တရုတ် ▁ပွဲ ▁ကျ ▁ ခမ်း ခမ်း နား နား ▁ကျင်းပ ▁ပေး ▁တယ် ▁တရုတ် ▁ပြည် ▁လည်း ▁ဝင် ▁တိုက် ▁လိုက် ▁လေ ▁ဆယ် ဆ ▁ပေး ▁ရင် ▁နိုင် ▁မယ် ▁လာ ▁။
▁အလုပ် ▁လည်း ▁လုပ် ▁ပညာ ▁လည်း ▁ယူ ▁ချမ်းသာ ▁ရင် ▁တရုတ် ▁ပြည် ▁သွား ▁လည် ▁ရင် ▁မ ▁ကောင်း ▁ဘူး ▁လား ▁။
▁အဲ့ ▁အတွေး ▁ပဲ ▁လူ ▁ဖြစ် ▁ရင် ▁ထမင်း ▁စား ▁လည်း ▁အလကား ▁ပဲ ▁။
(base) ye@:~/exp/sentence-seg/ersatz/my-data$ 
```

ထွက်လာတဲ့ output ဖိုင်ကနေမှ ersatz ရဲ့ training format ကို ရအောင် လုပ်ပေးရမယ်။  
\<eos\>, \<mos\> ကို confirmation လုပ်ရမယ်။  

```

```

## Training

```

```

### Sentence Segmentation

```

```

### Evaluation

```

```

## References

- https://github.com/google/sentencepiece/issues/500
