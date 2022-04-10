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

### Bash Script for Seq2Seq Training

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
--model_fn ./model/braille/seq2seq/br-my/seq-model-brmy.pth  | tee ./model/braille/seq2seq/br-my/brmy-seq2seq-training.log;

```

## Seq2Seq Training

training က အောက်ပါအတိုင်း လုပ်ခဲ့တယ်။  
(simple-nmt) ye@:~/exp/simple-nmt$ time ./braille-seq2seq-training.sh | tee ./braille-seq2seq-mybk-brmy-training.log  


training log for for my-br:  

```
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'mybr',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/braille/seq2seq/my-br/seq-model-mybr.pth',
    'n_epochs': 300,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/media/ye/project2/exp/braille-nmt/data/for-nmt/0/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(17001, 128)
  (emb_dec): Embedding(16798, 128)
  (encoder): Encoder(
    (rnn): LSTM(128, 64, num_layers=4, batch_first=True, dropout=0.2, bidirectional=True)
  )
  (decoder): Decoder(
    (rnn): LSTM(256, 128, num_layers=4, batch_first=True, dropout=0.2)
  )
  (attn): Attention(
    (linear): Linear(in_features=128, out_features=128, bias=False)
    (softmax): Softmax(dim=-1)
  )
  (concat): Linear(in_features=256, out_features=128, bias=True)
  (tanh): Tanh()
  (generator): Generator(
    (output): Linear(in_features=128, out_features=16798, bias=True)
    (softmax): LogSoftmax(dim=-1)
  )
)
NLLLoss()
Adam (
Parameter Group 0
    amsgrad: False
    betas: (0.9, 0.999)
    eps: 1e-08
    lr: 0.001
    weight_decay: 0
)
Epoch 1 - |param|=2.08e+03 |g_param|=1.09e+05 loss=5.5464e+00 ppl=256.31
Validation - loss=4.5969e+00 ppl=99.18 best_loss=inf best_ppl=inf
Epoch 2 - |param|=2.08e+03 |g_param|=7.63e+04 loss=5.0714e+00 ppl=159.40
Validation - loss=4.2254e+00 ppl=68.40 best_loss=4.5969e+00 best_ppl=99.18
Epoch 3 - |param|=2.08e+03 |g_param|=6.70e+04 loss=4.9176e+00 ppl=136.68
Validation - loss=4.0768e+00 ppl=58.96 best_loss=4.2254e+00 best_ppl=68.40
Epoch 4 - |param|=2.08e+03 |g_param|=7.65e+04 loss=4.7471e+00 ppl=115.25
Validation - loss=3.9643e+00 ppl=52.68 best_loss=4.0768e+00 best_ppl=58.96
Epoch 5 - |param|=2.08e+03 |g_param|=6.59e+04 loss=4.5055e+00 ppl=90.51
Validation - loss=3.8657e+00 ppl=47.74 best_loss=3.9643e+00 best_ppl=52.68
Epoch 6 - |param|=2.09e+03 |g_param|=7.51e+04 loss=4.4626e+00 ppl=86.72
Validation - loss=3.8064e+00 ppl=44.99 best_loss=3.8657e+00 best_ppl=47.74
Epoch 7 - |param|=2.09e+03 |g_param|=7.85e+04 loss=4.2485e+00 ppl=70.00
Validation - loss=3.7405e+00 ppl=42.12 best_loss=3.8064e+00 best_ppl=44.99
Epoch 8 - |param|=2.09e+03 |g_param|=7.82e+04 loss=4.1057e+00 ppl=60.69
Validation - loss=3.6542e+00 ppl=38.64 best_loss=3.7405e+00 best_ppl=42.12
Epoch 9 - |param|=2.09e+03 |g_param|=8.15e+04 loss=4.0542e+00 ppl=57.64
Validation - loss=3.6071e+00 ppl=36.86 best_loss=3.6542e+00 best_ppl=38.64
Epoch 10 - |param|=2.09e+03 |g_param|=8.24e+04 loss=3.8519e+00 ppl=47.08
Validation - loss=3.5445e+00 ppl=34.62 best_loss=3.6071e+00 best_ppl=36.86
Epoch 11 - |param|=2.09e+03 |g_param|=8.59e+04 loss=3.7685e+00 ppl=43.31
Validation - loss=3.4818e+00 ppl=32.52 best_loss=3.5445e+00 best_ppl=34.62
Epoch 12 - |param|=2.09e+03 |g_param|=7.86e+04 loss=3.6748e+00 ppl=39.44
Validation - loss=3.4409e+00 ppl=31.22 best_loss=3.4818e+00 best_ppl=32.52
Epoch 13 - |param|=2.09e+03 |g_param|=1.07e+05 loss=3.5348e+00 ppl=34.29
Validation - loss=3.3995e+00 ppl=29.95 best_loss=3.4409e+00 best_ppl=31.22
Epoch 14 - |param|=2.09e+03 |g_param|=8.99e+04 loss=3.4641e+00 ppl=31.95
Validation - loss=3.3497e+00 ppl=28.49 best_loss=3.3995e+00 best_ppl=29.95
Epoch 15 - |param|=2.09e+03 |g_param|=1.02e+05 loss=3.3657e+00 ppl=28.95
Validation - loss=3.3397e+00 ppl=28.21 best_loss=3.3497e+00 best_ppl=28.49
Epoch 16 - |param|=2.09e+03 |g_param|=1.48e+05 loss=3.2397e+00 ppl=25.53
Validation - loss=3.2877e+00 ppl=26.78 best_loss=3.3397e+00 best_ppl=28.21
Epoch 17 - |param|=2.09e+03 |g_param|=2.03e+05 loss=3.2164e+00 ppl=24.94
Validation - loss=3.2682e+00 ppl=26.26 best_loss=3.2877e+00 best_ppl=26.78
Epoch 18 - |param|=2.09e+03 |g_param|=1.97e+05 loss=3.1093e+00 ppl=22.41
Validation - loss=3.2305e+00 ppl=25.29 best_loss=3.2682e+00 best_ppl=26.26
Epoch 19 - |param|=2.10e+03 |g_param|=1.88e+05 loss=3.0110e+00 ppl=20.31
Validation - loss=3.1973e+00 ppl=24.47 best_loss=3.2305e+00 best_ppl=25.29
Epoch 20 - |param|=2.10e+03 |g_param|=1.93e+05 loss=2.9142e+00 ppl=18.43
Validation - loss=3.1846e+00 ppl=24.16 best_loss=3.1973e+00 best_ppl=24.47
Epoch 21 - |param|=2.10e+03 |g_param|=2.39e+05 loss=2.9455e+00 ppl=19.02
Validation - loss=3.1906e+00 ppl=24.30 best_loss=3.1846e+00 best_ppl=24.16
Epoch 22 - |param|=2.10e+03 |g_param|=1.17e+05 loss=2.8650e+00 ppl=17.55
Validation - loss=3.1659e+00 ppl=23.71 best_loss=3.1846e+00 best_ppl=24.16
Epoch 23 - |param|=2.10e+03 |g_param|=1.27e+05 loss=2.7931e+00 ppl=16.33
Validation - loss=3.2189e+00 ppl=25.00 best_loss=3.1659e+00 best_ppl=23.71
Epoch 24 - |param|=2.10e+03 |g_param|=1.09e+05 loss=2.7057e+00 ppl=14.96
Validation - loss=3.1345e+00 ppl=22.98 best_loss=3.1659e+00 best_ppl=23.71
Epoch 25 - |param|=2.10e+03 |g_param|=1.18e+05 loss=2.6430e+00 ppl=14.06
Validation - loss=3.1007e+00 ppl=22.21 best_loss=3.1345e+00 best_ppl=22.98
Epoch 26 - |param|=2.10e+03 |g_param|=1.17e+05 loss=2.6238e+00 ppl=13.79
Validation - loss=3.0831e+00 ppl=21.83 best_loss=3.1007e+00 best_ppl=22.21
Epoch 27 - |param|=2.10e+03 |g_param|=1.23e+05 loss=2.5319e+00 ppl=12.58
Validation - loss=3.1087e+00 ppl=22.39 best_loss=3.0831e+00 best_ppl=21.83
Epoch 28 - |param|=2.10e+03 |g_param|=1.07e+05 loss=2.4711e+00 ppl=11.84
Validation - loss=3.0522e+00 ppl=21.16 best_loss=3.0831e+00 best_ppl=21.83
Epoch 29 - |param|=2.10e+03 |g_param|=1.09e+05 loss=2.4382e+00 ppl=11.45
Validation - loss=3.0389e+00 ppl=20.88 best_loss=3.0522e+00 best_ppl=21.16
Epoch 30 - |param|=2.10e+03 |g_param|=1.42e+05 loss=2.4119e+00 ppl=11.15
Validation - loss=3.0770e+00 ppl=21.69 best_loss=3.0389e+00 best_ppl=20.88
Epoch 31 - |param|=2.11e+03 |g_param|=1.23e+05 loss=2.3377e+00 ppl=10.36
Validation - loss=3.0138e+00 ppl=20.36 best_loss=3.0389e+00 best_ppl=20.88
Epoch 32 - |param|=2.11e+03 |g_param|=1.47e+05 loss=2.2646e+00 ppl=9.63
Validation - loss=3.0679e+00 ppl=21.50 best_loss=3.0138e+00 best_ppl=20.36
Epoch 33 - |param|=2.11e+03 |g_param|=1.21e+05 loss=2.2067e+00 ppl=9.09
Validation - loss=3.0095e+00 ppl=20.28 best_loss=3.0138e+00 best_ppl=20.36
Epoch 34 - |param|=2.11e+03 |g_param|=1.14e+05 loss=2.1249e+00 ppl=8.37
Validation - loss=3.0137e+00 ppl=20.36 best_loss=3.0095e+00 best_ppl=20.28
Epoch 35 - |param|=2.11e+03 |g_param|=1.29e+05 loss=2.1596e+00 ppl=8.67
Validation - loss=2.9989e+00 ppl=20.06 best_loss=3.0095e+00 best_ppl=20.28
Epoch 36 - |param|=2.11e+03 |g_param|=1.30e+05 loss=2.0925e+00 ppl=8.10
Validation - loss=2.9981e+00 ppl=20.05 best_loss=2.9989e+00 best_ppl=20.06
Epoch 37 - |param|=2.11e+03 |g_param|=2.44e+05 loss=2.0618e+00 ppl=7.86
Validation - loss=2.9773e+00 ppl=19.63 best_loss=2.9981e+00 best_ppl=20.05
Epoch 38 - |param|=2.11e+03 |g_param|=2.62e+05 loss=2.0440e+00 ppl=7.72
Validation - loss=2.9699e+00 ppl=19.49 best_loss=2.9773e+00 best_ppl=19.63
Epoch 39 - |param|=2.11e+03 |g_param|=2.27e+05 loss=1.9441e+00 ppl=6.99
Validation - loss=2.9506e+00 ppl=19.12 best_loss=2.9699e+00 best_ppl=19.49
Epoch 40 - |param|=2.11e+03 |g_param|=2.64e+05 loss=1.9616e+00 ppl=7.11
Validation - loss=2.9887e+00 ppl=19.86 best_loss=2.9506e+00 best_ppl=19.12
Epoch 41 - |param|=2.11e+03 |g_param|=7.50e+04 loss=1.8706e+00 ppl=6.49
Validation - loss=2.9381e+00 ppl=18.88 best_loss=2.9506e+00 best_ppl=19.12
Epoch 42 - |param|=2.12e+03 |g_param|=8.78e+04 loss=1.9115e+00 ppl=6.76
Validation - loss=2.9831e+00 ppl=19.75 best_loss=2.9381e+00 best_ppl=18.88
Epoch 43 - |param|=2.12e+03 |g_param|=6.42e+04 loss=1.8956e+00 ppl=6.66
Validation - loss=2.9567e+00 ppl=19.24 best_loss=2.9381e+00 best_ppl=18.88
Epoch 44 - |param|=2.12e+03 |g_param|=6.66e+04 loss=1.8215e+00 ppl=6.18
Validation - loss=2.9342e+00 ppl=18.81 best_loss=2.9381e+00 best_ppl=18.88
Epoch 45 - |param|=2.12e+03 |g_param|=7.30e+04 loss=1.7701e+00 ppl=5.87
Validation - loss=2.9757e+00 ppl=19.60 best_loss=2.9342e+00 best_ppl=18.81
Epoch 46 - |param|=2.12e+03 |g_param|=6.23e+04 loss=1.7558e+00 ppl=5.79
Validation - loss=2.9402e+00 ppl=18.92 best_loss=2.9342e+00 best_ppl=18.81
Epoch 47 - |param|=2.12e+03 |g_param|=6.66e+04 loss=1.7275e+00 ppl=5.63
Validation - loss=2.9354e+00 ppl=18.83 best_loss=2.9342e+00 best_ppl=18.81
Epoch 48 - |param|=2.12e+03 |g_param|=6.75e+04 loss=1.6690e+00 ppl=5.31
Validation - loss=2.9483e+00 ppl=19.07 best_loss=2.9342e+00 best_ppl=18.81
Epoch 49 - |param|=2.12e+03 |g_param|=6.65e+04 loss=1.6621e+00 ppl=5.27
Validation - loss=2.9134e+00 ppl=18.42 best_loss=2.9342e+00 best_ppl=18.81
Epoch 50 - |param|=2.12e+03 |g_param|=8.58e+04 loss=1.6780e+00 ppl=5.35
Validation - loss=2.9288e+00 ppl=18.70 best_loss=2.9134e+00 best_ppl=18.42
Epoch 51 - |param|=2.12e+03 |g_param|=7.07e+04 loss=1.6259e+00 ppl=5.08
Validation - loss=2.9250e+00 ppl=18.63 best_loss=2.9134e+00 best_ppl=18.42
Epoch 52 - |param|=2.12e+03 |g_param|=6.60e+04 loss=1.5581e+00 ppl=4.75
Validation - loss=2.9305e+00 ppl=18.74 best_loss=2.9134e+00 best_ppl=18.42
Epoch 53 - |param|=2.13e+03 |g_param|=6.92e+04 loss=1.5395e+00 ppl=4.66
Validation - loss=2.9073e+00 ppl=18.31 best_loss=2.9134e+00 best_ppl=18.42
Epoch 54 - |param|=2.13e+03 |g_param|=7.53e+04 loss=1.5232e+00 ppl=4.59
Validation - loss=2.9197e+00 ppl=18.54 best_loss=2.9073e+00 best_ppl=18.31
Epoch 55 - |param|=2.13e+03 |g_param|=7.07e+04 loss=1.5271e+00 ppl=4.60
Validation - loss=2.9108e+00 ppl=18.37 best_loss=2.9073e+00 best_ppl=18.31
Epoch 56 - |param|=2.13e+03 |g_param|=6.81e+04 loss=1.4507e+00 ppl=4.27
Validation - loss=2.9099e+00 ppl=18.35 best_loss=2.9073e+00 best_ppl=18.31
Epoch 57 - |param|=2.13e+03 |g_param|=1.24e+05 loss=1.4195e+00 ppl=4.13
Validation - loss=2.9079e+00 ppl=18.32 best_loss=2.9073e+00 best_ppl=18.31
Epoch 58 - |param|=2.13e+03 |g_param|=1.44e+05 loss=1.4199e+00 ppl=4.14
Validation - loss=2.9430e+00 ppl=18.97 best_loss=2.9073e+00 best_ppl=18.31
Epoch 59 - |param|=2.13e+03 |g_param|=1.38e+05 loss=1.3818e+00 ppl=3.98
Validation - loss=2.9055e+00 ppl=18.27 best_loss=2.9073e+00 best_ppl=18.31
Epoch 60 - |param|=2.13e+03 |g_param|=1.60e+05 loss=1.4466e+00 ppl=4.25
Validation - loss=2.9400e+00 ppl=18.92 best_loss=2.9055e+00 best_ppl=18.27
Epoch 61 - |param|=2.13e+03 |g_param|=1.37e+05 loss=1.3731e+00 ppl=3.95
Validation - loss=2.9233e+00 ppl=18.60 best_loss=2.9055e+00 best_ppl=18.27
Epoch 62 - |param|=2.13e+03 |g_param|=1.70e+05 loss=1.3809e+00 ppl=3.98
Validation - loss=2.9224e+00 ppl=18.59 best_loss=2.9055e+00 best_ppl=18.27
Epoch 63 - |param|=2.13e+03 |g_param|=1.42e+05 loss=1.2887e+00 ppl=3.63
Validation - loss=2.9610e+00 ppl=19.32 best_loss=2.9055e+00 best_ppl=18.27
Epoch 64 - |param|=2.13e+03 |g_param|=1.34e+05 loss=1.2992e+00 ppl=3.67
Validation - loss=2.9214e+00 ppl=18.57 best_loss=2.9055e+00 best_ppl=18.27
Epoch 65 - |param|=2.14e+03 |g_param|=8.33e+04 loss=1.2807e+00 ppl=3.60
Validation - loss=2.9267e+00 ppl=18.67 best_loss=2.9055e+00 best_ppl=18.27
Epoch 66 - |param|=2.14e+03 |g_param|=7.07e+04 loss=1.2683e+00 ppl=3.55
Validation - loss=2.9401e+00 ppl=18.92 best_loss=2.9055e+00 best_ppl=18.27
Epoch 67 - |param|=2.14e+03 |g_param|=6.87e+04 loss=1.2085e+00 ppl=3.35
Validation - loss=2.9350e+00 ppl=18.82 best_loss=2.9055e+00 best_ppl=18.27
Epoch 68 - |param|=2.14e+03 |g_param|=6.81e+04 loss=1.2431e+00 ppl=3.47
Validation - loss=2.9317e+00 ppl=18.76 best_loss=2.9055e+00 best_ppl=18.27
Epoch 69 - |param|=2.14e+03 |g_param|=8.98e+04 loss=1.2547e+00 ppl=3.51
Validation - loss=2.9359e+00 ppl=18.84 best_loss=2.9055e+00 best_ppl=18.27
Epoch 70 - |param|=2.14e+03 |g_param|=7.84e+04 loss=1.2650e+00 ppl=3.54
Validation - loss=2.9339e+00 ppl=18.80 best_loss=2.9055e+00 best_ppl=18.27
Epoch 71 - |param|=2.14e+03 |g_param|=6.72e+04 loss=1.1597e+00 ppl=3.19
Validation - loss=2.9161e+00 ppl=18.47 best_loss=2.9055e+00 best_ppl=18.27
Epoch 72 - |param|=2.14e+03 |g_param|=7.36e+04 loss=1.1713e+00 ppl=3.23
Validation - loss=2.9372e+00 ppl=18.86 best_loss=2.9055e+00 best_ppl=18.27
Epoch 73 - |param|=2.14e+03 |g_param|=8.44e+04 loss=1.2107e+00 ppl=3.36
Validation - loss=2.9435e+00 ppl=18.98 best_loss=2.9055e+00 best_ppl=18.27
Epoch 74 - |param|=2.14e+03 |g_param|=8.41e+04 loss=1.1696e+00 ppl=3.22
Validation - loss=2.9568e+00 ppl=19.24 best_loss=2.9055e+00 best_ppl=18.27
Epoch 75 - |param|=2.14e+03 |g_param|=6.62e+04 loss=1.1004e+00 ppl=3.01
Validation - loss=2.9367e+00 ppl=18.85 best_loss=2.9055e+00 best_ppl=18.27
Epoch 76 - |param|=2.14e+03 |g_param|=6.53e+04 loss=1.0795e+00 ppl=2.94
Validation - loss=2.9618e+00 ppl=19.33 best_loss=2.9055e+00 best_ppl=18.27
Epoch 77 - |param|=2.15e+03 |g_param|=6.96e+04 loss=1.0907e+00 ppl=2.98
Validation - loss=2.9327e+00 ppl=18.78 best_loss=2.9055e+00 best_ppl=18.27
Epoch 78 - |param|=2.15e+03 |g_param|=7.72e+04 loss=1.1199e+00 ppl=3.06
Validation - loss=2.9473e+00 ppl=19.05 best_loss=2.9055e+00 best_ppl=18.27
Epoch 79 - |param|=2.15e+03 |g_param|=6.51e+04 loss=1.0667e+00 ppl=2.91
Validation - loss=2.9468e+00 ppl=19.04 best_loss=2.9055e+00 best_ppl=18.27
Epoch 80 - |param|=2.15e+03 |g_param|=8.02e+04 loss=1.0481e+00 ppl=2.85
Validation - loss=2.9379e+00 ppl=18.88 best_loss=2.9055e+00 best_ppl=18.27
Epoch 81 - |param|=2.15e+03 |g_param|=1.42e+05 loss=1.0579e+00 ppl=2.88
Validation - loss=2.9587e+00 ppl=19.27 best_loss=2.9055e+00 best_ppl=18.27
Epoch 82 - |param|=2.15e+03 |g_param|=9.07e+04 loss=1.0457e+00 ppl=2.85
Validation - loss=2.9488e+00 ppl=19.08 best_loss=2.9055e+00 best_ppl=18.27
Epoch 83 - |param|=2.15e+03 |g_param|=7.39e+04 loss=9.8304e-01 ppl=2.67
Validation - loss=2.9883e+00 ppl=19.85 best_loss=2.9055e+00 best_ppl=18.27
Epoch 84 - |param|=2.15e+03 |g_param|=8.07e+04 loss=1.0303e+00 ppl=2.80
Validation - loss=2.9755e+00 ppl=19.60 best_loss=2.9055e+00 best_ppl=18.27
Epoch 85 - |param|=2.15e+03 |g_param|=7.34e+04 loss=9.6454e-01 ppl=2.62
Validation - loss=2.9709e+00 ppl=19.51 best_loss=2.9055e+00 best_ppl=18.27
Epoch 86 - |param|=2.15e+03 |g_param|=1.08e+05 loss=1.0653e+00 ppl=2.90
Validation - loss=3.0012e+00 ppl=20.11 best_loss=2.9055e+00 best_ppl=18.27
Epoch 87 - |param|=2.15e+03 |g_param|=6.73e+04 loss=9.5830e-01 ppl=2.61
Validation - loss=2.9805e+00 ppl=19.70 best_loss=2.9055e+00 best_ppl=18.27
Epoch 88 - |param|=2.15e+03 |g_param|=8.31e+04 loss=9.4861e-01 ppl=2.58
Validation - loss=2.9742e+00 ppl=19.57 best_loss=2.9055e+00 best_ppl=18.27
Epoch 89 - |param|=2.15e+03 |g_param|=8.32e+04 loss=9.8714e-01 ppl=2.68
Validation - loss=2.9898e+00 ppl=19.88 best_loss=2.9055e+00 best_ppl=18.27
Epoch 90 - |param|=2.16e+03 |g_param|=8.08e+04 loss=9.1964e-01 ppl=2.51
Validation - loss=2.9944e+00 ppl=19.97 best_loss=2.9055e+00 best_ppl=18.27
Epoch 91 - |param|=2.16e+03 |g_param|=6.81e+04 loss=9.3242e-01 ppl=2.54
Validation - loss=2.9795e+00 ppl=19.68 best_loss=2.9055e+00 best_ppl=18.27
Epoch 92 - |param|=2.16e+03 |g_param|=8.02e+04 loss=9.1703e-01 ppl=2.50
Validation - loss=2.9887e+00 ppl=19.86 best_loss=2.9055e+00 best_ppl=18.27
Epoch 93 - |param|=2.16e+03 |g_param|=4.84e+04 loss=9.2775e-01 ppl=2.53
Validation - loss=2.9775e+00 ppl=19.64 best_loss=2.9055e+00 best_ppl=18.27
Epoch 94 - |param|=2.16e+03 |g_param|=4.06e+04 loss=9.0591e-01 ppl=2.47
Validation - loss=3.0290e+00 ppl=20.68 best_loss=2.9055e+00 best_ppl=18.27
Epoch 95 - |param|=2.16e+03 |g_param|=3.94e+04 loss=9.0814e-01 ppl=2.48
Validation - loss=3.0254e+00 ppl=20.60 best_loss=2.9055e+00 best_ppl=18.27
Epoch 96 - |param|=2.16e+03 |g_param|=4.20e+04 loss=8.9576e-01 ppl=2.45
Validation - loss=3.0097e+00 ppl=20.28 best_loss=2.9055e+00 best_ppl=18.27
Epoch 97 - |param|=2.16e+03 |g_param|=3.66e+04 loss=8.4677e-01 ppl=2.33
Validation - loss=3.0066e+00 ppl=20.22 best_loss=2.9055e+00 best_ppl=18.27
Epoch 98 - |param|=2.16e+03 |g_param|=4.77e+04 loss=8.9488e-01 ppl=2.45
Validation - loss=3.0168e+00 ppl=20.43 best_loss=2.9055e+00 best_ppl=18.27
Epoch 99 - |param|=2.16e+03 |g_param|=3.71e+04 loss=8.7513e-01 ppl=2.40
Validation - loss=3.0043e+00 ppl=20.17 best_loss=2.9055e+00 best_ppl=18.27
Epoch 100 - |param|=2.16e+03 |g_param|=3.79e+04 loss=8.2313e-01 ppl=2.28
Validation - loss=3.0264e+00 ppl=20.62 best_loss=2.9055e+00 best_ppl=18.27
Epoch 101 - |param|=2.16e+03 |g_param|=4.34e+04 loss=8.4989e-01 ppl=2.34
Validation - loss=3.0101e+00 ppl=20.29 best_loss=2.9055e+00 best_ppl=18.27
Epoch 102 - |param|=2.17e+03 |g_param|=3.63e+04 loss=7.7781e-01 ppl=2.18
Validation - loss=3.0269e+00 ppl=20.63 best_loss=2.9055e+00 best_ppl=18.27
Epoch 103 - |param|=2.17e+03 |g_param|=5.79e+04 loss=8.6495e-01 ppl=2.37
Validation - loss=3.1252e+00 ppl=22.76 best_loss=2.9055e+00 best_ppl=18.27
Epoch 104 - |param|=2.17e+03 |g_param|=4.28e+04 loss=8.6409e-01 ppl=2.37
Validation - loss=3.0258e+00 ppl=20.61 best_loss=2.9055e+00 best_ppl=18.27
Epoch 105 - |param|=2.17e+03 |g_param|=3.82e+04 loss=8.1037e-01 ppl=2.25
Validation - loss=3.0098e+00 ppl=20.28 best_loss=2.9055e+00 best_ppl=18.27
Epoch 106 - |param|=2.17e+03 |g_param|=4.00e+04 loss=7.9196e-01 ppl=2.21
Validation - loss=3.0132e+00 ppl=20.35 best_loss=2.9055e+00 best_ppl=18.27
Epoch 107 - |param|=2.17e+03 |g_param|=3.77e+04 loss=7.8189e-01 ppl=2.19
Validation - loss=3.0323e+00 ppl=20.74 best_loss=2.9055e+00 best_ppl=18.27
Epoch 108 - |param|=2.17e+03 |g_param|=3.76e+04 loss=7.8393e-01 ppl=2.19
Validation - loss=3.0476e+00 ppl=21.06 best_loss=2.9055e+00 best_ppl=18.27
Epoch 109 - |param|=2.17e+03 |g_param|=6.55e+04 loss=7.5391e-01 ppl=2.13
Validation - loss=3.0499e+00 ppl=21.11 best_loss=2.9055e+00 best_ppl=18.27
Epoch 110 - |param|=2.17e+03 |g_param|=7.82e+04 loss=7.6979e-01 ppl=2.16
Validation - loss=3.0423e+00 ppl=20.95 best_loss=2.9055e+00 best_ppl=18.27
Epoch 111 - |param|=2.17e+03 |g_param|=6.33e+04 loss=6.9617e-01 ppl=2.01
Validation - loss=3.0803e+00 ppl=21.77 best_loss=2.9055e+00 best_ppl=18.27
Epoch 112 - |param|=2.17e+03 |g_param|=6.68e+04 loss=7.2668e-01 ppl=2.07
Validation - loss=3.0552e+00 ppl=21.23 best_loss=2.9055e+00 best_ppl=18.27
Epoch 113 - |param|=2.17e+03 |g_param|=7.38e+04 loss=7.3036e-01 ppl=2.08
Validation - loss=3.0633e+00 ppl=21.40 best_loss=2.9055e+00 best_ppl=18.27
Epoch 114 - |param|=2.17e+03 |g_param|=7.80e+04 loss=7.4300e-01 ppl=2.10
Validation - loss=3.0685e+00 ppl=21.51 best_loss=2.9055e+00 best_ppl=18.27
Epoch 115 - |param|=2.18e+03 |g_param|=7.14e+04 loss=7.1226e-01 ppl=2.04
Validation - loss=3.0436e+00 ppl=20.98 best_loss=2.9055e+00 best_ppl=18.27
Epoch 116 - |param|=2.18e+03 |g_param|=8.47e+04 loss=7.3309e-01 ppl=2.08
Validation - loss=3.0676e+00 ppl=21.49 best_loss=2.9055e+00 best_ppl=18.27
Epoch 117 - |param|=2.18e+03 |g_param|=7.61e+04 loss=7.2015e-01 ppl=2.05
Validation - loss=3.0679e+00 ppl=21.50 best_loss=2.9055e+00 best_ppl=18.27
Epoch 118 - |param|=2.18e+03 |g_param|=7.40e+04 loss=7.1045e-01 ppl=2.03
Validation - loss=3.0823e+00 ppl=21.81 best_loss=2.9055e+00 best_ppl=18.27
Epoch 119 - |param|=2.18e+03 |g_param|=7.82e+04 loss=6.9540e-01 ppl=2.00
Validation - loss=3.0691e+00 ppl=21.52 best_loss=2.9055e+00 best_ppl=18.27
Epoch 120 - |param|=2.18e+03 |g_param|=7.32e+04 loss=6.8059e-01 ppl=1.98
Validation - loss=3.0760e+00 ppl=21.67 best_loss=2.9055e+00 best_ppl=18.27
Epoch 121 - |param|=2.18e+03 |g_param|=7.62e+04 loss=6.6139e-01 ppl=1.94
Validation - loss=3.1164e+00 ppl=22.57 best_loss=2.9055e+00 best_ppl=18.27
Epoch 122 - |param|=2.18e+03 |g_param|=6.95e+04 loss=6.8422e-01 ppl=1.98
Validation - loss=3.0758e+00 ppl=21.67 best_loss=2.9055e+00 best_ppl=18.27
Epoch 123 - |param|=2.18e+03 |g_param|=9.54e+04 loss=6.9209e-01 ppl=2.00
Validation - loss=3.0918e+00 ppl=22.02 best_loss=2.9055e+00 best_ppl=18.27
Epoch 124 - |param|=2.18e+03 |g_param|=8.02e+04 loss=6.6230e-01 ppl=1.94
Validation - loss=3.0932e+00 ppl=22.05 best_loss=2.9055e+00 best_ppl=18.27
Epoch 125 - |param|=2.18e+03 |g_param|=1.56e+05 loss=6.3192e-01 ppl=1.88
Validation - loss=3.1027e+00 ppl=22.26 best_loss=2.9055e+00 best_ppl=18.27
Epoch 126 - |param|=2.18e+03 |g_param|=9.55e+04 loss=6.3174e-01 ppl=1.88
Validation - loss=3.0951e+00 ppl=22.09 best_loss=2.9055e+00 best_ppl=18.27
Epoch 127 - |param|=2.18e+03 |g_param|=7.09e+04 loss=6.2802e-01 ppl=1.87
Validation - loss=3.1018e+00 ppl=22.24 best_loss=2.9055e+00 best_ppl=18.27
Epoch 128 - |param|=2.18e+03 |g_param|=7.83e+04 loss=6.4466e-01 ppl=1.91
Validation - loss=3.1167e+00 ppl=22.57 best_loss=2.9055e+00 best_ppl=18.27
Epoch 129 - |param|=2.19e+03 |g_param|=9.05e+04 loss=6.3706e-01 ppl=1.89
Validation - loss=3.1202e+00 ppl=22.65 best_loss=2.9055e+00 best_ppl=18.27
Epoch 130 - |param|=2.19e+03 |g_param|=7.63e+04 loss=6.2422e-01 ppl=1.87
Validation - loss=3.1344e+00 ppl=22.98 best_loss=2.9055e+00 best_ppl=18.27
Epoch 131 - |param|=2.19e+03 |g_param|=7.71e+04 loss=6.3889e-01 ppl=1.89
Validation - loss=3.1240e+00 ppl=22.74 best_loss=2.9055e+00 best_ppl=18.27
Epoch 132 - |param|=2.19e+03 |g_param|=7.15e+04 loss=6.0352e-01 ppl=1.83
Validation - loss=3.1207e+00 ppl=22.66 best_loss=2.9055e+00 best_ppl=18.27
Epoch 133 - |param|=2.19e+03 |g_param|=6.92e+04 loss=5.8576e-01 ppl=1.80
Validation - loss=3.1303e+00 ppl=22.88 best_loss=2.9055e+00 best_ppl=18.27
Epoch 134 - |param|=2.19e+03 |g_param|=8.90e+04 loss=6.1512e-01 ppl=1.85
Validation - loss=3.1504e+00 ppl=23.35 best_loss=2.9055e+00 best_ppl=18.27
Epoch 135 - |param|=2.19e+03 |g_param|=8.91e+04 loss=6.2975e-01 ppl=1.88
Validation - loss=3.2213e+00 ppl=25.06 best_loss=2.9055e+00 best_ppl=18.27
Epoch 136 - |param|=2.19e+03 |g_param|=8.15e+04 loss=6.0089e-01 ppl=1.82
Validation - loss=3.1484e+00 ppl=23.30 best_loss=2.9055e+00 best_ppl=18.27
Epoch 137 - |param|=2.19e+03 |g_param|=6.68e+04 loss=5.8228e-01 ppl=1.79
Validation - loss=3.1169e+00 ppl=22.58 best_loss=2.9055e+00 best_ppl=18.27
Epoch 138 - |param|=2.19e+03 |g_param|=7.67e+04 loss=5.9373e-01 ppl=1.81
Validation - loss=3.1428e+00 ppl=23.17 best_loss=2.9055e+00 best_ppl=18.27
Epoch 139 - |param|=2.19e+03 |g_param|=7.54e+04 loss=5.7218e-01 ppl=1.77
Validation - loss=3.1527e+00 ppl=23.40 best_loss=2.9055e+00 best_ppl=18.27
Epoch 140 - |param|=2.19e+03 |g_param|=7.42e+04 loss=5.7289e-01 ppl=1.77
Validation - loss=3.1297e+00 ppl=22.87 best_loss=2.9055e+00 best_ppl=18.27
Epoch 141 - |param|=2.19e+03 |g_param|=6.70e+04 loss=5.5849e-01 ppl=1.75
Validation - loss=3.1355e+00 ppl=23.00 best_loss=2.9055e+00 best_ppl=18.27
Epoch 142 - |param|=2.20e+03 |g_param|=1.69e+05 loss=5.7893e-01 ppl=1.78
Validation - loss=3.1805e+00 ppl=24.06 best_loss=2.9055e+00 best_ppl=18.27
Epoch 143 - |param|=2.20e+03 |g_param|=7.09e+04 loss=5.4406e-01 ppl=1.72
Validation - loss=3.1677e+00 ppl=23.75 best_loss=2.9055e+00 best_ppl=18.27
Epoch 144 - |param|=2.20e+03 |g_param|=6.96e+04 loss=5.0248e-01 ppl=1.65
Validation - loss=3.1508e+00 ppl=23.35 best_loss=2.9055e+00 best_ppl=18.27
Epoch 145 - |param|=2.20e+03 |g_param|=7.77e+04 loss=5.6535e-01 ppl=1.76
Validation - loss=3.1665e+00 ppl=23.72 best_loss=2.9055e+00 best_ppl=18.27
Epoch 146 - |param|=2.20e+03 |g_param|=6.71e+04 loss=5.2250e-01 ppl=1.69
Validation - loss=3.1750e+00 ppl=23.93 best_loss=2.9055e+00 best_ppl=18.27
Epoch 147 - |param|=2.20e+03 |g_param|=8.18e+04 loss=5.3454e-01 ppl=1.71
Validation - loss=3.1679e+00 ppl=23.76 best_loss=2.9055e+00 best_ppl=18.27
Epoch 148 - |param|=2.20e+03 |g_param|=8.65e+04 loss=5.4421e-01 ppl=1.72
Validation - loss=3.1990e+00 ppl=24.51 best_loss=2.9055e+00 best_ppl=18.27
Epoch 149 - |param|=2.20e+03 |g_param|=7.30e+04 loss=5.3530e-01 ppl=1.71
Validation - loss=3.1926e+00 ppl=24.35 best_loss=2.9055e+00 best_ppl=18.27
Epoch 150 - |param|=2.20e+03 |g_param|=7.07e+04 loss=5.1718e-01 ppl=1.68
Validation - loss=3.1777e+00 ppl=23.99 best_loss=2.9055e+00 best_ppl=18.27
Epoch 151 - |param|=2.20e+03 |g_param|=6.56e+04 loss=5.1636e-01 ppl=1.68
Validation - loss=3.1858e+00 ppl=24.19 best_loss=2.9055e+00 best_ppl=18.27
Epoch 152 - |param|=2.20e+03 |g_param|=8.99e+04 loss=5.1340e-01 ppl=1.67
Validation - loss=3.1816e+00 ppl=24.09 best_loss=2.9055e+00 best_ppl=18.27
Epoch 153 - |param|=2.20e+03 |g_param|=7.40e+04 loss=5.1776e-01 ppl=1.68
Validation - loss=3.1779e+00 ppl=24.00 best_loss=2.9055e+00 best_ppl=18.27
Epoch 154 - |param|=2.20e+03 |g_param|=7.14e+04 loss=5.0378e-01 ppl=1.65
Validation - loss=3.1883e+00 ppl=24.25 best_loss=2.9055e+00 best_ppl=18.27
Epoch 155 - |param|=2.20e+03 |g_param|=7.20e+04 loss=4.9324e-01 ppl=1.64
Validation - loss=3.1785e+00 ppl=24.01 best_loss=2.9055e+00 best_ppl=18.27
Epoch 156 - |param|=2.21e+03 |g_param|=6.80e+04 loss=4.7982e-01 ppl=1.62
Validation - loss=3.1941e+00 ppl=24.39 best_loss=2.9055e+00 best_ppl=18.27
Epoch 157 - |param|=2.21e+03 |g_param|=6.67e+04 loss=4.8017e-01 ppl=1.62
Validation - loss=3.2050e+00 ppl=24.66 best_loss=2.9055e+00 best_ppl=18.27
Epoch 158 - |param|=2.21e+03 |g_param|=7.73e+04 loss=4.8328e-01 ppl=1.62
Validation - loss=3.2215e+00 ppl=25.07 best_loss=2.9055e+00 best_ppl=18.27
Epoch 159 - |param|=2.21e+03 |g_param|=6.97e+04 loss=4.7128e-01 ppl=1.60
Validation - loss=3.2067e+00 ppl=24.70 best_loss=2.9055e+00 best_ppl=18.27
Epoch 160 - |param|=2.21e+03 |g_param|=7.41e+04 loss=4.9441e-01 ppl=1.64
Validation - loss=3.2011e+00 ppl=24.56 best_loss=2.9055e+00 best_ppl=18.27
Epoch 161 - |param|=2.21e+03 |g_param|=6.85e+04 loss=4.7309e-01 ppl=1.60
Validation - loss=3.2499e+00 ppl=25.79 best_loss=2.9055e+00 best_ppl=18.27
Epoch 162 - |param|=2.21e+03 |g_param|=9.43e+04 loss=5.0513e-01 ppl=1.66
Validation - loss=3.2437e+00 ppl=25.63 best_loss=2.9055e+00 best_ppl=18.27
Epoch 163 - |param|=2.21e+03 |g_param|=6.68e+04 loss=4.6609e-01 ppl=1.59
Validation - loss=3.2355e+00 ppl=25.42 best_loss=2.9055e+00 best_ppl=18.27
Epoch 164 - |param|=2.21e+03 |g_param|=7.72e+04 loss=4.6873e-01 ppl=1.60
Validation - loss=3.2364e+00 ppl=25.44 best_loss=2.9055e+00 best_ppl=18.27
Epoch 165 - |param|=2.21e+03 |g_param|=8.33e+04 loss=4.8588e-01 ppl=1.63
Validation - loss=3.2568e+00 ppl=25.97 best_loss=2.9055e+00 best_ppl=18.27
Epoch 166 - |param|=2.21e+03 |g_param|=6.95e+04 loss=4.3521e-01 ppl=1.55
Validation - loss=3.2412e+00 ppl=25.56 best_loss=2.9055e+00 best_ppl=18.27
Epoch 167 - |param|=2.21e+03 |g_param|=8.05e+04 loss=4.7859e-01 ppl=1.61
Validation - loss=3.2687e+00 ppl=26.28 best_loss=2.9055e+00 best_ppl=18.27
Epoch 168 - |param|=2.21e+03 |g_param|=9.42e+04 loss=4.9870e-01 ppl=1.65
Validation - loss=3.2507e+00 ppl=25.81 best_loss=2.9055e+00 best_ppl=18.27
Epoch 169 - |param|=2.21e+03 |g_param|=8.14e+04 loss=4.5312e-01 ppl=1.57
Validation - loss=3.2549e+00 ppl=25.92 best_loss=2.9055e+00 best_ppl=18.27
Epoch 170 - |param|=2.21e+03 |g_param|=7.02e+04 loss=4.5132e-01 ppl=1.57
Validation - loss=3.2653e+00 ppl=26.19 best_loss=2.9055e+00 best_ppl=18.27
Epoch 171 - |param|=2.22e+03 |g_param|=7.20e+04 loss=4.5814e-01 ppl=1.58
Validation - loss=3.2533e+00 ppl=25.88 best_loss=2.9055e+00 best_ppl=18.27
Epoch 172 - |param|=2.22e+03 |g_param|=7.86e+04 loss=4.4739e-01 ppl=1.56
Validation - loss=3.2451e+00 ppl=25.66 best_loss=2.9055e+00 best_ppl=18.27
Epoch 173 - |param|=2.22e+03 |g_param|=7.53e+04 loss=4.3405e-01 ppl=1.54
Validation - loss=3.2647e+00 ppl=26.17 best_loss=2.9055e+00 best_ppl=18.27
Epoch 174 - |param|=2.22e+03 |g_param|=7.95e+04 loss=4.4393e-01 ppl=1.56
Validation - loss=3.2797e+00 ppl=26.57 best_loss=2.9055e+00 best_ppl=18.27
Epoch 175 - |param|=2.22e+03 |g_param|=1.50e+05 loss=4.2976e-01 ppl=1.54
Validation - loss=3.3010e+00 ppl=27.14 best_loss=2.9055e+00 best_ppl=18.27
Epoch 176 - |param|=2.22e+03 |g_param|=1.42e+05 loss=4.4579e-01 ppl=1.56
Validation - loss=3.2875e+00 ppl=26.77 best_loss=2.9055e+00 best_ppl=18.27
Epoch 177 - |param|=2.22e+03 |g_param|=6.84e+04 loss=4.1055e-01 ppl=1.51
Validation - loss=3.3021e+00 ppl=27.17 best_loss=2.9055e+00 best_ppl=18.27
Epoch 178 - |param|=2.22e+03 |g_param|=3.72e+04 loss=4.3816e-01 ppl=1.55
Validation - loss=3.2879e+00 ppl=26.79 best_loss=2.9055e+00 best_ppl=18.27
Epoch 179 - |param|=2.22e+03 |g_param|=3.53e+04 loss=4.1204e-01 ppl=1.51
Validation - loss=3.2944e+00 ppl=26.96 best_loss=2.9055e+00 best_ppl=18.27
Epoch 180 - |param|=2.22e+03 |g_param|=3.34e+04 loss=4.1378e-01 ppl=1.51
Validation - loss=3.2889e+00 ppl=26.81 best_loss=2.9055e+00 best_ppl=18.27
Epoch 181 - |param|=2.22e+03 |g_param|=3.34e+04 loss=3.9694e-01 ppl=1.49
Validation - loss=3.3037e+00 ppl=27.21 best_loss=2.9055e+00 best_ppl=18.27
Epoch 182 - |param|=2.22e+03 |g_param|=3.54e+04 loss=3.9668e-01 ppl=1.49
Validation - loss=3.3090e+00 ppl=27.36 best_loss=2.9055e+00 best_ppl=18.27
Epoch 183 - |param|=2.22e+03 |g_param|=3.51e+04 loss=4.1388e-01 ppl=1.51
Validation - loss=3.3183e+00 ppl=27.61 best_loss=2.9055e+00 best_ppl=18.27
Epoch 184 - |param|=2.22e+03 |g_param|=3.73e+04 loss=4.0945e-01 ppl=1.51
Validation - loss=3.3223e+00 ppl=27.72 best_loss=2.9055e+00 best_ppl=18.27
Epoch 185 - |param|=2.22e+03 |g_param|=3.26e+04 loss=3.9583e-01 ppl=1.49
Validation - loss=3.3223e+00 ppl=27.72 best_loss=2.9055e+00 best_ppl=18.27
Epoch 186 - |param|=2.23e+03 |g_param|=3.73e+04 loss=3.9897e-01 ppl=1.49
Validation - loss=3.3116e+00 ppl=27.43 best_loss=2.9055e+00 best_ppl=18.27
Epoch 187 - |param|=2.23e+03 |g_param|=3.44e+04 loss=4.0216e-01 ppl=1.50
Validation - loss=3.3190e+00 ppl=27.63 best_loss=2.9055e+00 best_ppl=18.27
Epoch 188 - |param|=2.23e+03 |g_param|=3.73e+04 loss=3.9279e-01 ppl=1.48
Validation - loss=3.3349e+00 ppl=28.08 best_loss=2.9055e+00 best_ppl=18.27
Epoch 189 - |param|=2.23e+03 |g_param|=4.31e+04 loss=4.0378e-01 ppl=1.50
Validation - loss=3.3480e+00 ppl=28.45 best_loss=2.9055e+00 best_ppl=18.27
Epoch 190 - |param|=2.23e+03 |g_param|=4.23e+04 loss=3.9448e-01 ppl=1.48
Validation - loss=3.3399e+00 ppl=28.22 best_loss=2.9055e+00 best_ppl=18.27
Epoch 191 - |param|=2.23e+03 |g_param|=3.96e+04 loss=4.0254e-01 ppl=1.50
Validation - loss=3.3330e+00 ppl=28.02 best_loss=2.9055e+00 best_ppl=18.27
Epoch 192 - |param|=2.23e+03 |g_param|=3.42e+04 loss=4.0136e-01 ppl=1.49
Validation - loss=3.3263e+00 ppl=27.84 best_loss=2.9055e+00 best_ppl=18.27
Epoch 193 - |param|=2.23e+03 |g_param|=6.13e+04 loss=3.8970e-01 ppl=1.48
Validation - loss=3.3319e+00 ppl=27.99 best_loss=2.9055e+00 best_ppl=18.27
Epoch 194 - |param|=2.23e+03 |g_param|=7.08e+04 loss=3.7676e-01 ppl=1.46
Validation - loss=3.3545e+00 ppl=28.63 best_loss=2.9055e+00 best_ppl=18.27
Epoch 195 - |param|=2.23e+03 |g_param|=7.81e+04 loss=4.0061e-01 ppl=1.49
Validation - loss=3.3531e+00 ppl=28.59 best_loss=2.9055e+00 best_ppl=18.27
Epoch 196 - |param|=2.23e+03 |g_param|=6.66e+04 loss=3.5664e-01 ppl=1.43
Validation - loss=3.3444e+00 ppl=28.34 best_loss=2.9055e+00 best_ppl=18.27
Epoch 197 - |param|=2.23e+03 |g_param|=7.04e+04 loss=3.7821e-01 ppl=1.46
Validation - loss=3.3576e+00 ppl=28.72 best_loss=2.9055e+00 best_ppl=18.27
Epoch 198 - |param|=2.23e+03 |g_param|=7.01e+04 loss=3.5677e-01 ppl=1.43
Validation - loss=3.3603e+00 ppl=28.80 best_loss=2.9055e+00 best_ppl=18.27
Epoch 199 - |param|=2.23e+03 |g_param|=7.36e+04 loss=3.8534e-01 ppl=1.47
Validation - loss=3.3365e+00 ppl=28.12 best_loss=2.9055e+00 best_ppl=18.27
Epoch 200 - |param|=2.23e+03 |g_param|=6.63e+04 loss=3.6112e-01 ppl=1.43
Validation - loss=3.3605e+00 ppl=28.80 best_loss=2.9055e+00 best_ppl=18.27
Epoch 201 - |param|=2.24e+03 |g_param|=6.85e+04 loss=3.7125e-01 ppl=1.45
Validation - loss=3.3768e+00 ppl=29.28 best_loss=2.9055e+00 best_ppl=18.27
Epoch 202 - |param|=2.24e+03 |g_param|=7.33e+04 loss=3.6946e-01 ppl=1.45
Validation - loss=3.3686e+00 ppl=29.04 best_loss=2.9055e+00 best_ppl=18.27
Epoch 203 - |param|=2.24e+03 |g_param|=6.51e+04 loss=3.4949e-01 ppl=1.42
Validation - loss=3.3756e+00 ppl=29.24 best_loss=2.9055e+00 best_ppl=18.27
Epoch 204 - |param|=2.24e+03 |g_param|=6.96e+04 loss=3.5732e-01 ppl=1.43
Validation - loss=3.3935e+00 ppl=29.77 best_loss=2.9055e+00 best_ppl=18.27
Epoch 205 - |param|=2.24e+03 |g_param|=6.96e+04 loss=3.5877e-01 ppl=1.43
Validation - loss=3.4027e+00 ppl=30.05 best_loss=2.9055e+00 best_ppl=18.27
Epoch 206 - |param|=2.24e+03 |g_param|=6.72e+04 loss=3.3594e-01 ppl=1.40
Validation - loss=3.3816e+00 ppl=29.42 best_loss=2.9055e+00 best_ppl=18.27
Epoch 207 - |param|=2.24e+03 |g_param|=8.15e+04 loss=3.7931e-01 ppl=1.46
Validation - loss=3.3903e+00 ppl=29.67 best_loss=2.9055e+00 best_ppl=18.27
Epoch 208 - |param|=2.24e+03 |g_param|=7.50e+04 loss=3.4898e-01 ppl=1.42
Validation - loss=3.4146e+00 ppl=30.41 best_loss=2.9055e+00 best_ppl=18.27
Epoch 209 - |param|=2.24e+03 |g_param|=1.36e+05 loss=3.5865e-01 ppl=1.43
Validation - loss=3.3958e+00 ppl=29.84 best_loss=2.9055e+00 best_ppl=18.27
Epoch 210 - |param|=2.24e+03 |g_param|=1.57e+05 loss=3.4718e-01 ppl=1.42
Validation - loss=3.4110e+00 ppl=30.29 best_loss=2.9055e+00 best_ppl=18.27
Epoch 211 - |param|=2.24e+03 |g_param|=7.86e+04 loss=3.7575e-01 ppl=1.46
Validation - loss=3.4059e+00 ppl=30.14 best_loss=2.9055e+00 best_ppl=18.27
Epoch 212 - |param|=2.24e+03 |g_param|=6.72e+04 loss=3.5328e-01 ppl=1.42
Validation - loss=3.4035e+00 ppl=30.07 best_loss=2.9055e+00 best_ppl=18.27
Epoch 213 - |param|=2.24e+03 |g_param|=8.90e+04 loss=3.6710e-01 ppl=1.44
Validation - loss=3.4126e+00 ppl=30.34 best_loss=2.9055e+00 best_ppl=18.27
Epoch 214 - |param|=2.24e+03 |g_param|=7.07e+04 loss=3.3863e-01 ppl=1.40
Validation - loss=3.4138e+00 ppl=30.38 best_loss=2.9055e+00 best_ppl=18.27
Epoch 215 - |param|=2.24e+03 |g_param|=7.12e+04 loss=3.2426e-01 ppl=1.38
Validation - loss=3.4224e+00 ppl=30.64 best_loss=2.9055e+00 best_ppl=18.27
Epoch 216 - |param|=2.25e+03 |g_param|=6.62e+04 loss=3.3776e-01 ppl=1.40
Validation - loss=3.4144e+00 ppl=30.40 best_loss=2.9055e+00 best_ppl=18.27
Epoch 217 - |param|=2.25e+03 |g_param|=7.29e+04 loss=3.2132e-01 ppl=1.38
Validation - loss=3.4392e+00 ppl=31.16 best_loss=2.9055e+00 best_ppl=18.27
Epoch 218 - |param|=2.25e+03 |g_param|=7.31e+04 loss=3.3550e-01 ppl=1.40
Validation - loss=3.4182e+00 ppl=30.51 best_loss=2.9055e+00 best_ppl=18.27
Epoch 219 - |param|=2.25e+03 |g_param|=6.90e+04 loss=3.3136e-01 ppl=1.39
Validation - loss=3.4219e+00 ppl=30.63 best_loss=2.9055e+00 best_ppl=18.27
Epoch 220 - |param|=2.25e+03 |g_param|=6.71e+04 loss=3.1377e-01 ppl=1.37
Validation - loss=3.4305e+00 ppl=30.89 best_loss=2.9055e+00 best_ppl=18.27
Epoch 221 - |param|=2.25e+03 |g_param|=6.62e+04 loss=3.0071e-01 ppl=1.35
Validation - loss=3.4517e+00 ppl=31.55 best_loss=2.9055e+00 best_ppl=18.27
Epoch 222 - |param|=2.25e+03 |g_param|=7.81e+04 loss=3.3993e-01 ppl=1.40
Validation - loss=3.4580e+00 ppl=31.75 best_loss=2.9055e+00 best_ppl=18.27
Epoch 223 - |param|=2.25e+03 |g_param|=7.58e+04 loss=3.1953e-01 ppl=1.38
Validation - loss=3.4700e+00 ppl=32.14 best_loss=2.9055e+00 best_ppl=18.27
Epoch 224 - |param|=2.25e+03 |g_param|=7.22e+04 loss=3.3402e-01 ppl=1.40
Validation - loss=3.4426e+00 ppl=31.27 best_loss=2.9055e+00 best_ppl=18.27
Epoch 225 - |param|=2.25e+03 |g_param|=6.91e+04 loss=3.1490e-01 ppl=1.37
Validation - loss=3.4547e+00 ppl=31.65 best_loss=2.9055e+00 best_ppl=18.27
Epoch 226 - |param|=2.25e+03 |g_param|=7.93e+04 loss=3.0772e-01 ppl=1.36
Validation - loss=3.4357e+00 ppl=31.05 best_loss=2.9055e+00 best_ppl=18.27
Epoch 227 - |param|=2.25e+03 |g_param|=7.94e+04 loss=3.2702e-01 ppl=1.39
Validation - loss=3.4645e+00 ppl=31.96 best_loss=2.9055e+00 best_ppl=18.27
Epoch 228 - |param|=2.25e+03 |g_param|=7.58e+04 loss=3.1941e-01 ppl=1.38
Validation - loss=3.4341e+00 ppl=31.00 best_loss=2.9055e+00 best_ppl=18.27
Epoch 229 - |param|=2.25e+03 |g_param|=8.13e+04 loss=3.3643e-01 ppl=1.40
Validation - loss=3.4632e+00 ppl=31.92 best_loss=2.9055e+00 best_ppl=18.27
Epoch 230 - |param|=2.25e+03 |g_param|=6.50e+04 loss=3.0611e-01 ppl=1.36
Validation - loss=3.4563e+00 ppl=31.70 best_loss=2.9055e+00 best_ppl=18.27
Epoch 231 - |param|=2.25e+03 |g_param|=7.07e+04 loss=3.0885e-01 ppl=1.36
Validation - loss=3.4643e+00 ppl=31.95 best_loss=2.9055e+00 best_ppl=18.27
Epoch 232 - |param|=2.26e+03 |g_param|=7.25e+04 loss=3.1418e-01 ppl=1.37
Validation - loss=3.4702e+00 ppl=32.14 best_loss=2.9055e+00 best_ppl=18.27
Epoch 233 - |param|=2.26e+03 |g_param|=7.77e+04 loss=3.1078e-01 ppl=1.36
Validation - loss=3.4800e+00 ppl=32.46 best_loss=2.9055e+00 best_ppl=18.27
Epoch 234 - |param|=2.26e+03 |g_param|=7.42e+04 loss=3.0717e-01 ppl=1.36
Validation - loss=3.4817e+00 ppl=32.52 best_loss=2.9055e+00 best_ppl=18.27
Epoch 235 - |param|=2.26e+03 |g_param|=6.29e+04 loss=2.8369e-01 ppl=1.33
Validation - loss=3.4952e+00 ppl=32.96 best_loss=2.9055e+00 best_ppl=18.27
Epoch 236 - |param|=2.26e+03 |g_param|=6.39e+04 loss=2.8679e-01 ppl=1.33
Validation - loss=3.4924e+00 ppl=32.87 best_loss=2.9055e+00 best_ppl=18.27
Epoch 237 - |param|=2.26e+03 |g_param|=7.05e+04 loss=3.2065e-01 ppl=1.38
Validation - loss=3.4932e+00 ppl=32.89 best_loss=2.9055e+00 best_ppl=18.27
Epoch 238 - |param|=2.26e+03 |g_param|=6.88e+04 loss=2.9559e-01 ppl=1.34
Validation - loss=3.4900e+00 ppl=32.79 best_loss=2.9055e+00 best_ppl=18.27
Epoch 239 - |param|=2.26e+03 |g_param|=6.43e+04 loss=2.8511e-01 ppl=1.33
Validation - loss=3.4898e+00 ppl=32.78 best_loss=2.9055e+00 best_ppl=18.27
Epoch 240 - |param|=2.26e+03 |g_param|=7.84e+04 loss=3.1622e-01 ppl=1.37
Validation - loss=3.4928e+00 ppl=32.88 best_loss=2.9055e+00 best_ppl=18.27
Epoch 241 - |param|=2.26e+03 |g_param|=7.01e+04 loss=3.0659e-01 ppl=1.36
Validation - loss=3.5256e+00 ppl=33.97 best_loss=2.9055e+00 best_ppl=18.27
Epoch 242 - |param|=2.26e+03 |g_param|=1.47e+05 loss=2.9244e-01 ppl=1.34
Validation - loss=3.4873e+00 ppl=32.70 best_loss=2.9055e+00 best_ppl=18.27
Epoch 243 - |param|=2.26e+03 |g_param|=1.37e+05 loss=2.8760e-01 ppl=1.33
Validation - loss=3.4920e+00 ppl=32.85 best_loss=2.9055e+00 best_ppl=18.27
Epoch 244 - |param|=2.26e+03 |g_param|=1.36e+05 loss=2.7305e-01 ppl=1.31
Validation - loss=3.5035e+00 ppl=33.23 best_loss=2.9055e+00 best_ppl=18.27
Epoch 245 - |param|=2.26e+03 |g_param|=1.37e+05 loss=2.7596e-01 ppl=1.32
Validation - loss=3.5062e+00 ppl=33.32 best_loss=2.9055e+00 best_ppl=18.27
Epoch 246 - |param|=2.26e+03 |g_param|=1.29e+05 loss=2.7617e-01 ppl=1.32
Validation - loss=3.5495e+00 ppl=34.79 best_loss=2.9055e+00 best_ppl=18.27
Epoch 247 - |param|=2.26e+03 |g_param|=1.53e+05 loss=2.9032e-01 ppl=1.34
Validation - loss=3.5171e+00 ppl=33.69 best_loss=2.9055e+00 best_ppl=18.27
Epoch 248 - |param|=2.27e+03 |g_param|=1.43e+05 loss=2.8575e-01 ppl=1.33
Validation - loss=3.5584e+00 ppl=35.11 best_loss=2.9055e+00 best_ppl=18.27
Epoch 249 - |param|=2.27e+03 |g_param|=1.32e+05 loss=2.8371e-01 ppl=1.33
Validation - loss=3.5230e+00 ppl=33.89 best_loss=2.9055e+00 best_ppl=18.27
Epoch 250 - |param|=2.27e+03 |g_param|=8.55e+04 loss=2.8030e-01 ppl=1.32
Validation - loss=3.5220e+00 ppl=33.85 best_loss=2.9055e+00 best_ppl=18.27
Epoch 251 - |param|=2.27e+03 |g_param|=7.86e+04 loss=2.8557e-01 ppl=1.33
Validation - loss=3.6464e+00 ppl=38.34 best_loss=2.9055e+00 best_ppl=18.27
Epoch 252 - |param|=2.27e+03 |g_param|=7.14e+04 loss=2.7508e-01 ppl=1.32
Validation - loss=3.5327e+00 ppl=34.22 best_loss=2.9055e+00 best_ppl=18.27
Epoch 253 - |param|=2.27e+03 |g_param|=9.77e+04 loss=2.9459e-01 ppl=1.34
Validation - loss=3.5372e+00 ppl=34.37 best_loss=2.9055e+00 best_ppl=18.27
Epoch 254 - |param|=2.27e+03 |g_param|=7.00e+04 loss=2.7712e-01 ppl=1.32
Validation - loss=3.5432e+00 ppl=34.58 best_loss=2.9055e+00 best_ppl=18.27
Epoch 255 - |param|=2.27e+03 |g_param|=6.56e+04 loss=2.8917e-01 ppl=1.34
Validation - loss=3.5444e+00 ppl=34.62 best_loss=2.9055e+00 best_ppl=18.27
Epoch 256 - |param|=2.27e+03 |g_param|=7.19e+04 loss=2.6875e-01 ppl=1.31
Validation - loss=3.5571e+00 ppl=35.06 best_loss=2.9055e+00 best_ppl=18.27
Epoch 257 - |param|=2.27e+03 |g_param|=6.36e+04 loss=2.6591e-01 ppl=1.30
Validation - loss=3.5808e+00 ppl=35.90 best_loss=2.9055e+00 best_ppl=18.27
Epoch 258 - |param|=2.27e+03 |g_param|=6.81e+04 loss=2.5814e-01 ppl=1.29
Validation - loss=3.5708e+00 ppl=35.55 best_loss=2.9055e+00 best_ppl=18.27
Epoch 259 - |param|=2.27e+03 |g_param|=6.71e+04 loss=2.5863e-01 ppl=1.30
Validation - loss=3.5416e+00 ppl=34.52 best_loss=2.9055e+00 best_ppl=18.27
Epoch 260 - |param|=2.27e+03 |g_param|=7.35e+04 loss=2.8028e-01 ppl=1.32
Validation - loss=3.5483e+00 ppl=34.75 best_loss=2.9055e+00 best_ppl=18.27
Epoch 261 - |param|=2.27e+03 |g_param|=6.93e+04 loss=2.7970e-01 ppl=1.32
Validation - loss=3.5608e+00 ppl=35.19 best_loss=2.9055e+00 best_ppl=18.27
Epoch 262 - |param|=2.27e+03 |g_param|=6.72e+04 loss=2.5396e-01 ppl=1.29
Validation - loss=3.5671e+00 ppl=35.41 best_loss=2.9055e+00 best_ppl=18.27
Epoch 263 - |param|=2.27e+03 |g_param|=6.46e+04 loss=2.5357e-01 ppl=1.29
Validation - loss=3.5903e+00 ppl=36.25 best_loss=2.9055e+00 best_ppl=18.27
Epoch 264 - |param|=2.27e+03 |g_param|=7.91e+04 loss=2.9300e-01 ppl=1.34
Validation - loss=3.5889e+00 ppl=36.19 best_loss=2.9055e+00 best_ppl=18.27
Epoch 265 - |param|=2.28e+03 |g_param|=7.48e+04 loss=2.7372e-01 ppl=1.31
Validation - loss=3.5690e+00 ppl=35.48 best_loss=2.9055e+00 best_ppl=18.27
Epoch 266 - |param|=2.28e+03 |g_param|=1.39e+05 loss=2.6006e-01 ppl=1.30
Validation - loss=3.5762e+00 ppl=35.74 best_loss=2.9055e+00 best_ppl=18.27
Epoch 267 - |param|=2.28e+03 |g_param|=1.25e+05 loss=2.5535e-01 ppl=1.29
Validation - loss=3.5947e+00 ppl=36.40 best_loss=2.9055e+00 best_ppl=18.27
Epoch 268 - |param|=2.28e+03 |g_param|=1.28e+05 loss=2.4807e-01 ppl=1.28
Validation - loss=3.6004e+00 ppl=36.61 best_loss=2.9055e+00 best_ppl=18.27
Epoch 269 - |param|=2.28e+03 |g_param|=1.54e+05 loss=2.7087e-01 ppl=1.31
Validation - loss=3.6090e+00 ppl=36.93 best_loss=2.9055e+00 best_ppl=18.27
Epoch 270 - |param|=2.28e+03 |g_param|=1.36e+05 loss=2.3992e-01 ppl=1.27
Validation - loss=3.6182e+00 ppl=37.27 best_loss=2.9055e+00 best_ppl=18.27
Epoch 271 - |param|=2.28e+03 |g_param|=1.45e+05 loss=2.5532e-01 ppl=1.29
Validation - loss=3.6015e+00 ppl=36.65 best_loss=2.9055e+00 best_ppl=18.27
Epoch 272 - |param|=2.28e+03 |g_param|=1.59e+05 loss=2.6777e-01 ppl=1.31
Validation - loss=3.6413e+00 ppl=38.14 best_loss=2.9055e+00 best_ppl=18.27
Epoch 273 - |param|=2.28e+03 |g_param|=1.34e+05 loss=2.4011e-01 ppl=1.27
Validation - loss=3.6148e+00 ppl=37.14 best_loss=2.9055e+00 best_ppl=18.27
Epoch 274 - |param|=2.28e+03 |g_param|=9.02e+04 loss=2.5022e-01 ppl=1.28
Validation - loss=3.5940e+00 ppl=36.38 best_loss=2.9055e+00 best_ppl=18.27
Epoch 275 - |param|=2.28e+03 |g_param|=6.69e+04 loss=2.4381e-01 ppl=1.28
Validation - loss=3.6254e+00 ppl=37.54 best_loss=2.9055e+00 best_ppl=18.27
Epoch 276 - |param|=2.28e+03 |g_param|=6.73e+04 loss=2.4131e-01 ppl=1.27
Validation - loss=3.6509e+00 ppl=38.51 best_loss=2.9055e+00 best_ppl=18.27
Epoch 277 - |param|=2.28e+03 |g_param|=6.87e+04 loss=2.3666e-01 ppl=1.27
Validation - loss=3.6153e+00 ppl=37.16 best_loss=2.9055e+00 best_ppl=18.27
Epoch 278 - |param|=2.28e+03 |g_param|=9.45e+04 loss=2.6048e-01 ppl=1.30
Validation - loss=3.6394e+00 ppl=38.07 best_loss=2.9055e+00 best_ppl=18.27
Epoch 279 - |param|=2.28e+03 |g_param|=8.14e+04 loss=2.5924e-01 ppl=1.30
Validation - loss=3.6441e+00 ppl=38.25 best_loss=2.9055e+00 best_ppl=18.27
Epoch 280 - |param|=2.28e+03 |g_param|=8.21e+04 loss=2.5930e-01 ppl=1.30
Validation - loss=3.7098e+00 ppl=40.84 best_loss=2.9055e+00 best_ppl=18.27
Epoch 281 - |param|=2.28e+03 |g_param|=6.49e+04 loss=2.4772e-01 ppl=1.28
Validation - loss=3.6420e+00 ppl=38.17 best_loss=2.9055e+00 best_ppl=18.27
Epoch 282 - |param|=2.29e+03 |g_param|=6.85e+04 loss=2.3669e-01 ppl=1.27
Validation - loss=3.6472e+00 ppl=38.37 best_loss=2.9055e+00 best_ppl=18.27
Epoch 283 - |param|=2.29e+03 |g_param|=6.68e+04 loss=2.5336e-01 ppl=1.29
Validation - loss=3.6254e+00 ppl=37.54 best_loss=2.9055e+00 best_ppl=18.27
Epoch 284 - |param|=2.29e+03 |g_param|=5.71e+04 loss=2.2619e-01 ppl=1.25
Validation - loss=3.6553e+00 ppl=38.68 best_loss=2.9055e+00 best_ppl=18.27
Epoch 285 - |param|=2.29e+03 |g_param|=6.78e+04 loss=2.3797e-01 ppl=1.27
Validation - loss=3.6386e+00 ppl=38.04 best_loss=2.9055e+00 best_ppl=18.27
Epoch 286 - |param|=2.29e+03 |g_param|=8.25e+04 loss=2.6397e-01 ppl=1.30
Validation - loss=3.6448e+00 ppl=38.28 best_loss=2.9055e+00 best_ppl=18.27
Epoch 287 - |param|=2.29e+03 |g_param|=9.66e+04 loss=3.2191e-01 ppl=1.38
Validation - loss=3.7222e+00 ppl=41.36 best_loss=2.9055e+00 best_ppl=18.27
Epoch 288 - |param|=2.29e+03 |g_param|=6.95e+04 loss=2.3368e-01 ppl=1.26
Validation - loss=3.6601e+00 ppl=38.87 best_loss=2.9055e+00 best_ppl=18.27
Epoch 289 - |param|=2.29e+03 |g_param|=6.73e+04 loss=2.3733e-01 ppl=1.27
Validation - loss=3.6503e+00 ppl=38.49 best_loss=2.9055e+00 best_ppl=18.27
Epoch 290 - |param|=2.29e+03 |g_param|=1.24e+05 loss=2.2700e-01 ppl=1.25
Validation - loss=3.6381e+00 ppl=38.02 best_loss=2.9055e+00 best_ppl=18.27
Epoch 291 - |param|=2.29e+03 |g_param|=1.31e+05 loss=2.3089e-01 ppl=1.26
Validation - loss=3.6701e+00 ppl=39.26 best_loss=2.9055e+00 best_ppl=18.27
Epoch 292 - |param|=2.29e+03 |g_param|=1.23e+05 loss=2.0467e-01 ppl=1.23
Validation - loss=3.6880e+00 ppl=39.97 best_loss=2.9055e+00 best_ppl=18.27
Epoch 293 - |param|=2.29e+03 |g_param|=7.56e+04 loss=2.4110e-01 ppl=1.27
Validation - loss=3.6858e+00 ppl=39.88 best_loss=2.9055e+00 best_ppl=18.27
Epoch 294 - |param|=2.29e+03 |g_param|=7.38e+04 loss=2.4065e-01 ppl=1.27
Validation - loss=3.6911e+00 ppl=40.09 best_loss=2.9055e+00 best_ppl=18.27
Epoch 295 - |param|=2.29e+03 |g_param|=6.51e+04 loss=2.3615e-01 ppl=1.27
Validation - loss=3.6837e+00 ppl=39.79 best_loss=2.9055e+00 best_ppl=18.27
Epoch 296 - |param|=2.29e+03 |g_param|=4.25e+04 loss=2.2829e-01 ppl=1.26
Validation - loss=3.7059e+00 ppl=40.69 best_loss=2.9055e+00 best_ppl=18.27
Epoch 297 - |param|=2.29e+03 |g_param|=3.07e+04 loss=2.1703e-01 ppl=1.24
Validation - loss=3.6740e+00 ppl=39.41 best_loss=2.9055e+00 best_ppl=18.27
Epoch 298 - |param|=2.29e+03 |g_param|=3.21e+04 loss=2.1535e-01 ppl=1.24
Validation - loss=3.6903e+00 ppl=40.06 best_loss=2.9055e+00 best_ppl=18.27
Epoch 299 - |param|=2.29e+03 |g_param|=3.56e+04 loss=2.2659e-01 ppl=1.25
Validation - loss=3.7065e+00 ppl=40.71 best_loss=2.9055e+00 best_ppl=18.27
Epoch 300 - |param|=2.30e+03 |g_param|=3.38e+04 loss=2.2808e-01 ppl=1.26
Validation - loss=3.7000e+00 ppl=40.45 best_loss=2.9055e+00 best_ppl=18.27
```

training log for br-my:  

```
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'brmy',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/braille/seq2seq/br-my/seq-model-mybr.pth',
    'n_epochs': 300,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/media/ye/project2/exp/braille-nmt/data/for-nmt/0/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(16796, 128)
  (emb_dec): Embedding(17003, 128)
  (encoder): Encoder(
    (rnn): LSTM(128, 64, num_layers=4, batch_first=True, dropout=0.2, bidirectional=True)
  )
  (decoder): Decoder(
    (rnn): LSTM(256, 128, num_layers=4, batch_first=True, dropout=0.2)
  )
  (attn): Attention(
    (linear): Linear(in_features=128, out_features=128, bias=False)
    (softmax): Softmax(dim=-1)
  )
  (concat): Linear(in_features=256, out_features=128, bias=True)
  (tanh): Tanh()
  (generator): Generator(
    (output): Linear(in_features=128, out_features=17003, bias=True)
    (softmax): LogSoftmax(dim=-1)
  )
)
NLLLoss()
Adam (
Parameter Group 0
    amsgrad: False
    betas: (0.9, 0.999)
    eps: 1e-08
    lr: 0.001
    weight_decay: 0
)
Epoch 1 - |param|=2.08e+03 |g_param|=1.61e+05 loss=5.5268e+00 ppl=251.34
Validation - loss=4.6012e+00 ppl=99.60 best_loss=inf best_ppl=inf
Epoch 2 - |param|=2.08e+03 |g_param|=7.58e+04 loss=5.1940e+00 ppl=180.19
Validation - loss=4.2752e+00 ppl=71.90 best_loss=4.6012e+00 best_ppl=99.60
Epoch 3 - |param|=2.08e+03 |g_param|=6.49e+04 loss=4.9096e+00 ppl=135.58
Validation - loss=4.0715e+00 ppl=58.65 best_loss=4.2752e+00 best_ppl=71.90
Epoch 4 - |param|=2.08e+03 |g_param|=6.61e+04 loss=4.6611e+00 ppl=105.76
Validation - loss=3.9509e+00 ppl=51.98 best_loss=4.0715e+00 best_ppl=58.65
Epoch 5 - |param|=2.08e+03 |g_param|=7.46e+04 loss=4.5474e+00 ppl=94.39
Validation - loss=3.8678e+00 ppl=47.84 best_loss=3.9509e+00 best_ppl=51.98
Epoch 6 - |param|=2.08e+03 |g_param|=4.03e+04 loss=4.3557e+00 ppl=77.92
Validation - loss=3.7963e+00 ppl=44.53 best_loss=3.8678e+00 best_ppl=47.84
Epoch 7 - |param|=2.08e+03 |g_param|=4.20e+04 loss=4.2542e+00 ppl=70.40
Validation - loss=3.6544e+00 ppl=38.64 best_loss=3.7963e+00 best_ppl=44.53
Epoch 8 - |param|=2.08e+03 |g_param|=4.01e+04 loss=4.0988e+00 ppl=60.27
Validation - loss=3.5725e+00 ppl=35.61 best_loss=3.6544e+00 best_ppl=38.64
Epoch 9 - |param|=2.09e+03 |g_param|=4.10e+04 loss=3.9463e+00 ppl=51.74
Validation - loss=3.5103e+00 ppl=33.46 best_loss=3.5725e+00 best_ppl=35.61
Epoch 10 - |param|=2.09e+03 |g_param|=4.39e+04 loss=3.8204e+00 ppl=45.62
Validation - loss=3.4532e+00 ppl=31.60 best_loss=3.5103e+00 best_ppl=33.46
Epoch 11 - |param|=2.09e+03 |g_param|=4.76e+04 loss=3.7310e+00 ppl=41.72
Validation - loss=3.4264e+00 ppl=30.77 best_loss=3.4532e+00 best_ppl=31.60
Epoch 12 - |param|=2.09e+03 |g_param|=4.21e+04 loss=3.6087e+00 ppl=36.92
Validation - loss=3.3480e+00 ppl=28.44 best_loss=3.4264e+00 best_ppl=30.77
Epoch 13 - |param|=2.09e+03 |g_param|=4.78e+04 loss=3.4251e+00 ppl=30.72
Validation - loss=3.3150e+00 ppl=27.52 best_loss=3.3480e+00 best_ppl=28.44
Epoch 14 - |param|=2.09e+03 |g_param|=4.22e+04 loss=3.3303e+00 ppl=27.95
Validation - loss=3.2611e+00 ppl=26.08 best_loss=3.3150e+00 best_ppl=27.52
Epoch 15 - |param|=2.09e+03 |g_param|=6.19e+04 loss=3.3365e+00 ppl=28.12
Validation - loss=3.2879e+00 ppl=26.79 best_loss=3.2611e+00 best_ppl=26.08
Epoch 16 - |param|=2.09e+03 |g_param|=5.20e+04 loss=3.2468e+00 ppl=25.71
Validation - loss=3.2030e+00 ppl=24.61 best_loss=3.2611e+00 best_ppl=26.08
Epoch 17 - |param|=2.09e+03 |g_param|=4.68e+04 loss=3.0925e+00 ppl=22.03
Validation - loss=3.1565e+00 ppl=23.49 best_loss=3.2030e+00 best_ppl=24.61
Epoch 18 - |param|=2.09e+03 |g_param|=5.39e+04 loss=3.0645e+00 ppl=21.42
Validation - loss=3.1496e+00 ppl=23.33 best_loss=3.1565e+00 best_ppl=23.49
Epoch 19 - |param|=2.09e+03 |g_param|=5.16e+04 loss=2.9253e+00 ppl=18.64
Validation - loss=3.1092e+00 ppl=22.40 best_loss=3.1496e+00 best_ppl=23.33
Epoch 20 - |param|=2.09e+03 |g_param|=5.28e+04 loss=2.8891e+00 ppl=17.98
Validation - loss=3.0871e+00 ppl=21.91 best_loss=3.1092e+00 best_ppl=22.40
Epoch 21 - |param|=2.09e+03 |g_param|=1.01e+05 loss=2.7839e+00 ppl=16.18
Validation - loss=3.0524e+00 ppl=21.17 best_loss=3.0871e+00 best_ppl=21.91
Epoch 22 - |param|=2.10e+03 |g_param|=1.17e+05 loss=2.7077e+00 ppl=15.00
Validation - loss=3.0783e+00 ppl=21.72 best_loss=3.0524e+00 best_ppl=21.17
Epoch 23 - |param|=2.10e+03 |g_param|=1.05e+05 loss=2.6888e+00 ppl=14.71
Validation - loss=3.0044e+00 ppl=20.17 best_loss=3.0524e+00 best_ppl=21.17
Epoch 24 - |param|=2.10e+03 |g_param|=1.12e+05 loss=2.6419e+00 ppl=14.04
Validation - loss=2.9977e+00 ppl=20.04 best_loss=3.0044e+00 best_ppl=20.17
Epoch 25 - |param|=2.10e+03 |g_param|=1.28e+05 loss=2.5347e+00 ppl=12.61
Validation - loss=2.9816e+00 ppl=19.72 best_loss=2.9977e+00 best_ppl=20.04
Epoch 26 - |param|=2.10e+03 |g_param|=1.42e+05 loss=2.5442e+00 ppl=12.73
Validation - loss=2.9763e+00 ppl=19.62 best_loss=2.9816e+00 best_ppl=19.72
Epoch 27 - |param|=2.10e+03 |g_param|=1.17e+05 loss=2.4619e+00 ppl=11.73
Validation - loss=2.9756e+00 ppl=19.60 best_loss=2.9763e+00 best_ppl=19.62
Epoch 28 - |param|=2.10e+03 |g_param|=1.24e+05 loss=2.3740e+00 ppl=10.74
Validation - loss=2.9287e+00 ppl=18.70 best_loss=2.9756e+00 best_ppl=19.60
Epoch 29 - |param|=2.10e+03 |g_param|=1.12e+05 loss=2.2744e+00 ppl=9.72
Validation - loss=2.9258e+00 ppl=18.65 best_loss=2.9287e+00 best_ppl=18.70
Epoch 30 - |param|=2.10e+03 |g_param|=1.30e+05 loss=2.2996e+00 ppl=9.97
Validation - loss=2.9429e+00 ppl=18.97 best_loss=2.9258e+00 best_ppl=18.65
Epoch 31 - |param|=2.10e+03 |g_param|=1.16e+05 loss=2.1893e+00 ppl=8.93
Validation - loss=2.9118e+00 ppl=18.39 best_loss=2.9258e+00 best_ppl=18.65
Epoch 32 - |param|=2.10e+03 |g_param|=1.41e+05 loss=2.1690e+00 ppl=8.75
Validation - loss=2.9097e+00 ppl=18.35 best_loss=2.9118e+00 best_ppl=18.39
Epoch 33 - |param|=2.10e+03 |g_param|=1.12e+05 loss=2.1485e+00 ppl=8.57
Validation - loss=2.8887e+00 ppl=17.97 best_loss=2.9097e+00 best_ppl=18.35
Epoch 34 - |param|=2.11e+03 |g_param|=6.24e+04 loss=2.0944e+00 ppl=8.12
Validation - loss=2.8811e+00 ppl=17.83 best_loss=2.8887e+00 best_ppl=17.97
Epoch 35 - |param|=2.11e+03 |g_param|=6.49e+04 loss=2.0658e+00 ppl=7.89
Validation - loss=2.8791e+00 ppl=17.80 best_loss=2.8811e+00 best_ppl=17.83
Epoch 36 - |param|=2.11e+03 |g_param|=5.46e+04 loss=1.9460e+00 ppl=7.00
Validation - loss=2.8922e+00 ppl=18.03 best_loss=2.8791e+00 best_ppl=17.80
Epoch 37 - |param|=2.11e+03 |g_param|=6.67e+04 loss=1.9809e+00 ppl=7.25
Validation - loss=2.8581e+00 ppl=17.43 best_loss=2.8791e+00 best_ppl=17.80
Epoch 38 - |param|=2.11e+03 |g_param|=6.25e+04 loss=1.9154e+00 ppl=6.79
Validation - loss=2.8368e+00 ppl=17.06 best_loss=2.8581e+00 best_ppl=17.43
Epoch 39 - |param|=2.11e+03 |g_param|=7.08e+04 loss=1.9437e+00 ppl=6.98
Validation - loss=2.8489e+00 ppl=17.27 best_loss=2.8368e+00 best_ppl=17.06
Epoch 40 - |param|=2.11e+03 |g_param|=7.09e+04 loss=1.8499e+00 ppl=6.36
Validation - loss=2.8442e+00 ppl=17.19 best_loss=2.8368e+00 best_ppl=17.06
Epoch 41 - |param|=2.11e+03 |g_param|=6.44e+04 loss=1.8260e+00 ppl=6.21
Validation - loss=2.8242e+00 ppl=16.85 best_loss=2.8368e+00 best_ppl=17.06
Epoch 42 - |param|=2.11e+03 |g_param|=7.14e+04 loss=1.8287e+00 ppl=6.23
Validation - loss=2.8159e+00 ppl=16.71 best_loss=2.8242e+00 best_ppl=16.85
Epoch 43 - |param|=2.11e+03 |g_param|=7.19e+04 loss=1.7516e+00 ppl=5.76
Validation - loss=2.8080e+00 ppl=16.58 best_loss=2.8159e+00 best_ppl=16.71
Epoch 44 - |param|=2.11e+03 |g_param|=7.07e+04 loss=1.7199e+00 ppl=5.58
Validation - loss=2.8213e+00 ppl=16.80 best_loss=2.8080e+00 best_ppl=16.58
Epoch 45 - |param|=2.12e+03 |g_param|=7.96e+04 loss=1.7169e+00 ppl=5.57
Validation - loss=2.8278e+00 ppl=16.91 best_loss=2.8080e+00 best_ppl=16.58
Epoch 46 - |param|=2.12e+03 |g_param|=6.29e+04 loss=1.6345e+00 ppl=5.13
Validation - loss=2.8164e+00 ppl=16.72 best_loss=2.8080e+00 best_ppl=16.58
Epoch 47 - |param|=2.12e+03 |g_param|=6.34e+04 loss=1.6373e+00 ppl=5.14
Validation - loss=2.7989e+00 ppl=16.43 best_loss=2.8080e+00 best_ppl=16.58
Epoch 48 - |param|=2.12e+03 |g_param|=7.27e+04 loss=1.6533e+00 ppl=5.22
Validation - loss=2.8060e+00 ppl=16.54 best_loss=2.7989e+00 best_ppl=16.43
Epoch 49 - |param|=2.12e+03 |g_param|=1.34e+05 loss=1.5817e+00 ppl=4.86
Validation - loss=2.7999e+00 ppl=16.44 best_loss=2.7989e+00 best_ppl=16.43
Epoch 50 - |param|=2.12e+03 |g_param|=9.27e+04 loss=1.5866e+00 ppl=4.89
Validation - loss=2.8056e+00 ppl=16.54 best_loss=2.7989e+00 best_ppl=16.43
Epoch 51 - |param|=2.12e+03 |g_param|=7.13e+04 loss=1.5433e+00 ppl=4.68
Validation - loss=2.7953e+00 ppl=16.37 best_loss=2.7989e+00 best_ppl=16.43
Epoch 52 - |param|=2.12e+03 |g_param|=7.13e+04 loss=1.4949e+00 ppl=4.46
Validation - loss=2.8077e+00 ppl=16.57 best_loss=2.7953e+00 best_ppl=16.37
Epoch 53 - |param|=2.12e+03 |g_param|=6.66e+04 loss=1.4302e+00 ppl=4.18
Validation - loss=2.7930e+00 ppl=16.33 best_loss=2.7953e+00 best_ppl=16.37
Epoch 54 - |param|=2.12e+03 |g_param|=9.34e+04 loss=1.4863e+00 ppl=4.42
Validation - loss=2.9172e+00 ppl=18.49 best_loss=2.7930e+00 best_ppl=16.33
Epoch 55 - |param|=2.12e+03 |g_param|=6.76e+04 loss=1.3939e+00 ppl=4.03
Validation - loss=2.8145e+00 ppl=16.68 best_loss=2.7930e+00 best_ppl=16.33
Epoch 56 - |param|=2.13e+03 |g_param|=8.23e+04 loss=1.4306e+00 ppl=4.18
Validation - loss=2.8607e+00 ppl=17.47 best_loss=2.7930e+00 best_ppl=16.33
Epoch 57 - |param|=2.13e+03 |g_param|=6.70e+04 loss=1.3981e+00 ppl=4.05
Validation - loss=2.7861e+00 ppl=16.22 best_loss=2.7930e+00 best_ppl=16.33
Epoch 58 - |param|=2.13e+03 |g_param|=7.73e+04 loss=1.3833e+00 ppl=3.99
Validation - loss=2.7798e+00 ppl=16.12 best_loss=2.7861e+00 best_ppl=16.22
Epoch 59 - |param|=2.13e+03 |g_param|=6.77e+04 loss=1.3500e+00 ppl=3.86
Validation - loss=2.7981e+00 ppl=16.41 best_loss=2.7798e+00 best_ppl=16.12
Epoch 60 - |param|=2.13e+03 |g_param|=6.67e+04 loss=1.2989e+00 ppl=3.67
Validation - loss=2.7853e+00 ppl=16.20 best_loss=2.7798e+00 best_ppl=16.12
Epoch 61 - |param|=2.13e+03 |g_param|=6.55e+04 loss=1.2929e+00 ppl=3.64
Validation - loss=2.7903e+00 ppl=16.29 best_loss=2.7798e+00 best_ppl=16.12
Epoch 62 - |param|=2.13e+03 |g_param|=7.87e+04 loss=1.2823e+00 ppl=3.60
Validation - loss=2.7986e+00 ppl=16.42 best_loss=2.7798e+00 best_ppl=16.12
Epoch 63 - |param|=2.13e+03 |g_param|=6.98e+04 loss=1.2526e+00 ppl=3.50
Validation - loss=2.7980e+00 ppl=16.41 best_loss=2.7798e+00 best_ppl=16.12
Epoch 64 - |param|=2.13e+03 |g_param|=8.83e+04 loss=1.2848e+00 ppl=3.61
Validation - loss=2.9155e+00 ppl=18.46 best_loss=2.7798e+00 best_ppl=16.12
Epoch 65 - |param|=2.13e+03 |g_param|=7.28e+04 loss=1.2028e+00 ppl=3.33
Validation - loss=2.8005e+00 ppl=16.45 best_loss=2.7798e+00 best_ppl=16.12
Epoch 66 - |param|=2.13e+03 |g_param|=1.47e+05 loss=1.2135e+00 ppl=3.37
Validation - loss=2.7935e+00 ppl=16.34 best_loss=2.7798e+00 best_ppl=16.12
Epoch 67 - |param|=2.13e+03 |g_param|=1.51e+05 loss=1.1803e+00 ppl=3.26
Validation - loss=2.7982e+00 ppl=16.42 best_loss=2.7798e+00 best_ppl=16.12
Epoch 68 - |param|=2.14e+03 |g_param|=1.46e+05 loss=1.1891e+00 ppl=3.28
Validation - loss=2.8033e+00 ppl=16.50 best_loss=2.7798e+00 best_ppl=16.12
Epoch 69 - |param|=2.14e+03 |g_param|=1.15e+05 loss=1.1227e+00 ppl=3.07
Validation - loss=2.7953e+00 ppl=16.37 best_loss=2.7798e+00 best_ppl=16.12
Epoch 70 - |param|=2.14e+03 |g_param|=7.50e+04 loss=1.1316e+00 ppl=3.10
Validation - loss=2.8186e+00 ppl=16.75 best_loss=2.7798e+00 best_ppl=16.12
Epoch 71 - |param|=2.14e+03 |g_param|=6.91e+04 loss=1.1000e+00 ppl=3.00
Validation - loss=2.8021e+00 ppl=16.48 best_loss=2.7798e+00 best_ppl=16.12
Epoch 72 - |param|=2.14e+03 |g_param|=7.28e+04 loss=1.0943e+00 ppl=2.99
Validation - loss=2.7960e+00 ppl=16.38 best_loss=2.7798e+00 best_ppl=16.12
Epoch 73 - |param|=2.14e+03 |g_param|=7.36e+04 loss=1.1026e+00 ppl=3.01
Validation - loss=2.7985e+00 ppl=16.42 best_loss=2.7798e+00 best_ppl=16.12
Epoch 74 - |param|=2.14e+03 |g_param|=6.90e+04 loss=1.0473e+00 ppl=2.85
Validation - loss=2.8108e+00 ppl=16.62 best_loss=2.7798e+00 best_ppl=16.12
Epoch 75 - |param|=2.14e+03 |g_param|=7.25e+04 loss=1.0528e+00 ppl=2.87
Validation - loss=2.8045e+00 ppl=16.52 best_loss=2.7798e+00 best_ppl=16.12
Epoch 76 - |param|=2.14e+03 |g_param|=7.50e+04 loss=1.0267e+00 ppl=2.79
Validation - loss=2.8159e+00 ppl=16.71 best_loss=2.7798e+00 best_ppl=16.12
Epoch 77 - |param|=2.14e+03 |g_param|=8.36e+04 loss=1.0498e+00 ppl=2.86
Validation - loss=2.8110e+00 ppl=16.63 best_loss=2.7798e+00 best_ppl=16.12
Epoch 78 - |param|=2.14e+03 |g_param|=8.75e+04 loss=1.0378e+00 ppl=2.82
Validation - loss=2.8318e+00 ppl=16.98 best_loss=2.7798e+00 best_ppl=16.12
Epoch 79 - |param|=2.14e+03 |g_param|=6.82e+04 loss=9.6481e-01 ppl=2.62
Validation - loss=2.8182e+00 ppl=16.75 best_loss=2.7798e+00 best_ppl=16.12
Epoch 80 - |param|=2.15e+03 |g_param|=7.56e+04 loss=9.7931e-01 ppl=2.66
Validation - loss=2.8244e+00 ppl=16.85 best_loss=2.7798e+00 best_ppl=16.12
Epoch 81 - |param|=2.15e+03 |g_param|=7.74e+04 loss=9.7109e-01 ppl=2.64
Validation - loss=2.8313e+00 ppl=16.97 best_loss=2.7798e+00 best_ppl=16.12
Epoch 82 - |param|=2.15e+03 |g_param|=8.08e+04 loss=9.4137e-01 ppl=2.56
Validation - loss=2.8276e+00 ppl=16.90 best_loss=2.7798e+00 best_ppl=16.12
Epoch 83 - |param|=2.15e+03 |g_param|=7.20e+04 loss=9.3824e-01 ppl=2.56
Validation - loss=2.8379e+00 ppl=17.08 best_loss=2.7798e+00 best_ppl=16.12
Epoch 84 - |param|=2.15e+03 |g_param|=8.14e+04 loss=9.4182e-01 ppl=2.56
Validation - loss=2.8260e+00 ppl=16.88 best_loss=2.7798e+00 best_ppl=16.12
Epoch 85 - |param|=2.15e+03 |g_param|=1.62e+05 loss=9.4761e-01 ppl=2.58
Validation - loss=2.8442e+00 ppl=17.19 best_loss=2.7798e+00 best_ppl=16.12
Epoch 86 - |param|=2.15e+03 |g_param|=1.52e+05 loss=9.0810e-01 ppl=2.48
Validation - loss=2.8265e+00 ppl=16.89 best_loss=2.7798e+00 best_ppl=16.12
Epoch 87 - |param|=2.15e+03 |g_param|=1.26e+05 loss=8.9066e-01 ppl=2.44
Validation - loss=2.8303e+00 ppl=16.95 best_loss=2.7798e+00 best_ppl=16.12
Epoch 88 - |param|=2.15e+03 |g_param|=7.87e+04 loss=8.7112e-01 ppl=2.39
Validation - loss=2.8619e+00 ppl=17.50 best_loss=2.7798e+00 best_ppl=16.12
Epoch 89 - |param|=2.15e+03 |g_param|=7.00e+04 loss=8.4617e-01 ppl=2.33
Validation - loss=2.8557e+00 ppl=17.39 best_loss=2.7798e+00 best_ppl=16.12
Epoch 90 - |param|=2.15e+03 |g_param|=9.41e+04 loss=9.5675e-01 ppl=2.60
Validation - loss=2.8833e+00 ppl=17.87 best_loss=2.7798e+00 best_ppl=16.12
Epoch 91 - |param|=2.15e+03 |g_param|=6.90e+04 loss=8.4549e-01 ppl=2.33
Validation - loss=2.8571e+00 ppl=17.41 best_loss=2.7798e+00 best_ppl=16.12
Epoch 92 - |param|=2.16e+03 |g_param|=7.80e+04 loss=8.5057e-01 ppl=2.34
Validation - loss=2.8511e+00 ppl=17.31 best_loss=2.7798e+00 best_ppl=16.12
Epoch 93 - |param|=2.16e+03 |g_param|=7.74e+04 loss=7.9136e-01 ppl=2.21
Validation - loss=2.8972e+00 ppl=18.12 best_loss=2.7798e+00 best_ppl=16.12
Epoch 94 - |param|=2.16e+03 |g_param|=8.02e+04 loss=8.4128e-01 ppl=2.32
Validation - loss=2.8619e+00 ppl=17.49 best_loss=2.7798e+00 best_ppl=16.12
Epoch 95 - |param|=2.16e+03 |g_param|=7.69e+04 loss=8.0390e-01 ppl=2.23
Validation - loss=2.8721e+00 ppl=17.67 best_loss=2.7798e+00 best_ppl=16.12
Epoch 96 - |param|=2.16e+03 |g_param|=7.53e+04 loss=7.9575e-01 ppl=2.22
Validation - loss=2.8673e+00 ppl=17.59 best_loss=2.7798e+00 best_ppl=16.12
Epoch 97 - |param|=2.16e+03 |g_param|=6.98e+04 loss=7.7736e-01 ppl=2.18
Validation - loss=2.8786e+00 ppl=17.79 best_loss=2.7798e+00 best_ppl=16.12
Epoch 98 - |param|=2.16e+03 |g_param|=7.69e+04 loss=7.9752e-01 ppl=2.22
Validation - loss=2.8984e+00 ppl=18.15 best_loss=2.7798e+00 best_ppl=16.12
Epoch 99 - |param|=2.16e+03 |g_param|=6.17e+04 loss=7.4663e-01 ppl=2.11
Validation - loss=2.8806e+00 ppl=17.82 best_loss=2.7798e+00 best_ppl=16.12
Epoch 100 - |param|=2.16e+03 |g_param|=7.47e+04 loss=7.6758e-01 ppl=2.15
Validation - loss=2.9111e+00 ppl=18.38 best_loss=2.7798e+00 best_ppl=16.12
Epoch 101 - |param|=2.16e+03 |g_param|=7.07e+04 loss=7.5013e-01 ppl=2.12
Validation - loss=2.9169e+00 ppl=18.48 best_loss=2.7798e+00 best_ppl=16.12
Epoch 102 - |param|=2.16e+03 |g_param|=7.37e+04 loss=7.8630e-01 ppl=2.20
Validation - loss=2.9068e+00 ppl=18.30 best_loss=2.7798e+00 best_ppl=16.12
Epoch 103 - |param|=2.16e+03 |g_param|=1.41e+05 loss=7.7346e-01 ppl=2.17
Validation - loss=2.9068e+00 ppl=18.30 best_loss=2.7798e+00 best_ppl=16.12
Epoch 104 - |param|=2.16e+03 |g_param|=1.51e+05 loss=7.3241e-01 ppl=2.08
Validation - loss=2.8921e+00 ppl=18.03 best_loss=2.7798e+00 best_ppl=16.12
Epoch 105 - |param|=2.17e+03 |g_param|=1.51e+05 loss=7.1043e-01 ppl=2.03
Validation - loss=2.9022e+00 ppl=18.21 best_loss=2.7798e+00 best_ppl=16.12
Epoch 106 - |param|=2.17e+03 |g_param|=1.71e+05 loss=7.4569e-01 ppl=2.11
Validation - loss=2.9181e+00 ppl=18.51 best_loss=2.7798e+00 best_ppl=16.12
Epoch 107 - |param|=2.17e+03 |g_param|=1.62e+05 loss=7.1652e-01 ppl=2.05
Validation - loss=2.9083e+00 ppl=18.32 best_loss=2.7798e+00 best_ppl=16.12
Epoch 108 - |param|=2.17e+03 |g_param|=1.87e+05 loss=7.2377e-01 ppl=2.06
Validation - loss=2.9799e+00 ppl=19.69 best_loss=2.7798e+00 best_ppl=16.12
Epoch 109 - |param|=2.17e+03 |g_param|=1.47e+05 loss=7.0574e-01 ppl=2.03
Validation - loss=2.9327e+00 ppl=18.78 best_loss=2.7798e+00 best_ppl=16.12
Epoch 110 - |param|=2.17e+03 |g_param|=1.49e+05 loss=7.1375e-01 ppl=2.04
Validation - loss=2.9360e+00 ppl=18.84 best_loss=2.7798e+00 best_ppl=16.12
Epoch 111 - |param|=2.17e+03 |g_param|=1.43e+05 loss=6.8992e-01 ppl=1.99
Validation - loss=2.9318e+00 ppl=18.76 best_loss=2.7798e+00 best_ppl=16.12
Epoch 112 - |param|=2.17e+03 |g_param|=1.57e+05 loss=6.8562e-01 ppl=1.99
Validation - loss=2.9224e+00 ppl=18.59 best_loss=2.7798e+00 best_ppl=16.12
Epoch 113 - |param|=2.17e+03 |g_param|=1.45e+05 loss=6.5049e-01 ppl=1.92
Validation - loss=2.9371e+00 ppl=18.86 best_loss=2.7798e+00 best_ppl=16.12
Epoch 114 - |param|=2.17e+03 |g_param|=1.52e+05 loss=6.8615e-01 ppl=1.99
Validation - loss=2.9310e+00 ppl=18.75 best_loss=2.7798e+00 best_ppl=16.12
Epoch 115 - |param|=2.17e+03 |g_param|=1.38e+05 loss=6.5968e-01 ppl=1.93
Validation - loss=2.9226e+00 ppl=18.59 best_loss=2.7798e+00 best_ppl=16.12
Epoch 116 - |param|=2.17e+03 |g_param|=1.59e+05 loss=6.7585e-01 ppl=1.97
Validation - loss=2.9290e+00 ppl=18.71 best_loss=2.7798e+00 best_ppl=16.12
Epoch 117 - |param|=2.17e+03 |g_param|=8.49e+04 loss=6.3961e-01 ppl=1.90
Validation - loss=2.9407e+00 ppl=18.93 best_loss=2.7798e+00 best_ppl=16.12
Epoch 118 - |param|=2.18e+03 |g_param|=8.68e+04 loss=6.6963e-01 ppl=1.95
Validation - loss=2.9664e+00 ppl=19.42 best_loss=2.7798e+00 best_ppl=16.12
Epoch 119 - |param|=2.18e+03 |g_param|=7.49e+04 loss=6.3269e-01 ppl=1.88
Validation - loss=2.9363e+00 ppl=18.85 best_loss=2.7798e+00 best_ppl=16.12
Epoch 120 - |param|=2.18e+03 |g_param|=8.05e+04 loss=6.6051e-01 ppl=1.94
Validation - loss=2.9514e+00 ppl=19.13 best_loss=2.7798e+00 best_ppl=16.12
Epoch 121 - |param|=2.18e+03 |g_param|=7.33e+04 loss=6.1579e-01 ppl=1.85
Validation - loss=2.9610e+00 ppl=19.32 best_loss=2.7798e+00 best_ppl=16.12
Epoch 122 - |param|=2.18e+03 |g_param|=9.08e+04 loss=6.2355e-01 ppl=1.87
Validation - loss=2.9599e+00 ppl=19.30 best_loss=2.7798e+00 best_ppl=16.12
Epoch 123 - |param|=2.18e+03 |g_param|=6.25e+04 loss=5.9928e-01 ppl=1.82
Validation - loss=2.9570e+00 ppl=19.24 best_loss=2.7798e+00 best_ppl=16.12
Epoch 124 - |param|=2.18e+03 |g_param|=7.33e+04 loss=6.2429e-01 ppl=1.87
Validation - loss=2.9722e+00 ppl=19.53 best_loss=2.7798e+00 best_ppl=16.12
Epoch 125 - |param|=2.18e+03 |g_param|=7.69e+04 loss=5.9689e-01 ppl=1.82
Validation - loss=2.9880e+00 ppl=19.85 best_loss=2.7798e+00 best_ppl=16.12
Epoch 126 - |param|=2.18e+03 |g_param|=7.82e+04 loss=5.8680e-01 ppl=1.80
Validation - loss=2.9906e+00 ppl=19.90 best_loss=2.7798e+00 best_ppl=16.12
Epoch 127 - |param|=2.18e+03 |g_param|=7.53e+04 loss=5.7339e-01 ppl=1.77
Validation - loss=2.9616e+00 ppl=19.33 best_loss=2.7798e+00 best_ppl=16.12
Epoch 128 - |param|=2.18e+03 |g_param|=6.82e+04 loss=5.7933e-01 ppl=1.78
Validation - loss=2.9813e+00 ppl=19.71 best_loss=2.7798e+00 best_ppl=16.12
Epoch 129 - |param|=2.18e+03 |g_param|=8.51e+04 loss=5.7470e-01 ppl=1.78
Validation - loss=2.9895e+00 ppl=19.88 best_loss=2.7798e+00 best_ppl=16.12
Epoch 130 - |param|=2.18e+03 |g_param|=7.09e+04 loss=5.5700e-01 ppl=1.75
Validation - loss=3.0170e+00 ppl=20.43 best_loss=2.7798e+00 best_ppl=16.12
Epoch 131 - |param|=2.19e+03 |g_param|=7.79e+04 loss=5.8048e-01 ppl=1.79
Validation - loss=3.0229e+00 ppl=20.55 best_loss=2.7798e+00 best_ppl=16.12
Epoch 132 - |param|=2.19e+03 |g_param|=7.35e+04 loss=5.5784e-01 ppl=1.75
Validation - loss=3.0034e+00 ppl=20.15 best_loss=2.7798e+00 best_ppl=16.12
Epoch 133 - |param|=2.19e+03 |g_param|=1.36e+05 loss=5.5519e-01 ppl=1.74
Validation - loss=3.0159e+00 ppl=20.41 best_loss=2.7798e+00 best_ppl=16.12
Epoch 134 - |param|=2.19e+03 |g_param|=1.65e+05 loss=5.7217e-01 ppl=1.77
Validation - loss=3.0165e+00 ppl=20.42 best_loss=2.7798e+00 best_ppl=16.12
Epoch 135 - |param|=2.19e+03 |g_param|=1.51e+05 loss=5.4546e-01 ppl=1.73
Validation - loss=3.0153e+00 ppl=20.40 best_loss=2.7798e+00 best_ppl=16.12
Epoch 136 - |param|=2.19e+03 |g_param|=1.19e+05 loss=5.4353e-01 ppl=1.72
Validation - loss=2.9960e+00 ppl=20.01 best_loss=2.7798e+00 best_ppl=16.12
Epoch 137 - |param|=2.19e+03 |g_param|=8.95e+04 loss=5.8329e-01 ppl=1.79
Validation - loss=3.0353e+00 ppl=20.81 best_loss=2.7798e+00 best_ppl=16.12
Epoch 138 - |param|=2.19e+03 |g_param|=7.71e+04 loss=5.1972e-01 ppl=1.68
Validation - loss=3.0201e+00 ppl=20.49 best_loss=2.7798e+00 best_ppl=16.12
Epoch 139 - |param|=2.19e+03 |g_param|=6.56e+04 loss=5.1505e-01 ppl=1.67
Validation - loss=2.9973e+00 ppl=20.03 best_loss=2.7798e+00 best_ppl=16.12
Epoch 140 - |param|=2.19e+03 |g_param|=7.31e+04 loss=5.1275e-01 ppl=1.67
Validation - loss=3.0309e+00 ppl=20.72 best_loss=2.7798e+00 best_ppl=16.12
Epoch 141 - |param|=2.19e+03 |g_param|=8.65e+04 loss=5.3771e-01 ppl=1.71
Validation - loss=3.0712e+00 ppl=21.57 best_loss=2.7798e+00 best_ppl=16.12
Epoch 142 - |param|=2.19e+03 |g_param|=7.46e+04 loss=5.3795e-01 ppl=1.71
Validation - loss=3.0402e+00 ppl=20.91 best_loss=2.7798e+00 best_ppl=16.12
Epoch 143 - |param|=2.19e+03 |g_param|=7.38e+04 loss=5.2678e-01 ppl=1.69
Validation - loss=3.0400e+00 ppl=20.90 best_loss=2.7798e+00 best_ppl=16.12
Epoch 144 - |param|=2.19e+03 |g_param|=9.02e+04 loss=5.3614e-01 ppl=1.71
Validation - loss=3.1074e+00 ppl=22.36 best_loss=2.7798e+00 best_ppl=16.12
Epoch 145 - |param|=2.20e+03 |g_param|=7.91e+04 loss=5.2991e-01 ppl=1.70
Validation - loss=3.0731e+00 ppl=21.61 best_loss=2.7798e+00 best_ppl=16.12
Epoch 146 - |param|=2.20e+03 |g_param|=8.86e+04 loss=5.1556e-01 ppl=1.67
Validation - loss=3.0508e+00 ppl=21.13 best_loss=2.7798e+00 best_ppl=16.12
Epoch 147 - |param|=2.20e+03 |g_param|=6.85e+04 loss=4.8245e-01 ppl=1.62
Validation - loss=3.0529e+00 ppl=21.18 best_loss=2.7798e+00 best_ppl=16.12
Epoch 148 - |param|=2.20e+03 |g_param|=7.54e+04 loss=5.0051e-01 ppl=1.65
Validation - loss=3.0386e+00 ppl=20.88 best_loss=2.7798e+00 best_ppl=16.12
Epoch 149 - |param|=2.20e+03 |g_param|=8.16e+04 loss=4.9290e-01 ppl=1.64
Validation - loss=3.0423e+00 ppl=20.95 best_loss=2.7798e+00 best_ppl=16.12
Epoch 150 - |param|=2.20e+03 |g_param|=7.30e+04 loss=4.8122e-01 ppl=1.62
Validation - loss=3.0541e+00 ppl=21.20 best_loss=2.7798e+00 best_ppl=16.12
Epoch 151 - |param|=2.20e+03 |g_param|=7.44e+04 loss=4.7033e-01 ppl=1.60
Validation - loss=3.0736e+00 ppl=21.62 best_loss=2.7798e+00 best_ppl=16.12
Epoch 152 - |param|=2.20e+03 |g_param|=1.54e+05 loss=4.8531e-01 ppl=1.62
Validation - loss=3.0920e+00 ppl=22.02 best_loss=2.7798e+00 best_ppl=16.12
Epoch 153 - |param|=2.20e+03 |g_param|=1.53e+05 loss=4.6109e-01 ppl=1.59
Validation - loss=3.0667e+00 ppl=21.47 best_loss=2.7798e+00 best_ppl=16.12
Epoch 154 - |param|=2.20e+03 |g_param|=1.16e+05 loss=4.4531e-01 ppl=1.56
Validation - loss=3.0389e+00 ppl=20.88 best_loss=2.7798e+00 best_ppl=16.12
Epoch 155 - |param|=2.20e+03 |g_param|=6.81e+04 loss=4.6261e-01 ppl=1.59
Validation - loss=3.0533e+00 ppl=21.19 best_loss=2.7798e+00 best_ppl=16.12
Epoch 156 - |param|=2.20e+03 |g_param|=6.99e+04 loss=4.7638e-01 ppl=1.61
Validation - loss=3.0700e+00 ppl=21.54 best_loss=2.7798e+00 best_ppl=16.12
Epoch 157 - |param|=2.20e+03 |g_param|=6.97e+04 loss=4.5318e-01 ppl=1.57
Validation - loss=3.0734e+00 ppl=21.61 best_loss=2.7798e+00 best_ppl=16.12
Epoch 158 - |param|=2.20e+03 |g_param|=7.79e+04 loss=4.6848e-01 ppl=1.60
Validation - loss=3.0668e+00 ppl=21.47 best_loss=2.7798e+00 best_ppl=16.12
Epoch 159 - |param|=2.21e+03 |g_param|=7.24e+04 loss=4.3291e-01 ppl=1.54
Validation - loss=3.0930e+00 ppl=22.04 best_loss=2.7798e+00 best_ppl=16.12
Epoch 160 - |param|=2.21e+03 |g_param|=7.13e+04 loss=4.4454e-01 ppl=1.56
Validation - loss=3.0936e+00 ppl=22.06 best_loss=2.7798e+00 best_ppl=16.12
Epoch 161 - |param|=2.21e+03 |g_param|=7.19e+04 loss=4.5029e-01 ppl=1.57
Validation - loss=3.0957e+00 ppl=22.10 best_loss=2.7798e+00 best_ppl=16.12
Epoch 162 - |param|=2.21e+03 |g_param|=7.67e+04 loss=4.4438e-01 ppl=1.56
Validation - loss=3.1205e+00 ppl=22.66 best_loss=2.7798e+00 best_ppl=16.12
Epoch 163 - |param|=2.21e+03 |g_param|=7.18e+04 loss=4.5780e-01 ppl=1.58
Validation - loss=3.1156e+00 ppl=22.55 best_loss=2.7798e+00 best_ppl=16.12
Epoch 164 - |param|=2.21e+03 |g_param|=6.86e+04 loss=4.2853e-01 ppl=1.53
Validation - loss=3.1185e+00 ppl=22.61 best_loss=2.7798e+00 best_ppl=16.12
Epoch 165 - |param|=2.21e+03 |g_param|=8.34e+04 loss=4.3524e-01 ppl=1.55
Validation - loss=3.1037e+00 ppl=22.28 best_loss=2.7798e+00 best_ppl=16.12
Epoch 166 - |param|=2.21e+03 |g_param|=7.14e+04 loss=4.1195e-01 ppl=1.51
Validation - loss=3.1283e+00 ppl=22.84 best_loss=2.7798e+00 best_ppl=16.12
Epoch 167 - |param|=2.21e+03 |g_param|=7.05e+04 loss=4.4257e-01 ppl=1.56
Validation - loss=3.1379e+00 ppl=23.06 best_loss=2.7798e+00 best_ppl=16.12
Epoch 168 - |param|=2.21e+03 |g_param|=7.61e+04 loss=4.4386e-01 ppl=1.56
Validation - loss=3.1197e+00 ppl=22.64 best_loss=2.7798e+00 best_ppl=16.12
Epoch 169 - |param|=2.21e+03 |g_param|=7.58e+04 loss=4.2273e-01 ppl=1.53
Validation - loss=3.1304e+00 ppl=22.88 best_loss=2.7798e+00 best_ppl=16.12
Epoch 170 - |param|=2.21e+03 |g_param|=1.48e+05 loss=4.0469e-01 ppl=1.50
Validation - loss=3.1127e+00 ppl=22.48 best_loss=2.7798e+00 best_ppl=16.12
Epoch 171 - |param|=2.21e+03 |g_param|=1.75e+05 loss=4.3251e-01 ppl=1.54
Validation - loss=3.1178e+00 ppl=22.60 best_loss=2.7798e+00 best_ppl=16.12
Epoch 172 - |param|=2.22e+03 |g_param|=1.43e+05 loss=3.9740e-01 ppl=1.49
Validation - loss=3.1231e+00 ppl=22.72 best_loss=2.7798e+00 best_ppl=16.12
Epoch 173 - |param|=2.22e+03 |g_param|=1.44e+05 loss=3.9355e-01 ppl=1.48
Validation - loss=3.1281e+00 ppl=22.83 best_loss=2.7798e+00 best_ppl=16.12
Epoch 174 - |param|=2.22e+03 |g_param|=1.48e+05 loss=3.9959e-01 ppl=1.49
Validation - loss=3.1378e+00 ppl=23.05 best_loss=2.7798e+00 best_ppl=16.12
Epoch 175 - |param|=2.22e+03 |g_param|=1.42e+05 loss=4.1388e-01 ppl=1.51
Validation - loss=3.1503e+00 ppl=23.34 best_loss=2.7798e+00 best_ppl=16.12
Epoch 176 - |param|=2.22e+03 |g_param|=1.57e+05 loss=3.8579e-01 ppl=1.47
Validation - loss=3.1367e+00 ppl=23.03 best_loss=2.7798e+00 best_ppl=16.12
Epoch 177 - |param|=2.22e+03 |g_param|=1.64e+05 loss=4.0522e-01 ppl=1.50
Validation - loss=3.1716e+00 ppl=23.85 best_loss=2.7798e+00 best_ppl=16.12
Epoch 178 - |param|=2.22e+03 |g_param|=1.51e+05 loss=3.9954e-01 ppl=1.49
Validation - loss=3.1449e+00 ppl=23.22 best_loss=2.7798e+00 best_ppl=16.12
Epoch 179 - |param|=2.22e+03 |g_param|=1.75e+05 loss=4.2499e-01 ppl=1.53
Validation - loss=3.1715e+00 ppl=23.84 best_loss=2.7798e+00 best_ppl=16.12
Epoch 180 - |param|=2.22e+03 |g_param|=1.47e+05 loss=3.9903e-01 ppl=1.49
Validation - loss=3.1585e+00 ppl=23.53 best_loss=2.7798e+00 best_ppl=16.12
Epoch 181 - |param|=2.22e+03 |g_param|=7.60e+04 loss=3.9888e-01 ppl=1.49
Validation - loss=3.1634e+00 ppl=23.65 best_loss=2.7798e+00 best_ppl=16.12
Epoch 182 - |param|=2.22e+03 |g_param|=8.74e+04 loss=4.2310e-01 ppl=1.53
Validation - loss=3.2217e+00 ppl=25.07 best_loss=2.7798e+00 best_ppl=16.12
Epoch 183 - |param|=2.22e+03 |g_param|=7.94e+04 loss=4.0662e-01 ppl=1.50
Validation - loss=3.2021e+00 ppl=24.58 best_loss=2.7798e+00 best_ppl=16.12
Epoch 184 - |param|=2.22e+03 |g_param|=7.87e+04 loss=3.8616e-01 ppl=1.47
Validation - loss=3.1806e+00 ppl=24.06 best_loss=2.7798e+00 best_ppl=16.12
Epoch 185 - |param|=2.22e+03 |g_param|=6.23e+04 loss=3.6475e-01 ppl=1.44
Validation - loss=3.1786e+00 ppl=24.01 best_loss=2.7798e+00 best_ppl=16.12
Epoch 186 - |param|=2.22e+03 |g_param|=6.93e+04 loss=3.7693e-01 ppl=1.46
Validation - loss=3.1841e+00 ppl=24.15 best_loss=2.7798e+00 best_ppl=16.12
Epoch 187 - |param|=2.23e+03 |g_param|=7.49e+04 loss=3.7353e-01 ppl=1.45
Validation - loss=3.1817e+00 ppl=24.09 best_loss=2.7798e+00 best_ppl=16.12
Epoch 188 - |param|=2.23e+03 |g_param|=6.47e+04 loss=3.5836e-01 ppl=1.43
Validation - loss=3.1884e+00 ppl=24.25 best_loss=2.7798e+00 best_ppl=16.12
Epoch 189 - |param|=2.23e+03 |g_param|=6.89e+04 loss=3.5992e-01 ppl=1.43
Validation - loss=3.1949e+00 ppl=24.41 best_loss=2.7798e+00 best_ppl=16.12
Epoch 190 - |param|=2.23e+03 |g_param|=6.58e+04 loss=3.3342e-01 ppl=1.40
Validation - loss=3.2003e+00 ppl=24.54 best_loss=2.7798e+00 best_ppl=16.12
Epoch 191 - |param|=2.23e+03 |g_param|=8.16e+04 loss=3.6252e-01 ppl=1.44
Validation - loss=3.2188e+00 ppl=25.00 best_loss=2.7798e+00 best_ppl=16.12
Epoch 192 - |param|=2.23e+03 |g_param|=7.69e+04 loss=3.6163e-01 ppl=1.44
Validation - loss=3.2221e+00 ppl=25.08 best_loss=2.7798e+00 best_ppl=16.12
Epoch 193 - |param|=2.23e+03 |g_param|=6.22e+04 loss=3.5139e-01 ppl=1.42
Validation - loss=3.1820e+00 ppl=24.09 best_loss=2.7798e+00 best_ppl=16.12
Epoch 194 - |param|=2.23e+03 |g_param|=7.19e+04 loss=3.3544e-01 ppl=1.40
Validation - loss=3.2137e+00 ppl=24.87 best_loss=2.7798e+00 best_ppl=16.12
Epoch 195 - |param|=2.23e+03 |g_param|=9.09e+04 loss=3.8942e-01 ppl=1.48
Validation - loss=3.2090e+00 ppl=24.75 best_loss=2.7798e+00 best_ppl=16.12
Epoch 196 - |param|=2.23e+03 |g_param|=4.17e+04 loss=3.4872e-01 ppl=1.42
Validation - loss=3.1900e+00 ppl=24.29 best_loss=2.7798e+00 best_ppl=16.12
Epoch 197 - |param|=2.23e+03 |g_param|=4.00e+04 loss=3.5519e-01 ppl=1.43
Validation - loss=3.2225e+00 ppl=25.09 best_loss=2.7798e+00 best_ppl=16.12
Epoch 198 - |param|=2.23e+03 |g_param|=4.08e+04 loss=3.6200e-01 ppl=1.44
Validation - loss=3.2085e+00 ppl=24.74 best_loss=2.7798e+00 best_ppl=16.12
Epoch 199 - |param|=2.23e+03 |g_param|=3.19e+04 loss=3.3979e-01 ppl=1.40
Validation - loss=3.2471e+00 ppl=25.72 best_loss=2.7798e+00 best_ppl=16.12
Epoch 200 - |param|=2.23e+03 |g_param|=3.58e+04 loss=3.4803e-01 ppl=1.42
Validation - loss=3.2349e+00 ppl=25.40 best_loss=2.7798e+00 best_ppl=16.12
Epoch 201 - |param|=2.23e+03 |g_param|=3.74e+04 loss=3.2961e-01 ppl=1.39
Validation - loss=3.2367e+00 ppl=25.45 best_loss=2.7798e+00 best_ppl=16.12
Epoch 202 - |param|=2.24e+03 |g_param|=3.61e+04 loss=3.3162e-01 ppl=1.39
Validation - loss=3.2519e+00 ppl=25.84 best_loss=2.7798e+00 best_ppl=16.12
Epoch 203 - |param|=2.24e+03 |g_param|=3.84e+04 loss=3.4981e-01 ppl=1.42
Validation - loss=3.2500e+00 ppl=25.79 best_loss=2.7798e+00 best_ppl=16.12
Epoch 204 - |param|=2.24e+03 |g_param|=3.61e+04 loss=3.4930e-01 ppl=1.42
Validation - loss=3.2302e+00 ppl=25.28 best_loss=2.7798e+00 best_ppl=16.12
Epoch 205 - |param|=2.24e+03 |g_param|=3.61e+04 loss=3.3347e-01 ppl=1.40
Validation - loss=3.2465e+00 ppl=25.70 best_loss=2.7798e+00 best_ppl=16.12
Epoch 206 - |param|=2.24e+03 |g_param|=3.63e+04 loss=3.3354e-01 ppl=1.40
Validation - loss=3.2599e+00 ppl=26.05 best_loss=2.7798e+00 best_ppl=16.12
Epoch 207 - |param|=2.24e+03 |g_param|=3.19e+04 loss=3.3761e-01 ppl=1.40
Validation - loss=3.2598e+00 ppl=26.05 best_loss=2.7798e+00 best_ppl=16.12
Epoch 208 - |param|=2.24e+03 |g_param|=3.00e+04 loss=3.1610e-01 ppl=1.37
Validation - loss=3.2724e+00 ppl=26.38 best_loss=2.7798e+00 best_ppl=16.12
Epoch 209 - |param|=2.24e+03 |g_param|=3.61e+04 loss=3.1592e-01 ppl=1.37
Validation - loss=3.2709e+00 ppl=26.34 best_loss=2.7798e+00 best_ppl=16.12
Epoch 210 - |param|=2.24e+03 |g_param|=3.91e+04 loss=3.4353e-01 ppl=1.41
Validation - loss=3.2619e+00 ppl=26.10 best_loss=2.7798e+00 best_ppl=16.12
Epoch 211 - |param|=2.24e+03 |g_param|=3.58e+04 loss=3.1688e-01 ppl=1.37
Validation - loss=3.2857e+00 ppl=26.73 best_loss=2.7798e+00 best_ppl=16.12
Epoch 212 - |param|=2.24e+03 |g_param|=7.16e+04 loss=3.1887e-01 ppl=1.38
Validation - loss=3.2762e+00 ppl=26.48 best_loss=2.7798e+00 best_ppl=16.12
Epoch 213 - |param|=2.24e+03 |g_param|=8.11e+04 loss=3.2614e-01 ppl=1.39
Validation - loss=3.3049e+00 ppl=27.24 best_loss=2.7798e+00 best_ppl=16.12
Epoch 214 - |param|=2.24e+03 |g_param|=7.77e+04 loss=3.2462e-01 ppl=1.38
Validation - loss=3.2655e+00 ppl=26.19 best_loss=2.7798e+00 best_ppl=16.12
Epoch 215 - |param|=2.24e+03 |g_param|=8.15e+04 loss=3.5635e-01 ppl=1.43
Validation - loss=3.3128e+00 ppl=27.46 best_loss=2.7798e+00 best_ppl=16.12
Epoch 216 - |param|=2.25e+03 |g_param|=7.24e+04 loss=2.9664e-01 ppl=1.35
Validation - loss=3.2909e+00 ppl=26.87 best_loss=2.7798e+00 best_ppl=16.12
Epoch 217 - |param|=2.25e+03 |g_param|=6.69e+04 loss=3.0952e-01 ppl=1.36
Validation - loss=3.2868e+00 ppl=26.76 best_loss=2.7798e+00 best_ppl=16.12
Epoch 218 - |param|=2.25e+03 |g_param|=6.61e+04 loss=3.0959e-01 ppl=1.36
Validation - loss=3.2680e+00 ppl=26.26 best_loss=2.7798e+00 best_ppl=16.12
Epoch 219 - |param|=2.25e+03 |g_param|=6.13e+04 loss=2.8847e-01 ppl=1.33
Validation - loss=3.3010e+00 ppl=27.14 best_loss=2.7798e+00 best_ppl=16.12
Epoch 220 - |param|=2.25e+03 |g_param|=7.65e+04 loss=3.0648e-01 ppl=1.36
Validation - loss=3.3071e+00 ppl=27.31 best_loss=2.7798e+00 best_ppl=16.12
Epoch 221 - |param|=2.25e+03 |g_param|=7.12e+04 loss=3.0226e-01 ppl=1.35
Validation - loss=3.2824e+00 ppl=26.64 best_loss=2.7798e+00 best_ppl=16.12
Epoch 222 - |param|=2.25e+03 |g_param|=5.87e+04 loss=2.7844e-01 ppl=1.32
Validation - loss=3.2894e+00 ppl=26.83 best_loss=2.7798e+00 best_ppl=16.12
Epoch 223 - |param|=2.25e+03 |g_param|=7.56e+04 loss=2.8785e-01 ppl=1.33
Validation - loss=3.2914e+00 ppl=26.88 best_loss=2.7798e+00 best_ppl=16.12
Epoch 224 - |param|=2.25e+03 |g_param|=6.27e+04 loss=2.8013e-01 ppl=1.32
Validation - loss=3.2848e+00 ppl=26.70 best_loss=2.7798e+00 best_ppl=16.12
Epoch 225 - |param|=2.25e+03 |g_param|=6.46e+04 loss=2.9223e-01 ppl=1.34
Validation - loss=3.2700e+00 ppl=26.31 best_loss=2.7798e+00 best_ppl=16.12
Epoch 226 - |param|=2.25e+03 |g_param|=6.93e+04 loss=3.0721e-01 ppl=1.36
Validation - loss=3.2799e+00 ppl=26.57 best_loss=2.7798e+00 best_ppl=16.12
Epoch 227 - |param|=2.25e+03 |g_param|=9.86e+04 loss=3.0078e-01 ppl=1.35
Validation - loss=3.3069e+00 ppl=27.30 best_loss=2.7798e+00 best_ppl=16.12
Epoch 228 - |param|=2.25e+03 |g_param|=1.33e+05 loss=2.8394e-01 ppl=1.33
Validation - loss=3.3090e+00 ppl=27.36 best_loss=2.7798e+00 best_ppl=16.12
Epoch 229 - |param|=2.25e+03 |g_param|=1.06e+05 loss=2.9532e-01 ppl=1.34
Validation - loss=3.3357e+00 ppl=28.10 best_loss=2.7798e+00 best_ppl=16.12
Epoch 230 - |param|=2.25e+03 |g_param|=8.15e+04 loss=2.9559e-01 ppl=1.34
Validation - loss=3.3271e+00 ppl=27.86 best_loss=2.7798e+00 best_ppl=16.12
Epoch 231 - |param|=2.25e+03 |g_param|=7.48e+04 loss=2.9726e-01 ppl=1.35
Validation - loss=3.3193e+00 ppl=27.64 best_loss=2.7798e+00 best_ppl=16.12
Epoch 232 - |param|=2.26e+03 |g_param|=7.34e+04 loss=2.9243e-01 ppl=1.34
Validation - loss=3.3304e+00 ppl=27.95 best_loss=2.7798e+00 best_ppl=16.12
Epoch 233 - |param|=2.26e+03 |g_param|=6.06e+04 loss=2.7104e-01 ppl=1.31
Validation - loss=3.3052e+00 ppl=27.25 best_loss=2.7798e+00 best_ppl=16.12
Epoch 234 - |param|=2.26e+03 |g_param|=6.14e+04 loss=2.7185e-01 ppl=1.31
Validation - loss=3.3138e+00 ppl=27.49 best_loss=2.7798e+00 best_ppl=16.12
Epoch 235 - |param|=2.26e+03 |g_param|=7.38e+04 loss=2.9641e-01 ppl=1.35
Validation - loss=3.3276e+00 ppl=27.87 best_loss=2.7798e+00 best_ppl=16.12
Epoch 236 - |param|=2.26e+03 |g_param|=6.59e+04 loss=2.8391e-01 ppl=1.33
Validation - loss=3.3189e+00 ppl=27.63 best_loss=2.7798e+00 best_ppl=16.12
Epoch 237 - |param|=2.26e+03 |g_param|=6.39e+04 loss=2.7287e-01 ppl=1.31
Validation - loss=3.3313e+00 ppl=27.97 best_loss=2.7798e+00 best_ppl=16.12
Epoch 238 - |param|=2.26e+03 |g_param|=6.75e+04 loss=2.7375e-01 ppl=1.31
Validation - loss=3.3497e+00 ppl=28.49 best_loss=2.7798e+00 best_ppl=16.12
Epoch 239 - |param|=2.26e+03 |g_param|=7.53e+04 loss=2.7925e-01 ppl=1.32
Validation - loss=3.3502e+00 ppl=28.51 best_loss=2.7798e+00 best_ppl=16.12
Epoch 240 - |param|=2.26e+03 |g_param|=7.31e+04 loss=2.7807e-01 ppl=1.32
Validation - loss=3.3479e+00 ppl=28.44 best_loss=2.7798e+00 best_ppl=16.12
Epoch 241 - |param|=2.26e+03 |g_param|=7.14e+04 loss=2.6618e-01 ppl=1.30
Validation - loss=3.3770e+00 ppl=29.28 best_loss=2.7798e+00 best_ppl=16.12
Epoch 242 - |param|=2.26e+03 |g_param|=6.39e+04 loss=2.6167e-01 ppl=1.30
Validation - loss=3.3567e+00 ppl=28.69 best_loss=2.7798e+00 best_ppl=16.12
Epoch 243 - |param|=2.26e+03 |g_param|=6.43e+04 loss=2.6384e-01 ppl=1.30
Validation - loss=3.3645e+00 ppl=28.92 best_loss=2.7798e+00 best_ppl=16.12
Epoch 244 - |param|=2.26e+03 |g_param|=6.51e+04 loss=2.7422e-01 ppl=1.32
Validation - loss=3.3585e+00 ppl=28.74 best_loss=2.7798e+00 best_ppl=16.12
Epoch 245 - |param|=2.26e+03 |g_param|=1.46e+05 loss=2.7771e-01 ppl=1.32
Validation - loss=3.3561e+00 ppl=28.68 best_loss=2.7798e+00 best_ppl=16.12
Epoch 246 - |param|=2.26e+03 |g_param|=1.50e+05 loss=2.7055e-01 ppl=1.31
Validation - loss=3.3600e+00 ppl=28.79 best_loss=2.7798e+00 best_ppl=16.12
Epoch 247 - |param|=2.27e+03 |g_param|=1.75e+05 loss=3.1274e-01 ppl=1.37
Validation - loss=3.3536e+00 ppl=28.61 best_loss=2.7798e+00 best_ppl=16.12
Epoch 248 - |param|=2.27e+03 |g_param|=1.26e+05 loss=2.5665e-01 ppl=1.29
Validation - loss=3.3803e+00 ppl=29.38 best_loss=2.7798e+00 best_ppl=16.12
Epoch 249 - |param|=2.27e+03 |g_param|=1.30e+05 loss=2.6040e-01 ppl=1.30
Validation - loss=3.3651e+00 ppl=28.94 best_loss=2.7798e+00 best_ppl=16.12
Epoch 250 - |param|=2.27e+03 |g_param|=1.50e+05 loss=2.6443e-01 ppl=1.30
Validation - loss=3.3455e+00 ppl=28.37 best_loss=2.7798e+00 best_ppl=16.12
Epoch 251 - |param|=2.27e+03 |g_param|=1.43e+05 loss=2.5692e-01 ppl=1.29
Validation - loss=3.3499e+00 ppl=28.50 best_loss=2.7798e+00 best_ppl=16.12
Epoch 252 - |param|=2.27e+03 |g_param|=1.36e+05 loss=2.6150e-01 ppl=1.30
Validation - loss=3.3822e+00 ppl=29.44 best_loss=2.7798e+00 best_ppl=16.12
Epoch 253 - |param|=2.27e+03 |g_param|=1.60e+05 loss=2.8169e-01 ppl=1.33
Validation - loss=3.3525e+00 ppl=28.57 best_loss=2.7798e+00 best_ppl=16.12
Epoch 254 - |param|=2.27e+03 |g_param|=1.30e+05 loss=2.4655e-01 ppl=1.28
Validation - loss=3.4007e+00 ppl=29.98 best_loss=2.7798e+00 best_ppl=16.12
Epoch 255 - |param|=2.27e+03 |g_param|=6.34e+04 loss=2.4004e-01 ppl=1.27
Validation - loss=3.3581e+00 ppl=28.73 best_loss=2.7798e+00 best_ppl=16.12
Epoch 256 - |param|=2.27e+03 |g_param|=6.31e+04 loss=2.4451e-01 ppl=1.28
Validation - loss=3.3625e+00 ppl=28.86 best_loss=2.7798e+00 best_ppl=16.12
Epoch 257 - |param|=2.27e+03 |g_param|=6.21e+04 loss=2.4428e-01 ppl=1.28
Validation - loss=3.3773e+00 ppl=29.29 best_loss=2.7798e+00 best_ppl=16.12
Epoch 258 - |param|=2.27e+03 |g_param|=7.22e+04 loss=2.4796e-01 ppl=1.28
Validation - loss=3.3896e+00 ppl=29.65 best_loss=2.7798e+00 best_ppl=16.12
Epoch 259 - |param|=2.27e+03 |g_param|=7.93e+04 loss=2.6865e-01 ppl=1.31
Validation - loss=3.4070e+00 ppl=30.17 best_loss=2.7798e+00 best_ppl=16.12
Epoch 260 - |param|=2.27e+03 |g_param|=6.97e+04 loss=2.3823e-01 ppl=1.27
Validation - loss=3.3975e+00 ppl=29.89 best_loss=2.7798e+00 best_ppl=16.12
Epoch 261 - |param|=2.27e+03 |g_param|=5.79e+04 loss=2.4067e-01 ppl=1.27
Validation - loss=3.4108e+00 ppl=30.29 best_loss=2.7798e+00 best_ppl=16.12
Epoch 262 - |param|=2.27e+03 |g_param|=7.25e+04 loss=2.4205e-01 ppl=1.27
Validation - loss=3.4453e+00 ppl=31.35 best_loss=2.7798e+00 best_ppl=16.12
Epoch 263 - |param|=2.28e+03 |g_param|=6.71e+04 loss=2.5045e-01 ppl=1.28
Validation - loss=3.4107e+00 ppl=30.29 best_loss=2.7798e+00 best_ppl=16.12
Epoch 264 - |param|=2.28e+03 |g_param|=6.38e+04 loss=2.4053e-01 ppl=1.27
Validation - loss=3.4150e+00 ppl=30.42 best_loss=2.7798e+00 best_ppl=16.12
Epoch 265 - |param|=2.28e+03 |g_param|=7.19e+04 loss=2.4791e-01 ppl=1.28
Validation - loss=3.4062e+00 ppl=30.15 best_loss=2.7798e+00 best_ppl=16.12
Epoch 266 - |param|=2.28e+03 |g_param|=7.22e+04 loss=2.3959e-01 ppl=1.27
Validation - loss=3.4079e+00 ppl=30.20 best_loss=2.7798e+00 best_ppl=16.12
Epoch 267 - |param|=2.28e+03 |g_param|=7.04e+04 loss=2.4951e-01 ppl=1.28
Validation - loss=3.4165e+00 ppl=30.46 best_loss=2.7798e+00 best_ppl=16.12
Epoch 268 - |param|=2.28e+03 |g_param|=6.75e+04 loss=2.3838e-01 ppl=1.27
Validation - loss=3.4333e+00 ppl=30.98 best_loss=2.7798e+00 best_ppl=16.12
Epoch 269 - |param|=2.28e+03 |g_param|=6.35e+04 loss=2.4285e-01 ppl=1.27
Validation - loss=3.4091e+00 ppl=30.24 best_loss=2.7798e+00 best_ppl=16.12
Epoch 270 - |param|=2.28e+03 |g_param|=6.27e+04 loss=2.2701e-01 ppl=1.25
Validation - loss=3.4317e+00 ppl=30.93 best_loss=2.7798e+00 best_ppl=16.12
Epoch 271 - |param|=2.28e+03 |g_param|=1.41e+05 loss=2.4966e-01 ppl=1.28
Validation - loss=3.4206e+00 ppl=30.59 best_loss=2.7798e+00 best_ppl=16.12
Epoch 272 - |param|=2.28e+03 |g_param|=1.36e+05 loss=2.3614e-01 ppl=1.27
Validation - loss=3.4356e+00 ppl=31.05 best_loss=2.7798e+00 best_ppl=16.12
Epoch 273 - |param|=2.28e+03 |g_param|=1.48e+05 loss=2.3999e-01 ppl=1.27
Validation - loss=3.4609e+00 ppl=31.85 best_loss=2.7798e+00 best_ppl=16.12
Epoch 274 - |param|=2.28e+03 |g_param|=1.34e+05 loss=2.3603e-01 ppl=1.27
Validation - loss=3.4500e+00 ppl=31.50 best_loss=2.7798e+00 best_ppl=16.12
Epoch 275 - |param|=2.28e+03 |g_param|=1.30e+05 loss=2.3003e-01 ppl=1.26
Validation - loss=3.4205e+00 ppl=30.59 best_loss=2.7798e+00 best_ppl=16.12
Epoch 276 - |param|=2.28e+03 |g_param|=1.25e+05 loss=2.2412e-01 ppl=1.25
Validation - loss=3.4550e+00 ppl=31.66 best_loss=2.7798e+00 best_ppl=16.12
Epoch 277 - |param|=2.28e+03 |g_param|=1.56e+05 loss=2.4510e-01 ppl=1.28
Validation - loss=3.4442e+00 ppl=31.32 best_loss=2.7798e+00 best_ppl=16.12
Epoch 278 - |param|=2.28e+03 |g_param|=1.31e+05 loss=2.2943e-01 ppl=1.26
Validation - loss=3.4461e+00 ppl=31.38 best_loss=2.7798e+00 best_ppl=16.12
Epoch 279 - |param|=2.29e+03 |g_param|=1.45e+05 loss=2.4108e-01 ppl=1.27
Validation - loss=3.4844e+00 ppl=32.60 best_loss=2.7798e+00 best_ppl=16.12
Epoch 280 - |param|=2.29e+03 |g_param|=1.37e+05 loss=2.3591e-01 ppl=1.27
Validation - loss=3.4554e+00 ppl=31.67 best_loss=2.7798e+00 best_ppl=16.12
Epoch 281 - |param|=2.29e+03 |g_param|=9.51e+04 loss=2.3183e-01 ppl=1.26
Validation - loss=3.4442e+00 ppl=31.32 best_loss=2.7798e+00 best_ppl=16.12
Epoch 282 - |param|=2.29e+03 |g_param|=6.95e+04 loss=2.3690e-01 ppl=1.27
Validation - loss=3.4652e+00 ppl=31.98 best_loss=2.7798e+00 best_ppl=16.12
Epoch 283 - |param|=2.29e+03 |g_param|=7.14e+04 loss=2.3308e-01 ppl=1.26
Validation - loss=3.4833e+00 ppl=32.57 best_loss=2.7798e+00 best_ppl=16.12
Epoch 284 - |param|=2.29e+03 |g_param|=6.21e+04 loss=2.3180e-01 ppl=1.26
Validation - loss=3.4631e+00 ppl=31.92 best_loss=2.7798e+00 best_ppl=16.12
Epoch 285 - |param|=2.29e+03 |g_param|=6.85e+04 loss=2.2467e-01 ppl=1.25
Validation - loss=3.4797e+00 ppl=32.45 best_loss=2.7798e+00 best_ppl=16.12
Epoch 286 - |param|=2.29e+03 |g_param|=6.66e+04 loss=2.1578e-01 ppl=1.24
Validation - loss=3.4774e+00 ppl=32.38 best_loss=2.7798e+00 best_ppl=16.12
Epoch 287 - |param|=2.29e+03 |g_param|=8.52e+04 loss=2.5671e-01 ppl=1.29
Validation - loss=3.5431e+00 ppl=34.57 best_loss=2.7798e+00 best_ppl=16.12
Epoch 288 - |param|=2.29e+03 |g_param|=8.34e+04 loss=2.3783e-01 ppl=1.27
Validation - loss=3.5021e+00 ppl=33.19 best_loss=2.7798e+00 best_ppl=16.12
Epoch 289 - |param|=2.29e+03 |g_param|=6.56e+04 loss=2.2353e-01 ppl=1.25
Validation - loss=3.4813e+00 ppl=32.50 best_loss=2.7798e+00 best_ppl=16.12
Epoch 290 - |param|=2.29e+03 |g_param|=5.95e+04 loss=2.1102e-01 ppl=1.23
Validation - loss=3.4734e+00 ppl=32.25 best_loss=2.7798e+00 best_ppl=16.12
Epoch 291 - |param|=2.29e+03 |g_param|=7.17e+04 loss=2.1584e-01 ppl=1.24
Validation - loss=3.5149e+00 ppl=33.61 best_loss=2.7798e+00 best_ppl=16.12
Epoch 292 - |param|=2.29e+03 |g_param|=7.06e+04 loss=2.1054e-01 ppl=1.23
Validation - loss=3.4615e+00 ppl=31.87 best_loss=2.7798e+00 best_ppl=16.12
Epoch 293 - |param|=2.29e+03 |g_param|=6.55e+04 loss=2.1437e-01 ppl=1.24
Validation - loss=3.4930e+00 ppl=32.89 best_loss=2.7798e+00 best_ppl=16.12
Epoch 294 - |param|=2.29e+03 |g_param|=5.98e+04 loss=2.0725e-01 ppl=1.23
Validation - loss=3.4976e+00 ppl=33.04 best_loss=2.7798e+00 best_ppl=16.12
Epoch 295 - |param|=2.29e+03 |g_param|=5.75e+04 loss=2.1349e-01 ppl=1.24
Validation - loss=3.4865e+00 ppl=32.67 best_loss=2.7798e+00 best_ppl=16.12
Epoch 296 - |param|=2.30e+03 |g_param|=7.49e+04 loss=2.1637e-01 ppl=1.24
Validation - loss=3.4952e+00 ppl=32.96 best_loss=2.7798e+00 best_ppl=16.12
Epoch 297 - |param|=2.30e+03 |g_param|=1.27e+05 loss=2.3417e-01 ppl=1.26
Validation - loss=3.4875e+00 ppl=32.70 best_loss=2.7798e+00 best_ppl=16.12
Epoch 298 - |param|=2.30e+03 |g_param|=1.40e+05 loss=2.0349e-01 ppl=1.23
Validation - loss=3.4933e+00 ppl=32.90 best_loss=2.7798e+00 best_ppl=16.12
Epoch 299 - |param|=2.30e+03 |g_param|=1.19e+05 loss=2.0283e-01 ppl=1.22
Validation - loss=3.5088e+00 ppl=33.41 best_loss=2.7798e+00 best_ppl=16.12
Epoch 300 - |param|=2.30e+03 |g_param|=1.14e+05 loss=1.9790e-01 ppl=1.22
Validation - loss=3.5293e+00 ppl=34.10 best_loss=2.7798e+00 best_ppl=16.12
```

my-br, br-my နှစ်ခု training လုပ်တာမှာ ကြာချိန် က   

```
real	153m46.567s
user	143m7.627s
sys	10m23.731s

real	270m40.795s
user	254m41.634s
sys	15m34.916s
```

## Testing/Evaluation (Seq2Seq)

updated bash script for my-br:  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, Thailand
# Last updated: 9 April 2022
# find all models and parse to translate.py for testing and multi-bleu.perl for evaluation with BLEU score
# updated for my-br

cd ./model/braille/seq2seq/my-br/;

for i in *.pth; do
   MODEL=$i;

   # Testing
   python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang mybr < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my > $MODEL.hyp

   # Evaluation with BLEU Score
   echo "Evaluation result for the model: $MODEL" | tee -a eval-results-mybr-seq2seq-300epoch.txt;
   cat $MODEL.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee  -a eval-results-mybr-seq2seq-300epoch.txt;

done

cd -;

```

testing for my-br ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-loop-seq2seq-mybr.sh
Evaluation result for the model: seq-model-mybr.01.5.55-256.31.4.60-99.18.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
BLEU = 0.00, 14.4/2.0/0.0/0.0 (BP=1.000, ratio=1.013, hyp_len=29164, ref_len=28803)
Evaluation result for the model: seq-model-mybr.02.5.07-159.40.4.23-68.40.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
BLEU = 0.00, 16.4/2.4/0.0/0.0 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.03.4.92-136.68.4.08-58.96.pth
BLEU = 0.45, 19.7/2.7/0.2/0.0 (BP=1.000, ratio=1.001, hyp_len=28827, ref_len=28803)
Evaluation result for the model: seq-model-mybr.04.4.75-115.25.3.96-52.68.pth
BLEU = 1.00, 20.5/3.1/0.4/0.0 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.05.4.51-90.51.3.87-47.74.pth
BLEU = 1.16, 21.9/3.7/0.5/0.0 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.06.4.46-86.72.3.81-44.99.pth
BLEU = 1.30, 23.4/4.1/0.7/0.0 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.07.4.25-70.00.3.74-42.12.pth
BLEU = 1.12, 24.2/4.3/0.7/0.0 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.08.4.11-60.69.3.65-38.64.pth
BLEU = 2.10, 26.1/5.4/1.2/0.1 (BP=1.000, ratio=1.002, hyp_len=28856, ref_len=28803)
Evaluation result for the model: seq-model-mybr.09.4.05-57.64.3.61-36.86.pth
BLEU = 2.41, 27.0/6.1/1.3/0.2 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.100.0.82-2.28.3.03-20.62.pth
BLEU = 16.88, 45.9/22.2/12.1/6.6 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.101.0.85-2.34.3.01-20.29.pth
BLEU = 17.10, 46.4/22.4/12.2/6.7 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.102.0.78-2.18.3.03-20.63.pth
BLEU = 17.26, 46.2/22.5/12.4/6.9 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.103.0.86-2.37.3.13-22.76.pth
BLEU = 15.16, 44.8/20.3/10.6/5.5 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.10.3.85-47.08.3.54-34.62.pth
BLEU = 2.46, 27.3/6.5/1.5/0.1 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.104.0.86-2.37.3.03-20.61.pth
BLEU = 17.33, 46.5/22.6/12.4/6.9 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.105.0.81-2.25.3.01-20.28.pth
BLEU = 17.13, 46.4/22.3/12.3/6.8 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.106.0.79-2.21.3.01-20.35.pth
BLEU = 17.35, 46.3/22.5/12.5/7.0 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.107.0.78-2.19.3.03-20.74.pth
BLEU = 17.51, 46.6/22.8/12.6/7.0 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.108.0.78-2.19.3.05-21.06.pth
BLEU = 17.14, 46.3/22.3/12.3/6.8 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.109.0.75-2.13.3.05-21.11.pth
BLEU = 17.48, 46.2/22.6/12.6/7.1 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.110.0.77-2.16.3.04-20.95.pth
BLEU = 17.46, 46.6/22.8/12.6/7.0 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.111.0.70-2.01.3.08-21.77.pth
BLEU = 17.54, 46.9/22.9/12.7/7.0 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.112.0.73-2.07.3.06-21.23.pth
BLEU = 17.65, 46.7/22.9/12.8/7.1 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.113.0.73-2.08.3.06-21.40.pth
BLEU = 17.21, 46.3/22.4/12.4/6.8 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.11.3.77-43.31.3.48-32.52.pth
BLEU = 3.44, 28.9/7.3/2.0/0.3 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.114.0.74-2.10.3.07-21.51.pth
BLEU = 17.60, 46.4/22.9/12.8/7.1 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.115.0.71-2.04.3.04-20.98.pth
BLEU = 18.00, 47.1/23.3/13.1/7.3 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.116.0.73-2.08.3.07-21.49.pth
BLEU = 17.02, 46.3/22.3/12.2/6.7 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.117.0.72-2.05.3.07-21.50.pth
BLEU = 17.77, 46.8/23.0/12.9/7.2 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.118.0.71-2.03.3.08-21.81.pth
BLEU = 17.45, 46.7/22.8/12.6/6.9 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.119.0.70-2.00.3.07-21.52.pth
BLEU = 18.18, 47.3/23.5/13.2/7.4 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.120.0.68-1.98.3.08-21.67.pth
BLEU = 18.03, 47.1/23.2/13.0/7.4 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.121.0.66-1.94.3.12-22.57.pth
BLEU = 17.30, 46.3/22.7/12.5/6.8 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.122.0.68-1.98.3.08-21.67.pth
BLEU = 17.99, 46.9/23.1/13.0/7.4 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.123.0.69-2.00.3.09-22.02.pth
BLEU = 17.93, 46.8/23.1/13.0/7.4 (BP=1.000, ratio=1.001, hyp_len=28833, ref_len=28803)
Evaluation result for the model: seq-model-mybr.12.3.67-39.44.3.44-31.22.pth
BLEU = 3.65, 29.3/7.7/2.1/0.4 (BP=1.000, ratio=1.001, hyp_len=28838, ref_len=28803)
Evaluation result for the model: seq-model-mybr.124.0.66-1.94.3.09-22.05.pth
BLEU = 18.10, 47.0/23.3/13.2/7.5 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.125.0.63-1.88.3.10-22.26.pth
BLEU = 17.68, 46.7/23.0/12.8/7.1 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.126.0.63-1.88.3.10-22.09.pth
BLEU = 18.30, 47.6/23.6/13.3/7.5 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.127.0.63-1.87.3.10-22.24.pth
BLEU = 17.91, 46.9/23.2/13.0/7.3 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.128.0.64-1.91.3.12-22.57.pth
BLEU = 18.12, 47.2/23.3/13.2/7.4 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.129.0.64-1.89.3.12-22.65.pth
BLEU = 17.95, 46.8/23.2/13.1/7.3 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.130.0.62-1.87.3.13-22.98.pth
BLEU = 18.03, 46.7/23.2/13.1/7.4 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.131.0.64-1.89.3.12-22.74.pth
BLEU = 17.94, 46.9/23.2/13.0/7.3 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.132.0.60-1.83.3.12-22.66.pth
BLEU = 18.18, 47.4/23.4/13.1/7.5 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.133.0.59-1.80.3.13-22.88.pth
BLEU = 18.19, 46.9/23.3/13.3/7.6 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.13.3.53-34.29.3.40-29.95.pth
BLEU = 3.76, 29.5/7.6/2.0/0.4 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.134.0.62-1.85.3.15-23.35.pth
BLEU = 17.68, 46.5/22.8/12.8/7.2 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.135.0.63-1.88.3.22-25.06.pth
BLEU = 16.45, 45.7/21.7/11.7/6.3 (BP=1.000, ratio=1.001, hyp_len=28835, ref_len=28803)
Evaluation result for the model: seq-model-mybr.136.0.60-1.82.3.15-23.30.pth
BLEU = 18.08, 46.8/23.3/13.2/7.4 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.137.0.58-1.79.3.12-22.58.pth
BLEU = 18.20, 47.3/23.5/13.3/7.5 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.138.0.59-1.81.3.14-23.17.pth
BLEU = 18.10, 46.8/23.3/13.1/7.5 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.139.0.57-1.77.3.15-23.40.pth
BLEU = 18.24, 47.1/23.4/13.3/7.6 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.140.0.57-1.77.3.13-22.87.pth
BLEU = 18.71, 47.7/23.8/13.6/7.9 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.141.0.56-1.75.3.14-23.00.pth
BLEU = 18.61, 47.5/23.9/13.6/7.8 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.142.0.58-1.78.3.18-24.06.pth
BLEU = 17.67, 47.0/22.9/12.7/7.1 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.143.0.54-1.72.3.17-23.75.pth
BLEU = 18.49, 47.4/23.7/13.5/7.7 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.14.3.46-31.95.3.35-28.49.pth
BLEU = 4.15, 30.8/8.5/2.5/0.5 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.144.0.50-1.65.3.15-23.35.pth
BLEU = 18.61, 47.7/23.8/13.6/7.8 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.145.0.57-1.76.3.17-23.72.pth
BLEU = 18.51, 47.5/23.8/13.5/7.7 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.146.0.52-1.69.3.18-23.93.pth
BLEU = 18.73, 47.7/23.9/13.7/7.9 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.147.0.53-1.71.3.17-23.76.pth
BLEU = 18.75, 47.7/23.9/13.7/7.9 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.148.0.54-1.72.3.20-24.51.pth
BLEU = 18.28, 47.3/23.5/13.4/7.5 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.149.0.54-1.71.3.19-24.35.pth
BLEU = 18.58, 47.6/23.7/13.5/7.8 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.150.0.52-1.68.3.18-23.99.pth
BLEU = 18.75, 47.5/23.9/13.8/7.9 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.151.0.52-1.68.3.19-24.19.pth
BLEU = 18.58, 47.6/23.8/13.5/7.8 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.152.0.51-1.67.3.18-24.09.pth
BLEU = 18.72, 47.8/24.0/13.7/7.8 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.153.0.52-1.68.3.18-24.00.pth
BLEU = 18.86, 47.5/24.0/13.8/8.0 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.15.3.37-28.95.3.34-28.21.pth
BLEU = 4.54, 31.3/8.8/2.6/0.6 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.154.0.50-1.65.3.19-24.25.pth
BLEU = 18.83, 47.5/24.0/13.8/8.0 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.155.0.49-1.64.3.18-24.01.pth
BLEU = 18.68, 47.5/23.9/13.7/7.8 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.156.0.48-1.62.3.19-24.39.pth
BLEU = 18.68, 47.4/23.9/13.7/7.8 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.157.0.48-1.62.3.21-24.66.pth
BLEU = 18.73, 47.5/23.9/13.7/7.9 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.158.0.48-1.62.3.22-25.07.pth
BLEU = 18.34, 47.4/23.6/13.3/7.6 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.159.0.47-1.60.3.21-24.70.pth
BLEU = 19.06, 48.0/24.2/13.9/8.1 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.160.0.49-1.64.3.20-24.56.pth
BLEU = 18.84, 47.8/24.1/13.8/7.9 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.161.0.47-1.60.3.25-25.79.pth
BLEU = 18.44, 47.2/23.5/13.5/7.8 (BP=1.000, ratio=1.001, hyp_len=28833, ref_len=28803)
Evaluation result for the model: seq-model-mybr.162.0.51-1.66.3.24-25.63.pth
BLEU = 18.69, 47.2/23.7/13.7/8.0 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.163.0.47-1.59.3.24-25.42.pth
BLEU = 18.96, 47.6/24.1/13.9/8.1 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.16.3.24-25.53.3.29-26.78.pth
BLEU = 5.06, 31.9/9.3/3.0/0.7 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.164.0.47-1.60.3.24-25.44.pth
BLEU = 19.00, 47.9/24.1/13.9/8.1 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.165.0.49-1.63.3.26-25.97.pth
BLEU = 18.70, 47.6/23.8/13.6/7.9 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.166.0.44-1.55.3.24-25.56.pth
BLEU = 18.91, 47.8/24.0/13.8/8.0 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.167.0.48-1.61.3.27-26.28.pth
BLEU = 18.82, 47.4/24.0/13.8/8.0 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.168.0.50-1.65.3.25-25.81.pth
BLEU = 18.74, 47.5/23.8/13.7/7.9 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.169.0.45-1.57.3.25-25.92.pth
BLEU = 18.84, 47.5/24.0/13.7/8.1 (BP=1.000, ratio=1.001, hyp_len=28835, ref_len=28803)
Evaluation result for the model: seq-model-mybr.170.0.45-1.57.3.27-26.19.pth
BLEU = 18.60, 47.1/23.7/13.6/7.9 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.171.0.46-1.58.3.25-25.88.pth
BLEU = 19.04, 47.9/24.1/13.9/8.2 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.172.0.45-1.56.3.25-25.66.pth
BLEU = 19.37, 47.9/24.4/14.3/8.4 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.173.0.43-1.54.3.26-26.17.pth
BLEU = 18.73, 47.2/23.9/13.7/8.0 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.17.3.22-24.94.3.27-26.26.pth
BLEU = 5.52, 32.1/9.7/3.3/0.9 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.174.0.44-1.56.3.28-26.57.pth
BLEU = 19.17, 47.9/24.3/14.1/8.2 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.175.0.43-1.54.3.30-27.14.pth
BLEU = 18.53, 47.1/23.6/13.6/7.8 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.176.0.45-1.56.3.29-26.77.pth
BLEU = 19.11, 47.8/24.2/14.1/8.2 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.177.0.41-1.51.3.30-27.17.pth
BLEU = 19.06, 47.2/24.1/14.1/8.2 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.178.0.44-1.55.3.29-26.79.pth
BLEU = 18.84, 47.6/24.0/13.8/8.0 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.179.0.41-1.51.3.29-26.96.pth
BLEU = 19.06, 47.7/24.2/14.0/8.2 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.180.0.41-1.51.3.29-26.81.pth
BLEU = 19.26, 48.0/24.4/14.1/8.3 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.181.0.40-1.49.3.30-27.21.pth
BLEU = 19.22, 47.7/24.4/14.2/8.3 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.182.0.40-1.49.3.31-27.36.pth
BLEU = 19.03, 48.0/24.1/13.9/8.1 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.183.0.41-1.51.3.32-27.61.pth
BLEU = 19.44, 48.0/24.6/14.3/8.4 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.18.3.11-22.41.3.23-25.29.pth
BLEU = 5.99, 33.5/10.3/3.6/1.0 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.184.0.41-1.51.3.32-27.72.pth
BLEU = 19.24, 47.8/24.4/14.1/8.3 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.185.0.40-1.49.3.32-27.72.pth
BLEU = 18.86, 47.4/24.0/13.8/8.0 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.186.0.40-1.49.3.31-27.43.pth
BLEU = 18.95, 47.4/23.8/13.9/8.2 (BP=1.000, ratio=1.002, hyp_len=28851, ref_len=28803)
Evaluation result for the model: seq-model-mybr.187.0.40-1.50.3.32-27.63.pth
BLEU = 19.14, 47.5/24.2/14.1/8.3 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.188.0.39-1.48.3.33-28.08.pth
BLEU = 19.00, 47.9/24.1/13.9/8.1 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.189.0.40-1.50.3.35-28.45.pth
BLEU = 18.79, 47.2/23.9/13.8/8.0 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.190.0.39-1.48.3.34-28.22.pth
BLEU = 18.85, 47.4/23.9/13.9/8.0 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.191.0.40-1.50.3.33-28.02.pth
BLEU = 19.17, 47.8/24.2/14.1/8.3 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.192.0.40-1.49.3.33-27.84.pth
BLEU = 19.36, 48.2/24.5/14.2/8.3 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.19.3.01-20.31.3.20-24.47.pth
BLEU = 6.41, 34.2/11.0/3.9/1.2 (BP=1.000, ratio=1.001, hyp_len=28833, ref_len=28803)
Evaluation result for the model: seq-model-mybr.193.0.39-1.48.3.33-27.99.pth
BLEU = 19.58, 48.1/24.6/14.4/8.6 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.194.0.38-1.46.3.35-28.63.pth
BLEU = 19.36, 48.0/24.5/14.2/8.4 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.195.0.40-1.49.3.35-28.59.pth
BLEU = 19.29, 48.0/24.5/14.2/8.3 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.196.0.36-1.43.3.34-28.34.pth
BLEU = 19.50, 48.0/24.6/14.4/8.5 (BP=1.000, ratio=1.001, hyp_len=28830, ref_len=28803)
Evaluation result for the model: seq-model-mybr.197.0.38-1.46.3.36-28.72.pth
BLEU = 19.46, 48.1/24.7/14.4/8.4 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.198.0.36-1.43.3.36-28.80.pth
BLEU = 19.44, 47.8/24.5/14.4/8.5 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.199.0.39-1.47.3.34-28.12.pth
BLEU = 19.45, 48.0/24.5/14.4/8.4 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.200.0.36-1.43.3.36-28.80.pth
BLEU = 19.41, 48.0/24.5/14.4/8.4 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.201.0.37-1.45.3.38-29.28.pth
BLEU = 19.34, 48.1/24.4/14.2/8.4 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.202.0.37-1.45.3.37-29.04.pth
BLEU = 19.79, 48.2/25.0/14.7/8.7 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.20.2.91-18.43.3.18-24.16.pth
BLEU = 6.91, 34.7/11.4/4.2/1.4 (BP=1.000, ratio=1.001, hyp_len=28835, ref_len=28803)
Evaluation result for the model: seq-model-mybr.203.0.35-1.42.3.38-29.24.pth
BLEU = 19.70, 48.0/24.9/14.6/8.6 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.204.0.36-1.43.3.39-29.77.pth
BLEU = 19.51, 47.7/24.5/14.4/8.6 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.205.0.36-1.43.3.40-30.05.pth
BLEU = 18.90, 47.1/23.9/13.9/8.2 (BP=1.000, ratio=1.002, hyp_len=28851, ref_len=28803)
Evaluation result for the model: seq-model-mybr.206.0.34-1.40.3.38-29.42.pth
BLEU = 19.65, 48.1/24.6/14.5/8.7 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.207.0.38-1.46.3.39-29.67.pth
BLEU = 19.29, 47.7/24.2/14.2/8.4 (BP=1.000, ratio=1.002, hyp_len=28870, ref_len=28803)
Evaluation result for the model: seq-model-mybr.208.0.35-1.42.3.41-30.41.pth
BLEU = 19.08, 47.7/24.3/14.0/8.2 (BP=1.000, ratio=1.002, hyp_len=28872, ref_len=28803)
Evaluation result for the model: seq-model-mybr.209.0.36-1.43.3.40-29.84.pth
BLEU = 19.56, 48.1/24.6/14.4/8.6 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.210.0.35-1.42.3.41-30.29.pth
BLEU = 19.23, 47.8/24.1/14.2/8.4 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.211.0.38-1.46.3.41-30.14.pth
BLEU = 19.40, 47.8/24.3/14.2/8.6 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.212.0.35-1.42.3.40-30.07.pth
BLEU = 19.69, 48.1/24.7/14.6/8.7 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.21.2.95-19.02.3.19-24.30.pth
BLEU = 6.98, 34.9/11.5/4.3/1.4 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.213.0.37-1.44.3.41-30.34.pth
BLEU = 19.57, 47.9/24.7/14.5/8.6 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.214.0.34-1.40.3.41-30.38.pth
BLEU = 19.25, 47.8/24.3/14.2/8.3 (BP=1.000, ratio=1.002, hyp_len=28854, ref_len=28803)
Evaluation result for the model: seq-model-mybr.215.0.32-1.38.3.42-30.64.pth
BLEU = 19.02, 47.6/24.1/14.0/8.2 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.216.0.34-1.40.3.41-30.40.pth
BLEU = 19.43, 48.0/24.4/14.3/8.5 (BP=1.000, ratio=1.002, hyp_len=28852, ref_len=28803)
Evaluation result for the model: seq-model-mybr.217.0.32-1.38.3.44-31.16.pth
BLEU = 19.09, 47.6/24.2/14.0/8.2 (BP=1.000, ratio=1.002, hyp_len=28870, ref_len=28803)
Evaluation result for the model: seq-model-mybr.218.0.34-1.40.3.42-30.51.pth
BLEU = 19.51, 48.1/24.7/14.4/8.5 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.219.0.33-1.39.3.42-30.63.pth
BLEU = 19.58, 48.1/24.7/14.4/8.6 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.220.0.31-1.37.3.43-30.89.pth
BLEU = 19.41, 48.1/24.6/14.3/8.4 (BP=1.000, ratio=1.002, hyp_len=28871, ref_len=28803)
Evaluation result for the model: seq-model-mybr.221.0.30-1.35.3.45-31.55.pth
BLEU = 19.29, 47.8/24.4/14.3/8.3 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.222.0.34-1.40.3.46-31.75.pth
BLEU = 19.13, 48.0/24.3/14.1/8.2 (BP=1.000, ratio=1.002, hyp_len=28851, ref_len=28803)
Evaluation result for the model: seq-model-mybr.22.2.87-17.55.3.17-23.71.pth
BLEU = 7.03, 35.1/11.6/4.3/1.4 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.223.0.32-1.38.3.47-32.14.pth
BLEU = 19.31, 48.1/24.3/14.2/8.4 (BP=1.000, ratio=1.002, hyp_len=28867, ref_len=28803)
Evaluation result for the model: seq-model-mybr.224.0.33-1.40.3.44-31.27.pth
BLEU = 19.75, 48.2/24.8/14.7/8.7 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.225.0.31-1.37.3.45-31.65.pth
BLEU = 19.03, 47.4/24.0/14.0/8.2 (BP=1.000, ratio=1.002, hyp_len=28867, ref_len=28803)
Evaluation result for the model: seq-model-mybr.226.0.31-1.36.3.44-31.05.pth
BLEU = 19.64, 48.0/24.8/14.6/8.6 (BP=1.000, ratio=1.002, hyp_len=28866, ref_len=28803)
Evaluation result for the model: seq-model-mybr.227.0.33-1.39.3.46-31.96.pth
BLEU = 19.32, 47.8/24.5/14.3/8.3 (BP=1.000, ratio=1.002, hyp_len=28870, ref_len=28803)
Evaluation result for the model: seq-model-mybr.228.0.32-1.38.3.43-31.00.pth
BLEU = 19.85, 48.1/24.9/14.7/8.8 (BP=1.000, ratio=1.002, hyp_len=28870, ref_len=28803)
Evaluation result for the model: seq-model-mybr.229.0.34-1.40.3.46-31.92.pth
BLEU = 19.52, 47.9/24.5/14.5/8.6 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.230.0.31-1.36.3.46-31.70.pth
BLEU = 19.26, 48.0/24.4/14.2/8.3 (BP=1.000, ratio=1.002, hyp_len=28852, ref_len=28803)
Evaluation result for the model: seq-model-mybr.231.0.31-1.36.3.46-31.95.pth
BLEU = 19.59, 48.1/24.7/14.5/8.6 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.232.0.31-1.37.3.47-32.14.pth
BLEU = 19.63, 48.1/24.6/14.5/8.6 (BP=1.000, ratio=1.002, hyp_len=28871, ref_len=28803)
Evaluation result for the model: seq-model-mybr.23.2.79-16.33.3.22-25.00.pth
BLEU = 7.08, 35.4/11.7/4.4/1.4 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.233.0.31-1.36.3.48-32.46.pth
BLEU = 19.77, 48.1/24.9/14.6/8.7 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.234.0.31-1.36.3.48-32.52.pth
BLEU = 19.54, 47.8/24.6/14.5/8.6 (BP=1.000, ratio=1.002, hyp_len=28854, ref_len=28803)
Evaluation result for the model: seq-model-mybr.235.0.28-1.33.3.50-32.96.pth
BLEU = 19.95, 48.5/25.0/14.7/8.9 (BP=1.000, ratio=1.001, hyp_len=28833, ref_len=28803)
Evaluation result for the model: seq-model-mybr.236.0.29-1.33.3.49-32.87.pth
BLEU = 19.77, 48.2/24.8/14.6/8.7 (BP=1.000, ratio=1.002, hyp_len=28851, ref_len=28803)
Evaluation result for the model: seq-model-mybr.237.0.32-1.38.3.49-32.89.pth
BLEU = 19.76, 48.2/24.8/14.6/8.7 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.238.0.30-1.34.3.49-32.79.pth
BLEU = 19.55, 48.1/24.7/14.5/8.5 (BP=1.000, ratio=1.001, hyp_len=28834, ref_len=28803)
Evaluation result for the model: seq-model-mybr.239.0.29-1.33.3.49-32.78.pth
BLEU = 19.82, 48.2/24.9/14.7/8.7 (BP=1.000, ratio=1.002, hyp_len=28855, ref_len=28803)
Evaluation result for the model: seq-model-mybr.240.0.32-1.37.3.49-32.88.pth
BLEU = 19.61, 48.2/24.6/14.5/8.6 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.241.0.31-1.36.3.53-33.97.pth
BLEU = 19.58, 47.8/24.6/14.5/8.6 (BP=1.000, ratio=1.002, hyp_len=28857, ref_len=28803)
Evaluation result for the model: seq-model-mybr.242.0.29-1.34.3.49-32.70.pth
BLEU = 19.89, 48.2/24.9/14.8/8.8 (BP=1.000, ratio=1.001, hyp_len=28834, ref_len=28803)
Evaluation result for the model: seq-model-mybr.24.2.71-14.96.3.13-22.98.pth
BLEU = 7.73, 36.3/12.5/4.8/1.6 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.243.0.29-1.33.3.49-32.85.pth
BLEU = 19.85, 48.1/24.8/14.7/8.8 (BP=1.000, ratio=1.001, hyp_len=28838, ref_len=28803)
Evaluation result for the model: seq-model-mybr.244.0.27-1.31.3.50-33.23.pth
BLEU = 19.82, 48.2/24.8/14.7/8.8 (BP=1.000, ratio=1.001, hyp_len=28835, ref_len=28803)
Evaluation result for the model: seq-model-mybr.245.0.28-1.32.3.51-33.32.pth
BLEU = 19.56, 47.8/24.5/14.5/8.6 (BP=1.000, ratio=1.002, hyp_len=28851, ref_len=28803)
Evaluation result for the model: seq-model-mybr.246.0.28-1.32.3.55-34.79.pth
BLEU = 19.28, 47.4/24.3/14.3/8.4 (BP=1.000, ratio=1.002, hyp_len=28867, ref_len=28803)
Evaluation result for the model: seq-model-mybr.247.0.29-1.34.3.52-33.69.pth
BLEU = 19.95, 48.5/25.0/14.8/8.9 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.248.0.29-1.33.3.56-35.11.pth
BLEU = 19.34, 47.7/24.5/14.3/8.4 (BP=1.000, ratio=1.002, hyp_len=28870, ref_len=28803)
Evaluation result for the model: seq-model-mybr.249.0.28-1.33.3.52-33.89.pth
BLEU = 19.62, 48.0/24.7/14.5/8.6 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.250.0.28-1.32.3.52-33.85.pth
BLEU = 19.96, 48.5/25.0/14.7/8.9 (BP=1.000, ratio=1.001, hyp_len=28836, ref_len=28803)
Evaluation result for the model: seq-model-mybr.251.0.29-1.33.3.65-38.34.pth
BLEU = 18.69, 46.3/23.7/13.8/8.1 (BP=1.000, ratio=1.002, hyp_len=28875, ref_len=28803)
Evaluation result for the model: seq-model-mybr.252.0.28-1.32.3.53-34.22.pth
BLEU = 19.63, 48.3/24.6/14.5/8.6 (BP=1.000, ratio=1.002, hyp_len=28870, ref_len=28803)
Evaluation result for the model: seq-model-mybr.25.2.64-14.06.3.10-22.21.pth
BLEU = 8.10, 36.4/13.0/5.1/1.8 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.253.0.29-1.34.3.54-34.37.pth
BLEU = 19.80, 48.1/24.9/14.6/8.8 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.254.0.28-1.32.3.54-34.58.pth
BLEU = 19.59, 48.0/24.6/14.5/8.6 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.255.0.29-1.34.3.54-34.62.pth
BLEU = 19.45, 47.6/24.3/14.4/8.6 (BP=1.000, ratio=1.002, hyp_len=28871, ref_len=28803)
Evaluation result for the model: seq-model-mybr.256.0.27-1.31.3.56-35.06.pth
BLEU = 19.58, 47.9/24.6/14.5/8.6 (BP=1.000, ratio=1.003, hyp_len=28876, ref_len=28803)
Evaluation result for the model: seq-model-mybr.257.0.27-1.30.3.58-35.90.pth
BLEU = 19.60, 48.0/24.7/14.5/8.6 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.258.0.26-1.29.3.57-35.55.pth
BLEU = 19.78, 48.2/24.8/14.6/8.8 (BP=1.000, ratio=1.002, hyp_len=28857, ref_len=28803)
Evaluation result for the model: seq-model-mybr.259.0.26-1.30.3.54-34.52.pth
BLEU = 19.59, 47.8/24.5/14.5/8.7 (BP=1.000, ratio=1.001, hyp_len=28836, ref_len=28803)
Evaluation result for the model: seq-model-mybr.260.0.28-1.32.3.55-34.75.pth
BLEU = 19.67, 48.2/24.7/14.5/8.7 (BP=1.000, ratio=1.001, hyp_len=28837, ref_len=28803)
Evaluation result for the model: seq-model-mybr.261.0.28-1.32.3.56-35.19.pth
BLEU = 19.52, 48.0/24.5/14.4/8.6 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.262.0.25-1.29.3.57-35.41.pth
BLEU = 19.76, 48.0/24.7/14.6/8.8 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.26.2.62-13.79.3.08-21.83.pth
BLEU = 8.50, 37.2/13.4/5.4/1.9 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.263.0.25-1.29.3.59-36.25.pth
BLEU = 19.76, 47.8/24.6/14.7/8.8 (BP=1.000, ratio=1.002, hyp_len=28870, ref_len=28803)
Evaluation result for the model: seq-model-mybr.264.0.29-1.34.3.59-36.19.pth
BLEU = 19.70, 48.0/24.6/14.6/8.7 (BP=1.000, ratio=1.002, hyp_len=28853, ref_len=28803)
Evaluation result for the model: seq-model-mybr.265.0.27-1.31.3.57-35.48.pth
BLEU = 19.88, 48.1/24.8/14.8/8.9 (BP=1.000, ratio=1.002, hyp_len=28872, ref_len=28803)
Evaluation result for the model: seq-model-mybr.266.0.26-1.30.3.58-35.74.pth
BLEU = 19.42, 48.1/24.5/14.3/8.4 (BP=1.000, ratio=1.002, hyp_len=28849, ref_len=28803)
Evaluation result for the model: seq-model-mybr.267.0.26-1.29.3.59-36.40.pth
BLEU = 19.75, 48.4/24.8/14.6/8.7 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.268.0.25-1.28.3.60-36.61.pth
BLEU = 19.65, 48.0/24.7/14.5/8.7 (BP=1.000, ratio=1.002, hyp_len=28851, ref_len=28803)
Evaluation result for the model: seq-model-mybr.269.0.27-1.31.3.61-36.93.pth
BLEU = 19.28, 48.2/24.4/14.2/8.3 (BP=1.000, ratio=1.002, hyp_len=28851, ref_len=28803)
Evaluation result for the model: seq-model-mybr.270.0.24-1.27.3.62-37.27.pth
BLEU = 19.41, 47.5/24.4/14.4/8.5 (BP=1.000, ratio=1.002, hyp_len=28853, ref_len=28803)
Evaluation result for the model: seq-model-mybr.271.0.26-1.29.3.60-36.65.pth
BLEU = 19.83, 48.0/24.8/14.8/8.8 (BP=1.000, ratio=1.002, hyp_len=28858, ref_len=28803)
Evaluation result for the model: seq-model-mybr.272.0.27-1.31.3.64-38.14.pth
BLEU = 19.43, 47.4/24.4/14.5/8.5 (BP=1.000, ratio=1.002, hyp_len=28869, ref_len=28803)
Evaluation result for the model: seq-model-mybr.27.2.53-12.58.3.11-22.39.pth
BLEU = 8.35, 37.3/13.3/5.2/1.9 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.273.0.24-1.27.3.61-37.14.pth
BLEU = 19.55, 47.9/24.5/14.5/8.6 (BP=1.000, ratio=1.002, hyp_len=28874, ref_len=28803)
Evaluation result for the model: seq-model-mybr.274.0.25-1.28.3.59-36.38.pth
BLEU = 20.04, 48.5/25.2/14.9/8.8 (BP=1.000, ratio=1.002, hyp_len=28852, ref_len=28803)
Evaluation result for the model: seq-model-mybr.275.0.24-1.28.3.63-37.54.pth
BLEU = 19.74, 48.2/24.8/14.6/8.7 (BP=1.000, ratio=1.002, hyp_len=28874, ref_len=28803)
Evaluation result for the model: seq-model-mybr.276.0.24-1.27.3.65-38.51.pth
BLEU = 19.63, 48.1/24.6/14.6/8.6 (BP=1.000, ratio=1.002, hyp_len=28875, ref_len=28803)
Evaluation result for the model: seq-model-mybr.277.0.24-1.27.3.62-37.16.pth
BLEU = 19.81, 48.3/24.9/14.7/8.7 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.278.0.26-1.30.3.64-38.07.pth
BLEU = 19.65, 47.8/24.5/14.5/8.7 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.279.0.26-1.30.3.64-38.25.pth
BLEU = 19.57, 48.1/24.7/14.5/8.6 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.280.0.26-1.30.3.71-40.84.pth
BLEU = 18.49, 46.4/23.5/13.6/7.9 (BP=1.000, ratio=1.002, hyp_len=28854, ref_len=28803)
Evaluation result for the model: seq-model-mybr.281.0.25-1.28.3.64-38.17.pth
BLEU = 20.03, 48.2/25.0/14.8/9.0 (BP=1.000, ratio=1.002, hyp_len=28871, ref_len=28803)
Evaluation result for the model: seq-model-mybr.282.0.24-1.27.3.65-38.37.pth
BLEU = 19.78, 48.1/24.8/14.6/8.8 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.28.2.47-11.84.3.05-21.16.pth
BLEU = 9.36, 38.1/14.0/6.0/2.4 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.283.0.25-1.29.3.63-37.54.pth
BLEU = 19.77, 48.4/24.7/14.6/8.8 (BP=1.000, ratio=1.002, hyp_len=28851, ref_len=28803)
Evaluation result for the model: seq-model-mybr.284.0.23-1.25.3.66-38.68.pth
BLEU = 19.47, 47.6/24.5/14.4/8.6 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.285.0.24-1.27.3.64-38.04.pth
BLEU = 19.90, 48.3/24.9/14.7/8.8 (BP=1.000, ratio=1.002, hyp_len=28853, ref_len=28803)
Evaluation result for the model: seq-model-mybr.286.0.26-1.30.3.64-38.28.pth
BLEU = 19.82, 48.4/24.8/14.6/8.8 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.287.0.32-1.38.3.72-41.36.pth
BLEU = 18.84, 46.8/23.7/13.9/8.2 (BP=1.000, ratio=1.001, hyp_len=28833, ref_len=28803)
Evaluation result for the model: seq-model-mybr.288.0.23-1.26.3.66-38.87.pth
BLEU = 20.16, 48.6/25.2/15.0/9.0 (BP=1.000, ratio=1.002, hyp_len=28875, ref_len=28803)
Evaluation result for the model: seq-model-mybr.289.0.24-1.27.3.65-38.49.pth
BLEU = 20.00, 48.4/25.0/14.8/8.9 (BP=1.000, ratio=1.003, hyp_len=28877, ref_len=28803)
Evaluation result for the model: seq-model-mybr.290.0.23-1.25.3.64-38.02.pth
BLEU = 20.17, 48.5/25.1/15.0/9.1 (BP=1.000, ratio=1.002, hyp_len=28869, ref_len=28803)
Evaluation result for the model: seq-model-mybr.291.0.23-1.26.3.67-39.26.pth
BLEU = 19.67, 48.4/24.7/14.5/8.6 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.292.0.20-1.23.3.69-39.97.pth
BLEU = 19.71, 48.3/24.7/14.6/8.7 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.29.2.44-11.45.3.04-20.88.pth
BLEU = 9.56, 38.2/14.2/6.1/2.5 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.293.0.24-1.27.3.69-39.88.pth
BLEU = 19.78, 48.3/24.8/14.6/8.7 (BP=1.000, ratio=1.002, hyp_len=28851, ref_len=28803)
Evaluation result for the model: seq-model-mybr.294.0.24-1.27.3.69-40.09.pth
BLEU = 20.16, 48.5/25.2/14.9/9.1 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.295.0.24-1.27.3.68-39.79.pth
BLEU = 20.18, 48.6/25.2/15.0/9.0 (BP=1.000, ratio=1.002, hyp_len=28851, ref_len=28803)
Evaluation result for the model: seq-model-mybr.296.0.23-1.26.3.71-40.69.pth
BLEU = 19.79, 48.2/24.9/14.7/8.7 (BP=1.000, ratio=1.002, hyp_len=28869, ref_len=28803)
Evaluation result for the model: seq-model-mybr.297.0.22-1.24.3.67-39.41.pth
BLEU = 20.07, 48.7/25.1/14.9/8.9 (BP=1.000, ratio=1.002, hyp_len=28869, ref_len=28803)
Evaluation result for the model: seq-model-mybr.298.0.22-1.24.3.69-40.06.pth
BLEU = 20.04, 48.6/25.1/14.8/8.9 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.299.0.23-1.25.3.71-40.71.pth
BLEU = 19.73, 48.4/24.7/14.6/8.7 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.300.0.23-1.26.3.70-40.45.pth
BLEU = 19.88, 48.3/24.9/14.7/8.8 (BP=1.000, ratio=1.002, hyp_len=28856, ref_len=28803)
Evaluation result for the model: seq-model-mybr.30.2.41-11.15.3.08-21.69.pth
BLEU = 9.20, 38.1/14.0/5.8/2.3 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.31.2.34-10.36.3.01-20.36.pth
BLEU = 10.31, 38.9/14.9/6.7/2.9 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.32.2.26-9.63.3.07-21.50.pth
BLEU = 9.27, 37.9/14.2/5.9/2.3 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.33.2.21-9.09.3.01-20.28.pth
BLEU = 10.51, 39.3/15.2/6.8/3.0 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.34.2.12-8.37.3.01-20.36.pth
BLEU = 10.29, 39.5/15.2/6.7/2.8 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.35.2.16-8.67.3.00-20.06.pth
BLEU = 10.68, 39.8/15.5/6.9/3.1 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.36.2.09-8.10.3.00-20.05.pth
BLEU = 10.80, 39.9/15.7/7.0/3.1 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.37.2.06-7.86.2.98-19.63.pth
BLEU = 11.25, 40.2/16.1/7.4/3.4 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.38.2.04-7.72.2.97-19.49.pth
BLEU = 10.98, 40.4/15.8/7.0/3.2 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.39.1.94-6.99.2.95-19.12.pth
BLEU = 11.63, 41.0/16.7/7.6/3.5 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.40.1.96-7.11.2.99-19.86.pth
BLEU = 11.61, 40.8/16.4/7.5/3.6 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.41.1.87-6.49.2.94-18.88.pth
BLEU = 11.98, 41.3/17.0/8.0/3.7 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.42.1.91-6.76.2.98-19.75.pth
BLEU = 11.47, 41.2/16.6/7.5/3.4 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.43.1.90-6.66.2.96-19.24.pth
BLEU = 11.84, 41.5/16.9/7.8/3.6 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.44.1.82-6.18.2.93-18.81.pth
BLEU = 12.37, 41.7/17.5/8.3/3.9 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.45.1.77-5.87.2.98-19.60.pth
BLEU = 12.18, 41.3/17.2/8.1/3.8 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.46.1.76-5.79.2.94-18.92.pth
BLEU = 12.25, 41.8/17.3/8.1/3.8 (BP=1.000, ratio=1.002, hyp_len=28855, ref_len=28803)
Evaluation result for the model: seq-model-mybr.47.1.73-5.63.2.94-18.83.pth
BLEU = 12.51, 42.1/17.7/8.3/3.9 (BP=1.000, ratio=1.002, hyp_len=28855, ref_len=28803)
Evaluation result for the model: seq-model-mybr.48.1.67-5.31.2.95-19.07.pth
BLEU = 12.46, 41.7/17.6/8.3/3.9 (BP=1.000, ratio=1.002, hyp_len=28852, ref_len=28803)
Evaluation result for the model: seq-model-mybr.49.1.66-5.27.2.91-18.42.pth
BLEU = 13.20, 42.8/18.4/8.9/4.3 (BP=1.000, ratio=1.002, hyp_len=28855, ref_len=28803)
Evaluation result for the model: seq-model-mybr.50.1.68-5.35.2.93-18.70.pth
BLEU = 12.72, 42.4/18.0/8.5/4.0 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.51.1.63-5.08.2.92-18.63.pth
BLEU = 13.19, 43.1/18.4/8.9/4.3 (BP=1.000, ratio=1.002, hyp_len=28855, ref_len=28803)
Evaluation result for the model: seq-model-mybr.52.1.56-4.75.2.93-18.74.pth
BLEU = 13.01, 42.5/18.1/8.7/4.3 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.53.1.54-4.66.2.91-18.31.pth
BLEU = 13.51, 43.1/18.6/9.1/4.5 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.54.1.52-4.59.2.92-18.54.pth
BLEU = 13.36, 43.2/18.6/9.0/4.4 (BP=1.000, ratio=1.002, hyp_len=28858, ref_len=28803)
Evaluation result for the model: seq-model-mybr.55.1.53-4.60.2.91-18.37.pth
BLEU = 13.73, 43.5/19.0/9.3/4.6 (BP=1.000, ratio=1.002, hyp_len=28857, ref_len=28803)
Evaluation result for the model: seq-model-mybr.56.1.45-4.27.2.91-18.35.pth
BLEU = 13.88, 43.4/19.2/9.4/4.7 (BP=1.000, ratio=1.002, hyp_len=28852, ref_len=28803)
Evaluation result for the model: seq-model-mybr.57.1.42-4.13.2.91-18.32.pth
BLEU = 14.01, 43.6/19.2/9.6/4.8 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.58.1.42-4.14.2.94-18.97.pth
BLEU = 13.67, 42.6/18.8/9.4/4.7 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.59.1.38-3.98.2.91-18.27.pth
BLEU = 14.35, 44.0/19.4/9.8/5.0 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.60.1.45-4.25.2.94-18.92.pth
BLEU = 13.92, 43.4/19.1/9.5/4.8 (BP=1.000, ratio=1.002, hyp_len=28852, ref_len=28803)
Evaluation result for the model: seq-model-mybr.61.1.37-3.95.2.92-18.60.pth
BLEU = 14.38, 43.9/19.6/9.9/5.0 (BP=1.000, ratio=1.002, hyp_len=28852, ref_len=28803)
Evaluation result for the model: seq-model-mybr.62.1.38-3.98.2.92-18.59.pth
BLEU = 14.36, 43.8/19.5/9.9/5.0 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.63.1.29-3.63.2.96-19.32.pth
BLEU = 14.44, 43.5/19.6/10.0/5.1 (BP=1.000, ratio=1.002, hyp_len=28852, ref_len=28803)
Evaluation result for the model: seq-model-mybr.64.1.30-3.67.2.92-18.57.pth
BLEU = 14.41, 43.8/19.6/10.0/5.0 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.65.1.28-3.60.2.93-18.67.pth
BLEU = 14.58, 44.1/19.8/10.0/5.2 (BP=1.000, ratio=1.002, hyp_len=28855, ref_len=28803)
Evaluation result for the model: seq-model-mybr.66.1.27-3.55.2.94-18.92.pth
BLEU = 14.73, 44.4/20.0/10.2/5.2 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: seq-model-mybr.67.1.21-3.35.2.93-18.82.pth
BLEU = 14.95, 44.4/20.2/10.4/5.3 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.68.1.24-3.47.2.93-18.76.pth
BLEU = 15.01, 44.5/20.3/10.4/5.4 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.69.1.25-3.51.2.94-18.84.pth
BLEU = 14.80, 44.6/20.1/10.2/5.2 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.70.1.27-3.54.2.93-18.80.pth
BLEU = 14.94, 44.4/20.0/10.4/5.4 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.71.1.16-3.19.2.92-18.47.pth
BLEU = 15.24, 44.8/20.6/10.7/5.5 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.72.1.17-3.23.2.94-18.86.pth
BLEU = 15.21, 44.6/20.5/10.6/5.5 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.73.1.21-3.36.2.94-18.98.pth
BLEU = 15.39, 44.9/20.6/10.8/5.7 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.74.1.17-3.22.2.96-19.24.pth
BLEU = 15.35, 44.7/20.6/10.7/5.6 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.75.1.10-3.01.2.94-18.85.pth
BLEU = 15.76, 45.0/21.0/11.1/5.9 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.76.1.08-2.94.2.96-19.33.pth
BLEU = 14.96, 44.4/20.3/10.5/5.3 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.77.1.09-2.98.2.93-18.78.pth
BLEU = 15.93, 45.3/21.4/11.2/5.9 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.78.1.12-3.06.2.95-19.05.pth
BLEU = 15.79, 45.3/21.1/11.1/5.9 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.79.1.07-2.91.2.95-19.04.pth
BLEU = 15.90, 45.3/21.1/11.2/5.9 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.80.1.05-2.85.2.94-18.88.pth
BLEU = 16.17, 45.6/21.4/11.4/6.1 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.81.1.06-2.88.2.96-19.27.pth
BLEU = 16.05, 45.5/21.5/11.4/6.0 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.82.1.05-2.85.2.95-19.08.pth
BLEU = 16.21, 45.8/21.4/11.4/6.2 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.83.0.98-2.67.2.99-19.85.pth
BLEU = 16.12, 45.2/21.3/11.4/6.1 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.84.1.03-2.80.2.98-19.60.pth
BLEU = 16.26, 45.4/21.5/11.6/6.2 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.85.0.96-2.62.2.97-19.51.pth
BLEU = 16.09, 45.3/21.4/11.4/6.1 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.86.1.07-2.90.3.00-20.11.pth
BLEU = 15.33, 44.9/20.6/10.7/5.6 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.87.0.96-2.61.2.98-19.70.pth
BLEU = 16.54, 45.8/21.8/11.8/6.3 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-mybr.88.0.95-2.58.2.97-19.57.pth
BLEU = 16.55, 45.9/21.9/11.7/6.4 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.89.0.99-2.68.2.99-19.88.pth
BLEU = 16.66, 45.7/21.9/11.9/6.5 (BP=1.000, ratio=1.002, hyp_len=28849, ref_len=28803)
Evaluation result for the model: seq-model-mybr.90.0.92-2.51.2.99-19.97.pth
BLEU = 16.30, 45.6/21.7/11.6/6.2 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.91.0.93-2.54.2.98-19.68.pth
BLEU = 16.78, 46.0/22.1/12.0/6.5 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.92.0.92-2.50.2.99-19.86.pth
BLEU = 16.61, 45.8/22.0/11.9/6.4 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.93.0.93-2.53.2.98-19.64.pth
BLEU = 17.08, 46.3/22.3/12.3/6.7 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.94.0.91-2.47.3.03-20.68.pth
BLEU = 16.35, 45.6/21.7/11.6/6.2 (BP=1.000, ratio=1.002, hyp_len=28849, ref_len=28803)
Evaluation result for the model: seq-model-mybr.95.0.91-2.48.3.03-20.60.pth
BLEU = 16.66, 45.6/22.1/11.9/6.4 (BP=1.000, ratio=1.001, hyp_len=28833, ref_len=28803)
Evaluation result for the model: seq-model-mybr.96.0.90-2.45.3.01-20.28.pth
BLEU = 16.83, 46.0/22.1/12.1/6.5 (BP=1.000, ratio=1.001, hyp_len=28832, ref_len=28803)
Evaluation result for the model: seq-model-mybr.97.0.85-2.33.3.01-20.22.pth
BLEU = 16.78, 46.3/22.0/11.9/6.5 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: seq-model-mybr.98.0.89-2.45.3.02-20.43.pth
BLEU = 16.76, 45.9/22.0/12.0/6.5 (BP=1.000, ratio=1.002, hyp_len=28847, ref_len=28803)
Evaluation result for the model: seq-model-mybr.99.0.88-2.40.3.00-20.17.pth
BLEU = 16.99, 46.5/22.3/12.1/6.6 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
/home/ye/exp/simple-nmt

real	179m22.590s
user	175m45.462s
sys	6m42.050s
(simple-nmt) ye@:~/exp/simple-nmt$
```

Best model and best score for my-br, seq2seq with simple-nmt is:  

```
Evaluation result for the model: seq-model-mybr.295.0.24-1.27.3.68-39.79.pth
BLEU = 20.18, 48.6/25.2/15.0/9.0 (BP=1.000, ratio=1.002, hyp_len=28851, ref_len=28803)
```

bash script for br-my testing ...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, Thailand
# Last updated: 9 April 2022
# find all models and parse to translate.py for testing and multi-bleu.perl for evaluation with BLEU score
# updated for br-my

cd ./model/braille/seq2seq/br-my/;

for i in `ls *.pth | sort -V`; do
   MODEL=$i;

   # Testing
   python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang brmy < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br > $MODEL.hyp

   # Evaluation with BLEU Score
   echo "Evaluation result for the model: $MODEL" | tee -a eval-results-brmy-seq2seq-300epoch.txt;
   cat $MODEL.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee  -a eval-results-brmy-seq2seq-300epoch.txt;

done

cd -;

```

testing for br-my ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-loop-seq2seq-brmy.sh
Evaluation result for the model: seq-model-brmy.01.5.53-251.34.4.60-99.60.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
BLEU = 0.00, 16.4/1.8/0.0/0.0 (BP=1.000, ratio=1.013, hyp_len=29169, ref_len=28803)
Evaluation result for the model: seq-model-brmy.02.5.19-180.19.4.28-71.90.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
BLEU = 0.00, 17.8/2.3/0.0/0.0 (BP=1.000, ratio=1.000, hyp_len=28809, ref_len=28803)
Evaluation result for the model: seq-model-brmy.03.4.91-135.58.4.07-58.65.pth
BLEU = 1.05, 19.9/2.7/0.4/0.1 (BP=1.000, ratio=1.000, hyp_len=28808, ref_len=28803)
Evaluation result for the model: seq-model-brmy.04.4.66-105.76.3.95-51.98.pth
BLEU = 0.81, 21.1/3.4/0.4/0.0 (BP=1.000, ratio=1.000, hyp_len=28804, ref_len=28803)
Evaluation result for the model: seq-model-brmy.05.4.55-94.39.3.87-47.84.pth
BLEU = 1.35, 21.9/3.8/0.6/0.1 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.06.4.36-77.92.3.80-44.53.pth
BLEU = 1.57, 23.6/4.2/0.8/0.1 (BP=1.000, ratio=1.002, hyp_len=28848, ref_len=28803)
Evaluation result for the model: seq-model-brmy.07.4.25-70.40.3.65-38.64.pth
BLEU = 2.15, 25.1/5.6/1.2/0.1 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.08.4.10-60.27.3.57-35.61.pth
BLEU = 2.37, 27.1/6.5/1.3/0.1 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.09.3.95-51.74.3.51-33.46.pth
BLEU = 2.71, 28.3/7.0/1.6/0.2 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.10.3.82-45.62.3.45-31.60.pth
BLEU = 3.15, 29.2/7.3/1.7/0.3 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.11.3.73-41.72.3.43-30.77.pth
BLEU = 3.67, 30.0/8.0/2.1/0.4 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.12.3.61-36.92.3.35-28.44.pth
BLEU = 4.30, 30.5/8.5/2.4/0.5 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.13.3.43-30.72.3.31-27.52.pth
BLEU = 4.77, 32.5/9.4/2.8/0.6 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.14.3.33-27.95.3.26-26.08.pth
BLEU = 5.10, 32.9/9.6/3.0/0.7 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.15.3.34-28.12.3.29-26.79.pth
BLEU = 5.31, 31.2/9.6/3.2/0.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.16.3.25-25.71.3.20-24.61.pth
BLEU = 5.92, 34.1/10.5/3.6/1.0 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.17.3.09-22.03.3.16-23.49.pth
BLEU = 6.36, 34.2/11.1/3.9/1.1 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.18.3.06-21.42.3.15-23.33.pth
BLEU = 6.38, 34.4/11.0/3.8/1.1 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.19.2.93-18.64.3.11-22.40.pth
BLEU = 7.37, 36.0/12.0/4.5/1.5 (BP=1.000, ratio=1.001, hyp_len=28825, ref_len=28803)
Evaluation result for the model: seq-model-brmy.20.2.89-17.98.3.09-21.91.pth
BLEU = 7.70, 36.2/12.3/4.7/1.7 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.21.2.78-16.18.3.05-21.17.pth
BLEU = 8.17, 36.9/12.8/5.0/1.9 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.22.2.71-15.00.3.08-21.72.pth
BLEU = 7.73, 35.9/12.5/4.8/1.7 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.23.2.69-14.71.3.00-20.17.pth
BLEU = 8.60, 37.6/13.4/5.4/2.0 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.24.2.64-14.04.3.00-20.04.pth
BLEU = 9.24, 38.1/14.0/5.8/2.3 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.25.2.53-12.61.2.98-19.72.pth
BLEU = 9.13, 38.6/13.9/5.7/2.2 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.26.2.54-12.73.2.98-19.62.pth
BLEU = 9.38, 38.4/14.2/6.0/2.4 (BP=1.000, ratio=1.001, hyp_len=28822, ref_len=28803)
Evaluation result for the model: seq-model-brmy.27.2.46-11.73.2.98-19.60.pth
BLEU = 9.53, 38.9/14.6/6.2/2.4 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.28.2.37-10.74.2.93-18.70.pth
BLEU = 10.31, 39.8/15.4/6.7/2.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.29.2.27-9.72.2.93-18.65.pth
BLEU = 10.45, 40.2/15.4/6.7/2.9 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.30.2.30-9.97.2.94-18.97.pth
BLEU = 10.54, 39.7/15.5/6.8/2.9 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.31.2.19-8.93.2.91-18.39.pth
BLEU = 11.23, 40.4/16.2/7.5/3.2 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.32.2.17-8.75.2.91-18.35.pth
BLEU = 10.82, 40.2/15.8/7.0/3.1 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.33.2.15-8.57.2.89-17.97.pth
BLEU = 11.46, 41.3/16.5/7.5/3.4 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.34.2.09-8.12.2.88-17.83.pth
BLEU = 11.70, 41.5/16.8/7.8/3.5 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.35.2.07-7.89.2.88-17.80.pth
BLEU = 11.76, 41.5/16.8/7.8/3.5 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.36.1.95-7.00.2.89-18.03.pth
BLEU = 12.03, 41.5/17.0/8.0/3.7 (BP=1.000, ratio=1.000, hyp_len=28806, ref_len=28803)
Evaluation result for the model: seq-model-brmy.37.1.98-7.25.2.86-17.43.pth
BLEU = 12.27, 42.0/17.3/8.2/3.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.38.1.92-6.79.2.84-17.06.pth
BLEU = 12.39, 42.2/17.6/8.3/3.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.39.1.94-6.98.2.85-17.27.pth
BLEU = 12.56, 42.3/17.6/8.4/4.0 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.40.1.85-6.36.2.84-17.19.pth
BLEU = 12.89, 42.5/18.0/8.7/4.1 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.41.1.83-6.21.2.82-16.85.pth
BLEU = 13.07, 42.8/18.3/8.8/4.2 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.42.1.83-6.23.2.82-16.71.pth
BLEU = 13.23, 43.2/18.4/9.0/4.3 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.43.1.75-5.76.2.81-16.58.pth
BLEU = 13.48, 43.5/18.6/9.2/4.4 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.44.1.72-5.58.2.82-16.80.pth
BLEU = 13.40, 43.4/18.5/9.1/4.4 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.45.1.72-5.57.2.83-16.91.pth
BLEU = 13.59, 43.7/18.8/9.3/4.5 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.46.1.63-5.13.2.82-16.72.pth
BLEU = 13.55, 44.1/18.9/9.2/4.4 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.47.1.64-5.14.2.80-16.43.pth
BLEU = 13.83, 44.0/19.1/9.5/4.6 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.48.1.65-5.22.2.81-16.54.pth
BLEU = 14.12, 43.9/19.5/9.7/4.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.49.1.58-4.86.2.80-16.44.pth
BLEU = 13.98, 44.2/19.3/9.6/4.7 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.50.1.59-4.89.2.81-16.54.pth
BLEU = 14.13, 44.1/19.5/9.8/4.7 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.51.1.54-4.68.2.80-16.37.pth
BLEU = 14.42, 44.5/19.6/10.0/5.0 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.52.1.49-4.46.2.81-16.57.pth
BLEU = 14.08, 44.3/19.6/9.7/4.7 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.53.1.43-4.18.2.79-16.33.pth
BLEU = 14.59, 44.5/19.9/10.1/5.1 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.54.1.49-4.42.2.92-18.49.pth
BLEU = 13.03, 42.4/18.2/8.9/4.2 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.55.1.39-4.03.2.81-16.68.pth
BLEU = 14.61, 44.7/20.0/10.1/5.0 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.56.1.43-4.18.2.86-17.47.pth
BLEU = 14.22, 43.5/19.7/9.9/4.8 (BP=1.000, ratio=1.001, hyp_len=28829, ref_len=28803)
Evaluation result for the model: seq-model-brmy.57.1.40-4.05.2.79-16.22.pth
BLEU = 15.08, 44.9/20.5/10.5/5.4 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.58.1.38-3.99.2.78-16.12.pth
BLEU = 15.01, 45.1/20.2/10.5/5.3 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.59.1.35-3.86.2.80-16.41.pth
BLEU = 14.89, 45.1/20.3/10.4/5.2 (BP=1.000, ratio=1.001, hyp_len=28830, ref_len=28803)
Evaluation result for the model: seq-model-brmy.60.1.30-3.67.2.79-16.20.pth
BLEU = 15.50, 45.4/20.8/10.9/5.6 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.61.1.29-3.64.2.79-16.29.pth
BLEU = 15.14, 45.1/20.4/10.5/5.4 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.62.1.28-3.60.2.80-16.42.pth
BLEU = 15.87, 45.5/21.1/11.2/5.9 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.63.1.25-3.50.2.80-16.41.pth
BLEU = 15.59, 45.7/20.9/11.0/5.6 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.64.1.28-3.61.2.92-18.46.pth
BLEU = 14.09, 43.3/19.4/9.8/4.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.65.1.20-3.33.2.80-16.45.pth
BLEU = 15.74, 46.0/21.2/11.1/5.7 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.66.1.21-3.37.2.79-16.34.pth
BLEU = 15.97, 45.8/21.2/11.3/5.9 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.67.1.18-3.26.2.80-16.42.pth
BLEU = 16.03, 46.1/21.5/11.3/5.9 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.68.1.19-3.28.2.80-16.50.pth
BLEU = 16.24, 46.1/21.7/11.5/6.0 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.69.1.12-3.07.2.80-16.37.pth
BLEU = 16.54, 46.5/21.9/11.8/6.2 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.70.1.13-3.10.2.82-16.75.pth
BLEU = 16.20, 46.1/21.5/11.5/6.0 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.71.1.10-3.00.2.80-16.48.pth
BLEU = 16.57, 46.7/21.9/11.8/6.3 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.72.1.09-2.99.2.80-16.38.pth
BLEU = 16.52, 46.6/22.0/11.7/6.2 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.73.1.10-3.01.2.80-16.42.pth
BLEU = 16.57, 46.6/21.9/11.8/6.3 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.74.1.05-2.85.2.81-16.62.pth
BLEU = 16.57, 46.6/22.0/11.8/6.2 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.75.1.05-2.87.2.80-16.52.pth
BLEU = 16.55, 46.5/21.9/11.8/6.3 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.76.1.03-2.79.2.82-16.71.pth
BLEU = 16.84, 46.6/22.2/12.1/6.4 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.77.1.05-2.86.2.81-16.63.pth
BLEU = 16.55, 46.6/22.1/11.7/6.2 (BP=1.000, ratio=1.000, hyp_len=28814, ref_len=28803)
Evaluation result for the model: seq-model-brmy.78.1.04-2.82.2.83-16.98.pth
BLEU = 16.49, 46.4/21.9/11.7/6.2 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.79.0.96-2.62.2.82-16.75.pth
BLEU = 17.15, 47.3/22.6/12.3/6.6 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.80.0.98-2.66.2.82-16.85.pth
BLEU = 17.38, 47.0/22.7/12.5/6.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.81.0.97-2.64.2.83-16.97.pth
BLEU = 17.08, 46.7/22.4/12.2/6.6 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.82.0.94-2.56.2.83-16.90.pth
BLEU = 17.39, 47.1/22.8/12.5/6.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.83.0.94-2.56.2.84-17.08.pth
BLEU = 17.53, 47.3/22.9/12.6/6.9 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.84.0.94-2.56.2.83-16.88.pth
BLEU = 17.26, 47.3/22.7/12.3/6.7 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.85.0.95-2.58.2.84-17.19.pth
BLEU = 17.20, 47.0/22.7/12.4/6.7 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.86.0.91-2.48.2.83-16.89.pth
BLEU = 17.65, 47.5/23.0/12.7/7.0 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.87.0.89-2.44.2.83-16.95.pth
BLEU = 17.77, 47.8/23.2/12.8/7.1 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.88.0.87-2.39.2.86-17.50.pth
BLEU = 17.29, 46.9/22.6/12.4/6.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.89.0.85-2.33.2.86-17.39.pth
BLEU = 17.76, 47.5/23.1/12.8/7.1 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.90.0.96-2.60.2.88-17.87.pth
BLEU = 17.30, 46.8/22.6/12.4/6.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.91.0.85-2.33.2.86-17.41.pth
BLEU = 17.72, 47.4/23.1/12.8/7.0 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.92.0.85-2.34.2.85-17.31.pth
BLEU = 18.02, 47.4/23.4/13.0/7.3 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.93.0.79-2.21.2.90-18.12.pth
BLEU = 17.77, 47.0/23.1/12.9/7.1 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.94.0.84-2.32.2.86-17.49.pth
BLEU = 18.04, 47.8/23.5/13.1/7.2 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.95.0.80-2.23.2.87-17.67.pth
BLEU = 18.25, 47.6/23.6/13.3/7.4 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.96.0.80-2.22.2.87-17.59.pth
BLEU = 18.39, 48.0/23.9/13.3/7.5 (BP=1.000, ratio=1.000, hyp_len=28809, ref_len=28803)
Evaluation result for the model: seq-model-brmy.97.0.78-2.18.2.88-17.79.pth
BLEU = 18.29, 47.6/23.7/13.3/7.5 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.98.0.80-2.22.2.90-18.15.pth
BLEU = 17.94, 47.4/23.4/12.9/7.2 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.99.0.75-2.11.2.88-17.82.pth
BLEU = 18.52, 47.8/23.9/13.5/7.6 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.100.0.77-2.15.2.91-18.38.pth
BLEU = 18.50, 47.9/23.8/13.5/7.6 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.101.0.75-2.12.2.92-18.48.pth
BLEU = 18.05, 47.5/23.6/13.1/7.2 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.102.0.79-2.20.2.91-18.30.pth
BLEU = 18.69, 48.1/23.9/13.6/7.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.103.0.77-2.17.2.91-18.30.pth
BLEU = 18.56, 48.1/23.8/13.5/7.7 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.104.0.73-2.08.2.89-18.03.pth
BLEU = 18.82, 48.3/24.2/13.8/7.8 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.105.0.71-2.03.2.90-18.21.pth
BLEU = 18.74, 48.1/24.1/13.7/7.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.106.0.75-2.11.2.92-18.51.pth
BLEU = 18.51, 47.9/23.8/13.5/7.7 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.107.0.72-2.05.2.91-18.32.pth
BLEU = 18.44, 47.9/23.8/13.4/7.6 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.108.0.72-2.06.2.98-19.69.pth
BLEU = 18.04, 47.4/23.3/13.0/7.3 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.109.0.71-2.03.2.93-18.78.pth
BLEU = 18.86, 48.1/24.3/13.8/7.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.110.0.71-2.04.2.94-18.84.pth
BLEU = 18.67, 48.1/23.9/13.6/7.8 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.111.0.69-1.99.2.93-18.76.pth
BLEU = 18.55, 48.0/23.9/13.5/7.6 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.112.0.69-1.99.2.92-18.59.pth
BLEU = 18.95, 48.3/24.4/13.8/7.9 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.113.0.65-1.92.2.94-18.86.pth
BLEU = 18.76, 48.3/24.3/13.7/7.7 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.114.0.69-1.99.2.93-18.75.pth
BLEU = 19.01, 48.5/24.4/13.9/7.9 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.115.0.66-1.93.2.92-18.59.pth
BLEU = 19.22, 48.5/24.6/14.1/8.1 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.116.0.68-1.97.2.93-18.71.pth
BLEU = 19.02, 48.4/24.3/13.9/8.0 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.117.0.64-1.90.2.94-18.93.pth
BLEU = 19.07, 48.6/24.4/14.0/8.0 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.118.0.67-1.95.2.97-19.42.pth
BLEU = 19.00, 48.1/24.3/14.0/8.0 (BP=1.000, ratio=1.000, hyp_len=28814, ref_len=28803)
Evaluation result for the model: seq-model-brmy.119.0.63-1.88.2.94-18.85.pth
BLEU = 19.10, 48.2/24.3/14.0/8.1 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.120.0.66-1.94.2.95-19.13.pth
BLEU = 19.00, 48.1/24.3/14.0/8.0 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.121.0.62-1.85.2.96-19.32.pth
BLEU = 19.14, 48.6/24.6/14.0/8.1 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.122.0.62-1.87.2.96-19.30.pth
BLEU = 18.98, 48.0/24.3/13.9/8.0 (BP=1.000, ratio=1.000, hyp_len=28809, ref_len=28803)
Evaluation result for the model: seq-model-brmy.123.0.60-1.82.2.96-19.24.pth
BLEU = 19.40, 48.6/24.6/14.3/8.3 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.124.0.62-1.87.2.97-19.53.pth
BLEU = 19.69, 49.1/25.0/14.5/8.4 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.125.0.60-1.82.2.99-19.85.pth
BLEU = 19.23, 48.7/24.6/14.1/8.1 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.126.0.59-1.80.2.99-19.90.pth
BLEU = 19.60, 48.9/25.0/14.5/8.3 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.127.0.57-1.77.2.96-19.33.pth
BLEU = 19.58, 48.8/25.0/14.5/8.3 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.128.0.58-1.78.2.98-19.71.pth
BLEU = 19.34, 48.9/24.7/14.2/8.2 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.129.0.57-1.78.2.99-19.88.pth
BLEU = 19.41, 48.5/24.7/14.3/8.2 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.130.0.56-1.75.3.02-20.43.pth
BLEU = 19.47, 48.3/24.8/14.4/8.3 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.131.0.58-1.79.3.02-20.55.pth
BLEU = 19.41, 48.7/24.7/14.3/8.3 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.132.0.56-1.75.3.00-20.15.pth
BLEU = 19.65, 48.7/25.0/14.5/8.5 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.133.0.56-1.74.3.02-20.41.pth
BLEU = 19.76, 48.9/25.1/14.6/8.5 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.134.0.57-1.77.3.02-20.42.pth
BLEU = 19.80, 48.6/25.0/14.7/8.6 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.135.0.55-1.73.3.02-20.40.pth
BLEU = 19.79, 48.6/25.0/14.7/8.6 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.136.0.54-1.72.3.00-20.01.pth
BLEU = 19.84, 49.0/25.2/14.7/8.6 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.137.0.58-1.79.3.04-20.81.pth
BLEU = 19.50, 48.6/24.9/14.4/8.3 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.138.0.52-1.68.3.02-20.49.pth
BLEU = 19.78, 49.2/25.1/14.6/8.5 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.139.0.52-1.67.3.00-20.03.pth
BLEU = 20.04, 49.3/25.4/14.8/8.7 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.140.0.51-1.67.3.03-20.72.pth
BLEU = 19.75, 49.0/25.1/14.6/8.5 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.141.0.54-1.71.3.07-21.57.pth
BLEU = 18.93, 48.1/24.2/13.9/7.9 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.142.0.54-1.71.3.04-20.91.pth
BLEU = 19.73, 49.1/25.1/14.6/8.5 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.143.0.53-1.69.3.04-20.90.pth
BLEU = 20.08, 49.3/25.4/14.9/8.7 (BP=1.000, ratio=1.000, hyp_len=28814, ref_len=28803)
Evaluation result for the model: seq-model-brmy.144.0.54-1.71.3.11-22.36.pth
BLEU = 18.67, 47.9/24.1/13.7/7.6 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.145.0.53-1.70.3.07-21.61.pth
BLEU = 19.80, 48.7/25.0/14.6/8.6 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.146.0.52-1.67.3.05-21.13.pth
BLEU = 19.89, 48.9/25.2/14.7/8.6 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.147.0.48-1.62.3.05-21.18.pth
BLEU = 19.98, 49.2/25.3/14.8/8.7 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.148.0.50-1.65.3.04-20.88.pth
BLEU = 20.41, 49.3/25.7/15.2/9.0 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.149.0.49-1.64.3.04-20.95.pth
BLEU = 19.83, 48.8/25.2/14.7/8.5 (BP=1.000, ratio=1.000, hyp_len=28814, ref_len=28803)
Evaluation result for the model: seq-model-brmy.150.0.48-1.62.3.05-21.20.pth
BLEU = 19.88, 49.1/25.2/14.7/8.6 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.151.0.47-1.60.3.07-21.62.pth
BLEU = 19.95, 48.7/25.2/14.8/8.7 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.152.0.49-1.62.3.09-22.02.pth
BLEU = 19.67, 48.8/25.0/14.6/8.4 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.153.0.46-1.59.3.07-21.47.pth
BLEU = 20.28, 49.4/25.6/15.1/8.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.154.0.45-1.56.3.04-20.88.pth
BLEU = 20.41, 49.6/25.8/15.2/8.9 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.155.0.46-1.59.3.05-21.19.pth
BLEU = 20.42, 49.6/25.7/15.2/9.0 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.156.0.48-1.61.3.07-21.54.pth
BLEU = 20.36, 49.3/25.6/15.2/9.0 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.157.0.45-1.57.3.07-21.61.pth
BLEU = 20.18, 49.5/25.5/15.0/8.8 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.158.0.47-1.60.3.07-21.47.pth
BLEU = 20.33, 49.4/25.6/15.2/8.9 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.159.0.43-1.54.3.09-22.04.pth
BLEU = 20.00, 49.2/25.4/14.9/8.6 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.160.0.44-1.56.3.09-22.06.pth
BLEU = 20.30, 49.5/25.8/15.2/8.8 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.161.0.45-1.57.3.10-22.10.pth
BLEU = 20.35, 49.6/25.8/15.1/8.9 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.162.0.44-1.56.3.12-22.66.pth
BLEU = 20.09, 49.4/25.4/14.9/8.7 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.163.0.46-1.58.3.12-22.55.pth
BLEU = 20.51, 49.7/25.9/15.3/9.0 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.164.0.43-1.53.3.12-22.61.pth
BLEU = 20.24, 49.3/25.5/15.1/8.9 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.165.0.44-1.55.3.10-22.28.pth
BLEU = 20.53, 49.8/25.9/15.3/9.0 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.166.0.41-1.51.3.13-22.84.pth
BLEU = 20.33, 49.2/25.7/15.2/8.9 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.167.0.44-1.56.3.14-23.06.pth
BLEU = 20.17, 49.2/25.5/15.0/8.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.168.0.44-1.56.3.12-22.64.pth
BLEU = 20.38, 49.4/25.6/15.2/9.0 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.169.0.42-1.53.3.13-22.88.pth
BLEU = 20.23, 49.2/25.4/15.0/8.9 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.170.0.40-1.50.3.11-22.48.pth
BLEU = 20.50, 49.4/25.8/15.3/9.0 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.171.0.43-1.54.3.12-22.60.pth
BLEU = 20.23, 49.1/25.6/15.0/8.9 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.172.0.40-1.49.3.12-22.72.pth
BLEU = 20.71, 49.7/26.0/15.4/9.2 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.173.0.39-1.48.3.13-22.83.pth
BLEU = 20.83, 50.0/26.1/15.5/9.3 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.174.0.40-1.49.3.14-23.05.pth
BLEU = 20.34, 49.3/25.6/15.1/9.0 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.175.0.41-1.51.3.15-23.34.pth
BLEU = 20.35, 49.4/25.8/15.2/8.9 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.176.0.39-1.47.3.14-23.03.pth
BLEU = 20.82, 49.9/26.1/15.5/9.3 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.177.0.41-1.50.3.17-23.85.pth
BLEU = 20.08, 49.0/25.4/14.9/8.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.178.0.40-1.49.3.14-23.22.pth
BLEU = 20.75, 49.9/26.1/15.5/9.2 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.179.0.42-1.53.3.17-23.84.pth
BLEU = 20.28, 49.4/25.6/15.1/8.8 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.180.0.40-1.49.3.16-23.53.pth
BLEU = 21.01, 49.9/26.2/15.8/9.5 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.181.0.40-1.49.3.16-23.65.pth
BLEU = 21.15, 50.0/26.5/15.9/9.5 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.182.0.42-1.53.3.22-25.07.pth
BLEU = 19.72, 48.9/25.0/14.6/8.4 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.183.0.41-1.50.3.20-24.58.pth
BLEU = 20.34, 49.3/25.6/15.1/9.0 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.184.0.39-1.47.3.18-24.06.pth
BLEU = 20.91, 49.8/26.1/15.7/9.4 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.185.0.36-1.44.3.18-24.01.pth
BLEU = 20.62, 49.4/25.9/15.4/9.2 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.186.0.38-1.46.3.18-24.15.pth
BLEU = 20.90, 49.7/26.1/15.7/9.4 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.187.0.37-1.45.3.18-24.09.pth
BLEU = 20.72, 49.8/26.0/15.5/9.2 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.188.0.36-1.43.3.19-24.25.pth
BLEU = 21.12, 50.2/26.4/15.8/9.5 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.189.0.36-1.43.3.19-24.41.pth
BLEU = 20.89, 49.9/26.3/15.6/9.3 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.190.0.33-1.40.3.20-24.54.pth
BLEU = 20.66, 49.6/25.9/15.4/9.2 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.191.0.36-1.44.3.22-25.00.pth
BLEU = 20.62, 49.7/25.9/15.4/9.2 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.192.0.36-1.44.3.22-25.08.pth
BLEU = 20.61, 49.6/26.1/15.4/9.1 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.193.0.35-1.42.3.18-24.09.pth
BLEU = 21.07, 50.3/26.4/15.7/9.5 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.194.0.34-1.40.3.21-24.87.pth
BLEU = 21.24, 50.0/26.4/16.0/9.7 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.195.0.39-1.48.3.21-24.75.pth
BLEU = 20.88, 49.7/26.2/15.6/9.4 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.196.0.35-1.42.3.19-24.29.pth
BLEU = 21.21, 50.3/26.5/15.9/9.6 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.197.0.36-1.43.3.22-25.09.pth
BLEU = 21.13, 49.8/26.3/15.8/9.6 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.198.0.36-1.44.3.21-24.74.pth
BLEU = 20.96, 49.7/26.1/15.7/9.5 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.199.0.34-1.40.3.25-25.72.pth
BLEU = 20.46, 49.7/25.8/15.2/9.0 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.200.0.35-1.42.3.23-25.40.pth
BLEU = 21.29, 50.1/26.4/15.9/9.8 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.201.0.33-1.39.3.24-25.45.pth
BLEU = 20.97, 49.9/26.2/15.7/9.4 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.202.0.33-1.39.3.25-25.84.pth
BLEU = 21.07, 50.0/26.2/15.8/9.5 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.203.0.35-1.42.3.25-25.79.pth
BLEU = 20.76, 49.5/25.9/15.5/9.3 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.204.0.35-1.42.3.23-25.28.pth
BLEU = 21.23, 50.2/26.5/15.9/9.6 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.205.0.33-1.40.3.25-25.70.pth
BLEU = 21.06, 50.1/26.3/15.7/9.5 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.206.0.33-1.40.3.26-26.05.pth
BLEU = 21.15, 49.8/26.2/15.9/9.6 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.207.0.34-1.40.3.26-26.05.pth
BLEU = 21.15, 50.1/26.3/15.8/9.6 (BP=1.000, ratio=1.000, hyp_len=28814, ref_len=28803)
Evaluation result for the model: seq-model-brmy.208.0.32-1.37.3.27-26.38.pth
BLEU = 21.18, 49.9/26.3/15.8/9.7 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.209.0.32-1.37.3.27-26.34.pth
BLEU = 21.33, 50.0/26.5/16.0/9.8 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.210.0.34-1.41.3.26-26.10.pth
BLEU = 21.17, 50.0/26.3/15.8/9.6 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.211.0.32-1.37.3.29-26.73.pth
BLEU = 20.95, 49.8/26.3/15.6/9.4 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.212.0.32-1.38.3.28-26.48.pth
BLEU = 21.43, 50.2/26.6/16.1/9.8 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.213.0.33-1.39.3.30-27.24.pth
BLEU = 20.69, 49.7/25.9/15.4/9.2 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.214.0.32-1.38.3.27-26.19.pth
BLEU = 21.21, 50.2/26.4/15.8/9.6 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.215.0.36-1.43.3.31-27.46.pth
BLEU = 20.63, 49.5/25.8/15.4/9.2 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.216.0.30-1.35.3.29-26.87.pth
BLEU = 21.46, 50.2/26.7/16.1/9.8 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.217.0.31-1.36.3.29-26.76.pth
BLEU = 21.27, 50.3/26.5/15.9/9.7 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.218.0.31-1.36.3.27-26.26.pth
BLEU = 21.52, 50.3/26.7/16.2/9.8 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.219.0.29-1.33.3.30-27.14.pth
BLEU = 20.90, 49.9/26.2/15.6/9.4 (BP=1.000, ratio=1.000, hyp_len=28814, ref_len=28803)
Evaluation result for the model: seq-model-brmy.220.0.31-1.36.3.31-27.31.pth
BLEU = 21.21, 50.0/26.4/15.9/9.6 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.221.0.30-1.35.3.28-26.64.pth
BLEU = 21.52, 50.3/26.8/16.2/9.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.222.0.28-1.32.3.29-26.83.pth
BLEU = 21.38, 50.1/26.5/16.1/9.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.223.0.29-1.33.3.29-26.88.pth
BLEU = 21.74, 50.3/26.9/16.4/10.1 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.224.0.28-1.32.3.28-26.70.pth
BLEU = 21.68, 50.6/26.9/16.3/10.0 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.225.0.29-1.34.3.27-26.31.pth
BLEU = 21.95, 50.6/27.1/16.6/10.2 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.226.0.31-1.36.3.28-26.57.pth
BLEU = 21.77, 50.3/27.0/16.4/10.1 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.227.0.30-1.35.3.31-27.30.pth
BLEU = 21.74, 50.5/26.9/16.3/10.1 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.228.0.28-1.33.3.31-27.36.pth
BLEU = 21.50, 50.3/26.7/16.2/9.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.229.0.30-1.34.3.34-28.10.pth
BLEU = 21.26, 50.2/26.5/15.9/9.7 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.230.0.30-1.34.3.33-27.86.pth
BLEU = 21.05, 50.0/26.3/15.7/9.5 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.231.0.30-1.35.3.32-27.64.pth
BLEU = 21.26, 50.2/26.5/15.9/9.6 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.232.0.29-1.34.3.33-27.95.pth
BLEU = 21.26, 50.1/26.4/16.0/9.6 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.233.0.27-1.31.3.31-27.25.pth
BLEU = 21.52, 50.5/26.8/16.2/9.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.234.0.27-1.31.3.31-27.49.pth
BLEU = 21.30, 50.2/26.6/15.9/9.7 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.235.0.30-1.35.3.33-27.87.pth
BLEU = 21.31, 50.4/26.6/16.0/9.6 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.236.0.28-1.33.3.32-27.63.pth
BLEU = 21.51, 50.3/26.7/16.1/9.9 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.237.0.27-1.31.3.33-27.97.pth
BLEU = 21.68, 50.4/26.9/16.3/10.0 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.238.0.27-1.31.3.35-28.49.pth
BLEU = 21.15, 50.3/26.5/15.8/9.5 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.239.0.28-1.32.3.35-28.51.pth
BLEU = 21.19, 50.0/26.4/15.9/9.6 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.240.0.28-1.32.3.35-28.44.pth
BLEU = 21.58, 50.4/26.7/16.2/9.9 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.241.0.27-1.30.3.38-29.28.pth
BLEU = 21.27, 50.2/26.5/15.9/9.7 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.242.0.26-1.30.3.36-28.69.pth
BLEU = 21.44, 50.3/26.6/16.1/9.8 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.243.0.26-1.30.3.36-28.92.pth
BLEU = 21.31, 50.3/26.6/16.0/9.7 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.244.0.27-1.32.3.36-28.74.pth
BLEU = 21.71, 50.6/26.9/16.3/10.0 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.245.0.28-1.32.3.36-28.68.pth
BLEU = 21.18, 50.1/26.4/15.8/9.6 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.246.0.27-1.31.3.36-28.79.pth
BLEU = 21.50, 50.4/26.7/16.1/9.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.247.0.31-1.37.3.35-28.61.pth
BLEU = 21.42, 49.9/26.6/16.1/9.9 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.248.0.26-1.29.3.38-29.38.pth
BLEU = 21.54, 50.3/26.9/16.2/9.8 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.249.0.26-1.30.3.37-28.94.pth
BLEU = 21.51, 50.3/26.7/16.2/9.8 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.250.0.26-1.30.3.35-28.37.pth
BLEU = 21.82, 50.5/27.0/16.4/10.1 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.251.0.26-1.29.3.35-28.50.pth
BLEU = 21.94, 50.6/27.1/16.6/10.2 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.252.0.26-1.30.3.38-29.44.pth
BLEU = 21.56, 50.4/26.6/16.1/10.0 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.253.0.28-1.33.3.35-28.57.pth
BLEU = 21.77, 50.5/26.9/16.4/10.1 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.254.0.25-1.28.3.40-29.98.pth
BLEU = 21.62, 49.9/26.7/16.4/10.0 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.255.0.24-1.27.3.36-28.73.pth
BLEU = 21.72, 50.4/26.9/16.4/10.0 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.256.0.24-1.28.3.36-28.86.pth
BLEU = 21.88, 50.6/27.0/16.5/10.2 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.257.0.24-1.28.3.38-29.29.pth
BLEU = 21.94, 50.6/27.1/16.5/10.2 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.258.0.25-1.28.3.39-29.65.pth
BLEU = 21.39, 50.1/26.4/16.1/9.8 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.259.0.27-1.31.3.41-30.17.pth
BLEU = 21.64, 50.4/26.8/16.3/9.9 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.260.0.24-1.27.3.40-29.89.pth
BLEU = 21.69, 50.4/26.9/16.3/10.0 (BP=1.000, ratio=1.000, hyp_len=28816, ref_len=28803)
Evaluation result for the model: seq-model-brmy.261.0.24-1.27.3.41-30.29.pth
BLEU = 21.96, 50.8/27.1/16.5/10.2 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.262.0.24-1.27.3.45-31.35.pth
BLEU = 21.26, 50.2/26.5/15.9/9.6 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.263.0.25-1.28.3.41-30.29.pth
BLEU = 21.72, 50.3/26.8/16.4/10.1 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.264.0.24-1.27.3.42-30.42.pth
BLEU = 21.80, 50.4/26.8/16.4/10.2 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.265.0.25-1.28.3.41-30.15.pth
BLEU = 21.64, 50.4/26.7/16.3/10.0 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.266.0.24-1.27.3.41-30.20.pth
BLEU = 21.75, 50.6/27.0/16.4/10.0 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.267.0.25-1.28.3.42-30.46.pth
BLEU = 21.24, 50.1/26.5/15.9/9.6 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.268.0.24-1.27.3.43-30.98.pth
BLEU = 21.64, 50.3/26.9/16.3/9.9 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.269.0.24-1.27.3.41-30.24.pth
BLEU = 22.15, 50.8/27.3/16.7/10.4 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.270.0.23-1.25.3.43-30.93.pth
BLEU = 21.92, 50.5/27.1/16.5/10.2 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.271.0.25-1.28.3.42-30.59.pth
BLEU = 21.86, 50.6/26.9/16.4/10.2 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.272.0.24-1.27.3.44-31.05.pth
BLEU = 21.49, 50.4/26.8/16.1/9.8 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.273.0.24-1.27.3.46-31.85.pth
BLEU = 21.68, 50.4/26.8/16.4/10.0 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.274.0.24-1.27.3.45-31.50.pth
BLEU = 21.55, 50.4/26.7/16.2/9.9 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.275.0.23-1.26.3.42-30.59.pth
BLEU = 21.80, 50.6/27.0/16.4/10.0 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.276.0.22-1.25.3.45-31.66.pth
BLEU = 21.47, 50.4/26.7/16.1/9.9 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.277.0.25-1.28.3.44-31.32.pth
BLEU = 21.80, 50.8/27.1/16.4/10.0 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.278.0.23-1.26.3.45-31.38.pth
BLEU = 21.60, 50.3/26.7/16.3/10.0 (BP=1.000, ratio=1.000, hyp_len=28810, ref_len=28803)
Evaluation result for the model: seq-model-brmy.279.0.24-1.27.3.48-32.60.pth
BLEU = 21.35, 49.8/26.5/16.1/9.8 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.280.0.24-1.27.3.46-31.67.pth
BLEU = 21.96, 50.6/27.0/16.5/10.3 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.281.0.23-1.26.3.44-31.32.pth
BLEU = 22.05, 50.9/27.2/16.6/10.3 (BP=1.000, ratio=1.000, hyp_len=28814, ref_len=28803)
Evaluation result for the model: seq-model-brmy.282.0.24-1.27.3.47-31.98.pth
BLEU = 21.42, 50.4/26.7/16.1/9.7 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.283.0.23-1.26.3.48-32.57.pth
BLEU = 21.82, 50.4/27.0/16.5/10.1 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.284.0.23-1.26.3.46-31.92.pth
BLEU = 21.85, 50.5/27.0/16.5/10.1 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.285.0.22-1.25.3.48-32.45.pth
BLEU = 22.08, 50.7/27.2/16.6/10.3 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.286.0.22-1.24.3.48-32.38.pth
BLEU = 21.73, 50.5/26.9/16.4/10.0 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.287.0.26-1.29.3.54-34.57.pth
BLEU = 20.99, 49.8/26.1/15.7/9.5 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.288.0.24-1.27.3.50-33.19.pth
BLEU = 21.47, 50.2/26.6/16.1/9.9 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.289.0.22-1.25.3.48-32.50.pth
BLEU = 21.59, 50.2/26.8/16.2/10.0 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.290.0.21-1.23.3.47-32.25.pth
BLEU = 22.03, 50.6/27.1/16.7/10.3 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.291.0.22-1.24.3.51-33.61.pth
BLEU = 21.21, 49.9/26.3/16.0/9.6 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.292.0.21-1.23.3.46-31.87.pth
BLEU = 22.05, 50.8/27.3/16.7/10.2 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.293.0.21-1.24.3.49-32.89.pth
BLEU = 21.53, 50.0/26.5/16.2/10.0 (BP=1.000, ratio=1.000, hyp_len=28814, ref_len=28803)
Evaluation result for the model: seq-model-brmy.294.0.21-1.23.3.50-33.04.pth
BLEU = 21.94, 50.7/27.0/16.6/10.2 (BP=1.000, ratio=1.000, hyp_len=28813, ref_len=28803)
Evaluation result for the model: seq-model-brmy.295.0.21-1.24.3.49-32.67.pth
BLEU = 21.85, 50.7/27.0/16.5/10.1 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.296.0.22-1.24.3.50-32.96.pth
BLEU = 21.90, 50.6/26.8/16.5/10.2 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.297.0.23-1.26.3.49-32.70.pth
BLEU = 21.73, 50.6/26.9/16.4/10.0 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.298.0.20-1.23.3.49-32.90.pth
BLEU = 21.68, 50.4/26.9/16.3/10.0 (BP=1.000, ratio=1.000, hyp_len=28811, ref_len=28803)
Evaluation result for the model: seq-model-brmy.299.0.20-1.22.3.51-33.41.pth
BLEU = 21.89, 50.7/27.0/16.4/10.2 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
Evaluation result for the model: seq-model-brmy.300.0.20-1.22.3.53-34.10.pth
BLEU = 21.56, 50.5/26.6/16.2/9.9 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
/home/ye/exp/simple-nmt

real	175m57.886s
user	172m35.711s
sys	6m42.524s
(simple-nmt) ye@:~/exp/simple-nmt$
```

Best model and best score for br-my, seq2seq with simple-nmt is:  

```
Evaluation result for the model: seq-model-brmy.269.0.24-1.27.3.41-30.24.pth
BLEU = 22.15, 50.8/27.3/16.7/10.4 (BP=1.000, ratio=1.000, hyp_len=28812, ref_len=28803)
```

seq2seq ရဲ့ မော်ဒယ်တွေထဲက အကောင်းဆုံးမော်ဒယ်ကိုပဲ 1st-run-bk/ ဖိုလ်ဒါအောက်မှာ backup လုပ်ထားပြီး ကျန်တဲ့ .pth, .hyp ဖိုင်တွေအားလုံးကို နေရာယူလို့ ဖျက်ပစ်လိုက်တယ်။   

```
(base) ye@:~/exp/simple-nmt/model/braille/seq2seq/my-br$ rm *.pth
(base) ye@:~/exp/simple-nmt/model/braille/seq2seq/my-br$ rm *.hyp
(base) ye@:~/exp/simple-nmt/model/braille/seq2seq/my-br$ ls
1st-run-bk
(base) ye@:~/exp/simple-nmt/model/braille/seq2seq/my-br$ ls ./1st-run-bk/
eval-results-mybr-seq2seq-300epoch.txt  seq-model-mybr.295.0.24-1.27.3.68-39.79.pth
mybr-seq2seq-training.log               seq-model-mybr.295.0.24-1.27.3.68-39.79.pth.hyp
(base) ye@:~/exp/simple-nmt/model/braille/seq2seq/my-br$
```

## Training Transformer with Simple-NMT

bash script for training my-br and br-my ...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, Visiting Prof., LST, NECTEC, Thailand
# Last updated: 10 April 2022
# for transformer model training with Simple-NMT for Myanmar-MuHaung and MuHaung and Myanmar

echo "my-br, transformer-baseline training start for 300 epochs...";
time python train.py --train /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train \
--valid /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev \
--lang mybr \
--gpu_id 0 --batch_size 16 --n_epochs 300 \
--max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 \
--max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 \
--use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 \
--model_fn ./model/braille/transformer/my-br/transformer-model-mybr.pth  | tee ./model/braille/transformer/my-br/mybr-transformer-training.log;

echo "####################";
echo "br-my, transformer-baseline training start for 300 epochs...";
time python train.py --train /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train \
--valid /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev \
--lang brmy \
--gpu_id 1 --batch_size 16 --n_epochs 300 \
--max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 \
--max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 \
--use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 \
--model_fn ./model/braille/transformer/br-my/transformer-model-brmy.pth | tee ./model/braille/transformer/br-my/brmy-transformer-training.log;


```

training as follows:  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./braille-transformer-training.sh | tee ./braille-transformer-training-mybr-brmy.log
my-br, transformer-baseline training start for 300 epochs...
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 32,
    'init_epoch': 1,
    'iteration_per_update': 32,
    'lang': 'mybr',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/braille/transformer/my-br/transformer-model-mybr.pth',
    'n_epochs': 300,
    'n_layers': 6,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/media/ye/project2/exp/braille-nmt/data/for-nmt/0/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': True,
    'valid': '/media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(17001, 32)
  (emb_dec): Embedding(16798, 32)
  (emb_dropout): Dropout(p=0.2, inplace=False)
  (encoder): MySequential(
    (0): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (1): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (2): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (3): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (4): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (5): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
  )
  (decoder): MySequential(
    (0): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (1): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (2): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (3): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (4): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (5): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
  )
  (generator): Sequential(
    (0): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
    (1): Linear(in_features=32, out_features=16798, bias=True)
    (2): LogSoftmax(dim=-1)
  )
)
NLLLoss()
Adam (
Parameter Group 0
    amsgrad: False
    betas: (0.9, 0.98)
    eps: 1e-08
    lr: 0.001
    weight_decay: 0
)
Epoch 1 - |param|=1.04e+03 |g_param|=3.91e+05 loss=7.5618e+00 ppl=1923.23                                               
Validation - loss=7.6989e+00 ppl=2205.84 best_loss=inf best_ppl=inf                                                     
Epoch 2 - |param|=1.04e+03 |g_param|=4.13e+05 loss=6.4787e+00 ppl=651.14                                                
Validation - loss=6.6542e+00 ppl=776.03 best_loss=7.6989e+00 best_ppl=2205.84                                           
Epoch 3 - |param|=1.04e+03 |g_param|=3.35e+05 loss=5.8067e+00 ppl=332.52                                                
Validation - loss=6.0678e+00 ppl=431.72 best_loss=6.6542e+00 best_ppl=776.03                                            
Epoch 4 - |param|=1.04e+03 |g_param|=2.05e+05 loss=5.4997e+00 ppl=244.61                                                
Validation - loss=5.8305e+00 ppl=340.51 best_loss=6.0678e+00 best_ppl=431.72                                            
Epoch 5 - |param|=1.04e+03 |g_param|=1.43e+05 loss=5.3152e+00 ppl=203.41                                                
Validation - loss=5.6744e+00 ppl=291.31 best_loss=5.8305e+00 best_ppl=340.51                                            
Epoch 6 - |param|=1.04e+03 |g_param|=1.24e+05 loss=5.1824e+00 ppl=178.11                                                
Validation - loss=5.5551e+00 ppl=258.55 best_loss=5.6744e+00 best_ppl=291.31                                            
Epoch 7 - |param|=1.04e+03 |g_param|=1.21e+05 loss=5.0643e+00 ppl=158.28                                                
Validation - loss=5.4312e+00 ppl=228.42 best_loss=5.5551e+00 best_ppl=258.55                                            
Epoch 8 - |param|=1.04e+03 |g_param|=1.35e+05 loss=4.8575e+00 ppl=128.70                                                
Validation - loss=5.3075e+00 ppl=201.85 best_loss=5.4312e+00 best_ppl=228.42                                            
Epoch 9 - |param|=1.04e+03 |g_param|=1.21e+05 loss=4.8424e+00 ppl=126.77                                                
Validation - loss=5.2018e+00 ppl=181.59 best_loss=5.3075e+00 best_ppl=201.85                                            
Epoch 10 - |param|=1.04e+03 |g_param|=1.36e+05 loss=4.6618e+00 ppl=105.83                                               
Validation - loss=5.1035e+00 ppl=164.60 best_loss=5.2018e+00 best_ppl=181.59                                            
Epoch 11 - |param|=1.04e+03 |g_param|=1.88e+05 loss=4.6120e+00 ppl=100.68                                               
Validation - loss=5.0184e+00 ppl=151.16 best_loss=5.1035e+00 best_ppl=164.60                                            
Epoch 12 - |param|=1.04e+03 |g_param|=2.50e+05 loss=4.5492e+00 ppl=94.55                                                
Validation - loss=4.9472e+00 ppl=140.78 best_loss=5.0184e+00 best_ppl=151.16                                            
Epoch 13 - |param|=1.04e+03 |g_param|=1.62e+05 loss=4.4375e+00 ppl=84.57                                                
Validation - loss=4.8710e+00 ppl=130.45 best_loss=4.9472e+00 best_ppl=140.78                                            
Epoch 14 - |param|=1.04e+03 |g_param|=1.78e+05 loss=4.3724e+00 ppl=79.23                                                
Validation - loss=4.8136e+00 ppl=123.17 best_loss=4.8710e+00 best_ppl=130.45                                            
Epoch 15 - |param|=1.04e+03 |g_param|=2.75e+05 loss=4.2796e+00 ppl=72.21                                                
Validation - loss=4.7625e+00 ppl=117.04 best_loss=4.8136e+00 best_ppl=123.17                                            
Epoch 16 - |param|=1.04e+03 |g_param|=1.78e+05 loss=4.1777e+00 ppl=65.22                                                
Validation - loss=4.7105e+00 ppl=111.11 best_loss=4.7625e+00 best_ppl=117.04                                            
Epoch 17 - |param|=1.04e+03 |g_param|=2.09e+05 loss=4.0640e+00 ppl=58.20                                                
Validation - loss=4.6558e+00 ppl=105.20 best_loss=4.7105e+00 best_ppl=111.11                                            
Epoch 18 - |param|=1.04e+03 |g_param|=2.69e+05 loss=4.0962e+00 ppl=60.11                                                
Validation - loss=4.6102e+00 ppl=100.51 best_loss=4.6558e+00 best_ppl=105.20                                            
Epoch 19 - |param|=1.04e+03 |g_param|=2.69e+05 loss=3.9548e+00 ppl=52.18                                                
Validation - loss=4.5608e+00 ppl=95.66 best_loss=4.6102e+00 best_ppl=100.51                                             
Epoch 20 - |param|=1.04e+03 |g_param|=2.76e+05 loss=3.8996e+00 ppl=49.38                                                
Validation - loss=4.5256e+00 ppl=92.35 best_loss=4.5608e+00 best_ppl=95.66                                              
Epoch 21 - |param|=1.04e+03 |g_param|=3.43e+05 loss=3.9145e+00 ppl=50.12                                                
Validation - loss=4.4928e+00 ppl=89.37 best_loss=4.5256e+00 best_ppl=92.35                                              
Epoch 22 - |param|=1.04e+03 |g_param|=3.37e+05 loss=3.8973e+00 ppl=49.27                                                
Validation - loss=4.4407e+00 ppl=84.83 best_loss=4.4928e+00 best_ppl=89.37                                              
Epoch 23 - |param|=1.04e+03 |g_param|=2.73e+05 loss=3.8254e+00 ppl=45.85                                                
Validation - loss=4.4007e+00 ppl=81.51 best_loss=4.4407e+00 best_ppl=84.83                                              
Epoch 24 - |param|=1.04e+03 |g_param|=3.06e+05 loss=3.7240e+00 ppl=41.43                                                
Validation - loss=4.3606e+00 ppl=78.30 best_loss=4.4007e+00 best_ppl=81.51                                              
Epoch 25 - |param|=1.04e+03 |g_param|=3.27e+05 loss=3.7147e+00 ppl=41.05                                                
Validation - loss=4.3276e+00 ppl=75.76 best_loss=4.3606e+00 best_ppl=78.30                                              
Epoch 26 - |param|=1.04e+03 |g_param|=2.45e+05 loss=3.6373e+00 ppl=37.99                                                
Validation - loss=4.2939e+00 ppl=73.25 best_loss=4.3276e+00 best_ppl=75.76                                              
Epoch 27 - |param|=1.04e+03 |g_param|=2.26e+05 loss=3.6202e+00 ppl=37.34                                                
Validation - loss=4.2591e+00 ppl=70.75 best_loss=4.2939e+00 best_ppl=73.25                                              
Epoch 28 - |param|=1.04e+03 |g_param|=3.15e+05 loss=3.5282e+00 ppl=34.06                                                
Validation - loss=4.2319e+00 ppl=68.84 best_loss=4.2591e+00 best_ppl=70.75                                              
Epoch 29 - |param|=1.04e+03 |g_param|=3.80e+05 loss=3.6118e+00 ppl=37.03                                                
Validation - loss=4.2101e+00 ppl=67.36 best_loss=4.2319e+00 best_ppl=68.84                                              
Epoch 30 - |param|=1.04e+03 |g_param|=2.92e+05 loss=3.4498e+00 ppl=31.49                                                
Validation - loss=4.1685e+00 ppl=64.62 best_loss=4.2101e+00 best_ppl=67.36                                              
Epoch 31 - |param|=1.04e+03 |g_param|=3.23e+05 loss=3.4481e+00 ppl=31.44                                                
Validation - loss=4.1374e+00 ppl=62.64 best_loss=4.1685e+00 best_ppl=64.62                                              
Epoch 32 - |param|=1.04e+03 |g_param|=2.83e+05 loss=3.3538e+00 ppl=28.61                                                
Validation - loss=4.1115e+00 ppl=61.04 best_loss=4.1374e+00 best_ppl=62.64                                              
Epoch 33 - |param|=1.04e+03 |g_param|=4.01e+05 loss=3.3635e+00 ppl=28.89                                                
Validation - loss=4.0599e+00 ppl=57.97 best_loss=4.1115e+00 best_ppl=61.04                                              
Epoch 34 - |param|=1.04e+03 |g_param|=4.14e+05 loss=3.2996e+00 ppl=27.10                                                
Validation - loss=4.0427e+00 ppl=56.98 best_loss=4.0599e+00 best_ppl=57.97                                              
Epoch 35 - |param|=1.04e+03 |g_param|=3.04e+05 loss=3.2227e+00 ppl=25.10                                                
Validation - loss=3.9921e+00 ppl=54.17 best_loss=4.0427e+00 best_ppl=56.98                                              
Epoch 36 - |param|=1.04e+03 |g_param|=3.13e+05 loss=3.1994e+00 ppl=24.52                                                
Validation - loss=3.9746e+00 ppl=53.23 best_loss=3.9921e+00 best_ppl=54.17                                              
Epoch 37 - |param|=1.04e+03 |g_param|=3.52e+05 loss=3.2121e+00 ppl=24.83                                                
Validation - loss=3.9420e+00 ppl=51.52 best_loss=3.9746e+00 best_ppl=53.23                                              
Epoch 38 - |param|=1.04e+03 |g_param|=4.22e+05 loss=3.1316e+00 ppl=22.91                                                
Validation - loss=3.9155e+00 ppl=50.17 best_loss=3.9420e+00 best_ppl=51.52                                              
Epoch 39 - |param|=1.04e+03 |g_param|=3.49e+05 loss=3.1421e+00 ppl=23.15                                                
Validation - loss=3.8767e+00 ppl=48.26 best_loss=3.9155e+00 best_ppl=50.17                                              
Epoch 40 - |param|=1.04e+03 |g_param|=3.38e+05 loss=3.0231e+00 ppl=20.56                                                
Validation - loss=3.8520e+00 ppl=47.09 best_loss=3.8767e+00 best_ppl=48.26                                              
Epoch 41 - |param|=1.04e+03 |g_param|=3.43e+05 loss=3.0199e+00 ppl=20.49                                                
Validation - loss=3.8221e+00 ppl=45.70 best_loss=3.8520e+00 best_ppl=47.09                                              
Epoch 42 - |param|=1.04e+03 |g_param|=3.42e+05 loss=2.9936e+00 ppl=19.96                                                
Validation - loss=3.7929e+00 ppl=44.39 best_loss=3.8221e+00 best_ppl=45.70                                              
Epoch 43 - |param|=1.04e+03 |g_param|=4.48e+05 loss=2.8920e+00 ppl=18.03                                                
Validation - loss=3.7629e+00 ppl=43.07 best_loss=3.7929e+00 best_ppl=44.39                                              
  1%|▌                                                                                          | 1/181 [00:00<?, ?it/s]Epoch 44 - |param|=1.04e+03 |g_param|=3.27e+05 loss=2.8520e+00 ppl=17.32
Validation - loss=3.7287e+00 ppl=41.62 best_loss=3.7629e+00 best_ppl=43.07                                              
Epoch 45 - |param|=1.04e+03 |g_param|=4.37e+05 loss=2.8575e+00 ppl=17.42                                                
Validation - loss=3.6963e+00 ppl=40.30 best_loss=3.7287e+00 best_ppl=41.62                                              
Epoch 46 - |param|=1.04e+03 |g_param|=4.84e+05 loss=2.7947e+00 ppl=16.36                                                
Validation - loss=3.6622e+00 ppl=38.95 best_loss=3.6963e+00 best_ppl=40.30                                              
Epoch 47 - |param|=1.04e+03 |g_param|=6.22e+05 loss=2.8057e+00 ppl=16.54                                                
Validation - loss=3.6287e+00 ppl=37.66 best_loss=3.6622e+00 best_ppl=38.95                                              
Epoch 48 - |param|=1.04e+03 |g_param|=4.79e+05 loss=2.7271e+00 ppl=15.29                                                
Validation - loss=3.5960e+00 ppl=36.45 best_loss=3.6287e+00 best_ppl=37.66                                              
Epoch 49 - |param|=1.04e+03 |g_param|=4.60e+05 loss=2.7039e+00 ppl=14.94                                                
Validation - loss=3.5714e+00 ppl=35.57 best_loss=3.5960e+00 best_ppl=36.45                                              
Epoch 50 - |param|=1.04e+03 |g_param|=3.98e+05 loss=2.6697e+00 ppl=14.44                                                
Validation - loss=3.5222e+00 ppl=33.86 best_loss=3.5714e+00 best_ppl=35.57                                              
Epoch 51 - |param|=1.04e+03 |g_param|=3.62e+05 loss=2.6207e+00 ppl=13.75                                                
Validation - loss=3.4896e+00 ppl=32.77 best_loss=3.5222e+00 best_ppl=33.86                                              
Epoch 52 - |param|=1.04e+03 |g_param|=5.46e+05 loss=2.6422e+00 ppl=14.04                                                
Validation - loss=3.4538e+00 ppl=31.62 best_loss=3.4896e+00 best_ppl=32.77                                              
Epoch 53 - |param|=1.04e+03 |g_param|=3.73e+05 loss=2.5861e+00 ppl=13.28                                                
Validation - loss=3.4317e+00 ppl=30.93 best_loss=3.4538e+00 best_ppl=31.62                                              
Epoch 54 - |param|=1.04e+03 |g_param|=5.32e+05 loss=2.5519e+00 ppl=12.83                                                
Validation - loss=3.3917e+00 ppl=29.72 best_loss=3.4317e+00 best_ppl=30.93                                              
Epoch 55 - |param|=1.04e+03 |g_param|=5.69e+05 loss=2.4586e+00 ppl=11.69                                                
Validation - loss=3.3676e+00 ppl=29.01 best_loss=3.3917e+00 best_ppl=29.72                                              
Epoch 56 - |param|=1.04e+03 |g_param|=4.71e+05 loss=2.4491e+00 ppl=11.58                                                
Validation - loss=3.3303e+00 ppl=27.95 best_loss=3.3676e+00 best_ppl=29.01                                              
Epoch 57 - |param|=1.04e+03 |g_param|=5.82e+05 loss=2.4178e+00 ppl=11.22                                                
Validation - loss=3.3003e+00 ppl=27.12 best_loss=3.3303e+00 best_ppl=27.95                                              
Epoch 58 - |param|=1.04e+03 |g_param|=4.95e+05 loss=2.3788e+00 ppl=10.79                                                
Validation - loss=3.2553e+00 ppl=25.93 best_loss=3.3003e+00 best_ppl=27.12                                              
Epoch 59 - |param|=1.04e+03 |g_param|=6.89e+05 loss=2.3820e+00 ppl=10.83                                                
Validation - loss=3.2411e+00 ppl=25.56 best_loss=3.2553e+00 best_ppl=25.93                                              
Epoch 60 - |param|=1.04e+03 |g_param|=1.10e+06 loss=2.3551e+00 ppl=10.54                                                
Validation - loss=3.2448e+00 ppl=25.66 best_loss=3.2411e+00 best_ppl=25.56                                              
Epoch 61 - |param|=1.04e+03 |g_param|=5.35e+05 loss=2.2859e+00 ppl=9.83                                                 
Validation - loss=3.1673e+00 ppl=23.74 best_loss=3.2411e+00 best_ppl=25.56                                              
Epoch 62 - |param|=1.04e+03 |g_param|=5.18e+05 loss=2.2960e+00 ppl=9.93                                                 
Validation - loss=3.1325e+00 ppl=22.93 best_loss=3.1673e+00 best_ppl=23.74                                              
Epoch 63 - |param|=1.04e+03 |g_param|=1.25e+06 loss=2.2038e+00 ppl=9.06                                                 
Validation - loss=3.1185e+00 ppl=22.61 best_loss=3.1325e+00 best_ppl=22.93                                              
Epoch 64 - |param|=1.04e+03 |g_param|=2.08e+06 loss=2.2295e+00 ppl=9.30                                                 
Validation - loss=3.0717e+00 ppl=21.58 best_loss=3.1185e+00 best_ppl=22.61                                              
Epoch 65 - |param|=1.04e+03 |g_param|=7.74e+05 loss=2.1477e+00 ppl=8.57                                                 
Validation - loss=3.0500e+00 ppl=21.11 best_loss=3.0717e+00 best_ppl=21.58                                              
Epoch 66 - |param|=1.04e+03 |g_param|=5.38e+05 loss=2.1012e+00 ppl=8.18                                                 
Validation - loss=3.0191e+00 ppl=20.47 best_loss=3.0500e+00 best_ppl=21.11                                              
Epoch 67 - |param|=1.04e+03 |g_param|=6.95e+05 loss=2.1612e+00 ppl=8.68                                                 
Validation - loss=2.9916e+00 ppl=19.92 best_loss=3.0191e+00 best_ppl=20.47                                              
Epoch 68 - |param|=1.04e+03 |g_param|=1.18e+06 loss=2.0891e+00 ppl=8.08                                                 
Validation - loss=2.9644e+00 ppl=19.38 best_loss=2.9916e+00 best_ppl=19.92                                              
Epoch 69 - |param|=1.04e+03 |g_param|=6.21e+05 loss=2.0325e+00 ppl=7.63                                                 
Validation - loss=2.9392e+00 ppl=18.90 best_loss=2.9644e+00 best_ppl=19.38                                              
Epoch 70 - |param|=1.04e+03 |g_param|=5.97e+05 loss=1.9814e+00 ppl=7.25                                                 
Validation - loss=2.9034e+00 ppl=18.24 best_loss=2.9392e+00 best_ppl=18.90                                              
Epoch 71 - |param|=1.04e+03 |g_param|=6.24e+05 loss=2.0469e+00 ppl=7.74                                                 
Validation - loss=2.8936e+00 ppl=18.06 best_loss=2.9034e+00 best_ppl=18.24                                              
Epoch 72 - |param|=1.04e+03 |g_param|=7.48e+05 loss=2.0221e+00 ppl=7.55                                                 
Validation - loss=2.8589e+00 ppl=17.44 best_loss=2.8936e+00 best_ppl=18.06                                              
Epoch 73 - |param|=1.04e+03 |g_param|=7.81e+05 loss=1.9641e+00 ppl=7.13                                                 
Validation - loss=2.8436e+00 ppl=17.18 best_loss=2.8589e+00 best_ppl=17.44                                              
Epoch 74 - |param|=1.04e+03 |g_param|=5.77e+05 loss=1.8984e+00 ppl=6.68                                                 
Validation - loss=2.8093e+00 ppl=16.60 best_loss=2.8436e+00 best_ppl=17.18                                              
Epoch 75 - |param|=1.04e+03 |g_param|=6.59e+05 loss=1.8810e+00 ppl=6.56                                                 
Validation - loss=2.7738e+00 ppl=16.02 best_loss=2.8093e+00 best_ppl=16.60                                              
Epoch 76 - |param|=1.04e+03 |g_param|=7.18e+05 loss=1.8463e+00 ppl=6.34                                                 
Validation - loss=2.7537e+00 ppl=15.70 best_loss=2.7738e+00 best_ppl=16.02                                              
Epoch 77 - |param|=1.04e+03 |g_param|=7.84e+05 loss=1.8144e+00 ppl=6.14                                                 
Validation - loss=2.7192e+00 ppl=15.17 best_loss=2.7537e+00 best_ppl=15.70                                              
Epoch 78 - |param|=1.04e+03 |g_param|=1.53e+06 loss=1.8094e+00 ppl=6.11                                                 
Validation - loss=2.7033e+00 ppl=14.93 best_loss=2.7192e+00 best_ppl=15.17                                              
Epoch 79 - |param|=1.04e+03 |g_param|=7.04e+05 loss=1.8307e+00 ppl=6.24                                                 
Validation - loss=2.6940e+00 ppl=14.79 best_loss=2.7033e+00 best_ppl=14.93                                              
Epoch 80 - |param|=1.04e+03 |g_param|=1.04e+06 loss=1.7273e+00 ppl=5.63                                                 
Validation - loss=2.6750e+00 ppl=14.51 best_loss=2.6940e+00 best_ppl=14.79                                              
Epoch 81 - |param|=1.04e+03 |g_param|=1.02e+06 loss=1.7607e+00 ppl=5.82                                                 
Validation - loss=2.6587e+00 ppl=14.28 best_loss=2.6750e+00 best_ppl=14.51                                              
Epoch 82 - |param|=1.04e+03 |g_param|=6.82e+05 loss=1.7043e+00 ppl=5.50                                                 
Validation - loss=2.6363e+00 ppl=13.96 best_loss=2.6587e+00 best_ppl=14.28                                              
Epoch 83 - |param|=1.04e+03 |g_param|=6.90e+05 loss=1.6861e+00 ppl=5.40                                                 
Validation - loss=2.6025e+00 ppl=13.50 best_loss=2.6363e+00 best_ppl=13.96                                              
Epoch 84 - |param|=1.04e+03 |g_param|=1.44e+06 loss=1.7122e+00 ppl=5.54                                                 
Validation - loss=2.6363e+00 ppl=13.96 best_loss=2.6025e+00 best_ppl=13.50                                              
Epoch 85 - |param|=1.04e+03 |g_param|=1.06e+06 loss=1.6636e+00 ppl=5.28                                                 
Validation - loss=2.5905e+00 ppl=13.34 best_loss=2.6025e+00 best_ppl=13.50                                              
Epoch 86 - |param|=1.04e+03 |g_param|=6.90e+05 loss=1.5968e+00 ppl=4.94                                                 
Validation - loss=2.5447e+00 ppl=12.74 best_loss=2.5905e+00 best_ppl=13.34                                              
Epoch 87 - |param|=1.04e+03 |g_param|=8.15e+05 loss=1.6465e+00 ppl=5.19                                                 
Validation - loss=2.5232e+00 ppl=12.47 best_loss=2.5447e+00 best_ppl=12.74                                              
Epoch 88 - |param|=1.04e+03 |g_param|=6.56e+05 loss=1.5947e+00 ppl=4.93                                                 
Validation - loss=2.5054e+00 ppl=12.25 best_loss=2.5232e+00 best_ppl=12.47                                              
Epoch 89 - |param|=1.04e+03 |g_param|=8.11e+05 loss=1.5468e+00 ppl=4.70                                                 
Validation - loss=2.4889e+00 ppl=12.05 best_loss=2.5054e+00 best_ppl=12.25                                              
Epoch 90 - |param|=1.04e+03 |g_param|=9.82e+05 loss=1.5310e+00 ppl=4.62                                                 
Validation - loss=2.4858e+00 ppl=12.01 best_loss=2.4889e+00 best_ppl=12.05                                              
Epoch 91 - |param|=1.04e+03 |g_param|=7.10e+05 loss=1.5073e+00 ppl=4.51                                                 
Validation - loss=2.4642e+00 ppl=11.75 best_loss=2.4858e+00 best_ppl=12.01                                              
Epoch 92 - |param|=1.04e+03 |g_param|=1.15e+06 loss=1.4921e+00 ppl=4.45                                                 
Validation - loss=2.4601e+00 ppl=11.71 best_loss=2.4642e+00 best_ppl=11.75                                              
Epoch 93 - |param|=1.04e+03 |g_param|=9.87e+05 loss=1.4966e+00 ppl=4.47                                                 
Validation - loss=2.4487e+00 ppl=11.57 best_loss=2.4601e+00 best_ppl=11.71                                              
Epoch 94 - |param|=1.04e+03 |g_param|=7.80e+05 loss=1.5094e+00 ppl=4.52                                                 
Validation - loss=2.4304e+00 ppl=11.36 best_loss=2.4487e+00 best_ppl=11.57                                              
Epoch 95 - |param|=1.04e+03 |g_param|=7.64e+05 loss=1.4126e+00 ppl=4.11                                                 
Validation - loss=2.4325e+00 ppl=11.39 best_loss=2.4304e+00 best_ppl=11.36                                              
Epoch 96 - |param|=1.04e+03 |g_param|=7.92e+05 loss=1.4259e+00 ppl=4.16                                                 
Validation - loss=2.4104e+00 ppl=11.14 best_loss=2.4304e+00 best_ppl=11.36                                              
Epoch 97 - |param|=1.04e+03 |g_param|=5.42e+05 loss=1.4650e+00 ppl=4.33                                                 
Validation - loss=2.3946e+00 ppl=10.96 best_loss=2.4104e+00 best_ppl=11.14                                              
Epoch 98 - |param|=1.04e+03 |g_param|=9.92e+05 loss=1.3865e+00 ppl=4.00                                                 
Validation - loss=2.3771e+00 ppl=10.77 best_loss=2.3946e+00 best_ppl=10.96                                              
Epoch 99 - |param|=1.04e+03 |g_param|=5.05e+05 loss=1.3461e+00 ppl=3.84                                                 
Validation - loss=2.3539e+00 ppl=10.53 best_loss=2.3771e+00 best_ppl=10.77                                              
Epoch 100 - |param|=1.04e+03 |g_param|=4.60e+05 loss=1.3390e+00 ppl=3.82                                                
Validation - loss=2.3574e+00 ppl=10.56 best_loss=2.3539e+00 best_ppl=10.53                                              
Epoch 101 - |param|=1.04e+03 |g_param|=7.93e+05 loss=1.3137e+00 ppl=3.72                                                
Validation - loss=2.3945e+00 ppl=10.96 best_loss=2.3539e+00 best_ppl=10.53                                              
Epoch 102 - |param|=1.04e+03 |g_param|=9.05e+05 loss=1.3500e+00 ppl=3.86                                                
Validation - loss=2.3387e+00 ppl=10.37 best_loss=2.3539e+00 best_ppl=10.53                                              
Epoch 103 - |param|=1.04e+03 |g_param|=5.50e+05 loss=1.3322e+00 ppl=3.79                                                
Validation - loss=2.3138e+00 ppl=10.11 best_loss=2.3387e+00 best_ppl=10.37                                              
Epoch 104 - |param|=1.04e+03 |g_param|=5.00e+05 loss=1.2580e+00 ppl=3.52                                                
Validation - loss=2.3065e+00 ppl=10.04 best_loss=2.3138e+00 best_ppl=10.11                                              
Epoch 105 - |param|=1.04e+03 |g_param|=1.57e+06 loss=1.3020e+00 ppl=3.68                                                
Validation - loss=2.3065e+00 ppl=10.04 best_loss=2.3065e+00 best_ppl=10.04                                              
Epoch 106 - |param|=1.04e+03 |g_param|=3.79e+05 loss=1.2321e+00 ppl=3.43                                                
Validation - loss=2.2763e+00 ppl=9.74 best_loss=2.3065e+00 best_ppl=10.04                                               
Epoch 107 - |param|=1.04e+03 |g_param|=1.00e+06 loss=1.2280e+00 ppl=3.41                                                
Validation - loss=2.2977e+00 ppl=9.95 best_loss=2.2763e+00 best_ppl=9.74                                                
Epoch 108 - |param|=1.04e+03 |g_param|=6.14e+05 loss=1.2568e+00 ppl=3.51                                                
Validation - loss=2.2715e+00 ppl=9.69 best_loss=2.2763e+00 best_ppl=9.74                                                
Epoch 109 - |param|=1.04e+03 |g_param|=8.68e+05 loss=1.2139e+00 ppl=3.37                                                
Validation - loss=2.2765e+00 ppl=9.74 best_loss=2.2715e+00 best_ppl=9.69                                                
Epoch 110 - |param|=1.04e+03 |g_param|=1.16e+06 loss=1.2731e+00 ppl=3.57                                                
Validation - loss=2.2583e+00 ppl=9.57 best_loss=2.2715e+00 best_ppl=9.69                                                
Epoch 111 - |param|=1.04e+03 |g_param|=4.55e+05 loss=1.1487e+00 ppl=3.15                                                
Validation - loss=2.2476e+00 ppl=9.47 best_loss=2.2583e+00 best_ppl=9.57                                                
Epoch 112 - |param|=1.04e+03 |g_param|=5.76e+05 loss=1.2303e+00 ppl=3.42                                                
Validation - loss=2.2326e+00 ppl=9.32 best_loss=2.2476e+00 best_ppl=9.47                                                
Epoch 113 - |param|=1.04e+03 |g_param|=5.39e+05 loss=1.1281e+00 ppl=3.09                                                
Validation - loss=2.2315e+00 ppl=9.31 best_loss=2.2326e+00 best_ppl=9.32                                                
Epoch 114 - |param|=1.04e+03 |g_param|=5.26e+05 loss=1.1672e+00 ppl=3.21                                                
Validation - loss=2.2400e+00 ppl=9.39 best_loss=2.2315e+00 best_ppl=9.31                                                
Epoch 115 - |param|=1.04e+03 |g_param|=1.44e+06 loss=1.2093e+00 ppl=3.35                                                
Validation - loss=2.2395e+00 ppl=9.39 best_loss=2.2315e+00 best_ppl=9.31                                                
Epoch 116 - |param|=1.04e+03 |g_param|=8.87e+05 loss=1.1622e+00 ppl=3.20                                                
Validation - loss=2.2166e+00 ppl=9.18 best_loss=2.2315e+00 best_ppl=9.31                                                
Epoch 117 - |param|=1.04e+03 |g_param|=8.13e+05 loss=1.1344e+00 ppl=3.11                                                
Validation - loss=2.2054e+00 ppl=9.07 best_loss=2.2166e+00 best_ppl=9.18                                                
Epoch 118 - |param|=1.04e+03 |g_param|=1.43e+06 loss=1.1272e+00 ppl=3.09                                                
Validation - loss=2.2381e+00 ppl=9.38 best_loss=2.2054e+00 best_ppl=9.07                                                
Epoch 119 - |param|=1.04e+03 |g_param|=4.31e+05 loss=1.0557e+00 ppl=2.87                                                
Validation - loss=2.1862e+00 ppl=8.90 best_loss=2.2054e+00 best_ppl=9.07                                                
Epoch 120 - |param|=1.04e+03 |g_param|=4.50e+05 loss=1.1084e+00 ppl=3.03                                                
Validation - loss=2.1836e+00 ppl=8.88 best_loss=2.1862e+00 best_ppl=8.90                                                
Epoch 121 - |param|=1.04e+03 |g_param|=3.77e+05 loss=1.0675e+00 ppl=2.91                                                
Validation - loss=2.1662e+00 ppl=8.72 best_loss=2.1836e+00 best_ppl=8.88                                                
Epoch 122 - |param|=1.04e+03 |g_param|=9.90e+05 loss=1.0399e+00 ppl=2.83                                                
Validation - loss=2.1887e+00 ppl=8.92 best_loss=2.1662e+00 best_ppl=8.72                                                
Epoch 123 - |param|=1.04e+03 |g_param|=4.73e+05 loss=1.0030e+00 ppl=2.73                                                
Validation - loss=2.1523e+00 ppl=8.60 best_loss=2.1662e+00 best_ppl=8.72                                                
Epoch 124 - |param|=1.04e+03 |g_param|=1.04e+06 loss=1.0521e+00 ppl=2.86                                                
Validation - loss=2.1438e+00 ppl=8.53 best_loss=2.1523e+00 best_ppl=8.60                                                
Epoch 125 - |param|=1.04e+03 |g_param|=7.77e+05 loss=1.0283e+00 ppl=2.80                                                
Validation - loss=2.1618e+00 ppl=8.69 best_loss=2.1438e+00 best_ppl=8.53                                                
Epoch 126 - |param|=1.04e+03 |g_param|=2.71e+05 loss=1.0160e+00 ppl=2.76                                                
Validation - loss=2.1446e+00 ppl=8.54 best_loss=2.1438e+00 best_ppl=8.53                                                
Epoch 127 - |param|=1.04e+03 |g_param|=5.86e+05 loss=1.0717e+00 ppl=2.92                                                
Validation - loss=2.1284e+00 ppl=8.40 best_loss=2.1438e+00 best_ppl=8.53                                                
Epoch 128 - |param|=1.04e+03 |g_param|=3.99e+05 loss=9.4140e-01 ppl=2.56                                                
Validation - loss=2.1213e+00 ppl=8.34 best_loss=2.1284e+00 best_ppl=8.40                                                
Epoch 129 - |param|=1.04e+03 |g_param|=3.45e+05 loss=9.7938e-01 ppl=2.66                                                
Validation - loss=2.1358e+00 ppl=8.46 best_loss=2.1213e+00 best_ppl=8.34                                                
Epoch 130 - |param|=1.04e+03 |g_param|=7.03e+05 loss=1.0381e+00 ppl=2.82                                                
Validation - loss=2.1747e+00 ppl=8.80 best_loss=2.1213e+00 best_ppl=8.34                                                
Epoch 131 - |param|=1.04e+03 |g_param|=3.62e+05 loss=9.8987e-01 ppl=2.69                                                
Validation - loss=2.1404e+00 ppl=8.50 best_loss=2.1213e+00 best_ppl=8.34                                                
Epoch 132 - |param|=1.04e+03 |g_param|=2.58e+05 loss=9.0080e-01 ppl=2.46                                                
Validation - loss=2.1081e+00 ppl=8.23 best_loss=2.1213e+00 best_ppl=8.34                                                
Epoch 133 - |param|=1.04e+03 |g_param|=3.21e+05 loss=9.3075e-01 ppl=2.54                                                
Validation - loss=2.1045e+00 ppl=8.20 best_loss=2.1081e+00 best_ppl=8.23                                                
Epoch 134 - |param|=1.04e+03 |g_param|=5.41e+05 loss=9.8669e-01 ppl=2.68                                                
Validation - loss=2.1061e+00 ppl=8.22 best_loss=2.1045e+00 best_ppl=8.20                                                
Epoch 135 - |param|=1.04e+03 |g_param|=4.24e+05 loss=9.3050e-01 ppl=2.54                                                
Validation - loss=2.0954e+00 ppl=8.13 best_loss=2.1045e+00 best_ppl=8.20                                                
Epoch 136 - |param|=1.04e+03 |g_param|=5.74e+05 loss=9.3534e-01 ppl=2.55                                                
Validation - loss=2.1094e+00 ppl=8.24 best_loss=2.0954e+00 best_ppl=8.13                                                
Epoch 137 - |param|=1.04e+03 |g_param|=3.01e+05 loss=9.0580e-01 ppl=2.47                                                
Validation - loss=2.1037e+00 ppl=8.20 best_loss=2.0954e+00 best_ppl=8.13                                                
Epoch 138 - |param|=1.04e+03 |g_param|=3.19e+05 loss=8.9398e-01 ppl=2.44                                                
Validation - loss=2.0954e+00 ppl=8.13 best_loss=2.0954e+00 best_ppl=8.13                                                
Epoch 139 - |param|=1.04e+03 |g_param|=5.49e+05 loss=8.5955e-01 ppl=2.36                                                
Validation - loss=2.1019e+00 ppl=8.18 best_loss=2.0954e+00 best_ppl=8.13                                                
Epoch 140 - |param|=1.04e+03 |g_param|=5.69e+05 loss=8.7741e-01 ppl=2.40                                                
Validation - loss=2.1464e+00 ppl=8.55 best_loss=2.0954e+00 best_ppl=8.13                                                
Epoch 141 - |param|=1.04e+03 |g_param|=4.41e+05 loss=8.7771e-01 ppl=2.41                                                
Validation - loss=2.0880e+00 ppl=8.07 best_loss=2.0954e+00 best_ppl=8.13                                                
Epoch 142 - |param|=1.04e+03 |g_param|=4.55e+05 loss=8.9507e-01 ppl=2.45                                                
Validation - loss=2.0776e+00 ppl=7.99 best_loss=2.0880e+00 best_ppl=8.07                                                
Epoch 143 - |param|=1.04e+03 |g_param|=4.51e+05 loss=8.6696e-01 ppl=2.38                                                
Validation - loss=2.1248e+00 ppl=8.37 best_loss=2.0776e+00 best_ppl=7.99                                                
Epoch 144 - |param|=1.04e+03 |g_param|=3.94e+05 loss=8.6969e-01 ppl=2.39                                                
Validation - loss=2.0644e+00 ppl=7.88 best_loss=2.0776e+00 best_ppl=7.99                                                
Epoch 145 - |param|=1.04e+03 |g_param|=2.54e+05 loss=8.5039e-01 ppl=2.34                                                
Validation - loss=2.0747e+00 ppl=7.96 best_loss=2.0644e+00 best_ppl=7.88                                                
Epoch 146 - |param|=1.04e+03 |g_param|=4.14e+05 loss=8.6469e-01 ppl=2.37                                                
Validation - loss=2.0679e+00 ppl=7.91 best_loss=2.0644e+00 best_ppl=7.88                                                
Epoch 147 - |param|=1.04e+03 |g_param|=3.72e+05 loss=7.8921e-01 ppl=2.20                                                
Validation - loss=2.0418e+00 ppl=7.70 best_loss=2.0644e+00 best_ppl=7.88                                                
Epoch 148 - |param|=1.04e+03 |g_param|=6.89e+05 loss=8.1311e-01 ppl=2.25                                                
Validation - loss=2.0543e+00 ppl=7.80 best_loss=2.0418e+00 best_ppl=7.70                                                
Epoch 149 - |param|=1.04e+03 |g_param|=2.73e+05 loss=7.9972e-01 ppl=2.22                                                
Validation - loss=2.0435e+00 ppl=7.72 best_loss=2.0418e+00 best_ppl=7.70                                                
Epoch 150 - |param|=1.04e+03 |g_param|=4.01e+05 loss=7.4072e-01 ppl=2.10                                                
Validation - loss=2.0689e+00 ppl=7.92 best_loss=2.0418e+00 best_ppl=7.70                                                
Epoch 151 - |param|=1.04e+03 |g_param|=7.19e+05 loss=8.0622e-01 ppl=2.24                                                
Validation - loss=2.0901e+00 ppl=8.09 best_loss=2.0418e+00 best_ppl=7.70                                                
Epoch 152 - |param|=1.04e+03 |g_param|=5.57e+05 loss=8.1282e-01 ppl=2.25                                                
Validation - loss=2.0481e+00 ppl=7.75 best_loss=2.0418e+00 best_ppl=7.70                                                
Epoch 153 - |param|=1.04e+03 |g_param|=2.47e+05 loss=7.8483e-01 ppl=2.19                                                
Validation - loss=2.0327e+00 ppl=7.63 best_loss=2.0418e+00 best_ppl=7.70                                                
Epoch 154 - |param|=1.04e+03 |g_param|=4.93e+05 loss=7.7076e-01 ppl=2.16                                                
Validation - loss=2.0279e+00 ppl=7.60 best_loss=2.0327e+00 best_ppl=7.63                                                
Epoch 155 - |param|=1.04e+03 |g_param|=5.97e+05 loss=7.8837e-01 ppl=2.20                                                
Validation - loss=2.0728e+00 ppl=7.95 best_loss=2.0279e+00 best_ppl=7.60                                                
Epoch 156 - |param|=1.04e+03 |g_param|=6.22e+05 loss=7.7196e-01 ppl=2.16                                                
Validation - loss=2.0790e+00 ppl=8.00 best_loss=2.0279e+00 best_ppl=7.60                                                
Epoch 157 - |param|=1.04e+03 |g_param|=3.75e+05 loss=7.6397e-01 ppl=2.15                                                
Validation - loss=2.0204e+00 ppl=7.54 best_loss=2.0279e+00 best_ppl=7.60                                                
Epoch 158 - |param|=1.04e+03 |g_param|=7.20e+05 loss=7.6427e-01 ppl=2.15                                                
Validation - loss=2.0273e+00 ppl=7.59 best_loss=2.0204e+00 best_ppl=7.54                                                
Epoch 159 - |param|=1.04e+03 |g_param|=3.28e+05 loss=7.7276e-01 ppl=2.17                                                
Validation - loss=1.9999e+00 ppl=7.39 best_loss=2.0204e+00 best_ppl=7.54                                                
Epoch 160 - |param|=1.04e+03 |g_param|=3.28e+05 loss=7.6370e-01 ppl=2.15                                                
Validation - loss=2.0116e+00 ppl=7.48 best_loss=1.9999e+00 best_ppl=7.39                                                
Epoch 161 - |param|=1.04e+03 |g_param|=5.71e+05 loss=7.5210e-01 ppl=2.12                                                
Validation - loss=1.9932e+00 ppl=7.34 best_loss=1.9999e+00 best_ppl=7.39                                                
Epoch 162 - |param|=1.04e+03 |g_param|=7.45e+05 loss=7.4378e-01 ppl=2.10                                                
Validation - loss=2.0415e+00 ppl=7.70 best_loss=1.9932e+00 best_ppl=7.34                                                
Epoch 163 - |param|=1.04e+03 |g_param|=5.81e+05 loss=7.3986e-01 ppl=2.10                                                
Validation - loss=1.9958e+00 ppl=7.36 best_loss=1.9932e+00 best_ppl=7.34                                                
Epoch 164 - |param|=1.04e+03 |g_param|=2.83e+05 loss=7.2106e-01 ppl=2.06                                                
Validation - loss=2.0130e+00 ppl=7.49 best_loss=1.9932e+00 best_ppl=7.34                                                
Epoch 165 - |param|=1.04e+03 |g_param|=2.24e+05 loss=6.6776e-01 ppl=1.95                                                
Validation - loss=1.9951e+00 ppl=7.35 best_loss=1.9932e+00 best_ppl=7.34                                                
Epoch 166 - |param|=1.04e+03 |g_param|=3.76e+05 loss=7.3219e-01 ppl=2.08                                                
Validation - loss=1.9710e+00 ppl=7.18 best_loss=1.9932e+00 best_ppl=7.34                                                
Epoch 167 - |param|=1.04e+03 |g_param|=4.91e+05 loss=6.9840e-01 ppl=2.01                                                
Validation - loss=2.0097e+00 ppl=7.46 best_loss=1.9710e+00 best_ppl=7.18                                                
Epoch 168 - |param|=1.04e+03 |g_param|=3.90e+05 loss=6.8238e-01 ppl=1.98                                                
Validation - loss=2.0144e+00 ppl=7.50 best_loss=1.9710e+00 best_ppl=7.18                                                
Epoch 169 - |param|=1.04e+03 |g_param|=7.10e+05 loss=7.0340e-01 ppl=2.02                                                
Validation - loss=1.9864e+00 ppl=7.29 best_loss=1.9710e+00 best_ppl=7.18                                                
Epoch 170 - |param|=1.04e+03 |g_param|=3.00e+05 loss=6.4237e-01 ppl=1.90                                                
Validation - loss=1.9778e+00 ppl=7.23 best_loss=1.9710e+00 best_ppl=7.18                                                
Epoch 171 - |param|=1.04e+03 |g_param|=2.11e+05 loss=6.9150e-01 ppl=2.00                                                
Validation - loss=1.9691e+00 ppl=7.16 best_loss=1.9710e+00 best_ppl=7.18                                                
Epoch 172 - |param|=1.04e+03 |g_param|=3.92e+05 loss=6.8977e-01 ppl=1.99                                                
Validation - loss=1.9733e+00 ppl=7.19 best_loss=1.9691e+00 best_ppl=7.16                                                
Epoch 173 - |param|=1.04e+03 |g_param|=3.46e+05 loss=6.6487e-01 ppl=1.94                                                
Validation - loss=1.9512e+00 ppl=7.04 best_loss=1.9691e+00 best_ppl=7.16                                                
Epoch 174 - |param|=1.04e+03 |g_param|=9.57e+05 loss=7.1734e-01 ppl=2.05                                                
Validation - loss=2.1005e+00 ppl=8.17 best_loss=1.9512e+00 best_ppl=7.04                                                
Epoch 175 - |param|=1.04e+03 |g_param|=4.03e+05 loss=6.8504e-01 ppl=1.98                                                
Validation - loss=1.9632e+00 ppl=7.12 best_loss=1.9512e+00 best_ppl=7.04                                                
Epoch 176 - |param|=1.04e+03 |g_param|=4.84e+05 loss=6.5498e-01 ppl=1.93                                                
Validation - loss=1.9293e+00 ppl=6.88 best_loss=1.9512e+00 best_ppl=7.04                                                
Epoch 177 - |param|=1.04e+03 |g_param|=2.16e+05 loss=6.2973e-01 ppl=1.88                                                
Validation - loss=1.9456e+00 ppl=7.00 best_loss=1.9293e+00 best_ppl=6.88                                                
Epoch 178 - |param|=1.04e+03 |g_param|=6.13e+05 loss=7.0393e-01 ppl=2.02                                                
Validation - loss=1.9644e+00 ppl=7.13 best_loss=1.9293e+00 best_ppl=6.88                                                
Epoch 179 - |param|=1.04e+03 |g_param|=2.88e+05 loss=6.6615e-01 ppl=1.95                                                
Validation - loss=1.9451e+00 ppl=6.99 best_loss=1.9293e+00 best_ppl=6.88                                                
Epoch 180 - |param|=1.04e+03 |g_param|=5.16e+05 loss=6.7243e-01 ppl=1.96                                                
Validation - loss=1.9723e+00 ppl=7.19 best_loss=1.9293e+00 best_ppl=6.88                                                
Epoch 181 - |param|=1.04e+03 |g_param|=6.83e+05 loss=6.5594e-01 ppl=1.93                                                
Validation - loss=1.9494e+00 ppl=7.02 best_loss=1.9293e+00 best_ppl=6.88                                                
Epoch 182 - |param|=1.04e+03 |g_param|=4.52e+05 loss=6.3239e-01 ppl=1.88                                                
Validation - loss=1.9425e+00 ppl=6.98 best_loss=1.9293e+00 best_ppl=6.88                                                
Epoch 183 - |param|=1.04e+03 |g_param|=5.56e+05 loss=6.3642e-01 ppl=1.89                                                
Validation - loss=1.9539e+00 ppl=7.06 best_loss=1.9293e+00 best_ppl=6.88                                                
Epoch 184 - |param|=1.04e+03 |g_param|=5.83e+05 loss=5.7710e-01 ppl=1.78                                                
Validation - loss=1.9735e+00 ppl=7.20 best_loss=1.9293e+00 best_ppl=6.88                                                
Epoch 185 - |param|=1.04e+03 |g_param|=5.68e+05 loss=5.8447e-01 ppl=1.79                                                
Validation - loss=1.9414e+00 ppl=6.97 best_loss=1.9293e+00 best_ppl=6.88                                                
Epoch 186 - |param|=1.04e+03 |g_param|=4.13e+05 loss=6.1149e-01 ppl=1.84                                                
Validation - loss=1.9337e+00 ppl=6.92 best_loss=1.9293e+00 best_ppl=6.88                                                
Epoch 187 - |param|=1.04e+03 |g_param|=3.65e+05 loss=6.2406e-01 ppl=1.87                                                
Validation - loss=1.9382e+00 ppl=6.95 best_loss=1.9293e+00 best_ppl=6.88                                                
Epoch 188 - |param|=1.04e+03 |g_param|=9.83e+05 loss=5.6948e-01 ppl=1.77                                                
Validation - loss=1.9313e+00 ppl=6.90 best_loss=1.9293e+00 best_ppl=6.88                                                
Epoch 189 - |param|=1.04e+03 |g_param|=3.11e+05 loss=5.5344e-01 ppl=1.74                                                
Validation - loss=1.9273e+00 ppl=6.87 best_loss=1.9293e+00 best_ppl=6.88                                                
Epoch 190 - |param|=1.04e+03 |g_param|=5.34e+05 loss=6.1318e-01 ppl=1.85                                                
Validation - loss=1.9217e+00 ppl=6.83 best_loss=1.9273e+00 best_ppl=6.87                                                
Epoch 191 - |param|=1.04e+03 |g_param|=4.43e+05 loss=5.5790e-01 ppl=1.75                                                
Validation - loss=1.9194e+00 ppl=6.82 best_loss=1.9217e+00 best_ppl=6.83                                                
Epoch 192 - |param|=1.04e+03 |g_param|=5.71e+05 loss=5.7687e-01 ppl=1.78                                                
Validation - loss=1.9375e+00 ppl=6.94 best_loss=1.9194e+00 best_ppl=6.82                                                
Epoch 193 - |param|=1.04e+03 |g_param|=8.00e+05 loss=6.3263e-01 ppl=1.88                                                
Validation - loss=1.9925e+00 ppl=7.33 best_loss=1.9194e+00 best_ppl=6.82                                                
Epoch 194 - |param|=1.05e+03 |g_param|=2.87e+05 loss=5.9820e-01 ppl=1.82                                                
Validation - loss=1.9246e+00 ppl=6.85 best_loss=1.9194e+00 best_ppl=6.82                                                
Epoch 195 - |param|=1.05e+03 |g_param|=2.26e+05 loss=5.5545e-01 ppl=1.74                                                
Validation - loss=1.9182e+00 ppl=6.81 best_loss=1.9194e+00 best_ppl=6.82                                                
Epoch 196 - |param|=1.05e+03 |g_param|=4.25e+05 loss=5.9587e-01 ppl=1.81                                                
Validation - loss=1.9061e+00 ppl=6.73 best_loss=1.9182e+00 best_ppl=6.81                                                
Epoch 197 - |param|=1.05e+03 |g_param|=3.09e+05 loss=5.7177e-01 ppl=1.77                                                
Validation - loss=1.9281e+00 ppl=6.88 best_loss=1.9061e+00 best_ppl=6.73                                                
Epoch 198 - |param|=1.05e+03 |g_param|=2.75e+05 loss=5.6930e-01 ppl=1.77                                                
Validation - loss=1.9054e+00 ppl=6.72 best_loss=1.9061e+00 best_ppl=6.73                                                
Epoch 199 - |param|=1.05e+03 |g_param|=6.80e+05 loss=5.5325e-01 ppl=1.74                                                
Validation - loss=1.9205e+00 ppl=6.82 best_loss=1.9054e+00 best_ppl=6.72                                                
Epoch 200 - |param|=1.05e+03 |g_param|=8.42e+05 loss=6.2802e-01 ppl=1.87                                                
Validation - loss=1.9292e+00 ppl=6.88 best_loss=1.9054e+00 best_ppl=6.72                                                
Epoch 201 - |param|=1.05e+03 |g_param|=2.60e+05 loss=5.3883e-01 ppl=1.71                                                
Validation - loss=1.8940e+00 ppl=6.65 best_loss=1.9054e+00 best_ppl=6.72                                                
Epoch 202 - |param|=1.05e+03 |g_param|=6.03e+05 loss=5.5493e-01 ppl=1.74                                                
Validation - loss=1.8895e+00 ppl=6.62 best_loss=1.8940e+00 best_ppl=6.65                                                
Epoch 203 - |param|=1.05e+03 |g_param|=8.77e+05 loss=5.5741e-01 ppl=1.75                                                
Validation - loss=1.9092e+00 ppl=6.75 best_loss=1.8895e+00 best_ppl=6.62                                                
Epoch 204 - |param|=1.05e+03 |g_param|=1.08e+06 loss=5.7714e-01 ppl=1.78                                                
Validation - loss=1.9222e+00 ppl=6.84 best_loss=1.8895e+00 best_ppl=6.62                                                
Epoch 205 - |param|=1.05e+03 |g_param|=3.65e+05 loss=5.5594e-01 ppl=1.74                                                
Validation - loss=1.9098e+00 ppl=6.75 best_loss=1.8895e+00 best_ppl=6.62                                                
Epoch 206 - |param|=1.05e+03 |g_param|=3.21e+05 loss=5.1974e-01 ppl=1.68                                                
Validation - loss=1.8616e+00 ppl=6.43 best_loss=1.8895e+00 best_ppl=6.62                                                
Epoch 207 - |param|=1.05e+03 |g_param|=4.17e+05 loss=5.3107e-01 ppl=1.70                                                
Validation - loss=1.8768e+00 ppl=6.53 best_loss=1.8616e+00 best_ppl=6.43                                                
Epoch 208 - |param|=1.05e+03 |g_param|=9.09e+05 loss=6.1413e-01 ppl=1.85                                                
Validation - loss=1.9748e+00 ppl=7.21 best_loss=1.8616e+00 best_ppl=6.43                                                
Epoch 209 - |param|=1.05e+03 |g_param|=2.13e+05 loss=5.1452e-01 ppl=1.67                                                
Validation - loss=1.8558e+00 ppl=6.40 best_loss=1.8616e+00 best_ppl=6.43                                                
Epoch 210 - |param|=1.05e+03 |g_param|=3.38e+05 loss=5.4676e-01 ppl=1.73                                                
Validation - loss=1.8841e+00 ppl=6.58 best_loss=1.8558e+00 best_ppl=6.40                                                
Epoch 211 - |param|=1.05e+03 |g_param|=2.90e+05 loss=5.6122e-01 ppl=1.75                                                
Validation - loss=1.8591e+00 ppl=6.42 best_loss=1.8558e+00 best_ppl=6.40                                                
Epoch 212 - |param|=1.05e+03 |g_param|=1.07e+06 loss=5.7576e-01 ppl=1.78                                                
Validation - loss=1.9902e+00 ppl=7.32 best_loss=1.8558e+00 best_ppl=6.40                                                
Epoch 213 - |param|=1.05e+03 |g_param|=3.88e+05 loss=5.0238e-01 ppl=1.65                                                
Validation - loss=1.8948e+00 ppl=6.65 best_loss=1.8558e+00 best_ppl=6.40                                                
Epoch 214 - |param|=1.05e+03 |g_param|=2.34e+05 loss=5.1143e-01 ppl=1.67                                                
Validation - loss=1.8425e+00 ppl=6.31 best_loss=1.8558e+00 best_ppl=6.40                                                
Epoch 215 - |param|=1.05e+03 |g_param|=7.28e+05 loss=5.2640e-01 ppl=1.69                                                
Validation - loss=1.8632e+00 ppl=6.44 best_loss=1.8425e+00 best_ppl=6.31                                                
Epoch 216 - |param|=1.05e+03 |g_param|=3.55e+05 loss=5.0843e-01 ppl=1.66                                                
Validation - loss=1.8717e+00 ppl=6.50 best_loss=1.8425e+00 best_ppl=6.31                                                
Epoch 217 - |param|=1.05e+03 |g_param|=3.08e+05 loss=5.0476e-01 ppl=1.66                                                
Validation - loss=1.8943e+00 ppl=6.65 best_loss=1.8425e+00 best_ppl=6.31                                                
Epoch 218 - |param|=1.05e+03 |g_param|=1.20e+05 loss=5.0754e-01 ppl=1.66                                                
Validation - loss=1.8665e+00 ppl=6.47 best_loss=1.8425e+00 best_ppl=6.31                                                
Epoch 219 - |param|=1.05e+03 |g_param|=1.54e+05 loss=4.8454e-01 ppl=1.62                                                
Validation - loss=1.8516e+00 ppl=6.37 best_loss=1.8425e+00 best_ppl=6.31                                                
Epoch 220 - |param|=1.05e+03 |g_param|=1.78e+05 loss=4.8785e-01 ppl=1.63                                                
Validation - loss=1.8624e+00 ppl=6.44 best_loss=1.8425e+00 best_ppl=6.31                                                
Epoch 221 - |param|=1.05e+03 |g_param|=1.43e+05 loss=4.9486e-01 ppl=1.64                                                
Validation - loss=1.8402e+00 ppl=6.30 best_loss=1.8425e+00 best_ppl=6.31                                                
Epoch 222 - |param|=1.05e+03 |g_param|=3.49e+05 loss=5.2102e-01 ppl=1.68                                                
Validation - loss=1.8773e+00 ppl=6.54 best_loss=1.8402e+00 best_ppl=6.30                                                
Epoch 223 - |param|=1.05e+03 |g_param|=1.32e+05 loss=4.6445e-01 ppl=1.59                                                
Validation - loss=1.8516e+00 ppl=6.37 best_loss=1.8402e+00 best_ppl=6.30                                                
Epoch 224 - |param|=1.05e+03 |g_param|=2.92e+05 loss=4.7115e-01 ppl=1.60                                                
Validation - loss=1.8414e+00 ppl=6.31 best_loss=1.8402e+00 best_ppl=6.30                                                
Epoch 225 - |param|=1.05e+03 |g_param|=3.64e+05 loss=5.2157e-01 ppl=1.68                                                
Validation - loss=1.8580e+00 ppl=6.41 best_loss=1.8402e+00 best_ppl=6.30                                                
Epoch 226 - |param|=1.05e+03 |g_param|=3.57e+05 loss=4.7097e-01 ppl=1.60                                                
Validation - loss=1.8379e+00 ppl=6.28 best_loss=1.8402e+00 best_ppl=6.30                                                
Epoch 227 - |param|=1.05e+03 |g_param|=1.23e+05 loss=4.6270e-01 ppl=1.59                                                
Validation - loss=1.8282e+00 ppl=6.22 best_loss=1.8379e+00 best_ppl=6.28                                                
Epoch 228 - |param|=1.05e+03 |g_param|=1.27e+05 loss=4.7840e-01 ppl=1.61                                                
Validation - loss=1.8279e+00 ppl=6.22 best_loss=1.8282e+00 best_ppl=6.22                                                
Epoch 229 - |param|=1.05e+03 |g_param|=1.55e+05 loss=4.4753e-01 ppl=1.56                                                
Validation - loss=1.8361e+00 ppl=6.27 best_loss=1.8279e+00 best_ppl=6.22                                                
Epoch 230 - |param|=1.05e+03 |g_param|=2.90e+05 loss=4.8455e-01 ppl=1.62                                                
Validation - loss=1.8630e+00 ppl=6.44 best_loss=1.8279e+00 best_ppl=6.22                                                
Epoch 231 - |param|=1.05e+03 |g_param|=2.45e+05 loss=4.7310e-01 ppl=1.60                                                
Validation - loss=1.8199e+00 ppl=6.17 best_loss=1.8279e+00 best_ppl=6.22                                                
Epoch 232 - |param|=1.05e+03 |g_param|=3.52e+05 loss=4.8197e-01 ppl=1.62                                                
Validation - loss=1.8177e+00 ppl=6.16 best_loss=1.8199e+00 best_ppl=6.17                                                
Epoch 233 - |param|=1.05e+03 |g_param|=1.96e+05 loss=4.5603e-01 ppl=1.58                                                
Validation - loss=1.8166e+00 ppl=6.15 best_loss=1.8177e+00 best_ppl=6.16                                                
Epoch 234 - |param|=1.05e+03 |g_param|=9.43e+04 loss=4.6716e-01 ppl=1.60                                                
Validation - loss=1.8134e+00 ppl=6.13 best_loss=1.8166e+00 best_ppl=6.15                                                
Epoch 235 - |param|=1.05e+03 |g_param|=2.76e+05 loss=4.7039e-01 ppl=1.60                                                
Validation - loss=1.8523e+00 ppl=6.37 best_loss=1.8134e+00 best_ppl=6.13                                                
Epoch 236 - |param|=1.05e+03 |g_param|=3.53e+05 loss=4.8764e-01 ppl=1.63                                                
Validation - loss=1.8563e+00 ppl=6.40 best_loss=1.8134e+00 best_ppl=6.13                                                
Epoch 237 - |param|=1.05e+03 |g_param|=2.12e+05 loss=4.4469e-01 ppl=1.56                                                
Validation - loss=1.8266e+00 ppl=6.21 best_loss=1.8134e+00 best_ppl=6.13                                                
Epoch 238 - |param|=1.05e+03 |g_param|=1.74e+05 loss=4.2417e-01 ppl=1.53                                                
Validation - loss=1.8049e+00 ppl=6.08 best_loss=1.8134e+00 best_ppl=6.13                                                
Epoch 239 - |param|=1.05e+03 |g_param|=2.43e+05 loss=4.4929e-01 ppl=1.57                                                
Validation - loss=1.8359e+00 ppl=6.27 best_loss=1.8049e+00 best_ppl=6.08                                                
Epoch 240 - |param|=1.05e+03 |g_param|=9.26e+05 loss=5.6520e-01 ppl=1.76                                                
Validation - loss=1.8653e+00 ppl=6.46 best_loss=1.8049e+00 best_ppl=6.08                                                
Epoch 241 - |param|=1.05e+03 |g_param|=3.63e+05 loss=4.8891e-01 ppl=1.63                                                
Validation - loss=1.8590e+00 ppl=6.42 best_loss=1.8049e+00 best_ppl=6.08                                                
Epoch 242 - |param|=1.05e+03 |g_param|=2.33e+05 loss=4.2349e-01 ppl=1.53                                                
Validation - loss=1.8035e+00 ppl=6.07 best_loss=1.8049e+00 best_ppl=6.08                                                
Epoch 243 - |param|=1.05e+03 |g_param|=8.49e+04 loss=4.1999e-01 ppl=1.52                                                
Validation - loss=1.7994e+00 ppl=6.05 best_loss=1.8035e+00 best_ppl=6.07                                                
Epoch 244 - |param|=1.05e+03 |g_param|=2.05e+05 loss=4.3200e-01 ppl=1.54                                                
Validation - loss=1.7712e+00 ppl=5.88 best_loss=1.7994e+00 best_ppl=6.05                                                
Epoch 245 - |param|=1.05e+03 |g_param|=1.64e+05 loss=4.3074e-01 ppl=1.54                                                
Validation - loss=1.7790e+00 ppl=5.92 best_loss=1.7712e+00 best_ppl=5.88                                                
Epoch 246 - |param|=1.05e+03 |g_param|=2.56e+05 loss=4.2370e-01 ppl=1.53                                                
Validation - loss=1.7953e+00 ppl=6.02 best_loss=1.7712e+00 best_ppl=5.88                                                
Epoch 247 - |param|=1.05e+03 |g_param|=8.89e+05 loss=4.9297e-01 ppl=1.64                                                
Validation - loss=1.8507e+00 ppl=6.36 best_loss=1.7712e+00 best_ppl=5.88                                                
Epoch 248 - |param|=1.05e+03 |g_param|=2.57e+05 loss=4.3302e-01 ppl=1.54                                                
Validation - loss=1.8154e+00 ppl=6.14 best_loss=1.7712e+00 best_ppl=5.88                                                
Epoch 249 - |param|=1.05e+03 |g_param|=2.30e+05 loss=4.3064e-01 ppl=1.54                                                
Validation - loss=1.8024e+00 ppl=6.06 best_loss=1.7712e+00 best_ppl=5.88                                                
Epoch 250 - |param|=1.05e+03 |g_param|=1.41e+05 loss=4.4274e-01 ppl=1.56                                                
Validation - loss=1.8068e+00 ppl=6.09 best_loss=1.7712e+00 best_ppl=5.88                                                
Epoch 251 - |param|=1.05e+03 |g_param|=3.25e+05 loss=4.2561e-01 ppl=1.53                                                
Validation - loss=1.8002e+00 ppl=6.05 best_loss=1.7712e+00 best_ppl=5.88                                                
Epoch 252 - |param|=1.05e+03 |g_param|=1.96e+05 loss=3.9424e-01 ppl=1.48                                                
Validation - loss=1.7600e+00 ppl=5.81 best_loss=1.7712e+00 best_ppl=5.88                                                
Epoch 253 - |param|=1.05e+03 |g_param|=3.56e+05 loss=4.8457e-01 ppl=1.62                                                
Validation - loss=1.8047e+00 ppl=6.08 best_loss=1.7600e+00 best_ppl=5.81                                                
Epoch 254 - |param|=1.05e+03 |g_param|=1.53e+05 loss=4.1053e-01 ppl=1.51                                                
Validation - loss=1.7887e+00 ppl=5.98 best_loss=1.7600e+00 best_ppl=5.81                                                
Epoch 255 - |param|=1.05e+03 |g_param|=2.14e+05 loss=4.2167e-01 ppl=1.52                                                
Validation - loss=1.7847e+00 ppl=5.96 best_loss=1.7600e+00 best_ppl=5.81                                                
Epoch 256 - |param|=1.05e+03 |g_param|=3.98e+05 loss=4.4309e-01 ppl=1.56                                                
Validation - loss=1.7739e+00 ppl=5.89 best_loss=1.7600e+00 best_ppl=5.81                                                
Epoch 257 - |param|=1.05e+03 |g_param|=2.94e+05 loss=3.8095e-01 ppl=1.46                                                
Validation - loss=1.7836e+00 ppl=5.95 best_loss=1.7600e+00 best_ppl=5.81                                                
Epoch 258 - |param|=1.05e+03 |g_param|=3.18e+05 loss=4.6022e-01 ppl=1.58                                                
Validation - loss=1.7570e+00 ppl=5.79 best_loss=1.7600e+00 best_ppl=5.81                                                
Epoch 259 - |param|=1.05e+03 |g_param|=1.00e+05 loss=3.8726e-01 ppl=1.47                                                
Validation - loss=1.7647e+00 ppl=5.84 best_loss=1.7570e+00 best_ppl=5.79                                                
Epoch 260 - |param|=1.05e+03 |g_param|=2.43e+05 loss=3.9409e-01 ppl=1.48                                                
Validation - loss=1.7756e+00 ppl=5.90 best_loss=1.7570e+00 best_ppl=5.79                                                
Epoch 261 - |param|=1.05e+03 |g_param|=1.37e+05 loss=4.0086e-01 ppl=1.49                                                
Validation - loss=1.7602e+00 ppl=5.81 best_loss=1.7570e+00 best_ppl=5.79                                                
Epoch 262 - |param|=1.05e+03 |g_param|=1.66e+05 loss=4.1723e-01 ppl=1.52                                                
Validation - loss=1.7509e+00 ppl=5.76 best_loss=1.7570e+00 best_ppl=5.79                                                
Epoch 263 - |param|=1.05e+03 |g_param|=2.50e+05 loss=3.8954e-01 ppl=1.48                                                
Validation - loss=1.7465e+00 ppl=5.73 best_loss=1.7509e+00 best_ppl=5.76                                                
Epoch 264 - |param|=1.05e+03 |g_param|=1.42e+05 loss=3.7696e-01 ppl=1.46                                                
Validation - loss=1.7223e+00 ppl=5.60 best_loss=1.7465e+00 best_ppl=5.73                                                
Epoch 265 - |param|=1.05e+03 |g_param|=2.50e+05 loss=4.0172e-01 ppl=1.49                                                
Validation - loss=1.7359e+00 ppl=5.67 best_loss=1.7223e+00 best_ppl=5.60                                                
Epoch 266 - |param|=1.05e+03 |g_param|=1.03e+05 loss=3.6155e-01 ppl=1.44                                                
Validation - loss=1.7446e+00 ppl=5.72 best_loss=1.7223e+00 best_ppl=5.60                                                
Epoch 267 - |param|=1.05e+03 |g_param|=2.07e+05 loss=4.1845e-01 ppl=1.52                                                
Validation - loss=1.7485e+00 ppl=5.75 best_loss=1.7223e+00 best_ppl=5.60                                                
Epoch 268 - |param|=1.05e+03 |g_param|=7.26e+04 loss=3.9190e-01 ppl=1.48                                                
Validation - loss=1.7428e+00 ppl=5.71 best_loss=1.7223e+00 best_ppl=5.60                                                
Epoch 269 - |param|=1.05e+03 |g_param|=2.78e+05 loss=4.0956e-01 ppl=1.51                                                
Validation - loss=1.7932e+00 ppl=6.01 best_loss=1.7223e+00 best_ppl=5.60                                                
Epoch 270 - |param|=1.05e+03 |g_param|=4.66e+04 loss=4.0299e-01 ppl=1.50                                                
Validation - loss=1.7190e+00 ppl=5.58 best_loss=1.7223e+00 best_ppl=5.60                                                
Epoch 271 - |param|=1.05e+03 |g_param|=6.66e+04 loss=3.6796e-01 ppl=1.44                                                
Validation - loss=1.7462e+00 ppl=5.73 best_loss=1.7190e+00 best_ppl=5.58                                                
Epoch 272 - |param|=1.05e+03 |g_param|=8.45e+04 loss=3.5568e-01 ppl=1.43                                                
Validation - loss=1.7207e+00 ppl=5.59 best_loss=1.7190e+00 best_ppl=5.58                                                
Epoch 273 - |param|=1.05e+03 |g_param|=1.35e+05 loss=3.8778e-01 ppl=1.47                                                
Validation - loss=1.7502e+00 ppl=5.76 best_loss=1.7190e+00 best_ppl=5.58                                                
Epoch 274 - |param|=1.05e+03 |g_param|=5.17e+04 loss=4.0524e-01 ppl=1.50                                                
Validation - loss=1.7426e+00 ppl=5.71 best_loss=1.7190e+00 best_ppl=5.58                                                
Epoch 275 - |param|=1.05e+03 |g_param|=7.29e+04 loss=3.8454e-01 ppl=1.47                                                
Validation - loss=1.7423e+00 ppl=5.71 best_loss=1.7190e+00 best_ppl=5.58                                                
Epoch 276 - |param|=1.05e+03 |g_param|=8.04e+04 loss=3.8582e-01 ppl=1.47                                                
Validation - loss=1.7522e+00 ppl=5.77 best_loss=1.7190e+00 best_ppl=5.58                                                
Epoch 277 - |param|=1.05e+03 |g_param|=3.47e+04 loss=3.8224e-01 ppl=1.47                                                
Validation - loss=1.7213e+00 ppl=5.59 best_loss=1.7190e+00 best_ppl=5.58                                                
Epoch 278 - |param|=1.05e+03 |g_param|=2.80e+04 loss=3.5981e-01 ppl=1.43                                                
Validation - loss=1.7075e+00 ppl=5.52 best_loss=1.7190e+00 best_ppl=5.58                                                
Epoch 279 - |param|=1.05e+03 |g_param|=3.66e+04 loss=3.6722e-01 ppl=1.44                                                
Validation - loss=1.7347e+00 ppl=5.67 best_loss=1.7075e+00 best_ppl=5.52                                                
Epoch 280 - |param|=1.05e+03 |g_param|=5.87e+04 loss=3.8353e-01 ppl=1.47                                                
Validation - loss=1.7212e+00 ppl=5.59 best_loss=1.7075e+00 best_ppl=5.52                                                
Epoch 281 - |param|=1.05e+03 |g_param|=6.96e+04 loss=3.7373e-01 ppl=1.45                                                
Validation - loss=1.7313e+00 ppl=5.65 best_loss=1.7075e+00 best_ppl=5.52                                                
Epoch 282 - |param|=1.05e+03 |g_param|=9.09e+04 loss=3.7599e-01 ppl=1.46                                                
Validation - loss=1.6946e+00 ppl=5.44 best_loss=1.7075e+00 best_ppl=5.52                                                
Epoch 283 - |param|=1.05e+03 |g_param|=3.35e+04 loss=3.8101e-01 ppl=1.46                                                
Validation - loss=1.7215e+00 ppl=5.59 best_loss=1.6946e+00 best_ppl=5.44                                                
Epoch 284 - |param|=1.05e+03 |g_param|=5.18e+04 loss=3.7890e-01 ppl=1.46                                                
Validation - loss=1.7064e+00 ppl=5.51 best_loss=1.6946e+00 best_ppl=5.44                                                
Epoch 285 - |param|=1.05e+03 |g_param|=8.09e+04 loss=3.5508e-01 ppl=1.43                                                
Validation - loss=1.7224e+00 ppl=5.60 best_loss=1.6946e+00 best_ppl=5.44                                                
Epoch 286 - |param|=1.05e+03 |g_param|=4.78e+04 loss=3.7290e-01 ppl=1.45                                                
Validation - loss=1.7013e+00 ppl=5.48 best_loss=1.6946e+00 best_ppl=5.44                                                
Epoch 287 - |param|=1.05e+03 |g_param|=5.09e+04 loss=3.6422e-01 ppl=1.44                                                
Validation - loss=1.6973e+00 ppl=5.46 best_loss=1.6946e+00 best_ppl=5.44                                                
Epoch 288 - |param|=1.05e+03 |g_param|=4.28e+04 loss=3.8506e-01 ppl=1.47                                                
Validation - loss=1.6886e+00 ppl=5.41 best_loss=1.6946e+00 best_ppl=5.44                                                
Epoch 289 - |param|=1.05e+03 |g_param|=1.21e+05 loss=3.4085e-01 ppl=1.41                                                
Validation - loss=1.7233e+00 ppl=5.60 best_loss=1.6886e+00 best_ppl=5.41                                                
Epoch 290 - |param|=1.05e+03 |g_param|=7.74e+04 loss=3.6819e-01 ppl=1.45                                                
Validation - loss=1.7064e+00 ppl=5.51 best_loss=1.6886e+00 best_ppl=5.41                                                
Epoch 291 - |param|=1.05e+03 |g_param|=1.78e+05 loss=4.1229e-01 ppl=1.51                                                
Validation - loss=1.7084e+00 ppl=5.52 best_loss=1.6886e+00 best_ppl=5.41                                                
Epoch 292 - |param|=1.05e+03 |g_param|=4.84e+04 loss=3.5402e-01 ppl=1.42                                                
Validation - loss=1.7347e+00 ppl=5.67 best_loss=1.6886e+00 best_ppl=5.41                                                
Epoch 293 - |param|=1.05e+03 |g_param|=3.38e+04 loss=3.5325e-01 ppl=1.42                                                
Validation - loss=1.7208e+00 ppl=5.59 best_loss=1.6886e+00 best_ppl=5.41                                                
Epoch 294 - |param|=1.05e+03 |g_param|=3.14e+04 loss=3.3415e-01 ppl=1.40                                                
Validation - loss=1.6854e+00 ppl=5.39 best_loss=1.6886e+00 best_ppl=5.41                                                
Epoch 295 - |param|=1.05e+03 |g_param|=3.07e+04 loss=3.5607e-01 ppl=1.43                                                
Validation - loss=1.6749e+00 ppl=5.34 best_loss=1.6854e+00 best_ppl=5.39                                                
Epoch 296 - |param|=1.05e+03 |g_param|=1.47e+05 loss=3.7215e-01 ppl=1.45                                                
Validation - loss=1.6897e+00 ppl=5.42 best_loss=1.6749e+00 best_ppl=5.34                                                
Epoch 297 - |param|=1.05e+03 |g_param|=3.37e+04 loss=3.4480e-01 ppl=1.41                                                
Validation - loss=1.6795e+00 ppl=5.36 best_loss=1.6749e+00 best_ppl=5.34                                                
Epoch 298 - |param|=1.05e+03 |g_param|=1.35e+05 loss=3.7478e-01 ppl=1.45                                                
Validation - loss=1.7304e+00 ppl=5.64 best_loss=1.6749e+00 best_ppl=5.34                                                
Epoch 299 - |param|=1.05e+03 |g_param|=1.16e+05 loss=4.1540e-01 ppl=1.51                                                
Validation - loss=1.7351e+00 ppl=5.67 best_loss=1.6749e+00 best_ppl=5.34                                                
Epoch 300 - |param|=1.05e+03 |g_param|=7.70e+04 loss=3.5167e-01 ppl=1.42                                                
Validation - loss=1.7693e+00 ppl=5.87 best_loss=1.6749e+00 best_ppl=5.34                                                

real	209m34.355s
user	206m13.798s
sys	3m15.361s
####################
br-my, transformer-baseline training start for 300 epochs...
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 32,
    'init_epoch': 1,
    'iteration_per_update': 32,
    'lang': 'brmy',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/braille/transformer/br-my/transformer-model-brmy.pth',
    'n_epochs': 300,
    'n_layers': 6,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/media/ye/project2/exp/braille-nmt/data/for-nmt/0/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': True,
    'valid': '/media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(16796, 32)
  (emb_dec): Embedding(17003, 32)
  (emb_dropout): Dropout(p=0.2, inplace=False)
  (encoder): MySequential(
    (0): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (1): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (2): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (3): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (4): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (5): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
  )
  (decoder): MySequential(
    (0): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (1): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (2): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (3): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (4): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (5): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=32, out_features=32, bias=False)
        (K_linear): Linear(in_features=32, out_features=32, bias=False)
        (V_linear): Linear(in_features=32, out_features=32, bias=False)
        (linear): Linear(in_features=32, out_features=32, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=32, out_features=128, bias=True)
        (1): ReLU()
        (2): Linear(in_features=128, out_features=32, bias=True)
      )
      (fc_norm): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
  )
  (generator): Sequential(
    (0): LayerNorm((32,), eps=1e-05, elementwise_affine=True)
    (1): Linear(in_features=32, out_features=17003, bias=True)
    (2): LogSoftmax(dim=-1)
  )
)
NLLLoss()
Adam (
Parameter Group 0
    amsgrad: False
    betas: (0.9, 0.98)
    eps: 1e-08
    lr: 0.001
    weight_decay: 0
)
Epoch 1 - |param|=1.04e+03 |g_param|=4.11e+05 loss=7.4505e+00 ppl=1720.74                                               
Validation - loss=7.6275e+00 ppl=2053.84 best_loss=inf best_ppl=inf                                                     
Epoch 2 - |param|=1.04e+03 |g_param|=4.13e+05 loss=6.4568e+00 ppl=637.01                                                
Validation - loss=6.6314e+00 ppl=758.55 best_loss=7.6275e+00 best_ppl=2053.84                                           
Epoch 3 - |param|=1.04e+03 |g_param|=3.13e+05 loss=5.8262e+00 ppl=339.06                                                
Validation - loss=6.0538e+00 ppl=425.72 best_loss=6.6314e+00 best_ppl=758.55                                            
Epoch 4 - |param|=1.04e+03 |g_param|=2.04e+05 loss=5.4441e+00 ppl=231.38                                                
Validation - loss=5.7866e+00 ppl=325.89 best_loss=6.0538e+00 best_ppl=425.72                                            
Epoch 5 - |param|=1.04e+03 |g_param|=1.56e+05 loss=5.3307e+00 ppl=206.59                                                
Validation - loss=5.6288e+00 ppl=278.34 best_loss=5.7866e+00 best_ppl=325.89                                            
Epoch 6 - |param|=1.04e+03 |g_param|=1.25e+05 loss=5.1277e+00 ppl=168.63                                                
Validation - loss=5.5001e+00 ppl=244.72 best_loss=5.6288e+00 best_ppl=278.34                                            
Epoch 7 - |param|=1.04e+03 |g_param|=1.04e+05 loss=4.9878e+00 ppl=146.61                                                
Validation - loss=5.3834e+00 ppl=217.77 best_loss=5.5001e+00 best_ppl=244.72                                            
Epoch 8 - |param|=1.04e+03 |g_param|=1.76e+05 loss=4.7880e+00 ppl=120.07                                                
Validation - loss=5.2739e+00 ppl=195.18 best_loss=5.3834e+00 best_ppl=217.77                                            
Epoch 9 - |param|=1.04e+03 |g_param|=1.56e+05 loss=4.8163e+00 ppl=123.51                                                
Validation - loss=5.1714e+00 ppl=176.17 best_loss=5.2739e+00 best_ppl=195.18                                            
Epoch 10 - |param|=1.04e+03 |g_param|=1.59e+05 loss=4.6666e+00 ppl=106.33                                               
Validation - loss=5.0886e+00 ppl=162.17 best_loss=5.1714e+00 best_ppl=176.17                                            
Epoch 11 - |param|=1.04e+03 |g_param|=1.67e+05 loss=4.6105e+00 ppl=100.54                                               
Validation - loss=5.0047e+00 ppl=149.11 best_loss=5.0886e+00 best_ppl=162.17                                            
Epoch 12 - |param|=1.04e+03 |g_param|=2.05e+05 loss=4.5688e+00 ppl=96.43                                                
Validation - loss=4.9345e+00 ppl=139.00 best_loss=5.0047e+00 best_ppl=149.11                                            
Epoch 13 - |param|=1.04e+03 |g_param|=1.54e+05 loss=4.4860e+00 ppl=88.77                                                
Validation - loss=4.8571e+00 ppl=128.65 best_loss=4.9345e+00 best_ppl=139.00                                            
Epoch 14 - |param|=1.04e+03 |g_param|=2.30e+05 loss=4.3294e+00 ppl=75.90                                                
Validation - loss=4.7964e+00 ppl=121.07 best_loss=4.8571e+00 best_ppl=128.65                                            
Epoch 15 - |param|=1.04e+03 |g_param|=2.15e+05 loss=4.2537e+00 ppl=70.36                                                
Validation - loss=4.7365e+00 ppl=114.03 best_loss=4.7964e+00 best_ppl=121.07                                            
Epoch 16 - |param|=1.04e+03 |g_param|=2.34e+05 loss=4.1871e+00 ppl=65.83                                                
Validation - loss=4.6841e+00 ppl=108.22 best_loss=4.7365e+00 best_ppl=114.03                                            
Epoch 17 - |param|=1.04e+03 |g_param|=2.11e+05 loss=4.1287e+00 ppl=62.10                                                
Validation - loss=4.6248e+00 ppl=101.98 best_loss=4.6841e+00 best_ppl=108.22                                            
Epoch 18 - |param|=1.04e+03 |g_param|=2.54e+05 loss=4.1170e+00 ppl=61.37                                                
Validation - loss=4.5764e+00 ppl=97.16 best_loss=4.6248e+00 best_ppl=101.98                                             
Epoch 19 - |param|=1.04e+03 |g_param|=2.60e+05 loss=4.0862e+00 ppl=59.51                                                
Validation - loss=4.5251e+00 ppl=92.31 best_loss=4.5764e+00 best_ppl=97.16                                              
Epoch 20 - |param|=1.04e+03 |g_param|=2.22e+05 loss=3.9631e+00 ppl=52.62                                                
Validation - loss=4.4783e+00 ppl=88.09 best_loss=4.5251e+00 best_ppl=92.31                                              
Epoch 21 - |param|=1.04e+03 |g_param|=2.28e+05 loss=3.8796e+00 ppl=48.41                                                
Validation - loss=4.4320e+00 ppl=84.10 best_loss=4.4783e+00 best_ppl=88.09                                              
Epoch 22 - |param|=1.04e+03 |g_param|=3.05e+05 loss=3.8470e+00 ppl=46.85                                                
Validation - loss=4.3900e+00 ppl=80.64 best_loss=4.4320e+00 best_ppl=84.10                                              
Epoch 23 - |param|=1.04e+03 |g_param|=2.55e+05 loss=3.7583e+00 ppl=42.88                                                
Validation - loss=4.3463e+00 ppl=77.19 best_loss=4.3900e+00 best_ppl=80.64                                              
Epoch 24 - |param|=1.04e+03 |g_param|=2.08e+05 loss=3.7940e+00 ppl=44.43                                                
Validation - loss=4.2969e+00 ppl=73.47 best_loss=4.3463e+00 best_ppl=77.19                                              
Epoch 25 - |param|=1.04e+03 |g_param|=2.65e+05 loss=3.6713e+00 ppl=39.30                                                
Validation - loss=4.2602e+00 ppl=70.82 best_loss=4.2969e+00 best_ppl=73.47                                              
Epoch 26 - |param|=1.04e+03 |g_param|=3.30e+05 loss=3.6004e+00 ppl=36.61                                                
Validation - loss=4.2154e+00 ppl=67.72 best_loss=4.2602e+00 best_ppl=70.82                                              
Epoch 27 - |param|=1.04e+03 |g_param|=3.19e+05 loss=3.6562e+00 ppl=38.71                                                
Validation - loss=4.1779e+00 ppl=65.23 best_loss=4.2154e+00 best_ppl=67.72                                              
Epoch 28 - |param|=1.04e+03 |g_param|=3.47e+05 loss=3.5342e+00 ppl=34.27                                                
Validation - loss=4.1337e+00 ppl=62.41 best_loss=4.1779e+00 best_ppl=65.23                                              
Epoch 29 - |param|=1.04e+03 |g_param|=4.86e+05 loss=3.5125e+00 ppl=33.53                                                
Validation - loss=4.1060e+00 ppl=60.70 best_loss=4.1337e+00 best_ppl=62.41                                              
Epoch 30 - |param|=1.04e+03 |g_param|=2.95e+05 loss=3.4643e+00 ppl=31.95                                                
Validation - loss=4.0544e+00 ppl=57.65 best_loss=4.1060e+00 best_ppl=60.70                                              
Epoch 31 - |param|=1.04e+03 |g_param|=3.74e+05 loss=3.3517e+00 ppl=28.55                                                
Validation - loss=4.0148e+00 ppl=55.41 best_loss=4.0544e+00 best_ppl=57.65                                              
Epoch 32 - |param|=1.04e+03 |g_param|=4.85e+05 loss=3.3160e+00 ppl=27.55                                                
Validation - loss=3.9715e+00 ppl=53.06 best_loss=4.0148e+00 best_ppl=55.41                                              
Epoch 33 - |param|=1.04e+03 |g_param|=4.46e+05 loss=3.3363e+00 ppl=28.11                                                
Validation - loss=3.9351e+00 ppl=51.17 best_loss=3.9715e+00 best_ppl=53.06                                              
Epoch 34 - |param|=1.04e+03 |g_param|=4.57e+05 loss=3.2002e+00 ppl=24.54                                                
Validation - loss=3.8860e+00 ppl=48.71 best_loss=3.9351e+00 best_ppl=51.17                                              
Epoch 35 - |param|=1.04e+03 |g_param|=6.65e+05 loss=3.2688e+00 ppl=26.28                                                
Validation - loss=3.8585e+00 ppl=47.39 best_loss=3.8860e+00 best_ppl=48.71                                              
Epoch 36 - |param|=1.04e+03 |g_param|=3.89e+05 loss=3.1169e+00 ppl=22.58                                                
Validation - loss=3.8042e+00 ppl=44.89 best_loss=3.8585e+00 best_ppl=47.39                                              
Epoch 37 - |param|=1.04e+03 |g_param|=3.58e+05 loss=3.1348e+00 ppl=22.98                                                
Validation - loss=3.7669e+00 ppl=43.24 best_loss=3.8042e+00 best_ppl=44.89                                              
Epoch 38 - |param|=1.04e+03 |g_param|=4.01e+05 loss=3.1409e+00 ppl=23.12                                                
Validation - loss=3.7203e+00 ppl=41.28 best_loss=3.7669e+00 best_ppl=43.24                                              
Epoch 39 - |param|=1.04e+03 |g_param|=3.62e+05 loss=2.9654e+00 ppl=19.40                                                
Validation - loss=3.6773e+00 ppl=39.54 best_loss=3.7203e+00 best_ppl=41.28                                              
Epoch 40 - |param|=1.04e+03 |g_param|=5.09e+05 loss=2.9426e+00 ppl=18.96                                                
Validation - loss=3.6535e+00 ppl=38.61 best_loss=3.6773e+00 best_ppl=39.54                                              
Epoch 41 - |param|=1.04e+03 |g_param|=5.03e+05 loss=2.8965e+00 ppl=18.11                                                
Validation - loss=3.6148e+00 ppl=37.14 best_loss=3.6535e+00 best_ppl=38.61                                              
Epoch 42 - |param|=1.04e+03 |g_param|=4.10e+05 loss=2.8520e+00 ppl=17.32                                                
Validation - loss=3.5668e+00 ppl=35.40 best_loss=3.6148e+00 best_ppl=37.14                                              
Epoch 43 - |param|=1.04e+03 |g_param|=4.18e+05 loss=2.8256e+00 ppl=16.87                                                
Validation - loss=3.5236e+00 ppl=33.90 best_loss=3.5668e+00 best_ppl=35.40                                              
Epoch 44 - |param|=1.04e+03 |g_param|=3.46e+05 loss=2.6648e+00 ppl=14.37                                                
Validation - loss=3.5038e+00 ppl=33.24 best_loss=3.5236e+00 best_ppl=33.90                                              
Epoch 45 - |param|=1.04e+03 |g_param|=4.86e+05 loss=2.7361e+00 ppl=15.43                                                
Validation - loss=3.4505e+00 ppl=31.52 best_loss=3.5038e+00 best_ppl=33.24                                              
Epoch 46 - |param|=1.04e+03 |g_param|=5.23e+05 loss=2.6583e+00 ppl=14.27                                                
Validation - loss=3.4234e+00 ppl=30.67 best_loss=3.4505e+00 best_ppl=31.52                                              
Epoch 47 - |param|=1.04e+03 |g_param|=6.18e+05 loss=2.6496e+00 ppl=14.15                                                
Validation - loss=3.3769e+00 ppl=29.28 best_loss=3.4234e+00 best_ppl=30.67                                              
Epoch 48 - |param|=1.04e+03 |g_param|=6.15e+05 loss=2.6429e+00 ppl=14.05                                                
Validation - loss=3.3406e+00 ppl=28.24 best_loss=3.3769e+00 best_ppl=29.28                                              
Epoch 49 - |param|=1.04e+03 |g_param|=4.78e+05 loss=2.5927e+00 ppl=13.37                                                
Validation - loss=3.2987e+00 ppl=27.08 best_loss=3.3406e+00 best_ppl=28.24                                              
Epoch 50 - |param|=1.04e+03 |g_param|=4.17e+05 loss=2.5664e+00 ppl=13.02                                                
Validation - loss=3.2547e+00 ppl=25.91 best_loss=3.2987e+00 best_ppl=27.08                                              
Epoch 51 - |param|=1.04e+03 |g_param|=4.50e+05 loss=2.4662e+00 ppl=11.78                                                
Validation - loss=3.2313e+00 ppl=25.31 best_loss=3.2547e+00 best_ppl=25.91                                              
Epoch 52 - |param|=1.04e+03 |g_param|=4.32e+05 loss=2.4422e+00 ppl=11.50                                                
Validation - loss=3.1847e+00 ppl=24.16 best_loss=3.2313e+00 best_ppl=25.31                                              
Epoch 53 - |param|=1.04e+03 |g_param|=7.66e+05 loss=2.4798e+00 ppl=11.94                                                
Validation - loss=3.1593e+00 ppl=23.55 best_loss=3.1847e+00 best_ppl=24.16                                              
Epoch 54 - |param|=1.04e+03 |g_param|=8.14e+05 loss=2.3814e+00 ppl=10.82                                                
Validation - loss=3.1707e+00 ppl=23.82 best_loss=3.1593e+00 best_ppl=23.55                                              
Epoch 55 - |param|=1.04e+03 |g_param|=7.32e+05 loss=2.3796e+00 ppl=10.80                                                
Validation - loss=3.0833e+00 ppl=21.83 best_loss=3.1593e+00 best_ppl=23.55                                              
Epoch 56 - |param|=1.04e+03 |g_param|=5.99e+05 loss=2.3497e+00 ppl=10.48                                                
Validation - loss=3.0633e+00 ppl=21.40 best_loss=3.0833e+00 best_ppl=21.83                                              
Epoch 57 - |param|=1.04e+03 |g_param|=5.73e+05 loss=2.2942e+00 ppl=9.92                                                 
Validation - loss=3.0276e+00 ppl=20.65 best_loss=3.0633e+00 best_ppl=21.40                                              
Epoch 58 - |param|=1.04e+03 |g_param|=6.40e+05 loss=2.2223e+00 ppl=9.23                                                 
Validation - loss=2.9935e+00 ppl=19.96 best_loss=3.0276e+00 best_ppl=20.65                                              
Epoch 59 - |param|=1.04e+03 |g_param|=6.26e+05 loss=2.2200e+00 ppl=9.21                                                 
Validation - loss=2.9541e+00 ppl=19.18 best_loss=2.9935e+00 best_ppl=19.96                                              
Epoch 60 - |param|=1.04e+03 |g_param|=7.06e+05 loss=2.1494e+00 ppl=8.58                                                 
Validation - loss=2.9157e+00 ppl=18.46 best_loss=2.9541e+00 best_ppl=19.18                                              
Epoch 61 - |param|=1.04e+03 |g_param|=1.42e+06 loss=2.1818e+00 ppl=8.86                                                 
Validation - loss=2.9248e+00 ppl=18.63 best_loss=2.9157e+00 best_ppl=18.46                                              
Epoch 62 - |param|=1.04e+03 |g_param|=8.51e+05 loss=2.1285e+00 ppl=8.40                                                 
Validation - loss=2.8835e+00 ppl=17.88 best_loss=2.9157e+00 best_ppl=18.46                                              
Epoch 63 - |param|=1.04e+03 |g_param|=1.44e+06 loss=2.1306e+00 ppl=8.42                                                 
Validation - loss=2.8468e+00 ppl=17.23 best_loss=2.8835e+00 best_ppl=17.88                                              
Epoch 64 - |param|=1.04e+03 |g_param|=1.30e+06 loss=2.0341e+00 ppl=7.65                                                 
Validation - loss=2.8341e+00 ppl=17.02 best_loss=2.8468e+00 best_ppl=17.23                                              
Epoch 65 - |param|=1.04e+03 |g_param|=1.12e+06 loss=2.0418e+00 ppl=7.70                                                 
Validation - loss=2.7751e+00 ppl=16.04 best_loss=2.8341e+00 best_ppl=17.02                                              
Epoch 66 - |param|=1.04e+03 |g_param|=9.72e+05 loss=1.9887e+00 ppl=7.31                                                 
Validation - loss=2.7774e+00 ppl=16.08 best_loss=2.7751e+00 best_ppl=16.04                                              
Epoch 67 - |param|=1.04e+03 |g_param|=8.45e+05 loss=1.9451e+00 ppl=6.99                                                 
Validation - loss=2.7410e+00 ppl=15.50 best_loss=2.7751e+00 best_ppl=16.04                                              
Epoch 68 - |param|=1.04e+03 |g_param|=4.71e+05 loss=1.8877e+00 ppl=6.60                                                 
Validation - loss=2.7191e+00 ppl=15.17 best_loss=2.7410e+00 best_ppl=15.50                                              
Epoch 69 - |param|=1.04e+03 |g_param|=3.54e+05 loss=1.8867e+00 ppl=6.60                                                 
Validation - loss=2.6700e+00 ppl=14.44 best_loss=2.7191e+00 best_ppl=15.17                                              
Epoch 70 - |param|=1.04e+03 |g_param|=4.33e+05 loss=1.9336e+00 ppl=6.91                                                 
Validation - loss=2.6543e+00 ppl=14.21 best_loss=2.6700e+00 best_ppl=14.44                                              
Epoch 71 - |param|=1.04e+03 |g_param|=3.25e+05 loss=1.8649e+00 ppl=6.46                                                 
Validation - loss=2.6228e+00 ppl=13.77 best_loss=2.6543e+00 best_ppl=14.21                                              
Epoch 72 - |param|=1.04e+03 |g_param|=3.42e+05 loss=1.7896e+00 ppl=5.99                                                 
Validation - loss=2.6010e+00 ppl=13.48 best_loss=2.6228e+00 best_ppl=13.77                                              
Epoch 73 - |param|=1.04e+03 |g_param|=7.28e+05 loss=1.8319e+00 ppl=6.25                                                 
Validation - loss=2.5931e+00 ppl=13.37 best_loss=2.6010e+00 best_ppl=13.48                                              
Epoch 74 - |param|=1.04e+03 |g_param|=4.82e+05 loss=1.7683e+00 ppl=5.86                                                 
Validation - loss=2.5692e+00 ppl=13.05 best_loss=2.5931e+00 best_ppl=13.37                                              
Epoch 75 - |param|=1.04e+03 |g_param|=3.82e+05 loss=1.7157e+00 ppl=5.56                                                 
Validation - loss=2.5505e+00 ppl=12.81 best_loss=2.5692e+00 best_ppl=13.05                                              
Epoch 76 - |param|=1.04e+03 |g_param|=3.58e+05 loss=1.7451e+00 ppl=5.73                                                 
Validation - loss=2.5336e+00 ppl=12.60 best_loss=2.5505e+00 best_ppl=12.81                                              
Epoch 77 - |param|=1.04e+03 |g_param|=3.64e+05 loss=1.6693e+00 ppl=5.31                                                 
Validation - loss=2.5223e+00 ppl=12.46 best_loss=2.5336e+00 best_ppl=12.60                                              
Epoch 78 - |param|=1.04e+03 |g_param|=4.64e+05 loss=1.6241e+00 ppl=5.07                                                 
Validation - loss=2.4780e+00 ppl=11.92 best_loss=2.5223e+00 best_ppl=12.46                                              
Epoch 79 - |param|=1.04e+03 |g_param|=4.55e+05 loss=1.6828e+00 ppl=5.38                                                 
Validation - loss=2.4769e+00 ppl=11.90 best_loss=2.4780e+00 best_ppl=11.92                                              
Epoch 80 - |param|=1.04e+03 |g_param|=3.92e+05 loss=1.6139e+00 ppl=5.02                                                 
Validation - loss=2.4635e+00 ppl=11.75 best_loss=2.4769e+00 best_ppl=11.90                                              
Epoch 81 - |param|=1.04e+03 |g_param|=3.23e+05 loss=1.5988e+00 ppl=4.95                                                 
Validation - loss=2.4291e+00 ppl=11.35 best_loss=2.4635e+00 best_ppl=11.75                                              
Epoch 82 - |param|=1.04e+03 |g_param|=6.63e+05 loss=1.5706e+00 ppl=4.81                                                 
Validation - loss=2.4483e+00 ppl=11.57 best_loss=2.4291e+00 best_ppl=11.35                                              
Epoch 83 - |param|=1.04e+03 |g_param|=1.29e+06 loss=1.6192e+00 ppl=5.05                                                 
Validation - loss=2.4567e+00 ppl=11.67 best_loss=2.4291e+00 best_ppl=11.35                                              
Epoch 84 - |param|=1.04e+03 |g_param|=7.27e+05 loss=1.5803e+00 ppl=4.86                                                 
Validation - loss=2.4623e+00 ppl=11.73 best_loss=2.4291e+00 best_ppl=11.35                                              
Epoch 85 - |param|=1.04e+03 |g_param|=4.91e+05 loss=1.4766e+00 ppl=4.38                                                 
Validation - loss=2.3944e+00 ppl=10.96 best_loss=2.4291e+00 best_ppl=11.35                                              
Epoch 86 - |param|=1.04e+03 |g_param|=7.88e+05 loss=1.4583e+00 ppl=4.30                                                 
Validation - loss=2.4036e+00 ppl=11.06 best_loss=2.3944e+00 best_ppl=10.96                                              
Epoch 87 - |param|=1.04e+03 |g_param|=7.91e+05 loss=1.5179e+00 ppl=4.56                                                 
Validation - loss=2.4210e+00 ppl=11.26 best_loss=2.3944e+00 best_ppl=10.96                                              
Epoch 88 - |param|=1.04e+03 |g_param|=3.81e+05 loss=1.4558e+00 ppl=4.29                                                 
Validation - loss=2.3489e+00 ppl=10.47 best_loss=2.3944e+00 best_ppl=10.96                                              
Epoch 89 - |param|=1.04e+03 |g_param|=4.46e+05 loss=1.4331e+00 ppl=4.19                                                 
Validation - loss=2.3132e+00 ppl=10.11 best_loss=2.3489e+00 best_ppl=10.47                                              
Epoch 90 - |param|=1.04e+03 |g_param|=5.22e+05 loss=1.3945e+00 ppl=4.03                                                 
Validation - loss=2.3429e+00 ppl=10.41 best_loss=2.3132e+00 best_ppl=10.11                                              
Epoch 91 - |param|=1.04e+03 |g_param|=5.22e+05 loss=1.3531e+00 ppl=3.87                                                 
Validation - loss=2.3354e+00 ppl=10.33 best_loss=2.3132e+00 best_ppl=10.11                                              
Epoch 92 - |param|=1.04e+03 |g_param|=6.42e+05 loss=1.3217e+00 ppl=3.75                                                 
Validation - loss=2.3107e+00 ppl=10.08 best_loss=2.3132e+00 best_ppl=10.11                                              
Epoch 93 - |param|=1.04e+03 |g_param|=1.27e+06 loss=1.3982e+00 ppl=4.05                                                 
Validation - loss=2.3791e+00 ppl=10.80 best_loss=2.3107e+00 best_ppl=10.08                                              
Epoch 94 - |param|=1.04e+03 |g_param|=4.78e+05 loss=1.3026e+00 ppl=3.68                                                 
Validation - loss=2.2959e+00 ppl=9.93 best_loss=2.3107e+00 best_ppl=10.08                                               
Epoch 95 - |param|=1.04e+03 |g_param|=1.21e+06 loss=1.3893e+00 ppl=4.01                                                 
Validation - loss=2.3514e+00 ppl=10.50 best_loss=2.2959e+00 best_ppl=9.93                                               
Epoch 96 - |param|=1.04e+03 |g_param|=5.34e+05 loss=1.3085e+00 ppl=3.70                                                 
Validation - loss=2.2600e+00 ppl=9.58 best_loss=2.2959e+00 best_ppl=9.93                                                
Epoch 97 - |param|=1.04e+03 |g_param|=4.32e+05 loss=1.3136e+00 ppl=3.72                                                 
Validation - loss=2.2604e+00 ppl=9.59 best_loss=2.2600e+00 best_ppl=9.58                                                
Epoch 98 - |param|=1.04e+03 |g_param|=2.15e+06 loss=1.4026e+00 ppl=4.07                                                 
Validation - loss=2.3643e+00 ppl=10.64 best_loss=2.2600e+00 best_ppl=9.58                                               
Epoch 99 - |param|=1.04e+03 |g_param|=4.66e+05 loss=1.3267e+00 ppl=3.77                                                 
Validation - loss=2.2627e+00 ppl=9.61 best_loss=2.2600e+00 best_ppl=9.58                                                
Epoch 100 - |param|=1.04e+03 |g_param|=4.83e+05 loss=1.1727e+00 ppl=3.23                                                
Validation - loss=2.2425e+00 ppl=9.42 best_loss=2.2600e+00 best_ppl=9.58                                                
Epoch 101 - |param|=1.04e+03 |g_param|=8.98e+05 loss=1.2481e+00 ppl=3.48                                                
Validation - loss=2.2345e+00 ppl=9.34 best_loss=2.2425e+00 best_ppl=9.42                                                
Epoch 102 - |param|=1.04e+03 |g_param|=6.98e+05 loss=1.2425e+00 ppl=3.46                                                
Validation - loss=2.2267e+00 ppl=9.27 best_loss=2.2345e+00 best_ppl=9.34                                                
Epoch 103 - |param|=1.04e+03 |g_param|=4.59e+05 loss=1.2055e+00 ppl=3.34                                                
Validation - loss=2.2173e+00 ppl=9.18 best_loss=2.2267e+00 best_ppl=9.27                                                
Epoch 104 - |param|=1.04e+03 |g_param|=8.71e+05 loss=1.2107e+00 ppl=3.36                                                
Validation - loss=2.2205e+00 ppl=9.21 best_loss=2.2173e+00 best_ppl=9.18                                                
Epoch 105 - |param|=1.04e+03 |g_param|=7.70e+05 loss=1.1921e+00 ppl=3.29                                                
Validation - loss=2.2611e+00 ppl=9.59 best_loss=2.2173e+00 best_ppl=9.18                                                
Epoch 106 - |param|=1.04e+03 |g_param|=3.52e+05 loss=1.1442e+00 ppl=3.14                                                
Validation - loss=2.1997e+00 ppl=9.02 best_loss=2.2173e+00 best_ppl=9.18                                                
Epoch 107 - |param|=1.04e+03 |g_param|=1.00e+06 loss=1.1615e+00 ppl=3.19                                                
Validation - loss=2.2112e+00 ppl=9.13 best_loss=2.1997e+00 best_ppl=9.02                                                
Epoch 108 - |param|=1.04e+03 |g_param|=2.54e+05 loss=1.1181e+00 ppl=3.06                                                
Validation - loss=2.1757e+00 ppl=8.81 best_loss=2.1997e+00 best_ppl=9.02                                                
Epoch 109 - |param|=1.04e+03 |g_param|=3.23e+05 loss=1.1022e+00 ppl=3.01                                                
Validation - loss=2.1818e+00 ppl=8.86 best_loss=2.1757e+00 best_ppl=8.81                                                
Epoch 110 - |param|=1.04e+03 |g_param|=3.17e+05 loss=1.0807e+00 ppl=2.95                                                
Validation - loss=2.1639e+00 ppl=8.71 best_loss=2.1757e+00 best_ppl=8.81                                                
Epoch 111 - |param|=1.04e+03 |g_param|=1.78e+05 loss=1.1202e+00 ppl=3.07                                                
Validation - loss=2.1567e+00 ppl=8.64 best_loss=2.1639e+00 best_ppl=8.71                                                
Epoch 112 - |param|=1.04e+03 |g_param|=3.38e+05 loss=1.1226e+00 ppl=3.07                                                
Validation - loss=2.1535e+00 ppl=8.62 best_loss=2.1567e+00 best_ppl=8.64                                                
Epoch 113 - |param|=1.04e+03 |g_param|=3.42e+05 loss=1.1339e+00 ppl=3.11                                                
Validation - loss=2.1699e+00 ppl=8.76 best_loss=2.1535e+00 best_ppl=8.62                                                
Epoch 114 - |param|=1.04e+03 |g_param|=3.67e+05 loss=1.0207e+00 ppl=2.78                                                
Validation - loss=2.1387e+00 ppl=8.49 best_loss=2.1535e+00 best_ppl=8.62                                                
Epoch 115 - |param|=1.04e+03 |g_param|=3.09e+05 loss=1.0283e+00 ppl=2.80                                                
Validation - loss=2.2154e+00 ppl=9.17 best_loss=2.1387e+00 best_ppl=8.49                                                
Epoch 116 - |param|=1.04e+03 |g_param|=3.65e+05 loss=1.0788e+00 ppl=2.94                                                
Validation - loss=2.1376e+00 ppl=8.48 best_loss=2.1387e+00 best_ppl=8.49                                                
Epoch 117 - |param|=1.04e+03 |g_param|=5.65e+05 loss=1.0821e+00 ppl=2.95                                                
Validation - loss=2.1801e+00 ppl=8.85 best_loss=2.1376e+00 best_ppl=8.48                                                
Epoch 118 - |param|=1.04e+03 |g_param|=1.77e+05 loss=1.0208e+00 ppl=2.78                                                
Validation - loss=2.1501e+00 ppl=8.59 best_loss=2.1376e+00 best_ppl=8.48                                                
Epoch 119 - |param|=1.04e+03 |g_param|=2.88e+05 loss=9.9483e-01 ppl=2.70                                                
Validation - loss=2.1467e+00 ppl=8.56 best_loss=2.1376e+00 best_ppl=8.48                                                
Epoch 120 - |param|=1.04e+03 |g_param|=6.00e+05 loss=1.0183e+00 ppl=2.77                                                
Validation - loss=2.1587e+00 ppl=8.66 best_loss=2.1376e+00 best_ppl=8.48                                                
Epoch 121 - |param|=1.04e+03 |g_param|=2.76e+05 loss=1.0198e+00 ppl=2.77                                                
Validation - loss=2.1608e+00 ppl=8.68 best_loss=2.1376e+00 best_ppl=8.48                                                
Epoch 122 - |param|=1.04e+03 |g_param|=2.05e+05 loss=1.0033e+00 ppl=2.73                                                
Validation - loss=2.1130e+00 ppl=8.27 best_loss=2.1376e+00 best_ppl=8.48                                                
Epoch 123 - |param|=1.04e+03 |g_param|=2.82e+05 loss=1.0041e+00 ppl=2.73                                                
Validation - loss=2.1374e+00 ppl=8.48 best_loss=2.1130e+00 best_ppl=8.27                                                
Epoch 124 - |param|=1.04e+03 |g_param|=3.03e+05 loss=1.0081e+00 ppl=2.74                                                
Validation - loss=2.1291e+00 ppl=8.41 best_loss=2.1130e+00 best_ppl=8.27                                                
Epoch 125 - |param|=1.04e+03 |g_param|=2.30e+05 loss=1.0072e+00 ppl=2.74                                                
Validation - loss=2.0978e+00 ppl=8.15 best_loss=2.1130e+00 best_ppl=8.27                                                
Epoch 126 - |param|=1.04e+03 |g_param|=1.99e+05 loss=9.6708e-01 ppl=2.63                                                
Validation - loss=2.1407e+00 ppl=8.51 best_loss=2.0978e+00 best_ppl=8.15                                                
Epoch 127 - |param|=1.04e+03 |g_param|=1.51e+05 loss=9.3365e-01 ppl=2.54                                                
Validation - loss=2.1173e+00 ppl=8.31 best_loss=2.0978e+00 best_ppl=8.15                                                
Epoch 128 - |param|=1.04e+03 |g_param|=2.68e+05 loss=9.5501e-01 ppl=2.60                                                
Validation - loss=2.1390e+00 ppl=8.49 best_loss=2.0978e+00 best_ppl=8.15                                                
Epoch 129 - |param|=1.04e+03 |g_param|=2.33e+05 loss=9.3075e-01 ppl=2.54                                                
Validation - loss=2.1123e+00 ppl=8.27 best_loss=2.0978e+00 best_ppl=8.15                                                
Epoch 130 - |param|=1.04e+03 |g_param|=1.50e+05 loss=8.8060e-01 ppl=2.41                                                
Validation - loss=2.1008e+00 ppl=8.17 best_loss=2.0978e+00 best_ppl=8.15                                                
Epoch 131 - |param|=1.04e+03 |g_param|=1.21e+05 loss=8.6450e-01 ppl=2.37                                                
Validation - loss=2.0897e+00 ppl=8.08 best_loss=2.0978e+00 best_ppl=8.15                                                
Epoch 132 - |param|=1.04e+03 |g_param|=4.45e+05 loss=9.4905e-01 ppl=2.58                                                
Validation - loss=2.1460e+00 ppl=8.55 best_loss=2.0897e+00 best_ppl=8.08                                                
Epoch 133 - |param|=1.04e+03 |g_param|=2.04e+05 loss=8.7260e-01 ppl=2.39                                                
Validation - loss=2.0928e+00 ppl=8.11 best_loss=2.0897e+00 best_ppl=8.08                                                
Epoch 134 - |param|=1.04e+03 |g_param|=3.42e+05 loss=8.6894e-01 ppl=2.38                                                
Validation - loss=2.0815e+00 ppl=8.02 best_loss=2.0897e+00 best_ppl=8.08                                                
Epoch 135 - |param|=1.04e+03 |g_param|=1.09e+05 loss=8.1637e-01 ppl=2.26                                                
Validation - loss=2.1190e+00 ppl=8.32 best_loss=2.0815e+00 best_ppl=8.02                                                
Epoch 136 - |param|=1.04e+03 |g_param|=2.47e+05 loss=8.6048e-01 ppl=2.36                                                
Validation - loss=2.0719e+00 ppl=7.94 best_loss=2.0815e+00 best_ppl=8.02                                                
Epoch 137 - |param|=1.04e+03 |g_param|=2.53e+05 loss=8.5205e-01 ppl=2.34                                                
Validation - loss=2.1666e+00 ppl=8.73 best_loss=2.0719e+00 best_ppl=7.94                                                
Epoch 138 - |param|=1.04e+03 |g_param|=2.23e+05 loss=8.3993e-01 ppl=2.32                                                
Validation - loss=2.1572e+00 ppl=8.65 best_loss=2.0719e+00 best_ppl=7.94                                                
Epoch 139 - |param|=1.04e+03 |g_param|=2.31e+05 loss=7.9022e-01 ppl=2.20                                                
Validation - loss=2.0827e+00 ppl=8.03 best_loss=2.0719e+00 best_ppl=7.94                                                
Epoch 140 - |param|=1.04e+03 |g_param|=3.66e+05 loss=8.8313e-01 ppl=2.42                                                
Validation - loss=2.0845e+00 ppl=8.04 best_loss=2.0719e+00 best_ppl=7.94                                                
Epoch 141 - |param|=1.04e+03 |g_param|=3.63e+05 loss=8.2918e-01 ppl=2.29                                                
Validation - loss=2.0666e+00 ppl=7.90 best_loss=2.0719e+00 best_ppl=7.94                                                
Epoch 142 - |param|=1.04e+03 |g_param|=2.81e+05 loss=8.4203e-01 ppl=2.32                                                
Validation - loss=2.0654e+00 ppl=7.89 best_loss=2.0666e+00 best_ppl=7.90                                                
Epoch 143 - |param|=1.04e+03 |g_param|=2.74e+05 loss=8.0910e-01 ppl=2.25                                                
Validation - loss=2.1072e+00 ppl=8.23 best_loss=2.0654e+00 best_ppl=7.89                                                
Epoch 144 - |param|=1.04e+03 |g_param|=2.22e+05 loss=8.1066e-01 ppl=2.25                                                
Validation - loss=2.1318e+00 ppl=8.43 best_loss=2.0654e+00 best_ppl=7.89                                                
Epoch 145 - |param|=1.04e+03 |g_param|=1.88e+05 loss=7.7959e-01 ppl=2.18                                                
Validation - loss=2.0565e+00 ppl=7.82 best_loss=2.0654e+00 best_ppl=7.89                                                
Epoch 146 - |param|=1.04e+03 |g_param|=1.33e+05 loss=8.3399e-01 ppl=2.30                                                
Validation - loss=2.0706e+00 ppl=7.93 best_loss=2.0565e+00 best_ppl=7.82                                                
Epoch 147 - |param|=1.04e+03 |g_param|=3.11e+05 loss=7.9246e-01 ppl=2.21                                                
Validation - loss=2.0807e+00 ppl=8.01 best_loss=2.0565e+00 best_ppl=7.82                                                
Epoch 148 - |param|=1.04e+03 |g_param|=1.73e+05 loss=8.1153e-01 ppl=2.25                                                
Validation - loss=2.0703e+00 ppl=7.93 best_loss=2.0565e+00 best_ppl=7.82                                                
Epoch 149 - |param|=1.04e+03 |g_param|=2.19e+05 loss=7.9415e-01 ppl=2.21                                                
Validation - loss=2.0822e+00 ppl=8.02 best_loss=2.0565e+00 best_ppl=7.82                                                
Epoch 150 - |param|=1.04e+03 |g_param|=1.38e+05 loss=7.2497e-01 ppl=2.06                                                
Validation - loss=2.0641e+00 ppl=7.88 best_loss=2.0565e+00 best_ppl=7.82                                                
Epoch 151 - |param|=1.04e+03 |g_param|=4.94e+05 loss=8.1935e-01 ppl=2.27                                                
Validation - loss=2.0874e+00 ppl=8.06 best_loss=2.0565e+00 best_ppl=7.82                                                
Epoch 152 - |param|=1.04e+03 |g_param|=2.81e+05 loss=7.9763e-01 ppl=2.22                                                
Validation - loss=2.0782e+00 ppl=7.99 best_loss=2.0565e+00 best_ppl=7.82                                                
Epoch 153 - |param|=1.04e+03 |g_param|=2.00e+05 loss=7.1985e-01 ppl=2.05                                                
Validation - loss=2.0514e+00 ppl=7.78 best_loss=2.0565e+00 best_ppl=7.82                                                
Epoch 154 - |param|=1.04e+03 |g_param|=1.57e+05 loss=7.2472e-01 ppl=2.06                                                
Validation - loss=2.0368e+00 ppl=7.67 best_loss=2.0514e+00 best_ppl=7.78                                                
Epoch 155 - |param|=1.04e+03 |g_param|=1.69e+05 loss=7.4116e-01 ppl=2.10                                                
Validation - loss=2.0425e+00 ppl=7.71 best_loss=2.0368e+00 best_ppl=7.67                                                
Epoch 156 - |param|=1.04e+03 |g_param|=2.73e+05 loss=7.9183e-01 ppl=2.21                                                
Validation - loss=2.0409e+00 ppl=7.70 best_loss=2.0368e+00 best_ppl=7.67                                                
Epoch 157 - |param|=1.04e+03 |g_param|=5.26e+05 loss=7.8100e-01 ppl=2.18                                                
Validation - loss=2.1008e+00 ppl=8.17 best_loss=2.0368e+00 best_ppl=7.67                                                
Epoch 158 - |param|=1.04e+03 |g_param|=1.77e+05 loss=7.1352e-01 ppl=2.04                                                
Validation - loss=2.0268e+00 ppl=7.59 best_loss=2.0368e+00 best_ppl=7.67                                                
Epoch 159 - |param|=1.04e+03 |g_param|=1.50e+05 loss=6.6361e-01 ppl=1.94                                                
Validation - loss=2.0205e+00 ppl=7.54 best_loss=2.0268e+00 best_ppl=7.59                                                
Epoch 160 - |param|=1.04e+03 |g_param|=1.89e+05 loss=7.5148e-01 ppl=2.12                                                
Validation - loss=2.0459e+00 ppl=7.74 best_loss=2.0205e+00 best_ppl=7.54                                                
Epoch 161 - |param|=1.04e+03 |g_param|=1.79e+05 loss=6.9075e-01 ppl=2.00                                                
Validation - loss=2.0265e+00 ppl=7.59 best_loss=2.0205e+00 best_ppl=7.54                                                
Epoch 162 - |param|=1.04e+03 |g_param|=1.87e+05 loss=6.9818e-01 ppl=2.01                                                
Validation - loss=2.0219e+00 ppl=7.55 best_loss=2.0205e+00 best_ppl=7.54                                                
Epoch 163 - |param|=1.04e+03 |g_param|=2.46e+05 loss=6.3399e-01 ppl=1.89                                                
Validation - loss=2.0256e+00 ppl=7.58 best_loss=2.0205e+00 best_ppl=7.54                                                
Epoch 164 - |param|=1.04e+03 |g_param|=9.25e+04 loss=6.6821e-01 ppl=1.95                                                
Validation - loss=2.0234e+00 ppl=7.56 best_loss=2.0205e+00 best_ppl=7.54                                                
Epoch 165 - |param|=1.04e+03 |g_param|=1.77e+05 loss=6.8515e-01 ppl=1.98                                                
Validation - loss=2.0346e+00 ppl=7.65 best_loss=2.0205e+00 best_ppl=7.54                                                
Epoch 166 - |param|=1.04e+03 |g_param|=1.92e+05 loss=6.9103e-01 ppl=2.00                                                
Validation - loss=2.0417e+00 ppl=7.70 best_loss=2.0205e+00 best_ppl=7.54                                                
Epoch 167 - |param|=1.04e+03 |g_param|=3.69e+05 loss=7.1277e-01 ppl=2.04                                                
Validation - loss=2.0199e+00 ppl=7.54 best_loss=2.0205e+00 best_ppl=7.54                                                
Epoch 168 - |param|=1.04e+03 |g_param|=1.61e+05 loss=6.6752e-01 ppl=1.95                                                
Validation - loss=2.0130e+00 ppl=7.49 best_loss=2.0199e+00 best_ppl=7.54                                                
Epoch 169 - |param|=1.04e+03 |g_param|=1.58e+05 loss=6.8212e-01 ppl=1.98                                                
Validation - loss=2.0004e+00 ppl=7.39 best_loss=2.0130e+00 best_ppl=7.49                                                
Epoch 170 - |param|=1.04e+03 |g_param|=1.34e+05 loss=6.4519e-01 ppl=1.91                                                
Validation - loss=2.0125e+00 ppl=7.48 best_loss=2.0004e+00 best_ppl=7.39                                                
Epoch 171 - |param|=1.04e+03 |g_param|=1.86e+05 loss=6.7031e-01 ppl=1.95                                                
Validation - loss=1.9976e+00 ppl=7.37 best_loss=2.0004e+00 best_ppl=7.39                                                
Epoch 172 - |param|=1.04e+03 |g_param|=1.64e+05 loss=6.8026e-01 ppl=1.97                                                
Validation - loss=2.0093e+00 ppl=7.46 best_loss=1.9976e+00 best_ppl=7.37                                                
Epoch 173 - |param|=1.04e+03 |g_param|=1.70e+05 loss=6.5413e-01 ppl=1.92                                                
Validation - loss=1.9729e+00 ppl=7.19 best_loss=1.9976e+00 best_ppl=7.37                                                
Epoch 174 - |param|=1.04e+03 |g_param|=2.59e+05 loss=6.5980e-01 ppl=1.93                                                
Validation - loss=2.0102e+00 ppl=7.46 best_loss=1.9729e+00 best_ppl=7.19                                                
Epoch 175 - |param|=1.04e+03 |g_param|=1.76e+05 loss=6.1713e-01 ppl=1.85                                                
Validation - loss=2.0478e+00 ppl=7.75 best_loss=1.9729e+00 best_ppl=7.19                                                
Epoch 176 - |param|=1.04e+03 |g_param|=2.36e+05 loss=6.3205e-01 ppl=1.88                                                
Validation - loss=2.0072e+00 ppl=7.44 best_loss=1.9729e+00 best_ppl=7.19                                                
Epoch 177 - |param|=1.04e+03 |g_param|=1.07e+05 loss=6.1875e-01 ppl=1.86                                                
Validation - loss=2.0092e+00 ppl=7.46 best_loss=1.9729e+00 best_ppl=7.19                                                
Epoch 178 - |param|=1.04e+03 |g_param|=1.38e+05 loss=6.0253e-01 ppl=1.83                                                
Validation - loss=1.9873e+00 ppl=7.30 best_loss=1.9729e+00 best_ppl=7.19                                                
Epoch 179 - |param|=1.04e+03 |g_param|=1.74e+05 loss=5.8629e-01 ppl=1.80                                                
Validation - loss=2.0143e+00 ppl=7.50 best_loss=1.9729e+00 best_ppl=7.19                                                
Epoch 180 - |param|=1.04e+03 |g_param|=1.98e+05 loss=6.1513e-01 ppl=1.85                                                
Validation - loss=1.9769e+00 ppl=7.22 best_loss=1.9729e+00 best_ppl=7.19                                                
Epoch 181 - |param|=1.04e+03 |g_param|=1.70e+05 loss=6.3201e-01 ppl=1.88                                                
Validation - loss=2.0033e+00 ppl=7.41 best_loss=1.9729e+00 best_ppl=7.19                                                
Epoch 182 - |param|=1.04e+03 |g_param|=1.65e+05 loss=5.9757e-01 ppl=1.82                                                
Validation - loss=1.9664e+00 ppl=7.14 best_loss=1.9729e+00 best_ppl=7.19                                                
Epoch 183 - |param|=1.04e+03 |g_param|=2.95e+05 loss=6.2269e-01 ppl=1.86                                                
Validation - loss=1.9827e+00 ppl=7.26 best_loss=1.9664e+00 best_ppl=7.14                                                
Epoch 184 - |param|=1.05e+03 |g_param|=3.64e+05 loss=6.6025e-01 ppl=1.94                                                
Validation - loss=2.0183e+00 ppl=7.53 best_loss=1.9664e+00 best_ppl=7.14                                                
Epoch 185 - |param|=1.05e+03 |g_param|=1.17e+05 loss=6.0103e-01 ppl=1.82                                                
Validation - loss=1.9780e+00 ppl=7.23 best_loss=1.9664e+00 best_ppl=7.14                                                
Epoch 186 - |param|=1.05e+03 |g_param|=4.81e+05 loss=6.3834e-01 ppl=1.89                                                
Validation - loss=2.0119e+00 ppl=7.48 best_loss=1.9664e+00 best_ppl=7.14                                                
Epoch 187 - |param|=1.05e+03 |g_param|=2.23e+05 loss=5.9219e-01 ppl=1.81                                                
Validation - loss=1.9848e+00 ppl=7.28 best_loss=1.9664e+00 best_ppl=7.14                                                
Epoch 188 - |param|=1.05e+03 |g_param|=2.27e+05 loss=5.7465e-01 ppl=1.78                                                
Validation - loss=1.9696e+00 ppl=7.17 best_loss=1.9664e+00 best_ppl=7.14                                                
Epoch 189 - |param|=1.05e+03 |g_param|=4.46e+05 loss=5.8517e-01 ppl=1.80                                                
Validation - loss=1.9872e+00 ppl=7.30 best_loss=1.9664e+00 best_ppl=7.14                                                
Epoch 190 - |param|=1.05e+03 |g_param|=2.71e+05 loss=5.4693e-01 ppl=1.73                                                
Validation - loss=1.9943e+00 ppl=7.35 best_loss=1.9664e+00 best_ppl=7.14                                                
Epoch 191 - |param|=1.05e+03 |g_param|=3.07e+05 loss=5.6673e-01 ppl=1.76                                                
Validation - loss=1.9412e+00 ppl=6.97 best_loss=1.9664e+00 best_ppl=7.14                                                
Epoch 192 - |param|=1.05e+03 |g_param|=1.15e+06 loss=6.4823e-01 ppl=1.91                                                
Validation - loss=2.0248e+00 ppl=7.57 best_loss=1.9412e+00 best_ppl=6.97                                                
Epoch 193 - |param|=1.05e+03 |g_param|=2.48e+05 loss=5.6497e-01 ppl=1.76                                                
Validation - loss=1.9621e+00 ppl=7.11 best_loss=1.9412e+00 best_ppl=6.97                                                
Epoch 194 - |param|=1.05e+03 |g_param|=2.10e+05 loss=5.5360e-01 ppl=1.74                                                
Validation - loss=1.9728e+00 ppl=7.19 best_loss=1.9412e+00 best_ppl=6.97                                                
Epoch 195 - |param|=1.05e+03 |g_param|=5.06e+05 loss=6.1531e-01 ppl=1.85                                                
Validation - loss=1.9684e+00 ppl=7.16 best_loss=1.9412e+00 best_ppl=6.97                                                
Epoch 196 - |param|=1.05e+03 |g_param|=2.01e+05 loss=5.4093e-01 ppl=1.72                                                
Validation - loss=1.9783e+00 ppl=7.23 best_loss=1.9412e+00 best_ppl=6.97                                                
Epoch 197 - |param|=1.05e+03 |g_param|=1.36e+05 loss=5.4564e-01 ppl=1.73                                                
Validation - loss=1.9493e+00 ppl=7.02 best_loss=1.9412e+00 best_ppl=6.97                                                
Epoch 198 - |param|=1.05e+03 |g_param|=1.66e+05 loss=5.9448e-01 ppl=1.81                                                
Validation - loss=1.9456e+00 ppl=7.00 best_loss=1.9412e+00 best_ppl=6.97                                                
Epoch 199 - |param|=1.05e+03 |g_param|=2.87e+05 loss=5.3300e-01 ppl=1.70                                                
Validation - loss=1.9589e+00 ppl=7.09 best_loss=1.9412e+00 best_ppl=6.97                                                
Epoch 200 - |param|=1.05e+03 |g_param|=3.52e+05 loss=5.8474e-01 ppl=1.79                                                
Validation - loss=1.9646e+00 ppl=7.13 best_loss=1.9412e+00 best_ppl=6.97                                                
Epoch 201 - |param|=1.05e+03 |g_param|=2.68e+05 loss=5.4818e-01 ppl=1.73                                                
Validation - loss=1.9299e+00 ppl=6.89 best_loss=1.9412e+00 best_ppl=6.97                                                
Epoch 202 - |param|=1.05e+03 |g_param|=1.20e+05 loss=5.3049e-01 ppl=1.70                                                
Validation - loss=1.9306e+00 ppl=6.89 best_loss=1.9299e+00 best_ppl=6.89                                                
Epoch 203 - |param|=1.05e+03 |g_param|=1.35e+05 loss=5.9077e-01 ppl=1.81                                                
Validation - loss=1.9393e+00 ppl=6.95 best_loss=1.9299e+00 best_ppl=6.89                                                
Epoch 204 - |param|=1.05e+03 |g_param|=3.77e+05 loss=6.0572e-01 ppl=1.83                                                
Validation - loss=2.0225e+00 ppl=7.56 best_loss=1.9299e+00 best_ppl=6.89                                                
Epoch 205 - |param|=1.05e+03 |g_param|=1.56e+05 loss=5.6288e-01 ppl=1.76                                                
Validation - loss=1.9411e+00 ppl=6.97 best_loss=1.9299e+00 best_ppl=6.89                                                
Epoch 206 - |param|=1.05e+03 |g_param|=1.88e+05 loss=4.9600e-01 ppl=1.64                                                
Validation - loss=1.9785e+00 ppl=7.23 best_loss=1.9299e+00 best_ppl=6.89                                                
Epoch 207 - |param|=1.05e+03 |g_param|=2.36e+05 loss=5.1056e-01 ppl=1.67                                                
Validation - loss=1.9406e+00 ppl=6.96 best_loss=1.9299e+00 best_ppl=6.89                                                
Epoch 208 - |param|=1.05e+03 |g_param|=1.27e+05 loss=5.2675e-01 ppl=1.69                                                
Validation - loss=1.9507e+00 ppl=7.03 best_loss=1.9299e+00 best_ppl=6.89                                                
Epoch 209 - |param|=1.05e+03 |g_param|=2.65e+05 loss=5.3969e-01 ppl=1.72                                                
Validation - loss=1.9679e+00 ppl=7.16 best_loss=1.9299e+00 best_ppl=6.89                                                
Epoch 210 - |param|=1.05e+03 |g_param|=1.34e+05 loss=5.2855e-01 ppl=1.70                                                
Validation - loss=1.9438e+00 ppl=6.99 best_loss=1.9299e+00 best_ppl=6.89                                                
Epoch 211 - |param|=1.05e+03 |g_param|=1.27e+05 loss=4.7253e-01 ppl=1.60                                                
Validation - loss=1.9305e+00 ppl=6.89 best_loss=1.9299e+00 best_ppl=6.89                                                
Epoch 212 - |param|=1.05e+03 |g_param|=1.93e+05 loss=5.3199e-01 ppl=1.70                                                
Validation - loss=1.9538e+00 ppl=7.06 best_loss=1.9299e+00 best_ppl=6.89                                                
Epoch 213 - |param|=1.05e+03 |g_param|=2.31e+05 loss=5.5843e-01 ppl=1.75                                                
Validation - loss=1.9597e+00 ppl=7.10 best_loss=1.9299e+00 best_ppl=6.89                                                
Epoch 214 - |param|=1.05e+03 |g_param|=3.99e+05 loss=5.2296e-01 ppl=1.69                                                
Validation - loss=2.0113e+00 ppl=7.47 best_loss=1.9299e+00 best_ppl=6.89                                                
Epoch 215 - |param|=1.05e+03 |g_param|=9.46e+04 loss=4.9005e-01 ppl=1.63                                                
Validation - loss=1.9230e+00 ppl=6.84 best_loss=1.9299e+00 best_ppl=6.89                                                
Epoch 216 - |param|=1.05e+03 |g_param|=1.54e+05 loss=5.0090e-01 ppl=1.65                                                
Validation - loss=1.9435e+00 ppl=6.98 best_loss=1.9230e+00 best_ppl=6.84                                                
Epoch 217 - |param|=1.05e+03 |g_param|=1.29e+05 loss=4.8857e-01 ppl=1.63                                                
Validation - loss=1.9118e+00 ppl=6.77 best_loss=1.9230e+00 best_ppl=6.84                                                
Epoch 218 - |param|=1.05e+03 |g_param|=1.83e+05 loss=4.9659e-01 ppl=1.64                                                
Validation - loss=1.9292e+00 ppl=6.88 best_loss=1.9118e+00 best_ppl=6.77                                                
Epoch 219 - |param|=1.05e+03 |g_param|=1.75e+05 loss=4.6291e-01 ppl=1.59                                                
Validation - loss=1.9431e+00 ppl=6.98 best_loss=1.9118e+00 best_ppl=6.77                                                
Epoch 220 - |param|=1.05e+03 |g_param|=2.14e+05 loss=5.1412e-01 ppl=1.67                                                
Validation - loss=1.9287e+00 ppl=6.88 best_loss=1.9118e+00 best_ppl=6.77                                                
Epoch 221 - |param|=1.05e+03 |g_param|=1.68e+05 loss=5.0451e-01 ppl=1.66                                                
Validation - loss=1.9191e+00 ppl=6.81 best_loss=1.9118e+00 best_ppl=6.77                                                
Epoch 222 - |param|=1.05e+03 |g_param|=1.49e+05 loss=4.9109e-01 ppl=1.63                                                
Validation - loss=1.9231e+00 ppl=6.84 best_loss=1.9118e+00 best_ppl=6.77                                                
Epoch 223 - |param|=1.05e+03 |g_param|=2.68e+05 loss=4.7002e-01 ppl=1.60                                                
Validation - loss=1.9209e+00 ppl=6.83 best_loss=1.9118e+00 best_ppl=6.77                                                
Epoch 224 - |param|=1.05e+03 |g_param|=1.06e+05 loss=4.8710e-01 ppl=1.63                                                
Validation - loss=1.9193e+00 ppl=6.82 best_loss=1.9118e+00 best_ppl=6.77                                                
Epoch 225 - |param|=1.05e+03 |g_param|=2.00e+05 loss=4.7732e-01 ppl=1.61                                                
Validation - loss=1.9070e+00 ppl=6.73 best_loss=1.9118e+00 best_ppl=6.77                                                
Epoch 226 - |param|=1.05e+03 |g_param|=3.83e+05 loss=5.0751e-01 ppl=1.66                                                
Validation - loss=1.9590e+00 ppl=7.09 best_loss=1.9070e+00 best_ppl=6.73                                                
Epoch 227 - |param|=1.05e+03 |g_param|=1.92e+05 loss=4.7126e-01 ppl=1.60                                                
Validation - loss=1.9004e+00 ppl=6.69 best_loss=1.9070e+00 best_ppl=6.73                                                
Epoch 228 - |param|=1.05e+03 |g_param|=1.35e+05 loss=4.5109e-01 ppl=1.57                                                
Validation - loss=1.8949e+00 ppl=6.65 best_loss=1.9004e+00 best_ppl=6.69                                                
Epoch 229 - |param|=1.05e+03 |g_param|=1.91e+05 loss=4.9250e-01 ppl=1.64                                                
Validation - loss=1.9270e+00 ppl=6.87 best_loss=1.8949e+00 best_ppl=6.65                                                
Epoch 230 - |param|=1.05e+03 |g_param|=1.17e+05 loss=4.6073e-01 ppl=1.59                                                
Validation - loss=1.9000e+00 ppl=6.69 best_loss=1.8949e+00 best_ppl=6.65                                                
Epoch 231 - |param|=1.05e+03 |g_param|=8.33e+04 loss=4.3370e-01 ppl=1.54                                                
Validation - loss=1.9076e+00 ppl=6.74 best_loss=1.8949e+00 best_ppl=6.65                                                
Epoch 232 - |param|=1.05e+03 |g_param|=1.39e+05 loss=4.7948e-01 ppl=1.62                                                
Validation - loss=1.9122e+00 ppl=6.77 best_loss=1.8949e+00 best_ppl=6.65                                                
Epoch 233 - |param|=1.05e+03 |g_param|=1.89e+05 loss=4.9736e-01 ppl=1.64                                                
Validation - loss=1.8965e+00 ppl=6.66 best_loss=1.8949e+00 best_ppl=6.65                                                
Epoch 234 - |param|=1.05e+03 |g_param|=9.05e+04 loss=4.4816e-01 ppl=1.57                                                
Validation - loss=1.8847e+00 ppl=6.58 best_loss=1.8949e+00 best_ppl=6.65                                                
Epoch 235 - |param|=1.05e+03 |g_param|=8.06e+04 loss=4.4251e-01 ppl=1.56                                                
Validation - loss=1.8962e+00 ppl=6.66 best_loss=1.8847e+00 best_ppl=6.58                                                
Epoch 236 - |param|=1.05e+03 |g_param|=1.88e+05 loss=4.5893e-01 ppl=1.58                                                
Validation - loss=1.8884e+00 ppl=6.61 best_loss=1.8847e+00 best_ppl=6.58                                                
Epoch 237 - |param|=1.05e+03 |g_param|=2.06e+05 loss=4.6646e-01 ppl=1.59                                                
Validation - loss=1.9352e+00 ppl=6.93 best_loss=1.8847e+00 best_ppl=6.58                                                
Epoch 238 - |param|=1.05e+03 |g_param|=1.15e+05 loss=4.6554e-01 ppl=1.59                                                
Validation - loss=1.8887e+00 ppl=6.61 best_loss=1.8847e+00 best_ppl=6.58                                                
Epoch 239 - |param|=1.05e+03 |g_param|=6.74e+04 loss=4.3582e-01 ppl=1.55                                                
Validation - loss=1.8592e+00 ppl=6.42 best_loss=1.8847e+00 best_ppl=6.58                                                
Epoch 240 - |param|=1.05e+03 |g_param|=1.64e+05 loss=4.3987e-01 ppl=1.55                                                
Validation - loss=1.9008e+00 ppl=6.69 best_loss=1.8592e+00 best_ppl=6.42                                                
Epoch 241 - |param|=1.05e+03 |g_param|=6.95e+04 loss=4.4997e-01 ppl=1.57                                                
Validation - loss=1.8688e+00 ppl=6.48 best_loss=1.8592e+00 best_ppl=6.42                                                
Epoch 242 - |param|=1.05e+03 |g_param|=1.75e+05 loss=4.7141e-01 ppl=1.60                                                
Validation - loss=1.9412e+00 ppl=6.97 best_loss=1.8592e+00 best_ppl=6.42                                                
Epoch 243 - |param|=1.05e+03 |g_param|=1.92e+05 loss=4.4772e-01 ppl=1.56                                                
Validation - loss=1.8918e+00 ppl=6.63 best_loss=1.8592e+00 best_ppl=6.42                                                
Epoch 244 - |param|=1.05e+03 |g_param|=1.11e+05 loss=4.3069e-01 ppl=1.54                                                
Validation - loss=1.8566e+00 ppl=6.40 best_loss=1.8592e+00 best_ppl=6.42                                                
Epoch 245 - |param|=1.05e+03 |g_param|=7.75e+04 loss=4.0446e-01 ppl=1.50                                                
Validation - loss=1.8596e+00 ppl=6.42 best_loss=1.8566e+00 best_ppl=6.40                                                
Epoch 246 - |param|=1.05e+03 |g_param|=8.74e+04 loss=4.5042e-01 ppl=1.57                                                
Validation - loss=1.8713e+00 ppl=6.50 best_loss=1.8566e+00 best_ppl=6.40                                                
Epoch 247 - |param|=1.05e+03 |g_param|=1.51e+05 loss=4.0921e-01 ppl=1.51                                                
Validation - loss=1.8631e+00 ppl=6.44 best_loss=1.8566e+00 best_ppl=6.40                                                
Epoch 248 - |param|=1.05e+03 |g_param|=1.62e+05 loss=4.6299e-01 ppl=1.59                                                
Validation - loss=1.9261e+00 ppl=6.86 best_loss=1.8566e+00 best_ppl=6.40                                                
Epoch 249 - |param|=1.05e+03 |g_param|=1.55e+05 loss=4.2690e-01 ppl=1.53                                                
Validation - loss=1.8492e+00 ppl=6.35 best_loss=1.8566e+00 best_ppl=6.40                                                
Epoch 250 - |param|=1.05e+03 |g_param|=6.70e+04 loss=4.2290e-01 ppl=1.53                                                
Validation - loss=1.8473e+00 ppl=6.34 best_loss=1.8492e+00 best_ppl=6.35                                                
Epoch 251 - |param|=1.05e+03 |g_param|=2.24e+05 loss=4.2818e-01 ppl=1.53                                                
Validation - loss=1.8871e+00 ppl=6.60 best_loss=1.8473e+00 best_ppl=6.34                                                
Epoch 252 - |param|=1.05e+03 |g_param|=1.11e+05 loss=4.2010e-01 ppl=1.52                                                
Validation - loss=1.8705e+00 ppl=6.49 best_loss=1.8473e+00 best_ppl=6.34                                                
Epoch 253 - |param|=1.05e+03 |g_param|=1.78e+05 loss=4.3366e-01 ppl=1.54                                                
Validation - loss=1.8702e+00 ppl=6.49 best_loss=1.8473e+00 best_ppl=6.34                                                
Epoch 254 - |param|=1.05e+03 |g_param|=4.81e+04 loss=4.3604e-01 ppl=1.55                                                
Validation - loss=1.8510e+00 ppl=6.37 best_loss=1.8473e+00 best_ppl=6.34                                                
Epoch 255 - |param|=1.05e+03 |g_param|=9.01e+04 loss=3.9600e-01 ppl=1.49                                                
Validation - loss=1.8223e+00 ppl=6.19 best_loss=1.8473e+00 best_ppl=6.34                                                
Epoch 256 - |param|=1.05e+03 |g_param|=1.05e+05 loss=3.9288e-01 ppl=1.48                                                
Validation - loss=1.8715e+00 ppl=6.50 best_loss=1.8223e+00 best_ppl=6.19                                                
Epoch 257 - |param|=1.05e+03 |g_param|=9.45e+04 loss=4.0383e-01 ppl=1.50                                                
Validation - loss=1.8589e+00 ppl=6.42 best_loss=1.8223e+00 best_ppl=6.19                                                
Epoch 258 - |param|=1.05e+03 |g_param|=2.04e+05 loss=4.3255e-01 ppl=1.54                                                
Validation - loss=1.8770e+00 ppl=6.53 best_loss=1.8223e+00 best_ppl=6.19                                                
Epoch 259 - |param|=1.05e+03 |g_param|=1.11e+05 loss=3.7317e-01 ppl=1.45                                                
Validation - loss=1.8166e+00 ppl=6.15 best_loss=1.8223e+00 best_ppl=6.19                                                
Epoch 260 - |param|=1.05e+03 |g_param|=8.45e+04 loss=3.8309e-01 ppl=1.47                                                
Validation - loss=1.8201e+00 ppl=6.17 best_loss=1.8166e+00 best_ppl=6.15                                                
Epoch 261 - |param|=1.05e+03 |g_param|=8.31e+04 loss=3.9840e-01 ppl=1.49                                                
Validation - loss=1.8272e+00 ppl=6.22 best_loss=1.8166e+00 best_ppl=6.15                                                
Epoch 262 - |param|=1.05e+03 |g_param|=1.60e+05 loss=4.2026e-01 ppl=1.52                                                
Validation - loss=1.8410e+00 ppl=6.30 best_loss=1.8166e+00 best_ppl=6.15                                                
Epoch 263 - |param|=1.05e+03 |g_param|=6.94e+04 loss=3.9777e-01 ppl=1.49                                                
Validation - loss=1.8171e+00 ppl=6.15 best_loss=1.8166e+00 best_ppl=6.15                                                
Epoch 264 - |param|=1.05e+03 |g_param|=8.62e+04 loss=3.8151e-01 ppl=1.46                                                
Validation - loss=1.8336e+00 ppl=6.26 best_loss=1.8166e+00 best_ppl=6.15                                                
Epoch 265 - |param|=1.05e+03 |g_param|=1.36e+05 loss=4.1345e-01 ppl=1.51                                                
Validation - loss=1.8528e+00 ppl=6.38 best_loss=1.8166e+00 best_ppl=6.15                                                
Epoch 266 - |param|=1.05e+03 |g_param|=9.36e+04 loss=3.8835e-01 ppl=1.47                                                
Validation - loss=1.8013e+00 ppl=6.06 best_loss=1.8166e+00 best_ppl=6.15                                                
Epoch 267 - |param|=1.05e+03 |g_param|=7.54e+04 loss=3.8022e-01 ppl=1.46                                                
Validation - loss=1.8473e+00 ppl=6.34 best_loss=1.8013e+00 best_ppl=6.06                                                
Epoch 268 - |param|=1.05e+03 |g_param|=6.79e+04 loss=3.7725e-01 ppl=1.46                                                
Validation - loss=1.8484e+00 ppl=6.35 best_loss=1.8013e+00 best_ppl=6.06                                                
Epoch 269 - |param|=1.05e+03 |g_param|=8.58e+04 loss=4.2521e-01 ppl=1.53                                                
Validation - loss=1.8192e+00 ppl=6.17 best_loss=1.8013e+00 best_ppl=6.06                                                
Epoch 270 - |param|=1.05e+03 |g_param|=2.75e+05 loss=4.5237e-01 ppl=1.57                                                
Validation - loss=1.8954e+00 ppl=6.66 best_loss=1.8013e+00 best_ppl=6.06                                                
Epoch 271 - |param|=1.05e+03 |g_param|=1.50e+05 loss=4.1349e-01 ppl=1.51                                                
Validation - loss=1.8430e+00 ppl=6.32 best_loss=1.8013e+00 best_ppl=6.06                                                
Epoch 272 - |param|=1.05e+03 |g_param|=9.21e+04 loss=3.8442e-01 ppl=1.47                                                
Validation - loss=1.8262e+00 ppl=6.21 best_loss=1.8013e+00 best_ppl=6.06                                                
Epoch 273 - |param|=1.05e+03 |g_param|=7.30e+04 loss=3.5082e-01 ppl=1.42                                                
Validation - loss=1.8284e+00 ppl=6.22 best_loss=1.8013e+00 best_ppl=6.06                                                
Epoch 274 - |param|=1.05e+03 |g_param|=8.62e+04 loss=4.0169e-01 ppl=1.49                                                
Validation - loss=1.7877e+00 ppl=5.98 best_loss=1.8013e+00 best_ppl=6.06                                                
Epoch 275 - |param|=1.05e+03 |g_param|=7.69e+04 loss=3.6336e-01 ppl=1.44                                                
Validation - loss=1.8000e+00 ppl=6.05 best_loss=1.7877e+00 best_ppl=5.98                                                
Epoch 276 - |param|=1.05e+03 |g_param|=8.25e+04 loss=3.8663e-01 ppl=1.47                                                
Validation - loss=1.8002e+00 ppl=6.05 best_loss=1.7877e+00 best_ppl=5.98                                                
Epoch 277 - |param|=1.05e+03 |g_param|=9.20e+04 loss=3.7187e-01 ppl=1.45                                                
Validation - loss=1.7952e+00 ppl=6.02 best_loss=1.7877e+00 best_ppl=5.98                                                
Epoch 278 - |param|=1.05e+03 |g_param|=1.14e+05 loss=3.9455e-01 ppl=1.48                                                
Validation - loss=1.8117e+00 ppl=6.12 best_loss=1.7877e+00 best_ppl=5.98                                                
Epoch 279 - |param|=1.05e+03 |g_param|=6.20e+04 loss=3.8683e-01 ppl=1.47                                                
Validation - loss=1.7873e+00 ppl=5.97 best_loss=1.7877e+00 best_ppl=5.98                                                
Epoch 280 - |param|=1.05e+03 |g_param|=1.16e+05 loss=3.5710e-01 ppl=1.43                                                
Validation - loss=1.8320e+00 ppl=6.25 best_loss=1.7873e+00 best_ppl=5.97                                                
Epoch 281 - |param|=1.05e+03 |g_param|=2.28e+05 loss=3.7993e-01 ppl=1.46                                                
Validation - loss=1.8724e+00 ppl=6.50 best_loss=1.7873e+00 best_ppl=5.97                                                
Epoch 282 - |param|=1.05e+03 |g_param|=5.40e+04 loss=3.5073e-01 ppl=1.42                                                
Validation - loss=1.7911e+00 ppl=6.00 best_loss=1.7873e+00 best_ppl=5.97                                                
Epoch 283 - |param|=1.05e+03 |g_param|=8.37e+04 loss=3.6091e-01 ppl=1.43                                                
Validation - loss=1.7912e+00 ppl=6.00 best_loss=1.7873e+00 best_ppl=5.97                                                
Epoch 284 - |param|=1.05e+03 |g_param|=4.56e+05 loss=4.9830e-01 ppl=1.65                                                
Validation - loss=1.8426e+00 ppl=6.31 best_loss=1.7873e+00 best_ppl=5.97                                                
Epoch 285 - |param|=1.05e+03 |g_param|=6.73e+04 loss=3.4555e-01 ppl=1.41                                                
Validation - loss=1.8103e+00 ppl=6.11 best_loss=1.7873e+00 best_ppl=5.97                                                
Epoch 286 - |param|=1.05e+03 |g_param|=4.86e+04 loss=3.6355e-01 ppl=1.44                                                
Validation - loss=1.7786e+00 ppl=5.92 best_loss=1.7873e+00 best_ppl=5.97                                                
Epoch 287 - |param|=1.05e+03 |g_param|=1.83e+05 loss=3.8528e-01 ppl=1.47                                                
Validation - loss=1.7948e+00 ppl=6.02 best_loss=1.7786e+00 best_ppl=5.92                                                
Epoch 288 - |param|=1.05e+03 |g_param|=1.35e+05 loss=3.5334e-01 ppl=1.42                                                
Validation - loss=1.7783e+00 ppl=5.92 best_loss=1.7786e+00 best_ppl=5.92                                                
Epoch 289 - |param|=1.05e+03 |g_param|=6.39e+04 loss=3.5623e-01 ppl=1.43                                                
Validation - loss=1.7927e+00 ppl=6.01 best_loss=1.7783e+00 best_ppl=5.92                                                
Epoch 290 - |param|=1.05e+03 |g_param|=2.62e+05 loss=4.0612e-01 ppl=1.50                                                
Validation - loss=1.8421e+00 ppl=6.31 best_loss=1.7783e+00 best_ppl=5.92                                                
Epoch 291 - |param|=1.05e+03 |g_param|=1.06e+05 loss=3.6953e-01 ppl=1.45                                                
Validation - loss=1.7865e+00 ppl=5.97 best_loss=1.7783e+00 best_ppl=5.92                                                
Epoch 292 - |param|=1.05e+03 |g_param|=1.30e+05 loss=3.4407e-01 ppl=1.41                                                
Validation - loss=1.7479e+00 ppl=5.74 best_loss=1.7783e+00 best_ppl=5.92                                                
Epoch 293 - |param|=1.05e+03 |g_param|=7.50e+04 loss=3.3709e-01 ppl=1.40                                                
Validation - loss=1.7684e+00 ppl=5.86 best_loss=1.7479e+00 best_ppl=5.74                                                
Epoch 294 - |param|=1.05e+03 |g_param|=4.49e+04 loss=3.2986e-01 ppl=1.39                                                
Validation - loss=1.7625e+00 ppl=5.83 best_loss=1.7479e+00 best_ppl=5.74                                                
Epoch 295 - |param|=1.05e+03 |g_param|=1.21e+05 loss=3.4872e-01 ppl=1.42                                                
Validation - loss=1.8214e+00 ppl=6.18 best_loss=1.7479e+00 best_ppl=5.74                                                
Epoch 296 - |param|=1.05e+03 |g_param|=1.90e+05 loss=3.7798e-01 ppl=1.46                                                
Validation - loss=1.7910e+00 ppl=6.00 best_loss=1.7479e+00 best_ppl=5.74                                                
Epoch 297 - |param|=1.05e+03 |g_param|=8.94e+04 loss=3.2439e-01 ppl=1.38                                                
Validation - loss=1.7936e+00 ppl=6.01 best_loss=1.7479e+00 best_ppl=5.74                                                
Epoch 298 - |param|=1.05e+03 |g_param|=5.78e+04 loss=3.4346e-01 ppl=1.41                                                
Validation - loss=1.7766e+00 ppl=5.91 best_loss=1.7479e+00 best_ppl=5.74                                                
Epoch 299 - |param|=1.05e+03 |g_param|=3.59e+05 loss=4.6652e-01 ppl=1.59                                                
Validation - loss=1.8426e+00 ppl=6.31 best_loss=1.7479e+00 best_ppl=5.74                                                
Epoch 300 - |param|=1.05e+03 |g_param|=7.47e+04 loss=3.4901e-01 ppl=1.42                                                
Validation - loss=1.7640e+00 ppl=5.84 best_loss=1.7479e+00 best_ppl=5.74                                                

real	211m32.856s
user	208m17.233s
sys	3m8.135s

real	421m7.217s
user	414m31.043s
sys	6m23.556s
(simple-nmt) ye@:~/exp/simple-nmt$
```

## Testing Transformer Model
### bash script for testing (my-br)  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, Thailand
# Last updated: 10 April 2022
# find all models and parse to translate.py for testing and multi-bleu.perl for evaluation with BLEU score
# updated for Transformer model my-br

cd ./model/braille/transformer/my-br/;

for i in `ls *.pth | sort -V`; do
   MODEL=$i;

   # Testing
   python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 1 --lang mybr < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my > $MODEL.hyp

   # Evaluation with BLEU Score
   echo "Evaluation result for the model: $MODEL" | tee -a eval-results-mybr-transformer-300epoch.txt;
   cat $MODEL.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee  -a eval-results-mybr-transformer-300epoch.txt;

done

cd -;

```

testing my-br ...  
**`ls *.pth | sort -V`;** ကို အထက်က **test-eval-loop-transformer-mybr.sh** script မှာ ထည့်ဖို့ မေ့သွားလို့ အောက်မှာ မြင်ရတဲ့ evaluation score တွေက အစီအစဉ်တကျတော့ မရှိဘူး...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-loop-transformer-mybr.sh | tee ./test-eval-loop-transformer-mybr.log
Evaluation result for the model: transformer-model-mybr.01.7.56-1923.23.7.70-2205.84.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
BLEU = 0.00, 41.6/5.9/0.0/0.0 (BP=0.035, ratio=0.230, hyp_len=6627, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.02.6.48-651.14.6.65-776.03.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
BLEU = 0.00, 36.2/7.7/0.0/0.0 (BP=0.075, ratio=0.278, hyp_len=8008, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.03.5.81-332.52.6.07-431.72.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
BLEU = 0.00, 53.9/15.1/0.0/0.0 (BP=0.018, ratio=0.200, hyp_len=5766, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.04.5.50-244.61.5.83-340.51.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
BLEU = 0.00, 38.9/6.1/0.0/0.0 (BP=0.142, ratio=0.339, hyp_len=9754, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.05.5.32-203.41.5.67-291.31.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
BLEU = 0.00, 16.3/2.5/0.0/0.0 (BP=0.867, ratio=0.875, hyp_len=25210, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.06.5.18-178.11.5.56-258.55.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
BLEU = 0.00, 13.9/2.3/0.0/0.0 (BP=1.000, ratio=1.112, hyp_len=32031, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.07.5.06-158.28.5.43-228.42.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
BLEU = 0.00, 12.7/2.1/0.1/0.0 (BP=1.000, ratio=1.323, hyp_len=38102, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.08.4.86-128.70.5.31-201.85.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 2167.
BLEU = 0.00, 16.0/2.9/0.2/0.0 (BP=1.000, ratio=1.215, hyp_len=35008, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.09.4.84-126.77.5.20-181.59.pth
BLEU = 0.90, 19.9/3.9/0.4/0.0 (BP=1.000, ratio=1.096, hyp_len=31571, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.100.1.34-3.82.2.36-10.56.pth
BLEU = 42.09, 70.3/49.4/35.4/25.5 (BP=1.000, ratio=1.013, hyp_len=29174, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.101.1.31-3.72.2.39-10.96.pth
BLEU = 41.39, 70.2/49.3/34.6/24.5 (BP=1.000, ratio=1.018, hyp_len=29312, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.102.1.35-3.86.2.34-10.37.pth
BLEU = 42.76, 70.5/50.1/36.1/26.2 (BP=1.000, ratio=1.021, hyp_len=29414, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.103.1.33-3.79.2.31-10.11.pth
BLEU = 43.31, 70.7/50.5/36.6/26.9 (BP=1.000, ratio=1.017, hyp_len=29283, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.104.1.26-3.52.2.31-10.04.pth
BLEU = 44.55, 72.4/51.8/37.8/27.8 (BP=1.000, ratio=1.000, hyp_len=28809, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.10.4.66-105.83.5.10-164.60.pth
BLEU = 1.63, 22.0/4.5/0.8/0.1 (BP=1.000, ratio=1.132, hyp_len=32598, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.105.1.30-3.68.2.31-10.04.pth
BLEU = 43.30, 70.6/50.5/36.7/26.9 (BP=1.000, ratio=1.027, hyp_len=29578, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.106.1.23-3.43.2.28-9.74.pth
BLEU = 44.79, 71.9/52.0/38.1/28.2 (BP=1.000, ratio=1.011, hyp_len=29120, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.107.1.23-3.41.2.30-9.95.pth
BLEU = 45.60, 74.0/53.7/39.6/29.6 (BP=0.981, ratio=0.981, hyp_len=28270, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.108.1.26-3.51.2.27-9.69.pth
BLEU = 46.00, 72.9/53.1/39.3/29.4 (BP=1.000, ratio=1.003, hyp_len=28881, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.109.1.21-3.37.2.28-9.74.pth
BLEU = 43.27, 70.0/50.5/36.7/27.0 (BP=1.000, ratio=1.052, hyp_len=30291, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.110.1.27-3.57.2.26-9.57.pth
BLEU = 46.76, 73.5/53.8/40.1/30.1 (BP=1.000, ratio=1.002, hyp_len=28850, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.111.1.15-3.15.2.25-9.47.pth
BLEU = 46.96, 73.5/54.0/40.3/30.4 (BP=1.000, ratio=1.005, hyp_len=28941, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.112.1.23-3.42.2.23-9.32.pth
BLEU = 46.33, 72.6/53.5/39.7/29.8 (BP=1.000, ratio=1.020, hyp_len=29372, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.113.1.13-3.09.2.23-9.31.pth
BLEU = 48.14, 75.0/55.6/42.1/32.2 (BP=0.987, ratio=0.987, hyp_len=28442, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.114.1.17-3.21.2.24-9.39.pth
BLEU = 47.31, 73.7/54.5/40.7/30.7 (BP=1.000, ratio=1.012, hyp_len=29156, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.11.4.61-100.68.5.02-151.16.pth
BLEU = 2.14, 24.5/5.4/1.2/0.1 (BP=1.000, ratio=1.118, hyp_len=32190, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.115.1.21-3.35.2.24-9.39.pth
BLEU = 46.39, 72.6/53.7/39.9/29.8 (BP=1.000, ratio=1.027, hyp_len=29589, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.116.1.16-3.20.2.22-9.18.pth
BLEU = 47.83, 73.3/54.5/41.3/31.7 (BP=1.000, ratio=1.022, hyp_len=29432, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.117.1.13-3.11.2.21-9.07.pth
BLEU = 48.55, 74.0/55.3/42.0/32.3 (BP=1.000, ratio=1.010, hyp_len=29078, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.118.1.13-3.09.2.24-9.38.pth
BLEU = 49.21, 76.3/57.1/43.5/33.7 (BP=0.979, ratio=0.979, hyp_len=28197, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.119.1.06-2.87.2.19-8.90.pth
BLEU = 49.95, 75.2/56.6/43.4/33.6 (BP=1.000, ratio=1.003, hyp_len=28887, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.120.1.11-3.03.2.18-8.88.pth
BLEU = 49.88, 75.2/56.6/43.3/33.6 (BP=1.000, ratio=1.003, hyp_len=28899, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.121.1.07-2.91.2.17-8.72.pth
BLEU = 49.53, 74.3/56.2/43.1/33.5 (BP=1.000, ratio=1.020, hyp_len=29392, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.122.1.04-2.83.2.19-8.92.pth
BLEU = 48.93, 74.4/56.0/42.4/32.4 (BP=1.000, ratio=1.020, hyp_len=29375, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.123.1.00-2.73.2.15-8.60.pth
BLEU = 50.32, 75.0/57.0/43.9/34.2 (BP=1.000, ratio=1.020, hyp_len=29380, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.124.1.05-2.86.2.14-8.53.pth
BLEU = 50.73, 75.4/57.3/44.3/34.6 (BP=1.000, ratio=1.011, hyp_len=29117, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.12.4.55-94.55.4.95-140.78.pth
BLEU = 2.90, 31.6/7.7/1.9/0.2 (BP=0.890, ratio=0.896, hyp_len=25797, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.125.1.03-2.80.2.16-8.69.pth
BLEU = 51.81, 77.0/58.9/46.0/36.4 (BP=0.987, ratio=0.987, hyp_len=28421, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.126.1.02-2.76.2.14-8.54.pth
BLEU = 51.23, 76.0/58.1/44.7/34.9 (BP=1.000, ratio=1.008, hyp_len=29022, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.127.1.07-2.92.2.13-8.40.pth
BLEU = 50.81, 74.9/57.2/44.5/35.0 (BP=1.000, ratio=1.022, hyp_len=29433, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.128.0.94-2.56.2.12-8.34.pth
BLEU = 52.26, 76.5/58.9/45.8/36.1 (BP=1.000, ratio=1.005, hyp_len=28961, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.129.0.98-2.66.2.14-8.46.pth
BLEU = 49.79, 73.8/56.4/43.5/33.9 (BP=1.000, ratio=1.046, hyp_len=30141, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.130.1.04-2.82.2.17-8.80.pth
BLEU = 52.28, 77.5/59.6/46.6/36.8 (BP=0.986, ratio=0.986, hyp_len=28392, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.131.0.99-2.69.2.14-8.50.pth
BLEU = 50.74, 74.6/57.2/44.4/35.0 (BP=1.000, ratio=1.036, hyp_len=29831, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.132.0.90-2.46.2.11-8.23.pth
BLEU = 51.23, 74.7/57.6/45.1/35.5 (BP=1.000, ratio=1.040, hyp_len=29945, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.133.0.93-2.54.2.10-8.20.pth
BLEU = 53.52, 77.4/60.0/47.2/37.4 (BP=1.000, ratio=1.001, hyp_len=28833, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.134.0.99-2.68.2.11-8.22.pth
BLEU = 52.66, 76.4/59.1/46.4/36.7 (BP=1.000, ratio=1.015, hyp_len=29233, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.13.4.44-84.57.4.87-130.45.pth
BLEU = 3.07, 30.4/7.6/2.0/0.2 (BP=0.976, ratio=0.976, hyp_len=28116, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.135.0.93-2.54.2.10-8.13.pth
BLEU = 52.68, 76.6/59.4/46.3/36.5 (BP=1.000, ratio=1.013, hyp_len=29167, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.136.0.94-2.55.2.11-8.24.pth
BLEU = 52.04, 75.8/58.7/45.7/36.0 (BP=1.000, ratio=1.027, hyp_len=29574, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.137.0.91-2.47.2.10-8.20.pth
BLEU = 54.75, 77.9/60.9/48.5/39.2 (BP=0.999, ratio=0.999, hyp_len=28779, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.138.0.89-2.44.2.10-8.13.pth
BLEU = 54.29, 77.5/60.6/48.0/38.5 (BP=1.000, ratio=1.008, hyp_len=29022, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.139.0.86-2.36.2.10-8.18.pth
BLEU = 54.68, 78.0/61.0/48.5/38.7 (BP=1.000, ratio=1.003, hyp_len=28889, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.140.0.88-2.40.2.15-8.55.pth
BLEU = 50.92, 75.2/58.1/44.5/34.6 (BP=1.000, ratio=1.041, hyp_len=29988, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.141.0.88-2.41.2.09-8.07.pth
BLEU = 55.58, 78.5/61.8/49.5/40.2 (BP=0.997, ratio=0.997, hyp_len=28728, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.142.0.90-2.45.2.08-7.99.pth
BLEU = 54.18, 76.8/60.3/48.1/38.7 (BP=1.000, ratio=1.022, hyp_len=29446, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.143.0.87-2.38.2.12-8.37.pth
BLEU = 52.48, 76.3/59.4/46.2/36.2 (BP=1.000, ratio=1.029, hyp_len=29628, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.144.0.87-2.39.2.06-7.88.pth
BLEU = 55.44, 78.1/61.5/49.3/39.9 (BP=1.000, ratio=1.009, hyp_len=29055, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.14.4.37-79.23.4.81-123.17.pth
BLEU = 3.39, 30.8/7.8/2.1/0.3 (BP=0.996, ratio=0.996, hyp_len=28676, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.145.0.85-2.34.2.07-7.96.pth
BLEU = 56.14, 78.5/62.1/50.1/40.7 (BP=1.000, ratio=1.005, hyp_len=28944, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.146.0.86-2.37.2.07-7.91.pth
BLEU = 56.35, 78.6/62.2/50.2/41.0 (BP=1.000, ratio=1.004, hyp_len=28908, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.147.0.79-2.20.2.04-7.70.pth
BLEU = 55.18, 77.5/61.3/49.1/39.8 (BP=1.000, ratio=1.024, hyp_len=29486, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.148.0.81-2.25.2.05-7.80.pth
BLEU = 55.44, 77.3/61.3/49.4/40.3 (BP=1.000, ratio=1.024, hyp_len=29508, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.149.0.80-2.22.2.04-7.72.pth
BLEU = 55.62, 77.6/61.6/49.6/40.4 (BP=1.000, ratio=1.025, hyp_len=29531, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.150.0.74-2.10.2.07-7.92.pth
BLEU = 53.81, 76.0/59.9/47.8/38.5 (BP=1.000, ratio=1.047, hyp_len=30164, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.151.0.81-2.24.2.09-8.09.pth
BLEU = 53.16, 76.3/60.0/47.0/37.1 (BP=1.000, ratio=1.042, hyp_len=30019, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.152.0.81-2.25.2.05-7.75.pth
BLEU = 55.21, 77.3/61.3/49.2/39.9 (BP=1.000, ratio=1.033, hyp_len=29742, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.153.0.78-2.19.2.03-7.63.pth
BLEU = 55.93, 77.9/62.0/49.9/40.6 (BP=1.000, ratio=1.025, hyp_len=29510, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.154.0.77-2.16.2.03-7.60.pth
BLEU = 57.67, 79.3/63.4/51.7/42.6 (BP=1.000, ratio=1.008, hyp_len=29037, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.15.4.28-72.21.4.76-117.04.pth
BLEU = 3.88, 34.2/9.1/2.6/0.4 (BP=0.905, ratio=0.910, hyp_len=26200, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.155.0.79-2.20.2.07-7.95.pth
BLEU = 56.82, 79.6/63.5/50.7/40.9 (BP=0.999, ratio=0.999, hyp_len=28772, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.156.0.77-2.16.2.08-8.00.pth
BLEU = 55.84, 78.6/62.4/49.6/39.9 (BP=1.000, ratio=1.011, hyp_len=29129, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.157.0.76-2.15.2.02-7.54.pth
BLEU = 58.29, 79.7/64.1/52.4/43.2 (BP=1.000, ratio=1.008, hyp_len=29047, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.158.0.76-2.15.2.03-7.59.pth
BLEU = 58.73, 80.1/64.5/52.8/43.7 (BP=0.999, ratio=0.999, hyp_len=28780, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.159.0.77-2.17.2.00-7.39.pth
BLEU = 58.63, 79.8/64.3/52.7/43.7 (BP=1.000, ratio=1.010, hyp_len=29095, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.160.0.76-2.15.2.01-7.48.pth
BLEU = 57.54, 78.7/63.1/51.6/42.7 (BP=1.000, ratio=1.024, hyp_len=29490, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.161.0.75-2.12.1.99-7.34.pth
BLEU = 58.36, 79.5/64.1/52.4/43.4 (BP=1.000, ratio=1.012, hyp_len=29153, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.162.0.74-2.10.2.04-7.70.pth
BLEU = 58.96, 80.5/64.8/53.0/43.9 (BP=0.999, ratio=0.999, hyp_len=28766, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.163.0.74-2.10.2.00-7.36.pth
BLEU = 58.03, 79.1/63.7/52.1/43.2 (BP=1.000, ratio=1.022, hyp_len=29429, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.164.0.72-2.06.2.01-7.49.pth
BLEU = 57.06, 78.3/62.9/51.1/42.1 (BP=1.000, ratio=1.032, hyp_len=29737, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.16.4.18-65.22.4.71-111.11.pth
BLEU = 3.95, 36.1/9.6/2.8/0.4 (BP=0.880, ratio=0.886, hyp_len=25526, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.165.0.67-1.95.2.00-7.35.pth
BLEU = 59.13, 79.9/64.7/53.3/44.4 (BP=1.000, ratio=1.011, hyp_len=29123, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.166.0.73-2.08.1.97-7.18.pth
BLEU = 59.42, 79.9/64.9/53.6/44.8 (BP=1.000, ratio=1.014, hyp_len=29206, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.167.0.70-2.01.2.01-7.46.pth
BLEU = 58.07, 79.0/63.8/52.2/43.2 (BP=1.000, ratio=1.026, hyp_len=29564, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.168.0.68-1.98.2.01-7.50.pth
BLEU = 57.37, 78.6/63.4/51.4/42.3 (BP=1.000, ratio=1.031, hyp_len=29697, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.169.0.70-2.02.1.99-7.29.pth
BLEU = 60.41, 80.7/65.8/54.7/45.9 (BP=1.000, ratio=1.006, hyp_len=28965, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.170.0.64-1.90.1.98-7.23.pth
BLEU = 58.87, 79.3/64.4/53.1/44.3 (BP=1.000, ratio=1.026, hyp_len=29539, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.171.0.69-2.00.1.97-7.16.pth
BLEU = 60.22, 80.5/65.7/54.4/45.7 (BP=1.000, ratio=1.014, hyp_len=29192, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.172.0.69-1.99.1.97-7.19.pth
BLEU = 59.17, 79.2/64.5/53.5/44.9 (BP=1.000, ratio=1.031, hyp_len=29694, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.173.0.66-1.94.1.95-7.04.pth
BLEU = 59.77, 79.9/65.2/54.1/45.4 (BP=1.000, ratio=1.023, hyp_len=29476, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.17.4.06-58.20.4.66-105.20.pth
BLEU = 4.37, 34.6/9.6/2.9/0.5 (BP=0.944, ratio=0.946, hyp_len=27240, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.174.0.72-2.05.2.10-8.17.pth
BLEU = 53.62, 76.1/60.6/47.6/37.7 (BP=1.000, ratio=1.065, hyp_len=30688, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.175.0.69-1.98.1.96-7.12.pth
BLEU = 60.51, 80.7/66.0/54.8/46.0 (BP=1.000, ratio=1.012, hyp_len=29142, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.176.0.65-1.93.1.93-6.88.pth
BLEU = 61.26, 81.4/66.6/55.6/46.8 (BP=1.000, ratio=1.002, hyp_len=28873, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.177.0.63-1.88.1.95-7.00.pth
BLEU = 61.09, 81.0/66.4/55.4/46.7 (BP=1.000, ratio=1.009, hyp_len=29073, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.178.0.70-2.02.1.96-7.13.pth
BLEU = 60.71, 81.0/66.2/55.0/46.1 (BP=1.000, ratio=1.010, hyp_len=29086, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.179.0.67-1.95.1.95-6.99.pth
BLEU = 60.24, 80.4/65.7/54.5/45.7 (BP=1.000, ratio=1.020, hyp_len=29373, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.180.0.67-1.96.1.97-7.19.pth
BLEU = 61.35, 81.4/66.7/55.7/46.9 (BP=1.000, ratio=1.004, hyp_len=28922, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.181.0.66-1.93.1.95-7.02.pth
BLEU = 60.56, 80.6/66.0/54.9/46.1 (BP=1.000, ratio=1.017, hyp_len=29304, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.182.0.63-1.88.1.94-6.98.pth
BLEU = 60.34, 79.9/65.6/54.8/46.1 (BP=1.000, ratio=1.029, hyp_len=29643, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.183.0.64-1.89.1.95-7.06.pth
BLEU = 61.20, 80.8/66.4/55.6/47.0 (BP=1.000, ratio=1.013, hyp_len=29186, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.184.0.58-1.78.1.97-7.20.pth
BLEU = 59.34, 79.5/65.0/53.7/44.7 (BP=1.000, ratio=1.035, hyp_len=29798, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.18.4.10-60.11.4.61-100.51.pth
BLEU = 4.54, 35.3/9.9/2.9/0.5 (BP=0.947, ratio=0.949, hyp_len=27326, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.185.0.58-1.79.1.94-6.97.pth
BLEU = 60.38, 80.1/65.8/54.8/46.0 (BP=1.000, ratio=1.026, hyp_len=29561, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.186.0.61-1.84.1.93-6.92.pth
BLEU = 61.45, 81.2/66.9/55.8/47.1 (BP=1.000, ratio=1.014, hyp_len=29204, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.187.0.62-1.87.1.94-6.95.pth
BLEU = 61.61, 81.4/67.1/55.9/47.2 (BP=1.000, ratio=1.012, hyp_len=29152, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.188.0.57-1.77.1.93-6.90.pth
BLEU = 59.85, 79.7/65.5/54.2/45.3 (BP=1.000, ratio=1.036, hyp_len=29841, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.189.0.55-1.74.1.93-6.87.pth
BLEU = 62.41, 81.9/67.7/56.8/48.2 (BP=1.000, ratio=1.006, hyp_len=28989, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.190.0.61-1.85.1.92-6.83.pth
BLEU = 63.05, 82.4/68.3/57.5/48.9 (BP=1.000, ratio=1.002, hyp_len=28869, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.191.0.56-1.75.1.92-6.82.pth
BLEU = 61.19, 80.7/66.6/55.6/46.9 (BP=1.000, ratio=1.025, hyp_len=29516, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.192.0.58-1.78.1.94-6.94.pth
BLEU = 62.04, 81.3/67.2/56.5/48.0 (BP=1.000, ratio=1.016, hyp_len=29259, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.193.0.63-1.88.1.99-7.33.pth
BLEU = 59.45, 79.5/65.4/53.8/44.7 (BP=1.000, ratio=1.040, hyp_len=29957, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.19.3.95-52.18.4.56-95.66.pth
BLEU = 4.57, 36.6/10.3/3.1/0.5 (BP=0.925, ratio=0.927, hyp_len=26707, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.194.0.60-1.82.1.92-6.85.pth
BLEU = 62.70, 81.8/67.9/57.2/48.7 (BP=1.000, ratio=1.009, hyp_len=29074, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.195.0.56-1.74.1.92-6.81.pth
BLEU = 62.19, 81.5/67.5/56.6/48.1 (BP=1.000, ratio=1.018, hyp_len=29308, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.196.0.60-1.81.1.91-6.73.pth
BLEU = 63.12, 82.1/68.3/57.7/49.1 (BP=1.000, ratio=1.010, hyp_len=29101, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.197.0.57-1.77.1.93-6.88.pth
BLEU = 63.43, 82.5/68.6/57.9/49.4 (BP=1.000, ratio=1.003, hyp_len=28876, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.198.0.57-1.77.1.91-6.72.pth
BLEU = 62.36, 81.4/67.5/56.9/48.4 (BP=1.000, ratio=1.022, hyp_len=29437, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.199.0.55-1.74.1.92-6.82.pth
BLEU = 62.94, 82.0/68.2/57.4/48.9 (BP=1.000, ratio=1.010, hyp_len=29095, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.200.0.63-1.87.1.93-6.88.pth
BLEU = 63.06, 82.6/68.5/57.6/48.8 (BP=0.999, ratio=0.999, hyp_len=28765, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.201.0.54-1.71.1.89-6.65.pth
BLEU = 63.23, 82.1/68.3/57.8/49.4 (BP=1.000, ratio=1.015, hyp_len=29239, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.202.0.55-1.74.1.89-6.62.pth
BLEU = 62.63, 81.7/67.9/57.1/48.6 (BP=1.000, ratio=1.020, hyp_len=29370, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.203.0.56-1.75.1.91-6.75.pth
BLEU = 63.24, 82.2/68.5/57.8/49.2 (BP=1.000, ratio=1.006, hyp_len=28986, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.20.3.90-49.38.4.53-92.35.pth
BLEU = 4.97, 35.5/10.2/3.1/0.6 (BP=0.982, ratio=0.982, hyp_len=28280, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.204.0.58-1.78.1.92-6.84.pth
BLEU = 61.23, 80.8/66.8/55.6/46.9 (BP=1.000, ratio=1.029, hyp_len=29648, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.205.0.56-1.74.1.91-6.75.pth
BLEU = 63.46, 82.3/68.6/58.0/49.5 (BP=1.000, ratio=1.011, hyp_len=29120, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.206.0.52-1.68.1.86-6.43.pth
BLEU = 63.74, 82.3/68.8/58.4/49.9 (BP=1.000, ratio=1.013, hyp_len=29186, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.207.0.53-1.70.1.88-6.53.pth
BLEU = 64.44, 83.1/69.5/59.0/50.6 (BP=1.000, ratio=1.004, hyp_len=28922, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.208.0.61-1.85.1.97-7.21.pth
BLEU = 60.04, 80.5/66.3/54.3/44.9 (BP=1.000, ratio=1.033, hyp_len=29747, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.209.0.51-1.67.1.86-6.40.pth
BLEU = 63.94, 82.4/69.0/58.6/50.2 (BP=1.000, ratio=1.015, hyp_len=29246, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.210.0.55-1.73.1.88-6.58.pth
BLEU = 62.59, 81.6/68.0/57.1/48.5 (BP=1.000, ratio=1.024, hyp_len=29505, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.211.0.56-1.75.1.86-6.42.pth
BLEU = 64.06, 82.6/69.2/58.6/50.3 (BP=1.000, ratio=1.014, hyp_len=29216, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.212.0.58-1.78.1.99-7.32.pth
BLEU = 59.42, 80.2/66.0/53.6/43.9 (BP=1.000, ratio=1.032, hyp_len=29737, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.213.0.50-1.65.1.89-6.65.pth
BLEU = 64.41, 82.8/69.4/59.1/50.8 (BP=1.000, ratio=1.010, hyp_len=29097, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.21.3.91-50.12.4.49-89.37.pth
BLEU = 5.04, 38.6/11.5/3.5/0.6 (BP=0.911, ratio=0.915, hyp_len=26360, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.214.0.51-1.67.1.84-6.31.pth
BLEU = 63.73, 82.1/68.7/58.4/50.1 (BP=1.000, ratio=1.021, hyp_len=29419, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.215.0.53-1.69.1.86-6.44.pth
BLEU = 64.38, 82.7/69.4/59.0/50.7 (BP=1.000, ratio=1.012, hyp_len=29136, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.216.0.51-1.66.1.87-6.50.pth
BLEU = 65.17, 83.4/70.1/59.8/51.6 (BP=1.000, ratio=1.002, hyp_len=28865, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.217.0.50-1.66.1.89-6.65.pth
BLEU = 62.70, 81.5/68.1/57.2/48.6 (BP=1.000, ratio=1.029, hyp_len=29642, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.218.0.51-1.66.1.87-6.47.pth
BLEU = 64.38, 82.6/69.4/59.0/50.8 (BP=1.000, ratio=1.019, hyp_len=29339, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.219.0.48-1.62.1.85-6.37.pth
BLEU = 65.80, 83.8/70.8/60.5/52.3 (BP=1.000, ratio=1.001, hyp_len=28839, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.220.0.49-1.63.1.86-6.44.pth
BLEU = 64.69, 82.6/69.4/59.4/51.4 (BP=1.000, ratio=1.018, hyp_len=29327, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.221.0.49-1.64.1.84-6.30.pth
BLEU = 63.96, 82.0/68.9/58.7/50.5 (BP=1.000, ratio=1.029, hyp_len=29627, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.222.0.52-1.68.1.88-6.54.pth
BLEU = 64.12, 83.1/69.5/58.6/50.0 (BP=1.000, ratio=1.006, hyp_len=28963, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.223.0.46-1.59.1.85-6.37.pth
BLEU = 65.91, 83.8/70.7/60.6/52.5 (BP=1.000, ratio=1.003, hyp_len=28894, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.22.3.90-49.27.4.44-84.83.pth
BLEU = 5.66, 36.7/11.0/3.5/0.8 (BP=0.987, ratio=0.987, hyp_len=28434, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.224.0.47-1.60.1.84-6.31.pth
BLEU = 64.69, 82.7/69.6/59.4/51.2 (BP=1.000, ratio=1.016, hyp_len=29263, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.225.0.52-1.68.1.86-6.41.pth
BLEU = 64.89, 83.1/69.8/59.5/51.4 (BP=1.000, ratio=1.011, hyp_len=29111, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.226.0.47-1.60.1.84-6.28.pth
BLEU = 65.42, 83.3/70.3/60.1/52.0 (BP=1.000, ratio=1.011, hyp_len=29111, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.227.0.46-1.59.1.83-6.22.pth
BLEU = 65.31, 83.1/70.2/60.0/52.0 (BP=1.000, ratio=1.014, hyp_len=29193, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.228.0.48-1.61.1.83-6.22.pth
BLEU = 65.70, 83.4/70.5/60.5/52.4 (BP=1.000, ratio=1.011, hyp_len=29129, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.229.0.45-1.56.1.84-6.27.pth
BLEU = 65.08, 82.6/69.9/60.0/51.8 (BP=1.000, ratio=1.020, hyp_len=29372, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.230.0.48-1.62.1.86-6.44.pth
BLEU = 65.54, 83.8/70.6/60.1/51.8 (BP=1.000, ratio=1.003, hyp_len=28890, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.231.0.47-1.60.1.82-6.17.pth
BLEU = 65.53, 83.2/70.4/60.3/52.2 (BP=1.000, ratio=1.016, hyp_len=29262, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.232.0.48-1.62.1.82-6.16.pth
BLEU = 65.42, 83.2/70.3/60.2/52.1 (BP=1.000, ratio=1.017, hyp_len=29283, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.233.0.46-1.58.1.82-6.15.pth
BLEU = 63.79, 82.0/68.9/58.4/50.1 (BP=1.000, ratio=1.028, hyp_len=29598, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.23.3.83-45.85.4.40-81.51.pth
BLEU = 5.92, 39.0/11.9/3.9/0.9 (BP=0.937, ratio=0.939, hyp_len=27043, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.234.0.47-1.60.1.81-6.13.pth
BLEU = 65.76, 83.6/70.7/60.5/52.3 (BP=1.000, ratio=1.012, hyp_len=29145, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.235.0.47-1.60.1.85-6.37.pth
BLEU = 63.31, 81.6/68.6/58.0/49.5 (BP=1.000, ratio=1.037, hyp_len=29862, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.236.0.49-1.63.1.86-6.40.pth
BLEU = 65.57, 83.3/70.4/60.3/52.2 (BP=1.000, ratio=1.012, hyp_len=29150, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.237.0.44-1.56.1.83-6.21.pth
BLEU = 64.02, 82.2/69.3/58.6/50.3 (BP=1.000, ratio=1.028, hyp_len=29618, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.238.0.42-1.53.1.80-6.08.pth
BLEU = 65.36, 83.0/70.3/60.1/52.0 (BP=1.000, ratio=1.021, hyp_len=29407, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.239.0.45-1.57.1.84-6.27.pth
BLEU = 66.31, 83.8/71.1/61.1/53.1 (BP=1.000, ratio=1.007, hyp_len=29016, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.240.0.57-1.76.1.87-6.46.pth
BLEU = 65.99, 84.2/71.0/60.8/52.5 (BP=0.998, ratio=0.998, hyp_len=28753, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.241.0.49-1.63.1.86-6.42.pth
BLEU = 66.54, 84.2/71.3/61.3/53.3 (BP=0.999, ratio=0.999, hyp_len=28784, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.242.0.42-1.53.1.80-6.07.pth
BLEU = 65.91, 83.3/70.6/60.7/52.8 (BP=1.000, ratio=1.015, hyp_len=29240, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.243.0.42-1.52.1.80-6.05.pth
BLEU = 66.92, 84.2/71.6/61.7/53.8 (BP=1.000, ratio=1.006, hyp_len=28990, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.24.3.72-41.43.4.36-78.30.pth
BLEU = 6.10, 39.1/12.1/3.9/0.9 (BP=0.954, ratio=0.955, hyp_len=27500, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.244.0.43-1.54.1.77-5.88.pth
BLEU = 65.95, 83.3/70.8/60.8/52.7 (BP=1.000, ratio=1.017, hyp_len=29289, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.245.0.43-1.54.1.78-5.92.pth
BLEU = 66.16, 83.4/70.8/61.1/53.1 (BP=1.000, ratio=1.016, hyp_len=29260, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.246.0.42-1.53.1.80-6.02.pth
BLEU = 66.22, 83.6/71.0/61.1/53.0 (BP=1.000, ratio=1.015, hyp_len=29227, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.247.0.49-1.64.1.85-6.36.pth
BLEU = 66.51, 84.8/72.0/61.9/53.8 (BP=0.990, ratio=0.990, hyp_len=28522, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.248.0.43-1.54.1.82-6.14.pth
BLEU = 66.48, 83.8/71.2/61.3/53.4 (BP=1.000, ratio=1.010, hyp_len=29090, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.249.0.43-1.54.1.80-6.06.pth
BLEU = 66.75, 83.9/71.4/61.6/53.7 (BP=1.000, ratio=1.011, hyp_len=29122, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.250.0.44-1.56.1.81-6.09.pth
BLEU = 65.77, 83.2/70.7/60.6/52.5 (BP=1.000, ratio=1.022, hyp_len=29424, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.251.0.43-1.53.1.80-6.05.pth
BLEU = 67.29, 84.4/71.9/62.2/54.3 (BP=1.000, ratio=1.007, hyp_len=28998, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.252.0.39-1.48.1.76-5.81.pth
BLEU = 67.56, 84.5/72.1/62.5/54.7 (BP=1.000, ratio=1.007, hyp_len=28995, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.253.0.48-1.62.1.80-6.08.pth
BLEU = 66.81, 84.1/71.5/61.7/53.7 (BP=1.000, ratio=1.008, hyp_len=29025, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.25.3.71-41.05.4.33-75.76.pth
BLEU = 6.45, 39.4/12.4/4.1/1.0 (BP=0.964, ratio=0.964, hyp_len=27773, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.254.0.41-1.51.1.79-5.98.pth
BLEU = 67.48, 84.5/72.2/62.4/54.5 (BP=1.000, ratio=1.004, hyp_len=28918, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.255.0.42-1.52.1.78-5.96.pth
BLEU = 65.82, 83.2/70.7/60.6/52.6 (BP=1.000, ratio=1.023, hyp_len=29457, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.256.0.44-1.56.1.77-5.89.pth
BLEU = 67.41, 84.6/72.1/62.3/54.4 (BP=1.000, ratio=1.005, hyp_len=28944, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.257.0.38-1.46.1.78-5.95.pth
BLEU = 67.39, 84.3/72.0/62.3/54.5 (BP=1.000, ratio=1.010, hyp_len=29084, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.258.0.46-1.58.1.76-5.79.pth
BLEU = 67.37, 84.2/71.9/62.3/54.6 (BP=1.000, ratio=1.010, hyp_len=29094, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.259.0.39-1.47.1.76-5.84.pth
BLEU = 67.25, 84.3/72.0/62.2/54.2 (BP=1.000, ratio=1.010, hyp_len=29094, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.260.0.39-1.48.1.78-5.90.pth
BLEU = 66.80, 84.3/71.8/61.5/53.4 (BP=1.000, ratio=1.008, hyp_len=29028, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.261.0.40-1.49.1.76-5.81.pth
BLEU = 67.01, 84.0/71.8/61.9/54.0 (BP=1.000, ratio=1.014, hyp_len=29219, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.262.0.42-1.52.1.75-5.76.pth
BLEU = 67.01, 84.0/71.8/61.9/54.0 (BP=1.000, ratio=1.015, hyp_len=29231, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.263.0.39-1.48.1.75-5.73.pth
BLEU = 67.47, 84.4/72.1/62.4/54.6 (BP=1.000, ratio=1.012, hyp_len=29150, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.26.3.64-37.99.4.29-73.25.pth
BLEU = 6.44, 40.0/12.9/4.2/0.9 (BP=0.960, ratio=0.961, hyp_len=27673, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.264.0.38-1.46.1.72-5.60.pth
BLEU = 67.23, 84.2/72.0/62.2/54.2 (BP=1.000, ratio=1.014, hyp_len=29204, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.265.0.40-1.49.1.74-5.67.pth
BLEU = 67.24, 84.1/72.0/62.2/54.3 (BP=1.000, ratio=1.016, hyp_len=29265, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.266.0.36-1.44.1.74-5.72.pth
BLEU = 68.41, 84.9/72.9/63.5/55.8 (BP=1.000, ratio=1.006, hyp_len=28967, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.267.0.42-1.52.1.75-5.75.pth
BLEU = 68.50, 85.2/73.1/63.5/55.7 (BP=1.000, ratio=1.001, hyp_len=28844, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.268.0.39-1.48.1.74-5.71.pth
BLEU = 68.54, 85.3/73.1/63.5/55.8 (BP=1.000, ratio=1.000, hyp_len=28802, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.269.0.41-1.51.1.79-6.01.pth
BLEU = 66.69, 83.9/71.4/61.5/53.6 (BP=1.000, ratio=1.012, hyp_len=29149, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.270.0.40-1.50.1.72-5.58.pth
BLEU = 67.57, 84.4/72.2/62.5/54.7 (BP=1.000, ratio=1.012, hyp_len=29146, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.271.0.37-1.44.1.75-5.73.pth
BLEU = 67.25, 84.0/71.9/62.2/54.5 (BP=1.000, ratio=1.021, hyp_len=29400, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.272.0.36-1.43.1.72-5.59.pth
BLEU = 67.01, 83.6/71.7/62.0/54.2 (BP=1.000, ratio=1.025, hyp_len=29517, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.273.0.39-1.47.1.75-5.76.pth
BLEU = 68.41, 84.9/72.8/63.4/55.9 (BP=1.000, ratio=1.006, hyp_len=28965, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.27.3.62-37.34.4.26-70.75.pth
BLEU = 6.74, 39.8/12.8/4.3/1.0 (BP=0.984, ratio=0.985, hyp_len=28357, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.274.0.41-1.50.1.74-5.71.pth
BLEU = 67.12, 84.1/71.8/62.0/54.2 (BP=1.000, ratio=1.015, hyp_len=29234, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.275.0.38-1.47.1.74-5.71.pth
BLEU = 67.02, 83.9/71.8/61.9/54.0 (BP=1.000, ratio=1.019, hyp_len=29350, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.276.0.39-1.47.1.75-5.77.pth
BLEU = 67.54, 84.3/72.1/62.6/54.7 (BP=1.000, ratio=1.013, hyp_len=29189, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.277.0.38-1.47.1.72-5.59.pth
BLEU = 67.40, 84.2/72.1/62.4/54.5 (BP=1.000, ratio=1.017, hyp_len=29288, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.278.0.36-1.43.1.71-5.52.pth
BLEU = 67.44, 83.8/72.1/62.5/54.8 (BP=1.000, ratio=1.022, hyp_len=29447, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.279.0.37-1.44.1.73-5.67.pth
BLEU = 67.78, 84.6/72.5/62.8/54.8 (BP=1.000, ratio=1.012, hyp_len=29145, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.280.0.38-1.47.1.72-5.59.pth
BLEU = 67.82, 84.4/72.4/62.8/55.1 (BP=1.000, ratio=1.017, hyp_len=29286, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.281.0.37-1.45.1.73-5.65.pth
BLEU = 65.90, 83.1/70.9/60.7/52.7 (BP=1.000, ratio=1.030, hyp_len=29654, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.282.0.38-1.46.1.69-5.44.pth
BLEU = 68.70, 85.2/73.2/63.8/56.0 (BP=1.000, ratio=1.006, hyp_len=28982, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.283.0.38-1.46.1.72-5.59.pth
BLEU = 68.25, 84.5/72.7/63.3/55.7 (BP=1.000, ratio=1.013, hyp_len=29179, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.28.3.53-34.06.4.23-68.84.pth
BLEU = 7.20, 41.7/13.8/4.7/1.2 (BP=0.949, ratio=0.950, hyp_len=27373, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.284.0.38-1.46.1.71-5.51.pth
BLEU = 68.53, 84.7/73.0/63.6/56.0 (BP=1.000, ratio=1.011, hyp_len=29119, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.285.0.36-1.43.1.72-5.60.pth
BLEU = 67.78, 84.2/72.3/62.8/55.2 (BP=1.000, ratio=1.020, hyp_len=29385, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.286.0.37-1.45.1.70-5.48.pth
BLEU = 67.95, 84.3/72.5/63.0/55.3 (BP=1.000, ratio=1.018, hyp_len=29323, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.287.0.36-1.44.1.70-5.46.pth
BLEU = 68.27, 84.7/72.9/63.3/55.6 (BP=1.000, ratio=1.015, hyp_len=29248, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.288.0.39-1.47.1.69-5.41.pth
BLEU = 67.94, 84.4/72.6/63.0/55.2 (BP=1.000, ratio=1.017, hyp_len=29303, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.289.0.34-1.41.1.72-5.60.pth
BLEU = 68.12, 84.6/72.7/63.2/55.5 (BP=1.000, ratio=1.013, hyp_len=29179, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.290.0.37-1.45.1.71-5.51.pth
BLEU = 68.87, 85.1/73.3/64.0/56.4 (BP=1.000, ratio=1.009, hyp_len=29071, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.291.0.41-1.51.1.71-5.52.pth
BLEU = 68.60, 84.9/73.2/63.6/56.0 (BP=1.000, ratio=1.011, hyp_len=29132, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.292.0.35-1.42.1.73-5.67.pth
BLEU = 67.07, 84.1/72.0/61.9/53.9 (BP=1.000, ratio=1.020, hyp_len=29373, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.293.0.35-1.42.1.72-5.59.pth
BLEU = 69.25, 85.7/73.8/64.2/56.6 (BP=1.000, ratio=1.001, hyp_len=28823, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.29.3.61-37.03.4.21-67.36.pth
BLEU = 7.48, 41.2/13.9/4.8/1.3 (BP=0.970, ratio=0.970, hyp_len=27941, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.294.0.33-1.40.1.69-5.39.pth
BLEU = 68.70, 84.7/73.1/63.8/56.4 (BP=1.000, ratio=1.017, hyp_len=29289, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.295.0.36-1.43.1.67-5.34.pth
BLEU = 68.44, 84.7/72.9/63.5/55.9 (BP=1.000, ratio=1.017, hyp_len=29296, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.296.0.37-1.45.1.69-5.42.pth
BLEU = 68.20, 84.5/72.8/63.3/55.6 (BP=1.000, ratio=1.018, hyp_len=29310, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.297.0.34-1.41.1.68-5.36.pth
BLEU = 68.91, 85.3/73.6/63.9/56.2 (BP=1.000, ratio=1.009, hyp_len=29052, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.298.0.37-1.45.1.73-5.64.pth
BLEU = 69.18, 85.7/73.9/64.5/56.8 (BP=0.997, ratio=0.997, hyp_len=28713, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.299.0.42-1.51.1.74-5.67.pth
BLEU = 65.14, 81.6/69.8/60.3/52.5 (BP=1.000, ratio=1.051, hyp_len=30262, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.300.0.35-1.42.1.77-5.87.pth
BLEU = 65.65, 83.7/71.2/60.3/51.7 (BP=1.000, ratio=1.021, hyp_len=29403, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.30.3.45-31.49.4.17-64.62.pth
BLEU = 7.72, 41.7/14.2/4.9/1.3 (BP=0.985, ratio=0.985, hyp_len=28360, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.31.3.45-31.44.4.14-62.64.pth
BLEU = 8.43, 43.4/15.0/5.5/1.7 (BP=0.952, ratio=0.953, hyp_len=27461, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.32.3.35-28.61.4.11-61.04.pth
BLEU = 8.89, 42.2/14.9/5.5/1.8 (BP=1.000, ratio=1.000, hyp_len=28800, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.33.3.36-28.89.4.06-57.97.pth
BLEU = 8.75, 41.0/14.5/5.4/1.8 (BP=1.000, ratio=1.049, hyp_len=30216, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.34.3.30-27.10.4.04-56.98.pth
BLEU = 9.18, 42.1/15.3/5.7/1.9 (BP=1.000, ratio=1.025, hyp_len=29527, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.35.3.22-25.10.3.99-54.17.pth
BLEU = 10.04, 44.1/16.4/6.3/2.3 (BP=0.994, ratio=0.994, hyp_len=28638, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.36.3.20-24.52.3.97-53.23.pth
BLEU = 9.60, 42.9/15.9/6.1/2.1 (BP=1.000, ratio=1.035, hyp_len=29802, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.37.3.21-24.83.3.94-51.52.pth
BLEU = 10.40, 44.6/16.8/6.6/2.4 (BP=1.000, ratio=1.001, hyp_len=28844, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.38.3.13-22.91.3.92-50.17.pth
BLEU = 10.93, 46.3/17.7/7.1/2.7 (BP=0.975, ratio=0.975, hyp_len=28092, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.39.3.14-23.15.3.88-48.26.pth
BLEU = 10.97, 46.6/18.1/7.1/2.6 (BP=0.984, ratio=0.984, hyp_len=28355, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.40.3.02-20.56.3.85-47.09.pth
BLEU = 10.71, 43.5/17.1/6.9/2.6 (BP=1.000, ratio=1.072, hyp_len=30869, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.41.3.02-20.49.3.82-45.70.pth
BLEU = 11.89, 49.0/19.8/8.1/3.1 (BP=0.951, ratio=0.952, hyp_len=27425, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.42.2.99-19.96.3.79-44.39.pth
BLEU = 12.07, 46.8/19.0/7.9/3.0 (BP=1.000, ratio=1.018, hyp_len=29316, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.43.2.89-18.03.3.76-43.07.pth
BLEU = 12.21, 46.8/19.2/8.0/3.1 (BP=1.000, ratio=1.032, hyp_len=29735, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.44.2.85-17.32.3.73-41.62.pth
BLEU = 12.97, 48.6/20.2/8.6/3.4 (BP=1.000, ratio=1.004, hyp_len=28913, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.45.2.86-17.42.3.70-40.30.pth
BLEU = 12.79, 47.1/19.9/8.4/3.4 (BP=1.000, ratio=1.053, hyp_len=30340, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.46.2.79-16.36.3.66-38.95.pth
BLEU = 13.22, 47.3/20.2/8.7/3.6 (BP=1.000, ratio=1.051, hyp_len=30269, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.47.2.81-16.54.3.63-37.66.pth
BLEU = 13.63, 48.9/21.1/9.1/3.7 (BP=1.000, ratio=1.026, hyp_len=29541, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.48.2.73-15.29.3.60-36.45.pth
BLEU = 14.48, 50.7/22.2/9.7/4.0 (BP=1.000, ratio=1.001, hyp_len=28831, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.49.2.70-14.94.3.57-35.57.pth
BLEU = 14.63, 49.6/22.1/9.9/4.2 (BP=1.000, ratio=1.033, hyp_len=29740, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.50.2.67-14.44.3.52-33.86.pth
BLEU = 15.17, 50.4/22.8/10.3/4.5 (BP=1.000, ratio=1.022, hyp_len=29451, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.51.2.62-13.75.3.49-32.77.pth
BLEU = 16.04, 51.9/23.8/11.0/4.9 (BP=1.000, ratio=1.001, hyp_len=28833, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.52.2.64-14.04.3.45-31.62.pth
BLEU = 16.27, 52.3/24.2/11.1/5.0 (BP=1.000, ratio=1.001, hyp_len=28840, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.53.2.59-13.28.3.43-30.93.pth
BLEU = 16.61, 52.0/24.3/11.5/5.2 (BP=1.000, ratio=1.022, hyp_len=29435, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.54.2.55-12.83.3.39-29.72.pth
BLEU = 17.49, 53.8/25.6/12.3/5.7 (BP=0.993, ratio=0.993, hyp_len=28590, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.55.2.46-11.69.3.37-29.01.pth
BLEU = 18.22, 55.1/26.7/13.1/6.3 (BP=0.977, ratio=0.978, hyp_len=28159, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.56.2.45-11.58.3.33-27.95.pth
BLEU = 18.04, 52.8/25.9/12.7/6.1 (BP=1.000, ratio=1.038, hyp_len=29896, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.57.2.42-11.22.3.30-27.12.pth
BLEU = 18.65, 54.5/26.9/13.2/6.3 (BP=1.000, ratio=1.011, hyp_len=29127, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.58.2.38-10.79.3.26-25.93.pth
BLEU = 19.07, 54.1/27.1/13.6/6.6 (BP=1.000, ratio=1.029, hyp_len=29638, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.59.2.38-10.83.3.24-25.56.pth
BLEU = 20.14, 57.0/29.0/14.8/7.4 (BP=0.977, ratio=0.977, hyp_len=28147, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.60.2.36-10.54.3.24-25.66.pth
BLEU = 19.85, 55.2/28.2/14.3/7.0 (BP=1.000, ratio=1.021, hyp_len=29418, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.61.2.29-9.83.3.17-23.74.pth
BLEU = 21.25, 57.8/29.9/15.7/8.1 (BP=0.981, ratio=0.982, hyp_len=28275, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.62.2.30-9.93.3.13-22.93.pth
BLEU = 21.45, 56.9/29.9/15.7/7.9 (BP=1.000, ratio=1.008, hyp_len=29045, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.63.2.20-9.06.3.12-22.61.pth
BLEU = 21.65, 56.4/29.7/15.8/8.3 (BP=1.000, ratio=1.023, hyp_len=29467, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.64.2.23-9.30.3.07-21.58.pth
BLEU = 21.77, 55.9/29.8/16.0/8.4 (BP=1.000, ratio=1.047, hyp_len=30149, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.65.2.15-8.57.3.05-21.11.pth
BLEU = 23.43, 60.0/32.7/17.9/9.6 (BP=0.972, ratio=0.973, hyp_len=28021, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.66.2.10-8.18.3.02-20.47.pth
BLEU = 23.99, 59.1/32.3/17.9/9.7 (BP=1.000, ratio=1.003, hyp_len=28897, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.67.2.16-8.68.2.99-19.92.pth
BLEU = 24.68, 59.9/33.3/18.6/10.1 (BP=0.997, ratio=0.997, hyp_len=28710, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.68.2.09-8.08.2.96-19.38.pth
BLEU = 23.85, 57.5/31.8/17.9/9.9 (BP=1.000, ratio=1.047, hyp_len=30155, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.69.2.03-7.63.2.94-18.90.pth
BLEU = 25.48, 59.7/33.7/19.3/10.9 (BP=1.000, ratio=1.015, hyp_len=29238, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.70.1.98-7.25.2.90-18.24.pth
BLEU = 25.43, 58.5/33.4/19.3/11.1 (BP=1.000, ratio=1.049, hyp_len=30211, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.71.2.05-7.74.2.89-18.06.pth
BLEU = 26.96, 61.4/35.3/20.6/11.8 (BP=1.000, ratio=1.001, hyp_len=28840, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.72.2.02-7.55.2.86-17.44.pth
BLEU = 27.32, 61.8/35.7/20.9/12.1 (BP=0.999, ratio=0.999, hyp_len=28769, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.73.1.96-7.13.2.84-17.18.pth
BLEU = 27.09, 60.7/35.4/20.9/12.0 (BP=1.000, ratio=1.030, hyp_len=29655, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.74.1.90-6.68.2.81-16.60.pth
BLEU = 28.17, 61.9/36.7/21.9/12.7 (BP=1.000, ratio=1.011, hyp_len=29129, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.75.1.88-6.56.2.77-16.02.pth
BLEU = 29.36, 63.2/37.6/22.8/13.7 (BP=1.000, ratio=1.000, hyp_len=28815, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.76.1.85-6.34.2.75-15.70.pth
BLEU = 30.25, 63.0/38.3/23.7/14.6 (BP=1.000, ratio=1.009, hyp_len=29072, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.77.1.81-6.14.2.72-15.17.pth
BLEU = 30.25, 63.2/38.4/23.7/14.6 (BP=1.000, ratio=1.017, hyp_len=29301, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.78.1.81-6.11.2.70-14.93.pth
BLEU = 30.67, 63.1/38.7/24.2/15.0 (BP=1.000, ratio=1.023, hyp_len=29464, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.79.1.83-6.24.2.69-14.79.pth
BLEU = 31.45, 63.7/39.4/24.8/15.7 (BP=1.000, ratio=1.019, hyp_len=29345, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.80.1.73-5.63.2.68-14.51.pth
BLEU = 32.24, 65.2/40.5/25.7/16.2 (BP=0.996, ratio=0.996, hyp_len=28685, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.81.1.76-5.82.2.66-14.28.pth
BLEU = 33.25, 65.6/41.5/26.7/17.2 (BP=0.995, ratio=0.995, hyp_len=28669, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.82.1.70-5.50.2.64-13.96.pth
BLEU = 33.30, 64.7/41.0/26.7/17.4 (BP=1.000, ratio=1.018, hyp_len=29327, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.83.1.69-5.40.2.60-13.50.pth
BLEU = 33.59, 64.9/41.5/26.9/17.6 (BP=1.000, ratio=1.020, hyp_len=29382, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.84.1.71-5.54.2.64-13.96.pth
BLEU = 34.44, 67.8/43.5/28.4/18.6 (BP=0.974, ratio=0.974, hyp_len=28068, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.85.1.66-5.28.2.59-13.34.pth
BLEU = 33.19, 64.4/41.3/26.6/17.1 (BP=1.000, ratio=1.036, hyp_len=29851, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.86.1.60-4.94.2.54-12.74.pth
BLEU = 35.85, 67.4/43.9/29.3/19.5 (BP=0.995, ratio=0.995, hyp_len=28646, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.87.1.65-5.19.2.52-12.47.pth
BLEU = 35.88, 66.8/43.7/29.1/19.5 (BP=1.000, ratio=1.012, hyp_len=29158, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.88.1.59-4.93.2.51-12.25.pth
BLEU = 36.61, 67.0/44.3/29.9/20.2 (BP=1.000, ratio=1.014, hyp_len=29196, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.89.1.55-4.70.2.49-12.05.pth
BLEU = 35.72, 65.4/43.4/29.2/19.7 (BP=1.000, ratio=1.045, hyp_len=30091, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.90.1.53-4.62.2.49-12.01.pth
BLEU = 36.40, 66.1/44.1/29.8/20.3 (BP=1.000, ratio=1.040, hyp_len=29950, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.91.1.51-4.51.2.46-11.75.pth
BLEU = 37.38, 67.2/45.1/30.7/21.0 (BP=1.000, ratio=1.022, hyp_len=29448, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.92.1.49-4.45.2.46-11.71.pth
BLEU = 37.55, 66.8/45.1/31.0/21.3 (BP=1.000, ratio=1.035, hyp_len=29805, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.93.1.50-4.47.2.45-11.57.pth
BLEU = 39.61, 69.5/47.2/32.9/23.0 (BP=0.998, ratio=0.998, hyp_len=28743, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.94.1.51-4.52.2.43-11.36.pth
BLEU = 40.11, 70.3/48.2/33.7/23.8 (BP=0.988, ratio=0.988, hyp_len=28463, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.95.1.41-4.11.2.43-11.39.pth
BLEU = 39.03, 68.4/46.7/32.3/22.5 (BP=1.000, ratio=1.021, hyp_len=29406, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.96.1.43-4.16.2.41-11.14.pth
BLEU = 40.05, 69.0/47.6/33.3/23.5 (BP=1.000, ratio=1.013, hyp_len=29166, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.97.1.47-4.33.2.39-10.96.pth
BLEU = 39.66, 67.9/47.0/33.1/23.4 (BP=1.000, ratio=1.039, hyp_len=29936, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.98.1.39-4.00.2.38-10.77.pth
BLEU = 42.14, 71.0/49.7/35.5/25.6 (BP=0.995, ratio=0.995, hyp_len=28669, ref_len=28803)
Evaluation result for the model: transformer-model-mybr.99.1.35-3.84.2.35-10.53.pth
BLEU = 41.50, 69.7/48.9/34.8/25.0 (BP=1.000, ratio=1.020, hyp_len=29369, ref_len=28803)
/home/ye/exp/simple-nmt

real	329m7.108s
user	324m17.078s
sys	8m7.974s
(simple-nmt) ye@:~/exp/simple-nmt$
```

မြန်မာ-မူဟောင်းအတွက် Best model နဲ့ Best score က အောက်ပါအတိုင်း...  

```
Evaluation result for the model: transformer-model-mybr.293.0.35-1.42.1.72-5.59.pth
BLEU = 69.25, 85.7/73.8/64.2/56.6 (BP=1.000, ratio=1.001, hyp_len=28823, ref_len=28803)
```

### bash script for testing (br-my)  

```bash

```

testing br-my ...  

```

```




