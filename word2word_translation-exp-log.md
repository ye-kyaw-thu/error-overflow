# Word2Word Translation Log

## git clone

```
(base) ye@:/media/ye/project2/exp$ mkdir word2word-tran
(base) ye@:/media/ye/project2/exp$ cd word2word-tran/
(base) ye@:/media/ye/project2/exp/word2word-tran$ 
(base) ye@:/media/ye/project2/exp/word2word-tran$ git clone https://github.com/kakaobrain/word2word
Cloning into 'word2word'...
remote: Enumerating objects: 145, done.
remote: Counting objects: 100% (15/15), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 145 (delta 6), reused 7 (delta 2), pack-reused 130
Receiving objects: 100% (145/145), 1.09 MiB | 1.01 MiB/s, done.
Resolving deltas: 100% (74/74), done.
(base) ye@:/media/ye/project2/exp/word2word-tran$
```

## run setup

```
(base) ye@:/media/ye/project2/exp/word2word-tran$ ls
word2word
(base) ye@:/media/ye/project2/exp/word2word-tran$ cd word2word/
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ python ./setup.py install
running install
/home/ye/anaconda3/lib/python3.7/site-packages/setuptools/command/install.py:37: SetuptoolsDeprecationWarning: setup.py install is deprecated. Use build and pip and other standards-based tools.
  setuptools.SetuptoolsDeprecationWarning,
/home/ye/anaconda3/lib/python3.7/site-packages/setuptools/command/easy_install.py:159: EasyInstallDeprecationWarning: easy_install command is deprecated. Use build and pip and other standards-based tools.
  EasyInstallDeprecationWarning,
/home/ye/anaconda3/lib/python3.7/site-packages/pkg_resources/__init__.py:119: PkgResourcesDeprecationWarning: 4.0.0-unsupported is an invalid version and will not be supported in a future release
  PkgResourcesDeprecationWarning,
running bdist_egg
running egg_info
creating word2word.egg-info
writing word2word.egg-info/PKG-INFO
writing dependency_links to word2word.egg-info/dependency_links.txt
writing requirements to word2word.egg-info/requires.txt
writing top-level names to word2word.egg-info/top_level.txt
writing manifest file 'word2word.egg-info/SOURCES.txt'
reading manifest file 'word2word.egg-info/SOURCES.txt'
reading manifest template 'MANIFEST.in'
adding license file 'LICENSE'
writing manifest file 'word2word.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
creating build
creating build/lib
creating build/lib/word2word
copying word2word/__init__.py -> build/lib/word2word
copying word2word/methods.py -> build/lib/word2word
copying word2word/tokenization.py -> build/lib/word2word
copying word2word/utils.py -> build/lib/word2word
copying word2word/word2word.py -> build/lib/word2word
copying word2word/supporting_languages.txt -> build/lib/word2word
creating build/bdist.linux-x86_64
creating build/bdist.linux-x86_64/egg
creating build/bdist.linux-x86_64/egg/word2word
copying build/lib/word2word/__init__.py -> build/bdist.linux-x86_64/egg/word2word
copying build/lib/word2word/methods.py -> build/bdist.linux-x86_64/egg/word2word
copying build/lib/word2word/tokenization.py -> build/bdist.linux-x86_64/egg/word2word
copying build/lib/word2word/utils.py -> build/bdist.linux-x86_64/egg/word2word
copying build/lib/word2word/word2word.py -> build/bdist.linux-x86_64/egg/word2word
copying build/lib/word2word/supporting_languages.txt -> build/bdist.linux-x86_64/egg/word2word
byte-compiling build/bdist.linux-x86_64/egg/word2word/__init__.py to __init__.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/word2word/methods.py to methods.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/word2word/tokenization.py to tokenization.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/word2word/utils.py to utils.cpython-37.pyc
byte-compiling build/bdist.linux-x86_64/egg/word2word/word2word.py to word2word.cpython-37.pyc
creating build/bdist.linux-x86_64/egg/EGG-INFO
copying word2word.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying word2word.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying word2word.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying word2word.egg-info/requires.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying word2word.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
zip_safe flag not set; analyzing archive contents...
word2word.__pycache__.utils.cpython-37: module references __file__
creating dist
creating 'dist/word2word-1.0.0-py3.7.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing word2word-1.0.0-py3.7.egg
creating /home/ye/anaconda3/lib/python3.7/site-packages/word2word-1.0.0-py3.7.egg
Extracting word2word-1.0.0-py3.7.egg to /home/ye/anaconda3/lib/python3.7/site-packages
Adding word2word 1.0.0 to easy-install.pth file

Installed /home/ye/anaconda3/lib/python3.7/site-packages/word2word-1.0.0-py3.7.egg
Processing dependencies for word2word==1.0.0
Searching for tqdm==4.62.3
Best match: tqdm 4.62.3
Adding tqdm 4.62.3 to easy-install.pth file
Installing tqdm script to /home/ye/anaconda3/bin

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for numpy==1.20.3
Best match: numpy 1.20.3
Adding numpy 1.20.3 to easy-install.pth file
Installing f2py script to /home/ye/anaconda3/bin
Installing f2py3 script to /home/ye/anaconda3/bin
Installing f2py3.7 script to /home/ye/anaconda3/bin

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for wget==3.2
Best match: wget 3.2
Adding wget 3.2 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for requests==2.26.0
Best match: requests 2.26.0
Adding requests 2.26.0 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for urllib3==1.25.8
Best match: urllib3 1.25.8
Adding urllib3 1.25.8 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for idna==2.8
Best match: idna 2.8
Adding idna 2.8 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for charset-normalizer==2.0.7
Best match: charset-normalizer 2.0.7
Adding charset-normalizer 2.0.7 to easy-install.pth file
Installing normalizer script to /home/ye/anaconda3/bin

Using /home/ye/anaconda3/lib/python3.7/site-packages
Searching for certifi==2019.11.28
Best match: certifi 2019.11.28
Adding certifi 2019.11.28 to easy-install.pth file

Using /home/ye/anaconda3/lib/python3.7/site-packages
Finished processing dependencies for word2word==1.0.0
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$
```

