# Revisiting WFST-MT Experiment

WFST ကို သုံးပြီး MT ကို ဒီတစ်ခါတော့ ဘိတ်-ထားဝယ် နဲ့ ဘိတ်-ရခိုင် အတွဲနှစ်ခုကြားကို လုပ်ကြည့်မယ်။  

y@CADT  
03 May 2022  

## Copy Running Scripts

ရှေ့မှာ လုပ်ထားခဲ့တုန်းက ရေးထားခဲ့တဲ့၊ သုံးခဲ့တဲ့ script တွေကို အခုအသစ်လုပ်မယ့် experiment folder path အောက်ကို ကူးထည့်ခဲ့...  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp$ cp -r ready-to-run-scripts/ /media/ye/project1/exp/wfst-mt/exp/wfst-cadt
```

check the files ...  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt$ ls ./ready-to-run-scripts/
bigram.py         mk-symbol.pl        onetoone.py               test.sh
demo-data         mk-train-symbol.sh  shortest-path-to-line.sh  train-test-eval.sh
eval.sh           mk-uniq-word.sh     symbols.py                translate-nofstdraw.sh
mk-fst-format.pl  multi-test.sh       test-nofstdraw.sh         translate.sh
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt$
```

## Data Preparation  

training ဒေတာနဲ့ development ဒေတာကို ပေါင်းပြီး wfst ဆောက်ရမှာမို့ အဲဒီအတွက် ဒေတာကို ပြင်ခဲ့...  

for dw-bk pair:  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/dw-bk/1$ cp *.dw ../../4wfst/dw-bk/1/
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/dw-bk/1$ cp *.bk ../../4wfst/dw-bk/1/
```

4wfst/dw-bk/1/ အောက်ကို ရွှေ့ပြီးတော့ ...  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/4wfst/dw-bk/1$ ls
dev.bk  dev.dw  test.bk  test.dw  train.bk  train.dw
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/4wfst/dw-bk/1$ cat train.bk dev.bk > ../train.bk
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/4wfst/dw-bk/1$ cat train.dw dev.dw > ../train.dw
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/4wfst/dw-bk/1$ cd ..
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/4wfst/dw-bk$ wc *
wc: 1: Is a directory
      0       0       0 1
    670    4267   60615 test.bk
    670    4013   64228 test.dw
   5952   37686  540873 train.bk
   5952   35646  573030 train.dw
  13244   81612 1238746 total
```

for rk-bk pair:  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/rk-bk/1$ ls
dev.bk  dev.rk  test.bk  test.rk  train.bk  train.rk
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/rk-bk/1$ cp * ../../4wfst/rk-bk/1/
```

4wfst/rk-bk/1/ path အောက်ကို ရွှေ့ပြီးတော့ ...  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/4wfst/rk-bk/1$ ls
dev.bk  dev.rk  test.bk  test.rk  train.bk  train.rk
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/4wfst/rk-bk/1$ cat train.bk dev.bk > ../train.bk
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/4wfst/rk-bk/1$ cat train.rk dev.rk > ../train.rk
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/4wfst/rk-bk/1$ cp test.* ../(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/4wfst/rk-bk/1$ cd ..
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/4wfst/rk-bk$ wc *
wc: 1: Is a directory
      0       0       0 1
   1072    6956  103337 test.bk
   1072    6739  110724 test.rk
   9650   63491  944655 train.bk
   9650   62246 1013314 train.rk
  21444  139432 2172030 total
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/4wfst/rk-bk$
```

## Alignment

Alignment လုပ်ပြီးတော့ phrase-level dictionary ကို ဆောက်ခဲ့ ...  

ပထမဆုံး အထက်မှာ ပြင်ဆင်ခဲ့တဲ့ ဒေတာတွေကို alignment လုပ်မယ့် folder အောက်ကို ကော်ပီကူးပြီးတော့ အောက်ပါအတိုင်း သိမ်းယူထားခဲ့ ...  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/alignment$ tree
.
├── dw-bk
│   ├── test.bk
│   ├── test.dw
│   ├── train.bk
│   └── train.dw
└── rk-bk
    ├── test.bk
    ├── test.rk
    ├── train.bk
    └── train.rk

2 directories, 8 files
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/alignment$
```

alignment လုပ်ဖို့အတွက် လိုအပ်တဲ့ script ကို ကော်ပီကူးယူခဲ့ ...  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/word/alignment/my-bk$ cp anymalign.sh /media/ye/project1/exp/wfst-mt/exp/wfst-cadt/alignment/dw-bk/
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/word/alignment/my-bk$ cp anymalign.sh /media/ye/project1/exp/wfst-mt/exp/wfst-cadt/alignment/rk-bk/
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/word/alignment/my-bk$
```

alignment လုပ်တဲ့ script က အောက်ပါအတိုင်း ...  

