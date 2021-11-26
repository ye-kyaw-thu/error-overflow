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

## Word-to-Word translation between Myanmar and Sgaw Kayin

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

## pkl to txt File Conversion

.pkl ဖိုင်ထဲမှာ ဒေတာတွေကို ဘယ်လိုသိမ်းထားသလဲ ဆိုတာကို သိချင်တဲ့ သူတွေအတွက် pkl to txt file conversion ကို နမူနာအနေနဲ့ လုပ်ပြထားတာပါ။  
python code ကို အောက်ပါအတိုင်း ရေးပြီး my-sk.pkl ဖိုင်ကို text ဖိုင်အဖြစ် ပြောင်းကြည့်ရအောင်...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/train_dev.my-sk$ cat ./pkl-read.py 
import pickle

with open('my-sk.pkl', 'rb') as f:
    data = pickle.load(f)

print(data)
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/train_dev.my-sk$
```

run ပြီး ထွက်လာတဲ့ output ကို text ဖိုင်အနေနဲ့ သိမ်းခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/train_dev.my-sk$ python ./pkl-read.py > my-sk.pkl.txt
```

သူက data ကို serialization လုပ်ပြီး သိမ်းတဲ့ ပုံစံပါ အဲဒါကြောင့် wc command နဲ့ file size ကို စစ်ကြည့်ရင် one line ဆိုတာမျိုးနဲ့ပဲ ပြပေးပါလိမ့်မယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/train_dev.my-sk$ wc ./my-sk.pkl.txt 
      1  387616 5932283 ./my-sk.pkl.txt
