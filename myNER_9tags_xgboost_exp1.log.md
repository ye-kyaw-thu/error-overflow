# Experiment 1 Log

ဒီ experiment log ကတော့ လက်ရှိ ပြင်ဆင်နေဆဲ myNER corpus ရဲ့ တစ်ပိုင်း tag 9 ခုဒေတာ (work together with Kaung Lwin Thant) နဲ့ ပထမဆုံး အကြိမ် tagging training/testing ကို xgboost approach လုပ်ထားတဲ့ log ပါ။    

## Check the data

အသစ်ထပ်ဝင်လာတဲ့ စာကြောင်းရေ ၂၀၀ ဖိုင်ကို စစ်ကြည့်...  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$ wc sample_200_sentences
   200   6772 115626 sample_200_sentences
```

format က အောက်ပါအတိုင်း ...  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$ head sample_200_sentences
ေနာက်/O မှ/O လာ ေသာ/O ဒုတိယ/O မြောက်/O တိုင်တမသရီး/O ဒုံးပျံ/O ကို/O အမေရိကန်/B-ORG လေ/I-ORG တပ်/E-ORG ၏/O ကမ္ဘာပတ်လမ်းကြောင်း/O အတိုင်း/O လည်ပတ်/O နေ/O သော/O လူ/O လိုက်/O ပါ/O သည့်/O အာကာသ/O ဓါတ်ခွဲခန်း/O (/O အမ်အိုအယ်လ်/S-LOC )/O အတွက်/O ဒုံးပျံ/O ပစ်/O စင်/O အဖြစ်/O အသုံးပြု/O ရန်/O မွမ်းမံ/O ပြုပြင်/O ခဲ့/O ပါ/O သည်/O ။/O
အခြား/O သူ/O များ/O ၏/O တီထွင်ဆန်းသစ်/O မှု/O များ/O မှ/O သူ/O တို့/O အကျိုးကျေးဇူး/O များ/O ရ/O ရှိ/O နိုင်/O လိမ့်/O မည်/O ဟု/O ဖေ့စ်ဘွတ်/S-ORG က/O မျှော်လင့်/O သည်/O ။/O
ယူဂန်ဒါ/B-LOC နိုင်ငံ/E-LOC သမ္မတ/O ယူဝါရီ/B-PER မူစပန်နီ/E-PER ၏/O ယာဉ်/O တန်း/O တစ်/O ဝက်/O ကျော်/O ကို/O ကြာသပတေး/B-DATE နေ့/E-DATE တွင်/O ရဝမ်ဒါ/S-LOC ဝင်ရောက်/O ခြင်း/O မှ/O တားဆီး/O ခဲ့/O သည်/O ။/O
ယခု/O ချိန်/O မှာ/O အရေးကြီး/O သော/O အရာ/O သည်/O ဤ/O ရည်မှန်း/O ချက်/O ကို/O လက်တွေ့/O အကောင်အထည်ဖော်/O ဖို့/O လိုအပ်/O သည့်/O ရန်ပုံငွေ/O နှင့်/O နည်းပညာ/O ဆိုင်ရာ/O အကူအညီ/O ကို/O ဆီယာရာ/B-ORG လီယွန်/E-ORG က/O အမှန်တကယ်/O လက်ခံ/O ရ/O ရှိ/O ဖို့/O ဖြစ်/O ပါ/O တယ်/O ။/O
ကမ္ဘာ့/O တည်သရွေ့/O ရှိ/O နေ/O မှာ/O ဖြစ်/O သည်/O ။/O
ပြည်ခိုင်ဖြိုး/B-ORG ပါတီ/E-ORG ရှိ/O နေ/O သမျှ/O အမျိုး/O ဂုဏ်/O ဇာတိဂုဏ်/O မ/O ညှိုးနွမ်း/O စေ/O ရ/O ။/O
ဖယ်ဒရယ်/O စနစ်/O ကို/O အခြေခံ/O တဲ့/O နိုင်ငံတော်/O တစ်/O ခု/O တည်ထောင်/O ဖို့/O မှန်ကန်/O စွာ/O ဆန္ဒ/O ရှိ/O လျှင်/O usdp/S-ORG ကို/O မဲ/O ပေး/O ပါ/O ။/O
ကျွန်တော်/O တို့/O သည်/O နိုင်ငံ/O တိုင်း/O နှင့်/O တန်းတူ/O လေးစား/O စွာ/O ဆက်ဆံ/O ပြီး/O စီးပွား/O ရေး/O လူ/O မှု/O ရေး/O နှင့်/O သယ်ယူပို့ဆောင်ရေး/O တို့/O ကို/O ဦး/O စား/O ပေး/O ပူးပေါင်း/O ဆောင်ရွက်/O သည်/O ။/O
ကော်မရှင်/O အဖွဲ့/O ၏/O ကြိုးပမ်း/O အား/O ထုတ်/O မှု/O ကြောင့်/O အသေးစိတ်/O အစီရင်ခံစာ/O (/O မူကြမ်း/O )/O ကို/O စုစည်း/O ရေး/O သား/O ပြီး/O ဖြစ်/O သည်/O ။/O
နိုင်ငံတော်/O ၏/O အတိုင်ပင်ခံ/O ပုဂ္ဂိုလ်/O ဒေါ်/B-PER အောင်ဆန်း/I-PER စုကြည်/E-PER အနေဖြင့်/O နိုင်ငံတကာ/O မျက်နှာ/O စာ/O များ/O နိုင်ငံတကာ/O ကိစ္စရပ်/O များ/O တွင်/O အာဆီယံ/S-ORG ကိုယ်/O စား/O တက်ကြွ/O စွာ/O ဦးဆောင်/O မှု/O ပေး/O ရေး/O ကို/O လည်း/O ဆွေးနွေး/O ခဲ့/O ကြ/O သည်/O ။/O
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$
```

