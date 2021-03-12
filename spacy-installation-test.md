### Installation Spacy Python Library and Testing for English Word Segmentation

မြန်မာနိုင်ငံရဲ့ လက်ရှိ နိုင်ငံရေး အခြေအနေရ တကယ်တမ်း experiment တွေက အချိန်မှီပြီးစီးနိုင်မလားဆိုတာက ခန့်မှန်းလို့မရပေမဲ့ WAT-2021 ရဲ့ Myanmar-English, English-Myanmar machine translation share task အတွက် ပြင်ဆင်စရာရှိတာတွေကို ဆက်လက် ပြင်ဆင်နေပါတယ်။ အခု post က အဲဒီ share task အတွက် data preparation အပိုင်းထဲက တစ်ပိုင်းပါ။ အတိုပြောရရင် UCSY ရဲ့ မြန်မာစာ training data က word segmentation လုပ်မထားပါဘူး။ ဗမာစာစာလုံးဖြတ်ဖို့အတွက် word segmenter ကို သပ်သပ် develop လုပ်ခဲ့ပေမဲ့၊ ဗမာစာထဲမှာရောပြီးပါနေတဲ့ အင်္ဂလိပ်စာစာလုံးတွေပါ အောက်ပါအတိုင်း အားလုံး ပူးနေတာမို့၊ အဲဒီ အင်္ဂလိပ်စာလုံးတွေကို ဆွဲထုတ်ပြီး word segmentation လုပ်ဖို့အတွက် Spacy Python Library နဲ့ English word segmentation ကို စမ်းထားတုန်း မှတ်ထားတဲ့ installation note ပါ။   

```text
SeesaengKanyothaကုမ္ပဏီကဝန်ထမ်းသာဝပါ။
ဟုတ်လား။ငါကမင်းကိုရုံးကိုခဏခဏလာနေတဲ့JapanThilawaDevelopmentLtd.ကလို့ထင်တာ။
ကားဆရာရေParkTramstationကိုမောင်းခိုင်းမလို့၊ဒီကနေဆိုရင်တော်တော်ဝေးတာမို့ဘယ်လောက်လောက်ပိုက်ဆံပေးရမှာလည်းဆိုတာကိုခန့်မှန်းပေးလို့ရမလား။
GreentaxiServiceကကားကိုပဲခေါ်ပေးပါရှင့်။
ကျွန်မရဲ့အီးမေးလ်လိပ်စာကရိုက်ရမယ့်နေရာမှာတော့thailand@gmail.comဆိုပြီးရိုက်ထည့်ပေးပါ။
Anthory’sPipistrelleနှင့်Ioffre’sPipistrelleဆိုတာကလင်းနို့မျိုးစိတ်နာမည်တွေပါခင်ဗျာ။
```

CopyRight ဘာညာအတွက် အင်္ဂလိပ်စာလုံးကိုပဲ UCSY corpus ထဲက ဥပမာအနေနဲ့ ယူထားပေမဲ့ ဗမာစာကြောင်းတွေကတော့ အစားထိုးပြထားတာပါ။  


## Install Spacy Library

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ python
Python 3.7.6 (default, Jan  8 2020, 19:59:22) 
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import spacy
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'spacy'
>>> exit()
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ pip install -U spacy
Collecting spacy
  Downloading spacy-3.0.5-cp37-cp37m-manylinux2014_x86_64.whl (12.8 MB)
     |████████████████████████████████| 12.8 MB 665 kB/s 
Collecting murmurhash<1.1.0,>=0.28.0
  Downloading murmurhash-1.0.5-cp37-cp37m-manylinux2014_x86_64.whl (20 kB)
Requirement already satisfied, skipping upgrade: jinja2 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy) (2.11.1)
Requirement already satisfied, skipping upgrade: importlib-metadata>=0.20; python_version < "3.8" in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy) (1.5.0)
Requirement already satisfied, skipping upgrade: requests<3.0.0,>=2.13.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy) (2.22.0)
Collecting preshed<3.1.0,>=3.0.2
  Downloading preshed-3.0.5-cp37-cp37m-manylinux2014_x86_64.whl (126 kB)
     |████████████████████████████████| 126 kB 860 kB/s 
Collecting spacy-legacy<3.1.0,>=3.0.0
  Downloading spacy_legacy-3.0.1-py2.py3-none-any.whl (7.0 kB)
Collecting catalogue<2.1.0,>=2.0.1
  Downloading catalogue-2.0.1-py3-none-any.whl (9.6 kB)
