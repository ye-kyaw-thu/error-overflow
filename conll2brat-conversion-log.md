# conll2brat Conversion Log

ကျောင်းသူ ဇာဇာလှိုင် (Ph.D. candidate, KMITL, Thailand) အတွက် စမ်းကြည့်ခဲ့တဲ့ log ဖိုင်ပါ။  
သူ conversion အလုပ်အတွက် သုံးထားတဲ့ tool ကို installation လုပ်တဲ့အဆင့်ကနေ နောက်ဆုံး brat editor နဲ့ အဆင်ပြေပြေနဲ့ ဖွင့်ကြည့်လို့ ရဖို့အတွက် configuration ဖိုင်ကိုပါ ဆောက်ကြည့်ခဲ့တယ်။  

## CoNLL Format

wc နဲ့ ကြည့်ရင် စာကြောင်းရေ 20358 (နှစ်သောင်းကျော်) ရှိသလို မြင်ရပေမဲ့ ...  
```
$ wc ./test.conllu 
  20358  203086 1260932 ./test.conllu
```

CoNLL format အတိုင်း ရိုက်ထည့်ထားတာမို့ ဖိုင်ထဲမှာက အောက်ပါအတိုင်း ရှိနေတာမို့...  

```
$ head test.conllu 
# sent_id = 1
# text = ကိန်းဂဏန်း တွေ နဲ့ address အစား အက်ခရာ များ နဲ့ address ကို သုံး ခြင်း ဖြင့် Internet သုံးစွဲ သူ များ အနေနဲ့ website များ နဲ့ server based ဝန်ဆောင် မှု များ ကို လွယ်လွယ်ကူကူ ရှာဖွေ တွေ့ ရှိ နိုင် ပါ တယ် ။
1	ကိန်းဂဏန်း	ကိန်းဂဏန်း	NOUN	N	_	4	obl	_	_
2	တွေ	တွေ	PART	PART	_	1	case	_	_
3	နဲ့	နဲ့	PART	PART	_	1	case	_	_
4	address	address	NOUN	FOR	_	6	compound	_	_
5	အစား	အစား	NOUN	N	_	6	compound	_	_
6	အက်ခရာ	အက်ခရာ	NOUN	N	_	9	obl	_	_
7	များ	များ	PART	PART	_	6	case	_	_
8	နဲ့	နဲ့	PART	PART	_	6	case	_	_
```

```
$ tail ./test.conllu 
3	ငှက်	ငှက်	NOUN	N	_	9	obl	_	_
4	တို့	တို့	PART	PART	_	3	case	_	_
5	သည်	သည်	ADP	PPM	_	3	case	_	_
6	ဟင်းလျာ	ဟင်းလျာ	NOUN	N	_	9	obl	_	_
7	အတွက်	အတွက်	ADP	PPM	_	6	case	_	_
8	လည်း	လည်း	PART	PART	_	6	case	_	_
9	အသုံးဝင်	အသုံးဝင်	VERB	V	_	0	root	_	_
10	သည်	သည်	ADP	PPM	_	9	case	_	SpaceAfter=No
11	။	။	PUNCT	PUNC	_	9	punct	_	_

```

တကယ်တမ်း test data ဖိုင်က လိုင်းအရေအတွက် စုစုပေါင်း ရှစ်ရာကျော်ပဲ ရှိပါတယ်။  

```
$ grep sent_id ./test.conllu | tail -n 1
# sent_id = 802
```

## Tool Installation

Reference Link: https://github.com/cdli-gh/conllu.py  

အရင်ဆုံး python 2 နဲ့ ရေးထားတာမို့ python2.7 environment ကို conda command နဲ့ ပြောင်းခဲ့တယ်  

```
(base) ye@:/media/ye/project2/data/myDep$ conda activate py2.7env
```

Installation ကို အောက်ပါအတိုင်း လုပ်တယ်...  

```
(py2.7env) ye@:/media/ye/project2/data/myDep$ pip install git+https://github.com/cdli-gh/conllu.py.git
DEPRECATION: Python 2.7 reached the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 is no longer maintained. pip 21.0 will drop support for Python 2.7 in January 2021. More details about Python 2 support in pip can be found at https://pip.pypa.io/en/latest/development/release-process/#python-2-support pip 21.0 will remove support for this functionality.
Collecting git+https://github.com/cdli-gh/conllu.py.git
  Cloning https://github.com/cdli-gh/conllu.py.git to /tmp/pip-req-build-JyxoF7
  Running command git clone -q https://github.com/cdli-gh/conllu.py.git /tmp/pip-req-build-JyxoF7
Collecting click
  Using cached click-7.1.2-py2.py3-none-any.whl (82 kB)
Building wheels for collected packages: conllu.py
  Building wheel for conllu.py (setup.py) ... done
  Created wheel for conllu.py: filename=conllu.py-0.0.3-py2-none-any.whl size=9866 sha256=108781996accc846c1395f79d35905f77315bedea71d0b27419d8896cda1d212
  Stored in directory: /tmp/pip-ephem-wheel-cache-0hhkAC/wheels/ec/54/f7/45d31d5253ffe13a30ab243ece490ceffed49b2d11afa7fbb9
Successfully built conllu.py
Installing collected packages: click, conllu.py
Successfully installed click-7.1.2 conllu.py-0.0.3
```

