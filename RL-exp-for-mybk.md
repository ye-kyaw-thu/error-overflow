# RL Experiment for Myanmar-Beik Language Pair

ရှေ့မှာ လုပ်ခဲ့တဲ့ ရခိုင်-မြန်မာ RL experiment ရဲ့ အဆက်ပါ။ ရှေ့မှာလုပ်ခဲ့တဲ့ experiment တွေရဲ့ log က အောက်ပါအတိုင်းပါ။  

- [simple-nmt-experiment.md](https://github.com/ye-kyaw-thu/error-overflow/blob/master/simple-nmt-experiment.md)
- [simple-nmt-40-60-to-70-30-log.md](https://github.com/ye-kyaw-thu/error-overflow/blob/master/simple-nmt-40-60-to-70-30-log.md)

ဒီတစ်ခါတော့ မြန်မာ-ဘိတ် အတွဲအတွက်လုပ်ခဲ့စဉ်က မှတ်သားခဲ့တဲ့ running log ဖိုင်ပါ။  

## Folder Preparation

training မလုပ်ခင်မှာ အရင်ဆုံး အောက်ပါ folder-structure အတိုင်း ဖိုလ်ဒါတွေကိုဆောက်ထားလိုက်ပါတယ်။ ရှေ့က run ခဲ့တဲ့ မြန်မာ-ရခိုင်အတွဲရဲ့ folder-structure နဲ့တော့ အတိအကျမတူပါဘူး။ ဒီနေရာမှာ baseline/ က baseline model တွေကိုသိမ်းဖို့ ဖြစ်ပြီး၊ rl/ အောက်မှာကက reinforcement learning model တွေကို သိမ်းဖို့အတွက် ဖြစ်ပါတယ်။  

```
(base) ye@:~/exp/simple-nmt/model/rl2$ tree
.
├── baseline
│   ├── seq2seq
│   │   ├── bkmy-30epoch
│   │   ├── bkmy-40epoch
│   │   ├── bkmy-50epoch
│   │   ├── bkmy-60epoch
│   │   ├── bkmy-70epoch
│   │   ├── mybk-30epoch
│   │   ├── mybk-40epoch
│   │   ├── mybk-50epoch
│   │   ├── mybk-60epoch
│   │   └── mybk-70epoch
│   └── transformer
│       ├── bkmy-30epoch
│       ├── bkmy-40epoch
│       ├── bkmy-50epoch
│       ├── bkmy-60epoch
│       ├── bkmy-70epoch
│       ├── mybk-30epoch
│       ├── mybk-40epoch
│       ├── mybk-50epoch
│       ├── mybk-60epoch
│       └── mybk-70epoch
└── rl
    ├── seq2seq
    │   ├── bkmy-30epoch
    │   ├── bkmy-40epoch
    │   ├── bkmy-50epoch
    │   ├── bkmy-60epoch
    │   ├── bkmy-70epoch
    │   ├── mybk-30epoch
    │   ├── mybk-40epoch
    │   ├── mybk-50epoch
    │   ├── mybk-60epoch
    │   └── mybk-70epoch
    └── transformer
        ├── bkmy-30epoch
        ├── bkmy-40epoch
        ├── bkmy-50epoch
        ├── bkmy-60epoch
        ├── bkmy-70epoch
        ├── mybk-30epoch
        ├── mybk-40epoch
        ├── mybk-50epoch
        ├── mybk-60epoch
        └── mybk-70epoch

46 directories, 0 files

```

## for Seq2Seq Baseline
### Bash Script Writing

အရင်ဆုံး 30 epoch ကနေ 70 epoch အထိ seq2seq training အတွက် အောက်ပါ bash script ကို ရေးပြီး သုံးခဲ့...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Last updated: 3 April 2022
# Seq2Seq-Reinforcement Learning exp for Myanmar-Beik, Beik-Myanmar

# training baseline for my-bk

for i in {30,40,50,60,70}
do
      echo "mybk, seq2seq-baseline training start for ${i} epochs...";
   time python train.py --train /home/ye/exp/simple-nmt/data/my-bk/syl/train \
   --valid /home/ye/exp/simple-nmt/data/my-bk/syl/dev \
   --lang mybk \
   --gpu_id 0 --batch_size 64 --n_epochs ${i} \
   --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 \
   --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 \
   --use_adam --rl_n_epochs 0 \
   --model_fn ./model/rl2/baseline/seq2seq/mybk-${i}epoch/seq-model-mybk.pth  | tee ./model/rl2/baseline/seq2seq/mybk-${i}epoch/mybk-training.log;
done

echo "####################";

# training baseline for bk-my
for i in {30,40,50,60,70}
do
      echo "bkmy, seq2seq-baseline training start for ${i} epochs...";
   time python train.py --train /home/ye/exp/simple-nmt/data/my-bk/syl/train \
   --valid /home/ye/exp/simple-nmt/data/my-bk/syl/dev \
   --lang bkmy \
   --gpu_id 1 --batch_size 64 --n_epochs ${i} \
   --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 \
   --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 \
   --use_adam --rl_n_epochs 0 \
   --model_fn ./model/rl2/baseline/seq2seq/bkmy-${i}epoch/seq-model-bkmy.pth | tee ./model/rl2/baseline/seq2seq/bkmy-${i}epoch/bkmy-training.log;
done
```

### Training

output အကုန်ကိုတော့ ဒီနေရာမှာ မသိမ်းတော့ဘူး။ လိုင်းအရေအတွက်က တအားများလွန်းလို့...  
running process နဲ့ အဓိကကျတဲ့ အပိုင်းကို follow လိုက်လို့ ရအောင်ပဲ log မှတ်သွားမယ်။  
မော်ဒယ်တစ်ခုချင်းစီအတွက်က training လုပ်ရင်းနဲ့ tee command နဲ့ သိမ်းထားပြီးသားလည်း သက်ဆိုင်ရာ ဖိုလ်ဒါအောက်မှာ ရှိတယ်။  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./rl-seq2seq-train.sh | tee rl-seq2seq-baseline-training-for-mybk-bkmy.log
...
...
...
Epoch 56 - |param|=6.24e+02 |g_param|=4.65e+05 loss=1.8616e+00 ppl=6.43                                                 
Validation - loss=2.3675e+00 ppl=10.67 best_loss=2.3372e+00 best_ppl=10.35                                              
Epoch 57 - |param|=6.25e+02 |g_param|=4.68e+05 loss=1.8483e+00 ppl=6.35                                                 
Validation - loss=2.3562e+00 ppl=10.55 best_loss=2.3372e+00 best_ppl=10.35                                              
Epoch 58 - |param|=6.25e+02 |g_param|=5.09e+05 loss=1.8452e+00 ppl=6.33                                                 
Validation - loss=2.4093e+00 ppl=11.13 best_loss=2.3372e+00 best_ppl=10.35                                              
Epoch 59 - |param|=6.26e+02 |g_param|=5.03e+05 loss=1.7908e+00 ppl=5.99                                                 
Validation - loss=2.3624e+00 ppl=10.62 best_loss=2.3372e+00 best_ppl=10.35                                              
Epoch 60 - |param|=6.26e+02 |g_param|=4.83e+05 loss=1.7543e+00 ppl=5.78                                                 
Validation - loss=2.3715e+00 ppl=10.71 best_loss=2.3372e+00 best_ppl=10.35                                              

real	12m32.816s
user	12m18.553s
sys	0m15.420s
bkmy, seq2seq-baseline training start for 70 epochs...
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'bkmy',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/baseline/seq2seq/bkmy-70epoch/seq-model-bkmy.pth',
    'n_epochs': 70,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'rl_lr': 0.01,
    'rl_n_epochs': 0,
    'rl_n_gram': 6,
    'rl_n_samples': 1,
    'rl_reward': 'gleu',
    'train': '/home/ye/exp/simple-nmt/data/my-bk/syl/train',
    'use_adam': True,
    'use_radam': False,
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/my-bk/syl/dev',
    'verbose': 2,
    'word_vec_size': 128}
Seq2Seq(
  (emb_src): Embedding(1468, 128)
  (emb_dec): Embedding(1315, 128)
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
    (output): Linear(in_features=128, out_features=1315, bias=True)
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
Epoch 1 - |param|=6.00e+02 |g_param|=2.34e+05 loss=4.7526e+00 ppl=115.89                                                
Validation - loss=3.9725e+00 ppl=53.12 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=6.00e+02 |g_param|=2.03e+05 loss=4.2449e+00 ppl=69.75                                                 
Validation - loss=3.8145e+00 ppl=45.36 best_loss=3.9725e+00 best_ppl=53.12                                              
Epoch 3 - |param|=6.00e+02 |g_param|=1.97e+05 loss=4.1685e+00 ppl=64.62                                                 
Validation - loss=3.7949e+00 ppl=44.47 best_loss=3.8145e+00 best_ppl=45.36                                              
Epoch 4 - |param|=6.00e+02 |g_param|=1.93e+05 loss=4.1432e+00 ppl=63.00                                                 
Validation - loss=3.7877e+00 ppl=44.15 best_loss=3.7949e+00 best_ppl=44.47                                              
Epoch 5 - |param|=6.00e+02 |g_param|=1.92e+05 loss=4.1479e+00 ppl=63.30                                                 
Validation - loss=3.7642e+00 ppl=43.13 best_loss=3.7877e+00 best_ppl=44.15                                              
Epoch 6 - |param|=6.01e+02 |g_param|=2.03e+05 loss=4.1539e+00 ppl=63.68                                                 
Validation - loss=3.7653e+00 ppl=43.18 best_loss=3.7642e+00 best_ppl=43.13                                              
Epoch 7 - |param|=6.01e+02 |g_param|=2.00e+05 loss=4.1428e+00 ppl=62.98                                                 
Validation - loss=3.7332e+00 ppl=41.81 best_loss=3.7642e+00 best_ppl=43.13                                              
Epoch 8 - |param|=6.01e+02 |g_param|=1.86e+05 loss=4.0900e+00 ppl=59.74                                                 
Validation - loss=3.7278e+00 ppl=41.59 best_loss=3.7332e+00 best_ppl=41.81                                              
Epoch 9 - |param|=6.01e+02 |g_param|=2.16e+05 loss=4.1818e+00 ppl=65.49                                                 
Validation - loss=3.7151e+00 ppl=41.06 best_loss=3.7278e+00 best_ppl=41.59                                              
Epoch 10 - |param|=6.02e+02 |g_param|=2.03e+05 loss=4.0789e+00 ppl=59.08                                                
Validation - loss=3.6509e+00 ppl=38.51 best_loss=3.7151e+00 best_ppl=41.06                                              
Epoch 11 - |param|=6.02e+02 |g_param|=1.88e+05 loss=4.0612e+00 ppl=58.04                                                
Validation - loss=3.5849e+00 ppl=36.05 best_loss=3.6509e+00 best_ppl=38.51                                              
Epoch 12 - |param|=6.02e+02 |g_param|=1.62e+05 loss=3.8638e+00 ppl=47.65                                                
Validation - loss=3.3608e+00 ppl=28.81 best_loss=3.5849e+00 best_ppl=36.05                                              
Epoch 13 - |param|=6.03e+02 |g_param|=1.46e+05 loss=3.7770e+00 ppl=43.68                                                
Validation - loss=3.2356e+00 ppl=25.42 best_loss=3.3608e+00 best_ppl=28.81                                              
Epoch 14 - |param|=6.03e+02 |g_param|=1.39e+05 loss=3.5337e+00 ppl=34.25                                                
Validation - loss=3.1693e+00 ppl=23.79 best_loss=3.2356e+00 best_ppl=25.42                                              
Epoch 15 - |param|=6.04e+02 |g_param|=1.33e+05 loss=3.4623e+00 ppl=31.89                                                
Validation - loss=3.1107e+00 ppl=22.44 best_loss=3.1693e+00 best_ppl=23.79                                              
Epoch 16 - |param|=6.04e+02 |g_param|=1.40e+05 loss=3.3927e+00 ppl=29.75                                                
Validation - loss=3.0488e+00 ppl=21.09 best_loss=3.1107e+00 best_ppl=22.44                                              
Epoch 17 - |param|=6.05e+02 |g_param|=1.33e+05 loss=3.3143e+00 ppl=27.50                                                
Validation - loss=2.9850e+00 ppl=19.79 best_loss=3.0488e+00 best_ppl=21.09                                              
Epoch 18 - |param|=6.05e+02 |g_param|=1.48e+05 loss=3.2833e+00 ppl=26.66                                                
Validation - loss=2.9400e+00 ppl=18.92 best_loss=2.9850e+00 best_ppl=19.79                                              
Epoch 19 - |param|=6.06e+02 |g_param|=1.50e+05 loss=3.2770e+00 ppl=26.50                                                
Validation - loss=2.8964e+00 ppl=18.11 best_loss=2.9400e+00 best_ppl=18.92                                              
Epoch 20 - |param|=6.06e+02 |g_param|=1.38e+05 loss=3.1533e+00 ppl=23.41                                                
Validation - loss=2.8500e+00 ppl=17.29 best_loss=2.8964e+00 best_ppl=18.11                                              
Epoch 21 - |param|=6.07e+02 |g_param|=1.34e+05 loss=3.1187e+00 ppl=22.62                                                
Validation - loss=2.7906e+00 ppl=16.29 best_loss=2.8500e+00 best_ppl=17.29                                              
Epoch 22 - |param|=6.07e+02 |g_param|=1.48e+05 loss=3.0963e+00 ppl=22.12                                                
Validation - loss=2.7741e+00 ppl=16.02 best_loss=2.7906e+00 best_ppl=16.29                                              
Epoch 23 - |param|=6.08e+02 |g_param|=1.42e+05 loss=3.1021e+00 ppl=22.24                                                
Validation - loss=2.7135e+00 ppl=15.08 best_loss=2.7741e+00 best_ppl=16.02                                              
Epoch 24 - |param|=6.08e+02 |g_param|=1.51e+05 loss=2.9268e+00 ppl=18.67                                                
Validation - loss=2.6713e+00 ppl=14.46 best_loss=2.7135e+00 best_ppl=15.08                                              
Epoch 25 - |param|=6.09e+02 |g_param|=1.50e+05 loss=2.9304e+00 ppl=18.73                                                
Validation - loss=2.6566e+00 ppl=14.25 best_loss=2.6713e+00 best_ppl=14.46                                              
Epoch 26 - |param|=6.09e+02 |g_param|=1.56e+05 loss=2.9592e+00 ppl=19.28                                                
Validation - loss=2.6187e+00 ppl=13.72 best_loss=2.6566e+00 best_ppl=14.25                                              
Epoch 27 - |param|=6.10e+02 |g_param|=1.48e+05 loss=2.8155e+00 ppl=16.70                                                
Validation - loss=2.5866e+00 ppl=13.28 best_loss=2.6187e+00 best_ppl=13.72                                              
Epoch 28 - |param|=6.10e+02 |g_param|=1.57e+05 loss=2.7734e+00 ppl=16.01                                                
Validation - loss=2.5666e+00 ppl=13.02 best_loss=2.5866e+00 best_ppl=13.28                                              
Epoch 29 - |param|=6.11e+02 |g_param|=1.53e+05 loss=2.8031e+00 ppl=16.50                                                
Validation - loss=2.5365e+00 ppl=12.64 best_loss=2.5666e+00 best_ppl=13.02                                              
Epoch 30 - |param|=6.11e+02 |g_param|=1.69e+05 loss=2.7295e+00 ppl=15.33                                                
Validation - loss=2.5086e+00 ppl=12.29 best_loss=2.5365e+00 best_ppl=12.64                                              
Epoch 31 - |param|=6.11e+02 |g_param|=1.66e+05 loss=2.6866e+00 ppl=14.68                                                
Validation - loss=2.4812e+00 ppl=11.96 best_loss=2.5086e+00 best_ppl=12.29                                              
Epoch 32 - |param|=6.12e+02 |g_param|=1.68e+05 loss=2.6123e+00 ppl=13.63                                                
Validation - loss=2.4462e+00 ppl=11.54 best_loss=2.4812e+00 best_ppl=11.96                                              
Epoch 33 - |param|=6.12e+02 |g_param|=1.63e+05 loss=2.5846e+00 ppl=13.26                                                
Validation - loss=2.4160e+00 ppl=11.20 best_loss=2.4462e+00 best_ppl=11.54                                              
Epoch 34 - |param|=6.13e+02 |g_param|=3.32e+05 loss=2.6263e+00 ppl=13.82                                                
Validation - loss=2.4020e+00 ppl=11.05 best_loss=2.4160e+00 best_ppl=11.20                                              
Epoch 35 - |param|=6.13e+02 |g_param|=3.24e+05 loss=2.5072e+00 ppl=12.27                                                
Validation - loss=2.3667e+00 ppl=10.66 best_loss=2.4020e+00 best_ppl=11.05                                              
Epoch 36 - |param|=6.14e+02 |g_param|=3.42e+05 loss=2.4872e+00 ppl=12.03                                                
Validation - loss=2.3724e+00 ppl=10.72 best_loss=2.3667e+00 best_ppl=10.66                                              
Epoch 37 - |param|=6.14e+02 |g_param|=3.52e+05 loss=2.4504e+00 ppl=11.59                                                
Validation - loss=2.3285e+00 ppl=10.26 best_loss=2.3667e+00 best_ppl=10.66                                              
Epoch 38 - |param|=6.15e+02 |g_param|=3.87e+05 loss=2.4685e+00 ppl=11.80                                                
Validation - loss=2.3106e+00 ppl=10.08 best_loss=2.3285e+00 best_ppl=10.26                                              
Epoch 39 - |param|=6.15e+02 |g_param|=3.63e+05 loss=2.4875e+00 ppl=12.03                                                
Validation - loss=2.3081e+00 ppl=10.06 best_loss=2.3106e+00 best_ppl=10.08                                              
Epoch 40 - |param|=6.16e+02 |g_param|=3.77e+05 loss=2.4473e+00 ppl=11.56                                                
Validation - loss=2.3102e+00 ppl=10.08 best_loss=2.3081e+00 best_ppl=10.06                                              
Epoch 41 - |param|=6.16e+02 |g_param|=3.82e+05 loss=2.4025e+00 ppl=11.05                                                
Validation - loss=2.2973e+00 ppl=9.95 best_loss=2.3081e+00 best_ppl=10.06                                               
Epoch 42 - |param|=6.17e+02 |g_param|=3.79e+05 loss=2.2405e+00 ppl=9.40                                                 
Validation - loss=2.2576e+00 ppl=9.56 best_loss=2.2973e+00 best_ppl=9.95                                                
Epoch 43 - |param|=6.17e+02 |g_param|=3.68e+05 loss=2.2515e+00 ppl=9.50                                                 
Validation - loss=2.2452e+00 ppl=9.44 best_loss=2.2576e+00 best_ppl=9.56                                                
Epoch 44 - |param|=6.18e+02 |g_param|=3.94e+05 loss=2.2012e+00 ppl=9.04                                                 
Validation - loss=2.2426e+00 ppl=9.42 best_loss=2.2452e+00 best_ppl=9.44                                                
Epoch 45 - |param|=6.18e+02 |g_param|=3.90e+05 loss=2.2155e+00 ppl=9.17                                                 
Validation - loss=2.2179e+00 ppl=9.19 best_loss=2.2426e+00 best_ppl=9.42                                                
Epoch 46 - |param|=6.19e+02 |g_param|=3.98e+05 loss=2.1933e+00 ppl=8.96                                                 
Validation - loss=2.2043e+00 ppl=9.06 best_loss=2.2179e+00 best_ppl=9.19                                                
Epoch 47 - |param|=6.19e+02 |g_param|=4.23e+05 loss=2.1949e+00 ppl=8.98                                                 
Validation - loss=2.2048e+00 ppl=9.07 best_loss=2.2043e+00 best_ppl=9.06                                                
Epoch 48 - |param|=6.19e+02 |g_param|=4.18e+05 loss=2.0881e+00 ppl=8.07                                                 
Validation - loss=2.2028e+00 ppl=9.05 best_loss=2.2043e+00 best_ppl=9.06                                                
Epoch 49 - |param|=6.20e+02 |g_param|=4.00e+05 loss=2.0712e+00 ppl=7.93                                                 
Validation - loss=2.1868e+00 ppl=8.91 best_loss=2.2028e+00 best_ppl=9.05                                                
Epoch 50 - |param|=6.20e+02 |g_param|=4.68e+05 loss=2.1152e+00 ppl=8.29                                                 
Validation - loss=2.1664e+00 ppl=8.73 best_loss=2.1868e+00 best_ppl=8.91                                                
Epoch 51 - |param|=6.21e+02 |g_param|=4.46e+05 loss=2.1043e+00 ppl=8.20                                                 
Validation - loss=2.1766e+00 ppl=8.82 best_loss=2.1664e+00 best_ppl=8.73                                                
Epoch 52 - |param|=6.21e+02 |g_param|=4.34e+05 loss=2.0109e+00 ppl=7.47                                                 
Validation - loss=2.1415e+00 ppl=8.51 best_loss=2.1664e+00 best_ppl=8.73                                                
Epoch 53 - |param|=6.22e+02 |g_param|=4.32e+05 loss=1.9358e+00 ppl=6.93                                                 
Validation - loss=2.1707e+00 ppl=8.76 best_loss=2.1415e+00 best_ppl=8.51                                                
Epoch 54 - |param|=6.22e+02 |g_param|=4.33e+05 loss=1.9718e+00 ppl=7.18                                                 
Validation - loss=2.1432e+00 ppl=8.53 best_loss=2.1415e+00 best_ppl=8.51                                                
Epoch 55 - |param|=6.23e+02 |g_param|=4.18e+05 loss=1.8842e+00 ppl=6.58                                                 
Validation - loss=2.1293e+00 ppl=8.41 best_loss=2.1415e+00 best_ppl=8.51                                                
Epoch 56 - |param|=6.23e+02 |g_param|=4.51e+05 loss=1.8979e+00 ppl=6.67                                                 
Validation - loss=2.1295e+00 ppl=8.41 best_loss=2.1293e+00 best_ppl=8.41                                                
Epoch 57 - |param|=6.23e+02 |g_param|=4.64e+05 loss=1.9497e+00 ppl=7.03                                                 
Validation - loss=2.1349e+00 ppl=8.46 best_loss=2.1293e+00 best_ppl=8.41                                                
Epoch 58 - |param|=6.24e+02 |g_param|=4.69e+05 loss=1.8234e+00 ppl=6.19                                                 
Validation - loss=2.1280e+00 ppl=8.40 best_loss=2.1293e+00 best_ppl=8.41                                                
Epoch 59 - |param|=6.24e+02 |g_param|=4.49e+05 loss=1.7958e+00 ppl=6.02                                                 
Validation - loss=2.1213e+00 ppl=8.34 best_loss=2.1280e+00 best_ppl=8.40                                                
Epoch 60 - |param|=6.25e+02 |g_param|=4.69e+05 loss=1.8134e+00 ppl=6.13                                                 
Validation - loss=2.1103e+00 ppl=8.25 best_loss=2.1213e+00 best_ppl=8.34                                                
Epoch 61 - |param|=6.25e+02 |g_param|=4.57e+05 loss=1.7411e+00 ppl=5.70                                                 
Validation - loss=2.0984e+00 ppl=8.15 best_loss=2.1103e+00 best_ppl=8.25                                                
Epoch 62 - |param|=6.26e+02 |g_param|=5.23e+05 loss=1.7246e+00 ppl=5.61                                                 
Validation - loss=2.1191e+00 ppl=8.32 best_loss=2.0984e+00 best_ppl=8.15                                                
Epoch 63 - |param|=6.26e+02 |g_param|=4.90e+05 loss=1.8184e+00 ppl=6.16                                                 
Validation - loss=2.1026e+00 ppl=8.19 best_loss=2.0984e+00 best_ppl=8.15                                                
Epoch 64 - |param|=6.26e+02 |g_param|=4.95e+05 loss=1.7018e+00 ppl=5.48                                                 
Validation - loss=2.0887e+00 ppl=8.07 best_loss=2.0984e+00 best_ppl=8.15                                                
Epoch 65 - |param|=6.27e+02 |g_param|=5.04e+05 loss=1.8368e+00 ppl=6.28                                                 
Validation - loss=2.1053e+00 ppl=8.21 best_loss=2.0887e+00 best_ppl=8.07                                                
Epoch 66 - |param|=6.27e+02 |g_param|=7.45e+05 loss=1.6616e+00 ppl=5.27                                                 
Validation - loss=2.1118e+00 ppl=8.26 best_loss=2.0887e+00 best_ppl=8.07                                                
Epoch 67 - |param|=6.28e+02 |g_param|=7.24e+05 loss=1.7125e+00 ppl=5.54                                                 
Validation - loss=2.0842e+00 ppl=8.04 best_loss=2.0887e+00 best_ppl=8.07                                                
Epoch 68 - |param|=6.28e+02 |g_param|=5.11e+05 loss=1.7545e+00 ppl=5.78                                                 
Validation - loss=2.1153e+00 ppl=8.29 best_loss=2.0842e+00 best_ppl=8.04                                                
Epoch 69 - |param|=6.28e+02 |g_param|=4.90e+05 loss=1.6176e+00 ppl=5.04                                                 
Validation - loss=2.0986e+00 ppl=8.15 best_loss=2.0842e+00 best_ppl=8.04                                                
Epoch 70 - |param|=6.29e+02 |g_param|=4.97e+05 loss=1.5501e+00 ppl=4.71                                                 
Validation - loss=2.1237e+00 ppl=8.36 best_loss=2.0842e+00 best_ppl=8.04                                                

real	14m31.058s
user	14m14.082s
sys	0m17.880s

real	83m35.000s
user	82m6.299s
sys	1m35.128s
```

## Testing/Evaluation for Seq2Seq Baseline

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Last updated: 3 April 2022
# A part of Seq2Seq-Reinforcement Learning exp
# this script is for testing/evaluation of baseline seq2seq for both Myanmar-Beik and Beik-Myanmar

# testing/evaluation baseline for my-bk

for folder in {30,40,50,60,70};
do
   cd ./model/rl2/baseline/seq2seq/mybk-${folder}epoch/;
   pwd;
   for i in *.pth; do
      MODEL=$i;

      # Testing
      python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang mybk < /home/ye/exp/simple-nmt/data/my-bk/syl/test.my > ./$MODEL.hyp

      # Evaluation with BLEU Score
      echo "Evaluation result for the model: $MODEL" | tee -a eval-results-mybk-seq2seq-baseline-100epoch.txt;
      cat ./$MODEL.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/my-bk/syl/test.bk | tee  -a eval-results-mybk-seq2seq-baseline-100epoch.txt;

   done
   cd -; echo "==========";
done

# testing/evaluation baseline for bk-my
for folder in {30,40,50,60,70};
do
   cd ./model/rl2/baseline/seq2seq/bkmy-${folder}epoch/;
   pwd;
   for i in *.pth; do
      MODEL=$i;

      # Testing
      python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang bkmy < /home/ye/exp/simple-nmt/data/my-bk/syl/test.bk > ./$MODEL.hyp

      # Evaluation with BLEU Score
      echo "Evaluation result for the model: $MODEL" | tee -a eval-results-bkmy-seq2seq-baseline-100epoch.txt;
      cat ./$MODEL.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/my-bk/syl/test.my | tee  -a eval-results-bkmy-seq2seq-baseline-100epoch.txt;

   done
   cd -; echo "==========";
done

```

testing/evaluation ....   

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-rl2-seq2seq-baseline-mybk-bkmy.sh | tee test-eval-rl2-seq2seq-baseline-mybk-bkmy.log
/home/ye/exp/simple-nmt/model/rl2/baseline/seq2seq/mybk-30epoch
Evaluation result for the model: seq-model-mybk.01.4.93-137.87.4.09-59.52.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.4/0.0/0.0/0.0 (BP=0.924, ratio=0.927, hyp_len=10599, ref_len=11432)
Evaluation result for the model: seq-model-mybk.02.4.42-82.91.3.95-51.84.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.2/0.1/0.0/0.0 (BP=1.000, ratio=1.041, hyp_len=11898, ref_len=11432)
Evaluation result for the model: seq-model-mybk.03.4.38-79.60.3.84-46.55.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.5/0.2/0.0/0.0 (BP=0.981, ratio=0.981, hyp_len=11220, ref_len=11432)
Evaluation result for the model: seq-model-mybk.04.4.35-77.52.3.86-47.67.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.2/0.2/0.0/0.0 (BP=1.000, ratio=1.063, hyp_len=12149, ref_len=11432)
Evaluation result for the model: seq-model-mybk.05.4.36-78.59.3.89-48.69.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.4/0.3/0.0/0.0 (BP=0.966, ratio=0.966, hyp_len=11048, ref_len=11432)
Evaluation result for the model: seq-model-mybk.06.4.26-70.77.3.81-45.06.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.1/0.3/0.0/0.0 (BP=1.000, ratio=1.008, hyp_len=11526, ref_len=11432)
Evaluation result for the model: seq-model-mybk.07.4.36-77.94.3.81-44.96.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.4/0.4/0.0/0.0 (BP=0.962, ratio=0.963, hyp_len=11004, ref_len=11432)
Evaluation result for the model: seq-model-mybk.08.4.27-71.74.3.76-43.16.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 14.8/0.6/0.0/0.0 (BP=1.000, ratio=1.084, hyp_len=12396, ref_len=11432)
Evaluation result for the model: seq-model-mybk.09.4.24-69.21.3.75-42.34.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.5/0.9/0.0/0.0 (BP=1.000, ratio=1.091, hyp_len=12475, ref_len=11432)
Evaluation result for the model: seq-model-mybk.10.4.19-66.16.3.67-39.42.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.7/0.5/0.0/0.0 (BP=0.914, ratio=0.918, hyp_len=10492, ref_len=11432)
Evaluation result for the model: seq-model-mybk.11.4.05-57.30.3.44-31.24.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 23.5/1.1/0.1/0.0 (BP=0.780, ratio=0.801, hyp_len=9159, ref_len=11432)
Evaluation result for the model: seq-model-mybk.12.3.89-48.81.3.42-30.67.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.9/3.4/0.7/0.0 (BP=1.000, ratio=1.012, hyp_len=11573, ref_len=11432)
Evaluation result for the model: seq-model-mybk.13.3.76-42.96.3.30-27.18.pth
BLEU = 1.38, 23.1/4.3/1.0/0.0 (BP=1.000, ratio=1.006, hyp_len=11503, ref_len=11432)
Evaluation result for the model: seq-model-mybk.14.3.69-39.88.3.25-25.73.pth
BLEU = 3.31, 23.8/5.6/1.7/0.5 (BP=1.000, ratio=1.054, hyp_len=12045, ref_len=11432)
Evaluation result for the model: seq-model-mybk.15.3.63-37.82.3.14-23.04.pth
BLEU = 3.53, 23.1/5.9/1.9/0.6 (BP=1.000, ratio=1.108, hyp_len=12662, ref_len=11432)
Evaluation result for the model: seq-model-mybk.16.3.61-36.85.3.11-22.44.pth
BLEU = 1.29, 8.8/2.2/0.7/0.2 (BP=1.000, ratio=2.903, hyp_len=33190, ref_len=11432)
Evaluation result for the model: seq-model-mybk.17.3.56-35.02.3.02-20.57.pth
BLEU = 3.80, 22.4/5.8/2.1/0.8 (BP=1.000, ratio=1.206, hyp_len=13784, ref_len=11432)
Evaluation result for the model: seq-model-mybk.18.3.33-28.07.2.93-18.64.pth
BLEU = 4.93, 27.3/7.7/2.8/1.0 (BP=1.000, ratio=1.033, hyp_len=11809, ref_len=11432)
Evaluation result for the model: seq-model-mybk.19.3.29-26.81.2.88-17.86.pth
BLEU = 3.03, 17.2/4.8/1.7/0.6 (BP=1.000, ratio=1.658, hyp_len=18958, ref_len=11432)
Evaluation result for the model: seq-model-mybk.20.3.30-26.98.2.80-16.42.pth
BLEU = 4.24, 21.9/6.6/2.5/0.9 (BP=1.000, ratio=1.368, hyp_len=15639, ref_len=11432)
Evaluation result for the model: seq-model-mybk.21.3.21-24.89.2.78-16.16.pth
BLEU = 3.25, 16.4/4.9/1.9/0.7 (BP=1.000, ratio=1.769, hyp_len=20219, ref_len=11432)
Evaluation result for the model: seq-model-mybk.22.3.16-23.52.2.69-14.70.pth
BLEU = 5.05, 24.3/7.8/3.0/1.2 (BP=1.000, ratio=1.232, hyp_len=14083, ref_len=11432)
Evaluation result for the model: seq-model-mybk.23.3.08-21.84.2.66-14.25.pth
BLEU = 5.83, 26.8/8.8/3.5/1.4 (BP=1.000, ratio=1.154, hyp_len=13189, ref_len=11432)
Evaluation result for the model: seq-model-mybk.24.3.07-21.60.2.61-13.60.pth
BLEU = 5.54, 24.6/8.2/3.4/1.4 (BP=1.000, ratio=1.315, hyp_len=15037, ref_len=11432)
Evaluation result for the model: seq-model-mybk.25.2.99-19.97.2.59-13.30.pth
BLEU = 7.29, 30.1/10.6/4.5/2.0 (BP=1.000, ratio=1.137, hyp_len=13002, ref_len=11432)
Evaluation result for the model: seq-model-mybk.26.3.00-20.06.2.55-12.84.pth
BLEU = 7.57, 29.6/11.0/4.9/2.1 (BP=1.000, ratio=1.163, hyp_len=13301, ref_len=11432)
Evaluation result for the model: seq-model-mybk.27.2.90-18.17.2.51-12.24.pth
BLEU = 8.03, 31.3/11.5/5.1/2.3 (BP=1.000, ratio=1.092, hyp_len=12484, ref_len=11432)
Evaluation result for the model: seq-model-mybk.28.2.87-17.69.2.45-11.55.pth
BLEU = 8.11, 31.2/11.8/5.2/2.3 (BP=1.000, ratio=1.129, hyp_len=12912, ref_len=11432)
Evaluation result for the model: seq-model-mybk.29.2.81-16.61.2.43-11.34.pth
BLEU = 8.91, 33.9/12.9/5.8/2.5 (BP=1.000, ratio=1.100, hyp_len=12574, ref_len=11432)
Evaluation result for the model: seq-model-mybk.30.2.80-16.52.2.38-10.84.pth
BLEU = 9.36, 33.3/13.2/6.1/2.9 (BP=1.000, ratio=1.119, hyp_len=12789, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/baseline/seq2seq/mybk-40epoch
Evaluation result for the model: seq-model-mybk.01.4.89-132.53.4.02-55.92.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 24.0/0.0/0.0/0.0 (BP=0.533, ratio=0.614, hyp_len=7019, ref_len=11432)
Evaluation result for the model: seq-model-mybk.02.4.41-82.49.3.87-48.17.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.7/0.0/0.0/0.0 (BP=0.913, ratio=0.917, hyp_len=10481, ref_len=11432)
Evaluation result for the model: seq-model-mybk.03.4.45-86.03.3.85-46.99.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.6/0.2/0.0/0.0 (BP=0.991, ratio=0.991, hyp_len=11326, ref_len=11432)
Evaluation result for the model: seq-model-mybk.04.4.33-75.66.3.82-45.62.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.6/0.1/0.0/0.0 (BP=0.991, ratio=0.991, hyp_len=11329, ref_len=11432)
Evaluation result for the model: seq-model-mybk.05.4.34-76.95.3.82-45.68.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.7/0.2/0.0/0.0 (BP=0.936, ratio=0.938, hyp_len=10718, ref_len=11432)
Evaluation result for the model: seq-model-mybk.06.4.31-74.33.3.83-46.01.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.2/0.0/0.0/0.0 (BP=1.000, ratio=1.063, hyp_len=12152, ref_len=11432)
Evaluation result for the model: seq-model-mybk.07.4.28-71.98.3.82-45.42.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.8/0.3/0.0/0.0 (BP=1.000, ratio=1.070, hyp_len=12227, ref_len=11432)
Evaluation result for the model: seq-model-mybk.08.4.27-71.82.3.75-42.45.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.8/0.2/0.0/0.0 (BP=0.979, ratio=0.979, hyp_len=11191, ref_len=11432)
Evaluation result for the model: seq-model-mybk.09.4.22-68.22.3.72-41.47.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.3/0.4/0.0/0.0 (BP=1.000, ratio=1.000, hyp_len=11435, ref_len=11432)
Evaluation result for the model: seq-model-mybk.10.4.25-69.83.3.70-40.47.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.8/0.8/0.0/0.0 (BP=0.999, ratio=0.999, hyp_len=11421, ref_len=11432)
Evaluation result for the model: seq-model-mybk.11.4.22-67.73.3.67-39.31.pth
BLEU = 0.54, 18.1/0.9/0.2/0.0 (BP=1.000, ratio=1.046, hyp_len=11954, ref_len=11432)
Evaluation result for the model: seq-model-mybk.12.4.09-59.73.3.62-37.45.pth
BLEU = 1.44, 20.4/1.5/0.7/0.2 (BP=0.974, ratio=0.974, hyp_len=11137, ref_len=11432)
Evaluation result for the model: seq-model-mybk.13.3.99-54.11.3.40-29.95.pth
BLEU = 1.06, 23.2/2.7/0.9/0.0 (BP=0.861, ratio=0.870, hyp_len=9943, ref_len=11432)
Evaluation result for the model: seq-model-mybk.14.3.81-45.13.3.26-26.13.pth
BLEU = 3.18, 25.6/4.7/1.5/0.7 (BP=0.940, ratio=0.942, hyp_len=10766, ref_len=11432)
Evaluation result for the model: seq-model-mybk.15.3.67-39.08.3.19-24.28.pth
BLEU = 1.95, 23.7/4.7/1.1/0.1 (BP=1.000, ratio=1.045, hyp_len=11944, ref_len=11432)
Evaluation result for the model: seq-model-mybk.16.3.60-36.45.3.11-22.46.pth
BLEU = 2.39, 17.9/4.3/1.3/0.3 (BP=1.000, ratio=1.471, hyp_len=16819, ref_len=11432)
Evaluation result for the model: seq-model-mybk.17.3.47-32.21.3.03-20.63.pth
BLEU = 3.93, 26.3/6.8/2.2/0.6 (BP=1.000, ratio=1.029, hyp_len=11764, ref_len=11432)
Evaluation result for the model: seq-model-mybk.18.3.44-31.15.2.98-19.67.pth
BLEU = 2.08, 15.5/4.1/1.2/0.2 (BP=1.000, ratio=1.763, hyp_len=20159, ref_len=11432)
Evaluation result for the model: seq-model-mybk.19.3.37-29.22.2.93-18.65.pth
BLEU = 3.28, 20.0/5.5/1.9/0.6 (BP=1.000, ratio=1.448, hyp_len=16553, ref_len=11432)
Evaluation result for the model: seq-model-mybk.20.3.31-27.41.2.89-18.07.pth
BLEU = 4.53, 25.2/7.2/2.6/0.9 (BP=1.000, ratio=1.149, hyp_len=13138, ref_len=11432)
Evaluation result for the model: seq-model-mybk.21.3.27-26.37.2.87-17.59.pth
BLEU = 5.10, 26.1/7.8/3.0/1.1 (BP=1.000, ratio=1.196, hyp_len=13669, ref_len=11432)
Evaluation result for the model: seq-model-mybk.22.3.27-26.35.2.83-16.91.pth
BLEU = 3.07, 14.9/4.5/1.8/0.7 (BP=1.000, ratio=2.068, hyp_len=23640, ref_len=11432)
Evaluation result for the model: seq-model-mybk.23.3.10-22.13.2.74-15.49.pth
BLEU = 5.96, 28.3/8.6/3.5/1.5 (BP=1.000, ratio=1.081, hyp_len=12360, ref_len=11432)
Evaluation result for the model: seq-model-mybk.24.3.05-21.09.2.68-14.52.pth
BLEU = 7.51, 30.3/10.4/4.7/2.2 (BP=1.000, ratio=1.048, hyp_len=11979, ref_len=11432)
Evaluation result for the model: seq-model-mybk.25.3.11-22.45.2.70-14.89.pth
BLEU = 6.50, 27.6/9.2/4.0/1.8 (BP=1.000, ratio=1.130, hyp_len=12919, ref_len=11432)
Evaluation result for the model: seq-model-mybk.26.2.92-18.52.2.60-13.52.pth
BLEU = 7.83, 30.4/10.7/4.9/2.4 (BP=1.000, ratio=1.109, hyp_len=12676, ref_len=11432)
Evaluation result for the model: seq-model-mybk.27.2.94-18.94.2.56-12.99.pth
BLEU = 8.41, 32.2/11.9/5.3/2.5 (BP=1.000, ratio=1.093, hyp_len=12499, ref_len=11432)
Evaluation result for the model: seq-model-mybk.28.2.90-18.17.2.52-12.39.pth
BLEU = 8.46, 32.4/12.0/5.4/2.5 (BP=1.000, ratio=1.087, hyp_len=12424, ref_len=11432)
Evaluation result for the model: seq-model-mybk.29.2.76-15.76.2.49-12.08.pth
BLEU = 8.47, 31.6/11.8/5.4/2.5 (BP=1.000, ratio=1.175, hyp_len=13435, ref_len=11432)
Evaluation result for the model: seq-model-mybk.30.2.79-16.30.2.45-11.61.pth
BLEU = 9.30, 33.3/12.8/6.0/2.9 (BP=1.000, ratio=1.063, hyp_len=12148, ref_len=11432)
Evaluation result for the model: seq-model-mybk.31.2.76-15.85.2.42-11.24.pth
BLEU = 10.69, 35.9/14.4/7.2/3.5 (BP=1.000, ratio=1.056, hyp_len=12070, ref_len=11432)
Evaluation result for the model: seq-model-mybk.32.2.63-13.91.2.42-11.30.pth
BLEU = 9.92, 32.6/13.2/6.6/3.4 (BP=1.000, ratio=1.178, hyp_len=13467, ref_len=11432)
Evaluation result for the model: seq-model-mybk.33.2.66-14.29.2.36-10.60.pth
BLEU = 10.34, 33.8/13.8/6.9/3.6 (BP=1.000, ratio=1.152, hyp_len=13171, ref_len=11432)
Evaluation result for the model: seq-model-mybk.34.2.58-13.18.2.32-10.15.pth
BLEU = 11.82, 37.1/15.8/8.0/4.2 (BP=1.000, ratio=1.071, hyp_len=12246, ref_len=11432)
Evaluation result for the model: seq-model-mybk.35.2.59-13.34.2.27-9.71.pth
BLEU = 12.98, 39.0/17.0/8.8/4.9 (BP=1.000, ratio=1.062, hyp_len=12144, ref_len=11432)
Evaluation result for the model: seq-model-mybk.36.2.57-13.01.2.26-9.60.pth
BLEU = 12.86, 38.5/16.9/8.9/4.7 (BP=1.000, ratio=1.058, hyp_len=12093, ref_len=11432)
Evaluation result for the model: seq-model-mybk.37.2.54-12.71.2.24-9.40.pth
BLEU = 13.64, 39.4/17.7/9.5/5.2 (BP=1.000, ratio=1.040, hyp_len=11893, ref_len=11432)
Evaluation result for the model: seq-model-mybk.38.2.46-11.65.2.20-8.99.pth
BLEU = 14.06, 40.3/18.4/9.8/5.4 (BP=1.000, ratio=1.055, hyp_len=12056, ref_len=11432)
Evaluation result for the model: seq-model-mybk.39.2.38-10.80.2.20-9.06.pth
BLEU = 13.93, 39.3/18.1/9.8/5.4 (BP=1.000, ratio=1.076, hyp_len=12303, ref_len=11432)
Evaluation result for the model: seq-model-mybk.40.2.49-12.05.2.17-8.77.pth
BLEU = 14.15, 39.7/18.2/9.9/5.6 (BP=1.000, ratio=1.093, hyp_len=12492, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/baseline/seq2seq/mybk-50epoch
Evaluation result for the model: seq-model-mybk.01.4.87-130.05.4.05-57.21.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.6/0.3/0.0/0.0 (BP=0.984, ratio=0.985, hyp_len=11255, ref_len=11432)
Evaluation result for the model: seq-model-mybk.02.4.44-84.85.3.84-46.31.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.8/0.1/0.0/0.0 (BP=1.000, ratio=1.004, hyp_len=11474, ref_len=11432)
Evaluation result for the model: seq-model-mybk.03.4.36-78.14.3.89-48.82.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.5/0.3/0.0/0.0 (BP=1.000, ratio=1.037, hyp_len=11857, ref_len=11432)
Evaluation result for the model: seq-model-mybk.04.4.34-77.02.3.82-45.59.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.1/0.1/0.0/0.0 (BP=1.000, ratio=1.026, hyp_len=11732, ref_len=11432)
Evaluation result for the model: seq-model-mybk.05.4.30-73.39.3.87-47.71.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.8/0.3/0.0/0.0 (BP=1.000, ratio=1.034, hyp_len=11821, ref_len=11432)
Evaluation result for the model: seq-model-mybk.06.4.35-77.85.3.78-43.94.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.4/0.1/0.0/0.0 (BP=1.000, ratio=1.058, hyp_len=12099, ref_len=11432)
Evaluation result for the model: seq-model-mybk.07.4.29-72.81.3.79-44.05.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.0/0.4/0.0/0.0 (BP=1.000, ratio=1.008, hyp_len=11526, ref_len=11432)
Evaluation result for the model: seq-model-mybk.08.4.31-74.19.3.74-42.30.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.6/0.3/0.0/0.0 (BP=1.000, ratio=1.026, hyp_len=11725, ref_len=11432)
Evaluation result for the model: seq-model-mybk.09.4.26-70.73.3.76-42.89.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.5/0.6/0.0/0.0 (BP=1.000, ratio=1.075, hyp_len=12284, ref_len=11432)
Evaluation result for the model: seq-model-mybk.10.4.27-71.43.3.68-39.76.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.8/1.2/0.2/0.0 (BP=1.000, ratio=1.075, hyp_len=12286, ref_len=11432)
Evaluation result for the model: seq-model-mybk.11.4.07-58.62.3.58-36.00.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.9/0.8/0.0/0.0 (BP=0.922, ratio=0.925, hyp_len=10575, ref_len=11432)
Evaluation result for the model: seq-model-mybk.12.3.99-54.03.3.39-29.53.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 24.0/3.3/0.3/0.0 (BP=0.959, ratio=0.960, hyp_len=10977, ref_len=11432)
Evaluation result for the model: seq-model-mybk.13.3.76-43.10.3.27-26.21.pth
BLEU = 1.20, 24.9/5.5/1.3/0.0 (BP=0.966, ratio=0.967, hyp_len=11055, ref_len=11432)
Evaluation result for the model: seq-model-mybk.14.3.71-40.70.3.21-24.78.pth
BLEU = 2.30, 25.7/6.0/1.7/0.1 (BP=0.966, ratio=0.966, hyp_len=11049, ref_len=11432)
Evaluation result for the model: seq-model-mybk.15.3.61-37.00.3.14-23.18.pth
BLEU = 3.95, 26.8/7.0/2.2/0.6 (BP=0.989, ratio=0.989, hyp_len=11308, ref_len=11432)
Evaluation result for the model: seq-model-mybk.16.3.63-37.84.3.12-22.59.pth
BLEU = 4.00, 24.9/6.4/2.1/0.7 (BP=1.000, ratio=1.068, hyp_len=12208, ref_len=11432)
Evaluation result for the model: seq-model-mybk.17.3.49-32.86.3.08-21.73.pth
BLEU = 4.25, 24.7/6.9/2.3/0.8 (BP=1.000, ratio=1.102, hyp_len=12603, ref_len=11432)
Evaluation result for the model: seq-model-mybk.18.3.51-33.57.3.04-20.90.pth
BLEU = 4.14, 25.1/6.9/2.1/0.8 (BP=1.000, ratio=1.088, hyp_len=12435, ref_len=11432)
Evaluation result for the model: seq-model-mybk.19.3.38-29.38.2.99-19.83.pth
BLEU = 4.48, 25.7/7.4/2.5/0.9 (BP=1.000, ratio=1.117, hyp_len=12768, ref_len=11432)
Evaluation result for the model: seq-model-mybk.20.3.39-29.55.2.95-19.04.pth
BLEU = 5.03, 26.7/8.1/2.8/1.0 (BP=1.000, ratio=1.083, hyp_len=12380, ref_len=11432)
Evaluation result for the model: seq-model-mybk.21.3.38-29.40.2.94-18.99.pth
BLEU = 2.36, 13.2/3.8/1.3/0.5 (BP=1.000, ratio=2.145, hyp_len=24523, ref_len=11432)
Evaluation result for the model: seq-model-mybk.22.3.32-27.53.2.87-17.57.pth
BLEU = 3.43, 17.8/5.4/2.0/0.7 (BP=1.000, ratio=1.630, hyp_len=18633, ref_len=11432)
Evaluation result for the model: seq-model-mybk.23.3.22-25.10.2.86-17.54.pth
BLEU = 4.90, 24.7/7.7/2.9/1.0 (BP=1.000, ratio=1.209, hyp_len=13827, ref_len=11432)
Evaluation result for the model: seq-model-mybk.24.3.14-23.21.2.81-16.56.pth
BLEU = 4.53, 22.4/7.2/2.7/1.0 (BP=1.000, ratio=1.356, hyp_len=15499, ref_len=11432)
Evaluation result for the model: seq-model-mybk.25.3.07-21.53.2.76-15.87.pth
BLEU = 5.14, 25.2/8.3/3.1/1.1 (BP=1.000, ratio=1.193, hyp_len=13643, ref_len=11432)
Evaluation result for the model: seq-model-mybk.26.3.01-20.19.2.75-15.60.pth
BLEU = 5.93, 27.8/9.2/3.6/1.4 (BP=1.000, ratio=1.106, hyp_len=12640, ref_len=11432)
Evaluation result for the model: seq-model-mybk.27.3.01-20.34.2.69-14.76.pth
BLEU = 5.76, 27.9/9.0/3.4/1.3 (BP=1.000, ratio=1.111, hyp_len=12699, ref_len=11432)
Evaluation result for the model: seq-model-mybk.28.2.95-19.07.2.69-14.79.pth
BLEU = 6.50, 29.3/10.1/4.0/1.5 (BP=1.000, ratio=1.089, hyp_len=12450, ref_len=11432)
Evaluation result for the model: seq-model-mybk.29.2.93-18.69.2.70-14.89.pth
BLEU = 6.13, 27.3/9.4/3.7/1.5 (BP=1.000, ratio=1.168, hyp_len=13348, ref_len=11432)
Evaluation result for the model: seq-model-mybk.30.2.92-18.49.2.68-14.57.pth
BLEU = 6.66, 29.7/10.3/4.0/1.6 (BP=1.000, ratio=1.092, hyp_len=12485, ref_len=11432)
Evaluation result for the model: seq-model-mybk.31.2.86-17.41.2.64-13.95.pth
BLEU = 6.64, 29.6/10.0/4.0/1.7 (BP=1.000, ratio=1.081, hyp_len=12360, ref_len=11432)
Evaluation result for the model: seq-model-mybk.32.2.80-16.51.2.63-13.93.pth
BLEU = 6.75, 27.8/9.8/4.1/1.9 (BP=1.000, ratio=1.182, hyp_len=13518, ref_len=11432)
Evaluation result for the model: seq-model-mybk.33.2.75-15.69.2.62-13.69.pth
BLEU = 7.78, 31.9/11.6/4.8/2.1 (BP=1.000, ratio=1.086, hyp_len=12416, ref_len=11432)
Evaluation result for the model: seq-model-mybk.34.2.72-15.15.2.60-13.50.pth
BLEU = 7.83, 30.7/11.3/4.8/2.3 (BP=1.000, ratio=1.107, hyp_len=12651, ref_len=11432)
Evaluation result for the model: seq-model-mybk.35.2.70-14.94.2.58-13.19.pth
BLEU = 8.44, 32.7/12.2/5.3/2.4 (BP=1.000, ratio=1.096, hyp_len=12532, ref_len=11432)
Evaluation result for the model: seq-model-mybk.36.2.65-14.22.2.54-12.62.pth
BLEU = 9.22, 33.8/13.0/5.9/2.8 (BP=1.000, ratio=1.069, hyp_len=12220, ref_len=11432)
Evaluation result for the model: seq-model-mybk.37.2.63-13.82.2.57-13.04.pth
BLEU = 9.31, 33.8/12.8/6.0/2.9 (BP=1.000, ratio=1.046, hyp_len=11961, ref_len=11432)
Evaluation result for the model: seq-model-mybk.38.2.62-13.69.2.57-13.12.pth
BLEU = 8.94, 33.7/12.9/5.7/2.6 (BP=1.000, ratio=1.100, hyp_len=12575, ref_len=11432)
Evaluation result for the model: seq-model-mybk.39.2.56-12.96.2.53-12.54.pth
BLEU = 9.26, 33.3/13.0/5.9/2.9 (BP=1.000, ratio=1.100, hyp_len=12578, ref_len=11432)
Evaluation result for the model: seq-model-mybk.40.2.57-13.05.2.51-12.33.pth
BLEU = 10.09, 35.6/14.2/6.6/3.1 (BP=1.000, ratio=1.064, hyp_len=12158, ref_len=11432)
Evaluation result for the model: seq-model-mybk.41.2.48-11.96.2.54-12.65.pth
BLEU = 9.27, 33.0/12.8/6.0/2.9 (BP=1.000, ratio=1.122, hyp_len=12825, ref_len=11432)
Evaluation result for the model: seq-model-mybk.42.2.42-11.25.2.49-12.06.pth
BLEU = 9.94, 35.0/14.0/6.5/3.1 (BP=1.000, ratio=1.097, hyp_len=12538, ref_len=11432)
Evaluation result for the model: seq-model-mybk.43.2.46-11.67.2.52-12.41.pth
BLEU = 9.98, 34.5/13.6/6.5/3.2 (BP=1.000, ratio=1.074, hyp_len=12281, ref_len=11432)
Evaluation result for the model: seq-model-mybk.44.2.41-11.10.2.50-12.22.pth
BLEU = 10.59, 35.6/14.6/7.0/3.5 (BP=1.000, ratio=1.072, hyp_len=12259, ref_len=11432)
Evaluation result for the model: seq-model-mybk.45.2.36-10.55.2.50-12.13.pth
BLEU = 10.29, 35.4/14.2/6.8/3.3 (BP=1.000, ratio=1.088, hyp_len=12440, ref_len=11432)
Evaluation result for the model: seq-model-mybk.46.2.40-10.99.2.47-11.84.pth
BLEU = 11.16, 37.0/15.2/7.4/3.7 (BP=1.000, ratio=1.060, hyp_len=12121, ref_len=11432)
Evaluation result for the model: seq-model-mybk.47.2.34-10.35.2.48-11.99.pth
BLEU = 11.32, 37.1/15.4/7.6/3.8 (BP=1.000, ratio=1.055, hyp_len=12061, ref_len=11432)
Evaluation result for the model: seq-model-mybk.48.2.30-10.02.2.47-11.87.pth
BLEU = 11.03, 37.0/15.0/7.3/3.7 (BP=1.000, ratio=1.053, hyp_len=12035, ref_len=11432)
Evaluation result for the model: seq-model-mybk.49.2.28-9.79.2.48-11.92.pth
BLEU = 11.25, 36.8/15.3/7.5/3.8 (BP=1.000, ratio=1.070, hyp_len=12234, ref_len=11432)
Evaluation result for the model: seq-model-mybk.50.2.26-9.59.2.46-11.68.pth
BLEU = 11.42, 37.2/15.5/7.6/3.9 (BP=1.000, ratio=1.068, hyp_len=12210, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/baseline/seq2seq/mybk-60epoch
Evaluation result for the model: seq-model-mybk.01.4.89-132.65.4.17-64.56.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.0/0.0/0.0/0.0 (BP=0.879, ratio=0.886, hyp_len=10129, ref_len=11432)
Evaluation result for the model: seq-model-mybk.02.4.49-88.78.3.92-50.36.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.4/0.0/0.0/0.0 (BP=0.994, ratio=0.994, hyp_len=11361, ref_len=11432)
Evaluation result for the model: seq-model-mybk.03.4.38-79.51.3.86-47.29.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.9/0.2/0.0/0.0 (BP=1.000, ratio=1.030, hyp_len=11778, ref_len=11432)
Evaluation result for the model: seq-model-mybk.04.4.46-86.25.3.88-48.64.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.9/0.4/0.0/0.0 (BP=0.890, ratio=0.895, hyp_len=10237, ref_len=11432)
Evaluation result for the model: seq-model-mybk.05.4.34-76.61.3.81-45.25.pth
BLEU = 0.19, 18.6/0.3/0.0/0.0 (BP=0.933, ratio=0.935, hyp_len=10689, ref_len=11432)
Evaluation result for the model: seq-model-mybk.06.4.28-71.91.3.80-44.59.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 14.8/0.6/0.0/0.0 (BP=1.000, ratio=1.065, hyp_len=12177, ref_len=11432)
Evaluation result for the model: seq-model-mybk.07.4.26-70.70.3.79-44.27.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.1/0.3/0.0/0.0 (BP=1.000, ratio=1.029, hyp_len=11767, ref_len=11432)
Evaluation result for the model: seq-model-mybk.08.4.25-69.86.3.73-41.83.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.1/0.6/0.0/0.0 (BP=1.000, ratio=1.015, hyp_len=11601, ref_len=11432)
Evaluation result for the model: seq-model-mybk.09.4.16-64.28.3.66-38.78.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.6/0.9/0.0/0.0 (BP=0.814, ratio=0.829, hyp_len=9482, ref_len=11432)
Evaluation result for the model: seq-model-mybk.10.3.97-53.22.3.46-31.78.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 26.5/2.5/0.1/0.0 (BP=0.854, ratio=0.864, hyp_len=9876, ref_len=11432)
Evaluation result for the model: seq-model-mybk.11.3.81-45.20.3.37-29.20.pth
BLEU = 3.05, 20.7/4.3/1.5/0.6 (BP=1.000, ratio=1.127, hyp_len=12888, ref_len=11432)
Evaluation result for the model: seq-model-mybk.12.3.74-42.25.3.30-27.13.pth
BLEU = 1.17, 21.2/3.1/0.5/0.1 (BP=1.000, ratio=1.027, hyp_len=11746, ref_len=11432)
Evaluation result for the model: seq-model-mybk.13.3.65-38.30.3.24-25.48.pth
BLEU = 1.70, 22.6/4.0/0.7/0.1 (BP=1.000, ratio=1.037, hyp_len=11853, ref_len=11432)
Evaluation result for the model: seq-model-mybk.14.3.69-40.22.3.20-24.65.pth
BLEU = 2.32, 20.3/4.5/1.2/0.3 (BP=1.000, ratio=1.180, hyp_len=13488, ref_len=11432)
Evaluation result for the model: seq-model-mybk.15.3.56-35.13.3.14-23.18.pth
BLEU = 1.91, 21.8/4.7/1.0/0.1 (BP=1.000, ratio=1.105, hyp_len=12627, ref_len=11432)
Evaluation result for the model: seq-model-mybk.16.3.49-32.91.3.10-22.21.pth
BLEU = 3.14, 21.9/5.4/1.6/0.5 (BP=1.000, ratio=1.193, hyp_len=13637, ref_len=11432)
Evaluation result for the model: seq-model-mybk.17.3.40-29.95.3.02-20.41.pth
BLEU = 3.88, 23.2/6.0/2.0/0.8 (BP=1.000, ratio=1.131, hyp_len=12928, ref_len=11432)
Evaluation result for the model: seq-model-mybk.18.3.34-28.31.3.00-20.01.pth
BLEU = 4.01, 22.0/5.9/2.3/0.9 (BP=1.000, ratio=1.222, hyp_len=13972, ref_len=11432)
Evaluation result for the model: seq-model-mybk.19.3.30-27.09.2.96-19.28.pth
BLEU = 3.88, 21.4/5.8/2.2/0.8 (BP=1.000, ratio=1.258, hyp_len=14386, ref_len=11432)
Evaluation result for the model: seq-model-mybk.20.3.25-25.85.2.91-18.32.pth
BLEU = 4.35, 23.6/6.5/2.5/0.9 (BP=1.000, ratio=1.173, hyp_len=13405, ref_len=11432)
Evaluation result for the model: seq-model-mybk.21.3.16-23.55.2.84-17.10.pth
BLEU = 4.54, 24.3/6.8/2.6/1.0 (BP=1.000, ratio=1.159, hyp_len=13254, ref_len=11432)
Evaluation result for the model: seq-model-mybk.22.3.12-22.68.2.83-17.02.pth
BLEU = 4.42, 23.2/6.5/2.5/1.0 (BP=1.000, ratio=1.195, hyp_len=13664, ref_len=11432)
Evaluation result for the model: seq-model-mybk.23.3.16-23.53.2.78-16.15.pth
BLEU = 4.77, 24.7/7.0/2.8/1.1 (BP=1.000, ratio=1.163, hyp_len=13298, ref_len=11432)
Evaluation result for the model: seq-model-mybk.24.3.06-21.26.2.76-15.79.pth
BLEU = 4.20, 21.7/6.5/2.4/0.9 (BP=1.000, ratio=1.339, hyp_len=15311, ref_len=11432)
Evaluation result for the model: seq-model-mybk.25.2.99-19.86.2.75-15.57.pth
BLEU = 3.99, 19.4/5.9/2.4/0.9 (BP=1.000, ratio=1.551, hyp_len=17726, ref_len=11432)
Evaluation result for the model: seq-model-mybk.26.2.94-19.01.2.71-15.04.pth
BLEU = 4.32, 20.9/6.7/2.6/1.0 (BP=1.000, ratio=1.469, hyp_len=16790, ref_len=11432)
Evaluation result for the model: seq-model-mybk.27.2.91-18.33.2.69-14.72.pth
BLEU = 5.76, 25.9/8.8/3.5/1.4 (BP=1.000, ratio=1.189, hyp_len=13595, ref_len=11432)
Evaluation result for the model: seq-model-mybk.28.2.88-17.85.2.68-14.57.pth
BLEU = 3.21, 15.2/5.0/1.9/0.7 (BP=1.000, ratio=2.042, hyp_len=23347, ref_len=11432)
Evaluation result for the model: seq-model-mybk.29.2.81-16.55.2.65-14.14.pth
BLEU = 5.95, 27.0/9.1/3.6/1.4 (BP=1.000, ratio=1.170, hyp_len=13376, ref_len=11432)
Evaluation result for the model: seq-model-mybk.30.2.86-17.48.2.65-14.16.pth
BLEU = 6.86, 29.1/10.1/4.3/1.8 (BP=1.000, ratio=1.114, hyp_len=12731, ref_len=11432)
Evaluation result for the model: seq-model-mybk.31.2.75-15.65.2.65-14.12.pth
BLEU = 5.30, 22.6/8.0/3.3/1.3 (BP=1.000, ratio=1.425, hyp_len=16285, ref_len=11432)
Evaluation result for the model: seq-model-mybk.32.2.71-14.98.2.62-13.79.pth
BLEU = 6.74, 27.8/10.0/4.2/1.8 (BP=1.000, ratio=1.183, hyp_len=13523, ref_len=11432)
Evaluation result for the model: seq-model-mybk.33.2.71-15.03.2.59-13.35.pth
BLEU = 6.85, 27.2/9.9/4.3/1.9 (BP=1.000, ratio=1.189, hyp_len=13596, ref_len=11432)
Evaluation result for the model: seq-model-mybk.34.2.63-13.85.2.59-13.33.pth
BLEU = 6.50, 26.9/9.7/4.1/1.7 (BP=1.000, ratio=1.218, hyp_len=13919, ref_len=11432)
Evaluation result for the model: seq-model-mybk.35.2.68-14.56.2.62-13.71.pth
BLEU = 7.44, 31.0/10.8/4.6/2.0 (BP=1.000, ratio=1.067, hyp_len=12196, ref_len=11432)
Evaluation result for the model: seq-model-mybk.36.2.60-13.47.2.60-13.45.pth
BLEU = 7.59, 28.7/10.7/4.9/2.2 (BP=1.000, ratio=1.157, hyp_len=13227, ref_len=11432)
Evaluation result for the model: seq-model-mybk.37.2.57-13.05.2.58-13.24.pth
BLEU = 8.10, 31.2/11.6/5.2/2.3 (BP=1.000, ratio=1.082, hyp_len=12374, ref_len=11432)
Evaluation result for the model: seq-model-mybk.38.2.57-13.02.2.58-13.26.pth
BLEU = 6.96, 27.4/10.0/4.3/2.0 (BP=1.000, ratio=1.250, hyp_len=14291, ref_len=11432)
Evaluation result for the model: seq-model-mybk.39.2.57-13.05.2.58-13.23.pth
BLEU = 8.16, 31.2/11.6/5.3/2.3 (BP=1.000, ratio=1.095, hyp_len=12515, ref_len=11432)
Evaluation result for the model: seq-model-mybk.40.2.48-11.96.2.61-13.60.pth
BLEU = 8.28, 31.6/12.0/5.3/2.3 (BP=1.000, ratio=1.120, hyp_len=12799, ref_len=11432)
Evaluation result for the model: seq-model-mybk.41.2.46-11.70.2.58-13.24.pth
BLEU = 8.67, 31.8/12.2/5.6/2.6 (BP=1.000, ratio=1.106, hyp_len=12642, ref_len=11432)
Evaluation result for the model: seq-model-mybk.42.2.36-10.55.2.54-12.67.pth
BLEU = 8.72, 32.0/12.3/5.6/2.6 (BP=1.000, ratio=1.107, hyp_len=12650, ref_len=11432)
Evaluation result for the model: seq-model-mybk.43.2.38-10.78.2.56-13.00.pth
BLEU = 8.80, 32.7/12.5/5.7/2.6 (BP=1.000, ratio=1.117, hyp_len=12773, ref_len=11432)
Evaluation result for the model: seq-model-mybk.44.2.42-11.22.2.55-12.82.pth
BLEU = 8.32, 32.2/11.8/5.3/2.4 (BP=1.000, ratio=1.099, hyp_len=12561, ref_len=11432)
Evaluation result for the model: seq-model-mybk.45.2.35-10.46.2.56-12.94.pth
BLEU = 9.45, 33.8/13.2/6.2/2.9 (BP=1.000, ratio=1.069, hyp_len=12221, ref_len=11432)
Evaluation result for the model: seq-model-mybk.46.2.28-9.73.2.58-13.13.pth
BLEU = 8.97, 32.7/12.5/5.8/2.7 (BP=1.000, ratio=1.109, hyp_len=12679, ref_len=11432)
Evaluation result for the model: seq-model-mybk.47.2.29-9.89.2.56-12.97.pth
BLEU = 9.10, 32.8/12.9/5.9/2.8 (BP=1.000, ratio=1.109, hyp_len=12679, ref_len=11432)
Evaluation result for the model: seq-model-mybk.48.2.35-10.53.2.54-12.62.pth
BLEU = 9.45, 33.5/13.2/6.2/2.9 (BP=1.000, ratio=1.070, hyp_len=12231, ref_len=11432)
Evaluation result for the model: seq-model-mybk.49.2.24-9.40.2.56-13.00.pth
BLEU = 9.37, 33.1/13.0/6.1/2.9 (BP=1.000, ratio=1.108, hyp_len=12662, ref_len=11432)
Evaluation result for the model: seq-model-mybk.50.2.19-8.91.2.56-12.87.pth
BLEU = 9.19, 32.5/12.6/6.0/2.9 (BP=1.000, ratio=1.107, hyp_len=12652, ref_len=11432)
Evaluation result for the model: seq-model-mybk.51.2.25-9.53.2.56-12.94.pth
BLEU = 9.93, 34.1/13.7/6.6/3.2 (BP=1.000, ratio=1.072, hyp_len=12256, ref_len=11432)
Evaluation result for the model: seq-model-mybk.52.2.19-8.94.2.58-13.24.pth
BLEU = 9.70, 33.4/13.5/6.4/3.1 (BP=1.000, ratio=1.099, hyp_len=12563, ref_len=11432)
Evaluation result for the model: seq-model-mybk.53.2.14-8.47.2.57-13.13.pth
BLEU = 10.06, 34.2/13.6/6.6/3.3 (BP=1.000, ratio=1.067, hyp_len=12198, ref_len=11432)
Evaluation result for the model: seq-model-mybk.54.2.20-9.06.2.57-13.13.pth
BLEU = 9.78, 33.8/13.6/6.4/3.1 (BP=1.000, ratio=1.101, hyp_len=12588, ref_len=11432)
Evaluation result for the model: seq-model-mybk.55.2.07-7.93.2.58-13.21.pth
BLEU = 9.63, 33.2/12.9/6.2/3.2 (BP=1.000, ratio=1.105, hyp_len=12627, ref_len=11432)
Evaluation result for the model: seq-model-mybk.56.2.06-7.86.2.58-13.25.pth
BLEU = 9.41, 32.5/12.9/6.2/3.0 (BP=1.000, ratio=1.151, hyp_len=13154, ref_len=11432)
Evaluation result for the model: seq-model-mybk.57.2.06-7.84.2.58-13.15.pth
BLEU = 10.29, 34.6/13.9/6.8/3.5 (BP=1.000, ratio=1.089, hyp_len=12446, ref_len=11432)
Evaluation result for the model: seq-model-mybk.58.2.03-7.60.2.60-13.47.pth
BLEU = 10.17, 34.6/13.8/6.6/3.4 (BP=1.000, ratio=1.081, hyp_len=12353, ref_len=11432)
Evaluation result for the model: seq-model-mybk.59.2.00-7.40.2.61-13.63.pth
BLEU = 9.73, 34.4/13.5/6.4/3.0 (BP=1.000, ratio=1.087, hyp_len=12429, ref_len=11432)
Evaluation result for the model: seq-model-mybk.60.2.00-7.42.2.59-13.32.pth
BLEU = 10.25, 34.2/14.0/6.7/3.5 (BP=1.000, ratio=1.100, hyp_len=12576, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/baseline/seq2seq/mybk-70epoch
Evaluation result for the model: seq-model-mybk.01.4.92-136.88.4.10-60.40.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.2/0.2/0.0/0.0 (BP=0.815, ratio=0.830, hyp_len=9488, ref_len=11432)
Evaluation result for the model: seq-model-mybk.02.4.46-86.23.3.90-49.42.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.5/0.2/0.0/0.0 (BP=0.960, ratio=0.960, hyp_len=10979, ref_len=11432)
Evaluation result for the model: seq-model-mybk.03.4.45-86.00.3.87-48.00.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.8/0.2/0.0/0.0 (BP=1.000, ratio=1.038, hyp_len=11862, ref_len=11432)
Evaluation result for the model: seq-model-mybk.04.4.43-84.10.3.81-45.27.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.4/0.3/0.0/0.0 (BP=0.977, ratio=0.977, hyp_len=11170, ref_len=11432)
Evaluation result for the model: seq-model-mybk.05.4.37-78.79.3.80-44.72.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.2/0.2/0.0/0.0 (BP=1.000, ratio=1.024, hyp_len=11712, ref_len=11432)
Evaluation result for the model: seq-model-mybk.06.4.30-73.81.3.77-43.42.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.2/0.1/0.0/0.0 (BP=1.000, ratio=1.051, hyp_len=12015, ref_len=11432)
Evaluation result for the model: seq-model-mybk.07.4.26-71.02.3.77-43.20.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.7/0.3/0.0/0.0 (BP=1.000, ratio=1.030, hyp_len=11771, ref_len=11432)
Evaluation result for the model: seq-model-mybk.08.4.31-74.12.3.76-42.93.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.5/0.1/0.0/0.0 (BP=1.000, ratio=1.020, hyp_len=11656, ref_len=11432)
Evaluation result for the model: seq-model-mybk.09.4.24-69.75.3.76-43.12.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.9/0.6/0.0/0.0 (BP=1.000, ratio=1.031, hyp_len=11791, ref_len=11432)
Evaluation result for the model: seq-model-mybk.10.4.26-71.12.3.69-40.07.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.9/0.2/0.0/0.0 (BP=1.000, ratio=1.063, hyp_len=12155, ref_len=11432)
Evaluation result for the model: seq-model-mybk.11.4.01-55.25.3.51-33.41.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 24.0/1.2/0.0/0.0 (BP=0.815, ratio=0.830, hyp_len=9489, ref_len=11432)
Evaluation result for the model: seq-model-mybk.12.3.88-48.28.3.40-30.07.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 22.9/3.5/0.7/0.0 (BP=0.923, ratio=0.926, hyp_len=10588, ref_len=11432)
Evaluation result for the model: seq-model-mybk.13.3.78-43.60.3.33-27.89.pth
BLEU = 1.05, 22.3/4.3/1.1/0.0 (BP=1.000, ratio=1.015, hyp_len=11602, ref_len=11432)
Evaluation result for the model: seq-model-mybk.14.3.67-39.37.3.26-25.96.pth
BLEU = 1.92, 22.8/4.7/1.3/0.1 (BP=1.000, ratio=1.019, hyp_len=11649, ref_len=11432)
Evaluation result for the model: seq-model-mybk.15.3.54-34.61.3.19-24.31.pth
BLEU = 2.91, 21.4/5.5/1.4/0.4 (BP=1.000, ratio=1.173, hyp_len=13414, ref_len=11432)
Evaluation result for the model: seq-model-mybk.16.3.55-34.98.3.13-22.81.pth
BLEU = 3.54, 22.7/6.2/1.8/0.6 (BP=1.000, ratio=1.124, hyp_len=12854, ref_len=11432)
Evaluation result for the model: seq-model-mybk.17.3.37-29.03.3.04-21.00.pth
BLEU = 3.07, 18.3/5.0/1.6/0.6 (BP=1.000, ratio=1.432, hyp_len=16368, ref_len=11432)
Evaluation result for the model: seq-model-mybk.18.3.42-30.59.3.00-20.11.pth
BLEU = 2.73, 15.9/4.4/1.4/0.6 (BP=1.000, ratio=1.679, hyp_len=19199, ref_len=11432)
Evaluation result for the model: seq-model-mybk.19.3.29-26.89.2.96-19.31.pth
BLEU = 4.30, 22.4/6.4/2.4/1.0 (BP=1.000, ratio=1.203, hyp_len=13751, ref_len=11432)
Evaluation result for the model: seq-model-mybk.20.3.21-24.89.2.90-18.12.pth
BLEU = 3.19, 16.8/4.9/1.7/0.7 (BP=1.000, ratio=1.622, hyp_len=18538, ref_len=11432)
Evaluation result for the model: seq-model-mybk.21.3.17-23.70.2.85-17.32.pth
BLEU = 4.79, 24.9/7.3/2.7/1.1 (BP=1.000, ratio=1.130, hyp_len=12921, ref_len=11432)
Evaluation result for the model: seq-model-mybk.22.3.12-22.54.2.82-16.83.pth
BLEU = 5.17, 25.2/7.7/3.1/1.2 (BP=1.000, ratio=1.178, hyp_len=13464, ref_len=11432)
Evaluation result for the model: seq-model-mybk.23.3.07-21.63.2.77-15.97.pth
BLEU = 1.78, 9.0/2.7/1.0/0.4 (BP=1.000, ratio=3.140, hyp_len=35892, ref_len=11432)
Evaluation result for the model: seq-model-mybk.24.3.00-20.17.2.73-15.35.pth
BLEU = 5.88, 26.4/8.7/3.6/1.5 (BP=1.000, ratio=1.158, hyp_len=13243, ref_len=11432)
Evaluation result for the model: seq-model-mybk.25.3.01-20.20.2.71-14.98.pth
BLEU = 5.79, 28.0/8.9/3.4/1.3 (BP=1.000, ratio=1.106, hyp_len=12644, ref_len=11432)
Evaluation result for the model: seq-model-mybk.26.2.86-17.46.2.66-14.31.pth
BLEU = 6.17, 27.6/9.0/3.7/1.6 (BP=1.000, ratio=1.109, hyp_len=12673, ref_len=11432)
Evaluation result for the model: seq-model-mybk.27.2.83-16.93.2.64-14.01.pth
BLEU = 6.23, 28.1/9.3/3.8/1.5 (BP=1.000, ratio=1.107, hyp_len=12654, ref_len=11432)
Evaluation result for the model: seq-model-mybk.28.2.89-17.98.2.61-13.56.pth
BLEU = 7.01, 29.4/10.2/4.3/1.9 (BP=1.000, ratio=1.124, hyp_len=12844, ref_len=11432)
Evaluation result for the model: seq-model-mybk.29.2.87-17.61.2.59-13.27.pth
BLEU = 6.87, 28.8/9.8/4.3/1.8 (BP=1.000, ratio=1.163, hyp_len=13301, ref_len=11432)
Evaluation result for the model: seq-model-mybk.30.2.78-16.17.2.56-12.88.pth
BLEU = 7.22, 30.0/10.3/4.5/1.9 (BP=1.000, ratio=1.105, hyp_len=12630, ref_len=11432)
Evaluation result for the model: seq-model-mybk.31.2.70-14.93.2.54-12.72.pth
BLEU = 7.83, 30.9/11.4/4.9/2.1 (BP=1.000, ratio=1.132, hyp_len=12936, ref_len=11432)
Evaluation result for the model: seq-model-mybk.32.2.67-14.46.2.52-12.42.pth
BLEU = 8.13, 31.6/11.5/5.1/2.4 (BP=1.000, ratio=1.087, hyp_len=12430, ref_len=11432)
Evaluation result for the model: seq-model-mybk.33.2.65-14.10.2.53-12.50.pth
BLEU = 8.33, 32.3/11.8/5.3/2.4 (BP=1.000, ratio=1.107, hyp_len=12653, ref_len=11432)
Evaluation result for the model: seq-model-mybk.34.2.60-13.52.2.50-12.20.pth
BLEU = 8.68, 32.6/12.3/5.5/2.6 (BP=1.000, ratio=1.091, hyp_len=12473, ref_len=11432)
Evaluation result for the model: seq-model-mybk.35.2.48-12.00.2.48-11.97.pth
BLEU = 9.03, 33.0/12.6/5.8/2.7 (BP=1.000, ratio=1.087, hyp_len=12424, ref_len=11432)
Evaluation result for the model: seq-model-mybk.36.2.50-12.15.2.48-11.91.pth
BLEU = 8.99, 33.0/12.6/5.8/2.7 (BP=1.000, ratio=1.107, hyp_len=12651, ref_len=11432)
Evaluation result for the model: seq-model-mybk.37.2.53-12.49.2.47-11.88.pth
BLEU = 8.99, 32.9/12.6/5.8/2.7 (BP=1.000, ratio=1.110, hyp_len=12692, ref_len=11432)
Evaluation result for the model: seq-model-mybk.38.2.41-11.19.2.43-11.40.pth
BLEU = 9.58, 34.4/13.6/6.2/2.9 (BP=1.000, ratio=1.087, hyp_len=12424, ref_len=11432)
Evaluation result for the model: seq-model-mybk.39.2.41-11.09.2.42-11.20.pth
BLEU = 9.43, 33.8/13.3/6.1/2.9 (BP=1.000, ratio=1.100, hyp_len=12580, ref_len=11432)
Evaluation result for the model: seq-model-mybk.40.2.37-10.70.2.43-11.39.pth
BLEU = 9.30, 33.7/13.1/6.1/2.8 (BP=1.000, ratio=1.103, hyp_len=12608, ref_len=11432)
Evaluation result for the model: seq-model-mybk.41.2.34-10.43.2.42-11.28.pth
BLEU = 9.99, 34.8/13.7/6.5/3.2 (BP=1.000, ratio=1.093, hyp_len=12500, ref_len=11432)
Evaluation result for the model: seq-model-mybk.42.2.38-10.83.2.43-11.30.pth
BLEU = 10.54, 35.9/14.6/7.0/3.4 (BP=1.000, ratio=1.058, hyp_len=12100, ref_len=11432)
Evaluation result for the model: seq-model-mybk.43.2.30-9.93.2.40-11.06.pth
BLEU = 10.06, 34.6/13.8/6.6/3.3 (BP=1.000, ratio=1.111, hyp_len=12700, ref_len=11432)
Evaluation result for the model: seq-model-mybk.44.2.26-9.62.2.39-10.96.pth
BLEU = 10.72, 36.1/14.7/7.1/3.5 (BP=1.000, ratio=1.083, hyp_len=12377, ref_len=11432)
Evaluation result for the model: seq-model-mybk.45.2.23-9.28.2.39-10.89.pth
BLEU = 10.70, 35.7/15.0/7.2/3.4 (BP=1.000, ratio=1.104, hyp_len=12626, ref_len=11432)
Evaluation result for the model: seq-model-mybk.46.2.20-9.00.2.40-10.99.pth
BLEU = 10.68, 36.3/14.7/7.0/3.5 (BP=1.000, ratio=1.068, hyp_len=12214, ref_len=11432)
Evaluation result for the model: seq-model-mybk.47.2.18-8.89.2.40-11.03.pth
BLEU = 10.79, 36.2/15.0/7.2/3.5 (BP=1.000, ratio=1.085, hyp_len=12403, ref_len=11432)
Evaluation result for the model: seq-model-mybk.48.2.18-8.85.2.38-10.78.pth
BLEU = 10.86, 35.9/15.1/7.3/3.5 (BP=1.000, ratio=1.108, hyp_len=12670, ref_len=11432)
Evaluation result for the model: seq-model-mybk.49.2.11-8.26.2.39-10.89.pth
BLEU = 11.56, 36.8/15.9/7.8/3.9 (BP=1.000, ratio=1.107, hyp_len=12651, ref_len=11432)
Evaluation result for the model: seq-model-mybk.50.2.06-7.86.2.37-10.66.pth
BLEU = 11.14, 37.0/15.7/7.4/3.6 (BP=1.000, ratio=1.083, hyp_len=12381, ref_len=11432)
Evaluation result for the model: seq-model-mybk.51.2.04-7.71.2.36-10.61.pth
BLEU = 11.27, 37.4/15.8/7.6/3.6 (BP=1.000, ratio=1.096, hyp_len=12529, ref_len=11432)
Evaluation result for the model: seq-model-mybk.52.2.01-7.48.2.38-10.81.pth
BLEU = 10.66, 35.1/14.7/7.2/3.5 (BP=1.000, ratio=1.181, hyp_len=13499, ref_len=11432)
Evaluation result for the model: seq-model-mybk.53.2.11-8.26.2.36-10.54.pth
BLEU = 11.43, 36.6/15.9/7.8/3.7 (BP=1.000, ratio=1.129, hyp_len=12912, ref_len=11432)
Evaluation result for the model: seq-model-mybk.54.2.03-7.64.2.34-10.41.pth
BLEU = 11.85, 37.4/16.3/8.1/4.0 (BP=1.000, ratio=1.121, hyp_len=12810, ref_len=11432)
Evaluation result for the model: seq-model-mybk.55.1.99-7.31.2.37-10.69.pth
BLEU = 11.91, 38.0/16.5/8.1/4.0 (BP=1.000, ratio=1.106, hyp_len=12648, ref_len=11432)
Evaluation result for the model: seq-model-mybk.56.1.94-6.97.2.35-10.52.pth
BLEU = 11.82, 37.9/16.2/8.0/4.0 (BP=1.000, ratio=1.113, hyp_len=12723, ref_len=11432)
Evaluation result for the model: seq-model-mybk.57.1.96-7.09.2.36-10.58.pth
BLEU = 12.52, 39.0/17.2/8.5/4.3 (BP=1.000, ratio=1.092, hyp_len=12488, ref_len=11432)
Evaluation result for the model: seq-model-mybk.58.1.90-6.71.2.37-10.65.pth
BLEU = 12.39, 38.6/17.1/8.6/4.1 (BP=1.000, ratio=1.108, hyp_len=12670, ref_len=11432)
Evaluation result for the model: seq-model-mybk.59.1.86-6.40.2.38-10.77.pth
BLEU = 12.15, 38.8/16.9/8.3/4.0 (BP=1.000, ratio=1.083, hyp_len=12378, ref_len=11432)
Evaluation result for the model: seq-model-mybk.60.1.86-6.41.2.36-10.57.pth
BLEU = 12.72, 38.2/17.2/8.8/4.5 (BP=1.000, ratio=1.131, hyp_len=12927, ref_len=11432)
Evaluation result for the model: seq-model-mybk.61.1.85-6.34.2.34-10.39.pth
BLEU = 13.21, 39.6/17.8/9.1/4.8 (BP=1.000, ratio=1.089, hyp_len=12448, ref_len=11432)
Evaluation result for the model: seq-model-mybk.62.1.78-5.90.2.37-10.67.pth
BLEU = 12.43, 38.3/16.8/8.5/4.4 (BP=1.000, ratio=1.120, hyp_len=12802, ref_len=11432)
Evaluation result for the model: seq-model-mybk.63.1.82-6.19.2.38-10.84.pth
BLEU = 12.60, 38.0/16.9/8.6/4.6 (BP=1.000, ratio=1.120, hyp_len=12808, ref_len=11432)
Evaluation result for the model: seq-model-mybk.64.1.76-5.80.2.33-10.30.pth
BLEU = 13.25, 39.9/17.9/9.1/4.7 (BP=1.000, ratio=1.101, hyp_len=12582, ref_len=11432)
Evaluation result for the model: seq-model-mybk.65.1.75-5.75.2.34-10.34.pth
BLEU = 12.83, 39.2/17.4/8.8/4.5 (BP=1.000, ratio=1.107, hyp_len=12655, ref_len=11432)
Evaluation result for the model: seq-model-mybk.66.1.76-5.80.2.38-10.85.pth
BLEU = 12.59, 38.8/16.9/8.5/4.5 (BP=1.000, ratio=1.117, hyp_len=12764, ref_len=11432)
Evaluation result for the model: seq-model-mybk.67.1.75-5.77.2.36-10.57.pth
BLEU = 13.09, 39.7/17.7/9.0/4.6 (BP=1.000, ratio=1.107, hyp_len=12660, ref_len=11432)
Evaluation result for the model: seq-model-mybk.68.1.77-5.87.2.39-10.87.pth
BLEU = 13.40, 39.7/18.1/9.2/4.9 (BP=1.000, ratio=1.096, hyp_len=12525, ref_len=11432)
Evaluation result for the model: seq-model-mybk.69.1.65-5.22.2.39-10.95.pth
BLEU = 13.06, 39.6/17.7/8.9/4.6 (BP=1.000, ratio=1.115, hyp_len=12748, ref_len=11432)
Evaluation result for the model: seq-model-mybk.70.1.61-4.99.2.36-10.56.pth
BLEU = 13.31, 39.5/17.9/9.2/4.8 (BP=1.000, ratio=1.117, hyp_len=12771, ref_len=11432)
/home/ye/exp/simple-nmt
==========

```


## Seq2Seq-RL

နောက်ဆက်တွဲ continuous-training တွေရဲ့ model တွေကိုလည်း ရှေ့မှာ training လုပ်ခဲ့တဲ့ ဖိုလ်ဒါထဲမှာပဲအတူတူ သိမ်းခဲ့တယ်။ အဲဒါကြောင့် 30-epoch ရဲ့ RL model တွေက 30-epoch/ အောက်မှာပဲ ဆက်ရှိမယ်။   


## for Transformer Baseline
### Bash Script Writing

30 epoch ကနေ 70 epoch အထိ transformer training အတွက် အောက်ပါ bash script ကို ရေးပြီး သုံးခဲ့...   

```bash

```

## Transformer-RL

