# MuHaung Post Editing with Two NMT Models

## Script Preparation for Training Data

Post-Editing အတွက် training data တစ်ခုလုံးကို translation လုပ်ပြီး machine-translation output training data ကို ဖန်တီးမယ်။  

for my-br testing, tran-eval-traindata-mybr.sh:  

```bash
#!/bin/bash

## Preparation for Post-Editing with two NMT Models
## Written by Ye, LST, NECTEC, Thailand
## Translation and Evaluation with TRAINING-DATA, Marian, Transformer Model, for my-br
## 12 April 2022

marian-decoder -m ./model0-mybr.iter95000.npz -v /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml --devices 0 1 --output hyp.iter95000-trainingdata.br < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my
echo "Evaluation with hyp.iter95000-trainingdata.br, Best Transformer Model:" >> test-train0-mybr-results.txt
perl ~/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br < ./hyp.iter95000-trainingdata.br  >> test-train0-mybr-results.txt

```

for br-my testing:  

```bash
#!/bin/bash

## Preparation for Post-Editing with two NMT Models
## Written by Ye, LST, NECTEC, Thailand
## Translation and Evaluation with TRAINING-DATA, Marian, Transformer Model, for br-my
## 12 April 2022

marian-decoder -m ./model0-brmy.iter80000.npz -v /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml --devices 0 1 --output hyp.iter80000-trainingdata.my < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br
echo "Evaluation with hyp.iter80000-trainingdata.my, Best Transformer Model:" >> test-train0-brmy-results.txt
perl ~/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my < ./hyp.iter80000-trainingdata.my  >> test-train0-brmy-results.txt
```

## Translating Myanmar Training Data

Translating the whole training-set:  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer$ time ./tran-eval-traindata-mybr.sh
...
...
...
[2022-04-12 21:02:47] Best translation 16386 : ⠼⠙ ⠲ ⠹⠣⠃⠔ ⠰⠶ ⠣⠎⠥⠂⠣⠺⠱⠆ ⠲
[2022-04-12 21:02:47] Best translation 16387 : ⠏⠋⠆ ⠇⠑⠈⠶ ⠲
[2022-04-12 21:02:47] Best translation 16388 : ⠎⠣⠅⠁⠆⠿⠱ ⠣⠗⠱⠆⠣⠹⠁⠆ ⠩⠱⠂⠈⠶ ⠇⠋⠆⠿⠣⠾ ⠲
[2022-04-12 21:02:47] Best translation 16389 : ⠣⠸⠣⠥⠩⠔ ⠗ ⠗⠺⠁⠹⠥⠗⠺⠁⠹⠁⠆ ⠚ ⠇⠆ ⠁⠆⠗⠣⠏⠁⠆⠗⠣ ⠗⠮⠍⠻⠆ ⠟⠣ ⠃ ⠹⠞ ⠲
[2022-04-12 21:02:48] Best translation 16390 : ⠼⠂ ⠝⠴ ⠰⠣⠣ ⠾⠋⠍⠁ ⠚ ⠈⠑⠨⠋⠯ ⠅⠣⠿⠣ ⠇⠁ ⠨⠮⠂ ⠟⠣ ⠡ ⠿⠓ ⠽⠕⠆⠙⠣⠽⠁⠆ ⠣⠅⠣ ⠹⠏⠔ ⠾⠋⠍⠁ ⠇⠥⠾⠕⠆ ⠚ ⠊ ⠣⠾⠔⠂⠈⠉⠆ ⠹⠻⠆ ⠣⠈⠔⠂⠣⠞⠋⠆ ⠺⠔ ⠣⠝⠥⠂⠏⠔⠷⠁ ⠚ ⠏⠩ ⠹⠻⠆ ⠣⠅⠣ ⠏⠔⠷⠁⠗⠣⠞ ⠓ ⠹⠣⠞⠰⠣⠣⠞ ⠨⠮⠂ ⠟ ⠃ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16391 : ⠍⠋⠞⠣⠇⠱⠆ ⠙⠖⠽⠁⠍⠪⠅⠔⠃⠽⠭ ⠎⠑⠗⠉ ⠹ ⠩⠱⠆ ⠅⠣ ⠱⠝⠩⠱⠂⠅⠕⠞⠻⠟⠪⠆ ⠊ ⠇⠑⠝⠑ ⠗⠉ ⠭ ⠨⠮⠂ ⠊ ⠲
[2022-04-12 21:02:48] Best translation 16392 : ⠇⠱⠂⠟⠔⠂⠨⠋⠆ ⠍⠱⠆⠨⠥⠝⠆⠾ ⠲
[2022-04-12 21:02:48] Best translation 16393 : ⠟⠋⠎⠪ ⠲
[2022-04-12 21:02:48] Best translation 16394 : ⠱⠆⠎⠢⠂ ⠝⠱ ⠹⠻⠆ ⠝⠋⠝⠑ ⠹⠣⠃⠁⠺⠣ ⠗ ⠞⠱⠅⠈⠱⠅ ⠷⠢⠹⠑ ⠡ ⠚ ⠅⠣ ⠨⠣⠗⠪⠆⠁⠺⠑ ⠡ ⠅ ⠣⠗⠣⠹⠁ ⠞⠭⠾⠕⠆ ⠭⠎ ⠏ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16395 : ⠥⠆⠃⠣⠷⠋ ⠅⠁⠆ ⠺⠁⠹⠣⠝⠁ ⠣⠗⠔⠆⠨⠋ ⠵ ⠏⠋⠆⠡⠪ ⠏⠔⠷⠁ ⠞⠺ ⠟⠻⠟⠁⠆ ⠨⠮⠂ ⠹⠥ ⠭ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16396 : ⠞⠣⠍⠁⠏⠔ ⠲
[2022-04-12 21:02:48] Best translation 16397 : ⠟⠴⠹⠔⠏⠉⠆ ⠞⠦⠅⠴ ⠾⠴ ⠌⠁⠆ ⠡⠴ ⠲
[2022-04-12 21:02:48] Best translation 16398 : ⠼ ⠣⠇⠔⠅⠁⠾ ⠹ ⠹⠑⠈⠖⠗⠁ ⠎⠣⠅⠁⠆⠿⠱ ⠅ ⠍⠙ ⠍⠏⠉ ⠣⠁⠴⠣⠅⠥ ⠿⠥⠂ ⠝⠱ ⠟⠶⠆ ⠈⠑⠎⠣⠞ ⠇⠱⠂⠇⠁ ⠞⠣⠞ ⠶ ⠁⠆⠁⠦ ⠹⠔⠂ ⠏ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16399 : ⠅⠉⠆ ⠏⠋ ⠇⠕⠂ ⠡⠁⠆⠡⠁⠆ ⠲
[2022-04-12 21:02:48] Best translation 16400 : ⠇⠱⠂⠟⠔⠂⠨⠋⠆ ⠍⠱⠆⠨⠥⠝⠆⠾ ⠲
[2022-04-12 21:02:48] Best translation 16401 : ⠶ ⠛⠣ ⠶ ⠍⠶⠾⠔⠂ ⠅ ⠣⠃⠮⠳ ⠹⠥⠌⠮⠡⠔⠆⠅⠶⠆ ⠏⠪⠹⠣ ⠹⠓ ⠨⠻⠈⠕ ⠼⠬ ⠹⠝ ⠲
[2022-04-12 21:02:48] Best translation 16402 : ⠛⠣⠲
[2022-04-12 21:02:48] Best translation 16403 : ⠼⠉ ⠲ ⠍⠣⠓⠻⠹⠣⠙⠁ ⠝⠺⠁⠆ ⠞⠽ ⠎⠪ ⠗⠔⠏⠉ ⠿⠣⠵⠣⠞ ⠅ ⠟⠪⠂ ⠿⠪⠆ ⠍⠙ ⠨⠋⠎⠁⠆ ⠗⠣ ⠹⠝ ⠲
[2022-04-12 21:02:48] Best translation 16404 : ⠼⠁ ⠲ ⠴⠏⠁ ⠣⠡⠑⠾ ⠏⠻ ⠍⠥⠞⠮ ⠿⠪⠆ ⠵⠣⠽⠁⠆ ⠞⠺ ⠿⠓⠱⠂ ⠏ ⠲
[2022-04-12 21:02:48] Best translation 16405 : ⠞⠭⠝⠱⠂ ⠞⠺ ⠍⠔⠆⠟⠪⠆ ⠅⠣ ⠣⠍⠶ ⠇⠥⠂⠇⠔ ⠒ ⠪ ⠣⠞⠣⠞⠏⠔⠷⠁ ⠅ ⠣⠃⠮ ⠈⠣⠗⠁⠂ ⠁⠋ ⠞⠺ ⠇⠱⠂⠇⠁ ⠈⠪⠆⠏⠥⠆ ⠨⠮⠂ ⠹⠝ ⠲
[2022-04-12 21:02:48] Best translation 16406 : ⠥⠆⠘⠕⠆⠟⠁⠆ ⠹ ⠙⠥⠂⠞⠊⠽⠣ ⠅⠋⠃⠁⠎⠭ ⠣⠞⠺⠔⠆ ⠎⠭⠿⠱⠆ ⠗⠔⠆ ⠾⠋⠍⠁ ⠠⠣⠭ ⠼⠁ ⠉ ⠚ ⠉ ⠨⠥⠂ ⠶ ⠅⠗ ⠠⠣⠭ ⠼⠁ ⠊ ⠙ ⠃ ⠶ ⠞⠺ ⠁⠋⠆⠞⠣⠏⠔ ⠾⠕⠂ ⠫ ⠅⠺⠮⠇⠥⠝ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16407 : ⠹⠥ ⠺⠁⠹⠣⠝⠁ ⠏⠁ ⠗⠁ ⠒ ⠾⠣⠞⠝⠕⠆ ⠗⠁ ⠏⠋⠆⠡⠪ ⠣⠇⠦ ⠅ ⠇⠦ ⠱ ⠗⠣ ⠸ ⠣⠇⠥⠝ ⠟⠱⠝⠣⠞ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16408 : ⠞⠣⠞⠊⠽⠣ ⠠⠣⠭ ⠟⠣⠞⠻⠂ ⠇⠆ ⠓⠕⠓⠕⠙⠪⠙⠪ ⠈⠕⠯ ⠏⠱⠆ ⠇⠬ ⠗⠣⠞⠁ ⠅⠣ ⠌⠺⠱ ⠡⠴ ⠁⠶ ⠲
[2022-04-12 21:02:48] Best translation 16409 : ⠱⠅⠗⠁ ⠰⠣⠣ ⠁⠣⠯ ⠍⠣⠟⠁⠍⠪ ⠰⠣⠁ ⠏⠔ ⠣⠝⠪⠆⠣⠝⠁⠆ ⠩ ⠃⠉⠆⠟⠪⠆⠟⠶⠆ ⠰⠣⠣ ⠅⠣⠇⠣⠞⠑⠹⠋ ⠅ ⠟⠁⠆ ⠗⠣ ⠃ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16410 : ⠣⠍⠮⠆⠹⠁⠆ ⠌⠁⠆⠾ ⠋ ⠏⠦ ⠋ ⠹⠕⠆ ⠃⠮⠆ ⠞⠁⠩⠱⠨⠋ ⠶ ⠎⠓⠁⠆ ⠿⠓ ⠿⠥⠂⠿⠔ ⠞⠓⠁⠆ ⠝ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16411 : ⠏⠁⠝⠪ ⠇⠆ ⠇⠁ ⠞⠮ ⠩ ⠞⠮ ⠲
[2022-04-12 21:02:48] Best translation 16412 : ⠼⠃ ⠲ ⠈⠑⠎⠣⠞ ⠰⠶ ⠞⠭ ⠨⠥⠂ ⠗ ⠞⠭ ⠨⠥⠂ ⠏⠥⠆⠏⠶⠆ ⠹ ⠲ ⠈⠑⠝⠺⠮ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16413 : ⠚⠔ ⠏⠮⠂ ⠡⠔⠆ ⠏⠴ ⠟⠣⠎⠕⠂ ⠲
[2022-04-12 21:02:48] Best translation 16414 : ⠶ ⠗⠥⠞⠈⠕⠗⠋ ⠶ ⠲
[2022-04-12 21:02:48] Total time: 451.43179s wall

