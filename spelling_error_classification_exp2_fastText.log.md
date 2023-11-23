# Exp-2 for the Spelling Error Type Classification with fastText

တကယ်က ငါတို့ ဒေတာထဲမှာ multiple label တွေ ရှိနေတာကြောင့် အဲဒါကို fastText နဲ့ classification လုပ်မယ် ဆိုရင် option ပြောင်းပြီး လုပ်တာမျိုး လုပ်လို့ ရတယ်။  

```
__label__pho __label__typo ပုန်း တေ ရှိ
__label__pho __label__typo ရွာ တေ က
__label__pho __label__typo ယ နစ် တက်
__label__pho __label__typo ဆင် မှု လေး
__label__pho __label__typo နေ ပီး
__label__pho __label__typo ရဲ့ ဖစ် တည်
__label__pho __label__typo တီး မှု လက်
__label__pho __label__typo ရ ပီး ပါ
__label__pho __label__typo ကုန်း ပီး အော
__label__pho __label__typo ရ မာ မ
```

Experiment 1 တုန်းကလိုမျိုး fastText ကို မော်ဒယ် ဆောက်ခဲ့ရင်တော့ online testing လုပ်ကြည့်ရင် အောက်ပါလိုမျိုး single label ကိုပဲ predict လုပ်ပေးနိုင်လိမ့်မယ်။  

Online Testing Result:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ fasttext predict model.error_type.bin -
ပုန်း တေ ရှိ
__label__typo
ရွာ တေ က
__label__pho
ယ နစ် တက်
__label__pho
ဆင် မှု လေး
__label__typo
နေ ပီး
__label__typo
ဲ့ ဖစ် တည်
__label__typo
တီး မှု လက်
__label__typo
ရ ပီး ပါ
__label__typo
ကုန်း ပီး အော
__label__typo
ရ မာ မ
__label__typo
```

option ကို multiple label ထုတ်ပေးနိုင်အောင် ကစားလည်း မရဘူး ဆိုတာကို confirm လုပ်ခဲ့ ...  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ fasttext predict model.error_type_ep20.bin
- -1 0.5
ပုန်း တေ ရှိ
__label__typo
ရွာ တေ က
__label__pho
ယ နစ် တက်
__label__pho
ဆင် မှု လေး
__label__typo
နေ ပီး
__label__typo
ဲ့ ဖစ် တည်
__label__typo
တီး မှု လက်
__label__typo
ရ ပီး ပါ
__label__typo
ကုန်း ပီး အော
__label__typo
ရ မာ မ
__label__typo
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

## Print Labels with P and R

label တစ်ခုချင်း အလိုက် F1, P, R ထုတ်ကြည့်တဲ့အခါမှာလည်း အောက်ပါလိုမျိုး result ရတယ်။  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ fasttext test-label model.error_type_ep20.bin error_type.valid
F1-Score : 0.818670  Precision : 0.840191  Recall : 0.798223   __label__pho
F1-Score : 0.786107  Precision : 0.833995  Recall : 0.743420   __label__typo
F1-Score : 0.917271  Precision : 0.911977  Recall : 0.922628   __label__con
F1-Score : 0.881356  Precision : 0.912281  Recall : 0.852459   __label__seq
F1-Score : 0.764858  Precision : 0.783069  Recall : 0.747475   __label__slang
F1-Score : 0.771845  Precision : 0.811224  Recall : 0.736111   __label__stack
F1-Score : 0.817814  Precision : 0.893805  Recall : 0.753731   __label__sensitive
F1-Score : 0.771242  Precision : 0.786667  Recall : 0.756410   __label__short
F1-Score : 0.609756  Precision : 0.735294  Recall : 0.520833   __label__encode
F1-Score : 0.111111  Precision : 0.142857  Recall : 0.090909   __label__dialect
F1-Score : --------  Precision : --------  Recall : --------   __label__pho___label__typo
N       10794
P@1     0.842
R@1     0.781
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

ဒီနေရာမှာ ငါတစ်ခု သတိထားမိတာက လေဘယ်နှစ်မျိုးက တစ်ခုတည်းအဖြစ် ဆက်နေတာက ငါတို့ test data ထဲမှာ ရှိနိုင်တယ် ဆိုတဲ့ အချက်။  
"__label__pho___label__typo" ကို ပြောတာ။  

## Python Code for Label Counting

label counting လုပ်ဖို့ python code ကို ပြင်ဆင်ခဲ့ ...  
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext/multi-label/check_labels$ cat ./label_counter.py  

```python
## Written by Ye Kyaw Thu, LU Lab., Myanmar
## for counting unique lables from the multi-label file
## __label__typo ကြည့် ရင် နဲ့
## __label__pho __label__typo ယောင် တေ ကြေင့်
## __label__pho __label__typo ချိ ပီး ပစ်
## last updated: 23 Nov 2023

import sys
from collections import defaultdict

def extract_labels(filename):
    label_count = defaultdict(int)

    with open(filename, 'r', encoding='utf-8') as file:
        for line in file:
            parts = line.strip().split()
            for part in parts:
                if part.startswith('__label__'):
                    label_count[part] += 1

    return label_count

def main():
    if len(sys.argv) < 2:
        print("Usage: python script.py <filename>")
        sys.exit(1)

    filename = sys.argv[1]
    label_count = extract_labels(filename)

    for label, count in label_count.items():
        print(f"{label}: {count}")

if __name__ == "__main__":
    main()
```
	
## Label Counting on the Whole Dataset

Counting လုပ်ကြည့်ခဲ့ ...  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext/multi-label/check_labels$ python ./label_counter.py ./error_type.all.shuf.txt
__label__typo: 46225
__label__seq: 4730
__label__pho: 50050
__label__stack: 2099
__label__con: 6647
__label__slang: 3898
__label__encode: 510
__label__sensitive: 1347
__label__short: 646
__label__dialect: 131
__label__pho___label__typo: 2
```

## Prepare a Shell Script for the Experiment-2

အဓိကကတော့ multiple label အတွက် -loss one-vs-all ဆိုတဲ့ argument အသစ်ထပ်ဖြည့်ပြီး မော်ဒယ်ကို training လုပ်ခဲ့တဲ့ အပိုင်းနဲ့ testing လုပ်တဲ့ command မှာလည်း multiple label ကိုပါ ထုတ်ပေးနိုင်အောင် "-1 0.5" ဆိုတဲ့ option ကို ထပ်ဖြည့်ခဲ့တာပါ။  

Reference: https://fasttext.cc/docs/en/supervised-tutorial.html#multi-label-classification  
we want as many prediction as possible (argument -1) and we want only labels with probability higher or equal to 0.5  

