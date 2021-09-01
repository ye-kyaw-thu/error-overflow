# Extended Edit Distance

EED calculation/evaluation ကို စမ်းကြည့်ထားတဲ့ log ဖိုင်...  

## Git Clone

ကိုယ့်စက်ထဲကို clone လုပ်မယ်...  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ git clone https://github.com/rwth-i6/ExtendedEditDistance
Cloning into 'ExtendedEditDistance'...
remote: Enumerating objects: 35, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 35 (delta 0), reused 0 (delta 0), pack-reused 31
Unpacking objects: 100% (35/35), 284.50 KiB | 1.30 MiB/s, done.
```

## Check

ဘာဖိုင်တွေရှိလဲ ကြည့်ကြည့်ရအောင်...  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ cd ExtendedEditDistance/
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ExtendedEditDistance$ ls
EED.cpp  EED.py  examples  libEED.so  LICENSE  README.md  util.py
```

## --help

Call --help  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ExtendedEditDistance$ python ./EED.py 
usage: EED.py [-h] -ref REFERENCE -hyp HYPOTHESIS [-v]
EED.py: error: the following arguments are required: -ref/--reference, -hyp/--hypothesis
```

## Evaluation with EED

EED calculation with example reference and hypothesis files...  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ExtendedEditDistance$ python ./EED.py -ref ./examples/newstest2016
newstest2016-deen-ref.en              newstest2016.uedin-syntax.4271.de-en  

(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ExtendedEditDistance$ python ./EED.py -ref ./examples/newstest2016-deen-ref.en -hyp ./examples/newstest2016.uedin-syntax.4271.de-en 
System Score=0.3334
```

မြန်မာစာအတွက် EED measure လုပ်ကြည့်ရအောင်...  
Reference ဖိုင်က အောက်ပါအတိုင်း...  
```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ExtendedEditDistance$ cat ./y-tst/ref.my 
နေကောင်း ပါတယ် ။
ဒါပေမဲ့ ခေါင်းတော့ သိပ် မကြည့်ဘူး
မင်း ရော အလုပ်အကိုင် အဆင်ပြေ ရဲ့ လား
ကိုဗစ် ကို လည်း ဂရုစိုက် အုံး နော်
အားတဲ့အခါ တွေ့ကြမယ်။
ဒါပဲနော်
```

Hypothesis ဖိုင်က အောက်ပါအတိုင်း...  
```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ExtendedEditDistance$ cat ./y-tst/hyp.my 
နေကောင်း တယ် ။
ဒါပေမဲ့ ခေါင်းတော့ ကိုက် နေတယ်
မင်း အလုပ်အကိုင် ရော အဆင်ပြေ ရဲ့ လား
ကိုဗစ် ကို လည်း ဂရုစိုက် နော်
အားတဲ့အခါ တွေ့ကျမယ်။
ဒါပဲနော်
```

Evaluation with EED score:  
```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ExtendedEditDistance$ python ./EED.py -ref ./y-tst/ref.my -hyp ./y-tst/hyp.my 
System Score=0.1594
```

တစ်ကြောင်းချင်းစီအတွက် EED score တွက်ကြည့်လို့လည်း ရ...  
```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/ExtendedEditDistance$ python ./EED.py -ref ./y-tst/ref.my -hyp ./y-tst/hyp.my -v
Sentence 1: 0.1398
Sentence 2: 0.3815
Sentence 3: 0.1782
Sentence 4: 0.1864
Sentence 5: 0.0708
Sentence 6: 0.0000
System Score=0.1594
```
