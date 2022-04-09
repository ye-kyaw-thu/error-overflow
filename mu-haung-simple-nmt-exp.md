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
--model_fn ./model/braille/seq2seq/br-my/seq-model-mybr.pth  | tee ./model/braille/seq2seq/br-my/mybr-seq2seq-training.log;

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

## Testing/Evaluation

```bash

```

testing ...  

```

```
