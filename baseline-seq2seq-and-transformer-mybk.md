## Preparing Seq2Seq Baseline for my-bk

```
time python train.py --train /home/ye/exp/simple-nmt/data/my-bk/syl/train \
--valid /home/ye/exp/simple-nmt/data/my-bk/syl/dev \
--lang mybk --gpu_id 0 --batch_size 64 --n_epochs 100 \
--max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 \
--n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 \
--use_adam --rl_n_epochs 0 \
--model_fn ./model/seq2seq/baseline/mybk-100epoch/seq-model-mybk.pth | tee ./model/seq2seq/baseline/mybk-100epoch/mybk-seq2seq-baseline-train.log;
```

Training ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/my-bk/syl/train \
> --valid /home/ye/exp/simple-nmt/data/my-bk/syl/dev \
> --lang mybk --gpu_id 0 --batch_size 64 --n_epochs 100 \
> --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 \
> --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 \
> --use_adam --rl_n_epochs 0 \
> --model_fn ./model/seq2seq/baseline/mybk-100epoch/seq-model-mybk.pth | tee ./model/seq2seq/baseline/mybk-100epoch/mybk-seq2seq-baseline-train.log;
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'mybk',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/seq2seq/baseline/mybk-100epoch/seq-model-mybk.pth',
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
  (emb_src): Embedding(1313, 128)
  (emb_dec): Embedding(1470, 128)
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
    (output): Linear(in_features=128, out_features=1470, bias=True)
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
Epoch 1 - |param|=6.00e+02 |g_param|=3.68e+05 loss=4.8847e+00 ppl=132.26                                                
Validation - loss=3.9912e+00 ppl=54.12 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=6.00e+02 |g_param|=2.13e+05 loss=4.4319e+00 ppl=84.09                                                 
Validation - loss=3.9061e+00 ppl=49.71 best_loss=3.9912e+00 best_ppl=54.12                                              
Epoch 3 - |param|=6.00e+02 |g_param|=1.93e+05 loss=4.4190e+00 ppl=83.02                                                 
Validation - loss=3.8484e+00 ppl=46.92 best_loss=3.9061e+00 best_ppl=49.71                                              
Epoch 4 - |param|=6.00e+02 |g_param|=1.93e+05 loss=4.4031e+00 ppl=81.70                                                 
Validation - loss=3.7981e+00 ppl=44.62 best_loss=3.8484e+00 best_ppl=46.92                                              
Epoch 5 - |param|=6.01e+02 |g_param|=2.09e+05 loss=4.3395e+00 ppl=76.67                                                 
Validation - loss=3.8112e+00 ppl=45.21 best_loss=3.7981e+00 best_ppl=44.62                                              
Epoch 6 - |param|=6.01e+02 |g_param|=1.98e+05 loss=4.2578e+00 ppl=70.66                                                 
Validation - loss=3.7586e+00 ppl=42.89 best_loss=3.7981e+00 best_ppl=44.62                                              
Epoch 7 - |param|=6.01e+02 |g_param|=1.82e+05 loss=4.3092e+00 ppl=74.38                                                 
Validation - loss=3.7560e+00 ppl=42.78 best_loss=3.7586e+00 best_ppl=42.89                                              
Epoch 8 - |param|=6.02e+02 |g_param|=1.87e+05 loss=4.2116e+00 ppl=67.47                                                 
Validation - loss=3.7665e+00 ppl=43.23 best_loss=3.7560e+00 best_ppl=42.78                                              
Epoch 9 - |param|=6.02e+02 |g_param|=1.78e+05 loss=4.2098e+00 ppl=67.34                                                 
Validation - loss=3.5981e+00 ppl=36.53 best_loss=3.7560e+00 best_ppl=42.78                                              
Epoch 10 - |param|=6.02e+02 |g_param|=1.51e+05 loss=3.9760e+00 ppl=53.31                                                
Validation - loss=3.4345e+00 ppl=31.02 best_loss=3.5981e+00 best_ppl=36.53                                              
Epoch 11 - |param|=6.03e+02 |g_param|=1.36e+05 loss=3.9056e+00 ppl=49.68                                                
Validation - loss=3.3417e+00 ppl=28.27 best_loss=3.4345e+00 best_ppl=31.02                                              
Epoch 12 - |param|=6.03e+02 |g_param|=1.56e+05 loss=3.8080e+00 ppl=45.06                                                
Validation - loss=3.3313e+00 ppl=27.97 best_loss=3.3417e+00 best_ppl=28.27                                              
Epoch 13 - |param|=6.04e+02 |g_param|=1.41e+05 loss=3.7268e+00 ppl=41.54                                                
Validation - loss=3.2071e+00 ppl=24.71 best_loss=3.3313e+00 best_ppl=27.97                                              
Epoch 14 - |param|=6.04e+02 |g_param|=1.30e+05 loss=3.5885e+00 ppl=36.18                                                
Validation - loss=3.1673e+00 ppl=23.74 best_loss=3.2071e+00 best_ppl=24.71                                              
Epoch 15 - |param|=6.04e+02 |g_param|=1.48e+05 loss=3.5319e+00 ppl=34.19                                                
Validation - loss=3.1191e+00 ppl=22.63 best_loss=3.1673e+00 best_ppl=23.74                                              
Epoch 16 - |param|=6.05e+02 |g_param|=1.41e+05 loss=3.5145e+00 ppl=33.60                                                
Validation - loss=3.0839e+00 ppl=21.84 best_loss=3.1191e+00 best_ppl=22.63                                              
Epoch 17 - |param|=6.05e+02 |g_param|=1.36e+05 loss=3.4093e+00 ppl=30.24                                                
Validation - loss=3.0307e+00 ppl=20.71 best_loss=3.0839e+00 best_ppl=21.84                                              
Epoch 18 - |param|=6.06e+02 |g_param|=1.40e+05 loss=3.4274e+00 ppl=30.80                                                
Validation - loss=2.9462e+00 ppl=19.03 best_loss=3.0307e+00 best_ppl=20.71                                              
Epoch 19 - |param|=6.06e+02 |g_param|=1.47e+05 loss=3.3157e+00 ppl=27.54                                                
Validation - loss=2.9193e+00 ppl=18.53 best_loss=2.9462e+00 best_ppl=19.03                                              
Epoch 20 - |param|=6.07e+02 |g_param|=1.42e+05 loss=3.2020e+00 ppl=24.58                                                
Validation - loss=2.8705e+00 ppl=17.65 best_loss=2.9193e+00 best_ppl=18.53                                              
Epoch 21 - |param|=6.07e+02 |g_param|=1.52e+05 loss=3.3130e+00 ppl=27.47                                                
Validation - loss=2.8244e+00 ppl=16.85 best_loss=2.8705e+00 best_ppl=17.65                                              
Epoch 22 - |param|=6.08e+02 |g_param|=1.57e+05 loss=3.1424e+00 ppl=23.16                                                
Validation - loss=2.8013e+00 ppl=16.47 best_loss=2.8244e+00 best_ppl=16.85                                              
Epoch 23 - |param|=6.08e+02 |g_param|=1.47e+05 loss=3.1791e+00 ppl=24.03                                                
Validation - loss=2.7401e+00 ppl=15.49 best_loss=2.8013e+00 best_ppl=16.47                                              
Epoch 24 - |param|=6.09e+02 |g_param|=1.54e+05 loss=3.0365e+00 ppl=20.83                                                
Validation - loss=2.7312e+00 ppl=15.35 best_loss=2.7401e+00 best_ppl=15.49                                              
Epoch 25 - |param|=6.09e+02 |g_param|=1.66e+05 loss=3.0192e+00 ppl=20.48                                                
Validation - loss=2.6885e+00 ppl=14.71 best_loss=2.7312e+00 best_ppl=15.35                                              
Epoch 26 - |param|=6.10e+02 |g_param|=1.65e+05 loss=2.9609e+00 ppl=19.32                                                
Validation - loss=2.6503e+00 ppl=14.16 best_loss=2.6885e+00 best_ppl=14.71                                              
Epoch 27 - |param|=6.10e+02 |g_param|=1.64e+05 loss=2.8909e+00 ppl=18.01                                                
Validation - loss=2.6182e+00 ppl=13.71 best_loss=2.6503e+00 best_ppl=14.16                                              
Epoch 28 - |param|=6.11e+02 |g_param|=1.65e+05 loss=2.8315e+00 ppl=16.97                                                
Validation - loss=2.6014e+00 ppl=13.48 best_loss=2.6182e+00 best_ppl=13.71                                              
Epoch 29 - |param|=6.11e+02 |g_param|=1.76e+05 loss=2.8137e+00 ppl=16.67                                                
Validation - loss=2.5756e+00 ppl=13.14 best_loss=2.6014e+00 best_ppl=13.48                                              
Epoch 30 - |param|=6.12e+02 |g_param|=1.75e+05 loss=2.7572e+00 ppl=15.76                                                
Validation - loss=2.5096e+00 ppl=12.30 best_loss=2.5756e+00 best_ppl=13.14                                              
Epoch 31 - |param|=6.12e+02 |g_param|=1.71e+05 loss=2.7357e+00 ppl=15.42                                                
Validation - loss=2.4995e+00 ppl=12.18 best_loss=2.5096e+00 best_ppl=12.30                                              
Epoch 32 - |param|=6.13e+02 |g_param|=1.86e+05 loss=2.7333e+00 ppl=15.38                                                
Validation - loss=2.5012e+00 ppl=12.20 best_loss=2.4995e+00 best_ppl=12.18                                              
Epoch 33 - |param|=6.13e+02 |g_param|=1.83e+05 loss=2.7407e+00 ppl=15.50                                                
Validation - loss=2.4543e+00 ppl=11.64 best_loss=2.4995e+00 best_ppl=12.18                                              
Epoch 34 - |param|=6.14e+02 |g_param|=3.08e+05 loss=2.7452e+00 ppl=15.57                                                
Validation - loss=2.4387e+00 ppl=11.46 best_loss=2.4543e+00 best_ppl=11.64                                              
Epoch 35 - |param|=6.14e+02 |g_param|=3.74e+05 loss=2.5367e+00 ppl=12.64                                                
Validation - loss=2.4307e+00 ppl=11.37 best_loss=2.4387e+00 best_ppl=11.46                                              
Epoch 36 - |param|=6.15e+02 |g_param|=4.09e+05 loss=2.6088e+00 ppl=13.58                                                
Validation - loss=2.4044e+00 ppl=11.07 best_loss=2.4307e+00 best_ppl=11.37                                              
Epoch 37 - |param|=6.15e+02 |g_param|=3.78e+05 loss=2.5367e+00 ppl=12.64                                                
Validation - loss=2.4013e+00 ppl=11.04 best_loss=2.4044e+00 best_ppl=11.07                                              
Epoch 38 - |param|=6.16e+02 |g_param|=4.01e+05 loss=2.4546e+00 ppl=11.64                                                
Validation - loss=2.3528e+00 ppl=10.51 best_loss=2.4013e+00 best_ppl=11.04                                              
Epoch 39 - |param|=6.16e+02 |g_param|=3.84e+05 loss=2.4296e+00 ppl=11.35                                                
Validation - loss=2.3511e+00 ppl=10.50 best_loss=2.3528e+00 best_ppl=10.51                                              
Epoch 40 - |param|=6.17e+02 |g_param|=4.41e+05 loss=2.4768e+00 ppl=11.90                                                
Validation - loss=2.3452e+00 ppl=10.44 best_loss=2.3511e+00 best_ppl=10.50                                              
Epoch 41 - |param|=6.17e+02 |g_param|=4.09e+05 loss=2.3921e+00 ppl=10.94                                                
Validation - loss=2.3276e+00 ppl=10.25 best_loss=2.3452e+00 best_ppl=10.44                                              
Epoch 42 - |param|=6.18e+02 |g_param|=4.30e+05 loss=2.3172e+00 ppl=10.15                                                
Validation - loss=2.3063e+00 ppl=10.04 best_loss=2.3276e+00 best_ppl=10.25                                              
Epoch 43 - |param|=6.18e+02 |g_param|=4.15e+05 loss=2.2757e+00 ppl=9.73                                                 
Validation - loss=2.2682e+00 ppl=9.66 best_loss=2.3063e+00 best_ppl=10.04                                               
Epoch 44 - |param|=6.19e+02 |g_param|=4.36e+05 loss=2.2608e+00 ppl=9.59                                                 
Validation - loss=2.2564e+00 ppl=9.55 best_loss=2.2682e+00 best_ppl=9.66                                                
Epoch 45 - |param|=6.19e+02 |g_param|=4.29e+05 loss=2.2201e+00 ppl=9.21                                                 
Validation - loss=2.2499e+00 ppl=9.49 best_loss=2.2564e+00 best_ppl=9.55                                                
Epoch 46 - |param|=6.20e+02 |g_param|=4.41e+05 loss=2.2630e+00 ppl=9.61                                                 
Validation - loss=2.2434e+00 ppl=9.43 best_loss=2.2499e+00 best_ppl=9.49                                                
Epoch 47 - |param|=6.20e+02 |g_param|=4.26e+05 loss=2.1737e+00 ppl=8.79                                                 
Validation - loss=2.2438e+00 ppl=9.43 best_loss=2.2434e+00 best_ppl=9.43                                                
Epoch 48 - |param|=6.21e+02 |g_param|=4.46e+05 loss=2.1663e+00 ppl=8.73                                                 
Validation - loss=2.2317e+00 ppl=9.32 best_loss=2.2434e+00 best_ppl=9.43                                                
Epoch 49 - |param|=6.21e+02 |g_param|=4.60e+05 loss=2.2373e+00 ppl=9.37                                                 
Validation - loss=2.2309e+00 ppl=9.31 best_loss=2.2317e+00 best_ppl=9.32                                                
Epoch 50 - |param|=6.21e+02 |g_param|=4.78e+05 loss=2.0766e+00 ppl=7.98                                                 
Validation - loss=2.2172e+00 ppl=9.18 best_loss=2.2309e+00 best_ppl=9.31                                                
Epoch 51 - |param|=6.22e+02 |g_param|=4.64e+05 loss=2.1115e+00 ppl=8.26                                                 
Validation - loss=2.1917e+00 ppl=8.95 best_loss=2.2172e+00 best_ppl=9.18                                                
Epoch 52 - |param|=6.22e+02 |g_param|=3.16e+05 loss=2.0447e+00 ppl=7.73                                                 
Validation - loss=2.1993e+00 ppl=9.02 best_loss=2.1917e+00 best_ppl=8.95                                                
Epoch 53 - |param|=6.23e+02 |g_param|=2.44e+05 loss=2.1060e+00 ppl=8.22                                                 
Validation - loss=2.1833e+00 ppl=8.88 best_loss=2.1917e+00 best_ppl=8.95                                                
Epoch 54 - |param|=6.23e+02 |g_param|=2.49e+05 loss=2.0980e+00 ppl=8.15                                                 
Validation - loss=2.1714e+00 ppl=8.77 best_loss=2.1833e+00 best_ppl=8.88                                                
Epoch 55 - |param|=6.24e+02 |g_param|=2.42e+05 loss=2.0184e+00 ppl=7.53                                                 
Validation - loss=2.1783e+00 ppl=8.83 best_loss=2.1714e+00 best_ppl=8.77                                                
Epoch 56 - |param|=6.24e+02 |g_param|=2.52e+05 loss=1.9295e+00 ppl=6.89                                                 
Validation - loss=2.1569e+00 ppl=8.64 best_loss=2.1714e+00 best_ppl=8.77                                                
Epoch 57 - |param|=6.24e+02 |g_param|=2.41e+05 loss=1.9127e+00 ppl=6.77                                                 
Validation - loss=2.1758e+00 ppl=8.81 best_loss=2.1569e+00 best_ppl=8.64                                                
Epoch 58 - |param|=6.25e+02 |g_param|=2.51e+05 loss=1.9355e+00 ppl=6.93                                                 
Validation - loss=2.1450e+00 ppl=8.54 best_loss=2.1569e+00 best_ppl=8.64                                                
Epoch 59 - |param|=6.25e+02 |g_param|=2.58e+05 loss=1.9021e+00 ppl=6.70                                                 
Validation - loss=2.1600e+00 ppl=8.67 best_loss=2.1450e+00 best_ppl=8.54                                                
Epoch 60 - |param|=6.26e+02 |g_param|=2.62e+05 loss=1.8278e+00 ppl=6.22                                                 
Validation - loss=2.1591e+00 ppl=8.66 best_loss=2.1450e+00 best_ppl=8.54                                                
Epoch 61 - |param|=6.26e+02 |g_param|=2.55e+05 loss=1.8550e+00 ppl=6.39                                                 
Validation - loss=2.1725e+00 ppl=8.78 best_loss=2.1450e+00 best_ppl=8.54                                                
Epoch 62 - |param|=6.27e+02 |g_param|=2.60e+05 loss=1.8426e+00 ppl=6.31                                                 
Validation - loss=2.1727e+00 ppl=8.78 best_loss=2.1450e+00 best_ppl=8.54                                                
Epoch 63 - |param|=6.27e+02 |g_param|=2.74e+05 loss=1.8057e+00 ppl=6.08                                                 
Validation - loss=2.1686e+00 ppl=8.75 best_loss=2.1450e+00 best_ppl=8.54                                                
Epoch 64 - |param|=6.27e+02 |g_param|=2.63e+05 loss=1.8236e+00 ppl=6.19                                                 
Validation - loss=2.1572e+00 ppl=8.65 best_loss=2.1450e+00 best_ppl=8.54                                                
Epoch 65 - |param|=6.28e+02 |g_param|=2.55e+05 loss=1.7674e+00 ppl=5.86                                                 
Validation - loss=2.1692e+00 ppl=8.75 best_loss=2.1450e+00 best_ppl=8.54                                                
Epoch 66 - |param|=6.28e+02 |g_param|=2.91e+05 loss=1.8138e+00 ppl=6.13                                                 
Validation - loss=2.1688e+00 ppl=8.75 best_loss=2.1450e+00 best_ppl=8.54                                                
Epoch 67 - |param|=6.29e+02 |g_param|=2.76e+05 loss=1.7398e+00 ppl=5.70                                                 
Validation - loss=2.1829e+00 ppl=8.87 best_loss=2.1450e+00 best_ppl=8.54                                                
Epoch 68 - |param|=6.29e+02 |g_param|=2.67e+05 loss=1.6733e+00 ppl=5.33                                                 
Validation - loss=2.1555e+00 ppl=8.63 best_loss=2.1450e+00 best_ppl=8.54                                                
Epoch 69 - |param|=6.29e+02 |g_param|=2.71e+05 loss=1.7312e+00 ppl=5.65                                                 
Validation - loss=2.1464e+00 ppl=8.55 best_loss=2.1450e+00 best_ppl=8.54                                                
Epoch 70 - |param|=6.30e+02 |g_param|=2.98e+05 loss=1.7052e+00 ppl=5.50                                                 
Validation - loss=2.1521e+00 ppl=8.60 best_loss=2.1450e+00 best_ppl=8.54                                                
Epoch 71 - |param|=6.30e+02 |g_param|=2.78e+05 loss=1.6688e+00 ppl=5.31                                                 
Validation - loss=2.1435e+00 ppl=8.53 best_loss=2.1450e+00 best_ppl=8.54                                                
Epoch 72 - |param|=6.31e+02 |g_param|=3.02e+05 loss=1.5945e+00 ppl=4.93                                                 
Validation - loss=2.1285e+00 ppl=8.40 best_loss=2.1435e+00 best_ppl=8.53                                                
Epoch 73 - |param|=6.31e+02 |g_param|=2.67e+05 loss=1.5604e+00 ppl=4.76                                                 
Validation - loss=2.1416e+00 ppl=8.51 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 74 - |param|=6.31e+02 |g_param|=3.00e+05 loss=1.6528e+00 ppl=5.22                                                 
Validation - loss=2.1513e+00 ppl=8.60 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 75 - |param|=6.32e+02 |g_param|=2.71e+05 loss=1.5535e+00 ppl=4.73                                                 
Validation - loss=2.1501e+00 ppl=8.59 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 76 - |param|=6.32e+02 |g_param|=2.83e+05 loss=1.5215e+00 ppl=4.58                                                 
Validation - loss=2.1412e+00 ppl=8.51 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 77 - |param|=6.33e+02 |g_param|=2.87e+05 loss=1.5607e+00 ppl=4.76                                                 
Validation - loss=2.1472e+00 ppl=8.56 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 78 - |param|=6.33e+02 |g_param|=2.73e+05 loss=1.5225e+00 ppl=4.58                                                 
Validation - loss=2.1341e+00 ppl=8.45 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 79 - |param|=6.33e+02 |g_param|=2.79e+05 loss=1.4797e+00 ppl=4.39                                                 
Validation - loss=2.1473e+00 ppl=8.56 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 80 - |param|=6.34e+02 |g_param|=2.88e+05 loss=1.4810e+00 ppl=4.40                                                 
Validation - loss=2.1311e+00 ppl=8.42 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 81 - |param|=6.34e+02 |g_param|=2.83e+05 loss=1.4861e+00 ppl=4.42                                                 
Validation - loss=2.1551e+00 ppl=8.63 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 82 - |param|=6.35e+02 |g_param|=3.03e+05 loss=1.4258e+00 ppl=4.16                                                 
Validation - loss=2.1580e+00 ppl=8.65 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 83 - |param|=6.35e+02 |g_param|=2.90e+05 loss=1.5242e+00 ppl=4.59                                                 
Validation - loss=2.1704e+00 ppl=8.76 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 84 - |param|=6.35e+02 |g_param|=3.13e+05 loss=1.4995e+00 ppl=4.48                                                 
Validation - loss=2.1442e+00 ppl=8.54 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 85 - |param|=6.36e+02 |g_param|=5.53e+05 loss=1.3794e+00 ppl=3.97                                                 
Validation - loss=2.1732e+00 ppl=8.79 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 86 - |param|=6.36e+02 |g_param|=5.88e+05 loss=1.4002e+00 ppl=4.06                                                 
Validation - loss=2.1533e+00 ppl=8.61 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 87 - |param|=6.36e+02 |g_param|=5.98e+05 loss=1.4083e+00 ppl=4.09                                                 
Validation - loss=2.1718e+00 ppl=8.77 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 88 - |param|=6.37e+02 |g_param|=6.18e+05 loss=1.3667e+00 ppl=3.92                                                 
Validation - loss=2.1577e+00 ppl=8.65 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 89 - |param|=6.37e+02 |g_param|=5.85e+05 loss=1.3355e+00 ppl=3.80                                                 
Validation - loss=2.1871e+00 ppl=8.91 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 90 - |param|=6.38e+02 |g_param|=3.75e+05 loss=1.3921e+00 ppl=4.02                                                 
Validation - loss=2.1766e+00 ppl=8.82 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 91 - |param|=6.38e+02 |g_param|=3.14e+05 loss=1.3035e+00 ppl=3.68                                                 
Validation - loss=2.1925e+00 ppl=8.96 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 92 - |param|=6.38e+02 |g_param|=3.29e+05 loss=1.4372e+00 ppl=4.21                                                 
Validation - loss=2.1887e+00 ppl=8.92 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 93 - |param|=6.39e+02 |g_param|=2.87e+05 loss=1.3602e+00 ppl=3.90                                                 
Validation - loss=2.2394e+00 ppl=9.39 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 94 - |param|=6.39e+02 |g_param|=3.00e+05 loss=1.2862e+00 ppl=3.62                                                 
Validation - loss=2.2120e+00 ppl=9.13 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 95 - |param|=6.39e+02 |g_param|=2.89e+05 loss=1.2895e+00 ppl=3.63                                                 
Validation - loss=2.1923e+00 ppl=8.96 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 96 - |param|=6.40e+02 |g_param|=3.09e+05 loss=1.2928e+00 ppl=3.64                                                 
Validation - loss=2.1806e+00 ppl=8.85 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 97 - |param|=6.40e+02 |g_param|=3.02e+05 loss=1.2316e+00 ppl=3.43                                                 
Validation - loss=2.2252e+00 ppl=9.26 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 98 - |param|=6.41e+02 |g_param|=3.32e+05 loss=1.2626e+00 ppl=3.53                                                 
Validation - loss=2.2358e+00 ppl=9.35 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 99 - |param|=6.41e+02 |g_param|=3.09e+05 loss=1.2150e+00 ppl=3.37                                                 
Validation - loss=2.1874e+00 ppl=8.91 best_loss=2.1285e+00 best_ppl=8.40                                                
Epoch 100 - |param|=6.41e+02 |g_param|=3.05e+05 loss=1.1864e+00 ppl=3.28                                                
Validation - loss=2.2291e+00 ppl=9.29 best_loss=2.1285e+00 best_ppl=8.40                                                