```bash
#!/bin/bash -v

# How to run:
# e.g. ./anymalign.sh my bk
SOURCE=$1;
TARGET=$2;

time python2.7 /home/ye/tool/anymalign2.5/anymalign.py ./train.$SOURCE ./train.$TARGET > alignment-train.txt
wc ./alignment-train.txt

head ./alignment-train.txt
tail ./alignment-train.txt

cut -f1 ./alignment-train.txt > train-equal-smt.$SOURCE
cut -f2 ./alignment-train.txt > train-equal-smt.$TARGET

head ./train-equal-smt.$SOURCE
head ./train-equal-smt.$TARGET

tail ./train-equal-smt.$SOURCE
tail ./train-equal-smt.$TARGET

wc ./train-equal-smt.$SOURCE
wc ./train-equal-smt.$TARGET

echo "Alignment path:"
pwd;
```

alignment for dw-bk language pair:  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/alignment/dw-bk$ time ./anymalign.sh bk dw
#!/bin/bash -v

# How to run:
# e.g. ./anymalign.sh my bk
SOURCE=$1;
TARGET=$2;

time python2.7 /home/ye/tool/anymalign2.5/anymalign.py ./train.$SOURCE ./train.$TARGET > alignment-train.txt
Input corpus: 2 languages, 5952 lines
Aligning... (ctrl-c to interrupt)
(4568242 subcorpora, avg=11.95) Alignment interrupted! Proceeding...
183055 alignments
Sorting alignments
Computing conditional probabilities...
Outputting results...
100%
real	26m17.825s
user	26m8.015s
sys	0m2.703s
wc ./alignment-train.txt
  183055  1806362 22186254 ./alignment-train.txt

head ./alignment-train.txt
။	။	-	0.980111 0.983410	41655021
။	ဟှယ် ။	-	0.009424 0.717105	400534
နင်	နန်	-	0.918959 0.859376	367305
ဘဇာလောက်	ဟှယ်လော့	-	0.970911 0.979262	264382
သူ	သူ	-	0.921849 0.863447	215437
ရယ် ။	။	-	0.640275 0.003865	163712
ပြော	ပြော	-	0.916247 0.912796	112691
သိ	သိ	-	0.913766 0.950137	102764
ငါ	ငါ	-	0.526656 0.908933	94609
ရေချိုးခန်း လဲ ပါ ရယ်	ရေချိုးခန်း လည်း ရှိဟှယ်	-	0.993098 0.604144	90647
tail ./alignment-train.txt
ကို တောင်းပန် ရမယ်လား	တွန်းပန် ရဝို့လား	-	0.200000 0.001534	1
နှစ် အုပ်ယူ မယ်	အယ် စာအောက် နှေ့အောက်	-	0.015385 0.014085	1
တစ်ယောက် စီ မှာ ဘယ်လောက်စီ	တစ် ယွတ် စီ မှာ ဟှာမျှလွတ် စီ ရှိ	-	0.125000 0.055556	1
ရှိ လဲ ။	သိဟှ ။	-	0.017544 0.002538	1
ခင်ဗား သူဒို့ကို ထပ် ကြိုးစား ဖို့ အားပေး ခဲ့လား	သူးနို့ဂို ထပ်ကြိုးစားဟှို့	-	0.000118 0.004016	1
ထိုင်ခုံ ပေါ်မှာ ထိုင် နေရယ် ။	ထိုင်ခေါင်ထပ်မာ ထိုင် နေဟှယ်	-	0.001709 0.000682	1
နင့် ကို တကယ် မုန်းတိန်း	နန့်ဟှို တကယ် မူးပစ်	-	0.009346 0.004902	1
လား ။	လိုက်ဟှိလား ။	-	0.000022 0.002725	1
နင် ဘာ ကြား ခဲ့ရယ်	နန် ဟှယ်စာ ကြား နူး ။	-	0.000146 0.000838	1
ဒယ်စာဝို လို ချင်လား	သူ အဲ့မာ ဟှို လိုရှင် နေလား ။	-	0.002618 0.000838	1

cut -f1 ./alignment-train.txt > train-equal-smt.$SOURCE
cut -f2 ./alignment-train.txt > train-equal-smt.$TARGET

head ./train-equal-smt.$SOURCE
။
။
နင်
ဘဇာလောက်
သူ
ရယ် ။
ပြော
သိ
ငါ
ရေချိုးခန်း လဲ ပါ ရယ်
head ./train-equal-smt.$TARGET
။
ဟှယ် ။
နန်
ဟှယ်လော့
သူ
။
ပြော
သိ
ငါ
ရေချိုးခန်း လည်း ရှိဟှယ်

tail ./train-equal-smt.$SOURCE
ကို တောင်းပန် ရမယ်လား
နှစ် အုပ်ယူ မယ်
တစ်ယောက် စီ မှာ ဘယ်လောက်စီ
ရှိ လဲ ။
ခင်ဗား သူဒို့ကို ထပ် ကြိုးစား ဖို့ အားပေး ခဲ့လား
ထိုင်ခုံ ပေါ်မှာ ထိုင် နေရယ် ။
နင့် ကို တကယ် မုန်းတိန်း
လား ။
နင် ဘာ ကြား ခဲ့ရယ်
ဒယ်စာဝို လို ချင်လား
tail ./train-equal-smt.$TARGET
တွန်းပန် ရဝို့လား
အယ် စာအောက် နှေ့အောက်
တစ် ယွတ် စီ မှာ ဟှာမျှလွတ် စီ ရှိ
သိဟှ ။
သူးနို့ဂို ထပ်ကြိုးစားဟှို့
ထိုင်ခေါင်ထပ်မာ ထိုင် နေဟှယ်
နန့်ဟှို တကယ် မူးပစ်
လိုက်ဟှိလား ။
နန် ဟှယ်စာ ကြား နူး ။
သူ အဲ့မာ ဟှို လိုရှင် နေလား ။

