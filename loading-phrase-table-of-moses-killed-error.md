# Phrase Table Loading Error and Building Compact Phrase Table

စာကြောင်းရေ နှစ်သိမ်းကျော် နဲ့ PBSMT model training လုပ်ခဲ့ပြီး၊ development data ကတော့ တစ်ထောင်ကျော်သုံးပြီး model tunning လုပ်ခဲ့ပါတယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran$ wc ../exp-syl4/data/train.my 
  238014  6285996 60847350 ../exp-syl4/data/train.my
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran$ wc ../exp-syl4/data/dev.my
  1000  57709 550454 ../exp-syl4/data/dev.my
```
ပြဿနာက translation လုပ်ဖို့အတွက် phrase table ကို loading လုပ်တဲ့နေရာမှာ memory မနိုင်ပဲ killed ဖြစ်သွားတာပါ။  
အဲဒါကို compact phrase table လုပ်ပြီး ဖြေရှင်းခဲ့တာကို practical error solving log တစ်ခုအနေနဲ့ တင်ပေးထားတာပါ။  
MT experiment တွေအတွက် အသုံးဝင်ပါလိမ့်မယ်။  

## Decoding/Translation Error

translation.sh ဆိုတဲ့ shell script ထဲကနေ ခေါ် run တဲ့အခါမှာ error ပေးပါတယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran$ ./translation.sh 
Using tuned no filtered ini file ...
English-Myanmar:
Translation of development data...
Starting...
Defined parameters (per moses.ini or switch):
	config: /home/ye/exp/smt/wat2021/exp-syl4/baseline/en-my/tuning/moses.tuned.ini.1 
	distortion-limit: 6 
	feature: UnknownWordPenalty WordPenalty PhrasePenalty PhraseDictionaryMemory name=TranslationModel0 num-features=4 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/en-my/model/phrase-table.1.gz input-factor=0 output-factor=0 LexicalReordering name=LexicalReordering0 num-features=6 type=wbe-msd-bidirectional-fe-allff input-factor=0 output-factor=0 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/en-my/model/reordering-table.1.wbe-msd-bidirectional-fe.gz Distortion KENLM name=LM0 factor=0 path=/home/ye/exp/smt/wat2021/exp-syl4//baseline/en-my/lm/myrk.binlm.1 order=6 
	input-factors: 0 
	input-file: /home/ye/exp/smt/wat2021/exp-syl4/data/dev.en 
	mapping: 0 T 0 
	weight: LexicalReordering0= 0.0281432 0.0219143 0.159276 0.0346079 0.0218057 0.133628 Distortion0= 0.00462869 LM0= 0.0396439 WordPenalty0= -0.208 PhrasePenalty0= 0.208074 TranslationModel0= 0.0393394 0.0263135 0.031987 0.0426387 UnknownWordPenalty0= 1 
START featureFunctions.Load()
Loading WordPenalty0
Finished loading WordPenalty0
Loading PhrasePenalty0
Finished loading PhrasePenalty0
Loading LexicalReordering0
1000000 2000000 3000000 4000000 5000000 6000000 7000000 8000000 9000000 Finished loading LexicalReordering0
Loading Distortion0
Finished loading Distortion0
Loading LM0
Finished loading LM0
Loading UnknownWordPenalty0
Finished loading UnknownWordPenalty0
Loading TranslationModel0
1000000 2000000 3000000 4000000 5000000 6000000 7000000 8000000 9000000 Finished loading TranslationModel0
START LoadMappings()
END LoadMappings()
END LoadDecodeGraphBackoff()
Loaded : [146.078] seconds
RUN BATCH
Decoding took 163.257
Finished
Translation of training data...
Starting...
Defined parameters (per moses.ini or switch):
	config: /home/ye/exp/smt/wat2021/exp-syl4/baseline/en-my/tuning/moses.tuned.ini.1 
	distortion-limit: 6 
	feature: UnknownWordPenalty WordPenalty PhrasePenalty PhraseDictionaryMemory name=TranslationModel0 num-features=4 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/en-my/model/phrase-table.1.gz input-factor=0 output-factor=0 LexicalReordering name=LexicalReordering0 num-features=6 type=wbe-msd-bidirectional-fe-allff input-factor=0 output-factor=0 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/en-my/model/reordering-table.1.wbe-msd-bidirectional-fe.gz Distortion KENLM name=LM0 factor=0 path=/home/ye/exp/smt/wat2021/exp-syl4//baseline/en-my/lm/myrk.binlm.1 order=6 
	input-factors: 0 
	input-file: /home/ye/exp/smt/wat2021/exp-syl4/data/train.en 
	mapping: 0 T 0 
	weight: LexicalReordering0= 0.0281432 0.0219143 0.159276 0.0346079 0.0218057 0.133628 Distortion0= 0.00462869 LM0= 0.0396439 WordPenalty0= -0.208 PhrasePenalty0= 0.208074 TranslationModel0= 0.0393394 0.0263135 0.031987 0.0426387 UnknownWordPenalty0= 1 
START featureFunctions.Load()
Loading WordPenalty0
Finished loading WordPenalty0
Loading PhrasePenalty0
Finished loading PhrasePenalty0
Loading LexicalReordering0
1000000 2000000 3000000 4000000 5000000 6000000 7000000 8000000 9000000 Finished loading LexicalReordering0
Loading Distortion0
Finished loading Distortion0
Loading LM0
Finished loading LM0
Loading UnknownWordPenalty0
Finished loading UnknownWordPenalty0
Loading TranslationModel0
1000000 2000000 3000000 4000000 5000000 6000000 7000000 8000000 9000000 Finished loading TranslationModel0
START LoadMappings()
END LoadMappings()
END LoadDecodeGraphBackoff()
Loaded : [126.092] seconds
RUN BATCH
./translation.sh: line 9: 163613 Killed                  /home/ye/tool/mosesbin/ubuntu-17.04/moses/bin/moses2 -f /home/ye/exp/smt/wat2021/exp-syl4/baseline/en-my/tuning/moses.tuned.ini.1 -i /home/ye/exp/smt/wat2021/exp-syl4/data/train.en > ./en-my/train.enmy.hyp
Myanmar-English:
Translation of development data...
Starting...
Defined parameters (per moses.ini or switch):
	config: /home/ye/exp/smt/wat2021/exp-syl4/baseline/en-my/tuning/moses.tuned.ini.1 
	distortion-limit: 6 
	feature: UnknownWordPenalty WordPenalty PhrasePenalty PhraseDictionaryMemory name=TranslationModel0 num-features=4 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/en-my/model/phrase-table.1.gz input-factor=0 output-factor=0 LexicalReordering name=LexicalReordering0 num-features=6 type=wbe-msd-bidirectional-fe-allff input-factor=0 output-factor=0 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/en-my/model/reordering-table.1.wbe-msd-bidirectional-fe.gz Distortion KENLM name=LM0 factor=0 path=/home/ye/exp/smt/wat2021/exp-syl4//baseline/en-my/lm/myrk.binlm.1 order=6 
	input-factors: 0 
	input-file: /home/ye/exp/smt/wat2021/exp-syl4/data/dev.my 
	mapping: 0 T 0 
	weight: LexicalReordering0= 0.0281432 0.0219143 0.159276 0.0346079 0.0218057 0.133628 Distortion0= 0.00462869 LM0= 0.0396439 WordPenalty0= -0.208 PhrasePenalty0= 0.208074 TranslationModel0= 0.0393394 0.0263135 0.031987 0.0426387 UnknownWordPenalty0= 1 
START featureFunctions.Load()
Loading WordPenalty0
Finished loading WordPenalty0
Loading PhrasePenalty0
Finished loading PhrasePenalty0
Loading LexicalReordering0
1000000 2000000 3000000 4000000 5000000 6000000 7000000 8000000 9000000 Finished loading LexicalReordering0
Loading Distortion0
Finished loading Distortion0
Loading LM0
Finished loading LM0
Loading UnknownWordPenalty0
Finished loading UnknownWordPenalty0
Loading TranslationModel0
1000000 2000000 3000000 4000000 5000000 6000000 7000000 ./translation.sh: line 13: 167472 Killed                  /home/ye/tool/mosesbin/ubuntu-17.04/moses/bin/moses2 -f /home/ye/exp/smt/wat2021/exp-syl4/baseline/en-my/tuning/moses.tuned.ini.1 -i /home/ye/exp/smt/wat2021/exp-syl4/data/dev.my > ./my-en/dev.myen.hyp
Translation of training data...
Starting...
Defined parameters (per moses.ini or switch):
	config: /home/ye/exp/smt/wat2021/exp-syl4/baseline/en-my/tuning/moses.tuned.ini.1 
	distortion-limit: 6 
	feature: UnknownWordPenalty WordPenalty PhrasePenalty PhraseDictionaryMemory name=TranslationModel0 num-features=4 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/en-my/model/phrase-table.1.gz input-factor=0 output-factor=0 LexicalReordering name=LexicalReordering0 num-features=6 type=wbe-msd-bidirectional-fe-allff input-factor=0 output-factor=0 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/en-my/model/reordering-table.1.wbe-msd-bidirectional-fe.gz Distortion KENLM name=LM0 factor=0 path=/home/ye/exp/smt/wat2021/exp-syl4//baseline/en-my/lm/myrk.binlm.1 order=6 
	input-factors: 0 
	input-file: /home/ye/exp/smt/wat2021/exp-syl4/data/train.my 
	mapping: 0 T 0 
	weight: LexicalReordering0= 0.0281432 0.0219143 0.159276 0.0346079 0.0218057 0.133628 Distortion0= 0.00462869 LM0= 0.0396439 WordPenalty0= -0.208 PhrasePenalty0= 0.208074 TranslationModel0= 0.0393394 0.0263135 0.031987 0.0426387 UnknownWordPenalty0= 1 
START featureFunctions.Load()
Loading WordPenalty0
Finished loading WordPenalty0
Loading PhrasePenalty0
Finished loading PhrasePenalty0
Loading LexicalReordering0
1000000 2000000 3000000 4000000 5000000 6000000 7000000 8000000 9000000 Finished loading LexicalReordering0
Loading Distortion0
Finished loading Distortion0
Loading LM0
Finished loading LM0
Loading UnknownWordPenalty0
Finished loading UnknownWordPenalty0
Loading TranslationModel0
1000000 2000000 3000000 4000000 5000000 6000000 ./translation.sh: line 16: 167699 Killed                  /home/ye/tool/mosesbin/ubuntu-17.04/moses/bin/moses2 -f /home/ye/exp/smt/wat2021/exp-syl4/baseline/en-my/tuning/moses.tuned.ini.1 -i /home/ye/exp/smt/wat2021/exp-syl4/data/train.my > ./my-en/train.myen.hyp
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran$ 
```