real	12m35.119s
user	12m21.197s
sys	0m11.927s
```

Updating testing/evaluation bash script ...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, Thailand
# find all models and parse to translate.py for testing and multi-bleu.perl for evaluation with BLEU score
# updated for my-bk

cd ./model/seq2seq/baseline/mybk-100epoch;

for i in *.pth; do
   MODEL=$i;

   # Testing
   python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang mybk < /home/ye/exp/simple-nmt/data/my-bk/syl/test.my > $MODEL.hyp

   # Evaluation with BLEU Score
   echo "Evaluation result for the model: $MODEL" | tee -a eval-results-mybk-seq2seq-baseline-100epoch.txt;
   cat $MODEL.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/my-bk/syl/test.bk | tee  -a eval-results-mybk-seq2seq-baseline-100epoch.txt;

done

cd -;
```

Testing/Evaluation

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-loop-seq2seq-mybk.sh 
Evaluation result for the model: seq-model-mybk.01.4.88-132.26.3.99-54.12.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.2/0.0/0.0/0.0 (BP=0.712, ratio=0.747, hyp_len=8537, ref_len=11432)
Evaluation result for the model: seq-model-mybk.02.4.43-84.09.3.91-49.71.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.7/0.2/0.0/0.0 (BP=0.960, ratio=0.961, hyp_len=10986, ref_len=11432)
Evaluation result for the model: seq-model-mybk.03.4.42-83.02.3.85-46.92.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.1/0.2/0.0/0.0 (BP=1.000, ratio=1.019, hyp_len=11646, ref_len=11432)
Evaluation result for the model: seq-model-mybk.04.4.40-81.70.3.80-44.62.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.4/0.2/0.0/0.0 (BP=1.000, ratio=1.040, hyp_len=11893, ref_len=11432)
Evaluation result for the model: seq-model-mybk.05.4.34-76.67.3.81-45.21.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.3/0.2/0.0/0.0 (BP=1.000, ratio=1.020, hyp_len=11658, ref_len=11432)
Evaluation result for the model: seq-model-mybk.06.4.26-70.66.3.76-42.89.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.4/0.3/0.0/0.0 (BP=1.000, ratio=1.025, hyp_len=11723, ref_len=11432)
Evaluation result for the model: seq-model-mybk.07.4.31-74.38.3.76-42.78.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.4/0.1/0.0/0.0 (BP=1.000, ratio=1.021, hyp_len=11675, ref_len=11432)
Evaluation result for the model: seq-model-mybk.08.4.21-67.47.3.77-43.23.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.1/0.2/0.0/0.0 (BP=1.000, ratio=1.039, hyp_len=11873, ref_len=11432)
Evaluation result for the model: seq-model-mybk.09.4.21-67.34.3.60-36.53.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 23.5/0.2/0.0/0.0 (BP=0.750, ratio=0.776, hyp_len=8874, ref_len=11432)
Evaluation result for the model: seq-model-mybk.100.1.19-3.28.2.23-9.29.pth
BLEU = 17.84, 44.1/22.2/13.0/8.0 (BP=1.000, ratio=1.126, hyp_len=12868, ref_len=11432)
Evaluation result for the model: seq-model-mybk.10.3.98-53.31.3.43-31.02.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 26.0/1.2/0.0/0.0 (BP=0.730, ratio=0.761, hyp_len=8695, ref_len=11432)
Evaluation result for the model: seq-model-mybk.11.3.91-49.68.3.34-28.27.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 22.6/2.9/0.2/0.0 (BP=0.999, ratio=0.999, hyp_len=11425, ref_len=11432)
Evaluation result for the model: seq-model-mybk.12.3.81-45.06.3.33-27.97.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 26.0/3.7/0.3/0.0 (BP=0.943, ratio=0.945, hyp_len=10802, ref_len=11432)
Evaluation result for the model: seq-model-mybk.13.3.73-41.54.3.21-24.71.pth
BLEU = 1.73, 24.8/4.0/0.8/0.1 (BP=1.000, ratio=1.023, hyp_len=11692, ref_len=11432)
Evaluation result for the model: seq-model-mybk.14.3.59-36.18.3.17-23.74.pth
BLEU = 3.25, 22.7/5.5/1.6/0.6 (BP=1.000, ratio=1.169, hyp_len=13366, ref_len=11432)
Evaluation result for the model: seq-model-mybk.15.3.53-34.19.3.12-22.63.pth
BLEU = 3.11, 20.5/5.0/1.6/0.6 (BP=1.000, ratio=1.294, hyp_len=14792, ref_len=11432)
Evaluation result for the model: seq-model-mybk.16.3.51-33.60.3.08-21.84.pth
BLEU = 0.76, 4.9/1.2/0.4/0.1 (BP=1.000, ratio=5.088, hyp_len=58168, ref_len=11432)
Evaluation result for the model: seq-model-mybk.17.3.41-30.24.3.03-20.71.pth
BLEU = 3.89, 22.8/6.0/2.1/0.8 (BP=1.000, ratio=1.231, hyp_len=14078, ref_len=11432)
Evaluation result for the model: seq-model-mybk.18.3.43-30.80.2.95-19.03.pth
BLEU = 4.47, 25.7/7.0/2.5/0.9 (BP=1.000, ratio=1.127, hyp_len=12886, ref_len=11432)
Evaluation result for the model: seq-model-mybk.19.3.32-27.54.2.92-18.53.pth
BLEU = 4.67, 25.2/7.1/2.6/1.0 (BP=1.000, ratio=1.161, hyp_len=13278, ref_len=11432)
Evaluation result for the model: seq-model-mybk.20.3.20-24.58.2.87-17.65.pth
BLEU = 5.54, 26.8/8.0/3.2/1.4 (BP=1.000, ratio=1.122, hyp_len=12832, ref_len=11432)
Evaluation result for the model: seq-model-mybk.21.3.31-27.47.2.82-16.85.pth
BLEU = 5.34, 26.6/7.9/3.1/1.2 (BP=1.000, ratio=1.141, hyp_len=13045, ref_len=11432)
Evaluation result for the model: seq-model-mybk.22.3.14-23.16.2.80-16.47.pth
BLEU = 4.17, 19.8/6.1/2.5/1.0 (BP=1.000, ratio=1.571, hyp_len=17958, ref_len=11432)
Evaluation result for the model: seq-model-mybk.23.3.18-24.03.2.74-15.49.pth
BLEU = 6.30, 28.7/9.2/3.8/1.6 (BP=1.000, ratio=1.124, hyp_len=12854, ref_len=11432)
Evaluation result for the model: seq-model-mybk.24.3.04-20.83.2.73-15.35.pth
BLEU = 6.02, 28.3/8.8/3.6/1.5 (BP=1.000, ratio=1.129, hyp_len=12910, ref_len=11432)
Evaluation result for the model: seq-model-mybk.25.3.02-20.48.2.69-14.71.pth
BLEU = 6.64, 30.1/9.7/4.0/1.7 (BP=1.000, ratio=1.090, hyp_len=12466, ref_len=11432)
Evaluation result for the model: seq-model-mybk.26.2.96-19.32.2.65-14.16.pth
BLEU = 6.65, 29.4/9.8/4.0/1.7 (BP=1.000, ratio=1.121, hyp_len=12817, ref_len=11432)
Evaluation result for the model: seq-model-mybk.27.2.89-18.01.2.62-13.71.pth
BLEU = 7.21, 30.5/10.4/4.4/1.9 (BP=1.000, ratio=1.126, hyp_len=12871, ref_len=11432)
Evaluation result for the model: seq-model-mybk.28.2.83-16.97.2.60-13.48.pth
BLEU = 7.01, 29.3/10.0/4.3/1.9 (BP=1.000, ratio=1.150, hyp_len=13142, ref_len=11432)
Evaluation result for the model: seq-model-mybk.29.2.81-16.67.2.58-13.14.pth
BLEU = 7.23, 30.1/10.6/4.4/2.0 (BP=1.000, ratio=1.159, hyp_len=13249, ref_len=11432)
Evaluation result for the model: seq-model-mybk.30.2.76-15.76.2.51-12.30.pth
BLEU = 8.57, 32.6/12.1/5.4/2.5 (BP=1.000, ratio=1.092, hyp_len=12486, ref_len=11432)
Evaluation result for the model: seq-model-mybk.31.2.74-15.42.2.50-12.18.pth
BLEU = 8.21, 32.0/11.7/5.2/2.4 (BP=1.000, ratio=1.107, hyp_len=12656, ref_len=11432)
Evaluation result for the model: seq-model-mybk.32.2.73-15.38.2.50-12.20.pth
BLEU = 8.59, 32.7/12.1/5.4/2.6 (BP=1.000, ratio=1.091, hyp_len=12476, ref_len=11432)
Evaluation result for the model: seq-model-mybk.33.2.74-15.50.2.45-11.64.pth
BLEU = 9.19, 33.6/12.6/5.8/2.9 (BP=1.000, ratio=1.111, hyp_len=12701, ref_len=11432)
Evaluation result for the model: seq-model-mybk.34.2.75-15.57.2.44-11.46.pth
BLEU = 9.63, 34.3/13.3/6.2/3.0 (BP=1.000, ratio=1.098, hyp_len=12551, ref_len=11432)
Evaluation result for the model: seq-model-mybk.35.2.54-12.64.2.43-11.37.pth
BLEU = 9.76, 35.4/13.8/6.3/3.0 (BP=1.000, ratio=1.066, hyp_len=12184, ref_len=11432)
Evaluation result for the model: seq-model-mybk.36.2.61-13.58.2.40-11.07.pth
BLEU = 10.66, 36.3/14.5/6.9/3.5 (BP=1.000, ratio=1.070, hyp_len=12227, ref_len=11432)
Evaluation result for the model: seq-model-mybk.37.2.54-12.64.2.40-11.04.pth
BLEU = 9.60, 33.5/13.3/6.3/3.1 (BP=1.000, ratio=1.163, hyp_len=13295, ref_len=11432)
Evaluation result for the model: seq-model-mybk.38.2.45-11.64.2.35-10.51.pth
BLEU = 10.84, 36.1/14.6/7.2/3.6 (BP=1.000, ratio=1.072, hyp_len=12250, ref_len=11432)
Evaluation result for the model: seq-model-mybk.39.2.43-11.35.2.35-10.50.pth
BLEU = 10.92, 36.4/14.7/7.2/3.7 (BP=1.000, ratio=1.077, hyp_len=12315, ref_len=11432)
Evaluation result for the model: seq-model-mybk.40.2.48-11.90.2.35-10.44.pth
BLEU = 11.48, 36.2/15.1/7.7/4.1 (BP=1.000, ratio=1.098, hyp_len=12550, ref_len=11432)
Evaluation result for the model: seq-model-mybk.41.2.39-10.94.2.33-10.25.pth
BLEU = 11.24, 36.0/15.3/7.6/3.8 (BP=1.000, ratio=1.111, hyp_len=12702, ref_len=11432)
Evaluation result for the model: seq-model-mybk.42.2.32-10.15.2.31-10.04.pth
BLEU = 11.06, 35.9/14.8/7.3/3.8 (BP=1.000, ratio=1.084, hyp_len=12387, ref_len=11432)
Evaluation result for the model: seq-model-mybk.43.2.28-9.73.2.27-9.66.pth
BLEU = 12.15, 37.9/16.0/8.2/4.4 (BP=1.000, ratio=1.063, hyp_len=12152, ref_len=11432)
Evaluation result for the model: seq-model-mybk.44.2.26-9.59.2.26-9.55.pth
BLEU = 13.48, 39.4/17.8/9.2/5.1 (BP=1.000, ratio=1.062, hyp_len=12144, ref_len=11432)
Evaluation result for the model: seq-model-mybk.45.2.22-9.21.2.25-9.49.pth
BLEU = 13.33, 39.8/17.9/9.3/4.8 (BP=1.000, ratio=1.086, hyp_len=12417, ref_len=11432)
Evaluation result for the model: seq-model-mybk.46.2.26-9.61.2.24-9.43.pth
BLEU = 13.44, 39.7/17.6/9.3/5.0 (BP=1.000, ratio=1.075, hyp_len=12289, ref_len=11432)
Evaluation result for the model: seq-model-mybk.47.2.17-8.79.2.24-9.43.pth
BLEU = 12.77, 38.2/17.0/8.7/4.7 (BP=1.000, ratio=1.123, hyp_len=12834, ref_len=11432)
Evaluation result for the model: seq-model-mybk.48.2.17-8.73.2.23-9.32.pth
BLEU = 13.20, 38.3/17.1/9.1/5.1 (BP=1.000, ratio=1.118, hyp_len=12779, ref_len=11432)
Evaluation result for the model: seq-model-mybk.49.2.24-9.37.2.23-9.31.pth
BLEU = 12.66, 38.2/16.8/8.7/4.6 (BP=1.000, ratio=1.077, hyp_len=12312, ref_len=11432)
Evaluation result for the model: seq-model-mybk.50.2.08-7.98.2.22-9.18.pth
BLEU = 13.78, 39.5/18.2/9.6/5.2 (BP=1.000, ratio=1.120, hyp_len=12807, ref_len=11432)
Evaluation result for the model: seq-model-mybk.51.2.11-8.26.2.19-8.95.pth
BLEU = 14.01, 40.3/18.2/9.7/5.4 (BP=1.000, ratio=1.097, hyp_len=12542, ref_len=11432)
Evaluation result for the model: seq-model-mybk.52.2.04-7.73.2.20-9.02.pth
BLEU = 14.62, 41.2/19.2/10.2/5.7 (BP=1.000, ratio=1.075, hyp_len=12295, ref_len=11432)
Evaluation result for the model: seq-model-mybk.53.2.11-8.22.2.18-8.88.pth
BLEU = 15.10, 41.7/19.4/10.6/6.0 (BP=1.000, ratio=1.067, hyp_len=12195, ref_len=11432)
Evaluation result for the model: seq-model-mybk.54.2.10-8.15.2.17-8.77.pth
BLEU = 14.68, 40.6/18.9/10.3/5.9 (BP=1.000, ratio=1.089, hyp_len=12445, ref_len=11432)
Evaluation result for the model: seq-model-mybk.55.2.02-7.53.2.18-8.83.pth
BLEU = 14.46, 40.9/18.9/10.1/5.6 (BP=1.000, ratio=1.097, hyp_len=12541, ref_len=11432)
Evaluation result for the model: seq-model-mybk.56.1.93-6.89.2.16-8.64.pth
BLEU = 15.63, 41.9/20.1/11.1/6.4 (BP=1.000, ratio=1.096, hyp_len=12530, ref_len=11432)
Evaluation result for the model: seq-model-mybk.57.1.91-6.77.2.18-8.81.pth
BLEU = 15.07, 41.4/19.4/10.6/6.0 (BP=1.000, ratio=1.092, hyp_len=12488, ref_len=11432)
Evaluation result for the model: seq-model-mybk.58.1.94-6.93.2.14-8.54.pth
BLEU = 16.40, 44.3/21.2/11.7/6.6 (BP=1.000, ratio=1.056, hyp_len=12076, ref_len=11432)
Evaluation result for the model: seq-model-mybk.59.1.90-6.70.2.16-8.67.pth
BLEU = 16.11, 42.7/20.6/11.5/6.7 (BP=1.000, ratio=1.071, hyp_len=12246, ref_len=11432)
Evaluation result for the model: seq-model-mybk.60.1.83-6.22.2.16-8.66.pth
BLEU = 15.76, 42.4/20.2/11.2/6.4 (BP=1.000, ratio=1.107, hyp_len=12654, ref_len=11432)
Evaluation result for the model: seq-model-mybk.61.1.86-6.39.2.17-8.78.pth
BLEU = 15.78, 41.7/20.0/11.2/6.6 (BP=1.000, ratio=1.107, hyp_len=12658, ref_len=11432)
Evaluation result for the model: seq-model-mybk.62.1.84-6.31.2.17-8.78.pth
BLEU = 15.59, 42.2/20.1/11.2/6.2 (BP=1.000, ratio=1.084, hyp_len=12387, ref_len=11432)
Evaluation result for the model: seq-model-mybk.63.1.81-6.08.2.17-8.75.pth
BLEU = 15.82, 42.0/20.5/11.4/6.4 (BP=1.000, ratio=1.101, hyp_len=12591, ref_len=11432)
Evaluation result for the model: seq-model-mybk.64.1.82-6.19.2.16-8.65.pth
BLEU = 15.78, 42.7/20.3/11.2/6.4 (BP=1.000, ratio=1.098, hyp_len=12549, ref_len=11432)
Evaluation result for the model: seq-model-mybk.65.1.77-5.86.2.17-8.75.pth
BLEU = 16.14, 43.1/20.8/11.5/6.6 (BP=1.000, ratio=1.073, hyp_len=12266, ref_len=11432)
Evaluation result for the model: seq-model-mybk.66.1.81-6.13.2.17-8.75.pth
BLEU = 15.46, 41.6/19.7/10.9/6.4 (BP=1.000, ratio=1.114, hyp_len=12736, ref_len=11432)
Evaluation result for the model: seq-model-mybk.67.1.74-5.70.2.18-8.87.pth
BLEU = 16.31, 42.4/20.8/11.8/6.8 (BP=1.000, ratio=1.087, hyp_len=12430, ref_len=11432)
Evaluation result for the model: seq-model-mybk.68.1.67-5.33.2.16-8.63.pth
BLEU = 17.07, 44.2/22.0/12.3/7.1 (BP=1.000, ratio=1.081, hyp_len=12360, ref_len=11432)
Evaluation result for the model: seq-model-mybk.69.1.73-5.65.2.15-8.55.pth
BLEU = 17.03, 43.8/21.6/12.3/7.2 (BP=1.000, ratio=1.096, hyp_len=12525, ref_len=11432)
Evaluation result for the model: seq-model-mybk.70.1.71-5.50.2.15-8.60.pth
BLEU = 16.92, 43.2/21.3/12.2/7.3 (BP=1.000, ratio=1.095, hyp_len=12519, ref_len=11432)
Evaluation result for the model: seq-model-mybk.71.1.67-5.31.2.14-8.53.pth
BLEU = 17.30, 44.5/22.1/12.5/7.3 (BP=1.000, ratio=1.084, hyp_len=12387, ref_len=11432)
Evaluation result for the model: seq-model-mybk.72.1.59-4.93.2.13-8.40.pth
BLEU = 17.62, 45.0/22.4/12.8/7.5 (BP=1.000, ratio=1.083, hyp_len=12379, ref_len=11432)
Evaluation result for the model: seq-model-mybk.73.1.56-4.76.2.14-8.51.pth
BLEU = 17.80, 44.4/22.3/12.9/7.9 (BP=1.000, ratio=1.083, hyp_len=12379, ref_len=11432)
Evaluation result for the model: seq-model-mybk.74.1.65-5.22.2.15-8.60.pth
BLEU = 17.70, 43.7/22.0/12.9/7.9 (BP=1.000, ratio=1.097, hyp_len=12538, ref_len=11432)
Evaluation result for the model: seq-model-mybk.75.1.55-4.73.2.15-8.59.pth
BLEU = 17.51, 44.7/22.1/12.7/7.5 (BP=1.000, ratio=1.078, hyp_len=12326, ref_len=11432)
Evaluation result for the model: seq-model-mybk.76.1.52-4.58.2.14-8.51.pth
BLEU = 18.09, 45.2/22.9/13.2/7.8 (BP=1.000, ratio=1.074, hyp_len=12282, ref_len=11432)
Evaluation result for the model: seq-model-mybk.77.1.56-4.76.2.15-8.56.pth
BLEU = 17.31, 43.8/21.8/12.6/7.5 (BP=1.000, ratio=1.103, hyp_len=12607, ref_len=11432)
Evaluation result for the model: seq-model-mybk.78.1.52-4.58.2.13-8.45.pth
BLEU = 17.22, 44.3/21.9/12.4/7.3 (BP=1.000, ratio=1.095, hyp_len=12520, ref_len=11432)
Evaluation result for the model: seq-model-mybk.79.1.48-4.39.2.15-8.56.pth
BLEU = 17.70, 44.5/22.2/12.8/7.7 (BP=1.000, ratio=1.086, hyp_len=12414, ref_len=11432)
Evaluation result for the model: seq-model-mybk.80.1.48-4.40.2.13-8.42.pth
BLEU = 18.64, 46.3/23.6/13.7/8.1 (BP=1.000, ratio=1.072, hyp_len=12252, ref_len=11432)
Evaluation result for the model: seq-model-mybk.81.1.49-4.42.2.16-8.63.pth
BLEU = 18.99, 46.3/23.6/14.0/8.5 (BP=1.000, ratio=1.047, hyp_len=11972, ref_len=11432)
Evaluation result for the model: seq-model-mybk.82.1.43-4.16.2.16-8.65.pth
BLEU = 17.11, 44.1/21.7/12.3/7.3 (BP=1.000, ratio=1.106, hyp_len=12643, ref_len=11432)
Evaluation result for the model: seq-model-mybk.83.1.52-4.59.2.17-8.76.pth
BLEU = 17.89, 45.0/22.5/13.1/7.7 (BP=1.000, ratio=1.080, hyp_len=12349, ref_len=11432)
Evaluation result for the model: seq-model-mybk.84.1.50-4.48.2.14-8.54.pth
BLEU = 18.20, 45.3/23.0/13.3/8.0 (BP=1.000, ratio=1.091, hyp_len=12469, ref_len=11432)
Evaluation result for the model: seq-model-mybk.85.1.38-3.97.2.17-8.79.pth
BLEU = 18.28, 45.3/23.0/13.4/8.0 (BP=1.000, ratio=1.083, hyp_len=12383, ref_len=11432)
Evaluation result for the model: seq-model-mybk.86.1.40-4.06.2.15-8.61.pth
BLEU = 18.76, 45.8/23.5/13.7/8.4 (BP=1.000, ratio=1.089, hyp_len=12447, ref_len=11432)
Evaluation result for the model: seq-model-mybk.87.1.41-4.09.2.17-8.77.pth
BLEU = 18.41, 44.6/22.9/13.5/8.3 (BP=1.000, ratio=1.111, hyp_len=12697, ref_len=11432)
Evaluation result for the model: seq-model-mybk.88.1.37-3.92.2.16-8.65.pth
BLEU = 18.79, 45.5/23.5/13.8/8.5 (BP=1.000, ratio=1.097, hyp_len=12545, ref_len=11432)
Evaluation result for the model: seq-model-mybk.89.1.34-3.80.2.19-8.91.pth
BLEU = 18.11, 44.8/23.0/13.2/7.9 (BP=1.000, ratio=1.116, hyp_len=12754, ref_len=11432)
Evaluation result for the model: seq-model-mybk.90.1.39-4.02.2.18-8.82.pth
BLEU = 17.95, 45.0/22.5/13.1/7.8 (BP=1.000, ratio=1.085, hyp_len=12409, ref_len=11432)
Evaluation result for the model: seq-model-mybk.91.1.30-3.68.2.19-8.96.pth
BLEU = 17.91, 43.7/22.3/13.1/8.0 (BP=1.000, ratio=1.118, hyp_len=12779, ref_len=11432)
Evaluation result for the model: seq-model-mybk.92.1.44-4.21.2.19-8.92.pth
BLEU = 18.53, 45.2/23.0/13.6/8.3 (BP=1.000, ratio=1.109, hyp_len=12683, ref_len=11432)
Evaluation result for the model: seq-model-mybk.93.1.36-3.90.2.24-9.39.pth
BLEU = 18.59, 45.4/23.4/13.8/8.2 (BP=1.000, ratio=1.098, hyp_len=12550, ref_len=11432)
Evaluation result for the model: seq-model-mybk.94.1.29-3.62.2.21-9.13.pth
BLEU = 18.13, 44.9/22.6/13.2/8.0 (BP=1.000, ratio=1.080, hyp_len=12352, ref_len=11432)
Evaluation result for the model: seq-model-mybk.95.1.29-3.63.2.19-8.96.pth
BLEU = 18.17, 44.9/22.5/13.3/8.1 (BP=1.000, ratio=1.099, hyp_len=12565, ref_len=11432)
Evaluation result for the model: seq-model-mybk.96.1.29-3.64.2.18-8.85.pth
BLEU = 18.88, 46.2/23.6/13.8/8.4 (BP=1.000, ratio=1.089, hyp_len=12453, ref_len=11432)
Evaluation result for the model: seq-model-mybk.97.1.23-3.43.2.23-9.26.pth
BLEU = 17.75, 44.3/22.3/12.9/7.8 (BP=1.000, ratio=1.101, hyp_len=12592, ref_len=11432)
Evaluation result for the model: seq-model-mybk.98.1.26-3.53.2.24-9.35.pth
BLEU = 18.77, 46.0/23.5/13.8/8.3 (BP=1.000, ratio=1.086, hyp_len=12417, ref_len=11432)
Evaluation result for the model: seq-model-mybk.99.1.22-3.37.2.19-8.91.pth
BLEU = 18.56, 46.3/23.4/13.5/8.1 (BP=1.000, ratio=1.093, hyp_len=12491, ref_len=11432)
/home/ye/exp/simple-nmt