```

vi editor ကို သုံးပြီး ကြည့်ခဲ့တယ်။ text file ရဲ့ ထိပ်ဆုံးပိုင်းမှာက အောက်ပါအတိုင်း မြင်တွေ့ရပါလိမ့်မယ်။  

```
({'ကို': 0, 'မ': 1, 'မင်း': 2, 'ကျွန်တော': 3, '၂': 4, 'တယ်': 5, '၁': 6, 'သူ': 7, '၃': 8, '၅': 9, '၄': 10, 'မှာ': 11, '၉': 12, '၆': 13, '၇': 14, 'က': 15, '၈': 16: 17, '၀': 18, 'ခင်ဗျာ': 19, 'သူမ': 20, 'နဲ့': 21, 'ဘူး': 22, 'တွေ': 23, 'သူတို': 24, 'ရှိ': 25, 'ဖို': 26, 'လဲ': 27, 'ငါ': 28, 'သွာ': 29, 'လို': 30, 'တို': 31, 'ဒီ': 32, ', 'ဘာ': 34, 'လား': 35, 'တာ': 36, 'တဲ့': 37, 'သလဲ': 38, 'လုပ်': 39, 'ကျွန်တော': 40, 'ပြေ': 41, 'တစ်': 42, 'သူ့': 43, 'ပဲ': 44, 'ဘူးလား': 45, 'မယ်': 46, 'ကျွန်တောတို': 47,49, 'သိ': 50, 'ပါတယ်': 51, 'အတွက်': 52, 'လာ': 53, 'အဲ့ဒါ': 54, 'ရင်': 55, 'ဖြစ်': 56, 'ဘယ်သူ့': 57, 'ခဲ့တယ်': 58, 'ဘယ်လောက်': 59, 'ကောင်း': 60, 'သလား': 61, 'ဘယ်': 62, 'ပေ64, 'ဟာ': 65, 'ဆိုတာ': 66, 'အဲဒါ': 67, 'နေတယ်': 68, 'တော': 69, 'တာလဲ': 70, 'ရဲ့': 71, 'နော': 72, 'ငါ့': 73, 'စား': 74, 'နှစ်': 75, 'ဟုတ်': 76, 'တွေ': 77, 'အလုပ်': 78, ': 80, 'အိမ်': 81, 'လည်း': 82, 'ဘယ်လို': 83, 'ကြိက်': 84, 'လိမ့်မယ်': 85, 'အဲ့ဒါကို': 86, 'ဒီနေ့': 87, 'ပါဘူး': 88, 'လို': 89, 'မင်းကို': 90, 'အချိန်': 91, 'ဒါ': 92, 'မလဲ': 93, 'သူ့ထဲမှာ': 95, 'ကြ': 96, 'လိုက်': 97, 'နာရီ': 98, 'သူက': 99, 'မှာလား': 100, 'ပြန်': 101, 'ငါ့ကို': 102, 'ဒီမှာ': 103, 'ကျွန်မ': 104, 'ချင်': 105, 'မှာလဲ': 106, 'အဲဒီ': 107, 'ဘယ်: 109, 'အခု': 110, 'မေး': 111, 'ကား': 112, 'ဝယ်': 113, 'လောက်': 114, 'မဟုတ်ဘူးလား': 115, 'စာအုပ်': 116, 'ရောက်': 117, 'ယောက်': 118, 'မဟုတ်ဘူး': 119, 'ခဲ့ဘူးလား': 120, '2, 'သောက်': 123, 'ကြည့်': 124, 'ထား': 125, 'ကြိစား': 126, 'ကူညီ': 127, 'ကိုယ်': 128, 'မလား': 129, 'သေး': 130, 'သူတိုကို': 131, 'အဲဒါကို': 132, 'ငါတို': 133, 'ရှိတယ်': 134, 'ခတောကို': 136, 'အားလုံ': 137, 'နောက်': 138, 'မှ': 139, 'သည်': 140, 'ခဲ့': 141, 'ကြာ': 142, 'သုံ': 143, 'တာလား': 144, 'အရမ်း': 145, 'ရမလဲ': 146, 'ကျေဇူးပြုပြီ': 147, 'စကာ'ထပ်': 150, 'ဒါပေမဲ့': 151, 'ကြာ': 152, 'မျာ': 153, 'မင်းရဲ့': 154, 'ငွေ': 155, 'ပါနဲ့': 156, 'ဘယ်မှာ': 157, 'ထွက်': 158, 'အဲ့ဒီ': 159, 'မြင်': 160, 'ခု': 161, 'ရမယ်': 1623, 'စဉ်းစား': 164, 'တက်': 165, 'အကြေင်း': 166, 'ရတာ': 167, 'ဆိုရင်': 168, 'ပေါ': 169, 'တတ်': 170, 'ထဲ': 171, 'မနက်ဖြန်': 172, 'ဘာ့ကြေင့်': 173, 'ပို': 174, 'ကြတယ်': 175 'လ': 177, 'ဦး': 178, 'ဘယ်သူတွေ': 179, 'ထိုင်': 180, 'ခဲ့ဘူး': 181, 'ကြည့်': 182, 'ဟုတ်ကဲ့': 183, 'အောင်': 184, 'နေတာလဲ': 185, 'ဆရာ': 186, 'မြန်မာ': 187, 'နေ့': 188, 'နိုင်တယ်: 190, 'ရမလား': 191, 'ခဲ့လိုလား': 192, 'ပေါမှာ': 193, 'အခန်း': 194, 'ဘာကြေင့်': 195, 'ခဲ့သလား': 196, 'ဘာဖြစ်လို': 197, 'အမျာကြီ': 198, 'လမ်း': 199, 'တစ်ခု': 200, 'ကျွန်တောက်': 203, 'ခဲ့တာလဲ': 204, 'ဆို': 205, 'ဖတ်': 206, 'နည်းနည်း': 207, 'ရဲ့လား': 208, 'နိုင်မလား': 209, 'ထက်': 210, 'သူငယ်ချင်း': 211, 'ချင်တယ်': 212, 'ပေါ': 213, 'ယုံ': 214, 'မြိ216, 'ဘာတွေ': 217, 'အဖြေ': 218, 'စာ': 219, 'သူ့ရဲ့': 220, 'ရမှာ': 221, 'သွာတယ်': 222, 'မျှလင့်': 223, 'ရက်': 224, 'ကျေင်း': 225, 'နေတာ': 226, 'ရှင်': 227, 'စ': 228, 'ပ230, 'ဝမ်းသာ': 231, 'ခဲ့သလဲ': 232, 'တောတော': 233, 'ခင်ဗျာ': 234, 'ရေး': 235, 'ဒီလို': 236, 'ဖုန်းဆက်': 237, 'ပိုက်ဆံ': 238, 'အလွန်': 239, 'လေ': 240, 'မျိ': 241, 'ခင်ဗျာရဲ့':, 'တကယ်': 244, 'ဆီ': 245, 'ဒါကို': 246, 'အိပ်': 247, 'လိုက်တယ်': 248, 'ခေါ': 249, 'သလို': 250, 'မနက်': 251, 'ခဲ့တာလား': 252, 'ခဲ့ကြတယ်': 253, 'မှာပါ': 254, 'ပြီတော': 255, ''မနေ့က': 257, 'ဒါပေမယ့်': 258, 'ည': 259, 'သူမကို': 260, 'လေး': 261, 'တိုင်း': 262, 'ကလေး': 263, 'ကစား': 264, 'လိုချင်': 265, 'စောင့်': 266, 'ရောင်း': 267, 'ညစာ': 268, 70, 'ရအောင်': 271, 'မိနစ်': 272, 'ဆိုင်': 273, 'ကောဖီ': 274, 'ကိစ္စ': 275, 'တောင်': 276, 'စားပွဲ': 277, 'လာတယ်': 278, 'ရော': 279, 'နိုင်ငံ': 280, 'သူတိုက': 281, 'ကြီ': 282, 'ဒီကို': 284, 'ပစ္စည်း': 285, 'ရှာ': 286, 'အမေ': 287, 'ရတယ်': 288, 'ခဲ့ပါဘူး': 289, 'ချက်': 290, 'ကျ': 291, 'သူမရဲ့': 292, 'လုံ': 293, 'ဆေး': 294, 'သင်': 295, 'ရှင်းပြ': 2297, 'ခဏ': 298, 'ငါး': 299, 'လှ': 300, 'ဘယ်သူ့ကို': 301, 'ပါရစေ': 302, 'ဘယ်နှ': 303, 'သင့်တယ်': 304, 'ရေ': 305, 'တစ်ခုခု': 306, 'ဒါမှမဟုတ်': 307, 'ကောင်းကောင်း': 308, 'ဒေါကြေင့်': 310, 'အမြဲ': 311, 'ရာသီဥတု': 312, 'ပြ': 313, 'ပေးပါ': 314, 'ခဲ့ပါတယ်': 315, 'မေ့': 316, 'ဆရာဝန်': 317, 'ခွေ': 318, 'ဖွင့်': 319, 'နောက်ကျ': 320, 'ဝင်': 321, 'ဈ323, 'မင်းတို': 324, 'အဖေ': 325, 'အပြင်': 326, 'လမ်းလျှက်': 327, 'နေပြီ': 328, 'သင့်': 329, 'လေ့': 330, 'ဘာမှ': 331, '\u200bကျေဇူးပြုပြီ': 332, 'အလုပ်လုပ်': 333, 'အဆင်ပြေ': 'နားလည်': 336, 'တခြာ': 337, 'ရေကူး': 338, 'မဟုတ်ပါဘူး': 339, 'ထင်တယ်': 340, 'စောစော': 341, 'ရိုက်': 342, 'ရထား': 343, 'ဘယ်တောမှ': 344, 'ဖုန်း': 345, 'ပါလား': 346, 'ဝ 'ကောင်လေး': 349, 'အဲဒါက': 350, 'ကြဘူး': 351, 'အသစ်': 352, 'သင်တန်း': 353, 'နဲ့အတူ': 354, 'ဟုတ်ဘူး': 355, 'ပတ်': 356, 'ရန်ကုန်': 357, 'မဟုတ်': 358, 'တောမယ်': 359, 'အတော': 361, 'ပါသလား': 362, 'ဆရာမ': 363, 'အသက်': 364, 'ပြီပြီ': 365, 'တံခါး': 366, 'ကျွန်တောက': 367, 'ပိတ်': 368, 'အတန်း': 369, 'သား': 370, 'လက်မှတ်': 371, 'ကျေင်းသား': 372,: 374, 'နောက်ထပ်': 375, 'စာမေးပွဲ': 376, 'စကားပြေ': 377, 'ကျေဇူးတင်': 378, 'ဖူး': 379, 'ထဲက': 380, 'ကုမ္ပဏီ': 381, 'ဆေးလိပ်': 382, 'ဆုံဖြတ်': 383, 'မှတ်မိ': 384, 'နေကြတယ်': 'ရက်နေ့': 387, 'အစီအစဉ်': 388, 'ပါမယ်': 389, 'ဒါဆို': 390, 'ကျပ်': 391, 'အဲ့ဒီကို': 392, 'အောင်မြင်': 393, 'ဘုရား': 394, 'ဘယ်အချိန်': 395, 'ကနေ': 396, 'သူဟာ': 397, 'ဖြေ': 9, 'အခြေအနေ': 400, 'ပုံ': 401, 'တီဗွီ': 402, 'မုန်း': 403, 'ဘောလုံ': 404, 'အဲဒီကို': 405, 'လက်ထပ်': 406, 'နာမည်': 407, 'တုန်း': 408, 'ဘာမှမ': 409, 'ဘတ်စ်ကား': 410, 'ပြီလား': 2, 'နား': 413, 'အတိုင်း': 414, 'အင်္ဂလိပ်': 415, 'သီချင်း': 416, 'ကျွန်မတို': 417, 'နင်': 418, 'ရမှာလား': 419, 'ပြဿနာ': 420, 'ပို': 421, 'နားထောင်': 422, 'ညနေ': 423, 'လက်ခံ25, 'လေ့လာ': 426, 'ဘက်': 427, 'ပါ့မလား': 428, 'စီစဉ်': 429, 'မနေ့': 430, 'နေပါတယ်': 431, 'ဟင်း': 432, 'သာ': 433, 'လိမ့်မယ်': 434, 'ဘဝ': 435, 'ပါပဲ': 436, 'နှင့်': 437, , 'အကြေင်းကို': 439, 'ရပ်': 440, 'နှစ်သက်': 441, 'အား': 442, 'စစ်ဆေး': 443, 'အထိ': 444, 'ရဲ': 445, 'မျာမျာ': 446, 'မိန်းကလေး': 447, 'မကြာခင်': 448, 'နံပါတ်': 449, 'တဲ့အခ 'ဂရုစိုက်': 452, 'လိုက်ပါ': 453, 'သေချာ': 454, 'လေယာဉ်': 455, 'ရှေ': 456, 'ဘယ်တော': 457, 'ပြင်': 458, 'ငို': 459, 'ခဲ့တာ': 460, 'ကြေင့်': 461, 'ကြဘူးလား': 462, 'ကျေ': 46 465, 'ဆယ်': 466, 'ကျွန်တောရဲ့': 467, 'ကောင်မလေး': 468, 'ကိုယ်တိုင်': 469, 'ဘာပဲ': 470, 'ဆို': 471, 'စာရေး': 472, 'စရာ': 473, 'ကျွန်တောမှာ': 474, 'အချိန်တန်ပြီ': 475, 'ဟိုတယ်': ကျ': 478, 'ကြမှာ': 479, 'ပွဲ': 480, 'ဆွေနွေ': 481, 'ငှာ': 482, 'မင်းက': 483, 'ဘာကို': 484, 'နိုင်ဘူး': 485, 'နိုင်ပါတယ်': 486, 'ကြရအောင်': 487, 'သူတိုရဲ့': 488, 'မှန်': 489, 'ထွက်"./my-sk.pkl.txt" 1L, 5932283C 
```

ဖိုင်ရဲ့ နောက်ဆုံး အပိုင်းမှာက အောက်ပါအတိုင်း ရှိနေပါလိမ့်မယ်။  

```
12, 13], 17729: [5014, 36, 61], 18631: [72856, 4843, 174, 143], 16026: [37809, 16287, 35, 287, 756, 112], 17682: [55917, 59634, 36494, 45187, 631, 160, 385, 2], 16016: [1636, 170, 180, 1], 17412: [2427, 26801, 1654, 236, 22], 11454: [7, 14, 19254, 71012, 5967, 1187, 181, 77, 6], 19223: [26422, 75803, 39964, 10, 8, 0], 16922: [25850, 21192, 2138, 2], 17366: [396, 4203, 6889, 6, 15], 19884: [579, 59350, 59589, 9473, 34534, 57826, 21930, 65540, 49834, 12224], 16293: [579, 59350, 59589, 9473, 34534, 57826, 21930, 65540, 49834, 12224], 18499: [579, 59350, 59589, 9473, 34534, 57826, 21930, 65540, 49834, 12224], 16079: [579, 59350, 59589, 9473, 34534, 57826, 21930, 65540, 49834, 12224], 16566: [579, 59350, 59589, 9473, 34534, 57826, 21930, 65540, 49834, 12224], 19244: [579, 59350, 59589, 9473, 34534, 57826, 21930, 65540, 49834, 12224], 18872: [10, 23139, 53973, 36096, 41118, 34830, 12991, 957, 828, 1975], 18547: [10, 23139, 53973, 36096, 41118, 34830, 12991, 957, 828, 1975], 17285: [10, 23139, 53973, 36096, 41118, 34830, 12991, 957, 828, 1975], 19940: [3651, 65022, 460, 514, 1, 60, 73, 12, 2], 20524: [46110, 4896, 21168, 46302, 46798, 58712, 41770, 61923, 58798, 39722], 16665: [46110, 4896, 21168, 46302, 46798, 58712, 41770, 61923, 58798, 39722], 16986: [46110, 4896, 21168, 46302, 46798, 58712, 41770, 61923, 58798, 39722], 17717: [46110, 4896, 21168, 46302, 46798, 58712, 41770, 61923, 58798, 39722], 17946: [46110, 4896, 21168, 46302, 46798, 58712, 41770, 61923, 58798, 39722], 18855: [46110, 4896, 21168, 46302, 46798, 58712, 41770, 61923, 58798, 39722], 20461: [1557, 2247, 5560, 15, 1165, 21], 14229: [36, 14416, 479, 61, 54, 19, 5], 17132: [74884, 56752, 54538, 74318, 12873, 11690, 740, 3082, 12], 16245: [9141, 26, 1, 4], 16027: [8949, 610, 133, 603, 18, 15], 5615: [1049, 741, 7, 89, 10755, 39027, 7510, 6, 3], 9864: [44, 350, 15, 8, 236, 2622, 1037, 45], 17224: [3418, 48655, 1711, 430, 1086, 9, 12, 5, 7], 19165: [36578, 7000, 205, 9472, 100, 195, 28, 87, 9, 5], 16292: [10589, 71901, 286], 20573: [56784, 1721, 336, 347], 16512: [40569, 53599, 14103, 983, 366, 1125, 86, 62, 14, 6], 16876: [40569, 53599, 14103, 983, 366, 1125, 86, 62, 14, 6], 19997: [40569, 53599, 14103, 983, 366, 1125, 86, 62, 14, 6], 19785: [40569, 53599, 14103, 983, 366, 1125, 86, 62, 14, 6], 16046: [1414, 8447, 1702, 12, 17, 1, 0], 19525: [23825, 57000, 5010, 1096, 13337, 86, 10, 5, 2], 20211: [23825, 57000, 5010, 1096, 13337, 86, 10, 5, 2], 15133: [1131, 46444, 75764, 75771, 1508, 15, 10, 26, 3], 14295: [28, 14, 3303, 1113, 3113, 682, 7], 15679: [46049, 65041, 23510, 23342, 36382, 115, 10790, 15, 87, 143], 11452: [3931, 246, 19307, 31312, 19306, 14375, 3], 16914: [58048, 2467, 349, 412, 12, 3, 7], 19749: [75366, 54930, 55920, 30874, 4882, 75369, 57646, 21452, 54161, 43563], 18710: [75366, 54930, 55920, 30874, 4882, 75369, 57646, 21452, 54161, 43563], 16890: [2492, 5710, 11337, 99, 6, 0], 16748: [2867, 2694, 28701, 1297, 249, 165, 41, 6, 2], 19293: [57311, 3268, 17275, 6625, 1206, 53, 6, 7], 17305: [22798, 1109, 147, 543, 96, 409, 138, 2, 4, 31], 17578: [52436, 349, 6, 59, 0], 17762: [68515, 4000, 59, 2], 18113: [1066, 347, 85, 28], 20777: [64699, 27, 42, 11], 20596: [4604, 494, 48, 342], 17964: [334, 24, 59, 1], 16954: [19365, 6], 15136: [11750, 2784, 25, 24], 16944: [19299, 1339, 3352], 17384: [399, 995, 0], 20020: [216, 46130], 11447: [7, 6211, 685, 7533, 58864, 57, 38, 577, 3], 15137: [76154, 46981, 35, 15, 6, 8, 4], 20457: [17376, 2057, 15, 4], 20026: [46733, 1076, 1534, 3487, 5, 79], 16920: [55814, 53193, 44, 7], 7325: [367, 39015, 79, 7, 589, 10, 72196, 70644, 1348, 666], 16937: [19320, 25], 16916: [52965, 3673, 1037, 7], 20021: [1201, 15, 3, 39], 20029: [57296, 15, 6782], 20025: [15, 29, 322, 8, 56], 17140: [261, 1256, 401, 0], 20027: [58465, 2057, 3067, 99, 83], 16953: [11208, 7, 6], 19307: [11805, 28101, 49, 2782, 12], 20036: [2361, 26363, 70646, 15], 20039: [38299, 3336, 31482, 15, 5], 20466: [15, 170, 2253], 20028: [2622, 44, 3250, 1192], 20471: [17153, 669, 15, 45, 1, 4], 20450: [4109, 675, 45, 422, 15, 4], 16909: [19279, 8543, 1593], 16952: [19280, 41583, 65120, 1430, 243], 20469: [46111, 56710, 3861, 3, 5], 16951: [12568, 129, 7, 8, 15], 16947: [8247, 4012, 333, 130, 3], 20018: [46105, 57401, 53, 41737], 20448: [11044, 2812, 298, 422, 114, 15, 4], 16906: [13393, 3815, 177, 3, 7], 20467: [11721, 57, 248, 12, 2], 20474: [4553, 2457, 1035, 7511, 229, 4], 15687: [511, 46050, 48482, 12, 11744, 13326, 873, 570, 73, 21], 16929: [1603, 1131, 10, 7, 79, 165, 130, 3], 15676: [1609, 11746, 475, 97, 7127, 57, 86, 192, 69], 20462: [1035, 359, 560, 136, 3], 16911: [4598, 7084, 115, 7, 538], 20453: [7084, 162, 15, 109, 25, 172, 538, 5], 16942: [28377, 245, 7, 89, 3, 45], 16926: [20687, 7, 14, 245, 89, 45, 3], 16927: [9516, 805, 497, 7], 16960: [53428, 3469, 7, 143, 21, 3], 20460: [11747, 22752, 1888, 84, 1497, 3], 20022: [7577, 645, 1876, 330, 12539, 15], 20463: [33082, 56089, 66003, 6], 16958: [2085, 3214, 7], 16918: [8237, 656, 0], 20468: [36800, 46509, 578, 238, 1], 20017: [14160, 11861, 3606, 15, 17, 45], 16903: [570, 203, 6481, 7297, 212], 20032: [20295, 97, 602, 192, 927, 44, 4], 16925: [48950, 19356, 5933], 16948: [19271, 8970, 8239, 21495, 90], 16956: [19314, 58099, 312, 162, 4], 16935: [23509, 7, 3, 75], 7334: [263, 1430, 243, 19347, 19346, 387, 2752, 461, 75, 7], 16378: [1461, 143, 55011, 36], 17451: [59, 24, 184, 1]})
"./my-sk.pkl.txt" 1L, 5932283C
```

## Building Lexicon with make.py

make.py ကို သုံးပြီးတော့လည်း command line ကနေ lexicon (အဘိဓာန်) ဆောက်လို့ ရအောင် support လုပ်ထားတာမို့ ဒီတစ်ခါတော့ make.py ကို သုံးပြီး မြန်မာ-စကောကရင် lexicon ကို ဆောက်ကြည့်မယ်။  
ပထမပိုင်း ဆောက်ထားခဲ့တဲ့ ဖိုလ်ဒါကို အောက်ပါအတိုင်း နာမည်ပြောင်းပြီး သိမ်းခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ mv train_dev.my-sk train_dev.my-sk-1
```

