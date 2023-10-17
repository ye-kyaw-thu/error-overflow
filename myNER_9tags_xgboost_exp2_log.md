# myNER 9 Tags, XGBoost Experiment 2

ဒီတစ်ခါတော့ test set မှာ စာကြောင်းရေ တစ်ထောင် အတိဖြစ်အောင် ဒေတာကို update လုပ်ပြီး ပြန် run ထားတာပါ။  

## Bash Shell Script Preparation

Training data ကနေ နောက်ဆုံး တစ်ကြောင်းကို test data ထဲကို ရွှေ့ဖို့အတွက် shell script ကို အောက်ပါအတိုင်း ရေးခဲ့တယ်။  

```bash
#!/bin/bash

# Extract the last line of train.txt
last_line=$(tail -n 1 train.txt)

# Delete the last line from train.txt
sed -i '$d' train.txt

# Append the last line to test.txt
echo "$last_line" >> test.txt
```

run လို့ရအောင် chmod command နဲ့ executable file အဖြစ်ပြောင်း ...  

```
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$ chmod +x ./add_one_line_to_test_data.sh
```

## Make 1K Test Data

လက်ရှိ ရှိနေတဲ့ training, testing data ရဲ့ filesize က အောက်ပါအတိုင်း ...  

```
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$ wc {train,test}.txt
   9202  137734 2195960 train.txt
    999   14889  236610 test.txt
  10201  152623 2432570 total
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

bash shell script ကို run ...  

```
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$ ./add_one_line_to_test_data.sh
```

စာတမ်းရေးတဲ့အခါမှာ workshop မှာ စကားပြောတဲ့အခါမှာ အဆင်ပြေအောင်လို့ test data ကိုတော့ စာကြောင်းရေ တစ်ထောင်တိတိအဖြစ် ပြင်ဆင်တာ ပြီးသွားပြီ ...  

```
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$ wc {train,test}.txt
   9201  137697 2195376 train.txt
   1000   14925  237194 test.txt
  10201  152622 2432570 total
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

## Training Data Information