upgrade ကို အောက်ပါအတိုင်း လုပ်ခဲ့တယ်...  

```
(py2.7env) ye@:/media/ye/project2/data/myDep$ pip install git+https://github.com/cdli-gh/conllu.py.git --upgrade
DEPRECATION: Python 2.7 reached the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 is no longer maintained. pip 21.0 will drop support for Python 2.7 in January 2021. More details about Python 2 support in pip can be found at https://pip.pypa.io/en/latest/development/release-process/#python-2-support pip 21.0 will remove support for this functionality.
Collecting git+https://github.com/cdli-gh/conllu.py.git
  Cloning https://github.com/cdli-gh/conllu.py.git to /tmp/pip-req-build-7SE4Rb
  Running command git clone -q https://github.com/cdli-gh/conllu.py.git /tmp/pip-req-build-7SE4Rb
Requirement already satisfied, skipping upgrade: click in /home/ye/anaconda3/envs/py2.7env/lib/python2.7/site-packages (from conllu.py==0.0.3) (7.1.2)
Building wheels for collected packages: conllu.py
  Building wheel for conllu.py (setup.py) ... done
  Created wheel for conllu.py: filename=conllu.py-0.0.3-py2-none-any.whl size=9866 sha256=b2d9dfa572468387fe9bb562ac9869094ff8959b2015e43a60e3150713c679a4
  Stored in directory: /tmp/pip-ephem-wheel-cache-M2h3E8/wheels/ec/54/f7/45d31d5253ffe13a30ab243ece490ceffed49b2d11afa7fbb9
Successfully built conllu.py
Installing collected packages: conllu.py
  Attempting uninstall: conllu.py
    Found existing installation: conllu.py 0.0.3
    Uninstalling conllu.py-0.0.3:
      Successfully uninstalled conllu.py-0.0.3
Successfully installed conllu.py-0.0.3
(py2.7env) ye@:/media/ye/project2/data/myDep$
```

call help  

```
(py2.7env) ye@:/media/ye/project2/data/myDep$ conllu2brat --help
Usage: conllu2brat [OPTIONS]

Options:
  -i, --input_path PATH  Input the file/folder name.  [required]
  -v, --verbose          Enables verbose mode
  --version              Show the version and exit.
  --help                 Show this message and exit.
(py2.7env) ye@:/media/ye/project2/data/myDep$
```

## Conversion

CoNLL format ကနေ brat format ကို ပြောင်းကြည့်ရအောင်...  

```
(py2.7env) ye@:/media/ye/project2/data/myDep$ time conllu2brat -i ./tst/

Info: Correctly processed ./tst/test.conllu.
Info: Converting the files  [####################################]  100%

real	0m0.679s
user	0m0.633s
sys	0m0.044s
(py2.7env) ye@:/media/ye/project2/data/myDep$ 
```

## Check the Converted Output Files

./output/ ဆိုတဲ့ folder အောက်မှာ brat format ပြောင်းပြီးသား ဖိုင်တွေကို သိမ်းပေးတယ်။  

```
(py2.7env) ye@:/media/ye/project2/data/myDep$ ls ./output/
test.ann  test.txt
```

format ကို confirm လုပ်ကြည့်ရအောင်...  

```
(py2.7env) ye@:/media/ye/project2/data/myDep$ head ./output/test.ann 
T1.1	NOUN 0 10	ကိန်းဂဏန်း
R1.1-1	obl Arg1:T1.4 Arg2:T1.1
#1.1	AnnotatorNotes T1.1	LEMMA=ကိန်းဂဏန်း POSTAG=N
T1.2	PART 11 14	တွေ
R1.2-1	case Arg1:T1.1 Arg2:T1.2
#1.2	AnnotatorNotes T1.2	LEMMA=တွေ POSTAG=PART
T1.3	PART 15 18	နဲ့
R1.3-1	case Arg1:T1.1 Arg2:T1.3
#1.3	AnnotatorNotes T1.3	LEMMA=နဲ့ POSTAG=PART
T1.4	NOUN 19 26	address
```

test.txt ဖိုင်ကိုလည်း check လုပ်ကြည့်ရအောင်...  