## One more confirmation

အထက်ပါအတိုင်း error ပေးနေတာနဲ့ bash shell script ထဲကနေ မသွားတော့ပဲ interactive translation လုပ်ခိုင်းကြည့်ခဲ့ပါတယ်။  
ဒီနေရာမှာ -i နဲ့ input မပေးလည်း မရဘူးဆိုတာကို သွားတွေ့ရပါတယ်။  
phrase table ကို load လုပ်လိုက်ရင်ကို killed ဖြစ်သွားတာ...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran$ /home/ye/tool/mosesbin/ubuntu-17.04/moses/bin/moses -f /home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/tuning/moses.tuned.ini.1
...
...
FeatureFunction: Distortion0 start: 13 end: 13
line=KENLM name=LM0 factor=0 path=/home/ye/exp/smt/wat2021/exp-syl4//baseline/my-en/lm/myrk.binlm.1 order=6
FeatureFunction: LM0 start: 14 end: 14
Loading UnknownWordPenalty0
Loading WordPenalty0
Loading PhrasePenalty0
Loading LexicalReordering0
Loading table into memory...done.
Loading Distortion0
Loading LM0
Loading TranslationModel0
Start loading text phrase table. Moses format : [35.557] seconds
Reading /home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/model/phrase-table.1.gz
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
*************************************************************************Killed
```

## Building a Compact Phrase Table

Compact phrase table ကိုတော့ အောက်ပါအတိုင်း build လုပ်ခဲ့ပါတယ်။   

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4/baseline/my-en/model$ time ~/tool/mosesbin/ubuntu-17.04/moses/bin/processPhraseTableMin -in ./phrase-table.1.gz -out phrase-table -nscores 4 -threads 4
Used options:
	Text phrase table will be read from: ./phrase-table.1.gz
	Output phrase table will be written to: phrase-table.minphr
	Step size for source landmark phrases: 2^10=1024
	Source phrase fingerprint size: 16 bits / P(fp)=1.52588e-05
	Selected target phrase encoding: Huffman + PREnc
	Maxiumum allowed rank for PREnc: 100
	Number of score components in phrase table: 4
	Single Huffman code set for score components: no
	Using score quantization: no
	Explicitly included alignment information: yes
	Running with 4 threads

Pass 1/3: Creating hash function for rank assignment
.......................................

Pass 2/3: Creating source phrase index + Encoding target phrases
.......................................

Intermezzo: Calculating Huffman code sets
	Creating Huffman codes for 59765 target phrase symbols
	Creating Huffman codes for 30166 scores
	Creating Huffman codes for 3984828 scores
	Creating Huffman codes for 27397 scores
	Creating Huffman codes for 2425614 scores
	Creating Huffman codes for 145 alignment points

Pass 3/3: Compressing target phrases
.......................................

Saving to phrase-table.minphr
Done

real	1m18.765s
user	4m53.183s
sys	0m5.113s
```

## Comparing Original Phrase Table and Compact Phrase Table

compact ဖြစ်သွားတဲ့ phrase table နဲ့ original phrase table ရဲ့ file size တွေကို နှိုင်းယှဉ်ကြည့်တော့ 205M vs 124M မို့လို့ တဝက်နီးပါ (81M) လျော့သွားတာကို လေ့လာသိရှိရပါတယ်။   

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4/baseline/my-en/model$ ls
aligned.1.grow-diag-final-and  extract.1.o.sorted.gz  lex.1.e2f  moses.ini.1        phrase-table.minphr
extract.1.inv.sorted.gz        extract.1.sorted.gz    lex.1.f2e  phrase-table.1.gz  reordering-table.1.wbe-msd-bidirectional-fe.gz
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4/baseline/my-en/model$ ls -lh ./phrase-table.1.gz
-rw-rw-r-- 1 ye ye 205M မတ်   11 11:21 ./phrase-table.1.gz
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4/baseline/my-en/model$ ls -lh ./phrase-table.minphr 
-rw-rw-r-- 1 ye ye 124M ဧပြီ   8 00:05 ./phrase-table.minphr
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4/baseline/my-en/model$ file ./phrase-table.minphr 
./phrase-table.minphr: data
```

##  Editing moses.ini

moses.ini ဖိုင်ထဲမှာ အောက်ပါအတိုင်း ဝင် update လုပ်ပါတယ်။  
phrase-table.1.gz နေရာမှာ phrase-table.minphr နဲ့ အစားထိုးတာပါ...  

```
#PhraseDictionaryMemory name=TranslationModel0 num-features=4 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/model/phrase-table.1.gz input-factor=0 output-factor=0
PhraseDictionaryCompact name=TranslationModel0 num-features=4 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/model/phrase-table.minphr input-factor=0 output-factor=0
```

## Test Translation with STDIO

Interactive translation လုပ်ခိုင်းကြည့်တော့ အဆင်ပြေသွားပါပြီ...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4/baseline/my-en/model$ /home/ye/tool/mosesbin/ubuntu-17.04/moses/bin/moses -f /home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/tuning/moses.tuned.ini.1
Defined parameters (per moses.ini or switch):
	config: /home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/tuning/moses.tuned.ini.1 
	distortion-limit: 6 
	feature: UnknownWordPenalty WordPenalty PhrasePenalty PhraseDictionaryCompact name=TranslationModel0 num-features=4 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/model/phrase-table.minphr input-factor=0 output-factor=0 LexicalReordering name=LexicalReordering0 num-features=6 type=wbe-msd-bidirectional-fe-allff input-factor=0 output-factor=0 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/model/reordering-table.1.wbe-msd-bidirectional-fe.gz Distortion KENLM name=LM0 factor=0 path=/home/ye/exp/smt/wat2021/exp-syl4//baseline/my-en/lm/myrk.binlm.1 order=6 
	input-factors: 0 
	mapping: 0 T 0 
	weight: LexicalReordering0= 0.0295063 0.144319 0.114957 0.0621906 -0.0220501 0.0307571 Distortion0= 0.0628715 LM0= 0.0865004 WordPenalty0= -0.224658 PhrasePenalty0= -0.026615 TranslationModel0= -0.00641249 0.0654316 0.0872244 0.0365068 UnknownWordPenalty0= 1 
line=UnknownWordPenalty
FeatureFunction: UnknownWordPenalty0 start: 0 end: 0
line=WordPenalty
FeatureFunction: WordPenalty0 start: 1 end: 1
line=PhrasePenalty
FeatureFunction: PhrasePenalty0 start: 2 end: 2
line=PhraseDictionaryCompact name=TranslationModel0 num-features=4 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/model/phrase-table.minphr input-factor=0 output-factor=0
FeatureFunction: TranslationModel0 start: 3 end: 6
line=LexicalReordering name=LexicalReordering0 num-features=6 type=wbe-msd-bidirectional-fe-allff input-factor=0 output-factor=0 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/model/reordering-table.1.wbe-msd-bidirectional-fe.gz
Initializing Lexical Reordering Feature..
FeatureFunction: LexicalReordering0 start: 7 end: 12
line=Distortion
FeatureFunction: Distortion0 start: 13 end: 13
line=KENLM name=LM0 factor=0 path=/home/ye/exp/smt/wat2021/exp-syl4//baseline/my-en/lm/myrk.binlm.1 order=6
FeatureFunction: LM0 start: 14 end: 14
Loading UnknownWordPenalty0
Loading WordPenalty0
Loading PhrasePenalty0
Loading LexicalReordering0
Loading table into memory...done.
Loading Distortion0
Loading LM0
Loading TranslationModel0
Created input-output object : [34.175] seconds
အဆင်ပြေ သွား ပြီလား ။ ဘယ်လို လဲ
Translating: အဆင်ပြေ သွား ပြီလား ။ ဘယ်လို လဲ 
Line 0: Initialize search took 0.000 seconds total
Line 0: Collecting options took 0.018 seconds at moses/Manager.cpp Line 141
Line 0: Search took 0.016 seconds
အဆင်ပြေ go . ပြီလား ဘယ်လို ? 
BEST TRANSLATION: အဆင်ပြေ|UNK|UNK|UNK go . ပြီလား|UNK|UNK|UNK ဘယ်လို|UNK|UNK|UNK ? [111111]  [total=-305.061] core=(-300.000,-6.000,6.000,-5.934,-2.728,-2.057,-2.568,-4.099,0.000,-0.144,0.000,-5.882,-0.617,-4.000,-64.252)  
Line 0: Decision rule took 0.000 seconds total
Line 0: Additional reporting took 0.000 seconds total
Line 0: Translation took 0.034 seconds total
```

