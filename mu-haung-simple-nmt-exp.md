# MuHaung Braille Running With Simple-NMT

အထက်က link မှာ မြင်ရတဲ့အတိုင်းပဲ မူဟောင်း မျက်မမြင်စာနဲ့မြန်မာဘာသာ အကြားမှာ marian framework ကို သုံးပြီးတော့ GPU နှစ်လုံးနဲ့ training လုပ်တာမှာ အကြမ်းဖျဉ်းအားဖြင့် ၉နာရီကျော် ၁၀နာရီ ကြာတယ်။  
အဲဒါကြောင့် ဒီတစ်ခေါက်တော့ Simple-NMT နဲ့ training လုပ်ကြည့်ပြီးတော့ ကြာချိန်နဲ့ ရလဒ်ကို နှိုင်းယှဉ်ကြည့်ခဲ့...  

## Preparation

10-fold ခွဲထားတဲ့ထဲကနေ 0/ ဒေတာကို ယူပြီး experiment လုပ်မယ်။  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt/0$ head train.my
၄ ။ အောက်ပါ မေးခွန်းများ ကို ဖြေဆို ပါ ။
အဲဒီ မှာ ကိုရွှေ ဗျည်း တို့ မသရ တို့ ရှိ ကြ တယ် လေ ။
စစ် မှာ ယွန်းမ ။
ဆ ။
တံခွန်တိုင် ရွှေကုက္ကား နဲ့ ဘုရား ကို မြင် ။
ဥ ကုန် သော် ဟင်္သာ ငယ် တို့ ကို နောက် ဟင်္သာ အို တို့ ကို အစဉ် အတိုင်း စား ကြ လေ ၏ ။
ဦးပေါင်း ကျား နှင့် မြင်းကျား ရှင် ။
သူငယ် အမိ လည်း ငါ့ သား ကို ယူ၍ အဘယ် သို့ သွား မည်နည်း ဟု လိုက် လျက် ဘီလူးမ ကို ကိုင် ဆွဲ ၏ ။
ရွှေ အိမ် နန်း နှင့် ကြငှန်း လည်း ခံ မတ် ပေါင်းရံ လျက် ပျော်စံ ရိပ်ငြိမ် စည်းစိမ် မကွာ ။
မြန်မာ ဘာသာ ကား အိမ် ထန်းပင် ဟု ခေါ်ဝေါ် ကုန် ၏ ။
```

```
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt/0$ head train.br
⠼⠙ ⠲ ⠴⠏ ⠍⠱⠆⠨⠥⠝⠆⠾ ⠅ ⠿⠓⠱⠈⠕ ⠏ ⠲
⠮⠆⠙⠪ ⠰⠣⠁ ⠅⠕⠩⠺⠱ ⠃⠽⠪⠆ ⠚ ⠍⠣⠹⠣⠗⠣ ⠚ ⠩ ⠟ ⠞⠮ ⠇⠱ ⠲
⠎⠭ ⠰⠣⠁ ⠽⠥⠝⠆⠍⠣ ⠲
⠈⠣ ⠲
⠞⠋⠨⠥⠝⠞⠖ ⠩⠺⠱⠅⠦⠅⠁⠆ ⠝⠮⠂ ⠿ ⠅ ⠾⠔ ⠲
⠥⠂ ⠅⠉ ⠧ ⠓⠔⠹⠁ ⠌⠮ ⠚ ⠅ ⠱⠴ ⠓⠔⠹⠁ ⠕ ⠚ ⠅ ⠣⠎ ⠣⠞⠖⠆ ⠎⠁⠆ ⠟ ⠃ ⠊ ⠲
⠥⠆⠏⠶⠆ ⠟⠁⠆ ⠗ ⠾⠔⠆⠟⠁⠆ ⠩⠔ ⠲
⠹⠥⠌⠮ ⠣⠍⠊ ⠇⠆ ⠌⠣ ⠹⠁⠆ ⠅ ⠽⠥⠯ ⠣⠃⠮ ⠙ ⠹⠺⠁⠆ ⠍⠝ ⠓ ⠇⠬ ⠑ ⠃⠪⠇⠥⠆⠍⠣ ⠅ ⠅⠖ ⠈⠺⠮⠆ ⠊ ⠲
⠩⠺⠱ ⠱⠝ ⠝⠋⠆ ⠗ ⠟⠣⠓⠌⠋⠆ ⠇⠆ ⠨⠋ ⠍⠣⠞ ⠏⠶⠆⠗⠋ ⠑ ⠿⠻⠎⠋ ⠗⠱⠅⠷⠢ ⠎⠪⠆⠎⠢ ⠍⠣⠅⠺⠁ ⠲
⠾⠋⠍⠁ ⠃⠁⠹⠁ ⠅⠁⠆ ⠱⠝ ⠁⠋⠆⠏⠔ ⠓ ⠨⠻⠺⠻ ⠅⠉ ⠊ ⠲
(base) ye@:/media/ye/project2/exp/braille-nmt/data/for-nmt/0$
```

### Bash Script for Training

ရှေ့မှာလုပ်ခဲ့တဲ့ မြန်မာ-ရခိုင်၊ မြန်မာ-ဘိတ် တို့ကို Simple-NMT နဲ့ run ခဲ့တဲ့ရလဒ်တွေကို အခြေခံပြီး running command ကို အောက်ပါအတိုင်း ထားခဲ့တယ်။ epoch ကိုတော့ 300 ပေးထားတယ်။  
bash shell script ရဲ့ နာမည်က ```braille-seq2seq-training.sh```  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Visiting Professor, LST, NECTEC, Thailand
## Last updated: 9 April 2022
## for Myanmar-Mu_Haung and Mu_Haung-Myanmar NMT with Simple-NMT
## plan to compare with Marian NMT Framework

# training for my-br
time python train.py --train /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train \
--valid /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev \
--lang mybr \
--gpu_id 0 --batch_size 64 --n_epochs 300 \
--max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 \
--max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 \
--use_adam --rl_n_epochs 0 \
--model_fn ./model/braille/seq2seq/my-br/seq-model-mybr.pth  | tee ./model/braille/seq2seq/my-br/mybr-seq2seq-training.log;

# training for br-my
time python train.py --train /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train \
--valid /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev \
--lang brmy \
--gpu_id 1 --batch_size 64 --n_epochs 300 \
--max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 \
--max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 \
--use_adam --rl_n_epochs 0 \
--model_fn ./model/braille/seq2seq/br-my/seq-model-mybr.pth  | tee ./model/braille/seq2seq/br-my/mybr-seq2seq-training.log;

```

## Training

training က အောက်ပါအတိုင်း လုပ်ခဲ့တယ်။  
(simple-nmt) ye@:~/exp/simple-nmt$ time ./braille-seq2seq-training.sh | tee ./braille-seq2seq-mybk-brmy-training.log  


training log for for my-bk:  

```

```

training log for for my-bk:  

```

```