make.py ကို အောက်ပါအတိုင်း option တွေ ပေးပြီး run ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$ time python ./make.py --lang1 my --lang2 sk --datapref my-sgk/train_dev.my-sk --save_pmi --save_cooccurrence --savedir ./my-sgk/lex 
Step 0. Check files
Step 1. Load tokenizer
Step 2. Constructing sentences
Entering multiprocessing with 16 workers...
Entering multiprocessing with 16 workers...
Time taken for step 2: 0.89s
Step 3. Compute vocabularies
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 367364/367364 [00:00<00:00, 3313754.71it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 20856/20856 [00:00<00:00, 3181422.91it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 224021/224021 [00:00<00:00, 4240395.04it/s]
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████| 76796/76796 [00:00<00:00, 2451337.67it/s]
Step 4. Update count dictionaries
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 61714/61714 [00:01<00:00, 35745.99it/s]
Step 5. Translation using CPE scores
Entering multiprocessing with 16 workers... (#words=20856)
Entering multiprocessing with 16 workers... (#words=76796)
Time taken for step 5: 11.32s
Saving...
Step 5-1. Translation using co-occurrence counts
Step 5-2. Translation using PMI scores
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 20856/20856 [00:01<00:00, 18932.49it/s]
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 76796/76796 [00:02<00:00, 36552.13it/s]
Done!

real	0m19.663s
user	0m47.621s
sys	0m5.065s
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word$
```

အထက်မှာ make.py ကို run တဲ့အခါမှာ --save_pmi နဲ့ --save_cooccurrence ဆိုတဲ့ option တွေကိုပါ ပေးခဲ့တာမို့ output အနေနဲ့က အောက်ပါအတိုင်း ရလာပါလိမ့်မယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/lex$ tree
.
├── co
│   ├── my-sk.pkl
│   └── sk-my.pkl
├── my-sk.pkl
├── pmi
│   ├── my-sk.pkl
│   └── sk-my.pkl
└── sk-my.pkl

2 directories, 6 files
```

ဆွဲထုတ်ပြီး ရလာတဲ့ lexicon တွေရဲ့ size ကတော့ မတူဘူး...  
မြန်မာ-စကောကရင်အတွက်က အောက်ပါအတိုင်း တွေ့ရတယ်။  
နောက်တစ်ခုက မြန်မာ-စကောကရင် နဲ့ စကောကရင်-မြန်မာ direction မတူရင် ဆွဲထုတ်လို့ ရတဲ့ စာလုံးအရေအတွက်လည်း မတူဘူးလားလို့?!?!   

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/lex$ wc *.pkl
    5063    31427  5677846 my-sk.pkl
   13684    79284  7153823 sk-my.pkl
   18747   110711 12831669 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/lex$ wc ./co/*.pkl
    5383    32271  5635752 ./co/my-sk.pkl
   12703    77095  7114725 ./co/sk-my.pkl
   18086   109366 12750477 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/lex$ wc ./pmi/*.pkl
    4458    29905  5704552 ./pmi/my-sk.pkl
   13999    79868  7185483 ./pmi/sk-my.pkl
   18457   109773 12890035 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/lex$
```

## Converting co, pmi and cpe pickle files to text files

pkl-print.py ကို အောက်ပါအတိုင်း ရေးခဲ့တယ်။  

```python
import sys
import pickle

# for printing pkl file as normal text
# written by Ye, LST, NECTEC, Thailand

filename = sys.argv[1]

with open(filename, 'rb') as f:
    data = pickle.load(f)
f.close()

print(data)
```

အထက်က python script ကို သုံးပြီးတော့ conversion ကို အောက်ပါအတိုင်း လုပ်ခဲ့တယ်။  

``` 
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ python ./pkl-print.py ./lex/my-sk.pkl > ./lex/my-sk.txt
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ python ./pkl-print.py ./lex/sk-my.pkl > ./lex/sk-my.txt
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ python ./pkl-print.py ./lex/co/my-sk.pkl > ./lex/co/my-sk.txt
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ python ./pkl-print.py ./lex/co/sk-my.pkl > ./lex/co/sk-my.txt
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ python ./pkl-print.py ./lex/pmi/my-sk.pkl > ./lex/pmi/my-sk.txt
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ python ./pkl-print.py ./lex/pmi/sk-my.pkl > ./lex/pmi/sk-my.txt
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ 
```

လိုင်းကတော့ တစ်လိုင်းပဲ ရှိမှာပဲ ဒါပေမဲ့ "," နဲ့ ခြားထားပြီးတော့ အောက်ပါ format နဲ့ သိမ်းထားတာမို့...  

ဖိုင်အစမှာ word တွေကို ID သတ်မှတ်တယ်။  

```{'ကို': 0, 'မ': 1, 'မင်း': 2, 'ကျွန်တော': 3,```   

ပြီးတော့ နောက်ပိုင်းမှာ ID နဲ့ series အလိုက် မှတ်ပြီး သိမ်းသွားတဲ့ ပုံစံ...  

```
6: [4553, 2457, 1035, 7511, 229, 4], 15687: [511, 46050, 48482, 12, 11744, 13326, 873, 570, 73, 21], 16931: [1603, 1131, 10, 7, 79, 165, 130, 3], 15676: [1609, 11746, 475, 97, 7127, 57, 86, 192, 69], 20464: [1035, 359, 560, 136, 3], 16913: [4598, 7084, 115, 7, 538], 20455: [7084, 162, 15, 109, 25, 172, 538, 5], 16944: [28377, 245, 7, 89, 3, 45], 16928: [20687, 7, 14, 245, 89, 45, 3], 16929: [9516, 805, 497, 7], 16962: [53428, 3469, 7, 143, 21, 3], 20462: [11747, 22752, 1888, 84, 1497, 3], 20024: [7577, 645, 1876, 330, 12539, 15], 20465: [33082, 56089, 66003, 6], 16960: [2085, 3214, 7], 16920: [8237, 656, 0], 20470: [36800, 46509, 578, 238, 1], 20019: [14160, 11861, 3606, 15, 17, 45], 16905: [570, 203, 6481, 7297, 212], 20034: [20295, 97, 602, 192, 927, 44, 4], 16927: [48950, 19356, 5933], 16950: [19271, 8970, 8239, 21495, 90], 16958: [19314, 58099, 312, 162, 4], 16937: [23509, 7, 3, 75], 7334: [263, 1430, 243, 19347, 19346, 387, 2752, 461, 75, 7], 16380: [1461, 143, 55011, 36], 17453: [59, 24, 184, 1]})
```

အဲဒါကြောင့် dictionary မှာ ဘယ်နှစ်လုံး ပါသလဲ ဆိုတာကို ရေတွက်ဖို့က linux command line နဲ့ လုပ်ဖို့ မလွယ်လှဘူး...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ wc ./lex/*.txt
       1   387601  5932168 ./lex/my-sk.txt
       1   813308  8049597 ./lex/sk-my.txt
       2  1200909 13981765 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ wc ./lex/co/*.txt
       1   387601  5818194 ./lex/co/my-sk.txt
       1   813308  7951199 ./lex/co/sk-my.txt
       2  1200909 13769393 total
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk$ wc ./lex/pmi/*.txt
       1   387601  5967957 ./lex/pmi/my-sk.txt
       1   813308  8133421 ./lex/pmi/sk-my.txt
       2  1200909 14101378 total
```

## pkl to csv file conversion

CSV ဖိုင်အနေနဲ့ ပြောင်းပြီးတော့ pkl dictionary ထဲက စာလုံးအရေအတွက်ကို ရေလို့ ရမလား လုပ်ကြည့်ခဲ့...  

Reference link: [https://github.com/helenacuesta/csv-pickle-transition/blob/master/pickle2csv.py](https://github.com/helenacuesta/csv-pickle-transition/blob/master/pickle2csv.py)  

အထက်ပါ Github က python code ကို အောက်ပါအတိုင်း filename argument နဲ့ ပေးပြီး run လို့ရအောင် update လုပ်ခဲ့တယ်။  

```python
import csv
from six.moves import cPickle as pickle
import numpy as np
from sys import argv


def pkl_to_csv(path_pickle,path_csv):

    x = []
    with open(path_pickle,'rb') as f:
        x = pickle.load(f)

    with open(path_csv,'w') as f:
        writer = csv.writer(f)
        for line in x: writer.writerow(line)

pkl_file = argv[1]
pkl_to_csv(pkl_file, pkl_file + '.csv')
```

conversion ကို အောက်ပါအတိုင်း လုပ်ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/lex$ python ./pkl2csv.py ./my-sk.pkl ./my-sk.csv
```

csv ဖိုင်အဖြစ် ပြောင်းထားတဲ့ ဖိုင်က line သုံးလိုင်း ရှိတာကို တွေ့ရတယ်။   

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/lex$ wc ./my-sk.csv
      3       3 1167010 ./my-sk.csv
```

ပြောင်းထားပြီးသား ဖိုင်ကို ဝင်ကြည့်တော့ format က အောက်ပါအတိုင်း ...  

```
ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/lex$ head -c 1000 ./my-sk.csv
ကို,မ,မင်း,ကျွန်တော်,၂,တယ်,၁,သူ,၃,၅,၄,မှာ,၉,၆,၇,က,၈,ပါ,၀,ခင်ဗျား,သူမ,နဲ့,ဘူး,တွေ,သူတို့,ရှိ,ဖို့,လဲ,ငါ,သွား,လို့,တို့,ဒီ,ရ,ဘာ,လား,တာ,တဲ့,သလဲ,လုပ်,ကျွန်တော့်,ပြော,တစ်,သူ့,ပဲ,ဘူးလား,မယ်,ကျွန်တော်တို့,ပြီး,နေ,သိ,ပါတယ်,အတွက်,လာ,အဲ့ဒါ,ရင်,ဖြစ်,ဘယ်သူ့,ခဲ့တယ်,ဘယ်လောက်,ကောင်း,သလား,ဘယ်,ပေး,ပြီ,ဟာ,ဆိုတာ,အဲဒါ,နေတယ်,တော့,တာလဲ,ရဲ့,နော်,ငါ့,စား,နှစ်,ဟုတ်,တွေ့,အလုပ်,သိပ်,နိုင်,အိမ်,လည်း,ဘယ်လို,ကြိုက်,လ(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/lex$
```

နံပါတ်တွေကို နောက်ဆုံး လိုင်းမှာ သွားသိမ်းတယ်။  

```
ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/lex$ tail -n 1 ./my-sk.csv | head -c 100
2,57,0,111,988,159,166,41,77,582,1171,286,106,204,63,249,179,19,160,3132,127,2094,50,54,296,2633,124(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/lex$
```

စာလုံးရေ count လုပ်လို့ မရဘူး...  

## Trying with pickle command

Googling လုပ်ရင်းနဲ့ အောက်ပါ link ကို သွားတွေ့တယ်။  
[https://docs.python.org/3/library/pickletools.html#module-pickletools](https://docs.python.org/3/library/pickletools.html#module-pickletools)  

အဲဒါနဲ့ အောက်ပါအတိုင်း run ကြည့်ပြီး output ကို .normal ဆိုတဲ့ နာမည်နဲ့ extension ပေးပြီး သိမ်းခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/lex$ python -m pickle ./my-sk.pkl > ./my-sk.normal
```

head လုပ်ကြည့်တော့...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/lex$ head ./my-sk.normal 
({'*': 20855,
  '+': 20854,
  '-': 1443,
  '.': 5373,
  '.full': 20853,
  '.point': 20852,
  '/': 6623,
  ':': 1442,
  '=': 6622,
  'acer': 16014,
```

tail လုပ်ကြည့်တော့...  

```
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/lex$ tail ./my-sk.normal 
  20846: [49838, 76788, 24],
  20847: [50648, 76789, 76758, 87, 803],
  20848: [58575, 21356, 27598, 43561, 76753, 76790, 23532, 27817, 2060, 2864],
  20849: [43817, 76791, 76779, 76787, 54228, 65267],
  20850: [71509, 46551, 76776, 76792, 76757, 27167, 75610, 151, 31],
  20851: [55077, 8673, 27165, 151, 555],
  20852: [1812],
  20853: [43209],
  20854: [811, 14428, 897, 546, 274],
  20855: [68810, 14428, 2175, 409, 274]})
(base) ye@:/media/ye/project2/exp/word2word-tran/word2word/my-sgk/lex$
```

လက်ရှိအချိန်အထိ အခု ထုတ်ပေးတဲ့ format က json, csv တို့ထက် အများကြီး human readable ဖြစ်တယ်။ :)  

## To Do

- lexical building and test word-to-word translation for all Myanmar parallel corpora
- evaluation on word-to-word translation
- error analysis on word-to-word translation and explore more ...  

## Reference

```
@inproceedings{choe2020word2word,
 author = {Yo Joong Choe and Kyubyong Park and Dongwoo Kim},
 title = {word2word: A Collection of Bilingual Lexicons for 3,564 Language Pairs},
 booktitle = {Proceedings of the 12th International Conference on Language Resources and Evaluation (LREC 2020)},
 year = {2020}
}
```

- [https://github.com/kakaobrain/word2word](https://github.com/kakaobrain/word2word)  
- [https://sites.pitt.edu/~naraehan/python3/pickling.html](https://sites.pitt.edu/~naraehan/python3/pickling.html)  
- [https://github.com/helenacuesta/csv-pickle-transition](https://github.com/helenacuesta/csv-pickle-transition)  

