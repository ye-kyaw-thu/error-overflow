# Phrase Table Loading Error and Building Compact Phrase Table

## Decoding/Translation Error

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

-i နဲ့ input မပေးလည်း မရဘူး။  
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

## Compact Phrase Table

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

```
#PhraseDictionaryMemory name=TranslationModel0 num-features=4 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/model/phrase-table.1.gz input-factor=0 output-factor=0
PhraseDictionaryCompact name=TranslationModel0 num-features=4 path=/home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/model/phrase-table.minphr input-factor=0 output-factor=0
```

## Test Translation with STDIO

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

```
$/home/ye/tool/mosesbin/ubuntu-17.04/moses/bin/moses -threads all --max-phrase-length 200 -f /home/ye/exp/smt/wat2021/exp-syl4/baseline/my-en/tuning/moses.tuned.ini.1 -i /home/ye/exp/smt/wat2021/exp-syl4/data/train.my > ./my-en/train.myen.hyp
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
```

## Reference

https://garbo999.github.io/moses/2017/05/25/moses-error-loading-table-into-memory-killed.html  
https://moses-support.mit.narkive.com/9UOIYHZZ/phrasedictionarycompact-problem  
http://www.statmt.org/moses/?n=Advanced.RuleTables  
https://garbo999.github.io/moses/2017/08/23/binarise-phrase-table-lexicalised-reordering-models.html  