```
(py2.7env) ye@:/media/ye/project2/data/myDep$ head ./output/test.txt 
ကိန်းဂဏန်း တွေ နဲ့ address အစား အက်ခရာ များ နဲ့ address ကို သုံး ခြင်း ဖြင့် Internet သုံးစွဲ သူ များ အနေနဲ့ website များ နဲ့ server based ဝန်ဆောင် မှု များ ကို လွယ်လွယ်ကူကူ ရှာဖွေ တွေ့ ရှိ နိုင် ပါ တယ် ။
တိုင်းရင်းသား မျိုးနွယ်စု များ အနက် ခရစ်ယာန် ယုံကြည် ကိုးကွယ် မှု ကို အရှေ့တောင် ဒေသ ရှိ ကရင် လူမျိုး များ တွင် လည်းကောင်း ၊ မြောက် ဘက် အရပ် နှင့် အနောက်မြောက် ဒေသ ၌ ကချင် လူမျိုး နှင့် ချင်း လူမျိုး တိုင်းရင်းသား များ တွင် လည်းကောင်း မြင် တွေ့ နိုင် သည် ။
ဘက်စ်ကား မှတ်တိုင် ဘယ် မှာ ရှိ လဲ ။
ပြည်သူ ပြည်သား တို့ ၏ ဆန္ဒ သည် အုပ်ချုပ် အာဏာ ၏ အခြေခံ ဖြစ် ရ မည် ၊ အဆိုပါ ဆန္ဒ ကို အချိန်ကာလ ပိုင်းခြား လျက် စစ်မှန် သော ရွေးကောက်ပွဲ များ ဖြင့် ထင်ရှား စေ ရ မည် ။
မည် သို့ စတင် ပေါ်ပေါက် ခဲ့ သည် ကို မူ ယခု ထက်တိုင် အတိအကျ မ သိ ရ သေး ပေ ။
ဒီ ဟာ လေး က ခင်ဗျား နဲ့ ပို လိုက် တယ် ။
ထို မှတ်တမ်း တို့ သည် လွန် ခဲ့ သော ရာစုနှစ် ၂ ခု အတွင်း နက္ခတ္တဗေဒ ပညာရှင် တို့ အတွက် စကြဝဠာ ကို နားလည် ရန် ကြိုးစား ရာတွင် အလွန် ပင် အရေးကြီး သည် ။
ကော်ဖီ သောက် ချင် ပါ သလား ။
သမိုင်း ၁၈၂၆ ၁၈၅၂ ခုနှစ် တွင် ဖြစ်ပွား ခဲ့ သည့် ပထမ အင်္ဂလိပ် မြန်မာ စစ်ပွဲ အပြီး တွင် ဗြိတိသျှ လက်အောက် သို့ ရန္တပို စာချုပ် အရ မြန်မာ နိုင်ငံ ပေး လိုက် ရ သောအခါ မော်လမြိုင် မြို့ သည် အောက် မြန်မာ ပြည် ၏ ပထမ ဆုံး မြို့တော် ဖြစ် လာ ခဲ့ သည် ။
ဤ အချက် တစ် ရပ် နှင့် ပင် ပိုးမွှား တို့ သည် လူ ၏ ရန်သူ ဖြစ် သည် ကို သဘောပေါက် ကြ ပေ လိမ့် မည် ။
(py2.7env) ye@:/media/ye/project2/data/myDep$ 
```

အထက်ပါအတိုင်း အဆင်ပြေပြေနဲ့ ပြောင်းပေးနိုင်တာကို တွေ့ရတယ်။  

## Conversion with Verbose Mode

conversion လုပ်တဲ့အခါမှာ verbose mode နဲ့ run ကြည့်ရအောင်...  
conversion လုပ်ရင်းနဲ့ error ဘာညာ ရှိရင် ဘယ်နေရာမှာ error ဖြစ်တာလဲ ဆိုတာကို trace လိုက်ဖို့အတွက် အသုံးဝင်လိမ့်မယ်လို့ ထင်တယ်...  

```
(py2.7env) ye@:/media/ye/project2/data/myDep$ time conllu2brat -i ./tst/ -v | tee verbose.log

Info: Processing ./tst/test.conllu.

Info: Writing into output/test.ann.

Info: Correctly processed ./tst/test.conllu.

real	0m0.655s
user	0m0.578s
sys	0m0.081s
```

တစ်ကြောင်းချင်းစီအတွက် information ပေးမယ်လို့ ထင်တာ မပေးဘူး...  

## Opening with Brat Annotation Editor

အထက်က format conversion အလုပ်နဲ့ ဆက်စပ်ပြီး ပြောရရင် တကယ်လို့ python environment က 2.7 မှာပဲ ဆိုရင်  
"conda deactivate" လုပ်ပေးပါ။  

```
(py2.7env) ye@:~/tool/brat$ conda deactivate
(base) ye@:~/tool/brat$
```

brat ကို အောက်ပါအတိုင်း run ခေါ်ခဲ့...   

```
(base) ye@:~/tool/brat$ python ./standalone.py 
Serving brat at http://0.0.0.0:8001
```

http://0.0.0.0:8001 ကို Ctrl+Click လုပ်လိုက်ရင် default browser မှာ brat annotation editor က တက်လာလိမ့်မယ်...  

