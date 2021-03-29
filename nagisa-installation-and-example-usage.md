# "nagisa" Installation and Example Usage

Nagisa က ဂျပန်စာလုံးတွေကို word segmentation လုပ်ဖို့နဲ့ POS tagging လုပ်ဖို့အတွက် အသုံးဝင်တဲ့ Python module တစ်ခုပါ။ သုံးရတာ လွယ်ကူပါတယ်။  

## git clone

အလွယ်ဆုံး installation လုပ်တာက ```pip install nagisa``` ဆိုပြီး command ပေးတဲ့ ပုံစံပါ။ ဒီနေရာမှာတော့ source ကို clone လုပ်ပြီး install လုပ်တဲ့ ပုံစံနဲ့ပဲ သွားရအောင်...  
အရင်ဆုံး git clone လုပ်ပြီး ကိုယ့်စက်ထဲကို source repository ကို download လုပ်ယူရအောင်။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ git clone https://github.com/taishi-i/nagisa
Cloning into 'nagisa'...
remote: Enumerating objects: 66, done.
remote: Counting objects: 100% (66/66), done.
remote: Compressing objects: 100% (50/50), done.
remote: Total 658 (delta 31), reused 44 (delta 16), pack-reused 592
Receiving objects: 100% (658/658), 40.37 MiB | 560.00 KiB/s, done.
Resolving deltas: 100% (401/401), done.
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ cd nagisa/
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/nagisa$ ls
appveyor.yml  docs  LICENSE.txt  MANIFEST.in  nagisa  README.md  setup.cfg  setup.py  test
```

## setup.py install

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/nagisa$ python setup.py install
running install
Compiling nagisa/nagisa_utils.pyx because it changed.
[1/1] Cythonizing nagisa/nagisa_utils.pyx
/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/Cython/Compiler/Main.py:369: FutureWarning: Cython directive 'language_level' not set, using 2 for now (Py2). This will change in a later release! File: /home/ye/tool/nagisa/nagisa/nagisa_utils.pyx
  tree = Parsing.p_module(s, pxd, full_module_name)
running bdist_egg
running egg_info
creating nagisa.egg-info
writing nagisa.egg-info/PKG-INFO
writing dependency_links to nagisa.egg-info/dependency_links.txt
writing requirements to nagisa.egg-info/requires.txt
writing top-level names to nagisa.egg-info/top_level.txt
writing manifest file 'nagisa.egg-info/SOURCES.txt'
reading manifest file 'nagisa.egg-info/SOURCES.txt'
reading manifest template 'MANIFEST.in'
writing manifest file 'nagisa.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
creating build
creating build/lib.linux-x86_64-3.6
creating build/lib.linux-x86_64-3.6/nagisa
copying nagisa/tagger.py -> build/lib.linux-x86_64-3.6/nagisa
copying nagisa/__init__.py -> build/lib.linux-x86_64-3.6/nagisa
copying nagisa/prepro.py -> build/lib.linux-x86_64-3.6/nagisa
copying nagisa/train.py -> build/lib.linux-x86_64-3.6/nagisa
copying nagisa/mecab_system_eval.py -> build/lib.linux-x86_64-3.6/nagisa
copying nagisa/model.py -> build/lib.linux-x86_64-3.6/nagisa
copying nagisa/nagisa_utils.c -> build/lib.linux-x86_64-3.6/nagisa
copying nagisa/nagisa_utils.pyx -> build/lib.linux-x86_64-3.6/nagisa
creating build/lib.linux-x86_64-3.6/nagisa/data
copying nagisa/data/models.jpg -> build/lib.linux-x86_64-3.6/nagisa/data
copying nagisa/data/nagisa_logo.png -> build/lib.linux-x86_64-3.6/nagisa/data
copying nagisa/data/nagisa_v001.dict -> build/lib.linux-x86_64-3.6/nagisa/data
copying nagisa/data/nagisa_v001.hp -> build/lib.linux-x86_64-3.6/nagisa/data
copying nagisa/data/nagisa_v001.model -> build/lib.linux-x86_64-3.6/nagisa/data
creating build/lib.linux-x86_64-3.6/nagisa/data/sample_datasets
copying nagisa/data/sample_datasets/sample.dev -> build/lib.linux-x86_64-3.6/nagisa/data/sample_datasets
copying nagisa/data/sample_datasets/sample.dict -> build/lib.linux-x86_64-3.6/nagisa/data/sample_datasets
copying nagisa/data/sample_datasets/sample.emb -> build/lib.linux-x86_64-3.6/nagisa/data/sample_datasets
copying nagisa/data/sample_datasets/sample.pred -> build/lib.linux-x86_64-3.6/nagisa/data/sample_datasets
copying nagisa/data/sample_datasets/sample.test -> build/lib.linux-x86_64-3.6/nagisa/data/sample_datasets
copying nagisa/data/sample_datasets/sample.train -> build/lib.linux-x86_64-3.6/nagisa/data/sample_datasets
running build_ext
building 'nagisa_utils' extension
creating build/temp.linux-x86_64-3.6
creating build/temp.linux-x86_64-3.6/nagisa
gcc -pthread -B /home/ye/anaconda3/envs/py3.6env/compiler_compat -Wl,--sysroot=/ -Wsign-compare -DNDEBUG -g -fwrapv -O3 -Wall -Wstrict-prototypes -fPIC -I/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/numpy/core/include -I/home/ye/anaconda3/envs/py3.6env/include/python3.6m -c nagisa/nagisa_utils.c -o build/temp.linux-x86_64-3.6/nagisa/nagisa_utils.o
gcc -pthread -shared -B /home/ye/anaconda3/envs/py3.6env/compiler_compat -L/home/ye/anaconda3/envs/py3.6env/lib -Wl,-rpath=/home/ye/anaconda3/envs/py3.6env/lib -Wl,--no-as-needed -Wl,--sysroot=/ build/temp.linux-x86_64-3.6/nagisa/nagisa_utils.o -o build/lib.linux-x86_64-3.6/nagisa_utils.cpython-36m-x86_64-linux-gnu.so
creating build/bdist.linux-x86_64
creating build/bdist.linux-x86_64/egg
creating build/bdist.linux-x86_64/egg/nagisa
copying build/lib.linux-x86_64-3.6/nagisa/tagger.py -> build/bdist.linux-x86_64/egg/nagisa
copying build/lib.linux-x86_64-3.6/nagisa/nagisa_utils.pyx -> build/bdist.linux-x86_64/egg/nagisa
copying build/lib.linux-x86_64-3.6/nagisa/nagisa_utils.c -> build/bdist.linux-x86_64/egg/nagisa
creating build/bdist.linux-x86_64/egg/nagisa/data
copying build/lib.linux-x86_64-3.6/nagisa/data/nagisa_v001.hp -> build/bdist.linux-x86_64/egg/nagisa/data
copying build/lib.linux-x86_64-3.6/nagisa/data/nagisa_v001.model -> build/bdist.linux-x86_64/egg/nagisa/data
creating build/bdist.linux-x86_64/egg/nagisa/data/sample_datasets
copying build/lib.linux-x86_64-3.6/nagisa/data/sample_datasets/sample.train -> build/bdist.linux-x86_64/egg/nagisa/data/sample_datasets
copying build/lib.linux-x86_64-3.6/nagisa/data/sample_datasets/sample.test -> build/bdist.linux-x86_64/egg/nagisa/data/sample_datasets
copying build/lib.linux-x86_64-3.6/nagisa/data/sample_datasets/sample.dict -> build/bdist.linux-x86_64/egg/nagisa/data/sample_datasets
copying build/lib.linux-x86_64-3.6/nagisa/data/sample_datasets/sample.pred -> build/bdist.linux-x86_64/egg/nagisa/data/sample_datasets
copying build/lib.linux-x86_64-3.6/nagisa/data/sample_datasets/sample.dev -> build/bdist.linux-x86_64/egg/nagisa/data/sample_datasets
copying build/lib.linux-x86_64-3.6/nagisa/data/sample_datasets/sample.emb -> build/bdist.linux-x86_64/egg/nagisa/data/sample_datasets
copying build/lib.linux-x86_64-3.6/nagisa/data/nagisa_logo.png -> build/bdist.linux-x86_64/egg/nagisa/data
copying build/lib.linux-x86_64-3.6/nagisa/data/models.jpg -> build/bdist.linux-x86_64/egg/nagisa/data
copying build/lib.linux-x86_64-3.6/nagisa/data/nagisa_v001.dict -> build/bdist.linux-x86_64/egg/nagisa/data
copying build/lib.linux-x86_64-3.6/nagisa/__init__.py -> build/bdist.linux-x86_64/egg/nagisa
copying build/lib.linux-x86_64-3.6/nagisa/prepro.py -> build/bdist.linux-x86_64/egg/nagisa
copying build/lib.linux-x86_64-3.6/nagisa/train.py -> build/bdist.linux-x86_64/egg/nagisa
copying build/lib.linux-x86_64-3.6/nagisa/mecab_system_eval.py -> build/bdist.linux-x86_64/egg/nagisa
copying build/lib.linux-x86_64-3.6/nagisa/model.py -> build/bdist.linux-x86_64/egg/nagisa
copying build/lib.linux-x86_64-3.6/nagisa_utils.cpython-36m-x86_64-linux-gnu.so -> build/bdist.linux-x86_64/egg
byte-compiling build/bdist.linux-x86_64/egg/nagisa/tagger.py to tagger.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/nagisa/__init__.py to __init__.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/nagisa/prepro.py to prepro.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/nagisa/train.py to train.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/nagisa/mecab_system_eval.py to mecab_system_eval.cpython-36.pyc
byte-compiling build/bdist.linux-x86_64/egg/nagisa/model.py to model.cpython-36.pyc
creating stub loader for nagisa_utils.cpython-36m-x86_64-linux-gnu.so
byte-compiling build/bdist.linux-x86_64/egg/nagisa_utils.py to nagisa_utils.cpython-36.pyc
creating build/bdist.linux-x86_64/egg/EGG-INFO
copying nagisa.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying nagisa.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying nagisa.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying nagisa.egg-info/requires.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying nagisa.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
writing build/bdist.linux-x86_64/egg/EGG-INFO/native_libs.txt
zip_safe flag not set; analyzing archive contents...
__pycache__.nagisa_utils.cpython-36: module references __file__
nagisa.__pycache__.tagger.cpython-36: module references __file__
creating dist
creating 'dist/nagisa-0.2.7-py3.6-linux-x86_64.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing nagisa-0.2.7-py3.6-linux-x86_64.egg
creating /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/nagisa-0.2.7-py3.6-linux-x86_64.egg
Extracting nagisa-0.2.7-py3.6-linux-x86_64.egg to /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Adding nagisa 0.2.7 to easy-install.pth file

Installed /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/nagisa-0.2.7-py3.6-linux-x86_64.egg
Processing dependencies for nagisa==0.2.7
Searching for DyNet
Reading https://pypi.org/simple/DyNet/
Downloading https://files.pythonhosted.org/packages/9d/73/b5435275aa9b00f21a7aa7f50bb476a3768d6c0b9cfffde09b39035a7019/dyNET-2.1.2-cp36-cp36m-manylinux1_x86_64.whl#sha256=e55fde2fd703a4e5f736ae7e691a042967eed7b7aae4921035d4273b64132817
Best match: dyNET 2.1.2
Processing dyNET-2.1.2-cp36-cp36m-manylinux1_x86_64.whl
Installing dyNET-2.1.2-cp36-cp36m-manylinux1_x86_64.whl to /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Adding dyNET 2.1.2 to easy-install.pth file

Installed /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/dyNET-2.1.2-py3.6-linux-x86_64.egg
Searching for numpy==1.19.4
Best match: numpy 1.19.4
Adding numpy 1.19.4 to easy-install.pth file
Installing f2py script to /home/ye/anaconda3/envs/py3.6env/bin
Installing f2py3 script to /home/ye/anaconda3/envs/py3.6env/bin
Installing f2py3.6 script to /home/ye/anaconda3/envs/py3.6env/bin

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for six==1.15.0
Best match: six 1.15.0
Adding six 1.15.0 to easy-install.pth file

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Searching for Cython==0.29.22
Best match: Cython 0.29.22
Adding Cython 0.29.22 to easy-install.pth file
Installing cygdb script to /home/ye/anaconda3/envs/py3.6env/bin
Installing cython script to /home/ye/anaconda3/envs/py3.6env/bin
Installing cythonize script to /home/ye/anaconda3/envs/py3.6env/bin

Using /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages
Finished processing dependencies for nagisa==0.2.7
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/nagisa$
```