```bash
#!/bin/bash

## bash shell script for experiment 1 from epoch 10 to 100 with fastText model
## this is for spelling error type classification
## written by Ye Kyaw Thu, LU Lab., Myanmar
## Last updated: 23 Nov 2023

# Define the input and validation files
train_file="error_type.train"
valid_file="error_type.valid"

# Loop through epochs 10 to 100 with increments of 10
for epoch in $(seq 10 10 100)
do
    echo "Training with epoch $epoch"
    model_file="model.error_type_ep${epoch}"

    # Train the model
    echo "Command: time fasttext supervised -input $train_file -output $model_file -loss one-vs-all -epoch $epoch"
    time fasttext supervised -input $train_file -output $model_file -loss one-vs-all -epoch $epoch

    echo "Testing with epoch $epoch"

    # Test the model
    echo "Command: time fasttext test ${model_file}.bin $valid_file -1 0.5"
    time fasttext test ${model_file}.bin $valid_file -1 0.5

    echo "=========="
done
```

## Run Exp2

Run Experiment 2 ...  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext/multi-label$ ./exp2.sh | tee exp2.results.txt
Training with epoch 10
Command: time fasttext supervised -input error_type.train -output model.error_type_ep10 -loss one-vs-all -epoch 10
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:  15.9% words/sec/thread:  633153 lr:  0.084090 avg.loss:  1.287183 ETA:   0h 0m Progress:  26.2% words/sec/thread:  522295 lr:  0.073768 avg.loss:  1.167389 ETA:   0h 0m Progress:  45.8% words/sec/thread:  608680 lr:  0.054165 avg.loss:  1.059183 ETA:   0h 0m Progress:  65.7% words/sec/thread:  654047 lr:  0.034346 avg.loss:  0.991122 ETA:   0h 0m Progress:  85.4% words/sec/thread:  681111 lr:  0.014551 avg.loss:  0.941961 ETA:   0h 0m Progress: 100.0% words/sec/thread:  664335 lr: -0.000004 avg.loss:  0.915412 ETA:   0h 0m Progress: 100.0% words/sec/thread:  664232 lr:  0.000000 avg.loss:  0.915412 ETA:   0h 0m 0s

real    0m0.791s
user    0m7.041s
sys     0m0.048s
Testing with epoch 10
Command: time fasttext test model.error_type_ep10.bin error_type.valid -1 0.5
N       10794
P@-1    0.85
R@-1    0.833

real    0m0.015s
user    0m0.011s
sys     0m0.004s
==========
Training with epoch 20
Command: time fasttext supervised -input error_type.train -output model.error_type_ep20 -loss one-vs-all -epoch 20
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:  10.2% words/sec/thread:  814041 lr:  0.089761 avg.loss:  1.268355 ETA:   0h 0m Progress:  20.0% words/sec/thread:  794807 lr:  0.080029 avg.loss:  1.145122 ETA:   0h 0m Progress:  29.6% words/sec/thread:  786767 lr:  0.070364 avg.loss:  1.053518 ETA:   0h 0m Progress:  39.3% words/sec/thread:  782003 lr:  0.060737 avg.loss:  1.012869 ETA:   0h 0m Progress:  48.9% words/sec/thread:  779827 lr:  0.051067 avg.loss:  0.977136 ETA:   0h 0m Progress:  58.6% words/sec/thread:  778336 lr:  0.041398 avg.loss:  0.958776 ETA:   0h 0m Progress:  68.3% words/sec/thread:  777287 lr:  0.031730 avg.loss:  0.936103 ETA:   0h 0m Progress:  77.9% words/sec/thread:  776126 lr:  0.022098 avg.loss:  0.918071 ETA:   0h 0m Progress:  87.6% words/sec/thread:  775457 lr:  0.012440 avg.loss:  0.898876 ETA:   0h 0m Progress:  97.2% words/sec/thread:  774788 lr:  0.002799 avg.loss:  0.883124 ETA:   0h 0m Progress: 100.0% words/sec/thread:  724650 lr: -0.000001 avg.loss:  0.878839 ETA:   0h 0m Progress: 100.0% words/sec/thread:  724603 lr:  0.000000 avg.loss:  0.878839 ETA:   0h 0m 0s

real    0m1.284s
user    0m12.498s
sys     0m0.052s
Testing with epoch 20
Command: time fasttext test model.error_type_ep20.bin error_type.valid -1 0.5
N       10794
P@-1    0.847
R@-1    0.834

real    0m0.015s
user    0m0.015s
sys     0m0.000s
==========
Training with epoch 30
Command: time fasttext supervised -input error_type.train -output model.error_type_ep30 -loss one-vs-all -epoch 30
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:   6.8% words/sec/thread:  812725 lr:  0.093196 avg.loss:  1.256857 ETA:   0h 0m Progress:  13.2% words/sec/thread:  789825 lr:  0.086781 avg.loss:  1.104197 ETA:   0h 0m Progress:  19.6% words/sec/thread:  781870 lr:  0.080376 avg.loss:  1.020706 ETA:   0h 0m Progress:  26.0% words/sec/thread:  778153 lr:  0.073963 avg.loss:  0.986162 ETA:   0h 0m Progress:  32.4% words/sec/thread:  775753 lr:  0.067557 avg.loss:  0.955904 ETA:   0h 0m Progress:  38.8% words/sec/thread:  773389 lr:  0.061191 avg.loss:  0.936754 ETA:   0h 0m Progress:  45.2% words/sec/thread:  771946 lr:  0.054812 avg.loss:  0.916728 ETA:   0h 0m Progress:  51.6% words/sec/thread:  771121 lr:  0.048413 avg.loss:  0.901200 ETA:   0h 0m Progress:  58.0% words/sec/thread:  770623 lr:  0.042001 avg.loss:  0.892277 ETA:   0h 0m Progress:  64.4% words/sec/thread:  770288 lr:  0.035586 avg.loss:  0.881554 ETA:   0h 0m Progress:  70.8% words/sec/thread:  769942 lr:  0.029177 avg.loss:  0.872880 ETA:   0h 0m Progress:  77.2% words/sec/thread:  769722 lr:  0.022761 avg.loss:  0.863862 ETA:   0h 0m Progress:  83.6% words/sec/thread:  769481 lr:  0.016351 avg.loss:  0.854855 ETA:   0h 0m Progress:  90.1% words/sec/thread:  769356 lr:  0.009932 avg.loss:  0.846624 ETA:   0h 0m Progress:  96.5% words/sec/thread:  769226 lr:  0.003516 avg.loss:  0.837483 ETA:   0h 0m Progress: 100.0% words/sec/thread:  747422 lr: -0.000000 avg.loss:  0.833534 ETA:   0h 0m Progress: 100.0% words/sec/thread:  747388 lr:  0.000000 avg.loss:  0.833534 ETA:   0h 0m 0s

real    0m1.784s
user    0m18.787s
sys     0m0.064s
Testing with epoch 30
Command: time fasttext test model.error_type_ep30.bin error_type.valid -1 0.5
N       10794
P@-1    0.848
R@-1    0.839

