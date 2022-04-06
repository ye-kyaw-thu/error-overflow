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
ဖိုင်နာမည်က rl-seq2seq-train.sh   

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

သုံးခဲ့တဲ့ test-eval-rl2-seq2seq-baseline-mybk-bkmy.sh က အောက်ပါအတိုင်း...  

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
/home/ye/exp/simple-nmt/model/rl2/baseline/seq2seq/bkmy-30epoch
Evaluation result for the model: seq-model-bkmy.01.4.75-116.00.3.97-52.83.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.4/0.5/0.0/0.0 (BP=1.000, ratio=1.012, hyp_len=12382, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.02.4.22-67.74.3.82-45.64.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.4/0.6/0.0/0.0 (BP=0.960, ratio=0.961, hyp_len=11750, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.03.4.18-65.07.3.77-43.48.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.1/0.4/0.0/0.0 (BP=0.997, ratio=0.997, hyp_len=12199, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.04.4.17-64.96.3.74-42.31.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.4/0.5/0.0/0.0 (BP=0.997, ratio=0.997, hyp_len=12197, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.05.4.16-64.15.3.73-41.80.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.3/0.6/0.0/0.0 (BP=1.000, ratio=1.009, hyp_len=12335, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.06.4.14-62.97.3.75-42.47.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.7/0.5/0.0/0.0 (BP=1.000, ratio=1.033, hyp_len=12630, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.07.4.11-61.01.3.72-41.11.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.6/0.6/0.0/0.0 (BP=0.988, ratio=0.988, hyp_len=12089, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.08.4.09-59.86.3.66-39.01.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.8/0.9/0.0/0.0 (BP=1.000, ratio=1.033, hyp_len=12632, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.09.4.03-56.35.3.66-38.94.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.5/0.9/0.0/0.0 (BP=1.000, ratio=1.011, hyp_len=12367, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.10.4.09-59.60.3.59-36.24.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.4/0.9/0.0/0.0 (BP=1.000, ratio=1.141, hyp_len=13955, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.11.3.84-46.39.3.40-30.08.pth
BLEU = 0.87, 20.9/2.4/0.3/0.0 (BP=1.000, ratio=1.011, hyp_len=12363, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.12.3.73-41.78.3.27-26.22.pth
BLEU = 0.33, 5.6/0.9/0.1/0.0 (BP=1.000, ratio=4.201, hyp_len=51386, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.13.3.50-33.23.3.17-23.86.pth
BLEU = 0.14, 2.7/0.6/0.1/0.0 (BP=1.000, ratio=8.059, hyp_len=98572, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.14.3.43-30.82.3.08-21.68.pth
BLEU = 0.51, 8.0/1.9/0.3/0.0 (BP=1.000, ratio=3.405, hyp_len=41652, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.15.3.34-28.32.3.00-20.15.pth
BLEU = 0.55, 5.6/1.4/0.3/0.0 (BP=1.000, ratio=4.804, hyp_len=58755, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.16.3.30-27.21.2.96-19.25.pth
BLEU = 2.62, 20.9/6.2/1.5/0.2 (BP=1.000, ratio=1.505, hyp_len=18410, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.17.3.28-26.65.2.90-18.25.pth
BLEU = 1.91, 15.6/4.8/1.0/0.2 (BP=1.000, ratio=2.003, hyp_len=24497, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.18.3.19-24.41.2.87-17.65.pth
BLEU = 1.72, 12.7/3.9/1.0/0.2 (BP=1.000, ratio=2.499, hyp_len=30568, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.19.3.13-22.91.2.84-17.03.pth
BLEU = 4.36, 23.4/8.0/2.5/0.8 (BP=1.000, ratio=1.419, hyp_len=17351, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.20.3.08-21.76.2.79-16.35.pth
BLEU = 6.63, 32.3/11.9/4.2/1.2 (BP=1.000, ratio=1.050, hyp_len=12840, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.21.3.06-21.26.2.75-15.65.pth
BLEU = 6.16, 27.9/10.4/3.8/1.3 (BP=1.000, ratio=1.213, hyp_len=14831, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.22.2.99-19.92.2.75-15.62.pth
BLEU = 7.96, 33.7/13.2/4.9/1.8 (BP=1.000, ratio=1.010, hyp_len=12351, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.23.2.94-18.89.2.72-15.24.pth
BLEU = 7.65, 30.9/12.5/4.7/1.9 (BP=1.000, ratio=1.141, hyp_len=13957, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.24.2.95-19.17.2.68-14.63.pth
BLEU = 5.03, 22.9/8.3/3.0/1.1 (BP=1.000, ratio=1.511, hyp_len=18480, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.25.2.87-17.65.2.67-14.40.pth
BLEU = 8.06, 31.3/12.7/5.1/2.1 (BP=1.000, ratio=1.158, hyp_len=14168, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.26.2.79-16.20.2.63-13.88.pth
BLEU = 6.59, 26.9/10.6/4.1/1.6 (BP=1.000, ratio=1.343, hyp_len=16423, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.27.2.81-16.59.2.62-13.74.pth
BLEU = 7.43, 29.7/11.8/4.5/1.9 (BP=1.000, ratio=1.207, hyp_len=14763, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.28.2.73-15.28.2.58-13.13.pth
BLEU = 9.13, 35.1/14.4/5.6/2.4 (BP=1.000, ratio=1.041, hyp_len=12731, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.29.2.80-16.50.2.57-13.09.pth
BLEU = 5.81, 22.3/9.2/3.7/1.5 (BP=1.000, ratio=1.642, hyp_len=20081, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.30.2.69-14.67.2.53-12.59.pth
BLEU = 9.54, 35.5/14.8/6.1/2.6 (BP=1.000, ratio=1.043, hyp_len=12751, ref_len=12231)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/baseline/seq2seq/bkmy-40epoch
Evaluation result for the model: seq-model-bkmy.01.4.77-117.66.3.99-53.84.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 25.1/0.7/0.0/0.0 (BP=0.785, ratio=0.805, hyp_len=9849, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.02.4.33-75.97.3.85-47.02.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.4/0.3/0.0/0.0 (BP=1.000, ratio=1.011, hyp_len=12361, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.03.4.21-67.23.3.79-44.22.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.8/1.9/0.3/0.0 (BP=0.940, ratio=0.941, hyp_len=11513, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.04.4.19-66.01.3.77-43.18.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.4/2.0/0.3/0.0 (BP=1.000, ratio=1.005, hyp_len=12295, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.05.4.22-67.97.3.73-41.63.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.3/0.5/0.0/0.0 (BP=1.000, ratio=1.010, hyp_len=12352, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.06.4.21-67.32.3.71-40.87.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.3/0.6/0.0/0.0 (BP=1.000, ratio=1.009, hyp_len=12343, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.07.4.19-66.08.3.69-40.17.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.1/0.5/0.0/0.0 (BP=1.000, ratio=1.055, hyp_len=12909, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.08.4.09-59.64.3.67-39.29.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.7/1.0/0.1/0.0 (BP=1.000, ratio=1.060, hyp_len=12961, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.09.4.05-57.59.3.62-37.18.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.8/1.0/0.0/0.0 (BP=1.000, ratio=1.067, hyp_len=13047, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.10.3.94-51.17.3.39-29.76.pth
BLEU = 0.50, 20.5/1.4/0.2/0.0 (BP=1.000, ratio=1.026, hyp_len=12544, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.11.3.60-36.73.3.24-25.58.pth
BLEU = 0.10, 1.8/0.3/0.1/0.0 (BP=1.000, ratio=11.246, hyp_len=137550, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.12.3.58-35.81.3.14-23.06.pth
BLEU = 0.14, 2.2/0.4/0.1/0.0 (BP=1.000, ratio=10.338, hyp_len=126440, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.13.3.42-30.48.3.08-21.70.pth
BLEU = 1.33, 10.8/2.8/0.7/0.1 (BP=1.000, ratio=2.666, hyp_len=32605, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.14.3.36-28.81.3.03-20.60.pth
BLEU = 1.62, 11.7/3.3/0.9/0.2 (BP=1.000, ratio=2.641, hyp_len=32300, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.15.3.27-26.33.2.97-19.53.pth
BLEU = 1.61, 11.5/3.4/1.0/0.2 (BP=1.000, ratio=2.676, hyp_len=32731, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.16.3.22-24.95.2.91-18.41.pth
BLEU = 4.10, 25.4/8.0/2.5/0.6 (BP=1.000, ratio=1.224, hyp_len=14971, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.17.3.21-24.73.2.92-18.63.pth
BLEU = 1.72, 11.2/3.5/1.0/0.2 (BP=1.000, ratio=2.766, hyp_len=33834, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.18.3.22-25.15.2.84-17.20.pth
BLEU = 5.22, 29.6/10.1/3.2/0.8 (BP=1.000, ratio=1.097, hyp_len=13423, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.19.3.08-21.68.2.81-16.56.pth
BLEU = 4.57, 21.7/8.0/2.9/0.9 (BP=1.000, ratio=1.535, hyp_len=18775, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.20.3.05-21.10.2.78-16.19.pth
BLEU = 6.58, 31.7/11.8/4.2/1.2 (BP=1.000, ratio=1.094, hyp_len=13383, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.21.3.02-20.48.2.74-15.46.pth
BLEU = 3.10, 14.7/5.4/1.9/0.6 (BP=1.000, ratio=2.350, hyp_len=28746, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.22.2.92-18.45.2.74-15.53.pth
BLEU = 4.56, 21.0/7.8/2.9/0.9 (BP=1.000, ratio=1.637, hyp_len=20026, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.23.2.93-18.71.2.73-15.35.pth
BLEU = 4.12, 18.8/7.0/2.5/0.9 (BP=1.000, ratio=1.864, hyp_len=22804, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.24.2.98-19.72.2.66-14.27.pth
BLEU = 4.91, 22.4/8.4/3.1/1.0 (BP=1.000, ratio=1.598, hyp_len=19544, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.25.2.80-16.41.2.64-13.98.pth
BLEU = 6.68, 27.0/10.7/4.2/1.6 (BP=1.000, ratio=1.349, hyp_len=16497, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.26.2.82-16.81.2.65-14.22.pth
BLEU = 4.08, 17.3/6.7/2.6/0.9 (BP=1.000, ratio=2.077, hyp_len=25408, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.27.2.76-15.76.2.60-13.53.pth
BLEU = 5.01, 20.7/8.1/3.2/1.2 (BP=1.000, ratio=1.768, hyp_len=21624, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.28.2.73-15.29.2.60-13.51.pth
BLEU = 6.98, 27.7/10.9/4.5/1.8 (BP=1.000, ratio=1.329, hyp_len=16253, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.29.2.67-14.48.2.59-13.38.pth
BLEU = 8.70, 34.0/13.7/5.4/2.3 (BP=1.000, ratio=1.088, hyp_len=13312, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.30.2.62-13.76.2.59-13.38.pth
BLEU = 6.41, 24.6/9.7/4.1/1.7 (BP=1.000, ratio=1.533, hyp_len=18751, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.31.2.67-14.51.2.57-13.04.pth
BLEU = 6.72, 26.8/10.7/4.3/1.7 (BP=1.000, ratio=1.421, hyp_len=17382, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.32.2.57-13.11.2.54-12.62.pth
BLEU = 7.66, 29.8/12.2/4.9/1.9 (BP=1.000, ratio=1.289, hyp_len=15768, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.33.2.49-12.10.2.53-12.59.pth
BLEU = 8.33, 32.0/13.2/5.4/2.1 (BP=1.000, ratio=1.174, hyp_len=14358, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.34.2.52-12.47.2.54-12.65.pth
BLEU = 5.11, 20.1/8.0/3.2/1.3 (BP=1.000, ratio=1.905, hyp_len=23303, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.35.2.47-11.76.2.54-12.70.pth
BLEU = 6.84, 26.9/10.7/4.4/1.7 (BP=1.000, ratio=1.414, hyp_len=17294, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.36.2.46-11.69.2.52-12.42.pth
BLEU = 3.61, 14.8/5.8/2.3/0.9 (BP=1.000, ratio=2.557, hyp_len=31269, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.37.2.44-11.44.2.52-12.40.pth
BLEU = 7.36, 28.8/11.8/4.8/1.8 (BP=1.000, ratio=1.336, hyp_len=16336, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.38.2.38-10.82.2.53-12.57.pth
BLEU = 8.47, 31.6/13.0/5.5/2.3 (BP=1.000, ratio=1.230, hyp_len=15040, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.39.2.35-10.48.2.51-12.29.pth
BLEU = 8.23, 31.2/12.7/5.3/2.2 (BP=1.000, ratio=1.232, hyp_len=15069, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.40.2.37-10.75.2.48-11.96.pth
BLEU = 6.35, 24.7/10.0/4.0/1.6 (BP=1.000, ratio=1.560, hyp_len=19079, ref_len=12231)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/baseline/seq2seq/bkmy-50epoch
Evaluation result for the model: seq-model-bkmy.01.4.78-119.15.3.99-53.81.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 23.8/0.7/0.0/0.0 (BP=0.746, ratio=0.774, hyp_len=9464, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.02.4.36-78.00.3.83-46.07.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.5/0.5/0.0/0.0 (BP=1.000, ratio=1.010, hyp_len=12355, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.03.4.20-66.96.3.78-44.00.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.1/2.0/0.3/0.0 (BP=1.000, ratio=1.018, hyp_len=12453, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.04.4.26-70.80.3.79-44.41.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.8/1.1/0.1/0.0 (BP=1.000, ratio=1.003, hyp_len=12269, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.05.4.21-67.69.3.75-42.47.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.4/0.5/0.0/0.0 (BP=1.000, ratio=1.053, hyp_len=12884, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.06.4.20-66.88.3.74-42.07.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.7/0.5/0.0/0.0 (BP=1.000, ratio=1.015, hyp_len=12415, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.07.4.11-60.82.3.69-39.97.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.3/0.7/0.0/0.0 (BP=1.000, ratio=1.038, hyp_len=12699, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.08.4.13-62.06.3.64-38.08.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.8/1.2/0.1/0.0 (BP=1.000, ratio=1.003, hyp_len=12268, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.09.4.01-55.07.3.60-36.56.pth
BLEU = 0.53, 21.4/1.8/0.2/0.0 (BP=1.000, ratio=1.037, hyp_len=12689, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.10.3.84-46.33.3.39-29.73.pth
BLEU = 0.46, 20.7/1.9/0.1/0.0 (BP=1.000, ratio=1.058, hyp_len=12946, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.11.3.64-38.00.3.24-25.42.pth
BLEU = 0.75, 21.7/3.7/0.5/0.0 (BP=1.000, ratio=1.183, hyp_len=14468, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.12.3.52-33.80.3.14-23.09.pth
BLEU = 0.13, 2.5/0.5/0.1/0.0 (BP=1.000, ratio=9.040, hyp_len=110566, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.13.3.51-33.46.3.08-21.75.pth
BLEU = 2.66, 20.8/5.8/1.6/0.3 (BP=1.000, ratio=1.365, hyp_len=16692, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.14.3.44-31.31.3.02-20.51.pth
BLEU = 1.55, 13.0/3.7/0.9/0.1 (BP=1.000, ratio=2.373, hyp_len=29027, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.15.3.42-30.42.2.99-19.85.pth
BLEU = 0.27, 1.9/0.6/0.2/0.0 (BP=1.000, ratio=13.460, hyp_len=164633, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.16.3.23-25.36.2.95-19.07.pth
BLEU = 0.73, 5.3/1.7/0.5/0.1 (BP=1.000, ratio=5.993, hyp_len=73302, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.17.3.27-26.38.2.88-17.85.pth
BLEU = 3.73, 23.1/8.0/2.3/0.5 (BP=1.000, ratio=1.458, hyp_len=17834, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.18.3.15-23.40.2.84-17.11.pth
BLEU = 6.77, 32.1/12.6/4.2/1.2 (BP=1.000, ratio=1.068, hyp_len=13062, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.19.3.09-21.98.2.80-16.37.pth
BLEU = 6.03, 30.2/11.4/3.8/1.0 (BP=1.000, ratio=1.139, hyp_len=13930, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.20.3.05-21.14.2.81-16.57.pth
BLEU = 2.54, 12.4/4.7/1.6/0.5 (BP=1.000, ratio=2.739, hyp_len=33502, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.21.3.09-21.94.2.76-15.82.pth
BLEU = 7.60, 32.0/12.8/4.7/1.7 (BP=1.000, ratio=1.100, hyp_len=13453, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.22.2.96-19.33.2.72-15.16.pth
BLEU = 5.06, 21.4/8.5/3.2/1.1 (BP=1.000, ratio=1.696, hyp_len=20741, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.23.2.92-18.60.2.70-14.91.pth
BLEU = 7.68, 31.8/12.5/4.7/1.8 (BP=1.000, ratio=1.136, hyp_len=13900, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.24.2.89-18.05.2.66-14.32.pth
BLEU = 6.25, 25.7/10.3/3.8/1.5 (BP=1.000, ratio=1.425, hyp_len=17426, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.25.2.88-17.88.2.68-14.54.pth
BLEU = 5.08, 21.4/8.7/3.1/1.2 (BP=1.000, ratio=1.696, hyp_len=20745, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.26.2.82-16.74.2.63-13.92.pth
BLEU = 6.33, 26.2/10.6/3.9/1.5 (BP=1.000, ratio=1.388, hyp_len=16972, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.27.2.81-16.63.2.61-13.56.pth
BLEU = 6.61, 27.1/11.0/4.1/1.6 (BP=1.000, ratio=1.384, hyp_len=16924, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.28.2.75-15.60.2.64-14.06.pth
BLEU = 4.92, 20.9/8.3/3.1/1.1 (BP=1.000, ratio=1.758, hyp_len=21501, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.29.2.70-14.84.2.58-13.19.pth
BLEU = 7.51, 29.4/12.0/4.7/1.9 (BP=1.000, ratio=1.279, hyp_len=15642, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.30.2.69-14.78.2.58-13.26.pth
BLEU = 4.53, 18.8/7.6/2.8/1.0 (BP=1.000, ratio=1.939, hyp_len=23711, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.31.2.62-13.77.2.55-12.78.pth
BLEU = 7.76, 31.2/12.6/4.8/1.9 (BP=1.000, ratio=1.224, hyp_len=14971, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.32.2.59-13.39.2.55-12.77.pth
BLEU = 7.33, 29.5/12.0/4.6/1.8 (BP=1.000, ratio=1.276, hyp_len=15603, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.33.2.58-13.15.2.51-12.33.pth
BLEU = 8.41, 32.3/13.3/5.3/2.2 (BP=1.000, ratio=1.191, hyp_len=14569, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.34.2.55-12.77.2.50-12.17.pth
BLEU = 7.06, 27.3/11.3/4.5/1.8 (BP=1.000, ratio=1.433, hyp_len=17525, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.35.2.51-12.35.2.52-12.48.pth
BLEU = 5.61, 22.1/8.9/3.5/1.4 (BP=1.000, ratio=1.750, hyp_len=21410, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.36.2.58-13.26.2.49-12.08.pth
BLEU = 7.13, 27.6/11.3/4.6/1.8 (BP=1.000, ratio=1.401, hyp_len=17133, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.37.2.46-11.71.2.49-12.12.pth
BLEU = 6.00, 23.3/9.6/3.9/1.5 (BP=1.000, ratio=1.680, hyp_len=20553, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.38.2.41-11.16.2.47-11.85.pth
BLEU = 7.64, 29.7/12.0/4.8/2.0 (BP=1.000, ratio=1.329, hyp_len=16260, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.39.2.36-10.61.2.46-11.75.pth
BLEU = 7.87, 30.9/12.7/5.0/1.9 (BP=1.000, ratio=1.277, hyp_len=15614, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.40.2.34-10.39.2.48-11.89.pth
BLEU = 9.51, 34.6/14.5/6.1/2.7 (BP=1.000, ratio=1.151, hyp_len=14077, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.41.2.29-9.91.2.46-11.66.pth
BLEU = 8.33, 31.9/13.3/5.4/2.1 (BP=1.000, ratio=1.241, hyp_len=15182, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.42.2.35-10.47.2.45-11.63.pth
BLEU = 8.21, 30.7/12.6/5.2/2.3 (BP=1.000, ratio=1.303, hyp_len=15931, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.43.2.25-9.52.2.44-11.46.pth
BLEU = 9.08, 33.6/14.1/5.9/2.4 (BP=1.000, ratio=1.185, hyp_len=14492, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.44.2.27-9.71.2.44-11.51.pth
BLEU = 9.65, 35.6/15.2/6.3/2.6 (BP=1.000, ratio=1.140, hyp_len=13946, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.45.2.30-9.99.2.44-11.51.pth
BLEU = 9.18, 33.4/14.2/5.9/2.5 (BP=1.000, ratio=1.223, hyp_len=14959, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.46.2.19-8.92.2.44-11.46.pth
BLEU = 10.56, 37.2/16.0/6.9/3.0 (BP=1.000, ratio=1.091, hyp_len=13344, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.47.2.18-8.88.2.44-11.52.pth
BLEU = 10.75, 36.8/16.1/7.0/3.2 (BP=1.000, ratio=1.085, hyp_len=13275, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.48.2.09-8.09.2.44-11.43.pth
BLEU = 10.35, 35.9/15.5/6.8/3.0 (BP=1.000, ratio=1.145, hyp_len=14001, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.49.2.10-8.16.2.43-11.36.pth
BLEU = 10.72, 37.5/16.0/7.0/3.1 (BP=1.000, ratio=1.081, hyp_len=13218, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.50.2.08-8.01.2.45-11.63.pth
BLEU = 10.62, 36.6/15.7/7.0/3.2 (BP=1.000, ratio=1.118, hyp_len=13676, ref_len=12231)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/baseline/seq2seq/bkmy-60epoch
Evaluation result for the model: seq-model-bkmy.01.4.74-114.76.3.93-50.92.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 28.0/0.8/0.0/0.0 (BP=0.611, ratio=0.670, hyp_len=8193, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.02.4.31-74.36.3.80-44.87.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.4/0.5/0.0/0.0 (BP=1.000, ratio=1.017, hyp_len=12437, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.03.4.17-64.56.3.79-44.16.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.1/0.5/0.0/0.0 (BP=1.000, ratio=1.012, hyp_len=12378, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.04.4.23-68.62.3.76-43.14.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.6/1.9/0.3/0.0 (BP=1.000, ratio=1.009, hyp_len=12338, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.05.4.17-65.00.3.73-41.66.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.1/0.5/0.0/0.0 (BP=1.000, ratio=1.019, hyp_len=12458, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.06.4.18-65.07.3.70-40.43.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.3/0.7/0.0/0.0 (BP=1.000, ratio=1.094, hyp_len=13376, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.07.4.06-57.84.3.66-38.76.pth
BLEU = 0.86, 19.9/1.7/0.4/0.0 (BP=1.000, ratio=1.076, hyp_len=13156, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.08.4.02-55.79.3.58-35.70.pth
BLEU = 0.71, 19.5/1.8/0.4/0.0 (BP=1.000, ratio=1.050, hyp_len=12847, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.09.3.89-48.80.3.38-29.43.pth
BLEU = 1.09, 20.8/2.6/0.5/0.1 (BP=1.000, ratio=1.007, hyp_len=12316, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.10.3.69-40.05.3.22-24.97.pth
BLEU = 1.17, 22.1/4.0/0.5/0.0 (BP=1.000, ratio=1.111, hyp_len=13592, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.11.3.52-33.75.3.12-22.70.pth
BLEU = 0.38, 4.5/0.9/0.2/0.0 (BP=1.000, ratio=5.357, hyp_len=65519, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.12.3.43-30.79.3.07-21.59.pth
BLEU = 0.23, 2.6/0.6/0.1/0.0 (BP=1.000, ratio=9.233, hyp_len=112928, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.13.3.34-28.21.3.00-20.03.pth
BLEU = 0.30, 3.3/0.8/0.2/0.0 (BP=1.000, ratio=7.676, hyp_len=93890, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.14.3.33-27.82.2.94-18.96.pth
BLEU = 2.75, 25.6/6.6/1.6/0.2 (BP=1.000, ratio=1.147, hyp_len=14024, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.15.3.22-25.08.2.88-17.78.pth
BLEU = 4.71, 30.3/10.2/2.9/0.6 (BP=1.000, ratio=1.066, hyp_len=13040, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.16.3.23-25.36.2.83-16.93.pth
BLEU = 3.23, 19.2/6.5/1.9/0.5 (BP=1.000, ratio=1.724, hyp_len=21090, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.17.3.11-22.52.2.79-16.23.pth
BLEU = 6.35, 32.5/11.8/3.7/1.1 (BP=1.000, ratio=1.063, hyp_len=13002, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.18.3.14-23.15.2.75-15.58.pth
BLEU = 7.03, 32.0/12.3/4.3/1.4 (BP=1.000, ratio=1.070, hyp_len=13083, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.19.3.07-21.60.2.71-15.10.pth
BLEU = 6.26, 27.1/10.7/3.9/1.3 (BP=1.000, ratio=1.280, hyp_len=15659, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.20.3.04-20.97.2.68-14.58.pth
BLEU = 4.26, 20.2/7.5/2.6/0.8 (BP=1.000, ratio=1.694, hyp_len=20715, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.21.2.93-18.78.2.64-14.03.pth
BLEU = 6.57, 26.9/10.6/4.1/1.6 (BP=1.000, ratio=1.286, hyp_len=15727, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.22.2.86-17.42.2.61-13.62.pth
BLEU = 5.72, 24.2/9.4/3.5/1.3 (BP=1.000, ratio=1.462, hyp_len=17885, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.23.2.81-16.69.2.59-13.31.pth
BLEU = 7.53, 30.5/12.0/4.7/1.9 (BP=1.000, ratio=1.158, hyp_len=14158, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.24.2.76-15.78.2.55-12.85.pth
BLEU = 6.93, 29.0/11.2/4.3/1.6 (BP=1.000, ratio=1.243, hyp_len=15207, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.25.2.82-16.74.2.52-12.40.pth
BLEU = 5.71, 23.6/9.4/3.6/1.3 (BP=1.000, ratio=1.540, hyp_len=18831, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.26.2.79-16.26.2.50-12.15.pth
BLEU = 7.28, 29.8/11.9/4.7/1.7 (BP=1.000, ratio=1.232, hyp_len=15071, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.27.2.63-13.92.2.48-11.94.pth
BLEU = 6.25, 24.8/10.0/3.9/1.6 (BP=1.000, ratio=1.472, hyp_len=18001, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.28.2.63-13.94.2.47-11.83.pth
BLEU = 8.56, 33.6/13.6/5.5/2.2 (BP=1.000, ratio=1.086, hyp_len=13287, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.29.2.62-13.76.2.45-11.62.pth
BLEU = 8.75, 35.0/13.9/5.6/2.2 (BP=1.000, ratio=1.054, hyp_len=12891, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.30.2.59-13.28.2.45-11.56.pth
BLEU = 7.64, 29.1/12.0/5.0/2.0 (BP=1.000, ratio=1.288, hyp_len=15750, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.31.2.48-11.99.2.44-11.49.pth
BLEU = 7.40, 28.8/11.5/4.7/1.9 (BP=1.000, ratio=1.316, hyp_len=16098, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.32.2.45-11.64.2.43-11.30.pth
BLEU = 6.53, 26.5/10.5/4.2/1.6 (BP=1.000, ratio=1.435, hyp_len=17547, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.33.2.46-11.67.2.40-11.06.pth
BLEU = 7.25, 27.9/11.1/4.7/1.9 (BP=1.000, ratio=1.342, hyp_len=16413, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.34.2.48-11.91.2.41-11.09.pth
BLEU = 9.20, 35.3/14.2/5.9/2.4 (BP=1.000, ratio=1.075, hyp_len=13147, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.35.2.45-11.59.2.38-10.75.pth
BLEU = 9.18, 35.9/14.2/5.8/2.4 (BP=1.000, ratio=1.072, hyp_len=13112, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.36.2.35-10.47.2.38-10.85.pth
BLEU = 9.31, 35.9/14.5/5.9/2.5 (BP=1.000, ratio=1.075, hyp_len=13149, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.37.2.30-9.97.2.36-10.63.pth
BLEU = 9.82, 36.1/14.9/6.4/2.7 (BP=1.000, ratio=1.085, hyp_len=13272, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.38.2.34-10.42.2.39-10.90.pth
BLEU = 9.70, 35.9/14.7/6.3/2.7 (BP=1.000, ratio=1.107, hyp_len=13545, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.39.2.25-9.50.2.38-10.81.pth
BLEU = 9.45, 35.6/14.4/6.0/2.6 (BP=1.000, ratio=1.100, hyp_len=13459, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.40.2.32-10.19.2.34-10.35.pth
BLEU = 10.24, 36.7/15.4/6.6/3.0 (BP=1.000, ratio=1.080, hyp_len=13205, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.41.2.20-8.99.2.36-10.62.pth
BLEU = 9.78, 36.3/15.0/6.3/2.7 (BP=1.000, ratio=1.089, hyp_len=13322, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.42.2.15-8.58.2.36-10.64.pth
BLEU = 9.72, 36.1/14.6/6.2/2.7 (BP=1.000, ratio=1.096, hyp_len=13410, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.43.2.13-8.38.2.36-10.60.pth
BLEU = 9.49, 36.5/14.6/6.0/2.5 (BP=1.000, ratio=1.088, hyp_len=13311, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.44.2.17-8.78.2.37-10.75.pth
BLEU = 10.39, 36.9/15.5/6.8/3.0 (BP=1.000, ratio=1.087, hyp_len=13300, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.45.2.09-8.12.2.37-10.69.pth
BLEU = 9.90, 36.6/14.8/6.2/2.8 (BP=1.000, ratio=1.095, hyp_len=13396, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.46.2.16-8.64.2.36-10.60.pth
BLEU = 10.72, 37.8/15.8/7.0/3.2 (BP=1.000, ratio=1.065, hyp_len=13027, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.47.2.05-7.80.2.35-10.54.pth
BLEU = 10.12, 36.7/15.3/6.5/2.9 (BP=1.000, ratio=1.091, hyp_len=13338, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.48.2.03-7.63.2.36-10.57.pth
BLEU = 10.49, 37.4/15.4/6.7/3.1 (BP=1.000, ratio=1.084, hyp_len=13253, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.49.1.99-7.29.2.35-10.45.pth
BLEU = 9.96, 37.0/15.3/6.4/2.7 (BP=1.000, ratio=1.077, hyp_len=13168, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.50.2.02-7.56.2.35-10.45.pth
BLEU = 10.66, 38.5/16.2/6.9/3.0 (BP=1.000, ratio=1.062, hyp_len=12990, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.51.2.01-7.48.2.34-10.36.pth
BLEU = 11.07, 38.0/16.3/7.2/3.4 (BP=1.000, ratio=1.083, hyp_len=13246, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.52.1.94-6.98.2.36-10.59.pth
BLEU = 10.98, 39.1/16.5/7.1/3.2 (BP=1.000, ratio=1.060, hyp_len=12959, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.53.1.99-7.32.2.37-10.68.pth
BLEU = 10.52, 37.0/15.5/6.8/3.1 (BP=1.000, ratio=1.088, hyp_len=13312, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.54.1.96-7.12.2.37-10.67.pth
BLEU = 10.37, 37.0/15.3/6.6/3.1 (BP=1.000, ratio=1.100, hyp_len=13450, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.55.2.00-7.35.2.37-10.74.pth
BLEU = 10.72, 38.2/16.1/7.0/3.1 (BP=1.000, ratio=1.075, hyp_len=13151, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.56.1.86-6.43.2.37-10.67.pth
BLEU = 10.69, 38.0/15.8/6.9/3.2 (BP=1.000, ratio=1.077, hyp_len=13176, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.57.1.85-6.35.2.36-10.55.pth
BLEU = 11.17, 38.6/16.5/7.3/3.4 (BP=1.000, ratio=1.074, hyp_len=13136, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.58.1.85-6.33.2.41-11.13.pth
BLEU = 10.32, 37.5/15.6/6.7/2.9 (BP=1.000, ratio=1.088, hyp_len=13304, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.59.1.79-5.99.2.36-10.62.pth
BLEU = 10.34, 37.7/16.0/6.7/2.8 (BP=1.000, ratio=1.074, hyp_len=13134, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.60.1.75-5.78.2.37-10.71.pth
BLEU = 10.73, 37.9/15.8/6.9/3.2 (BP=1.000, ratio=1.093, hyp_len=13367, ref_len=12231)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/baseline/seq2seq/bkmy-70epoch
Evaluation result for the model: seq-model-bkmy.01.4.75-115.89.3.97-53.12.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.2/0.7/0.0/0.0 (BP=0.930, ratio=0.933, hyp_len=11406, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.02.4.24-69.75.3.81-45.36.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.9/0.6/0.0/0.0 (BP=0.935, ratio=0.937, hyp_len=11456, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.03.4.17-64.62.3.79-44.47.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.6/1.5/0.2/0.0 (BP=0.991, ratio=0.991, hyp_len=12127, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.04.4.14-63.00.3.79-44.15.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.3/0.5/0.0/0.0 (BP=1.000, ratio=1.064, hyp_len=13009, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.05.4.15-63.30.3.76-43.13.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.5/1.1/0.2/0.0 (BP=1.000, ratio=1.047, hyp_len=12807, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.06.4.15-63.68.3.77-43.18.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.8/1.6/0.2/0.0 (BP=0.996, ratio=0.996, hyp_len=12188, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.07.4.14-62.98.3.73-41.81.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.0/1.7/0.2/0.0 (BP=0.993, ratio=0.993, hyp_len=12141, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.08.4.09-59.74.3.73-41.59.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.9/0.4/0.0/0.0 (BP=1.000, ratio=1.079, hyp_len=13196, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.09.4.18-65.49.3.72-41.06.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 22.1/1.3/0.1/0.0 (BP=0.997, ratio=0.997, hyp_len=12194, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.10.4.08-59.08.3.65-38.51.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.5/2.1/0.1/0.0 (BP=1.000, ratio=1.056, hyp_len=12922, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.11.4.06-58.04.3.58-36.05.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 22.7/1.2/0.0/0.0 (BP=0.959, ratio=0.960, hyp_len=11737, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.12.3.86-47.65.3.36-28.81.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 22.9/1.9/0.1/0.0 (BP=0.914, ratio=0.918, hyp_len=11225, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.13.3.78-43.68.3.24-25.42.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 25.1/5.1/0.6/0.0 (BP=0.999, ratio=0.999, hyp_len=12216, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.14.3.53-34.25.3.17-23.79.pth
BLEU = 0.13, 3.0/0.7/0.1/0.0 (BP=1.000, ratio=8.050, hyp_len=98464, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.15.3.46-31.89.3.11-22.44.pth
BLEU = 0.10, 1.2/0.3/0.1/0.0 (BP=1.000, ratio=15.805, hyp_len=193310, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.16.3.39-29.75.3.05-21.09.pth
BLEU = 0.28, 3.4/0.9/0.2/0.0 (BP=1.000, ratio=7.942, hyp_len=97135, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.17.3.31-27.50.2.99-19.79.pth
BLEU = 0.36, 3.6/1.0/0.2/0.0 (BP=1.000, ratio=7.584, hyp_len=92755, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.18.3.28-26.66.2.94-18.92.pth
BLEU = 1.64, 13.8/3.8/0.9/0.1 (BP=1.000, ratio=2.298, hyp_len=28104, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.19.3.28-26.50.2.90-18.11.pth
BLEU = 3.34, 22.4/7.2/1.7/0.5 (BP=1.000, ratio=1.446, hyp_len=17686, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.20.3.15-23.41.2.85-17.29.pth
BLEU = 4.96, 27.8/9.6/2.6/0.9 (BP=1.000, ratio=1.195, hyp_len=14619, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.21.3.12-22.62.2.79-16.29.pth
BLEU = 5.06, 27.5/9.8/2.9/0.9 (BP=1.000, ratio=1.225, hyp_len=14983, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.22.3.10-22.12.2.77-16.02.pth
BLEU = 5.76, 27.1/10.0/3.4/1.2 (BP=1.000, ratio=1.332, hyp_len=16289, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.23.3.10-22.24.2.71-15.08.pth
BLEU = 6.30, 29.2/10.9/3.8/1.3 (BP=1.000, ratio=1.207, hyp_len=14757, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.24.2.93-18.67.2.67-14.46.pth
BLEU = 7.93, 32.8/13.1/4.9/1.9 (BP=1.000, ratio=1.119, hyp_len=13682, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.25.2.93-18.73.2.66-14.25.pth
BLEU = 7.87, 33.6/13.4/5.0/1.7 (BP=1.000, ratio=1.109, hyp_len=13567, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.26.2.96-19.28.2.62-13.72.pth
BLEU = 8.44, 34.2/13.8/5.2/2.1 (BP=1.000, ratio=1.101, hyp_len=13463, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.27.2.82-16.70.2.59-13.28.pth
BLEU = 6.45, 26.7/10.8/4.0/1.5 (BP=1.000, ratio=1.414, hyp_len=17300, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.28.2.77-16.01.2.57-13.02.pth
BLEU = 9.06, 33.8/14.2/5.8/2.4 (BP=1.000, ratio=1.148, hyp_len=14044, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.29.2.80-16.50.2.54-12.64.pth
BLEU = 5.19, 19.8/8.3/3.3/1.3 (BP=1.000, ratio=1.946, hyp_len=23802, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.30.2.73-15.33.2.51-12.29.pth
BLEU = 8.96, 32.4/13.7/5.8/2.5 (BP=1.000, ratio=1.215, hyp_len=14863, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.31.2.69-14.68.2.48-11.96.pth
BLEU = 7.75, 28.2/12.0/5.0/2.1 (BP=1.000, ratio=1.426, hyp_len=17447, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.32.2.61-13.63.2.45-11.54.pth
BLEU = 8.89, 30.9/13.5/5.8/2.6 (BP=1.000, ratio=1.295, hyp_len=15835, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.33.2.58-13.26.2.42-11.20.pth
BLEU = 9.44, 32.4/14.3/6.3/2.7 (BP=1.000, ratio=1.266, hyp_len=15486, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.34.2.63-13.82.2.40-11.05.pth
BLEU = 9.07, 30.8/13.7/6.0/2.7 (BP=1.000, ratio=1.326, hyp_len=16213, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.35.2.51-12.27.2.37-10.66.pth
BLEU = 8.22, 27.6/12.2/5.4/2.5 (BP=1.000, ratio=1.499, hyp_len=18331, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.36.2.49-12.03.2.37-10.72.pth
BLEU = 7.72, 26.3/11.5/5.1/2.3 (BP=1.000, ratio=1.581, hyp_len=19341, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.37.2.45-11.59.2.33-10.26.pth
BLEU = 8.54, 28.1/12.5/5.7/2.6 (BP=1.000, ratio=1.486, hyp_len=18176, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.38.2.47-11.80.2.31-10.08.pth
BLEU = 8.25, 27.2/12.1/5.5/2.5 (BP=1.000, ratio=1.550, hyp_len=18964, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.39.2.49-12.03.2.31-10.06.pth
BLEU = 10.38, 32.5/14.9/7.0/3.4 (BP=1.000, ratio=1.322, hyp_len=16173, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.40.2.45-11.56.2.31-10.08.pth
BLEU = 7.15, 22.8/10.4/4.8/2.3 (BP=1.000, ratio=1.857, hyp_len=22715, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.41.2.40-11.05.2.30-9.95.pth
BLEU = 8.77, 27.4/12.6/5.9/2.9 (BP=1.000, ratio=1.578, hyp_len=19297, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.42.2.24-9.40.2.26-9.56.pth
BLEU = 11.08, 33.1/15.5/7.6/3.9 (BP=1.000, ratio=1.326, hyp_len=16224, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.43.2.25-9.50.2.25-9.44.pth
BLEU = 11.62, 35.3/16.5/7.9/4.0 (BP=1.000, ratio=1.259, hyp_len=15396, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.44.2.20-9.04.2.24-9.42.pth
BLEU = 8.32, 25.6/11.8/5.6/2.8 (BP=1.000, ratio=1.704, hyp_len=20844, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.45.2.22-9.17.2.22-9.19.pth
BLEU = 12.13, 35.2/16.8/8.4/4.4 (BP=1.000, ratio=1.285, hyp_len=15714, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.46.2.19-8.96.2.20-9.06.pth
BLEU = 13.57, 40.0/18.9/9.3/4.8 (BP=1.000, ratio=1.133, hyp_len=13863, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.47.2.19-8.98.2.20-9.07.pth
BLEU = 14.32, 41.0/20.0/10.0/5.2 (BP=1.000, ratio=1.109, hyp_len=13565, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.48.2.09-8.07.2.20-9.05.pth
BLEU = 14.18, 39.4/19.3/9.9/5.4 (BP=1.000, ratio=1.171, hyp_len=14321, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.49.2.07-7.93.2.19-8.91.pth
BLEU = 13.39, 38.1/18.5/9.3/4.9 (BP=1.000, ratio=1.216, hyp_len=14873, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.50.2.12-8.29.2.17-8.73.pth
BLEU = 11.99, 34.2/16.7/8.4/4.3 (BP=1.000, ratio=1.366, hyp_len=16702, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.51.2.10-8.20.2.18-8.82.pth
BLEU = 12.97, 37.9/17.9/9.0/4.7 (BP=1.000, ratio=1.216, hyp_len=14871, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.52.2.01-7.47.2.14-8.51.pth
BLEU = 15.16, 41.6/20.8/10.7/5.7 (BP=1.000, ratio=1.138, hyp_len=13916, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.53.1.94-6.93.2.17-8.76.pth
BLEU = 12.90, 35.9/17.8/9.0/4.8 (BP=1.000, ratio=1.310, hyp_len=16028, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.54.1.97-7.18.2.14-8.53.pth
BLEU = 14.87, 40.0/20.1/10.6/5.7 (BP=1.000, ratio=1.183, hyp_len=14468, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.55.1.88-6.58.2.13-8.41.pth
BLEU = 17.49, 46.1/23.7/12.5/6.8 (BP=1.000, ratio=1.030, hyp_len=12601, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.56.1.90-6.67.2.13-8.41.pth
BLEU = 14.54, 39.2/19.5/10.4/5.7 (BP=1.000, ratio=1.213, hyp_len=14836, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.57.1.95-7.03.2.13-8.46.pth
BLEU = 16.14, 43.3/21.7/11.4/6.3 (BP=1.000, ratio=1.109, hyp_len=13567, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.58.1.82-6.19.2.13-8.40.pth
BLEU = 16.89, 44.5/22.9/12.1/6.6 (BP=1.000, ratio=1.098, hyp_len=13424, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.59.1.80-6.02.2.12-8.34.pth
BLEU = 17.67, 46.0/23.6/12.7/7.1 (BP=1.000, ratio=1.065, hyp_len=13021, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.60.1.81-6.13.2.11-8.25.pth
BLEU = 18.36, 46.7/24.3/13.2/7.5 (BP=1.000, ratio=1.037, hyp_len=12678, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.61.1.74-5.70.2.10-8.15.pth
BLEU = 17.00, 44.6/22.8/12.3/6.7 (BP=1.000, ratio=1.107, hyp_len=13544, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.62.1.72-5.61.2.12-8.32.pth
BLEU = 16.12, 43.7/21.9/11.4/6.2 (BP=1.000, ratio=1.122, hyp_len=13724, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.63.1.82-6.16.2.10-8.19.pth
BLEU = 15.85, 41.9/21.3/11.3/6.2 (BP=1.000, ratio=1.169, hyp_len=14303, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.64.1.70-5.48.2.09-8.07.pth
BLEU = 17.92, 45.6/23.7/12.9/7.4 (BP=1.000, ratio=1.087, hyp_len=13295, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.65.1.84-6.28.2.11-8.21.pth
BLEU = 16.83, 44.0/22.5/12.0/6.7 (BP=1.000, ratio=1.115, hyp_len=13633, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.66.1.66-5.27.2.11-8.26.pth
BLEU = 18.49, 45.7/24.0/13.5/7.9 (BP=1.000, ratio=1.079, hyp_len=13202, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.67.1.71-5.54.2.08-8.04.pth
BLEU = 18.32, 47.1/24.4/13.3/7.4 (BP=1.000, ratio=1.051, hyp_len=12857, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.68.1.75-5.78.2.12-8.29.pth
BLEU = 18.73, 46.6/24.5/13.6/7.9 (BP=1.000, ratio=1.067, hyp_len=13048, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.69.1.62-5.04.2.10-8.15.pth
BLEU = 17.23, 43.3/22.6/12.5/7.2 (BP=1.000, ratio=1.146, hyp_len=14012, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.70.1.55-4.71.2.12-8.36.pth
BLEU = 18.33, 46.0/24.1/13.4/7.6 (BP=1.000, ratio=1.063, hyp_len=13003, ref_len=12231)
/home/ye/exp/simple-nmt
==========

```

my-bk အတွဲ testing/evaluation အတွက် ကြာချိန်က အောက်ပါအတိုင်း...  

```
real	50m5.608s
user	48m38.332s
sys	4m18.151s
```

bk-my အတွဲ testing/evaluation အတွက် ကြာချိန်က အောက်ပါအတိုင်း...  

```
real	79m48.118s
user	78m15.186s
sys	4m19.828s
```
my-bk နဲ့ bk-my အတွက် Seq2Seq Baseline Best model တွေနဲ့ Best Score ရလဒ်တွေက အောက်ပါအတိုင်း...  

**for Myanmar-Beik**

<div align="center"> 
    
Table 1. Best model and best score for each baseline training of my-bk pair  
| No of Epoch for Training | Best Model Epoch | Model File | Best BLEU |
|-----------:|-----------:|:-----------:|-----------:|
| 30 | 30 | seq-model-mybk.30.2.80-16.52.2.38-10.84.pth | 9.36 |
| 40 | 40 | seq-model-mybk.40.2.49-12.05.2.17-8.77.pth | 14.15 |
| 50 | 50 | seq-model-mybk.50.2.26-9.59.2.46-11.68.pth | 11.42 |
| 60 | 57 | seq-model-mybk.57.2.06-7.84.2.58-13.15.pth | 10.29 |
| 70 | 68 | seq-model-mybk.68.1.77-5.87.2.39-10.87.pth | 13.40 |

</div>  

**for Beik-Myanmar**

<div align="center"> 
    
Table 2. Best model and best score for each baseline training of bk-my pair 
| No of Epoch for Training | Best Model Epoch | Model File | Best BLEU |
|-----------:|-----------:|:-----------:|-----------:|
| 30 | 30 | seq-model-bkmy.30.2.69-14.67.2.53-12.59.pth | 9.54 |
| 40 | 29 | seq-model-bkmy.29.2.67-14.48.2.59-13.38.pth | 8.70 |
| 50 | 47 | seq-model-bkmy.47.2.18-8.88.2.44-11.52.pth | 10.75 |
| 60 | 57 | seq-model-bkmy.57.1.85-6.35.2.36-10.55.pth | 11.17 |
| 70 | 64 | seq-model-bkmy.64.1.70-5.48.2.09-8.07.pth | 17.92 |

</div>  

## Seq2Seq-RL

နောက်ဆက်တွဲ continuous-training တွေရဲ့ model တွေကိုလည်း ရှေ့မှာ training လုပ်ခဲ့တဲ့ ဖိုလ်ဒါထဲမှာပဲအတူတူ သိမ်းခဲ့တယ်။ အဲဒါကြောင့် 30-epoch ရဲ့ RL model တွေက 30-epoch/ အောက်မှာပဲ ဆက်ရှိမယ်။   

Seq2Seq-RL training (i.e. continue-training) အတွက် ရေးခဲ့တဲ့ bash shell script က အောက်ပါအတိုင်း...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Last updated: 4 April 2022
# a part of Seq2Seq-Reinforcement Learning exp for Myanmar-Beik, Beik-Myanmar
# this script is for CONTINUE-training or RL training.

   echo "mybk, seq2seq-RL training start for 30 epochs...";
   time python continue_train.py --load_fn ./model/rl2/baseline/seq2seq/mybk-30epoch/seq-model-mybk.30.2.80-16.52.2.38-10.84.pth --model_fn ./model/rl2/rl/seq2seq/mybk-30epoch/seq-rl-model-mybk.pth --init_epoch 31 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/seq2seq/mybk-30epoch/con-train.log;

   echo "mybk, seq2seq-RL training start for 40 epochs...";
   time python continue_train.py --load_fn ./model/rl2/baseline/seq2seq/mybk-40epoch/seq-model-mybk.40.2.49-12.05.2.17-8.77.pth --model_fn ./model/rl2/rl/seq2seq/mybk-40epoch/seq-rl-model-mybk.pth --init_epoch 41 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/seq2seq/mybk-40epoch/con-train.log;

   echo "mybk, seq2seq-RL training start for 50 epochs...";
   time python continue_train.py --load_fn ./model/rl2/baseline/seq2seq/mybk-50epoch/seq-model-mybk.50.2.26-9.59.2.46-11.68.pth --model_fn ./model/rl2/rl/seq2seq/mybk-50epoch/seq-rl-model-mybk.pth --init_epoch 51 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/seq2seq/mybk-50epoch/con-train.log;
   
   echo "mybk, seq2seq-RL training start for 60 epochs...";
   time python continue_train.py --load_fn ./model/rl2/baseline/seq2seq/mybk-60epoch/seq-model-mybk.57.2.06-7.84.2.58-13.15.pth --model_fn ./model/rl2/rl/seq2seq/mybk-60epoch/seq-rl-model-mybk.pth --init_epoch 58 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/seq2seq/mybk-60epoch/con-train.log;
   
   echo "mybk, seq2seq-RL training start for 70 epochs...";
   time python continue_train.py --load_fn ./model/rl2/baseline/seq2seq/mybk-70epoch/seq-model-mybk.68.1.77-5.87.2.39-10.87.pth --model_fn ./model/rl2/rl/seq2seq/mybk-70epoch/seq-rl-model-mybk.pth --init_epoch 69 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/seq2seq/mybk-70epoch/con-train.log;
      
echo "####################";

   echo "bkmy, seq2seq-RL training start for 30 epochs...";
   time python continue_train.py --load_fn ./model/rl2/baseline/seq2seq/bkmy-30epoch/seq-model-bkmy.30.2.69-14.67.2.53-12.59.pth --model_fn ./model/rl2/rl/seq2seq/bkmy-30epoch/seq-rl-model-bkmy.pth --init_epoch 31 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/seq2seq/bkmy-30epoch/con-train.log;
   
    echo "bkmy, seq2seq-RL training start for 40 epochs...";
   time python continue_train.py --load_fn ./model/rl2/baseline/seq2seq/bkmy-40epoch/seq-model-bkmy.29.2.67-14.48.2.59-13.38.pth --model_fn ./model/rl2/rl/seq2seq/bkmy-40epoch/seq-rl-model-bkmy.pth --init_epoch 30 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/seq2seq/bkmy-40epoch/con-train.log;
   
    echo "bkmy, seq2seq-RL training start for 50 epochs...";
   time python continue_train.py --load_fn ./model/rl2/baseline/seq2seq/bkmy-50epoch/seq-model-bkmy.47.2.18-8.88.2.44-11.52.pth --model_fn ./model/rl2/rl/seq2seq/bkmy-50epoch/seq-rl-model-bkmy.pth --init_epoch 48 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/seq2seq/bkmy-50epoch/con-train.log;   

    echo "bkmy, seq2seq-RL training start for 60 epochs...";
   time python continue_train.py --load_fn ./model/rl2/baseline/seq2seq/bkmy-60epoch/seq-model-bkmy.57.1.85-6.35.2.36-10.55.pth --model_fn ./model/rl2/rl/seq2seq/bkmy-60epoch/seq-rl-model-bkmy.pth --init_epoch 58 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/seq2seq/bkmy-60epoch/con-train.log;   
   
    echo "bkmy, seq2seq-RL training start for 70 epochs...";
   time python continue_train.py --load_fn ./model/rl2/baseline/seq2seq/bkmy-70epoch/seq-model-bkmy.64.1.70-5.48.2.09-8.07.pth --model_fn ./model/rl2/rl/seq2seq/bkmy-70epoch/seq-rl-model-bkmy.pth --init_epoch 65 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/seq2seq/bkmy-70epoch/con-train.log;   
   
```

training seq2seq-RL ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./rl-seq2seq-con-train.sh | tee rl-seq2seq-con-train-for-mybk-bkmy.log
...
...
...
Epoch 85 - |param|=6.36e+02 |g_param|=5.85e+05 loss=1.5067e+00 ppl=4.51                                                 
Validation - loss=2.5451e+00 ppl=12.74 best_loss=2.3555e+00 best_ppl=10.54                                              
Epoch 86 - |param|=6.36e+02 |g_param|=6.09e+05 loss=1.4256e+00 ppl=4.16                                                 
Validation - loss=2.5168e+00 ppl=12.39 best_loss=2.3555e+00 best_ppl=10.54                                              
Epoch 87 - |param|=6.37e+02 |g_param|=5.74e+05 loss=1.3743e+00 ppl=3.95                                                 
Validation - loss=2.5296e+00 ppl=12.55 best_loss=2.3555e+00 best_ppl=10.54                                              
Epoch 88 - |param|=6.37e+02 |g_param|=6.04e+05 loss=1.3916e+00 ppl=4.02                                                 
Validation - loss=2.5221e+00 ppl=12.45 best_loss=2.3555e+00 best_ppl=10.54                                              
Epoch 89 - |param|=6.37e+02 |g_param|=5.92e+05 loss=1.3638e+00 ppl=3.91                                                 
Validation - loss=2.5422e+00 ppl=12.71 best_loss=2.3555e+00 best_ppl=10.54                                              
Epoch 90 - |param|=6.38e+02 |g_param|=1.03e+06 loss=1.3468e+00 ppl=3.85                                                 
Validation - loss=2.5309e+00 ppl=12.56 best_loss=2.3555e+00 best_ppl=10.54                                              
Epoch 91 - |param|=6.38e+02 |g_param|=6.31e+05 loss=1.3162e+00 ppl=3.73                                                 
Validation - loss=2.5320e+00 ppl=12.58 best_loss=2.3555e+00 best_ppl=10.54                                              
Epoch 92 - |param|=6.39e+02 |g_param|=6.12e+05 loss=1.3751e+00 ppl=3.96                                                 
Validation - loss=2.5347e+00 ppl=12.61 best_loss=2.3555e+00 best_ppl=10.54                                              
Epoch 93 - |param|=6.39e+02 |g_param|=5.95e+05 loss=1.3171e+00 ppl=3.73                                                 
Validation - loss=2.5504e+00 ppl=12.81 best_loss=2.3555e+00 best_ppl=10.54                                              
Epoch 94 - |param|=6.39e+02 |g_param|=6.43e+05 loss=1.3873e+00 ppl=4.00                                                 
Validation - loss=2.5545e+00 ppl=12.87 best_loss=2.3555e+00 best_ppl=10.54                                              
Epoch 95 - |param|=6.40e+02 |g_param|=6.21e+05 loss=1.2943e+00 ppl=3.65                                                 
Validation - loss=2.5574e+00 ppl=12.90 best_loss=2.3555e+00 best_ppl=10.54                                              
Epoch 96 - |param|=6.40e+02 |g_param|=6.06e+05 loss=1.2603e+00 ppl=3.53                                                 
Validation - loss=2.5686e+00 ppl=13.05 best_loss=2.3555e+00 best_ppl=10.54                                              
Epoch 97 - |param|=6.40e+02 |g_param|=6.19e+05 loss=1.3048e+00 ppl=3.69                                                 
Validation - loss=2.5798e+00 ppl=13.19 best_loss=2.3555e+00 best_ppl=10.54                                              
Epoch 98 - |param|=6.41e+02 |g_param|=6.31e+05 loss=1.2796e+00 ppl=3.60                                                 
Validation - loss=2.6101e+00 ppl=13.60 best_loss=2.3555e+00 best_ppl=10.54                                              
Epoch 99 - |param|=6.41e+02 |g_param|=6.16e+05 loss=1.2934e+00 ppl=3.65                                                 
Validation - loss=2.5930e+00 ppl=13.37 best_loss=2.3555e+00 best_ppl=10.54                                              
Epoch 100 - |param|=6.42e+02 |g_param|=6.22e+05 loss=1.2950e+00 ppl=3.65                                                
Validation - loss=2.6141e+00 ppl=13.66 best_loss=2.3555e+00 best_ppl=10.54                                              

real	9m25.741s
user	9m11.242s
sys	0m15.351s
bkmy, seq2seq-RL training start for 70 epochs...
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/rl2/baseline/seq2seq/bkmy-70epoch/seq-model-bkmy.64.1.70-5.48.2.09-8.07.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/rl2/rl/seq2seq/bkmy-70epoch/seq-rl-model-bkmy.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 65
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 128,
    'init_epoch': 65,
    'iteration_per_update': 2,
    'lang': 'bkmy',
    'load_fn': './model/rl2/baseline/seq2seq/bkmy-70epoch/seq-model-bkmy.64.1.70-5.48.2.09-8.07.pth',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/rl2/rl/seq2seq/bkmy-70epoch/seq-rl-model-bkmy.pth',
    'n_epochs': 100,
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
Epoch 65 - |param|=6.27e+02 |g_param|=4.77e+05 loss=1.6796e+00 ppl=5.36                                                 
Validation - loss=2.0957e+00 ppl=8.13 best_loss=inf best_ppl=inf                                                        
Epoch 66 - |param|=6.27e+02 |g_param|=4.81e+05 loss=1.7481e+00 ppl=5.74                                                 
Validation - loss=2.0908e+00 ppl=8.09 best_loss=2.0957e+00 best_ppl=8.13                                                
Epoch 67 - |param|=6.28e+02 |g_param|=4.91e+05 loss=1.6466e+00 ppl=5.19                                                 
Validation - loss=2.0845e+00 ppl=8.04 best_loss=2.0908e+00 best_ppl=8.09                                                
Epoch 68 - |param|=6.28e+02 |g_param|=4.86e+05 loss=1.5973e+00 ppl=4.94                                                 
Validation - loss=2.0882e+00 ppl=8.07 best_loss=2.0845e+00 best_ppl=8.04                                                
Epoch 69 - |param|=6.29e+02 |g_param|=5.03e+05 loss=1.5823e+00 ppl=4.87                                                 
Validation - loss=2.0731e+00 ppl=7.95 best_loss=2.0845e+00 best_ppl=8.04                                                
Epoch 70 - |param|=6.29e+02 |g_param|=5.27e+05 loss=1.6710e+00 ppl=5.32                                                 
Validation - loss=2.0807e+00 ppl=8.01 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 71 - |param|=6.29e+02 |g_param|=4.88e+05 loss=1.5371e+00 ppl=4.65                                                 
Validation - loss=2.0869e+00 ppl=8.06 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 72 - |param|=6.30e+02 |g_param|=5.08e+05 loss=1.6173e+00 ppl=5.04                                                 
Validation - loss=2.0820e+00 ppl=8.02 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 73 - |param|=6.30e+02 |g_param|=5.68e+05 loss=1.6505e+00 ppl=5.21                                                 
Validation - loss=2.0880e+00 ppl=8.07 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 74 - |param|=6.31e+02 |g_param|=4.99e+05 loss=1.5553e+00 ppl=4.74                                                 
Validation - loss=2.0823e+00 ppl=8.02 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 75 - |param|=6.31e+02 |g_param|=5.00e+05 loss=1.4954e+00 ppl=4.46                                                 
Validation - loss=2.0823e+00 ppl=8.02 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 76 - |param|=6.31e+02 |g_param|=5.12e+05 loss=1.5131e+00 ppl=4.54                                                 
Validation - loss=2.0804e+00 ppl=8.01 best_loss=2.0731e+00 best_ppl=7.95                                                
  5%|████▏                                                                                       | 1/22 [00:00<?, ?it/s]Epoch 77 - |param|=6.32e+02 |g_param|=5.11e+05 loss=1.5670e+00 ppl=4.79
Validation - loss=2.0953e+00 ppl=8.13 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 78 - |param|=6.32e+02 |g_param|=5.64e+05 loss=1.4101e+00 ppl=4.10                                                 
Validation - loss=2.0921e+00 ppl=8.10 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 79 - |param|=6.33e+02 |g_param|=5.07e+05 loss=1.4307e+00 ppl=4.18                                                 
Validation - loss=2.0976e+00 ppl=8.15 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 80 - |param|=6.33e+02 |g_param|=5.25e+05 loss=1.3833e+00 ppl=3.99                                                 
Validation - loss=2.1271e+00 ppl=8.39 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 81 - |param|=6.33e+02 |g_param|=5.34e+05 loss=1.4005e+00 ppl=4.06                                                 
Validation - loss=2.1233e+00 ppl=8.36 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 82 - |param|=6.34e+02 |g_param|=5.40e+05 loss=1.4110e+00 ppl=4.10                                                 
Validation - loss=2.1043e+00 ppl=8.20 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 83 - |param|=6.34e+02 |g_param|=5.23e+05 loss=1.3662e+00 ppl=3.92                                                 
Validation - loss=2.1241e+00 ppl=8.37 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 84 - |param|=6.35e+02 |g_param|=5.27e+05 loss=1.3184e+00 ppl=3.74                                                 
Validation - loss=2.1029e+00 ppl=8.19 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 85 - |param|=6.35e+02 |g_param|=5.20e+05 loss=1.2926e+00 ppl=3.64                                                 
Validation - loss=2.1314e+00 ppl=8.43 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 86 - |param|=6.35e+02 |g_param|=5.53e+05 loss=1.2931e+00 ppl=3.64                                                 
Validation - loss=2.1005e+00 ppl=8.17 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 87 - |param|=6.36e+02 |g_param|=5.39e+05 loss=1.3500e+00 ppl=3.86                                                 
Validation - loss=2.1060e+00 ppl=8.22 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 88 - |param|=6.36e+02 |g_param|=5.64e+05 loss=1.2832e+00 ppl=3.61                                                 
Validation - loss=2.1276e+00 ppl=8.40 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 89 - |param|=6.37e+02 |g_param|=5.58e+05 loss=1.2727e+00 ppl=3.57                                                 
Validation - loss=2.1434e+00 ppl=8.53 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 90 - |param|=6.37e+02 |g_param|=5.56e+05 loss=1.2030e+00 ppl=3.33                                                 
Validation - loss=2.1229e+00 ppl=8.36 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 91 - |param|=6.37e+02 |g_param|=5.35e+05 loss=1.2204e+00 ppl=3.39                                                 
Validation - loss=2.0999e+00 ppl=8.17 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 92 - |param|=6.38e+02 |g_param|=5.90e+05 loss=1.2290e+00 ppl=3.42                                                 
Validation - loss=2.1183e+00 ppl=8.32 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 93 - |param|=6.38e+02 |g_param|=5.49e+05 loss=1.1836e+00 ppl=3.27                                                 
Validation - loss=2.1541e+00 ppl=8.62 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 94 - |param|=6.38e+02 |g_param|=3.62e+05 loss=1.2032e+00 ppl=3.33                                                 
Validation - loss=2.1366e+00 ppl=8.47 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 95 - |param|=6.39e+02 |g_param|=2.83e+05 loss=1.1877e+00 ppl=3.28                                                 
Validation - loss=2.1312e+00 ppl=8.42 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 96 - |param|=6.39e+02 |g_param|=3.03e+05 loss=1.2826e+00 ppl=3.61                                                 
Validation - loss=2.1215e+00 ppl=8.34 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 97 - |param|=6.40e+02 |g_param|=2.86e+05 loss=1.2256e+00 ppl=3.41                                                 
Validation - loss=2.1507e+00 ppl=8.59 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 98 - |param|=6.40e+02 |g_param|=2.02e+05 loss=1.1788e+00 ppl=3.25                                                 
Validation - loss=2.1397e+00 ppl=8.50 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 99 - |param|=6.40e+02 |g_param|=1.46e+05 loss=1.2412e+00 ppl=3.46                                                 
Validation - loss=2.1317e+00 ppl=8.43 best_loss=2.0731e+00 best_ppl=7.95                                                
Epoch 100 - |param|=6.41e+02 |g_param|=1.41e+05 loss=1.1487e+00 ppl=3.15                                                
Validation - loss=2.1882e+00 ppl=8.92 best_loss=2.0731e+00 best_ppl=7.95                                                

real	7m32.874s
user	7m23.957s
sys	0m9.694s
```

seq2seq-RL continue-training တစ်ခုလုံးအတွက် ကြာတဲ့အချိန်က အောက်ပါအတိုင်း...  

```
real	89m41.581s
user	87m52.417s
sys	1m56.495s
```

### Testing and Evaluation for Seq2Seq-RL

သုံးခဲ့တဲ့ bash script (test-eval-rl2-seq2seq-RL-mybk-bkmy.sh) က အောက်ပါအတိုင်း...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Last updated: 4 April 2022
# A part of Seq2Seq-Reinforcement Learning exp
# this script is for testing/evaluation of seq2seq-RL for both Myanmar-Beik and Beik-Myanmar

# testing/evaluation baseline for my-bk

for folder in {30,40,50,60,70};
do
   cd ./model/rl2/rl/seq2seq/mybk-${folder}epoch/;
   pwd;
   for i in *.pth; do
      MODEL=$i;

      # Testing
      python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang mybk < /home/ye/exp/simple-nmt/data/my-bk/syl/test.my > ./$MODEL.hyp

      # Evaluation with BLEU Score
      echo "Evaluation result for the model: $MODEL" | tee -a eval-results-mybk-seq2seq-RL-100epoch.txt;
      cat ./$MODEL.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/my-bk/syl/test.bk | tee  -a eval-results-mybk-seq2seq-RL-100epoch.txt;

   done
   cd -; echo "==========";
done

# testing/evaluation baseline for bk-my
for folder in {30,40,50,60,70};
do
   cd ./model/rl2/rl/seq2seq/bkmy-${folder}epoch/;
   pwd;
   for i in *.pth; do
      MODEL=$i;

      # Testing
      python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang bkmy < /home/ye/exp/simple-nmt/data/my-bk/syl/test.bk > ./$MODEL.hyp

      # Evaluation with BLEU Score
      echo "Evaluation result for the model: $MODEL" | tee -a eval-results-bkmy-seq2seq-RL-100epoch.txt;
      cat ./$MODEL.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/my-bk/syl/test.my | tee  -a eval-results-bkmy-seq2seq-RL-100epoch.txt;

   done
   cd -; echo "==========";
done

```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-rl2-seq2seq-RL-mybk-bkmy.sh | tee ./test-eval-rl2-seq2seq-RL-mybk-bkmy.log
/home/ye/exp/simple-nmt/model/rl2/rl/seq2seq/mybk-30epoch
Evaluation result for the model: seq-rl-model-mybk.100.1.24-3.45.2.10-8.14.pth
BLEU = 22.21, 48.7/27.3/16.8/10.9 (BP=1.000, ratio=1.084, hyp_len=12388, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.31.2.70-14.92.2.37-10.68.pth
BLEU = 10.56, 36.0/14.7/6.9/3.4 (BP=1.000, ratio=1.088, hyp_len=12437, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.32.2.67-14.41.2.32-10.21.pth
BLEU = 10.69, 35.5/14.8/7.1/3.5 (BP=1.000, ratio=1.090, hyp_len=12465, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.33.2.57-13.07.2.31-10.06.pth
BLEU = 10.61, 35.3/14.7/7.1/3.4 (BP=1.000, ratio=1.136, hyp_len=12989, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.34.2.62-13.75.2.29-9.86.pth
BLEU = 11.36, 36.3/15.4/7.6/3.9 (BP=1.000, ratio=1.108, hyp_len=12669, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.35.2.49-12.12.2.25-9.50.pth
BLEU = 12.58, 38.6/16.8/8.5/4.5 (BP=1.000, ratio=1.068, hyp_len=12207, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.36.2.45-11.63.2.24-9.36.pth
BLEU = 12.60, 38.3/16.9/8.6/4.6 (BP=1.000, ratio=1.060, hyp_len=12121, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.37.2.40-11.05.2.22-9.18.pth
BLEU = 12.88, 38.1/17.2/8.9/4.7 (BP=1.000, ratio=1.111, hyp_len=12697, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.38.2.50-12.22.2.22-9.17.pth
BLEU = 13.74, 40.5/18.4/9.5/5.1 (BP=1.000, ratio=1.045, hyp_len=11950, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.39.2.37-10.68.2.18-8.89.pth
BLEU = 13.87, 39.6/18.1/9.6/5.4 (BP=1.000, ratio=1.110, hyp_len=12691, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.40.2.35-10.51.2.16-8.68.pth
BLEU = 14.61, 40.9/19.1/10.1/5.7 (BP=1.000, ratio=1.095, hyp_len=12513, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.41.2.31-10.03.2.15-8.58.pth
BLEU = 13.92, 40.1/18.6/9.7/5.2 (BP=1.000, ratio=1.082, hyp_len=12374, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.42.2.26-9.63.2.15-8.56.pth
BLEU = 14.37, 39.9/18.5/10.0/5.8 (BP=1.000, ratio=1.081, hyp_len=12355, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.43.2.16-8.69.2.14-8.50.pth
BLEU = 15.49, 41.7/20.0/11.0/6.3 (BP=1.000, ratio=1.075, hyp_len=12293, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.44.2.15-8.61.2.11-8.29.pth
BLEU = 15.78, 42.7/20.5/11.2/6.3 (BP=1.000, ratio=1.054, hyp_len=12048, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.45.2.09-8.07.2.11-8.21.pth
BLEU = 15.54, 41.2/20.2/11.1/6.3 (BP=1.000, ratio=1.092, hyp_len=12487, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.46.2.11-8.21.2.10-8.21.pth
BLEU = 16.71, 44.1/21.7/11.9/6.9 (BP=1.000, ratio=1.032, hyp_len=11799, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.47.2.14-8.53.2.09-8.12.pth
BLEU = 16.16, 42.2/20.8/11.6/6.7 (BP=1.000, ratio=1.081, hyp_len=12353, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.48.2.02-7.50.2.06-7.85.pth
BLEU = 17.69, 44.2/22.6/12.8/7.6 (BP=1.000, ratio=1.065, hyp_len=12171, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.49.2.15-8.59.2.07-7.91.pth
BLEU = 17.64, 44.6/22.7/12.8/7.5 (BP=1.000, ratio=1.081, hyp_len=12355, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.50.1.98-7.27.2.08-7.99.pth
BLEU = 17.76, 45.1/22.8/12.8/7.6 (BP=1.000, ratio=1.062, hyp_len=12143, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.51.2.06-7.82.2.06-7.81.pth
BLEU = 16.94, 43.0/21.6/12.2/7.3 (BP=1.000, ratio=1.116, hyp_len=12760, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.52.1.94-6.97.2.05-7.79.pth
BLEU = 17.75, 43.9/22.5/12.9/7.8 (BP=1.000, ratio=1.075, hyp_len=12291, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.53.1.98-7.21.2.03-7.59.pth
BLEU = 19.13, 46.0/24.0/14.1/8.6 (BP=1.000, ratio=1.051, hyp_len=12010, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.54.1.98-7.24.2.04-7.65.pth
BLEU = 18.00, 45.0/23.0/13.1/7.8 (BP=1.000, ratio=1.072, hyp_len=12251, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.55.1.91-6.78.2.01-7.44.pth
BLEU = 19.39, 47.4/24.7/14.1/8.5 (BP=1.000, ratio=1.034, hyp_len=11817, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.56.1.86-6.39.2.05-7.74.pth
BLEU = 19.01, 46.2/24.1/14.0/8.4 (BP=1.000, ratio=1.070, hyp_len=12228, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.57.1.84-6.28.2.04-7.66.pth
BLEU = 19.21, 46.6/24.1/14.0/8.7 (BP=1.000, ratio=1.046, hyp_len=11961, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.58.1.82-6.16.2.03-7.63.pth
BLEU = 18.73, 45.1/23.6/13.9/8.3 (BP=1.000, ratio=1.090, hyp_len=12463, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.59.1.84-6.30.2.06-7.84.pth
BLEU = 19.59, 46.3/24.4/14.4/9.0 (BP=1.000, ratio=1.085, hyp_len=12409, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.60.1.80-6.04.2.02-7.53.pth
BLEU = 19.98, 46.6/25.0/14.9/9.2 (BP=1.000, ratio=1.099, hyp_len=12567, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.61.1.80-6.07.2.03-7.62.pth
BLEU = 20.45, 47.9/25.7/15.2/9.4 (BP=1.000, ratio=1.053, hyp_len=12034, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.62.1.78-5.95.2.06-7.87.pth
BLEU = 19.13, 45.1/24.0/14.2/8.7 (BP=1.000, ratio=1.105, hyp_len=12634, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.63.1.81-6.13.2.00-7.41.pth
BLEU = 20.65, 48.1/25.8/15.3/9.6 (BP=1.000, ratio=1.050, hyp_len=12005, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.64.1.70-5.50.2.00-7.39.pth
BLEU = 21.44, 48.9/26.6/16.1/10.1 (BP=1.000, ratio=1.045, hyp_len=11944, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.65.1.64-5.13.2.04-7.66.pth
BLEU = 20.17, 47.2/25.1/14.9/9.4 (BP=1.000, ratio=1.073, hyp_len=12267, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.66.1.67-5.29.2.02-7.51.pth
BLEU = 20.78, 47.6/25.7/15.4/9.9 (BP=1.000, ratio=1.085, hyp_len=12405, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.67.1.71-5.55.2.02-7.53.pth
BLEU = 20.89, 47.9/25.9/15.6/9.9 (BP=1.000, ratio=1.050, hyp_len=11998, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.68.1.60-4.94.2.00-7.35.pth
BLEU = 21.13, 48.1/26.3/16.0/9.9 (BP=1.000, ratio=1.070, hyp_len=12229, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.69.1.65-5.21.2.02-7.52.pth
BLEU = 21.29, 48.4/26.5/16.1/10.0 (BP=1.000, ratio=1.070, hyp_len=12228, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.70.1.60-4.95.2.02-7.53.pth
BLEU = 21.81, 48.6/26.8/16.5/10.5 (BP=1.000, ratio=1.063, hyp_len=12148, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.71.1.55-4.73.2.05-7.77.pth
BLEU = 20.73, 47.1/25.7/15.6/9.8 (BP=1.000, ratio=1.074, hyp_len=12281, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.72.1.55-4.70.2.02-7.54.pth
BLEU = 21.85, 47.8/26.7/16.6/10.8 (BP=1.000, ratio=1.094, hyp_len=12509, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.73.1.54-4.69.2.02-7.55.pth
BLEU = 21.13, 47.5/26.1/16.0/10.0 (BP=1.000, ratio=1.082, hyp_len=12367, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.74.1.50-4.49.2.01-7.43.pth
BLEU = 21.53, 48.2/26.4/16.2/10.4 (BP=1.000, ratio=1.065, hyp_len=12176, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.75.1.53-4.64.2.02-7.55.pth
BLEU = 21.05, 47.5/26.0/15.8/10.0 (BP=1.000, ratio=1.106, hyp_len=12649, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.76.1.50-4.50.2.01-7.48.pth
BLEU = 22.14, 49.0/27.2/16.8/10.7 (BP=1.000, ratio=1.066, hyp_len=12185, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.77.1.60-4.95.2.03-7.61.pth
BLEU = 22.39, 49.8/27.6/16.9/10.8 (BP=1.000, ratio=1.053, hyp_len=12035, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.78.1.59-4.92.2.03-7.59.pth
BLEU = 21.41, 48.3/26.5/16.1/10.2 (BP=1.000, ratio=1.059, hyp_len=12108, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.79.1.45-4.27.2.07-7.95.pth
BLEU = 21.00, 47.5/25.8/15.7/10.1 (BP=1.000, ratio=1.078, hyp_len=12321, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.80.1.50-4.47.2.05-7.75.pth
BLEU = 20.35, 46.9/25.1/15.2/9.6 (BP=1.000, ratio=1.094, hyp_len=12507, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.81.1.40-4.05.2.00-7.38.pth
BLEU = 22.61, 49.5/27.8/17.1/11.1 (BP=1.000, ratio=1.098, hyp_len=12550, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.82.1.40-4.07.2.00-7.38.pth
BLEU = 22.82, 49.5/27.8/17.5/11.2 (BP=1.000, ratio=1.074, hyp_len=12283, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.83.1.45-4.26.2.05-7.74.pth
BLEU = 21.45, 47.5/26.3/16.2/10.5 (BP=1.000, ratio=1.073, hyp_len=12266, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.84.1.38-3.97.2.08-7.97.pth
BLEU = 22.21, 48.5/27.0/16.9/11.0 (BP=1.000, ratio=1.062, hyp_len=12141, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.85.1.40-4.06.2.05-7.80.pth
BLEU = 22.04, 48.5/27.0/16.7/10.8 (BP=1.000, ratio=1.078, hyp_len=12322, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.86.1.37-3.92.2.02-7.53.pth
BLEU = 22.64, 49.8/28.0/17.3/10.9 (BP=1.000, ratio=1.060, hyp_len=12113, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.87.1.38-3.98.2.04-7.66.pth
BLEU = 22.14, 48.8/27.3/16.8/10.7 (BP=1.000, ratio=1.068, hyp_len=12207, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.88.1.33-3.76.2.03-7.59.pth
BLEU = 22.63, 49.5/27.7/17.2/11.1 (BP=1.000, ratio=1.080, hyp_len=12349, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.89.1.35-3.87.2.06-7.87.pth
BLEU = 22.26, 48.9/27.2/16.9/10.9 (BP=1.000, ratio=1.068, hyp_len=12207, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.90.1.25-3.50.2.02-7.54.pth
BLEU = 22.24, 49.5/27.5/16.9/10.6 (BP=1.000, ratio=1.080, hyp_len=12350, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.91.1.39-4.01.2.08-8.04.pth
BLEU = 22.17, 48.7/27.0/16.8/10.9 (BP=1.000, ratio=1.078, hyp_len=12327, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.92.1.31-3.70.2.08-7.98.pth
BLEU = 21.66, 47.8/26.5/16.4/10.6 (BP=1.000, ratio=1.088, hyp_len=12437, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.93.1.28-3.58.2.05-7.78.pth
BLEU = 21.58, 48.1/26.6/16.3/10.4 (BP=1.000, ratio=1.093, hyp_len=12497, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.94.1.21-3.35.2.04-7.66.pth
BLEU = 21.99, 48.4/26.9/16.7/10.8 (BP=1.000, ratio=1.074, hyp_len=12283, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.95.1.28-3.58.2.06-7.82.pth
BLEU = 22.48, 49.4/27.5/17.0/11.1 (BP=1.000, ratio=1.076, hyp_len=12303, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.96.1.21-3.35.2.05-7.79.pth
BLEU = 22.57, 49.4/27.5/17.1/11.2 (BP=1.000, ratio=1.059, hyp_len=12104, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.97.1.24-3.44.2.09-8.10.pth
BLEU = 22.82, 48.9/27.5/17.6/11.5 (BP=1.000, ratio=1.077, hyp_len=12315, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.98.1.18-3.26.2.12-8.32.pth
BLEU = 22.02, 48.2/26.8/16.8/10.8 (BP=1.000, ratio=1.073, hyp_len=12268, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.99.1.19-3.30.2.06-7.83.pth
BLEU = 22.38, 48.7/27.2/17.1/11.1 (BP=1.000, ratio=1.084, hyp_len=12395, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/seq2seq/mybk-40epoch
Evaluation result for the model: seq-rl-model-mybk.100.1.22-3.38.2.12-8.34.pth
BLEU = 22.22, 48.6/27.1/16.8/11.1 (BP=1.000, ratio=1.097, hyp_len=12540, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.41.2.40-11.03.2.22-9.21.pth
BLEU = 14.28, 40.1/18.3/10.0/5.7 (BP=1.000, ratio=1.096, hyp_len=12526, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.42.2.37-10.69.2.15-8.56.pth
BLEU = 15.26, 41.8/19.9/10.7/6.1 (BP=1.000, ratio=1.071, hyp_len=12245, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.43.2.25-9.50.2.15-8.59.pth
BLEU = 15.79, 42.3/20.1/11.3/6.5 (BP=1.000, ratio=1.062, hyp_len=12141, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.44.2.15-8.58.2.11-8.22.pth
BLEU = 16.00, 41.4/20.4/11.5/6.7 (BP=1.000, ratio=1.104, hyp_len=12617, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.45.2.22-9.20.2.09-8.09.pth
BLEU = 16.63, 42.6/21.2/12.0/7.1 (BP=1.000, ratio=1.073, hyp_len=12272, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.46.2.12-8.34.2.08-7.98.pth
BLEU = 17.91, 45.1/22.9/13.1/7.6 (BP=1.000, ratio=1.057, hyp_len=12082, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.47.2.12-8.31.2.10-8.13.pth
BLEU = 16.88, 43.4/22.0/12.2/7.0 (BP=1.000, ratio=1.094, hyp_len=12507, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.48.2.07-7.89.2.04-7.70.pth
BLEU = 18.65, 45.8/23.4/13.6/8.3 (BP=1.000, ratio=1.050, hyp_len=12006, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.49.2.05-7.76.2.06-7.81.pth
BLEU = 18.35, 45.0/23.0/13.4/8.2 (BP=1.000, ratio=1.072, hyp_len=12251, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.50.2.03-7.60.2.05-7.81.pth
BLEU = 18.16, 44.7/22.7/13.2/8.1 (BP=1.000, ratio=1.080, hyp_len=12347, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.51.2.00-7.42.2.01-7.50.pth
BLEU = 19.04, 45.9/24.2/14.0/8.4 (BP=1.000, ratio=1.076, hyp_len=12305, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.52.2.00-7.41.2.02-7.57.pth
BLEU = 19.70, 47.1/24.8/14.5/8.9 (BP=1.000, ratio=1.074, hyp_len=12273, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.53.2.10-8.17.2.01-7.45.pth
BLEU = 18.79, 45.3/23.8/13.8/8.3 (BP=1.000, ratio=1.095, hyp_len=12521, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.54.1.94-6.98.2.03-7.64.pth
BLEU = 19.64, 46.1/24.5/14.6/9.0 (BP=1.000, ratio=1.094, hyp_len=12506, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.55.1.95-7.00.2.03-7.64.pth
BLEU = 19.85, 46.7/24.8/14.7/9.1 (BP=1.000, ratio=1.078, hyp_len=12327, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.56.1.91-6.73.1.99-7.32.pth
BLEU = 20.45, 47.9/25.8/15.2/9.3 (BP=1.000, ratio=1.068, hyp_len=12213, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.57.1.98-7.26.2.05-7.75.pth
BLEU = 20.03, 46.3/24.8/15.0/9.4 (BP=1.000, ratio=1.088, hyp_len=12436, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.58.1.91-6.76.2.03-7.59.pth
BLEU = 20.12, 46.7/25.1/15.0/9.3 (BP=1.000, ratio=1.084, hyp_len=12391, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.59.1.83-6.25.2.02-7.56.pth
BLEU = 20.70, 47.6/26.1/15.5/9.5 (BP=1.000, ratio=1.076, hyp_len=12304, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.60.1.77-5.87.2.02-7.54.pth
BLEU = 20.49, 46.9/25.3/15.2/9.7 (BP=1.000, ratio=1.065, hyp_len=12174, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.61.1.89-6.65.2.00-7.37.pth
BLEU = 21.52, 48.8/26.9/16.1/10.1 (BP=1.000, ratio=1.056, hyp_len=12075, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.62.1.78-5.93.1.98-7.27.pth
BLEU = 20.69, 47.2/25.5/15.4/9.9 (BP=1.000, ratio=1.085, hyp_len=12401, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.63.1.70-5.50.1.98-7.21.pth
BLEU = 22.25, 48.7/27.1/16.9/11.0 (BP=1.000, ratio=1.075, hyp_len=12293, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.64.1.70-5.48.2.04-7.70.pth
BLEU = 20.29, 46.3/25.4/15.2/9.5 (BP=1.000, ratio=1.105, hyp_len=12638, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.65.1.74-5.67.2.00-7.39.pth
BLEU = 21.61, 48.4/26.8/16.3/10.3 (BP=1.000, ratio=1.087, hyp_len=12432, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.66.1.69-5.43.2.01-7.50.pth
BLEU = 21.21, 47.7/26.3/15.9/10.1 (BP=1.000, ratio=1.097, hyp_len=12539, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.67.1.71-5.53.2.01-7.43.pth
BLEU = 21.87, 48.5/26.9/16.4/10.7 (BP=1.000, ratio=1.081, hyp_len=12354, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.68.1.60-4.94.2.02-7.57.pth
BLEU = 21.22, 47.2/26.2/16.0/10.2 (BP=1.000, ratio=1.092, hyp_len=12489, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.69.1.64-5.17.2.00-7.42.pth
BLEU = 21.77, 47.7/26.7/16.5/10.7 (BP=1.000, ratio=1.093, hyp_len=12497, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.70.1.60-4.95.2.00-7.38.pth
BLEU = 22.08, 48.7/27.1/16.6/10.9 (BP=1.000, ratio=1.093, hyp_len=12495, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.71.1.60-4.95.2.00-7.42.pth
BLEU = 22.55, 49.4/27.9/17.1/10.9 (BP=1.000, ratio=1.077, hyp_len=12314, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.72.1.55-4.69.2.01-7.50.pth
BLEU = 22.74, 49.8/28.2/17.3/11.0 (BP=1.000, ratio=1.083, hyp_len=12377, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.73.1.56-4.76.2.00-7.38.pth
BLEU = 22.46, 48.8/27.4/17.1/11.1 (BP=1.000, ratio=1.092, hyp_len=12481, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.74.1.50-4.50.2.02-7.57.pth
BLEU = 22.89, 49.6/27.8/17.3/11.5 (BP=1.000, ratio=1.093, hyp_len=12499, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.75.1.48-4.40.2.00-7.42.pth
BLEU = 23.09, 49.2/28.1/17.7/11.6 (BP=1.000, ratio=1.081, hyp_len=12354, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.76.1.50-4.46.2.05-7.73.pth
BLEU = 21.54, 48.0/26.4/16.2/10.5 (BP=1.000, ratio=1.100, hyp_len=12571, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.77.1.56-4.77.2.01-7.43.pth
BLEU = 23.16, 50.1/28.5/17.6/11.4 (BP=1.000, ratio=1.091, hyp_len=12467, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.78.1.50-4.49.1.99-7.30.pth
BLEU = 23.42, 50.1/28.5/17.9/11.8 (BP=1.000, ratio=1.082, hyp_len=12368, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.79.1.44-4.21.2.04-7.66.pth
BLEU = 23.16, 50.3/28.4/17.6/11.4 (BP=1.000, ratio=1.075, hyp_len=12287, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.80.1.47-4.34.2.03-7.63.pth
BLEU = 23.10, 49.2/28.1/17.7/11.6 (BP=1.000, ratio=1.080, hyp_len=12342, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.81.1.44-4.22.2.00-7.38.pth
BLEU = 22.85, 49.5/28.1/17.4/11.2 (BP=1.000, ratio=1.087, hyp_len=12427, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.82.1.43-4.20.2.04-7.66.pth
BLEU = 23.16, 49.4/28.0/17.7/11.8 (BP=1.000, ratio=1.085, hyp_len=12403, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.83.1.37-3.94.2.04-7.73.pth
BLEU = 22.55, 48.9/27.5/17.1/11.3 (BP=1.000, ratio=1.084, hyp_len=12390, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.84.1.44-4.23.2.05-7.74.pth
BLEU = 22.85, 49.3/28.0/17.5/11.3 (BP=1.000, ratio=1.085, hyp_len=12400, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.85.1.40-4.05.2.02-7.52.pth
BLEU = 22.69, 49.5/27.8/17.2/11.2 (BP=1.000, ratio=1.085, hyp_len=12403, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.86.1.33-3.79.2.06-7.82.pth
BLEU = 23.34, 50.0/28.4/17.8/11.8 (BP=1.000, ratio=1.073, hyp_len=12262, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.87.1.30-3.68.2.04-7.66.pth
BLEU = 23.16, 49.2/28.0/17.8/11.8 (BP=1.000, ratio=1.088, hyp_len=12441, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.88.1.36-3.90.2.04-7.66.pth
BLEU = 23.32, 49.9/28.4/17.8/11.7 (BP=1.000, ratio=1.081, hyp_len=12354, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.89.1.37-3.95.2.09-8.10.pth
BLEU = 22.76, 49.5/27.9/17.3/11.3 (BP=1.000, ratio=1.096, hyp_len=12535, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.90.1.34-3.82.2.09-8.06.pth
BLEU = 22.48, 48.4/27.4/17.1/11.3 (BP=1.000, ratio=1.116, hyp_len=12756, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.91.1.32-3.76.2.05-7.74.pth
BLEU = 21.60, 47.6/26.6/16.2/10.6 (BP=1.000, ratio=1.121, hyp_len=12819, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.92.1.28-3.60.2.03-7.63.pth
BLEU = 22.60, 49.2/27.7/17.1/11.2 (BP=1.000, ratio=1.090, hyp_len=12459, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.93.1.34-3.81.2.06-7.85.pth
BLEU = 22.26, 48.5/27.2/16.8/11.1 (BP=1.000, ratio=1.089, hyp_len=12452, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.94.1.24-3.47.2.12-8.30.pth
BLEU = 22.03, 48.1/26.8/16.6/11.0 (BP=1.000, ratio=1.116, hyp_len=12755, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.95.1.25-3.49.2.03-7.59.pth
BLEU = 23.23, 49.4/28.0/17.7/11.9 (BP=1.000, ratio=1.084, hyp_len=12388, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.96.1.27-3.55.2.03-7.65.pth
BLEU = 23.37, 49.4/28.1/17.9/12.0 (BP=1.000, ratio=1.094, hyp_len=12510, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.97.1.22-3.40.2.08-8.00.pth
BLEU = 22.66, 48.6/27.6/17.3/11.3 (BP=1.000, ratio=1.085, hyp_len=12405, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.98.1.19-3.29.2.09-8.05.pth
BLEU = 23.61, 49.6/28.5/18.0/12.2 (BP=1.000, ratio=1.083, hyp_len=12377, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.99.1.23-3.43.2.05-7.77.pth
BLEU = 23.72, 50.4/28.7/18.1/12.1 (BP=1.000, ratio=1.067, hyp_len=12198, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/seq2seq/mybk-50epoch
Evaluation result for the model: seq-rl-model-mybk.100.1.39-4.00.2.63-13.93.pth
BLEU = 12.28, 38.3/16.3/8.1/4.5 (BP=1.000, ratio=1.107, hyp_len=12656, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.51.2.22-9.16.2.45-11.59.pth
BLEU = 11.27, 37.1/15.5/7.6/3.7 (BP=1.000, ratio=1.068, hyp_len=12215, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.52.2.11-8.28.2.48-11.99.pth
BLEU = 11.44, 37.2/15.5/7.7/3.9 (BP=1.000, ratio=1.079, hyp_len=12338, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.53.2.14-8.53.2.49-12.11.pth
BLEU = 11.24, 36.9/15.4/7.5/3.7 (BP=1.000, ratio=1.090, hyp_len=12458, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.54.2.18-8.85.2.48-11.98.pth
BLEU = 11.70, 37.5/15.9/7.8/4.0 (BP=1.000, ratio=1.067, hyp_len=12201, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.55.2.15-8.55.2.52-12.44.pth
BLEU = 11.91, 37.2/15.9/7.9/4.3 (BP=1.000, ratio=1.091, hyp_len=12474, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.56.2.04-7.69.2.53-12.60.pth
BLEU = 11.70, 37.7/15.7/7.8/4.1 (BP=1.000, ratio=1.064, hyp_len=12159, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.57.2.03-7.59.2.51-12.36.pth
BLEU = 12.30, 38.1/16.3/8.3/4.4 (BP=1.000, ratio=1.060, hyp_len=12121, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.58.2.07-7.96.2.51-12.25.pth
BLEU = 11.84, 37.5/15.8/7.9/4.2 (BP=1.000, ratio=1.091, hyp_len=12472, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.59.2.01-7.43.2.49-12.09.pth
BLEU = 12.49, 38.5/16.6/8.3/4.6 (BP=1.000, ratio=1.076, hyp_len=12305, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.60.1.99-7.33.2.47-11.82.pth
BLEU = 12.04, 38.2/16.2/8.1/4.2 (BP=1.000, ratio=1.057, hyp_len=12082, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.61.1.95-7.06.2.49-12.01.pth
BLEU = 12.24, 38.4/16.4/8.3/4.3 (BP=1.000, ratio=1.077, hyp_len=12307, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.62.1.92-6.80.2.50-12.17.pth
BLEU = 12.07, 38.1/16.2/8.1/4.3 (BP=1.000, ratio=1.065, hyp_len=12179, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.63.1.90-6.71.2.50-12.12.pth
BLEU = 11.74, 37.3/15.8/7.9/4.1 (BP=1.000, ratio=1.104, hyp_len=12620, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.64.1.94-6.97.2.49-12.09.pth
BLEU = 11.98, 37.2/15.8/8.1/4.4 (BP=1.000, ratio=1.114, hyp_len=12740, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.65.1.85-6.37.2.50-12.16.pth
BLEU = 12.53, 39.0/16.5/8.3/4.6 (BP=1.000, ratio=1.075, hyp_len=12287, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.66.1.94-6.95.2.48-11.95.pth
BLEU = 12.64, 38.9/16.8/8.5/4.6 (BP=1.000, ratio=1.078, hyp_len=12318, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.67.1.83-6.25.2.50-12.17.pth
BLEU = 12.76, 38.6/16.9/8.6/4.7 (BP=1.000, ratio=1.087, hyp_len=12430, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.68.1.81-6.10.2.49-12.09.pth
BLEU = 12.69, 39.1/17.1/8.5/4.5 (BP=1.000, ratio=1.071, hyp_len=12243, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.69.1.78-5.94.2.48-11.98.pth
BLEU = 12.50, 38.0/16.6/8.4/4.6 (BP=1.000, ratio=1.099, hyp_len=12566, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.70.1.80-6.06.2.53-12.52.pth
BLEU = 12.70, 38.6/17.0/8.5/4.6 (BP=1.000, ratio=1.097, hyp_len=12539, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.71.1.75-5.75.2.53-12.52.pth
BLEU = 12.41, 38.0/16.2/8.3/4.6 (BP=1.000, ratio=1.098, hyp_len=12548, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.72.1.69-5.40.2.50-12.15.pth
BLEU = 13.15, 39.2/17.1/8.9/5.0 (BP=1.000, ratio=1.082, hyp_len=12367, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.73.1.70-5.50.2.51-12.34.pth
BLEU = 12.31, 38.8/16.7/8.3/4.3 (BP=1.000, ratio=1.103, hyp_len=12610, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.74.1.68-5.37.2.53-12.55.pth
BLEU = 12.37, 38.2/16.6/8.4/4.4 (BP=1.000, ratio=1.124, hyp_len=12851, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.75.1.73-5.62.2.55-12.80.pth
BLEU = 12.09, 38.1/16.6/8.2/4.1 (BP=1.000, ratio=1.100, hyp_len=12574, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.76.1.65-5.19.2.52-12.42.pth
BLEU = 12.49, 38.4/16.7/8.4/4.5 (BP=1.000, ratio=1.096, hyp_len=12534, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.77.1.70-5.50.2.54-12.66.pth
BLEU = 12.50, 38.2/16.7/8.4/4.5 (BP=1.000, ratio=1.116, hyp_len=12757, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.78.1.59-4.91.2.50-12.23.pth
BLEU = 12.76, 38.9/16.8/8.6/4.7 (BP=1.000, ratio=1.083, hyp_len=12380, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.79.1.64-5.16.2.54-12.63.pth
BLEU = 12.49, 38.0/16.4/8.3/4.7 (BP=1.000, ratio=1.115, hyp_len=12747, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.80.1.60-4.96.2.54-12.71.pth
BLEU = 13.04, 39.0/17.1/8.8/4.9 (BP=1.000, ratio=1.099, hyp_len=12566, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.81.1.57-4.79.2.54-12.64.pth
BLEU = 12.43, 38.0/16.2/8.3/4.7 (BP=1.000, ratio=1.125, hyp_len=12859, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.82.1.57-4.83.2.55-12.86.pth
BLEU = 12.34, 37.9/16.3/8.4/4.5 (BP=1.000, ratio=1.105, hyp_len=12632, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.83.1.53-4.63.2.56-12.95.pth
BLEU = 12.38, 38.7/16.6/8.2/4.4 (BP=1.000, ratio=1.106, hyp_len=12648, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.84.1.51-4.55.2.57-13.00.pth
BLEU = 12.87, 39.2/17.1/8.6/4.7 (BP=1.000, ratio=1.096, hyp_len=12527, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.85.1.52-4.55.2.54-12.74.pth
BLEU = 13.50, 39.1/17.5/9.1/5.3 (BP=1.000, ratio=1.082, hyp_len=12364, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.86.1.48-4.41.2.58-13.23.pth
BLEU = 12.86, 38.5/16.8/8.7/4.9 (BP=1.000, ratio=1.095, hyp_len=12516, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.87.1.49-4.44.2.56-12.91.pth
BLEU = 13.38, 40.0/17.5/9.0/5.1 (BP=1.000, ratio=1.063, hyp_len=12147, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.88.1.59-4.90.2.59-13.30.pth
BLEU = 13.08, 39.6/17.4/8.8/4.8 (BP=1.000, ratio=1.089, hyp_len=12446, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.89.1.45-4.25.2.61-13.58.pth
BLEU = 13.18, 39.3/17.3/9.0/4.9 (BP=1.000, ratio=1.092, hyp_len=12486, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.90.1.45-4.26.2.57-13.06.pth
BLEU = 13.46, 39.7/17.7/9.1/5.1 (BP=1.000, ratio=1.077, hyp_len=12309, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.91.1.49-4.44.2.60-13.41.pth
BLEU = 13.05, 39.4/17.0/8.8/4.9 (BP=1.000, ratio=1.094, hyp_len=12503, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.92.1.42-4.14.2.63-13.88.pth
BLEU = 12.64, 38.5/16.7/8.5/4.7 (BP=1.000, ratio=1.109, hyp_len=12675, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.93.1.48-4.38.2.60-13.50.pth
BLEU = 13.01, 39.3/17.1/8.8/4.9 (BP=1.000, ratio=1.095, hyp_len=12519, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.94.1.40-4.07.2.61-13.64.pth
BLEU = 12.09, 38.0/16.1/8.0/4.4 (BP=1.000, ratio=1.122, hyp_len=12831, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.95.1.45-4.26.2.62-13.69.pth
BLEU = 12.74, 38.5/16.6/8.5/4.8 (BP=1.000, ratio=1.103, hyp_len=12614, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.96.1.36-3.90.2.64-13.96.pth
BLEU = 12.48, 38.3/16.5/8.3/4.7 (BP=1.000, ratio=1.124, hyp_len=12850, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.97.1.33-3.79.2.65-14.11.pth
BLEU = 13.17, 38.9/17.1/8.8/5.1 (BP=1.000, ratio=1.103, hyp_len=12607, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.98.1.35-3.88.2.61-13.54.pth
BLEU = 12.47, 38.3/16.4/8.4/4.6 (BP=1.000, ratio=1.097, hyp_len=12537, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.99.1.37-3.93.2.62-13.70.pth
BLEU = 12.94, 38.6/16.7/8.7/5.0 (BP=1.000, ratio=1.110, hyp_len=12690, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/seq2seq/mybk-60epoch
Evaluation result for the model: seq-rl-model-mybk.100.1.38-3.97.2.78-16.17.pth
BLEU = 11.28, 36.4/15.3/7.5/3.9 (BP=1.000, ratio=1.092, hyp_len=12489, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.58.2.05-7.73.2.59-13.35.pth
BLEU = 10.26, 34.5/13.9/6.7/3.5 (BP=1.000, ratio=1.075, hyp_len=12289, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.59.2.10-8.18.2.60-13.47.pth
BLEU = 10.16, 33.7/13.7/6.7/3.5 (BP=1.000, ratio=1.116, hyp_len=12763, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.60.1.98-7.27.2.58-13.21.pth
BLEU = 10.13, 33.9/14.0/6.7/3.3 (BP=1.000, ratio=1.111, hyp_len=12705, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.61.2.02-7.55.2.58-13.24.pth
BLEU = 10.60, 35.0/14.3/7.1/3.6 (BP=1.000, ratio=1.067, hyp_len=12194, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.62.1.96-7.11.2.58-13.21.pth
BLEU = 10.45, 35.1/14.3/6.9/3.5 (BP=1.000, ratio=1.068, hyp_len=12204, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.63.1.98-7.23.2.59-13.35.pth
BLEU = 10.24, 34.5/13.9/6.7/3.4 (BP=1.000, ratio=1.102, hyp_len=12593, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.64.1.91-6.74.2.58-13.16.pth
BLEU = 9.94, 33.7/13.8/6.5/3.2 (BP=1.000, ratio=1.100, hyp_len=12580, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.65.1.92-6.81.2.61-13.56.pth
BLEU = 9.98, 34.3/13.7/6.5/3.2 (BP=1.000, ratio=1.101, hyp_len=12591, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.66.1.92-6.85.2.62-13.74.pth
BLEU = 10.22, 34.2/13.8/6.7/3.4 (BP=1.000, ratio=1.087, hyp_len=12425, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.67.1.85-6.37.2.61-13.55.pth
BLEU = 10.64, 34.7/14.4/7.2/3.6 (BP=1.000, ratio=1.104, hyp_len=12617, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.68.1.83-6.21.2.64-14.06.pth
BLEU = 10.55, 34.4/14.1/6.9/3.7 (BP=1.000, ratio=1.087, hyp_len=12426, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.69.1.82-6.18.2.62-13.80.pth
BLEU = 10.36, 34.5/14.2/6.9/3.4 (BP=1.000, ratio=1.108, hyp_len=12665, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.70.1.89-6.59.2.62-13.80.pth
BLEU = 10.51, 35.1/14.3/6.8/3.5 (BP=1.000, ratio=1.086, hyp_len=12410, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.71.1.78-5.94.2.62-13.73.pth
BLEU = 10.32, 35.1/14.2/6.8/3.3 (BP=1.000, ratio=1.082, hyp_len=12375, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.72.1.77-5.86.2.62-13.70.pth
BLEU = 10.32, 35.2/14.1/6.7/3.4 (BP=1.000, ratio=1.084, hyp_len=12393, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.73.1.81-6.11.2.63-13.86.pth
BLEU = 10.59, 34.4/14.1/6.9/3.8 (BP=1.000, ratio=1.096, hyp_len=12530, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.74.1.73-5.66.2.64-13.97.pth
BLEU = 10.86, 35.4/14.6/7.1/3.8 (BP=1.000, ratio=1.087, hyp_len=12429, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.75.1.70-5.47.2.66-14.23.pth
BLEU = 10.50, 35.1/14.3/6.8/3.5 (BP=1.000, ratio=1.078, hyp_len=12323, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.76.1.71-5.55.2.64-14.00.pth
BLEU = 11.12, 35.8/14.8/7.3/3.9 (BP=1.000, ratio=1.062, hyp_len=12138, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.77.1.72-5.59.2.67-14.51.pth
BLEU = 10.58, 34.5/14.3/7.0/3.6 (BP=1.000, ratio=1.109, hyp_len=12680, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.78.1.72-5.58.2.67-14.51.pth
BLEU = 10.75, 35.6/14.7/7.0/3.6 (BP=1.000, ratio=1.087, hyp_len=12427, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.79.1.67-5.30.2.67-14.49.pth
BLEU = 10.94, 35.1/14.5/7.2/3.9 (BP=1.000, ratio=1.077, hyp_len=12316, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.80.1.66-5.26.2.71-15.01.pth
BLEU = 11.06, 35.4/14.7/7.4/3.9 (BP=1.000, ratio=1.091, hyp_len=12469, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.81.1.60-4.98.2.66-14.35.pth
BLEU = 11.16, 35.6/14.9/7.4/3.9 (BP=1.000, ratio=1.094, hyp_len=12501, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.82.1.68-5.38.2.69-14.76.pth
BLEU = 11.50, 36.2/15.3/7.7/4.1 (BP=1.000, ratio=1.083, hyp_len=12384, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.83.1.59-4.91.2.71-14.98.pth
BLEU = 10.83, 35.7/14.5/7.1/3.8 (BP=1.000, ratio=1.076, hyp_len=12303, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.84.1.65-5.23.2.73-15.37.pth
BLEU = 10.82, 34.7/14.4/7.2/3.8 (BP=1.000, ratio=1.110, hyp_len=12687, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.85.1.62-5.06.2.70-14.85.pth
BLEU = 11.06, 35.7/14.9/7.3/3.9 (BP=1.000, ratio=1.092, hyp_len=12481, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.86.1.61-5.03.2.71-14.99.pth
BLEU = 10.62, 35.7/14.5/7.0/3.5 (BP=1.000, ratio=1.074, hyp_len=12275, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.87.1.60-4.94.2.71-14.98.pth
BLEU = 10.40, 34.4/14.0/6.8/3.6 (BP=1.000, ratio=1.095, hyp_len=12517, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.88.1.58-4.87.2.74-15.50.pth
BLEU = 10.97, 36.0/15.1/7.2/3.7 (BP=1.000, ratio=1.080, hyp_len=12352, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.89.1.52-4.58.2.76-15.78.pth
BLEU = 10.88, 35.7/14.7/7.3/3.7 (BP=1.000, ratio=1.086, hyp_len=12410, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.90.1.59-4.91.2.76-15.76.pth
BLEU = 10.67, 35.7/14.4/7.0/3.6 (BP=1.000, ratio=1.108, hyp_len=12668, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.91.1.58-4.85.2.76-15.73.pth
BLEU = 10.96, 35.3/14.7/7.3/3.8 (BP=1.000, ratio=1.096, hyp_len=12534, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.92.1.51-4.53.2.78-16.10.pth
BLEU = 11.09, 35.6/14.9/7.4/3.9 (BP=1.000, ratio=1.095, hyp_len=12523, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.93.1.49-4.45.2.76-15.85.pth
BLEU = 11.17, 35.8/14.9/7.4/4.0 (BP=1.000, ratio=1.091, hyp_len=12467, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.94.1.47-4.33.2.78-16.17.pth
BLEU = 10.92, 35.2/14.8/7.3/3.7 (BP=1.000, ratio=1.091, hyp_len=12474, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.95.1.53-4.64.2.78-16.17.pth
BLEU = 11.09, 35.9/15.0/7.4/3.8 (BP=1.000, ratio=1.093, hyp_len=12492, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.96.1.45-4.27.2.79-16.34.pth
BLEU = 11.20, 35.8/14.9/7.5/3.9 (BP=1.000, ratio=1.092, hyp_len=12482, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.97.1.41-4.08.2.79-16.24.pth
BLEU = 11.32, 36.0/15.1/7.5/4.0 (BP=1.000, ratio=1.079, hyp_len=12333, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.98.1.43-4.18.2.82-16.74.pth
BLEU = 11.36, 36.0/15.1/7.6/4.0 (BP=1.000, ratio=1.083, hyp_len=12376, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.99.1.49-4.44.2.84-17.14.pth
BLEU = 11.28, 36.4/15.4/7.6/3.8 (BP=1.000, ratio=1.088, hyp_len=12442, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/seq2seq/mybk-70epoch
Evaluation result for the model: seq-rl-model-mybk.100.1.18-3.26.2.50-12.24.pth
BLEU = 14.89, 41.1/19.2/10.4/6.0 (BP=1.000, ratio=1.101, hyp_len=12592, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.69.1.66-5.27.2.37-10.70.pth
BLEU = 13.63, 40.0/17.8/9.4/5.2 (BP=1.000, ratio=1.090, hyp_len=12466, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.70.1.60-4.94.2.36-10.58.pth
BLEU = 13.84, 40.5/18.5/9.6/5.1 (BP=1.000, ratio=1.098, hyp_len=12556, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.71.1.62-5.05.2.40-11.06.pth
BLEU = 13.09, 39.4/17.6/9.0/4.7 (BP=1.000, ratio=1.127, hyp_len=12889, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.72.1.58-4.86.2.38-10.78.pth
BLEU = 13.98, 41.0/18.5/9.6/5.2 (BP=1.000, ratio=1.095, hyp_len=12513, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.73.1.65-5.19.2.43-11.31.pth
BLEU = 14.29, 40.4/18.5/10.0/5.6 (BP=1.000, ratio=1.078, hyp_len=12319, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.74.1.53-4.60.2.39-10.95.pth
BLEU = 12.89, 39.2/17.4/8.8/4.6 (BP=1.000, ratio=1.123, hyp_len=12837, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.75.1.56-4.74.2.39-10.93.pth
BLEU = 13.35, 38.9/17.6/9.2/5.0 (BP=1.000, ratio=1.121, hyp_len=12815, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.76.1.53-4.63.2.42-11.23.pth
BLEU = 13.60, 40.0/18.2/9.3/5.1 (BP=1.000, ratio=1.098, hyp_len=12552, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.77.1.59-4.93.2.43-11.34.pth
BLEU = 13.31, 39.6/17.8/9.1/4.9 (BP=1.000, ratio=1.107, hyp_len=12659, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.78.1.51-4.51.2.39-10.96.pth
BLEU = 13.80, 40.7/18.3/9.4/5.2 (BP=1.000, ratio=1.086, hyp_len=12415, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.79.1.47-4.34.2.41-11.17.pth
BLEU = 14.13, 40.7/18.7/9.7/5.4 (BP=1.000, ratio=1.096, hyp_len=12534, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.80.1.56-4.78.2.41-11.19.pth
BLEU = 14.21, 41.0/18.7/9.9/5.4 (BP=1.000, ratio=1.089, hyp_len=12447, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.81.1.48-4.38.2.43-11.35.pth
BLEU = 13.51, 39.9/17.8/9.3/5.1 (BP=1.000, ratio=1.110, hyp_len=12692, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.82.1.38-3.99.2.41-11.19.pth
BLEU = 14.28, 40.3/18.3/9.9/5.7 (BP=1.000, ratio=1.099, hyp_len=12559, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.83.1.40-4.06.2.45-11.57.pth
BLEU = 13.89, 40.2/18.1/9.6/5.3 (BP=1.000, ratio=1.109, hyp_len=12677, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.84.1.43-4.19.2.40-11.07.pth
BLEU = 14.32, 40.6/18.6/9.9/5.6 (BP=1.000, ratio=1.105, hyp_len=12637, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.85.1.39-4.01.2.43-11.34.pth
BLEU = 14.82, 41.7/19.4/10.4/5.7 (BP=1.000, ratio=1.081, hyp_len=12353, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.86.1.39-4.02.2.45-11.55.pth
BLEU = 14.20, 40.3/18.4/9.8/5.6 (BP=1.000, ratio=1.119, hyp_len=12788, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.87.1.36-3.90.2.45-11.58.pth
BLEU = 14.99, 41.4/19.4/10.4/6.0 (BP=1.000, ratio=1.108, hyp_len=12670, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.88.1.33-3.78.2.44-11.43.pth
BLEU = 14.79, 41.3/19.2/10.3/5.9 (BP=1.000, ratio=1.102, hyp_len=12595, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.89.1.31-3.70.2.43-11.38.pth
BLEU = 14.73, 41.4/19.1/10.2/5.8 (BP=1.000, ratio=1.098, hyp_len=12556, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.90.1.33-3.79.2.45-11.58.pth
BLEU = 14.66, 40.9/18.9/10.2/5.8 (BP=1.000, ratio=1.123, hyp_len=12842, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.91.1.32-3.75.2.41-11.17.pth
BLEU = 14.37, 41.4/18.9/9.9/5.5 (BP=1.000, ratio=1.091, hyp_len=12474, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.92.1.30-3.68.2.44-11.51.pth
BLEU = 15.72, 42.3/19.9/11.0/6.6 (BP=1.000, ratio=1.083, hyp_len=12377, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.93.1.26-3.54.2.46-11.71.pth
BLEU = 14.87, 41.3/19.1/10.4/6.0 (BP=1.000, ratio=1.097, hyp_len=12543, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.94.1.35-3.86.2.49-12.01.pth
BLEU = 14.74, 40.8/18.9/10.3/5.9 (BP=1.000, ratio=1.121, hyp_len=12818, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.95.1.26-3.53.2.49-12.07.pth
BLEU = 14.42, 40.7/18.7/10.0/5.7 (BP=1.000, ratio=1.110, hyp_len=12686, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.96.1.28-3.60.2.51-12.29.pth
BLEU = 15.11, 41.6/19.4/10.6/6.1 (BP=1.000, ratio=1.095, hyp_len=12522, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.97.1.25-3.50.2.47-11.86.pth
BLEU = 15.41, 41.9/19.6/10.9/6.3 (BP=1.000, ratio=1.093, hyp_len=12490, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.98.1.21-3.36.2.51-12.35.pth
BLEU = 15.15, 41.6/19.4/10.7/6.1 (BP=1.000, ratio=1.098, hyp_len=12552, ref_len=11432)
Evaluation result for the model: seq-rl-model-mybk.99.1.20-3.31.2.50-12.16.pth
BLEU = 14.43, 41.0/18.7/10.0/5.7 (BP=1.000, ratio=1.115, hyp_len=12751, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/seq2seq/bkmy-30epoch
Evaluation result for the model: seq-rl-model-bkmy.100.1.30-3.68.2.52-12.37.pth
BLEU = 13.29, 41.0/18.5/9.0/4.6 (BP=1.000, ratio=1.065, hyp_len=13021, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.31.2.62-13.71.2.50-12.20.pth
BLEU = 9.88, 36.5/15.3/6.3/2.7 (BP=1.000, ratio=1.034, hyp_len=12650, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.32.2.64-14.04.2.49-12.06.pth
BLEU = 9.81, 36.0/15.1/6.4/2.7 (BP=1.000, ratio=1.058, hyp_len=12939, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.33.2.64-14.02.2.48-11.96.pth
BLEU = 9.17, 33.7/14.1/5.9/2.5 (BP=1.000, ratio=1.132, hyp_len=13844, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.34.2.56-12.90.2.46-11.72.pth
BLEU = 7.90, 29.6/12.4/5.1/2.1 (BP=1.000, ratio=1.316, hyp_len=16093, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.35.2.56-12.97.2.47-11.77.pth
BLEU = 8.85, 32.4/13.8/5.8/2.4 (BP=1.000, ratio=1.201, hyp_len=14695, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.36.2.45-11.57.2.44-11.44.pth
BLEU = 6.85, 26.1/10.8/4.4/1.8 (BP=1.000, ratio=1.469, hyp_len=17968, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.37.2.43-11.42.2.43-11.41.pth
BLEU = 8.27, 30.4/12.6/5.2/2.3 (BP=1.000, ratio=1.287, hyp_len=15746, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.38.2.36-10.64.2.41-11.10.pth
BLEU = 9.67, 34.8/14.9/6.3/2.7 (BP=1.000, ratio=1.147, hyp_len=14033, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.39.2.35-10.52.2.40-11.04.pth
BLEU = 10.10, 35.5/15.4/6.7/2.8 (BP=1.000, ratio=1.137, hyp_len=13908, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.40.2.31-10.08.2.41-11.18.pth
BLEU = 10.09, 37.0/15.7/6.6/2.7 (BP=1.000, ratio=1.100, hyp_len=13457, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.41.2.26-9.62.2.39-10.91.pth
BLEU = 10.39, 36.2/15.6/6.9/3.0 (BP=1.000, ratio=1.144, hyp_len=13994, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.42.2.33-10.31.2.41-11.18.pth
BLEU = 10.61, 37.4/16.1/6.9/3.0 (BP=1.000, ratio=1.080, hyp_len=13207, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.43.2.27-9.68.2.37-10.70.pth
BLEU = 11.08, 38.3/16.8/7.3/3.2 (BP=1.000, ratio=1.076, hyp_len=13165, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.44.2.29-9.88.2.36-10.63.pth
BLEU = 10.68, 37.5/16.1/7.0/3.1 (BP=1.000, ratio=1.097, hyp_len=13417, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.45.2.33-10.31.2.36-10.62.pth
BLEU = 11.18, 37.9/16.4/7.3/3.4 (BP=1.000, ratio=1.090, hyp_len=13337, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.46.2.16-8.64.2.35-10.46.pth
BLEU = 11.06, 38.3/16.6/7.4/3.2 (BP=1.000, ratio=1.098, hyp_len=13425, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.47.2.20-9.02.2.36-10.62.pth
BLEU = 12.50, 40.2/18.2/8.4/4.0 (BP=1.000, ratio=1.060, hyp_len=12969, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.48.2.10-8.15.2.37-10.70.pth
BLEU = 10.99, 38.0/16.2/7.1/3.3 (BP=1.000, ratio=1.103, hyp_len=13495, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.49.2.15-8.56.2.35-10.45.pth
BLEU = 11.93, 39.7/17.4/7.9/3.7 (BP=1.000, ratio=1.058, hyp_len=12941, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.50.2.01-7.47.2.33-10.28.pth
BLEU = 11.76, 39.9/17.4/7.9/3.5 (BP=1.000, ratio=1.058, hyp_len=12946, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.51.2.02-7.55.2.33-10.31.pth
BLEU = 11.92, 39.2/17.4/7.9/3.7 (BP=1.000, ratio=1.082, hyp_len=13229, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.52.2.06-7.87.2.34-10.34.pth
BLEU = 10.26, 35.8/15.5/6.8/3.0 (BP=1.000, ratio=1.181, hyp_len=14441, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.53.2.01-7.49.2.32-10.19.pth
BLEU = 12.24, 40.2/18.0/8.1/3.8 (BP=1.000, ratio=1.068, hyp_len=13062, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.54.1.95-7.06.2.33-10.26.pth
BLEU = 11.73, 39.4/17.3/7.7/3.6 (BP=1.000, ratio=1.072, hyp_len=13109, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.55.1.95-7.01.2.31-10.08.pth
BLEU = 11.96, 40.0/17.5/7.9/3.7 (BP=1.000, ratio=1.064, hyp_len=13012, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.56.1.92-6.80.2.36-10.59.pth
BLEU = 11.31, 37.7/16.7/7.5/3.5 (BP=1.000, ratio=1.118, hyp_len=13678, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.57.1.92-6.85.2.31-10.10.pth
BLEU = 12.67, 40.7/18.2/8.6/4.1 (BP=1.000, ratio=1.061, hyp_len=12980, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.58.1.90-6.66.2.35-10.53.pth
BLEU = 10.72, 36.2/15.6/7.1/3.3 (BP=1.000, ratio=1.183, hyp_len=14471, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.59.1.85-6.37.2.34-10.41.pth
BLEU = 12.08, 39.2/17.5/8.1/3.8 (BP=1.000, ratio=1.103, hyp_len=13493, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.60.1.86-6.40.2.34-10.36.pth
BLEU = 12.68, 40.2/18.3/8.6/4.1 (BP=1.000, ratio=1.077, hyp_len=13178, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.61.1.77-5.86.2.35-10.51.pth
BLEU = 12.57, 40.0/18.0/8.4/4.1 (BP=1.000, ratio=1.090, hyp_len=13327, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.62.1.78-5.95.2.33-10.29.pth
BLEU = 12.68, 41.0/18.5/8.5/4.0 (BP=1.000, ratio=1.068, hyp_len=13058, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.63.1.80-6.08.2.35-10.45.pth
BLEU = 12.82, 39.8/18.3/8.6/4.3 (BP=1.000, ratio=1.094, hyp_len=13380, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.64.1.73-5.62.2.35-10.46.pth
BLEU = 12.54, 40.3/18.1/8.3/4.1 (BP=1.000, ratio=1.071, hyp_len=13103, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.65.1.79-5.98.2.34-10.36.pth
BLEU = 13.43, 41.8/19.1/9.0/4.6 (BP=1.000, ratio=1.054, hyp_len=12890, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.66.1.76-5.82.2.37-10.65.pth
BLEU = 12.81, 40.3/18.1/8.5/4.3 (BP=1.000, ratio=1.096, hyp_len=13401, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.67.1.69-5.39.2.35-10.51.pth
BLEU = 13.40, 41.2/18.8/9.1/4.6 (BP=1.000, ratio=1.059, hyp_len=12951, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.68.1.74-5.68.2.36-10.60.pth
BLEU = 13.07, 41.6/18.5/8.8/4.3 (BP=1.000, ratio=1.060, hyp_len=12969, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.69.1.69-5.42.2.34-10.37.pth
BLEU = 13.42, 41.8/19.2/9.1/4.4 (BP=1.000, ratio=1.024, hyp_len=12529, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.70.1.64-5.14.2.35-10.54.pth
BLEU = 13.06, 41.3/18.7/8.8/4.3 (BP=1.000, ratio=1.054, hyp_len=12892, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.71.1.70-5.48.2.36-10.58.pth
BLEU = 12.60, 40.6/18.1/8.5/4.0 (BP=1.000, ratio=1.072, hyp_len=13110, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.72.1.61-5.00.2.36-10.57.pth
BLEU = 13.04, 41.2/18.5/8.8/4.3 (BP=1.000, ratio=1.055, hyp_len=12907, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.73.1.56-4.77.2.36-10.63.pth
BLEU = 13.04, 41.3/18.6/8.8/4.3 (BP=1.000, ratio=1.061, hyp_len=12973, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.74.1.56-4.77.2.40-11.02.pth
BLEU = 13.19, 41.2/18.5/8.9/4.4 (BP=1.000, ratio=1.063, hyp_len=13007, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.75.1.60-4.94.2.39-10.89.pth
BLEU = 12.90, 40.4/18.4/8.8/4.3 (BP=1.000, ratio=1.072, hyp_len=13109, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.76.1.51-4.53.2.40-11.06.pth
BLEU = 13.31, 41.2/18.7/9.0/4.5 (BP=1.000, ratio=1.062, hyp_len=12985, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.77.1.59-4.92.2.39-10.92.pth
BLEU = 12.49, 40.8/18.0/8.3/4.0 (BP=1.000, ratio=1.066, hyp_len=13043, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.78.1.53-4.64.2.42-11.21.pth
BLEU = 13.40, 41.3/18.9/9.0/4.6 (BP=1.000, ratio=1.067, hyp_len=13047, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.79.1.50-4.47.2.42-11.23.pth
BLEU = 12.60, 40.3/18.2/8.6/4.0 (BP=1.000, ratio=1.090, hyp_len=13332, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.80.1.48-4.38.2.43-11.40.pth
BLEU = 12.65, 40.8/18.1/8.4/4.1 (BP=1.000, ratio=1.070, hyp_len=13089, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.81.1.56-4.74.2.41-11.14.pth
BLEU = 13.04, 40.1/18.3/8.8/4.5 (BP=1.000, ratio=1.094, hyp_len=13375, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.82.1.46-4.30.2.46-11.68.pth
BLEU = 13.14, 41.5/18.8/8.9/4.3 (BP=1.000, ratio=1.062, hyp_len=12988, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.83.1.54-4.67.2.47-11.83.pth
BLEU = 12.76, 40.2/18.2/8.6/4.2 (BP=1.000, ratio=1.094, hyp_len=13377, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.84.1.48-4.39.2.42-11.20.pth
BLEU = 13.15, 41.3/18.7/8.8/4.4 (BP=1.000, ratio=1.062, hyp_len=12989, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.85.1.43-4.17.2.40-11.06.pth
BLEU = 13.18, 42.1/19.0/8.9/4.3 (BP=1.000, ratio=1.043, hyp_len=12754, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.86.1.45-4.25.2.43-11.40.pth
BLEU = 12.59, 40.2/17.7/8.4/4.2 (BP=1.000, ratio=1.074, hyp_len=13136, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.87.1.36-3.91.2.46-11.76.pth
BLEU = 13.37, 41.2/18.5/9.0/4.6 (BP=1.000, ratio=1.061, hyp_len=12981, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.88.1.46-4.31.2.50-12.19.pth
BLEU = 12.40, 39.8/17.6/8.2/4.1 (BP=1.000, ratio=1.079, hyp_len=13201, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.89.1.41-4.08.2.50-12.22.pth
BLEU = 12.72, 40.7/18.0/8.6/4.2 (BP=1.000, ratio=1.063, hyp_len=13000, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.90.1.35-3.87.2.47-11.85.pth
BLEU = 12.83, 41.0/18.2/8.5/4.2 (BP=1.000, ratio=1.057, hyp_len=12930, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.91.1.41-4.10.2.49-12.10.pth
BLEU = 13.13, 41.2/18.5/8.9/4.4 (BP=1.000, ratio=1.070, hyp_len=13086, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.92.1.36-3.91.2.47-11.86.pth
BLEU = 12.86, 40.9/18.1/8.6/4.3 (BP=1.000, ratio=1.063, hyp_len=12998, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.93.1.33-3.79.2.50-12.15.pth
BLEU = 12.70, 40.6/18.1/8.5/4.2 (BP=1.000, ratio=1.062, hyp_len=12985, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.94.1.28-3.60.2.50-12.17.pth
BLEU = 12.97, 41.1/18.4/8.7/4.3 (BP=1.000, ratio=1.054, hyp_len=12897, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.95.1.26-3.53.2.48-11.98.pth
BLEU = 13.26, 41.6/18.6/8.9/4.5 (BP=1.000, ratio=1.061, hyp_len=12975, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.96.1.26-3.52.2.50-12.15.pth
BLEU = 13.09, 41.4/18.2/8.8/4.4 (BP=1.000, ratio=1.060, hyp_len=12965, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.97.1.30-3.68.2.52-12.40.pth
BLEU = 13.17, 41.2/18.5/8.8/4.5 (BP=1.000, ratio=1.066, hyp_len=13044, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.98.1.23-3.41.2.54-12.70.pth
BLEU = 12.71, 40.8/18.0/8.5/4.2 (BP=1.000, ratio=1.075, hyp_len=13149, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.99.1.23-3.41.2.51-12.35.pth
BLEU = 13.30, 41.7/18.7/8.9/4.5 (BP=1.000, ratio=1.050, hyp_len=12841, ref_len=12231)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/seq2seq/bkmy-40epoch
Evaluation result for the model: seq-rl-model-bkmy.100.1.34-3.81.2.68-14.52.pth
BLEU = 12.45, 39.2/17.4/8.4/4.2 (BP=1.000, ratio=1.089, hyp_len=13321, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.30.2.62-13.74.2.57-13.02.pth
BLEU = 5.95, 23.8/9.5/3.7/1.5 (BP=1.000, ratio=1.567, hyp_len=19162, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.31.2.63-13.94.2.56-12.96.pth
BLEU = 6.70, 26.3/10.5/4.2/1.7 (BP=1.000, ratio=1.436, hyp_len=17566, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.32.2.55-12.76.2.58-13.21.pth
BLEU = 6.99, 27.8/10.9/4.4/1.8 (BP=1.000, ratio=1.345, hyp_len=16454, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.33.2.57-13.09.2.54-12.73.pth
BLEU = 5.41, 21.7/8.5/3.4/1.4 (BP=1.000, ratio=1.750, hyp_len=21405, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.34.2.49-12.07.2.54-12.64.pth
BLEU = 6.28, 24.6/9.8/4.0/1.6 (BP=1.000, ratio=1.541, hyp_len=18850, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.35.2.49-12.09.2.54-12.73.pth
BLEU = 4.39, 17.6/6.9/2.8/1.1 (BP=1.000, ratio=2.128, hyp_len=26025, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.36.2.45-11.53.2.51-12.28.pth
BLEU = 7.75, 29.3/12.1/5.0/2.0 (BP=1.000, ratio=1.313, hyp_len=16055, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.37.2.42-11.25.2.51-12.27.pth
BLEU = 7.76, 28.6/11.8/5.1/2.1 (BP=1.000, ratio=1.367, hyp_len=16714, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.38.2.37-10.70.2.52-12.40.pth
BLEU = 7.27, 28.2/11.4/4.6/1.9 (BP=1.000, ratio=1.380, hyp_len=16878, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.39.2.33-10.25.2.52-12.37.pth
BLEU = 7.24, 27.4/11.3/4.7/1.9 (BP=1.000, ratio=1.437, hyp_len=17580, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.40.2.30-9.99.2.51-12.28.pth
BLEU = 8.45, 32.2/13.2/5.4/2.2 (BP=1.000, ratio=1.210, hyp_len=14805, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.41.2.27-9.72.2.50-12.21.pth
BLEU = 8.43, 32.9/13.4/5.4/2.1 (BP=1.000, ratio=1.199, hyp_len=14667, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.42.2.25-9.52.2.51-12.32.pth
BLEU = 9.77, 35.9/15.0/6.3/2.7 (BP=1.000, ratio=1.109, hyp_len=13565, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.43.2.26-9.56.2.49-12.10.pth
BLEU = 8.68, 33.5/13.7/5.5/2.3 (BP=1.000, ratio=1.168, hyp_len=14286, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.44.2.23-9.34.2.47-11.81.pth
BLEU = 9.54, 34.6/14.6/6.1/2.7 (BP=1.000, ratio=1.155, hyp_len=14125, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.45.2.22-9.25.2.51-12.25.pth
BLEU = 10.59, 36.7/15.7/7.0/3.1 (BP=1.000, ratio=1.087, hyp_len=13298, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.46.2.18-8.89.2.49-12.01.pth
BLEU = 10.27, 36.0/15.3/6.7/3.0 (BP=1.000, ratio=1.134, hyp_len=13870, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.47.2.20-9.04.2.45-11.60.pth
BLEU = 10.31, 37.3/15.7/6.8/2.8 (BP=1.000, ratio=1.069, hyp_len=13073, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.48.2.12-8.29.2.47-11.83.pth
BLEU = 10.09, 36.7/15.2/6.6/2.8 (BP=1.000, ratio=1.109, hyp_len=13563, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.49.2.09-8.08.2.46-11.69.pth
BLEU = 10.67, 38.2/16.1/6.9/3.1 (BP=1.000, ratio=1.053, hyp_len=12885, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.50.2.12-8.30.2.47-11.82.pth
BLEU = 10.17, 36.7/15.5/6.6/2.9 (BP=1.000, ratio=1.089, hyp_len=13314, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.51.2.03-7.64.2.47-11.86.pth
BLEU = 10.76, 38.1/16.0/7.0/3.1 (BP=1.000, ratio=1.080, hyp_len=13213, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.52.2.02-7.51.2.46-11.69.pth
BLEU = 11.14, 38.5/16.6/7.3/3.3 (BP=1.000, ratio=1.067, hyp_len=13046, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.53.1.99-7.33.2.46-11.67.pth
BLEU = 11.33, 38.0/16.6/7.5/3.5 (BP=1.000, ratio=1.077, hyp_len=13177, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.54.2.04-7.69.2.47-11.80.pth
BLEU = 10.93, 38.1/16.3/7.2/3.2 (BP=1.000, ratio=1.071, hyp_len=13104, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.55.1.93-6.88.2.44-11.48.pth
BLEU = 10.74, 38.0/16.1/7.0/3.1 (BP=1.000, ratio=1.068, hyp_len=13066, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.56.1.92-6.84.2.45-11.58.pth
BLEU = 11.17, 38.8/16.6/7.3/3.3 (BP=1.000, ratio=1.046, hyp_len=12789, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.57.1.95-7.04.2.46-11.72.pth
BLEU = 11.09, 38.1/16.4/7.3/3.3 (BP=1.000, ratio=1.077, hyp_len=13178, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.58.1.93-6.91.2.48-11.99.pth
BLEU = 11.02, 38.3/16.1/7.2/3.3 (BP=1.000, ratio=1.080, hyp_len=13208, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.59.1.86-6.41.2.48-11.93.pth
BLEU = 11.31, 38.1/16.2/7.5/3.6 (BP=1.000, ratio=1.081, hyp_len=13222, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.60.1.90-6.68.2.48-11.93.pth
BLEU = 11.29, 38.3/16.5/7.4/3.5 (BP=1.000, ratio=1.065, hyp_len=13030, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.61.1.86-6.41.2.50-12.18.pth
BLEU = 11.36, 39.0/16.7/7.5/3.4 (BP=1.000, ratio=1.060, hyp_len=12967, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.62.1.80-6.04.2.48-11.99.pth
BLEU = 11.41, 38.4/16.8/7.6/3.5 (BP=1.000, ratio=1.077, hyp_len=13171, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.63.1.81-6.12.2.50-12.22.pth
BLEU = 11.15, 37.7/16.2/7.4/3.4 (BP=1.000, ratio=1.088, hyp_len=13309, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.64.1.80-6.04.2.51-12.34.pth
BLEU = 11.64, 38.8/16.9/7.7/3.6 (BP=1.000, ratio=1.071, hyp_len=13099, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.65.1.74-5.68.2.50-12.20.pth
BLEU = 11.68, 39.4/17.2/7.7/3.6 (BP=1.000, ratio=1.059, hyp_len=12948, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.66.1.77-5.86.2.54-12.72.pth
BLEU = 10.93, 37.2/16.0/7.2/3.3 (BP=1.000, ratio=1.115, hyp_len=13635, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.67.1.82-6.15.2.54-12.62.pth
BLEU = 10.78, 37.8/16.1/7.1/3.1 (BP=1.000, ratio=1.110, hyp_len=13571, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.68.1.73-5.61.2.53-12.52.pth
BLEU = 11.73, 39.8/17.3/7.7/3.5 (BP=1.000, ratio=1.057, hyp_len=12929, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.69.1.68-5.39.2.50-12.22.pth
BLEU = 11.37, 38.6/16.6/7.5/3.5 (BP=1.000, ratio=1.075, hyp_len=13152, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.70.1.65-5.22.2.55-12.76.pth
BLEU = 11.64, 39.0/16.7/7.7/3.6 (BP=1.000, ratio=1.067, hyp_len=13055, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.71.1.64-5.18.2.50-12.24.pth
BLEU = 11.01, 38.3/16.4/7.2/3.3 (BP=1.000, ratio=1.087, hyp_len=13297, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.72.1.62-5.04.2.52-12.39.pth
BLEU = 11.52, 38.7/16.6/7.6/3.6 (BP=1.000, ratio=1.087, hyp_len=13292, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.73.1.60-4.94.2.51-12.24.pth
BLEU = 12.10, 39.5/17.3/8.1/3.9 (BP=1.000, ratio=1.059, hyp_len=12947, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.74.1.60-4.94.2.57-13.10.pth
BLEU = 11.61, 38.4/16.6/7.6/3.7 (BP=1.000, ratio=1.085, hyp_len=13267, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.75.1.62-5.05.2.55-12.81.pth
BLEU = 11.80, 38.8/16.9/7.8/3.8 (BP=1.000, ratio=1.065, hyp_len=13024, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.76.1.58-4.84.2.53-12.59.pth
BLEU = 11.80, 39.2/17.1/7.9/3.7 (BP=1.000, ratio=1.057, hyp_len=12924, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.77.1.58-4.86.2.57-13.01.pth
BLEU = 11.80, 38.8/16.9/7.8/3.8 (BP=1.000, ratio=1.085, hyp_len=13266, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.78.1.57-4.82.2.56-12.90.pth
BLEU = 12.11, 39.7/17.5/8.0/3.9 (BP=1.000, ratio=1.068, hyp_len=13067, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.79.1.56-4.76.2.56-12.96.pth
BLEU = 11.28, 38.7/16.4/7.4/3.5 (BP=1.000, ratio=1.079, hyp_len=13203, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.80.1.52-4.59.2.53-12.56.pth
BLEU = 11.47, 38.4/16.7/7.6/3.5 (BP=1.000, ratio=1.084, hyp_len=13262, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.81.1.53-4.63.2.57-13.10.pth
BLEU = 11.99, 39.2/16.9/8.0/3.9 (BP=1.000, ratio=1.081, hyp_len=13216, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.82.1.54-4.66.2.58-13.21.pth
BLEU = 11.95, 38.8/16.9/7.8/4.0 (BP=1.000, ratio=1.057, hyp_len=12932, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.83.1.48-4.41.2.61-13.61.pth
BLEU = 11.53, 38.1/16.6/7.6/3.7 (BP=1.000, ratio=1.095, hyp_len=13391, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.84.1.44-4.24.2.57-13.09.pth
BLEU = 12.01, 38.8/17.3/8.0/3.9 (BP=1.000, ratio=1.087, hyp_len=13299, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.85.1.45-4.26.2.61-13.54.pth
BLEU = 11.72, 38.5/16.8/7.8/3.7 (BP=1.000, ratio=1.076, hyp_len=13155, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.86.1.55-4.69.2.62-13.78.pth
BLEU = 12.08, 38.5/17.3/8.2/3.9 (BP=1.000, ratio=1.088, hyp_len=13307, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.87.1.49-4.46.2.63-13.86.pth
BLEU = 11.83, 38.6/17.0/8.0/3.7 (BP=1.000, ratio=1.097, hyp_len=13421, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.88.1.50-4.46.2.61-13.56.pth
BLEU = 11.62, 38.6/16.5/7.7/3.7 (BP=1.000, ratio=1.103, hyp_len=13494, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.89.1.49-4.43.2.64-13.99.pth
BLEU = 11.95, 39.0/17.2/8.0/3.8 (BP=1.000, ratio=1.081, hyp_len=13227, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.90.1.40-4.04.2.63-13.85.pth
BLEU = 11.95, 38.7/16.8/7.9/3.9 (BP=1.000, ratio=1.084, hyp_len=13264, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.91.1.39-4.03.2.65-14.21.pth
BLEU = 12.46, 40.0/17.9/8.3/4.0 (BP=1.000, ratio=1.067, hyp_len=13048, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.92.1.37-3.92.2.67-14.41.pth
BLEU = 12.22, 39.3/17.2/8.0/4.1 (BP=1.000, ratio=1.079, hyp_len=13195, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.93.1.35-3.86.2.70-14.82.pth
BLEU = 11.97, 39.1/17.1/8.0/3.8 (BP=1.000, ratio=1.082, hyp_len=13230, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.94.1.38-3.98.2.69-14.70.pth
BLEU = 12.10, 39.3/17.2/8.1/3.9 (BP=1.000, ratio=1.061, hyp_len=12978, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.95.1.36-3.91.2.66-14.35.pth
BLEU = 12.13, 39.3/17.1/8.0/4.0 (BP=1.000, ratio=1.075, hyp_len=13148, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.96.1.31-3.71.2.66-14.34.pth
BLEU = 12.15, 39.9/17.4/8.1/3.9 (BP=1.000, ratio=1.058, hyp_len=12943, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.97.1.31-3.69.2.68-14.65.pth
BLEU = 11.90, 39.6/17.1/7.8/3.8 (BP=1.000, ratio=1.081, hyp_len=13220, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.98.1.35-3.85.2.68-14.54.pth
BLEU = 12.08, 39.6/17.3/8.0/3.9 (BP=1.000, ratio=1.059, hyp_len=12947, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.99.1.28-3.60.2.65-14.20.pth
BLEU = 11.92, 39.2/17.1/7.9/3.8 (BP=1.000, ratio=1.077, hyp_len=13171, ref_len=12231)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/seq2seq/bkmy-50epoch
Evaluation result for the model: seq-rl-model-bkmy.100.1.28-3.58.2.65-14.09.pth
BLEU = 11.77, 39.1/17.0/7.8/3.7 (BP=1.000, ratio=1.094, hyp_len=13384, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.48.2.13-8.44.2.44-11.47.pth
BLEU = 10.64, 36.9/15.8/6.9/3.2 (BP=1.000, ratio=1.124, hyp_len=13742, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.49.2.08-8.01.2.45-11.62.pth
BLEU = 10.79, 37.5/16.1/7.1/3.1 (BP=1.000, ratio=1.091, hyp_len=13346, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.50.2.11-8.25.2.44-11.49.pth
BLEU = 10.00, 35.3/15.0/6.5/2.9 (BP=1.000, ratio=1.154, hyp_len=14116, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.51.2.06-7.84.2.45-11.59.pth
BLEU = 11.00, 38.3/16.5/7.2/3.2 (BP=1.000, ratio=1.064, hyp_len=13016, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.52.2.08-7.99.2.47-11.76.pth
BLEU = 11.38, 38.4/16.8/7.4/3.5 (BP=1.000, ratio=1.090, hyp_len=13337, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.53.2.05-7.79.2.44-11.49.pth
BLEU = 11.82, 39.2/17.4/7.8/3.7 (BP=1.000, ratio=1.054, hyp_len=12888, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.54.2.04-7.66.2.46-11.69.pth
BLEU = 10.53, 35.9/15.4/7.0/3.2 (BP=1.000, ratio=1.171, hyp_len=14322, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.55.1.96-7.11.2.46-11.66.pth
BLEU = 11.58, 39.4/17.3/7.7/3.4 (BP=1.000, ratio=1.072, hyp_len=13108, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.56.1.96-7.09.2.45-11.62.pth
BLEU = 10.96, 38.0/16.5/7.2/3.2 (BP=1.000, ratio=1.103, hyp_len=13491, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.57.1.98-7.25.2.48-11.90.pth
BLEU = 10.49, 36.1/15.5/6.9/3.1 (BP=1.000, ratio=1.161, hyp_len=14197, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.58.1.96-7.08.2.44-11.52.pth
BLEU = 11.21, 37.4/16.4/7.5/3.5 (BP=1.000, ratio=1.118, hyp_len=13673, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.59.1.87-6.47.2.45-11.59.pth
BLEU = 11.51, 38.0/16.7/7.7/3.6 (BP=1.000, ratio=1.105, hyp_len=13518, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.60.1.90-6.68.2.46-11.73.pth
BLEU = 11.32, 37.5/16.7/7.6/3.4 (BP=1.000, ratio=1.124, hyp_len=13748, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.61.1.84-6.27.2.46-11.66.pth
BLEU = 11.63, 38.5/17.1/7.8/3.6 (BP=1.000, ratio=1.110, hyp_len=13574, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.62.1.82-6.16.2.46-11.69.pth
BLEU = 11.32, 39.1/17.0/7.5/3.3 (BP=1.000, ratio=1.086, hyp_len=13277, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.63.1.82-6.15.2.45-11.63.pth
BLEU = 11.27, 37.9/16.5/7.4/3.5 (BP=1.000, ratio=1.107, hyp_len=13537, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.64.1.80-6.06.2.46-11.72.pth
BLEU = 11.92, 39.2/17.1/8.0/3.8 (BP=1.000, ratio=1.077, hyp_len=13170, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.65.1.80-6.06.2.48-11.98.pth
BLEU = 11.64, 39.0/17.1/7.7/3.6 (BP=1.000, ratio=1.086, hyp_len=13281, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.66.1.74-5.68.2.46-11.68.pth
BLEU = 12.07, 39.9/17.7/8.1/3.7 (BP=1.000, ratio=1.073, hyp_len=13119, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.67.1.73-5.63.2.49-12.01.pth
BLEU = 11.96, 39.2/17.4/8.1/3.7 (BP=1.000, ratio=1.072, hyp_len=13115, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.68.1.78-5.96.2.47-11.82.pth
BLEU = 11.60, 39.2/17.2/7.7/3.5 (BP=1.000, ratio=1.098, hyp_len=13428, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.69.1.70-5.45.2.48-11.96.pth
BLEU = 11.76, 39.5/17.1/7.8/3.7 (BP=1.000, ratio=1.071, hyp_len=13096, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.70.1.70-5.49.2.47-11.81.pth
BLEU = 11.31, 38.1/16.6/7.6/3.4 (BP=1.000, ratio=1.109, hyp_len=13567, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.71.1.65-5.18.2.51-12.30.pth
BLEU = 11.81, 39.3/17.2/7.8/3.7 (BP=1.000, ratio=1.082, hyp_len=13239, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.72.1.63-5.11.2.51-12.29.pth
BLEU = 11.27, 37.7/16.3/7.5/3.5 (BP=1.000, ratio=1.131, hyp_len=13836, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.73.1.62-5.08.2.51-12.32.pth
BLEU = 11.56, 37.7/16.7/7.8/3.6 (BP=1.000, ratio=1.144, hyp_len=13991, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.74.1.59-4.89.2.52-12.40.pth
BLEU = 12.05, 39.1/17.4/8.0/3.9 (BP=1.000, ratio=1.091, hyp_len=13340, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.75.1.59-4.91.2.50-12.24.pth
BLEU = 11.98, 39.7/17.3/7.9/3.8 (BP=1.000, ratio=1.081, hyp_len=13218, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.76.1.58-4.85.2.52-12.37.pth
BLEU = 11.91, 39.0/17.3/7.9/3.8 (BP=1.000, ratio=1.091, hyp_len=13346, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.77.1.58-4.87.2.52-12.42.pth
BLEU = 12.00, 40.1/17.7/8.0/3.6 (BP=1.000, ratio=1.077, hyp_len=13169, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.78.1.57-4.83.2.53-12.58.pth
BLEU = 11.65, 38.9/16.9/7.8/3.6 (BP=1.000, ratio=1.098, hyp_len=13431, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.79.1.60-4.98.2.51-12.28.pth
BLEU = 12.37, 39.7/17.6/8.3/4.1 (BP=1.000, ratio=1.074, hyp_len=13141, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.80.1.56-4.78.2.52-12.38.pth
BLEU = 11.93, 39.6/17.2/8.0/3.7 (BP=1.000, ratio=1.082, hyp_len=13237, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.81.1.53-4.60.2.52-12.46.pth
BLEU = 12.00, 39.7/17.6/8.0/3.7 (BP=1.000, ratio=1.090, hyp_len=13328, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.82.1.48-4.41.2.55-12.75.pth
BLEU = 11.85, 39.3/17.1/7.8/3.7 (BP=1.000, ratio=1.087, hyp_len=13296, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.83.1.51-4.51.2.56-12.98.pth
BLEU = 11.86, 39.8/17.4/7.8/3.7 (BP=1.000, ratio=1.079, hyp_len=13198, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.84.1.43-4.19.2.56-12.96.pth
BLEU = 12.52, 40.4/18.0/8.3/4.0 (BP=1.000, ratio=1.068, hyp_len=13065, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.85.1.43-4.20.2.56-12.91.pth
BLEU = 11.36, 38.7/17.0/7.4/3.4 (BP=1.000, ratio=1.114, hyp_len=13625, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.86.1.47-4.33.2.57-13.09.pth
BLEU = 11.65, 39.4/17.0/7.7/3.6 (BP=1.000, ratio=1.088, hyp_len=13309, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.87.1.44-4.20.2.54-12.65.pth
BLEU = 11.95, 39.4/17.1/8.0/3.8 (BP=1.000, ratio=1.084, hyp_len=13258, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.88.1.46-4.33.2.58-13.16.pth
BLEU = 11.95, 39.6/17.5/7.9/3.7 (BP=1.000, ratio=1.089, hyp_len=13322, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.89.1.39-4.03.2.59-13.37.pth
BLEU = 11.43, 38.5/16.8/7.5/3.5 (BP=1.000, ratio=1.115, hyp_len=13632, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.90.1.37-3.94.2.59-13.34.pth
BLEU = 12.40, 40.5/17.7/8.3/4.0 (BP=1.000, ratio=1.065, hyp_len=13030, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.91.1.44-4.23.2.60-13.53.pth
BLEU = 11.82, 38.9/17.2/7.8/3.8 (BP=1.000, ratio=1.105, hyp_len=13513, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.92.1.34-3.81.2.59-13.35.pth
BLEU = 12.11, 39.6/17.3/8.0/3.9 (BP=1.000, ratio=1.091, hyp_len=13342, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.93.1.37-3.92.2.62-13.71.pth
BLEU = 11.45, 38.6/16.6/7.6/3.6 (BP=1.000, ratio=1.122, hyp_len=13728, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.94.1.36-3.92.2.59-13.28.pth
BLEU = 12.10, 39.6/17.4/8.1/3.9 (BP=1.000, ratio=1.080, hyp_len=13214, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.95.1.37-3.92.2.59-13.31.pth
BLEU = 12.15, 39.7/17.5/8.2/3.9 (BP=1.000, ratio=1.107, hyp_len=13543, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.96.1.33-3.78.2.60-13.46.pth
BLEU = 12.20, 40.2/17.7/8.1/3.8 (BP=1.000, ratio=1.074, hyp_len=13130, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.97.1.34-3.83.2.62-13.71.pth
BLEU = 12.11, 39.7/17.5/8.2/3.8 (BP=1.000, ratio=1.088, hyp_len=13307, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.98.1.34-3.81.2.62-13.67.pth
BLEU = 11.89, 39.2/17.1/7.9/3.8 (BP=1.000, ratio=1.092, hyp_len=13357, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.99.1.34-3.83.2.61-13.63.pth
BLEU = 11.72, 39.0/16.9/7.8/3.7 (BP=1.000, ratio=1.119, hyp_len=13682, ref_len=12231)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/seq2seq/bkmy-60epoch
Evaluation result for the model: seq-rl-model-bkmy.100.1.30-3.65.2.61-13.66.pth
BLEU = 11.60, 39.0/16.8/7.7/3.6 (BP=1.000, ratio=1.083, hyp_len=13247, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.58.1.81-6.14.2.37-10.75.pth
BLEU = 10.38, 37.1/15.4/6.7/3.0 (BP=1.000, ratio=1.096, hyp_len=13409, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.59.1.88-6.55.2.38-10.84.pth
BLEU = 11.38, 38.6/16.8/7.5/3.5 (BP=1.000, ratio=1.063, hyp_len=13005, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.60.1.76-5.83.2.39-10.86.pth
BLEU = 11.30, 39.0/16.6/7.4/3.4 (BP=1.000, ratio=1.058, hyp_len=12943, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.61.1.77-5.87.2.40-11.07.pth
BLEU = 11.51, 39.0/16.6/7.5/3.6 (BP=1.000, ratio=1.060, hyp_len=12966, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.62.1.75-5.77.2.41-11.10.pth
BLEU = 10.79, 38.4/16.1/7.0/3.1 (BP=1.000, ratio=1.071, hyp_len=13104, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.63.1.81-6.11.2.36-10.54.pth
BLEU = 11.30, 39.3/16.7/7.3/3.4 (BP=1.000, ratio=1.049, hyp_len=12829, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.64.1.78-5.92.2.39-10.96.pth
BLEU = 11.29, 39.5/16.6/7.4/3.4 (BP=1.000, ratio=1.050, hyp_len=12841, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.65.1.66-5.26.2.39-10.89.pth
BLEU = 11.29, 39.0/16.5/7.3/3.4 (BP=1.000, ratio=1.060, hyp_len=12959, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.66.1.67-5.31.2.39-10.94.pth
BLEU = 11.57, 39.6/17.1/7.7/3.5 (BP=1.000, ratio=1.061, hyp_len=12973, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.67.1.68-5.35.2.39-10.93.pth
BLEU = 11.63, 39.5/17.0/7.6/3.6 (BP=1.000, ratio=1.058, hyp_len=12937, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.68.1.66-5.25.2.39-10.90.pth
BLEU = 11.33, 38.9/16.7/7.3/3.5 (BP=1.000, ratio=1.076, hyp_len=13158, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.69.1.61-5.02.2.42-11.22.pth
BLEU = 11.03, 38.4/16.2/7.2/3.3 (BP=1.000, ratio=1.075, hyp_len=13151, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.70.1.61-5.02.2.43-11.40.pth
BLEU = 11.68, 39.4/16.7/7.7/3.7 (BP=1.000, ratio=1.070, hyp_len=13089, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.71.1.61-4.98.2.40-11.06.pth
BLEU = 11.29, 38.9/16.6/7.4/3.4 (BP=1.000, ratio=1.078, hyp_len=13182, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.72.1.58-4.86.2.40-11.07.pth
BLEU = 11.18, 39.1/16.8/7.3/3.3 (BP=1.000, ratio=1.062, hyp_len=12984, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.73.1.66-5.28.2.43-11.35.pth
BLEU = 11.18, 39.0/16.3/7.2/3.4 (BP=1.000, ratio=1.068, hyp_len=13065, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.74.1.54-4.66.2.44-11.51.pth
BLEU = 11.18, 38.5/16.4/7.4/3.3 (BP=1.000, ratio=1.076, hyp_len=13163, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.75.1.60-4.93.2.46-11.76.pth
BLEU = 11.10, 38.7/16.4/7.2/3.3 (BP=1.000, ratio=1.085, hyp_len=13274, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.76.1.51-4.52.2.46-11.73.pth
BLEU = 11.94, 39.7/17.1/7.9/3.8 (BP=1.000, ratio=1.057, hyp_len=12931, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.77.1.54-4.66.2.47-11.85.pth
BLEU = 10.97, 38.7/16.3/7.1/3.2 (BP=1.000, ratio=1.077, hyp_len=13167, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.78.1.51-4.55.2.52-12.39.pth
BLEU = 10.93, 38.2/16.2/7.2/3.2 (BP=1.000, ratio=1.088, hyp_len=13307, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.79.1.56-4.74.2.48-11.97.pth
BLEU = 11.68, 39.2/17.2/7.7/3.6 (BP=1.000, ratio=1.086, hyp_len=13286, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.80.1.48-4.41.2.46-11.71.pth
BLEU = 11.11, 38.4/16.1/7.2/3.4 (BP=1.000, ratio=1.083, hyp_len=13252, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.81.1.45-4.24.2.47-11.83.pth
BLEU = 11.50, 39.2/16.7/7.5/3.6 (BP=1.000, ratio=1.082, hyp_len=13229, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.82.1.59-4.88.2.47-11.77.pth
BLEU = 11.77, 39.6/17.1/7.7/3.7 (BP=1.000, ratio=1.069, hyp_len=13069, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.83.1.53-4.61.2.51-12.34.pth
BLEU = 10.87, 38.6/16.0/7.1/3.2 (BP=1.000, ratio=1.083, hyp_len=13243, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.84.1.48-4.39.2.48-11.89.pth
BLEU = 11.56, 38.9/16.6/7.7/3.6 (BP=1.000, ratio=1.070, hyp_len=13086, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.85.1.51-4.51.2.55-12.74.pth
BLEU = 11.24, 38.6/16.2/7.3/3.5 (BP=1.000, ratio=1.092, hyp_len=13360, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.86.1.43-4.16.2.52-12.39.pth
BLEU = 11.84, 39.1/16.7/7.8/3.9 (BP=1.000, ratio=1.072, hyp_len=13114, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.87.1.37-3.95.2.53-12.55.pth
BLEU = 11.79, 39.6/17.1/7.7/3.7 (BP=1.000, ratio=1.063, hyp_len=13005, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.88.1.39-4.02.2.52-12.45.pth
BLEU = 11.27, 39.1/16.4/7.4/3.4 (BP=1.000, ratio=1.074, hyp_len=13138, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.89.1.36-3.91.2.54-12.71.pth
BLEU = 11.27, 39.0/16.4/7.3/3.4 (BP=1.000, ratio=1.091, hyp_len=13338, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.90.1.35-3.85.2.53-12.56.pth
BLEU = 11.96, 39.6/17.4/7.9/3.8 (BP=1.000, ratio=1.054, hyp_len=12892, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.91.1.32-3.73.2.53-12.58.pth
BLEU = 11.47, 39.2/16.5/7.4/3.6 (BP=1.000, ratio=1.074, hyp_len=13140, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.92.1.38-3.96.2.53-12.61.pth
BLEU = 11.71, 39.3/16.9/7.8/3.6 (BP=1.000, ratio=1.081, hyp_len=13218, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.93.1.32-3.73.2.55-12.81.pth
BLEU = 11.54, 39.1/16.7/7.5/3.6 (BP=1.000, ratio=1.069, hyp_len=13076, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.94.1.39-4.00.2.55-12.87.pth
BLEU = 11.64, 39.0/16.9/7.7/3.6 (BP=1.000, ratio=1.085, hyp_len=13268, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.95.1.29-3.65.2.56-12.90.pth
BLEU = 11.86, 40.3/17.4/7.8/3.6 (BP=1.000, ratio=1.066, hyp_len=13033, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.96.1.26-3.53.2.57-13.05.pth
BLEU = 11.43, 39.2/16.6/7.4/3.6 (BP=1.000, ratio=1.075, hyp_len=13144, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.97.1.30-3.69.2.58-13.19.pth
BLEU = 11.66, 39.8/16.9/7.7/3.6 (BP=1.000, ratio=1.080, hyp_len=13208, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.98.1.28-3.60.2.61-13.60.pth
BLEU = 11.81, 39.7/17.0/7.8/3.7 (BP=1.000, ratio=1.076, hyp_len=13156, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.99.1.29-3.65.2.59-13.37.pth
BLEU = 11.62, 39.4/16.9/7.6/3.6 (BP=1.000, ratio=1.084, hyp_len=13255, ref_len=12231)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/seq2seq/bkmy-70epoch
Evaluation result for the model: seq-rl-model-bkmy.100.1.15-3.15.2.19-8.92.pth
BLEU = 20.60, 48.2/26.5/15.4/9.1 (BP=1.000, ratio=1.069, hyp_len=13074, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.65.1.68-5.36.2.10-8.13.pth
BLEU = 18.35, 45.6/24.2/13.5/7.6 (BP=1.000, ratio=1.082, hyp_len=13240, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.66.1.75-5.74.2.09-8.09.pth
BLEU = 17.55, 45.0/23.2/12.7/7.1 (BP=1.000, ratio=1.094, hyp_len=13379, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.67.1.65-5.19.2.08-8.04.pth
BLEU = 18.16, 46.5/24.3/13.1/7.3 (BP=1.000, ratio=1.068, hyp_len=13064, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.68.1.60-4.94.2.09-8.07.pth
BLEU = 18.52, 45.3/24.2/13.5/7.9 (BP=1.000, ratio=1.099, hyp_len=13443, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.69.1.58-4.87.2.07-7.95.pth
BLEU = 18.68, 46.1/24.6/13.8/7.8 (BP=1.000, ratio=1.081, hyp_len=13226, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.70.1.67-5.32.2.08-8.01.pth
BLEU = 19.29, 47.1/25.1/14.1/8.3 (BP=1.000, ratio=1.060, hyp_len=12969, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.71.1.54-4.65.2.09-8.06.pth
BLEU = 18.84, 46.9/24.9/13.8/7.8 (BP=1.000, ratio=1.070, hyp_len=13089, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.72.1.62-5.04.2.08-8.02.pth
BLEU = 18.16, 45.6/23.7/13.2/7.6 (BP=1.000, ratio=1.075, hyp_len=13146, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.73.1.65-5.21.2.09-8.07.pth
BLEU = 17.50, 44.9/23.4/12.7/7.0 (BP=1.000, ratio=1.122, hyp_len=13724, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.74.1.56-4.74.2.08-8.02.pth
BLEU = 18.64, 47.2/24.6/13.5/7.7 (BP=1.000, ratio=1.060, hyp_len=12964, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.75.1.50-4.46.2.08-8.02.pth
BLEU = 19.51, 47.5/25.4/14.4/8.4 (BP=1.000, ratio=1.070, hyp_len=13089, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.76.1.51-4.54.2.08-8.01.pth
BLEU = 18.78, 46.2/24.6/13.8/8.0 (BP=1.000, ratio=1.093, hyp_len=13373, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.77.1.57-4.79.2.10-8.13.pth
BLEU = 19.61, 48.1/25.6/14.4/8.3 (BP=1.000, ratio=1.047, hyp_len=12808, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.78.1.41-4.10.2.09-8.10.pth
BLEU = 19.95, 48.2/26.0/14.8/8.6 (BP=1.000, ratio=1.045, hyp_len=12787, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.79.1.43-4.18.2.10-8.15.pth
BLEU = 19.58, 48.2/25.7/14.4/8.2 (BP=1.000, ratio=1.053, hyp_len=12877, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.80.1.38-3.99.2.13-8.39.pth
BLEU = 18.98, 47.1/25.0/14.1/7.9 (BP=1.000, ratio=1.077, hyp_len=13168, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.81.1.40-4.06.2.12-8.36.pth
BLEU = 19.13, 47.2/25.0/14.0/8.1 (BP=1.000, ratio=1.060, hyp_len=12966, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.82.1.41-4.10.2.10-8.20.pth
BLEU = 20.78, 49.0/26.8/15.5/9.2 (BP=1.000, ratio=1.048, hyp_len=12813, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.83.1.37-3.92.2.12-8.37.pth
BLEU = 20.39, 48.6/26.4/15.1/8.9 (BP=1.000, ratio=1.050, hyp_len=12846, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.84.1.32-3.74.2.10-8.19.pth
BLEU = 19.57, 47.8/25.7/14.3/8.3 (BP=1.000, ratio=1.071, hyp_len=13099, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.85.1.29-3.64.2.13-8.43.pth
BLEU = 20.06, 48.1/25.9/14.8/8.8 (BP=1.000, ratio=1.060, hyp_len=12961, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.86.1.29-3.64.2.10-8.17.pth
BLEU = 20.23, 48.4/26.2/15.0/8.8 (BP=1.000, ratio=1.059, hyp_len=12954, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.87.1.35-3.86.2.11-8.22.pth
BLEU = 20.49, 48.4/26.3/15.3/9.1 (BP=1.000, ratio=1.059, hyp_len=12948, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.88.1.28-3.61.2.13-8.40.pth
BLEU = 20.62, 48.3/26.4/15.4/9.2 (BP=1.000, ratio=1.061, hyp_len=12975, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.89.1.27-3.57.2.14-8.53.pth
BLEU = 20.24, 48.2/25.9/14.9/9.0 (BP=1.000, ratio=1.056, hyp_len=12915, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.90.1.20-3.33.2.12-8.36.pth
BLEU = 20.67, 48.4/26.5/15.5/9.2 (BP=1.000, ratio=1.052, hyp_len=12873, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.91.1.22-3.39.2.10-8.17.pth
BLEU = 19.76, 48.2/25.9/14.5/8.4 (BP=1.000, ratio=1.064, hyp_len=13011, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.92.1.23-3.42.2.12-8.32.pth
BLEU = 20.52, 48.7/26.8/15.3/8.9 (BP=1.000, ratio=1.064, hyp_len=13010, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.93.1.18-3.27.2.15-8.62.pth
BLEU = 20.37, 48.6/26.3/15.1/8.9 (BP=1.000, ratio=1.055, hyp_len=12909, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.94.1.20-3.33.2.14-8.47.pth
BLEU = 20.37, 48.2/26.2/15.2/9.0 (BP=1.000, ratio=1.061, hyp_len=12975, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.95.1.19-3.28.2.13-8.42.pth
BLEU = 19.88, 48.2/25.9/14.7/8.5 (BP=1.000, ratio=1.067, hyp_len=13051, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.96.1.28-3.61.2.12-8.34.pth
BLEU = 21.48, 49.4/27.5/16.2/9.7 (BP=1.000, ratio=1.051, hyp_len=12860, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.97.1.23-3.41.2.15-8.59.pth
BLEU = 21.03, 48.7/26.8/15.8/9.5 (BP=1.000, ratio=1.053, hyp_len=12885, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.98.1.18-3.25.2.14-8.50.pth
BLEU = 18.99, 46.5/24.8/13.9/8.1 (BP=1.000, ratio=1.097, hyp_len=13413, ref_len=12231)
Evaluation result for the model: seq-rl-model-bkmy.99.1.24-3.46.2.13-8.43.pth
BLEU = 21.10, 48.9/27.0/15.9/9.4 (BP=1.000, ratio=1.064, hyp_len=13016, ref_len=12231)
/home/ye/exp/simple-nmt
==========

real	100m16.757s
user	96m58.546s
sys	9m2.774s
(simple-nmt) ye@:~/exp/simple-nmt$
```

## Seq2Seq-RL Results

**for Myanmar-Beik**

<div align="center"> 
    
Table 1. Best model and best score for each seq2seq-RL training of my-bk pair  
    (Note: for epoch 30-70, got two same best BLEU scores)  
| No of Epoch for Training | Best Model Epoch | Model File | Best BLEU |
|-----------:|-----------:|:-----------:|-----------:|
| 30-70 | 82 | seq-rl-model-mybk.82.1.40-4.07.2.00-7.38.pth | 22.82 |
| 30-70 | 97 | seq-rl-model-mybk.97.1.24-3.44.2.09-8.10.pth | 22.82 |    
| 40-60 | 99 | seq-rl-model-mybk.99.1.23-3.43.2.05-7.77.pth | 23.72 |
| 50-50 | 85 | seq-rl-model-mybk.85.1.52-4.55.2.54-12.74.pth | 13.50 |
| 60-40 | 82 | seq-rl-model-mybk.82.1.68-5.38.2.69-14.76.pth | 11.50 |
| 70-30 | 92 | seq-rl-model-mybk.92.1.30-3.68.2.44-11.51.pth | 15.72 |

</div>  

**for Beik-Myanmar**

<div align="center"> 
    
Table 2. Best model and best score for each seq2seq-RL training of bk-my pair 
| No of Epoch for Training | Best Model Epoch | Model File | Best BLEU |
|-----------:|-----------:|:-----------:|-----------:|
| 30-70 | 65 | seq-rl-model-bkmy.65.1.79-5.98.2.34-10.36.pth | 13.43 |
| 40-60 | 91 | seq-rl-model-bkmy.91.1.39-4.03.2.65-14.21.pth | 12.46 |
| 50-50 | 84 | seq-rl-model-bkmy.84.1.43-4.19.2.56-12.96.pth | 12.52 |
| 60-40 | 90 | seq-rl-model-bkmy.90.1.35-3.85.2.53-12.56.pth | 11.96 |
| 70-30 | 96 | seq-rl-model-bkmy.96.1.28-3.61.2.12-8.34.pth | 21.48 |

</div>  

## Graph Drawing for Seq2Seq-RL

### Preparation for Drawing Graph

for seq2seq (baseline), my-bk results:  

```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/baseline/seq2seq/mybk-30epoch/eval-results-mybk-seq2seq-baseline-100epoch.txt ./seq30-mybk.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/baseline/seq2seq/mybk-40epoch/eval-results-mybk-seq2seq-baseline-100epoch.txt ./seq40-mybk.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/baseline/seq2seq/mybk-50epoch/eval-results-mybk-seq2seq-baseline-100epoch.txt ./seq50-mybk.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/baseline/seq2seq/mybk-60epoch/eval-results-mybk-seq2seq-baseline-100epoch.txt ./seq60-mybk.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/baseline/seq2seq/mybk-70epoch/eval-results-mybk-seq2seq-baseline-100epoch.txt ./seq70-mybk.txt
```

for seq2seq (baseline), bk-my results:  

```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/baseline/seq2seq/bkmy-30epoch/eval-results-bkmy-seq2seq-baseline-100epoch.txt ./seq30-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/baseline/seq2seq/bkmy-40epoch/eval-results-bkmy-seq2seq-baseline-100epoch.txt ./seq40-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/baseline/seq2seq/bkmy-50epoch/eval-results-bkmy-seq2seq-baseline-100epoch.txt ./seq50-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/baseline/seq2seq/bkmy-60epoch/eval-results-bkmy-seq2seq-baseline-100epoch.txt ./seq60-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/baseline/seq2seq/bkmy-70epoch/eval-results-bkmy-seq2seq-baseline-100epoch.txt ./seq70-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$
```

for seq-RL, my-bk results:  

```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/rl/seq2seq/mybk-30epoch/eval-results-mybk-seq2seq-RL-100epoch.txt ./seq-rl30-mybk.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/rl/seq2seq/mybk-40epoch/eval-results-mybk-seq2seq-RL-100epoch.txt ./seq-rl40-mybk.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/rl/seq2seq/mybk-50epoch/eval-results-mybk-seq2seq-RL-100epoch.txt ./seq-rl50-mybk.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/rl/seq2seq/mybk-60epoch/eval-results-mybk-seq2seq-RL-100epoch.txt ./seq-rl60-mybk.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/rl/seq2seq/mybk-70epoch/eval-results-mybk-seq2seq-RL-100epoch.txt ./seq-rl70-mybk.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$
```

for seq-RL, bk-my results:  

```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/rl/seq2seq/bkmy-30epoch/eval-results-bkmy-seq2seq-RL-100epoch.txt ./seq-rl30-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/rl/seq2seq/bkmy-40epoch/eval-results-bkmy-seq2seq-RL-100epoch.txt ./seq-rl40-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/rl/seq2seq/bkmy-50epoch/eval-results-bkmy-seq2seq-RL-100epoch.txt ./seq-rl50-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/rl/seq2seq/bkmy-60epoch/eval-results-bkmy-seq2seq-RL-100epoch.txt ./seq-rl60-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ cp ../../../rl2/rl/seq2seq/bkmy-70epoch/eval-results-bkmy-seq2seq-RL-100epoch.txt ./seq-rl70-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$
```

### BLEU Score Extraction and Drawing Graph

extract မလုပ်ခင်မှာ BLEU score ဖိုင်ကို ဖွင့်ကြည့်ဖို့ လိုအပ်တယ်။ ဘာကြောင့်လဲ ဆိုတော့ 100 epoch က sorting မလုပ်ထားတော့ ဖိုင်ရဲ့ ထိပ်ဆုံးကို ရောက်နေတတ်လို့ ဖိုင်ရဲ့အောက်ဆုံးကို manual ပြန်ရွှေ့ရတာမို့လို့...  

**for my-bk**  

for 30-70:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ ./extract.sh ./seq30-mybk.txt ./seq-rl30-mybk.txt 30
  30   60  390 ./seq30-mybk.txt.bleu
  70  140  980 ./seq-rl30-mybk.txt.bleu
 100  200 1370 total
 (base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ python ./draw.py seq30-mybk.txt.bleu seq-rl30-mybk.txt.bleu "Seq2Seq 30 epochs + RL 70 epochs (my-bk)" seq2seq_RL-30-70-mybk
```

for 40-60:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ ./extract.sh ./seq40-mybk.txt ./seq-rl40-mybk.txt 40
  40   80  529 ./seq40-mybk.txt.bleu
  60  120  840 ./seq-rl40-mybk.txt.bleu
 100  200 1369 total
 (base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ python ./draw.py ./seq40-mybk.txt.bleu ./seq-rl40-mybk.txt.bleu "Seq2Seq 40 epochs + RL 60 epochs (my-bk)" seq2seq_RL-40-60-mybk
```

for 50-50:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ ./extract.sh ./seq50-mybk.txt ./seq-rl50-mybk.txt 50
  50  100  658 ./seq50-mybk.txt.bleu
  50  100  700 ./seq-rl50-mybk.txt.bleu
 100  200 1358 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ python ./draw.py ./seq50-mybk.txt.bleu ./seq-rl50-mybk.txt.bleu "Seq2Seq 50 epochs + RL 50 epochs (my-bk)" seq2seq_RL-50-50-mybk
```

for 60-40:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ ./extract.sh ./seq60-mybk.txt ./seq-rl60-mybk.txt 58
  60  120  784 ./seq60-mybk.txt.bleu
  43   86  600 ./seq-rl60-mybk.txt.bleu
 103  206 1384 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ python ./draw.py ./seq60-mybk.txt.bleu ./seq-rl60-mybk.txt.bleu "Seq2Seq 60 epochs + RL 40 epochs (my-bk)" seq2seq_RL-60-40-mybk

```

for 70-30:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ ./extract.sh ./seq70-mybk.txt ./seq-rl70-mybk.txt 69
  70  140  939 ./seq70-mybk.txt.bleu
  32   64  448 ./seq-rl70-mybk.txt.bleu
 102  204 1387 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ python ./draw.py ./seq70-mybk.txt.bleu ./seq-rl70-mybk.txt.bleu "Seq2Seq 70 epochs + RL 30 epochs (my-bk)" seq2seq_RL-70-30-mybk
```

**for bk-my**

for 30-70:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ ./extract.sh ./seq30-bkmy.txt ./seq-rl30-bkmy.txt 30
  30   60  390 ./seq30-bkmy.txt.bleu
  70  140  972 ./seq-rl30-bkmy.txt.bleu
 100  200 1362 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ python ./draw.py ./seq30-bkmy.txt.bleu ./seq-rl30-bkmy.txt.bleu "Seq2Seq 30 epochs + RL 70 epochs (bk-my)" seq2seq_RL-30-70-bkmy
```

for 40-60:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ ./extract.sh ./seq40-bkmy.txt ./seq-rl40-bkmy.txt 30
  40   80  520 ./seq40-bkmy.txt.bleu
  71  142  979 ./seq-rl40-bkmy.txt.bleu
 111  222 1499 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ python ./draw.py ./seq40-bkmy.txt.bleu ./seq-rl40-bkmy.txt.bleu "Seq2Seq 40 epochs + RL 60 epochs (bk-my)" seq2seq_RL-40-60-bkmy
```

for 50-50:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ ./extract.sh ./seq50-bkmy.txt ./seq-rl50-bkmy.txt 48
  50  100  655 ./seq50-bkmy.txt.bleu
  53  106  742 ./seq-rl50-bkmy.txt.bleu
 103  206 1397 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ python ./draw.py ./seq50-bkmy.txt.bleu ./seq-rl50-bkmy.txt.bleu "Seq2Seq 50 epochs + RL 50 epochs (bk-my)" seq2seq_RL-50-50-bkmy
```

for 60-40:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ ./extract.sh ./seq60-bkmy.txt ./seq-rl60-bkmy.txt 58
  60  120  796 ./seq60-bkmy.txt.bleu
  43   86  602 ./seq-rl60-bkmy.txt.bleu
 103  206 1398 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ python ./draw.py ./seq60-bkmy.txt.bleu ./seq-rl60-bkmy.txt.bleu "Seq2Seq 60 epochs + RL 40 epochs (bk-my)" seq2seq_RL-60-40-bkmy
```

for 70-30:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ ./extract.sh ./seq70-bkmy.txt ./seq-rl70-bkmy.txt 65
  70  140  939 ./seq70-bkmy.txt.bleu
  36   72  504 ./seq-rl70-bkmy.txt.bleu
 106  212 1443 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/seq$ python ./draw.py ./seq70-bkmy.txt.bleu ./seq-rl70-bkmy.txt.bleu "Seq2Seq 70 epochs + RL 30 epochs (bk-my)" seq2seq_RL-70-30-bkmy
```


## for Transformer Baseline (my-bk, bk-my)
### Bash Script Writing

30 epoch ကနေ 70 epoch အထိ transformer training အတွက် အောက်ပါ bash script ကို ရေးပြီး သုံးခဲ့...   

```bash
#!/bin/bash
# Written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Last updated: 3 April 2022
# Transformer-Reinforcement Learning exp for Myanmar-Beik, Beik-Myanmar

## Reference command from my-rk training process
#time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 16 --n_epochs 40 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/myrk-40epoch/myrk-transformer-model.pth

# training baseline for my-bk
for i in {30,40,50,60,70}
do
   echo "mybk, transformer-baseline training start for ${i} epochs...";
   time python train.py --train /home/ye/exp/simple-nmt/data/my-bk/syl/train \
   --valid /home/ye/exp/simple-nmt/data/my-bk/syl/dev \
   --lang mybk \
   --gpu_id 0 --batch_size 16 --n_epochs ${i} \
   --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 \
   --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 \
   --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 \
   --model_fn ./model/rl2/baseline/transformer/mybk-${i}epoch/transformer-model-mybk.pth  | tee ./model/rl2/baseline/transformer/mybk-${i}epoch/mybk-training.log;
done

echo "####################";

# training baseline for bk-my
for i in {30,40,50,60,70}
do
      echo "bkmy, transformer-baseline training start for ${i} epochs...";
   time python train.py --train /home/ye/exp/simple-nmt/data/my-bk/syl/train \
   --valid /home/ye/exp/simple-nmt/data/my-bk/syl/dev \
   --lang bkmy \
   --gpu_id 1 --batch_size 16 --n_epochs ${i} \
   --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 \
   --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 \
   --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 \
   --model_fn ./model/rl2/baseline/transformer/bkmy-${i}epoch/transformer-model-bkmy.pth | tee ./model/rl2/baseline/transformer/bkmy-${i}epoch/bkmy-training.log;
done

```

### Training 

Training log တစ်ခုလုံးက [RL-exp-for-mybk-screen-output.md](https://github.com/ye-kyaw-thu/error-overflow/blob/master/RL-exp-for-mybk-screen-output.md) မှာ ကြည့်ပါ။   
training ...   

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./rl-transformer-train.sh | tee rl-transformer-train.log
...
...
...
Validation - loss=2.4728e+00 ppl=11.86 best_loss=2.4748e+00 best_ppl=11.88                                              
Epoch 63 - |param|=3.07e+02 |g_param|=1.84e+05 loss=2.5102e+00 ppl=12.31                                                
Validation - loss=2.4612e+00 ppl=11.72 best_loss=2.4728e+00 best_ppl=11.86                                              
Epoch 64 - |param|=3.07e+02 |g_param|=1.94e+05 loss=2.4588e+00 ppl=11.69                                                
Validation - loss=2.4635e+00 ppl=11.75 best_loss=2.4612e+00 best_ppl=11.72                                              
Epoch 65 - |param|=3.07e+02 |g_param|=1.87e+05 loss=2.5101e+00 ppl=12.31                                                
Validation - loss=2.4568e+00 ppl=11.67 best_loss=2.4612e+00 best_ppl=11.72                                              
Epoch 66 - |param|=3.07e+02 |g_param|=1.89e+05 loss=2.4734e+00 ppl=11.86                                                
Validation - loss=2.4387e+00 ppl=11.46 best_loss=2.4568e+00 best_ppl=11.67                                              
Epoch 67 - |param|=3.07e+02 |g_param|=1.99e+05 loss=2.5390e+00 ppl=12.67                                                
Validation - loss=2.4350e+00 ppl=11.42 best_loss=2.4387e+00 best_ppl=11.46                                              
Epoch 68 - |param|=3.07e+02 |g_param|=1.97e+05 loss=2.5081e+00 ppl=12.28                                                
Validation - loss=2.4301e+00 ppl=11.36 best_loss=2.4350e+00 best_ppl=11.42                                              
Epoch 69 - |param|=3.07e+02 |g_param|=2.00e+05 loss=2.4656e+00 ppl=11.77                                                
Validation - loss=2.4262e+00 ppl=11.32 best_loss=2.4301e+00 best_ppl=11.36                                              
Epoch 70 - |param|=3.07e+02 |g_param|=1.81e+05 loss=2.4884e+00 ppl=12.04                                                
Validation - loss=2.4183e+00 ppl=11.23 best_loss=2.4262e+00 best_ppl=11.32                                              

real	21m9.699s
user	21m6.659s
sys	0m3.522s

real	149m11.281s
user	148m45.071s
sys	0m31.116s
```

### Testing/Evaluation

Bash script writing ...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Last updated: 5 April 2022
# A part of Seq2Seq-Reinforcement Learning exp
# this script is for testing/evaluation of baseline transformer for both Myanmar-Beik and Beik-Myanmar

# testing/evaluation baseline for my-bk
for folder in {30,40,50,60,70};
do
   cd ./model/rl2/baseline/transformer/mybk-${folder}epoch/;
   pwd;
   for i in *.pth; do
      MODEL=$i;

      # Testing
      python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang mybk < /home/ye/exp/simple-nmt/data/my-bk/syl/test.my > ./$MODEL.hyp

      # Evaluation with BLEU Score
      echo "Evaluation result for the model: $MODEL" | tee -a eval-results-mybk-transformer-baseline-100epoch.txt;
      cat ./$MODEL.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/my-bk/syl/test.bk | tee  -a eval-results-mybk-transformer-baseline-100epoch.txt;

   done
   cd -; echo "==========";
done

# testing/evaluation baseline for bk-my
for folder in {30,40,50,60,70};
do
   cd ./model/rl2/baseline/transformer/bkmy-${folder}epoch/;
   pwd;
   for i in *.pth; do
      MODEL=$i;

      # Testing
      python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang bkmy < /home/ye/exp/simple-nmt/data/my-bk/syl/test.bk > ./$MODEL.hyp

      # Evaluation with BLEU Score
      echo "Evaluation result for the model: $MODEL" | tee -a eval-results-bkmy-transformer-baseline-100epoch.txt;
      cat ./$MODEL.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/my-bk/syl/test.my | tee  -a eval-results-bkmy-transformer-baseline-100epoch.txt;

   done
   cd -; echo "==========";
done

```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-rl2-transformer-baseline-mybk-bkmy.sh | tee test-eval-rl2-transformer-baseline-mybk-bkmy.log
/home/ye/exp/simple-nmt/model/rl2/baseline/transformer/mybk-30epoch
Evaluation result for the model: transformer-model-mybk.01.6.07-433.79.5.93-376.52.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 31.9/7.2/0.0/0.0 (BP=0.347, ratio=0.486, hyp_len=5557, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.02.5.49-242.47.5.37-214.48.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 31.2/7.6/0.0/0.0 (BP=0.403, ratio=0.524, hyp_len=5989, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.03.5.05-156.18.4.92-137.48.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 33.6/6.0/0.0/0.0 (BP=0.300, ratio=0.454, hyp_len=5186, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.04.4.74-114.19.4.63-102.25.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 37.5/8.3/0.0/0.0 (BP=0.178, ratio=0.367, hyp_len=4196, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.05.4.52-91.43.4.42-83.38.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 31.7/5.6/0.0/0.0 (BP=0.437, ratio=0.547, hyp_len=6258, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.06.4.34-76.55.4.27-71.31.pth
BLEU = 1.60, 32.7/4.0/2.1/0.6 (BP=0.436, ratio=0.547, hyp_len=6249, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.07.4.25-70.11.4.15-63.44.pth
BLEU = 3.25, 27.7/5.6/2.6/1.2 (BP=0.698, ratio=0.736, hyp_len=8411, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.08.4.14-63.04.4.05-57.52.pth
BLEU = 4.40, 23.2/5.8/2.5/1.2 (BP=0.981, ratio=0.981, hyp_len=11214, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.09.4.08-59.26.3.95-51.96.pth
BLEU = 4.13, 22.2/5.3/2.2/1.1 (BP=0.999, ratio=0.999, hyp_len=11419, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.10.3.97-52.84.3.86-47.70.pth
BLEU = 3.79, 20.2/5.4/2.1/0.9 (BP=1.000, ratio=1.178, hyp_len=13462, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.11.3.88-48.40.3.79-44.14.pth
BLEU = 3.67, 19.7/5.4/2.1/0.8 (BP=1.000, ratio=1.241, hyp_len=14189, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.12.3.83-46.09.3.71-40.96.pth
BLEU = 3.55, 18.6/5.3/2.0/0.8 (BP=1.000, ratio=1.332, hyp_len=15223, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.13.3.74-42.07.3.65-38.39.pth
BLEU = 3.10, 16.3/4.7/1.6/0.7 (BP=1.000, ratio=1.443, hyp_len=16495, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.14.3.67-39.45.3.57-35.66.pth
BLEU = 3.08, 16.0/4.6/1.7/0.7 (BP=1.000, ratio=1.527, hyp_len=17460, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.15.3.70-40.51.3.53-34.11.pth
BLEU = 2.75, 13.4/4.2/1.5/0.7 (BP=1.000, ratio=1.711, hyp_len=19560, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.16.3.62-37.49.3.46-31.89.pth
BLEU = 2.69, 13.3/4.0/1.5/0.7 (BP=1.000, ratio=1.644, hyp_len=18792, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.17.3.55-34.88.3.41-30.36.pth
BLEU = 2.87, 13.9/4.3/1.6/0.7 (BP=1.000, ratio=1.741, hyp_len=19900, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.18.3.54-34.46.3.37-28.95.pth
BLEU = 3.63, 16.6/5.2/2.1/1.0 (BP=1.000, ratio=1.527, hyp_len=17455, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.19.3.46-31.86.3.32-27.80.pth
BLEU = 3.69, 17.0/5.4/2.1/1.0 (BP=1.000, ratio=1.536, hyp_len=17565, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.20.3.47-31.99.3.28-26.45.pth
BLEU = 3.50, 16.2/5.0/2.0/0.9 (BP=1.000, ratio=1.628, hyp_len=18613, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.21.3.38-29.45.3.24-25.66.pth
BLEU = 3.51, 16.0/5.0/2.0/0.9 (BP=1.000, ratio=1.617, hyp_len=18485, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.22.3.42-30.55.3.21-24.70.pth
BLEU = 3.15, 14.5/4.5/1.8/0.9 (BP=1.000, ratio=1.813, hyp_len=20725, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.23.3.33-28.05.3.17-23.89.pth
BLEU = 3.65, 16.3/5.3/2.1/1.0 (BP=1.000, ratio=1.688, hyp_len=19294, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.24.3.30-27.15.3.14-23.15.pth
BLEU = 3.67, 16.1/5.2/2.1/1.0 (BP=1.000, ratio=1.625, hyp_len=18582, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.25.3.29-26.87.3.11-22.49.pth
BLEU = 4.15, 18.0/6.1/2.5/1.1 (BP=1.000, ratio=1.546, hyp_len=17673, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.26.3.25-25.75.3.08-21.74.pth
BLEU = 3.57, 15.6/5.2/2.1/0.9 (BP=1.000, ratio=1.724, hyp_len=19707, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.27.3.26-26.15.3.05-21.16.pth
BLEU = 4.82, 20.2/6.9/2.9/1.4 (BP=1.000, ratio=1.364, hyp_len=15596, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.28.3.26-25.99.3.03-20.69.pth
BLEU = 4.59, 19.2/6.6/2.8/1.2 (BP=1.000, ratio=1.532, hyp_len=17514, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.29.3.19-24.19.3.00-20.13.pth
BLEU = 4.80, 19.3/6.8/2.9/1.4 (BP=1.000, ratio=1.522, hyp_len=17394, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.30.3.21-24.75.2.98-19.78.pth
BLEU = 4.37, 18.2/6.4/2.7/1.2 (BP=1.000, ratio=1.650, hyp_len=18859, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/baseline/transformer/mybk-40epoch
Evaluation result for the model: transformer-model-mybk.01.6.05-425.92.5.88-359.34.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 31.8/0.0/0.0/0.0 (BP=0.083, ratio=0.286, hyp_len=3271, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.02.5.46-235.28.5.33-205.85.pth
BLEU = 0.00, 61.2/0.3/0.0/0.0 (BP=0.011, ratio=0.181, hyp_len=2074, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.03.5.03-153.45.4.92-136.68.pth
BLEU = 0.00, 61.2/0.3/0.0/0.0 (BP=0.011, ratio=0.181, hyp_len=2074, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.04.4.77-117.90.4.66-105.87.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 40.7/0.2/0.0/0.0 (BP=0.120, ratio=0.321, hyp_len=3664, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.05.4.54-93.71.4.48-88.15.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 52.6/0.1/0.0/0.0 (BP=0.076, ratio=0.280, hyp_len=3196, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.06.4.43-84.17.4.33-76.06.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 49.2/1.7/0.0/0.0 (BP=0.154, ratio=0.348, hyp_len=3979, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.07.4.29-73.01.4.21-67.69.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 46.5/4.9/2.4/0.0 (BP=0.172, ratio=0.363, hyp_len=4145, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.08.4.18-65.09.4.11-60.88.pth
BLEU = 2.59, 31.4/5.0/3.1/1.5 (BP=0.499, ratio=0.590, hyp_len=6741, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.09.4.11-60.65.4.01-54.95.pth
BLEU = 3.68, 27.0/6.0/2.9/1.5 (BP=0.711, ratio=0.746, hyp_len=8527, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.10.4.06-58.18.3.93-50.97.pth
BLEU = 3.95, 21.8/5.4/2.1/1.0 (BP=0.992, ratio=0.992, hyp_len=11342, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.11.3.92-50.27.3.85-46.82.pth
BLEU = 3.40, 18.9/5.0/1.7/0.8 (BP=1.000, ratio=1.188, hyp_len=13583, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.12.3.84-46.30.3.77-43.51.pth
BLEU = 2.48, 13.8/3.7/1.2/0.6 (BP=1.000, ratio=1.621, hyp_len=18529, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.13.3.85-47.10.3.71-40.82.pth
BLEU = 2.39, 12.7/3.4/1.3/0.6 (BP=1.000, ratio=1.887, hyp_len=21567, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.14.3.69-40.18.3.64-38.04.pth
BLEU = 2.29, 11.5/3.2/1.3/0.6 (BP=1.000, ratio=2.116, hyp_len=24186, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.15.3.68-39.59.3.58-35.92.pth
BLEU = 2.74, 13.5/3.8/1.5/0.7 (BP=1.000, ratio=1.824, hyp_len=20851, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.16.3.63-37.71.3.53-33.98.pth
BLEU = 2.53, 12.4/3.5/1.4/0.7 (BP=1.000, ratio=2.009, hyp_len=22962, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.17.3.60-36.57.3.47-32.27.pth
BLEU = 2.81, 13.1/3.8/1.6/0.8 (BP=1.000, ratio=1.839, hyp_len=21019, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.18.3.56-35.20.3.43-30.81.pth
BLEU = 2.91, 13.8/3.9/1.6/0.8 (BP=1.000, ratio=1.730, hyp_len=19772, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.19.3.50-33.21.3.38-29.43.pth
BLEU = 3.88, 17.9/5.3/2.2/1.1 (BP=1.000, ratio=1.363, hyp_len=15585, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.20.3.49-32.78.3.34-28.22.pth
BLEU = 3.32, 15.3/4.6/1.9/0.9 (BP=1.000, ratio=1.562, hyp_len=17856, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.21.3.47-32.12.3.30-27.15.pth
BLEU = 3.73, 17.2/5.3/2.1/1.0 (BP=1.000, ratio=1.470, hyp_len=16802, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.22.3.40-30.05.3.27-26.29.pth
BLEU = 3.79, 17.1/5.2/2.2/1.1 (BP=1.000, ratio=1.431, hyp_len=16363, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.23.3.40-29.85.3.24-25.41.pth
BLEU = 3.63, 16.0/5.0/2.1/1.1 (BP=1.000, ratio=1.535, hyp_len=17544, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.24.3.35-28.56.3.19-24.36.pth
BLEU = 4.01, 17.8/5.6/2.4/1.1 (BP=1.000, ratio=1.480, hyp_len=16918, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.25.3.37-29.04.3.16-23.46.pth
BLEU = 5.07, 21.2/7.0/3.0/1.5 (BP=1.000, ratio=1.260, hyp_len=14410, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.26.3.25-25.89.3.14-23.04.pth
BLEU = 4.41, 18.8/6.1/2.6/1.2 (BP=1.000, ratio=1.421, hyp_len=16245, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.27.3.27-26.31.3.09-22.07.pth
BLEU = 5.14, 21.2/7.1/3.1/1.5 (BP=1.000, ratio=1.276, hyp_len=14588, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.28.3.30-27.02.3.08-21.66.pth
BLEU = 4.78, 20.6/6.7/2.8/1.3 (BP=1.000, ratio=1.300, hyp_len=14865, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.29.3.22-25.04.3.05-21.06.pth
BLEU = 5.12, 22.2/7.4/3.0/1.4 (BP=1.000, ratio=1.274, hyp_len=14565, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.30.3.20-24.42.3.02-20.57.pth
BLEU = 5.67, 23.3/7.9/3.5/1.6 (BP=1.000, ratio=1.205, hyp_len=13772, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.31.3.15-23.24.3.01-20.20.pth
BLEU = 6.40, 25.5/8.9/3.9/1.9 (BP=1.000, ratio=1.137, hyp_len=12997, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.32.3.18-23.98.2.98-19.74.pth
BLEU = 5.90, 24.3/8.4/3.6/1.6 (BP=1.000, ratio=1.199, hyp_len=13703, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.33.3.11-22.52.2.95-19.17.pth
BLEU = 5.91, 24.5/8.4/3.7/1.6 (BP=1.000, ratio=1.262, hyp_len=14426, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.34.3.09-21.90.2.94-18.89.pth
BLEU = 6.34, 25.2/9.0/4.0/1.8 (BP=1.000, ratio=1.206, hyp_len=13785, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.35.3.09-21.88.2.92-18.45.pth
BLEU = 7.08, 27.1/9.9/4.5/2.1 (BP=1.000, ratio=1.188, hyp_len=13584, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.36.3.09-21.98.2.90-18.14.pth
BLEU = 6.86, 27.1/9.9/4.3/1.9 (BP=1.000, ratio=1.183, hyp_len=13526, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.37.3.12-22.75.2.88-17.80.pth
BLEU = 6.76, 26.0/9.5/4.3/2.0 (BP=1.000, ratio=1.226, hyp_len=14016, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.38.3.03-20.69.2.87-17.59.pth
BLEU = 7.75, 29.2/10.8/5.0/2.3 (BP=1.000, ratio=1.117, hyp_len=12767, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.39.3.04-20.86.2.84-17.19.pth
BLEU = 7.70, 29.5/11.1/5.0/2.2 (BP=1.000, ratio=1.138, hyp_len=13007, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.40.3.05-21.02.2.83-16.96.pth
BLEU = 8.23, 30.9/11.8/5.3/2.4 (BP=1.000, ratio=1.098, hyp_len=12547, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/baseline/transformer/mybk-50epoch
Evaluation result for the model: transformer-model-mybk.01.6.01-406.58.5.88-359.47.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 36.1/0.0/0.0/0.0 (BP=0.173, ratio=0.363, hyp_len=4148, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.02.5.47-238.07.5.37-214.65.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 9.0/0.0/0.0/0.0 (BP=0.300, ratio=0.454, hyp_len=5185, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.03.5.04-153.79.4.93-138.38.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 28.5/0.3/0.0/0.0 (BP=0.430, ratio=0.542, hyp_len=6197, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.04.4.76-116.98.4.66-105.49.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 38.2/0.4/0.0/0.0 (BP=0.238, ratio=0.411, hyp_len=4696, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.05.4.55-94.41.4.48-88.50.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 35.7/0.7/0.0/0.0 (BP=0.424, ratio=0.538, hyp_len=6152, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.06.4.39-80.96.4.34-76.46.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 37.5/1.2/0.0/0.0 (BP=0.385, ratio=0.512, hyp_len=5851, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.07.4.27-71.75.4.21-67.55.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 30.1/2.1/0.0/0.0 (BP=0.585, ratio=0.651, hyp_len=7440, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.08.4.17-64.83.4.10-60.15.pth
BLEU = 3.31, 26.5/6.3/2.2/1.0 (BP=0.764, ratio=0.788, hyp_len=9006, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.09.4.08-59.41.4.00-54.84.pth
BLEU = 4.25, 25.3/7.2/2.9/1.2 (BP=0.845, ratio=0.856, hyp_len=9789, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.10.3.99-53.96.3.91-49.96.pth
BLEU = 4.06, 24.7/7.0/2.8/1.2 (BP=0.821, ratio=0.835, hyp_len=9550, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.11.3.88-48.36.3.84-46.48.pth
BLEU = 4.18, 22.3/6.1/2.7/1.1 (BP=0.936, ratio=0.938, hyp_len=10727, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.12.3.87-47.97.3.76-43.16.pth
BLEU = 3.81, 18.7/5.1/2.2/1.0 (BP=1.000, ratio=1.132, hyp_len=12938, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.13.3.81-44.94.3.69-40.24.pth
BLEU = 4.16, 18.7/5.4/2.4/1.2 (BP=1.000, ratio=1.197, hyp_len=13680, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.14.3.73-41.56.3.64-38.00.pth
BLEU = 4.18, 17.7/5.4/2.4/1.3 (BP=1.000, ratio=1.247, hyp_len=14254, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.15.3.68-39.78.3.59-36.23.pth
BLEU = 4.02, 17.6/5.3/2.3/1.2 (BP=1.000, ratio=1.269, hyp_len=14511, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.16.3.65-38.35.3.54-34.34.pth
BLEU = 2.96, 13.4/4.0/1.7/0.8 (BP=1.000, ratio=1.748, hyp_len=19980, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.17.3.58-35.96.3.49-32.81.pth
BLEU = 3.13, 14.3/4.3/1.8/0.9 (BP=1.000, ratio=1.661, hyp_len=18993, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.18.3.54-34.37.3.44-31.29.pth
BLEU = 3.29, 14.6/4.4/1.9/1.0 (BP=1.000, ratio=1.554, hyp_len=17770, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.19.3.49-32.95.3.40-30.08.pth
BLEU = 3.33, 14.8/4.5/1.9/1.0 (BP=1.000, ratio=1.578, hyp_len=18044, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.20.3.46-31.67.3.37-28.94.pth
BLEU = 3.35, 14.7/4.5/1.9/1.0 (BP=1.000, ratio=1.561, hyp_len=17842, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.21.3.43-30.92.3.33-28.03.pth
BLEU = 2.71, 12.3/3.7/1.5/0.8 (BP=1.000, ratio=1.940, hyp_len=22181, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.22.3.41-30.28.3.30-27.07.pth
BLEU = 2.83, 13.0/3.9/1.6/0.8 (BP=1.000, ratio=1.840, hyp_len=21039, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.23.3.37-29.21.3.27-26.23.pth
BLEU = 2.86, 13.1/3.9/1.6/0.8 (BP=1.000, ratio=1.851, hyp_len=21157, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.24.3.35-28.40.3.22-25.15.pth
BLEU = 2.68, 12.4/3.7/1.5/0.7 (BP=1.000, ratio=2.062, hyp_len=23575, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.25.3.31-27.45.3.20-24.46.pth
BLEU = 3.30, 15.0/4.5/1.9/0.9 (BP=1.000, ratio=1.622, hyp_len=18543, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.26.3.32-27.68.3.17-23.70.pth
BLEU = 3.28, 14.7/4.6/1.9/0.9 (BP=1.000, ratio=1.757, hyp_len=20084, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.27.3.29-26.73.3.13-22.95.pth
BLEU = 3.72, 16.5/5.1/2.1/1.1 (BP=1.000, ratio=1.557, hyp_len=17804, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.28.3.29-26.77.3.12-22.61.pth
BLEU = 3.89, 17.3/5.4/2.3/1.1 (BP=1.000, ratio=1.487, hyp_len=17005, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.29.3.20-24.63.3.09-22.04.pth
BLEU = 3.79, 16.9/5.4/2.2/1.0 (BP=1.000, ratio=1.600, hyp_len=18287, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.30.3.23-25.36.3.06-21.38.pth
BLEU = 4.89, 20.5/6.8/2.9/1.4 (BP=1.000, ratio=1.287, hyp_len=14714, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.31.3.16-23.50.3.04-20.86.pth
BLEU = 3.80, 16.9/5.5/2.2/1.0 (BP=1.000, ratio=1.663, hyp_len=19013, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.32.3.15-23.35.3.02-20.54.pth
BLEU = 4.49, 19.3/6.4/2.7/1.2 (BP=1.000, ratio=1.432, hyp_len=16374, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.33.3.17-23.85.2.99-19.92.pth
BLEU = 5.05, 21.7/7.2/3.0/1.4 (BP=1.000, ratio=1.269, hyp_len=14511, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.34.3.07-21.56.2.98-19.62.pth
BLEU = 4.90, 20.8/6.9/3.0/1.4 (BP=1.000, ratio=1.343, hyp_len=15349, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.35.3.15-23.31.2.95-19.20.pth
BLEU = 5.44, 22.8/7.8/3.3/1.5 (BP=1.000, ratio=1.273, hyp_len=14548, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.36.3.11-22.48.2.93-18.79.pth
BLEU = 5.41, 22.7/7.7/3.2/1.5 (BP=1.000, ratio=1.301, hyp_len=14875, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.37.3.12-22.58.2.92-18.53.pth
BLEU = 5.43, 22.3/7.7/3.3/1.5 (BP=1.000, ratio=1.300, hyp_len=14864, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.38.3.11-22.47.2.90-18.21.pth
BLEU = 5.91, 24.4/8.5/3.6/1.7 (BP=1.000, ratio=1.241, hyp_len=14189, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.39.3.02-20.52.2.88-17.73.pth
BLEU = 6.26, 25.1/8.9/3.9/1.8 (BP=1.000, ratio=1.212, hyp_len=13857, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.40.3.11-22.33.2.86-17.51.pth
BLEU = 6.73, 26.4/9.5/4.2/2.0 (BP=1.000, ratio=1.178, hyp_len=13467, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.41.3.03-20.79.2.85-17.23.pth
BLEU = 6.42, 25.6/9.3/3.9/1.8 (BP=1.000, ratio=1.257, hyp_len=14374, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.42.3.02-20.51.2.84-17.13.pth
BLEU = 6.54, 26.5/9.5/4.0/1.8 (BP=1.000, ratio=1.175, hyp_len=13429, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.43.3.01-20.37.2.82-16.70.pth
BLEU = 6.32, 24.5/8.9/4.0/1.8 (BP=1.000, ratio=1.344, hyp_len=15365, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.44.3.01-20.36.2.81-16.62.pth
BLEU = 6.92, 26.7/9.9/4.4/2.0 (BP=1.000, ratio=1.228, hyp_len=14035, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.45.2.98-19.77.2.80-16.44.pth
BLEU = 7.11, 27.1/10.1/4.5/2.1 (BP=1.000, ratio=1.196, hyp_len=13675, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.46.2.97-19.49.2.78-16.12.pth
BLEU = 7.03, 27.1/10.1/4.5/2.0 (BP=1.000, ratio=1.215, hyp_len=13895, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.47.2.96-19.29.2.77-16.01.pth
BLEU = 7.38, 27.9/10.6/4.8/2.1 (BP=1.000, ratio=1.238, hyp_len=14154, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.48.2.96-19.35.2.76-15.74.pth
BLEU = 7.64, 28.4/10.8/4.9/2.2 (BP=1.000, ratio=1.256, hyp_len=14363, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.49.2.98-19.78.2.74-15.51.pth
BLEU = 8.54, 30.6/11.9/5.6/2.6 (BP=1.000, ratio=1.152, hyp_len=13165, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.50.2.94-18.96.2.73-15.41.pth
BLEU = 8.05, 29.8/11.2/5.2/2.4 (BP=1.000, ratio=1.157, hyp_len=13230, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/baseline/transformer/mybk-60epoch
Evaluation result for the model: transformer-model-mybk.01.6.13-459.18.6.00-401.44.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 1.9/0.0/0.0/0.0 (BP=0.069, ratio=0.272, hyp_len=3113, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.02.5.56-258.56.5.46-235.29.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 8.8/0.0/0.0/0.0 (BP=0.300, ratio=0.453, hyp_len=5184, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.03.5.11-165.11.5.00-148.05.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.8/0.3/0.0/0.0 (BP=0.504, ratio=0.594, hyp_len=6786, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.04.4.77-118.15.4.70-110.25.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 30.5/0.9/0.0/0.0 (BP=0.430, ratio=0.542, hyp_len=6199, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.05.4.55-95.07.4.50-89.65.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 28.7/0.2/0.0/0.0 (BP=0.440, ratio=0.549, hyp_len=6275, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.06.4.45-85.57.4.34-76.90.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 27.5/0.9/0.0/0.0 (BP=0.551, ratio=0.626, hyp_len=7162, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.07.4.25-69.91.4.21-67.17.pth
BLEU = 2.60, 30.5/4.8/3.3/1.8 (BP=0.483, ratio=0.578, hyp_len=6613, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.08.4.16-63.99.4.09-59.74.pth
BLEU = 3.08, 24.3/4.2/2.8/1.6 (BP=0.672, ratio=0.715, hyp_len=8176, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.09.4.08-59.36.4.00-54.68.pth
BLEU = 3.24, 22.7/3.9/2.5/1.3 (BP=0.785, ratio=0.805, hyp_len=9201, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.10.4.04-56.63.3.93-50.76.pth
BLEU = 2.69, 16.1/2.8/1.5/0.8 (BP=1.000, ratio=1.215, hyp_len=13894, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.11.3.93-50.82.3.85-47.10.pth
BLEU = 2.69, 14.4/3.7/1.4/0.7 (BP=1.000, ratio=1.547, hyp_len=17690, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.12.3.89-48.76.3.78-43.68.pth
BLEU = 3.93, 18.6/5.4/2.1/1.1 (BP=1.000, ratio=1.266, hyp_len=14473, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.13.3.84-46.49.3.73-41.54.pth
BLEU = 4.07, 18.8/5.6/2.3/1.1 (BP=1.000, ratio=1.241, hyp_len=14188, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.14.3.75-42.71.3.67-39.18.pth
BLEU = 4.15, 19.4/5.9/2.3/1.1 (BP=1.000, ratio=1.263, hyp_len=14443, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.15.3.74-42.22.3.61-36.84.pth
BLEU = 4.24, 19.2/5.7/2.4/1.2 (BP=1.000, ratio=1.210, hyp_len=13832, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.16.3.64-38.06.3.56-35.03.pth
BLEU = 3.90, 18.2/5.3/2.2/1.1 (BP=1.000, ratio=1.311, hyp_len=14985, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.17.3.60-36.53.3.51-33.31.pth
BLEU = 3.85, 18.4/5.4/2.1/1.1 (BP=1.000, ratio=1.345, hyp_len=15376, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.18.3.60-36.72.3.46-31.83.pth
BLEU = 4.02, 18.7/5.5/2.2/1.1 (BP=1.000, ratio=1.303, hyp_len=14896, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.19.3.54-34.49.3.42-30.55.pth
BLEU = 3.36, 16.0/4.6/1.8/0.9 (BP=1.000, ratio=1.553, hyp_len=17755, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.20.3.45-31.39.3.37-29.13.pth
BLEU = 3.81, 17.8/5.2/2.1/1.1 (BP=1.000, ratio=1.435, hyp_len=16405, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.21.3.42-30.61.3.34-28.08.pth
BLEU = 4.66, 20.9/6.4/2.6/1.4 (BP=1.000, ratio=1.244, hyp_len=14221, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.22.3.43-30.79.3.31-27.28.pth
BLEU = 4.31, 20.2/6.0/2.4/1.2 (BP=1.000, ratio=1.305, hyp_len=14918, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.23.3.37-29.12.3.27-26.27.pth
BLEU = 4.27, 19.0/5.9/2.5/1.2 (BP=1.000, ratio=1.375, hyp_len=15719, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.24.3.34-28.27.3.24-25.45.pth
BLEU = 4.77, 20.5/6.6/2.8/1.4 (BP=1.000, ratio=1.261, hyp_len=14421, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.25.3.33-28.02.3.21-24.68.pth
BLEU = 3.76, 16.7/5.2/2.2/1.0 (BP=1.000, ratio=1.586, hyp_len=18126, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.26.3.30-27.20.3.18-24.02.pth
BLEU = 4.15, 18.7/5.9/2.4/1.1 (BP=1.000, ratio=1.466, hyp_len=16757, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.27.3.27-26.30.3.15-23.28.pth
BLEU = 4.59, 20.4/6.4/2.7/1.3 (BP=1.000, ratio=1.266, hyp_len=14475, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.28.3.23-25.35.3.12-22.70.pth
BLEU = 5.57, 23.9/7.9/3.3/1.5 (BP=1.000, ratio=1.152, hyp_len=13167, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.29.3.26-26.00.3.09-22.08.pth
BLEU = 5.02, 21.9/7.1/3.0/1.4 (BP=1.000, ratio=1.263, hyp_len=14442, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.30.3.22-25.03.3.08-21.68.pth
BLEU = 5.07, 21.3/7.3/3.0/1.4 (BP=1.000, ratio=1.298, hyp_len=14843, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.31.3.19-24.32.3.05-21.08.pth
BLEU = 5.76, 23.5/8.2/3.6/1.6 (BP=1.000, ratio=1.221, hyp_len=13962, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.32.3.16-23.51.3.02-20.48.pth
BLEU = 5.74, 24.0/8.2/3.5/1.6 (BP=1.000, ratio=1.187, hyp_len=13569, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.33.3.15-23.31.3.00-20.17.pth
BLEU = 6.37, 25.8/9.0/4.0/1.8 (BP=1.000, ratio=1.152, hyp_len=13170, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.34.3.18-24.00.2.98-19.65.pth
BLEU = 6.17, 25.3/8.8/3.8/1.7 (BP=1.000, ratio=1.187, hyp_len=13568, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.35.3.16-23.59.2.97-19.41.pth
BLEU = 7.41, 28.8/10.2/4.7/2.2 (BP=1.000, ratio=1.047, hyp_len=11967, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.36.3.05-21.19.2.95-19.06.pth
BLEU = 6.04, 24.6/8.6/3.8/1.6 (BP=1.000, ratio=1.200, hyp_len=13722, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.37.3.10-22.21.2.94-18.90.pth
BLEU = 6.31, 25.0/8.9/4.1/1.8 (BP=1.000, ratio=1.242, hyp_len=14201, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.38.3.10-22.30.2.91-18.37.pth
BLEU = 7.11, 27.5/10.0/4.6/2.0 (BP=1.000, ratio=1.185, hyp_len=13548, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.39.3.06-21.32.2.90-18.09.pth
BLEU = 7.29, 28.1/10.3/4.7/2.1 (BP=1.000, ratio=1.168, hyp_len=13358, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.40.3.10-22.15.2.87-17.66.pth
BLEU = 7.84, 29.1/11.0/5.1/2.3 (BP=1.000, ratio=1.146, hyp_len=13101, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.41.3.05-21.21.2.86-17.50.pth
BLEU = 7.79, 28.7/10.7/5.0/2.4 (BP=1.000, ratio=1.126, hyp_len=12874, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.42.3.01-20.23.2.86-17.40.pth
BLEU = 7.05, 26.7/10.1/4.6/2.0 (BP=1.000, ratio=1.269, hyp_len=14511, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.43.3.00-20.01.2.84-17.12.pth
BLEU = 8.29, 29.6/11.6/5.6/2.5 (BP=1.000, ratio=1.179, hyp_len=13481, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.44.3.04-20.89.2.82-16.86.pth
BLEU = 7.38, 27.3/10.3/4.9/2.2 (BP=1.000, ratio=1.240, hyp_len=14172, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.45.2.99-19.87.2.81-16.62.pth
BLEU = 8.19, 29.9/11.5/5.5/2.4 (BP=1.000, ratio=1.152, hyp_len=13173, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.46.2.98-19.73.2.80-16.39.pth
BLEU = 8.42, 30.1/11.7/5.6/2.6 (BP=1.000, ratio=1.156, hyp_len=13210, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.47.2.99-19.93.2.78-16.15.pth
BLEU = 8.57, 30.4/11.8/5.7/2.6 (BP=1.000, ratio=1.171, hyp_len=13392, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.48.2.97-19.46.2.78-16.07.pth
BLEU = 8.48, 30.7/12.1/5.6/2.5 (BP=1.000, ratio=1.156, hyp_len=13212, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.49.2.99-19.91.2.77-15.89.pth
BLEU = 8.96, 32.2/12.6/5.9/2.7 (BP=1.000, ratio=1.111, hyp_len=12706, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.50.2.92-18.50.2.76-15.84.pth
BLEU = 8.25, 30.0/11.4/5.3/2.5 (BP=1.000, ratio=1.148, hyp_len=13122, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.51.2.94-18.93.2.74-15.56.pth
BLEU = 8.84, 31.7/12.2/5.8/2.7 (BP=1.000, ratio=1.117, hyp_len=12771, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.52.2.91-18.39.2.74-15.50.pth
BLEU = 8.96, 31.6/12.5/6.0/2.8 (BP=1.000, ratio=1.121, hyp_len=12820, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.53.2.89-17.96.2.73-15.28.pth
BLEU = 9.56, 33.0/13.1/6.3/3.1 (BP=1.000, ratio=1.090, hyp_len=12463, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.54.2.87-17.63.2.71-15.06.pth
BLEU = 9.09, 31.3/12.4/6.1/2.9 (BP=1.000, ratio=1.133, hyp_len=12958, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.55.2.87-17.61.2.71-15.05.pth
BLEU = 8.97, 31.8/12.4/5.9/2.8 (BP=1.000, ratio=1.132, hyp_len=12941, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.56.2.92-18.46.2.70-14.86.pth
BLEU = 9.17, 31.8/12.6/6.2/2.9 (BP=1.000, ratio=1.130, hyp_len=12913, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.57.2.88-17.78.2.69-14.69.pth
BLEU = 10.18, 34.0/13.9/6.8/3.3 (BP=1.000, ratio=1.101, hyp_len=12586, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.58.2.83-17.01.2.67-14.50.pth
BLEU = 10.17, 34.4/14.0/6.8/3.2 (BP=1.000, ratio=1.089, hyp_len=12451, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.59.2.88-17.82.2.68-14.58.pth
BLEU = 9.60, 32.6/13.0/6.4/3.1 (BP=1.000, ratio=1.131, hyp_len=12929, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.60.2.84-17.04.2.67-14.47.pth
BLEU = 9.24, 31.9/12.7/6.1/2.9 (BP=1.000, ratio=1.149, hyp_len=13139, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/baseline/transformer/mybk-70epoch
Evaluation result for the model: transformer-model-mybk.01.6.07-434.67.5.95-382.79.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 25.0/0.0/0.0/0.0 (BP=0.173, ratio=0.363, hyp_len=4148, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.02.5.56-259.94.5.44-229.73.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 26.6/0.0/0.0/0.0 (BP=0.173, ratio=0.363, hyp_len=4148, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.03.5.07-158.42.5.00-149.02.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 38.9/0.0/0.0/0.0 (BP=0.069, ratio=0.272, hyp_len=3111, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.04.4.78-119.13.4.72-112.33.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 40.4/0.2/0.0/0.0 (BP=0.160, ratio=0.353, hyp_len=4037, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.05.4.55-94.62.4.52-91.44.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.4/0.5/0.0/0.0 (BP=0.850, ratio=0.860, hyp_len=9833, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.06.4.39-80.87.4.35-77.27.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 7.2/0.5/0.0/0.0 (BP=1.000, ratio=2.421, hyp_len=27677, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.07.4.30-73.70.4.21-67.60.pth
BLEU = 1.81, 11.9/2.2/0.9/0.5 (BP=1.000, ratio=1.805, hyp_len=20640, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.08.4.11-60.83.4.10-60.25.pth
BLEU = 1.35, 8.3/2.0/0.6/0.3 (BP=1.000, ratio=2.865, hyp_len=32755, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.09.4.05-57.52.4.00-54.62.pth
BLEU = 1.99, 11.7/2.7/1.0/0.5 (BP=1.000, ratio=2.059, hyp_len=23544, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.10.3.97-53.19.3.92-50.35.pth
BLEU = 2.57, 13.1/3.5/1.4/0.7 (BP=1.000, ratio=1.918, hyp_len=21928, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.11.3.88-48.53.3.84-46.29.pth
BLEU = 3.52, 17.0/4.8/2.0/1.0 (BP=1.000, ratio=1.396, hyp_len=15963, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.12.3.85-47.03.3.76-43.14.pth
BLEU = 3.32, 16.0/4.5/1.9/0.9 (BP=1.000, ratio=1.397, hyp_len=15970, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.13.3.76-42.82.3.71-40.88.pth
BLEU = 3.34, 15.8/4.5/1.9/0.9 (BP=1.000, ratio=1.413, hyp_len=16155, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.14.3.72-41.13.3.64-38.17.pth
BLEU = 3.68, 16.6/4.9/2.1/1.1 (BP=1.000, ratio=1.319, hyp_len=15079, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.15.3.68-39.68.3.60-36.43.pth
BLEU = 3.66, 16.9/5.0/2.1/1.0 (BP=1.000, ratio=1.317, hyp_len=15051, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.16.3.59-36.19.3.54-34.35.pth
BLEU = 3.43, 15.8/4.7/1.9/1.0 (BP=1.000, ratio=1.436, hyp_len=16420, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.17.3.58-35.83.3.49-32.90.pth
BLEU = 3.46, 16.8/4.9/1.9/0.9 (BP=1.000, ratio=1.425, hyp_len=16296, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.18.3.58-35.96.3.45-31.60.pth
BLEU = 3.58, 17.2/5.0/2.0/0.9 (BP=1.000, ratio=1.467, hyp_len=16768, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.19.3.46-31.91.3.41-30.34.pth
BLEU = 3.97, 19.2/5.5/2.2/1.1 (BP=1.000, ratio=1.300, hyp_len=14865, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.20.3.55-34.95.3.37-29.03.pth
BLEU = 4.32, 19.8/5.9/2.4/1.2 (BP=1.000, ratio=1.279, hyp_len=14618, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.21.3.46-31.74.3.33-27.91.pth
BLEU = 3.91, 18.3/5.4/2.2/1.1 (BP=1.000, ratio=1.358, hyp_len=15530, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.22.3.45-31.65.3.28-26.59.pth
BLEU = 4.56, 20.6/6.4/2.6/1.3 (BP=1.000, ratio=1.255, hyp_len=14345, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.23.3.42-30.66.3.25-25.91.pth
BLEU = 4.17, 18.9/6.0/2.4/1.1 (BP=1.000, ratio=1.418, hyp_len=16212, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.24.3.39-29.55.3.23-25.19.pth
BLEU = 4.69, 21.0/6.6/2.7/1.3 (BP=1.000, ratio=1.247, hyp_len=14257, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.25.3.37-29.02.3.18-24.00.pth
BLEU = 4.71, 20.8/6.6/2.7/1.3 (BP=1.000, ratio=1.300, hyp_len=14863, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.26.3.26-25.96.3.15-23.43.pth
BLEU = 5.15, 23.0/7.3/2.9/1.4 (BP=1.000, ratio=1.219, hyp_len=13933, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.27.3.31-27.40.3.13-22.83.pth
BLEU = 5.00, 21.9/7.0/2.9/1.4 (BP=1.000, ratio=1.247, hyp_len=14253, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.28.3.27-26.35.3.09-22.00.pth
BLEU = 5.24, 22.3/7.3/3.1/1.5 (BP=1.000, ratio=1.224, hyp_len=13995, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.29.3.25-25.81.3.07-21.62.pth
BLEU = 4.61, 20.4/6.7/2.7/1.2 (BP=1.000, ratio=1.441, hyp_len=16477, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.30.3.26-25.95.3.05-21.13.pth
BLEU = 4.47, 19.8/6.5/2.6/1.2 (BP=1.000, ratio=1.457, hyp_len=16662, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.31.3.17-23.69.3.03-20.64.pth
BLEU = 5.92, 24.4/8.3/3.6/1.7 (BP=1.000, ratio=1.182, hyp_len=13513, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.32.3.19-24.41.3.00-20.05.pth
BLEU = 4.87, 20.7/7.0/3.0/1.3 (BP=1.000, ratio=1.452, hyp_len=16598, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.33.3.17-23.81.2.98-19.67.pth
BLEU = 6.33, 25.1/8.7/3.9/1.9 (BP=1.000, ratio=1.141, hyp_len=13046, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.34.3.11-22.45.2.96-19.23.pth
BLEU = 6.78, 26.9/9.8/4.2/1.9 (BP=1.000, ratio=1.129, hyp_len=12902, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.35.3.12-22.71.2.94-18.95.pth
BLEU = 6.90, 26.7/9.6/4.3/2.1 (BP=1.000, ratio=1.106, hyp_len=12643, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.36.3.15-23.36.2.93-18.68.pth
BLEU = 6.68, 26.2/9.4/4.2/1.9 (BP=1.000, ratio=1.126, hyp_len=12867, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.37.3.12-22.55.2.91-18.36.pth
BLEU = 6.76, 26.7/9.7/4.2/1.9 (BP=1.000, ratio=1.152, hyp_len=13167, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.38.3.09-21.95.2.89-17.93.pth
BLEU = 7.42, 27.9/10.5/4.7/2.2 (BP=1.000, ratio=1.149, hyp_len=13135, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.39.3.13-22.82.2.88-17.80.pth
BLEU = 6.62, 25.9/9.7/4.2/1.8 (BP=1.000, ratio=1.243, hyp_len=14210, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.40.3.07-21.53.2.85-17.31.pth
BLEU = 7.03, 26.8/10.0/4.5/2.0 (BP=1.000, ratio=1.222, hyp_len=13971, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.41.3.06-21.25.2.84-17.06.pth
BLEU = 8.03, 29.2/11.1/5.2/2.5 (BP=1.000, ratio=1.083, hyp_len=12378, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.42.3.03-20.71.2.82-16.71.pth
BLEU = 7.79, 28.8/11.2/5.1/2.2 (BP=1.000, ratio=1.159, hyp_len=13248, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.43.3.04-20.88.2.81-16.63.pth
BLEU = 7.54, 28.2/10.6/4.9/2.2 (BP=1.000, ratio=1.157, hyp_len=13222, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.44.3.02-20.42.2.79-16.30.pth
BLEU = 8.46, 30.1/11.6/5.6/2.6 (BP=1.000, ratio=1.129, hyp_len=12909, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.45.2.91-18.33.2.78-16.14.pth
BLEU = 8.02, 29.1/11.2/5.3/2.4 (BP=1.000, ratio=1.146, hyp_len=13104, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.46.2.96-19.35.2.78-16.04.pth
BLEU = 7.79, 28.0/10.7/5.1/2.4 (BP=1.000, ratio=1.178, hyp_len=13472, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.47.2.99-19.93.2.76-15.78.pth
BLEU = 8.02, 28.9/11.0/5.3/2.5 (BP=1.000, ratio=1.181, hyp_len=13504, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.48.2.95-19.17.2.75-15.59.pth
BLEU = 8.72, 29.9/11.6/5.8/2.9 (BP=1.000, ratio=1.102, hyp_len=12595, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.49.2.97-19.47.2.74-15.41.pth
BLEU = 8.80, 31.1/12.3/5.8/2.7 (BP=1.000, ratio=1.110, hyp_len=12692, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.50.2.91-18.29.2.72-15.19.pth
BLEU = 8.94, 30.9/12.3/5.9/2.8 (BP=1.000, ratio=1.139, hyp_len=13018, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.51.2.92-18.58.2.71-15.02.pth
BLEU = 8.71, 30.3/11.9/5.7/2.8 (BP=1.000, ratio=1.151, hyp_len=13160, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.52.2.92-18.56.2.70-14.86.pth
BLEU = 8.67, 29.9/11.8/5.7/2.8 (BP=1.000, ratio=1.176, hyp_len=13449, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.53.2.93-18.68.2.69-14.76.pth
BLEU = 8.89, 30.5/12.0/5.9/2.9 (BP=1.000, ratio=1.116, hyp_len=12757, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.54.2.86-17.52.2.69-14.66.pth
BLEU = 8.77, 30.4/12.0/5.9/2.8 (BP=1.000, ratio=1.131, hyp_len=12933, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.55.2.91-18.38.2.67-14.41.pth
BLEU = 9.39, 32.0/12.8/6.2/3.1 (BP=1.000, ratio=1.120, hyp_len=12807, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.56.2.89-17.90.2.66-14.34.pth
BLEU = 9.92, 32.9/13.5/6.6/3.3 (BP=1.000, ratio=1.097, hyp_len=12545, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.57.2.83-16.89.2.65-14.15.pth
BLEU = 10.05, 33.3/13.6/6.7/3.3 (BP=1.000, ratio=1.065, hyp_len=12174, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.58.2.84-17.07.2.65-14.22.pth
BLEU = 8.60, 28.8/11.8/5.7/2.8 (BP=1.000, ratio=1.246, hyp_len=14240, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.59.2.86-17.48.2.64-14.02.pth
BLEU = 9.57, 31.9/13.1/6.4/3.2 (BP=1.000, ratio=1.137, hyp_len=12996, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.60.2.89-18.06.2.63-13.81.pth
BLEU = 9.97, 32.8/13.4/6.6/3.4 (BP=1.000, ratio=1.089, hyp_len=12444, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.61.2.79-16.23.2.63-13.83.pth
BLEU = 9.98, 32.5/13.3/6.7/3.4 (BP=1.000, ratio=1.087, hyp_len=12424, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.62.2.77-15.89.2.61-13.65.pth
BLEU = 10.84, 34.2/14.4/7.3/3.8 (BP=1.000, ratio=1.097, hyp_len=12544, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.63.2.84-17.18.2.60-13.41.pth
BLEU = 9.89, 32.7/13.2/6.6/3.4 (BP=1.000, ratio=1.107, hyp_len=12650, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.64.2.85-17.31.2.59-13.36.pth
BLEU = 10.81, 34.7/14.5/7.2/3.8 (BP=1.000, ratio=1.069, hyp_len=12221, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.65.2.78-16.17.2.59-13.32.pth
BLEU = 11.37, 35.7/15.2/7.7/4.0 (BP=1.000, ratio=1.035, hyp_len=11834, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.66.2.76-15.79.2.58-13.25.pth
BLEU = 10.11, 32.7/13.6/6.7/3.5 (BP=1.000, ratio=1.170, hyp_len=13371, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.67.2.75-15.70.2.57-13.10.pth
BLEU = 10.65, 34.7/14.3/7.0/3.7 (BP=1.000, ratio=1.083, hyp_len=12385, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.68.2.81-16.55.2.57-13.05.pth
BLEU = 10.33, 33.2/13.7/6.9/3.6 (BP=1.000, ratio=1.110, hyp_len=12687, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.69.2.77-16.02.2.57-13.02.pth
BLEU = 11.68, 36.7/15.3/7.8/4.3 (BP=1.000, ratio=1.035, hyp_len=11836, ref_len=11432)
Evaluation result for the model: transformer-model-mybk.70.2.79-16.36.2.55-12.86.pth
BLEU = 11.57, 35.8/15.4/7.9/4.1 (BP=1.000, ratio=1.069, hyp_len=12226, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/baseline/transformer/bkmy-30epoch
Evaluation result for the model: transformer-model-bkmy.01.5.97-390.72.5.84-345.34.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 40.1/0.5/0.0/0.0 (BP=0.089, ratio=0.292, hyp_len=3576, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.02.5.37-215.13.5.27-195.21.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 39.4/5.8/0.2/0.0 (BP=0.147, ratio=0.342, hyp_len=4188, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.03.4.89-133.37.4.81-122.59.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 35.1/1.4/0.0/0.0 (BP=0.142, ratio=0.339, hyp_len=4148, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.04.4.60-99.53.4.50-90.44.pth
BLEU = 0.63, 44.2/4.3/1.3/0.1 (BP=0.257, ratio=0.424, hyp_len=5183, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.05.4.35-77.50.4.28-72.56.pth
BLEU = 0.75, 22.2/4.0/0.8/0.1 (BP=0.442, ratio=0.550, hyp_len=6730, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.06.4.15-63.35.4.11-61.20.pth
BLEU = 1.27, 31.3/6.9/0.9/0.1 (BP=0.663, ratio=0.709, hyp_len=8672, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.07.3.99-54.22.3.97-53.21.pth
BLEU = 1.29, 28.6/6.3/0.8/0.1 (BP=0.742, ratio=0.770, hyp_len=9417, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.08.3.87-48.08.3.84-46.47.pth
BLEU = 3.75, 31.0/8.6/2.4/0.7 (BP=0.806, ratio=0.822, hyp_len=10057, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.09.3.75-42.56.3.74-41.91.pth
BLEU = 4.37, 27.8/8.2/2.8/0.8 (BP=0.920, ratio=0.923, hyp_len=11289, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.10.3.69-40.23.3.65-38.48.pth
BLEU = 4.00, 23.8/6.8/2.4/0.7 (BP=1.000, ratio=1.095, hyp_len=13397, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.11.3.59-36.22.3.56-35.25.pth
BLEU = 4.81, 27.9/8.5/3.0/0.8 (BP=0.967, ratio=0.968, hyp_len=11837, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.12.3.56-35.25.3.49-32.78.pth
BLEU = 4.78, 27.1/8.0/2.8/0.9 (BP=1.000, ratio=1.022, hyp_len=12500, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.13.3.43-30.93.3.43-30.92.pth
BLEU = 5.03, 28.0/8.5/3.0/1.0 (BP=0.985, ratio=0.985, hyp_len=12052, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.14.3.39-29.56.3.37-28.94.pth
BLEU = 4.84, 27.4/8.3/2.9/0.8 (BP=1.000, ratio=1.027, hyp_len=12563, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.15.3.31-27.51.3.31-27.48.pth
BLEU = 5.03, 26.9/8.2/3.0/1.0 (BP=1.000, ratio=1.076, hyp_len=13162, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.16.3.26-26.01.3.26-25.98.pth
BLEU = 5.38, 28.0/8.8/3.1/1.1 (BP=1.000, ratio=1.048, hyp_len=12821, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.17.3.21-24.86.3.22-25.01.pth
BLEU = 5.27, 28.1/8.9/3.1/1.0 (BP=1.000, ratio=1.057, hyp_len=12930, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.18.3.21-24.83.3.18-24.08.pth
BLEU = 5.17, 28.8/8.9/3.1/0.9 (BP=1.000, ratio=1.045, hyp_len=12778, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.19.3.17-23.80.3.14-23.01.pth
BLEU = 5.18, 27.5/8.8/3.1/1.0 (BP=1.000, ratio=1.108, hyp_len=13549, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.20.3.14-23.20.3.10-22.16.pth
BLEU = 5.46, 27.9/9.1/3.2/1.1 (BP=1.000, ratio=1.121, hyp_len=13710, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.21.3.14-23.07.3.07-21.47.pth
BLEU = 5.70, 29.3/9.5/3.4/1.1 (BP=1.000, ratio=1.046, hyp_len=12795, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.22.3.08-21.78.3.03-20.67.pth
BLEU = 5.74, 28.0/9.3/3.5/1.2 (BP=1.000, ratio=1.111, hyp_len=13584, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.23.3.09-21.97.3.00-20.12.pth
BLEU = 6.17, 29.0/9.9/3.7/1.4 (BP=1.000, ratio=1.125, hyp_len=13759, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.24.3.06-21.23.2.97-19.51.pth
BLEU = 5.74, 27.6/9.5/3.4/1.2 (BP=1.000, ratio=1.230, hyp_len=15047, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.25.3.01-20.37.2.94-19.01.pth
BLEU = 6.48, 30.8/10.7/4.0/1.4 (BP=1.000, ratio=1.071, hyp_len=13105, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.26.3.01-20.21.2.91-18.38.pth
BLEU = 6.45, 29.6/10.3/3.9/1.4 (BP=1.000, ratio=1.151, hyp_len=14082, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.27.2.93-18.81.2.88-17.86.pth
BLEU = 7.58, 34.0/12.5/4.6/1.7 (BP=1.000, ratio=1.004, hyp_len=12283, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.28.2.95-19.17.2.86-17.41.pth
BLEU = 7.00, 31.8/11.6/4.3/1.5 (BP=1.000, ratio=1.104, hyp_len=13509, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.29.2.96-19.34.2.84-17.14.pth
BLEU = 7.76, 32.7/11.9/4.8/2.0 (BP=1.000, ratio=1.071, hyp_len=13104, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.30.2.92-18.52.2.82-16.76.pth
BLEU = 7.83, 32.8/12.3/4.9/1.9 (BP=1.000, ratio=1.099, hyp_len=13446, ref_len=12231)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/baseline/transformer/bkmy-40epoch
Evaluation result for the model: transformer-model-bkmy.01.5.94-380.54.5.83-341.04.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 11.5/0.0/0.0/0.0 (BP=0.007, ratio=0.170, hyp_len=2074, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.02.5.36-212.16.5.29-198.67.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 8.1/0.0/0.0/0.0 (BP=0.039, ratio=0.236, hyp_len=2884, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.03.4.90-133.94.4.81-122.94.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 24.7/0.0/0.0/0.0 (BP=0.013, ratio=0.188, hyp_len=2301, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.04.4.56-95.72.4.52-91.79.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 51.4/0.3/0.0/0.0 (BP=0.054, ratio=0.255, hyp_len=3119, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.05.4.36-78.42.4.32-74.82.pth
BLEU = 0.90, 35.2/3.8/0.7/0.1 (BP=0.522, ratio=0.606, hyp_len=7412, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.06.4.16-63.96.4.14-63.07.pth
BLEU = 1.09, 24.7/3.6/0.5/0.1 (BP=0.870, ratio=0.878, hyp_len=10736, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.07.4.00-54.45.4.01-55.01.pth
BLEU = 1.22, 22.7/4.5/0.5/0.0 (BP=0.979, ratio=0.979, hyp_len=11972, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.08.3.89-49.13.3.88-48.65.pth
BLEU = 1.08, 20.1/3.6/0.5/0.0 (BP=1.000, ratio=1.053, hyp_len=12883, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.09.3.80-44.54.3.77-43.42.pth
BLEU = 1.57, 22.5/4.2/0.7/0.1 (BP=0.954, ratio=0.955, hyp_len=11681, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.10.3.72-41.21.3.67-39.36.pth
BLEU = 2.88, 27.1/6.4/1.7/0.5 (BP=0.831, ratio=0.843, hyp_len=10316, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.11.3.62-37.31.3.59-36.12.pth
BLEU = 3.87, 31.6/8.3/2.6/0.8 (BP=0.807, ratio=0.824, hyp_len=10074, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.12.3.52-33.93.3.51-33.59.pth
BLEU = 3.66, 32.3/8.4/2.6/0.6 (BP=0.792, ratio=0.811, hyp_len=9922, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.13.3.45-31.47.3.45-31.52.pth
BLEU = 3.29, 32.8/8.5/2.2/0.6 (BP=0.763, ratio=0.787, hyp_len=9631, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.14.3.40-29.90.3.39-29.57.pth
BLEU = 4.17, 33.7/9.7/3.0/0.9 (BP=0.755, ratio=0.781, hyp_len=9550, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.15.3.31-27.35.3.34-28.14.pth
BLEU = 4.73, 33.0/10.0/3.3/1.1 (BP=0.806, ratio=0.822, hyp_len=10057, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.16.3.30-27.19.3.29-26.72.pth
BLEU = 5.17, 33.9/10.8/3.6/1.3 (BP=0.804, ratio=0.821, hyp_len=10042, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.17.3.23-25.38.3.24-25.61.pth
BLEU = 5.70, 33.8/11.4/4.1/1.4 (BP=0.826, ratio=0.839, hyp_len=10263, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.18.3.19-24.19.3.20-24.65.pth
BLEU = 5.98, 32.5/11.3/4.1/1.3 (BP=0.896, ratio=0.901, hyp_len=11024, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.19.3.18-23.95.3.17-23.70.pth
BLEU = 6.27, 30.9/10.8/3.9/1.2 (BP=0.992, ratio=0.992, hyp_len=12133, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.20.3.13-22.87.3.14-22.99.pth
BLEU = 6.50, 34.1/12.2/4.5/1.4 (BP=0.905, ratio=0.909, hyp_len=11116, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.21.3.05-21.20.3.10-22.10.pth
BLEU = 6.49, 31.0/11.0/4.0/1.3 (BP=1.000, ratio=1.006, hyp_len=12299, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.22.3.08-21.67.3.07-21.54.pth
BLEU = 6.93, 31.4/11.3/4.3/1.5 (BP=1.000, ratio=1.025, hyp_len=12533, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.23.3.08-21.83.3.04-20.86.pth
BLEU = 5.63, 26.6/9.4/3.4/1.2 (BP=1.000, ratio=1.249, hyp_len=15280, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.24.3.01-20.27.3.01-20.19.pth
BLEU = 7.41, 32.6/12.1/4.6/1.7 (BP=1.000, ratio=1.031, hyp_len=12607, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.25.3.02-20.45.2.99-19.79.pth
BLEU = 7.51, 32.7/11.9/4.6/1.8 (BP=1.000, ratio=1.027, hyp_len=12559, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.26.2.99-19.96.2.96-19.38.pth
BLEU = 7.33, 32.4/11.9/4.4/1.7 (BP=1.000, ratio=1.030, hyp_len=12596, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.27.2.95-19.16.2.93-18.74.pth
BLEU = 7.59, 32.9/12.2/4.6/1.8 (BP=1.000, ratio=1.061, hyp_len=12977, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.28.2.95-19.18.2.91-18.30.pth
BLEU = 7.81, 33.8/12.5/4.7/1.9 (BP=1.000, ratio=1.027, hyp_len=12560, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.29.2.89-18.05.2.88-17.88.pth
BLEU = 7.26, 31.1/11.7/4.4/1.7 (BP=1.000, ratio=1.142, hyp_len=13969, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.30.2.85-17.23.2.87-17.57.pth
BLEU = 7.76, 31.5/12.2/4.8/2.0 (BP=1.000, ratio=1.137, hyp_len=13908, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.31.2.96-19.29.2.85-17.28.pth
BLEU = 8.36, 35.4/13.4/5.1/2.0 (BP=1.000, ratio=1.006, hyp_len=12310, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.32.2.87-17.55.2.83-16.87.pth
BLEU = 8.69, 34.8/13.6/5.4/2.2 (BP=1.000, ratio=1.026, hyp_len=12550, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.33.2.82-16.84.2.81-16.59.pth
BLEU = 7.86, 32.6/12.6/4.8/1.9 (BP=1.000, ratio=1.113, hyp_len=13615, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.34.2.83-16.92.2.79-16.20.pth
BLEU = 8.15, 33.8/12.9/5.0/2.0 (BP=1.000, ratio=1.084, hyp_len=13255, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.35.2.80-16.42.2.77-15.98.pth
BLEU = 8.98, 37.8/14.7/5.8/2.3 (BP=0.960, ratio=0.961, hyp_len=11750, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.36.2.85-17.20.2.76-15.81.pth
BLEU = 8.69, 35.2/13.7/5.4/2.2 (BP=1.000, ratio=1.056, hyp_len=12917, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.37.2.81-16.62.2.74-15.48.pth
BLEU = 9.46, 37.8/15.0/6.0/2.6 (BP=0.977, ratio=0.978, hyp_len=11958, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.38.2.79-16.28.2.72-15.22.pth
BLEU = 9.88, 38.1/15.2/6.3/2.6 (BP=0.999, ratio=0.999, hyp_len=12215, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.39.2.74-15.41.2.72-15.13.pth
BLEU = 9.48, 36.8/14.6/5.8/2.6 (BP=1.000, ratio=1.033, hyp_len=12636, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.40.2.74-15.44.2.69-14.75.pth
BLEU = 9.93, 39.2/15.8/6.5/2.8 (BP=0.962, ratio=0.963, hyp_len=11780, ref_len=12231)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/baseline/transformer/bkmy-50epoch
Evaluation result for the model: transformer-model-bkmy.01.5.94-378.82.5.80-329.55.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 26.9/0.1/0.0/0.0 (BP=0.143, ratio=0.339, hyp_len=4152, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.02.5.32-203.99.5.21-183.27.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 59.8/0.0/0.0/0.0 (BP=0.009, ratio=0.174, hyp_len=2126, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.03.4.85-127.82.4.76-116.60.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 53.2/2.6/0.3/0.0 (BP=0.142, ratio=0.339, hyp_len=4148, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.04.4.55-94.89.4.46-86.48.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 58.4/0.0/0.0/0.0 (BP=0.054, ratio=0.255, hyp_len=3114, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.05.4.29-73.26.4.25-70.35.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 45.9/5.7/0.1/0.0 (BP=0.209, ratio=0.390, hyp_len=4770, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.06.4.13-62.31.4.09-59.52.pth
BLEU = 1.39, 31.2/6.5/1.1/0.1 (BP=0.651, ratio=0.700, hyp_len=8561, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.07.4.01-55.23.3.95-51.91.pth
BLEU = 2.51, 25.7/6.3/1.2/0.3 (BP=0.924, ratio=0.927, hyp_len=11339, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.08.3.84-46.69.3.82-45.75.pth
BLEU = 4.62, 27.4/8.3/2.7/0.8 (BP=0.980, ratio=0.980, hyp_len=11984, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.09.3.73-41.64.3.72-41.18.pth
BLEU = 4.43, 28.3/8.4/2.7/0.7 (BP=0.963, ratio=0.964, hyp_len=11786, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.10.3.70-40.48.3.62-37.48.pth
BLEU = 4.57, 28.8/8.8/2.9/0.8 (BP=0.920, ratio=0.923, hyp_len=11290, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.11.3.52-33.88.3.54-34.49.pth
BLEU = 4.81, 28.7/8.9/3.0/0.8 (BP=0.961, ratio=0.962, hyp_len=11766, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.12.3.52-33.87.3.46-31.90.pth
BLEU = 5.03, 29.9/9.8/3.2/1.0 (BP=0.921, ratio=0.924, hyp_len=11300, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.13.3.43-30.84.3.40-30.03.pth
BLEU = 5.67, 29.4/9.8/3.5/1.1 (BP=0.988, ratio=0.989, hyp_len=12091, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.14.3.39-29.69.3.34-28.14.pth
BLEU = 5.13, 26.4/8.6/3.1/1.0 (BP=1.000, ratio=1.122, hyp_len=13728, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.15.3.25-25.88.3.29-26.76.pth
BLEU = 5.26, 28.4/9.3/3.1/0.9 (BP=1.000, ratio=1.066, hyp_len=13040, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.16.3.31-27.26.3.24-25.59.pth
BLEU = 5.18, 26.4/8.9/3.1/1.0 (BP=1.000, ratio=1.160, hyp_len=14193, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.17.3.17-23.83.3.20-24.55.pth
BLEU = 5.29, 26.8/9.2/3.1/1.0 (BP=1.000, ratio=1.168, hyp_len=14291, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.18.3.19-24.40.3.15-23.41.pth
BLEU = 5.17, 25.8/8.9/3.2/1.0 (BP=1.000, ratio=1.259, hyp_len=15398, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.19.3.12-22.54.3.12-22.59.pth
BLEU = 5.20, 26.0/9.2/3.2/0.9 (BP=1.000, ratio=1.291, hyp_len=15793, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.20.3.11-22.32.3.08-21.79.pth
BLEU = 6.29, 30.3/11.1/3.9/1.2 (BP=1.000, ratio=1.116, hyp_len=13651, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.21.3.09-21.98.3.05-21.20.pth
BLEU = 5.36, 26.5/9.7/3.3/1.0 (BP=1.000, ratio=1.321, hyp_len=16156, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.22.3.06-21.39.3.02-20.45.pth
BLEU = 5.67, 26.8/9.9/3.5/1.1 (BP=1.000, ratio=1.316, hyp_len=16099, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.23.2.99-19.84.3.00-20.05.pth
BLEU = 6.65, 30.1/11.3/4.1/1.4 (BP=1.000, ratio=1.147, hyp_len=14032, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.24.2.98-19.66.2.97-19.48.pth
BLEU = 6.16, 28.1/10.5/3.8/1.3 (BP=1.000, ratio=1.262, hyp_len=15438, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.25.2.98-19.63.2.94-18.95.pth
BLEU = 6.39, 28.5/10.9/4.1/1.3 (BP=1.000, ratio=1.281, hyp_len=15670, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.26.2.95-19.12.2.92-18.50.pth
BLEU = 6.39, 28.9/10.7/3.9/1.4 (BP=1.000, ratio=1.241, hyp_len=15183, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.27.2.90-18.13.2.89-17.99.pth
BLEU = 6.87, 29.8/11.4/4.2/1.6 (BP=1.000, ratio=1.227, hyp_len=15009, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.28.2.89-18.08.2.87-17.61.pth
BLEU = 7.21, 30.6/11.7/4.5/1.7 (BP=1.000, ratio=1.192, hyp_len=14583, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.29.2.92-18.47.2.85-17.28.pth
BLEU = 7.97, 34.1/13.2/5.0/1.8 (BP=1.000, ratio=1.063, hyp_len=12998, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.30.2.83-16.96.2.84-17.04.pth
BLEU = 8.40, 34.2/13.6/5.3/2.0 (BP=1.000, ratio=1.095, hyp_len=13391, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.31.2.81-16.65.2.82-16.71.pth
BLEU = 7.71, 32.4/12.7/4.8/1.8 (BP=1.000, ratio=1.167, hyp_len=14268, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.32.2.83-16.89.2.79-16.35.pth
BLEU = 7.66, 30.9/12.4/4.8/1.9 (BP=1.000, ratio=1.258, hyp_len=15390, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.33.2.78-16.16.2.77-15.96.pth
BLEU = 8.64, 35.2/14.1/5.6/2.0 (BP=1.000, ratio=1.104, hyp_len=13499, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.34.2.81-16.61.2.76-15.74.pth
BLEU = 9.14, 35.4/14.5/5.8/2.3 (BP=1.000, ratio=1.097, hyp_len=13419, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.35.2.81-16.68.2.73-15.40.pth
BLEU = 8.89, 34.7/14.2/5.7/2.2 (BP=1.000, ratio=1.135, hyp_len=13882, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.36.2.77-15.88.2.72-15.20.pth
BLEU = 9.04, 34.8/14.4/5.8/2.3 (BP=1.000, ratio=1.128, hyp_len=13802, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.37.2.74-15.55.2.71-14.99.pth
BLEU = 9.11, 35.0/14.4/5.8/2.3 (BP=1.000, ratio=1.143, hyp_len=13981, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.38.2.76-15.74.2.69-14.76.pth
BLEU = 10.23, 38.5/16.0/6.5/2.7 (BP=1.000, ratio=1.024, hyp_len=12530, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.39.2.72-15.15.2.68-14.62.pth
BLEU = 9.93, 36.1/15.3/6.4/2.7 (BP=1.000, ratio=1.120, hyp_len=13700, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.40.2.72-15.24.2.67-14.43.pth
BLEU = 10.09, 37.7/15.7/6.4/2.7 (BP=1.000, ratio=1.041, hyp_len=12729, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.41.2.67-14.42.2.66-14.26.pth
BLEU = 10.41, 37.4/16.0/6.9/2.9 (BP=1.000, ratio=1.092, hyp_len=13356, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.42.2.69-14.78.2.64-14.03.pth
BLEU = 10.13, 37.8/15.9/6.5/2.7 (BP=1.000, ratio=1.058, hyp_len=12937, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.43.2.66-14.31.2.63-13.85.pth
BLEU = 11.20, 40.3/17.3/7.3/3.1 (BP=0.998, ratio=0.998, hyp_len=12209, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.44.2.68-14.53.2.63-13.82.pth
BLEU = 11.35, 40.7/17.5/7.4/3.2 (BP=0.997, ratio=0.997, hyp_len=12198, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.45.2.63-13.86.2.60-13.50.pth
BLEU = 11.38, 40.3/17.4/7.4/3.2 (BP=1.000, ratio=1.011, hyp_len=12367, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.46.2.63-13.92.2.60-13.45.pth
BLEU = 10.62, 38.4/16.4/6.9/2.9 (BP=1.000, ratio=1.068, hyp_len=13063, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.47.2.66-14.37.2.59-13.35.pth
BLEU = 12.05, 41.5/18.2/8.0/3.5 (BP=1.000, ratio=1.000, hyp_len=12230, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.48.2.61-13.63.2.58-13.18.pth
BLEU = 11.66, 42.2/18.3/8.0/3.5 (BP=0.962, ratio=0.962, hyp_len=11771, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.49.2.64-13.95.2.57-13.10.pth
BLEU = 12.06, 41.4/18.0/8.1/3.6 (BP=0.992, ratio=0.992, hyp_len=12135, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.50.2.62-13.68.2.57-13.01.pth
BLEU = 11.68, 41.8/18.0/7.8/3.4 (BP=0.981, ratio=0.981, hyp_len=11995, ref_len=12231)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/baseline/transformer/bkmy-60epoch
Evaluation result for the model: transformer-model-bkmy.01.5.96-386.57.5.83-340.63.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 25.5/0.0/0.0/0.0 (BP=0.140, ratio=0.337, hyp_len=4122, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.02.5.34-208.54.5.23-187.35.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 44.5/0.0/0.0/0.0 (BP=0.053, ratio=0.254, hyp_len=3111, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.03.4.90-134.08.4.79-120.86.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 54.4/5.3/1.4/0.0 (BP=0.142, ratio=0.339, hyp_len=4148, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.04.4.56-95.25.4.51-91.34.pth
BLEU = 0.72, 45.3/5.4/1.3/0.2 (BP=0.258, ratio=0.425, hyp_len=5193, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.05.4.34-76.79.4.30-74.03.pth
BLEU = 0.95, 25.0/2.9/0.6/0.1 (BP=0.755, ratio=0.781, hyp_len=9547, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.06.4.19-66.15.4.13-62.06.pth
BLEU = 0.98, 21.8/2.7/0.5/0.0 (BP=0.907, ratio=0.911, hyp_len=11147, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.07.4.02-55.85.3.99-53.86.pth
BLEU = 1.41, 21.9/4.8/0.6/0.1 (BP=0.985, ratio=0.985, hyp_len=12045, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.08.3.84-46.63.3.84-46.72.pth
BLEU = 3.03, 25.2/6.7/1.4/0.4 (BP=0.974, ratio=0.974, hyp_len=11918, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.09.3.83-46.03.3.74-42.11.pth
BLEU = 4.14, 25.5/7.4/2.2/0.7 (BP=1.000, ratio=1.025, hyp_len=12540, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.10.3.68-39.69.3.64-38.07.pth
BLEU = 4.41, 27.7/8.1/2.5/0.7 (BP=0.982, ratio=0.982, hyp_len=12011, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.11.3.56-35.02.3.55-34.83.pth
BLEU = 4.69, 28.9/8.7/2.7/0.8 (BP=0.967, ratio=0.967, hyp_len=11832, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.12.3.48-32.49.3.48-32.32.pth
BLEU = 4.61, 26.6/8.3/2.7/0.8 (BP=1.000, ratio=1.095, hyp_len=13391, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.13.3.43-30.88.3.41-30.28.pth
BLEU = 4.11, 24.3/7.4/2.3/0.7 (BP=1.000, ratio=1.210, hyp_len=14794, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.14.3.38-29.28.3.35-28.54.pth
BLEU = 3.51, 21.1/6.4/2.0/0.6 (BP=1.000, ratio=1.410, hyp_len=17242, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.15.3.31-27.26.3.30-27.07.pth
BLEU = 3.12, 17.4/5.5/1.8/0.6 (BP=1.000, ratio=1.752, hyp_len=21425, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.16.3.28-26.51.3.25-25.68.pth
BLEU = 3.13, 18.4/5.5/1.8/0.5 (BP=1.000, ratio=1.638, hyp_len=20040, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.17.3.25-25.70.3.20-24.56.pth
BLEU = 3.76, 20.1/6.5/2.1/0.7 (BP=1.000, ratio=1.532, hyp_len=18740, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.18.3.21-24.74.3.17-23.72.pth
BLEU = 3.90, 20.9/6.8/2.2/0.7 (BP=1.000, ratio=1.511, hyp_len=18477, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.19.3.13-22.99.3.12-22.67.pth
BLEU = 4.15, 20.8/7.0/2.4/0.8 (BP=1.000, ratio=1.570, hyp_len=19206, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.20.3.10-22.11.3.09-21.99.pth
BLEU = 5.76, 28.6/9.7/3.4/1.1 (BP=1.000, ratio=1.103, hyp_len=13493, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.21.3.12-22.57.3.05-21.13.pth
BLEU = 6.34, 30.4/10.6/3.8/1.3 (BP=1.000, ratio=1.072, hyp_len=13108, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.22.3.08-21.67.3.02-20.48.pth
BLEU = 5.24, 24.7/8.8/3.1/1.1 (BP=1.000, ratio=1.368, hyp_len=16732, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.23.3.02-20.42.2.99-19.84.pth
BLEU = 5.46, 25.7/9.2/3.3/1.1 (BP=1.000, ratio=1.330, hyp_len=16271, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.24.2.97-19.51.2.96-19.30.pth
BLEU = 6.86, 30.3/11.1/4.2/1.6 (BP=1.000, ratio=1.130, hyp_len=13817, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.25.2.97-19.44.2.93-18.71.pth
BLEU = 6.30, 28.0/10.2/3.9/1.4 (BP=1.000, ratio=1.237, hyp_len=15126, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.26.2.95-19.03.2.90-18.20.pth
BLEU = 7.98, 32.9/12.4/5.0/2.0 (BP=1.000, ratio=1.069, hyp_len=13071, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.27.2.91-18.35.2.87-17.72.pth
BLEU = 6.49, 27.7/10.5/4.0/1.5 (BP=1.000, ratio=1.319, hyp_len=16138, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.28.2.99-19.97.2.85-17.22.pth
BLEU = 6.93, 29.1/10.8/4.4/1.7 (BP=1.000, ratio=1.239, hyp_len=15151, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.29.2.92-18.57.2.82-16.84.pth
BLEU = 8.17, 32.5/12.8/5.2/2.1 (BP=1.000, ratio=1.127, hyp_len=13783, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.30.2.84-17.08.2.81-16.60.pth
BLEU = 6.60, 27.0/10.3/4.1/1.7 (BP=1.000, ratio=1.381, hyp_len=16897, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.31.2.87-17.62.2.79-16.24.pth
BLEU = 7.08, 28.5/10.9/4.5/1.8 (BP=1.000, ratio=1.311, hyp_len=16035, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.32.2.85-17.31.2.76-15.84.pth
BLEU = 7.93, 30.9/12.2/5.0/2.1 (BP=1.000, ratio=1.226, hyp_len=14997, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.33.2.83-16.92.2.75-15.67.pth
BLEU = 8.82, 33.7/13.2/5.6/2.4 (BP=1.000, ratio=1.106, hyp_len=13526, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.34.2.76-15.86.2.72-15.24.pth
BLEU = 8.91, 33.3/13.6/5.7/2.4 (BP=1.000, ratio=1.140, hyp_len=13945, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.35.2.80-16.47.2.71-15.09.pth
BLEU = 8.38, 32.6/12.9/5.3/2.2 (BP=1.000, ratio=1.156, hyp_len=14144, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.36.2.76-15.72.2.69-14.70.pth
BLEU = 9.55, 34.8/14.1/6.2/2.7 (BP=1.000, ratio=1.083, hyp_len=13248, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.37.2.79-16.33.2.67-14.49.pth
BLEU = 9.40, 34.7/14.1/6.0/2.6 (BP=1.000, ratio=1.094, hyp_len=13377, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.38.2.74-15.50.2.67-14.42.pth
BLEU = 9.11, 34.0/13.8/5.9/2.5 (BP=1.000, ratio=1.126, hyp_len=13776, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.39.2.73-15.35.2.65-14.13.pth
BLEU = 9.87, 36.0/14.8/6.4/2.8 (BP=1.000, ratio=1.061, hyp_len=12980, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.40.2.81-16.55.2.63-13.91.pth
BLEU = 9.41, 33.5/14.0/6.1/2.7 (BP=1.000, ratio=1.186, hyp_len=14503, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.41.2.61-13.57.2.62-13.74.pth
BLEU = 10.40, 37.5/15.6/6.8/2.9 (BP=1.000, ratio=1.037, hyp_len=12680, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.42.2.70-14.86.2.60-13.49.pth
BLEU = 10.61, 37.3/15.8/6.9/3.1 (BP=1.000, ratio=1.050, hyp_len=12837, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.43.2.66-14.23.2.60-13.43.pth
BLEU = 10.71, 37.5/15.8/7.0/3.2 (BP=1.000, ratio=1.056, hyp_len=12912, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.44.2.63-13.87.2.58-13.15.pth
BLEU = 10.46, 37.2/15.7/6.9/3.0 (BP=1.000, ratio=1.071, hyp_len=13099, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.45.2.64-14.04.2.56-13.00.pth
BLEU = 11.44, 39.0/16.6/7.5/3.5 (BP=1.000, ratio=1.008, hyp_len=12329, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.46.2.62-13.68.2.55-12.84.pth
BLEU = 11.98, 41.5/18.2/8.3/3.7 (BP=0.972, ratio=0.973, hyp_len=11896, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.47.2.56-12.98.2.55-12.78.pth
BLEU = 10.04, 35.0/14.8/6.6/3.0 (BP=1.000, ratio=1.135, hyp_len=13879, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.48.2.63-13.84.2.53-12.61.pth
BLEU = 11.90, 39.3/17.3/8.0/3.7 (BP=1.000, ratio=1.026, hyp_len=12546, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.49.2.62-13.71.2.53-12.55.pth
BLEU = 10.50, 36.3/15.4/7.0/3.1 (BP=1.000, ratio=1.117, hyp_len=13663, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.50.2.58-13.16.2.51-12.36.pth
BLEU = 11.07, 37.7/16.2/7.4/3.3 (BP=1.000, ratio=1.097, hyp_len=13419, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.51.2.61-13.64.2.51-12.28.pth
BLEU = 12.19, 40.4/17.8/8.2/3.7 (BP=1.000, ratio=1.009, hyp_len=12340, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.52.2.55-12.78.2.50-12.13.pth
BLEU = 12.03, 39.7/17.3/8.1/3.8 (BP=1.000, ratio=1.027, hyp_len=12558, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.53.2.60-13.50.2.48-11.96.pth
BLEU = 13.04, 41.5/18.6/8.8/4.3 (BP=1.000, ratio=1.000, hyp_len=12231, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.54.2.56-12.90.2.47-11.88.pth
BLEU = 13.00, 41.4/18.6/8.8/4.3 (BP=0.997, ratio=0.997, hyp_len=12193, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.55.2.51-12.35.2.46-11.74.pth
BLEU = 12.82, 41.0/18.3/8.7/4.1 (BP=1.000, ratio=1.010, hyp_len=12357, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.56.2.52-12.43.2.46-11.66.pth
BLEU = 13.25, 42.5/19.2/9.2/4.2 (BP=0.993, ratio=0.993, hyp_len=12147, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.57.2.53-12.54.2.45-11.61.pth
BLEU = 13.50, 42.8/19.5/9.5/4.6 (BP=0.979, ratio=0.979, hyp_len=11978, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.58.2.54-12.68.2.44-11.49.pth
BLEU = 13.50, 42.7/19.5/9.4/4.4 (BP=0.991, ratio=0.991, hyp_len=12117, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.59.2.51-12.26.2.45-11.53.pth
BLEU = 13.02, 41.0/18.6/9.0/4.2 (BP=1.000, ratio=1.022, hyp_len=12502, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.60.2.55-12.79.2.43-11.34.pth
BLEU = 13.93, 43.8/20.2/9.8/4.8 (BP=0.975, ratio=0.975, hyp_len=11927, ref_len=12231)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/baseline/transformer/bkmy-70epoch
Evaluation result for the model: transformer-model-bkmy.01.5.89-360.76.5.78-322.45.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 47.3/0.0/0.0/0.0 (BP=0.053, ratio=0.254, hyp_len=3111, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.02.5.31-201.96.5.22-185.40.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 46.3/0.0/0.0/0.0 (BP=0.142, ratio=0.339, hyp_len=4148, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.03.4.86-128.44.4.76-117.12.pth
BLEU = 0.00, 51.8/1.3/0.3/0.0 (BP=0.053, ratio=0.254, hyp_len=3111, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.04.4.58-97.34.4.48-88.41.pth
BLEU = 0.62, 26.7/5.5/1.3/0.2 (BP=0.256, ratio=0.423, hyp_len=5174, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.05.4.36-78.03.4.28-71.95.pth
BLEU = 0.74, 22.0/4.1/0.9/0.1 (BP=0.431, ratio=0.543, hyp_len=6641, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.06.4.16-64.32.4.10-60.56.pth
BLEU = 1.10, 25.7/3.4/0.7/0.2 (BP=0.625, ratio=0.680, hyp_len=8319, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.07.4.01-55.07.3.97-52.84.pth
BLEU = 3.03, 28.1/6.5/1.9/0.6 (BP=0.812, ratio=0.828, hyp_len=10126, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.08.3.87-47.99.3.83-46.12.pth
BLEU = 3.46, 30.2/7.6/2.2/0.6 (BP=0.811, ratio=0.827, hyp_len=10111, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.09.3.79-44.27.3.73-41.60.pth
BLEU = 4.40, 31.2/9.0/3.0/0.9 (BP=0.849, ratio=0.859, hyp_len=10510, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.10.3.68-39.70.3.64-37.97.pth
BLEU = 3.51, 24.5/6.4/2.0/0.5 (BP=1.000, ratio=1.028, hyp_len=12577, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.11.3.57-35.63.3.55-34.68.pth
BLEU = 4.23, 26.1/7.5/2.6/0.6 (BP=1.000, ratio=1.004, hyp_len=12281, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.12.3.48-32.61.3.48-32.36.pth
BLEU = 4.53, 27.2/8.0/2.7/0.8 (BP=0.979, ratio=0.980, hyp_len=11981, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.13.3.44-31.05.3.42-30.47.pth
BLEU = 4.62, 27.9/8.5/2.8/0.7 (BP=0.979, ratio=0.979, hyp_len=11973, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.14.3.35-28.37.3.36-28.88.pth
BLEU = 4.38, 26.6/7.9/2.6/0.7 (BP=1.000, ratio=1.039, hyp_len=12705, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.15.3.35-28.51.3.32-27.57.pth
BLEU = 4.16, 24.8/7.4/2.4/0.7 (BP=1.000, ratio=1.126, hyp_len=13773, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.16.3.24-25.59.3.27-26.29.pth
BLEU = 4.11, 24.0/7.3/2.4/0.7 (BP=1.000, ratio=1.180, hyp_len=14437, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.17.3.21-24.81.3.23-25.36.pth
BLEU = 4.59, 27.4/8.2/2.6/0.7 (BP=1.000, ratio=1.059, hyp_len=12951, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.18.3.22-24.99.3.19-24.35.pth
BLEU = 4.77, 29.4/9.4/2.8/0.7 (BP=1.000, ratio=1.036, hyp_len=12677, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.19.3.22-24.92.3.15-23.42.pth
BLEU = 4.45, 27.1/8.7/2.6/0.6 (BP=1.000, ratio=1.160, hyp_len=14191, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.20.3.13-22.98.3.12-22.71.pth
BLEU = 5.16, 29.9/9.8/3.1/0.8 (BP=1.000, ratio=1.050, hyp_len=12845, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.21.3.13-22.92.3.09-22.00.pth
BLEU = 5.10, 29.1/9.6/3.0/0.8 (BP=1.000, ratio=1.081, hyp_len=13224, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.22.3.11-22.35.3.06-21.29.pth
BLEU = 5.54, 30.3/10.3/3.3/0.9 (BP=1.000, ratio=1.069, hyp_len=13081, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.23.3.08-21.76.3.03-20.75.pth
BLEU = 5.60, 30.9/10.4/3.4/0.9 (BP=1.000, ratio=1.050, hyp_len=12846, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.24.3.03-20.62.3.00-20.18.pth
BLEU = 4.82, 26.9/9.0/2.9/0.8 (BP=1.000, ratio=1.242, hyp_len=15196, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.25.2.93-18.74.2.97-19.55.pth
BLEU = 6.05, 29.6/10.3/3.6/1.2 (BP=1.000, ratio=1.139, hyp_len=13933, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.26.2.96-19.39.2.95-19.16.pth
BLEU = 5.01, 25.9/8.7/3.0/0.9 (BP=1.000, ratio=1.323, hyp_len=16178, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.27.2.98-19.62.2.92-18.59.pth
BLEU = 6.27, 29.6/10.5/3.7/1.3 (BP=1.000, ratio=1.151, hyp_len=14083, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.28.2.92-18.63.2.90-18.23.pth
BLEU = 5.87, 30.3/10.7/3.6/1.0 (BP=1.000, ratio=1.119, hyp_len=13692, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.29.2.95-19.05.2.89-17.97.pth
BLEU = 5.95, 29.6/10.3/3.5/1.2 (BP=1.000, ratio=1.140, hyp_len=13939, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.30.2.85-17.27.2.86-17.44.pth
BLEU = 7.42, 33.2/12.2/4.5/1.7 (BP=1.000, ratio=1.037, hyp_len=12679, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.31.2.89-18.04.2.85-17.24.pth
BLEU = 6.95, 31.4/11.6/4.3/1.5 (BP=1.000, ratio=1.108, hyp_len=13546, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.32.2.92-18.49.2.81-16.64.pth
BLEU = 7.12, 31.8/11.7/4.3/1.6 (BP=1.000, ratio=1.119, hyp_len=13684, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.33.2.85-17.37.2.80-16.42.pth
BLEU = 7.38, 32.9/12.1/4.4/1.7 (BP=1.000, ratio=1.074, hyp_len=13133, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.34.2.81-16.68.2.78-16.15.pth
BLEU = 7.16, 30.9/11.5/4.4/1.7 (BP=1.000, ratio=1.174, hyp_len=14357, ref_len=12231)
^[Evaluation result for the model: transformer-model-bkmy.35.2.82-16.72.2.77-15.90.pth
BLEU = 6.96, 30.4/11.3/4.2/1.6 (BP=1.000, ratio=1.176, hyp_len=14382, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.36.2.79-16.20.2.75-15.58.pth
BLEU = 6.73, 27.9/10.7/4.2/1.7 (BP=1.000, ratio=1.328, hyp_len=16242, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.37.2.86-17.39.2.73-15.33.pth
BLEU = 6.74, 28.3/10.8/4.2/1.6 (BP=1.000, ratio=1.297, hyp_len=15859, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.38.2.73-15.26.2.72-15.19.pth
BLEU = 6.56, 27.2/10.4/4.0/1.6 (BP=1.000, ratio=1.361, hyp_len=16644, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.39.2.73-15.32.2.70-14.89.pth
BLEU = 9.06, 35.7/14.0/5.7/2.4 (BP=1.000, ratio=1.033, hyp_len=12634, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.40.2.79-16.26.2.69-14.79.pth
BLEU = 6.97, 27.3/10.9/4.3/1.8 (BP=1.000, ratio=1.379, hyp_len=16866, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.41.2.76-15.85.2.68-14.56.pth
BLEU = 7.97, 30.5/12.2/5.0/2.2 (BP=1.000, ratio=1.251, hyp_len=15303, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.42.2.75-15.66.2.66-14.35.pth
BLEU = 7.59, 29.2/11.6/4.8/2.0 (BP=1.000, ratio=1.300, hyp_len=15897, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.43.2.70-14.89.2.66-14.24.pth
BLEU = 7.51, 28.6/11.5/4.7/2.0 (BP=1.000, ratio=1.392, hyp_len=17023, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.44.2.69-14.68.2.64-13.99.pth
BLEU = 7.60, 29.1/11.7/4.8/2.0 (BP=1.000, ratio=1.335, hyp_len=16330, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.45.2.62-13.71.2.64-14.03.pth
BLEU = 8.28, 31.0/12.5/5.3/2.3 (BP=1.000, ratio=1.243, hyp_len=15208, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.46.2.67-14.42.2.61-13.63.pth
BLEU = 9.08, 32.8/13.5/5.9/2.6 (BP=1.000, ratio=1.198, hyp_len=14650, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.47.2.66-14.32.2.61-13.63.pth
BLEU = 8.46, 30.5/12.6/5.4/2.4 (BP=1.000, ratio=1.294, hyp_len=15826, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.48.2.62-13.70.2.60-13.42.pth
BLEU = 8.76, 32.2/13.3/5.6/2.5 (BP=1.000, ratio=1.221, hyp_len=14936, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.49.2.58-13.26.2.58-13.23.pth
BLEU = 9.32, 32.5/13.7/6.0/2.8 (BP=1.000, ratio=1.231, hyp_len=15056, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.50.2.64-13.95.2.57-13.01.pth
BLEU = 11.32, 39.1/16.8/7.4/3.4 (BP=1.000, ratio=1.016, hyp_len=12432, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.51.2.65-14.13.2.56-12.92.pth
BLEU = 11.79, 39.5/17.2/7.7/3.7 (BP=1.000, ratio=1.014, hyp_len=12400, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.52.2.60-13.52.2.55-12.81.pth
BLEU = 10.45, 35.4/15.3/6.9/3.2 (BP=1.000, ratio=1.149, hyp_len=14054, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.53.2.63-13.94.2.55-12.86.pth
BLEU = 9.38, 32.2/13.8/6.1/2.9 (BP=1.000, ratio=1.269, hyp_len=15517, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.54.2.61-13.58.2.54-12.65.pth
BLEU = 11.52, 38.1/16.6/7.6/3.7 (BP=1.000, ratio=1.065, hyp_len=13027, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.55.2.58-13.24.2.52-12.46.pth
BLEU = 11.24, 36.6/16.1/7.4/3.7 (BP=1.000, ratio=1.121, hyp_len=13713, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.56.2.65-14.09.2.51-12.36.pth
BLEU = 12.13, 39.5/17.6/8.0/3.9 (BP=1.000, ratio=1.043, hyp_len=12752, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.57.2.54-12.71.2.51-12.29.pth
BLEU = 12.08, 38.8/17.1/7.9/4.0 (BP=1.000, ratio=1.042, hyp_len=12739, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.58.2.55-12.84.2.51-12.27.pth
BLEU = 12.47, 39.7/17.7/8.3/4.1 (BP=1.000, ratio=1.026, hyp_len=12546, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.59.2.54-12.74.2.50-12.12.pth
BLEU = 11.73, 38.1/17.0/7.8/3.8 (BP=1.000, ratio=1.080, hyp_len=13209, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.60.2.53-12.52.2.48-11.91.pth
BLEU = 12.54, 40.1/17.9/8.3/4.1 (BP=1.000, ratio=1.024, hyp_len=12525, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.61.2.51-12.36.2.47-11.88.pth
BLEU = 12.97, 41.0/18.7/8.7/4.2 (BP=1.000, ratio=1.033, hyp_len=12639, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.62.2.51-12.35.2.47-11.86.pth
BLEU = 12.76, 39.8/18.1/8.5/4.3 (BP=1.000, ratio=1.059, hyp_len=12949, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.63.2.51-12.31.2.46-11.72.pth
BLEU = 12.95, 40.2/18.4/8.7/4.4 (BP=1.000, ratio=1.036, hyp_len=12673, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.64.2.46-11.69.2.46-11.75.pth
BLEU = 12.58, 39.1/17.6/8.4/4.3 (BP=1.000, ratio=1.069, hyp_len=13071, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.65.2.51-12.31.2.46-11.67.pth
BLEU = 13.13, 40.6/18.5/8.8/4.5 (BP=1.000, ratio=1.033, hyp_len=12635, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.66.2.47-11.86.2.44-11.46.pth
BLEU = 13.63, 41.3/19.0/9.2/4.8 (BP=1.000, ratio=1.019, hyp_len=12466, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.67.2.54-12.67.2.43-11.42.pth
BLEU = 13.47, 40.9/18.8/9.1/4.7 (BP=1.000, ratio=1.037, hyp_len=12680, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.68.2.51-12.28.2.43-11.36.pth
BLEU = 13.51, 40.2/18.9/9.2/4.8 (BP=1.000, ratio=1.070, hyp_len=13090, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.69.2.47-11.77.2.43-11.32.pth
BLEU = 14.10, 42.1/19.7/9.6/5.0 (BP=1.000, ratio=1.016, hyp_len=12431, ref_len=12231)
Evaluation result for the model: transformer-model-bkmy.70.2.49-12.04.2.42-11.23.pth
BLEU = 13.33, 40.7/18.9/9.1/4.5 (BP=1.000, ratio=1.056, hyp_len=12917, ref_len=12231)
/home/ye/exp/simple-nmt
==========

real	162m39.874s
user	155m39.836s
sys	9m48.317s
(simple-nmt) ye@:~/exp/simple-nmt$
```

my-bk နဲ့ bk-my အတွက် Transformer Baseline Best model တွေနဲ့ Best Score ရလဒ်တွေက အောက်ပါအတိုင်း...  

**for Myanmar-Beik**

<div align="center"> 
    
Table 1. Best model and best score for each transformer baseline training of my-bk pair  
| No of Epoch for Training | Best Model Epoch | Model File | Best BLEU |
|-----------:|-----------:|:-----------:|-----------:|
| 30 | 27 | transformer-model-mybk.27.3.26-26.15.3.05-21.16.pth | 4.82 |
| 40 | 40 | transformer-model-mybk.40.3.05-21.02.2.83-16.96.pth | 8.23 |
| 50 | 49 | transformer-model-mybk.49.2.98-19.78.2.74-15.51.pth | 8.54 |
| 60 | 57 | transformer-model-mybk.57.2.88-17.78.2.69-14.69.pth | 10.18 |
| 70 | 69 | transformer-model-mybk.69.2.77-16.02.2.57-13.02.pth | 11.68 |

</div>  

**for Beik-Myanmar**

<div align="center"> 
    
Table 2. Best model and best score for each transformer baseline training of bk-my pair 
| No of Epoch for Training | Best Model Epoch | Model File | Best BLEU |
|-----------:|-----------:|:-----------:|-----------:|
| 30 | 30 | transformer-model-bkmy.30.2.92-18.52.2.82-16.76.pth | 7.83 |
| 40 | 40 | transformer-model-bkmy.40.2.74-15.44.2.69-14.75.pth | 9.93 |
| 50 | 49 | transformer-model-bkmy.49.2.64-13.95.2.57-13.10.pth | 12.06 |
| 60 | 60 | transformer-model-bkmy.60.2.55-12.79.2.43-11.34.pth | 13.93 |
| 70 | 69 | transformer-model-bkmy.69.2.47-11.77.2.43-11.32.pth | 14.10 |

</div> 

## Transformer-RL (my-bk, bk-my)

သုံးခဲ့တဲ့ bash script က အောက်ပါအတိုင်း...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Last updated: 5 April 2022
# a part of Transformer-Reinforcement Learning exp for Myanmar-Beik, Beik-Myanmar
# this script is for CONTINUE-training or RL training

echo "mybk, transformer-RL training start for 30 epochs...";
time python continue_train.py --load_fn ./model/rl2/baseline/transformer/mybk-30epoch/transformer-model-mybk.27.3.26-26.15.3.05-21.16.pth --model_fn ./model/rl2/rl/transformer/mybk-30epoch/transformer-rl-mybk.pth --init_epoch 28 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/transformer/mybk-30epoch/con-train.log;

echo "mybk, transformer-RL training start for 40 epochs...";
time python continue_train.py --load_fn ./model/rl2/baseline/transformer/mybk-40epoch/transformer-model-mybk.40.3.05-21.02.2.83-16.96.pth --model_fn ./model/rl2/rl/transformer/mybk-40epoch/transformer-rl-mybk.pth --init_epoch 41 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/transformer/mybk-40epoch/con-train.log;

echo "mybk, transformer-RL training start for 50 epochs...";
time python continue_train.py --load_fn ./model/rl2/baseline/transformer/mybk-50epoch/transformer-model-mybk.49.2.98-19.78.2.74-15.51.pth --model_fn ./model/rl2/rl/transformer/mybk-50epoch/transformer-rl-mybk.pth --init_epoch 50 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/transformer/mybk-50epoch/con-train.log;

echo "mybk, transformer-RL training start for 60 epochs...";
time python continue_train.py --load_fn ./model/rl2/baseline/transformer/mybk-60epoch/transformer-model-mybk.57.2.88-17.78.2.69-14.69.pth --model_fn ./model/rl2/rl/transformer/mybk-60epoch/transformer-rl-mybk.pth --init_epoch 58 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/transformer/mybk-60epoch/con-train.log;

echo "mybk, transformer-RL training start for 70 epochs...";
time python continue_train.py --load_fn ./model/rl2/baseline/transformer/mybk-70epoch/transformer-model-mybk.69.2.77-16.02.2.57-13.02.pth --model_fn ./model/rl2/rl/transformer/mybk-70epoch/transformer-rl-mybk.pth --init_epoch 70 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/transformer/mybk-70epoch/con-train.log;

echo "####################";

echo "bkmy, transformer-RL training start for 30 epochs...";
time python continue_train.py --load_fn ./model/rl2/baseline/transformer/bkmy-30epoch/transformer-model-bkmy.30.2.92-18.52.2.82-16.76.pth --model_fn ./model/rl2/rl/transformer/bkmy-30epoch/transformer-rl-bkmy.pth --init_epoch 31 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/transformer/bkmy-30epoch/con-train.log;

echo "bkmy, transformer-RL training start for 40 epochs...";
time python continue_train.py --load_fn ./model/rl2/baseline/transformer/bkmy-40epoch/transformer-model-bkmy.40.2.74-15.44.2.69-14.75.pth --model_fn ./model/rl2/rl/transformer/bkmy-40epoch/transformer-rl-bkmy.pth --init_epoch 41 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/transformer/bkmy-40epoch/con-train.log;

echo "bkmy, transformer-RL training start for 50 epochs...";
time python continue_train.py --load_fn ./model/rl2/baseline/transformer/bkmy-50epoch/transformer-model-bkmy.49.2.64-13.95.2.57-13.10.pth --model_fn ./model/rl2/rl/transformer/bkmy-50epoch/transformer-rl-bkmy.pth --init_epoch 50 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/transformer/bkmy-50epoch/con-train.log;

echo "bkmy, transformer-RL training start for 60 epochs...";
time python continue_train.py --load_fn ./model/rl2/baseline/transformer/bkmy-60epoch/transformer-model-bkmy.60.2.55-12.79.2.43-11.34.pth --model_fn ./model/rl2/rl/transformer/bkmy-60epoch/transformer-rl-bkmy.pth --init_epoch 61 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/transformer/bkmy-60epoch/con-train.log;

echo "bkmy, transformer-RL training start for 70 epochs...";
time python continue_train.py --load_fn ./model/rl2/baseline/transformer/bkmy-70epoch/transformer-model-bkmy.69.2.47-11.77.2.43-11.32.pth --model_fn ./model/rl2/rl/transformer/bkmy-70epoch/transformer-rl-bkmy.pth --init_epoch 70 --iteration_per_update 32 --max_grad_norm 1e+8 --n_epochs 100 | tee ./model/rl2/rl/transformer/bkmy-70epoch/con-train.log;


```

### Training 

Training log တစ်ခုလုံးက [RL-exp-for-mybk-screen-output.md](https://github.com/ye-kyaw-thu/error-overflow/blob/master/RL-exp-for-mybk-screen-output.md) မှာ ကြည့်ပါ။   
training ...   

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./rl-transformer-con-train.sh | tee ./rl-transformer-con-train.log
...
...
...
Epoch 90 - |param|=3.09e+02 |g_param|=2.20e+05 loss=2.3254e+00 ppl=10.23                                                
Validation - loss=2.3168e+00 ppl=10.14 best_loss=2.3225e+00 best_ppl=10.20                                              
Epoch 91 - |param|=3.09e+02 |g_param|=2.22e+05 loss=2.3305e+00 ppl=10.28                                                
Validation - loss=2.3068e+00 ppl=10.04 best_loss=2.3168e+00 best_ppl=10.14                                              
Epoch 92 - |param|=3.10e+02 |g_param|=2.06e+05 loss=2.3486e+00 ppl=10.47                                                
Validation - loss=2.2967e+00 ppl=9.94 best_loss=2.3068e+00 best_ppl=10.04                                               
Epoch 93 - |param|=3.10e+02 |g_param|=2.19e+05 loss=2.3533e+00 ppl=10.52                                                
Validation - loss=2.2953e+00 ppl=9.93 best_loss=2.2967e+00 best_ppl=9.94                                                
Epoch 94 - |param|=3.10e+02 |g_param|=2.17e+05 loss=2.3371e+00 ppl=10.35                                                
Validation - loss=2.2895e+00 ppl=9.87 best_loss=2.2953e+00 best_ppl=9.93                                                
Epoch 95 - |param|=3.10e+02 |g_param|=2.17e+05 loss=2.3151e+00 ppl=10.13                                                
Validation - loss=2.2898e+00 ppl=9.87 best_loss=2.2895e+00 best_ppl=9.87                                                
Epoch 96 - |param|=3.10e+02 |g_param|=2.33e+05 loss=2.2814e+00 ppl=9.79                                                 
Validation - loss=2.2808e+00 ppl=9.78 best_loss=2.2895e+00 best_ppl=9.87                                                
Epoch 97 - |param|=3.10e+02 |g_param|=2.23e+05 loss=2.3064e+00 ppl=10.04                                                
Validation - loss=2.2784e+00 ppl=9.76 best_loss=2.2808e+00 best_ppl=9.78                                                
Epoch 98 - |param|=3.10e+02 |g_param|=2.53e+05 loss=2.2905e+00 ppl=9.88                                                 
Validation - loss=2.2747e+00 ppl=9.73 best_loss=2.2784e+00 best_ppl=9.76                                                
Epoch 99 - |param|=3.10e+02 |g_param|=2.29e+05 loss=2.3001e+00 ppl=9.98                                                 
Validation - loss=2.2718e+00 ppl=9.70 best_loss=2.2747e+00 best_ppl=9.73                                                
Epoch 100 - |param|=3.10e+02 |g_param|=2.33e+05 loss=2.3048e+00 ppl=10.02                                               
Validation - loss=2.2640e+00 ppl=9.62 best_loss=2.2718e+00 best_ppl=9.70                                                

real	9m16.625s
user	9m13.730s
sys	0m2.644s

real	163m36.055s
user	154m50.789s
sys	2m14.647s

```

### Testing/Evaluation

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Last updated: 5 April 2022
# A part of Transformer-Reinforcement Learning exp
# this script is for testing/evaluation of baseline transformer for both Myanmar-Beik and Beik-Myanmar

# testing/evaluation transformer-RL for my-bk
for folder in {30,40,50,60,70};
do
   cd ./model/rl2/rl/transformer/mybk-${folder}epoch/;
   pwd;
   for i in *.pth; do
      MODEL=$i;

      # Testing
      python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang mybk < /home/ye/exp/simple-nmt/data/my-bk/syl/test.my > ./$MODEL.hyp

      # Evaluation with BLEU Score
      echo "Evaluation result for the model: $MODEL" | tee -a eval-results-mybk-transformer-RL-100epoch.txt;
      cat ./$MODEL.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/my-bk/syl/test.bk | tee  -a eval-results-mybk-transformer-RL-100epoch.txt;

   done
   cd -; echo "==========";
done

# testing/evaluation transformer-RL for bk-my
for folder in {30,40,50,60,70};
do
   cd ./model/rl2/rl/transformer/bkmy-${folder}epoch/;
   pwd;
   for i in *.pth; do
      MODEL=$i;

      # Testing
      python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang bkmy < /home/ye/exp/simple-nmt/data/my-bk/syl/test.bk > ./$MODEL.hyp

      # Evaluation with BLEU Score
      echo "Evaluation result for the model: $MODEL" | tee -a eval-results-bkmy-transformer-RL-100epoch.txt;
      cat ./$MODEL.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/my-bk/syl/test.my | tee  -a eval-results-bkmy-transformer-RL-100epoch.txt;

   done
   cd -; echo "==========";
done

```

testing/evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-rl2-transformer-RL-mybk-bkmy.sh | tee test-eval-rl2-transformer-RL-mybk-bkmy.log
/home/ye/exp/simple-nmt/model/rl2/rl/transformer/mybk-30epoch
Evaluation result for the model: transformer-rl-mybk.100.2.56-12.97.2.39-10.93.pth
BLEU = 15.32, 41.9/20.1/10.8/6.1 (BP=1.000, ratio=1.043, hyp_len=11929, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.28.3.25-25.81.3.03-20.62.pth
BLEU = 4.96, 20.7/7.1/3.0/1.4 (BP=1.000, ratio=1.386, hyp_len=15848, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.29.3.21-24.67.3.00-20.14.pth
BLEU = 4.54, 18.7/6.5/2.8/1.3 (BP=1.000, ratio=1.564, hyp_len=17884, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.30.3.21-24.85.2.98-19.59.pth
BLEU = 4.78, 19.7/7.0/2.9/1.3 (BP=1.000, ratio=1.573, hyp_len=17983, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.31.3.14-23.21.2.96-19.21.pth
BLEU = 4.87, 20.1/7.1/3.0/1.3 (BP=1.000, ratio=1.470, hyp_len=16805, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.32.3.19-24.37.2.94-18.83.pth
BLEU = 5.79, 22.5/8.2/3.6/1.7 (BP=1.000, ratio=1.347, hyp_len=15403, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.33.3.13-22.80.2.92-18.50.pth
BLEU = 5.49, 22.0/7.9/3.4/1.5 (BP=1.000, ratio=1.387, hyp_len=15858, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.34.3.13-22.86.2.90-18.21.pth
BLEU = 5.64, 22.0/8.0/3.5/1.6 (BP=1.000, ratio=1.417, hyp_len=16196, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.35.3.06-21.43.2.88-17.81.pth
BLEU = 5.77, 22.7/8.3/3.6/1.6 (BP=1.000, ratio=1.373, hyp_len=15700, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.36.3.14-23.13.2.86-17.41.pth
BLEU = 7.02, 26.8/10.1/4.4/2.0 (BP=1.000, ratio=1.174, hyp_len=13421, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.37.3.08-21.73.2.85-17.30.pth
BLEU = 5.75, 22.6/8.3/3.6/1.6 (BP=1.000, ratio=1.429, hyp_len=16334, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.38.3.05-21.21.2.84-17.03.pth
BLEU = 4.92, 19.1/7.1/3.2/1.4 (BP=1.000, ratio=1.656, hyp_len=18936, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.39.3.01-20.27.2.82-16.79.pth
BLEU = 6.12, 23.3/8.8/3.9/1.7 (BP=1.000, ratio=1.412, hyp_len=16138, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.40.2.99-19.94.2.80-16.46.pth
BLEU = 6.07, 23.1/8.8/3.9/1.7 (BP=1.000, ratio=1.386, hyp_len=15849, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.41.3.03-20.78.2.79-16.23.pth
BLEU = 7.75, 28.3/10.9/5.0/2.4 (BP=1.000, ratio=1.144, hyp_len=13080, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.42.3.01-20.36.2.78-16.05.pth
BLEU = 5.46, 20.8/7.8/3.5/1.6 (BP=1.000, ratio=1.590, hyp_len=18178, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.43.3.00-20.00.2.76-15.81.pth
BLEU = 7.26, 26.4/10.4/4.7/2.1 (BP=1.000, ratio=1.291, hyp_len=14760, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.44.2.94-19.01.2.75-15.65.pth
BLEU = 8.02, 29.0/11.3/5.3/2.4 (BP=1.000, ratio=1.156, hyp_len=13216, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.45.2.96-19.21.2.73-15.41.pth
BLEU = 7.40, 27.0/10.5/4.9/2.2 (BP=1.000, ratio=1.274, hyp_len=14566, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.46.2.95-19.10.2.72-15.25.pth
BLEU = 7.70, 27.8/11.0/5.1/2.2 (BP=1.000, ratio=1.250, hyp_len=14295, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.47.2.98-19.63.2.71-15.00.pth
BLEU = 7.73, 27.0/10.7/5.1/2.4 (BP=1.000, ratio=1.285, hyp_len=14689, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.48.2.94-18.92.2.70-14.91.pth
BLEU = 7.47, 26.6/10.5/4.9/2.3 (BP=1.000, ratio=1.326, hyp_len=15155, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.49.2.88-17.75.2.70-14.88.pth
BLEU = 7.76, 27.4/10.9/5.1/2.4 (BP=1.000, ratio=1.296, hyp_len=14812, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.50.2.89-17.93.2.69-14.66.pth
BLEU = 8.34, 28.9/11.5/5.5/2.7 (BP=1.000, ratio=1.216, hyp_len=13898, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.51.2.92-18.54.2.67-14.50.pth
BLEU = 8.74, 29.7/12.3/5.9/2.7 (BP=1.000, ratio=1.225, hyp_len=14005, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.52.2.86-17.51.2.66-14.32.pth
BLEU = 8.27, 28.8/11.5/5.5/2.6 (BP=1.000, ratio=1.242, hyp_len=14198, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.53.2.93-18.67.2.65-14.17.pth
BLEU = 9.69, 31.8/13.3/6.5/3.2 (BP=1.000, ratio=1.188, hyp_len=13581, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.54.2.82-16.81.2.64-14.05.pth
BLEU = 8.67, 29.2/11.9/5.8/2.8 (BP=1.000, ratio=1.251, hyp_len=14296, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.55.2.86-17.40.2.64-14.07.pth
BLEU = 9.64, 31.6/13.2/6.5/3.2 (BP=1.000, ratio=1.183, hyp_len=13520, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.56.2.79-16.23.2.62-13.78.pth
BLEU = 9.96, 32.6/13.9/6.8/3.2 (BP=1.000, ratio=1.184, hyp_len=13533, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.57.2.86-17.46.2.62-13.70.pth
BLEU = 9.03, 29.9/12.5/6.0/3.0 (BP=1.000, ratio=1.265, hyp_len=14456, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.58.2.77-16.04.2.62-13.69.pth
BLEU = 9.70, 31.5/13.2/6.6/3.2 (BP=1.000, ratio=1.194, hyp_len=13648, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.59.2.79-16.30.2.61-13.55.pth
BLEU = 9.37, 30.6/12.9/6.3/3.1 (BP=1.000, ratio=1.239, hyp_len=14161, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.60.2.85-17.30.2.60-13.43.pth
BLEU = 11.10, 34.5/15.1/7.6/3.8 (BP=1.000, ratio=1.124, hyp_len=12854, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.61.2.78-16.04.2.60-13.48.pth
BLEU = 9.30, 30.8/12.7/6.2/3.1 (BP=1.000, ratio=1.207, hyp_len=13799, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.62.2.85-17.28.2.58-13.24.pth
BLEU = 10.41, 32.7/13.9/7.1/3.7 (BP=1.000, ratio=1.191, hyp_len=13610, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.63.2.78-16.09.2.58-13.18.pth
BLEU = 10.56, 33.6/14.3/7.1/3.6 (BP=1.000, ratio=1.160, hyp_len=13264, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.64.2.75-15.56.2.57-13.02.pth
BLEU = 10.74, 33.7/14.5/7.3/3.7 (BP=1.000, ratio=1.148, hyp_len=13127, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.65.2.81-16.66.2.56-12.97.pth
BLEU = 10.74, 33.2/14.4/7.3/3.8 (BP=1.000, ratio=1.191, hyp_len=13616, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.66.2.77-16.03.2.56-12.90.pth
BLEU = 12.26, 36.8/16.4/8.5/4.4 (BP=1.000, ratio=1.102, hyp_len=12597, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.67.2.73-15.36.2.56-12.89.pth
BLEU = 11.30, 35.1/15.1/7.7/4.0 (BP=1.000, ratio=1.117, hyp_len=12775, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.68.2.73-15.34.2.55-12.80.pth
BLEU = 10.96, 34.0/14.7/7.5/3.9 (BP=1.000, ratio=1.154, hyp_len=13191, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.69.2.73-15.35.2.54-12.69.pth
BLEU = 11.84, 36.3/15.7/8.1/4.2 (BP=1.000, ratio=1.120, hyp_len=12806, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.70.2.77-15.96.2.54-12.69.pth
BLEU = 12.44, 37.3/16.4/8.5/4.6 (BP=1.000, ratio=1.079, hyp_len=12332, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.71.2.70-14.90.2.53-12.58.pth
BLEU = 11.81, 35.8/15.8/8.1/4.3 (BP=1.000, ratio=1.105, hyp_len=12638, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.72.2.71-15.09.2.52-12.47.pth
BLEU = 12.09, 36.3/16.1/8.4/4.3 (BP=1.000, ratio=1.126, hyp_len=12874, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.73.2.74-15.56.2.51-12.32.pth
BLEU = 12.07, 36.2/16.0/8.3/4.4 (BP=1.000, ratio=1.138, hyp_len=13009, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.74.2.66-14.28.2.51-12.36.pth
BLEU = 11.71, 35.3/15.5/8.1/4.2 (BP=1.000, ratio=1.132, hyp_len=12944, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.75.2.72-15.16.2.50-12.22.pth
BLEU = 12.84, 37.8/16.9/8.9/4.8 (BP=1.000, ratio=1.094, hyp_len=12501, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.76.2.73-15.37.2.50-12.14.pth
BLEU = 13.03, 37.7/17.1/9.0/4.9 (BP=1.000, ratio=1.104, hyp_len=12619, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.77.2.68-14.59.2.49-12.01.pth
BLEU = 13.43, 39.1/17.7/9.3/5.1 (BP=1.000, ratio=1.052, hyp_len=12030, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.78.2.60-13.47.2.49-12.10.pth
BLEU = 12.54, 36.8/16.6/8.6/4.7 (BP=1.000, ratio=1.116, hyp_len=12762, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.79.2.71-15.00.2.48-11.96.pth
BLEU = 12.84, 36.7/16.8/8.9/4.9 (BP=1.000, ratio=1.131, hyp_len=12932, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.80.2.65-14.19.2.48-11.96.pth
BLEU = 13.13, 37.6/17.2/9.1/5.0 (BP=1.000, ratio=1.100, hyp_len=12579, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.81.2.69-14.67.2.48-11.91.pth
BLEU = 13.18, 38.2/17.2/9.1/5.0 (BP=1.000, ratio=1.071, hyp_len=12247, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.82.2.58-13.18.2.47-11.81.pth
BLEU = 12.74, 36.8/16.8/8.8/4.9 (BP=1.000, ratio=1.130, hyp_len=12921, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.83.2.64-13.95.2.47-11.79.pth
BLEU = 13.56, 39.0/17.7/9.3/5.2 (BP=1.000, ratio=1.083, hyp_len=12381, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.84.2.63-13.83.2.46-11.73.pth
BLEU = 12.43, 36.6/16.4/8.6/4.6 (BP=1.000, ratio=1.124, hyp_len=12855, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.85.2.60-13.43.2.45-11.63.pth
BLEU = 14.25, 40.0/18.5/10.0/5.6 (BP=1.000, ratio=1.054, hyp_len=12052, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.86.2.62-13.76.2.45-11.60.pth
BLEU = 14.46, 40.9/18.9/10.1/5.6 (BP=1.000, ratio=1.037, hyp_len=11857, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.87.2.58-13.26.2.44-11.50.pth
BLEU = 13.84, 39.4/18.0/9.6/5.4 (BP=1.000, ratio=1.081, hyp_len=12359, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.88.2.60-13.47.2.44-11.48.pth
BLEU = 13.02, 37.7/17.1/9.0/4.9 (BP=1.000, ratio=1.137, hyp_len=12994, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.89.2.63-13.91.2.43-11.32.pth
BLEU = 14.69, 40.0/18.9/10.4/5.9 (BP=1.000, ratio=1.073, hyp_len=12262, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.90.2.66-14.26.2.43-11.33.pth
BLEU = 13.92, 39.3/18.0/9.7/5.5 (BP=1.000, ratio=1.073, hyp_len=12266, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.91.2.61-13.66.2.43-11.37.pth
BLEU = 14.57, 40.2/18.8/10.3/5.8 (BP=1.000, ratio=1.059, hyp_len=12111, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.92.2.60-13.48.2.43-11.33.pth
BLEU = 14.40, 40.3/18.7/10.1/5.6 (BP=1.000, ratio=1.062, hyp_len=12141, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.93.2.55-12.76.2.42-11.24.pth
BLEU = 13.87, 39.2/18.2/9.7/5.4 (BP=1.000, ratio=1.089, hyp_len=12455, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.94.2.54-12.73.2.41-11.15.pth
BLEU = 14.25, 39.5/18.5/10.0/5.7 (BP=1.000, ratio=1.101, hyp_len=12588, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.95.2.60-13.43.2.41-11.09.pth
BLEU = 13.88, 38.6/18.2/9.7/5.4 (BP=1.000, ratio=1.116, hyp_len=12755, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.96.2.60-13.43.2.40-11.01.pth
BLEU = 14.78, 40.9/19.4/10.4/5.7 (BP=1.000, ratio=1.080, hyp_len=12346, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.97.2.53-12.60.2.40-11.05.pth
BLEU = 14.82, 40.9/19.2/10.4/5.9 (BP=1.000, ratio=1.066, hyp_len=12182, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.98.2.52-12.43.2.39-10.93.pth
BLEU = 14.73, 40.4/19.0/10.3/6.0 (BP=1.000, ratio=1.081, hyp_len=12354, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.99.2.58-13.23.2.39-10.93.pth
BLEU = 14.26, 39.5/18.5/10.0/5.6 (BP=1.000, ratio=1.096, hyp_len=12531, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/transformer/mybk-40epoch
Evaluation result for the model: transformer-rl-mybk.100.2.54-12.68.2.39-10.92.pth
BLEU = 14.21, 39.3/18.3/10.0/5.7 (BP=1.000, ratio=1.100, hyp_len=12576, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.41.3.04-20.89.2.81-16.60.pth
BLEU = 8.76, 31.8/12.3/5.8/2.6 (BP=1.000, ratio=1.093, hyp_len=12499, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.42.2.99-19.86.2.81-16.64.pth
BLEU = 8.43, 30.9/11.8/5.4/2.5 (BP=1.000, ratio=1.089, hyp_len=12444, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.43.3.01-20.29.2.79-16.35.pth
BLEU = 7.87, 29.7/11.2/5.1/2.3 (BP=1.000, ratio=1.176, hyp_len=13449, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.44.2.98-19.75.2.77-16.01.pth
BLEU = 9.10, 32.3/12.9/6.1/2.7 (BP=1.000, ratio=1.112, hyp_len=12715, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.45.3.01-20.38.2.76-15.81.pth
BLEU = 8.24, 29.6/11.6/5.4/2.5 (BP=1.000, ratio=1.184, hyp_len=13538, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.46.2.97-19.54.2.74-15.51.pth
BLEU = 9.83, 34.0/13.7/6.5/3.1 (BP=1.000, ratio=1.066, hyp_len=12187, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.47.2.92-18.46.2.73-15.35.pth
BLEU = 8.71, 31.0/12.4/5.7/2.6 (BP=1.000, ratio=1.174, hyp_len=13426, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.48.2.93-18.82.2.72-15.18.pth
BLEU = 9.76, 34.2/13.7/6.5/3.0 (BP=1.000, ratio=1.065, hyp_len=12179, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.49.2.91-18.40.2.73-15.26.pth
BLEU = 10.05, 34.0/13.8/6.7/3.3 (BP=1.000, ratio=1.072, hyp_len=12255, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.50.2.89-17.96.2.72-15.11.pth
BLEU = 9.57, 33.5/13.4/6.3/2.9 (BP=1.000, ratio=1.085, hyp_len=12408, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.51.2.83-16.89.2.69-14.80.pth
BLEU = 10.06, 33.6/13.8/6.7/3.3 (BP=1.000, ratio=1.097, hyp_len=12544, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.52.2.88-17.83.2.69-14.67.pth
BLEU = 10.00, 33.7/13.8/6.7/3.2 (BP=1.000, ratio=1.099, hyp_len=12565, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.53.2.89-17.95.2.68-14.57.pth
BLEU = 9.97, 34.2/13.9/6.7/3.1 (BP=1.000, ratio=1.084, hyp_len=12394, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.54.2.86-17.41.2.66-14.32.pth
BLEU = 10.20, 34.2/14.1/6.9/3.3 (BP=1.000, ratio=1.106, hyp_len=12642, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.55.2.85-17.36.2.66-14.25.pth
BLEU = 8.96, 31.1/12.5/6.0/2.8 (BP=1.000, ratio=1.181, hyp_len=13498, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.56.2.85-17.28.2.64-14.00.pth
BLEU = 10.60, 34.9/14.6/7.1/3.5 (BP=1.000, ratio=1.091, hyp_len=12474, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.57.2.83-16.99.2.63-13.94.pth
BLEU = 10.85, 35.7/15.0/7.4/3.5 (BP=1.000, ratio=1.091, hyp_len=12473, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.58.2.82-16.76.2.63-13.85.pth
BLEU = 10.78, 35.4/14.7/7.3/3.5 (BP=1.000, ratio=1.088, hyp_len=12435, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.59.2.77-15.94.2.61-13.60.pth
BLEU = 11.59, 36.7/15.7/7.9/4.0 (BP=1.000, ratio=1.074, hyp_len=12281, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.60.2.82-16.82.2.61-13.59.pth
BLEU = 11.81, 36.8/15.8/8.1/4.1 (BP=1.000, ratio=1.044, hyp_len=11931, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.61.2.78-16.13.2.59-13.37.pth
BLEU = 12.22, 37.8/16.4/8.4/4.3 (BP=1.000, ratio=1.052, hyp_len=12029, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.62.2.71-15.03.2.59-13.33.pth
BLEU = 11.67, 36.9/15.6/7.9/4.1 (BP=1.000, ratio=1.066, hyp_len=12183, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.63.2.82-16.77.2.59-13.38.pth
BLEU = 11.52, 37.1/15.7/7.8/3.9 (BP=1.000, ratio=1.028, hyp_len=11755, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.64.2.76-15.73.2.58-13.20.pth
BLEU = 11.23, 35.9/15.2/7.6/3.8 (BP=1.000, ratio=1.089, hyp_len=12447, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.65.2.77-16.04.2.56-12.95.pth
BLEU = 11.26, 35.6/15.2/7.7/3.9 (BP=1.000, ratio=1.114, hyp_len=12734, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.66.2.70-14.83.2.56-12.94.pth
BLEU = 11.53, 36.3/15.6/7.9/3.9 (BP=1.000, ratio=1.104, hyp_len=12617, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.67.2.68-14.61.2.56-12.94.pth
BLEU = 11.65, 36.4/15.6/8.0/4.1 (BP=1.000, ratio=1.088, hyp_len=12434, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.68.2.73-15.31.2.55-12.77.pth
BLEU = 11.52, 36.1/15.5/7.9/4.0 (BP=1.000, ratio=1.098, hyp_len=12558, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.69.2.70-14.88.2.53-12.61.pth
BLEU = 11.88, 36.8/15.9/8.2/4.2 (BP=1.000, ratio=1.086, hyp_len=12412, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.70.2.75-15.70.2.53-12.55.pth
BLEU = 12.03, 37.3/16.0/8.2/4.3 (BP=1.000, ratio=1.064, hyp_len=12160, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.71.2.71-15.06.2.53-12.58.pth
BLEU = 11.92, 36.1/15.8/8.3/4.3 (BP=1.000, ratio=1.112, hyp_len=12718, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.72.2.72-15.22.2.52-12.43.pth
BLEU = 12.31, 37.7/16.5/8.5/4.4 (BP=1.000, ratio=1.075, hyp_len=12286, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.73.2.68-14.60.2.51-12.35.pth
BLEU = 12.98, 38.6/17.2/9.0/4.7 (BP=1.000, ratio=1.057, hyp_len=12085, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.74.2.74-15.50.2.51-12.31.pth
BLEU = 12.86, 38.3/16.8/8.9/4.8 (BP=1.000, ratio=1.067, hyp_len=12201, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.75.2.72-15.22.2.50-12.17.pth
BLEU = 12.87, 39.1/17.3/8.9/4.6 (BP=1.000, ratio=1.046, hyp_len=11959, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.76.2.67-14.45.2.49-12.07.pth
BLEU = 12.05, 36.6/16.1/8.4/4.3 (BP=1.000, ratio=1.131, hyp_len=12933, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.77.2.68-14.64.2.49-12.02.pth
BLEU = 12.41, 37.5/16.6/8.6/4.4 (BP=1.000, ratio=1.101, hyp_len=12584, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.78.2.65-14.17.2.49-12.04.pth
BLEU = 11.27, 35.3/15.2/7.7/3.9 (BP=1.000, ratio=1.148, hyp_len=13121, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.79.2.64-13.95.2.47-11.84.pth
BLEU = 13.57, 39.9/17.9/9.5/5.0 (BP=1.000, ratio=1.057, hyp_len=12082, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.80.2.59-13.32.2.47-11.81.pth
BLEU = 12.38, 37.7/16.6/8.6/4.4 (BP=1.000, ratio=1.092, hyp_len=12484, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.81.2.69-14.75.2.48-11.91.pth
BLEU = 12.92, 38.3/16.9/9.0/4.8 (BP=1.000, ratio=1.063, hyp_len=12157, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.82.2.65-14.14.2.46-11.66.pth
BLEU = 12.92, 37.3/17.0/9.1/4.8 (BP=1.000, ratio=1.129, hyp_len=12909, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.83.2.59-13.38.2.46-11.74.pth
BLEU = 12.64, 37.8/16.6/8.7/4.7 (BP=1.000, ratio=1.074, hyp_len=12274, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.84.2.66-14.34.2.46-11.68.pth
BLEU = 12.82, 37.3/16.8/8.9/4.8 (BP=1.000, ratio=1.137, hyp_len=12996, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.85.2.63-13.86.2.45-11.59.pth
BLEU = 13.01, 37.9/17.0/9.0/4.9 (BP=1.000, ratio=1.098, hyp_len=12547, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.86.2.62-13.75.2.45-11.62.pth
BLEU = 13.22, 38.9/17.4/9.3/4.9 (BP=1.000, ratio=1.055, hyp_len=12062, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.87.2.63-13.86.2.44-11.48.pth
BLEU = 13.47, 39.6/17.9/9.4/4.9 (BP=1.000, ratio=1.068, hyp_len=12214, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.88.2.58-13.25.2.43-11.39.pth
BLEU = 13.01, 38.2/17.2/9.0/4.8 (BP=1.000, ratio=1.107, hyp_len=12660, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.89.2.63-13.92.2.43-11.34.pth
BLEU = 13.56, 39.4/17.9/9.5/5.1 (BP=1.000, ratio=1.069, hyp_len=12219, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.90.2.59-13.37.2.43-11.36.pth
BLEU = 14.14, 40.3/18.3/9.9/5.5 (BP=1.000, ratio=1.041, hyp_len=11904, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.91.2.57-13.12.2.42-11.27.pth
BLEU = 13.61, 39.0/17.8/9.5/5.2 (BP=1.000, ratio=1.064, hyp_len=12167, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.92.2.56-12.92.2.41-11.17.pth
BLEU = 13.58, 39.2/17.7/9.5/5.2 (BP=1.000, ratio=1.087, hyp_len=12421, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.93.2.60-13.42.2.41-11.16.pth
BLEU = 13.62, 39.5/18.1/9.5/5.0 (BP=1.000, ratio=1.086, hyp_len=12420, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.94.2.54-12.72.2.41-11.17.pth
BLEU = 13.74, 39.1/17.9/9.6/5.3 (BP=1.000, ratio=1.091, hyp_len=12478, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.95.2.53-12.58.2.40-11.01.pth
BLEU = 14.50, 40.6/19.0/10.2/5.6 (BP=1.000, ratio=1.051, hyp_len=12015, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.96.2.58-13.22.2.41-11.15.pth
BLEU = 14.32, 40.7/18.7/10.0/5.5 (BP=1.000, ratio=1.060, hyp_len=12113, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.97.2.59-13.33.2.40-11.07.pth
BLEU = 13.83, 39.0/18.0/9.7/5.4 (BP=1.000, ratio=1.095, hyp_len=12517, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.98.2.53-12.58.2.39-10.97.pth
BLEU = 15.61, 42.4/20.3/11.1/6.2 (BP=1.000, ratio=1.035, hyp_len=11833, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.99.2.50-12.15.2.38-10.86.pth
BLEU = 14.44, 40.5/19.0/10.2/5.6 (BP=1.000, ratio=1.091, hyp_len=12475, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/transformer/mybk-50epoch
Evaluation result for the model: transformer-rl-mybk.100.2.62-13.70.2.40-11.03.pth
BLEU = 14.97, 41.3/19.5/10.5/5.9 (BP=1.000, ratio=1.063, hyp_len=12150, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.50.2.97-19.47.2.74-15.42.pth
BLEU = 8.47, 30.5/11.7/5.5/2.6 (BP=1.000, ratio=1.138, hyp_len=13014, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.51.2.94-18.90.2.72-15.21.pth
BLEU = 9.21, 31.6/12.6/6.1/3.0 (BP=1.000, ratio=1.096, hyp_len=12525, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.52.2.86-17.50.2.71-15.10.pth
BLEU = 7.75, 28.2/11.0/5.0/2.3 (BP=1.000, ratio=1.261, hyp_len=14417, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.53.2.84-17.20.2.70-14.85.pth
BLEU = 9.50, 32.6/13.2/6.3/3.0 (BP=1.000, ratio=1.115, hyp_len=12744, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.54.2.91-18.44.2.69-14.68.pth
BLEU = 9.38, 31.3/12.7/6.2/3.1 (BP=1.000, ratio=1.151, hyp_len=13154, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.55.2.83-16.93.2.68-14.60.pth
BLEU = 8.80, 30.8/12.3/5.7/2.7 (BP=1.000, ratio=1.197, hyp_len=13684, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.56.2.90-18.10.2.67-14.38.pth
BLEU = 9.60, 32.4/13.1/6.4/3.1 (BP=1.000, ratio=1.138, hyp_len=13012, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.57.2.87-17.57.2.67-14.39.pth
BLEU = 9.43, 31.7/12.8/6.2/3.1 (BP=1.000, ratio=1.166, hyp_len=13328, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.58.2.83-16.87.2.66-14.33.pth
BLEU = 9.68, 32.8/13.0/6.4/3.2 (BP=1.000, ratio=1.091, hyp_len=12474, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.59.2.83-17.02.2.64-14.08.pth
BLEU = 9.16, 31.0/12.5/6.0/3.0 (BP=1.000, ratio=1.216, hyp_len=13896, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.60.2.83-16.88.2.63-13.92.pth
BLEU = 10.01, 33.1/13.6/6.7/3.4 (BP=1.000, ratio=1.123, hyp_len=12835, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.61.2.82-16.71.2.63-13.89.pth
BLEU = 10.59, 34.7/14.3/7.1/3.6 (BP=1.000, ratio=1.091, hyp_len=12468, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.62.2.81-16.56.2.62-13.72.pth
BLEU = 10.21, 33.6/13.8/6.8/3.5 (BP=1.000, ratio=1.128, hyp_len=12892, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.63.2.83-16.87.2.62-13.67.pth
BLEU = 10.20, 32.9/13.8/6.8/3.5 (BP=1.000, ratio=1.170, hyp_len=13381, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.64.2.76-15.87.2.60-13.47.pth
BLEU = 10.66, 34.0/14.2/7.1/3.7 (BP=1.000, ratio=1.115, hyp_len=12745, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.65.2.72-15.24.2.60-13.43.pth
BLEU = 11.16, 35.0/14.9/7.6/3.9 (BP=1.000, ratio=1.088, hyp_len=12436, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.66.2.80-16.37.2.59-13.27.pth
BLEU = 10.21, 32.8/13.8/6.8/3.5 (BP=1.000, ratio=1.179, hyp_len=13478, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.67.2.76-15.84.2.58-13.21.pth
BLEU = 11.14, 35.1/14.8/7.5/4.0 (BP=1.000, ratio=1.107, hyp_len=12654, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.68.2.75-15.62.2.58-13.24.pth
BLEU = 11.04, 35.0/14.8/7.4/3.9 (BP=1.000, ratio=1.084, hyp_len=12387, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.69.2.76-15.87.2.57-13.06.pth
BLEU = 11.62, 35.9/15.5/7.9/4.1 (BP=1.000, ratio=1.076, hyp_len=12301, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.70.2.76-15.80.2.55-12.82.pth
BLEU = 11.83, 35.8/15.6/8.1/4.3 (BP=1.000, ratio=1.107, hyp_len=12650, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.71.2.77-15.90.2.55-12.75.pth
BLEU = 11.40, 35.0/15.3/7.8/4.1 (BP=1.000, ratio=1.136, hyp_len=12984, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.72.2.73-15.40.2.55-12.74.pth
BLEU = 11.26, 34.9/14.9/7.6/4.0 (BP=1.000, ratio=1.128, hyp_len=12890, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.73.2.69-14.69.2.55-12.84.pth
BLEU = 12.10, 36.6/16.0/8.3/4.4 (BP=1.000, ratio=1.071, hyp_len=12244, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.74.2.74-15.52.2.53-12.56.pth
BLEU = 11.78, 35.7/15.7/8.0/4.3 (BP=1.000, ratio=1.122, hyp_len=12821, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.75.2.73-15.30.2.52-12.48.pth
BLEU = 12.39, 36.7/16.3/8.6/4.6 (BP=1.000, ratio=1.100, hyp_len=12570, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.76.2.73-15.34.2.53-12.59.pth
BLEU = 12.11, 36.2/16.2/8.4/4.4 (BP=1.000, ratio=1.119, hyp_len=12794, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.77.2.65-14.17.2.52-12.49.pth
BLEU = 11.66, 35.4/15.5/7.9/4.2 (BP=1.000, ratio=1.143, hyp_len=13071, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.78.2.68-14.62.2.51-12.36.pth
BLEU = 12.69, 37.7/17.0/8.7/4.7 (BP=1.000, ratio=1.085, hyp_len=12408, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.79.2.71-14.96.2.51-12.26.pth
BLEU = 12.55, 37.7/16.6/8.6/4.6 (BP=1.000, ratio=1.063, hyp_len=12151, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.80.2.66-14.27.2.50-12.22.pth
BLEU = 12.28, 36.8/16.4/8.5/4.5 (BP=1.000, ratio=1.118, hyp_len=12781, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.81.2.61-13.60.2.49-12.06.pth
BLEU = 12.45, 37.1/16.6/8.5/4.6 (BP=1.000, ratio=1.093, hyp_len=12500, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.82.2.65-14.22.2.49-12.08.pth
BLEU = 12.67, 37.2/16.8/8.8/4.7 (BP=1.000, ratio=1.093, hyp_len=12494, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.83.2.62-13.74.2.49-12.07.pth
BLEU = 12.25, 36.4/16.3/8.5/4.5 (BP=1.000, ratio=1.125, hyp_len=12859, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.84.2.71-15.06.2.49-12.09.pth
BLEU = 12.39, 36.5/16.5/8.6/4.6 (BP=1.000, ratio=1.122, hyp_len=12831, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.85.2.59-13.28.2.47-11.78.pth
BLEU = 13.23, 38.6/17.3/9.1/5.0 (BP=1.000, ratio=1.064, hyp_len=12169, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.86.2.62-13.78.2.47-11.82.pth
BLEU = 12.92, 38.0/17.1/8.9/4.8 (BP=1.000, ratio=1.077, hyp_len=12313, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.87.2.64-13.95.2.46-11.76.pth
BLEU = 13.36, 38.1/17.4/9.3/5.2 (BP=1.000, ratio=1.082, hyp_len=12364, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.88.2.65-14.09.2.45-11.65.pth
BLEU = 13.82, 39.1/18.0/9.7/5.3 (BP=1.000, ratio=1.065, hyp_len=12172, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.89.2.55-12.80.2.45-11.56.pth
BLEU = 13.15, 37.4/17.2/9.2/5.0 (BP=1.000, ratio=1.128, hyp_len=12896, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.90.2.62-13.72.2.45-11.61.pth
BLEU = 13.79, 39.1/17.9/9.7/5.3 (BP=1.000, ratio=1.049, hyp_len=11994, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.91.2.59-13.39.2.44-11.49.pth
BLEU = 14.24, 39.2/18.4/10.1/5.7 (BP=1.000, ratio=1.074, hyp_len=12279, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.92.2.58-13.25.2.44-11.49.pth
BLEU = 13.86, 39.1/18.1/9.8/5.3 (BP=1.000, ratio=1.065, hyp_len=12171, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.93.2.68-14.52.2.43-11.41.pth
BLEU = 14.21, 39.6/18.7/10.0/5.5 (BP=1.000, ratio=1.098, hyp_len=12554, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.94.2.54-12.63.2.44-11.44.pth
BLEU = 14.22, 39.4/18.4/10.0/5.6 (BP=1.000, ratio=1.087, hyp_len=12430, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.95.2.57-13.01.2.43-11.33.pth
BLEU = 15.18, 41.0/19.5/10.8/6.2 (BP=1.000, ratio=1.039, hyp_len=11882, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.96.2.65-14.19.2.42-11.23.pth
BLEU = 14.60, 40.5/19.3/10.4/5.6 (BP=1.000, ratio=1.081, hyp_len=12363, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.97.2.59-13.30.2.42-11.28.pth
BLEU = 13.68, 38.7/17.9/9.6/5.3 (BP=1.000, ratio=1.108, hyp_len=12668, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.98.2.55-12.79.2.41-11.17.pth
BLEU = 15.62, 42.5/20.6/11.1/6.1 (BP=1.000, ratio=1.039, hyp_len=11880, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.99.2.55-12.82.2.41-11.10.pth
BLEU = 15.14, 41.9/19.9/10.7/5.9 (BP=1.000, ratio=1.059, hyp_len=12104, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/transformer/mybk-60epoch
Evaluation result for the model: transformer-rl-mybk.100.2.53-12.51.2.43-11.41.pth
BLEU = 13.75, 39.6/17.9/9.5/5.3 (BP=1.000, ratio=1.062, hyp_len=12137, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.58.2.89-18.04.2.67-14.48.pth
BLEU = 9.79, 33.8/13.6/6.5/3.1 (BP=1.000, ratio=1.096, hyp_len=12533, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.59.2.85-17.23.2.67-14.42.pth
BLEU = 9.86, 33.7/13.7/6.6/3.1 (BP=1.000, ratio=1.149, hyp_len=13134, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.60.2.82-16.80.2.67-14.46.pth
BLEU = 9.64, 33.1/13.3/6.4/3.0 (BP=1.000, ratio=1.142, hyp_len=13058, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.61.2.83-16.96.2.65-14.21.pth
BLEU = 9.19, 31.7/12.7/6.2/2.9 (BP=1.000, ratio=1.162, hyp_len=13285, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.62.2.83-16.91.2.64-14.00.pth
BLEU = 10.16, 34.3/13.8/6.8/3.3 (BP=1.000, ratio=1.108, hyp_len=12668, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.63.2.82-16.82.2.65-14.15.pth
BLEU = 9.81, 33.8/13.7/6.5/3.1 (BP=1.000, ratio=1.125, hyp_len=12862, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.64.2.84-17.08.2.63-13.86.pth
BLEU = 11.04, 35.2/14.8/7.5/3.8 (BP=1.000, ratio=1.074, hyp_len=12278, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.65.2.82-16.77.2.62-13.68.pth
BLEU = 10.25, 34.3/13.9/6.9/3.4 (BP=1.000, ratio=1.088, hyp_len=12438, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.66.2.77-16.04.2.62-13.72.pth
BLEU = 10.52, 34.4/14.5/7.1/3.5 (BP=1.000, ratio=1.119, hyp_len=12794, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.67.2.80-16.42.2.61-13.60.pth
BLEU = 10.63, 34.5/14.4/7.2/3.6 (BP=1.000, ratio=1.127, hyp_len=12884, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.68.2.77-15.91.2.61-13.57.pth
BLEU = 10.71, 34.7/14.4/7.2/3.6 (BP=1.000, ratio=1.102, hyp_len=12597, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.69.2.78-16.06.2.59-13.37.pth
BLEU = 11.52, 36.5/15.6/7.8/4.0 (BP=1.000, ratio=1.071, hyp_len=12246, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.70.2.69-14.66.2.60-13.40.pth
BLEU = 12.05, 37.9/16.2/8.2/4.2 (BP=1.000, ratio=1.052, hyp_len=12029, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.71.2.78-16.07.2.58-13.23.pth
BLEU = 11.74, 36.9/16.0/8.0/4.0 (BP=1.000, ratio=1.061, hyp_len=12126, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.72.2.74-15.46.2.58-13.26.pth
BLEU = 10.93, 34.7/14.7/7.5/3.7 (BP=1.000, ratio=1.120, hyp_len=12799, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.73.2.78-16.18.2.57-13.07.pth
BLEU = 11.28, 36.2/15.5/7.7/3.8 (BP=1.000, ratio=1.090, hyp_len=12461, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.74.2.71-15.08.2.56-12.96.pth
BLEU = 11.91, 37.0/16.0/8.2/4.2 (BP=1.000, ratio=1.084, hyp_len=12389, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.75.2.70-14.89.2.56-12.88.pth
BLEU = 12.58, 38.5/17.0/8.7/4.4 (BP=1.000, ratio=1.058, hyp_len=12090, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.76.2.71-15.04.2.55-12.76.pth
BLEU = 12.66, 38.5/16.8/8.6/4.6 (BP=1.000, ratio=1.058, hyp_len=12096, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.77.2.71-15.08.2.55-12.79.pth
BLEU = 11.64, 36.2/15.6/8.0/4.1 (BP=1.000, ratio=1.111, hyp_len=12698, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.78.2.66-14.29.2.55-12.82.pth
BLEU = 11.51, 36.6/15.5/7.8/4.0 (BP=1.000, ratio=1.077, hyp_len=12317, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.79.2.62-13.75.2.54-12.70.pth
BLEU = 12.54, 38.5/16.8/8.6/4.5 (BP=1.000, ratio=1.051, hyp_len=12013, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.80.2.63-13.91.2.54-12.66.pth
BLEU = 12.07, 37.0/15.9/8.2/4.4 (BP=1.000, ratio=1.084, hyp_len=12397, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.81.2.64-13.99.2.53-12.56.pth
BLEU = 12.73, 38.4/16.9/8.7/4.7 (BP=1.000, ratio=1.055, hyp_len=12066, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.82.2.63-13.81.2.52-12.42.pth
BLEU = 11.96, 36.8/15.9/8.2/4.3 (BP=1.000, ratio=1.081, hyp_len=12355, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.83.2.65-14.16.2.52-12.40.pth
BLEU = 12.93, 38.9/17.5/8.9/4.6 (BP=1.000, ratio=1.061, hyp_len=12129, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.84.2.65-14.15.2.51-12.28.pth
BLEU = 12.93, 38.8/17.1/8.9/4.7 (BP=1.000, ratio=1.045, hyp_len=11947, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.85.2.63-13.84.2.52-12.38.pth
BLEU = 12.64, 37.7/16.5/8.7/4.7 (BP=1.000, ratio=1.088, hyp_len=12440, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.86.2.62-13.70.2.50-12.18.pth
BLEU = 12.22, 37.1/16.4/8.3/4.4 (BP=1.000, ratio=1.081, hyp_len=12362, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.87.2.58-13.21.2.49-12.03.pth
BLEU = 14.05, 40.9/18.5/9.7/5.3 (BP=1.000, ratio=1.031, hyp_len=11792, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.88.2.63-13.88.2.48-11.95.pth
BLEU = 13.45, 39.4/17.5/9.2/5.1 (BP=1.000, ratio=1.052, hyp_len=12024, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.89.2.61-13.63.2.49-12.11.pth
BLEU = 12.60, 38.4/16.7/8.6/4.6 (BP=1.000, ratio=1.046, hyp_len=11955, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.90.2.60-13.42.2.48-11.89.pth
BLEU = 12.52, 37.7/16.6/8.6/4.5 (BP=1.000, ratio=1.074, hyp_len=12277, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.91.2.67-14.50.2.47-11.79.pth
BLEU = 13.43, 39.1/17.6/9.3/5.1 (BP=1.000, ratio=1.074, hyp_len=12273, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.92.2.60-13.47.2.46-11.75.pth
BLEU = 13.93, 40.0/18.3/9.7/5.3 (BP=1.000, ratio=1.029, hyp_len=11763, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.93.2.62-13.70.2.46-11.66.pth
BLEU = 14.16, 40.8/18.5/9.8/5.5 (BP=1.000, ratio=1.034, hyp_len=11819, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.94.2.53-12.55.2.46-11.65.pth
BLEU = 13.56, 39.4/17.6/9.4/5.2 (BP=1.000, ratio=1.061, hyp_len=12129, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.95.2.56-12.92.2.45-11.55.pth
BLEU = 14.15, 40.1/18.5/9.8/5.5 (BP=1.000, ratio=1.064, hyp_len=12158, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.96.2.56-12.95.2.45-11.54.pth
BLEU = 13.49, 38.5/17.6/9.5/5.2 (BP=1.000, ratio=1.069, hyp_len=12226, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.97.2.55-12.84.2.44-11.48.pth
BLEU = 14.14, 40.0/18.4/9.9/5.5 (BP=1.000, ratio=1.042, hyp_len=11912, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.98.2.57-13.06.2.45-11.53.pth
BLEU = 14.40, 40.6/18.7/10.1/5.6 (BP=1.000, ratio=1.048, hyp_len=11981, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.99.2.59-13.33.2.44-11.43.pth
BLEU = 13.84, 39.8/18.2/9.7/5.2 (BP=1.000, ratio=1.063, hyp_len=12149, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/transformer/mybk-70epoch
Evaluation result for the model: transformer-rl-mybk.100.2.52-12.43.2.40-11.06.pth
BLEU = 13.17, 37.6/17.3/9.3/5.0 (BP=1.000, ratio=1.098, hyp_len=12550, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.70.2.71-15.04.2.56-12.89.pth
BLEU = 11.21, 35.0/14.7/7.5/4.1 (BP=1.000, ratio=1.085, hyp_len=12403, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.71.2.71-14.98.2.56-12.94.pth
BLEU = 10.88, 34.4/14.3/7.3/3.9 (BP=1.000, ratio=1.079, hyp_len=12334, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.72.2.71-15.09.2.55-12.78.pth
BLEU = 11.20, 34.8/14.8/7.5/4.0 (BP=1.000, ratio=1.075, hyp_len=12286, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.73.2.75-15.62.2.54-12.73.pth
BLEU = 10.87, 34.6/14.6/7.3/3.8 (BP=1.000, ratio=1.088, hyp_len=12434, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.74.2.77-15.99.2.54-12.62.pth
BLEU = 12.01, 37.0/15.7/8.1/4.4 (BP=1.000, ratio=1.013, hyp_len=11585, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.75.2.74-15.53.2.52-12.47.pth
BLEU = 10.93, 34.0/14.5/7.4/3.9 (BP=1.000, ratio=1.109, hyp_len=12679, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.76.2.68-14.66.2.52-12.46.pth
BLEU = 12.23, 37.3/16.2/8.3/4.4 (BP=1.000, ratio=1.039, hyp_len=11878, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.77.2.77-15.98.2.51-12.33.pth
BLEU = 11.71, 35.4/15.3/8.0/4.4 (BP=1.000, ratio=1.090, hyp_len=12465, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.78.2.62-13.73.2.50-12.20.pth
BLEU = 12.19, 37.3/16.1/8.3/4.4 (BP=1.000, ratio=1.053, hyp_len=12033, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.79.2.66-14.24.2.50-12.20.pth
BLEU = 11.17, 34.8/14.9/7.6/3.9 (BP=1.000, ratio=1.136, hyp_len=12992, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.80.2.65-14.17.2.49-12.08.pth
BLEU = 10.45, 32.4/14.1/7.1/3.7 (BP=1.000, ratio=1.221, hyp_len=13960, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.81.2.59-13.29.2.49-12.03.pth
BLEU = 11.08, 34.5/14.8/7.5/4.0 (BP=1.000, ratio=1.142, hyp_len=13056, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.82.2.69-14.75.2.48-11.95.pth
BLEU = 12.31, 36.7/16.2/8.4/4.6 (BP=1.000, ratio=1.075, hyp_len=12285, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.83.2.66-14.32.2.47-11.86.pth
BLEU = 12.10, 36.7/15.9/8.3/4.4 (BP=1.000, ratio=1.068, hyp_len=12204, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.84.2.68-14.64.2.47-11.82.pth
BLEU = 12.26, 36.1/16.1/8.5/4.6 (BP=1.000, ratio=1.108, hyp_len=12670, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.85.2.62-13.74.2.47-11.78.pth
BLEU = 11.91, 36.0/15.8/8.1/4.4 (BP=1.000, ratio=1.131, hyp_len=12935, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.86.2.68-14.53.2.46-11.67.pth
BLEU = 11.58, 34.5/15.3/8.0/4.3 (BP=1.000, ratio=1.175, hyp_len=13430, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.87.2.62-13.67.2.46-11.65.pth
BLEU = 12.35, 36.5/16.3/8.6/4.6 (BP=1.000, ratio=1.121, hyp_len=12818, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.88.2.66-14.28.2.43-11.41.pth
BLEU = 12.91, 37.5/17.0/9.0/4.8 (BP=1.000, ratio=1.106, hyp_len=12640, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.89.2.63-13.91.2.44-11.50.pth
BLEU = 13.00, 38.0/17.2/9.0/4.8 (BP=1.000, ratio=1.082, hyp_len=12370, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.90.2.60-13.45.2.44-11.46.pth
BLEU = 12.92, 37.3/16.8/9.0/4.9 (BP=1.000, ratio=1.110, hyp_len=12685, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.91.2.56-12.90.2.45-11.56.pth
BLEU = 13.75, 39.4/18.1/9.6/5.2 (BP=1.000, ratio=1.035, hyp_len=11832, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.92.2.65-14.09.2.44-11.47.pth
BLEU = 12.72, 37.8/16.8/8.8/4.7 (BP=1.000, ratio=1.076, hyp_len=12302, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.93.2.61-13.59.2.43-11.41.pth
BLEU = 11.98, 36.3/16.0/8.2/4.3 (BP=1.000, ratio=1.111, hyp_len=12696, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.94.2.63-13.93.2.42-11.25.pth
BLEU = 12.84, 37.3/16.9/9.0/4.8 (BP=1.000, ratio=1.104, hyp_len=12616, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.95.2.56-12.99.2.42-11.22.pth
BLEU = 12.50, 36.9/16.6/8.6/4.6 (BP=1.000, ratio=1.136, hyp_len=12992, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.96.2.55-12.79.2.43-11.34.pth
BLEU = 13.41, 39.1/17.7/9.3/5.0 (BP=1.000, ratio=1.053, hyp_len=12037, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.97.2.56-12.89.2.42-11.29.pth
BLEU = 13.34, 37.7/17.4/9.4/5.1 (BP=1.000, ratio=1.110, hyp_len=12694, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.98.2.61-13.56.2.42-11.20.pth
BLEU = 13.29, 38.1/17.3/9.2/5.2 (BP=1.000, ratio=1.068, hyp_len=12214, ref_len=11432)
Evaluation result for the model: transformer-rl-mybk.99.2.54-12.68.2.40-11.07.pth
BLEU = 12.89, 36.8/16.9/9.1/4.9 (BP=1.000, ratio=1.153, hyp_len=13176, ref_len=11432)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/transformer/bkmy-30epoch
Evaluation result for the model: transformer-rl-bkmy.100.2.34-10.38.2.26-9.54.pth
BLEU = 18.68, 47.7/24.8/13.4/7.6 (BP=1.000, ratio=1.013, hyp_len=12394, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.31.2.92-18.56.2.80-16.40.pth
BLEU = 7.90, 32.9/12.3/4.9/2.0 (BP=1.000, ratio=1.097, hyp_len=13412, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.32.2.82-16.85.2.78-16.13.pth
BLEU = 8.64, 34.8/13.3/5.4/2.2 (BP=1.000, ratio=1.039, hyp_len=12710, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.33.2.84-17.05.2.76-15.87.pth
BLEU = 8.76, 35.0/13.5/5.6/2.2 (BP=1.000, ratio=1.048, hyp_len=12824, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.34.2.86-17.46.2.74-15.50.pth
BLEU = 8.85, 35.8/13.9/5.6/2.2 (BP=1.000, ratio=1.046, hyp_len=12788, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.35.2.80-16.41.2.72-15.18.pth
BLEU = 9.03, 35.5/14.0/5.7/2.3 (BP=1.000, ratio=1.069, hyp_len=13073, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.36.2.80-16.37.2.70-14.95.pth
BLEU = 9.79, 37.0/15.0/6.2/2.7 (BP=1.000, ratio=1.025, hyp_len=12532, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.37.2.76-15.88.2.69-14.80.pth
BLEU = 8.96, 33.7/13.7/5.8/2.4 (BP=1.000, ratio=1.155, hyp_len=14124, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.38.2.76-15.86.2.68-14.55.pth
BLEU = 9.69, 36.7/14.8/6.1/2.6 (BP=1.000, ratio=1.050, hyp_len=12840, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.39.2.75-15.64.2.66-14.24.pth
BLEU = 9.98, 37.6/15.5/6.4/2.6 (BP=1.000, ratio=1.051, hyp_len=12856, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.40.2.78-16.15.2.64-14.00.pth
BLEU = 9.99, 36.7/15.3/6.5/2.7 (BP=1.000, ratio=1.084, hyp_len=13261, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.41.2.73-15.34.2.64-13.95.pth
BLEU = 8.88, 34.0/14.0/5.7/2.3 (BP=1.000, ratio=1.189, hyp_len=14539, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.42.2.71-15.05.2.62-13.76.pth
BLEU = 9.66, 35.8/14.8/6.3/2.6 (BP=1.000, ratio=1.122, hyp_len=13720, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.43.2.66-14.34.2.62-13.67.pth
BLEU = 9.29, 35.0/14.4/6.0/2.5 (BP=1.000, ratio=1.122, hyp_len=13728, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.44.2.73-15.33.2.60-13.46.pth
BLEU = 10.24, 37.5/15.7/6.6/2.8 (BP=1.000, ratio=1.088, hyp_len=13313, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.45.2.70-14.91.2.59-13.33.pth
BLEU = 10.38, 37.0/15.7/6.8/3.0 (BP=1.000, ratio=1.090, hyp_len=13330, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.46.2.64-13.98.2.57-13.10.pth
BLEU = 11.10, 39.1/16.8/7.3/3.2 (BP=1.000, ratio=1.030, hyp_len=12594, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.47.2.62-13.74.2.57-13.02.pth
BLEU = 10.55, 37.7/16.0/6.9/3.0 (BP=1.000, ratio=1.111, hyp_len=13592, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.48.2.64-13.95.2.56-12.90.pth
BLEU = 10.04, 36.2/15.4/6.5/2.8 (BP=1.000, ratio=1.160, hyp_len=14193, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.49.2.65-14.14.2.54-12.72.pth
BLEU = 11.27, 39.5/17.1/7.3/3.3 (BP=1.000, ratio=1.045, hyp_len=12785, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.50.2.59-13.39.2.53-12.53.pth
BLEU = 11.12, 38.8/16.9/7.3/3.2 (BP=1.000, ratio=1.098, hyp_len=13425, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.51.2.58-13.23.2.53-12.51.pth
BLEU = 9.74, 34.8/15.1/6.3/2.7 (BP=1.000, ratio=1.228, hyp_len=15021, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.52.2.60-13.40.2.51-12.27.pth
BLEU = 11.75, 40.1/17.6/7.7/3.5 (BP=1.000, ratio=1.049, hyp_len=12836, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.53.2.64-14.04.2.51-12.25.pth
BLEU = 12.13, 40.2/17.9/8.0/3.8 (BP=1.000, ratio=1.077, hyp_len=13168, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.54.2.53-12.53.2.50-12.21.pth
BLEU = 10.79, 36.4/16.2/7.1/3.2 (BP=1.000, ratio=1.195, hyp_len=14611, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.55.2.57-13.09.2.49-12.10.pth
BLEU = 12.40, 41.1/18.5/8.3/3.7 (BP=1.000, ratio=1.028, hyp_len=12579, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.56.2.54-12.69.2.49-12.05.pth
BLEU = 11.55, 38.7/16.9/7.7/3.5 (BP=1.000, ratio=1.116, hyp_len=13653, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.57.2.53-12.50.2.48-11.92.pth
BLEU = 11.85, 38.9/17.4/7.9/3.7 (BP=1.000, ratio=1.122, hyp_len=13721, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.58.2.52-12.44.2.47-11.82.pth
BLEU = 12.68, 40.7/18.3/8.4/4.1 (BP=1.000, ratio=1.061, hyp_len=12972, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.59.2.50-12.17.2.46-11.65.pth
BLEU = 13.15, 41.3/19.0/9.0/4.2 (BP=1.000, ratio=1.049, hyp_len=12825, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.60.2.50-12.15.2.45-11.64.pth
BLEU = 12.90, 41.3/18.7/8.7/4.1 (BP=1.000, ratio=1.050, hyp_len=12846, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.61.2.49-12.08.2.44-11.49.pth
BLEU = 13.05, 40.9/19.0/8.9/4.2 (BP=1.000, ratio=1.079, hyp_len=13200, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.62.2.49-12.01.2.44-11.49.pth
BLEU = 11.52, 37.5/17.0/7.7/3.6 (BP=1.000, ratio=1.191, hyp_len=14562, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.63.2.49-12.12.2.43-11.40.pth
BLEU = 13.22, 41.2/18.9/8.9/4.4 (BP=1.000, ratio=1.061, hyp_len=12971, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.64.2.45-11.56.2.42-11.27.pth
BLEU = 13.74, 42.6/19.8/9.4/4.5 (BP=1.000, ratio=1.034, hyp_len=12646, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.65.2.47-11.79.2.42-11.24.pth
BLEU = 13.42, 41.9/19.5/9.1/4.3 (BP=1.000, ratio=1.063, hyp_len=12999, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.66.2.50-12.20.2.41-11.11.pth
BLEU = 13.95, 42.7/19.8/9.5/4.7 (BP=1.000, ratio=1.038, hyp_len=12697, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.67.2.45-11.53.2.41-11.16.pth
BLEU = 13.04, 40.6/19.0/8.8/4.2 (BP=1.000, ratio=1.109, hyp_len=13563, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.68.2.45-11.63.2.40-11.06.pth
BLEU = 13.75, 42.4/19.5/9.4/4.6 (BP=1.000, ratio=1.031, hyp_len=12608, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.69.2.50-12.15.2.39-10.95.pth
BLEU = 13.80, 42.1/19.8/9.4/4.6 (BP=1.000, ratio=1.060, hyp_len=12960, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.70.2.46-11.67.2.39-10.95.pth
BLEU = 13.32, 40.5/19.0/9.1/4.5 (BP=1.000, ratio=1.122, hyp_len=13724, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.71.2.48-11.91.2.38-10.85.pth
BLEU = 13.91, 42.0/19.8/9.6/4.7 (BP=1.000, ratio=1.070, hyp_len=13084, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.72.2.51-12.27.2.37-10.67.pth
BLEU = 14.70, 43.3/20.9/10.2/5.0 (BP=1.000, ratio=1.058, hyp_len=12945, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.73.2.46-11.75.2.37-10.73.pth
BLEU = 14.83, 43.8/20.9/10.2/5.2 (BP=1.000, ratio=1.041, hyp_len=12728, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.74.2.40-11.08.2.37-10.67.pth
BLEU = 15.47, 45.0/21.6/10.7/5.5 (BP=1.000, ratio=1.015, hyp_len=12417, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.75.2.41-11.13.2.35-10.53.pth
BLEU = 14.67, 42.3/20.6/10.3/5.2 (BP=1.000, ratio=1.088, hyp_len=13304, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.76.2.40-11.01.2.36-10.57.pth
BLEU = 14.99, 43.8/20.9/10.4/5.3 (BP=1.000, ratio=1.043, hyp_len=12763, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.77.2.38-10.84.2.35-10.53.pth
BLEU = 15.25, 44.6/21.2/10.6/5.4 (BP=1.000, ratio=1.020, hyp_len=12471, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.78.2.40-10.97.2.34-10.37.pth
BLEU = 14.98, 44.6/21.4/10.3/5.1 (BP=1.000, ratio=1.032, hyp_len=12627, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.79.2.37-10.72.2.33-10.29.pth
BLEU = 14.93, 42.9/20.7/10.3/5.4 (BP=1.000, ratio=1.081, hyp_len=13224, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.80.2.35-10.50.2.33-10.25.pth
BLEU = 16.48, 45.7/22.8/11.6/6.1 (BP=1.000, ratio=1.026, hyp_len=12549, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.81.2.35-10.49.2.33-10.24.pth
BLEU = 15.92, 45.5/22.3/11.1/5.7 (BP=1.000, ratio=1.033, hyp_len=12629, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.82.2.34-10.35.2.33-10.32.pth
BLEU = 15.24, 43.8/21.3/10.6/5.5 (BP=1.000, ratio=1.049, hyp_len=12836, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.83.2.37-10.68.2.32-10.20.pth
BLEU = 16.03, 44.9/22.2/11.2/5.9 (BP=1.000, ratio=1.032, hyp_len=12624, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.84.2.37-10.65.2.31-10.06.pth
BLEU = 16.37, 46.1/22.4/11.5/6.0 (BP=1.000, ratio=1.009, hyp_len=12341, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.85.2.33-10.28.2.31-10.12.pth
BLEU = 15.09, 43.5/21.0/10.5/5.4 (BP=1.000, ratio=1.075, hyp_len=13151, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.86.2.32-10.17.2.31-10.03.pth
BLEU = 16.97, 46.5/23.2/11.8/6.5 (BP=1.000, ratio=1.008, hyp_len=12334, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.87.2.29-9.84.2.31-10.03.pth
BLEU = 16.44, 45.8/22.5/11.5/6.2 (BP=1.000, ratio=1.008, hyp_len=12323, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.88.2.30-10.01.2.29-9.89.pth
BLEU = 16.61, 45.1/22.7/11.7/6.4 (BP=1.000, ratio=1.049, hyp_len=12835, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.89.2.32-10.17.2.29-9.84.pth
BLEU = 17.05, 45.5/23.1/12.1/6.7 (BP=1.000, ratio=1.048, hyp_len=12820, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.90.2.32-10.16.2.29-9.85.pth
BLEU = 17.92, 47.1/24.2/12.7/7.1 (BP=1.000, ratio=1.027, hyp_len=12559, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.91.2.32-10.22.2.28-9.77.pth
BLEU = 18.87, 48.3/25.3/13.7/7.7 (BP=0.998, ratio=0.998, hyp_len=12206, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.92.2.31-10.11.2.28-9.81.pth
BLEU = 17.07, 45.4/22.9/12.1/6.7 (BP=1.000, ratio=1.049, hyp_len=12835, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.93.2.32-10.21.2.28-9.77.pth
BLEU = 17.63, 46.8/23.7/12.5/7.0 (BP=1.000, ratio=1.010, hyp_len=12355, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.94.2.33-10.32.2.28-9.73.pth
BLEU = 17.67, 47.0/24.0/12.6/6.8 (BP=1.000, ratio=1.018, hyp_len=12446, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.95.2.31-10.10.2.27-9.73.pth
BLEU = 17.70, 46.3/23.8/12.7/7.0 (BP=1.000, ratio=1.050, hyp_len=12846, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.96.2.34-10.37.2.27-9.72.pth
BLEU = 17.59, 46.8/23.7/12.5/6.9 (BP=1.000, ratio=1.020, hyp_len=12476, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.97.2.32-10.13.2.26-9.61.pth
BLEU = 17.45, 45.8/23.5/12.5/6.9 (BP=1.000, ratio=1.063, hyp_len=13003, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.98.2.23-9.28.2.26-9.57.pth
BLEU = 17.69, 46.8/23.8/12.5/7.0 (BP=1.000, ratio=1.051, hyp_len=12855, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.99.2.27-9.64.2.26-9.54.pth
BLEU = 18.80, 47.7/25.0/13.5/7.8 (BP=1.000, ratio=1.025, hyp_len=12540, ref_len=12231)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/transformer/bkmy-40epoch
Evaluation result for the model: transformer-rl-bkmy.100.2.26-9.63.2.29-9.84.pth
BLEU = 16.63, 45.9/23.1/11.7/6.2 (BP=1.000, ratio=1.014, hyp_len=12407, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.41.2.72-15.19.2.68-14.63.pth
BLEU = 10.22, 38.2/15.5/6.6/2.8 (BP=1.000, ratio=1.011, hyp_len=12366, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.42.2.68-14.64.2.68-14.58.pth
BLEU = 10.03, 37.5/15.1/6.3/2.8 (BP=1.000, ratio=1.025, hyp_len=12540, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.43.2.69-14.76.2.66-14.32.pth
BLEU = 10.77, 39.3/16.3/7.0/3.2 (BP=0.985, ratio=0.985, hyp_len=12046, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.44.2.76-15.86.2.65-14.10.pth
BLEU = 10.72, 39.3/16.2/6.9/3.1 (BP=0.993, ratio=0.993, hyp_len=12150, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.45.2.69-14.68.2.63-13.93.pth
BLEU = 10.69, 40.2/16.6/7.1/3.2 (BP=0.963, ratio=0.964, hyp_len=11786, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.46.2.65-14.20.2.62-13.71.pth
BLEU = 11.07, 40.2/17.0/7.2/3.2 (BP=0.985, ratio=0.985, hyp_len=12049, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.47.2.64-13.97.2.61-13.60.pth
BLEU = 11.18, 40.1/16.9/7.2/3.3 (BP=0.994, ratio=0.994, hyp_len=12161, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.48.2.71-15.09.2.60-13.48.pth
BLEU = 11.20, 40.8/17.4/7.4/3.3 (BP=0.975, ratio=0.975, hyp_len=11929, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.49.2.68-14.54.2.58-13.25.pth
BLEU = 11.31, 39.7/17.0/7.3/3.3 (BP=1.000, ratio=1.021, hyp_len=12483, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.50.2.65-14.17.2.58-13.17.pth
BLEU = 11.09, 41.7/17.7/7.5/3.5 (BP=0.941, ratio=0.943, hyp_len=11530, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.51.2.62-13.69.2.56-12.98.pth
BLEU = 11.81, 40.7/17.7/7.8/3.6 (BP=0.990, ratio=0.991, hyp_len=12115, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.52.2.53-12.58.2.55-12.86.pth
BLEU = 12.19, 41.5/18.3/8.2/3.7 (BP=0.985, ratio=0.986, hyp_len=12054, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.53.2.59-13.36.2.54-12.74.pth
BLEU = 12.07, 42.0/18.4/8.1/3.7 (BP=0.975, ratio=0.976, hyp_len=11933, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.54.2.62-13.76.2.54-12.62.pth
BLEU = 12.23, 40.5/17.9/8.1/3.8 (BP=1.000, ratio=1.021, hyp_len=12485, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.55.2.54-12.62.2.54-12.69.pth
BLEU = 11.80, 39.6/17.3/7.7/3.7 (BP=1.000, ratio=1.034, hyp_len=12644, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.56.2.57-13.09.2.53-12.51.pth
BLEU = 12.49, 41.6/18.7/8.3/3.8 (BP=0.995, ratio=0.995, hyp_len=12175, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.57.2.58-13.15.2.51-12.30.pth
BLEU = 12.80, 41.5/18.5/8.6/4.1 (BP=1.000, ratio=1.009, hyp_len=12345, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.58.2.58-13.19.2.50-12.22.pth
BLEU = 13.06, 42.1/19.2/8.8/4.1 (BP=1.000, ratio=1.004, hyp_len=12274, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.59.2.53-12.59.2.49-12.09.pth
BLEU = 13.31, 42.0/19.4/9.0/4.2 (BP=1.000, ratio=1.021, hyp_len=12492, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.60.2.50-12.22.2.49-12.04.pth
BLEU = 13.26, 42.1/19.3/8.9/4.3 (BP=1.000, ratio=1.005, hyp_len=12298, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.61.2.47-11.86.2.48-11.91.pth
BLEU = 12.84, 41.9/18.9/8.6/4.0 (BP=1.000, ratio=1.024, hyp_len=12519, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.62.2.57-13.01.2.47-11.88.pth
BLEU = 13.17, 42.7/19.5/9.0/4.3 (BP=0.984, ratio=0.984, hyp_len=12031, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.63.2.50-12.22.2.47-11.81.pth
BLEU = 13.42, 43.0/19.7/9.1/4.2 (BP=1.000, ratio=1.001, hyp_len=12247, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.64.2.51-12.34.2.46-11.67.pth
BLEU = 13.58, 43.4/20.0/9.3/4.2 (BP=0.999, ratio=0.999, hyp_len=12224, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.65.2.49-12.09.2.45-11.64.pth
BLEU = 13.04, 42.2/19.0/8.8/4.1 (BP=1.000, ratio=1.005, hyp_len=12288, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.66.2.45-11.61.2.46-11.70.pth
BLEU = 13.56, 42.6/19.4/9.3/4.5 (BP=0.995, ratio=0.995, hyp_len=12173, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.67.2.44-11.53.2.44-11.47.pth
BLEU = 13.90, 43.5/20.2/9.7/4.7 (BP=0.984, ratio=0.984, hyp_len=12033, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.68.2.47-11.80.2.43-11.36.pth
BLEU = 13.55, 42.9/19.6/9.2/4.4 (BP=1.000, ratio=1.003, hyp_len=12272, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.69.2.46-11.72.2.43-11.31.pth
BLEU = 13.78, 42.5/19.8/9.5/4.5 (BP=1.000, ratio=1.028, hyp_len=12568, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.70.2.44-11.50.2.42-11.30.pth
BLEU = 13.81, 43.0/19.9/9.5/4.5 (BP=1.000, ratio=1.006, hyp_len=12305, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.71.2.45-11.56.2.41-11.13.pth
BLEU = 13.51, 42.5/19.4/9.2/4.4 (BP=1.000, ratio=1.013, hyp_len=12390, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.72.2.42-11.24.2.40-11.03.pth
BLEU = 14.03, 43.8/20.3/9.6/4.5 (BP=1.000, ratio=1.011, hyp_len=12368, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.73.2.44-11.44.2.39-10.95.pth
BLEU = 14.37, 43.9/20.5/9.8/4.8 (BP=1.000, ratio=1.003, hyp_len=12266, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.74.2.37-10.65.2.40-10.98.pth
BLEU = 14.40, 43.9/20.5/9.9/4.8 (BP=1.000, ratio=1.002, hyp_len=12256, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.75.2.50-12.20.2.40-10.98.pth
BLEU = 14.37, 42.9/20.4/10.0/4.9 (BP=1.000, ratio=1.033, hyp_len=12630, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.76.2.41-11.16.2.39-10.89.pth
BLEU = 14.37, 43.3/20.3/9.9/4.9 (BP=1.000, ratio=1.033, hyp_len=12631, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.77.2.42-11.24.2.39-10.89.pth
BLEU = 14.16, 43.8/20.3/9.8/4.6 (BP=1.000, ratio=1.024, hyp_len=12524, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.78.2.41-11.08.2.38-10.77.pth
BLEU = 15.31, 45.0/21.5/10.8/5.4 (BP=0.992, ratio=0.992, hyp_len=12138, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.79.2.40-11.03.2.37-10.70.pth
BLEU = 14.49, 43.1/20.5/10.0/5.0 (BP=1.000, ratio=1.026, hyp_len=12547, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.80.2.38-10.76.2.36-10.57.pth
BLEU = 14.71, 44.3/20.9/10.2/5.0 (BP=0.999, ratio=0.999, hyp_len=12222, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.81.2.35-10.51.2.36-10.56.pth
BLEU = 14.64, 44.2/20.8/10.1/4.9 (BP=1.000, ratio=1.007, hyp_len=12319, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.82.2.37-10.69.2.35-10.53.pth
BLEU = 15.45, 44.9/21.6/10.7/5.5 (BP=1.000, ratio=1.004, hyp_len=12278, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.83.2.40-11.02.2.35-10.45.pth
BLEU = 15.30, 45.3/21.8/10.8/5.4 (BP=0.991, ratio=0.991, hyp_len=12120, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.84.2.39-10.87.2.34-10.43.pth
BLEU = 14.97, 44.3/21.2/10.3/5.2 (BP=1.000, ratio=1.018, hyp_len=12457, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.85.2.36-10.63.2.34-10.36.pth
BLEU = 15.24, 44.7/21.4/10.6/5.3 (BP=1.000, ratio=1.024, hyp_len=12521, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.86.2.40-11.01.2.34-10.33.pth
BLEU = 15.41, 45.3/21.9/11.0/5.5 (BP=0.987, ratio=0.987, hyp_len=12068, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.87.2.37-10.71.2.32-10.21.pth
BLEU = 15.73, 45.2/21.9/11.0/5.6 (BP=1.000, ratio=1.005, hyp_len=12289, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.88.2.33-10.24.2.32-10.18.pth
BLEU = 15.84, 45.2/22.0/11.1/5.7 (BP=1.000, ratio=1.006, hyp_len=12299, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.89.2.28-9.82.2.32-10.15.pth
BLEU = 15.99, 45.2/22.4/11.3/5.7 (BP=1.000, ratio=1.035, hyp_len=12653, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.90.2.32-10.14.2.32-10.13.pth
BLEU = 16.20, 46.2/22.8/11.4/5.9 (BP=0.992, ratio=0.992, hyp_len=12136, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.91.2.30-10.00.2.32-10.13.pth
BLEU = 15.66, 44.8/21.7/10.9/5.7 (BP=1.000, ratio=1.013, hyp_len=12388, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.92.2.30-9.96.2.30-10.02.pth
BLEU = 16.04, 45.4/22.3/11.2/5.8 (BP=1.000, ratio=1.025, hyp_len=12542, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.93.2.35-10.52.2.31-10.08.pth
BLEU = 15.95, 45.3/22.3/11.2/5.7 (BP=1.000, ratio=1.023, hyp_len=12510, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.94.2.27-9.72.2.31-10.02.pth
BLEU = 16.38, 45.6/22.7/11.5/6.0 (BP=1.000, ratio=1.012, hyp_len=12383, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.95.2.32-10.21.2.30-9.99.pth
BLEU = 16.59, 46.2/23.0/11.7/6.2 (BP=0.994, ratio=0.994, hyp_len=12153, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.96.2.28-9.79.2.30-9.97.pth
BLEU = 16.08, 45.3/22.4/11.3/5.9 (BP=1.000, ratio=1.020, hyp_len=12473, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.97.2.28-9.81.2.29-9.87.pth
BLEU = 17.22, 47.1/23.9/12.3/6.4 (BP=0.997, ratio=0.997, hyp_len=12199, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.98.2.28-9.79.2.28-9.75.pth
BLEU = 17.34, 47.1/23.8/12.4/6.5 (BP=0.999, ratio=0.999, hyp_len=12213, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.99.2.31-10.12.2.28-9.82.pth
BLEU = 17.24, 46.6/23.4/12.2/6.6 (BP=1.000, ratio=1.015, hyp_len=12416, ref_len=12231)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/transformer/bkmy-50epoch
Evaluation result for the model: transformer-rl-bkmy.100.2.27-9.68.2.25-9.49.pth
BLEU = 18.48, 48.1/24.9/13.2/7.4 (BP=1.000, ratio=1.015, hyp_len=12409, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.50.2.58-13.22.2.56-12.99.pth
BLEU = 11.98, 41.0/18.0/7.9/3.5 (BP=1.000, ratio=1.020, hyp_len=12473, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.51.2.60-13.43.2.53-12.61.pth
BLEU = 12.90, 42.6/19.1/8.7/3.9 (BP=0.999, ratio=0.999, hyp_len=12222, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.52.2.59-13.39.2.54-12.70.pth
BLEU = 12.82, 42.9/19.1/8.8/4.1 (BP=0.977, ratio=0.977, hyp_len=11949, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.53.2.60-13.51.2.53-12.61.pth
BLEU = 12.83, 42.5/19.2/8.9/4.0 (BP=0.982, ratio=0.982, hyp_len=12008, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.54.2.55-12.76.2.53-12.50.pth
BLEU = 12.98, 42.4/18.9/8.7/4.1 (BP=1.000, ratio=1.005, hyp_len=12288, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.55.2.49-12.01.2.52-12.39.pth
BLEU = 13.12, 42.3/19.1/8.8/4.2 (BP=0.998, ratio=0.998, hyp_len=12209, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.56.2.58-13.16.2.51-12.31.pth
BLEU = 13.43, 42.3/19.2/9.0/4.4 (BP=1.000, ratio=1.008, hyp_len=12329, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.57.2.55-12.81.2.50-12.14.pth
BLEU = 13.90, 43.3/19.8/9.4/4.6 (BP=1.000, ratio=1.000, hyp_len=12231, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.58.2.51-12.34.2.50-12.13.pth
BLEU = 13.40, 42.2/19.1/9.1/4.4 (BP=1.000, ratio=1.005, hyp_len=12293, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.59.2.47-11.86.2.49-12.06.pth
BLEU = 13.52, 42.5/19.4/9.2/4.4 (BP=1.000, ratio=1.022, hyp_len=12499, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.60.2.49-12.10.2.47-11.76.pth
BLEU = 13.79, 43.9/20.1/9.5/4.7 (BP=0.978, ratio=0.978, hyp_len=11959, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.61.2.53-12.52.2.48-11.92.pth
BLEU = 13.41, 43.0/19.6/9.2/4.4 (BP=0.989, ratio=0.989, hyp_len=12101, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.62.2.50-12.18.2.46-11.68.pth
BLEU = 13.36, 42.3/19.2/9.0/4.3 (BP=1.000, ratio=1.024, hyp_len=12520, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.63.2.45-11.58.2.45-11.59.pth
BLEU = 14.59, 44.3/20.6/10.1/5.1 (BP=0.991, ratio=0.991, hyp_len=12125, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.64.2.47-11.77.2.45-11.56.pth
BLEU = 14.04, 43.4/20.0/9.6/4.7 (BP=1.000, ratio=1.000, hyp_len=12229, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.65.2.40-11.05.2.44-11.50.pth
BLEU = 13.81, 42.6/19.8/9.4/4.6 (BP=1.000, ratio=1.030, hyp_len=12597, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.66.2.49-12.05.2.44-11.45.pth
BLEU = 14.15, 43.5/20.1/9.6/4.8 (BP=1.000, ratio=1.007, hyp_len=12311, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.67.2.46-11.75.2.43-11.31.pth
BLEU = 14.36, 43.6/20.5/9.8/4.8 (BP=1.000, ratio=1.015, hyp_len=12414, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.68.2.46-11.69.2.42-11.23.pth
BLEU = 14.83, 44.6/21.0/10.3/5.2 (BP=0.988, ratio=0.988, hyp_len=12085, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.69.2.46-11.68.2.41-11.18.pth
BLEU = 14.83, 44.7/21.2/10.3/5.2 (BP=0.989, ratio=0.989, hyp_len=12101, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.70.2.45-11.63.2.41-11.12.pth
BLEU = 14.69, 44.5/20.8/10.1/5.0 (BP=1.000, ratio=1.003, hyp_len=12268, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.71.2.45-11.59.2.41-11.10.pth
BLEU = 14.58, 44.1/20.8/10.0/4.9 (BP=1.000, ratio=1.000, hyp_len=12232, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.72.2.48-11.94.2.40-10.98.pth
BLEU = 14.95, 44.5/21.1/10.3/5.2 (BP=1.000, ratio=1.011, hyp_len=12369, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.73.2.41-11.19.2.39-10.94.pth
BLEU = 15.25, 44.6/21.4/10.5/5.4 (BP=1.000, ratio=1.005, hyp_len=12297, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.74.2.40-11.04.2.38-10.79.pth
BLEU = 15.38, 44.6/21.5/10.7/5.4 (BP=1.000, ratio=1.026, hyp_len=12546, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.75.2.39-10.88.2.38-10.79.pth
BLEU = 15.18, 45.5/21.7/10.7/5.5 (BP=0.979, ratio=0.979, hyp_len=11972, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.76.2.40-11.05.2.36-10.63.pth
BLEU = 16.02, 46.6/22.8/11.3/5.9 (BP=0.983, ratio=0.983, hyp_len=12025, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.77.2.41-11.11.2.36-10.62.pth
BLEU = 15.34, 45.4/21.8/10.7/5.3 (BP=0.996, ratio=0.996, hyp_len=12179, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.78.2.35-10.50.2.35-10.53.pth
BLEU = 15.79, 45.9/22.3/11.1/5.7 (BP=0.990, ratio=0.990, hyp_len=12113, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.79.2.34-10.40.2.35-10.49.pth
BLEU = 15.96, 45.5/22.2/11.2/5.7 (BP=1.000, ratio=1.004, hyp_len=12283, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.80.2.34-10.35.2.34-10.40.pth
BLEU = 16.44, 46.7/23.1/11.7/6.0 (BP=0.991, ratio=0.991, hyp_len=12123, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.81.2.33-10.31.2.33-10.29.pth
BLEU = 16.30, 47.7/23.6/11.9/6.2 (BP=0.958, ratio=0.959, hyp_len=11730, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.82.2.33-10.24.2.34-10.33.pth
BLEU = 16.02, 46.6/23.1/11.4/5.9 (BP=0.977, ratio=0.977, hyp_len=11949, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.83.2.38-10.76.2.32-10.18.pth
BLEU = 16.97, 47.4/23.7/12.1/6.4 (BP=0.989, ratio=0.989, hyp_len=12094, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.84.2.36-10.62.2.33-10.25.pth
BLEU = 16.65, 46.4/23.0/11.7/6.2 (BP=1.000, ratio=1.005, hyp_len=12291, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.85.2.37-10.70.2.31-10.08.pth
BLEU = 16.26, 46.0/22.4/11.3/6.0 (BP=1.000, ratio=1.007, hyp_len=12317, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.86.2.34-10.43.2.31-10.11.pth
BLEU = 16.59, 46.1/22.9/11.7/6.2 (BP=1.000, ratio=1.034, hyp_len=12650, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.87.2.28-9.79.2.31-10.06.pth
BLEU = 16.98, 47.0/23.4/12.1/6.5 (BP=0.991, ratio=0.991, hyp_len=12117, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.88.2.31-10.05.2.30-10.01.pth
BLEU = 17.10, 48.0/24.0/12.3/6.7 (BP=0.973, ratio=0.973, hyp_len=11902, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.89.2.31-10.04.2.29-9.92.pth
BLEU = 17.19, 48.1/24.0/12.3/6.6 (BP=0.981, ratio=0.981, hyp_len=11997, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.90.2.29-9.90.2.29-9.90.pth
BLEU = 17.56, 48.0/24.2/12.5/6.9 (BP=0.986, ratio=0.986, hyp_len=12064, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.91.2.33-10.32.2.28-9.81.pth
BLEU = 17.53, 47.9/24.2/12.5/6.9 (BP=0.987, ratio=0.987, hyp_len=12068, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.92.2.28-9.77.2.29-9.88.pth
BLEU = 17.32, 47.8/24.0/12.5/6.8 (BP=0.983, ratio=0.983, hyp_len=12025, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.93.2.28-9.81.2.29-9.85.pth
BLEU = 17.44, 47.1/23.7/12.3/6.8 (BP=1.000, ratio=1.009, hyp_len=12343, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.94.2.31-10.11.2.28-9.80.pth
BLEU = 17.83, 47.5/24.0/12.7/7.0 (BP=1.000, ratio=1.008, hyp_len=12328, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.95.2.28-9.75.2.28-9.81.pth
BLEU = 17.68, 47.1/23.9/12.5/6.9 (BP=1.000, ratio=1.002, hyp_len=12253, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.96.2.26-9.59.2.27-9.66.pth
BLEU = 17.88, 48.0/24.3/12.7/7.0 (BP=0.997, ratio=0.997, hyp_len=12189, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.97.2.30-9.93.2.26-9.56.pth
BLEU = 18.01, 49.2/25.2/13.1/7.1 (BP=0.978, ratio=0.978, hyp_len=11968, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.98.2.29-9.87.2.26-9.63.pth
BLEU = 18.30, 48.3/24.7/13.1/7.3 (BP=0.994, ratio=0.994, hyp_len=12162, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.99.2.26-9.61.2.25-9.52.pth
BLEU = 17.73, 47.3/23.9/12.6/6.9 (BP=1.000, ratio=1.017, hyp_len=12440, ref_len=12231)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/transformer/bkmy-60epoch
Evaluation result for the model: transformer-rl-bkmy.100.2.24-9.36.2.22-9.18.pth
BLEU = 19.49, 49.2/25.9/14.3/8.2 (BP=0.990, ratio=0.990, hyp_len=12104, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.61.2.52-12.41.2.43-11.37.pth
BLEU = 13.69, 43.6/20.1/9.6/4.6 (BP=0.977, ratio=0.977, hyp_len=11953, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.62.2.46-11.72.2.41-11.14.pth
BLEU = 13.09, 41.5/18.9/8.9/4.2 (BP=1.000, ratio=1.043, hyp_len=12755, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.63.2.48-11.97.2.40-11.07.pth
BLEU = 13.80, 42.6/19.7/9.5/4.6 (BP=1.000, ratio=1.033, hyp_len=12635, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.64.2.45-11.62.2.40-10.99.pth
BLEU = 14.70, 44.0/20.8/10.3/5.3 (BP=0.984, ratio=0.985, hyp_len=12042, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.65.2.50-12.20.2.39-10.92.pth
BLEU = 14.15, 42.7/19.8/9.8/4.9 (BP=1.000, ratio=1.023, hyp_len=12507, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.66.2.47-11.87.2.39-10.88.pth
BLEU = 14.52, 44.0/20.5/10.2/5.1 (BP=0.983, ratio=0.983, hyp_len=12028, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.67.2.44-11.48.2.38-10.83.pth
BLEU = 14.27, 43.5/20.0/9.9/4.9 (BP=0.997, ratio=0.997, hyp_len=12190, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.68.2.47-11.78.2.38-10.75.pth
BLEU = 14.72, 44.1/20.6/10.3/5.3 (BP=0.988, ratio=0.988, hyp_len=12084, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.69.2.42-11.26.2.37-10.66.pth
BLEU = 14.41, 43.4/20.2/10.0/4.9 (BP=1.000, ratio=1.004, hyp_len=12279, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.70.2.40-10.98.2.36-10.56.pth
BLEU = 15.60, 45.1/21.7/11.0/5.8 (BP=0.988, ratio=0.988, hyp_len=12084, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.71.2.46-11.71.2.36-10.57.pth
BLEU = 15.07, 44.4/21.0/10.5/5.3 (BP=0.996, ratio=0.996, hyp_len=12182, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.72.2.41-11.10.2.35-10.47.pth
BLEU = 14.72, 44.4/20.6/10.2/5.1 (BP=0.994, ratio=0.994, hyp_len=12158, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.73.2.43-11.38.2.34-10.36.pth
BLEU = 16.13, 45.8/22.3/11.5/6.0 (BP=0.987, ratio=0.987, hyp_len=12071, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.74.2.41-11.16.2.35-10.47.pth
BLEU = 15.26, 44.7/21.3/10.7/5.4 (BP=0.996, ratio=0.996, hyp_len=12180, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.75.2.41-11.13.2.33-10.32.pth
BLEU = 15.01, 44.0/20.7/10.4/5.3 (BP=1.000, ratio=1.005, hyp_len=12298, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.76.2.33-10.33.2.33-10.30.pth
BLEU = 15.33, 44.5/21.2/10.7/5.5 (BP=1.000, ratio=1.015, hyp_len=12419, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.77.2.45-11.54.2.32-10.17.pth
BLEU = 16.42, 46.1/22.5/11.5/6.1 (BP=1.000, ratio=1.000, hyp_len=12237, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.78.2.45-11.63.2.31-10.11.pth
BLEU = 16.33, 46.6/22.8/11.8/6.2 (BP=0.979, ratio=0.979, hyp_len=11980, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.79.2.34-10.40.2.31-10.11.pth
BLEU = 14.86, 42.2/20.5/10.4/5.4 (BP=1.000, ratio=1.093, hyp_len=13372, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.80.2.37-10.67.2.31-10.03.pth
BLEU = 16.33, 45.3/22.1/11.5/6.2 (BP=1.000, ratio=1.017, hyp_len=12436, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.81.2.31-10.12.2.29-9.89.pth
BLEU = 17.19, 47.1/23.5/12.4/6.7 (BP=0.987, ratio=0.987, hyp_len=12067, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.82.2.37-10.74.2.28-9.83.pth
BLEU = 16.75, 45.4/22.7/11.9/6.4 (BP=1.000, ratio=1.030, hyp_len=12598, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.83.2.35-10.50.2.29-9.90.pth
BLEU = 16.69, 46.4/22.7/12.1/6.6 (BP=0.982, ratio=0.982, hyp_len=12007, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.84.2.30-9.93.2.28-9.80.pth
BLEU = 17.22, 46.8/23.3/12.4/6.9 (BP=0.985, ratio=0.985, hyp_len=12043, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.85.2.32-10.13.2.29-9.86.pth
BLEU = 16.46, 45.2/22.2/11.6/6.3 (BP=1.000, ratio=1.019, hyp_len=12469, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.86.2.31-10.06.2.27-9.70.pth
BLEU = 17.53, 46.9/23.8/12.6/6.7 (BP=1.000, ratio=1.024, hyp_len=12528, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.87.2.36-10.61.2.27-9.73.pth
BLEU = 16.71, 45.6/22.5/11.8/6.5 (BP=1.000, ratio=1.017, hyp_len=12443, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.88.2.36-10.62.2.28-9.73.pth
BLEU = 16.50, 45.0/22.2/11.7/6.4 (BP=1.000, ratio=1.028, hyp_len=12576, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.89.2.33-10.32.2.27-9.69.pth
BLEU = 17.23, 46.3/23.4/12.3/6.6 (BP=1.000, ratio=1.021, hyp_len=12489, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.90.2.28-9.82.2.26-9.55.pth
BLEU = 18.12, 47.8/24.3/13.1/7.4 (BP=0.989, ratio=0.989, hyp_len=12098, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.91.2.26-9.61.2.26-9.55.pth
BLEU = 18.00, 47.5/24.1/13.0/7.3 (BP=0.991, ratio=0.991, hyp_len=12127, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.92.2.29-9.83.2.25-9.47.pth
BLEU = 18.48, 48.1/24.7/13.4/7.6 (BP=0.990, ratio=0.990, hyp_len=12108, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.93.2.28-9.74.2.25-9.52.pth
BLEU = 18.71, 47.8/24.8/13.6/7.6 (BP=1.000, ratio=1.001, hyp_len=12245, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.94.2.29-9.87.2.24-9.40.pth
BLEU = 18.49, 47.9/24.6/13.5/7.5 (BP=0.994, ratio=0.994, hyp_len=12161, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.95.2.26-9.59.2.24-9.35.pth
BLEU = 18.30, 46.3/24.0/13.3/7.6 (BP=1.000, ratio=1.043, hyp_len=12751, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.96.2.31-10.03.2.23-9.29.pth
BLEU = 17.73, 45.2/23.7/12.9/7.2 (BP=1.000, ratio=1.084, hyp_len=13259, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.97.2.27-9.69.2.22-9.25.pth
BLEU = 18.94, 47.7/24.9/13.7/7.9 (BP=1.000, ratio=1.021, hyp_len=12483, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.98.2.20-9.02.2.23-9.32.pth
BLEU = 19.32, 48.1/25.3/14.0/8.2 (BP=1.000, ratio=1.004, hyp_len=12282, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.99.2.30-9.93.2.23-9.26.pth
BLEU = 19.33, 48.3/25.4/14.1/8.1 (BP=1.000, ratio=1.004, hyp_len=12286, ref_len=12231)
/home/ye/exp/simple-nmt
==========
/home/ye/exp/simple-nmt/model/rl2/rl/transformer/bkmy-70epoch
Evaluation result for the model: transformer-rl-bkmy.100.2.30-10.02.2.26-9.62.pth
BLEU = 17.78, 46.6/23.7/12.6/7.1 (BP=1.000, ratio=1.008, hyp_len=12331, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.70.2.49-12.11.2.41-11.16.pth
BLEU = 14.29, 42.6/20.0/9.7/5.1 (BP=1.000, ratio=1.024, hyp_len=12520, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.71.2.42-11.22.2.41-11.10.pth
BLEU = 13.22, 40.0/18.6/9.0/4.6 (BP=1.000, ratio=1.082, hyp_len=13233, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.72.2.45-11.64.2.40-11.06.pth
BLEU = 14.66, 43.4/20.4/10.2/5.4 (BP=0.986, ratio=0.986, hyp_len=12056, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.73.2.42-11.20.2.40-10.97.pth
BLEU = 13.88, 41.2/19.2/9.5/4.9 (BP=1.000, ratio=1.065, hyp_len=13022, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.74.2.45-11.55.2.39-10.93.pth
BLEU = 13.86, 41.2/19.3/9.4/4.9 (BP=1.000, ratio=1.058, hyp_len=12944, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.75.2.36-10.62.2.39-10.90.pth
BLEU = 13.93, 40.6/19.2/9.6/5.0 (BP=1.000, ratio=1.080, hyp_len=13213, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.76.2.37-10.66.2.38-10.79.pth
BLEU = 14.63, 42.6/20.0/10.1/5.3 (BP=1.000, ratio=1.033, hyp_len=12632, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.77.2.35-10.53.2.37-10.72.pth
BLEU = 14.47, 42.1/20.0/10.0/5.2 (BP=1.000, ratio=1.045, hyp_len=12785, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.78.2.37-10.75.2.37-10.68.pth
BLEU = 14.32, 42.0/19.8/9.9/5.1 (BP=1.000, ratio=1.047, hyp_len=12811, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.79.2.37-10.69.2.36-10.58.pth
BLEU = 15.62, 43.8/21.5/11.0/5.8 (BP=1.000, ratio=1.033, hyp_len=12640, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.80.2.40-11.05.2.36-10.54.pth
BLEU = 14.64, 42.1/20.2/10.1/5.3 (BP=1.000, ratio=1.053, hyp_len=12875, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.81.2.41-11.17.2.35-10.44.pth
BLEU = 15.16, 43.4/20.9/10.5/5.5 (BP=1.000, ratio=1.034, hyp_len=12650, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.82.2.40-11.00.2.35-10.49.pth
BLEU = 14.96, 42.6/20.4/10.4/5.6 (BP=1.000, ratio=1.051, hyp_len=12854, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.83.2.36-10.60.2.35-10.45.pth
BLEU = 15.21, 43.0/20.9/10.6/5.6 (BP=1.000, ratio=1.046, hyp_len=12796, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.84.2.38-10.84.2.34-10.35.pth
BLEU = 15.82, 44.3/21.5/11.0/6.0 (BP=1.000, ratio=1.023, hyp_len=12508, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.85.2.38-10.78.2.33-10.33.pth
BLEU = 15.27, 43.3/21.0/10.6/5.6 (BP=1.000, ratio=1.063, hyp_len=13006, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.86.2.40-11.06.2.33-10.27.pth
BLEU = 15.75, 43.1/21.1/11.1/6.1 (BP=1.000, ratio=1.058, hyp_len=12938, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.87.2.36-10.57.2.32-10.21.pth
BLEU = 15.87, 43.9/21.5/11.0/6.1 (BP=1.000, ratio=1.035, hyp_len=12657, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.88.2.30-10.02.2.33-10.23.pth
BLEU = 15.86, 44.4/21.6/11.0/6.0 (BP=1.000, ratio=1.023, hyp_len=12513, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.89.2.36-10.64.2.32-10.20.pth
BLEU = 16.05, 43.3/21.3/11.3/6.3 (BP=1.000, ratio=1.064, hyp_len=13008, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.90.2.33-10.23.2.32-10.14.pth
BLEU = 16.34, 43.5/21.7/11.5/6.6 (BP=1.000, ratio=1.054, hyp_len=12896, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.91.2.33-10.28.2.31-10.04.pth
BLEU = 17.20, 45.9/22.9/12.1/6.9 (BP=1.000, ratio=1.005, hyp_len=12289, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.92.2.35-10.47.2.30-9.94.pth
BLEU = 17.31, 46.5/23.4/12.3/6.7 (BP=1.000, ratio=1.003, hyp_len=12270, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.93.2.35-10.52.2.30-9.93.pth
BLEU = 17.66, 46.0/23.1/12.5/7.3 (BP=1.000, ratio=1.010, hyp_len=12356, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.94.2.34-10.35.2.29-9.87.pth
BLEU = 17.18, 45.8/23.1/12.2/6.8 (BP=1.000, ratio=1.024, hyp_len=12528, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.95.2.32-10.13.2.29-9.87.pth
BLEU = 17.12, 45.1/22.9/12.2/6.8 (BP=1.000, ratio=1.043, hyp_len=12751, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.96.2.28-9.79.2.28-9.78.pth
BLEU = 18.17, 47.1/24.1/13.0/7.4 (BP=0.999, ratio=0.999, hyp_len=12219, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.97.2.31-10.04.2.28-9.76.pth
BLEU = 18.02, 47.2/24.1/12.9/7.4 (BP=0.994, ratio=0.994, hyp_len=12156, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.98.2.29-9.88.2.27-9.73.pth
BLEU = 18.79, 47.9/24.9/13.7/7.9 (BP=0.990, ratio=0.990, hyp_len=12106, ref_len=12231)
Evaluation result for the model: transformer-rl-bkmy.99.2.30-9.98.2.27-9.70.pth
BLEU = 18.26, 47.0/23.9/13.0/7.6 (BP=1.000, ratio=1.004, hyp_len=12286, ref_len=12231)
/home/ye/exp/simple-nmt
==========
real	169m44.151s
user	146m43.296s
sys	12m28.718s
```

## Transformer-RL Results

**for Myanmar-Beik**

<div align="center"> 
    
Table 1. Best model and best score for each transformer-RL training of my-bk pair  
| No of Epoch for Training | Best Model Epoch | Model File | Best BLEU |
|-----------:|-----------:|:-----------:|-----------:|
| 30-70 | 100 | transformer-rl-mybk.100.2.56-12.97.2.39-10.93.pth | 15.32 |
| 40-60 | 98 | transformer-rl-mybk.98.2.53-12.58.2.39-10.97.pth | 15.61 |
| 50-50 | 98 | transformer-rl-mybk.98.2.55-12.79.2.41-11.17.pth | 15.62 |
| 60-40 | 98 | transformer-rl-mybk.98.2.57-13.06.2.45-11.53.pth | 14.40 |
| 70-30 | 91 | transformer-rl-mybk.91.2.56-12.90.2.45-11.56.pth | 13.75 |

</div>  

**for Beik-Myanmar**

<div align="center"> 
    
Table 2. Best model and best score for each transformer-RL training of bk-my pair 
| No of Epoch for Training | Best Model Epoch | Model File | Best BLEU |
|-----------:|-----------:|:-----------:|-----------:|
| 30-70 | 91 | transformer-rl-bkmy.91.2.32-10.22.2.28-9.77.pth | 18.87 |
| 40-60 | 98 | transformer-rl-bkmy.98.2.28-9.79.2.28-9.75.pth | 17.34 |
| 50-50 | 100 | transformer-rl-bkmy.100.2.27-9.68.2.25-9.49.pth | 18.48 |
| 60-40 | 100 | transformer-rl-bkmy.100.2.24-9.36.2.22-9.18.pth | 19.49 |
| 70-30 | 98 | transformer-rl-bkmy.98.2.29-9.88.2.27-9.73.pth | 18.79 |

</div>  

## Preparation for Drawing Graph

```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/baseline/transformer/mybk-30epoch/eval-results-mybk-transformer-baseline-100epoch.txt ./tran30-mybk.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/baseline/transformer/mybk-40epoch/eval-results-mybk-transformer-baseline-100epoch.txt ./tran40-mybk.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/baseline/transformer/mybk-50epoch/eval-results-mybk-transformer-baseline-100epoch.txt ./tran50-mybk.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/baseline/transformer/mybk-60epoch/eval-results-mybk-transformer-baseline-100epoch.txt ./tran60-mybk.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/baseline/transformer/mybk-70epoch/eval-results-mybk-transformer-baseline-100epoch.txt ./tran70-mybk.txt
```

```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/baseline/transformer/bkmy-30epoch/eval-results-bkmy-transformer-baseline-100epoch.txt ./tran30-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/baseline/transformer/bkmy-40epoch/eval-results-bkmy-transformer-baseline-100epoch.txt ./tran40-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/baseline/transformer/bkmy-50epoch/eval-results-bkmy-transformer-baseline-100epoch.txt ./tran50-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/baseline/transformer/bkmy-60epoch/eval-results-bkmy-transformer-baseline-100epoch.txt ./tran60-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/baseline/transformer/bkmy-70epoch/eval-results-bkmy-transformer-baseline-100epoch.txt ./tran70-bkmy.txt
```

```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/rl/transformer/mybk-30epoch/eval-results-mybk-transformer-RL-100epoch.txt ./tran-rl30-mybk.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/rl/transformer/mybk-40epoch/eval-results-mybk-transformer-RL-100epoch.txt ./tran-rl40-mybk.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/rl/transformer/mybk-50epoch/eval-results-mybk-transformer-RL-100epoch.txt ./tran-rl50-mybk.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/rl/transformer/mybk-60epoch/eval-results-mybk-transformer-RL-100epoch.txt ./tran-rl60-mybk.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/rl/transformer/mybk-70epoch/eval-results-mybk-transformer-RL-100epoch.txt ./tran-rl70-mybk.txt
```

```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/rl/transformer/bkmy-30epoch/eval-results-bkmy-transformer-RL-100epoch.txt ./tran-rl30-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/rl/transformer/bkmy-40epoch/eval-results-bkmy-transformer-RL-100epoch.txt ./tran-rl40-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/rl/transformer/bkmy-50epoch/eval-results-bkmy-transformer-RL-100epoch.txt ./tran-rl50-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/rl/transformer/bkmy-60epoch/eval-results-bkmy-transformer-RL-100epoch.txt ./tran-rl60-bkmy.txt
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ cp ../../../rl2/rl/transformer/bkmy-70epoch/eval-results-bkmy-transformer-RL-100epoch.txt ./tran-rl70-bkmy.txt
```

## BLEU Score Extraction and Drawing Graph

extract မလုပ်ခင်မှာ BLEU score ဖိုင်ကို ဖွင့်ကြည့်ဖို့ လိုအပ်တယ်။ ဘာကြောင့်လဲ ဆိုတော့ 100 epoch က sorting မလုပ်ထားတော့ ဖိုင်ရဲ့ ထိပ်ဆုံးကို ရောက်နေတတ်လို့ ဖိုင်ရဲ့အောက်ဆုံးကို manual ပြန်ရွှေ့ရတာမို့လို့...  

**for my-bk**  

for 30-70:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ ./extract.sh ./tran30-mybk.txt ./tran-rl30-mybk.txt 28
  30   60  390 ./tran30-mybk.txt.bleu
  73  146  989 ./tran-rl30-mybk.txt.bleu
 103  206 1379 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ python ./draw-transformer.py ./tran30-mybk.txt.bleu ./tran-rl30-mybk.txt.bleu "Transformer 30 epochs + RL 70 epochs (my-bk)" transformer_RL-30-70-mybk
```

for 40-60:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ ./extract.sh ./tran40-mybk.txt ./tran-rl40-mybk.txt 40
  40   80  520 ./tran40-mybk.txt.bleu
  60  120  829 ./tran-rl40-mybk.txt.bleu
 100  200 1349 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ python ./draw-transformer.py ./tran40-mybk.txt.bleu ./tran-rl40-mybk.txt.bleu "Transformer 40 epochs + RL 60 epochs (my-bk)" transformer_RL-40-60-mybk
```

for 50-50:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ ./extract.sh ./tran50-mybk.txt ./tran-rl50-mybk.txt 49
  50  100  650 ./tran50-mybk.txt.bleu
  51  102  704 ./tran-rl50-mybk.txt.bleu
 101  202 1354 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ python ./draw-transformer.py ./tran50-mybk.txt.bleu ./tran-rl50-mybk.txt.bleu "Transformer 50 epochs + RL 50 epochs (my-bk)" transformer_RL-50-50-mybk
```

for 60-40:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ ./extract.sh ./tran60-mybk.txt ./tran-rl60-mybk.txt 58
  60  120  782 ./tran60-mybk.txt.bleu
  43   86  597 ./tran-rl60-mybk.txt.bleu
 103  206 1379 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ python ./draw-transformer.py ./tran60-mybk.txt.bleu ./tran-rl60-mybk.txt.bleu "Transformer 60 epochs + RL 40 epochs (my-bk)" transformer_RL-60-40-mybk
```

for 70-30:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ ./extract.sh ./tran70-mybk.txt ./tran-rl70-mybk.txt 70
  70  140  919 ./tran70-mybk.txt.bleu
  31   62  434 ./tran-rl70-mybk.txt.bleu
 101  202 1353 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ python ./draw-transformer.py ./tran70-mybk.txt.bleu ./tran-rl70-mybk.txt.bleu "Transformer 70 epochs + RL 30 epochs (my-bk)" transformer_RL-70-30-mybk
```

**for bk-my**  

for 30-70:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ ./extract.sh ./tran30-bkmy.txt ./tran-rl30-bkmy.txt 30
  30   60  390 ./tran30-bkmy.txt.bleu
  70  140  966 ./tran-rl30-bkmy.txt.bleu
 100  200 1356 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ python ./draw-transformer.py ./tran30-bkmy.txt.bleu ./tran-rl30-bkmy.txt.bleu "Transformer 30 epochs + RL 70 epochs (bk-my)" transformer_RL-30-70-bkmy
```

for 40-60:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ ./extract.sh ./tran40-bkmy.txt ./tran-rl40-bkmy.txt 40
  40   80  520 ./tran40-bkmy.txt.bleu
  60  120  840 ./tran-rl40-bkmy.txt.bleu
 100  200 1360 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ python ./draw-transformer.py ./tran40-bkmy.txt.bleu ./tran-rl40-bkmy.txt.bleu "Transformer 40 epochs + RL 60 epochs (bk-my)" transformer_RL-40-60-bkmy
```

for 50-50:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ ./extract.sh ./tran50-bkmy.txt ./tran-rl50-bkmy.txt 50
  50  100  662 ./tran50-bkmy.txt.bleu
  51  102  714 ./tran-rl50-bkmy.txt.bleu
 101  202 1376 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ python ./draw-transformer.py ./tran50-bkmy.txt.bleu ./tran-rl50-bkmy.txt.bleu "Transformer 50 epochs + RL 50 epochs (bk-my)" transformer_RL-50-50-bkmy
```

for 60-40:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ ./extract.sh ./tran60-bkmy.txt ./tran-rl60-bkmy.txt 60
  60  120  800 ./tran60-bkmy.txt.bleu
  40   80  560 ./tran-rl60-bkmy.txt.bleu
 100  200 1360 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ python ./draw-transformer.py ./tran60-bkmy.txt.bleu ./tran-rl60-bkmy.txt.bleu "Transformer 60 epochs + RL 40 epochs (bk-my)" transformer_RL-60-40-bkmy
```

for 70-30:  
```
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ ./extract.sh ./tran70-bkmy.txt ./tran-rl70-bkmy.txt 70
  70  140  930 ./tran70-bkmy.txt.bleu
  31   62  434 ./tran-rl70-bkmy.txt.bleu
 101  202 1364 total
(base) ye@:~/exp/simple-nmt/model/graph/30-70exp2/tran$ python ./draw-transformer.py ./tran70-bkmy.txt.bleu ./tran-rl70-bkmy.txt.bleu "Transformer 70 epochs + RL 30 epochs (bk-my)" transformer_RL-70-30-bkmy
```

## Graphs

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/seq2seq/seq2seq_RL-30-70-mybk.png" alt="30-70 graph" width="330"/>  
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/seq2seq/seq2seq_RL-40-60-mybk.png" alt="40-60 graph" width="330"/>
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/seq2seq/seq2seq_RL-50-50-mybk.png" alt="50-50 graph" width="330"/>
</p>  
<div align="center">
  Fig.1 BLEU score improvements of Seq2Seq+RL (Minimum Risk Training) for Myanmar-Beik language pair <br />
  (Left: 30-70, Middle: 40-60, Right: 50-50)
</div> 

<br />

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/seq2seq/seq2seq_RL-60-40-mybk.png" alt="60-40 graph" width="500"/>  
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/seq2seq/seq2seq_RL-70-30-mybk.png" alt="70-30 graph" width="500"/>
</p>  
<div align="center">
  Fig.2 BLEU score improvements of Seq2Seq+RL (Minimum Risk Training) for Myanmar-Beik language pair <br />
  (Left: 60-40, Right: 70-30)
</div> 

<br />

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/seq2seq/seq2seq_RL-30-70-bkmy.png" alt="30-70 graph" width="330"/>  
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/seq2seq/seq2seq_RL-40-60-bkmy.png" alt="40-60 graph" width="330"/>
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/seq2seq/seq2seq_RL-50-50-bkmy.png" alt="50-50 graph" width="330"/>
</p>  
<div align="center">
  Fig.3 BLEU score improvements of Seq2Seq+RL (Minimum Risk Training) for Beik-Myanmar language pair <br />
  (Left: 30-70, Middle: 40-60, Right: 50-50)
</div> 

<br />

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/seq2seq/seq2seq_RL-60-40-bkmy.png" alt="60-40 graph" width="500"/>  
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/seq2seq/seq2seq_RL-70-30-bkmy.png" alt="70-30 graph" width="500"/>
</p>  
<div align="center">
  Fig.4 BLEU score improvements of Seq2Seq+RL (Minimum Risk Training) for Beik-Myanmar language pair <br />
  (Left: 60-40, Right: 70-30)
</div> 

<br />

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/transformer/transformer_RL-30-70-mybk.png" alt="30-70 graph" width="330"/>  
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/transformer/transformer_RL-40-60-mybk.png" alt="40-60 graph" width="330"/>
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/transformer/transformer_RL-50-50-mybk.png" alt="50-50 graph" width="330"/>
</p>  
<div align="center">
  Fig.5 BLEU score improvements of Transformer+RL (Minimum Risk Training) for Myanmar-Beik language pair <br />
  (Left: 30-70, Middle: 40-60, Right: 50-50)
</div> 

<br />

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/transformer/transformer_RL-60-40-mybk.png" alt="60-40 graph" width="500"/>  
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/transformer/transformer_RL-70-30-mybk.png" alt="70-30 graph" width="500"/>
</p>  
<div align="center">
  Fig.6 BLEU score improvements of Transformer+RL (Minimum Risk Training) for Myanmar-Beik language pair <br />
  (Left: 60-40, Right: 70-30)
</div> 

<br />

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/transformer/transformer_RL-30-70-bkmy.png" alt="30-70 graph" width="330"/>  
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/transformer/transformer_RL-40-60-bkmy.png" alt="40-60 graph" width="330"/>
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/transformer/transformer_RL-50-50-bkmy.png" alt="50-50 graph" width="330"/>
</p>  
<div align="center">
  Fig.7 BLEU score improvements of Transformer+RL (Minimum Risk Training) for Beik-Myanmar language pair <br /> 
  (Left: 30-70, Middle: 40-60, Right: 50-50)
</div> 

<br />

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/transformer/transformer_RL-60-40-bkmy.png" alt="60-40 graph" width="500"/>  
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/RL-exp/transformer/transformer_RL-70-30-bkmy.png" alt="70-30 graph" width="500"/>
</p>  
<div align="center">
  Fig.8 BLEU score improvements of Transformer+RL (Minimum Risk Training) for Beik-Myanmar language pair <br />
  (Left: 60-40, Right: 70-30)
</div> 

<br />