## Testing English to French Word-to-Word Translation

ဥပမာ ပြထားတဲ့ python script ကို အခြေခံပြီး delicious ဆိုတဲ့ အင်္ဂလိပ်စာလုံးကို ဘာသာပြန်ခိုင်းကြည့်တဲ့ script ကို ပြင်ဆင်ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ cat ./en2fr-word2word.py 
from word2word import Word2word
en2fr = Word2word("en", "fr")
print(en2fr("delicious"))
```

ပထမဆုံး run တာမို့လို့ data download လုပ်ပုံရတယ်။  
ပြင်သစ်လို့ ဘာသာပြနေပေးတာကို အောက်ပါအတိုင်း တွေ့ရတယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ python ./en2fr-word2word.py 
Downloading data ...
100% [..........................................................................] 8022400 / 8022400['délicieux', 'délicieuse', 'délicieuses', 'Délicieux', 'repas']
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$
```

## Testing English to Chinese Word-to-Word Translation

ဒီတစ်ခါတော့ အင်္ဂလိပ်ကနေ တရုပ်ဘာသာကို ပြန်ခိုင်းကြည့်ခဲ့တယ်။  
n_best=3 ဆိုတဲ့ parameter ကိုပေးပြီး စမ်းကြည့်ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ cat ./en2zh-word2word.py 
from word2word import Word2word

en2fr = Word2word("en", "zh_cn")
print(en2fr("delicious", n_best=3))
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ python ./en2zh-word2word.py 
Downloading data ...
100% [........................................................................] 11151257 / 11151257['美味', '好吃', 'delicious']
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ 
```

Error မပေးပဲ အလုပ်လုပ်ပေးပါတယ်။  
သုံးလုံးမြောက်ကတော့ အင်္ဂလိပ်လိုပဲ ပြန်ထွက်လာတာကို တွေ့ရတယ်။  

## Testing English to Thai Word-to-Word Translation

ဒီတစ်ခါတော့ အင်္ဂလိပ်ကနေ ထိုင်းကို ဘာသာပြန်တာကို interactive Python mode နဲ့ run ကြည့်ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ python
Python 3.7.6 (default, Jan  8 2020, 19:59:22) 
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from word2word import Word2word
>>> en2th = Word2word("en", "th")
Downloading data ...
100% [........................................................................] 37941045 / 37941045Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/word2word.py", line 50, in __init__
    lang1, lang2, custom_savedir
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/utils.py", line 56, in download_or_load
    word2x, y2word, x2ys = pickle.load(open(fpath, 'rb'))
ModuleNotFoundError: No module named 'pythainlp'
>>> exit()
```