## Translation with -i option

ဒီတစ်ခါတော့ -i option ကို သုံးပြီး input file (i.e. the whole English training file) ပေးပြီး translation လုပ်ခိုင်းကြည့်ခဲ့ပါတယ်။   
အောက်ပါအတိုင်း အဆင်ပြေပြေနဲ့ phrase table ကို loading လုပ်သွားပြီး translation လည်း တော်တော်များများ လုပ်ပေးနိုင်တာကို တွေ့ရပါတယ်။ သို့သော် နှစ်သိန်းကျော်ရှိတဲ့ စာကြောင်းရေ အားလုံးကိုတော့ ဘာသာပြန်မပေးနိုင်ပဲနဲ့  လိုင်းနံပါတ် 7,835 အရောက်မှာ အောက်ပါအတိုင်း moses decoder က killed ဖြစ်သွားတာကို တွေ့ရတယ်... ?!?!  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran$/home/ye/tool/mosesbin/ubuntu-17.04/moses/bin/moses -threads all --max-phrase-length 200 -f /home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/tuning/moses.tuned.ini.1 -i /home/ye/exp/smt/wat2021/exp-syl4/data/train.my > ./my-en/train.myen.hyp
...
...
...
Line 2384: Decision rule took 0.000 seconds total
Line 2384: Additional reporting took 0.000 seconds total
Line 2384: Translation took 0.455 seconds total
Translating: အ စိုး ရ အ ဖွဲ့ ၏ အ တည် ပြု ချက် ဖြ င့် ကော် မ ရှင် က အ မိ န့် ကြော် ငြာ စာ ထုတ် ပြန် သတ် မှတ် ကာ ဇုန် ( ၂ ) အ တွင်း ရင်း နှီး မြှုပ် နှံ သူ များ အား စီး ပွား ဖြစ် စ တင် သော နှစ် အ ပါ အ ဝင် တ ဆက် တည်း ၅ နှစ် အ ထိ ဝင် ငွေ ခွန် ကင်း လွတ် ခွ င့် ပြု နိုင် သည် ။ 
Line 2386: Initialize search took 0.003 seconds total
Line 2385: Collecting options took 0.205 seconds at moses/Manager.cpp Line 141
Translating: အ စိုး ရ အ ဖွဲ့ ၏ အ တည် ပြု ချက် ဖြ င့် ကော် မ ရှင် က အ မိ န့် ကြော် ငြာ စာ ထုတ် ပြန် သတ် မှတ် ကာ ဇုန် ( ၃ ) အ တွင်း ရင်း နှီး မြှုပ် နှံ သူ များ အား စီး ပွား ဖြစ် စ တင် သော နှစ် အ ပါ အ ဝင် တ ဆက် တည်း ၃ နှစ် အ ထိ ဝင် ငွေ ခွန် ကင်း လွတ် ခွ င့် ပြု နိုင် သည် ။ 
Line 2387: Initialize search took 0.003 seconds total
Line 2386: Collecting options took 0.228 seconds at moses/Manager.cpp Line 141
Line 2377: Search took 2.066 seconds
Line 2377: Decision rule took 0.000 seconds total
Line 2377: Additional reporting took 0.000 seconds total
Line 2377: Translation took 2.831 seconds total
Translating: အ စိုး ရ အ ဖွဲ့ ၏ အ တည် ပြု ချက် ဖြ င့် ကော် မ ရှင် သည် ဇုန် သတ် မှတ် ခြင်း ကို သက် ဆိုင် ရာ ဒေ သ များ ၏ ဖွံ့ ဖြိုး တိုး တက် မှု အ ပေါ် မူ တည် ၍ အ ခါ အား လျော် စွာ လို အပ် သ လို ပြောင်း လဲ သတ် မှတ် နိုင် သည် ။ 
Line 2388: Initialize search took 0.019 seconds total
Line 2388: Collecting options took 0.207 seconds at moses/Manager.cpp Line 141
Line 2387: Collecting options took 0.510 seconds at moses/Manager.cpp Line 141
Line 2376: Search took 2.776 seconds
Line 2376: Decision rule took 0.000 seconds total
Line 2376: Additional reporting took 0.000 seconds total
Line 2376: Translation took 3.511 seconds total
Translating: ဝင် ငွေ ခွန် ကင်း လွတ် ခွ င့် ကို ရင်း နှီး မြှုပ် နှံ မှု မြှ င့် တင် ဆောင် ရွက် ရန် ကော် မ ရှင် က အ မိ န့် ကြော် ငြာ စာ ထုတ် ပြန် ထား သူ များ အ တွက် သာ ခွ င့် ပြု ရ သည် ။ 
Line 2389: Initialize search took 0.045 seconds total
Line 2389: Collecting options took 0.169 seconds at moses/Manager.cpp Line 141
Line 2381: Search took 2.628 seconds
Line 2381: Decision rule took 0.000 seconds total
Line 2381: Additional reporting took 0.000 seconds total
Line 2381: Translation took 2.899 seconds total
Translating: အ ခန်း ( ၁၁ ) ပါ ရင်း နှီး မြှုပ် နှံ သူ များ အား ဆက် ဆံ ဆောင် ရွက် ခြင်း ပြဋ္ဌာန်း ချက် များ အ ပြင် အ စိုး ရ အ ဖွဲ့ သည် မြန် မာ နိုင် ငံ သား ရင်း နှီး မြှုပ် နှံ သူ များ သို့ မ ဟုတ် နိုင် ငံ သား ပိုင် အ သေး စား အ လတ် စား စီး ပွား ရေး လုပ် ငန်း များ အား အ ထောက် အ ပံ့ များ ငွေ ကြေး ဆိုင် ရာ ပံ့ ပိုး မှု များ စွမ်း ဆောင် ရည် မြှ င့် တင် ခြင်း သင် တန်း များ ဖွ င့် လှစ် ပေး ခြင်း တို့ ကို ဆောင် ရွက် နိုင် သည် ။ 
Line 2390: Initialize search took 0.017 seconds total
Line 2379: Search took 3.033 seconds
Line 2379: Decision rule took 0.000 seconds total
Line 2379: Additional reporting took 0.000 seconds total
Line 2379: Translation took 3.565 seconds total
Translating: အ ခန်း ( ၁၁ ) ပါ ရင်း နှီး မြှုပ် နှံ သူ များ အား ဆက် ဆံ ဆောင် ရွက် ခြင်း ပြဋ္ဌာန်း ချက် များ အ ပြင် ။ 
Line 2391: Initialize search took 0.023 seconds total
Line 2391: Collecting options took 0.041 seconds at moses/Manager.cpp Line 141
Line 2390: Collecting options took 0.480 seconds at moses/Manager.cpp Line 141
Line 2374: Search took 5.063 seconds
...
...
...
Line 7825: Collecting options took 0.660 seconds at moses/Manager.cpp Line 141
Line 7826: Collecting options took 0.654 seconds at moses/Manager.cpp Line 141
Translating: ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် သည် ပြည် ထောင် စု လွှတ် တော် အ စည်း အ ဝေး တွင် ဖြစ် စေ ပြည် သူ့ လွှတ် တော် သို့ မ ဟုတ် အ မျိုး သား လွှတ် တော် အ စည်း အ ဝေး တွင် ဖြစ် စေ နိုင် ငံ တော် သို့ မ ဟုတ် အ များ ပြည် သူ တို့ နှ င့် သက် ဆိုင် သ ည့် အ ရေး ကြီး သော တ ရား စီ ရင် ရေး ဆိုင် ရာ အ ခြေ အ နေ ကို အ ခါ အား လျော် စွာ တင် ပြ နိုင် သည် ။ 
Line 7829: Initialize search took 0.014 seconds total
Line 7828: Collecting options took 0.564 seconds at moses/Manager.cpp Line 141
Line 7829: Collecting options took 1.643 seconds at moses/Manager.cpp Line 141
Line 7821: Search took 3.961 seconds
Line 7821: Decision rule took 0.000 seconds total
Line 7821: Additional reporting took 0.000 seconds total
Line 7821: Translation took 5.343 seconds total
Translating: ပုဒ် မ ၃၀၁ တွင် သတ် မှတ် ထား သော ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် နှ င့် ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး များ ၏ အ ရည် အ ချင်း များ နှ င့် မ ပြ ည့် စုံ ကြောင်း အ ထင် အ ရှား မ ပြ နိုင် ပါ က ပြည် ထောင် စု လွှတ် တော် သည် နိုင် ငံ တော် သမ္မ တ က ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် အ ဖြစ် ခ န့် အပ် ရန် အ မည် စာ ရင်း တင် သွင်း သူ ကို ငြင်း ပယ် ခွ င့် မ ရှိ စေ ရ ။ 
Line 7830: Initialize search took 0.039 seconds total
Line 7830: Collecting options took 1.362 seconds at moses/Manager.cpp Line 141
Line 7827: Search took 3.699 seconds
Line 7827: Decision rule took 0.000 seconds total
Line 7827: Additional reporting took 0.000 seconds total
Line 7827: Translation took 3.911 seconds total
Line 7828: Search took 3.178 seconds
Line 7828: Decision rule took 0.000 seconds total
Line 7828: Additional reporting took 0.000 seconds total
Line 7828: Translation took 3.748 seconds total
Translating: ပုဒ် မ ၃၀၁ တွင် သတ် မှတ် ထား သော ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် နှ င့် ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး များ ၏ အ ရည် အ ချင်း များ နှ င့် မ ပြ ည့် စုံ ကြောင်း အ ထင် အ ရှား မ ပြ နိုင် ပါ က ပြည် ထောင် စု လွှတ် တော် သည် နိုင် ငံ တော် သမ္မ တ က ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး များ အ ဖြစ် ခ န့် အပ် ရန် အ မည် စာ ရင်း တင် သွင်း သူ များ ကို ငြင်း ပယ် ခွ င့် မ ရှိ စေ ရ ။ 
Line 7831: Initialize search took 0.009 seconds total
Translating: နိုင် ငံ တော် သမ္မ တ သည် ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး အ ဖြစ် ခ န့် အပ် တာ ဝန် ပေး ရန် ပြည် ထောင် စု လွှတ် တော် ၏ သ ဘော တူ ညီ ချက် မ ရ ရှိ သ ည့် ပုဂ္ဂိုလ် အ စား အ မည် စာ ရင်း သစ် ကို ပြည် ထောင် စု လွှတ် တော် သို့ ထပ် မံ တင် သွင်း ခွ င့် ရှိ သည် ။ 
Line 7832: Initialize search took 0.013 seconds total
Line 7826: Search took 3.408 seconds
Line 7826: Decision rule took 0.000 seconds total
Line 7826: Additional reporting took 0.000 seconds total
Line 7826: Translation took 4.067 seconds total
Translating: ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် သို့ မ ဟုတ် ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး များ သည် နိုင် ငံ့ ဝန် ထမ်း ဖြစ် လျှင် ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် သို့ မ ဟုတ် ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး အ ဖြစ် ခ န့် အပ် တာ ဝန် ပေး ခြင်း ခံ ရ သ ည့် နေ့ မှ စ ၍ တည် ဆဲ ဝန် ထမ်း စည်း မျဉ်း စည်း ကမ်း များ နှ င့် အ ညီ အ ငြိမ်း စား ယူ ပြီး ဖြစ် သည် ဟု မှတ် ယူ ရ မည် ။ 
Line 7833: Initialize search took 0.013 seconds total
Line 7832: Collecting options took 0.217 seconds at moses/Manager.cpp Line 141
Line 7833: Collecting options took 0.349 seconds at moses/Manager.cpp Line 141
Line 7831: Collecting options took 1.006 seconds at moses/Manager.cpp Line 141
Line 7805: Search took 24.157 seconds
BEST TRANSLATION: relevant self-administered division or self-administered zone , the chairperson and members of the leading သည်–|UNK|UNK|UNK ( 1 ) of the relevant of the self-administered division or self-administered zone residing in the relevant of the self-administered division or self-administered zone and ethnic nationalities , except the national races and with suitable population , as a population of at least 10,000 and above concerned prescribed by the ethnic nationalities if it is national races representatives each to members elected as the shall be appointed The elected member of the leading body under section 169 . Region or State Hluttaw representatives prescribed shall have qualifications ( 2 ) , the self-administered division leading body or self-administered zone leading bodies in the number of members , 10 as the number of members , at least 10 full the required number of members of the self-administered division or the self-administered zone residents from among under section 169 . Region or State Hluttaw representatives prescribed qualifications suitable persons their consent voluntarily chosen be filled . [1111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111]  [total=-219.778] core=(-100.000,-169.000,78.000,-284.628,-852.446,-145.969,-515.457,-124.887,0.000,-0.406,-108.818,0.000,-0.960,-10.000,-682.199)  
BEST TRANSLATION: of the self-administered division or the self-administered zone leading members assigned duty by the commander-in-chief of the defence services , to in accord with the law and shall submit a list of the Tatmadaw Region or State Hluttaw representatives shall have qualifications . [1111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111]  [total=-21.910] core=(0.000,-43.000,14.000,-45.565,-188.905,-33.435,-129.689,-23.033,0.000,0.000,-16.793,0.000,0.000,0.000,-112.769)  
BEST TRANSLATION: the provisions of the constitution , if not contrary to the self-administered division leading body or self-administered zone , the self- executive power of the leading bodies of the following matters ( a ) ; the schedule three of the self-administered division leading body or self-administered zone leading bodies of the law and matters ( b ) , the law enacted by the Pyidaungsu Hluttaw , any of the self-administered division leading body or self-administered zone leading bodies to carry out the matters permitted ( c ) , the relevant Region or State Hluttaw any law enacted by the self-administered division leading body or self-administered zone leading bodies to carry out the matters permitted extends . [111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111]  [total=-58.651] core=(0.000,-116.000,38.000,-101.509,-432.124,-83.272,-368.998,-61.172,-0.336,-0.123,-64.880,-2.944,-2.193,-8.000,-334.490)  
BEST TRANSLATION: self-administered division leading body or self-administered zone leading bodies of the union government preserves stability of the union , community peace and tranquility and prevalence of law and order in preserving responsible to help . [111111111111111111111111111111111111111111111111111111111111111111111111111]  [total=-17.013] core=(0.000,-35.000,10.000,-22.268,-153.839,-15.756,-128.487,-15.742,0.000,0.000,-16.299,0.000,0.000,0.000,-82.589)  
BEST TRANSLATION: self-administered division leading body or self-administered zone leading bodies of the union government policies and against within their territory all-round development for implementing its work plans for the relevant region or state through negotiations with the government . [1111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111]  [total=-28.008] core=(0.000,-38.000,16.000,-56.846,-239.173,-29.212,-115.967,-23.003,0.000,0.000,-22.596,0.000,0.000,0.000,-138.369)  
BEST TRANSLATION: self-administered division leading body or self-administered zone leading bodies of the annual budgets of the constitution in accordance with the provisions of the relevant region or state government , in co-ordination with the agreement shall be obtained . [111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111]  [total=-21.133] core=(0.000,-38.000,13.000,-35.833,-187.167,-24.100,-120.039,-20.415,0.000,0.000,-19.336,0.000,0.000,0.000,-104.256)  
BEST TRANSLATION: self-administered division leading body or self-administered zone leading bodies of the relevant region or state budget law and allotted budget prescribed in accordance with rules and regulations of finance . [1111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111]  [total=-21.718] core=(0.000,-30.000,13.000,-58.618,-210.576,-20.703,-97.959,-20.446,0.000,0.000,-19.071,0.000,0.000,0.000,-87.149)  
BEST TRANSLATION: self-administered division leading body or self-administered zone leading bodies of the financial year before the expiry of the relevant region or state parliament budget law may not in the region or state concerned from the government budget permission time before the Region or State Hluttaw is budget law which is permitted expenditure within the framework of the . [11111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111]  [total=-44.635] core=(0.000,-58.000,26.000,-116.870,-368.808,-51.337,-171.693,-47.431,0.000,0.000,-44.729,0.000,0.000,0.000,-215.771)  
Line 7805: Decision rule took 0.001 seconds total
Line 7805: Additional reporting took 0.001 seconds total
Line 7805: Translation took 26.691 seconds total
Translating: ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် နှ င့် ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး များ သည် အောက် ပါ အ ရည် အ ချင်း ( က ) အ သက် ၅၀ နှစ် ထက် မ ငယ် အ သက် ၇၀ နှစ် ထက် မ ကြီး သူ ( ခ ) အ သက် က န့် သတ် ချက် မှ အ ပ ပုဒ် မ ၁၂၀ တွင် ဖော် ပြ ထား သ ည့် ပြည် သူ့ လွှတ် တော် ကိုယ် စား လှယ် များ အ တွက် သတ် မှတ် ထား သော အ ရည် အ ချင်း များ နှ င့် ပြ ည့် စုံ သူ ( ဂ ) ပုဒ် မ ၁၂၁ တွင် ဖော် ပြ ထား သ ည့် ပြည် သူ့ လွှတ် တော် ကိုယ် စား လှယ် များ အ ဖြစ် ရွေး ကောက် တင် မြှောက် ခံ ပိုင် ခွ င့် မ ရှိ စေ သော ပြဋ္ဌာန်း ချက် များ နှ င့် လည်း ငြိ စွန်း ခြင်း မ ရှိ သူ ( ဃ ) ( ၁ ) တိုင်း ဒေ သ ကြီး သို့ မ ဟုတ် ပြည် နယ် တ ရား လွှတ် တော် တ ရား သူ ကြီး အ ဖြစ် အ နည်း ဆုံး ငါး နှစ် ဆောင် ရွက် ခဲ့ သူ သို့ မ ဟုတ် ( ၂ ) တိုင်း ဒေ သ ကြီး သို့ မ ဟုတ် ပြည် နယ် အ ဆ င့် ထက် မ နိ မ့် သော တ ရား ရေး အ ရာ ရှိ သို့ မ ဟုတ် ဥ ပ ဒေ အ ရာ ရှိ ရာ ထူး တွင် အ နည်း ဆုံး ၁၀ နှစ် တာ ဝန် ထမ်း ဆောင် ခဲ့ သူ သို့ မ ဟုတ် ( ၃ ) တ ရား လွှတ် တော် ရှေ့ နေ အ ဖြစ် အ နည်း ဆုံး ၂၀ နှစ် အ မှု လိုက် ပါ ဆောင် ရွက် ခဲ့ သူ သို့ မ ဟုတ် ( ၄ ) ထင် ပေါ် ကျော် ကြား သ ည့် ဂုဏ် သ တင်း ရှိ သော ဥ ပ ဒေ ပ ညာ ရှင် အ ဖြစ် နိုင် ငံ တော် သမ္မ တ က ယူ ဆ သူ ၊ ( င ) နိုင် ငံ တော် နှ င့် နိုင် ငံ သား များ အ ပေါ် သစ္စာ ရှိ သူ ( စ ) နိုင် ငံ ရေး ပါ တီ ဝင် မ ဟုတ် သူ ( ဆ ) လွှတ် တော် ကိုယ် စား လှယ် မ ဟုတ် သူ များ နှ င့် ပြ ည့် စုံ ရ မည် ။ 
Line 7834: Initialize search took 0.112 seconds total
Line 7829: Search took 4.275 seconds
Line 7829: Decision rule took 0.000 seconds total
Line 7829: Additional reporting took 0.000 seconds total
Line 7829: Translation took 5.933 seconds total
Translating: နိုင် ငံ တော် သမ္မ တ သို့ မ ဟုတ် ပြည် သူ့ လွှတ် တော် သို့ မ ဟုတ် အ မျိုး သား လွှတ် တော် ကိုယ် စား လှယ် များ သည် ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် သို့ မ ဟုတ် ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး တစ် ဦး ဦး အား အောက် ပါ အ ကြောင်း တစ် ရပ် ရပ် ဖြ င့် ( ၁ ) နိုင် ငံ တော် ၏ ကျေး ဇူး သစ္စာ တော် ကို ဖောက် ဖျက် ခြင်း ( ၂ ) ဖွဲ့ စည်း ပုံ အ ခြေ ခံ ဥ ပ ဒေ ပါ ပြဋ္ဌာန်း ချက် တစ် ရပ် ရပ် ကို ဖောက် ဖျက် ကျူး လွန် ခြင်း ( ၃ ) အ ကျ င့် သိက္ခာ ပျက် ပြား ခြင်း ( ၄ ) ပုဒ် မ ၃၀၁ တွင် ပြဋ္ဌာန်း ထား သော ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် နှ င့် ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး များ ၏ အ ရည် အ ချင်း ပျက် ယွင်း ခြင်း ( ၅ ) ဥ ပ ဒေ အ ရ ပေး အပ် သော တာ ဝန် များ ကို ကျေ ပွန် စွာ မ ဆောင် ရွက် ခြင်း များ နှ င့် စွပ် စွဲ ပြစ် တင် နိုင် သည် ။ 
Line 7835: Initialize search took 0.046 seconds total
Line 7834: Collecting options took 1.332 seconds at moses/Manager.cpp Line 141
Line 7832: Search took 3.136 seconds
Line 7832: Decision rule took 0.000 seconds total
Line 7832: Additional reporting took 0.000 seconds total
Line 7832: Translation took 3.366 seconds total
Line 7835: Collecting options took 0.720 seconds at moses/Manager.cpp Line 141
Killed