real	7m36.136s
user	14m46.195s
sys	0m16.659s
```

Evaluation Result:  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer$ cat ./test-train0-mybr-results.txt 
Evaluation with hyp.iter95000-trainingdata.br, Best Transformer Model:
BLEU = 99.98, 100.0/100.0/100.0/100.0 (BP=1.000, ratio=1.000, hyp_len=220154, ref_len=220157)
```

## Translating Braille Training Data 

Translating the whole training-set:  


```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-brmy$ time ./tran-eval-traindata-brmy.sh
...
...
...
[2022-04-12 23:24:05] Best translation 16385 : ( င ) ပြေး ပွဲ ပြိုင်ပွဲ ( ကဗျာ ) ။
[2022-04-12 23:24:05] Best translation 16386 : ၄ ။ သဘင် = အစုအဝေး ။
[2022-04-12 23:24:05] Best translation 16387 : ပန်း လက်ဆောင် ။
[2022-04-12 23:24:05] Best translation 16388 : စကားပြေ အရေးအသား ရှေ့ဆောင် လမ်းပြများ ။
[2022-04-12 23:24:05] Best translation 16389 : အလှူရှင် နှင့် ရွာသူရွာသား တို့ လည်း အားရပါးရ ရယ်မော ကြ လေ သတည်း ။
[2022-04-12 23:24:05] Best translation 16390 : ထို့ နောက် မှ မြန်မာ တို့ ဆက်ခံ၍ ကပြ လာ ခဲ့ ကြ ခြင်း ဖြင့် ယိုးဒယား အက သည်ပင် မြန်မာ လူမျိုး တို့ ၏ အမြင့်ဆုံး သော အဆင့်အတန်း ဝင် အနုပညာ တို့ ပါရှိ သော အက ပညာရပ် ဟု သတ်မှတ် ခဲ့ ကြ လေ သည် ။
[2022-04-12 23:24:05] Best translation 16391 : မန္တလေး ဒိုင်ယာမီကင်ဗျစ် စက်ရုံ သည် ရှေး က အိမ်ရှေ့ကိုယ်တော်ကြီး ၏ လက်နက် ရုံ ဖြစ် ခဲ့ ၏ ။
[2022-04-12 23:24:05] Best translation 16392 : လေ့ကျင့်ခန်း မေးခွန်းများ ။
[2022-04-12 23:24:05] Best translation 16393 : ကြံစည် ။
[2022-04-12 23:24:05] Best translation 16394 : အေးစိမ့် နေ သော နံနက် သဘာဝ နှင့် တိတ်ဆိတ် ငြိမ်သက် ခြင်း တို့ က ခရီးထွက် ခြင်း ကို အရသာ တစ်မျိုး ဖြစ်စေ ပါ သည် ။
[2022-04-12 23:24:05] Best translation 16395 : ဦးဘဉာဏ် ကား ဝါသနာ အရင်းခံ သောကြောင့် ပန်းချီ ပညာ တွင် ကျော်ကြား ခဲ့ သူ ဖြစ် သည် ။
[2022-04-12 23:24:05] Best translation 16396 : တမာပင် ။
[2022-04-12 23:24:05] Best translation 16397 : ကျောက်သင်ပုန်း တုတ်ကောက် မျောက် ငါး ခြောက် ။
[2022-04-12 23:24:05] Best translation 16398 : ထို အလင်္ကာများ သည် သက်ဆိုင်ရာ စကားပြေ ကို မည်သို့ မည်ပုံ အထောက်အကူ ပြု နေ ကြောင်း ဆက်စပ် လေ့လာ တတ် အောင် အားထုတ် သင့် ပါ သည် ။
[2022-04-12 23:24:05] Best translation 16399 : ကုံး ပန် လို့ ခြားခြား ။
[2022-04-12 23:24:05] Best translation 16400 : လေ့ကျင့်ခန်း မေးခွန်းများ ။
[2022-04-12 23:24:05] Best translation 16401 : ( ဂ ) မောင်မြင့် ကို အဘယ်ကြောင့် သူငယ်ချင်းကောင်း ပီသ သည်ဟု ခေါ်ဆို ထိုက် သနည်း ။
[2022-04-12 23:24:05] Best translation 16402 : ဂ။
[2022-04-12 23:24:05] Best translation 16403 : ၃ ။ မဟော်သဓာ နွား တရား စီ ရင်ပုံ ပြဇာတ် ကို ကြည့် ပြီး မည်သို့ ခံစား ရ သနည်း ။
[2022-04-12 23:24:05] Best translation 16404 : ၁ ။ အောက်ပါ အချက်များ ပေါ် မူတည် ပြီး ဇယား တွင် ဖြည့် ပါ ။
[2022-04-12 23:24:05] Best translation 16405 : တစ်နေ့ တွင် မင်းကြီး က အမောင် လုလင် ၊ ဤ အတတ်ပညာ ကို အဘယ် ဆရာ့ ထံ တွင် လေ့လာ ဆည်းပူး ခဲ့ သနည်း ။
[2022-04-12 23:24:05] Best translation 16406 : ဦးဖိုးကျား သည် ဒုတိယ ကမ္ဘာစစ် အတွင်း စစ်ပြေး ရင်း မြန်မာ နှစ် ၁ ၃ ၀ ၃ ခု ( ခရစ် နှစ် ၁ ၉ ၄ ၂ ) တွင် ထန်းတပင် မြို့ ၌ ကွယ်လွန် သည် ။
[2022-04-12 23:24:05] Best translation 16407 : သူ ဝါသနာ ပါ ရာ ၊ မြတ်နိုး ရာ ပန်းချီ အလုပ် ကို လုပ် နေ ရ လျှင် အလွန် ကျေနပ် သည် ။
[2022-04-12 23:24:05] Best translation 16408 : တတိယ နှစ် ကျတော့ လည်း ဟိုဟိုဒီဒီ ဆို၍ ပေး လိုက် ရတာ က ငွေ ခြောက် ထောင် ။
[2022-04-12 23:24:06] Best translation 16409 : အိပ်ရာ မှ ထ၍ မကြာမီ မှာ ပင် အနီးအနား ရှိ ဘုန်းကြီးကျောင်း မှ ကလတက်သံ ကို ကြား ရ လေ သည် ။
[2022-04-12 23:24:06] Best translation 16410 : အမဲသား ငါးများ မ ပုပ် မ သိုး ဘဲ တာရှည်ခံ အောင် ဆား ဖြင့် ပြုပြင် ထား နိုင် သည် ။
[2022-04-12 23:24:06] Best translation 16411 : ပါနီ လည်း လာ တယ် ရှိ တယ် ။
[2022-04-12 23:24:06] Best translation 16412 : ၂ ။ ဆက်စပ် = တစ် ခု နှင့် တစ် ခု ပူးပေါင်း သည် ။ ဆက်နွယ် သည် ။
[2022-04-12 23:24:06] Best translation 16413 : ဂျင် ပဲ့ ချင်း ပေါက် ကြစို့ ။
[2022-04-12 23:24:06] Best translation 16414 : ( ရွတ်ဆိုရန် ) ။
[2022-04-12 23:24:06] Total time: 458.91151s wall

real	7m43.005s
user	15m0.544s
sys	0m16.851s
 
```

