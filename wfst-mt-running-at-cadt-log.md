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

```

```

```

```

```

```

```



