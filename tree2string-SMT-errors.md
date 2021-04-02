# Tree to String SMT Errors Note

An example of tree-to-string SMT running with noisy data.  
Here, the language pair is English-to-Myanmar.  
Most of the notes are written in Burmese (Myanmar language) and mainly prepared for Myanmar students.  

Thanks!  

ye  

tree-to-string SMT က သုတေသန အနေနဲ့ လုပ်စရာတွေ အများကြီးရှိပါတယ်။ ဒီနေရာမှာက အင်္ဂလိပ်စာကြောင်းတွေကို syntax tree parsing လုပ်ပြီး မြန်မာစာ စာကြောင်းတွေကို ဘာသာပြန်ဖို့အတွက် စမ်းထားတဲ့ experiment တစ်ခုနဲ့ ပတ်သက်ပြီး လေ့လာလို့ရအောင် ကြုံတွေ့ရတဲ့ လက်တွေ့ အခက်အခဲတွေနဲ့ Error တွေကို အကြမ်းမျဉ်း ချရေးပြထားတာ ဖြစ်ပါတယ်။ တကယ့် experimental log အကြမ်းပါ။  


## Parsing

အင်္ဂလိပ်စာကြောင်းတွေကို syntax tree အဖြစ်ပြောင်းပေးတဲ့ Parser တွေ အမျိုးမျိုး ရှိတယ်။ Parsing လုပ်တဲ့ technique တွေကလည်း အမျိုးမျိုး study လုပ်နေကြသလို၊ သဒ္ဒါပိုင်းအနေနဲ့လည်း လေ့လာတဲ့ အပိုင်းတွေ၊ ဦးတည်ချက်တွေက အမျိုးမျိုးပါပဲ။ ကိုယ်က ဘယ်လို parsing မျိုးကို လုပ်ချင်တာလဲ ဆိုတဲ့ အပေါ်ကို မူတည်ပြီး parser ကိုလည်း ရွေးကြရပါလိမ့်မယ်။    
ဥပမာ  