Requirement already satisfied, skipping upgrade: packaging>=20.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy) (20.1)
Collecting pathy>=0.3.5
  Downloading pathy-0.4.0-py3-none-any.whl (36 kB)
Collecting wasabi<1.1.0,>=0.8.1
  Downloading wasabi-0.8.2-py3-none-any.whl (23 kB)
Requirement already satisfied, skipping upgrade: numpy>=1.15.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy) (1.18.1)
Requirement already satisfied, skipping upgrade: setuptools in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy) (45.2.0.post20200210)
Collecting thinc<8.1.0,>=8.0.2
  Downloading thinc-8.0.2-cp37-cp37m-manylinux2014_x86_64.whl (1.1 MB)
     |████████████████████████████████| 1.1 MB 514 kB/s 
Collecting blis<0.8.0,>=0.4.0
  Downloading blis-0.7.4-cp37-cp37m-manylinux2014_x86_64.whl (9.8 MB)
     |████████████████████████████████| 9.8 MB 598 kB/s 
Collecting cymem<2.1.0,>=2.0.2
  Downloading cymem-2.0.5-cp37-cp37m-manylinux2014_x86_64.whl (35 kB)
Requirement already satisfied, skipping upgrade: typing-extensions<4.0.0.0,>=3.7.4; python_version < "3.8" in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy) (3.7.4.3)
Collecting pydantic<1.8.0,>=1.7.1
  Downloading pydantic-1.7.3-cp37-cp37m-manylinux2014_x86_64.whl (9.1 MB)
     |████████████████████████████████| 9.1 MB 897 kB/s 
Collecting typer<0.4.0,>=0.3.0
  Downloading typer-0.3.2-py3-none-any.whl (21 kB)
Collecting srsly<3.0.0,>=2.4.0
  Downloading srsly-2.4.0-cp37-cp37m-manylinux2014_x86_64.whl (456 kB)
     |████████████████████████████████| 456 kB 116 kB/s 
Requirement already satisfied, skipping upgrade: tqdm<5.0.0,>=4.38.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy) (4.56.0)
Requirement already satisfied, skipping upgrade: MarkupSafe>=0.23 in /home/ye/anaconda3/lib/python3.7/site-packages (from jinja2->spacy) (1.1.1)
Requirement already satisfied, skipping upgrade: zipp>=0.5 in /home/ye/anaconda3/lib/python3.7/site-packages (from importlib-metadata>=0.20; python_version < "3.8"->spacy) (2.2.0)
Requirement already satisfied, skipping upgrade: certifi>=2017.4.17 in /home/ye/anaconda3/lib/python3.7/site-packages (from requests<3.0.0,>=2.13.0->spacy) (2019.11.28)
Requirement already satisfied, skipping upgrade: idna<2.9,>=2.5 in /home/ye/anaconda3/lib/python3.7/site-packages (from requests<3.0.0,>=2.13.0->spacy) (2.8)
Requirement already satisfied, skipping upgrade: urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 in /home/ye/anaconda3/lib/python3.7/site-packages (from requests<3.0.0,>=2.13.0->spacy) (1.25.8)
Requirement already satisfied, skipping upgrade: chardet<3.1.0,>=3.0.2 in /home/ye/anaconda3/lib/python3.7/site-packages (from requests<3.0.0,>=2.13.0->spacy) (3.0.4)
Requirement already satisfied, skipping upgrade: six in /home/ye/anaconda3/lib/python3.7/site-packages (from packaging>=20.0->spacy) (1.14.0)
Requirement already satisfied, skipping upgrade: pyparsing>=2.0.2 in /home/ye/anaconda3/lib/python3.7/site-packages (from packaging>=20.0->spacy) (2.4.6)
Collecting smart-open<4.0.0,>=2.2.0
  Downloading smart_open-3.0.0.tar.gz (113 kB)
     |████████████████████████████████| 113 kB 510 kB/s 
Collecting click<7.2.0,>=7.1.1
  Downloading click-7.1.2-py2.py3-none-any.whl (82 kB)
     |████████████████████████████████| 82 kB 460 kB/s 
Building wheels for collected packages: smart-open
  Building wheel for smart-open (setup.py) ... done
  Created wheel for smart-open: filename=smart_open-3.0.0-py3-none-any.whl size=107097 sha256=7d35c816a0edef08292b9e44b21e7dfece936af0d157b9e1b295a2ca1e923a08
  Stored in directory: /home/ye/.cache/pip/wheels/83/a6/12/bf3c1a667bde4251be5b7a3368b2d604c9af2105b5c1cb1870