Evaluation Result:  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-brmy$ cat ./test-train0-brmy-results.txt 
Evaluation with hyp.iter80000-trainingdata.my, Best Transformer Model:
BLEU = 99.97, 100.0/100.0/100.0/100.0 (BP=1.000, ratio=1.000, hyp_len=220146, ref_len=220157)
```

## Translating Myanmar Development Data

Development data ကိုလည်း ဘာသာပြန်ဖို့ လိုအပ်လို့၊ command ကို အောက်ပါအတိုင်းပေးခဲ့...  

```bash
time marian-decoder -m ./model0-mybr.iter95000.npz \
-v /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
/media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
--devices 0 1 \
--output hyp.iter95000-devdata.br < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.my
```

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer$ time marian-decoder -m ./model0-mybr.iter95000.npz -v /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml --devices 0 1 --output hyp.iter95000-devdata.br < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.my
...
...
...
[2022-04-13 00:18:26] Best translation 2871 : ⠣⠿⠓⠱⠾ ⠅ ⠇⠱⠂⠟⠔⠂⠨⠋⠆ ⠎⠁⠕⠅ ⠞⠺ ⠗⠱⠆⠰⠣⠣⠞ ⠏ ⠲
[2022-04-13 00:18:26] Best translation 2872 : ⠼⠂⠝⠴ ⠅⠕⠇⠕⠝⠪ ⠨⠭ ⠅⠣ ⠣⠁⠔⠩⠁⠆ ⠈⠉⠆ ⠗ ⠨⠭ ⠩⠊⠹ ⠈⠉⠆ ⠭ ⠹⠂ ⠙⠣⠛⠉ ⠍⠣⠞⠛⠣⠵⠔⠆ ⠫ ⠮⠙⠪⠞⠁⠡⠦ ⠇⠦ ⠹ ⠲
[2022-04-13 00:18:26] Best translation 2873 : ⠹⠔⠨⠋⠆⠎⠁ ⠣⠟⠔⠆ ⠲
[2022-04-13 00:18:26] Best translation 2874 : ⠈⠪ ⠌⠺⠱⠂ ⠒ ⠎⠓⠁⠆ ⠌⠺⠱⠂ ⠑⠈⠭ ⠌⠺⠱⠂ ⠎⠣⠹⠂ ⠞⠬⠎⠁⠆ ⠟⠉⠂⠽⠉ ⠎ ⠹⠻⠆ ⠣⠌⠺⠱⠂⠾ ⠏⠁ ⠹⠂ ⠷⠭⠷⠋⠆ ⠹⠻⠆ ⠇⠱⠁⠥⠂ ⠳ ⠇⠆ ⠣⠈⠴⠣⠕⠝ ⠏⠭⠎⠪⠆⠏⠭⠎⠣⠽⠣⠾ ⠶⠝⠣⠖ ⠿⠕⠿⠑ ⠇⠁ ⠟ ⠹ ⠲
[2022-04-13 00:18:26] Best translation 2875 : ⠼⠣⠨⠁ ⠟⠥⠚ ⠗ ⠏⠁⠇⠁ ⠹⠻⠆ ⠗⠣⠞⠨⠋ ⠇⠥⠟⠪⠆ ⠞⠭ ⠥⠆ ⠅⠣ ⠟⠥⠚ ⠅ ⠈⠺⠮⠆⠨⠻ ⠎⠣⠅⠁⠆⠘⠁ ⠹⠂ ⠣⠝⠱ ⠗ ⠣⠰⠣⠣⠞⠞⠓⠁⠆ ⠒ ⠥⠆ ⠈⠪ ⠅⠣ ⠙⠪ ⠞⠭ ⠗⠁ ⠇⠴ ⠰⠣⠋⠆⠞⠓⠁⠆ ⠇⠕⠂ ⠿⠓ ⠟⠞⠚ ⠋ ⠇⠁ ⠨⠮⠂ ⠏ ⠃⠥⠆ ⠲
[2022-04-13 00:18:26] Best translation 2876 : ⠼⠉ ⠲ ⠵⠋⠃⠥ ⠎⠕⠆⠗⠣ ⠰⠶ ⠵⠋⠃⠥⠙⠱⠅⠟⠥⠝⠆ ⠅ ⠣⠎⠕⠆⠗⠣ ⠹⠥ ⠲
[2022-04-13 00:18:26] Best translation 2877 : ⠪ ⠍⠺⠱ ⠅⠁⠆ ⠥⠆⠨⠶⠆ ⠇⠆ ⠌⠮ ⠊ ⠣⠾⠪⠆ ⠇⠆ ⠹⠺⠮ ⠊ ⠲
[2022-04-13 00:18:26] Best translation 2878 : ⠔⠛⠣⠏⠭⠎⠔ ⠲
[2022-04-13 00:18:26] Best translation 2879 : ⠎⠓⠁⠆ ⠹ ⠨⠋⠙⠁⠅⠕ ⠣⠞⠺⠑ ⠣⠹⠉⠆⠺⠔ ⠗⠉ ⠹⠁⠍⠣⠅⠣ ⠣⠹⠁⠆ ⠌⠁⠆⠾ ⠝⠌⠡⠁⠆ ⠃⠮⠆ ⠟⠁⠩⠱ ⠟⠁⠩⠱ ⠨⠋ ⠶ ⠣⠟⠕⠆⠣⠟⠶⠆ ⠌⠁⠆⠏⠊ ⠒ ⠌⠁⠆⠡⠴ ⠒ ⠣⠹⠁⠆ ⠡⠴ ⠎⠣⠹ ⠚ ⠿⠥⠂⠇⠦ ⠗⠁ ⠞⠺ ⠇⠆ ⠣⠹⠉⠆⠺⠔ ⠹ ⠲
[2022-04-13 00:18:26] Best translation 2880 : ⠼⠁ ⠓ ⠗⠁⠎⠥⠂ ⠝⠢⠂⠯ ⠍⠶⠆⠋ ⠲
[2022-04-13 00:18:26] Best translation 2881 : ⠶ ⠼⠙ ⠶ ⠞⠭ ⠏⠔ ⠲
[2022-04-13 00:18:26] Best translation 2882 : ⠶ ⠓⠱⠂ ⠎⠢ ⠇⠁⠆ ⠒ ⠓⠱⠂ ⠾⠣ ⠇⠁⠆ ⠶ ⠓⠱⠆ ⠇⠁⠆ ⠍⠶⠍⠮ ⠗⠕⠂ ⠺⠁⠆ ⠲
[2022-04-13 00:18:26] Best translation 2883 : ⠣⠾⠕⠆⠹⠁⠆ ⠿⠣⠞⠬ ⠞⠺ ⠣⠁⠣⠞ ⠌⠁⠆ ⠁⠣⠞ ⠩ ⠹ ⠲
[2022-04-13 00:18:26] Best translation 2884 : ⠗⠕⠆⠗⠕⠆ ⠿⠻⠆⠎⠣⠅⠁⠆ ⠅ ⠨⠭ ⠣⠹⠪⠆⠹⠪⠆ ⠅⠣ ⠝⠁⠆⠇⠮ ⠝ ⠏ ⠹ ⠲
[2022-04-13 00:18:26] Best translation 2885 : ⠼⠊ ⠲ ⠎⠁ ⠗⠥⠞ ⠰⠶ ⠎⠁ ⠅ ⠣⠹⠋ ⠁⠺⠑⠯ ⠈⠕ ⠹ ⠲
[2022-04-13 00:18:26] Best translation 2886 : ⠗⠱ ⠨⠕⠂ ⠗⠱⠆ ⠲
[2022-04-13 00:18:26] Best translation 2887 : ⠼⠃ ⠲ ⠎⠣⠇⠺⠮⠹⠖⠆ ⠰⠶ ⠟⠕⠆ ⠎⠣⠹ ⠅ ⠏⠣⠨⠉⠆ ⠞⠺ ⠎⠣⠇⠺⠮ ⠹⠣⠘⠺⠮ ⠞⠣⠞⠈⠔ ⠹ ⠲
[2022-04-13 00:18:26] Best translation 2888 : ⠇⠱⠂⠟⠔⠂⠨⠋⠆ ⠲
[2022-04-13 00:18:26] Best translation 2889 : ⠼⠉ ⠲ ⠅⠕⠆⠎⠁⠆ ⠰⠶ ⠣⠁⠥⠆ ⠁⠆⠅⠕⠆ ⠹ ⠲
[2022-04-13 00:18:27] Best translation 2890 : ⠇⠮ ⠩⠔ ⠽⠴⠟⠁⠆ ⠇⠆ ⠞⠭⠷⠔⠂ ⠠⠣⠭⠹⠑ ⠟⠪⠷⠕ ⠑ ⠟⠱⠆ ⠍⠔⠆ ⠁⠆ ⠣⠇⠕⠩ ⠞⠖⠆ ⠹⠉⠆⠈⠶ ⠇⠱ ⠮ ⠓ ⠞⠭⠍⠪ ⠓⠾⠣ ⠹⠻⠆ ⠇⠮ ⠅ ⠏⠱⠆⠸⠣⠥ ⠏⠥⠵⠻ ⠃ ⠹⠞ ⠲
[2022-04-13 00:18:27] Best translation 2891 : ⠾⠋⠍⠁ ⠝⠌ ⠞⠺ ⠞⠊⠗⠭⠈⠋ ⠥⠂⠽⠔ ⠹⠉⠆ ⠨⠥⠂ ⠩ ⠹ ⠲
[2022-04-13 00:18:27] Best translation 2892 : ⠣⠞⠖ ⠾⠑⠰⠣⠋ ⠝⠑ ⠝⠮⠂ ⠃⠶⠆⠃⠪ ⠞⠕ ⠲
[2022-04-13 00:18:27] Best translation 2893 : ⠨⠺⠱⠆ ⠓⠭ ⠇⠥ ⠓⠭ ⠒ ⠣⠹⠋⠿⠁ ⠅⠮ ⠡⠴ ⠹⠻⠆⠣⠨⠁ ⠲
[2022-04-13 00:18:27] Best translation 2894 : ⠁⠊ ⠁⠪ ⠁⠪⠆ ⠲
[2022-04-13 00:18:27] Best translation 2895 : ⠞⠋ ⠏⠁ ⠅⠺⠮ ⠚ ⠌⠣ ⠓⠁ ⠌ ⠅⠥⠞ ⠏⠁⠂ ⠍⠮ ⠲
[2022-04-13 00:18:27] Best translation 2896 : ⠣⠰⠣⠁⠞ ⠏⠁⠆ ⠇⠬ ⠩⠁ ⠞⠮ ⠇⠱⠆ ⠲
[2022-04-13 00:18:27] Total time: 80.81048s wall

real	1m21.546s
user	2m33.697s
sys	0m3.292s
```

## Translating Braille Development Data