အထက်ပါအတိုင်း ထိုင်းဘာသာပြန်ဖို့အတွက်က pythainlp module ကို ကိုယ့်စက်ထဲမှာ install လုပ်ထားဖို့ လိုအပ်တာကို တွေ့ရတယ်။  
အဲဒါနဲ့ pip install command ကို သုံးပြီး အောက်ပါအတိုင်း pythainlp ကို installation လုပ်ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ pip install pythainlp
Collecting pythainlp
  Downloading pythainlp-2.3.2-py3-none-any.whl (11.0 MB)
     |████████████████████████████████| 11.0 MB 1.7 MB/s            
Collecting tinydb>=3.0
  Downloading tinydb-4.5.2-py3-none-any.whl (23 kB)
Collecting python-crfsuite>=0.9.6
  Downloading python_crfsuite-0.9.7-cp37-cp37m-manylinux1_x86_64.whl (743 kB)
     |████████████████████████████████| 743 kB 139.8 MB/s            
Requirement already satisfied: requests>=2.22.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from pythainlp) (2.26.0)
Requirement already satisfied: charset-normalizer~=2.0.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from requests>=2.22.0->pythainlp) (2.0.7)
Requirement already satisfied: idna<4,>=2.5 in /home/ye/anaconda3/lib/python3.7/site-packages (from requests>=2.22.0->pythainlp) (2.8)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/anaconda3/lib/python3.7/site-packages (from requests>=2.22.0->pythainlp) (2019.11.28)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /home/ye/anaconda3/lib/python3.7/site-packages (from requests>=2.22.0->pythainlp) (1.25.8)
Collecting typing-extensions<4.0.0,>=3.10.0
  Using cached typing_extensions-3.10.0.2-py3-none-any.whl (26 kB)
Installing collected packages: typing-extensions, tinydb, python-crfsuite, pythainlp
  Attempting uninstall: typing-extensions
    Found existing installation: typing-extensions 3.7.4.3
    Uninstalling typing-extensions-3.7.4.3:
      Successfully uninstalled typing-extensions-3.7.4.3
Successfully installed pythainlp-2.3.2 python-crfsuite-0.9.7 tinydb-4.5.2 typing-extensions-3.10.0.2
```

English-to-Thai ဘာသာပြန်တာကို ထပ်စမ်းခဲ့တယ်။  
"hello!" ဆိုပြီး punctuation character ထည့်ပြီး စမ်းခဲ့တာလက်မခံတာကို တွေ့ရတယ်။  
ပြီးတော့ လုံးဝ word to word ပဲ ဘာသာပြန်တာ compound word level အထိ မသွားနိုင်တာကို တွေ့ရတယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ python
Python 3.7.6 (default, Jan  8 2020, 19:59:22) 
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from word2word import Word2word
>>> en2th = Word2word("en", "th")
>>> print(en2th("hello!"))
Traceback (most recent call last):
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/word2word.py", line 59, in __call__
    x = self.word2x[query]
KeyError: 'hello!'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/word2word.py", line 64, in __call__
    f"query word {query} not found in the bilingual lexicon."
KeyError: 'query word hello! not found in the bilingual lexicon.'
>>> print(en2th("hello"))
['สวัสดี', 'ทักทาย', 'ฮัลโหล', 'หวัด', 'ฝาก']
>>> print(en2th("pagoda"))
['ศาลา', 'ข้างนอกน่ะ', 'แถวๆ', 'อยู่', 'เห็น']
>>> print(en2th("noodle"))
['บะหมี่', 'ยอน', 'ก๋วยเตี๋ยว', 'ร้านบะหมี่', 'สมอง']
>>> print(en2th("how much"))
Traceback (most recent call last):
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/word2word.py", line 59, in __call__
    x = self.word2x[query]
KeyError: 'how much'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/word2word.py", line 64, in __call__
    f"query word {query} not found in the bilingual lexicon."
KeyError: 'query word how much not found in the bilingual lexicon.'
>>> print(en2th("how"))
['เป็นไง', 'อย่างไร', 'วิธี', 'เท่าไหร่', 'กี่']
>>> print(en2th("much"))
['มากนัก', 'มากเกินไป', 'เท่าไร', 'เท่าไหร่', 'ไม่ค่อย']
>>> exit()
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$
```