real	21m43.646s
user	19m5.124s
sys	2m17.389s
(simple-nmt) ye@:~/exp/simple-nmt$
```

Best model is 81 epoch model (seq-model-mybk.81.1.49-4.42.2.16-8.63.pth) and Best BLEU Score: 18.99  


## Preparing Seq2Seq Baseline for bk-my


```
time python train.py --train /home/ye/exp/simple-nmt/data/my-bk/syl/train \
--valid /home/ye/exp/simple-nmt/data/my-bk/syl/dev \
--lang bkmy --gpu_id 0 --batch_size 64 --n_epochs 100 \
--max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 \
--n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 \
--use_adam --rl_n_epochs 0 \
--model_fn ./model/seq2seq/baseline/bkmy-100epoch/seq-model-bkmy.pth | tee ./model/seq2seq/baseline/bkmy-100epoch/bkmy-seq2seq-baseline-train.log;
```

Training ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/my-bk/syl/train \
> --valid /home/ye/exp/simple-nmt/data/my-bk/syl/dev \
> --lang bkmy --gpu_id 0 --batch_size 64 --n_epochs 100 \
> --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 \
> --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 \
> --use_adam --rl_n_epochs 0 \
> --model_fn ./model/seq2seq/baseline/bkmy-100epoch/seq-model-bkmy.pth | tee ./model/seq2seq/baseline/bkmy-100epoch/bkmy-seq2seq-baseline-train.log;
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
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
    'model_fn': './model/seq2seq/baseline/bkmy-100epoch/seq-model-bkmy.pth',
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
Epoch 1 - |param|=6.02e+02 |g_param|=3.45e+05 loss=4.7325e+00 ppl=113.58                                                
Validation - loss=4.0315e+00 ppl=56.34 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=6.02e+02 |g_param|=4.12e+05 loss=4.2635e+00 ppl=71.06                                                 
Validation - loss=3.8382e+00 ppl=46.44 best_loss=4.0315e+00 best_ppl=56.34                                              
Epoch 3 - |param|=6.02e+02 |g_param|=3.88e+05 loss=4.2701e+00 ppl=71.53                                                 
Validation - loss=3.7868e+00 ppl=44.11 best_loss=3.8382e+00 best_ppl=46.44                                              
Epoch 4 - |param|=6.02e+02 |g_param|=2.48e+05 loss=4.1770e+00 ppl=65.17                                                 
Validation - loss=3.7957e+00 ppl=44.51 best_loss=3.7868e+00 best_ppl=44.11                                              
Epoch 5 - |param|=6.02e+02 |g_param|=1.97e+05 loss=4.1466e+00 ppl=63.22                                                 
Validation - loss=3.7726e+00 ppl=43.49 best_loss=3.7868e+00 best_ppl=44.11                                              
Epoch 6 - |param|=6.02e+02 |g_param|=2.21e+05 loss=4.2589e+00 ppl=70.73                                                 
Validation - loss=3.7314e+00 ppl=41.74 best_loss=3.7726e+00 best_ppl=43.49                                              
Epoch 7 - |param|=6.02e+02 |g_param|=1.96e+05 loss=4.0684e+00 ppl=58.46                                                 
Validation - loss=3.6715e+00 ppl=39.31 best_loss=3.7314e+00 best_ppl=41.74                                              
Epoch 8 - |param|=6.03e+02 |g_param|=1.91e+05 loss=3.9848e+00 ppl=53.77                                                 
Validation - loss=3.5865e+00 ppl=36.11 best_loss=3.6715e+00 best_ppl=39.31                                              
Epoch 9 - |param|=6.03e+02 |g_param|=1.55e+05 loss=3.8827e+00 ppl=48.56                                                 
Validation - loss=3.4242e+00 ppl=30.70 best_loss=3.5865e+00 best_ppl=36.11                                              
Epoch 10 - |param|=6.03e+02 |g_param|=1.48e+05 loss=3.7249e+00 ppl=41.47                                                
Validation - loss=3.3217e+00 ppl=27.71 best_loss=3.4242e+00 best_ppl=30.70                                              
Epoch 11 - |param|=6.04e+02 |g_param|=1.63e+05 loss=3.7541e+00 ppl=42.70                                                
Validation - loss=3.2380e+00 ppl=25.48 best_loss=3.3217e+00 best_ppl=27.71                                              
Epoch 12 - |param|=6.04e+02 |g_param|=1.45e+05 loss=3.5507e+00 ppl=34.84                                                
Validation - loss=3.1599e+00 ppl=23.57 best_loss=3.2380e+00 best_ppl=25.48                                              
Epoch 13 - |param|=6.04e+02 |g_param|=1.45e+05 loss=3.4247e+00 ppl=30.71                                                
Validation - loss=3.1221e+00 ppl=22.69 best_loss=3.1599e+00 best_ppl=23.57                                              
Epoch 14 - |param|=6.05e+02 |g_param|=1.69e+05 loss=3.4802e+00 ppl=32.47                                                
Validation - loss=3.1020e+00 ppl=22.24 best_loss=3.1221e+00 best_ppl=22.69                                              
Epoch 15 - |param|=6.05e+02 |g_param|=1.61e+05 loss=3.3599e+00 ppl=28.79                                                
Validation - loss=3.0584e+00 ppl=21.29 best_loss=3.1020e+00 best_ppl=22.24                                              
Epoch 16 - |param|=6.06e+02 |g_param|=1.55e+05 loss=3.2934e+00 ppl=26.93                                                
Validation - loss=3.0202e+00 ppl=20.50 best_loss=3.0584e+00 best_ppl=21.29                                              
Epoch 17 - |param|=6.06e+02 |g_param|=1.57e+05 loss=3.2776e+00 ppl=26.51                                                
Validation - loss=2.9882e+00 ppl=19.85 best_loss=3.0202e+00 best_ppl=20.50                                              
Epoch 18 - |param|=6.07e+02 |g_param|=1.48e+05 loss=3.2358e+00 ppl=25.43                                                
Validation - loss=2.9529e+00 ppl=19.16 best_loss=2.9882e+00 best_ppl=19.85                                              
Epoch 19 - |param|=6.07e+02 |g_param|=1.55e+05 loss=3.2331e+00 ppl=25.36                                                
Validation - loss=2.9394e+00 ppl=18.91 best_loss=2.9529e+00 best_ppl=19.16                                              
Epoch 20 - |param|=6.08e+02 |g_param|=1.52e+05 loss=3.0922e+00 ppl=22.03                                                
Validation - loss=2.8807e+00 ppl=17.83 best_loss=2.9394e+00 best_ppl=18.91                                              
Epoch 21 - |param|=6.08e+02 |g_param|=1.45e+05 loss=3.0702e+00 ppl=21.55                                                
Validation - loss=2.8285e+00 ppl=16.92 best_loss=2.8807e+00 best_ppl=17.83                                              
Epoch 22 - |param|=6.09e+02 |g_param|=1.55e+05 loss=3.0971e+00 ppl=22.13                                                
Validation - loss=2.7832e+00 ppl=16.17 best_loss=2.8285e+00 best_ppl=16.92                                              
Epoch 23 - |param|=6.09e+02 |g_param|=1.56e+05 loss=3.0105e+00 ppl=20.30                                                
Validation - loss=2.7473e+00 ppl=15.60 best_loss=2.7832e+00 best_ppl=16.17                                              
Epoch 24 - |param|=6.10e+02 |g_param|=1.59e+05 loss=2.9388e+00 ppl=18.89                                                
Validation - loss=2.7133e+00 ppl=15.08 best_loss=2.7473e+00 best_ppl=15.60                                              
Epoch 25 - |param|=6.10e+02 |g_param|=1.59e+05 loss=2.8631e+00 ppl=17.52                                                
Validation - loss=2.6484e+00 ppl=14.13 best_loss=2.7133e+00 best_ppl=15.08                                              
Epoch 26 - |param|=6.11e+02 |g_param|=1.78e+05 loss=2.8779e+00 ppl=17.78                                                
Validation - loss=2.6005e+00 ppl=13.47 best_loss=2.6484e+00 best_ppl=14.13                                              
Epoch 27 - |param|=6.11e+02 |g_param|=1.69e+05 loss=2.7957e+00 ppl=16.37                                                
Validation - loss=2.5644e+00 ppl=12.99 best_loss=2.6005e+00 best_ppl=13.47                                              
Epoch 28 - |param|=6.12e+02 |g_param|=1.75e+05 loss=2.7625e+00 ppl=15.84                                                
Validation - loss=2.5271e+00 ppl=12.52 best_loss=2.5644e+00 best_ppl=12.99                                              
Epoch 29 - |param|=6.12e+02 |g_param|=1.70e+05 loss=2.7645e+00 ppl=15.87                                                
Validation - loss=2.5326e+00 ppl=12.59 best_loss=2.5271e+00 best_ppl=12.52                                              
Epoch 30 - |param|=6.13e+02 |g_param|=1.78e+05 loss=2.6309e+00 ppl=13.89                                                
Validation - loss=2.4427e+00 ppl=11.50 best_loss=2.5271e+00 best_ppl=12.52                                              
Epoch 31 - |param|=6.13e+02 |g_param|=1.64e+05 loss=2.5568e+00 ppl=12.89                                                
Validation - loss=2.4181e+00 ppl=11.22 best_loss=2.4427e+00 best_ppl=11.50                                              
Epoch 32 - |param|=6.14e+02 |g_param|=1.90e+05 loss=2.6099e+00 ppl=13.60                                                
Validation - loss=2.4239e+00 ppl=11.29 best_loss=2.4181e+00 best_ppl=11.22                                              
Epoch 33 - |param|=6.14e+02 |g_param|=1.75e+05 loss=2.5789e+00 ppl=13.18                                                
Validation - loss=2.3709e+00 ppl=10.71 best_loss=2.4181e+00 best_ppl=11.22                                              
Epoch 34 - |param|=6.15e+02 |g_param|=1.94e+05 loss=2.5367e+00 ppl=12.64                                                
Validation - loss=2.3329e+00 ppl=10.31 best_loss=2.3709e+00 best_ppl=10.71                                              
Epoch 35 - |param|=6.15e+02 |g_param|=1.81e+05 loss=2.4487e+00 ppl=11.57                                                
Validation - loss=2.3191e+00 ppl=10.17 best_loss=2.3329e+00 best_ppl=10.31                                              
Epoch 36 - |param|=6.16e+02 |g_param|=2.69e+05 loss=2.3726e+00 ppl=10.73                                                
Validation - loss=2.2830e+00 ppl=9.81 best_loss=2.3191e+00 best_ppl=10.17                                               
Epoch 37 - |param|=6.16e+02 |g_param|=3.98e+05 loss=2.4590e+00 ppl=11.69                                                
Validation - loss=2.2863e+00 ppl=9.84 best_loss=2.2830e+00 best_ppl=9.81                                                
Epoch 38 - |param|=6.17e+02 |g_param|=4.12e+05 loss=2.3156e+00 ppl=10.13                                                
Validation - loss=2.2532e+00 ppl=9.52 best_loss=2.2830e+00 best_ppl=9.81                                                
Epoch 39 - |param|=6.17e+02 |g_param|=3.88e+05 loss=2.2886e+00 ppl=9.86                                                 
Validation - loss=2.2231e+00 ppl=9.24 best_loss=2.2532e+00 best_ppl=9.52                                                
Epoch 40 - |param|=6.18e+02 |g_param|=4.12e+05 loss=2.3284e+00 ppl=10.26                                                
Validation - loss=2.2021e+00 ppl=9.04 best_loss=2.2231e+00 best_ppl=9.24                                                
Epoch 41 - |param|=6.18e+02 |g_param|=4.24e+05 loss=2.2078e+00 ppl=9.10                                                 
Validation - loss=2.2003e+00 ppl=9.03 best_loss=2.2021e+00 best_ppl=9.04                                                
Epoch 42 - |param|=6.19e+02 |g_param|=4.21e+05 loss=2.2091e+00 ppl=9.11                                                 
Validation - loss=2.1667e+00 ppl=8.73 best_loss=2.2003e+00 best_ppl=9.03                                                
Epoch 43 - |param|=6.19e+02 |g_param|=4.27e+05 loss=2.1896e+00 ppl=8.93                                                 
Validation - loss=2.1374e+00 ppl=8.48 best_loss=2.1667e+00 best_ppl=8.73                                                
Epoch 44 - |param|=6.20e+02 |g_param|=4.36e+05 loss=2.1739e+00 ppl=8.79                                                 
Validation - loss=2.1274e+00 ppl=8.39 best_loss=2.1374e+00 best_ppl=8.48                                                
Epoch 45 - |param|=6.20e+02 |g_param|=4.29e+05 loss=2.1407e+00 ppl=8.51                                                 
Validation - loss=2.1060e+00 ppl=8.21 best_loss=2.1274e+00 best_ppl=8.39                                                
Epoch 46 - |param|=6.21e+02 |g_param|=3.08e+05 loss=2.0544e+00 ppl=7.80                                                 
Validation - loss=2.1003e+00 ppl=8.17 best_loss=2.1060e+00 best_ppl=8.21                                                
Epoch 47 - |param|=6.21e+02 |g_param|=2.12e+05 loss=1.9870e+00 ppl=7.29                                                 
Validation - loss=2.0937e+00 ppl=8.11 best_loss=2.1003e+00 best_ppl=8.17                                                
Epoch 48 - |param|=6.21e+02 |g_param|=2.32e+05 loss=1.9669e+00 ppl=7.15                                                 
Validation - loss=2.0841e+00 ppl=8.04 best_loss=2.0937e+00 best_ppl=8.11                                                
Epoch 49 - |param|=6.22e+02 |g_param|=2.22e+05 loss=1.9094e+00 ppl=6.75                                                 
Validation - loss=2.0833e+00 ppl=8.03 best_loss=2.0841e+00 best_ppl=8.04                                                
Epoch 50 - |param|=6.22e+02 |g_param|=2.44e+05 loss=1.9621e+00 ppl=7.11                                                 
Validation - loss=2.0675e+00 ppl=7.90 best_loss=2.0833e+00 best_ppl=8.03                                                
Epoch 51 - |param|=6.23e+02 |g_param|=2.17e+05 loss=1.9717e+00 ppl=7.18                                                 
Validation - loss=2.0632e+00 ppl=7.87 best_loss=2.0675e+00 best_ppl=7.90                                                
Epoch 52 - |param|=6.23e+02 |g_param|=2.35e+05 loss=1.9116e+00 ppl=6.76                                                 
Validation - loss=2.0517e+00 ppl=7.78 best_loss=2.0632e+00 best_ppl=7.87                                                
Epoch 53 - |param|=6.24e+02 |g_param|=2.43e+05 loss=1.9536e+00 ppl=7.05                                                 
Validation - loss=2.0435e+00 ppl=7.72 best_loss=2.0517e+00 best_ppl=7.78                                                
Epoch 54 - |param|=6.24e+02 |g_param|=2.43e+05 loss=1.7988e+00 ppl=6.04                                                 
Validation - loss=2.0252e+00 ppl=7.58 best_loss=2.0435e+00 best_ppl=7.72                                                
Epoch 55 - |param|=6.25e+02 |g_param|=2.22e+05 loss=1.7820e+00 ppl=5.94                                                 
Validation - loss=2.0487e+00 ppl=7.76 best_loss=2.0252e+00 best_ppl=7.58                                                
Epoch 56 - |param|=6.25e+02 |g_param|=2.42e+05 loss=1.8378e+00 ppl=6.28                                                 
Validation - loss=2.0261e+00 ppl=7.58 best_loss=2.0252e+00 best_ppl=7.58                                                
Epoch 57 - |param|=6.25e+02 |g_param|=2.48e+05 loss=1.7529e+00 ppl=5.77                                                 
Validation - loss=2.0307e+00 ppl=7.62 best_loss=2.0252e+00 best_ppl=7.58                                                
Epoch 58 - |param|=6.26e+02 |g_param|=2.66e+05 loss=1.7136e+00 ppl=5.55                                                 
Validation - loss=2.0170e+00 ppl=7.52 best_loss=2.0252e+00 best_ppl=7.58                                                
Epoch 59 - |param|=6.26e+02 |g_param|=2.62e+05 loss=1.7093e+00 ppl=5.53                                                 
Validation - loss=2.0098e+00 ppl=7.46 best_loss=2.0170e+00 best_ppl=7.52                                                
Epoch 60 - |param|=6.27e+02 |g_param|=2.46e+05 loss=1.6597e+00 ppl=5.26                                                 
Validation - loss=2.0109e+00 ppl=7.47 best_loss=2.0098e+00 best_ppl=7.46                                                
Epoch 61 - |param|=6.27e+02 |g_param|=2.56e+05 loss=1.7756e+00 ppl=5.90                                                 
Validation - loss=2.0181e+00 ppl=7.52 best_loss=2.0098e+00 best_ppl=7.46                                                
Epoch 62 - |param|=6.28e+02 |g_param|=2.49e+05 loss=1.6288e+00 ppl=5.10                                                 
Validation - loss=1.9966e+00 ppl=7.36 best_loss=2.0098e+00 best_ppl=7.46                                                
Epoch 63 - |param|=6.28e+02 |g_param|=2.52e+05 loss=1.7084e+00 ppl=5.52                                                 
Validation - loss=1.9949e+00 ppl=7.35 best_loss=1.9966e+00 best_ppl=7.36                                                
Epoch 64 - |param|=6.29e+02 |g_param|=2.61e+05 loss=1.6491e+00 ppl=5.20                                                 
Validation - loss=2.0096e+00 ppl=7.46 best_loss=1.9949e+00 best_ppl=7.35                                                
Epoch 65 - |param|=6.29e+02 |g_param|=2.62e+05 loss=1.5810e+00 ppl=4.86                                                 
Validation - loss=2.0144e+00 ppl=7.50 best_loss=1.9949e+00 best_ppl=7.35                                                
Epoch 66 - |param|=6.29e+02 |g_param|=2.70e+05 loss=1.5475e+00 ppl=4.70                                                 
Validation - loss=2.0083e+00 ppl=7.45 best_loss=1.9949e+00 best_ppl=7.35                                                
Epoch 67 - |param|=6.30e+02 |g_param|=2.55e+05 loss=1.5423e+00 ppl=4.68                                                 
Validation - loss=2.0003e+00 ppl=7.39 best_loss=1.9949e+00 best_ppl=7.35                                                
Epoch 68 - |param|=6.30e+02 |g_param|=2.79e+05 loss=1.6300e+00 ppl=5.10                                                 
Validation - loss=2.0110e+00 ppl=7.47 best_loss=1.9949e+00 best_ppl=7.35                                                
Epoch 69 - |param|=6.31e+02 |g_param|=2.47e+05 loss=1.4540e+00 ppl=4.28                                                 
Validation - loss=1.9947e+00 ppl=7.35 best_loss=1.9949e+00 best_ppl=7.35                                                
Epoch 70 - |param|=6.31e+02 |g_param|=2.67e+05 loss=1.4736e+00 ppl=4.37                                                 
Validation - loss=1.9930e+00 ppl=7.34 best_loss=1.9947e+00 best_ppl=7.35                                                
Epoch 71 - |param|=6.31e+02 |g_param|=2.69e+05 loss=1.4941e+00 ppl=4.46                                                 
Validation - loss=2.0175e+00 ppl=7.52 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 72 - |param|=6.32e+02 |g_param|=2.98e+05 loss=1.4867e+00 ppl=4.42                                                 
Validation - loss=2.0058e+00 ppl=7.43 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 73 - |param|=6.32e+02 |g_param|=2.73e+05 loss=1.4226e+00 ppl=4.15                                                 
Validation - loss=2.0119e+00 ppl=7.48 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 74 - |param|=6.33e+02 |g_param|=2.68e+05 loss=1.4422e+00 ppl=4.23                                                 
Validation - loss=2.0150e+00 ppl=7.50 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 75 - |param|=6.33e+02 |g_param|=2.58e+05 loss=1.3577e+00 ppl=3.89                                                 
Validation - loss=2.0121e+00 ppl=7.48 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 76 - |param|=6.34e+02 |g_param|=2.82e+05 loss=1.3764e+00 ppl=3.96                                                 
Validation - loss=2.0103e+00 ppl=7.47 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 77 - |param|=6.34e+02 |g_param|=2.74e+05 loss=1.3663e+00 ppl=3.92                                                 
Validation - loss=2.0074e+00 ppl=7.44 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 78 - |param|=6.34e+02 |g_param|=2.83e+05 loss=1.3317e+00 ppl=3.79                                                 
Validation - loss=2.0059e+00 ppl=7.43 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 79 - |param|=6.35e+02 |g_param|=4.89e+05 loss=1.3419e+00 ppl=3.83                                                 
Validation - loss=2.0063e+00 ppl=7.44 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 80 - |param|=6.35e+02 |g_param|=5.65e+05 loss=1.3170e+00 ppl=3.73                                                 
Validation - loss=2.0081e+00 ppl=7.45 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 81 - |param|=6.35e+02 |g_param|=5.36e+05 loss=1.3002e+00 ppl=3.67                                                 
Validation - loss=2.0054e+00 ppl=7.43 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 82 - |param|=6.36e+02 |g_param|=6.02e+05 loss=1.3743e+00 ppl=3.95                                                 
Validation - loss=2.0289e+00 ppl=7.61 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 83 - |param|=6.36e+02 |g_param|=3.10e+05 loss=1.2538e+00 ppl=3.50                                                 
Validation - loss=2.0071e+00 ppl=7.44 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 84 - |param|=6.37e+02 |g_param|=2.99e+05 loss=1.2499e+00 ppl=3.49                                                 
Validation - loss=2.0123e+00 ppl=7.48 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 85 - |param|=6.37e+02 |g_param|=2.98e+05 loss=1.2560e+00 ppl=3.51                                                 
Validation - loss=2.0108e+00 ppl=7.47 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 86 - |param|=6.37e+02 |g_param|=3.00e+05 loss=1.2314e+00 ppl=3.43                                                 
Validation - loss=2.0098e+00 ppl=7.46 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 87 - |param|=6.38e+02 |g_param|=2.83e+05 loss=1.2684e+00 ppl=3.56                                                 
Validation - loss=2.0249e+00 ppl=7.58 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 88 - |param|=6.38e+02 |g_param|=2.96e+05 loss=1.2426e+00 ppl=3.46                                                 
Validation - loss=2.0062e+00 ppl=7.43 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 89 - |param|=6.39e+02 |g_param|=2.96e+05 loss=1.2932e+00 ppl=3.64                                                 
Validation - loss=2.0171e+00 ppl=7.52 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 90 - |param|=6.39e+02 |g_param|=2.98e+05 loss=1.1675e+00 ppl=3.21                                                 
Validation - loss=2.0243e+00 ppl=7.57 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 91 - |param|=6.39e+02 |g_param|=2.99e+05 loss=1.1672e+00 ppl=3.21                                                 
Validation - loss=2.0362e+00 ppl=7.66 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 92 - |param|=6.40e+02 |g_param|=3.19e+05 loss=1.1477e+00 ppl=3.15                                                 
Validation - loss=2.0582e+00 ppl=7.83 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 93 - |param|=6.40e+02 |g_param|=2.90e+05 loss=1.1376e+00 ppl=3.12                                                 
Validation - loss=2.0348e+00 ppl=7.65 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 94 - |param|=6.41e+02 |g_param|=3.08e+05 loss=1.1556e+00 ppl=3.18                                                 
Validation - loss=2.0240e+00 ppl=7.57 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 95 - |param|=6.41e+02 |g_param|=3.27e+05 loss=1.1810e+00 ppl=3.26                                                 
Validation - loss=2.0435e+00 ppl=7.72 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 96 - |param|=6.41e+02 |g_param|=3.10e+05 loss=1.1564e+00 ppl=3.18                                                 
Validation - loss=2.0342e+00 ppl=7.65 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 97 - |param|=6.42e+02 |g_param|=3.08e+05 loss=1.1638e+00 ppl=3.20                                                 
Validation - loss=2.0598e+00 ppl=7.84 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 98 - |param|=6.42e+02 |g_param|=2.93e+05 loss=1.0730e+00 ppl=2.92                                                 
Validation - loss=2.0380e+00 ppl=7.67 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 99 - |param|=6.42e+02 |g_param|=2.75e+05 loss=1.0229e+00 ppl=2.78                                                 
Validation - loss=2.0602e+00 ppl=7.85 best_loss=1.9930e+00 best_ppl=7.34                                                
Epoch 100 - |param|=6.43e+02 |g_param|=3.06e+05 loss=1.0616e+00 ppl=2.89                                                
Validation - loss=2.0630e+00 ppl=7.87 best_loss=1.9930e+00 best_ppl=7.34                                                

real	13m0.180s
user	12m46.897s
sys	0m11.858s
(simple-nmt) ye@:~/exp/simple-nmt$
```