```bash
marian-decoder -m ./model0-brmy.iter80000.npz \
-v /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
/media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
--devices 0 1 \
--output hyp.iter80000-devdata.my < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.br
```

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-brmy$ marian-decoder -m ./model0-brmy.iter80000.npz -v /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml --devices 0 1 --output hyp.iter80000-devdata.my < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.br
...
...
...
[2022-04-13 00:24:05] Best translation 2868 : လျှော လျှော့ လျှော် ။
[2022-04-13 00:24:05] Best translation 2869 : နှင်း ကို မြင် ခိုက် ။
[2022-04-13 00:24:05] Best translation 2870 : လယ်ထွန် သွား နွား မေ့ ။
[2022-04-13 00:24:05] Best translation 2871 : အဖြေများ ကို လေ့ကျင့်ခန်း စာအုပ် တွင် ရေးမှတ် ပါ ။
[2022-04-13 00:24:05] Best translation 2872 : ထို့နောက် ကိုလိုနီ ခေတ် က အထင်ရှား ဆုံး နှင့် ခေတ် တူတော် ဆုံး ဖြစ် သည့် ဒဂုန် မဂ္ဂဇင်း ၌ အယ်ဒီတာချုပ် လုပ် သည် ။
[2022-04-13 00:24:05] Best translation 2873 : သင်ခန်းစာ အကျဉ်း ။
[2022-04-13 00:24:05] Best translation 2874 : ဆီ ငွေ့ ၊ ဆား ငွေ့ အက်ဆစ် ငွေ့ စသည့် တိုက်စား ဆွေးမြည့် စေ သော အငွေ့များ ပါ သည့် ညစ်ညမ်း သော လေထု ကြောင့် လည်း အဆောက်အအုံ ပစ္စည်းပစ္စယများ ဆွေးမြည့် ပြိုပျက် လာ ကြ သည် ။
[2022-04-13 00:24:05] Best translation 2875 : ထိုအခါ ကျွန်ုပ်တို့ နှင့် ပါလာ သော ရပ်ခံ လူကြီး တစ် ဦး က ကျွန်ုပ်တို့ ကို ပြုတ်ကျ စကားဖာ သည့် အနေ နှင့် စည်းသား ၊ ဦး ဆီ က ဒီ တစ် ရာ လောက် မှန်းထား လို့ ဖြင့် ကျွန်တော်တို့ မ လာ ခဲ့ ပါ ဘူး ။
[2022-04-13 00:24:05] Best translation 2876 : ၃ ။ ဇမ္ဗူ စိုးရ = ဇမ္ဗူဒိပ်ကျွန်း ကို အစိုးရ သူ ။
[2022-04-13 00:24:05] Best translation 2877 : ဤ မြွေ ကား ဦးခေါင်း လည်း ငယ် ၏ အမြီး လည်း သွယ် ၏ ။
[2022-04-13 00:24:05] Best translation 2878 : အင်္ဂပစ္စင် ။
[2022-04-13 00:24:05] Best translation 2879 : ဆား သည် ခန္ဓာကိုယ် အတွက် အသုံးဝင် ရုံ သာမက အသား ငါးများ နုပ် ဘဲ ကြာရှည် ခံ အောင် ဖြေဖျော် လှန်း၍ ငါးပိ ၊ ငါးခြောက် ၊ အသား ခြောက် စသည် တို့ ပြုလုပ် ရာ တွင် လည်း အသုံးဝင် သည် ။
[2022-04-13 00:24:05] Best translation 2880 : ၁ ၈ ရာစု ချောင်းဦး စွန့်စား၍ ။
[2022-04-13 00:24:05] Best translation 2881 : ( ၄ ) တစ် ပင် ။
[2022-04-13 00:24:05] Best translation 2882 : ( ဟေ့ စိန် လား ၊ ဟေ့ မြ လား ) ဟေး လား မောင်မယ် ရို့ ဝါး ။
[2022-04-13 00:24:05] Best translation 2883 : အမျိုးသား ပြတိုက် တွင် အထပ် ငါး ထပ် ရှိ သည် ။
[2022-04-13 00:24:05] Best translation 2884 : ရိုးရိုး ပြောစကား ကို ခေတ် အသီးသီး က နားလည် နိုင် ပါ သည် ။
[2022-04-13 00:24:05] Best translation 2885 : ၉ ။ စာ ရွတ် = စာ ကို အသံ ထွက်၍ ဆို သည် ။
[2022-04-13 00:24:05] Best translation 2886 : ရေ တူတဲ့ ရေး ။
[2022-04-13 00:24:05] Best translation 2887 : ၂ ။ စလွယ်သိုင်း = ကြိုး စသည် ကို ပခုံး တွင် စလွယ် သဖွယ် တပ်ဆင် သည် ။
[2022-04-13 00:24:05] Best translation 2888 : လေ့ကျင့်ခန်း ။
[2022-04-13 00:24:05] Best translation 2889 : ၃ ။ ကိုးစား = အထူး အားကိုး သည် ။
[2022-04-13 00:24:05] Best translation 2890 : လယ် ရှင် ယောက်ျား လည်း ဒေါင်းပေါင် နှစ်သက် ကြည်ညို လျက် ကျေး မင်း အား အလိုရှိ တိုင်း သုံးဆောင် လေ လော့ ဟု အမှတ်ထား မျှ သော လယ် ကို ပေးလှူ ပူဇော် လေ သတည်း ။
[2022-04-13 00:24:05] Best translation 2891 : မြန်မာ နိုင်ငံ တွင် တိရစ္ဆာန် ဥယျာဉ် သုံး ခု ရှိ သည် ။
[2022-04-13 00:24:05] Best translation 2892 : အတိုင် မျက်မှန် နက် နဲ့ ဘောင်းဘီ တို ။
[2022-04-13 00:24:05] Best translation 2893 : ခွေး ဟစ် လူ ဟစ် ၊ ကျည်းသား ကယ် ခြောက် သောအခါ ။
[2022-04-13 00:24:06] Best translation 2894 : ထိ ထီ ထီး ။
[2022-04-13 00:24:06] Best translation 2895 : တန် ပါ ကွယ် တို့ ငါ့ ဟာ ငါ ကွပ် ပါ့ မယ် ။
[2022-04-13 00:24:06] Best translation 2896 : အမှာတော် ပါး လိုက် ရှာ တယ် လေး ။
[2022-04-13 00:24:06] Total time: 83.95003s wall

```

## Training MT_Braille-to-Ref_Braille

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, LST, NECTEC, Thailand
## Experiments for Transformer MT_Braille-to-Ref_Braille
## 13 April 2022

mkdir model.transformer-mt-br;

marian \
    --model  /media/ye/project2/exp/braille-nmt/model.transformer-mt-br/model0-mtbr.npz --type transformer \
    --train-sets /media/ye/project2/exp/braille-nmt/model.transformer/hyp.iter95000-trainingdata.br /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br \
    --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets /media/ye/project2/exp/braille-nmt/model.transformer/hyp.iter95000-devdata.br /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.br \
    --valid-translation-output /media/ye/project2/exp/braille-nmt/model.transformer-mt-br/dev.mt-br.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log ./model.transformer-mt-br/train-mtbr.log --valid-log ./model.transformer-mt-br/valid-mtbr.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 1 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > /media/ye/project2/exp/braille-nmt/model.transformer-mt-br/config-mtbr0.yml
    
time marian -c /media/ye/project2/exp/braille-nmt/model.transformer-mt-br/config-mtbr0.yml  2>&1 | tee transformer-mtbr0.log

```