wc ./train-equal-smt.$SOURCE
 183055  530101 8438087 ./train-equal-smt.bk
wc ./train-equal-smt.$TARGET
 183055  544041 9576735 ./train-equal-smt.dw

echo "Alignment path:"
Alignment path:
pwd;
/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/alignment/dw-bk



real	26m18.920s
user	26m8.878s
sys	0m2.792s
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/alignment/dw-bk$
```

for bk-rk pair:  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/alignment/rk-bk$ time ./anymalign.sh bk rk
#!/bin/bash -v

# How to run:
# e.g. ./anymalign.sh my bk
SOURCE=$1;
TARGET=$2;

time python2.7 /home/ye/tool/anymalign2.5/anymalign.py ./train.$SOURCE ./train.$TARGET > alignment-train.txt
Input corpus: 2 languages, 9650 lines
Aligning... (ctrl-c to interrupt)
(5246089 subcorpora, avg=12.77) Alignment interrupted! Proceeding...
294352 alignments
Sorting alignments
Computing conditional probabilities...
Outputting results...
100%
real	24m28.958s
user	24m23.843s
sys	0m3.509s
wc ./alignment-train.txt
  294352  2980716 36743568 ./alignment-train.txt

head ./alignment-train.txt
။	။	-	0.904938 0.965847	14476373
မ	မ	-	0.909321 0.934329	829697
သူ	သူ	-	0.905877 0.898486	320108
သိ	သိ	-	0.963547 0.952186	250027
နင်	မင်း	-	0.902978 0.447674	242305
ကို	ကို	-	0.732186 0.450506	207055
။	မင်း	-	0.011477 0.339220	183604
ရယ် ။	။	-	0.586329 0.010789	161703
ကူညီ	ကူညီ	-	0.972580 0.955970	138369
အတွက်	အတွက်	-	0.977607 0.910176	138264
tail ./alignment-train.txt
။	သား ဟိ ပါလား ။	-	0.000000 0.001876	1
သူက ဆရာဝန် ဆီ	သူက ဆရာဝန် ဘက်လားရစွာ	-	0.500000 0.020000	1
သောရဇာ ကြိုက် ပဲ့လား ။	ကြိုက် ပါ လား ။	-	1.000000 0.032258	1
တို့ ငါ့	သူ ရို့ ငါ့	-	0.045455 0.125000	1
သော ဝို့ ရည်ရွယ်	ဖို့ ရည်ရွယ်	-	0.333333 0.006849	1
ကျဒေါ် ကျောင်း မှာ	ကျောင်း မာ	-	0.500000 0.020408	1
နှစ် ရှိ	နှစ် ဟိ ဗျာယ်	-	0.010204 0.500000	1
ဟိတ် နင် ဘာ တင်ပြ အုန်း ။	မင်း တစ်ခုခု တင်ပြဖို့ ဟိ လား	-	0.001183 0.000696	1
ဒယ်မာ ဖယ်သူတွေ ရှိ ခဲ့တယ်	ဇာသူရို့ ဟိ ဂတ်လေး ။	-	0.000360 0.041667	1
နင် သူလို့ဝို တွေ့ ခဲ့ရယ်လား	သူရို့ ကို တွိ	-	0.000668 0.076923	1

cut -f1 ./alignment-train.txt > train-equal-smt.$SOURCE
cut -f2 ./alignment-train.txt > train-equal-smt.$TARGET

head ./train-equal-smt.$SOURCE
။
မ
သူ
သိ
နင်
ကို
။
ရယ် ။
ကူညီ
အတွက်
head ./train-equal-smt.$TARGET
။
မ
သူ
သိ
မင်း
ကို
မင်း
။
ကူညီ
အတွက်

tail ./train-equal-smt.$SOURCE
။
သူက ဆရာဝန် ဆီ
သောရဇာ ကြိုက် ပဲ့လား ။
တို့ ငါ့
သော ဝို့ ရည်ရွယ်
ကျဒေါ် ကျောင်း မှာ
နှစ် ရှိ
ဟိတ် နင် ဘာ တင်ပြ အုန်း ။
ဒယ်မာ ဖယ်သူတွေ ရှိ ခဲ့တယ်
နင် သူလို့ဝို တွေ့ ခဲ့ရယ်လား
tail ./train-equal-smt.$TARGET
သား ဟိ ပါလား ။
သူက ဆရာဝန် ဘက်လားရစွာ
ကြိုက် ပါ လား ။
သူ ရို့ ငါ့
ဖို့ ရည်ရွယ်
ကျောင်း မာ
နှစ် ဟိ ဗျာယ်
မင်း တစ်ခုခု တင်ပြဖို့ ဟိ လား
ဇာသူရို့ ဟိ ဂတ်လေး ။
သူရို့ ကို တွိ

wc ./train-equal-smt.$SOURCE
  294352   915264 14679597 ./train-equal-smt.bk
wc ./train-equal-smt.$TARGET
  294352   888044 15392718 ./train-equal-smt.rk

echo "Alignment path:"
Alignment path:
pwd;
/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/alignment/rk-bk



real	24m30.841s
user	24m25.255s
sys	0m3.627s
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/alignment/rk-bk$
```

