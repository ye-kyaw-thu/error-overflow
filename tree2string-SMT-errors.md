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

```
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

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-tmp/data/parsing/example$ python ./nltk_parser.py 
[nltk_data] Downloading package averaged_perceptron_tagger to
[nltk_data]     /home/ye/nltk_data...
[nltk_data]   Package averaged_perceptron_tagger is already up-to-
[nltk_data]       date!
```

ဥပမာ အနေနဲ့ parsing လုပ်ပြမယ့် စာကြောင်းတွေက BBC News (https://www.bbc.com/news/world-asia-56612247) က စာကြောင်းငါးကြောင်းကို ယူသုံးထားပါတယ်။ Parsing မလုပ်ခင်က အင်္ဂလိပ်စာကြောင်းတွေက အောက်ပါအတိုင်း ရှိပါလိမ့်မယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-tmp/data/parsing/example$ cat ./bbc.article.txt 
Myanmar's military seized power in the South East Asian nation after overthrowing the government and declared a state of emergency.
Just days later, the civil disobedience movement began to emerge - professionals refusing to return to work in protest.
The movement quickly started to gain momentum and it was not long before hundreds of thousands of people began taking part in street protests.
But there has increasingly been an escalation of violence between police officers and civilians.
Rights group the Assistance Association for Political Prisoners say more than 500 people have been killed since the military crackdown began.
```

Parsing လုပ်ပြီးတဲ့အခါမှာတော့ အောက်ပါပုံစံ ရရှိပါလိမ့်မယ်။  

```
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

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string$ tree -L 1 ./data.tok/
./data.tok/
├── dev.my
├── test.my
└── train.my
```

tree ဒေတာကတော့ data.tree/ အောက်မှာ သိမ်းထားတယ်။  

```
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

```
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

```
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

```
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

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/wmt2014-scripts/example/data$ head -n 1 parallelC.de-en.parsed.en 
<tree label="sent"><tree label="root"><tree label="nsubj"><tree label="det"><tree label="DT">The</tree></tree><tree label="NN">ECB</tree></tree><tree label="VBZ">wants</tree><tree label="xcomp"><tree label="aux"><tree label="TO">to</tree></tree><tree label="VB">hold</tree><tree label="dobj"><tree label="NN">inflation</tree></tree><tree label="prep"><tree label="TO">to</tree><tree label="pcomp"><tree label="IN">under</tree><tree label="pobj"><tree label="num"><tree label="CD">two</tree></tree><tree label="NN">percent</tree><tree label="punct"><tree label=",">,</tree></tree><tree label="cc"><tree label="CC">or</tree></tree><tree label="conj"><tree label="advmod"><tree label="RB">somewhere</tree></tree><tree label="IN">in</tree><tree label="pobj"><tree label="det"><tree label="DT">that</tree></tree><tree label="NN">vicinity</tree></tree></tree></tree></tree></tree></tree><tree label="punct"><tree label=".">.</tree></tree></tree></tree>
```

moses က လက်ခံတာက အထက်မှာ ပြထားသလို xml tag format ပုံစံလို့ ထင်တယ်။  
လက်ရှိ parsed လုပ်ထားတဲ့ training ဒေတာက bracket နဲ့ parsed လုပ်ထားတဲ့ format ဖြစ်နေတာကိုတွေ့ရ။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/data.tree$ head -n 3 ./train.en 
(S (NP A/DT murder/NN) (NP case/NN) (VP (V has/VBZ)) (VP (V been/VBN)) (VP (V opened/VBN)) (P at/IN) the/DT Kyeikgyaung/NNP police/NNS (NP station/NN) ./.)
(S Police/NNS (VP (V are/VBP)) (VP (V investigating/VBG)) ./.)
(S Tatmadaw/NNP troops/NNS (VP (V seized/VBD)) arms/NNS and/CC (NP illegal/JJ timber/NN) (PP (P from/IN) (NP a/DT vehicle/NN)) (PP (P during/IN) (NP a/DT surprise/NN)) (NP check/NN) (P in/IN) Tarmoenyae/NNP (P in/IN) northern/JJ Shan/NNP (NP state/NN) (NP yesterday/NN) ./.)
```

## Format Conversion

Bracket format ကနေ XML tag format အဖြစ်ပြောင်းဖို့ tool program တွေက moses မှာ wrapper အနေနဲ့ ပါပါတယ်။ သို့သော် SMT experiment အတွက် NLTK parser ရဲ့ output ကို ဒီ wrapper နဲ့ တကယ်တမ်း အဆင်ပြေ မပြေဆိုတာကတော့ လေ့လာဖို့ လိုအပ်လိမ့်မယ်...  

```
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

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-smt/tree2string/data.tree$ head -n 3 test.en | perl /home/ye/tool/mosesbin/ubuntu-17.04/moses/scripts/training/wrappers/berkeleyparsed2mosesxml.perl 
<tree label="S"> It/PRP <tree label="VP"> <tree label="V"> has/VBZ </tree> </tree> <tree label="VP"> <tree label="V"> been/VBN </tree> </tree> <tree label="VP"> <tree label="V"> confirmed/VBN </tree> </tree> <tree label="P"> that/IN </tree> eight/CD <tree label="VP"> <tree label="V"> thoroughbred/VBD </tree> <tree label="NP"> race/NN </tree> </tree> horses/NNS <tree label="P"> at/IN </tree> Randwick/NNP Racecourse/NNP <tree label="P"> in/IN </tree> Sydney/NNP <tree label="VP"> <tree label="V"> have/VBP </tree> </tree> <tree label="VP"> <tree label="V"> been/VBN </tree> </tree> <tree label="VP"> <tree label="V"> infected/VBN </tree> <tree label="PP"> <tree label="P"> with/IN </tree> <tree label="NP"> equine/JJ influenza/NN </tree> </tree> </tree> ./. </tree>
<tree label="S"> Randwick/NNP <tree label="VP"> <tree label="V"> has/VBZ </tree> </tree> <tree label="VP"> <tree label="V"> been/VBN </tree> </tree> <tree label="VP"> <tree label="V"> locked/VBN </tree> </tree> down/RP ,/, and/CC <tree label="VP"> <tree label="V"> is/VBZ </tree> </tree> <tree label="VP"> <tree label="V"> expected/VBN </tree> </tree> to/TO <tree label="VP"> <tree label="V"> remain/VB </tree> </tree> so/RB <tree label="P"> for/IN </tree> <tree label="P"> up/IN </tree> to/TO two/CD months/NNS ./. </tree>
<tree label="S"> It/PRP <tree label="VP"> <tree label="V"> is/VBZ </tree> </tree> <tree label="VP"> <tree label="V"> expected/VBN </tree> <tree label="PP"> <tree label="P"> that/IN </tree> <tree label="NP"> the/DT virulent/NN </tree> </tree> <tree label="NP"> flu/NN </tree> </tree> will/MD <tree label="VP"> <tree label="V"> affect/VB </tree> <tree label="NP"> the/DT majority/NN </tree> </tree> <tree label="P"> of/IN </tree> the/DT 700/CD horses/NNS <tree label="VP"> <tree label="V"> stabled/VBN </tree> </tree> <tree label="P"> at/IN </tree> Randwick/NNP ./. </tree>
```

အောက်ပါအတိုင်း အင်္ဂလိပ်စာ training/development/test data အားလုံးကို format conversion လုပ်ခဲ့တယ်။  

```
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

```
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

```
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

```
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