```
(base) ye@:/media/ye/project2/exp/braille-nmt$ ./mt-ref-transformer-br.sh 
...
...
...
[2022-04-13 06:47:44] [data] Shuffling data
[2022-04-13 06:47:44] [data] Done reading 16,415 sentences
[2022-04-13 06:47:44] [data] Done shuffling 16,415 sentences to temp files
[2022-04-13 06:48:13] Seen 16415 samples
[2022-04-13 06:48:13] Starting data epoch 739 in logical epoch 739
[2022-04-13 06:48:13] [data] Shuffling data
[2022-04-13 06:48:13] [data] Done reading 16,415 sentences
[2022-04-13 06:48:14] [data] Done shuffling 16,415 sentences to temp files
[2022-04-13 06:48:43] Seen 16415 samples
[2022-04-13 06:48:43] Starting data epoch 740 in logical epoch 740
[2022-04-13 06:48:43] [data] Shuffling data
[2022-04-13 06:48:43] [data] Done reading 16,415 sentences
[2022-04-13 06:48:43] [data] Done shuffling 16,415 sentences to temp files
[2022-04-13 06:49:12] Seen 16415 samples
[2022-04-13 06:49:12] Starting data epoch 741 in logical epoch 741
[2022-04-13 06:49:12] [data] Shuffling data
[2022-04-13 06:49:12] [data] Done reading 16,415 sentences
[2022-04-13 06:49:12] [data] Done shuffling 16,415 sentences to temp files
[2022-04-13 06:49:42] Seen 16415 samples
[2022-04-13 06:49:42] Starting data epoch 742 in logical epoch 742
[2022-04-13 06:49:42] [data] Shuffling data
[2022-04-13 06:49:42] [data] Done reading 16,415 sentences
[2022-04-13 06:49:42] [data] Done shuffling 16,415 sentences to temp files
[2022-04-13 06:50:12] Seen 16415 samples
[2022-04-13 06:50:12] Starting data epoch 743 in logical epoch 743
[2022-04-13 06:50:12] [data] Shuffling data
[2022-04-13 06:50:12] [data] Done reading 16,415 sentences
[2022-04-13 06:50:12] [data] Done shuffling 16,415 sentences to temp files
[2022-04-13 06:50:14] Ep. 743 : Up. 54500 : Sen. 2,024 : Cost 1.32428324 * 1,606,964 @ 2,405 after 175,555,492 : Time 200.61s : 8010.57 words/s : L.r. 1.6255e-04
[2022-04-13 06:50:41] Seen 16415 samples
[2022-04-13 06:50:41] Starting data epoch 744 in logical epoch 744
[2022-04-13 06:50:41] [data] Shuffling data
[2022-04-13 06:50:41] [data] Done reading 16,415 sentences
[2022-04-13 06:50:41] [data] Done shuffling 16,415 sentences to temp files
[2022-04-13 06:51:11] Seen 16415 samples
[2022-04-13 06:51:11] Starting data epoch 745 in logical epoch 745
[2022-04-13 06:51:11] [data] Shuffling data
[2022-04-13 06:51:11] [data] Done reading 16,415 sentences
[2022-04-13 06:51:11] [data] Done shuffling 16,415 sentences to temp files
[2022-04-13 06:51:40] Seen 16415 samples
[2022-04-13 06:51:40] Starting data epoch 746 in logical epoch 746
[2022-04-13 06:51:40] [data] Shuffling data
[2022-04-13 06:51:40] [data] Done reading 16,415 sentences
[2022-04-13 06:51:40] [data] Done shuffling 16,415 sentences to temp files
[2022-04-13 06:52:10] Seen 16415 samples
[2022-04-13 06:52:10] Starting data epoch 747 in logical epoch 747
[2022-04-13 06:52:10] [data] Shuffling data
[2022-04-13 06:52:10] [data] Done reading 16,415 sentences
[2022-04-13 06:52:10] [data] Done shuffling 16,415 sentences to temp files
[2022-04-13 06:52:40] Seen 16415 samples
[2022-04-13 06:52:40] Starting data epoch 748 in logical epoch 748
[2022-04-13 06:52:40] [data] Shuffling data
[2022-04-13 06:52:40] [data] Done reading 16,415 sentences
[2022-04-13 06:52:40] [data] Done shuffling 16,415 sentences to temp files
[2022-04-13 06:53:09] Seen 16415 samples
[2022-04-13 06:53:09] Starting data epoch 749 in logical epoch 749
[2022-04-13 06:53:09] [data] Shuffling data
[2022-04-13 06:53:09] [data] Done reading 16,415 sentences
[2022-04-13 06:53:09] [data] Done shuffling 16,415 sentences to temp files
[2022-04-13 06:53:35] Ep. 749 : Up. 55000 : Sen. 14,753 : Cost 1.32442284 * 1,612,240 @ 3,162 after 177,167,732 : Time 201.25s : 8011.13 words/s : L.r. 1.6181e-04
[2022-04-13 06:53:35] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-mt-br/model0-mtbr.npz.orig.npz
[2022-04-13 06:53:36] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-mt-br/model0-mtbr.iter55000.npz
[2022-04-13 06:53:36] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-mt-br/model0-mtbr.npz
[2022-04-13 06:53:37] Saving Adam parameters to /media/ye/project2/exp/braille-nmt/model.transformer-mt-br/model0-mtbr.npz.optimizer.npz
[2022-04-13 06:53:44] [valid] Ep. 749 : Up. 55000 : cross-entropy : 13.3764 : stalled 10 times (last best: 12.9159)
[2022-04-13 06:53:46] [valid] Ep. 749 : Up. 55000 : perplexity : 2.51369 : stalled 10 times (last best: 2.43518)
[2022-04-13 06:54:00] [valid] Ep. 749 : Up. 55000 : bleu : 86.2131 : stalled 1 times (last best: 86.2406)
[2022-04-13 06:54:00] Training finished
[2022-04-13 06:54:01] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-mt-br/model0-mtbr.npz.orig.npz
[2022-04-13 06:54:01] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-mt-br/model0-mtbr.npz
[2022-04-13 06:54:02] Saving Adam parameters to /media/ye/project2/exp/braille-nmt/model.transformer-mt-br/model0-mtbr.npz.optimizer.npz

real	374m57.086s
user	622m5.019s
sys	0m39.203s

```

output ဖိုလ်ဒါကို ဝင်စစ်ကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-mt-br$ ls
config-mtbr0.yml           model0-mtbr.iter25000.npz  model0-mtbr.iter50000.npz    model0-mtbr.npz.optimizer.npz         train-mtbr.log
dev.mt-br.output           model0-mtbr.iter30000.npz  model0-mtbr.iter5000.npz     model0-mtbr.npz.orig.npz              valid-mtbr.log
model0-mtbr.iter10000.npz  model0-mtbr.iter35000.npz  model0-mtbr.iter55000.npz    model0-mtbr.npz.orig.npz.decoder.yml
model0-mtbr.iter15000.npz  model0-mtbr.iter40000.npz  model0-mtbr.npz              model0-mtbr.npz.progress.yml
model0-mtbr.iter20000.npz  model0-mtbr.iter45000.npz  model0-mtbr.npz.decoder.yml  model0-mtbr.npz.yml
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-mt-br$
```

testing bash for PE model:  

```bash
#!/bin/bash

## Preparation for Myanmar-MuHaung PE
## Written by Ye, LST, NECTEC, Thailand
## Translation and Evaluation with Marian, Transformer PE Model
## 13 April 2022

model0-mtbr.iter5000.npz

#for i in {5000,10000,15000,20000,25000,30000,35000,40000,45000,50000,55000,60000,65000,70000,75000,80000,85000,90000,95000,100000}
for i in {5000,10000,15000,20000,25000,30000,35000,40000,45000,50000,55000}
do
   marian-decoder -m ./model0-mtbr.iter$i.npz -v /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml --devices 0 1 --output hyp.iter$i.br < ../model.transformer/hyp.iter95000.br
   echo "Evaluation on ./model0-mtbr.iter${i}.npz with ../model.transformer/hyp.iter95000.br, Transformer PE Model:" >> test0-PE-results.txt
   perl ~/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br < ./hyp.iter$i.br  >> test0-PE-results.txt