```
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$ head train.txt
ပစ္စည်း/O ကောင်း/O ဝယ်/O ချင်/O ရင်/O ဘယ်/O ကို/O သွား/O ရ/O မ/O လဲ/O ။/O
သူ/O ဟာ/O လူသတ်/O မှု/O ကို/O မြင်/O ခဲ့/O တယ်/O ။/O
ကျွန်တော်/O က/O ကြိုးစားပမ်းစား/O သီဆို/O နေ/O တဲ့/O အဆိုတော်/O ကို/O လက်ခုပ်သြဘာ/O ပေး/O ခဲ့/O တယ်/O ။/O
ဟုတ်ကဲ့/O ။/O ဧည့်ခန်း/O ပါ/O ။/O
ရှီအတ်/O အစ္စလာမ်/O တွင်/O ဂိုဏ်း/O ခွဲ/O များ/O များ/O စွာ/O ရှိ/O သည်/O ။/O
လက်မှတ်/O ရောင်းစက်/O က/O ဘယ်/O မှာ/O ရှိ/O ပါ/O သလဲ/O ။/O
သူ/O အခု/O ပဲ/O ထွက်သွား/O တယ်/O ။/O
သူ/O က/O ကျွန်တော့်/O စကား/O နဲ့/O ပတ်သက်/O လို့/O စိတ်ခု/O ပြီး/O စကား/O မ/O ပြော/O ဘူး/O ။/O
ထို/O ခေတ်/O အခါ/O လောက်/O တွင်/O ပင်/O အိန္ဒိယ/B-LOC ပြည်/E-LOC ၌/O ဗေဒ/O ကျမ်း/O ကြီး/O များ/O ပေါ်ထွန်း/O ခဲ့/O သည်/O ။/O
မိဘ/O တွေ/O က/O ပညာသင်/O သွား/O တဲ့/O သမီး/O ကိုယ့်/O နိုင်ငံ/O ကို/O ပြန်လာ/O မယ့်/O ရက်/O ကို/O လက်ချိုး/O စောင့်/O နေ/O တယ်/O ။/O
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

tail command နဲ့လည်း ရိုက်ထုတ်ကြည့်၊ နောက်ပိုင်း စာတမ်းရေးတဲ့အခါမှာ ဥပမာစာကြောင်းတွေအဖြစ် ပြချင်တဲ့အခါမှာလည်း အလွယ်တကူနဲ့ ကော်ပီကူးယူလို့ ရအောင်လို့ ...  

```
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$ tail ./train.txt
ကစားပွဲ/O ပထမ/O ပိုင်း/O တွင်/O ၄/S-NUM ဂိုး/O နှင့်/O ဖွင့်/O ခဲ့/O ပြီး/O ၊/O ညာ/O ဘက်/O တောင်ပံ/O ကစားသမား/O ဒန်ကိုလင်/S-PER သည်/O ဝေလာ/S-ORG အတွက်/O နှစ်/O ဂိုးသွင်း/O ခဲ့/O သည်/O ။/O
ကျူဗာ/S-LOC ၊/O ဆာဘီးရီးယား/S-LOC နှင့်/O ဘိုရပ်တီရာ/B-LOC မြို့/E-LOC အနီး/O တွင်/O လူ/O ၁ဝဝဝဝဝ/S-NUM မှာ/O ၇၇/S-NUM ယောက်/O နှင့်/O ၁၂ဝ/S-NUM ယောက်/O နှုန်း/O များ/O အထိ/O အသီးသီး/O ရှိ/O ကြ/O သည်/O ။/O
မြန်မာ/B-LOC နိုင်ငံ/E-LOC ၏/O မူးယစ်ဆေးဝါး/O ပြဿနာ/O သည်/O ပြည်တွင်း/O လက်နက်ကိုင်/O ပဋိပက္ခ/O များ/O နှင့်/O နက်နက်ရှိုင်းရှိုင်း/O ဆက်နွယ်/O ပတ်သက်/O သည့်/O ရှုပ်ထွေး/O လှ/O သော/O နောက်/O ခံ/O အခြေအနေ/O များ/O အရ/O ရောင်းဝယ်ဖောက်ကား/O မှု/O များ/O ကြီးထွား/O နေ/O ခဲ့/O သည်/O မှာ/O နှစ်/O ပေါင်း/O များ/O စွာ/O ကြာမြင့်/O ခဲ့/O ပြီ/O ဖြစ်/O ပါ/O သည်/O ။/O
မြောက်ကိုရီးယား/S-LOC အရေး/O တင်းမာ/O မှု/O ဆက်လက်/O ဖြစ်ပွား/O နေ/O တာ/O ကြောင်/O ဂျပန်/B-LOC နိုင်ငံ/I-LOC မြောက်ပိုင်း/E-LOC တွင်/O အမေရိကန်/S-LOC လုပ်/O F-A/B-PRODUCT ကိုယ်ပျောက်/I-PRODUCT တိုက်/I-PRODUCT လေယာဉ်/E-PRODUCT များ/O ဖြန်/O ကြက်/O ချ/O ထား/O ။/O
ကနေဒါ/B-LOC နိုင်ငံ/E-LOC သား/O ခံ/O ယူ/O ထား/O သော/O ယွမ်/S-PER က/O သူမ/O ကို/O လူဝင်မှုကြီးကြပ်ရေး/O က/O ညှာတာ/O မှု/O ပေး/O ခြင်း/O နဲ့/O ပြိုင်ပွဲ/O ရဲ့/O တိုင်းရင်းသား/O ဒေသ/O တွေ/O ၊/O သူမ/O ၏/O လူဝင်/O မှု/O သမိုင်း/O ကြောင်း/O ကို/O ဖော်ပြ/O ခဲ့/O သည်/O ။/O
ပြင်သစ်/S-LOC သည်/O နော်ဝေး/S-LOC ထက်/O ပို/O ၍/O အလှမ်းဝေး/O သော/O ဘာသာ/O ရေး/O နှင့်/O မ/O ဆိုင်/O သော/O လူ့/O အဖွဲ့အစည်း/O တစ်/O ခု/O ဖြစ်/O ပြီး/O ၊/O ပြင်သစ်/O လူမျိုး/O များ/O သည်/O ၎င်း/O တို့/O ၏/O တရားစွဲ/O ဆို/O မှု/O တွင်/O အလွန်/O အလှမ်းဝေး/O ကွာ/O သွား/O လိမ့်/O မည်/O ဟု/O မတ်သိစ်ဖို့စီ/S-PER သည်/O ပြော/O ခဲ့/O သည်/O ။/O
များ/O ပြား/O လှ/O သော/O မြို့/O ကြီး/O များ/O ၊/O အထူးသဖြင့်/O နယူးယော့ခ်/B-LOC မြို့တော်/E-LOC ၌/O ကွင်းစ်/S-LOC နှင့်/O စတတ်တန်/B-LOC ကျွန်း/E-LOC ရှိ/O အချို့/O နေ/O ရာ/O များ/O သည်/O ဇူလိုင်/B-DATE လ/E-DATE လယ်/O ၏/O အပူလှိုင်း/O ကျ/O ရောက်/O ချိန်/O မှ/O စတင်/O ၍/O လျှပ်စစ်ဓါတ်အား/O ပြတ်တောက်/O မှု/O များ/O ကြောင့်/O ကြိုးစား/O ရုန်းကန်/O လှုပ်ရှား/O နေ/O ကြ/O ရ/O သည်/O ။/O
ပြည်ပ/O နိုင်ငံ/O များ/O ၏/O ယဉ်ကျေး/O မှု/O များ/O စိမ့်ဝင်/O ပျံ့နှံ/O လာ/O ခြင်း/O ကို/O တိုက်ဖျက်/O ရန်/O မြောက်ကိုရီးယား/S-LOC က/O ပြီး/O ခဲ့/O သည့်/O နှစ်/O က/O ဥပဒေ/O သစ်/O တစ်/O ရပ်/O ပြဌာန်း/O ထား/O ပြီး/O ၎င်း/O ဥပဒေ/O အရ/O တောင်ကိုရီးယား/S-LOC ဇာတ်ကား/O ဗီဒီယို/O များ/O ဖြန့်ဝေ/O ပါ/O က/O သေဒဏ်/O အထိ/O အပြစ်/O ပေး/O နိုင်/O ပြီး/O ကြည့်ရှု/O လျှင်/O လည်း/O ထောင်ဒဏ်/O ၁၅/S-NUM နှစ်/O အထိ/O အပြစ်/O ပေး/O နိုင်/O သည်/O ။/O
ထို/O ရောဂါ/O ခံစား/O နေ/O ရ/O သူ/O များ/O မှ/O အနည်းဆုံး/O ၈၀/S-NUM ရာခိုင်နှုန်း/O သည်/O အခြား/O ဆေး/O များ/O အား/O ခံနိုင်ရည်/O ရှိ/O မှု/O ကို/O ပြသ/O ခဲ့/O ပြီး/O ပြီ/O ဖြစ်/O သည်/O ။/O
ဝီကီ/B-ORG နယူး/E-ORG မှ/O ပထမဆုံး/O ဖော်ပြ/O ခဲ့/O သည့်/O စုံစမ်း/O စစ်ဆေး/O ခြင်း/O တစ်/O ခု/O တွင်/O ဝီကီလိခ်/S-ORG က/O ယနေ့/O ဂွမ်တာနာမို/B-LOC စခန်း/E-LOC မှာ/O မြစ်ဝကျွန်းပေါ်/O စက်ရုံ/O များ/O အတွက်/O အဆင့်/O မီ/O သော/O လုပ်ငန်းစဉ်/O များ/O (/O အက်စ်အိုပီ/O )/O ကို/O ယင်း/O အကြောင်းအရာ/O ၏/O အခြား/O အခန်း/O တွင်/O ဖော်ပြ/O ထား/O သည်/O ။/O
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