Updating testing/evaluation bash shell script ...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, Thailand
# find all models and parse to translate.py for testing and multi-bleu.perl for evaluation with BLEU score
# updated for bk-my

cd ./model/seq2seq/baseline/bkmy-100epoch;

for i in *.pth; do
   MODEL=$i;

   # Testing
   python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang bkmy < /home/ye/exp/simple-nmt/data/my-bk/syl/test.bk > $MODEL.hyp

   # Evaluation with BLEU Score
   echo "Evaluation result for the model: $MODEL" | tee -a eval-results-bkmy-seq2seq-baseline-100epoch.txt;
   cat $MODEL.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/my-bk/syl/test.my | tee  -a eval-results-bkmy-seq2seq-baseline-100epoch.txt;

done

cd -;

```

Testing/Evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-loop-seq2seq-bkmy.sh 
Evaluation result for the model: seq-model-bkmy.01.4.73-113.58.4.03-56.34.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.9/0.6/0.0/0.0 (BP=0.931, ratio=0.933, hyp_len=11413, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.02.4.26-71.06.3.84-46.44.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.2/0.6/0.0/0.0 (BP=0.966, ratio=0.966, hyp_len=11821, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.03.4.27-71.53.3.79-44.11.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.2/0.4/0.0/0.0 (BP=0.981, ratio=0.981, hyp_len=12004, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.04.4.18-65.17.3.80-44.51.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.0/0.5/0.0/0.0 (BP=1.000, ratio=1.024, hyp_len=12526, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.05.4.15-63.22.3.77-43.49.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.5/0.5/0.0/0.0 (BP=1.000, ratio=1.055, hyp_len=12908, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.06.4.26-70.73.3.73-41.74.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.2/0.6/0.0/0.0 (BP=0.987, ratio=0.987, hyp_len=12068, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.07.4.07-58.46.3.67-39.31.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.5/0.1/0.0/0.0 (BP=1.000, ratio=1.052, hyp_len=12869, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.08.3.98-53.77.3.59-36.11.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.9/1.1/0.1/0.0 (BP=1.000, ratio=1.084, hyp_len=13259, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.09.3.88-48.56.3.42-30.70.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.9/1.4/0.0/0.0 (BP=1.000, ratio=1.072, hyp_len=13115, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.100.1.06-2.89.2.06-7.87.pth
BLEU = 20.93, 48.4/26.7/15.5/9.6 (BP=1.000, ratio=1.094, hyp_len=13380, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.10.3.72-41.47.3.32-27.71.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.1/3.9/0.2/0.0 (BP=1.000, ratio=1.172, hyp_len=14340, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.11.3.75-42.70.3.24-25.48.pth
BLEU = 0.04, 0.8/0.1/0.0/0.0 (BP=1.000, ratio=16.789, hyp_len=205351, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.12.3.55-34.84.3.16-23.57.pth
BLEU = 0.03, 0.7/0.1/0.0/0.0 (BP=1.000, ratio=18.763, hyp_len=229495, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.13.3.42-30.71.3.12-22.69.pth
BLEU = 0.10, 2.0/0.4/0.1/0.0 (BP=1.000, ratio=11.094, hyp_len=135693, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.14.3.48-32.47.3.10-22.24.pth
BLEU = 0.05, 0.7/0.1/0.0/0.0 (BP=1.000, ratio=21.705, hyp_len=265472, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.15.3.36-28.79.3.06-21.29.pth
BLEU = 0.06, 0.7/0.2/0.0/0.0 (BP=1.000, ratio=20.996, hyp_len=256808, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.16.3.29-26.93.3.02-20.50.pth
BLEU = 0.33, 2.9/0.6/0.2/0.0 (BP=1.000, ratio=9.024, hyp_len=110367, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.17.3.28-26.51.2.99-19.85.pth
BLEU = 2.36, 21.7/5.1/1.3/0.2 (BP=1.000, ratio=1.351, hyp_len=16526, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.18.3.24-25.43.2.95-19.16.pth
BLEU = 0.48, 4.0/1.1/0.3/0.0 (BP=1.000, ratio=6.757, hyp_len=82649, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.19.3.23-25.36.2.94-18.91.pth
BLEU = 1.94, 12.8/3.8/1.1/0.3 (BP=1.000, ratio=2.385, hyp_len=29170, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.20.3.09-22.03.2.88-17.83.pth
BLEU = 4.76, 24.7/8.3/2.7/0.9 (BP=1.000, ratio=1.320, hyp_len=16143, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.21.3.07-21.55.2.83-16.92.pth
BLEU = 4.48, 22.0/7.5/2.7/0.9 (BP=1.000, ratio=1.486, hyp_len=18177, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.22.3.10-22.13.2.78-16.17.pth
BLEU = 6.33, 28.2/10.5/3.9/1.4 (BP=1.000, ratio=1.173, hyp_len=14347, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.23.3.01-20.30.2.75-15.60.pth
BLEU = 3.42, 16.5/5.9/2.1/0.7 (BP=1.000, ratio=2.055, hyp_len=25132, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.24.2.94-18.89.2.71-15.08.pth
BLEU = 2.79, 14.3/5.0/1.7/0.5 (BP=1.000, ratio=2.359, hyp_len=28855, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.25.2.86-17.52.2.65-14.13.pth
BLEU = 3.26, 14.2/5.6/2.1/0.7 (BP=1.000, ratio=2.439, hyp_len=29827, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.26.2.88-17.78.2.60-13.47.pth
BLEU = 5.33, 22.3/8.7/3.4/1.2 (BP=1.000, ratio=1.613, hyp_len=19727, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.27.2.80-16.37.2.56-12.99.pth
BLEU = 5.09, 20.5/8.0/3.2/1.3 (BP=1.000, ratio=1.781, hyp_len=21789, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.28.2.76-15.84.2.53-12.52.pth
BLEU = 7.07, 27.2/11.1/4.6/1.8 (BP=1.000, ratio=1.375, hyp_len=16819, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.29.2.76-15.87.2.53-12.59.pth
BLEU = 7.31, 27.7/11.2/4.8/1.9 (BP=1.000, ratio=1.362, hyp_len=16656, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.30.2.63-13.89.2.44-11.50.pth
BLEU = 8.94, 31.4/13.6/5.9/2.5 (BP=1.000, ratio=1.255, hyp_len=15356, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.31.2.56-12.89.2.42-11.22.pth
BLEU = 9.76, 34.4/14.5/6.4/2.8 (BP=1.000, ratio=1.139, hyp_len=13933, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.32.2.61-13.60.2.42-11.29.pth
BLEU = 10.85, 36.6/15.8/7.3/3.3 (BP=1.000, ratio=1.094, hyp_len=13379, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.33.2.58-13.18.2.37-10.71.pth
BLEU = 10.12, 33.7/14.7/6.7/3.2 (BP=1.000, ratio=1.216, hyp_len=14877, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.34.2.54-12.64.2.33-10.31.pth
BLEU = 12.06, 38.9/17.4/8.1/3.9 (BP=1.000, ratio=1.083, hyp_len=13250, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.35.2.45-11.57.2.32-10.17.pth
BLEU = 13.25, 41.2/18.8/9.0/4.4 (BP=1.000, ratio=1.046, hyp_len=12799, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.36.2.37-10.73.2.28-9.81.pth
BLEU = 11.13, 35.8/16.2/7.5/3.5 (BP=1.000, ratio=1.202, hyp_len=14699, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.37.2.46-11.69.2.29-9.84.pth
BLEU = 11.75, 37.2/16.9/7.9/3.8 (BP=1.000, ratio=1.149, hyp_len=14050, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.38.2.32-10.13.2.25-9.52.pth
BLEU = 12.14, 38.3/17.3/8.2/4.0 (BP=1.000, ratio=1.152, hyp_len=14096, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.39.2.29-9.86.2.22-9.24.pth
BLEU = 13.56, 40.9/19.0/9.3/4.7 (BP=1.000, ratio=1.097, hyp_len=13415, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.40.2.33-10.26.2.20-9.04.pth
BLEU = 13.18, 41.0/18.6/8.9/4.4 (BP=1.000, ratio=1.091, hyp_len=13347, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.41.2.21-9.10.2.20-9.03.pth
BLEU = 13.56, 41.3/19.2/9.3/4.6 (BP=1.000, ratio=1.067, hyp_len=13051, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.42.2.21-9.11.2.17-8.73.pth
BLEU = 14.35, 42.4/20.2/9.9/5.0 (BP=1.000, ratio=1.075, hyp_len=13146, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.43.2.19-8.93.2.14-8.48.pth
BLEU = 15.11, 42.5/20.6/10.5/5.7 (BP=1.000, ratio=1.092, hyp_len=13354, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.44.2.17-8.79.2.13-8.39.pth
BLEU = 15.66, 44.6/21.8/10.9/5.7 (BP=1.000, ratio=1.058, hyp_len=12942, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.45.2.14-8.51.2.11-8.21.pth
BLEU = 16.21, 44.4/21.9/11.3/6.3 (BP=1.000, ratio=1.059, hyp_len=12958, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.46.2.05-7.80.2.10-8.17.pth
BLEU = 15.98, 44.6/21.8/11.1/6.0 (BP=1.000, ratio=1.044, hyp_len=12773, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.47.1.99-7.29.2.09-8.11.pth
BLEU = 15.87, 43.6/21.6/11.0/6.1 (BP=1.000, ratio=1.099, hyp_len=13437, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.48.1.97-7.15.2.08-8.04.pth
BLEU = 16.67, 44.8/22.5/11.8/6.5 (BP=1.000, ratio=1.076, hyp_len=13162, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.49.1.91-6.75.2.08-8.03.pth
BLEU = 16.17, 42.3/21.4/11.4/6.6 (BP=1.000, ratio=1.141, hyp_len=13951, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.50.1.96-7.11.2.07-7.90.pth
BLEU = 16.68, 44.7/22.5/11.8/6.5 (BP=1.000, ratio=1.063, hyp_len=13000, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.51.1.97-7.18.2.06-7.87.pth
BLEU = 17.26, 44.6/22.7/12.2/7.2 (BP=1.000, ratio=1.092, hyp_len=13357, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.52.1.91-6.76.2.05-7.78.pth
BLEU = 18.14, 46.7/24.3/13.1/7.3 (BP=1.000, ratio=1.071, hyp_len=13098, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.53.1.95-7.05.2.04-7.72.pth
BLEU = 18.18, 45.8/23.9/13.1/7.7 (BP=1.000, ratio=1.081, hyp_len=13219, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.54.1.80-6.04.2.03-7.58.pth
BLEU = 18.19, 46.5/24.1/13.0/7.5 (BP=1.000, ratio=1.070, hyp_len=13093, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.55.1.78-5.94.2.05-7.76.pth
BLEU = 17.51, 45.1/22.9/12.4/7.3 (BP=1.000, ratio=1.093, hyp_len=13369, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.56.1.84-6.28.2.03-7.58.pth
BLEU = 18.95, 47.3/25.0/13.7/8.0 (BP=1.000, ratio=1.063, hyp_len=12996, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.57.1.75-5.77.2.03-7.62.pth
BLEU = 18.72, 46.8/24.5/13.6/7.9 (BP=1.000, ratio=1.072, hyp_len=13107, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.58.1.71-5.55.2.02-7.52.pth
BLEU = 19.04, 47.3/24.9/13.8/8.1 (BP=1.000, ratio=1.051, hyp_len=12851, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.59.1.71-5.53.2.01-7.46.pth
BLEU = 19.99, 47.8/26.1/14.6/8.7 (BP=1.000, ratio=1.062, hyp_len=12990, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.60.1.66-5.26.2.01-7.47.pth
BLEU = 18.99, 46.4/24.8/13.8/8.2 (BP=1.000, ratio=1.085, hyp_len=13268, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.61.1.78-5.90.2.02-7.52.pth
BLEU = 19.24, 47.0/25.0/14.0/8.3 (BP=1.000, ratio=1.083, hyp_len=13248, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.62.1.63-5.10.2.00-7.36.pth
BLEU = 19.79, 47.7/25.7/14.4/8.7 (BP=1.000, ratio=1.068, hyp_len=13060, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.63.1.71-5.52.1.99-7.35.pth
BLEU = 20.36, 48.3/26.2/15.0/9.1 (BP=1.000, ratio=1.054, hyp_len=12887, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.64.1.65-5.20.2.01-7.46.pth
BLEU = 20.92, 48.4/26.5/15.5/9.6 (BP=1.000, ratio=1.052, hyp_len=12868, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.65.1.58-4.86.2.01-7.50.pth
BLEU = 20.31, 48.5/26.3/14.9/9.0 (BP=1.000, ratio=1.056, hyp_len=12913, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.66.1.55-4.70.2.01-7.45.pth
BLEU = 21.25, 49.1/27.0/15.8/9.7 (BP=1.000, ratio=1.059, hyp_len=12949, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.67.1.54-4.68.2.00-7.39.pth
BLEU = 20.85, 49.0/26.9/15.4/9.3 (BP=1.000, ratio=1.052, hyp_len=12871, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.68.1.63-5.10.2.01-7.47.pth
BLEU = 21.11, 49.0/27.1/15.7/9.5 (BP=1.000, ratio=1.063, hyp_len=12996, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.69.1.45-4.28.1.99-7.35.pth
BLEU = 21.22, 49.3/27.2/15.8/9.6 (BP=1.000, ratio=1.061, hyp_len=12972, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.70.1.47-4.37.1.99-7.34.pth
BLEU = 21.16, 49.3/27.2/15.7/9.5 (BP=1.000, ratio=1.058, hyp_len=12939, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.71.1.49-4.46.2.02-7.52.pth
BLEU = 21.16, 49.2/27.1/15.7/9.6 (BP=1.000, ratio=1.054, hyp_len=12886, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.72.1.49-4.42.2.01-7.43.pth
BLEU = 20.79, 47.9/26.3/15.3/9.7 (BP=1.000, ratio=1.066, hyp_len=13035, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.73.1.42-4.15.2.01-7.48.pth
BLEU = 21.13, 48.7/27.0/15.7/9.6 (BP=1.000, ratio=1.060, hyp_len=12960, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.74.1.44-4.23.2.01-7.50.pth
BLEU = 21.58, 49.6/27.6/16.1/9.9 (BP=1.000, ratio=1.049, hyp_len=12826, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.75.1.36-3.89.2.01-7.48.pth
BLEU = 20.46, 48.7/26.6/15.0/9.0 (BP=1.000, ratio=1.053, hyp_len=12874, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.76.1.38-3.96.2.01-7.47.pth
BLEU = 21.49, 49.6/27.7/16.0/9.7 (BP=1.000, ratio=1.045, hyp_len=12782, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.77.1.37-3.92.2.01-7.44.pth
BLEU = 21.18, 49.6/27.3/15.7/9.5 (BP=1.000, ratio=1.056, hyp_len=12911, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.78.1.33-3.79.2.01-7.43.pth
BLEU = 21.64, 49.5/27.4/16.1/10.1 (BP=1.000, ratio=1.059, hyp_len=12948, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.79.1.34-3.83.2.01-7.44.pth
BLEU = 21.00, 48.5/26.9/15.6/9.6 (BP=1.000, ratio=1.069, hyp_len=13081, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.80.1.32-3.73.2.01-7.45.pth
BLEU = 22.00, 50.3/27.9/16.4/10.2 (BP=1.000, ratio=1.046, hyp_len=12789, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.81.1.30-3.67.2.01-7.43.pth
BLEU = 21.32, 49.0/26.9/15.8/9.9 (BP=1.000, ratio=1.060, hyp_len=12965, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.82.1.37-3.95.2.03-7.61.pth
BLEU = 20.72, 48.8/26.7/15.3/9.2 (BP=1.000, ratio=1.081, hyp_len=13225, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.83.1.25-3.50.2.01-7.44.pth
BLEU = 20.66, 48.8/26.6/15.3/9.2 (BP=1.000, ratio=1.067, hyp_len=13052, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.84.1.25-3.49.2.01-7.48.pth
BLEU = 20.51, 48.6/26.3/15.0/9.2 (BP=1.000, ratio=1.063, hyp_len=13000, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.85.1.26-3.51.2.01-7.47.pth
BLEU = 20.96, 48.8/26.5/15.5/9.6 (BP=1.000, ratio=1.041, hyp_len=12729, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.86.1.23-3.43.2.01-7.46.pth
BLEU = 21.31, 48.9/27.2/15.9/9.8 (BP=1.000, ratio=1.073, hyp_len=13122, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.87.1.27-3.56.2.02-7.58.pth
BLEU = 21.37, 48.8/27.2/15.9/9.9 (BP=1.000, ratio=1.072, hyp_len=13109, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.88.1.24-3.46.2.01-7.43.pth
BLEU = 22.03, 49.7/28.0/16.6/10.2 (BP=1.000, ratio=1.062, hyp_len=12990, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.89.1.29-3.64.2.02-7.52.pth
BLEU = 21.25, 49.0/27.0/15.8/9.7 (BP=1.000, ratio=1.088, hyp_len=13310, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.90.1.17-3.21.2.02-7.57.pth
BLEU = 21.91, 49.2/27.7/16.5/10.3 (BP=1.000, ratio=1.094, hyp_len=13381, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.91.1.17-3.21.2.04-7.66.pth
BLEU = 22.12, 49.9/28.2/16.6/10.2 (BP=1.000, ratio=1.055, hyp_len=12909, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.92.1.15-3.15.2.06-7.83.pth
BLEU = 20.64, 48.0/26.4/15.3/9.4 (BP=1.000, ratio=1.085, hyp_len=13271, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.93.1.14-3.12.2.03-7.65.pth
BLEU = 20.93, 48.7/26.9/15.5/9.4 (BP=1.000, ratio=1.080, hyp_len=13205, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.94.1.16-3.18.2.02-7.57.pth
BLEU = 21.49, 49.0/27.3/16.1/9.9 (BP=1.000, ratio=1.060, hyp_len=12967, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.95.1.18-3.26.2.04-7.72.pth
BLEU = 22.62, 49.8/28.3/17.2/10.8 (BP=1.000, ratio=1.058, hyp_len=12938, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.96.1.16-3.18.2.03-7.65.pth
BLEU = 22.16, 49.9/28.1/16.5/10.4 (BP=1.000, ratio=1.052, hyp_len=12862, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.97.1.16-3.20.2.06-7.84.pth
BLEU = 21.07, 48.9/27.0/15.8/9.4 (BP=1.000, ratio=1.085, hyp_len=13272, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.98.1.07-2.92.2.04-7.67.pth
BLEU = 22.51, 49.9/28.2/17.0/10.8 (BP=1.000, ratio=1.071, hyp_len=13094, ref_len=12231)
Evaluation result for the model: seq-model-bkmy.99.1.02-2.78.2.06-7.85.pth
BLEU = 22.11, 50.3/28.1/16.5/10.2 (BP=1.000, ratio=1.050, hyp_len=12847, ref_len=12231)
/home/ye/exp/simple-nmt

real	41m49.577s
user	32m52.493s
sys	3m53.019s
```