Successfully built smart-open
Installing collected packages: murmurhash, cymem, preshed, spacy-legacy, catalogue, smart-open, click, typer, pathy, wasabi, pydantic, srsly, blis, thinc, spacy
  Attempting uninstall: click
    Found existing installation: Click 7.0
    Uninstalling Click-7.0:
      Successfully uninstalled Click-7.0
Successfully installed blis-0.7.4 catalogue-2.0.1 click-7.1.2 cymem-2.0.5 murmurhash-1.0.5 pathy-0.4.0 preshed-3.0.5 pydantic-1.7.3 smart-open-3.0.0 spacy-3.0.5 spacy-legacy-3.0.1 srsly-2.4.0 thinc-8.0.2 typer-0.3.2 wasabi-0.8.2
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$
```

## If you don't have downloaded trained pipeline

Spacy library ကို install လုပ်ယုံနဲ့က word segmentation တန်းလုပ်လို့ မရသေးပါဘူး။ အောက်ပါအတိုင်း error ပေးပါလိမ့်မယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ python
Python 3.7.6 (default, Jan  8 2020, 19:59:22) 
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import spacy
>>> nlp = spacy.load("en_core_web_sm")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/home/ye/anaconda3/lib/python3.7/site-packages/spacy/__init__.py", line 47, in load
    return util.load_model(name, disable=disable, exclude=exclude, config=config)
  File "/home/ye/anaconda3/lib/python3.7/site-packages/spacy/util.py", line 329, in load_model
    raise IOError(Errors.E050.format(name=name))
OSError: [E050] Can't find model 'en_core_web_sm'. It doesn't seem to be a Python package or a valid path to a data directory.
>>> exit()
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$
```

## Download

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/word-seg-tool/spacy$ python -m spacy download en_core_web_sm
Collecting en-core-web-sm==3.0.0
  Downloading https://github.com/explosion/spacy-models/releases/download/en_core_web_sm-3.0.0/en_core_web_sm-3.0.0-py3-none-any.whl (13.7 MB)
     |████████████████████████████████| 13.7 MB 689 kB/s 