real    0m0.015s
user    0m0.010s
sys     0m0.005s
==========
Training with epoch 40
Command: time fasttext supervised -input error_type.train -output model.error_type_ep40 -loss one-vs-all -epoch 40
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:   4.9% words/sec/thread:  784632 lr:  0.095069 avg.loss:  1.257934 ETA:   0h 0m Progress:   9.8% words/sec/thread:  776795 lr:  0.090247 avg.loss:  1.101898 ETA:   0h 0m Progress:  14.6% words/sec/thread:  773663 lr:  0.085434 avg.loss:  1.025118 ETA:   0h 0m Progress:  19.4% words/sec/thread:  772527 lr:  0.080611 avg.loss:  0.981827 ETA:   0h 0m Progress:  24.2% words/sec/thread:  771627 lr:  0.075794 avg.loss:  0.951035 ETA:   0h 0m Progress:  29.0% words/sec/thread:  771297 lr:  0.070969 avg.loss:  0.924702 ETA:   0h 0m Progress:  33.8% words/sec/thread:  770786 lr:  0.066155 avg.loss:  0.899851 ETA:   0h 0m Progress:  38.7% words/sec/thread:  770485 lr:  0.061336 avg.loss:  0.881709 ETA:   0h 0m Progress:  43.4% words/sec/thread:  768722 lr:  0.056604 avg.loss:  0.872281 ETA:   0h 0m Progress:  48.2% words/sec/thread:  768370 lr:  0.051805 avg.loss:  0.861739 ETA:   0h 0m Progress:  53.0% words/sec/thread:  768436 lr:  0.046982 avg.loss:  0.853784 ETA:   0h 0m Progress:  57.8% words/sec/thread:  768413 lr:  0.042165 avg.loss:  0.844744 ETA:   0h 0m Progress:  62.7% words/sec/thread:  768410 lr:  0.037347 avg.loss:  0.836623 ETA:   0h 0m Progress:  67.5% words/sec/thread:  768451 lr:  0.032525 avg.loss:  0.830208 ETA:   0h 0m Progress:  72.3% words/sec/thread:  768530 lr:  0.027700 avg.loss:  0.823569 ETA:   0h 0m Progress:  77.2% words/sec/thread:  768931 lr:  0.022839 avg.loss:  0.817273 ETA:   0h 0m Progress:  82.2% words/sec/thread:  770617 lr:  0.017837 avg.loss:  0.808838 ETA:   0h 0m Progress:  87.1% words/sec/thread:  771283 lr:  0.012930 avg.loss:  0.802411 ETA:   0h 0m Progress:  92.0% words/sec/thread:  771985 lr:  0.008010 avg.loss:  0.798074 ETA:   0h 0m Progress:  96.9% words/sec/thread:  772538 lr:  0.003099 avg.loss:  0.792934 ETA:   0h 0m Progress: 100.0% words/sec/thread:  759291 lr: -0.000002 avg.loss:  0.790278 ETA:   0h 0m Progress: 100.0% words/sec/thread:  759264 lr:  0.000000 avg.loss:  0.790278 ETA:   0h 0m 0s

real    0m2.294s
user    0m24.930s
sys     0m0.052s
Testing with epoch 40
Command: time fasttext test model.error_type_ep40.bin error_type.valid -1 0.5
N       10794
P@-1    0.847
R@-1    0.838

real    0m0.015s
user    0m0.007s
sys     0m0.007s
==========
Training with epoch 50
Command: time fasttext supervised -input error_type.train -output model.error_type_ep50 -loss one-vs-all -epoch 50
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:   4.1% words/sec/thread:  810205 lr:  0.095925 avg.loss:  1.249935 ETA:   0h 0m Progress:   8.0% words/sec/thread:  794085 lr:  0.092021 avg.loss:  1.101374 ETA:   0h 0m Progress:  11.8% words/sec/thread:  785274 lr:  0.088170 avg.loss:  1.026898 ETA:   0h 0m Progress:  15.7% words/sec/thread:  780695 lr:  0.084323 avg.loss:  0.980693 ETA:   0h 0m Progress:  19.5% words/sec/thread:  778002 lr:  0.080474 avg.loss:  0.955301 ETA:   0h 0m Progress:  23.4% words/sec/thread:  776321 lr:  0.076622 avg.loss:  0.937103 ETA:   0h 0m Progress:  27.2% words/sec/thread:  774076 lr:  0.072806 avg.loss:  0.912036 ETA:   0h 0m Progress:  31.0% words/sec/thread:  773094 lr:  0.068962 avg.loss:  0.895532 ETA:   0h 0m Progress:  34.9% words/sec/thread:  772459 lr:  0.065112 avg.loss:  0.882192 ETA:   0h 0m Progress:  38.7% words/sec/thread:  771869 lr:  0.061267 avg.loss:  0.873540 ETA:   0h 0m Progress:  42.6% words/sec/thread:  771124 lr:  0.057435 avg.loss:  0.866735 ETA:   0h 0m Progress:  46.3% words/sec/thread:  768387 lr:  0.053732 avg.loss:  0.859922 ETA:   0h 0m Progress:  50.1% words/sec/thread:  767292 lr:  0.049948 avg.loss:  0.853677 ETA:   0h 0m Progress:  53.9% words/sec/thread:  767196 lr:  0.046105 avg.loss:  0.848236 ETA:   0h 0m Progress:  57.7% words/sec/thread:  767227 lr:  0.042253 avg.loss:  0.841573 ETA:   0h 0m Progress:  61.6% words/sec/thread:  767255 lr:  0.038404 avg.loss:  0.837759 ETA:   0h 0m Progress:  65.4% words/sec/thread:  767291 lr:  0.034551 avg.loss:  0.832406 ETA:   0h 0m Progress:  69.3% words/sec/thread:  767328 lr:  0.030698 avg.loss:  0.828009 ETA:   0h 0m Progress:  73.2% words/sec/thread:  767387 lr:  0.026843 avg.loss:  0.821396 ETA:   0h 0m Progress:  77.0% words/sec/thread:  767436 lr:  0.022988 avg.loss:  0.817606 ETA:   0h 0m Progress:  80.9% words/sec/thread:  767488 lr:  0.019132 avg.loss:  0.813017 ETA:   0h 0m Progress:  84.7% words/sec/thread:  767476 lr:  0.015284 avg.loss:  0.808422 ETA:   0h 0m Progress:  88.6% words/sec/thread:  767517 lr:  0.011429 avg.loss:  0.805196 ETA:   0h 0m Progress:  92.4% words/sec/thread:  767505 lr:  0.007580 avg.loss:  0.801206 ETA:   0h 0m Progress:  96.3% words/sec/thread:  767503 lr:  0.003730 avg.loss:  0.797435 ETA:   0h 0m Progress: 100.0% words/sec/thread:  766574 lr: -0.000000 avg.loss:  0.794017 ETA:   0h 0m Progress: 100.0% words/sec/thread:  766545 lr:  0.000000 avg.loss:  0.794017 ETA:   0h 0m 0s

