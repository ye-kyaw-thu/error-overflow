# MuHaung Post Editing with Two NMT Models

## Preparation

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