# Combine with the 10K data

ရှေ့မှာ ပြင်ထားပြီးသား 10K (i.e. 10,000 sentences) ဒေတာနဲ့ အသစ်ထပ်ဝင်လာတဲ့ စာကြောင်းရေ ၂၀၀ ကို ပေါင်းတဲ့ အလုပ်ပါ ...  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$ cp ../10k_NER_draft_version1_KaungLwinThant.txt .
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$ wc 10k_NER_draft_version1_KaungLwinThant.txt
  10002  145867 2317130 10k_NER_draft_version1_KaungLwinThant.txt
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$
```

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ cp train.txt ../data/exp1/
(xgboost) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ cd ../data/exp1/
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$ ls
10k_NER_draft_version1_KaungLwinThant.txt  original              train.txt
exp1.log.txt                               sample_200_sentences
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$ cat train.txt sample_200_sentences > new_train.txt
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$ wc new_train.txt
   9202  137739 2195956 new_train.txt
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$
```

I will use this new_train.txt for training  

## Data Cleaning

I found some errors on new 200 sentences and some are as follows:  

လက်တွေ့မှာ ထုံးစံအတိုင်းပါပဲ manual tagging လုပ်ထားတာမို့လို့ ကျောင်းသားရဲ့ အတွေ့အကြုံပေါ်မူတည်ပြီး မှားတာတွေ ပါတတ်ပါတယ်။ ဒီ cleaning အဆင့်က ရေးထားတဲ့ python code နဲ့ စစ်ကြည့်လိုက်၊ လက်နဲ့ ပြန်ပြင်လိုက်နဲ့ လေးငါးခြောက်ခါ ထပ်လုပ်ရတာမို့လို့ training လုပ်တဲ့အဆင့်အထိက တော်တော် ကြာခဲ့ပါတယ်။  

အမှားတွေထဲက example တချို့က အောက်ပါအတိုင်းပါ။  

```
စတန်/B-PER လီ/E-PER နှင့်/O သူ/O ၏/O မိသားစု/O အတွက်/O အပြုသဘော/O ဆုံးဖြတ်/O ချက်/O ကို/O ကျွန်တော်/O တို့ ေမျှာ်/O လင့်/O သည်/O ဟု/O လီ/S-PER ၏/O ရှေ့နေ/O ၊/O မကဝီလီလျှံ/S-PER က/O ပြော/O ခဲ့/O သည်/O ။/O
```

```
မင်းလှ/B-LOC မြို့နယ်/E-LOC ၊/O စိန်ကန့်လန့်/B-LOC ကျေးရွာ/E-LOC အနီး/O ရှိ/O မက္ခာ/B-LOC ရေတံခွန်/E-LOC ဆင်/O စခန်း/O စတင်/O ဖွင့်လှစ် ။/O
```

```
ပုလော/B-LOC မြို့နယ်/E-LOC တွင်/O မောင်/O ဖြစ်/O သူ/O သေဆုံး/O ခဲ့/O တဲ့/O ဖြစ်/O စဉ်/O ကို/O မသင်္ကာ/O သ/O ဖြင်/O အစ်မ/O ဖြစ်/O သူ/O က/O အမှု/O ဖွင်/O ရာ/O အလောင်း/O ကို/O ပြန်လည်/O ဖော်/O ယူ/O စစ်ဆေး/O ခဲ့/O ပြီး/O လူ/O သတ်/O မှု/O ဖြစ်/O ကြောင်း/O စစ်ဆေး/O တွေ့/O ရှိ/O ခဲ့
```