Best model is 95 epoch model and Best Score: 22.62 

## Preparing Transformer Baseline for Myanmar-Beik

Training ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/my-bk/syl/train --valid /home/ye/exp/simple-nmt/data/my-bk/syl/dev --lang mybk --gpu_id 1 --batch_size 16 --n_epochs 100 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/mybk-100epoch/mybk-transformer-model.pth | tee ./model/transformer/baseline/mybk-100epoch/mybk-transformer-baseline-training.log
'{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 32,
    'init_epoch': 1,
    'iteration_per_update': 32,
    'lang': 'mybk',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/transformer/baseline/mybk-100epoch/mybk-transformer-model.pth',
    'n_epochs': 100,
    'n_layers': 6,
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
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/my-bk/syl/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1313, 32)
  (emb_dec): Embedding(1470, 32)
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
    (1): Linear(in_features=32, out_features=1470, bias=True)
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
Iteration:   1%|▉                                                                                | 1/87 [00:00<?, ?it/s]Epoch 1 - |param|=3.03e+02 |g_param|=2.97e+05 loss=6.0344e+00 ppl=417.55
Validation - loss=5.8927e+00 ppl=362.39 best_loss=inf best_ppl=inf                                                      
Iteration:   1%|▋                                                             | 1/87 [00:00<?, ?it/s, loss=4.54, ppl=94]Epoch 2 - |param|=3.03e+02 |g_param|=3.00e+05 loss=5.4725e+00 ppl=238.05
Validation - loss=5.3294e+00 ppl=206.31 best_loss=5.8927e+00 best_ppl=362.39                                            
Iteration:   1%|▉                                                                                | 1/87 [00:00<?, ?it/s]Epoch 3 - |param|=3.03e+02 |g_param|=2.78e+05 loss=5.0240e+00 ppl=152.02
Validation - loss=4.8854e+00 ppl=132.34 best_loss=5.3294e+00 best_ppl=206.31                                            
Epoch 4 - |param|=3.03e+02 |g_param|=2.15e+05 loss=4.7550e+00 ppl=116.17                                                
Validation - loss=4.6496e+00 ppl=104.54 best_loss=4.8854e+00 best_ppl=132.34                                            
Iteration:   1%|▉                                                                                | 1/87 [00:00<?, ?it/s]Epoch 5 - |param|=3.03e+02 |g_param|=2.06e+05 loss=4.5723e+00 ppl=96.77
Validation - loss=4.4973e+00 ppl=89.77 best_loss=4.6496e+00 best_ppl=104.54                                             
Iteration:   1%|▋                                                           | 1/87 [00:00<?, ?it/s, loss=3.56, ppl=35.3]Epoch 6 - |param|=3.03e+02 |g_param|=1.72e+05 loss=4.4276e+00 ppl=83.73
Validation - loss=4.3723e+00 ppl=79.23 best_loss=4.4973e+00 best_ppl=89.77                                              
Iteration:   1%|▉                                                                                | 1/87 [00:00<?, ?it/s]Epoch 7 - |param|=3.03e+02 |g_param|=1.42e+05 loss=4.3274e+00 ppl=75.74
Validation - loss=4.2621e+00 ppl=70.96 best_loss=4.3723e+00 best_ppl=79.23                                              
Epoch 8 - |param|=3.04e+02 |g_param|=1.40e+05 loss=4.2178e+00 ppl=67.88                                                 
Validation - loss=4.1399e+00 ppl=62.80 best_loss=4.2621e+00 best_ppl=70.96                                              
Epoch 9 - |param|=3.04e+02 |g_param|=1.17e+05 loss=4.1476e+00 ppl=63.28                                                 
Validation - loss=4.0426e+00 ppl=56.97 best_loss=4.1399e+00 best_ppl=62.80                                              
Iteration:   1%|▋                                                             | 1/87 [00:00<?, ?it/s, loss=3.26, ppl=26]Epoch 10 - |param|=3.04e+02 |g_param|=1.11e+05 loss=4.0641e+00 ppl=58.22
Validation - loss=3.9689e+00 ppl=52.93 best_loss=4.0426e+00 best_ppl=56.97                                              
Epoch 11 - |param|=3.04e+02 |g_param|=1.17e+05 loss=3.9461e+00 ppl=51.73                                                
Validation - loss=3.8868e+00 ppl=48.75 best_loss=3.9689e+00 best_ppl=52.93                                              
Epoch 12 - |param|=3.04e+02 |g_param|=1.01e+05 loss=3.9224e+00 ppl=50.52                                                
Validation - loss=3.8180e+00 ppl=45.51 best_loss=3.8868e+00 best_ppl=48.75                                              
Epoch 13 - |param|=3.04e+02 |g_param|=1.26e+05 loss=3.8132e+00 ppl=45.30                                                
Validation - loss=3.7471e+00 ppl=42.40 best_loss=3.8180e+00 best_ppl=45.51                                              
Epoch 14 - |param|=3.04e+02 |g_param|=1.63e+05 loss=3.7852e+00 ppl=44.04                                                
Validation - loss=3.6973e+00 ppl=40.34 best_loss=3.7471e+00 best_ppl=42.40                                              
Epoch 15 - |param|=3.04e+02 |g_param|=1.43e+05 loss=3.6927e+00 ppl=40.15                                                
Validation - loss=3.6486e+00 ppl=38.42 best_loss=3.6973e+00 best_ppl=40.34                                              
Epoch 16 - |param|=3.04e+02 |g_param|=1.14e+05 loss=3.6318e+00 ppl=37.78                                                
Validation - loss=3.5849e+00 ppl=36.05 best_loss=3.6486e+00 best_ppl=38.42                                              
Epoch 17 - |param|=3.04e+02 |g_param|=1.11e+05 loss=3.6060e+00 ppl=36.82                                                
Validation - loss=3.5401e+00 ppl=34.47 best_loss=3.5849e+00 best_ppl=36.05                                              
Epoch 18 - |param|=3.04e+02 |g_param|=1.05e+05 loss=3.5994e+00 ppl=36.58                                                
Validation - loss=3.4874e+00 ppl=32.70 best_loss=3.5401e+00 best_ppl=34.47                                              
Epoch 19 - |param|=3.04e+02 |g_param|=1.17e+05 loss=3.5828e+00 ppl=35.97                                                
Validation - loss=3.4354e+00 ppl=31.04 best_loss=3.4874e+00 best_ppl=32.70                                              
Epoch 20 - |param|=3.05e+02 |g_param|=1.20e+05 loss=3.4552e+00 ppl=31.67                                                
Validation - loss=3.3912e+00 ppl=29.70 best_loss=3.4354e+00 best_ppl=31.04                                              
Epoch 21 - |param|=3.05e+02 |g_param|=1.22e+05 loss=3.4436e+00 ppl=31.30                                                
Validation - loss=3.3581e+00 ppl=28.73 best_loss=3.3912e+00 best_ppl=29.70                                              
Epoch 22 - |param|=3.05e+02 |g_param|=1.17e+05 loss=3.4902e+00 ppl=32.79                                                
Validation - loss=3.3078e+00 ppl=27.32 best_loss=3.3581e+00 best_ppl=28.73                                              
Epoch 23 - |param|=3.05e+02 |g_param|=1.38e+05 loss=3.3823e+00 ppl=29.44                                                
Validation - loss=3.2801e+00 ppl=26.58 best_loss=3.3078e+00 best_ppl=27.32                                              
Epoch 24 - |param|=3.05e+02 |g_param|=1.32e+05 loss=3.3076e+00 ppl=27.32                                                
Validation - loss=3.2361e+00 ppl=25.43 best_loss=3.2801e+00 best_ppl=26.58                                              
Epoch 25 - |param|=3.05e+02 |g_param|=1.38e+05 loss=3.3329e+00 ppl=28.02                                                
Validation - loss=3.2041e+00 ppl=24.63 best_loss=3.2361e+00 best_ppl=25.43                                              
Epoch 26 - |param|=3.05e+02 |g_param|=1.38e+05 loss=3.3420e+00 ppl=28.27                                                
Validation - loss=3.1652e+00 ppl=23.69 best_loss=3.2041e+00 best_ppl=24.63                                              
Epoch 27 - |param|=3.05e+02 |g_param|=1.50e+05 loss=3.2643e+00 ppl=26.16                                                
Validation - loss=3.1474e+00 ppl=23.28 best_loss=3.1652e+00 best_ppl=23.69                                              
Epoch 28 - |param|=3.05e+02 |g_param|=1.35e+05 loss=3.2314e+00 ppl=25.32                                                
Validation - loss=3.1136e+00 ppl=22.50 best_loss=3.1474e+00 best_ppl=23.28                                              
Epoch 29 - |param|=3.05e+02 |g_param|=1.44e+05 loss=3.2004e+00 ppl=24.54                                                
Validation - loss=3.0839e+00 ppl=21.84 best_loss=3.1136e+00 best_ppl=22.50                                              
Epoch 30 - |param|=3.06e+02 |g_param|=1.36e+05 loss=3.2619e+00 ppl=26.10                                                
Validation - loss=3.0571e+00 ppl=21.27 best_loss=3.0839e+00 best_ppl=21.84                                              
Epoch 31 - |param|=3.06e+02 |g_param|=1.68e+05 loss=3.2347e+00 ppl=25.40                                                
Validation - loss=3.0363e+00 ppl=20.83 best_loss=3.0571e+00 best_ppl=21.27                                              
Epoch 32 - |param|=3.06e+02 |g_param|=1.66e+05 loss=3.1766e+00 ppl=23.96                                                
Validation - loss=3.0037e+00 ppl=20.16 best_loss=3.0363e+00 best_ppl=20.83                                              
Epoch 33 - |param|=3.06e+02 |g_param|=1.54e+05 loss=3.1974e+00 ppl=24.47                                                
Validation - loss=2.9818e+00 ppl=19.72 best_loss=3.0037e+00 best_ppl=20.16                                              
Epoch 34 - |param|=3.06e+02 |g_param|=1.54e+05 loss=3.1433e+00 ppl=23.18                                                
Validation - loss=2.9678e+00 ppl=19.45 best_loss=2.9818e+00 best_ppl=19.72                                              
Epoch 35 - |param|=3.06e+02 |g_param|=1.75e+05 loss=3.1288e+00 ppl=22.85                                                
Validation - loss=2.9567e+00 ppl=19.23 best_loss=2.9678e+00 best_ppl=19.45                                              
Epoch 36 - |param|=3.06e+02 |g_param|=1.49e+05 loss=3.1054e+00 ppl=22.32                                                
Validation - loss=2.9361e+00 ppl=18.84 best_loss=2.9567e+00 best_ppl=19.23                                              
Epoch 37 - |param|=3.06e+02 |g_param|=1.71e+05 loss=3.0796e+00 ppl=21.75                                                
Validation - loss=2.9055e+00 ppl=18.28 best_loss=2.9361e+00 best_ppl=18.84                                              
Epoch 38 - |param|=3.06e+02 |g_param|=1.54e+05 loss=3.0763e+00 ppl=21.68                                                
Validation - loss=2.8933e+00 ppl=18.05 best_loss=2.9055e+00 best_ppl=18.28                                              
Epoch 39 - |param|=3.06e+02 |g_param|=1.60e+05 loss=3.0248e+00 ppl=20.59                                                
Validation - loss=2.8793e+00 ppl=17.80 best_loss=2.8933e+00 best_ppl=18.05                                              
Epoch 40 - |param|=3.06e+02 |g_param|=1.87e+05 loss=3.0492e+00 ppl=21.10                                                
Validation - loss=2.8644e+00 ppl=17.54 best_loss=2.8793e+00 best_ppl=17.80                                              
Epoch 41 - |param|=3.07e+02 |g_param|=1.73e+05 loss=3.0337e+00 ppl=20.77                                                
Validation - loss=2.8500e+00 ppl=17.29 best_loss=2.8644e+00 best_ppl=17.54                                              
Epoch 42 - |param|=3.07e+02 |g_param|=1.76e+05 loss=3.0164e+00 ppl=20.42                                                
Validation - loss=2.8398e+00 ppl=17.11 best_loss=2.8500e+00 best_ppl=17.29                                              
Epoch 43 - |param|=3.07e+02 |g_param|=1.64e+05 loss=3.0078e+00 ppl=20.24                                                
Validation - loss=2.8175e+00 ppl=16.74 best_loss=2.8398e+00 best_ppl=17.11                                              
Epoch 44 - |param|=3.07e+02 |g_param|=1.60e+05 loss=2.9372e+00 ppl=18.86                                                
Validation - loss=2.8019e+00 ppl=16.48 best_loss=2.8175e+00 best_ppl=16.74                                              
Epoch 45 - |param|=3.07e+02 |g_param|=1.95e+05 loss=2.9857e+00 ppl=19.80                                                
Validation - loss=2.7917e+00 ppl=16.31 best_loss=2.8019e+00 best_ppl=16.48                                              
Epoch 46 - |param|=3.07e+02 |g_param|=1.62e+05 loss=2.9496e+00 ppl=19.10                                                
Validation - loss=2.7885e+00 ppl=16.26 best_loss=2.7917e+00 best_ppl=16.31                                              
Epoch 47 - |param|=3.07e+02 |g_param|=1.63e+05 loss=2.9604e+00 ppl=19.31                                                
Validation - loss=2.7632e+00 ppl=15.85 best_loss=2.7885e+00 best_ppl=16.26                                              
Epoch 48 - |param|=3.07e+02 |g_param|=1.87e+05 loss=2.8931e+00 ppl=18.05                                                
Validation - loss=2.7604e+00 ppl=15.81 best_loss=2.7632e+00 best_ppl=15.85                                              
Epoch 49 - |param|=3.07e+02 |g_param|=1.78e+05 loss=2.8929e+00 ppl=18.05                                                
Validation - loss=2.7421e+00 ppl=15.52 best_loss=2.7604e+00 best_ppl=15.81                                              
Epoch 50 - |param|=3.07e+02 |g_param|=1.78e+05 loss=2.8974e+00 ppl=18.13                                                
Validation - loss=2.7287e+00 ppl=15.31 best_loss=2.7421e+00 best_ppl=15.52                                              
Epoch 51 - |param|=3.07e+02 |g_param|=1.85e+05 loss=2.9316e+00 ppl=18.76                                                
Validation - loss=2.7294e+00 ppl=15.32 best_loss=2.7287e+00 best_ppl=15.31                                              
Epoch 52 - |param|=3.08e+02 |g_param|=1.77e+05 loss=2.9288e+00 ppl=18.70                                                
Validation - loss=2.7108e+00 ppl=15.04 best_loss=2.7287e+00 best_ppl=15.31                                              
Epoch 53 - |param|=3.08e+02 |g_param|=2.05e+05 loss=2.8384e+00 ppl=17.09                                                
Validation - loss=2.6978e+00 ppl=14.85 best_loss=2.7108e+00 best_ppl=15.04                                              
Epoch 54 - |param|=3.08e+02 |g_param|=1.74e+05 loss=2.8131e+00 ppl=16.66                                                
Validation - loss=2.6927e+00 ppl=14.77 best_loss=2.6978e+00 best_ppl=14.85                                              
Epoch 55 - |param|=3.08e+02 |g_param|=1.82e+05 loss=2.8574e+00 ppl=17.42                                                
Validation - loss=2.6782e+00 ppl=14.56 best_loss=2.6927e+00 best_ppl=14.77                                              
Epoch 56 - |param|=3.08e+02 |g_param|=2.02e+05 loss=2.8587e+00 ppl=17.44                                                
Validation - loss=2.6709e+00 ppl=14.45 best_loss=2.6782e+00 best_ppl=14.56                                              
Epoch 57 - |param|=3.08e+02 |g_param|=1.85e+05 loss=2.8859e+00 ppl=17.92                                                
Validation - loss=2.6712e+00 ppl=14.46 best_loss=2.6709e+00 best_ppl=14.45                                              
Epoch 58 - |param|=3.08e+02 |g_param|=1.91e+05 loss=2.8181e+00 ppl=16.74                                                
Validation - loss=2.6449e+00 ppl=14.08 best_loss=2.6709e+00 best_ppl=14.45                                              
Epoch 59 - |param|=3.08e+02 |g_param|=1.78e+05 loss=2.8136e+00 ppl=16.67                                                
Validation - loss=2.6431e+00 ppl=14.06 best_loss=2.6449e+00 best_ppl=14.08                                              
Epoch 60 - |param|=3.08e+02 |g_param|=1.83e+05 loss=2.8199e+00 ppl=16.78                                                
Validation - loss=2.6261e+00 ppl=13.82 best_loss=2.6431e+00 best_ppl=14.06                                              
Epoch 61 - |param|=3.08e+02 |g_param|=2.02e+05 loss=2.7986e+00 ppl=16.42                                                
Validation - loss=2.6145e+00 ppl=13.66 best_loss=2.6261e+00 best_ppl=13.82                                              
Epoch 62 - |param|=3.09e+02 |g_param|=1.87e+05 loss=2.7961e+00 ppl=16.38                                                
Validation - loss=2.6037e+00 ppl=13.51 best_loss=2.6145e+00 best_ppl=13.66                                              
Epoch 63 - |param|=3.09e+02 |g_param|=1.98e+05 loss=2.7724e+00 ppl=16.00                                                
Validation - loss=2.6102e+00 ppl=13.60 best_loss=2.6037e+00 best_ppl=13.51                                              
Epoch 64 - |param|=3.09e+02 |g_param|=2.20e+05 loss=2.8382e+00 ppl=17.08                                                
Validation - loss=2.5980e+00 ppl=13.44 best_loss=2.6037e+00 best_ppl=13.51                                              
Epoch 65 - |param|=3.09e+02 |g_param|=1.85e+05 loss=2.8527e+00 ppl=17.34                                                
Validation - loss=2.5883e+00 ppl=13.31 best_loss=2.5980e+00 best_ppl=13.44                                              
Epoch 66 - |param|=3.09e+02 |g_param|=2.02e+05 loss=2.7693e+00 ppl=15.95                                                
Validation - loss=2.5809e+00 ppl=13.21 best_loss=2.5883e+00 best_ppl=13.31                                              
Epoch 67 - |param|=3.09e+02 |g_param|=1.89e+05 loss=2.7939e+00 ppl=16.34                                                
Validation - loss=2.5750e+00 ppl=13.13 best_loss=2.5809e+00 best_ppl=13.21                                              
Epoch 68 - |param|=3.09e+02 |g_param|=1.84e+05 loss=2.7836e+00 ppl=16.18                                                
Validation - loss=2.5621e+00 ppl=12.96 best_loss=2.5750e+00 best_ppl=13.13                                              
Epoch 69 - |param|=3.09e+02 |g_param|=2.43e+05 loss=2.7348e+00 ppl=15.41                                                
Validation - loss=2.5614e+00 ppl=12.95 best_loss=2.5621e+00 best_ppl=12.96                                              
Epoch 70 - |param|=3.09e+02 |g_param|=1.99e+05 loss=2.7734e+00 ppl=16.01                                                
Validation - loss=2.5469e+00 ppl=12.77 best_loss=2.5614e+00 best_ppl=12.95                                              
Epoch 71 - |param|=3.09e+02 |g_param|=2.03e+05 loss=2.7170e+00 ppl=15.13                                                
Validation - loss=2.5382e+00 ppl=12.66 best_loss=2.5469e+00 best_ppl=12.77                                              
Epoch 72 - |param|=3.10e+02 |g_param|=2.14e+05 loss=2.6782e+00 ppl=14.56                                                
Validation - loss=2.5341e+00 ppl=12.60 best_loss=2.5382e+00 best_ppl=12.66                                              
Epoch 73 - |param|=3.10e+02 |g_param|=1.86e+05 loss=2.7376e+00 ppl=15.45                                                
Validation - loss=2.5310e+00 ppl=12.57 best_loss=2.5341e+00 best_ppl=12.60                                              
Epoch 74 - |param|=3.10e+02 |g_param|=2.05e+05 loss=2.6304e+00 ppl=13.88                                                
Validation - loss=2.5245e+00 ppl=12.48 best_loss=2.5310e+00 best_ppl=12.57                                              
Epoch 75 - |param|=3.10e+02 |g_param|=1.97e+05 loss=2.7255e+00 ppl=15.26                                                
Validation - loss=2.5160e+00 ppl=12.38 best_loss=2.5245e+00 best_ppl=12.48                                              
Epoch 76 - |param|=3.10e+02 |g_param|=2.00e+05 loss=2.7516e+00 ppl=15.67                                                
Validation - loss=2.5088e+00 ppl=12.29 best_loss=2.5160e+00 best_ppl=12.38                                              
Epoch 77 - |param|=3.10e+02 |g_param|=2.11e+05 loss=2.6547e+00 ppl=14.22                                                
Validation - loss=2.5074e+00 ppl=12.27 best_loss=2.5088e+00 best_ppl=12.29                                              
Epoch 78 - |param|=3.10e+02 |g_param|=2.14e+05 loss=2.7270e+00 ppl=15.29                                                
Validation - loss=2.4990e+00 ppl=12.17 best_loss=2.5074e+00 best_ppl=12.27                                              
Epoch 79 - |param|=3.10e+02 |g_param|=2.13e+05 loss=2.6732e+00 ppl=14.49                                                
Validation - loss=2.4894e+00 ppl=12.05 best_loss=2.4990e+00 best_ppl=12.17                                              
Epoch 80 - |param|=3.10e+02 |g_param|=2.17e+05 loss=2.7367e+00 ppl=15.44                                                
Validation - loss=2.4831e+00 ppl=11.98 best_loss=2.4894e+00 best_ppl=12.05                                              
Epoch 81 - |param|=3.10e+02 |g_param|=2.08e+05 loss=2.6601e+00 ppl=14.30                                                
Validation - loss=2.4828e+00 ppl=11.97 best_loss=2.4831e+00 best_ppl=11.98                                              
Epoch 82 - |param|=3.11e+02 |g_param|=2.05e+05 loss=2.6385e+00 ppl=13.99                                                
Validation - loss=2.4732e+00 ppl=11.86 best_loss=2.4828e+00 best_ppl=11.97                                              
Epoch 83 - |param|=3.11e+02 |g_param|=2.22e+05 loss=2.6140e+00 ppl=13.65                                                
Validation - loss=2.4645e+00 ppl=11.76 best_loss=2.4732e+00 best_ppl=11.86                                              
Epoch 84 - |param|=3.11e+02 |g_param|=2.21e+05 loss=2.6755e+00 ppl=14.52                                                
Validation - loss=2.4623e+00 ppl=11.73 best_loss=2.4645e+00 best_ppl=11.76                                              
Epoch 85 - |param|=3.11e+02 |g_param|=2.33e+05 loss=2.6375e+00 ppl=13.98                                                
Validation - loss=2.4498e+00 ppl=11.59 best_loss=2.4623e+00 best_ppl=11.73                                              
Epoch 86 - |param|=3.11e+02 |g_param|=1.98e+05 loss=2.6034e+00 ppl=13.51                                                
Validation - loss=2.4485e+00 ppl=11.57 best_loss=2.4498e+00 best_ppl=11.59                                              
Epoch 87 - |param|=3.11e+02 |g_param|=2.16e+05 loss=2.5993e+00 ppl=13.45                                                
Validation - loss=2.4393e+00 ppl=11.47 best_loss=2.4485e+00 best_ppl=11.57                                              
Epoch 88 - |param|=3.11e+02 |g_param|=2.43e+05 loss=2.6116e+00 ppl=13.62                                                
Validation - loss=2.4361e+00 ppl=11.43 best_loss=2.4393e+00 best_ppl=11.47                                              
Epoch 89 - |param|=3.11e+02 |g_param|=2.05e+05 loss=2.6186e+00 ppl=13.72                                                
Validation - loss=2.4303e+00 ppl=11.36 best_loss=2.4361e+00 best_ppl=11.43                                              
Epoch 90 - |param|=3.11e+02 |g_param|=2.08e+05 loss=2.5958e+00 ppl=13.41                                                
Validation - loss=2.4279e+00 ppl=11.34 best_loss=2.4303e+00 best_ppl=11.36                                              
Epoch 91 - |param|=3.11e+02 |g_param|=2.06e+05 loss=2.6650e+00 ppl=14.37                                                
Validation - loss=2.4215e+00 ppl=11.26 best_loss=2.4279e+00 best_ppl=11.34                                              
Epoch 92 - |param|=3.12e+02 |g_param|=2.11e+05 loss=2.5567e+00 ppl=12.89                                                
Validation - loss=2.4190e+00 ppl=11.23 best_loss=2.4215e+00 best_ppl=11.26                                              
Iteration:   1%|▉                                                                                | 1/87 [00:00<?, ?it/s]Epoch 93 - |param|=3.12e+02 |g_param|=2.29e+05 loss=2.5423e+00 ppl=12.71
Validation - loss=2.4168e+00 ppl=11.21 best_loss=2.4190e+00 best_ppl=11.23                                              
Epoch 94 - |param|=3.12e+02 |g_param|=2.42e+05 loss=2.6142e+00 ppl=13.66                                                
Validation - loss=2.4145e+00 ppl=11.18 best_loss=2.4168e+00 best_ppl=11.21                                              
Epoch 95 - |param|=3.12e+02 |g_param|=2.20e+05 loss=2.5631e+00 ppl=12.98                                                
Validation - loss=2.4011e+00 ppl=11.04 best_loss=2.4145e+00 best_ppl=11.18                                              
Epoch 96 - |param|=3.12e+02 |g_param|=2.30e+05 loss=2.5055e+00 ppl=12.25                                                
Validation - loss=2.4024e+00 ppl=11.05 best_loss=2.4011e+00 best_ppl=11.04                                              
Epoch 97 - |param|=3.12e+02 |g_param|=2.09e+05 loss=2.5325e+00 ppl=12.59                                                
Validation - loss=2.3935e+00 ppl=10.95 best_loss=2.4011e+00 best_ppl=11.04                                              
Epoch 98 - |param|=3.12e+02 |g_param|=2.25e+05 loss=2.5703e+00 ppl=13.07                                                
Validation - loss=2.3827e+00 ppl=10.83 best_loss=2.3935e+00 best_ppl=10.95                                              
Epoch 99 - |param|=3.12e+02 |g_param|=2.59e+05 loss=2.4787e+00 ppl=11.93                                                
Validation - loss=2.3937e+00 ppl=10.95 best_loss=2.3827e+00 best_ppl=10.83                                              
Epoch 100 - |param|=3.12e+02 |g_param|=2.13e+05 loss=2.4962e+00 ppl=12.14                                               
Validation - loss=2.3821e+00 ppl=10.83 best_loss=2.3827e+00 best_ppl=10.83                                              