done
```

testing or translation with PE model:  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-mt-br$ time ./tran-eval-pe.sh
...
...
...
[2022-04-13 07:47:22] Best translation 2141 : ⠇⠱⠅⠿⠁ ⠞⠺ ⠇⠆ ⠣⠡⠁⠆ ⠹⠻⠆ ⠓⠌⠑⠾ ⠅⠹ ⠥⠆⠨⠶⠆ ⠏⠖⠆ ⠒ ⠗⠔ ⠏⠖⠆ ⠒ ⠺⠋⠆⠃⠬ ⠏⠖⠆ ⠓⠥⠯ ⠩ ⠹ ⠲
[2022-04-13 07:47:22] Best translation 2142 : ⠅⠁⠞⠥⠝⠆ ⠈⠣⠗⠁⠟⠪⠆ ⠥⠆⠃⠣⠚⠋⠆ ⠲
[2022-04-13 07:47:22] Best translation 2143 : ⠵⠣⠾⠔⠆⠈⠺⠮⠆ ⠲
[2022-04-13 07:47:22] Best translation 2144 : ⠹⠺⠱⠆⠞⠥⠍⠺⠱⠆⠞⠥ ⠝⠺⠁⠆⠾ ⠅ ⠡⠥⠾ ⠒ ⠣⠈⠔⠞⠋⠎⠓⠁⠾ ⠈⠔ ⠿⠪⠆⠸ ⠸⠣⠮⠆⠽⠔ ⠞⠺ ⠏⠋⠆⠈⠕⠆⠞⠋⠆ ⠍⠶⠆ ⠇⠱⠂ ⠩ ⠹ ⠲
[2022-04-13 07:47:22] Best translation 2145 : ⠩⠔ ⠒ ⠨⠔⠃⠽⠁ ⠓ ⠁⠥⠆ ⠰⠣ ⠽⠔⠟⠱⠆⠹ ⠲
[2022-04-13 07:47:22] Best translation 2146 : ⠼⠊ ⠉ ⠙ ⠨⠥⠂ ⠞⠺ ⠏⠻⠏⠴ ⠨⠮⠂ ⠹⠻⠆ ⠎⠡⠓⠌⠁ ⠇⠑⠝⠁⠆ ⠹ ⠣⠗⠱⠆ ⠞⠺ ⠅⠁⠆ ⠍⠔⠆⠞⠽⠟⠪⠆ ⠅⠣ ⠃⠣⠷⠁⠆⠙⠣⠇⠣ ⠣⠏⠻ ⠣⠾⠑ ⠞ ⠩⠯ ⠣⠇⠶⠆⠞ ⠓⠥⠹⠻⠆ ⠽⠕⠆⠙⠣⠽⠁⠆ ⠟⠱⠆⠗⠺⠁ ⠞⠺ ⠟⠥⠝ ⠌⠁⠆ ⠽⠴ ⠗ ⠞⠓⠁⠆ ⠞ ⠍⠥ ⠹ ⠲
[2022-04-13 07:47:22] Best translation 2147 : ⠼⠁ ⠚ ⠲ ⠺⠁⠹⠣⠝⠁ ⠰⠶ ⠎⠺⠮⠆⠾⠮⠆ ⠝⠱ ⠹⠻⠆ ⠣⠇⠱⠂⠣⠟⠔⠂ ⠲
[2022-04-13 07:47:22] Best translation 2148 : ⠍⠶⠘⠕⠆⠎⠢ ⠹ ⠵⠣⠞⠹⠣⠃⠔⠏⠔⠷⠁ ⠅ ⠣⠡⠱⠨⠋ ⠰⠣⠣ ⠎⠣⠯ ⠹⠔⠽⠥ ⠇⠱⠂⠇⠁ ⠨⠮⠂ ⠹ ⠲
[2022-04-13 07:47:22] Best translation 2149 : ⠗⠣⠞⠥⠂ ⠒ ⠞⠱⠆⠁⠣⠞ ⠚ ⠞⠺ ⠝⠋⠆ ⠍⠥ ⠝⠋⠆ ⠗⠁ ⠅ ⠞⠺⠱⠂ ⠝ ⠹ ⠲
[2022-04-13 07:47:22] Best translation 2150 : ⠪ ⠣⠨⠁ ⠌⠣⠞⠁ ⠅⠣ ⠃⠁⠳ ⠏⠁ ⠇⠆ ⠿ ⠓ ⠸⠽⠴ ⠗⠁ ⠎⠪⠆⠞ ⠅⠣ ⠝⠔ ⠰⠣⠣ ⠎⠁ ⠋ ⠞⠣⠞ ⠃⠮⠆ ⠝⠮⠂ ⠌ ⠗⠱⠆ ⠞⠮⠂ ⠎⠁ ⠞⠺⠱ ⠡⠪⠆⠍⠥⠝⠆ ⠏⠁⠸ ⠌ ⠏ ⠏⠭⠗⠣ ⠝⠱ ⠰⠣⠁ ⠏⠻⠂ ⠲
[2022-04-13 07:47:22] Best translation 2151 : ⠝⠱⠂⠞⠖⠆ ⠰⠣⠁ ⠅⠁⠆ ⠙⠶⠆⠏⠶ ⠹ ⠣⠎⠁ ⠩⠁⠯ ⠿⠋ ⠹ ⠩ ⠧ ⠈⠱⠅ ⠹⠁⠆⠌⠮ ⠚ ⠹ ⠣⠍⠊ ⠾⠑⠠⠣⠁ ⠅ ⠟⠪⠂ ⠅⠉ ⠑ ⠇⠬ ⠹⠅⠹ ⠌⠣ ⠹⠁⠆ ⠒ ⠌⠣ ⠹⠣⠍⠪⠆ ⠚ ⠹ ⠾⠱⠰⠣⠉⠂ ⠣⠇⠢⠆⠇⠢⠆ ⠅⠣⠞ ⠹⠻⠆ ⠅⠕ ⠿⠓ ⠣⠍⠊ ⠙ ⠅⠣⠞⠯ ⠱ ⠊ ⠲
[2022-04-13 07:47:22] Best translation 2152 : ⠪ ⠁⠑ ⠇⠥⠝⠯ ⠈⠋⠆⠟⠮ ⠇⠽⠴⠏⠣⠞ ⠹⠻⠆ ⠣⠽ ⠅ ⠟⠥ ⠋ ⠞⠣⠞ ⠛ ⠓ ⠈⠕ ⠊ ⠲
[2022-04-13 07:47:22] Best translation 2153 : ⠹⠥⠌⠮⠡⠔⠆ ⠏⠱⠆ ⠞⠮⠂ ⠍⠥⠞⠮ ⠣⠾⠣⠟⠕⠆⠓⠌⠁ ⠿⠪⠆ ⠿⠋ ⠗⠱⠆ ⠟ ⠗⠣⠶ ⠲
[2022-04-13 07:47:22] Best translation 2154 : ⠟⠥⠚ ⠹ ⠪ ⠍⠊⠞⠣⠈⠕⠆ ⠩⠔⠿⠥⠂ ⠅ ⠣⠇⠥⠝ ⠹⠣⠝⠁⠆ ⠎⠞⠝ ⠩ ⠇⠁ ⠟ ⠹ ⠗ ⠥⠆⠎⠋⠩⠺⠱ ⠗ ⠞⠖⠏⠔ ⠅⠁ ⠣⠸⠣⠥ ⠱⠝ ⠞⠺ ⠷⠣ ⠱⠅⠯ ⠞⠣⠞ ⠝ ⠹⠣⠓⠾⠣ ⠗⠣⠞⠞⠪ ⠈⠉⠆⠿⠓⠣⠞ ⠇⠬ ⠟ ⠃ ⠹ ⠲
[2022-04-13 07:47:22] Best translation 2155 : ⠟⠑⠥⠂ ⠿⠦ ⠹ ⠲
[2022-04-13 07:47:22] Best translation 2156 : ⠽⠨ ⠏⠔ ⠣⠈⠱⠅ ⠇⠥⠆ ⠹⠻⠆ ⠾⠁⠆ ⠿⠓ ⠏⠭ ⠹⠣⠞ ⠋⠂ ⠲
[2022-04-13 07:47:22] Best translation 2157 : ⠺⠋⠆⠹⠁⠁⠆⠗⠣ ⠒ ⠍⠣⠽⠁⠆ ⠅⠣ ⠞⠭ ⠹⠺⠮ ⠲
[2022-04-13 07:47:22] Best translation 2158 : ⠺⠱ ⠺⠱⠂ ⠺⠱⠆ ⠲
[2022-04-13 07:47:22] Best translation 2159 : ⠿⠋⠯ ⠹⠉⠆⠹⠣⠞ ⠟⠪⠂ ⠏⠁ ⠸ ⠾⠋⠍⠁ ⠃⠁⠹⠁⠎⠣⠅⠁⠆ ⠞⠺ ⠣⠗⠱⠆ ⠑⠨⠣⠗⠁ ⠩ ⠞⠓⠁⠆ ⠿⠪⠆ ⠭ ⠹⠿ ⠣⠗⠱⠆ ⠗ ⠣⠘⠣⠞ ⠓⠥⠯ ⠠⠣⠭ ⠾⠕⠆ ⠩ ⠱ ⠹ ⠲
[2022-04-13 07:47:22] Best translation 2160 : ⠺⠔⠆⠘⠋⠂ ⠇⠆ ⠋ ⠁⠖ ⠗⠣ ⠲
[2022-04-13 07:47:22] Best translation 2161 : ⠼⠁ ⠲ ⠴⠏⠁ ⠎⠣⠅⠁⠆⠇⠉⠆ ⠚ ⠊ ⠣⠝⠑ ⠣⠙⠱⠅⠏⠮ ⠅ ⠣⠃⠊⠙⠋ ⠞⠺ ⠩⠁ ⠏ ⠲
[2022-04-13 07:47:22] Best translation 2162 : ⠹⠔⠨⠋⠆⠎⠁ ⠣⠟⠔⠆ ⠲
[2022-04-13 07:47:22] Best translation 2163 : ⠡⠭⠸⠣⠣⠎ ⠹⠻⠆ ⠹⠁⠆ ⠲
[2022-04-13 07:47:22] Best translation 2164 : ⠓⠕ ⠩⠱⠂ ⠅⠣ ⠈⠥⠷⠋ ⠈⠥⠷⠋ ⠒ ⠃⠁ ⠹⠋ ⠇⠕⠂ ⠍⠱⠆ ⠲
[2022-04-13 07:47:22] Best translation 2165 : ⠍⠔⠛⠣⠇⠁⠏⠁ ⠲
[2022-04-13 07:47:23] Best translation 2166 : ⠍⠊⠍⠊ ⠞⠪ ⠹⠻⠆ ⠿ ⠍⠣⠹⠴⠹⠉⠆ ⠒ ⠸⠣⠥ ⠨⠮⠂ ⠹⠻⠆ ⠟⠥⠝ ⠗ ⠺⠥⠞⠁⠥⠂ ⠏⠭⠎⠪⠆ ⠣⠎⠥⠂⠎⠥⠂ ⠅ ⠠⠣⠶⠆⠇⠥ ⠚ ⠿⠓⠑⠈⠪⠆ ⠠⠣⠱⠅⠎⠑ ⠍⠂ ⠗⠋ ⠰⠣⠣ ⠅⠁⠅⠺⠮ ⠇⠕ ⠡ ⠭ ⠹ ⠲
[2022-04-13 07:47:23] Total time: 57.65462s wall

real	10m47.831s
user	19m59.719s
sys	0m31.420s
```

PE ရလဒ်တွေက အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-mt-br$ cat ./test0-PE-results.txt 
Evaluation on ./model0-mtbr.iter5000.npz with ../model.transformer/hyp.iter95000.br, Transformer PE Model:
BLEU = 84.48, 94.9/89.4/84.3/79.6 (BP=0.972, ratio=0.973, hyp_len=28019, ref_len=28803)
Evaluation on ./model0-mtbr.iter10000.npz with ../model.transformer/hyp.iter95000.br, Transformer PE Model:
BLEU = 85.55, 94.8/89.4/84.3/79.5 (BP=0.985, ratio=0.985, hyp_len=28384, ref_len=28803)
Evaluation on ./model0-mtbr.iter15000.npz with ../model.transformer/hyp.iter95000.br, Transformer PE Model:
BLEU = 85.47, 95.0/89.6/84.7/80.0 (BP=0.981, ratio=0.981, hyp_len=28265, ref_len=28803)
Evaluation on ./model0-mtbr.iter20000.npz with ../model.transformer/hyp.iter95000.br, Transformer PE Model:
BLEU = 85.99, 95.0/89.6/84.7/80.1 (BP=0.987, ratio=0.987, hyp_len=28419, ref_len=28803)
Evaluation on ./model0-mtbr.iter25000.npz with ../model.transformer/hyp.iter95000.br, Transformer PE Model:
BLEU = 85.94, 94.8/89.4/84.4/79.8 (BP=0.989, ratio=0.989, hyp_len=28487, ref_len=28803)
Evaluation on ./model0-mtbr.iter30000.npz with ../model.transformer/hyp.iter95000.br, Transformer PE Model:
BLEU = 85.99, 94.9/89.5/84.6/80.0 (BP=0.988, ratio=0.988, hyp_len=28447, ref_len=28803)
Evaluation on ./model0-mtbr.iter35000.npz with ../model.transformer/hyp.iter95000.br, Transformer PE Model:
BLEU = 86.16, 94.9/89.4/84.5/79.9 (BP=0.990, ratio=0.990, hyp_len=28527, ref_len=28803)
Evaluation on ./model0-mtbr.iter40000.npz with ../model.transformer/hyp.iter95000.br, Transformer PE Model:
BLEU = 86.15, 94.9/89.4/84.5/79.9 (BP=0.990, ratio=0.990, hyp_len=28527, ref_len=28803)
Evaluation on ./model0-mtbr.iter45000.npz with ../model.transformer/hyp.iter95000.br, Transformer PE Model:
BLEU = 86.21, 94.9/89.5/84.6/80.0 (BP=0.991, ratio=0.991, hyp_len=28531, ref_len=28803)
Evaluation on ./model0-mtbr.iter50000.npz with ../model.transformer/hyp.iter95000.br, Transformer PE Model:
BLEU = 86.26, 94.9/89.5/84.6/80.1 (BP=0.990, ratio=0.990, hyp_len=28525, ref_len=28803)
Evaluation on ./model0-mtbr.iter55000.npz with ../model.transformer/hyp.iter95000.br, Transformer PE Model:
BLEU = 86.26, 94.9/89.5/84.6/80.1 (BP=0.990, ratio=0.990, hyp_len=28528, ref_len=28803)
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-mt-br$
```

Transformer mt ရဲ့ အကောင်းဆုံးရလဒ်နဲ့ PE ရဲ့အကောင်းဆုံး ရလဒ် နှစ်ခုကို နှိုင်းယှဉ်ကြည့်ရင် အောက်ပါအတိုင်း...  

| Transformer | Post-Editing |
|----------:|----------:|
| 86.73 | 86.26 |

comparable result ကိုပဲ ပေးနိုင်တယ်။   

## Training MT_Myanmar-to-Myanmar

bash script ကို update လုပ်ခဲ့တယ်။ mt-ref-transformer-my.sh ဆိုတဲ့နာမည်နဲ့ သိမ်းခဲ့တယ်။  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, LST, NECTEC, Thailand
## Experiments for Transformer MT_Burmese-to-Ref_Burmese
## 13 April 2022

mkdir model.transformer-mt-my;

marian \
    --model  /media/ye/project2/exp/braille-nmt/model.transformer-mt-my/model0-mtmy.npz --type transformer \
    --train-sets /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000-trainingdata.my /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my \
    --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000-devdata.my /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.my \
    --valid-translation-output /media/ye/project2/exp/braille-nmt/model.transformer-mt-my/dev.mt-my.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log ./model.transformer-mt-br/train-mtbr.log --valid-log ./model.transformer-mt-br/valid-mtbr.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 1 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > /media/ye/project2/exp/braille-nmt/model.transformer-mt-my/config-mtmy0.yml
    
time marian -c /media/ye/project2/exp/braille-nmt/model.transformer-mt-my/config-mtmy0.yml  2>&1 | tee transformer-mtmy0.log

```

