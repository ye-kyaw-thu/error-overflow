# conll2brat Conversion Log

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
http://0.0.0.0:8001 ကို Ctrl+Click လုပ်လိုက်ရင် default browser မှာ brat annotation editor က တက်လာလိမ့်မယ်...  

```
(base) ye@:~/tool/brat$ python ./standalone.py 
Serving brat at http://0.0.0.0:8001
```

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myDep-folder.png" alt="shortest path" width="840"/>  
</p>  
<div align="center">
  Fig.2 the shortest path for the input sentence "ဆရာက" 
</div> 

<br />

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

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myDep-folder2.png" alt="shortest path" width="340"/>  
</p>  
<div align="center">
  Fig.2 the shortest path for the input sentence "ဆရာက" 
</div> 

<br />

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myDep-tst-data-browsing.png" alt="shortest path" width="340"/>  
</p>  
<div align="center">
  Fig.2 the shortest path for the input sentence "ဆရာက" 
</div> 

<br />