real    0m2.789s
user    0m31.319s
sys     0m0.064s
Testing with epoch 50
Command: time fasttext test model.error_type_ep50.bin error_type.valid -1 0.5
N       10794
P@-1    0.846
R@-1    0.838

real    0m0.015s
user    0m0.011s
sys     0m0.004s
==========
Training with epoch 60
Command: time fasttext supervised -input error_type.train -output model.error_type_ep60 -loss one-vs-all -epoch 60
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:   3.4% words/sec/thread:  807408 lr:  0.096599 avg.loss:  1.270928 ETA:   0h 0m Progress:   6.6% words/sec/thread:  786315 lr:  0.093399 avg.loss:  1.111874 ETA:   0h 0m Progress:   9.8% words/sec/thread:  779312 lr:  0.090199 avg.loss:  1.039362 ETA:   0h 0m Progress:  13.0% words/sec/thread:  777861 lr:  0.086966 avg.loss:  1.000101 ETA:   0h 0m Progress:  16.3% words/sec/thread:  778544 lr:  0.083700 avg.loss:  0.972943 ETA:   0h 0m Progress:  19.6% words/sec/thread:  778919 lr:  0.080436 avg.loss:  0.955322 ETA:   0h 0m Progress:  22.8% words/sec/thread:  778820 lr:  0.077183 avg.loss:  0.935028 ETA:   0h 0m Progress:  26.1% words/sec/thread:  778372 lr:  0.073941 avg.loss:  0.914865 ETA:   0h 0m Progress:  29.3% words/sec/thread:  778425 lr:  0.070685 avg.loss:  0.900600 ETA:   0h 0m Progress:  32.6% words/sec/thread:  778575 lr:  0.067425 avg.loss:  0.888142 ETA:   0h 0m Progress:  35.8% words/sec/thread:  778768 lr:  0.064162 avg.loss:  0.878507 ETA:   0h 0m Progress:  39.1% words/sec/thread:  778766 lr:  0.060907 avg.loss:  0.870610 ETA:   0h 0m Progress:  42.4% words/sec/thread:  778880 lr:  0.057645 avg.loss:  0.864163 ETA:   0h 0m Progress:  45.6% words/sec/thread:  778947 lr:  0.054384 avg.loss:  0.857488 ETA:   0h 0m Progress:  48.9% words/sec/thread:  779009 lr:  0.051123 avg.loss:  0.852437 ETA:   0h 0m Progress:  52.1% words/sec/thread:  779032 lr:  0.047865 avg.loss:  0.849191 ETA:   0h 0m Progress:  55.4% words/sec/thread:  779055 lr:  0.044607 avg.loss:  0.844867 ETA:   0h 0m Progress:  58.6% words/sec/thread:  779019 lr:  0.041352 avg.loss:  0.840276 ETA:   0h 0m Progress:  61.9% words/sec/thread:  779051 lr:  0.038093 avg.loss:  0.834506 ETA:   0h 0m Progress:  65.2% words/sec/thread:  779033 lr:  0.034838 avg.loss:  0.829650 ETA:   0h 0m Progress:  68.4% words/sec/thread:  778880 lr:  0.031594 avg.loss:  0.824623 ETA:   0h 0m Progress:  71.7% words/sec/thread:  778881 lr:  0.028338 avg.loss:  0.820541 ETA:   0h 0m Progress:  74.9% words/sec/thread:  778886 lr:  0.025081 avg.loss:  0.816215 ETA:   0h 0m Progress:  78.2% words/sec/thread:  778940 lr:  0.021820 avg.loss:  0.812941 ETA:   0h 0m Progress:  81.4% words/sec/thread:  779009 lr:  0.018556 avg.loss:  0.809931 ETA:   0h 0m Progress:  84.7% words/sec/thread:  779054 lr:  0.015294 avg.loss:  0.806918 ETA:   0h 0m Progress:  88.0% words/sec/thread:  779084 lr:  0.012034 avg.loss:  0.804585 ETA:   0h 0m Progress:  91.2% words/sec/thread:  779105 lr:  0.008775 avg.loss:  0.801013 ETA:   0h 0m Progress:  94.5% words/sec/thread:  779146 lr:  0.005512 avg.loss:  0.797739 ETA:   0h 0m Progress:  97.7% words/sec/thread:  779174 lr:  0.002251 avg.loss:  0.793916 ETA:   0h 0m Progress: 100.0% words/sec/thread:  771413 lr: -0.000001 avg.loss:  0.791700 ETA:   0h 0m Progress: 100.0% words/sec/thread:  771394 lr:  0.000000 avg.loss:  0.791700 ETA:   0h 0m 0s

real    0m3.350s
user    0m37.018s
sys     0m0.056s
Testing with epoch 60
Command: time fasttext test model.error_type_ep60.bin error_type.valid -1 0.5
N       10794
P@-1    0.846
R@-1    0.837