1. (Stanford Parser version 4.2.0)[https://nlp.stanford.edu/software/lex-parser.shtml]  
2. (BLLIP Reranking Parser)[https://github.com/BLLIP/bllip-parser]
3. (Berkeley Neural Parser)[https://github.com/nikitakit/self-attentive-parser]
4. (nltk.parse package)[https://www.nltk.org/api/nltk.parse.html]
5. (The Phrase Parser)[https://www.link.cs.cmu.edu/link/ph-explanation.html]

## Syntax Tree Parsing with NLTK

Parser တွေက အင်္ဂလိပ်စာမှာတောင် အဆင်မပြေတဲ့ limitation တွေ အများကြီးပါ။ အဲဒီအထဲက တစ်ခုက string length က ရှည်လာရင် မှန်မှန်ကန်ကန် parsing လုပ်မပေးနိုင်တာနဲ့၊ လုံးဝကို parsing လုပ်မပေးတော့ပဲ blank line အဖြစ်နဲ့သာ output ထုတ်လို့ Statistical Machine Translation/Neural Machine Translation လုပ်ဖို့အတွက် source-target အတွဲက လွဲကုန်တဲ့ ပြဿနာတွေ ရှိလာပါတယ်။  

ဒီနေရာမှာတော့ NLTK parser ကို သုံးပြီး ကျောင်းသူတစ်ယောက်က သူစမ်းထားတာကို report တင်ထားလို့ အဲဒီ NLTK parser နဲ့ parsing လုပ်ထားတဲ့ ဒေတာကိုပဲ သုံးပြီး moses နဲ့ SMT experiment လုပ်သွားမှာ ဖြစ်ပါတယ်။  
NLT နဲ့ parse လုပ်မယ် ဆိုရင် အောက်ပါလိုမျိုး Python script ရေးပြီး parsing လုပ်လို့ ရပါတယ်။  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-tmp/data/parsing/example$ cat ./nltk_parser.py 
import nltk 
#nltk.download('punkt') 
nltk.download('averaged_perceptron_tagger') 
from nltk import pos_tag, word_tokenize, RegexpParser 
   
#Extract all parts of speech from any text 
chunker = RegexpParser(""" 
                       NP: {<DT>?<JJ>*<NN>}    #To extract Noun Phrases 
                       P: {<IN>}               #To extract Prepositions 
                       V: {<V.*>}              #To extract Verbs 
                       PP: {<P> <NP>}          #To extract Prepostional Phrases 
                       VP: {<V> <NP|PP>*}      #To extarct Verb Phrases 
                       """) 


r_file = open("bbc.article.txt", "r")

with open("bbc.article.parse.txt","a") as w_file:
    for line in r_file:
      tagged = pos_tag(word_tokenize(line)) 
      parse_out= chunker.parse(tagged) 
      parse_str= ' '.join(str(parse_out).split()) 
      w_file.write(parse_str+"\n")
      parse_str=""
      parse_out=""
      tagged=""

```

Python script ကို run တဲ့အခါမှာ တကယ်လို့ nltk package တွေ၊ မော်ဒယ်တွေက ကိုယ့်စက်ထဲမှာ မရှိသေးရင် download လုပ်သွားပါလိမ့်မယ်။  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-tmp/data/parsing/example$ python ./nltk_parser.py 
[nltk_data] Downloading package averaged_perceptron_tagger to
[nltk_data]     /home/ye/nltk_data...
[nltk_data]   Package averaged_perceptron_tagger is already up-to-
[nltk_data]       date!
```

ဥပမာ အနေနဲ့ parsing လုပ်ပြမယ့် စာကြောင်းတွေက BBC News (https://www.bbc.com/news/world-asia-56612247) က စာကြောင်းငါးကြောင်းကို ယူသုံးထားပါတယ်။ Parsing မလုပ်ခင်က အင်္ဂလိပ်စာကြောင်းတွေက အောက်ပါအတိုင်း ရှိပါလိမ့်မယ်။  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-tmp/data/parsing/example$ cat ./bbc.article.txt 
Myanmar's military seized power in the South East Asian nation after overthrowing the government and declared a state of emergency.
Just days later, the civil disobedience movement began to emerge - professionals refusing to return to work in protest.
The movement quickly started to gain momentum and it was not long before hundreds of thousands of people began taking part in street protests.
But there has increasingly been an escalation of violence between police officers and civilians.
Rights group the Assistance Association for Political Prisoners say more than 500 people have been killed since the military crackdown began.
```

Parsing လုပ်ပြီးတဲ့အခါမှာတော့ အောက်ပါပုံစံ ရရှိပါလိမ့်မယ်။  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-tmp/data/parsing/example$ cat ./bbc.article.parse.txt
(S Myanmar/NNP 's/POS (NP military/JJ seized/JJ power/NN) (P in/IN) the/DT South/NNP East/NNP (NP Asian/JJ nation/NN) (P after/IN) (VP (V overthrowing/VBG) (NP the/DT government/NN)) and/CC (VP (V declared/VBD) (NP a/DT state/NN) (PP (P of/IN) (NP emergency/NN))) ./.)
(S Just/RB days/NNS later/RB ,/, (NP the/DT civil/JJ disobedience/NN) (NP movement/NN) (VP (V began/VBD)) to/TO (VP (V emerge/VB)) -/: professionals/NNS (VP (V refusing/VBG)) to/TO (VP (V return/VB)) to/TO (VP (V work/VB) (PP (P in/IN) (NP protest/NN))) ./.)
(S (NP The/DT movement/NN) quickly/RB (VP (V started/VBD)) to/TO (VP (V gain/VB) (NP momentum/NN)) and/CC it/PRP (VP (V was/VBD)) not/RB long/RB before/RB hundreds/NNS (P of/IN) thousands/NNS (P of/IN) people/NNS (VP (V began/VBD)) (VP (V taking/VBG) (NP part/NN) (PP (P in/IN) (NP street/NN))) protests/NNS ./.)
(S But/CC there/EX (VP (V has/VBZ)) increasingly/RB (VP (V been/VBN) (NP an/DT escalation/NN) (PP (P of/IN) (NP violence/NN)) (PP (P between/IN) (NP police/NN))) officers/NNS and/CC civilians/NNS ./.)
(S Rights/NNS (NP group/NN) the/DT Assistance/NNP Association/NNP (P for/IN) Political/JJ Prisoners/NNS (VP (V say/VBP)) more/JJR (P than/IN) 500/CD people/NNS (VP (V have/VBP)) (VP (V been/VBN)) (VP (V killed/VBN) (PP (P since/IN) (NP the/DT military/JJ crackdown/NN))) (VP (V began/VBD)) ./.)
```

တကယ် လက်တွေ့ SMT/NMT experiment တွေအတွက် parsing လုပ်တဲ့အခါမှာတော့ parsing grammar တွေကို အသေးစိတ် စစ်ဆေးတာ၊ ပြင်တာ လုပ်နိုင်ရင် လုပ်ကြပါ။ အနည်းဆုံးတော့ input ပေးလိုက်တဲ့ စာကြောင်းတွေအားလုံးက output အဖြစ် ထုတ်ပေးနိုင်ရဲ့လား (i.e. check no. of sentences between input vs output) ဆိုတာကိုတော့ စစ်ရပါလိမ့်မယ်။  

ဒါ့အပြင် သုံးတဲ့ parser တွေအပေါ်မူတည်ပြီးထွက်လာတဲ့ output တွေရဲ့ format က bracket နဲ့ ထုတ်တာ၊ XML tree အနေနဲ့ ထုတ်တာ စသည်ဖြင့် အမျိုးမျိုး ကွဲပြားနိုင်ပါတယ်။ ဥပမာ CMU တက္ကသိုလ်ရဲ့ phrase-parser (version 4.0) ရဲ့ online demo site ကို "But there has increasingly been an escalation of violence between police officers and civilians." ဆိုတဲ့ စာကြောင်းကို parse လုပ်လိုက်ရင် အောက်ပါလိုမျိုး output ထုတ်ပေးပါလိမ့်မယ်။  

```
++++Time                                          0.01 seconds (252.53 total)
Found 12 linkages (8 with no P.P. violations)
  Linkage 1, cost vector = (UNUSED=0 DIS=1 AND=1 LEN=22)

    +---------------------------------------------------------Xp------------
    |                                     +-----------------MVp-------------
    |                 +--------PPf--------+-----Ost----+                    
    +--Wc--+-Wdc+-SFst+         +----E----+    +--Dsu--+---Mp--+--Jp--+     
    |      |    |     |         |         |    |       |       |      |     
LEFT-WALL but there has.v increasingly been.v an escalation.n of violence.n 


--------------------------------------------+
---+                                        |
   +--------Jp--------+                     |
   |        +----AN---+                     |
   |        |         |                     |
between police.s officers.n and civilians.n . 


    +---------------------------------------------------------Xp------------
    |                                     +-----------------MVp-------------
    |                 +--------PPf--------+-----Ost----+                    
    +--Wc--+-Wdc+-SFst+         +----E----+    +--Dsu--+---Mp--+--Jp--+     
    |      |    |     |         |         |    |       |       |      |     
LEFT-WALL but there has.v increasingly been.v an escalation.n of violence.n 


--------------------------------------------+
---+                                        |
   |                                        |
   +----------------Jp---------------+      |
   |                                 |      |
between police.s officers.n and civilians.n . 

Constituent tree:

(S But
   (NP there)
   (VP has
       (VP (ADVP increasingly)
           been
           (NP (NP an escalation)
               (PP of
                   (NP violence)))
           (PP between
               (NP (NP police officers)
                   and
                   (NP civilians)))))
   .)

```

Note: ထိုနည်းလည်းကောင်းပဲ Billip parser က အများဆုံး parse လုပ်ပေးနိုင်တာက 184 words အထိပဲ ဖြစ်ပြီးတော့ အဲဒီထက်ကျော်တဲ့ စာကြောင်းတွေဆိုရင် "list index out of range error" ပေးပါလိမ့်မယ်။  
 
## Tokenized and Tree Data Preparation

ထုံးစံအတိုင်း SMT experiment အတွက် corpus preparation လုပ်ရတယ်။ tree-to-string, string-to-tree SMT experiment လုပ်ဖို့အတွက်က ဒေတာနှစ်မျိုး ပြင်ရပါလိမ့်မယ်။ Tokenized (e.g. word segmented, syllable segmented, sub-word level segmented) ဒေတာတွေကို ပြင်ရတဲ့အပိုင်းနဲ့ syntax tree parse လုပ်ထားတဲ့ ဒေတာကိုလည်း အောက်ပါအတိုင်း ဖိုလ်ဒါခွဲသိမ်းရပါတယ်။  

```console
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string$ tree -L 1 ./data.tok/
./data.tok/
├── dev.my
├── test.my
└── train.my
```

tree ဒေတာကတော့ data.tree/ အောက်မှာ သိမ်းထားတယ်။  

```console
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string$ tree -L 1 ./data.tree/
./data.tree/
├── dev.en
├── test.en
├── train.en
└── train.my
```

## Preparing t2s.sh Shell Script

tree-to-string SMT experiment ကို လုပ်ဖို့အတွက်က ကိုယ့်စက်ထဲမှာ moses က run လို့ ရအောင် ပြင်ဆင်ပြီးသား ဖြစ်ရပါလိမ့်မယ်။  
Link for downloading moses: https://github.com/moses-smt/mosesdecoder  
Online manual of moses: https://www.statmt.org/moses/manual/manual.pdf  

Experiment ကို config ဖိုင် ပြင်ဆင်ပြီး Experiment Management System (EMS) နဲ့လည်း run လို့ရပေမဲ့ ဒီနေရာမှာတော့ shell script ပြင်ပြီးပဲ run တာနဲ့ပဲသွားပါမယ်။  

[WAT2015](http://orchid.kuee.kyoto-u.ac.jp/WAT/WAT2015/baseline/baselineSystemTree2String.html) က tree to string SMT shell script ကို အခြေခံပြီးတော့ t2s.sh ဖိုင်ကို ပြင်ခဲ့တယ်။   
## Error Relating to Alignment Process or GIZA++/mgiza

အောက်ပါအတိုင်း error ပေးတာမျိုး ကြုံရနိုင်ပါတယ်။  

```
Using SCRIPTS_ROOTDIR: /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts
Using single-thread GIZA
using gzip 
ERROR: Cannot find mkcls, GIZA++/mgiza, & snt2cooc.out/snt2cooc in /home/ye/tool/mosesbin/ubuntu-17.04/training-tools.
You MUST specify the parameter -external-bin-dir at /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/training/train-model.perl line 491.
```

Error ကို ဖြေရှင်းတာကတော့ moses system က ရှာနေတဲ့ path အတိုင်း mgiza ကို GIZA++/ ဖိုလ်ဒါအောက်မှာ ကော်ပီကူးထည့်ခဲ့တယ်။ ထိုနည်းလည်းကောင်းပဲ snt2cooc ဖိုင်ကိုလည်း snt2cooc.out/ ဖိုလ်ဒါအောက်မှာ ကော်ပီကူးထည့်ခဲ့ပါတယ်။ folder tree က အောက်ပါအတိုင်း လုပ်ပေးလိုက်ရင် ပြေလည်သွားလိမ့်မယ်။  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesbin/ubuntu-17.04/training-tools$ ls
merge_alignment.py  mgiza  mkcls  snt2cooc
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesbin/ubuntu-17.04/training-tools$ mkdir GIZA++
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesbin/ubuntu-17.04/training-tools$ cp mgiza  ./GIZA++/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesbin/ubuntu-17.04/training-tools$ mkdir snt2cooc.out
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesbin/ubuntu-17.04/training-tools$ cp snt2cooc ./snt2cooc.out/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesbin/ubuntu-17.04/training-tools$ tree
.
├── GIZA++
│   └── mgiza
├── merge_alignment.py
├── mgiza
├── mkcls
├── snt2cooc
└── snt2cooc.out
    └── snt2cooc

2 directories, 6 files
```

တစ်ခု ရှိတာက GIZA single thread နဲ့ align လုပ်တာက အရမ်းကြာနေတယ်။ အဲဒါကြောင့် Ctrl+C နဲ့ ပရိုဂရမ်ကို break လုပ်လိုက်တယ်။  
Log ကို ကြည့်တော့...  

```console
Using SCRIPTS_ROOTDIR: /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts
Using single-thread GIZA
using gzip 
(1) preparing corpus @ Tue Mar 30 23:55:23 +0630 2021
Executing: mkdir -p /home/ye/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/training/corpus
(1.0) selecting factors @ Tue Mar 30 23:55:23 +0630 2021
Forking...
(1.0.5) reducing factors to produce /home/ye/exp/smt/wat2021/tree-smt/tree2string/data.tree/train.0-0.my  @ Tue Mar 30 23:55:23 +0630 2021
(1.0.5) reducing factors to produce /home/ye/exp/smt/wat2021/tree-smt/tree2string/data.tree/train.0-0.en  @ Tue Mar 30 23:55:23 +0630 2021
  /home/ye/exp/smt/wat2021/tree-smt/tree2string/data.tree/train.0-0.en in place, reusing
```

Training time မြန်ဖို့အတွက် mgiza နဲ့ သုံးလို့ ရဖို့ အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့...  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mgiza/mgizapp/bin$ ls
d4norm                    force-align-moses.sh  hmmnorm             mgiza  plain2snt            run.sh    snt2cooc.pl  snt2plain       symal
force-align-moses-old.sh  giza2bal.pl           merge_alignment.py  mkcls  plain2snt-hasvcb.py  snt2cooc  snt2coocrmp  sntpostproc.py
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mgiza/mgizapp/bin$ mkdir GIZA++
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mgiza/mgizapp/bin$ cp mgiza ./GIZA++/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mgiza/mgizapp/bin$ mkdir snt2cooc.out
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mgiza/mgizapp/bin$ cp snt2cooc ./snt2cooc.out/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mgiza/mgizapp/bin$ tree
.
├── d4norm
├── force-align-moses-old.sh -> /home/ye/tool/mgiza/mgizapp/scripts/force-align-moses-old.sh
├── force-align-moses.sh -> /home/ye/tool/mgiza/mgizapp/scripts/force-align-moses.sh
├── GIZA++
│   └── mgiza
├── giza2bal.pl -> /home/ye/tool/mgiza/mgizapp/scripts/giza2bal.pl
├── hmmnorm
├── merge_alignment.py -> /home/ye/tool/mgiza/mgizapp/scripts/merge_alignment.py
├── mgiza
├── mkcls
├── plain2snt
├── plain2snt-hasvcb.py -> /home/ye/tool/mgiza/mgizapp/scripts/plain2snt-hasvcb.py
├── run.sh -> /home/ye/tool/mgiza/mgizapp/scripts/run.sh
├── snt2cooc
├── snt2cooc.out
│   └── snt2cooc
├── snt2cooc.pl -> /home/ye/tool/mgiza/mgizapp/scripts/snt2cooc.pl
├── snt2coocrmp
├── snt2plain
├── sntpostproc.py -> /home/ye/tool/mgiza/mgizapp/scripts/sntpostproc.py
└── symal

2 directories, 19 files
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mgiza/mgizapp/bin$
```

## Assign More CPU for the Alignment Process

train-model.perl  run တဲ့ command မှာ အောက်ပါ option ကို ဖြည့်လိုက်တယ်။  
```  --mgiza --mgiza-cpus 6 \```

ပြီးတော့ လက်ရှိ စက်မှာက CPU က ရှစ်လုံးပဲ ရှိတာမို့ ```JOBS=6``` ထားလိုက်တယ်။  
ပြန် train တော့ log ဖိုင်မှာတော့ အောက်ပါအတိုင်း multi-thread ကို GIZA သုံးတယ်ဆိုတာတော့ မြင်လာရပြီ...   

```
Using SCRIPTS_ROOTDIR: /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts
Using multi-thread GIZA
using gzip 
...
```

သို့သော် training က အရမ်းကြာနေသေး...  

## Recheck the format of parsed tree

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/wmt2014-scripts/example/data$ head -n 1 parallelC.de-en.parsed.en 
<tree label="sent"><tree label="root"><tree label="nsubj"><tree label="det"><tree label="DT">The</tree></tree><tree label="NN">ECB</tree></tree><tree label="VBZ">wants</tree><tree label="xcomp"><tree label="aux"><tree label="TO">to</tree></tree><tree label="VB">hold</tree><tree label="dobj"><tree label="NN">inflation</tree></tree><tree label="prep"><tree label="TO">to</tree><tree label="pcomp"><tree label="IN">under</tree><tree label="pobj"><tree label="num"><tree label="CD">two</tree></tree><tree label="NN">percent</tree><tree label="punct"><tree label=",">,</tree></tree><tree label="cc"><tree label="CC">or</tree></tree><tree label="conj"><tree label="advmod"><tree label="RB">somewhere</tree></tree><tree label="IN">in</tree><tree label="pobj"><tree label="det"><tree label="DT">that</tree></tree><tree label="NN">vicinity</tree></tree></tree></tree></tree></tree></tree><tree label="punct"><tree label=".">.</tree></tree></tree></tree>
```

moses က လက်ခံတာက အထက်မှာ ပြထားသလို xml tag format ပုံစံလို့ ထင်တယ်။  
လက်ရှိ parsed လုပ်ထားတဲ့ training ဒေတာက bracket နဲ့ parsed လုပ်ထားတဲ့ format ဖြစ်နေတာကိုတွေ့ရ။  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/data.tree$ head -n 3 ./train.en 
(S (NP A/DT murder/NN) (NP case/NN) (VP (V has/VBZ)) (VP (V been/VBN)) (VP (V opened/VBN)) (P at/IN) the/DT Kyeikgyaung/NNP police/NNS (NP station/NN) ./.)
(S Police/NNS (VP (V are/VBP)) (VP (V investigating/VBG)) ./.)
(S Tatmadaw/NNP troops/NNS (VP (V seized/VBD)) arms/NNS and/CC (NP illegal/JJ timber/NN) (PP (P from/IN) (NP a/DT vehicle/NN)) (PP (P during/IN) (NP a/DT surprise/NN)) (NP check/NN) (P in/IN) Tarmoenyae/NNP (P in/IN) northern/JJ Shan/NNP (NP state/NN) (NP yesterday/NN) ./.)
```

## Format Conversion

Bracket format ကနေ XML tag format အဖြစ်ပြောင်းဖို့ tool program တွေက moses မှာ wrapper အနေနဲ့ ပါပါတယ်။ သို့သော် SMT experiment အတွက် NLTK parser ရဲ့ output ကို ဒီ wrapper နဲ့ တကယ်တမ်း အဆင်ပြေ မပြေဆိုတာကတော့ လေ့လာဖို့ လိုအပ်လိမ့်မယ်...  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesbin/ubuntu-17.04/moses/scripts/training/wrappers$ ls
adam-suffix-array                 madamira-wrapper.perl                 make-factor-en-pos.mxpost.perl    parse-de-berkeley.perl  senna2brackets.py
berkeleyparsed2mosesxml.perl      mada-wrapper.perl                     make-factor-pos.tree-tagger.perl  parse-de-bitpar.perl    syntax-hyphen-splitting.perl
berkeleyparsed2mosesxml_PTB.perl  make-factor-brown-cluster-mkcls.perl  make-factor-stem.perl             parse-en-bllip.perl     tagger-german-chunk.perl
conll2mosesxml.py                 make-factor-de-lemma.perl             make-factor-suffix.perl           parse-en-collins.perl   tree-converter-mosesxml.sh
filter-excluded-lines.perl        make-factor-de-morph.perl             morfessor-wrapper.perl            parse-en-egret.perl
find-unparseable.perl             make-factor-de-pos.perl               mosesxml2berkeleyparsed.perl      parse-en-senna.perl
madamira-tok.perl                 make-factor-en-porter.perl            mosesxml2brackets.py              parse-en-stanford.py
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/mosesbin/ubuntu-17.04/moses/scripts/training/wrappers$
```

berkeleyparsed2mosesxml.perl နဲ့ ပြောင်းတဲ့ ပုံစံ ဥပမာကတော့ အောက်ပါအတိုင်းပါ  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/data.tree$ head -n 3 test.en | perl /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/training/wrappers/berkeleyparsed2mosesxml.perl 
<tree label="S"> It/PRP <tree label="VP"> <tree label="V"> has/VBZ </tree> </tree> <tree label="VP"> <tree label="V"> been/VBN </tree> </tree> <tree label="VP"> <tree label="V"> confirmed/VBN </tree> </tree> <tree label="P"> that/IN </tree> eight/CD <tree label="VP"> <tree label="V"> thoroughbred/VBD </tree> <tree label="NP"> race/NN </tree> </tree> horses/NNS <tree label="P"> at/IN </tree> Randwick/NNP Racecourse/NNP <tree label="P"> in/IN </tree> Sydney/NNP <tree label="VP"> <tree label="V"> have/VBP </tree> </tree> <tree label="VP"> <tree label="V"> been/VBN </tree> </tree> <tree label="VP"> <tree label="V"> infected/VBN </tree> <tree label="PP"> <tree label="P"> with/IN </tree> <tree label="NP"> equine/JJ influenza/NN </tree> </tree> </tree> ./. </tree>
<tree label="S"> Randwick/NNP <tree label="VP"> <tree label="V"> has/VBZ </tree> </tree> <tree label="VP"> <tree label="V"> been/VBN </tree> </tree> <tree label="VP"> <tree label="V"> locked/VBN </tree> </tree> down/RP ,/, and/CC <tree label="VP"> <tree label="V"> is/VBZ </tree> </tree> <tree label="VP"> <tree label="V"> expected/VBN </tree> </tree> to/TO <tree label="VP"> <tree label="V"> remain/VB </tree> </tree> so/RB <tree label="P"> for/IN </tree> <tree label="P"> up/IN </tree> to/TO two/CD months/NNS ./. </tree>
<tree label="S"> It/PRP <tree label="VP"> <tree label="V"> is/VBZ </tree> </tree> <tree label="VP"> <tree label="V"> expected/VBN </tree> <tree label="PP"> <tree label="P"> that/IN </tree> <tree label="NP"> the/DT virulent/NN </tree> </tree> <tree label="NP"> flu/NN </tree> </tree> will/MD <tree label="VP"> <tree label="V"> affect/VB </tree> <tree label="NP"> the/DT majority/NN </tree> </tree> <tree label="P"> of/IN </tree> the/DT 700/CD horses/NNS <tree label="VP"> <tree label="V"> stabled/VBN </tree> </tree> <tree label="P"> at/IN </tree> Randwick/NNP ./. </tree>
```

အောက်ပါအတိုင်း အင်္ဂလိပ်စာ training/development/test data အားလုံးကို format conversion လုပ်ခဲ့တယ်။  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/data.tree/original.tree$ ls
dev.en  test.en  train.en

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/data.tree/original.tree$ cat train.en | perl /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/training/wrappers/berkeleyparsed2mosesxml.perl > ../train.en

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/data.tree/original.tree$ cat dev.en | perl /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/training/wrappers/berkeleyparsed2mosesxml.perl > ../dev.en

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/data.tree/original.tree$ cat test.en | perl /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/training/wrappers/berkeleyparsed2mosesxml.perl > ../test.en
```

SMT/NMT experiment တွေလုပ်တဲ့အခါမှာ data preparation အဆင့်ကနေ နောက်ပိတ်ဆုံး testing/evauation အဆင့်အထိ log ဖိုင်တွေက အဆင့်ဆင့်ရှိပါလိမ့်မယ်။ Error ရှိတယ်လို့ ယူဆရင်၊ BLEU score ဘာညာက တအားနည်းနေရင် အဲဒီ log ဖိုင်တွေကို အဆင့်ဆင့်ကြည့်ပြီး debug လုပ်ကြရပါတယ်...  

ဒီ tree-to-string expeirment ကို WAT2021 share task data (English-Myanmar parallel data) နဲ့ လုပ်ကြည့်တဲ့အခါမှာလည်း အရမ်းကြာနေတာ... ရလဒ်က မကောင်းတာကို တောက်လျှောက် တွေ့ရပါတယ်။  
ဒီ error log ဖိုင်က အဲဒီလိုလက်တွေ့ တွေ့ရတဲ့ error တွေကို debug လုပ်တာ၊ ရလဒ် အပြောင်းအလဲ တချို့ ရှိတာ၊ tree-to-string experiment က လက်တွေ့မှာ ခက်တာတွေကို မှတ်တမ်းအနေနဲ့ log လုပ်ထားတာ ဖြစ်ပါတယ်။ အောက်ပါ အဆင့်တွေ ကနေ တချို့ အသုံးဝင်မယ့် information တချို့ကို ရရှိပါလိမ့်မယ်။  

## Check log file

mert.log ဖိုင်မှာတော့ အောက်ပါအတိုင်း  tuning ကို 2 iteration အထိတော့ လုပ်သွားပုံရတယ်။  
ERROR message မရှိဘူး။  

```console
Name:moses_chart        VmPeak:1175656 kB       VmRSS:197696 kB RSSMax:801380 kB        user:11.596     sys:16.548      CPU:28.144      real:17.031
The decoder returns the scores in this order: LM0 WordPenalty0 PhrasePenalty0 TranslationModel0 TranslationModel0 TranslationModel0 TranslationModel0 TranslationModel1
Executing: gzip -f run2.best100.out
Scoring the nbestlist.
exec: /home/ye/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/tuning/mert/extractor.sh
Executing: /home/ye/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/tuning/mert/extractor.sh > extract.out 2> extract.err
Executing: \cp -f init.opt run2.init.opt
exec: /home/ye/tool/mosesbin/ubuntu-17.04/moses/bin/mert -d 8  --sctype BLEU --scconfig case:true --ffile run1.features.dat,run2.features.dat --scfile run1.scores.dat,run2.scores.dat --ifile run2.init.opt -n 20 -r 2000 --threads 8
Executing: /home/ye/tool/mosesbin/ubuntu-17.04/moses/bin/mert -d 8  --sctype BLEU --scconfig case:true --ffile run1.features.dat,run2.features.dat --scfile run1.scores.dat,run2.scores.dat --ifile run2.init.opt -n 20 -r 2000 --threads 8 > mert.out 2> mert.log
Executing: \cp -f extract.err run2.extract.err
Executing: \cp -f extract.out run2.extract.out
Executing: \cp -f mert.out run2.mert.out
Executing: \cp -f mert.log run2.mert.log
Executing: touch mert.log run2.mert.log
Executing: \cp -f weights.txt run2.weights.txt
run 2 end at ၂၀၂၁ မတ် ၃၁ ဗုဒ္ဓဟူး ၀၄:၄၃:၁၂ နံနက် +0630
None of the weights changed more than 1e-05. Stopping.
Executing: \cp -f init.opt run2.init.opt
(2) BEST at 2: 0 0 0 0 0 0 0 0 => 0 at ၂၀၂၁ မတ် ၃၁ ဗုဒ္ဓဟူး ၀၄:၄၃:၁၂ နံနက် +0630
Executing: \cp -f mert.log run2.mert.log
featlist: LM0=0
featlist: WordPenalty0=0
featlist: PhrasePenalty0=0
featlist: TranslationModel0=0
featlist: TranslationModel0=0
featlist: TranslationModel0=0
featlist: TranslationModel0=0
featlist: TranslationModel1=0
Parsing --decoder-flags: |-threads 8 -max-chart-span 1000|
Saving new config to: ./moses.ini
Saved: ./moses.ini
1-10.20.2 0.2 0.2 0.2-1000.5Training finished at ၂၀၂၁ မတ် ၃၁ ဗုဒ္ဓဟူး ၀၄:၄၃:၁၂ နံနက် +0630
```

ကျောင်းသူ ဇာဇာလှိုင် report ထဲမှာ ပြောခဲ့သလိုပဲ input က English ကို output ကလည်း English ပဲ ပြန်ထွက်နေတယ်။  
tunning 1, 2 ရဲ့ translated output ၁၀ကြောင်းစီက အောက်ပါအတိုင်း ...  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/tuning/mert$ head run1.out
``/`` Though/IN we/PRP are/VBP sad/JJ for/IN his/PRP$ loss/NN ,/, he/PRP left/VBD a/DT legacy/NN that/WDT will/MD inflame/VB the/DT enemy/NN nation/NN and/CC religion/NN ./. &apos;&apos;/&apos;&apos;
It/PRP is/VBZ speculated/VBN that/IN he/PRP was/VBD hit/VBN by/IN a/DT United/NNP States/NNPS missile/NN ,/, which/WDT is/VBZ now/RB identified/VBN as/IN being/VBG fired/VBN from/IN a/DT Predator/NNP drone/NN ,/, in/IN the/DT North/NNP Waziristan/NNP of/IN Pakistan/NNP ,/, and/CC a/DT dozen/NN more/JJR militants/NNS were/VBD also/RB reported/VBN dead/JJ ./.
``/`` The/DT missile/NN appeared/VBD to/TO have/VB been/VBN fired/VBN by/IN a/DT drone/NN ,/, &apos;&apos;/&apos;&apos; said/VBD a/DT Pakistani/NNP intelligence/NN official/NN ./.
``/`` They/PRP do/VBP have/VB an/DT ability/NN to/TO regenerate/VB and/CC replace/VB these/DT guys/NNS ,/, &apos;&apos;/&apos;&apos; said/VBD a/DT Western/JJ intelligence/NN official/NN ./.
Al-Libi/NNP is/VBZ said/VBD to/TO have/VB been/VBN the/DT third/JJ highest/JJS ranking/JJ member/NN of/IN al-Qaeda/NN ./.
The/DT Government/NNP of/IN Pakistan/NNP said/VBD they/PRP did/VBD not/RB know/VB about/IN his/PRP$ death/NN ./.
The/DT details/NNS of/IN the/DT death/NN have/VBP not/RB yet/RB been/VBN fully/RB released/VBN ./.
Both/DT teams/NNS entered/VBD Sunday/NNP &apos;s/POS match/NN with/IN a/DT seven-game/JJ unbeaten/JJ streak/NN to/TO give/VB them/PRP the/DT chance/NN to/TO take/VB the/DT final/JJ playoff/NN spot/NN ./.
In/IN the/DT end/NN ,/, Chicago/NNP Fire/NNP beat/NN Los/NNP Angeles/NNP Galaxy/NNP to/TO take/VB the/DT last/JJ playoff/NN spot/NN ./.
Chicago/NNP Fire/NNP controlled/VBD the/DT game/NN as/IN they/PRP outshot/VBP Los/NNP Angeles/NNP Galaxy/NNP 22-5/CD ./.
```

tuning iteration no. 2 ရဲ့ output ဖိုင်ကိုလည်း စစ်ကြည့်ခဲ့...  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/tuning/mert$ head run2.out
``/`` Though/IN we/PRP are/VBP sad/JJ for/IN his/PRP$ loss/NN ,/, he/PRP left/VBD a/DT legacy/NN that/WDT will/MD inflame/VB the/DT enemy/NN nation/NN and/CC religion/NN ./. &apos;&apos;/&apos;&apos;
It/PRP is/VBZ speculated/VBN that/IN he/PRP was/VBD hit/VBN by/IN a/DT United/NNP States/NNPS missile/NN ,/, which/WDT is/VBZ now/RB identified/VBN as/IN being/VBG fired/VBN from/IN a/DT Predator/NNP drone/NN ,/, in/IN the/DT North/NNP Waziristan/NNP of/IN Pakistan/NNP ,/, and/CC a/DT dozen/NN more/JJR militants/NNS were/VBD also/RB reported/VBN dead/JJ ./.
``/`` The/DT missile/NN appeared/VBD to/TO have/VB been/VBN fired/VBN by/IN a/DT drone/NN ,/, &apos;&apos;/&apos;&apos; said/VBD a/DT Pakistani/NNP intelligence/NN official/NN ./.
``/`` They/PRP do/VBP have/VB an/DT ability/NN to/TO regenerate/VB and/CC replace/VB these/DT guys/NNS ,/, &apos;&apos;/&apos;&apos; said/VBD a/DT Western/JJ intelligence/NN official/NN ./.
Al-Libi/NNP is/VBZ said/VBD to/TO have/VB been/VBN the/DT third/JJ highest/JJS ranking/JJ member/NN of/IN al-Qaeda/NN ./.
The/DT Government/NNP of/IN Pakistan/NNP said/VBD they/PRP did/VBD not/RB know/VB about/IN his/PRP$ death/NN ./.
The/DT details/NNS of/IN the/DT death/NN have/VBP not/RB yet/RB been/VBN fully/RB released/VBN ./.
Both/DT teams/NNS entered/VBD Sunday/NNP &apos;s/POS match/NN with/IN a/DT seven-game/JJ unbeaten/JJ streak/NN to/TO give/VB them/PRP the/DT chance/NN to/TO take/VB the/DT final/JJ playoff/NN spot/NN ./.
In/IN the/DT end/NN ,/, Chicago/NNP Fire/NNP beat/NN Los/NNP Angeles/NNP Galaxy/NNP to/TO take/VB the/DT last/JJ playoff/NN spot/NN ./.
Chicago/NNP Fire/NNP controlled/VBD the/DT game/NN as/IN they/PRP outshot/VBP Los/NNP Angeles/NNP Galaxy/NNP 22-5/CD ./.
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/tuning/mert$
```

## Faild to Build the Rule Table

tree-to-string, string-to-tree, tree-to-tree SMT experiment မှာက PBSMT ရဲ့ phrase table လိုပဲ rule table ဆိုတာ ရှိတယ်။ အဲဒီ rule table ကို ဆောက်မပေးနိုင်တာကို အောက်ပါအတိုင်း တွေ့ရ။  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/training/model$ wc ./rule-table.gz 
 0  0 20 ./rule-table.gz
```

XML format ကို PTB အဖြစ် ပြောင်းပြီး run ကြည့်ရင်ကော... ?!   

## Changing English tree data into PTB

XML tag parsing လုပ်တဲ့ tool တွေထဲမှာ berkeleyparsed2mosesxml_PTB.perl ဆိုတဲ့ wrapper လည်း ရှိသေးတယ်။  
ဘာတွေကွာတာလဲ?!  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/data.tree$ cat ./original.tree/train.en.parse | perl /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/training/wrappers/berkeleyparsed2mosesxml_PTB.perl > ./train.en
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/data.tree$ cat ./original.tree/dev.en.parse | perl /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/training/wrappers/berkeleyparsed2mosesxml_PTB.perl > ./dev.en
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/data.tree$ cat ./original.tree/test.en.parse | perl /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/training/wrappers/berkeleyparsed2mosesxml_PTB.perl > ./test.en
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/data.tree$ head -n 1 *.en
==> dev.en <==
<tree label="S"> &quot;/&quot; <tree label="P"> Though/IN </tree> we/PRP <tree label="VP"> <tree label="V"> are/VBP </tree> </tree> sad/JJ <tree label="P"> for/IN </tree> his/PRP$ <tree label="NP"> loss/NN </tree> ,/, he/PRP <tree label="VP"> <tree label="V"> left/VBD </tree> <tree label="NP"> a/DT legacy/NN </tree> </tree> that/WDT will/MD <tree label="VP"> <tree label="V"> inflame/VB </tree> <tree label="NP"> the/DT enemy/NN </tree> <tree label="NP"> nation/NN </tree> </tree> and/CC <tree label="NP"> religion/NN </tree> ./. &quot;/&quot; </tree>

==> test.en <==
<tree label="S"> It/PRP <tree label="VP"> <tree label="V"> has/VBZ </tree> </tree> <tree label="VP"> <tree label="V"> been/VBN </tree> </tree> <tree label="VP"> <tree label="V"> confirmed/VBN </tree> </tree> <tree label="P"> that/IN </tree> eight/CD <tree label="VP"> <tree label="V"> thoroughbred/VBD </tree> <tree label="NP"> race/NN </tree> </tree> horses/NNS <tree label="P"> at/IN </tree> Randwick/NNP Racecourse/NNP <tree label="P"> in/IN </tree> Sydney/NNP <tree label="VP"> <tree label="V"> have/VBP </tree> </tree> <tree label="VP"> <tree label="V"> been/VBN </tree> </tree> <tree label="VP"> <tree label="V"> infected/VBN </tree> <tree label="PP"> <tree label="P"> with/IN </tree> <tree label="NP"> equine/JJ influenza/NN </tree> </tree> </tree> ./. </tree>

==> train.en <==
<tree label="S"> <tree label="NP"> A/DT murder/NN </tree> <tree label="NP"> case/NN </tree> <tree label="VP"> <tree label="V"> has/VBZ </tree> </tree> <tree label="VP"> <tree label="V"> been/VBN </tree> </tree> <tree label="VP"> <tree label="V"> opened/VBN </tree> </tree> <tree label="P"> at/IN </tree> the/DT Kyeikgyaung/NNP police/NNS <tree label="NP"> station/NN </tree> ./. </tree>
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/data.tree$
```

**** တစ်ခုရှိတာက PTB ဆိုတဲ့ ဖိုင်နာမည်က မတူပေမဲ့ output က အရမ်း ကွဲပြားမှုရှိပုံ မရဘူးလို့ ထင်တယ်။ 

PTB perl script မှာက အောက်ပါလို single, double အားလုံးကို cover ဖြစ်အောင် update လုပ်ထားပုံရတယ်။  

```perl
  s/\'\'/\&quot;/g;
  s/``/\&quot;/g;
```

နောက်ပိုင်း experiment တွေအားလုံးကို PTB tree format နဲ့ပဲ ထပ် run ခဲ့တယ်။  

## Training/Tunning Again with PTB Tree Format

```console
Memory estimate for binary LM:
type     MB
probing 185 assuming -p 1.5
probing 218 assuming -r models -p 1.5
trie     84 without quantization
trie     43 assuming -q 8 -b 8 quantization 
trie     74 assuming -a 22 array pointer compression
trie     34 assuming -a 22 -q 8 -b 8 array pointer compression and quantization
=== 3/5 Calculating and sorting initial probabilities ===
Chain sizes: 1:117468 2:3554176 3:19131180 4:45563952 5:74635764 6:100454272
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
####################################################################################################
=== 4/5 Calculating and writing order-interpolated probabilities ===
Chain sizes: 1:117468 2:3554176 3:19131180 4:45563952 5:74635764 6:100454272
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
####################################################################################################
=== 5/5 Writing ARPA model ===
Name:lmplz	VmPeak:13032640 kB	VmRSS:28588 kB	RSSMax:2152644 kB	user:8.64781	sys:2.26682	CPU:10.9146	real:24.4983
Use of uninitialized value in division (/) at /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl line 139, <STDIN> line 1018.
Use of uninitialized value in division (/) at /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl line 139, <STDIN> line 1018.
Use of uninitialized value in division (/) at /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl line 139, <STDIN> line 1018.
BLEU = 0.00, 0.0/0.0/0.0/0.0 (BP=0.456, ratio=0.560, hyp_len=32989, ref_len=58895)
BLEU=0.000000	RIBES=0.000000	WER=1.020299

real	32m57.119s
user	134m46.693s
sys	21m35.443s
```

အထက်ပါအတိုင်း ရပ်သွားတာ တွေ့ရတယ်။  
model/ Folder ထဲက file size တွေကို check လုပ်ကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရ...  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/training/model$ wc *
   238014   3463768  28441812 aligned.0.en
   238014   6285996  60847350 aligned.0.my
   238014   5294762  26303989 aligned.grow-diag-final-and
        0         0        20 extract.inv.sorted.gz
        0         0        20 extract.sorted.gz
        3        45       192 glue-grammar
   518555   1555665  16595410 lex.e2f
   518555   1555665  16595410 lex.f2e
       48       102      1230 moses.ini
       46        77      1007 moses-tuned.ini
        0         0        20 rule-table.gz
  1751249  18156080 148786460 total
```

sorting လုပ်တဲ့ နေရာမှာ failed ဖြစ်နေတာလား ?!?!?!  
Reference: moses manual, page 98  

Removed: 
```console
sort-buffer-size 10G
```

Added:   
```console
--sort-batch-size 1024 --sort-compress gzip
```  

## Training/Tuning Again

စောစောကလိုပဲ extraction မှာ faild ဖြစ်တယ်လို့ ယူဆတယ်။  
အထက်မှာ ပြထားသလိုပဲ rule-table.gz, *.sorted.gz ဖိုင်တွေက file size 0 ပဲ ဖြစ်နေတယ်။  

ဒီတစ်ခါတော့ sorting နဲ့ ပတ်သက်တဲ့ option တွေကို အကုန်ဖြုတ်ထားပြီး run ကြည့်မယ်...  

Training လုပ်နေစဉ်မှာ model အောက်က ဖိုင် size တွေကို ဆက်တိုက် check လုပ်ကြည့်တော့ sorting က ပြဿနာပေးနေတာတော့ သေချာတယ်။  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/training/model$ wc *
   238014   3463768  28441812 aligned.0.en
   238014   6285996  60847350 aligned.0.my
   238014   5294762  26303989 aligned.grow-diag-final-and
        0         0        20 extract.inv.sorted.gz
        0         0        20 extract.sorted.gz
        3        45       192 glue-grammar
   518555   1555665  16595410 lex.e2f
   518555   1555665  16595410 lex.f2e
       48       102      1230 moses.ini
       46        77      1007 moses-tuned.ini
        0         0        20 rule-table.gz
wc: tmp.553155: Is a directory
        0         0         0 tmp.553155
  1751249  18156080 148786460 total
```

အချိန်စောင့်ပြီး folder ထဲက ဖိုင်တွေကို check လုပ်...  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/training/model$ wc *
   238014   3463768  28441812 aligned.0.en
   238014   6285996  60847350 aligned.0.my
   238014   5294762  26303989 aligned.grow-diag-final-and
  1386793   8006103 361940532 extract.inv.sorted.gz
  1439043   8190724 369570567 extract.sorted.gz
        3        45       192 glue-grammar
   518555   1555665  16595410 lex.e2f
   518555   1555665  16595410 lex.f2e
       48       102      1230 moses.ini
       46        77      1007 moses-tuned.ini
        0         0        20 rule-table.gz
wc: tmp.554451: Is a directory
        0         0         0 tmp.554451
wc: tmp.554452: Is a directory
        0         0         0 tmp.554452
  4577085  34352907 880297519 total
```

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/training/model$ wc *
   238014   3463768  28441812 aligned.0.en
   238014   6285996  60847350 aligned.0.my
   238014   5294762  26303989 aligned.grow-diag-final-and
  1386793   8006103 361940532 extract.inv.sorted.gz
  1439043   8190724 369570567 extract.sorted.gz
        3        45       192 glue-grammar
   518555   1555665  16595410 lex.e2f
   518555   1555665  16595410 lex.f2e
       48       102      1230 moses.ini
       46        77      1007 moses-tuned.ini
        0         0        20 rule-table.gz
    35358    199128   8970250 rule-table.half.f2e.gz
wc: tmp.554452: Is a directory
        0         0         0 tmp.554452
  4612443  34552035 889267769 total
```

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/training/model$ wc *
   238014   3463768  28441812 aligned.0.en
   238014   6285996  60847350 aligned.0.my
   238014   5294762  26303989 aligned.grow-diag-final-and
  1386793   8006103 361940532 extract.inv.sorted.gz
  1439043   8190724 369570567 extract.sorted.gz
        3        45       192 glue-grammar
   518555   1555665  16595410 lex.e2f
   518555   1555665  16595410 lex.f2e
       48       102      1230 moses.ini
       46        77      1007 moses-tuned.ini
        0         0        20 rule-table.gz
  4577085  34352907 880297519 total
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/training/model$
```

ဒီတစ်ခေါက် တိုးတက်မှုရှိတာက အောက်ပါ ဖိုင် နှစ်ဖိုင်က အိုကေသွားပုံရတယ်။  

```console
  1386793   8006103 361940532 extract.inv.sorted.gz
  1439043   8190724 369570567 extract.sorted.gz
```

File content ကို စစ်ကြည့်တော့ rule တွေလည်း ဆွဲထုတ်လို့ ရနေတာကို confirm!!!  
extract.sorted.gz ဖိုင်ထဲက ဥပမာ တချို့...  

```text
,/, [NP][X] [PP] ||| [NP][X] - ရာ စု ပင် လုံ ကျင်း ပ မ ည့် ကိစ္စ ရ ခိုင် ပြည် နယ် တွင် တည် ငြိမ် အေး ချမ်း မှု နှ င့် ဖွံ့ ဖြိုး တိုး တက် မှု မြှ င့် တင် ရေး အ တွက် ကြိုး ပမ်း ဆောင် ရွက် နေ မှု များ [X] ||| 1-0 ||| 0.0180362 ||| 
,/, [NP][X] [PP] ||| [NP][X] - ရာ စု ပင် လုံ ကျင်း ပ မ ည့် ကိစ္စ ရ ခိုင် ပြည် နယ် တွင် တည် ငြိမ် အေး ချမ်း မှု နှ င့် ဖွံ့ ဖြိုး တိုး တက် မှု မြှ င့် တင် ရေး အ တွက် ကြိုး ပမ်း ဆောင် ရွက် နေ မှု များ ဒေ [X] ||| 1-0 ||| 0.0176127 ||| 
,/, [NP][X] [PP] ||| [NP][X] - ရာ စု ပင် လုံ ကျင်း ပ မ ည့် ကိစ္စ ရ ခိုင် ပြည် နယ် တွင် တည် ငြိမ် အေး ချမ်း မှု နှ င့် ဖွံ့ ဖြိုး တိုး တက် မှု မြှ င့် တင် ရေး အ တွက် ကြိုး ပမ်း ဆောင် ရွက် နေ မှု များ ဒေ သ [X] ||| 1-0 ||| 0.0172085 ||| 
,/, [NP][X] [PP] ||| [NP][X] - ရာ စု ပင် လုံ ကျင်း ပ မ ည့် ကိစ္စ ရ ခိုင် ပြည် နယ် တွင် တည် ငြိမ် အေး ချမ်း မှု နှ င့် ဖွံ့ ဖြိုး တိုး တက် မှု မြှ င့် တင် ရေး အ တွက် ကြိုး ပမ်း ဆောင် ရွက် နေ မှု များ ဒေ သ တွင်း [X] ||| 1-0 ||| 0.0168225 ||| 
,/, [NP][X] [PP] ||| [NP][X] - ရာ စု ပင် လုံ ကျင်း ပ မ ည့် ကိစ္စ ရ ခိုင် ပြည် နယ် တွင် တည် ငြိမ် အေး ချမ်း မှု နှ င့် ဖွံ့ ဖြိုး တိုး တက် မှု မြှ င့် တင် ရေး အ တွက် ကြိုး ပမ်း ဆောင် ရွက် နေ မှု များ ဒေ သ တွင်း နှ [X] ||| 1-0 ||| 0.0164535 ||| 
,/, [NP][X] [PP] ||| [NP][X] - ရာ စု ပင် လုံ ကျင်း ပ မ ည့် ကိစ္စ ရ ခိုင် ပြည် နယ် တွင် တည် ငြိမ် အေး ချမ်း မှု နှ င့် ဖွံ့ ဖြိုး တိုး တက် မှု မြှ င့် တင် ရေး အ တွက် ကြိုး ပမ်း ဆောင် ရွက် နေ မှု များ ဒေ သ တွင်း နှ င့် [X] ||| 1-0 ||| 0.0161003 ||| 
,/, [NP][X] [PP] ||| [NP][X] - ရာ စု ပင် လုံ ကျင်း ပ မ ည့် ကိစ္စ ရ ခိုင် ပြည် နယ် တွင် တည် ငြိမ် အေး ချမ်း မှု နှ င့် ဖွံ့ ဖြိုး တိုး တက် မှု မြှ င့် တင် ရေး အ တွက် ကြိုး ပမ်း ဆောင် ရွက် နေ မှု များ ဒေ သ တွင်း နှ င့် နိုင် [X] ||| 1-0 ||| 0.0157619 ||| 
,/, [NP][X] [PP] ||| [NP][X] - ရာ စု ပင် လုံ ကျင်း ပ မ ည့် ကိစ္စ ရ ခိုင် ပြည် နယ် တွင် တည် ငြိမ် အေး ချမ်း မှု နှ င့် ဖွံ့ ဖြိုး တိုး တက် မှု မြှ င့် တင် ရေး အ တွက် ကြိုး ပမ်း ဆောင် ရွက် နေ မှု များ ဒေ သ တွင်း နှ င့် နိုင် ငံ [X] ||| 1-0 ||| 0.0154375 ||| 
,/, [NP][X] [PP] ||| [NP][X] - ရာ စု ပင် လုံ ကျင်း ပ မ ည့် ကိစ္စ ရ ခိုင် ပြည် နယ် တွင် တည် ငြိမ် အေး ချမ်း မှု နှ င့် ဖွံ့ ဖြိုး တိုး တက် မှု မြှ င့် တင် ရေး အ တွက် ကြိုး ပမ်း ဆောင် ရွက် နေ မှု များ ဒေ သ တွင်း နှ င့် နိုင် ငံ တ [X] ||| 1-0 ||| 0.0151261 ||| 
,/, [NP][X] [PP] ||| [NP][X] - ရာ စု ပင် လုံ ကျင်း ပ မ ည့် ကိစ္စ ရ ခိုင် ပြည် နယ် တွင် တည် ငြိမ် အေး ချမ်း မှု နှ င့် ဖွံ့ ဖြိုး တိုး တက် မှု မြှ င့် တင် ရေး အ တွက် ကြိုး ပမ်း ဆောင် ရွက် နေ မှု များ ဒေ သ တွင်း နှ င့် နိုင် ငံ တ ကာ [X] ||| 1-0 ||| 0.0148271 ||| 
,/, [NP][X] [PP] ||| [NP][X] - ရာ စု ပင် လုံ ကျင်း ပ မ ည့် ကိစ္စ ရ ခိုင် ပြည် နယ် တွင် တည် ငြိမ် အေး ချမ်း မှု နှ င့် ဖွံ့ ဖြိုး တိုး တက် မှု မြှ င့် တင် ရေး အ တွက် ကြိုး ပမ်း ဆောင် ရွက် နေ မှု များ ဒေ သ တွင်း နှ င့် နိုင် ငံ တ ကာ ရေး [X] ||| 1-0 ||| 0.0145397 ||| 
,/, [NP][X] [PP] ||| [NP][X] - ရာ စု ပင် လုံ ကျင်း ပ မ ည့် ကိစ္စ ရ ခိုင် ပြည် နယ် တွင် တည် ငြိမ် အေး ချမ်း မှု နှ င့် ဖွံ့ ဖြိုး တိုး တက် မှု မြှ င့် တင် ရေး အ တွက် ကြိုး ပမ်း ဆောင် ရွက် နေ မှု များ ဒေ သ တွင်း နှ င့် နိုင် ငံ တ ကာ ရေး ရာ [X] ||| 1-0 ||| 0.0142631 ||| 
,/, [NP][X] [PP] ||| [NP][X] - ရာ စု ပင် လုံ ကျင်း ပ မ ည့် ကိစ္စ ရ ခိုင် ပြည် နယ် တွင် တည် ငြိမ် အေး ချမ်း မှု နှ င့် ဖွံ့ ဖြိုး တိုး တက် မှု မြှ င့် တင် ရေး အ တွက် ကြိုး ပမ်း ဆောင် ရွက် နေ မှု များ ဒေ သ တွင်း နှ င့် နိုင် ငံ တ ကာ ရေး ရာ ကိစ္စ [X] ||| 1-0 ||| 0.013997 ||| 
,/, [NP][X] [PP] ||| [NP][X] - ရာ စု ပင် လုံ ကျင်း ပ မ ည့် ကိစ္စ ရ ခိုင် ပြည် နယ် တွင် တည် ငြိမ် အေး ချမ်း မှု နှ င့် ဖွံ့ ဖြိုး တိုး တက် မှု မြှ င့် တင် ရေး အ တွက် ကြိုး ပမ်း ဆောင် ရွက် နေ မှု များ ဒေ သ တွင်း နှ င့် နိုင် ငံ တ ကာ ရေး ရာ ကိစ္စ ရပ် [X] ||| 1-0 ||| 0.0137405 ||| 
,/, [NP][X] [PP] ||| [NP][X] - ရာ စု ပင် လုံ ကျင်း ပ မ ည့် ကိစ္စ ရ ခိုင် ပြည် နယ် တွင် တည် ငြိမ် အေး ချမ်း မှု နှ င့် ဖွံ့ ဖြိုး တိုး တက် မှု မြှ င့် တင် ရေး အ တွက် ကြိုး ပမ်း ဆောင် ရွက် နေ မှု များ ဒေ သ တွင်း နှ င့် နိုင် ငံ တ ကာ ရေး ရာ ကိစ္စ ရပ် များ [X] ||| 1-0 ||| 0.0134933 ||| 
,/, [NP][X] [PP] ||| [NP][X] - ရာ စု ပင် လုံ ကျင်း ပ မ ည့် ကိစ္စ ရ ခိုင် ပြည် နယ် တွင် တည် ငြိမ် အေး ချမ်း မှု နှ င့် ဖွံ့ ဖြိုး တိုး တက် မှု မြှ င့် တင် ရေး အ တွက် ကြိုး ပမ်း ဆောင် ရွက် နေ မှု များ ဒေ သ တွင်း နှ င့် နိုင် ငံ တ ကာ ရေး ရာ ကိစ္စ ရပ် များ အာ [X] ||| 1-0 ||| 0.0132548 ||| 
,/, [NP][X] [PP] ||| [NP][X] - ရာ စု ပင် လုံ ကျင်း ပ မ ည့် ကိစ္စ ရ ခိုင် ပြည် နယ် တွင် တည် ငြိမ် အေး ချမ်း မှု နှ င့် ဖွံ့ ဖြိုး တိုး တက် မှု မြှ င့် တင် ရေး အ တွက် ကြိုး ပမ်း ဆောင် ရွက် နေ မှု များ ဒေ သ တွင်း နှ င့် နိုင် ငံ တ ကာ ရေး ရာ ကိစ္စ ရပ် များ အာ ဆီ [X] ||| 1-0 ||| 0.0130247 ||| 
```

*** သို့သော် ပြဿနာက နောက်ဆုံး combine လုပ်ပြီးဆောက်တဲ့ rule-table.gz ရဲ့ ဖိုင် size က zero ဖြစ်နေတာကိုသွားတွေ့ရတယ်။  

--extract-options နဲ့ ပတ်သက်တဲ့ parameter တွေကြောင့်လို့ နားလည်တယ်။  
Reference: moses manual, page no. 83  

```console
  --extract-options "--MaxSpan 1000 --MinHoleSource 1 --MinWords 0 --NonTermConsecSource --AllowOnlyUnalignedWords" \
```
ကို  
```console
    --extract-options "--MinHoleSource 1 --MinWords 0 --NonTermConsecSource --AllowOnlyUnalignedWords" \ 
``` 
နဲ့ အစားထိုးပြီး ထပ် training/tuning လုပ်ကြည့်ခဲ့...  
    
## Training/Tuning Again

ဒီတစ်ခါတော့ rule-table ဆောက်လာတာကိုတွေ့ရတယ်။   

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/training/model$ wc *
   238014   3463768  28441812 aligned.0.en
   238014   6285996  60847350 aligned.0.my
   238014   5294762  26303989 aligned.grow-diag-final-and
   226200   1304573  59036406 extract.inv.sorted.gz
   229819   1290217  58004830 extract.sorted.gz
        3        45       192 glue-grammar
   518555   1555665  16595410 lex.e2f
   518555   1555665  16595410 lex.f2e
       48       102      1230 moses.ini
       46        77      1007 moses-tuned.ini
   503677   2783535 129475054 rule-table.gz
  2710945  23534405 395302690 total
```
rule-table.gz ဖိုင်ကို ဝင်ကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရ...  

```console
%/NN [NP] ||| - ၂၀၁၁ မှာ ၅၃ . ၁၆ % [X] ||| 0.0239796 0.686515 5.45775e-06 2.28377e-25 ||| 0-6 ||| 0.209524 920.582 0.142857 ||| |||
%/NN [NP] ||| - ၂၀၁၁ မှာ ၅၃ . ၁၆ % သာ [X] ||| 0.0197833 0.686515 2.72888e-06 5.11358e-28 ||| 0-6 ||| 0.126984 920.582 0.0714286 ||| |||
%/NN [NP] ||| . ၀ % [X] ||| 0.0351702 0.686515 1.27348e-05 1.45365e-09 ||| 0-2 ||| 0.333333 920.582 0.333333 ||| |||
%/NN [NP] ||| . ၀ ရာ ခိုင် နှုန်း [X] ||| 0.0351702 0.0953001 2.03756e-05 1.22101e-10 ||| 0-2 0-3 0-4 ||| 0.533333 920.582 0.533333 ||| |||
%/NN [NP] ||| . ၀ ရာ ခိုင် နှုန်း ရှိ [X] ||| 0.0351702 0.0953001 6.36739e-06 1.50283e-12 ||| 0-2 0-3 0-4 ||| 0.166667 920.582 0.166667 ||| |||
%/NN [NP] ||| . ၁ ရာ [X] ||| 0.0351702 0.0127721 3.82043e-05 1.09201e-08 ||| 0-2 ||| 0.999999 920.582 0.999999 ||| |||
%/NN [NP] ||| . ၁ ရာ ခိုင် [X] ||| 0.0351702 0.0127721 1.91022e-05 6.70056e-12 ||| 0-2 ||| 0.500001 920.582 0.500001 ||| |||
%/NN [NP] ||| . ၁ ရာ ခိုင် နှုန်း [X] ||| 0.0219814 0.0127721 1.27348e-05 2.47452e-15 ||| 0-2 ||| 0.533333 920.582 0.333333 ||| |||
%/NN [NP] ||| . ၁ ရာ ခိုင် နှုန်း မှ ၂၅ . ၅ ရာ [X] ||| 0.0351702 0.0127721 3.82043e-06 5.28729e-32 ||| 0-9 ||| 0.1 920.582 0.1 ||| |||
%/NN [NP] ||| . ၁ ရာ ခိုင် နှုန်း ရှိ [X] ||| 0.0117234 0.0127721 3.18369e-06 3.04566e-17 ||| 0-2 ||| 0.25 920.582 0.0833333 ||| |||
%/NN [NP] ||| . ၁၆ % [X] ||| 0.0351702 0.686515 2.54695e-05 7.57403e-10 ||| 0-2 ||| 0.666666 920.582 0.666666 ||| |||
%/NN [NP] ||| . ၁၆ % သာ [X] ||| 0.0351702 0.686515 6.36739e-06 1.6959e-12 ||| 0-2 ||| 0.166667 920.582 0.166667 ||| |||
%/NN [NP] ||| . ၂ ရာ ခိုင် နှုန်း [X] ||| 0.0166699 0.0953001 1.27348e-05 7.03761e-10 ||| 0-2 0-3 0-4 ||| 0.703268 920.582 0.333333 ||| |||
%/NN [NP] ||| . ၂ ရာ ခိုင် နှုန်း ကို [X] ||| 0.0351702 0.0953001 6.36739e-06 1.98347e-11 ||| 0-2 0-3 0-4 ||| 0.166667 920.582 0.166667 ||| |||
%/NN [NP] ||| . ၄ ရာ [X] ||| 0.0188411 0.0127721 3.82043e-05 6.15533e-09 ||| 0-2 ||| 1.86667 920.582 0.999999 ||| |||
%/NN [NP] ||| . ၄ ရာ ခိုင် [X] ||| 0.0190265 0.0127721 1.91022e-05 3.77691e-12 ||| 0-2 ||| 0.924244 920.582 0.500001 ||| |||
%/NN [NP] ||| . ၄ ရာ ခိုင် နှုန်း [X] ||| 0.0232945 0.0127721 1.27348e-05 1.39481e-15 ||| 0-2 ||| 0.503268 920.582 0.333333 ||| |||
%/NN [NP] ||| . ၄ ရာ ခိုင် နှုန်း တို့ [X] ||| 0.0351702 0.0127721 3.18369e-06 8.08294e-18 ||| 0-2 ||| 0.0833333 920.582 0.0833333 ||| |||
%/NN [NP] ||| . ၄ ရာ ခိုင် နှုန်း တို့ ထက် [X] ||| 0.0351702 0.0127721 2.54695e-06 4.83925e-21 ||| 0-2 ||| 0.0666667 920.582 0.0666667 ||| |||
%/NN [NP] ||| . ၄ ရာ ခိုင် နှုန်း ဖြစ် [X] ||| 0.0139468 0.0127721 3.18369e-06 1.53307e-17 ||| 0-2 ||| 0.210145 920.582 0.0833333 ||| |||
%/NN [NP] ||| . ၄ ရာ ခိုင် နှုန်း သည် [X] ||| 0.0351702 0.0127721 3.18369e-06 1.87065e-17 ||| 0-2 ||| 0.0833333 920.582 0.0833333 ||| |||
%/NN [NP] ||| . ၄ ရာ ခိုင် နှုန်း သည် အ [X] ||| 0.0351702 0.0127721 2.54695e-06 1.73241e-18 ||| 0-2 ||| 0.0666667 920.582 0.0666667 ||| |||
%/NN [NP] ||| . ၅ ရာ [X] ||| 0.359346 0.0127721 0.000563832 7.63451e-09 ||| 0-2 ||| 1.44444 920.582 1.33333 ||| |||
%/NN [NP] ||| . ၅ ရာ ခိုင် [X] ||| 0.0315319 0.0127721 2.54696e-05 4.68454e-12 ||| 0-2 ||| 0.743591 920.582 0.666668 ||| |||
%/NN [NP] ||| . ၅ ရာ ခိုင် နှုန်း [X] ||| 0.0310593 0.0127721 1.69797e-05 1.73e-15 ||| 0-2 ||| 0.503268 920.582 0.444444 ||| |||
%/NN [NP] ||| . ၅ ရာ ခိုင် နှုန်း သည် [X] ||| 0.0351702 0.0127721 3.18369e-06 2.32019e-17 ||| 0-2 ||| 0.0833333 920.582 0.0833333 ||| |||
%/NN [NP] ||| . ၆ ရာ [X] ||| 0.0140681 0.0127721 2.54695e-05 5.82132e-09 ||| 0-2 ||| 1.66666 920.582 0.666666 ||| |||
%/NN [NP] ||| . ၆ ရာ ခိုင် [X] ||| 0.0140681 0.0127721 1.27348e-05 3.57196e-12 ||| 0-2 ||| 0.833335 920.582 0.333334 ||| |||
%/NN [NP] ||| . ၆ ရာ ခိုင် နှုန်း [X] ||| 0.00879255 0.0127721 4.24492e-06 1.31912e-15 ||| 0-2 ||| 0.444444 920.582 0.111111 ||| |||
%/NN [NP] ||| . ၆ ရာ ခိုင် နှုန်း သို့ [X] ||| 0.0351702 0.0127721 3.18369e-06 4.9053e-18 ||| 0-2 ||| 0.0833333 920.582 0.0833333 ||| |||
%/NN [NP] ||| . ၇ ရာ [X] ||| 0.0351702 0.0127721 2.54695e-05 6.32574e-09 ||| 0-2 ||| 0.666666 920.582 0.666666 ||| |||
%/NN [NP] ||| . ၇ ရာ ခိုင် [X] ||| 0.0351702 0.0127721 1.27348e-05 3.88147e-12 ||| 0-2 ||| 0.333334 920.582 0.333334 ||| |||
%/NN [NP] ||| . ၇ ရာ ခိုင် နှုန်း [X] ||| 0.0351702 0.0127721 4.24492e-06 1.43343e-15 ||| 0-2 ||| 0.111111 920.582 0.111111 ||| |||
%/NN [NP] ||| . ၈ % ) [X] ||| 0.0351702 0.686515 1.27348e-05 5.10228e-12 ||| 0-2 ||| 0.333334 920.582 0.333334 ||| |||
%/NN [NP] ||| . ၈ % ) သို့ [X] ||| 0.0351702 0.686515 8.48983e-06 1.89733e-14 ||| 0-2 ||| 0.222222 920.582 0.222222 ||| |||
```

သို့သော် process pipeline အစအဆုံးမပြီးသေး အောက်ပါအတိုင်း ERROR ကို တွေ့ရ...  

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/tuning$ tail -n 5 ./mert.log 
...
...
...
 [18,20]=X (1) [18,21]=X (1) [18,22]=X (1) [18,23]=X (1) [18,24]=X (1) [18,25]=X (1) [18,26]=X (1) [18,27]=X (1) [18,28]=X (1) [18,29]=X (1) [18,30]=X (1) [18,31]=X (1) [19,19]=X (1) [19,20]=X (1) [19,21]=X (1) [19,22]=X (1) [19,23]=X (1) [19,24]=X (1) [19,25]=X (1) [19,26]=X (1) [19,27]=X (1) [19,28]=X (1) [19,29]=X (1) [19,30]=X (1) [19,31]=X (1) [20,20]=X (1) [20,21]=X (1) [20,22]=X (1) [20,23]=X (1) [20,24]=X (1) [20,25]=X (1) [20,26]=X (1) [20,27]=X (1) [20,28]=X (1) [20,29]=X (1) [20,30]=X (1) [20,31]=X (1) [21,21]=X (1) [21,21]=P (1) [21,22]=X (1) [21,23]=X (1) [21,23]=PP (1) [21,24]=X (1) [21,25]=X (1) [21,26]=X (1) [21,27]=X (1) [21,28]=X (1) [21,29]=X (1) [21,30]=X (1) [21,31]=X (1) [22,22]=X (1) [22,23]=X (1) [22,23]=NP (1) [22,24]=X (1) [22,25]=X (1) [22,26]=X (1) [22,27]=X (1) [22,28]=X (1) [22,29]=X (1) [22,30]=X (1) [22,31]=X (1) [23,23]=X (1) [23,24]=X (1) [23,25]=X (1) [23,26]=X (1) [23,27]=X (1) [23,28]=X (1) [23,29]=X (1) [23,30]=X (1) [23,31]=X (1) [24,24]=X (1) [24,25]=X (1) [24,26]=X (1) [24,27]=X (1) [24,28]=X (1) [24,29]=X (1) [24,30]=X (1) [24,31]=X (1) [25,25]=X (1) [25,26]=X (1) [25,26]=NP (1) [25,27]=X (1) [25,28]=X (1) [25,29]=X (1) [25,30]=X (1) [25,31]=X (1) [26,26]=X (1) [26,27]=X (1) [26,28]=X (1) [26,29]=X (1) [26,30]=X (1) [26,31]=X (1) [27,27]=X (1) [27,27]=NP (1) [27,28]=X (1) [27,29]=X (1) [27,30]=X (1) [27,31]=X (1) [28,28]=X (1) [28,29]=X (1) [28,29]=NP (1) [28,30]=X (1) [28,31]=X (1) [29,29]=X (1) [29,30]=X (1) [29,31]=X (1) [30,30]=X (1) [30,31]=X (1) [31,31]=X (1) 
Killed
Exit code: 137
The decoder died. CONFIG WAS -weight-overwrite 'PhrasePenalty0= 0.001951 TranslationModel0= 0.001951 0.001951 0.001951 0.001951 WordPenalty0= -0.009756 TranslationModel1= -0.975610 LM0= 0.004878' 
```

STDIO မှာ ပေးတဲ့ message က အောက်ပါအတိုင်း...  

```console
probing 185 assuming -p 1.5
probing 218 assuming -r models -p 1.5
trie     84 without quantization
trie     43 assuming -q 8 -b 8 quantization 
trie     74 assuming -a 22 array pointer compression
trie     34 assuming -a 22 -q 8 -b 8 array pointer compression and quantization
=== 3/5 Calculating and sorting initial probabilities ===
Chain sizes: 1:117468 2:3554176 3:19131180 4:45563952 5:74635764 6:100454272
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
####################################################################################################
=== 4/5 Calculating and writing order-interpolated probabilities ===
Chain sizes: 1:117468 2:3554176 3:19131180 4:45563952 5:74635764 6:100454272
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
####################################################################################################
=== 5/5 Writing ARPA model ===
Name:lmplz	VmPeak:13032640 kB	VmRSS:28552 kB	RSSMax:2152680 kB	user:8.65769	sys:2.38937	CPU:11.0471	real:24.3283
mkdir: cannot create directory ‘work.en-my/output’: File exists
./t2s.sh: line 107: 557608 Killed                  ${MOSES_BIN}/moses_chart -config ${MODEL_DIR}/moses-tuned.ini -max-chart-span 1000 -threads ${JOBS} -inputtype 3 < ${TEST} > ${outfile} 2> ${outfile}.log
Use of uninitialized value in division (/) at /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl line 139, <STDIN> line 13.
BLEU = 0.00, 15.3/1.9/0.3/0.0 (BP=1.000, ratio=1.828, hyp_len=1108, ref_len=606)
BLEU=0.000000	RIBES=0.297547	WER=1.726437

real	7m11.980s
user	20m23.466s
sys	0m27.315s
```

*** ဒီတစ်ခေါက်တော့ -threads ကိုပါ ဖြုတ်ပြီး ထပ် run ကြည့်မယ်။  

```console
${MOSES_BIN}/moses_chart -config ${MODEL_DIR}/moses-tuned.ini -inputtype 3 < ${TEST} > ${outfile} 2> ${outfile}.log
```

## Training/Tuning Again

```console

                    200  79  93 200 166  79 147  53  59  56  60  54  62   0
                      200  54 194 200  85 137  54  61  49  52  64  70   0
                        200 131 202  90 141  50  59  52  44  56  87   0
                          200 157  41 133  67  61  53  45  59  72   0
                            180  89  84 128  71  49  46  56  58   0
                              200 145  81 117  65  44  63  54   0
                                129  55  79  82  55  70  71   0
                                  194  75  65  64 101  87   0
                                    200  58  57 119 128   0
                                      196  54  89 169   0
                                        188  57 113   0
                                          200  82   0
                                            200   0
                                                1
BEST TRANSLATION: 565227 S  -> S </s> :0-0 : term=1-1 : nonterm=0-0 : c=-0.018 core=(0.000,-1.000,1.000,0.000,0.000,0.000,0.000,0.000,0.000)  [0..23] 563645 [total=-601.815] core=(-600.000,-28.000,39.000,-78.429,-54.963,-58.760,-24.729,1.000,-156.980)
Line 26Killed
Exit code: 137
The decoder died. CONFIG WAS -weight-overwrite 'PhrasePenalty0= 0.001951 LM0= 0.004878 TranslationModel1= -0.975610 TranslationModel0= 0.001951 0.001951 0.001951 0.001951 WordPenalty0= -0.009756'
```

**** Tuning Step No. 2 မှာ ရပ်သွားတယ်။ အဲဒါ ဘာကြောင့်လဲ ဆိုတာကို သိအောင် ကြိုးစားရလိမ့်မယ်။

အဲဒီ 2 iteration tuned tree-to-string model နဲ့ပဲ test input English ဖိုင်ကို အစအဆုံး ပြန်ပေးနိုင်လားနဲ့ BLEU score ကို checking ... လုပ်ခဲ့ အောက်ပါ ရလဒ် ကို တွေ့ရ...  

```console
1 9789 D1=0.722244 D2=1.10259 D3+=1.08703
2 222136 D1=0.67195 D2=1.06259 D3+=1.44678
3 956559 D1=0.770592 D2=1.1215 D3+=1.34752
4 1898498 D1=0.833995 D2=1.18933 D3+=1.33204
5 2665563 D1=0.877419 D2=1.26852 D3+=1.38285
6 3139196 D1=0.582375 D2=1.71726 D3+=1.66681
Memory estimate for binary LM:
type     MB
probing 185 assuming -p 1.5
probing 218 assuming -r models -p 1.5
trie     84 without quantization
trie     43 assuming -q 8 -b 8 quantization 
trie     74 assuming -a 22 array pointer compression
trie     34 assuming -a 22 -q 8 -b 8 array pointer compression and quantization
=== 3/5 Calculating and sorting initial probabilities ===
Chain sizes: 1:117468 2:3554176 3:19131180 4:45563952 5:74635764 6:100454272
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
####################################################################################################
=== 4/5 Calculating and writing order-interpolated probabilities ===
Chain sizes: 1:117468 2:3554176 3:19131180 4:45563952 5:74635764 6:100454272
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
####################################################################################################
=== 5/5 Writing ARPA model ===
Name:lmplz	VmPeak:13032640 kB	VmRSS:28480 kB	RSSMax:2152632 kB	user:8.90507	sys:2.25423	CPU:11.1593	real:24.9991
mkdir: cannot create directory ‘work.en-my/output’: File exists
BLEU = 1.51, 17.1/2.6/0.7/0.2 (BP=1.000, ratio=1.855, hyp_len=109271, ref_len=58895)
BLEU=0.015136	RIBES=0.309893	WER=1.735291

real	54m9.279s
user	60m3.523s
sys	0m33.632s
```

```console
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/output$ wc *
    1018   109271  1042311 test.out
   43272  2818960 18677336 test.out.log
   44290  2928231 19719647 total
```

*** တိုးတက်မှုတော့ ရှိတယ်။ Training/Tuning/Testing/Evaluation pipeline အားလုံး အစအဆုံး လုပ်သွားပုံရတယ်။ :)  
*** Score ကတော့ မကောင်းသေးဘူး...  


## Update t2s.sh and Training/Tunning/Testing Again

#!/bin/bash

## Tree to String SMT with moses
## Written by Ye, LST, NECTEC, Thailand
## Preparation for WAT2021 MT Share Task
## This shell script referred: http://orchid.kuee.kyoto-u.ac.jp/WAT/WAT2017/baseline/baselineSystemTree2String.html
## Last updated: 30 Mar 2021
##
## If you want to run this shell script you will need parallel corpus including tree parsed SOURCE data,
## moses SMT toolkit: https://github.com/moses-smt/mosesdecoder
## mgiza alignment tool: https://github.com/moses-smt/mgiza

## Variables preparations for data, script and path
SOURCE=en
TARGET=my
EXP_DIR=/home/ye/exp/smt/wat2021/tree-smt/tree2string
LM=${EXP_DIR}/data.tok/train
CORPUS=${EXP_DIR}/data.tree/train
DEV_SOURCE=${EXP_DIR}/data.tree/dev.${SOURCE}
DEV_TARGET=${EXP_DIR}/data.tok/dev.${TARGET}
TEST=${EXP_DIR}/data.tree/test.${SOURCE}
REF=${EXP_DIR}/data.tok/test.${TARGET}
LM_ORDER=6
JOBS=8

MOSES_SCRIPT=/home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts
MOSES_BIN=/home/ye/tool/mosesbin/ubuntu-17.04/moses/bin
#EXT_BIN=/home/ye/tool/mgiza/mgizapp/bin/
EXT_BIN=/home/ye/tool/mosesbin/ubuntu-17.04/training-tools

WORK_DIR=work.${SOURCE}-${TARGET}
TRAINING_DIR=${WORK_DIR}/training
MODEL_DIR=${WORK_DIR}/training/model

## Optional tool for evaluation
## https://github.com/odashi/mteval
MTEVAL_DIR=/home/ye/tool/mteval/build/bin

## Prepare directories
mkdir t2s_Model
cd t2s_Model/
mkdir -p ${TRAINING_DIR}/lm

## Training STRING language model for TARGET language
LM_FILE=`pwd`/${TRAINING_DIR}/lm/lm.${TARGET}.arpa.gz
${MOSES_BIN}/lmplz --order ${LM_ORDER} -S 80% -T /tmp < ${LM}.${TARGET} | gzip > ${LM_FILE}


## Training translation model
# Removed: sort-buffer-size 10G
# Removed:  --sort-batch-size 1024 --sort-compress gzip \
# Removed:   --extract-options "--MaxSpan 1000 --MinHoleSource 1 --MinWords 0 --NonTermConsecSource --AllowOnlyUnalignedWords" \

${MOSES_SCRIPT}/training/train-model.perl \
  --root-dir `pwd`/${TRAINING_DIR} \
  --model-dir `pwd`/${MODEL_DIR} \
  --corpus ${CORPUS} \
  --external-bin-dir ${EXT_BIN} \
  --f ${SOURCE} \
  --e ${TARGET} \
  --parallel \
  --alignment grow-diag-final-and \
  --mgiza --mgiza-cpus 8 \
  --score-options "--GoodTuring" \
  --hierarchical \
  --glue-grammar \
  --lm 0:${LM_ORDER}:${LM_FILE}:8 \
  --source-syntax \
  --extract-options "--MaxSpan 500 --MinHoleSource 1 --MinWords 0 --NonTermConsecSource --AllowOnlyUnalignedWords" \
  --cores ${JOBS} \
  --parallel \
  >& ${TRAINING_DIR}/training_TM.log


## Tuning
mkdir -p ${WORK_DIR}/tuning
#   --decoder-flags "-threads ${JOBS} -max-chart-span 1000" \
#   --decoder-flags " -max-chart-span 1000" \
#   --continue --skip-decoder \
#   --decoder-flags "-threads ${JOBS} -v 0" \

${MOSES_SCRIPT}/training/mert-moses.pl \
  ${DEV_SOURCE} \
  ${DEV_TARGET} \
  ${MOSES_BIN}/moses_chart \
  --continue \
  `pwd`/${MODEL_DIR}/moses.ini \
  --mertdir ${MOSES_BIN} \
  --working-dir `pwd`/${WORK_DIR}/tuning/mert \
  --threads ${JOBS} \
  --no-filter-phrase-table \
  --inputtype 3 \
  --predictable-seeds \
  --batch-mira --return-best-dev --batch-mira-args "-J 300"  \
  --decoder-flags "-max-chart-span 500 -threads all -v 0" \
  >& ${WORK_DIR}/tuning/mert.log


## Updating tuned best weights into the configuration file
perl ${MOSES_SCRIPT}/ems/support/substitute-weights.perl \
  ${MODEL_DIR}/moses.ini \
  ${WORK_DIR}/tuning/mert/moses.ini \
  ${MODEL_DIR}/moses-tuned.ini


## Translating
OUTPUT_DIR=${WORK_DIR}/output
mkdir ${OUTPUT_DIR}
outfile=${OUTPUT_DIR}/test.out

#${MOSES_BIN}/moses_chart -config ${MODEL_DIR}/moses-tuned.ini -max-chart-span 1000 -threads ${JOBS} -inputtype 3 < ${TEST} > ${outfile} 2> ${outfile}.log
#${MOSES_BIN}/moses_chart -config ${MODEL_DIR}/moses-tuned.ini -threads ${JOBS} -inputtype 3 < ${TEST} > ${outfile} 2> ${outfile}.log
${MOSES_BIN}/moses_chart -config ${MODEL_DIR}/moses-tuned.ini --inputtype 3 < ${TEST} > ${outfile} 2> ${outfile}.log

## Evaluation with multi-bleu.perl
# /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts
perl ${MOSES_SCRIPT}/generic/multi-bleu.perl ${REF} < ${outfile}

## Evaluation with mteval tool
## Check corpus level BLEU, RIBES and WER scores for your tree2string experiment
${MTEVAL_DIR}/mteval-corpus -e BLEU RIBES WER -r ${REF} -h ${outfile}

-----------------

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string$ time ./t2s.sh 
=== 1/5 Counting and sorting n-grams ===
Reading /home/ye/exp/smt/wat2021/tree-smt/tree2string/data.tok/train.my
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
****************************************************************************************************
Unigram tokens 6285996 types 9789
=== 2/5 Calculating and sorting adjusted counts ===
Chain sizes: 1:117468 2:809923776 3:1518607104 4:2429771264 5:3543416576 6:4859542528
Statistics:
1 9789 D1=0.722244 D2=1.10259 D3+=1.08703
2 222136 D1=0.67195 D2=1.06259 D3+=1.44678
3 956559 D1=0.770592 D2=1.1215 D3+=1.34752
4 1898498 D1=0.833995 D2=1.18933 D3+=1.33204
5 2665563 D1=0.877419 D2=1.26852 D3+=1.38285
6 3139196 D1=0.582375 D2=1.71726 D3+=1.66681
Memory estimate for binary LM:
type     MB
probing 185 assuming -p 1.5
probing 218 assuming -r models -p 1.5
trie     84 without quantization
trie     43 assuming -q 8 -b 8 quantization 
trie     74 assuming -a 22 array pointer compression
trie     34 assuming -a 22 -q 8 -b 8 array pointer compression and quantization
=== 3/5 Calculating and sorting initial probabilities ===
Chain sizes: 1:117468 2:3554176 3:19131180 4:45563952 5:74635764 6:100454272
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
####################################################################################################
=== 4/5 Calculating and writing order-interpolated probabilities ===
Chain sizes: 1:117468 2:3554176 3:19131180 4:45563952 5:74635764 6:100454272
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
####################################################################################################
=== 5/5 Writing ARPA model ===
Name:lmplz	VmPeak:13032640 kB	VmRSS:28352 kB	RSSMax:2152772 kB	user:7.24807	sys:1.74523	CPU:8.99329	real:22.0898
ERROR cannot open weight-ini 'work.en-my/tuning/mert/moses.ini': No such file or directory at /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/ems/support/substitute-weights.perl line 34.
Use of uninitialized value in division (/) at /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl line 139, <STDIN> line 1018.
Use of uninitialized value in division (/) at /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl line 139, <STDIN> line 1018.
Use of uninitialized value in division (/) at /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl line 139, <STDIN> line 1018.
BLEU = 0.00, 0.0/0.0/0.0/0.0 (BP=0.456, ratio=0.560, hyp_len=32989, ref_len=58895)
BLEU=0.000000	RIBES=0.000000	WER=1.020299

real	38m1.788s
user	142m9.764s
sys	30m53.357s

Note:   --extract-options "--MaxSpan 500 --MinHoleSource 1 --MinWords 0 --NonTermConsecSource --AllowOnlyUnalignedWords" \
--decoder-flags "-max-chart-span 500 -threads all -v 0" \ ထည့်တော့ အချိန်ကတော့ ပုံမှန်ထက် ပိုကြာတယ်။
သို့သော် rule-table က မထွက်ဘူး။

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/training/model$ wc *
   238014   3463768  28441812 aligned.0.en
   238014   6285996  60847350 aligned.0.my
   238014   5294741  26303924 aligned.grow-diag-final-and
  1444800   8323532 374485305 extract.inv.sorted.gz
  1498839   8520905 384199383 extract.sorted.gz
        3        45       192 glue-grammar
   518528   1555584  16594419 lex.e2f
   518528   1555584  16594419 lex.f2e
       48       102      1230 moses.ini
       38        58       871 moses-tuned.ini
        0         0        20 rule-table.gz
  4694826  35000315 907468925 total

training error က အောက်ပါအတိုင်း

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/training$ tail training_TM.log 
....Score v2.1 -- scoring methods for extracted rules
processing hierarchical rules
adjusting phrase translation probabilities with Good Turing discounting
Loading lexical translation table from /home/ye/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/training/model/lex.f2e.....
............................................................................................................................................................................................................................................................................................................................terminate called after throwing an instance of 'std::length_error'
  what():  vector::_M_default_append
Aborted (core dumped)

gzip: /home/ye/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/training/model/tmp.11447/phrase-table.half.0000000.gz: unexpected end of file
..................................................................Killed
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/training$ 

## Update the script and Run again

Rule ကို maximum 300 ထိပဲ ထားပြီး လုပ်ခဲ့...

extraction လုပ်တာ... learn လုပ်တာတော့ အဆင့်ဆင့်ဖြစ်လာလို့ တိုးတက်မှု ရှိ ...

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/training/model/tmp.14008$ ls
align.0000000  align.0000007           extract.0000002.inv.gz  extract.0000006.gz      glue.0000003  sortBD6gLO  source.0000000  source.0000007  target.0000006
align.0000001  chk.extract.6.out       extract.0000003.gz      extract.0000006.inv.gz  glue.0000004  sortfueEbB  source.0000001  target.0000000  target.0000007
align.0000002  extract.0000000.gz      extract.0000003.inv.gz  extract.0000007.gz      glue.0000005  sortjX7JkD  source.0000002  target.0000001
align.0000003  extract.0000000.inv.gz  extract.0000004.gz      extract.0000007.inv.gz  glue.0000006  sortM4eLDz  source.0000003  target.0000002
align.0000004  extract.0000001.gz      extract.0000004.inv.gz  glue.0000000            sort089xhB    sortMzBcvP  source.0000004  target.0000003
align.0000005  extract.0000001.inv.gz  extract.0000005.gz      glue.0000001            sort4TNBdO    sortRnJTJP  source.0000005  target.0000004
align.0000006  extract.0000002.gz      extract.0000005.inv.gz  glue.0000002            sortA9TAjB    sortTmCiGQ  source.0000006  target.0000005
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/t2s_Model/work.en-my/training/model/tmp.14008$

သို့သော် Rule table မဆောက်ပေးနိုင်...

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string$ time ./t2s.sh 
=== 1/5 Counting and sorting n-grams ===
Reading /home/ye/exp/smt/wat2021/tree-smt/tree2string/data.tok/train.my
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
****************************************************************************************************
Unigram tokens 6285996 types 9789
=== 2/5 Calculating and sorting adjusted counts ===
Chain sizes: 1:117468 2:809923776 3:1518607104 4:2429771264 5:3543416576 6:4859542528
Statistics:
1 9789 D1=0.722244 D2=1.10259 D3+=1.08703
2 222136 D1=0.67195 D2=1.06259 D3+=1.44678
3 956559 D1=0.770592 D2=1.1215 D3+=1.34752
4 1898498 D1=0.833995 D2=1.18933 D3+=1.33204
5 2665563 D1=0.877419 D2=1.26852 D3+=1.38285
6 3139196 D1=0.582375 D2=1.71726 D3+=1.66681
Memory estimate for binary LM:
type     MB
probing 185 assuming -p 1.5
probing 218 assuming -r models -p 1.5
trie     84 without quantization
trie     43 assuming -q 8 -b 8 quantization 
trie     74 assuming -a 22 array pointer compression
trie     34 assuming -a 22 -q 8 -b 8 array pointer compression and quantization
=== 3/5 Calculating and sorting initial probabilities ===
Chain sizes: 1:117468 2:3554176 3:19131180 4:45563952 5:74635764 6:100454272
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
####################################################################################################
=== 4/5 Calculating and writing order-interpolated probabilities ===
Chain sizes: 1:117468 2:3554176 3:19131180 4:45563952 5:74635764 6:100454272
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
####################################################################################################
=== 5/5 Writing ARPA model ===
Name:lmplz	VmPeak:13032640 kB	VmRSS:28564 kB	RSSMax:2152608 kB	user:7.31025	sys:1.72898	CPU:9.03923	real:22.1509
ERROR cannot open weight-ini 'work.en-my/tuning/mert/moses.ini': No such file or directory at /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/ems/support/substitute-weights.perl line 34.
Use of uninitialized value in division (/) at /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl line 139, <STDIN> line 1018.
Use of uninitialized value in division (/) at /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl line 139, <STDIN> line 1018.
Use of uninitialized value in division (/) at /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl line 139, <STDIN> line 1018.
BLEU = 0.00, 0.0/0.0/0.0/0.0 (BP=0.456, ratio=0.560, hyp_len=32989, ref_len=58895)
BLEU=0.000000	RIBES=0.000000	WER=1.020299

real	37m50.763s
user	144m0.369s
sys	34m14.781s
