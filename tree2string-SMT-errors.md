# Tree to String SMT Errors Note

An example of tree-to-string SMT running with noisy data.  
Here, the language pair is English-to-Myanmar.  
Most of the notes are written in Burmese (Myanmar language) and mainly prepared for Myanmar students.  

Thanks!  

ye  

tree-to-string SMT က သုတေသန အနေနဲ့ လုပ်စရာတွေ အများကြီးရှိပါတယ်။ ဒီနေရာမှာက အင်္ဂလိပ်စာကြောင်းတွေကို syntax tree parsing လုပ်ပြီး မြန်မာစာ စာကြောင်းတွေကို ဘာသာပြန်ဖို့အတွက် စမ်းထားတဲ့ experiment တစ်ခုနဲ့ ပတ်သက်ပြီး လေ့လာလို့ရအောင် ကြုံတွေ့ရတဲ့ လက်တွေ့ အခက်အခဲတွေနဲ့ Error တွေကို အကြမ်းမျဉ်း ချရေးပြထားတာ ဖြစ်ပါတယ်။ တကယ့် experimental log အကြမ်းပါ။  


## Parsing

အင်္ဂလိပ်စာကြောင်းတွေကို syntax tree အဖြစ်ပြောင်းပေးတဲ့ Parser တွေ အမျိုးမျိုး ရှိတယ်။  
ဥပမာ  

1. (Stanford Parser version 4.2.0)[https://nlp.stanford.edu/software/lex-parser.shtml]  
2. (BLLIP Reranking Parser)[https://github.com/BLLIP/bllip-parser]
3. (Berkeley Neural Parser)[https://github.com/nikitakit/self-attentive-parser]
4. (nltk.parse package)[https://www.nltk.org/api/nltk.parse.html]

## Syntax Tree Parsing with NLTK

Parser တွေက အင်္ဂလိပ်စာမှာတောင် အဆင်မပြေတဲ့ limitation တွေ အများကြီးပါ။ အဲဒီအထဲက တစ်ခုက string length က ရှည်လာရင် မှန်မှန်ကန်ကန် parsing လုပ်မပေးနိုင်တာနဲ့၊ လုံးဝကို parsing လုပ်မပေးတော့ပဲ blank line အဖြစ်နဲ့သာ output ထုတ်လို့ Statistical Machine Translation/Neural Machine Translation လုပ်ဖို့အတွက် source-target အတွဲက လွဲကုန်တဲ့ ပြဿနာတွေ ရှိလာပါတယ်။  

ဒီနေရာမှာတော့ NLTK parser ကို သုံးပြီး ကျောင်းသူတစ်ယောက်က သူစမ်းထားတာကို report တင်ထားလို့ အဲဒီ NLTK parser နဲ့ parsing လုပ်ထားတဲ့ ဒေတာကိုပဲ သုံးပြီး moses နဲ့ SMT experiment လုပ်သွားမှာ ဖြစ်ပါတယ်။  
NLT နဲ့ parse လုပ်မယ် ဆိုရင် အောက်ပါလိုမျိုး Python script ရေးပြီး parsing လုပ်လို့ ရပါတယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-tmp/data/parsing$ cat nltk_train.py 
import nltk 

# Written by Zar Zar Hlaing, KMITL, Thailand

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


r_file = open("train.en.txt", "r")

with open("train.en.parse.txt","a") as w_file:
    for line in r_file:
      tagged = pos_tag(word_tokenize(line)) 
      parse_out= chunker.parse(tagged) 
      parse_str= ' '.join(str(parse_out).split()) 
      w_file.write(parse_str+"\n")
      parse_str=""
      parse_out=""
      tagged=""
```

Parsing မလုပ်ခင်က အင်္ဂလိပ်စာကြောင်းတွေက အောက်ပါအတိုင်း ရှိပါလိမ့်မယ်။  

```text
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-tmp/data/parsing$ head -n 3 ./train.en
A murder case has been opened at the Kyeikgyaung police station .
Police are investigating .
Tatmadaw troops seized arms and illegal timber from a vehicle during a surprise check in Tarmoenyae in northern Shan state yesterday .
```

Parsing လုပ်ပြီးတဲ့အခါမှာတော့ အောက်ပါပုံစံ ရရှိပါလိမ့်မယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/tree-tmp/data/parsing$ head -n 3 ./train.en.parse.txt 
(S (NP A/DT murder/NN) (NP case/NN) (VP (V has/VBZ)) (VP (V been/VBN)) (VP (V opened/VBN)) (P at/IN) the/DT Kyeikgyaung/NNP police/NNS (NP station/NN) ./.)
(S Police/NNS (VP (V are/VBP)) (VP (V investigating/VBG)) ./.)
(S Tatmadaw/NNP troops/NNS (VP (V seized/VBD)) arms/NNS and/CC (NP illegal/JJ timber/NN) (PP (P from/IN) (NP a/DT vehicle/NN)) (PP (P during/IN) (NP a/DT surprise/NN)) (NP check/NN) (P in/IN) Tarmoenyae/NNP (P in/IN) northern/JJ Shan/NNP (NP state/NN) (NP yesterday/NN) ./.)
```

## Preparing t2s.sh Shell Script

ဒီနေရာမှာ 