## Example Usage

Nagisa ရဲ့ GitHub source မှာ ပြထားတဲ့ example usage ကိုပဲ ကိုယ့်စက်ထဲမှာ ဂျပန်စာကြောင်း အသစ်တစ်ကြောင်းနဲ့ လက်တွေ့ လုပ်ကြည့်ရအောင်...  
ဥပမာအဖြစ် သုံးပြထားတဲ့ ဂျပန်စာကြောင်း တစ်ကြောင်းကတော့ NHK Japan ရဲ့ ဒီနေ့ (29 Mar 2021) မြန်မာနိုင်ငံနဲ့ ပတ်သက်တဲ့ ဆောင်းပါးတစ်ပုဒ်ထဲကနေပဲ ယူလိုက်တာပါ။ အောက်မှာ link ထည့်ပေးထားပါတယ်။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/nagisa$ python
Python 3.6.12 |Anaconda, Inc.| (default, Sep  8 2020, 23:10:56) 
[GCC 7.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import nagisa
[dynet] random seed: 1234
[dynet] allocating memory: 32MB
[dynet] memory allocation done.
>>> text = 'ミャンマーでは、軍による市民への弾圧が、国際社会から激しく非難されている中でも軍は弾圧を一段と強め、市民に加勢する少数民族の武装勢力に対して、3日連続で空爆を行いました。'
>>> words = nagisa.tagging(text)
>>> print(words)
ミャンマー/名詞 で/助詞 は/助詞 、/補助記号 軍/名詞 に/助詞 よる/動詞 市民/名詞 へ/助詞 の/助詞 弾圧/名詞 が/助詞 、/補助記号 国際/名詞 社会/名詞 から/助詞 激しく/形容詞 非難/名詞 さ/動詞 れ/助動詞 て/助詞 いる/動詞 中/名詞 で/助詞 も/助詞 軍/名詞 は/助詞 弾圧/名詞 を/助詞 一段/名詞 と/助詞 強め/動詞 、/補助記号 市民/名詞 に/助詞 加勢/名詞 する/動詞 少数/名詞 民族/名詞 の/助詞 武装/名詞 勢力/名詞 に/助詞 対し/動詞 て/助詞 、/補助記号 3/名詞 日/接尾辞 連続/名詞 で/助詞 空爆/名詞 を/助詞 行い/動詞 まし/助動詞 た/助動詞 。/補助記号
>>> print(words.word)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: '_Token' object has no attribute 'word'
>>> print(words.words)
['ミャンマー', 'で', 'は', '、', '軍', 'に', 'よる', '市民', 'へ', 'の', '弾圧', 'が', '、', '国際', '社会', 'から', '激しく', '非難', 'さ', 'れ', 'て', 'いる', '中', 'で', 'も', '軍', 'は', '弾圧', 'を', '一段', 'と', '強め', '、', '市民', 'に', '加勢', 'する', '少数', '民族', 'の', '武装', '勢力', 'に', '対し', 'て', '、', '3', '日', '連続', 'で', '空爆', 'を', '行い', 'まし', 'た', '。']
>>> print(words.postags)
['名詞', '助詞', '助詞', '補助記号', '名詞', '助詞', '動詞', '名詞', '助詞', '助詞', '名詞', '助詞', '補助記号', '名詞', '名詞', '助詞', '形容詞', '名詞', '動詞', '助動詞', '助詞', '動詞', '名詞', '助詞', '助詞', '名詞', '助詞', '名詞', '助詞', '名詞', '助詞', '動詞', '補助記号', '名詞', '助詞', '名詞', '動詞', '名詞', '名詞', '助詞', '名詞', '名詞', '助詞', '動詞', '助詞', '補助記号', '名詞', '接尾辞', '名詞', '助詞', '名詞', '助詞', '動詞', '助動詞', '助動詞', '補助記号']
>>> words = nagisa.filter(text, filter_postags=['助詞', '助動詞'])
>>> print(words)
ミャンマー/名詞 、/補助記号 軍/名詞 よる/動詞 市民/名詞 弾圧/名詞 、/補助記号 国際/名詞 社会/名詞 激しく/形容詞 非難/名詞 さ/動詞 いる/動詞 中/名詞 軍/名詞 弾圧/名詞 一段/名詞 強め/動詞 、/補助記号 市民/名詞 加勢/名詞 する/動詞 少数/名詞 民族/名詞 武装/名詞 勢力/名詞 対し/動詞 、/補助記号 3/名詞 日/接尾辞 連続/名詞 空爆/名詞 行い/動詞 。/補助記号
>>> words = nagisa.extract(text, extract_postags=['名詞'])
>>> print(words)
ミャンマー/名詞 軍/名詞 市民/名詞 弾圧/名詞 国際/名詞 社会/名詞 非難/名詞 中/名詞 軍/名詞 弾圧/名詞 一段/名詞 市民/名詞 加勢/名詞 少数/名詞 民族/名詞 武装/名詞 勢力/名詞 3/名詞 連続/名詞 空爆/名詞
>>> print(nagisa.tagger.postags)
['oov', '補助記号', '名詞', '空白', '助詞', '接尾辞', '動詞', '連体詞', '助動詞', '形容詞', '感動詞', '接頭辞', '記号', '接続詞', '副詞', '代名詞', '形状詞', 'web誤脱', 'URL', '英単語', '漢文', '未知語', '言いよどみ', 'ローマ字文']
>>> 
```

## Reference

1. GitHub Link of Nagisa:  
https://github.com/taishi-i/nagisa  

2. ミャンマー軍 市民に加勢の武装勢力に3日連続空爆 弾圧強める (2021年3月29日 19時34分)  
https://www3.nhk.or.jp/news/html/20210329/k10012943191000.html