real    0m0.015s
user    0m0.011s
sys     0m0.004s
==========
Training with epoch 70
Command: time fasttext supervised -input error_type.train -output model.error_type_ep70 -loss one-vs-all -epoch 70
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:   2.8% words/sec/thread:  785961 lr:  0.097163 avg.loss:  1.266017 ETA:   0h 0m Progress:   5.6% words/sec/thread:  776040 lr:  0.094417 avg.loss:  1.106338 ETA:   0h 0m Progress:   8.3% words/sec/thread:  772651 lr:  0.091673 avg.loss:  1.032033 ETA:   0h 0m Progress:  11.1% words/sec/thread:  770921 lr:  0.088929 avg.loss:  0.985654 ETA:   0h 0m Progress:  13.8% words/sec/thread:  770291 lr:  0.086178 avg.loss:  0.956648 ETA:   0h 0m Progress:  16.6% words/sec/thread:  769825 lr:  0.083428 avg.loss:  0.935095 ETA:   0h 0m Progress:  19.3% words/sec/thread:  769232 lr:  0.080685 avg.loss:  0.915064 ETA:   0h 0m Progress:  22.0% words/sec/thread:  767804 lr:  0.077969 avg.loss:  0.896099 ETA:   0h 0m Progress:  24.8% words/sec/thread:  767404 lr:  0.075231 avg.loss:  0.884053 ETA:   0h 0m Progress:  27.5% words/sec/thread:  767410 lr:  0.072480 avg.loss:  0.874807 ETA:   0h 0m Progress:  30.3% words/sec/thread:  767242 lr:  0.069738 avg.loss:  0.869217 ETA:   0h 0m Progress:  33.0% words/sec/thread:  767258 lr:  0.066988 avg.loss:  0.860249 ETA:   0h 0m Progress:  35.8% words/sec/thread:  767186 lr:  0.064242 avg.loss:  0.855294 ETA:   0h 0m Progress:  38.5% words/sec/thread:  767158 lr:  0.061494 avg.loss:  0.850417 ETA:   0h 0m Progress:  41.3% words/sec/thread:  767213 lr:  0.058741 avg.loss:  0.845491 ETA:   0h 0m Progress:  44.0% words/sec/thread:  767291 lr:  0.055988 avg.loss:  0.841505 ETA:   0h 0m Progress:  46.8% words/sec/thread:  767238 lr:  0.053242 avg.loss:  0.836507 ETA:   0h 0m Progress:  49.5% words/sec/thread:  767187 lr:  0.050496 avg.loss:  0.832472 ETA:   0h 0m Progress:  52.3% words/sec/thread:  767185 lr:  0.047746 avg.loss:  0.828037 ETA:   0h 0m Progress:  55.0% words/sec/thread:  767179 lr:  0.044998 avg.loss:  0.824032 ETA:   0h 0m Progress:  57.8% words/sec/thread:  767192 lr:  0.042248 avg.loss:  0.822475 ETA:   0h 0m Progress:  60.5% words/sec/thread:  767189 lr:  0.039500 avg.loss:  0.817350 ETA:   0h 0m Progress:  63.2% words/sec/thread:  767113 lr:  0.036758 avg.loss:  0.810798 ETA:   0h 0m Progress:  66.1% words/sec/thread:  768204 lr:  0.033915 avg.loss:  0.805604 ETA:   0h 0m Progress:  69.0% words/sec/thread:  769692 lr:  0.031028 avg.loss:  0.801068 ETA:   0h 0m Progress:  71.8% words/sec/thread:  770337 lr:  0.028210 avg.loss:  0.797421 ETA:   0h 0m Progress:  74.6% words/sec/thread:  770907 lr:  0.025395 avg.loss:  0.792904 ETA:   0h 0m Progress:  77.4% words/sec/thread:  771344 lr:  0.022588 avg.loss:  0.789456 ETA:   0h 0m Progress:  80.2% words/sec/thread:  771676 lr:  0.019788 avg.loss:  0.786290 ETA:   0h 0m Progress:  83.0% words/sec/thread:  772198 lr:  0.016967 avg.loss:  0.783243 ETA:   0h 0m Progress:  85.9% words/sec/thread:  772691 lr:  0.014145 avg.loss:  0.780083 ETA:   0h 0m Progress:  88.7% words/sec/thread:  773144 lr:  0.011325 avg.loss:  0.777576 ETA:   0h 0m Progress:  91.5% words/sec/thread:  773573 lr:  0.008504 avg.loss:  0.775105 ETA:   0h 0m Progress:  94.3% words/sec/thread:  773974 lr:  0.005682 avg.loss:  0.772267 ETA:   0h 0m Progress:  97.1% words/sec/thread:  774330 lr:  0.002864 avg.loss:  0.770016 ETA:   0h 0m Progress: 100.0% words/sec/thread:  774701 lr:  0.000042 avg.loss:  0.767768 ETA:   0h 0m Progress: 100.0% words/sec/thread:  754076 lr: -0.000001 avg.loss:  0.767774 ETA:   0h 0m Progress: 100.0% words/sec/thread:  754059 lr:  0.000000 avg.loss:  0.767774 ETA:   0h 0m 0s

real    0m3.895s
user    0m43.409s
sys     0m0.056s
Testing with epoch 70
Command: time fasttext test model.error_type_ep70.bin error_type.valid -1 0.5
N       10794
P@-1    0.846
R@-1    0.838

real    0m0.015s
user    0m0.014s
sys     0m0.000s
==========
Training with epoch 80
Command: time fasttext supervised -input error_type.train -output model.error_type_ep80 -loss one-vs-all -epoch 80
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:   2.5% words/sec/thread:  799243 lr:  0.097483 avg.loss:  1.242856 ETA:   0h 0m Progress:   4.9% words/sec/thread:  785382 lr:  0.095064 avg.loss:  1.102742 ETA:   0h 0m Progress:   7.4% words/sec/thread:  780426 lr:  0.092648 avg.loss:  1.027615 ETA:   0h 0m Progress:   9.8% words/sec/thread:  778506 lr:  0.090225 avg.loss:  0.986891 ETA:   0h 0m Progress:  12.2% words/sec/thread:  777693 lr:  0.087797 avg.loss:  0.954238 ETA:   0h 0m Progress:  14.6% words/sec/thread:  776977 lr:  0.085372 avg.loss:  0.925505 ETA:   0h 0m Progress:  17.0% words/sec/thread:  776221 lr:  0.082953 avg.loss:  0.907072 ETA:   0h 0m Progress:  19.5% words/sec/thread:  775759 lr:  0.080530 avg.loss:  0.887836 ETA:   0h 0m Progress:  21.9% words/sec/thread:  775450 lr:  0.078107 avg.loss:  0.873575 ETA:   0h 0m Progress:  24.3% words/sec/thread:  774214 lr:  0.075714 avg.loss:  0.865819 ETA:   0h 0m Progress:  26.7% words/sec/thread:  773574 lr:  0.073308 avg.loss:  0.858757 ETA:   0h 0m Progress:  29.1% words/sec/thread:  773526 lr:  0.070884 avg.loss:  0.851876 ETA:   0h 0m Progress:  31.5% words/sec/thread:  773535 lr:  0.068459 avg.loss:  0.844272 ETA:   0h 0m Progress:  34.0% words/sec/thread:  773422 lr:  0.066038 avg.loss:  0.838133 ETA:   0h 0m Progress:  36.4% words/sec/thread:  773751 lr:  0.063598 avg.loss:  0.833106 ETA:   0h 0m Progress:  39.0% words/sec/thread:  776282 lr:  0.061046 avg.loss:  0.826284 ETA:   0h 0m Progress:  41.5% words/sec/thread:  777454 lr:  0.058549 avg.loss:  0.820329 ETA:   0h 0m Progress:  43.9% words/sec/thread:  778424 lr:  0.056057 avg.loss:  0.813707 ETA:   0h 0m Progress:  46.4% words/sec/thread:  779267 lr:  0.053567 avg.loss:  0.808699 ETA:   0h 0m Progress:  48.9% words/sec/thread:  780123 lr:  0.051070 avg.loss:  0.805246 ETA:   0h 0m Progress:  51.4% words/sec/thread:  780859 lr:  0.048575 avg.loss:  0.801385 ETA:   0h 0m Progress:  53.9% words/sec/thread:  781498 lr:  0.046083 avg.loss:  0.797748 ETA:   0h 0m Progress:  56.4% words/sec/thread:  782096 lr:  0.043589 avg.loss:  0.793904 ETA:   0h 0m Progress:  58.9% words/sec/thread:  782634 lr:  0.041097 avg.loss:  0.790871 ETA:   0h 0m Progress:  61.4% words/sec/thread:  782700 lr:  0.038637 avg.loss:  0.787690 ETA:   0h 0m Progress:  63.8% words/sec/thread:  782790 lr:  0.036176 avg.loss:  0.783973 ETA:   0h 0m Progress:  66.3% words/sec/thread:  782831 lr:  0.033718 avg.loss:  0.780342 ETA:   0h 0m Progress:  68.7% words/sec/thread:  782892 lr:  0.031258 avg.loss:  0.776791 ETA:   0h 0m Progress:  71.2% words/sec/thread:  782936 lr:  0.028800 avg.loss:  0.774778 ETA:   0h 0m Progress:  73.7% words/sec/thread:  783027 lr:  0.026336 avg.loss:  0.772584 ETA:   0h 0m Progress:  76.1% words/sec/thread:  782842 lr:  0.023900 avg.loss:  0.770100 ETA:   0h 0m Progress:  78.6% words/sec/thread:  782810 lr:  0.021447 avg.loss:  0.768012 ETA:   0h 0m Progress:  81.0% words/sec/thread:  782809 lr:  0.018993 avg.loss:  0.765665 ETA:   0h 0m Progress:  83.5% words/sec/thread:  782858 lr:  0.016533 avg.loss:  0.763485 ETA:   0h 0m Progress:  85.9% words/sec/thread:  782837 lr:  0.014081 avg.loss:  0.761379 ETA:   0h 0m Progress:  88.4% words/sec/thread:  782886 lr:  0.011621 avg.loss:  0.758903 ETA:   0h 0m Progress:  90.8% words/sec/thread:  782969 lr:  0.009157 avg.loss:  0.756631 ETA:   0h 0m Progress:  93.3% words/sec/thread:  783032 lr:  0.006694 avg.loss:  0.754268 ETA:   0h 0m Progress:  95.8% words/sec/thread:  783099 lr:  0.004231 avg.loss:  0.752364 ETA:   0h 0m Progress:  98.2% words/sec/thread:  783126 lr:  0.001772 avg.loss:  0.750695 ETA:   0h 0m Progress: 100.0% words/sec/thread:  777809 lr: -0.000000 avg.loss:  0.749749 ETA:   0h 0m Progress: 100.0% words/sec/thread:  777795 lr:  0.000000 avg.loss:  0.749749 ETA:   0h 0m 0s