real	29m21.799s
user	171m2.735s
sys	0m29.617s
```

## Controlling the Input Length

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran/my-en$ ls
dev.myen.hyp  tmp
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran/my-en$ cd ..
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran$ time /home/ye/tool/mosesbin/ubuntu-17.04/moses/bin/moses -threads 4 --max-phrase-length 150 -f /home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/tuning/moses.tuned.ini.1 -i /home/ye/exp/smt/wat2021/exp-syl4/data/train.my > ./my-en/train.myen.hyp
Defined parameters (per moses.ini or switch):
	config: /home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/tuning/moses.tuned.ini.1 
	distortion-limit: 6 
	feature: UnknownWordPenalty WordPenalty PhrasePenalty PhraseDictionaryCompact name=TranslationModel0 num-features=4 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/model/phrase-table.minphr input-factor=0 output-factor=0 LexicalReordering name=LexicalReordering0 num-features=6 type=wbe-msd-bidirectional-fe-allff input-factor=0 output-factor=0 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/model/reordering-table.1.wbe-msd-bidirectional-fe.gz Distortion KENLM name=LM0 factor=0 path=/home/ye/exp/smt/wat2021/exp-syl4//baseline/my-en/lm/myrk.binlm.1 order=6 
	input-factors: 0 
	input-file: /home/ye/exp/smt/wat2021/exp-syl4/data/train.my 
	mapping: 0 T 0 
	max-phrase-length: 150 
	threads: 4 
	weight: LexicalReordering0= 0.0295063 0.144319 0.114957 0.0621906 -0.0220501 0.0307571 Distortion0= 0.0628715 LM0= 0.0865004 WordPenalty0= -0.224658 PhrasePenalty0= -0.026615 TranslationModel0= -0.00641249 0.0654316 0.0872244 0.0365068 UnknownWordPenalty0= 1 
line=UnknownWordPenalty
FeatureFunction: UnknownWordPenalty0 start: 0 end: 0
line=WordPenalty
FeatureFunction: WordPenalty0 start: 1 end: 1
line=PhrasePenalty
FeatureFunction: PhrasePenalty0 start: 2 end: 2
line=PhraseDictionaryCompact name=TranslationModel0 num-features=4 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/model/phrase-table.minphr input-factor=0 output-factor=0
FeatureFunction: TranslationModel0 start: 3 end: 6
line=LexicalReordering name=LexicalReordering0 num-features=6 type=wbe-msd-bidirectional-fe-allff input-factor=0 output-factor=0 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/model/reordering-table.1.wbe-msd-bidirectional-fe.gz
Initializing Lexical Reordering Feature..
FeatureFunction: LexicalReordering0 start: 7 end: 12
line=Distortion
FeatureFunction: Distortion0 start: 13 end: 13
line=KENLM name=LM0 factor=0 path=/home/ye/exp/smt/wat2021/exp-syl4//baseline/my-en/lm/myrk.binlm.1 order=6
FeatureFunction: LM0 start: 14 end: 14
Loading UnknownWordPenalty0
Loading WordPenalty0
Loading PhrasePenalty0
Loading LexicalReordering0
Loading table into memory...done.
Loading Distortion0
Loading LM0
Loading TranslationModel0
Created input-output object : [34.430] seconds
Translating: ရဲ များ က စုံ Translating: Translating: စမ်း လျက် ရှိ သည် ။ 
Line 1: Initialize search took 0.000 seconds total
ကြိမ် ချောင်း ရဲ စ ခန်း တွင် လူ သတ် မှု ဖြ င့် အ မှု ဖွ င့် ထား ပြီး ပြီ ။ 
ရဲ များ သည် မစ် ဆူ ဘီ ရှီ ပါ ဂျဲ ရိုး ကားLine 0: Initialize search took  တစ်0.001 seconds total
 စီး ကို ရပ် တန်း ခိုင်း ခဲ့ ပြီး စစ် ဆေး ခဲ့ သည် ။ 
Line 3: Initialize search took 0.001 seconds total
Translating: တပ် မ တော် တပ် ဖွဲ့ သည် ရှမ်း ပြည် နယ် မြောက် ပိုင်း တာ မိုး ညဲ မြို့ ၌ မ နေ့ က ရှောင် တ ခင် စစ် ဆေး မှု တစ် ခု ပြု လုပ် စဉ် အ တွင်း ယာဉ် တစ် စီး မှ လက် နက် များ နှ င့် တ ရား မ ဝင် သစ် များ ကို ဖမ်း ဆီး ရ မိ ခဲ့ သည် ။ 
Line 2: Initialize search took 0.002 seconds total
Line 1: Collecting options took 0.174 seconds at moses/Manager.cpp Line 141
Line 0: Collecting options took 0.224 seconds at moses/Manager.cpp Line 141
Line 3: Collecting options took 0.240 seconds at moses/Manager.cpp Line 141
Line 1: Search took 0.116 seconds
Line 1: Decision rule took 0.000 seconds total
Line 1: Additional reporting took 0.000 seconds total
Line 1: Translation took 0.291 seconds total
Translating: ရဲ များ သည် ကျည် ခု နှစ် တော င့် နှ င့် အ တူ ပစ္စ တို တစ် လက် နှ င့် သစ် ခွဲ သား ဆိုဒ် စုံ အ ချောင်း ၇၄၀ ကို ရှာ ဖွေ တွေ့ ရှိ ခဲ့ သည် ။ 
Line 4: Initialize search took 0.000 seconds total
Line 0: Search took 0.277 seconds
BEST TRANSLATION: at the Kyeikgyaung police station murder case has been opened . [1111111111111111111]  [total=-7.684] core=(0.000,-11.000,4.000,-10.355,-43.924,-3.028,-41.751,-5.762,0.000,0.000,-4.828,0.000,0.000,0.000,-57.596)  
BEST TRANSLATION: Police are investigating . [111111111]  [total=-2.291] core=(0.000,-4.000,1.000,-0.690,-17.066,-0.690,-14.289,-0.511,0.000,0.000,0.000,0.000,0.000,0.000,-16.813)  
Line 0: Decision rule took 0.000 seconds total
Line 0: Additional reporting took 0.000 seconds total
Line 0: Translation took 0.502 seconds total
Translating: ဒေ သ ခံ အာ ဏာ ပိုင် များ ၏ အ ဆို အ ရ ကား ဒ ရိုက် ဘာ ဦး စိုင်း ကျော် ဝင်း နှ င့် ကား ပေါ် တွင် ပစ္စ တို သယ် ဆောင် လာ သူ ခ ရီး သည် တစ် ဦး ဖြစ် သော ဦး သန်း မောင် တို့ ကို တာ မိုး ညဲ ရဲ စ ခန်း သို့ လွှဲ ပြောင်း အပ် နှံ မည် ။ 
Line 5: Initialize search took 0.001 seconds total
Line 3: Search took 0.278 seconds
Line 3: Decision rule took 0.000 seconds total
Line 3: Additional reporting took 0.000 seconds total
Line 3: Translation took 0.518 seconds total
Translating: တပ် မ တော် စစ် ကြောင်း နှ င့် ကေ အိုင် အေ လက် နက် ကိုင် များ အ ကြား တိုက် ပွဲ ဖြစ် ပွား ခဲ့ သည် ။ 
Line 6: Initialize search took 0.000 seconds total
...
...
...
Translating: နိုင် ငံ တော် ဖွဲ့ စည်း ပုံ အ ခြေ ခံ ဥ ပ ဒေ ဆိုင် ရာ ခုံ ရုံး ဥက္ကဋ္ဌ နှ င့် အ ဖွဲ့ ဝင် တစ် ဦး ဦး အ ပေါ် စွပ် စွဲ ပြစ် တင် လို ပါ က ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် သို့ မ ဟုတ် ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး တစ် ဦး ဦး အား စွပ် စွဲ ပြစ် တင် ခြင်း နှ င့် စပ် လျဉ်း ၍ ပုဒ် မ ၃၀၂ ပါ ပြဋ္ဌာန်း ချက် များ နှ င့် အ ညီ ဆောင် ရွက် ရ မည် ။ 
Line 7870: Initialize search took 0.013 seconds total
Line 7870: Collecting options took 1.101 seconds at moses/Manager.cpp Line 141
Line 7869: Search took 7.101 seconds
Line 7869: Decision rule took 0.001 seconds total
Line 7869: Additional reporting took 0.002 seconds total
Line 7869: Translation took 8.186 seconds total
Translating: သို့ ရာ တွင် သက် တမ်း ကုန် ဆုံး ပြီး ဖြစ် သော် လည်း လက် ရှိ တာ ဝန် ထမ်း ဆောင် လျက် ရှိ သော နိုင် ငံ တော် ဖွဲ့ စည်း ပုံ အ ခြေ ခံ ဥ ပ ဒေ ဆိုင် ရာ ခုံ ရုံး သည် ဖွဲ့ စည်း ပုံ အ ခြေ ခံ ဥ ပ ဒေ အ ရ နိုင် ငံ တော် သမ္မ တ က နိုင် ငံ တော် ဖွဲ့ စည်း ပုံ အ ခြေ ခံ ဥ ပ ဒေ ဆိုင် ရာ ခုံ ရုံး အ သစ် ဖွဲ့ စည်း ပြီး သ ည့် အ ချိန် အ ထိ မိ မိ ၏ လုပ် ငန်း တာ ဝန် များ ကို ဆက် လက် တာ ဝန် ထမ်း ဆောင် ရ မည် ။ 
Line 7871: Initialize search took 0.007 seconds total
Line 7871: Collecting options took 1.847 seconds at moses/Manager.cpp Line 141
Line 7870: Search took 5.824 seconds
Line 7870: Decision rule took 0.001 seconds total
Line 7870: Additional reporting took 0.001 seconds total
Line 7870: Translation took 6.941 seconds total
Translating: အောက် ဖော် ပြ ပါ အ ရည် အ ချင်း တစ် ရပ် ရပ် ( က ) ပြည် ထောင် စု သမ္မ တ မြန် မာ နိုင် ငံ တော် ၏ တိုင်း ရင်း သား မိ ဘ နှစ် ပါး မှ မွေး ဖွား သူ ( ခ ) ဤ ဖွဲ့ စည်း ပုံ အ ခြေ ခံ ဥ ပ ဒေ အ တည် ပြု ပြဋ္ဌာန်း သ ည့် နေ့ တွင် ဥ ပ ဒေ အ ရ နိုင် ငံ သား ဖြစ် ပြီး သူ နှ င့် ပြ ည့် စုံ သူ များ သည် ပြည် ထောင် စု သမ္မ တ မြန် မာ နိုင် ငံ တော် ၏ နိုင် ငံ သား များ ဖြစ် ကြ သည် ။ 
Line 7872: Initialize search took 0.006 seconds total
Line 7872: Collecting options took 1.532 seconds at moses/Manager.cpp Line 141
Killed

real	39m7.887s
user	151m1.157s
sys	0m32.294s
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran$
```