brat က သူ့ root အောက်မှာ ရှိနေတဲ့ folder တွေထဲကနေပဲ ဖိုင်တွေကို ဖွင့်လို့ရတာလို့ ထင်တယ်။  
အဲဒါကြောင့် data/ အောက်မှာ tst-myDep/ ဆိုတဲ့ folder အသစ်ကို ဆောက်လိုက်ပြီးတော့ စောစောက convert လုပ်ထားတဲ့ .ann နဲ့ .txt ဖိုင်နှစ်ဖိုင်ကို ကော်ပီကူးခဲ့  

```
(base) ye@:~/tool/brat/data$ mkdir tst-myDep
(base) ye@:~/tool/brat/data$ cd tst-myDep/
(base) ye@:~/tool/brat/data/tst-myDep$ cp /media/ye/project2/data/myDep/output/* .
(base) ye@:~/tool/brat/data/tst-myDep$ ls
test.ann  test.txt
(base) ye@:~/tool/brat/data/tst-myDep$
```

browser မှာ အောက်ပါအတိုင်း မြင်ရလိမ့်မယ်။  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myDep-folder.png" alt="opening brat annotation editor" width="840"/>  
</p>  
<div align="center">
  Fig.1 Opening brat annotation editor
</div> 

<br />

convert လုပ်ခဲ့တာက test ဆိုတဲ့ ဖိုင်နာမည်မို့လို့ test ဖိုင်ကို ရွေးပေးလိုက်ပါတယ်။  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myDep-folder2.png" alt="Select your converted output folder" width="340"/>  
</p>  
<div align="center">
  Fig.2 Select your converted output folder 
</div> 

<br />

မြန်မာစာအတွက် လေဘယ်ထိုးထားတဲ့ dependency parsing tree တွေကို အောက်ပါအတိုင်း မြင်ရပါလိမ့်မယ်။  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myDep-browsing1.png" alt="some examples of Myanmar dependency trees" width="1040"/>  
</p>  
<div align="center">
  Fig.3 Some example of Myanmar dependency trees  
</div> 

<br />

အရမ်းရှည်တဲ့ စာကြောင်းတွေဆိုရင်တော့ အောက်ပါပုံထဲကလိုပဲ ကြည့်ရတာ အရမ်းအဆင်အပြေကြီးတော့ မဟုတ်ပါဘူး...  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myDep-browsing2.png" alt="when you browse the longer sentences" width="1040"/>  
</p>  
<div align="center">
  Fig.4 When you browse the longer annotated sentences
</div> 

<br />

## Preparation for config file

ငါတို့ရဲ့ converted output format က အောက်ပါအတိုင်း...  

```
(base) ye@:~/tool/brat/data/tst-myDep$ head ./test.ann
T1.1	NOUN 0 10	ကိန်းဂဏန်း
R1.1-1	obl Arg1:T1.4 Arg2:T1.1
#1.1	AnnotatorNotes T1.1	LEMMA=ကိန်းဂဏန်း POSTAG=N
T1.2	PART 11 14	တွေ
R1.2-1	case Arg1:T1.1 Arg2:T1.2
#1.2	AnnotatorNotes T1.2	LEMMA=တွေ POSTAG=PART
T1.3	PART 15 18	နဲ့
R1.3-1	case Arg1:T1.1 Arg2:T1.3
#1.3	AnnotatorNotes T1.3	LEMMA=နဲ့ POSTAG=PART
T1.4	NOUN 19 26	address
(base) ye@:~/tool/brat/data/tst-myDep$ 
```

Universal POS-tag ကို ဆွဲထုတ်ကြည့်ရင် စုစုပေါင်း tag ၁၄ခု ရှိတာကို အောက်ပါအတိုင်း တွေ့ရ...  

```
(base) ye@:/media/ye/project2/data/myDep/from-zzh/Updated-ConllU-Data$ cut -f4 ./test.conllu | grep -v "#" | sort | uniq

ADJ
ADP
ADV
CCONJ
INTJ
NOUN
NUM
PART
PRON
PROPN
PUNCT
SCONJ
SYM
VERB
```

myPOS POS-tag ကို ဆွဲထုတ်ကြည့်ရင် အောက်ပါအတိုင်း tag ၁၅ခု ရှိတာကို တွေ့ရ...  

```
(base) ye@:/media/ye/project2/data/myDep/from-zzh/Updated-ConllU-Data$ cut -f5 ./test.conllu | grep -v "#" | sort | uniq

ABB
ADJ
ADV
CONJ
FOR
INT
N
NUM
PART
PPM
PRON
PUNC
SB
TNUM
V
(base) ye@:/media/ye/project2/data/myDep/from-zzh/Updated-ConllU-Data$
```

Tag အရေအတွက်ကို စစ်ကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project2/data/myDep/from-zzh/Updated-ConllU-Data$ cut -f4 ./test.conllu | grep -v "#" | sort | uniq | wc
     15      14      70