real    0m4.318s
user    0m49.031s
sys     0m0.076s
Testing with epoch 80
Command: time fasttext test model.error_type_ep80.bin error_type.valid -1 0.5
N       10794
P@-1    0.846
R@-1    0.837

real    0m0.015s
user    0m0.010s
sys     0m0.005s
==========
Training with epoch 90
Command: time fasttext supervised -input error_type.train -output model.error_type_ep90 -loss one-vs-all -epoch 90
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:   2.2% words/sec/thread:  792703 lr:  0.097785 avg.loss:  1.261987 ETA:   0h 0m Progress:   4.4% words/sec/thread:  781921 lr:  0.095635 avg.loss:  1.105549 ETA:   0h 0m Progress:   6.5% words/sec/thread:  778810 lr:  0.093482 avg.loss:  1.024158 ETA:   0h 0m Progress:   8.7% words/sec/thread:  777058 lr:  0.091330 avg.loss:  0.984262 ETA:   0h 0m Progress:  10.8% words/sec/thread:  776186 lr:  0.089177 avg.loss:  0.950192 ETA:   0h 0m Progress:  13.0% words/sec/thread:  775711 lr:  0.087022 avg.loss:  0.926023 ETA:   0h 0m Progress:  15.1% words/sec/thread:  775302 lr:  0.084867 avg.loss:  0.909607 ETA:   0h 0m Progress:  17.3% words/sec/thread:  775049 lr:  0.082714 avg.loss:  0.893010 ETA:   0h 0m Progress:  19.4% words/sec/thread:  773877 lr:  0.080583 avg.loss:  0.881652 ETA:   0h 0m Progress:  21.6% words/sec/thread:  773823 lr:  0.078427 avg.loss:  0.870883 ETA:   0h 0m Progress:  23.7% words/sec/thread:  773748 lr:  0.076273 avg.loss:  0.861801 ETA:   0h 0m Progress:  25.9% words/sec/thread:  773697 lr:  0.074118 avg.loss:  0.853848 ETA:   0h 0m Progress:  28.0% words/sec/thread:  773733 lr:  0.071960 avg.loss:  0.844756 ETA:   0h 0m Progress:  30.2% words/sec/thread:  773723 lr:  0.069804 avg.loss:  0.838942 ETA:   0h 0m Progress:  32.4% words/sec/thread:  773771 lr:  0.067646 avg.loss:  0.832020 ETA:   0h 0m Progress:  34.5% words/sec/thread:  773762 lr:  0.065490 avg.loss:  0.825377 ETA:   0h 0m Progress:  36.7% words/sec/thread:  773505 lr:  0.063345 avg.loss:  0.820649 ETA:   0h 0m Progress:  38.8% words/sec/thread:  773537 lr:  0.061187 avg.loss:  0.815093 ETA:   0h 0m Progress:  41.0% words/sec/thread:  773523 lr:  0.059032 avg.loss:  0.810137 ETA:   0h 0m Progress:  43.1% words/sec/thread:  773572 lr:  0.056874 avg.loss:  0.806102 ETA:   0h 0m Progress:  45.3% words/sec/thread:  773513 lr:  0.054721 avg.loss:  0.801516 ETA:   0h 0m Progress:  47.4% words/sec/thread:  773539 lr:  0.052564 avg.loss:  0.796345 ETA:   0h 0m Progress:  49.6% words/sec/thread:  773582 lr:  0.050405 avg.loss:  0.790693 ETA:   0h 0m Progress:  51.8% words/sec/thread:  773626 lr:  0.048246 avg.loss:  0.786650 ETA:   0h 0m Progress:  53.9% words/sec/thread:  773680 lr:  0.046086 avg.loss:  0.781724 ETA:   0h 0m Progress:  56.1% words/sec/thread:  773702 lr:  0.043928 avg.loss:  0.779071 ETA:   0h 0m Progress:  58.2% words/sec/thread:  773741 lr:  0.041769 avg.loss:  0.778218 ETA:   0h 0m Progress:  60.4% words/sec/thread:  773762 lr:  0.039611 avg.loss:  0.776784 ETA:   0h 0m Progress:  62.5% words/sec/thread:  773612 lr:  0.037466 avg.loss:  0.775432 ETA:   0h 0m Progress:  64.7% words/sec/thread:  773390 lr:  0.035329 avg.loss:  0.774985 ETA:   0h 0m Progress:  66.8% words/sec/thread:  773386 lr:  0.033173 avg.loss:  0.774006 ETA:   0h 0m Progress:  69.0% words/sec/thread:  773402 lr:  0.031016 avg.loss:  0.772818 ETA:   0h 0m Progress:  71.1% words/sec/thread:  773414 lr:  0.028859 avg.loss:  0.770824 ETA:   0h 0m Progress:  73.3% words/sec/thread:  773445 lr:  0.026701 avg.loss:  0.769202 ETA:   0h 0m Progress:  75.5% words/sec/thread:  773484 lr:  0.024541 avg.loss:  0.768199 ETA:   0h 0m Progress:  77.6% words/sec/thread:  773492 lr:  0.022385 avg.loss:  0.766539 ETA:   0h 0m Progress:  79.8% words/sec/thread:  773524 lr:  0.020226 avg.loss:  0.765736 ETA:   0h 0m Progress:  81.9% words/sec/thread:  773532 lr:  0.018070 avg.loss:  0.764239 ETA:   0h 0m Progress:  84.1% words/sec/thread:  773512 lr:  0.015917 avg.loss:  0.763062 ETA:   0h 0m Progress:  86.2% words/sec/thread:  773550 lr:  0.013757 avg.loss:  0.762156 ETA:   0h 0m Progress:  88.4% words/sec/thread:  773552 lr:  0.011602 avg.loss:  0.760930 ETA:   0h 0m Progress:  90.6% words/sec/thread:  774238 lr:  0.009365 avg.loss:  0.759641 ETA:   0h 0m Progress:  92.9% words/sec/thread:  775125 lr:  0.007102 avg.loss:  0.757845 ETA:   0h 0m Progress:  95.2% words/sec/thread:  775928 lr:  0.004844 avg.loss:  0.756598 ETA:   0h 0m Progress:  97.4% words/sec/thread:  776710 lr:  0.002583 avg.loss:  0.755196 ETA:   0h 0m Progress:  99.7% words/sec/thread:  777436 lr:  0.000325 avg.loss:  0.753549 ETA:   0h 0m Progress: 100.0% words/sec/thread:  763373 lr: -0.000000 avg.loss:  0.753477 ETA:   0h 0m Progress: 100.0% words/sec/thread:  763360 lr:  0.000000 avg.loss:  0.753477 ETA:   0h 0m 0s