## Preparation for Running WFST-MT

အရင်တုန်းက လုပ်ခဲ့တဲ့ WFST-MT experiment ဖိုလ်ဒါက script ကို ကော်ပီကူးယူခဲ့ ...  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/word$ cp prepare-rkmy-fast-pt.sh /media/ye/project1/exp/wfst-mt/exp/wfst-cadt/
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/word$
```

script ကို ဝင် အောက်ပါအတိုင်း update လုပ်ခဲ့...  
အရင်တုန်းက path တွေကို ဝင်ရိုက်ထည့်ခဲ့ပေမဲ့ ဒီတစ်ခါတော့ ပိုလုပ်ရကိုင်ရတာ အဆင်ပြေအောင်လို့ script ရဲ့ ထိပ်ဆုံးပိုင်းမှာ variable တွေအဖြစ် assign လုပ်ခဲ့...  

```bash
#!/bin/bash -v

# written by Ye Kyaw Thu, LST, NECTEC, Thailand
# last updated: 4 June 2020

mkdir -p ./wfst-mt/bk-dw-anymalign;
EXP_PATH="./wfst-mt/bk-dw-anymalign";
ALIGN_DATA_PATH="/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/alignment/dw-bk";
SCRIPTS_PATH="/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/ready-to-run-scripts";
SRC="bk";
TGT="dw";

# copying aligned data
cp $ALIGN_DATA_PATH/train-equal-smt.{$SRC,$TGT} $EXP_PATH;
cp $ALIGN_DATA_PATH/test.{$SRC,$TGT} $EXP_PATH;

cat $EXP_PATH/train-equal-smt.$SRC $EXP_PATH/test.$SRC > $EXP_PATH/all.$SRC;
cat $EXP_PATH/train-equal-smt.$TGT $EXP_PATH/test.$TGT > $EXP_PATH/all.$TGT;