အထက်မှာ မြင်ရတဲ့အတိုင်း line နံပါတ် 7800 ပတ်ဝန်းကျင်မှာ killed ဖြစ်ဖြစ်သွားတာကို တွေ့ရ...  

ပထမတစ်ခေါက် translated output ဖိုင်နဲ့ နှိုင်းယှဉ်ကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရ...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran/my-en$ wc *
   1000   30674  159260 dev.myen.hyp
wc: tmp: Is a directory
      0       0       0 tmp
   7863  157411  903674 train.myen.hyp
   8863  188085 1062934 total
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran/my-en$ wc ./tmp/train.myen.hyp 
  7813 153657 883681 ./tmp/train.myen.hyp
```

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran/my-en$ tail -3 ./tmp/train.myen.hyp 
self-administered division leading body or self-administered zone leading bodies of the annual budgets of the constitution in accordance with the provisions of the relevant region or state government , in co-ordination with the agreement shall be obtained . 
self-administered division leading body or self-administered zone leading bodies of the relevant region or state budget law and allotted budget prescribed in accordance with rules and regulations of finance . 
self-administered division leading body or self-administered zone leading bodies of the financial year before the expiry of the relevant region or state parliament budget law may not in the region or state concerned from the government budget permission time before the Region or State Hluttaw is budget law which is permitted expenditure within the framework of the . 
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran/my-en$ tail -3 ./train.myen.hyp 
region or state under the supervision of the high court of the courts at different levels of judges jurisdictions Magistral powers , duties , powers and rights , and prescribing , in accord with the law . 
The supreme court of the union , region or state and courts in the other ranks and staff of the staff institutional duties , powers and prescribing , in accord with the law . 
The president select three members of the speaker of the Pyithu Hluttaw elected by the three members and Amyotha Hluttaw speaker select three members of the total nine the list of its of the state , the constitution tribunal , chairman of the member &amp; apos ; s be submitted to the Pyidaungsu Hluttaw for its approval . 
```