real    0m4.920s
user    0m55.554s
sys     0m0.080s
Testing with epoch 90
Command: time fasttext test model.error_type_ep90.bin error_type.valid -1 0.5
N       10794
P@-1    0.844
R@-1    0.837

real    0m0.015s
user    0m0.015s
sys     0m0.000s
==========
Training with epoch 100
Command: time fasttext supervised -input error_type.train -output model.error_type_ep100 -loss one-vs-all -epoch 100
Read 0M words
Number of words:  8054
Number of labels: 11
Progress:   2.0% words/sec/thread:  802357 lr:  0.097980 avg.loss:  1.266052 ETA:   0h 0m Progress:   3.9% words/sec/thread:  782726 lr:  0.096065 avg.loss:  1.112471 ETA:   0h 0m Progress:   5.9% words/sec/thread:  777466 lr:  0.094141 avg.loss:  1.033859 ETA:   0h 0m Progress:   7.8% words/sec/thread:  774473 lr:  0.092221 avg.loss:  0.986153 ETA:   0h 0m Progress:   9.7% words/sec/thread:  772966 lr:  0.090297 avg.loss:  0.953814 ETA:   0h 0m Progress:  11.6% words/sec/thread:  772096 lr:  0.088371 avg.loss:  0.933403 ETA:   0h 0m Progress:  13.6% words/sec/thread:  771512 lr:  0.086445 avg.loss:  0.911752 ETA:   0h 0m Progress:  15.5% words/sec/thread:  770924 lr:  0.084521 avg.loss:  0.895514 ETA:   0h 0m Progress:  17.4% words/sec/thread:  770581 lr:  0.082595 avg.loss:  0.888558 ETA:   0h 0m Progress:  19.3% words/sec/thread:  770076 lr:  0.080676 avg.loss:  0.880135 ETA:   0h 0m Progress:  21.2% words/sec/thread:  769817 lr:  0.078752 avg.loss:  0.873745 ETA:   0h 0m Progress:  23.2% words/sec/thread:  769509 lr:  0.076832 avg.loss:  0.864848 ETA:   0h 0m Progress:  25.1% words/sec/thread:  769462 lr:  0.074903 avg.loss:  0.857568 ETA:   0h 0m Progress:  27.0% words/sec/thread:  769325 lr:  0.072977 avg.loss:  0.851669 ETA:   0h 0m Progress:  29.0% words/sec/thread:  770036 lr:  0.071021 avg.loss:  0.845678 ETA:   0h 0m Progress:  30.9% words/sec/thread:  770713 lr:  0.069062 avg.loss:  0.841016 ETA:   0h 0m Progress:  32.9% words/sec/thread:  771065 lr:  0.067114 avg.loss:  0.832904 ETA:   0h 0m Progress:  34.8% words/sec/thread:  771584 lr:  0.065156 avg.loss:  0.828000 ETA:   0h 0m Progress:  36.8% words/sec/thread:  772050 lr:  0.063198 avg.loss:  0.825229 ETA:   0h 0m Progress:  38.8% words/sec/thread:  772379 lr:  0.061245 avg.loss:  0.822248 ETA:   0h 0m Progress:  40.7% words/sec/thread:  772792 lr:  0.059286 avg.loss:  0.819809 ETA:   0h 0m Progress:  42.7% words/sec/thread:  772804 lr:  0.057347 avg.loss:  0.816352 ETA:   0h 0m Progress:  44.6% words/sec/thread:  773083 lr:  0.055392 avg.loss:  0.813882 ETA:   0h 0m Progress:  46.6% words/sec/thread:  773431 lr:  0.053432 avg.loss:  0.810654 ETA:   0h 0m Progress:  48.5% words/sec/thread:  773749 lr:  0.051473 avg.loss:  0.807567 ETA:   0h 0m Progress:  50.5% words/sec/thread:  774014 lr:  0.049514 avg.loss:  0.804907 ETA:   0h 0m Progress:  52.4% words/sec/thread:  774268 lr:  0.047556 avg.loss:  0.802107 ETA:   0h 0m Progress:  54.4% words/sec/thread:  774509 lr:  0.045597 avg.loss:  0.798994 ETA:   0h 0m Progress:  56.4% words/sec/thread:  774746 lr:  0.043636 avg.loss:  0.794986 ETA:   0h 0m Progress:  58.3% words/sec/thread:  774949 lr:  0.041678 avg.loss:  0.793340 ETA:   0h 0m Progress:  60.3% words/sec/thread:  775139 lr:  0.039719 avg.loss:  0.791560 ETA:   0h 0m Progress:  62.2% words/sec/thread:  775292 lr:  0.037762 avg.loss:  0.789666 ETA:   0h 0m Progress:  64.2% words/sec/thread:  775475 lr:  0.035803 avg.loss:  0.787540 ETA:   0h 0m Progress:  66.2% words/sec/thread:  775592 lr:  0.033847 avg.loss:  0.784786 ETA:   0h 0m Progress:  68.1% words/sec/thread:  775747 lr:  0.031888 avg.loss:  0.782767 ETA:   0h 0m Progress:  70.1% words/sec/thread:  775923 lr:  0.029926 avg.loss:  0.780424 ETA:   0h 0m Progress:  72.0% words/sec/thread:  776039 lr:  0.027969 avg.loss:  0.778445 ETA:   0h 0m Progress:  74.0% words/sec/thread:  776206 lr:  0.026006 avg.loss:  0.775692 ETA:   0h 0m Progress:  76.0% words/sec/thread:  776310 lr:  0.024049 avg.loss:  0.773016 ETA:   0h 0m Progress:  77.9% words/sec/thread:  776438 lr:  0.022089 avg.loss:  0.770312 ETA:   0h 0m Progress:  79.9% words/sec/thread:  776522 lr:  0.020133 avg.loss:  0.768110 ETA:   0h 0m Progress:  81.8% words/sec/thread:  776529 lr:  0.018185 avg.loss:  0.765453 ETA:   0h 0m Progress:  83.8% words/sec/thread:  776452 lr:  0.016246 avg.loss:  0.763277 ETA:   0h 0m Progress:  85.7% words/sec/thread:  776530 lr:  0.014290 avg.loss:  0.761818 ETA:   0h 0m Progress:  87.7% words/sec/thread:  776626 lr:  0.012331 avg.loss:  0.760310 ETA:   0h 0m Progress:  89.6% words/sec/thread:  776733 lr:  0.010370 avg.loss:  0.758867 ETA:   0h 0m Progress:  91.6% words/sec/thread:  776805 lr:  0.008413 avg.loss:  0.757318 ETA:   0h 0m Progress:  93.5% words/sec/thread:  776872 lr:  0.006457 avg.loss:  0.755836 ETA:   0h 0m Progress:  95.5% words/sec/thread:  776935 lr:  0.004501 avg.loss:  0.754658 ETA:   0h 0m Progress:  97.5% words/sec/thread:  777043 lr:  0.002538 avg.loss:  0.753148 ETA:   0h 0m Progress:  99.4% words/sec/thread:  777107 lr:  0.000581 avg.loss:  0.751912 ETA:   0h 0m Progress: 100.0% words/sec/thread:  766616 lr: -0.000000 avg.loss:  0.751654 ETA:   0h 0m Progress: 100.0% words/sec/thread:  766605 lr:  0.000000 avg.loss:  0.751654 ETA:   0h 0m 0s