## Test Data Information

check with head command ...  

```
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$ head test.txt
အပေါ်ထပ်/O မှာ/O ပြင်/O ထား/O ပါ/O တယ်/O ။/O လိုက်/O ပို့/O ပေး/O ပါ/O မယ်/O ။/O
လွယ်/O တဲ့/O စကား/O တွေ/O ရှိ/O သလို/O ခက်ခဲ/O တဲ့/O စကား/O လည်း/O ရှိ/O တာ/O သဘာဝ/O ပဲ/O ။/O
သခင်/B-PER အောင်ဆန်း/E-PER သည်/O ကိုယ်ခန္ဓာ/O ညှက်/O ပြီး/O အားကောင်း/O သန်မာ/O လှ/O ခြင်း/O မ/O ရှိ/O သော်လည်း/O တိုက်ရေးခိုက်ရေး/O ကျွမ်းကျင်/O ကာ/O သတ္တိ/O ရှိ/O ၍/O အပင်ပန်း/O ခံ/O နိုင်/O သော/O စစ်သား/O တစ်/O ဦး/O ဖြစ်/O လာ/O ၏/O ။/O
အရင်/O တုန်း/O က/O သူ/O မကြာခဏ/O အလည်လာ/O လေ့/O ရှိ/O ပေမဲ့/O အခုတလော/O တော့/O လုံးဝ/O သူ့/O မျက်နှာ/O ကို/O မ/O မြင်/O ရ/O ဘူး/O ။/O
ဥပဒေ/O အရ/O ထိမ်းမြား/O ခြင်း/O ဖြင့်/O ဖြစ်စေ/O အခြား/O နည်း/O ဖြင့်/O ဖြစ်စေ/O မွေးဖွား/O သော/O ကလေး/O အားလုံး/O သည်/O တူညီ/O သော/O လူမှု/O ကာကွယ်/O စောင့်ရှောက်/O ရေး/O ကို/O ရယူ/O ခံစား/O ကြ/O ရ/O မည်/O ။/O
စျေး/O က/O နေ/O အဝတ်/O ဝယ်/O ပါ/O တယ်/O ။/O
အခု/O ဘာ/O တွေ/O များ/O ပြ/O နေ/O သလဲ/O ။/O
ဝမ်/O ၅/B-NUM သောင်း/E-NUM လောက်/O ကလေး/O ဘဲ/O စု/O ခဲ့/O တယ်/O ။/O
ကျွန်တော်/O လည်း/O နေ့လယ်/O က/O ကိုဇော်နိုင်/S-PER နဲ့/O တွေ့/O လို့/O ဒေါ်ဒေါ်/O နေမကောင်းမှန်း/O သိ/O ရ/O တာ/O ။/O
ကျွန်တော်/O က/O သူငယ်ချင်း/O ပုံပြော/O တာ/O ခံ/O လိုက်/O ရ/O လို့/O စိတ်တို/O နေ/O တယ်/O ။/O
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

tail command ...  

```
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$ tail test.txt
တောင်/O ပေါ်/O က/O နေ/O အနောက်ဘက်/O မျှော်/O ကြည့်/O လိုက်/O ရင်/O တိမ်ဖြူ/O မိုးပြာ/O အောက်/O မှာ/O မြစမ်းတောင်/S-LOC ပေါ်/O က/O စေတီတော်/O ကို/O ကောင်းကောင်း/O မြင်/O ရ/O ပါ/O တယ်/O ။/O
နားလည်/O ပါ/O တယ်/O ။/O
သူ/O စာတိုက်/O မှ/O ပြန်လာ/O လိမ့်/O မယ်/O ။/O
သစ်ပင်/O က/O နေ/O ပြုတ်ကျ/O နေ/O ဦး/O မယ်/O ။/O
ပြီး/O ခဲ့/O တဲ့/O အခေါက်/O က/O ပေး/O လိုက်/O တဲ့/O ဆေး/O ကျွန်တော့်/O အတွက်/O အရာမရောက်/O သလို/O ပဲ/O ။/O
ဒီ/O အညိုရောင်/O လေး/O ပြော/O တာ/O လား/O ။/O
ညှပ်/O ပြီး/O ရိတ်/O ပေး/O ပါ/O ။/O
ပူတောင်း/O ဆို/O သည်/O မှာ/O ရှမ်း/O ဘာသာ/O အားဖြင့်/O ပူ/O အဘိုး/O ၊/O တောင်း/O စောင့်/O သည်/O အဘိုး/O မျှော်/O မြို့/O ဟု/O အဓိပ္ပါယ်ရ/O သည်/O ။/O
အဲဒီ/O လူ/O ရဲ့/O စကား/O က/O တချက်/O မှ/O မ/O မှား/O ဘူး/O ။/O
အတော်/O ပါ/O ပဲ/O ။/Oဒါပေမဲ့/O အမှန်/O မှာ/O သူ/O တို့/O သည်/O ဘာသာ/O ရေး/O သမား/O များ/O ဖြစ်/O တယ်/O လို့/O ဒင်ဗာ/S-LOC ၏/O ဘာသာ/O ရေး/O လေ့လာ/O မှု/O တက္ကသိုလ်/O ပါမောက္ခ/B-PER ကားရပ်ချက်ခ်/E-PER က/O ဝေါစထရစ်/B-ORG ဂျာနယ်/E-ORG မှ/O ကြေညာ/O ချက်/O တစ်/O ခု/O ထဲ/O မှာ/O ဖော်ပြ/O ထား/O ပါ/O တယ်/O ။/O
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

