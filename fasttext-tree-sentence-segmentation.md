# Developing Log for Fasttext-Tree Sentence Segmenter  
Last updated: 6 Dec 2024  
By Ye Kyaw Thu, Visiting Professor, LST, NECTEC, Thailand.  

## Test Run  

```
$ time python ./fasttext-tree.py --train ./data/train-valid.tagged | tee ./training1.log
Read 0M words
Number of words:  10221
Number of labels: 0
Progress: 100.0% words/sec/thread:   25942 lr:  0.000000 avg.loss:  2.138484 ETA:   0h 0m 0s
Loading training data...
Training FastText model...
Preparing features...
Training Decision Tree model...
Saving trained model to decision_tree_model.pkl...
Training completed.

real    1m32.433s
user    4m29.194s
sys     0m5.923s
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python fasttext-tree.py --test ./data/test.tagged --evaluate
Loading tagged test data...
Loading FastText and Decision Tree models...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Preparing features...
Predicting...
Evaluating...
              precision    recall  f1-score   support

           B       0.55      0.34      0.42      6779
           E       0.73      0.79      0.76      6860
           N       0.57      0.35      0.44     18956
           O       0.77      0.89      0.83     64037

    accuracy                           0.74     96632
   macro avg       0.66      0.59      0.61     96632
weighted avg       0.72      0.74      0.72     96632


real    0m3.513s
user    0m5.701s
sys     0m4.656s
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ python ./fasttext-tree.py --real-time "ဗိုက်နာပြီ အထူးသဖြင့် ဝမ်းဗိုက်ညာဘက်အောက်ပိုင်းက နာပြီဆိုရင် အူအတက်ရောင်တာများလားလို့ တွေးတတ်ကြပါတယ်။ ဝမ်းဗိုက်ထဲမှာ ကလီစာ အများကြီး ရှိတဲ့အတွက် ဗိုက်အောင့်တိုင်း အူအတက်ရောင်တာ မဟုတ်ပါဘူး။ မှားတတ်ကြတာတော့ လေနာတာနဲ့ အူအတက်ရောင်တာနဲ့ မှားတတ်ကြပါတယ်။ ဒါကြောင့် ဗိုက်အောင့်တာက အူအတက်ကြောင့်လား၊ လေနာတာကြောင့်လားဆိုတာ အကြမ်းဖျင်း ခွဲကြည့်ရအောင်။"
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
ဗိုက်နာပြီ/O အထူးသဖြင့်/O ဝမ်းဗိုက်ညာဘက်အောက်ပိုင်းက/O နာပြီဆိုရင်/O အူအတက်ရောင်တာများလားလို့/B တွေးတတ်ကြပါတယ်။/O ဝမ်းဗိုက်ထဲမှာ/O ကလီစာ/O အများကြီး/N ရှိတဲ့အတွက်/O ဗိုက်အောင့်တိုင်း/O အူအတက်ရောင်တာ/N မဟုတ်ပါဘူး။/O မှားတတ်ကြတာတော့/O လေနာတာနဲ့/B အူအတက်ရောင်တာနဲ့/N မှားတတ်ကြပါတယ်။/O ဒါကြောင့်/B ဗိုက်အောင့်တာက/O အူအတက်ကြောင့်လား၊/O လေနာတာကြောင့်လားဆိုတာ/O အကြမ်းဖျင်း/O ခွဲကြည့်ရအောင်။/N
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

```
အဆင့်/B အေ/O ဝင်ငွေခွန်/O ကို/O လစာ/N မှ/N ဖြတ်တောက်/N သည်/E
လိုကီ/B က/O အတ်/O ဂါဒါ/O လိုကီ/O ရဲ့/O မျက်လုံး/O တွေ/O ကို/O သေချာ/O တည့်တည့်/O ကြည့်/O ရင်း/N ငါ/N က/N လိုကီ/E

အဆင့် အေ ဝင်ငွေခွန် ကို လစာ မှ ဖြတ်တောက် သည် လိုကီ က အတ် ဂါဒါ လိုကီ ရဲ့ မျက်လုံး တွေ ကို သေချာ တည့်တည့် ကြည့် ရင်း ငါ က လိုကီ
```

```
$ python ./fasttext-tree.py --real-time "အဆင့် အေ ဝင်ငွေခွန် ကို လစာ မှ ဖြတ်တောက် သည် လိုကီ က အတ် ဂါဒါ လိုကီ ရဲ့ မျက်လုံး တွေ ကို သေချာ တည့်တည့် ကြည့် ရင်း ငါ က လိုကီ"
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
အဆင့်/O အေ/O ဝင်ငွေခွန်/O ကို/O လစာ/O မှ/O ဖြတ်တောက်/O သည်/E လိုကီ/O က/O အတ်/O ဂါဒါ/O လိုကီ/O ရဲ့/O မျက်လုံး/O တွေ/O ကို/O သေချာ/O တည့်တည့်/O ကြည့်/O ရင်း/O ငါ/O က/O လိုကီ/O
```

## Syllable Breaking

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data/syl/original$ python sylbreak.py -i train.my -o train.syl -s " "
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data/syl/original$ python sylbreak.py -i valid.my -o valid.syl -s " "
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data/syl/original$ python sylbreak.py -i test.my -o test.syl -s " "
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data/syl/original$
```

Check ... 

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data/syl/original$ head train.syl
နား လည် ပါ ပြီ
ဈေး က များ လှ ချေ လား
သူ ဒီ နေ့ နည်း နည်း ပင် ပန်း နေ တယ် ထင် တယ်
ဘာ ကြောင့် လဲ ဆို စမ်း ပါ ဦး
စိတ် ကောက် တဲ့ စ ကား မျိုး ပြော ပြန် ပြီ
၁ ၆ ရာ စု နှစ် တွင် ရော မ ပန်း ချီ ကျော် က ဝိ လီ ယို နာ ဒို ဒါ ဗင်း ချိ က ပင် လယ် ခ ရု များ ရှိ ရာ လက် ရှိ ကုန်း မြင့် များ သည် တစ် ကြိမ် က ပင် လယ် အောက် တွင် ရှိ ခဲ့ ၍ နောက် မှ မြေ မြင့် တက် လာ ခဲ့ ခြင်း ဖြစ် သည် ဟု တွေး ယူ ခဲ့ ဖူး လေ သည်
ဂင်မ် ချီ သိပ် ပြီး နောက် ဂင်မ် ချီ အိုး ကို မြေ ကြီး ထဲ မြုပ် လိုက် တယ်
အ အေး မိ မယ်
ဧ ည့် လမ်း ညွှန် ရော ထ ည့် ပေး လို့ ရ လား
မှန် တင် ခုံ ဘေး က အ ရက် ပု လင်း ကို ထုတ် ယူ လိုက် ရင်း ကောက် မော့ လိုက် သည် ပု လင်း ပြန် အ သိမ်း မှာ အ ပြာ ရောင် ဝတ် စုံ ကို မြင် လိုက် ရ သည်
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data/syl/original$
```

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data/syl/original$ head valid.syl
သူ ဘယ် သူ နဲ့ အ ရင်း နှီး ဆုံး လဲ
ဒီ က နေ ရှေ့ ကို တည့် တည့် သွား မီး ပွိုင့် တွေ့ ရင် ဘယ် ဘက် ကွေ့ ၂ မှတ် တိုင် ဆက် လက် သွား ရင် ရောက် ပါ လိမ့် မယ်
ရေ ခဲ မ ပါ ဘဲ နဲ့
နောက် တော့ အဲ ဒီ အ ဆောက် အ ဦ ကို ကမ္ဘာ့ အ လယ် ဗ ဟို ချက် လို့ သတ် မှတ် လာ ကြ တယ် ။
ဒီ ဟာ က တော့ လူ ကြီး မင်း အ ခန်း အ တွက် မီ နူး ပါ အ ချိန် နဲ့ စား ချင် တဲ့ ဟင်း လျာ ကို မှတ် လိုက် ပါ ပြီး ရင် မီ နူး ကို တံ ခါး ရဲ့ အ ပြင် ဘက် မှာ ချိတ် ထား လိုက် ပါ
အာ မ ခံ လုပ် ငန်း ထွန်း ကား ရေး ဟာ စီး ပွား ရေး ဖွံ့ ဖြိုး တိုး တက် မှု နဲ့ ဆိုင် ပါ တယ် မြန် မာ ပြည် စီး ပွား ရေး ဖွံ့ ဖြိုး လာ တာ နဲ့ အ မျှ မြန် မာ ပြည် ရဲ့ အာ မ ခံ လုပ် ငန်း လည်း ထွန်း ကား လာ ပါ လိမ့် မယ်
ခင် ဗျား ဟို တစ် ခါ ရိတ် သွား တာ မေ့ ပြီး ပေး မ သွား ဘူး လေ တဲ့
ဒီ နေ့ ဆို ရင် ပ ထ မ နှစ် ရဲ့ ဒု တိ ယ ပ ညာ သင် ကာ လ သင် တန်း ပြီး လို့ နွေ ရာ သီ ကျောင်း ပိတ် ရက် ကို ဝင် လာ ပြီ
ကျွန် တော် သိ ပါ ပြီ
ဂ လူး ကို့စ် က အ ချို ဓာတ် ပြ ည့် ဝ စေ တဲ့ ဓာတ် တစ် မျိုး ပါ အ စား အ စာ တွေ ထဲ မှာ ပါ တဲ့ အ ချို ဓာတ် တစ် မျိုး ပေါ့ ခန္ဓာ ကိုယ် မှာ ရှိ တဲ့ ဆဲလ် အ များ စု က အ မိုင် နို အက် ဆစ် နဲ့ အ တူ ဂ လူး ကို့စ် ကို အ သုံး ပြု ပြီး စွမ်း အင် ရ ရှိ စေ ဖို့ လုပ် ဆောင် ပေး ပါ တယ်
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data/syl/original$
```

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data/syl/original$ head test.syl
ရင် ဘတ် အော င့် လာ ရင် သ တိ ထား ပါ
ဘယ် လောက် နောက် ကျ သ လဲ
ကြို ပို့ ဘတ်စ် ကား က အ ဆင် အ ပြေ ဆုံး ပဲ
အဲ ဒီ အ ဖွဲ့ ရဲ့ ဥက္ကဋ္ဌ ဖြစ် တဲ့ ယို ကို ယာ မာ့ အာ ကိ ဟီ တို Y o k o y a m a A k i h i t o က တ ခြား နိုင် ငံ တွေ မှာ ဖြစ် ပွား တဲ့ လူ နာ တွေ ရဲ့ အ ဆုတ် လုပ် ဆောင် ပုံ တွေ က ဗိုင်း ရပ်စ် ကူး စက် ခံ ရ ပြီး ကု သ လိုက် လို့ ရော ဂါ ပိုး မ ရှိ တော့ ဘူး လို့ စစ် ဆေး ပြီး နောက် မှာ တောင် မှ အ ဆုတ် က အ ပြည့် အ ဝ ပုံ မှန် ပြန် ဖြစ် မ လာ တဲ့ လူ နာ တွေ အ များ အ ပြား တွေ့ ရ တယ် လို့ ပြော ပါ တယ်
အ ဆ င့် အေ ဝင် ငွေ ခွန် ကို လ စာ မှ ဖြတ် တောက် သည်
လို ကီ က အတ် ဂါ ဒါ လို ကီ ရဲ့ မျက် လုံး တွေ ကို သေ ချာ တ ည့် တ ည့် ကြ ည့် ရင်း ငါ က လို ကီ
ခင် ဗျား ကြိုက် တဲ့ အ ရောင် က ဘာ လဲ
သူ သီ ချင်း ဆို တတ် သ လို က လည်း က တတ် သည်
ထို့ ကြောင့် ဥ ပါယ် ဂို့ ဟု ခေါ် ကာ ကာ လ ကြာ သော် ဥ ပါယ် ဂို့ မှ ပ ဂိုး ဟု ပြောင်း လဲ ခေါ် လာ ကြ သည်
ဒီ နေ့ ခင် ဗျား ဘယ် လို ဖြစ် နေ တာ လဲ
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data/syl/original$
```

သေချာ ပြန်စဉ်းစားကြည့်တော့ untagged data ကနေ syllable ဖြတ်ပြီးမှ auto tagging လုပ်တာက sentence level အတွက် အိုကေပေမဲ့ paragraph level tagging အတွက်က auto tagging က အဆင်မပြေဘူး။  

အဲဒါကြောင့် လက်ရှိ tagged လုပ်ပြီးသား ဒေတာတွေကနေပဲ syllable ဖြတ်နိုင်မှ အဆင်ပြေလိမ့်မယ်။  

## Python Code for Converting Word-Tagged to Syllable-Tagged 

```
$ head train-valid.tagged
နားလည်/B ပါ/N ပြီ/E
ဈေး/B က/O များ/N လှ/N ချေ/N လား/E
သူ/B ဒီ/O နေ့/O နည်းနည်း/O ပင်ပန်း/O နေ/N တယ်/N ထင်/N တယ်/E
ဘာ/B ကြောင့်/O လဲ/O ဆို/N စမ်း/N ပါ/N ဦး/E
စိတ်ကောက်/B တဲ့/O စကား/O မျိုး/N ပြော/N ပြန်/N ပြီ/E
၁၆/B ရာစုနှစ်/O တွင်/O ရောမ/O ပန်းချီကျော်/O က/O ဝိလီယိုနာဒိုဒါဗင်းချိ/O က/O ပင်လယ်/O ခရု/O များ/O ရှိ/O ရာ/O လက်ရှိ/O ကုန်းမြင့်/O များ/O သည်/O တစ်/O ကြိမ်/O က/O ပင်လယ်/O အောက်/O တွင်/O ရှိ/O ခဲ့/O ၍/O နောက်/O မှ/O မြေ/O မြင့်တက်/O လာ/O ခဲ့/O ခြင်း/O ဖြစ်/O သည်/O ဟု/O တွေးယူ/O ခဲ့/N ဖူး/N လေ/N သည်/E
ဂင်မ်ချီ/B သိပ်/O ပြီး/O နောက်/O ဂင်မ်ချီ/O အိုး/O ကို/O မြေကြီး/O ထဲ/N မြုပ်/N လိုက်/N တယ်/E
အအေးမိ/B မယ်/E
ဧည့်လမ်းညွှန်/B ရော/O ထည့်/O ပေး/N လို့/N ရ/N လား/E
မှန်တင်ခုံ/B ဘေး/O က/O အရက်/O ပုလင်း/O ကို/O ထုတ်ယူ/N လိုက်ရင်းကောက်မော့/N လိုက်/N သည်/E ပုလင်း/B ပြန်/O အသိမ်း/O မှာ/O အပြာရောင်/O ဝတ်စုံ/O ကို/O မြင်/N လိုက်/N ရ/N သည်/E
```

လုပ်ရမှာက အောက်ပါ format အဖြစ် ပြောင်းလဲနိုင်ဖို့...  

```
ဧည့်/B လမ်း/O ညွှန်/O ရော/O ထည့်/O ပေး/N လို့/N ရ/N လား/E
မှန်/B တင်/O ခုံ/O ဘေး/O က/O အ/O ရက်/O ပု/O လင်း/O ကို/O ထုတ်/O ယူ/O လိုက်/O ရင်း/O ကောက်/N မော့/N လိုက်/N သည်/E ပု/B လင်း/O ပြန်/O အ/O သိမ်း/O မှာ/O အ/O ပြာ/O ရောင်/O ဝတ်/O စုံ/O ကို/O မြင်/N လိုက်/N ရ/N သည်/E
```

draft algorithm က  

```
read line by line
make syllable segmentation on each word and tagged based on the original tag
Check /B and /N tagged syllables; if continuous more than one /B tagged syllables found, Changed 2nd to other /B tagged syllables to /O. if continuous more than three /N tagged syllables found, keep last three /N tagged syllables and Changed other /N tagged into /O.
```

```
input: မှန်တင်ခုံ/B ဘေး/O က/O အရက်/O ပုလင်း/O ကို/O ထုတ်ယူ/N လိုက်ရင်းကောက်မော့/N လိုက်/N သည်/E ပုလင်း/B ပြန်/O အသိမ်း/O မှာ/O အပြာရောင်/O ဝတ်စုံ/O ကို/O မြင်/N လိုက်/N ရ/N သည်/E

syllable segmented and copy original tags: မှန်/B တင်/B ခုံ/B ဘေး/O က/O အ/O ရက်/O ပု/O လင်း/O ကို/O ထုတ်/N ယူ/N လိုက်/N ရင်း/N ကောက်/N မော့/N လိုက်/N သည်/E ပု/B လင်း/B ပြန်/O အ/O သိမ်း/O မှာ/O အ/O ပြာ/O ရောင်/O ဝတ်/O စုံ/O ကို/O မြင်/N လိုက်/N ရ/N သည်/E

Check and Replace: မှန်/B တင်/O ခုံ/O ဘေး/O က/O အ/O ရက်/O ပု/O လင်း/O ကို/O ထုတ်/O ယူ/O လိုက်/O ရင်း/O ကောက်/N မော့/N လိုက်/N သည်/E ပု/B လင်း/O ပြန်/O အ/O သိမ်း/O မှာ/O အ/O ပြာ/O ရောင်/O ဝတ်/O စုံ/O ကို/O မြင်/N လိုက်/N ရ/N သည်/E
```

1st version of the code is as follows:  

```python
#!/usr/bin/env python3
# -*- coding:utf-8 -*-

import argparse
import re
import sys

def parse_arguments():
    """Parse command line arguments."""
    parser = argparse.ArgumentParser(description="Convert word-tagged Burmese data to syllable-tagged data.")
    parser.add_argument("-i", "--input", type=str, required=True, help="Input file (word-tagged data)")
    parser.add_argument("-o", "--output", type=str, required=True, help="Output file (syllable-tagged data)")
    return parser.parse_args()

def create_break_pattern():
    """Create the regular expression pattern for syllable segmentation."""
    my_consonant = r"က-အ"
    en_char = r"a-zA-Z0-9"
    other_char = r"ဣဤဥဦဧဩဪဿ၌၍၏၀-၉၊။!-/:-@[-`{-~\s"
    subscript_symbol = r'္'
    a_that = r'်'

    return re.compile(
        r"((?<!" + subscript_symbol + r")[" + my_consonant + r"]"
        r"(?![" + a_that + subscript_symbol + r"])"
        r"|[" + en_char + other_char + r"])"
    )

def syllable_segment_word_tag(word_tag, break_pattern):
    """Segment a word and duplicate its tag for all syllables."""
    if '/' not in word_tag:
        return word_tag
    word, tag = word_tag.rsplit('/', 1)
    syllables = break_pattern.sub(r" \1", word).strip().split()
    return " ".join(f"{syl}/{tag}" for syl in syllables)

def clean_tags(syllable_tags):
    """Clean the tags in the syllable-tagged sentence."""
    cleaned_tags = []
    n_tag_count = 0

    for tag in syllable_tags:
        if '/B' in tag:
            if not cleaned_tags or '/B' not in cleaned_tags[-1]:
                cleaned_tags.append(tag)
            else:
                cleaned_tags.append(tag.replace('/B', '/O'))
        elif '/N' in tag:
            if n_tag_count < 3:
                cleaned_tags.append(tag)
                n_tag_count += 1
            else:
                cleaned_tags.append(tag.replace('/N', '/O'))
        else:
            cleaned_tags.append(tag)
            if '/N' not in tag:
                n_tag_count = 0

    return cleaned_tags

def process_line(line, break_pattern):
    """Process a single line to convert word tags to syllable tags."""
    syllable_tags = []
    for word_tag in line.strip().split():
        syllable_tags.extend(syllable_segment_word_tag(word_tag, break_pattern).split())
    return " ".join(clean_tags(syllable_tags))

def process_file(input_file, output_file, break_pattern):
    """Process the input file line by line and write the result to the output file."""
    with open(input_file, 'r', encoding='utf-8') as infile, open(output_file, 'w', encoding='utf-8') as outfile:
        for line in infile:
            processed_line = process_line(line, break_pattern)
            outfile.write(processed_line + '\n')

if __name__ == "__main__":
    args = parse_arguments()
    break_pattern = create_break_pattern()
    process_file(args.input, args.output, break_pattern)

```

above code က N tag တွေကို ပြင်တာမှာ မှားနေသေးတယ်။  

input:  
```
ရင်ဘတ်/B အောင့်/O လာ/N ရင်/N သတိထား/N ပါ/E
ဘယ်လောက်/B နောက်ကျ/N သလဲ/E
ကြိုပို့/B ဘတ်စ်ကား/N က/N အဆင်အပြေဆုံး/N ပဲ/E
သူမ/B သူငယ်ချင်း/O များ/O တွင်/O မ/O တော့/O ဘုန်းကြီး/O ဝတ်/O သွား/O သော/O ဗေဒင်/O တတ်/O သည့်/O အဘိုး/O မ/O ရှိ/O ၍/O ပဲ/N လား/N မ/N သိ/E နာမည်/B လှလှ/O ကလေး/O တွေ/N နှင့်/N ဖြစ်/N သည်/E တခြား/B မိန်းကလေး/O တွေ/O ရဲ့/O နာမည်/O တွေ/O က/O လည်း/O မ/O ကောင်း/O ရင်/O သာ/N ရှိ/N ရ/N မည်/E
```

current output:  
```
ရင်/B ဘတ်/O အော/O င့်/O လာ/N ရင်/N သ/N တိ/O ထား/O ပါ/E
ဘယ်/B လောက်/O နောက်/N ကျ/N သ/E လဲ/E
ကြို/B ပို့/O ဘတ်စ်/N ကား/N က/N အ/O ဆင်/O အ/O ပြေ/O ဆုံး/O ပဲ/E
သူ/B မ/O သူ/O ငယ်/O ချင်း/O များ/O တွင်/O မ/O တော့/O ဘုန်း/O ကြီး/O ဝတ်/O သွား/O သော/O ဗေ/O ဒင်/O တတ်/O သ/O ည့်/O အ/O ဘိုး/O မ/O ရှိ/O ၍/O ပဲ/N လား/N မ/N သိ/E နာ/B မည်/O လှ/O လှ/O က/O လေး/O တွေ/N နှ/N င့်/N ဖြစ်/O သည်/E တ/B ခြား/O မိန်း/O က/O လေး/O တွေ/O ရဲ့/O နာ/O မည်/O တွေ/O က/O လည်း/O မ/O ကောင်း/O ရင်/O သာ/N ရှိ/N ရ/N မည်/E
```

It should be as follows:  
```
ရင်/B ဘတ်/O အော/O င့်/O လာ/O ရင်/O သ/N တိ/N ထား/N ပါ/E
ဘယ်/B လောက်/O နောက်/N ကျ/N သ/E လဲ/E
ကြို/B ပို့/O ဘတ်စ်/O ကား/O က/O အ/O ဆင်/O အ/N ပြေ/N ဆုံး/N ပဲ/E
သူ/B မ/O သူ/O ငယ်/O ချင်း/O များ/O တွင်/O မ/O တော့/O ဘုန်း/O ကြီး/O ဝတ်/O သွား/O သော/O ဗေ/O ဒင်/O တတ်/O သ/O ည့်/O အ/O ဘိုး/O မ/O ရှိ/O ၍/O ပဲ/N လား/N မ/N သိ/E နာ/B မည်/O လှ/O လှ/O က/O လေး/O တွေ/O နှ/N င့်/N ဖြစ်/N သည်/E တ/B ခြား/O မိန်း/O က/O လေး/O တွေ/O ရဲ့/O နာ/O မည်/O တွေ/O က/O လည်း/O မ/O ကောင်း/O ရင်/O သာ/N ရှိ/N ရ/N မည်/E
```

အဲဒါကြောင့် algorithm ကို အောက်ပါအတိုင်း ပြင်ဆင်လို့ ရလိမ့်မယ်။  

1. read the word tagged input file line by line
2. Sentence splitting based on "\E" tag (here, \E mean end of one sentence) and put into a list or array.
3. loop each sentence and work followings: 
 - make syllable segmentation on each word and copy the original tags to each syllables until end of the line.
 - Checked the syllable segmented and tagged output sentence and make cleaning or replacing for "more than one continuous /B tags" and "more than three continuous /N tags" and also "more than one /E tags".
 
Here, cleaning for continuous /B tags are easy, keep the 1st /B tag in one sentence and replace other continuous /B tags with /O. Similarly, cleaning for continuous /E tags are also easy, keep the last /E tag and replace others with /N tags. However, after doing rough replacing, we have to check the whole sentence. What I mean is we have to see all taggings for the whole sentence. The rule is only one /B and only one /E tag for a sentence. And it should be maximum 3 /N tags (i.e. depends on number of syllable or word in a sentence) in a sentence. If we found more than three continuous /N tags in a sentence, we should keep the last three /N tags (i.e. /N /N /N /E) and replace other /N tags with /O tags.

4. We have to work above 3 steps for the whole input file.


## Updating Python Code  

```python
#!/usr/bin/env python3
# -*- coding:utf-8 -*-

import argparse
import re

def parse_arguments():
    """Parse command line arguments."""
    parser = argparse.ArgumentParser(description="Convert word-tagged Burmese data to syllable-tagged data.")
    parser.add_argument("-i", "--input", type=str, required=True, help="Input file (word-tagged data)")
    parser.add_argument("-o", "--output", type=str, required=True, help="Output file (syllable-tagged data)")
    return parser.parse_args()

def create_break_pattern():
    """Create the regular expression pattern for syllable segmentation."""
    my_consonant = r"က-အ"
    en_char = r"a-zA-Z0-9"
    other_char = r"ဣဤဥဦဧဩဪဿ၌၍၏၀-၉၊။!-/:-@[-`{-~\s"
    subscript_symbol = r'္'
    a_that = r'်'

    return re.compile(
        r"((?<!" + subscript_symbol + r")[" + my_consonant + r"]"
        r"(?![" + a_that + subscript_symbol + r"])"
        r"|[" + en_char + other_char + r"])"
    )

def syllable_segment_word_tag(word_tag, break_pattern):
    """Segment a word and duplicate its tag for all syllables."""
    if '/' not in word_tag:
        return word_tag
    word, tag = word_tag.rsplit('/', 1)
    syllables = break_pattern.sub(r" \1", word).strip().split()
    return " ".join(f"{syl}/{tag}" for syl in syllables)