Requirement already satisfied: spacy<3.1.0,>=3.0.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from en-core-web-sm==3.0.0) (3.0.5)
Requirement already satisfied: packaging>=20.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (20.1)
Requirement already satisfied: setuptools in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (45.2.0.post20200210)
Requirement already satisfied: thinc<8.1.0,>=8.0.2 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (8.0.2)
Requirement already satisfied: pathy>=0.3.5 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (0.4.0)
Requirement already satisfied: typer<0.4.0,>=0.3.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (0.3.2)
Requirement already satisfied: wasabi<1.1.0,>=0.8.1 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (0.8.2)
Requirement already satisfied: cymem<2.1.0,>=2.0.2 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (2.0.5)
Requirement already satisfied: murmurhash<1.1.0,>=0.28.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (1.0.5)
Requirement already satisfied: spacy-legacy<3.1.0,>=3.0.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (3.0.1)
Requirement already satisfied: jinja2 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (2.11.1)
Requirement already satisfied: numpy>=1.15.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (1.18.1)
Requirement already satisfied: preshed<3.1.0,>=3.0.2 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (3.0.5)
Requirement already satisfied: typing-extensions<4.0.0.0,>=3.7.4; python_version < "3.8" in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (3.7.4.3)
Requirement already satisfied: importlib-metadata>=0.20; python_version < "3.8" in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (1.5.0)
Requirement already satisfied: requests<3.0.0,>=2.13.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (2.22.0)
Requirement already satisfied: tqdm<5.0.0,>=4.38.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (4.56.0)
Requirement already satisfied: catalogue<2.1.0,>=2.0.1 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (2.0.1)
Requirement already satisfied: pydantic<1.8.0,>=1.7.1 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (1.7.3)
Requirement already satisfied: blis<0.8.0,>=0.4.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (0.7.4)
Requirement already satisfied: srsly<3.0.0,>=2.4.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (2.4.0)
Requirement already satisfied: six in /home/ye/anaconda3/lib/python3.7/site-packages (from packaging>=20.0->spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (1.14.0)
Requirement already satisfied: pyparsing>=2.0.2 in /home/ye/anaconda3/lib/python3.7/site-packages (from packaging>=20.0->spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (2.4.6)
Requirement already satisfied: smart-open<4.0.0,>=2.2.0 in /home/ye/anaconda3/lib/python3.7/site-packages (from pathy>=0.3.5->spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (3.0.0)
Requirement already satisfied: click<7.2.0,>=7.1.1 in /home/ye/anaconda3/lib/python3.7/site-packages (from typer<0.4.0,>=0.3.0->spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (7.1.2)
Requirement already satisfied: MarkupSafe>=0.23 in /home/ye/anaconda3/lib/python3.7/site-packages (from jinja2->spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (1.1.1)
Requirement already satisfied: zipp>=0.5 in /home/ye/anaconda3/lib/python3.7/site-packages (from importlib-metadata>=0.20; python_version < "3.8"->spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (2.2.0)
Requirement already satisfied: chardet<3.1.0,>=3.0.2 in /home/ye/anaconda3/lib/python3.7/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (3.0.4)
Requirement already satisfied: urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 in /home/ye/anaconda3/lib/python3.7/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (1.25.8)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/anaconda3/lib/python3.7/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (2019.11.28)
Requirement already satisfied: idna<2.9,>=2.5 in /home/ye/anaconda3/lib/python3.7/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.1.0,>=3.0.0->en-core-web-sm==3.0.0) (2.8)
Installing collected packages: en-core-web-sm
Successfully installed en-core-web-sm-3.0.0
✔ Download and installation successful
You can now load the package via spacy.load('en_core_web_sm')
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/word-seg-tool/spacy$
```

## Testing with Example Program

Reference link က ယူလာတဲ့ python code နဲ့ အင်္ဂလိပ်စာလုံးဖြတ်ကြည့်တာ အို
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/word-seg-tool/spacy$ python ./test.py 
Noun phrases: ['Sebastian Thrun', 'self-driving cars', 'Google', 'few people', 'the company', 'him', 'I', 'you', 'very senior CEOs', 'major American car companies', 'my hand', 'I', 'Thrun', 'an interview', 'Recode']
Verbs: ['start', 'work', 'drive', 'take', 'tell', 'shake', 'turn', 'be', 'talk', 'say']
Sebastian Thrun PERSON
2007 DATE
American NORP
Thrun PERSON
Recode PERSON
earlier this week DATE
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/word-seg-tool/spacy$
```

## Testing for English Word Segmentation

### Case 1:

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/word-seg-tool/spacy$ cat tokenization.py 
import spacy

nlp = spacy.load("en_core_web_sm")
doc = nlp("It has been confirmed that eight thoroughbred race horses at Randwick Racecourse in Sydney have been infected with equine influenza . Randwick has been locked down , and is expected to remain so for up to two months .")

for token in doc:
    print(token.text, token.pos_, token.dep_)
    
    
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/word-seg-tool/spacy$ python ./tokenization.py 
It PRON nsubjpass
has AUX aux
been AUX auxpass
confirmed VERB ROOT
that SCONJ mark
eight NUM nummod
thoroughbred ADJ amod
race NOUN compound
horses NOUN nsubjpass
at ADP prep
Randwick PROPN compound
Racecourse PROPN pobj
in ADP prep
Sydney PROPN pobj
have AUX aux
been AUX auxpass
infected VERB ccomp
with ADP prep
equine NOUN compound
influenza NOUN pobj
. PUNCT punct
Randwick PROPN nsubjpass
has AUX aux
been AUX auxpass
locked VERB ROOT
down ADP prt
, PUNCT punct
and CCONJ cc
is AUX auxpass
expected VERB conj
to PART aux
remain VERB xcomp
so ADV advmod
for ADP prep
up ADP quantmod
to PART quantmod
two NUM nummod
months NOUN pobj
. PUNCT punct
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/word-seg-tool/spacy$
```

### Case 2:

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/word-seg-tool/spacy$ cat ./tokenization.py 
import spacy

nlp = spacy.load("en_core_web_sm")
doc = nlp("IthasbeenconfirmedthateightthoroughbredracehorsesatRandwickRacecourseinSydneyhavebeeninfectedwithequineinfluenza.Randwickhasbeenlockeddown,andisexpectedtoremainsofor uptotwomonths.")
for token in doc:
    print(token.text, token.pos_, token.dep_)
    
    
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/word-seg-tool/spacy$ python ./tokenization.py 
IthasbeenconfirmedthateightthoroughbredracehorsesatRandwickRacecourseinSydneyhavebeeninfectedwithequineinfluenza NOUN ROOT
. PUNCT punct
Randwickhasbeenlockeddown ADJ ROOT
, PUNCT punct
andisexpectedtoremainsofor NOUN prep
uptotwomonths NOUN pobj
. PUNCT punct
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/word-seg-tool/spacy$
```

## Reference

https://spacy.io/
https://spacy.io/usage/spacy-101