(base) ye@:/media/ye/project2/data/myDep/from-zzh/Updated-ConllU-Data$
```

Relationship ကို အောက်ပါအတိုင်း ဆွဲထုတ်ကြည့်ခဲ့...  

```
(base) ye@:~/tool/brat/data/tst-myDep$ cat ./test.ann | egrep '^R' | cut -f 2 | head
obl Arg1:T1.4 Arg2:T1.1
case Arg1:T1.1 Arg2:T1.2
case Arg1:T1.1 Arg2:T1.3
compound Arg1:T1.6 Arg2:T1.4
compound Arg1:T1.6 Arg2:T1.5
obl Arg1:T1.9 Arg2:T1.6
case Arg1:T1.6 Arg2:T1.7
case Arg1:T1.6 Arg2:T1.8
obl Arg1:T1.11 Arg2:T1.9
case Arg1:T1.9 Arg2:T1.10
```

configuration ဖိုင်အတွက်က format ကို ပြောင်းဖို့ လိုအပ်တယ်။  
T<number>+.<number>+ ကို အစားထိုးရမယ်။  

```
(base) ye@:~/tool/brat/data/tst-myDep$ cat ./test.ann | egrep '^R' | cut -f 2 | sed "s/T[[:digit:]]\+.[[:digit:]]\+/<TOKEN>/g" | sort | uniq
acl Arg1:<TOKEN> Arg2:<TOKEN>
advmod Arg1:<TOKEN> Arg2:<TOKEN>
amod Arg1:<TOKEN> Arg2:<TOKEN>
case Arg1:<TOKEN> Arg2:<TOKEN>
compound Arg1:<TOKEN> Arg2:<TOKEN>
mark Arg1:<TOKEN> Arg2:<TOKEN>
nmod Arg1:<TOKEN> Arg2:<TOKEN>
nummod Arg1:<TOKEN> Arg2:<TOKEN>
obl Arg1:<TOKEN> Arg2:<TOKEN>
punct Arg1:<TOKEN> Arg2:<TOKEN>
(base) ye@:~/tool/brat/data/tst-myDep$
```

အထက်ပါအတိုင်း လိုချင်တဲ့ information တချို့ကို ဆွဲထုတ်ခဲ့ပြီး annotation.conf ဖိုင်ကို အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့...  

```
# Simple text-based definitions of entity types for the CoNLL format
# Task on dependency tree of Myanmar language (Burmese)


[entities]

ADJ
ADP
ADV
CCONJ
INTJ
NOUN
NUM
PART
PRON
PROPN
PUNCT
SCONJ
SYM
VERB

# (only entities defined, so the remaining sections are empty)

[relations]

# Macros
<TOKEN>=<ENTITY>

# Permitted forms of overlap between textbound annotations
#<OVERLAP> Arg1:<TOKEN>, Arg2:<TOKEN>, <OVL-TYPE>:contain

# Dependency relations

acl Arg1:<TOKEN>, Arg2:<TOKEN>
advmod Arg1:<TOKEN>, Arg2:<TOKEN>
amod Arg1:<TOKEN>, Arg2:<TOKEN>
case Arg1:<TOKEN>, Arg2:<TOKEN>
compound Arg1:<TOKEN>, Arg2:<TOKEN>
mark Arg1:<TOKEN>, Arg2:<TOKEN>
nmod Arg1:<TOKEN>, Arg2:<TOKEN>
nummod Arg1:<TOKEN>, Arg2:<TOKEN>
obl Arg1:<TOKEN>, Arg2:<TOKEN>
punct Arg1:<TOKEN>, Arg2:<TOKEN>


[events]
# not relevant to UD

[attributes]

# for Features followings did not work
# <TOKEN>=<ENTITY>
```

## Checking with Updated Configuration File
  
ဒီတစ်ခါတော့ relationship တွေနေရာမှာ error မပြတော့ပါဘူး...  
  
 
<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/with-correct-myDep-configuration-file1.png" alt="with correct configuration file" width="1040"/>  
</p>  
<div align="center">
  Fig.5 Opening with updated configuration file
</div> 
  
PageUp, PageDown လုပ်ကြည့်ခဲ့...  
  
<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/with-correct-myDep-configuration-file1.png" alt="with correct configuration file" width="1040"/>  
</p>  
<div align="center">
  Fig.6 Opening with updated configuration file
</div> 
  

<br />
  
relationship arrow ကို ထောက်ကြည့်တာ၊ စာလုံး တစ်လုံးချင်းစီကို ထောက်ကြည့်တာမျိုးလုပ်ရင် အောက်ပါအတိုင်း မြင်ရပါလိမ့်မယ်။  
 
<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/detail-info1.png" alt="detail information" width="1040"/>  
</p>  
<div align="center">
  Fig.7 Detail information
</div> 
  

<br />
  
<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/detail-info2.png" alt="detail information" width="640"/>  
</p>  
<div align="center">
  Fig.8 Detail information
</div> 
  

<br />

## Preparing One Line One Tree
  
brat annotation editor နဲ့ လိုင်း အများကြီးပါတဲ့ ဖိုင်ကို ဖွင့်ကြည့်ရင် လေးတယ်။ အဲဒါကြောင့် အများစုက လိုင်း ၁၀လိုင်းကို တစ်ဖိုင် သပ်သပ်စီ ခွဲသိမ်းကြတာမျိုး လုပ်ပြီး အလုပ်လုပ်လေ့ရှိတယ်။  
မြန်မာစာကြောင်း တစ်ကြောင်းကို တစ်ဖိုင်စီ ဖြစ်အောင် အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့တယ်။  


Reference: https://stackoverflow.com/questions/33294986/splitting-large-text-file-on-every-blank-line  

conversion လုပ်ပေးတဲ့ tool က ".conllu" ဆိုတဲ့ extension နဲ့ ဖိုင်တွေကို ရှာမှာမို့လို့ perl script ကို အောက်ပါအတိုင်း update လုပ်ခဲ့တယ်။    
  
```perl
#!/usr/bin/env perl
use strict;
use warnings;