## Check Tags

ဒီ analyze_NER_corpus.py code က github ရဲ့ tools အောက်မှာ တင်ပေးထားမို့ စိတ်ဝင်စားရင် လေ့လာကြည့်ပါ။  
အစပိုင်းမှာ error ကတော်တော်များများ ရှိပါတယ်။ အောက်ပါအတိုင်းပါ။  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ python ../data/analyze_NER_corpus.py ./train.txt
Analysis of './train.txt'
----------------------------------------
1. Number of sentences without named entities: 6788
2. Frequency of each tag:
   B-DATE: 514
   B-EVENT: 67
   B-LCO: 1
   B-LOC: 1060
   B-NUM: 161
   B-ORG: 305
...
...
...
   က: 0.00%
   ကျယ်ပြန့်: 0.00%
   ခဲ့: 0.00%
   တို့: 0.00%
   ဖွင့်လှစ်: 0.00%
   မ: 0.00%
   ရ: 0.00%
   လာ: 0.00%
   သည်: 0.00%
```

အကြောင်း ၂၀၀ ဖိုင်ကို ဖွင့် ဝင်ပြင်လိုက် ပြန်စစ်လိုက်နဲ့ နောက်ဆုံး data cleaning အပိုင်းက ပြီးခါနီးတဲ့ အခြေအနေမှာတော့ အောက်ပါအတိုင်း ပါ။  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ python ../data/analyze_NER_corpus.py train.txt
Analysis of 'train.txt'
----------------------------------------
1. Number of sentences without named entities: 6788
2. Frequency of each tag:
   B-DATE: 514
   B-EVENT: 67
   B-LCO: 1
   B-LOC: 1060
   B-NUM: 161
   B-ORG: 305
   B-PER: 244
   B-PRODUCT: 19
   B-TIME: 124
   E-DATE: 514
   E-EVENT: 67
   E-LOC: 1060
   E-NUM: 161
   E-ORG: 306
   E-PER: 245
   E-PRODUCT: 19
   E-TIME: 124
   I-DATE: 399
   I-EVENT: 59
   I-LOC: 173
   I-NUM: 27
   I-ORG: 232
   I-PER: 19
   I-PRODUCT: 5
   I-TIME: 84
   O: 129123
   S-DATE: 123
   S-EVENT: 13
   S-LOC: 891
   S-NUM: 690
   S-ORG: 160
   S-PER: 669
   S-PRODUCT: 17
   S-TIME: 58
   SNUM: 1
3. Distribution of each tag:
   B-DATE: 0.37%
   B-EVENT: 0.05%
   B-LCO: 0.00%
   B-LOC: 0.77%
   B-NUM: 0.12%
   B-ORG: 0.22%
   B-PER: 0.18%
   B-PRODUCT: 0.01%
   B-TIME: 0.09%
   E-DATE: 0.37%
   E-EVENT: 0.05%
   E-LOC: 0.77%
   E-NUM: 0.12%
   E-ORG: 0.22%
   E-PER: 0.18%
   E-PRODUCT: 0.01%
   E-TIME: 0.09%
   I-DATE: 0.29%
   I-EVENT: 0.04%
   I-LOC: 0.13%
   I-NUM: 0.02%
   I-ORG: 0.17%
   I-PER: 0.01%
   I-PRODUCT: 0.00%
   I-TIME: 0.06%
   O: 93.75%
   S-DATE: 0.09%
   S-EVENT: 0.01%
   S-LOC: 0.65%
   S-NUM: 0.50%
   S-ORG: 0.12%
   S-PER: 0.49%
   S-PRODUCT: 0.01%
   S-TIME: 0.04%
   SNUM: 0.00%
```

Why SNUM?!  

After error fixing SNUM to S-NUM, I combined again (hope this is the final error fixing ...)  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$ cat train.txt sample_200_sentences > new_train.txt
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$ wc new_train.txt
   9202  137734 2195960 new_train.txt
```

Remake or Update train.txt as follows:   

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$ (xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$ cp new_train.txt ../../xgboost/
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$ cp new_train.txt ../../bi-LSTM/
```