def clean_tags(sentence_tags):
    """Clean the tags in the syllable-tagged sentence."""
    cleaned_tags = []
    n_tag_count = 0
    found_b_tag = False
    e_tag_indices = []

    # Identify positions of `/E` tags
    for i, tag in enumerate(sentence_tags):
        if '/E' in tag:
            e_tag_indices.append(i)

    # Process each tag
    for i, tag in enumerate(sentence_tags):
        if '/B' in tag:
            if not found_b_tag:
                cleaned_tags.append(tag)
                found_b_tag = True
            else:
                cleaned_tags.append(tag.replace('/B', '/O'))
        elif '/N' in tag:
            if n_tag_count < 3:
                cleaned_tags.append(tag)
                n_tag_count += 1
            else:
                cleaned_tags.append(tag.replace('/N', '/O'))
        elif '/E' in tag:
            # Keep only the last `/E` tag
            if i == e_tag_indices[-1]:
                cleaned_tags.append(tag)
            else:
                cleaned_tags.append(tag.replace('/E', '/N'))
        else:
            cleaned_tags.append(tag)
            if '/N' not in tag:
                n_tag_count = 0

    return cleaned_tags

def process_sentence(sentence, break_pattern):
    """Process a single sentence to convert word tags to syllable tags and clean tags."""
    syllable_tags = []
    for word_tag in sentence.strip().split():
        syllable_tags.extend(syllable_segment_word_tag(word_tag, break_pattern).split())
    return " ".join(clean_tags(syllable_tags))

def process_file(input_file, output_file, break_pattern):
    """Process the input file line by line and write the result to the output file."""
    with open(input_file, 'r', encoding='utf-8') as infile, open(output_file, 'w', encoding='utf-8') as outfile:
        for line in infile:
            # Split the line into sentences using `/E` as the delimiter
            sentences = line.strip().split("/E")
            processed_sentences = [
                process_sentence(sentence + "/E", break_pattern).strip() for sentence in sentences if sentence.strip()
            ]
            outfile.write(" ".join(processed_sentences) + '\n')

if __name__ == "__main__":
    args = parse_arguments()
    break_pattern = create_break_pattern()
    process_file(args.input, args.output, break_pattern)

```

input:  

```
ရင်ဘတ်/B အောင့်/O လာ/N ရင်/N သတိထား/N ပါ/E
ဘယ်လောက်/B နောက်ကျ/N သလဲ/E
ကြိုပို့/B ဘတ်စ်ကား/N က/N အဆင်အပြေဆုံး/N ပဲ/E
သူမ/B သူငယ်ချင်း/O များ/O တွင်/O မ/O တော့/O ဘုန်းကြီး/O ဝတ်/O သွား/O သော/O ဗေဒင်/O တတ်/O သည့်/O အဘိုး/O မ/O ရှိ/O ၍/O ပဲ/N လား/N မ/N သိ/E နာမည်/B လှလှ/O ကလေး/O တွေ/N နှင့်/N ဖြစ်/N သည်/E တခြား/B မိန်းကလေး/O တွေ/O ရဲ့/O နာမည်/O တွေ/O က/O လည်း/O မ/O ကောင်း/O ရင်/O သာ/N ရှိ/N ရ/N မည်/E
```

output:  

```
ရင်/B ဘတ်/O အော/O င့်/O လာ/N ရင်/N သ/N တိ/O ထား/O ပါ/E
ဘယ်/B လောက်/O နောက်/N ကျ/N သ/N လဲ/E
ကြို/B ပို့/O ဘတ်စ်/N ကား/N က/N အ/O ဆင်/O အ/O ပြေ/O ဆုံး/O ပဲ/E
သူ/B မ/O သူ/O ငယ်/O ချင်း/O များ/O တွင်/O မ/O တော့/O ဘုန်း/O ကြီး/O ဝတ်/O သွား/O သော/O ဗေ/O ဒင်/O တတ်/O သ/O ည့်/O အ/O ဘိုး/O မ/O ရှိ/O ၍/O ပဲ/N လား/N မ/N သိ/E နာ/B မည်/O လှ/O လှ/O က/O လေး/O တွေ/N နှ/N င့်/N ဖြစ်/O သည်/E တ/B ခြား/O မိန်း/O က/O လေး/O တွေ/O ရဲ့/O နာ/O မည်/O တွေ/O က/O လည်း/O မ/O ကောင်း/O ရင်/O သာ/N ရှိ/N ရ/N မည်/E
```

/N tag ကို cleaning လုပ်တာမှာ မှားနေသေးတယ်။  
It should be as follows:  
```
ရင်/B ဘတ်/O အော/O င့်/O လာ/O ရင်/O သ/N တိ/N ထား/N ပါ/E
ဘယ်/B လောက်/O နောက်/N ကျ/N သ/N လဲ/E
ကြို/B ပို့/O ဘတ်စ်/O ကား/O က/O အ/O ဆင်/O အ/N ပြေ/N ဆုံး/N ပဲ/E
သူ/B မ/O သူ/O ငယ်/O ချင်း/O များ/O တွင်/O မ/O တော့/O ဘုန်း/O ကြီး/O ဝတ်/O သွား/O သော/O ဗေ/O ဒင်/O တတ်/O သ/O ည့်/O အ/O ဘိုး/O မ/O ရှိ/O ၍/O ပဲ/N လား/N မ/N သိ/E နာ/B မည်/O လှ/O လှ/O က/O လေး/O တွေ/O နှ/N င့်/N ဖြစ်/N သည်/E တ/B ခြား/O မိန်း/O က/O လေး/O တွေ/O ရဲ့/O နာ/O မည်/O တွေ/O က/O လည်း/O မ/O ကောင်း/O ရင်/O သာ/N ရှိ/N ရ/N မည်/E
```

## Updating Python Code Again  

တကယ်က ဒီနေရာမှာ နာရီဝက်လောက် အချိန်ပေး ပြင်ခဲ့ရတယ်။  

```python
#!/usr/bin/env python3
# -*- coding:utf-8 -*-

import argparse
import re

def parse_arguments():
    """Parse command line arguments."""
    parser = argparse.ArgumentParser(description="Convert word-tagged Burmese data to syllable-tagged data.")
    parser.add_argument("-i", "--input", type=str, required=True, help="Input file (word-tagged data)")
    parser.add_argument("-o", "--output", type=str, required=True, help="Output file (syllable-tagged data)")
    return parser.parse_args()

def create_break_pattern():
    """Create the regular expression pattern for syllable segmentation."""
    my_consonant = r"က-အ"
    en_char = r"a-zA-Z0-9"
    other_char = r"ဣဤဥဦဧဩဪဿ၌၍၏၀-၉၊။!-/:-@[-`{-~\s"
    subscript_symbol = r'္'
    a_that = r'်'

    return re.compile(
        r"((?<!" + subscript_symbol + r")[" + my_consonant + r"]"
        r"(?![" + a_that + subscript_symbol + r"])"
        r"|[" + en_char + other_char + r"])"
    )

def syllable_segment_word_tag(word_tag, break_pattern):
    """Segment a word and duplicate its tag for all syllables."""
    if '/' not in word_tag:
        return word_tag
    word, tag = word_tag.rsplit('/', 1)
    syllables = break_pattern.sub(r" \1", word).strip().split()
    return " ".join(f"{syl}/{tag}" for syl in syllables)

def clean_tags(sentence_tags):
    """Clean the tags in the syllable-tagged sentence."""
    cleaned_tags = []
    n_tag_positions = []
    b_tag_found = False

    # Identify `/N` and `/E` positions
    for i, tag in enumerate(sentence_tags):
        if '/N' in tag:
            n_tag_positions.append(i)
        elif '/B' in tag:
            if not b_tag_found:
                b_tag_found = True
                cleaned_tags.append(tag)
            else:
                cleaned_tags.append(tag.replace('/B', '/O'))
        elif '/E' in tag:
            # Mark position but handle in final cleanup
            continue
        else:
            cleaned_tags.append(tag)

    # Handle `/N` tags: Only keep the last three
    n_tag_positions_to_keep = n_tag_positions[-3:]  # Keep the last three `/N` tags
    for i in n_tag_positions:
        if i in n_tag_positions_to_keep:
            cleaned_tags.append(sentence_tags[i])
        else:
            cleaned_tags.append(sentence_tags[i].replace('/N', '/O'))

    # Ensure exactly one `/E` tag at the end
    cleaned_tags.append('/E')

    return cleaned_tags

def process_sentence(sentence, break_pattern):
    """Process a single sentence to convert word tags to syllable tags and clean tags."""
    syllable_tags = []
    for word_tag in sentence.strip().split():
        syllable_tags.extend(syllable_segment_word_tag(word_tag, break_pattern).split())
    return " ".join(clean_tags(syllable_tags))

def process_file(input_file, output_file, break_pattern):
    """Process the input file line by line and write the result to the output file."""
    with open(input_file, 'r', encoding='utf-8') as infile, open(output_file, 'w', encoding='utf-8') as outfile:
        for line in infile:
            # Split the line into sentences using `/E` as the delimiter
            sentences = line.strip().split("/E")
            processed_sentences = [
                process_sentence(sentence + "/E", break_pattern).strip() for sentence in sentences if sentence.strip()
            ]
            outfile.write(" ".join(processed_sentences) + '\n')

if __name__ == "__main__":
    args = parse_arguments()
    break_pattern = create_break_pattern()
    process_file(args.input, args.output, break_pattern)

```

လက်ရှိ code က တော်တော်လေး အဆင်ပြေသွားပြီ။  

input:  

```
ရင်ဘတ်/B အောင့်/O လာ/N ရင်/N သတိထား/N ပါ/E
ဘယ်လောက်/B နောက်ကျ/N သလဲ/E
ကြိုပို့/B ဘတ်စ်ကား/N က/N အဆင်အပြေဆုံး/N ပဲ/E
သူမ/B သူငယ်ချင်း/O များ/O တွင်/O မ/O တော့/O ဘုန်းကြီး/O ဝတ်/O သွား/O သော/O ဗေဒင်/O တတ်/O သည့်/O အဘိုး/O မ/O ရှိ/O ၍/O ပဲ/N လား/N မ/N သိ/E နာမည်/B လှလှ/O ကလေး/O တွေ/N နှင့်/N ဖြစ်/N သည်/E တခြား/B မိန်းကလေး/O တွေ/O ရဲ့/O နာမည်/O တွေ/O က/O လည်း/O မ/O ကောင်း/O ရင်/O သာ/N ရှိ/N ရ/N မည်/E
```

output:  

```
ရင်/B ဘတ်/O အော/O င့်/O လာ/O ရင်/O သ/N တိ/N ထား/N /E
ဘယ်/B လောက်/O နောက်/N ကျ/N /E
ကြို/B ပို့/O ဘတ်စ်/O ကား/O က/O အ/O ဆင်/O အ/N ပြေ/N ဆုံး/N /E
သူ/B မ/O သူ/O ငယ်/O ချင်း/O များ/O တွင်/O မ/O တော့/O ဘုန်း/O ကြီး/O ဝတ်/O သွား/O သော/O ဗေ/O ဒင်/O တတ်/O သ/O ည့်/O အ/O ဘိုး/O မ/O ရှိ/O ၍/O ပဲ/N လား/N မ/N /E နာ/B မည်/O လှ/O လှ/O က/O လေး/O တွေ/O နှ/N င့်/N ဖြစ်/N /E တ/B ခြား/O မိန်း/O က/O လေး/O တွေ/O ရဲ့/O နာ/O မည်/O တွေ/O က/O လည်း/O မ/O ကောင်း/O ရင်/O သာ/N ရှိ/N ရ/N /E
```

ဒါပေမဲ့ အောက်ပါလိုမျိုး စာကြောင်း ကို ဒီအတိုင်းပဲ ထားမလား သို့မဟုတ် /O ကို /N နဲ့ အစားထိုးမလား ဆိုတာကို စဉ်းစားရလိမ့်မယ်။ ငါတို့ သတ်မှတ်ထားတဲ့ Rule အရ ဆိုရင် /O နေရာမှာ /N နဲ့ အစားထိုးသင့်တယ်။ သို့သော်လည်း အစားမထိုးရင်လည်း training ကတော့ လုပ်လို့ ရတဲ့ အနေအထားတော့ ရှိနေပြီ။  

```
ဘယ်/B လောက်/O နောက်/N ကျ/N /E
```

တကယ်ကတော့ လူတွေက tag လုပ်ရင်တောင် ဒါမျိုး minor ကွဲပြားတာက ရှိနိုင်လို့ လွှတ်ထားလိုက်ရင်လည်း ရနိုင်ပါတယ်။

အိပ်ယာနိုးလာရင် တခြား အမှားတွေကော ရှိသေးလား manual checking လုပ်ပြီးမှ code updating ကိစ္စကို ဆက်စဉ်းစားရန်။  

ပြင်ချင်တဲ့ စာကြောင်းတွေ က အောက်ပါအတိုင်း  

syllable breaking လုပ်တဲ့အခါမှာ အင်္ဂလိပ်စာလုံးတွေကို မထိအောင် ပြင်ရန် ...  
e.g. line no. 18 of test.tagged file.   
  
```
၂၀၂၁/B မှာ/O ဖြစ်/O ခဲ့/O တဲ့/O ကိုရိုနာ/O ဗိုင်းရပ်စ်ကူးစက်မှု/O ပဉ္စမ/O လှိုင်း/O တုန်း/O က/O ကာကွယ်/O ဆေး/O ၂/O ကြိမ်ထိုး/O ထား/O ပြီး/O သူ/O တွေ/O လည်း/O breakthrough/O infections/O လို့/O ခေါ်/O တဲ့/O ကာကွယ်/O ဆေးထိုး/O ပြီးနောက်/O ကူးစက်မှု/O တွေ/O ဖြစ်/N ခဲ့/N ပါ/N တယ်/E သက်ကြီးရွယ်အို/B စောင့်ရှောက်/O ရေး/O ဂေဟာ/O တွေ/O မှာ/O လည်း/O အဲဒီ/O လို/O ကာကွယ်/O ဆေးထိုး/O ပြီးနောက်/O ကူးစက်မှု/O တွေ/O အစု/O လိုက်/O အပြုံ/O လိုက်/O ဖြစ်/O ခဲ့/O တာ/O များ/O ခဲ့/O ပုံ/N ရ/N ပါ/N တယ်/E

၂/B ၀/O ၂/O ၁/O မှာ/O ဖြစ်/O ခဲ့/O တဲ့/O ကို/O ရို/O နာ/O ဗိုင်း/O ရပ်စ်/O ကူး/O စက်/O မှု/O ပဉ္စ/O မ/O လှိုင်း/O တုန်း/O က/O ကာ/O ကွယ်/O ဆေး/O ၂/O ကြိမ်/O ထိုး/O ထား/O ပြီး/O သူ/O တွေ/O လည်း/O b/O r/O e/O a/O k/O t/O h/O r/O o/O u/O g/O h/O i/O n/O f/O e/O c/O t/O i/O o/O n/O s/O လို့/O ခေါ်/O တဲ့/O ကာ/O ကွယ်/O ဆေး/O ထိုး/O ပြီး/O နောက်/O ကူး/O စက်/O မှု/O တွေ/O ဖြစ်/N ခဲ့/N ပါ/N /E သက်/B ကြီး/O ရွယ်/O အို/O စော/O င့်/O ရှောက်/O ရေး/O ဂေ/O ဟာ/O တွေ/O မှာ/O လည်း/O အဲ/O ဒီ/O လို/O ကာ/O ကွယ်/O ဆေး/O ထိုး/O ပြီး/O နောက်/O ကူး/O စက်/O မှု/O တွေ/O အ/O စု/O လိုက်/O အ/O ပြုံ/O လိုက်/O ဖြစ်/O ခဲ့/O တာ/O များ/O ခဲ့/O ပုံ/N ရ/N ပါ/N /E
```

\E tag without word  
line no. 19  

```
ခင်ဗျား/B အခု/O အလုပ်ချင်ဆုံး/O အရာ/N ဟာ/N ဘာ/N လဲ/E
ခင်/B ဗျား/O အ/O ခု/O အ/O လုပ်/O ချင်/O ဆုံး/O အ/O ရာ/N ဟာ/N ဘာ/N /E
```

line no. 20  

```
နောက်/B တစ်/O ပတ်/O ကြာသပတေး/O နေ့/O မနက်/O ၉/N နာရီ/N မှာ/N ပါ/E
နောက်/B တစ်/O ပတ်/O ကြာ/O သ/O ပ/O တေး/O နေ့/O မ/O နက်/O ၉/O နာ/N ရီ/N မှာ/N /E
```

word ငါးလုံးပဲ ရှိတဲ့ စာကြောင်းမှာ /N tag က နှစ်ခုပဲ ပါနေတာမျိုး။  
line no. 33
```
ဆရာ/B နေကောင်း/N လား/E
ဆ/B ရာ/O နေ/N ကောင်း/N /E
```

ဒါက လက်ရှိ Python code နဲ့တော့ မဆိုင်ဘူး။ Normalization လုပ်ပြီးမှ run ရင် အဆင်ပြေလိမ့်မယ်။  
ကြော နဲ့ င့် ကွဲသွားတဲ့ ကိစ္စမျိုး line no. 39  

```
ဘာ/B ကြောင့်/N လာ/N ခဲ့/N သလဲ/E
ဘာ/B ကြော/O င့်/N လာ/N ခဲ့/N /E
```

line no. 1315  

```
ကူညီ/B ပါရစေ/E
ကူ/B ညီ/O /E
```

တိုတဲ့စာကြောင်းမှာ \N tag တောင်မပါတာမျိုး။  
line no. 

```
ကျက်ကျက်/B လား/E  
ကျက်/B ကျက်/O /E
```

Thinking ...  

```
1 syllable: ကျား\E
2 syllables: ကျွန်\B တော်\E
3 syllables: ကျွန်\B တော့်\N ကား\E
4 syllables: ကျွန်\B မ\N ၏\N ကြောင်\E
5 syllables: ကျွန်\B တော်\N ရဲ့\N မိန်း\N မ\E
6 syllables: အိမ်\B ရှေ့\O က\N လမ်း\N ကြား\N ဆိုင်\E
7 syllables: မ\B ရ\O မ\O က\N ချီ\N တက်\N ကြ\E
8 syllables: မ\B သောက်\O ရ\O ရင်\O မ\N နေ\N နိုင်\N ပါ\E
9 syllables: ကျောင်း\B မှန်\O မှန်\O တက်\O စာ\O မ\N ခက်\N ပါ\N ဘူး\E
10 syllables: ဘုန်း\B ကြီး\O ကျောင်း\O သား\O လုပ်\O ရင်း\O စာ\N သင်\N ခဲ့\N တယ်\E
11 syllables: အ\B ချစ်\O နဲ့\O ကျွန်\O တော်\O အ\O ထက်\O တန်း\N ကျောင်း\N မှာ\N တွေ့\E
12 syllables: သ\B မိုင်း\O က\O နေ\O မြေ\O နီ\O ကုန်း\O ကို\O သွား\N ကြ\N ရ\N အောင်\E
```

\B နဲ့ ကပ်နေတဲ့ စာကြောင်းတွေရဲ့ information ကိုပါ ယူချင်ရင် အောက်ပါ pattern နဲ့ သွားမယ်။  

```
1 syllable: ကျား\E
2 syllables: ကျွန်\B တော်\E
3 syllables: ကျွန်\B တော့်\N ကား\E
4 syllables: ကျွန်\B မ\N ၏\N ကြောင်\E
5 syllables: ကျွန်\B တော်\N ရဲ့\N မိန်း\N မ\E
6 syllables: အိမ်\B ရှေ့\F က\N လမ်း\N ကြား\N ဆိုင်\E
7 syllables: မ\B ရ\F မ\F က\N ချီ\N တက်\N ကြ\E
8 syllables: မ\B သောက်\F ရ\F ရင်\F မ\N နေ\N နိုင်\N ပါ\E
9 syllables: ကျောင်း\B မှန်\F မှန်\F တက်\F စာ\O မ\N ခက်\N ပါ\N ဘူး\E
10 syllables: ဘုန်း\B ကြီး\F ကျောင်း\F သား\F လုပ်\O ရင်း\O စာ\N သင်\N ခဲ့\N တယ်\E
11 syllables: အ\B ချစ်\F နဲ့\F ကျွန်\F တော်\O အ\O ထက်\O တန်း\N ကျောင်း\N မှာ\N တွေ့\E
12 syllables: သ\B မိုင်း\F က\F နေ\F မြေ\O နီ\O ကုန်း\O ကို\O သွား\N ကြ\N ရ\N အောင်\E
```

To fix current error, I changed the algorithm and it is as follows:

1. read the word tagged input file line by line
2. Sentence splitting based on "\E" tag (here, \E mean end of one sentence) and put into a list or array.
3. loop each sentence inside the array or list and work followings:  
 - make syllable segmentation on each sentence after that count the no of syllables and tagged based on following patterns two patterns based on the -p or --pattern option, --pattern BONE (default), --pattern BFONE:
 
BONE pattern is as follows:  

1 syllable: ကျား\E
2 syllables: ကျွန်\B တော်\E
3 syllables: ကျွန်\B တော့်\N ကား\E
4 syllables: ကျွန်\B မ\N ၏\N ကြောင်\E
5 syllables: ကျွန်\B တော်\N ရဲ့\N မိန်း\N မ\E
6 syllables: အိမ်\B ရှေ့\O က\N လမ်း\N ကြား\N ဆိုင်\E
7 syllables: မ\B ရ\O မ\O က\N ချီ\N တက်\N ကြ\E
8 syllables: မ\B သောက်\O ရ\O ရင်\O မ\N နေ\N နိုင်\N ပါ\E
9 syllables: ကျောင်း\B မှန်\O မှန်\O တက်\O စာ\O မ\N ခက်\N ပါ\N ဘူး\E
10 syllables: ဘုန်း\B ကြီး\O ကျောင်း\O သား\O လုပ်\O ရင်း\O စာ\N သင်\N ခဲ့\N တယ်\E
11 syllables: အ\B ချစ်\O နဲ့\O ကျွန်\O တော်\O အ\O ထက်\O တန်း\N ကျောင်း\N မှာ\N တွေ့\E
12 syllables: သ\B မိုင်း\O က\O နေ\O မြေ\O နီ\O ကုန်း\O ကို\O သွား\N ကြ\N ရ\N အောင်\E

In BONE pattern, if the number of syllables increase more than 6 syllables, just increase \O tags between \B and \N tags.

The follows is the BFONE pattern:  

1 syllable: ကျား\E
2 syllables: ကျွန်\B တော်\E
3 syllables: ကျွန်\B တော့်\N ကား\E
4 syllables: ကျွန်\B မ\N ၏\N ကြောင်\E
5 syllables: ကျွန်\B တော်\N ရဲ့\N မိန်း\N မ\E
6 syllables: အိမ်\B ရှေ့\F က\N လမ်း\N ကြား\N ဆိုင်\E
7 syllables: မ\B ရ\F မ\F က\N ချီ\N တက်\N ကြ\E
8 syllables: မ\B သောက်\F ရ\F ရင်\F မ\N နေ\N နိုင်\N ပါ\E
9 syllables: ကျောင်း\B မှန်\F မှန်\F တက်\F စာ\O မ\N ခက်\N ပါ\N ဘူး\E
10 syllables: ဘုန်း\B ကြီး\F ကျောင်း\F သား\F လုပ်\O ရင်း\O စာ\N သင်\N ခဲ့\N တယ်\E
11 syllables: အ\B ချစ်\F နဲ့\F ကျွန်\F တော်\O အ\O ထက်\O တန်း\N ကျောင်း\N မှာ\N တွေ့\E
12 syllables: သ\B မိုင်း\F က\F နေ\F မြေ\O နီ\O ကုန်း\O ကို\O သွား\N ကြ\N ရ\N အောင်\E

In BFONE pattern, if the number of syllables increase more than 9, just increase \O tags between \F and \N tags.

Of course, for the practical implementation, you can select the best way to make tagging faster and easier to read for further updating.

4. We have to work above 3 steps for the whole input file.

==========

Moreover, for the syllable breaking rule, I wanna update not to make break on other languages including English. We will make syllable breaking on Myanmar text, Myanmar numbers, English numbers, all punctuation. However, we won't touch English characters and other language characters such as Japanese, Chinese, Korean, Latin, Hindi ...  

Can you debug/update the code? 

syllable breaking pattern က အောက်ပါအတိုင်းဆိုရင် အဆင်ပြေနိုင်တယ်။  

```
def create_break_pattern():
    """Create the regular expression pattern for syllable segmentation."""
    my_consonant = r"\u1000-\u1021"  # Myanmar consonants
    my_numbers = r"\u1040-\u1049"    # Myanmar digits
    punctuation = r"\u104A-\u104F"  # Myanmar punctuation
    other_symbols = r"\u102B-\u103F" # Vowels, signs, etc.

    return re.compile(
        rf"([{my_consonant}{my_numbers}{punctuation}{other_symbols}]+|[^\u1000-\u109F\s]+|\s)"
    )

def syllable_segment(sentence, break_pattern):
    """Segment a sentence into syllables."""
    return break_pattern.findall(sentence)