real    0m5.439s
user    1m1.753s
sys     0m0.064s
Testing with epoch 100
Command: time fasttext test model.error_type_ep100.bin error_type.valid -1 0.5
N       10794
P@-1    0.843
R@-1    0.839

real    0m0.020s
user    0m0.020s
sys     0m0.000s
==========
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext/multi-label$
```

## Online Prediction 

-1 0.5 option တွေနဲ့ဆိုရင် multiple label ကိုပါ ခန့်မှန်းပေးနိုင်တယ်။  

(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext/multi-label$ fasttext predict model.error_type_ep100.bin - -1 0.5
ပုန်း တေ ရှိ
__label__typo __label__pho
ရွာ တေ က
__label__typo __label__pho
ယ နစ် တက်
__label__typo __label__pho
ဆင် မှု လေး
__label__typo
နေ ပီး
__label__typo __label__pho
ဲ့ ဖစ် တည်
__label__typo
တီး မှု လက်
__label__typo
ရ ပီး ပါ
__label__typo __label__pho
ကုန်း ပီး အော
__label__typo __label__pho
ရ မာ မ
__label__typo __label__pho

epoch 20 မော်ဒယ်နဲ့ စမ်းကြည့်ရင်လည်း အဆင်ပြေတယ် ...  

(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext/multi-label$ fasttext predict model.error_type_ep20.bin - -1 0.5
ပုန်း တေ ရှိ
__label__typo __label__pho
ရွာ တေ က
__label__typo __label__pho
ယ နစ် တက်
__label__typo __label__pho
ဆင် မှု လေး
__label__typo
နေ ပီး
__label__typo __label__pho
ဲ့ ဖစ် တည်
__label__typo
တီး မှု လက်
__label__typo
ရ ပီး ပါ
__label__typo __label__pho
ကုန်း ပီး အော
__label__typo __label__pho
ရ မာ မ
__label__typo __label__pho
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext/multi-label$

## Recounting Labels

label တွေကို ပြန်ရေတွက်ကြည့်ဖို့ ဆုံးဖြတ်ခဲ့တယ်။ ဒီတစ်ခါတော့ multiple label တွေက ဘယ်လောက် ရာခိုင်နှုန်း ပါနေတာလဲ ဆိုတာကိုပါ သိအောင် code ကို ပြင်ရေးခဲ့တယ်။

(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext/multi-label/check_labels$ cat ./label_counter_multiple.py
## Written by Ye Kyaw Thu, LU Lab., Myanmar
## for counting unique lables from the multi-label file
## __label__typo ကြည့် ရင် နဲ့
## __label__pho __label__typo ယောင် တေ ကြေင့်
## __label__pho __label__typo ချိ ပီး ပစ်
## for this time, I wanna see % of multiple labels also
## last updated: 23 Nov 2023

import sys
from collections import defaultdict

def extract_labels(filename):
    label_count = defaultdict(int)
    total_count = 0

    with open(filename, 'r', encoding='utf-8') as file:
        for line in file:
            label_parts = ' '.join([part for part in line.strip().split() if part.startswith('__label__')])
            label_count[label_parts] += 1
            total_count += 1

    return label_count, total_count

def main():
    if len(sys.argv) < 2:
        print("Usage: python script.py <filename>")
        sys.exit(1)

    filename = sys.argv[1]
    label_count, total_count = extract_labels(filename)

    for label, count in label_count.items():
        percentage = (count / total_count) * 100
        print(f"{label}: {count}, {percentage:.2f}%")

if __name__ == "__main__":
    main()

(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext/multi-label/check_labels$

multiple label တွေကိုပါ ရေတွက်ကြည့်တော့ "__label__pho __label__typo" တမျိုးပဲ 7.61% ရှိတာကိုတွေ့ရပြီး၊ ကျန်တဲ့ multiple label တွေကတော့ အောက်ပါအတိုင်း % က တအားနည်းတာကိုတော့ တွေ့ရတယ်။  

(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext/multi-label/check_labels$ python ./label_counter_multiple.py ./error_type.all.shuf.txt
__label__typo: 37933, 35.14%
__label__seq: 4650, 4.31%
__label__pho: 41799, 38.73%
__label__pho __label__typo: 8217, 7.61%
__label__stack: 2099, 1.94%
__label__con: 6601, 6.12%
__label__slang: 3867, 3.58%
__label__encode: 510, 0.47%
__label__sensitive: 1347, 1.25%
__label__short: 646, 0.60%
__label__slang __label__typo: 28, 0.03%
__label__dialect: 131, 0.12%
__label__con __label__pho: 9, 0.01%
__label__pho __label__seq: 25, 0.02%
__label__seq __label__typo: 31, 0.03%
__label__con __label__seq: 21, 0.02%
__label__pho___label__typo: 2, 0.00%
__label__con __label__typo: 16, 0.01%
__label__slang __label__seq: 3, 0.00%
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext/multi-label/check_labels$