## Checking Tag Distributions for Training Data 

python code for tag distributions, frequency analysis ...  

```python
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$ cat ../data/analyze_NER_corpus.py
## Written by Ye, LU Lab., Myanmar
## for checking NER tagged data
## Last updated: 28 Sept 2023

import sys
import argparse

def analyze_corpus(filename, format_option):
    # Initialize counters and dictionaries
    sentences_without_entities = 0
    tag_frequency = {}
    total_tags = 0

    # Open and read the corpus file line by line
    with open(filename, 'r', encoding='utf-8') as file:
        for line in file:
            line = line.strip()
            if not line:
                continue  # skip empty lines

            tags = [token.split('/')[-1] for token in line.split()]

            if format_option == "abstract":
                # Converting the B, I, E and S tags to the general category
                #tags = ['O' if tag == 'O' else tag.split('-')[1] for tag in tags]
                tags = ['O' if tag == 'O' else (tag.split('-')[1] if '-' in tag else 'UNKNOWN') for tag in tags]


            unique_tags = set(tags)

            # Check if only the O tag is present in the sentence
            if unique_tags == {'O'}:
                sentences_without_entities += 1

            # Count the frequency of each tag
            for tag in tags:
                tag_frequency[tag] = tag_frequency.get(tag, 0) + 1
                total_tags += 1

    # Generate the report
    report = f"Analysis of '{filename}'\n"
    report += "-" * 40 + "\n"
    report += f"1. Number of sentences without named entities: {sentences_without_entities}\n"
    report += "2. Frequency of each tag:\n"
    for tag, count in sorted(tag_frequency.items()):
        report += f"   {tag}: {count}\n"
    report += "3. Distribution of each tag:\n"
    for tag, count in sorted(tag_frequency.items()):
        percentage = (count / total_tags) * 100
        report += f"   {tag}: {percentage:.2f}%\n"

    return report

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description='Analyze NER tagged data.')
    parser.add_argument('filename', type=str, help='Path to the input file.')
    parser.add_argument('-f', '--format', type=str, choices=['abstract', 'detailed'], default='detailed', help='Output format. "abstract" to consider all B, I, E, S tags as one tag; "detailed" for detailed tags.')

    args = parser.parse_args()

    result = analyze_corpus(args.filename, args.format)
    print(result)

(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

for the training data ... 

```
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$ python ../data/analyze_NER_corpus.py ./train.txt
Analysis of './train.txt'
----------------------------------------
1. Number of sentences without named entities: 6788
2. Frequency of each tag:
   B-DATE: 514
   B-EVENT: 67
   B-LOC: 1061
   B-NUM: 161
   B-ORG: 304
   B-PER: 243
   B-PRODUCT: 19
   B-TIME: 124
   E-DATE: 514
   E-EVENT: 67
   E-LOC: 1060
   E-NUM: 161
   E-ORG: 305
   E-PER: 244
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
   O: 129091
   S-DATE: 123
   S-EVENT: 13
   S-LOC: 890
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