real	33m21.003s
user	32m41.243s
sys	0m13.877s
(simple-nmt) ye@:~/exp/simple-nmt$
```

updating testing/evaluation bash script ...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, Thailand
# Last updated: 27 Mar 2022
# find all models and parse to translate.py for testing and multi-bleu.perl for evaluation with BLEU score
# updated for Transformer baseline my-bk

cd ./model/transformer/baseline/mybk-100epoch;

for i in *.pth; do
   MODEL=$i;

   # Testing
   python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 1 --lang mybk < /home/ye/exp/simple-nmt/data/my-bk/syl/test.my > $MODEL.hyp

   # Evaluation with BLEU Score
   echo "Evaluation result for the model: $MODEL" | tee -a eval-results-mybk-transformer-baseline-100epoch.txt;
   cat $MODEL.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/my-bk/syl/test.bk | tee  -a eval-results-mybk-transformer-baseline-100epoch.txt;

done

cd -;

```

Testing/Evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-loop-transformer-mybk.sh 
Evaluation result for the model: mybk-transformer-model.01.6.03-417.55.5.89-362.39.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.7/0.0/0.0/0.0 (BP=0.433, ratio=0.544, hyp_len=6222, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.02.5.47-238.05.5.33-206.31.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 27.8/0.5/0.0/0.0 (BP=0.173, ratio=0.363, hyp_len=4148, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.03.5.02-152.02.4.89-132.34.pth
BLEU = 0.00, 61.9/18.4/0.0/0.0 (BP=0.011, ratio=0.181, hyp_len=2074, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.04.4.76-116.17.4.65-104.54.pth
BLEU = 0.00, 61.9/18.4/0.0/0.0 (BP=0.011, ratio=0.181, hyp_len=2074, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.05.4.57-96.77.4.50-89.77.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 53.9/1.6/0.0/0.0 (BP=0.073, ratio=0.277, hyp_len=3162, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.06.4.43-83.73.4.37-79.23.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 43.1/1.1/0.0/0.0 (BP=0.200, ratio=0.384, hyp_len=4385, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.07.4.33-75.74.4.26-70.96.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 27.1/4.1/0.8/0.0 (BP=0.742, ratio=0.771, hyp_len=8809, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.08.4.22-67.88.4.14-62.80.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 31.8/6.2/1.0/0.0 (BP=0.677, ratio=0.719, hyp_len=8225, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.09.4.15-63.28.4.04-56.97.pth
BLEU = 1.06, 32.9/7.5/1.3/0.0 (BP=0.678, ratio=0.720, hyp_len=8230, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.100.2.50-12.14.2.38-10.83.pth
BLEU = 15.19, 40.8/19.7/10.9/6.1 (BP=1.000, ratio=1.074, hyp_len=12281, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.10.4.06-58.22.3.97-52.93.pth
BLEU = 2.07, 28.9/7.5/1.4/0.1 (BP=0.837, ratio=0.849, hyp_len=9705, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.11.3.95-51.73.3.89-48.75.pth
BLEU = 5.29, 25.5/8.3/3.4/1.5 (BP=0.919, ratio=0.922, hyp_len=10543, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.12.3.92-50.52.3.82-45.51.pth
BLEU = 5.03, 24.5/7.3/3.1/1.4 (BP=0.945, ratio=0.947, hyp_len=10822, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.13.3.81-45.30.3.75-42.40.pth
BLEU = 5.04, 22.7/7.0/3.0/1.4 (BP=1.000, ratio=1.043, hyp_len=11924, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.14.3.79-44.04.3.70-40.34.pth
BLEU = 4.40, 20.5/6.1/2.5/1.2 (BP=1.000, ratio=1.166, hyp_len=13330, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.15.3.69-40.15.3.65-38.42.pth
BLEU = 3.02, 15.0/4.2/1.7/0.8 (BP=1.000, ratio=1.574, hyp_len=17996, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.16.3.63-37.78.3.58-36.05.pth
BLEU = 2.76, 13.6/3.9/1.5/0.7 (BP=1.000, ratio=1.741, hyp_len=19899, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.17.3.61-36.82.3.54-34.47.pth
BLEU = 2.09, 10.6/2.9/1.1/0.5 (BP=1.000, ratio=2.236, hyp_len=25560, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.18.3.60-36.58.3.49-32.70.pth
BLEU = 2.20, 11.2/3.1/1.2/0.6 (BP=1.000, ratio=2.236, hyp_len=25561, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.19.3.58-35.97.3.44-31.04.pth
BLEU = 2.02, 10.4/2.9/1.1/0.5 (BP=1.000, ratio=2.345, hyp_len=26804, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.20.3.46-31.67.3.39-29.70.pth
BLEU = 1.62, 8.8/2.5/0.8/0.4 (BP=1.000, ratio=2.974, hyp_len=33995, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.21.3.44-31.30.3.36-28.73.pth
BLEU = 2.32, 12.2/3.4/1.2/0.6 (BP=1.000, ratio=2.153, hyp_len=24615, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.22.3.49-32.79.3.31-27.32.pth
BLEU = 2.00, 10.4/3.1/1.1/0.5 (BP=1.000, ratio=2.620, hyp_len=29954, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.23.3.38-29.44.3.28-26.58.pth
BLEU = 1.63, 8.7/2.5/0.9/0.4 (BP=1.000, ratio=3.048, hyp_len=34847, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.24.3.31-27.32.3.24-25.43.pth
BLEU = 2.02, 10.5/3.0/1.1/0.5 (BP=1.000, ratio=2.546, hyp_len=29111, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.25.3.33-28.02.3.20-24.63.pth
BLEU = 2.34, 11.8/3.6/1.3/0.5 (BP=1.000, ratio=2.334, hyp_len=26683, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.26.3.34-28.27.3.17-23.69.pth
BLEU = 2.14, 11.1/3.2/1.2/0.5 (BP=1.000, ratio=2.563, hyp_len=29300, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.27.3.26-26.16.3.15-23.28.pth
BLEU = 2.16, 10.9/3.3/1.2/0.5 (BP=1.000, ratio=2.699, hyp_len=30850, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.28.3.23-25.32.3.11-22.50.pth
BLEU = 2.27, 11.0/3.4/1.3/0.5 (BP=1.000, ratio=2.579, hyp_len=29478, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.29.3.20-24.54.3.08-21.84.pth
BLEU = 2.49, 12.3/3.8/1.4/0.6 (BP=1.000, ratio=2.420, hyp_len=27666, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.30.3.26-26.10.3.06-21.27.pth
BLEU = 3.01, 13.8/4.5/1.8/0.7 (BP=1.000, ratio=2.196, hyp_len=25102, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.31.3.23-25.40.3.04-20.83.pth
BLEU = 3.59, 16.3/5.4/2.2/0.9 (BP=1.000, ratio=1.873, hyp_len=21409, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.32.3.18-23.96.3.00-20.16.pth
BLEU = 2.76, 12.8/4.2/1.6/0.7 (BP=1.000, ratio=2.467, hyp_len=28205, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.33.3.20-24.47.2.98-19.72.pth
BLEU = 3.26, 14.7/5.0/2.0/0.8 (BP=1.000, ratio=2.226, hyp_len=25451, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.34.3.14-23.18.2.97-19.45.pth
BLEU = 5.40, 22.8/8.0/3.4/1.4 (BP=1.000, ratio=1.409, hyp_len=16113, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.35.3.13-22.85.2.96-19.23.pth
BLEU = 2.99, 13.4/4.5/1.8/0.7 (BP=1.000, ratio=2.416, hyp_len=27618, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.36.3.11-22.32.2.94-18.84.pth
BLEU = 4.57, 19.4/6.9/2.9/1.1 (BP=1.000, ratio=1.724, hyp_len=19708, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.37.3.08-21.75.2.91-18.28.pth
BLEU = 5.61, 23.2/8.4/3.6/1.4 (BP=1.000, ratio=1.469, hyp_len=16790, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.38.3.08-21.68.2.89-18.05.pth
BLEU = 5.15, 21.7/7.8/3.3/1.3 (BP=1.000, ratio=1.569, hyp_len=17942, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.39.3.02-20.59.2.88-17.80.pth
BLEU = 5.97, 23.9/8.9/3.9/1.5 (BP=1.000, ratio=1.441, hyp_len=16468, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.40.3.05-21.10.2.86-17.54.pth
BLEU = 5.09, 20.5/7.6/3.3/1.3 (BP=1.000, ratio=1.653, hyp_len=18892, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.41.3.03-20.77.2.85-17.29.pth
BLEU = 6.52, 25.6/9.6/4.3/1.7 (BP=1.000, ratio=1.383, hyp_len=15816, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.42.3.02-20.42.2.84-17.11.pth
BLEU = 5.99, 23.6/9.0/3.9/1.6 (BP=1.000, ratio=1.510, hyp_len=17260, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.43.3.01-20.24.2.82-16.74.pth
BLEU = 6.44, 24.8/9.5/4.2/1.7 (BP=1.000, ratio=1.435, hyp_len=16401, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.44.2.94-18.86.2.80-16.48.pth
BLEU = 7.02, 26.5/10.3/4.6/1.9 (BP=1.000, ratio=1.353, hyp_len=15473, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.45.2.99-19.80.2.79-16.31.pth
BLEU = 7.65, 28.6/11.4/5.1/2.0 (BP=1.000, ratio=1.284, hyp_len=14676, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.46.2.95-19.10.2.79-16.26.pth
BLEU = 7.33, 26.9/10.7/4.9/2.1 (BP=1.000, ratio=1.330, hyp_len=15208, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.47.2.96-19.31.2.76-15.85.pth
BLEU = 7.72, 28.0/11.0/5.1/2.3 (BP=1.000, ratio=1.320, hyp_len=15091, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.48.2.89-18.05.2.76-15.81.pth
BLEU = 8.64, 30.4/12.3/5.9/2.5 (BP=1.000, ratio=1.213, hyp_len=13872, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.49.2.89-18.05.2.74-15.52.pth
BLEU = 8.67, 30.2/12.2/5.9/2.6 (BP=1.000, ratio=1.223, hyp_len=13982, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.50.2.90-18.13.2.73-15.31.pth
BLEU = 8.80, 31.0/12.5/5.9/2.6 (BP=1.000, ratio=1.194, hyp_len=13649, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.51.2.93-18.76.2.73-15.32.pth
BLEU = 9.43, 32.5/13.3/6.3/2.9 (BP=1.000, ratio=1.145, hyp_len=13084, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.52.2.93-18.70.2.71-15.04.pth
BLEU = 8.81, 30.8/12.5/6.0/2.6 (BP=1.000, ratio=1.232, hyp_len=14085, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.53.2.84-17.09.2.70-14.85.pth
BLEU = 9.97, 34.1/14.0/6.8/3.1 (BP=1.000, ratio=1.092, hyp_len=12483, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.54.2.81-16.66.2.69-14.77.pth
BLEU = 8.97, 30.5/12.7/6.2/2.7 (BP=1.000, ratio=1.257, hyp_len=14368, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.55.2.86-17.42.2.68-14.56.pth
BLEU = 9.54, 32.7/13.6/6.4/2.9 (BP=1.000, ratio=1.155, hyp_len=13209, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.56.2.86-17.44.2.67-14.45.pth
BLEU = 10.64, 35.2/14.9/7.3/3.3 (BP=1.000, ratio=1.092, hyp_len=12488, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.57.2.89-17.92.2.67-14.46.pth
BLEU = 8.50, 29.9/12.2/5.7/2.5 (BP=1.000, ratio=1.260, hyp_len=14409, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.58.2.82-16.74.2.64-14.08.pth
BLEU = 10.44, 34.9/14.7/7.1/3.2 (BP=1.000, ratio=1.126, hyp_len=12869, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.59.2.81-16.67.2.64-14.06.pth
BLEU = 10.71, 35.2/15.0/7.3/3.4 (BP=1.000, ratio=1.115, hyp_len=12743, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.60.2.82-16.78.2.63-13.82.pth
BLEU = 10.48, 35.2/14.9/7.2/3.2 (BP=1.000, ratio=1.106, hyp_len=12641, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.61.2.80-16.42.2.61-13.66.pth
BLEU = 10.72, 34.5/14.9/7.5/3.4 (BP=1.000, ratio=1.134, hyp_len=12962, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.62.2.80-16.38.2.60-13.51.pth
BLEU = 10.43, 34.5/14.5/7.2/3.3 (BP=1.000, ratio=1.138, hyp_len=13015, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.63.2.77-16.00.2.61-13.60.pth
BLEU = 10.57, 35.2/14.9/7.3/3.3 (BP=1.000, ratio=1.106, hyp_len=12641, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.64.2.84-17.08.2.60-13.44.pth
BLEU = 11.14, 35.9/15.5/7.7/3.6 (BP=1.000, ratio=1.095, hyp_len=12515, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.65.2.85-17.34.2.59-13.31.pth
BLEU = 10.92, 35.9/15.2/7.5/3.5 (BP=1.000, ratio=1.088, hyp_len=12436, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.66.2.77-15.95.2.58-13.21.pth
BLEU = 9.60, 31.9/13.4/6.6/3.0 (BP=1.000, ratio=1.220, hyp_len=13942, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.67.2.79-16.34.2.57-13.13.pth
BLEU = 10.59, 34.7/14.7/7.3/3.4 (BP=1.000, ratio=1.138, hyp_len=13011, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.68.2.78-16.18.2.56-12.96.pth
BLEU = 11.50, 37.1/16.0/7.9/3.7 (BP=1.000, ratio=1.088, hyp_len=12438, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.69.2.73-15.41.2.56-12.95.pth
BLEU = 11.74, 37.5/16.4/8.1/3.8 (BP=1.000, ratio=1.066, hyp_len=12181, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.70.2.77-16.01.2.55-12.77.pth
BLEU = 12.02, 37.5/16.5/8.4/4.0 (BP=1.000, ratio=1.082, hyp_len=12365, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.71.2.72-15.13.2.54-12.66.pth
BLEU = 11.56, 36.5/15.9/8.0/3.8 (BP=1.000, ratio=1.123, hyp_len=12835, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.72.2.68-14.56.2.53-12.60.pth
BLEU = 11.33, 35.7/15.7/7.9/3.7 (BP=1.000, ratio=1.131, hyp_len=12934, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.73.2.74-15.45.2.53-12.57.pth
BLEU = 12.54, 38.7/17.2/8.7/4.3 (BP=1.000, ratio=1.041, hyp_len=11899, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.74.2.63-13.88.2.52-12.48.pth
BLEU = 11.43, 36.2/15.6/7.9/3.8 (BP=1.000, ratio=1.105, hyp_len=12633, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.75.2.73-15.26.2.52-12.38.pth
BLEU = 11.90, 37.1/16.3/8.3/4.0 (BP=1.000, ratio=1.088, hyp_len=12435, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.76.2.75-15.67.2.51-12.29.pth
BLEU = 12.39, 37.6/16.8/8.6/4.3 (BP=1.000, ratio=1.087, hyp_len=12421, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.77.2.65-14.22.2.51-12.27.pth
BLEU = 13.56, 39.4/18.1/9.6/4.9 (BP=1.000, ratio=1.052, hyp_len=12032, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.78.2.73-15.29.2.50-12.17.pth
BLEU = 12.68, 38.4/17.2/8.7/4.5 (BP=1.000, ratio=1.080, hyp_len=12352, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.79.2.67-14.49.2.49-12.05.pth
BLEU = 12.31, 37.0/16.7/8.6/4.3 (BP=1.000, ratio=1.117, hyp_len=12768, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.80.2.74-15.44.2.48-11.98.pth
BLEU = 13.35, 39.4/17.9/9.5/4.8 (BP=1.000, ratio=1.065, hyp_len=12177, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.81.2.66-14.30.2.48-11.97.pth
BLEU = 13.19, 39.9/18.0/9.3/4.5 (BP=1.000, ratio=1.025, hyp_len=11720, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.82.2.64-13.99.2.47-11.86.pth
BLEU = 13.82, 40.3/18.6/9.8/5.0 (BP=1.000, ratio=1.037, hyp_len=11852, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.83.2.61-13.65.2.46-11.76.pth
BLEU = 12.98, 38.0/17.4/9.2/4.7 (BP=1.000, ratio=1.074, hyp_len=12283, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.84.2.68-14.52.2.46-11.73.pth
BLEU = 13.83, 40.2/18.5/9.9/5.0 (BP=1.000, ratio=1.041, hyp_len=11901, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.85.2.64-13.98.2.45-11.59.pth
BLEU = 13.30, 39.1/18.0/9.4/4.7 (BP=1.000, ratio=1.092, hyp_len=12481, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.86.2.60-13.51.2.45-11.57.pth
BLEU = 12.82, 38.1/17.4/9.0/4.5 (BP=1.000, ratio=1.106, hyp_len=12639, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.87.2.60-13.45.2.44-11.47.pth
BLEU = 13.90, 39.8/18.5/9.8/5.2 (BP=1.000, ratio=1.070, hyp_len=12234, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.88.2.61-13.62.2.44-11.43.pth
BLEU = 13.96, 40.2/18.6/9.9/5.1 (BP=1.000, ratio=1.087, hyp_len=12423, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.89.2.62-13.72.2.43-11.36.pth
BLEU = 13.73, 39.4/18.4/9.7/5.1 (BP=1.000, ratio=1.084, hyp_len=12396, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.90.2.60-13.41.2.43-11.34.pth
BLEU = 13.82, 39.5/18.6/9.8/5.1 (BP=1.000, ratio=1.080, hyp_len=12346, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.91.2.66-14.37.2.42-11.26.pth
BLEU = 14.34, 40.2/19.0/10.2/5.4 (BP=1.000, ratio=1.084, hyp_len=12397, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.92.2.56-12.89.2.42-11.23.pth
BLEU = 14.45, 41.4/19.4/10.3/5.3 (BP=1.000, ratio=1.028, hyp_len=11757, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.93.2.54-12.71.2.42-11.21.pth
BLEU = 14.63, 41.0/19.5/10.5/5.5 (BP=1.000, ratio=1.068, hyp_len=12209, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.94.2.61-13.66.2.41-11.18.pth
BLEU = 14.87, 40.9/19.7/10.6/5.7 (BP=1.000, ratio=1.080, hyp_len=12352, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.95.2.56-12.98.2.40-11.04.pth
BLEU = 14.81, 41.2/19.5/10.6/5.7 (BP=1.000, ratio=1.063, hyp_len=12157, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.96.2.51-12.25.2.40-11.05.pth
BLEU = 14.75, 40.2/19.1/10.5/5.9 (BP=1.000, ratio=1.065, hyp_len=12178, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.97.2.53-12.59.2.39-10.95.pth
BLEU = 15.42, 41.2/20.0/11.1/6.2 (BP=1.000, ratio=1.061, hyp_len=12132, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.98.2.57-13.07.2.38-10.83.pth
BLEU = 15.80, 43.1/20.9/11.3/6.1 (BP=1.000, ratio=1.037, hyp_len=11856, ref_len=11432)
Evaluation result for the model: mybk-transformer-model.99.2.48-11.93.2.39-10.95.pth
BLEU = 14.67, 40.1/19.3/10.5/5.7 (BP=1.000, ratio=1.068, hyp_len=12212, ref_len=11432)
/home/ye/exp/simple-nmt

real	40m32.726s
user	37m34.376s
sys	2m25.748s
(simple-nmt) ye@:~/exp/simple-nmt$
```

Best model က 98 epoch model ဖြစ်ပြီးတော့ Best BLEU Score က 15.80  

## Preparing Transformer Baseline for Beik-Myanmar

Training ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python train.py --train /home/ye/exp/simple-nmt/data/my-bk/syl/train --valid /home/ye/exp/simple-nmt/data/my-bk/syl/dev --lang bkmy --gpu_id 1 --batch_size 16 --n_epochs 100 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/bkmy-100epoch/bkmy-transformer-model.pth | tee ./model/transformer/baseline/bkmy-100epoch/bkmy-transformer-baseline-training.log
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 32,
    'init_epoch': 1,
    'iteration_per_update': 32,
    'lang': 'bkmy',
    'lr': 0.001,
    'lr_decay_start': 10,
    'lr_gamma': 0.5,
    'lr_step': 0,
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/transformer/baseline/bkmy-100epoch/bkmy-transformer-model.pth',
    'n_epochs': 100,
    'n_layers': 6,
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
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/my-bk/syl/dev',
    'verbose': 2,
    'word_vec_size': 512}
Transformer(
  (emb_enc): Embedding(1468, 32)
  (emb_dec): Embedding(1315, 32)
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
    (1): Linear(in_features=32, out_features=1315, bias=True)
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
Epoch 1 - |param|=3.01e+02 |g_param|=3.18e+05 loss=5.9272e+00 ppl=375.10                                                
Validation - loss=5.7850e+00 ppl=325.39 best_loss=inf best_ppl=inf                                                      
Epoch 2 - |param|=3.01e+02 |g_param|=3.23e+05 loss=5.2912e+00 ppl=198.59                                                
Validation - loss=5.2175e+00 ppl=184.48 best_loss=5.7850e+00 best_ppl=325.39                                            
Epoch 3 - |param|=3.01e+02 |g_param|=3.06e+05 loss=4.8644e+00 ppl=129.60                                                
Validation - loss=4.7709e+00 ppl=118.02 best_loss=5.2175e+00 best_ppl=184.48                                            
Epoch 4 - |param|=3.01e+02 |g_param|=2.44e+05 loss=4.5404e+00 ppl=93.72                                                 
Validation - loss=4.4840e+00 ppl=88.59 best_loss=4.7709e+00 best_ppl=118.02                                             
Epoch 5 - |param|=3.01e+02 |g_param|=2.24e+05 loss=4.3278e+00 ppl=75.78                                                 
Validation - loss=4.2816e+00 ppl=72.35 best_loss=4.4840e+00 best_ppl=88.59                                              
Epoch 6 - |param|=3.01e+02 |g_param|=1.92e+05 loss=4.1269e+00 ppl=61.99                                                 
Validation - loss=4.1234e+00 ppl=61.77 best_loss=4.2816e+00 best_ppl=72.35                                              
Epoch 7 - |param|=3.01e+02 |g_param|=1.61e+05 loss=4.0293e+00 ppl=56.22                                                 
Validation - loss=3.9825e+00 ppl=53.65 best_loss=4.1234e+00 best_ppl=61.77                                              
Epoch 8 - |param|=3.01e+02 |g_param|=1.66e+05 loss=3.8345e+00 ppl=46.27                                                 
Validation - loss=3.8480e+00 ppl=46.90 best_loss=3.9825e+00 best_ppl=53.65                                              
Epoch 9 - |param|=3.01e+02 |g_param|=1.37e+05 loss=3.7631e+00 ppl=43.08                                                 
Validation - loss=3.7434e+00 ppl=42.24 best_loss=3.8480e+00 best_ppl=46.90                                              
Epoch 10 - |param|=3.01e+02 |g_param|=1.40e+05 loss=3.6552e+00 ppl=38.68                                                
Validation - loss=3.6520e+00 ppl=38.55 best_loss=3.7434e+00 best_ppl=42.24                                              
Epoch 11 - |param|=3.01e+02 |g_param|=1.24e+05 loss=3.5600e+00 ppl=35.16                                                
Validation - loss=3.5658e+00 ppl=35.37 best_loss=3.6520e+00 best_ppl=38.55                                              
Epoch 12 - |param|=3.01e+02 |g_param|=1.10e+05 loss=3.5179e+00 ppl=33.72                                                
Validation - loss=3.4960e+00 ppl=32.98 best_loss=3.5658e+00 best_ppl=35.37                                              
Epoch 13 - |param|=3.01e+02 |g_param|=1.33e+05 loss=3.4226e+00 ppl=30.65                                                
Validation - loss=3.4362e+00 ppl=31.07 best_loss=3.4960e+00 best_ppl=32.98                                              
Epoch 14 - |param|=3.02e+02 |g_param|=1.16e+05 loss=3.3746e+00 ppl=29.21                                                
Validation - loss=3.3739e+00 ppl=29.19 best_loss=3.4362e+00 best_ppl=31.07                                              
Epoch 15 - |param|=3.02e+02 |g_param|=1.19e+05 loss=3.3005e+00 ppl=27.13                                                
Validation - loss=3.3242e+00 ppl=27.78 best_loss=3.3739e+00 best_ppl=29.19                                              
Epoch 16 - |param|=3.02e+02 |g_param|=1.46e+05 loss=3.2423e+00 ppl=25.59                                                
Validation - loss=3.2760e+00 ppl=26.47 best_loss=3.3242e+00 best_ppl=27.78                                              
Epoch 17 - |param|=3.02e+02 |g_param|=1.22e+05 loss=3.2732e+00 ppl=26.40                                                
Validation - loss=3.2323e+00 ppl=25.34 best_loss=3.2760e+00 best_ppl=26.47                                              
Epoch 18 - |param|=3.02e+02 |g_param|=1.24e+05 loss=3.2236e+00 ppl=25.12                                                
Validation - loss=3.1927e+00 ppl=24.35 best_loss=3.2323e+00 best_ppl=25.34                                              
Epoch 19 - |param|=3.02e+02 |g_param|=1.31e+05 loss=3.1983e+00 ppl=24.49                                                
Validation - loss=3.1557e+00 ppl=23.47 best_loss=3.1927e+00 best_ppl=24.35                                              
Epoch 20 - |param|=3.02e+02 |g_param|=1.32e+05 loss=3.1428e+00 ppl=23.17                                                
Validation - loss=3.1248e+00 ppl=22.75 best_loss=3.1557e+00 best_ppl=23.47                                              
Epoch 21 - |param|=3.02e+02 |g_param|=1.39e+05 loss=3.1236e+00 ppl=22.73                                                
Validation - loss=3.0961e+00 ppl=22.11 best_loss=3.1248e+00 best_ppl=22.75                                              
Epoch 22 - |param|=3.02e+02 |g_param|=1.28e+05 loss=3.1068e+00 ppl=22.35                                                
Validation - loss=3.0609e+00 ppl=21.35 best_loss=3.0961e+00 best_ppl=22.11                                              
Epoch 23 - |param|=3.02e+02 |g_param|=1.42e+05 loss=3.0553e+00 ppl=21.23                                                
Validation - loss=3.0291e+00 ppl=20.68 best_loss=3.0609e+00 best_ppl=21.35                                              
Epoch 24 - |param|=3.03e+02 |g_param|=1.56e+05 loss=3.0349e+00 ppl=20.80                                                
Validation - loss=2.9992e+00 ppl=20.07 best_loss=3.0291e+00 best_ppl=20.68                                              
Epoch 25 - |param|=3.03e+02 |g_param|=1.34e+05 loss=2.9623e+00 ppl=19.34                                                
Validation - loss=2.9853e+00 ppl=19.79 best_loss=2.9992e+00 best_ppl=20.07                                              
Epoch 26 - |param|=3.03e+02 |g_param|=1.37e+05 loss=2.9312e+00 ppl=18.75                                                
Validation - loss=2.9555e+00 ppl=19.21 best_loss=2.9853e+00 best_ppl=19.79                                              
Epoch 27 - |param|=3.03e+02 |g_param|=1.42e+05 loss=2.9198e+00 ppl=18.54                                                
Validation - loss=2.9348e+00 ppl=18.82 best_loss=2.9555e+00 best_ppl=19.21                                              
Epoch 28 - |param|=3.03e+02 |g_param|=1.61e+05 loss=2.9369e+00 ppl=18.86                                                
Validation - loss=2.9181e+00 ppl=18.51 best_loss=2.9348e+00 best_ppl=18.82                                              
Epoch 29 - |param|=3.03e+02 |g_param|=1.65e+05 loss=2.8984e+00 ppl=18.15                                                
Validation - loss=2.8795e+00 ppl=17.81 best_loss=2.9181e+00 best_ppl=18.51                                              
Epoch 30 - |param|=3.03e+02 |g_param|=1.42e+05 loss=2.8990e+00 ppl=18.16                                                
Validation - loss=2.8678e+00 ppl=17.60 best_loss=2.8795e+00 best_ppl=17.81                                              
Epoch 31 - |param|=3.03e+02 |g_param|=1.58e+05 loss=2.8503e+00 ppl=17.29                                                
Validation - loss=2.8339e+00 ppl=17.01 best_loss=2.8678e+00 best_ppl=17.60                                              
Epoch 32 - |param|=3.03e+02 |g_param|=1.86e+05 loss=2.8520e+00 ppl=17.32                                                
Validation - loss=2.8221e+00 ppl=16.81 best_loss=2.8339e+00 best_ppl=17.01                                              
Epoch 33 - |param|=3.03e+02 |g_param|=1.52e+05 loss=2.7665e+00 ppl=15.90                                                
Validation - loss=2.8059e+00 ppl=16.54 best_loss=2.8221e+00 best_ppl=16.81                                              
Epoch 34 - |param|=3.04e+02 |g_param|=1.74e+05 loss=2.7685e+00 ppl=15.93                                                
Validation - loss=2.7935e+00 ppl=16.34 best_loss=2.8059e+00 best_ppl=16.54                                              
Epoch 35 - |param|=3.04e+02 |g_param|=1.71e+05 loss=2.7530e+00 ppl=15.69                                                
Validation - loss=2.7676e+00 ppl=15.92 best_loss=2.7935e+00 best_ppl=16.34                                              
Epoch 36 - |param|=3.04e+02 |g_param|=1.63e+05 loss=2.8121e+00 ppl=16.64                                                
Validation - loss=2.7407e+00 ppl=15.50 best_loss=2.7676e+00 best_ppl=15.92                                              
Epoch 37 - |param|=3.04e+02 |g_param|=1.84e+05 loss=2.7833e+00 ppl=16.17                                                
Validation - loss=2.7253e+00 ppl=15.26 best_loss=2.7407e+00 best_ppl=15.50                                              
Epoch 38 - |param|=3.04e+02 |g_param|=1.65e+05 loss=2.7308e+00 ppl=15.34                                                
Validation - loss=2.7176e+00 ppl=15.14 best_loss=2.7253e+00 best_ppl=15.26                                              
Epoch 39 - |param|=3.04e+02 |g_param|=1.78e+05 loss=2.7543e+00 ppl=15.71                                                
Validation - loss=2.6983e+00 ppl=14.85 best_loss=2.7176e+00 best_ppl=15.14                                              
Epoch 40 - |param|=3.04e+02 |g_param|=2.01e+05 loss=2.7427e+00 ppl=15.53                                                
Validation - loss=2.6938e+00 ppl=14.79 best_loss=2.6983e+00 best_ppl=14.85                                              
Epoch 41 - |param|=3.04e+02 |g_param|=1.56e+05 loss=2.6872e+00 ppl=14.69                                                
Validation - loss=2.6787e+00 ppl=14.57 best_loss=2.6938e+00 best_ppl=14.79                                              
Epoch 42 - |param|=3.04e+02 |g_param|=1.73e+05 loss=2.7412e+00 ppl=15.51                                                
Validation - loss=2.6596e+00 ppl=14.29 best_loss=2.6787e+00 best_ppl=14.57                                              
Epoch 43 - |param|=3.05e+02 |g_param|=1.88e+05 loss=2.6489e+00 ppl=14.14                                                
Validation - loss=2.6457e+00 ppl=14.09 best_loss=2.6596e+00 best_ppl=14.29                                              
Epoch 44 - |param|=3.05e+02 |g_param|=1.79e+05 loss=2.6482e+00 ppl=14.13                                                
Validation - loss=2.6441e+00 ppl=14.07 best_loss=2.6457e+00 best_ppl=14.09                                              
Epoch 45 - |param|=3.05e+02 |g_param|=1.74e+05 loss=2.6433e+00 ppl=14.06                                                
Validation - loss=2.6270e+00 ppl=13.83 best_loss=2.6441e+00 best_ppl=14.07                                              
Epoch 46 - |param|=3.05e+02 |g_param|=1.71e+05 loss=2.6660e+00 ppl=14.38                                                
Validation - loss=2.6231e+00 ppl=13.78 best_loss=2.6270e+00 best_ppl=13.83                                              
Epoch 47 - |param|=3.05e+02 |g_param|=1.89e+05 loss=2.7101e+00 ppl=15.03                                                
Validation - loss=2.6045e+00 ppl=13.52 best_loss=2.6231e+00 best_ppl=13.78                                              
Epoch 48 - |param|=3.05e+02 |g_param|=2.01e+05 loss=2.5658e+00 ppl=13.01                                                
Validation - loss=2.5854e+00 ppl=13.27 best_loss=2.6045e+00 best_ppl=13.52                                              
Epoch 49 - |param|=3.05e+02 |g_param|=1.73e+05 loss=2.6306e+00 ppl=13.88                                                
Validation - loss=2.5768e+00 ppl=13.16 best_loss=2.5854e+00 best_ppl=13.27                                              
Epoch 50 - |param|=3.05e+02 |g_param|=1.84e+05 loss=2.5735e+00 ppl=13.11                                                
Validation - loss=2.5659e+00 ppl=13.01 best_loss=2.5768e+00 best_ppl=13.16                                              
Epoch 51 - |param|=3.05e+02 |g_param|=1.73e+05 loss=2.5959e+00 ppl=13.41                                                
Validation - loss=2.5736e+00 ppl=13.11 best_loss=2.5659e+00 best_ppl=13.01                                              
Epoch 52 - |param|=3.05e+02 |g_param|=1.79e+05 loss=2.5915e+00 ppl=13.35                                                
Validation - loss=2.5692e+00 ppl=13.06 best_loss=2.5659e+00 best_ppl=13.01                                              
Epoch 53 - |param|=3.06e+02 |g_param|=1.95e+05 loss=2.5982e+00 ppl=13.44                                                
Validation - loss=2.5494e+00 ppl=12.80 best_loss=2.5659e+00 best_ppl=13.01                                              
Epoch 54 - |param|=3.06e+02 |g_param|=2.05e+05 loss=2.5481e+00 ppl=12.78                                                
Validation - loss=2.5435e+00 ppl=12.72 best_loss=2.5494e+00 best_ppl=12.80                                              
Epoch 55 - |param|=3.06e+02 |g_param|=1.82e+05 loss=2.5981e+00 ppl=13.44                                                
Validation - loss=2.5341e+00 ppl=12.60 best_loss=2.5435e+00 best_ppl=12.72                                              
Epoch 56 - |param|=3.06e+02 |g_param|=1.97e+05 loss=2.5731e+00 ppl=13.11                                                
Validation - loss=2.5205e+00 ppl=12.44 best_loss=2.5341e+00 best_ppl=12.60                                              
Epoch 57 - |param|=3.06e+02 |g_param|=1.86e+05 loss=2.5357e+00 ppl=12.63                                                
Validation - loss=2.5126e+00 ppl=12.34 best_loss=2.5205e+00 best_ppl=12.44                                              
Epoch 58 - |param|=3.06e+02 |g_param|=2.01e+05 loss=2.5164e+00 ppl=12.38                                                
Validation - loss=2.5120e+00 ppl=12.33 best_loss=2.5126e+00 best_ppl=12.34                                              
Epoch 59 - |param|=3.06e+02 |g_param|=1.95e+05 loss=2.5240e+00 ppl=12.48                                                
Validation - loss=2.5019e+00 ppl=12.21 best_loss=2.5120e+00 best_ppl=12.33                                              
Epoch 60 - |param|=3.06e+02 |g_param|=1.91e+05 loss=2.5113e+00 ppl=12.32                                                
Validation - loss=2.5018e+00 ppl=12.20 best_loss=2.5019e+00 best_ppl=12.21                                              
Epoch 61 - |param|=3.06e+02 |g_param|=2.05e+05 loss=2.4755e+00 ppl=11.89                                                
Validation - loss=2.4933e+00 ppl=12.10 best_loss=2.5018e+00 best_ppl=12.20                                              
Epoch 62 - |param|=3.07e+02 |g_param|=1.92e+05 loss=2.4886e+00 ppl=12.04                                                
Validation - loss=2.4811e+00 ppl=11.95 best_loss=2.4933e+00 best_ppl=12.10                                              
Epoch 63 - |param|=3.07e+02 |g_param|=1.88e+05 loss=2.4773e+00 ppl=11.91                                                
Validation - loss=2.4729e+00 ppl=11.86 best_loss=2.4811e+00 best_ppl=11.95                                              
Epoch 64 - |param|=3.07e+02 |g_param|=2.34e+05 loss=2.5047e+00 ppl=12.24                                                
Validation - loss=2.4645e+00 ppl=11.76 best_loss=2.4729e+00 best_ppl=11.86                                              
Epoch 65 - |param|=3.07e+02 |g_param|=1.97e+05 loss=2.5249e+00 ppl=12.49                                                
Validation - loss=2.4560e+00 ppl=11.66 best_loss=2.4645e+00 best_ppl=11.76                                              
Epoch 66 - |param|=3.07e+02 |g_param|=2.12e+05 loss=2.5332e+00 ppl=12.59                                                
Validation - loss=2.4512e+00 ppl=11.60 best_loss=2.4560e+00 best_ppl=11.66                                              
Epoch 67 - |param|=3.07e+02 |g_param|=2.03e+05 loss=2.4789e+00 ppl=11.93                                                
Validation - loss=2.4405e+00 ppl=11.48 best_loss=2.4512e+00 best_ppl=11.60                                              
Epoch 68 - |param|=3.07e+02 |g_param|=2.04e+05 loss=2.4317e+00 ppl=11.38                                                
Validation - loss=2.4386e+00 ppl=11.46 best_loss=2.4405e+00 best_ppl=11.48                                              
Epoch 69 - |param|=3.07e+02 |g_param|=2.15e+05 loss=2.4210e+00 ppl=11.26                                                
Validation - loss=2.4437e+00 ppl=11.52 best_loss=2.4386e+00 best_ppl=11.46                                              
Epoch 70 - |param|=3.07e+02 |g_param|=2.02e+05 loss=2.3782e+00 ppl=10.79                                                
Validation - loss=2.4460e+00 ppl=11.54 best_loss=2.4386e+00 best_ppl=11.46                                              
Epoch 71 - |param|=3.08e+02 |g_param|=2.26e+05 loss=2.4326e+00 ppl=11.39                                                
Validation - loss=2.4214e+00 ppl=11.26 best_loss=2.4386e+00 best_ppl=11.46                                              
Epoch 72 - |param|=3.08e+02 |g_param|=2.32e+05 loss=2.4111e+00 ppl=11.15                                                
Validation - loss=2.4131e+00 ppl=11.17 best_loss=2.4214e+00 best_ppl=11.26                                              
Epoch 73 - |param|=3.08e+02 |g_param|=2.01e+05 loss=2.4051e+00 ppl=11.08                                                
Validation - loss=2.4108e+00 ppl=11.14 best_loss=2.4131e+00 best_ppl=11.17                                              
Epoch 74 - |param|=3.08e+02 |g_param|=2.19e+05 loss=2.4414e+00 ppl=11.49                                                
Validation - loss=2.4130e+00 ppl=11.17 best_loss=2.4108e+00 best_ppl=11.14                                              
Epoch 75 - |param|=3.08e+02 |g_param|=2.30e+05 loss=2.4213e+00 ppl=11.26                                                
Validation - loss=2.4057e+00 ppl=11.09 best_loss=2.4108e+00 best_ppl=11.14                                              
Epoch 76 - |param|=3.08e+02 |g_param|=2.07e+05 loss=2.4140e+00 ppl=11.18                                                
Validation - loss=2.3908e+00 ppl=10.92 best_loss=2.4057e+00 best_ppl=11.09                                              
Epoch 77 - |param|=3.08e+02 |g_param|=2.25e+05 loss=2.3657e+00 ppl=10.65                                                
Validation - loss=2.3921e+00 ppl=10.94 best_loss=2.3908e+00 best_ppl=10.92                                              
Epoch 78 - |param|=3.08e+02 |g_param|=2.03e+05 loss=2.4535e+00 ppl=11.63                                                
Validation - loss=2.3870e+00 ppl=10.88 best_loss=2.3908e+00 best_ppl=10.92                                              
Epoch 79 - |param|=3.08e+02 |g_param|=2.12e+05 loss=2.3830e+00 ppl=10.84                                                
Validation - loss=2.3819e+00 ppl=10.83 best_loss=2.3870e+00 best_ppl=10.88                                              
Epoch 80 - |param|=3.09e+02 |g_param|=2.24e+05 loss=2.3286e+00 ppl=10.26                                                
Validation - loss=2.3824e+00 ppl=10.83 best_loss=2.3819e+00 best_ppl=10.83                                              
Epoch 81 - |param|=3.09e+02 |g_param|=1.97e+05 loss=2.3369e+00 ppl=10.35                                                
Validation - loss=2.3712e+00 ppl=10.71 best_loss=2.3819e+00 best_ppl=10.83                                              
Epoch 82 - |param|=3.09e+02 |g_param|=2.16e+05 loss=2.3443e+00 ppl=10.43                                                
Validation - loss=2.3676e+00 ppl=10.67 best_loss=2.3712e+00 best_ppl=10.71                                              
Epoch 83 - |param|=3.09e+02 |g_param|=2.24e+05 loss=2.3866e+00 ppl=10.88                                                
Validation - loss=2.3603e+00 ppl=10.59 best_loss=2.3676e+00 best_ppl=10.67                                              
Epoch 84 - |param|=3.09e+02 |g_param|=2.11e+05 loss=2.3449e+00 ppl=10.43                                                
Validation - loss=2.3513e+00 ppl=10.50 best_loss=2.3603e+00 best_ppl=10.59                                              
Epoch 85 - |param|=3.09e+02 |g_param|=2.34e+05 loss=2.3842e+00 ppl=10.85                                                
Validation - loss=2.3485e+00 ppl=10.47 best_loss=2.3513e+00 best_ppl=10.50                                              
Epoch 86 - |param|=3.09e+02 |g_param|=2.16e+05 loss=2.3382e+00 ppl=10.36                                                
Validation - loss=2.3396e+00 ppl=10.38 best_loss=2.3485e+00 best_ppl=10.47                                              
Epoch 87 - |param|=3.09e+02 |g_param|=2.18e+05 loss=2.3698e+00 ppl=10.70                                                
Validation - loss=2.3368e+00 ppl=10.35 best_loss=2.3396e+00 best_ppl=10.38                                              
Epoch 88 - |param|=3.09e+02 |g_param|=2.35e+05 loss=2.3242e+00 ppl=10.22                                                
Validation - loss=2.3340e+00 ppl=10.32 best_loss=2.3368e+00 best_ppl=10.35                                              
Epoch 89 - |param|=3.10e+02 |g_param|=2.20e+05 loss=2.2869e+00 ppl=9.84                                                 
Validation - loss=2.3428e+00 ppl=10.41 best_loss=2.3340e+00 best_ppl=10.32                                              
Epoch 90 - |param|=3.10e+02 |g_param|=2.32e+05 loss=2.2808e+00 ppl=9.78                                                 
Validation - loss=2.3355e+00 ppl=10.34 best_loss=2.3340e+00 best_ppl=10.32                                              
Epoch 91 - |param|=3.10e+02 |g_param|=2.24e+05 loss=2.3275e+00 ppl=10.25                                                
Validation - loss=2.3324e+00 ppl=10.30 best_loss=2.3340e+00 best_ppl=10.32                                              
Epoch 92 - |param|=3.10e+02 |g_param|=2.27e+05 loss=2.3463e+00 ppl=10.45                                                
Validation - loss=2.3186e+00 ppl=10.16 best_loss=2.3324e+00 best_ppl=10.30                                              
Epoch 93 - |param|=3.10e+02 |g_param|=2.24e+05 loss=2.3319e+00 ppl=10.30                                                
Validation - loss=2.3113e+00 ppl=10.09 best_loss=2.3186e+00 best_ppl=10.16                                              
Epoch 94 - |param|=3.10e+02 |g_param|=2.24e+05 loss=2.3005e+00 ppl=9.98                                                 
Validation - loss=2.3103e+00 ppl=10.08 best_loss=2.3113e+00 best_ppl=10.09                                              
Epoch 95 - |param|=3.10e+02 |g_param|=2.43e+05 loss=2.3924e+00 ppl=10.94                                                
Validation - loss=2.3093e+00 ppl=10.07 best_loss=2.3103e+00 best_ppl=10.08                                              
Epoch 96 - |param|=3.10e+02 |g_param|=2.51e+05 loss=2.2997e+00 ppl=9.97                                                 
Validation - loss=2.3082e+00 ppl=10.06 best_loss=2.3093e+00 best_ppl=10.07                                              
Epoch 97 - |param|=3.10e+02 |g_param|=2.25e+05 loss=2.3312e+00 ppl=10.29                                                
Validation - loss=2.3015e+00 ppl=9.99 best_loss=2.3082e+00 best_ppl=10.06                                               
Epoch 98 - |param|=3.11e+02 |g_param|=2.29e+05 loss=2.3349e+00 ppl=10.33                                                
Validation - loss=2.2925e+00 ppl=9.90 best_loss=2.3015e+00 best_ppl=9.99                                                
Epoch 99 - |param|=3.11e+02 |g_param|=2.64e+05 loss=2.3040e+00 ppl=10.01                                                
Validation - loss=2.2964e+00 ppl=9.94 best_loss=2.2925e+00 best_ppl=9.90                                                
Epoch 100 - |param|=3.11e+02 |g_param|=2.40e+05 loss=2.2385e+00 ppl=9.38                                                
Validation - loss=2.2855e+00 ppl=9.83 best_loss=2.2925e+00 best_ppl=9.90                                                

real	31m59.493s
user	31m54.730s
sys	0m4.627s
(simple-nmt) ye@:~/exp/simple-nmt$
```

updating testing/evaluation bash shell script ...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, Thailand
# Last updated: 27 Mar 2022
# find all models and parse to translate.py for testing and multi-bleu.perl for evaluation with BLEU score
# updated for Transformer baseline my-bk

cd ./model/transformer/baseline/bkmy-100epoch;

for i in *.pth; do
   MODEL=$i;

   # Testing
   python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 1 --lang bkmy < /home/ye/exp/simple-nmt/data/my-bk/syl/test.bk > $MODEL.hyp

   # Evaluation with BLEU Score
   echo "Evaluation result for the model: $MODEL" | tee -a eval-results-bkmy-transformer-baseline-100epoch.txt;
   cat $MODEL.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/my-bk/syl/test.my | tee  -a eval-results-bkmy-transformer-baseline-100epoch.txt;

done

cd -;

```

Testing/Evaluation ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-loop-transformer-bkmy.sh 
Evaluation result for the model: bkmy-transformer-model.01.5.93-375.10.5.79-325.39.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 46.7/1.7/0.0/0.0 (BP=0.143, ratio=0.339, hyp_len=4149, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.02.5.29-198.59.5.22-184.48.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 46.3/1.7/0.0/0.0 (BP=0.142, ratio=0.339, hyp_len=4148, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.03.4.86-129.60.4.77-118.02.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 44.1/2.7/0.0/0.0 (BP=0.142, ratio=0.339, hyp_len=4148, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.04.4.54-93.72.4.48-88.59.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 33.2/2.9/0.1/0.0 (BP=0.329, ratio=0.474, hyp_len=5796, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.05.4.33-75.78.4.28-72.35.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 29.9/3.2/0.1/0.0 (BP=0.535, ratio=0.615, hyp_len=7523, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.06.4.13-61.99.4.12-61.77.pth
BLEU = 0.68, 27.8/4.2/0.4/0.0 (BP=0.770, ratio=0.793, hyp_len=9698, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.07.4.03-56.22.3.98-53.65.pth
BLEU = 1.93, 29.7/7.3/1.7/0.1 (BP=0.819, ratio=0.834, hyp_len=10198, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.08.3.83-46.27.3.85-46.90.pth
BLEU = 2.83, 29.5/7.7/2.0/0.2 (BP=0.907, ratio=0.911, hyp_len=11147, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.09.3.76-43.08.3.74-42.24.pth
BLEU = 4.18, 28.9/8.6/2.7/0.6 (BP=0.923, ratio=0.926, hyp_len=11328, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.100.2.24-9.38.2.29-9.83.pth
BLEU = 16.94, 45.8/23.4/12.1/6.4 (BP=1.000, ratio=1.057, hyp_len=12933, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.10.3.66-38.68.3.65-38.55.pth
BLEU = 4.63, 28.8/8.7/2.9/0.8 (BP=0.940, ratio=0.941, hyp_len=11514, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.11.3.56-35.16.3.57-35.37.pth
BLEU = 4.86, 28.5/8.6/2.9/0.9 (BP=0.978, ratio=0.978, hyp_len=11959, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.12.3.52-33.72.3.50-32.98.pth
BLEU = 4.34, 26.3/7.9/2.6/0.7 (BP=1.000, ratio=1.080, hyp_len=13215, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.13.3.42-30.65.3.44-31.07.pth
BLEU = 4.19, 24.5/7.6/2.5/0.7 (BP=1.000, ratio=1.179, hyp_len=14417, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.14.3.37-29.21.3.37-29.19.pth
BLEU = 3.95, 22.5/7.1/2.4/0.6 (BP=1.000, ratio=1.329, hyp_len=16259, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.15.3.30-27.13.3.32-27.78.pth
BLEU = 5.03, 27.2/8.8/3.1/0.9 (BP=1.000, ratio=1.083, hyp_len=13241, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.16.3.24-25.59.3.28-26.47.pth
BLEU = 4.98, 27.6/8.8/3.0/0.8 (BP=1.000, ratio=1.095, hyp_len=13399, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.17.3.27-26.40.3.23-25.34.pth
BLEU = 4.24, 23.2/7.6/2.5/0.7 (BP=1.000, ratio=1.337, hyp_len=16353, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.18.3.22-25.12.3.19-24.35.pth
BLEU = 5.75, 30.2/10.3/3.5/1.0 (BP=1.000, ratio=1.045, hyp_len=12787, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.19.3.20-24.49.3.16-23.47.pth
BLEU = 5.78, 28.2/10.2/3.5/1.1 (BP=1.000, ratio=1.175, hyp_len=14372, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.20.3.14-23.17.3.12-22.75.pth
BLEU = 6.24, 30.6/11.2/3.8/1.2 (BP=1.000, ratio=1.055, hyp_len=12901, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.21.3.12-22.73.3.10-22.11.pth
BLEU = 6.07, 28.8/10.4/3.7/1.2 (BP=1.000, ratio=1.150, hyp_len=14069, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.22.3.11-22.35.3.06-21.35.pth
BLEU = 6.78, 30.8/11.2/4.1/1.5 (BP=1.000, ratio=1.068, hyp_len=13066, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.23.3.06-21.23.3.03-20.68.pth
BLEU = 7.23, 32.3/12.0/4.3/1.6 (BP=1.000, ratio=1.016, hyp_len=12425, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.24.3.03-20.80.3.00-20.07.pth
BLEU = 7.02, 32.1/11.7/4.3/1.5 (BP=1.000, ratio=1.032, hyp_len=12622, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.25.2.96-19.34.2.99-19.79.pth
BLEU = 7.20, 31.5/11.8/4.5/1.6 (BP=1.000, ratio=1.067, hyp_len=13051, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.26.2.93-18.75.2.96-19.21.pth
BLEU = 7.70, 33.2/12.4/4.7/1.8 (BP=1.000, ratio=1.000, hyp_len=12229, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.27.2.92-18.54.2.93-18.82.pth
BLEU = 7.15, 32.4/11.9/4.4/1.6 (BP=1.000, ratio=1.029, hyp_len=12591, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.28.2.94-18.86.2.92-18.51.pth
BLEU = 7.65, 34.4/12.8/4.8/1.8 (BP=0.967, ratio=0.967, hyp_len=11833, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.29.2.90-18.15.2.88-17.81.pth
BLEU = 7.78, 33.5/12.7/4.9/1.8 (BP=1.000, ratio=1.024, hyp_len=12519, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.30.2.90-18.16.2.87-17.60.pth
BLEU = 8.04, 33.9/13.0/5.1/1.9 (BP=1.000, ratio=1.023, hyp_len=12515, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.31.2.85-17.29.2.83-17.01.pth
BLEU = 7.42, 32.6/12.5/4.7/1.6 (BP=1.000, ratio=1.078, hyp_len=13179, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.32.2.85-17.32.2.82-16.81.pth
BLEU = 7.66, 33.0/12.8/4.8/1.7 (BP=1.000, ratio=1.072, hyp_len=13109, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.33.2.77-15.90.2.81-16.54.pth
BLEU = 8.32, 34.4/13.6/5.2/2.0 (BP=1.000, ratio=1.049, hyp_len=12825, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.34.2.77-15.93.2.79-16.34.pth
BLEU = 9.10, 36.6/14.5/5.8/2.3 (BP=0.994, ratio=0.994, hyp_len=12152, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.35.2.75-15.69.2.77-15.92.pth
BLEU = 8.93, 35.4/14.2/5.7/2.2 (BP=1.000, ratio=1.043, hyp_len=12758, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.36.2.81-16.64.2.74-15.50.pth
BLEU = 9.48, 37.6/15.4/6.2/2.3 (BP=0.993, ratio=0.993, hyp_len=12143, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.37.2.78-16.17.2.73-15.26.pth
BLEU = 9.27, 36.8/15.1/6.0/2.2 (BP=1.000, ratio=1.005, hyp_len=12287, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.38.2.73-15.34.2.72-15.14.pth
BLEU = 9.02, 36.3/14.5/5.8/2.2 (BP=1.000, ratio=1.035, hyp_len=12657, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.39.2.75-15.71.2.70-14.85.pth
BLEU = 9.20, 35.9/14.6/5.9/2.3 (BP=1.000, ratio=1.034, hyp_len=12644, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.40.2.74-15.53.2.69-14.79.pth
BLEU = 9.41, 36.8/14.9/6.0/2.4 (BP=1.000, ratio=1.019, hyp_len=12469, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.41.2.69-14.69.2.68-14.57.pth
BLEU = 10.20, 39.0/16.3/6.8/2.8 (BP=0.972, ratio=0.972, hyp_len=11893, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.42.2.74-15.51.2.66-14.29.pth
BLEU = 9.94, 38.6/15.7/6.4/2.6 (BP=0.993, ratio=0.993, hyp_len=12149, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.43.2.65-14.14.2.65-14.09.pth
BLEU = 9.92, 37.0/15.5/6.4/2.6 (BP=1.000, ratio=1.047, hyp_len=12811, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.44.2.65-14.13.2.64-14.07.pth
BLEU = 10.44, 38.8/16.3/6.9/3.0 (BP=0.981, ratio=0.981, hyp_len=12000, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.45.2.64-14.06.2.63-13.83.pth
BLEU = 10.02, 37.4/15.6/6.5/2.7 (BP=1.000, ratio=1.030, hyp_len=12597, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.46.2.67-14.38.2.62-13.78.pth
BLEU = 10.32, 37.5/15.7/6.7/2.9 (BP=1.000, ratio=1.026, hyp_len=12545, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.47.2.71-15.03.2.60-13.52.pth
BLEU = 10.49, 38.7/16.3/6.8/2.8 (BP=1.000, ratio=1.013, hyp_len=12388, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.48.2.57-13.01.2.59-13.27.pth
BLEU = 10.98, 39.4/16.9/7.2/3.0 (BP=1.000, ratio=1.013, hyp_len=12385, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.49.2.63-13.88.2.58-13.16.pth
BLEU = 10.51, 38.4/16.3/6.8/2.9 (BP=1.000, ratio=1.051, hyp_len=12851, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.50.2.57-13.11.2.57-13.01.pth
BLEU = 11.50, 39.9/17.4/7.5/3.3 (BP=1.000, ratio=1.003, hyp_len=12269, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.51.2.60-13.41.2.57-13.11.pth
BLEU = 11.57, 40.6/17.7/7.7/3.4 (BP=0.990, ratio=0.990, hyp_len=12105, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.52.2.59-13.35.2.57-13.06.pth
BLEU = 11.44, 40.9/17.8/7.9/3.6 (BP=0.956, ratio=0.957, hyp_len=11700, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.53.2.60-13.44.2.55-12.80.pth
BLEU = 11.01, 38.9/16.9/7.2/3.1 (BP=1.000, ratio=1.027, hyp_len=12556, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.54.2.55-12.78.2.54-12.72.pth
BLEU = 11.07, 38.4/16.8/7.3/3.2 (BP=1.000, ratio=1.077, hyp_len=13177, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.55.2.60-13.44.2.53-12.60.pth
BLEU = 11.14, 39.6/17.0/7.4/3.1 (BP=1.000, ratio=1.015, hyp_len=12418, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.56.2.57-13.11.2.52-12.44.pth
BLEU = 11.19, 39.1/16.9/7.4/3.2 (BP=1.000, ratio=1.037, hyp_len=12679, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.57.2.54-12.63.2.51-12.34.pth
BLEU = 12.05, 40.9/18.0/7.9/3.6 (BP=1.000, ratio=1.008, hyp_len=12330, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.58.2.52-12.38.2.51-12.33.pth
BLEU = 11.40, 39.4/17.3/7.5/3.3 (BP=1.000, ratio=1.055, hyp_len=12902, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.59.2.52-12.48.2.50-12.21.pth
BLEU = 11.96, 39.2/17.6/7.9/3.7 (BP=1.000, ratio=1.066, hyp_len=13039, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.60.2.51-12.32.2.50-12.20.pth
BLEU = 11.84, 40.2/17.7/7.8/3.5 (BP=1.000, ratio=1.015, hyp_len=12410, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.61.2.48-11.89.2.49-12.10.pth
BLEU = 12.21, 40.0/17.8/8.1/3.9 (BP=1.000, ratio=1.026, hyp_len=12547, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.62.2.49-12.04.2.48-11.95.pth
BLEU = 12.27, 40.9/18.1/8.1/3.8 (BP=1.000, ratio=1.004, hyp_len=12282, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.63.2.48-11.91.2.47-11.86.pth
BLEU = 12.66, 40.5/18.6/8.6/4.0 (BP=1.000, ratio=1.055, hyp_len=12908, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.64.2.50-12.24.2.46-11.76.pth
BLEU = 12.77, 41.0/18.8/8.5/4.1 (BP=1.000, ratio=1.023, hyp_len=12510, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.65.2.52-12.49.2.46-11.66.pth
BLEU = 13.52, 42.7/19.7/9.3/4.4 (BP=0.994, ratio=0.994, hyp_len=12152, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.66.2.53-12.59.2.45-11.60.pth
BLEU = 12.16, 39.9/18.1/8.2/3.7 (BP=1.000, ratio=1.077, hyp_len=13178, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.67.2.48-11.93.2.44-11.48.pth
BLEU = 13.78, 42.8/20.1/9.4/4.5 (BP=1.000, ratio=1.013, hyp_len=12385, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.68.2.43-11.38.2.44-11.46.pth
BLEU = 13.18, 41.5/19.1/8.9/4.3 (BP=1.000, ratio=1.050, hyp_len=12845, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.69.2.42-11.26.2.44-11.52.pth
BLEU = 13.77, 42.7/19.8/9.4/4.5 (BP=1.000, ratio=1.005, hyp_len=12292, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.70.2.38-10.79.2.45-11.54.pth
BLEU = 13.38, 41.5/19.2/9.0/4.5 (BP=1.000, ratio=1.025, hyp_len=12536, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.71.2.43-11.39.2.42-11.26.pth
BLEU = 13.92, 42.5/19.9/9.5/4.7 (BP=1.000, ratio=1.045, hyp_len=12786, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.72.2.41-11.15.2.41-11.17.pth
BLEU = 13.23, 41.5/19.2/9.0/4.3 (BP=1.000, ratio=1.053, hyp_len=12880, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.73.2.41-11.08.2.41-11.14.pth
BLEU = 14.17, 43.5/20.6/9.6/4.7 (BP=1.000, ratio=1.002, hyp_len=12257, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.74.2.44-11.49.2.41-11.17.pth
BLEU = 14.30, 43.2/20.5/9.8/4.8 (BP=1.000, ratio=1.005, hyp_len=12298, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.75.2.42-11.26.2.41-11.09.pth
BLEU = 13.69, 42.3/19.8/9.3/4.5 (BP=1.000, ratio=1.047, hyp_len=12807, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.76.2.41-11.18.2.39-10.92.pth
BLEU = 13.73, 41.7/19.9/9.4/4.5 (BP=1.000, ratio=1.069, hyp_len=13075, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.77.2.37-10.65.2.39-10.94.pth
BLEU = 14.65, 43.3/20.9/10.1/5.0 (BP=1.000, ratio=1.035, hyp_len=12663, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.78.2.45-11.63.2.39-10.88.pth
BLEU = 14.44, 42.2/20.3/10.0/5.1 (BP=1.000, ratio=1.049, hyp_len=12831, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.79.2.38-10.84.2.38-10.83.pth
BLEU = 15.42, 44.3/21.5/10.6/5.6 (BP=1.000, ratio=1.010, hyp_len=12356, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.80.2.33-10.26.2.38-10.83.pth
BLEU = 14.66, 42.9/20.7/10.1/5.1 (BP=1.000, ratio=1.036, hyp_len=12677, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.81.2.34-10.35.2.37-10.71.pth
BLEU = 14.87, 43.5/21.0/10.3/5.2 (BP=1.000, ratio=1.042, hyp_len=12741, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.82.2.34-10.43.2.37-10.67.pth
BLEU = 14.91, 43.6/21.1/10.3/5.2 (BP=1.000, ratio=1.035, hyp_len=12656, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.83.2.39-10.88.2.36-10.59.pth
BLEU = 14.83, 43.9/21.3/10.3/5.0 (BP=1.000, ratio=1.060, hyp_len=12968, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.84.2.34-10.43.2.35-10.50.pth
BLEU = 15.72, 45.2/22.3/10.9/5.6 (BP=1.000, ratio=1.015, hyp_len=12416, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.85.2.38-10.85.2.35-10.47.pth
BLEU = 15.73, 44.5/21.9/11.0/5.7 (BP=1.000, ratio=1.039, hyp_len=12711, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.86.2.34-10.36.2.34-10.38.pth
BLEU = 15.37, 44.0/21.5/10.7/5.5 (BP=1.000, ratio=1.057, hyp_len=12934, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.87.2.37-10.70.2.34-10.35.pth
BLEU = 16.59, 46.1/22.8/11.6/6.2 (BP=0.998, ratio=0.998, hyp_len=12207, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.88.2.32-10.22.2.33-10.32.pth
BLEU = 16.23, 45.2/22.3/11.4/6.0 (BP=1.000, ratio=1.025, hyp_len=12541, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.89.2.29-9.84.2.34-10.41.pth
BLEU = 16.33, 45.3/22.5/11.5/6.1 (BP=1.000, ratio=1.012, hyp_len=12382, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.90.2.28-9.78.2.34-10.34.pth
BLEU = 16.26, 45.3/22.6/11.4/6.0 (BP=1.000, ratio=1.027, hyp_len=12559, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.91.2.33-10.25.2.33-10.30.pth
BLEU = 15.24, 43.4/21.4/10.7/5.4 (BP=1.000, ratio=1.058, hyp_len=12944, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.92.2.35-10.45.2.32-10.16.pth
BLEU = 17.55, 47.7/24.3/12.6/6.7 (BP=0.989, ratio=0.989, hyp_len=12099, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.93.2.33-10.30.2.31-10.09.pth
BLEU = 17.12, 47.3/23.8/12.1/6.3 (BP=0.999, ratio=0.999, hyp_len=12221, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.94.2.30-9.98.2.31-10.08.pth
BLEU = 17.10, 46.3/23.3/12.0/6.6 (BP=1.000, ratio=1.018, hyp_len=12448, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.95.2.39-10.94.2.31-10.07.pth
BLEU = 16.73, 45.2/23.0/11.8/6.4 (BP=1.000, ratio=1.044, hyp_len=12768, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.96.2.30-9.97.2.31-10.06.pth
BLEU = 16.31, 44.6/22.3/11.6/6.1 (BP=1.000, ratio=1.056, hyp_len=12916, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.97.2.33-10.29.2.30-9.99.pth
BLEU = 16.98, 46.1/23.3/12.0/6.5 (BP=1.000, ratio=1.033, hyp_len=12633, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.98.2.33-10.33.2.29-9.90.pth
BLEU = 17.31, 46.3/23.7/12.3/6.6 (BP=1.000, ratio=1.025, hyp_len=12538, ref_len=12231)
Evaluation result for the model: bkmy-transformer-model.99.2.30-10.01.2.30-9.94.pth
BLEU = 17.58, 47.2/24.0/12.5/6.8 (BP=1.000, ratio=1.010, hyp_len=12358, ref_len=12231)
/home/ye/exp/simple-nmt

real	35m31.133s
user	31m41.657s
sys	2m32.909s
```

epoch 100 မှာ အကောင်းဆုံး မော်ဒယ်က 99 epoch model ဖြစ်ပြီးတော့ Best BLEU score (baseline) က 17.58 ဖြစ်တယ်။  
