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
 
 
## Preparing t2s.sh Shell Script

tree-to-string SMT experiment ကို လုပ်ဖို့အတွက်က ကိုယ့်စက်ထဲမှာ moses က run လို့ ရအောင် ပြင်ဆင်ပြီးသား ဖြစ်ရပါလိမ့်မယ်။  
Link for downloading moses: https://github.com/moses-smt/mosesdecoder  
Online manual of moses: https://www.statmt.org/moses/manual/manual.pdf  

Experiment ကို config ဖိုင် ပြင်ဆင်ပြီး Experiment Management System (EMS) နဲ့လည်း run လို့ရပေမဲ့ ဒီနေရာမှာတော့ shell script ပြင်ပြီးပဲ run တာနဲ့ပဲသွားပါမယ်။  

[WAT2015](http://orchid.kuee.kyoto-u.ac.jp/WAT/WAT2015/baseline/baselineSystemTree2String.html) က tree to string SMT shell script ကို အခြေခံပြီးတော့ t2s.sh ဖိုင်ကို ပြင်ခဲ့တယ်။   
## Error Relating to Alignment Process

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