local $/ = "\n\n"; 
my $count = 1; 

while ( my $chunk = <> ) {
    open ( my $output, '>', "line_".$count++.".conllu" ) or die $!;
    print {$output} $chunk;
    close ( $output ); 
}
```
  
line_by_line/ ဆိုတဲ့ ဖိုလ်ဒါအသစ်တစ်ခုကို အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့...  
  
```
(base) ye@:~/tool/brat/data/tst-myDep/line_by_line$ ls
split-with-blank-line.pl  test.conllu
(base) ye@:~/tool/brat/data/tst-myDep/line_by_line$
```
  
အောက်ပါအတိုင်း run ခဲ့...  
  
```
(base) ye@:~/tool/brat/data/tst-myDep/line_by_line$ perl ./split-with-blank-line.pl ./test.conllu
```

original ဖိုင်မှာက စုစုပေါင်း စာကြောင်းအရေအတွက် 802 ကြောင်းရှိတယ်။  
  
```
(base) ye@:~/tool/brat/data/tst-myDep/line_by_line$ grep sent_id ./test.conllu | tail
# sent_id = 793
# sent_id = 794
# sent_id = 795
# sent_id = 796
# sent_id = 797
# sent_id = 798
# sent_id = 799
# sent_id = 800
# sent_id = 801
# sent_id = 802
```

count လုပ်ရင် extension တူရင် တစ်ဖိုင်ပိုသွားမှာမို့ original ဖိုင်ကို နာမည်ပြောင်းခဲ့...  
  
```
(base) ye@:~/tool/brat/data/tst-myDep/line_by_line$ mv test.conllu test.conllu.original
```

split လုပ်ထားတဲ့ ဖိုင်အရေအတွက် စုစုပေါင်းကို အောက်ပါအတိုင်း confirm လုပ်ခဲ့...  
  
```
(base) ye@:~/tool/brat/data/tst-myDep/line_by_line$ ls *.conllu | wc
    802     802   12724
(base) ye@:~/tool/brat/data/tst-myDep/line_by_line$
```

perl script ထဲမှာက လိုင်းနံပါတ်က ၁ ကနေ စတာမို့ ပထမဆုံး စာကြောင်းက line_1 နဲ့ စလိမ့်မယ်။  
အောက်ပါအတိုင်း...  
  
```
(base) ye@:~/tool/brat/data/tst-myDep/line_by_line$ ls *.conllu | sort -V | head
line_1.conllu
line_2.conllu
line_3.conllu
line_4.conllu
line_5.conllu
line_6.conllu
line_7.conllu
line_8.conllu
line_9.conllu
line_10.conllu
(base) ye@:~/tool/brat/data/tst-myDep/line_by_line$
```

line no. 802 မှာ ဆုံးသွားလိမ့်မယ်။  
  
```
(base) ye@:~/tool/brat/data/tst-myDep/line_by_line$ ls *.conllu | sort -V | tail
line_793.conllu
line_794.conllu
line_795.conllu
line_796.conllu
line_797.conllu
line_798.conllu
line_799.conllu
line_800.conllu
line_801.conllu
line_802.conllu
(base) ye@:~/tool/brat/data/tst-myDep/line_by_line$
```

split လုပ်ထားတဲ့ ဖိုင်တွေရဲ့ အထဲကို ဝင်ကြည့်ပြီး confirmation လုပ်ခဲ့...  
  
```
(base) ye@:~/tool/brat/data/tst-myDep/line_by_line$ cat ./line_802.conllu
# sent_id = 802
# text = ထို မှတစ်ပါး ငှက် တို့ သည် ဟင်းလျာ အတွက် လည်း အသုံးဝင် သည် ။
1	ထို	ထို	PRON	PRON	_	9	obl	_	_
2	မှတစ်ပါး	မှတစ်ပါး	SCONJ	CONJ	_	9	mark	_	_
3	ငှက်	ငှက်	NOUN	N	_	9	obl	_	_
4	တို့	တို့	PART	PART	_	3	case	_	_
5	သည်	သည်	ADP	PPM	_	3	case	_	_
6	ဟင်းလျာ	ဟင်းလျာ	NOUN	N	_	9	obl	_	_
7	အတွက်	အတွက်	ADP	PPM	_	6	case	_	_
8	လည်း	လည်း	PART	PART	_	6	case	_	_
9	အသုံးဝင်	အသုံးဝင်	VERB	V	_	0	root	_	_
10	သည်	သည်	ADP	PPM	_	9	case	_	SpaceAfter=No
11	။	။	PUNCT	PUNC	_	9	punct	_	_