Hint အနေနဲ့တော့ ငါ ဘာမှ မရသလိုပဲ...  
သို့သော်... သို့သော်... နောက်ဆုံးရပ်သွားတဲ့ စာကြောင်း တွေကို word count လုပ်ကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရ...  

``
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran/my-en$ echo "The president select three members of the speaker of the Pyithu Hluttaw elected by the three members and Amyotha Hluttaw speaker select three members of the total nine the list of its of the state , the constitution tribunal , chairman of the member &amp; apos ; s be submitted to the Pyidaungsu Hluttaw for its approval ." | wc
      1      58     323
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran/my-en$ echo "self-administered division leading body or self-administered zone leading bodies of the financial year before the expiry of the relevant region or state parliament budget law may not in the region or state concerned from the government budget permission time before the Region or State Hluttaw is budget law which is permitted expenditure within the framework of the ." | wc
      1      58     369
```

wc ရလဒ်က "58" လုံး တူနေတာကို သွားတွေ့ရ...  
သေချာတယ် no. of words, phrase length တို့နဲ့ ပတ်သက်မှုရှိကို ရှိရမယ်...  

## Try again

ဒီတစ်ခါတော့ -threads all ပြန်ထားပြီး၊ max-phrase-length option ကို မထည့်ပဲ ထားကြည့်လိုက်တယ်....  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran$ time /home/ye/tool/mosesbin/ubuntu-17.04/moses/bin/moses -threads all -f /home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/tuning/moses.tuned.ini.1 -i /home/ye/exp/smt/wat2021/exp-syl4/data/train.my > ./my-en/train.myen.hyp

Line 7825: Initialize search took 0.031 seconds total
Line 7820: Search took 3.039 seconds
Line 7820: Decision rule took 0.000 seconds total
Line 7820: Additional reporting took 0.000 seconds total
Line 7820: Translation took 3.416 seconds total
Translating: ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် သည် ဖွဲ့ စည်း ပုံ အ ခြေ ခံ ဥ ပ ဒေ ပါ ပြဋ္ဌာန်း ချက် တစ် ရပ် ရပ် ကို ဖြစ် စေ အ ခြား ဥ ပ ဒေ ပါ ပြဋ္ဌာန်း ချက် တစ် ရပ် ရပ် ကို ဖြစ် စေ မ ဆ န့် ကျင် စေ ဘဲ တိုင်း ဒေ သ ကြီး သို့ မ ဟုတ် ပြည် နယ် တ ရား လွှတ် တော် ၏ စီ ရင် ချက် များ ကို ဆုံး ဖြတ် နိုင် သော အ ယူ ခံ မှု စီ ရင် ပိုင် ခွ င့် အာ ဏာ ရှိ သည် ။ 
Line 7826: Initialize search took 0.008 seconds total
Line 7825: Collecting options took 0.553 seconds at moses/Manager.cpp Line 141
Line 7826: Collecting options took 0.474 seconds at moses/Manager.cpp Line 141
Line 7823: Search took 2.095 seconds
Line 7823: Decision rule took 0.000 seconds total
Line 7823: Additional reporting took 0.000 seconds total
Line 7823: Translation took 2.560 seconds total
Translating: ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် သည် ( က ) အောက် ပါ စာ ချွန် တော် အ မိ န့် များ ( ၁ ) ရှေ့ တော် သွင်း စာ ချွန် တော် အ မိ န့် ( ၂ ) အာ ဏာ ပေး စာ ချွန် တော် အ မိ န့် ( ၃ ) တား မြစ် စေ စာ ချွန် တော် အ မိ န့် ( ၄ ) အာ ဏာ ပိုင် မေး စာ ချွန် တော် အ မိ န့် ( ၅ ) အ မှု ခေါ် စာ ချွန် တော် အ မိ န့် ကို ထုတ် ပိုင် ခွ င့် အာ ဏာ ရှိ သည် ။ 
Line 7827: Initialize search took 0.005 seconds total
Line 7824: Search took 1.361 seconds
Line 7824: Decision rule took 0.000 seconds total
Line 7824: Additional reporting took 0.000 seconds total
Line 7824: Translation took 1.841 seconds total
Translating: ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် သည် တ ရား စီ ရင် ရေး ဆိုင် ရာ ဘဏ္ဍာ ငွေ အ ရ အ သုံး စာ ရင်း များ ကို ဖွဲ့ စည်း ပုံ အ ခြေ ခံ ဥ ပ ဒေ ပါ ပြဋ္ဌာန်း ချက် များ နှ င့် အ ညီ ပြည် ထောင် စု ၏ နှစ် စဉ် ဘဏ္ဍာ ငွေ အ ရ အ သုံး ဆိုင် ရာ ဥ ပ ဒေ ကြမ်း တွင် ထ ည့် သွင်း တင် ပြ နိုင် ရန် ပြည် ထောင် စု အ စိုး ရ ထံ တင် ပြ ရ မည် ။ 
Line 7828: Initialize search took 0.015 seconds total
Line 7827: Collecting options took 0.198 seconds at moses/Manager.cpp Line 141
Line 7805: Search took 20.932 seconds
BEST TRANSLATION: relevant self-administered division or self-administered zone , the chairperson and members of the leading သည်–|UNK|UNK|UNK ( 1 ) of the relevant of the self-administered division or self-administered zone residing in the relevant of the self-administered division or self-administered zone and ethnic nationalities , except the national races and with suitable population , as a population of at least 10,000 and above concerned prescribed by the ethnic nationalities if it is national races representatives each to members elected as the shall be appointed The elected member of the leading body under section 169 . Region or State Hluttaw representatives prescribed shall have qualifications ( 2 ) , the self-administered division leading body or self-administered zone leading bodies in the number of members , 10 as the number of members , at least 10 full the required number of members of the self-administered division or the self-administered zone residents from among under section 169 . Region or State Hluttaw representatives prescribed qualifications suitable persons their consent voluntarily chosen be filled . [1111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111]  [total=-219.778] core=(-100.000,-169.000,78.000,-284.628,-852.446,-145.969,-515.457,-124.887,0.000,-0.406,-108.818,0.000,-0.960,-10.000,-682.199)  
BEST TRANSLATION: of the self-administered division or the self-administered zone leading members assigned duty by the commander-in-chief of the defence services , to in accord with the law and shall submit a list of the Tatmadaw Region or State Hluttaw representatives shall have qualifications . [1111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111]  [total=-21.910] core=(0.000,-43.000,14.000,-45.565,-188.905,-33.435,-129.689,-23.033,0.000,0.000,-16.793,0.000,0.000,0.000,-112.769)  
BEST TRANSLATION: the provisions of the constitution , if not contrary to the self-administered division leading body or self-administered zone , the self- executive power of the leading bodies of the following matters ( a ) ; the schedule three of the self-administered division leading body or self-administered zone leading bodies of the law and matters ( b ) , the law enacted by the Pyidaungsu Hluttaw , any of the self-administered division leading body or self-administered zone leading bodies to carry out the matters permitted ( c ) , the relevant Region or State Hluttaw any law enacted by the self-administered division leading body or self-administered zone leading bodies to carry out the matters permitted extends . [111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111]  [total=-58.651] core=(0.000,-116.000,38.000,-101.509,-432.124,-83.272,-368.998,-61.172,-0.336,-0.123,-64.880,-2.944,-2.193,-8.000,-334.490)  
BEST TRANSLATION: self-administered division leading body or self-administered zone leading bodies of the union government preserves stability of the union , community peace and tranquility and prevalence of law and order in preserving responsible to help . [111111111111111111111111111111111111111111111111111111111111111111111111111]  [total=-17.013] core=(0.000,-35.000,10.000,-22.268,-153.839,-15.756,-128.487,-15.742,0.000,0.000,-16.299,0.000,0.000,0.000,-82.589)  
BEST TRANSLATION: self-administered division leading body or self-administered zone leading bodies of the union government policies and against within their territory all-round development for implementing its work plans for the relevant region or state through negotiations with the government . [1111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111]  [total=-28.008] core=(0.000,-38.000,16.000,-56.846,-239.173,-29.212,-115.967,-23.003,0.000,0.000,-22.596,0.000,0.000,0.000,-138.369)  
BEST TRANSLATION: self-administered division leading body or self-administered zone leading bodies of the annual budgets of the constitution in accordance with the provisions of the relevant region or state government , in co-ordination with the agreement shall be obtained . [111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111]  [total=-21.133] core=(0.000,-38.000,13.000,-35.833,-187.167,-24.100,-120.039,-20.415,0.000,0.000,-19.336,0.000,0.000,0.000,-104.256)  
BEST TRANSLATION: self-administered division leading body or self-administered zone leading bodies of the relevant region or state budget law and allotted budget prescribed in accordance with rules and regulations of finance . [1111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111]  [total=-21.718] core=(0.000,-30.000,13.000,-58.618,-210.576,-20.703,-97.959,-20.446,0.000,0.000,-19.071,0.000,0.000,0.000,-87.149)  
BEST TRANSLATION: self-administered division leading body or self-administered zone leading bodies of the financial year before the expiry of the relevant region or state parliament budget law may not in the region or state concerned from the government budget permission time before the Region or State Hluttaw is budget law which is permitted expenditure within the framework of the . [11111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111]  [total=-44.635] core=(0.000,-58.000,26.000,-116.870,-368.808,-51.337,-171.693,-47.431,0.000,0.000,-44.729,0.000,0.000,0.000,-215.771)  
Line 7805: Decision rule took 0.000 seconds total
Line 7805: Additional reporting took 0.000 seconds total
Line 7805: Translation took 22.065 seconds total
Translating: ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် သည် ပြည် ထောင် စု လွှတ် တော် အ စည်း အ ဝေး တွင် ဖြစ် စေ ပြည် သူ့ လွှတ် တော် သို့ မ ဟုတ် အ မျိုး သား လွှတ် တော် အ စည်း အ ဝေး တွင် ဖြစ် စေ နိုင် ငံ တော် သို့ မ ဟုတ် အ များ ပြည် သူ တို့ နှ င့် သက် ဆိုင် သ ည့် အ ရေး ကြီး သော တ ရား စီ ရင် ရေး ဆိုင် ရာ အ ခြေ အ နေ ကို အ ခါ အား လျော် စွာ တင် ပြ နိုင် သည် ။ 
Line 7829: Initialize search took 0.018 seconds total
Line 7828: Collecting options took 0.395 seconds at moses/Manager.cpp Line 141
Line 7821: Search took 5.044 seconds
Line 7821: Decision rule took 0.000 seconds total
Line 7821: Additional reporting took 0.000 seconds total
Line 7821: Translation took 5.282 seconds total
Translating: ပုဒ် မ ၃၀၁ တွင် သတ် မှတ် ထား သော ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် နှ င့် ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး များ ၏ အ ရည် အ ချင်း များ နှ င့် မ ပြ ည့် စုံ ကြောင်း အ ထင် အ ရှား မ ပြ နိုင် ပါ က ပြည် ထောင် စု လွှတ် တော် သည် နိုင် ငံ တော် သမ္မ တ က ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် အ ဖြစ် ခ န့် အပ် ရန် အ မည် စာ ရင်း တင် သွင်း သူ ကို ငြင်း ပယ် ခွ င့် မ ရှိ စေ ရ ။ 
Line 7830: Initialize search took 0.025 seconds total
Line 7829: Collecting options took 0.779 seconds at moses/Manager.cpp Line 141
Line 7826: Search took 3.050 seconds
Line 7826: Decision rule took 0.000 seconds total
Line 7826: Additional reporting took 0.000 seconds total
Line 7826: Translation took 3.532 seconds total
Translating: ပုဒ် မ ၃၀၁ တွင် သတ် မှတ် ထား သော ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် နှ င့် ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး များ ၏ အ ရည် အ ချင်း များ နှ င့် မ ပြ ည့် စုံ ကြောင်း အ ထင် အ ရှား မ ပြ နိုင် ပါ က ပြည် ထောင် စု လွှတ် တော် သည် နိုင် ငံ တော် သမ္မ တ က ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး များ အ ဖြစ် ခ န့် အပ် ရန် အ မည် စာ ရင်း တင် သွင်း သူ များ ကို ငြင်း ပယ် ခွ င့် မ ရှိ စေ ရ ။ 
Line 7831: Initialize search took 0.036 seconds total
Line 7830: Collecting options took 1.420 seconds at moses/Manager.cpp Line 141
Line 7831: Collecting options took 0.302 seconds at moses/Manager.cpp Line 141
Line 7816: Search took 9.648 seconds
Line 7816: Decision rule took 0.000 seconds total
Line 7816: Additional reporting took 0.000 seconds total
Line 7816: Translation took 11.256 seconds total
Translating: နိုင် ငံ တော် သမ္မ တ သည် ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး အ ဖြစ် ခ န့် အပ် တာ ဝန် ပေး ရန် ပြည် ထောင် စု လွှတ် တော် ၏ သ ဘော တူ ညီ ချက် မ ရ ရှိ သ ည့် ပုဂ္ဂိုလ် အ စား အ မည် စာ ရင်း သစ် ကို ပြည် ထောင် စု လွှတ် တော် သို့ ထပ် မံ တင် သွင်း ခွ င့် ရှိ သည် ။ 
Line 7832: Initialize search took 0.009 seconds total
Line 7827: Search took 3.674 seconds
Line 7827: Decision rule took 0.000 seconds total
Line 7827: Additional reporting took 0.000 seconds total
Line 7827: Translation took 3.878 seconds total
Translating: ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် သို့ မ ဟုတ် ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး များ သည် နိုင် ငံ့ ဝန် ထမ်း ဖြစ် လျှင် ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် သို့ မ ဟုတ် ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး အ ဖြစ် ခ န့် အပ် တာ ဝန် ပေး ခြင်း ခံ ရ သ ည့် နေ့ မှ စ ၍ တည် ဆဲ ဝန် ထမ်း စည်း မျဉ်း စည်း ကမ်း များ နှ င့် အ ညီ အ ငြိမ်း စား ယူ ပြီး ဖြစ် သည် ဟု မှတ် ယူ ရ မည် ။ 
Line 7833: Initialize search took 0.025 seconds total
Line 7832: Collecting options took 0.786 seconds at moses/Manager.cpp Line 141
Line 7833: Collecting options took 0.364 seconds at moses/Manager.cpp Line 141
Line 7828: Search took 3.923 seconds
Line 7828: Decision rule took 0.000 seconds total
Line 7828: Additional reporting took 0.000 seconds total
Line 7828: Translation took 4.333 seconds total
Line 7829: Search took 3.330 seconds
Line 7829: Decision rule took 0.000 seconds total
Line 7829: Additional reporting took 0.000 seconds total
Line 7829: Translation took 4.127 seconds total
Translating: နိုင် ငံ တော် သမ္မ တ သို့ မ ဟုတ် ပြည် သူ့ လွှတ် တော် သို့ မ ဟုတ် အ မျိုး သား လွှတ် တော် ကိုယ် စား လှယ် များ သည် ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် သို့ မ ဟုတ် ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး တစ် ဦး ဦး အား အောက် ပါ အ ကြောင်း တစ် ရပ် ရပ် ဖြ င့် ( ၁ ) နိုင် ငံ တော် ၏ ကျေး ဇူး သစ္စာ တော် ကို ဖောက် ဖျက် ခြင်း ( ၂ ) ဖွဲ့ စည်း ပုံ အ ခြေ ခံ ဥ ပ ဒေ ပါ ပြဋ္ဌာန်း ချက် တစ် ရပ် ရပ် ကို ဖောက် ဖျက် ကျူး လွန် ခြင်း ( ၃ ) အ ကျ င့် သိက္ခာ ပျက် ပြား ခြင်း ( ၄ ) ပုဒ် မ ၃၀၁ တွင် ပြဋ္ဌာန်း ထား သော ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် နှ င့် ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး များ ၏ အ ရည် အ ချင်း ပျက် ယွင်း ခြင်း ( ၅ ) ဥ ပ ဒေ အ ရ ပေး အပ် သော တာ ဝန် များ ကို ကျေ ပွန် စွာ မ ဆောင် ရွက် ခြင်း များ နှ င့် စွပ် စွဲ ပြစ် တင် နိုင် သည် ။ 
Line 7835: Initialize search took 0.027 seconds total
Translating: ပြည် ထောင် စု တ ရား သူ ကြီး ချုပ် နှ င့် ပြည် ထောင် စု တ ရား လွှတ် တော် ချုပ် တ ရား သူ ကြီး များ သည် အောက် ပါ အ ရည် အ ချင်း ( က ) အ သက် ၅၀ နှစ် ထက် မ ငယ် အ သက် ၇၀ နှစ် ထက် မ ကြီး သူ ( ခ ) အ သက် က န့် သတ် ချက် မှ အ ပ ပုဒ် မ ၁၂၀ တွင် ဖော် ပြ ထား သ ည့် ပြည် သူ့ လွှတ် တော် ကိုယ် စား လှယ် များ အ တွက် သတ် မှတ် ထား သော အ ရည် အ ချင်း များ နှ င့် ပြ ည့် စုံ သူ ( ဂ ) ပုဒ် မ ၁၂၁ တွင် ဖော် ပြ ထား သ ည့် ပြည် သူ့ လွှတ် တော် ကိုယ် စား လှယ် များ အ ဖြစ် ရွေး ကောက် တင် မြှောက် ခံ ပိုင် ခွ င့် မ ရှိ စေ သော ပြဋ္ဌာန်း ချက် များ နှ င့် လည်း ငြိ စွန်း ခြင်း မ ရှိ သူ ( ဃ ) ( ၁ ) တိုင်း ဒေ သ ကြီး သို့ မ ဟုတ် ပြည် နယ် တ ရား လွှတ် တော် တ ရား သူ ကြီး အ ဖြစ် အ နည်း ဆုံး ငါး နှစ် ဆောင် ရွက် ခဲ့ သူ သို့ မ ဟုတ် ( ၂ ) တိုင်း ဒေ သ ကြီး သို့ မ ဟုတ် ပြည် နယ် အ ဆ င့် ထက် မ နိ မ့် သော တ ရား ရေး အ ရာ ရှိ သို့ မ ဟုတ် ဥ ပ ဒေ အ ရာ ရှိ ရာ ထူး တွင် အ နည်း ဆုံး ၁၀ နှစ် တာ ဝန် ထမ်း ဆောင် ခဲ့ သူ သို့ မ ဟုတ် ( ၃ ) တ ရား လွှတ် တော် ရှေ့ နေ အ ဖြစ် အ နည်း ဆုံး ၂၀ နှစ် အ မှု လိုက် ပါ ဆောင် ရွက် ခဲ့ သူ သို့ မ ဟုတ် ( ၄ ) ထင် ပေါ် ကျော် ကြား သ ည့် ဂုဏ် သ တင်း ရှိ သော ဥ ပ ဒေ ပ ညာ ရှင် အ ဖြစ် နိုင် ငံ တော် သမ္မ တ က ယူ ဆ သူ ၊ ( င ) နိုင် ငံ တော် နှ င့် နိုင် ငံ သား များ အ ပေါ် သစ္စာ ရှိ သူ ( စ ) နိုင် ငံ ရေး ပါ တီ ဝင် မ ဟုတ် သူ ( ဆ ) လွှတ် တော် ကိုယ် စား လှယ် မ ဟုတ် သူ များ နှ င့် ပြ ည့် စုံ ရ မည် ။ 
Line 7834: Initialize search took 0.299 seconds total
Line 7835: Collecting options took 0.693 seconds at moses/Manager.cpp Line 141
Line 7834: Collecting options took 1.119 seconds at moses/Manager.cpp Line 141
Line 7830: Search took 4.320 seconds
Line 7830: Decision rule took 0.000 seconds total
Line 7830: Additional reporting took 0.000 seconds total
Line 7830: Translation took 5.766 seconds total
Line 7831: Search took 4.649 seconds
Line 7831: Decision rule took 0.000 seconds total
Line 7831: Additional reporting took 0.000 seconds total
Line 7831: Translation took 4.998 seconds total
Translating: နိုင် ငံ တော် သမ္မ တ က စွပ် စွဲ ပြစ် တင် ရန် လို အပ် ပါ က စုံ စမ်း စစ် ဆေး ရေး အ ဖွဲ့ ကို ဖွဲ့ စည်း ရာ တွင် ပြည် သူ့ လွှတ် တော် နှ င့် အ မျိုး သား လွှတ် တော် ကိုယ် စား လှယ် ဦး ရေ တူ ညီ စွာ ပါ ဝင် စေ ပြီး ယင်း အ ဖွဲ့ ဝင် များ ထဲ မှ သ င့် လျော် သူ တစ် ဦး ဦး ကို စုံ စမ်း စစ် ဆေး ရေး အ ဖွဲ့ ဥက္ကဋ္ဌ အ ဖြစ် တာ ဝန် ပေး ရ မည် ။ 
Line 7837: Initialize search took 0.009 seconds total
Killed

real	28m51.184s
user	172m19.783s
sys	0m24.932s
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/exp/smt/wat2021/exp-syl4-tran$
```


## Reference

https://garbo999.github.io/moses/2017/05/25/moses-error-loading-table-into-memory-killed.html  
https://moses-support.mit.narkive.com/9UOIYHZZ/phrasedictionarycompact-problem  
http://www.statmt.org/moses/?n=Advanced.RuleTables  
https://garbo999.github.io/moses/2017/08/23/binarise-phrase-table-lexicalised-reordering-models.html  
