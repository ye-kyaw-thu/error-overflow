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

training ဒေတာနဲ့ development ဒေတာကို ပေါင်းပြီး wfst ဆောက်ရမှာမို့ အဲဒီအတွက် ဒေတာကို ပြင်ခဲ့...  

for dw-bk pair:  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/dw-bk/1$ cp *.dw ../../4wfst/dw-bk/1/
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/dw-bk/1$ cp *.bk ../../4wfst/dw-bk/1/


```

for rk-bk pair:  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/rk-bk/1$ ls
dev.bk  dev.rk  test.bk  test.rk  train.bk  train.rk
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/rk-bk/1$ cp * ../../4wfst/rk-bk/1/
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/rk-bk/1$ cat train.bk dev.bk > ../train.bk
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/rk-bk/1$ cat train.rk dev.rk > ../train.rk
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/rk-bk/1$ cp test.bk ../
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/rk-bk/1$ cp test.rk ../
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/rk-bk/1$ cd ..
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/rk-bk$ wc *.bk
   1072    6956  103337 test.bk
   9650   63491  944655 train.bk
  10722   70447 1047992 total
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/rk-bk$ wc *.rk
   1072    6739  110724 test.rk
   9650   62246 1013314 train.rk
  10722   68985 1124038 total
```

4wfst အောက်ကို ရွှေ့...  

```
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/rk-bk$ mv *.bk ../4wfst/rk-bk/
(base) ye@ykt-pro:/media/ye/project1/exp/wfst-mt/exp/wfst-cadt/data/word/rk-bk$ mv *.rk ../4wfst/rk-bk/
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

```

```

```

```