## Testing Japanese to English Translation

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ python
Python 3.7.6 (default, Jan  8 2020, 19:59:22) 
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from word2word import Word2word
>>> ja2en = Word2word("ja", "en")
Downloading data ...
100% [..........................................................................] 7272863 / 7272863>>> 
>>> print(ja2en("ビルマ"))
['Burma', 'Burmese', 'Rangoon', 'burma', 'Kyi']
>>> print(ja2en("刺し身"))
Traceback (most recent call last):
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/word2word.py", line 59, in __call__
    x = self.word2x[query]
KeyError: '刺し身'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/word2word.py", line 64, in __call__
    f"query word {query} not found in the bilingual lexicon."
KeyError: 'query word 刺し身 not found in the bilingual lexicon.'
>>> print(ja2en("刺身"))
['sashimi', 'sabu', 'lacquered', 'tartare', 'confit']
>>> print(ja2en("人工知能"))
Traceback (most recent call last):
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/word2word.py", line 59, in __call__
    x = self.word2x[query]
KeyError: '人工知能'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/word2word.py", line 64, in __call__
    f"query word {query} not found in the bilingual lexicon."
KeyError: 'query word 人工知能 not found in the bilingual lexicon.'
>>> print(ja2en("自然言語処理"))
Traceback (most recent call last):
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/word2word.py", line 59, in __call__
    x = self.word2x[query]
KeyError: '自然言語処理'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/word2word.py", line 64, in __call__
    f"query word {query} not found in the bilingual lexicon."
KeyError: 'query word 自然言語処理 not found in the bilingual lexicon.'
>>> print(ja2en("言語処理"))
Traceback (most recent call last):
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/word2word.py", line 59, in __call__
    x = self.word2x[query]
KeyError: '言語処理'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/word2word.py", line 64, in __call__
    f"query word {query} not found in the bilingual lexicon."
KeyError: 'query word 言語処理 not found in the bilingual lexicon.'
>>> print(ja2en("言語"))
['language', 'languages', 'speech', 'programming', 'linguist']
>>> print(ja2en("自然"))
['natural', 'nature', 'naturally', 'Nature', 'unnatural']
>>> print(ja2en("処理"))
['handle', 'processing', 'process', 'paperwork', 'squad']
>>> print(ja2en("合気道"))
Traceback (most recent call last):
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/word2word.py", line 59, in __call__
    x = self.word2x[query]
KeyError: '合気道'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/word2word.py", line 64, in __call__
    f"query word {query} not found in the bilingual lexicon."
KeyError: 'query word 合気道 not found in the bilingual lexicon.'
>>> print(ja2en("空手"))
['karate', 'Karate', 'chop', 'fighting', 'geto']
>>> exit()
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$
```

## Building Lexicon with Myanmar-Sgaw-Kayin Parallel Data

training data နဲ့ development data ကို ပေါင်းခဲ့တယ်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ cat train.mya dev.mya > train_dev.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ cat train.sgk dev.sgk > train_dev.sk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ wc train_dev.my 
  61714  367354 5808719 train_dev.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ wc train_dev.sk
  61714  223980 6073587 train_dev.sk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$
```