training ကိုလုပ်ခဲ့တယ်...  
training က တရက်ကျော် ကြာတယ် ဒီကြားထဲ training လုပ်နေစဉ်မှာ ရုံးမှာက သင်္ကြန်ပိတ်ရက်မို့လို့ မီးတွေကို ပြင်တာလုပ်တာမို့ နောက်တရက် (14 April 2022) မနက်အစောကြီးမှာ မီးပျက်သွားပြီး ညဘက် ၈နာရီလောက်မှ ပြန်လာတာမို့ training ပြီးသလောက် အခြေအနေကို ကြည့်ခဲ့တယ်...  

```
[2022-04-14 05:55:40] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-mt-my/model0-mtmy.npz.orig.npz
[2022-04-14 05:55:40] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-mt-my/model0-mtmy.iter180000.npz
[2022-04-14 05:55:41] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-mt-my/model0-mtmy.npz
[2022-04-14 05:55:41] Saving Adam parameters to /media/ye/project2/exp/braille-nmt/model.transformer-mt-my/model0-mtmy.npz.optimizer.npz
[2022-04-14 05:55:48] [valid] Ep. 2450 : Up. 180000 : cross-entropy : 12.6841 : stalled 3 times (last best: 12.6782)
[2022-04-14 05:55:50] [valid] Ep. 2450 : Up. 180000 : perplexity : 2.39658 : stalled 3 times (last best: 2.39562)
[2022-04-14 05:56:03] [valid] Ep. 2450 : Up. 180000 : bleu : 87.0547 : stalled 19 times (last best: 87.159)
[2022-04-14 05:56:19] Seen 16415 samples
[2022-04-14 05:56:19] Starting data epoch 2451 in logical epoch 2451
[2022-04-14 05:56:19] [data] Shuffling data
[2022-04-14 05:56:19] [data] Done reading 16,415 sentences
[2022-04-14 05:56:19] [data] Done shuffling 16,415 sentences to temp files
[2022-04-14 05:56:49] Seen 16415 samples
[2022-04-14 05:56:49] Starting data epoch 2452 in logical epoch 2452
[2022-04-14 05:56:49] [data] Shuffling data
[2022-04-14 05:56:49] [data] Done reading 16,415 sentences
[2022-04-14 05:56:49] [data] Done shuffling 16,415 sentences to temp files
```

အထက်မှာ မြင်ရတဲ့အတိုင်း BLEU score က stalled ဖြစ်တာလည်း ၁၉ ကြိမ် ရှိနေပြီမို့ လက်ရှိ training လုပ်ထားတဲ့ထဲက best model ကိုပဲ ယူဖို့ ဆုံးဖြတ်ခဲ့တယ်။  
ဒီတစ်ခေါက် test/eval လုပ်ရမယ့် မော်ဒယ်အရေအတွက် များတယ် အဲဒါကြောင့် bash looping ကို အောက်ပါလိုမျိုး မလုပ်တော့ပဲ...  

```bash
for i in {5000,10000,15000,20000,25000,30000,35000,40000,45000,50000,55000,60000,65000,70000,75000,80000,85000,90000,95000,100000,105000,110000,115000,120000,125000,130000,135000,140000,145000,150000,155000,160000,165000,170000,175000,180000}
```

အောက်ပါလို incremental နဲ့ ရေးခဲ့...  

```bash
for i in {5000..180000..5000} 
```

testing bash script (tran-eval-pe.sh) ကို အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့ပြီး model output ဖိုလ်ဒါဖြစ်တဲ့ ```model.transformer-mt-my/``` အောက်မှာ run  ခဲ့တယ် ...  

```bash
#!/bin/bash

## Preparation for Myanmar-MuHaung PE
## Written by Ye, LST, NECTEC, Thailand
## Translation and Evaluation with Marian, Transformer PE Model
## 14 April 2022
model0-mtmy.iter5000.npz
for i in {5000..180000..5000} 
do
   marian-decoder -m ./model0-mtmy.iter$i.npz -v /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml --devices 0 1 --output hyp.iter$i.my < ../model.transformer-brmy/hyp.iteriter80000.my
   echo "Evaluation on ./model0-mtmy.iter${i}.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:" >> test0-PE-results.txt
   perl ~/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my < ./hyp.iter$i.my  >> test0-PE-results.txt
done
```

testing/evaluation for mt-my PE:  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-mt-my$ time ./tran-eval-pe.sh 
...
...
...
[2022-04-14 21:57:30] Best translation 2140 : ရှေးခေတ် စစ်သည် တစ် ဦး ၏ ဘဝ တစ် စိတ် တစ် ပိုင်း ကို ထင်ဟပ် သော အိုင်းချင်း ဖြစ် သည် ။
[2022-04-14 21:57:30] Best translation 2141 : လိပ်ပြာ တွင် လည်း အခြား သော ဥပေါသထ ကဲ့သို့ ဦးခေါင်း ပိုင်း ၊ ရင် ပိုင်း ၊ ဝမ်းဗိုက် ပိုင်း ဟူ၍ ရှိ သည် ။
[2022-04-14 21:57:30] Best translation 2142 : ကာတွန်း ဆရာကြီး ဦးဘဂျမ်း ။
[2022-04-14 21:57:30] Best translation 2143 : ဈမျဉ်းဆွဲ ။
[2022-04-14 21:57:30] Best translation 2144 : သွေးတူမွေးတူ နွားများ ကို ချူများ ၊ အဆင်တန်ဆာများ ဆင် ပြီးလျှင် လှည်းယဉ် တွင် ခင်မ မောင်း လေ့ ရှိ သည် ။
[2022-04-14 21:57:30] Best translation 2145 : ရှင် ၊ ခင်ဗျာ ဟု ထူး မှ ယဉ်ကျေးသည် ။
[2022-04-14 21:57:30] Best translation 2146 : ၉ ၃ ၄ ခု တွင် ပေါ်ပေါက် ခဲ့ သော အသားရောင် သည် အရေး တွင် အရေး တွင် ကား မင်းတရားကြီး က ဗညားဒလ အပေါ် အမျက် တော် ရှိ၍ ချောင်းဦး ကျေးရွာ တွင် ကျွန် ငါး ယောက် နှင့် ထား တော် မူ သည် ။
[2022-04-14 21:57:30] Best translation 2147 : ၁ ၀ ။ ဝါသနာ = စွဲမြဲ နေ သော အလေ့အကျင့် ။
[2022-04-14 21:57:30] Best translation 2148 : မောင်ဖိုးစိန် သည် ဇာတ်သဘင်ပညာ ကို အခြေခံ မှ စ၍ သင်ယူ လေ့လာ ခဲ့ သည် ။
[2022-04-14 21:57:30] Best translation 2149 : ရတု ၊ တေးထပ် တို့ တွင် နန်း မူ နန်း ရာ ကို တွေ့ နိုင် သည် ။
[2022-04-14 21:57:30] Best translation 2150 : ဤ အခါ ငတာ က ဘာကြောင့် ပါ လည်း ဘုရား ဟု လျှောက် ရာ ငယ်ထိပ် က နင် မှ စာ မ တတ် ဘဲ နဲ့ ငါ ရေး တဲ့ စာ တွေ ချီးမွမ်း ပါလျှင် ငါ ပါ ပစ်ရ နေ မှာ ပေါ့ ။
[2022-04-14 21:57:30] Best translation 2151 : နေ့တိုင်း မှာ ကား ပုတ်သင်ညို သည် အစာ ရှာ၍ ပြန် သည် ရှိ သော် ဆိတ် သားငယ် တို့ သည် အမိ မျက်နှာ ကို ကြည့် ကုန် လျက် လိုက် သကဲ့သို့ ငါ့ သား ၊ ငါ့ သမီး တို့ သည် မြေမှုန့် အလိမ်းလိမ်း ကပ် သော ကိုယ် ဖြင့် အမိ သို့ ကပ်၍ နေ ၏ ။
[2022-04-14 21:57:30] Best translation 2152 : ဤ ထက် လွန်၍ ဆန်းကြယ် လျောက်ပတ် သော အရာ ကို ကျွန်ုပ် မ တတ် ပြီ ဟု ဆို ၏ ။
[2022-04-14 21:57:30] Best translation 2153 : သူငယ်ချင်း ပေး တဲ့ ပုတ်သင်ညို မူတည် ပြီး ပြန် ရေး ကြ ရအောင် ။
[2022-04-14 21:57:30] Best translation 2154 : ကျွန်ုပ်တို့ သည် ဤ မိတဆိုး ရှင်ပြု ကို အလွန် သနား စေတနာ ရှိ လာ ကြ သည် နှင့် ဦးစံရွှေ နှင့် တိုင်ပင် ကာ အလှူ အိမ် တွင် ည အိပ်၍ တတ် နိုင် သမျှ ကုပ်ကုပ် ဆုံးဖြတ် လိုက် ကြ လေ သည် ။
[2022-04-14 21:57:30] Best translation 2155 : ကြက်ဥ ပြုတ် သည် ။
[2022-04-14 21:57:30] Best translation 2156 : ယခု ပင် အဆိပ် လူး သော မြား ဖြင့် ပစ် သတ် အံ့ ။
[2022-04-14 21:57:30] Best translation 2157 : ဝမ်းသာအားရ ၊ မယား က တစ် သွယ် ။
[2022-04-14 21:57:30] Best translation 2158 : ဝေ ဝေ့ ဝေး ။
[2022-04-14 21:57:30] Best translation 2159 : ပြန်၍ သုံးသပ် ကြည့် ပါ လျှင် မြန်မာ ဘာသာစကား တွင် အရေး အက္ခရာ ရှိ ထား ပြီး ဖြစ် သဖြင့် အရေး နှင့် အဖတ် ဟူ၍ နှစ် မျိုး ရှိ နေ သည် ။
[2022-04-14 21:57:30] Best translation 2160 : ဂြောင် လည်း မ ထိုင် ရ ။
[2022-04-14 21:57:30] Best translation 2161 : ၁ ။ အောက်ပါ စကားလုံး တို့ ၏ အနက် အဓိပ္ပာယ် ကို အဘိဓာန် တွင် ရှာ ပါ ။
[2022-04-14 21:57:30] Best translation 2162 : သင်ခန်းစာ အကျဉ်း ။
[2022-04-14 21:57:30] Best translation 2163 : ချစ်လှစွာ သော သား ။
[2022-04-14 21:57:31] Best translation 2164 : ဟို ရှေ့ က ဆူညံ ဆူညံ ၊ ဘာ သံ လို့ မေး ။
[2022-04-14 21:57:31] Best translation 2165 : ဒူးရင်းသီး ။
[2022-04-14 21:57:31] Best translation 2166 : မိမိ တည် သော ဘုရား ကလအုတ် ၊ လှူ ခဲ့ သော ကျွန် နှင့် ဝတ္ထု ပစ္စည်း အစုစု ကို နှောင်းလူ တို့ ဖျက်ဆီး နှိပ်စက် မည့် မှ ကာကွယ် လို ခြင်း ဖြစ် သည် ။
[2022-04-14 21:57:31] Total time: 58.33343s wall