# copying shell, perl and python scripts for running WFST based MT experiment
cp $SCRIPTS_PATH/*.{sh,pl,py} $EXP_PATH;

# confirmation
tree $EXP_PATH;

```

Running above script ...  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt$ ./prepare-bkdw-anymalign.sh 
#!/bin/bash -v

# written by Ye Kyaw Thu, LST, NECTEC, Thailand
# last updated: 4 June 2020

mkdir -p ./wfst-mt/bk-dw-anymalign;
EXP_PATH="./wfst-mt/bk-dw-anymalign";
ALIGN_DATA_PATH="/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/alignment/dw-bk";
SCRIPTS_PATH="/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/ready-to-run-scripts";
SRC="bk";
TGT="dw";

# copying aligned data
cp $ALIGN_DATA_PATH/train-equal-smt.{$SRC,$TGT} $EXP_PATH;
cp $ALIGN_DATA_PATH/test.{$SRC,$TGT} $EXP_PATH;

cat $EXP_PATH/train-equal-smt.$SRC $EXP_PATH/test.$SRC > $EXP_PATH/all.$SRC;
cat $EXP_PATH/train-equal-smt.$TGT $EXP_PATH/test.$TGT > $EXP_PATH/all.$TGT;

# copying shell, perl and python scripts for running WFST based MT experiment
cp $SCRIPTS_PATH/*.{sh,pl,py} $EXP_PATH;

# confirmation
tree $EXP_PATH;
./wfst-mt/bk-dw-anymalign
├── all.bk
├── all.dw
├── bigram.py
├── eval.sh
├── mk-fst-format.pl
├── mk-symbol.pl
├── mk-train-symbol.sh
├── mk-uniq-word.sh
├── multi-test.sh
├── onetoone.py
├── shortest-path-to-line.sh
├── symbols.py
├── test.bk
├── test.dw
├── test-nofstdraw.sh
├── test.sh
├── train-equal-smt.bk
├── train-equal-smt.dw
├── train-test-eval.sh
├── translate-nofstdraw.sh
└── translate.sh

0 directories, 21 files


(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt$
```

## Building WFST for bk-dw Translation

အရင်ဆုံး folder change ပြီး script တွေကို စစ်ကြည့်ခဲ့ ...  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt$ cd wfst-mt/bk-dw-anymalign/
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/wfst-mt/bk-dw-anymalign$ ls
all.bk            mk-symbol.pl        shortest-path-to-line.sh  test.sh                 translate.sh
all.dw            mk-train-symbol.sh  symbols.py                train-equal-smt.bk
bigram.py         mk-uniq-word.sh     test.bk                   train-equal-smt.dw
eval.sh           multi-test.sh       test.dw                   train-test-eval.sh
mk-fst-format.pl  onetoone.py         test-nofstdraw.sh         translate-nofstdraw.sh
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/wfst-mt/bk-dw-anymalign$
```

train-test-eval.sh က အောက်ပါအတိုင်းပါ...  

```bash
#!/bin/bash

# Written by Ye, LST, NECTEC, Thailand

# Prepare oneline test data
# head က ပုဒ်မ တစ်ခုတည်းဖြစ်နေလို့ tail ကို သုံးဖို့ ဆုံးဖြတ်လိုက်တယ်
tail -n 1 ./train-equal-smt.my > oneline.my

# Building Transducers with training data (i.e. language model, translation model, composing etc.)
time ./translate-nofstdraw.sh ./train-equal-smt.my ./train-equal-smt.rk oneline.my ./all.my ./all.rk ./all.rk

# Testing with WFST MT
time ./multi-test.sh ./all.my ./all.rk ./test.my 2>&1 | tee anymaTrainingDataOnly-test-myrk.log1

# Evaluation
time ./eval.sh ./test.rk hyp.txt.clean

```

အထက်ပါ script ကို အောက်ပါအတိုင်း update လုပ်ခဲ့...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, 
# Affiliate Professor, IDRI, CADT, Cambodia
# Last Updated: 4 June 2022

SRC="bk";
TGT="dw";

# Prepare oneline test data
# head က ပုဒ်မ တစ်ခုတည်းဖြစ်နေလို့ tail ကို သုံးဖို့ ဆုံးဖြတ်လိုက်တယ်
tail -n 1 ./train-equal-smt.$SRC > oneline.$SRC

# Building Transducers with training data (i.e. language model, translation model, composing etc.)
time ./translate-nofstdraw.sh ./train-equal-smt.$SRC ./train-equal-smt.$TGT oneline.$SRC ./all.$SRC ./all.$TGT ./all.$TGT

# Testing with WFST MT
time ./multi-test.sh ./all.$SRC ./all.$TGT ./test.$SRC 2>&1 | tee anymaTrainingDataOnly-test-$SRC-$TGT.log1

# Evaluation
time ./eval.sh ./test.$TGT hyp.txt.clean

```

WFST-MT transducer ကို အောက်ပါအတိုင်း ဆောက်ခဲ့ ...  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/wfst-mt/bk-dw-anymalign$ time ./train-test-eval.sh 2>&1 | tee train-test-eval-word-bkdw.log1  
```

a part of running log is as follows:  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/wfst-mt/bk-dw-anymalign$ time ./train-test-eval.sh 2>&1 | tee train-test-eval-word-bkdw.log1
...
...
...
Translation: သူ ကံကောင်းတယ် သူ့ဇာသူ မနည်း ခိုက်မိ မယ် ။
Translation: ဆရာဝန် က ဒါ ဆေး အား ရှာ ခက်ရရ်ဆို ပြော ဝရ်ပဲ ။
Translation: ဒယ်ဇာ ကို သိမ်း ထားရယ်လား ။
Translation: ဘဇာလောက် ပျော်စရာကောင်း ရိ ။
Translation: ဦး ကျော် ဇော က သူ့ရဲ့ ရုံးခန်း ထဲမှာ ရှိ နိုင်ရယ် ။
Translation: နင် ဘာ လျော် နေရယ် ။
Translation: သူ ဒယ်ဇာကို ရှင်းပြ ရရိ ဝမ်းသာ နေဇာ ။
Translation: ငါဝို့ နင့်ဝို ကျေးဇူးတင်ရယ် ။
Translation: နင် လက်ထပ် ဖို့ မ ရည်ရွယ် ခဲ့ရလား ။
Translation: နောက် တစ်ချိန်ဆို မင့် ဝို တွေ့ ရဝို့လား ။
Translation: နောက် တစ်ချိန်ဆို မင့် ဝို တွေ့ ရဝို့လား ။
Translation: ကျွန်တော် မင့်ဝို တွေ့ ရဇာ ပျော် ရယ် ။
Translation: မင်း ဘဝ မှာ တစ်ယောက်ယောက်ကို လေးလေးနက်နက် ချစ်ဖူး ရယ်လား ။
Translation: သစ်သား တအား မ မာ က ။
Translation: ဒယ်လို စကားတွေ တအားများ ရှိ ရယ် ။
Translation: ဒယ်လို စကားတွေ တအားများ ရှိ ရယ် ။
Translation: သူတို့ ငါ့ ကို ဂရုစိုက် နေသော်လည်း ငါ ဂရုမစိုက် ဘူး ။
Translation: ဒယ်ကောင်မ သီချင်း ဆိုဝယ် ၊ မ ဆို ဝ လား ။
Translation: မင်း ဖယ်သူ့ ဝို မေး ဝို့လဲ ။
Translation: ဒယ် ညမျိုး အကြွေ မ ရှိ ရိ ။
Translation: ဒယ် ညမျိုး အကြွေ မ ရှိ ရိ ။
Translation: သူ သူ့ ကို မ ယုံ ကလား ။
Translation: ကျွန်တော် တရားနာ ဝို့ စိတ်ရှည် ရမယ် ။
Translation: နင် ဘယ်သူ့ ဝို စော်ကား နေဝ ။
Translation: ဘာ အထိမ်းအမှတ် ဝို ။
Translation: ဘာ အထိမ်းအမှတ် ဝို ။
Translation: ဒယ်ကောင်မငယ် ဆေးလိပ် ဖြတ် ခဲ့ရယ် ။
Translation: ငါ စင် ထက်မှာ က ခဲ့ပါဟယ် ။
Translation: ငါ နင့် နေရာ မှ ဆို ဒယ်အတိုင်း ပဲ လုပ် မယ် ။
Translation: ငါ နင့် နေရာ မှ ဆို ဒယ်အတိုင်း ပဲ လုပ် မယ် ။
Translation: အဲဒါ ကနေ မင့် ကြိုက် တဲ့ဟာ ရ နိုင်ရယ် ။
Translation: ငါ့ နှိုးစက် နာရီ ။
Translation: ငါ့ နှိုးစက် နာရီ ။
Translation: နင် ဖယ်သူ ဒေ ဝို မေး ဟားရစ်တယ် ။
Translation: ကျွန်တော်လို့ ပျော်ပျော်ရွှင်ရွှင် က ကြရမယ် မ ဟုတ် လား ။
Translation: ငါ ကျီးပြား နဲ့ ချေ ပါမယ် ။
FATAL: FstCompiler: Symbol "ပါမယ်" is not mapped to any integer arc ilabel, symbol table = onetoone.all.isym, source = ./oneline-test.formatted, line = 5
Translation: ငါ ကျီးပြား နဲ့ ချေ ပါမယ် ။
FATAL: FstCompiler: Symbol "ပါမယ်" is not mapped to any integer arc ilabel, symbol table = onetoone.all.isym, source = ./oneline-test.formatted, line = 5
Translation: ဘဇာလောက် နောက်ကျ ရိ ။
Translation: သူ ဟိုကို သောတာ ငါ မြင် ရယ် ။
Translation: သူ ဟိုကို သောတာ ငါ မြင် ရယ် ။
Translation: ပေးဖို့ ဘာမှ မ ရှိ က ။
Translation: နင် က ဘာတွေ ရှင်းပြ ခဲ့ရယ် ။
Translation: လမ်း ပေါ်မှာ ယောက်ျားငယ် တစ်အုပ် ရှိ ရယ် ။
Translation: သူ့စာသူ ဘယ်သူ့ကို ဆဲဆဲ ပြန် မ ပြော နဲ့ ။
Translation: နင်တို့ ဘယ်မှာ လက်ထပ် ထားရယ် ။
Translation: ငါ နင့်ဝို ချစ် ရယ်ရ် ။
Translation: ခင်ဗျား အောင်မြင် ချင်ရင် အလုပ် ဝို ကြိုးစား ဟို့ လို ဝယ် ။
Translation: ခင်ဗျား ဒယ်ဇာ ကို သိ လား ။
Translation: ငါ နင့် ကို နမ်း ရဝို့လား ။
Translation: ငါ ကူညီ မယ်လန်း ။
Translation: ငါ ကူညီ မယ်လန်း ။
Translation: နင် မ လာ ကလား ။
Translation: သားကင်းငယ် ကို သေချာ ချီ လန်း ။
Translation: သူဝို့ ကို ခွင့်ပြု လိုက်လား ။
Translation: သူ အမြဲ ညည်း နေရယ် ။
Translation: ဟုတ်ဝ ၊ သူ လုပ် မယ် မ ထင် ရ ။
Translation: သူလို့ အနားယူ ကြရယ်လား ။
Translation: နင်ကိုယ်တိုင် မီး ပိတ် ပီးလား ။
Translation: ငါလို့ အလုပ် လျှောက် ခဲ့ကြဟယ် ။
Translation: နင့်ရဲ့ ဆရာ က ဘယ်သူဘောဝမ့် ။
Translation: နင့်ရဲ့ ဆရာ က ဘယ်သူဘောဝမ့် ။
Translation: ငါလို့ ကြို ပြီး မ ခန့်မှန်း ထားလား ။
Translation: မင် သွားသွား ငါ့ကို သတိရ ။
Translation: သူ ဖယ်မှာ ။
Translation: သူ ရေဒီယို နားထောင် ဟုတ် ဝ ။
Translation: သူတို့ ငါ့ကို ဘင်းမျိုး စစ်ဆေး လဲ ။
Translation: ဘဘ က ခြံအလုပ် အား လုပ် ရရ် ။
Translation: ခင်ဗျား ကျွန်တော်ဝို့ ကို လာ ခိုင်းဇာ ။
Translation: မနေ့ က သူ ပြန်လာ သေးရရ်လား ။
Translation: နင် ဘယ်မှာ ပြော ဝို့ ။
Translation: လေ့ကျင့်ပေး ထားတဲ့ သူတွေ က ပို ကျွမ်း တယ် ။
Translation: မင်း စကား ပြော နေရိလား ။
Translation: နင် ဒယ် အကြောင်း စုံစမ်း မယ်လား ။
Translation: နင် မေး ချင်စာ မေး အဆင်သင့်ပဲ ။
Translation: သူတို့ကိုယ်သူတို့ သိ ရယ် ။
Translation: သူ ညဘက် အလုပ် လုပ် ရတာကို ပို သဘောကျရယ် ။
Translation: သူ ညဘက် အလုပ် လုပ် ရတာကို ပို သဘောကျရယ် ။
Translation: မင်း ငါ တင်းနစ်ခ် ပွဲ ကစား ဝို့လား ။
Translation: နင် ဘာဇာတွေ ညီး နေရယ်ဆိုတာ ငါတော့ နားမလည် နိုင်ပီ ။
Translation: နင် ဘာဇာတွေ ညီး နေရယ်ဆိုတာ ငါတော့ နားမလည် နိုင်ပီ ။
Translation: ဒါဆို ဒါ ကျောင်း ကို သွား ပြီး သာဆို ဘာသရယ် ဘယ်ဟာ ပေးထား ဆိုပီး မေး ။
Translation: ဒါဆို ဒါ ကျောင်း ကို သွား ပြီး သာဆို ဘာသရယ် ဘယ်ဟာ ပေးထား ဆိုပီး မေး ။
Translation: ကျနော် လမ်း မှာ လမ်းလျှောက် ရင်း ခြေထောက် နာ သွား တယ် ။
Translation: နင် ဖယ်သူ့ ဝို ကူညီ သင့်ရယ် ။
Translation: ကျွန်တော် နိုင်ငံခြား သော ရယ် ။
Translation: သူ နှင်းကျ ဆို အမြဲ ခမောက် ဆောင်း ဝယ် ။
Translation: ဒယ် စာအုပ် သူ့ ဝိုဝ် ပေး ရပ် ။
Translation: သူ ဒယ့်ဇာ ကို အသံထွက် ပြရိမယ် ။
Translation: သူ နှုတ်ဆက်စကား ပြော ရယ် ။
Translation: နင် ဖယ်သူ နဲ့ ဆွေးနွေး သင့်ရယ် ။
Translation: ဒယ်ကောင်မငယ် ကိုယ် နဲ့ အိပ် ဖို့ ရှက် နေရယ် ။
Translation: နင်က ဘာ ရှင်းပြ လိုက်ရယ် ။
Translation: စကားပြော သင်တန်း တက် ဝို့ နင် သူ့ ကို တွန်းအား မ ပေး ဟလား ။
Translation: ဒယ်ကောင်မငယ် မင်းဝို ချိန်း ရိလား ။
Translation: ကျွန်တော် ပြော ဇာဝို သူတို့ နာခံ ကြပါဟယ် ။
Translation: မင်း အဲ့ဇာ မ နိုင် ဘဲ့လား ။
Translation: စာအုပ် အနီ ရ စားပွဲ ပေါ် မှာ ။
Translation: နင် ငါ့ဝို ဘယ်မှာ စောင့် နေရယ် ။
Translation: ကျနော့် ခမောက် လိုမျိုး သူ ဆောင်းထား ဝယ် ။
Translation: စားဝို့ တခုခု သွား ဝယ်လန်း ။
Translation: နင် ညနေ ဆို ဘာတွေ လုပ် နေရရ် ။
Translation: အား မှောင် ရိ ငါတို့ ဘားလည်း မ မြင် ရပီ ။
FATAL: FstCompiler: Symbol "ရပီ" is not mapped to any integer arc ilabel, symbol table = onetoone.all.isym, source = ./oneline-test.formatted, line = 8
Translation: သူ့ ကို ဘာ က ဒဏ်ရာရ စေတာလဲ ။
Translation: ငါ ဒယ်ဇာ အတွက် မေး တိန်းလား ။
Translation: သားငယ် လေ ရရ် ဟုံး မှာ ။
Translation: သူတို့ ဖယ်သူ့မှ သံသယ မ ဝင် ရလား ။
Translation: ဖယ်သူတွေ အိပ် နေကြရယ် ။
Translation: မင် စကား ပြော နေစာ ။
Translation: သူ ဒယ်စာဝို ဆုံးဖြတ် ခဲ့ဟယ် ။
Translation: ငါ့ အနား မှာ နေ ရဇာ ပျော် လား ။
Translation: ငါ့ ဝို ယုံတဲ့ လူဒေ ဝို ဘယ်တော့မှ သစ္စာ မ ဖောက် ရ ။
FATAL: FstCompiler: Symbol "ဖောက်" is not mapped to any integer arc ilabel, symbol table = onetoone.all.isym, source = ./oneline-test.formatted, line = 9
Translation: မင့် ဘာအကြောင်းကြောင့် ဟင်းမချက် ။
Translation: ခင်ဗျား ဒယ်စာ ဝို စဉ်းစား ကြည့် ရိုက် ။
Translation: တံခါး ဖွင့် ရင် စိတ်ဆိုး ဝို့လား ။
Translation: ဟုတ် ရရယ်လန်း ။
Translation: မင်း ဘာ လုပ် ထားရယ် ။
Translation: ကျွန်တော်လို့ ဒယ့်ဇာ ကို ကာကွယ် မယ်လား ။
Translation: နင် ဘယ်ဇာ တွေ လုပ် နေသေးရရ် ။
Translation: နင် ဘယ်ဇာ တွေ လုပ် နေသေးရရ် ။
Translation: ခင်ဗျား လို ရင် ရေ ကြိုက် သလောက် ရ နိုင်ရယ် ။
Translation: ကျွန်တော်ဝို့ အဲ့ဒါဝို အတည်မပြု ခဲ့ရလေ ။
Translation: ငါရဲ့ ရည်းစားဟောင်း ကို ဆက်သွယ် ဖို့ မျှော်လင့် တယ် ။
Translation: နင် ဒုက္ခ မ ရောက် ဝ ။
Translation: ငါ ပြော ပြမယ် စနေနေ့ ကျရင်လန်း ငါတို့ ကိုယ်တိုင် ကစား မယ် ။
Translation: ငါ ပြော ပြမယ် စနေနေ့ ကျရင်လန်း ငါတို့ ကိုယ်တိုင် ကစား မယ် ။
Translation: အယ့်ဒါ ဘယ်သူ့ လှောင်အိမ် ရိ ။
Translation: နင် သူ့ဝို မုန်း နေဇာ မ ဟုတ် ဝလား ။
Translation: နင့် ကြီးကြီး တို့ က ဖယ်သူတွေ ။
Translation: ဖယ်သူလေ ကို မေး ရိလဲ ။
Translation: သူ ဒယ့်ဟာ ကို လိုချင် မ ဟုတ် ဝ ။
Translation: ဘဇာလောက် စိတ်လှုပ်ရှား ရိ ။
Translation: မင်း ငါ့ ကို ရှင်းပြ နိုင်မလား ။
Translation: အဲဒီ ကို သော ဖို့ ငါ မင်းကို ငါ မ တိုက်တွန်း ရ ။
Translation: နင် ခရီး မ ထွက် ခဲ့ရလား ။
Translation: သူတို့ ဘဇာလောက် သတ္တိရှိ လဲ ။
Translation: ဒါ ထဲမှာ အဝေးပြော ဖုန်းပြော တအား များရယ် ။
Translation: ဒါ ထဲမှာ အဝေးပြော ဖုန်းပြော တအား များရယ် ။
Translation: အဲ့အမ ကို လက်ထပ် လိုက်ရယ်လား ။
hypothesis file: hyp.txt.clean

real	26m22.358s
user	23m34.314s
sys	1m50.068s
Evaluation with BLEU score:
BLEU = 9.77, 36.2/11.9/6.3/3.3 (BP=1.000, ratio=1.057, hyp_len=4243, ref_len=4013)
Evaluation with chrF++ score:
start_time:	1654328310
c6+w2-F2	35.2383
c6+w2-avgF2	35.6171
end_time:	1654328311

real	0m0.389s
user	0m0.354s
sys	0m0.020s

real	27m55.179s
user	23m43.782s
sys	1m51.003s
```

## Build WFST for dw-bk Translation

အရင်ဆုံး bk-dw အတွက် run ထားခဲ့တဲ့ ဖိုလ်ဒါတစ်ခုလုံးကို နာမည်ပြောင်းပြီး copy ကူးယူ ...   

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/wfst-mt$ cp -r bk-dw-anymalign/ ./dw-bk-anymalign
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/wfst-mt$ cd dw-bk-anymalign/
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/wfst-mt/dw-bk-anymalign$
```

update the shell script ...  

```
#!/bin/bash

# Written by Ye Kyaw Thu, 
# Affiliate Professor, IDRI, CADT, Cambodia
# Last Updated: 4 June 2022

SRC="dw";
TGT="bk";

# Prepare oneline test data
# head က ပုဒ်မ တစ်ခုတည်းဖြစ်နေလို့ tail ကို သုံးဖို့ ဆုံးဖြတ်လိုက်တယ်
tail -n 1 ./train-equal-smt.$SRC > oneline.$SRC

# Building Transducers with training data (i.e. language model, translation model, composing etc.)
time ./translate-nofstdraw.sh ./train-equal-smt.$SRC ./train-equal-smt.$TGT oneline.$SRC ./all.$SRC ./all.$TGT ./all.$TGT

# Testing with WFST MT
time ./multi-test.sh ./all.$SRC ./all.$TGT ./test.$SRC 2>&1 | tee anymaTrainingDataOnly-test-$SRC-$TGT.log1

# Evaluation
time ./eval.sh ./test.$TGT hyp.txt.clean

```

Train/Test/Eval running ...  

```
time ./train-test-eval.sh 2>&1 | tee train-test-eval-word-dwbk.log1
```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```


## Reference

မြန်မာစာလုံးတွေက shortest-path graph မှာ မှန်မှန်ကန်ကန် ပေါ်စေဖို့အတွက်က အောက်ပါအတိုင်း command ပေးပါ။  

```
fstdraw --portrait --isymbols=onetoone.isym  --osymbols=$corpusf.words.sym ./shortest-path.fst | dot -Tpdf:cairo -Nfontname=Padauk -Nfontsize=15 -Efontname=Padauk -Efontsize=15 -Gsize=6,3 -Eheadport=e -Etailport=w > shortest-path.pdf
```