Recheck again:  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$ python ../analyze_NER_corpus.py ./new_train.txt
Analysis of './new_train.txt'
----------------------------------------
1. Number of sentences without named entities: 6788
2. Frequency of each tag:
   B-DATE: 514
   B-EVENT: 67
   B-LCO: 1
   B-LOC: 1060
   B-NUM: 161
   B-ORG: 305
   B-PER: 244
   B-PRODUCT: 19
   B-TIME: 124
   E-DATE: 514
   E-EVENT: 67
   E-LOC: 1060
   E-NUM: 161
   E-ORG: 306
   E-PER: 245
   E-PRODUCT: 19
   E-TIME: 124
   I-DATE: 399
   I-EVENT: 59
   I-LOC: 173
   I-NUM: 27
   I-ORG: 232
   I-PER: 19
   I-PRODUCT: 5
   I-TIME: 84
   O: 129123
   S-DATE: 123
   S-EVENT: 13
   S-LOC: 891
   S-NUM: 691
   S-ORG: 160
   S-PER: 669
   S-PRODUCT: 17
   S-TIME: 58
3. Distribution of each tag:
   B-DATE: 0.37%
   B-EVENT: 0.05%
   B-LCO: 0.00%
   B-LOC: 0.77%
   B-NUM: 0.12%
   B-ORG: 0.22%
   B-PER: 0.18%
   B-PRODUCT: 0.01%
   B-TIME: 0.09%
   E-DATE: 0.37%
   E-EVENT: 0.05%
   E-LOC: 0.77%
   E-NUM: 0.12%
   E-ORG: 0.22%
   E-PER: 0.18%
   E-PRODUCT: 0.01%
   E-TIME: 0.09%
   I-DATE: 0.29%
   I-EVENT: 0.04%
   I-LOC: 0.13%
   I-NUM: 0.02%
   I-ORG: 0.17%
   I-PER: 0.01%
   I-PRODUCT: 0.00%
   I-TIME: 0.06%
   O: 93.75%
   S-DATE: 0.09%
   S-EVENT: 0.01%
   S-LOC: 0.65%
   S-NUM: 0.50%
   S-ORG: 0.12%
   S-PER: 0.49%
   S-PRODUCT: 0.01%
   S-TIME: 0.04%