```

## Prompt Log

အောက်ပါ prompt နဲလည်း ကြိုးစားခဲ့တယ်။  


Our current python code has errors on taggings and syllable breaking. 

To fix current errors, I changed the algorithm and it is as follows: 

1. read the word tagged input file line by line
2. Sentence splitting based on "\E" tag (here, \E mean end of one sentence) and put into a list or array.
3. loop each sentence inside the array or list and work followings:  
 - make syllable segmentation on each sentence after that count the no of syllables and tagged based on following patterns two patterns based on the -p or --pattern option, --pattern BONE (default), --pattern BFONE:
 
BONE pattern is as follows:  

1 syllable sentence: syllable1\E 
2 syllables sentence: syllable1\B syllable2\E
3 syllables sentence: syllable1\B syllable2\N syllable3\E
4 syllables sentence: syllable1\B syllable2\N syllable3\N syllable4\E
5 syllables sentence: syllable1\B syllable2\N syllable3\N syllable4\N syllable5\E
6 syllables sentence: syllable1\B syllable2\O syllable3\N syllable4\N syllable5\N syllable6\E
7 syllables sentence: syllable1\B syllable2\O syllable3\O syllable4\N syllable5\N syllable6\N syllable7\E
8 syllables sentence: syllable1\B syllable2\O syllable3\O syllable4\O syllable5\N syllable6\N syllable7\N syllable8\E
9 syllables sentence: syllable1\B syllable2\O syllable3\O syllable4\O syllable5\O syllable6\N syllable7\N syllable8\N syllable9\E
10 syllables sentence: syllable1\B syllable2\O syllable3\O syllable4\O syllable5\O syllable6\O syllable7\N syllable8\N syllable9\N syllable10\E
11 syllables sentence: syllable1\B syllable2\O syllable3\O syllable4\O syllable5\O syllable6\O syllable7\O syllable8\N syllable9\N syllable10\N syllable11\E
12 syllables sentence: syllable1\B syllable2\O syllable3\O syllable4\O syllable5\O syllable6\O syllable7\O syllable8\O syllable9\N syllable10\N syllable11\N syllable12\E

In BONE pattern, if the number of syllables increase more than 6 syllables, just increase \O tags between \B and \N tags.

The follows is the BFONE pattern:  

1 syllable sentence: syllable1\E 
2 syllables sentence: syllable1\B syllable2\E
3 syllables sentence: syllable1\B syllable2\N syllable3\E
4 syllables sentence: syllable1\B syllable2\N syllable3\N syllable4\E
5 syllables sentence: syllable1\B syllable2\N syllable3\N syllable4\N syllable5\E
6 syllables sentence: syllable1\B syllable2\F syllable3\N syllable4\N syllable5\N syllable6\E
7 syllables sentence: syllable1\B syllable2\F syllable3\F syllable4\N syllable5\N syllable6\N syllable7\E
8 syllables sentence: syllable1\B syllable2\F syllable3\F syllable4\F syllable5\N syllable6\N syllable7\N syllable8\E
9 syllables sentence: syllable1\B syllable2\F syllable3\F syllable4\F syllable5\O syllable6\N syllable7\N syllable8\N syllable9\E
10 syllables sentence: syllable1\B syllable2\F syllable3\F syllable4\F syllable5\O syllable6\O syllable7\N syllable8\N syllable9\N syllable10\E
11 syllables sentence: syllable1\B syllable2\F syllable3\F syllable4\F syllable5\O syllable6\O syllable7\O syllable8\N syllable9\N syllable10\N syllable11\E
12 syllables sentence: syllable1\B syllable2\F syllable3\F syllable4\F syllable5\O syllable6\O syllable7\O syllable8\O syllable9\N syllable10\N syllable11\N syllable12\E

In BFONE pattern, if the number of syllables increase more than 9, just increase \O tags between \F and \N tags.

Here, the syllable1, syllable2, syllable12 are just example and it can be any Myanmar syllables. What you have to do is count the no of syllables in syllable segmented sentence and just tag based on that no of syllables according to BONE or BFONE tagging patterns.

4. We have to work above 3 steps for the whole input file.

==========

Moreover, for the syllable breaking rule, I wanna update not to make break on other languages including English. We will make syllable breaking on Myanmar text, Myanmar numbers, English numbers, all punctuation. However, we won't touch English characters and other language characters such as Japanese, Chinese, Korean, Latin, Hindi ...  

Can you debug/update the code? 

For your convenience, our current python code is as follows:

#!/usr/bin/env python3
# -*- coding:utf-8 -*-

import argparse
import re

def parse_arguments():
    """Parse command line arguments."""
    parser = argparse.ArgumentParser(description="Convert word-tagged Burmese data to syllable-tagged data.")
    parser.add_argument("-i", "--input", type=str, required=True, help="Input file (word-tagged data)")
    parser.add_argument("-o", "--output", type=str, required=True, help="Output file (syllable-tagged data)")
    return parser.parse_args()

def create_break_pattern():
    """Create the regular expression pattern for syllable segmentation."""
    my_consonant = r"က-အ"
    en_char = r"a-zA-Z0-9"
    other_char = r"ဣဤဥဦဧဩဪဿ၌၍၏၀-၉၊။!-/:-@[-`{-~\s"
    subscript_symbol = r'္'
    a_that = r'်'

    return re.compile(
        r"((?<!" + subscript_symbol + r")[" + my_consonant + r"]"
        r"(?![" + a_that + subscript_symbol + r"])"
        r"|[" + en_char + other_char + r"])"
    )

def syllable_segment_word_tag(word_tag, break_pattern):
    """Segment a word and duplicate its tag for all syllables."""
    if '/' not in word_tag:
        return word_tag
    word, tag = word_tag.rsplit('/', 1)
    syllables = break_pattern.sub(r" \1", word).strip().split()
    return " ".join(f"{syl}/{tag}" for syl in syllables)

def clean_tags(sentence_tags):
    """Clean the tags in the syllable-tagged sentence."""
    cleaned_tags = []
    n_tag_positions = []
    b_tag_found = False

    # Identify `/N` and `/E` positions
    for i, tag in enumerate(sentence_tags):
        if '/N' in tag:
            n_tag_positions.append(i)
        elif '/B' in tag:
            if not b_tag_found:
                b_tag_found = True
                cleaned_tags.append(tag)
            else:
                cleaned_tags.append(tag.replace('/B', '/O'))
        elif '/E' in tag:
            # Mark position but handle in final cleanup
            continue
        else:
            cleaned_tags.append(tag)

    # Handle `/N` tags: Only keep the last three
    n_tag_positions_to_keep = n_tag_positions[-3:]  # Keep the last three `/N` tags
    for i in n_tag_positions:
        if i in n_tag_positions_to_keep:
            cleaned_tags.append(sentence_tags[i])
        else:
            cleaned_tags.append(sentence_tags[i].replace('/N', '/O'))

    # Ensure exactly one `/E` tag at the end
    cleaned_tags.append('/E')

    return cleaned_tags

def process_sentence(sentence, break_pattern):
    """Process a single sentence to convert word tags to syllable tags and clean tags."""
    syllable_tags = []
    for word_tag in sentence.strip().split():
        syllable_tags.extend(syllable_segment_word_tag(word_tag, break_pattern).split())
    return " ".join(clean_tags(syllable_tags))

def process_file(input_file, output_file, break_pattern):
    """Process the input file line by line and write the result to the output file."""
    with open(input_file, 'r', encoding='utf-8') as infile, open(output_file, 'w', encoding='utf-8') as outfile:
        for line in infile:
            # Split the line into sentences using `/E` as the delimiter
            sentences = line.strip().split("/E")
            processed_sentences = [
                process_sentence(sentence + "/E", break_pattern).strip() for sentence in sentences if sentence.strip()
            ]
            outfile.write(" ".join(processed_sentences) + '\n')

if __name__ == "__main__":
    args = parse_arguments()
    break_pattern = create_break_pattern()
    process_file(args.input, args.output, break_pattern)

==========

I think for the syllable breaking the following might be work:

def create_break_pattern():
    """Create the regular expression pattern for syllable segmentation."""
    my_consonant = r"\u1000-\u1021"  # Myanmar consonants
    my_numbers = r"\u1040-\u1049"    # Myanmar digits
    punctuation = r"\u104A-\u104F"  # Myanmar punctuation
    other_symbols = r"\u102B-\u103F" # Vowels, signs, etc.

    return re.compile(
        rf"([{my_consonant}{my_numbers}{punctuation}{other_symbols}]+|[^\u1000-\u109F\s]+|\s)"
    )

def syllable_segment(sentence, break_pattern):
    """Segment a sentence into syllables."""
    return break_pattern.findall(sentence)

Read the current python code well. Try to understand my explanation well before you start coding or debugging. I need the complete code. 


## Test Tagging

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ time python ./wordtag2syltag.py -i ./test.tagged -o ./test.tagged.bone -p BONE

real    0m0.243s
user    0m0.239s
sys     0m0.004s
```

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ time python ./wordtag2syltag.py -i ./test.tagged -o ./test.tagged.bfone -p BFONE

real    0m0.255s
user    0m0.242s
sys     0m0.012s
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$

```

## Updated Code 

```python
#!/usr/bin/env python3
# -*- coding:utf-8 -*-

import argparse
import re


def parse_arguments():
    """Parse command line arguments."""
    parser = argparse.ArgumentParser(description="Convert word-tagged Burmese data to syllable-tagged data.")
    parser.add_argument("-i", "--input", type=str, required=True, help="Input file (word-tagged data)")
    parser.add_argument("-o", "--output", type=str, required=True, help="Output file (syllable-tagged data)")
    parser.add_argument("-p", "--pattern", type=str, choices=["BONE", "BFONE"], default="BONE",
                        help="Tagging pattern: BONE or BFONE (default: BONE)")
    return parser.parse_args()


def create_break_pattern():
    """Create the regular expression pattern for syllable segmentation."""
    my_consonant = r"က-အ"
    en_no = r"0-9"  # Update to exclude English characters from segmentation
    other_char = r"ဣဤဥဦဧဩဪဿ၌၍၏၀-၉၊။!-/:-@[-`{-~\s"
    subscript_symbol = r'္'
    a_that = r'်'

    return re.compile(
        r"((?<!" + subscript_symbol + r")[" + my_consonant + r"]"
        r"(?![" + a_that + subscript_symbol + r"])"
        r"|[" + en_no + other_char + r"])"
    )


def syllable_segment(sentence, break_pattern):
    """Segment a sentence into syllables."""
    return break_pattern.sub(r" \1", sentence).strip().split()


def remove_tags_and_join(sentence):
    """Remove tags and join words into a tag-free sentence."""
    words = sentence.strip().split()
    cleaned_words = [word.split('/')[0] for word in words if '/' in word]  # Remove tags
    return " ".join(cleaned_words)


def tag_sentence(syllables, pattern):
    """Tag the syllables based on the selected pattern."""
    n = len(syllables)
    tags = []

    for i, syllable in enumerate(syllables):
        if i == 0:
            tags.append(f"{syllable}\\B")  # Beginning
        elif i == n - 1:
            tags.append(f"{syllable}\\E")  # Ending
        else:
            if pattern == "BONE":
                if n - i <= 4:  # Near Ending (N)
                    tags.append(f"{syllable}\\N")
                else:  # Other (O)
                    tags.append(f"{syllable}\\O")
            elif pattern == "BFONE":
                if i <= 3:  # Near Beginning (F)
                    tags.append(f"{syllable}\\F")
                elif n - i <= 4:  # Near Ending (N)
                    tags.append(f"{syllable}\\N")
                else:  # Other (O)
                    tags.append(f"{syllable}\\O")
    return " ".join(tags)


def process_sentence(sentence, break_pattern, pattern):
    """Process a single sentence for syllable segmentation and tagging."""
    # Remove tags and join words
    cleaned_sentence = remove_tags_and_join(sentence)

    # Segment the cleaned sentence into syllables
    syllables = syllable_segment(cleaned_sentence, break_pattern)

    # Tag the segmented syllables
    return tag_sentence(syllables, pattern)


def process_file(input_file, output_file, break_pattern, pattern):
    """Process the input file line by line and write the result to the output file."""
    with open(input_file, 'r', encoding='utf-8') as infile, open(output_file, 'w', encoding='utf-8') as outfile:
        for line in infile:
            # Split the line into sentences using "\E" as the delimiter
            sentences = line.strip().split("\\E")
            tagged_sentences = [
                process_sentence(sentence.strip(), break_pattern, pattern) for sentence in sentences if sentence.strip()
            ]
            outfile.write(" ".join(tagged_sentences) + "\n")


if __name__ == "__main__":
    args = parse_arguments()
    break_pattern = create_break_pattern()
    process_file(args.input, args.output, break_pattern, args.pattern)

```

the above code is working well. However, when compete F and N tags in BFONE pattern, F got more weight as follows:  

```
ဘယ်\B လောက်\F နောက်\F ကျ\F သ\N လဲ\E
```

at that case, we want followings output:  

```
ဘယ်\B လောက်\F နောက်\N ကျ\N သ\N လဲ\E
```

## Code Updating  

```python
            elif pattern == "BFONE":
                if i <= 3:  # Near Beginning (F)
                    tags.append(f"{syllable}\\F")
                elif n - i <= 3:  # Near Ending (N)
                    tags.append(f"{syllable}\\N")
                else:  # Other (O)
                    tags.append(f"{syllable}\\O")
```

အထက်ပါ code ကို အောက်ပါအတိုင်း update လုပ်ခဲ့တယ်။  

```python
        else:
            if pattern == "BONE":
                if n - i <= 4:  # Near Ending (N)
                    tags.append(f"{syllable}\\N")
                else:  # Other (O)
                    tags.append(f"{syllable}\\O")
            elif pattern == "BFONE":
                if n - i <= 4:  # Near Ending (N)
                    tags.append(f"{syllable}\\N")
                elif i <= 3:  # Near Beginning (F)
                    tags.append(f"{syllable}\\F")
                else:  # Other (O)
                    tags.append(f"{syllable}\\O")
    return " ".join(tags)
```

## Check Syllable Segmented, Tagged Outputs  

for BONE Pattern:  

```
ရင်\B ဘတ်\O အော\O င့်\O လာ\O ရင်\O သ\N တိ\N ထား\N ပါ\E
ဘယ်\B လောက်\O နောက်\N ကျ\N သ\N လဲ\E
ကြို\B ပို့\O ဘတ်စ်\O ကား\O က\O အ\O ဆင်\O အ\N ပြေ\N ဆုံး\N ပဲ\E
အဲ\B ဒီ\O အ\O ဖွဲ့\O ရဲ့\O ဥက္ကဋ္ဌ\O ဖြစ်\O တဲ့\O ယို\O ကို\O ယာ\O မာ့\O အာ\O ကိ\O ဟီ\O တို\O YokoyamaAkihito\O က\O တ\O ခြား\O နိုင်\O ငံ\O တွေ\O မှာ\O ဖြစ်\O ပွား\O တဲ့\O လူ\O နာ\O တွေ\O ရဲ့\O အ\O ဆုတ်\O လုပ်\O ဆောင်\O ပုံ\O တွေ\O က\O ဗိုင်း\O ရပ်စ်\O ကူး\O စက်\O ခံ\O ရ\O ပြီး\O ကု\O သ\O လိုက်\O လို့\O ရော\O ဂါ\O ပိုး\O မ\O ရှိ\O တော့\O ဘူး\O လို့\O စစ်\O ဆေး\O ပြီး\O နောက်\O မှာ\O တောင်\O မှ\O အ\O ဆုတ်\O က\O အ\O ပြည့်\O အ\O ဝ\O ပုံ\O မှန်\O ပြန်\O ဖြစ်\O မ\O လာ\O တဲ့\O လူ\O နာ\O တွေ\O အ\O များ\O အ\O ပြား\O တွေ့\O ရ\O တယ်\O လို့\N ပြော\N ပါ\N တယ်\E
အ\B ဆ\O င့်\O အေ\O ဝင်\O ငွေ\O ခွန်\O ကို\O လ\O စာ\O မှ\N ဖြတ်\N တောက်\N သည်\E
လို\B ကီ\O က\O အတ်\O ဂါ\O ဒါ\O လို\O ကီ\O ရဲ့\O မျက်\O လုံး\O တွေ\O ကို\O သေ\O ချာ\O တ\O ည့်\O တ\O ည့်\O ကြ\O ည့်\O ရင်း\O ငါ\N က\N လို\N ကီ\E
ခင်\B ဗျား\O ကြိုက်\O တဲ့\O အ\O ရောင်\N က\N ဘာ\N လဲ\E
သူ\B သီ\O ချင်း\O ဆို\O တတ်\O သ\O လို\O က\O လည်း\N က\N တတ်\N သည်\E
ထို့\B ကြောင့်\O ဥ\O ပါယ်\O ဂို့\O ဟု\O ခေါ်\O ကာ\O ကာ\O လ\O ကြာ\O သော်\O ဥ\O ပါယ်\O ဂို့\O မှ\O ပ\O ဂိုး\O ဟု\O ပြောင်း\O လဲ\O ခေါ်\N လာ\N ကြ\N သည်\E
ဒီ\B နေ့\O ခင်\O ဗျား\O ဘယ်\O လို\O ဖြစ်\N နေ\N တာ\N လဲ\E

```

for BFONE Pattern:  

```
ရင်\B ဘတ်\F အော\F င့်\F လာ\O ရင်\O သ\N တိ\N ထား\N ပါ\E
ဘယ်\B လောက်\F နောက်\N ကျ\N သ\N လဲ\E
ကြို\B ပို့\F ဘတ်စ်\F ကား\F က\O အ\O ဆင်\O အ\N ပြေ\N ဆုံး\N ပဲ\E
အဲ\B ဒီ\F အ\F ဖွဲ့\F ရဲ့\O ဥက္ကဋ္ဌ\O ဖြစ်\O တဲ့\O ယို\O ကို\O ယာ\O မာ့\O အာ\O ကိ\O ဟီ\O တို\O YokoyamaAkihito\O က\O တ\O ခြား\O နိုင်\O ငံ\O တွေ\O မှာ\O ဖြစ်\O ပွား\O တဲ့\O လူ\O နာ\O တွေ\O ရဲ့\O အ\O ဆုတ်\O လုပ်\O ဆောင်\O ပုံ\O တွေ\O က\O ဗိုင်း\O ရပ်စ်\O ကူး\O စက်\O ခံ\O ရ\O ပြီး\O ကု\O သ\O လိုက်\O လို့\O ရော\O ဂါ\O ပိုး\O မ\O ရှိ\O တော့\O ဘူး\O လို့\O စစ်\O ဆေး\O ပြီး\O နောက်\O မှာ\O တောင်\O မှ\O အ\O ဆုတ်\O က\O အ\O ပြည့်\O အ\O ဝ\O ပုံ\O မှန်\O ပြန်\O ဖြစ်\O မ\O လာ\O တဲ့\O လူ\O နာ\O တွေ\O အ\O များ\O အ\O ပြား\O တွေ့\O ရ\O တယ်\O လို့\N ပြော\N ပါ\N တယ်\E
အ\B ဆ\F င့်\F အေ\F ဝင်\O ငွေ\O ခွန်\O ကို\O လ\O စာ\O မှ\N ဖြတ်\N တောက်\N သည်\E
လို\B ကီ\F က\F အတ်\F ဂါ\O ဒါ\O လို\O ကီ\O ရဲ့\O မျက်\O လုံး\O တွေ\O ကို\O သေ\O ချာ\O တ\O ည့်\O တ\O ည့်\O ကြ\O ည့်\O ရင်း\O ငါ\N က\N လို\N ကီ\E
ခင်\B ဗျား\F ကြိုက်\F တဲ့\F အ\O ရောင်\N က\N ဘာ\N လဲ\E
သူ\B သီ\F ချင်း\F ဆို\F တတ်\O သ\O လို\O က\O လည်း\N က\N တတ်\N သည်\E
ထို့\B ကြောင့်\F ဥ\F ပါယ်\F ဂို့\O ဟု\O ခေါ်\O ကာ\O ကာ\O လ\O ကြာ\O သော်\O ဥ\O ပါယ်\O ဂို့\O မှ\O ပ\O ဂိုး\O ဟု\O ပြောင်း\O လဲ\O ခေါ်\N လာ\N ကြ\N သည်\E
ဒီ\B နေ့\F ခင်\F ဗျား\F ဘယ်\O လို\O ဖြစ်\N နေ\N တာ\N လဲ\E
```

## Error Found for Paragraph Level

Multiple Sentence တွေ ပါနေတဲ့ စာပိုဒ် level မှာ error သွားတွေ့ရတယ်။  
ဥပမာ Sentence No. 16 of test.tagged (i.e. word level)  

Input:  
```
သူမ/B သူငယ်ချင်း/O များ/O တွင်/O မ/O တော့/O ဘုန်းကြီး/O ဝတ်/O သွား/O သော/O ဗေဒင်/O တတ်/O သည့်/O အဘိုး/O မ/O ရှိ/O ၍/O ပဲ/N လား/N မ/N သိ/E နာမည်/B လှလှ/O ကလေး/O တွေ/N နှင့်/N ဖြစ်/N သည်/E တခြား/B မိန်းကလေး/O တွေ/O ရဲ့/O နာမည်/O တွေ/O က/O လည်း/O မ/O ကောင်း/O ရင်/O သာ/N ရှိ/N ရ/N မည်/E
```

Bone Output:  
```
သူ\B မ\O သူ\O ငယ်\O ချင်း\O များ\O တွင်\O မ\O တော့\O ဘုန်း\O ကြီး\O ဝတ်\O သွား\O သော\O ဗေ\O ဒင်\O တတ်\O သ\O ည့်\O အ\O ဘိုး\O မ\O ရှိ\O ၍\O ပဲ\O လား\O မ\O သိ\O နာ\O မည်\O လှ\O လှ\O က\O လေး\O တွေ\O နှ\O င့်\O ဖြစ်\O သည်\O တ\O ခြား\O မိန်း\O က\O လေး\O တွေ\O ရဲ့\O နာ\O မည်\O တွေ\O က\O လည်း\O မ\O ကောင်း\O ရင်\O သာ\N ရှိ\N ရ\N မည်\E
```

Bfone Output:  
```
သူ\B မ\F သူ\F ငယ်\F ချင်း\O များ\O တွင်\O မ\O တော့\O ဘုန်း\O ကြီး\O ဝတ်\O သွား\O သော\O ဗေ\O ဒင်\O တတ်\O သ\O ည့်\O အ\O ဘိုး\O မ\O ရှိ\O ၍\O ပဲ\O လား\O မ\O သိ\O နာ\O မည်\O လှ\O လှ\O က\O လေး\O တွေ\O နှ\O င့်\O ဖြစ်\O သည်\O တ\O ခြား\O မိန်း\O က\O လေး\O တွေ\O ရဲ့\O နာ\O မည်\O တွေ\O က\O လည်း\O မ\O ကောင်း\O ရင်\O သာ\N ရှိ\N ရ\N မည်\E

```

## Debugging the Code   

I updated the code and the following code is working well ...  

```python
#!/usr/bin/env python3
# -*- coding:utf-8 -*-

import argparse
import re

def parse_arguments():
    """Parse command line arguments."""
    parser = argparse.ArgumentParser(description="Convert word-tagged Burmese data to syllable-tagged data.")
    parser.add_argument("-i", "--input", type=str, required=True, help="Input file (word-tagged data)")
    parser.add_argument("-o", "--output", type=str, required=True, help="Output file (syllable-tagged data)")
    parser.add_argument("-p", "--pattern", type=str, choices=["BONE", "BFONE"], default="BONE",
                        help="Tagging pattern: BONE or BFONE (default: BONE)")
    return parser.parse_args()

def create_break_pattern():
    """Create the regular expression pattern for syllable segmentation."""
    my_consonant = r"က-အ"
    en_no = r"0-9"
    other_char = r"ဣဤဥဦဧဩဪဿ၌၍၏၀-၉၊။!-/:-@[-`{-~\\s"
    subscript_symbol = r'္'
    a_that = r'်'

    return re.compile(
        r"((?<!"
        + subscript_symbol
        + r")["
        + my_consonant
        + r"](?!["
        + a_that
        + subscript_symbol
        + r"])|["
        + en_no
        + other_char
        + r"])"
    )

def syllable_segment(sentence, break_pattern):
    """Segment a sentence into syllables."""
    return break_pattern.sub(r" \1", sentence).strip().split()

def remove_tags_and_join(sentence):
    """Remove tags and join words into a tag-free sentence."""
    words = sentence.strip().split()
    cleaned_words = [word.split('/')[0] for word in words if '/' in word]  # Remove tags
    return " ".join(cleaned_words)

def tag_sentence(syllables, pattern):
    """Tag the syllables based on the selected pattern."""
    n = len(syllables)
    print("syllables:", syllables)
    print("n:", n)
    tags = []

    for i, syllable in enumerate(syllables):
        if i == 0:
            tags.append(f"{syllable}/B")  # Beginning
        elif i == n - 1:
            tags.append(f"{syllable}/E")  # Ending
        else:
            if pattern == "BONE":
                if n - i <= 4:  # Near Ending (N)
                    tags.append(f"{syllable}/N")
                else:  # Other (O)
                    tags.append(f"{syllable}/O")
            elif pattern == "BFONE":
                if n - i <= 4:  # Near Ending (N)
                    tags.append(f"{syllable}/N")
                elif i <= 3:  # Near Beginning (F)
                    tags.append(f"{syllable}/F")
                else:  # Other (O)
                    tags.append(f"{syllable}/O")
    return " ".join(tags)

def process_sentence(sentence, break_pattern, pattern):
    """Process a single sentence for syllable segmentation and tagging."""
    # Remove tags and join words
    cleaned_sentence = remove_tags_and_join(sentence)

    # Segment the cleaned sentence into syllables
    syllables = syllable_segment(cleaned_sentence, break_pattern)

    # Tag the segmented syllables
    return tag_sentence(syllables, pattern)

#def process_file(input_file, output_file, break_pattern, pattern):
#    """Process the input file line by line and write the result to the output file."""
#    with open(input_file, 'r', encoding='utf-8') as infile, open(output_file, 'w', encoding='utf-8') as outfile:
#        for line in infile:
            # Debugging print: Split the line by \E, treating it as individual sentences
#            sentences = re.split(r"\/E", line.strip())  # Properly split by \E
#            print("sentences:", sentences)  # Debugging

            # Process each sentence individually
#            tagged_sentences = [
#                process_sentence(sentence.strip(), break_pattern, pattern) for sentence in sentences if sentence.strip()
#            ]
#            outfile.write(" ".join(tagged_sentences) + "\n")

def process_file(input_file, output_file, break_pattern, pattern):
    """Process the input file line by line and write the result to the output file."""
    with open(input_file, 'r', encoding='utf-8') as infile, open(output_file, 'w', encoding='utf-8') as outfile:
        for line in infile:
            line = line.strip()

            # Split by "/E", but keep "/E" in the split sentences
            sentences = []
            temp_sentence = ''
            for word in line.split():
                if word.endswith('/E'):
                    # Add the word with "/E" at the end and finalize the sentence
                    temp_sentence += word
                    sentences.append(temp_sentence.strip())
                    temp_sentence = ''
                else:
                    # Add word to the temporary sentence
                    temp_sentence += word + ' '

            # If there's any leftover sentence that doesn't end with "/E"
            if temp_sentence.strip():
                sentences.append(temp_sentence.strip())

            print("sentences:", sentences)  # Debugging

            # Process the sentences and write to the output
            tagged_sentences = [
                process_sentence(sentence.strip(), break_pattern, pattern) for sentence in sentences if sentence.strip()
            ]
            outfile.write(" ".join(tagged_sentences) + "\n")


#def process_file(input_file, output_file, break_pattern, pattern):
#    """Process the input file line by line and write the result to the output file."""
#    with open(input_file, 'r', encoding='utf-8') as infile, open(output_file, 'w', encoding='utf-8') as outfile:
#        for line in infile:
            # Split the line into sentences using "\E" as the delimiter
#            sentences = line.strip().split("\/E")
#            print("sentences:", sentences)
#            tagged_sentences = [
#                process_sentence(sentence.strip(), break_pattern, pattern) for sentence in sentences if sentence.strip()
#            ]
#            outfile.write(" ".join(tagged_sentences) + "\n")

if __name__ == "__main__":
    args = parse_arguments()
    break_pattern = create_break_pattern()
    process_file(args.input, args.output, break_pattern, args.pattern)
```

Polishing/Cleaning the code ...  

```python
#!/usr/bin/env python3
# -*- coding:utf-8 -*-

"""

For converting word level tagged sentences into syllable level sentences.
Written by Ye Kyaw Thu, LST Lab, NECTEC, Thailand.
Last updated: 5 Dec 2024.

How to use:  
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ time python ./wordtag2syltag.py -i ./test.tagged -o test.tagged.bone -p BONE
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ time python ./wordtag2syltag.py -i ./test.tagged -o test.tagged.bfone -p BFONE

"""

import argparse
import re

def parse_arguments():
    """Parse command line arguments."""
    parser = argparse.ArgumentParser(description="Convert word-tagged Burmese data to syllable-tagged data.")
    parser.add_argument("-i", "--input", type=str, required=True, help="Input file (word-tagged data)")
    parser.add_argument("-o", "--output", type=str, required=True, help="Output file (syllable-tagged data)")
    parser.add_argument("-p", "--pattern", type=str, choices=["BONE", "BFONE"], default="BONE",
                        help="Tagging pattern: BONE or BFONE (default: BONE)")
    return parser.parse_args()

def create_break_pattern():
    """Create the regular expression pattern for syllable segmentation."""
    my_consonant = r"က-အ"
    en_no = r"0-9"
    other_char = r"ဣဤဥဦဧဩဪဿ၌၍၏၀-၉၊။!-/:-@[-`{-~\\s"
    subscript_symbol = r'္'
    a_that = r'်'

    return re.compile(
        r"((?<!"
        + subscript_symbol
        + r")["
        + my_consonant
        + r"](?!["
        + a_that
        + subscript_symbol
        + r"])|["
        + en_no
        + other_char
        + r"])"
    )

def syllable_segment(sentence, break_pattern):
    """Segment a sentence into syllables."""
    return break_pattern.sub(r" \1", sentence).strip().split()

def remove_tags_and_join(sentence):
    """Remove tags and join words into a tag-free sentence."""
    words = sentence.strip().split()
    cleaned_words = [word.split('/')[0] for word in words if '/' in word]  # Remove tags
    return " ".join(cleaned_words)

def tag_sentence(syllables, pattern):
    """Tag the syllables based on the selected pattern."""
    n = len(syllables)
    #print("syllables:", syllables) # Debugging
    #print("n:", n) # Debugging
    tags = []

    for i, syllable in enumerate(syllables):
        if i == 0:
            tags.append(f"{syllable}/B")  # Beginning
        elif i == n - 1:
            tags.append(f"{syllable}/E")  # Ending
        else:
            if pattern == "BONE":
                if n - i <= 4:  # Near Ending (N)
                    tags.append(f"{syllable}/N")
                else:  # Other (O)
                    tags.append(f"{syllable}/O")
            elif pattern == "BFONE":
                if n - i <= 4:  # Near Ending (N)
                    tags.append(f"{syllable}/N")
                elif i <= 3:  # Near Beginning (F)
                    tags.append(f"{syllable}/F")
                else:  # Other (O)
                    tags.append(f"{syllable}/O")
    return " ".join(tags)

def process_sentence(sentence, break_pattern, pattern):
    """Process a single sentence for syllable segmentation and tagging."""
    # Remove tags and join words
    cleaned_sentence = remove_tags_and_join(sentence)

    # Segment the cleaned sentence into syllables
    syllables = syllable_segment(cleaned_sentence, break_pattern)

    # Tag the segmented syllables
    return tag_sentence(syllables, pattern)

def process_file(input_file, output_file, break_pattern, pattern):
    """Process the input file line by line and write the result to the output file."""
    with open(input_file, 'r', encoding='utf-8') as infile, open(output_file, 'w', encoding='utf-8') as outfile:
        for line in infile:
            line = line.strip()

            # Split by "/E", but keep "/E" in the split sentences
            sentences = []
            temp_sentence = ''
            for word in line.split():
                if word.endswith('/E'):
                    # Add the word with "/E" at the end and finalize the sentence
                    temp_sentence += word
                    sentences.append(temp_sentence.strip())
                    temp_sentence = ''
                else:
                    # Add word to the temporary sentence
                    temp_sentence += word + ' '

            # If there's any leftover sentence that doesn't end with "/E"
            if temp_sentence.strip():
                sentences.append(temp_sentence.strip())

            #print("sentences:", sentences)  # Debugging

            # Process the sentences and write to the output
            tagged_sentences = [
                process_sentence(sentence.strip(), break_pattern, pattern) for sentence in sentences if sentence.strip()
            ]
            outfile.write(" ".join(tagged_sentences) + "\n")


if __name__ == "__main__":
    args = parse_arguments()
    break_pattern = create_break_pattern()
    process_file(args.input, args.output, break_pattern, args.pattern)
```

## Test Run Again  

bash shell script ပြင်ဆင်ခဲ့...  
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ cat run-wordtag2syltag.sh  

```bash
#!/bin/bash

set -x;

# Running for training data:
time python ./wordtag2syltag.py -i ./train-valid.tagged -o train-valid.tagged.bone -p BONE;
time python ./wordtag2syltag.py -i ./train-valid.tagged -o train-valid.tagged.bfone -p BFONE;

# Running for test data:
time python ./wordtag2syltag.py -i ./test.tagged -o test.tagged.bone -p BONE;
time python ./wordtag2syltag.py -i ./test.tagged -o test.tagged.bfone -p BFONE;

set +x;
```

Running ...  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ time ./run-wordtag2syltag.sh
+ python ./wordtag2syltag.py -i ./train-valid.tagged -o train-valid.tagged.bone -p BONE

real    0m4.068s
user    0m4.023s
sys     0m0.045s
+ python ./wordtag2syltag.py -i ./train-valid.tagged -o train-valid.tagged.bfone -p BFONE

real    0m3.901s
user    0m3.868s
sys     0m0.032s
+ python ./wordtag2syltag.py -i ./test.tagged -o test.tagged.bone -p BONE

real    0m0.455s
user    0m0.435s
sys     0m0.020s
+ python ./wordtag2syltag.py -i ./test.tagged -o test.tagged.bfone -p BFONE

real    0m0.457s
user    0m0.453s
sys     0m0.004s
+ set +x

real    0m8.885s
user    0m8.780s
sys     0m0.104s
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$
```

Check filesizes:  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ wc train-valid.tagged
   50081   896088 14613857 train-valid.tagged
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ wc train-valid.tagged.{bone,bfone}
   50081  1348989 15972560 train-valid.tagged.bone
   50081  1348989 15972560 train-valid.tagged.bfone
  100162  2697978 31945120 total
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$
```

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ wc test.tagged
   5512   96647 1573446 test.tagged
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ wc test.tagged.{bone,bfone}
   5512  145367 1719606 test.tagged.bone
   5512  145367 1719606 test.tagged.bfone
  11024  290734 3439212 total
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$
```

Word level tagged ဒေတာဖိုင်ကို syllable level tagged ဒေတာဖိုင်အဖြစ် ပြောင်းတဲ့ အလုပ်ပြီးသွားပြီ။  

working path:  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ pwd
/home/ye/data/hello-sayarwon/coding/model-based/data  
```

## Create Normalizer Library    

လက်တွေ့မှာက Normalization အရင် လုပ်ပြီးမှပဲ conversion လုပ်ရမှာမို့ normalization code ကို library အဖြစ် ပြောင်းရမယ်။  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/normalizer4thura$ ls
chk_normalize.py                           note.txt       real_err1.syl.normalized
final_syl_dictionary_13Feb2024.sorted.txt  real_err1.syl  syllable_checked_result.txt
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/normalizer4thura$ pwd
/home/ye/data/hello-sayarwon/coding/normalizer4thura
```

အရင်ဆုံး ရှိပြီးသား normalizer ကို library အဖြစ်ဆောက်ခဲ့တယ်။  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ ls ./normalizer/
final_syl_dictionary_13Feb2024.sorted.txt  __init__.py  normalizer.py  __pycache__  syllable_checker.py
```

syllable_checker.py code က အောက်ပါအတိုင်းပါ။  

```python
import re

class BurmeseSyllableChecker:
    def __init__(self, dictionary_file, min_frequency=2):
        C = r'[က-အ]'  # Consonants
        M = r'(ျ|ြ)?ွ?ှ?'  # Medials
        V = r'ေ?(?!ီူ|ီု)(ါ|ာ)?(ို|ိ|ီ|ဲ)?(ု|ူ)?'  # Vowels
        F = r'[ံ့]?း?'  # Final consonants and signs
        A = r'်'  # Asat
        S = r'္'  # Sa-lon
        G = r'ဿ'  # Great SA
        IVS = r'([ဣဤဥဦဧဩဪ၌၍၏၎]+)?'  # Independent Vowels before Subscripts
        SUB = r'((?:{C}{S}{C})+)'.format(C=C, S=S)  # Subscript syllables, allowing for multiple
        KZ = r'င်္'

        # Merging the Complex pattern for better handling of various cases
        Complex = r'(' \
                  f"{IVS}?" \
                  f"(?:{C}{M}?{V}?{F}?)*" \
                  f"(?:{SUB}{V}?{F}?)*" \
                  f"|{G}{V}?" \
                  f"|{KZ}{C}{S}{C}(?:{V}?{F}?)*" \
                  f"|{C}{S}{C}{V}{F}?" \
                  f"|{C}{M}?{V}?{F}?{A}?" \
                  f"|{C}{C}{A}{C}{M}{A}" \
                  f"|{SUB}{C}{A}" \
                  f"|{C}{M}{M}{C}{A}{V}{C}{A}" \
                  f"|{C}{SUB}{C}{A}{F}?" \
                  f"|{IVS}{SUB}{C}" \
                  f"|{C}{SUB}*{V}{C}{A}{F}?" \
                  f"|{C}{KZ}{C}{SUB}" \
                  r')'

        self.patterns = {
            'C': C,
            'M': M,
            'V': V,
            'F': F,
            'A': A,
            'S': S,
            'G': G,
            'I': r'[ဤဧဪ၌၍၏]',  # Independent vowels
            'E': r'[ဣဥဦဩ၎]',  # Independent vowels with "အ"
            'D': r'[၀-၉]',  # Digits
            'P': r'[၊။]',  # Punctuation
            'SUB': SUB,
            'IVS': IVS,
            'Complex': Complex,
            'K': r'({C}{M}?{KZ}{C}{M}?{V}?{A}?[ံ့း]?({C}{A}း?)?)'.format(C=C, M=M, V=V, A=A, KZ=KZ),
            'CA': r'({C}{M}{V}{F}?{C}{A}း?)'.format(C=C, M=M, V=V, F=F, A=A)
        }

        self.syllable_regex = re.compile(
            f"^("
            f"{Complex}|"
            f"{IVS}{C}{M}{V}{F}{A}?|"
            f"{self.patterns['E']}{C}?{A}?{F}|"
            f"{self.patterns['I']}|"
            f"{self.patterns['D']}|"
            f"{self.patterns['P']}|"
            f"{self.patterns['CA']}|"
            f"{self.patterns['K']}"
            f")$",
            re.UNICODE
        )

        self.dictionary = {}
        with open(dictionary_file, 'r', encoding='utf-8') as f:
            for line in f:
                syllable, frequency = line.strip().split()
                frequency = int(frequency)
                if frequency >= min_frequency:
                    self.dictionary[syllable] = frequency

    def check_syllable(self, syllable):
        if self.syllable_regex.fullmatch(syllable) and syllable in self.dictionary:
        #if syllable in self.dictionary:
            return syllable
        else:
            return f"<{syllable}>"


```

normalizer.py က အောက်ပါအတိုင်း...  

```python
import re
from .syllable_checker import BurmeseSyllableChecker

class BurmeseNormalizer:
    def __init__(self):
        self.rules = [
            # Rule 1 (Updated)
            {'pattern': r'[\u200B\u200C\u202C\u00A0\u200D\u200A]', 'repl': ''},
            # Rule 2
            {'pattern': r'([ခဂငပဒဝ])ာ', 'repl': r'\1ါ'},
            # Rule 3
            {'pattern': r'(ျ|ြ)([က-အ])', 'repl': r'\2\1'},
            # Rule 4
            {'pattern': r'ေ([က-အ][ျြ]*)', 'repl': r'\1ေ'},
            # Rule 5
            {'pattern': r'့်', 'repl': '့်'},
            # Rule 6
            {'pattern': r'ှွ', 'repl': 'ွှ'},
            # Rule 7
            {'pattern': r'ှျ', 'repl': 'ျှ'},
            # Rule 8
            {'pattern': r'ှြ', 'repl': 'ြှ'},
            # Rule 9
            {'pattern': r'ဦ', 'repl': 'ဦ'},
            # Rule 10
            {'pattern': r'့ာ', 'repl': 'ာ့'},
            # Rule 11
            {'pattern': r'([က-အဿ])ံု', 'repl': r'\1ုံ'},
            # Rule 12
            {'pattern': r'([က-အဿ])ိ့ု', 'repl': r'\1ို့'},
            # Rule 13
            {'pattern': r'([က-အဿ])ံွ', 'repl': r'\1ွံ'},
            # Rule 14
            {'pattern': r'(ိ|ီ)ူ', 'repl': r'\1ု'},
            # Rule 15
            {'pattern': r'([\u102B-\u103E])\1+', 'repl': r'\1'},
            # Rule 16
            {'pattern': r'၇(?=[က-အ]*[\u102B-\u103E]+)', 'repl': 'ရ'},
            # Rule 17
            {'pattern': r'ဥ်', 'repl': 'ဉ်'},
            # Rule 18
            {'pattern': r'ဥာ', 'repl': 'ဉာ'},
            # Rule 19
            {'pattern': r'ေ([က-အ])ျ', 'repl': r'\1ျေ'},
            # Rule 20
            {'pattern': r'တကသိုလ်', 'repl': 'တက္ကသိုလ်'},
            # Rule 21
            {'pattern': r'tတ်', 'repl': 'သတ်'},
            # Rule 22
            {'pattern': r'ေt', 'repl': 'သေ'},
            # Rule 23
            {'pattern': r'ေsာက်', 'repl': 'စောက်'},
            # Rule 24
            {'pattern': r'သြ', 'repl': 'ဩ'},
            # Rule 25
            {'pattern': r'သြော်', 'repl': 'ဪ'},
            # Rule 26
            {'pattern': r'၄င်း', 'repl': '၎င်း'},
            # Rule 27
            {'pattern': r'([က-အ])ံွ့', 'repl': r'\1ွံ့'},
            # Rule 28
            {'pattern': r'စျ', 'repl': 'ဈ'},
            # Rule 29
            {'pattern': r'ဏာန်း', 'repl': 'ဏန်း'},
            # Rule 30
            {'pattern': r'([က-အ])ာ်', 'repl': r'\1ော်'},
            # Rule 31
            {'pattern': r'ဆဥ်', 'repl': 'ဆင်'},
            # Rule 33
            {'pattern': r'ုိး', 'repl': 'ိုး'},
            # Rule 34
            {'pattern': r'ီုး', 'repl': 'ိုး'},
            # Rule 35
            {'pattern': r'ိး', 'repl': 'ီး'},
            # Rule 36
            {'pattern': r'ဲ([၊။])့', 'repl': r'ဲ့\1'},
            # Rule 37
            {'pattern': r'၀([\u102B-\u103E])', 'repl': r'ဝ\1'},
            # Rule 38
            {'pattern': r'(ေ-ခွး|ခဝေး|ေ_ခွး)', 'repl': 'ခွေး'},
            # Rule 39
            {'pattern': r'(?<![က-အ])(\u1004)(\u1031)(\u103A)(\u1039)([\u1000-\u1021])', 'repl': r'\1\3\4\5\2'},
            # New Rule 40
            {'pattern': r'([က-အ])([က-အ])([ျြ])်', 'repl': r'\1\3\2်'},
            # New Rule 41
            {'pattern': r'ေ([က-အ])ြ', 'repl': r'\1ြေ'},
            # New Rule 42
            {'pattern': r'ာွ', 'repl': r'ွာ'},
            # New Rule 43
           {'pattern': r'မ႓ာ', 'repl': r'မ္ဘာ့'},

    ]

    def normalize(self, input_text):
        # Split input text into lines
        lines = input_text.split('\n')
        output_lines = []

        for line in lines:
            # Split each line into words based on spaces
            words = line.split()
            normalized_words = []

            for word in words:
                # Apply normalization rules to each word
                for rule in self.rules:
                    word = re.sub(rule['pattern'], rule['repl'], word)

                normalized_words.append(word)

            # Join the normalized words back into a line
            normalized_line = ' '.join(normalized_words)
            output_lines.append(normalized_line)

        # Join the normalized lines back into a single string
        output_text = '\n'.join(output_lines)
        return output_text


def process_input(input_text, dictionary_file, min_frequency=2, check='dictionary'):
    checker = BurmeseSyllableChecker(dictionary_file, min_frequency)
    normalizer = BurmeseNormalizer()

    lines = input_text.splitlines()
    results = []

    # Check syllables using the dictionary and/or regex
    for line in lines:
        syllables = line.split()
        if check == 'RE_and_dictionary':
            result = [checker.check_syllable(s) for s in syllables]
        else:
            result = [s if s in checker.dictionary else f"<{s}>" for s in syllables]
        results.append(' '.join(result))

    # Normalize the checked lines
    normalized_lines = []
    for line in results:
        if '<' in line:  # Handle unrecognized syllables marked with `< >`
            cleaned_line = line.replace('<', '').replace('>', '')
            normalized_lines.append(normalizer.normalize(cleaned_line))
        else:
            normalized_lines.append(normalizer.normalize(line))

    return '\n'.join(normalized_lines)


```
test code က အောက်ပါအတိုင်း...  

(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ cat tst-normalizer.py  

```python
from normalizer import process_input

input_text = "မြန်မာစာ စာကြောင်း"
dictionary_file = "./normalizer/final_syl_dictionary_13Feb2024.sorted.txt"

result = process_input(input_text, dictionary_file, min_frequency=2, check='dictionary')
print(result)
```

file input နဲ့ run လို့ ရဖို့ ပြင်ဆင်ခဲ့...  

```python
"""

Testing Normalizer library.
Written by Ye Kyaw Thu, Visiting Professor, LST, NECTEC, Thailand.
Last updated: 5 Dec 2024

How to run:  
python ./tst-normalizer-file.py -i ./tst4normalizer.txt  
python ./tst-normalizer-file.py -i ./tst4normalizer.txt -o tst4normalizer.out  
cat ./tst4normalizer.txt | python ./tst-normalizer-file.py  
python ./tst-normalizer-file.py -i ./tst4normalizer.txt -d your_dictionary.txt  
python tst-normalizer.py -i ./tst4normalizer.txt -f 3  
python ./tst-normalizer-file.py --help  

"""

import argparse
import sys
from normalizer import process_input

def main():
    # Argument parser setup
    parser = argparse.ArgumentParser(description="Test Burmese normalizer library.")
    parser.add_argument(
        '-i', '--input', 
        type=str, 
        help="Input file containing text. If not provided, input will be read from stdin."
    )
    parser.add_argument(
        '-o', '--output', 
        type=str, 
        help="Output file to save normalized text. If not provided, output will be printed to stdout."
    )
    parser.add_argument(
        '-d', '--dictionary', 
        type=str, 
        default="./normalizer/final_syl_dictionary_13Feb2024.sorted.txt",
        help="Path to the syllable dictionary file (default: ./normalizer/final_syl_dictionary_13Feb2024.sorted.txt)."
    )
    parser.add_argument(
        '-f', '--frequency', 
        type=int, 
        default=2, 
        help="Minimum frequency for syllable acceptance (default: 2)."
    )
    parser.add_argument(
        '-c', '--check', 
        choices=['dictionary', 'RE_and_dictionary'], 
        default='dictionary',
        help="Check mode: 'dictionary' or 'RE_and_dictionary' (default: dictionary)."
    )
    args = parser.parse_args()

    # Read input
    if args.input:
        with open(args.input, 'r', encoding='utf-8') as infile:
            input_text = infile.read()
    else:
        input_text = sys.stdin.read()

    # Process input
    normalized_text = process_input(
        input_text, 
        dictionary_file=args.dictionary, 
        min_frequency=args.frequency, 
        check=args.check
    )

    # Write or print output
    if args.output:
        with open(args.output, 'w', encoding='utf-8') as outfile:
            outfile.write(normalized_text)
    else:
        print(normalized_text)

if __name__ == "__main__":
    main()


```

## Testing Normalizer with File Input  

အရင်ဆုံး --help ခေါ်ကြည်...  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ python ./tst-normalizer-file.py --help
usage: tst-normalizer-file.py [-h] [-i INPUT] [-o OUTPUT] [-d DICTIONARY] [-f FREQUENCY]
                              [-c {dictionary,RE_and_dictionary}]

Test Burmese normalizer library.

optional arguments:
  -h, --help            show this help message and exit
  -i INPUT, --input INPUT
                        Input file containing text. If not provided, input will be read from stdin.
  -o OUTPUT, --output OUTPUT
                        Output file to save normalized text. If not provided, output will be printed to
                        stdout.
  -d DICTIONARY, --dictionary DICTIONARY
                        Path to the syllable dictionary file (default:
                        ./normalizer/final_syl_dictionary_13Feb2024.sorted.txt).
  -f FREQUENCY, --frequency FREQUENCY
                        Minimum frequency for syllable acceptance (default: 2).
  -c {dictionary,RE_and_dictionary}, --check {dictionary,RE_and_dictionary}
                        Check mode: 'dictionary' or 'RE_and_dictionary' (default: dictionary).
```

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ cat ./tst4normalizer.txt | python ./tst-normalizer-file.py
လက် ရေး ကို ဖြစ် သ လို ရေး လို့ ဘာ အ ကြောင်း အ ရာ မှန်း မ သိ တော့ ဘူး ။
ဒီ ဓာတ် ပုံ ကို တည်း ဖြတ် သူ က တော့ ကျောင်း လော က မှာ ကျော် ကြား တဲ့ ပ ရော် ဖက် ဆာ ဘတ် ဖြစ် ပါ တယ် ။
ကို ယ့် ကိုယ် ကို ယုံ ကြည် ချက် အ ပြ ည့် ရှိ သည် ။ 자신 만만하다 .
အ မျိုး သ မီး အ ဝတ် အ စား ရောင်း တဲ့ နေ ရာ က ဘယ် မှာ ရှိ ပါ သ လဲ ။
ကု လား ထိုင် ထော င့် ကို ရွှေ့ သည် ။ 의자를 구석으로 옮기다 .
အဲ ဒါ ကျွန် တော့် ဟာ ပါ ။
သူ က အ ဝတ် ဈေး ကို မြှ င့် လိုက် နှိ မ့် လိုက် နဲ့ စိတ် တိုင်း ကျ ကို လုပ် နေ တာ ။
ပြ ဇာတ် ကြ ည့် မယ် ။
ဧည့် သည် အဲ့ ဒီ အိတ် က ငါး သောင်း ဝမ် ပါ ။
ချော စု က သူ့ ကို ဒီ နေ ရာ မှာ သက် တော င့် သက် သာ ထိုင် ပါ တဲ့ ။
```

input file က အောက်ပါအတိုင်း ...  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ cat ./tst4normalizer.txt
လက် ရေး ကို ဖြစ် သ လို‌‌‌ ရေး လို့ ဘာ အ ကြောင်း အ ရာ မှန်း မ သိ တော့ ဘူး ။
ဒီ ဓာတ် ပုံ ကို တည်း ဖြတ် သူ က တော့ ကျောင်း‌ လော က မှာ ကျော် ကြား တဲ့ ပ ရော် ဖက် ဆာ ဘတ် ဖြစ် ပါ တယ် ။
ကို ယ့် ကိုယ် ကို ယုံ ကြည် ချက် အ ပြ ည့် ရှိ သည် ။  자신  만만하다 .
အ မျိုး သ မီး အ ဝတ် အ စား ရောင်း တဲ့ နေ ရာ က ဘယ် မှာ ရှိ ပါ သ လဲ ။
ကု လား ထိုင် ထော င့် ကို ရွှေ့ သည် ။  의자를  구석으로  옮기다 .
အဲ ဒါ ကျွန် တော့် ဟာ ပါ ။
သူ က အ ဝတ် စျေး ကို မြှ င့် လိုက် နှိ မ့် လိုက် နဲ့ စိတ် တိုင်း ကျ ကို လုပ် နေ တာ ။
ပြ ဇာတ် ကြ ည့် မယ် ။
ဧည့် သည် အဲ့ ဒီ အိတ် က ငါး သောင်း ဝမ် ပါ ။
ချော စု က သူ့ ကို ဒီ နေ ရာ မှာ သက် တော င့် သက် သာ ထိုင် ပါ တဲ့ ။
```

## Calling Normalizer inside Converter  

ဟိုးအထက်မှာ ရေးခဲ့တဲ့ wordtag2syltag.py မှာ normalizer ကို ထည့်မယ်။  

```python
#!/usr/bin/env python3
# -*- coding:utf-8 -*-

"""

For converting word level tagged sentences into syllable level sentences.
Written by Ye Kyaw Thu, LST Lab, NECTEC, Thailand.
Last updated: 5 Dec 2024.

How to use:  
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ time python ./wordtag2syltag.py -i ./test.tagged -o test.tagged.bone -p BONE
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ time python ./wordtag2syltag.py -i ./test.tagged -o test.tagged.bfone -p BFONE

"""

import argparse
import re
from normalizer import process_input

def parse_arguments():
    """Parse command line arguments."""
    parser = argparse.ArgumentParser(description="Convert word-tagged Burmese data to syllable-tagged data.")
    parser.add_argument("-i", "--input", type=str, required=True, help="Input file (word-tagged data)")
    parser.add_argument("-o", "--output", type=str, required=True, help="Output file (syllable-tagged data)")
    parser.add_argument("-p", "--pattern", type=str, choices=["BONE", "BFONE"], default="BONE",
                        help="Tagging pattern: BONE or BFONE (default: BONE)")
    return parser.parse_args()

def create_break_pattern():
    """Create the regular expression pattern for syllable segmentation."""
    my_consonant = r"က-အ"
    en_no = r"0-9"
    other_char = r"ဣဤဥဦဧဩဪဿ၌၍၏၀-၉၊။!-/:-@[-`{-~\\s"
    subscript_symbol = r'္'
    a_that = r'်'

    return re.compile(
        r"((?<!"
        + subscript_symbol
        + r")["
        + my_consonant
        + r"](?!["
        + a_that
        + subscript_symbol
        + r"])|["
        + en_no
        + other_char
        + r"])"
    )

def syllable_segment(sentence, break_pattern):
    """Segment a sentence into syllables."""
    return break_pattern.sub(r" \1", sentence).strip().split()

def remove_tags_and_join(sentence):
    """Remove tags and join words into a tag-free sentence."""
    words = sentence.strip().split()
    cleaned_words = [word.split('/')[0] for word in words if '/' in word]  # Remove tags
    return " ".join(cleaned_words)

def tag_sentence(syllables, pattern):
    """Tag the syllables based on the selected pattern."""
    n = len(syllables)
    #print("syllables:", syllables)
    #print("n:", n)
    tags = []

    for i, syllable in enumerate(syllables):
        if i == 0:
            tags.append(f"{syllable}/B")  # Beginning
        elif i == n - 1:
            tags.append(f"{syllable}/E")  # Ending
        else:
            if pattern == "BONE":
                if n - i <= 4:  # Near Ending (N)
                    tags.append(f"{syllable}/N")
                else:  # Other (O)
                    tags.append(f"{syllable}/O")
            elif pattern == "BFONE":
                if n - i <= 4:  # Near Ending (N)
                    tags.append(f"{syllable}/N")
                elif i <= 3:  # Near Beginning (F)
                    tags.append(f"{syllable}/F")
                else:  # Other (O)
                    tags.append(f"{syllable}/O")
    return " ".join(tags)

def process_sentence(sentence, break_pattern, pattern):
    """Process a single sentence for syllable segmentation and tagging."""
    # Remove tags and join words
    cleaned_sentence = remove_tags_and_join(sentence)

    # Normalization
    normalized_sentence = process_input(
        sentence, 
        dictionary_file="./normalizer/final_syl_dictionary_13Feb2024.sorted.txt", 
        min_frequency=2, 
        check= 'dictionary'
    )

    # Segment the normalized sentence into syllables
    syllables = syllable_segment(normalized_sentence, break_pattern)

    # Tag the segmented syllables
    return tag_sentence(syllables, pattern)

def process_file(input_file, output_file, break_pattern, pattern):
    """Process the input file line by line and write the result to the output file."""
    with open(input_file, 'r', encoding='utf-8') as infile, open(output_file, 'w', encoding='utf-8') as outfile:
        for line in infile:
            line = line.strip()

            # Split by "/E", but keep "/E" in the split sentences
            sentences = []
            temp_sentence = ''
            for word in line.split():
                if word.endswith('/E'):
                    # Add the word with "/E" at the end and finalize the sentence
                    temp_sentence += word
                    sentences.append(temp_sentence.strip())
                    temp_sentence = ''
                else:
                    # Add word to the temporary sentence
                    temp_sentence += word + ' '

            # If there's any leftover sentence that doesn't end with "/E"
            if temp_sentence.strip():
                sentences.append(temp_sentence.strip())

            #print("sentences:", sentences)  # Debugging

            # Process the sentences and write to the output
            tagged_sentences = [
                process_sentence(sentence.strip(), break_pattern, pattern) for sentence in sentences if sentence.strip()
            ]
            outfile.write(" ".join(tagged_sentences) + "\n")


if __name__ == "__main__":
    args = parse_arguments()
    break_pattern = create_break_pattern()
    process_file(args.input, args.output, break_pattern, args.pattern)


```

(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ cat ./run-wordtag2syltag-normalize.sh  

```bash
#!/bin/bash

set -x;

# Running for training data:
time python ./wordtag2syltag-normalize.py -i ./train-valid.tagged -o train-valid.tagged.bone -p BONE;
time python ./wordtag2syltag-normalize.py -i ./train-valid.tagged -o train-valid.tagged.bfone -p BFONE;

# Running for test data:
time python ./wordtag2syltag-normalize.py -i ./test.tagged -o test.tagged.bone -p BONE;
time python ./wordtag2syltag-normalize.py -i ./test.tagged -o test.tagged.bfone -p BFONE;

set +x;
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$
```

converting with normalizer:  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ ./run-wordtag2syltag-normalize.sh
+ python ./wordtag2syltag-normalize.py -i ./train-valid.tagged -o train-valid.tagged.bone -p BONE

real    5m33.638s
user    5m27.491s
sys     0m6.128s
+ python ./wordtag2syltag-normalize.py -i ./train-valid.tagged -o train-valid.tagged.bfone -p BFONE

real    5m32.900s
user    5m26.846s
sys     0m6.032s
+ python ./wordtag2syltag-normalize.py -i ./test.tagged -o test.tagged.bone -p BONE

real    0m36.961s
user    0m36.270s
sys     0m0.688s
+ python ./wordtag2syltag-normalize.py -i ./test.tagged -o test.tagged.bfone -p BFONE

real    0m36.731s
user    0m36.001s
sys     0m0.728s
+ set +x
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$
```

checking filesizes:  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ wc train-valid.tagged
   50081   896088 14613857 train-valid.tagged
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ wc train-valid.tagged.{bone,bfone}
   50081  2232434 20404817 train-valid.tagged.bone
   50081  2232434 20404817 train-valid.tagged.bfone
  100162  4464868 40809634 total
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$
```

for test data:  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ wc test.tagged
   5512   96647 1573446 test.tagged
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ wc test.tagged.{bone,bfone}
   5512  240619 2197513 test.tagged.bone
   5512  240619 2197513 test.tagged.bfone
  11024  481238 4395026 total
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$
```

## Check Output Files Manually 

Server မှာ run ပြီးထွက်လာတဲ့ tagged ဖိုင်တွေကို local စက်ထဲ ကောပီကူးပြီး စစ်ကြည့်တော့ အောက်ပါအတိုင်း error တွေ တွေ့ရတယ်။  

test.tagged.bone ဖိုင်ထဲက အမှားများ...  
```
ရင်/B ဘတ်/O /B/O အောင့်/O /O/O လာ/O /N/O ရင်/O /N/O သ/O တိ/O ထား/N /N/N ပါ/N /E/E
ဘယ်/B လောက်/O /B/O နောက်/O ကျ/O /N/N သ/N လဲ/N /E/E
ကြို/B ပို့/O /B/O ဘတ်စ်/O ကား/O /N/O က/O /N/O အ/O ဆင်/O အ/O ပြ/O ဆေုံး/N /N/N ပဲ/N /E/E
```

test.tagged.bfone ဖိုင်ထဲက အမှားများ...  
```
ရင်/B ဘတ်/F /B/F အောင့်/F /O/O လာ/O /N/O ရင်/O /N/O သ/O တိ/O ထား/N /N/N ပါ/N /E/E
ဘယ်/B လောက်/F /B/F နောက်/F ကျ/O /N/N သ/N လဲ/N /E/E
ကြို/B ပို့/F /B/F ဘတ်စ်/F ကား/O /N/O က/O /N/O အ/O ဆင်/O အ/O ပြ/O ဆေုံး/N /N/N ပဲ/N /E/E
```

ဖြစ်ဖို့များတာက normalized လုပ်ပြီးထွက်လာတဲ့ ဖိုင်တွေမှာ space တွေ ပိုပါလာတာမျိုးလို့ ယူဆခဲ့။  
debug print နဲ့ normalized စာကြောင်းတွေကို စစ်ကြည့်တော့ အောက်ပါအတိုင်းတွေ့ရ။  
  
```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ time python ./wordtag2syltag-normalize.py -i ./test.tagged -o test.tagged.bone -p BONE | head
normalized:  ရင်ဘတ်/B အောင့်/O လာ/N ရင်/N သတိထား/N ပါ/E
normalized:  ဘယ်လောက်/B နောက်ကျ/N သလဲ/E
normalized:  ကြိုပို့/B ဘတ်စ်ကား/N က/N အဆင်အပြဆေုံး/N ပဲ/E
normalized:  အဲဒီ/B အဖွဲ့/O ရဲ့/O ဥက္ကဋ္ဌ/O ဖြစ်/O တဲ့/O ယို/O ကို/O ယာမာ့/O အာကိဟီတို/O YokoyamaAkihito/O က/O တခြား/O နိုင်ငံ/O တွေ/O မှာ/O ဖြစ်ပွား/O တဲ့/O လူနာ/O တွေ/O ရဲ့/O အဆုတ်လုပ်ဆောင်/O ပုံ/O တွေ/O က/O ဗိုင်းရပ်စ်ကူးစက်/O ခံ/O ရ/O ပြီး/O ကုသ/O လိုက်/O လို့/O ရောဂါပိုး/O မ/O ရှိ/O တော့/O ဘူး/O လို့/O စစ်ဆေး/O ပြီးနောက်/O မှာ/O တောင်/O မှ/O အဆုတ်/O က/O အပြည့်/O အဝ/O ပုံမှန်/O ပြန်/O ဖြစ်/O မလာ/O တဲ့/O လူနာ/O တွေ/O အများအပြား/O တွေ့/O ရ/O တယ်/O လို့/N ပြော/N ပါ/N တယ်/E
normalized:  အဆင့်/B အေ/O ဝင်ငွခေွန်/O ကို/O လစာ/N မှ/N ဖြတ်တောက်/N သည်/E
normalized:  လိုကီ/B က/O အတ်/O ဂါဒါ/O လိုကီ/O ရဲ့/O မျက်လုံး/O တွေ/O ကို/O သချော/O တည့်တည့်/O ကြည့်/O ရင်း/N ငါ/N က/N လိုကီ/E
normalized:  ခင်ဗျား/B ကြိုက်/O တဲ့/O အရောင်/N က/N ဘာ/N လဲ/E
normalized:  သူ/B သီချင်း/O ဆို/O တတ်/O သလို/O က/O လည်း/N က/N တတ်/N သည်/E
normalized:  ထို့ကြောင့်/B ဥပါယ်ဂို့/O ဟု/O ခေါ်/O ကာ/O ကာလ/O ကြာ/O သော်/O ဥပါယ်ဂို့/O မှ/O ပဂိုး/O ဟု/O ပြောင်းလဲ/O ခေါ်/N လာ/N ကြ/N သည်/E
normalized:  ဒီ/B နေ့/O ခင်ဗျား/O ဘယ်လို/O ဖြစ်/N နေ/N တာ/N လဲ/E
```

Error က cleaned_sentence ကို pass မလုပ်ပဲ sentence ကို pass လုပ်ထားခဲ့လို့ ဆိုတာကို အောက်ပါအတိုင်း တွေ့ရ။ စကားပြောရင်းနဲ့ coding လုပ်ခဲ့ခြင်းရဲ့ ရလဒ်ပါ :)  

```python
    # Normalization
    normalized_sentence = process_input(
        sentence,
        dictionary_file="./normalizer/final_syl_dictionary_13Feb2024.sorted.txt",
        min_frequency=2,
        check= 'dictionary'
    )

    print("normalized: ", normalized_sentence)
```

## Updated the Code and ReRun Again  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ ./run-wordtag2syltag-normalize.sh
+ python ./wordtag2syltag-normalize.py -i ./train-valid.tagged -o train-valid.tagged.bone -p BONE

real    5m30.219s
user    5m23.734s
sys     0m6.448s
+ python ./wordtag2syltag-normalize.py -i ./train-valid.tagged -o train-valid.tagged.bfone -p BFONE

real    5m31.158s
user    5m25.031s
sys     0m6.108s
+ python ./wordtag2syltag-normalize.py -i ./test.tagged -o test.tagged.bone -p BONE

real    0m36.358s
user    0m35.710s
sys     0m0.644s
+ python ./wordtag2syltag-normalize.py -i ./test.tagged -o test.tagged.bfone -p BFONE

real    0m36.200s
user    0m35.490s
sys     0m0.708s
+ set +x
```

Download to local machine and check each file manually ...  

test.tagged.bone  

```
ရင်/B ဘတ်/O အောင့်/O လာ/O ရင်/O သ/N တိ/N ထား/N ပါ/E
ဘယ်/B လောက်/O နောက်/N ကျ/N သ/N လဲ/E
ကြို/B ပို့/O ဘတ်စ်/O ကား/O က/O အ/O ဆင်/O အ/N ပြ/N ဆေုံး/N ပဲ/E
သူ/B မ/O သူ/O ငယ်/O ချင်း/O များ/O တွင်/O မ/O တော့/O ဘုန်း/O ကြီး/O ဝတ်/O သွား/O သော/O ဗ/O ဒေင်/O တတ်/O သည့်/O အ/O ဘိုး/O မ/O ရှိ/O ၍/O ပဲ/N လား/N မ/N သိ/E နာ/B မည်/O လှ/O လှ/O က/O လေး/O တွေ/N နှင့်/N ဖြစ်/N သည်/E တ/B ခြား/O မိန်း/O က/O လေး/O တွေ/O ရဲ့/O နာ/O မည်/O တွေ/O က/O လည်း/O မ/O ကောင်း/O ရင်/O သာ/N ရှိ/N ရ/N မည်/E
```

test.tagged.bfone  

```
ရင်/B ဘတ်/F အောင့်/F လာ/F ရင်/O သ/N တိ/N ထား/N ပါ/E
ဘယ်/B လောက်/F နောက်/N ကျ/N သ/N လဲ/E
ကြို/B ပို့/F ဘတ်စ်/F ကား/F က/O အ/O ဆင်/O အ/N ပြ/N ဆေုံး/N ပဲ/E
သူ/B မ/F သူ/F ငယ်/F ချင်း/O များ/O တွင်/O မ/O တော့/O ဘုန်း/O ကြီး/O ဝတ်/O သွား/O သော/O ဗ/O ဒေင်/O တတ်/O သည့်/O အ/O ဘိုး/O မ/O ရှိ/O ၍/O ပဲ/N လား/N မ/N သိ/E နာ/B မည်/F လှ/F လှ/F က/O လေး/O တွေ/N နှင့်/N ဖြစ်/N သည်/E တ/B ခြား/F မိန်း/F က/F လေး/O တွေ/O ရဲ့/O နာ/O မည်/O တွေ/O က/O လည်း/O မ/O ကောင်း/O ရင်/O သာ/N ရှိ/N ရ/N မည်/E
```

Normalize မလုပ်ခင်က output မှာ ဖြစ်တဲ့ ပြဿနာတော့ တချို့တော့ ရှင်းသွားပြီ။  

```
ရင်/B ဘတ်/O အော/O င့်/O လာ/O ရင်/O သ/N တိ/N ထား/N ပါ/E
```

သို့သော် 100% perfect တော့ မဟုတ်ဘူး။  
training ဖိုင်ထဲက တချို့ အမှားတွေက အောက်ပါအတိုင်း...  

train-valid.tagged.bone  

48629, 48654
```
ခေါင်/B မိုး/O မှ/N ရ/N ယေို/N သည်/E
ဓာ/B တု/O ဗ/O ဒေ/O ပ/O ညာ/O ရပ်/O ပိုင်း/O က/O သုံး/O သပ်/O ရင်/O လည်း/O ဓာ/O တု/O ပ/O ညာ/O ရပ်/O ကို/O စ/O ခဲ့/O တဲ့/O ရှေး/O ခ/O တေ်/O အဂ္ဂိ/O ရတ်/O ဆ/O ရာ/O ကြီး/O တွေ/O ရဲ့/O ယမ်း/O င/O ရဲ/O မီး/O ကန့်/O င/O ရဲ/O မီး/O ဆား/O င/O ရဲ/O မီး/O နဲ့/O ရွှ/O စေား/O င/O ရဲ/O မီး/O ထုတ်/O လုပ်/O ပုံ/O နည်း/O စ/O နစ်/O တွေ/O နဲ့/O ပုံ/O စံ/O တူ/O တာ/N တွေ့/N ရ/N သည်/E
```

train-valid.tagged.bfone  

48620, 48654
```
ခေါင်/B မိုး/F မှ/N ရ/N ယေို/N သည်/E
ဓာ/B တု/F ဗ/F ဒေ/F ပ/O ညာ/O ရပ်/O ပိုင်း/O က/O သုံး/O သပ်/O ရင်/O လည်း/O ဓာ/O တု/O ပ/O ညာ/O ရပ်/O ကို/O စ/O ခဲ့/O တဲ့/O ရှေး/O ခ/O တေ်/O အဂ္ဂိ/O ရတ်/O ဆ/O ရာ/O ကြီး/O တွေ/O ရဲ့/O ယမ်း/O င/O ရဲ/O မီး/O ကန့်/O င/O ရဲ/O မီး/O ဆား/O င/O ရဲ/O မီး/O နဲ့/O ရွှ/O စေား/O င/O ရဲ/O မီး/O ထုတ်/O လုပ်/O ပုံ/O နည်း/O စ/O နစ်/O တွေ/O နဲ့/O ပုံ/O စံ/O တူ/O တာ/N တွေ့/N ရ/N သည်/E
```

train-valid.tagged ဖိုင်မှာက  
48620, 48654

```
ခေါင်မိုး/B မှ/N ရေယို/N သည်/E
ဓာတုဗေဒ/B ပညာရပ်/O ပိုင်း/O က/O သုံးသပ်/O ရင်/O လည်း/O ဓာတု/O ပညာရပ်/O ကို/O စ/O ခဲ့/O တဲ့/O ရှေး/O ခေတ်/O အဂ္ဂိရတ်/O ဆရာကြီး/O တွေ/O ရဲ့/O ယမ်းငရဲမီး/O ကန့်ငရဲမီး/O ဆားငရဲမီး/O နဲ့/O ရွှေစားငရဲမီး/O ထုတ်လုပ်/O ပုံ/O နည်းစနစ်/O တွေ/O နဲ့/O ပုံစံ/O တူ/O တာ/N တွေ့/N ရ/N သည်/E
```

## Debugging the Code  

syllable ဖြတ်ပြီးမှ normalization လုပ်ရမှာကို မလုပ်ခဲ့လို့လို့ ယူဆတယ်။  
လက်ရှိ code က အောက်ပါအတိုင်း ...  

```python
def process_sentence(sentence, break_pattern, pattern):
    """Process a single sentence for syllable segmentation and tagging."""
    # Remove tags and join words
    cleaned_sentence = remove_tags_and_join(sentence)

    # Normalization
    normalized_sentence = process_input(
        cleaned_sentence,
        dictionary_file="./normalizer/final_syl_dictionary_13Feb2024.sorted.txt",
        min_frequency=2,
        check= 'dictionary'
    )

    #print("normalized: ", normalized_sentence) # Debugging

    # Segment the normalized sentence into syllables
    syllables = syllable_segment(normalized_sentence, break_pattern)

    # Tag the segmented syllables
    return tag_sentence(syllables, pattern)
```

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ python ./wordtag2syltag.py -i ./tmp4normalize.txt -o tmp.bone -p BONE
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ cat tmp.bone
ခေါင်/B မိုး/O မှ/N ရေ/N ယို/N သည်/E
ဓာ/B တု/O ဗေ/O ဒ/O ပ/O ညာ/O ရပ်/O ပိုင်း/O က/O သုံး/O သပ်/O ရင်/O လည်း/O ဓာ/O တု/O ပ/O ညာ/O ရပ်/O ကို/O စ/O ခဲ့/O တဲ့/O ရှေး/O ခေတ်/O အဂ္ဂိ/O ရတ်/O ဆ/O ရာ/O ကြီး/O တွေ/O ရဲ့/O ယမ်း/O င/O ရဲ/O မီး/O ကန့်/O င/O ရဲ/O မီး/O ဆား/O င/O ရဲ/O မီး/O နဲ့/O ရွှေ/O စား/O င/O ရဲ/O မီး/O ထုတ်/O လုပ်/O ပုံ/O နည်း/O စ/O နစ်/O တွေ/O နဲ့/O ပုံ/O စံ/O တူ/O တာ/N တွေ့/N ရ/N သည်/E
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$
```

အထက်မှာ မြင်ရတဲ့အတိုင်း normalize feature ကို မထည့်ခင်က အထက်ပါရလဒ်အတိုင်း ပြဿနာ မရှိတာကို တွေ့ရတယ်။  

normalize ဗားရှင်းလက်ရှိ code မှာပဲ debug print statement ကို ထည့်ပြီး run ကြည့်တော့ အောက်ပါအတိုင်း error ဖြစ်တာကို တွေ့ရတယ်။  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ python ./wordtag2syltag-normalize.py -i ./tmp4normalize.txt -o tmp.bone -p BONE
cleaned:  ခေါင်မိုး မှ ရေယို သည်
normalized:  ခေါင်မိုး မှ ရယေို သည်
cleaned:  ဓာတုဗေဒ ပညာရပ် ပိုင်း က သုံးသပ် ရင် လည်း ဓာတု ပညာရပ် ကို စ ခဲ့ တဲ့ ရှေး ခေတ် အဂ္ဂိရတ် ဆရာကြီး တွေ ရဲ့ ယမ်းငရဲမီး ကန့်ငရဲမီး ဆားငရဲမီး နဲ့ ရွှေစားငရဲမီး ထုတ်လုပ် ပုံ နည်းစနစ် တွေ နဲ့ ပုံစံ တူ တာ တွေ့ ရ သည်
normalized:  ဓာတုဗဒေ ပညာရပ် ပိုင်း က သုံးသပ် ရင် လည်း ဓာတု ပညာရပ် ကို စ ခဲ့ တဲ့ ရှေး ခတေ် အဂ္ဂိရတ် ဆရာကြီး တွေ ရဲ့ ယမ်းငရဲမီး ကန့်ငရဲမီး ဆားငရဲမီး နဲ့ ရွှစေားငရဲမီး ထုတ်လုပ် ပုံ နည်းစနစ် တွေ နဲ့ ပုံစံ တူ တာ တွေ့ ရ သည်
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$
```

အဲဒါကြောင့် အောက်ပါအတိုင်း code ကို update လုပ်ခဲ့တယ်။  

```python
def process_sentence(sentence, break_pattern, pattern):
    """Process a single sentence for syllable segmentation and tagging."""
    # Remove tags and join words
    cleaned_sentence = remove_tags_and_join(sentence)
    print("cleaned: ", cleaned_sentence)

    # Segment the normalized sentence into syllables
    syllables = syllable_segment(cleaned_sentence, break_pattern)
    print("syllables: ", syllables)

    # Normalization
    normalized_output = process_input(
        ' '.join(syllables),  # Join list into space-separated string
        dictionary_file="./normalizer/final_syl_dictionary_13Feb2024.sorted.txt",
        min_frequency=2,
        check='dictionary'
    )

    # Split normalized output back into a list
    normalized_syllables = normalized_output.split()
    print("normalized (list): ", normalized_syllables)  # Debugging

    # Tag the segmented syllables
    return tag_sentence(normalized_syllables, pattern)
```

ပြင်ထားတဲ့ code နဲ့ run ကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရတယ်။  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ python ./wordtag2syltag-normalize.py -i ./tmp4normalize.txt -o tmp.bone -p BONE
cleaned:  ခေါင်မိုး မှ ရေယို သည်
syllables:  ['ခေါင်', 'မိုး', 'မှ', 'ရေ', 'ယို', 'သည်']
normalized (list):  ['ခေါင်', 'မိုး', 'မှ', 'ရေ', 'ယို', 'သည်']
cleaned:  ဓာတုဗေဒ ပညာရပ် ပိုင်း က သုံးသပ် ရင် လည်း ဓာတု ပညာရပ် ကို စ ခဲ့ တဲ့ ရှေး ခေတ် အဂ္ဂိရတ် ဆရာကြီး တွေ ရဲ့ ယမ်းငရဲမီး ကန့်ငရဲမီး ဆားငရဲမီး နဲ့ ရွှေစားငရဲမီး ထုတ်လုပ် ပုံ နည်းစနစ် တွေ နဲ့ ပုံစံ တူ တာ တွေ့ ရ သည်
syllables:  ['ဓာ', 'တု', 'ဗေ', 'ဒ', 'ပ', 'ညာ', 'ရပ်', 'ပိုင်း', 'က', 'သုံး', 'သပ်', 'ရင်', 'လည်း', 'ဓာ', 'တု', 'ပ', 'ညာ', 'ရပ်', 'ကို', 'စ', 'ခဲ့', 'တဲ့', 'ရှေး', 'ခေတ်', 'အဂ္ဂိ', 'ရတ်', 'ဆ', 'ရာ', 'ကြီး', 'တွေ', 'ရဲ့', 'ယမ်း', 'င', 'ရဲ', 'မီး', 'ကန့်', 'င', 'ရဲ', 'မီး', 'ဆား', 'င', 'ရဲ', 'မီး', 'နဲ့', 'ရွှေ', 'စား', 'င', 'ရဲ', 'မီး', 'ထုတ်', 'လုပ်', 'ပုံ', 'နည်း', 'စ', 'နစ်', 'တွေ', 'နဲ့', 'ပုံ', 'စံ', 'တူ', 'တာ', 'တွေ့', 'ရ', 'သည်']
normalized (list):  ['ဓာ', 'တု', 'ဗေ', 'ဒ', 'ပ', 'ညာ', 'ရပ်', 'ပိုင်း', 'က', 'သုံး', 'သပ်', 'ရင်', 'လည်း', 'ဓာ', 'တု', 'ပ', 'ညာ', 'ရပ်', 'ကို', 'စ', 'ခဲ့', 'တဲ့', 'ရှေး', 'ခတေ်', 'အဂ္ဂိ', 'ရတ်', 'ဆ', 'ရာ', 'ကြီး', 'တွေ', 'ရဲ့', 'ယမ်း', 'င', 'ရဲ', 'မီး', 'ကန့်', 'င', 'ရဲ', 'မီး', 'ဆား', 'င', 'ရဲ', 'မီး', 'နဲ့', 'ရွှေ', 'စား', 'င', 'ရဲ', 'မီး', 'ထုတ်', 'လုပ်', 'ပုံ', 'နည်း', 'စ', 'နစ်', 'တွေ', 'နဲ့', 'ပုံ', 'စံ', 'တူ', 'တာ', 'တွေ့', 'ရ', 'သည်']
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$
```

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ cat ./tmp.bone
ခေါင်/B မိုး/O မှ/N ရေ/N ယို/N သည်/E
ဓာ/B တု/O ဗေ/O ဒ/O ပ/O ညာ/O ရပ်/O ပိုင်း/O က/O သုံး/O သပ်/O ရင်/O လည်း/O ဓာ/O တု/O ပ/O ညာ/O ရပ်/O ကို/O စ/O ခဲ့/O တဲ့/O ရှေး/O ခတေ်/O အဂ္ဂိ/O ရတ်/O ဆ/O ရာ/O ကြီး/O တွေ/O ရဲ့/O ယမ်း/O င/O ရဲ/O မီး/O ကန့်/O င/O ရဲ/O မီး/O ဆား/O င/O ရဲ/O မီး/O နဲ့/O ရွှေ/O စား/O င/O ရဲ/O မီး/O ထုတ်/O လုပ်/O ပုံ/O နည်း/O စ/O နစ်/O တွေ/O နဲ့/O ပုံ/O စံ/O တူ/O တာ/N တွေ့/N ရ/N သည်/E
```

temp ဖိုင်မှာ multiple sentence input စာကြောင်း စတာတွေ ထပ်ဖြည့်ပြီး run ကြည့်ခဲ့...  

```
ခေါင်မိုး/B မှ/N ရေယို/N သည်/E
ဓာတုဗေဒ/B ပညာရပ်/O ပိုင်း/O က/O သုံးသပ်/O ရင်/O လည်း/O ဓာတု/O ပညာရပ်/O ကို/O စ/O ခဲ့/O တဲ့/O ရှေး/O ခေတ်/O အဂ္ဂိရတ်/O ဆရာကြီး/O တွေ/O ရဲ့/O ယမ်းငရဲမီး/O ကန့်ငရဲမီး/O ဆားငရဲမီး/O နဲ့/O ရွှေစားငရဲမီး/O ထုတ်လုပ်/O ပုံ/O နည်းစနစ်/O တွေ/O နဲ့/O ပုံစံ/O တူ/O တာ/N တွေ့/N ရ/N သည်/E
သူမ/B သူငယ်ချင်း/O များ/O တွင်/O မ/O တော့/O ဘုန်းကြီး/O ဝတ်/O သွား/O သော/O ဗေဒင်/O တတ်/O သည့်/O အဘိုး/O မ/O ရှိ/O ၍/O ပဲ/N လား/N မ/N သိ/E နာမည်/B လှလှ/O ကလေး/O တွေ/N နှင့်/N ဖြစ်/N သည်/E တခြား/B မိန်းကလေး/O တွေ/O ရဲ့/O နာမည်/O တွေ/O က/O လည်း/O မ/O ကောင်း/O ရင်/O သာ/N ရှိ/N ရ/N မည်/E
ရင်ဘတ်/B အောင့်/O လာ/N ရင်/N သတိထား/N ပါ/E
```

Run with updated code and updated test file.  
scren output is as follows:  

```
tag cleaned:  ခေါင်မိုး မှ ရေယို သည်
syllables:  ['ခေါင်', 'မိုး', 'မှ', 'ရေ', 'ယို', 'သည်']
normalized syllables:  ['ခေါင်', 'မိုး', 'မှ', 'ရေ', 'ယို', 'သည်']
tagged:  ခေါင်/B မိုး/O မှ/N ရေ/N ယို/N သည်/E
tag cleaned:  ဓာတုဗေဒ ပညာရပ် ပိုင်း က သုံးသပ် ရင် လည်း ဓာတု ပညာရပ် ကို စ ခဲ့ တဲ့ ရှေး ခေတ် အဂ္ဂိရတ် ဆရာကြီး တွေ ရဲ့ ယမ်းငရဲမီး ကန့်ငရဲမီး ဆားငရဲမီး နဲ့ ရွှေစားငရဲမီး ထုတ်လုပ် ပုံ နည်းစနစ် တွေ နဲ့ ပုံစံ တူ တာ တွေ့ ရ သည်
syllables:  ['ဓာ', 'တု', 'ဗေ', 'ဒ', 'ပ', 'ညာ', 'ရပ်', 'ပိုင်း', 'က', 'သုံး', 'သပ်', 'ရင်', 'လည်း', 'ဓာ', 'တု', 'ပ', 'ညာ', 'ရပ်', 'ကို', 'စ', 'ခဲ့', 'တဲ့', 'ရှေး', 'ခေတ်', 'အဂ္ဂိ', 'ရတ်', 'ဆ', 'ရာ', 'ကြီး', 'တွေ', 'ရဲ့', 'ယမ်း', 'င', 'ရဲ', 'မီး', 'ကန့်', 'င', 'ရဲ', 'မီး', 'ဆား', 'င', 'ရဲ', 'မီး', 'နဲ့', 'ရွှေ', 'စား', 'င', 'ရဲ', 'မီး', 'ထုတ်', 'လုပ်', 'ပုံ', 'နည်း', 'စ', 'နစ်', 'တွေ', 'နဲ့', 'ပုံ', 'စံ', 'တူ', 'တာ', 'တွေ့', 'ရ', 'သည်']
normalized syllables:  ['ဓာ', 'တု', 'ဗေ', 'ဒ', 'ပ', 'ညာ', 'ရပ်', 'ပိုင်း', 'က', 'သုံး', 'သပ်', 'ရင်', 'လည်း', 'ဓာ', 'တု', 'ပ', 'ညာ', 'ရပ်', 'ကို', 'စ', 'ခဲ့', 'တဲ့', 'ရှေး', 'ခတေ်', 'အဂ္ဂိ', 'ရတ်', 'ဆ', 'ရာ', 'ကြီး', 'တွေ', 'ရဲ့', 'ယမ်း', 'င', 'ရဲ', 'မီး', 'ကန့်', 'င', 'ရဲ', 'မီး', 'ဆား', 'င', 'ရဲ', 'မီး', 'နဲ့', 'ရွှေ', 'စား', 'င', 'ရဲ', 'မီး', 'ထုတ်', 'လုပ်', 'ပုံ', 'နည်း', 'စ', 'နစ်', 'တွေ', 'နဲ့', 'ပုံ', 'စံ', 'တူ', 'တာ', 'တွေ့', 'ရ', 'သည်']
tagged:  ဓာ/B တု/O ဗေ/O ဒ/O ပ/O ညာ/O ရပ်/O ပိုင်း/O က/O သုံး/O သပ်/O ရင်/O လည်း/O ဓာ/O တု/O ပ/O ညာ/O ရပ်/O ကို/O စ/O ခဲ့/O တဲ့/O ရှေး/O ခတေ်/O အဂ္ဂိ/O ရတ်/O ဆ/O ရာ/O ကြီး/O တွေ/O ရဲ့/O ယမ်း/O င/O ရဲ/O မီး/O ကန့်/O င/O ရဲ/O မီး/O ဆား/O င/O ရဲ/O မီး/O နဲ့/O ရွှေ/O စား/O င/O ရဲ/O မီး/O ထုတ်/O လုပ်/O ပုံ/O နည်း/O စ/O နစ်/O တွေ/O နဲ့/O ပုံ/O စံ/O တူ/O တာ/N တွေ့/N ရ/N သည်/E
tag cleaned:  သူမ သူငယ်ချင်း များ တွင် မ တော့ ဘုန်းကြီး ဝတ် သွား သော ဗေဒင် တတ် သည့် အဘိုး မ ရှိ ၍ ပဲ လား မ သိ
syllables:  ['သူ', 'မ', 'သူ', 'ငယ်', 'ချင်း', 'များ', 'တွင်', 'မ', 'တော့', 'ဘုန်း', 'ကြီး', 'ဝတ်', 'သွား', 'သော', 'ဗေ', 'ဒင်', 'တတ်', 'သ', 'ည့်', 'အ', 'ဘိုး', 'မ', 'ရှိ', '၍', 'ပဲ', 'လား', 'မ', 'သိ']
normalized syllables:  ['သူ', 'မ', 'သူ', 'ငယ်', 'ချင်း', 'များ', 'တွင်', 'မ', 'တော့', 'ဘုန်း', 'ကြီး', 'ဝတ်', 'သွား', 'သော', 'ဗေ', 'ဒင်', 'တတ်', 'သ', 'ည့်', 'အ', 'ဘိုး', 'မ', 'ရှိ', '၍', 'ပဲ', 'လား', 'မ', 'သိ']
tagged:  သူ/B မ/O သူ/O ငယ်/O ချင်း/O များ/O တွင်/O မ/O တော့/O ဘုန်း/O ကြီး/O ဝတ်/O သွား/O သော/O ဗေ/O ဒင်/O တတ်/O သ/O ည့်/O အ/O ဘိုး/O မ/O ရှိ/O ၍/O ပဲ/N လား/N မ/N သိ/E
tag cleaned:  နာမည် လှလှ ကလေး တွေ နှင့် ဖြစ် သည်
syllables:  ['နာ', 'မည်', 'လှ', 'လှ', 'က', 'လေး', 'တွေ', 'နှ', 'င့်', 'ဖြစ်', 'သည်']
normalized syllables:  ['နာ', 'မည်', 'လှ', 'လှ', 'က', 'လေး', 'တွေ', 'နှ', 'င့်', 'ဖြစ်', 'သည်']
tagged:  နာ/B မည်/O လှ/O လှ/O က/O လေး/O တွေ/O နှ/N င့်/N ဖြစ်/N သည်/E
tag cleaned:  တခြား မိန်းကလေး တွေ ရဲ့ နာမည် တွေ က လည်း မ ကောင်း ရင် သာ ရှိ ရ မည်
syllables:  ['တ', 'ခြား', 'မိန်း', 'က', 'လေး', 'တွေ', 'ရဲ့', 'နာ', 'မည်', 'တွေ', 'က', 'လည်း', 'မ', 'ကောင်း', 'ရင်', 'သာ', 'ရှိ', 'ရ', 'မည်']
normalized syllables:  ['တ', 'ခြား', 'မိန်း', 'က', 'လေး', 'တွေ', 'ရဲ့', 'နာ', 'မည်', 'တွေ', 'က', 'လည်း', 'မ', 'ကောင်း', 'ရင်', 'သာ', 'ရှိ', 'ရ', 'မည်']
tagged:  တ/B ခြား/O မိန်း/O က/O လေး/O တွေ/O ရဲ့/O နာ/O မည်/O တွေ/O က/O လည်း/O မ/O ကောင်း/O ရင်/O သာ/N ရှိ/N ရ/N မည်/E
tag cleaned:  ရင်ဘတ် အောင့် လာ ရင် သတိထား ပါ
syllables:  ['ရင်', 'ဘတ်', 'အော', 'င့်', 'လာ', 'ရင်', 'သ', 'တိ', 'ထား', 'ပါ']
normalized syllables:  ['ရင်', 'ဘတ်', 'အော', 'င့်', 'လာ', 'ရင်', 'သ', 'တိ', 'ထား', 'ပါ']
tagged:  ရင်/B ဘတ်/O အော/O င့်/O လာ/O ရင်/O သ/N တိ/N ထား/N ပါ/E
```

အထက်ပါအတိုင်း normalization မလုပ်တာကို တွေ့ရတယ်။ (အော/O င့်/O)
output ဖိုင်ကို စစ်ကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရတယ်။  

```
ခေါင်/B မိုး/O မှ/N ရေ/N ယို/N သည်/E
ဓာ/B တု/O ဗေ/O ဒ/O ပ/O ညာ/O ရပ်/O ပိုင်း/O က/O သုံး/O သပ်/O ရင်/O လည်း/O ဓာ/O တု/O ပ/O ညာ/O ရပ်/O ကို/O စ/O ခဲ့/O တဲ့/O ရှေး/O ခတေ်/O အဂ္ဂိ/O ရတ်/O ဆ/O ရာ/O ကြီး/O တွေ/O ရဲ့/O ယမ်း/O င/O ရဲ/O မီး/O ကန့်/O င/O ရဲ/O မီး/O ဆား/O င/O ရဲ/O မီး/O နဲ့/O ရွှေ/O စား/O င/O ရဲ/O မီး/O ထုတ်/O လုပ်/O ပုံ/O နည်း/O စ/O နစ်/O တွေ/O နဲ့/O ပုံ/O စံ/O တူ/O တာ/N တွေ့/N ရ/N သည်/E
သူ/B မ/O သူ/O ငယ်/O ချင်း/O များ/O တွင်/O မ/O တော့/O ဘုန်း/O ကြီး/O ဝတ်/O သွား/O သော/O ဗေ/O ဒင်/O တတ်/O သ/O ည့်/O အ/O ဘိုး/O မ/O ရှိ/O ၍/O ပဲ/N လား/N မ/N သိ/E နာ/B မည်/O လှ/O လှ/O က/O လေး/O တွေ/O နှ/N င့်/N ဖြစ်/N သည်/E တ/B ခြား/O မိန်း/O က/O လေး/O တွေ/O ရဲ့/O နာ/O မည်/O တွေ/O က/O လည်း/O မ/O ကောင်း/O ရင်/O သာ/N ရှိ/N ရ/N မည်/E
ရင်/B ဘတ်/O အော/O င့်/O လာ/O ရင်/O သ/N တိ/N ထား/N ပါ/E
```

Normalization code အတွက် input က syllable segmented လား၊ no space format လားဆိုတာကို ပြန် check လုပ်။  

real_err1.syl ဖိုင်ရဲ့ head command output က အောက်ပါအတိုင်း ...  

```
~/data/hello-sayarwon/coding/normalizer4thura$ head real_err1.syl
လက် ရေး ကို ဖြစ် သ လို‌‌‌ ရေး လို့ ဘာ အ ကြောင်း အ ရာ မှန်း မ သိ တော့ ဘူး ။
ဒီ ဓာတ် ပုံ ကို တည်း ဖြတ် သူ က တော့ ကျောင်း‌ လော က မှာ ကျော် ကြား တဲ့ ပ ရော် ဖက် ဆာ ဘတ် ဖြစ် ပါ တယ် ။
ကို ယ့် ကိုယ် ကို ယုံ ကြည် ချက် အ ပြ ည့် ရှိ သည် ။  자신  만만하다 .
အ မျိုး သ မီး အ ဝတ် အ စား ရောင်း တဲ့ နေ ရာ က ဘယ် မှာ ရှိ ပါ သ လဲ ။
ကု လား ထိုင် ထော င့် ကို ရွှေ့ သည် ။  의자를  구석으로  옮기다 .
အဲ ဒါ ကျွန် တော့် ဟာ ပါ ။
သူ က အ ဝတ် စျေး ကို မြှ င့် လိုက် နှိ မ့် လိုက် နဲ့ စိတ် တိုင်း ကျ ကို လုပ် နေ တာ ။
ပြ ဇာတ် ကြ ည့် မယ် ။
ဧည့် သည် အဲ့ ဒီ အိတ် က ငါး သောင်း ဝမ် ပါ ။
ချော စု က သူ့ ကို ဒီ နေ ရာ မှာ သက် တော င့် သက် သာ ထိုင် ပါ တဲ့ ။
```

အဲဒါကြောင့် syllable segmented ကို input လုပ်တာတော့ သေချာသွားပြီ။  
real_err1.syl ကို normalized လုပ်ပြီးထွက်လာတဲ့ output ဖိုင်ကို confirmation လုပ်ခဲ့။  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/normalizer4thura$ head real_err1.syl.normalized
လက် ရေး ကို ဖြစ် သ လို ရေး လို့ ဘာ အ ကြောင်း အ ရာ မှန်း မ သိ တော့ ဘူး ။
ဒီ ဓာတ် ပုံ ကို တည်း ဖြတ် သူ က တော့ ကျောင်း လော က မှာ ကျော် ကြား တဲ့ ပ ရော် ဖက် ဆာ ဘတ် ဖြစ် ပါ တယ် ။
ကို ယ့် ကိုယ် ကို ယုံ ကြည် ချက် အ ပြ ည့် ရှိ သည် ။ 자신 만만하다 .
အ မျိုး သ မီး အ ဝတ် အ စား ရောင်း တဲ့ နေ ရာ က ဘယ် မှာ ရှိ ပါ သ လဲ ။
ကု လား ထိုင် ထော င့် ကို ရွှေ့ သည် ။ 의자를 구석으로 옮기다 .
အဲ ဒါ ကျွန် တော့် ဟာ ပါ ။
သူ က အ ဝတ် ဈေး ကို မြှ င့် လိုက် နှိ မ့် လိုက် နဲ့ စိတ် တိုင်း ကျ ကို လုပ် နေ တာ ။
ပြ ဇာတ် ကြ ည့် မယ် ။
ဧည့် သည် အဲ့ ဒီ အိတ် က ငါး သောင်း ဝမ် ပါ ။
ချော စု က သူ့ ကို ဒီ နေ ရာ မှာ သက် တော င့် သက် သာ ထိုင် ပါ တဲ့ ။
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/normalizer4thura$
```

Checked result ဖိုင်ထုတ်ပေးထားတယ်။ 

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/normalizer4thura$ head syllable_checked_result.txt
လက် ရေး ကို ဖြစ် သ <လို‌‌‌> ရေး လို့ ဘာ အ ကြောင်း အ ရာ မှန်း မ သိ တော့ ဘူး <။>
ဒီ ဓာတ် ပုံ ကို တည်း ဖြတ် သူ က တော့ <ကျောင်း‌> လော က မှာ ကျော် ကြား တဲ့ ပ ရော် ဖက် ဆာ ဘတ် ဖြစ် ပါ တယ် <။>
ကို <ယ့်> ကိုယ် ကို ယုံ ကြည် ချက် အ ပြ <ည့်> ရှိ သည် <။> <자신> <만만하다> <.>
အ မျိုး သ မီး အ ဝတ် အ စား ရောင်း တဲ့ နေ ရာ က ဘယ် မှာ ရှိ ပါ သ လဲ <။>
ကု လား ထိုင် ထော <င့်> ကို ရွှေ့ သည် <။> <의자를> <구석으로> <옮기다> <.>
အဲ ဒါ ကျွန် <တော့်> ဟာ ပါ <။>
သူ က အ ဝတ် စျေး ကို မြှ <င့်> လိုက် နှိ <မ့်> လိုက် နဲ့ စိတ် တိုင်း ကျ ကို လုပ် နေ တာ <။>
ပြ ဇာတ် ကြ <ည့်> မယ် <။>
ဧည့် သည် အဲ့ ဒီ အိတ် က ငါး သောင်း ဝမ် ပါ <။>
ချော စု က သူ့ ကို ဒီ နေ ရာ မှာ သက် တော <င့်> သက် သာ ထိုင် ပါ တဲ့ <။>
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/normalizer4thura$
```

ရေးခဲ့တဲ့ normalize code ကို ပြန်စဉ်းစားပြီးတော့ မှတ်မိတာက 
input ကတော့ syllable segmented ဖြစ်ရမယ်။ အဲဒါကြောင့် လက်ရှိ ရေးထားတဲ့ code အစီအစဉ်က မှန်တယ်။  

normalization လုပ်ပေးတယ်။ output ဖိုင်မှာက syllable ဖြတ်ထားရင် အဲဒီအတိုင်း လုပ်ပေးတာမို့ ပြင်သွားပေမဲ့ အသတ်လိုမျိုး ကွဲနေတဲ့ ကောင်တွေကိုတော့ ပြန် မဆက်ပေးထားဘူး။  
  

```
time python3 ./chk_normalize.py \
--dictionary ./final_syl_dictionary_13Feb2024.sorted.txt --frequency 2 \
--input real_err1.syl --out real_err1.syl.normalized
```

```
ခေါင် မိုး မှ ရေ ယို သည်
ဓာ တု ဗေ ဒ ပ ညာ ရပ် ပိုင်း က သုံး သပ် ရင် လည်း ဓာ တု ပ ညာ ရပ် ကို စ ခဲ့ တဲ့ ရှေး ခတေ် အဂ္ဂိ ရတ် ဆ ရာ ကြီး တွေ ရဲ့ ယမ်း င ရဲ မီး ကန့် င ရဲ မီး ဆား င ရဲ မီး နဲ့ ရွှေ စား င ရဲ မီး ထုတ် လုပ် ပုံ နည်း စ နစ် တွေ နဲ့ ပုံ စံ တူ တာ တွေ့ ရ သည်
သူ မ သူ ငယ် ချင်း များ တွင် မ တော့ ဘုန်း ကြီး ဝတ် သွား သော ဗေ ဒင် တတ် သ ည့် အ ဘိုး မ ရှိ ၍ ပဲ လား မ သိ နာ မည် လှ လှ က လေး တွေ နှ င့် ဖြစ် သည် တ ခြား မိန်း က လေး တွေ ရဲ့ နာ မည် တွေ က လည်း မ ကောင်း ရင် သာ ရှိ ရ မည်
ရင် ဘတ် အော င့် လာ ရင် သ တိ ထား ပါ
```

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding$ python ./normalizer4thura/chk_normalize.py --dictionary ./normalizer4thura/final_syl_dictionary_13Feb2024.sorted.txt --frequency 2 --input ./chk-normalizer/chk4normalizer.txt --out ./chk-normalizer/chk4normalizer.txt.normalized
```

Check the normalized output file:  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding$ cat ./chk-normalizer/chk4normalizer.txt.normalized
ခေါင် မိုး မှ ရေ ယို သည်
ဓာ တု ဗေ ဒ ပ ညာ ရပ် ပိုင်း က သုံး သပ် ရင် လည်း ဓာ တု ပ ညာ ရပ် ကို စ ခဲ့ တဲ့ ရှေး ခတေ် အဂ္ဂိ ရတ် ဆ ရာ ကြီး တွေ ရဲ့ ယမ်း င ရဲ မီး ကန့် င ရဲ မီး ဆား င ရဲ မီး နဲ့ ရွှေ စား င ရဲ မီး ထုတ် လုပ် ပုံ နည်း စ နစ် တွေ နဲ့ ပုံ စံ တူ တာ တွေ့ ရ သည်
သူ မ သူ ငယ် ချင်း များ တွင် မ တော့ ဘုန်း ကြီး ဝတ် သွား သော ဗေ ဒင် တတ် သ ည့် အ ဘိုး မ ရှိ ၍ ပဲ လား မ သိ နာ မည် လှ လှ က လေး တွေ နှ င့် ဖြစ် သည် တ ခြား မိန်း က လေး တွေ ရဲ့ နာ မည် တွေ က လည်း မ ကောင်း ရင် သာ ရှိ ရ မည်
ရင် ဘတ် အော င့် လာ ရင် သ တိ ထား ပါ(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding$
```

Checked the log file ...  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding$ cat syllable_checked_result.txt
ခေါင် မိုး မှ ရေ ယို သည်
ဓာ တု ဗေ ဒ ပ ညာ ရပ် ပိုင်း က သုံး သပ် ရင် လည်း ဓာ တု ပ ညာ ရပ် ကို စ ခဲ့ တဲ့ ရှေး <ခတေ်> အဂ္ဂိ ရတ် ဆ ရာ ကြီး တွေ ရဲ့ ယမ်း င ရဲ မီး ကန့် င ရဲ မီး ဆား င ရဲ မီး နဲ့ ရွှေ စား င ရဲ မီး ထုတ် လုပ် ပုံ နည်း စ နစ် တွေ နဲ့ ပုံ စံ တူ တာ တွေ့ ရ သည်
သူ မ သူ ငယ် ချင်း များ တွင် မ တော့ ဘုန်း ကြီး ဝတ် သွား သော ဗေ ဒင် တတ် သ <ည့်> အ ဘိုး မ ရှိ ၍ ပဲ လား မ သိ နာ မည် လှ လှ က လေး တွေ နှ <င့်> ဖြစ် သည် တ ခြား မိန်း က လေး တွေ ရဲ့ နာ မည် တွေ က လည်း မ ကောင်း ရင် သာ ရှိ ရ မည်
ရင် ဘတ် အော <င့်> လာ ရင် သ တိ ထား ပါ(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding$
```

## Run Normalizer for test.syl 

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding$ python ./normalizer4thura/chk_normalize.py --dictionary ./normalizer4thura/final_syl_dictionary_13Feb2024.sorted.txt --frequency 2 --input ./chk-normalizer/test.syl --out ./chk-normalizer/test.syl.normalized
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding$ mv ./syllable_checked_result.txt log4test.syl
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding$ mv ./log4test.syl ./chk-normalizer/
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding$
```

Checked log file: log4test.syl file:  

```
ရင် ဘတ် အော <င့်> လာ ရင် သ တိ ထား ပါ
ဘယ် လောက် နောက် ကျ သ လဲ
ကြို ပို့ ဘတ်စ် ကား က အ ဆင် အ ပြေ ဆုံး ပဲ
အဲ ဒီ အ ဖွဲ့ ရဲ့ ဥက္ကဋ္ဌ ဖြစ် တဲ့ ယို ကို ယာ မာ့ အာ ကိ ဟီ တို <Y> <o> <k> <o> <y> <a> <m> <a> <A> <k> <i> <h> <i> <t> <o> က တ ခြား နိုင် ငံ တွေ မှာ ဖြစ် ပွား တဲ့ လူ နာ တွေ ရဲ့ အ ဆုတ် လုပ် ဆောင် ပုံ တွေ က ဗိုင်း ရပ်စ် ကူး စက် ခံ ရ ပြီး ကု သ လိုက် လို့ ရော ဂါ ပိုး မ ရှိ တော့ ဘူး လို့ စစ် ဆေး ပြီး နောက် မှာ တောင် မှ အ ဆုတ် က အ ပြည့် အ ဝ ပုံ မှန် ပြန် ဖြစ် မ လာ တဲ့ လူ နာ တွေ အ များ အ ပြား တွေ့ ရ တယ် လို့ ပြော ပါ တယ်
အ ဆ <င့်> အေ ဝင် ငွေ ခွန် ကို လ စာ မှ ဖြတ် တောက် သည်
လို ကီ က အတ် ဂါ ဒါ လို ကီ ရဲ့ မျက် လုံး တွေ ကို သေ ချာ တ <ည့်> တ <ည့်> ကြ <ည့်> ရင်း ငါ က လို ကီ
ခင် ဗျား ကြိုက် တဲ့ အ ရောင် က ဘာ လဲ
သူ သီ ချင်း ဆို တတ် သ လို က လည်း က တတ် သည်
ထို့ ကြောင့် ဥ ပါယ် ဂို့ ဟု ခေါ် ကာ ကာ လ ကြာ သော် ဥ ပါယ် ဂို့ မှ ပ ဂိုး ဟု ပြောင်း လဲ ခေါ် လာ ကြ သည်
ဒီ နေ့ ခင် ဗျား ဘယ် လို ဖြစ် နေ တာ လဲ
```

Run for training file:  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding$ time python ./normalizer4thura/chk_normalize.p
y --dictionary ./normalizer4thura/final_syl_dictionary_13Feb2024.sorted.txt --frequency 2 --input ./chk-n
ormalizer/train-valid.syl --out ./chk-normalizer/train-valid.syl.normalized

real    0m46.478s
user    0m46.179s
sys     0m0.296s
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding$ mv syllable_checked_result.txt log4train-valid.syl
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding$ mv ./log4train-valid.syl ./chk-normalizer/
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding$
```

## Python Code for Making Unique List of Err

```python
"""

Making a unique list of <> words.
Written by Ye Kyaw Thu, Visiting Professor, LST, NECTEC, Thailand.
Last updated: 6 Dec 2024.
How to run: 
python list-normalization-err.py -i input.txt -o output.txt
python list-normalization-err.py -i input.txt
cat input.txt | python list-normalization-err.py -o output.txt
python list-normalization-err.py -i input.txt | head

"""

import re
import sys
import argparse

def extract_unique_bracketed_words(input_stream):
    """Extract unique angle-bracketed words from the input stream."""
    pattern = r'<[^>]+>'
    unique_words = set()

    for line in input_stream:
        unique_words.update(re.findall(pattern, line))

    return sorted(unique_words)

def main():
    parser = argparse.ArgumentParser(description="Extract unique angle-bracketed words from text.")
    parser.add_argument("-i", "--input", type=str, help="Input file (default: stdin)", default=None)
    parser.add_argument("-o", "--output", type=str, help="Output file (default: stdout)", default=None)
    args = parser.parse_args()

    # Input handling
    if args.input:
        with open(args.input, "r", encoding="utf-8") as infile:
            unique_words = extract_unique_bracketed_words(infile)
    else:
        unique_words = extract_unique_bracketed_words(sys.stdin)

    # Output handling
    if args.output:
        with open(args.output, "w", encoding="utf-8") as outfile:
            outfile.write("\n".join(unique_words) + "\n")
    else:
        sys.stdout.write("\n".join(unique_words) + "\n")

if __name__ == "__main__":
    main()


```

Running ...  


```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/chk-normalizer$ python ./list-normalization-err.py -i ./log4test.syl -o test.syl.uniq.err
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/chk-normalizer$ python ./list-normalization-err.py -i ./log4train-valid.syl -o train-valid.syl.uniq.err
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/chk-normalizer$
```

Roughly check unique encoding errors for test.syl:  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/chk-normalizer$ wc test.syl.uniq.err
 222  229 2411 test.syl.uniq.err
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/chk-normalizer$
```

Roughly check unique encoding errors for train-valid.syl:  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/chk-normalizer$ wc train-valid.syl.uniq.err
  913   932 13238 train-valid.syl.uniq.err
```

Note: the above number containing non encoding error such as English character.  

## Unique Error File

for test file:  

```
<">
<%>
<&>
<'>
<,>
<->
<.>
<0>
<1>
<2>
<3>
<4>
<5>
<5–>
<6>
<6–>
<7>
<8>
<9>
<9–>
<?>
<A>
<B>
<C>
<D>
<E>
<Eး>
<F>
<G>
<H>
<I>
<J>
<K>
<L>
<M>
<N>
<Nး>
<O>
<P>
<Q>
<R>
<S>
<T>
<U>
<V>
<W>
<X>
<Y>
<\>
<a>
<b>
<c>
<d>
<d’>
<e>
<f>
<g>
<h>
<i>
<j>
<k>
<l>
<m>
<m’>
<n>
<o>
<p>
<q>
<r>
<s>
<t>
<u>
<v>
<w>
<x>
<y>
<z>
<{>
<}>
<éé>
<ကပ္ပီ>
<ကီ့>
<ကီးရ်>
<ကုဋ္ဌ>
<ကျာ်>
<ကျာ်း>
<ကျောင်း၎င်း>
<ကျ်ား>
<ကွိတ်>
<က‌>
<ခဲန်း>
<ချတ္တာ>
<ဂပ်ပ်>
<ဂါ့ဒ်>
<ဂုဏ္ဏ>
<ဂျားလ်>
<ဂ‡>
<င့်>
<င်>
<စက္>
<စန္ဒံ>
<စန္န>
<စာ့>
<စိတ်‌>
<စို⁠>
<ဆစ်ဖ်>
<ဆပ်စ်>
<ဆီးရ်>
<ဇူးစ်>
<ဉ့်>
<ည့်>
<တင်‌>
<တစ်စ်>
<တည်‌>
<တားရ်>
<တိတ္တိ>
<တုမ်း>
<တော့်>
<တ်>
<တွက်‌>
<တှို့>
<ထော်​>
<ဒုမ္မ>
<ဒ့်>
<ဒ်>
<ဓိစ္>
<ဓျာ>
<နိုုင်း>
<နို်င်>
<နီးရ်>
<နူးဟ်>
<န့်>
<န်>
<နွံ့>
<ပေ့ါ>
<ပျန်>
<ပျီး>
<ဖို့စ်>
<ဖူဇ်>
<ဖူူး>
<ဗာရ်>
<ဘက္ကရ်>
<ဘန့်ဇ်>
<မစ်ရ်>
<မန္ဈ>
<မို့‌>
<မီစ်း>
<မုဉ္စ>
<မုဒ္ဓ>
<မ့်>
<မွား>
<မ‌>
<ယ့်>
<ယ်>
<ယှင်း>
<ရဂ်>
<ရင်းမ်>
<ရစ်ဂ်>
<ရစ်ပ်>
<ရာ့စ်>
<ရှပ်ဖ်>
<လပ္ပီး>
<လို့‌>
<ဝ⁠>
<သင့််>
<သင်္ဂြိုလ်>
<သန္ဒိ>
<သမ္မဂ္ဂ>
<သလ္လံ>
<သုက္က>
<သောရ်>
<သြ>
<သွယ်⁠>
<ဟတ်စ်>
<ဟယ်လ်>
<ဟိမ်>
<ဟိုင်းမ်>
<ဟော့ဂ်>
<ဟွန်းမ်>
<အိုးစ်>
<အေင်>
<အွတ်စ်>
<အ‌>
<အ‌‌‌>
<ဥ်>
<ဥ်း>
<ားလ်စ်>
<ိုင်း>
<ူ>
<္ကမ္မ>
<်>
<ျ>
<၀>
<၀က်>
<၀င်>
<၀တ်>
<၀န်>
<၀⁠>
<၁>
<၁−>
<၂>
<၃>
<၄>
<၄င်း>
<၅>
<၆>
<၇>
<၈>
<၈⁠>
<၉>
<၉⁠>
<။>
<​>
<‌>
<–>
<‘>
<’>
<“>
<”>
<⁠>
<−>
<つ>

```

## Make Manual Cleaning Based on Unique Error

Real unique encoding error for test.syl is as follows (129 in total):  

```
<Eး>
<Nး>
<ကပ္ပီ>
<ကီ့>
<ကီးရ်>
<ကုဋ္ဌ>
<ကျာ်>
<ကျာ်း>
<ကျောင်း၎င်း>
<ကျ်ား>
<ကွိတ်>
<က‌>
<ခဲန်း>
<ချတ္တာ>
<ဂပ်ပ်>
<ဂါ့ဒ်>
<ဂုဏ္ဏ>
<ဂျားလ်>
<ဂ‡>
<င့်>
<င်>
<စက္>
<စန္ဒံ>
<စန္န>
<စာ့>
<စိတ်‌>
<စို⁠>
<ဆစ်ဖ်>
<ဆပ်စ်>
<ဆီးရ်>
<ဇူးစ်>
<ဉ့်>
<ည့်>
<တင်‌>
<တစ်စ်>
<တည်‌>
<တားရ်>
<တိတ္တိ>
<တုမ်း>
<တော့်>
<တ်>
<တွက်‌>
<တှို့>
<ထော်​>
<ဒုမ္မ>
<ဒ့်>
<ဒ်>
<ဓိစ္>
<ဓျာ>
<နိုုင်း>
<နို်င်>
<နီးရ်>
<နူးဟ်>
<န့်>
<န်>
<နွံ့>
<ပေ့ါ>
<ပျန်>
<ပျီး>
<ဖို့စ်>
<ဖူဇ်>
<ဖူူး>
<ဗာရ်>
<ဘက္ကရ်>
<ဘန့်ဇ်>
<မစ်ရ်>
<မန္ဈ>
<မို့‌>
<မီစ်း>
<မုဉ္စ>
<မုဒ္ဓ>
<မ့်>
<မွား>
<မ‌>
<ယ့်>
<ယ်>
<ယှင်း>
<ရဂ်>
<ရင်းမ်>
<ရစ်ဂ်>
<ရစ်ပ်>
<ရာ့စ်>
<ရှပ်ဖ်>
<လပ္ပီး>
<လို့‌>
<ဝ⁠>
<သင့််>
<သင်္ဂြိုလ်>
<သန္ဒိ>
<သမ္မဂ္ဂ>
<သလ္လံ>
<သုက္က>
<သောရ်>
<သြ>
<သွယ်⁠>
<ဟတ်စ်>
<ဟယ်လ်>
<ဟိမ်>
<ဟိုင်းမ်>
<ဟော့ဂ်>
<ဟွန်းမ်>
<အိုးစ်>
<အေင်>
<အွတ်စ်>
<အ‌>
<အ‌‌‌>
<ဥ်>
<ဥ်း>
<ားလ်စ်>
<ိုင်း>
<ူ>
<္ကမ္မ>
<်>
<ျ>
<၀>
<၀က်>
<၀င်>
<၀တ်>
<၀န်>
<၀⁠>
<၄င်း>
<၈⁠>
<၉⁠>
<။>
<​>
<‌>
<⁠>
<−>
<つ>
```

Real unique encoding error for train-valid.syl is as follows (785 in total):  

တော်တော်များများ ရှင်းထားတဲ့ output။ တချို့ စာလုံးတွေက လေ့လာနိုင်အောင် တမင်တကာ မဖျက်ပဲ ထည့်ပေးထားတာ။  

```
<(စ်>
<Bတ်>
<Bယ်>
<Eမ်း>
<Eာ>
<Eး>
<Nည်>
<Nန်း>
<Nာ>
<Nး>
<aசிங்கसिंह>
<iΙνδοί>
<iไทย>
<læː>
<lā>
<m²>
<°>
<²>
<·>
<γη>
<λόγος>
<τηλε>
<الإسلام‎’ā>
<भारतगणराज्>
<य>
<சிங்கப்பூர்>
<புரपुर>
<คน>
<จักรไทย>
<พระนครศรีอยุธยา>
<ราชอาณา>
<สยาม>
<က´>
<ကက္က>
<ကက္ဍ>
<ကင်‌>
<ကဏ္ဍု>
<ကတ္တာ>
<ကန္>
<ကန္နန္နာ>
<ကန့်တ်>
<ကပ္ပီ>
<ကမ္ညာ>
<ကယ္ြန်>
<ကာင်း>
<ကာအ်>
<ကိစ္>
<ကိဖ်>
<ကိုက်‌>
<ကိုယ်‌>
<ကို‌>
<ကို“>
<ကီ့>
<ကီးရ်>
<ကုက္ကိ>
<ကုဇ္ဇ>
<ကုဇ်>
<ကူဗ်>
<ကောင်းစ်>
<ကောင်‌း>
<ကော့ပ်စ်>
<ကေိ>
<က်>
<က်ဒ်>
<ကျမ့်>
<ကျာင်း>
<ကျာ်>
<ကျာ်း>
<ကျုဒ်>
<ကျုဘ်>
<ကျောင်း‌>
<ကျေံ>
<ကျဲလ်>
<ကျ်ား>
<ကျွင့်>
<ကျွန်ပ်>
<ကျွန့်>
<ကျွန်‌>
<ကြက္က>
<ကြမ္မတ်>
<ကြိုတ်>
<ကြိး>
<ကြီမ်>
<ကြောင်း၎င်း>
<ကွင်း⁠>
<ကွပ်ဇ်>
<ကွယ်း>
<က​>
<က‌>
<က”>
<ခန္တာ>
<ခန်ံ့>
<ခါးလ်>
<ခါး‌>
<ခိန်>
<ခိုင််>
<ခို့စ်ထ်>
<ခိုးလ်>
<ခေတ်‌>
<ခေါင်း−>
<ခေျာင်း>
<ခဲား>
<ခ့ဲ>
<ခ့်>
<ခ်ျ>
<ချက်‌>
<ချည်‌>
<ချမ်း‌>
<ချိန််>
<ချိန်‌>
<ချူင်>
<ချဲန်>
<ခြါး>
<ဂစ်ဒ်>
<ဂတ္တိ>
<ဂပ်ပ်>
<ဂါ့ဒ်>
<ဂါ‌>
<ဂိုစ်>
<ဂီလ်>
<ဂုဏ်း>
<ဂုမ္မ>
<ဂေ့ါ>
<ဂေျာ့>
<ဂျင်းန်>
<ဂျပ်စ်>
<ဂျမ္မ>
<ဂျမ္မူ>
<ဂျားလ်>
<ဂျိန္န>
<ဂျိန်းစ်>
<ဂျီဇ်>
<ဂျီလ်>
<ဂျော့ခ်ျ>
<ဂျဲလ်>
<ဂ‡>
<ငယ်‌>
<ငါ်>
<ငိမ်း>
<င့်>
<င့်α>
<င့်ခ်>
<င့်စ်>
<င်>
<ငြှော>
<ငှော့>
<စဉ််>
<စပ်စ်>
<စပ်‌>
<စမ္ပါ>
<စါး>
<စာ့>
<စာ‌>
<စိတ်‌>
<စီရ်>
<စုဒ္ဒ>
<စဲန်>
<စ္စ>
<စ်>
<စျာ>
<စွက်း>
<စွ်>
<ဆက်စ်>
<ဆင်မ်>
<ဆစ္စ>
<ဆစ်ဖ်>
<ဆစ့်>
<ဆန်းဒ်>
<ဆပ်စ်>
<ဆဗ်>
<ဆာရ်>
<ဆိုင်‌>
<ဆီးရ်>
<ဆီး‌>
<ဆူု>
<ဆူးန်>
<ဆောက်‌>
<ဆောင်‌>
<ဆောတ်>
<ဆဲ⁠>
<ဆွစ္စ်>
<ဆွာ့တ်>
<ဆွး>
<ဇစ်ခ်>
<ဇတ္တ>
<ဇန္ဒ>
<ဇာဋ္ဌာန်>
<ဇိဒ္ဓိ>
<ဇုစ်>
<ဇူးစ်>
<ဇူးပ်>
<ဇော့်>
<ဈက္ခိ>
<ဉာတ္တိ>
<ဉာတ်>
<ဉ့်>
<ညတ်‌>
<ည့်>
<ည့်⁠>
<ည်>
<ည်‌>
<ညှ>
<ညှိး>
<ဌား>
<ဏှောက်>
<တက်‌>
<တစ်စ်>
<တစ်ပ်>
<တစ်‌>
<တစ်‌‌>
<တည့််>
<တည်‌>
<တဋ္ဌ>
<တတ်‌>
<တန္နိ>
<တန်‌>
<တဖ်>
<တသ်စ်>
<တားရ်>
<တာ်>
<တာ‌>
<တိုင်းမ်စ်>
<တိုင်‌>
<တို့အ်ိမ်>
<တို့‌‌ေ>
<တိဲ>
<တီးစ်>
<တီ၎င်း>
<တုန်းမ်>
<တု့ံ>
<တော့‌>
<တော်တ်ို>
<တော့်>
<တော်‌>
<တေ့ာ>
<တး>
<တ္တ>
<တ်>
<တျန့်>
<တျု>
<တျံ>
<တွင်‌>
<တွင်–>
<တွမ့်>
<တွေ‌>
<တွ့>
<တ​>
<တ‌>
<ထက်‌>
<ထည့််>
<ထပ်²>
<ထပ်​>
<ထိပ်‌>
<ထိ⁠>
<ထုတ်‌>
<ထုပ္ပါတ်>
<ထောင်‌>
<ထော်​>
<ထံမ်>
<ဒင်္>
<ဒါတ်>
<ဒါရ်>
<ဒါးရ်>
<ဒါ‌>
<ဒာ>
<ဒိစ်>
<ဒိဋ္>
<ဒိုတ်>
<ဒီ‌>
<ဒီ‌ေ>
<ဒုဗ္ဗိ>
<ဒူးစ်>
<ဒေါ့စ်>
<ဒေါ့်>
<ဒေ့ခ်ျ>
<ဒ့ါ>
<ဒ်>
<ဒျု>
<ဒျူ>
<ဒျူး>
<ဒွဖ်>
<ဒွိုက်>
<ဓမ္မုတ္တ>
<ဓေါ>
<ဓျာ>
<နက်‌>
<နင်္က>
<နစ်‌>
<နည်‌း>
<နဋ္ဌ>
<နယ်‌>
<နယ်‌‌>
<နါး>
<နာလ်>
<နား−>
<နိစ္ဆ>
<နိဒ်>
<နိုင်ား>
<နို‌င်>
<နီုင်>
<နီးရ်>
<နုမ်း>
<နုး>
<နူးဟ်>
<နောတ္တပ္ပ>
<နော့်>
<နေဲ့>
<နဲလ်>
<န့်>
<န့်ခ်>
<န့်缅甸>
<န္တ>
<န်>
<နျုး>
<နျော့ထ်>
<နှစ့်>
<နှား>
<နှာ‌>
<နှုး>
<နှံး>
<ပက်ခ်ဆ်>
<ပက်စ်>
<ပက်ဒ်>
<ပင်‌>
<ပစ္စု>
<ပစ်‌>
<ပစ်⁠>
<ပဇ္ဇော>
<ပန္နား>
<ပန်ု>
<ပါဋ္ဌ>
<ပါ့စ်>
<ပါ်>
<ပိန့်>
<ပုစ္စာ>
<ပုတ်‌>
<ပုပ္ပ>
<ပုပ္မါး>
<ပုဗ္ဗာ>
<ပေါက္ဗံ>
<ပေ့ါ>
<ပျန်>
<ပြင်း‌>
<ပြာင်း>
<ပြိး>
<ပြီဲ>
<ပြီး၎င်း>
<ပွား‌>
<ပွိုက်>
<ဖင်န်>
<ဖစ်ဇ်>
<ဖန်‌>
<ဖါ့စ်>
<ဖိုက်ဒ်>
<ဖိ့ု>
<ဖီ“>
<ဖုန်း‌>
<ဖူဇ်>
<ဖေါင့်>
<ဖေွ>
<ဖ့်>
<ဖျူးစ်>
<ဖြစ်‌>
<ဖြည်း⁠>
<ဖြ်>
<ဖွင်>
<ဖှမ်>
<ဖှမ်း>
<ဗက္က>
<ဗဂ္ဂ>
<ဗင်န်>
<ဗင်္ဂ>
<ဗင်္ဂါ>
<ဗစ်စ်>
<ဗန္တု>
<ဗန်စ်>
<ဗော့ဒ်>
<ဗဲစ်>
<ဗ်>
<ဗျဉ်း>
<ဗျီ>
<ဘက္ကရ်>
<ဘက််>
<ဘက်‌>
<ဘင်ရ်>
<ဘတ္တာ>
<ဘတ််>
<ဘယ်‌>
<ဘာလ္>
<ဘာြ>
<ဘိန်>
<ဘီ⁠>
<ဘောရ်>
<ဘွတ်စ်>
<ဘွိုင်းစ်>
<မက္>
<မက္ကင်>
<မက္ကာဟ်>
<မဂ္ဂင်း>
<မင်းလ်>
<မင်း‌>
<မစ်ရ်>
<မဇ္ဖျိ>
<မည်‌>
<မတ်⁠>
<မဒ်>
<မန္>
<မန္တဏ်>
<မန္ဓ>
<မန္နား>
<မန်းစ်>
<မလ္>
<မလ္လ>
<မါ>
<မါန်>
<မါ့>
<မာခ်စ်>
<မာ့က်ခ်>
<မာ့က်ဆ်>
<မိတ္>
<မိုင်းရ်>
<မိုလ်း>
<မိူင်း>
<မိး>
<မီးစ်မ်း>
<မီးန်>
<မုဟ်ၜဳ>
<မု့န်>
<မေါ့>
<မောက်‎>
<မော့တ်>
<မေွှ>
<မဲမ်>
<မံင်>
<မ့်>
<မ့်ပ်>
<များ‌>
<မျိုး‌>
<မျး>
<မြိင်>
<မြောင့်>
<မွန်ဂ်>
<မှတ််>
<မှတ်‌>
<မှန်⁠>
<မှာ‌>
<မှုု>
<မ​>
<မ‌>
<ယမ်စ်>
<ယသ်>
<ယဟ်>
<ယာဇ်>
<ယောင်္ကျား>
<ယောဉ်>
<ယောန်>
<ယောာက်>
<ယော်လ်>
<ယ့်>
<ယ်>
<ယွန်ó>
<ယွိ>
<ယှည်>
<ရဂ်>
<ရင်မ်း>
<ရင်းမ်>
<ရစ်α>
<ရစ်ဂ်>
<ရစ်စ္စ>
<ရစ်ပ်>
<ရစ်‌>
<ရဇ္ဈယ်>
<ရတ်ဒ်>
<ရန်စ္စ>
<ရန်‌>
<ရပ်စ်‌>
<ရပ်ပ်>
<ရပ်ရ်>
<ရပ််စ်>
<ရပ်‌>
<ရဖ်>
<ရဗ်>
<ရါ>
<ရာ့စ်>
<ရားစ်>
<ရားဒ်>
<ရိစ္ဆာန်>
<ရိတ်ခ်>
<ရိုဋ်>
<ရောန်>
<ရော့ခ်စ်>
<ရော့ပ်>
<ရေး‌>
<ရဲံ>
<ရဲ‌>
<ရ်>
<ရွေးာက်>
<ရှက်ဖ်>
<ရှူံး>
<ရ‌>
<လက်ဒ်>
<လခ်>
<လင်းမ်>
<လင်‌းစ်>
<လစ်ထ်>
<လည့်>
<လန္>
<လပ္ပီး>
<လမ္ဗီး>
<လာဆ်>
<လာမ့်>
<လာယ်>
<လာ‌>
<လိမ်‌့>
<လို့‌>
<လို‌>
<လီု>
<လုပ်‌>
<လုံမ်>
<လုံး‌>
<လု့း>
<လော့ဖ်>
<လေ့ာ>
<လဲန်>
<လဲပ်>
<လျား⁠>
<လျိ>
<လျှင်‌>
<လျှစ်>
<လျှမ်း⁠>
<လွီယ်>
<လွုင်>
<လှူံ>
<ဝက်‌>
<ဝင်္ကန္ဈ>
<ဝင်္ဘာ>
<ဝင်‌>
<ဝဋ္ဌ>
<ဝန်‌>
<ဝါ့ဖ်>
<ဝာမ်>
<ဝိဇ္>
<ဝိဇ္စာ>
<ဝိဋ္ဌ>
<ဝိန္ဒြာ>
<ဝီစ်>
<ဝူလ်>
<ဝေါ့လ်>
<ဝေါ့လ်ဇ်>
<ဝှစ်တ်>
<ဝှိုင်>
<ဝ⁠>
<သက်‌>
<သင်္ဂီ>
<သင်္ဂြုလ်>
<သင်‌>
<သည်‌>
<သတ္တူ>
<သတ္ထ>
<သတ္ထာ>
<သတ်‌>
<သန္တန်>
<သဗ္ဗတ္ထိ>
<သဗ္ဗော>
<သမ္>
<သာက်>
<သားစ်>
<သားဖ်>
<သားꩻ>
<သိက္ခါ>
<သိင်္ဃာ>
<သိဒ္ဓတ်>
<သိပ်‌>
<သုက္ကော>
<သုက္ကံ>
<သုတ္ထန်>
<သုဒ္ဓာ>
<သုံးက္ကူ>
<သူ‌>
<သေတ္ထာ>
<သောα>
<သောရ်>
<သော်‌>
<သေ​>
<သံင်္ဂါ>
<သ်>
<သျှဒ်>
<သျှပ်>
<သျှာ>
<သြ>
<သြော>
<သ‌>
<ဟက္က>
<ဟက်စ်>
<ဟင်မ်>
<ဟင်္နာ>
<ဟင်‌့>
<ဟင်‌း>
<ဟစ်ဒ်>
<ဟဒ်>
<ဟန္ဆာ>
<ဟန္ထာ>
<ဟန္နာ>
<ဟပ္ဖ>
<ဟဗ်>
<ဟယ်လ်>
<ဟာက်>
<ဟာ့တ်>
<ဟိန္ဒု>
<ဟိမ်>
<ဟိိုင်း>
<ဟိိုင်းမ်>
<ဟိုင်မ်း>
<ဟိုင်းမ်>
<ဟိုင်းမ်း>
<ဟုတ်း>
<ဟုတ်‌>
<ဟူ​>
<ဟေလ်>
<ဟော့ဂ်>
<ဟြး>
<ဟွန်ʾā>
<ဟွီ>
<အက်ခ်>
<အက်ဂ်>
<အက်စ်ခ်>
<အက်ဘ်>
<အခ်>
<အစ်‌>
<အတ္တု>
<အတ္ထိုပ္ပတ္တိ>
<အပ်ဖ်>
<အမ်း​>
<အယ်‌လ်‌>
<အသ်>
<အါး>
<အာင်>
<အာလ်>
<အာ်>
<အိခ်>
<အိုက်ဗ်>
<အို−>
<အုစ်>
<အုပ်ခ်>
<အောင်​>
<အောစ့်>
<အောာင်>
<အော့ခ်>
<အော့ဘ်>
<အော့်>
<အော့်>
<အေ်>
<အး>
<အြ>
<အွတ်စ်>
<အ​>
<အ‌>
<အ‌‌ေ>
<ဣဋ္ဌ>
<ဥဒ္ဓ>
<ဥုဒ်>
<ဥ့်>
<ဥ္စ>
<ဥ္ဇ>
<ဥ်>
<ဥ်း>
<ဧတ္ထ>
<ဧတ္ထော>
<ဩတ္တပ္တ>
<ါက်>
<ာ>
<ာဉ်>
<ာ့>
<ား>
<ိ>
<ိစ္ဆာ>
<ိုင်း>
<ီ>
<ီလ်>
<ု>
<ုင်း>
<ူ>
<ူး>
<ေ>
<ော>
<ောဂ္ဂ>
<ော့>
<ံ>
<့>
<့ခ်>
<့တ်>
<း>
<္ခ>
<္ဃ>
<္စ>
<်>
<်င်း>
<ျ>
<ျာ>
<ြ>
<ွင်…“>
<ွန်း>
<ွှ>
<ှ>
<ဿတ်>
<၀>
<၀က်>
<၀င်>
<၀ဏ္ဏ>
<၀တ္တ>
<၀တ်>
<၀န်>
<၀န်း>
<၀မ်>
<၀မ်း>
<၀ယ်>
<၀ါ>
<၀ါး>
<၀ိုင်း>
<၀ိုး>
<၀ုန်း>
<၀ံ>
<၀⁠>
<၁>
<၁°>
<၁့>
<၁⁠>
<၁−>
<၂>
<၂့>
<၂⁠>
<၂−>
<၃>
<၃−>
<၄>
<၄င်း>
<၄း>
<၅>
<၅း>
<၅⁠>
<၆>
<၇>
<၇°>
<၇’>
<၈>
<၈°>
<၈⁠>
<၉>
<၉°>
<၉⁠>
<၊>
<၊‌>
<။>
<၏–>
<႔>
<​>
<‌>
<‌‌>
<‌‌‌>
<‌‌‌‌‌>
<–>
<‘>
<’>
<’‘>
<“>
<“”>
<“…>
<”>
<…>
<…”>
<⁠>
<−>
<おじいさん>
<おじさん>
<つ>
<つなみ>
<ビルマ人>
<ミャンマー>
<新加坡>
<日本語>
<昭南島>
<昭和の時代に得た南の島>
<禪>
<缅甸>
<﻿>
```

အထက်ပါ list ထဲက မြန်မာစာနဲ့ ပတ်သက်တာတွေကို manual search/replace ပဲ ဖြစ်ဖြစ် လုပ်လိုက်ရင်တော့ training/testing ဒေတာက တော်တော်လေး သန့်သွားလိမ့်မယ်။ 

ငါရေးထားတဲ့ normalizer code နဲ့ Normalization လုပ်လိုက်ရင် ဒါမျိုး <အ‌‌ေ> တွေက ရှင်းသွားမှာ။ မရှင်းပဲ ကျန်ခဲ့မှာက အသတ် error တွေပဲ (ဆိုလိုတာက ဗျည်းနဲ့ ကွဲထွက်နေမဲ့ အသတ်တွေ)။ အဲဒါကိုပဲ ရှင်းလိုက်ပြီး sentence segmenter ကို လုပ်လိုက်လို့တော့ ရတယ်။  

## Cleaning Consonant<Space>Athat Pairs  

```python
def syllable_segment(sentence, break_pattern):

    clean_sentence = re.sub(r"့်", "့်", sentence)
    #print("RE: ", clean_sentence)
    """Segment a sentence into syllables."""
    return break_pattern.sub(r" \1", clean_sentence).strip().split()
```

## Updated Python Code Without Normalization

```python
#!/usr/bin/env python3
# -*- coding:utf-8 -*-

"""

For converting word level tagged sentences into syllable level sentences.
Written by Ye Kyaw Thu, LST Lab, NECTEC, Thailand.
Last updated: 5 Dec 2024.

How to use:  
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ time python ./wordtag2syltag.py -i ./test.tagged -o test.tagged.bone -p BONE
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ time python ./wordtag2syltag.py -i ./test.tagged -o test.tagged.bfone -p BFONE

"""

import argparse
import re

def parse_arguments():
    """Parse command line arguments."""
    parser = argparse.ArgumentParser(description="Convert word-tagged Burmese data to syllable-tagged data.")
    parser.add_argument("-i", "--input", type=str, required=True, help="Input file (word-tagged data)")
    parser.add_argument("-o", "--output", type=str, required=True, help="Output file (syllable-tagged data)")
    parser.add_argument("-p", "--pattern", type=str, choices=["BONE", "BFONE"], default="BONE",
                        help="Tagging pattern: BONE or BFONE (default: BONE)")
    return parser.parse_args()

def create_break_pattern():
    """Create the regular expression pattern for syllable segmentation."""
    my_consonant = r"က-အ"
    en_no = r"0-9"
    other_char = r"ဣဤဥဦဧဩဪဿ၌၍၏၀-၉၊။!-/:-@[-`{-~\\s"
    subscript_symbol = r'္'
    a_that = r'်'

    return re.compile(
        r"((?<!"
        + subscript_symbol
        + r")["
        + my_consonant
        + r"](?!["
        + a_that
        + subscript_symbol
        + r"])|["
        + en_no
        + other_char
        + r"])"
    )

def syllable_segment(sentence, break_pattern):

    clean_sentence = re.sub(r"့်", "့်", sentence)
    #print("RE: ", clean_sentence)
    """Segment a sentence into syllables."""
    return break_pattern.sub(r" \1", clean_sentence).strip().split()

def remove_tags_and_join(sentence):
    """Remove tags and join words into a tag-free sentence."""
    words = sentence.strip().split()
    cleaned_words = [word.split('/')[0] for word in words if '/' in word]  # Remove tags
    return " ".join(cleaned_words)

def tag_sentence(syllables, pattern):
    """Tag the syllables based on the selected pattern."""
    n = len(syllables)
    #print("syllables:", syllables)
    #print("n:", n)
    tags = []

    for i, syllable in enumerate(syllables):
        if i == 0:
            tags.append(f"{syllable}/B")  # Beginning
        elif i == n - 1:
            tags.append(f"{syllable}/E")  # Ending
        else:
            if pattern == "BONE":
                if n - i <= 4:  # Near Ending (N)
                    tags.append(f"{syllable}/N")
                else:  # Other (O)
                    tags.append(f"{syllable}/O")
            elif pattern == "BFONE":
                if n - i <= 4:  # Near Ending (N)
                    tags.append(f"{syllable}/N")
                elif i <= 3:  # Near Beginning (F)
                    tags.append(f"{syllable}/F")
                else:  # Other (O)
                    tags.append(f"{syllable}/O")
    return " ".join(tags)

def process_sentence(sentence, break_pattern, pattern):
    """Process a single sentence for syllable segmentation and tagging."""
    # Remove tags and join words
    cleaned_sentence = remove_tags_and_join(sentence)

    # Segment the cleaned sentence into syllables
    syllables = syllable_segment(cleaned_sentence, break_pattern)

    # Tag the segmented syllables
    return tag_sentence(syllables, pattern)

def process_file(input_file, output_file, break_pattern, pattern):
    """Process the input file line by line and write the result to the output file."""
    with open(input_file, 'r', encoding='utf-8') as infile, open(output_file, 'w', encoding='utf-8') as outfile:
        for line in infile:
            line = line.strip()

            # Split by "/E", but keep "/E" in the split sentences
            sentences = []
            temp_sentence = ''
            for word in line.split():
                if word.endswith('/E'):
                    # Add the word with "/E" at the end and finalize the sentence
                    temp_sentence += word
                    sentences.append(temp_sentence.strip())
                    temp_sentence = ''
                else:
                    # Add word to the temporary sentence
                    temp_sentence += word + ' '

            # If there's any leftover sentence that doesn't end with "/E"
            if temp_sentence.strip():
                sentences.append(temp_sentence.strip())

            #print("sentences:", sentences)  # Debugging

            # Process the sentences and write to the output
            tagged_sentences = [
                process_sentence(sentence.strip(), break_pattern, pattern) for sentence in sentences if sentence.strip()
            ]
            outfile.write(" ".join(tagged_sentences) + "\n")


if __name__ == "__main__":
    args = parse_arguments()
    break_pattern = create_break_pattern()
    process_file(args.input, args.output, break_pattern, args.pattern)


```

## Updated Python Code with Normalization  

```python
#!/usr/bin/env python3
# -*- coding:utf-8 -*-

"""

For converting word level tagged sentences into syllable level sentences.
Written by Ye Kyaw Thu, LST Lab, NECTEC, Thailand.
Last updated: 5 Dec 2024.

How to use:  
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ time python ./wordtag2syltag-normalize.py -i ./test.tagged -o test.tagged.bone -p BONE
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data$ time python ./wordtag2syltag-normalize.py -i ./test.tagged -o test.tagged.bfone -p BFONE

"""

import argparse
import re
from normalizer import process_input

def parse_arguments():
    """Parse command line arguments."""
    parser = argparse.ArgumentParser(description="Convert word-tagged Burmese data to syllable-tagged data.")
    parser.add_argument("-i", "--input", type=str, required=True, help="Input file (word-tagged data)")
    parser.add_argument("-o", "--output", type=str, required=True, help="Output file (syllable-tagged data)")
    parser.add_argument("-p", "--pattern", type=str, choices=["BONE", "BFONE"], default="BONE",
                        help="Tagging pattern: BONE or BFONE (default: BONE)")
    return parser.parse_args()

def create_break_pattern():
    """Create the regular expression pattern for syllable segmentation."""
    my_consonant = r"က-အ"
    en_no = r"0-9"
    other_char = r"ဣဤဥဦဧဩဪဿ၌၍၏၀-၉၊။!-/:-@[-`{-~\\s"
    subscript_symbol = r'္'
    a_that = r'်'

#    return re.compile(
#        r"((?<!"
#        + subscript_symbol
#        + r")["
#        + my_consonant
#        + r"](?!["
#        + a_that
#        + subscript_symbol
#        + r"])|["
#        + en_no
#        + other_char
#        + r"])"
#    )

    return re.compile(
        r"((?<!" + subscript_symbol + r")[" + my_consonant + r"]"
        r"(?!["
        + a_that + subscript_symbol + r"])"
        + r"|[" + en_no + other_char + r"])"
    )

def syllable_segment(sentence, break_pattern):

    clean_sentence = re.sub(r"့်", "့်", sentence)
    #print("RE: ", clean_sentence)

    """Segment a sentence into syllables."""
    return break_pattern.sub(r" \1", clean_sentence).strip().split()

def remove_tags_and_join(sentence):
    """Remove tags and join words into a tag-free sentence."""
    words = sentence.strip().split()
    cleaned_words = [word.split('/')[0] for word in words if '/' in word]  # Remove tags
    return " ".join(cleaned_words)

def tag_sentence(syllables, pattern):
    """Tag the syllables based on the selected pattern."""
    n = len(syllables)
    #print("syllables:", syllables)
    #print("n:", n)
    tags = []

    for i, syllable in enumerate(syllables):
        if i == 0:
            tags.append(f"{syllable}/B")  # Beginning
        elif i == n - 1:
            tags.append(f"{syllable}/E")  # Ending
        else:
            if pattern == "BONE":
                if n - i <= 4:  # Near Ending (N)
                    tags.append(f"{syllable}/N")
                else:  # Other (O)
                    tags.append(f"{syllable}/O")
            elif pattern == "BFONE":
                if n - i <= 4:  # Near Ending (N)
                    tags.append(f"{syllable}/N")
                elif i <= 3:  # Near Beginning (F)
                    tags.append(f"{syllable}/F")
                else:  # Other (O)
                    tags.append(f"{syllable}/O")
    return " ".join(tags)

def process_sentence(sentence, break_pattern, pattern):
    """Process a single sentence for syllable segmentation and tagging."""
    # Remove tags and join words
    cleaned_sentence = remove_tags_and_join(sentence)
    #print("tag cleaned: ", cleaned_sentence)

    # Segment the normalized sentence into syllables
    syllables = syllable_segment(cleaned_sentence, break_pattern)
    #print("syllables: ", syllables)

    # Normalization
    normalized_output = process_input(
        ' '.join(syllables),  # Join list into space-separated string
        dictionary_file="./normalizer/final_syl_dictionary_13Feb2024.sorted.txt",
        min_frequency=2,
        check='dictionary'
    )
    
    # Split normalized output back into a list
    normalized_syllables = normalized_output.split()
    #print("normalized syllables: ", normalized_syllables)  # Debugging

    # Tag the segmented syllables
    tagged_sentence = tag_sentence(normalized_syllables, pattern)
    #print("tagged: ", tagged_sentence) 
    return tagged_sentence

def process_file(input_file, output_file, break_pattern, pattern):
    """Process the input file line by line and write the result to the output file."""
    with open(input_file, 'r', encoding='utf-8') as infile, open(output_file, 'w', encoding='utf-8') as outfile:
        for line in infile:
            line = line.strip()

            # Split by "/E", but keep "/E" in the split sentences
            sentences = []
            temp_sentence = ''
            for word in line.split():
                if word.endswith('/E'):
                    # Add the word with "/E" at the end and finalize the sentence
                    temp_sentence += word
                    sentences.append(temp_sentence.strip())
                    temp_sentence = ''
                else:
                    # Add word to the temporary sentence
                    temp_sentence += word + ' '

            # If there's any leftover sentence that doesn't end with "/E"
            if temp_sentence.strip():
                sentences.append(temp_sentence.strip())

            #print("sentences:", sentences)  # Debugging

            # Process the sentences and write to the output
            tagged_sentences = [
                process_sentence(sentence.strip(), break_pattern, pattern) for sentence in sentences if sentence.strip()
            ]
            outfile.write(" ".join(tagged_sentences) + "\n")


if __name__ == "__main__":
    args = parse_arguments()
    break_pattern = create_break_pattern()
    process_file(args.input, args.output, break_pattern, args.pattern)


```

Run ပြီးထွက်လာတဲ့ .bone, .bfone pattrn နှစ်မျိုးစလုံးကို အကြမ်းစစ်ကြည့်တာ အဆင်ပြေတယ်။  

## Training with Syllable Unit BONE Pattern  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data/syl/bone$ wc *.bone
    5512   143788  1714263 test.tagged.bone
   50081  1334906 15924600 train-valid.tagged.bone
   55593  1478694 17638863 total
```

Let's see the file content ...  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data/syl/bone$ head ./train-valid.tagged.bone
နား/B လည်/N ပါ/N ပြီ/E
ဈေး/B က/O များ/N လှ/N ချေ/N လား/E
သူ/B ဒီ/O နေ့/O နည်း/O နည်း/O ပင်/O ပန်း/O နေ/N တယ်/N ထင်/N တယ်/E
ဘာ/B ကြောင့်/O လဲ/O ဆို/N စမ်း/N ပါ/N ဦး/E
စိတ်/B ကောက်/O တဲ့/O စ/O ကား/O မျိုး/N ပြော/N ပြန်/N ပြီ/E
၁/B ၆/O ရာ/O စု/O နှစ်/O တွင်/O ရော/O မ/O ပန်း/O ချီ/O ကျော်/O က/O ဝိ/O လီ/O ယို/O နာ/O ဒို/O ဒါ/O ဗင်း/O ချိ/O က/O ပင်/O လယ်/O ခ/O ရု/O များ/O ရှိ/O ရာ/O လက်/O ရှိ/O ကုန်း/O မြင့်/O များ/O သည်/O တစ်/O ကြိမ်/O က/O ပင်/O လယ်/O အောက်/O တွင်/O ရှိ/O ခဲ့/O ၍/O နောက်/O မှ/O မြေ/O မြင့်/O တက်/O လာ/O ခဲ့/O ခြင်း/O ဖြစ်/O သည်/O ဟု/O တွေး/O ယူ/O ခဲ့/N ဖူး/N လေ/N သည်/E
ဂင်မ်/B ချီ/O သိပ်/O ပြီး/O နောက်/O ဂင်မ်/O ချီ/O အိုး/O ကို/O မြေ/O ကြီး/O ထဲ/N မြုပ်/N လိုက်/N တယ်/E
အ/B အေး/N မိ/N မယ်/E
ဧည့်/B လမ်း/O ညွှန်/O ရော/O ထည့်/O ပေး/N လို့/N ရ/N လား/E
မှန်/B တင်/O ခုံ/O ဘေး/O က/O အ/O ရက်/O ပု/O လင်း/O ကို/O ထုတ်/O ယူ/O လိုက်/O ရင်း/O ကောက်/N မော့/N လိုက်/N သည်/E ပု/B လင်း/O ပြန်/O အ/O သိမ်း/O မှာ/O အ/O ပြာ/O ရောင်/O ဝတ်/O စုံ/O ကို/O မြင်/N လိုက်/N ရ/N သည်/E
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data/syl/bone$
```

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data/syl/bone$ head ./test.tagged.bone
ရင်/B ဘတ်/O အောင့်/O လာ/O ရင်/O သ/N တိ/N ထား/N ပါ/E
ဘယ်/B လောက်/O နောက်/N ကျ/N သ/N လဲ/E
ကြို/B ပို့/O ဘတ်စ်/O ကား/O က/O အ/O ဆင်/O အ/N ပြေ/N ဆုံး/N ပဲ/E
အဲ/B ဒီ/O အ/O ဖွဲ့/O ရဲ့/O ဥက္ကဋ္ဌ/O ဖြစ်/O တဲ့/O ယို/O ကို/O ယာ/O မာ့/O အာ/O ကိ/O ဟီ/O တို/O YokoyamaAkihito/O က/O တ/O ခြား/O နိုင်/O ငံ/O တွေ/O မှာ/O ဖြစ်/O ပွား/O တဲ့/O လူ/O နာ/O တွေ/O ရဲ့/O အ/O ဆုတ်/O လုပ်/O ဆောင်/O ပုံ/O တွေ/O က/O ဗိုင်း/O ရပ်စ်/O ကူး/O စက်/O ခံ/O ရ/O ပြီး/O ကု/O သ/O လိုက်/O လို့/O ရော/O ဂါ/O ပိုး/O မ/O ရှိ/O တော့/O ဘူး/O လို့/O စစ်/O ဆေး/O ပြီး/O နောက်/O မှာ/O တောင်/O မှ/O အ/O ဆုတ်/O က/O အ/O ပြည့်/O အ/O ဝ/O ပုံ/O မှန်/O ပြန်/O ဖြစ်/O မ/O လာ/O တဲ့/O လူ/O နာ/O တွေ/O အ/O များ/O အ/O ပြား/O တွေ့/O ရ/O တယ်/O လို့/N ပြော/N ပါ/N တယ်/E
အ/B ဆင့်/O အေ/O ဝင်/O ငွေ/O ခွန်/O ကို/O လ/O စာ/O မှ/N ဖြတ်/N တောက်/N သည်/E
လို/B ကီ/O က/O အတ်/O ဂါ/O ဒါ/O လို/O ကီ/O ရဲ့/O မျက်/O လုံး/O တွေ/O ကို/O သေ/O ချာ/O တည့်/O တည့်/O ကြည့်/O ရင်း/O ငါ/N က/N လို/N ကီ/E
ခင်/B ဗျား/O ကြိုက်/O တဲ့/O အ/O ရောင်/N က/N ဘာ/N လဲ/E
သူ/B သီ/O ချင်း/O ဆို/O တတ်/O သ/O လို/O က/O လည်း/N က/N တတ်/N သည်/E
ထို့/B ကြောင့်/O ဥ/O ပါယ်/O ဂို့/O ဟု/O ခေါ်/O ကာ/O ကာ/O လ/O ကြာ/O သော်/O ဥ/O ပါယ်/O ဂို့/O မှ/O ပ/O ဂိုး/O ဟု/O ပြောင်း/O လဲ/O ခေါ်/N လာ/N ကြ/N သည်/E
ဒီ/B နေ့/O ခင်/O ဗျား/O ဘယ်/O လို/O ဖြစ်/N နေ/N တာ/N လဲ/E
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data/syl/bone$
```

Call --help ...  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ conda activate hs-fasttext
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ python ./fasttext-tree.py --help
usage: fasttext-tree.py [-h] [--train TRAIN] [--test TEST] [--real-time REAL_TIME]
                        [--ft-model FT_MODEL] [--model MODEL] [--evaluate]

FastText + Decision Tree for Burmese Sentence Segmentation.

options:
  -h, --help            show this help message and exit
  --train TRAIN         Train the model. Provide the training corpus file path.
  --test TEST           Test the model. Provide the test corpus file path.
  --real-time REAL_TIME
                        Segment raw text in real-time. Provide the input text.
  --ft-model FT_MODEL   FastText model file (default: fasttext_model.bin).
  --model MODEL         Decision Tree model file (default: decision_tree_model.pkl).
  --evaluate            Evaluate the model during testing if reference data is provided.
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

training ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-tree.py --train ./data/syl/bone/train-valid.tagged.bone --model syl.bone.fasttest.tree.model
Loading training data...
Training FastText model...
Read 1M words
Number of words:  4482
Number of labels: 0
Progress: 100.0% words/sec/thread:   33746 lr:  0.000000 avg.loss:  2.312498 ETA:   0h 0m 0s
Preparing features...
Training Decision Tree model...
Saving trained model to syl.bone.fasttest.tree.model...
Training completed.

real    1m28.040s
user    4m46.963s
sys     0m6.868s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Testing/Evaluation with syllable-BONE model...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-tree.py --test ./data/syl/bone/test.tagged.bone --model ./syl.bone.fasttest.tree.model --evaluate
Loading tagged test data...
Loading FastText and Decision Tree models...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Preparing features...
Predicting...
Evaluating...
              precision    recall  f1-score   support

           B       0.56      0.19      0.28      6861
           E       0.71      0.77      0.74      6829
           N       0.60      0.18      0.28     19728
           O       0.83      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.67      0.53      0.55    143773
weighted avg       0.78      0.81      0.77    143773


real    0m3.957s
user    0m6.318s
sys     0m4.559s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

word level unit နဲ့ training လုပ်တာထက် ရလဒ်က ကောင်းတယ်။ ဒီ Experiment အစပိုင်းမှာ word unit နဲ့ training ရလဒ်က အောက်ပါအတိုင်းပါ။  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python fasttext-tree.py --test ./data/test.tagged --evaluate
Loading tagged test data...
Loading FastText and Decision Tree models...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Preparing features...
Predicting...
Evaluating...
              precision    recall  f1-score   support

           B       0.55      0.34      0.42      6779
           E       0.73      0.79      0.76      6860
           N       0.57      0.35      0.44     18956
           O       0.77      0.89      0.83     64037

    accuracy                           0.74     96632
   macro avg       0.66      0.59      0.61     96632
weighted avg       0.72      0.74      0.72     96632


real    0m3.513s
user    0m5.701s
sys     0m4.656s
```

Accuracy = 0.74 vs 0.81   

## Training with Syllable Unit BFONE Pattern  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data/syl/bfone$ wc *
    5512   143788  1714263 test.tagged.bfone
   50081  1334906 15924600 train-valid.tagged.bfone
   55593  1478694 17638863 total
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/data/syl/bfone$
```

Training with BFONE Pattern ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-tree.py --train ./data/syl/bfone/train-valid.tagged.bfone --model syl.bfone.fasttest.tree.model
Loading training data...
Training FastText model...
Read 1M words
Number of words:  5696
Number of labels: 0
Progress: 100.0% words/sec/thread:   31841 lr:  0.000000 avg.loss:  2.236114 ETA:   0h 0m 0s
Preparing features...
Training Decision Tree model...
Saving trained model to syl.bfone.fasttest.tree.model...
Training completed.

real    1m41.867s
user    5m10.647s
sys     0m6.941s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Testing/Evaluation with Syllable-BFONE Model ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-tree.py --test ./data/syl/bfone/test.tagged.bfone --model ./syl.bfone.fasttest.tree.model --evaluate
Loading tagged test data...
Loading FastText and Decision Tree models...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Preparing features...
Predicting...
Evaluating...
              precision    recall  f1-score   support

           B       0.51      0.23      0.32      6861
           E       0.71      0.77      0.74      6829
           F       0.54      0.03      0.06     17577
           N       0.59      0.20      0.29     19728
           O       0.70      0.95      0.81     92778

    accuracy                           0.69    143773
   macro avg       0.61      0.44      0.44    143773
weighted avg       0.66      0.69      0.62    143773


real    0m3.732s
user    0m6.201s
sys     0m4.406s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

လက်ရှိအချိန်ထိ experiment အရ BONE pattern model က BFONE ထက် သာတယ်။   
Accuracy က 0.69 vs 0.81.  

## To Do  

တခြား approach တွေနဲ့ experiment ထပ်ဖြည့်လုပ်ရန်။  