ဒေတာ ကို head command နဲ့ confirm လုပ်ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ head ./train_dev.my 
မင်း ဘယ်သူ့ ကို မေး ရမှာလဲ
အဲ့ဒီ အကြောင်း မင်း ဘယ်သူ့ ကို ပြော ရမှာလဲ
မင်း ဘယ်သူ့ ကို တွေ့ ရမှာလဲ
မင်း ဘယ်သူ့ ကို ရွေး ရမှာလဲ
မင်း ဘယ်သူ့ ကို အပြစ်ပေး ရမှာလဲ
မင်း ဘယ်သူ့ ကို ရှာ မှာလဲ
မင်း ဘယ်သူ့ ကို ပြော ခဲ့တာလဲ
မင်း ဘယ်သူ့ ကို ပေး ခဲ့တာလဲ
မင်း ဘယ်သူ့ ကို ခေါ် ခဲ့တာလဲ
ဘယ်သူတွေ ကို ခင်ဗျား မြင် ခဲ့တာလဲ
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ head ./train_dev.sk
န ဘၣ်သံကွၢ်တၢ် မတၤ န့ၣ်လဲၣ်
တၢ်ဂ့ၢ်ဝဲအံၤ နဘၣ်တဲတၢ် မတၤ န့ၣ်လဲၣ်
န ဘၣ်ထံၣ်လိာ်သးဒီး မတၤ န့ၣ်လဲၣ်
န ဘၣ်တၢ်ဃုထၢ မတၤ န့ၣ်လဲၣ်
န ဘၣ်စံၣ်ညီၣ်တၢ် မတၤ န့ၣ်လဲၣ်
န ဘၣ်ကွၢ်ဃုတၢ် မတၤန့ၣ်လဲၣ်
န တဲတ့ၢ် မတၤ န့ၣ်လဲၣ်
န ဟ့ၣ်တ့ၢ် မတၤ န့ၣ်လဲၣ်
န ကိးတ့ၢ် မတၤ န့ၣ်လဲၣ်
န ထံၣ်တ့ၢ် မတၤသ့ၣ် န့ၣ်လဲၣ်
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$
```

ဖိုင်နာမည်ကို သတ်မှတ်ထားတဲ့အတိုင်း ပြောင်းပေးခဲ့တယ်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ mv ./my-sgk/train_dev.my ./my-sgk/train_dev.my-sk.my
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ mv ./my-sgk/train_dev.sk ./my-sgk/train_dev.my-sk.sk
```

GitHub မှာ ဥပမာအနေနဲ့ ပြထားတာကိုပဲ အခြေခံပြီး training and testing python program ကို အောက်ပါအတိုင်း ရေးခဲ့တယ်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ cat ./train-tran-my-sk.py 
from word2word import Word2word

# custom parallel data: my-sgk/train_dev.my-sk.my, my-sgk/train_dev.my-sk.sk ဆိုပြီး ပြင်ထားခဲ့တယ်
my_my2sk = Word2word.make("my", "sk", "my-sgk/train_dev.my-sk")
# ...building...
print(my_my2sk("အပြစ်ပေး"))
```

ပထမဆုံး training/testing လုပ်တော့ အောက်ပါအတိုင်း ဖိုင်က ရှိနေတယ် ဆိုပြီး error ပေးခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ time python ./train-tran-my-sk.py 
Step 0. Check files
Step 1. Load tokenizer
Step 2. Constructing sentences
Entering multiprocessing with 16 workers...
Entering multiprocessing with 16 workers...
Time taken for step 2: 0.80s
Traceback (most recent call last):
  File "./train-tran-my-sk.py", line 4, in <module>
    my_my2sk = Word2word.make("my", "sk", "my-sgk/train_dev.my-sk")
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/word2word.py", line 139, in make
    savedir = get_savedir(savedir if savedir else datapref)
  File "/media/ye/project2/exp/word2word-tran/word2word/word2word/utils.py", line 13, in get_savedir
    os.makedirs(savedir, exist_ok=True)
  File "/home/ye/anaconda3/lib/python3.7/os.py", line 221, in makedirs
    mkdir(name, mode)
FileExistsError: [Errno 17] File exists: 'my-sgk/train_dev.my-sk'

real	0m1.693s
user	0m4.089s
sys	0m0.874s
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$
```