(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$
```

Check with --format abstract  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ python ../data/analyze_NER_corpus.py ./train.txt --format abstract
Analysis of './train.txt'
----------------------------------------
1. Number of sentences without named entities: 6788
2. Frequency of each tag:
   DATE: 1550
   EVENT: 206
   LCO: 1
   LOC: 3184
   NUM: 1040
   O: 129123
   ORG: 1003
   PER: 1177
   PRODUCT: 60
   TIME: 390
3. Distribution of each tag:
   DATE: 1.13%
   EVENT: 0.15%
   LCO: 0.00%
   LOC: 2.31%
   NUM: 0.76%
   O: 93.75%
   ORG: 0.73%
   PER: 0.85%
   PRODUCT: 0.04%
   TIME: 0.28%

(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

## Checking Testing Data

Training data ကို စစ်ကြည့်ခဲ့သလို testing data ကိုလည်း analyze_NER_corpus.py နဲ့ပဲ စစ်ကြည့်ခဲ့ပါတယ်။  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ python ../data/analyze_NER_corpus.py ./test.txt
Analysis of './test.txt'
----------------------------------------
1. Number of sentences without named entities: 744
2. Frequency of each tag:
   B-DATE: 56
   B-EVENT: 6
   B-LOC: 107
   B-NUM: 24
   B-ORG: 35
   B-PER: 26
   B-PRODUCT: 1
   B-TIME: 11
   E-DATE: 56
   E-EVENT: 6
   E-LOC: 107
   E-NUM: 24
   E-ORG: 35
   E-PER: 26
   E-PRODUCT: 1
   E-TIME: 11
   I-DATE: 60
   I-EVENT: 3
   I-LOC: 17
   I-NUM: 5
   I-ORG: 14
   I-TIME: 5
   O: 14002
   S-DATE: 14
   S-LOC: 71
   S-NUM: 67
   S-ORG: 20
   S-PER: 74
   S-TIME: 5
3. Distribution of each tag:
   B-DATE: 0.38%
   B-EVENT: 0.04%
   B-LOC: 0.72%
   B-NUM: 0.16%
   B-ORG: 0.24%
   B-PER: 0.17%
   B-PRODUCT: 0.01%
   B-TIME: 0.07%
   E-DATE: 0.38%
   E-EVENT: 0.04%
   E-LOC: 0.72%
   E-NUM: 0.16%
   E-ORG: 0.24%
   E-PER: 0.17%
   E-PRODUCT: 0.01%
   E-TIME: 0.07%
   I-DATE: 0.40%
   I-EVENT: 0.02%
   I-LOC: 0.11%
   I-NUM: 0.03%
   I-ORG: 0.09%
   I-TIME: 0.03%
   O: 94.04%
   S-DATE: 0.09%
   S-LOC: 0.48%
   S-NUM: 0.45%
   S-ORG: 0.13%
   S-PER: 0.50%
   S-TIME: 0.03%
```

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ (xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ python ../data/analyze_NER_corpus.py ./test.txt --format abstract
Analysis of './test.txt'
----------------------------------------
1. Number of sentences without named entities: 744
2. Frequency of each tag:
   DATE: 186
   EVENT: 15
   LOC: 302
   NUM: 120
   O: 14002
   ORG: 104
   PER: 126
   PRODUCT: 2
   TIME: 32
3. Distribution of each tag:
   DATE: 1.25%
   EVENT: 0.10%
   LOC: 2.03%
   NUM: 0.81%
   O: 94.04%
   ORG: 0.70%
   PER: 0.85%
   PRODUCT: 0.01%
   TIME: 0.21%

(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

## xgboost Training

Data size info:  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ wc ./train.txt
   9202  137734 2195960 ./train.txt
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ wc ./test.txt
   999  14889 236610 ./test.txt
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

Training start ...  
မနေ့က ညက မအိပ်ခင် ဒေတာကို တဖြတ်စစ်တာ လုပ်ပြီး အခု မနက်မိုးလင်း ဆက်လုပ်နဲ့ ခုမှပဲ formal experiment ကို စလုပ်နိုင်ပါတယ်။  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ time python ./xgboost_ner.py --task train -i ./train.txt -m exp1_xgboost.model -f exp1_xgboost.feature
Read 0M words
Number of words:  2398
Number of labels: 0
Progress:  61.0% words/sec/thread:  192171 lr:  0.019512 avg.loss:  2.570059 ETA:   0h 0m Progress: 100.1% words/sec/thread:  147978 lr: -0.000026 avg.loss:  2.532439 ETA:   0h 0m Progress: 100.0% words/sec/thread:  147645 lr:  0.000000 avg.loss:  2.532439 ETA:   0h 0m 0s
FastText model saved to fasttext_model.bin
No NaN found in data
Traceback (most recent call last):
  File "./xgboost_ner.py", line 131, in <module>
    train_model(args.feature_filename, args.model_filename)
  File "./xgboost_ner.py", line 78, in train_model
    model.fit(X_train, y_train)
  File "/home/ye/anaconda3/envs/xgboost/lib/python3.8/site-packages/xgboost/core.py", line 729, in inner_f
    return func(**kwargs)
  File "/home/ye/anaconda3/envs/xgboost/lib/python3.8/site-packages/xgboost/sklearn.py", line 1467, in fit
    raise ValueError(
ValueError: Invalid classes inferred from unique values of `y`.  Expected: [ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23
 24 25 26 27 28 29 30 31 32], got [ 0  1  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24
 25 26 27 28 29 30 31 32 33]

real    0m20.510s
user    0m14.985s
sys     0m5.318s
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

I got above Error Message!  
အထက်မှာ မြင်ရတဲ့အတိုင်းပါပဲ Error က ရှိတုန်းပါပဲ။  
ဒီတခါတော့ training data ထဲမှာ ရှိတဲ့ unique tag အရေအတွက်နဲ့ testing data ထဲမှာ ရှိနေတဲ့ unique tag အရေအတွက်က မတူတာကြောင့် error ပေးတာလို့ ထင်ပါတယ်။ တကယ်ကတော့ testing data မှာက ပါတဲ့ စာကြောင်းပေါ်မူတည်ပြီးတော့ training data ထဲက tag အရေအတွက်နဲ့ မတူတာမျိုးလည်း ရှိနိုင်ပါတယ်။ သို့သော် တကယ်တမ်း စာတမ်း ရေးဖို့အတွက်၊ ပြီးတော့ formal experiment လုပ်ချင်တာမို့လို့ test data ထဲမှာက training data ထဲကလိုပဲ သတ်မှတ်ထားတဲ့ tag အပြည့်အစုံ ပါစေချင်တာမို့လို့ training လုပ်တဲ့ python code ထဲမှာ တမင်တကာကို ထည့်စစ်ထားတာမို့လို့ပါ။ အဲဒီလိုမှ မလုတ်ရင် ကိုယ့်မော်ဒယ်က bias ဖြစ်နိုင်လို့ပါ။  

## Debugging xgboost Training Part

```
Unique Tags in the Training Data is as follows:  

   DATE: 1.13%
   EVENT: 0.15%
   LCO: 0.00%
   LOC: 2.31%
   NUM: 0.76%
   O: 93.75%
   ORG: 0.73%
   PER: 0.85%
   PRODUCT: 0.04%
   TIME: 0.28%
```
   
Unique Tags in the Testing Data is as follows:  

```
   DATE: 1.25%
   EVENT: 0.10%
   LOC: 2.03%
   NUM: 0.81%
   O: 94.04%
   ORG: 0.70%
   PER: 0.85%
   PRODUCT: 0.01%
   TIME: 0.21%
```

Training data မှာ အောက်ပါလိုမျိုး LCO ဆိုပြီး မှားရိုက်ထားတာတွေ့ခဲ့ ...  

```
ကယ်ဆယ်/O ရေး/O သမား/O များ/O သည်/O ပိုက်လော့/O ဝေလငါး/O ၁၃/S-NUM ကောင်/O တစ်/O အုပ်/O ကို/O အနောက်/B-LCO ဩစတြေးလျ/E-LOC ၊/O ပါသ်/S-LOC ၏/O တောင်ဘက်/O ၊/O ဘူဆယ်လ်တန်/S-LOC အနီး/O ဂျီအိုဂရပ်ဖီ/B-LOC ပင်လယ်အော်/E-LOC သမုဒ္ဒရာ/O ထဲ/O သို့/O ယနေ့/O ပြန်/O လွှတ်/O ခဲ့/O သည်/O ။/O
```

Manual ပြင်တာက remote နဲ့ လှမ်းသုံးနေတဲ့ server ပေါ်မှာက လုပ်လို့ အဆင်မပြေလို့ တကယ်တမ်းက local notebook ဆီကို ကော်ပီကူးပြင်ရတယ်။ ပြန်ပြင်ပြီးရင်တော့ server ပေါ်ကို ကော်ပီကူး ... practical လုပ်ရတဲ့ အခက်အခဲတွေပါ ...  

```
C:\Users\801680>scp Downloads\new_train.txt ye@10.222.41.24:/home/ye/exp/myNER/data/exp1/
ye@10.222.41.24's password:
new_train.txt                                           100% 2144KB 497.4KB/s   00:04
```

xgboost run မယ့် ဖိုလ်ဒါဆီကို ပြန် copy ကူး ...  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$ ls
10k_NER_draft_version1_KaungLwinThant.txt  original              train.txt
new_train.txt                              sample_200_sentences
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$ cp new_train.txt ../../xgboost/
(xgboost) ye@lst-gpu-3090:~/exp/myNER/data/exp1$ cd ../../xgboost/
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ mv new_train.txt train.txt
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

bi-LSTM run ဖို့အတွက် python script ဘာညာရေးထားတဲ့ ဖိုလ်ဒါဆီကိုလည်း copy ကူးထည့်ခဲ့ ...  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ cp train.txt ../bi-LSTM/
```

## Recheck the Corpus

updated corpus ကို ပြန်စစ်...  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ python ../data/analyze_NER_corpus.py ./train.txt
Analysis of './train.txt'
----------------------------------------
1. Number of sentences without named entities: 6788
2. Frequency of each tag:
   B-DATE: 514
   B-EVENT: 67
   B-LOC: 1061
   B-NUM: 161
   B-ORG: 305
   B-PER: 244
   B-PRODUCT: 19
   B-TIME: 124
   E-DATE: 514
   E-EVENT: 67
   E-LOC: 1060
   E-NUM: 161
   E-ORG: 306
   E-PER: 245
   E-PRODUCT: 19
   E-TIME: 124
   I-DATE: 399
   I-EVENT: 59
   I-LOC: 173
   I-NUM: 27
   I-ORG: 232
   I-PER: 19
   I-PRODUCT: 5
   I-TIME: 84
   O: 129123
   S-DATE: 123
   S-EVENT: 13
   S-LOC: 891
   S-NUM: 691
   S-ORG: 160
   S-PER: 669
   S-PRODUCT: 17
   S-TIME: 58
3. Distribution of each tag:
   B-DATE: 0.37%
   B-EVENT: 0.05%
   B-LOC: 0.77%
   B-NUM: 0.12%
   B-ORG: 0.22%
   B-PER: 0.18%
   B-PRODUCT: 0.01%
   B-TIME: 0.09%
   E-DATE: 0.37%
   E-EVENT: 0.05%
   E-LOC: 0.77%
   E-NUM: 0.12%
   E-ORG: 0.22%
   E-PER: 0.18%
   E-PRODUCT: 0.01%
   E-TIME: 0.09%
   I-DATE: 0.29%
   I-EVENT: 0.04%
   I-LOC: 0.13%
   I-NUM: 0.02%
   I-ORG: 0.17%
   I-PER: 0.01%
   I-PRODUCT: 0.00%
   I-TIME: 0.06%
   O: 93.75%
   S-DATE: 0.09%
   S-EVENT: 0.01%
   S-LOC: 0.65%
   S-NUM: 0.50%
   S-ORG: 0.12%
   S-PER: 0.49%
   S-PRODUCT: 0.01%
   S-TIME: 0.04%
```

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ python ../data/analyze_NER_corpus.py ./train.txt --format abstract
Analysis of './train.txt'
----------------------------------------
1. Number of sentences without named entities: 6788
2. Frequency of each tag:
   DATE: 1550
   EVENT: 206
   LOC: 3185
   NUM: 1040
   O: 129123
   ORG: 1003
   PER: 1177
   PRODUCT: 60
   TIME: 390
3. Distribution of each tag:
   DATE: 1.13%
   EVENT: 0.15%
   LOC: 2.31%
   NUM: 0.76%
   O: 93.75%
   ORG: 0.73%
   PER: 0.85%
   PRODUCT: 0.04%
   TIME: 0.28%

(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

Test data ကိုလည်း စစ်ကြည့်မယ်။ အောက်ပါအတိုင်း output က ...  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ python ../data/analyze_NER_corpus.py ./test.txt
Analysis of './test.txt'
----------------------------------------
1. Number of sentences without named entities: 744
2. Frequency of each tag:
   B-DATE: 56
   B-EVENT: 6
   B-LOC: 107
   B-NUM: 24
   B-ORG: 35
   B-PER: 26
   B-PRODUCT: 1
   B-TIME: 11
   E-DATE: 56
   E-EVENT: 6
   E-LOC: 107
   E-NUM: 24
   E-ORG: 35
   E-PER: 26
   E-PRODUCT: 1
   E-TIME: 11
   I-DATE: 60
   I-EVENT: 3
   I-LOC: 17
   I-NUM: 5
   I-ORG: 14
   I-TIME: 5
   O: 14002
   S-DATE: 14
   S-LOC: 71
   S-NUM: 67
   S-ORG: 20
   S-PER: 74
   S-TIME: 5
3. Distribution of each tag:
   B-DATE: 0.38%
   B-EVENT: 0.04%
   B-LOC: 0.72%
   B-NUM: 0.16%
   B-ORG: 0.24%
   B-PER: 0.17%
   B-PRODUCT: 0.01%
   B-TIME: 0.07%
   E-DATE: 0.38%
   E-EVENT: 0.04%
   E-LOC: 0.72%
   E-NUM: 0.16%
   E-ORG: 0.24%
   E-PER: 0.17%
   E-PRODUCT: 0.01%
   E-TIME: 0.07%
   I-DATE: 0.40%
   I-EVENT: 0.02%
   I-LOC: 0.11%
   I-NUM: 0.03%
   I-ORG: 0.09%
   I-TIME: 0.03%
   O: 94.04%
   S-DATE: 0.09%
   S-LOC: 0.48%
   S-NUM: 0.45%
   S-ORG: 0.13%
   S-PER: 0.50%
   S-TIME: 0.03%
```

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ python ../data/analyze_NER_corpus.py ./test.txt --format abstract
Analysis of './test.txt'
----------------------------------------
1. Number of sentences without named entities: 744
2. Frequency of each tag:
   DATE: 186
   EVENT: 15
   LOC: 302
   NUM: 120
   O: 14002
   ORG: 104
   PER: 126
   PRODUCT: 2
   TIME: 32
3. Distribution of each tag:
   DATE: 1.25%
   EVENT: 0.10%
   LOC: 2.03%
   NUM: 0.81%
   O: 94.04%
   ORG: 0.70%
   PER: 0.85%
   PRODUCT: 0.01%
   TIME: 0.21%

(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

## Training for xgboost

Finally, I can train ... 

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ time python ./xgboost_ner.py --task train -i ./train.txt -m exp1_xgboost.model -f exp1_xgboost.feature | tee exp1_training.log
Read 0M words
Number of words:  2398
Number of labels: 0
Progress:  60.3% words/sec/thread:  189776 lr:  0.019864 avg.loss:  2.577710 ETA:   0h 0m Progress: 100.1% words/sec/thread:  158477 lr: -0.000039 avg.loss:  2.553837 ETA:   0h 0m Progress: 100.0% words/sec/thread:  158282 lr:  0.000000 avg.loss:  2.553837 ETA:   0h 0m 0s
FastText model saved to fasttext_model.bin
No NaN found in data
Validation Results:
               precision    recall  f1-score   support

      B-DATE       0.62      0.57      0.59        95
     B-EVENT       0.25      0.06      0.10        17
       B-LOC       0.42      0.50      0.45       195
       B-NUM       0.10      0.03      0.04        40
       B-ORG       0.33      0.06      0.11        64
       B-PER       0.74      0.60      0.66        42
   B-PRODUCT       0.00      0.00      0.00         4
      B-TIME       0.44      0.33      0.38        21
      E-DATE       0.72      0.53      0.61        86
     E-EVENT       0.50      0.29      0.36        14
       E-LOC       0.59      0.73      0.65       193
       E-NUM       0.48      0.29      0.36        35
       E-ORG       0.50      0.12      0.20        57
       E-PER       0.83      0.33      0.47        58
      E-TIME       0.55      0.84      0.67        25
      I-DATE       0.55      0.23      0.33        69
     I-EVENT       0.00      0.00      0.00         6
       I-LOC       0.00      0.00      0.00        33
       I-NUM       0.00      0.00      0.00         7
       I-ORG       0.25      0.02      0.04        45
       I-PER       0.00      0.00      0.00         2
      I-TIME       0.00      0.00      0.00        14
           O       0.98      0.99      0.98     25894
      S-DATE       0.43      0.14      0.21        22
     S-EVENT       0.00      0.00      0.00         3
       S-LOC       0.51      0.36      0.42       180
       S-NUM       0.56      0.75      0.64       154
       S-ORG       0.65      0.38      0.48        39
       S-PER       0.84      0.39      0.53       120
   S-PRODUCT       0.00      0.00      0.00         3
      S-TIME       1.00      0.40      0.57        10

    accuracy                           0.96     27547
   macro avg       0.41      0.29      0.32     27547
weighted avg       0.95      0.96      0.95     27547

Model and label encoder saved to exp1_xgboost.model and exp1_xgboost.model.label_encoder

real    0m45.335s
user    12m59.195s
sys     0m4.948s
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

Training ရလဒ်က အထက်မှာ တွေ့ရတဲ့ အတိုင်းပါပဲ။  
ဒီနေရာမှာ label_encoder ဆိုတာက label dictionary ပါ။  

## Testing for xgboost approach

Testing command က အောက်ပါအတိုင်း ...  

```
python ./xgboost_ner.py -m ./exp1_xgboost.model -f ./exp1_xgboost.feature -t ./test.txt -o test.hyp --task test

(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ time python ./xgboost_ner.py -m ./exp1_xgboost.model -f ./exp1_xgboost.feature -t ./test.txt -o test.hyp --task test
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Model and label encoder loaded from ./exp1_xgboost.model and ./exp1_xgboost.model.label_encoder

Evaluation Results on Test Data:
              precision    recall  f1-score   support

      B-DATE       0.69      0.59      0.63        56
     B-EVENT       1.00      0.33      0.50         6
       B-LOC       0.38      0.46      0.41       107
       B-NUM       0.00      0.00      0.00        24
       B-ORG       0.00      0.00      0.00        35
       B-PER       0.81      0.81      0.81        26
   B-PRODUCT       0.00      0.00      0.00         1
      B-TIME       0.43      0.27      0.33        11
      E-DATE       0.58      0.50      0.54        56
     E-EVENT       0.33      0.17      0.22         6
       E-LOC       0.53      0.60      0.56       107
       E-NUM       0.33      0.08      0.13        24
       E-ORG       0.46      0.17      0.25        35
       E-PER       0.71      0.65      0.68        26
   E-PRODUCT       0.00      0.00      0.00         1
      E-TIME       0.57      0.73      0.64        11
      I-DATE       0.65      0.25      0.36        60
     I-EVENT       0.00      0.00      0.00         3
       I-LOC       1.00      0.06      0.11        17
       I-NUM       1.00      0.20      0.33         5
       I-ORG       0.00      0.00      0.00        14
       I-PER       0.00      0.00      0.00         0
      I-TIME       0.00      0.00      0.00         5
           O       0.98      0.99      0.98     14002
      S-DATE       0.22      0.14      0.17        14
       S-LOC       0.41      0.30      0.34        71
       S-NUM       0.42      0.63      0.51        67
       S-ORG       0.58      0.55      0.56        20
       S-PER       0.86      0.43      0.58        74
      S-TIME       1.00      0.20      0.33         5

    accuracy                           0.95     14889
   macro avg       0.47      0.30      0.33     14889
weighted avg       0.95      0.95      0.95     14889


real    0m10.422s
user    3m35.947s
sys     0m3.813s
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