real	36m23.197s
user	67m41.948s
sys	1m36.316s
```

translation result for mt_Burmese to Burmese PE:  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-mt-my$ cat test0-PE-results.txt
Evaluation on ./model0-mtmy.iter5000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 85.20, 95.0/89.8/85.1/80.7 (BP=0.974, ratio=0.974, hyp_len=28057, ref_len=28803)
Evaluation on ./model0-mtmy.iter10000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 86.30, 95.0/89.8/85.2/80.8 (BP=0.986, ratio=0.986, hyp_len=28395, ref_len=28803)
Evaluation on ./model0-mtmy.iter15000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 86.67, 95.1/90.0/85.4/81.1 (BP=0.988, ratio=0.988, hyp_len=28448, ref_len=28803)
Evaluation on ./model0-mtmy.iter20000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.12, 95.1/90.0/85.5/81.2 (BP=0.992, ratio=0.992, hyp_len=28578, ref_len=28803)
Evaluation on ./model0-mtmy.iter25000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.16, 95.1/90.1/85.6/81.3 (BP=0.992, ratio=0.992, hyp_len=28577, ref_len=28803)
Evaluation on ./model0-mtmy.iter30000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.13, 95.1/90.0/85.5/81.3 (BP=0.992, ratio=0.992, hyp_len=28580, ref_len=28803)
Evaluation on ./model0-mtmy.iter35000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.16, 95.1/90.0/85.5/81.2 (BP=0.993, ratio=0.993, hyp_len=28588, ref_len=28803)
Evaluation on ./model0-mtmy.iter40000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.11, 95.1/90.0/85.5/81.2 (BP=0.993, ratio=0.993, hyp_len=28589, ref_len=28803)
Evaluation on ./model0-mtmy.iter45000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.18, 95.1/90.0/85.5/81.3 (BP=0.993, ratio=0.993, hyp_len=28591, ref_len=28803)
Evaluation on ./model0-mtmy.iter50000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.24, 95.1/90.1/85.6/81.3 (BP=0.993, ratio=0.993, hyp_len=28597, ref_len=28803)
Evaluation on ./model0-mtmy.iter55000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.21, 95.1/90.0/85.6/81.3 (BP=0.993, ratio=0.993, hyp_len=28598, ref_len=28803)
Evaluation on ./model0-mtmy.iter60000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.17, 95.0/90.0/85.5/81.2 (BP=0.993, ratio=0.993, hyp_len=28597, ref_len=28803)
Evaluation on ./model0-mtmy.iter65000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.20, 95.1/90.0/85.5/81.3 (BP=0.993, ratio=0.993, hyp_len=28601, ref_len=28803)
Evaluation on ./model0-mtmy.iter70000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.22, 95.1/90.0/85.5/81.3 (BP=0.993, ratio=0.993, hyp_len=28603, ref_len=28803)
Evaluation on ./model0-mtmy.iter75000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.23, 95.1/90.1/85.6/81.3 (BP=0.993, ratio=0.993, hyp_len=28599, ref_len=28803)
Evaluation on ./model0-mtmy.iter80000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.21, 95.1/90.1/85.5/81.3 (BP=0.993, ratio=0.993, hyp_len=28596, ref_len=28803)
Evaluation on ./model0-mtmy.iter85000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.18, 95.1/90.0/85.5/81.2 (BP=0.993, ratio=0.993, hyp_len=28595, ref_len=28803)
Evaluation on ./model0-mtmy.iter90000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.17, 95.1/90.0/85.5/81.2 (BP=0.993, ratio=0.993, hyp_len=28597, ref_len=28803)
Evaluation on ./model0-mtmy.iter95000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.22, 95.1/90.0/85.5/81.3 (BP=0.993, ratio=0.993, hyp_len=28600, ref_len=28803)
Evaluation on ./model0-mtmy.iter100000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.23, 95.1/90.1/85.6/81.3 (BP=0.993, ratio=0.993, hyp_len=28594, ref_len=28803)
Evaluation on ./model0-mtmy.iter105000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.25, 95.1/90.1/85.6/81.4 (BP=0.993, ratio=0.993, hyp_len=28596, ref_len=28803)
Evaluation on ./model0-mtmy.iter110000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.21, 95.1/90.0/85.6/81.3 (BP=0.993, ratio=0.993, hyp_len=28594, ref_len=28803)
Evaluation on ./model0-mtmy.iter115000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.22, 95.1/90.1/85.6/81.3 (BP=0.993, ratio=0.993, hyp_len=28596, ref_len=28803)
Evaluation on ./model0-mtmy.iter120000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.21, 95.1/90.1/85.5/81.3 (BP=0.993, ratio=0.993, hyp_len=28593, ref_len=28803)
Evaluation on ./model0-mtmy.iter125000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.22, 95.1/90.1/85.6/81.3 (BP=0.993, ratio=0.993, hyp_len=28593, ref_len=28803)
Evaluation on ./model0-mtmy.iter130000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.25, 95.1/90.1/85.6/81.4 (BP=0.993, ratio=0.993, hyp_len=28592, ref_len=28803)
Evaluation on ./model0-mtmy.iter135000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.25, 95.1/90.1/85.6/81.3 (BP=0.993, ratio=0.993, hyp_len=28596, ref_len=28803)
Evaluation on ./model0-mtmy.iter140000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.19, 95.1/90.0/85.5/81.3 (BP=0.993, ratio=0.993, hyp_len=28597, ref_len=28803)
Evaluation on ./model0-mtmy.iter145000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.22, 95.1/90.0/85.6/81.3 (BP=0.993, ratio=0.993, hyp_len=28597, ref_len=28803)
Evaluation on ./model0-mtmy.iter150000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.22, 95.1/90.1/85.6/81.3 (BP=0.993, ratio=0.993, hyp_len=28593, ref_len=28803)
Evaluation on ./model0-mtmy.iter155000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.22, 95.1/90.0/85.6/81.3 (BP=0.993, ratio=0.993, hyp_len=28597, ref_len=28803)
Evaluation on ./model0-mtmy.iter160000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.19, 95.1/90.0/85.5/81.3 (BP=0.993, ratio=0.993, hyp_len=28595, ref_len=28803)
Evaluation on ./model0-mtmy.iter165000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.21, 95.1/90.1/85.5/81.3 (BP=0.993, ratio=0.993, hyp_len=28597, ref_len=28803)
Evaluation on ./model0-mtmy.iter170000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.21, 95.1/90.1/85.5/81.3 (BP=0.993, ratio=0.993, hyp_len=28599, ref_len=28803)
Evaluation on ./model0-mtmy.iter175000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.18, 95.1/90.0/85.5/81.2 (BP=0.993, ratio=0.993, hyp_len=28600, ref_len=28803)
Evaluation on ./model0-mtmy.iter180000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.19, 95.1/90.0/85.5/81.2 (BP=0.993, ratio=0.993, hyp_len=28595, ref_len=28803)
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-mt-my
```

Best model, best score ပေးတာက အောက်ပါအတိုင်း  

```
Evaluation on ./model0-mtmy.iter105000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.25, 95.1/90.1/85.6/81.4 (BP=0.993, ratio=0.993, hyp_len=28596, ref_len=28803)
```

```
Evaluation on ./model0-mtmy.iter130000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.25, 95.1/90.1/85.6/81.4 (BP=0.993, ratio=0.993, hyp_len=28592, ref_len=28803)
```

```
Evaluation on ./model0-mtmy.iter135000.npz with ../model.transformer-brmy/hyp.iteriter80000.my, Transformer PE Model:
BLEU = 87.25, 95.1/90.1/85.6/81.3 (BP=0.993, ratio=0.993, hyp_len=28596, ref_len=28803)
```