အကြောင်းအရင်းက လိုရမယ်ရ parallel data အဖြစ် paste နဲ့ တွဲထားတဲ့ ဖိုင်နာမည်တူက အောက်ပါအတိုင်း ရှိနေခဲ့လို့...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ head ./train_dev.my-sk 
မင်း ဘယ်သူ့ ကို မေး ရမှာလဲ	န ဘၣ်သံကွၢ်တၢ် မတၤ န့ၣ်လဲၣ်
အဲ့ဒီ အကြောင်း မင်း ဘယ်သူ့ ကို ပြော ရမှာလဲ	တၢ်ဂ့ၢ်ဝဲအံၤ နဘၣ်တဲတၢ် မတၤ န့ၣ်လဲၣ်
မင်း ဘယ်သူ့ ကို တွေ့ ရမှာလဲ	န ဘၣ်ထံၣ်လိာ်သးဒီး မတၤ န့ၣ်လဲၣ်
မင်း ဘယ်သူ့ ကို ရွေး ရမှာလဲ	န ဘၣ်တၢ်ဃုထၢ မတၤ န့ၣ်လဲၣ်
မင်း ဘယ်သူ့ ကို အပြစ်ပေး ရမှာလဲ	န ဘၣ်စံၣ်ညီၣ်တၢ် မတၤ န့ၣ်လဲၣ်
မင်း ဘယ်သူ့ ကို ရှာ မှာလဲ	န ဘၣ်ကွၢ်ဃုတၢ် မတၤန့ၣ်လဲၣ်
မင်း ဘယ်သူ့ ကို ပြော ခဲ့တာလဲ	န တဲတ့ၢ် မတၤ န့ၣ်လဲၣ်
မင်း ဘယ်သူ့ ကို ပေး ခဲ့တာလဲ	န ဟ့ၣ်တ့ၢ် မတၤ န့ၣ်လဲၣ်
မင်း ဘယ်သူ့ ကို ခေါ် ခဲ့တာလဲ	န ကိးတ့ၢ် မတၤ န့ၣ်လဲၣ်
ဘယ်သူတွေ ကို ခင်ဗျား မြင် ခဲ့တာလဲ	န ထံၣ်တ့ၢ် မတၤသ့ၣ် န့ၣ်လဲၣ်
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$
```
print(my_my2sk("ခင်ဗျား"))
အဲဒါကြောင့် အဲဒီ file ကို bk ဆိုတဲ့ folder အောက်ထဲကို ရွှေ့ပေးထားခဲ့တယ်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ mkdir bk
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ mv train_dev.my-sk ./bk/
```

အဲဒါကြောင့် training မလုပ်ခင်မှာ "train_dev.my-sk" လိုမျိုး နာမည်တူ ဖိုင်မရှိစေဖို့ ဂရုပြုပါ။  
ဒီတစ်ခေါက် training/testing သို့မဟုတ် မြန်မာ-စကောကရင် lexicon building လုပ်ပြီး word-to-word translation လုပ်ကြည့်ခဲ့တော့ အောက်ပါအတိုင်း အဆင်ပြေပြေနဲ့ လုပ်ပေးတာကို တွေ့ရပါတယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ time python ./train-tran-my-sk.py 
Step 0. Check files
Step 1. Load tokenizer
Step 2. Constructing sentences
Entering multiprocessing with 16 workers...
Entering multiprocessing with 16 workers...
Time taken for step 2: 0.83s
Step 3. Compute vocabularies
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 367364/367364 [00:00<00:00, 2588083.63it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 20858/20858 [00:00<00:00, 3179184.27it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 224021/224021 [00:00<00:00, 4171456.25it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 76796/76796 [00:00<00:00, 2420628.48it/s]
Step 4. Update count dictionaries
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 61714/61714 [00:01<00:00, 35281.60it/s]
Step 5. Translation using CPE scores
Entering multiprocessing with 16 workers... (#words=20858)
Entering multiprocessing with 16 workers... (#words=76796)
Time taken for step 5: 11.59s
Saving...
Done!
['စံၣ်ညီၣ်', 'နကစံၣ်ညီၣ်ဝဲ', 'စံၣ်ညီၣ်တၢ်', 'စံၣ်ညီၣ်ဝဲ', 'ဘၣ်စံၣ်ညီၣ်']

real	0m15.557s
user	0m43.753s
sys	0m5.505s
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$
```

output အနေနဲ့ က အောက်ပါအတိုင်း bidirectional အတွက် lexicon နှစ်ခု ရတာကို တွေ့ရတယ်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/train_dev.my-sk$ ls
my-sk.pkl  sk-my.pkl
```

## word-to-word translation between Myanmar and Sgaw Kayin

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ python
Python 3.7.6 (default, Jan  8 2020, 19:59:22) 
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from word2word import Word2word
>>> my_my2sk = Word2word.load("my", "sk", "my-sgk/train_dev.my-sk")
Loaded word2word custom bilingual lexicon from my-sgk/train_dev.my-sk/my-sk.pkl
>>> print(my_my2sk("ခင်ဗျား"))
['နကဘၣ်', 'နၤန့ၣ်လီၤ', 'နမၤဝဲ', 'နဘၣ်သး', 'နဲ']
>>> my_sk2my = Word2word.load("sk", "my", "my-sgk/train_dev.my-sk")
Loaded word2word custom bilingual lexicon from my-sgk/train_dev.my-sk/sk-my.pkl
>>> print(my_sk2my("နကဘၣ်"))
['ခင်ဗျား', 'ရမယ်', 'လိမ့်မယ်', 'မင်း', 'ရမှာလဲ']
>>> 
```