(base) ye@:~/tool/brat/data/tst-myDep/line_by_line$
```

conllu2brat ကို run ဖို့အတွက် python 2.7 environment ကို change ခဲ့...  
  
```
(base) ye@:~/tool/brat/data/tst-myDep/line_by_line$ conda activate py2.7env
(py2.7env) ye@:~/tool/brat/data/tst-myDep/line_by_line$
```

conllu2brat နဲ့ ".ann" နဲ့ ".txt" ဖိုင်တွေကို ထုတ်ခဲ့...  
  
```
(py2.7env) ye@:~/tool/brat/data/tst-myDep$ time conllu2brat -i ./line_by_line/
...
...
...
Info: Correctly processed ./line_by_line/line_365.conllu.

Info: Correctly processed ./line_by_line/line_132.conllu.

Info: Correctly processed ./line_by_line/line_627.conllu.

Info: Correctly processed ./line_by_line/line_55.conllu.

Info: Correctly processed ./line_by_line/line_36.conllu.
Info: Converting the files  [##################################--]   97%
Info: Correctly processed ./line_by_line/line_457.conllu.

Info: Correctly processed ./line_by_line/line_638.conllu.
Info: Converting the files  [###################################-]   97%
Info: Correctly processed ./line_by_line/line_439.conllu.

Info: Correctly processed ./line_by_line/line_237.conllu.

Info: Correctly processed ./line_by_line/line_161.conllu.

Info: Correctly processed ./line_by_line/line_614.conllu.

Info: Correctly processed ./line_by_line/line_768.conllu.

Info: Correctly processed ./line_by_line/line_430.conllu.
Info: Converting the files  [###################################-]   98%
Info: Correctly processed ./line_by_line/line_118.conllu.

Info: Correctly processed ./line_by_line/line_233.conllu.

Info: Correctly processed ./line_by_line/line_645.conllu.

Info: Correctly processed ./line_by_line/line_135.conllu.

Info: Correctly processed ./line_by_line/line_306.conllu.

Info: Correctly processed ./line_by_line/line_99.conllu.

Info: Correctly processed ./line_by_line/line_208.conllu.

Info: Correctly processed ./line_by_line/line_628.conllu.
Info: Converting the files  [###################################-]   99%
Info: Correctly processed ./line_by_line/line_298.conllu.

Info: Correctly processed ./line_by_line/line_651.conllu.

Info: Correctly processed ./line_by_line/line_705.conllu.

Info: Correctly processed ./line_by_line/line_142.conllu.

Info: Correctly processed ./line_by_line/line_796.conllu.

Info: Correctly processed ./line_by_line/line_778.conllu.

Info: Correctly processed ./line_by_line/line_256.conllu.

Info: Correctly processed ./line_by_line/line_252.conllu.
Info: Converting the files  [####################################]  100%

real	0m0.786s
user	0m0.664s
sys	0m0.105s

```

".ann", ".txt" ဖိုင်တွေကို output/ ဖိုလ်ဒါအောက်မှာ သိမ်းပေးတာကို အောက်ပါအတိုင်း တွေ့ရ...  
  
```
(py2.7env) ye@:~/tool/brat/data/tst-myDep$ ls ./output/ | sort -V | head -n 20
line_1.ann
line_1.txt
line_2.ann
line_2.txt
line_3.ann
line_3.txt
line_4.ann
line_4.txt
line_5.ann
line_5.txt
line_6.ann
line_6.txt
line_7.ann
line_7.txt
line_8.ann
line_8.txt
line_9.ann
line_9.txt
line_10.ann
line_10.txt
(py2.7env) ye@:~/tool/brat/data/tst-myDep$ 
```

brat annotation editor က ဖတ်လို့ရဖို့အတွက် သတ်မှတ်ထားတဲ့ format အတိုင်း ပြောင်းပေးထားတာကို confirmation လုပ်ခဲ့...   
  
```
(py2.7env) ye@:~/tool/brat/data/tst-myDep$ cat ./output/line_5.txt
မည် သို့ စတင် ပေါ်ပေါက် ခဲ့ သည် ကို မူ ယခု ထက်တိုင် အတိအကျ မ သိ ရ သေး ပေ ။
(py2.7env) ye@:~/tool/brat/data/tst-myDep$ cat ./output/line_5.ann 
T1.1	PRON 0 3	မည်
R1.1-1	obl Arg1:T1.4 Arg2:T1.1
#1.1	AnnotatorNotes T1.1	LEMMA=မည် POSTAG=PRON
T1.2	PART 4 8	သို့
R1.2-1	case Arg1:T1.1 Arg2:T1.2
#1.2	AnnotatorNotes T1.2	LEMMA=သို့ POSTAG=PART
T1.3	VERB 9 13	စတင်
R1.3-1	acl Arg1:T1.4 Arg2:T1.3
#1.3	AnnotatorNotes T1.3	LEMMA=စတင် POSTAG=V
T1.4	VERB 14 23	ပေါ်ပေါက်
R1.4-1	acl Arg1:T1.13 Arg2:T1.4
#1.4	AnnotatorNotes T1.4	LEMMA=ပေါ်ပေါက် POSTAG=V
T1.5	PART 24 27	ခဲ့
R1.5-1	mark Arg1:T1.4 Arg2:T1.5
#1.5	AnnotatorNotes T1.5	LEMMA=ခဲ့ POSTAG=PART
T1.6	ADP 28 31	သည်
R1.6-1	case Arg1:T1.4 Arg2:T1.6
#1.6	AnnotatorNotes T1.6	LEMMA=သည် POSTAG=PPM
T1.7	ADP 32 35	ကို
R1.7-1	case Arg1:T1.4 Arg2:T1.7
#1.7	AnnotatorNotes T1.7	LEMMA=ကို POSTAG=PPM
T1.8	SCONJ 36 38	မူ
R1.8-1	mark Arg1:T1.4 Arg2:T1.8
#1.8	AnnotatorNotes T1.8	LEMMA=မူ POSTAG=CONJ
T1.9	NOUN 39 42	ယခု
R1.9-1	obl Arg1:T1.13 Arg2:T1.9
#1.9	AnnotatorNotes T1.9	LEMMA=ယခု POSTAG=N
T1.10	ADP 43 51	ထက်တိုင်
R1.10-1	case Arg1:T1.9 Arg2:T1.10
#1.10	AnnotatorNotes T1.10	LEMMA=ထက်တိုင် POSTAG=PPM
T1.11	ADV 52 58	အတိအကျ
R1.11-1	advmod Arg1:T1.13 Arg2:T1.11
#1.11	AnnotatorNotes T1.11	LEMMA=အတိအကျ POSTAG=ADV
T1.12	PART 59 60	မ
R1.12-1	case Arg1:T1.13 Arg2:T1.12
#1.12	AnnotatorNotes T1.12	LEMMA=မ POSTAG=PART
T1.13	VERB 61 63	သိ
#1.13	AnnotatorNotes T1.13	LEMMA=သိ POSTAG=V
T1.14	PART 64 65	ရ
R1.14-1	mark Arg1:T1.13 Arg2:T1.14
#1.14	AnnotatorNotes T1.14	LEMMA=ရ POSTAG=PART
T1.15	PART 66 69	သေး
R1.15-1	case Arg1:T1.13 Arg2:T1.15
#1.15	AnnotatorNotes T1.15	LEMMA=သေး POSTAG=PART
T1.16	PART 70 72	ပေ
R1.16-1	mark Arg1:T1.13 Arg2:T1.16
#1.16	AnnotatorNotes T1.16	LEMMA=ပေ POSTAG=PART MISC=SpaceAfter=No
T1.17	PUNCT 73 74	။
R1.17-1	punct Arg1:T1.13 Arg2:T1.17
#1.17	AnnotatorNotes T1.17	LEMMA=။ POSTAG=PUNC
(py2.7env) ye@:~/tool/brat/data/tst-myDep$
```
  
## Opening with Brat

လက်ရှိ output/ ဖိုလ်ဒါအောက်မှာက annotation.config ဖိုင်က မရှိသေးလို့ copy ကူးထည့်တာ၊ ပြီးတော့ python environment ကိုလည်း 2.7 environment ကနေ normal (python 3.x environment) ကို ပြန်ပြောင်းတာ အရင်ဆုံး လုပ်ခဲ့တယ်။
  
```
(py2.7env) ye@:~/tool/brat/data/tst-myDep$ cp ./annotation.conf ./output/
(py2.7env) ye@:~/tool/brat/data/tst-myDep$ conda deactivate
```
  
ပြီးမှ တစ်ကြောင်းချင်းစီ ဖြတ်ထုတ်ထားတဲ့ မြန်မာစာကြောင်း dependency tree တွေကို ဖွင့်ကြည့်ခဲ့တယ်။  
  
```
(base) ye@:~/tool/brat$ python ./standalone.py 
Serving brat at http://0.0.0.0:8001
```
  
## Reference
  
- [https://brat.nlplab.org/configuration.html](https://brat.nlplab.org/configuration.html)  
- [https://universaldependencies.org/u/feat/index.html](https://universaldependencies.org/u/feat/index.html)  