(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

S, B, I, E ဆိုတဲ့ အပိုင်းတွေမပါပဲ analysis လုပ်ကြည့်ချင်လို့ --format option ကို abstract အဖြစ်ထားပြီး run ကြည့်ခဲ့ ...  

```
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$ python ../data/analyze_NER_corpus.py ./train.txt --format abstract
Analysis of './train.txt'
----------------------------------------
1. Number of sentences without named entities: 6788
2. Frequency of each tag:
   DATE: 1550
   EVENT: 206
   LOC: 3184
   NUM: 1040
   O: 129091
   ORG: 1001
   PER: 1175
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

```

## Checking Tag Distributions for the Test Data

S, B, I, E တွေပါ အပါအဝင် ...  

```
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$ python ../data/analyze_NER_corpus.py ./test.txt
Analysis of './test.txt'
----------------------------------------
1. Number of sentences without named entities: 743
2. Frequency of each tag:
   B-DATE: 56
   B-EVENT: 6
   B-LOC: 107
   B-NUM: 24
   B-ORG: 36
   B-PER: 27
   B-PRODUCT: 1
   B-TIME: 11
   E-DATE: 56
   E-EVENT: 6
   E-LOC: 107
   E-NUM: 24
   E-ORG: 36
   E-PER: 27
   E-PRODUCT: 1
   E-TIME: 11
   I-DATE: 60
   I-EVENT: 3
   I-LOC: 17
   I-NUM: 5
   I-ORG: 14
   I-TIME: 5
   O: 14033
   S-DATE: 14
   S-LOC: 72
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
   B-PER: 0.18%
   B-PRODUCT: 0.01%
   B-TIME: 0.07%
   E-DATE: 0.38%
   E-EVENT: 0.04%
   E-LOC: 0.72%
   E-NUM: 0.16%
   E-ORG: 0.24%
   E-PER: 0.18%
   E-PRODUCT: 0.01%
   E-TIME: 0.07%
   I-DATE: 0.40%
   I-EVENT: 0.02%
   I-LOC: 0.11%
   I-NUM: 0.03%
   I-ORG: 0.09%
   I-TIME: 0.03%
   O: 94.02%
   S-DATE: 0.09%
   S-LOC: 0.48%
   S-NUM: 0.45%
   S-ORG: 0.13%
   S-PER: 0.50%
   S-TIME: 0.03%

```

sub-tag တွေ မပါပဲ distribution ကို စစ်ကြည့်ခဲ့ ...  

```
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$ python ../data/analyze_NER_corpus.py ./test.txt --format abstract
Analysis of './test.txt'
----------------------------------------
1. Number of sentences without named entities: 743
2. Frequency of each tag:
   DATE: 186
   EVENT: 15
   LOC: 303
   NUM: 120
   O: 14033
   ORG: 106
   PER: 128
   PRODUCT: 2
   TIME: 32
3. Distribution of each tag:
   DATE: 1.25%
   EVENT: 0.10%
   LOC: 2.03%
   NUM: 0.80%
   O: 94.02%
   ORG: 0.71%
   PER: 0.86%
   PRODUCT: 0.01%
   TIME: 0.21%

(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

အကြမ်းစစ်ကြည့်ခဲ့တာ experiment လုပ်ဖို့ အဆင်ပြေပြီလို့ assumption လုပ်ပြီး train, test လုပ်မယ်။ Workshop အတွက် draft paper ရေးပြီးနောက်ပိုင်းမှပဲ ကောင်းလွင်သန့်နဲ့ corpus တစ်ခုလုံးကို update လုပ်ရင်း ပြန်စစ်ကြည့်မယ် စိတ်ကူးခဲ့ ...  

## Backup

ပထမဆုံး စမ်းခဲ့တဲ့ စာကြောင်းရေ 999 ကြောင်း test-data နဲ့ experiment ဖိုင်တွေကို backup ကူးထားခဲ့ ...  


```
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost/bk$ mkdir 999_testdata
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost/bk$ cd ..
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$ mv exp1_* ./bk/999_testdata/
```

## XGBoost Training 

Anaconda environment ကို change ...  

```
(base) ye@lst-gpu-3090:~/exp/myNER/xgboost$ conda activate xgboost
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

Training and Validation Result is as follows:  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ time python ./xgboost_ner.py --task train --input_corpus train.txt --feature_filename exp1_features.csv --model_filename model.xgb
Read 0M words
Number of words:  2398
Number of labels: 0
Progress:  60.5% words/sec/thread:  191438 lr:  0.019725 avg.loss:  2.566964 ETA:   0h 0m Progress: 100.0% words/sec/thread:  158717 lr: -0.000017 avg.loss:  2.537227 ETA:   0h 0m Progress: 100.0% words/sec/thread:  158493 lr:  0.000000 avg.loss:  2.537227 ETA:   0h 0m 0s
FastText model saved to fasttext_model.bin
No NaN found in data
Validation Results:
               precision    recall  f1-score   support

      B-DATE       0.63      0.53      0.58        98
     B-EVENT       1.00      0.07      0.12        15
       B-LOC       0.41      0.49      0.45       183
       B-NUM       0.00      0.00      0.00        21
       B-ORG       0.25      0.04      0.07        50
       B-PER       0.58      0.54      0.56        39
   B-PRODUCT       0.00      0.00      0.00         3
      B-TIME       0.28      0.28      0.28        18
      E-DATE       0.76      0.56      0.64        95
     E-EVENT       0.44      0.31      0.36        13
       E-LOC       0.61      0.67      0.64       211
       E-NUM       0.65      0.33      0.43        40
       E-ORG       0.41      0.16      0.23        57
       E-PER       0.82      0.49      0.61        55
   E-PRODUCT       0.00      0.00      0.00         3
      E-TIME       0.63      0.82      0.71        33
      I-DATE       0.64      0.33      0.44        84
     I-EVENT       0.00      0.00      0.00        11
       I-LOC       0.00      0.00      0.00        36
       I-NUM       0.00      0.00      0.00         4
       I-ORG       0.33      0.02      0.04        47
       I-PER       0.00      0.00      0.00         3
   I-PRODUCT       0.00      0.00      0.00         2
      I-TIME       0.00      0.00      0.00        15
           O       0.98      0.99      0.98     25860
      S-DATE       0.40      0.22      0.29        27
     S-EVENT       0.00      0.00      0.00         1
       S-LOC       0.55      0.36      0.43       184
       S-NUM       0.55      0.73      0.63       135
       S-ORG       0.58      0.34      0.43        32
       S-PER       0.84      0.36      0.50       147
   S-PRODUCT       0.50      0.25      0.33         4
      S-TIME       0.86      0.43      0.57        14

    accuracy                           0.96     27540
   macro avg       0.41      0.28      0.31     27540
weighted avg       0.95      0.96      0.95     27540

Model and label encoder saved to model.xgb and model.xgb.label_encoder

real    0m52.125s
user    13m33.657s
sys     0m5.465s
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

Some file information:  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ ls
10k_NER_draft_version1_KaungLwinThant.txt  note.txt
bk                                         running_log_7Oct2023.txt
chk_features.py                            test.hyp
exp1_features.csv                          test.txt
fasttext_model.bin                         train_test.sh
feature_importance_plot.png                train.txt
features.csv                               t-SNE_visualization.py
model.xgb                                  xgboost_ner.py
model.xgb.label_encoder
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

## XGBoost Testing

Testing with 1K test data. The result is as follows:  

```
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$ time python ./xgboost_ner.py --task test --test_filename test.txt --model_filename model.xgb --feature_filename exp1_features.csv --output_filename test.hyp
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Model and label encoder loaded from model.xgb and model.xgb.label_encoder

Evaluation Results on Test Data:
              precision    recall  f1-score   support

      B-DATE       0.65      0.55      0.60        56
     B-EVENT       1.00      0.17      0.29         6
       B-LOC       0.39      0.48      0.43       107
       B-NUM       0.00      0.00      0.00        24
       B-ORG       0.00      0.00      0.00        36
       B-PER       0.81      0.78      0.79        27
   B-PRODUCT       0.00      0.00      0.00         1
      B-TIME       0.30      0.27      0.29        11
      E-DATE       0.58      0.50      0.54        56
     E-EVENT       0.33      0.17      0.22         6
       E-LOC       0.53      0.60      0.56       107
       E-NUM       0.50      0.17      0.25        24
       E-ORG       0.43      0.17      0.24        36
       E-PER       0.72      0.67      0.69        27
   E-PRODUCT       0.00      0.00      0.00         1
      E-TIME       0.57      0.73      0.64        11
      I-DATE       0.62      0.27      0.37        60
     I-EVENT       0.00      0.00      0.00         3
       I-LOC       1.00      0.06      0.11        17
       I-NUM       1.00      0.20      0.33         5
       I-ORG       0.00      0.00      0.00        14
      I-TIME       0.00      0.00      0.00         5
           O       0.98      0.99      0.98     14033
      S-DATE       0.29      0.29      0.29        14
       S-LOC       0.40      0.35      0.37        72
       S-NUM       0.46      0.70      0.55        67
       S-ORG       0.58      0.55      0.56        20
       S-PER       0.87      0.46      0.60        74
      S-TIME       1.00      0.20      0.33         5

    accuracy                           0.95     14925
   macro avg       0.48      0.32      0.35     14925
weighted avg       0.95      0.95      0.95     14925


real    0m7.052s
user    1m48.252s
sys     0m4.372s
(xgboost) ye@lst-gpu-3090:~/exp/myNER/xgboost$
```

## Prepared Training/Testing/Feature_Extration Bash Script

နောက်ပိုင်း experiment တွေအတွက် shell script ပြင်ထားတာကိုလည်း update လုပ်ခဲ့ ...  
filename: train_test.sh  

```bash
#!/bin/bash

# Function for training
train_model() {
    echo "Training..."
    time python ./xgboost_ner.py --task train --input_corpus train.txt --feature_filename exp1_features.csv --model_filename model.xgb
}

# Function for testing
test_model() {
    echo "Testing..."
    time python ./xgboost_ner.py --task test --test_filename test.txt --model_filename model.xgb --feature_filename exp1_features.csv --output_filename test.hyp

    # Check the hyp file
    echo "Check the tagged output or hyp file"
    #shuf ./test.hyp | head -n 50
    paste -d "\n" ./test.txt ./test.hyp | head -n 50
}

# Function for building fasttext model only
build_fasttext_model() {
    echo "Building FastText model task"
    time python ./xgboost_ner.py --task build_fasttext --input_corpus ./train.txt --feature_filename fasttext_features.csv
}

# Check command-line arguments
if [ "$#" -ne 1 ]; then
    echo "Usage: $0 {train|test|build_fasttext}"
    exit 1
fi

# Run the requested task
case $1 in
    train)
        train_model
        ;;
    test)
        test_model
        ;;
    build_fasttext)
        build_fasttext_model
        ;;
    *)
        echo "Unknown task: $1"
        echo "Usage: $0 {train|test|build_fasttext}"
        exit 1
        ;;
esac


```

## To Do List

- လက်ရှိ ရေးထားတဲ့ XGBoost python script ကို ပြန်စစ်ရန်၊ update လုပ်ရန်
- Manual Error Analysis လုပ်ရန်

