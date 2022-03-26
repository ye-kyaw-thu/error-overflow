# Dual Supervised Learning (DSL) for Myanmar-Beik Language Pair

## Preparation for Myanmar-Beik

ထုံးစံအတိုင်းပါပဲ ဘယ်ဒေတာကို သုံးမယ်ဆိုတာ... ဒေတာပမာဏကို ကြည့်တာ... data cleaning, syllable breaking စတာတွေကို လုပ်ခဲ့တယ်။  


### Data Statistics

ဘိတ်ဘာသာ အတွက်...  

```
(simple-nmt) ye@:~/exp/simple-nmt/data/my-bk/syl$ wc *.bk
   1390   15399  141958 dev.bk
   1037   11432  106079 test.bk
   7871   87090  808557 train.bk
  10298  113921 1056594 total
```

မြန်မာဘာသာအတွက်...  

```
(simple-nmt) ye@:~/exp/simple-nmt/data/my-bk/syl$ wc *.my
   1390   16712  153744 dev.my
   1037   12231  113030 test.my
   7871   93911  869163 train.my
  10298  122854 1135937 total
(simple-nmt) ye@:~/exp/simple-nmt/data/my-bk/syl$
```

## LM Building

```
   time python lm_train.py --train /home/ye/exp/simple-nmt/data/my-bk/syl/train --valid /home/ye/exp/simple-nmt/data/my-bk/syl/dev --lang mybk \
   --gpu_id 0 --batch_size 64 --n_epochs 200 --max_length 100 --dropout .2 \
   --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
   --model_fn ./model/lm/mybk/lm-200epoch-mybk.pth | tee ./model/lm/my/mybk/lm-200epoch-training-my.log
```

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python lm_train.py --train /home/ye/exp/simple-nmt/data/my-bk/syl/train --valid /home/ye/exp/simple-nmt/data/my-bk/syl/dev --lang mybk \
>    --gpu_id 0 --batch_size 64 --n_epochs 200 --max_length 100 --dropout .2 \
>    --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
>    --model_fn ./model/lm/mybk/lm-200epoch-mybk.pth | tee ./model/lm/my/mybk/lm-200epoch-training-my.log
tee: ./model/lm/my/mybk/lm-200epoch-training-my.log: No such file or directory
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 0,
    'hidden_size': 128,
    'lang': 'mybk',
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/lm/mybk/lm-200epoch-mybk.pth',
    'n_epochs': 200,
    'n_layers': 4,
    'off_autocast': False,
    'train': '/home/ye/exp/simple-nmt/data/my-bk/syl/train',
    'valid': '/home/ye/exp/simple-nmt/data/my-bk/syl/dev',
    'verbose': 2,
    'word_vec_size': 128}
[LanguageModel(
  (emb): Embedding(1470, 128, padding_idx=1)
  (rnn): LSTM(128, 128, num_layers=4, batch_first=True, dropout=0.2)
  (out): Linear(in_features=128, out_features=1470, bias=True)
  (log_softmax): LogSoftmax(dim=-1)
), LanguageModel(
  (emb): Embedding(1315, 128, padding_idx=1)
  (rnn): LSTM(128, 128, num_layers=4, batch_first=True, dropout=0.2)
  (out): Linear(in_features=128, out_features=1315, bias=True)
  (log_softmax): LogSoftmax(dim=-1)
)]
Epoch 1 - |param|=4.34e+02 |g_param|=3.74e+05 loss=4.8761e+00 ppl=131.12                                                
Validation - loss=4.2695e+00 ppl=71.48 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=4.35e+02 |g_param|=3.67e+05 loss=4.4999e+00 ppl=90.01                                                 
Validation - loss=4.1191e+00 ppl=61.50 best_loss=4.2695e+00 best_ppl=71.48                                              
Epoch 3 - |param|=4.35e+02 |g_param|=2.07e+05 loss=4.4106e+00 ppl=82.32                                                 
Validation - loss=4.3262e+00 ppl=75.65 best_loss=4.1191e+00 best_ppl=61.50                                              
Epoch 4 - |param|=4.35e+02 |g_param|=1.81e+05 loss=4.4566e+00 ppl=86.19                                                 
Validation - loss=4.1519e+00 ppl=63.55 best_loss=4.1191e+00 best_ppl=61.50                                              
Epoch 5 - |param|=4.35e+02 |g_param|=1.02e+05 loss=4.4312e+00 ppl=84.04                                                 
Validation - loss=4.4210e+00 ppl=83.18 best_loss=4.1191e+00 best_ppl=61.50                                              
Epoch 6 - |param|=4.36e+02 |g_param|=7.46e+04 loss=4.4159e+00 ppl=82.76                                                 
Validation - loss=4.3075e+00 ppl=74.25 best_loss=4.1191e+00 best_ppl=61.50                                              
Epoch 7 - |param|=4.36e+02 |g_param|=6.68e+04 loss=4.2656e+00 ppl=71.21                                                 
Validation - loss=3.9986e+00 ppl=54.52 best_loss=4.1191e+00 best_ppl=61.50                                              
Epoch 8 - |param|=4.37e+02 |g_param|=5.53e+04 loss=4.1404e+00 ppl=62.83                                                 
Validation - loss=3.9156e+00 ppl=50.18 best_loss=3.9986e+00 best_ppl=54.52                                              
Epoch 9 - |param|=4.37e+02 |g_param|=5.31e+04 loss=4.0522e+00 ppl=57.52                                                 
Validation - loss=3.6819e+00 ppl=39.72 best_loss=3.9156e+00 best_ppl=50.18                                              
Epoch 10 - |param|=4.38e+02 |g_param|=4.16e+04 loss=3.8716e+00 ppl=48.02                                                
Validation - loss=3.6198e+00 ppl=37.33 best_loss=3.6819e+00 best_ppl=39.72                                              
Epoch 11 - |param|=4.39e+02 |g_param|=3.98e+04 loss=3.8101e+00 ppl=45.15                                                
Validation - loss=3.5561e+00 ppl=35.03 best_loss=3.6198e+00 best_ppl=37.33                                              
Epoch 12 - |param|=4.40e+02 |g_param|=3.78e+04 loss=3.7350e+00 ppl=41.89                                                
Validation - loss=3.5058e+00 ppl=33.31 best_loss=3.5561e+00 best_ppl=35.03                                              
Epoch 13 - |param|=4.41e+02 |g_param|=4.09e+04 loss=3.7603e+00 ppl=42.96                                                
Validation - loss=3.4506e+00 ppl=31.52 best_loss=3.5058e+00 best_ppl=33.31                                              
Epoch 14 - |param|=4.41e+02 |g_param|=3.71e+04 loss=3.6858e+00 ppl=39.88                                                
Validation - loss=3.4344e+00 ppl=31.01 best_loss=3.4506e+00 best_ppl=31.52                                              
Epoch 15 - |param|=4.42e+02 |g_param|=3.61e+04 loss=3.5273e+00 ppl=34.03                                                
Validation - loss=3.4197e+00 ppl=30.56 best_loss=3.4344e+00 best_ppl=31.01                                              
Epoch 16 - |param|=4.43e+02 |g_param|=3.63e+04 loss=3.5111e+00 ppl=33.48                                                
Validation - loss=3.3857e+00 ppl=29.54 best_loss=3.4197e+00 best_ppl=30.56                                              
Epoch 17 - |param|=4.43e+02 |g_param|=3.72e+04 loss=3.5076e+00 ppl=33.37                                                
Validation - loss=3.3793e+00 ppl=29.35 best_loss=3.3857e+00 best_ppl=29.54                                              
Epoch 18 - |param|=4.44e+02 |g_param|=3.93e+04 loss=3.5476e+00 ppl=34.73                                                
Validation - loss=3.3564e+00 ppl=28.68 best_loss=3.3793e+00 best_ppl=29.35                                              
Epoch 19 - |param|=4.45e+02 |g_param|=3.74e+04 loss=3.4711e+00 ppl=32.17                                                
Validation - loss=3.3247e+00 ppl=27.79 best_loss=3.3564e+00 best_ppl=28.68                                              
Epoch 20 - |param|=4.45e+02 |g_param|=3.73e+04 loss=3.3933e+00 ppl=29.77                                                
Validation - loss=3.3266e+00 ppl=27.84 best_loss=3.3247e+00 best_ppl=27.79                                              
Epoch 21 - |param|=4.46e+02 |g_param|=5.56e+04 loss=3.3729e+00 ppl=29.16                                                
Validation - loss=3.3267e+00 ppl=27.85 best_loss=3.3247e+00 best_ppl=27.79                                              
Epoch 22 - |param|=4.47e+02 |g_param|=7.92e+04 loss=3.3522e+00 ppl=28.56                                                
Validation - loss=3.3269e+00 ppl=27.85 best_loss=3.3247e+00 best_ppl=27.79                                              
Epoch 23 - |param|=4.47e+02 |g_param|=7.90e+04 loss=3.2943e+00 ppl=26.96                                                
Validation - loss=3.3040e+00 ppl=27.22 best_loss=3.3247e+00 best_ppl=27.79                                              
Epoch 24 - |param|=4.48e+02 |g_param|=8.03e+04 loss=3.3273e+00 ppl=27.86                                                
Validation - loss=3.3156e+00 ppl=27.54 best_loss=3.3040e+00 best_ppl=27.22                                              
Epoch 25 - |param|=4.49e+02 |g_param|=7.90e+04 loss=3.2648e+00 ppl=26.18                                                
Validation - loss=3.2702e+00 ppl=26.32 best_loss=3.3040e+00 best_ppl=27.22                                              
Epoch 26 - |param|=4.49e+02 |g_param|=8.05e+04 loss=3.2353e+00 ppl=25.41                                                
Validation - loss=3.2792e+00 ppl=26.55 best_loss=3.2702e+00 best_ppl=26.32                                              
Epoch 27 - |param|=4.50e+02 |g_param|=8.57e+04 loss=3.3016e+00 ppl=27.16                                                
Validation - loss=3.2689e+00 ppl=26.28 best_loss=3.2702e+00 best_ppl=26.32                                              
Epoch 28 - |param|=4.51e+02 |g_param|=8.22e+04 loss=3.1642e+00 ppl=23.67                                                
Validation - loss=3.2657e+00 ppl=26.20 best_loss=3.2689e+00 best_ppl=26.28                                              
Epoch 29 - |param|=4.51e+02 |g_param|=8.28e+04 loss=3.1699e+00 ppl=23.80                                                
Validation - loss=3.2476e+00 ppl=25.73 best_loss=3.2657e+00 best_ppl=26.20                                              
Epoch 30 - |param|=4.52e+02 |g_param|=8.26e+04 loss=3.1186e+00 ppl=22.61                                                
Validation - loss=3.2441e+00 ppl=25.64 best_loss=3.2476e+00 best_ppl=25.73                                              
Epoch 31 - |param|=4.53e+02 |g_param|=8.43e+04 loss=3.1245e+00 ppl=22.75                                                
Validation - loss=3.2361e+00 ppl=25.43 best_loss=3.2441e+00 best_ppl=25.64                                              
Epoch 32 - |param|=4.54e+02 |g_param|=8.82e+04 loss=3.1388e+00 ppl=23.08                                                
Validation - loss=3.2450e+00 ppl=25.66 best_loss=3.2361e+00 best_ppl=25.43                                              
Epoch 33 - |param|=4.54e+02 |g_param|=8.98e+04 loss=3.1256e+00 ppl=22.77                                                
Validation - loss=3.2216e+00 ppl=25.07 best_loss=3.2361e+00 best_ppl=25.43                                              
Epoch 34 - |param|=4.55e+02 |g_param|=8.61e+04 loss=3.0317e+00 ppl=20.73                                                
Validation - loss=3.2288e+00 ppl=25.25 best_loss=3.2216e+00 best_ppl=25.07                                              
Epoch 35 - |param|=4.56e+02 |g_param|=8.72e+04 loss=3.0039e+00 ppl=20.16                                                
Validation - loss=3.1953e+00 ppl=24.42 best_loss=3.2216e+00 best_ppl=25.07                                              
Epoch 36 - |param|=4.57e+02 |g_param|=9.01e+04 loss=3.0100e+00 ppl=20.29                                                
Validation - loss=3.1985e+00 ppl=24.50 best_loss=3.1953e+00 best_ppl=24.42                                              
Epoch 37 - |param|=4.57e+02 |g_param|=9.29e+04 loss=2.9646e+00 ppl=19.39                                                
Validation - loss=3.1953e+00 ppl=24.42 best_loss=3.1953e+00 best_ppl=24.42                                              
Epoch 38 - |param|=4.58e+02 |g_param|=1.79e+05 loss=2.9368e+00 ppl=18.86                                                
Validation - loss=3.1999e+00 ppl=24.53 best_loss=3.1953e+00 best_ppl=24.42                                              
Epoch 39 - |param|=4.59e+02 |g_param|=1.84e+05 loss=2.9478e+00 ppl=19.06                                                
Validation - loss=3.1888e+00 ppl=24.26 best_loss=3.1953e+00 best_ppl=24.42                                              
Epoch 40 - |param|=4.60e+02 |g_param|=1.89e+05 loss=2.9458e+00 ppl=19.03                                                
Validation - loss=3.1897e+00 ppl=24.28 best_loss=3.1888e+00 best_ppl=24.26                                              
Epoch 41 - |param|=4.60e+02 |g_param|=1.93e+05 loss=2.9254e+00 ppl=18.64                                                
Validation - loss=3.1849e+00 ppl=24.16 best_loss=3.1888e+00 best_ppl=24.26                                              
Epoch 42 - |param|=4.61e+02 |g_param|=1.93e+05 loss=2.8537e+00 ppl=17.35                                                
Validation - loss=3.2003e+00 ppl=24.54 best_loss=3.1849e+00 best_ppl=24.16                                              
Epoch 43 - |param|=4.62e+02 |g_param|=1.98e+05 loss=2.9052e+00 ppl=18.27                                                
Validation - loss=3.1757e+00 ppl=23.94 best_loss=3.1849e+00 best_ppl=24.16                                              
Epoch 44 - |param|=4.63e+02 |g_param|=2.00e+05 loss=2.8948e+00 ppl=18.08                                                
Validation - loss=3.1878e+00 ppl=24.24 best_loss=3.1757e+00 best_ppl=23.94                                              
Epoch 45 - |param|=4.63e+02 |g_param|=2.13e+05 loss=2.9032e+00 ppl=18.23                                                
Validation - loss=3.1837e+00 ppl=24.14 best_loss=3.1757e+00 best_ppl=23.94                                              
Epoch 46 - |param|=4.64e+02 |g_param|=1.95e+05 loss=2.7963e+00 ppl=16.38                                                
Validation - loss=3.2023e+00 ppl=24.59 best_loss=3.1757e+00 best_ppl=23.94                                              
Epoch 47 - |param|=4.65e+02 |g_param|=1.94e+05 loss=2.7927e+00 ppl=16.32                                                
Validation - loss=3.1661e+00 ppl=23.71 best_loss=3.1757e+00 best_ppl=23.94                                              
Epoch 48 - |param|=4.66e+02 |g_param|=1.97e+05 loss=2.7804e+00 ppl=16.13                                                
Validation - loss=3.1916e+00 ppl=24.33 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 49 - |param|=4.67e+02 |g_param|=1.93e+05 loss=2.7567e+00 ppl=15.75                                                
Validation - loss=3.1772e+00 ppl=23.98 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 50 - |param|=4.67e+02 |g_param|=2.06e+05 loss=2.7557e+00 ppl=15.73                                                
Validation - loss=3.1818e+00 ppl=24.09 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 51 - |param|=4.68e+02 |g_param|=2.03e+05 loss=2.7451e+00 ppl=15.57                                                
Validation - loss=3.1869e+00 ppl=24.21 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 52 - |param|=4.69e+02 |g_param|=1.99e+05 loss=2.7004e+00 ppl=14.89                                                
Validation - loss=3.1722e+00 ppl=23.86 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 53 - |param|=4.70e+02 |g_param|=2.06e+05 loss=2.6805e+00 ppl=14.59                                                
Validation - loss=3.1856e+00 ppl=24.18 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 54 - |param|=4.71e+02 |g_param|=3.91e+05 loss=2.6821e+00 ppl=14.62                                                
Validation - loss=3.1831e+00 ppl=24.12 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 55 - |param|=4.72e+02 |g_param|=4.17e+05 loss=2.6751e+00 ppl=14.51                                                
Validation - loss=3.1911e+00 ppl=24.32 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 56 - |param|=4.72e+02 |g_param|=4.24e+05 loss=2.6560e+00 ppl=14.24                                                
Validation - loss=3.1899e+00 ppl=24.29 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 57 - |param|=4.73e+02 |g_param|=4.37e+05 loss=2.7041e+00 ppl=14.94                                                
Validation - loss=3.1813e+00 ppl=24.08 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 58 - |param|=4.74e+02 |g_param|=4.28e+05 loss=2.6155e+00 ppl=13.67                                                
Validation - loss=3.2052e+00 ppl=24.66 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 59 - |param|=4.75e+02 |g_param|=4.20e+05 loss=2.6010e+00 ppl=13.48                                                
Validation - loss=3.1819e+00 ppl=24.09 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 60 - |param|=4.76e+02 |g_param|=4.29e+05 loss=2.5769e+00 ppl=13.16                                                
Validation - loss=3.1869e+00 ppl=24.21 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 61 - |param|=4.77e+02 |g_param|=4.30e+05 loss=2.6076e+00 ppl=13.57                                                
Validation - loss=3.1991e+00 ppl=24.51 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 62 - |param|=4.78e+02 |g_param|=4.39e+05 loss=2.5707e+00 ppl=13.07                                                
Validation - loss=3.1757e+00 ppl=23.94 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 63 - |param|=4.78e+02 |g_param|=4.44e+05 loss=2.5567e+00 ppl=12.89                                                
Validation - loss=3.1995e+00 ppl=24.52 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 64 - |param|=4.79e+02 |g_param|=4.55e+05 loss=2.5795e+00 ppl=13.19                                                
Validation - loss=3.2186e+00 ppl=24.99 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 65 - |param|=4.80e+02 |g_param|=4.40e+05 loss=2.5382e+00 ppl=12.66                                                
Validation - loss=3.2035e+00 ppl=24.62 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 66 - |param|=4.81e+02 |g_param|=4.59e+05 loss=2.5324e+00 ppl=12.58                                                
Validation - loss=3.2067e+00 ppl=24.70 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 67 - |param|=4.82e+02 |g_param|=4.43e+05 loss=2.4955e+00 ppl=12.13                                                
Validation - loss=3.2070e+00 ppl=24.70 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 68 - |param|=4.83e+02 |g_param|=4.56e+05 loss=2.4905e+00 ppl=12.07                                                
Validation - loss=3.2031e+00 ppl=24.61 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 69 - |param|=4.84e+02 |g_param|=4.49e+05 loss=2.4868e+00 ppl=12.02                                                
Validation - loss=3.1958e+00 ppl=24.43 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 70 - |param|=4.85e+02 |g_param|=7.86e+05 loss=2.4724e+00 ppl=11.85                                                
Validation - loss=3.2167e+00 ppl=24.94 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 71 - |param|=4.86e+02 |g_param|=6.17e+05 loss=2.4896e+00 ppl=12.06                                                
Validation - loss=3.2043e+00 ppl=24.64 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 72 - |param|=4.87e+02 |g_param|=5.17e+05 loss=2.5324e+00 ppl=12.58                                                
Validation - loss=3.1958e+00 ppl=24.43 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 73 - |param|=4.88e+02 |g_param|=4.73e+05 loss=2.4179e+00 ppl=11.22                                                
Validation - loss=3.2177e+00 ppl=24.97 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 74 - |param|=4.89e+02 |g_param|=4.83e+05 loss=2.4560e+00 ppl=11.66                                                
Validation - loss=3.2105e+00 ppl=24.79 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 75 - |param|=4.90e+02 |g_param|=4.78e+05 loss=2.4077e+00 ppl=11.11                                                
Validation - loss=3.2106e+00 ppl=24.79 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 76 - |param|=4.91e+02 |g_param|=4.78e+05 loss=2.3949e+00 ppl=10.97                                                
Validation - loss=3.2314e+00 ppl=25.32 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 77 - |param|=4.92e+02 |g_param|=4.81e+05 loss=2.4088e+00 ppl=11.12                                                
Validation - loss=3.2218e+00 ppl=25.07 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 78 - |param|=4.93e+02 |g_param|=4.63e+05 loss=2.3658e+00 ppl=10.65                                                
Validation - loss=3.2291e+00 ppl=25.26 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 79 - |param|=4.94e+02 |g_param|=4.96e+05 loss=2.3790e+00 ppl=10.79                                                
Validation - loss=3.2337e+00 ppl=25.37 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 80 - |param|=4.95e+02 |g_param|=4.88e+05 loss=2.3714e+00 ppl=10.71                                                
Validation - loss=3.2277e+00 ppl=25.22 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 81 - |param|=4.96e+02 |g_param|=4.89e+05 loss=2.3488e+00 ppl=10.47                                                
Validation - loss=3.2357e+00 ppl=25.42 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 82 - |param|=4.97e+02 |g_param|=5.05e+05 loss=2.3786e+00 ppl=10.79                                                
Validation - loss=3.2331e+00 ppl=25.36 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 83 - |param|=4.98e+02 |g_param|=4.87e+05 loss=2.3268e+00 ppl=10.24                                                
Validation - loss=3.2241e+00 ppl=25.13 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 84 - |param|=4.99e+02 |g_param|=5.18e+05 loss=2.3733e+00 ppl=10.73                                                
Validation - loss=3.2376e+00 ppl=25.47 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 85 - |param|=5.00e+02 |g_param|=5.01e+05 loss=2.3173e+00 ppl=10.15                                                
Validation - loss=3.2218e+00 ppl=25.07 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 86 - |param|=5.01e+02 |g_param|=5.17e+05 loss=2.3205e+00 ppl=10.18                                                
Validation - loss=3.2290e+00 ppl=25.25 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 87 - |param|=5.02e+02 |g_param|=6.20e+05 loss=2.3135e+00 ppl=10.11                                                
Validation - loss=3.2335e+00 ppl=25.37 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 88 - |param|=5.03e+02 |g_param|=7.44e+05 loss=2.3082e+00 ppl=10.06                                                
Validation - loss=3.2200e+00 ppl=25.03 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 89 - |param|=5.04e+02 |g_param|=5.01e+05 loss=2.2704e+00 ppl=9.68                                                 
Validation - loss=3.2344e+00 ppl=25.39 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 90 - |param|=5.05e+02 |g_param|=5.04e+05 loss=2.2728e+00 ppl=9.71                                                 
Validation - loss=3.2400e+00 ppl=25.53 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 91 - |param|=5.06e+02 |g_param|=5.10e+05 loss=2.2764e+00 ppl=9.74                                                 
Validation - loss=3.2283e+00 ppl=25.24 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 92 - |param|=5.07e+02 |g_param|=5.17e+05 loss=2.2626e+00 ppl=9.61                                                 
Validation - loss=3.2543e+00 ppl=25.90 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 93 - |param|=5.08e+02 |g_param|=5.21e+05 loss=2.2640e+00 ppl=9.62                                                 
Validation - loss=3.2590e+00 ppl=26.02 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 94 - |param|=5.09e+02 |g_param|=5.17e+05 loss=2.2369e+00 ppl=9.36                                                 
Validation - loss=3.2509e+00 ppl=25.81 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 95 - |param|=5.10e+02 |g_param|=5.23e+05 loss=2.2399e+00 ppl=9.39                                                 
Validation - loss=3.2477e+00 ppl=25.73 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 96 - |param|=5.11e+02 |g_param|=5.14e+05 loss=2.2006e+00 ppl=9.03                                                 
Validation - loss=3.2649e+00 ppl=26.18 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 97 - |param|=5.12e+02 |g_param|=5.17e+05 loss=2.2009e+00 ppl=9.03                                                 
Validation - loss=3.2562e+00 ppl=25.95 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 98 - |param|=5.14e+02 |g_param|=5.37e+05 loss=2.2178e+00 ppl=9.19                                                 
Validation - loss=3.2719e+00 ppl=26.36 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 99 - |param|=5.15e+02 |g_param|=5.37e+05 loss=2.2191e+00 ppl=9.20                                                 
Validation - loss=3.2562e+00 ppl=25.95 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 100 - |param|=5.16e+02 |g_param|=2.95e+05 loss=2.2204e+00 ppl=9.21                                                
Validation - loss=3.2656e+00 ppl=26.20 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 101 - |param|=5.17e+02 |g_param|=2.72e+05 loss=2.1955e+00 ppl=8.98                                                
Validation - loss=3.2885e+00 ppl=26.80 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 102 - |param|=5.18e+02 |g_param|=2.64e+05 loss=2.1600e+00 ppl=8.67                                                
Validation - loss=3.2535e+00 ppl=25.88 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 103 - |param|=5.19e+02 |g_param|=2.71e+05 loss=2.1687e+00 ppl=8.75                                                
Validation - loss=3.2702e+00 ppl=26.32 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 104 - |param|=5.20e+02 |g_param|=2.80e+05 loss=2.1954e+00 ppl=8.98                                                
Validation - loss=3.2679e+00 ppl=26.25 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 105 - |param|=5.21e+02 |g_param|=2.67e+05 loss=2.1471e+00 ppl=8.56                                                
Validation - loss=3.2889e+00 ppl=26.81 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 106 - |param|=5.22e+02 |g_param|=2.79e+05 loss=2.1731e+00 ppl=8.79                                                
Validation - loss=3.2752e+00 ppl=26.45 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 107 - |param|=5.23e+02 |g_param|=2.74e+05 loss=2.1491e+00 ppl=8.58                                                
Validation - loss=3.2886e+00 ppl=26.80 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 108 - |param|=5.24e+02 |g_param|=2.74e+05 loss=2.1650e+00 ppl=8.71                                                
Validation - loss=3.2823e+00 ppl=26.64 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 109 - |param|=5.26e+02 |g_param|=2.79e+05 loss=2.1444e+00 ppl=8.54                                                
Validation - loss=3.2777e+00 ppl=26.51 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 110 - |param|=5.27e+02 |g_param|=2.69e+05 loss=2.1092e+00 ppl=8.24                                                
Validation - loss=3.2985e+00 ppl=27.07 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 111 - |param|=5.28e+02 |g_param|=2.78e+05 loss=2.1052e+00 ppl=8.21                                                
Validation - loss=3.3117e+00 ppl=27.43 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 112 - |param|=5.29e+02 |g_param|=2.82e+05 loss=2.1107e+00 ppl=8.25                                                
Validation - loss=3.2928e+00 ppl=26.92 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 113 - |param|=5.30e+02 |g_param|=2.93e+05 loss=2.1481e+00 ppl=8.57                                                
Validation - loss=3.2878e+00 ppl=26.78 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 114 - |param|=5.31e+02 |g_param|=2.83e+05 loss=2.1179e+00 ppl=8.31                                                
Validation - loss=3.3123e+00 ppl=27.45 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 115 - |param|=5.32e+02 |g_param|=2.94e+05 loss=2.1201e+00 ppl=8.33                                                
Validation - loss=3.3101e+00 ppl=27.39 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 116 - |param|=5.33e+02 |g_param|=5.13e+05 loss=2.1039e+00 ppl=8.20                                                
Validation - loss=3.3342e+00 ppl=28.06 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 117 - |param|=5.34e+02 |g_param|=5.50e+05 loss=2.0860e+00 ppl=8.05                                                
Validation - loss=3.3249e+00 ppl=27.80 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 118 - |param|=5.36e+02 |g_param|=5.56e+05 loss=2.0633e+00 ppl=7.87                                                
Validation - loss=3.3203e+00 ppl=27.67 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 119 - |param|=5.37e+02 |g_param|=5.50e+05 loss=2.0568e+00 ppl=7.82                                                
Validation - loss=3.3080e+00 ppl=27.33 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 120 - |param|=5.38e+02 |g_param|=5.51e+05 loss=2.0547e+00 ppl=7.80                                                
Validation - loss=3.3078e+00 ppl=27.32 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 121 - |param|=5.39e+02 |g_param|=5.60e+05 loss=2.0485e+00 ppl=7.76                                                
Validation - loss=3.3206e+00 ppl=27.68 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 122 - |param|=5.40e+02 |g_param|=6.00e+05 loss=2.0749e+00 ppl=7.96                                                
Validation - loss=3.3180e+00 ppl=27.61 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 123 - |param|=5.41e+02 |g_param|=5.88e+05 loss=2.0716e+00 ppl=7.94                                                
Validation - loss=3.3339e+00 ppl=28.05 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 124 - |param|=5.42e+02 |g_param|=3.24e+05 loss=2.0374e+00 ppl=7.67                                                
Validation - loss=3.3422e+00 ppl=28.28 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 125 - |param|=5.43e+02 |g_param|=2.91e+05 loss=2.0221e+00 ppl=7.55                                                
Validation - loss=3.3425e+00 ppl=28.29 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 126 - |param|=5.44e+02 |g_param|=2.84e+05 loss=2.0484e+00 ppl=7.76                                                
Validation - loss=3.3358e+00 ppl=28.10 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 127 - |param|=5.45e+02 |g_param|=2.98e+05 loss=2.0531e+00 ppl=7.79                                                
Validation - loss=3.3370e+00 ppl=28.13 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 128 - |param|=5.46e+02 |g_param|=3.05e+05 loss=2.0411e+00 ppl=7.70                                                
Validation - loss=3.3511e+00 ppl=28.54 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 129 - |param|=5.47e+02 |g_param|=2.99e+05 loss=2.0230e+00 ppl=7.56                                                
Validation - loss=3.3476e+00 ppl=28.43 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 130 - |param|=5.49e+02 |g_param|=3.02e+05 loss=2.0069e+00 ppl=7.44                                                
Validation - loss=3.3483e+00 ppl=28.45 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 131 - |param|=5.50e+02 |g_param|=2.92e+05 loss=1.9858e+00 ppl=7.28                                                
Validation - loss=3.3474e+00 ppl=28.43 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 132 - |param|=5.51e+02 |g_param|=2.88e+05 loss=1.9867e+00 ppl=7.29                                                
Validation - loss=3.3762e+00 ppl=29.26 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 133 - |param|=5.52e+02 |g_param|=2.89e+05 loss=2.0029e+00 ppl=7.41                                                
Validation - loss=3.3651e+00 ppl=28.94 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 134 - |param|=5.53e+02 |g_param|=2.91e+05 loss=1.9673e+00 ppl=7.15                                                
Validation - loss=3.3464e+00 ppl=28.40 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 135 - |param|=5.54e+02 |g_param|=3.24e+05 loss=2.0408e+00 ppl=7.70                                                
Validation - loss=3.3572e+00 ppl=28.71 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 136 - |param|=5.55e+02 |g_param|=2.91e+05 loss=1.9610e+00 ppl=7.11                                                
Validation - loss=3.3729e+00 ppl=29.16 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 137 - |param|=5.56e+02 |g_param|=3.01e+05 loss=1.9778e+00 ppl=7.23                                                
Validation - loss=3.3817e+00 ppl=29.42 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 138 - |param|=5.57e+02 |g_param|=3.09e+05 loss=1.9718e+00 ppl=7.18                                                
Validation - loss=3.3715e+00 ppl=29.12 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 139 - |param|=5.58e+02 |g_param|=2.93e+05 loss=1.9579e+00 ppl=7.08                                                
Validation - loss=3.3628e+00 ppl=28.87 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 140 - |param|=5.59e+02 |g_param|=5.21e+05 loss=1.9509e+00 ppl=7.03                                                
Validation - loss=3.3760e+00 ppl=29.25 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 141 - |param|=5.60e+02 |g_param|=5.89e+05 loss=1.9461e+00 ppl=7.00                                                
Validation - loss=3.3893e+00 ppl=29.65 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 142 - |param|=5.61e+02 |g_param|=6.29e+05 loss=1.9542e+00 ppl=7.06                                                
Validation - loss=3.4089e+00 ppl=30.23 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 143 - |param|=5.63e+02 |g_param|=6.59e+05 loss=1.9746e+00 ppl=7.20                                                
Validation - loss=3.4108e+00 ppl=30.29 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 144 - |param|=5.64e+02 |g_param|=6.15e+05 loss=1.9470e+00 ppl=7.01                                                
Validation - loss=3.3773e+00 ppl=29.29 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 145 - |param|=5.65e+02 |g_param|=6.18e+05 loss=1.9290e+00 ppl=6.88                                                
Validation - loss=3.4055e+00 ppl=30.13 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 146 - |param|=5.66e+02 |g_param|=6.20e+05 loss=1.9301e+00 ppl=6.89                                                
Validation - loss=3.4209e+00 ppl=30.60 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 147 - |param|=5.67e+02 |g_param|=3.28e+05 loss=1.9117e+00 ppl=6.76                                                
Validation - loss=3.4094e+00 ppl=30.25 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 148 - |param|=5.68e+02 |g_param|=3.29e+05 loss=1.9584e+00 ppl=7.09                                                
Validation - loss=3.4253e+00 ppl=30.73 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 149 - |param|=5.69e+02 |g_param|=2.96e+05 loss=1.8939e+00 ppl=6.65                                                
Validation - loss=3.4198e+00 ppl=30.56 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 150 - |param|=5.70e+02 |g_param|=3.10e+05 loss=1.9037e+00 ppl=6.71                                                
Validation - loss=3.4305e+00 ppl=30.89 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 151 - |param|=5.71e+02 |g_param|=3.08e+05 loss=1.8934e+00 ppl=6.64                                                
Validation - loss=3.4466e+00 ppl=31.39 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 152 - |param|=5.72e+02 |g_param|=3.20e+05 loss=1.9043e+00 ppl=6.71                                                
Validation - loss=3.4174e+00 ppl=30.49 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 153 - |param|=5.73e+02 |g_param|=3.14e+05 loss=1.8844e+00 ppl=6.58                                                
Validation - loss=3.4293e+00 ppl=30.86 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 154 - |param|=5.74e+02 |g_param|=3.17e+05 loss=1.9090e+00 ppl=6.75                                                
Validation - loss=3.4094e+00 ppl=30.25 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 155 - |param|=5.75e+02 |g_param|=2.98e+05 loss=1.8804e+00 ppl=6.56                                                
Validation - loss=3.4358e+00 ppl=31.06 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 156 - |param|=5.76e+02 |g_param|=3.04e+05 loss=1.8912e+00 ppl=6.63                                                
Validation - loss=3.4348e+00 ppl=31.03 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 157 - |param|=5.77e+02 |g_param|=3.07e+05 loss=1.8712e+00 ppl=6.50                                                
Validation - loss=3.4250e+00 ppl=30.72 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 158 - |param|=5.78e+02 |g_param|=3.09e+05 loss=1.8750e+00 ppl=6.52                                                
Validation - loss=3.4533e+00 ppl=31.61 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 159 - |param|=5.79e+02 |g_param|=3.15e+05 loss=1.8600e+00 ppl=6.42                                                
Validation - loss=3.4525e+00 ppl=31.58 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 160 - |param|=5.80e+02 |g_param|=3.04e+05 loss=1.8407e+00 ppl=6.30                                                
Validation - loss=3.4677e+00 ppl=32.06 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 161 - |param|=5.81e+02 |g_param|=3.13e+05 loss=1.8556e+00 ppl=6.40                                                
Validation - loss=3.4668e+00 ppl=32.03 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 162 - |param|=5.82e+02 |g_param|=3.04e+05 loss=1.8579e+00 ppl=6.41                                                
Validation - loss=3.4668e+00 ppl=32.04 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 163 - |param|=5.83e+02 |g_param|=5.70e+05 loss=1.8591e+00 ppl=6.42                                                
Validation - loss=3.4568e+00 ppl=31.72 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 164 - |param|=5.84e+02 |g_param|=6.20e+05 loss=1.8467e+00 ppl=6.34                                                
Validation - loss=3.4709e+00 ppl=32.16 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 165 - |param|=5.85e+02 |g_param|=5.52e+05 loss=1.8708e+00 ppl=6.49                                                
Validation - loss=3.4745e+00 ppl=32.28 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 166 - |param|=5.86e+02 |g_param|=3.05e+05 loss=1.8430e+00 ppl=6.32                                                
Validation - loss=3.4882e+00 ppl=32.73 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 167 - |param|=5.87e+02 |g_param|=3.24e+05 loss=1.8450e+00 ppl=6.33                                                
Validation - loss=3.4609e+00 ppl=31.85 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 168 - |param|=5.88e+02 |g_param|=3.21e+05 loss=1.8356e+00 ppl=6.27                                                
Validation - loss=3.5070e+00 ppl=33.35 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 169 - |param|=5.89e+02 |g_param|=3.18e+05 loss=1.8435e+00 ppl=6.32                                                
Validation - loss=3.4880e+00 ppl=32.72 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 170 - |param|=5.90e+02 |g_param|=3.39e+05 loss=1.8481e+00 ppl=6.35                                                
Validation - loss=3.4644e+00 ppl=31.96 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 171 - |param|=5.91e+02 |g_param|=3.17e+05 loss=1.8164e+00 ppl=6.15                                                
Validation - loss=3.5014e+00 ppl=33.16 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 172 - |param|=5.92e+02 |g_param|=3.03e+05 loss=1.8127e+00 ppl=6.13                                                
Validation - loss=3.5015e+00 ppl=33.17 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 173 - |param|=5.93e+02 |g_param|=3.17e+05 loss=1.8134e+00 ppl=6.13                                                
Validation - loss=3.5148e+00 ppl=33.61 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 174 - |param|=5.94e+02 |g_param|=3.18e+05 loss=1.8216e+00 ppl=6.18                                                
Validation - loss=3.4794e+00 ppl=32.44 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 175 - |param|=5.95e+02 |g_param|=3.25e+05 loss=1.8000e+00 ppl=6.05                                                
Validation - loss=3.5099e+00 ppl=33.45 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 176 - |param|=5.96e+02 |g_param|=3.37e+05 loss=1.8294e+00 ppl=6.23                                                
Validation - loss=3.4974e+00 ppl=33.03 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 177 - |param|=5.97e+02 |g_param|=3.07e+05 loss=1.7978e+00 ppl=6.04                                                
Validation - loss=3.5022e+00 ppl=33.19 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 178 - |param|=5.98e+02 |g_param|=3.41e+05 loss=1.8174e+00 ppl=6.16                                                
Validation - loss=3.5345e+00 ppl=34.28 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 179 - |param|=5.99e+02 |g_param|=3.11e+05 loss=1.7866e+00 ppl=5.97                                                
Validation - loss=3.5193e+00 ppl=33.76 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 180 - |param|=5.99e+02 |g_param|=3.08e+05 loss=1.7850e+00 ppl=5.96                                                
Validation - loss=3.5259e+00 ppl=33.99 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 181 - |param|=6.00e+02 |g_param|=3.25e+05 loss=1.7977e+00 ppl=6.04                                                
Validation - loss=3.5112e+00 ppl=33.49 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 182 - |param|=6.01e+02 |g_param|=6.06e+05 loss=1.7897e+00 ppl=5.99                                                
Validation - loss=3.5126e+00 ppl=33.54 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 183 - |param|=6.02e+02 |g_param|=6.56e+05 loss=1.7813e+00 ppl=5.94                                                
Validation - loss=3.5251e+00 ppl=33.96 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 184 - |param|=6.03e+02 |g_param|=3.55e+05 loss=1.7740e+00 ppl=5.89                                                
Validation - loss=3.5302e+00 ppl=34.13 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 185 - |param|=6.04e+02 |g_param|=3.39e+05 loss=1.7959e+00 ppl=6.02                                                
Validation - loss=3.5364e+00 ppl=34.34 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 186 - |param|=6.05e+02 |g_param|=3.35e+05 loss=1.7889e+00 ppl=5.98                                                
Validation - loss=3.5419e+00 ppl=34.53 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 187 - |param|=6.06e+02 |g_param|=3.19e+05 loss=1.7918e+00 ppl=6.00                                                
Validation - loss=3.5373e+00 ppl=34.37 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 188 - |param|=6.07e+02 |g_param|=3.12e+05 loss=1.7768e+00 ppl=5.91                                                
Validation - loss=3.5614e+00 ppl=35.21 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 189 - |param|=6.08e+02 |g_param|=3.46e+05 loss=1.7872e+00 ppl=5.97                                                
Validation - loss=3.5558e+00 ppl=35.02 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 190 - |param|=6.09e+02 |g_param|=3.37e+05 loss=1.7608e+00 ppl=5.82                                                
Validation - loss=3.5580e+00 ppl=35.09 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 191 - |param|=6.10e+02 |g_param|=3.31e+05 loss=1.7648e+00 ppl=5.84                                                
Validation - loss=3.5650e+00 ppl=35.34 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 192 - |param|=6.10e+02 |g_param|=3.39e+05 loss=1.7584e+00 ppl=5.80                                                
Validation - loss=3.5855e+00 ppl=36.07 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 193 - |param|=6.11e+02 |g_param|=3.42e+05 loss=1.7675e+00 ppl=5.86                                                
Validation - loss=3.5861e+00 ppl=36.09 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 194 - |param|=6.12e+02 |g_param|=3.18e+05 loss=1.7396e+00 ppl=5.70                                                
Validation - loss=3.5657e+00 ppl=35.36 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 195 - |param|=6.13e+02 |g_param|=3.20e+05 loss=1.7448e+00 ppl=5.72                                                
Validation - loss=3.5749e+00 ppl=35.69 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 196 - |param|=6.14e+02 |g_param|=3.22e+05 loss=1.7442e+00 ppl=5.72                                                
Validation - loss=3.5836e+00 ppl=36.00 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 197 - |param|=6.15e+02 |g_param|=3.42e+05 loss=1.7452e+00 ppl=5.73                                                
Validation - loss=3.5764e+00 ppl=35.74 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 198 - |param|=6.16e+02 |g_param|=3.31e+05 loss=1.7269e+00 ppl=5.62                                                
Validation - loss=3.5714e+00 ppl=35.57 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 199 - |param|=6.17e+02 |g_param|=3.47e+05 loss=1.7518e+00 ppl=5.77                                                
Validation - loss=3.5897e+00 ppl=36.22 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 200 - |param|=6.18e+02 |g_param|=5.79e+05 loss=1.7414e+00 ppl=5.71                                                
Validation - loss=3.5921e+00 ppl=36.31 best_loss=3.1661e+00 best_ppl=23.71                                              
Epoch 1 - |param|=4.13e+02 |g_param|=2.75e+05 loss=4.7409e+00 ppl=114.54                                                
Validation - loss=4.2074e+00 ppl=67.18 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=4.14e+02 |g_param|=1.53e+05 loss=4.3525e+00 ppl=77.67                                                 
Validation - loss=3.9809e+00 ppl=53.57 best_loss=4.2074e+00 best_ppl=67.18                                              
Epoch 3 - |param|=4.14e+02 |g_param|=1.19e+05 loss=4.2218e+00 ppl=68.16                                                 
Validation - loss=4.2486e+00 ppl=70.01 best_loss=3.9809e+00 best_ppl=53.57                                              
Epoch 4 - |param|=4.14e+02 |g_param|=1.12e+05 loss=4.2325e+00 ppl=68.89                                                 
Validation - loss=4.3048e+00 ppl=74.05 best_loss=3.9809e+00 best_ppl=53.57                                              
Epoch 5 - |param|=4.14e+02 |g_param|=1.18e+05 loss=4.3016e+00 ppl=73.82                                                 
Validation - loss=4.0697e+00 ppl=58.54 best_loss=3.9809e+00 best_ppl=53.57                                              
Epoch 6 - |param|=4.14e+02 |g_param|=1.11e+05 loss=4.2648e+00 ppl=71.15                                                 
Validation - loss=4.2215e+00 ppl=68.14 best_loss=3.9809e+00 best_ppl=53.57                                              
Epoch 7 - |param|=4.15e+02 |g_param|=9.86e+04 loss=4.1212e+00 ppl=61.64                                                 
Validation - loss=3.9546e+00 ppl=52.18 best_loss=3.9809e+00 best_ppl=53.57                                              
Epoch 8 - |param|=4.15e+02 |g_param|=7.42e+04 loss=3.9271e+00 ppl=50.76                                                 
Validation - loss=3.8522e+00 ppl=47.10 best_loss=3.9546e+00 best_ppl=52.18                                              
Epoch 9 - |param|=4.16e+02 |g_param|=6.57e+04 loss=3.8179e+00 ppl=45.51                                                 
Validation - loss=3.6632e+00 ppl=38.98 best_loss=3.8522e+00 best_ppl=47.10                                              
Epoch 10 - |param|=4.16e+02 |g_param|=5.28e+04 loss=3.6920e+00 ppl=40.13                                                
Validation - loss=3.5750e+00 ppl=35.70 best_loss=3.6632e+00 best_ppl=38.98                                              
Epoch 11 - |param|=4.17e+02 |g_param|=4.96e+04 loss=3.5652e+00 ppl=35.35                                                
Validation - loss=3.4182e+00 ppl=30.51 best_loss=3.5750e+00 best_ppl=35.70                                              
Epoch 12 - |param|=4.18e+02 |g_param|=4.62e+04 loss=3.6110e+00 ppl=37.00                                                
Validation - loss=3.3311e+00 ppl=27.97 best_loss=3.4182e+00 best_ppl=30.51                                              
Epoch 13 - |param|=4.19e+02 |g_param|=4.60e+04 loss=3.4388e+00 ppl=31.15                                                
Validation - loss=3.3445e+00 ppl=28.35 best_loss=3.3311e+00 best_ppl=27.97                                              
Epoch 14 - |param|=4.20e+02 |g_param|=4.06e+04 loss=3.4183e+00 ppl=30.52                                                
Validation - loss=3.2703e+00 ppl=26.32 best_loss=3.3311e+00 best_ppl=27.97                                              
Epoch 15 - |param|=4.20e+02 |g_param|=4.10e+04 loss=3.2846e+00 ppl=26.70                                                
Validation - loss=3.2127e+00 ppl=24.85 best_loss=3.2703e+00 best_ppl=26.32                                              
Epoch 16 - |param|=4.21e+02 |g_param|=4.04e+04 loss=3.2255e+00 ppl=25.17                                                
Validation - loss=3.2238e+00 ppl=25.12 best_loss=3.2127e+00 best_ppl=24.85                                              
Epoch 17 - |param|=4.22e+02 |g_param|=4.67e+04 loss=3.3183e+00 ppl=27.61                                                
Validation - loss=3.1371e+00 ppl=23.04 best_loss=3.2127e+00 best_ppl=24.85                                              
Epoch 18 - |param|=4.22e+02 |g_param|=6.98e+04 loss=3.1527e+00 ppl=23.40                                                
Validation - loss=3.1332e+00 ppl=22.95 best_loss=3.1371e+00 best_ppl=23.04                                              
Epoch 19 - |param|=4.23e+02 |g_param|=8.06e+04 loss=3.1635e+00 ppl=23.65                                                
Validation - loss=3.1030e+00 ppl=22.27 best_loss=3.1332e+00 best_ppl=22.95                                              
Epoch 20 - |param|=4.24e+02 |g_param|=8.37e+04 loss=3.0824e+00 ppl=21.81                                                
Validation - loss=3.0707e+00 ppl=21.56 best_loss=3.1030e+00 best_ppl=22.27                                              
Epoch 21 - |param|=4.24e+02 |g_param|=7.76e+04 loss=3.0202e+00 ppl=20.49                                                
Validation - loss=3.0549e+00 ppl=21.22 best_loss=3.0707e+00 best_ppl=21.56                                              
Epoch 22 - |param|=4.25e+02 |g_param|=7.98e+04 loss=2.9949e+00 ppl=19.98                                                
Validation - loss=3.0403e+00 ppl=20.91 best_loss=3.0549e+00 best_ppl=21.22                                              
Epoch 23 - |param|=4.26e+02 |g_param|=8.26e+04 loss=3.0208e+00 ppl=20.51                                                
Validation - loss=3.0414e+00 ppl=20.93 best_loss=3.0403e+00 best_ppl=20.91                                              
Epoch 24 - |param|=4.26e+02 |g_param|=7.87e+04 loss=2.9230e+00 ppl=18.60                                                
Validation - loss=3.0002e+00 ppl=20.09 best_loss=3.0403e+00 best_ppl=20.91                                              
Epoch 25 - |param|=4.27e+02 |g_param|=8.04e+04 loss=2.8997e+00 ppl=18.17                                                
Validation - loss=3.0125e+00 ppl=20.34 best_loss=3.0002e+00 best_ppl=20.09                                              
Epoch 26 - |param|=4.28e+02 |g_param|=8.18e+04 loss=2.8784e+00 ppl=17.79                                                
Validation - loss=2.9685e+00 ppl=19.46 best_loss=3.0002e+00 best_ppl=20.09                                              
Epoch 27 - |param|=4.29e+02 |g_param|=8.22e+04 loss=2.8614e+00 ppl=17.49                                                
Validation - loss=2.9693e+00 ppl=19.48 best_loss=2.9685e+00 best_ppl=19.46                                              
Epoch 28 - |param|=4.29e+02 |g_param|=8.42e+04 loss=2.8263e+00 ppl=16.88                                                
Validation - loss=2.9523e+00 ppl=19.15 best_loss=2.9685e+00 best_ppl=19.46                                              
Epoch 29 - |param|=4.30e+02 |g_param|=8.17e+04 loss=2.7601e+00 ppl=15.80                                                
Validation - loss=2.9515e+00 ppl=19.13 best_loss=2.9523e+00 best_ppl=19.15                                              
Epoch 30 - |param|=4.31e+02 |g_param|=8.35e+04 loss=2.7430e+00 ppl=15.53                                                
Validation - loss=2.9575e+00 ppl=19.25 best_loss=2.9515e+00 best_ppl=19.13                                              
Epoch 31 - |param|=4.32e+02 |g_param|=8.71e+04 loss=2.7443e+00 ppl=15.55                                                
Validation - loss=2.9185e+00 ppl=18.51 best_loss=2.9515e+00 best_ppl=19.13                                              
Epoch 32 - |param|=4.32e+02 |g_param|=8.88e+04 loss=2.7509e+00 ppl=15.66                                                
Validation - loss=2.9232e+00 ppl=18.60 best_loss=2.9185e+00 best_ppl=18.51                                              
Epoch 33 - |param|=4.33e+02 |g_param|=8.96e+04 loss=2.7434e+00 ppl=15.54                                                
Validation - loss=2.9355e+00 ppl=18.83 best_loss=2.9185e+00 best_ppl=18.51                                              
Epoch 34 - |param|=4.34e+02 |g_param|=1.39e+05 loss=2.6428e+00 ppl=14.05                                                
Validation - loss=2.9078e+00 ppl=18.32 best_loss=2.9185e+00 best_ppl=18.51                                              
Epoch 35 - |param|=4.35e+02 |g_param|=1.84e+05 loss=2.7146e+00 ppl=15.10                                                
Validation - loss=2.9070e+00 ppl=18.30 best_loss=2.9078e+00 best_ppl=18.32                                              
Epoch 36 - |param|=4.35e+02 |g_param|=1.82e+05 loss=2.6438e+00 ppl=14.07                                                
Validation - loss=2.9224e+00 ppl=18.59 best_loss=2.9070e+00 best_ppl=18.30                                              
Epoch 37 - |param|=4.36e+02 |g_param|=1.84e+05 loss=2.6212e+00 ppl=13.75                                                
Validation - loss=2.8958e+00 ppl=18.10 best_loss=2.9070e+00 best_ppl=18.30                                              
Epoch 38 - |param|=4.37e+02 |g_param|=1.76e+05 loss=2.5544e+00 ppl=12.86                                                
Validation - loss=2.8877e+00 ppl=17.95 best_loss=2.8958e+00 best_ppl=18.10                                              
Epoch 39 - |param|=4.38e+02 |g_param|=1.83e+05 loss=2.5750e+00 ppl=13.13                                                
Validation - loss=2.9029e+00 ppl=18.23 best_loss=2.8877e+00 best_ppl=17.95                                              
Epoch 40 - |param|=4.39e+02 |g_param|=1.84e+05 loss=2.5277e+00 ppl=12.52                                                
Validation - loss=2.8786e+00 ppl=17.79 best_loss=2.8877e+00 best_ppl=17.95                                              
Epoch 41 - |param|=4.39e+02 |g_param|=1.86e+05 loss=2.5203e+00 ppl=12.43                                                
Validation - loss=2.8894e+00 ppl=17.98 best_loss=2.8786e+00 best_ppl=17.79                                              
Epoch 42 - |param|=4.40e+02 |g_param|=1.91e+05 loss=2.5133e+00 ppl=12.35                                                
Validation - loss=2.8909e+00 ppl=18.01 best_loss=2.8786e+00 best_ppl=17.79                                              
Epoch 43 - |param|=4.41e+02 |g_param|=1.99e+05 loss=2.5678e+00 ppl=13.04                                                
Validation - loss=2.8847e+00 ppl=17.90 best_loss=2.8786e+00 best_ppl=17.79                                              
Epoch 44 - |param|=4.42e+02 |g_param|=2.04e+05 loss=2.5696e+00 ppl=13.06                                                
Validation - loss=2.8859e+00 ppl=17.92 best_loss=2.8786e+00 best_ppl=17.79                                              
Epoch 45 - |param|=4.42e+02 |g_param|=1.86e+05 loss=2.4284e+00 ppl=11.34                                                
Validation - loss=2.8713e+00 ppl=17.66 best_loss=2.8786e+00 best_ppl=17.79                                              
Epoch 46 - |param|=4.43e+02 |g_param|=1.94e+05 loss=2.4296e+00 ppl=11.35                                                
Validation - loss=2.8533e+00 ppl=17.35 best_loss=2.8713e+00 best_ppl=17.66                                              
Epoch 47 - |param|=4.44e+02 |g_param|=1.96e+05 loss=2.4227e+00 ppl=11.28                                                
Validation - loss=2.8811e+00 ppl=17.83 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 48 - |param|=4.45e+02 |g_param|=1.92e+05 loss=2.3967e+00 ppl=10.99                                                
Validation - loss=2.8603e+00 ppl=17.47 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 49 - |param|=4.46e+02 |g_param|=2.01e+05 loss=2.3711e+00 ppl=10.71                                                
Validation - loss=2.8618e+00 ppl=17.49 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 50 - |param|=4.47e+02 |g_param|=2.50e+05 loss=2.3695e+00 ppl=10.69                                                
Validation - loss=2.8723e+00 ppl=17.68 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 51 - |param|=4.47e+02 |g_param|=4.65e+05 loss=2.4590e+00 ppl=11.69                                                
Validation - loss=2.8757e+00 ppl=17.74 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 52 - |param|=4.48e+02 |g_param|=4.10e+05 loss=2.3599e+00 ppl=10.59                                                
Validation - loss=2.8765e+00 ppl=17.75 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 53 - |param|=4.49e+02 |g_param|=2.30e+05 loss=2.3157e+00 ppl=10.13                                                
Validation - loss=2.8687e+00 ppl=17.61 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 54 - |param|=4.50e+02 |g_param|=2.17e+05 loss=2.4073e+00 ppl=11.10                                                
Validation - loss=2.8579e+00 ppl=17.43 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 55 - |param|=4.51e+02 |g_param|=2.17e+05 loss=2.3591e+00 ppl=10.58                                                
Validation - loss=2.8585e+00 ppl=17.43 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 56 - |param|=4.52e+02 |g_param|=2.00e+05 loss=2.2850e+00 ppl=9.83                                                 
Validation - loss=2.8833e+00 ppl=17.87 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 57 - |param|=4.52e+02 |g_param|=2.03e+05 loss=2.2592e+00 ppl=9.57                                                 
Validation - loss=2.8633e+00 ppl=17.52 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 58 - |param|=4.53e+02 |g_param|=2.12e+05 loss=2.2863e+00 ppl=9.84                                                 
Validation - loss=2.8921e+00 ppl=18.03 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 59 - |param|=4.54e+02 |g_param|=2.16e+05 loss=2.2630e+00 ppl=9.61                                                 
Validation - loss=2.8917e+00 ppl=18.02 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 60 - |param|=4.55e+02 |g_param|=2.24e+05 loss=2.2871e+00 ppl=9.85                                                 
Validation - loss=2.8845e+00 ppl=17.89 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 61 - |param|=4.56e+02 |g_param|=2.21e+05 loss=2.2641e+00 ppl=9.62                                                 
Validation - loss=2.8753e+00 ppl=17.73 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 62 - |param|=4.57e+02 |g_param|=2.16e+05 loss=2.2286e+00 ppl=9.29                                                 
Validation - loss=2.8867e+00 ppl=17.93 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 63 - |param|=4.58e+02 |g_param|=2.19e+05 loss=2.2072e+00 ppl=9.09                                                 
Validation - loss=2.9038e+00 ppl=18.24 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 64 - |param|=4.59e+02 |g_param|=2.27e+05 loss=2.2085e+00 ppl=9.10                                                 
Validation - loss=2.9067e+00 ppl=18.30 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 65 - |param|=4.60e+02 |g_param|=2.23e+05 loss=2.2060e+00 ppl=9.08                                                 
Validation - loss=2.8853e+00 ppl=17.91 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 66 - |param|=4.60e+02 |g_param|=2.23e+05 loss=2.1913e+00 ppl=8.95                                                 
Validation - loss=2.8979e+00 ppl=18.14 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 67 - |param|=4.61e+02 |g_param|=2.35e+05 loss=2.2283e+00 ppl=9.28                                                 
Validation - loss=2.9167e+00 ppl=18.48 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 68 - |param|=4.62e+02 |g_param|=2.27e+05 loss=2.1787e+00 ppl=8.83                                                 
Validation - loss=2.9074e+00 ppl=18.31 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 69 - |param|=4.63e+02 |g_param|=4.28e+05 loss=2.1771e+00 ppl=8.82                                                 
Validation - loss=2.8961e+00 ppl=18.10 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 70 - |param|=4.64e+02 |g_param|=4.68e+05 loss=2.1736e+00 ppl=8.79                                                 
Validation - loss=2.9240e+00 ppl=18.61 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 71 - |param|=4.65e+02 |g_param|=2.84e+05 loss=2.1508e+00 ppl=8.59                                                 
Validation - loss=2.9136e+00 ppl=18.42 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 72 - |param|=4.66e+02 |g_param|=2.29e+05 loss=2.1276e+00 ppl=8.39                                                 
Validation - loss=2.9315e+00 ppl=18.76 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 73 - |param|=4.67e+02 |g_param|=2.36e+05 loss=2.1274e+00 ppl=8.39                                                 
Validation - loss=2.9186e+00 ppl=18.52 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 74 - |param|=4.68e+02 |g_param|=2.34e+05 loss=2.1040e+00 ppl=8.20                                                 
Validation - loss=2.9207e+00 ppl=18.55 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 75 - |param|=4.69e+02 |g_param|=2.39e+05 loss=2.1023e+00 ppl=8.19                                                 
Validation - loss=2.9417e+00 ppl=18.95 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 76 - |param|=4.70e+02 |g_param|=2.45e+05 loss=2.1236e+00 ppl=8.36                                                 
Validation - loss=2.9407e+00 ppl=18.93 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 77 - |param|=4.71e+02 |g_param|=2.37e+05 loss=2.0850e+00 ppl=8.04                                                 
Validation - loss=2.9091e+00 ppl=18.34 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 78 - |param|=4.72e+02 |g_param|=2.38e+05 loss=2.0656e+00 ppl=7.89                                                 
Validation - loss=2.9308e+00 ppl=18.74 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 79 - |param|=4.73e+02 |g_param|=2.36e+05 loss=2.0737e+00 ppl=7.95                                                 
Validation - loss=2.9402e+00 ppl=18.92 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 80 - |param|=4.74e+02 |g_param|=2.42e+05 loss=2.0638e+00 ppl=7.88                                                 
Validation - loss=2.9550e+00 ppl=19.20 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 81 - |param|=4.75e+02 |g_param|=2.41e+05 loss=2.0481e+00 ppl=7.75                                                 
Validation - loss=2.9512e+00 ppl=19.13 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 82 - |param|=4.76e+02 |g_param|=2.36e+05 loss=2.0281e+00 ppl=7.60                                                 
Validation - loss=2.9576e+00 ppl=19.25 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 83 - |param|=4.77e+02 |g_param|=2.43e+05 loss=2.0942e+00 ppl=8.12                                                 
Validation - loss=2.9658e+00 ppl=19.41 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 84 - |param|=4.78e+02 |g_param|=2.55e+05 loss=2.0735e+00 ppl=7.95                                                 
Validation - loss=2.9655e+00 ppl=19.41 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 85 - |param|=4.79e+02 |g_param|=2.54e+05 loss=2.0560e+00 ppl=7.81                                                 
Validation - loss=2.9660e+00 ppl=19.41 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 86 - |param|=4.80e+02 |g_param|=2.65e+05 loss=2.0607e+00 ppl=7.85                                                 
Validation - loss=2.9766e+00 ppl=19.62 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 87 - |param|=4.81e+02 |g_param|=3.74e+05 loss=2.0226e+00 ppl=7.56                                                 
Validation - loss=2.9645e+00 ppl=19.39 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 88 - |param|=4.82e+02 |g_param|=3.52e+05 loss=2.0138e+00 ppl=7.49                                                 
Validation - loss=2.9635e+00 ppl=19.37 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 89 - |param|=4.83e+02 |g_param|=2.68e+05 loss=2.0556e+00 ppl=7.81                                                 
Validation - loss=2.9756e+00 ppl=19.60 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 90 - |param|=4.84e+02 |g_param|=2.58e+05 loss=2.0187e+00 ppl=7.53                                                 
Validation - loss=2.9849e+00 ppl=19.78 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 91 - |param|=4.85e+02 |g_param|=2.56e+05 loss=1.9866e+00 ppl=7.29                                                 
Validation - loss=2.9780e+00 ppl=19.65 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 92 - |param|=4.86e+02 |g_param|=2.59e+05 loss=1.9945e+00 ppl=7.35                                                 
Validation - loss=2.9952e+00 ppl=19.99 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 93 - |param|=4.87e+02 |g_param|=2.60e+05 loss=1.9829e+00 ppl=7.26                                                 
Validation - loss=2.9778e+00 ppl=19.64 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 94 - |param|=4.88e+02 |g_param|=2.50e+05 loss=1.9634e+00 ppl=7.12                                                 
Validation - loss=2.9949e+00 ppl=19.98 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 95 - |param|=4.89e+02 |g_param|=2.46e+05 loss=1.9565e+00 ppl=7.07                                                 
Validation - loss=3.0130e+00 ppl=20.35 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 96 - |param|=4.90e+02 |g_param|=2.55e+05 loss=1.9475e+00 ppl=7.01                                                 
Validation - loss=2.9869e+00 ppl=19.82 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 97 - |param|=4.91e+02 |g_param|=2.73e+05 loss=1.9586e+00 ppl=7.09                                                 
Validation - loss=3.0026e+00 ppl=20.14 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 98 - |param|=4.92e+02 |g_param|=2.64e+05 loss=1.9481e+00 ppl=7.02                                                 
Validation - loss=3.0014e+00 ppl=20.11 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 99 - |param|=4.93e+02 |g_param|=2.57e+05 loss=1.9258e+00 ppl=6.86                                                 
Validation - loss=2.9981e+00 ppl=20.05 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 100 - |param|=4.94e+02 |g_param|=2.58e+05 loss=1.9198e+00 ppl=6.82                                                
Validation - loss=3.0180e+00 ppl=20.45 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 101 - |param|=4.95e+02 |g_param|=2.68e+05 loss=1.9347e+00 ppl=6.92                                                
Validation - loss=3.0164e+00 ppl=20.42 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 102 - |param|=4.96e+02 |g_param|=2.62e+05 loss=1.9279e+00 ppl=6.87                                                
Validation - loss=3.0133e+00 ppl=20.36 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 103 - |param|=4.97e+02 |g_param|=2.63e+05 loss=1.9029e+00 ppl=6.71                                                
Validation - loss=3.0083e+00 ppl=20.25 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 104 - |param|=4.98e+02 |g_param|=3.23e+05 loss=1.9261e+00 ppl=6.86                                                
Validation - loss=3.0168e+00 ppl=20.43 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 105 - |param|=4.99e+02 |g_param|=5.32e+05 loss=1.8942e+00 ppl=6.65                                                
Validation - loss=3.0064e+00 ppl=20.22 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 106 - |param|=5.00e+02 |g_param|=5.89e+05 loss=1.9544e+00 ppl=7.06                                                
Validation - loss=3.0294e+00 ppl=20.68 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 107 - |param|=5.02e+02 |g_param|=5.29e+05 loss=1.8782e+00 ppl=6.54                                                
Validation - loss=3.0263e+00 ppl=20.62 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 108 - |param|=5.03e+02 |g_param|=4.02e+05 loss=1.8801e+00 ppl=6.55                                                
Validation - loss=3.0189e+00 ppl=20.47 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 109 - |param|=5.04e+02 |g_param|=2.78e+05 loss=1.8957e+00 ppl=6.66                                                
Validation - loss=3.0170e+00 ppl=20.43 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 110 - |param|=5.05e+02 |g_param|=2.69e+05 loss=1.8529e+00 ppl=6.38                                                
Validation - loss=3.0367e+00 ppl=20.84 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 111 - |param|=5.06e+02 |g_param|=2.83e+05 loss=1.8948e+00 ppl=6.65                                                
Validation - loss=3.0317e+00 ppl=20.73 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 112 - |param|=5.07e+02 |g_param|=2.97e+05 loss=1.9126e+00 ppl=6.77                                                
Validation - loss=3.0475e+00 ppl=21.06 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 113 - |param|=5.08e+02 |g_param|=2.74e+05 loss=1.8657e+00 ppl=6.46                                                
Validation - loss=3.0621e+00 ppl=21.37 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 114 - |param|=5.09e+02 |g_param|=2.67e+05 loss=1.8321e+00 ppl=6.25                                                
Validation - loss=3.0561e+00 ppl=21.25 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 115 - |param|=5.10e+02 |g_param|=2.77e+05 loss=1.8444e+00 ppl=6.32                                                
Validation - loss=3.0516e+00 ppl=21.15 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 116 - |param|=5.11e+02 |g_param|=2.82e+05 loss=1.8386e+00 ppl=6.29                                                
Validation - loss=3.0731e+00 ppl=21.61 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 117 - |param|=5.12e+02 |g_param|=2.84e+05 loss=1.8461e+00 ppl=6.33                                                
Validation - loss=3.0593e+00 ppl=21.31 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 118 - |param|=5.13e+02 |g_param|=3.27e+05 loss=1.8978e+00 ppl=6.67                                                
Validation - loss=3.0648e+00 ppl=21.43 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 119 - |param|=5.14e+02 |g_param|=2.72e+05 loss=1.8210e+00 ppl=6.18                                                
Validation - loss=3.0515e+00 ppl=21.15 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 120 - |param|=5.15e+02 |g_param|=2.97e+05 loss=1.8544e+00 ppl=6.39                                                
Validation - loss=3.0459e+00 ppl=21.03 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 121 - |param|=5.17e+02 |g_param|=2.79e+05 loss=1.8294e+00 ppl=6.23                                                
Validation - loss=3.0752e+00 ppl=21.65 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 122 - |param|=5.18e+02 |g_param|=2.82e+05 loss=1.8264e+00 ppl=6.21                                                
Validation - loss=3.0642e+00 ppl=21.42 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 123 - |param|=5.19e+02 |g_param|=2.85e+05 loss=1.8017e+00 ppl=6.06                                                
Validation - loss=3.1069e+00 ppl=22.35 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 124 - |param|=5.20e+02 |g_param|=2.84e+05 loss=1.8118e+00 ppl=6.12                                                
Validation - loss=3.0907e+00 ppl=21.99 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 125 - |param|=5.21e+02 |g_param|=5.43e+05 loss=1.7868e+00 ppl=5.97                                                
Validation - loss=3.1000e+00 ppl=22.20 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 126 - |param|=5.22e+02 |g_param|=5.82e+05 loss=1.8127e+00 ppl=6.13                                                
Validation - loss=3.0970e+00 ppl=22.13 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 127 - |param|=5.23e+02 |g_param|=5.64e+05 loss=1.7772e+00 ppl=5.91                                                
Validation - loss=3.0947e+00 ppl=22.08 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 128 - |param|=5.24e+02 |g_param|=3.37e+05 loss=1.7880e+00 ppl=5.98                                                
Validation - loss=3.1209e+00 ppl=22.67 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 129 - |param|=5.25e+02 |g_param|=2.83e+05 loss=1.7645e+00 ppl=5.84                                                
Validation - loss=3.1151e+00 ppl=22.53 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 130 - |param|=5.26e+02 |g_param|=2.81e+05 loss=1.7538e+00 ppl=5.78                                                
Validation - loss=3.1045e+00 ppl=22.30 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 131 - |param|=5.27e+02 |g_param|=2.86e+05 loss=1.7530e+00 ppl=5.77                                                
Validation - loss=3.1023e+00 ppl=22.25 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 132 - |param|=5.28e+02 |g_param|=3.10e+05 loss=1.7963e+00 ppl=6.03                                                
Validation - loss=3.1107e+00 ppl=22.44 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 133 - |param|=5.29e+02 |g_param|=3.04e+05 loss=1.7849e+00 ppl=5.96                                                
Validation - loss=3.1294e+00 ppl=22.86 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 134 - |param|=5.30e+02 |g_param|=2.92e+05 loss=1.7545e+00 ppl=5.78                                                
Validation - loss=3.1006e+00 ppl=22.21 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 135 - |param|=5.31e+02 |g_param|=2.93e+05 loss=1.7537e+00 ppl=5.78                                                
Validation - loss=3.1293e+00 ppl=22.86 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 136 - |param|=5.32e+02 |g_param|=2.82e+05 loss=1.7654e+00 ppl=5.84                                                
Validation - loss=3.1132e+00 ppl=22.49 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 137 - |param|=5.33e+02 |g_param|=3.04e+05 loss=1.7721e+00 ppl=5.88                                                
Validation - loss=3.1103e+00 ppl=22.43 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 138 - |param|=5.35e+02 |g_param|=3.07e+05 loss=1.7672e+00 ppl=5.85                                                
Validation - loss=3.1341e+00 ppl=22.97 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 139 - |param|=5.36e+02 |g_param|=2.94e+05 loss=1.7359e+00 ppl=5.67                                                
Validation - loss=3.1452e+00 ppl=23.22 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 140 - |param|=5.37e+02 |g_param|=2.83e+05 loss=1.7323e+00 ppl=5.65                                                
Validation - loss=3.1119e+00 ppl=22.46 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 141 - |param|=5.38e+02 |g_param|=3.03e+05 loss=1.7470e+00 ppl=5.74                                                
Validation - loss=3.1243e+00 ppl=22.74 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 142 - |param|=5.39e+02 |g_param|=3.15e+05 loss=1.7425e+00 ppl=5.71                                                
Validation - loss=3.1288e+00 ppl=22.85 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 143 - |param|=5.40e+02 |g_param|=1.79e+05 loss=1.7142e+00 ppl=5.55                                                
Validation - loss=3.1263e+00 ppl=22.79 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 144 - |param|=5.41e+02 |g_param|=1.45e+05 loss=1.7445e+00 ppl=5.72                                                
Validation - loss=3.1463e+00 ppl=23.25 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 145 - |param|=5.42e+02 |g_param|=1.43e+05 loss=1.7005e+00 ppl=5.48                                                
Validation - loss=3.1449e+00 ppl=23.22 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 146 - |param|=5.43e+02 |g_param|=1.53e+05 loss=1.7159e+00 ppl=5.56                                                
Validation - loss=3.1526e+00 ppl=23.40 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 147 - |param|=5.44e+02 |g_param|=1.59e+05 loss=1.7107e+00 ppl=5.53                                                
Validation - loss=3.1443e+00 ppl=23.20 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 148 - |param|=5.45e+02 |g_param|=1.47e+05 loss=1.7053e+00 ppl=5.50                                                
Validation - loss=3.1240e+00 ppl=22.74 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 149 - |param|=5.46e+02 |g_param|=1.52e+05 loss=1.6972e+00 ppl=5.46                                                
Validation - loss=3.1537e+00 ppl=23.42 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 150 - |param|=5.47e+02 |g_param|=1.47e+05 loss=1.6808e+00 ppl=5.37                                                
Validation - loss=3.1765e+00 ppl=23.96 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 151 - |param|=5.48e+02 |g_param|=1.50e+05 loss=1.6983e+00 ppl=5.46                                                
Validation - loss=3.1577e+00 ppl=23.52 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 152 - |param|=5.49e+02 |g_param|=1.44e+05 loss=1.6673e+00 ppl=5.30                                                
Validation - loss=3.1754e+00 ppl=23.94 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 153 - |param|=5.50e+02 |g_param|=1.41e+05 loss=1.7051e+00 ppl=5.50                                                
Validation - loss=3.1707e+00 ppl=23.82 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 154 - |param|=5.51e+02 |g_param|=1.51e+05 loss=1.6952e+00 ppl=5.45                                                
Validation - loss=3.1613e+00 ppl=23.60 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 155 - |param|=5.52e+02 |g_param|=1.47e+05 loss=1.6854e+00 ppl=5.39                                                
Validation - loss=3.1646e+00 ppl=23.68 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 156 - |param|=5.53e+02 |g_param|=1.55e+05 loss=1.6970e+00 ppl=5.46                                                
Validation - loss=3.1830e+00 ppl=24.12 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 157 - |param|=5.54e+02 |g_param|=1.50e+05 loss=1.6659e+00 ppl=5.29                                                
Validation - loss=3.1963e+00 ppl=24.44 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 158 - |param|=5.55e+02 |g_param|=1.50e+05 loss=1.6619e+00 ppl=5.27                                                
Validation - loss=3.2017e+00 ppl=24.57 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 159 - |param|=5.56e+02 |g_param|=2.23e+05 loss=1.7220e+00 ppl=5.60                                                
Validation - loss=3.1939e+00 ppl=24.38 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 160 - |param|=5.57e+02 |g_param|=3.05e+05 loss=1.6527e+00 ppl=5.22                                                
Validation - loss=3.2061e+00 ppl=24.68 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 161 - |param|=5.58e+02 |g_param|=3.06e+05 loss=1.6478e+00 ppl=5.20                                                
Validation - loss=3.2175e+00 ppl=24.97 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 162 - |param|=5.58e+02 |g_param|=2.95e+05 loss=1.6406e+00 ppl=5.16                                                
Validation - loss=3.2084e+00 ppl=24.74 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 163 - |param|=5.59e+02 |g_param|=3.21e+05 loss=1.6649e+00 ppl=5.29                                                
Validation - loss=3.2242e+00 ppl=25.13 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 164 - |param|=5.60e+02 |g_param|=3.44e+05 loss=1.6793e+00 ppl=5.36                                                
Validation - loss=3.1753e+00 ppl=23.94 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 165 - |param|=5.61e+02 |g_param|=3.13e+05 loss=1.6402e+00 ppl=5.16                                                
Validation - loss=3.2057e+00 ppl=24.67 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 166 - |param|=5.62e+02 |g_param|=3.03e+05 loss=1.6385e+00 ppl=5.15                                                
Validation - loss=3.2010e+00 ppl=24.56 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 167 - |param|=5.63e+02 |g_param|=3.37e+05 loss=1.6619e+00 ppl=5.27                                                
Validation - loss=3.2157e+00 ppl=24.92 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 168 - |param|=5.64e+02 |g_param|=3.09e+05 loss=1.6315e+00 ppl=5.11                                                
Validation - loss=3.2378e+00 ppl=25.48 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 169 - |param|=5.65e+02 |g_param|=3.23e+05 loss=1.6454e+00 ppl=5.18                                                
Validation - loss=3.2321e+00 ppl=25.33 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 170 - |param|=5.66e+02 |g_param|=3.01e+05 loss=1.6276e+00 ppl=5.09                                                
Validation - loss=3.2219e+00 ppl=25.07 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 171 - |param|=5.67e+02 |g_param|=3.01e+05 loss=1.6249e+00 ppl=5.08                                                
Validation - loss=3.2069e+00 ppl=24.70 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 172 - |param|=5.68e+02 |g_param|=3.11e+05 loss=1.6052e+00 ppl=4.98                                                
Validation - loss=3.2100e+00 ppl=24.78 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 173 - |param|=5.69e+02 |g_param|=3.00e+05 loss=1.6101e+00 ppl=5.00                                                
Validation - loss=3.2261e+00 ppl=25.18 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 174 - |param|=5.70e+02 |g_param|=3.00e+05 loss=1.5996e+00 ppl=4.95                                                
Validation - loss=3.2367e+00 ppl=25.45 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 175 - |param|=5.71e+02 |g_param|=3.22e+05 loss=1.6068e+00 ppl=4.99                                                
Validation - loss=3.2322e+00 ppl=25.34 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 176 - |param|=5.72e+02 |g_param|=4.42e+05 loss=1.5998e+00 ppl=4.95                                                
Validation - loss=3.2518e+00 ppl=25.84 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 177 - |param|=5.73e+02 |g_param|=3.10e+05 loss=1.5930e+00 ppl=4.92                                                
Validation - loss=3.2405e+00 ppl=25.55 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 178 - |param|=5.73e+02 |g_param|=3.14e+05 loss=1.5929e+00 ppl=4.92                                                
Validation - loss=3.2285e+00 ppl=25.24 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 179 - |param|=5.74e+02 |g_param|=3.05e+05 loss=1.5998e+00 ppl=4.95                                                
Validation - loss=3.2397e+00 ppl=25.53 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 180 - |param|=5.75e+02 |g_param|=3.17e+05 loss=1.6018e+00 ppl=4.96                                                
Validation - loss=3.2421e+00 ppl=25.59 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 181 - |param|=5.76e+02 |g_param|=3.08e+05 loss=1.5812e+00 ppl=4.86                                                
Validation - loss=3.2442e+00 ppl=25.64 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 182 - |param|=5.77e+02 |g_param|=3.15e+05 loss=1.5790e+00 ppl=4.85                                                
Validation - loss=3.2830e+00 ppl=26.66 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 183 - |param|=5.78e+02 |g_param|=3.06e+05 loss=1.5825e+00 ppl=4.87                                                
Validation - loss=3.2672e+00 ppl=26.24 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 184 - |param|=5.79e+02 |g_param|=3.12e+05 loss=1.5810e+00 ppl=4.86                                                
Validation - loss=3.2526e+00 ppl=25.86 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 185 - |param|=5.80e+02 |g_param|=3.03e+05 loss=1.5765e+00 ppl=4.84                                                
Validation - loss=3.2615e+00 ppl=26.09 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 186 - |param|=5.81e+02 |g_param|=3.10e+05 loss=1.5719e+00 ppl=4.82                                                
Validation - loss=3.2405e+00 ppl=25.55 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 187 - |param|=5.82e+02 |g_param|=3.19e+05 loss=1.5751e+00 ppl=4.83                                                
Validation - loss=3.2501e+00 ppl=25.79 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 188 - |param|=5.82e+02 |g_param|=3.17e+05 loss=1.5858e+00 ppl=4.88                                                
Validation - loss=3.2551e+00 ppl=25.92 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 189 - |param|=5.83e+02 |g_param|=3.35e+05 loss=1.5788e+00 ppl=4.85                                                
Validation - loss=3.2804e+00 ppl=26.59 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 190 - |param|=5.84e+02 |g_param|=3.21e+05 loss=1.5605e+00 ppl=4.76                                                
Validation - loss=3.2646e+00 ppl=26.17 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 191 - |param|=5.85e+02 |g_param|=3.12e+05 loss=1.5438e+00 ppl=4.68                                                
Validation - loss=3.2848e+00 ppl=26.70 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 192 - |param|=5.86e+02 |g_param|=3.20e+05 loss=1.5752e+00 ppl=4.83                                                
Validation - loss=3.2790e+00 ppl=26.55 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 193 - |param|=5.87e+02 |g_param|=3.31e+05 loss=1.5496e+00 ppl=4.71                                                
Validation - loss=3.2940e+00 ppl=26.95 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 194 - |param|=5.88e+02 |g_param|=3.30e+05 loss=1.5603e+00 ppl=4.76                                                
Validation - loss=3.2801e+00 ppl=26.58 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 195 - |param|=5.88e+02 |g_param|=3.32e+05 loss=1.5698e+00 ppl=4.81                                                
Validation - loss=3.3078e+00 ppl=27.33 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 196 - |param|=5.89e+02 |g_param|=3.26e+05 loss=1.5546e+00 ppl=4.73                                                
Validation - loss=3.2920e+00 ppl=26.90 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 197 - |param|=5.90e+02 |g_param|=3.12e+05 loss=1.5432e+00 ppl=4.68                                                
Validation - loss=3.3021e+00 ppl=27.17 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 198 - |param|=5.91e+02 |g_param|=3.42e+05 loss=1.5648e+00 ppl=4.78                                                
Validation - loss=3.3175e+00 ppl=27.59 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 199 - |param|=5.92e+02 |g_param|=3.10e+05 loss=1.5541e+00 ppl=4.73                                                
Validation - loss=3.3302e+00 ppl=27.94 best_loss=2.8533e+00 best_ppl=17.35                                              
Epoch 200 - |param|=5.93e+02 |g_param|=3.38e+05 loss=1.5618e+00 ppl=4.77                                                
Validation - loss=3.2914e+00 ppl=26.88 best_loss=2.8533e+00 best_ppl=17.35                                              

real	12m19.771s
user	12m13.863s
sys	0m4.512s
(simple-nmt) ye@:~/exp/simple-nmt$
```

## Script for Testing/Evaluation (my-bk)

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Last Updated: 25 Mar 2022
# find all models and parse to translate.py for testing and multi-bleu.perl for evaluation with BLEU score
# used for seq2seq-DSL evaluation for Myanmar-Beik pair

for folder in {mybk-30epoch,mybk-40epoch,mybk-50epoch,mybk-60epoch,mybk-70epoch,mybk-80epoch,mybk-90epoch,mybk-100epoch};
do
   cd ./model/dsl/${folder};
   pwd;
   for i in *.pth;
   do
      MODEL=$i;

      # Testing X-Y
      python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang mybk < /home/ye/exp/simple-nmt/data/my-bk/syl/test.my > $MODEL.mybk.hyp

      # Evaluation with BLEU Score
      echo "Evaluation result for the model: $MODEL, mybk" | tee -a eval-results-xy-seq2seq.txt;
      cat $MODEL.mybk.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/my-bk/syl/test.bk | tee  -a eval-results-xy-seq2seq.txt;

      # Testing Y-X
      python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang bkmy < /home/ye/exp/simple-nmt/data/my-bk/syl/test.bk > $MODEL.bkmy.hyp

      # Evaluation with BLEU Score
      echo "Evaluation result for the model: $MODEL, bkmy" | tee -a eval-results-yx-seq2seq.txt;
      cat $MODEL.bkmy.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/my-bk/syl/test.my | tee  -a eval-results-yx-seq2seq.txt;
   done
   cd ~/exp/simple-nmt/;
   echo "==========";
done
```

## Seq2Seq-DSL, my-bk, 30epoch

training

```
{   'batch_size': 64,
    'dropout': 0.2,
    'dsl_lambda': 0.01,
    'dsl_n_warmup_epochs': 20,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'mybk',
    'lm_fn': './model/lm/mybk/lm-200epoch-mybk.pth',
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/dsl/mybk-30epoch/dsl-model-mybk.pth',
    'n_epochs': 30,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'train': '/home/ye/exp/simple-nmt/data/my-bk/syl/train',
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/my-bk/syl/dev',
    'verbose': 2,
    'word_vec_size': 128}
[LanguageModel(
  (emb): Embedding(1470, 128, padding_idx=1)
  (rnn): LSTM(128, 128, num_layers=4, batch_first=True, dropout=0.2)
  (out): Linear(in_features=128, out_features=1470, bias=True)
  (log_softmax): LogSoftmax(dim=-1)
), LanguageModel(
  (emb): Embedding(1315, 128, padding_idx=1)
  (rnn): LSTM(128, 128, num_layers=4, batch_first=True, dropout=0.2)
  (out): Linear(in_features=128, out_features=1315, bias=True)
  (log_softmax): LogSoftmax(dim=-1)
)]
[Seq2Seq(
  (emb_src): Embedding(1315, 128)
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
), Seq2Seq(
  (emb_src): Embedding(1470, 128)
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
)]
[NLLLoss(), NLLLoss()]
[Adam (
Parameter Group 0
    amsgrad: False
    betas: (0.9, 0.999)
    eps: 1e-08
    lr: 0.001
    weight_decay: 0
), Adam (
Parameter Group 0
    amsgrad: False
    betas: (0.9, 0.999)
    eps: 1e-08
    lr: 0.001
    weight_decay: 0
)]
Epoch 1 - |param|=8.50e+02 |g_param|=4.24e+05 loss_x2y=4.8680e+00 ppl_x2y=130.06 loss_y2x=4.7326e+00 ppl_y2x=113.59 dual_loss=0.0000e+00
Validation X2Y - loss=4.0126e+00 ppl=55.29 best_loss=inf best_ppl=inf
Validation Y2X - loss=3.9494e+00 ppl=51.90 best_loss=inf best_ppl=inf
Epoch 2 - |param|=8.50e+02 |g_param|=3.91e+05 loss_x2y=4.4606e+00 ppl_x2y=86.54 loss_y2x=4.2224e+00 ppl_y2x=68.20 dual_loss=0.0000e+00
Validation X2Y - loss=3.8916e+00 ppl=48.99 best_loss=4.0126e+00 best_ppl=55.29
Validation Y2X - loss=3.8141e+00 ppl=45.34 best_loss=3.9494e+00 best_ppl=51.90
Epoch 3 - |param|=8.50e+02 |g_param|=3.40e+05 loss_x2y=4.4565e+00 ppl_x2y=86.19 loss_y2x=4.1931e+00 ppl_y2x=66.23 dual_loss=0.0000e+00
Validation X2Y - loss=3.8660e+00 ppl=47.75 best_loss=3.8916e+00 best_ppl=48.99
Validation Y2X - loss=3.7358e+00 ppl=41.92 best_loss=3.8141e+00 best_ppl=45.34
Epoch 4 - |param|=8.51e+02 |g_param|=2.34e+05 loss_x2y=4.3472e+00 ppl_x2y=77.26 loss_y2x=4.1372e+00 ppl_y2x=62.63 dual_loss=0.0000e+00
Validation X2Y - loss=3.8579e+00 ppl=47.37 best_loss=3.8660e+00 best_ppl=47.75
Validation Y2X - loss=3.7304e+00 ppl=41.69 best_loss=3.7358e+00 best_ppl=41.92
Epoch 5 - |param|=8.51e+02 |g_param|=2.23e+05 loss_x2y=4.3274e+00 ppl_x2y=75.75 loss_y2x=4.1374e+00 ppl_y2x=62.64 dual_loss=0.0000e+00
Validation X2Y - loss=3.8159e+00 ppl=45.42 best_loss=3.8579e+00 best_ppl=47.37
Validation Y2X - loss=3.7188e+00 ppl=41.21 best_loss=3.7304e+00 best_ppl=41.69
Epoch 6 - |param|=8.51e+02 |g_param|=2.62e+05 loss_x2y=4.2784e+00 ppl_x2y=72.13 loss_y2x=4.0812e+00 ppl_y2x=59.22 dual_loss=0.0000e+00
Validation X2Y - loss=3.8310e+00 ppl=46.11 best_loss=3.8159e+00 best_ppl=45.42
Validation Y2X - loss=3.7268e+00 ppl=41.55 best_loss=3.7188e+00 best_ppl=41.21
Epoch 7 - |param|=8.51e+02 |g_param|=2.21e+05 loss_x2y=4.3526e+00 ppl_x2y=77.68 loss_y2x=4.1557e+00 ppl_y2x=63.79 dual_loss=0.0000e+00
Validation X2Y - loss=3.7923e+00 ppl=44.36 best_loss=3.8159e+00 best_ppl=45.42
Validation Y2X - loss=3.6684e+00 ppl=39.19 best_loss=3.7188e+00 best_ppl=41.21
Epoch 8 - |param|=8.52e+02 |g_param|=2.37e+05 loss_x2y=4.2370e+00 ppl_x2y=69.20 loss_y2x=4.0163e+00 ppl_y2x=55.50 dual_loss=0.0000e+00
Validation X2Y - loss=3.7294e+00 ppl=41.65 best_loss=3.7923e+00 best_ppl=44.36
Validation Y2X - loss=3.6127e+00 ppl=37.07 best_loss=3.6684e+00 best_ppl=39.19
Epoch 9 - |param|=8.52e+02 |g_param|=2.30e+05 loss_x2y=4.2562e+00 ppl_x2y=70.54 loss_y2x=4.0305e+00 ppl_y2x=56.29 dual_loss=0.0000e+00
Validation X2Y - loss=3.6733e+00 ppl=39.38 best_loss=3.7294e+00 best_ppl=41.65
Validation Y2X - loss=3.6079e+00 ppl=36.89 best_loss=3.6127e+00 best_ppl=37.07
Epoch 10 - |param|=8.53e+02 |g_param|=1.88e+05 loss_x2y=3.9662e+00 ppl_x2y=52.79 loss_y2x=3.8498e+00 ppl_y2x=46.98 dual_loss=0.0000e+00
Validation X2Y - loss=3.4523e+00 ppl=31.57 best_loss=3.6733e+00 best_ppl=39.38
Validation Y2X - loss=3.5261e+00 ppl=33.99 best_loss=3.6079e+00 best_ppl=36.89
Epoch 11 - |param|=8.53e+02 |g_param|=1.64e+05 loss_x2y=3.9099e+00 ppl_x2y=49.89 loss_y2x=3.7911e+00 ppl_y2x=44.31 dual_loss=0.0000e+00
Validation X2Y - loss=3.4011e+00 ppl=30.00 best_loss=3.4523e+00 best_ppl=31.57
Validation Y2X - loss=3.3460e+00 ppl=28.39 best_loss=3.5261e+00 best_ppl=33.99
Epoch 12 - |param|=8.54e+02 |g_param|=1.60e+05 loss_x2y=3.8628e+00 ppl_x2y=47.60 loss_y2x=3.7156e+00 ppl_y2x=41.08 dual_loss=0.0000e+00
Validation X2Y - loss=3.3467e+00 ppl=28.41 best_loss=3.4011e+00 best_ppl=30.00
Validation Y2X - loss=3.2396e+00 ppl=25.52 best_loss=3.3460e+00 best_ppl=28.39
Epoch 13 - |param|=8.54e+02 |g_param|=1.66e+05 loss_x2y=3.7029e+00 ppl_x2y=40.57 loss_y2x=3.5031e+00 ppl_y2x=33.22 dual_loss=0.0000e+00
Validation X2Y - loss=3.2689e+00 ppl=26.28 best_loss=3.3467e+00 best_ppl=28.41
Validation Y2X - loss=3.2054e+00 ppl=24.66 best_loss=3.2396e+00 best_ppl=25.52
Epoch 14 - |param|=8.55e+02 |g_param|=1.49e+05 loss_x2y=3.7216e+00 ppl_x2y=41.33 loss_y2x=3.5388e+00 ppl_y2x=34.42 dual_loss=0.0000e+00
Validation X2Y - loss=3.2498e+00 ppl=25.79 best_loss=3.2689e+00 best_ppl=26.28
Validation Y2X - loss=3.0901e+00 ppl=21.98 best_loss=3.2054e+00 best_ppl=24.66
Epoch 15 - |param|=8.55e+02 |g_param|=1.60e+05 loss_x2y=3.6345e+00 ppl_x2y=37.88 loss_y2x=3.3800e+00 ppl_y2x=29.37 dual_loss=0.0000e+00
Validation X2Y - loss=3.2090e+00 ppl=24.75 best_loss=3.2498e+00 best_ppl=25.79
Validation Y2X - loss=3.0296e+00 ppl=20.69 best_loss=3.0901e+00 best_ppl=21.98
Epoch 16 - |param|=8.56e+02 |g_param|=1.71e+05 loss_x2y=3.5483e+00 ppl_x2y=34.75 loss_y2x=3.3106e+00 ppl_y2x=27.40 dual_loss=0.0000e+00
Validation X2Y - loss=3.1601e+00 ppl=23.57 best_loss=3.2090e+00 best_ppl=24.75
Validation Y2X - loss=2.9817e+00 ppl=19.72 best_loss=3.0296e+00 best_ppl=20.69
Epoch 17 - |param|=8.57e+02 |g_param|=1.44e+05 loss_x2y=3.4724e+00 ppl_x2y=32.21 loss_y2x=3.2317e+00 ppl_y2x=25.32 dual_loss=0.0000e+00
Validation X2Y - loss=3.1325e+00 ppl=22.93 best_loss=3.1601e+00 best_ppl=23.57
Validation Y2X - loss=2.9200e+00 ppl=18.54 best_loss=2.9817e+00 best_ppl=19.72
Epoch 18 - |param|=8.58e+02 |g_param|=1.62e+05 loss_x2y=3.4156e+00 ppl_x2y=30.43 loss_y2x=3.1496e+00 ppl_y2x=23.33 dual_loss=0.0000e+00
Validation X2Y - loss=3.0910e+00 ppl=22.00 best_loss=3.1325e+00 best_ppl=22.93
Validation Y2X - loss=2.9091e+00 ppl=18.34 best_loss=2.9200e+00 best_ppl=18.54
Epoch 19 - |param|=8.58e+02 |g_param|=1.61e+05 loss_x2y=3.4005e+00 ppl_x2y=29.98 loss_y2x=3.1434e+00 ppl_y2x=23.18 dual_loss=0.0000e+00
Validation X2Y - loss=3.0515e+00 ppl=21.15 best_loss=3.0910e+00 best_ppl=22.00
Validation Y2X - loss=2.8352e+00 ppl=17.03 best_loss=2.9091e+00 best_ppl=18.34
Epoch 20 - |param|=8.59e+02 |g_param|=1.68e+05 loss_x2y=3.3846e+00 ppl_x2y=29.51 loss_y2x=3.1448e+00 ppl_y2x=23.21 dual_loss=0.0000e+00
Validation X2Y - loss=3.0080e+00 ppl=20.25 best_loss=3.0515e+00 best_ppl=21.15
Validation Y2X - loss=2.7958e+00 ppl=16.38 best_loss=2.8352e+00 best_ppl=17.03
Epoch 21 - |param|=8.60e+02 |g_param|=1.61e+05 loss_x2y=3.3363e+00 ppl_x2y=28.11 loss_y2x=3.0677e+00 ppl_y2x=21.49 dual_loss=6.2826e-01
Validation X2Y - loss=2.9850e+00 ppl=19.79 best_loss=3.0080e+00 best_ppl=20.25
Validation Y2X - loss=2.7693e+00 ppl=15.95 best_loss=2.7958e+00 best_ppl=16.38
Epoch 22 - |param|=8.60e+02 |g_param|=1.73e+05 loss_x2y=3.3424e+00 ppl_x2y=28.29 loss_y2x=3.1027e+00 ppl_y2x=22.26 dual_loss=6.5609e-01
Validation X2Y - loss=2.9449e+00 ppl=19.01 best_loss=2.9850e+00 best_ppl=19.79
Validation Y2X - loss=2.7434e+00 ppl=15.54 best_loss=2.7693e+00 best_ppl=15.95
Epoch 23 - |param|=8.61e+02 |g_param|=1.63e+05 loss_x2y=3.2074e+00 ppl_x2y=24.71 loss_y2x=2.9724e+00 ppl_y2x=19.54 dual_loss=5.2734e-01
Validation X2Y - loss=2.9138e+00 ppl=18.43 best_loss=2.9449e+00 best_ppl=19.01
Validation Y2X - loss=2.6861e+00 ppl=14.67 best_loss=2.7434e+00 best_ppl=15.54
Epoch 24 - |param|=8.62e+02 |g_param|=1.93e+05 loss_x2y=3.1891e+00 ppl_x2y=24.27 loss_y2x=2.9504e+00 ppl_y2x=19.11 dual_loss=5.4548e-01
Validation X2Y - loss=2.9168e+00 ppl=18.48 best_loss=2.9138e+00 best_ppl=18.43
Validation Y2X - loss=2.6588e+00 ppl=14.28 best_loss=2.6861e+00 best_ppl=14.67
Epoch 25 - |param|=8.62e+02 |g_param|=1.78e+05 loss_x2y=3.1189e+00 ppl_x2y=22.62 loss_y2x=2.8703e+00 ppl_y2x=17.64 dual_loss=4.7485e-01
Validation X2Y - loss=2.8468e+00 ppl=17.23 best_loss=2.9138e+00 best_ppl=18.43
Validation Y2X - loss=2.6526e+00 ppl=14.19 best_loss=2.6588e+00 best_ppl=14.28
Epoch 26 - |param|=8.63e+02 |g_param|=1.92e+05 loss_x2y=3.1048e+00 ppl_x2y=22.30 loss_y2x=2.8397e+00 ppl_y2x=17.11 dual_loss=4.6875e-01
Validation X2Y - loss=2.7997e+00 ppl=16.44 best_loss=2.8468e+00 best_ppl=17.23
Validation Y2X - loss=2.5834e+00 ppl=13.24 best_loss=2.6526e+00 best_ppl=14.19
Epoch 27 - |param|=8.64e+02 |g_param|=1.82e+05 loss_x2y=3.1123e+00 ppl_x2y=22.47 loss_y2x=2.8746e+00 ppl_y2x=17.72 dual_loss=4.9844e-01
Validation X2Y - loss=2.8011e+00 ppl=16.46 best_loss=2.7997e+00 best_ppl=16.44
Validation Y2X - loss=2.6267e+00 ppl=13.83 best_loss=2.5834e+00 best_ppl=13.24
Epoch 28 - |param|=8.64e+02 |g_param|=1.90e+05 loss_x2y=3.0370e+00 ppl_x2y=20.84 loss_y2x=2.7849e+00 ppl_y2x=16.20 dual_loss=4.6385e-01
Validation X2Y - loss=2.8139e+00 ppl=16.68 best_loss=2.7997e+00 best_ppl=16.44
Validation Y2X - loss=2.5917e+00 ppl=13.35 best_loss=2.5834e+00 best_ppl=13.24
Epoch 29 - |param|=8.65e+02 |g_param|=1.88e+05 loss_x2y=3.0100e+00 ppl_x2y=20.29 loss_y2x=2.7822e+00 ppl_y2x=16.16 dual_loss=4.2174e-01
Validation X2Y - loss=2.7793e+00 ppl=16.11 best_loss=2.7997e+00 best_ppl=16.44
Validation Y2X - loss=2.5506e+00 ppl=12.81 best_loss=2.5834e+00 best_ppl=13.24
Epoch 30 - |param|=8.66e+02 |g_param|=2.23e+05 loss_x2y=2.9469e+00 ppl_x2y=19.05 loss_y2x=2.6825e+00 ppl_y2x=14.62 dual_loss=3.8517e-01
Validation X2Y - loss=2.7468e+00 ppl=15.59 best_loss=2.7793e+00 best_ppl=16.11
Validation Y2X - loss=2.5163e+00 ppl=12.38 best_loss=2.5506e+00 best_ppl=12.81
```

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/mybk-30epoch
Evaluation result for the model: dsl-model-mybk.01.4.87-130.06.4.73-113.59.4.01-55.29.3.95-51.90.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.7/0.1/0.0/0.0 (BP=0.903, ratio=0.907, hyp_len=10372, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.87-130.06.4.73-113.59.4.01-55.29.3.95-51.90.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 27.1/0.1/0.0/0.0 (BP=0.461, ratio=0.564, hyp_len=6895, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.02.4.46-86.54.4.22-68.20.3.89-48.99.3.81-45.34.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 14.9/0.0/0.0/0.0 (BP=1.000, ratio=1.029, hyp_len=11761, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.4.46-86.54.4.22-68.20.3.89-48.99.3.81-45.34.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.7/1.6/0.3/0.0 (BP=0.942, ratio=0.944, hyp_len=11540, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.4.46-86.19.4.19-66.23.3.87-47.75.3.74-41.92.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.4/0.1/0.0/0.0 (BP=0.981, ratio=0.981, hyp_len=11213, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.4.46-86.19.4.19-66.23.3.87-47.75.3.74-41.92.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.6/0.9/0.1/0.0 (BP=0.944, ratio=0.946, hyp_len=11569, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.4.35-77.26.4.14-62.63.3.86-47.37.3.73-41.69.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.9/0.3/0.0/0.0 (BP=1.000, ratio=1.023, hyp_len=11694, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.4.35-77.26.4.14-62.63.3.86-47.37.3.73-41.69.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.2/2.0/0.3/0.0 (BP=1.000, ratio=1.014, hyp_len=12407, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.4.33-75.75.4.14-62.64.3.82-45.42.3.72-41.21.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.8/0.2/0.0/0.0 (BP=1.000, ratio=1.049, hyp_len=11993, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.4.33-75.75.4.14-62.64.3.82-45.42.3.72-41.21.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.5/1.7/0.3/0.0 (BP=0.997, ratio=0.997, hyp_len=12198, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.4.28-72.13.4.08-59.22.3.83-46.11.3.73-41.55.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.9/0.3/0.0/0.0 (BP=1.000, ratio=1.057, hyp_len=12080, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.4.28-72.13.4.08-59.22.3.83-46.11.3.73-41.55.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.4/0.5/0.0/0.0 (BP=1.000, ratio=1.057, hyp_len=12933, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.4.35-77.68.4.16-63.79.3.79-44.36.3.67-39.19.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.0/0.1/0.0/0.0 (BP=1.000, ratio=1.085, hyp_len=12405, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.4.35-77.68.4.16-63.79.3.79-44.36.3.67-39.19.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.1/0.6/0.0/0.0 (BP=1.000, ratio=1.005, hyp_len=12288, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.4.24-69.20.4.02-55.50.3.73-41.65.3.61-37.07.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.7/0.3/0.0/0.0 (BP=1.000, ratio=1.034, hyp_len=11825, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.4.24-69.20.4.02-55.50.3.73-41.65.3.61-37.07.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.1/1.1/0.1/0.0 (BP=1.000, ratio=1.037, hyp_len=12687, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.4.26-70.54.4.03-56.29.3.67-39.38.3.61-36.89.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.7/0.4/0.0/0.0 (BP=0.813, ratio=0.828, hyp_len=9469, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.4.26-70.54.4.03-56.29.3.67-39.38.3.61-36.89.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.1/1.0/0.1/0.0 (BP=1.000, ratio=1.055, hyp_len=12905, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.3.97-52.79.3.85-46.98.3.45-31.57.3.53-33.99.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 25.5/1.2/0.0/0.0 (BP=0.706, ratio=0.741, hyp_len=8476, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.3.97-52.79.3.85-46.98.3.45-31.57.3.53-33.99.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 5.1/0.2/0.0/0.0 (BP=1.000, ratio=4.006, hyp_len=48992, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.3.91-49.89.3.79-44.31.3.40-30.00.3.35-28.39.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 24.4/2.3/0.1/0.0 (BP=0.912, ratio=0.916, hyp_len=10472, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.3.91-49.89.3.79-44.31.3.40-30.00.3.35-28.39.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.3/1.0/0.0/0.0 (BP=1.000, ratio=1.020, hyp_len=12480, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.3.86-47.60.3.72-41.08.3.35-28.41.3.24-25.52.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 23.5/2.5/0.1/0.0 (BP=0.952, ratio=0.953, hyp_len=10900, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.3.86-47.60.3.72-41.08.3.35-28.41.3.24-25.52.pth, bkmy
BLEU = 0.02, 0.4/0.1/0.0/0.0 (BP=1.000, ratio=21.705, hyp_len=265472, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.3.70-40.57.3.50-33.22.3.27-26.28.3.21-24.66.pth, mybk
BLEU = 2.22, 25.9/4.9/1.2/0.3 (BP=0.864, ratio=0.872, hyp_len=9974, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.3.70-40.57.3.50-33.22.3.27-26.28.3.21-24.66.pth, bkmy
BLEU = 0.11, 1.3/0.3/0.1/0.0 (BP=1.000, ratio=12.824, hyp_len=156847, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.3.72-41.33.3.54-34.42.3.25-25.79.3.09-21.98.pth, mybk
BLEU = 2.64, 20.1/4.4/1.2/0.5 (BP=1.000, ratio=1.159, hyp_len=13249, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.3.72-41.33.3.54-34.42.3.25-25.79.3.09-21.98.pth, bkmy
BLEU = 0.08, 1.5/0.3/0.0/0.0 (BP=1.000, ratio=11.812, hyp_len=144467, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.3.63-37.88.3.38-29.37.3.21-24.75.3.03-20.69.pth, mybk
BLEU = 3.56, 22.1/5.4/1.8/0.7 (BP=1.000, ratio=1.125, hyp_len=12859, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.3.63-37.88.3.38-29.37.3.21-24.75.3.03-20.69.pth, bkmy
BLEU = 0.37, 4.1/0.9/0.2/0.0 (BP=1.000, ratio=6.304, hyp_len=77102, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.3.55-34.75.3.31-27.40.3.16-23.57.2.98-19.72.pth, mybk
BLEU = 3.87, 23.7/5.8/2.0/0.8 (BP=1.000, ratio=1.089, hyp_len=12449, ref_len=11432)
^[Evaluation result for the model: dsl-model-mybk.16.3.55-34.75.3.31-27.40.3.16-23.57.2.98-19.72.pth, bkmy
BLEU = 0.52, 5.2/1.3/0.2/0.0 (BP=1.000, ratio=5.120, hyp_len=62625, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.3.47-32.21.3.23-25.32.3.13-22.93.2.92-18.54.pth, mybk
BLEU = 3.16, 19.7/5.0/1.7/0.6 (BP=1.000, ratio=1.321, hyp_len=15102, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.3.47-32.21.3.23-25.32.3.13-22.93.2.92-18.54.pth, bkmy
BLEU = 2.02, 22.5/5.6/0.9/0.1 (BP=1.000, ratio=1.235, hyp_len=15110, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.3.42-30.43.3.15-23.33.3.09-22.00.2.91-18.34.pth, mybk
BLEU = 2.96, 17.7/4.7/1.5/0.6 (BP=1.000, ratio=1.443, hyp_len=16495, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.3.42-30.43.3.15-23.33.3.09-22.00.2.91-18.34.pth, bkmy
BLEU = 3.65, 26.3/7.7/2.1/0.4 (BP=1.000, ratio=1.186, hyp_len=14510, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.3.40-29.98.3.14-23.18.3.05-21.15.2.84-17.03.pth, mybk
BLEU = 1.68, 10.0/2.7/0.9/0.3 (BP=1.000, ratio=2.692, hyp_len=30773, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.3.40-29.98.3.14-23.18.3.05-21.15.2.84-17.03.pth, bkmy
BLEU = 4.26, 27.5/8.9/2.4/0.6 (BP=1.000, ratio=1.199, hyp_len=14670, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.3.38-29.51.3.14-23.21.3.01-20.25.2.80-16.38.pth, mybk
BLEU = 2.86, 16.2/4.5/1.5/0.6 (BP=1.000, ratio=1.707, hyp_len=19513, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.3.38-29.51.3.14-23.21.3.01-20.25.2.80-16.38.pth, bkmy
BLEU = 3.36, 20.9/7.1/2.1/0.4 (BP=1.000, ratio=1.605, hyp_len=19632, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.3.34-28.11.3.07-21.49.2.99-19.79.2.77-15.95.pth, mybk
BLEU = 2.41, 14.4/4.0/1.3/0.5 (BP=1.000, ratio=1.987, hyp_len=22712, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.3.34-28.11.3.07-21.49.2.99-19.79.2.77-15.95.pth, bkmy
BLEU = 2.30, 12.3/4.3/1.3/0.4 (BP=1.000, ratio=2.729, hyp_len=33380, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.3.34-28.29.3.10-22.26.2.94-19.01.2.74-15.54.pth, mybk
BLEU = 3.05, 16.6/4.7/1.7/0.6 (BP=1.000, ratio=1.688, hyp_len=19298, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.3.34-28.29.3.10-22.26.2.94-19.01.2.74-15.54.pth, bkmy
BLEU = 1.22, 6.3/2.2/0.7/0.2 (BP=1.000, ratio=5.210, hyp_len=63721, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.3.21-24.71.2.97-19.54.2.91-18.43.2.69-14.67.pth, mybk
BLEU = 1.23, 7.0/2.0/0.7/0.2 (BP=1.000, ratio=3.976, hyp_len=45451, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.3.21-24.71.2.97-19.54.2.91-18.43.2.69-14.67.pth, bkmy
BLEU = 3.10, 17.2/5.9/1.8/0.5 (BP=1.000, ratio=1.977, hyp_len=24177, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.3.19-24.27.2.95-19.11.2.92-18.48.2.66-14.28.pth, mybk
BLEU = 3.78, 19.3/5.8/2.2/0.8 (BP=1.000, ratio=1.560, hyp_len=17829, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.3.19-24.27.2.95-19.11.2.92-18.48.2.66-14.28.pth, bkmy
BLEU = 6.15, 31.1/11.3/3.7/1.1 (BP=1.000, ratio=1.106, hyp_len=13530, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.3.12-22.62.2.87-17.64.2.85-17.23.2.65-14.19.pth, mybk
BLEU = 3.62, 18.5/5.9/2.1/0.7 (BP=1.000, ratio=1.665, hyp_len=19034, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.3.12-22.62.2.87-17.64.2.85-17.23.2.65-14.19.pth, bkmy
BLEU = 4.54, 23.0/8.0/2.7/0.9 (BP=1.000, ratio=1.528, hyp_len=18689, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.3.10-22.30.2.84-17.11.2.80-16.44.2.58-13.24.pth, mybk
BLEU = 5.03, 23.8/7.8/3.0/1.2 (BP=1.000, ratio=1.300, hyp_len=14864, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.3.10-22.30.2.84-17.11.2.80-16.44.2.58-13.24.pth, bkmy
BLEU = 3.87, 18.5/6.7/2.3/0.8 (BP=1.000, ratio=1.910, hyp_len=23366, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.3.11-22.47.2.87-17.72.2.80-16.46.2.63-13.83.pth, mybk
BLEU = 4.79, 23.6/7.5/2.8/1.0 (BP=1.000, ratio=1.317, hyp_len=15061, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.3.11-22.47.2.87-17.72.2.80-16.46.2.63-13.83.pth, bkmy
BLEU = 2.49, 11.2/4.2/1.5/0.5 (BP=1.000, ratio=3.084, hyp_len=37716, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.3.04-20.84.2.78-16.20.2.81-16.68.2.59-13.35.pth, mybk
BLEU = 4.00, 20.1/6.4/2.3/0.9 (BP=1.000, ratio=1.598, hyp_len=18263, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.3.04-20.84.2.78-16.20.2.81-16.68.2.59-13.35.pth, bkmy
BLEU = 5.45, 24.9/9.1/3.2/1.2 (BP=1.000, ratio=1.408, hyp_len=17224, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.3.01-20.29.2.78-16.16.2.78-16.11.2.55-12.81.pth, mybk
BLEU = 3.89, 18.9/6.1/2.3/0.9 (BP=1.000, ratio=1.687, hyp_len=19291, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.3.01-20.29.2.78-16.16.2.78-16.11.2.55-12.81.pth, bkmy
BLEU = 5.87, 26.6/9.8/3.5/1.3 (BP=1.000, ratio=1.346, hyp_len=16462, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.2.95-19.05.2.68-14.62.2.75-15.59.2.52-12.38.pth, mybk
BLEU = 4.77, 22.7/7.6/2.8/1.1 (BP=1.000, ratio=1.416, hyp_len=16187, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.2.95-19.05.2.68-14.62.2.75-15.59.2.52-12.38.pth, bkmy
BLEU = 6.88, 28.2/10.8/4.3/1.7 (BP=1.000, ratio=1.298, hyp_len=15875, ref_len=12231)
```

Best BLEU Score for my-bk, 27epoch: 4.79  
Best BLEU Score for bk-my, 30 epoch:  6.88  

## Seq2Seq-DSL, my-bk, 40epoch

training

```
Epoch 1 - |param|=8.48e+02 |g_param|=4.24e+05 loss_x2y=4.8691e+00 ppl_x2y=130.21 loss_y2x=4.6748e+00 ppl_y2x=107.21 dual_loss=0.0000e+00
Validation X2Y - loss=4.0146e+00 ppl=55.40 best_loss=inf best_ppl=inf
Validation Y2X - loss=3.8795e+00 ppl=48.40 best_loss=inf best_ppl=inf
Epoch 2 - |param|=8.48e+02 |g_param|=4.13e+05 loss_x2y=4.4353e+00 ppl_x2y=84.37 loss_y2x=4.2123e+00 ppl_y2x=67.51 dual_loss=0.0000e+00
Validation X2Y - loss=3.9422e+00 ppl=51.53 best_loss=4.0146e+00 best_ppl=55.40
Validation Y2X - loss=3.7503e+00 ppl=42.53 best_loss=3.8795e+00 best_ppl=48.40
Epoch 3 - |param|=8.48e+02 |g_param|=2.74e+05 loss_x2y=4.3700e+00 ppl_x2y=79.04 loss_y2x=4.1409e+00 ppl_y2x=62.86 dual_loss=0.0000e+00
Validation X2Y - loss=3.8416e+00 ppl=46.60 best_loss=3.9422e+00 best_ppl=51.53
Validation Y2X - loss=3.7589e+00 ppl=42.90 best_loss=3.7503e+00 best_ppl=42.53
Epoch 4 - |param|=8.48e+02 |g_param|=2.33e+05 loss_x2y=4.4245e+00 ppl_x2y=83.47 loss_y2x=4.2340e+00 ppl_y2x=68.99 dual_loss=0.0000e+00
Validation X2Y - loss=3.8321e+00 ppl=46.16 best_loss=3.8416e+00 best_ppl=46.60
Validation Y2X - loss=3.7342e+00 ppl=41.85 best_loss=3.7503e+00 best_ppl=42.53
Epoch 5 - |param|=8.48e+02 |g_param|=2.17e+05 loss_x2y=4.3970e+00 ppl_x2y=81.21 loss_y2x=4.1706e+00 ppl_y2x=64.75 dual_loss=0.0000e+00
Validation X2Y - loss=3.8104e+00 ppl=45.17 best_loss=3.8321e+00 best_ppl=46.16
Validation Y2X - loss=3.7404e+00 ppl=42.12 best_loss=3.7342e+00 best_ppl=41.85
Epoch 6 - |param|=8.48e+02 |g_param|=2.34e+05 loss_x2y=4.3171e+00 ppl_x2y=74.97 loss_y2x=4.0970e+00 ppl_y2x=60.16 dual_loss=0.0000e+00
Validation X2Y - loss=3.7827e+00 ppl=43.94 best_loss=3.8104e+00 best_ppl=45.17
Validation Y2X - loss=3.7508e+00 ppl=42.56 best_loss=3.7342e+00 best_ppl=41.85
Epoch 7 - |param|=8.49e+02 |g_param|=2.25e+05 loss_x2y=4.2873e+00 ppl_x2y=72.77 loss_y2x=4.0901e+00 ppl_y2x=59.75 dual_loss=0.0000e+00
Validation X2Y - loss=3.7597e+00 ppl=42.94 best_loss=3.7827e+00 best_ppl=43.94
Validation Y2X - loss=3.7236e+00 ppl=41.41 best_loss=3.7342e+00 best_ppl=41.85
Epoch 8 - |param|=8.49e+02 |g_param|=2.25e+05 loss_x2y=4.3164e+00 ppl_x2y=74.92 loss_y2x=4.1451e+00 ppl_y2x=63.12 dual_loss=0.0000e+00
Validation X2Y - loss=3.7128e+00 ppl=40.97 best_loss=3.7597e+00 best_ppl=42.94
Validation Y2X - loss=3.6304e+00 ppl=37.73 best_loss=3.7236e+00 best_ppl=41.41
Epoch 9 - |param|=8.50e+02 |g_param|=2.22e+05 loss_x2y=4.1761e+00 ppl_x2y=65.11 loss_y2x=4.0229e+00 ppl_y2x=55.86 dual_loss=0.0000e+00
Validation X2Y - loss=3.7168e+00 ppl=41.13 best_loss=3.7128e+00 best_ppl=40.97
Validation Y2X - loss=3.6366e+00 ppl=37.96 best_loss=3.6304e+00 best_ppl=37.73
Epoch 10 - |param|=8.50e+02 |g_param|=2.31e+05 loss_x2y=4.1990e+00 ppl_x2y=66.62 loss_y2x=4.0993e+00 ppl_y2x=60.30 dual_loss=0.0000e+00
Validation X2Y - loss=3.5427e+00 ppl=34.56 best_loss=3.7128e+00 best_ppl=40.97
Validation Y2X - loss=3.5500e+00 ppl=34.81 best_loss=3.6304e+00 best_ppl=37.73
Epoch 11 - |param|=8.51e+02 |g_param|=1.63e+05 loss_x2y=3.8570e+00 ppl_x2y=47.33 loss_y2x=3.7870e+00 ppl_y2x=44.12 dual_loss=0.0000e+00
Validation X2Y - loss=3.3945e+00 ppl=29.80 best_loss=3.5427e+00 best_ppl=34.56
Validation Y2X - loss=3.4014e+00 ppl=30.00 best_loss=3.5500e+00 best_ppl=34.81
Epoch 12 - |param|=8.51e+02 |g_param|=1.71e+05 loss_x2y=3.7732e+00 ppl_x2y=43.52 loss_y2x=3.6687e+00 ppl_y2x=39.20 dual_loss=0.0000e+00
Validation X2Y - loss=3.3254e+00 ppl=27.81 best_loss=3.3945e+00 best_ppl=29.80
Validation Y2X - loss=3.2848e+00 ppl=26.70 best_loss=3.4014e+00 best_ppl=30.00
Epoch 13 - |param|=8.52e+02 |g_param|=1.59e+05 loss_x2y=3.7701e+00 ppl_x2y=43.38 loss_y2x=3.5918e+00 ppl_y2x=36.30 dual_loss=0.0000e+00
Validation X2Y - loss=3.2724e+00 ppl=26.37 best_loss=3.3254e+00 best_ppl=27.81
Validation Y2X - loss=3.1577e+00 ppl=23.52 best_loss=3.2848e+00 best_ppl=26.70
Epoch 14 - |param|=8.52e+02 |g_param|=1.70e+05 loss_x2y=3.6155e+00 ppl_x2y=37.17 loss_y2x=3.4360e+00 ppl_y2x=31.06 dual_loss=0.0000e+00
Validation X2Y - loss=3.2067e+00 ppl=24.70 best_loss=3.2724e+00 best_ppl=26.37
Validation Y2X - loss=3.1357e+00 ppl=23.00 best_loss=3.1577e+00 best_ppl=23.52
Epoch 15 - |param|=8.53e+02 |g_param|=1.55e+05 loss_x2y=3.6247e+00 ppl_x2y=37.51 loss_y2x=3.4565e+00 ppl_y2x=31.71 dual_loss=0.0000e+00
Validation X2Y - loss=3.1783e+00 ppl=24.01 best_loss=3.2067e+00 best_ppl=24.70
Validation Y2X - loss=3.0529e+00 ppl=21.18 best_loss=3.1357e+00 best_ppl=23.00
Epoch 16 - |param|=8.54e+02 |g_param|=1.62e+05 loss_x2y=3.4948e+00 ppl_x2y=32.94 loss_y2x=3.3075e+00 ppl_y2x=27.32 dual_loss=0.0000e+00
Validation X2Y - loss=3.1215e+00 ppl=22.68 best_loss=3.1783e+00 best_ppl=24.01
Validation Y2X - loss=3.0029e+00 ppl=20.14 best_loss=3.0529e+00 best_ppl=21.18
Epoch 17 - |param|=8.54e+02 |g_param|=1.54e+05 loss_x2y=3.4321e+00 ppl_x2y=30.94 loss_y2x=3.2815e+00 ppl_y2x=26.62 dual_loss=0.0000e+00
Validation X2Y - loss=3.1080e+00 ppl=22.38 best_loss=3.1215e+00 best_ppl=22.68
Validation Y2X - loss=2.9663e+00 ppl=19.42 best_loss=3.0029e+00 best_ppl=20.14
Epoch 18 - |param|=8.55e+02 |g_param|=1.58e+05 loss_x2y=3.4085e+00 ppl_x2y=30.22 loss_y2x=3.2427e+00 ppl_y2x=25.60 dual_loss=0.0000e+00
Validation X2Y - loss=3.0603e+00 ppl=21.33 best_loss=3.1080e+00 best_ppl=22.38
Validation Y2X - loss=2.9364e+00 ppl=18.85 best_loss=2.9663e+00 best_ppl=19.42
Epoch 19 - |param|=8.56e+02 |g_param|=1.65e+05 loss_x2y=3.3849e+00 ppl_x2y=29.52 loss_y2x=3.2463e+00 ppl_y2x=25.69 dual_loss=0.0000e+00
Validation X2Y - loss=2.9822e+00 ppl=19.73 best_loss=3.0603e+00 best_ppl=21.33
Validation Y2X - loss=2.8669e+00 ppl=17.58 best_loss=2.9364e+00 best_ppl=18.85
Epoch 20 - |param|=8.57e+02 |g_param|=1.67e+05 loss_x2y=3.2381e+00 ppl_x2y=25.49 loss_y2x=3.0609e+00 ppl_y2x=21.35 dual_loss=0.0000e+00
Validation X2Y - loss=2.9734e+00 ppl=19.56 best_loss=2.9822e+00 best_ppl=19.73
Validation Y2X - loss=2.8346e+00 ppl=17.02 best_loss=2.8669e+00 best_ppl=17.58
Epoch 21 - |param|=8.57e+02 |g_param|=1.61e+05 loss_x2y=3.2662e+00 ppl_x2y=26.21 loss_y2x=3.1234e+00 ppl_y2x=22.72 dual_loss=7.8499e-01
Validation X2Y - loss=2.9020e+00 ppl=18.21 best_loss=2.9734e+00 best_ppl=19.56
Validation Y2X - loss=2.8261e+00 ppl=16.88 best_loss=2.8346e+00 best_ppl=17.02
Epoch 22 - |param|=8.58e+02 |g_param|=1.69e+05 loss_x2y=3.1761e+00 ppl_x2y=23.95 loss_y2x=3.0240e+00 ppl_y2x=20.57 dual_loss=6.1602e-01
Validation X2Y - loss=2.8650e+00 ppl=17.55 best_loss=2.9020e+00 best_ppl=18.21
Validation Y2X - loss=2.7446e+00 ppl=15.56 best_loss=2.8261e+00 best_ppl=16.88
Epoch 23 - |param|=8.59e+02 |g_param|=1.59e+05 loss_x2y=3.1298e+00 ppl_x2y=22.87 loss_y2x=2.9876e+00 ppl_y2x=19.84 dual_loss=6.3727e-01
Validation X2Y - loss=2.8256e+00 ppl=16.87 best_loss=2.8650e+00 best_ppl=17.55
Validation Y2X - loss=2.7367e+00 ppl=15.44 best_loss=2.7446e+00 best_ppl=15.56
Epoch 24 - |param|=8.59e+02 |g_param|=1.78e+05 loss_x2y=3.1539e+00 ppl_x2y=23.43 loss_y2x=2.9733e+00 ppl_y2x=19.56 dual_loss=5.8686e-01
Validation X2Y - loss=2.8080e+00 ppl=16.58 best_loss=2.8256e+00 best_ppl=16.87
Validation Y2X - loss=2.7141e+00 ppl=15.09 best_loss=2.7367e+00 best_ppl=15.44
Epoch 25 - |param|=8.60e+02 |g_param|=1.69e+05 loss_x2y=3.0762e+00 ppl_x2y=21.68 loss_y2x=2.9484e+00 ppl_y2x=19.08 dual_loss=6.0911e-01
Validation X2Y - loss=2.7768e+00 ppl=16.07 best_loss=2.8080e+00 best_ppl=16.58
Validation Y2X - loss=2.6786e+00 ppl=14.56 best_loss=2.7141e+00 best_ppl=15.09
Epoch 26 - |param|=8.61e+02 |g_param|=1.89e+05 loss_x2y=3.0360e+00 ppl_x2y=20.82 loss_y2x=2.8529e+00 ppl_y2x=17.34 dual_loss=5.0492e-01
Validation X2Y - loss=2.7583e+00 ppl=15.77 best_loss=2.7768e+00 best_ppl=16.07
Validation Y2X - loss=2.6593e+00 ppl=14.29 best_loss=2.6786e+00 best_ppl=14.56
Epoch 27 - |param|=8.62e+02 |g_param|=1.74e+05 loss_x2y=2.9628e+00 ppl_x2y=19.35 loss_y2x=2.8274e+00 ppl_y2x=16.90 dual_loss=5.0139e-01
Validation X2Y - loss=2.7450e+00 ppl=15.56 best_loss=2.7583e+00 best_ppl=15.77
Validation Y2X - loss=2.6296e+00 ppl=13.87 best_loss=2.6593e+00 best_ppl=14.29
Epoch 28 - |param|=8.62e+02 |g_param|=1.83e+05 loss_x2y=2.9205e+00 ppl_x2y=18.55 loss_y2x=2.7819e+00 ppl_y2x=16.15 dual_loss=4.9286e-01
Validation X2Y - loss=2.7126e+00 ppl=15.07 best_loss=2.7450e+00 best_ppl=15.56
Validation Y2X - loss=2.5606e+00 ppl=12.94 best_loss=2.6296e+00 best_ppl=13.87
Epoch 29 - |param|=8.63e+02 |g_param|=1.77e+05 loss_x2y=2.8864e+00 ppl_x2y=17.93 loss_y2x=2.7427e+00 ppl_y2x=15.53 dual_loss=4.8427e-01
Validation X2Y - loss=2.6826e+00 ppl=14.62 best_loss=2.7126e+00 best_ppl=15.07
Validation Y2X - loss=2.5650e+00 ppl=13.00 best_loss=2.5606e+00 best_ppl=12.94
Epoch 30 - |param|=8.64e+02 |g_param|=1.84e+05 loss_x2y=2.8781e+00 ppl_x2y=17.78 loss_y2x=2.7279e+00 ppl_y2x=15.30 dual_loss=4.6755e-01
Validation X2Y - loss=2.6783e+00 ppl=14.56 best_loss=2.6826e+00 best_ppl=14.62
Validation Y2X - loss=2.5292e+00 ppl=12.54 best_loss=2.5606e+00 best_ppl=12.94
Epoch 31 - |param|=8.64e+02 |g_param|=1.95e+05 loss_x2y=2.8501e+00 ppl_x2y=17.29 loss_y2x=2.7062e+00 ppl_y2x=14.97 dual_loss=4.9932e-01
Validation X2Y - loss=2.6800e+00 ppl=14.59 best_loss=2.6783e+00 best_ppl=14.56
Validation Y2X - loss=2.5486e+00 ppl=12.79 best_loss=2.5292e+00 best_ppl=12.54
Epoch 32 - |param|=8.65e+02 |g_param|=1.95e+05 loss_x2y=2.8435e+00 ppl_x2y=17.18 loss_y2x=2.6623e+00 ppl_y2x=14.33 dual_loss=4.5043e-01
Validation X2Y - loss=2.6391e+00 ppl=14.00 best_loss=2.6783e+00 best_ppl=14.56
Validation Y2X - loss=2.5188e+00 ppl=12.41 best_loss=2.5292e+00 best_ppl=12.54
Epoch 33 - |param|=8.66e+02 |g_param|=2.03e+05 loss_x2y=2.8773e+00 ppl_x2y=17.77 loss_y2x=2.7546e+00 ppl_y2x=15.71 dual_loss=6.5206e-01
Validation X2Y - loss=2.6371e+00 ppl=13.97 best_loss=2.6391e+00 best_ppl=14.00
Validation Y2X - loss=2.5285e+00 ppl=12.54 best_loss=2.5188e+00 best_ppl=12.41
Epoch 34 - |param|=8.66e+02 |g_param|=2.09e+05 loss_x2y=2.6693e+00 ppl_x2y=14.43 loss_y2x=2.5435e+00 ppl_y2x=12.72 dual_loss=4.1104e-01
Validation X2Y - loss=2.6398e+00 ppl=14.01 best_loss=2.6371e+00 best_ppl=13.97
Validation Y2X - loss=2.4553e+00 ppl=11.65 best_loss=2.5188e+00 best_ppl=12.41
Epoch 35 - |param|=8.67e+02 |g_param|=2.50e+05 loss_x2y=2.6416e+00 ppl_x2y=14.04 loss_y2x=2.5045e+00 ppl_y2x=12.24 dual_loss=3.8489e-01
Validation X2Y - loss=2.6239e+00 ppl=13.79 best_loss=2.6371e+00 best_ppl=13.97
Validation Y2X - loss=2.4620e+00 ppl=11.73 best_loss=2.4553e+00 best_ppl=11.65
Epoch 36 - |param|=8.68e+02 |g_param|=3.86e+05 loss_x2y=2.6319e+00 ppl_x2y=13.90 loss_y2x=2.4882e+00 ppl_y2x=12.04 dual_loss=3.9258e-01
Validation X2Y - loss=2.6367e+00 ppl=13.97 best_loss=2.6239e+00 best_ppl=13.79
Validation Y2X - loss=2.4476e+00 ppl=11.56 best_loss=2.4553e+00 best_ppl=11.65
Epoch 37 - |param|=8.68e+02 |g_param|=4.06e+05 loss_x2y=2.5477e+00 ppl_x2y=12.78 loss_y2x=2.4081e+00 ppl_y2x=11.11 dual_loss=3.5747e-01
Validation X2Y - loss=2.6115e+00 ppl=13.62 best_loss=2.6239e+00 best_ppl=13.79
Validation Y2X - loss=2.4143e+00 ppl=11.18 best_loss=2.4476e+00 best_ppl=11.56
Epoch 38 - |param|=8.69e+02 |g_param|=4.10e+05 loss_x2y=2.5711e+00 ppl_x2y=13.08 loss_y2x=2.4089e+00 ppl_y2x=11.12 dual_loss=3.5059e-01
Validation X2Y - loss=2.6060e+00 ppl=13.55 best_loss=2.6115e+00 best_ppl=13.62
Validation Y2X - loss=2.3816e+00 ppl=10.82 best_loss=2.4143e+00 best_ppl=11.18
Epoch 39 - |param|=8.70e+02 |g_param|=4.08e+05 loss_x2y=2.6139e+00 ppl_x2y=13.65 loss_y2x=2.4859e+00 ppl_y2x=12.01 dual_loss=4.0202e-01
Validation X2Y - loss=2.6315e+00 ppl=13.89 best_loss=2.6060e+00 best_ppl=13.55
Validation Y2X - loss=2.4249e+00 ppl=11.30 best_loss=2.3816e+00 best_ppl=10.82
Epoch 40 - |param|=8.70e+02 |g_param|=4.37e+05 loss_x2y=2.5989e+00 ppl_x2y=13.45 loss_y2x=2.3925e+00 ppl_y2x=10.94 dual_loss=3.5276e-01
Validation X2Y - loss=2.6204e+00 ppl=13.74 best_loss=2.6060e+00 best_ppl=13.55
Validation Y2X - loss=2.3744e+00 ppl=10.74 best_loss=2.3816e+00 best_ppl=10.82
```

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/mybk-40epoch
Evaluation result for the model: dsl-model-mybk.01.4.87-130.21.4.67-107.21.4.01-55.40.3.88-48.40.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.5/0.0/0.0/0.0 (BP=0.635, ratio=0.688, hyp_len=7866, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.87-130.21.4.67-107.21.4.01-55.40.3.88-48.40.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.1/0.1/0.0/0.0 (BP=0.894, ratio=0.899, hyp_len=10995, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.02.4.44-84.37.4.21-67.51.3.94-51.53.3.75-42.53.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.4/0.0/0.0/0.0 (BP=0.993, ratio=0.993, hyp_len=11352, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.4.44-84.37.4.21-67.51.3.94-51.53.3.75-42.53.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.5/0.7/0.0/0.0 (BP=0.971, ratio=0.971, hyp_len=11876, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.4.37-79.04.4.14-62.86.3.84-46.60.3.76-42.90.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.3/0.4/0.0/0.0 (BP=1.000, ratio=1.000, hyp_len=11429, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.4.37-79.04.4.14-62.86.3.84-46.60.3.76-42.90.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.2/0.5/0.0/0.0 (BP=1.000, ratio=1.007, hyp_len=12316, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.4.42-83.47.4.23-68.99.3.83-46.16.3.73-41.85.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.3/0.8/0.0/0.0 (BP=1.000, ratio=1.050, hyp_len=12000, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.4.42-83.47.4.23-68.99.3.83-46.16.3.73-41.85.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.1/0.4/0.0/0.0 (BP=0.966, ratio=0.966, hyp_len=11820, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.4.40-81.21.4.17-64.75.3.81-45.17.3.74-42.12.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.7/0.3/0.0/0.0 (BP=1.000, ratio=1.031, hyp_len=11782, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.4.40-81.21.4.17-64.75.3.81-45.17.3.74-42.12.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.3/0.5/0.0/0.0 (BP=0.998, ratio=0.998, hyp_len=12211, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.4.32-74.97.4.10-60.16.3.78-43.94.3.75-42.56.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.5/0.3/0.0/0.0 (BP=1.000, ratio=1.048, hyp_len=11982, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.4.32-74.97.4.10-60.16.3.78-43.94.3.75-42.56.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.1/0.5/0.0/0.0 (BP=1.000, ratio=1.002, hyp_len=12259, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.4.29-72.77.4.09-59.75.3.76-42.94.3.72-41.41.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.3/0.2/0.0/0.0 (BP=1.000, ratio=1.040, hyp_len=11891, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.4.29-72.77.4.09-59.75.3.76-42.94.3.72-41.41.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.5/0.6/0.0/0.0 (BP=0.996, ratio=0.996, hyp_len=12187, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.4.32-74.92.4.15-63.12.3.71-40.97.3.63-37.73.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.3/0.2/0.0/0.0 (BP=1.000, ratio=1.099, hyp_len=12562, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.4.32-74.92.4.15-63.12.3.71-40.97.3.63-37.73.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.7/0.8/0.0/0.0 (BP=1.000, ratio=1.045, hyp_len=12776, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.4.18-65.11.4.02-55.86.3.72-41.13.3.64-37.96.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.8/0.6/0.0/0.0 (BP=1.000, ratio=1.121, hyp_len=12819, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.4.18-65.11.4.02-55.86.3.72-41.13.3.64-37.96.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.6/1.7/0.2/0.0 (BP=1.000, ratio=1.066, hyp_len=13043, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.4.20-66.62.4.10-60.30.3.54-34.56.3.55-34.81.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 25.6/2.0/0.5/0.0 (BP=0.725, ratio=0.757, hyp_len=8654, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.4.20-66.62.4.10-60.30.3.54-34.56.3.55-34.81.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.3/1.9/0.2/0.0 (BP=1.000, ratio=1.022, hyp_len=12496, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.3.86-47.33.3.79-44.12.3.39-29.80.3.40-30.00.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 23.2/2.9/0.4/0.0 (BP=0.927, ratio=0.929, hyp_len=10624, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.3.86-47.33.3.79-44.12.3.39-29.80.3.40-30.00.pth, bkmy
BLEU = 1.10, 25.8/3.4/0.4/0.0 (BP=0.961, ratio=0.962, hyp_len=11765, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.3.77-43.52.3.67-39.20.3.33-27.81.3.28-26.70.pth, mybk
BLEU = 0.90, 19.9/3.2/0.5/0.0 (BP=1.000, ratio=1.064, hyp_len=12164, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.3.77-43.52.3.67-39.20.3.33-27.81.3.28-26.70.pth, bkmy
BLEU = 1.40, 27.3/5.2/0.9/0.0 (BP=0.964, ratio=0.965, hyp_len=11802, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.3.77-43.38.3.59-36.30.3.27-26.37.3.16-23.52.pth, mybk
BLEU = 1.44, 19.2/3.1/0.7/0.1 (BP=1.000, ratio=1.199, hyp_len=13708, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.3.77-43.38.3.59-36.30.3.27-26.37.3.16-23.52.pth, bkmy
BLEU = 2.00, 28.0/6.5/0.9/0.1 (BP=1.000, ratio=1.043, hyp_len=12755, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.3.62-37.17.3.44-31.06.3.21-24.70.3.14-23.00.pth, mybk
BLEU = 0.56, 5.7/1.0/0.3/0.1 (BP=1.000, ratio=3.915, hyp_len=44758, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.3.62-37.17.3.44-31.06.3.21-24.70.3.14-23.00.pth, bkmy
BLEU = 0.08, 1.0/0.2/0.0/0.0 (BP=1.000, ratio=18.540, hyp_len=226759, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.3.62-37.51.3.46-31.71.3.18-24.01.3.05-21.18.pth, mybk
BLEU = 3.09, 24.5/5.5/1.5/0.5 (BP=0.990, ratio=0.990, hyp_len=11317, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.3.62-37.51.3.46-31.71.3.18-24.01.3.05-21.18.pth, bkmy
BLEU = 0.22, 1.7/0.5/0.1/0.0 (BP=1.000, ratio=12.839, hyp_len=157038, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.3.49-32.94.3.31-27.32.3.12-22.68.3.00-20.14.pth, mybk
BLEU = 3.81, 25.9/6.8/2.0/0.6 (BP=1.000, ratio=1.008, hyp_len=11524, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.3.49-32.94.3.31-27.32.3.12-22.68.3.00-20.14.pth, bkmy
BLEU = 3.38, 25.5/7.1/2.1/0.3 (BP=1.000, ratio=1.175, hyp_len=14369, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.3.43-30.94.3.28-26.62.3.11-22.38.2.97-19.42.pth, mybk
BLEU = 4.68, 26.8/8.0/2.5/0.9 (BP=1.000, ratio=1.027, hyp_len=11738, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.3.43-30.94.3.28-26.62.3.11-22.38.2.97-19.42.pth, bkmy
BLEU = 0.95, 8.6/2.4/0.5/0.1 (BP=1.000, ratio=3.454, hyp_len=42243, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.3.41-30.22.3.24-25.60.3.06-21.33.2.94-18.85.pth, mybk
BLEU = 4.63, 25.9/7.5/2.4/1.0 (BP=1.000, ratio=1.079, hyp_len=12332, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.3.41-30.22.3.24-25.60.3.06-21.33.2.94-18.85.pth, bkmy
BLEU = 0.36, 2.6/0.8/0.2/0.0 (BP=1.000, ratio=10.257, hyp_len=125448, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.3.38-29.52.3.25-25.69.2.98-19.73.2.87-17.58.pth, mybk
BLEU = 5.31, 27.0/8.2/2.9/1.2 (BP=1.000, ratio=1.043, hyp_len=11927, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.3.38-29.52.3.25-25.69.2.98-19.73.2.87-17.58.pth, bkmy
BLEU = 3.94, 20.4/6.9/2.4/0.7 (BP=1.000, ratio=1.674, hyp_len=20479, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.3.24-25.49.3.06-21.35.2.97-19.56.2.83-17.02.pth, mybk
BLEU = 1.35, 7.5/2.1/0.7/0.3 (BP=1.000, ratio=3.542, hyp_len=40490, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.3.24-25.49.3.06-21.35.2.97-19.56.2.83-17.02.pth, bkmy
BLEU = 2.87, 14.9/4.9/1.7/0.5 (BP=1.000, ratio=2.235, hyp_len=27334, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.3.27-26.21.3.12-22.72.2.90-18.21.2.83-16.88.pth, mybk
BLEU = 3.48, 17.7/5.3/1.9/0.8 (BP=1.000, ratio=1.631, hyp_len=18647, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.3.27-26.21.3.12-22.72.2.90-18.21.2.83-16.88.pth, bkmy
BLEU = 2.50, 12.0/4.3/1.5/0.5 (BP=1.000, ratio=2.847, hyp_len=34825, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.3.18-23.95.3.02-20.57.2.86-17.55.2.74-15.56.pth, mybk
BLEU = 2.61, 13.2/4.0/1.5/0.6 (BP=1.000, ratio=2.211, hyp_len=25272, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.3.18-23.95.3.02-20.57.2.86-17.55.2.74-15.56.pth, bkmy
BLEU = 6.82, 28.8/11.2/4.3/1.6 (BP=1.000, ratio=1.219, hyp_len=14914, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.3.13-22.87.2.99-19.84.2.83-16.87.2.74-15.44.pth, mybk
BLEU = 3.75, 19.6/5.9/2.1/0.8 (BP=1.000, ratio=1.479, hyp_len=16913, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.3.13-22.87.2.99-19.84.2.83-16.87.2.74-15.44.pth, bkmy
BLEU = 5.93, 25.9/9.8/3.7/1.3 (BP=1.000, ratio=1.403, hyp_len=17162, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.3.15-23.43.2.97-19.56.2.81-16.58.2.71-15.09.pth, mybk
BLEU = 2.04, 10.5/3.2/1.1/0.5 (BP=1.000, ratio=2.834, hyp_len=32397, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.3.15-23.43.2.97-19.56.2.81-16.58.2.71-15.09.pth, bkmy
BLEU = 7.55, 31.4/12.0/4.7/1.8 (BP=1.000, ratio=1.168, hyp_len=14291, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.3.08-21.68.2.95-19.08.2.78-16.07.2.68-14.56.pth, mybk
BLEU = 4.99, 23.0/7.7/3.0/1.2 (BP=1.000, ratio=1.328, hyp_len=15176, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.3.08-21.68.2.95-19.08.2.78-16.07.2.68-14.56.pth, bkmy
BLEU = 5.95, 24.4/9.6/3.7/1.4 (BP=1.000, ratio=1.499, hyp_len=18329, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.3.04-20.82.2.85-17.34.2.76-15.77.2.66-14.29.pth, mybk
BLEU = 5.92, 26.6/8.9/3.5/1.5 (BP=1.000, ratio=1.185, hyp_len=13547, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.3.04-20.82.2.85-17.34.2.76-15.77.2.66-14.29.pth, bkmy
BLEU = 5.37, 21.6/8.7/3.4/1.3 (BP=1.000, ratio=1.700, hyp_len=20791, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.2.96-19.35.2.83-16.90.2.74-15.56.2.63-13.87.pth, mybk
BLEU = 6.48, 28.8/9.9/4.0/1.5 (BP=1.000, ratio=1.082, hyp_len=12369, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.2.96-19.35.2.83-16.90.2.74-15.56.2.63-13.87.pth, bkmy
BLEU = 5.64, 23.5/9.4/3.5/1.3 (BP=1.000, ratio=1.588, hyp_len=19423, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.2.92-18.55.2.78-16.15.2.71-15.07.2.56-12.94.pth, mybk
BLEU = 3.11, 14.2/4.8/1.8/0.7 (BP=1.000, ratio=2.165, hyp_len=24753, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.2.92-18.55.2.78-16.15.2.71-15.07.2.56-12.94.pth, bkmy
BLEU = 5.49, 21.7/8.6/3.5/1.4 (BP=1.000, ratio=1.770, hyp_len=21649, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.2.89-17.93.2.74-15.53.2.68-14.62.2.57-13.00.pth, mybk
BLEU = 6.36, 27.5/9.6/3.9/1.6 (BP=1.000, ratio=1.172, hyp_len=13402, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.2.89-17.93.2.74-15.53.2.68-14.62.2.57-13.00.pth, bkmy
BLEU = 4.21, 16.7/6.8/2.7/1.0 (BP=1.000, ratio=2.286, hyp_len=27958, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.2.88-17.78.2.73-15.30.2.68-14.56.2.53-12.54.pth, mybk
BLEU = 6.89, 28.4/10.1/4.2/1.9 (BP=1.000, ratio=1.170, hyp_len=13376, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.2.88-17.78.2.73-15.30.2.68-14.56.2.53-12.54.pth, bkmy
BLEU = 6.26, 23.0/9.6/4.0/1.7 (BP=1.000, ratio=1.678, hyp_len=20523, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.31.2.85-17.29.2.71-14.97.2.68-14.59.2.55-12.79.pth, mybk
BLEU = 7.18, 29.1/10.5/4.4/2.0 (BP=1.000, ratio=1.098, hyp_len=12548, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.31.2.85-17.29.2.71-14.97.2.68-14.59.2.55-12.79.pth, bkmy
BLEU = 3.81, 14.6/6.0/2.4/1.0 (BP=1.000, ratio=2.606, hyp_len=31877, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.32.2.84-17.18.2.66-14.33.2.64-14.00.2.52-12.41.pth, mybk
BLEU = 7.07, 28.7/10.4/4.4/1.9 (BP=1.000, ratio=1.130, hyp_len=12919, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.32.2.84-17.18.2.66-14.33.2.64-14.00.2.52-12.41.pth, bkmy
BLEU = 5.99, 22.0/9.2/3.9/1.7 (BP=1.000, ratio=1.775, hyp_len=21704, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.33.2.88-17.77.2.75-15.71.2.64-13.97.2.53-12.54.pth, mybk
BLEU = 7.71, 29.5/11.0/4.8/2.3 (BP=1.000, ratio=1.123, hyp_len=12833, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.33.2.88-17.77.2.75-15.71.2.64-13.97.2.53-12.54.pth, bkmy
BLEU = 4.96, 18.5/7.5/3.2/1.4 (BP=1.000, ratio=2.141, hyp_len=26181, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.34.2.67-14.43.2.54-12.72.2.64-14.01.2.46-11.65.pth, mybk
BLEU = 5.11, 21.0/7.5/3.1/1.4 (BP=1.000, ratio=1.543, hyp_len=17634, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.34.2.67-14.43.2.54-12.72.2.64-14.01.2.46-11.65.pth, bkmy
BLEU = 4.20, 15.4/6.5/2.7/1.1 (BP=1.000, ratio=2.569, hyp_len=31424, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.35.2.64-14.04.2.50-12.24.2.62-13.79.2.46-11.73.pth, mybk
BLEU = 7.33, 30.0/10.9/4.5/2.0 (BP=1.000, ratio=1.126, hyp_len=12878, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.35.2.64-14.04.2.50-12.24.2.62-13.79.2.46-11.73.pth, bkmy
BLEU = 7.38, 25.2/11.0/4.8/2.2 (BP=1.000, ratio=1.588, hyp_len=19426, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.36.2.63-13.90.2.49-12.04.2.64-13.97.2.45-11.56.pth, mybk
BLEU = 6.61, 25.7/9.7/4.2/1.8 (BP=1.000, ratio=1.339, hyp_len=15311, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.36.2.63-13.90.2.49-12.04.2.64-13.97.2.45-11.56.pth, bkmy
BLEU = 4.77, 17.7/7.4/3.1/1.3 (BP=1.000, ratio=2.258, hyp_len=27619, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.37.2.55-12.78.2.41-11.11.2.61-13.62.2.41-11.18.pth, mybk
BLEU = 8.28, 31.6/11.9/5.2/2.4 (BP=1.000, ratio=1.100, hyp_len=12575, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.37.2.55-12.78.2.41-11.11.2.61-13.62.2.41-11.18.pth, bkmy
BLEU = 5.14, 18.5/8.0/3.3/1.4 (BP=1.000, ratio=2.160, hyp_len=26423, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.38.2.57-13.08.2.41-11.12.2.61-13.55.2.38-10.82.pth, mybk
BLEU = 8.52, 31.8/12.2/5.4/2.5 (BP=1.000, ratio=1.085, hyp_len=12402, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.38.2.57-13.08.2.41-11.12.2.61-13.55.2.38-10.82.pth, bkmy
BLEU = 7.98, 27.2/11.9/5.3/2.4 (BP=1.000, ratio=1.528, hyp_len=18690, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.39.2.61-13.65.2.49-12.01.2.63-13.89.2.42-11.30.pth, mybk
BLEU = 8.40, 32.1/12.2/5.3/2.4 (BP=1.000, ratio=1.083, hyp_len=12384, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.39.2.61-13.65.2.49-12.01.2.63-13.89.2.42-11.30.pth, bkmy
BLEU = 6.07, 21.0/9.2/4.0/1.7 (BP=1.000, ratio=1.940, hyp_len=23727, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.40.2.60-13.45.2.39-10.94.2.62-13.74.2.37-10.74.pth, mybk
BLEU = 7.71, 28.8/11.0/4.8/2.3 (BP=1.000, ratio=1.218, hyp_len=13923, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.40.2.60-13.45.2.39-10.94.2.62-13.74.2.37-10.74.pth, bkmy
BLEU = 7.61, 25.9/11.4/5.1/2.2 (BP=1.000, ratio=1.583, hyp_len=19357, ref_len=12231)
```

Best BLEU Score for my-bk, 38 epoch: 8.52 
Best BLEU Score for bk-my, 38 epoch: 7.98  

## Seq2Seq-DSL, my-bk, 50epoch

training

```
Epoch 1 - |param|=8.51e+02 |g_param|=5.12e+05 loss_x2y=4.8842e+00 ppl_x2y=132.19 loss_y2x=4.7158e+00 ppl_y2x=111.70 dual_loss=0.0000e+00
Validation X2Y - loss=4.0222e+00 ppl=55.82 best_loss=inf best_ppl=inf
Validation Y2X - loss=4.0056e+00 ppl=54.91 best_loss=inf best_ppl=inf
Epoch 2 - |param|=8.51e+02 |g_param|=2.84e+05 loss_x2y=4.4699e+00 ppl_x2y=87.35 loss_y2x=4.2711e+00 ppl_y2x=71.60 dual_loss=0.0000e+00
Validation X2Y - loss=3.8824e+00 ppl=48.54 best_loss=4.0222e+00 best_ppl=55.82
Validation Y2X - loss=3.8895e+00 ppl=48.88 best_loss=4.0056e+00 best_ppl=54.91
Epoch 3 - |param|=8.51e+02 |g_param|=2.38e+05 loss_x2y=4.4038e+00 ppl_x2y=81.76 loss_y2x=4.2199e+00 ppl_y2x=68.02 dual_loss=0.0000e+00
Validation X2Y - loss=3.8438e+00 ppl=46.70 best_loss=3.8824e+00 best_ppl=48.54
Validation Y2X - loss=3.7456e+00 ppl=42.34 best_loss=3.8895e+00 best_ppl=48.88
Epoch 4 - |param|=8.51e+02 |g_param|=2.42e+05 loss_x2y=4.4130e+00 ppl_x2y=82.52 loss_y2x=4.2497e+00 ppl_y2x=70.09 dual_loss=0.0000e+00
Validation X2Y - loss=3.8042e+00 ppl=44.89 best_loss=3.8438e+00 best_ppl=46.70
Validation Y2X - loss=3.7233e+00 ppl=41.40 best_loss=3.7456e+00 best_ppl=42.34
Epoch 5 - |param|=8.51e+02 |g_param|=2.37e+05 loss_x2y=4.3184e+00 ppl_x2y=75.07 loss_y2x=4.1149e+00 ppl_y2x=61.25 dual_loss=0.0000e+00
Validation X2Y - loss=3.8033e+00 ppl=44.85 best_loss=3.8042e+00 best_ppl=44.89
Validation Y2X - loss=3.7788e+00 ppl=43.76 best_loss=3.7233e+00 best_ppl=41.40
Epoch 6 - |param|=8.52e+02 |g_param|=2.45e+05 loss_x2y=4.3511e+00 ppl_x2y=77.57 loss_y2x=4.1532e+00 ppl_y2x=63.64 dual_loss=0.0000e+00
Validation X2Y - loss=3.7830e+00 ppl=43.95 best_loss=3.8033e+00 best_ppl=44.85
Validation Y2X - loss=3.6924e+00 ppl=40.14 best_loss=3.7233e+00 best_ppl=41.40
Epoch 7 - |param|=8.52e+02 |g_param|=2.32e+05 loss_x2y=4.3176e+00 ppl_x2y=75.01 loss_y2x=4.1115e+00 ppl_y2x=61.04 dual_loss=0.0000e+00
Validation X2Y - loss=3.7508e+00 ppl=42.55 best_loss=3.7830e+00 best_ppl=43.95
Validation Y2X - loss=3.6664e+00 ppl=39.11 best_loss=3.6924e+00 best_ppl=40.14
Epoch 8 - |param|=8.52e+02 |g_param|=2.25e+05 loss_x2y=4.2564e+00 ppl_x2y=70.55 loss_y2x=4.0570e+00 ppl_y2x=57.80 dual_loss=0.0000e+00
Validation X2Y - loss=3.7390e+00 ppl=42.05 best_loss=3.7508e+00 best_ppl=42.55
Validation Y2X - loss=3.6984e+00 ppl=40.38 best_loss=3.6664e+00 best_ppl=39.11
Epoch 9 - |param|=8.53e+02 |g_param|=2.17e+05 loss_x2y=4.1919e+00 ppl_x2y=66.15 loss_y2x=4.0317e+00 ppl_y2x=56.36 dual_loss=0.0000e+00
Validation X2Y - loss=3.6429e+00 ppl=38.20 best_loss=3.7390e+00 best_ppl=42.05
Validation Y2X - loss=3.6578e+00 ppl=38.78 best_loss=3.6664e+00 best_ppl=39.11
Epoch 10 - |param|=8.53e+02 |g_param|=2.01e+05 loss_x2y=3.9570e+00 ppl_x2y=52.30 loss_y2x=3.9714e+00 ppl_y2x=53.06 dual_loss=0.0000e+00
Validation X2Y - loss=3.4837e+00 ppl=32.58 best_loss=3.6429e+00 best_ppl=38.20
Validation Y2X - loss=3.5852e+00 ppl=36.06 best_loss=3.6578e+00 best_ppl=38.78
Epoch 11 - |param|=8.54e+02 |g_param|=1.66e+05 loss_x2y=3.9305e+00 ppl_x2y=50.93 loss_y2x=3.9880e+00 ppl_y2x=53.95 dual_loss=0.0000e+00
Validation X2Y - loss=3.3770e+00 ppl=29.28 best_loss=3.4837e+00 best_ppl=32.58
Validation Y2X - loss=3.4606e+00 ppl=31.84 best_loss=3.5852e+00 best_ppl=36.06
Epoch 12 - |param|=8.54e+02 |g_param|=1.61e+05 loss_x2y=3.7753e+00 ppl_x2y=43.61 loss_y2x=3.6870e+00 ppl_y2x=39.93 dual_loss=0.0000e+00
Validation X2Y - loss=3.3110e+00 ppl=27.41 best_loss=3.3770e+00 best_ppl=29.28
Validation Y2X - loss=3.2588e+00 ppl=26.02 best_loss=3.4606e+00 best_ppl=31.84
Epoch 13 - |param|=8.55e+02 |g_param|=1.57e+05 loss_x2y=3.7184e+00 ppl_x2y=41.20 loss_y2x=3.5926e+00 ppl_y2x=36.33 dual_loss=0.0000e+00
Validation X2Y - loss=3.2323e+00 ppl=25.34 best_loss=3.3110e+00 best_ppl=27.41
Validation Y2X - loss=3.1333e+00 ppl=22.95 best_loss=3.2588e+00 best_ppl=26.02
Epoch 14 - |param|=8.56e+02 |g_param|=1.57e+05 loss_x2y=3.6022e+00 ppl_x2y=36.68 loss_y2x=3.4031e+00 ppl_y2x=30.06 dual_loss=0.0000e+00
Validation X2Y - loss=3.1739e+00 ppl=23.90 best_loss=3.2323e+00 best_ppl=25.34
Validation Y2X - loss=3.1219e+00 ppl=22.69 best_loss=3.1333e+00 best_ppl=22.95
Epoch 15 - |param|=8.56e+02 |g_param|=1.50e+05 loss_x2y=3.6212e+00 ppl_x2y=37.38 loss_y2x=3.4695e+00 ppl_y2x=32.12 dual_loss=0.0000e+00
Validation X2Y - loss=3.1295e+00 ppl=22.86 best_loss=3.1739e+00 best_ppl=23.90
Validation Y2X - loss=3.0221e+00 ppl=20.54 best_loss=3.1219e+00 best_ppl=22.69
Epoch 16 - |param|=8.57e+02 |g_param|=1.53e+05 loss_x2y=3.5126e+00 ppl_x2y=33.53 loss_y2x=3.3277e+00 ppl_y2x=27.87 dual_loss=0.0000e+00
Validation X2Y - loss=3.0446e+00 ppl=21.00 best_loss=3.1295e+00 best_ppl=22.86
Validation Y2X - loss=2.9585e+00 ppl=19.27 best_loss=3.0221e+00 best_ppl=20.54
Epoch 17 - |param|=8.58e+02 |g_param|=1.44e+05 loss_x2y=3.3934e+00 ppl_x2y=29.77 loss_y2x=3.2423e+00 ppl_y2x=25.59 dual_loss=0.0000e+00
Validation X2Y - loss=2.9992e+00 ppl=20.07 best_loss=3.0446e+00 best_ppl=21.00
Validation Y2X - loss=2.8921e+00 ppl=18.03 best_loss=2.9585e+00 best_ppl=19.27
Epoch 18 - |param|=8.58e+02 |g_param|=1.62e+05 loss_x2y=3.3356e+00 ppl_x2y=28.09 loss_y2x=3.1525e+00 ppl_y2x=23.40 dual_loss=0.0000e+00
Validation X2Y - loss=2.9697e+00 ppl=19.49 best_loss=2.9992e+00 best_ppl=20.07
Validation Y2X - loss=2.8401e+00 ppl=17.12 best_loss=2.8921e+00 best_ppl=18.03
Epoch 19 - |param|=8.59e+02 |g_param|=1.55e+05 loss_x2y=3.2690e+00 ppl_x2y=26.28 loss_y2x=3.0886e+00 ppl_y2x=21.95 dual_loss=0.0000e+00
Validation X2Y - loss=2.8974e+00 ppl=18.13 best_loss=2.9697e+00 best_ppl=19.49
Validation Y2X - loss=2.8067e+00 ppl=16.56 best_loss=2.8401e+00 best_ppl=17.12
Epoch 20 - |param|=8.60e+02 |g_param|=1.70e+05 loss_x2y=3.2922e+00 ppl_x2y=26.90 loss_y2x=3.0383e+00 ppl_y2x=20.87 dual_loss=0.0000e+00
Validation X2Y - loss=2.8883e+00 ppl=17.96 best_loss=2.8974e+00 best_ppl=18.13
Validation Y2X - loss=2.7198e+00 ppl=15.18 best_loss=2.8067e+00 best_ppl=16.56
Epoch 21 - |param|=8.61e+02 |g_param|=1.70e+05 loss_x2y=3.2209e+00 ppl_x2y=25.05 loss_y2x=3.0070e+00 ppl_y2x=20.23 dual_loss=6.7018e-01
Validation X2Y - loss=2.8971e+00 ppl=18.12 best_loss=2.8883e+00 best_ppl=17.96
Validation Y2X - loss=2.7005e+00 ppl=14.89 best_loss=2.7198e+00 best_ppl=15.18
Epoch 22 - |param|=8.61e+02 |g_param|=1.66e+05 loss_x2y=3.1953e+00 ppl_x2y=24.42 loss_y2x=3.0603e+00 ppl_y2x=21.33 dual_loss=7.1410e-01
Validation X2Y - loss=2.8167e+00 ppl=16.72 best_loss=2.8883e+00 best_ppl=17.96
Validation Y2X - loss=2.6620e+00 ppl=14.33 best_loss=2.7005e+00 best_ppl=14.89
Epoch 23 - |param|=8.62e+02 |g_param|=1.65e+05 loss_x2y=3.1177e+00 ppl_x2y=22.59 loss_y2x=2.9229e+00 ppl_y2x=18.60 dual_loss=5.2342e-01
Validation X2Y - loss=2.8162e+00 ppl=16.71 best_loss=2.8167e+00 best_ppl=16.72
Validation Y2X - loss=2.6105e+00 ppl=13.61 best_loss=2.6620e+00 best_ppl=14.33
Epoch 24 - |param|=8.63e+02 |g_param|=1.73e+05 loss_x2y=3.0268e+00 ppl_x2y=20.63 loss_y2x=2.8117e+00 ppl_y2x=16.64 dual_loss=4.4919e-01
Validation X2Y - loss=2.7735e+00 ppl=16.01 best_loss=2.8162e+00 best_ppl=16.71
Validation Y2X - loss=2.5485e+00 ppl=12.79 best_loss=2.6105e+00 best_ppl=13.61
Epoch 25 - |param|=8.64e+02 |g_param|=1.71e+05 loss_x2y=3.0142e+00 ppl_x2y=20.37 loss_y2x=2.7983e+00 ppl_y2x=16.42 dual_loss=5.0778e-01
Validation X2Y - loss=2.7520e+00 ppl=15.67 best_loss=2.7735e+00 best_ppl=16.01
Validation Y2X - loss=2.5412e+00 ppl=12.70 best_loss=2.5485e+00 best_ppl=12.79
Epoch 26 - |param|=8.64e+02 |g_param|=1.85e+05 loss_x2y=2.9324e+00 ppl_x2y=18.77 loss_y2x=2.7396e+00 ppl_y2x=15.48 dual_loss=4.2058e-01
Validation X2Y - loss=2.7380e+00 ppl=15.46 best_loss=2.7520e+00 best_ppl=15.67
Validation Y2X - loss=2.5308e+00 ppl=12.56 best_loss=2.5412e+00 best_ppl=12.70
Epoch 27 - |param|=8.65e+02 |g_param|=1.73e+05 loss_x2y=2.9372e+00 ppl_x2y=18.86 loss_y2x=2.7219e+00 ppl_y2x=15.21 dual_loss=4.1720e-01
Validation X2Y - loss=2.7201e+00 ppl=15.18 best_loss=2.7380e+00 best_ppl=15.46
Validation Y2X - loss=2.4681e+00 ppl=11.80 best_loss=2.5308e+00 best_ppl=12.56
Epoch 28 - |param|=8.66e+02 |g_param|=1.81e+05 loss_x2y=2.8451e+00 ppl_x2y=17.20 loss_y2x=2.6274e+00 ppl_y2x=13.84 dual_loss=3.5689e-01
Validation X2Y - loss=2.7153e+00 ppl=15.11 best_loss=2.7201e+00 best_ppl=15.18
Validation Y2X - loss=2.4346e+00 ppl=11.41 best_loss=2.4681e+00 best_ppl=11.80
Epoch 29 - |param|=8.66e+02 |g_param|=1.86e+05 loss_x2y=2.8834e+00 ppl_x2y=17.88 loss_y2x=2.6935e+00 ppl_y2x=14.78 dual_loss=4.1017e-01
Validation X2Y - loss=2.6653e+00 ppl=14.37 best_loss=2.7153e+00 best_ppl=15.11
Validation Y2X - loss=2.4172e+00 ppl=11.21 best_loss=2.4346e+00 best_ppl=11.41
Epoch 30 - |param|=8.67e+02 |g_param|=1.97e+05 loss_x2y=2.8886e+00 ppl_x2y=17.97 loss_y2x=2.6553e+00 ppl_y2x=14.23 dual_loss=3.6459e-01
Validation X2Y - loss=2.6693e+00 ppl=14.43 best_loss=2.6653e+00 best_ppl=14.37
Validation Y2X - loss=2.3989e+00 ppl=11.01 best_loss=2.4172e+00 best_ppl=11.21
Epoch 31 - |param|=8.68e+02 |g_param|=1.91e+05 loss_x2y=2.7555e+00 ppl_x2y=15.73 loss_y2x=2.5265e+00 ppl_y2x=12.51 dual_loss=3.0923e-01
Validation X2Y - loss=2.6541e+00 ppl=14.21 best_loss=2.6653e+00 best_ppl=14.37
Validation Y2X - loss=2.3857e+00 ppl=10.87 best_loss=2.3989e+00 best_ppl=11.01
Epoch 32 - |param|=8.69e+02 |g_param|=1.95e+05 loss_x2y=2.7230e+00 ppl_x2y=15.23 loss_y2x=2.4797e+00 ppl_y2x=11.94 dual_loss=3.1594e-01
Validation X2Y - loss=2.6271e+00 ppl=13.83 best_loss=2.6541e+00 best_ppl=14.21
Validation Y2X - loss=2.3804e+00 ppl=10.81 best_loss=2.3857e+00 best_ppl=10.87
Epoch 33 - |param|=8.69e+02 |g_param|=1.92e+05 loss_x2y=2.7264e+00 ppl_x2y=15.28 loss_y2x=2.4811e+00 ppl_y2x=11.95 dual_loss=3.1692e-01
Validation X2Y - loss=2.6411e+00 ppl=14.03 best_loss=2.6271e+00 best_ppl=13.83
Validation Y2X - loss=2.3776e+00 ppl=10.78 best_loss=2.3804e+00 best_ppl=10.81
Epoch 34 - |param|=8.70e+02 |g_param|=1.96e+05 loss_x2y=2.6919e+00 ppl_x2y=14.76 loss_y2x=2.4368e+00 ppl_y2x=11.44 dual_loss=3.0925e-01
Validation X2Y - loss=2.6138e+00 ppl=13.65 best_loss=2.6271e+00 best_ppl=13.83
Validation Y2X - loss=2.3210e+00 ppl=10.19 best_loss=2.3776e+00 best_ppl=10.78
Epoch 35 - |param|=8.71e+02 |g_param|=3.64e+05 loss_x2y=2.5803e+00 ppl_x2y=13.20 loss_y2x=2.3534e+00 ppl_y2x=10.52 dual_loss=2.9145e-01
Validation X2Y - loss=2.6125e+00 ppl=13.63 best_loss=2.6138e+00 best_ppl=13.65
Validation Y2X - loss=2.3474e+00 ppl=10.46 best_loss=2.3210e+00 best_ppl=10.19
Epoch 36 - |param|=8.71e+02 |g_param|=4.01e+05 loss_x2y=2.5817e+00 ppl_x2y=13.22 loss_y2x=2.3446e+00 ppl_y2x=10.43 dual_loss=2.8207e-01
Validation X2Y - loss=2.6088e+00 ppl=13.58 best_loss=2.6125e+00 best_ppl=13.63
Validation Y2X - loss=2.3438e+00 ppl=10.42 best_loss=2.3210e+00 best_ppl=10.19
Epoch 37 - |param|=8.72e+02 |g_param|=4.07e+05 loss_x2y=2.5864e+00 ppl_x2y=13.28 loss_y2x=2.3348e+00 ppl_y2x=10.33 dual_loss=2.7979e-01
Validation X2Y - loss=2.6017e+00 ppl=13.49 best_loss=2.6088e+00 best_ppl=13.58
Validation Y2X - loss=2.3146e+00 ppl=10.12 best_loss=2.3210e+00 best_ppl=10.19
Epoch 38 - |param|=8.73e+02 |g_param|=4.13e+05 loss_x2y=2.4823e+00 ppl_x2y=11.97 loss_y2x=2.2592e+00 ppl_y2x=9.57 dual_loss=2.6178e-01
Validation X2Y - loss=2.5653e+00 ppl=13.00 best_loss=2.6017e+00 best_ppl=13.49
Validation Y2X - loss=2.3205e+00 ppl=10.18 best_loss=2.3146e+00 best_ppl=10.12
Epoch 39 - |param|=8.73e+02 |g_param|=4.03e+05 loss_x2y=2.4888e+00 ppl_x2y=12.05 loss_y2x=2.2560e+00 ppl_y2x=9.54 dual_loss=2.7806e-01
Validation X2Y - loss=2.5827e+00 ppl=13.23 best_loss=2.5653e+00 best_ppl=13.00
Validation Y2X - loss=2.3086e+00 ppl=10.06 best_loss=2.3146e+00 best_ppl=10.12
Epoch 40 - |param|=8.74e+02 |g_param|=4.27e+05 loss_x2y=2.4468e+00 ppl_x2y=11.55 loss_y2x=2.2037e+00 ppl_y2x=9.06 dual_loss=2.5743e-01
Validation X2Y - loss=2.5799e+00 ppl=13.20 best_loss=2.5653e+00 best_ppl=13.00
Validation Y2X - loss=2.3145e+00 ppl=10.12 best_loss=2.3086e+00 best_ppl=10.06
Epoch 41 - |param|=8.75e+02 |g_param|=4.15e+05 loss_x2y=2.4347e+00 ppl_x2y=11.41 loss_y2x=2.2156e+00 ppl_y2x=9.17 dual_loss=2.5765e-01
Validation X2Y - loss=2.5921e+00 ppl=13.36 best_loss=2.5653e+00 best_ppl=13.00
Validation Y2X - loss=2.3026e+00 ppl=10.00 best_loss=2.3086e+00 best_ppl=10.06
Epoch 42 - |param|=8.75e+02 |g_param|=4.45e+05 loss_x2y=2.3817e+00 ppl_x2y=10.82 loss_y2x=2.1810e+00 ppl_y2x=8.86 dual_loss=2.5487e-01
Validation X2Y - loss=2.5670e+00 ppl=13.03 best_loss=2.5653e+00 best_ppl=13.00
Validation Y2X - loss=2.3129e+00 ppl=10.10 best_loss=2.3026e+00 best_ppl=10.00
Epoch 43 - |param|=8.76e+02 |g_param|=4.37e+05 loss_x2y=2.3751e+00 ppl_x2y=10.75 loss_y2x=2.1723e+00 ppl_y2x=8.78 dual_loss=2.6267e-01
Validation X2Y - loss=2.5837e+00 ppl=13.25 best_loss=2.5653e+00 best_ppl=13.00
Validation Y2X - loss=2.3035e+00 ppl=10.01 best_loss=2.3026e+00 best_ppl=10.00
Epoch 44 - |param|=8.77e+02 |g_param|=4.51e+05 loss_x2y=2.3590e+00 ppl_x2y=10.58 loss_y2x=2.1385e+00 ppl_y2x=8.49 dual_loss=2.5648e-01
Validation X2Y - loss=2.5573e+00 ppl=12.90 best_loss=2.5653e+00 best_ppl=13.00
Validation Y2X - loss=2.2739e+00 ppl=9.72 best_loss=2.3026e+00 best_ppl=10.00
Epoch 45 - |param|=8.77e+02 |g_param|=4.51e+05 loss_x2y=2.3995e+00 ppl_x2y=11.02 loss_y2x=2.1563e+00 ppl_y2x=8.64 dual_loss=2.6441e-01
Validation X2Y - loss=2.5590e+00 ppl=12.92 best_loss=2.5573e+00 best_ppl=12.90
Validation Y2X - loss=2.2885e+00 ppl=9.86 best_loss=2.2739e+00 best_ppl=9.72
Epoch 46 - |param|=8.78e+02 |g_param|=4.94e+05 loss_x2y=2.2593e+00 ppl_x2y=9.58 loss_y2x=2.0401e+00 ppl_y2x=7.69 dual_loss=2.4456e-01
Validation X2Y - loss=2.5969e+00 ppl=13.42 best_loss=2.5573e+00 best_ppl=12.90
Validation Y2X - loss=2.2715e+00 ppl=9.69 best_loss=2.2739e+00 best_ppl=9.72
Epoch 47 - |param|=8.79e+02 |g_param|=4.58e+05 loss_x2y=2.2726e+00 ppl_x2y=9.70 loss_y2x=2.0641e+00 ppl_y2x=7.88 dual_loss=2.5514e-01
Validation X2Y - loss=2.5576e+00 ppl=12.90 best_loss=2.5573e+00 best_ppl=12.90
Validation Y2X - loss=2.2641e+00 ppl=9.62 best_loss=2.2715e+00 best_ppl=9.69
Epoch 48 - |param|=8.79e+02 |g_param|=4.89e+05 loss_x2y=2.2953e+00 ppl_x2y=9.93 loss_y2x=2.0855e+00 ppl_y2x=8.05 dual_loss=2.6356e-01
Validation X2Y - loss=2.5397e+00 ppl=12.68 best_loss=2.5573e+00 best_ppl=12.90
Validation Y2X - loss=2.2633e+00 ppl=9.61 best_loss=2.2641e+00 best_ppl=9.62
Epoch 49 - |param|=8.80e+02 |g_param|=4.88e+05 loss_x2y=2.2726e+00 ppl_x2y=9.70 loss_y2x=2.0389e+00 ppl_y2x=7.68 dual_loss=2.5563e-01
Validation X2Y - loss=2.5645e+00 ppl=12.99 best_loss=2.5397e+00 best_ppl=12.68
Validation Y2X - loss=2.2639e+00 ppl=9.62 best_loss=2.2633e+00 best_ppl=9.61
Epoch 50 - |param|=8.81e+02 |g_param|=4.85e+05 loss_x2y=2.2172e+00 ppl_x2y=9.18 loss_y2x=2.0291e+00 ppl_y2x=7.61 dual_loss=2.5187e-01
Validation X2Y - loss=2.5800e+00 ppl=13.20 best_loss=2.5397e+00 best_ppl=12.68
Validation Y2X - loss=2.2237e+00 ppl=9.24 best_loss=2.2633e+00 best_ppl=9.61
```

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/mybk-50epoch
Evaluation result for the model: dsl-model-mybk.01.4.88-132.19.4.72-111.70.4.02-55.82.4.01-54.91.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.5/0.0/0.0/0.0 (BP=0.746, ratio=0.773, hyp_len=8840, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.88-132.19.4.72-111.70.4.02-55.82.4.01-54.91.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.0/0.1/0.0/0.0 (BP=0.737, ratio=0.766, hyp_len=9373, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.02.4.47-87.35.4.27-71.60.3.88-48.54.3.89-48.88.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.4/0.4/0.0/0.0 (BP=0.887, ratio=0.893, hyp_len=10206, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.4.47-87.35.4.27-71.60.3.88-48.54.3.89-48.88.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.6/0.4/0.0/0.0 (BP=1.000, ratio=1.162, hyp_len=14207, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.4.40-81.76.4.22-68.02.3.84-46.70.3.75-42.34.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.4/0.2/0.0/0.0 (BP=1.000, ratio=1.070, hyp_len=12231, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.4.40-81.76.4.22-68.02.3.84-46.70.3.75-42.34.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 22.2/1.5/0.1/0.0 (BP=0.929, ratio=0.931, hyp_len=11387, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.4.41-82.52.4.25-70.09.3.80-44.89.3.72-41.40.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.1/0.3/0.0/0.0 (BP=1.000, ratio=1.005, hyp_len=11485, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.4.41-82.52.4.25-70.09.3.80-44.89.3.72-41.40.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.8/0.6/0.0/0.0 (BP=0.942, ratio=0.943, hyp_len=11536, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.4.32-75.07.4.11-61.25.3.80-44.85.3.78-43.76.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.2/0.3/0.0/0.0 (BP=0.993, ratio=0.993, hyp_len=11350, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.4.32-75.07.4.11-61.25.3.80-44.85.3.78-43.76.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.3/0.5/0.0/0.0 (BP=1.000, ratio=1.016, hyp_len=12425, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.4.35-77.57.4.15-63.64.3.78-43.95.3.69-40.14.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.9/0.2/0.0/0.0 (BP=1.000, ratio=1.084, hyp_len=12387, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.4.35-77.57.4.15-63.64.3.78-43.95.3.69-40.14.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.7/1.8/0.3/0.0 (BP=1.000, ratio=1.037, hyp_len=12689, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.4.32-75.01.4.11-61.04.3.75-42.55.3.67-39.11.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 14.8/0.2/0.0/0.0 (BP=1.000, ratio=1.112, hyp_len=12716, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.4.32-75.01.4.11-61.04.3.75-42.55.3.67-39.11.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.4/1.6/0.3/0.0 (BP=1.000, ratio=1.034, hyp_len=12652, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.4.26-70.55.4.06-57.80.3.74-42.05.3.70-40.38.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.8/0.3/0.0/0.0 (BP=1.000, ratio=1.074, hyp_len=12274, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.4.26-70.55.4.06-57.80.3.74-42.05.3.70-40.38.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.0/0.6/0.0/0.0 (BP=1.000, ratio=1.082, hyp_len=13231, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.4.19-66.15.4.03-56.36.3.64-38.20.3.66-38.78.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.7/0.5/0.0/0.0 (BP=0.828, ratio=0.841, hyp_len=9618, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.4.19-66.15.4.03-56.36.3.64-38.20.3.66-38.78.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.9/0.9/0.0/0.0 (BP=1.000, ratio=1.083, hyp_len=13241, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.3.96-52.30.3.97-53.06.3.48-32.58.3.59-36.06.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.5/2.7/0.8/0.0 (BP=0.816, ratio=0.831, hyp_len=9505, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.3.96-52.30.3.97-53.06.3.48-32.58.3.59-36.06.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.4/1.2/0.2/0.0 (BP=1.000, ratio=1.079, hyp_len=13192, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.3.93-50.93.3.99-53.95.3.38-29.28.3.46-31.84.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 23.0/2.6/0.2/0.0 (BP=0.978, ratio=0.978, hyp_len=11183, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.3.93-50.93.3.99-53.95.3.38-29.28.3.46-31.84.pth, bkmy
BLEU = 0.02, 0.4/0.0/0.0/0.0 (BP=1.000, ratio=21.349, hyp_len=261117, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.3.78-43.61.3.69-39.93.3.31-27.41.3.26-26.02.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.9/2.6/0.4/0.0 (BP=1.000, ratio=1.361, hyp_len=15563, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.3.78-43.61.3.69-39.93.3.31-27.41.3.26-26.02.pth, bkmy
BLEU = 0.82, 16.3/3.0/0.3/0.0 (BP=1.000, ratio=1.508, hyp_len=18445, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.3.72-41.20.3.59-36.33.3.23-25.34.3.13-22.95.pth, mybk
BLEU = 1.72, 25.0/5.2/1.1/0.1 (BP=0.992, ratio=0.992, hyp_len=11337, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.3.72-41.20.3.59-36.33.3.23-25.34.3.13-22.95.pth, bkmy
BLEU = 1.26, 23.4/5.0/0.7/0.0 (BP=1.000, ratio=1.097, hyp_len=13417, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.3.60-36.68.3.40-30.06.3.17-23.90.3.12-22.69.pth, mybk
BLEU = 2.59, 21.3/4.9/1.4/0.3 (BP=1.000, ratio=1.186, hyp_len=13553, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.3.60-36.68.3.40-30.06.3.17-23.90.3.12-22.69.pth, bkmy
BLEU = 2.67, 24.0/6.2/1.7/0.2 (BP=1.000, ratio=1.172, hyp_len=14335, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.3.62-37.38.3.47-32.12.3.13-22.86.3.02-20.54.pth, mybk
BLEU = 2.03, 19.5/4.8/1.1/0.2 (BP=1.000, ratio=1.324, hyp_len=15131, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.3.62-37.38.3.47-32.12.3.13-22.86.3.02-20.54.pth, bkmy
BLEU = 2.51, 23.5/5.8/1.3/0.2 (BP=1.000, ratio=1.191, hyp_len=14568, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.3.51-33.53.3.33-27.87.3.04-21.00.2.96-19.27.pth, mybk
BLEU = 1.98, 19.5/5.0/1.2/0.1 (BP=1.000, ratio=1.385, hyp_len=15831, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.3.51-33.53.3.33-27.87.3.04-21.00.2.96-19.27.pth, bkmy
BLEU = 2.13, 25.3/6.8/1.5/0.1 (BP=1.000, ratio=1.077, hyp_len=13171, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.3.39-29.77.3.24-25.59.3.00-20.07.2.89-18.03.pth, mybk
BLEU = 2.74, 16.5/4.3/1.4/0.6 (BP=1.000, ratio=1.645, hyp_len=18808, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.3.39-29.77.3.24-25.59.3.00-20.07.2.89-18.03.pth, bkmy
BLEU = 4.02, 24.6/7.9/2.4/0.6 (BP=1.000, ratio=1.169, hyp_len=14293, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.3.34-28.09.3.15-23.40.2.97-19.49.2.84-17.12.pth, mybk
BLEU = 3.95, 22.0/6.2/2.2/0.8 (BP=1.000, ratio=1.272, hyp_len=14541, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.3.34-28.09.3.15-23.40.2.97-19.49.2.84-17.12.pth, bkmy
BLEU = 4.09, 27.1/8.4/2.4/0.5 (BP=1.000, ratio=1.081, hyp_len=13224, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.3.27-26.28.3.09-21.95.2.90-18.13.2.81-16.56.pth, mybk
BLEU = 3.17, 18.3/5.1/1.8/0.6 (BP=1.000, ratio=1.534, hyp_len=17535, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.3.27-26.28.3.09-21.95.2.90-18.13.2.81-16.56.pth, bkmy
BLEU = 2.59, 17.1/5.4/1.5/0.3 (BP=1.000, ratio=1.790, hyp_len=21895, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.3.29-26.90.3.04-20.87.2.89-17.96.2.72-15.18.pth, mybk
BLEU = 2.77, 16.2/4.3/1.5/0.6 (BP=1.000, ratio=1.739, hyp_len=19876, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.3.29-26.90.3.04-20.87.2.89-17.96.2.72-15.18.pth, bkmy
BLEU = 3.86, 24.9/7.7/2.3/0.5 (BP=1.000, ratio=1.205, hyp_len=14735, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.3.22-25.05.3.01-20.23.2.90-18.12.2.70-14.89.pth, mybk
BLEU = 5.04, 26.4/7.8/2.9/1.1 (BP=1.000, ratio=1.120, hyp_len=12801, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.3.22-25.05.3.01-20.23.2.90-18.12.2.70-14.89.pth, bkmy
BLEU = 3.63, 18.7/6.4/2.2/0.7 (BP=1.000, ratio=1.706, hyp_len=20872, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.3.20-24.42.3.06-21.33.2.82-16.72.2.66-14.33.pth, mybk
BLEU = 4.07, 21.5/6.2/2.4/0.9 (BP=1.000, ratio=1.340, hyp_len=15324, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.3.20-24.42.3.06-21.33.2.82-16.72.2.66-14.33.pth, bkmy
BLEU = 2.17, 11.4/3.8/1.3/0.4 (BP=1.000, ratio=2.790, hyp_len=34123, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.3.12-22.59.2.92-18.60.2.82-16.71.2.61-13.61.pth, mybk
BLEU = 4.44, 23.3/6.7/2.6/0.9 (BP=1.000, ratio=1.279, hyp_len=14624, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.3.12-22.59.2.92-18.60.2.82-16.71.2.61-13.61.pth, bkmy
BLEU = 3.21, 16.9/5.6/2.0/0.6 (BP=1.000, ratio=1.877, hyp_len=22962, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.3.03-20.63.2.81-16.64.2.77-16.01.2.55-12.79.pth, mybk
BLEU = 4.53, 23.9/7.2/2.6/0.9 (BP=1.000, ratio=1.248, hyp_len=14270, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.3.03-20.63.2.81-16.64.2.77-16.01.2.55-12.79.pth, bkmy
BLEU = 3.31, 16.0/5.7/2.0/0.6 (BP=1.000, ratio=2.091, hyp_len=25571, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.3.01-20.37.2.80-16.42.2.75-15.67.2.54-12.70.pth, mybk
BLEU = 5.27, 26.1/8.1/3.2/1.2 (BP=1.000, ratio=1.161, hyp_len=13273, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.3.01-20.37.2.80-16.42.2.75-15.67.2.54-12.70.pth, bkmy
BLEU = 2.35, 11.3/3.9/1.4/0.5 (BP=1.000, ratio=2.879, hyp_len=35209, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.2.93-18.77.2.74-15.48.2.74-15.46.2.53-12.56.pth, mybk
BLEU = 5.26, 26.9/8.2/3.1/1.1 (BP=1.000, ratio=1.146, hyp_len=13098, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.2.93-18.77.2.74-15.48.2.74-15.46.2.53-12.56.pth, bkmy
BLEU = 5.75, 25.6/9.5/3.5/1.3 (BP=1.000, ratio=1.347, hyp_len=16476, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.2.94-18.86.2.72-15.21.2.72-15.18.2.47-11.80.pth, mybk
BLEU = 5.95, 27.4/8.8/3.5/1.5 (BP=1.000, ratio=1.130, hyp_len=12922, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.2.94-18.86.2.72-15.21.2.72-15.18.2.47-11.80.pth, bkmy
BLEU = 7.44, 31.9/11.9/4.7/1.7 (BP=1.000, ratio=1.090, hyp_len=13329, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.2.85-17.20.2.63-13.84.2.72-15.11.2.43-11.41.pth, mybk
BLEU = 4.92, 22.7/7.1/3.0/1.2 (BP=1.000, ratio=1.340, hyp_len=15316, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.2.85-17.20.2.63-13.84.2.72-15.11.2.43-11.41.pth, bkmy
BLEU = 6.08, 26.0/9.8/3.7/1.4 (BP=1.000, ratio=1.339, hyp_len=16377, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.2.88-17.88.2.69-14.78.2.67-14.37.2.42-11.21.pth, mybk
BLEU = 6.33, 27.7/9.2/3.8/1.7 (BP=1.000, ratio=1.148, hyp_len=13129, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.2.88-17.88.2.69-14.78.2.67-14.37.2.42-11.21.pth, bkmy
BLEU = 4.80, 21.5/7.7/2.9/1.1 (BP=1.000, ratio=1.614, hyp_len=19736, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.2.89-17.97.2.66-14.23.2.67-14.43.2.40-11.01.pth, mybk
BLEU = 5.86, 26.6/8.7/3.4/1.5 (BP=1.000, ratio=1.201, hyp_len=13728, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.2.89-17.97.2.66-14.23.2.67-14.43.2.40-11.01.pth, bkmy
BLEU = 8.35, 33.9/12.9/5.2/2.1 (BP=1.000, ratio=1.054, hyp_len=12890, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.31.2.76-15.73.2.53-12.51.2.65-14.21.2.39-10.87.pth, mybk
BLEU = 6.36, 27.6/9.2/3.8/1.7 (BP=1.000, ratio=1.159, hyp_len=13247, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.31.2.76-15.73.2.53-12.51.2.65-14.21.2.39-10.87.pth, bkmy
BLEU = 7.77, 32.8/12.3/4.9/1.9 (BP=1.000, ratio=1.100, hyp_len=13452, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.32.2.72-15.23.2.48-11.94.2.63-13.83.2.38-10.81.pth, mybk
BLEU = 7.20, 29.2/10.2/4.4/2.1 (BP=1.000, ratio=1.121, hyp_len=12810, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.32.2.72-15.23.2.48-11.94.2.63-13.83.2.38-10.81.pth, bkmy
BLEU = 7.81, 31.7/12.3/4.9/1.9 (BP=1.000, ratio=1.162, hyp_len=14216, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.33.2.73-15.28.2.48-11.95.2.64-14.03.2.38-10.78.pth, mybk
BLEU = 6.59, 28.4/9.5/4.0/1.8 (BP=1.000, ratio=1.135, hyp_len=12975, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.33.2.73-15.28.2.48-11.95.2.64-14.03.2.38-10.78.pth, bkmy
BLEU = 5.90, 25.7/9.6/3.6/1.3 (BP=1.000, ratio=1.432, hyp_len=17512, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.34.2.69-14.76.2.44-11.44.2.61-13.65.2.32-10.19.pth, mybk
BLEU = 7.43, 29.5/10.5/4.6/2.2 (BP=1.000, ratio=1.134, hyp_len=12969, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.34.2.69-14.76.2.44-11.44.2.61-13.65.2.32-10.19.pth, bkmy
BLEU = 7.47, 30.9/11.9/4.7/1.8 (BP=1.000, ratio=1.219, hyp_len=14910, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.35.2.58-13.20.2.35-10.52.2.61-13.63.2.35-10.46.pth, mybk
BLEU = 7.74, 30.5/10.8/4.8/2.3 (BP=1.000, ratio=1.115, hyp_len=12741, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.35.2.58-13.20.2.35-10.52.2.61-13.63.2.35-10.46.pth, bkmy
BLEU = 8.24, 33.4/13.0/5.1/2.1 (BP=1.000, ratio=1.118, hyp_len=13675, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.36.2.58-13.22.2.34-10.43.2.61-13.58.2.34-10.42.pth, mybk
BLEU = 7.70, 29.8/10.9/4.8/2.2 (BP=1.000, ratio=1.124, hyp_len=12847, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.36.2.58-13.22.2.34-10.43.2.61-13.58.2.34-10.42.pth, bkmy
BLEU = 7.83, 32.3/12.4/4.9/1.9 (BP=1.000, ratio=1.178, hyp_len=14413, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.37.2.59-13.28.2.33-10.33.2.60-13.49.2.31-10.12.pth, mybk
BLEU = 7.62, 30.6/10.9/4.7/2.1 (BP=1.000, ratio=1.119, hyp_len=12795, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.37.2.59-13.28.2.33-10.33.2.60-13.49.2.31-10.12.pth, bkmy
BLEU = 8.31, 33.6/13.0/5.1/2.1 (BP=1.000, ratio=1.133, hyp_len=13855, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.38.2.48-11.97.2.26-9.57.2.57-13.00.2.32-10.18.pth, mybk
BLEU = 8.27, 31.1/11.4/5.2/2.6 (BP=1.000, ratio=1.102, hyp_len=12600, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.38.2.48-11.97.2.26-9.57.2.57-13.00.2.32-10.18.pth, bkmy
BLEU = 7.58, 32.2/12.3/4.7/1.8 (BP=1.000, ratio=1.177, hyp_len=14399, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.39.2.49-12.05.2.26-9.54.2.58-13.23.2.31-10.06.pth, mybk
BLEU = 8.02, 31.5/11.3/5.0/2.3 (BP=1.000, ratio=1.077, hyp_len=12315, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.39.2.49-12.05.2.26-9.54.2.58-13.23.2.31-10.06.pth, bkmy
BLEU = 9.53, 36.5/14.4/6.1/2.6 (BP=1.000, ratio=1.053, hyp_len=12878, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.40.2.45-11.55.2.20-9.06.2.58-13.20.2.31-10.12.pth, mybk
BLEU = 8.24, 31.6/11.5/5.2/2.4 (BP=1.000, ratio=1.115, hyp_len=12751, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.40.2.45-11.55.2.20-9.06.2.58-13.20.2.31-10.12.pth, bkmy
BLEU = 9.18, 35.7/14.2/5.9/2.4 (BP=1.000, ratio=1.079, hyp_len=13200, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.41.2.43-11.41.2.22-9.17.2.59-13.36.2.30-10.00.pth, mybk
BLEU = 8.60, 32.3/12.1/5.4/2.6 (BP=1.000, ratio=1.084, hyp_len=12390, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.41.2.43-11.41.2.22-9.17.2.59-13.36.2.30-10.00.pth, bkmy
BLEU = 9.14, 35.7/14.2/5.7/2.4 (BP=1.000, ratio=1.069, hyp_len=13071, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.42.2.38-10.82.2.18-8.86.2.57-13.03.2.31-10.10.pth, mybk
BLEU = 8.91, 33.0/12.3/5.6/2.8 (BP=1.000, ratio=1.075, hyp_len=12290, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.42.2.38-10.82.2.18-8.86.2.57-13.03.2.31-10.10.pth, bkmy
BLEU = 8.47, 32.6/12.8/5.4/2.3 (BP=1.000, ratio=1.175, hyp_len=14368, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.43.2.38-10.75.2.17-8.78.2.58-13.25.2.30-10.01.pth, mybk
BLEU = 8.63, 32.5/12.2/5.5/2.6 (BP=1.000, ratio=1.104, hyp_len=12618, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.43.2.38-10.75.2.17-8.78.2.58-13.25.2.30-10.01.pth, bkmy
BLEU = 9.11, 35.6/13.9/5.8/2.4 (BP=1.000, ratio=1.088, hyp_len=13305, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.44.2.36-10.58.2.14-8.49.2.56-12.90.2.27-9.72.pth, mybk
BLEU = 9.14, 32.6/12.3/5.8/3.0 (BP=1.000, ratio=1.100, hyp_len=12574, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.44.2.36-10.58.2.14-8.49.2.56-12.90.2.27-9.72.pth, bkmy
BLEU = 9.76, 36.1/14.7/6.2/2.8 (BP=1.000, ratio=1.097, hyp_len=13418, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.45.2.40-11.02.2.16-8.64.2.56-12.92.2.29-9.86.pth, mybk
BLEU = 9.26, 33.2/12.7/5.9/3.0 (BP=1.000, ratio=1.094, hyp_len=12503, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.45.2.40-11.02.2.16-8.64.2.56-12.92.2.29-9.86.pth, bkmy
BLEU = 9.89, 34.8/14.7/6.4/2.9 (BP=1.000, ratio=1.145, hyp_len=14004, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.46.2.26-9.58.2.04-7.69.2.60-13.42.2.27-9.69.pth, mybk
BLEU = 8.04, 31.0/11.5/5.1/2.3 (BP=1.000, ratio=1.148, hyp_len=13122, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.46.2.26-9.58.2.04-7.69.2.60-13.42.2.27-9.69.pth, bkmy
BLEU = 10.40, 37.8/15.5/6.6/3.0 (BP=1.000, ratio=1.042, hyp_len=12744, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.47.2.27-9.70.2.06-7.88.2.56-12.90.2.26-9.62.pth, mybk
BLEU = 9.30, 33.7/12.8/5.9/2.9 (BP=1.000, ratio=1.081, hyp_len=12361, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.47.2.27-9.70.2.06-7.88.2.56-12.90.2.26-9.62.pth, bkmy
BLEU = 10.57, 38.0/15.7/6.9/3.0 (BP=1.000, ratio=1.060, hyp_len=12961, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.48.2.30-9.93.2.09-8.05.2.54-12.68.2.26-9.61.pth, mybk
BLEU = 9.32, 33.8/13.0/5.9/2.9 (BP=1.000, ratio=1.086, hyp_len=12419, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.48.2.30-9.93.2.09-8.05.2.54-12.68.2.26-9.61.pth, bkmy
BLEU = 9.03, 35.7/13.9/5.8/2.3 (BP=1.000, ratio=1.115, hyp_len=13632, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.49.2.27-9.70.2.04-7.68.2.56-12.99.2.26-9.62.pth, mybk
BLEU = 9.62, 34.1/13.3/6.2/3.1 (BP=1.000, ratio=1.076, hyp_len=12301, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.49.2.27-9.70.2.04-7.68.2.56-12.99.2.26-9.62.pth, bkmy
BLEU = 10.17, 37.1/15.4/6.5/2.9 (BP=1.000, ratio=1.084, hyp_len=13258, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.50.2.22-9.18.2.03-7.61.2.58-13.20.2.22-9.24.pth, mybk
BLEU = 9.65, 34.4/13.5/6.2/3.0 (BP=1.000, ratio=1.080, hyp_len=12342, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.50.2.22-9.18.2.03-7.61.2.58-13.20.2.22-9.24.pth, bkmy
BLEU = 10.79, 38.0/16.0/7.0/3.2 (BP=1.000, ratio=1.061, hyp_len=12980, ref_len=12231)
```

Best BLEU Score for my-bk, 50 epoch: 9.65  
Best BLEU Score for bk-my, 50 epoch: 10.79  

## Seq2Seq-DSL, my-bk, 60epoch

training

```
Epoch 1 - |param|=8.49e+02 |g_param|=4.11e+05 loss_x2y=4.9120e+00 ppl_x2y=135.90 loss_y2x=4.6857e+00 ppl_y2x=108.39 dual_loss=0.0000e+00
Validation X2Y - loss=4.0523e+00 ppl=57.53 best_loss=inf best_ppl=inf
Validation Y2X - loss=4.1398e+00 ppl=62.79 best_loss=inf best_ppl=inf
Epoch 2 - |param|=8.49e+02 |g_param|=3.90e+05 loss_x2y=4.4424e+00 ppl_x2y=84.98 loss_y2x=4.2252e+00 ppl_y2x=68.39 dual_loss=0.0000e+00
Validation X2Y - loss=3.8887e+00 ppl=48.85 best_loss=4.0523e+00 best_ppl=57.53
Validation Y2X - loss=3.8673e+00 ppl=47.81 best_loss=4.1398e+00 best_ppl=62.79
Epoch 3 - |param|=8.49e+02 |g_param|=2.79e+05 loss_x2y=4.3784e+00 ppl_x2y=79.71 loss_y2x=4.1715e+00 ppl_y2x=64.81 dual_loss=0.0000e+00
Validation X2Y - loss=3.8295e+00 ppl=46.04 best_loss=3.8887e+00 best_ppl=48.85
Validation Y2X - loss=3.7422e+00 ppl=42.19 best_loss=3.8673e+00 best_ppl=47.81
Epoch 4 - |param|=8.49e+02 |g_param|=2.47e+05 loss_x2y=4.3701e+00 ppl_x2y=79.06 loss_y2x=4.1503e+00 ppl_y2x=63.45 dual_loss=0.0000e+00
Validation X2Y - loss=3.8022e+00 ppl=44.80 best_loss=3.8295e+00 best_ppl=46.04
Validation Y2X - loss=3.7405e+00 ppl=42.12 best_loss=3.7422e+00 best_ppl=42.19
Epoch 5 - |param|=8.50e+02 |g_param|=2.24e+05 loss_x2y=4.2728e+00 ppl_x2y=71.72 loss_y2x=4.0816e+00 ppl_y2x=59.24 dual_loss=0.0000e+00
Validation X2Y - loss=3.8032e+00 ppl=44.85 best_loss=3.8022e+00 best_ppl=44.80
Validation Y2X - loss=3.7593e+00 ppl=42.92 best_loss=3.7405e+00 best_ppl=42.12
Epoch 6 - |param|=8.50e+02 |g_param|=2.38e+05 loss_x2y=4.3214e+00 ppl_x2y=75.29 loss_y2x=4.0972e+00 ppl_y2x=60.17 dual_loss=0.0000e+00
Validation X2Y - loss=3.7903e+00 ppl=44.27 best_loss=3.8022e+00 best_ppl=44.80
Validation Y2X - loss=3.7189e+00 ppl=41.22 best_loss=3.7405e+00 best_ppl=42.12
Epoch 7 - |param|=8.50e+02 |g_param|=2.35e+05 loss_x2y=4.2969e+00 ppl_x2y=73.47 loss_y2x=4.0977e+00 ppl_y2x=60.20 dual_loss=0.0000e+00
Validation X2Y - loss=3.7904e+00 ppl=44.27 best_loss=3.7903e+00 best_ppl=44.27
Validation Y2X - loss=3.6983e+00 ppl=40.38 best_loss=3.7189e+00 best_ppl=41.22
Epoch 8 - |param|=8.51e+02 |g_param|=2.23e+05 loss_x2y=4.2199e+00 ppl_x2y=68.02 loss_y2x=3.9969e+00 ppl_y2x=54.43 dual_loss=0.0000e+00
Validation X2Y - loss=3.7505e+00 ppl=42.54 best_loss=3.7903e+00 best_ppl=44.27
Validation Y2X - loss=3.6110e+00 ppl=37.00 best_loss=3.6983e+00 best_ppl=40.38
Epoch 9 - |param|=8.51e+02 |g_param|=1.90e+05 loss_x2y=4.1656e+00 ppl_x2y=64.43 loss_y2x=3.9059e+00 ppl_y2x=49.70 dual_loss=0.0000e+00
Validation X2Y - loss=3.6611e+00 ppl=38.90 best_loss=3.7505e+00 best_ppl=42.54
Validation Y2X - loss=3.4767e+00 ppl=32.35 best_loss=3.6110e+00 best_ppl=37.00
Epoch 10 - |param|=8.52e+02 |g_param|=1.84e+05 loss_x2y=4.0587e+00 ppl_x2y=57.90 loss_y2x=3.8054e+00 ppl_y2x=44.94 dual_loss=0.0000e+00
Validation X2Y - loss=3.4804e+00 ppl=32.47 best_loss=3.6611e+00 best_ppl=38.90
Validation Y2X - loss=3.3250e+00 ppl=27.80 best_loss=3.4767e+00 best_ppl=32.35
Epoch 11 - |param|=8.52e+02 |g_param|=1.60e+05 loss_x2y=3.8879e+00 ppl_x2y=48.81 loss_y2x=3.6298e+00 ppl_y2x=37.71 dual_loss=0.0000e+00
Validation X2Y - loss=3.3937e+00 ppl=29.78 best_loss=3.4804e+00 best_ppl=32.47
Validation Y2X - loss=3.1929e+00 ppl=24.36 best_loss=3.3250e+00 best_ppl=27.80
Epoch 12 - |param|=8.53e+02 |g_param|=1.58e+05 loss_x2y=3.7436e+00 ppl_x2y=42.25 loss_y2x=3.4953e+00 ppl_y2x=32.96 dual_loss=0.0000e+00
Validation X2Y - loss=3.2949e+00 ppl=26.98 best_loss=3.3937e+00 best_ppl=29.78
Validation Y2X - loss=3.0793e+00 ppl=21.74 best_loss=3.1929e+00 best_ppl=24.36
Epoch 13 - |param|=8.53e+02 |g_param|=1.67e+05 loss_x2y=3.7684e+00 ppl_x2y=43.31 loss_y2x=3.5110e+00 ppl_y2x=33.48 dual_loss=0.0000e+00
Validation X2Y - loss=3.2441e+00 ppl=25.64 best_loss=3.2949e+00 best_ppl=26.98
Validation Y2X - loss=3.0104e+00 ppl=20.29 best_loss=3.0793e+00 best_ppl=21.74
Epoch 14 - |param|=8.54e+02 |g_param|=1.58e+05 loss_x2y=3.5698e+00 ppl_x2y=35.51 loss_y2x=3.2945e+00 ppl_y2x=26.96 dual_loss=0.0000e+00
Validation X2Y - loss=3.1809e+00 ppl=24.07 best_loss=3.2441e+00 best_ppl=25.64
Validation Y2X - loss=2.9521e+00 ppl=19.15 best_loss=3.0104e+00 best_ppl=20.29
Epoch 15 - |param|=8.55e+02 |g_param|=1.61e+05 loss_x2y=3.6021e+00 ppl_x2y=36.67 loss_y2x=3.2995e+00 ppl_y2x=27.10 dual_loss=0.0000e+00
Validation X2Y - loss=3.1400e+00 ppl=23.10 best_loss=3.1809e+00 best_ppl=24.07
Validation Y2X - loss=2.9529e+00 ppl=19.16 best_loss=2.9521e+00 best_ppl=19.15
Epoch 16 - |param|=8.55e+02 |g_param|=1.60e+05 loss_x2y=3.4703e+00 ppl_x2y=32.15 loss_y2x=3.2160e+00 ppl_y2x=24.93 dual_loss=0.0000e+00
Validation X2Y - loss=3.0854e+00 ppl=21.88 best_loss=3.1400e+00 best_ppl=23.10
Validation Y2X - loss=2.8841e+00 ppl=17.89 best_loss=2.9521e+00 best_ppl=19.15
Epoch 17 - |param|=8.56e+02 |g_param|=1.61e+05 loss_x2y=3.4457e+00 ppl_x2y=31.36 loss_y2x=3.2004e+00 ppl_y2x=24.54 dual_loss=0.0000e+00
Validation X2Y - loss=3.0641e+00 ppl=21.41 best_loss=3.0854e+00 best_ppl=21.88
Validation Y2X - loss=2.8400e+00 ppl=17.12 best_loss=2.8841e+00 best_ppl=17.89
Epoch 18 - |param|=8.57e+02 |g_param|=1.68e+05 loss_x2y=3.4197e+00 ppl_x2y=30.56 loss_y2x=3.1250e+00 ppl_y2x=22.76 dual_loss=0.0000e+00
Validation X2Y - loss=3.0360e+00 ppl=20.82 best_loss=3.0641e+00 best_ppl=21.41
Validation Y2X - loss=2.8104e+00 ppl=16.62 best_loss=2.8400e+00 best_ppl=17.12
Epoch 19 - |param|=8.57e+02 |g_param|=1.59e+05 loss_x2y=3.2517e+00 ppl_x2y=25.83 loss_y2x=3.0289e+00 ppl_y2x=20.68 dual_loss=0.0000e+00
Validation X2Y - loss=2.9754e+00 ppl=19.60 best_loss=3.0360e+00 best_ppl=20.82
Validation Y2X - loss=2.7640e+00 ppl=15.86 best_loss=2.8104e+00 best_ppl=16.62
Epoch 20 - |param|=8.58e+02 |g_param|=1.63e+05 loss_x2y=3.2613e+00 ppl_x2y=26.08 loss_y2x=3.0222e+00 ppl_y2x=20.54 dual_loss=0.0000e+00
Validation X2Y - loss=2.9639e+00 ppl=19.37 best_loss=2.9754e+00 best_ppl=19.60
Validation Y2X - loss=2.7367e+00 ppl=15.44 best_loss=2.7640e+00 best_ppl=15.86
Epoch 21 - |param|=8.59e+02 |g_param|=1.84e+05 loss_x2y=3.2623e+00 ppl_x2y=26.11 loss_y2x=3.0524e+00 ppl_y2x=21.17 dual_loss=6.9092e-01
Validation X2Y - loss=2.9614e+00 ppl=19.33 best_loss=2.9639e+00 best_ppl=19.37
Validation Y2X - loss=2.7631e+00 ppl=15.85 best_loss=2.7367e+00 best_ppl=15.44
Epoch 22 - |param|=8.60e+02 |g_param|=1.70e+05 loss_x2y=3.1928e+00 ppl_x2y=24.36 loss_y2x=2.9834e+00 ppl_y2x=19.76 dual_loss=5.6411e-01
Validation X2Y - loss=2.8696e+00 ppl=17.63 best_loss=2.9614e+00 best_ppl=19.33
Validation Y2X - loss=2.6733e+00 ppl=14.49 best_loss=2.7367e+00 best_ppl=15.44
Epoch 23 - |param|=8.60e+02 |g_param|=1.78e+05 loss_x2y=3.1128e+00 ppl_x2y=22.48 loss_y2x=2.9183e+00 ppl_y2x=18.51 dual_loss=5.5549e-01
Validation X2Y - loss=2.8742e+00 ppl=17.71 best_loss=2.8696e+00 best_ppl=17.63
Validation Y2X - loss=2.6526e+00 ppl=14.19 best_loss=2.6733e+00 best_ppl=14.49
Epoch 24 - |param|=8.61e+02 |g_param|=1.84e+05 loss_x2y=3.0823e+00 ppl_x2y=21.81 loss_y2x=2.8894e+00 ppl_y2x=17.98 dual_loss=5.6230e-01
Validation X2Y - loss=2.8624e+00 ppl=17.50 best_loss=2.8696e+00 best_ppl=17.63
Validation Y2X - loss=2.6463e+00 ppl=14.10 best_loss=2.6526e+00 best_ppl=14.19
Epoch 25 - |param|=8.62e+02 |g_param|=1.74e+05 loss_x2y=3.0394e+00 ppl_x2y=20.89 loss_y2x=2.8299e+00 ppl_y2x=16.94 dual_loss=4.4485e-01
Validation X2Y - loss=2.8188e+00 ppl=16.76 best_loss=2.8624e+00 best_ppl=17.50
Validation Y2X - loss=2.6166e+00 ppl=13.69 best_loss=2.6463e+00 best_ppl=14.10
Epoch 26 - |param|=8.62e+02 |g_param|=1.83e+05 loss_x2y=3.0741e+00 ppl_x2y=21.63 loss_y2x=2.9021e+00 ppl_y2x=18.21 dual_loss=5.5286e-01
Validation X2Y - loss=2.8026e+00 ppl=16.49 best_loss=2.8188e+00 best_ppl=16.76
Validation Y2X - loss=2.6109e+00 ppl=13.61 best_loss=2.6166e+00 best_ppl=13.69
Epoch 27 - |param|=8.63e+02 |g_param|=1.74e+05 loss_x2y=2.9653e+00 ppl_x2y=19.40 loss_y2x=2.7711e+00 ppl_y2x=15.98 dual_loss=4.5627e-01
Validation X2Y - loss=2.7538e+00 ppl=15.70 best_loss=2.8026e+00 best_ppl=16.49
Validation Y2X - loss=2.5542e+00 ppl=12.86 best_loss=2.6109e+00 best_ppl=13.61
Epoch 28 - |param|=8.64e+02 |g_param|=1.86e+05 loss_x2y=2.8824e+00 ppl_x2y=17.86 loss_y2x=2.6831e+00 ppl_y2x=14.63 dual_loss=4.0043e-01
Validation X2Y - loss=2.7832e+00 ppl=16.17 best_loss=2.7538e+00 best_ppl=15.70
Validation Y2X - loss=2.5238e+00 ppl=12.48 best_loss=2.5542e+00 best_ppl=12.86
Epoch 29 - |param|=8.64e+02 |g_param|=2.01e+05 loss_x2y=2.9694e+00 ppl_x2y=19.48 loss_y2x=2.7230e+00 ppl_y2x=15.23 dual_loss=4.2738e-01
Validation X2Y - loss=2.7173e+00 ppl=15.14 best_loss=2.7538e+00 best_ppl=15.70
Validation Y2X - loss=2.5074e+00 ppl=12.27 best_loss=2.5238e+00 best_ppl=12.48
Epoch 30 - |param|=8.65e+02 |g_param|=1.93e+05 loss_x2y=2.8446e+00 ppl_x2y=17.19 loss_y2x=2.6755e+00 ppl_y2x=14.52 dual_loss=4.0864e-01
Validation X2Y - loss=2.7457e+00 ppl=15.58 best_loss=2.7173e+00 best_ppl=15.14
Validation Y2X - loss=2.5049e+00 ppl=12.24 best_loss=2.5074e+00 best_ppl=12.27
Epoch 31 - |param|=8.66e+02 |g_param|=1.92e+05 loss_x2y=2.7623e+00 ppl_x2y=15.84 loss_y2x=2.5730e+00 ppl_y2x=13.10 dual_loss=3.7300e-01
Validation X2Y - loss=2.6980e+00 ppl=14.85 best_loss=2.7173e+00 best_ppl=15.14
Validation Y2X - loss=2.4732e+00 ppl=11.86 best_loss=2.5049e+00 best_ppl=12.24
Epoch 32 - |param|=8.66e+02 |g_param|=2.02e+05 loss_x2y=2.7974e+00 ppl_x2y=16.40 loss_y2x=2.5902e+00 ppl_y2x=13.33 dual_loss=3.7479e-01
Validation X2Y - loss=2.6857e+00 ppl=14.67 best_loss=2.6980e+00 best_ppl=14.85
Validation Y2X - loss=2.4585e+00 ppl=11.69 best_loss=2.4732e+00 best_ppl=11.86
Epoch 33 - |param|=8.67e+02 |g_param|=1.98e+05 loss_x2y=2.7534e+00 ppl_x2y=15.70 loss_y2x=2.5769e+00 ppl_y2x=13.16 dual_loss=3.7751e-01
Validation X2Y - loss=2.6726e+00 ppl=14.48 best_loss=2.6857e+00 best_ppl=14.67
Validation Y2X - loss=2.4500e+00 ppl=11.59 best_loss=2.4585e+00 best_ppl=11.69
Epoch 34 - |param|=8.68e+02 |g_param|=2.65e+05 loss_x2y=2.7156e+00 ppl_x2y=15.11 loss_y2x=2.5359e+00 ppl_y2x=12.63 dual_loss=3.5111e-01
Validation X2Y - loss=2.6798e+00 ppl=14.58 best_loss=2.6726e+00 best_ppl=14.48
Validation Y2X - loss=2.4507e+00 ppl=11.60 best_loss=2.4500e+00 best_ppl=11.59
Epoch 35 - |param|=8.68e+02 |g_param|=2.72e+05 loss_x2y=2.7007e+00 ppl_x2y=14.89 loss_y2x=2.5588e+00 ppl_y2x=12.92 dual_loss=3.8949e-01
Validation X2Y - loss=2.6656e+00 ppl=14.38 best_loss=2.6726e+00 best_ppl=14.48
Validation Y2X - loss=2.4350e+00 ppl=11.42 best_loss=2.4500e+00 best_ppl=11.59
Epoch 36 - |param|=8.69e+02 |g_param|=4.03e+05 loss_x2y=2.6375e+00 ppl_x2y=13.98 loss_y2x=2.4640e+00 ppl_y2x=11.75 dual_loss=3.3514e-01
Validation X2Y - loss=2.6408e+00 ppl=14.02 best_loss=2.6656e+00 best_ppl=14.38
Validation Y2X - loss=2.4132e+00 ppl=11.17 best_loss=2.4350e+00 best_ppl=11.42
Epoch 37 - |param|=8.70e+02 |g_param|=3.95e+05 loss_x2y=2.5747e+00 ppl_x2y=13.13 loss_y2x=2.3947e+00 ppl_y2x=10.96 dual_loss=3.2415e-01
Validation X2Y - loss=2.6410e+00 ppl=14.03 best_loss=2.6408e+00 best_ppl=14.02
Validation Y2X - loss=2.4372e+00 ppl=11.44 best_loss=2.4132e+00 best_ppl=11.17
Epoch 38 - |param|=8.70e+02 |g_param|=4.69e+05 loss_x2y=2.6501e+00 ppl_x2y=14.16 loss_y2x=2.4123e+00 ppl_y2x=11.16 dual_loss=3.3705e-01
Validation X2Y - loss=2.6475e+00 ppl=14.12 best_loss=2.6408e+00 best_ppl=14.02
Validation Y2X - loss=2.4332e+00 ppl=11.39 best_loss=2.4132e+00 best_ppl=11.17
Epoch 39 - |param|=8.71e+02 |g_param|=4.66e+05 loss_x2y=2.6390e+00 ppl_x2y=14.00 loss_y2x=2.5047e+00 ppl_y2x=12.24 dual_loss=4.0229e-01
Validation X2Y - loss=2.6243e+00 ppl=13.79 best_loss=2.6408e+00 best_ppl=14.02
Validation Y2X - loss=2.3937e+00 ppl=10.95 best_loss=2.4132e+00 best_ppl=11.17
Epoch 40 - |param|=8.72e+02 |g_param|=4.31e+05 loss_x2y=2.4828e+00 ppl_x2y=11.97 loss_y2x=2.3335e+00 ppl_y2x=10.31 dual_loss=3.1128e-01
Validation X2Y - loss=2.6252e+00 ppl=13.81 best_loss=2.6243e+00 best_ppl=13.79
Validation Y2X - loss=2.3833e+00 ppl=10.84 best_loss=2.3937e+00 best_ppl=10.95
Epoch 41 - |param|=8.72e+02 |g_param|=4.32e+05 loss_x2y=2.4587e+00 ppl_x2y=11.69 loss_y2x=2.3042e+00 ppl_y2x=10.02 dual_loss=3.1680e-01
Validation X2Y - loss=2.6338e+00 ppl=13.93 best_loss=2.6243e+00 best_ppl=13.79
Validation Y2X - loss=2.4034e+00 ppl=11.06 best_loss=2.3833e+00 best_ppl=10.84
Epoch 42 - |param|=8.73e+02 |g_param|=4.44e+05 loss_x2y=2.4429e+00 ppl_x2y=11.51 loss_y2x=2.3080e+00 ppl_y2x=10.05 dual_loss=3.0595e-01
Validation X2Y - loss=2.6218e+00 ppl=13.76 best_loss=2.6243e+00 best_ppl=13.79
Validation Y2X - loss=2.3740e+00 ppl=10.74 best_loss=2.3833e+00 best_ppl=10.84
Epoch 43 - |param|=8.74e+02 |g_param|=4.42e+05 loss_x2y=2.4420e+00 ppl_x2y=11.50 loss_y2x=2.2761e+00 ppl_y2x=9.74 dual_loss=3.0837e-01
Validation X2Y - loss=2.6187e+00 ppl=13.72 best_loss=2.6218e+00 best_ppl=13.76
Validation Y2X - loss=2.3848e+00 ppl=10.86 best_loss=2.3740e+00 best_ppl=10.74
Epoch 44 - |param|=8.74e+02 |g_param|=4.98e+05 loss_x2y=2.4552e+00 ppl_x2y=11.65 loss_y2x=2.2595e+00 ppl_y2x=9.58 dual_loss=3.0877e-01
Validation X2Y - loss=2.6023e+00 ppl=13.49 best_loss=2.6187e+00 best_ppl=13.72
Validation Y2X - loss=2.3771e+00 ppl=10.77 best_loss=2.3740e+00 best_ppl=10.74
Epoch 45 - |param|=8.75e+02 |g_param|=4.44e+05 loss_x2y=2.4027e+00 ppl_x2y=11.05 loss_y2x=2.2281e+00 ppl_y2x=9.28 dual_loss=3.1805e-01
Validation X2Y - loss=2.6347e+00 ppl=13.94 best_loss=2.6023e+00 best_ppl=13.49
Validation Y2X - loss=2.3777e+00 ppl=10.78 best_loss=2.3740e+00 best_ppl=10.74
Epoch 46 - |param|=8.75e+02 |g_param|=4.55e+05 loss_x2y=2.3348e+00 ppl_x2y=10.33 loss_y2x=2.1857e+00 ppl_y2x=8.90 dual_loss=2.9720e-01
Validation X2Y - loss=2.6088e+00 ppl=13.58 best_loss=2.6023e+00 best_ppl=13.49
Validation Y2X - loss=2.3505e+00 ppl=10.49 best_loss=2.3740e+00 best_ppl=10.74
Epoch 47 - |param|=8.76e+02 |g_param|=4.61e+05 loss_x2y=2.3742e+00 ppl_x2y=10.74 loss_y2x=2.1892e+00 ppl_y2x=8.93 dual_loss=3.0180e-01
Validation X2Y - loss=2.6443e+00 ppl=14.07 best_loss=2.6023e+00 best_ppl=13.49
Validation Y2X - loss=2.3523e+00 ppl=10.51 best_loss=2.3505e+00 best_ppl=10.49
Epoch 48 - |param|=8.77e+02 |g_param|=4.97e+05 loss_x2y=2.2573e+00 ppl_x2y=9.56 loss_y2x=2.1252e+00 ppl_y2x=8.37 dual_loss=3.0301e-01
Validation X2Y - loss=2.5905e+00 ppl=13.34 best_loss=2.6023e+00 best_ppl=13.49
Validation Y2X - loss=2.3515e+00 ppl=10.50 best_loss=2.3505e+00 best_ppl=10.49
Epoch 49 - |param|=8.77e+02 |g_param|=4.67e+05 loss_x2y=2.2383e+00 ppl_x2y=9.38 loss_y2x=2.0840e+00 ppl_y2x=8.04 dual_loss=2.9164e-01
Validation X2Y - loss=2.6274e+00 ppl=13.84 best_loss=2.5905e+00 best_ppl=13.34
Validation Y2X - loss=2.3697e+00 ppl=10.69 best_loss=2.3505e+00 best_ppl=10.49
Epoch 50 - |param|=8.78e+02 |g_param|=5.09e+05 loss_x2y=2.2459e+00 ppl_x2y=9.45 loss_y2x=2.0958e+00 ppl_y2x=8.13 dual_loss=2.9737e-01
Validation X2Y - loss=2.6440e+00 ppl=14.07 best_loss=2.5905e+00 best_ppl=13.34
Validation Y2X - loss=2.3435e+00 ppl=10.42 best_loss=2.3505e+00 best_ppl=10.49
Epoch 51 - |param|=8.78e+02 |g_param|=5.08e+05 loss_x2y=2.2647e+00 ppl_x2y=9.63 loss_y2x=2.1148e+00 ppl_y2x=8.29 dual_loss=3.1580e-01
Validation X2Y - loss=2.6455e+00 ppl=14.09 best_loss=2.5905e+00 best_ppl=13.34
Validation Y2X - loss=2.3544e+00 ppl=10.53 best_loss=2.3435e+00 best_ppl=10.42
Epoch 52 - |param|=8.79e+02 |g_param|=4.95e+05 loss_x2y=2.2138e+00 ppl_x2y=9.15 loss_y2x=2.0865e+00 ppl_y2x=8.06 dual_loss=2.9964e-01
Validation X2Y - loss=2.6418e+00 ppl=14.04 best_loss=2.5905e+00 best_ppl=13.34
Validation Y2X - loss=2.3200e+00 ppl=10.18 best_loss=2.3435e+00 best_ppl=10.42
Epoch 53 - |param|=8.80e+02 |g_param|=4.87e+05 loss_x2y=2.1613e+00 ppl_x2y=8.68 loss_y2x=2.0160e+00 ppl_y2x=7.51 dual_loss=2.8476e-01
Validation X2Y - loss=2.6212e+00 ppl=13.75 best_loss=2.5905e+00 best_ppl=13.34
Validation Y2X - loss=2.3515e+00 ppl=10.50 best_loss=2.3200e+00 best_ppl=10.18
Epoch 54 - |param|=8.80e+02 |g_param|=5.26e+05 loss_x2y=2.1003e+00 ppl_x2y=8.17 loss_y2x=1.9627e+00 ppl_y2x=7.12 dual_loss=2.8450e-01
Validation X2Y - loss=2.6518e+00 ppl=14.18 best_loss=2.5905e+00 best_ppl=13.34
Validation Y2X - loss=2.3613e+00 ppl=10.60 best_loss=2.3200e+00 best_ppl=10.18
Epoch 55 - |param|=8.81e+02 |g_param|=5.05e+05 loss_x2y=2.1703e+00 ppl_x2y=8.76 loss_y2x=2.0185e+00 ppl_y2x=7.53 dual_loss=3.1688e-01
Validation X2Y - loss=2.6391e+00 ppl=14.00 best_loss=2.5905e+00 best_ppl=13.34
Validation Y2X - loss=2.3476e+00 ppl=10.46 best_loss=2.3200e+00 best_ppl=10.18
Epoch 56 - |param|=8.81e+02 |g_param|=5.20e+05 loss_x2y=2.0940e+00 ppl_x2y=8.12 loss_y2x=1.9637e+00 ppl_y2x=7.13 dual_loss=2.9941e-01
Validation X2Y - loss=2.6326e+00 ppl=13.91 best_loss=2.5905e+00 best_ppl=13.34
Validation Y2X - loss=2.3381e+00 ppl=10.36 best_loss=2.3200e+00 best_ppl=10.18
Epoch 57 - |param|=8.82e+02 |g_param|=5.14e+05 loss_x2y=2.1029e+00 ppl_x2y=8.19 loss_y2x=1.9485e+00 ppl_y2x=7.02 dual_loss=2.9646e-01
Validation X2Y - loss=2.6603e+00 ppl=14.30 best_loss=2.5905e+00 best_ppl=13.34
Validation Y2X - loss=2.3387e+00 ppl=10.37 best_loss=2.3200e+00 best_ppl=10.18
Epoch 58 - |param|=8.82e+02 |g_param|=5.47e+05 loss_x2y=2.0383e+00 ppl_x2y=7.68 loss_y2x=1.8890e+00 ppl_y2x=6.61 dual_loss=2.8445e-01
Validation X2Y - loss=2.6441e+00 ppl=14.07 best_loss=2.5905e+00 best_ppl=13.34
Validation Y2X - loss=2.3362e+00 ppl=10.34 best_loss=2.3200e+00 best_ppl=10.18
Epoch 59 - |param|=8.83e+02 |g_param|=5.06e+05 loss_x2y=2.0133e+00 ppl_x2y=7.49 loss_y2x=1.8587e+00 ppl_y2x=6.42 dual_loss=2.7783e-01
Validation X2Y - loss=2.6486e+00 ppl=14.13 best_loss=2.5905e+00 best_ppl=13.34
Validation Y2X - loss=2.3311e+00 ppl=10.29 best_loss=2.3200e+00 best_ppl=10.18
Epoch 60 - |param|=8.84e+02 |g_param|=5.24e+05 loss_x2y=1.9889e+00 ppl_x2y=7.31 loss_y2x=1.8542e+00 ppl_y2x=6.39 dual_loss=2.9038e-01
Validation X2Y - loss=2.6508e+00 ppl=14.17 best_loss=2.5905e+00 best_ppl=13.34
Validation Y2X - loss=2.3429e+00 ppl=10.41 best_loss=2.3200e+00 best_ppl=10.18
```

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/mybk-60epoch
Evaluation result for the model: dsl-model-mybk.01.4.91-135.90.4.69-108.39.4.05-57.53.4.14-62.79.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.9/0.0/0.0/0.0 (BP=0.646, ratio=0.696, hyp_len=7956, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.91-135.90.4.69-108.39.4.05-57.53.4.14-62.79.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.4/0.5/0.0/0.0 (BP=0.999, ratio=0.999, hyp_len=12216, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.02.4.44-84.98.4.23-68.39.3.89-48.85.3.87-47.81.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.1/0.1/0.0/0.0 (BP=0.982, ratio=0.982, hyp_len=11231, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.4.44-84.98.4.23-68.39.3.89-48.85.3.87-47.81.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.7/1.0/0.1/0.0 (BP=1.000, ratio=1.004, hyp_len=12281, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.4.38-79.71.4.17-64.81.3.83-46.04.3.74-42.19.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.4/0.3/0.0/0.0 (BP=0.959, ratio=0.960, hyp_len=10978, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.4.38-79.71.4.17-64.81.3.83-46.04.3.74-42.19.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.9/2.2/0.4/0.0 (BP=0.928, ratio=0.931, hyp_len=11384, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.4.37-79.06.4.15-63.45.3.80-44.80.3.74-42.12.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.0/0.1/0.0/0.0 (BP=0.916, ratio=0.919, hyp_len=10510, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.4.37-79.06.4.15-63.45.3.80-44.80.3.74-42.12.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.3/2.1/0.4/0.0 (BP=0.961, ratio=0.961, hyp_len=11758, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.4.27-71.72.4.08-59.24.3.80-44.85.3.76-42.92.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.0/0.3/0.0/0.0 (BP=1.000, ratio=1.000, hyp_len=11434, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.4.27-71.72.4.08-59.24.3.80-44.85.3.76-42.92.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.8/0.5/0.0/0.0 (BP=0.996, ratio=0.996, hyp_len=12177, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.4.32-75.29.4.10-60.17.3.79-44.27.3.72-41.22.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.5/0.2/0.0/0.0 (BP=1.000, ratio=1.008, hyp_len=11522, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.4.32-75.29.4.10-60.17.3.79-44.27.3.72-41.22.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.4/2.0/0.3/0.0 (BP=1.000, ratio=1.008, hyp_len=12330, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.4.30-73.47.4.10-60.20.3.79-44.27.3.70-40.38.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.0/0.3/0.0/0.0 (BP=0.985, ratio=0.985, hyp_len=11257, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.4.30-73.47.4.10-60.20.3.79-44.27.3.70-40.38.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.6/0.9/0.0/0.0 (BP=1.000, ratio=1.009, hyp_len=12345, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.4.22-68.02.4.00-54.43.3.75-42.54.3.61-37.00.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.5/0.9/0.0/0.0 (BP=1.000, ratio=1.052, hyp_len=12032, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.4.22-68.02.4.00-54.43.3.75-42.54.3.61-37.00.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.0/1.2/0.0/0.0 (BP=1.000, ratio=1.000, hyp_len=12231, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.4.17-64.43.3.91-49.70.3.66-38.90.3.48-32.35.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.4/0.6/0.0/0.0 (BP=0.884, ratio=0.890, hyp_len=10174, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.4.17-64.43.3.91-49.70.3.66-38.90.3.48-32.35.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 22.3/2.3/0.1/0.0 (BP=0.979, ratio=0.979, hyp_len=11973, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.4.06-57.90.3.81-44.94.3.48-32.47.3.33-27.80.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 26.1/2.5/0.3/0.0 (BP=0.732, ratio=0.762, hyp_len=8710, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.4.06-57.90.3.81-44.94.3.48-32.47.3.33-27.80.pth, bkmy
BLEU = 1.13, 23.9/4.4/0.5/0.0 (BP=0.981, ratio=0.981, hyp_len=11996, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.3.89-48.81.3.63-37.71.3.39-29.78.3.19-24.36.pth, mybk
BLEU = 0.78, 23.0/3.8/0.4/0.0 (BP=1.000, ratio=1.030, hyp_len=11775, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.3.89-48.81.3.63-37.71.3.39-29.78.3.19-24.36.pth, bkmy
BLEU = 0.05, 1.5/0.3/0.0/0.0 (BP=1.000, ratio=12.053, hyp_len=147426, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.3.74-42.25.3.50-32.96.3.29-26.98.3.08-21.74.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.6/3.7/0.4/0.0 (BP=1.000, ratio=1.131, hyp_len=12925, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.3.74-42.25.3.50-32.96.3.29-26.98.3.08-21.74.pth, bkmy
BLEU = 0.10, 1.8/0.3/0.0/0.0 (BP=1.000, ratio=10.865, hyp_len=132892, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.3.77-43.31.3.51-33.48.3.24-25.64.3.01-20.29.pth, mybk
BLEU = 1.89, 22.7/5.6/1.0/0.1 (BP=1.000, ratio=1.072, hyp_len=12253, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.3.77-43.31.3.51-33.48.3.24-25.64.3.01-20.29.pth, bkmy
BLEU = 0.31, 4.9/0.9/0.1/0.0 (BP=1.000, ratio=5.182, hyp_len=63387, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.3.57-35.51.3.29-26.96.3.18-24.07.2.95-19.15.pth, mybk
BLEU = 3.88, 23.8/6.5/2.0/0.7 (BP=1.000, ratio=1.047, hyp_len=11965, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.3.57-35.51.3.29-26.96.3.18-24.07.2.95-19.15.pth, bkmy
BLEU = 0.10, 1.6/0.4/0.0/0.0 (BP=1.000, ratio=12.100, hyp_len=148000, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.3.60-36.67.3.30-27.10.3.14-23.10.2.95-19.16.pth, mybk
BLEU = 3.91, 22.6/6.2/2.0/0.8 (BP=1.000, ratio=1.149, hyp_len=13139, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.3.60-36.67.3.30-27.10.3.14-23.10.2.95-19.16.pth, bkmy
BLEU = 0.09, 0.8/0.2/0.0/0.0 (BP=1.000, ratio=20.927, hyp_len=255960, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.3.47-32.15.3.22-24.93.3.09-21.88.2.88-17.89.pth, mybk
BLEU = 3.62, 21.2/5.8/1.9/0.7 (BP=1.000, ratio=1.254, hyp_len=14336, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.3.47-32.15.3.22-24.93.3.09-21.88.2.88-17.89.pth, bkmy
BLEU = 0.90, 6.1/2.0/0.5/0.1 (BP=1.000, ratio=4.905, hyp_len=59996, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.3.45-31.36.3.20-24.54.3.06-21.41.2.84-17.12.pth, mybk
BLEU = 3.14, 18.1/5.0/1.7/0.6 (BP=1.000, ratio=1.459, hyp_len=16682, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.3.45-31.36.3.20-24.54.3.06-21.41.2.84-17.12.pth, bkmy
BLEU = 0.68, 3.9/1.4/0.4/0.1 (BP=1.000, ratio=7.537, hyp_len=92190, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.3.42-30.56.3.13-22.76.3.04-20.82.2.81-16.62.pth, mybk
BLEU = 3.65, 19.5/5.6/2.1/0.8 (BP=1.000, ratio=1.378, hyp_len=15748, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.3.42-30.56.3.13-22.76.3.04-20.82.2.81-16.62.pth, bkmy
BLEU = 4.62, 26.7/9.6/2.8/0.6 (BP=1.000, ratio=1.225, hyp_len=14986, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.3.25-25.83.3.03-20.68.2.98-19.60.2.76-15.86.pth, mybk
BLEU = 4.24, 23.0/6.8/2.4/0.9 (BP=1.000, ratio=1.194, hyp_len=13645, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.3.25-25.83.3.03-20.68.2.98-19.60.2.76-15.86.pth, bkmy
BLEU = 5.85, 31.3/11.5/3.5/0.9 (BP=1.000, ratio=1.062, hyp_len=12991, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.3.26-26.08.3.02-20.54.2.96-19.37.2.74-15.44.pth, mybk
BLEU = 3.58, 20.0/5.7/2.0/0.7 (BP=1.000, ratio=1.349, hyp_len=15420, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.3.26-26.08.3.02-20.54.2.96-19.37.2.74-15.44.pth, bkmy
BLEU = 5.71, 31.1/11.1/3.4/0.9 (BP=1.000, ratio=1.089, hyp_len=13321, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.3.26-26.11.3.05-21.17.2.96-19.33.2.76-15.85.pth, mybk
BLEU = 2.33, 12.5/3.7/1.4/0.5 (BP=1.000, ratio=2.139, hyp_len=24458, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.3.26-26.11.3.05-21.17.2.96-19.33.2.76-15.85.pth, bkmy
BLEU = 3.03, 17.3/6.0/1.7/0.5 (BP=1.000, ratio=1.938, hyp_len=23701, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.3.19-24.36.2.98-19.76.2.87-17.63.2.67-14.49.pth, mybk
BLEU = 4.97, 24.3/7.6/2.9/1.1 (BP=1.000, ratio=1.152, hyp_len=13168, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.3.19-24.36.2.98-19.76.2.87-17.63.2.67-14.49.pth, bkmy
BLEU = 6.31, 31.3/11.4/3.7/1.2 (BP=1.000, ratio=1.094, hyp_len=13377, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.3.11-22.48.2.92-18.51.2.87-17.71.2.65-14.19.pth, mybk
BLEU = 2.53, 13.2/4.0/1.5/0.5 (BP=1.000, ratio=2.135, hyp_len=24405, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.3.11-22.48.2.92-18.51.2.87-17.71.2.65-14.19.pth, bkmy
BLEU = 6.88, 33.7/12.5/4.2/1.3 (BP=1.000, ratio=1.025, hyp_len=12537, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.3.08-21.81.2.89-17.98.2.86-17.50.2.65-14.10.pth, mybk
BLEU = 2.56, 12.4/4.0/1.5/0.6 (BP=1.000, ratio=2.282, hyp_len=26083, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.3.08-21.81.2.89-17.98.2.86-17.50.2.65-14.10.pth, bkmy
BLEU = 6.67, 32.4/11.9/4.0/1.3 (BP=1.000, ratio=1.092, hyp_len=13360, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.3.04-20.89.2.83-16.94.2.82-16.76.2.62-13.69.pth, mybk
BLEU = 3.40, 16.4/5.3/2.0/0.8 (BP=1.000, ratio=1.728, hyp_len=19751, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.3.04-20.89.2.83-16.94.2.82-16.76.2.62-13.69.pth, bkmy
BLEU = 5.17, 24.2/8.8/3.0/1.1 (BP=1.000, ratio=1.439, hyp_len=17602, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.3.07-21.63.2.90-18.21.2.80-16.49.2.61-13.61.pth, mybk
BLEU = 5.02, 23.2/7.5/3.0/1.2 (BP=1.000, ratio=1.280, hyp_len=14628, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.3.07-21.63.2.90-18.21.2.80-16.49.2.61-13.61.pth, bkmy
BLEU = 4.63, 21.2/7.9/2.8/1.0 (BP=1.000, ratio=1.693, hyp_len=20704, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.2.97-19.40.2.77-15.98.2.75-15.70.2.55-12.86.pth, mybk
BLEU = 6.07, 27.0/9.1/3.8/1.5 (BP=1.000, ratio=1.106, hyp_len=12642, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.2.97-19.40.2.77-15.98.2.75-15.70.2.55-12.86.pth, bkmy
BLEU = 5.27, 23.3/8.8/3.2/1.2 (BP=1.000, ratio=1.522, hyp_len=18619, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.2.88-17.86.2.68-14.63.2.78-16.17.2.52-12.48.pth, mybk
BLEU = 4.81, 22.1/7.1/2.9/1.2 (BP=1.000, ratio=1.383, hyp_len=15806, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.2.88-17.86.2.68-14.63.2.78-16.17.2.52-12.48.pth, bkmy
BLEU = 7.12, 30.1/11.8/4.4/1.7 (BP=1.000, ratio=1.203, hyp_len=14715, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.2.97-19.48.2.72-15.23.2.72-15.14.2.51-12.27.pth, mybk
BLEU = 4.31, 19.6/6.5/2.6/1.0 (BP=1.000, ratio=1.552, hyp_len=17741, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.2.97-19.48.2.72-15.23.2.72-15.14.2.51-12.27.pth, bkmy
BLEU = 8.38, 35.0/13.6/5.2/2.0 (BP=1.000, ratio=1.024, hyp_len=12528, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.2.84-17.19.2.68-14.52.2.75-15.58.2.50-12.24.pth, mybk
BLEU = 4.45, 20.9/6.7/2.7/1.0 (BP=1.000, ratio=1.487, hyp_len=17002, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.2.84-17.19.2.68-14.52.2.75-15.58.2.50-12.24.pth, bkmy
BLEU = 6.07, 26.5/9.9/3.7/1.4 (BP=1.000, ratio=1.348, hyp_len=16489, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.31.2.76-15.84.2.57-13.10.2.70-14.85.2.47-11.86.pth, mybk
BLEU = 6.70, 28.6/9.9/4.2/1.7 (BP=1.000, ratio=1.125, hyp_len=12860, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.31.2.76-15.84.2.57-13.10.2.70-14.85.2.47-11.86.pth, bkmy
BLEU = 5.78, 24.3/9.4/3.5/1.4 (BP=1.000, ratio=1.508, hyp_len=18450, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.32.2.80-16.40.2.59-13.33.2.69-14.67.2.46-11.69.pth, mybk
BLEU = 6.84, 28.4/9.7/4.3/1.9 (BP=1.000, ratio=1.112, hyp_len=12707, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.32.2.80-16.40.2.59-13.33.2.69-14.67.2.46-11.69.pth, bkmy
BLEU = 8.44, 34.4/13.5/5.3/2.1 (BP=1.000, ratio=1.059, hyp_len=12958, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.33.2.75-15.70.2.58-13.16.2.67-14.48.2.45-11.59.pth, mybk
BLEU = 6.88, 28.8/10.0/4.2/1.8 (BP=1.000, ratio=1.114, hyp_len=12730, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.33.2.75-15.70.2.58-13.16.2.67-14.48.2.45-11.59.pth, bkmy
BLEU = 4.67, 19.5/7.6/2.9/1.1 (BP=1.000, ratio=1.870, hyp_len=22868, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.34.2.72-15.11.2.54-12.63.2.68-14.58.2.45-11.60.pth, mybk
BLEU = 6.96, 29.4/10.4/4.3/1.8 (BP=1.000, ratio=1.132, hyp_len=12945, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.34.2.72-15.11.2.54-12.63.2.68-14.58.2.45-11.60.pth, bkmy
BLEU = 5.74, 24.6/9.5/3.6/1.3 (BP=1.000, ratio=1.481, hyp_len=18119, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.35.2.70-14.89.2.56-12.92.2.67-14.38.2.43-11.42.pth, mybk
BLEU = 7.33, 29.6/10.6/4.5/2.1 (BP=1.000, ratio=1.107, hyp_len=12654, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.35.2.70-14.89.2.56-12.92.2.67-14.38.2.43-11.42.pth, bkmy
BLEU = 8.00, 32.0/12.6/5.0/2.0 (BP=1.000, ratio=1.152, hyp_len=14084, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.36.2.64-13.98.2.46-11.75.2.64-14.02.2.41-11.17.pth, mybk
BLEU = 7.46, 29.9/10.8/4.6/2.1 (BP=1.000, ratio=1.119, hyp_len=12791, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.36.2.64-13.98.2.46-11.75.2.64-14.02.2.41-11.17.pth, bkmy
BLEU = 8.44, 34.3/13.2/5.2/2.2 (BP=1.000, ratio=1.090, hyp_len=13333, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.37.2.57-13.13.2.39-10.96.2.64-14.03.2.44-11.44.pth, mybk
BLEU = 7.92, 30.8/11.3/4.9/2.3 (BP=1.000, ratio=1.094, hyp_len=12501, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.37.2.57-13.13.2.39-10.96.2.64-14.03.2.44-11.44.pth, bkmy
BLEU = 8.44, 34.6/13.5/5.3/2.1 (BP=1.000, ratio=1.089, hyp_len=13323, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.38.2.65-14.16.2.41-11.16.2.65-14.12.2.43-11.39.pth, mybk
BLEU = 7.69, 30.2/10.9/4.8/2.2 (BP=1.000, ratio=1.104, hyp_len=12623, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.38.2.65-14.16.2.41-11.16.2.65-14.12.2.43-11.39.pth, bkmy
BLEU = 8.73, 34.7/13.7/5.5/2.2 (BP=1.000, ratio=1.087, hyp_len=13297, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.39.2.64-14.00.2.50-12.24.2.62-13.79.2.39-10.95.pth, mybk
BLEU = 8.07, 31.9/11.8/5.1/2.2 (BP=1.000, ratio=1.088, hyp_len=12433, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.39.2.64-14.00.2.50-12.24.2.62-13.79.2.39-10.95.pth, bkmy
BLEU = 9.24, 36.3/14.5/5.8/2.4 (BP=1.000, ratio=1.052, hyp_len=12871, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.40.2.48-11.97.2.33-10.31.2.63-13.81.2.38-10.84.pth, mybk
BLEU = 8.47, 31.7/12.0/5.3/2.5 (BP=1.000, ratio=1.078, hyp_len=12320, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.40.2.48-11.97.2.33-10.31.2.63-13.81.2.38-10.84.pth, bkmy
BLEU = 9.33, 35.5/14.7/6.0/2.4 (BP=1.000, ratio=1.092, hyp_len=13354, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.41.2.46-11.69.2.30-10.02.2.63-13.93.2.40-11.06.pth, mybk
BLEU = 8.27, 30.6/11.7/5.3/2.5 (BP=1.000, ratio=1.126, hyp_len=12870, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.41.2.46-11.69.2.30-10.02.2.63-13.93.2.40-11.06.pth, bkmy
BLEU = 8.89, 33.7/13.8/5.7/2.4 (BP=1.000, ratio=1.149, hyp_len=14054, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.42.2.44-11.51.2.31-10.05.2.62-13.76.2.37-10.74.pth, mybk
BLEU = 8.32, 31.6/12.0/5.2/2.4 (BP=1.000, ratio=1.121, hyp_len=12812, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.42.2.44-11.51.2.31-10.05.2.62-13.76.2.37-10.74.pth, bkmy
BLEU = 9.59, 35.4/14.4/6.1/2.7 (BP=1.000, ratio=1.079, hyp_len=13202, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.43.2.44-11.50.2.28-9.74.2.62-13.72.2.38-10.86.pth, mybk
BLEU = 8.74, 33.0/12.3/5.5/2.6 (BP=1.000, ratio=1.080, hyp_len=12343, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.43.2.44-11.50.2.28-9.74.2.62-13.72.2.38-10.86.pth, bkmy
BLEU = 9.06, 35.9/14.2/5.7/2.3 (BP=1.000, ratio=1.087, hyp_len=13298, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.44.2.46-11.65.2.26-9.58.2.60-13.49.2.38-10.77.pth, mybk
BLEU = 9.18, 33.4/12.9/5.8/2.8 (BP=1.000, ratio=1.044, hyp_len=11939, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.44.2.46-11.65.2.26-9.58.2.60-13.49.2.38-10.77.pth, bkmy
BLEU = 8.39, 32.6/12.9/5.3/2.2 (BP=1.000, ratio=1.192, hyp_len=14584, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.45.2.40-11.05.2.23-9.28.2.63-13.94.2.38-10.78.pth, mybk
BLEU = 9.17, 33.1/13.0/5.9/2.8 (BP=1.000, ratio=1.090, hyp_len=12464, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.45.2.40-11.05.2.23-9.28.2.63-13.94.2.38-10.78.pth, bkmy
BLEU = 9.61, 36.2/15.0/6.2/2.5 (BP=1.000, ratio=1.080, hyp_len=13206, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.46.2.33-10.33.2.19-8.90.2.61-13.58.2.35-10.49.pth, mybk
BLEU = 9.29, 32.8/12.9/6.0/2.9 (BP=1.000, ratio=1.086, hyp_len=12420, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.46.2.33-10.33.2.19-8.90.2.61-13.58.2.35-10.49.pth, bkmy
BLEU = 9.47, 36.3/14.7/6.1/2.5 (BP=1.000, ratio=1.084, hyp_len=13256, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.47.2.37-10.74.2.19-8.93.2.64-14.07.2.35-10.51.pth, mybk
BLEU = 8.71, 32.8/12.3/5.5/2.6 (BP=1.000, ratio=1.085, hyp_len=12399, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.47.2.37-10.74.2.19-8.93.2.64-14.07.2.35-10.51.pth, bkmy
BLEU = 9.96, 36.6/14.8/6.3/2.9 (BP=1.000, ratio=1.078, hyp_len=13191, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.48.2.26-9.56.2.13-8.37.2.59-13.34.2.35-10.50.pth, mybk
BLEU = 8.87, 32.3/12.6/5.6/2.7 (BP=1.000, ratio=1.103, hyp_len=12610, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.48.2.26-9.56.2.13-8.37.2.59-13.34.2.35-10.50.pth, bkmy
BLEU = 9.61, 36.6/15.1/6.2/2.5 (BP=1.000, ratio=1.083, hyp_len=13241, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.49.2.24-9.38.2.08-8.04.2.63-13.84.2.37-10.69.pth, mybk
BLEU = 8.76, 32.6/12.7/5.6/2.6 (BP=1.000, ratio=1.115, hyp_len=12749, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.49.2.24-9.38.2.08-8.04.2.63-13.84.2.37-10.69.pth, bkmy
BLEU = 9.22, 34.9/14.2/5.9/2.5 (BP=1.000, ratio=1.108, hyp_len=13546, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.50.2.25-9.45.2.10-8.13.2.64-14.07.2.34-10.42.pth, mybk
BLEU = 8.94, 32.6/12.7/5.8/2.7 (BP=1.000, ratio=1.107, hyp_len=12659, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.50.2.25-9.45.2.10-8.13.2.64-14.07.2.34-10.42.pth, bkmy
BLEU = 10.08, 36.7/15.4/6.5/2.8 (BP=1.000, ratio=1.083, hyp_len=13251, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.51.2.26-9.63.2.11-8.29.2.65-14.09.2.35-10.53.pth, mybk
BLEU = 8.87, 32.5/12.4/5.7/2.7 (BP=1.000, ratio=1.117, hyp_len=12767, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.51.2.26-9.63.2.11-8.29.2.65-14.09.2.35-10.53.pth, bkmy
BLEU = 8.63, 32.1/13.2/5.6/2.4 (BP=1.000, ratio=1.238, hyp_len=15147, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.52.2.21-9.15.2.09-8.06.2.64-14.04.2.32-10.18.pth, mybk
BLEU = 9.39, 33.4/13.0/5.9/3.0 (BP=1.000, ratio=1.095, hyp_len=12517, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.52.2.21-9.15.2.09-8.06.2.64-14.04.2.32-10.18.pth, bkmy
BLEU = 9.86, 36.1/15.1/6.5/2.7 (BP=1.000, ratio=1.110, hyp_len=13573, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.53.2.16-8.68.2.02-7.51.2.62-13.75.2.35-10.50.pth, mybk
BLEU = 9.49, 34.1/13.4/6.2/2.8 (BP=1.000, ratio=1.068, hyp_len=12215, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.53.2.16-8.68.2.02-7.51.2.62-13.75.2.35-10.50.pth, bkmy
BLEU = 9.85, 35.7/14.8/6.3/2.8 (BP=1.000, ratio=1.101, hyp_len=13470, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.54.2.10-8.17.1.96-7.12.2.65-14.18.2.36-10.60.pth, mybk
BLEU = 9.62, 34.1/13.6/6.2/3.0 (BP=1.000, ratio=1.084, hyp_len=12394, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.54.2.10-8.17.1.96-7.12.2.65-14.18.2.36-10.60.pth, bkmy
BLEU = 9.41, 33.9/14.0/6.1/2.7 (BP=1.000, ratio=1.183, hyp_len=14469, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.55.2.17-8.76.2.02-7.53.2.64-14.00.2.35-10.46.pth, mybk
BLEU = 9.19, 33.0/13.0/5.9/2.8 (BP=1.000, ratio=1.108, hyp_len=12671, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.55.2.17-8.76.2.02-7.53.2.64-14.00.2.35-10.46.pth, bkmy
BLEU = 10.21, 36.4/15.2/6.7/3.0 (BP=1.000, ratio=1.119, hyp_len=13683, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.56.2.09-8.12.1.96-7.13.2.63-13.91.2.34-10.36.pth, mybk
BLEU = 9.71, 34.8/13.7/6.3/3.0 (BP=1.000, ratio=1.073, hyp_len=12268, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.56.2.09-8.12.1.96-7.13.2.63-13.91.2.34-10.36.pth, bkmy
BLEU = 10.78, 38.5/16.1/7.1/3.1 (BP=1.000, ratio=1.057, hyp_len=12925, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.57.2.10-8.19.1.95-7.02.2.66-14.30.2.34-10.37.pth, mybk
BLEU = 9.59, 33.8/13.0/6.2/3.1 (BP=1.000, ratio=1.067, hyp_len=12196, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.57.2.10-8.19.1.95-7.02.2.66-14.30.2.34-10.37.pth, bkmy
BLEU = 10.36, 37.1/15.3/6.8/3.0 (BP=1.000, ratio=1.067, hyp_len=13047, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.58.2.04-7.68.1.89-6.61.2.64-14.07.2.34-10.34.pth, mybk
BLEU = 9.45, 33.8/13.3/6.1/2.9 (BP=1.000, ratio=1.088, hyp_len=12435, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.58.2.04-7.68.1.89-6.61.2.64-14.07.2.34-10.34.pth, bkmy
BLEU = 10.52, 37.3/15.7/6.9/3.0 (BP=1.000, ratio=1.087, hyp_len=13294, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.59.2.01-7.49.1.86-6.42.2.65-14.13.2.33-10.29.pth, mybk
BLEU = 9.71, 34.3/13.8/6.2/3.0 (BP=1.000, ratio=1.084, hyp_len=12392, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.59.2.01-7.49.1.86-6.42.2.65-14.13.2.33-10.29.pth, bkmy
BLEU = 10.71, 37.7/15.8/7.0/3.1 (BP=1.000, ratio=1.076, hyp_len=13157, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.60.1.99-7.31.1.85-6.39.2.65-14.17.2.34-10.41.pth, mybk
BLEU = 9.84, 34.5/13.8/6.3/3.1 (BP=1.000, ratio=1.091, hyp_len=12469, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.60.1.99-7.31.1.85-6.39.2.65-14.17.2.34-10.41.pth, bkmy
BLEU = 10.88, 37.2/15.8/7.2/3.3 (BP=1.000, ratio=1.099, hyp_len=13441, ref_len=12231)
```

Best BLEU Score of my-bk, 60 epoch: 9.84  
Best BLEU Score of bk-my, 60 epoch: 10.88  

## Seq2Seq-DSL, my-bk, 70epoch

training

```
Epoch 1 - |param|=8.50e+02 |g_param|=4.15e+05 loss_x2y=4.9124e+00 ppl_x2y=135.97 loss_y2x=4.7050e+00 ppl_y2x=110.49 dual_loss=0.0000e+00
Validation X2Y - loss=4.0458e+00 ppl=57.16 best_loss=inf best_ppl=inf
Validation Y2X - loss=3.9686e+00 ppl=52.91 best_loss=inf best_ppl=inf
Epoch 2 - |param|=8.50e+02 |g_param|=2.56e+05 loss_x2y=4.4293e+00 ppl_x2y=83.87 loss_y2x=4.2222e+00 ppl_y2x=68.18 dual_loss=0.0000e+00
Validation X2Y - loss=3.9691e+00 ppl=52.94 best_loss=4.0458e+00 best_ppl=57.16
Validation Y2X - loss=3.7886e+00 ppl=44.19 best_loss=3.9686e+00 best_ppl=52.91
Epoch 3 - |param|=8.50e+02 |g_param|=2.26e+05 loss_x2y=4.3858e+00 ppl_x2y=80.30 loss_y2x=4.1730e+00 ppl_y2x=64.91 dual_loss=0.0000e+00
Validation X2Y - loss=3.8710e+00 ppl=47.99 best_loss=3.9691e+00 best_ppl=52.94
Validation Y2X - loss=3.7329e+00 ppl=41.80 best_loss=3.7886e+00 best_ppl=44.19
Epoch 4 - |param|=8.50e+02 |g_param|=2.54e+05 loss_x2y=4.4404e+00 ppl_x2y=84.81 loss_y2x=4.1788e+00 ppl_y2x=65.29 dual_loss=0.0000e+00
Validation X2Y - loss=3.8589e+00 ppl=47.41 best_loss=3.8710e+00 best_ppl=47.99
Validation Y2X - loss=3.7413e+00 ppl=42.15 best_loss=3.7329e+00 best_ppl=41.80
Epoch 5 - |param|=8.50e+02 |g_param|=2.23e+05 loss_x2y=4.3553e+00 ppl_x2y=77.89 loss_y2x=4.1203e+00 ppl_y2x=61.58 dual_loss=0.0000e+00
Validation X2Y - loss=3.8077e+00 ppl=45.05 best_loss=3.8589e+00 best_ppl=47.41
Validation Y2X - loss=3.7171e+00 ppl=41.14 best_loss=3.7329e+00 best_ppl=41.80
Epoch 6 - |param|=8.50e+02 |g_param|=2.37e+05 loss_x2y=4.3138e+00 ppl_x2y=74.73 loss_y2x=4.1016e+00 ppl_y2x=60.44 dual_loss=0.0000e+00
Validation X2Y - loss=3.8089e+00 ppl=45.10 best_loss=3.8077e+00 best_ppl=45.05
Validation Y2X - loss=3.6580e+00 ppl=38.78 best_loss=3.7171e+00 best_ppl=41.14
Epoch 7 - |param|=8.50e+02 |g_param|=2.11e+05 loss_x2y=4.2765e+00 ppl_x2y=71.99 loss_y2x=4.0613e+00 ppl_y2x=58.05 dual_loss=0.0000e+00
Validation X2Y - loss=3.7741e+00 ppl=43.56 best_loss=3.8077e+00 best_ppl=45.05
Validation Y2X - loss=3.6799e+00 ppl=39.64 best_loss=3.6580e+00 best_ppl=38.78
Epoch 8 - |param|=8.51e+02 |g_param|=2.20e+05 loss_x2y=4.3108e+00 ppl_x2y=74.50 loss_y2x=4.0991e+00 ppl_y2x=60.29 dual_loss=0.0000e+00
Validation X2Y - loss=3.7322e+00 ppl=41.77 best_loss=3.7741e+00 best_ppl=43.56
Validation Y2X - loss=3.6421e+00 ppl=38.17 best_loss=3.6580e+00 best_ppl=38.78
Epoch 9 - |param|=8.51e+02 |g_param|=2.19e+05 loss_x2y=4.2628e+00 ppl_x2y=71.01 loss_y2x=4.0458e+00 ppl_y2x=57.16 dual_loss=0.0000e+00
Validation X2Y - loss=3.7798e+00 ppl=43.81 best_loss=3.7322e+00 best_ppl=41.77
Validation Y2X - loss=3.6391e+00 ppl=38.06 best_loss=3.6421e+00 best_ppl=38.17
Epoch 10 - |param|=8.52e+02 |g_param|=2.19e+05 loss_x2y=4.1826e+00 ppl_x2y=65.53 loss_y2x=4.0080e+00 ppl_y2x=55.04 dual_loss=0.0000e+00
Validation X2Y - loss=3.6982e+00 ppl=40.37 best_loss=3.7322e+00 best_ppl=41.77
Validation Y2X - loss=3.6092e+00 ppl=36.94 best_loss=3.6391e+00 best_ppl=38.06
Epoch 11 - |param|=8.53e+02 |g_param|=2.13e+05 loss_x2y=4.1039e+00 ppl_x2y=60.58 loss_y2x=3.9557e+00 ppl_y2x=52.23 dual_loss=0.0000e+00
Validation X2Y - loss=3.6601e+00 ppl=38.86 best_loss=3.6982e+00 best_ppl=40.37
Validation Y2X - loss=3.5338e+00 ppl=34.25 best_loss=3.6092e+00 best_ppl=36.94
Epoch 12 - |param|=8.53e+02 |g_param|=1.78e+05 loss_x2y=4.0223e+00 ppl_x2y=55.83 loss_y2x=3.8889e+00 ppl_y2x=48.86 dual_loss=0.0000e+00
Validation X2Y - loss=3.4120e+00 ppl=30.33 best_loss=3.6601e+00 best_ppl=38.86
Validation Y2X - loss=3.3901e+00 ppl=29.67 best_loss=3.5338e+00 best_ppl=34.25
Epoch 13 - |param|=8.54e+02 |g_param|=1.56e+05 loss_x2y=3.7780e+00 ppl_x2y=43.73 loss_y2x=3.6929e+00 ppl_y2x=40.16 dual_loss=0.0000e+00
Validation X2Y - loss=3.2937e+00 ppl=26.94 best_loss=3.4120e+00 best_ppl=30.33
Validation Y2X - loss=3.2429e+00 ppl=25.61 best_loss=3.3901e+00 best_ppl=29.67
Epoch 14 - |param|=8.54e+02 |g_param|=1.53e+05 loss_x2y=3.6236e+00 ppl_x2y=37.47 loss_y2x=3.5280e+00 ppl_y2x=34.06 dual_loss=0.0000e+00
Validation X2Y - loss=3.2221e+00 ppl=25.08 best_loss=3.2937e+00 best_ppl=26.94
Validation Y2X - loss=3.1551e+00 ppl=23.46 best_loss=3.2429e+00 best_ppl=25.61
Epoch 15 - |param|=8.55e+02 |g_param|=1.46e+05 loss_x2y=3.5445e+00 ppl_x2y=34.62 loss_y2x=3.4522e+00 ppl_y2x=31.57 dual_loss=0.0000e+00
Validation X2Y - loss=3.1545e+00 ppl=23.44 best_loss=3.2221e+00 best_ppl=25.08
Validation Y2X - loss=3.0616e+00 ppl=21.36 best_loss=3.1551e+00 best_ppl=23.46
Epoch 16 - |param|=8.56e+02 |g_param|=1.49e+05 loss_x2y=3.4650e+00 ppl_x2y=31.98 loss_y2x=3.3858e+00 ppl_y2x=29.54 dual_loss=0.0000e+00
Validation X2Y - loss=3.0771e+00 ppl=21.69 best_loss=3.1545e+00 best_ppl=23.44
Validation Y2X - loss=3.0367e+00 ppl=20.84 best_loss=3.0616e+00 best_ppl=21.36
Epoch 17 - |param|=8.56e+02 |g_param|=1.52e+05 loss_x2y=3.3972e+00 ppl_x2y=29.88 loss_y2x=3.2931e+00 ppl_y2x=26.93 dual_loss=0.0000e+00
Validation X2Y - loss=3.0335e+00 ppl=20.77 best_loss=3.0771e+00 best_ppl=21.69
Validation Y2X - loss=2.9603e+00 ppl=19.30 best_loss=3.0367e+00 best_ppl=20.84
Epoch 18 - |param|=8.57e+02 |g_param|=1.55e+05 loss_x2y=3.3148e+00 ppl_x2y=27.52 loss_y2x=3.2176e+00 ppl_y2x=24.97 dual_loss=0.0000e+00
Validation X2Y - loss=2.9900e+00 ppl=19.89 best_loss=3.0335e+00 best_ppl=20.77
Validation Y2X - loss=2.8852e+00 ppl=17.91 best_loss=2.9603e+00 best_ppl=19.30
Epoch 19 - |param|=8.58e+02 |g_param|=1.53e+05 loss_x2y=3.3167e+00 ppl_x2y=27.57 loss_y2x=3.2537e+00 ppl_y2x=25.88 dual_loss=0.0000e+00
Validation X2Y - loss=2.9303e+00 ppl=18.73 best_loss=2.9900e+00 best_ppl=19.89
Validation Y2X - loss=2.8376e+00 ppl=17.08 best_loss=2.8852e+00 best_ppl=17.91
Epoch 20 - |param|=8.59e+02 |g_param|=1.56e+05 loss_x2y=3.1722e+00 ppl_x2y=23.86 loss_y2x=3.1108e+00 ppl_y2x=22.44 dual_loss=0.0000e+00
Validation X2Y - loss=2.8798e+00 ppl=17.81 best_loss=2.9303e+00 best_ppl=18.73
Validation Y2X - loss=2.7960e+00 ppl=16.38 best_loss=2.8376e+00 best_ppl=17.08
Epoch 21 - |param|=8.59e+02 |g_param|=1.51e+05 loss_x2y=3.1973e+00 ppl_x2y=24.47 loss_y2x=3.1138e+00 ppl_y2x=22.51 dual_loss=7.8919e-01
Validation X2Y - loss=2.8371e+00 ppl=17.07 best_loss=2.8798e+00 best_ppl=17.81
Validation Y2X - loss=2.7478e+00 ppl=15.61 best_loss=2.7960e+00 best_ppl=16.38
Epoch 22 - |param|=8.60e+02 |g_param|=1.62e+05 loss_x2y=3.1376e+00 ppl_x2y=23.05 loss_y2x=3.0683e+00 ppl_y2x=21.50 dual_loss=7.6495e-01
Validation X2Y - loss=2.8196e+00 ppl=16.77 best_loss=2.8371e+00 best_ppl=17.07
Validation Y2X - loss=2.7335e+00 ppl=15.39 best_loss=2.7478e+00 best_ppl=15.61
Epoch 23 - |param|=8.61e+02 |g_param|=1.54e+05 loss_x2y=3.0873e+00 ppl_x2y=21.92 loss_y2x=3.0115e+00 ppl_y2x=20.32 dual_loss=7.0857e-01
Validation X2Y - loss=2.7748e+00 ppl=16.04 best_loss=2.8196e+00 best_ppl=16.77
Validation Y2X - loss=2.6981e+00 ppl=14.85 best_loss=2.7335e+00 best_ppl=15.39
Epoch 24 - |param|=8.61e+02 |g_param|=1.64e+05 loss_x2y=3.0882e+00 ppl_x2y=21.94 loss_y2x=3.0087e+00 ppl_y2x=20.26 dual_loss=6.9812e-01
Validation X2Y - loss=2.7436e+00 ppl=15.54 best_loss=2.7748e+00 best_ppl=16.04
Validation Y2X - loss=2.6625e+00 ppl=14.33 best_loss=2.6981e+00 best_ppl=14.85
Epoch 25 - |param|=8.62e+02 |g_param|=1.57e+05 loss_x2y=2.9612e+00 ppl_x2y=19.32 loss_y2x=2.8894e+00 ppl_y2x=17.98 dual_loss=6.1157e-01
Validation X2Y - loss=2.7415e+00 ppl=15.51 best_loss=2.7436e+00 best_ppl=15.54
Validation Y2X - loss=2.6148e+00 ppl=13.66 best_loss=2.6625e+00 best_ppl=14.33
Epoch 26 - |param|=8.63e+02 |g_param|=1.73e+05 loss_x2y=3.0302e+00 ppl_x2y=20.70 loss_y2x=2.9417e+00 ppl_y2x=18.95 dual_loss=6.6919e-01
Validation X2Y - loss=2.7169e+00 ppl=15.13 best_loss=2.7415e+00 best_ppl=15.51
Validation Y2X - loss=2.5795e+00 ppl=13.19 best_loss=2.6148e+00 best_ppl=13.66
Epoch 27 - |param|=8.64e+02 |g_param|=1.63e+05 loss_x2y=2.9200e+00 ppl_x2y=18.54 loss_y2x=2.8247e+00 ppl_y2x=16.86 dual_loss=5.6634e-01
Validation X2Y - loss=2.6851e+00 ppl=14.66 best_loss=2.7169e+00 best_ppl=15.13
Validation Y2X - loss=2.5596e+00 ppl=12.93 best_loss=2.5795e+00 best_ppl=13.19
Epoch 28 - |param|=8.64e+02 |g_param|=1.79e+05 loss_x2y=2.8659e+00 ppl_x2y=17.56 loss_y2x=2.7813e+00 ppl_y2x=16.14 dual_loss=5.7425e-01
Validation X2Y - loss=2.6582e+00 ppl=14.27 best_loss=2.6851e+00 best_ppl=14.66
Validation Y2X - loss=2.5144e+00 ppl=12.36 best_loss=2.5596e+00 best_ppl=12.93
Epoch 29 - |param|=8.65e+02 |g_param|=1.64e+05 loss_x2y=2.8153e+00 ppl_x2y=16.70 loss_y2x=2.7430e+00 ppl_y2x=15.53 dual_loss=5.3933e-01
Validation X2Y - loss=2.6743e+00 ppl=14.50 best_loss=2.6582e+00 best_ppl=14.27
Validation Y2X - loss=2.4804e+00 ppl=11.95 best_loss=2.5144e+00 best_ppl=12.36
Epoch 30 - |param|=8.66e+02 |g_param|=1.81e+05 loss_x2y=2.8092e+00 ppl_x2y=16.60 loss_y2x=2.7004e+00 ppl_y2x=14.89 dual_loss=5.1248e-01
Validation X2Y - loss=2.6581e+00 ppl=14.27 best_loss=2.6582e+00 best_ppl=14.27
Validation Y2X - loss=2.4459e+00 ppl=11.54 best_loss=2.4804e+00 best_ppl=11.95
Epoch 31 - |param|=8.66e+02 |g_param|=1.74e+05 loss_x2y=2.7084e+00 ppl_x2y=15.00 loss_y2x=2.6188e+00 ppl_y2x=13.72 dual_loss=4.7041e-01
Validation X2Y - loss=2.6215e+00 ppl=13.76 best_loss=2.6581e+00 best_ppl=14.27
Validation Y2X - loss=2.4108e+00 ppl=11.14 best_loss=2.4459e+00 best_ppl=11.54
Epoch 32 - |param|=8.67e+02 |g_param|=1.83e+05 loss_x2y=2.7077e+00 ppl_x2y=14.99 loss_y2x=2.5761e+00 ppl_y2x=13.15 dual_loss=4.4120e-01
Validation X2Y - loss=2.6286e+00 ppl=13.85 best_loss=2.6215e+00 best_ppl=13.76
Validation Y2X - loss=2.4058e+00 ppl=11.09 best_loss=2.4108e+00 best_ppl=11.14
Epoch 33 - |param|=8.68e+02 |g_param|=2.37e+05 loss_x2y=2.7606e+00 ppl_x2y=15.81 loss_y2x=2.6714e+00 ppl_y2x=14.46 dual_loss=5.3304e-01
Validation X2Y - loss=2.6292e+00 ppl=13.86 best_loss=2.6215e+00 best_ppl=13.76
Validation Y2X - loss=2.3990e+00 ppl=11.01 best_loss=2.4058e+00 best_ppl=11.09
Epoch 34 - |param|=8.69e+02 |g_param|=3.47e+05 loss_x2y=2.6520e+00 ppl_x2y=14.18 loss_y2x=2.5457e+00 ppl_y2x=12.75 dual_loss=4.5596e-01
Validation X2Y - loss=2.6435e+00 ppl=14.06 best_loss=2.6215e+00 best_ppl=13.76
Validation Y2X - loss=2.3628e+00 ppl=10.62 best_loss=2.3990e+00 best_ppl=11.01
Epoch 35 - |param|=8.69e+02 |g_param|=3.82e+05 loss_x2y=2.7181e+00 ppl_x2y=15.15 loss_y2x=2.5421e+00 ppl_y2x=12.71 dual_loss=4.5907e-01
Validation X2Y - loss=2.5823e+00 ppl=13.23 best_loss=2.6215e+00 best_ppl=13.76
Validation Y2X - loss=2.3468e+00 ppl=10.45 best_loss=2.3628e+00 best_ppl=10.62
Epoch 36 - |param|=8.70e+02 |g_param|=3.85e+05 loss_x2y=2.6112e+00 ppl_x2y=13.62 loss_y2x=2.5132e+00 ppl_y2x=12.34 dual_loss=4.1065e-01
Validation X2Y - loss=2.5663e+00 ppl=13.02 best_loss=2.5823e+00 best_ppl=13.23
Validation Y2X - loss=2.3331e+00 ppl=10.31 best_loss=2.3468e+00 best_ppl=10.45
Epoch 37 - |param|=8.71e+02 |g_param|=3.81e+05 loss_x2y=2.5172e+00 ppl_x2y=12.39 loss_y2x=2.4172e+00 ppl_y2x=11.21 dual_loss=4.0421e-01
Validation X2Y - loss=2.5786e+00 ppl=13.18 best_loss=2.5663e+00 best_ppl=13.02
Validation Y2X - loss=2.3035e+00 ppl=10.01 best_loss=2.3331e+00 best_ppl=10.31
Epoch 38 - |param|=8.71e+02 |g_param|=3.93e+05 loss_x2y=2.5166e+00 ppl_x2y=12.39 loss_y2x=2.4105e+00 ppl_y2x=11.14 dual_loss=3.9252e-01
Validation X2Y - loss=2.5848e+00 ppl=13.26 best_loss=2.5663e+00 best_ppl=13.02
Validation Y2X - loss=2.2854e+00 ppl=9.83 best_loss=2.3035e+00 best_ppl=10.01
Epoch 39 - |param|=8.72e+02 |g_param|=4.09e+05 loss_x2y=2.5595e+00 ppl_x2y=12.93 loss_y2x=2.4344e+00 ppl_y2x=11.41 dual_loss=3.9967e-01
Validation X2Y - loss=2.5647e+00 ppl=13.00 best_loss=2.5663e+00 best_ppl=13.02
Validation Y2X - loss=2.2795e+00 ppl=9.77 best_loss=2.2854e+00 best_ppl=9.83
Epoch 40 - |param|=8.73e+02 |g_param|=4.18e+05 loss_x2y=2.4864e+00 ppl_x2y=12.02 loss_y2x=2.3557e+00 ppl_y2x=10.55 dual_loss=3.6875e-01
Validation X2Y - loss=2.5792e+00 ppl=13.19 best_loss=2.5647e+00 best_ppl=13.00
Validation Y2X - loss=2.2504e+00 ppl=9.49 best_loss=2.2795e+00 best_ppl=9.77
Epoch 41 - |param|=8.73e+02 |g_param|=4.14e+05 loss_x2y=2.4426e+00 ppl_x2y=11.50 loss_y2x=2.3396e+00 ppl_y2x=10.38 dual_loss=3.9379e-01
Validation X2Y - loss=2.6058e+00 ppl=13.54 best_loss=2.5647e+00 best_ppl=13.00
Validation Y2X - loss=2.2768e+00 ppl=9.75 best_loss=2.2504e+00 best_ppl=9.49
Epoch 42 - |param|=8.74e+02 |g_param|=4.45e+05 loss_x2y=2.3907e+00 ppl_x2y=10.92 loss_y2x=2.2849e+00 ppl_y2x=9.82 dual_loss=3.7669e-01
Validation X2Y - loss=2.5763e+00 ppl=13.15 best_loss=2.5647e+00 best_ppl=13.00
Validation Y2X - loss=2.2217e+00 ppl=9.22 best_loss=2.2504e+00 best_ppl=9.49
Epoch 43 - |param|=8.75e+02 |g_param|=4.31e+05 loss_x2y=2.3391e+00 ppl_x2y=10.37 loss_y2x=2.2221e+00 ppl_y2x=9.23 dual_loss=3.6024e-01
Validation X2Y - loss=2.5766e+00 ppl=13.15 best_loss=2.5647e+00 best_ppl=13.00
Validation Y2X - loss=2.2358e+00 ppl=9.35 best_loss=2.2217e+00 best_ppl=9.22
Epoch 44 - |param|=8.75e+02 |g_param|=4.31e+05 loss_x2y=2.3478e+00 ppl_x2y=10.46 loss_y2x=2.2250e+00 ppl_y2x=9.25 dual_loss=3.6519e-01
Validation X2Y - loss=2.5464e+00 ppl=12.76 best_loss=2.5647e+00 best_ppl=13.00
Validation Y2X - loss=2.2259e+00 ppl=9.26 best_loss=2.2217e+00 best_ppl=9.22
Epoch 45 - |param|=8.76e+02 |g_param|=4.28e+05 loss_x2y=2.3182e+00 ppl_x2y=10.16 loss_y2x=2.1864e+00 ppl_y2x=8.90 dual_loss=3.4352e-01
Validation X2Y - loss=2.5577e+00 ppl=12.91 best_loss=2.5464e+00 best_ppl=12.76
Validation Y2X - loss=2.2051e+00 ppl=9.07 best_loss=2.2217e+00 best_ppl=9.22
Epoch 46 - |param|=8.77e+02 |g_param|=4.43e+05 loss_x2y=2.2712e+00 ppl_x2y=9.69 loss_y2x=2.1305e+00 ppl_y2x=8.42 dual_loss=3.3851e-01
Validation X2Y - loss=2.5581e+00 ppl=12.91 best_loss=2.5464e+00 best_ppl=12.76
Validation Y2X - loss=2.2003e+00 ppl=9.03 best_loss=2.2051e+00 best_ppl=9.07
Epoch 47 - |param|=8.77e+02 |g_param|=4.33e+05 loss_x2y=2.2565e+00 ppl_x2y=9.55 loss_y2x=2.1605e+00 ppl_y2x=8.68 dual_loss=3.4904e-01
Validation X2Y - loss=2.5403e+00 ppl=12.68 best_loss=2.5464e+00 best_ppl=12.76
Validation Y2X - loss=2.1606e+00 ppl=8.68 best_loss=2.2003e+00 best_ppl=9.03
Epoch 48 - |param|=8.78e+02 |g_param|=4.61e+05 loss_x2y=2.3406e+00 ppl_x2y=10.39 loss_y2x=2.2337e+00 ppl_y2x=9.33 dual_loss=3.9092e-01
Validation X2Y - loss=2.5432e+00 ppl=12.72 best_loss=2.5403e+00 best_ppl=12.68
Validation Y2X - loss=2.2008e+00 ppl=9.03 best_loss=2.1606e+00 best_ppl=8.68
Epoch 49 - |param|=8.78e+02 |g_param|=4.46e+05 loss_x2y=2.2020e+00 ppl_x2y=9.04 loss_y2x=2.0578e+00 ppl_y2x=7.83 dual_loss=3.3165e-01
Validation X2Y - loss=2.5822e+00 ppl=13.23 best_loss=2.5403e+00 best_ppl=12.68
Validation Y2X - loss=2.1692e+00 ppl=8.75 best_loss=2.1606e+00 best_ppl=8.68
Epoch 50 - |param|=8.79e+02 |g_param|=4.62e+05 loss_x2y=2.1806e+00 ppl_x2y=8.85 loss_y2x=2.0666e+00 ppl_y2x=7.90 dual_loss=3.2856e-01
Validation X2Y - loss=2.5762e+00 ppl=13.15 best_loss=2.5403e+00 best_ppl=12.68
Validation Y2X - loss=2.1535e+00 ppl=8.61 best_loss=2.1606e+00 best_ppl=8.68
Epoch 51 - |param|=8.80e+02 |g_param|=4.52e+05 loss_x2y=2.2161e+00 ppl_x2y=9.17 loss_y2x=2.0706e+00 ppl_y2x=7.93 dual_loss=3.4322e-01
Validation X2Y - loss=2.5557e+00 ppl=12.88 best_loss=2.5403e+00 best_ppl=12.68
Validation Y2X - loss=2.1577e+00 ppl=8.65 best_loss=2.1535e+00 best_ppl=8.61
Epoch 52 - |param|=8.80e+02 |g_param|=4.75e+05 loss_x2y=2.1517e+00 ppl_x2y=8.60 loss_y2x=2.0171e+00 ppl_y2x=7.52 dual_loss=3.3256e-01
Validation X2Y - loss=2.5551e+00 ppl=12.87 best_loss=2.5403e+00 best_ppl=12.68
Validation Y2X - loss=2.1737e+00 ppl=8.79 best_loss=2.1535e+00 best_ppl=8.61
Epoch 53 - |param|=8.81e+02 |g_param|=5.00e+05 loss_x2y=2.2513e+00 ppl_x2y=9.50 loss_y2x=2.1419e+00 ppl_y2x=8.52 dual_loss=3.8451e-01
Validation X2Y - loss=2.5635e+00 ppl=12.98 best_loss=2.5403e+00 best_ppl=12.68
Validation Y2X - loss=2.1225e+00 ppl=8.35 best_loss=2.1535e+00 best_ppl=8.61
Epoch 54 - |param|=8.81e+02 |g_param|=5.00e+05 loss_x2y=2.1115e+00 ppl_x2y=8.26 loss_y2x=1.9823e+00 ppl_y2x=7.26 dual_loss=3.3160e-01
Validation X2Y - loss=2.5870e+00 ppl=13.29 best_loss=2.5403e+00 best_ppl=12.68
Validation Y2X - loss=2.1329e+00 ppl=8.44 best_loss=2.1225e+00 best_ppl=8.35
Epoch 55 - |param|=8.82e+02 |g_param|=5.02e+05 loss_x2y=2.1102e+00 ppl_x2y=8.25 loss_y2x=2.0139e+00 ppl_y2x=7.49 dual_loss=3.5475e-01
Validation X2Y - loss=2.5483e+00 ppl=12.78 best_loss=2.5403e+00 best_ppl=12.68
Validation Y2X - loss=2.1471e+00 ppl=8.56 best_loss=2.1225e+00 best_ppl=8.35
Epoch 56 - |param|=8.83e+02 |g_param|=4.75e+05 loss_x2y=2.0024e+00 ppl_x2y=7.41 loss_y2x=1.8726e+00 ppl_y2x=6.50 dual_loss=3.1040e-01
Validation X2Y - loss=2.5629e+00 ppl=12.97 best_loss=2.5403e+00 best_ppl=12.68
Validation Y2X - loss=2.1363e+00 ppl=8.47 best_loss=2.1225e+00 best_ppl=8.35
Epoch 57 - |param|=8.83e+02 |g_param|=4.88e+05 loss_x2y=2.0513e+00 ppl_x2y=7.78 loss_y2x=1.9240e+00 ppl_y2x=6.85 dual_loss=3.4163e-01
Validation X2Y - loss=2.5978e+00 ppl=13.43 best_loss=2.5403e+00 best_ppl=12.68
Validation Y2X - loss=2.1502e+00 ppl=8.59 best_loss=2.1225e+00 best_ppl=8.35
Epoch 58 - |param|=8.84e+02 |g_param|=5.16e+05 loss_x2y=2.0076e+00 ppl_x2y=7.45 loss_y2x=1.8602e+00 ppl_y2x=6.42 dual_loss=3.2727e-01
Validation X2Y - loss=2.5451e+00 ppl=12.74 best_loss=2.5403e+00 best_ppl=12.68
Validation Y2X - loss=2.1161e+00 ppl=8.30 best_loss=2.1225e+00 best_ppl=8.35
Epoch 59 - |param|=8.84e+02 |g_param|=5.11e+05 loss_x2y=2.0059e+00 ppl_x2y=7.43 loss_y2x=1.9039e+00 ppl_y2x=6.71 dual_loss=3.3685e-01
Validation X2Y - loss=2.5372e+00 ppl=12.64 best_loss=2.5403e+00 best_ppl=12.68
Validation Y2X - loss=2.1169e+00 ppl=8.31 best_loss=2.1161e+00 best_ppl=8.30
Epoch 60 - |param|=8.85e+02 |g_param|=5.16e+05 loss_x2y=1.9611e+00 ppl_x2y=7.11 loss_y2x=1.8471e+00 ppl_y2x=6.34 dual_loss=3.2664e-01
Validation X2Y - loss=2.6005e+00 ppl=13.47 best_loss=2.5372e+00 best_ppl=12.64
Validation Y2X - loss=2.0894e+00 ppl=8.08 best_loss=2.1161e+00 best_ppl=8.30
Epoch 61 - |param|=8.86e+02 |g_param|=4.97e+05 loss_x2y=1.9439e+00 ppl_x2y=6.99 loss_y2x=1.8297e+00 ppl_y2x=6.23 dual_loss=3.1552e-01
Validation X2Y - loss=2.5437e+00 ppl=12.73 best_loss=2.5372e+00 best_ppl=12.64
Validation Y2X - loss=2.1054e+00 ppl=8.21 best_loss=2.0894e+00 best_ppl=8.08
Epoch 62 - |param|=8.86e+02 |g_param|=5.29e+05 loss_x2y=1.9545e+00 ppl_x2y=7.06 loss_y2x=1.8268e+00 ppl_y2x=6.21 dual_loss=3.3483e-01
Validation X2Y - loss=2.6005e+00 ppl=13.47 best_loss=2.5372e+00 best_ppl=12.64
Validation Y2X - loss=2.0950e+00 ppl=8.13 best_loss=2.0894e+00 best_ppl=8.08
Epoch 63 - |param|=8.87e+02 |g_param|=5.21e+05 loss_x2y=1.9547e+00 ppl_x2y=7.06 loss_y2x=1.7841e+00 ppl_y2x=5.95 dual_loss=3.5492e-01
Validation X2Y - loss=2.5574e+00 ppl=12.90 best_loss=2.5372e+00 best_ppl=12.64
Validation Y2X - loss=2.0848e+00 ppl=8.04 best_loss=2.0894e+00 best_ppl=8.08
Epoch 64 - |param|=8.87e+02 |g_param|=5.34e+05 loss_x2y=1.9119e+00 ppl_x2y=6.77 loss_y2x=1.7812e+00 ppl_y2x=5.94 dual_loss=3.3298e-01
Validation X2Y - loss=2.5717e+00 ppl=13.09 best_loss=2.5372e+00 best_ppl=12.64
Validation Y2X - loss=2.0901e+00 ppl=8.09 best_loss=2.0848e+00 best_ppl=8.04
Epoch 65 - |param|=8.88e+02 |g_param|=5.20e+05 loss_x2y=1.8501e+00 ppl_x2y=6.36 loss_y2x=1.7338e+00 ppl_y2x=5.66 dual_loss=3.3348e-01
Validation X2Y - loss=2.5829e+00 ppl=13.24 best_loss=2.5372e+00 best_ppl=12.64
Validation Y2X - loss=2.1154e+00 ppl=8.29 best_loss=2.0848e+00 best_ppl=8.04
Epoch 66 - |param|=8.88e+02 |g_param|=9.24e+05 loss_x2y=1.8591e+00 ppl_x2y=6.42 loss_y2x=1.7439e+00 ppl_y2x=5.72 dual_loss=3.4410e-01
Validation X2Y - loss=2.5640e+00 ppl=12.99 best_loss=2.5372e+00 best_ppl=12.64
Validation Y2X - loss=2.1084e+00 ppl=8.24 best_loss=2.0848e+00 best_ppl=8.04
Epoch 67 - |param|=8.89e+02 |g_param|=1.05e+06 loss_x2y=1.8660e+00 ppl_x2y=6.46 loss_y2x=1.7626e+00 ppl_y2x=5.83 dual_loss=3.3829e-01
Validation X2Y - loss=2.6046e+00 ppl=13.53 best_loss=2.5372e+00 best_ppl=12.64
Validation Y2X - loss=2.1255e+00 ppl=8.38 best_loss=2.0848e+00 best_ppl=8.04
Epoch 68 - |param|=8.90e+02 |g_param|=1.11e+06 loss_x2y=1.8447e+00 ppl_x2y=6.33 loss_y2x=1.7480e+00 ppl_y2x=5.74 dual_loss=3.5735e-01
Validation X2Y - loss=2.5984e+00 ppl=13.44 best_loss=2.5372e+00 best_ppl=12.64
Validation Y2X - loss=2.1135e+00 ppl=8.28 best_loss=2.0848e+00 best_ppl=8.04
Epoch 69 - |param|=8.90e+02 |g_param|=1.07e+06 loss_x2y=1.7950e+00 ppl_x2y=6.02 loss_y2x=1.6628e+00 ppl_y2x=5.27 dual_loss=3.2800e-01
Validation X2Y - loss=2.5886e+00 ppl=13.31 best_loss=2.5372e+00 best_ppl=12.64
Validation Y2X - loss=2.0967e+00 ppl=8.14 best_loss=2.0848e+00 best_ppl=8.04
Epoch 70 - |param|=8.91e+02 |g_param|=1.17e+06 loss_x2y=1.7989e+00 ppl_x2y=6.04 loss_y2x=1.6747e+00 ppl_y2x=5.34 dual_loss=3.5205e-01
Validation X2Y - loss=2.5834e+00 ppl=13.24 best_loss=2.5372e+00 best_ppl=12.64
Validation Y2X - loss=2.0941e+00 ppl=8.12 best_loss=2.0848e+00 best_ppl=8.04
```

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/mybk-70epoch
Evaluation result for the model: dsl-model-mybk.01.4.91-135.97.4.70-110.49.4.05-57.16.3.97-52.91.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 27.1/0.0/0.0/0.0 (BP=0.459, ratio=0.562, hyp_len=6430, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.91-135.97.4.70-110.49.4.05-57.16.3.97-52.91.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.5/0.1/0.0/0.0 (BP=0.926, ratio=0.928, hyp_len=11356, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.02.4.43-83.87.4.22-68.18.3.97-52.94.3.79-44.19.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.7/0.2/0.0/0.0 (BP=1.000, ratio=1.083, hyp_len=12383, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.4.43-83.87.4.22-68.18.3.97-52.94.3.79-44.19.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 23.0/0.6/0.0/0.0 (BP=0.801, ratio=0.819, hyp_len=10013, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.4.39-80.30.4.17-64.91.3.87-47.99.3.73-41.80.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.3/0.2/0.0/0.0 (BP=1.000, ratio=1.131, hyp_len=12926, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.4.39-80.30.4.17-64.91.3.87-47.99.3.73-41.80.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.5/2.0/0.3/0.0 (BP=1.000, ratio=1.001, hyp_len=12239, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.4.44-84.81.4.18-65.29.3.86-47.41.3.74-42.15.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.2/0.0/0.0/0.0 (BP=1.000, ratio=1.046, hyp_len=11963, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.4.44-84.81.4.18-65.29.3.86-47.41.3.74-42.15.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.5/0.5/0.0/0.0 (BP=0.981, ratio=0.981, hyp_len=11999, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.4.36-77.89.4.12-61.58.3.81-45.05.3.72-41.14.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.9/0.0/0.0/0.0 (BP=1.000, ratio=1.000, hyp_len=11427, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.4.36-77.89.4.12-61.58.3.81-45.05.3.72-41.14.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.3/0.5/0.0/0.0 (BP=1.000, ratio=1.050, hyp_len=12843, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.4.31-74.73.4.10-60.44.3.81-45.10.3.66-38.78.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 14.5/0.0/0.0/0.0 (BP=1.000, ratio=1.111, hyp_len=12700, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.4.31-74.73.4.10-60.44.3.81-45.10.3.66-38.78.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.3/0.8/0.1/0.0 (BP=0.969, ratio=0.970, hyp_len=11858, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.4.28-71.99.4.06-58.05.3.77-43.56.3.68-39.64.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.1/0.2/0.0/0.0 (BP=1.000, ratio=1.007, hyp_len=11507, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.4.28-71.99.4.06-58.05.3.77-43.56.3.68-39.64.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.3/0.5/0.0/0.0 (BP=1.000, ratio=1.056, hyp_len=12917, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.4.31-74.50.4.10-60.29.3.73-41.77.3.64-38.17.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.0/0.3/0.0/0.0 (BP=1.000, ratio=1.078, hyp_len=12329, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.4.31-74.50.4.10-60.29.3.73-41.77.3.64-38.17.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.1/1.4/0.0/0.0 (BP=1.000, ratio=1.038, hyp_len=12701, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.4.26-71.01.4.05-57.16.3.78-43.81.3.64-38.06.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.8/0.7/0.0/0.0 (BP=1.000, ratio=1.108, hyp_len=12670, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.4.26-71.01.4.05-57.16.3.78-43.81.3.64-38.06.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.8/1.3/0.0/0.0 (BP=1.000, ratio=1.025, hyp_len=12532, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.4.18-65.53.4.01-55.04.3.70-40.37.3.61-36.94.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.6/0.9/0.0/0.0 (BP=1.000, ratio=1.091, hyp_len=12469, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.4.18-65.53.4.01-55.04.3.70-40.37.3.61-36.94.pth, bkmy
BLEU = 0.62, 21.5/1.8/0.2/0.0 (BP=0.987, ratio=0.987, hyp_len=12070, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.4.10-60.58.3.96-52.23.3.66-38.86.3.53-34.25.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.0/1.4/0.2/0.0 (BP=1.000, ratio=1.043, hyp_len=11928, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.4.10-60.58.3.96-52.23.3.66-38.86.3.53-34.25.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.1/2.0/0.1/0.0 (BP=1.000, ratio=1.021, hyp_len=12486, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.4.02-55.83.3.89-48.86.3.41-30.33.3.39-29.67.pth, mybk
BLEU = 1.04, 23.0/3.1/0.8/0.0 (BP=0.954, ratio=0.955, hyp_len=10915, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.4.02-55.83.3.89-48.86.3.41-30.33.3.39-29.67.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.3/1.8/0.1/0.0 (BP=1.000, ratio=1.104, hyp_len=13505, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.3.78-43.73.3.69-40.16.3.29-26.94.3.24-25.61.pth, mybk
BLEU = 2.22, 21.2/5.2/1.3/0.2 (BP=1.000, ratio=1.110, hyp_len=12693, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.3.78-43.73.3.69-40.16.3.29-26.94.3.24-25.61.pth, bkmy
BLEU = 1.09, 24.6/5.0/0.5/0.0 (BP=1.000, ratio=1.048, hyp_len=12818, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.3.62-37.47.3.53-34.06.3.22-25.08.3.16-23.46.pth, mybk
BLEU = 4.47, 26.4/7.1/2.5/1.0 (BP=0.958, ratio=0.959, hyp_len=10960, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.3.62-37.47.3.53-34.06.3.22-25.08.3.16-23.46.pth, bkmy
BLEU = 0.28, 6.7/1.3/0.1/0.0 (BP=1.000, ratio=3.643, hyp_len=44561, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.3.54-34.62.3.45-31.57.3.15-23.44.3.06-21.36.pth, mybk
BLEU = 4.46, 24.7/6.7/2.5/1.0 (BP=1.000, ratio=1.032, hyp_len=11798, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.3.54-34.62.3.45-31.57.3.15-23.44.3.06-21.36.pth, bkmy
BLEU = 0.87, 19.2/4.1/0.5/0.0 (BP=1.000, ratio=1.353, hyp_len=16545, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.3.46-31.98.3.39-29.54.3.08-21.69.3.04-20.84.pth, mybk
BLEU = 4.36, 25.0/6.8/2.4/0.9 (BP=1.000, ratio=1.039, hyp_len=11874, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.3.46-31.98.3.39-29.54.3.08-21.69.3.04-20.84.pth, bkmy
BLEU = 0.08, 1.4/0.3/0.1/0.0 (BP=1.000, ratio=13.547, hyp_len=165688, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.3.40-29.88.3.29-26.93.3.03-20.77.2.96-19.30.pth, mybk
BLEU = 3.40, 18.7/4.9/2.0/0.8 (BP=1.000, ratio=1.348, hyp_len=15406, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.3.40-29.88.3.29-26.93.3.03-20.77.2.96-19.30.pth, bkmy
BLEU = 0.44, 4.5/1.1/0.2/0.0 (BP=1.000, ratio=5.786, hyp_len=70767, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.3.31-27.52.3.22-24.97.2.99-19.89.2.89-17.91.pth, mybk
BLEU = 1.38, 8.2/2.0/0.8/0.3 (BP=1.000, ratio=3.047, hyp_len=34834, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.3.31-27.52.3.22-24.97.2.99-19.89.2.89-17.91.pth, bkmy
BLEU = 0.91, 6.6/2.0/0.5/0.1 (BP=1.000, ratio=4.337, hyp_len=53044, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.3.32-27.57.3.25-25.88.2.93-18.73.2.84-17.08.pth, mybk
BLEU = 1.53, 8.7/2.5/0.9/0.3 (BP=1.000, ratio=3.039, hyp_len=34743, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.3.32-27.57.3.25-25.88.2.93-18.73.2.84-17.08.pth, bkmy
BLEU = 2.22, 17.5/5.3/1.0/0.3 (BP=1.000, ratio=1.740, hyp_len=21281, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.3.17-23.86.3.11-22.44.2.88-17.81.2.80-16.38.pth, mybk
BLEU = 2.18, 12.1/3.4/1.2/0.5 (BP=1.000, ratio=2.193, hyp_len=25071, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.3.17-23.86.3.11-22.44.2.88-17.81.2.80-16.38.pth, bkmy
BLEU = 3.17, 18.1/6.1/1.7/0.5 (BP=1.000, ratio=1.836, hyp_len=22457, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.3.20-24.47.3.11-22.51.2.84-17.07.2.75-15.61.pth, mybk
BLEU = 1.79, 9.4/2.7/1.0/0.4 (BP=1.000, ratio=2.825, hyp_len=32291, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.3.20-24.47.3.11-22.51.2.84-17.07.2.75-15.61.pth, bkmy
BLEU = 2.28, 11.8/4.1/1.4/0.4 (BP=1.000, ratio=2.883, hyp_len=35257, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.3.14-23.05.3.07-21.50.2.82-16.77.2.73-15.39.pth, mybk
BLEU = 2.61, 13.8/4.1/1.4/0.6 (BP=1.000, ratio=2.054, hyp_len=23482, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.3.14-23.05.3.07-21.50.2.82-16.77.2.73-15.39.pth, bkmy
BLEU = 1.08, 5.6/1.9/0.6/0.2 (BP=1.000, ratio=5.717, hyp_len=69925, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.3.09-21.92.3.01-20.32.2.77-16.04.2.70-14.85.pth, mybk
BLEU = 2.36, 12.2/3.7/1.3/0.5 (BP=1.000, ratio=2.273, hyp_len=25981, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.3.09-21.92.3.01-20.32.2.77-16.04.2.70-14.85.pth, bkmy
BLEU = 1.56, 7.3/2.6/0.9/0.3 (BP=1.000, ratio=4.597, hyp_len=56230, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.3.09-21.94.3.01-20.26.2.74-15.54.2.66-14.33.pth, mybk
BLEU = 2.86, 14.9/4.5/1.7/0.6 (BP=1.000, ratio=1.965, hyp_len=22467, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.3.09-21.94.3.01-20.26.2.74-15.54.2.66-14.33.pth, bkmy
BLEU = 2.60, 11.6/4.2/1.6/0.6 (BP=1.000, ratio=3.069, hyp_len=37543, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.2.96-19.32.2.89-17.98.2.74-15.51.2.61-13.66.pth, mybk
BLEU = 3.32, 17.2/5.2/1.9/0.7 (BP=1.000, ratio=1.724, hyp_len=19714, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.2.96-19.32.2.89-17.98.2.74-15.51.2.61-13.66.pth, bkmy
BLEU = 2.74, 11.5/4.5/1.7/0.6 (BP=1.000, ratio=3.154, hyp_len=38571, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.3.03-20.70.2.94-18.95.2.72-15.13.2.58-13.19.pth, mybk
BLEU = 3.86, 18.6/6.2/2.3/0.8 (BP=1.000, ratio=1.678, hyp_len=19180, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.3.03-20.70.2.94-18.95.2.72-15.13.2.58-13.19.pth, bkmy
BLEU = 3.98, 16.7/6.4/2.5/0.9 (BP=1.000, ratio=2.186, hyp_len=26743, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.2.92-18.54.2.82-16.86.2.69-14.66.2.56-12.93.pth, mybk
BLEU = 6.30, 28.7/9.7/3.8/1.5 (BP=1.000, ratio=1.097, hyp_len=12539, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.2.92-18.54.2.82-16.86.2.69-14.66.2.56-12.93.pth, bkmy
BLEU = 2.53, 10.7/4.2/1.6/0.6 (BP=1.000, ratio=3.439, hyp_len=42058, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.2.87-17.56.2.78-16.14.2.66-14.27.2.51-12.36.pth, mybk
BLEU = 3.15, 14.9/4.9/1.9/0.7 (BP=1.000, ratio=2.111, hyp_len=24132, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.2.87-17.56.2.78-16.14.2.66-14.27.2.51-12.36.pth, bkmy
BLEU = 3.48, 13.9/5.4/2.2/0.9 (BP=1.000, ratio=2.731, hyp_len=33405, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.2.82-16.70.2.74-15.53.2.67-14.50.2.48-11.95.pth, mybk
BLEU = 5.87, 26.3/8.9/3.5/1.4 (BP=1.000, ratio=1.206, hyp_len=13783, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.2.82-16.70.2.74-15.53.2.67-14.50.2.48-11.95.pth, bkmy
BLEU = 3.81, 15.2/6.0/2.4/0.9 (BP=1.000, ratio=2.493, hyp_len=30487, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.2.81-16.60.2.70-14.89.2.66-14.27.2.45-11.54.pth, mybk
BLEU = 3.30, 15.1/4.9/2.0/0.8 (BP=1.000, ratio=2.109, hyp_len=24109, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.2.81-16.60.2.70-14.89.2.66-14.27.2.45-11.54.pth, bkmy
BLEU = 4.07, 15.4/6.3/2.6/1.1 (BP=1.000, ratio=2.511, hyp_len=30716, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.31.2.71-15.00.2.62-13.72.2.62-13.76.2.41-11.14.pth, mybk
BLEU = 5.89, 26.0/8.9/3.5/1.5 (BP=1.000, ratio=1.240, hyp_len=14170, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.31.2.71-15.00.2.62-13.72.2.62-13.76.2.41-11.14.pth, bkmy
BLEU = 3.95, 15.0/5.9/2.5/1.1 (BP=1.000, ratio=2.572, hyp_len=31464, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.32.2.71-14.99.2.58-13.15.2.63-13.85.2.41-11.09.pth, mybk
BLEU = 7.01, 29.4/10.3/4.3/1.9 (BP=1.000, ratio=1.113, hyp_len=12724, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.32.2.71-14.99.2.58-13.15.2.63-13.85.2.41-11.09.pth, bkmy
BLEU = 7.45, 26.9/11.3/4.9/2.0 (BP=1.000, ratio=1.496, hyp_len=18295, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.33.2.76-15.81.2.67-14.46.2.63-13.86.2.40-11.01.pth, mybk
BLEU = 6.54, 27.3/9.5/4.0/1.8 (BP=1.000, ratio=1.201, hyp_len=13729, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.33.2.76-15.81.2.67-14.46.2.63-13.86.2.40-11.01.pth, bkmy
BLEU = 4.58, 17.1/6.9/3.0/1.2 (BP=1.000, ratio=2.278, hyp_len=27861, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.34.2.65-14.18.2.55-12.75.2.64-14.06.2.36-10.62.pth, mybk
BLEU = 6.94, 29.5/10.4/4.3/1.8 (BP=1.000, ratio=1.122, hyp_len=12827, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.34.2.65-14.18.2.55-12.75.2.64-14.06.2.36-10.62.pth, bkmy
BLEU = 5.39, 19.2/8.0/3.5/1.6 (BP=1.000, ratio=2.075, hyp_len=25375, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.35.2.72-15.15.2.54-12.71.2.58-13.23.2.35-10.45.pth, mybk
BLEU = 7.37, 30.1/10.8/4.6/2.0 (BP=1.000, ratio=1.123, hyp_len=12841, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.35.2.72-15.15.2.54-12.71.2.58-13.23.2.35-10.45.pth, bkmy
BLEU = 4.39, 15.6/6.5/2.9/1.3 (BP=1.000, ratio=2.564, hyp_len=31357, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.36.2.61-13.62.2.51-12.34.2.57-13.02.2.33-10.31.pth, mybk
BLEU = 7.93, 31.3/11.6/4.9/2.2 (BP=1.000, ratio=1.088, hyp_len=12442, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.36.2.61-13.62.2.51-12.34.2.57-13.02.2.33-10.31.pth, bkmy
BLEU = 5.74, 20.7/8.7/3.8/1.6 (BP=1.000, ratio=1.952, hyp_len=23879, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.37.2.52-12.39.2.42-11.21.2.58-13.18.2.30-10.01.pth, mybk
BLEU = 8.40, 32.6/11.9/5.2/2.4 (BP=1.000, ratio=1.074, hyp_len=12276, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.37.2.52-12.39.2.42-11.21.2.58-13.18.2.30-10.01.pth, bkmy
BLEU = 9.75, 32.1/14.3/6.5/3.0 (BP=1.000, ratio=1.320, hyp_len=16144, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.38.2.52-12.39.2.41-11.14.2.58-13.26.2.29-9.83.pth, mybk
BLEU = 7.00, 27.6/10.0/4.4/2.0 (BP=1.000, ratio=1.225, hyp_len=14005, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.38.2.52-12.39.2.41-11.14.2.58-13.26.2.29-9.83.pth, bkmy
BLEU = 8.87, 29.9/13.0/5.9/2.7 (BP=1.000, ratio=1.402, hyp_len=17144, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.39.2.56-12.93.2.43-11.41.2.56-13.00.2.28-9.77.pth, mybk
BLEU = 8.33, 31.5/11.7/5.3/2.5 (BP=1.000, ratio=1.107, hyp_len=12660, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.39.2.56-12.93.2.43-11.41.2.56-13.00.2.28-9.77.pth, bkmy
BLEU = 10.84, 34.9/15.6/7.2/3.5 (BP=1.000, ratio=1.212, hyp_len=14826, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.40.2.49-12.02.2.36-10.55.2.58-13.19.2.25-9.49.pth, mybk
BLEU = 8.21, 31.9/12.0/5.1/2.3 (BP=1.000, ratio=1.102, hyp_len=12601, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.40.2.49-12.02.2.36-10.55.2.58-13.19.2.25-9.49.pth, bkmy
BLEU = 11.17, 36.0/16.1/7.4/3.6 (BP=1.000, ratio=1.194, hyp_len=14599, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.41.2.44-11.50.2.34-10.38.2.61-13.54.2.28-9.75.pth, mybk
BLEU = 8.01, 30.9/11.3/5.0/2.3 (BP=1.000, ratio=1.109, hyp_len=12676, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.41.2.44-11.50.2.34-10.38.2.61-13.54.2.28-9.75.pth, bkmy
BLEU = 11.61, 37.2/16.6/7.8/3.8 (BP=1.000, ratio=1.134, hyp_len=13870, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.42.2.39-10.92.2.28-9.82.2.58-13.15.2.22-9.22.pth, mybk
BLEU = 7.85, 31.2/11.4/4.9/2.2 (BP=1.000, ratio=1.111, hyp_len=12706, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.42.2.39-10.92.2.28-9.82.2.58-13.15.2.22-9.22.pth, bkmy
BLEU = 12.55, 39.0/17.8/8.4/4.3 (BP=1.000, ratio=1.124, hyp_len=13753, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.43.2.34-10.37.2.22-9.23.2.58-13.15.2.24-9.35.pth, mybk
BLEU = 8.43, 31.7/12.0/5.4/2.5 (BP=1.000, ratio=1.105, hyp_len=12628, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.43.2.34-10.37.2.22-9.23.2.58-13.15.2.24-9.35.pth, bkmy
BLEU = 8.56, 28.3/12.5/5.7/2.7 (BP=1.000, ratio=1.512, hyp_len=18497, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.44.2.35-10.46.2.23-9.25.2.55-12.76.2.23-9.26.pth, mybk
BLEU = 8.18, 31.4/11.7/5.2/2.4 (BP=1.000, ratio=1.118, hyp_len=12785, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.44.2.35-10.46.2.23-9.25.2.55-12.76.2.23-9.26.pth, bkmy
BLEU = 12.85, 39.8/18.1/8.6/4.4 (BP=1.000, ratio=1.078, hyp_len=13190, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.45.2.32-10.16.2.19-8.90.2.56-12.91.2.21-9.07.pth, mybk
BLEU = 9.01, 32.6/12.5/5.7/2.8 (BP=1.000, ratio=1.096, hyp_len=12531, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.45.2.32-10.16.2.19-8.90.2.56-12.91.2.21-9.07.pth, bkmy
BLEU = 13.17, 39.1/18.6/8.9/4.6 (BP=1.000, ratio=1.132, hyp_len=13844, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.46.2.27-9.69.2.13-8.42.2.56-12.91.2.20-9.03.pth, mybk
BLEU = 9.02, 32.8/12.7/5.8/2.7 (BP=1.000, ratio=1.102, hyp_len=12597, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.46.2.27-9.69.2.13-8.42.2.56-12.91.2.20-9.03.pth, bkmy
BLEU = 11.08, 34.2/15.9/7.6/3.7 (BP=1.000, ratio=1.296, hyp_len=15856, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.47.2.26-9.55.2.16-8.68.2.54-12.68.2.16-8.68.pth, mybk
BLEU = 9.40, 33.8/13.2/6.1/2.9 (BP=1.000, ratio=1.082, hyp_len=12370, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.47.2.26-9.55.2.16-8.68.2.54-12.68.2.16-8.68.pth, bkmy
BLEU = 14.44, 42.5/20.1/9.9/5.1 (BP=1.000, ratio=1.050, hyp_len=12848, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.48.2.34-10.39.2.23-9.33.2.54-12.72.2.20-9.03.pth, mybk
BLEU = 9.09, 33.4/12.8/5.8/2.7 (BP=1.000, ratio=1.081, hyp_len=12355, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.48.2.34-10.39.2.23-9.33.2.54-12.72.2.20-9.03.pth, bkmy
BLEU = 12.36, 36.8/17.3/8.4/4.4 (BP=1.000, ratio=1.205, hyp_len=14739, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.49.2.20-9.04.2.06-7.83.2.58-13.23.2.17-8.75.pth, mybk
BLEU = 8.96, 32.3/12.5/5.7/2.8 (BP=1.000, ratio=1.133, hyp_len=12952, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.49.2.20-9.04.2.06-7.83.2.58-13.23.2.17-8.75.pth, bkmy
BLEU = 15.06, 42.5/20.6/10.4/5.7 (BP=1.000, ratio=1.035, hyp_len=12662, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.50.2.18-8.85.2.07-7.90.2.58-13.15.2.15-8.61.pth, mybk
BLEU = 8.77, 32.6/12.4/5.6/2.6 (BP=1.000, ratio=1.113, hyp_len=12728, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.50.2.18-8.85.2.07-7.90.2.58-13.15.2.15-8.61.pth, bkmy
BLEU = 15.01, 43.0/21.0/10.5/5.4 (BP=1.000, ratio=1.055, hyp_len=12908, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.51.2.22-9.17.2.07-7.93.2.56-12.88.2.16-8.65.pth, mybk
BLEU = 9.48, 33.6/13.2/6.2/2.9 (BP=1.000, ratio=1.080, hyp_len=12341, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.51.2.22-9.17.2.07-7.93.2.56-12.88.2.16-8.65.pth, bkmy
BLEU = 14.05, 41.2/19.8/9.6/5.0 (BP=1.000, ratio=1.098, hyp_len=13431, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.52.2.15-8.60.2.02-7.52.2.56-12.87.2.17-8.79.pth, mybk
BLEU = 9.92, 34.4/13.7/6.4/3.2 (BP=1.000, ratio=1.080, hyp_len=12341, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.52.2.15-8.60.2.02-7.52.2.56-12.87.2.17-8.79.pth, bkmy
BLEU = 15.07, 42.5/20.4/10.4/5.7 (BP=1.000, ratio=1.092, hyp_len=13356, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.53.2.25-9.50.2.14-8.52.2.56-12.98.2.12-8.35.pth, mybk
BLEU = 9.31, 33.4/13.0/6.0/2.9 (BP=1.000, ratio=1.104, hyp_len=12616, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.53.2.25-9.50.2.14-8.52.2.56-12.98.2.12-8.35.pth, bkmy
BLEU = 14.58, 42.5/20.6/10.0/5.2 (BP=1.000, ratio=1.083, hyp_len=13249, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.54.2.11-8.26.1.98-7.26.2.59-13.29.2.13-8.44.pth, mybk
BLEU = 9.84, 34.1/13.5/6.4/3.2 (BP=1.000, ratio=1.089, hyp_len=12454, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.54.2.11-8.26.1.98-7.26.2.59-13.29.2.13-8.44.pth, bkmy
BLEU = 15.12, 42.8/20.8/10.5/5.6 (BP=1.000, ratio=1.086, hyp_len=13287, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.55.2.11-8.25.2.01-7.49.2.55-12.78.2.15-8.56.pth, mybk
BLEU = 9.52, 34.7/13.5/6.2/2.8 (BP=1.000, ratio=1.077, hyp_len=12311, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.55.2.11-8.25.2.01-7.49.2.55-12.78.2.15-8.56.pth, bkmy
BLEU = 15.31, 43.2/21.2/10.7/5.6 (BP=1.000, ratio=1.070, hyp_len=13087, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.56.2.00-7.41.1.87-6.50.2.56-12.97.2.14-8.47.pth, mybk
BLEU = 9.90, 34.4/13.8/6.4/3.2 (BP=1.000, ratio=1.090, hyp_len=12462, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.56.2.00-7.41.1.87-6.50.2.56-12.97.2.14-8.47.pth, bkmy
BLEU = 14.48, 42.1/20.0/9.9/5.3 (BP=1.000, ratio=1.087, hyp_len=13290, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.57.2.05-7.78.1.92-6.85.2.60-13.43.2.15-8.59.pth, mybk
BLEU = 9.66, 33.5/13.3/6.3/3.1 (BP=1.000, ratio=1.105, hyp_len=12637, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.57.2.05-7.78.1.92-6.85.2.60-13.43.2.15-8.59.pth, bkmy
BLEU = 15.02, 42.9/20.9/10.5/5.4 (BP=1.000, ratio=1.068, hyp_len=13064, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.58.2.01-7.45.1.86-6.42.2.55-12.74.2.12-8.30.pth, mybk
BLEU = 10.15, 35.5/14.2/6.6/3.2 (BP=1.000, ratio=1.061, hyp_len=12129, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.58.2.01-7.45.1.86-6.42.2.55-12.74.2.12-8.30.pth, bkmy
BLEU = 15.51, 43.3/21.5/10.9/5.7 (BP=1.000, ratio=1.060, hyp_len=12963, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.59.2.01-7.43.1.90-6.71.2.54-12.64.2.12-8.31.pth, mybk
BLEU = 10.17, 34.8/14.2/6.8/3.2 (BP=1.000, ratio=1.084, hyp_len=12395, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.59.2.01-7.43.1.90-6.71.2.54-12.64.2.12-8.31.pth, bkmy
BLEU = 15.54, 43.1/21.2/10.9/5.9 (BP=1.000, ratio=1.094, hyp_len=13375, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.60.1.96-7.11.1.85-6.34.2.60-13.47.2.09-8.08.pth, mybk
BLEU = 9.68, 33.7/13.5/6.2/3.1 (BP=1.000, ratio=1.105, hyp_len=12635, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.60.1.96-7.11.1.85-6.34.2.60-13.47.2.09-8.08.pth, bkmy
BLEU = 16.35, 45.0/22.4/11.5/6.2 (BP=1.000, ratio=1.029, hyp_len=12581, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.61.1.94-6.99.1.83-6.23.2.54-12.73.2.11-8.21.pth, mybk
BLEU = 10.09, 35.3/14.2/6.7/3.1 (BP=1.000, ratio=1.070, hyp_len=12233, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.61.1.94-6.99.1.83-6.23.2.54-12.73.2.11-8.21.pth, bkmy
BLEU = 16.57, 44.2/22.4/11.8/6.5 (BP=1.000, ratio=1.085, hyp_len=13273, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.62.1.95-7.06.1.83-6.21.2.60-13.47.2.09-8.13.pth, mybk
BLEU = 9.63, 34.1/13.3/6.2/3.1 (BP=1.000, ratio=1.114, hyp_len=12733, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.62.1.95-7.06.1.83-6.21.2.60-13.47.2.09-8.13.pth, bkmy
BLEU = 15.80, 44.1/21.8/11.0/5.9 (BP=1.000, ratio=1.060, hyp_len=12963, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.63.1.95-7.06.1.78-5.95.2.56-12.90.2.08-8.04.pth, mybk
BLEU = 9.88, 34.5/13.7/6.5/3.1 (BP=1.000, ratio=1.095, hyp_len=12520, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.63.1.95-7.06.1.78-5.95.2.56-12.90.2.08-8.04.pth, bkmy
BLEU = 16.26, 43.8/22.0/11.5/6.3 (BP=1.000, ratio=1.079, hyp_len=13200, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.64.1.91-6.77.1.78-5.94.2.57-13.09.2.09-8.09.pth, mybk
BLEU = 10.22, 35.4/14.2/6.7/3.2 (BP=1.000, ratio=1.074, hyp_len=12279, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.64.1.91-6.77.1.78-5.94.2.57-13.09.2.09-8.09.pth, bkmy
BLEU = 16.50, 44.6/22.4/11.7/6.3 (BP=1.000, ratio=1.076, hyp_len=13162, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.65.1.85-6.36.1.73-5.66.2.58-13.24.2.12-8.29.pth, mybk
BLEU = 9.95, 35.3/14.0/6.4/3.1 (BP=1.000, ratio=1.087, hyp_len=12431, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.65.1.85-6.36.1.73-5.66.2.58-13.24.2.12-8.29.pth, bkmy
BLEU = 16.40, 44.5/22.1/11.5/6.4 (BP=1.000, ratio=1.055, hyp_len=12902, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.66.1.86-6.42.1.74-5.72.2.56-12.99.2.11-8.24.pth, mybk
BLEU = 9.80, 34.7/13.6/6.2/3.1 (BP=1.000, ratio=1.074, hyp_len=12274, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.66.1.86-6.42.1.74-5.72.2.56-12.99.2.11-8.24.pth, bkmy
BLEU = 16.63, 44.9/22.6/11.8/6.4 (BP=1.000, ratio=1.061, hyp_len=12976, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.67.1.87-6.46.1.76-5.83.2.60-13.53.2.13-8.38.pth, mybk
BLEU = 10.26, 35.1/14.0/6.7/3.4 (BP=1.000, ratio=1.093, hyp_len=12498, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.67.1.87-6.46.1.76-5.83.2.60-13.53.2.13-8.38.pth, bkmy
BLEU = 16.86, 44.5/22.6/12.0/6.7 (BP=1.000, ratio=1.054, hyp_len=12893, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.68.1.84-6.33.1.75-5.74.2.60-13.44.2.11-8.28.pth, mybk
BLEU = 9.96, 34.7/13.8/6.4/3.2 (BP=1.000, ratio=1.091, hyp_len=12478, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.68.1.84-6.33.1.75-5.74.2.60-13.44.2.11-8.28.pth, bkmy
BLEU = 16.65, 44.6/22.5/11.9/6.4 (BP=1.000, ratio=1.045, hyp_len=12787, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.69.1.79-6.02.1.66-5.27.2.59-13.31.2.10-8.14.pth, mybk
BLEU = 10.89, 35.2/14.6/7.3/3.8 (BP=1.000, ratio=1.085, hyp_len=12405, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.69.1.79-6.02.1.66-5.27.2.59-13.31.2.10-8.14.pth, bkmy
BLEU = 16.56, 44.1/22.3/11.8/6.5 (BP=1.000, ratio=1.087, hyp_len=13297, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.70.1.80-6.04.1.67-5.34.2.58-13.24.2.09-8.12.pth, mybk
BLEU = 10.72, 35.8/14.7/7.1/3.6 (BP=1.000, ratio=1.073, hyp_len=12270, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.70.1.80-6.04.1.67-5.34.2.58-13.24.2.09-8.12.pth, bkmy
BLEU = 16.74, 44.6/22.6/11.9/6.5 (BP=1.000, ratio=1.074, hyp_len=13141, ref_len=12231)
```

Best BLEU Score for my-bk, 69 epoch: 10.89  
Best BLEU Score for bk-my, 67 epoch: 16.86  

## Seq2Seq-DSL, my-bk, 80epoch

training

```
Epoch 1 - |param|=8.51e+02 |g_param|=5.14e+05 loss_x2y=4.8867e+00 ppl_x2y=132.52 loss_y2x=4.7388e+00 ppl_y2x=114.30 dual_loss=0.0000e+00
Validation X2Y - loss=4.0326e+00 ppl=56.41 best_loss=inf best_ppl=inf
Validation Y2X - loss=3.9613e+00 ppl=52.52 best_loss=inf best_ppl=inf
Epoch 2 - |param|=8.51e+02 |g_param|=4.87e+05 loss_x2y=4.5266e+00 ppl_x2y=92.45 loss_y2x=4.3306e+00 ppl_y2x=75.99 dual_loss=0.0000e+00
Validation X2Y - loss=3.9338e+00 ppl=51.10 best_loss=4.0326e+00 best_ppl=56.41
Validation Y2X - loss=3.8382e+00 ppl=46.44 best_loss=3.9613e+00 best_ppl=52.52
Epoch 3 - |param|=8.51e+02 |g_param|=2.47e+05 loss_x2y=4.3484e+00 ppl_x2y=77.36 loss_y2x=4.1367e+00 ppl_y2x=62.60 dual_loss=0.0000e+00
Validation X2Y - loss=3.8698e+00 ppl=47.93 best_loss=3.9338e+00 best_ppl=51.10
Validation Y2X - loss=3.7771e+00 ppl=43.69 best_loss=3.8382e+00 best_ppl=46.44
Epoch 4 - |param|=8.51e+02 |g_param|=2.22e+05 loss_x2y=4.3539e+00 ppl_x2y=77.78 loss_y2x=4.1094e+00 ppl_y2x=60.91 dual_loss=0.0000e+00
Validation X2Y - loss=3.8318e+00 ppl=46.15 best_loss=3.8698e+00 best_ppl=47.93
Validation Y2X - loss=3.7151e+00 ppl=41.06 best_loss=3.7771e+00 best_ppl=43.69
Epoch 5 - |param|=8.51e+02 |g_param|=2.24e+05 loss_x2y=4.3065e+00 ppl_x2y=74.18 loss_y2x=4.0923e+00 ppl_y2x=59.88 dual_loss=0.0000e+00
Validation X2Y - loss=3.7960e+00 ppl=44.52 best_loss=3.8318e+00 best_ppl=46.15
Validation Y2X - loss=3.7123e+00 ppl=40.95 best_loss=3.7151e+00 best_ppl=41.06
Epoch 6 - |param|=8.51e+02 |g_param|=2.50e+05 loss_x2y=4.3117e+00 ppl_x2y=74.57 loss_y2x=4.0749e+00 ppl_y2x=58.84 dual_loss=0.0000e+00
Validation X2Y - loss=3.8065e+00 ppl=44.99 best_loss=3.7960e+00 best_ppl=44.52
Validation Y2X - loss=3.7245e+00 ppl=41.45 best_loss=3.7123e+00 best_ppl=40.95
Epoch 7 - |param|=8.52e+02 |g_param|=2.39e+05 loss_x2y=4.3244e+00 ppl_x2y=75.52 loss_y2x=4.1100e+00 ppl_y2x=60.95 dual_loss=0.0000e+00
Validation X2Y - loss=3.8019e+00 ppl=44.79 best_loss=3.7960e+00 best_ppl=44.52
Validation Y2X - loss=3.6736e+00 ppl=39.39 best_loss=3.7123e+00 best_ppl=40.95
Epoch 8 - |param|=8.52e+02 |g_param|=2.24e+05 loss_x2y=4.2563e+00 ppl_x2y=70.55 loss_y2x=4.0476e+00 ppl_y2x=57.26 dual_loss=0.0000e+00
Validation X2Y - loss=3.7279e+00 ppl=41.59 best_loss=3.7960e+00 best_ppl=44.52
Validation Y2X - loss=3.6492e+00 ppl=38.44 best_loss=3.6736e+00 best_ppl=39.39
Epoch 9 - |param|=8.52e+02 |g_param|=2.36e+05 loss_x2y=4.1960e+00 ppl_x2y=66.42 loss_y2x=3.9982e+00 ppl_y2x=54.50 dual_loss=0.0000e+00
Validation X2Y - loss=3.6737e+00 ppl=39.40 best_loss=3.7279e+00 best_ppl=41.59
Validation Y2X - loss=3.6217e+00 ppl=37.40 best_loss=3.6492e+00 best_ppl=38.44
Epoch 10 - |param|=8.53e+02 |g_param|=2.13e+05 loss_x2y=4.0793e+00 ppl_x2y=59.10 loss_y2x=3.9543e+00 ppl_y2x=52.16 dual_loss=0.0000e+00
Validation X2Y - loss=3.5358e+00 ppl=34.32 best_loss=3.6737e+00 best_ppl=39.40
Validation Y2X - loss=3.5571e+00 ppl=35.06 best_loss=3.6217e+00 best_ppl=37.40
Epoch 11 - |param|=8.54e+02 |g_param|=1.73e+05 loss_x2y=3.9421e+00 ppl_x2y=51.52 loss_y2x=3.8534e+00 ppl_y2x=47.15 dual_loss=0.0000e+00
Validation X2Y - loss=3.4137e+00 ppl=30.38 best_loss=3.5358e+00 best_ppl=34.32
Validation Y2X - loss=3.4076e+00 ppl=30.19 best_loss=3.5571e+00 best_ppl=35.06
Epoch 12 - |param|=8.54e+02 |g_param|=1.69e+05 loss_x2y=3.8890e+00 ppl_x2y=48.86 loss_y2x=3.6819e+00 ppl_y2x=39.72 dual_loss=0.0000e+00
Validation X2Y - loss=3.3358e+00 ppl=28.10 best_loss=3.4137e+00 best_ppl=30.38
Validation Y2X - loss=3.2208e+00 ppl=25.05 best_loss=3.4076e+00 best_ppl=30.19
Epoch 13 - |param|=8.55e+02 |g_param|=1.65e+05 loss_x2y=3.8613e+00 ppl_x2y=47.53 loss_y2x=3.5452e+00 ppl_y2x=34.65 dual_loss=0.0000e+00
Validation X2Y - loss=3.2964e+00 ppl=27.02 best_loss=3.3358e+00 best_ppl=28.10
Validation Y2X - loss=3.1408e+00 ppl=23.12 best_loss=3.2208e+00 best_ppl=25.05
Epoch 14 - |param|=8.55e+02 |g_param|=1.69e+05 loss_x2y=3.7114e+00 ppl_x2y=40.91 loss_y2x=3.3944e+00 ppl_y2x=29.80 dual_loss=0.0000e+00
Validation X2Y - loss=3.2606e+00 ppl=26.07 best_loss=3.2964e+00 best_ppl=27.02
Validation Y2X - loss=3.0859e+00 ppl=21.89 best_loss=3.1408e+00 best_ppl=23.12
Epoch 15 - |param|=8.56e+02 |g_param|=1.51e+05 loss_x2y=3.6661e+00 ppl_x2y=39.10 loss_y2x=3.3348e+00 ppl_y2x=28.07 dual_loss=0.0000e+00
Validation X2Y - loss=3.1735e+00 ppl=23.89 best_loss=3.2606e+00 best_ppl=26.07
Validation Y2X - loss=3.0038e+00 ppl=20.16 best_loss=3.0859e+00 best_ppl=21.89
Epoch 16 - |param|=8.56e+02 |g_param|=1.75e+05 loss_x2y=3.6044e+00 ppl_x2y=36.76 loss_y2x=3.2678e+00 ppl_y2x=26.25 dual_loss=0.0000e+00
Validation X2Y - loss=3.1508e+00 ppl=23.35 best_loss=3.1735e+00 best_ppl=23.89
Validation Y2X - loss=2.9658e+00 ppl=19.41 best_loss=3.0038e+00 best_ppl=20.16
Epoch 17 - |param|=8.57e+02 |g_param|=1.55e+05 loss_x2y=3.5312e+00 ppl_x2y=34.16 loss_y2x=3.1987e+00 ppl_y2x=24.50 dual_loss=0.0000e+00
Validation X2Y - loss=3.0694e+00 ppl=21.53 best_loss=3.1508e+00 best_ppl=23.35
Validation Y2X - loss=2.9257e+00 ppl=18.65 best_loss=2.9658e+00 best_ppl=19.41
Epoch 18 - |param|=8.58e+02 |g_param|=1.53e+05 loss_x2y=3.4842e+00 ppl_x2y=32.60 loss_y2x=3.1867e+00 ppl_y2x=24.21 dual_loss=0.0000e+00
Validation X2Y - loss=3.0198e+00 ppl=20.49 best_loss=3.0694e+00 best_ppl=21.53
Validation Y2X - loss=2.9044e+00 ppl=18.25 best_loss=2.9257e+00 best_ppl=18.65
Epoch 19 - |param|=8.58e+02 |g_param|=1.66e+05 loss_x2y=3.5020e+00 ppl_x2y=33.18 loss_y2x=3.1504e+00 ppl_y2x=23.34 dual_loss=0.0000e+00
Validation X2Y - loss=3.0044e+00 ppl=20.17 best_loss=3.0198e+00 best_ppl=20.49
Validation Y2X - loss=2.8640e+00 ppl=17.53 best_loss=2.9044e+00 best_ppl=18.25
Epoch 20 - |param|=8.59e+02 |g_param|=1.69e+05 loss_x2y=3.3862e+00 ppl_x2y=29.55 loss_y2x=3.0862e+00 ppl_y2x=21.89 dual_loss=0.0000e+00
Validation X2Y - loss=2.9432e+00 ppl=18.98 best_loss=3.0044e+00 best_ppl=20.17
Validation Y2X - loss=2.8359e+00 ppl=17.05 best_loss=2.8640e+00 best_ppl=17.53
Epoch 21 - |param|=8.60e+02 |g_param|=1.62e+05 loss_x2y=3.3801e+00 ppl_x2y=29.37 loss_y2x=3.0986e+00 ppl_y2x=22.17 dual_loss=7.0354e-01
Validation X2Y - loss=2.9567e+00 ppl=19.23 best_loss=2.9432e+00 best_ppl=18.98
Validation Y2X - loss=2.8245e+00 ppl=16.85 best_loss=2.8359e+00 best_ppl=17.05
Epoch 22 - |param|=8.61e+02 |g_param|=1.81e+05 loss_x2y=3.4114e+00 ppl_x2y=30.31 loss_y2x=3.0836e+00 ppl_y2x=21.84 dual_loss=7.3147e-01
Validation X2Y - loss=2.9186e+00 ppl=18.52 best_loss=2.9432e+00 best_ppl=18.98
Validation Y2X - loss=2.7848e+00 ppl=16.20 best_loss=2.8245e+00 best_ppl=16.85
Epoch 23 - |param|=8.61e+02 |g_param|=1.66e+05 loss_x2y=3.2807e+00 ppl_x2y=26.59 loss_y2x=2.9924e+00 ppl_y2x=19.93 dual_loss=5.7935e-01
Validation X2Y - loss=2.8815e+00 ppl=17.84 best_loss=2.9186e+00 best_ppl=18.52
Validation Y2X - loss=2.7557e+00 ppl=15.73 best_loss=2.7848e+00 best_ppl=16.20
Epoch 24 - |param|=8.62e+02 |g_param|=1.80e+05 loss_x2y=3.2828e+00 ppl_x2y=26.65 loss_y2x=2.9433e+00 ppl_y2x=18.98 dual_loss=6.1522e-01
Validation X2Y - loss=2.8233e+00 ppl=16.83 best_loss=2.8815e+00 best_ppl=17.84
Validation Y2X - loss=2.6896e+00 ppl=14.73 best_loss=2.7557e+00 best_ppl=15.73
Epoch 25 - |param|=8.63e+02 |g_param|=1.77e+05 loss_x2y=3.2890e+00 ppl_x2y=26.82 loss_y2x=3.0276e+00 ppl_y2x=20.65 dual_loss=5.9906e-01
Validation X2Y - loss=2.8091e+00 ppl=16.60 best_loss=2.8233e+00 best_ppl=16.83
Validation Y2X - loss=2.6679e+00 ppl=14.41 best_loss=2.6896e+00 best_ppl=14.73
Epoch 26 - |param|=8.63e+02 |g_param|=1.86e+05 loss_x2y=3.1401e+00 ppl_x2y=23.11 loss_y2x=2.8339e+00 ppl_y2x=17.01 dual_loss=4.5869e-01
Validation X2Y - loss=2.7688e+00 ppl=15.94 best_loss=2.8091e+00 best_ppl=16.60
Validation Y2X - loss=2.6348e+00 ppl=13.94 best_loss=2.6679e+00 best_ppl=14.41
Epoch 27 - |param|=8.64e+02 |g_param|=1.74e+05 loss_x2y=3.1234e+00 ppl_x2y=22.72 loss_y2x=2.8568e+00 ppl_y2x=17.41 dual_loss=4.6336e-01
Validation X2Y - loss=2.7476e+00 ppl=15.61 best_loss=2.7688e+00 best_ppl=15.94
Validation Y2X - loss=2.5714e+00 ppl=13.08 best_loss=2.6348e+00 best_ppl=13.94
Epoch 28 - |param|=8.65e+02 |g_param|=1.94e+05 loss_x2y=3.0776e+00 ppl_x2y=21.71 loss_y2x=2.7559e+00 ppl_y2x=15.73 dual_loss=4.3807e-01
Validation X2Y - loss=2.7375e+00 ppl=15.45 best_loss=2.7476e+00 best_ppl=15.61
Validation Y2X - loss=2.5731e+00 ppl=13.11 best_loss=2.5714e+00 best_ppl=13.08
Epoch 29 - |param|=8.65e+02 |g_param|=1.81e+05 loss_x2y=2.9543e+00 ppl_x2y=19.19 loss_y2x=2.6870e+00 ppl_y2x=14.69 dual_loss=4.0264e-01
Validation X2Y - loss=2.7147e+00 ppl=15.10 best_loss=2.7375e+00 best_ppl=15.45
Validation Y2X - loss=2.5295e+00 ppl=12.55 best_loss=2.5714e+00 best_ppl=13.08
Epoch 30 - |param|=8.66e+02 |g_param|=1.83e+05 loss_x2y=2.9819e+00 ppl_x2y=19.72 loss_y2x=2.6807e+00 ppl_y2x=14.59 dual_loss=4.0070e-01
Validation X2Y - loss=2.7008e+00 ppl=14.89 best_loss=2.7147e+00 best_ppl=15.10
Validation Y2X - loss=2.5298e+00 ppl=12.55 best_loss=2.5295e+00 best_ppl=12.55
Epoch 31 - |param|=8.67e+02 |g_param|=1.87e+05 loss_x2y=2.9230e+00 ppl_x2y=18.60 loss_y2x=2.6284e+00 ppl_y2x=13.85 dual_loss=3.5554e-01
Validation X2Y - loss=2.6699e+00 ppl=14.44 best_loss=2.7008e+00 best_ppl=14.89
Validation Y2X - loss=2.4866e+00 ppl=12.02 best_loss=2.5295e+00 best_ppl=12.55
Epoch 32 - |param|=8.68e+02 |g_param|=1.90e+05 loss_x2y=2.8608e+00 ppl_x2y=17.48 loss_y2x=2.5777e+00 ppl_y2x=13.17 dual_loss=3.3766e-01
Validation X2Y - loss=2.6361e+00 ppl=13.96 best_loss=2.6699e+00 best_ppl=14.44
Validation Y2X - loss=2.4891e+00 ppl=12.05 best_loss=2.4866e+00 best_ppl=12.02
Epoch 33 - |param|=8.68e+02 |g_param|=1.88e+05 loss_x2y=2.8184e+00 ppl_x2y=16.75 loss_y2x=2.5197e+00 ppl_y2x=12.43 dual_loss=3.3002e-01
Validation X2Y - loss=2.6146e+00 ppl=13.66 best_loss=2.6361e+00 best_ppl=13.96
Validation Y2X - loss=2.4550e+00 ppl=11.65 best_loss=2.4866e+00 best_ppl=12.02
Epoch 34 - |param|=8.69e+02 |g_param|=1.92e+05 loss_x2y=2.8436e+00 ppl_x2y=17.18 loss_y2x=2.5924e+00 ppl_y2x=13.36 dual_loss=3.5738e-01
Validation X2Y - loss=2.6026e+00 ppl=13.50 best_loss=2.6146e+00 best_ppl=13.66
Validation Y2X - loss=2.4477e+00 ppl=11.56 best_loss=2.4550e+00 best_ppl=11.65
Epoch 35 - |param|=8.70e+02 |g_param|=3.46e+05 loss_x2y=2.8261e+00 ppl_x2y=16.88 loss_y2x=2.5233e+00 ppl_y2x=12.47 dual_loss=3.0868e-01
Validation X2Y - loss=2.5802e+00 ppl=13.20 best_loss=2.6026e+00 best_ppl=13.50
Validation Y2X - loss=2.4202e+00 ppl=11.25 best_loss=2.4477e+00 best_ppl=11.56
Epoch 36 - |param|=8.70e+02 |g_param|=4.10e+05 loss_x2y=2.7207e+00 ppl_x2y=15.19 loss_y2x=2.4039e+00 ppl_y2x=11.07 dual_loss=2.9768e-01
Validation X2Y - loss=2.5770e+00 ppl=13.16 best_loss=2.5802e+00 best_ppl=13.20
Validation Y2X - loss=2.3955e+00 ppl=10.97 best_loss=2.4202e+00 best_ppl=11.25
Epoch 37 - |param|=8.71e+02 |g_param|=3.98e+05 loss_x2y=2.7032e+00 ppl_x2y=14.93 loss_y2x=2.3907e+00 ppl_y2x=10.92 dual_loss=3.1222e-01
Validation X2Y - loss=2.5452e+00 ppl=12.75 best_loss=2.5770e+00 best_ppl=13.16
Validation Y2X - loss=2.3802e+00 ppl=10.81 best_loss=2.3955e+00 best_ppl=10.97
Epoch 38 - |param|=8.72e+02 |g_param|=4.15e+05 loss_x2y=2.6515e+00 ppl_x2y=14.18 loss_y2x=2.3430e+00 ppl_y2x=10.41 dual_loss=2.8570e-01
Validation X2Y - loss=2.5509e+00 ppl=12.82 best_loss=2.5452e+00 best_ppl=12.75
Validation Y2X - loss=2.3790e+00 ppl=10.79 best_loss=2.3802e+00 best_ppl=10.81
Epoch 39 - |param|=8.72e+02 |g_param|=4.17e+05 loss_x2y=2.6131e+00 ppl_x2y=13.64 loss_y2x=2.2929e+00 ppl_y2x=9.90 dual_loss=2.9016e-01
Validation X2Y - loss=2.5262e+00 ppl=12.51 best_loss=2.5452e+00 best_ppl=12.75
Validation Y2X - loss=2.3740e+00 ppl=10.74 best_loss=2.3790e+00 best_ppl=10.79
Epoch 40 - |param|=8.73e+02 |g_param|=4.58e+05 loss_x2y=2.7135e+00 ppl_x2y=15.08 loss_y2x=2.4462e+00 ppl_y2x=11.54 dual_loss=3.3748e-01
Validation X2Y - loss=2.5112e+00 ppl=12.32 best_loss=2.5262e+00 best_ppl=12.51
Validation Y2X - loss=2.3751e+00 ppl=10.75 best_loss=2.3740e+00 best_ppl=10.74
Epoch 41 - |param|=8.74e+02 |g_param|=4.12e+05 loss_x2y=2.5480e+00 ppl_x2y=12.78 loss_y2x=2.2572e+00 ppl_y2x=9.56 dual_loss=2.7039e-01
Validation X2Y - loss=2.4974e+00 ppl=12.15 best_loss=2.5112e+00 best_ppl=12.32
Validation Y2X - loss=2.3604e+00 ppl=10.60 best_loss=2.3740e+00 best_ppl=10.74
Epoch 42 - |param|=8.74e+02 |g_param|=4.37e+05 loss_x2y=2.4961e+00 ppl_x2y=12.14 loss_y2x=2.2025e+00 ppl_y2x=9.05 dual_loss=2.7326e-01
Validation X2Y - loss=2.4747e+00 ppl=11.88 best_loss=2.4974e+00 best_ppl=12.15
Validation Y2X - loss=2.3292e+00 ppl=10.27 best_loss=2.3604e+00 best_ppl=10.60
Epoch 43 - |param|=8.75e+02 |g_param|=4.35e+05 loss_x2y=2.4617e+00 ppl_x2y=11.72 loss_y2x=2.1959e+00 ppl_y2x=8.99 dual_loss=2.5565e-01
Validation X2Y - loss=2.4685e+00 ppl=11.81 best_loss=2.4747e+00 best_ppl=11.88
Validation Y2X - loss=2.3397e+00 ppl=10.38 best_loss=2.3292e+00 best_ppl=10.27
Epoch 44 - |param|=8.75e+02 |g_param|=4.54e+05 loss_x2y=2.5325e+00 ppl_x2y=12.59 loss_y2x=2.2046e+00 ppl_y2x=9.07 dual_loss=2.6949e-01
Validation X2Y - loss=2.4668e+00 ppl=11.78 best_loss=2.4685e+00 best_ppl=11.81
Validation Y2X - loss=2.3111e+00 ppl=10.09 best_loss=2.3292e+00 best_ppl=10.27
Epoch 45 - |param|=8.76e+02 |g_param|=4.42e+05 loss_x2y=2.4319e+00 ppl_x2y=11.38 loss_y2x=2.1574e+00 ppl_y2x=8.65 dual_loss=2.5350e-01
Validation X2Y - loss=2.4661e+00 ppl=11.78 best_loss=2.4668e+00 best_ppl=11.78
Validation Y2X - loss=2.2994e+00 ppl=9.97 best_loss=2.3111e+00 best_ppl=10.09
Epoch 46 - |param|=8.77e+02 |g_param|=4.91e+05 loss_x2y=2.4609e+00 ppl_x2y=11.71 loss_y2x=2.1731e+00 ppl_y2x=8.79 dual_loss=2.7044e-01
Validation X2Y - loss=2.4431e+00 ppl=11.51 best_loss=2.4661e+00 best_ppl=11.78
Validation Y2X - loss=2.2995e+00 ppl=9.97 best_loss=2.2994e+00 best_ppl=9.97
Epoch 47 - |param|=8.77e+02 |g_param|=4.53e+05 loss_x2y=2.4662e+00 ppl_x2y=11.78 loss_y2x=2.1487e+00 ppl_y2x=8.57 dual_loss=2.6203e-01
Validation X2Y - loss=2.4252e+00 ppl=11.30 best_loss=2.4431e+00 best_ppl=11.51
Validation Y2X - loss=2.3074e+00 ppl=10.05 best_loss=2.2994e+00 best_ppl=9.97
Epoch 48 - |param|=8.78e+02 |g_param|=4.62e+05 loss_x2y=2.3224e+00 ppl_x2y=10.20 loss_y2x=2.0649e+00 ppl_y2x=7.88 dual_loss=2.5505e-01
Validation X2Y - loss=2.4332e+00 ppl=11.40 best_loss=2.4252e+00 best_ppl=11.30
Validation Y2X - loss=2.3144e+00 ppl=10.12 best_loss=2.2994e+00 best_ppl=9.97
Epoch 49 - |param|=8.79e+02 |g_param|=4.48e+05 loss_x2y=2.3526e+00 ppl_x2y=10.51 loss_y2x=2.0790e+00 ppl_y2x=8.00 dual_loss=2.7035e-01
Validation X2Y - loss=2.4090e+00 ppl=11.12 best_loss=2.4252e+00 best_ppl=11.30
Validation Y2X - loss=2.3066e+00 ppl=10.04 best_loss=2.2994e+00 best_ppl=9.97
Epoch 50 - |param|=8.79e+02 |g_param|=4.86e+05 loss_x2y=2.3122e+00 ppl_x2y=10.10 loss_y2x=2.0230e+00 ppl_y2x=7.56 dual_loss=2.6984e-01
Validation X2Y - loss=2.4088e+00 ppl=11.12 best_loss=2.4090e+00 best_ppl=11.12
Validation Y2X - loss=2.2883e+00 ppl=9.86 best_loss=2.2994e+00 best_ppl=9.97
Epoch 51 - |param|=8.80e+02 |g_param|=4.66e+05 loss_x2y=2.2707e+00 ppl_x2y=9.69 loss_y2x=2.0203e+00 ppl_y2x=7.54 dual_loss=2.7467e-01
Validation X2Y - loss=2.4352e+00 ppl=11.42 best_loss=2.4088e+00 best_ppl=11.12
Validation Y2X - loss=2.3069e+00 ppl=10.04 best_loss=2.2883e+00 best_ppl=9.86
Epoch 52 - |param|=8.80e+02 |g_param|=5.06e+05 loss_x2y=2.2648e+00 ppl_x2y=9.63 loss_y2x=2.0085e+00 ppl_y2x=7.45 dual_loss=2.5517e-01
Validation X2Y - loss=2.4032e+00 ppl=11.06 best_loss=2.4088e+00 best_ppl=11.12
Validation Y2X - loss=2.2901e+00 ppl=9.88 best_loss=2.2883e+00 best_ppl=9.86
Epoch 53 - |param|=8.81e+02 |g_param|=4.82e+05 loss_x2y=2.2644e+00 ppl_x2y=9.63 loss_y2x=1.9880e+00 ppl_y2x=7.30 dual_loss=2.6672e-01
Validation X2Y - loss=2.4029e+00 ppl=11.06 best_loss=2.4032e+00 best_ppl=11.06
Validation Y2X - loss=2.3112e+00 ppl=10.09 best_loss=2.2883e+00 best_ppl=9.86
Epoch 54 - |param|=8.82e+02 |g_param|=4.86e+05 loss_x2y=2.1915e+00 ppl_x2y=8.95 loss_y2x=1.9391e+00 ppl_y2x=6.95 dual_loss=2.5879e-01
Validation X2Y - loss=2.4053e+00 ppl=11.08 best_loss=2.4029e+00 best_ppl=11.06
Validation Y2X - loss=2.2810e+00 ppl=9.79 best_loss=2.2883e+00 best_ppl=9.86
Epoch 55 - |param|=8.82e+02 |g_param|=5.22e+05 loss_x2y=2.2363e+00 ppl_x2y=9.36 loss_y2x=2.0257e+00 ppl_y2x=7.58 dual_loss=2.8185e-01
Validation X2Y - loss=2.3883e+00 ppl=10.90 best_loss=2.4029e+00 best_ppl=11.06
Validation Y2X - loss=2.2815e+00 ppl=9.79 best_loss=2.2810e+00 best_ppl=9.79
Epoch 56 - |param|=8.83e+02 |g_param|=5.23e+05 loss_x2y=2.2249e+00 ppl_x2y=9.25 loss_y2x=1.9403e+00 ppl_y2x=6.96 dual_loss=2.6381e-01
Validation X2Y - loss=2.3779e+00 ppl=10.78 best_loss=2.3883e+00 best_ppl=10.90
Validation Y2X - loss=2.2796e+00 ppl=9.77 best_loss=2.2810e+00 best_ppl=9.79
Epoch 57 - |param|=8.84e+02 |g_param|=5.11e+05 loss_x2y=2.1521e+00 ppl_x2y=8.60 loss_y2x=1.9069e+00 ppl_y2x=6.73 dual_loss=2.7711e-01
Validation X2Y - loss=2.4004e+00 ppl=11.03 best_loss=2.3779e+00 best_ppl=10.78
Validation Y2X - loss=2.2826e+00 ppl=9.80 best_loss=2.2796e+00 best_ppl=9.77
Epoch 58 - |param|=8.84e+02 |g_param|=5.11e+05 loss_x2y=2.1003e+00 ppl_x2y=8.17 loss_y2x=1.8440e+00 ppl_y2x=6.32 dual_loss=2.5668e-01
Validation X2Y - loss=2.3828e+00 ppl=10.84 best_loss=2.3779e+00 best_ppl=10.78
Validation Y2X - loss=2.2886e+00 ppl=9.86 best_loss=2.2796e+00 best_ppl=9.77
Epoch 59 - |param|=8.85e+02 |g_param|=5.16e+05 loss_x2y=2.0720e+00 ppl_x2y=7.94 loss_y2x=1.8564e+00 ppl_y2x=6.40 dual_loss=2.7135e-01
Validation X2Y - loss=2.3874e+00 ppl=10.89 best_loss=2.3779e+00 best_ppl=10.78
Validation Y2X - loss=2.2835e+00 ppl=9.81 best_loss=2.2796e+00 best_ppl=9.77
Epoch 60 - |param|=8.85e+02 |g_param|=5.39e+05 loss_x2y=2.1492e+00 ppl_x2y=8.58 loss_y2x=1.8604e+00 ppl_y2x=6.43 dual_loss=2.7928e-01
Validation X2Y - loss=2.3919e+00 ppl=10.93 best_loss=2.3779e+00 best_ppl=10.78
Validation Y2X - loss=2.2667e+00 ppl=9.65 best_loss=2.2796e+00 best_ppl=9.77
Epoch 61 - |param|=8.86e+02 |g_param|=5.08e+05 loss_x2y=2.0340e+00 ppl_x2y=7.64 loss_y2x=1.7942e+00 ppl_y2x=6.01 dual_loss=2.8114e-01
Validation X2Y - loss=2.3842e+00 ppl=10.85 best_loss=2.3779e+00 best_ppl=10.78
Validation Y2X - loss=2.2768e+00 ppl=9.75 best_loss=2.2667e+00 best_ppl=9.65
Epoch 62 - |param|=8.86e+02 |g_param|=5.46e+05 loss_x2y=2.0170e+00 ppl_x2y=7.52 loss_y2x=1.7949e+00 ppl_y2x=6.02 dual_loss=2.7452e-01
Validation X2Y - loss=2.3803e+00 ppl=10.81 best_loss=2.3779e+00 best_ppl=10.78
Validation Y2X - loss=2.2920e+00 ppl=9.89 best_loss=2.2667e+00 best_ppl=9.65
Epoch 63 - |param|=8.87e+02 |g_param|=5.19e+05 loss_x2y=1.9877e+00 ppl_x2y=7.30 loss_y2x=1.7505e+00 ppl_y2x=5.76 dual_loss=2.8337e-01
Validation X2Y - loss=2.3758e+00 ppl=10.76 best_loss=2.3779e+00 best_ppl=10.78
Validation Y2X - loss=2.2988e+00 ppl=9.96 best_loss=2.2667e+00 best_ppl=9.65
Epoch 64 - |param|=8.88e+02 |g_param|=5.64e+05 loss_x2y=2.0689e+00 ppl_x2y=7.92 loss_y2x=1.8600e+00 ppl_y2x=6.42 dual_loss=3.1565e-01
Validation X2Y - loss=2.3770e+00 ppl=10.77 best_loss=2.3758e+00 best_ppl=10.76
Validation Y2X - loss=2.3017e+00 ppl=9.99 best_loss=2.2667e+00 best_ppl=9.65
Epoch 65 - |param|=8.88e+02 |g_param|=5.41e+05 loss_x2y=2.0049e+00 ppl_x2y=7.43 loss_y2x=1.8053e+00 ppl_y2x=6.08 dual_loss=2.9028e-01
Validation X2Y - loss=2.3747e+00 ppl=10.75 best_loss=2.3758e+00 best_ppl=10.76
Validation Y2X - loss=2.2575e+00 ppl=9.56 best_loss=2.2667e+00 best_ppl=9.65
Epoch 66 - |param|=8.89e+02 |g_param|=5.72e+05 loss_x2y=2.0453e+00 ppl_x2y=7.73 loss_y2x=1.7383e+00 ppl_y2x=5.69 dual_loss=2.7376e-01
Validation X2Y - loss=2.3951e+00 ppl=10.97 best_loss=2.3747e+00 best_ppl=10.75
Validation Y2X - loss=2.2730e+00 ppl=9.71 best_loss=2.2575e+00 best_ppl=9.56
Epoch 67 - |param|=8.89e+02 |g_param|=7.38e+05 loss_x2y=1.9118e+00 ppl_x2y=6.77 loss_y2x=1.6530e+00 ppl_y2x=5.22 dual_loss=2.6200e-01
Validation X2Y - loss=2.3869e+00 ppl=10.88 best_loss=2.3747e+00 best_ppl=10.75
Validation Y2X - loss=2.3033e+00 ppl=10.01 best_loss=2.2575e+00 best_ppl=9.56
Epoch 68 - |param|=8.90e+02 |g_param|=1.13e+06 loss_x2y=1.9674e+00 ppl_x2y=7.15 loss_y2x=1.6846e+00 ppl_y2x=5.39 dual_loss=2.9473e-01
Validation X2Y - loss=2.3425e+00 ppl=10.41 best_loss=2.3747e+00 best_ppl=10.75
Validation Y2X - loss=2.2872e+00 ppl=9.85 best_loss=2.2575e+00 best_ppl=9.56
Epoch 69 - |param|=8.91e+02 |g_param|=1.17e+06 loss_x2y=1.9030e+00 ppl_x2y=6.71 loss_y2x=1.6436e+00 ppl_y2x=5.17 dual_loss=2.9973e-01
Validation X2Y - loss=2.3658e+00 ppl=10.65 best_loss=2.3425e+00 best_ppl=10.41
Validation Y2X - loss=2.2952e+00 ppl=9.93 best_loss=2.2575e+00 best_ppl=9.56
Epoch 70 - |param|=8.91e+02 |g_param|=8.16e+05 loss_x2y=1.9707e+00 ppl_x2y=7.18 loss_y2x=1.6431e+00 ppl_y2x=5.17 dual_loss=2.9031e-01
Validation X2Y - loss=2.3802e+00 ppl=10.81 best_loss=2.3425e+00 best_ppl=10.41
Validation Y2X - loss=2.2907e+00 ppl=9.88 best_loss=2.2575e+00 best_ppl=9.56
Epoch 71 - |param|=8.92e+02 |g_param|=7.20e+05 loss_x2y=1.8111e+00 ppl_x2y=6.12 loss_y2x=1.6077e+00 ppl_y2x=4.99 dual_loss=2.8088e-01
Validation X2Y - loss=2.3528e+00 ppl=10.52 best_loss=2.3425e+00 best_ppl=10.41
Validation Y2X - loss=2.2854e+00 ppl=9.83 best_loss=2.2575e+00 best_ppl=9.56
Epoch 72 - |param|=8.92e+02 |g_param|=7.48e+05 loss_x2y=1.8279e+00 ppl_x2y=6.22 loss_y2x=1.6220e+00 ppl_y2x=5.06 dual_loss=2.9009e-01
Validation X2Y - loss=2.3550e+00 ppl=10.54 best_loss=2.3425e+00 best_ppl=10.41
Validation Y2X - loss=2.2876e+00 ppl=9.85 best_loss=2.2575e+00 best_ppl=9.56
Epoch 73 - |param|=8.93e+02 |g_param|=7.53e+05 loss_x2y=1.8592e+00 ppl_x2y=6.42 loss_y2x=1.6006e+00 ppl_y2x=4.96 dual_loss=3.0727e-01
Validation X2Y - loss=2.3561e+00 ppl=10.55 best_loss=2.3425e+00 best_ppl=10.41
Validation Y2X - loss=2.3016e+00 ppl=9.99 best_loss=2.2575e+00 best_ppl=9.56
Epoch 74 - |param|=8.93e+02 |g_param|=7.56e+05 loss_x2y=1.8446e+00 ppl_x2y=6.33 loss_y2x=1.6083e+00 ppl_y2x=4.99 dual_loss=3.1047e-01
Validation X2Y - loss=2.3768e+00 ppl=10.77 best_loss=2.3425e+00 best_ppl=10.41
Validation Y2X - loss=2.3140e+00 ppl=10.12 best_loss=2.2575e+00 best_ppl=9.56
Epoch 75 - |param|=8.94e+02 |g_param|=7.49e+05 loss_x2y=1.8115e+00 ppl_x2y=6.12 loss_y2x=1.6019e+00 ppl_y2x=4.96 dual_loss=3.0621e-01
Validation X2Y - loss=2.3754e+00 ppl=10.76 best_loss=2.3425e+00 best_ppl=10.41
Validation Y2X - loss=2.3157e+00 ppl=10.13 best_loss=2.2575e+00 best_ppl=9.56
Epoch 76 - |param|=8.94e+02 |g_param|=7.56e+05 loss_x2y=1.7675e+00 ppl_x2y=5.86 loss_y2x=1.5544e+00 ppl_y2x=4.73 dual_loss=3.0754e-01
Validation X2Y - loss=2.3865e+00 ppl=10.88 best_loss=2.3425e+00 best_ppl=10.41
Validation Y2X - loss=2.3175e+00 ppl=10.15 best_loss=2.2575e+00 best_ppl=9.56
Epoch 77 - |param|=8.95e+02 |g_param|=7.70e+05 loss_x2y=1.7973e+00 ppl_x2y=6.03 loss_y2x=1.5908e+00 ppl_y2x=4.91 dual_loss=3.1984e-01
Validation X2Y - loss=2.3895e+00 ppl=10.91 best_loss=2.3425e+00 best_ppl=10.41
Validation Y2X - loss=2.3201e+00 ppl=10.18 best_loss=2.2575e+00 best_ppl=9.56
Epoch 78 - |param|=8.96e+02 |g_param|=8.00e+05 loss_x2y=1.7499e+00 ppl_x2y=5.75 loss_y2x=1.5623e+00 ppl_y2x=4.77 dual_loss=3.0957e-01
Validation X2Y - loss=2.3845e+00 ppl=10.85 best_loss=2.3425e+00 best_ppl=10.41
Validation Y2X - loss=2.3060e+00 ppl=10.03 best_loss=2.2575e+00 best_ppl=9.56
Epoch 79 - |param|=8.96e+02 |g_param|=7.48e+05 loss_x2y=1.6988e+00 ppl_x2y=5.47 loss_y2x=1.5047e+00 ppl_y2x=4.50 dual_loss=3.2058e-01
Validation X2Y - loss=2.3672e+00 ppl=10.67 best_loss=2.3425e+00 best_ppl=10.41
Validation Y2X - loss=2.3131e+00 ppl=10.11 best_loss=2.2575e+00 best_ppl=9.56
Epoch 80 - |param|=8.97e+02 |g_param|=8.19e+05 loss_x2y=1.7244e+00 ppl_x2y=5.61 loss_y2x=1.5323e+00 ppl_y2x=4.63 dual_loss=3.2751e-01
Validation X2Y - loss=2.3823e+00 ppl=10.83 best_loss=2.3425e+00 best_ppl=10.41
Validation Y2X - loss=2.3206e+00 ppl=10.18 best_loss=2.2575e+00 best_ppl=9.56
```

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/mybk-80epoch
Evaluation result for the model: dsl-model-mybk.01.4.89-132.52.4.74-114.30.4.03-56.41.3.96-52.52.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.0/0.0/0.0/0.0 (BP=0.834, ratio=0.846, hyp_len=9677, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.89-132.52.4.74-114.30.4.03-56.41.3.96-52.52.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.7/0.1/0.0/0.0 (BP=0.915, ratio=0.919, hyp_len=11235, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.01.4.91-135.30.4.70-109.84.4.08-58.98.3.96-52.34.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.4/0.0/0.0/0.0 (BP=0.649, ratio=0.698, hyp_len=7979, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.91-135.30.4.70-109.84.4.08-58.98.3.96-52.34.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.6/0.3/0.0/0.0 (BP=0.793, ratio=0.811, hyp_len=9924, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.02.4.46-86.17.4.25-70.33.3.90-49.55.3.81-45.16.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.3/0.2/0.0/0.0 (BP=0.967, ratio=0.967, hyp_len=11058, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.4.46-86.17.4.25-70.33.3.90-49.55.3.81-45.16.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.9/0.4/0.0/0.0 (BP=0.983, ratio=0.983, hyp_len=12029, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.02.4.53-92.45.4.33-75.99.3.93-51.10.3.84-46.44.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.6/0.2/0.0/0.0 (BP=1.000, ratio=1.110, hyp_len=12692, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.4.53-92.45.4.33-75.99.3.93-51.10.3.84-46.44.pth, bkmy
BLEU = 0.52, 21.0/2.0/0.2/0.0 (BP=0.930, ratio=0.932, hyp_len=11403, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.4.35-77.36.4.14-62.60.3.87-47.93.3.78-43.69.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.4/0.4/0.0/0.0 (BP=0.986, ratio=0.986, hyp_len=11273, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.4.35-77.36.4.14-62.60.3.87-47.93.3.78-43.69.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.0/0.5/0.0/0.0 (BP=1.000, ratio=1.016, hyp_len=12421, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.4.42-82.90.4.16-64.26.3.87-47.89.3.76-43.00.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.4/0.2/0.0/0.0 (BP=1.000, ratio=1.073, hyp_len=12272, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.4.42-82.90.4.16-64.26.3.87-47.89.3.76-43.00.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.9/0.5/0.0/0.0 (BP=0.969, ratio=0.969, hyp_len=11857, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.4.35-77.78.4.11-60.91.3.83-46.15.3.72-41.06.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.9/0.4/0.0/0.0 (BP=0.985, ratio=0.985, hyp_len=11262, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.4.35-77.78.4.11-60.91.3.83-46.15.3.72-41.06.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.1/0.5/0.0/0.0 (BP=1.000, ratio=1.001, hyp_len=12240, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.4.36-78.00.4.12-61.75.3.88-48.34.3.70-40.34.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.1/0.2/0.0/0.0 (BP=1.000, ratio=1.027, hyp_len=11735, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.4.36-78.00.4.12-61.75.3.88-48.34.3.70-40.34.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.5/0.8/0.0/0.0 (BP=0.998, ratio=0.998, hyp_len=12203, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.4.31-74.18.4.09-59.88.3.80-44.52.3.71-40.95.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.2/0.2/0.0/0.0 (BP=1.000, ratio=1.062, hyp_len=12141, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.4.31-74.18.4.09-59.88.3.80-44.52.3.71-40.95.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.3/0.6/0.0/0.0 (BP=1.000, ratio=1.066, hyp_len=13036, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.4.37-79.10.4.14-62.53.3.81-45.32.3.66-38.80.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.9/0.1/0.0/0.0 (BP=1.000, ratio=1.014, hyp_len=11587, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.4.37-79.10.4.14-62.53.3.81-45.32.3.66-38.80.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.4/0.8/0.1/0.0 (BP=1.000, ratio=1.021, hyp_len=12490, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.4.31-74.57.4.07-58.84.3.81-44.99.3.72-41.45.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.0/0.4/0.0/0.0 (BP=1.000, ratio=1.036, hyp_len=11847, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.4.31-74.57.4.07-58.84.3.81-44.99.3.72-41.45.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.5/0.5/0.0/0.0 (BP=1.000, ratio=1.049, hyp_len=12830, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.4.32-75.43.4.11-60.98.3.83-46.09.3.70-40.39.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 14.8/0.1/0.0/0.0 (BP=1.000, ratio=1.095, hyp_len=12520, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.4.32-75.43.4.11-60.98.3.83-46.09.3.70-40.39.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.9/0.8/0.0/0.0 (BP=1.000, ratio=1.002, hyp_len=12251, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.4.29-72.61.4.09-59.85.3.78-43.77.3.62-37.36.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.3/0.6/0.0/0.0 (BP=1.000, ratio=1.053, hyp_len=12033, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.4.29-72.61.4.09-59.85.3.78-43.77.3.62-37.36.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.6/1.2/0.1/0.0 (BP=1.000, ratio=1.013, hyp_len=12384, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.4.32-75.52.4.11-60.95.3.80-44.79.3.67-39.39.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.0/0.6/0.0/0.0 (BP=1.000, ratio=1.099, hyp_len=12563, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.4.32-75.52.4.11-60.95.3.80-44.79.3.67-39.39.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.2/0.5/0.0/0.0 (BP=1.000, ratio=1.058, hyp_len=12945, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.4.22-68.03.4.03-56.39.3.76-43.10.3.62-37.18.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.9/0.7/0.0/0.0 (BP=1.000, ratio=1.050, hyp_len=12004, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.4.22-68.03.4.03-56.39.3.76-43.10.3.62-37.18.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.9/1.5/0.0/0.0 (BP=1.000, ratio=1.008, hyp_len=12333, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.4.26-70.55.4.05-57.26.3.73-41.59.3.65-38.44.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.2/0.2/0.0/0.0 (BP=1.000, ratio=1.029, hyp_len=11762, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.4.26-70.55.4.05-57.26.3.73-41.59.3.65-38.44.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.7/0.9/0.0/0.0 (BP=1.000, ratio=1.006, hyp_len=12308, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.4.20-66.42.4.00-54.50.3.67-39.40.3.62-37.40.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.4/0.3/0.0/0.0 (BP=1.000, ratio=1.009, hyp_len=11537, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.4.20-66.42.4.00-54.50.3.67-39.40.3.62-37.40.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.0/1.1/0.0/0.0 (BP=1.000, ratio=1.073, hyp_len=13127, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.4.24-69.28.4.08-59.27.3.70-40.40.3.57-35.35.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.6/0.3/0.0/0.0 (BP=0.978, ratio=0.978, hyp_len=11181, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.4.24-69.28.4.08-59.27.3.70-40.40.3.57-35.35.pth, bkmy
BLEU = 0.77, 22.1/2.2/0.3/0.0 (BP=1.000, ratio=1.016, hyp_len=12431, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.4.08-59.10.3.95-52.16.3.54-34.32.3.56-35.06.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 23.5/0.5/0.0/0.0 (BP=0.776, ratio=0.797, hyp_len=9116, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.4.08-59.10.3.95-52.16.3.54-34.32.3.56-35.06.pth, bkmy
BLEU = 0.51, 20.1/1.8/0.2/0.0 (BP=1.000, ratio=1.076, hyp_len=13159, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.4.08-59.14.3.97-52.76.3.52-33.62.3.52-33.92.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 24.8/0.6/0.0/0.0 (BP=0.717, ratio=0.751, hyp_len=8582, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.4.08-59.14.3.97-52.76.3.52-33.62.3.52-33.92.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.4/1.9/0.1/0.0 (BP=1.000, ratio=1.138, hyp_len=13916, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.3.94-51.52.3.85-47.15.3.41-30.38.3.41-30.19.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 26.7/0.6/0.0/0.0 (BP=0.676, ratio=0.719, hyp_len=8215, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.3.94-51.52.3.85-47.15.3.41-30.38.3.41-30.19.pth, bkmy
BLEU = 1.08, 21.0/2.4/0.5/0.1 (BP=0.977, ratio=0.978, hyp_len=11956, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.3.98-53.44.3.86-47.34.3.39-29.56.3.42-30.51.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 27.4/1.6/0.0/0.0 (BP=0.774, ratio=0.796, hyp_len=9097, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.3.98-53.44.3.86-47.34.3.39-29.56.3.42-30.51.pth, bkmy
BLEU = 0.61, 22.3/1.9/0.2/0.0 (BP=1.000, ratio=1.072, hyp_len=13116, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.3.82-45.81.3.69-40.24.3.30-27.15.3.27-26.35.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 26.9/3.7/0.4/0.0 (BP=0.827, ratio=0.840, hyp_len=9607, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.3.82-45.81.3.69-40.24.3.30-27.15.3.27-26.35.pth, bkmy
BLEU = 1.50, 23.8/5.0/0.6/0.1 (BP=1.000, ratio=1.100, hyp_len=13448, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.3.89-48.86.3.68-39.72.3.34-28.10.3.22-25.05.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 25.1/2.3/0.2/0.0 (BP=0.878, ratio=0.885, hyp_len=10118, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.3.89-48.86.3.68-39.72.3.34-28.10.3.22-25.05.pth, bkmy
BLEU = 1.19, 25.0/4.5/0.5/0.0 (BP=0.933, ratio=0.935, hyp_len=11438, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.3.81-44.98.3.55-34.94.3.23-25.34.3.17-23.91.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 25.7/3.8/0.5/0.0 (BP=0.955, ratio=0.956, hyp_len=10932, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.3.81-44.98.3.55-34.94.3.23-25.34.3.17-23.91.pth, bkmy
BLEU = 0.41, 7.5/1.6/0.1/0.0 (BP=1.000, ratio=3.645, hyp_len=44579, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.3.86-47.53.3.55-34.65.3.30-27.02.3.14-23.12.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 24.3/2.6/0.1/0.0 (BP=0.965, ratio=0.965, hyp_len=11036, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.3.86-47.53.3.55-34.65.3.30-27.02.3.14-23.12.pth, bkmy
BLEU = 1.26, 23.8/4.5/0.6/0.0 (BP=1.000, ratio=1.040, hyp_len=12723, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.3.69-40.22.3.43-31.03.3.20-24.57.3.08-21.81.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 24.6/3.8/0.5/0.0 (BP=1.000, ratio=1.042, hyp_len=11911, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.3.69-40.22.3.43-31.03.3.20-24.57.3.08-21.81.pth, bkmy
BLEU = 1.33, 21.5/4.9/0.7/0.0 (BP=1.000, ratio=1.339, hyp_len=16375, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.3.71-40.91.3.39-29.80.3.26-26.07.3.09-21.89.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 23.6/3.1/0.3/0.0 (BP=1.000, ratio=1.034, hyp_len=11822, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.3.71-40.91.3.39-29.80.3.26-26.07.3.09-21.89.pth, bkmy
BLEU = 0.25, 3.5/0.7/0.1/0.0 (BP=1.000, ratio=6.766, hyp_len=82752, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.3.65-38.29.3.39-29.77.3.15-23.43.3.02-20.49.pth, mybk
BLEU = 1.48, 22.8/5.0/1.0/0.0 (BP=1.000, ratio=1.120, hyp_len=12808, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.3.65-38.29.3.39-29.77.3.15-23.43.3.02-20.49.pth, bkmy
BLEU = 0.67, 8.7/2.1/0.4/0.0 (BP=1.000, ratio=3.349, hyp_len=40959, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.3.67-39.10.3.33-28.07.3.17-23.89.3.00-20.16.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 23.6/3.8/0.4/0.0 (BP=1.000, ratio=1.058, hyp_len=12090, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.3.67-39.10.3.33-28.07.3.17-23.89.3.00-20.16.pth, bkmy
BLEU = 1.11, 11.7/2.9/0.5/0.1 (BP=1.000, ratio=2.304, hyp_len=28181, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.3.58-35.74.3.32-27.60.3.12-22.55.3.00-20.12.pth, mybk
BLEU = 3.42, 25.5/6.1/1.9/0.5 (BP=1.000, ratio=1.027, hyp_len=11744, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.3.58-35.74.3.32-27.60.3.12-22.55.3.00-20.12.pth, bkmy
BLEU = 2.01, 19.4/4.7/1.2/0.2 (BP=1.000, ratio=1.649, hyp_len=20175, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.3.60-36.76.3.27-26.25.3.15-23.35.2.97-19.41.pth, mybk
BLEU = 1.98, 24.0/5.2/1.1/0.1 (BP=1.000, ratio=1.080, hyp_len=12351, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.3.60-36.76.3.27-26.25.3.15-23.35.2.97-19.41.pth, bkmy
BLEU = 2.63, 23.4/6.1/1.1/0.3 (BP=1.000, ratio=1.197, hyp_len=14645, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.3.51-33.45.3.24-25.47.3.07-21.65.2.91-18.35.pth, mybk
BLEU = 3.93, 26.5/6.7/2.1/0.6 (BP=1.000, ratio=1.042, hyp_len=11908, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.3.51-33.45.3.24-25.47.3.07-21.65.2.91-18.35.pth, bkmy
BLEU = 2.00, 17.9/4.8/1.2/0.2 (BP=1.000, ratio=1.743, hyp_len=21316, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.3.53-34.16.3.20-24.50.3.07-21.53.2.93-18.65.pth, mybk
BLEU = 2.87, 23.3/5.2/1.4/0.4 (BP=1.000, ratio=1.144, hyp_len=13079, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.3.53-34.16.3.20-24.50.3.07-21.53.2.93-18.65.pth, bkmy
BLEU = 2.82, 21.2/5.9/1.5/0.3 (BP=1.000, ratio=1.369, hyp_len=16745, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.3.46-31.66.3.18-24.06.3.03-20.78.2.89-18.03.pth, mybk
BLEU = 4.71, 26.8/7.4/2.6/1.0 (BP=1.000, ratio=1.047, hyp_len=11965, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.3.46-31.66.3.18-24.06.3.03-20.78.2.89-18.03.pth, bkmy
BLEU = 4.00, 27.4/7.9/2.4/0.5 (BP=1.000, ratio=1.184, hyp_len=14486, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.3.48-32.60.3.19-24.21.3.02-20.49.2.90-18.25.pth, mybk
BLEU = 2.79, 18.0/4.8/1.4/0.5 (BP=1.000, ratio=1.504, hyp_len=17190, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.3.48-32.60.3.19-24.21.3.02-20.49.2.90-18.25.pth, bkmy
BLEU = 3.69, 27.7/8.1/2.1/0.4 (BP=1.000, ratio=1.069, hyp_len=13078, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.3.40-29.97.3.11-22.46.3.03-20.73.2.89-17.95.pth, mybk
BLEU = 4.35, 24.5/6.7/2.4/0.9 (BP=1.000, ratio=1.179, hyp_len=13475, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.3.40-29.97.3.11-22.46.3.03-20.73.2.89-17.95.pth, bkmy
BLEU = 4.95, 29.9/9.5/3.1/0.7 (BP=1.000, ratio=1.113, hyp_len=13611, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.3.50-33.18.3.15-23.34.3.00-20.17.2.86-17.53.pth, mybk
BLEU = 0.70, 4.5/1.1/0.4/0.1 (BP=1.000, ratio=5.642, hyp_len=64496, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.3.50-33.18.3.15-23.34.3.00-20.17.2.86-17.53.pth, bkmy
BLEU = 3.32, 20.0/6.2/1.8/0.5 (BP=1.000, ratio=1.531, hyp_len=18728, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.3.38-29.30.3.08-21.81.2.98-19.69.2.78-16.14.pth, mybk
BLEU = 4.97, 25.8/7.6/2.7/1.1 (BP=1.000, ratio=1.127, hyp_len=12881, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.3.38-29.30.3.08-21.81.2.98-19.69.2.78-16.14.pth, bkmy
BLEU = 6.15, 32.8/10.4/3.5/1.2 (BP=1.000, ratio=1.019, hyp_len=12467, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.3.39-29.55.3.09-21.89.2.94-18.98.2.84-17.05.pth, mybk
BLEU = 2.13, 13.8/3.7/1.1/0.4 (BP=1.000, ratio=2.077, hyp_len=23741, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.3.39-29.55.3.09-21.89.2.94-18.98.2.84-17.05.pth, bkmy
BLEU = 4.57, 28.4/9.0/2.6/0.6 (BP=1.000, ratio=1.101, hyp_len=13468, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.3.38-29.37.3.10-22.17.2.96-19.23.2.82-16.85.pth, mybk
BLEU = 0.87, 5.1/1.4/0.5/0.2 (BP=1.000, ratio=5.324, hyp_len=60862, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.3.38-29.37.3.10-22.17.2.96-19.23.2.82-16.85.pth, bkmy
BLEU = 3.82, 22.5/7.0/2.2/0.6 (BP=1.000, ratio=1.409, hyp_len=17231, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.3.39-29.65.3.11-22.33.2.97-19.53.2.76-15.78.pth, mybk
BLEU = 5.04, 27.5/7.9/2.9/1.0 (BP=1.000, ratio=1.111, hyp_len=12703, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.3.39-29.65.3.11-22.33.2.97-19.53.2.76-15.78.pth, bkmy
BLEU = 4.35, 21.8/7.4/2.6/0.8 (BP=1.000, ratio=1.530, hyp_len=18716, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.3.33-27.94.3.03-20.74.2.93-18.82.2.70-14.86.pth, mybk
BLEU = 5.80, 28.6/8.8/3.4/1.3 (BP=1.000, ratio=1.089, hyp_len=12450, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.3.33-27.94.3.03-20.74.2.93-18.82.2.70-14.86.pth, bkmy
BLEU = 4.14, 21.1/7.2/2.5/0.8 (BP=1.000, ratio=1.601, hyp_len=19579, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.3.41-30.31.3.08-21.84.2.92-18.52.2.78-16.20.pth, mybk
BLEU = 0.79, 4.7/1.2/0.4/0.2 (BP=1.000, ratio=5.717, hyp_len=65353, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.3.41-30.31.3.08-21.84.2.92-18.52.2.78-16.20.pth, bkmy
BLEU = 4.63, 25.5/8.3/2.6/0.8 (BP=1.000, ratio=1.268, hyp_len=15507, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.3.28-26.59.2.99-19.93.2.88-17.84.2.76-15.73.pth, mybk
BLEU = 3.50, 19.7/5.5/1.9/0.7 (BP=1.000, ratio=1.431, hyp_len=16363, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.3.28-26.59.2.99-19.93.2.88-17.84.2.76-15.73.pth, bkmy
BLEU = 4.26, 25.2/8.0/2.5/0.7 (BP=1.000, ratio=1.270, hyp_len=15533, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.3.34-28.34.3.08-21.76.2.91-18.43.2.64-13.99.pth, mybk
BLEU = 5.64, 27.2/8.5/3.3/1.3 (BP=1.000, ratio=1.145, hyp_len=13094, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.3.34-28.34.3.08-21.76.2.91-18.43.2.64-13.99.pth, bkmy
BLEU = 4.48, 21.4/7.7/2.8/0.9 (BP=1.000, ratio=1.610, hyp_len=19695, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.3.24-25.53.2.93-18.79.2.87-17.70.2.64-13.99.pth, mybk
BLEU = 4.22, 20.8/6.8/2.5/0.9 (BP=1.000, ratio=1.497, hyp_len=17112, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.3.24-25.53.2.93-18.79.2.87-17.70.2.64-13.99.pth, bkmy
BLEU = 3.91, 18.7/6.5/2.4/0.8 (BP=1.000, ratio=1.819, hyp_len=22253, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.3.28-26.65.2.94-18.98.2.82-16.83.2.69-14.73.pth, mybk
BLEU = 1.99, 10.6/3.1/1.1/0.4 (BP=1.000, ratio=2.812, hyp_len=32146, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.3.28-26.65.2.94-18.98.2.82-16.83.2.69-14.73.pth, bkmy
BLEU = 4.83, 26.3/8.9/2.8/0.8 (BP=1.000, ratio=1.269, hyp_len=15520, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.3.24-25.51.2.97-19.59.2.88-17.83.2.59-13.38.pth, mybk
BLEU = 5.81, 26.8/8.6/3.5/1.4 (BP=1.000, ratio=1.218, hyp_len=13919, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.3.24-25.51.2.97-19.59.2.88-17.83.2.59-13.38.pth, bkmy
BLEU = 5.15, 24.2/8.9/3.1/1.0 (BP=1.000, ratio=1.463, hyp_len=17892, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.3.29-26.82.3.03-20.65.2.81-16.60.2.67-14.41.pth, mybk
BLEU = 1.09, 5.9/1.7/0.6/0.2 (BP=1.000, ratio=4.745, hyp_len=54242, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.3.29-26.82.3.03-20.65.2.81-16.60.2.67-14.41.pth, bkmy
BLEU = 2.93, 17.6/5.5/1.7/0.5 (BP=1.000, ratio=1.818, hyp_len=22231, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.3.11-22.52.2.79-16.33.2.82-16.84.2.56-12.89.pth, mybk
BLEU = 6.21, 27.0/9.3/3.7/1.6 (BP=1.000, ratio=1.209, hyp_len=13817, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.3.11-22.52.2.79-16.33.2.82-16.84.2.56-12.89.pth, bkmy
BLEU = 3.10, 14.5/5.2/1.9/0.6 (BP=1.000, ratio=2.400, hyp_len=29354, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.3.14-23.11.2.83-17.01.2.77-15.94.2.63-13.94.pth, mybk
BLEU = 2.38, 12.1/3.6/1.3/0.5 (BP=1.000, ratio=2.456, hyp_len=28072, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.3.14-23.11.2.83-17.01.2.77-15.94.2.63-13.94.pth, bkmy
BLEU = 3.80, 21.4/7.3/2.3/0.6 (BP=1.000, ratio=1.568, hyp_len=19177, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.3.11-22.44.2.79-16.23.2.80-16.45.2.52-12.42.pth, mybk
BLEU = 6.27, 26.4/9.3/3.8/1.7 (BP=1.000, ratio=1.231, hyp_len=14069, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.3.11-22.44.2.79-16.23.2.80-16.45.2.52-12.42.pth, bkmy
BLEU = 4.88, 20.8/7.9/3.1/1.1 (BP=1.000, ratio=1.737, hyp_len=21248, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.3.12-22.72.2.86-17.41.2.75-15.61.2.57-13.08.pth, mybk
BLEU = 2.87, 13.8/4.4/1.7/0.7 (BP=1.000, ratio=2.242, hyp_len=25633, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.3.12-22.72.2.86-17.41.2.75-15.61.2.57-13.08.pth, bkmy
BLEU = 4.60, 24.0/8.4/2.8/0.8 (BP=1.000, ratio=1.430, hyp_len=17485, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.2.98-19.72.2.71-14.99.2.75-15.65.2.47-11.77.pth, mybk
BLEU = 6.85, 28.8/10.1/4.3/1.8 (BP=1.000, ratio=1.174, hyp_len=13419, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.2.98-19.72.2.71-14.99.2.75-15.65.2.47-11.77.pth, bkmy
BLEU = 4.89, 20.6/7.9/3.0/1.2 (BP=1.000, ratio=1.771, hyp_len=21658, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.3.08-21.71.2.76-15.73.2.74-15.45.2.57-13.11.pth, mybk
BLEU = 1.95, 9.2/3.0/1.2/0.4 (BP=1.000, ratio=3.390, hyp_len=38760, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.3.08-21.71.2.76-15.73.2.74-15.45.2.57-13.11.pth, bkmy
BLEU = 1.58, 9.0/3.0/0.9/0.2 (BP=1.000, ratio=3.676, hyp_len=44956, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.2.93-18.72.2.63-13.89.2.73-15.26.2.45-11.61.pth, mybk
BLEU = 8.29, 32.8/12.0/5.2/2.3 (BP=1.000, ratio=1.069, hyp_len=12216, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.2.93-18.72.2.63-13.89.2.73-15.26.2.45-11.61.pth, bkmy
BLEU = 3.45, 14.2/5.5/2.2/0.8 (BP=1.000, ratio=2.547, hyp_len=31155, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.2.95-19.19.2.69-14.69.2.71-15.10.2.53-12.55.pth, mybk
BLEU = 3.62, 16.7/5.3/2.1/0.9 (BP=1.000, ratio=1.886, hyp_len=21560, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.2.95-19.19.2.69-14.69.2.71-15.10.2.53-12.55.pth, bkmy
BLEU = 3.66, 17.8/6.5/2.2/0.7 (BP=1.000, ratio=1.924, hyp_len=23535, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.2.94-18.92.2.64-13.98.2.72-15.25.2.44-11.44.pth, mybk
BLEU = 8.38, 33.3/12.3/5.2/2.3 (BP=1.000, ratio=1.042, hyp_len=11915, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.2.94-18.92.2.64-13.98.2.72-15.25.2.44-11.44.pth, bkmy
BLEU = 4.29, 17.8/6.8/2.7/1.1 (BP=1.000, ratio=2.056, hyp_len=25150, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.2.98-19.72.2.68-14.59.2.70-14.89.2.53-12.55.pth, mybk
BLEU = 4.46, 19.7/6.7/2.7/1.1 (BP=1.000, ratio=1.715, hyp_len=19610, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.2.98-19.72.2.68-14.59.2.70-14.89.2.53-12.55.pth, bkmy
BLEU = 3.85, 20.0/6.9/2.3/0.7 (BP=1.000, ratio=1.717, hyp_len=21001, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.31.2.92-18.60.2.63-13.85.2.67-14.44.2.49-12.02.pth, mybk
BLEU = 3.68, 17.2/5.6/2.2/0.9 (BP=1.000, ratio=1.968, hyp_len=22494, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.31.2.92-18.60.2.63-13.85.2.67-14.44.2.49-12.02.pth, bkmy
BLEU = 6.54, 29.6/10.7/4.0/1.4 (BP=1.000, ratio=1.216, hyp_len=14870, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.31.2.94-18.82.2.65-14.21.2.69-14.76.2.39-10.92.pth, mybk
BLEU = 8.57, 32.9/12.4/5.3/2.5 (BP=1.000, ratio=1.070, hyp_len=12235, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.31.2.94-18.82.2.65-14.21.2.69-14.76.2.39-10.92.pth, bkmy
BLEU = 7.51, 29.0/11.6/4.8/2.0 (BP=1.000, ratio=1.306, hyp_len=15969, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.32.2.83-16.97.2.53-12.55.2.66-14.30.2.37-10.72.pth, mybk
BLEU = 8.15, 31.1/11.6/5.1/2.4 (BP=1.000, ratio=1.135, hyp_len=12973, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.32.2.83-16.97.2.53-12.55.2.66-14.30.2.37-10.72.pth, bkmy
BLEU = 7.40, 28.3/11.3/4.7/2.0 (BP=1.000, ratio=1.364, hyp_len=16681, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.32.2.86-17.48.2.58-13.17.2.64-13.96.2.49-12.05.pth, mybk
BLEU = 4.77, 20.2/7.0/2.9/1.3 (BP=1.000, ratio=1.687, hyp_len=19282, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.32.2.86-17.48.2.58-13.17.2.64-13.96.2.49-12.05.pth, bkmy
BLEU = 4.90, 22.1/8.0/3.0/1.1 (BP=1.000, ratio=1.628, hyp_len=19910, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.33.2.82-16.75.2.52-12.43.2.61-13.66.2.45-11.65.pth, mybk
BLEU = 2.64, 11.5/3.9/1.6/0.7 (BP=1.000, ratio=2.913, hyp_len=33299, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.33.2.82-16.75.2.52-12.43.2.61-13.66.2.45-11.65.pth, bkmy
BLEU = 5.78, 26.4/9.8/3.6/1.2 (BP=1.000, ratio=1.393, hyp_len=17037, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.33.2.85-17.31.2.58-13.25.2.67-14.37.2.36-10.55.pth, mybk
BLEU = 7.77, 30.6/11.1/4.9/2.2 (BP=1.000, ratio=1.165, hyp_len=13321, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.33.2.85-17.31.2.58-13.25.2.67-14.37.2.36-10.55.pth, bkmy
BLEU = 8.59, 32.8/13.0/5.4/2.4 (BP=1.000, ratio=1.184, hyp_len=14485, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.34.2.76-15.75.2.44-11.49.2.66-14.26.2.33-10.23.pth, mybk
BLEU = 8.49, 32.4/12.0/5.3/2.5 (BP=1.000, ratio=1.121, hyp_len=12814, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.34.2.76-15.75.2.44-11.49.2.66-14.26.2.33-10.23.pth, bkmy
BLEU = 8.94, 34.3/13.8/5.7/2.4 (BP=1.000, ratio=1.132, hyp_len=13850, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.34.2.84-17.18.2.59-13.36.2.60-13.50.2.45-11.56.pth, mybk
BLEU = 4.67, 20.4/7.0/2.8/1.2 (BP=1.000, ratio=1.702, hyp_len=19455, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.34.2.84-17.18.2.59-13.36.2.60-13.50.2.45-11.56.pth, bkmy
BLEU = 5.11, 21.6/8.4/3.2/1.2 (BP=1.000, ratio=1.728, hyp_len=21133, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.35.2.72-15.24.2.42-11.24.2.62-13.78.2.31-10.04.pth, mybk
BLEU = 9.07, 33.7/12.8/5.8/2.7 (BP=1.000, ratio=1.096, hyp_len=12529, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.35.2.72-15.24.2.42-11.24.2.62-13.78.2.31-10.04.pth, bkmy
BLEU = 9.90, 36.7/14.8/6.3/2.8 (BP=1.000, ratio=1.066, hyp_len=13037, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.35.2.83-16.88.2.52-12.47.2.58-13.20.2.42-11.25.pth, mybk
BLEU = 5.12, 21.7/7.5/3.1/1.4 (BP=1.000, ratio=1.584, hyp_len=18111, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.35.2.83-16.88.2.52-12.47.2.58-13.20.2.42-11.25.pth, bkmy
BLEU = 4.86, 20.9/8.0/3.0/1.1 (BP=1.000, ratio=1.786, hyp_len=21848, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.36.2.68-14.60.2.39-10.88.2.64-14.06.2.31-10.08.pth, mybk
BLEU = 8.57, 32.9/12.1/5.3/2.5 (BP=1.000, ratio=1.137, hyp_len=12996, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.36.2.68-14.60.2.39-10.88.2.64-14.06.2.31-10.08.pth, bkmy
BLEU = 9.73, 36.1/14.7/6.3/2.7 (BP=1.000, ratio=1.113, hyp_len=13619, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.36.2.72-15.19.2.40-11.07.2.58-13.16.2.40-10.97.pth, mybk
BLEU = 4.64, 18.8/6.8/2.9/1.3 (BP=1.000, ratio=1.885, hyp_len=21551, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.36.2.72-15.19.2.40-11.07.2.58-13.16.2.40-10.97.pth, bkmy
BLEU = 6.79, 29.5/11.3/4.2/1.5 (BP=1.000, ratio=1.273, hyp_len=15574, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.37.2.62-13.80.2.34-10.33.2.63-13.90.2.30-10.02.pth, mybk
BLEU = 7.77, 28.3/10.8/5.1/2.4 (BP=1.000, ratio=1.323, hyp_len=15120, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.37.2.62-13.80.2.34-10.33.2.63-13.90.2.30-10.02.pth, bkmy
BLEU = 8.74, 32.4/13.3/5.5/2.4 (BP=1.000, ratio=1.221, hyp_len=14929, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.37.2.70-14.93.2.39-10.92.2.55-12.75.2.38-10.81.pth, mybk
BLEU = 7.99, 30.3/11.5/5.1/2.3 (BP=1.000, ratio=1.203, hyp_len=13754, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.37.2.70-14.93.2.39-10.92.2.55-12.75.2.38-10.81.pth, bkmy
BLEU = 6.41, 25.6/10.2/4.1/1.6 (BP=1.000, ratio=1.489, hyp_len=18216, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.38.2.63-13.91.2.35-10.52.2.59-13.36.2.31-10.04.pth, mybk
BLEU = 10.53, 37.2/14.8/6.9/3.2 (BP=1.000, ratio=1.024, hyp_len=11704, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.38.2.63-13.91.2.35-10.52.2.59-13.36.2.31-10.04.pth, bkmy
BLEU = 10.14, 36.8/15.0/6.5/2.9 (BP=1.000, ratio=1.095, hyp_len=13391, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.38.2.65-14.18.2.34-10.41.2.55-12.82.2.38-10.79.pth, mybk
BLEU = 6.26, 25.0/9.2/3.9/1.7 (BP=1.000, ratio=1.390, hyp_len=15889, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.38.2.65-14.18.2.34-10.41.2.55-12.82.2.38-10.79.pth, bkmy
BLEU = 7.74, 31.5/12.6/4.9/1.8 (BP=1.000, ratio=1.242, hyp_len=15191, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.39.2.57-13.08.2.29-9.85.2.59-13.28.2.28-9.74.pth, mybk
BLEU = 9.38, 32.9/12.8/6.1/3.0 (BP=1.000, ratio=1.158, hyp_len=13233, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.39.2.57-13.08.2.29-9.85.2.59-13.28.2.28-9.74.pth, bkmy
BLEU = 9.72, 35.8/14.4/6.2/2.8 (BP=1.000, ratio=1.132, hyp_len=13841, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.39.2.61-13.64.2.29-9.90.2.53-12.51.2.37-10.74.pth, mybk
BLEU = 9.09, 33.2/12.8/5.9/2.7 (BP=1.000, ratio=1.081, hyp_len=12358, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.39.2.61-13.64.2.29-9.90.2.53-12.51.2.37-10.74.pth, bkmy
BLEU = 6.35, 25.4/10.1/4.0/1.6 (BP=1.000, ratio=1.503, hyp_len=18381, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.40.2.62-13.70.2.30-10.02.2.57-13.12.2.27-9.63.pth, mybk
BLEU = 9.87, 35.1/13.8/6.5/3.0 (BP=1.000, ratio=1.108, hyp_len=12664, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.40.2.62-13.70.2.30-10.02.2.57-13.12.2.27-9.63.pth, bkmy
BLEU = 8.67, 31.8/13.1/5.5/2.4 (BP=1.000, ratio=1.265, hyp_len=15478, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.40.2.71-15.08.2.45-11.54.2.51-12.32.2.38-10.75.pth, mybk
BLEU = 8.22, 30.8/11.7/5.2/2.5 (BP=1.000, ratio=1.192, hyp_len=13623, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.40.2.71-15.08.2.45-11.54.2.51-12.32.2.38-10.75.pth, bkmy
BLEU = 5.86, 23.0/9.2/3.7/1.5 (BP=1.000, ratio=1.700, hyp_len=20795, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.41.2.55-12.78.2.26-9.56.2.50-12.15.2.36-10.60.pth, mybk
BLEU = 8.15, 30.4/11.6/5.1/2.4 (BP=1.000, ratio=1.184, hyp_len=13533, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.41.2.55-12.78.2.26-9.56.2.50-12.15.2.36-10.60.pth, bkmy
BLEU = 6.33, 23.8/9.6/4.1/1.7 (BP=1.000, ratio=1.619, hyp_len=19798, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.41.2.62-13.67.2.35-10.47.2.54-12.67.2.23-9.29.pth, mybk
BLEU = 9.63, 33.0/13.3/6.3/3.1 (BP=1.000, ratio=1.176, hyp_len=13443, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.41.2.62-13.67.2.35-10.47.2.54-12.67.2.23-9.29.pth, bkmy
BLEU = 10.28, 36.0/15.0/6.7/3.1 (BP=1.000, ratio=1.127, hyp_len=13784, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.42.2.50-12.14.2.20-9.05.2.47-11.88.2.33-10.27.pth, mybk
BLEU = 9.40, 33.4/13.3/6.1/2.9 (BP=1.000, ratio=1.098, hyp_len=12550, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.42.2.50-12.14.2.20-9.05.2.47-11.88.2.33-10.27.pth, bkmy
BLEU = 8.59, 32.4/13.3/5.5/2.3 (BP=1.000, ratio=1.206, hyp_len=14749, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.42.2.57-13.08.2.23-9.31.2.52-12.48.2.27-9.64.pth, mybk
BLEU = 10.96, 36.5/14.8/7.2/3.7 (BP=1.000, ratio=1.071, hyp_len=12247, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.42.2.57-13.08.2.23-9.31.2.52-12.48.2.27-9.64.pth, bkmy
BLEU = 8.09, 29.7/11.8/5.1/2.4 (BP=1.000, ratio=1.371, hyp_len=16767, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.43.2.46-11.72.2.20-8.99.2.47-11.81.2.34-10.38.pth, mybk
BLEU = 10.25, 35.8/14.2/6.7/3.3 (BP=1.000, ratio=1.051, hyp_len=12010, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.43.2.46-11.72.2.20-8.99.2.47-11.81.2.34-10.38.pth, bkmy
BLEU = 8.64, 32.3/13.4/5.6/2.3 (BP=1.000, ratio=1.235, hyp_len=15106, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.43.2.48-11.98.2.18-8.81.2.52-12.39.2.23-9.34.pth, mybk
BLEU = 11.13, 36.0/14.9/7.5/3.8 (BP=1.000, ratio=1.103, hyp_len=12606, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.43.2.48-11.98.2.18-8.81.2.52-12.39.2.23-9.34.pth, bkmy
BLEU = 10.49, 37.2/15.5/6.9/3.0 (BP=1.000, ratio=1.112, hyp_len=13598, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.44.2.47-11.82.2.17-8.72.2.52-12.44.2.23-9.33.pth, mybk
BLEU = 11.22, 37.5/15.2/7.4/3.8 (BP=1.000, ratio=1.057, hyp_len=12084, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.44.2.47-11.82.2.17-8.72.2.52-12.44.2.23-9.33.pth, bkmy
BLEU = 10.50, 37.0/15.4/6.8/3.1 (BP=1.000, ratio=1.122, hyp_len=13720, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.44.2.53-12.59.2.20-9.07.2.47-11.78.2.31-10.09.pth, mybk
BLEU = 10.07, 34.4/13.9/6.5/3.3 (BP=1.000, ratio=1.094, hyp_len=12504, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.44.2.53-12.59.2.20-9.07.2.47-11.78.2.31-10.09.pth, bkmy
BLEU = 10.52, 36.5/15.6/6.9/3.1 (BP=1.000, ratio=1.102, hyp_len=13484, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.45.2.40-10.99.2.11-8.27.2.52-12.42.2.23-9.34.pth, mybk
BLEU = 11.26, 37.6/15.4/7.5/3.7 (BP=1.000, ratio=1.075, hyp_len=12284, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.45.2.40-10.99.2.11-8.27.2.52-12.42.2.23-9.34.pth, bkmy
BLEU = 10.81, 37.8/15.7/7.1/3.3 (BP=1.000, ratio=1.114, hyp_len=13629, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.45.2.43-11.38.2.16-8.65.2.47-11.78.2.30-9.97.pth, mybk
BLEU = 9.38, 32.5/13.0/6.1/3.0 (BP=1.000, ratio=1.180, hyp_len=13495, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.45.2.43-11.38.2.16-8.65.2.47-11.78.2.30-9.97.pth, bkmy
BLEU = 8.42, 30.8/12.8/5.4/2.3 (BP=1.000, ratio=1.304, hyp_len=15945, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.46.2.37-10.68.2.13-8.38.2.49-12.02.2.23-9.28.pth, mybk
BLEU = 11.41, 37.1/15.7/7.6/3.8 (BP=1.000, ratio=1.094, hyp_len=12501, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.46.2.37-10.68.2.13-8.38.2.49-12.02.2.23-9.28.pth, bkmy
BLEU = 10.94, 38.2/16.0/7.1/3.3 (BP=1.000, ratio=1.093, hyp_len=13365, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.46.2.46-11.71.2.17-8.79.2.44-11.51.2.30-9.97.pth, mybk
BLEU = 9.68, 33.1/13.4/6.3/3.1 (BP=1.000, ratio=1.145, hyp_len=13087, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.46.2.46-11.71.2.17-8.79.2.44-11.51.2.30-9.97.pth, bkmy
BLEU = 7.32, 27.3/11.2/4.8/2.0 (BP=1.000, ratio=1.471, hyp_len=17990, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.47.2.32-10.21.2.06-7.84.2.48-11.97.2.22-9.24.pth, mybk
BLEU = 11.14, 37.1/15.4/7.4/3.7 (BP=1.000, ratio=1.063, hyp_len=12148, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.47.2.32-10.21.2.06-7.84.2.48-11.97.2.22-9.24.pth, bkmy
BLEU = 11.16, 37.9/15.9/7.3/3.5 (BP=1.000, ratio=1.099, hyp_len=13441, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.47.2.47-11.78.2.15-8.57.2.43-11.30.2.31-10.05.pth, mybk
BLEU = 10.62, 35.2/14.4/7.0/3.6 (BP=1.000, ratio=1.103, hyp_len=12610, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.47.2.47-11.78.2.15-8.57.2.43-11.30.2.31-10.05.pth, bkmy
BLEU = 9.40, 34.2/14.2/6.2/2.6 (BP=1.000, ratio=1.194, hyp_len=14601, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.48.2.32-10.20.2.06-7.85.2.48-11.93.2.21-9.09.pth, mybk
BLEU = 11.59, 37.6/15.7/7.8/3.9 (BP=1.000, ratio=1.075, hyp_len=12287, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.48.2.32-10.20.2.06-7.85.2.48-11.93.2.21-9.09.pth, bkmy
BLEU = 11.11, 38.9/16.3/7.2/3.3 (BP=1.000, ratio=1.084, hyp_len=13253, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.48.2.32-10.20.2.06-7.88.2.43-11.40.2.31-10.12.pth, mybk
BLEU = 10.96, 35.2/14.7/7.3/3.8 (BP=1.000, ratio=1.087, hyp_len=12428, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.48.2.32-10.20.2.06-7.88.2.43-11.40.2.31-10.12.pth, bkmy
BLEU = 10.09, 36.4/15.2/6.6/2.8 (BP=1.000, ratio=1.132, hyp_len=13841, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.49.2.33-10.27.2.12-8.37.2.46-11.74.2.24-9.41.pth, mybk
BLEU = 12.55, 38.9/16.8/8.4/4.5 (BP=1.000, ratio=1.056, hyp_len=12074, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.49.2.33-10.27.2.12-8.37.2.46-11.74.2.24-9.41.pth, bkmy
BLEU = 11.31, 38.6/16.4/7.3/3.5 (BP=1.000, ratio=1.094, hyp_len=13381, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.49.2.35-10.51.2.08-8.00.2.41-11.12.2.31-10.04.pth, mybk
BLEU = 11.06, 36.5/15.1/7.3/3.7 (BP=1.000, ratio=1.073, hyp_len=12265, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.49.2.35-10.51.2.08-8.00.2.41-11.12.2.31-10.04.pth, bkmy
BLEU = 10.66, 36.7/15.7/6.9/3.2 (BP=1.000, ratio=1.107, hyp_len=13534, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.50.2.28-9.80.2.07-7.96.2.48-11.90.2.24-9.37.pth, mybk
BLEU = 11.36, 37.0/15.5/7.6/3.8 (BP=1.000, ratio=1.104, hyp_len=12620, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.50.2.28-9.80.2.07-7.96.2.48-11.90.2.24-9.37.pth, bkmy
BLEU = 11.15, 38.8/16.4/7.3/3.3 (BP=1.000, ratio=1.078, hyp_len=13179, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.50.2.31-10.10.2.02-7.56.2.41-11.12.2.29-9.86.pth, mybk
BLEU = 11.21, 36.9/15.4/7.4/3.8 (BP=1.000, ratio=1.060, hyp_len=12116, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.50.2.31-10.10.2.02-7.56.2.41-11.12.2.29-9.86.pth, bkmy
BLEU = 9.78, 33.5/14.3/6.5/2.9 (BP=1.000, ratio=1.228, hyp_len=15019, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.51.2.21-9.10.1.96-7.07.2.45-11.61.2.22-9.21.pth, mybk
BLEU = 12.92, 39.8/17.5/8.9/4.5 (BP=1.000, ratio=1.033, hyp_len=11814, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.51.2.21-9.10.1.96-7.07.2.45-11.61.2.22-9.21.pth, bkmy
BLEU = 11.24, 37.5/16.2/7.4/3.6 (BP=1.000, ratio=1.146, hyp_len=14018, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.51.2.27-9.69.2.02-7.54.2.44-11.42.2.31-10.04.pth, mybk
BLEU = 11.38, 37.1/15.5/7.5/3.9 (BP=1.000, ratio=1.063, hyp_len=12156, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.51.2.27-9.69.2.02-7.54.2.44-11.42.2.31-10.04.pth, bkmy
BLEU = 9.05, 31.5/13.1/5.9/2.8 (BP=1.000, ratio=1.280, hyp_len=15658, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.52.2.19-8.96.1.94-6.98.2.47-11.84.2.24-9.41.pth, mybk
BLEU = 12.27, 38.0/16.4/8.4/4.4 (BP=1.000, ratio=1.085, hyp_len=12401, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.52.2.19-8.96.1.94-6.98.2.47-11.84.2.24-9.41.pth, bkmy
BLEU = 11.22, 38.9/16.5/7.3/3.4 (BP=1.000, ratio=1.096, hyp_len=13400, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.52.2.26-9.63.2.01-7.45.2.40-11.06.2.29-9.88.pth, mybk
BLEU = 12.14, 38.3/16.2/8.1/4.4 (BP=1.000, ratio=1.046, hyp_len=11953, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.52.2.26-9.63.2.01-7.45.2.40-11.06.2.29-9.88.pth, bkmy
BLEU = 10.50, 35.3/15.3/7.0/3.2 (BP=1.000, ratio=1.168, hyp_len=14284, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.53.2.22-9.23.2.02-7.50.2.44-11.51.2.23-9.32.pth, mybk
BLEU = 13.21, 40.0/17.5/8.9/4.9 (BP=1.000, ratio=1.053, hyp_len=12037, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.53.2.22-9.23.2.02-7.50.2.44-11.51.2.23-9.32.pth, bkmy
BLEU = 11.04, 37.7/15.9/7.1/3.5 (BP=1.000, ratio=1.128, hyp_len=13799, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.53.2.26-9.63.1.99-7.30.2.40-11.06.2.31-10.09.pth, mybk
BLEU = 12.00, 38.3/16.4/7.9/4.2 (BP=1.000, ratio=1.067, hyp_len=12198, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.53.2.26-9.63.1.99-7.30.2.40-11.06.2.31-10.09.pth, bkmy
BLEU = 11.08, 37.9/16.4/7.4/3.3 (BP=1.000, ratio=1.091, hyp_len=13341, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.54.2.12-8.36.1.89-6.59.2.45-11.57.2.21-9.12.pth, mybk
BLEU = 12.01, 36.9/15.9/8.1/4.4 (BP=1.000, ratio=1.130, hyp_len=12916, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.54.2.12-8.36.1.89-6.59.2.45-11.57.2.21-9.12.pth, bkmy
BLEU = 12.15, 39.6/17.2/7.9/4.0 (BP=1.000, ratio=1.079, hyp_len=13203, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.54.2.19-8.95.1.94-6.95.2.41-11.08.2.28-9.79.pth, mybk
BLEU = 12.26, 38.1/16.4/8.2/4.4 (BP=1.000, ratio=1.078, hyp_len=12318, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.54.2.19-8.95.1.94-6.95.2.41-11.08.2.28-9.79.pth, bkmy
BLEU = 9.54, 32.7/13.8/6.3/2.9 (BP=1.000, ratio=1.243, hyp_len=15209, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.55.2.10-8.15.1.86-6.45.2.43-11.38.2.20-9.05.pth, mybk
BLEU = 12.99, 38.8/17.2/9.0/4.7 (BP=1.000, ratio=1.085, hyp_len=12407, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.55.2.10-8.15.1.86-6.45.2.43-11.38.2.20-9.05.pth, bkmy
BLEU = 11.85, 39.4/17.1/7.8/3.8 (BP=1.000, ratio=1.093, hyp_len=13365, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.55.2.24-9.36.2.03-7.58.2.39-10.90.2.28-9.79.pth, mybk
BLEU = 12.33, 38.8/16.5/8.2/4.4 (BP=1.000, ratio=1.053, hyp_len=12041, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.55.2.24-9.36.2.03-7.58.2.39-10.90.2.28-9.79.pth, bkmy
BLEU = 8.57, 31.0/13.0/5.6/2.4 (BP=1.000, ratio=1.336, hyp_len=16340, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.56.2.10-8.20.1.86-6.40.2.43-11.41.2.22-9.23.pth, mybk
BLEU = 12.90, 38.8/17.2/8.8/4.7 (BP=1.000, ratio=1.087, hyp_len=12426, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.56.2.10-8.20.1.86-6.40.2.43-11.41.2.22-9.23.pth, bkmy
BLEU = 11.41, 38.6/16.5/7.5/3.5 (BP=1.000, ratio=1.104, hyp_len=13498, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.56.2.22-9.25.1.94-6.96.2.38-10.78.2.28-9.77.pth, mybk
BLEU = 12.56, 38.5/16.7/8.4/4.6 (BP=1.000, ratio=1.052, hyp_len=12023, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.56.2.22-9.25.1.94-6.96.2.38-10.78.2.28-9.77.pth, bkmy
BLEU = 10.75, 36.3/15.6/7.1/3.3 (BP=1.000, ratio=1.135, hyp_len=13880, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.57.2.06-7.88.1.81-6.09.2.40-11.03.2.20-8.99.pth, mybk
BLEU = 13.25, 40.2/17.7/9.1/4.8 (BP=1.000, ratio=1.069, hyp_len=12223, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.57.2.06-7.88.1.81-6.09.2.40-11.03.2.20-8.99.pth, bkmy
BLEU = 12.31, 39.9/17.4/8.2/4.1 (BP=1.000, ratio=1.074, hyp_len=13141, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.57.2.15-8.60.1.91-6.73.2.40-11.03.2.28-9.80.pth, mybk
BLEU = 12.46, 38.4/16.6/8.4/4.5 (BP=1.000, ratio=1.077, hyp_len=12308, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.57.2.15-8.60.1.91-6.73.2.40-11.03.2.28-9.80.pth, bkmy
BLEU = 11.18, 37.4/16.3/7.5/3.4 (BP=1.000, ratio=1.101, hyp_len=13462, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.58.2.10-8.17.1.84-6.32.2.38-10.84.2.29-9.86.pth, mybk
BLEU = 12.13, 38.1/16.4/8.1/4.2 (BP=1.000, ratio=1.068, hyp_len=12209, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.58.2.10-8.17.1.84-6.32.2.38-10.84.2.29-9.86.pth, bkmy
BLEU = 11.52, 37.6/16.3/7.8/3.7 (BP=1.000, ratio=1.100, hyp_len=13458, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.58.2.11-8.22.1.85-6.33.2.45-11.57.2.19-8.90.pth, mybk
BLEU = 12.64, 39.1/17.0/8.5/4.5 (BP=1.000, ratio=1.082, hyp_len=12364, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.58.2.11-8.22.1.85-6.33.2.45-11.57.2.19-8.90.pth, bkmy
BLEU = 11.69, 39.1/16.5/7.6/3.8 (BP=1.000, ratio=1.095, hyp_len=13388, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.59.2.06-7.83.1.85-6.37.2.45-11.53.2.19-8.96.pth, mybk
BLEU = 12.81, 39.4/17.5/8.8/4.5 (BP=1.000, ratio=1.081, hyp_len=12359, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.59.2.06-7.83.1.85-6.37.2.45-11.53.2.19-8.96.pth, bkmy
BLEU = 11.68, 39.1/16.7/7.7/3.7 (BP=1.000, ratio=1.098, hyp_len=13431, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.59.2.07-7.94.1.86-6.40.2.39-10.89.2.28-9.81.pth, mybk
BLEU = 12.46, 38.3/16.7/8.4/4.5 (BP=1.000, ratio=1.088, hyp_len=12437, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.59.2.07-7.94.1.86-6.40.2.39-10.89.2.28-9.81.pth, bkmy
BLEU = 9.85, 32.7/14.0/6.6/3.1 (BP=1.000, ratio=1.267, hyp_len=15495, ref_len=12231)
Traceback (most recent call last):
  File "/home/ye/exp/simple-nmt/translate.py", line 182, in <module>
    map_location='cpu',
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/serialization.py", line 600, in load
    with _open_zipfile_reader(opened_file) as opened_zipfile:
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/serialization.py", line 242, in __init__
    super(_open_zipfile_reader, self).__init__(torch._C.PyTorchFileReader(name_or_buffer))
RuntimeError: PytorchStreamReader failed reading zip archive: failed finding central directory
Evaluation result for the model: dsl-model-mybk.60.2.03-7.59.1.83-6.24.2.43-11.36.2.21-9.14.pth, mybk
Use of uninitialized value $length_reference in numeric eq (==) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 148.
BLEU = 0, 0/0/0/0 (BP=0, ratio=0, hyp_len=0, ref_len=0)
Traceback (most recent call last):
  File "/home/ye/exp/simple-nmt/translate.py", line 182, in <module>
    map_location='cpu',
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/serialization.py", line 600, in load
    with _open_zipfile_reader(opened_file) as opened_zipfile:
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/serialization.py", line 242, in __init__
    super(_open_zipfile_reader, self).__init__(torch._C.PyTorchFileReader(name_or_buffer))
RuntimeError: PytorchStreamReader failed reading zip archive: failed finding central directory
Evaluation result for the model: dsl-model-mybk.60.2.03-7.59.1.83-6.24.2.43-11.36.2.21-9.14.pth, bkmy
Use of uninitialized value $length_reference in numeric eq (==) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 148.
BLEU = 0, 0/0/0/0 (BP=0, ratio=0, hyp_len=0, ref_len=0)
Evaluation result for the model: dsl-model-mybk.60.2.15-8.58.1.86-6.43.2.39-10.93.2.27-9.65.pth, mybk
BLEU = 12.45, 37.8/16.5/8.4/4.6 (BP=1.000, ratio=1.088, hyp_len=12442, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.60.2.15-8.58.1.86-6.43.2.39-10.93.2.27-9.65.pth, bkmy
BLEU = 9.05, 31.0/13.1/6.0/2.7 (BP=1.000, ratio=1.329, hyp_len=16257, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.61.2.03-7.64.1.79-6.01.2.38-10.85.2.28-9.75.pth, mybk
BLEU = 12.74, 38.9/17.0/8.6/4.6 (BP=1.000, ratio=1.078, hyp_len=12324, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.61.2.03-7.64.1.79-6.01.2.38-10.85.2.28-9.75.pth, bkmy
BLEU = 11.24, 38.3/16.5/7.4/3.4 (BP=1.000, ratio=1.082, hyp_len=13229, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.62.2.02-7.52.1.79-6.02.2.38-10.81.2.29-9.89.pth, mybk
BLEU = 13.29, 39.7/17.3/8.9/5.1 (BP=1.000, ratio=1.053, hyp_len=12033, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.62.2.02-7.52.1.79-6.02.2.38-10.81.2.29-9.89.pth, bkmy
BLEU = 10.77, 36.1/15.7/7.1/3.3 (BP=1.000, ratio=1.153, hyp_len=14107, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.63.1.99-7.30.1.75-5.76.2.38-10.76.2.30-9.96.pth, mybk
BLEU = 12.86, 38.9/17.4/8.8/4.6 (BP=1.000, ratio=1.080, hyp_len=12341, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.63.1.99-7.30.1.75-5.76.2.38-10.76.2.30-9.96.pth, bkmy
BLEU = 11.79, 38.2/16.8/7.9/3.8 (BP=1.000, ratio=1.092, hyp_len=13361, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.64.2.07-7.92.1.86-6.42.2.38-10.77.2.30-9.99.pth, mybk
BLEU = 12.66, 38.4/16.8/8.6/4.6 (BP=1.000, ratio=1.089, hyp_len=12454, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.64.2.07-7.92.1.86-6.42.2.38-10.77.2.30-9.99.pth, bkmy
BLEU = 11.57, 38.5/16.5/7.6/3.7 (BP=1.000, ratio=1.079, hyp_len=13203, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.65.2.00-7.43.1.81-6.08.2.37-10.75.2.26-9.56.pth, mybk
BLEU = 13.21, 40.3/18.0/9.0/4.7 (BP=1.000, ratio=1.064, hyp_len=12164, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.65.2.00-7.43.1.81-6.08.2.37-10.75.2.26-9.56.pth, bkmy
BLEU = 11.74, 39.4/17.0/7.8/3.6 (BP=1.000, ratio=1.063, hyp_len=13001, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.66.2.05-7.73.1.74-5.69.2.40-10.97.2.27-9.71.pth, mybk
BLEU = 13.32, 39.7/17.5/8.9/5.1 (BP=1.000, ratio=1.060, hyp_len=12113, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.66.2.05-7.73.1.74-5.69.2.40-10.97.2.27-9.71.pth, bkmy
BLEU = 11.74, 39.5/17.0/7.8/3.6 (BP=1.000, ratio=1.075, hyp_len=13145, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.67.1.91-6.77.1.65-5.22.2.39-10.88.2.30-10.01.pth, mybk
BLEU = 13.99, 40.4/18.4/9.7/5.4 (BP=1.000, ratio=1.061, hyp_len=12128, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.67.1.91-6.77.1.65-5.22.2.39-10.88.2.30-10.01.pth, bkmy
BLEU = 11.34, 38.1/16.4/7.5/3.5 (BP=1.000, ratio=1.093, hyp_len=13373, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.68.1.97-7.15.1.68-5.39.2.34-10.41.2.29-9.85.pth, mybk
BLEU = 14.22, 40.9/18.5/9.8/5.5 (BP=1.000, ratio=1.065, hyp_len=12174, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.68.1.97-7.15.1.68-5.39.2.34-10.41.2.29-9.85.pth, bkmy
BLEU = 12.15, 39.8/17.2/8.1/3.9 (BP=1.000, ratio=1.056, hyp_len=12921, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.69.1.90-6.71.1.64-5.17.2.37-10.65.2.30-9.93.pth, mybk
BLEU = 13.63, 40.8/18.1/9.3/5.0 (BP=1.000, ratio=1.055, hyp_len=12057, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.69.1.90-6.71.1.64-5.17.2.37-10.65.2.30-9.93.pth, bkmy
BLEU = 11.31, 38.0/16.4/7.5/3.5 (BP=1.000, ratio=1.097, hyp_len=13414, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.70.1.97-7.18.1.64-5.17.2.38-10.81.2.29-9.88.pth, mybk
BLEU = 13.95, 40.4/18.1/9.5/5.5 (BP=1.000, ratio=1.046, hyp_len=11958, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.70.1.97-7.18.1.64-5.17.2.38-10.81.2.29-9.88.pth, bkmy
BLEU = 12.00, 39.3/17.0/8.0/3.9 (BP=1.000, ratio=1.063, hyp_len=13001, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.71.1.81-6.12.1.61-4.99.2.35-10.52.2.29-9.83.pth, mybk
BLEU = 13.55, 40.0/17.9/9.2/5.1 (BP=1.000, ratio=1.082, hyp_len=12369, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.71.1.81-6.12.1.61-4.99.2.35-10.52.2.29-9.83.pth, bkmy
BLEU = 11.66, 38.6/16.6/7.8/3.7 (BP=1.000, ratio=1.090, hyp_len=13331, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.72.1.83-6.22.1.62-5.06.2.36-10.54.2.29-9.85.pth, mybk
BLEU = 13.81, 40.0/17.8/9.4/5.4 (BP=1.000, ratio=1.083, hyp_len=12381, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.72.1.83-6.22.1.62-5.06.2.36-10.54.2.29-9.85.pth, bkmy
BLEU = 11.93, 39.7/17.2/7.9/3.8 (BP=1.000, ratio=1.057, hyp_len=12923, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.73.1.86-6.42.1.60-4.96.2.36-10.55.2.30-9.99.pth, mybk
BLEU = 13.96, 40.0/18.2/9.6/5.4 (BP=1.000, ratio=1.084, hyp_len=12397, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.73.1.86-6.42.1.60-4.96.2.36-10.55.2.30-9.99.pth, bkmy
BLEU = 11.94, 39.4/17.1/8.0/3.8 (BP=1.000, ratio=1.069, hyp_len=13076, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.74.1.84-6.33.1.61-4.99.2.38-10.77.2.31-10.12.pth, mybk
BLEU = 13.85, 40.3/18.2/9.5/5.3 (BP=1.000, ratio=1.074, hyp_len=12281, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.74.1.84-6.33.1.61-4.99.2.38-10.77.2.31-10.12.pth, bkmy
BLEU = 11.59, 39.0/16.7/7.7/3.6 (BP=1.000, ratio=1.081, hyp_len=13220, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.75.1.81-6.12.1.60-4.96.2.38-10.76.2.32-10.13.pth, mybk
BLEU = 13.94, 40.6/18.4/9.5/5.3 (BP=1.000, ratio=1.064, hyp_len=12160, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.75.1.81-6.12.1.60-4.96.2.38-10.76.2.32-10.13.pth, bkmy
BLEU = 12.01, 39.4/17.2/7.9/3.9 (BP=1.000, ratio=1.069, hyp_len=13072, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.76.1.77-5.86.1.55-4.73.2.39-10.88.2.32-10.15.pth, mybk
BLEU = 13.93, 39.8/18.0/9.6/5.5 (BP=1.000, ratio=1.081, hyp_len=12353, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.76.1.77-5.86.1.55-4.73.2.39-10.88.2.32-10.15.pth, bkmy
BLEU = 11.55, 38.9/16.8/7.7/3.6 (BP=1.000, ratio=1.081, hyp_len=13226, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.77.1.80-6.03.1.59-4.91.2.39-10.91.2.32-10.18.pth, mybk
BLEU = 13.97, 40.2/18.4/9.6/5.3 (BP=1.000, ratio=1.077, hyp_len=12310, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.77.1.80-6.03.1.59-4.91.2.39-10.91.2.32-10.18.pth, bkmy
BLEU = 12.07, 39.4/17.2/8.1/3.8 (BP=1.000, ratio=1.071, hyp_len=13104, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.78.1.75-5.75.1.56-4.77.2.38-10.85.2.31-10.03.pth, mybk
BLEU = 14.04, 40.4/18.3/9.6/5.5 (BP=1.000, ratio=1.084, hyp_len=12393, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.78.1.75-5.75.1.56-4.77.2.38-10.85.2.31-10.03.pth, bkmy
BLEU = 11.21, 37.6/16.1/7.3/3.6 (BP=1.000, ratio=1.115, hyp_len=13642, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.79.1.70-5.47.1.50-4.50.2.37-10.67.2.31-10.11.pth, mybk
BLEU = 13.99, 40.9/18.3/9.5/5.4 (BP=1.000, ratio=1.064, hyp_len=12162, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.79.1.70-5.47.1.50-4.50.2.37-10.67.2.31-10.11.pth, bkmy
BLEU = 11.71, 39.4/16.8/7.8/3.7 (BP=1.000, ratio=1.069, hyp_len=13081, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.80.1.72-5.61.1.53-4.63.2.38-10.83.2.32-10.18.pth, mybk
BLEU = 13.69, 40.1/18.2/9.3/5.2 (BP=1.000, ratio=1.079, hyp_len=12338, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.80.1.72-5.61.1.53-4.63.2.38-10.83.2.32-10.18.pth, bkmy
BLEU = 11.91, 39.6/17.0/7.9/3.8 (BP=1.000, ratio=1.059, hyp_len=12953, ref_len=12231)
```

Best BLEU Score for my-bk, 68 epoch: 14.22 
Best BLEU Score for bk-my, 57 epoch: 12.31  

## Seq2Seq-DSL, my-bk, 90epoch

training

```
Epoch 1 - |param|=8.50e+02 |g_param|=4.40e+05 loss_x2y=4.8982e+00 ppl_x2y=134.05 loss_y2x=4.6988e+00 ppl_y2x=109.82 dual_loss=0.0000e+00
Validation X2Y - loss=4.0415e+00 ppl=56.91 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=3.9568e+00 ppl=52.29 best_loss=inf best_ppl=inf
Epoch 2 - |param|=8.50e+02 |g_param|=5.14e+05 loss_x2y=4.4576e+00 ppl_x2y=86.28 loss_y2x=4.2427e+00 ppl_y2x=69.60 dual_loss=0.0000e+00
Validation X2Y - loss=3.9699e+00 ppl=52.98 best_loss=4.0415e+00 best_ppl=56.91                                          
Validation Y2X - loss=3.7954e+00 ppl=44.50 best_loss=3.9568e+00 best_ppl=52.29
Epoch 3 - |param|=8.50e+02 |g_param|=3.02e+05 loss_x2y=4.3687e+00 ppl_x2y=78.94 loss_y2x=4.1401e+00 ppl_y2x=62.81 dual_loss=0.0000e+00
Validation X2Y - loss=3.8672e+00 ppl=47.81 best_loss=3.9699e+00 best_ppl=52.98                                          
Validation Y2X - loss=3.7380e+00 ppl=42.01 best_loss=3.7954e+00 best_ppl=44.50
Epoch 4 - |param|=8.50e+02 |g_param|=2.24e+05 loss_x2y=4.3368e+00 ppl_x2y=76.46 loss_y2x=4.1312e+00 ppl_y2x=62.25 dual_loss=0.0000e+00
Validation X2Y - loss=3.8626e+00 ppl=47.59 best_loss=3.8672e+00 best_ppl=47.81                                          
Validation Y2X - loss=3.7328e+00 ppl=41.79 best_loss=3.7380e+00 best_ppl=42.01
Epoch 5 - |param|=8.50e+02 |g_param|=2.19e+05 loss_x2y=4.3226e+00 ppl_x2y=75.39 loss_y2x=4.1106e+00 ppl_y2x=60.98 dual_loss=0.0000e+00
Validation X2Y - loss=3.8401e+00 ppl=46.53 best_loss=3.8626e+00 best_ppl=47.59                                          
Validation Y2X - loss=3.7391e+00 ppl=42.06 best_loss=3.7328e+00 best_ppl=41.79
Epoch 6 - |param|=8.50e+02 |g_param|=2.49e+05 loss_x2y=4.3179e+00 ppl_x2y=75.03 loss_y2x=4.1217e+00 ppl_y2x=61.67 dual_loss=0.0000e+00
Validation X2Y - loss=3.8092e+00 ppl=45.11 best_loss=3.8401e+00 best_ppl=46.53                                          
Validation Y2X - loss=3.6865e+00 ppl=39.91 best_loss=3.7328e+00 best_ppl=41.79
Epoch 7 - |param|=8.51e+02 |g_param|=2.04e+05 loss_x2y=4.2654e+00 ppl_x2y=71.19 loss_y2x=4.0716e+00 ppl_y2x=58.65 dual_loss=0.0000e+00
Validation X2Y - loss=3.7816e+00 ppl=43.89 best_loss=3.8092e+00 best_ppl=45.11                                          
Validation Y2X - loss=3.6854e+00 ppl=39.86 best_loss=3.6865e+00 best_ppl=39.91
Epoch 8 - |param|=8.51e+02 |g_param|=2.25e+05 loss_x2y=4.2619e+00 ppl_x2y=70.94 loss_y2x=4.0961e+00 ppl_y2x=60.11 dual_loss=0.0000e+00
Validation X2Y - loss=3.7426e+00 ppl=42.21 best_loss=3.7816e+00 best_ppl=43.89                                          
Validation Y2X - loss=3.6615e+00 ppl=38.92 best_loss=3.6854e+00 best_ppl=39.86
Epoch 9 - |param|=8.52e+02 |g_param|=2.23e+05 loss_x2y=4.2566e+00 ppl_x2y=70.57 loss_y2x=4.0262e+00 ppl_y2x=56.05 dual_loss=0.0000e+00
Validation X2Y - loss=3.7343e+00 ppl=41.86 best_loss=3.7426e+00 best_ppl=42.21                                          
Validation Y2X - loss=3.5960e+00 ppl=36.45 best_loss=3.6615e+00 best_ppl=38.92
Epoch 10 - |param|=8.52e+02 |g_param|=2.16e+05 loss_x2y=4.1342e+00 ppl_x2y=62.44 loss_y2x=3.9896e+00 ppl_y2x=54.04 dual_loss=0.0000e+00
Validation X2Y - loss=3.6399e+00 ppl=38.09 best_loss=3.7343e+00 best_ppl=41.86                                          
Validation Y2X - loss=3.5283e+00 ppl=34.07 best_loss=3.5960e+00 best_ppl=36.45
Epoch 11 - |param|=8.53e+02 |g_param|=1.82e+05 loss_x2y=3.9747e+00 ppl_x2y=53.23 loss_y2x=3.7807e+00 ppl_y2x=43.85 dual_loss=0.0000e+00
Validation X2Y - loss=3.4481e+00 ppl=31.44 best_loss=3.6399e+00 best_ppl=38.09                                          
Validation Y2X - loss=3.3378e+00 ppl=28.16 best_loss=3.5283e+00 best_ppl=34.07
Epoch 12 - |param|=8.53e+02 |g_param|=1.69e+05 loss_x2y=3.7755e+00 ppl_x2y=43.62 loss_y2x=3.6290e+00 ppl_y2x=37.67 dual_loss=0.0000e+00
Validation X2Y - loss=3.3358e+00 ppl=28.10 best_loss=3.4481e+00 best_ppl=31.44                                          
Validation Y2X - loss=3.2262e+00 ppl=25.18 best_loss=3.3378e+00 best_ppl=28.16
Epoch 13 - |param|=8.54e+02 |g_param|=1.64e+05 loss_x2y=3.6920e+00 ppl_x2y=40.12 loss_y2x=3.5323e+00 ppl_y2x=34.20 dual_loss=0.0000e+00
Validation X2Y - loss=3.2507e+00 ppl=25.81 best_loss=3.3358e+00 best_ppl=28.10                                          
Validation Y2X - loss=3.1274e+00 ppl=22.81 best_loss=3.2262e+00 best_ppl=25.18
Epoch 14 - |param|=8.55e+02 |g_param|=1.67e+05 loss_x2y=3.5749e+00 ppl_x2y=35.69 loss_y2x=3.4189e+00 ppl_y2x=30.54 dual_loss=0.0000e+00
Validation X2Y - loss=3.1700e+00 ppl=23.81 best_loss=3.2507e+00 best_ppl=25.81                                          
Validation Y2X - loss=3.0894e+00 ppl=21.96 best_loss=3.1274e+00 best_ppl=22.81
Epoch 15 - |param|=8.55e+02 |g_param|=1.43e+05 loss_x2y=3.4540e+00 ppl_x2y=31.63 loss_y2x=3.3372e+00 ppl_y2x=28.14 dual_loss=0.0000e+00
Validation X2Y - loss=3.0490e+00 ppl=21.09 best_loss=3.1700e+00 best_ppl=23.81                                          
Validation Y2X - loss=2.9824e+00 ppl=19.73 best_loss=3.0894e+00 best_ppl=21.96
Epoch 16 - |param|=8.56e+02 |g_param|=1.60e+05 loss_x2y=3.4059e+00 ppl_x2y=30.14 loss_y2x=3.2687e+00 ppl_y2x=26.28 dual_loss=0.0000e+00
Validation X2Y - loss=3.0047e+00 ppl=20.18 best_loss=3.0490e+00 best_ppl=21.09                                          
Validation Y2X - loss=2.9290e+00 ppl=18.71 best_loss=2.9824e+00 best_ppl=19.73
Epoch 17 - |param|=8.57e+02 |g_param|=1.49e+05 loss_x2y=3.3560e+00 ppl_x2y=28.67 loss_y2x=3.2600e+00 ppl_y2x=26.05 dual_loss=0.0000e+00
Validation X2Y - loss=2.9455e+00 ppl=19.02 best_loss=3.0047e+00 best_ppl=20.18                                          
Validation Y2X - loss=2.8864e+00 ppl=17.93 best_loss=2.9290e+00 best_ppl=18.71
Epoch 18 - |param|=8.57e+02 |g_param|=1.60e+05 loss_x2y=3.2677e+00 ppl_x2y=26.25 loss_y2x=3.1456e+00 ppl_y2x=23.23 dual_loss=0.0000e+00
Validation X2Y - loss=2.9137e+00 ppl=18.42 best_loss=2.9455e+00 best_ppl=19.02                                          
Validation Y2X - loss=2.8286e+00 ppl=16.92 best_loss=2.8864e+00 best_ppl=17.93
Epoch 19 - |param|=8.58e+02 |g_param|=1.64e+05 loss_x2y=3.3032e+00 ppl_x2y=27.20 loss_y2x=3.2091e+00 ppl_y2x=24.76 dual_loss=0.0000e+00
Validation X2Y - loss=2.8781e+00 ppl=17.78 best_loss=2.9137e+00 best_ppl=18.42                                          
Validation Y2X - loss=2.7587e+00 ppl=15.78 best_loss=2.8286e+00 best_ppl=16.92
Epoch 20 - |param|=8.59e+02 |g_param|=1.68e+05 loss_x2y=3.2412e+00 ppl_x2y=25.56 loss_y2x=3.0453e+00 ppl_y2x=21.02 dual_loss=0.0000e+00
Validation X2Y - loss=2.8190e+00 ppl=16.76 best_loss=2.8781e+00 best_ppl=17.78                                          
Validation Y2X - loss=2.7089e+00 ppl=15.01 best_loss=2.7587e+00 best_ppl=15.78
Epoch 21 - |param|=8.60e+02 |g_param|=1.63e+05 loss_x2y=3.1454e+00 ppl_x2y=23.23 loss_y2x=3.0204e+00 ppl_y2x=20.50 dual_loss=7.3028e-01
Validation X2Y - loss=2.8370e+00 ppl=17.06 best_loss=2.8190e+00 best_ppl=16.76                                          
Validation Y2X - loss=2.6732e+00 ppl=14.49 best_loss=2.7089e+00 best_ppl=15.01
Epoch 22 - |param|=8.60e+02 |g_param|=1.75e+05 loss_x2y=3.2451e+00 ppl_x2y=25.66 loss_y2x=3.0250e+00 ppl_y2x=20.59 dual_loss=8.2148e-01
Validation X2Y - loss=2.7873e+00 ppl=16.24 best_loss=2.8190e+00 best_ppl=16.76                                          
Validation Y2X - loss=2.6690e+00 ppl=14.43 best_loss=2.6732e+00 best_ppl=14.49
Epoch 23 - |param|=8.61e+02 |g_param|=1.68e+05 loss_x2y=3.1607e+00 ppl_x2y=23.59 loss_y2x=2.9314e+00 ppl_y2x=18.75 dual_loss=7.4926e-01
Validation X2Y - loss=2.7597e+00 ppl=15.80 best_loss=2.7873e+00 best_ppl=16.24                                          
Validation Y2X - loss=2.5947e+00 ppl=13.39 best_loss=2.6690e+00 best_ppl=14.43
Epoch 24 - |param|=8.62e+02 |g_param|=1.70e+05 loss_x2y=3.0568e+00 ppl_x2y=21.26 loss_y2x=2.9410e+00 ppl_y2x=18.94 dual_loss=6.0885e-01
Validation X2Y - loss=2.7388e+00 ppl=15.47 best_loss=2.7597e+00 best_ppl=15.80                                          
Validation Y2X - loss=2.5381e+00 ppl=12.66 best_loss=2.5947e+00 best_ppl=13.39
Epoch 25 - |param|=8.63e+02 |g_param|=1.70e+05 loss_x2y=2.9544e+00 ppl_x2y=19.19 loss_y2x=2.7899e+00 ppl_y2x=16.28 dual_loss=5.0474e-01
Validation X2Y - loss=2.7110e+00 ppl=15.04 best_loss=2.7388e+00 best_ppl=15.47                                          
Validation Y2X - loss=2.4919e+00 ppl=12.08 best_loss=2.5381e+00 best_ppl=12.66
Epoch 26 - |param|=8.63e+02 |g_param|=1.76e+05 loss_x2y=2.9532e+00 ppl_x2y=19.17 loss_y2x=2.8327e+00 ppl_y2x=16.99 dual_loss=5.3109e-01
Validation X2Y - loss=2.6732e+00 ppl=14.49 best_loss=2.7110e+00 best_ppl=15.04                                          
Validation Y2X - loss=2.4870e+00 ppl=12.02 best_loss=2.4919e+00 best_ppl=12.08
Epoch 27 - |param|=8.64e+02 |g_param|=1.69e+05 loss_x2y=2.8932e+00 ppl_x2y=18.05 loss_y2x=2.7220e+00 ppl_y2x=15.21 dual_loss=4.9260e-01
Validation X2Y - loss=2.6814e+00 ppl=14.61 best_loss=2.6732e+00 best_ppl=14.49                                          
Validation Y2X - loss=2.4279e+00 ppl=11.34 best_loss=2.4870e+00 best_ppl=12.02
Epoch 28 - |param|=8.65e+02 |g_param|=1.78e+05 loss_x2y=2.7861e+00 ppl_x2y=16.22 loss_y2x=2.5963e+00 ppl_y2x=13.41 dual_loss=3.8449e-01
Validation X2Y - loss=2.6688e+00 ppl=14.42 best_loss=2.6732e+00 best_ppl=14.49                                          
Validation Y2X - loss=2.4020e+00 ppl=11.05 best_loss=2.4279e+00 best_ppl=11.34
Epoch 29 - |param|=8.66e+02 |g_param|=1.86e+05 loss_x2y=2.7844e+00 ppl_x2y=16.19 loss_y2x=2.5854e+00 ppl_y2x=13.27 dual_loss=4.0101e-01
Validation X2Y - loss=2.6587e+00 ppl=14.28 best_loss=2.6688e+00 best_ppl=14.42                                          
Validation Y2X - loss=2.3762e+00 ppl=10.76 best_loss=2.4020e+00 best_ppl=11.05
Epoch 30 - |param|=8.66e+02 |g_param|=1.88e+05 loss_x2y=2.7618e+00 ppl_x2y=15.83 loss_y2x=2.5649e+00 ppl_y2x=13.00 dual_loss=4.0829e-01
Validation X2Y - loss=2.6542e+00 ppl=14.21 best_loss=2.6587e+00 best_ppl=14.28                                          
Validation Y2X - loss=2.3609e+00 ppl=10.60 best_loss=2.3762e+00 best_ppl=10.76
Epoch 31 - |param|=8.67e+02 |g_param|=1.82e+05 loss_x2y=2.6759e+00 ppl_x2y=14.52 loss_y2x=2.4967e+00 ppl_y2x=12.14 dual_loss=3.6752e-01
Validation X2Y - loss=2.6326e+00 ppl=13.91 best_loss=2.6542e+00 best_ppl=14.21                                          
Validation Y2X - loss=2.3168e+00 ppl=10.14 best_loss=2.3609e+00 best_ppl=10.60
Epoch 32 - |param|=8.68e+02 |g_param|=2.02e+05 loss_x2y=2.7007e+00 ppl_x2y=14.89 loss_y2x=2.5229e+00 ppl_y2x=12.46 dual_loss=4.0321e-01
Validation X2Y - loss=2.6078e+00 ppl=13.57 best_loss=2.6326e+00 best_ppl=13.91                                          
Validation Y2X - loss=2.3197e+00 ppl=10.17 best_loss=2.3168e+00 best_ppl=10.14
Epoch 33 - |param|=8.68e+02 |g_param|=1.88e+05 loss_x2y=2.6385e+00 ppl_x2y=13.99 loss_y2x=2.4405e+00 ppl_y2x=11.48 dual_loss=3.4658e-01
Validation X2Y - loss=2.6230e+00 ppl=13.78 best_loss=2.6078e+00 best_ppl=13.57                                          
Validation Y2X - loss=2.2821e+00 ppl=9.80 best_loss=2.3168e+00 best_ppl=10.14
Epoch 34 - |param|=8.69e+02 |g_param|=1.99e+05 loss_x2y=2.6117e+00 ppl_x2y=13.62 loss_y2x=2.3926e+00 ppl_y2x=10.94 dual_loss=3.3452e-01
Validation X2Y - loss=2.5995e+00 ppl=13.46 best_loss=2.6078e+00 best_ppl=13.57                                          
Validation Y2X - loss=2.2737e+00 ppl=9.72 best_loss=2.2821e+00 best_ppl=9.80
Epoch 35 - |param|=8.70e+02 |g_param|=2.05e+05 loss_x2y=2.5913e+00 ppl_x2y=13.35 loss_y2x=2.3609e+00 ppl_y2x=10.60 dual_loss=3.3499e-01
Validation X2Y - loss=2.5895e+00 ppl=13.32 best_loss=2.5995e+00 best_ppl=13.46                                          
Validation Y2X - loss=2.3441e+00 ppl=10.42 best_loss=2.2737e+00 best_ppl=9.72
Epoch 36 - |param|=8.71e+02 |g_param|=3.97e+05 loss_x2y=2.5337e+00 ppl_x2y=12.60 loss_y2x=2.2914e+00 ppl_y2x=9.89 dual_loss=3.1067e-01
Validation X2Y - loss=2.5815e+00 ppl=13.22 best_loss=2.5895e+00 best_ppl=13.32                                          
Validation Y2X - loss=2.2000e+00 ppl=9.02 best_loss=2.2737e+00 best_ppl=9.72
Epoch 37 - |param|=8.71e+02 |g_param|=3.97e+05 loss_x2y=2.4917e+00 ppl_x2y=12.08 loss_y2x=2.2724e+00 ppl_y2x=9.70 dual_loss=2.9322e-01
Validation X2Y - loss=2.5906e+00 ppl=13.34 best_loss=2.5815e+00 best_ppl=13.22                                          
Validation Y2X - loss=2.1936e+00 ppl=8.97 best_loss=2.2000e+00 best_ppl=9.02
Epoch 38 - |param|=8.72e+02 |g_param|=4.24e+05 loss_x2y=2.5021e+00 ppl_x2y=12.21 loss_y2x=2.2664e+00 ppl_y2x=9.64 dual_loss=3.0594e-01
Validation X2Y - loss=2.5925e+00 ppl=13.36 best_loss=2.5815e+00 best_ppl=13.22                                          
Validation Y2X - loss=2.1946e+00 ppl=8.98 best_loss=2.1936e+00 best_ppl=8.97
Epoch 39 - |param|=8.73e+02 |g_param|=4.04e+05 loss_x2y=2.4282e+00 ppl_x2y=11.34 loss_y2x=2.1983e+00 ppl_y2x=9.01 dual_loss=2.9519e-01
Validation X2Y - loss=2.5834e+00 ppl=13.24 best_loss=2.5815e+00 best_ppl=13.22                                          
Validation Y2X - loss=2.1878e+00 ppl=8.92 best_loss=2.1936e+00 best_ppl=8.97
Epoch 40 - |param|=8.73e+02 |g_param|=4.39e+05 loss_x2y=2.4409e+00 ppl_x2y=11.48 loss_y2x=2.2001e+00 ppl_y2x=9.03 dual_loss=2.9226e-01
Validation X2Y - loss=2.6030e+00 ppl=13.50 best_loss=2.5815e+00 best_ppl=13.22                                          
Validation Y2X - loss=2.1799e+00 ppl=8.85 best_loss=2.1878e+00 best_ppl=8.92
Epoch 41 - |param|=8.74e+02 |g_param|=4.08e+05 loss_x2y=2.3736e+00 ppl_x2y=10.74 loss_y2x=2.1182e+00 ppl_y2x=8.32 dual_loss=2.7931e-01
Validation X2Y - loss=2.5628e+00 ppl=12.97 best_loss=2.5815e+00 best_ppl=13.22                                          
Validation Y2X - loss=2.1518e+00 ppl=8.60 best_loss=2.1799e+00 best_ppl=8.85
Epoch 42 - |param|=8.75e+02 |g_param|=4.59e+05 loss_x2y=2.3301e+00 ppl_x2y=10.28 loss_y2x=2.1079e+00 ppl_y2x=8.23 dual_loss=2.9209e-01
Validation X2Y - loss=2.5707e+00 ppl=13.08 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=2.1377e+00 ppl=8.48 best_loss=2.1518e+00 best_ppl=8.60
Epoch 43 - |param|=8.75e+02 |g_param|=4.58e+05 loss_x2y=2.3438e+00 ppl_x2y=10.42 loss_y2x=2.1236e+00 ppl_y2x=8.36 dual_loss=3.0168e-01
Validation X2Y - loss=2.6028e+00 ppl=13.50 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=2.1557e+00 ppl=8.63 best_loss=2.1377e+00 best_ppl=8.48
Epoch 44 - |param|=8.76e+02 |g_param|=4.66e+05 loss_x2y=2.3137e+00 ppl_x2y=10.11 loss_y2x=2.0449e+00 ppl_y2x=7.73 dual_loss=2.7992e-01
Validation X2Y - loss=2.5702e+00 ppl=13.07 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=2.0807e+00 ppl=8.01 best_loss=2.1377e+00 best_ppl=8.48
Epoch 45 - |param|=8.77e+02 |g_param|=4.54e+05 loss_x2y=2.2674e+00 ppl_x2y=9.65 loss_y2x=2.0540e+00 ppl_y2x=7.80 dual_loss=2.8477e-01
Validation X2Y - loss=2.6058e+00 ppl=13.54 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=2.1157e+00 ppl=8.30 best_loss=2.0807e+00 best_ppl=8.01
Epoch 46 - |param|=8.77e+02 |g_param|=4.68e+05 loss_x2y=2.2542e+00 ppl_x2y=9.53 loss_y2x=2.0082e+00 ppl_y2x=7.45 dual_loss=2.8409e-01
Validation X2Y - loss=2.5845e+00 ppl=13.26 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=2.0698e+00 ppl=7.92 best_loss=2.0807e+00 best_ppl=8.01
Epoch 47 - |param|=8.78e+02 |g_param|=4.66e+05 loss_x2y=2.2373e+00 ppl_x2y=9.37 loss_y2x=1.9630e+00 ppl_y2x=7.12 dual_loss=2.7825e-01
Validation X2Y - loss=2.5928e+00 ppl=13.37 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=2.0800e+00 ppl=8.00 best_loss=2.0698e+00 best_ppl=7.92
Epoch 48 - |param|=8.78e+02 |g_param|=4.91e+05 loss_x2y=2.2359e+00 ppl_x2y=9.35 loss_y2x=1.9705e+00 ppl_y2x=7.17 dual_loss=2.8989e-01
Validation X2Y - loss=2.5862e+00 ppl=13.28 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=2.0493e+00 ppl=7.76 best_loss=2.0698e+00 best_ppl=7.92
Epoch 49 - |param|=8.79e+02 |g_param|=4.72e+05 loss_x2y=2.1642e+00 ppl_x2y=8.71 loss_y2x=1.8871e+00 ppl_y2x=6.60 dual_loss=2.8412e-01
Validation X2Y - loss=2.5778e+00 ppl=13.17 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=2.0479e+00 ppl=7.75 best_loss=2.0493e+00 best_ppl=7.76
Epoch 50 - |param|=8.80e+02 |g_param|=4.91e+05 loss_x2y=2.2061e+00 ppl_x2y=9.08 loss_y2x=1.9270e+00 ppl_y2x=6.87 dual_loss=2.9328e-01
Validation X2Y - loss=2.6157e+00 ppl=13.68 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=2.0283e+00 ppl=7.60 best_loss=2.0479e+00 best_ppl=7.75
Epoch 51 - |param|=8.80e+02 |g_param|=4.96e+05 loss_x2y=2.1066e+00 ppl_x2y=8.22 loss_y2x=1.8072e+00 ppl_y2x=6.09 dual_loss=2.7236e-01
Validation X2Y - loss=2.6118e+00 ppl=13.62 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=2.0353e+00 ppl=7.65 best_loss=2.0283e+00 best_ppl=7.60
Epoch 52 - |param|=8.81e+02 |g_param|=5.55e+05 loss_x2y=2.1136e+00 ppl_x2y=8.28 loss_y2x=1.8078e+00 ppl_y2x=6.10 dual_loss=2.8039e-01
Validation X2Y - loss=2.6269e+00 ppl=13.83 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=2.0215e+00 ppl=7.55 best_loss=2.0283e+00 best_ppl=7.60
Epoch 53 - |param|=8.82e+02 |g_param|=4.94e+05 loss_x2y=2.0784e+00 ppl_x2y=7.99 loss_y2x=1.7889e+00 ppl_y2x=5.98 dual_loss=2.8390e-01
Validation X2Y - loss=2.6200e+00 ppl=13.74 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=2.0323e+00 ppl=7.63 best_loss=2.0215e+00 best_ppl=7.55
Epoch 54 - |param|=8.82e+02 |g_param|=5.08e+05 loss_x2y=2.0507e+00 ppl_x2y=7.77 loss_y2x=1.7558e+00 ppl_y2x=5.79 dual_loss=2.8736e-01
Validation X2Y - loss=2.5926e+00 ppl=13.36 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=2.0143e+00 ppl=7.50 best_loss=2.0215e+00 best_ppl=7.55
Epoch 55 - |param|=8.83e+02 |g_param|=4.92e+05 loss_x2y=2.0564e+00 ppl_x2y=7.82 loss_y2x=1.7942e+00 ppl_y2x=6.01 dual_loss=2.9551e-01
Validation X2Y - loss=2.6292e+00 ppl=13.86 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9863e+00 ppl=7.29 best_loss=2.0143e+00 best_ppl=7.50
Epoch 56 - |param|=8.83e+02 |g_param|=5.36e+05 loss_x2y=2.0345e+00 ppl_x2y=7.65 loss_y2x=1.7618e+00 ppl_y2x=5.82 dual_loss=3.1465e-01
Validation X2Y - loss=2.6096e+00 ppl=13.59 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9901e+00 ppl=7.32 best_loss=1.9863e+00 best_ppl=7.29
Epoch 57 - |param|=8.84e+02 |g_param|=4.93e+05 loss_x2y=1.9501e+00 ppl_x2y=7.03 loss_y2x=1.6880e+00 ppl_y2x=5.41 dual_loss=2.9531e-01
Validation X2Y - loss=2.6225e+00 ppl=13.77 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9709e+00 ppl=7.18 best_loss=1.9863e+00 best_ppl=7.29
Epoch 58 - |param|=8.85e+02 |g_param|=5.64e+05 loss_x2y=2.0083e+00 ppl_x2y=7.45 loss_y2x=1.6837e+00 ppl_y2x=5.39 dual_loss=3.0332e-01
Validation X2Y - loss=2.6138e+00 ppl=13.65 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9916e+00 ppl=7.33 best_loss=1.9709e+00 best_ppl=7.18
Epoch 59 - |param|=8.85e+02 |g_param|=5.47e+05 loss_x2y=1.9801e+00 ppl_x2y=7.24 loss_y2x=1.7640e+00 ppl_y2x=5.84 dual_loss=3.1636e-01
Validation X2Y - loss=2.6480e+00 ppl=14.13 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9855e+00 ppl=7.28 best_loss=1.9709e+00 best_ppl=7.18
Epoch 60 - |param|=8.86e+02 |g_param|=5.59e+05 loss_x2y=1.9473e+00 ppl_x2y=7.01 loss_y2x=1.6434e+00 ppl_y2x=5.17 dual_loss=3.0061e-01
Validation X2Y - loss=2.6614e+00 ppl=14.32 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9593e+00 ppl=7.09 best_loss=1.9709e+00 best_ppl=7.18
Epoch 61 - |param|=8.86e+02 |g_param|=5.76e+05 loss_x2y=2.0024e+00 ppl_x2y=7.41 loss_y2x=1.7183e+00 ppl_y2x=5.58 dual_loss=3.3612e-01
Validation X2Y - loss=2.6470e+00 ppl=14.11 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9785e+00 ppl=7.23 best_loss=1.9593e+00 best_ppl=7.09
Epoch 62 - |param|=8.87e+02 |g_param|=5.93e+05 loss_x2y=1.8844e+00 ppl_x2y=6.58 loss_y2x=1.5969e+00 ppl_y2x=4.94 dual_loss=2.9604e-01
Validation X2Y - loss=2.6455e+00 ppl=14.09 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9583e+00 ppl=7.09 best_loss=1.9593e+00 best_ppl=7.09
Epoch 63 - |param|=8.88e+02 |g_param|=5.63e+05 loss_x2y=1.9079e+00 ppl_x2y=6.74 loss_y2x=1.6593e+00 ppl_y2x=5.26 dual_loss=3.3004e-01
Validation X2Y - loss=2.6328e+00 ppl=13.91 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9377e+00 ppl=6.94 best_loss=1.9583e+00 best_ppl=7.09
Epoch 64 - |param|=8.88e+02 |g_param|=5.85e+05 loss_x2y=1.8492e+00 ppl_x2y=6.35 loss_y2x=1.5382e+00 ppl_y2x=4.66 dual_loss=3.0051e-01
Validation X2Y - loss=2.6583e+00 ppl=14.27 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9080e+00 ppl=6.74 best_loss=1.9377e+00 best_ppl=6.94
Epoch 65 - |param|=8.89e+02 |g_param|=5.53e+05 loss_x2y=1.8520e+00 ppl_x2y=6.37 loss_y2x=1.5601e+00 ppl_y2x=4.76 dual_loss=3.1194e-01
Validation X2Y - loss=2.6662e+00 ppl=14.38 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9279e+00 ppl=6.88 best_loss=1.9080e+00 best_ppl=6.74
Epoch 66 - |param|=8.89e+02 |g_param|=6.10e+05 loss_x2y=1.9046e+00 ppl_x2y=6.72 loss_y2x=1.6445e+00 ppl_y2x=5.18 dual_loss=3.6112e-01
Validation X2Y - loss=2.6811e+00 ppl=14.60 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9328e+00 ppl=6.91 best_loss=1.9080e+00 best_ppl=6.74
Epoch 67 - |param|=8.90e+02 |g_param|=5.94e+05 loss_x2y=1.8134e+00 ppl_x2y=6.13 loss_y2x=1.5112e+00 ppl_y2x=4.53 dual_loss=3.2809e-01
Validation X2Y - loss=2.6856e+00 ppl=14.67 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9251e+00 ppl=6.86 best_loss=1.9080e+00 best_ppl=6.74
Epoch 68 - |param|=8.90e+02 |g_param|=8.87e+05 loss_x2y=1.7848e+00 ppl_x2y=5.96 loss_y2x=1.5214e+00 ppl_y2x=4.58 dual_loss=3.2836e-01
Validation X2Y - loss=2.6814e+00 ppl=14.61 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9452e+00 ppl=6.99 best_loss=1.9080e+00 best_ppl=6.74
Epoch 69 - |param|=8.91e+02 |g_param|=1.21e+06 loss_x2y=1.8464e+00 ppl_x2y=6.34 loss_y2x=1.5685e+00 ppl_y2x=4.80 dual_loss=3.6537e-01
Validation X2Y - loss=2.7039e+00 ppl=14.94 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9150e+00 ppl=6.79 best_loss=1.9080e+00 best_ppl=6.74
Epoch 70 - |param|=8.92e+02 |g_param|=1.20e+06 loss_x2y=1.7935e+00 ppl_x2y=6.01 loss_y2x=1.5444e+00 ppl_y2x=4.69 dual_loss=3.5781e-01
Validation X2Y - loss=2.7064e+00 ppl=14.98 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9255e+00 ppl=6.86 best_loss=1.9080e+00 best_ppl=6.74
Epoch 71 - |param|=8.92e+02 |g_param|=1.17e+06 loss_x2y=1.7252e+00 ppl_x2y=5.61 loss_y2x=1.4781e+00 ppl_y2x=4.38 dual_loss=3.3470e-01
Validation X2Y - loss=2.6929e+00 ppl=14.77 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9280e+00 ppl=6.88 best_loss=1.9080e+00 best_ppl=6.74
Epoch 72 - |param|=8.93e+02 |g_param|=1.23e+06 loss_x2y=1.7028e+00 ppl_x2y=5.49 loss_y2x=1.4176e+00 ppl_y2x=4.13 dual_loss=3.5059e-01
Validation X2Y - loss=2.7028e+00 ppl=14.92 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9418e+00 ppl=6.97 best_loss=1.9080e+00 best_ppl=6.74
Epoch 73 - |param|=8.93e+02 |g_param|=1.18e+06 loss_x2y=1.7176e+00 ppl_x2y=5.57 loss_y2x=1.4229e+00 ppl_y2x=4.15 dual_loss=3.3847e-01
Validation X2Y - loss=2.7272e+00 ppl=15.29 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9086e+00 ppl=6.74 best_loss=1.9080e+00 best_ppl=6.74
Epoch 74 - |param|=8.94e+02 |g_param|=8.83e+05 loss_x2y=1.7433e+00 ppl_x2y=5.72 loss_y2x=1.4714e+00 ppl_y2x=4.36 dual_loss=3.7305e-01
Validation X2Y - loss=2.7334e+00 ppl=15.39 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9368e+00 ppl=6.94 best_loss=1.9080e+00 best_ppl=6.74
Epoch 75 - |param|=8.94e+02 |g_param|=7.34e+05 loss_x2y=1.6552e+00 ppl_x2y=5.23 loss_y2x=1.3347e+00 ppl_y2x=3.80 dual_loss=3.2520e-01
Validation X2Y - loss=2.7304e+00 ppl=15.34 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9287e+00 ppl=6.88 best_loss=1.9080e+00 best_ppl=6.74
Epoch 76 - |param|=8.95e+02 |g_param|=7.67e+05 loss_x2y=1.6134e+00 ppl_x2y=5.02 loss_y2x=1.3323e+00 ppl_y2x=3.79 dual_loss=3.4266e-01
Validation X2Y - loss=2.7341e+00 ppl=15.40 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9190e+00 ppl=6.81 best_loss=1.9080e+00 best_ppl=6.74
Epoch 77 - |param|=8.95e+02 |g_param|=7.40e+05 loss_x2y=1.6190e+00 ppl_x2y=5.05 loss_y2x=1.3048e+00 ppl_y2x=3.69 dual_loss=3.5252e-01
Validation X2Y - loss=2.7461e+00 ppl=15.58 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9042e+00 ppl=6.71 best_loss=1.9080e+00 best_ppl=6.74
Epoch 78 - |param|=8.96e+02 |g_param|=7.94e+05 loss_x2y=1.6024e+00 ppl_x2y=4.97 loss_y2x=1.3173e+00 ppl_y2x=3.73 dual_loss=3.4339e-01
Validation X2Y - loss=2.7688e+00 ppl=15.94 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9348e+00 ppl=6.92 best_loss=1.9042e+00 best_ppl=6.71
Epoch 79 - |param|=8.96e+02 |g_param|=7.95e+05 loss_x2y=1.6201e+00 ppl_x2y=5.05 loss_y2x=1.3670e+00 ppl_y2x=3.92 dual_loss=3.4848e-01
Validation X2Y - loss=2.7333e+00 ppl=15.38 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.8961e+00 ppl=6.66 best_loss=1.9042e+00 best_ppl=6.71
Epoch 80 - |param|=8.97e+02 |g_param|=8.28e+05 loss_x2y=1.6470e+00 ppl_x2y=5.19 loss_y2x=1.3205e+00 ppl_y2x=3.75 dual_loss=3.8399e-01
Validation X2Y - loss=2.7423e+00 ppl=15.52 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9136e+00 ppl=6.78 best_loss=1.8961e+00 best_ppl=6.66
Epoch 81 - |param|=8.98e+02 |g_param|=8.32e+05 loss_x2y=1.6193e+00 ppl_x2y=5.05 loss_y2x=1.3710e+00 ppl_y2x=3.94 dual_loss=3.7127e-01
Validation X2Y - loss=2.7740e+00 ppl=16.02 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9471e+00 ppl=7.01 best_loss=1.8961e+00 best_ppl=6.66
Epoch 82 - |param|=8.98e+02 |g_param|=8.45e+05 loss_x2y=1.5965e+00 ppl_x2y=4.94 loss_y2x=1.3026e+00 ppl_y2x=3.68 dual_loss=4.0582e-01
Validation X2Y - loss=2.7855e+00 ppl=16.21 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9183e+00 ppl=6.81 best_loss=1.8961e+00 best_ppl=6.66
Epoch 83 - |param|=8.99e+02 |g_param|=7.70e+05 loss_x2y=1.5215e+00 ppl_x2y=4.58 loss_y2x=1.2269e+00 ppl_y2x=3.41 dual_loss=3.5929e-01
Validation X2Y - loss=2.7672e+00 ppl=15.91 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9242e+00 ppl=6.85 best_loss=1.8961e+00 best_ppl=6.66
Epoch 84 - |param|=8.99e+02 |g_param|=8.43e+05 loss_x2y=1.5682e+00 ppl_x2y=4.80 loss_y2x=1.2555e+00 ppl_y2x=3.51 dual_loss=3.8369e-01
Validation X2Y - loss=2.7852e+00 ppl=16.20 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9111e+00 ppl=6.76 best_loss=1.8961e+00 best_ppl=6.66
Epoch 85 - |param|=9.00e+02 |g_param|=7.98e+05 loss_x2y=1.5099e+00 ppl_x2y=4.53 loss_y2x=1.2135e+00 ppl_y2x=3.37 dual_loss=3.8026e-01
Validation X2Y - loss=2.7957e+00 ppl=16.37 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9242e+00 ppl=6.85 best_loss=1.8961e+00 best_ppl=6.66
Epoch 86 - |param|=9.00e+02 |g_param|=8.62e+05 loss_x2y=1.5123e+00 ppl_x2y=4.54 loss_y2x=1.2463e+00 ppl_y2x=3.48 dual_loss=3.5845e-01
Validation X2Y - loss=2.8137e+00 ppl=16.67 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9735e+00 ppl=7.20 best_loss=1.8961e+00 best_ppl=6.66
Epoch 87 - |param|=9.01e+02 |g_param|=7.99e+05 loss_x2y=1.5481e+00 ppl_x2y=4.70 loss_y2x=1.2787e+00 ppl_y2x=3.59 dual_loss=3.9449e-01
Validation X2Y - loss=2.8121e+00 ppl=16.65 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9191e+00 ppl=6.81 best_loss=1.8961e+00 best_ppl=6.66
Epoch 88 - |param|=9.01e+02 |g_param|=7.97e+05 loss_x2y=1.4698e+00 ppl_x2y=4.35 loss_y2x=1.1632e+00 ppl_y2x=3.20 dual_loss=3.6460e-01
Validation X2Y - loss=2.8119e+00 ppl=16.64 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9207e+00 ppl=6.83 best_loss=1.8961e+00 best_ppl=6.66
Epoch 89 - |param|=9.02e+02 |g_param|=8.08e+05 loss_x2y=1.5460e+00 ppl_x2y=4.69 loss_y2x=1.1986e+00 ppl_y2x=3.32 dual_loss=3.9874e-01
Validation X2Y - loss=2.8392e+00 ppl=17.10 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9471e+00 ppl=7.01 best_loss=1.8961e+00 best_ppl=6.66
Epoch 90 - |param|=9.02e+02 |g_param|=8.34e+05 loss_x2y=1.4795e+00 ppl_x2y=4.39 loss_y2x=1.2235e+00 ppl_y2x=3.40 dual_loss=3.8465e-01
Validation X2Y - loss=2.8127e+00 ppl=16.66 best_loss=2.5628e+00 best_ppl=12.97                                          
Validation Y2X - loss=1.9560e+00 ppl=7.07 best_loss=1.8961e+00 best_ppl=6.66

real	24m30.378s
user	24m9.727s
sys	0m18.345s
```

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/mybk-90epoch
Evaluation result for the model: dsl-model-mybk.01.4.90-134.05.4.70-109.82.4.04-56.91.3.96-52.29.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.5/0.0/0.0/0.0 (BP=0.727, ratio=0.758, hyp_len=8668, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.90-134.05.4.70-109.82.4.04-56.91.3.96-52.29.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.1/0.1/0.0/0.0 (BP=0.784, ratio=0.804, hyp_len=9836, ref_len=12231)
Traceback (most recent call last):
  File "/home/ye/exp/simple-nmt/translate.py", line 182, in <module>
    map_location='cpu',
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/serialization.py", line 608, in load
    return _legacy_load(opened_file, map_location, pickle_module, **pickle_load_args)
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/serialization.py", line 777, in _legacy_load
    magic_number = pickle_module.load(f, **pickle_load_args)
EOFError: Ran out of input
Evaluation result for the model: dsl-model-mybk.01.4.91-136.22.4.74-114.62.4.21-67.08.3.96-52.40.pth, mybk
Use of uninitialized value $length_reference in numeric eq (==) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 148.
BLEU = 0, 0/0/0/0 (BP=0, ratio=0, hyp_len=0, ref_len=0)
Traceback (most recent call last):
  File "/home/ye/exp/simple-nmt/translate.py", line 182, in <module>
    map_location='cpu',
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/serialization.py", line 608, in load
    return _legacy_load(opened_file, map_location, pickle_module, **pickle_load_args)
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/serialization.py", line 777, in _legacy_load
    magic_number = pickle_module.load(f, **pickle_load_args)
EOFError: Ran out of input
Evaluation result for the model: dsl-model-mybk.01.4.91-136.22.4.74-114.62.4.21-67.08.3.96-52.40.pth, bkmy
Use of uninitialized value $length_reference in numeric eq (==) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 148.
BLEU = 0, 0/0/0/0 (BP=0, ratio=0, hyp_len=0, ref_len=0)
Evaluation result for the model: dsl-model-mybk.02.4.46-86.28.4.24-69.60.3.97-52.98.3.80-44.50.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 17.8/0.3/0.0/0.0 (BP=0.995, ratio=0.995, hyp_len=11377, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.4.46-86.28.4.24-69.60.3.97-52.98.3.80-44.50.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.6/0.6/0.0/0.0 (BP=0.871, ratio=0.879, hyp_len=10750, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.4.37-78.94.4.14-62.81.3.87-47.81.3.74-42.01.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.1/0.2/0.0/0.0 (BP=1.000, ratio=1.065, hyp_len=12172, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.4.37-78.94.4.14-62.81.3.87-47.81.3.74-42.01.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.9/1.7/0.2/0.0 (BP=0.950, ratio=0.952, hyp_len=11640, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.4.34-76.46.4.13-62.25.3.86-47.59.3.73-41.79.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.5/0.0/0.0/0.0 (BP=1.000, ratio=1.034, hyp_len=11823, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.4.34-76.46.4.13-62.25.3.86-47.59.3.73-41.79.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.4/0.4/0.0/0.0 (BP=0.964, ratio=0.965, hyp_len=11798, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.4.32-75.39.4.11-60.98.3.84-46.53.3.74-42.06.pth, mybk
BLEU = 0.30, 18.8/0.5/0.1/0.0 (BP=1.000, ratio=1.020, hyp_len=11662, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.4.32-75.39.4.11-60.98.3.84-46.53.3.74-42.06.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.3/0.5/0.0/0.0 (BP=1.000, ratio=1.013, hyp_len=12389, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.4.32-75.03.4.12-61.67.3.81-45.11.3.69-39.91.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.5/0.1/0.0/0.0 (BP=1.000, ratio=1.059, hyp_len=12101, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.4.32-75.03.4.12-61.67.3.81-45.11.3.69-39.91.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.9/0.5/0.0/0.0 (BP=0.968, ratio=0.968, hyp_len=11844, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.4.27-71.19.4.07-58.65.3.78-43.89.3.69-39.86.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.4/0.2/0.0/0.0 (BP=1.000, ratio=1.064, hyp_len=12165, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.4.27-71.19.4.07-58.65.3.78-43.89.3.69-39.86.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.3/0.6/0.0/0.0 (BP=1.000, ratio=1.060, hyp_len=12964, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.4.26-70.94.4.10-60.11.3.74-42.21.3.66-38.92.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.5/0.3/0.0/0.0 (BP=1.000, ratio=1.100, hyp_len=12571, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.4.26-70.94.4.10-60.11.3.74-42.21.3.66-38.92.pth, bkmy
BLEU = 0.38, 21.6/1.3/0.1/0.0 (BP=1.000, ratio=1.016, hyp_len=12426, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.4.26-70.57.4.03-56.05.3.73-41.86.3.60-36.45.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 18.2/0.3/0.0/0.0 (BP=1.000, ratio=1.047, hyp_len=11972, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.4.26-70.57.4.03-56.05.3.73-41.86.3.60-36.45.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.4/1.8/0.1/0.0 (BP=1.000, ratio=1.047, hyp_len=12801, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.4.13-62.44.3.99-54.04.3.64-38.09.3.53-34.07.pth, mybk
BLEU = 0.18, 21.2/0.2/0.0/0.0 (BP=0.770, ratio=0.793, hyp_len=9061, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.4.13-62.44.3.99-54.04.3.64-38.09.3.53-34.07.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 10.7/0.6/0.0/0.0 (BP=1.000, ratio=1.659, hyp_len=20292, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.3.97-53.23.3.78-43.85.3.45-31.44.3.34-28.16.pth, mybk
BLEU = 0.67, 23.3/2.9/0.2/0.0 (BP=0.921, ratio=0.924, hyp_len=10561, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.3.97-53.23.3.78-43.85.3.45-31.44.3.34-28.16.pth, bkmy
BLEU = 0.55, 21.0/1.6/0.3/0.0 (BP=1.000, ratio=1.028, hyp_len=12572, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.3.78-43.62.3.63-37.67.3.34-28.10.3.23-25.18.pth, mybk
BLEU = 2.21, 26.7/4.7/1.0/0.3 (BP=0.929, ratio=0.931, hyp_len=10648, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.3.78-43.62.3.63-37.67.3.34-28.10.3.23-25.18.pth, bkmy
BLEU = 0.06, 1.9/0.3/0.0/0.0 (BP=1.000, ratio=9.392, hyp_len=114869, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.3.69-40.12.3.53-34.20.3.25-25.81.3.13-22.81.pth, mybk
BLEU = 3.78, 22.6/5.5/1.9/0.8 (BP=1.000, ratio=1.055, hyp_len=12060, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.3.69-40.12.3.53-34.20.3.25-25.81.3.13-22.81.pth, bkmy
BLEU = 0.41, 9.1/1.6/0.2/0.0 (BP=1.000, ratio=2.799, hyp_len=34238, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.3.57-35.69.3.42-30.54.3.17-23.81.3.09-21.96.pth, mybk
BLEU = 3.87, 22.8/5.6/2.0/0.9 (BP=1.000, ratio=1.078, hyp_len=12320, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.3.57-35.69.3.42-30.54.3.17-23.81.3.09-21.96.pth, bkmy
BLEU = 0.19, 2.6/0.6/0.1/0.0 (BP=1.000, ratio=8.847, hyp_len=108205, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.3.45-31.63.3.34-28.14.3.05-21.09.2.98-19.73.pth, mybk
BLEU = 4.57, 25.0/6.9/2.5/1.0 (BP=1.000, ratio=1.037, hyp_len=11852, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.3.45-31.63.3.34-28.14.3.05-21.09.2.98-19.73.pth, bkmy
BLEU = 0.53, 7.0/1.9/0.3/0.0 (BP=1.000, ratio=3.859, hyp_len=47203, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.3.41-30.14.3.27-26.28.3.00-20.18.2.93-18.71.pth, mybk
BLEU = 4.72, 24.0/7.2/2.6/1.1 (BP=1.000, ratio=1.074, hyp_len=12283, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.3.41-30.14.3.27-26.28.3.00-20.18.2.93-18.71.pth, bkmy
BLEU = 0.81, 7.3/2.0/0.4/0.1 (BP=1.000, ratio=4.162, hyp_len=50909, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.3.36-28.67.3.26-26.05.2.95-19.02.2.89-17.93.pth, mybk
BLEU = 4.65, 24.6/7.1/2.5/1.1 (BP=1.000, ratio=1.092, hyp_len=12486, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.3.36-28.67.3.26-26.05.2.95-19.02.2.89-17.93.pth, bkmy
BLEU = 0.94, 7.1/2.2/0.5/0.1 (BP=1.000, ratio=4.487, hyp_len=54881, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.3.27-26.25.3.15-23.23.2.91-18.42.2.83-16.92.pth, mybk
BLEU = 4.81, 25.3/7.7/2.7/1.0 (BP=1.000, ratio=1.100, hyp_len=12571, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.3.27-26.25.3.15-23.23.2.91-18.42.2.83-16.92.pth, bkmy
BLEU = 0.78, 5.5/1.8/0.5/0.1 (BP=1.000, ratio=5.843, hyp_len=71469, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.3.30-27.20.3.21-24.76.2.88-17.78.2.76-15.78.pth, mybk
BLEU = 4.82, 25.7/8.0/2.6/1.0 (BP=1.000, ratio=1.086, hyp_len=12419, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.3.30-27.20.3.21-24.76.2.88-17.78.2.76-15.78.pth, bkmy
BLEU = 1.65, 9.5/3.1/1.0/0.3 (BP=1.000, ratio=3.518, hyp_len=43030, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.3.24-25.56.3.05-21.02.2.82-16.76.2.71-15.01.pth, mybk
BLEU = 5.59, 25.6/8.8/3.3/1.3 (BP=1.000, ratio=1.134, hyp_len=12964, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.3.24-25.56.3.05-21.02.2.82-16.76.2.71-15.01.pth, bkmy
BLEU = 3.16, 16.8/5.7/1.8/0.6 (BP=1.000, ratio=2.069, hyp_len=25300, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.3.15-23.23.3.02-20.50.2.84-17.06.2.67-14.49.pth, mybk
BLEU = 5.23, 24.9/8.1/3.1/1.2 (BP=1.000, ratio=1.181, hyp_len=13502, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.3.15-23.23.3.02-20.50.2.84-17.06.2.67-14.49.pth, bkmy
BLEU = 2.13, 10.7/3.8/1.3/0.4 (BP=1.000, ratio=3.232, hyp_len=39532, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.3.25-25.66.3.03-20.59.2.79-16.24.2.67-14.43.pth, mybk
BLEU = 5.62, 26.4/9.0/3.4/1.2 (BP=1.000, ratio=1.115, hyp_len=12745, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.3.25-25.66.3.03-20.59.2.79-16.24.2.67-14.43.pth, bkmy
BLEU = 3.68, 15.9/6.0/2.2/0.9 (BP=1.000, ratio=2.280, hyp_len=27889, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.3.16-23.59.2.93-18.75.2.76-15.80.2.59-13.39.pth, mybk
BLEU = 5.46, 26.1/8.7/3.3/1.2 (BP=1.000, ratio=1.154, hyp_len=13197, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.3.16-23.59.2.93-18.75.2.76-15.80.2.59-13.39.pth, bkmy
BLEU = 2.21, 10.0/3.6/1.3/0.5 (BP=1.000, ratio=3.478, hyp_len=42542, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.3.06-21.26.2.94-18.94.2.74-15.47.2.54-12.66.pth, mybk
BLEU = 6.47, 28.8/10.0/3.9/1.6 (BP=1.000, ratio=1.062, hyp_len=12137, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.3.06-21.26.2.94-18.94.2.74-15.47.2.54-12.66.pth, bkmy
BLEU = 4.46, 18.1/7.0/2.8/1.1 (BP=1.000, ratio=2.068, hyp_len=25299, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.2.95-19.19.2.79-16.28.2.71-15.04.2.49-12.08.pth, mybk
BLEU = 6.13, 27.8/9.7/3.7/1.4 (BP=1.000, ratio=1.124, hyp_len=12847, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.2.95-19.19.2.79-16.28.2.71-15.04.2.49-12.08.pth, bkmy
BLEU = 6.08, 23.7/9.5/3.9/1.5 (BP=1.000, ratio=1.612, hyp_len=19711, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.2.95-19.17.2.83-16.99.2.67-14.49.2.49-12.02.pth, mybk
BLEU = 6.97, 29.6/10.5/4.3/1.7 (BP=1.000, ratio=1.072, hyp_len=12257, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.2.95-19.17.2.83-16.99.2.67-14.49.2.49-12.02.pth, bkmy
BLEU = 7.79, 28.3/11.7/5.0/2.2 (BP=1.000, ratio=1.365, hyp_len=16690, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.2.89-18.05.2.72-15.21.2.68-14.61.2.43-11.34.pth, mybk
BLEU = 6.53, 28.8/10.3/4.1/1.5 (BP=1.000, ratio=1.093, hyp_len=12499, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.2.89-18.05.2.72-15.21.2.68-14.61.2.43-11.34.pth, bkmy
BLEU = 2.41, 9.0/3.7/1.5/0.7 (BP=1.000, ratio=4.075, hyp_len=49839, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.2.79-16.22.2.60-13.41.2.67-14.42.2.40-11.05.pth, mybk
BLEU = 6.85, 30.1/10.4/4.2/1.7 (BP=1.000, ratio=1.070, hyp_len=12234, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.2.79-16.22.2.60-13.41.2.67-14.42.2.40-11.05.pth, bkmy
BLEU = 9.13, 32.6/13.6/5.9/2.7 (BP=1.000, ratio=1.201, hyp_len=14689, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.2.78-16.19.2.59-13.27.2.66-14.28.2.38-10.76.pth, mybk
BLEU = 6.92, 29.1/10.6/4.3/1.7 (BP=1.000, ratio=1.090, hyp_len=12464, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.2.78-16.19.2.59-13.27.2.66-14.28.2.38-10.76.pth, bkmy
BLEU = 8.48, 30.1/12.7/5.5/2.5 (BP=1.000, ratio=1.323, hyp_len=16176, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.2.76-15.83.2.56-13.00.2.65-14.21.2.36-10.60.pth, mybk
BLEU = 7.84, 31.0/11.2/4.9/2.2 (BP=1.000, ratio=1.066, hyp_len=12184, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.2.76-15.83.2.56-13.00.2.65-14.21.2.36-10.60.pth, bkmy
BLEU = 5.55, 19.7/8.3/3.6/1.6 (BP=1.000, ratio=2.054, hyp_len=25123, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.31.2.68-14.52.2.50-12.14.2.63-13.91.2.32-10.14.pth, mybk
BLEU = 7.30, 30.2/10.9/4.6/1.9 (BP=1.000, ratio=1.096, hyp_len=12530, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.31.2.68-14.52.2.50-12.14.2.63-13.91.2.32-10.14.pth, bkmy
BLEU = 7.23, 25.0/10.8/4.8/2.1 (BP=1.000, ratio=1.651, hyp_len=20198, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.32.2.70-14.89.2.52-12.46.2.61-13.57.2.32-10.17.pth, mybk
BLEU = 7.45, 30.7/10.9/4.6/2.0 (BP=1.000, ratio=1.050, hyp_len=12007, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.32.2.70-14.89.2.52-12.46.2.61-13.57.2.32-10.17.pth, bkmy
BLEU = 6.99, 23.8/10.6/4.7/2.0 (BP=1.000, ratio=1.782, hyp_len=21801, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.33.2.64-13.99.2.44-11.48.2.62-13.78.2.28-9.80.pth, mybk
BLEU = 7.69, 30.8/11.2/4.9/2.1 (BP=1.000, ratio=1.089, hyp_len=12454, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.33.2.64-13.99.2.44-11.48.2.62-13.78.2.28-9.80.pth, bkmy
BLEU = 6.24, 21.2/9.4/4.1/1.8 (BP=1.000, ratio=2.021, hyp_len=24717, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.34.2.61-13.62.2.39-10.94.2.60-13.46.2.27-9.72.pth, mybk
BLEU = 7.94, 31.5/11.8/5.0/2.1 (BP=1.000, ratio=1.077, hyp_len=12317, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.34.2.61-13.62.2.39-10.94.2.60-13.46.2.27-9.72.pth, bkmy
BLEU = 9.52, 30.8/13.9/6.5/3.0 (BP=1.000, ratio=1.399, hyp_len=17111, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.35.2.59-13.35.2.36-10.60.2.59-13.32.2.34-10.42.pth, mybk
BLEU = 8.62, 31.9/12.3/5.5/2.6 (BP=1.000, ratio=1.050, hyp_len=12006, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.35.2.59-13.35.2.36-10.60.2.59-13.32.2.34-10.42.pth, bkmy
BLEU = 6.71, 22.5/10.0/4.5/2.0 (BP=1.000, ratio=1.918, hyp_len=23460, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.36.2.53-12.60.2.29-9.89.2.58-13.22.2.20-9.02.pth, mybk
BLEU = 8.57, 32.0/12.4/5.5/2.5 (BP=1.000, ratio=1.093, hyp_len=12500, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.36.2.53-12.60.2.29-9.89.2.58-13.22.2.20-9.02.pth, bkmy
BLEU = 10.74, 33.4/15.6/7.4/3.5 (BP=1.000, ratio=1.330, hyp_len=16271, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.37.2.49-12.08.2.27-9.70.2.59-13.34.2.19-8.97.pth, mybk
BLEU = 8.14, 30.6/11.6/5.2/2.4 (BP=1.000, ratio=1.129, hyp_len=12904, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.37.2.49-12.08.2.27-9.70.2.59-13.34.2.19-8.97.pth, bkmy
BLEU = 12.76, 39.0/18.4/8.8/4.2 (BP=1.000, ratio=1.126, hyp_len=13766, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.38.2.50-12.21.2.27-9.64.2.59-13.36.2.19-8.98.pth, mybk
BLEU = 8.70, 32.5/12.3/5.5/2.6 (BP=1.000, ratio=1.075, hyp_len=12285, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.38.2.50-12.21.2.27-9.64.2.59-13.36.2.19-8.98.pth, bkmy
BLEU = 11.52, 35.6/16.7/7.9/3.8 (BP=1.000, ratio=1.252, hyp_len=15319, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.39.2.43-11.34.2.20-9.01.2.58-13.24.2.19-8.92.pth, mybk
BLEU = 8.57, 32.4/12.4/5.5/2.4 (BP=1.000, ratio=1.084, hyp_len=12390, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.39.2.43-11.34.2.20-9.01.2.58-13.24.2.19-8.92.pth, bkmy
BLEU = 12.19, 36.8/17.6/8.3/4.1 (BP=1.000, ratio=1.208, hyp_len=14777, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.40.2.44-11.48.2.20-9.03.2.60-13.50.2.18-8.85.pth, mybk
BLEU = 9.33, 33.1/13.1/6.0/2.9 (BP=1.000, ratio=1.075, hyp_len=12286, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.40.2.44-11.48.2.20-9.03.2.60-13.50.2.18-8.85.pth, bkmy
BLEU = 10.89, 34.0/16.0/7.4/3.5 (BP=1.000, ratio=1.314, hyp_len=16072, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.41.2.37-10.74.2.12-8.32.2.56-12.97.2.15-8.60.pth, mybk
BLEU = 9.56, 34.0/13.5/6.2/2.9 (BP=1.000, ratio=1.061, hyp_len=12127, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.41.2.37-10.74.2.12-8.32.2.56-12.97.2.15-8.60.pth, bkmy
BLEU = 14.40, 41.2/20.1/10.1/5.1 (BP=1.000, ratio=1.103, hyp_len=13488, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.42.2.33-10.28.2.11-8.23.2.57-13.08.2.14-8.48.pth, mybk
BLEU = 9.66, 33.6/13.4/6.3/3.1 (BP=1.000, ratio=1.081, hyp_len=12362, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.42.2.33-10.28.2.11-8.23.2.57-13.08.2.14-8.48.pth, bkmy
BLEU = 12.04, 35.9/17.3/8.3/4.1 (BP=1.000, ratio=1.276, hyp_len=15603, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.43.2.34-10.42.2.12-8.36.2.60-13.50.2.16-8.63.pth, mybk
BLEU = 9.10, 32.6/12.7/5.9/2.8 (BP=1.000, ratio=1.112, hyp_len=12715, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.43.2.34-10.42.2.12-8.36.2.60-13.50.2.16-8.63.pth, bkmy
BLEU = 11.70, 34.4/16.5/8.0/4.1 (BP=1.000, ratio=1.315, hyp_len=16085, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.44.2.31-10.11.2.04-7.73.2.57-13.07.2.08-8.01.pth, mybk
BLEU = 9.39, 33.2/13.2/6.2/2.9 (BP=1.000, ratio=1.098, hyp_len=12550, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.44.2.31-10.11.2.04-7.73.2.57-13.07.2.08-8.01.pth, bkmy
BLEU = 15.14, 42.2/20.7/10.6/5.7 (BP=1.000, ratio=1.092, hyp_len=13357, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.45.2.27-9.65.2.05-7.80.2.61-13.54.2.12-8.30.pth, mybk
BLEU = 9.27, 32.9/13.0/6.1/2.9 (BP=1.000, ratio=1.103, hyp_len=12610, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.45.2.27-9.65.2.05-7.80.2.61-13.54.2.12-8.30.pth, bkmy
BLEU = 15.15, 43.1/21.1/10.6/5.5 (BP=1.000, ratio=1.079, hyp_len=13202, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.46.2.25-9.53.2.01-7.45.2.58-13.26.2.07-7.92.pth, mybk
BLEU = 10.06, 34.3/13.6/6.5/3.3 (BP=1.000, ratio=1.077, hyp_len=12312, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.46.2.25-9.53.2.01-7.45.2.58-13.26.2.07-7.92.pth, bkmy
BLEU = 15.92, 44.5/21.9/11.2/5.9 (BP=1.000, ratio=1.055, hyp_len=12899, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.47.2.24-9.37.1.96-7.12.2.59-13.37.2.08-8.00.pth, mybk
BLEU = 9.78, 34.1/13.5/6.3/3.1 (BP=1.000, ratio=1.067, hyp_len=12202, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.47.2.24-9.37.1.96-7.12.2.59-13.37.2.08-8.00.pth, bkmy
BLEU = 14.39, 39.1/19.7/10.2/5.5 (BP=1.000, ratio=1.227, hyp_len=15010, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.48.2.24-9.35.1.97-7.17.2.59-13.28.2.05-7.76.pth, mybk
BLEU = 9.90, 34.0/13.7/6.5/3.2 (BP=1.000, ratio=1.103, hyp_len=12615, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.48.2.24-9.35.1.97-7.17.2.59-13.28.2.05-7.76.pth, bkmy
BLEU = 15.59, 41.5/21.0/11.1/6.1 (BP=1.000, ratio=1.163, hyp_len=14223, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.49.2.16-8.71.1.89-6.60.2.58-13.17.2.05-7.75.pth, mybk
BLEU = 10.01, 34.4/14.0/6.6/3.2 (BP=1.000, ratio=1.079, hyp_len=12331, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.49.2.16-8.71.1.89-6.60.2.58-13.17.2.05-7.75.pth, bkmy
BLEU = 16.36, 44.4/22.2/11.6/6.3 (BP=1.000, ratio=1.062, hyp_len=12992, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.50.2.21-9.08.1.93-6.87.2.62-13.68.2.03-7.60.pth, mybk
BLEU = 10.08, 34.4/14.0/6.6/3.3 (BP=1.000, ratio=1.092, hyp_len=12486, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.50.2.21-9.08.1.93-6.87.2.62-13.68.2.03-7.60.pth, bkmy
BLEU = 17.42, 45.1/23.1/12.5/7.1 (BP=1.000, ratio=1.069, hyp_len=13081, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.51.2.11-8.22.1.81-6.09.2.61-13.62.2.04-7.65.pth, mybk
BLEU = 10.59, 35.4/14.7/7.0/3.5 (BP=1.000, ratio=1.055, hyp_len=12059, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.51.2.11-8.22.1.81-6.09.2.61-13.62.2.04-7.65.pth, bkmy
BLEU = 16.04, 42.5/21.6/11.4/6.3 (BP=1.000, ratio=1.107, hyp_len=13545, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.52.2.11-8.28.1.81-6.10.2.63-13.83.2.02-7.55.pth, mybk
BLEU = 9.89, 33.8/13.6/6.4/3.2 (BP=1.000, ratio=1.096, hyp_len=12534, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.52.2.11-8.28.1.81-6.10.2.63-13.83.2.02-7.55.pth, bkmy
BLEU = 17.32, 45.2/23.2/12.4/6.9 (BP=1.000, ratio=1.084, hyp_len=13258, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.53.2.08-7.99.1.79-5.98.2.62-13.74.2.03-7.63.pth, mybk
BLEU = 9.75, 34.6/13.9/6.4/2.9 (BP=1.000, ratio=1.091, hyp_len=12471, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.53.2.08-7.99.1.79-5.98.2.62-13.74.2.03-7.63.pth, bkmy
BLEU = 16.72, 43.9/22.6/11.9/6.6 (BP=1.000, ratio=1.109, hyp_len=13569, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.54.2.05-7.77.1.76-5.79.2.59-13.36.2.01-7.50.pth, mybk
BLEU = 9.85, 34.1/13.5/6.4/3.2 (BP=1.000, ratio=1.093, hyp_len=12500, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.54.2.05-7.77.1.76-5.79.2.59-13.36.2.01-7.50.pth, bkmy
BLEU = 16.17, 43.2/21.9/11.4/6.3 (BP=1.000, ratio=1.127, hyp_len=13785, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.55.2.06-7.82.1.79-6.01.2.63-13.86.1.99-7.29.pth, mybk
BLEU = 10.01, 34.7/14.1/6.5/3.2 (BP=1.000, ratio=1.092, hyp_len=12483, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.55.2.06-7.82.1.79-6.01.2.63-13.86.1.99-7.29.pth, bkmy
BLEU = 17.48, 45.0/23.2/12.6/7.1 (BP=1.000, ratio=1.083, hyp_len=13246, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.56.2.03-7.65.1.76-5.82.2.61-13.59.1.99-7.32.pth, mybk
BLEU = 10.54, 35.8/14.7/6.9/3.4 (BP=1.000, ratio=1.070, hyp_len=12236, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.56.2.03-7.65.1.76-5.82.2.61-13.59.1.99-7.32.pth, bkmy
BLEU = 17.31, 43.4/22.7/12.5/7.3 (BP=1.000, ratio=1.150, hyp_len=14069, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.57.1.95-7.03.1.69-5.41.2.62-13.77.1.97-7.18.pth, mybk
BLEU = 10.22, 34.6/14.1/6.6/3.4 (BP=1.000, ratio=1.089, hyp_len=12454, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.57.1.95-7.03.1.69-5.41.2.62-13.77.1.97-7.18.pth, bkmy
BLEU = 18.92, 46.9/24.8/13.8/8.0 (BP=1.000, ratio=1.061, hyp_len=12980, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.58.2.01-7.45.1.68-5.39.2.61-13.65.1.99-7.33.pth, mybk
BLEU = 9.91, 35.1/14.3/6.5/3.0 (BP=1.000, ratio=1.088, hyp_len=12434, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.58.2.01-7.45.1.68-5.39.2.61-13.65.1.99-7.33.pth, bkmy
BLEU = 18.76, 46.4/24.9/13.7/7.8 (BP=1.000, ratio=1.100, hyp_len=13451, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.59.1.98-7.24.1.76-5.84.2.65-14.13.1.99-7.28.pth, mybk
BLEU = 9.98, 34.7/14.1/6.5/3.1 (BP=1.000, ratio=1.105, hyp_len=12628, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.59.1.98-7.24.1.76-5.84.2.65-14.13.1.99-7.28.pth, bkmy
BLEU = 17.90, 44.5/23.6/12.9/7.6 (BP=1.000, ratio=1.113, hyp_len=13611, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.60.1.95-7.01.1.64-5.17.2.66-14.32.1.96-7.09.pth, mybk
BLEU = 10.35, 34.4/14.3/6.8/3.5 (BP=1.000, ratio=1.078, hyp_len=12326, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.60.1.95-7.01.1.64-5.17.2.66-14.32.1.96-7.09.pth, bkmy
BLEU = 18.31, 46.0/24.0/13.2/7.7 (BP=1.000, ratio=1.075, hyp_len=13145, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.61.2.00-7.41.1.72-5.58.2.65-14.11.1.98-7.23.pth, mybk
BLEU = 10.29, 35.2/14.2/6.7/3.4 (BP=1.000, ratio=1.084, hyp_len=12397, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.61.2.00-7.41.1.72-5.58.2.65-14.11.1.98-7.23.pth, bkmy
BLEU = 18.89, 46.7/24.7/13.8/8.0 (BP=1.000, ratio=1.077, hyp_len=13178, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.62.1.88-6.58.1.60-4.94.2.65-14.09.1.96-7.09.pth, mybk
BLEU = 10.41, 34.8/14.3/6.9/3.4 (BP=1.000, ratio=1.080, hyp_len=12352, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.62.1.88-6.58.1.60-4.94.2.65-14.09.1.96-7.09.pth, bkmy
BLEU = 19.21, 47.4/25.2/14.0/8.1 (BP=1.000, ratio=1.061, hyp_len=12982, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.63.1.91-6.74.1.66-5.26.2.63-13.91.1.94-6.94.pth, mybk
BLEU = 10.35, 35.8/14.6/6.8/3.2 (BP=1.000, ratio=1.074, hyp_len=12273, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.63.1.91-6.74.1.66-5.26.2.63-13.91.1.94-6.94.pth, bkmy
BLEU = 18.93, 47.0/24.8/13.8/8.0 (BP=1.000, ratio=1.069, hyp_len=13070, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.64.1.85-6.35.1.54-4.66.2.66-14.27.1.91-6.74.pth, mybk
BLEU = 10.20, 35.2/14.1/6.6/3.3 (BP=1.000, ratio=1.092, hyp_len=12486, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.64.1.85-6.35.1.54-4.66.2.66-14.27.1.91-6.74.pth, bkmy
BLEU = 20.39, 48.2/26.1/15.0/9.1 (BP=1.000, ratio=1.056, hyp_len=12916, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.65.1.85-6.37.1.56-4.76.2.67-14.38.1.93-6.88.pth, mybk
BLEU = 10.17, 35.0/14.2/6.7/3.2 (BP=1.000, ratio=1.080, hyp_len=12351, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.65.1.85-6.37.1.56-4.76.2.67-14.38.1.93-6.88.pth, bkmy
BLEU = 19.41, 47.5/25.1/14.1/8.4 (BP=1.000, ratio=1.049, hyp_len=12829, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.66.1.90-6.72.1.64-5.18.2.68-14.60.1.93-6.91.pth, mybk
BLEU = 10.52, 35.7/14.5/6.9/3.4 (BP=1.000, ratio=1.080, hyp_len=12345, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.66.1.90-6.72.1.64-5.18.2.68-14.60.1.93-6.91.pth, bkmy
BLEU = 19.62, 48.2/26.0/14.3/8.3 (BP=1.000, ratio=1.066, hyp_len=13035, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.67.1.81-6.13.1.51-4.53.2.69-14.67.1.93-6.86.pth, mybk
BLEU = 10.66, 35.1/14.6/7.0/3.6 (BP=1.000, ratio=1.103, hyp_len=12614, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.67.1.81-6.13.1.51-4.53.2.69-14.67.1.93-6.86.pth, bkmy
BLEU = 20.30, 48.3/26.2/14.9/9.0 (BP=1.000, ratio=1.059, hyp_len=12954, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.68.1.78-5.96.1.52-4.58.2.68-14.61.1.95-6.99.pth, mybk
BLEU = 10.71, 36.1/14.9/7.0/3.5 (BP=1.000, ratio=1.069, hyp_len=12216, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.68.1.78-5.96.1.52-4.58.2.68-14.61.1.95-6.99.pth, bkmy
BLEU = 20.06, 48.4/26.0/14.6/8.8 (BP=1.000, ratio=1.064, hyp_len=13011, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.69.1.85-6.34.1.57-4.80.2.70-14.94.1.91-6.79.pth, mybk
BLEU = 10.74, 35.1/14.5/7.1/3.7 (BP=1.000, ratio=1.094, hyp_len=12501, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.69.1.85-6.34.1.57-4.80.2.70-14.94.1.91-6.79.pth, bkmy
BLEU = 20.30, 48.3/26.4/14.8/9.0 (BP=1.000, ratio=1.067, hyp_len=13055, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.70.1.79-6.01.1.54-4.69.2.71-14.98.1.93-6.86.pth, mybk
BLEU = 10.21, 34.8/14.3/6.6/3.3 (BP=1.000, ratio=1.099, hyp_len=12559, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.70.1.79-6.01.1.54-4.69.2.71-14.98.1.93-6.86.pth, bkmy
BLEU = 19.92, 47.8/25.9/14.6/8.7 (BP=1.000, ratio=1.077, hyp_len=13167, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.71.1.73-5.61.1.48-4.38.2.69-14.77.1.93-6.88.pth, mybk
BLEU = 11.08, 36.1/15.1/7.4/3.7 (BP=1.000, ratio=1.079, hyp_len=12339, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.71.1.73-5.61.1.48-4.38.2.69-14.77.1.93-6.88.pth, bkmy
BLEU = 20.23, 48.5/26.4/14.8/8.8 (BP=1.000, ratio=1.065, hyp_len=13028, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.72.1.70-5.49.1.42-4.13.2.70-14.92.1.94-6.97.pth, mybk
BLEU = 10.82, 36.1/14.8/7.1/3.6 (BP=1.000, ratio=1.066, hyp_len=12189, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.72.1.70-5.49.1.42-4.13.2.70-14.92.1.94-6.97.pth, bkmy
BLEU = 19.72, 47.2/25.2/14.5/8.8 (BP=1.000, ratio=1.089, hyp_len=13322, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.73.1.72-5.57.1.42-4.15.2.73-15.29.1.91-6.74.pth, mybk
BLEU = 10.83, 35.5/14.6/7.1/3.7 (BP=1.000, ratio=1.089, hyp_len=12448, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.73.1.72-5.57.1.42-4.15.2.73-15.29.1.91-6.74.pth, bkmy
BLEU = 20.22, 48.4/26.2/14.9/8.8 (BP=1.000, ratio=1.072, hyp_len=13116, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.74.1.74-5.72.1.47-4.36.2.73-15.39.1.94-6.94.pth, mybk
BLEU = 11.09, 35.6/14.9/7.3/3.9 (BP=1.000, ratio=1.094, hyp_len=12511, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.74.1.74-5.72.1.47-4.36.2.73-15.39.1.94-6.94.pth, bkmy
BLEU = 21.00, 48.4/26.7/15.6/9.7 (BP=1.000, ratio=1.070, hyp_len=13089, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.75.1.66-5.23.1.33-3.80.2.73-15.34.1.93-6.88.pth, mybk
BLEU = 11.12, 35.8/15.0/7.4/3.9 (BP=1.000, ratio=1.089, hyp_len=12450, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.75.1.66-5.23.1.33-3.80.2.73-15.34.1.93-6.88.pth, bkmy
BLEU = 19.75, 47.6/25.7/14.4/8.6 (BP=1.000, ratio=1.078, hyp_len=13191, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.76.1.61-5.02.1.33-3.79.2.73-15.40.1.92-6.81.pth, mybk
BLEU = 10.84, 35.5/14.7/7.2/3.7 (BP=1.000, ratio=1.076, hyp_len=12304, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.76.1.61-5.02.1.33-3.79.2.73-15.40.1.92-6.81.pth, bkmy
BLEU = 21.00, 48.4/26.8/15.6/9.6 (BP=1.000, ratio=1.079, hyp_len=13199, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.77.1.62-5.05.1.30-3.69.2.75-15.58.1.90-6.71.pth, mybk
BLEU = 11.17, 36.0/14.9/7.4/3.9 (BP=1.000, ratio=1.084, hyp_len=12387, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.77.1.62-5.05.1.30-3.69.2.75-15.58.1.90-6.71.pth, bkmy
BLEU = 21.48, 48.7/27.2/16.0/10.1 (BP=1.000, ratio=1.080, hyp_len=13204, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.78.1.60-4.97.1.32-3.73.2.77-15.94.1.93-6.92.pth, mybk
BLEU = 10.93, 36.1/14.8/7.2/3.7 (BP=1.000, ratio=1.079, hyp_len=12338, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.78.1.60-4.97.1.32-3.73.2.77-15.94.1.93-6.92.pth, bkmy
BLEU = 20.11, 47.6/26.1/14.8/8.9 (BP=1.000, ratio=1.103, hyp_len=13491, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.79.1.62-5.05.1.37-3.92.2.73-15.38.1.90-6.66.pth, mybk
BLEU = 10.85, 35.9/14.8/7.1/3.7 (BP=1.000, ratio=1.087, hyp_len=12429, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.79.1.62-5.05.1.37-3.92.2.73-15.38.1.90-6.66.pth, bkmy
BLEU = 21.25, 49.5/27.3/15.7/9.6 (BP=1.000, ratio=1.054, hyp_len=12890, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.80.1.65-5.19.1.32-3.75.2.74-15.52.1.91-6.78.pth, mybk
BLEU = 11.18, 36.0/15.0/7.4/3.9 (BP=1.000, ratio=1.075, hyp_len=12292, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.80.1.65-5.19.1.32-3.75.2.74-15.52.1.91-6.78.pth, bkmy
BLEU = 20.91, 48.6/26.9/15.4/9.5 (BP=1.000, ratio=1.060, hyp_len=12970, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.81.1.62-5.05.1.37-3.94.2.77-16.02.1.95-7.01.pth, mybk
BLEU = 11.10, 36.6/15.2/7.2/3.8 (BP=1.000, ratio=1.069, hyp_len=12216, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.81.1.62-5.05.1.37-3.94.2.77-16.02.1.95-7.01.pth, bkmy
BLEU = 20.95, 48.5/26.9/15.6/9.5 (BP=1.000, ratio=1.079, hyp_len=13199, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.82.1.60-4.94.1.30-3.68.2.79-16.21.1.92-6.81.pth, mybk
BLEU = 10.60, 35.7/14.4/6.9/3.6 (BP=1.000, ratio=1.095, hyp_len=12513, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.82.1.60-4.94.1.30-3.68.2.79-16.21.1.92-6.81.pth, bkmy
BLEU = 21.14, 48.6/26.9/15.7/9.7 (BP=1.000, ratio=1.084, hyp_len=13253, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.83.1.52-4.58.1.23-3.41.2.77-15.91.1.92-6.85.pth, mybk
BLEU = 10.76, 35.9/14.6/7.1/3.6 (BP=1.000, ratio=1.097, hyp_len=12539, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.83.1.52-4.58.1.23-3.41.2.77-15.91.1.92-6.85.pth, bkmy
BLEU = 21.89, 49.7/27.8/16.3/10.2 (BP=1.000, ratio=1.059, hyp_len=12953, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.84.1.57-4.80.1.26-3.51.2.79-16.20.1.91-6.76.pth, mybk
BLEU = 10.96, 35.9/14.8/7.2/3.8 (BP=1.000, ratio=1.090, hyp_len=12465, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.84.1.57-4.80.1.26-3.51.2.79-16.20.1.91-6.76.pth, bkmy
BLEU = 21.17, 48.3/27.0/15.8/9.8 (BP=1.000, ratio=1.090, hyp_len=13328, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.85.1.51-4.53.1.21-3.37.2.80-16.37.1.92-6.85.pth, mybk
BLEU = 10.92, 36.4/14.7/7.2/3.7 (BP=1.000, ratio=1.052, hyp_len=12029, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.85.1.51-4.53.1.21-3.37.2.80-16.37.1.92-6.85.pth, bkmy
BLEU = 21.27, 48.8/27.2/15.8/9.7 (BP=1.000, ratio=1.084, hyp_len=13257, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.86.1.51-4.54.1.25-3.48.2.81-16.67.1.97-7.20.pth, mybk
BLEU = 10.84, 35.6/14.6/7.1/3.7 (BP=1.000, ratio=1.080, hyp_len=12350, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.86.1.51-4.54.1.25-3.48.2.81-16.67.1.97-7.20.pth, bkmy
BLEU = 20.96, 48.7/26.8/15.6/9.5 (BP=1.000, ratio=1.076, hyp_len=13155, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.87.1.55-4.70.1.28-3.59.2.81-16.65.1.92-6.81.pth, mybk
BLEU = 10.87, 35.9/14.7/7.1/3.7 (BP=1.000, ratio=1.091, hyp_len=12470, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.87.1.55-4.70.1.28-3.59.2.81-16.65.1.92-6.81.pth, bkmy
BLEU = 21.89, 49.7/27.8/16.4/10.1 (BP=1.000, ratio=1.049, hyp_len=12826, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.88.1.47-4.35.1.16-3.20.2.81-16.64.1.92-6.83.pth, mybk
BLEU = 10.58, 35.0/14.3/7.0/3.6 (BP=1.000, ratio=1.099, hyp_len=12564, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.88.1.47-4.35.1.16-3.20.2.81-16.64.1.92-6.83.pth, bkmy
BLEU = 21.28, 49.2/27.2/15.7/9.8 (BP=1.000, ratio=1.058, hyp_len=12935, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.89.1.55-4.69.1.20-3.32.2.84-17.10.1.95-7.01.pth, mybk
BLEU = 10.85, 35.8/15.0/7.2/3.6 (BP=1.000, ratio=1.094, hyp_len=12512, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.89.1.55-4.69.1.20-3.32.2.84-17.10.1.95-7.01.pth, bkmy
BLEU = 21.71, 48.9/27.5/16.2/10.2 (BP=1.000, ratio=1.091, hyp_len=13340, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.90.1.48-4.39.1.22-3.40.2.81-16.66.1.96-7.07.pth, mybk
BLEU = 10.98, 36.1/14.8/7.3/3.7 (BP=1.000, ratio=1.087, hyp_len=12432, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.90.1.48-4.39.1.22-3.40.2.81-16.66.1.96-7.07.pth, bkmy
BLEU = 21.20, 48.6/26.9/15.8/9.8 (BP=1.000, ratio=1.086, hyp_len=13283, ref_len=12231)
```

Best BLEU Score for my-bk, 80 epoch: 11.18  
Best BLEU Score for bk-my, 83 epoch and 87 epoch: 21.89  


## Seq2Seq-DSL, my-bk, 100epoch

training

```
Epoch 1 - |param|=8.50e+02 |g_param|=5.00e+05 loss_x2y=4.8929e+00 ppl_x2y=133.35 loss_y2x=4.6950e+00 ppl_y2x=109.40 dual_loss=0.0000e+00
Validation X2Y - loss=4.0962e+00 ppl=60.11 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=3.9118e+00 ppl=49.99 best_loss=inf best_ppl=inf
Epoch 2 - |param|=8.50e+02 |g_param|=3.42e+05 loss_x2y=4.4284e+00 ppl_x2y=83.79 loss_y2x=4.2252e+00 ppl_y2x=68.39 dual_loss=0.0000e+00
Validation X2Y - loss=3.9043e+00 ppl=49.61 best_loss=4.0962e+00 best_ppl=60.11                                          
Validation Y2X - loss=3.8237e+00 ppl=45.77 best_loss=3.9118e+00 best_ppl=49.99
Epoch 3 - |param|=8.50e+02 |g_param|=3.14e+05 loss_x2y=4.3699e+00 ppl_x2y=79.04 loss_y2x=4.1557e+00 ppl_y2x=63.80 dual_loss=0.0000e+00
Validation X2Y - loss=3.8773e+00 ppl=48.29 best_loss=3.9043e+00 best_ppl=49.61                                          
Validation Y2X - loss=3.8044e+00 ppl=44.90 best_loss=3.8237e+00 best_ppl=45.77
Epoch 4 - |param|=8.50e+02 |g_param|=3.24e+05 loss_x2y=4.3575e+00 ppl_x2y=78.06 loss_y2x=4.1410e+00 ppl_y2x=62.86 dual_loss=0.0000e+00
Validation X2Y - loss=3.8467e+00 ppl=46.84 best_loss=3.8773e+00 best_ppl=48.29                                          
Validation Y2X - loss=3.7404e+00 ppl=42.11 best_loss=3.8044e+00 best_ppl=44.90
Epoch 5 - |param|=8.51e+02 |g_param|=2.90e+05 loss_x2y=4.3159e+00 ppl_x2y=74.88 loss_y2x=4.0796e+00 ppl_y2x=59.12 dual_loss=0.0000e+00
Validation X2Y - loss=3.8396e+00 ppl=46.51 best_loss=3.8467e+00 best_ppl=46.84                                          
Validation Y2X - loss=3.6740e+00 ppl=39.41 best_loss=3.7404e+00 best_ppl=42.11
Epoch 6 - |param|=8.51e+02 |g_param|=3.18e+05 loss_x2y=4.3051e+00 ppl_x2y=74.07 loss_y2x=4.0858e+00 ppl_y2x=59.49 dual_loss=0.0000e+00
Validation X2Y - loss=3.8203e+00 ppl=45.62 best_loss=3.8396e+00 best_ppl=46.51                                          
Validation Y2X - loss=3.6872e+00 ppl=39.93 best_loss=3.6740e+00 best_ppl=39.41
Epoch 7 - |param|=8.51e+02 |g_param|=3.22e+05 loss_x2y=4.3918e+00 ppl_x2y=80.79 loss_y2x=4.1137e+00 ppl_y2x=61.18 dual_loss=0.0000e+00
Validation X2Y - loss=3.7699e+00 ppl=43.37 best_loss=3.8203e+00 best_ppl=45.62                                          
Validation Y2X - loss=3.6521e+00 ppl=38.56 best_loss=3.6740e+00 best_ppl=39.41
Epoch 8 - |param|=8.52e+02 |g_param|=2.57e+05 loss_x2y=4.3581e+00 ppl_x2y=78.11 loss_y2x=4.1172e+00 ppl_y2x=61.39 dual_loss=0.0000e+00
Validation X2Y - loss=3.7698e+00 ppl=43.37 best_loss=3.7699e+00 best_ppl=43.37                                          
Validation Y2X - loss=3.6144e+00 ppl=37.13 best_loss=3.6521e+00 best_ppl=38.56
Epoch 9 - |param|=8.52e+02 |g_param|=2.30e+05 loss_x2y=4.3124e+00 ppl_x2y=74.62 loss_y2x=4.0896e+00 ppl_y2x=59.71 dual_loss=0.0000e+00
Validation X2Y - loss=3.8072e+00 ppl=45.02 best_loss=3.7698e+00 best_ppl=43.37                                          
Validation Y2X - loss=3.5575e+00 ppl=35.07 best_loss=3.6144e+00 best_ppl=37.13
Epoch 10 - |param|=8.53e+02 |g_param|=2.13e+05 loss_x2y=4.1226e+00 ppl_x2y=61.72 loss_y2x=3.8816e+00 ppl_y2x=48.50 dual_loss=0.0000e+00
Validation X2Y - loss=3.6034e+00 ppl=36.72 best_loss=3.7698e+00 best_ppl=43.37                                          
Validation Y2X - loss=3.4204e+00 ppl=30.58 best_loss=3.5575e+00 best_ppl=35.07
Epoch 11 - |param|=8.53e+02 |g_param|=1.84e+05 loss_x2y=4.0662e+00 ppl_x2y=58.33 loss_y2x=3.7641e+00 ppl_y2x=43.13 dual_loss=0.0000e+00
Validation X2Y - loss=3.4631e+00 ppl=31.92 best_loss=3.6034e+00 best_ppl=36.72                                          
Validation Y2X - loss=3.2979e+00 ppl=27.06 best_loss=3.4204e+00 best_ppl=30.58
Epoch 12 - |param|=8.54e+02 |g_param|=1.69e+05 loss_x2y=3.9047e+00 ppl_x2y=49.64 loss_y2x=3.6121e+00 ppl_y2x=37.05 dual_loss=0.0000e+00
Validation X2Y - loss=3.3978e+00 ppl=29.90 best_loss=3.4631e+00 best_ppl=31.92                                          
Validation Y2X - loss=3.2101e+00 ppl=24.78 best_loss=3.2979e+00 best_ppl=27.06
Epoch 13 - |param|=8.54e+02 |g_param|=1.61e+05 loss_x2y=3.8076e+00 ppl_x2y=45.04 loss_y2x=3.5083e+00 ppl_y2x=33.39 dual_loss=0.0000e+00
Validation X2Y - loss=3.3268e+00 ppl=27.85 best_loss=3.3978e+00 best_ppl=29.90                                          
Validation Y2X - loss=3.1267e+00 ppl=22.80 best_loss=3.2101e+00 best_ppl=24.78
Epoch 14 - |param|=8.55e+02 |g_param|=1.62e+05 loss_x2y=3.7877e+00 ppl_x2y=44.16 loss_y2x=3.4899e+00 ppl_y2x=32.78 dual_loss=0.0000e+00
Validation X2Y - loss=3.2781e+00 ppl=26.52 best_loss=3.3268e+00 best_ppl=27.85                                          
Validation Y2X - loss=3.0345e+00 ppl=20.79 best_loss=3.1267e+00 best_ppl=22.80
Epoch 15 - |param|=8.55e+02 |g_param|=1.50e+05 loss_x2y=3.6309e+00 ppl_x2y=37.75 loss_y2x=3.3052e+00 ppl_y2x=27.25 dual_loss=0.0000e+00
Validation X2Y - loss=3.2483e+00 ppl=25.75 best_loss=3.2781e+00 best_ppl=26.52                                          
Validation Y2X - loss=2.9989e+00 ppl=20.06 best_loss=3.0345e+00 best_ppl=20.79
Epoch 16 - |param|=8.56e+02 |g_param|=1.64e+05 loss_x2y=3.6249e+00 ppl_x2y=37.52 loss_y2x=3.3086e+00 ppl_y2x=27.35 dual_loss=0.0000e+00
Validation X2Y - loss=3.2291e+00 ppl=25.26 best_loss=3.2483e+00 best_ppl=25.75                                          
Validation Y2X - loss=2.9642e+00 ppl=19.38 best_loss=2.9989e+00 best_ppl=20.06
Epoch 17 - |param|=8.57e+02 |g_param|=1.61e+05 loss_x2y=3.5851e+00 ppl_x2y=36.06 loss_y2x=3.2583e+00 ppl_y2x=26.00 dual_loss=0.0000e+00
Validation X2Y - loss=3.2034e+00 ppl=24.62 best_loss=3.2291e+00 best_ppl=25.26                                          
Validation Y2X - loss=2.9283e+00 ppl=18.70 best_loss=2.9642e+00 best_ppl=19.38
Epoch 18 - |param|=8.57e+02 |g_param|=1.61e+05 loss_x2y=3.5290e+00 ppl_x2y=34.09 loss_y2x=3.2011e+00 ppl_y2x=24.56 dual_loss=0.0000e+00
Validation X2Y - loss=3.1463e+00 ppl=23.25 best_loss=3.2034e+00 best_ppl=24.62                                          
Validation Y2X - loss=2.9015e+00 ppl=18.20 best_loss=2.9283e+00 best_ppl=18.70
Epoch 19 - |param|=8.58e+02 |g_param|=1.72e+05 loss_x2y=3.4663e+00 ppl_x2y=32.02 loss_y2x=3.1479e+00 ppl_y2x=23.29 dual_loss=0.0000e+00
Validation X2Y - loss=3.1139e+00 ppl=22.51 best_loss=3.1463e+00 best_ppl=23.25                                          
Validation Y2X - loss=2.8392e+00 ppl=17.10 best_loss=2.9015e+00 best_ppl=18.20
Epoch 20 - |param|=8.59e+02 |g_param|=1.78e+05 loss_x2y=3.4208e+00 ppl_x2y=30.60 loss_y2x=3.0760e+00 ppl_y2x=21.67 dual_loss=0.0000e+00
Validation X2Y - loss=3.0498e+00 ppl=21.11 best_loss=3.1139e+00 best_ppl=22.51                                          
Validation Y2X - loss=2.8408e+00 ppl=17.13 best_loss=2.8392e+00 best_ppl=17.10
Epoch 21 - |param|=8.59e+02 |g_param|=1.65e+05 loss_x2y=3.4352e+00 ppl_x2y=31.04 loss_y2x=3.0814e+00 ppl_y2x=21.79 dual_loss=7.3057e-01
Validation X2Y - loss=3.0355e+00 ppl=20.81 best_loss=3.0498e+00 best_ppl=21.11                                          
Validation Y2X - loss=2.8148e+00 ppl=16.69 best_loss=2.8392e+00 best_ppl=17.10
Epoch 22 - |param|=8.60e+02 |g_param|=1.82e+05 loss_x2y=3.3385e+00 ppl_x2y=28.18 loss_y2x=3.0416e+00 ppl_y2x=20.94 dual_loss=5.8184e-01
Validation X2Y - loss=2.9720e+00 ppl=19.53 best_loss=3.0355e+00 best_ppl=20.81                                          
Validation Y2X - loss=2.7922e+00 ppl=16.32 best_loss=2.8148e+00 best_ppl=16.69
Epoch 23 - |param|=8.61e+02 |g_param|=1.67e+05 loss_x2y=3.2691e+00 ppl_x2y=26.29 loss_y2x=2.9649e+00 ppl_y2x=19.39 dual_loss=5.2743e-01
Validation X2Y - loss=2.9928e+00 ppl=19.94 best_loss=2.9720e+00 best_ppl=19.53                                          
Validation Y2X - loss=2.7399e+00 ppl=15.49 best_loss=2.7922e+00 best_ppl=16.32
Epoch 24 - |param|=8.62e+02 |g_param|=1.75e+05 loss_x2y=3.2294e+00 ppl_x2y=25.26 loss_y2x=2.9077e+00 ppl_y2x=18.31 dual_loss=5.1545e-01
Validation X2Y - loss=2.9283e+00 ppl=18.70 best_loss=2.9720e+00 best_ppl=19.53                                          
Validation Y2X - loss=2.7252e+00 ppl=15.26 best_loss=2.7399e+00 best_ppl=15.49
Epoch 25 - |param|=8.62e+02 |g_param|=1.79e+05 loss_x2y=3.3173e+00 ppl_x2y=27.58 loss_y2x=3.0280e+00 ppl_y2x=20.66 dual_loss=6.4024e-01
Validation X2Y - loss=2.8962e+00 ppl=18.10 best_loss=2.9283e+00 best_ppl=18.70                                          
Validation Y2X - loss=2.7059e+00 ppl=14.97 best_loss=2.7252e+00 best_ppl=15.26
Epoch 26 - |param|=8.63e+02 |g_param|=1.77e+05 loss_x2y=3.1325e+00 ppl_x2y=22.93 loss_y2x=2.8499e+00 ppl_y2x=17.29 dual_loss=4.7011e-01
Validation X2Y - loss=2.8575e+00 ppl=17.42 best_loss=2.8962e+00 best_ppl=18.10                                          
Validation Y2X - loss=2.6781e+00 ppl=14.56 best_loss=2.7059e+00 best_ppl=14.97
Epoch 27 - |param|=8.64e+02 |g_param|=1.70e+05 loss_x2y=3.1506e+00 ppl_x2y=23.35 loss_y2x=2.8483e+00 ppl_y2x=17.26 dual_loss=4.8481e-01
Validation X2Y - loss=2.8339e+00 ppl=17.01 best_loss=2.8575e+00 best_ppl=17.42                                          
Validation Y2X - loss=2.6231e+00 ppl=13.78 best_loss=2.6781e+00 best_ppl=14.56
Epoch 28 - |param|=8.64e+02 |g_param|=1.83e+05 loss_x2y=3.0345e+00 ppl_x2y=20.79 loss_y2x=2.7582e+00 ppl_y2x=15.77 dual_loss=3.9756e-01
Validation X2Y - loss=2.8126e+00 ppl=16.65 best_loss=2.8339e+00 best_ppl=17.01                                          
Validation Y2X - loss=2.6192e+00 ppl=13.72 best_loss=2.6231e+00 best_ppl=13.78
Epoch 29 - |param|=8.65e+02 |g_param|=1.84e+05 loss_x2y=3.0161e+00 ppl_x2y=20.41 loss_y2x=2.7522e+00 ppl_y2x=15.68 dual_loss=3.9321e-01
Validation X2Y - loss=2.7992e+00 ppl=16.43 best_loss=2.8126e+00 best_ppl=16.65                                          
Validation Y2X - loss=2.5952e+00 ppl=13.40 best_loss=2.6192e+00 best_ppl=13.72
Epoch 30 - |param|=8.66e+02 |g_param|=1.87e+05 loss_x2y=2.9513e+00 ppl_x2y=19.13 loss_y2x=2.6512e+00 ppl_y2x=14.17 dual_loss=3.7632e-01
Validation X2Y - loss=2.7743e+00 ppl=16.03 best_loss=2.7992e+00 best_ppl=16.43                                          
Validation Y2X - loss=2.5587e+00 ppl=12.92 best_loss=2.5952e+00 best_ppl=13.40
Epoch 31 - |param|=8.66e+02 |g_param|=1.87e+05 loss_x2y=3.0091e+00 ppl_x2y=20.27 loss_y2x=2.7190e+00 ppl_y2x=15.16 dual_loss=4.0924e-01
Validation X2Y - loss=2.7597e+00 ppl=15.79 best_loss=2.7743e+00 best_ppl=16.03                                          
Validation Y2X - loss=2.5337e+00 ppl=12.60 best_loss=2.5587e+00 best_ppl=12.92
Epoch 32 - |param|=8.67e+02 |g_param|=1.99e+05 loss_x2y=2.9790e+00 ppl_x2y=19.67 loss_y2x=2.6685e+00 ppl_y2x=14.42 dual_loss=4.1302e-01
Validation X2Y - loss=2.7594e+00 ppl=15.79 best_loss=2.7597e+00 best_ppl=15.79                                          
Validation Y2X - loss=2.5295e+00 ppl=12.55 best_loss=2.5337e+00 best_ppl=12.60
Epoch 33 - |param|=8.68e+02 |g_param|=1.91e+05 loss_x2y=2.9109e+00 ppl_x2y=18.37 loss_y2x=2.6258e+00 ppl_y2x=13.82 dual_loss=3.6793e-01
Validation X2Y - loss=2.7150e+00 ppl=15.10 best_loss=2.7594e+00 best_ppl=15.79                                          
Validation Y2X - loss=2.4942e+00 ppl=12.11 best_loss=2.5295e+00 best_ppl=12.55
Epoch 34 - |param|=8.68e+02 |g_param|=3.12e+05 loss_x2y=2.8506e+00 ppl_x2y=17.30 loss_y2x=2.5471e+00 ppl_y2x=12.77 dual_loss=3.3967e-01
Validation X2Y - loss=2.6884e+00 ppl=14.71 best_loss=2.7150e+00 best_ppl=15.10                                          
Validation Y2X - loss=2.4489e+00 ppl=11.58 best_loss=2.4942e+00 best_ppl=12.11
Epoch 35 - |param|=8.69e+02 |g_param|=3.44e+05 loss_x2y=2.7840e+00 ppl_x2y=16.18 loss_y2x=2.4754e+00 ppl_y2x=11.89 dual_loss=3.2401e-01
Validation X2Y - loss=2.6976e+00 ppl=14.84 best_loss=2.6884e+00 best_ppl=14.71                                          
Validation Y2X - loss=2.4496e+00 ppl=11.58 best_loss=2.4489e+00 best_ppl=11.58
Epoch 36 - |param|=8.69e+02 |g_param|=3.82e+05 loss_x2y=2.8065e+00 ppl_x2y=16.55 loss_y2x=2.4827e+00 ppl_y2x=11.97 dual_loss=3.3315e-01
Validation X2Y - loss=2.6696e+00 ppl=14.43 best_loss=2.6884e+00 best_ppl=14.71                                          
Validation Y2X - loss=2.4282e+00 ppl=11.34 best_loss=2.4489e+00 best_ppl=11.58
Epoch 37 - |param|=8.70e+02 |g_param|=3.83e+05 loss_x2y=2.7626e+00 ppl_x2y=15.84 loss_y2x=2.4347e+00 ppl_y2x=11.41 dual_loss=3.1165e-01
Validation X2Y - loss=2.6791e+00 ppl=14.57 best_loss=2.6696e+00 best_ppl=14.43                                          
Validation Y2X - loss=2.4440e+00 ppl=11.52 best_loss=2.4282e+00 best_ppl=11.34
Epoch 38 - |param|=8.71e+02 |g_param|=3.98e+05 loss_x2y=2.7730e+00 ppl_x2y=16.01 loss_y2x=2.4836e+00 ppl_y2x=11.98 dual_loss=3.1780e-01
Validation X2Y - loss=2.6834e+00 ppl=14.64 best_loss=2.6696e+00 best_ppl=14.43                                          
Validation Y2X - loss=2.4299e+00 ppl=11.36 best_loss=2.4282e+00 best_ppl=11.34
Epoch 39 - |param|=8.71e+02 |g_param|=3.74e+05 loss_x2y=2.6598e+00 ppl_x2y=14.29 loss_y2x=2.3455e+00 ppl_y2x=10.44 dual_loss=2.8736e-01
Validation X2Y - loss=2.6752e+00 ppl=14.52 best_loss=2.6696e+00 best_ppl=14.43                                          
Validation Y2X - loss=2.4023e+00 ppl=11.05 best_loss=2.4282e+00 best_ppl=11.34
Epoch 40 - |param|=8.72e+02 |g_param|=4.01e+05 loss_x2y=2.6668e+00 ppl_x2y=14.39 loss_y2x=2.3483e+00 ppl_y2x=10.47 dual_loss=2.8597e-01
Validation X2Y - loss=2.6508e+00 ppl=14.17 best_loss=2.6696e+00 best_ppl=14.43                                          
Validation Y2X - loss=2.3931e+00 ppl=10.95 best_loss=2.4023e+00 best_ppl=11.05
Epoch 41 - |param|=8.73e+02 |g_param|=4.08e+05 loss_x2y=2.6046e+00 ppl_x2y=13.53 loss_y2x=2.3169e+00 ppl_y2x=10.14 dual_loss=2.7934e-01
Validation X2Y - loss=2.6401e+00 ppl=14.01 best_loss=2.6508e+00 best_ppl=14.17                                          
Validation Y2X - loss=2.3951e+00 ppl=10.97 best_loss=2.3931e+00 best_ppl=10.95
Epoch 42 - |param|=8.73e+02 |g_param|=4.49e+05 loss_x2y=2.5468e+00 ppl_x2y=12.77 loss_y2x=2.2401e+00 ppl_y2x=9.39 dual_loss=2.6151e-01
Validation X2Y - loss=2.6168e+00 ppl=13.69 best_loss=2.6401e+00 best_ppl=14.01                                          
Validation Y2X - loss=2.3744e+00 ppl=10.74 best_loss=2.3931e+00 best_ppl=10.95
Epoch 43 - |param|=8.74e+02 |g_param|=4.31e+05 loss_x2y=2.5640e+00 ppl_x2y=12.99 loss_y2x=2.2522e+00 ppl_y2x=9.51 dual_loss=2.6771e-01
Validation X2Y - loss=2.6217e+00 ppl=13.76 best_loss=2.6168e+00 best_ppl=13.69                                          
Validation Y2X - loss=2.3899e+00 ppl=10.91 best_loss=2.3744e+00 best_ppl=10.74
Epoch 44 - |param|=8.75e+02 |g_param|=4.33e+05 loss_x2y=2.4899e+00 ppl_x2y=12.06 loss_y2x=2.1805e+00 ppl_y2x=8.85 dual_loss=2.5347e-01
Validation X2Y - loss=2.6157e+00 ppl=13.68 best_loss=2.6168e+00 best_ppl=13.69                                          
Validation Y2X - loss=2.3231e+00 ppl=10.21 best_loss=2.3744e+00 best_ppl=10.74
Epoch 45 - |param|=8.75e+02 |g_param|=4.30e+05 loss_x2y=2.4558e+00 ppl_x2y=11.66 loss_y2x=2.1433e+00 ppl_y2x=8.53 dual_loss=2.4553e-01
Validation X2Y - loss=2.6393e+00 ppl=14.00 best_loss=2.6157e+00 best_ppl=13.68                                          
Validation Y2X - loss=2.3657e+00 ppl=10.65 best_loss=2.3231e+00 best_ppl=10.21
Epoch 46 - |param|=8.76e+02 |g_param|=4.47e+05 loss_x2y=2.4643e+00 ppl_x2y=11.76 loss_y2x=2.1571e+00 ppl_y2x=8.65 dual_loss=2.5339e-01
Validation X2Y - loss=2.5936e+00 ppl=13.38 best_loss=2.6157e+00 best_ppl=13.68                                          
Validation Y2X - loss=2.3546e+00 ppl=10.53 best_loss=2.3231e+00 best_ppl=10.21
Epoch 47 - |param|=8.76e+02 |g_param|=4.59e+05 loss_x2y=2.5197e+00 ppl_x2y=12.42 loss_y2x=2.2475e+00 ppl_y2x=9.46 dual_loss=2.7771e-01
Validation X2Y - loss=2.5926e+00 ppl=13.36 best_loss=2.5936e+00 best_ppl=13.38                                          
Validation Y2X - loss=2.3525e+00 ppl=10.51 best_loss=2.3231e+00 best_ppl=10.21
Epoch 48 - |param|=8.77e+02 |g_param|=5.11e+05 loss_x2y=2.4302e+00 ppl_x2y=11.36 loss_y2x=2.1516e+00 ppl_y2x=8.60 dual_loss=2.5814e-01
Validation X2Y - loss=2.6286e+00 ppl=13.85 best_loss=2.5926e+00 best_ppl=13.36                                          
Validation Y2X - loss=2.3346e+00 ppl=10.33 best_loss=2.3231e+00 best_ppl=10.21
Epoch 49 - |param|=8.78e+02 |g_param|=4.87e+05 loss_x2y=2.4319e+00 ppl_x2y=11.38 loss_y2x=2.1273e+00 ppl_y2x=8.39 dual_loss=2.5694e-01
Validation X2Y - loss=2.5837e+00 ppl=13.25 best_loss=2.5926e+00 best_ppl=13.36                                          
Validation Y2X - loss=2.3301e+00 ppl=10.28 best_loss=2.3231e+00 best_ppl=10.21
Epoch 50 - |param|=8.78e+02 |g_param|=4.86e+05 loss_x2y=2.3789e+00 ppl_x2y=10.79 loss_y2x=2.0683e+00 ppl_y2x=7.91 dual_loss=2.4825e-01
Validation X2Y - loss=2.5941e+00 ppl=13.38 best_loss=2.5837e+00 best_ppl=13.25                                          
Validation Y2X - loss=2.3342e+00 ppl=10.32 best_loss=2.3231e+00 best_ppl=10.21
Epoch 51 - |param|=8.79e+02 |g_param|=4.69e+05 loss_x2y=2.3356e+00 ppl_x2y=10.34 loss_y2x=2.0215e+00 ppl_y2x=7.55 dual_loss=2.4632e-01
Validation X2Y - loss=2.6055e+00 ppl=13.54 best_loss=2.5837e+00 best_ppl=13.25                                          
Validation Y2X - loss=2.3467e+00 ppl=10.45 best_loss=2.3231e+00 best_ppl=10.21
Epoch 52 - |param|=8.79e+02 |g_param|=5.41e+05 loss_x2y=2.3105e+00 ppl_x2y=10.08 loss_y2x=2.0268e+00 ppl_y2x=7.59 dual_loss=2.5108e-01
Validation X2Y - loss=2.5655e+00 ppl=13.01 best_loss=2.5837e+00 best_ppl=13.25                                          
Validation Y2X - loss=2.3216e+00 ppl=10.19 best_loss=2.3231e+00 best_ppl=10.21
Epoch 53 - |param|=8.80e+02 |g_param|=4.88e+05 loss_x2y=2.2726e+00 ppl_x2y=9.70 loss_y2x=1.9686e+00 ppl_y2x=7.16 dual_loss=2.4348e-01
Validation X2Y - loss=2.5646e+00 ppl=13.00 best_loss=2.5655e+00 best_ppl=13.01                                          
Validation Y2X - loss=2.3401e+00 ppl=10.38 best_loss=2.3216e+00 best_ppl=10.19
Epoch 54 - |param|=8.81e+02 |g_param|=5.28e+05 loss_x2y=2.2857e+00 ppl_x2y=9.83 loss_y2x=2.0418e+00 ppl_y2x=7.70 dual_loss=2.5127e-01
Validation X2Y - loss=2.5854e+00 ppl=13.27 best_loss=2.5646e+00 best_ppl=13.00                                          
Validation Y2X - loss=2.3251e+00 ppl=10.23 best_loss=2.3216e+00 best_ppl=10.19
Epoch 55 - |param|=8.81e+02 |g_param|=5.04e+05 loss_x2y=2.2532e+00 ppl_x2y=9.52 loss_y2x=1.9619e+00 ppl_y2x=7.11 dual_loss=2.5002e-01
Validation X2Y - loss=2.6017e+00 ppl=13.49 best_loss=2.5646e+00 best_ppl=13.00                                          
Validation Y2X - loss=2.3306e+00 ppl=10.28 best_loss=2.3216e+00 best_ppl=10.19
Epoch 56 - |param|=8.82e+02 |g_param|=5.09e+05 loss_x2y=2.2113e+00 ppl_x2y=9.13 loss_y2x=1.8829e+00 ppl_y2x=6.57 dual_loss=2.4017e-01
Validation X2Y - loss=2.5859e+00 ppl=13.27 best_loss=2.5646e+00 best_ppl=13.00                                          
Validation Y2X - loss=2.3077e+00 ppl=10.05 best_loss=2.3216e+00 best_ppl=10.19
Epoch 57 - |param|=8.82e+02 |g_param|=5.39e+05 loss_x2y=2.2800e+00 ppl_x2y=9.78 loss_y2x=1.9962e+00 ppl_y2x=7.36 dual_loss=2.5853e-01
Validation X2Y - loss=2.5656e+00 ppl=13.01 best_loss=2.5646e+00 best_ppl=13.00                                          
Validation Y2X - loss=2.3068e+00 ppl=10.04 best_loss=2.3077e+00 best_ppl=10.05
Epoch 58 - |param|=8.83e+02 |g_param|=5.46e+05 loss_x2y=2.2132e+00 ppl_x2y=9.15 loss_y2x=1.9117e+00 ppl_y2x=6.76 dual_loss=2.5246e-01
Validation X2Y - loss=2.5837e+00 ppl=13.25 best_loss=2.5646e+00 best_ppl=13.00                                          
Validation Y2X - loss=2.3211e+00 ppl=10.19 best_loss=2.3068e+00 best_ppl=10.04
Epoch 59 - |param|=8.84e+02 |g_param|=5.09e+05 loss_x2y=2.1262e+00 ppl_x2y=8.38 loss_y2x=1.8263e+00 ppl_y2x=6.21 dual_loss=2.2914e-01
Validation X2Y - loss=2.5792e+00 ppl=13.19 best_loss=2.5646e+00 best_ppl=13.00                                          
Validation Y2X - loss=2.3097e+00 ppl=10.07 best_loss=2.3068e+00 best_ppl=10.04
Epoch 60 - |param|=8.84e+02 |g_param|=5.31e+05 loss_x2y=2.1258e+00 ppl_x2y=8.38 loss_y2x=1.8221e+00 ppl_y2x=6.19 dual_loss=2.3813e-01
Validation X2Y - loss=2.6004e+00 ppl=13.47 best_loss=2.5646e+00 best_ppl=13.00                                          
Validation Y2X - loss=2.2919e+00 ppl=9.89 best_loss=2.3068e+00 best_ppl=10.04
Epoch 61 - |param|=8.85e+02 |g_param|=5.16e+05 loss_x2y=2.0566e+00 ppl_x2y=7.82 loss_y2x=1.7951e+00 ppl_y2x=6.02 dual_loss=2.3464e-01
Validation X2Y - loss=2.6072e+00 ppl=13.56 best_loss=2.5646e+00 best_ppl=13.00                                          
Validation Y2X - loss=2.3267e+00 ppl=10.24 best_loss=2.2919e+00 best_ppl=9.89
Epoch 62 - |param|=8.85e+02 |g_param|=5.71e+05 loss_x2y=2.0829e+00 ppl_x2y=8.03 loss_y2x=1.7913e+00 ppl_y2x=6.00 dual_loss=2.4704e-01
Validation X2Y - loss=2.5823e+00 ppl=13.23 best_loss=2.5646e+00 best_ppl=13.00                                          
Validation Y2X - loss=2.2931e+00 ppl=9.91 best_loss=2.2919e+00 best_ppl=9.89
Epoch 63 - |param|=8.86e+02 |g_param|=5.59e+05 loss_x2y=2.1238e+00 ppl_x2y=8.36 loss_y2x=1.8039e+00 ppl_y2x=6.07 dual_loss=2.5259e-01
Validation X2Y - loss=2.5687e+00 ppl=13.05 best_loss=2.5646e+00 best_ppl=13.00                                          
Validation Y2X - loss=2.3162e+00 ppl=10.14 best_loss=2.2919e+00 best_ppl=9.89
Epoch 64 - |param|=8.86e+02 |g_param|=5.63e+05 loss_x2y=2.0052e+00 ppl_x2y=7.43 loss_y2x=1.7172e+00 ppl_y2x=5.57 dual_loss=2.3552e-01
Validation X2Y - loss=2.5475e+00 ppl=12.78 best_loss=2.5646e+00 best_ppl=13.00                                          
Validation Y2X - loss=2.2999e+00 ppl=9.97 best_loss=2.2919e+00 best_ppl=9.89
Epoch 65 - |param|=8.87e+02 |g_param|=5.58e+05 loss_x2y=2.0766e+00 ppl_x2y=7.98 loss_y2x=1.7741e+00 ppl_y2x=5.90 dual_loss=2.4168e-01
Validation X2Y - loss=2.5666e+00 ppl=13.02 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.2991e+00 ppl=9.97 best_loss=2.2919e+00 best_ppl=9.89
Epoch 66 - |param|=8.87e+02 |g_param|=7.17e+05 loss_x2y=2.0240e+00 ppl_x2y=7.57 loss_y2x=1.7278e+00 ppl_y2x=5.63 dual_loss=2.4522e-01
Validation X2Y - loss=2.5519e+00 ppl=12.83 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3214e+00 ppl=10.19 best_loss=2.2919e+00 best_ppl=9.89
Epoch 67 - |param|=8.88e+02 |g_param|=1.03e+06 loss_x2y=2.0128e+00 ppl_x2y=7.48 loss_y2x=1.7450e+00 ppl_y2x=5.73 dual_loss=2.6035e-01
Validation X2Y - loss=2.5801e+00 ppl=13.20 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.2844e+00 ppl=9.82 best_loss=2.2919e+00 best_ppl=9.89
Epoch 68 - |param|=8.89e+02 |g_param|=1.07e+06 loss_x2y=1.9681e+00 ppl_x2y=7.16 loss_y2x=1.6616e+00 ppl_y2x=5.27 dual_loss=2.4572e-01
Validation X2Y - loss=2.5798e+00 ppl=13.19 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.2832e+00 ppl=9.81 best_loss=2.2844e+00 best_ppl=9.82
Epoch 69 - |param|=8.89e+02 |g_param|=1.03e+06 loss_x2y=1.9146e+00 ppl_x2y=6.78 loss_y2x=1.6324e+00 ppl_y2x=5.12 dual_loss=2.4103e-01
Validation X2Y - loss=2.6065e+00 ppl=13.55 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.2957e+00 ppl=9.93 best_loss=2.2832e+00 best_ppl=9.81
Epoch 70 - |param|=8.90e+02 |g_param|=6.88e+05 loss_x2y=1.9065e+00 ppl_x2y=6.73 loss_y2x=1.6033e+00 ppl_y2x=4.97 dual_loss=2.4200e-01
Validation X2Y - loss=2.6051e+00 ppl=13.53 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3185e+00 ppl=10.16 best_loss=2.2832e+00 best_ppl=9.81
Epoch 71 - |param|=8.90e+02 |g_param|=5.77e+05 loss_x2y=1.8971e+00 ppl_x2y=6.67 loss_y2x=1.5929e+00 ppl_y2x=4.92 dual_loss=2.4855e-01
Validation X2Y - loss=2.5761e+00 ppl=13.15 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.2839e+00 ppl=9.81 best_loss=2.2832e+00 best_ppl=9.81
Epoch 72 - |param|=8.91e+02 |g_param|=6.13e+05 loss_x2y=1.9051e+00 ppl_x2y=6.72 loss_y2x=1.6034e+00 ppl_y2x=4.97 dual_loss=2.5730e-01
Validation X2Y - loss=2.5950e+00 ppl=13.40 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3165e+00 ppl=10.14 best_loss=2.2832e+00 best_ppl=9.81
Epoch 73 - |param|=8.91e+02 |g_param|=6.63e+05 loss_x2y=1.9241e+00 ppl_x2y=6.85 loss_y2x=1.6227e+00 ppl_y2x=5.07 dual_loss=2.6919e-01
Validation X2Y - loss=2.6177e+00 ppl=13.70 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3107e+00 ppl=10.08 best_loss=2.2832e+00 best_ppl=9.81
Epoch 74 - |param|=8.92e+02 |g_param|=7.52e+05 loss_x2y=1.8413e+00 ppl_x2y=6.31 loss_y2x=1.5435e+00 ppl_y2x=4.68 dual_loss=2.5482e-01
Validation X2Y - loss=2.6474e+00 ppl=14.12 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.2959e+00 ppl=9.93 best_loss=2.2832e+00 best_ppl=9.81
Epoch 75 - |param|=8.92e+02 |g_param|=7.95e+05 loss_x2y=1.9086e+00 ppl_x2y=6.74 loss_y2x=1.6450e+00 ppl_y2x=5.18 dual_loss=2.7099e-01
Validation X2Y - loss=2.6092e+00 ppl=13.59 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3158e+00 ppl=10.13 best_loss=2.2832e+00 best_ppl=9.81
Epoch 76 - |param|=8.93e+02 |g_param|=7.58e+05 loss_x2y=1.8097e+00 ppl_x2y=6.11 loss_y2x=1.5237e+00 ppl_y2x=4.59 dual_loss=2.5581e-01
Validation X2Y - loss=2.6109e+00 ppl=13.61 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.2974e+00 ppl=9.95 best_loss=2.2832e+00 best_ppl=9.81
Epoch 77 - |param|=8.93e+02 |g_param|=7.75e+05 loss_x2y=1.7855e+00 ppl_x2y=5.96 loss_y2x=1.4952e+00 ppl_y2x=4.46 dual_loss=2.6045e-01
Validation X2Y - loss=2.6280e+00 ppl=13.85 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.2943e+00 ppl=9.92 best_loss=2.2832e+00 best_ppl=9.81
Epoch 78 - |param|=8.94e+02 |g_param|=7.82e+05 loss_x2y=1.7691e+00 ppl_x2y=5.87 loss_y2x=1.4936e+00 ppl_y2x=4.45 dual_loss=2.6287e-01
Validation X2Y - loss=2.6233e+00 ppl=13.78 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3352e+00 ppl=10.33 best_loss=2.2832e+00 best_ppl=9.81
Epoch 79 - |param|=8.95e+02 |g_param|=7.26e+05 loss_x2y=1.7158e+00 ppl_x2y=5.56 loss_y2x=1.4280e+00 ppl_y2x=4.17 dual_loss=2.5193e-01
Validation X2Y - loss=2.6120e+00 ppl=13.63 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3349e+00 ppl=10.33 best_loss=2.2832e+00 best_ppl=9.81
Epoch 80 - |param|=8.95e+02 |g_param|=8.11e+05 loss_x2y=1.7942e+00 ppl_x2y=6.01 loss_y2x=1.5303e+00 ppl_y2x=4.62 dual_loss=2.7559e-01
Validation X2Y - loss=2.6264e+00 ppl=13.82 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3347e+00 ppl=10.33 best_loss=2.2832e+00 best_ppl=9.81
Epoch 81 - |param|=8.96e+02 |g_param|=8.18e+05 loss_x2y=1.8201e+00 ppl_x2y=6.17 loss_y2x=1.5425e+00 ppl_y2x=4.68 dual_loss=2.9200e-01
Validation X2Y - loss=2.6300e+00 ppl=13.87 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3321e+00 ppl=10.30 best_loss=2.2832e+00 best_ppl=9.81
Epoch 82 - |param|=8.96e+02 |g_param|=8.10e+05 loss_x2y=1.7536e+00 ppl_x2y=5.78 loss_y2x=1.4333e+00 ppl_y2x=4.19 dual_loss=2.7286e-01
Validation X2Y - loss=2.6225e+00 ppl=13.77 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3308e+00 ppl=10.29 best_loss=2.2832e+00 best_ppl=9.81
Epoch 83 - |param|=8.97e+02 |g_param|=7.86e+05 loss_x2y=1.6833e+00 ppl_x2y=5.38 loss_y2x=1.4058e+00 ppl_y2x=4.08 dual_loss=2.6173e-01
Validation X2Y - loss=2.6658e+00 ppl=14.38 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3186e+00 ppl=10.16 best_loss=2.2832e+00 best_ppl=9.81
Epoch 84 - |param|=8.97e+02 |g_param|=8.51e+05 loss_x2y=1.7135e+00 ppl_x2y=5.55 loss_y2x=1.4238e+00 ppl_y2x=4.15 dual_loss=2.6572e-01
Validation X2Y - loss=2.6567e+00 ppl=14.25 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3095e+00 ppl=10.07 best_loss=2.2832e+00 best_ppl=9.81
Epoch 85 - |param|=8.98e+02 |g_param|=7.91e+05 loss_x2y=1.6710e+00 ppl_x2y=5.32 loss_y2x=1.4037e+00 ppl_y2x=4.07 dual_loss=2.8230e-01
Validation X2Y - loss=2.6649e+00 ppl=14.37 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3353e+00 ppl=10.33 best_loss=2.2832e+00 best_ppl=9.81
Epoch 86 - |param|=8.98e+02 |g_param|=8.99e+05 loss_x2y=1.7130e+00 ppl_x2y=5.55 loss_y2x=1.4613e+00 ppl_y2x=4.31 dual_loss=2.8963e-01
Validation X2Y - loss=2.6390e+00 ppl=14.00 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3166e+00 ppl=10.14 best_loss=2.2832e+00 best_ppl=9.81
Epoch 87 - |param|=8.99e+02 |g_param|=8.05e+05 loss_x2y=1.6673e+00 ppl_x2y=5.30 loss_y2x=1.3693e+00 ppl_y2x=3.93 dual_loss=2.7769e-01
Validation X2Y - loss=2.6490e+00 ppl=14.14 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.2998e+00 ppl=9.97 best_loss=2.2832e+00 best_ppl=9.81
Epoch 88 - |param|=8.99e+02 |g_param|=8.21e+05 loss_x2y=1.6662e+00 ppl_x2y=5.29 loss_y2x=1.3414e+00 ppl_y2x=3.82 dual_loss=2.8298e-01
Validation X2Y - loss=2.6402e+00 ppl=14.02 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3241e+00 ppl=10.22 best_loss=2.2832e+00 best_ppl=9.81
Epoch 89 - |param|=9.00e+02 |g_param|=8.10e+05 loss_x2y=1.6430e+00 ppl_x2y=5.17 loss_y2x=1.3647e+00 ppl_y2x=3.91 dual_loss=2.7688e-01
Validation X2Y - loss=2.6582e+00 ppl=14.27 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3726e+00 ppl=10.73 best_loss=2.2832e+00 best_ppl=9.81
Epoch 90 - |param|=9.00e+02 |g_param|=8.49e+05 loss_x2y=1.6102e+00 ppl_x2y=5.00 loss_y2x=1.3074e+00 ppl_y2x=3.70 dual_loss=2.8270e-01
Validation X2Y - loss=2.6549e+00 ppl=14.22 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3152e+00 ppl=10.13 best_loss=2.2832e+00 best_ppl=9.81
Epoch 91 - |param|=9.01e+02 |g_param|=8.86e+05 loss_x2y=1.6858e+00 ppl_x2y=5.40 loss_y2x=1.4405e+00 ppl_y2x=4.22 dual_loss=3.6370e-01
Validation X2Y - loss=2.6526e+00 ppl=14.19 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3379e+00 ppl=10.36 best_loss=2.2832e+00 best_ppl=9.81
Epoch 92 - |param|=9.01e+02 |g_param|=8.27e+05 loss_x2y=1.5755e+00 ppl_x2y=4.83 loss_y2x=1.2828e+00 ppl_y2x=3.61 dual_loss=2.9024e-01
Validation X2Y - loss=2.6688e+00 ppl=14.42 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3593e+00 ppl=10.58 best_loss=2.2832e+00 best_ppl=9.81
Epoch 93 - |param|=9.02e+02 |g_param|=8.46e+05 loss_x2y=1.5830e+00 ppl_x2y=4.87 loss_y2x=1.2810e+00 ppl_y2x=3.60 dual_loss=3.0190e-01
Validation X2Y - loss=2.6933e+00 ppl=14.78 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3696e+00 ppl=10.69 best_loss=2.2832e+00 best_ppl=9.81
Epoch 94 - |param|=9.02e+02 |g_param|=8.49e+05 loss_x2y=1.5319e+00 ppl_x2y=4.63 loss_y2x=1.2402e+00 ppl_y2x=3.46 dual_loss=2.8816e-01
Validation X2Y - loss=2.6553e+00 ppl=14.23 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3481e+00 ppl=10.47 best_loss=2.2832e+00 best_ppl=9.81
Epoch 95 - |param|=9.03e+02 |g_param|=8.34e+05 loss_x2y=1.6237e+00 ppl_x2y=5.07 loss_y2x=1.2644e+00 ppl_y2x=3.54 dual_loss=2.9179e-01
Validation X2Y - loss=2.7312e+00 ppl=15.35 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3125e+00 ppl=10.10 best_loss=2.2832e+00 best_ppl=9.81
Epoch 96 - |param|=9.03e+02 |g_param|=8.58e+05 loss_x2y=1.5595e+00 ppl_x2y=4.76 loss_y2x=1.2811e+00 ppl_y2x=3.60 dual_loss=3.2209e-01
Validation X2Y - loss=2.6870e+00 ppl=14.69 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3292e+00 ppl=10.27 best_loss=2.2832e+00 best_ppl=9.81
Epoch 97 - |param|=9.04e+02 |g_param|=8.43e+05 loss_x2y=1.5165e+00 ppl_x2y=4.56 loss_y2x=1.2259e+00 ppl_y2x=3.41 dual_loss=3.0335e-01
Validation X2Y - loss=2.7042e+00 ppl=14.94 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3496e+00 ppl=10.48 best_loss=2.2832e+00 best_ppl=9.81
Epoch 98 - |param|=9.04e+02 |g_param|=8.33e+05 loss_x2y=1.4845e+00 ppl_x2y=4.41 loss_y2x=1.1910e+00 ppl_y2x=3.29 dual_loss=2.9313e-01
Validation X2Y - loss=2.7206e+00 ppl=15.19 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3597e+00 ppl=10.59 best_loss=2.2832e+00 best_ppl=9.81
Epoch 99 - |param|=9.05e+02 |g_param|=8.71e+05 loss_x2y=1.4911e+00 ppl_x2y=4.44 loss_y2x=1.2347e+00 ppl_y2x=3.44 dual_loss=3.2359e-01
Validation X2Y - loss=2.7394e+00 ppl=15.48 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3536e+00 ppl=10.52 best_loss=2.2832e+00 best_ppl=9.81
Epoch 100 - |param|=9.05e+02 |g_param|=9.03e+05 loss_x2y=1.4899e+00 ppl_x2y=4.44 loss_y2x=1.1712e+00 ppl_y2x=3.23 dual_loss=3.0753e-01
Validation X2Y - loss=2.7239e+00 ppl=15.24 best_loss=2.5475e+00 best_ppl=12.78                                          
Validation Y2X - loss=2.3963e+00 ppl=10.98 best_loss=2.2832e+00 best_ppl=9.81

real	26m38.967s
user	26m17.418s
sys	0m19.712s
```

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/mybk-100epoch
Evaluation result for the model: dsl-model-mybk.01.4.89-133.35.4.70-109.40.4.10-60.11.3.91-49.99.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.4/0.0/0.0/0.0 (BP=0.764, ratio=0.788, hyp_len=9006, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.89-133.35.4.70-109.40.4.10-60.11.3.91-49.99.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 23.4/0.1/0.0/0.0 (BP=0.604, ratio=0.665, hyp_len=8128, ref_len=12231)
Traceback (most recent call last):
  File "/home/ye/exp/simple-nmt/translate.py", line 182, in <module>
    map_location='cpu',
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/serialization.py", line 608, in load
    return _legacy_load(opened_file, map_location, pickle_module, **pickle_load_args)
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/serialization.py", line 777, in _legacy_load
    magic_number = pickle_module.load(f, **pickle_load_args)
EOFError: Ran out of input
Evaluation result for the model: dsl-model-mybk.01.4.92-137.59.4.74-113.95.4.09-59.90.3.99-54.10.pth, mybk
Use of uninitialized value $length_reference in numeric eq (==) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 148.
BLEU = 0, 0/0/0/0 (BP=0, ratio=0, hyp_len=0, ref_len=0)
Traceback (most recent call last):
  File "/home/ye/exp/simple-nmt/translate.py", line 182, in <module>
    map_location='cpu',
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/serialization.py", line 608, in load
    return _legacy_load(opened_file, map_location, pickle_module, **pickle_load_args)
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/serialization.py", line 777, in _legacy_load
    magic_number = pickle_module.load(f, **pickle_load_args)
EOFError: Ran out of input
Evaluation result for the model: dsl-model-mybk.01.4.92-137.59.4.74-113.95.4.09-59.90.3.99-54.10.pth, bkmy
Use of uninitialized value $length_reference in numeric eq (==) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 148.
BLEU = 0, 0/0/0/0 (BP=0, ratio=0, hyp_len=0, ref_len=0)
Evaluation result for the model: dsl-model-mybk.02.4.43-83.79.4.23-68.39.3.90-49.61.3.82-45.77.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.4/0.2/0.0/0.0 (BP=1.000, ratio=1.009, hyp_len=11537, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.4.43-83.79.4.23-68.39.3.90-49.61.3.82-45.77.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.5/0.6/0.0/0.0 (BP=0.960, ratio=0.961, hyp_len=11755, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.4.37-79.04.4.16-63.80.3.88-48.29.3.80-44.90.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.4/0.2/0.0/0.0 (BP=1.000, ratio=1.048, hyp_len=11977, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.4.37-79.04.4.16-63.80.3.88-48.29.3.80-44.90.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.3/1.0/0.1/0.0 (BP=1.000, ratio=1.004, hyp_len=12280, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.4.36-78.06.4.14-62.86.3.85-46.84.3.74-42.11.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.2/0.1/0.0/0.0 (BP=1.000, ratio=1.029, hyp_len=11762, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.4.36-78.06.4.14-62.86.3.85-46.84.3.74-42.11.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.1/0.5/0.0/0.0 (BP=1.000, ratio=1.026, hyp_len=12543, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.4.32-74.88.4.08-59.12.3.84-46.51.3.67-39.41.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.5/0.4/0.0/0.0 (BP=1.000, ratio=1.074, hyp_len=12280, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.4.32-74.88.4.08-59.12.3.84-46.51.3.67-39.41.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.9/0.6/0.0/0.0 (BP=1.000, ratio=1.030, hyp_len=12604, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.4.31-74.07.4.09-59.49.3.82-45.62.3.69-39.93.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 15.3/0.0/0.0/0.0 (BP=1.000, ratio=1.036, hyp_len=11844, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.4.31-74.07.4.09-59.49.3.82-45.62.3.69-39.93.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.3/1.0/0.1/0.0 (BP=0.960, ratio=0.961, hyp_len=11748, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.4.39-80.79.4.11-61.18.3.77-43.37.3.65-38.56.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 14.5/0.1/0.0/0.0 (BP=1.000, ratio=1.090, hyp_len=12456, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.4.39-80.79.4.11-61.18.3.77-43.37.3.65-38.56.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.9/0.5/0.0/0.0 (BP=1.000, ratio=1.029, hyp_len=12588, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.4.36-78.11.4.12-61.39.3.77-43.37.3.61-37.13.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.8/0.9/0.0/0.0 (BP=1.000, ratio=1.063, hyp_len=12153, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.4.36-78.11.4.12-61.39.3.77-43.37.3.61-37.13.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 19.9/1.0/0.1/0.0 (BP=1.000, ratio=1.052, hyp_len=12869, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.4.31-74.62.4.09-59.71.3.81-45.02.3.56-35.07.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 16.4/0.8/0.0/0.0 (BP=1.000, ratio=1.126, hyp_len=12877, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.4.31-74.62.4.09-59.71.3.81-45.02.3.56-35.07.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 14.4/0.1/0.0/0.0 (BP=1.000, ratio=1.143, hyp_len=13986, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.100.1.49-4.44.1.17-3.23.2.72-15.24.2.40-10.98.pth, mybk
BLEU = 10.91, 36.6/14.9/7.1/3.7 (BP=1.000, ratio=1.089, hyp_len=12445, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.100.1.49-4.44.1.17-3.23.2.72-15.24.2.40-10.98.pth, bkmy
BLEU = 14.31, 42.3/19.7/9.8/5.1 (BP=1.000, ratio=1.078, hyp_len=13183, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.4.12-61.72.3.88-48.50.3.60-36.72.3.42-30.58.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 21.6/0.7/0.0/0.0 (BP=0.812, ratio=0.828, hyp_len=9463, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.4.12-61.72.3.88-48.50.3.60-36.72.3.42-30.58.pth, bkmy
BLEU = 0.81, 20.8/1.9/0.4/0.0 (BP=0.975, ratio=0.976, hyp_len=11933, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.4.07-58.33.3.76-43.13.3.46-31.92.3.30-27.06.pth, mybk
BLEU = 0.68, 23.4/2.3/0.6/0.0 (BP=0.782, ratio=0.802, hyp_len=9174, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.4.07-58.33.3.76-43.13.3.46-31.92.3.30-27.06.pth, bkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 20.3/2.1/0.3/0.0 (BP=1.000, ratio=1.007, hyp_len=12322, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.3.90-49.64.3.61-37.05.3.40-29.90.3.21-24.78.pth, mybk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1037.
BLEU = 0.00, 23.2/3.0/0.1/0.0 (BP=0.903, ratio=0.907, hyp_len=10373, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.3.90-49.64.3.61-37.05.3.40-29.90.3.21-24.78.pth, bkmy
BLEU = 1.07, 19.8/3.2/0.5/0.0 (BP=1.000, ratio=1.182, hyp_len=14454, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.3.81-45.04.3.51-33.39.3.33-27.85.3.13-22.80.pth, mybk
BLEU = 0.83, 22.1/2.9/0.3/0.0 (BP=1.000, ratio=1.015, hyp_len=11601, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.3.81-45.04.3.51-33.39.3.33-27.85.3.13-22.80.pth, bkmy
BLEU = 0.19, 3.9/0.7/0.1/0.0 (BP=1.000, ratio=5.464, hyp_len=66831, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.3.79-44.16.3.49-32.78.3.28-26.52.3.03-20.79.pth, mybk
BLEU = 0.99, 20.0/4.2/1.1/0.0 (BP=1.000, ratio=1.124, hyp_len=12852, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.3.79-44.16.3.49-32.78.3.28-26.52.3.03-20.79.pth, bkmy
BLEU = 0.12, 1.6/0.4/0.1/0.0 (BP=1.000, ratio=11.311, hyp_len=138339, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.3.63-37.75.3.31-27.25.3.25-25.75.3.00-20.06.pth, mybk
BLEU = 1.51, 23.0/5.0/1.3/0.0 (BP=0.992, ratio=0.992, hyp_len=11344, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.3.63-37.75.3.31-27.25.3.25-25.75.3.00-20.06.pth, bkmy
BLEU = 2.08, 19.5/5.1/1.1/0.2 (BP=1.000, ratio=1.532, hyp_len=18733, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.3.62-37.52.3.31-27.35.3.23-25.26.2.96-19.38.pth, mybk
BLEU = 1.85, 22.0/5.2/1.2/0.1 (BP=1.000, ratio=1.124, hyp_len=12852, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.3.62-37.52.3.31-27.35.3.23-25.26.2.96-19.38.pth, bkmy
BLEU = 0.52, 5.2/1.3/0.3/0.0 (BP=1.000, ratio=5.496, hyp_len=67222, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.3.59-36.06.3.26-26.00.3.20-24.62.2.93-18.70.pth, mybk
BLEU = 2.54, 18.5/4.7/1.3/0.4 (BP=1.000, ratio=1.367, hyp_len=15628, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.3.59-36.06.3.26-26.00.3.20-24.62.2.93-18.70.pth, bkmy
BLEU = 2.27, 19.0/5.2/1.2/0.2 (BP=1.000, ratio=1.536, hyp_len=18785, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.3.53-34.09.3.20-24.56.3.15-23.25.2.90-18.20.pth, mybk
BLEU = 3.06, 20.8/5.2/1.6/0.5 (BP=1.000, ratio=1.288, hyp_len=14721, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.3.53-34.09.3.20-24.56.3.15-23.25.2.90-18.20.pth, bkmy
BLEU = 4.65, 28.1/8.8/2.6/0.7 (BP=1.000, ratio=1.095, hyp_len=13398, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.3.47-32.02.3.15-23.29.3.11-22.51.2.84-17.10.pth, mybk
BLEU = 2.91, 22.1/5.4/1.5/0.4 (BP=1.000, ratio=1.206, hyp_len=13782, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.3.47-32.02.3.15-23.29.3.11-22.51.2.84-17.10.pth, bkmy
BLEU = 4.75, 30.2/9.8/2.8/0.6 (BP=1.000, ratio=1.044, hyp_len=12767, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.3.42-30.60.3.08-21.67.3.05-21.11.2.84-17.13.pth, mybk
BLEU = 2.54, 16.2/4.2/1.3/0.5 (BP=1.000, ratio=1.632, hyp_len=18658, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.3.42-30.60.3.08-21.67.3.05-21.11.2.84-17.13.pth, bkmy
BLEU = 6.27, 31.1/10.7/3.8/1.2 (BP=1.000, ratio=1.032, hyp_len=12621, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.3.44-31.04.3.08-21.79.3.04-20.81.2.81-16.69.pth, mybk
BLEU = 2.84, 17.0/4.4/1.5/0.6 (BP=1.000, ratio=1.543, hyp_len=17645, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.3.44-31.04.3.08-21.79.3.04-20.81.2.81-16.69.pth, bkmy
BLEU = 6.63, 32.0/11.5/4.1/1.3 (BP=1.000, ratio=1.033, hyp_len=12637, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.3.34-28.18.3.04-20.94.2.97-19.53.2.79-16.32.pth, mybk
BLEU = 2.81, 16.3/4.3/1.6/0.6 (BP=1.000, ratio=1.637, hyp_len=18719, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.3.34-28.18.3.04-20.94.2.97-19.53.2.79-16.32.pth, bkmy
BLEU = 3.50, 16.9/5.9/2.1/0.7 (BP=1.000, ratio=1.931, hyp_len=23617, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.3.27-26.29.2.96-19.39.2.99-19.94.2.74-15.49.pth, mybk
BLEU = 2.43, 14.1/3.8/1.3/0.5 (BP=1.000, ratio=1.925, hyp_len=22001, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.3.27-26.29.2.96-19.39.2.99-19.94.2.74-15.49.pth, bkmy
BLEU = 2.70, 13.0/4.6/1.6/0.5 (BP=1.000, ratio=2.539, hyp_len=31058, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.3.23-25.26.2.91-18.31.2.93-18.70.2.73-15.26.pth, mybk
BLEU = 2.96, 15.9/4.5/1.7/0.6 (BP=1.000, ratio=1.746, hyp_len=19958, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.3.23-25.26.2.91-18.31.2.93-18.70.2.73-15.26.pth, bkmy
BLEU = 7.39, 31.3/11.9/4.6/1.7 (BP=1.000, ratio=1.101, hyp_len=13461, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.3.32-27.58.3.03-20.66.2.90-18.10.2.71-14.97.pth, mybk
BLEU = 2.74, 14.5/4.3/1.6/0.6 (BP=1.000, ratio=1.968, hyp_len=22503, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.3.32-27.58.3.03-20.66.2.90-18.10.2.71-14.97.pth, bkmy
BLEU = 6.14, 27.8/10.3/3.7/1.3 (BP=1.000, ratio=1.240, hyp_len=15162, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.3.13-22.93.2.85-17.29.2.86-17.42.2.68-14.56.pth, mybk
BLEU = 5.07, 23.3/7.7/3.0/1.2 (BP=1.000, ratio=1.299, hyp_len=14851, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.3.13-22.93.2.85-17.29.2.86-17.42.2.68-14.56.pth, bkmy
BLEU = 4.42, 19.8/7.4/2.7/1.0 (BP=1.000, ratio=1.792, hyp_len=21919, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.3.15-23.35.2.85-17.26.2.83-17.01.2.62-13.78.pth, mybk
BLEU = 3.91, 20.2/6.2/2.2/0.8 (BP=1.000, ratio=1.447, hyp_len=16539, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.3.15-23.35.2.85-17.26.2.83-17.01.2.62-13.78.pth, bkmy
BLEU = 7.86, 31.4/12.3/5.0/2.0 (BP=1.000, ratio=1.149, hyp_len=14048, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.3.03-20.79.2.76-15.77.2.81-16.65.2.62-13.72.pth, mybk
BLEU = 4.25, 19.9/6.6/2.6/1.0 (BP=1.000, ratio=1.518, hyp_len=17358, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.3.03-20.79.2.76-15.77.2.81-16.65.2.62-13.72.pth, bkmy
BLEU = 8.21, 34.5/13.4/5.2/1.9 (BP=1.000, ratio=1.054, hyp_len=12888, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.3.02-20.41.2.75-15.68.2.80-16.43.2.60-13.40.pth, mybk
BLEU = 5.51, 25.5/8.4/3.2/1.3 (BP=1.000, ratio=1.192, hyp_len=13631, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.3.02-20.41.2.75-15.68.2.80-16.43.2.60-13.40.pth, bkmy
BLEU = 8.75, 35.2/14.0/5.5/2.2 (BP=1.000, ratio=1.047, hyp_len=12803, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.2.95-19.13.2.65-14.17.2.77-16.03.2.56-12.92.pth, mybk
BLEU = 4.80, 22.3/7.3/2.8/1.1 (BP=1.000, ratio=1.420, hyp_len=16236, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.2.95-19.13.2.65-14.17.2.77-16.03.2.56-12.92.pth, bkmy
BLEU = 7.57, 30.7/12.0/4.7/1.9 (BP=1.000, ratio=1.192, hyp_len=14574, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.31.3.01-20.27.2.72-15.16.2.76-15.79.2.53-12.60.pth, mybk
BLEU = 6.25, 27.6/9.5/3.8/1.5 (BP=1.000, ratio=1.160, hyp_len=13260, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.31.3.01-20.27.2.72-15.16.2.76-15.79.2.53-12.60.pth, bkmy
BLEU = 5.92, 24.5/9.5/3.7/1.4 (BP=1.000, ratio=1.494, hyp_len=18274, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.32.2.98-19.67.2.67-14.42.2.76-15.79.2.53-12.55.pth, mybk
BLEU = 3.58, 15.7/5.3/2.1/0.9 (BP=1.000, ratio=1.997, hyp_len=22829, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.32.2.98-19.67.2.67-14.42.2.76-15.79.2.53-12.55.pth, bkmy
BLEU = 8.45, 34.5/13.5/5.3/2.1 (BP=1.000, ratio=1.085, hyp_len=13272, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.33.2.91-18.37.2.63-13.82.2.71-15.10.2.49-12.11.pth, mybk
BLEU = 5.87, 24.6/8.5/3.6/1.6 (BP=1.000, ratio=1.322, hyp_len=15114, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.33.2.91-18.37.2.63-13.82.2.71-15.10.2.49-12.11.pth, bkmy
BLEU = 8.99, 34.5/14.0/5.8/2.3 (BP=1.000, ratio=1.112, hyp_len=13604, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.34.2.85-17.30.2.55-12.77.2.69-14.71.2.45-11.58.pth, mybk
BLEU = 6.72, 28.3/9.9/4.1/1.8 (BP=1.000, ratio=1.159, hyp_len=13244, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.34.2.85-17.30.2.55-12.77.2.69-14.71.2.45-11.58.pth, bkmy
BLEU = 9.65, 36.4/14.8/6.2/2.6 (BP=1.000, ratio=1.046, hyp_len=12798, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.35.2.78-16.18.2.48-11.89.2.70-14.84.2.45-11.58.pth, mybk
BLEU = 7.13, 28.9/10.1/4.4/2.0 (BP=1.000, ratio=1.141, hyp_len=13039, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.35.2.78-16.18.2.48-11.89.2.70-14.84.2.45-11.58.pth, bkmy
BLEU = 9.85, 36.8/14.9/6.4/2.7 (BP=1.000, ratio=1.039, hyp_len=12712, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.36.2.81-16.55.2.48-11.97.2.67-14.43.2.43-11.34.pth, mybk
BLEU = 7.42, 30.4/10.7/4.5/2.0 (BP=1.000, ratio=1.100, hyp_len=12580, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.36.2.81-16.55.2.48-11.97.2.67-14.43.2.43-11.34.pth, bkmy
BLEU = 10.13, 36.3/15.4/6.7/2.8 (BP=1.000, ratio=1.078, hyp_len=13191, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.37.2.76-15.84.2.43-11.41.2.68-14.57.2.44-11.52.pth, mybk
BLEU = 7.43, 29.9/10.7/4.5/2.1 (BP=1.000, ratio=1.123, hyp_len=12842, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.37.2.76-15.84.2.43-11.41.2.68-14.57.2.44-11.52.pth, bkmy
BLEU = 9.65, 36.2/15.0/6.3/2.6 (BP=1.000, ratio=1.097, hyp_len=13418, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.38.2.77-16.01.2.48-11.98.2.68-14.64.2.43-11.36.pth, mybk
BLEU = 7.31, 29.4/10.6/4.5/2.0 (BP=1.000, ratio=1.159, hyp_len=13244, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.38.2.77-16.01.2.48-11.98.2.68-14.64.2.43-11.36.pth, bkmy
BLEU = 9.64, 36.2/15.0/6.3/2.5 (BP=1.000, ratio=1.099, hyp_len=13446, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.39.2.66-14.29.2.35-10.44.2.68-14.52.2.40-11.05.pth, mybk
BLEU = 8.03, 30.7/11.5/5.0/2.4 (BP=1.000, ratio=1.139, hyp_len=13021, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.39.2.66-14.29.2.35-10.44.2.68-14.52.2.40-11.05.pth, bkmy
BLEU = 10.40, 37.3/15.6/6.9/2.9 (BP=1.000, ratio=1.054, hyp_len=12895, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.40.2.67-14.39.2.35-10.47.2.65-14.17.2.39-10.95.pth, mybk
BLEU = 8.02, 30.5/11.4/5.0/2.4 (BP=1.000, ratio=1.133, hyp_len=12956, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.40.2.67-14.39.2.35-10.47.2.65-14.17.2.39-10.95.pth, bkmy
BLEU = 10.75, 38.6/16.3/7.1/3.0 (BP=1.000, ratio=1.052, hyp_len=12862, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.41.2.60-13.53.2.32-10.14.2.64-14.01.2.40-10.97.pth, mybk
BLEU = 8.38, 31.9/11.8/5.3/2.5 (BP=1.000, ratio=1.096, hyp_len=12528, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.41.2.60-13.53.2.32-10.14.2.64-14.01.2.40-10.97.pth, bkmy
BLEU = 10.67, 38.3/16.1/7.0/3.0 (BP=1.000, ratio=1.070, hyp_len=13089, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.42.2.55-12.77.2.24-9.39.2.62-13.69.2.37-10.74.pth, mybk
BLEU = 8.02, 31.0/11.5/5.1/2.3 (BP=1.000, ratio=1.131, hyp_len=12932, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.42.2.55-12.77.2.24-9.39.2.62-13.69.2.37-10.74.pth, bkmy
BLEU = 10.75, 38.8/16.3/7.0/3.0 (BP=1.000, ratio=1.060, hyp_len=12970, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.43.2.56-12.99.2.25-9.51.2.62-13.76.2.39-10.91.pth, mybk
BLEU = 8.70, 32.0/12.3/5.5/2.6 (BP=1.000, ratio=1.116, hyp_len=12754, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.43.2.56-12.99.2.25-9.51.2.62-13.76.2.39-10.91.pth, bkmy
BLEU = 10.80, 38.1/16.0/7.1/3.1 (BP=1.000, ratio=1.091, hyp_len=13349, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.44.2.49-12.06.2.18-8.85.2.62-13.68.2.32-10.21.pth, mybk
BLEU = 8.83, 32.2/12.3/5.7/2.7 (BP=1.000, ratio=1.123, hyp_len=12836, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.44.2.49-12.06.2.18-8.85.2.62-13.68.2.32-10.21.pth, bkmy
BLEU = 11.80, 39.9/17.3/7.9/3.6 (BP=1.000, ratio=1.052, hyp_len=12870, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.45.2.46-11.66.2.14-8.53.2.64-14.00.2.37-10.65.pth, mybk
BLEU = 8.82, 32.1/12.4/5.6/2.7 (BP=1.000, ratio=1.120, hyp_len=12799, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.45.2.46-11.66.2.14-8.53.2.64-14.00.2.37-10.65.pth, bkmy
BLEU = 10.93, 37.8/16.3/7.3/3.2 (BP=1.000, ratio=1.098, hyp_len=13432, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.46.2.46-11.76.2.16-8.65.2.59-13.38.2.35-10.53.pth, mybk
BLEU = 8.74, 32.2/12.5/5.7/2.5 (BP=1.000, ratio=1.115, hyp_len=12749, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.46.2.46-11.76.2.16-8.65.2.59-13.38.2.35-10.53.pth, bkmy
BLEU = 11.30, 38.5/16.6/7.5/3.4 (BP=1.000, ratio=1.090, hyp_len=13327, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.47.2.52-12.42.2.25-9.46.2.59-13.36.2.35-10.51.pth, mybk
BLEU = 9.43, 34.4/13.5/6.1/2.8 (BP=1.000, ratio=1.071, hyp_len=12247, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.47.2.52-12.42.2.25-9.46.2.59-13.36.2.35-10.51.pth, bkmy
BLEU = 11.78, 39.8/17.4/7.8/3.5 (BP=1.000, ratio=1.068, hyp_len=13067, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.48.2.43-11.36.2.15-8.60.2.63-13.85.2.33-10.33.pth, mybk
BLEU = 8.47, 31.7/12.1/5.3/2.5 (BP=1.000, ratio=1.161, hyp_len=13267, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.48.2.43-11.36.2.15-8.60.2.63-13.85.2.33-10.33.pth, bkmy
BLEU = 11.19, 38.3/16.8/7.5/3.2 (BP=1.000, ratio=1.110, hyp_len=13580, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.49.2.43-11.38.2.13-8.39.2.58-13.25.2.33-10.28.pth, mybk
BLEU = 9.51, 33.4/13.3/6.2/3.0 (BP=1.000, ratio=1.107, hyp_len=12653, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.49.2.43-11.38.2.13-8.39.2.58-13.25.2.33-10.28.pth, bkmy
BLEU = 11.11, 38.1/16.5/7.4/3.3 (BP=1.000, ratio=1.102, hyp_len=13483, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.50.2.38-10.79.2.07-7.91.2.59-13.38.2.33-10.32.pth, mybk
BLEU = 9.00, 33.0/12.7/5.7/2.8 (BP=1.000, ratio=1.130, hyp_len=12920, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.50.2.38-10.79.2.07-7.91.2.59-13.38.2.33-10.32.pth, bkmy
BLEU = 11.94, 39.6/17.3/8.0/3.7 (BP=1.000, ratio=1.081, hyp_len=13223, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.51.2.34-10.34.2.02-7.55.2.61-13.54.2.35-10.45.pth, mybk
BLEU = 9.20, 32.8/12.8/6.0/2.9 (BP=1.000, ratio=1.129, hyp_len=12905, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.51.2.34-10.34.2.02-7.55.2.61-13.54.2.35-10.45.pth, bkmy
BLEU = 11.71, 39.6/17.2/7.8/3.5 (BP=1.000, ratio=1.065, hyp_len=13023, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.52.2.31-10.08.2.03-7.59.2.57-13.01.2.32-10.19.pth, mybk
BLEU = 9.34, 34.3/13.3/5.9/2.8 (BP=1.000, ratio=1.092, hyp_len=12480, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.52.2.31-10.08.2.03-7.59.2.57-13.01.2.32-10.19.pth, bkmy
BLEU = 12.42, 40.2/18.1/8.3/3.9 (BP=1.000, ratio=1.083, hyp_len=13246, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.53.2.27-9.70.1.97-7.16.2.56-13.00.2.34-10.38.pth, mybk
BLEU = 9.76, 34.7/13.6/6.3/3.1 (BP=1.000, ratio=1.066, hyp_len=12190, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.53.2.27-9.70.1.97-7.16.2.56-13.00.2.34-10.38.pth, bkmy
BLEU = 12.54, 40.0/18.0/8.5/4.1 (BP=1.000, ratio=1.104, hyp_len=13498, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.54.2.29-9.83.2.04-7.70.2.59-13.27.2.33-10.23.pth, mybk
BLEU = 9.37, 32.6/13.1/6.1/3.0 (BP=1.000, ratio=1.152, hyp_len=13175, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.54.2.29-9.83.2.04-7.70.2.59-13.27.2.33-10.23.pth, bkmy
BLEU = 11.77, 39.1/17.5/8.0/3.5 (BP=1.000, ratio=1.116, hyp_len=13645, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.55.2.25-9.52.1.96-7.11.2.60-13.49.2.33-10.28.pth, mybk
BLEU = 10.06, 35.4/14.1/6.5/3.2 (BP=1.000, ratio=1.078, hyp_len=12327, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.55.2.25-9.52.1.96-7.11.2.60-13.49.2.33-10.28.pth, bkmy
BLEU = 12.37, 39.9/17.8/8.3/4.0 (BP=1.000, ratio=1.093, hyp_len=13368, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.56.2.21-9.13.1.88-6.57.2.59-13.27.2.31-10.05.pth, mybk
BLEU = 9.39, 32.9/13.0/6.2/3.0 (BP=1.000, ratio=1.161, hyp_len=13270, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.56.2.21-9.13.1.88-6.57.2.59-13.27.2.31-10.05.pth, bkmy
BLEU = 12.39, 40.4/18.0/8.4/3.9 (BP=1.000, ratio=1.077, hyp_len=13175, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.57.2.28-9.78.2.00-7.36.2.57-13.01.2.31-10.04.pth, mybk
BLEU = 9.63, 33.6/13.5/6.2/3.0 (BP=1.000, ratio=1.128, hyp_len=12892, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.57.2.28-9.78.2.00-7.36.2.57-13.01.2.31-10.04.pth, bkmy
BLEU = 12.94, 40.9/18.6/8.9/4.2 (BP=1.000, ratio=1.068, hyp_len=13067, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.58.2.21-9.15.1.91-6.76.2.58-13.25.2.32-10.19.pth, mybk
BLEU = 9.83, 34.0/13.7/6.5/3.1 (BP=1.000, ratio=1.126, hyp_len=12870, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.58.2.21-9.15.1.91-6.76.2.58-13.25.2.32-10.19.pth, bkmy
BLEU = 12.60, 40.7/18.1/8.5/4.0 (BP=1.000, ratio=1.055, hyp_len=12904, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.59.2.13-8.38.1.83-6.21.2.58-13.19.2.31-10.07.pth, mybk
BLEU = 9.75, 34.3/13.4/6.3/3.1 (BP=1.000, ratio=1.106, hyp_len=12639, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.59.2.13-8.38.1.83-6.21.2.58-13.19.2.31-10.07.pth, bkmy
BLEU = 12.35, 40.1/17.9/8.2/4.0 (BP=1.000, ratio=1.107, hyp_len=13543, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.60.2.13-8.38.1.82-6.19.2.60-13.47.2.29-9.89.pth, mybk
BLEU = 9.47, 32.7/13.0/6.2/3.1 (BP=1.000, ratio=1.172, hyp_len=13398, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.60.2.13-8.38.1.82-6.19.2.60-13.47.2.29-9.89.pth, bkmy
BLEU = 13.20, 41.0/18.8/9.0/4.4 (BP=1.000, ratio=1.067, hyp_len=13048, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.61.2.06-7.82.1.80-6.02.2.61-13.56.2.33-10.24.pth, mybk
BLEU = 10.11, 34.6/14.0/6.5/3.3 (BP=1.000, ratio=1.104, hyp_len=12616, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.61.2.06-7.82.1.80-6.02.2.61-13.56.2.33-10.24.pth, bkmy
BLEU = 12.87, 40.5/18.5/8.8/4.2 (BP=1.000, ratio=1.102, hyp_len=13479, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.62.2.08-8.03.1.79-6.00.2.58-13.23.2.29-9.91.pth, mybk
BLEU = 9.73, 33.8/13.5/6.3/3.1 (BP=1.000, ratio=1.125, hyp_len=12860, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.62.2.08-8.03.1.79-6.00.2.58-13.23.2.29-9.91.pth, bkmy
BLEU = 12.53, 40.1/18.3/8.5/3.9 (BP=1.000, ratio=1.098, hyp_len=13435, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.63.2.12-8.36.1.80-6.07.2.57-13.05.2.32-10.14.pth, mybk
BLEU = 10.33, 35.5/14.3/6.7/3.4 (BP=1.000, ratio=1.076, hyp_len=12306, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.63.2.12-8.36.1.80-6.07.2.57-13.05.2.32-10.14.pth, bkmy
BLEU = 12.64, 40.4/18.2/8.5/4.1 (BP=1.000, ratio=1.102, hyp_len=13480, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.64.2.01-7.43.1.72-5.57.2.55-12.78.2.30-9.97.pth, mybk
BLEU = 10.04, 35.4/14.1/6.5/3.2 (BP=1.000, ratio=1.085, hyp_len=12408, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.64.2.01-7.43.1.72-5.57.2.55-12.78.2.30-9.97.pth, bkmy
BLEU = 13.12, 41.4/18.9/8.9/4.3 (BP=1.000, ratio=1.074, hyp_len=13141, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.65.2.08-7.98.1.77-5.90.2.57-13.02.2.30-9.97.pth, mybk
BLEU = 10.56, 34.8/14.4/7.0/3.6 (BP=1.000, ratio=1.098, hyp_len=12558, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.65.2.08-7.98.1.77-5.90.2.57-13.02.2.30-9.97.pth, bkmy
BLEU = 12.81, 40.8/18.5/8.7/4.1 (BP=1.000, ratio=1.085, hyp_len=13273, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.66.2.02-7.57.1.73-5.63.2.55-12.83.2.32-10.19.pth, mybk
BLEU = 10.41, 35.8/14.4/6.7/3.4 (BP=1.000, ratio=1.075, hyp_len=12291, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.66.2.02-7.57.1.73-5.63.2.55-12.83.2.32-10.19.pth, bkmy
BLEU = 12.96, 41.3/18.6/8.8/4.2 (BP=1.000, ratio=1.068, hyp_len=13063, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.67.2.01-7.48.1.74-5.73.2.58-13.20.2.28-9.82.pth, mybk
BLEU = 10.74, 35.8/14.8/7.0/3.6 (BP=1.000, ratio=1.067, hyp_len=12200, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.67.2.01-7.48.1.74-5.73.2.58-13.20.2.28-9.82.pth, bkmy
BLEU = 12.67, 40.2/18.4/8.6/4.1 (BP=1.000, ratio=1.117, hyp_len=13668, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.68.1.97-7.16.1.66-5.27.2.58-13.19.2.28-9.81.pth, mybk
BLEU = 9.65, 34.0/13.5/6.2/3.0 (BP=1.000, ratio=1.129, hyp_len=12908, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.68.1.97-7.16.1.66-5.27.2.58-13.19.2.28-9.81.pth, bkmy
BLEU = 13.43, 41.8/19.3/9.2/4.4 (BP=1.000, ratio=1.067, hyp_len=13056, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.69.1.91-6.78.1.63-5.12.2.61-13.55.2.30-9.93.pth, mybk
BLEU = 9.98, 33.4/13.5/6.5/3.4 (BP=1.000, ratio=1.161, hyp_len=13275, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.69.1.91-6.78.1.63-5.12.2.61-13.55.2.30-9.93.pth, bkmy
BLEU = 13.42, 41.2/18.9/9.2/4.5 (BP=1.000, ratio=1.090, hyp_len=13329, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.70.1.91-6.73.1.60-4.97.2.61-13.53.2.32-10.16.pth, mybk
BLEU = 10.33, 35.1/14.1/6.6/3.5 (BP=1.000, ratio=1.096, hyp_len=12534, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.70.1.91-6.73.1.60-4.97.2.61-13.53.2.32-10.16.pth, bkmy
BLEU = 13.51, 41.9/19.3/9.3/4.4 (BP=1.000, ratio=1.071, hyp_len=13104, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.71.1.90-6.67.1.59-4.92.2.58-13.15.2.28-9.81.pth, mybk
BLEU = 10.52, 36.8/14.5/6.8/3.4 (BP=1.000, ratio=1.053, hyp_len=12041, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.71.1.90-6.67.1.59-4.92.2.58-13.15.2.28-9.81.pth, bkmy
BLEU = 13.59, 41.8/19.3/9.4/4.5 (BP=1.000, ratio=1.080, hyp_len=13207, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.72.1.91-6.72.1.60-4.97.2.60-13.40.2.32-10.14.pth, mybk
BLEU = 10.70, 35.6/14.6/7.0/3.6 (BP=1.000, ratio=1.103, hyp_len=12611, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.72.1.91-6.72.1.60-4.97.2.60-13.40.2.32-10.14.pth, bkmy
BLEU = 13.22, 40.9/18.7/9.1/4.4 (BP=1.000, ratio=1.104, hyp_len=13500, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.73.1.92-6.85.1.62-5.07.2.62-13.70.2.31-10.08.pth, mybk
BLEU = 10.68, 35.3/14.5/7.0/3.6 (BP=1.000, ratio=1.102, hyp_len=12597, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.73.1.92-6.85.1.62-5.07.2.62-13.70.2.31-10.08.pth, bkmy
BLEU = 12.76, 40.2/18.5/8.7/4.1 (BP=1.000, ratio=1.113, hyp_len=13614, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.74.1.84-6.31.1.54-4.68.2.65-14.12.2.30-9.93.pth, mybk
BLEU = 10.18, 35.2/13.9/6.6/3.3 (BP=1.000, ratio=1.094, hyp_len=12511, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.74.1.84-6.31.1.54-4.68.2.65-14.12.2.30-9.93.pth, bkmy
BLEU = 13.44, 41.6/19.2/9.2/4.5 (BP=1.000, ratio=1.058, hyp_len=12939, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.75.1.91-6.74.1.65-5.18.2.61-13.59.2.32-10.13.pth, mybk
BLEU = 10.70, 36.0/14.7/7.0/3.5 (BP=1.000, ratio=1.074, hyp_len=12273, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.75.1.91-6.74.1.65-5.18.2.61-13.59.2.32-10.13.pth, bkmy
BLEU = 13.43, 41.2/19.0/9.2/4.5 (BP=1.000, ratio=1.094, hyp_len=13386, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.76.1.81-6.11.1.52-4.59.2.61-13.61.2.30-9.95.pth, mybk
BLEU = 10.71, 36.4/14.6/6.9/3.6 (BP=1.000, ratio=1.082, hyp_len=12374, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.76.1.81-6.11.1.52-4.59.2.61-13.61.2.30-9.95.pth, bkmy
BLEU = 13.22, 41.8/19.0/9.0/4.3 (BP=1.000, ratio=1.068, hyp_len=13065, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.77.1.79-5.96.1.50-4.46.2.63-13.85.2.29-9.92.pth, mybk
BLEU = 10.79, 36.0/14.7/7.0/3.6 (BP=1.000, ratio=1.068, hyp_len=12207, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.77.1.79-5.96.1.50-4.46.2.63-13.85.2.29-9.92.pth, bkmy
BLEU = 14.06, 41.9/19.4/9.7/4.9 (BP=1.000, ratio=1.080, hyp_len=13207, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.78.1.77-5.87.1.49-4.45.2.62-13.78.2.34-10.33.pth, mybk
BLEU = 11.13, 36.9/15.0/7.3/3.8 (BP=1.000, ratio=1.068, hyp_len=12211, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.78.1.77-5.87.1.49-4.45.2.62-13.78.2.34-10.33.pth, bkmy
BLEU = 13.74, 41.6/19.3/9.4/4.7 (BP=1.000, ratio=1.087, hyp_len=13297, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.79.1.72-5.56.1.43-4.17.2.61-13.63.2.33-10.33.pth, mybk
BLEU = 11.11, 36.7/15.1/7.3/3.8 (BP=1.000, ratio=1.088, hyp_len=12434, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.79.1.72-5.56.1.43-4.17.2.61-13.63.2.33-10.33.pth, bkmy
BLEU = 14.39, 42.4/20.1/10.0/5.0 (BP=1.000, ratio=1.077, hyp_len=13169, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.80.1.79-6.01.1.53-4.62.2.63-13.82.2.33-10.33.pth, mybk
BLEU = 10.76, 36.5/14.7/7.1/3.5 (BP=1.000, ratio=1.072, hyp_len=12254, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.80.1.79-6.01.1.53-4.62.2.63-13.82.2.33-10.33.pth, bkmy
BLEU = 13.72, 41.8/19.4/9.6/4.6 (BP=1.000, ratio=1.085, hyp_len=13271, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.81.1.82-6.17.1.54-4.68.2.63-13.87.2.33-10.30.pth, mybk
BLEU = 10.77, 36.6/15.2/7.1/3.4 (BP=1.000, ratio=1.079, hyp_len=12331, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.81.1.82-6.17.1.54-4.68.2.63-13.87.2.33-10.30.pth, bkmy
BLEU = 14.08, 42.4/19.6/9.6/4.9 (BP=1.000, ratio=1.069, hyp_len=13077, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.82.1.75-5.78.1.43-4.19.2.62-13.77.2.33-10.29.pth, mybk
BLEU = 10.64, 36.3/14.6/6.9/3.5 (BP=1.000, ratio=1.094, hyp_len=12508, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.82.1.75-5.78.1.43-4.19.2.62-13.77.2.33-10.29.pth, bkmy
BLEU = 14.22, 42.2/19.9/9.8/4.9 (BP=1.000, ratio=1.072, hyp_len=13115, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.83.1.68-5.38.1.41-4.08.2.67-14.38.2.32-10.16.pth, mybk
BLEU = 11.03, 36.5/15.1/7.3/3.7 (BP=1.000, ratio=1.081, hyp_len=12354, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.83.1.68-5.38.1.41-4.08.2.67-14.38.2.32-10.16.pth, bkmy
BLEU = 14.35, 42.2/19.8/9.9/5.1 (BP=1.000, ratio=1.079, hyp_len=13200, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.84.1.71-5.55.1.42-4.15.2.66-14.25.2.31-10.07.pth, mybk
BLEU = 10.92, 36.6/14.9/7.1/3.7 (BP=1.000, ratio=1.082, hyp_len=12365, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.84.1.71-5.55.1.42-4.15.2.66-14.25.2.31-10.07.pth, bkmy
BLEU = 14.70, 42.7/20.2/10.3/5.3 (BP=1.000, ratio=1.067, hyp_len=13045, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.85.1.67-5.32.1.40-4.07.2.66-14.37.2.34-10.33.pth, mybk
BLEU = 11.16, 36.4/15.0/7.3/3.9 (BP=1.000, ratio=1.081, hyp_len=12358, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.85.1.67-5.32.1.40-4.07.2.66-14.37.2.34-10.33.pth, bkmy
BLEU = 14.16, 42.6/19.7/9.8/4.9 (BP=1.000, ratio=1.089, hyp_len=13316, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.86.1.71-5.55.1.46-4.31.2.64-14.00.2.32-10.14.pth, mybk
BLEU = 10.67, 35.2/14.5/7.0/3.6 (BP=1.000, ratio=1.109, hyp_len=12673, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.86.1.71-5.55.1.46-4.31.2.64-14.00.2.32-10.14.pth, bkmy
BLEU = 14.13, 42.3/19.7/9.7/4.9 (BP=1.000, ratio=1.087, hyp_len=13289, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.87.1.67-5.30.1.37-3.93.2.65-14.14.2.30-9.97.pth, mybk
BLEU = 10.69, 35.9/14.6/7.0/3.5 (BP=1.000, ratio=1.086, hyp_len=12419, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.87.1.67-5.30.1.37-3.93.2.65-14.14.2.30-9.97.pth, bkmy
BLEU = 13.98, 42.5/19.9/9.6/4.7 (BP=1.000, ratio=1.066, hyp_len=13038, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.88.1.67-5.29.1.34-3.82.2.64-14.02.2.32-10.22.pth, mybk
BLEU = 10.73, 36.1/14.4/7.0/3.6 (BP=1.000, ratio=1.074, hyp_len=12283, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.88.1.67-5.29.1.34-3.82.2.64-14.02.2.32-10.22.pth, bkmy
BLEU = 14.70, 42.5/20.2/10.2/5.3 (BP=1.000, ratio=1.084, hyp_len=13255, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.89.1.64-5.17.1.36-3.91.2.66-14.27.2.37-10.73.pth, mybk
BLEU = 11.13, 36.6/15.0/7.3/3.8 (BP=1.000, ratio=1.079, hyp_len=12335, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.89.1.64-5.17.1.36-3.91.2.66-14.27.2.37-10.73.pth, bkmy
BLEU = 14.32, 42.2/19.9/10.0/5.0 (BP=1.000, ratio=1.089, hyp_len=13321, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.90.1.61-5.00.1.31-3.70.2.65-14.22.2.32-10.13.pth, mybk
BLEU = 10.78, 35.9/14.6/7.0/3.7 (BP=1.000, ratio=1.110, hyp_len=12686, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.90.1.61-5.00.1.31-3.70.2.65-14.22.2.32-10.13.pth, bkmy
BLEU = 14.74, 43.0/20.4/10.3/5.2 (BP=1.000, ratio=1.066, hyp_len=13038, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.91.1.69-5.40.1.44-4.22.2.65-14.19.2.34-10.36.pth, mybk
BLEU = 10.57, 36.4/14.5/6.8/3.5 (BP=1.000, ratio=1.087, hyp_len=12423, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.91.1.69-5.40.1.44-4.22.2.65-14.19.2.34-10.36.pth, bkmy
BLEU = 14.08, 42.4/19.5/9.6/4.9 (BP=1.000, ratio=1.071, hyp_len=13105, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.92.1.58-4.83.1.28-3.61.2.67-14.42.2.36-10.58.pth, mybk
BLEU = 10.98, 37.1/15.1/7.1/3.6 (BP=1.000, ratio=1.090, hyp_len=12458, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.92.1.58-4.83.1.28-3.61.2.67-14.42.2.36-10.58.pth, bkmy
BLEU = 13.91, 42.0/19.4/9.5/4.8 (BP=1.000, ratio=1.086, hyp_len=13286, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.93.1.58-4.87.1.28-3.60.2.69-14.78.2.37-10.69.pth, mybk
BLEU = 10.55, 35.9/14.5/6.9/3.5 (BP=1.000, ratio=1.096, hyp_len=12530, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.93.1.58-4.87.1.28-3.60.2.69-14.78.2.37-10.69.pth, bkmy
BLEU = 14.43, 42.3/19.9/10.0/5.1 (BP=1.000, ratio=1.083, hyp_len=13249, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.94.1.53-4.63.1.24-3.46.2.66-14.23.2.35-10.47.pth, mybk
BLEU = 10.24, 36.2/14.2/6.6/3.2 (BP=1.000, ratio=1.080, hyp_len=12348, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.94.1.53-4.63.1.24-3.46.2.66-14.23.2.35-10.47.pth, bkmy
BLEU = 14.96, 42.8/20.6/10.5/5.4 (BP=1.000, ratio=1.073, hyp_len=13126, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.95.1.62-5.07.1.26-3.54.2.73-15.35.2.31-10.10.pth, mybk
BLEU = 10.87, 36.5/15.0/7.1/3.6 (BP=1.000, ratio=1.080, hyp_len=12345, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.95.1.62-5.07.1.26-3.54.2.73-15.35.2.31-10.10.pth, bkmy
BLEU = 14.46, 42.5/20.1/10.1/5.1 (BP=1.000, ratio=1.076, hyp_len=13157, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.96.1.56-4.76.1.28-3.60.2.69-14.69.2.33-10.27.pth, mybk
BLEU = 10.88, 36.4/14.8/7.2/3.6 (BP=1.000, ratio=1.066, hyp_len=12183, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.96.1.56-4.76.1.28-3.60.2.69-14.69.2.33-10.27.pth, bkmy
BLEU = 14.43, 42.7/20.0/9.9/5.1 (BP=1.000, ratio=1.062, hyp_len=12991, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.97.1.52-4.56.1.23-3.41.2.70-14.94.2.35-10.48.pth, mybk
BLEU = 10.52, 36.6/14.6/6.9/3.3 (BP=1.000, ratio=1.072, hyp_len=12254, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.97.1.52-4.56.1.23-3.41.2.70-14.94.2.35-10.48.pth, bkmy
BLEU = 14.80, 42.7/20.2/10.3/5.4 (BP=1.000, ratio=1.072, hyp_len=13114, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.98.1.48-4.41.1.19-3.29.2.72-15.19.2.36-10.59.pth, mybk
BLEU = 10.73, 36.4/14.6/7.0/3.6 (BP=1.000, ratio=1.075, hyp_len=12288, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.98.1.48-4.41.1.19-3.29.2.72-15.19.2.36-10.59.pth, bkmy
BLEU = 14.38, 42.3/19.9/10.0/5.1 (BP=1.000, ratio=1.062, hyp_len=12984, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.99.1.49-4.44.1.23-3.44.2.74-15.48.2.35-10.52.pth, mybk
BLEU = 11.36, 37.5/15.4/7.5/3.8 (BP=1.000, ratio=1.057, hyp_len=12078, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.99.1.49-4.44.1.23-3.44.2.74-15.48.2.35-10.52.pth, bkmy
BLEU = 14.48, 42.9/20.3/10.0/5.1 (BP=1.000, ratio=1.070, hyp_len=13087, ref_len=12231)
==========
```

Seq2Seq-DSL ကို epoch 30 ကနေ epoch 100 အထိ training လုပ်တာ စုစုပေါင်းကြာချိန်က အောက်ပါအတိုင်း...  

```
real	326m39.893s
user	316m30.512s
sys	22m20.539s
```

Best BLEU Score for mybk, 100 epoch: 11.36  
Best BLEU Score for bkmy,94 epoch: 14.96  

## Transformer-DSL for my-bk

command:  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./dsl-transformer-train-loop-mybk.sh | tee ./model/dsl/transformer/dsl-transformer-train-mybk.log
```

### Transformer-DSL, 30 epoch

```
training start for 30 epochs...
{   'batch_size': 64,
    'dropout': 0.2,
    'dsl_lambda': 0.01,
    'dsl_n_warmup_epochs': 20,
    'gpu_id': 1,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'mybk',
    'lm_fn': './model/lm/mybk/lm-200epoch-mybk.pth',
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/dsl/transformer/mybk-30epoch/dsl-model-mybk.pth',
    'n_epochs': 30,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'train': '/home/ye/exp/simple-nmt/data/my-bk/syl/train',
    'use_transformer': True,
    'valid': '/home/ye/exp/simple-nmt/data/my-bk/syl/dev',
    'verbose': 2,
    'word_vec_size': 128}
[LanguageModel(
  (emb): Embedding(1470, 128, padding_idx=1)
  (rnn): LSTM(128, 128, num_layers=4, batch_first=True, dropout=0.2)
  (out): Linear(in_features=128, out_features=1470, bias=True)
  (log_softmax): LogSoftmax(dim=-1)
), LanguageModel(
  (emb): Embedding(1315, 128, padding_idx=1)
  (rnn): LSTM(128, 128, num_layers=4, batch_first=True, dropout=0.2)
  (out): Linear(in_features=128, out_features=1315, bias=True)
  (log_softmax): LogSoftmax(dim=-1)
)]
[Transformer(
  (emb_enc): Embedding(1315, 128)
  (emb_dec): Embedding(1470, 128)
  (emb_dropout): Dropout(p=0.2, inplace=False)
  (encoder): MySequential(
    (0): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=128, out_features=512, bias=True)
        (1): ReLU()
        (2): Linear(in_features=512, out_features=128, bias=True)
      )
      (fc_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (1): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=128, out_features=512, bias=True)
        (1): ReLU()
        (2): Linear(in_features=512, out_features=128, bias=True)
      )
      (fc_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (2): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=128, out_features=512, bias=True)
        (1): ReLU()
        (2): Linear(in_features=512, out_features=128, bias=True)
      )
      (fc_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (3): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=128, out_features=512, bias=True)
        (1): ReLU()
        (2): Linear(in_features=512, out_features=128, bias=True)
      )
      (fc_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
  )
  (decoder): MySequential(
    (0): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=128, out_features=512, bias=True)
        (1): ReLU()
        (2): Linear(in_features=512, out_features=128, bias=True)
      )
      (fc_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (1): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=128, out_features=512, bias=True)
        (1): ReLU()
        (2): Linear(in_features=512, out_features=128, bias=True)
      )
      (fc_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (2): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=128, out_features=512, bias=True)
        (1): ReLU()
        (2): Linear(in_features=512, out_features=128, bias=True)
      )
      (fc_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (3): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=128, out_features=512, bias=True)
        (1): ReLU()
        (2): Linear(in_features=512, out_features=128, bias=True)
      )
      (fc_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
  )
  (generator): Sequential(
    (0): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
    (1): Linear(in_features=128, out_features=1470, bias=True)
    (2): LogSoftmax(dim=-1)
  )
), Transformer(
  (emb_enc): Embedding(1470, 128)
  (emb_dec): Embedding(1315, 128)
  (emb_dropout): Dropout(p=0.2, inplace=False)
  (encoder): MySequential(
    (0): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=128, out_features=512, bias=True)
        (1): ReLU()
        (2): Linear(in_features=512, out_features=128, bias=True)
      )
      (fc_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (1): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=128, out_features=512, bias=True)
        (1): ReLU()
        (2): Linear(in_features=512, out_features=128, bias=True)
      )
      (fc_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (2): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=128, out_features=512, bias=True)
        (1): ReLU()
        (2): Linear(in_features=512, out_features=128, bias=True)
      )
      (fc_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (3): EncoderBlock(
      (attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=128, out_features=512, bias=True)
        (1): ReLU()
        (2): Linear(in_features=512, out_features=128, bias=True)
      )
      (fc_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
  )
  (decoder): MySequential(
    (0): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=128, out_features=512, bias=True)
        (1): ReLU()
        (2): Linear(in_features=512, out_features=128, bias=True)
      )
      (fc_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (1): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=128, out_features=512, bias=True)
        (1): ReLU()
        (2): Linear(in_features=512, out_features=128, bias=True)
      )
      (fc_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (2): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=128, out_features=512, bias=True)
        (1): ReLU()
        (2): Linear(in_features=512, out_features=128, bias=True)
      )
      (fc_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
    (3): DecoderBlock(
      (masked_attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (masked_attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (masked_attn_dropout): Dropout(p=0.2, inplace=False)
      (attn): MultiHead(
        (Q_linear): Linear(in_features=128, out_features=128, bias=False)
        (K_linear): Linear(in_features=128, out_features=128, bias=False)
        (V_linear): Linear(in_features=128, out_features=128, bias=False)
        (linear): Linear(in_features=128, out_features=128, bias=False)
        (attn): Attention(
          (softmax): Softmax(dim=-1)
        )
      )
      (attn_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn_dropout): Dropout(p=0.2, inplace=False)
      (fc): Sequential(
        (0): Linear(in_features=128, out_features=512, bias=True)
        (1): ReLU()
        (2): Linear(in_features=512, out_features=128, bias=True)
      )
      (fc_norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (fc_dropout): Dropout(p=0.2, inplace=False)
    )
  )
  (generator): Sequential(
    (0): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
    (1): Linear(in_features=128, out_features=1315, bias=True)
    (2): LogSoftmax(dim=-1)
  )
)]
[NLLLoss(), NLLLoss()]
[Adam (
Parameter Group 0
    amsgrad: False
    betas: (0.9, 0.98)
    eps: 1e-08
    lr: 0.001
    weight_decay: 0
), Adam (
Parameter Group 0
    amsgrad: False
    betas: (0.9, 0.98)
    eps: 1e-08
    lr: 0.001
    weight_decay: 0
)]
Epoch 1 - |param|=8.52e+02 |g_param|=1.75e+05 loss_x2y=4.4737e+00 ppl_x2y=87.68 loss_y2x=4.1175e+00 ppl_y2x=61.40 dual_loss=0.0000e+00
Validation X2Y - loss=3.6165e+00 ppl=37.21 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=3.2339e+00 ppl=25.38 best_loss=inf best_ppl=inf
Epoch 2 - |param|=8.53e+02 |g_param|=1.16e+05 loss_x2y=3.6604e+00 ppl_x2y=38.88 loss_y2x=3.2477e+00 ppl_y2x=25.73 dual_loss=0.0000e+00
Validation X2Y - loss=3.0161e+00 ppl=20.41 best_loss=3.6165e+00 best_ppl=37.21                                          
Validation Y2X - loss=2.7394e+00 ppl=15.48 best_loss=3.2339e+00 best_ppl=25.38
Epoch 3 - |param|=8.54e+02 |g_param|=9.91e+04 loss_x2y=3.3156e+00 ppl_x2y=27.54 loss_y2x=2.8553e+00 ppl_y2x=17.38 dual_loss=0.0000e+00
Validation X2Y - loss=2.6331e+00 ppl=13.92 best_loss=3.0161e+00 best_ppl=20.41                                          
Validation Y2X - loss=2.3706e+00 ppl=10.70 best_loss=2.7394e+00 best_ppl=15.48
Epoch 4 - |param|=8.54e+02 |g_param|=1.08e+05 loss_x2y=2.9864e+00 ppl_x2y=19.81 loss_y2x=2.5747e+00 ppl_y2x=13.13 dual_loss=0.0000e+00
Validation X2Y - loss=2.3515e+00 ppl=10.50 best_loss=2.6331e+00 best_ppl=13.92                                          
Validation Y2X - loss=2.0850e+00 ppl=8.04 best_loss=2.3706e+00 best_ppl=10.70
Epoch 5 - |param|=8.55e+02 |g_param|=1.12e+05 loss_x2y=2.7914e+00 ppl_x2y=16.30 loss_y2x=2.4194e+00 ppl_y2x=11.24 dual_loss=0.0000e+00
Validation X2Y - loss=2.0317e+00 ppl=7.63 best_loss=2.3515e+00 best_ppl=10.50                                           
Validation Y2X - loss=1.8657e+00 ppl=6.46 best_loss=2.0850e+00 best_ppl=8.04
Epoch 6 - |param|=8.56e+02 |g_param|=1.24e+05 loss_x2y=2.6962e+00 ppl_x2y=14.82 loss_y2x=2.3687e+00 ppl_y2x=10.68 dual_loss=0.0000e+00
Validation X2Y - loss=1.8607e+00 ppl=6.43 best_loss=2.0317e+00 best_ppl=7.63                                            
Validation Y2X - loss=1.6559e+00 ppl=5.24 best_loss=1.8657e+00 best_ppl=6.46
Epoch 7 - |param|=8.56e+02 |g_param|=1.17e+05 loss_x2y=2.4680e+00 ppl_x2y=11.80 loss_y2x=2.1421e+00 ppl_y2x=8.52 dual_loss=0.0000e+00
Validation X2Y - loss=1.7043e+00 ppl=5.50 best_loss=1.8607e+00 best_ppl=6.43                                            
Validation Y2X - loss=1.5433e+00 ppl=4.68 best_loss=1.6559e+00 best_ppl=5.24
Epoch 8 - |param|=8.57e+02 |g_param|=1.28e+05 loss_x2y=2.3293e+00 ppl_x2y=10.27 loss_y2x=2.0248e+00 ppl_y2x=7.57 dual_loss=0.0000e+00
Validation X2Y - loss=1.5793e+00 ppl=4.85 best_loss=1.7043e+00 best_ppl=5.50                                            
Validation Y2X - loss=1.4357e+00 ppl=4.20 best_loss=1.5433e+00 best_ppl=4.68
Epoch 9 - |param|=8.57e+02 |g_param|=1.28e+05 loss_x2y=2.2221e+00 ppl_x2y=9.23 loss_y2x=1.9209e+00 ppl_y2x=6.83 dual_loss=0.0000e+00
Validation X2Y - loss=1.4884e+00 ppl=4.43 best_loss=1.5793e+00 best_ppl=4.85                                            
Validation Y2X - loss=1.3627e+00 ppl=3.91 best_loss=1.4357e+00 best_ppl=4.20
Epoch 10 - |param|=8.58e+02 |g_param|=1.40e+05 loss_x2y=2.0692e+00 ppl_x2y=7.92 loss_y2x=1.7878e+00 ppl_y2x=5.98 dual_loss=0.0000e+00
Validation X2Y - loss=1.4418e+00 ppl=4.23 best_loss=1.4884e+00 best_ppl=4.43                                            
Validation Y2X - loss=1.2867e+00 ppl=3.62 best_loss=1.3627e+00 best_ppl=3.91
Epoch 11 - |param|=8.58e+02 |g_param|=1.38e+05 loss_x2y=2.0320e+00 ppl_x2y=7.63 loss_y2x=1.7584e+00 ppl_y2x=5.80 dual_loss=0.0000e+00
Validation X2Y - loss=1.3665e+00 ppl=3.92 best_loss=1.4418e+00 best_ppl=4.23                                            
Validation Y2X - loss=1.2075e+00 ppl=3.34 best_loss=1.2867e+00 best_ppl=3.62
Epoch 12 - |param|=8.59e+02 |g_param|=1.49e+05 loss_x2y=1.9650e+00 ppl_x2y=7.14 loss_y2x=1.6915e+00 ppl_y2x=5.43 dual_loss=0.0000e+00
Validation X2Y - loss=1.3282e+00 ppl=3.77 best_loss=1.3665e+00 best_ppl=3.92                                            
Validation Y2X - loss=1.1928e+00 ppl=3.30 best_loss=1.2075e+00 best_ppl=3.34
Epoch 13 - |param|=8.59e+02 |g_param|=1.48e+05 loss_x2y=1.8867e+00 ppl_x2y=6.60 loss_y2x=1.6274e+00 ppl_y2x=5.09 dual_loss=0.0000e+00
Validation X2Y - loss=1.3060e+00 ppl=3.69 best_loss=1.3282e+00 best_ppl=3.77                                            
Validation Y2X - loss=1.1430e+00 ppl=3.14 best_loss=1.1928e+00 best_ppl=3.30
Epoch 14 - |param|=8.60e+02 |g_param|=1.65e+05 loss_x2y=1.8588e+00 ppl_x2y=6.42 loss_y2x=1.5981e+00 ppl_y2x=4.94 dual_loss=0.0000e+00
Validation X2Y - loss=1.2770e+00 ppl=3.59 best_loss=1.3060e+00 best_ppl=3.69                                            
Validation Y2X - loss=1.1289e+00 ppl=3.09 best_loss=1.1430e+00 best_ppl=3.14
Epoch 15 - |param|=8.61e+02 |g_param|=1.55e+05 loss_x2y=1.7342e+00 ppl_x2y=5.66 loss_y2x=1.4930e+00 ppl_y2x=4.45 dual_loss=0.0000e+00
Validation X2Y - loss=1.2199e+00 ppl=3.39 best_loss=1.2770e+00 best_ppl=3.59                                            
Validation Y2X - loss=1.1066e+00 ppl=3.02 best_loss=1.1289e+00 best_ppl=3.09
Epoch 16 - |param|=8.61e+02 |g_param|=1.62e+05 loss_x2y=1.6940e+00 ppl_x2y=5.44 loss_y2x=1.4433e+00 ppl_y2x=4.23 dual_loss=0.0000e+00
Validation X2Y - loss=1.2272e+00 ppl=3.41 best_loss=1.2199e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.0837e+00 ppl=2.96 best_loss=1.1066e+00 best_ppl=3.02
Epoch 17 - |param|=8.62e+02 |g_param|=1.60e+05 loss_x2y=1.6811e+00 ppl_x2y=5.37 loss_y2x=1.4268e+00 ppl_y2x=4.17 dual_loss=0.0000e+00
Validation X2Y - loss=1.2527e+00 ppl=3.50 best_loss=1.2199e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1240e+00 ppl=3.08 best_loss=1.0837e+00 best_ppl=2.96
Epoch 18 - |param|=8.62e+02 |g_param|=1.61e+05 loss_x2y=1.6180e+00 ppl_x2y=5.04 loss_y2x=1.3771e+00 ppl_y2x=3.96 dual_loss=0.0000e+00
Validation X2Y - loss=1.2201e+00 ppl=3.39 best_loss=1.2199e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.0900e+00 ppl=2.97 best_loss=1.0837e+00 best_ppl=2.96
Epoch 19 - |param|=8.63e+02 |g_param|=1.67e+05 loss_x2y=1.5558e+00 ppl_x2y=4.74 loss_y2x=1.3331e+00 ppl_y2x=3.79 dual_loss=0.0000e+00
Validation X2Y - loss=1.2240e+00 ppl=3.40 best_loss=1.2199e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.0523e+00 ppl=2.86 best_loss=1.0837e+00 best_ppl=2.96
Epoch 20 - |param|=8.63e+02 |g_param|=1.86e+05 loss_x2y=1.5586e+00 ppl_x2y=4.75 loss_y2x=1.3415e+00 ppl_y2x=3.82 dual_loss=0.0000e+00
Validation X2Y - loss=1.1998e+00 ppl=3.32 best_loss=1.2199e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.0837e+00 ppl=2.96 best_loss=1.0523e+00 best_ppl=2.86
Epoch 21 - |param|=8.64e+02 |g_param|=1.68e+05 loss_x2y=1.4562e+00 ppl_x2y=4.29 loss_y2x=1.2490e+00 ppl_y2x=3.49 dual_loss=5.5847e-01
Validation X2Y - loss=1.1965e+00 ppl=3.31 best_loss=1.1998e+00 best_ppl=3.32                                            
Validation Y2X - loss=1.0506e+00 ppl=2.86 best_loss=1.0523e+00 best_ppl=2.86
Epoch 22 - |param|=8.64e+02 |g_param|=1.79e+05 loss_x2y=1.4372e+00 ppl_x2y=4.21 loss_y2x=1.2340e+00 ppl_y2x=3.43 dual_loss=5.2752e-01
Validation X2Y - loss=1.2499e+00 ppl=3.49 best_loss=1.1965e+00 best_ppl=3.31                                            
Validation Y2X - loss=1.0442e+00 ppl=2.84 best_loss=1.0506e+00 best_ppl=2.86
Epoch 23 - |param|=8.65e+02 |g_param|=1.76e+05 loss_x2y=1.4006e+00 ppl_x2y=4.06 loss_y2x=1.1989e+00 ppl_y2x=3.32 dual_loss=4.8967e-01
Validation X2Y - loss=1.2235e+00 ppl=3.40 best_loss=1.1965e+00 best_ppl=3.31                                            
Validation Y2X - loss=1.0714e+00 ppl=2.92 best_loss=1.0442e+00 best_ppl=2.84
Epoch 24 - |param|=8.65e+02 |g_param|=1.82e+05 loss_x2y=1.3735e+00 ppl_x2y=3.95 loss_y2x=1.1552e+00 ppl_y2x=3.17 dual_loss=4.7305e-01
Validation X2Y - loss=1.2328e+00 ppl=3.43 best_loss=1.1965e+00 best_ppl=3.31                                            
Validation Y2X - loss=1.0503e+00 ppl=2.86 best_loss=1.0442e+00 best_ppl=2.84
Epoch 25 - |param|=8.66e+02 |g_param|=1.82e+05 loss_x2y=1.4026e+00 ppl_x2y=4.07 loss_y2x=1.2139e+00 ppl_y2x=3.37 dual_loss=5.1799e-01
Validation X2Y - loss=1.2738e+00 ppl=3.57 best_loss=1.1965e+00 best_ppl=3.31                                            
Validation Y2X - loss=1.0825e+00 ppl=2.95 best_loss=1.0442e+00 best_ppl=2.84
Epoch 26 - |param|=8.67e+02 |g_param|=1.89e+05 loss_x2y=1.3758e+00 ppl_x2y=3.96 loss_y2x=1.1523e+00 ppl_y2x=3.17 dual_loss=5.1907e-01
Validation X2Y - loss=1.2376e+00 ppl=3.45 best_loss=1.1965e+00 best_ppl=3.31                                            
Validation Y2X - loss=1.0751e+00 ppl=2.93 best_loss=1.0442e+00 best_ppl=2.84
Epoch 27 - |param|=8.67e+02 |g_param|=1.86e+05 loss_x2y=1.2849e+00 ppl_x2y=3.61 loss_y2x=1.0840e+00 ppl_y2x=2.96 dual_loss=5.2175e-01
Validation X2Y - loss=1.2618e+00 ppl=3.53 best_loss=1.1965e+00 best_ppl=3.31                                            
Validation Y2X - loss=1.0906e+00 ppl=2.98 best_loss=1.0442e+00 best_ppl=2.84
Epoch 28 - |param|=8.68e+02 |g_param|=1.91e+05 loss_x2y=1.2238e+00 ppl_x2y=3.40 loss_y2x=1.0304e+00 ppl_y2x=2.80 dual_loss=4.9374e-01
Validation X2Y - loss=1.2721e+00 ppl=3.57 best_loss=1.1965e+00 best_ppl=3.31                                            
Validation Y2X - loss=1.0905e+00 ppl=2.98 best_loss=1.0442e+00 best_ppl=2.84
Epoch 29 - |param|=8.68e+02 |g_param|=1.83e+05 loss_x2y=1.2080e+00 ppl_x2y=3.35 loss_y2x=1.0020e+00 ppl_y2x=2.72 dual_loss=5.1693e-01
Validation X2Y - loss=1.2994e+00 ppl=3.67 best_loss=1.1965e+00 best_ppl=3.31                                            
Validation Y2X - loss=1.0874e+00 ppl=2.97 best_loss=1.0442e+00 best_ppl=2.84
Epoch 30 - |param|=8.69e+02 |g_param|=1.91e+05 loss_x2y=1.1662e+00 ppl_x2y=3.21 loss_y2x=9.7528e-01 ppl_y2x=2.65 dual_loss=5.1188e-01
Validation X2Y - loss=1.2558e+00 ppl=3.51 best_loss=1.1965e+00 best_ppl=3.31                                            
Validation Y2X - loss=1.0973e+00 ppl=3.00 best_loss=1.0442e+00 best_ppl=2.84

real	9m36.038s
user	9m22.930s
sys	0m12.151s
```

testing/evaluatin အတွက် update လုပ်ခဲ့တဲ့ shell script က အောက်ပါအတိုင်း...  

testing/evaluation ...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Last Updated: 25 Mar 2022
# find all models and parse to translate.py for testing and multi-bleu.perl for evaluation with BLEU score
# used for transformer-DSL evaluation for Myanmar-Beik pair

for folder in {mybk-30epoch,mybk-40epoch,mybk-50epoch,mybk-60epoch,mybk-70epoch,mybk-80epoch,mybk-90epoch,mybk-100epoch};
do
   cd ./model/dsl/transformer/${folder};
   pwd;
   for i in *.pth;
   do
      MODEL=$i;

      # Testing X-Y
      python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang mybk < /home/ye/exp/simple-nmt/data/my-bk/syl/test.my > $MODEL.mybk.hyp

      # Evaluation with BLEU Score
      echo "Evaluation result for the model: $MODEL, mybk" | tee -a eval-results-xy-transformer.txt;
      cat $MODEL.mybk.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/my-bk/syl/test.bk | tee  -a eval-results-xy-transformer.txt;

      # Testing Y-X
      python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang bkmy < /home/ye/exp/simple-nmt/data/my-bk/syl/test.bk > $MODEL.bkmy.hyp

      # Evaluation with BLEU Score
      echo "Evaluation result for the model: $MODEL, bkmy" | tee -a eval-results-yx-transformer.txt;
      cat $MODEL.bkmy.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/my-bk/syl/test.my | tee  -a eval-results-yx-transformer.txt;
   done
   cd ~/exp/simple-nmt/;
   echo "==========";
done
```

testing/evaluation အတွက် သုံးခဲ့တဲ့ command က အောက်ပါအတိုင်း...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time ./test-eval-loop-xy-transformer-mybk.sh | tee ./model/dsl/transformer/test-eval.log
```

30 epoch မော်ဒယ်အတွက် testing/evaluation ရလဒ်တွေက အောက်ပါအတိုင်း...  

```
/home/ye/exp/simple-nmt/model/dsl/transformer/mybk-30epoch
Evaluation result for the model: dsl-model-mybk.01.4.47-87.68.4.12-61.40.3.62-37.21.3.23-25.38.pth, mybk
BLEU = 2.92, 14.7/3.7/1.7/0.8 (BP=1.000, ratio=1.370, hyp_len=15663, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.47-87.68.4.12-61.40.3.62-37.21.3.23-25.38.pth, bkmy
BLEU = 4.39, 27.1/7.6/2.6/0.7 (BP=1.000, ratio=1.002, hyp_len=12254, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.02.3.66-38.88.3.25-25.73.3.02-20.41.2.74-15.48.pth, mybk
BLEU = 5.28, 23.0/7.0/3.0/1.6 (BP=1.000, ratio=1.051, hyp_len=12012, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.3.66-38.88.3.25-25.73.3.02-20.41.2.74-15.48.pth, bkmy
BLEU = 3.57, 18.4/6.3/2.1/0.7 (BP=1.000, ratio=1.669, hyp_len=20410, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.3.32-27.54.2.86-17.38.2.63-13.92.2.37-10.70.pth, mybk
BLEU = 6.26, 25.8/8.8/3.6/1.9 (BP=1.000, ratio=1.101, hyp_len=12587, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.3.32-27.54.2.86-17.38.2.63-13.92.2.37-10.70.pth, bkmy
BLEU = 3.48, 14.5/5.5/2.2/0.9 (BP=1.000, ratio=2.663, hyp_len=32567, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.2.99-19.81.2.57-13.13.2.35-10.50.2.09-8.04.pth, mybk
BLEU = 9.81, 32.6/13.2/6.6/3.3 (BP=1.000, ratio=1.116, hyp_len=12758, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.2.99-19.81.2.57-13.13.2.35-10.50.2.09-8.04.pth, bkmy
BLEU = 12.34, 39.5/17.7/8.4/3.9 (BP=1.000, ratio=1.080, hyp_len=13205, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.2.79-16.30.2.42-11.24.2.03-7.63.1.87-6.46.pth, mybk
BLEU = 13.70, 39.5/18.1/9.6/5.1 (BP=1.000, ratio=1.046, hyp_len=11953, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.2.79-16.30.2.42-11.24.2.03-7.63.1.87-6.46.pth, bkmy
BLEU = 16.73, 47.8/24.3/12.7/7.0 (BP=0.932, ratio=0.935, hyp_len=11432, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.2.70-14.82.2.37-10.68.1.86-6.43.1.66-5.24.pth, mybk
BLEU = 16.48, 42.0/20.8/11.9/7.1 (BP=1.000, ratio=1.064, hyp_len=12164, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.2.70-14.82.2.37-10.68.1.86-6.43.1.66-5.24.pth, bkmy
BLEU = 20.13, 49.1/26.3/14.7/8.7 (BP=1.000, ratio=1.021, hyp_len=12484, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.2.47-11.80.2.14-8.52.1.70-5.50.1.54-4.68.pth, mybk
BLEU = 19.54, 44.8/24.3/14.6/9.1 (BP=1.000, ratio=1.097, hyp_len=12537, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.2.47-11.80.2.14-8.52.1.70-5.50.1.54-4.68.pth, bkmy
BLEU = 23.90, 55.2/32.2/19.7/12.7 (BP=0.927, ratio=0.930, hyp_len=11369, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.2.33-10.27.2.02-7.57.1.58-4.85.1.44-4.20.pth, mybk
BLEU = 22.93, 49.9/28.1/17.3/11.4 (BP=1.000, ratio=1.029, hyp_len=11767, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.2.33-10.27.2.02-7.57.1.58-4.85.1.44-4.20.pth, bkmy
BLEU = 29.54, 59.5/37.5/24.7/16.9 (BP=0.950, ratio=0.952, hyp_len=11638, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.2.22-9.23.1.92-6.83.1.49-4.43.1.36-3.91.pth, mybk
BLEU = 21.95, 47.6/26.8/16.6/11.0 (BP=1.000, ratio=1.096, hyp_len=12526, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.2.22-9.23.1.92-6.83.1.49-4.43.1.36-3.91.pth, bkmy
BLEU = 30.18, 57.0/36.0/24.0/16.9 (BP=1.000, ratio=1.025, hyp_len=12534, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.2.07-7.92.1.79-5.98.1.44-4.23.1.29-3.62.pth, mybk
BLEU = 23.53, 48.3/28.2/18.3/12.3 (BP=1.000, ratio=1.119, hyp_len=12790, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.2.07-7.92.1.79-5.98.1.44-4.23.1.29-3.62.pth, bkmy
BLEU = 32.94, 62.1/40.5/27.5/20.0 (BP=0.960, ratio=0.961, hyp_len=11748, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.2.03-7.63.1.76-5.80.1.37-3.92.1.21-3.34.pth, mybk
BLEU = 26.04, 52.4/31.3/20.3/13.8 (BP=1.000, ratio=1.083, hyp_len=12376, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.2.03-7.63.1.76-5.80.1.37-3.92.1.21-3.34.pth, bkmy
BLEU = 35.10, 62.2/41.4/28.6/20.7 (BP=1.000, ratio=1.033, hyp_len=12637, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.1.97-7.14.1.69-5.43.1.33-3.77.1.19-3.30.pth, mybk
BLEU = 29.43, 56.7/34.9/23.3/16.3 (BP=1.000, ratio=1.036, hyp_len=11844, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.1.97-7.14.1.69-5.43.1.33-3.77.1.19-3.30.pth, bkmy
BLEU = 32.45, 57.4/38.3/26.6/18.9 (BP=1.000, ratio=1.157, hyp_len=14146, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.1.89-6.60.1.63-5.09.1.31-3.69.1.14-3.14.pth, mybk
BLEU = 26.20, 51.3/31.1/20.6/14.3 (BP=1.000, ratio=1.150, hyp_len=13143, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.1.89-6.60.1.63-5.09.1.31-3.69.1.14-3.14.pth, bkmy
BLEU = 35.58, 61.1/41.4/29.3/21.6 (BP=1.000, ratio=1.063, hyp_len=12996, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.1.86-6.42.1.60-4.94.1.28-3.59.1.13-3.09.pth, mybk
BLEU = 30.06, 57.3/35.6/24.0/16.7 (BP=1.000, ratio=1.054, hyp_len=12055, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.1.86-6.42.1.60-4.94.1.28-3.59.1.13-3.09.pth, bkmy
BLEU = 38.30, 64.9/44.5/31.7/23.5 (BP=1.000, ratio=1.018, hyp_len=12448, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.1.73-5.66.1.49-4.45.1.22-3.39.1.11-3.02.pth, mybk
BLEU = 31.46, 59.2/37.3/25.1/17.7 (BP=1.000, ratio=1.032, hyp_len=11796, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.1.73-5.66.1.49-4.45.1.22-3.39.1.11-3.02.pth, bkmy
BLEU = 38.16, 64.1/44.3/31.6/23.6 (BP=1.000, ratio=1.047, hyp_len=12803, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.1.69-5.44.1.44-4.23.1.23-3.41.1.08-2.96.pth, mybk
BLEU = 30.84, 58.1/36.8/24.6/17.2 (BP=1.000, ratio=1.086, hyp_len=12420, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.1.69-5.44.1.44-4.23.1.23-3.41.1.08-2.96.pth, bkmy
BLEU = 39.20, 65.1/45.3/32.7/24.5 (BP=1.000, ratio=1.031, hyp_len=12608, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.1.68-5.37.1.43-4.17.1.25-3.50.1.12-3.08.pth, mybk
BLEU = 31.47, 59.1/37.1/25.1/17.9 (BP=1.000, ratio=1.058, hyp_len=12091, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.1.68-5.37.1.43-4.17.1.25-3.50.1.12-3.08.pth, bkmy
BLEU = 39.07, 65.7/45.2/32.3/24.3 (BP=1.000, ratio=1.006, hyp_len=12308, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.1.62-5.04.1.38-3.96.1.22-3.39.1.09-2.97.pth, mybk
BLEU = 29.49, 56.1/35.0/23.6/16.3 (BP=1.000, ratio=1.112, hyp_len=12716, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.1.62-5.04.1.38-3.96.1.22-3.39.1.09-2.97.pth, bkmy
BLEU = 40.04, 66.0/46.2/33.3/25.3 (BP=1.000, ratio=1.030, hyp_len=12597, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.1.56-4.74.1.33-3.79.1.22-3.40.1.05-2.86.pth, mybk
BLEU = 32.10, 59.4/38.0/25.9/18.2 (BP=1.000, ratio=1.080, hyp_len=12346, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.1.56-4.74.1.33-3.79.1.22-3.40.1.05-2.86.pth, bkmy
BLEU = 39.22, 65.9/45.6/32.6/24.2 (BP=1.000, ratio=1.035, hyp_len=12654, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.1.56-4.75.1.34-3.82.1.20-3.32.1.08-2.96.pth, mybk
BLEU = 33.44, 61.2/39.4/27.1/19.2 (BP=1.000, ratio=1.063, hyp_len=12152, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.1.56-4.75.1.34-3.82.1.20-3.32.1.08-2.96.pth, bkmy
BLEU = 38.41, 64.6/44.9/31.9/23.6 (BP=1.000, ratio=1.049, hyp_len=12825, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.1.46-4.29.1.25-3.49.1.20-3.31.1.05-2.86.pth, mybk
BLEU = 30.64, 57.3/36.1/24.6/17.3 (BP=1.000, ratio=1.116, hyp_len=12760, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.1.46-4.29.1.25-3.49.1.20-3.31.1.05-2.86.pth, bkmy
BLEU = 39.53, 65.5/45.9/33.0/24.6 (BP=1.000, ratio=1.043, hyp_len=12757, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.1.44-4.21.1.23-3.43.1.25-3.49.1.04-2.84.pth, mybk
BLEU = 33.57, 61.1/39.2/27.1/19.5 (BP=1.000, ratio=1.040, hyp_len=11894, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.1.44-4.21.1.23-3.43.1.25-3.49.1.04-2.84.pth, bkmy
BLEU = 39.38, 64.6/45.5/33.0/24.8 (BP=1.000, ratio=1.086, hyp_len=13280, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.1.40-4.06.1.20-3.32.1.22-3.40.1.07-2.92.pth, mybk
BLEU = 33.53, 61.1/39.2/27.0/19.5 (BP=1.000, ratio=1.042, hyp_len=11916, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.1.40-4.06.1.20-3.32.1.22-3.40.1.07-2.92.pth, bkmy
BLEU = 40.97, 67.0/47.2/34.2/26.0 (BP=1.000, ratio=1.006, hyp_len=12303, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.1.37-3.95.1.16-3.17.1.23-3.43.1.05-2.86.pth, mybk
BLEU = 32.85, 61.1/38.8/26.3/18.7 (BP=1.000, ratio=1.040, hyp_len=11884, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.1.37-3.95.1.16-3.17.1.23-3.43.1.05-2.86.pth, bkmy
BLEU = 40.61, 66.7/47.2/33.9/25.5 (BP=1.000, ratio=1.032, hyp_len=12628, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.1.40-4.07.1.21-3.37.1.27-3.57.1.08-2.95.pth, mybk
BLEU = 33.92, 61.8/40.0/27.4/19.5 (BP=1.000, ratio=1.042, hyp_len=11911, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.1.40-4.07.1.21-3.37.1.27-3.57.1.08-2.95.pth, bkmy
BLEU = 38.00, 63.0/44.1/31.6/23.7 (BP=1.000, ratio=1.111, hyp_len=13592, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.1.38-3.96.1.15-3.17.1.24-3.45.1.08-2.93.pth, mybk
BLEU = 33.36, 61.3/39.3/26.9/19.1 (BP=1.000, ratio=1.060, hyp_len=12122, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.1.38-3.96.1.15-3.17.1.24-3.45.1.08-2.93.pth, bkmy
BLEU = 40.30, 66.2/46.7/33.7/25.3 (BP=1.000, ratio=1.050, hyp_len=12838, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.1.28-3.61.1.08-2.96.1.26-3.53.1.09-2.98.pth, mybk
BLEU = 32.25, 60.0/37.9/25.9/18.4 (BP=1.000, ratio=1.071, hyp_len=12238, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.1.28-3.61.1.08-2.96.1.26-3.53.1.09-2.98.pth, bkmy
BLEU = 41.31, 67.0/47.6/34.8/26.3 (BP=1.000, ratio=1.020, hyp_len=12473, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.1.22-3.40.1.03-2.80.1.27-3.57.1.09-2.98.pth, mybk
BLEU = 34.40, 62.3/40.0/27.8/20.2 (BP=1.000, ratio=1.025, hyp_len=11722, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.1.22-3.40.1.03-2.80.1.27-3.57.1.09-2.98.pth, bkmy
BLEU = 38.83, 64.7/45.1/32.4/24.0 (BP=1.000, ratio=1.078, hyp_len=13189, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.1.21-3.35.1.00-2.72.1.30-3.67.1.09-2.97.pth, mybk
BLEU = 31.84, 58.6/37.3/25.6/18.4 (BP=1.000, ratio=1.062, hyp_len=12145, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.1.21-3.35.1.00-2.72.1.30-3.67.1.09-2.97.pth, bkmy
BLEU = 41.34, 67.1/47.7/34.7/26.3 (BP=1.000, ratio=1.033, hyp_len=12640, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.1.17-3.21.0.98-2.65.1.26-3.51.1.10-3.00.pth, mybk
BLEU = 33.07, 60.5/38.9/26.7/19.1 (BP=1.000, ratio=1.067, hyp_len=12194, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.1.17-3.21.0.98-2.65.1.26-3.51.1.10-3.00.pth, bkmy
BLEU = 39.48, 65.5/45.5/32.8/24.8 (BP=1.000, ratio=1.046, hyp_len=12793, ref_len=12231)
```

Best BLEU Score for my-bk ကို dsl-model-mybk.28.1.22-3.40.1.03-2.80.1.27-3.57.1.09-2.98.pth မော်ဒယ်က ပေးတယ်။ Score ကတော့ : 34.40   
Best BLEU Score for bk-my ကို dsl-model-mybk.29.1.21-3.35.1.00-2.72.1.30-3.67.1.09-2.97.pth မော်ဒယ်က ပေးတယ်။ Score ကတော့ : 41.34 

## Transformer-DSL, 40 epoch

```
Epoch 1 - |param|=8.53e+02 |g_param|=2.41e+05 loss_x2y=4.3805e+00 ppl_x2y=79.88 loss_y2x=4.0984e+00 ppl_y2x=60.24 dual_loss=0.0000e+00
Validation X2Y - loss=3.3977e+00 ppl=29.90 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=3.2121e+00 ppl=24.83 best_loss=inf best_ppl=inf
Epoch 2 - |param|=8.53e+02 |g_param|=2.03e+05 loss_x2y=3.5368e+00 ppl_x2y=34.36 loss_y2x=3.1783e+00 ppl_y2x=24.01 dual_loss=0.0000e+00
Validation X2Y - loss=2.8815e+00 ppl=17.84 best_loss=3.3977e+00 best_ppl=29.90                                          
Validation Y2X - loss=2.6983e+00 ppl=14.85 best_loss=3.2121e+00 best_ppl=24.83
Epoch 3 - |param|=8.54e+02 |g_param|=2.08e+05 loss_x2y=3.1956e+00 ppl_x2y=24.42 loss_y2x=2.8518e+00 ppl_y2x=17.32 dual_loss=0.0000e+00
Validation X2Y - loss=2.4843e+00 ppl=11.99 best_loss=2.8815e+00 best_ppl=17.84                                          
Validation Y2X - loss=2.3356e+00 ppl=10.34 best_loss=2.6983e+00 best_ppl=14.85
Epoch 4 - |param|=8.54e+02 |g_param|=2.18e+05 loss_x2y=3.0015e+00 ppl_x2y=20.12 loss_y2x=2.7193e+00 ppl_y2x=15.17 dual_loss=0.0000e+00
Validation X2Y - loss=2.1858e+00 ppl=8.90 best_loss=2.4843e+00 best_ppl=11.99                                           
Validation Y2X - loss=2.1040e+00 ppl=8.20 best_loss=2.3356e+00 best_ppl=10.34
Epoch 5 - |param|=8.55e+02 |g_param|=2.23e+05 loss_x2y=2.7323e+00 ppl_x2y=15.37 loss_y2x=2.4293e+00 ppl_y2x=11.35 dual_loss=0.0000e+00
Validation X2Y - loss=1.9844e+00 ppl=7.27 best_loss=2.1858e+00 best_ppl=8.90                                            
Validation Y2X - loss=1.8870e+00 ppl=6.60 best_loss=2.1040e+00 best_ppl=8.20
Epoch 6 - |param|=8.56e+02 |g_param|=2.38e+05 loss_x2y=2.5780e+00 ppl_x2y=13.17 loss_y2x=2.2601e+00 ppl_y2x=9.58 dual_loss=0.0000e+00
Validation X2Y - loss=1.7926e+00 ppl=6.01 best_loss=1.9844e+00 best_ppl=7.27                                            
Validation Y2X - loss=1.6584e+00 ppl=5.25 best_loss=1.8870e+00 best_ppl=6.60
Epoch 7 - |param|=8.56e+02 |g_param|=2.45e+05 loss_x2y=2.4762e+00 ppl_x2y=11.90 loss_y2x=2.1567e+00 ppl_y2x=8.64 dual_loss=0.0000e+00
Validation X2Y - loss=1.6584e+00 ppl=5.25 best_loss=1.7926e+00 best_ppl=6.01                                            
Validation Y2X - loss=1.5286e+00 ppl=4.61 best_loss=1.6584e+00 best_ppl=5.25
Epoch 8 - |param|=8.57e+02 |g_param|=2.59e+05 loss_x2y=2.3100e+00 ppl_x2y=10.07 loss_y2x=2.0043e+00 ppl_y2x=7.42 dual_loss=0.0000e+00
Validation X2Y - loss=1.5452e+00 ppl=4.69 best_loss=1.6584e+00 best_ppl=5.25                                            
Validation Y2X - loss=1.4089e+00 ppl=4.09 best_loss=1.5286e+00 best_ppl=4.61
Epoch 9 - |param|=8.57e+02 |g_param|=2.76e+05 loss_x2y=2.2565e+00 ppl_x2y=9.55 loss_y2x=2.0009e+00 ppl_y2x=7.40 dual_loss=0.0000e+00
Validation X2Y - loss=1.4834e+00 ppl=4.41 best_loss=1.5452e+00 best_ppl=4.69                                            
Validation Y2X - loss=1.3912e+00 ppl=4.02 best_loss=1.4089e+00 best_ppl=4.09
Epoch 10 - |param|=8.58e+02 |g_param|=2.92e+05 loss_x2y=2.2369e+00 ppl_x2y=9.36 loss_y2x=2.0105e+00 ppl_y2x=7.47 dual_loss=0.0000e+00
Validation X2Y - loss=1.3988e+00 ppl=4.05 best_loss=1.4834e+00 best_ppl=4.41                                            
Validation Y2X - loss=1.2785e+00 ppl=3.59 best_loss=1.3912e+00 best_ppl=4.02
Epoch 11 - |param|=8.59e+02 |g_param|=2.75e+05 loss_x2y=2.0432e+00 ppl_x2y=7.72 loss_y2x=1.7758e+00 ppl_y2x=5.91 dual_loss=0.0000e+00
Validation X2Y - loss=1.3487e+00 ppl=3.85 best_loss=1.3988e+00 best_ppl=4.05                                            
Validation Y2X - loss=1.2323e+00 ppl=3.43 best_loss=1.2785e+00 best_ppl=3.59
Epoch 12 - |param|=8.59e+02 |g_param|=3.01e+05 loss_x2y=2.0670e+00 ppl_x2y=7.90 loss_y2x=1.7546e+00 ppl_y2x=5.78 dual_loss=0.0000e+00
Validation X2Y - loss=1.3243e+00 ppl=3.76 best_loss=1.3487e+00 best_ppl=3.85                                            
Validation Y2X - loss=1.1995e+00 ppl=3.32 best_loss=1.2323e+00 best_ppl=3.43
Epoch 13 - |param|=8.60e+02 |g_param|=2.97e+05 loss_x2y=1.8846e+00 ppl_x2y=6.58 loss_y2x=1.6367e+00 ppl_y2x=5.14 dual_loss=0.0000e+00
Validation X2Y - loss=1.2885e+00 ppl=3.63 best_loss=1.3243e+00 best_ppl=3.76                                            
Validation Y2X - loss=1.1417e+00 ppl=3.13 best_loss=1.1995e+00 best_ppl=3.32
Epoch 14 - |param|=8.60e+02 |g_param|=3.02e+05 loss_x2y=1.7563e+00 ppl_x2y=5.79 loss_y2x=1.5285e+00 ppl_y2x=4.61 dual_loss=0.0000e+00
Validation X2Y - loss=1.2681e+00 ppl=3.55 best_loss=1.2885e+00 best_ppl=3.63                                            
Validation Y2X - loss=1.1408e+00 ppl=3.13 best_loss=1.1417e+00 best_ppl=3.13
Epoch 15 - |param|=8.61e+02 |g_param|=3.02e+05 loss_x2y=1.7324e+00 ppl_x2y=5.65 loss_y2x=1.4841e+00 ppl_y2x=4.41 dual_loss=0.0000e+00
Validation X2Y - loss=1.2489e+00 ppl=3.49 best_loss=1.2681e+00 best_ppl=3.55                                            
Validation Y2X - loss=1.0968e+00 ppl=2.99 best_loss=1.1408e+00 best_ppl=3.13
Epoch 16 - |param|=8.61e+02 |g_param|=3.26e+05 loss_x2y=1.7078e+00 ppl_x2y=5.52 loss_y2x=1.4765e+00 ppl_y2x=4.38 dual_loss=0.0000e+00
Validation X2Y - loss=1.2273e+00 ppl=3.41 best_loss=1.2489e+00 best_ppl=3.49                                            
Validation Y2X - loss=1.0921e+00 ppl=2.98 best_loss=1.0968e+00 best_ppl=2.99
Epoch 17 - |param|=8.62e+02 |g_param|=3.21e+05 loss_x2y=1.6497e+00 ppl_x2y=5.21 loss_y2x=1.4370e+00 ppl_y2x=4.21 dual_loss=0.0000e+00
Validation X2Y - loss=1.2180e+00 ppl=3.38 best_loss=1.2273e+00 best_ppl=3.41                                            
Validation Y2X - loss=1.0875e+00 ppl=2.97 best_loss=1.0921e+00 best_ppl=2.98
Epoch 18 - |param|=8.62e+02 |g_param|=3.37e+05 loss_x2y=1.6188e+00 ppl_x2y=5.05 loss_y2x=1.3900e+00 ppl_y2x=4.02 dual_loss=0.0000e+00
Validation X2Y - loss=1.2380e+00 ppl=3.45 best_loss=1.2180e+00 best_ppl=3.38                                            
Validation Y2X - loss=1.0885e+00 ppl=2.97 best_loss=1.0875e+00 best_ppl=2.97
Epoch 19 - |param|=8.63e+02 |g_param|=3.38e+05 loss_x2y=1.5452e+00 ppl_x2y=4.69 loss_y2x=1.3224e+00 ppl_y2x=3.75 dual_loss=0.0000e+00
Validation X2Y - loss=1.2152e+00 ppl=3.37 best_loss=1.2180e+00 best_ppl=3.38                                            
Validation Y2X - loss=1.0957e+00 ppl=2.99 best_loss=1.0875e+00 best_ppl=2.97
Epoch 20 - |param|=8.63e+02 |g_param|=3.56e+05 loss_x2y=1.5362e+00 ppl_x2y=4.65 loss_y2x=1.3750e+00 ppl_y2x=3.96 dual_loss=0.0000e+00
Validation X2Y - loss=1.2403e+00 ppl=3.46 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.0905e+00 ppl=2.98 best_loss=1.0875e+00 best_ppl=2.97
Epoch 21 - |param|=8.64e+02 |g_param|=3.40e+05 loss_x2y=1.4887e+00 ppl_x2y=4.43 loss_y2x=1.2958e+00 ppl_y2x=3.65 dual_loss=6.0596e-01
Validation X2Y - loss=1.2253e+00 ppl=3.41 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.0554e+00 ppl=2.87 best_loss=1.0875e+00 best_ppl=2.97
Epoch 22 - |param|=8.64e+02 |g_param|=3.46e+05 loss_x2y=1.4802e+00 ppl_x2y=4.39 loss_y2x=1.2953e+00 ppl_y2x=3.65 dual_loss=5.2189e-01
Validation X2Y - loss=1.2520e+00 ppl=3.50 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.0177e+00 ppl=2.77 best_loss=1.0554e+00 best_ppl=2.87
Epoch 23 - |param|=8.65e+02 |g_param|=3.50e+05 loss_x2y=1.4194e+00 ppl_x2y=4.13 loss_y2x=1.2387e+00 ppl_y2x=3.45 dual_loss=4.9773e-01
Validation X2Y - loss=1.2639e+00 ppl=3.54 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.0507e+00 ppl=2.86 best_loss=1.0177e+00 best_ppl=2.77
Epoch 24 - |param|=8.66e+02 |g_param|=3.67e+05 loss_x2y=1.4006e+00 ppl_x2y=4.06 loss_y2x=1.1769e+00 ppl_y2x=3.24 dual_loss=4.9449e-01
Validation X2Y - loss=1.2793e+00 ppl=3.59 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.0625e+00 ppl=2.89 best_loss=1.0177e+00 best_ppl=2.77
Epoch 25 - |param|=8.66e+02 |g_param|=3.53e+05 loss_x2y=1.3101e+00 ppl_x2y=3.71 loss_y2x=1.1303e+00 ppl_y2x=3.10 dual_loss=4.8135e-01
Validation X2Y - loss=1.2538e+00 ppl=3.50 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.0866e+00 ppl=2.96 best_loss=1.0177e+00 best_ppl=2.77
Epoch 26 - |param|=8.67e+02 |g_param|=4.00e+05 loss_x2y=1.3469e+00 ppl_x2y=3.85 loss_y2x=1.1926e+00 ppl_y2x=3.30 dual_loss=6.2713e-01
Validation X2Y - loss=1.2748e+00 ppl=3.58 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.0626e+00 ppl=2.89 best_loss=1.0177e+00 best_ppl=2.77
Epoch 27 - |param|=8.67e+02 |g_param|=3.63e+05 loss_x2y=1.2836e+00 ppl_x2y=3.61 loss_y2x=1.1075e+00 ppl_y2x=3.03 dual_loss=4.8410e-01
Validation X2Y - loss=1.2671e+00 ppl=3.55 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.0773e+00 ppl=2.94 best_loss=1.0177e+00 best_ppl=2.77
Epoch 28 - |param|=8.68e+02 |g_param|=3.78e+05 loss_x2y=1.2131e+00 ppl_x2y=3.36 loss_y2x=1.0328e+00 ppl_y2x=2.81 dual_loss=5.0799e-01
Validation X2Y - loss=1.2673e+00 ppl=3.55 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.0413e+00 ppl=2.83 best_loss=1.0177e+00 best_ppl=2.77
Epoch 29 - |param|=8.68e+02 |g_param|=3.65e+05 loss_x2y=1.1957e+00 ppl_x2y=3.31 loss_y2x=1.0285e+00 ppl_y2x=2.80 dual_loss=5.1966e-01
Validation X2Y - loss=1.3192e+00 ppl=3.74 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.0638e+00 ppl=2.90 best_loss=1.0177e+00 best_ppl=2.77
Epoch 30 - |param|=8.69e+02 |g_param|=3.97e+05 loss_x2y=1.1951e+00 ppl_x2y=3.30 loss_y2x=1.0200e+00 ppl_y2x=2.77 dual_loss=5.7727e-01
Validation X2Y - loss=1.3121e+00 ppl=3.71 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.0819e+00 ppl=2.95 best_loss=1.0177e+00 best_ppl=2.77
Epoch 31 - |param|=8.69e+02 |g_param|=3.72e+05 loss_x2y=1.1768e+00 ppl_x2y=3.24 loss_y2x=9.8013e-01 ppl_y2x=2.66 dual_loss=5.3458e-01
Validation X2Y - loss=1.3467e+00 ppl=3.84 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.0704e+00 ppl=2.92 best_loss=1.0177e+00 best_ppl=2.77
Epoch 32 - |param|=8.70e+02 |g_param|=3.91e+05 loss_x2y=1.1453e+00 ppl_x2y=3.14 loss_y2x=9.5788e-01 ppl_y2x=2.61 dual_loss=5.7417e-01
Validation X2Y - loss=1.3273e+00 ppl=3.77 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.1098e+00 ppl=3.03 best_loss=1.0177e+00 best_ppl=2.77
Epoch 33 - |param|=8.70e+02 |g_param|=6.21e+05 loss_x2y=1.0878e+00 ppl_x2y=2.97 loss_y2x=9.3424e-01 ppl_y2x=2.55 dual_loss=5.4398e-01
Validation X2Y - loss=1.3004e+00 ppl=3.67 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.0943e+00 ppl=2.99 best_loss=1.0177e+00 best_ppl=2.77
Epoch 34 - |param|=8.71e+02 |g_param|=7.95e+05 loss_x2y=1.0897e+00 ppl_x2y=2.97 loss_y2x=9.1841e-01 ppl_y2x=2.51 dual_loss=5.5537e-01
Validation X2Y - loss=1.3185e+00 ppl=3.74 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.0987e+00 ppl=3.00 best_loss=1.0177e+00 best_ppl=2.77
Epoch 35 - |param|=8.71e+02 |g_param|=7.97e+05 loss_x2y=1.0800e+00 ppl_x2y=2.94 loss_y2x=9.2854e-01 ppl_y2x=2.53 dual_loss=6.3166e-01
Validation X2Y - loss=1.3525e+00 ppl=3.87 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.1040e+00 ppl=3.02 best_loss=1.0177e+00 best_ppl=2.77
Epoch 36 - |param|=8.72e+02 |g_param|=7.84e+05 loss_x2y=1.0734e+00 ppl_x2y=2.93 loss_y2x=8.8974e-01 ppl_y2x=2.43 dual_loss=6.0749e-01
Validation X2Y - loss=1.3370e+00 ppl=3.81 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.1409e+00 ppl=3.13 best_loss=1.0177e+00 best_ppl=2.77
Epoch 37 - |param|=8.72e+02 |g_param|=7.54e+05 loss_x2y=1.0020e+00 ppl_x2y=2.72 loss_y2x=8.4914e-01 ppl_y2x=2.34 dual_loss=5.8004e-01
Validation X2Y - loss=1.3524e+00 ppl=3.87 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.1333e+00 ppl=3.11 best_loss=1.0177e+00 best_ppl=2.77
Epoch 38 - |param|=8.73e+02 |g_param|=8.17e+05 loss_x2y=1.1070e+00 ppl_x2y=3.03 loss_y2x=8.8703e-01 ppl_y2x=2.43 dual_loss=8.8409e-01
Validation X2Y - loss=1.3613e+00 ppl=3.90 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.1349e+00 ppl=3.11 best_loss=1.0177e+00 best_ppl=2.77
Epoch 39 - |param|=8.73e+02 |g_param|=7.97e+05 loss_x2y=1.0044e+00 ppl_x2y=2.73 loss_y2x=8.2803e-01 ppl_y2x=2.29 dual_loss=6.3859e-01
Validation X2Y - loss=1.3858e+00 ppl=4.00 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.1657e+00 ppl=3.21 best_loss=1.0177e+00 best_ppl=2.77
Epoch 40 - |param|=8.74e+02 |g_param|=8.26e+05 loss_x2y=1.0149e+00 ppl_x2y=2.76 loss_y2x=8.3176e-01 ppl_y2x=2.30 dual_loss=6.7831e-01
Validation X2Y - loss=1.3610e+00 ppl=3.90 best_loss=1.2152e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.1699e+00 ppl=3.22 best_loss=1.0177e+00 best_ppl=2.77

real	12m46.363s
user	12m32.343s
sys	0m14.192s

```

testing/evaluation...  

```
/home/ye/exp/simple-nmt/model/dsl/transformer/mybk-40epoch
Evaluation result for the model: dsl-model-mybk.01.4.38-79.88.4.10-60.24.3.40-29.90.3.21-24.83.pth, mybk
BLEU = 4.87, 23.6/6.9/3.3/1.8 (BP=0.879, ratio=0.885, hyp_len=10121, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.38-79.88.4.10-60.24.3.40-29.90.3.21-24.83.pth, bkmy
BLEU = 4.29, 30.5/8.5/3.0/0.9 (BP=0.838, ratio=0.850, hyp_len=10396, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.02.3.54-34.36.3.18-24.01.2.88-17.84.2.70-14.85.pth, mybk
BLEU = 3.37, 16.4/4.9/1.8/0.9 (BP=1.000, ratio=1.616, hyp_len=18479, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.3.54-34.36.3.18-24.01.2.88-17.84.2.70-14.85.pth, bkmy
BLEU = 3.98, 20.4/7.0/2.3/0.7 (BP=1.000, ratio=1.563, hyp_len=19122, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.3.20-24.42.2.85-17.32.2.48-11.99.2.34-10.34.pth, mybk
BLEU = 3.29, 13.9/4.8/2.0/0.9 (BP=1.000, ratio=2.212, hyp_len=25292, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.3.20-24.42.2.85-17.32.2.48-11.99.2.34-10.34.pth, bkmy
BLEU = 5.08, 21.3/8.3/3.2/1.2 (BP=1.000, ratio=1.812, hyp_len=22167, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.3.00-20.12.2.72-15.17.2.19-8.90.2.10-8.20.pth, mybk
BLEU = 7.63, 25.3/10.5/5.1/2.5 (BP=1.000, ratio=1.435, hyp_len=16403, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.3.00-20.12.2.72-15.17.2.19-8.90.2.10-8.20.pth, bkmy
BLEU = 6.64, 22.7/10.0/4.4/2.0 (BP=1.000, ratio=1.843, hyp_len=22542, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.2.73-15.37.2.43-11.35.1.98-7.27.1.89-6.60.pth, mybk
BLEU = 9.87, 29.7/13.2/6.9/3.5 (BP=1.000, ratio=1.398, hyp_len=15977, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.2.73-15.37.2.43-11.35.1.98-7.27.1.89-6.60.pth, bkmy
BLEU = 11.15, 31.1/15.4/7.9/4.1 (BP=1.000, ratio=1.549, hyp_len=18949, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.2.58-13.17.2.26-9.58.1.79-6.01.1.66-5.25.pth, mybk
BLEU = 14.20, 35.6/18.0/10.3/6.1 (BP=1.000, ratio=1.284, hyp_len=14680, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.2.58-13.17.2.26-9.58.1.79-6.01.1.66-5.25.pth, bkmy
BLEU = 15.63, 39.1/20.6/11.4/6.5 (BP=1.000, ratio=1.278, hyp_len=15635, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.2.48-11.90.2.16-8.64.1.66-5.25.1.53-4.61.pth, mybk
BLEU = 13.69, 34.2/17.4/10.0/5.9 (BP=1.000, ratio=1.407, hyp_len=16089, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.2.48-11.90.2.16-8.64.1.66-5.25.1.53-4.61.pth, bkmy
BLEU = 24.18, 53.0/31.0/19.1/12.3 (BP=0.969, ratio=0.969, hyp_len=11856, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.2.31-10.07.2.00-7.42.1.55-4.69.1.41-4.09.pth, mybk
BLEU = 23.74, 51.0/29.0/18.2/11.8 (BP=1.000, ratio=1.041, hyp_len=11902, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.2.31-10.07.2.00-7.42.1.55-4.69.1.41-4.09.pth, bkmy
BLEU = 23.05, 47.5/28.7/17.9/11.6 (BP=1.000, ratio=1.203, hyp_len=14708, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.2.26-9.55.2.00-7.40.1.48-4.41.1.39-4.02.pth, mybk
BLEU = 25.66, 52.5/30.6/19.9/13.5 (BP=1.000, ratio=1.030, hyp_len=11780, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.2.26-9.55.2.00-7.40.1.48-4.41.1.39-4.02.pth, bkmy
BLEU = 29.44, 55.7/35.4/23.4/16.3 (BP=1.000, ratio=1.041, hyp_len=12728, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.2.24-9.36.2.01-7.47.1.40-4.05.1.28-3.59.pth, mybk
BLEU = 25.41, 50.6/30.3/20.0/13.6 (BP=1.000, ratio=1.124, hyp_len=12844, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.2.24-9.36.2.01-7.47.1.40-4.05.1.28-3.59.pth, bkmy
BLEU = 31.55, 58.0/37.9/25.5/17.7 (BP=1.000, ratio=1.051, hyp_len=12856, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.2.04-7.72.1.78-5.91.1.35-3.85.1.23-3.43.pth, mybk
BLEU = 27.92, 53.7/32.9/22.2/15.5 (BP=1.000, ratio=1.078, hyp_len=12318, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.2.04-7.72.1.78-5.91.1.35-3.85.1.23-3.43.pth, bkmy
BLEU = 34.44, 61.1/40.6/28.1/20.2 (BP=1.000, ratio=1.015, hyp_len=12413, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.2.07-7.90.1.75-5.78.1.32-3.76.1.20-3.32.pth, mybk
BLEU = 29.22, 56.0/34.4/23.2/16.3 (BP=1.000, ratio=1.034, hyp_len=11818, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.2.07-7.90.1.75-5.78.1.32-3.76.1.20-3.32.pth, bkmy
BLEU = 36.16, 63.0/42.6/29.7/21.5 (BP=1.000, ratio=1.009, hyp_len=12336, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.1.88-6.58.1.64-5.14.1.29-3.63.1.14-3.13.pth, mybk
BLEU = 27.36, 53.5/32.3/21.6/15.1 (BP=1.000, ratio=1.055, hyp_len=12058, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.1.88-6.58.1.64-5.14.1.29-3.63.1.14-3.13.pth, bkmy
BLEU = 36.50, 62.9/42.8/30.0/21.9 (BP=1.000, ratio=1.038, hyp_len=12697, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.1.76-5.79.1.53-4.61.1.27-3.55.1.14-3.13.pth, mybk
BLEU = 31.88, 59.6/37.8/25.6/17.9 (BP=1.000, ratio=1.017, hyp_len=11628, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.1.76-5.79.1.53-4.61.1.27-3.55.1.14-3.13.pth, bkmy
BLEU = 36.34, 62.9/42.7/29.9/21.7 (BP=1.000, ratio=1.025, hyp_len=12539, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.1.73-5.65.1.48-4.41.1.25-3.49.1.10-2.99.pth, mybk
BLEU = 30.20, 57.5/35.9/24.0/16.8 (BP=1.000, ratio=1.073, hyp_len=12268, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.1.73-5.65.1.48-4.41.1.25-3.49.1.10-2.99.pth, bkmy
BLEU = 37.18, 63.6/43.7/30.8/22.3 (BP=1.000, ratio=1.042, hyp_len=12746, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.1.71-5.52.1.48-4.38.1.23-3.41.1.09-2.98.pth, mybk
BLEU = 32.46, 60.1/38.6/26.1/18.3 (BP=1.000, ratio=1.033, hyp_len=11807, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.1.71-5.52.1.48-4.38.1.23-3.41.1.09-2.98.pth, bkmy
BLEU = 39.17, 66.4/46.0/32.4/23.8 (BP=1.000, ratio=1.025, hyp_len=12540, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.1.65-5.21.1.44-4.21.1.22-3.38.1.09-2.97.pth, mybk
BLEU = 33.26, 60.8/39.2/26.8/19.2 (BP=1.000, ratio=1.024, hyp_len=11702, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.1.65-5.21.1.44-4.21.1.22-3.38.1.09-2.97.pth, bkmy
BLEU = 36.53, 61.9/43.1/30.4/22.0 (BP=1.000, ratio=1.123, hyp_len=13735, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.1.62-5.05.1.39-4.02.1.24-3.45.1.09-2.97.pth, mybk
BLEU = 33.38, 61.0/39.1/26.8/19.4 (BP=1.000, ratio=1.058, hyp_len=12093, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.1.62-5.05.1.39-4.02.1.24-3.45.1.09-2.97.pth, bkmy
BLEU = 39.07, 64.8/45.5/32.7/24.1 (BP=1.000, ratio=1.055, hyp_len=12903, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.1.55-4.69.1.32-3.75.1.22-3.37.1.10-2.99.pth, mybk
BLEU = 33.01, 60.7/39.0/26.6/18.9 (BP=1.000, ratio=1.053, hyp_len=12039, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.1.55-4.69.1.32-3.75.1.22-3.37.1.10-2.99.pth, bkmy
BLEU = 39.91, 65.9/46.5/33.4/24.8 (BP=1.000, ratio=1.060, hyp_len=12969, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.1.54-4.65.1.37-3.96.1.24-3.46.1.09-2.98.pth, mybk
BLEU = 32.91, 60.4/38.8/26.5/18.8 (BP=1.000, ratio=1.055, hyp_len=12056, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.1.54-4.65.1.37-3.96.1.24-3.46.1.09-2.98.pth, bkmy
BLEU = 36.89, 62.0/43.1/30.7/22.6 (BP=1.000, ratio=1.123, hyp_len=13735, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.1.49-4.43.1.30-3.65.1.23-3.41.1.06-2.87.pth, mybk
BLEU = 33.87, 61.2/39.6/27.4/19.8 (BP=1.000, ratio=1.059, hyp_len=12102, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.1.49-4.43.1.30-3.65.1.23-3.41.1.06-2.87.pth, bkmy
BLEU = 39.89, 65.9/46.3/33.4/24.9 (BP=1.000, ratio=1.049, hyp_len=12832, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.1.48-4.39.1.30-3.65.1.25-3.50.1.02-2.77.pth, mybk
BLEU = 32.80, 60.5/39.0/26.4/18.6 (BP=1.000, ratio=1.078, hyp_len=12321, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.1.48-4.39.1.30-3.65.1.25-3.50.1.02-2.77.pth, bkmy
BLEU = 41.62, 67.0/48.0/35.1/26.6 (BP=1.000, ratio=1.032, hyp_len=12627, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.1.42-4.13.1.24-3.45.1.26-3.54.1.05-2.86.pth, mybk
BLEU = 34.20, 61.9/40.1/27.5/20.0 (BP=1.000, ratio=1.044, hyp_len=11935, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.1.42-4.13.1.24-3.45.1.26-3.54.1.05-2.86.pth, bkmy
BLEU = 40.46, 66.0/46.8/34.0/25.5 (BP=1.000, ratio=1.049, hyp_len=12830, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.1.40-4.06.1.18-3.24.1.28-3.59.1.06-2.89.pth, mybk
BLEU = 32.90, 60.3/38.6/26.5/19.0 (BP=1.000, ratio=1.063, hyp_len=12149, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.1.40-4.06.1.18-3.24.1.28-3.59.1.06-2.89.pth, bkmy
BLEU = 39.72, 65.6/46.0/33.2/24.8 (BP=1.000, ratio=1.040, hyp_len=12719, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.1.31-3.71.1.13-3.10.1.25-3.50.1.09-2.96.pth, mybk
BLEU = 33.12, 60.5/38.9/26.7/19.1 (BP=1.000, ratio=1.056, hyp_len=12077, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.1.31-3.71.1.13-3.10.1.25-3.50.1.09-2.96.pth, bkmy
BLEU = 41.67, 67.9/48.3/35.0/26.2 (BP=1.000, ratio=1.000, hyp_len=12232, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.1.35-3.85.1.19-3.30.1.27-3.58.1.06-2.89.pth, mybk
BLEU = 33.58, 60.8/39.5/27.1/19.6 (BP=1.000, ratio=1.050, hyp_len=12004, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.1.35-3.85.1.19-3.30.1.27-3.58.1.06-2.89.pth, bkmy
BLEU = 40.66, 66.4/47.0/34.0/25.7 (BP=1.000, ratio=1.045, hyp_len=12786, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.1.28-3.61.1.11-3.03.1.27-3.55.1.08-2.94.pth, mybk
BLEU = 33.83, 61.2/39.8/27.3/19.7 (BP=1.000, ratio=1.055, hyp_len=12056, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.1.28-3.61.1.11-3.03.1.27-3.55.1.08-2.94.pth, bkmy
BLEU = 41.48, 67.0/47.8/35.0/26.4 (BP=1.000, ratio=1.045, hyp_len=12781, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.1.21-3.36.1.03-2.81.1.27-3.55.1.04-2.83.pth, mybk
BLEU = 33.15, 60.4/39.1/26.7/19.2 (BP=1.000, ratio=1.050, hyp_len=12009, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.1.21-3.36.1.03-2.81.1.27-3.55.1.04-2.83.pth, bkmy
BLEU = 42.49, 68.4/49.0/35.7/27.2 (BP=1.000, ratio=1.012, hyp_len=12378, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.1.20-3.31.1.03-2.80.1.32-3.74.1.06-2.90.pth, mybk
BLEU = 30.61, 56.7/36.1/24.6/17.4 (BP=1.000, ratio=1.110, hyp_len=12684, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.1.20-3.31.1.03-2.80.1.32-3.74.1.06-2.90.pth, bkmy
BLEU = 37.94, 64.1/44.5/31.5/23.1 (BP=1.000, ratio=1.086, hyp_len=13279, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.1.20-3.30.1.02-2.77.1.31-3.71.1.08-2.95.pth, mybk
BLEU = 34.14, 61.6/39.7/27.7/20.1 (BP=1.000, ratio=1.040, hyp_len=11885, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.1.20-3.30.1.02-2.77.1.31-3.71.1.08-2.95.pth, bkmy
BLEU = 38.23, 63.6/44.5/31.9/23.6 (BP=1.000, ratio=1.095, hyp_len=13396, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.31.1.18-3.24.0.98-2.66.1.35-3.84.1.07-2.92.pth, mybk
BLEU = 33.13, 60.6/38.8/26.7/19.2 (BP=1.000, ratio=1.046, hyp_len=11956, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.31.1.18-3.24.0.98-2.66.1.35-3.84.1.07-2.92.pth, bkmy
BLEU = 40.28, 65.9/46.7/33.8/25.3 (BP=1.000, ratio=1.057, hyp_len=12928, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.32.1.15-3.14.0.96-2.61.1.33-3.77.1.11-3.03.pth, mybk
BLEU = 32.40, 59.4/37.8/26.1/18.8 (BP=1.000, ratio=1.080, hyp_len=12345, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.32.1.15-3.14.0.96-2.61.1.33-3.77.1.11-3.03.pth, bkmy
BLEU = 39.67, 65.0/45.7/33.2/25.1 (BP=1.000, ratio=1.045, hyp_len=12780, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.33.1.09-2.97.0.93-2.55.1.30-3.67.1.09-2.99.pth, mybk
BLEU = 33.11, 60.6/38.7/26.7/19.2 (BP=1.000, ratio=1.075, hyp_len=12288, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.33.1.09-2.97.0.93-2.55.1.30-3.67.1.09-2.99.pth, bkmy
BLEU = 39.09, 64.3/45.4/32.7/24.4 (BP=1.000, ratio=1.086, hyp_len=13278, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.34.1.09-2.97.0.92-2.51.1.32-3.74.1.10-3.00.pth, mybk
BLEU = 31.95, 59.2/37.7/25.6/18.2 (BP=1.000, ratio=1.080, hyp_len=12342, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.34.1.09-2.97.0.92-2.51.1.32-3.74.1.10-3.00.pth, bkmy
BLEU = 37.91, 63.3/44.1/31.6/23.4 (BP=1.000, ratio=1.099, hyp_len=13436, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.35.1.08-2.94.0.93-2.53.1.35-3.87.1.10-3.02.pth, mybk
BLEU = 32.53, 59.2/38.1/26.3/18.9 (BP=1.000, ratio=1.082, hyp_len=12371, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.35.1.08-2.94.0.93-2.53.1.35-3.87.1.10-3.02.pth, bkmy
BLEU = 39.04, 63.9/45.0/32.7/24.7 (BP=1.000, ratio=1.074, hyp_len=13141, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.36.1.07-2.93.0.89-2.43.1.34-3.81.1.14-3.13.pth, mybk
BLEU = 33.07, 60.6/38.8/26.6/19.1 (BP=1.000, ratio=1.043, hyp_len=11918, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.36.1.07-2.93.0.89-2.43.1.34-3.81.1.14-3.13.pth, bkmy
BLEU = 39.99, 65.7/46.1/33.5/25.2 (BP=1.000, ratio=1.049, hyp_len=12831, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.37.1.00-2.72.0.85-2.34.1.35-3.87.1.13-3.11.pth, mybk
BLEU = 31.27, 57.7/36.7/25.1/18.0 (BP=1.000, ratio=1.095, hyp_len=12513, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.37.1.00-2.72.0.85-2.34.1.35-3.87.1.13-3.11.pth, bkmy
BLEU = 40.61, 66.2/46.7/34.1/25.8 (BP=1.000, ratio=1.037, hyp_len=12685, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.38.1.11-3.03.0.89-2.43.1.36-3.90.1.13-3.11.pth, mybk
BLEU = 33.74, 61.5/39.6/27.2/19.6 (BP=1.000, ratio=1.032, hyp_len=11794, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.38.1.11-3.03.0.89-2.43.1.36-3.90.1.13-3.11.pth, bkmy
BLEU = 40.21, 66.1/46.6/33.7/25.2 (BP=1.000, ratio=1.053, hyp_len=12874, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.39.1.00-2.73.0.83-2.29.1.39-4.00.1.17-3.21.pth, mybk
BLEU = 30.58, 57.8/36.1/24.3/17.2 (BP=1.000, ratio=1.080, hyp_len=12350, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.39.1.00-2.73.0.83-2.29.1.39-4.00.1.17-3.21.pth, bkmy
BLEU = 37.73, 63.1/43.8/31.4/23.3 (BP=1.000, ratio=1.089, hyp_len=13317, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.40.1.01-2.76.0.83-2.30.1.36-3.90.1.17-3.22.pth, mybk
BLEU = 32.36, 59.5/37.9/25.9/18.7 (BP=1.000, ratio=1.068, hyp_len=12208, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.40.1.01-2.76.0.83-2.30.1.36-3.90.1.17-3.22.pth, bkmy
BLEU = 37.67, 62.9/43.6/31.4/23.4 (BP=1.000, ratio=1.113, hyp_len=13619, ref_len=12231)
```

Best model for my-bk က epoch 23 မော်ဒယ် ဖြစ်ပြီးတော့၊ Best BLEU Score က : 34.20  
Best model for bk-my က epoch 28 မော်ဒယ် ဖြစ်ပြီးတော့၊ Best BLEU Score က : 42.49  

## Transformer-DSL, 50 epoch

```
Epoch 1 - |param|=8.54e+02 |g_param|=2.37e+05 loss_x2y=4.4578e+00 ppl_x2y=86.30 loss_y2x=4.0588e+00 ppl_y2x=57.91 dual_loss=0.0000e+00
Validation X2Y - loss=3.4657e+00 ppl=32.00 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=3.1429e+00 ppl=23.17 best_loss=inf best_ppl=inf
Epoch 2 - |param|=8.54e+02 |g_param|=1.60e+05 loss_x2y=3.6625e+00 ppl_x2y=38.96 loss_y2x=3.2830e+00 ppl_y2x=26.65 dual_loss=0.0000e+00
Validation X2Y - loss=2.9714e+00 ppl=19.52 best_loss=3.4657e+00 best_ppl=32.00                                          
Validation Y2X - loss=2.6769e+00 ppl=14.54 best_loss=3.1429e+00 best_ppl=23.17
Epoch 3 - |param|=8.55e+02 |g_param|=1.31e+05 loss_x2y=3.2272e+00 ppl_x2y=25.21 loss_y2x=2.8410e+00 ppl_y2x=17.13 dual_loss=0.0000e+00
Validation X2Y - loss=2.5453e+00 ppl=12.75 best_loss=2.9714e+00 best_ppl=19.52                                          
Validation Y2X - loss=2.3135e+00 ppl=10.11 best_loss=2.6769e+00 best_ppl=14.54
Epoch 4 - |param|=8.56e+02 |g_param|=1.45e+05 loss_x2y=3.0035e+00 ppl_x2y=20.15 loss_y2x=2.6147e+00 ppl_y2x=13.66 dual_loss=0.0000e+00
Validation X2Y - loss=2.2896e+00 ppl=9.87 best_loss=2.5453e+00 best_ppl=12.75                                           
Validation Y2X - loss=2.0816e+00 ppl=8.02 best_loss=2.3135e+00 best_ppl=10.11
Epoch 5 - |param|=8.56e+02 |g_param|=1.37e+05 loss_x2y=2.7312e+00 ppl_x2y=15.35 loss_y2x=2.4011e+00 ppl_y2x=11.04 dual_loss=0.0000e+00
Validation X2Y - loss=2.0363e+00 ppl=7.66 best_loss=2.2896e+00 best_ppl=9.87                                            
Validation Y2X - loss=1.8108e+00 ppl=6.12 best_loss=2.0816e+00 best_ppl=8.02
Epoch 6 - |param|=8.57e+02 |g_param|=1.53e+05 loss_x2y=2.6250e+00 ppl_x2y=13.80 loss_y2x=2.2951e+00 ppl_y2x=9.93 dual_loss=0.0000e+00
Validation X2Y - loss=1.8528e+00 ppl=6.38 best_loss=2.0363e+00 best_ppl=7.66                                            
Validation Y2X - loss=1.6517e+00 ppl=5.22 best_loss=1.8108e+00 best_ppl=6.12
Epoch 7 - |param|=8.57e+02 |g_param|=1.57e+05 loss_x2y=2.4647e+00 ppl_x2y=11.76 loss_y2x=2.1626e+00 ppl_y2x=8.69 dual_loss=0.0000e+00
Validation X2Y - loss=1.7328e+00 ppl=5.66 best_loss=1.8528e+00 best_ppl=6.38                                            
Validation Y2X - loss=1.5703e+00 ppl=4.81 best_loss=1.6517e+00 best_ppl=5.22
Epoch 8 - |param|=8.58e+02 |g_param|=1.64e+05 loss_x2y=2.3178e+00 ppl_x2y=10.15 loss_y2x=2.0213e+00 ppl_y2x=7.55 dual_loss=0.0000e+00
Validation X2Y - loss=1.5827e+00 ppl=4.87 best_loss=1.7328e+00 best_ppl=5.66                                            
Validation Y2X - loss=1.4601e+00 ppl=4.31 best_loss=1.5703e+00 best_ppl=4.81
Epoch 9 - |param|=8.59e+02 |g_param|=1.68e+05 loss_x2y=2.1769e+00 ppl_x2y=8.82 loss_y2x=1.8941e+00 ppl_y2x=6.65 dual_loss=0.0000e+00
Validation X2Y - loss=1.4939e+00 ppl=4.45 best_loss=1.5827e+00 best_ppl=4.87                                            
Validation Y2X - loss=1.3131e+00 ppl=3.72 best_loss=1.4601e+00 best_ppl=4.31
Epoch 10 - |param|=8.59e+02 |g_param|=1.74e+05 loss_x2y=2.1631e+00 ppl_x2y=8.70 loss_y2x=1.8999e+00 ppl_y2x=6.68 dual_loss=0.0000e+00
Validation X2Y - loss=1.4600e+00 ppl=4.31 best_loss=1.4939e+00 best_ppl=4.45                                            
Validation Y2X - loss=1.2576e+00 ppl=3.52 best_loss=1.3131e+00 best_ppl=3.72
Epoch 11 - |param|=8.60e+02 |g_param|=1.77e+05 loss_x2y=2.0079e+00 ppl_x2y=7.45 loss_y2x=1.7326e+00 ppl_y2x=5.66 dual_loss=0.0000e+00
Validation X2Y - loss=1.3829e+00 ppl=3.99 best_loss=1.4600e+00 best_ppl=4.31                                            
Validation Y2X - loss=1.2373e+00 ppl=3.45 best_loss=1.2576e+00 best_ppl=3.52
Epoch 12 - |param|=8.60e+02 |g_param|=1.87e+05 loss_x2y=2.0577e+00 ppl_x2y=7.83 loss_y2x=1.7315e+00 ppl_y2x=5.65 dual_loss=0.0000e+00
Validation X2Y - loss=1.3609e+00 ppl=3.90 best_loss=1.3829e+00 best_ppl=3.99                                            
Validation Y2X - loss=1.1803e+00 ppl=3.26 best_loss=1.2373e+00 best_ppl=3.45
Epoch 13 - |param|=8.61e+02 |g_param|=1.84e+05 loss_x2y=1.9511e+00 ppl_x2y=7.04 loss_y2x=1.6669e+00 ppl_y2x=5.30 dual_loss=0.0000e+00
Validation X2Y - loss=1.3376e+00 ppl=3.81 best_loss=1.3609e+00 best_ppl=3.90                                            
Validation Y2X - loss=1.1427e+00 ppl=3.14 best_loss=1.1803e+00 best_ppl=3.26
Epoch 14 - |param|=8.61e+02 |g_param|=1.99e+05 loss_x2y=1.8787e+00 ppl_x2y=6.55 loss_y2x=1.6211e+00 ppl_y2x=5.06 dual_loss=0.0000e+00
Validation X2Y - loss=1.3212e+00 ppl=3.75 best_loss=1.3376e+00 best_ppl=3.81                                            
Validation Y2X - loss=1.1304e+00 ppl=3.10 best_loss=1.1427e+00 best_ppl=3.14
Epoch 15 - |param|=8.62e+02 |g_param|=1.94e+05 loss_x2y=1.7691e+00 ppl_x2y=5.87 loss_y2x=1.5113e+00 ppl_y2x=4.53 dual_loss=0.0000e+00
Validation X2Y - loss=1.3205e+00 ppl=3.75 best_loss=1.3212e+00 best_ppl=3.75                                            
Validation Y2X - loss=1.1236e+00 ppl=3.08 best_loss=1.1304e+00 best_ppl=3.10
Epoch 16 - |param|=8.62e+02 |g_param|=2.18e+05 loss_x2y=1.7878e+00 ppl_x2y=5.98 loss_y2x=1.5595e+00 ppl_y2x=4.76 dual_loss=0.0000e+00
Validation X2Y - loss=1.3086e+00 ppl=3.70 best_loss=1.3205e+00 best_ppl=3.75                                            
Validation Y2X - loss=1.1059e+00 ppl=3.02 best_loss=1.1236e+00 best_ppl=3.08
Epoch 17 - |param|=8.63e+02 |g_param|=2.07e+05 loss_x2y=1.6800e+00 ppl_x2y=5.37 loss_y2x=1.5008e+00 ppl_y2x=4.49 dual_loss=0.0000e+00
Validation X2Y - loss=1.2737e+00 ppl=3.57 best_loss=1.3086e+00 best_ppl=3.70                                            
Validation Y2X - loss=1.0800e+00 ppl=2.94 best_loss=1.1059e+00 best_ppl=3.02
Epoch 18 - |param|=8.63e+02 |g_param|=2.15e+05 loss_x2y=1.6941e+00 ppl_x2y=5.44 loss_y2x=1.4217e+00 ppl_y2x=4.14 dual_loss=0.0000e+00
Validation X2Y - loss=1.2768e+00 ppl=3.59 best_loss=1.2737e+00 best_ppl=3.57                                            
Validation Y2X - loss=1.0648e+00 ppl=2.90 best_loss=1.0800e+00 best_ppl=2.94
Epoch 19 - |param|=8.64e+02 |g_param|=2.09e+05 loss_x2y=1.5582e+00 ppl_x2y=4.75 loss_y2x=1.3361e+00 ppl_y2x=3.80 dual_loss=0.0000e+00
Validation X2Y - loss=1.2364e+00 ppl=3.44 best_loss=1.2737e+00 best_ppl=3.57                                            
Validation Y2X - loss=1.0429e+00 ppl=2.84 best_loss=1.0648e+00 best_ppl=2.90
Epoch 20 - |param|=8.65e+02 |g_param|=2.20e+05 loss_x2y=1.4405e+00 ppl_x2y=4.22 loss_y2x=1.2403e+00 ppl_y2x=3.46 dual_loss=0.0000e+00
Validation X2Y - loss=1.2803e+00 ppl=3.60 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.1028e+00 ppl=3.01 best_loss=1.0429e+00 best_ppl=2.84
Epoch 21 - |param|=8.65e+02 |g_param|=2.16e+05 loss_x2y=1.5290e+00 ppl_x2y=4.61 loss_y2x=1.3283e+00 ppl_y2x=3.77 dual_loss=6.6990e-01
Validation X2Y - loss=1.3009e+00 ppl=3.67 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.0600e+00 ppl=2.89 best_loss=1.0429e+00 best_ppl=2.84
Epoch 22 - |param|=8.66e+02 |g_param|=2.24e+05 loss_x2y=1.4356e+00 ppl_x2y=4.20 loss_y2x=1.2309e+00 ppl_y2x=3.42 dual_loss=4.8878e-01
Validation X2Y - loss=1.2974e+00 ppl=3.66 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.0959e+00 ppl=2.99 best_loss=1.0429e+00 best_ppl=2.84
Epoch 23 - |param|=8.66e+02 |g_param|=2.29e+05 loss_x2y=1.4552e+00 ppl_x2y=4.29 loss_y2x=1.2773e+00 ppl_y2x=3.59 dual_loss=5.6500e-01
Validation X2Y - loss=1.3113e+00 ppl=3.71 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.0851e+00 ppl=2.96 best_loss=1.0429e+00 best_ppl=2.84
Epoch 24 - |param|=8.67e+02 |g_param|=2.28e+05 loss_x2y=1.3764e+00 ppl_x2y=3.96 loss_y2x=1.1634e+00 ppl_y2x=3.20 dual_loss=4.7474e-01
Validation X2Y - loss=1.3277e+00 ppl=3.77 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.0976e+00 ppl=3.00 best_loss=1.0429e+00 best_ppl=2.84
Epoch 25 - |param|=8.67e+02 |g_param|=2.35e+05 loss_x2y=1.3456e+00 ppl_x2y=3.84 loss_y2x=1.1854e+00 ppl_y2x=3.27 dual_loss=4.9150e-01
Validation X2Y - loss=1.3152e+00 ppl=3.73 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.0842e+00 ppl=2.96 best_loss=1.0429e+00 best_ppl=2.84
Epoch 26 - |param|=8.68e+02 |g_param|=2.40e+05 loss_x2y=1.2874e+00 ppl_x2y=3.62 loss_y2x=1.0855e+00 ppl_y2x=2.96 dual_loss=4.6697e-01
Validation X2Y - loss=1.3206e+00 ppl=3.75 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.0825e+00 ppl=2.95 best_loss=1.0429e+00 best_ppl=2.84
Epoch 27 - |param|=8.68e+02 |g_param|=2.24e+05 loss_x2y=1.2662e+00 ppl_x2y=3.55 loss_y2x=1.0578e+00 ppl_y2x=2.88 dual_loss=4.9899e-01
Validation X2Y - loss=1.3315e+00 ppl=3.79 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.1117e+00 ppl=3.04 best_loss=1.0429e+00 best_ppl=2.84
Epoch 28 - |param|=8.69e+02 |g_param|=2.39e+05 loss_x2y=1.2509e+00 ppl_x2y=3.49 loss_y2x=1.0593e+00 ppl_y2x=2.88 dual_loss=4.9828e-01
Validation X2Y - loss=1.3114e+00 ppl=3.71 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.1069e+00 ppl=3.02 best_loss=1.0429e+00 best_ppl=2.84
Epoch 29 - |param|=8.69e+02 |g_param|=2.44e+05 loss_x2y=1.2336e+00 ppl_x2y=3.43 loss_y2x=1.0794e+00 ppl_y2x=2.94 dual_loss=5.6552e-01
Validation X2Y - loss=1.3338e+00 ppl=3.80 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.0969e+00 ppl=2.99 best_loss=1.0429e+00 best_ppl=2.84
Epoch 30 - |param|=8.70e+02 |g_param|=2.51e+05 loss_x2y=1.3060e+00 ppl_x2y=3.69 loss_y2x=1.0541e+00 ppl_y2x=2.87 dual_loss=6.8316e-01
Validation X2Y - loss=1.3392e+00 ppl=3.82 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.0909e+00 ppl=2.98 best_loss=1.0429e+00 best_ppl=2.84
Epoch 31 - |param|=8.70e+02 |g_param|=2.44e+05 loss_x2y=1.2691e+00 ppl_x2y=3.56 loss_y2x=1.0573e+00 ppl_y2x=2.88 dual_loss=6.4932e-01
Validation X2Y - loss=1.3609e+00 ppl=3.90 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.1127e+00 ppl=3.04 best_loss=1.0429e+00 best_ppl=2.84
Epoch 32 - |param|=8.71e+02 |g_param|=2.48e+05 loss_x2y=1.2248e+00 ppl_x2y=3.40 loss_y2x=9.9912e-01 ppl_y2x=2.72 dual_loss=6.1126e-01
Validation X2Y - loss=1.3495e+00 ppl=3.86 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.1024e+00 ppl=3.01 best_loss=1.0429e+00 best_ppl=2.84
Epoch 33 - |param|=8.71e+02 |g_param|=2.52e+05 loss_x2y=1.1306e+00 ppl_x2y=3.10 loss_y2x=9.5821e-01 ppl_y2x=2.61 dual_loss=5.8290e-01
Validation X2Y - loss=1.3726e+00 ppl=3.95 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.0969e+00 ppl=2.99 best_loss=1.0429e+00 best_ppl=2.84
Epoch 34 - |param|=8.72e+02 |g_param|=4.12e+05 loss_x2y=1.0879e+00 ppl_x2y=2.97 loss_y2x=9.2635e-01 ppl_y2x=2.53 dual_loss=5.7588e-01
Validation X2Y - loss=1.3888e+00 ppl=4.01 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.1340e+00 ppl=3.11 best_loss=1.0429e+00 best_ppl=2.84
Epoch 35 - |param|=8.72e+02 |g_param|=4.88e+05 loss_x2y=1.0994e+00 ppl_x2y=3.00 loss_y2x=9.3805e-01 ppl_y2x=2.55 dual_loss=5.8698e-01
Validation X2Y - loss=1.4090e+00 ppl=4.09 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.1664e+00 ppl=3.21 best_loss=1.0429e+00 best_ppl=2.84
Epoch 36 - |param|=8.73e+02 |g_param|=5.11e+05 loss_x2y=1.0567e+00 ppl_x2y=2.88 loss_y2x=8.7215e-01 ppl_y2x=2.39 dual_loss=5.8517e-01
Validation X2Y - loss=1.4246e+00 ppl=4.16 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.1442e+00 ppl=3.14 best_loss=1.0429e+00 best_ppl=2.84
Epoch 37 - |param|=8.73e+02 |g_param|=4.88e+05 loss_x2y=1.0196e+00 ppl_x2y=2.77 loss_y2x=8.6773e-01 ppl_y2x=2.38 dual_loss=6.1929e-01
Validation X2Y - loss=1.4412e+00 ppl=4.23 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.1632e+00 ppl=3.20 best_loss=1.0429e+00 best_ppl=2.84
Epoch 38 - |param|=8.74e+02 |g_param|=5.48e+05 loss_x2y=1.0069e+00 ppl_x2y=2.74 loss_y2x=9.1157e-01 ppl_y2x=2.49 dual_loss=6.7689e-01
Validation X2Y - loss=1.4217e+00 ppl=4.14 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.1680e+00 ppl=3.22 best_loss=1.0429e+00 best_ppl=2.84
Epoch 39 - |param|=8.75e+02 |g_param|=5.00e+05 loss_x2y=9.9914e-01 ppl_x2y=2.72 loss_y2x=8.6014e-01 ppl_y2x=2.36 dual_loss=6.5512e-01
Validation X2Y - loss=1.4035e+00 ppl=4.07 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.1567e+00 ppl=3.18 best_loss=1.0429e+00 best_ppl=2.84
Epoch 40 - |param|=8.75e+02 |g_param|=5.24e+05 loss_x2y=9.9222e-01 ppl_x2y=2.70 loss_y2x=8.3577e-01 ppl_y2x=2.31 dual_loss=6.5489e-01
Validation X2Y - loss=1.4521e+00 ppl=4.27 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.2018e+00 ppl=3.33 best_loss=1.0429e+00 best_ppl=2.84
Epoch 41 - |param|=8.76e+02 |g_param|=4.84e+05 loss_x2y=9.4593e-01 ppl_x2y=2.58 loss_y2x=7.8077e-01 ppl_y2x=2.18 dual_loss=6.1232e-01
Validation X2Y - loss=1.4948e+00 ppl=4.46 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.1996e+00 ppl=3.32 best_loss=1.0429e+00 best_ppl=2.84
Epoch 42 - |param|=8.76e+02 |g_param|=5.07e+05 loss_x2y=9.4608e-01 ppl_x2y=2.58 loss_y2x=7.8629e-01 ppl_y2x=2.20 dual_loss=6.5450e-01
Validation X2Y - loss=1.4680e+00 ppl=4.34 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.2355e+00 ppl=3.44 best_loss=1.0429e+00 best_ppl=2.84
Epoch 43 - |param|=8.77e+02 |g_param|=4.98e+05 loss_x2y=9.0323e-01 ppl_x2y=2.47 loss_y2x=7.5781e-01 ppl_y2x=2.13 dual_loss=6.6361e-01
Validation X2Y - loss=1.5030e+00 ppl=4.50 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.2101e+00 ppl=3.35 best_loss=1.0429e+00 best_ppl=2.84
Epoch 44 - |param|=8.77e+02 |g_param|=5.25e+05 loss_x2y=9.9560e-01 ppl_x2y=2.71 loss_y2x=8.3404e-01 ppl_y2x=2.30 dual_loss=8.5540e-01
Validation X2Y - loss=1.5258e+00 ppl=4.60 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.2020e+00 ppl=3.33 best_loss=1.0429e+00 best_ppl=2.84
Epoch 45 - |param|=8.78e+02 |g_param|=4.98e+05 loss_x2y=9.0389e-01 ppl_x2y=2.47 loss_y2x=7.5383e-01 ppl_y2x=2.13 dual_loss=6.9336e-01
Validation X2Y - loss=1.5018e+00 ppl=4.49 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.2246e+00 ppl=3.40 best_loss=1.0429e+00 best_ppl=2.84
Epoch 46 - |param|=8.78e+02 |g_param|=5.52e+05 loss_x2y=9.5526e-01 ppl_x2y=2.60 loss_y2x=7.9027e-01 ppl_y2x=2.20 dual_loss=7.9701e-01
Validation X2Y - loss=1.4996e+00 ppl=4.48 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.2345e+00 ppl=3.44 best_loss=1.0429e+00 best_ppl=2.84
Epoch 47 - |param|=8.79e+02 |g_param|=5.11e+05 loss_x2y=9.1799e-01 ppl_x2y=2.50 loss_y2x=7.5653e-01 ppl_y2x=2.13 dual_loss=7.8556e-01
Validation X2Y - loss=1.5198e+00 ppl=4.57 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.1984e+00 ppl=3.31 best_loss=1.0429e+00 best_ppl=2.84
Epoch 48 - |param|=8.79e+02 |g_param|=5.14e+05 loss_x2y=8.4829e-01 ppl_x2y=2.34 loss_y2x=7.0022e-01 ppl_y2x=2.01 dual_loss=6.9892e-01
Validation X2Y - loss=1.5347e+00 ppl=4.64 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.2510e+00 ppl=3.49 best_loss=1.0429e+00 best_ppl=2.84
Epoch 49 - |param|=8.79e+02 |g_param|=5.08e+05 loss_x2y=8.5258e-01 ppl_x2y=2.35 loss_y2x=7.1913e-01 ppl_y2x=2.05 dual_loss=7.6438e-01
Validation X2Y - loss=1.5356e+00 ppl=4.64 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.2192e+00 ppl=3.38 best_loss=1.0429e+00 best_ppl=2.84
Epoch 50 - |param|=8.80e+02 |g_param|=5.21e+05 loss_x2y=8.5016e-01 ppl_x2y=2.34 loss_y2x=7.0183e-01 ppl_y2x=2.02 dual_loss=7.6037e-01
Validation X2Y - loss=1.5546e+00 ppl=4.73 best_loss=1.2364e+00 best_ppl=3.44                                            
Validation Y2X - loss=1.2504e+00 ppl=3.49 best_loss=1.0429e+00 best_ppl=2.84

real	16m5.034s
user	15m49.180s
sys	0m15.896s
```

testing/evaluation...  

```
/home/ye/exp/simple-nmt/model/dsl/transformer/mybk-50epoch
Evaluation result for the model: dsl-model-mybk.01.4.46-86.30.4.06-57.91.3.47-32.00.3.14-23.17.pth, mybk
BLEU = 3.54, 15.8/4.2/2.2/1.1 (BP=1.000, ratio=1.128, hyp_len=12898, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.46-86.30.4.06-57.91.3.47-32.00.3.14-23.17.pth, bkmy
BLEU = 4.70, 32.2/9.5/3.0/1.0 (BP=0.848, ratio=0.859, hyp_len=10504, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.02.3.66-38.96.3.28-26.65.2.97-19.52.2.68-14.54.pth, mybk
BLEU = 2.81, 12.4/3.8/1.6/0.8 (BP=1.000, ratio=1.868, hyp_len=21355, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.3.66-38.96.3.28-26.65.2.97-19.52.2.68-14.54.pth, bkmy
BLEU = 6.16, 37.7/13.4/4.4/1.2 (BP=0.848, ratio=0.858, hyp_len=10497, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.3.23-25.21.2.84-17.13.2.55-12.75.2.31-10.11.pth, mybk
BLEU = 5.99, 25.0/8.7/3.6/1.6 (BP=1.000, ratio=1.152, hyp_len=13166, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.3.23-25.21.2.84-17.13.2.55-12.75.2.31-10.11.pth, bkmy
BLEU = 10.44, 40.4/16.5/7.1/2.9 (BP=0.963, ratio=0.963, hyp_len=11781, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.3.00-20.15.2.61-13.66.2.29-9.87.2.08-8.02.pth, mybk
BLEU = 6.11, 20.9/8.6/4.1/1.9 (BP=1.000, ratio=1.721, hyp_len=19673, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.3.00-20.15.2.61-13.66.2.29-9.87.2.08-8.02.pth, bkmy
BLEU = 10.72, 34.2/15.7/7.1/3.5 (BP=1.000, ratio=1.212, hyp_len=14818, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.2.73-15.35.2.40-11.04.2.04-7.66.1.81-6.12.pth, mybk
BLEU = 11.11, 32.0/14.6/7.8/4.2 (BP=1.000, ratio=1.273, hyp_len=14548, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.2.73-15.35.2.40-11.04.2.04-7.66.1.81-6.12.pth, bkmy
BLEU = 12.42, 34.0/16.9/8.8/4.7 (BP=1.000, ratio=1.395, hyp_len=17063, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.2.62-13.80.2.30-9.93.1.85-6.38.1.65-5.22.pth, mybk
BLEU = 18.81, 45.7/23.7/13.9/8.3 (BP=1.000, ratio=1.009, hyp_len=11530, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.2.62-13.80.2.30-9.93.1.85-6.38.1.65-5.22.pth, bkmy
BLEU = 17.86, 41.5/22.9/13.3/8.0 (BP=1.000, ratio=1.273, hyp_len=15576, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.2.46-11.76.2.16-8.69.1.73-5.66.1.57-4.81.pth, mybk
BLEU = 22.55, 51.3/28.0/17.3/11.1 (BP=0.982, ratio=0.983, hyp_len=11232, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.2.46-11.76.2.16-8.69.1.73-5.66.1.57-4.81.pth, bkmy
BLEU = 22.29, 49.0/28.2/16.9/10.6 (BP=1.000, ratio=1.137, hyp_len=13901, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.2.32-10.15.2.02-7.55.1.58-4.87.1.46-4.31.pth, mybk
BLEU = 23.88, 51.8/29.4/18.3/11.7 (BP=1.000, ratio=1.025, hyp_len=11718, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.2.32-10.15.2.02-7.55.1.58-4.87.1.46-4.31.pth, bkmy
BLEU = 22.15, 46.0/27.6/17.1/11.1 (BP=1.000, ratio=1.282, hyp_len=15686, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.2.18-8.82.1.89-6.65.1.49-4.45.1.31-3.72.pth, mybk
BLEU = 26.36, 55.8/32.4/20.8/14.2 (BP=0.976, ratio=0.976, hyp_len=11157, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.2.18-8.82.1.89-6.65.1.49-4.45.1.31-3.72.pth, bkmy
BLEU = 29.62, 57.2/36.0/23.5/15.9 (BP=1.000, ratio=1.071, hyp_len=13104, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.2.16-8.70.1.90-6.68.1.46-4.31.1.26-3.52.pth, mybk
BLEU = 27.76, 55.4/33.1/21.8/14.9 (BP=1.000, ratio=1.041, hyp_len=11898, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.2.16-8.70.1.90-6.68.1.46-4.31.1.26-3.52.pth, bkmy
BLEU = 34.63, 62.3/41.1/28.2/20.0 (BP=0.999, ratio=0.999, hyp_len=12213, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.2.01-7.45.1.73-5.66.1.38-3.99.1.24-3.45.pth, mybk
BLEU = 26.52, 51.9/31.7/20.9/14.4 (BP=1.000, ratio=1.137, hyp_len=12997, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.2.01-7.45.1.73-5.66.1.38-3.99.1.24-3.45.pth, bkmy
BLEU = 31.15, 56.5/36.9/25.2/17.9 (BP=1.000, ratio=1.137, hyp_len=13901, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.2.06-7.83.1.73-5.65.1.36-3.90.1.18-3.26.pth, mybk
BLEU = 29.49, 57.0/35.0/23.4/16.2 (BP=1.000, ratio=1.060, hyp_len=12117, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.2.06-7.83.1.73-5.65.1.36-3.90.1.18-3.26.pth, bkmy
BLEU = 35.94, 62.7/42.2/29.5/21.4 (BP=1.000, ratio=1.027, hyp_len=12564, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.1.95-7.04.1.67-5.30.1.34-3.81.1.14-3.14.pth, mybk
BLEU = 29.89, 57.0/35.4/23.9/16.6 (BP=1.000, ratio=1.057, hyp_len=12086, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.1.95-7.04.1.67-5.30.1.34-3.81.1.14-3.14.pth, bkmy
BLEU = 39.00, 65.7/45.6/32.4/23.9 (BP=0.999, ratio=0.999, hyp_len=12219, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.1.88-6.55.1.62-5.06.1.32-3.75.1.13-3.10.pth, mybk
BLEU = 31.21, 59.1/37.2/24.9/17.3 (BP=1.000, ratio=1.064, hyp_len=12160, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.1.88-6.55.1.62-5.06.1.32-3.75.1.13-3.10.pth, bkmy
BLEU = 38.85, 65.2/45.2/32.2/24.0 (BP=1.000, ratio=1.015, hyp_len=12412, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.1.77-5.87.1.51-4.53.1.32-3.75.1.12-3.08.pth, mybk
BLEU = 31.94, 59.5/37.8/25.6/18.0 (BP=1.000, ratio=1.056, hyp_len=12068, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.1.77-5.87.1.51-4.53.1.32-3.75.1.12-3.08.pth, bkmy
BLEU = 38.62, 65.2/45.0/32.3/24.0 (BP=0.995, ratio=0.995, hyp_len=12166, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.1.79-5.98.1.56-4.76.1.31-3.70.1.11-3.02.pth, mybk
BLEU = 33.26, 61.2/39.2/26.7/19.1 (BP=1.000, ratio=1.024, hyp_len=11707, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.1.79-5.98.1.56-4.76.1.31-3.70.1.11-3.02.pth, bkmy
BLEU = 39.92, 66.0/46.1/33.5/24.9 (BP=1.000, ratio=1.034, hyp_len=12646, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.1.68-5.37.1.50-4.49.1.27-3.57.1.08-2.94.pth, mybk
BLEU = 34.94, 63.7/41.1/28.6/20.7 (BP=0.991, ratio=0.991, hyp_len=11327, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.1.68-5.37.1.50-4.49.1.27-3.57.1.08-2.94.pth, bkmy
BLEU = 38.14, 63.9/44.3/31.9/23.5 (BP=1.000, ratio=1.079, hyp_len=13193, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.1.69-5.44.1.42-4.14.1.28-3.59.1.06-2.90.pth, mybk
BLEU = 32.47, 59.2/38.1/26.3/18.8 (BP=1.000, ratio=1.092, hyp_len=12480, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.1.69-5.44.1.42-4.14.1.28-3.59.1.06-2.90.pth, bkmy
BLEU = 39.40, 64.7/45.6/33.1/24.7 (BP=1.000, ratio=1.089, hyp_len=13324, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.1.56-4.75.1.34-3.80.1.24-3.44.1.04-2.84.pth, mybk
BLEU = 33.71, 60.8/39.4/27.3/19.7 (BP=1.000, ratio=1.059, hyp_len=12111, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.1.56-4.75.1.34-3.80.1.24-3.44.1.04-2.84.pth, bkmy
BLEU = 41.50, 66.9/47.8/35.0/26.5 (BP=1.000, ratio=1.032, hyp_len=12623, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.1.44-4.22.1.24-3.46.1.28-3.60.1.10-3.01.pth, mybk
BLEU = 34.05, 60.8/39.5/27.7/20.2 (BP=1.000, ratio=1.057, hyp_len=12083, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.1.44-4.22.1.24-3.46.1.28-3.60.1.10-3.01.pth, bkmy
BLEU = 38.72, 63.8/44.8/32.5/24.2 (BP=1.000, ratio=1.094, hyp_len=13383, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.1.53-4.61.1.33-3.77.1.30-3.67.1.06-2.89.pth, mybk
BLEU = 34.27, 61.6/40.0/27.9/20.0 (BP=1.000, ratio=1.043, hyp_len=11925, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.1.53-4.61.1.33-3.77.1.30-3.67.1.06-2.89.pth, bkmy
BLEU = 41.24, 67.1/47.6/34.6/26.1 (BP=1.000, ratio=1.027, hyp_len=12560, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.1.44-4.20.1.23-3.42.1.30-3.66.1.10-2.99.pth, mybk
BLEU = 33.49, 60.9/39.2/27.1/19.4 (BP=1.000, ratio=1.043, hyp_len=11929, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.1.44-4.20.1.23-3.42.1.30-3.66.1.10-2.99.pth, bkmy
BLEU = 41.06, 67.0/47.4/34.5/26.0 (BP=1.000, ratio=1.038, hyp_len=12690, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.1.46-4.29.1.28-3.59.1.31-3.71.1.09-2.96.pth, mybk
BLEU = 34.11, 60.6/39.8/27.9/20.1 (BP=1.000, ratio=1.078, hyp_len=12326, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.1.46-4.29.1.28-3.59.1.31-3.71.1.09-2.96.pth, bkmy
BLEU = 40.64, 65.7/46.7/34.3/25.9 (BP=1.000, ratio=1.069, hyp_len=13075, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.1.38-3.96.1.16-3.20.1.33-3.77.1.10-3.00.pth, mybk
BLEU = 33.84, 60.6/39.3/27.5/20.0 (BP=1.000, ratio=1.067, hyp_len=12200, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.1.38-3.96.1.16-3.20.1.33-3.77.1.10-3.00.pth, bkmy
BLEU = 40.09, 65.3/46.0/33.7/25.5 (BP=1.000, ratio=1.054, hyp_len=12896, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.1.35-3.84.1.19-3.27.1.32-3.73.1.08-2.96.pth, mybk
BLEU = 32.59, 59.8/38.0/26.3/18.8 (BP=1.000, ratio=1.077, hyp_len=12316, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.1.35-3.84.1.19-3.27.1.32-3.73.1.08-2.96.pth, bkmy
BLEU = 40.97, 66.5/47.0/34.5/26.1 (BP=1.000, ratio=1.043, hyp_len=12751, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.1.29-3.62.1.09-2.96.1.32-3.75.1.08-2.95.pth, mybk
BLEU = 32.59, 58.9/37.9/26.3/19.2 (BP=1.000, ratio=1.103, hyp_len=12611, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.1.29-3.62.1.09-2.96.1.32-3.75.1.08-2.95.pth, bkmy
BLEU = 41.37, 67.0/47.3/34.8/26.5 (BP=1.000, ratio=1.041, hyp_len=12734, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.1.27-3.55.1.06-2.88.1.33-3.79.1.11-3.04.pth, mybk
BLEU = 32.94, 60.0/38.4/26.6/19.2 (BP=1.000, ratio=1.043, hyp_len=11918, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.1.27-3.55.1.06-2.88.1.33-3.79.1.11-3.04.pth, bkmy
BLEU = 40.06, 66.3/46.3/33.5/25.0 (BP=1.000, ratio=1.030, hyp_len=12597, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.1.25-3.49.1.06-2.88.1.31-3.71.1.11-3.02.pth, mybk
BLEU = 34.70, 61.9/40.4/28.2/20.6 (BP=1.000, ratio=1.048, hyp_len=11981, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.1.25-3.49.1.06-2.88.1.31-3.71.1.11-3.02.pth, bkmy
BLEU = 39.12, 64.5/45.5/32.7/24.4 (BP=1.000, ratio=1.077, hyp_len=13176, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.1.23-3.43.1.08-2.94.1.33-3.80.1.10-2.99.pth, mybk
BLEU = 33.78, 61.2/39.6/27.3/19.7 (BP=1.000, ratio=1.075, hyp_len=12289, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.1.23-3.43.1.08-2.94.1.33-3.80.1.10-2.99.pth, bkmy
BLEU = 41.09, 67.4/47.3/34.4/26.0 (BP=1.000, ratio=1.036, hyp_len=12674, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.1.31-3.69.1.05-2.87.1.34-3.82.1.09-2.98.pth, mybk
BLEU = 33.88, 61.5/39.5/27.4/19.8 (BP=1.000, ratio=1.055, hyp_len=12063, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.1.31-3.69.1.05-2.87.1.34-3.82.1.09-2.98.pth, bkmy
BLEU = 38.92, 65.3/45.4/32.4/23.9 (BP=1.000, ratio=1.073, hyp_len=13127, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.31.1.27-3.56.1.06-2.88.1.36-3.90.1.11-3.04.pth, mybk
BLEU = 34.18, 61.2/39.6/27.7/20.3 (BP=1.000, ratio=1.043, hyp_len=11919, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.31.1.27-3.56.1.06-2.88.1.36-3.90.1.11-3.04.pth, bkmy
BLEU = 38.50, 63.7/44.6/32.2/24.1 (BP=1.000, ratio=1.096, hyp_len=13410, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.32.1.22-3.40.1.00-2.72.1.35-3.86.1.10-3.01.pth, mybk
BLEU = 34.95, 62.3/40.3/28.5/20.9 (BP=1.000, ratio=1.035, hyp_len=11834, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.32.1.22-3.40.1.00-2.72.1.35-3.86.1.10-3.01.pth, bkmy
BLEU = 41.27, 67.4/47.6/34.8/26.0 (BP=1.000, ratio=1.041, hyp_len=12730, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.33.1.13-3.10.0.96-2.61.1.37-3.95.1.10-2.99.pth, mybk
BLEU = 32.46, 58.9/37.7/26.3/19.0 (BP=1.000, ratio=1.078, hyp_len=12327, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.33.1.13-3.10.0.96-2.61.1.37-3.95.1.10-2.99.pth, bkmy
BLEU = 39.73, 65.4/45.8/33.3/25.0 (BP=1.000, ratio=1.059, hyp_len=12954, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.34.1.09-2.97.0.93-2.53.1.39-4.01.1.13-3.11.pth, mybk
BLEU = 34.31, 61.3/39.9/27.8/20.3 (BP=1.000, ratio=1.062, hyp_len=12140, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.34.1.09-2.97.0.93-2.53.1.39-4.01.1.13-3.11.pth, bkmy
BLEU = 37.34, 63.0/43.4/31.1/22.9 (BP=1.000, ratio=1.112, hyp_len=13606, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.35.1.10-3.00.0.94-2.55.1.41-4.09.1.17-3.21.pth, mybk
BLEU = 33.80, 61.3/39.3/27.3/19.9 (BP=1.000, ratio=1.047, hyp_len=11964, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.35.1.10-3.00.0.94-2.55.1.41-4.09.1.17-3.21.pth, bkmy
BLEU = 37.71, 63.7/44.0/31.4/23.0 (BP=1.000, ratio=1.109, hyp_len=13568, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.36.1.06-2.88.0.87-2.39.1.42-4.16.1.14-3.14.pth, mybk
BLEU = 34.04, 61.4/39.4/27.5/20.2 (BP=1.000, ratio=1.031, hyp_len=11791, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.36.1.06-2.88.0.87-2.39.1.42-4.16.1.14-3.14.pth, bkmy
BLEU = 39.98, 65.9/46.1/33.5/25.1 (BP=1.000, ratio=1.032, hyp_len=12624, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.37.1.02-2.77.0.87-2.38.1.44-4.23.1.16-3.20.pth, mybk
BLEU = 32.20, 59.1/37.5/26.0/18.7 (BP=1.000, ratio=1.067, hyp_len=12203, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.37.1.02-2.77.0.87-2.38.1.44-4.23.1.16-3.20.pth, bkmy
BLEU = 41.00, 67.2/47.3/34.3/25.9 (BP=1.000, ratio=1.022, hyp_len=12499, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.38.1.01-2.74.0.91-2.49.1.42-4.14.1.17-3.22.pth, mybk
BLEU = 31.95, 58.5/37.3/25.8/18.5 (BP=1.000, ratio=1.088, hyp_len=12443, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.38.1.01-2.74.0.91-2.49.1.42-4.14.1.17-3.22.pth, bkmy
BLEU = 36.56, 61.6/42.0/30.3/22.8 (BP=1.000, ratio=1.083, hyp_len=13250, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.39.1.00-2.72.0.86-2.36.1.40-4.07.1.16-3.18.pth, mybk
BLEU = 32.67, 60.0/38.2/26.4/18.8 (BP=1.000, ratio=1.064, hyp_len=12161, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.39.1.00-2.72.0.86-2.36.1.40-4.07.1.16-3.18.pth, bkmy
BLEU = 39.06, 65.0/45.3/32.6/24.2 (BP=1.000, ratio=1.062, hyp_len=12990, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.40.0.99-2.70.0.84-2.31.1.45-4.27.1.20-3.33.pth, mybk
BLEU = 32.66, 59.4/38.1/26.3/19.1 (BP=1.000, ratio=1.060, hyp_len=12121, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.40.0.99-2.70.0.84-2.31.1.45-4.27.1.20-3.33.pth, bkmy
BLEU = 39.14, 64.8/45.1/32.7/24.5 (BP=1.000, ratio=1.050, hyp_len=12841, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.41.0.95-2.58.0.78-2.18.1.49-4.46.1.20-3.32.pth, mybk
BLEU = 30.54, 57.5/35.9/24.3/17.4 (BP=1.000, ratio=1.094, hyp_len=12502, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.41.0.95-2.58.0.78-2.18.1.49-4.46.1.20-3.32.pth, bkmy
BLEU = 38.03, 63.9/44.1/31.7/23.5 (BP=1.000, ratio=1.062, hyp_len=12995, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.42.0.95-2.58.0.79-2.20.1.47-4.34.1.24-3.44.pth, mybk
BLEU = 33.01, 60.3/38.7/26.6/19.1 (BP=1.000, ratio=1.054, hyp_len=12046, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.42.0.95-2.58.0.79-2.20.1.47-4.34.1.24-3.44.pth, bkmy
BLEU = 40.10, 66.1/46.1/33.6/25.3 (BP=1.000, ratio=1.028, hyp_len=12569, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.43.0.90-2.47.0.76-2.13.1.50-4.50.1.21-3.35.pth, mybk
BLEU = 31.53, 58.3/37.0/25.3/18.1 (BP=1.000, ratio=1.107, hyp_len=12660, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.43.0.90-2.47.0.76-2.13.1.50-4.50.1.21-3.35.pth, bkmy
BLEU = 37.81, 63.5/43.8/31.4/23.4 (BP=1.000, ratio=1.082, hyp_len=13230, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.44.1.00-2.71.0.83-2.30.1.53-4.60.1.20-3.33.pth, mybk
BLEU = 32.14, 59.5/37.5/25.8/18.6 (BP=1.000, ratio=1.057, hyp_len=12087, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.44.1.00-2.71.0.83-2.30.1.53-4.60.1.20-3.33.pth, bkmy
BLEU = 36.97, 62.0/42.9/30.9/22.7 (BP=1.000, ratio=1.113, hyp_len=13609, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.45.0.90-2.47.0.75-2.13.1.50-4.49.1.22-3.40.pth, mybk
BLEU = 32.45, 59.8/37.9/26.1/18.7 (BP=1.000, ratio=1.055, hyp_len=12062, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.45.0.90-2.47.0.75-2.13.1.50-4.49.1.22-3.40.pth, bkmy
BLEU = 40.37, 66.2/46.3/33.8/25.6 (BP=1.000, ratio=1.023, hyp_len=12514, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.46.0.96-2.60.0.79-2.20.1.50-4.48.1.23-3.44.pth, mybk
BLEU = 31.61, 58.1/36.8/25.4/18.4 (BP=1.000, ratio=1.071, hyp_len=12247, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.46.0.96-2.60.0.79-2.20.1.50-4.48.1.23-3.44.pth, bkmy
BLEU = 36.36, 62.0/42.2/30.0/22.3 (BP=1.000, ratio=1.088, hyp_len=13302, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.47.0.92-2.50.0.76-2.13.1.52-4.57.1.20-3.31.pth, mybk
BLEU = 30.68, 56.8/35.7/24.6/17.8 (BP=1.000, ratio=1.097, hyp_len=12542, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.47.0.92-2.50.0.76-2.13.1.52-4.57.1.20-3.31.pth, bkmy
BLEU = 38.78, 64.7/44.8/32.2/24.2 (BP=1.000, ratio=1.067, hyp_len=13050, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.48.0.85-2.34.0.70-2.01.1.53-4.64.1.25-3.49.pth, mybk
BLEU = 32.29, 59.4/37.7/25.9/18.8 (BP=1.000, ratio=1.066, hyp_len=12183, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.48.0.85-2.34.0.70-2.01.1.53-4.64.1.25-3.49.pth, bkmy
BLEU = 36.54, 62.4/42.5/30.2/22.3 (BP=1.000, ratio=1.090, hyp_len=13332, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.49.0.85-2.35.0.72-2.05.1.54-4.64.1.22-3.38.pth, mybk
BLEU = 31.21, 58.3/36.4/25.0/17.9 (BP=1.000, ratio=1.071, hyp_len=12245, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.49.0.85-2.35.0.72-2.05.1.54-4.64.1.22-3.38.pth, bkmy
BLEU = 38.94, 64.2/44.8/32.6/24.5 (BP=1.000, ratio=1.057, hyp_len=12929, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.50.0.85-2.34.0.70-2.02.1.55-4.73.1.25-3.49.pth, mybk
BLEU = 31.68, 58.3/36.8/25.3/18.5 (BP=1.000, ratio=1.068, hyp_len=12215, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.50.0.85-2.34.0.70-2.02.1.55-4.73.1.25-3.49.pth, bkmy
BLEU = 36.79, 62.4/42.4/30.5/22.7 (BP=1.000, ratio=1.065, hyp_len=13020, ref_len=12231)
```

Best model for my-bk က epoch 32 မော်ဒယ် ဖြစ်ပြီးတော့၊ Best BLEU Score က : 34.95  
Best model for bk-my က epoch 19 မော်ဒယ် ဖြစ်ပြီးတော့၊ Best BLEU Score က : 41.50  

## Transformer-DSL, 60 epoch

```
Epoch 1 - |param|=8.52e+02 |g_param|=2.80e+05 loss_x2y=4.3963e+00 ppl_x2y=81.15 loss_y2x=4.0578e+00 ppl_y2x=57.85 dual_loss=0.0000e+00
Validation X2Y - loss=3.5003e+00 ppl=33.12 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=3.1050e+00 ppl=22.31 best_loss=inf best_ppl=inf
Epoch 2 - |param|=8.53e+02 |g_param|=2.67e+05 loss_x2y=3.6236e+00 ppl_x2y=37.47 loss_y2x=3.1728e+00 ppl_y2x=23.87 dual_loss=0.0000e+00
Validation X2Y - loss=3.0429e+00 ppl=20.97 best_loss=3.5003e+00 best_ppl=33.12                                          
Validation Y2X - loss=2.7876e+00 ppl=16.24 best_loss=3.1050e+00 best_ppl=22.31
Epoch 3 - |param|=8.54e+02 |g_param|=2.54e+05 loss_x2y=3.2871e+00 ppl_x2y=26.77 loss_y2x=2.8771e+00 ppl_y2x=17.76 dual_loss=0.0000e+00
Validation X2Y - loss=2.6872e+00 ppl=14.69 best_loss=3.0429e+00 best_ppl=20.97                                          
Validation Y2X - loss=2.3651e+00 ppl=10.65 best_loss=2.7876e+00 best_ppl=16.24
Epoch 4 - |param|=8.54e+02 |g_param|=2.70e+05 loss_x2y=2.9697e+00 ppl_x2y=19.49 loss_y2x=2.5984e+00 ppl_y2x=13.44 dual_loss=0.0000e+00
Validation X2Y - loss=2.3143e+00 ppl=10.12 best_loss=2.6872e+00 best_ppl=14.69                                          
Validation Y2X - loss=2.1272e+00 ppl=8.39 best_loss=2.3651e+00 best_ppl=10.65
Epoch 5 - |param|=8.55e+02 |g_param|=2.87e+05 loss_x2y=2.8859e+00 ppl_x2y=17.92 loss_y2x=2.4785e+00 ppl_y2x=11.92 dual_loss=0.0000e+00
Validation X2Y - loss=2.0924e+00 ppl=8.10 best_loss=2.3143e+00 best_ppl=10.12                                           
Validation Y2X - loss=1.8800e+00 ppl=6.55 best_loss=2.1272e+00 best_ppl=8.39
Epoch 6 - |param|=8.55e+02 |g_param|=3.00e+05 loss_x2y=2.6046e+00 ppl_x2y=13.53 loss_y2x=2.2215e+00 ppl_y2x=9.22 dual_loss=0.0000e+00
Validation X2Y - loss=1.8706e+00 ppl=6.49 best_loss=2.0924e+00 best_ppl=8.10                                            
Validation Y2X - loss=1.6742e+00 ppl=5.33 best_loss=1.8800e+00 best_ppl=6.55
Epoch 7 - |param|=8.56e+02 |g_param|=3.01e+05 loss_x2y=2.4294e+00 ppl_x2y=11.35 loss_y2x=2.1017e+00 ppl_y2x=8.18 dual_loss=0.0000e+00
Validation X2Y - loss=1.7125e+00 ppl=5.54 best_loss=1.8706e+00 best_ppl=6.49                                            
Validation Y2X - loss=1.5706e+00 ppl=4.81 best_loss=1.6742e+00 best_ppl=5.33
Epoch 8 - |param|=8.57e+02 |g_param|=3.33e+05 loss_x2y=2.3586e+00 ppl_x2y=10.58 loss_y2x=2.0300e+00 ppl_y2x=7.61 dual_loss=0.0000e+00
Validation X2Y - loss=1.6182e+00 ppl=5.04 best_loss=1.7125e+00 best_ppl=5.54                                            
Validation Y2X - loss=1.4171e+00 ppl=4.12 best_loss=1.5706e+00 best_ppl=4.81
Epoch 9 - |param|=8.57e+02 |g_param|=3.37e+05 loss_x2y=2.3744e+00 ppl_x2y=10.74 loss_y2x=1.9973e+00 ppl_y2x=7.37 dual_loss=0.0000e+00
Validation X2Y - loss=1.5134e+00 ppl=4.54 best_loss=1.6182e+00 best_ppl=5.04                                            
Validation Y2X - loss=1.3386e+00 ppl=3.81 best_loss=1.4171e+00 best_ppl=4.12
Epoch 10 - |param|=8.58e+02 |g_param|=3.63e+05 loss_x2y=2.1752e+00 ppl_x2y=8.80 loss_y2x=1.9055e+00 ppl_y2x=6.72 dual_loss=0.0000e+00
Validation X2Y - loss=1.4325e+00 ppl=4.19 best_loss=1.5134e+00 best_ppl=4.54                                            
Validation Y2X - loss=1.2949e+00 ppl=3.65 best_loss=1.3386e+00 best_ppl=3.81
Epoch 11 - |param|=8.58e+02 |g_param|=3.57e+05 loss_x2y=2.1978e+00 ppl_x2y=9.01 loss_y2x=1.8296e+00 ppl_y2x=6.23 dual_loss=0.0000e+00
Validation X2Y - loss=1.3989e+00 ppl=4.05 best_loss=1.4325e+00 best_ppl=4.19                                            
Validation Y2X - loss=1.2547e+00 ppl=3.51 best_loss=1.2949e+00 best_ppl=3.65
Epoch 12 - |param|=8.59e+02 |g_param|=3.84e+05 loss_x2y=1.9643e+00 ppl_x2y=7.13 loss_y2x=1.6695e+00 ppl_y2x=5.31 dual_loss=0.0000e+00
Validation X2Y - loss=1.3634e+00 ppl=3.91 best_loss=1.3989e+00 best_ppl=4.05                                            
Validation Y2X - loss=1.2006e+00 ppl=3.32 best_loss=1.2547e+00 best_ppl=3.51
Epoch 13 - |param|=8.59e+02 |g_param|=3.63e+05 loss_x2y=1.8588e+00 ppl_x2y=6.42 loss_y2x=1.5763e+00 ppl_y2x=4.84 dual_loss=0.0000e+00
Validation X2Y - loss=1.3090e+00 ppl=3.70 best_loss=1.3634e+00 best_ppl=3.91                                            
Validation Y2X - loss=1.1847e+00 ppl=3.27 best_loss=1.2006e+00 best_ppl=3.32
Epoch 14 - |param|=8.60e+02 |g_param|=3.88e+05 loss_x2y=1.8080e+00 ppl_x2y=6.10 loss_y2x=1.5426e+00 ppl_y2x=4.68 dual_loss=0.0000e+00
Validation X2Y - loss=1.3116e+00 ppl=3.71 best_loss=1.3090e+00 best_ppl=3.70                                            
Validation Y2X - loss=1.1382e+00 ppl=3.12 best_loss=1.1847e+00 best_ppl=3.27
Epoch 15 - |param|=8.60e+02 |g_param|=3.89e+05 loss_x2y=1.8045e+00 ppl_x2y=6.08 loss_y2x=1.5351e+00 ppl_y2x=4.64 dual_loss=0.0000e+00
Validation X2Y - loss=1.2970e+00 ppl=3.66 best_loss=1.3090e+00 best_ppl=3.70                                            
Validation Y2X - loss=1.1124e+00 ppl=3.04 best_loss=1.1382e+00 best_ppl=3.12
Epoch 16 - |param|=8.61e+02 |g_param|=4.13e+05 loss_x2y=1.7216e+00 ppl_x2y=5.59 loss_y2x=1.4695e+00 ppl_y2x=4.35 dual_loss=0.0000e+00
Validation X2Y - loss=1.2822e+00 ppl=3.60 best_loss=1.2970e+00 best_ppl=3.66                                            
Validation Y2X - loss=1.0885e+00 ppl=2.97 best_loss=1.1124e+00 best_ppl=3.04
Epoch 17 - |param|=8.61e+02 |g_param|=3.98e+05 loss_x2y=1.5981e+00 ppl_x2y=4.94 loss_y2x=1.3655e+00 ppl_y2x=3.92 dual_loss=0.0000e+00
Validation X2Y - loss=1.2762e+00 ppl=3.58 best_loss=1.2822e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1054e+00 ppl=3.02 best_loss=1.0885e+00 best_ppl=2.97
Epoch 18 - |param|=8.62e+02 |g_param|=4.28e+05 loss_x2y=1.6285e+00 ppl_x2y=5.10 loss_y2x=1.3814e+00 ppl_y2x=3.98 dual_loss=0.0000e+00
Validation X2Y - loss=1.2690e+00 ppl=3.56 best_loss=1.2762e+00 best_ppl=3.58                                            
Validation Y2X - loss=1.1078e+00 ppl=3.03 best_loss=1.0885e+00 best_ppl=2.97
Epoch 19 - |param|=8.63e+02 |g_param|=4.13e+05 loss_x2y=1.5601e+00 ppl_x2y=4.76 loss_y2x=1.3224e+00 ppl_y2x=3.75 dual_loss=0.0000e+00
Validation X2Y - loss=1.2431e+00 ppl=3.47 best_loss=1.2690e+00 best_ppl=3.56                                            
Validation Y2X - loss=1.0930e+00 ppl=2.98 best_loss=1.0885e+00 best_ppl=2.97
Epoch 20 - |param|=8.63e+02 |g_param|=4.28e+05 loss_x2y=1.5034e+00 ppl_x2y=4.50 loss_y2x=1.2731e+00 ppl_y2x=3.57 dual_loss=0.0000e+00
Validation X2Y - loss=1.2847e+00 ppl=3.61 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.1117e+00 ppl=3.04 best_loss=1.0885e+00 best_ppl=2.97
Epoch 21 - |param|=8.64e+02 |g_param|=4.30e+05 loss_x2y=1.5698e+00 ppl_x2y=4.81 loss_y2x=1.3066e+00 ppl_y2x=3.69 dual_loss=6.2438e-01
Validation X2Y - loss=1.2611e+00 ppl=3.53 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.0718e+00 ppl=2.92 best_loss=1.0885e+00 best_ppl=2.97
Epoch 22 - |param|=8.64e+02 |g_param|=4.43e+05 loss_x2y=1.4420e+00 ppl_x2y=4.23 loss_y2x=1.2102e+00 ppl_y2x=3.35 dual_loss=5.3343e-01
Validation X2Y - loss=1.2641e+00 ppl=3.54 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.0563e+00 ppl=2.88 best_loss=1.0718e+00 best_ppl=2.92
Epoch 23 - |param|=8.65e+02 |g_param|=4.43e+05 loss_x2y=1.4226e+00 ppl_x2y=4.15 loss_y2x=1.2014e+00 ppl_y2x=3.32 dual_loss=4.8790e-01
Validation X2Y - loss=1.2598e+00 ppl=3.52 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.0851e+00 ppl=2.96 best_loss=1.0563e+00 best_ppl=2.88
Epoch 24 - |param|=8.65e+02 |g_param|=4.51e+05 loss_x2y=1.3318e+00 ppl_x2y=3.79 loss_y2x=1.1371e+00 ppl_y2x=3.12 dual_loss=4.5614e-01
Validation X2Y - loss=1.2633e+00 ppl=3.54 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.0708e+00 ppl=2.92 best_loss=1.0563e+00 best_ppl=2.88
Epoch 25 - |param|=8.66e+02 |g_param|=4.49e+05 loss_x2y=1.3306e+00 ppl_x2y=3.78 loss_y2x=1.1204e+00 ppl_y2x=3.07 dual_loss=4.9983e-01
Validation X2Y - loss=1.2709e+00 ppl=3.56 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.0892e+00 ppl=2.97 best_loss=1.0563e+00 best_ppl=2.88
Epoch 26 - |param|=8.66e+02 |g_param|=5.14e+05 loss_x2y=1.3202e+00 ppl_x2y=3.74 loss_y2x=1.1079e+00 ppl_y2x=3.03 dual_loss=5.1610e-01
Validation X2Y - loss=1.2967e+00 ppl=3.66 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.0896e+00 ppl=2.97 best_loss=1.0563e+00 best_ppl=2.88
Epoch 27 - |param|=8.67e+02 |g_param|=4.64e+05 loss_x2y=1.2364e+00 ppl_x2y=3.44 loss_y2x=1.0591e+00 ppl_y2x=2.88 dual_loss=4.9642e-01
Validation X2Y - loss=1.2639e+00 ppl=3.54 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.0748e+00 ppl=2.93 best_loss=1.0563e+00 best_ppl=2.88
Epoch 28 - |param|=8.67e+02 |g_param|=4.81e+05 loss_x2y=1.2590e+00 ppl_x2y=3.52 loss_y2x=1.0510e+00 ppl_y2x=2.86 dual_loss=5.4207e-01
Validation X2Y - loss=1.3001e+00 ppl=3.67 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.0794e+00 ppl=2.94 best_loss=1.0563e+00 best_ppl=2.88
Epoch 29 - |param|=8.68e+02 |g_param|=4.70e+05 loss_x2y=1.2025e+00 ppl_x2y=3.33 loss_y2x=1.0041e+00 ppl_y2x=2.73 dual_loss=5.1635e-01
Validation X2Y - loss=1.3170e+00 ppl=3.73 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.0966e+00 ppl=2.99 best_loss=1.0563e+00 best_ppl=2.88
Epoch 30 - |param|=8.68e+02 |g_param|=4.89e+05 loss_x2y=1.2571e+00 ppl_x2y=3.52 loss_y2x=1.0542e+00 ppl_y2x=2.87 dual_loss=5.6067e-01
Validation X2Y - loss=1.3207e+00 ppl=3.75 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.0863e+00 ppl=2.96 best_loss=1.0563e+00 best_ppl=2.88
Epoch 31 - |param|=8.69e+02 |g_param|=4.75e+05 loss_x2y=1.1614e+00 ppl_x2y=3.19 loss_y2x=9.6861e-01 ppl_y2x=2.63 dual_loss=5.3018e-01
Validation X2Y - loss=1.3137e+00 ppl=3.72 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.0790e+00 ppl=2.94 best_loss=1.0563e+00 best_ppl=2.88
Epoch 32 - |param|=8.69e+02 |g_param|=4.83e+05 loss_x2y=1.1473e+00 ppl_x2y=3.15 loss_y2x=9.9174e-01 ppl_y2x=2.70 dual_loss=6.0325e-01
Validation X2Y - loss=1.3330e+00 ppl=3.79 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.0910e+00 ppl=2.98 best_loss=1.0563e+00 best_ppl=2.88
Epoch 33 - |param|=8.70e+02 |g_param|=8.31e+05 loss_x2y=1.1635e+00 ppl_x2y=3.20 loss_y2x=9.5459e-01 ppl_y2x=2.60 dual_loss=6.0414e-01
Validation X2Y - loss=1.3572e+00 ppl=3.89 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.1019e+00 ppl=3.01 best_loss=1.0563e+00 best_ppl=2.88
Epoch 34 - |param|=8.70e+02 |g_param|=8.38e+05 loss_x2y=1.1026e+00 ppl_x2y=3.01 loss_y2x=9.3115e-01 ppl_y2x=2.54 dual_loss=6.1662e-01
Validation X2Y - loss=1.3581e+00 ppl=3.89 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.1053e+00 ppl=3.02 best_loss=1.0563e+00 best_ppl=2.88
Epoch 35 - |param|=8.71e+02 |g_param|=7.93e+05 loss_x2y=1.1437e+00 ppl_x2y=3.14 loss_y2x=9.3726e-01 ppl_y2x=2.55 dual_loss=7.0870e-01
Validation X2Y - loss=1.3386e+00 ppl=3.81 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.1317e+00 ppl=3.10 best_loss=1.0563e+00 best_ppl=2.88
Epoch 36 - |param|=8.71e+02 |g_param|=8.18e+05 loss_x2y=1.0486e+00 ppl_x2y=2.85 loss_y2x=8.8033e-01 ppl_y2x=2.41 dual_loss=6.2239e-01
Validation X2Y - loss=1.3594e+00 ppl=3.89 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.1666e+00 ppl=3.21 best_loss=1.0563e+00 best_ppl=2.88
Epoch 37 - |param|=8.72e+02 |g_param|=7.76e+05 loss_x2y=1.0660e+00 ppl_x2y=2.90 loss_y2x=8.7697e-01 ppl_y2x=2.40 dual_loss=5.8734e-01
Validation X2Y - loss=1.3452e+00 ppl=3.84 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.1620e+00 ppl=3.20 best_loss=1.0563e+00 best_ppl=2.88
Epoch 38 - |param|=8.72e+02 |g_param|=8.24e+05 loss_x2y=1.0586e+00 ppl_x2y=2.88 loss_y2x=8.6785e-01 ppl_y2x=2.38 dual_loss=6.5068e-01
Validation X2Y - loss=1.3847e+00 ppl=3.99 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.1620e+00 ppl=3.20 best_loss=1.0563e+00 best_ppl=2.88
Epoch 39 - |param|=8.73e+02 |g_param|=7.61e+05 loss_x2y=9.6690e-01 ppl_x2y=2.63 loss_y2x=8.1399e-01 ppl_y2x=2.26 dual_loss=6.0885e-01
Validation X2Y - loss=1.3869e+00 ppl=4.00 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.1689e+00 ppl=3.22 best_loss=1.0563e+00 best_ppl=2.88
Epoch 40 - |param|=8.73e+02 |g_param|=8.02e+05 loss_x2y=9.7428e-01 ppl_x2y=2.65 loss_y2x=8.1215e-01 ppl_y2x=2.25 dual_loss=6.7654e-01
Validation X2Y - loss=1.3987e+00 ppl=4.05 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.1880e+00 ppl=3.28 best_loss=1.0563e+00 best_ppl=2.88
Epoch 41 - |param|=8.74e+02 |g_param|=7.87e+05 loss_x2y=9.3957e-01 ppl_x2y=2.56 loss_y2x=7.8167e-01 ppl_y2x=2.19 dual_loss=6.2523e-01
Validation X2Y - loss=1.3904e+00 ppl=4.02 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.1768e+00 ppl=3.24 best_loss=1.0563e+00 best_ppl=2.88
Epoch 42 - |param|=8.74e+02 |g_param|=8.32e+05 loss_x2y=1.0326e+00 ppl_x2y=2.81 loss_y2x=8.3653e-01 ppl_y2x=2.31 dual_loss=7.7842e-01
Validation X2Y - loss=1.3911e+00 ppl=4.02 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.1815e+00 ppl=3.26 best_loss=1.0563e+00 best_ppl=2.88
Epoch 43 - |param|=8.75e+02 |g_param|=7.87e+05 loss_x2y=9.2948e-01 ppl_x2y=2.53 loss_y2x=7.8665e-01 ppl_y2x=2.20 dual_loss=6.7643e-01
Validation X2Y - loss=1.4042e+00 ppl=4.07 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.1990e+00 ppl=3.32 best_loss=1.0563e+00 best_ppl=2.88
Epoch 44 - |param|=8.75e+02 |g_param|=8.14e+05 loss_x2y=9.1449e-01 ppl_x2y=2.50 loss_y2x=7.5871e-01 ppl_y2x=2.14 dual_loss=6.7313e-01
Validation X2Y - loss=1.4185e+00 ppl=4.13 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.2127e+00 ppl=3.36 best_loss=1.0563e+00 best_ppl=2.88
Epoch 45 - |param|=8.76e+02 |g_param|=7.77e+05 loss_x2y=8.9989e-01 ppl_x2y=2.46 loss_y2x=7.3376e-01 ppl_y2x=2.08 dual_loss=6.9771e-01
Validation X2Y - loss=1.4172e+00 ppl=4.13 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.1818e+00 ppl=3.26 best_loss=1.0563e+00 best_ppl=2.88
Epoch 46 - |param|=8.76e+02 |g_param|=8.66e+05 loss_x2y=9.0169e-01 ppl_x2y=2.46 loss_y2x=7.8046e-01 ppl_y2x=2.18 dual_loss=8.9378e-01
Validation X2Y - loss=1.4343e+00 ppl=4.20 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.2787e+00 ppl=3.59 best_loss=1.0563e+00 best_ppl=2.88
Epoch 47 - |param|=8.77e+02 |g_param|=7.94e+05 loss_x2y=8.8201e-01 ppl_x2y=2.42 loss_y2x=7.2663e-01 ppl_y2x=2.07 dual_loss=7.4449e-01
Validation X2Y - loss=1.4863e+00 ppl=4.42 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.2629e+00 ppl=3.54 best_loss=1.0563e+00 best_ppl=2.88
Epoch 48 - |param|=8.77e+02 |g_param|=8.02e+05 loss_x2y=8.3896e-01 ppl_x2y=2.31 loss_y2x=7.0328e-01 ppl_y2x=2.02 dual_loss=7.1143e-01
Validation X2Y - loss=1.4449e+00 ppl=4.24 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.2763e+00 ppl=3.58 best_loss=1.0563e+00 best_ppl=2.88
Epoch 49 - |param|=8.78e+02 |g_param|=7.67e+05 loss_x2y=8.3429e-01 ppl_x2y=2.30 loss_y2x=6.7274e-01 ppl_y2x=1.96 dual_loss=6.7545e-01
Validation X2Y - loss=1.4673e+00 ppl=4.34 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.2652e+00 ppl=3.54 best_loss=1.0563e+00 best_ppl=2.88
Epoch 50 - |param|=8.78e+02 |g_param|=8.22e+05 loss_x2y=8.2638e-01 ppl_x2y=2.29 loss_y2x=6.8200e-01 ppl_y2x=1.98 dual_loss=7.6360e-01
Validation X2Y - loss=1.4690e+00 ppl=4.35 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.2792e+00 ppl=3.59 best_loss=1.0563e+00 best_ppl=2.88
Epoch 51 - |param|=8.79e+02 |g_param|=8.18e+05 loss_x2y=8.5641e-01 ppl_x2y=2.35 loss_y2x=7.2033e-01 ppl_y2x=2.06 dual_loss=8.5882e-01
Validation X2Y - loss=1.4986e+00 ppl=4.48 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.2542e+00 ppl=3.50 best_loss=1.0563e+00 best_ppl=2.88
Epoch 52 - |param|=8.79e+02 |g_param|=8.32e+05 loss_x2y=8.9084e-01 ppl_x2y=2.44 loss_y2x=7.1009e-01 ppl_y2x=2.03 dual_loss=9.2916e-01
Validation X2Y - loss=1.5063e+00 ppl=4.51 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.2728e+00 ppl=3.57 best_loss=1.0563e+00 best_ppl=2.88
Epoch 53 - |param|=8.80e+02 |g_param|=7.93e+05 loss_x2y=8.1634e-01 ppl_x2y=2.26 loss_y2x=6.7410e-01 ppl_y2x=1.96 dual_loss=7.6745e-01
Validation X2Y - loss=1.5107e+00 ppl=4.53 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.2818e+00 ppl=3.60 best_loss=1.0563e+00 best_ppl=2.88
Epoch 54 - |param|=8.80e+02 |g_param|=8.65e+05 loss_x2y=8.0343e-01 ppl_x2y=2.23 loss_y2x=7.0302e-01 ppl_y2x=2.02 dual_loss=9.5524e-01
Validation X2Y - loss=1.4985e+00 ppl=4.48 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.3056e+00 ppl=3.69 best_loss=1.0563e+00 best_ppl=2.88
Epoch 55 - |param|=8.81e+02 |g_param|=7.82e+05 loss_x2y=7.7324e-01 ppl_x2y=2.17 loss_y2x=6.3069e-01 ppl_y2x=1.88 dual_loss=7.7122e-01
Validation X2Y - loss=1.5009e+00 ppl=4.49 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.3118e+00 ppl=3.71 best_loss=1.0563e+00 best_ppl=2.88
Epoch 56 - |param|=8.81e+02 |g_param|=8.19e+05 loss_x2y=7.7700e-01 ppl_x2y=2.17 loss_y2x=6.3666e-01 ppl_y2x=1.89 dual_loss=8.1325e-01
Validation X2Y - loss=1.4995e+00 ppl=4.48 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.2983e+00 ppl=3.66 best_loss=1.0563e+00 best_ppl=2.88
Epoch 57 - |param|=8.81e+02 |g_param|=8.05e+05 loss_x2y=7.9928e-01 ppl_x2y=2.22 loss_y2x=6.4857e-01 ppl_y2x=1.91 dual_loss=9.0544e-01
Validation X2Y - loss=1.5519e+00 ppl=4.72 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.3048e+00 ppl=3.69 best_loss=1.0563e+00 best_ppl=2.88
Epoch 58 - |param|=8.82e+02 |g_param|=8.25e+05 loss_x2y=7.6399e-01 ppl_x2y=2.15 loss_y2x=6.1934e-01 ppl_y2x=1.86 dual_loss=8.2517e-01
Validation X2Y - loss=1.5492e+00 ppl=4.71 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.3146e+00 ppl=3.72 best_loss=1.0563e+00 best_ppl=2.88
Epoch 59 - |param|=8.82e+02 |g_param|=7.77e+05 loss_x2y=7.4647e-01 ppl_x2y=2.11 loss_y2x=6.1643e-01 ppl_y2x=1.85 dual_loss=9.0265e-01
Validation X2Y - loss=1.5476e+00 ppl=4.70 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.3241e+00 ppl=3.76 best_loss=1.0563e+00 best_ppl=2.88
Epoch 60 - |param|=8.83e+02 |g_param|=6.21e+05 loss_x2y=7.6247e-01 ppl_x2y=2.14 loss_y2x=6.1332e-01 ppl_y2x=1.85 dual_loss=8.8748e-01
Validation X2Y - loss=1.5579e+00 ppl=4.75 best_loss=1.2431e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.3060e+00 ppl=3.69 best_loss=1.0563e+00 best_ppl=2.88

real	19m24.694s
user	19m7.802s
sys	0m18.840s
```

testing/evaluation...  

```
/home/ye/exp/simple-nmt/model/dsl/transformer/mybk-60epoch
Evaluation result for the model: dsl-model-mybk.01.4.40-81.15.4.06-57.85.3.50-33.12.3.10-22.31.pth, mybk
BLEU = 4.46, 19.5/5.8/2.6/1.3 (BP=1.000, ratio=1.077, hyp_len=12308, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.40-81.15.4.06-57.85.3.50-33.12.3.10-22.31.pth, bkmy
BLEU = 4.41, 25.6/7.4/2.7/0.7 (BP=1.000, ratio=1.055, hyp_len=12902, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.02.3.62-37.47.3.17-23.87.3.04-20.97.2.79-16.24.pth, mybk
BLEU = 1.43, 7.3/2.0/0.8/0.4 (BP=1.000, ratio=3.179, hyp_len=36344, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.3.62-37.47.3.17-23.87.3.04-20.97.2.79-16.24.pth, bkmy
BLEU = 2.11, 11.2/3.4/1.2/0.4 (BP=1.000, ratio=2.748, hyp_len=33612, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.3.29-26.77.2.88-17.76.2.69-14.69.2.37-10.65.pth, mybk
BLEU = 0.78, 3.7/1.1/0.5/0.2 (BP=1.000, ratio=5.985, hyp_len=68424, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.3.29-26.77.2.88-17.76.2.69-14.69.2.37-10.65.pth, bkmy
BLEU = 8.86, 33.4/13.4/5.7/2.4 (BP=1.000, ratio=1.145, hyp_len=14010, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.2.97-19.49.2.60-13.44.2.31-10.12.2.13-8.39.pth, mybk
BLEU = 4.15, 14.8/5.9/2.7/1.3 (BP=1.000, ratio=2.363, hyp_len=27009, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.2.97-19.49.2.60-13.44.2.31-10.12.2.13-8.39.pth, bkmy
BLEU = 6.87, 22.7/10.0/4.6/2.1 (BP=1.000, ratio=1.933, hyp_len=23638, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.2.89-17.92.2.48-11.92.2.09-8.10.1.88-6.55.pth, mybk
BLEU = 5.89, 18.3/8.0/4.1/2.0 (BP=1.000, ratio=2.161, hyp_len=24708, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.2.89-17.92.2.48-11.92.2.09-8.10.1.88-6.55.pth, bkmy
BLEU = 15.13, 40.7/20.3/10.7/5.9 (BP=1.000, ratio=1.144, hyp_len=13994, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.2.60-13.53.2.22-9.22.1.87-6.49.1.67-5.33.pth, mybk
BLEU = 10.60, 28.8/13.9/7.6/4.1 (BP=1.000, ratio=1.494, hyp_len=17075, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.2.60-13.53.2.22-9.22.1.87-6.49.1.67-5.33.pth, bkmy
BLEU = 22.01, 53.4/30.3/17.9/11.2 (BP=0.924, ratio=0.927, hyp_len=11333, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.2.43-11.35.2.10-8.18.1.71-5.54.1.57-4.81.pth, mybk
BLEU = 19.93, 46.9/24.8/14.8/9.2 (BP=1.000, ratio=1.034, hyp_len=11821, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.2.43-11.35.2.10-8.18.1.71-5.54.1.57-4.81.pth, bkmy
BLEU = 27.14, 55.8/33.4/21.1/13.8 (BP=1.000, ratio=1.016, hyp_len=12429, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.2.36-10.58.2.03-7.61.1.62-5.04.1.42-4.12.pth, mybk
BLEU = 20.35, 46.8/25.1/15.2/9.6 (BP=1.000, ratio=1.109, hyp_len=12681, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.2.36-10.58.2.03-7.61.1.62-5.04.1.42-4.12.pth, bkmy
BLEU = 29.41, 56.7/35.7/23.3/15.8 (BP=1.000, ratio=1.030, hyp_len=12593, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.2.37-10.74.2.00-7.37.1.51-4.54.1.34-3.81.pth, mybk
BLEU = 23.54, 50.9/28.7/18.0/11.7 (BP=1.000, ratio=1.071, hyp_len=12249, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.2.37-10.74.2.00-7.37.1.51-4.54.1.34-3.81.pth, bkmy
BLEU = 33.22, 61.1/40.2/27.5/19.6 (BP=0.980, ratio=0.980, hyp_len=11984, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.2.18-8.80.1.91-6.72.1.43-4.19.1.29-3.65.pth, mybk
BLEU = 26.20, 53.7/31.8/20.4/13.5 (BP=1.000, ratio=1.040, hyp_len=11892, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.2.18-8.80.1.91-6.72.1.43-4.19.1.29-3.65.pth, bkmy
BLEU = 33.93, 61.9/40.6/27.7/19.8 (BP=0.990, ratio=0.990, hyp_len=12112, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.2.20-9.01.1.83-6.23.1.40-4.05.1.25-3.51.pth, mybk
BLEU = 27.05, 54.6/32.6/21.2/14.2 (BP=1.000, ratio=1.068, hyp_len=12211, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.2.20-9.01.1.83-6.23.1.40-4.05.1.25-3.51.pth, bkmy
BLEU = 34.44, 61.8/40.9/28.0/19.9 (BP=1.000, ratio=1.039, hyp_len=12708, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.1.96-7.13.1.67-5.31.1.36-3.91.1.20-3.32.pth, mybk
BLEU = 28.07, 55.3/33.6/22.1/15.1 (BP=1.000, ratio=1.059, hyp_len=12106, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.1.96-7.13.1.67-5.31.1.36-3.91.1.20-3.32.pth, bkmy
BLEU = 33.72, 58.9/39.9/27.7/19.8 (BP=1.000, ratio=1.126, hyp_len=13767, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.1.86-6.42.1.58-4.84.1.31-3.70.1.18-3.27.pth, mybk
BLEU = 30.94, 58.0/36.3/24.9/17.5 (BP=1.000, ratio=1.038, hyp_len=11867, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.1.86-6.42.1.58-4.84.1.31-3.70.1.18-3.27.pth, bkmy
BLEU = 36.89, 63.3/42.9/30.4/22.5 (BP=1.000, ratio=1.015, hyp_len=12410, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.1.81-6.10.1.54-4.68.1.31-3.71.1.14-3.12.pth, mybk
BLEU = 29.95, 56.7/35.3/23.8/16.9 (BP=1.000, ratio=1.056, hyp_len=12073, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.1.81-6.10.1.54-4.68.1.31-3.71.1.14-3.12.pth, bkmy
BLEU = 38.94, 65.0/45.0/32.4/24.3 (BP=1.000, ratio=1.009, hyp_len=12343, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.1.80-6.08.1.54-4.64.1.30-3.66.1.11-3.04.pth, mybk
BLEU = 31.53, 59.0/37.3/25.3/17.7 (BP=1.000, ratio=1.040, hyp_len=11886, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.1.80-6.08.1.54-4.64.1.30-3.66.1.11-3.04.pth, bkmy
BLEU = 39.76, 66.1/46.4/33.3/24.5 (BP=1.000, ratio=1.032, hyp_len=12617, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.1.72-5.59.1.47-4.35.1.28-3.60.1.09-2.97.pth, mybk
BLEU = 32.22, 59.9/37.9/25.8/18.4 (BP=1.000, ratio=1.047, hyp_len=11973, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.1.72-5.59.1.47-4.35.1.28-3.60.1.09-2.97.pth, bkmy
BLEU = 40.27, 66.6/46.8/33.7/25.0 (BP=1.000, ratio=1.023, hyp_len=12516, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.1.60-4.94.1.37-3.92.1.28-3.58.1.11-3.02.pth, mybk
BLEU = 31.59, 59.1/37.5/25.3/17.7 (BP=1.000, ratio=1.081, hyp_len=12360, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.1.60-4.94.1.37-3.92.1.28-3.58.1.11-3.02.pth, bkmy
BLEU = 38.53, 65.0/45.0/32.0/23.5 (BP=1.000, ratio=1.053, hyp_len=12884, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.1.63-5.10.1.38-3.98.1.27-3.56.1.11-3.03.pth, mybk
BLEU = 30.91, 58.0/36.9/24.8/17.2 (BP=1.000, ratio=1.110, hyp_len=12691, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.1.63-5.10.1.38-3.98.1.27-3.56.1.11-3.03.pth, bkmy
BLEU = 37.80, 64.0/44.2/31.4/23.0 (BP=1.000, ratio=1.091, hyp_len=13348, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.1.56-4.76.1.32-3.75.1.24-3.47.1.09-2.98.pth, mybk
BLEU = 32.56, 60.4/38.6/26.1/18.5 (BP=1.000, ratio=1.059, hyp_len=12104, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.1.56-4.76.1.32-3.75.1.24-3.47.1.09-2.98.pth, bkmy
BLEU = 39.39, 65.5/46.0/33.0/24.3 (BP=1.000, ratio=1.052, hyp_len=12870, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.1.50-4.50.1.27-3.57.1.28-3.61.1.11-3.04.pth, mybk
BLEU = 32.38, 59.8/38.2/26.0/18.5 (BP=1.000, ratio=1.054, hyp_len=12051, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.1.50-4.50.1.27-3.57.1.28-3.61.1.11-3.04.pth, bkmy
BLEU = 40.53, 66.4/46.7/34.1/25.5 (BP=1.000, ratio=1.026, hyp_len=12547, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.1.57-4.81.1.31-3.69.1.26-3.53.1.07-2.92.pth, mybk
BLEU = 31.83, 59.4/37.6/25.5/18.0 (BP=1.000, ratio=1.071, hyp_len=12238, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.1.57-4.81.1.31-3.69.1.26-3.53.1.07-2.92.pth, bkmy
BLEU = 40.70, 67.1/47.1/34.0/25.5 (BP=1.000, ratio=1.014, hyp_len=12399, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.1.44-4.23.1.21-3.35.1.26-3.54.1.06-2.88.pth, mybk
BLEU = 33.63, 61.7/39.5/27.1/19.4 (BP=1.000, ratio=1.046, hyp_len=11962, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.1.44-4.23.1.21-3.35.1.26-3.54.1.06-2.88.pth, bkmy
BLEU = 40.91, 67.0/47.3/34.3/25.7 (BP=1.000, ratio=1.037, hyp_len=12687, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.1.42-4.15.1.20-3.32.1.26-3.52.1.09-2.96.pth, mybk
BLEU = 32.22, 59.1/37.9/26.1/18.4 (BP=1.000, ratio=1.061, hyp_len=12133, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.1.42-4.15.1.20-3.32.1.26-3.52.1.09-2.96.pth, bkmy
BLEU = 39.96, 66.5/46.6/33.3/24.7 (BP=1.000, ratio=1.038, hyp_len=12691, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.1.33-3.79.1.14-3.12.1.26-3.54.1.07-2.92.pth, mybk
BLEU = 33.86, 61.1/39.4/27.5/19.9 (BP=1.000, ratio=1.028, hyp_len=11752, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.1.33-3.79.1.14-3.12.1.26-3.54.1.07-2.92.pth, bkmy
BLEU = 40.57, 67.4/47.1/33.9/25.2 (BP=1.000, ratio=1.030, hyp_len=12598, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.1.33-3.78.1.12-3.07.1.27-3.56.1.09-2.97.pth, mybk
BLEU = 33.51, 61.3/39.4/27.1/19.3 (BP=1.000, ratio=1.035, hyp_len=11829, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.1.33-3.78.1.12-3.07.1.27-3.56.1.09-2.97.pth, bkmy
BLEU = 40.94, 67.1/47.2/34.3/25.9 (BP=1.000, ratio=1.013, hyp_len=12396, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.1.32-3.74.1.11-3.03.1.30-3.66.1.09-2.97.pth, mybk
BLEU = 34.19, 61.9/40.0/27.7/19.9 (BP=1.000, ratio=1.043, hyp_len=11925, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.1.32-3.74.1.11-3.03.1.30-3.66.1.09-2.97.pth, bkmy
BLEU = 39.68, 65.8/45.8/33.1/24.9 (BP=1.000, ratio=1.036, hyp_len=12675, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.1.24-3.44.1.06-2.88.1.26-3.54.1.07-2.93.pth, mybk
BLEU = 33.71, 61.3/39.5/27.1/19.7 (BP=1.000, ratio=1.044, hyp_len=11937, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.1.24-3.44.1.06-2.88.1.26-3.54.1.07-2.93.pth, bkmy
BLEU = 40.68, 66.9/46.8/33.9/25.8 (BP=1.000, ratio=1.014, hyp_len=12400, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.1.26-3.52.1.05-2.86.1.30-3.67.1.08-2.94.pth, mybk
BLEU = 34.62, 62.2/40.4/28.1/20.4 (BP=1.000, ratio=1.052, hyp_len=12021, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.1.26-3.52.1.05-2.86.1.30-3.67.1.08-2.94.pth, bkmy
BLEU = 40.61, 66.5/46.7/34.1/25.7 (BP=1.000, ratio=1.024, hyp_len=12528, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.1.20-3.33.1.00-2.73.1.32-3.73.1.10-2.99.pth, mybk
BLEU = 31.84, 59.0/37.6/25.5/18.2 (BP=1.000, ratio=1.104, hyp_len=12623, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.1.20-3.33.1.00-2.73.1.32-3.73.1.10-2.99.pth, bkmy
BLEU = 39.17, 65.3/45.4/32.5/24.4 (BP=1.000, ratio=1.048, hyp_len=12817, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.1.26-3.52.1.05-2.87.1.32-3.75.1.09-2.96.pth, mybk
BLEU = 34.00, 60.7/39.5/27.5/20.3 (BP=1.000, ratio=1.062, hyp_len=12145, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.1.26-3.52.1.05-2.87.1.32-3.75.1.09-2.96.pth, bkmy
BLEU = 38.74, 64.6/44.8/32.2/24.1 (BP=1.000, ratio=1.079, hyp_len=13195, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.31.1.16-3.19.0.97-2.63.1.31-3.72.1.08-2.94.pth, mybk
BLEU = 32.28, 59.7/37.9/25.9/18.5 (BP=1.000, ratio=1.075, hyp_len=12288, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.31.1.16-3.19.0.97-2.63.1.31-3.72.1.08-2.94.pth, bkmy
BLEU = 39.21, 65.4/45.5/32.7/24.3 (BP=1.000, ratio=1.060, hyp_len=12970, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.32.1.15-3.15.0.99-2.70.1.33-3.79.1.09-2.98.pth, mybk
BLEU = 33.34, 60.5/39.2/26.9/19.3 (BP=1.000, ratio=1.069, hyp_len=12217, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.32.1.15-3.15.0.99-2.70.1.33-3.79.1.09-2.98.pth, bkmy
BLEU = 40.14, 65.3/46.0/33.7/25.6 (BP=1.000, ratio=1.055, hyp_len=12900, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.33.1.16-3.20.0.95-2.60.1.36-3.89.1.10-3.01.pth, mybk
BLEU = 32.33, 59.4/37.8/26.1/18.6 (BP=1.000, ratio=1.051, hyp_len=12019, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.33.1.16-3.20.0.95-2.60.1.36-3.89.1.10-3.01.pth, bkmy
BLEU = 39.07, 65.3/45.3/32.5/24.2 (BP=1.000, ratio=1.056, hyp_len=12914, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.34.1.10-3.01.0.93-2.54.1.36-3.89.1.11-3.02.pth, mybk
BLEU = 32.22, 59.0/37.7/26.0/18.6 (BP=1.000, ratio=1.073, hyp_len=12261, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.34.1.10-3.01.0.93-2.54.1.36-3.89.1.11-3.02.pth, bkmy
BLEU = 38.66, 64.8/45.0/32.1/23.9 (BP=1.000, ratio=1.058, hyp_len=12937, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.35.1.14-3.14.0.94-2.55.1.34-3.81.1.13-3.10.pth, mybk
BLEU = 33.12, 60.6/38.9/26.8/19.0 (BP=1.000, ratio=1.054, hyp_len=12048, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.35.1.14-3.14.0.94-2.55.1.34-3.81.1.13-3.10.pth, bkmy
BLEU = 40.39, 66.2/46.7/33.9/25.4 (BP=1.000, ratio=1.040, hyp_len=12720, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.36.1.05-2.85.0.88-2.41.1.36-3.89.1.17-3.21.pth, mybk
BLEU = 32.72, 60.0/38.4/26.3/18.9 (BP=1.000, ratio=1.077, hyp_len=12315, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.36.1.05-2.85.0.88-2.41.1.36-3.89.1.17-3.21.pth, bkmy
BLEU = 40.87, 66.6/46.8/34.3/26.1 (BP=1.000, ratio=1.025, hyp_len=12532, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.37.1.07-2.90.0.88-2.40.1.35-3.84.1.16-3.20.pth, mybk
BLEU = 33.03, 60.2/38.7/26.6/19.2 (BP=1.000, ratio=1.066, hyp_len=12192, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.37.1.07-2.90.0.88-2.40.1.35-3.84.1.16-3.20.pth, bkmy
BLEU = 40.35, 66.4/46.4/33.8/25.4 (BP=1.000, ratio=1.035, hyp_len=12665, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.38.1.06-2.88.0.87-2.38.1.38-3.99.1.16-3.20.pth, mybk
BLEU = 32.96, 60.5/38.8/26.5/19.0 (BP=1.000, ratio=1.049, hyp_len=11994, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.38.1.06-2.88.0.87-2.38.1.38-3.99.1.16-3.20.pth, bkmy
BLEU = 39.31, 65.1/45.2/32.7/24.8 (BP=1.000, ratio=1.033, hyp_len=12636, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.39.0.97-2.63.0.81-2.26.1.39-4.00.1.17-3.22.pth, mybk
BLEU = 31.20, 58.3/36.9/24.9/17.7 (BP=1.000, ratio=1.075, hyp_len=12286, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.39.0.97-2.63.0.81-2.26.1.39-4.00.1.17-3.22.pth, bkmy
BLEU = 39.58, 65.9/45.8/33.0/24.7 (BP=1.000, ratio=1.030, hyp_len=12602, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.40.0.97-2.65.0.81-2.25.1.40-4.05.1.19-3.28.pth, mybk
BLEU = 32.36, 60.1/38.0/26.0/18.5 (BP=1.000, ratio=1.052, hyp_len=12030, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.40.0.97-2.65.0.81-2.25.1.40-4.05.1.19-3.28.pth, bkmy
BLEU = 38.46, 64.0/44.5/32.0/24.0 (BP=1.000, ratio=1.056, hyp_len=12910, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.41.0.94-2.56.0.78-2.19.1.39-4.02.1.18-3.24.pth, mybk
BLEU = 32.04, 59.4/37.7/25.8/18.3 (BP=1.000, ratio=1.051, hyp_len=12018, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.41.0.94-2.56.0.78-2.19.1.39-4.02.1.18-3.24.pth, bkmy
BLEU = 38.40, 64.8/44.7/31.8/23.6 (BP=1.000, ratio=1.049, hyp_len=12835, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.42.1.03-2.81.0.84-2.31.1.39-4.02.1.18-3.26.pth, mybk
BLEU = 30.57, 57.4/36.0/24.4/17.3 (BP=1.000, ratio=1.096, hyp_len=12534, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.42.1.03-2.81.0.84-2.31.1.39-4.02.1.18-3.26.pth, bkmy
BLEU = 37.99, 63.8/44.1/31.7/23.4 (BP=1.000, ratio=1.069, hyp_len=13076, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.43.0.93-2.53.0.79-2.20.1.40-4.07.1.20-3.32.pth, mybk
BLEU = 33.01, 61.1/38.9/26.5/18.9 (BP=1.000, ratio=1.039, hyp_len=11875, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.43.0.93-2.53.0.79-2.20.1.40-4.07.1.20-3.32.pth, bkmy
BLEU = 36.92, 62.7/42.9/30.5/22.7 (BP=1.000, ratio=1.076, hyp_len=13158, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.44.0.91-2.50.0.76-2.14.1.42-4.13.1.21-3.36.pth, mybk
BLEU = 31.77, 58.7/37.3/25.5/18.3 (BP=1.000, ratio=1.068, hyp_len=12210, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.44.0.91-2.50.0.76-2.14.1.42-4.13.1.21-3.36.pth, bkmy
BLEU = 37.74, 63.6/43.9/31.2/23.3 (BP=1.000, ratio=1.063, hyp_len=13006, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.45.0.90-2.46.0.73-2.08.1.42-4.13.1.18-3.26.pth, mybk
BLEU = 32.73, 60.1/38.2/26.4/18.9 (BP=1.000, ratio=1.058, hyp_len=12096, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.45.0.90-2.46.0.73-2.08.1.42-4.13.1.18-3.26.pth, bkmy
BLEU = 39.59, 65.0/45.6/33.1/25.1 (BP=1.000, ratio=1.057, hyp_len=12932, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.46.0.90-2.46.0.78-2.18.1.43-4.20.1.28-3.59.pth, mybk
BLEU = 31.15, 59.1/37.1/24.7/17.4 (BP=1.000, ratio=1.076, hyp_len=12297, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.46.0.90-2.46.0.78-2.18.1.43-4.20.1.28-3.59.pth, bkmy
BLEU = 35.66, 60.8/41.4/29.6/21.7 (BP=1.000, ratio=1.086, hyp_len=13288, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.47.0.88-2.42.0.73-2.07.1.49-4.42.1.26-3.54.pth, mybk
BLEU = 28.82, 55.5/34.1/22.7/16.1 (BP=1.000, ratio=1.118, hyp_len=12786, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.47.0.88-2.42.0.73-2.07.1.49-4.42.1.26-3.54.pth, bkmy
BLEU = 38.88, 64.3/44.6/32.3/24.6 (BP=1.000, ratio=1.038, hyp_len=12697, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.48.0.84-2.31.0.70-2.02.1.44-4.24.1.28-3.58.pth, mybk
BLEU = 31.70, 59.0/37.4/25.4/18.0 (BP=1.000, ratio=1.067, hyp_len=12197, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.48.0.84-2.31.0.70-2.02.1.44-4.24.1.28-3.58.pth, bkmy
BLEU = 37.33, 62.7/43.3/31.1/23.0 (BP=1.000, ratio=1.082, hyp_len=13231, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.49.0.83-2.30.0.67-1.96.1.47-4.34.1.27-3.54.pth, mybk
BLEU = 32.36, 60.0/38.0/26.0/18.5 (BP=1.000, ratio=1.039, hyp_len=11883, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.49.0.83-2.30.0.67-1.96.1.47-4.34.1.27-3.54.pth, bkmy
BLEU = 37.01, 62.2/42.6/30.6/23.2 (BP=1.000, ratio=1.059, hyp_len=12953, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.50.0.83-2.29.0.68-1.98.1.47-4.35.1.28-3.59.pth, mybk
BLEU = 31.44, 58.2/36.9/25.1/18.1 (BP=1.000, ratio=1.055, hyp_len=12059, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.50.0.83-2.29.0.68-1.98.1.47-4.35.1.28-3.59.pth, bkmy
BLEU = 37.81, 63.2/43.6/31.4/23.6 (BP=1.000, ratio=1.046, hyp_len=12798, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.51.0.86-2.35.0.72-2.06.1.50-4.48.1.25-3.50.pth, mybk
BLEU = 32.06, 59.4/37.7/25.7/18.4 (BP=1.000, ratio=1.075, hyp_len=12287, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.51.0.86-2.35.0.72-2.06.1.50-4.48.1.25-3.50.pth, bkmy
BLEU = 37.41, 63.7/43.4/30.9/22.9 (BP=1.000, ratio=1.054, hyp_len=12890, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.52.0.89-2.44.0.71-2.03.1.51-4.51.1.27-3.57.pth, mybk
BLEU = 31.07, 57.7/36.4/24.8/17.8 (BP=1.000, ratio=1.092, hyp_len=12481, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.52.0.89-2.44.0.71-2.03.1.51-4.51.1.27-3.57.pth, bkmy
BLEU = 36.37, 61.5/42.1/30.2/22.4 (BP=1.000, ratio=1.064, hyp_len=13017, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.53.0.82-2.26.0.67-1.96.1.51-4.53.1.28-3.60.pth, mybk
BLEU = 30.57, 58.4/36.6/24.3/16.8 (BP=1.000, ratio=1.070, hyp_len=12232, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.53.0.82-2.26.0.67-1.96.1.51-4.53.1.28-3.60.pth, bkmy
BLEU = 36.81, 61.9/42.3/30.5/22.9 (BP=1.000, ratio=1.041, hyp_len=12738, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.54.0.80-2.23.0.70-2.02.1.50-4.48.1.31-3.69.pth, mybk
BLEU = 30.68, 58.1/36.3/24.4/17.3 (BP=1.000, ratio=1.074, hyp_len=12274, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.54.0.80-2.23.0.70-2.02.1.50-4.48.1.31-3.69.pth, bkmy
BLEU = 37.06, 62.3/42.8/30.7/23.1 (BP=1.000, ratio=1.074, hyp_len=13142, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.55.0.77-2.17.0.63-1.88.1.50-4.49.1.31-3.71.pth, mybk
BLEU = 30.84, 58.3/36.4/24.5/17.4 (BP=1.000, ratio=1.070, hyp_len=12228, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.55.0.77-2.17.0.63-1.88.1.50-4.49.1.31-3.71.pth, bkmy
BLEU = 36.69, 62.2/42.5/30.3/22.6 (BP=1.000, ratio=1.072, hyp_len=13111, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.56.0.78-2.17.0.64-1.89.1.50-4.48.1.30-3.66.pth, mybk
BLEU = 30.76, 58.0/36.4/24.4/17.3 (BP=1.000, ratio=1.093, hyp_len=12495, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.56.0.78-2.17.0.64-1.89.1.50-4.48.1.30-3.66.pth, bkmy
BLEU = 37.05, 63.1/43.0/30.7/22.6 (BP=1.000, ratio=1.062, hyp_len=12988, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.57.0.80-2.22.0.65-1.91.1.55-4.72.1.30-3.69.pth, mybk
BLEU = 30.75, 57.7/36.1/24.5/17.5 (BP=1.000, ratio=1.067, hyp_len=12203, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.57.0.80-2.22.0.65-1.91.1.55-4.72.1.30-3.69.pth, bkmy
BLEU = 37.14, 62.8/42.9/30.7/23.0 (BP=1.000, ratio=1.050, hyp_len=12845, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.58.0.76-2.15.0.62-1.86.1.55-4.71.1.31-3.72.pth, mybk
BLEU = 30.54, 57.9/36.1/24.3/17.1 (BP=1.000, ratio=1.080, hyp_len=12351, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.58.0.76-2.15.0.62-1.86.1.55-4.71.1.31-3.72.pth, bkmy
BLEU = 37.42, 62.6/43.1/31.1/23.3 (BP=1.000, ratio=1.075, hyp_len=13146, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.59.0.75-2.11.0.62-1.85.1.55-4.70.1.32-3.76.pth, mybk
BLEU = 31.01, 58.4/36.5/24.6/17.6 (BP=1.000, ratio=1.063, hyp_len=12150, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.59.0.75-2.11.0.62-1.85.1.55-4.70.1.32-3.76.pth, bkmy
BLEU = 37.64, 63.0/43.1/31.3/23.7 (BP=1.000, ratio=1.042, hyp_len=12747, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.60.0.76-2.14.0.61-1.85.1.56-4.75.1.31-3.69.pth, mybk
BLEU = 30.53, 57.4/35.8/24.4/17.3 (BP=1.000, ratio=1.065, hyp_len=12176, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.60.0.76-2.14.0.61-1.85.1.56-4.75.1.31-3.69.pth, bkmy
BLEU = 35.36, 60.8/41.0/29.1/21.6 (BP=1.000, ratio=1.074, hyp_len=13141, ref_len=12231)
```

Best model for my-bk က epoch 28 မော်ဒယ် ဖြစ်ပြီးတော့၊ Best BLEU Score က : 34.62  
Best model for bk-my က epoch 25 မော်ဒယ် ဖြစ်ပြီးတော့၊ Best BLEU Score က : 40.94  

## Transformer-DSL, 70 epoch

```
Epoch 1 - |param|=8.54e+02 |g_param|=2.03e+05 loss_x2y=4.4578e+00 ppl_x2y=86.30 loss_y2x=4.0969e+00 ppl_y2x=60.15 dual_loss=0.0000e+00
Validation X2Y - loss=3.5306e+00 ppl=34.14 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=3.1834e+00 ppl=24.13 best_loss=inf best_ppl=inf
Epoch 2 - |param|=8.55e+02 |g_param|=1.31e+05 loss_x2y=3.5832e+00 ppl_x2y=35.99 loss_y2x=3.1793e+00 ppl_y2x=24.03 dual_loss=0.0000e+00
Validation X2Y - loss=2.9984e+00 ppl=20.05 best_loss=3.5306e+00 best_ppl=34.14                                          
Validation Y2X - loss=2.7160e+00 ppl=15.12 best_loss=3.1834e+00 best_ppl=24.13
Epoch 3 - |param|=8.55e+02 |g_param|=1.24e+05 loss_x2y=3.2569e+00 ppl_x2y=25.97 loss_y2x=2.9050e+00 ppl_y2x=18.27 dual_loss=0.0000e+00
Validation X2Y - loss=2.5387e+00 ppl=12.66 best_loss=2.9984e+00 best_ppl=20.05                                          
Validation Y2X - loss=2.3486e+00 ppl=10.47 best_loss=2.7160e+00 best_ppl=15.12
Epoch 4 - |param|=8.56e+02 |g_param|=1.41e+05 loss_x2y=2.9962e+00 ppl_x2y=20.01 loss_y2x=2.6438e+00 ppl_y2x=14.07 dual_loss=0.0000e+00
Validation X2Y - loss=2.2551e+00 ppl=9.54 best_loss=2.5387e+00 best_ppl=12.66                                           
Validation Y2X - loss=2.0765e+00 ppl=7.98 best_loss=2.3486e+00 best_ppl=10.47
Epoch 5 - |param|=8.57e+02 |g_param|=1.38e+05 loss_x2y=2.8244e+00 ppl_x2y=16.85 loss_y2x=2.4654e+00 ppl_y2x=11.77 dual_loss=0.0000e+00
Validation X2Y - loss=2.0741e+00 ppl=7.96 best_loss=2.2551e+00 best_ppl=9.54                                            
Validation Y2X - loss=1.9099e+00 ppl=6.75 best_loss=2.0765e+00 best_ppl=7.98
Epoch 6 - |param|=8.57e+02 |g_param|=1.50e+05 loss_x2y=2.5895e+00 ppl_x2y=13.32 loss_y2x=2.2799e+00 ppl_y2x=9.78 dual_loss=0.0000e+00
Validation X2Y - loss=1.8415e+00 ppl=6.31 best_loss=2.0741e+00 best_ppl=7.96                                            
Validation Y2X - loss=1.7114e+00 ppl=5.54 best_loss=1.9099e+00 best_ppl=6.75
Epoch 7 - |param|=8.58e+02 |g_param|=1.56e+05 loss_x2y=2.4977e+00 ppl_x2y=12.15 loss_y2x=2.1723e+00 ppl_y2x=8.78 dual_loss=0.0000e+00
Validation X2Y - loss=1.6909e+00 ppl=5.42 best_loss=1.8415e+00 best_ppl=6.31                                            
Validation Y2X - loss=1.5239e+00 ppl=4.59 best_loss=1.7114e+00 best_ppl=5.54
Epoch 8 - |param|=8.58e+02 |g_param|=1.63e+05 loss_x2y=2.3546e+00 ppl_x2y=10.53 loss_y2x=2.0398e+00 ppl_y2x=7.69 dual_loss=0.0000e+00
Validation X2Y - loss=1.5921e+00 ppl=4.91 best_loss=1.6909e+00 best_ppl=5.42                                            
Validation Y2X - loss=1.4340e+00 ppl=4.20 best_loss=1.5239e+00 best_ppl=4.59
Epoch 9 - |param|=8.59e+02 |g_param|=1.64e+05 loss_x2y=2.2145e+00 ppl_x2y=9.16 loss_y2x=1.9276e+00 ppl_y2x=6.87 dual_loss=0.0000e+00
Validation X2Y - loss=1.5535e+00 ppl=4.73 best_loss=1.5921e+00 best_ppl=4.91                                            
Validation Y2X - loss=1.3489e+00 ppl=3.85 best_loss=1.4340e+00 best_ppl=4.20
Epoch 10 - |param|=8.59e+02 |g_param|=1.71e+05 loss_x2y=2.0778e+00 ppl_x2y=7.99 loss_y2x=1.7952e+00 ppl_y2x=6.02 dual_loss=0.0000e+00
Validation X2Y - loss=1.4700e+00 ppl=4.35 best_loss=1.5535e+00 best_ppl=4.73                                            
Validation Y2X - loss=1.2404e+00 ppl=3.46 best_loss=1.3489e+00 best_ppl=3.85
Epoch 11 - |param|=8.60e+02 |g_param|=1.72e+05 loss_x2y=2.0382e+00 ppl_x2y=7.68 loss_y2x=1.7622e+00 ppl_y2x=5.83 dual_loss=0.0000e+00
Validation X2Y - loss=1.4063e+00 ppl=4.08 best_loss=1.4700e+00 best_ppl=4.35                                            
Validation Y2X - loss=1.2117e+00 ppl=3.36 best_loss=1.2404e+00 best_ppl=3.46
Epoch 12 - |param|=8.61e+02 |g_param|=2.11e+05 loss_x2y=2.0829e+00 ppl_x2y=8.03 loss_y2x=1.8353e+00 ppl_y2x=6.27 dual_loss=0.0000e+00
Validation X2Y - loss=1.3932e+00 ppl=4.03 best_loss=1.4063e+00 best_ppl=4.08                                            
Validation Y2X - loss=1.1839e+00 ppl=3.27 best_loss=1.2117e+00 best_ppl=3.36
Epoch 13 - |param|=8.61e+02 |g_param|=1.87e+05 loss_x2y=1.9023e+00 ppl_x2y=6.70 loss_y2x=1.6560e+00 ppl_y2x=5.24 dual_loss=0.0000e+00
Validation X2Y - loss=1.3494e+00 ppl=3.85 best_loss=1.3932e+00 best_ppl=4.03                                            
Validation Y2X - loss=1.1589e+00 ppl=3.19 best_loss=1.1839e+00 best_ppl=3.27
Epoch 14 - |param|=8.62e+02 |g_param|=2.03e+05 loss_x2y=1.7949e+00 ppl_x2y=6.02 loss_y2x=1.5466e+00 ppl_y2x=4.70 dual_loss=0.0000e+00
Validation X2Y - loss=1.3312e+00 ppl=3.79 best_loss=1.3494e+00 best_ppl=3.85                                            
Validation Y2X - loss=1.1533e+00 ppl=3.17 best_loss=1.1589e+00 best_ppl=3.19
Epoch 15 - |param|=8.62e+02 |g_param|=1.99e+05 loss_x2y=1.8968e+00 ppl_x2y=6.66 loss_y2x=1.5719e+00 ppl_y2x=4.82 dual_loss=0.0000e+00
Validation X2Y - loss=1.3181e+00 ppl=3.74 best_loss=1.3312e+00 best_ppl=3.79                                            
Validation Y2X - loss=1.1018e+00 ppl=3.01 best_loss=1.1533e+00 best_ppl=3.17
Epoch 16 - |param|=8.63e+02 |g_param|=2.09e+05 loss_x2y=1.6707e+00 ppl_x2y=5.32 loss_y2x=1.4481e+00 ppl_y2x=4.26 dual_loss=0.0000e+00
Validation X2Y - loss=1.2974e+00 ppl=3.66 best_loss=1.3181e+00 best_ppl=3.74                                            
Validation Y2X - loss=1.1049e+00 ppl=3.02 best_loss=1.1018e+00 best_ppl=3.01
Epoch 17 - |param|=8.63e+02 |g_param|=2.01e+05 loss_x2y=1.6370e+00 ppl_x2y=5.14 loss_y2x=1.4000e+00 ppl_y2x=4.06 dual_loss=0.0000e+00
Validation X2Y - loss=1.2916e+00 ppl=3.64 best_loss=1.2974e+00 best_ppl=3.66                                            
Validation Y2X - loss=1.0858e+00 ppl=2.96 best_loss=1.1018e+00 best_ppl=3.01
Epoch 18 - |param|=8.64e+02 |g_param|=2.28e+05 loss_x2y=1.6105e+00 ppl_x2y=5.01 loss_y2x=1.4052e+00 ppl_y2x=4.08 dual_loss=0.0000e+00
Validation X2Y - loss=1.3304e+00 ppl=3.78 best_loss=1.2916e+00 best_ppl=3.64                                            
Validation Y2X - loss=1.0943e+00 ppl=2.99 best_loss=1.0858e+00 best_ppl=2.96
Epoch 19 - |param|=8.64e+02 |g_param|=2.06e+05 loss_x2y=1.5213e+00 ppl_x2y=4.58 loss_y2x=1.2945e+00 ppl_y2x=3.65 dual_loss=0.0000e+00
Validation X2Y - loss=1.2781e+00 ppl=3.59 best_loss=1.2916e+00 best_ppl=3.64                                            
Validation Y2X - loss=1.0576e+00 ppl=2.88 best_loss=1.0858e+00 best_ppl=2.96
Epoch 20 - |param|=8.65e+02 |g_param|=2.23e+05 loss_x2y=1.5690e+00 ppl_x2y=4.80 loss_y2x=1.3201e+00 ppl_y2x=3.74 dual_loss=0.0000e+00
Validation X2Y - loss=1.2643e+00 ppl=3.54 best_loss=1.2781e+00 best_ppl=3.59                                            
Validation Y2X - loss=1.0531e+00 ppl=2.87 best_loss=1.0576e+00 best_ppl=2.88
Epoch 21 - |param|=8.65e+02 |g_param|=2.13e+05 loss_x2y=1.5321e+00 ppl_x2y=4.63 loss_y2x=1.3144e+00 ppl_y2x=3.72 dual_loss=6.0753e-01
Validation X2Y - loss=1.2853e+00 ppl=3.62 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.0708e+00 ppl=2.92 best_loss=1.0531e+00 best_ppl=2.87
Epoch 22 - |param|=8.66e+02 |g_param|=2.24e+05 loss_x2y=1.4124e+00 ppl_x2y=4.11 loss_y2x=1.2139e+00 ppl_y2x=3.37 dual_loss=5.2452e-01
Validation X2Y - loss=1.2914e+00 ppl=3.64 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.0616e+00 ppl=2.89 best_loss=1.0531e+00 best_ppl=2.87
Epoch 23 - |param|=8.66e+02 |g_param|=2.25e+05 loss_x2y=1.4491e+00 ppl_x2y=4.26 loss_y2x=1.2782e+00 ppl_y2x=3.59 dual_loss=5.3370e-01
Validation X2Y - loss=1.2844e+00 ppl=3.61 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.0489e+00 ppl=2.85 best_loss=1.0531e+00 best_ppl=2.87
Epoch 24 - |param|=8.67e+02 |g_param|=2.29e+05 loss_x2y=1.3437e+00 ppl_x2y=3.83 loss_y2x=1.1393e+00 ppl_y2x=3.12 dual_loss=4.9610e-01
Validation X2Y - loss=1.3214e+00 ppl=3.75 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.0710e+00 ppl=2.92 best_loss=1.0489e+00 best_ppl=2.85
Epoch 25 - |param|=8.67e+02 |g_param|=2.20e+05 loss_x2y=1.3372e+00 ppl_x2y=3.81 loss_y2x=1.1278e+00 ppl_y2x=3.09 dual_loss=5.1546e-01
Validation X2Y - loss=1.3503e+00 ppl=3.86 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.0761e+00 ppl=2.93 best_loss=1.0489e+00 best_ppl=2.85
Epoch 26 - |param|=8.68e+02 |g_param|=2.32e+05 loss_x2y=1.3124e+00 ppl_x2y=3.71 loss_y2x=1.1244e+00 ppl_y2x=3.08 dual_loss=5.0240e-01
Validation X2Y - loss=1.3182e+00 ppl=3.74 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.0761e+00 ppl=2.93 best_loss=1.0489e+00 best_ppl=2.85
Epoch 27 - |param|=8.69e+02 |g_param|=2.27e+05 loss_x2y=1.2771e+00 ppl_x2y=3.59 loss_y2x=1.0796e+00 ppl_y2x=2.94 dual_loss=5.1362e-01
Validation X2Y - loss=1.3510e+00 ppl=3.86 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.0948e+00 ppl=2.99 best_loss=1.0489e+00 best_ppl=2.85
Epoch 28 - |param|=8.69e+02 |g_param|=2.50e+05 loss_x2y=1.2449e+00 ppl_x2y=3.47 loss_y2x=1.0456e+00 ppl_y2x=2.85 dual_loss=5.3103e-01
Validation X2Y - loss=1.3340e+00 ppl=3.80 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.0883e+00 ppl=2.97 best_loss=1.0489e+00 best_ppl=2.85
Epoch 29 - |param|=8.70e+02 |g_param|=2.32e+05 loss_x2y=1.2093e+00 ppl_x2y=3.35 loss_y2x=1.0180e+00 ppl_y2x=2.77 dual_loss=5.2799e-01
Validation X2Y - loss=1.3532e+00 ppl=3.87 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.0881e+00 ppl=2.97 best_loss=1.0489e+00 best_ppl=2.85
Epoch 30 - |param|=8.70e+02 |g_param|=2.48e+05 loss_x2y=1.2040e+00 ppl_x2y=3.33 loss_y2x=1.0374e+00 ppl_y2x=2.82 dual_loss=5.5229e-01
Validation X2Y - loss=1.3621e+00 ppl=3.90 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.0641e+00 ppl=2.90 best_loss=1.0489e+00 best_ppl=2.85
Epoch 31 - |param|=8.71e+02 |g_param|=2.35e+05 loss_x2y=1.1731e+00 ppl_x2y=3.23 loss_y2x=9.8333e-01 ppl_y2x=2.67 dual_loss=5.1486e-01
Validation X2Y - loss=1.3472e+00 ppl=3.85 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.0807e+00 ppl=2.95 best_loss=1.0489e+00 best_ppl=2.85
Epoch 32 - |param|=8.71e+02 |g_param|=2.48e+05 loss_x2y=1.1294e+00 ppl_x2y=3.09 loss_y2x=9.5722e-01 ppl_y2x=2.60 dual_loss=5.3752e-01
Validation X2Y - loss=1.3818e+00 ppl=3.98 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.0546e+00 ppl=2.87 best_loss=1.0489e+00 best_ppl=2.85
Epoch 33 - |param|=8.72e+02 |g_param|=2.49e+05 loss_x2y=1.2301e+00 ppl_x2y=3.42 loss_y2x=1.0029e+00 ppl_y2x=2.73 dual_loss=7.3989e-01
Validation X2Y - loss=1.3687e+00 ppl=3.93 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.0681e+00 ppl=2.91 best_loss=1.0489e+00 best_ppl=2.85
Epoch 34 - |param|=8.72e+02 |g_param|=4.63e+05 loss_x2y=1.0887e+00 ppl_x2y=2.97 loss_y2x=9.2391e-01 ppl_y2x=2.52 dual_loss=5.4080e-01
Validation X2Y - loss=1.3834e+00 ppl=3.99 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.1026e+00 ppl=3.01 best_loss=1.0489e+00 best_ppl=2.85
Epoch 35 - |param|=8.73e+02 |g_param|=4.98e+05 loss_x2y=1.1643e+00 ppl_x2y=3.20 loss_y2x=9.7028e-01 ppl_y2x=2.64 dual_loss=7.9817e-01
Validation X2Y - loss=1.4024e+00 ppl=4.07 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.1107e+00 ppl=3.04 best_loss=1.0489e+00 best_ppl=2.85
Epoch 36 - |param|=8.73e+02 |g_param|=5.11e+05 loss_x2y=1.0247e+00 ppl_x2y=2.79 loss_y2x=8.6040e-01 ppl_y2x=2.36 dual_loss=5.8349e-01
Validation X2Y - loss=1.3862e+00 ppl=4.00 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.1468e+00 ppl=3.15 best_loss=1.0489e+00 best_ppl=2.85
Epoch 37 - |param|=8.74e+02 |g_param|=4.86e+05 loss_x2y=1.0208e+00 ppl_x2y=2.78 loss_y2x=8.5844e-01 ppl_y2x=2.36 dual_loss=6.0380e-01
Validation X2Y - loss=1.4558e+00 ppl=4.29 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.1106e+00 ppl=3.04 best_loss=1.0489e+00 best_ppl=2.85
Epoch 38 - |param|=8.74e+02 |g_param|=5.13e+05 loss_x2y=1.0237e+00 ppl_x2y=2.78 loss_y2x=8.5132e-01 ppl_y2x=2.34 dual_loss=5.8353e-01
Validation X2Y - loss=1.4541e+00 ppl=4.28 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.1269e+00 ppl=3.09 best_loss=1.0489e+00 best_ppl=2.85
Epoch 39 - |param|=8.75e+02 |g_param|=5.05e+05 loss_x2y=1.0033e+00 ppl_x2y=2.73 loss_y2x=8.2849e-01 ppl_y2x=2.29 dual_loss=6.3511e-01
Validation X2Y - loss=1.4556e+00 ppl=4.29 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.1115e+00 ppl=3.04 best_loss=1.0489e+00 best_ppl=2.85
Epoch 40 - |param|=8.75e+02 |g_param|=5.01e+05 loss_x2y=9.4898e-01 ppl_x2y=2.58 loss_y2x=7.8888e-01 ppl_y2x=2.20 dual_loss=6.1658e-01
Validation X2Y - loss=1.4587e+00 ppl=4.30 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.1223e+00 ppl=3.07 best_loss=1.0489e+00 best_ppl=2.85
Epoch 41 - |param|=8.76e+02 |g_param|=4.91e+05 loss_x2y=9.4137e-01 ppl_x2y=2.56 loss_y2x=7.7775e-01 ppl_y2x=2.18 dual_loss=6.2774e-01
Validation X2Y - loss=1.4738e+00 ppl=4.37 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.1551e+00 ppl=3.17 best_loss=1.0489e+00 best_ppl=2.85
Epoch 42 - |param|=8.76e+02 |g_param|=5.01e+05 loss_x2y=9.4271e-01 ppl_x2y=2.57 loss_y2x=7.7646e-01 ppl_y2x=2.17 dual_loss=6.5831e-01
Validation X2Y - loss=1.4868e+00 ppl=4.42 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.1415e+00 ppl=3.13 best_loss=1.0489e+00 best_ppl=2.85
Epoch 43 - |param|=8.77e+02 |g_param|=4.99e+05 loss_x2y=9.2495e-01 ppl_x2y=2.52 loss_y2x=7.7131e-01 ppl_y2x=2.16 dual_loss=6.8080e-01
Validation X2Y - loss=1.4690e+00 ppl=4.34 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.1774e+00 ppl=3.25 best_loss=1.0489e+00 best_ppl=2.85
Epoch 44 - |param|=8.77e+02 |g_param|=5.49e+05 loss_x2y=9.1684e-01 ppl_x2y=2.50 loss_y2x=7.7120e-01 ppl_y2x=2.16 dual_loss=7.1049e-01
Validation X2Y - loss=1.4903e+00 ppl=4.44 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.1277e+00 ppl=3.09 best_loss=1.0489e+00 best_ppl=2.85
Epoch 45 - |param|=8.78e+02 |g_param|=5.18e+05 loss_x2y=9.8552e-01 ppl_x2y=2.68 loss_y2x=8.2712e-01 ppl_y2x=2.29 dual_loss=8.7448e-01
Validation X2Y - loss=1.4784e+00 ppl=4.39 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.1811e+00 ppl=3.26 best_loss=1.0489e+00 best_ppl=2.85
Epoch 46 - |param|=8.78e+02 |g_param|=5.15e+05 loss_x2y=8.8951e-01 ppl_x2y=2.43 loss_y2x=7.3763e-01 ppl_y2x=2.09 dual_loss=7.0993e-01
Validation X2Y - loss=1.4866e+00 ppl=4.42 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.1646e+00 ppl=3.20 best_loss=1.0489e+00 best_ppl=2.85
Epoch 47 - |param|=8.79e+02 |g_param|=5.17e+05 loss_x2y=9.5640e-01 ppl_x2y=2.60 loss_y2x=7.6502e-01 ppl_y2x=2.15 dual_loss=8.7628e-01
Validation X2Y - loss=1.4917e+00 ppl=4.44 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.1927e+00 ppl=3.30 best_loss=1.0489e+00 best_ppl=2.85
Epoch 48 - |param|=8.79e+02 |g_param|=5.43e+05 loss_x2y=8.8205e-01 ppl_x2y=2.42 loss_y2x=7.3164e-01 ppl_y2x=2.08 dual_loss=7.3938e-01
Validation X2Y - loss=1.5081e+00 ppl=4.52 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.1634e+00 ppl=3.20 best_loss=1.0489e+00 best_ppl=2.85
Epoch 49 - |param|=8.80e+02 |g_param|=5.04e+05 loss_x2y=8.5837e-01 ppl_x2y=2.36 loss_y2x=6.8217e-01 ppl_y2x=1.98 dual_loss=7.1930e-01
Validation X2Y - loss=1.5500e+00 ppl=4.71 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.2315e+00 ppl=3.43 best_loss=1.0489e+00 best_ppl=2.85
Epoch 50 - |param|=8.80e+02 |g_param|=5.36e+05 loss_x2y=8.3468e-01 ppl_x2y=2.30 loss_y2x=7.0233e-01 ppl_y2x=2.02 dual_loss=8.2413e-01
Validation X2Y - loss=1.5235e+00 ppl=4.59 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.1932e+00 ppl=3.30 best_loss=1.0489e+00 best_ppl=2.85
Epoch 51 - |param|=8.81e+02 |g_param|=5.02e+05 loss_x2y=8.2176e-01 ppl_x2y=2.27 loss_y2x=6.8328e-01 ppl_y2x=1.98 dual_loss=7.3803e-01
Validation X2Y - loss=1.5583e+00 ppl=4.75 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.2202e+00 ppl=3.39 best_loss=1.0489e+00 best_ppl=2.85
Epoch 52 - |param|=8.81e+02 |g_param|=5.28e+05 loss_x2y=7.8648e-01 ppl_x2y=2.20 loss_y2x=6.4969e-01 ppl_y2x=1.91 dual_loss=7.2434e-01
Validation X2Y - loss=1.5444e+00 ppl=4.69 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.2429e+00 ppl=3.47 best_loss=1.0489e+00 best_ppl=2.85
Epoch 53 - |param|=8.81e+02 |g_param|=4.99e+05 loss_x2y=7.7557e-01 ppl_x2y=2.17 loss_y2x=6.4107e-01 ppl_y2x=1.90 dual_loss=7.4347e-01
Validation X2Y - loss=1.5665e+00 ppl=4.79 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.2387e+00 ppl=3.45 best_loss=1.0489e+00 best_ppl=2.85
Epoch 54 - |param|=8.82e+02 |g_param|=5.09e+05 loss_x2y=7.8379e-01 ppl_x2y=2.19 loss_y2x=6.4412e-01 ppl_y2x=1.90 dual_loss=7.6694e-01
Validation X2Y - loss=1.6232e+00 ppl=5.07 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.2233e+00 ppl=3.40 best_loss=1.0489e+00 best_ppl=2.85
Epoch 55 - |param|=8.82e+02 |g_param|=4.99e+05 loss_x2y=7.7194e-01 ppl_x2y=2.16 loss_y2x=6.4664e-01 ppl_y2x=1.91 dual_loss=8.1511e-01
Validation X2Y - loss=1.6313e+00 ppl=5.11 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.2401e+00 ppl=3.46 best_loss=1.0489e+00 best_ppl=2.85
Epoch 56 - |param|=8.83e+02 |g_param|=5.33e+05 loss_x2y=7.5647e-01 ppl_x2y=2.13 loss_y2x=6.2840e-01 ppl_y2x=1.87 dual_loss=8.1675e-01
Validation X2Y - loss=1.6177e+00 ppl=5.04 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.2994e+00 ppl=3.67 best_loss=1.0489e+00 best_ppl=2.85
Epoch 57 - |param|=8.83e+02 |g_param|=5.12e+05 loss_x2y=8.4418e-01 ppl_x2y=2.33 loss_y2x=6.6130e-01 ppl_y2x=1.94 dual_loss=9.6385e-01
Validation X2Y - loss=1.5889e+00 ppl=4.90 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.3135e+00 ppl=3.72 best_loss=1.0489e+00 best_ppl=2.85
Epoch 58 - |param|=8.84e+02 |g_param|=5.31e+05 loss_x2y=8.3895e-01 ppl_x2y=2.31 loss_y2x=6.6916e-01 ppl_y2x=1.95 dual_loss=1.0513e+00
Validation X2Y - loss=1.5799e+00 ppl=4.85 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.3094e+00 ppl=3.70 best_loss=1.0489e+00 best_ppl=2.85
Epoch 59 - |param|=8.84e+02 |g_param|=5.04e+05 loss_x2y=7.8288e-01 ppl_x2y=2.19 loss_y2x=6.2205e-01 ppl_y2x=1.86 dual_loss=9.1145e-01
Validation X2Y - loss=1.5943e+00 ppl=4.92 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.3066e+00 ppl=3.69 best_loss=1.0489e+00 best_ppl=2.85
Epoch 60 - |param|=8.85e+02 |g_param|=5.14e+05 loss_x2y=7.4069e-01 ppl_x2y=2.10 loss_y2x=6.0025e-01 ppl_y2x=1.82 dual_loss=8.8220e-01
Validation X2Y - loss=1.6266e+00 ppl=5.09 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.3088e+00 ppl=3.70 best_loss=1.0489e+00 best_ppl=2.85
Epoch 61 - |param|=8.85e+02 |g_param|=5.00e+05 loss_x2y=7.1986e-01 ppl_x2y=2.05 loss_y2x=5.7521e-01 ppl_y2x=1.78 dual_loss=8.4051e-01
Validation X2Y - loss=1.5944e+00 ppl=4.93 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.3062e+00 ppl=3.69 best_loss=1.0489e+00 best_ppl=2.85
Epoch 62 - |param|=8.86e+02 |g_param|=5.20e+05 loss_x2y=7.1891e-01 ppl_x2y=2.05 loss_y2x=5.9514e-01 ppl_y2x=1.81 dual_loss=8.8711e-01
Validation X2Y - loss=1.6119e+00 ppl=5.01 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.2921e+00 ppl=3.64 best_loss=1.0489e+00 best_ppl=2.85
Epoch 63 - |param|=8.86e+02 |g_param|=4.98e+05 loss_x2y=7.1392e-01 ppl_x2y=2.04 loss_y2x=5.6965e-01 ppl_y2x=1.77 dual_loss=8.8203e-01
Validation X2Y - loss=1.6445e+00 ppl=5.18 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.3314e+00 ppl=3.79 best_loss=1.0489e+00 best_ppl=2.85
Epoch 64 - |param|=8.86e+02 |g_param|=5.15e+05 loss_x2y=6.9849e-01 ppl_x2y=2.01 loss_y2x=5.8007e-01 ppl_y2x=1.79 dual_loss=9.1125e-01
Validation X2Y - loss=1.6489e+00 ppl=5.20 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.3222e+00 ppl=3.75 best_loss=1.0489e+00 best_ppl=2.85
Epoch 65 - |param|=8.87e+02 |g_param|=5.10e+05 loss_x2y=7.1148e-01 ppl_x2y=2.04 loss_y2x=5.7507e-01 ppl_y2x=1.78 dual_loss=9.7152e-01
Validation X2Y - loss=1.6290e+00 ppl=5.10 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.3157e+00 ppl=3.73 best_loss=1.0489e+00 best_ppl=2.85
Epoch 66 - |param|=8.87e+02 |g_param|=8.02e+05 loss_x2y=6.7557e-01 ppl_x2y=1.97 loss_y2x=5.5431e-01 ppl_y2x=1.74 dual_loss=8.7262e-01
Validation X2Y - loss=1.6653e+00 ppl=5.29 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.3299e+00 ppl=3.78 best_loss=1.0489e+00 best_ppl=2.85
Epoch 67 - |param|=8.88e+02 |g_param|=8.06e+05 loss_x2y=6.8584e-01 ppl_x2y=1.99 loss_y2x=5.4695e-01 ppl_y2x=1.73 dual_loss=8.7694e-01
Validation X2Y - loss=1.6445e+00 ppl=5.18 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.3473e+00 ppl=3.85 best_loss=1.0489e+00 best_ppl=2.85
Epoch 68 - |param|=8.88e+02 |g_param|=8.36e+05 loss_x2y=6.8816e-01 ppl_x2y=1.99 loss_y2x=5.5393e-01 ppl_y2x=1.74 dual_loss=9.3749e-01
Validation X2Y - loss=1.6084e+00 ppl=4.99 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.3257e+00 ppl=3.76 best_loss=1.0489e+00 best_ppl=2.85
Epoch 69 - |param|=8.89e+02 |g_param|=7.85e+05 loss_x2y=6.7796e-01 ppl_x2y=1.97 loss_y2x=5.5783e-01 ppl_y2x=1.75 dual_loss=9.6481e-01
Validation X2Y - loss=1.6281e+00 ppl=5.09 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.3125e+00 ppl=3.72 best_loss=1.0489e+00 best_ppl=2.85
Epoch 70 - |param|=8.89e+02 |g_param|=8.27e+05 loss_x2y=6.6022e-01 ppl_x2y=1.94 loss_y2x=5.3935e-01 ppl_y2x=1.71 dual_loss=9.1815e-01
Validation X2Y - loss=1.6676e+00 ppl=5.30 best_loss=1.2643e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.3595e+00 ppl=3.89 best_loss=1.0489e+00 best_ppl=2.85

real	22m45.269s
user	22m22.692s
sys	0m20.361s

```

testing/evaluation...  

```
/home/ye/exp/simple-nmt/model/dsl/transformer/mybk-70epoch
Evaluation result for the model: dsl-model-mybk.01.4.46-86.30.4.10-60.15.3.53-34.14.3.18-24.13.pth, mybk
BLEU = 4.99, 22.4/6.6/2.9/1.6 (BP=0.976, ratio=0.976, hyp_len=11161, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.46-86.30.4.10-60.15.3.53-34.14.3.18-24.13.pth, bkmy
BLEU = 4.27, 27.3/7.4/2.6/0.7 (BP=0.970, ratio=0.970, hyp_len=11865, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.02.3.58-35.99.3.18-24.03.3.00-20.05.2.72-15.12.pth, mybk
BLEU = 1.72, 8.3/2.4/1.0/0.5 (BP=1.000, ratio=2.609, hyp_len=29823, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.3.58-35.99.3.18-24.03.3.00-20.05.2.72-15.12.pth, bkmy
BLEU = 4.44, 22.8/7.3/2.6/0.9 (BP=1.000, ratio=1.404, hyp_len=17178, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.3.26-25.97.2.91-18.27.2.54-12.66.2.35-10.47.pth, mybk
BLEU = 8.00, 30.2/11.3/5.1/2.4 (BP=1.000, ratio=1.014, hyp_len=11594, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.3.26-25.97.2.91-18.27.2.54-12.66.2.35-10.47.pth, bkmy
BLEU = 8.97, 37.5/14.3/5.9/2.4 (BP=0.960, ratio=0.961, hyp_len=11756, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.3.00-20.01.2.64-14.07.2.26-9.54.2.08-7.98.pth, mybk
BLEU = 8.51, 28.3/11.6/5.6/2.8 (BP=1.000, ratio=1.261, hyp_len=14416, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.3.00-20.01.2.64-14.07.2.26-9.54.2.08-7.98.pth, bkmy
BLEU = 12.37, 40.4/17.8/8.4/4.0 (BP=0.992, ratio=0.992, hyp_len=12130, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.2.82-16.85.2.47-11.77.2.07-7.96.1.91-6.75.pth, mybk
BLEU = 14.66, 41.0/18.9/10.4/5.9 (BP=0.994, ratio=0.994, hyp_len=11361, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.2.82-16.85.2.47-11.77.2.07-7.96.1.91-6.75.pth, bkmy
BLEU = 13.30, 38.9/18.6/9.3/4.7 (BP=1.000, ratio=1.199, hyp_len=14664, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.2.59-13.32.2.28-9.78.1.84-6.31.1.71-5.54.pth, mybk
BLEU = 14.77, 37.7/18.8/10.8/6.2 (BP=1.000, ratio=1.171, hyp_len=13389, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.2.59-13.32.2.28-9.78.1.84-6.31.1.71-5.54.pth, bkmy
BLEU = 19.08, 46.6/24.8/14.1/8.1 (BP=1.000, ratio=1.079, hyp_len=13200, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.2.50-12.15.2.17-8.78.1.69-5.42.1.52-4.59.pth, mybk
BLEU = 20.99, 47.6/26.0/15.9/9.9 (BP=1.000, ratio=1.072, hyp_len=12251, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.2.50-12.15.2.17-8.78.1.69-5.42.1.52-4.59.pth, bkmy
BLEU = 26.28, 59.4/35.7/22.5/14.6 (BP=0.910, ratio=0.913, hyp_len=11173, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.2.35-10.53.2.04-7.69.1.59-4.91.1.43-4.20.pth, mybk
BLEU = 22.74, 49.4/27.8/17.3/11.2 (BP=1.000, ratio=1.078, hyp_len=12319, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.2.35-10.53.2.04-7.69.1.59-4.91.1.43-4.20.pth, bkmy
BLEU = 26.61, 53.4/33.1/20.9/13.6 (BP=1.000, ratio=1.100, hyp_len=13449, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.2.21-9.16.1.93-6.87.1.55-4.73.1.35-3.85.pth, mybk
BLEU = 25.16, 52.7/30.3/19.3/13.0 (BP=1.000, ratio=1.006, hyp_len=11496, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.2.21-9.16.1.93-6.87.1.55-4.73.1.35-3.85.pth, bkmy
BLEU = 28.15, 55.1/34.3/22.2/14.9 (BP=1.000, ratio=1.071, hyp_len=13103, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.2.08-7.99.1.80-6.02.1.47-4.35.1.24-3.46.pth, mybk
BLEU = 25.02, 52.0/30.3/19.3/12.9 (BP=1.000, ratio=1.086, hyp_len=12417, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.2.08-7.99.1.80-6.02.1.47-4.35.1.24-3.46.pth, bkmy
BLEU = 33.56, 61.1/40.1/27.1/19.1 (BP=1.000, ratio=1.013, hyp_len=12385, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.2.04-7.68.1.76-5.83.1.41-4.08.1.21-3.36.pth, mybk
BLEU = 29.08, 56.9/34.8/22.9/15.8 (BP=1.000, ratio=1.024, hyp_len=11704, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.2.04-7.68.1.76-5.83.1.41-4.08.1.21-3.36.pth, bkmy
BLEU = 36.22, 63.9/43.1/29.9/21.5 (BP=0.993, ratio=0.993, hyp_len=12146, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.2.08-8.03.1.84-6.27.1.39-4.03.1.18-3.27.pth, mybk
BLEU = 29.14, 56.8/34.5/22.9/16.1 (BP=1.000, ratio=1.024, hyp_len=11702, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.2.08-8.03.1.84-6.27.1.39-4.03.1.18-3.27.pth, bkmy
BLEU = 35.47, 61.9/41.8/29.1/21.0 (BP=1.000, ratio=1.041, hyp_len=12730, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.1.90-6.70.1.66-5.24.1.35-3.85.1.16-3.19.pth, mybk
BLEU = 29.50, 56.9/35.0/23.4/16.2 (BP=1.000, ratio=1.061, hyp_len=12126, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.1.90-6.70.1.66-5.24.1.35-3.85.1.16-3.19.pth, bkmy
BLEU = 36.86, 63.5/43.3/30.5/22.4 (BP=0.996, ratio=0.996, hyp_len=12182, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.1.79-6.02.1.55-4.70.1.33-3.79.1.15-3.17.pth, mybk
BLEU = 31.70, 60.0/37.7/25.3/17.6 (BP=1.000, ratio=1.031, hyp_len=11791, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.1.79-6.02.1.55-4.70.1.33-3.79.1.15-3.17.pth, bkmy
BLEU = 37.55, 63.8/44.3/31.2/22.6 (BP=1.000, ratio=1.061, hyp_len=12979, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.1.90-6.66.1.57-4.82.1.32-3.74.1.10-3.01.pth, mybk
BLEU = 31.84, 59.0/37.6/25.6/18.1 (BP=1.000, ratio=1.041, hyp_len=11905, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.1.90-6.66.1.57-4.82.1.32-3.74.1.10-3.01.pth, bkmy
BLEU = 39.65, 66.1/46.2/33.0/24.5 (BP=1.000, ratio=1.011, hyp_len=12369, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.1.67-5.32.1.45-4.26.1.30-3.66.1.10-3.02.pth, mybk
BLEU = 31.81, 58.9/37.5/25.6/18.1 (BP=1.000, ratio=1.069, hyp_len=12220, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.1.67-5.32.1.45-4.26.1.30-3.66.1.10-3.02.pth, bkmy
BLEU = 39.16, 65.9/45.9/32.6/23.8 (BP=1.000, ratio=1.031, hyp_len=12611, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.1.64-5.14.1.40-4.06.1.29-3.64.1.09-2.96.pth, mybk
BLEU = 32.53, 59.7/38.1/26.2/18.8 (BP=1.000, ratio=1.033, hyp_len=11804, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.1.64-5.14.1.40-4.06.1.29-3.64.1.09-2.96.pth, bkmy
BLEU = 39.83, 65.9/46.2/33.3/24.9 (BP=1.000, ratio=1.010, hyp_len=12358, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.1.61-5.01.1.41-4.08.1.33-3.78.1.09-2.99.pth, mybk
BLEU = 29.87, 56.2/35.2/23.9/16.8 (BP=1.000, ratio=1.068, hyp_len=12208, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.1.61-5.01.1.41-4.08.1.33-3.78.1.09-2.99.pth, bkmy
BLEU = 40.75, 66.4/47.2/34.3/25.6 (BP=1.000, ratio=1.021, hyp_len=12485, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.1.52-4.58.1.29-3.65.1.28-3.59.1.06-2.88.pth, mybk
BLEU = 33.04, 60.4/38.7/26.7/19.1 (BP=1.000, ratio=1.055, hyp_len=12062, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.1.52-4.58.1.29-3.65.1.28-3.59.1.06-2.88.pth, bkmy
BLEU = 41.27, 67.9/48.2/34.5/25.7 (BP=1.000, ratio=1.031, hyp_len=12605, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.1.57-4.80.1.32-3.74.1.26-3.54.1.05-2.87.pth, mybk
BLEU = 34.91, 63.0/40.8/28.3/20.4 (BP=1.000, ratio=1.034, hyp_len=11822, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.1.57-4.80.1.32-3.74.1.26-3.54.1.05-2.87.pth, bkmy
BLEU = 40.81, 67.2/47.6/34.3/25.3 (BP=1.000, ratio=1.030, hyp_len=12604, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.1.53-4.63.1.31-3.72.1.29-3.62.1.07-2.92.pth, mybk
BLEU = 34.42, 62.2/40.0/27.8/20.3 (BP=1.000, ratio=1.022, hyp_len=11684, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.1.53-4.63.1.31-3.72.1.29-3.62.1.07-2.92.pth, bkmy
BLEU = 39.85, 66.2/46.7/33.4/24.4 (BP=1.000, ratio=1.063, hyp_len=12997, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.1.41-4.11.1.21-3.37.1.29-3.64.1.06-2.89.pth, mybk
BLEU = 34.08, 62.1/39.9/27.6/19.7 (BP=1.000, ratio=1.020, hyp_len=11661, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.1.41-4.11.1.21-3.37.1.29-3.64.1.06-2.89.pth, bkmy
BLEU = 40.90, 67.0/47.3/34.3/25.7 (BP=1.000, ratio=1.027, hyp_len=12556, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.1.45-4.26.1.28-3.59.1.28-3.61.1.05-2.85.pth, mybk
BLEU = 32.98, 60.7/39.0/26.6/18.8 (BP=1.000, ratio=1.062, hyp_len=12140, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.1.45-4.26.1.28-3.59.1.28-3.61.1.05-2.85.pth, bkmy
BLEU = 41.12, 66.9/47.5/34.5/26.1 (BP=1.000, ratio=1.022, hyp_len=12498, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.1.34-3.83.1.14-3.12.1.32-3.75.1.07-2.92.pth, mybk
BLEU = 32.50, 59.8/38.2/26.2/18.6 (BP=1.000, ratio=1.070, hyp_len=12229, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.1.34-3.83.1.14-3.12.1.32-3.75.1.07-2.92.pth, bkmy
BLEU = 42.10, 67.9/48.5/35.4/26.9 (BP=1.000, ratio=1.021, hyp_len=12493, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.1.34-3.81.1.13-3.09.1.35-3.86.1.08-2.93.pth, mybk
BLEU = 34.90, 63.1/40.8/28.1/20.5 (BP=1.000, ratio=1.003, hyp_len=11467, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.1.34-3.81.1.13-3.09.1.35-3.86.1.08-2.93.pth, bkmy
BLEU = 40.82, 66.9/47.3/34.2/25.6 (BP=1.000, ratio=1.035, hyp_len=12661, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.1.31-3.71.1.12-3.08.1.32-3.74.1.08-2.93.pth, mybk
BLEU = 32.28, 59.0/37.9/26.0/18.6 (BP=1.000, ratio=1.077, hyp_len=12313, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.1.31-3.71.1.12-3.08.1.32-3.74.1.08-2.93.pth, bkmy
BLEU = 42.07, 68.2/48.6/35.5/26.6 (BP=1.000, ratio=1.031, hyp_len=12606, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.1.28-3.59.1.08-2.94.1.35-3.86.1.09-2.99.pth, mybk
BLEU = 32.99, 61.1/38.8/26.5/18.8 (BP=1.000, ratio=1.036, hyp_len=11844, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.1.28-3.59.1.08-2.94.1.35-3.86.1.09-2.99.pth, bkmy
BLEU = 38.45, 64.4/44.6/32.0/23.7 (BP=1.000, ratio=1.065, hyp_len=13023, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.1.24-3.47.1.05-2.85.1.33-3.80.1.09-2.97.pth, mybk
BLEU = 32.07, 58.9/37.7/25.8/18.5 (BP=1.000, ratio=1.078, hyp_len=12325, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.1.24-3.47.1.05-2.85.1.33-3.80.1.09-2.97.pth, bkmy
BLEU = 41.56, 67.4/47.8/35.0/26.4 (BP=1.000, ratio=1.018, hyp_len=12446, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.1.21-3.35.1.02-2.77.1.35-3.87.1.09-2.97.pth, mybk
BLEU = 32.89, 59.9/38.6/26.7/19.0 (BP=1.000, ratio=1.068, hyp_len=12215, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.1.21-3.35.1.02-2.77.1.35-3.87.1.09-2.97.pth, bkmy
BLEU = 38.59, 64.4/44.9/32.2/23.8 (BP=1.000, ratio=1.063, hyp_len=13003, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.1.20-3.33.1.04-2.82.1.36-3.90.1.06-2.90.pth, mybk
BLEU = 32.88, 60.0/38.5/26.6/19.1 (BP=1.000, ratio=1.053, hyp_len=12034, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.1.20-3.33.1.04-2.82.1.36-3.90.1.06-2.90.pth, bkmy
BLEU = 40.44, 65.7/46.6/34.0/25.7 (BP=1.000, ratio=1.063, hyp_len=12996, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.31.1.17-3.23.0.98-2.67.1.35-3.85.1.08-2.95.pth, mybk
BLEU = 32.84, 60.3/38.6/26.5/18.8 (BP=1.000, ratio=1.070, hyp_len=12233, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.31.1.17-3.23.0.98-2.67.1.35-3.85.1.08-2.95.pth, bkmy
BLEU = 40.67, 66.7/47.2/34.1/25.5 (BP=1.000, ratio=1.028, hyp_len=12570, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.32.1.13-3.09.0.96-2.60.1.38-3.98.1.05-2.87.pth, mybk
BLEU = 33.14, 60.5/38.9/26.8/19.2 (BP=1.000, ratio=1.061, hyp_len=12126, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.32.1.13-3.09.0.96-2.60.1.38-3.98.1.05-2.87.pth, bkmy
BLEU = 39.98, 66.4/46.7/33.4/24.7 (BP=1.000, ratio=1.055, hyp_len=12903, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.33.1.23-3.42.1.00-2.73.1.37-3.93.1.07-2.91.pth, mybk
BLEU = 32.49, 59.6/38.1/26.1/18.8 (BP=1.000, ratio=1.082, hyp_len=12366, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.33.1.23-3.42.1.00-2.73.1.37-3.93.1.07-2.91.pth, bkmy
BLEU = 40.55, 66.9/47.2/34.1/25.1 (BP=1.000, ratio=1.048, hyp_len=12814, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.34.1.09-2.97.0.92-2.52.1.38-3.99.1.10-3.01.pth, mybk
BLEU = 32.54, 59.9/38.2/26.2/18.7 (BP=1.000, ratio=1.063, hyp_len=12154, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.34.1.09-2.97.0.92-2.52.1.38-3.99.1.10-3.01.pth, bkmy
BLEU = 40.41, 66.1/46.8/33.8/25.5 (BP=1.000, ratio=1.054, hyp_len=12894, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.35.1.16-3.20.0.97-2.64.1.40-4.07.1.11-3.04.pth, mybk
BLEU = 32.19, 59.3/37.6/25.9/18.6 (BP=1.000, ratio=1.059, hyp_len=12101, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.35.1.16-3.20.0.97-2.64.1.40-4.07.1.11-3.04.pth, bkmy
BLEU = 39.47, 65.4/45.6/33.0/24.7 (BP=1.000, ratio=1.044, hyp_len=12774, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.36.1.02-2.79.0.86-2.36.1.39-4.00.1.15-3.15.pth, mybk
BLEU = 32.94, 59.8/38.5/26.6/19.3 (BP=1.000, ratio=1.066, hyp_len=12192, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.36.1.02-2.79.0.86-2.36.1.39-4.00.1.15-3.15.pth, bkmy
BLEU = 38.47, 64.2/44.8/32.0/23.8 (BP=1.000, ratio=1.076, hyp_len=13162, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.37.1.02-2.78.0.86-2.36.1.46-4.29.1.11-3.04.pth, mybk
BLEU = 31.13, 58.7/36.9/24.8/17.5 (BP=1.000, ratio=1.094, hyp_len=12506, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.37.1.02-2.78.0.86-2.36.1.46-4.29.1.11-3.04.pth, bkmy
BLEU = 39.18, 64.6/45.5/32.8/24.4 (BP=1.000, ratio=1.064, hyp_len=13019, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.38.1.02-2.78.0.85-2.34.1.45-4.28.1.13-3.09.pth, mybk
BLEU = 31.25, 58.1/36.7/25.0/17.9 (BP=1.000, ratio=1.090, hyp_len=12463, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.38.1.02-2.78.0.85-2.34.1.45-4.28.1.13-3.09.pth, bkmy
BLEU = 39.94, 66.3/46.5/33.4/24.7 (BP=1.000, ratio=1.037, hyp_len=12688, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.39.1.00-2.73.0.83-2.29.1.46-4.29.1.11-3.04.pth, mybk
BLEU = 33.40, 60.9/39.2/26.9/19.4 (BP=1.000, ratio=1.048, hyp_len=11980, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.39.1.00-2.73.0.83-2.29.1.46-4.29.1.11-3.04.pth, bkmy
BLEU = 37.90, 63.9/44.2/31.6/23.2 (BP=1.000, ratio=1.076, hyp_len=13158, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.40.0.95-2.58.0.79-2.20.1.46-4.30.1.12-3.07.pth, mybk
BLEU = 32.69, 60.0/38.2/26.4/18.9 (BP=1.000, ratio=1.072, hyp_len=12252, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.40.0.95-2.58.0.79-2.20.1.46-4.30.1.12-3.07.pth, bkmy
BLEU = 39.20, 65.0/45.6/32.8/24.2 (BP=1.000, ratio=1.050, hyp_len=12843, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.41.0.94-2.56.0.78-2.18.1.47-4.37.1.16-3.17.pth, mybk
BLEU = 29.80, 56.7/35.4/23.8/16.5 (BP=1.000, ratio=1.140, hyp_len=13038, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.41.0.94-2.56.0.78-2.18.1.47-4.37.1.16-3.17.pth, bkmy
BLEU = 37.77, 64.2/44.1/31.3/23.0 (BP=1.000, ratio=1.065, hyp_len=13024, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.42.0.94-2.57.0.78-2.17.1.49-4.42.1.14-3.13.pth, mybk
BLEU = 31.55, 58.5/37.0/25.3/18.1 (BP=1.000, ratio=1.063, hyp_len=12156, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.42.0.94-2.57.0.78-2.17.1.49-4.42.1.14-3.13.pth, bkmy
BLEU = 38.27, 64.2/44.5/31.9/23.5 (BP=1.000, ratio=1.067, hyp_len=13045, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.43.0.92-2.52.0.77-2.16.1.47-4.34.1.18-3.25.pth, mybk
BLEU = 30.74, 57.8/36.4/24.6/17.3 (BP=1.000, ratio=1.084, hyp_len=12397, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.43.0.92-2.52.0.77-2.16.1.47-4.34.1.18-3.25.pth, bkmy
BLEU = 39.85, 65.8/46.3/33.4/24.8 (BP=1.000, ratio=1.036, hyp_len=12674, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.44.0.92-2.50.0.77-2.16.1.49-4.44.1.13-3.09.pth, mybk
BLEU = 30.74, 57.6/36.0/24.5/17.6 (BP=1.000, ratio=1.088, hyp_len=12438, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.44.0.92-2.50.0.77-2.16.1.49-4.44.1.13-3.09.pth, bkmy
BLEU = 40.02, 65.9/46.1/33.4/25.3 (BP=1.000, ratio=1.044, hyp_len=12770, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.45.0.99-2.68.0.83-2.29.1.48-4.39.1.18-3.26.pth, mybk
BLEU = 31.55, 58.6/37.0/25.2/18.2 (BP=1.000, ratio=1.061, hyp_len=12126, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.45.0.99-2.68.0.83-2.29.1.48-4.39.1.18-3.26.pth, bkmy
BLEU = 37.01, 63.5/43.1/30.4/22.5 (BP=1.000, ratio=1.057, hyp_len=12928, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.46.0.89-2.43.0.74-2.09.1.49-4.42.1.16-3.20.pth, mybk
BLEU = 30.58, 57.5/35.9/24.4/17.4 (BP=1.000, ratio=1.071, hyp_len=12246, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.46.0.89-2.43.0.74-2.09.1.49-4.42.1.16-3.20.pth, bkmy
BLEU = 39.15, 64.7/45.0/32.7/24.7 (BP=1.000, ratio=1.050, hyp_len=12843, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.47.0.96-2.60.0.77-2.15.1.49-4.44.1.19-3.30.pth, mybk
BLEU = 30.74, 58.2/36.3/24.5/17.3 (BP=1.000, ratio=1.041, hyp_len=11905, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.47.0.96-2.60.0.77-2.15.1.49-4.44.1.19-3.30.pth, bkmy
BLEU = 37.12, 63.0/43.2/30.7/22.7 (BP=1.000, ratio=1.088, hyp_len=13303, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.48.0.88-2.42.0.73-2.08.1.51-4.52.1.16-3.20.pth, mybk
BLEU = 31.80, 59.6/37.7/25.4/17.9 (BP=1.000, ratio=1.058, hyp_len=12100, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.48.0.88-2.42.0.73-2.08.1.51-4.52.1.16-3.20.pth, bkmy
BLEU = 38.66, 64.9/44.9/32.0/23.9 (BP=1.000, ratio=1.045, hyp_len=12777, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.49.0.86-2.36.0.68-1.98.1.55-4.71.1.23-3.43.pth, mybk
BLEU = 32.05, 59.3/37.6/25.7/18.4 (BP=1.000, ratio=1.049, hyp_len=11991, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.49.0.86-2.36.0.68-1.98.1.55-4.71.1.23-3.43.pth, bkmy
BLEU = 35.60, 61.1/41.5/29.3/21.6 (BP=1.000, ratio=1.089, hyp_len=13318, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.50.0.83-2.30.0.70-2.02.1.52-4.59.1.19-3.30.pth, mybk
BLEU = 30.60, 57.9/36.3/24.4/17.1 (BP=1.000, ratio=1.068, hyp_len=12215, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.50.0.83-2.30.0.70-2.02.1.52-4.59.1.19-3.30.pth, bkmy
BLEU = 38.59, 64.8/44.9/31.9/23.9 (BP=1.000, ratio=1.045, hyp_len=12782, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.51.0.82-2.27.0.68-1.98.1.56-4.75.1.22-3.39.pth, mybk
BLEU = 30.11, 57.4/35.6/23.9/16.8 (BP=1.000, ratio=1.075, hyp_len=12292, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.51.0.82-2.27.0.68-1.98.1.56-4.75.1.22-3.39.pth, bkmy
BLEU = 37.48, 63.2/43.4/31.1/23.1 (BP=1.000, ratio=1.051, hyp_len=12852, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.52.0.79-2.20.0.65-1.91.1.54-4.69.1.24-3.47.pth, mybk
BLEU = 31.68, 59.3/37.1/25.3/18.1 (BP=1.000, ratio=1.044, hyp_len=11940, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.52.0.79-2.20.0.65-1.91.1.54-4.69.1.24-3.47.pth, bkmy
BLEU = 37.04, 63.1/43.0/30.6/22.7 (BP=1.000, ratio=1.053, hyp_len=12882, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.53.0.78-2.17.0.64-1.90.1.57-4.79.1.24-3.45.pth, mybk
BLEU = 32.12, 59.4/37.7/25.8/18.4 (BP=1.000, ratio=1.043, hyp_len=11926, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.53.0.78-2.17.0.64-1.90.1.57-4.79.1.24-3.45.pth, bkmy
BLEU = 37.11, 62.4/43.0/30.7/23.0 (BP=1.000, ratio=1.082, hyp_len=13235, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.54.0.78-2.19.0.64-1.90.1.62-5.07.1.22-3.40.pth, mybk
BLEU = 30.94, 58.3/36.2/24.7/17.6 (BP=1.000, ratio=1.052, hyp_len=12023, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.54.0.78-2.19.0.64-1.90.1.62-5.07.1.22-3.40.pth, bkmy
BLEU = 36.58, 62.4/42.7/30.3/22.1 (BP=1.000, ratio=1.052, hyp_len=12872, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.55.0.77-2.16.0.65-1.91.1.63-5.11.1.24-3.46.pth, mybk
BLEU = 31.19, 58.8/36.6/24.8/17.7 (BP=1.000, ratio=1.069, hyp_len=12222, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.55.0.77-2.16.0.65-1.91.1.63-5.11.1.24-3.46.pth, bkmy
BLEU = 36.41, 61.9/42.4/30.1/22.3 (BP=1.000, ratio=1.072, hyp_len=13107, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.56.0.76-2.13.0.63-1.87.1.62-5.04.1.30-3.67.pth, mybk
BLEU = 29.53, 56.0/34.6/23.5/16.7 (BP=1.000, ratio=1.094, hyp_len=12511, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.56.0.76-2.13.0.63-1.87.1.62-5.04.1.30-3.67.pth, bkmy
BLEU = 36.50, 62.1/42.4/30.2/22.4 (BP=1.000, ratio=1.061, hyp_len=12979, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.57.0.84-2.33.0.66-1.94.1.59-4.90.1.31-3.72.pth, mybk
BLEU = 29.82, 57.1/35.0/23.5/16.8 (BP=1.000, ratio=1.077, hyp_len=12309, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.57.0.84-2.33.0.66-1.94.1.59-4.90.1.31-3.72.pth, bkmy
BLEU = 34.72, 60.5/40.5/28.5/20.8 (BP=1.000, ratio=1.097, hyp_len=13423, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.58.0.84-2.31.0.67-1.95.1.58-4.85.1.31-3.70.pth, mybk
BLEU = 30.28, 57.1/35.5/24.2/17.1 (BP=1.000, ratio=1.094, hyp_len=12501, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.58.0.84-2.31.0.67-1.95.1.58-4.85.1.31-3.70.pth, bkmy
BLEU = 36.03, 61.9/41.9/29.7/21.9 (BP=1.000, ratio=1.080, hyp_len=13214, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.59.0.78-2.19.0.62-1.86.1.59-4.92.1.31-3.69.pth, mybk
BLEU = 31.15, 58.5/36.6/24.9/17.7 (BP=1.000, ratio=1.040, hyp_len=11885, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.59.0.78-2.19.0.62-1.86.1.59-4.92.1.31-3.69.pth, bkmy
BLEU = 35.78, 61.3/41.5/29.5/21.8 (BP=1.000, ratio=1.069, hyp_len=13070, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.60.0.74-2.10.0.60-1.82.1.63-5.09.1.31-3.70.pth, mybk
BLEU = 30.84, 57.8/36.1/24.6/17.7 (BP=1.000, ratio=1.060, hyp_len=12117, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.60.0.74-2.10.0.60-1.82.1.63-5.09.1.31-3.70.pth, bkmy
BLEU = 37.07, 62.4/43.0/30.8/22.9 (BP=1.000, ratio=1.072, hyp_len=13106, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.61.0.72-2.05.0.58-1.78.1.59-4.93.1.31-3.69.pth, mybk
BLEU = 27.65, 54.0/32.7/21.7/15.2 (BP=1.000, ratio=1.120, hyp_len=12806, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.61.0.72-2.05.0.58-1.78.1.59-4.93.1.31-3.69.pth, bkmy
BLEU = 37.78, 63.3/43.7/31.4/23.4 (BP=1.000, ratio=1.042, hyp_len=12747, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.62.0.72-2.05.0.60-1.81.1.61-5.01.1.29-3.64.pth, mybk
BLEU = 29.99, 57.1/35.4/23.8/16.8 (BP=1.000, ratio=1.081, hyp_len=12358, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.62.0.72-2.05.0.60-1.81.1.61-5.01.1.29-3.64.pth, bkmy
BLEU = 35.84, 61.4/41.7/29.5/21.8 (BP=1.000, ratio=1.072, hyp_len=13116, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.63.0.71-2.04.0.57-1.77.1.64-5.18.1.33-3.79.pth, mybk
BLEU = 30.16, 57.6/35.9/23.9/16.8 (BP=1.000, ratio=1.066, hyp_len=12190, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.63.0.71-2.04.0.57-1.77.1.64-5.18.1.33-3.79.pth, bkmy
BLEU = 36.36, 61.9/42.1/30.0/22.4 (BP=1.000, ratio=1.062, hyp_len=12995, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.64.0.70-2.01.0.58-1.79.1.65-5.20.1.32-3.75.pth, mybk
BLEU = 30.54, 57.6/36.0/24.2/17.3 (BP=1.000, ratio=1.072, hyp_len=12251, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.64.0.70-2.01.0.58-1.79.1.65-5.20.1.32-3.75.pth, bkmy
BLEU = 37.20, 62.8/43.3/30.7/22.9 (BP=1.000, ratio=1.052, hyp_len=12867, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.65.0.71-2.04.0.58-1.78.1.63-5.10.1.32-3.73.pth, mybk
BLEU = 30.27, 57.8/35.9/23.9/16.9 (BP=1.000, ratio=1.074, hyp_len=12273, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.65.0.71-2.04.0.58-1.78.1.63-5.10.1.32-3.73.pth, bkmy
BLEU = 35.63, 61.4/41.5/29.2/21.7 (BP=1.000, ratio=1.078, hyp_len=13181, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.66.0.68-1.97.0.55-1.74.1.67-5.29.1.33-3.78.pth, mybk
BLEU = 29.32, 56.5/34.7/23.2/16.2 (BP=1.000, ratio=1.085, hyp_len=12403, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.66.0.68-1.97.0.55-1.74.1.67-5.29.1.33-3.78.pth, bkmy
BLEU = 36.38, 61.4/41.9/30.2/22.6 (BP=1.000, ratio=1.059, hyp_len=12957, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.67.0.69-1.99.0.55-1.73.1.64-5.18.1.35-3.85.pth, mybk
BLEU = 28.95, 55.3/34.1/22.8/16.3 (BP=1.000, ratio=1.081, hyp_len=12355, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.67.0.69-1.99.0.55-1.73.1.64-5.18.1.35-3.85.pth, bkmy
BLEU = 35.93, 60.9/41.3/29.7/22.3 (BP=1.000, ratio=1.078, hyp_len=13183, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.68.0.69-1.99.0.55-1.74.1.61-4.99.1.33-3.76.pth, mybk
BLEU = 28.90, 56.2/34.4/22.6/16.0 (BP=1.000, ratio=1.105, hyp_len=12631, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.68.0.69-1.99.0.55-1.74.1.61-4.99.1.33-3.76.pth, bkmy
BLEU = 35.85, 61.0/41.4/29.6/22.1 (BP=1.000, ratio=1.084, hyp_len=13262, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.69.0.68-1.97.0.56-1.75.1.63-5.09.1.31-3.72.pth, mybk
BLEU = 30.84, 58.5/36.5/24.7/17.2 (BP=1.000, ratio=1.060, hyp_len=12121, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.69.0.68-1.97.0.56-1.75.1.63-5.09.1.31-3.72.pth, bkmy
BLEU = 36.57, 62.1/42.3/30.2/22.6 (BP=1.000, ratio=1.074, hyp_len=13141, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.70.0.66-1.94.0.54-1.71.1.67-5.30.1.36-3.89.pth, mybk
BLEU = 28.77, 55.0/34.0/22.8/16.1 (BP=1.000, ratio=1.112, hyp_len=12715, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.70.0.66-1.94.0.54-1.71.1.67-5.30.1.36-3.89.pth, bkmy
BLEU = 34.76, 59.5/40.2/28.7/21.3 (BP=1.000, ratio=1.095, hyp_len=13398, ref_len=12231)
```

Best model for my-bk က epoch 20 မော်ဒယ် ဖြစ်ပြီးတော့၊ Best BLEU Score က : 34.91  
Best model for bk-my က epoch 24 မော်ဒယ် ဖြစ်ပြီးတော့၊ Best BLEU Score က : 42.10  

## Transformer-DSL, 80 epoch

```
Epoch 1 - |param|=8.52e+02 |g_param|=1.87e+05 loss_x2y=4.4367e+00 ppl_x2y=84.49 loss_y2x=4.0895e+00 ppl_y2x=59.71 dual_loss=0.0000e+00
Validation X2Y - loss=3.4974e+00 ppl=33.03 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=3.2626e+00 ppl=26.12 best_loss=inf best_ppl=inf
Epoch 2 - |param|=8.53e+02 |g_param|=1.40e+05 loss_x2y=3.6093e+00 ppl_x2y=36.94 loss_y2x=3.1789e+00 ppl_y2x=24.02 dual_loss=0.0000e+00
Validation X2Y - loss=3.0609e+00 ppl=21.35 best_loss=3.4974e+00 best_ppl=33.03                                          
Validation Y2X - loss=2.7287e+00 ppl=15.31 best_loss=3.2626e+00 best_ppl=26.12
Epoch 3 - |param|=8.54e+02 |g_param|=1.28e+05 loss_x2y=3.3292e+00 ppl_x2y=27.92 loss_y2x=2.8316e+00 ppl_y2x=16.97 dual_loss=0.0000e+00
Validation X2Y - loss=2.6517e+00 ppl=14.18 best_loss=3.0609e+00 best_ppl=21.35                                          
Validation Y2X - loss=2.3618e+00 ppl=10.61 best_loss=2.7287e+00 best_ppl=15.31
Epoch 4 - |param|=8.54e+02 |g_param|=1.37e+05 loss_x2y=2.9138e+00 ppl_x2y=18.43 loss_y2x=2.5617e+00 ppl_y2x=12.96 dual_loss=0.0000e+00
Validation X2Y - loss=2.2720e+00 ppl=9.70 best_loss=2.6517e+00 best_ppl=14.18                                           
Validation Y2X - loss=2.1538e+00 ppl=8.62 best_loss=2.3618e+00 best_ppl=10.61
Epoch 5 - |param|=8.55e+02 |g_param|=1.38e+05 loss_x2y=2.7345e+00 ppl_x2y=15.40 loss_y2x=2.4203e+00 ppl_y2x=11.25 dual_loss=0.0000e+00
Validation X2Y - loss=2.0135e+00 ppl=7.49 best_loss=2.2720e+00 best_ppl=9.70                                            
Validation Y2X - loss=1.8378e+00 ppl=6.28 best_loss=2.1538e+00 best_ppl=8.62
Epoch 6 - |param|=8.56e+02 |g_param|=1.55e+05 loss_x2y=2.6618e+00 ppl_x2y=14.32 loss_y2x=2.3179e+00 ppl_y2x=10.15 dual_loss=0.0000e+00
Validation X2Y - loss=1.9124e+00 ppl=6.77 best_loss=2.0135e+00 best_ppl=7.49                                            
Validation Y2X - loss=1.7065e+00 ppl=5.51 best_loss=1.8378e+00 best_ppl=6.28
Epoch 7 - |param|=8.56e+02 |g_param|=1.51e+05 loss_x2y=2.4328e+00 ppl_x2y=11.39 loss_y2x=2.1130e+00 ppl_y2x=8.27 dual_loss=0.0000e+00
Validation X2Y - loss=1.7219e+00 ppl=5.60 best_loss=1.9124e+00 best_ppl=6.77                                            
Validation Y2X - loss=1.5360e+00 ppl=4.65 best_loss=1.7065e+00 best_ppl=5.51
Epoch 8 - |param|=8.57e+02 |g_param|=1.65e+05 loss_x2y=2.3380e+00 ppl_x2y=10.36 loss_y2x=2.0555e+00 ppl_y2x=7.81 dual_loss=0.0000e+00
Validation X2Y - loss=1.5903e+00 ppl=4.91 best_loss=1.7219e+00 best_ppl=5.60                                            
Validation Y2X - loss=1.4417e+00 ppl=4.23 best_loss=1.5360e+00 best_ppl=4.65
Epoch 9 - |param|=8.57e+02 |g_param|=1.66e+05 loss_x2y=2.2458e+00 ppl_x2y=9.45 loss_y2x=1.9349e+00 ppl_y2x=6.92 dual_loss=0.0000e+00
Validation X2Y - loss=1.5187e+00 ppl=4.57 best_loss=1.5903e+00 best_ppl=4.91                                            
Validation Y2X - loss=1.3587e+00 ppl=3.89 best_loss=1.4417e+00 best_ppl=4.23
Epoch 10 - |param|=8.58e+02 |g_param|=1.74e+05 loss_x2y=2.1170e+00 ppl_x2y=8.31 loss_y2x=1.8292e+00 ppl_y2x=6.23 dual_loss=0.0000e+00
Validation X2Y - loss=1.4374e+00 ppl=4.21 best_loss=1.5187e+00 best_ppl=4.57                                            
Validation Y2X - loss=1.2840e+00 ppl=3.61 best_loss=1.3587e+00 best_ppl=3.89
Epoch 11 - |param|=8.58e+02 |g_param|=1.78e+05 loss_x2y=2.0662e+00 ppl_x2y=7.89 loss_y2x=1.7710e+00 ppl_y2x=5.88 dual_loss=0.0000e+00
Validation X2Y - loss=1.3857e+00 ppl=4.00 best_loss=1.4374e+00 best_ppl=4.21                                            
Validation Y2X - loss=1.1879e+00 ppl=3.28 best_loss=1.2840e+00 best_ppl=3.61
Epoch 12 - |param|=8.59e+02 |g_param|=1.93e+05 loss_x2y=2.0219e+00 ppl_x2y=7.55 loss_y2x=1.6882e+00 ppl_y2x=5.41 dual_loss=0.0000e+00
Validation X2Y - loss=1.3968e+00 ppl=4.04 best_loss=1.3857e+00 best_ppl=4.00                                            
Validation Y2X - loss=1.2313e+00 ppl=3.43 best_loss=1.1879e+00 best_ppl=3.28
Epoch 13 - |param|=8.59e+02 |g_param|=1.87e+05 loss_x2y=1.9371e+00 ppl_x2y=6.94 loss_y2x=1.6858e+00 ppl_y2x=5.40 dual_loss=0.0000e+00
Validation X2Y - loss=1.3611e+00 ppl=3.90 best_loss=1.3857e+00 best_ppl=4.00                                            
Validation Y2X - loss=1.1580e+00 ppl=3.18 best_loss=1.1879e+00 best_ppl=3.28
Epoch 14 - |param|=8.60e+02 |g_param|=1.98e+05 loss_x2y=1.9014e+00 ppl_x2y=6.70 loss_y2x=1.6680e+00 ppl_y2x=5.30 dual_loss=0.0000e+00
Validation X2Y - loss=1.3546e+00 ppl=3.88 best_loss=1.3611e+00 best_ppl=3.90                                            
Validation Y2X - loss=1.1887e+00 ppl=3.28 best_loss=1.1580e+00 best_ppl=3.18
Epoch 15 - |param|=8.61e+02 |g_param|=2.04e+05 loss_x2y=1.8132e+00 ppl_x2y=6.13 loss_y2x=1.6009e+00 ppl_y2x=4.96 dual_loss=0.0000e+00
Validation X2Y - loss=1.3226e+00 ppl=3.75 best_loss=1.3546e+00 best_ppl=3.88                                            
Validation Y2X - loss=1.1522e+00 ppl=3.16 best_loss=1.1580e+00 best_ppl=3.18
Epoch 16 - |param|=8.61e+02 |g_param|=2.03e+05 loss_x2y=1.7282e+00 ppl_x2y=5.63 loss_y2x=1.4664e+00 ppl_y2x=4.33 dual_loss=0.0000e+00
Validation X2Y - loss=1.2922e+00 ppl=3.64 best_loss=1.3226e+00 best_ppl=3.75                                            
Validation Y2X - loss=1.1093e+00 ppl=3.03 best_loss=1.1522e+00 best_ppl=3.16
Epoch 17 - |param|=8.62e+02 |g_param|=1.98e+05 loss_x2y=1.6399e+00 ppl_x2y=5.15 loss_y2x=1.3900e+00 ppl_y2x=4.01 dual_loss=0.0000e+00
Validation X2Y - loss=1.2915e+00 ppl=3.64 best_loss=1.2922e+00 best_ppl=3.64                                            
Validation Y2X - loss=1.1088e+00 ppl=3.03 best_loss=1.1093e+00 best_ppl=3.03
Epoch 18 - |param|=8.62e+02 |g_param|=2.10e+05 loss_x2y=1.5861e+00 ppl_x2y=4.88 loss_y2x=1.3402e+00 ppl_y2x=3.82 dual_loss=0.0000e+00
Validation X2Y - loss=1.3058e+00 ppl=3.69 best_loss=1.2915e+00 best_ppl=3.64                                            
Validation Y2X - loss=1.1041e+00 ppl=3.02 best_loss=1.1088e+00 best_ppl=3.03
Epoch 19 - |param|=8.63e+02 |g_param|=2.11e+05 loss_x2y=1.6544e+00 ppl_x2y=5.23 loss_y2x=1.3601e+00 ppl_y2x=3.90 dual_loss=0.0000e+00
Validation X2Y - loss=1.2800e+00 ppl=3.60 best_loss=1.2915e+00 best_ppl=3.64                                            
Validation Y2X - loss=1.0724e+00 ppl=2.92 best_loss=1.1041e+00 best_ppl=3.02
Epoch 20 - |param|=8.63e+02 |g_param|=2.22e+05 loss_x2y=1.5007e+00 ppl_x2y=4.49 loss_y2x=1.2699e+00 ppl_y2x=3.56 dual_loss=0.0000e+00
Validation X2Y - loss=1.3041e+00 ppl=3.68 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.0801e+00 ppl=2.95 best_loss=1.0724e+00 best_ppl=2.92
Epoch 21 - |param|=8.64e+02 |g_param|=2.13e+05 loss_x2y=1.5050e+00 ppl_x2y=4.50 loss_y2x=1.2576e+00 ppl_y2x=3.52 dual_loss=5.5081e-01
Validation X2Y - loss=1.2870e+00 ppl=3.62 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.0635e+00 ppl=2.90 best_loss=1.0724e+00 best_ppl=2.92
Epoch 22 - |param|=8.64e+02 |g_param|=2.30e+05 loss_x2y=1.4409e+00 ppl_x2y=4.22 loss_y2x=1.2475e+00 ppl_y2x=3.48 dual_loss=5.5559e-01
Validation X2Y - loss=1.3007e+00 ppl=3.67 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.0709e+00 ppl=2.92 best_loss=1.0635e+00 best_ppl=2.90
Epoch 23 - |param|=8.65e+02 |g_param|=2.19e+05 loss_x2y=1.3628e+00 ppl_x2y=3.91 loss_y2x=1.1627e+00 ppl_y2x=3.20 dual_loss=4.6338e-01
Validation X2Y - loss=1.2936e+00 ppl=3.65 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.0653e+00 ppl=2.90 best_loss=1.0635e+00 best_ppl=2.90
Epoch 24 - |param|=8.65e+02 |g_param|=2.33e+05 loss_x2y=1.3869e+00 ppl_x2y=4.00 loss_y2x=1.1712e+00 ppl_y2x=3.23 dual_loss=5.0948e-01
Validation X2Y - loss=1.2996e+00 ppl=3.67 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.0974e+00 ppl=3.00 best_loss=1.0635e+00 best_ppl=2.90
Epoch 25 - |param|=8.66e+02 |g_param|=2.29e+05 loss_x2y=1.3172e+00 ppl_x2y=3.73 loss_y2x=1.1212e+00 ppl_y2x=3.07 dual_loss=5.0070e-01
Validation X2Y - loss=1.3074e+00 ppl=3.70 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1106e+00 ppl=3.04 best_loss=1.0635e+00 best_ppl=2.90
Epoch 26 - |param|=8.66e+02 |g_param|=2.41e+05 loss_x2y=1.3110e+00 ppl_x2y=3.71 loss_y2x=1.0972e+00 ppl_y2x=3.00 dual_loss=4.9304e-01
Validation X2Y - loss=1.3418e+00 ppl=3.83 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.0994e+00 ppl=3.00 best_loss=1.0635e+00 best_ppl=2.90
Epoch 27 - |param|=8.67e+02 |g_param|=2.26e+05 loss_x2y=1.2772e+00 ppl_x2y=3.59 loss_y2x=1.0548e+00 ppl_y2x=2.87 dual_loss=5.0581e-01
Validation X2Y - loss=1.3372e+00 ppl=3.81 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.0826e+00 ppl=2.95 best_loss=1.0635e+00 best_ppl=2.90
Epoch 28 - |param|=8.67e+02 |g_param|=2.29e+05 loss_x2y=1.2410e+00 ppl_x2y=3.46 loss_y2x=1.0423e+00 ppl_y2x=2.84 dual_loss=5.2219e-01
Validation X2Y - loss=1.3516e+00 ppl=3.86 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1171e+00 ppl=3.06 best_loss=1.0635e+00 best_ppl=2.90
Epoch 29 - |param|=8.68e+02 |g_param|=2.39e+05 loss_x2y=1.2844e+00 ppl_x2y=3.61 loss_y2x=1.0733e+00 ppl_y2x=2.92 dual_loss=6.1038e-01
Validation X2Y - loss=1.3379e+00 ppl=3.81 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.0957e+00 ppl=2.99 best_loss=1.0635e+00 best_ppl=2.90
Epoch 30 - |param|=8.69e+02 |g_param|=2.34e+05 loss_x2y=1.1976e+00 ppl_x2y=3.31 loss_y2x=1.0018e+00 ppl_y2x=2.72 dual_loss=5.3377e-01
Validation X2Y - loss=1.3099e+00 ppl=3.71 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1148e+00 ppl=3.05 best_loss=1.0635e+00 best_ppl=2.90
Epoch 31 - |param|=8.69e+02 |g_param|=2.37e+05 loss_x2y=1.1895e+00 ppl_x2y=3.29 loss_y2x=9.7986e-01 ppl_y2x=2.66 dual_loss=5.2873e-01
Validation X2Y - loss=1.3373e+00 ppl=3.81 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1345e+00 ppl=3.11 best_loss=1.0635e+00 best_ppl=2.90
Epoch 32 - |param|=8.70e+02 |g_param|=2.49e+05 loss_x2y=1.1223e+00 ppl_x2y=3.07 loss_y2x=9.3811e-01 ppl_y2x=2.56 dual_loss=5.3020e-01
Validation X2Y - loss=1.3620e+00 ppl=3.90 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1134e+00 ppl=3.04 best_loss=1.0635e+00 best_ppl=2.90
Epoch 33 - |param|=8.70e+02 |g_param|=2.35e+05 loss_x2y=1.1215e+00 ppl_x2y=3.07 loss_y2x=9.2924e-01 ppl_y2x=2.53 dual_loss=5.4856e-01
Validation X2Y - loss=1.3808e+00 ppl=3.98 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1634e+00 ppl=3.20 best_loss=1.0635e+00 best_ppl=2.90
Epoch 34 - |param|=8.71e+02 |g_param|=4.62e+05 loss_x2y=1.1268e+00 ppl_x2y=3.09 loss_y2x=9.4512e-01 ppl_y2x=2.57 dual_loss=5.8220e-01
Validation X2Y - loss=1.3975e+00 ppl=4.04 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1418e+00 ppl=3.13 best_loss=1.0635e+00 best_ppl=2.90
Epoch 35 - |param|=8.71e+02 |g_param|=4.93e+05 loss_x2y=1.0997e+00 ppl_x2y=3.00 loss_y2x=9.2108e-01 ppl_y2x=2.51 dual_loss=6.1227e-01
Validation X2Y - loss=1.4094e+00 ppl=4.09 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1672e+00 ppl=3.21 best_loss=1.0635e+00 best_ppl=2.90
Epoch 36 - |param|=8.72e+02 |g_param|=5.18e+05 loss_x2y=1.0705e+00 ppl_x2y=2.92 loss_y2x=9.1210e-01 ppl_y2x=2.49 dual_loss=6.5133e-01
Validation X2Y - loss=1.3928e+00 ppl=4.03 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1276e+00 ppl=3.09 best_loss=1.0635e+00 best_ppl=2.90
Epoch 37 - |param|=8.72e+02 |g_param|=5.00e+05 loss_x2y=1.0652e+00 ppl_x2y=2.90 loss_y2x=9.1351e-01 ppl_y2x=2.49 dual_loss=6.5632e-01
Validation X2Y - loss=1.4003e+00 ppl=4.06 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1699e+00 ppl=3.22 best_loss=1.0635e+00 best_ppl=2.90
Epoch 38 - |param|=8.73e+02 |g_param|=4.95e+05 loss_x2y=1.0021e+00 ppl_x2y=2.72 loss_y2x=8.3177e-01 ppl_y2x=2.30 dual_loss=6.0465e-01
Validation X2Y - loss=1.3988e+00 ppl=4.05 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1820e+00 ppl=3.26 best_loss=1.0635e+00 best_ppl=2.90
Epoch 39 - |param|=8.73e+02 |g_param|=5.10e+05 loss_x2y=1.0321e+00 ppl_x2y=2.81 loss_y2x=8.4770e-01 ppl_y2x=2.33 dual_loss=6.3214e-01
Validation X2Y - loss=1.4358e+00 ppl=4.20 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1777e+00 ppl=3.25 best_loss=1.0635e+00 best_ppl=2.90
Epoch 40 - |param|=8.74e+02 |g_param|=5.06e+05 loss_x2y=1.0103e+00 ppl_x2y=2.75 loss_y2x=8.0901e-01 ppl_y2x=2.25 dual_loss=6.6406e-01
Validation X2Y - loss=1.4084e+00 ppl=4.09 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1798e+00 ppl=3.25 best_loss=1.0635e+00 best_ppl=2.90
Epoch 41 - |param|=8.74e+02 |g_param|=5.20e+05 loss_x2y=1.0002e+00 ppl_x2y=2.72 loss_y2x=8.5248e-01 ppl_y2x=2.35 dual_loss=7.2480e-01
Validation X2Y - loss=1.4203e+00 ppl=4.14 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.2391e+00 ppl=3.45 best_loss=1.0635e+00 best_ppl=2.90
Epoch 42 - |param|=8.75e+02 |g_param|=5.43e+05 loss_x2y=1.0381e+00 ppl_x2y=2.82 loss_y2x=8.5592e-01 ppl_y2x=2.35 dual_loss=7.4950e-01
Validation X2Y - loss=1.4248e+00 ppl=4.16 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.2169e+00 ppl=3.38 best_loss=1.0635e+00 best_ppl=2.90
Epoch 43 - |param|=8.75e+02 |g_param|=5.02e+05 loss_x2y=9.6752e-01 ppl_x2y=2.63 loss_y2x=7.9290e-01 ppl_y2x=2.21 dual_loss=7.0407e-01
Validation X2Y - loss=1.4581e+00 ppl=4.30 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.2412e+00 ppl=3.46 best_loss=1.0635e+00 best_ppl=2.90
Epoch 44 - |param|=8.76e+02 |g_param|=5.13e+05 loss_x2y=9.1570e-01 ppl_x2y=2.50 loss_y2x=7.4764e-01 ppl_y2x=2.11 dual_loss=6.7279e-01
Validation X2Y - loss=1.4200e+00 ppl=4.14 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.2196e+00 ppl=3.39 best_loss=1.0635e+00 best_ppl=2.90
Epoch 45 - |param|=8.76e+02 |g_param|=5.10e+05 loss_x2y=9.2986e-01 ppl_x2y=2.53 loss_y2x=7.6647e-01 ppl_y2x=2.15 dual_loss=7.1913e-01
Validation X2Y - loss=1.4462e+00 ppl=4.25 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.2024e+00 ppl=3.33 best_loss=1.0635e+00 best_ppl=2.90
Epoch 46 - |param|=8.77e+02 |g_param|=5.09e+05 loss_x2y=9.4745e-01 ppl_x2y=2.58 loss_y2x=7.5996e-01 ppl_y2x=2.14 dual_loss=7.9768e-01
Validation X2Y - loss=1.4476e+00 ppl=4.25 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.2710e+00 ppl=3.56 best_loss=1.0635e+00 best_ppl=2.90
Epoch 47 - |param|=8.77e+02 |g_param|=4.86e+05 loss_x2y=8.5373e-01 ppl_x2y=2.35 loss_y2x=7.0369e-01 ppl_y2x=2.02 dual_loss=6.6579e-01
Validation X2Y - loss=1.4441e+00 ppl=4.24 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.2686e+00 ppl=3.56 best_loss=1.0635e+00 best_ppl=2.90
Epoch 48 - |param|=8.78e+02 |g_param|=5.17e+05 loss_x2y=8.5065e-01 ppl_x2y=2.34 loss_y2x=6.9874e-01 ppl_y2x=2.01 dual_loss=7.3088e-01
Validation X2Y - loss=1.4687e+00 ppl=4.34 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.2514e+00 ppl=3.50 best_loss=1.0635e+00 best_ppl=2.90
Epoch 49 - |param|=8.78e+02 |g_param|=5.01e+05 loss_x2y=8.5671e-01 ppl_x2y=2.36 loss_y2x=6.9991e-01 ppl_y2x=2.01 dual_loss=7.4616e-01
Validation X2Y - loss=1.4751e+00 ppl=4.37 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.3079e+00 ppl=3.70 best_loss=1.0635e+00 best_ppl=2.90
Epoch 50 - |param|=8.78e+02 |g_param|=5.23e+05 loss_x2y=8.5824e-01 ppl_x2y=2.36 loss_y2x=6.9955e-01 ppl_y2x=2.01 dual_loss=7.6380e-01
Validation X2Y - loss=1.4804e+00 ppl=4.39 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.2824e+00 ppl=3.61 best_loss=1.0635e+00 best_ppl=2.90
Epoch 51 - |param|=8.79e+02 |g_param|=4.91e+05 loss_x2y=8.0698e-01 ppl_x2y=2.24 loss_y2x=6.5325e-01 ppl_y2x=1.92 dual_loss=7.2656e-01
Validation X2Y - loss=1.4798e+00 ppl=4.39 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.2828e+00 ppl=3.61 best_loss=1.0635e+00 best_ppl=2.90
Epoch 52 - |param|=8.79e+02 |g_param|=5.15e+05 loss_x2y=8.0851e-01 ppl_x2y=2.24 loss_y2x=6.5086e-01 ppl_y2x=1.92 dual_loss=7.4263e-01
Validation X2Y - loss=1.4939e+00 ppl=4.45 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.2786e+00 ppl=3.59 best_loss=1.0635e+00 best_ppl=2.90
Epoch 53 - |param|=8.80e+02 |g_param|=5.00e+05 loss_x2y=7.9588e-01 ppl_x2y=2.22 loss_y2x=6.5463e-01 ppl_y2x=1.92 dual_loss=7.9690e-01
Validation X2Y - loss=1.4905e+00 ppl=4.44 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.2507e+00 ppl=3.49 best_loss=1.0635e+00 best_ppl=2.90
Epoch 54 - |param|=8.80e+02 |g_param|=5.20e+05 loss_x2y=8.1157e-01 ppl_x2y=2.25 loss_y2x=6.9370e-01 ppl_y2x=2.00 dual_loss=9.2756e-01
Validation X2Y - loss=1.5417e+00 ppl=4.67 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.2732e+00 ppl=3.57 best_loss=1.0635e+00 best_ppl=2.90
Epoch 55 - |param|=8.81e+02 |g_param|=5.07e+05 loss_x2y=8.3904e-01 ppl_x2y=2.31 loss_y2x=6.7629e-01 ppl_y2x=1.97 dual_loss=1.0107e+00
Validation X2Y - loss=1.5453e+00 ppl=4.69 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.2632e+00 ppl=3.54 best_loss=1.0635e+00 best_ppl=2.90
Epoch 56 - |param|=8.81e+02 |g_param|=5.21e+05 loss_x2y=7.7505e-01 ppl_x2y=2.17 loss_y2x=6.3455e-01 ppl_y2x=1.89 dual_loss=8.3198e-01
Validation X2Y - loss=1.5559e+00 ppl=4.74 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.3094e+00 ppl=3.70 best_loss=1.0635e+00 best_ppl=2.90
Epoch 57 - |param|=8.82e+02 |g_param|=4.99e+05 loss_x2y=7.5305e-01 ppl_x2y=2.12 loss_y2x=6.1326e-01 ppl_y2x=1.85 dual_loss=7.8532e-01
Validation X2Y - loss=1.5473e+00 ppl=4.70 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.2997e+00 ppl=3.67 best_loss=1.0635e+00 best_ppl=2.90
Epoch 58 - |param|=8.82e+02 |g_param|=5.34e+05 loss_x2y=7.7217e-01 ppl_x2y=2.16 loss_y2x=6.6567e-01 ppl_y2x=1.95 dual_loss=1.0544e+00
Validation X2Y - loss=1.5565e+00 ppl=4.74 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.2919e+00 ppl=3.64 best_loss=1.0635e+00 best_ppl=2.90
Epoch 59 - |param|=8.83e+02 |g_param|=4.95e+05 loss_x2y=7.5011e-01 ppl_x2y=2.12 loss_y2x=6.0699e-01 ppl_y2x=1.83 dual_loss=8.5040e-01
Validation X2Y - loss=1.5553e+00 ppl=4.74 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.3092e+00 ppl=3.70 best_loss=1.0635e+00 best_ppl=2.90
Epoch 60 - |param|=8.83e+02 |g_param|=5.23e+05 loss_x2y=7.4686e-01 ppl_x2y=2.11 loss_y2x=6.0288e-01 ppl_y2x=1.83 dual_loss=8.9640e-01
Validation X2Y - loss=1.5716e+00 ppl=4.81 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.3448e+00 ppl=3.84 best_loss=1.0635e+00 best_ppl=2.90
Epoch 61 - |param|=8.84e+02 |g_param|=5.12e+05 loss_x2y=7.4528e-01 ppl_x2y=2.11 loss_y2x=6.0705e-01 ppl_y2x=1.84 dual_loss=8.7858e-01
Validation X2Y - loss=1.6087e+00 ppl=5.00 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.3379e+00 ppl=3.81 best_loss=1.0635e+00 best_ppl=2.90
Epoch 62 - |param|=8.84e+02 |g_param|=5.29e+05 loss_x2y=7.6549e-01 ppl_x2y=2.15 loss_y2x=6.2292e-01 ppl_y2x=1.86 dual_loss=9.6231e-01
Validation X2Y - loss=1.5783e+00 ppl=4.85 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.3660e+00 ppl=3.92 best_loss=1.0635e+00 best_ppl=2.90
Epoch 63 - |param|=8.84e+02 |g_param|=4.94e+05 loss_x2y=6.8714e-01 ppl_x2y=1.99 loss_y2x=5.6721e-01 ppl_y2x=1.76 dual_loss=8.9207e-01
Validation X2Y - loss=1.5584e+00 ppl=4.75 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.3556e+00 ppl=3.88 best_loss=1.0635e+00 best_ppl=2.90
Epoch 64 - |param|=8.85e+02 |g_param|=5.08e+05 loss_x2y=6.9981e-01 ppl_x2y=2.01 loss_y2x=5.7976e-01 ppl_y2x=1.79 dual_loss=8.7457e-01
Validation X2Y - loss=1.6045e+00 ppl=4.98 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.3629e+00 ppl=3.91 best_loss=1.0635e+00 best_ppl=2.90
Epoch 65 - |param|=8.85e+02 |g_param|=5.03e+05 loss_x2y=7.0554e-01 ppl_x2y=2.02 loss_y2x=5.6999e-01 ppl_y2x=1.77 dual_loss=8.6011e-01
Validation X2Y - loss=1.6214e+00 ppl=5.06 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.3842e+00 ppl=3.99 best_loss=1.0635e+00 best_ppl=2.90
Epoch 66 - |param|=8.86e+02 |g_param|=8.53e+05 loss_x2y=6.9892e-01 ppl_x2y=2.01 loss_y2x=5.6736e-01 ppl_y2x=1.76 dual_loss=9.2284e-01
Validation X2Y - loss=1.6212e+00 ppl=5.06 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.4028e+00 ppl=4.07 best_loss=1.0635e+00 best_ppl=2.90
Epoch 67 - |param|=8.86e+02 |g_param|=7.81e+05 loss_x2y=6.9740e-01 ppl_x2y=2.01 loss_y2x=5.5617e-01 ppl_y2x=1.74 dual_loss=9.1467e-01
Validation X2Y - loss=1.6080e+00 ppl=4.99 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.3925e+00 ppl=4.02 best_loss=1.0635e+00 best_ppl=2.90
Epoch 68 - |param|=8.87e+02 |g_param|=8.51e+05 loss_x2y=7.5719e-01 ppl_x2y=2.13 loss_y2x=6.0788e-01 ppl_y2x=1.84 dual_loss=1.2235e+00
Validation X2Y - loss=1.5867e+00 ppl=4.89 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.3841e+00 ppl=3.99 best_loss=1.0635e+00 best_ppl=2.90
Epoch 69 - |param|=8.87e+02 |g_param|=7.81e+05 loss_x2y=6.9358e-01 ppl_x2y=2.00 loss_y2x=5.6003e-01 ppl_y2x=1.75 dual_loss=9.2419e-01
Validation X2Y - loss=1.6520e+00 ppl=5.22 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.3997e+00 ppl=4.05 best_loss=1.0635e+00 best_ppl=2.90
Epoch 70 - |param|=8.88e+02 |g_param|=8.32e+05 loss_x2y=6.8283e-01 ppl_x2y=1.98 loss_y2x=5.3503e-01 ppl_y2x=1.71 dual_loss=9.7266e-01
Validation X2Y - loss=1.6278e+00 ppl=5.09 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.3610e+00 ppl=3.90 best_loss=1.0635e+00 best_ppl=2.90
Epoch 71 - |param|=8.88e+02 |g_param|=7.65e+05 loss_x2y=6.6502e-01 ppl_x2y=1.94 loss_y2x=5.2952e-01 ppl_y2x=1.70 dual_loss=9.6220e-01
Validation X2Y - loss=1.6081e+00 ppl=4.99 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.3902e+00 ppl=4.02 best_loss=1.0635e+00 best_ppl=2.90
Epoch 72 - |param|=8.88e+02 |g_param|=8.25e+05 loss_x2y=6.6469e-01 ppl_x2y=1.94 loss_y2x=5.4342e-01 ppl_y2x=1.72 dual_loss=1.0804e+00
Validation X2Y - loss=1.6214e+00 ppl=5.06 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.3483e+00 ppl=3.85 best_loss=1.0635e+00 best_ppl=2.90
Epoch 73 - |param|=8.89e+02 |g_param|=7.94e+05 loss_x2y=6.6384e-01 ppl_x2y=1.94 loss_y2x=5.2598e-01 ppl_y2x=1.69 dual_loss=1.0385e+00
Validation X2Y - loss=1.6074e+00 ppl=4.99 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.3894e+00 ppl=4.01 best_loss=1.0635e+00 best_ppl=2.90
Epoch 74 - |param|=8.89e+02 |g_param|=8.08e+05 loss_x2y=6.4262e-01 ppl_x2y=1.90 loss_y2x=5.2526e-01 ppl_y2x=1.69 dual_loss=1.0487e+00
Validation X2Y - loss=1.6145e+00 ppl=5.03 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.4235e+00 ppl=4.15 best_loss=1.0635e+00 best_ppl=2.90
Epoch 75 - |param|=8.90e+02 |g_param|=7.64e+05 loss_x2y=6.2618e-01 ppl_x2y=1.87 loss_y2x=4.9323e-01 ppl_y2x=1.64 dual_loss=9.1868e-01
Validation X2Y - loss=1.6392e+00 ppl=5.15 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.4319e+00 ppl=4.19 best_loss=1.0635e+00 best_ppl=2.90
Epoch 76 - |param|=8.90e+02 |g_param|=8.34e+05 loss_x2y=6.5132e-01 ppl_x2y=1.92 loss_y2x=5.3146e-01 ppl_y2x=1.70 dual_loss=1.0378e+00
Validation X2Y - loss=1.6418e+00 ppl=5.16 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.4506e+00 ppl=4.27 best_loss=1.0635e+00 best_ppl=2.90
Epoch 77 - |param|=8.91e+02 |g_param|=7.87e+05 loss_x2y=6.3960e-01 ppl_x2y=1.90 loss_y2x=5.1473e-01 ppl_y2x=1.67 dual_loss=1.0330e+00
Validation X2Y - loss=1.6588e+00 ppl=5.25 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.4605e+00 ppl=4.31 best_loss=1.0635e+00 best_ppl=2.90
Epoch 78 - |param|=8.91e+02 |g_param|=8.19e+05 loss_x2y=6.1629e-01 ppl_x2y=1.85 loss_y2x=4.9937e-01 ppl_y2x=1.65 dual_loss=9.9018e-01
Validation X2Y - loss=1.6651e+00 ppl=5.29 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.4201e+00 ppl=4.14 best_loss=1.0635e+00 best_ppl=2.90
Epoch 79 - |param|=8.91e+02 |g_param|=7.92e+05 loss_x2y=6.1645e-01 ppl_x2y=1.85 loss_y2x=4.9646e-01 ppl_y2x=1.64 dual_loss=1.0503e+00
Validation X2Y - loss=1.6584e+00 ppl=5.25 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.4145e+00 ppl=4.11 best_loss=1.0635e+00 best_ppl=2.90
Epoch 80 - |param|=8.92e+02 |g_param|=8.17e+05 loss_x2y=6.2427e-01 ppl_x2y=1.87 loss_y2x=5.0667e-01 ppl_y2x=1.66 dual_loss=1.1483e+00
Validation X2Y - loss=1.6357e+00 ppl=5.13 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.4290e+00 ppl=4.17 best_loss=1.0635e+00 best_ppl=2.90

real	25m53.518s
user	25m29.035s
sys	0m22.546s
```

testing/evaluation...  

```
/home/ye/exp/simple-nmt/model/dsl/transformer/mybk-80epoch
Evaluation result for the model: dsl-model-mybk.01.4.44-84.49.4.09-59.71.3.50-33.03.3.26-26.12.pth, mybk
BLEU = 4.04, 19.1/4.7/2.5/1.2 (BP=1.000, ratio=1.118, hyp_len=12776, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.44-84.49.4.09-59.71.3.50-33.03.3.26-26.12.pth, bkmy
BLEU = 4.23, 25.6/7.4/2.5/0.7 (BP=1.000, ratio=1.086, hyp_len=13286, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.02.3.61-36.94.3.18-24.02.3.06-21.35.2.73-15.31.pth, mybk
BLEU = 2.41, 11.8/3.5/1.3/0.6 (BP=1.000, ratio=2.071, hyp_len=23670, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.3.61-36.94.3.18-24.02.3.06-21.35.2.73-15.31.pth, bkmy
BLEU = 5.02, 25.8/8.5/3.0/1.0 (BP=1.000, ratio=1.149, hyp_len=14050, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.3.33-27.92.2.83-16.97.2.65-14.18.2.36-10.61.pth, mybk
BLEU = 3.40, 15.0/5.0/2.1/0.9 (BP=1.000, ratio=2.101, hyp_len=24020, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.3.33-27.92.2.83-16.97.2.65-14.18.2.36-10.61.pth, bkmy
BLEU = 9.17, 35.4/13.7/5.7/2.5 (BP=1.000, ratio=1.035, hyp_len=12653, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.2.91-18.43.2.56-12.96.2.27-9.70.2.15-8.62.pth, mybk
BLEU = 6.95, 23.7/9.6/4.6/2.2 (BP=1.000, ratio=1.530, hyp_len=17493, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.2.91-18.43.2.56-12.96.2.27-9.70.2.15-8.62.pth, bkmy
BLEU = 9.19, 31.3/13.9/6.2/2.6 (BP=1.000, ratio=1.354, hyp_len=16560, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.2.73-15.40.2.42-11.25.2.01-7.49.1.84-6.28.pth, mybk
BLEU = 10.69, 31.3/14.2/7.4/4.0 (BP=1.000, ratio=1.328, hyp_len=15178, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.2.73-15.40.2.42-11.25.2.01-7.49.1.84-6.28.pth, bkmy
BLEU = 16.98, 45.2/22.9/12.2/6.6 (BP=1.000, ratio=1.038, hyp_len=12695, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.2.66-14.32.2.32-10.15.1.91-6.77.1.71-5.51.pth, mybk
BLEU = 16.17, 41.9/20.9/11.6/6.8 (BP=1.000, ratio=1.152, hyp_len=13175, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.2.66-14.32.2.32-10.15.1.91-6.77.1.71-5.51.pth, bkmy
BLEU = 19.61, 47.9/25.3/14.4/8.5 (BP=1.000, ratio=1.032, hyp_len=12627, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.2.43-11.39.2.11-8.27.1.72-5.60.1.54-4.65.pth, mybk
BLEU = 15.95, 39.2/20.3/11.7/7.0 (BP=1.000, ratio=1.242, hyp_len=14199, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.2.43-11.39.2.11-8.27.1.72-5.60.1.54-4.65.pth, bkmy
BLEU = 25.67, 54.8/32.4/19.7/12.4 (BP=1.000, ratio=1.009, hyp_len=12337, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.2.34-10.36.2.06-7.81.1.59-4.91.1.44-4.23.pth, mybk
BLEU = 21.92, 49.2/27.3/16.7/10.3 (BP=1.000, ratio=1.054, hyp_len=12048, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.2.34-10.36.2.06-7.81.1.59-4.91.1.44-4.23.pth, bkmy
BLEU = 28.43, 55.3/34.3/22.5/15.3 (BP=1.000, ratio=1.056, hyp_len=12910, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.2.25-9.45.1.93-6.92.1.52-4.57.1.36-3.89.pth, mybk
BLEU = 23.76, 50.6/28.7/18.1/12.1 (BP=1.000, ratio=1.088, hyp_len=12436, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.2.25-9.45.1.93-6.92.1.52-4.57.1.36-3.89.pth, bkmy
BLEU = 30.77, 58.0/36.9/24.5/17.1 (BP=1.000, ratio=1.034, hyp_len=12644, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.2.12-8.31.1.83-6.23.1.44-4.21.1.28-3.61.pth, mybk
BLEU = 24.03, 49.8/29.2/18.6/12.3 (BP=1.000, ratio=1.144, hyp_len=13077, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.2.12-8.31.1.83-6.23.1.44-4.21.1.28-3.61.pth, bkmy
BLEU = 33.58, 60.5/39.6/27.1/19.6 (BP=1.000, ratio=1.006, hyp_len=12303, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.2.07-7.89.1.77-5.88.1.39-4.00.1.19-3.28.pth, mybk
BLEU = 28.86, 57.1/34.4/22.6/15.6 (BP=1.000, ratio=1.032, hyp_len=11800, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.2.07-7.89.1.77-5.88.1.39-4.00.1.19-3.28.pth, bkmy
BLEU = 35.91, 63.2/42.5/29.4/21.1 (BP=1.000, ratio=1.025, hyp_len=12538, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.2.02-7.55.1.69-5.41.1.40-4.04.1.23-3.43.pth, mybk
BLEU = 27.37, 54.1/32.6/21.5/14.8 (BP=1.000, ratio=1.092, hyp_len=12480, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.2.02-7.55.1.69-5.41.1.40-4.04.1.23-3.43.pth, bkmy
BLEU = 35.49, 62.7/42.0/29.4/21.6 (BP=0.987, ratio=0.987, hyp_len=12069, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.1.94-6.94.1.69-5.40.1.36-3.90.1.16-3.18.pth, mybk
BLEU = 29.07, 56.2/34.5/22.9/16.1 (BP=1.000, ratio=1.038, hyp_len=11869, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.1.94-6.94.1.69-5.40.1.36-3.90.1.16-3.18.pth, bkmy
BLEU = 36.50, 63.6/42.9/30.0/21.7 (BP=1.000, ratio=1.030, hyp_len=12596, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.1.90-6.70.1.67-5.30.1.35-3.88.1.19-3.28.pth, mybk
BLEU = 31.72, 59.2/37.4/25.4/18.0 (BP=1.000, ratio=1.040, hyp_len=11894, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.1.90-6.70.1.67-5.30.1.35-3.88.1.19-3.28.pth, bkmy
BLEU = 34.55, 60.2/41.0/28.4/20.3 (BP=1.000, ratio=1.085, hyp_len=13266, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.1.81-6.13.1.60-4.96.1.32-3.75.1.15-3.16.pth, mybk
BLEU = 31.23, 59.2/37.3/24.9/17.4 (BP=1.000, ratio=1.065, hyp_len=12178, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.1.81-6.13.1.60-4.96.1.32-3.75.1.15-3.16.pth, bkmy
BLEU = 37.57, 64.2/44.1/31.0/22.7 (BP=1.000, ratio=1.041, hyp_len=12730, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.1.73-5.63.1.47-4.33.1.29-3.64.1.11-3.03.pth, mybk
BLEU = 30.89, 58.5/36.9/24.7/17.1 (BP=1.000, ratio=1.070, hyp_len=12233, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.1.73-5.63.1.47-4.33.1.29-3.64.1.11-3.03.pth, bkmy
BLEU = 38.80, 64.8/45.1/32.3/24.0 (BP=1.000, ratio=1.040, hyp_len=12723, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.1.64-5.15.1.39-4.01.1.29-3.64.1.11-3.03.pth, mybk
BLEU = 30.99, 58.2/36.7/24.8/17.4 (BP=1.000, ratio=1.068, hyp_len=12204, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.1.64-5.15.1.39-4.01.1.29-3.64.1.11-3.03.pth, bkmy
BLEU = 39.32, 65.3/45.5/32.8/24.5 (BP=1.000, ratio=1.050, hyp_len=12844, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.1.59-4.88.1.34-3.82.1.31-3.69.1.10-3.02.pth, mybk
BLEU = 31.73, 59.0/37.3/25.4/18.1 (BP=1.000, ratio=1.054, hyp_len=12047, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.1.59-4.88.1.34-3.82.1.31-3.69.1.10-3.02.pth, bkmy
BLEU = 37.94, 64.7/44.2/31.4/23.1 (BP=1.000, ratio=1.039, hyp_len=12704, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.1.65-5.23.1.36-3.90.1.28-3.60.1.07-2.92.pth, mybk
BLEU = 32.13, 59.4/37.8/25.7/18.5 (BP=1.000, ratio=1.077, hyp_len=12309, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.1.65-5.23.1.36-3.90.1.28-3.60.1.07-2.92.pth, bkmy
BLEU = 38.88, 64.9/45.2/32.4/24.1 (BP=1.000, ratio=1.056, hyp_len=12914, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.1.50-4.49.1.27-3.56.1.30-3.68.1.08-2.95.pth, mybk
BLEU = 31.39, 58.2/36.9/25.2/18.0 (BP=1.000, ratio=1.076, hyp_len=12299, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.1.50-4.49.1.27-3.56.1.30-3.68.1.08-2.95.pth, bkmy
BLEU = 39.25, 65.3/45.5/32.7/24.4 (BP=1.000, ratio=1.039, hyp_len=12713, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.1.51-4.50.1.26-3.52.1.29-3.62.1.06-2.90.pth, mybk
BLEU = 31.79, 58.7/37.4/25.4/18.2 (BP=1.000, ratio=1.089, hyp_len=12450, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.1.51-4.50.1.26-3.52.1.29-3.62.1.06-2.90.pth, bkmy
BLEU = 39.98, 66.4/46.3/33.3/25.0 (BP=1.000, ratio=1.030, hyp_len=12596, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.1.44-4.22.1.25-3.48.1.30-3.67.1.07-2.92.pth, mybk
BLEU = 32.13, 59.8/37.8/25.8/18.3 (BP=1.000, ratio=1.057, hyp_len=12080, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.1.44-4.22.1.25-3.48.1.30-3.67.1.07-2.92.pth, bkmy
BLEU = 41.13, 66.7/47.7/34.6/26.0 (BP=1.000, ratio=1.031, hyp_len=12609, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.1.36-3.91.1.16-3.20.1.29-3.65.1.07-2.90.pth, mybk
BLEU = 33.25, 60.8/38.8/26.7/19.4 (BP=1.000, ratio=1.045, hyp_len=11950, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.1.36-3.91.1.16-3.20.1.29-3.65.1.07-2.90.pth, bkmy
BLEU = 41.26, 66.7/47.4/34.8/26.3 (BP=1.000, ratio=1.047, hyp_len=12810, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.1.39-4.00.1.17-3.23.1.30-3.67.1.10-3.00.pth, mybk
BLEU = 33.33, 61.6/39.3/26.6/19.1 (BP=1.000, ratio=1.055, hyp_len=12057, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.1.39-4.00.1.17-3.23.1.30-3.67.1.10-3.00.pth, bkmy
BLEU = 38.14, 63.5/44.2/31.8/23.7 (BP=1.000, ratio=1.085, hyp_len=13266, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.1.32-3.73.1.12-3.07.1.31-3.70.1.11-3.04.pth, mybk
BLEU = 34.24, 61.7/40.0/27.8/20.0 (BP=1.000, ratio=1.041, hyp_len=11898, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.1.32-3.73.1.12-3.07.1.31-3.70.1.11-3.04.pth, bkmy
BLEU = 36.69, 62.2/42.9/30.4/22.3 (BP=1.000, ratio=1.114, hyp_len=13621, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.1.31-3.71.1.10-3.00.1.34-3.83.1.10-3.00.pth, mybk
BLEU = 33.16, 60.3/38.5/26.8/19.4 (BP=1.000, ratio=1.052, hyp_len=12024, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.1.31-3.71.1.10-3.00.1.34-3.83.1.10-3.00.pth, bkmy
BLEU = 40.82, 67.4/47.3/34.1/25.5 (BP=1.000, ratio=1.024, hyp_len=12527, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.1.28-3.59.1.05-2.87.1.34-3.81.1.08-2.95.pth, mybk
BLEU = 35.08, 62.4/40.8/28.6/20.8 (BP=1.000, ratio=1.051, hyp_len=12012, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.1.28-3.59.1.05-2.87.1.34-3.81.1.08-2.95.pth, bkmy
BLEU = 40.00, 66.2/46.3/33.4/25.0 (BP=1.000, ratio=1.043, hyp_len=12763, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.1.24-3.46.1.04-2.84.1.35-3.86.1.12-3.06.pth, mybk
BLEU = 34.18, 61.4/39.8/27.8/20.1 (BP=1.000, ratio=1.044, hyp_len=11936, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.1.24-3.46.1.04-2.84.1.35-3.86.1.12-3.06.pth, bkmy
BLEU = 40.09, 65.6/46.4/33.7/25.2 (BP=1.000, ratio=1.074, hyp_len=13137, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.1.28-3.61.1.07-2.92.1.34-3.81.1.10-2.99.pth, mybk
BLEU = 32.02, 59.4/37.7/25.6/18.3 (BP=1.000, ratio=1.086, hyp_len=12420, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.1.28-3.61.1.07-2.92.1.34-3.81.1.10-2.99.pth, bkmy
BLEU = 41.55, 67.1/47.9/35.0/26.5 (BP=1.000, ratio=1.040, hyp_len=12720, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.1.20-3.31.1.00-2.72.1.31-3.71.1.11-3.05.pth, mybk
BLEU = 34.01, 61.6/39.7/27.5/20.0 (BP=1.000, ratio=1.044, hyp_len=11937, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.1.20-3.31.1.00-2.72.1.31-3.71.1.11-3.05.pth, bkmy
BLEU = 40.52, 66.6/46.9/34.0/25.4 (BP=1.000, ratio=1.051, hyp_len=12855, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.31.1.19-3.29.0.98-2.66.1.34-3.81.1.13-3.11.pth, mybk
BLEU = 32.75, 59.8/38.1/26.3/19.2 (BP=1.000, ratio=1.041, hyp_len=11896, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.31.1.19-3.29.0.98-2.66.1.34-3.81.1.13-3.11.pth, bkmy
BLEU = 40.82, 66.4/46.9/34.3/26.0 (BP=1.000, ratio=1.026, hyp_len=12552, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.32.1.12-3.07.0.94-2.56.1.36-3.90.1.11-3.04.pth, mybk
BLEU = 32.41, 58.9/37.8/26.2/18.9 (BP=1.000, ratio=1.084, hyp_len=12398, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.32.1.12-3.07.0.94-2.56.1.36-3.90.1.11-3.04.pth, bkmy
BLEU = 40.46, 66.4/46.8/34.0/25.4 (BP=1.000, ratio=1.059, hyp_len=12951, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.33.1.12-3.07.0.93-2.53.1.38-3.98.1.16-3.20.pth, mybk
BLEU = 32.96, 59.7/38.3/26.6/19.4 (BP=1.000, ratio=1.048, hyp_len=11985, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.33.1.12-3.07.0.93-2.53.1.38-3.98.1.16-3.20.pth, bkmy
BLEU = 38.97, 65.1/45.4/32.5/24.0 (BP=1.000, ratio=1.063, hyp_len=12996, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.34.1.13-3.09.0.95-2.57.1.40-4.04.1.14-3.13.pth, mybk
BLEU = 32.63, 59.6/38.2/26.3/18.9 (BP=1.000, ratio=1.062, hyp_len=12141, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.34.1.13-3.09.0.95-2.57.1.40-4.04.1.14-3.13.pth, bkmy
BLEU = 39.47, 65.6/45.7/33.0/24.5 (BP=1.000, ratio=1.044, hyp_len=12767, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.35.1.10-3.00.0.92-2.51.1.41-4.09.1.17-3.21.pth, mybk
BLEU = 33.93, 60.8/39.3/27.5/20.2 (BP=1.000, ratio=1.045, hyp_len=11948, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.35.1.10-3.00.0.92-2.51.1.41-4.09.1.17-3.21.pth, bkmy
BLEU = 37.09, 62.9/43.3/30.8/22.5 (BP=1.000, ratio=1.086, hyp_len=13287, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.36.1.07-2.92.0.91-2.49.1.39-4.03.1.13-3.09.pth, mybk
BLEU = 32.30, 59.4/37.9/26.0/18.6 (BP=1.000, ratio=1.069, hyp_len=12221, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.36.1.07-2.92.0.91-2.49.1.39-4.03.1.13-3.09.pth, bkmy
BLEU = 39.95, 66.0/46.2/33.3/25.1 (BP=1.000, ratio=1.044, hyp_len=12767, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.37.1.07-2.90.0.91-2.49.1.40-4.06.1.17-3.22.pth, mybk
BLEU = 31.94, 58.9/37.3/25.7/18.4 (BP=1.000, ratio=1.063, hyp_len=12157, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.37.1.07-2.90.0.91-2.49.1.40-4.06.1.17-3.22.pth, bkmy
BLEU = 38.92, 65.5/45.4/32.4/23.8 (BP=1.000, ratio=1.045, hyp_len=12776, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.38.1.00-2.72.0.83-2.30.1.40-4.05.1.18-3.26.pth, mybk
BLEU = 32.60, 59.6/37.8/26.3/19.1 (BP=1.000, ratio=1.042, hyp_len=11909, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.38.1.00-2.72.0.83-2.30.1.40-4.05.1.18-3.26.pth, bkmy
BLEU = 39.74, 66.0/45.9/33.1/24.9 (BP=1.000, ratio=1.026, hyp_len=12551, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.39.1.03-2.81.0.85-2.33.1.44-4.20.1.18-3.25.pth, mybk
BLEU = 32.04, 59.4/37.3/25.6/18.6 (BP=1.000, ratio=1.048, hyp_len=11983, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.39.1.03-2.81.0.85-2.33.1.44-4.20.1.18-3.25.pth, bkmy
BLEU = 38.86, 64.9/45.0/32.3/24.2 (BP=1.000, ratio=1.044, hyp_len=12771, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.40.1.01-2.75.0.81-2.25.1.41-4.09.1.18-3.25.pth, mybk
BLEU = 32.52, 59.8/37.9/25.9/19.0 (BP=1.000, ratio=1.072, hyp_len=12250, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.40.1.01-2.75.0.81-2.25.1.41-4.09.1.18-3.25.pth, bkmy
BLEU = 39.30, 65.2/45.3/32.8/24.6 (BP=1.000, ratio=1.049, hyp_len=12828, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.41.1.00-2.72.0.85-2.35.1.42-4.14.1.24-3.45.pth, mybk
BLEU = 32.46, 59.9/38.0/26.0/18.7 (BP=1.000, ratio=1.061, hyp_len=12131, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.41.1.00-2.72.0.85-2.35.1.42-4.14.1.24-3.45.pth, bkmy
BLEU = 37.09, 62.7/43.0/30.8/22.8 (BP=1.000, ratio=1.084, hyp_len=13256, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.42.1.04-2.82.0.86-2.35.1.42-4.16.1.22-3.38.pth, mybk
BLEU = 31.88, 59.5/37.3/25.5/18.3 (BP=1.000, ratio=1.051, hyp_len=12015, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.42.1.04-2.82.0.86-2.35.1.42-4.16.1.22-3.38.pth, bkmy
BLEU = 39.77, 65.9/45.9/33.2/24.9 (BP=1.000, ratio=1.028, hyp_len=12577, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.43.0.97-2.63.0.79-2.21.1.46-4.30.1.24-3.46.pth, mybk
BLEU = 31.57, 59.3/37.3/25.2/17.8 (BP=1.000, ratio=1.055, hyp_len=12060, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.43.0.97-2.63.0.79-2.21.1.46-4.30.1.24-3.46.pth, bkmy
BLEU = 37.41, 63.3/43.4/31.0/23.0 (BP=1.000, ratio=1.062, hyp_len=12985, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.44.0.92-2.50.0.75-2.11.1.42-4.14.1.22-3.39.pth, mybk
BLEU = 31.88, 59.2/37.3/25.5/18.3 (BP=1.000, ratio=1.065, hyp_len=12177, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.44.0.92-2.50.0.75-2.11.1.42-4.14.1.22-3.39.pth, bkmy
BLEU = 39.79, 66.0/46.0/33.2/24.9 (BP=1.000, ratio=1.028, hyp_len=12578, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.45.0.93-2.53.0.77-2.15.1.45-4.25.1.20-3.33.pth, mybk
BLEU = 30.53, 57.4/35.7/24.3/17.4 (BP=1.000, ratio=1.075, hyp_len=12287, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.45.0.93-2.53.0.77-2.15.1.45-4.25.1.20-3.33.pth, bkmy
BLEU = 37.64, 63.9/43.8/31.2/23.0 (BP=1.000, ratio=1.060, hyp_len=12960, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.46.0.95-2.58.0.76-2.14.1.45-4.25.1.27-3.56.pth, mybk
BLEU = 30.90, 57.8/36.4/24.7/17.5 (BP=1.000, ratio=1.072, hyp_len=12250, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.46.0.95-2.58.0.76-2.14.1.45-4.25.1.27-3.56.pth, bkmy
BLEU = 36.63, 62.6/42.6/30.2/22.4 (BP=1.000, ratio=1.076, hyp_len=13162, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.47.0.85-2.35.0.70-2.02.1.44-4.24.1.27-3.56.pth, mybk
BLEU = 32.90, 59.3/37.9/26.5/19.7 (BP=1.000, ratio=1.062, hyp_len=12140, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.47.0.85-2.35.0.70-2.02.1.44-4.24.1.27-3.56.pth, bkmy
BLEU = 37.72, 64.2/44.1/31.2/22.9 (BP=1.000, ratio=1.064, hyp_len=13011, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.48.0.85-2.34.0.70-2.01.1.47-4.34.1.25-3.50.pth, mybk
BLEU = 33.37, 59.8/38.4/27.0/20.0 (BP=1.000, ratio=1.059, hyp_len=12102, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.48.0.85-2.34.0.70-2.01.1.47-4.34.1.25-3.50.pth, bkmy
BLEU = 38.88, 65.0/44.9/32.3/24.3 (BP=1.000, ratio=1.043, hyp_len=12759, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.49.0.86-2.36.0.70-2.01.1.48-4.37.1.31-3.70.pth, mybk
BLEU = 31.82, 58.5/37.0/25.5/18.6 (BP=1.000, ratio=1.081, hyp_len=12363, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.49.0.86-2.36.0.70-2.01.1.48-4.37.1.31-3.70.pth, bkmy
BLEU = 34.47, 59.7/40.1/28.3/20.8 (BP=1.000, ratio=1.107, hyp_len=13539, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.50.0.86-2.36.0.70-2.01.1.48-4.39.1.28-3.61.pth, mybk
BLEU = 31.60, 59.1/37.1/25.3/18.0 (BP=1.000, ratio=1.055, hyp_len=12058, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.50.0.86-2.36.0.70-2.01.1.48-4.39.1.28-3.61.pth, bkmy
BLEU = 36.71, 62.3/42.4/30.4/22.6 (BP=1.000, ratio=1.066, hyp_len=13035, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.51.0.81-2.24.0.65-1.92.1.48-4.39.1.28-3.61.pth, mybk
BLEU = 32.67, 59.8/38.1/26.2/19.1 (BP=1.000, ratio=1.054, hyp_len=12052, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.51.0.81-2.24.0.65-1.92.1.48-4.39.1.28-3.61.pth, bkmy
BLEU = 36.71, 62.2/42.6/30.3/22.6 (BP=1.000, ratio=1.096, hyp_len=13403, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.52.0.81-2.24.0.65-1.92.1.49-4.45.1.28-3.59.pth, mybk
BLEU = 33.25, 60.1/38.5/26.9/19.7 (BP=1.000, ratio=1.038, hyp_len=11861, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.52.0.81-2.24.0.65-1.92.1.49-4.45.1.28-3.59.pth, bkmy
BLEU = 35.96, 61.8/41.8/29.6/21.9 (BP=1.000, ratio=1.075, hyp_len=13151, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.53.0.80-2.22.0.65-1.92.1.49-4.44.1.25-3.49.pth, mybk
BLEU = 30.19, 56.6/35.4/24.1/17.2 (BP=1.000, ratio=1.088, hyp_len=12443, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.53.0.80-2.22.0.65-1.92.1.49-4.44.1.25-3.49.pth, bkmy
BLEU = 36.51, 61.7/42.1/30.2/22.6 (BP=1.000, ratio=1.093, hyp_len=13371, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.54.0.81-2.25.0.69-2.00.1.54-4.67.1.27-3.57.pth, mybk
BLEU = 30.55, 57.2/35.9/24.4/17.4 (BP=1.000, ratio=1.082, hyp_len=12375, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.54.0.81-2.25.0.69-2.00.1.54-4.67.1.27-3.57.pth, bkmy
BLEU = 37.30, 62.4/42.9/31.0/23.3 (BP=1.000, ratio=1.079, hyp_len=13193, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.55.0.84-2.31.0.68-1.97.1.55-4.69.1.26-3.54.pth, mybk
BLEU = 30.27, 57.8/35.8/24.0/16.9 (BP=1.000, ratio=1.080, hyp_len=12343, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.55.0.84-2.31.0.68-1.97.1.55-4.69.1.26-3.54.pth, bkmy
BLEU = 37.34, 63.5/43.6/30.9/22.8 (BP=1.000, ratio=1.064, hyp_len=13017, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.56.0.78-2.17.0.63-1.89.1.56-4.74.1.31-3.70.pth, mybk
BLEU = 28.99, 55.7/34.4/22.9/16.1 (BP=1.000, ratio=1.080, hyp_len=12352, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.56.0.78-2.17.0.63-1.89.1.56-4.74.1.31-3.70.pth, bkmy
BLEU = 35.44, 61.1/41.4/29.1/21.4 (BP=1.000, ratio=1.100, hyp_len=13455, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.57.0.75-2.12.0.61-1.85.1.55-4.70.1.30-3.67.pth, mybk
BLEU = 29.99, 56.5/35.0/23.8/17.2 (BP=1.000, ratio=1.081, hyp_len=12355, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.57.0.75-2.12.0.61-1.85.1.55-4.70.1.30-3.67.pth, bkmy
BLEU = 37.16, 63.1/43.5/30.7/22.7 (BP=1.000, ratio=1.059, hyp_len=12956, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.58.0.77-2.16.0.67-1.95.1.56-4.74.1.29-3.64.pth, mybk
BLEU = 31.01, 57.6/36.1/24.8/17.9 (BP=1.000, ratio=1.068, hyp_len=12214, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.58.0.77-2.16.0.67-1.95.1.56-4.74.1.29-3.64.pth, bkmy
BLEU = 35.86, 61.4/41.6/29.6/21.9 (BP=1.000, ratio=1.081, hyp_len=13221, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.59.0.75-2.12.0.61-1.83.1.56-4.74.1.31-3.70.pth, mybk
BLEU = 30.02, 56.5/35.6/23.9/16.9 (BP=1.000, ratio=1.097, hyp_len=12546, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.59.0.75-2.12.0.61-1.83.1.56-4.74.1.31-3.70.pth, bkmy
BLEU = 36.21, 61.7/41.9/29.9/22.3 (BP=1.000, ratio=1.057, hyp_len=12933, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.60.0.75-2.11.0.60-1.83.1.57-4.81.1.34-3.84.pth, mybk
BLEU = 29.82, 56.6/35.2/23.7/16.8 (BP=1.000, ratio=1.077, hyp_len=12310, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.60.0.75-2.11.0.60-1.83.1.57-4.81.1.34-3.84.pth, bkmy
BLEU = 36.94, 62.7/42.6/30.4/22.9 (BP=1.000, ratio=1.046, hyp_len=12799, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.61.0.75-2.11.0.61-1.84.1.61-5.00.1.34-3.81.pth, mybk
BLEU = 29.80, 56.8/35.1/23.5/16.8 (BP=1.000, ratio=1.071, hyp_len=12243, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.61.0.75-2.11.0.61-1.84.1.61-5.00.1.34-3.81.pth, bkmy
BLEU = 36.93, 62.5/42.7/30.6/22.8 (BP=1.000, ratio=1.048, hyp_len=12823, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.62.0.77-2.15.0.62-1.86.1.58-4.85.1.37-3.92.pth, mybk
BLEU = 31.33, 58.0/36.3/25.0/18.3 (BP=1.000, ratio=1.055, hyp_len=12064, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.62.0.77-2.15.0.62-1.86.1.58-4.85.1.37-3.92.pth, bkmy
BLEU = 35.88, 60.8/41.3/29.6/22.3 (BP=1.000, ratio=1.077, hyp_len=13170, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.63.0.69-1.99.0.57-1.76.1.56-4.75.1.36-3.88.pth, mybk
BLEU = 29.57, 56.1/34.8/23.3/16.8 (BP=1.000, ratio=1.074, hyp_len=12275, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.63.0.69-1.99.0.57-1.76.1.56-4.75.1.36-3.88.pth, bkmy
BLEU = 35.75, 61.3/41.6/29.4/21.8 (BP=1.000, ratio=1.080, hyp_len=13204, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.64.0.70-2.01.0.58-1.79.1.60-4.98.1.36-3.91.pth, mybk
BLEU = 30.12, 56.9/35.3/23.9/17.1 (BP=1.000, ratio=1.063, hyp_len=12151, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.64.0.70-2.01.0.58-1.79.1.60-4.98.1.36-3.91.pth, bkmy
BLEU = 33.99, 59.5/39.8/27.8/20.3 (BP=1.000, ratio=1.115, hyp_len=13635, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.65.0.71-2.02.0.57-1.77.1.62-5.06.1.38-3.99.pth, mybk
BLEU = 30.87, 57.8/36.2/24.6/17.7 (BP=1.000, ratio=1.050, hyp_len=12005, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.65.0.71-2.02.0.57-1.77.1.62-5.06.1.38-3.99.pth, bkmy
BLEU = 33.97, 59.1/39.8/27.9/20.3 (BP=1.000, ratio=1.148, hyp_len=14038, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.66.0.70-2.01.0.57-1.76.1.62-5.06.1.40-4.07.pth, mybk
BLEU = 29.19, 55.8/34.5/23.2/16.2 (BP=1.000, ratio=1.091, hyp_len=12470, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.66.0.70-2.01.0.57-1.76.1.62-5.06.1.40-4.07.pth, bkmy
BLEU = 33.45, 59.0/39.1/27.2/20.0 (BP=1.000, ratio=1.091, hyp_len=13339, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.67.0.70-2.01.0.56-1.74.1.61-4.99.1.39-4.02.pth, mybk
BLEU = 31.40, 58.8/36.9/25.0/18.0 (BP=1.000, ratio=1.055, hyp_len=12063, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.67.0.70-2.01.0.56-1.74.1.61-4.99.1.39-4.02.pth, bkmy
BLEU = 35.73, 61.3/41.4/29.3/21.9 (BP=1.000, ratio=1.067, hyp_len=13050, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.68.0.76-2.13.0.61-1.84.1.59-4.89.1.38-3.99.pth, mybk
BLEU = 29.07, 55.5/34.1/23.0/16.4 (BP=1.000, ratio=1.086, hyp_len=12419, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.68.0.76-2.13.0.61-1.84.1.59-4.89.1.38-3.99.pth, bkmy
BLEU = 37.14, 62.3/42.6/30.7/23.3 (BP=1.000, ratio=1.049, hyp_len=12829, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.69.0.69-2.00.0.56-1.75.1.65-5.22.1.40-4.05.pth, mybk
BLEU = 27.99, 54.3/33.0/22.0/15.6 (BP=1.000, ratio=1.124, hyp_len=12846, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.69.0.69-2.00.0.56-1.75.1.65-5.22.1.40-4.05.pth, bkmy
BLEU = 33.71, 58.7/39.0/27.5/20.5 (BP=1.000, ratio=1.078, hyp_len=13190, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.70.0.68-1.98.0.54-1.71.1.63-5.09.1.36-3.90.pth, mybk
BLEU = 29.82, 56.6/35.0/23.5/17.0 (BP=1.000, ratio=1.078, hyp_len=12320, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.70.0.68-1.98.0.54-1.71.1.63-5.09.1.36-3.90.pth, bkmy
BLEU = 34.24, 59.5/39.7/28.1/20.7 (BP=1.000, ratio=1.089, hyp_len=13319, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.71.0.67-1.94.0.53-1.70.1.61-4.99.1.39-4.02.pth, mybk
BLEU = 30.52, 57.2/35.7/24.3/17.5 (BP=1.000, ratio=1.062, hyp_len=12146, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.71.0.67-1.94.0.53-1.70.1.61-4.99.1.39-4.02.pth, bkmy
BLEU = 34.77, 59.5/40.3/28.7/21.2 (BP=1.000, ratio=1.099, hyp_len=13445, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.72.0.66-1.94.0.54-1.72.1.62-5.06.1.35-3.85.pth, mybk
BLEU = 29.88, 56.3/34.7/23.7/17.2 (BP=1.000, ratio=1.067, hyp_len=12199, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.72.0.66-1.94.0.54-1.72.1.62-5.06.1.35-3.85.pth, bkmy
BLEU = 35.42, 60.8/41.0/29.1/21.7 (BP=1.000, ratio=1.081, hyp_len=13217, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.73.0.66-1.94.0.53-1.69.1.61-4.99.1.39-4.01.pth, mybk
BLEU = 30.24, 57.9/35.6/24.0/16.9 (BP=1.000, ratio=1.054, hyp_len=12051, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.73.0.66-1.94.0.53-1.69.1.61-4.99.1.39-4.01.pth, bkmy
BLEU = 35.05, 60.3/40.8/28.8/21.3 (BP=1.000, ratio=1.087, hyp_len=13291, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.74.0.64-1.90.0.53-1.69.1.61-5.03.1.42-4.15.pth, mybk
BLEU = 30.00, 57.2/35.3/23.8/16.8 (BP=1.000, ratio=1.079, hyp_len=12337, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.74.0.64-1.90.0.53-1.69.1.61-5.03.1.42-4.15.pth, bkmy
BLEU = 34.47, 59.7/39.8/28.3/21.0 (BP=1.000, ratio=1.083, hyp_len=13247, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.75.0.63-1.87.0.49-1.64.1.64-5.15.1.43-4.19.pth, mybk
BLEU = 30.45, 57.0/35.5/24.3/17.5 (BP=1.000, ratio=1.078, hyp_len=12323, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.75.0.63-1.87.0.49-1.64.1.64-5.15.1.43-4.19.pth, bkmy
BLEU = 34.47, 60.1/40.0/28.2/20.8 (BP=1.000, ratio=1.071, hyp_len=13104, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.76.0.65-1.92.0.53-1.70.1.64-5.16.1.45-4.27.pth, mybk
BLEU = 29.15, 55.3/33.9/23.1/16.7 (BP=1.000, ratio=1.070, hyp_len=12232, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.76.0.65-1.92.0.53-1.70.1.64-5.16.1.45-4.27.pth, bkmy
BLEU = 32.87, 58.4/38.4/26.7/19.5 (BP=1.000, ratio=1.087, hyp_len=13289, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.77.0.64-1.90.0.51-1.67.1.66-5.25.1.46-4.31.pth, mybk
BLEU = 29.24, 55.3/34.2/23.2/16.6 (BP=1.000, ratio=1.073, hyp_len=12270, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.77.0.64-1.90.0.51-1.67.1.66-5.25.1.46-4.31.pth, bkmy
BLEU = 32.72, 58.0/38.1/26.6/19.5 (BP=1.000, ratio=1.089, hyp_len=13314, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.78.0.62-1.85.0.50-1.65.1.67-5.29.1.42-4.14.pth, mybk
BLEU = 29.70, 56.1/35.0/23.6/16.8 (BP=1.000, ratio=1.070, hyp_len=12228, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.78.0.62-1.85.0.50-1.65.1.67-5.29.1.42-4.14.pth, bkmy
BLEU = 34.91, 60.7/40.5/28.5/21.2 (BP=1.000, ratio=1.059, hyp_len=12950, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.79.0.62-1.85.0.50-1.64.1.66-5.25.1.41-4.11.pth, mybk
BLEU = 28.55, 55.3/33.7/22.5/15.8 (BP=1.000, ratio=1.084, hyp_len=12389, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.79.0.62-1.85.0.50-1.64.1.66-5.25.1.41-4.11.pth, bkmy
BLEU = 34.25, 59.4/39.6/28.1/20.8 (BP=1.000, ratio=1.088, hyp_len=13305, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.80.0.62-1.87.0.51-1.66.1.64-5.13.1.43-4.17.pth, mybk
BLEU = 29.02, 56.4/34.3/22.8/16.1 (BP=1.000, ratio=1.070, hyp_len=12232, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.80.0.62-1.87.0.51-1.66.1.64-5.13.1.43-4.17.pth, bkmy
BLEU = 35.19, 60.9/40.9/28.9/21.3 (BP=1.000, ratio=1.060, hyp_len=12970, ref_len=12231)
```

Best model for my-bk က epoch 27 မော်ဒယ် ဖြစ်ပြီးတော့၊ Best BLEU Score က : 35.08   
Best model for bk-my က epoch 29 မော်ဒယ် ဖြစ်ပြီးတော့၊ Best BLEU Score က : 41.55  


## Transformer-DSL, 90 epoch

```
Epoch 1 - |param|=8.52e+02 |g_param|=2.97e+05 loss_x2y=4.4218e+00 ppl_x2y=83.24 loss_y2x=4.1014e+00 ppl_y2x=60.42 dual_loss=0.0000e+00
Validation X2Y - loss=3.6540e+00 ppl=38.63 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=3.3299e+00 ppl=27.94 best_loss=inf best_ppl=inf
Epoch 2 - |param|=8.53e+02 |g_param|=2.69e+05 loss_x2y=3.5669e+00 ppl_x2y=35.41 loss_y2x=3.1724e+00 ppl_y2x=23.86 dual_loss=0.0000e+00
Validation X2Y - loss=3.0181e+00 ppl=20.45 best_loss=3.6540e+00 best_ppl=38.63                                          
Validation Y2X - loss=2.7134e+00 ppl=15.08 best_loss=3.3299e+00 best_ppl=27.94
Epoch 3 - |param|=8.53e+02 |g_param|=2.59e+05 loss_x2y=3.2661e+00 ppl_x2y=26.21 loss_y2x=2.8767e+00 ppl_y2x=17.75 dual_loss=0.0000e+00
Validation X2Y - loss=2.5699e+00 ppl=13.06 best_loss=3.0181e+00 best_ppl=20.45                                          
Validation Y2X - loss=2.4151e+00 ppl=11.19 best_loss=2.7134e+00 best_ppl=15.08
Epoch 4 - |param|=8.54e+02 |g_param|=2.75e+05 loss_x2y=2.9730e+00 ppl_x2y=19.55 loss_y2x=2.6271e+00 ppl_y2x=13.83 dual_loss=0.0000e+00
Validation X2Y - loss=2.2687e+00 ppl=9.67 best_loss=2.5699e+00 best_ppl=13.06                                           
Validation Y2X - loss=2.1245e+00 ppl=8.37 best_loss=2.4151e+00 best_ppl=11.19
Epoch 5 - |param|=8.55e+02 |g_param|=2.84e+05 loss_x2y=2.7864e+00 ppl_x2y=16.22 loss_y2x=2.4579e+00 ppl_y2x=11.68 dual_loss=0.0000e+00
Validation X2Y - loss=2.0534e+00 ppl=7.79 best_loss=2.2687e+00 best_ppl=9.67                                            
Validation Y2X - loss=1.9236e+00 ppl=6.85 best_loss=2.1245e+00 best_ppl=8.37
Epoch 6 - |param|=8.55e+02 |g_param|=3.13e+05 loss_x2y=2.5893e+00 ppl_x2y=13.32 loss_y2x=2.2577e+00 ppl_y2x=9.56 dual_loss=0.0000e+00
Validation X2Y - loss=1.8359e+00 ppl=6.27 best_loss=2.0534e+00 best_ppl=7.79                                            
Validation Y2X - loss=1.6833e+00 ppl=5.38 best_loss=1.9236e+00 best_ppl=6.85
Epoch 7 - |param|=8.56e+02 |g_param|=3.14e+05 loss_x2y=2.5301e+00 ppl_x2y=12.56 loss_y2x=2.2402e+00 ppl_y2x=9.40 dual_loss=0.0000e+00
Validation X2Y - loss=1.7191e+00 ppl=5.58 best_loss=1.8359e+00 best_ppl=6.27                                            
Validation Y2X - loss=1.5104e+00 ppl=4.53 best_loss=1.6833e+00 best_ppl=5.38
Epoch 8 - |param|=8.56e+02 |g_param|=3.39e+05 loss_x2y=2.3510e+00 ppl_x2y=10.50 loss_y2x=2.0661e+00 ppl_y2x=7.89 dual_loss=0.0000e+00
Validation X2Y - loss=1.5870e+00 ppl=4.89 best_loss=1.7191e+00 best_ppl=5.58                                            
Validation Y2X - loss=1.4415e+00 ppl=4.23 best_loss=1.5104e+00 best_ppl=4.53
Epoch 9 - |param|=8.57e+02 |g_param|=3.32e+05 loss_x2y=2.2306e+00 ppl_x2y=9.31 loss_y2x=1.9355e+00 ppl_y2x=6.93 dual_loss=0.0000e+00
Validation X2Y - loss=1.4933e+00 ppl=4.45 best_loss=1.5870e+00 best_ppl=4.89                                            
Validation Y2X - loss=1.3693e+00 ppl=3.93 best_loss=1.4415e+00 best_ppl=4.23
Epoch 10 - |param|=8.57e+02 |g_param|=3.45e+05 loss_x2y=2.0985e+00 ppl_x2y=8.15 loss_y2x=1.8235e+00 ppl_y2x=6.19 dual_loss=0.0000e+00
Validation X2Y - loss=1.4305e+00 ppl=4.18 best_loss=1.4933e+00 best_ppl=4.45                                            
Validation Y2X - loss=1.2628e+00 ppl=3.54 best_loss=1.3693e+00 best_ppl=3.93
Epoch 11 - |param|=8.58e+02 |g_param|=3.39e+05 loss_x2y=2.0013e+00 ppl_x2y=7.40 loss_y2x=1.7257e+00 ppl_y2x=5.62 dual_loss=0.0000e+00
Validation X2Y - loss=1.4219e+00 ppl=4.14 best_loss=1.4305e+00 best_ppl=4.18                                            
Validation Y2X - loss=1.2346e+00 ppl=3.44 best_loss=1.2628e+00 best_ppl=3.54
Epoch 12 - |param|=8.59e+02 |g_param|=3.73e+05 loss_x2y=1.9676e+00 ppl_x2y=7.15 loss_y2x=1.6846e+00 ppl_y2x=5.39 dual_loss=0.0000e+00
Validation X2Y - loss=1.3375e+00 ppl=3.81 best_loss=1.4219e+00 best_ppl=4.14                                            
Validation Y2X - loss=1.2203e+00 ppl=3.39 best_loss=1.2346e+00 best_ppl=3.44
Epoch 13 - |param|=8.59e+02 |g_param|=3.63e+05 loss_x2y=1.8415e+00 ppl_x2y=6.31 loss_y2x=1.5898e+00 ppl_y2x=4.90 dual_loss=0.0000e+00
Validation X2Y - loss=1.2890e+00 ppl=3.63 best_loss=1.3375e+00 best_ppl=3.81                                            
Validation Y2X - loss=1.1517e+00 ppl=3.16 best_loss=1.2203e+00 best_ppl=3.39
Epoch 14 - |param|=8.60e+02 |g_param|=3.83e+05 loss_x2y=1.7813e+00 ppl_x2y=5.94 loss_y2x=1.5200e+00 ppl_y2x=4.57 dual_loss=0.0000e+00
Validation X2Y - loss=1.2823e+00 ppl=3.60 best_loss=1.2890e+00 best_ppl=3.63                                            
Validation Y2X - loss=1.1298e+00 ppl=3.10 best_loss=1.1517e+00 best_ppl=3.16
Epoch 15 - |param|=8.60e+02 |g_param|=3.76e+05 loss_x2y=1.7310e+00 ppl_x2y=5.65 loss_y2x=1.4916e+00 ppl_y2x=4.44 dual_loss=0.0000e+00
Validation X2Y - loss=1.3087e+00 ppl=3.70 best_loss=1.2823e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1510e+00 ppl=3.16 best_loss=1.1298e+00 best_ppl=3.10
Epoch 16 - |param|=8.61e+02 |g_param|=4.18e+05 loss_x2y=1.7266e+00 ppl_x2y=5.62 loss_y2x=1.4999e+00 ppl_y2x=4.48 dual_loss=0.0000e+00
Validation X2Y - loss=1.3053e+00 ppl=3.69 best_loss=1.2823e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1045e+00 ppl=3.02 best_loss=1.1298e+00 best_ppl=3.10
Epoch 17 - |param|=8.61e+02 |g_param|=3.97e+05 loss_x2y=1.6552e+00 ppl_x2y=5.23 loss_y2x=1.4091e+00 ppl_y2x=4.09 dual_loss=0.0000e+00
Validation X2Y - loss=1.2649e+00 ppl=3.54 best_loss=1.2823e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1034e+00 ppl=3.01 best_loss=1.1045e+00 best_ppl=3.02
Epoch 18 - |param|=8.62e+02 |g_param|=4.14e+05 loss_x2y=1.5755e+00 ppl_x2y=4.83 loss_y2x=1.3433e+00 ppl_y2x=3.83 dual_loss=0.0000e+00
Validation X2Y - loss=1.2763e+00 ppl=3.58 best_loss=1.2649e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.0741e+00 ppl=2.93 best_loss=1.1034e+00 best_ppl=3.01
  5%|████▏                                                                                       | 1/22 [00:00<?, ?it/s]Epoch 19 - |param|=8.62e+02 |g_param|=4.23e+05 loss_x2y=1.5818e+00 ppl_x2y=4.86 loss_y2x=1.3371e+00 ppl_y2x=3.81 dual_loss=0.0000e+00
Validation X2Y - loss=1.2549e+00 ppl=3.51 best_loss=1.2649e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.0830e+00 ppl=2.95 best_loss=1.0741e+00 best_ppl=2.93
Epoch 20 - |param|=8.63e+02 |g_param|=4.32e+05 loss_x2y=1.4749e+00 ppl_x2y=4.37 loss_y2x=1.2742e+00 ppl_y2x=3.58 dual_loss=0.0000e+00
Validation X2Y - loss=1.2391e+00 ppl=3.45 best_loss=1.2549e+00 best_ppl=3.51                                            
Validation Y2X - loss=1.0751e+00 ppl=2.93 best_loss=1.0741e+00 best_ppl=2.93
Epoch 21 - |param|=8.63e+02 |g_param|=4.21e+05 loss_x2y=1.4736e+00 ppl_x2y=4.36 loss_y2x=1.2555e+00 ppl_y2x=3.51 dual_loss=5.8957e-01
Validation X2Y - loss=1.2606e+00 ppl=3.53 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.0607e+00 ppl=2.89 best_loss=1.0741e+00 best_ppl=2.93
Epoch 22 - |param|=8.64e+02 |g_param|=4.44e+05 loss_x2y=1.4888e+00 ppl_x2y=4.43 loss_y2x=1.2568e+00 ppl_y2x=3.51 dual_loss=5.2353e-01
Validation X2Y - loss=1.2666e+00 ppl=3.55 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.0716e+00 ppl=2.92 best_loss=1.0607e+00 best_ppl=2.89
Epoch 23 - |param|=8.65e+02 |g_param|=4.43e+05 loss_x2y=1.5428e+00 ppl_x2y=4.68 loss_y2x=1.2966e+00 ppl_y2x=3.66 dual_loss=6.3918e-01
Validation X2Y - loss=1.3149e+00 ppl=3.72 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.0954e+00 ppl=2.99 best_loss=1.0607e+00 best_ppl=2.89
Epoch 24 - |param|=8.65e+02 |g_param|=4.76e+05 loss_x2y=1.3817e+00 ppl_x2y=3.98 loss_y2x=1.1885e+00 ppl_y2x=3.28 dual_loss=5.4870e-01
Validation X2Y - loss=1.3009e+00 ppl=3.67 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.0715e+00 ppl=2.92 best_loss=1.0607e+00 best_ppl=2.89
Epoch 25 - |param|=8.66e+02 |g_param|=4.60e+05 loss_x2y=1.4140e+00 ppl_x2y=4.11 loss_y2x=1.2058e+00 ppl_y2x=3.34 dual_loss=5.4999e-01
Validation X2Y - loss=1.3026e+00 ppl=3.68 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.0542e+00 ppl=2.87 best_loss=1.0607e+00 best_ppl=2.89
Epoch 26 - |param|=8.66e+02 |g_param|=4.79e+05 loss_x2y=1.3251e+00 ppl_x2y=3.76 loss_y2x=1.1327e+00 ppl_y2x=3.10 dual_loss=5.0670e-01
Validation X2Y - loss=1.2999e+00 ppl=3.67 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.0899e+00 ppl=2.97 best_loss=1.0542e+00 best_ppl=2.87
Epoch 27 - |param|=8.67e+02 |g_param|=4.70e+05 loss_x2y=1.3643e+00 ppl_x2y=3.91 loss_y2x=1.1311e+00 ppl_y2x=3.10 dual_loss=6.2746e-01
Validation X2Y - loss=1.3131e+00 ppl=3.72 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.0619e+00 ppl=2.89 best_loss=1.0542e+00 best_ppl=2.87
Epoch 28 - |param|=8.67e+02 |g_param|=4.65e+05 loss_x2y=1.1912e+00 ppl_x2y=3.29 loss_y2x=9.9886e-01 ppl_y2x=2.72 dual_loss=4.6541e-01
Validation X2Y - loss=1.3078e+00 ppl=3.70 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.0617e+00 ppl=2.89 best_loss=1.0542e+00 best_ppl=2.87
Epoch 29 - |param|=8.68e+02 |g_param|=4.67e+05 loss_x2y=1.2099e+00 ppl_x2y=3.35 loss_y2x=1.0039e+00 ppl_y2x=2.73 dual_loss=4.9976e-01
Validation X2Y - loss=1.3146e+00 ppl=3.72 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1008e+00 ppl=3.01 best_loss=1.0542e+00 best_ppl=2.87
Epoch 30 - |param|=8.68e+02 |g_param|=5.02e+05 loss_x2y=1.1922e+00 ppl_x2y=3.29 loss_y2x=1.0136e+00 ppl_y2x=2.76 dual_loss=5.0742e-01
Validation X2Y - loss=1.3269e+00 ppl=3.77 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1087e+00 ppl=3.03 best_loss=1.0542e+00 best_ppl=2.87
Epoch 31 - |param|=8.69e+02 |g_param|=4.57e+05 loss_x2y=1.1530e+00 ppl_x2y=3.17 loss_y2x=9.5054e-01 ppl_y2x=2.59 dual_loss=5.1616e-01
Validation X2Y - loss=1.3379e+00 ppl=3.81 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1076e+00 ppl=3.03 best_loss=1.0542e+00 best_ppl=2.87
Epoch 32 - |param|=8.69e+02 |g_param|=4.95e+05 loss_x2y=1.1309e+00 ppl_x2y=3.10 loss_y2x=9.4400e-01 ppl_y2x=2.57 dual_loss=5.4939e-01
Validation X2Y - loss=1.3424e+00 ppl=3.83 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.0972e+00 ppl=3.00 best_loss=1.0542e+00 best_ppl=2.87
Epoch 33 - |param|=8.70e+02 |g_param|=8.19e+05 loss_x2y=1.1455e+00 ppl_x2y=3.14 loss_y2x=9.6103e-01 ppl_y2x=2.61 dual_loss=5.5284e-01
Validation X2Y - loss=1.3681e+00 ppl=3.93 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1306e+00 ppl=3.10 best_loss=1.0542e+00 best_ppl=2.87
Epoch 34 - |param|=8.70e+02 |g_param|=1.00e+06 loss_x2y=1.0813e+00 ppl_x2y=2.95 loss_y2x=9.0064e-01 ppl_y2x=2.46 dual_loss=5.4047e-01
Validation X2Y - loss=1.3881e+00 ppl=4.01 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1170e+00 ppl=3.06 best_loss=1.0542e+00 best_ppl=2.87
Epoch 35 - |param|=8.71e+02 |g_param|=9.70e+05 loss_x2y=1.0554e+00 ppl_x2y=2.87 loss_y2x=8.9905e-01 ppl_y2x=2.46 dual_loss=6.2241e-01
Validation X2Y - loss=1.3845e+00 ppl=3.99 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1125e+00 ppl=3.04 best_loss=1.0542e+00 best_ppl=2.87
Epoch 36 - |param|=8.71e+02 |g_param|=1.04e+06 loss_x2y=1.0853e+00 ppl_x2y=2.96 loss_y2x=9.4737e-01 ppl_y2x=2.58 dual_loss=6.6842e-01
Validation X2Y - loss=1.3862e+00 ppl=4.00 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1264e+00 ppl=3.08 best_loss=1.0542e+00 best_ppl=2.87
Epoch 37 - |param|=8.72e+02 |g_param|=1.00e+06 loss_x2y=1.0695e+00 ppl_x2y=2.91 loss_y2x=9.1308e-01 ppl_y2x=2.49 dual_loss=6.9155e-01
Validation X2Y - loss=1.4205e+00 ppl=4.14 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1511e+00 ppl=3.16 best_loss=1.0542e+00 best_ppl=2.87
Epoch 38 - |param|=8.72e+02 |g_param|=1.02e+06 loss_x2y=1.0189e+00 ppl_x2y=2.77 loss_y2x=8.7961e-01 ppl_y2x=2.41 dual_loss=6.2567e-01
Validation X2Y - loss=1.4205e+00 ppl=4.14 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1580e+00 ppl=3.18 best_loss=1.0542e+00 best_ppl=2.87
Epoch 39 - |param|=8.73e+02 |g_param|=8.55e+05 loss_x2y=9.7835e-01 ppl_x2y=2.66 loss_y2x=8.1991e-01 ppl_y2x=2.27 dual_loss=6.2854e-01
Validation X2Y - loss=1.4095e+00 ppl=4.09 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1407e+00 ppl=3.13 best_loss=1.0542e+00 best_ppl=2.87
Epoch 40 - |param|=8.73e+02 |g_param|=8.20e+05 loss_x2y=9.7889e-01 ppl_x2y=2.66 loss_y2x=8.1084e-01 ppl_y2x=2.25 dual_loss=6.4952e-01
Validation X2Y - loss=1.4352e+00 ppl=4.20 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1327e+00 ppl=3.10 best_loss=1.0542e+00 best_ppl=2.87
Epoch 41 - |param|=8.74e+02 |g_param|=8.05e+05 loss_x2y=9.8260e-01 ppl_x2y=2.67 loss_y2x=8.0006e-01 ppl_y2x=2.23 dual_loss=6.6824e-01
Validation X2Y - loss=1.4535e+00 ppl=4.28 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1802e+00 ppl=3.25 best_loss=1.0542e+00 best_ppl=2.87
Epoch 42 - |param|=8.74e+02 |g_param|=8.37e+05 loss_x2y=9.4731e-01 ppl_x2y=2.58 loss_y2x=8.1978e-01 ppl_y2x=2.27 dual_loss=7.5012e-01
Validation X2Y - loss=1.4635e+00 ppl=4.32 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1585e+00 ppl=3.19 best_loss=1.0542e+00 best_ppl=2.87
Epoch 43 - |param|=8.75e+02 |g_param|=8.08e+05 loss_x2y=1.0124e+00 ppl_x2y=2.75 loss_y2x=8.3417e-01 ppl_y2x=2.30 dual_loss=8.4498e-01
Validation X2Y - loss=1.4756e+00 ppl=4.37 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1580e+00 ppl=3.18 best_loss=1.0542e+00 best_ppl=2.87
Epoch 44 - |param|=8.75e+02 |g_param|=8.38e+05 loss_x2y=9.6963e-01 ppl_x2y=2.64 loss_y2x=8.1640e-01 ppl_y2x=2.26 dual_loss=8.0279e-01
Validation X2Y - loss=1.4922e+00 ppl=4.45 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.2041e+00 ppl=3.33 best_loss=1.0542e+00 best_ppl=2.87
Epoch 45 - |param|=8.76e+02 |g_param|=8.37e+05 loss_x2y=9.3711e-01 ppl_x2y=2.55 loss_y2x=7.8114e-01 ppl_y2x=2.18 dual_loss=8.3003e-01
Validation X2Y - loss=1.5121e+00 ppl=4.54 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1826e+00 ppl=3.26 best_loss=1.0542e+00 best_ppl=2.87
Epoch 46 - |param|=8.76e+02 |g_param|=8.06e+05 loss_x2y=9.0237e-01 ppl_x2y=2.47 loss_y2x=7.3794e-01 ppl_y2x=2.09 dual_loss=7.5454e-01
Validation X2Y - loss=1.5170e+00 ppl=4.56 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1787e+00 ppl=3.25 best_loss=1.0542e+00 best_ppl=2.87
Epoch 47 - |param|=8.77e+02 |g_param|=8.02e+05 loss_x2y=8.5323e-01 ppl_x2y=2.35 loss_y2x=7.2954e-01 ppl_y2x=2.07 dual_loss=7.2948e-01
Validation X2Y - loss=1.5049e+00 ppl=4.50 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1911e+00 ppl=3.29 best_loss=1.0542e+00 best_ppl=2.87
Epoch 48 - |param|=8.77e+02 |g_param|=8.31e+05 loss_x2y=8.7863e-01 ppl_x2y=2.41 loss_y2x=7.1198e-01 ppl_y2x=2.04 dual_loss=7.9632e-01
Validation X2Y - loss=1.5188e+00 ppl=4.57 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1952e+00 ppl=3.30 best_loss=1.0542e+00 best_ppl=2.87
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 49 - |param|=8.78e+02 |g_param|=7.88e+05 loss_x2y=8.3991e-01 ppl_x2y=2.32 loss_y2x=6.8663e-01 ppl_y2x=1.99 dual_loss=7.0808e-01
Validation X2Y - loss=1.5321e+00 ppl=4.63 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1681e+00 ppl=3.22 best_loss=1.0542e+00 best_ppl=2.87
Iteration:   5%|██▊                                                          | 1/22 [00:00<?, ?it/s, x2y=1.35, y2x=1.02]Epoch 50 - |param|=8.78e+02 |g_param|=8.34e+05 loss_x2y=8.3680e-01 ppl_x2y=2.31 loss_y2x=6.8483e-01 ppl_y2x=1.98 dual_loss=7.5661e-01
Validation X2Y - loss=1.5204e+00 ppl=4.57 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.2105e+00 ppl=3.36 best_loss=1.0542e+00 best_ppl=2.87
Epoch 51 - |param|=8.79e+02 |g_param|=7.87e+05 loss_x2y=8.4507e-01 ppl_x2y=2.33 loss_y2x=6.9241e-01 ppl_y2x=2.00 dual_loss=7.3835e-01
Validation X2Y - loss=1.5521e+00 ppl=4.72 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.2367e+00 ppl=3.44 best_loss=1.0542e+00 best_ppl=2.87
Epoch 52 - |param|=8.79e+02 |g_param|=8.18e+05 loss_x2y=8.4891e-01 ppl_x2y=2.34 loss_y2x=6.8372e-01 ppl_y2x=1.98 dual_loss=7.8744e-01
Validation X2Y - loss=1.5656e+00 ppl=4.79 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.2019e+00 ppl=3.33 best_loss=1.0542e+00 best_ppl=2.87
Epoch 53 - |param|=8.80e+02 |g_param|=8.09e+05 loss_x2y=8.1295e-01 ppl_x2y=2.25 loss_y2x=6.6286e-01 ppl_y2x=1.94 dual_loss=8.1063e-01
Validation X2Y - loss=1.5312e+00 ppl=4.62 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.2391e+00 ppl=3.45 best_loss=1.0542e+00 best_ppl=2.87
Epoch 54 - |param|=8.80e+02 |g_param|=8.25e+05 loss_x2y=7.8988e-01 ppl_x2y=2.20 loss_y2x=6.6780e-01 ppl_y2x=1.95 dual_loss=9.3485e-01
Validation X2Y - loss=1.5924e+00 ppl=4.92 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.1677e+00 ppl=3.21 best_loss=1.0542e+00 best_ppl=2.87
Epoch 55 - |param|=8.81e+02 |g_param|=7.96e+05 loss_x2y=7.8870e-01 ppl_x2y=2.20 loss_y2x=6.5174e-01 ppl_y2x=1.92 dual_loss=8.1994e-01
Validation X2Y - loss=1.5613e+00 ppl=4.77 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.2391e+00 ppl=3.45 best_loss=1.0542e+00 best_ppl=2.87
Epoch 56 - |param|=8.81e+02 |g_param|=8.36e+05 loss_x2y=7.8869e-01 ppl_x2y=2.20 loss_y2x=6.5811e-01 ppl_y2x=1.93 dual_loss=8.3119e-01
Validation X2Y - loss=1.6188e+00 ppl=5.05 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.2806e+00 ppl=3.60 best_loss=1.0542e+00 best_ppl=2.87
Epoch 57 - |param|=8.82e+02 |g_param|=7.98e+05 loss_x2y=7.6017e-01 ppl_x2y=2.14 loss_y2x=6.2548e-01 ppl_y2x=1.87 dual_loss=8.4313e-01
Validation X2Y - loss=1.6219e+00 ppl=5.06 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.2516e+00 ppl=3.50 best_loss=1.0542e+00 best_ppl=2.87
Epoch 58 - |param|=8.82e+02 |g_param|=8.28e+05 loss_x2y=8.6193e-01 ppl_x2y=2.37 loss_y2x=6.6597e-01 ppl_y2x=1.95 dual_loss=1.1529e+00
Validation X2Y - loss=1.6053e+00 ppl=4.98 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.2805e+00 ppl=3.60 best_loss=1.0542e+00 best_ppl=2.87
Epoch 59 - |param|=8.82e+02 |g_param|=8.15e+05 loss_x2y=7.3799e-01 ppl_x2y=2.09 loss_y2x=6.0726e-01 ppl_y2x=1.84 dual_loss=8.4882e-01
Validation X2Y - loss=1.5904e+00 ppl=4.91 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.2643e+00 ppl=3.54 best_loss=1.0542e+00 best_ppl=2.87
Epoch 60 - |param|=8.83e+02 |g_param|=8.44e+05 loss_x2y=7.3612e-01 ppl_x2y=2.09 loss_y2x=5.9377e-01 ppl_y2x=1.81 dual_loss=8.4973e-01
Validation X2Y - loss=1.6096e+00 ppl=5.00 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3071e+00 ppl=3.70 best_loss=1.0542e+00 best_ppl=2.87
Epoch 61 - |param|=8.83e+02 |g_param|=7.94e+05 loss_x2y=7.2112e-01 ppl_x2y=2.06 loss_y2x=5.9932e-01 ppl_y2x=1.82 dual_loss=8.6463e-01
Validation X2Y - loss=1.6549e+00 ppl=5.23 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.2809e+00 ppl=3.60 best_loss=1.0542e+00 best_ppl=2.87
Epoch 62 - |param|=8.84e+02 |g_param|=8.27e+05 loss_x2y=7.3550e-01 ppl_x2y=2.09 loss_y2x=6.0802e-01 ppl_y2x=1.84 dual_loss=9.5389e-01
Validation X2Y - loss=1.6731e+00 ppl=5.33 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3283e+00 ppl=3.77 best_loss=1.0542e+00 best_ppl=2.87
Epoch 63 - |param|=8.84e+02 |g_param|=8.04e+05 loss_x2y=7.6332e-01 ppl_x2y=2.15 loss_y2x=6.1093e-01 ppl_y2x=1.84 dual_loss=1.0242e+00
Validation X2Y - loss=1.6597e+00 ppl=5.26 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.2871e+00 ppl=3.62 best_loss=1.0542e+00 best_ppl=2.87
Epoch 64 - |param|=8.85e+02 |g_param|=8.38e+05 loss_x2y=8.0701e-01 ppl_x2y=2.24 loss_y2x=6.3894e-01 ppl_y2x=1.89 dual_loss=1.2029e+00
Validation X2Y - loss=1.6879e+00 ppl=5.41 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3035e+00 ppl=3.68 best_loss=1.0542e+00 best_ppl=2.87
Epoch 65 - |param|=8.85e+02 |g_param|=8.32e+05 loss_x2y=7.2579e-01 ppl_x2y=2.07 loss_y2x=6.1828e-01 ppl_y2x=1.86 dual_loss=1.0594e+00
Validation X2Y - loss=1.6839e+00 ppl=5.39 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3809e+00 ppl=3.98 best_loss=1.0542e+00 best_ppl=2.87
Epoch 66 - |param|=8.86e+02 |g_param|=8.33e+05 loss_x2y=7.0412e-01 ppl_x2y=2.02 loss_y2x=5.7089e-01 ppl_y2x=1.77 dual_loss=9.8042e-01
Validation X2Y - loss=1.6438e+00 ppl=5.17 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3282e+00 ppl=3.77 best_loss=1.0542e+00 best_ppl=2.87
Epoch 67 - |param|=8.86e+02 |g_param|=8.11e+05 loss_x2y=7.7292e-01 ppl_x2y=2.17 loss_y2x=6.1567e-01 ppl_y2x=1.85 dual_loss=1.2550e+00
Validation X2Y - loss=1.6960e+00 ppl=5.45 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3449e+00 ppl=3.84 best_loss=1.0542e+00 best_ppl=2.87
Epoch 68 - |param|=8.87e+02 |g_param|=8.27e+05 loss_x2y=7.8869e-01 ppl_x2y=2.20 loss_y2x=5.9167e-01 ppl_y2x=1.81 dual_loss=1.1614e+00
Validation X2Y - loss=1.7021e+00 ppl=5.49 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3443e+00 ppl=3.84 best_loss=1.0542e+00 best_ppl=2.87
Epoch 69 - |param|=8.87e+02 |g_param|=7.75e+05 loss_x2y=6.7747e-01 ppl_x2y=1.97 loss_y2x=5.5420e-01 ppl_y2x=1.74 dual_loss=9.2708e-01
Validation X2Y - loss=1.7260e+00 ppl=5.62 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3269e+00 ppl=3.77 best_loss=1.0542e+00 best_ppl=2.87
Epoch 70 - |param|=8.87e+02 |g_param|=8.32e+05 loss_x2y=6.7396e-01 ppl_x2y=1.96 loss_y2x=5.4607e-01 ppl_y2x=1.73 dual_loss=9.2746e-01
Validation X2Y - loss=1.7335e+00 ppl=5.66 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3345e+00 ppl=3.80 best_loss=1.0542e+00 best_ppl=2.87
Epoch 71 - |param|=8.88e+02 |g_param|=7.86e+05 loss_x2y=6.8371e-01 ppl_x2y=1.98 loss_y2x=5.7492e-01 ppl_y2x=1.78 dual_loss=1.1403e+00
Validation X2Y - loss=1.6994e+00 ppl=5.47 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3243e+00 ppl=3.76 best_loss=1.0542e+00 best_ppl=2.87
Epoch 72 - |param|=8.88e+02 |g_param|=9.88e+05 loss_x2y=6.5316e-01 ppl_x2y=1.92 loss_y2x=5.2371e-01 ppl_y2x=1.69 dual_loss=9.1047e-01
Validation X2Y - loss=1.7442e+00 ppl=5.72 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3583e+00 ppl=3.89 best_loss=1.0542e+00 best_ppl=2.87
Epoch 73 - |param|=8.89e+02 |g_param|=8.12e+05 loss_x2y=6.4661e-01 ppl_x2y=1.91 loss_y2x=5.1128e-01 ppl_y2x=1.67 dual_loss=9.2624e-01
Validation X2Y - loss=1.7104e+00 ppl=5.53 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3524e+00 ppl=3.87 best_loss=1.0542e+00 best_ppl=2.87
Epoch 74 - |param|=8.89e+02 |g_param|=7.92e+05 loss_x2y=6.2638e-01 ppl_x2y=1.87 loss_y2x=5.1272e-01 ppl_y2x=1.67 dual_loss=9.3628e-01
Validation X2Y - loss=1.7459e+00 ppl=5.73 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3848e+00 ppl=3.99 best_loss=1.0542e+00 best_ppl=2.87
Epoch 75 - |param|=8.90e+02 |g_param|=8.37e+05 loss_x2y=6.6626e-01 ppl_x2y=1.95 loss_y2x=5.8184e-01 ppl_y2x=1.79 dual_loss=1.6205e+00
Validation X2Y - loss=1.7549e+00 ppl=5.78 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3640e+00 ppl=3.91 best_loss=1.0542e+00 best_ppl=2.87
Epoch 76 - |param|=8.90e+02 |g_param|=8.10e+05 loss_x2y=6.3112e-01 ppl_x2y=1.88 loss_y2x=5.0833e-01 ppl_y2x=1.66 dual_loss=9.1404e-01
Validation X2Y - loss=1.7282e+00 ppl=5.63 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3761e+00 ppl=3.96 best_loss=1.0542e+00 best_ppl=2.87
Epoch 77 - |param|=8.90e+02 |g_param|=7.60e+05 loss_x2y=6.1157e-01 ppl_x2y=1.84 loss_y2x=4.8520e-01 ppl_y2x=1.62 dual_loss=9.1551e-01
Validation X2Y - loss=1.7496e+00 ppl=5.75 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3781e+00 ppl=3.97 best_loss=1.0542e+00 best_ppl=2.87
Epoch 78 - |param|=8.91e+02 |g_param|=7.98e+05 loss_x2y=6.2368e-01 ppl_x2y=1.87 loss_y2x=5.0666e-01 ppl_y2x=1.66 dual_loss=9.9715e-01
Validation X2Y - loss=1.7589e+00 ppl=5.81 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3999e+00 ppl=4.05 best_loss=1.0542e+00 best_ppl=2.87
Epoch 79 - |param|=8.91e+02 |g_param|=7.72e+05 loss_x2y=6.0044e-01 ppl_x2y=1.82 loss_y2x=4.8546e-01 ppl_y2x=1.62 dual_loss=9.6158e-01
Validation X2Y - loss=1.7609e+00 ppl=5.82 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.3806e+00 ppl=3.98 best_loss=1.0542e+00 best_ppl=2.87
Epoch 80 - |param|=8.92e+02 |g_param|=8.18e+05 loss_x2y=6.0579e-01 ppl_x2y=1.83 loss_y2x=5.0837e-01 ppl_y2x=1.66 dual_loss=1.0449e+00
Validation X2Y - loss=1.7728e+00 ppl=5.89 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.4182e+00 ppl=4.13 best_loss=1.0542e+00 best_ppl=2.87
Epoch 81 - |param|=8.92e+02 |g_param|=7.85e+05 loss_x2y=6.2203e-01 ppl_x2y=1.86 loss_y2x=5.0385e-01 ppl_y2x=1.66 dual_loss=1.0220e+00
Validation X2Y - loss=1.7459e+00 ppl=5.73 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.4135e+00 ppl=4.11 best_loss=1.0542e+00 best_ppl=2.87
Epoch 82 - |param|=8.93e+02 |g_param|=8.10e+05 loss_x2y=6.7445e-01 ppl_x2y=1.96 loss_y2x=5.1537e-01 ppl_y2x=1.67 dual_loss=1.2321e+00
Validation X2Y - loss=1.7401e+00 ppl=5.70 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.4222e+00 ppl=4.15 best_loss=1.0542e+00 best_ppl=2.87
Epoch 83 - |param|=8.93e+02 |g_param|=7.70e+05 loss_x2y=6.5263e-01 ppl_x2y=1.92 loss_y2x=5.0886e-01 ppl_y2x=1.66 dual_loss=1.2227e+00
Validation X2Y - loss=1.7635e+00 ppl=5.83 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.4186e+00 ppl=4.13 best_loss=1.0542e+00 best_ppl=2.87
Epoch 84 - |param|=8.93e+02 |g_param|=7.94e+05 loss_x2y=5.7374e-01 ppl_x2y=1.77 loss_y2x=4.7787e-01 ppl_y2x=1.61 dual_loss=9.9149e-01
Validation X2Y - loss=1.7698e+00 ppl=5.87 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.4474e+00 ppl=4.25 best_loss=1.0542e+00 best_ppl=2.87
Epoch 85 - |param|=8.94e+02 |g_param|=7.49e+05 loss_x2y=5.6187e-01 ppl_x2y=1.75 loss_y2x=4.5363e-01 ppl_y2x=1.57 dual_loss=9.9446e-01
Validation X2Y - loss=1.7840e+00 ppl=5.95 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.4376e+00 ppl=4.21 best_loss=1.0542e+00 best_ppl=2.87
Epoch 86 - |param|=8.94e+02 |g_param|=7.80e+05 loss_x2y=5.8409e-01 ppl_x2y=1.79 loss_y2x=4.7186e-01 ppl_y2x=1.60 dual_loss=1.0873e+00
Validation X2Y - loss=1.8169e+00 ppl=6.15 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.4194e+00 ppl=4.13 best_loss=1.0542e+00 best_ppl=2.87
Epoch 87 - |param|=8.95e+02 |g_param|=7.83e+05 loss_x2y=5.8613e-01 ppl_x2y=1.80 loss_y2x=4.9311e-01 ppl_y2x=1.64 dual_loss=1.1364e+00
Validation X2Y - loss=1.8499e+00 ppl=6.36 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.4785e+00 ppl=4.39 best_loss=1.0542e+00 best_ppl=2.87
Epoch 88 - |param|=8.95e+02 |g_param|=8.28e+05 loss_x2y=5.8226e-01 ppl_x2y=1.79 loss_y2x=4.6540e-01 ppl_y2x=1.59 dual_loss=1.1533e+00
Validation X2Y - loss=1.8415e+00 ppl=6.31 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.4359e+00 ppl=4.20 best_loss=1.0542e+00 best_ppl=2.87
Epoch 89 - |param|=8.95e+02 |g_param|=7.65e+05 loss_x2y=5.8832e-01 ppl_x2y=1.80 loss_y2x=4.8509e-01 ppl_y2x=1.62 dual_loss=1.1849e+00
Validation X2Y - loss=1.8196e+00 ppl=6.17 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.4694e+00 ppl=4.35 best_loss=1.0542e+00 best_ppl=2.87
Epoch 90 - |param|=8.96e+02 |g_param|=8.15e+05 loss_x2y=5.9671e-01 ppl_x2y=1.82 loss_y2x=4.8554e-01 ppl_y2x=1.63 dual_loss=1.3309e+00
Validation X2Y - loss=1.8162e+00 ppl=6.15 best_loss=1.2391e+00 best_ppl=3.45                                            
Validation Y2X - loss=1.4496e+00 ppl=4.26 best_loss=1.0542e+00 best_ppl=2.87

real	29m30.558s
user	29m0.889s
sys	0m24.565s
```

testing/evaluation...  

```
/home/ye/exp/simple-nmt/model/dsl/transformer/mybk-90epoch
Evaluation result for the model: dsl-model-mybk.01.4.42-83.24.4.10-60.42.3.65-38.63.3.33-27.94.pth, mybk
BLEU = 3.14, 15.5/4.5/1.7/0.8 (BP=1.000, ratio=1.575, hyp_len=18001, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.42-83.24.4.10-60.42.3.65-38.63.3.33-27.94.pth, bkmy
BLEU = 4.71, 26.9/7.0/2.7/1.0 (BP=1.000, ratio=1.070, hyp_len=13093, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.02.3.57-35.41.3.17-23.86.3.02-20.45.2.71-15.08.pth, mybk
BLEU = 3.09, 15.4/4.5/1.7/0.8 (BP=1.000, ratio=1.679, hyp_len=19194, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.3.57-35.41.3.17-23.86.3.02-20.45.2.71-15.08.pth, bkmy
BLEU = 4.73, 26.4/8.1/2.9/0.8 (BP=1.000, ratio=1.147, hyp_len=14029, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.3.27-26.21.2.88-17.75.2.57-13.06.2.42-11.19.pth, mybk
BLEU = 7.19, 29.1/10.1/4.4/2.1 (BP=0.996, ratio=0.997, hyp_len=11392, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.3.27-26.21.2.88-17.75.2.57-13.06.2.42-11.19.pth, bkmy
BLEU = 8.53, 37.5/13.8/5.7/2.5 (BP=0.922, ratio=0.925, hyp_len=11309, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.2.97-19.55.2.63-13.83.2.27-9.67.2.12-8.37.pth, mybk
BLEU = 4.93, 17.9/6.9/3.2/1.5 (BP=1.000, ratio=2.041, hyp_len=23328, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.2.97-19.55.2.63-13.83.2.27-9.67.2.12-8.37.pth, bkmy
BLEU = 11.93, 39.8/17.2/8.0/3.7 (BP=1.000, ratio=1.013, hyp_len=12393, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.2.79-16.22.2.46-11.68.2.05-7.79.1.92-6.85.pth, mybk
BLEU = 12.46, 36.6/16.7/8.7/4.5 (BP=1.000, ratio=1.140, hyp_len=13033, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.2.79-16.22.2.46-11.68.2.05-7.79.1.92-6.85.pth, bkmy
BLEU = 16.01, 46.2/22.5/11.6/6.1 (BP=0.973, ratio=0.973, hyp_len=11905, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.2.59-13.32.2.26-9.56.1.84-6.27.1.68-5.38.pth, mybk
BLEU = 18.99, 46.9/24.1/14.0/8.2 (BP=1.000, ratio=1.001, hyp_len=11445, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.2.59-13.32.2.26-9.56.1.84-6.27.1.68-5.38.pth, bkmy
BLEU = 21.37, 50.6/27.9/16.5/10.1 (BP=0.970, ratio=0.971, hyp_len=11872, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.2.53-12.56.2.24-9.40.1.72-5.58.1.51-4.53.pth, mybk
BLEU = 19.15, 44.6/23.8/14.3/8.9 (BP=1.000, ratio=1.128, hyp_len=12895, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.2.53-12.56.2.24-9.40.1.72-5.58.1.51-4.53.pth, bkmy
BLEU = 26.78, 55.8/33.2/20.7/13.5 (BP=0.998, ratio=0.998, hyp_len=12206, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.2.35-10.50.2.07-7.89.1.59-4.89.1.44-4.23.pth, mybk
BLEU = 24.34, 52.2/29.7/18.6/12.2 (BP=1.000, ratio=1.027, hyp_len=11745, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.2.35-10.50.2.07-7.89.1.59-4.89.1.44-4.23.pth, bkmy
BLEU = 28.15, 57.0/34.8/22.2/14.8 (BP=0.992, ratio=0.992, hyp_len=12133, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.2.23-9.31.1.94-6.93.1.49-4.45.1.37-3.93.pth, mybk
BLEU = 21.25, 45.6/26.2/16.3/10.4 (BP=1.000, ratio=1.204, hyp_len=13764, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.2.23-9.31.1.94-6.93.1.49-4.45.1.37-3.93.pth, bkmy
BLEU = 30.13, 57.8/36.2/23.7/16.6 (BP=1.000, ratio=1.005, hyp_len=12291, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.2.10-8.15.1.82-6.19.1.43-4.18.1.26-3.54.pth, mybk
BLEU = 24.06, 49.8/29.1/18.7/12.4 (BP=1.000, ratio=1.128, hyp_len=12898, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.2.10-8.15.1.82-6.19.1.43-4.18.1.26-3.54.pth, bkmy
BLEU = 34.18, 61.7/40.5/27.6/19.7 (BP=1.000, ratio=1.014, hyp_len=12398, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.2.00-7.40.1.73-5.62.1.42-4.14.1.23-3.44.pth, mybk
BLEU = 28.41, 55.6/34.0/22.4/15.4 (BP=1.000, ratio=1.034, hyp_len=11817, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.2.00-7.40.1.73-5.62.1.42-4.14.1.23-3.44.pth, bkmy
BLEU = 36.16, 63.6/42.8/29.9/21.8 (BP=0.991, ratio=0.991, hyp_len=12116, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.1.97-7.15.1.68-5.39.1.34-3.81.1.22-3.39.pth, mybk
BLEU = 29.45, 57.6/35.4/23.3/15.8 (BP=1.000, ratio=1.043, hyp_len=11925, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.1.97-7.15.1.68-5.39.1.34-3.81.1.22-3.39.pth, bkmy
BLEU = 35.51, 62.2/41.6/29.1/21.4 (BP=0.997, ratio=0.997, hyp_len=12199, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.1.84-6.31.1.59-4.90.1.29-3.63.1.15-3.16.pth, mybk
BLEU = 28.78, 56.0/34.6/22.8/15.6 (BP=1.000, ratio=1.058, hyp_len=12098, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.1.84-6.31.1.59-4.90.1.29-3.63.1.15-3.16.pth, bkmy
BLEU = 37.29, 63.5/43.7/30.8/22.6 (BP=1.000, ratio=1.043, hyp_len=12761, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.1.78-5.94.1.52-4.57.1.28-3.60.1.13-3.10.pth, mybk
BLEU = 31.20, 58.7/36.8/25.0/17.5 (BP=1.000, ratio=1.025, hyp_len=11715, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.1.78-5.94.1.52-4.57.1.28-3.60.1.13-3.10.pth, bkmy
BLEU = 38.67, 65.5/45.3/32.1/23.5 (BP=1.000, ratio=1.031, hyp_len=12610, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.1.73-5.65.1.49-4.44.1.31-3.70.1.15-3.16.pth, mybk
BLEU = 32.28, 60.1/38.2/25.9/18.3 (BP=1.000, ratio=1.021, hyp_len=11670, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.1.73-5.65.1.49-4.44.1.31-3.70.1.15-3.16.pth, bkmy
BLEU = 35.61, 61.8/41.8/29.3/21.3 (BP=1.000, ratio=1.066, hyp_len=13038, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.1.73-5.62.1.50-4.48.1.31-3.69.1.10-3.02.pth, mybk
BLEU = 29.74, 56.2/35.3/23.8/16.6 (BP=1.000, ratio=1.099, hyp_len=12563, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.1.73-5.62.1.50-4.48.1.31-3.69.1.10-3.02.pth, bkmy
BLEU = 36.95, 63.4/43.4/30.5/22.2 (BP=1.000, ratio=1.074, hyp_len=13132, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.1.66-5.23.1.41-4.09.1.26-3.54.1.10-3.01.pth, mybk
BLEU = 31.21, 57.9/36.9/25.1/17.7 (BP=1.000, ratio=1.118, hyp_len=12776, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.1.66-5.23.1.41-4.09.1.26-3.54.1.10-3.01.pth, bkmy
BLEU = 38.25, 64.5/44.7/31.7/23.4 (BP=1.000, ratio=1.067, hyp_len=13054, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.1.58-4.83.1.34-3.83.1.28-3.58.1.07-2.93.pth, mybk
BLEU = 30.92, 57.1/36.4/24.8/17.7 (BP=1.000, ratio=1.097, hyp_len=12540, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.1.58-4.83.1.34-3.83.1.28-3.58.1.07-2.93.pth, bkmy
BLEU = 40.19, 66.5/46.6/33.5/25.1 (BP=1.000, ratio=1.007, hyp_len=12313, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.1.58-4.86.1.34-3.81.1.25-3.51.1.08-2.95.pth, mybk
BLEU = 33.33, 60.5/39.3/27.0/19.2 (BP=1.000, ratio=1.043, hyp_len=11920, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.1.58-4.86.1.34-3.81.1.25-3.51.1.08-2.95.pth, bkmy
BLEU = 39.97, 66.0/46.2/33.4/25.1 (BP=1.000, ratio=1.051, hyp_len=12855, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.1.47-4.37.1.27-3.58.1.24-3.45.1.08-2.93.pth, mybk
BLEU = 33.19, 60.5/39.2/27.0/19.0 (BP=1.000, ratio=1.056, hyp_len=12070, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.1.47-4.37.1.27-3.58.1.24-3.45.1.08-2.93.pth, bkmy
BLEU = 40.46, 66.6/46.8/34.0/25.3 (BP=1.000, ratio=1.032, hyp_len=12624, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.1.47-4.36.1.26-3.51.1.26-3.53.1.06-2.89.pth, mybk
BLEU = 31.32, 57.7/37.0/25.2/17.9 (BP=1.000, ratio=1.125, hyp_len=12866, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.1.47-4.36.1.26-3.51.1.26-3.53.1.06-2.89.pth, bkmy
BLEU = 40.76, 66.6/47.2/34.3/25.6 (BP=1.000, ratio=1.059, hyp_len=12947, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.1.49-4.43.1.26-3.51.1.27-3.55.1.07-2.92.pth, mybk
BLEU = 32.36, 58.9/38.1/26.2/18.6 (BP=1.000, ratio=1.090, hyp_len=12461, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.1.49-4.43.1.26-3.51.1.27-3.55.1.07-2.92.pth, bkmy
BLEU = 39.84, 66.1/46.2/33.3/24.7 (BP=1.000, ratio=1.061, hyp_len=12973, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.1.54-4.68.1.30-3.66.1.31-3.72.1.10-2.99.pth, mybk
BLEU = 31.73, 58.3/37.0/25.6/18.4 (BP=1.000, ratio=1.066, hyp_len=12183, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.1.54-4.68.1.30-3.66.1.31-3.72.1.10-2.99.pth, bkmy
BLEU = 40.04, 65.8/45.8/33.4/25.5 (BP=1.000, ratio=1.032, hyp_len=12619, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.1.38-3.98.1.19-3.28.1.30-3.67.1.07-2.92.pth, mybk
BLEU = 33.80, 60.7/39.3/27.5/19.9 (BP=1.000, ratio=1.052, hyp_len=12030, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.1.38-3.98.1.19-3.28.1.30-3.67.1.07-2.92.pth, bkmy
BLEU = 41.23, 66.9/47.2/34.7/26.3 (BP=1.000, ratio=1.035, hyp_len=12657, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.1.41-4.11.1.21-3.34.1.30-3.68.1.05-2.87.pth, mybk
BLEU = 32.47, 60.4/38.1/26.0/18.5 (BP=1.000, ratio=1.060, hyp_len=12115, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.1.41-4.11.1.21-3.34.1.30-3.68.1.05-2.87.pth, bkmy
BLEU = 39.00, 65.0/44.9/32.4/24.4 (BP=1.000, ratio=1.052, hyp_len=12866, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.1.33-3.76.1.13-3.10.1.30-3.67.1.09-2.97.pth, mybk
BLEU = 34.77, 61.8/40.1/28.2/20.9 (BP=1.000, ratio=1.018, hyp_len=11642, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.1.33-3.76.1.13-3.10.1.30-3.67.1.09-2.97.pth, bkmy
BLEU = 39.10, 64.3/45.0/32.8/24.6 (BP=1.000, ratio=1.072, hyp_len=13112, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.1.36-3.91.1.13-3.10.1.31-3.72.1.06-2.89.pth, mybk
BLEU = 31.51, 58.3/37.0/25.3/18.1 (BP=1.000, ratio=1.073, hyp_len=12269, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.1.36-3.91.1.13-3.10.1.31-3.72.1.06-2.89.pth, bkmy
BLEU = 41.79, 67.7/48.0/35.2/26.7 (BP=1.000, ratio=1.021, hyp_len=12486, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.1.19-3.29.1.00-2.72.1.31-3.70.1.06-2.89.pth, mybk
BLEU = 34.52, 61.7/40.3/28.1/20.3 (BP=1.000, ratio=1.067, hyp_len=12203, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.1.19-3.29.1.00-2.72.1.31-3.70.1.06-2.89.pth, bkmy
BLEU = 40.03, 66.0/46.4/33.5/25.0 (BP=1.000, ratio=1.064, hyp_len=13016, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.1.21-3.35.1.00-2.73.1.31-3.72.1.10-3.01.pth, mybk
BLEU = 33.03, 60.1/38.7/26.7/19.2 (BP=1.000, ratio=1.074, hyp_len=12278, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.1.21-3.35.1.00-2.73.1.31-3.72.1.10-3.01.pth, bkmy
BLEU = 39.83, 65.7/46.1/33.4/24.9 (BP=1.000, ratio=1.053, hyp_len=12879, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.1.19-3.29.1.01-2.76.1.33-3.77.1.11-3.03.pth, mybk
BLEU = 31.74, 58.6/37.5/25.5/18.1 (BP=1.000, ratio=1.108, hyp_len=12663, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.1.19-3.29.1.01-2.76.1.33-3.77.1.11-3.03.pth, bkmy
BLEU = 38.23, 64.4/44.5/31.7/23.5 (BP=1.000, ratio=1.060, hyp_len=12966, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.31.1.15-3.17.0.95-2.59.1.34-3.81.1.11-3.03.pth, mybk
BLEU = 33.13, 60.2/38.8/26.7/19.3 (BP=1.000, ratio=1.052, hyp_len=12030, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.31.1.15-3.17.0.95-2.59.1.34-3.81.1.11-3.03.pth, bkmy
BLEU = 38.28, 63.5/44.1/32.0/23.9 (BP=1.000, ratio=1.089, hyp_len=13323, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.32.1.13-3.10.0.94-2.57.1.34-3.83.1.10-3.00.pth, mybk
BLEU = 32.20, 59.0/37.8/25.9/18.6 (BP=1.000, ratio=1.086, hyp_len=12414, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.32.1.13-3.10.0.94-2.57.1.34-3.83.1.10-3.00.pth, bkmy
BLEU = 38.52, 64.4/44.8/32.2/23.7 (BP=1.000, ratio=1.088, hyp_len=13307, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.33.1.15-3.14.0.96-2.61.1.37-3.93.1.13-3.10.pth, mybk
BLEU = 33.24, 60.5/38.8/26.9/19.4 (BP=1.000, ratio=1.056, hyp_len=12077, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.33.1.15-3.14.0.96-2.61.1.37-3.93.1.13-3.10.pth, bkmy
BLEU = 39.18, 64.7/45.1/32.8/24.7 (BP=1.000, ratio=1.056, hyp_len=12919, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.34.1.08-2.95.0.90-2.46.1.39-4.01.1.12-3.06.pth, mybk
BLEU = 32.57, 59.5/38.3/26.4/18.7 (BP=1.000, ratio=1.077, hyp_len=12310, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.34.1.08-2.95.0.90-2.46.1.39-4.01.1.12-3.06.pth, bkmy
BLEU = 39.91, 65.6/45.9/33.5/25.1 (BP=1.000, ratio=1.064, hyp_len=13009, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.35.1.06-2.87.0.90-2.46.1.38-3.99.1.11-3.04.pth, mybk
BLEU = 33.48, 61.1/39.1/27.0/19.5 (BP=1.000, ratio=1.024, hyp_len=11705, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.35.1.06-2.87.0.90-2.46.1.38-3.99.1.11-3.04.pth, bkmy
BLEU = 39.41, 65.6/45.7/32.9/24.5 (BP=1.000, ratio=1.061, hyp_len=12977, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.36.1.09-2.96.0.95-2.58.1.39-4.00.1.13-3.08.pth, mybk
BLEU = 33.26, 59.9/38.6/26.9/19.6 (BP=1.000, ratio=1.050, hyp_len=11998, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.36.1.09-2.96.0.95-2.58.1.39-4.00.1.13-3.08.pth, bkmy
BLEU = 39.44, 65.2/45.5/32.9/24.8 (BP=1.000, ratio=1.060, hyp_len=12969, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.37.1.07-2.91.0.91-2.49.1.42-4.14.1.15-3.16.pth, mybk
BLEU = 31.43, 57.8/36.8/25.4/18.1 (BP=1.000, ratio=1.079, hyp_len=12337, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.37.1.07-2.91.0.91-2.49.1.42-4.14.1.15-3.16.pth, bkmy
BLEU = 37.34, 62.7/43.1/31.0/23.2 (BP=1.000, ratio=1.082, hyp_len=13238, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.38.1.02-2.77.0.88-2.41.1.42-4.14.1.16-3.18.pth, mybk
BLEU = 34.01, 60.8/39.5/27.7/20.1 (BP=1.000, ratio=1.048, hyp_len=11983, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.38.1.02-2.77.0.88-2.41.1.42-4.14.1.16-3.18.pth, bkmy
BLEU = 37.67, 63.0/43.4/31.3/23.5 (BP=1.000, ratio=1.065, hyp_len=13032, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.39.0.98-2.66.0.82-2.27.1.41-4.09.1.14-3.13.pth, mybk
BLEU = 33.57, 61.7/39.5/27.0/19.3 (BP=1.000, ratio=1.039, hyp_len=11876, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.39.0.98-2.66.0.82-2.27.1.41-4.09.1.14-3.13.pth, bkmy
BLEU = 39.04, 64.9/45.2/32.5/24.4 (BP=1.000, ratio=1.040, hyp_len=12725, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.40.0.98-2.66.0.81-2.25.1.44-4.20.1.13-3.10.pth, mybk
BLEU = 32.64, 59.8/38.2/26.4/18.8 (BP=1.000, ratio=1.057, hyp_len=12080, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.40.0.98-2.66.0.81-2.25.1.44-4.20.1.13-3.10.pth, bkmy
BLEU = 38.53, 64.5/44.7/32.0/23.9 (BP=1.000, ratio=1.061, hyp_len=12973, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.41.0.98-2.67.0.80-2.23.1.45-4.28.1.18-3.25.pth, mybk
BLEU = 32.52, 59.0/37.9/26.3/19.1 (BP=1.000, ratio=1.072, hyp_len=12252, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.41.0.98-2.67.0.80-2.23.1.45-4.28.1.18-3.25.pth, bkmy
BLEU = 37.87, 63.3/43.6/31.4/23.7 (BP=1.000, ratio=1.091, hyp_len=13343, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.42.0.95-2.58.0.82-2.27.1.46-4.32.1.16-3.19.pth, mybk
BLEU = 32.20, 59.7/37.9/25.8/18.4 (BP=1.000, ratio=1.066, hyp_len=12186, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.42.0.95-2.58.0.82-2.27.1.46-4.32.1.16-3.19.pth, bkmy
BLEU = 39.32, 65.3/45.6/32.7/24.6 (BP=1.000, ratio=1.054, hyp_len=12889, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.43.1.01-2.75.0.83-2.30.1.48-4.37.1.16-3.18.pth, mybk
BLEU = 31.41, 58.4/37.1/25.2/17.8 (BP=1.000, ratio=1.088, hyp_len=12435, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.43.1.01-2.75.0.83-2.30.1.48-4.37.1.16-3.18.pth, bkmy
BLEU = 36.30, 61.8/42.2/30.0/22.2 (BP=1.000, ratio=1.078, hyp_len=13179, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.44.0.97-2.64.0.82-2.26.1.49-4.45.1.20-3.33.pth, mybk
BLEU = 32.96, 60.1/38.4/26.5/19.3 (BP=1.000, ratio=1.061, hyp_len=12132, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.44.0.97-2.64.0.82-2.26.1.49-4.45.1.20-3.33.pth, bkmy
BLEU = 37.78, 63.7/43.9/31.3/23.2 (BP=1.000, ratio=1.069, hyp_len=13069, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.45.0.94-2.55.0.78-2.18.1.51-4.54.1.18-3.26.pth, mybk
BLEU = 32.54, 59.8/38.0/26.2/18.8 (BP=1.000, ratio=1.038, hyp_len=11870, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.45.0.94-2.55.0.78-2.18.1.51-4.54.1.18-3.26.pth, bkmy
BLEU = 37.14, 62.7/42.8/30.8/23.1 (BP=1.000, ratio=1.045, hyp_len=12781, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.46.0.90-2.47.0.74-2.09.1.52-4.56.1.18-3.25.pth, mybk
BLEU = 31.09, 58.1/36.6/24.9/17.7 (BP=1.000, ratio=1.085, hyp_len=12407, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.46.0.90-2.47.0.74-2.09.1.52-4.56.1.18-3.25.pth, bkmy
BLEU = 37.47, 63.4/43.5/31.1/23.0 (BP=1.000, ratio=1.065, hyp_len=13021, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.47.0.85-2.35.0.73-2.07.1.50-4.50.1.19-3.29.pth, mybk
BLEU = 32.50, 59.5/38.0/26.2/18.8 (BP=1.000, ratio=1.067, hyp_len=12203, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.47.0.85-2.35.0.73-2.07.1.50-4.50.1.19-3.29.pth, bkmy
BLEU = 38.40, 64.4/44.6/31.9/23.8 (BP=1.000, ratio=1.068, hyp_len=13064, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.48.0.88-2.41.0.71-2.04.1.52-4.57.1.20-3.30.pth, mybk
BLEU = 31.03, 58.4/36.7/24.8/17.4 (BP=1.000, ratio=1.096, hyp_len=12533, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.48.0.88-2.41.0.71-2.04.1.52-4.57.1.20-3.30.pth, bkmy
BLEU = 38.31, 64.7/44.5/31.7/23.6 (BP=1.000, ratio=1.048, hyp_len=12818, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.49.0.84-2.32.0.69-1.99.1.53-4.63.1.17-3.22.pth, mybk
BLEU = 32.01, 58.7/37.2/25.8/18.6 (BP=1.000, ratio=1.069, hyp_len=12221, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.49.0.84-2.32.0.69-1.99.1.53-4.63.1.17-3.22.pth, bkmy
BLEU = 37.73, 63.6/43.7/31.2/23.4 (BP=1.000, ratio=1.060, hyp_len=12969, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.50.0.84-2.31.0.68-1.98.1.52-4.57.1.21-3.36.pth, mybk
BLEU = 33.23, 61.0/39.0/26.7/19.2 (BP=1.000, ratio=1.042, hyp_len=11908, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.50.0.84-2.31.0.68-1.98.1.52-4.57.1.21-3.36.pth, bkmy
BLEU = 35.87, 61.3/41.4/29.6/22.0 (BP=1.000, ratio=1.084, hyp_len=13263, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.51.0.85-2.33.0.69-2.00.1.55-4.72.1.24-3.44.pth, mybk
BLEU = 31.07, 58.2/36.5/24.9/17.6 (BP=1.000, ratio=1.072, hyp_len=12251, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.51.0.85-2.33.0.69-2.00.1.55-4.72.1.24-3.44.pth, bkmy
BLEU = 34.41, 60.3/40.2/28.2/20.5 (BP=1.000, ratio=1.072, hyp_len=13109, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.52.0.85-2.34.0.68-1.98.1.57-4.79.1.20-3.33.pth, mybk
BLEU = 31.35, 58.1/36.7/25.1/18.0 (BP=1.000, ratio=1.089, hyp_len=12454, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.52.0.85-2.34.0.68-1.98.1.57-4.79.1.20-3.33.pth, bkmy
BLEU = 37.92, 64.1/44.1/31.4/23.3 (BP=1.000, ratio=1.054, hyp_len=12888, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.53.0.81-2.25.0.66-1.94.1.53-4.62.1.24-3.45.pth, mybk
BLEU = 31.25, 58.5/36.8/25.0/17.7 (BP=1.000, ratio=1.077, hyp_len=12308, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.53.0.81-2.25.0.66-1.94.1.53-4.62.1.24-3.45.pth, bkmy
BLEU = 34.99, 60.6/40.7/28.8/21.1 (BP=1.000, ratio=1.082, hyp_len=13239, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.54.0.79-2.20.0.67-1.95.1.59-4.92.1.17-3.21.pth, mybk
BLEU = 31.46, 59.0/37.3/25.1/17.7 (BP=1.000, ratio=1.067, hyp_len=12201, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.54.0.79-2.20.0.67-1.95.1.59-4.92.1.17-3.21.pth, bkmy
BLEU = 36.86, 62.6/42.6/30.5/22.6 (BP=1.000, ratio=1.065, hyp_len=13029, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.55.0.79-2.20.0.65-1.92.1.56-4.77.1.24-3.45.pth, mybk
BLEU = 31.97, 59.2/37.4/25.6/18.4 (BP=1.000, ratio=1.050, hyp_len=12000, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.55.0.79-2.20.0.65-1.92.1.56-4.77.1.24-3.45.pth, bkmy
BLEU = 35.95, 61.7/41.9/29.6/21.8 (BP=1.000, ratio=1.063, hyp_len=13006, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.56.0.79-2.20.0.66-1.93.1.62-5.05.1.28-3.60.pth, mybk
BLEU = 30.74, 57.9/36.2/24.6/17.3 (BP=1.000, ratio=1.076, hyp_len=12296, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.56.0.79-2.20.0.66-1.93.1.62-5.05.1.28-3.60.pth, bkmy
BLEU = 35.40, 61.4/41.4/29.1/21.2 (BP=1.000, ratio=1.085, hyp_len=13275, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.57.0.76-2.14.0.63-1.87.1.62-5.06.1.25-3.50.pth, mybk
BLEU = 31.00, 57.3/36.3/24.8/17.9 (BP=1.000, ratio=1.080, hyp_len=12347, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.57.0.76-2.14.0.63-1.87.1.62-5.06.1.25-3.50.pth, bkmy
BLEU = 34.16, 60.1/39.9/27.8/20.4 (BP=1.000, ratio=1.094, hyp_len=13384, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.58.0.86-2.37.0.67-1.95.1.61-4.98.1.28-3.60.pth, mybk
BLEU = 30.47, 57.3/35.9/24.4/17.2 (BP=1.000, ratio=1.070, hyp_len=12228, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.58.0.86-2.37.0.67-1.95.1.61-4.98.1.28-3.60.pth, bkmy
BLEU = 35.47, 60.9/41.1/29.2/21.7 (BP=1.000, ratio=1.097, hyp_len=13416, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.59.0.74-2.09.0.61-1.84.1.59-4.91.1.26-3.54.pth, mybk
BLEU = 31.04, 58.8/36.8/24.8/17.3 (BP=1.000, ratio=1.069, hyp_len=12216, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.59.0.74-2.09.0.61-1.84.1.59-4.91.1.26-3.54.pth, bkmy
BLEU = 37.46, 63.1/43.2/31.0/23.3 (BP=1.000, ratio=1.057, hyp_len=12929, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.60.0.74-2.09.0.59-1.81.1.61-5.00.1.31-3.70.pth, mybk
BLEU = 31.70, 58.7/37.4/25.3/18.2 (BP=1.000, ratio=1.063, hyp_len=12149, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.60.0.74-2.09.0.59-1.81.1.61-5.00.1.31-3.70.pth, bkmy
BLEU = 36.20, 62.1/41.9/29.8/22.2 (BP=1.000, ratio=1.066, hyp_len=13042, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.61.0.72-2.06.0.60-1.82.1.65-5.23.1.28-3.60.pth, mybk
BLEU = 30.42, 57.1/35.9/24.3/17.2 (BP=1.000, ratio=1.089, hyp_len=12451, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.61.0.72-2.06.0.60-1.82.1.65-5.23.1.28-3.60.pth, bkmy
BLEU = 37.09, 62.5/42.9/30.8/22.9 (BP=1.000, ratio=1.078, hyp_len=13181, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.62.0.74-2.09.0.61-1.84.1.67-5.33.1.33-3.77.pth, mybk
BLEU = 31.07, 57.9/36.5/24.8/17.8 (BP=1.000, ratio=1.058, hyp_len=12096, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.62.0.74-2.09.0.61-1.84.1.67-5.33.1.33-3.77.pth, bkmy
BLEU = 35.53, 61.2/41.2/29.2/21.7 (BP=1.000, ratio=1.056, hyp_len=12921, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.63.0.76-2.15.0.61-1.84.1.66-5.26.1.29-3.62.pth, mybk
BLEU = 31.60, 58.2/37.0/25.3/18.3 (BP=1.000, ratio=1.071, hyp_len=12239, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.63.0.76-2.15.0.61-1.84.1.66-5.26.1.29-3.62.pth, bkmy
BLEU = 36.27, 61.7/42.1/29.9/22.2 (BP=1.000, ratio=1.078, hyp_len=13184, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.64.0.81-2.24.0.64-1.89.1.69-5.41.1.30-3.68.pth, mybk
BLEU = 31.10, 57.9/36.5/24.9/17.8 (BP=1.000, ratio=1.066, hyp_len=12190, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.64.0.81-2.24.0.64-1.89.1.69-5.41.1.30-3.68.pth, bkmy
BLEU = 36.04, 62.0/41.8/29.7/21.9 (BP=1.000, ratio=1.069, hyp_len=13080, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.65.0.73-2.07.0.62-1.86.1.68-5.39.1.38-3.98.pth, mybk
BLEU = 30.52, 57.2/36.0/24.4/17.2 (BP=1.000, ratio=1.080, hyp_len=12346, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.65.0.73-2.07.0.62-1.86.1.68-5.39.1.38-3.98.pth, bkmy
BLEU = 34.65, 60.4/40.6/28.4/20.7 (BP=1.000, ratio=1.079, hyp_len=13192, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.66.0.70-2.02.0.57-1.77.1.64-5.17.1.33-3.77.pth, mybk
BLEU = 30.16, 57.4/35.8/24.0/16.7 (BP=1.000, ratio=1.079, hyp_len=12333, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.66.0.70-2.02.0.57-1.77.1.64-5.17.1.33-3.77.pth, bkmy
BLEU = 35.39, 61.3/41.0/29.0/21.4 (BP=1.000, ratio=1.066, hyp_len=13043, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.67.0.77-2.17.0.62-1.85.1.70-5.45.1.34-3.84.pth, mybk
BLEU = 30.57, 57.0/35.7/24.4/17.6 (BP=1.000, ratio=1.074, hyp_len=12274, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.67.0.77-2.17.0.62-1.85.1.70-5.45.1.34-3.84.pth, bkmy
BLEU = 36.06, 61.4/41.7/29.8/22.2 (BP=1.000, ratio=1.059, hyp_len=12954, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.68.0.79-2.20.0.59-1.81.1.70-5.49.1.34-3.84.pth, mybk
BLEU = 29.30, 56.1/34.7/23.2/16.3 (BP=1.000, ratio=1.077, hyp_len=12307, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.68.0.79-2.20.0.59-1.81.1.70-5.49.1.34-3.84.pth, bkmy
BLEU = 35.07, 60.6/40.8/28.8/21.2 (BP=1.000, ratio=1.084, hyp_len=13259, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.69.0.68-1.97.0.55-1.74.1.73-5.62.1.33-3.77.pth, mybk
BLEU = 30.47, 57.7/36.1/24.2/17.1 (BP=1.000, ratio=1.068, hyp_len=12215, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.69.0.68-1.97.0.55-1.74.1.73-5.62.1.33-3.77.pth, bkmy
BLEU = 37.19, 62.6/42.8/30.8/23.2 (BP=1.000, ratio=1.061, hyp_len=12976, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.70.0.67-1.96.0.55-1.73.1.73-5.66.1.33-3.80.pth, mybk
BLEU = 30.27, 57.1/35.9/24.1/17.0 (BP=1.000, ratio=1.072, hyp_len=12250, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.70.0.67-1.96.0.55-1.73.1.73-5.66.1.33-3.80.pth, bkmy
BLEU = 34.98, 61.0/40.6/28.7/21.1 (BP=1.000, ratio=1.075, hyp_len=13143, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.71.0.68-1.98.0.57-1.78.1.70-5.47.1.32-3.76.pth, mybk
BLEU = 30.86, 57.5/36.1/24.6/17.8 (BP=1.000, ratio=1.077, hyp_len=12313, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.71.0.68-1.98.0.57-1.78.1.70-5.47.1.32-3.76.pth, bkmy
BLEU = 34.14, 59.9/39.8/27.8/20.4 (BP=1.000, ratio=1.105, hyp_len=13521, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.72.0.65-1.92.0.52-1.69.1.74-5.72.1.36-3.89.pth, mybk
BLEU = 30.48, 56.7/35.7/24.4/17.5 (BP=1.000, ratio=1.054, hyp_len=12055, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.72.0.65-1.92.0.52-1.69.1.74-5.72.1.36-3.89.pth, bkmy
BLEU = 33.28, 58.6/38.9/27.2/19.8 (BP=1.000, ratio=1.114, hyp_len=13630, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.73.0.65-1.91.0.51-1.67.1.71-5.53.1.35-3.87.pth, mybk
BLEU = 31.84, 59.5/37.3/25.4/18.2 (BP=1.000, ratio=1.040, hyp_len=11886, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.73.0.65-1.91.0.51-1.67.1.71-5.53.1.35-3.87.pth, bkmy
BLEU = 35.62, 60.7/41.2/29.4/21.9 (BP=1.000, ratio=1.079, hyp_len=13196, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.74.0.63-1.87.0.51-1.67.1.75-5.73.1.38-3.99.pth, mybk
BLEU = 28.90, 55.0/34.0/23.0/16.2 (BP=1.000, ratio=1.100, hyp_len=12578, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.74.0.63-1.87.0.51-1.67.1.75-5.73.1.38-3.99.pth, bkmy
BLEU = 34.59, 60.0/40.2/28.4/20.9 (BP=1.000, ratio=1.079, hyp_len=13197, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.75.0.67-1.95.0.58-1.79.1.75-5.78.1.36-3.91.pth, mybk
BLEU = 31.41, 58.7/37.0/25.0/17.9 (BP=1.000, ratio=1.031, hyp_len=11783, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.75.0.67-1.95.0.58-1.79.1.75-5.78.1.36-3.91.pth, bkmy
BLEU = 35.84, 61.6/41.6/29.4/21.9 (BP=1.000, ratio=1.058, hyp_len=12938, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.76.0.63-1.88.0.51-1.66.1.73-5.63.1.38-3.96.pth, mybk
BLEU = 29.37, 56.1/34.7/23.2/16.4 (BP=1.000, ratio=1.077, hyp_len=12308, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.76.0.63-1.88.0.51-1.66.1.73-5.63.1.38-3.96.pth, bkmy
BLEU = 33.77, 58.9/39.0/27.6/20.5 (BP=1.000, ratio=1.091, hyp_len=13350, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.77.0.61-1.84.0.49-1.62.1.75-5.75.1.38-3.97.pth, mybk
BLEU = 30.91, 57.7/36.3/24.7/17.7 (BP=1.000, ratio=1.087, hyp_len=12421, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.77.0.61-1.84.0.49-1.62.1.75-5.75.1.38-3.97.pth, bkmy
BLEU = 34.51, 59.7/40.1/28.2/21.0 (BP=1.000, ratio=1.088, hyp_len=13305, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.78.0.62-1.87.0.51-1.66.1.76-5.81.1.40-4.05.pth, mybk
BLEU = 28.44, 55.3/33.7/22.3/15.7 (BP=1.000, ratio=1.074, hyp_len=12278, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.78.0.62-1.87.0.51-1.66.1.76-5.81.1.40-4.05.pth, bkmy
BLEU = 35.38, 60.6/40.9/29.1/21.7 (BP=1.000, ratio=1.063, hyp_len=12997, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.79.0.60-1.82.0.49-1.62.1.76-5.82.1.38-3.98.pth, mybk
BLEU = 31.13, 58.0/36.5/24.9/17.8 (BP=1.000, ratio=1.072, hyp_len=12256, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.79.0.60-1.82.0.49-1.62.1.76-5.82.1.38-3.98.pth, bkmy
BLEU = 33.92, 59.5/39.7/27.7/20.2 (BP=1.000, ratio=1.103, hyp_len=13489, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.80.0.61-1.83.0.51-1.66.1.77-5.89.1.42-4.13.pth, mybk
BLEU = 29.18, 56.0/34.2/23.1/16.4 (BP=1.000, ratio=1.068, hyp_len=12209, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.80.0.61-1.83.0.51-1.66.1.77-5.89.1.42-4.13.pth, bkmy
BLEU = 34.57, 59.9/40.2/28.3/20.9 (BP=1.000, ratio=1.071, hyp_len=13098, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.81.0.62-1.86.0.50-1.66.1.75-5.73.1.41-4.11.pth, mybk
BLEU = 31.73, 58.0/36.9/25.6/18.5 (BP=1.000, ratio=1.039, hyp_len=11878, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.81.0.62-1.86.0.50-1.66.1.75-5.73.1.41-4.11.pth, bkmy
BLEU = 34.43, 59.5/39.8/28.3/21.0 (BP=1.000, ratio=1.090, hyp_len=13334, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.82.0.67-1.96.0.52-1.67.1.74-5.70.1.42-4.15.pth, mybk
BLEU = 29.48, 56.2/35.0/23.4/16.4 (BP=1.000, ratio=1.075, hyp_len=12290, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.82.0.67-1.96.0.52-1.67.1.74-5.70.1.42-4.15.pth, bkmy
BLEU = 33.87, 58.5/38.9/27.8/20.8 (BP=1.000, ratio=1.080, hyp_len=13205, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.83.0.65-1.92.0.51-1.66.1.76-5.83.1.42-4.13.pth, mybk
BLEU = 29.60, 56.9/34.9/23.5/16.5 (BP=1.000, ratio=1.042, hyp_len=11917, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.83.0.65-1.92.0.51-1.66.1.76-5.83.1.42-4.13.pth, bkmy
BLEU = 34.22, 59.8/39.9/28.0/20.6 (BP=1.000, ratio=1.074, hyp_len=13139, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.84.0.57-1.77.0.48-1.61.1.77-5.87.1.45-4.25.pth, mybk
BLEU = 29.59, 56.3/34.9/23.5/16.6 (BP=1.000, ratio=1.082, hyp_len=12368, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.84.0.57-1.77.0.48-1.61.1.77-5.87.1.45-4.25.pth, bkmy
BLEU = 33.70, 58.9/39.0/27.5/20.4 (BP=1.000, ratio=1.077, hyp_len=13174, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.85.0.56-1.75.0.45-1.57.1.78-5.95.1.44-4.21.pth, mybk
BLEU = 29.13, 55.4/34.6/23.2/16.2 (BP=1.000, ratio=1.097, hyp_len=12542, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.85.0.56-1.75.0.45-1.57.1.78-5.95.1.44-4.21.pth, bkmy
BLEU = 34.23, 58.9/39.2/28.3/21.0 (BP=1.000, ratio=1.081, hyp_len=13227, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.86.0.58-1.79.0.47-1.60.1.82-6.15.1.42-4.13.pth, mybk
BLEU = 30.25, 57.0/35.5/24.2/17.1 (BP=1.000, ratio=1.073, hyp_len=12263, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.86.0.58-1.79.0.47-1.60.1.82-6.15.1.42-4.13.pth, bkmy
BLEU = 34.89, 59.7/40.1/28.7/21.5 (BP=1.000, ratio=1.074, hyp_len=13131, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.87.0.59-1.80.0.49-1.64.1.85-6.36.1.48-4.39.pth, mybk
BLEU = 29.64, 55.7/35.0/23.7/16.7 (BP=1.000, ratio=1.074, hyp_len=12281, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.87.0.59-1.80.0.49-1.64.1.85-6.36.1.48-4.39.pth, bkmy
BLEU = 32.75, 57.7/38.1/26.7/19.6 (BP=1.000, ratio=1.094, hyp_len=13376, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.88.0.58-1.79.0.47-1.59.1.84-6.31.1.44-4.20.pth, mybk
BLEU = 29.85, 56.7/35.1/23.7/16.8 (BP=1.000, ratio=1.058, hyp_len=12094, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.88.0.58-1.79.0.47-1.59.1.84-6.31.1.44-4.20.pth, bkmy
BLEU = 32.88, 58.1/38.4/26.7/19.6 (BP=1.000, ratio=1.084, hyp_len=13261, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.89.0.59-1.80.0.49-1.62.1.82-6.17.1.47-4.35.pth, mybk
BLEU = 29.50, 55.4/34.6/23.5/16.8 (BP=1.000, ratio=1.098, hyp_len=12550, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.89.0.59-1.80.0.49-1.62.1.82-6.17.1.47-4.35.pth, bkmy
BLEU = 31.71, 56.7/37.3/25.8/18.5 (BP=1.000, ratio=1.134, hyp_len=13866, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.90.0.60-1.82.0.49-1.63.1.82-6.15.1.45-4.26.pth, mybk
BLEU = 29.34, 55.9/34.5/23.4/16.4 (BP=1.000, ratio=1.072, hyp_len=12258, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.90.0.60-1.82.0.49-1.63.1.82-6.15.1.45-4.26.pth, bkmy
BLEU = 34.76, 59.7/40.0/28.5/21.4 (BP=1.000, ratio=1.074, hyp_len=13142, ref_len=12231)
```

Best model for my-bk က epoch 26 မော်ဒယ် ဖြစ်ပြီးတော့၊ Best BLEU Score က : 34.77   
Best model for bk-my က epoch 27 မော်ဒယ် ဖြစ်ပြီးတော့၊ Best BLEU Score က : 41.79    

## Transformer-DSL, 100 epoch

```
Epoch 1 - |param|=8.53e+02 |g_param|=2.41e+05 loss_x2y=4.4553e+00 ppl_x2y=86.08 loss_y2x=4.1102e+00 ppl_y2x=60.96 dual_loss=0.0000e+00
Validation X2Y - loss=3.4363e+00 ppl=31.07 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=3.1307e+00 ppl=22.89 best_loss=inf best_ppl=inf
Epoch 2 - |param|=8.54e+02 |g_param|=2.22e+05 loss_x2y=3.6879e+00 ppl_x2y=39.96 loss_y2x=3.2951e+00 ppl_y2x=26.98 dual_loss=0.0000e+00
Validation X2Y - loss=2.9898e+00 ppl=19.88 best_loss=3.4363e+00 best_ppl=31.07                                          
Validation Y2X - loss=2.6620e+00 ppl=14.33 best_loss=3.1307e+00 best_ppl=22.89
Epoch 3 - |param|=8.54e+02 |g_param|=1.98e+05 loss_x2y=3.2115e+00 ppl_x2y=24.82 loss_y2x=2.8254e+00 ppl_y2x=16.87 dual_loss=0.0000e+00
Validation X2Y - loss=2.4953e+00 ppl=12.12 best_loss=2.9898e+00 best_ppl=19.88                                          
Validation Y2X - loss=2.2753e+00 ppl=9.73 best_loss=2.6620e+00 best_ppl=14.33
Epoch 4 - |param|=8.55e+02 |g_param|=2.23e+05 loss_x2y=3.0085e+00 ppl_x2y=20.26 loss_y2x=2.6518e+00 ppl_y2x=14.18 dual_loss=0.0000e+00
Validation X2Y - loss=2.2915e+00 ppl=9.89 best_loss=2.4953e+00 best_ppl=12.12                                           
Validation Y2X - loss=2.0525e+00 ppl=7.79 best_loss=2.2753e+00 best_ppl=9.73
Epoch 5 - |param|=8.56e+02 |g_param|=2.22e+05 loss_x2y=2.7328e+00 ppl_x2y=15.38 loss_y2x=2.3572e+00 ppl_y2x=10.56 dual_loss=0.0000e+00
Validation X2Y - loss=1.9903e+00 ppl=7.32 best_loss=2.2915e+00 best_ppl=9.89                                            
Validation Y2X - loss=1.7945e+00 ppl=6.02 best_loss=2.0525e+00 best_ppl=7.79
Epoch 6 - |param|=8.56e+02 |g_param|=2.34e+05 loss_x2y=2.5792e+00 ppl_x2y=13.19 loss_y2x=2.2602e+00 ppl_y2x=9.58 dual_loss=0.0000e+00
Validation X2Y - loss=1.8005e+00 ppl=6.05 best_loss=1.9903e+00 best_ppl=7.32                                            
Validation Y2X - loss=1.6138e+00 ppl=5.02 best_loss=1.7945e+00 best_ppl=6.02
Epoch 7 - |param|=8.57e+02 |g_param|=2.42e+05 loss_x2y=2.4262e+00 ppl_x2y=11.32 loss_y2x=2.1026e+00 ppl_y2x=8.19 dual_loss=0.0000e+00
Validation X2Y - loss=1.6617e+00 ppl=5.27 best_loss=1.8005e+00 best_ppl=6.05                                            
Validation Y2X - loss=1.4918e+00 ppl=4.44 best_loss=1.6138e+00 best_ppl=5.02
Epoch 8 - |param|=8.57e+02 |g_param|=2.65e+05 loss_x2y=2.3312e+00 ppl_x2y=10.29 loss_y2x=2.0034e+00 ppl_y2x=7.41 dual_loss=0.0000e+00
Validation X2Y - loss=1.5045e+00 ppl=4.50 best_loss=1.6617e+00 best_ppl=5.27                                            
Validation Y2X - loss=1.3735e+00 ppl=3.95 best_loss=1.4918e+00 best_ppl=4.44
Epoch 9 - |param|=8.58e+02 |g_param|=2.57e+05 loss_x2y=2.2958e+00 ppl_x2y=9.93 loss_y2x=1.9874e+00 ppl_y2x=7.30 dual_loss=0.0000e+00
Validation X2Y - loss=1.4798e+00 ppl=4.39 best_loss=1.5045e+00 best_ppl=4.50                                            
Validation Y2X - loss=1.2993e+00 ppl=3.67 best_loss=1.3735e+00 best_ppl=3.95
Epoch 10 - |param|=8.58e+02 |g_param|=2.82e+05 loss_x2y=2.0997e+00 ppl_x2y=8.16 loss_y2x=1.8250e+00 ppl_y2x=6.20 dual_loss=0.0000e+00
Validation X2Y - loss=1.4084e+00 ppl=4.09 best_loss=1.4798e+00 best_ppl=4.39                                            
Validation Y2X - loss=1.2034e+00 ppl=3.33 best_loss=1.2993e+00 best_ppl=3.67
Epoch 11 - |param|=8.59e+02 |g_param|=2.70e+05 loss_x2y=1.9933e+00 ppl_x2y=7.34 loss_y2x=1.7262e+00 ppl_y2x=5.62 dual_loss=0.0000e+00
Validation X2Y - loss=1.3575e+00 ppl=3.89 best_loss=1.4084e+00 best_ppl=4.09                                            
Validation Y2X - loss=1.1895e+00 ppl=3.29 best_loss=1.2034e+00 best_ppl=3.33
Epoch 12 - |param|=8.60e+02 |g_param|=3.00e+05 loss_x2y=1.9468e+00 ppl_x2y=7.01 loss_y2x=1.6837e+00 ppl_y2x=5.39 dual_loss=0.0000e+00
Validation X2Y - loss=1.3143e+00 ppl=3.72 best_loss=1.3575e+00 best_ppl=3.89                                            
Validation Y2X - loss=1.1302e+00 ppl=3.10 best_loss=1.1895e+00 best_ppl=3.29
Epoch 13 - |param|=8.60e+02 |g_param|=2.90e+05 loss_x2y=1.9081e+00 ppl_x2y=6.74 loss_y2x=1.6277e+00 ppl_y2x=5.09 dual_loss=0.0000e+00
Validation X2Y - loss=1.2547e+00 ppl=3.51 best_loss=1.3143e+00 best_ppl=3.72                                            
Validation Y2X - loss=1.0768e+00 ppl=2.94 best_loss=1.1302e+00 best_ppl=3.10
Epoch 14 - |param|=8.61e+02 |g_param|=3.15e+05 loss_x2y=1.8706e+00 ppl_x2y=6.49 loss_y2x=1.5900e+00 ppl_y2x=4.90 dual_loss=0.0000e+00
Validation X2Y - loss=1.2729e+00 ppl=3.57 best_loss=1.2547e+00 best_ppl=3.51                                            
Validation Y2X - loss=1.0947e+00 ppl=2.99 best_loss=1.0768e+00 best_ppl=2.94
Epoch 15 - |param|=8.61e+02 |g_param|=3.03e+05 loss_x2y=1.7107e+00 ppl_x2y=5.53 loss_y2x=1.4640e+00 ppl_y2x=4.32 dual_loss=0.0000e+00
Validation X2Y - loss=1.2246e+00 ppl=3.40 best_loss=1.2547e+00 best_ppl=3.51                                            
Validation Y2X - loss=1.0644e+00 ppl=2.90 best_loss=1.0768e+00 best_ppl=2.94
Epoch 16 - |param|=8.62e+02 |g_param|=3.37e+05 loss_x2y=1.6955e+00 ppl_x2y=5.45 loss_y2x=1.4624e+00 ppl_y2x=4.32 dual_loss=0.0000e+00
Validation X2Y - loss=1.2504e+00 ppl=3.49 best_loss=1.2246e+00 best_ppl=3.40                                            
Validation Y2X - loss=1.0590e+00 ppl=2.88 best_loss=1.0644e+00 best_ppl=2.90
Epoch 17 - |param|=8.62e+02 |g_param|=3.33e+05 loss_x2y=1.7447e+00 ppl_x2y=5.72 loss_y2x=1.4545e+00 ppl_y2x=4.28 dual_loss=0.0000e+00
Validation X2Y - loss=1.2700e+00 ppl=3.56 best_loss=1.2246e+00 best_ppl=3.40                                            
Validation Y2X - loss=1.0439e+00 ppl=2.84 best_loss=1.0590e+00 best_ppl=2.88
Epoch 18 - |param|=8.63e+02 |g_param|=3.62e+05 loss_x2y=1.6748e+00 ppl_x2y=5.34 loss_y2x=1.4715e+00 ppl_y2x=4.36 dual_loss=0.0000e+00
Validation X2Y - loss=1.2558e+00 ppl=3.51 best_loss=1.2246e+00 best_ppl=3.40                                            
Validation Y2X - loss=1.0745e+00 ppl=2.93 best_loss=1.0439e+00 best_ppl=2.84
Epoch 19 - |param|=8.63e+02 |g_param|=3.31e+05 loss_x2y=1.5511e+00 ppl_x2y=4.72 loss_y2x=1.3405e+00 ppl_y2x=3.82 dual_loss=0.0000e+00
Validation X2Y - loss=1.2296e+00 ppl=3.42 best_loss=1.2246e+00 best_ppl=3.40                                            
Validation Y2X - loss=1.0557e+00 ppl=2.87 best_loss=1.0439e+00 best_ppl=2.84
Epoch 20 - |param|=8.64e+02 |g_param|=3.59e+05 loss_x2y=1.5462e+00 ppl_x2y=4.69 loss_y2x=1.3183e+00 ppl_y2x=3.74 dual_loss=0.0000e+00
Validation X2Y - loss=1.2753e+00 ppl=3.58 best_loss=1.2246e+00 best_ppl=3.40                                            
Validation Y2X - loss=1.0659e+00 ppl=2.90 best_loss=1.0439e+00 best_ppl=2.84
Epoch 21 - |param|=8.64e+02 |g_param|=3.29e+05 loss_x2y=1.4610e+00 ppl_x2y=4.31 loss_y2x=1.2326e+00 ppl_y2x=3.43 dual_loss=5.5161e-01
Validation X2Y - loss=1.2590e+00 ppl=3.52 best_loss=1.2246e+00 best_ppl=3.40                                            
Validation Y2X - loss=1.0659e+00 ppl=2.90 best_loss=1.0439e+00 best_ppl=2.84
Epoch 22 - |param|=8.65e+02 |g_param|=3.57e+05 loss_x2y=1.4087e+00 ppl_x2y=4.09 loss_y2x=1.1885e+00 ppl_y2x=3.28 dual_loss=5.0429e-01
Validation X2Y - loss=1.2628e+00 ppl=3.54 best_loss=1.2246e+00 best_ppl=3.40                                            
Validation Y2X - loss=1.0424e+00 ppl=2.84 best_loss=1.0439e+00 best_ppl=2.84
Epoch 23 - |param|=8.65e+02 |g_param|=3.58e+05 loss_x2y=1.4600e+00 ppl_x2y=4.31 loss_y2x=1.2494e+00 ppl_y2x=3.49 dual_loss=5.4245e-01
Validation X2Y - loss=1.2598e+00 ppl=3.52 best_loss=1.2246e+00 best_ppl=3.40                                            
Validation Y2X - loss=1.0372e+00 ppl=2.82 best_loss=1.0424e+00 best_ppl=2.84
Epoch 24 - |param|=8.66e+02 |g_param|=3.64e+05 loss_x2y=1.3992e+00 ppl_x2y=4.05 loss_y2x=1.2088e+00 ppl_y2x=3.35 dual_loss=5.4061e-01
Validation X2Y - loss=1.2558e+00 ppl=3.51 best_loss=1.2246e+00 best_ppl=3.40                                            
Validation Y2X - loss=1.0541e+00 ppl=2.87 best_loss=1.0372e+00 best_ppl=2.82
Epoch 25 - |param|=8.67e+02 |g_param|=3.55e+05 loss_x2y=1.3391e+00 ppl_x2y=3.82 loss_y2x=1.1505e+00 ppl_y2x=3.16 dual_loss=4.8663e-01
Validation X2Y - loss=1.2214e+00 ppl=3.39 best_loss=1.2246e+00 best_ppl=3.40                                            
Validation Y2X - loss=1.0560e+00 ppl=2.87 best_loss=1.0372e+00 best_ppl=2.82
Epoch 26 - |param|=8.67e+02 |g_param|=3.88e+05 loss_x2y=1.3340e+00 ppl_x2y=3.80 loss_y2x=1.1745e+00 ppl_y2x=3.24 dual_loss=5.5902e-01
Validation X2Y - loss=1.2459e+00 ppl=3.48 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.0724e+00 ppl=2.92 best_loss=1.0372e+00 best_ppl=2.82
Epoch 27 - |param|=8.68e+02 |g_param|=3.52e+05 loss_x2y=1.2824e+00 ppl_x2y=3.61 loss_y2x=1.0645e+00 ppl_y2x=2.90 dual_loss=5.0454e-01
Validation X2Y - loss=1.2753e+00 ppl=3.58 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.0531e+00 ppl=2.87 best_loss=1.0372e+00 best_ppl=2.82
Epoch 28 - |param|=8.68e+02 |g_param|=3.88e+05 loss_x2y=1.3454e+00 ppl_x2y=3.84 loss_y2x=1.1326e+00 ppl_y2x=3.10 dual_loss=5.6129e-01
Validation X2Y - loss=1.2764e+00 ppl=3.58 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.0860e+00 ppl=2.96 best_loss=1.0372e+00 best_ppl=2.82
Epoch 29 - |param|=8.69e+02 |g_param|=3.60e+05 loss_x2y=1.2072e+00 ppl_x2y=3.34 loss_y2x=1.0062e+00 ppl_y2x=2.74 dual_loss=4.9285e-01
Validation X2Y - loss=1.2688e+00 ppl=3.56 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1018e+00 ppl=3.01 best_loss=1.0372e+00 best_ppl=2.82
Epoch 30 - |param|=8.69e+02 |g_param|=3.91e+05 loss_x2y=1.2030e+00 ppl_x2y=3.33 loss_y2x=1.0136e+00 ppl_y2x=2.76 dual_loss=5.3924e-01
Validation X2Y - loss=1.2947e+00 ppl=3.65 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.0717e+00 ppl=2.92 best_loss=1.0372e+00 best_ppl=2.82
Epoch 31 - |param|=8.70e+02 |g_param|=3.86e+05 loss_x2y=1.2063e+00 ppl_x2y=3.34 loss_y2x=1.0016e+00 ppl_y2x=2.72 dual_loss=5.8669e-01
Validation X2Y - loss=1.3053e+00 ppl=3.69 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.0962e+00 ppl=2.99 best_loss=1.0372e+00 best_ppl=2.82
Epoch 32 - |param|=8.70e+02 |g_param|=3.96e+05 loss_x2y=1.1290e+00 ppl_x2y=3.09 loss_y2x=9.3982e-01 ppl_y2x=2.56 dual_loss=5.5659e-01
Validation X2Y - loss=1.3438e+00 ppl=3.83 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1199e+00 ppl=3.06 best_loss=1.0372e+00 best_ppl=2.82
Epoch 33 - |param|=8.71e+02 |g_param|=6.12e+05 loss_x2y=1.1508e+00 ppl_x2y=3.16 loss_y2x=9.5053e-01 ppl_y2x=2.59 dual_loss=5.6814e-01
Validation X2Y - loss=1.3688e+00 ppl=3.93 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1103e+00 ppl=3.04 best_loss=1.0372e+00 best_ppl=2.82
Epoch 34 - |param|=8.71e+02 |g_param|=7.92e+05 loss_x2y=1.1038e+00 ppl_x2y=3.02 loss_y2x=9.1356e-01 ppl_y2x=2.49 dual_loss=5.8248e-01
Validation X2Y - loss=1.3584e+00 ppl=3.89 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1284e+00 ppl=3.09 best_loss=1.0372e+00 best_ppl=2.82
Epoch 35 - |param|=8.72e+02 |g_param|=7.62e+05 loss_x2y=1.1625e+00 ppl_x2y=3.20 loss_y2x=9.3504e-01 ppl_y2x=2.55 dual_loss=6.5835e-01
Validation X2Y - loss=1.3639e+00 ppl=3.91 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1428e+00 ppl=3.14 best_loss=1.0372e+00 best_ppl=2.82
Epoch 36 - |param|=8.72e+02 |g_param|=8.10e+05 loss_x2y=1.0755e+00 ppl_x2y=2.93 loss_y2x=9.3279e-01 ppl_y2x=2.54 dual_loss=6.7729e-01
Validation X2Y - loss=1.3707e+00 ppl=3.94 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1399e+00 ppl=3.13 best_loss=1.0372e+00 best_ppl=2.82
Epoch 37 - |param|=8.73e+02 |g_param|=7.95e+05 loss_x2y=1.0337e+00 ppl_x2y=2.81 loss_y2x=8.8529e-01 ppl_y2x=2.42 dual_loss=7.0702e-01
Validation X2Y - loss=1.3912e+00 ppl=4.02 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1249e+00 ppl=3.08 best_loss=1.0372e+00 best_ppl=2.82
Epoch 38 - |param|=8.73e+02 |g_param|=8.01e+05 loss_x2y=1.0203e+00 ppl_x2y=2.77 loss_y2x=8.5282e-01 ppl_y2x=2.35 dual_loss=6.0117e-01
Validation X2Y - loss=1.4009e+00 ppl=4.06 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1461e+00 ppl=3.15 best_loss=1.0372e+00 best_ppl=2.82
Epoch 39 - |param|=8.74e+02 |g_param|=7.77e+05 loss_x2y=1.0491e+00 ppl_x2y=2.85 loss_y2x=8.5082e-01 ppl_y2x=2.34 dual_loss=6.5877e-01
Validation X2Y - loss=1.4533e+00 ppl=4.28 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1530e+00 ppl=3.17 best_loss=1.0372e+00 best_ppl=2.82
Epoch 40 - |param|=8.74e+02 |g_param|=8.04e+05 loss_x2y=9.8785e-01 ppl_x2y=2.69 loss_y2x=8.1649e-01 ppl_y2x=2.26 dual_loss=6.3095e-01
Validation X2Y - loss=1.4456e+00 ppl=4.24 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1302e+00 ppl=3.10 best_loss=1.0372e+00 best_ppl=2.82
Epoch 41 - |param|=8.75e+02 |g_param|=8.04e+05 loss_x2y=9.9888e-01 ppl_x2y=2.72 loss_y2x=8.5952e-01 ppl_y2x=2.36 dual_loss=6.9181e-01
Validation X2Y - loss=1.4372e+00 ppl=4.21 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1327e+00 ppl=3.10 best_loss=1.0372e+00 best_ppl=2.82
Epoch 42 - |param|=8.75e+02 |g_param|=8.41e+05 loss_x2y=9.7841e-01 ppl_x2y=2.66 loss_y2x=8.0396e-01 ppl_y2x=2.23 dual_loss=6.6720e-01
Validation X2Y - loss=1.4004e+00 ppl=4.06 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1629e+00 ppl=3.20 best_loss=1.0372e+00 best_ppl=2.82
Epoch 43 - |param|=8.76e+02 |g_param|=7.69e+05 loss_x2y=9.1915e-01 ppl_x2y=2.51 loss_y2x=7.5285e-01 ppl_y2x=2.12 dual_loss=6.4413e-01
Validation X2Y - loss=1.4132e+00 ppl=4.11 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1725e+00 ppl=3.23 best_loss=1.0372e+00 best_ppl=2.82
Epoch 44 - |param|=8.76e+02 |g_param|=8.17e+05 loss_x2y=9.4350e-01 ppl_x2y=2.57 loss_y2x=7.7103e-01 ppl_y2x=2.16 dual_loss=7.1306e-01
Validation X2Y - loss=1.4390e+00 ppl=4.22 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1885e+00 ppl=3.28 best_loss=1.0372e+00 best_ppl=2.82
Epoch 45 - |param|=8.77e+02 |g_param|=7.95e+05 loss_x2y=9.0476e-01 ppl_x2y=2.47 loss_y2x=7.4101e-01 ppl_y2x=2.10 dual_loss=6.6844e-01
Validation X2Y - loss=1.4722e+00 ppl=4.36 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1778e+00 ppl=3.25 best_loss=1.0372e+00 best_ppl=2.82
Epoch 46 - |param|=8.77e+02 |g_param|=8.25e+05 loss_x2y=9.0064e-01 ppl_x2y=2.46 loss_y2x=7.4263e-01 ppl_y2x=2.10 dual_loss=7.0640e-01
Validation X2Y - loss=1.4783e+00 ppl=4.39 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1885e+00 ppl=3.28 best_loss=1.0372e+00 best_ppl=2.82
Epoch 47 - |param|=8.78e+02 |g_param|=8.13e+05 loss_x2y=9.0342e-01 ppl_x2y=2.47 loss_y2x=7.4501e-01 ppl_y2x=2.11 dual_loss=7.8945e-01
Validation X2Y - loss=1.5046e+00 ppl=4.50 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.1865e+00 ppl=3.28 best_loss=1.0372e+00 best_ppl=2.82
Epoch 48 - |param|=8.78e+02 |g_param|=8.31e+05 loss_x2y=9.4621e-01 ppl_x2y=2.58 loss_y2x=7.4260e-01 ppl_y2x=2.10 dual_loss=8.6962e-01
Validation X2Y - loss=1.4911e+00 ppl=4.44 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.2552e+00 ppl=3.51 best_loss=1.0372e+00 best_ppl=2.82
Epoch 49 - |param|=8.79e+02 |g_param|=8.16e+05 loss_x2y=8.8796e-01 ppl_x2y=2.43 loss_y2x=7.4280e-01 ppl_y2x=2.10 dual_loss=8.0018e-01
Validation X2Y - loss=1.4737e+00 ppl=4.37 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.2396e+00 ppl=3.45 best_loss=1.0372e+00 best_ppl=2.82
Epoch 50 - |param|=8.79e+02 |g_param|=8.63e+05 loss_x2y=8.9625e-01 ppl_x2y=2.45 loss_y2x=7.2765e-01 ppl_y2x=2.07 dual_loss=8.9333e-01
Validation X2Y - loss=1.4943e+00 ppl=4.46 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.2407e+00 ppl=3.46 best_loss=1.0372e+00 best_ppl=2.82
Epoch 51 - |param|=8.80e+02 |g_param|=8.04e+05 loss_x2y=8.3504e-01 ppl_x2y=2.30 loss_y2x=6.7626e-01 ppl_y2x=1.97 dual_loss=7.9208e-01
Validation X2Y - loss=1.5122e+00 ppl=4.54 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.2850e+00 ppl=3.61 best_loss=1.0372e+00 best_ppl=2.82
Epoch 52 - |param|=8.80e+02 |g_param|=8.07e+05 loss_x2y=8.0862e-01 ppl_x2y=2.24 loss_y2x=6.6782e-01 ppl_y2x=1.95 dual_loss=7.6667e-01
Validation X2Y - loss=1.5062e+00 ppl=4.51 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.2781e+00 ppl=3.59 best_loss=1.0372e+00 best_ppl=2.82
Epoch 53 - |param|=8.81e+02 |g_param|=7.87e+05 loss_x2y=7.9554e-01 ppl_x2y=2.22 loss_y2x=6.4707e-01 ppl_y2x=1.91 dual_loss=7.7780e-01
Validation X2Y - loss=1.5112e+00 ppl=4.53 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.2668e+00 ppl=3.55 best_loss=1.0372e+00 best_ppl=2.82
Epoch 54 - |param|=8.81e+02 |g_param|=8.24e+05 loss_x2y=8.0194e-01 ppl_x2y=2.23 loss_y2x=6.6588e-01 ppl_y2x=1.95 dual_loss=8.4501e-01
Validation X2Y - loss=1.5230e+00 ppl=4.59 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.2264e+00 ppl=3.41 best_loss=1.0372e+00 best_ppl=2.82
Epoch 55 - |param|=8.82e+02 |g_param|=7.88e+05 loss_x2y=7.7702e-01 ppl_x2y=2.17 loss_y2x=6.2143e-01 ppl_y2x=1.86 dual_loss=7.7651e-01
Validation X2Y - loss=1.5636e+00 ppl=4.78 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.2717e+00 ppl=3.57 best_loss=1.0372e+00 best_ppl=2.82
Epoch 56 - |param|=8.82e+02 |g_param|=8.25e+05 loss_x2y=7.9062e-01 ppl_x2y=2.20 loss_y2x=6.3604e-01 ppl_y2x=1.89 dual_loss=8.3831e-01
Validation X2Y - loss=1.5862e+00 ppl=4.88 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.2782e+00 ppl=3.59 best_loss=1.0372e+00 best_ppl=2.82
Epoch 57 - |param|=8.83e+02 |g_param|=8.00e+05 loss_x2y=7.9428e-01 ppl_x2y=2.21 loss_y2x=6.4604e-01 ppl_y2x=1.91 dual_loss=8.7053e-01
Validation X2Y - loss=1.5611e+00 ppl=4.76 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.2814e+00 ppl=3.60 best_loss=1.0372e+00 best_ppl=2.82
Epoch 58 - |param|=8.83e+02 |g_param|=8.20e+05 loss_x2y=7.5859e-01 ppl_x2y=2.14 loss_y2x=6.2205e-01 ppl_y2x=1.86 dual_loss=8.4331e-01
Validation X2Y - loss=1.5818e+00 ppl=4.86 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3216e+00 ppl=3.75 best_loss=1.0372e+00 best_ppl=2.82
Epoch 59 - |param|=8.83e+02 |g_param|=7.68e+05 loss_x2y=7.1696e-01 ppl_x2y=2.05 loss_y2x=5.9524e-01 ppl_y2x=1.81 dual_loss=7.7098e-01
Validation X2Y - loss=1.5962e+00 ppl=4.93 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3049e+00 ppl=3.69 best_loss=1.0372e+00 best_ppl=2.82
Epoch 60 - |param|=8.84e+02 |g_param|=8.51e+05 loss_x2y=7.3837e-01 ppl_x2y=2.09 loss_y2x=6.3019e-01 ppl_y2x=1.88 dual_loss=1.0278e+00
Validation X2Y - loss=1.5765e+00 ppl=4.84 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3051e+00 ppl=3.69 best_loss=1.0372e+00 best_ppl=2.82
Epoch 61 - |param|=8.84e+02 |g_param|=7.79e+05 loss_x2y=7.3866e-01 ppl_x2y=2.09 loss_y2x=6.0217e-01 ppl_y2x=1.83 dual_loss=9.0240e-01
Validation X2Y - loss=1.6071e+00 ppl=4.99 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3130e+00 ppl=3.72 best_loss=1.0372e+00 best_ppl=2.82
Epoch 62 - |param|=8.85e+02 |g_param|=8.21e+05 loss_x2y=7.0076e-01 ppl_x2y=2.02 loss_y2x=5.8954e-01 ppl_y2x=1.80 dual_loss=8.4799e-01
Validation X2Y - loss=1.6434e+00 ppl=5.17 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3240e+00 ppl=3.76 best_loss=1.0372e+00 best_ppl=2.82
Epoch 63 - |param|=8.85e+02 |g_param|=7.84e+05 loss_x2y=7.1166e-01 ppl_x2y=2.04 loss_y2x=5.7922e-01 ppl_y2x=1.78 dual_loss=9.1985e-01
Validation X2Y - loss=1.6273e+00 ppl=5.09 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3492e+00 ppl=3.85 best_loss=1.0372e+00 best_ppl=2.82
Epoch 64 - |param|=8.86e+02 |g_param|=8.16e+05 loss_x2y=7.1966e-01 ppl_x2y=2.05 loss_y2x=5.8047e-01 ppl_y2x=1.79 dual_loss=9.0052e-01
Validation X2Y - loss=1.6094e+00 ppl=5.00 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3322e+00 ppl=3.79 best_loss=1.0372e+00 best_ppl=2.82
Epoch 65 - |param|=8.86e+02 |g_param|=8.28e+05 loss_x2y=7.0977e-01 ppl_x2y=2.03 loss_y2x=6.0524e-01 ppl_y2x=1.83 dual_loss=1.0600e+00
Validation X2Y - loss=1.6550e+00 ppl=5.23 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3404e+00 ppl=3.82 best_loss=1.0372e+00 best_ppl=2.82
Epoch 66 - |param|=8.87e+02 |g_param|=9.76e+05 loss_x2y=6.7447e-01 ppl_x2y=1.96 loss_y2x=5.4867e-01 ppl_y2x=1.73 dual_loss=8.7011e-01
Validation X2Y - loss=1.6314e+00 ppl=5.11 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3644e+00 ppl=3.91 best_loss=1.0372e+00 best_ppl=2.82
Epoch 67 - |param|=8.87e+02 |g_param|=9.81e+05 loss_x2y=7.2363e-01 ppl_x2y=2.06 loss_y2x=5.7784e-01 ppl_y2x=1.78 dual_loss=9.4730e-01
Validation X2Y - loss=1.6109e+00 ppl=5.01 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3706e+00 ppl=3.94 best_loss=1.0372e+00 best_ppl=2.82
Epoch 68 - |param|=8.87e+02 |g_param|=1.03e+06 loss_x2y=6.9242e-01 ppl_x2y=2.00 loss_y2x=6.0368e-01 ppl_y2x=1.83 dual_loss=1.1409e+00
Validation X2Y - loss=1.6765e+00 ppl=5.35 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3887e+00 ppl=4.01 best_loss=1.0372e+00 best_ppl=2.82
Epoch 69 - |param|=8.88e+02 |g_param|=1.00e+06 loss_x2y=6.9419e-01 ppl_x2y=2.00 loss_y2x=5.6011e-01 ppl_y2x=1.75 dual_loss=9.7474e-01
Validation X2Y - loss=1.6401e+00 ppl=5.16 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4021e+00 ppl=4.06 best_loss=1.0372e+00 best_ppl=2.82
Epoch 70 - |param|=8.88e+02 |g_param|=1.04e+06 loss_x2y=6.7138e-01 ppl_x2y=1.96 loss_y2x=5.4480e-01 ppl_y2x=1.72 dual_loss=9.6231e-01
Validation X2Y - loss=1.6721e+00 ppl=5.32 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3628e+00 ppl=3.91 best_loss=1.0372e+00 best_ppl=2.82
Epoch 71 - |param|=8.89e+02 |g_param|=9.70e+05 loss_x2y=6.5798e-01 ppl_x2y=1.93 loss_y2x=5.3536e-01 ppl_y2x=1.71 dual_loss=9.6375e-01
Validation X2Y - loss=1.6765e+00 ppl=5.35 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3725e+00 ppl=3.95 best_loss=1.0372e+00 best_ppl=2.82
Epoch 72 - |param|=8.89e+02 |g_param|=1.03e+06 loss_x2y=7.2221e-01 ppl_x2y=2.06 loss_y2x=5.7974e-01 ppl_y2x=1.79 dual_loss=1.2307e+00
Validation X2Y - loss=1.6759e+00 ppl=5.34 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3737e+00 ppl=3.95 best_loss=1.0372e+00 best_ppl=2.82
Epoch 73 - |param|=8.90e+02 |g_param|=9.80e+05 loss_x2y=6.7372e-01 ppl_x2y=1.96 loss_y2x=5.2679e-01 ppl_y2x=1.69 dual_loss=9.8412e-01
Validation X2Y - loss=1.7334e+00 ppl=5.66 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4123e+00 ppl=4.11 best_loss=1.0372e+00 best_ppl=2.82
Epoch 74 - |param|=8.90e+02 |g_param|=1.06e+06 loss_x2y=6.4697e-01 ppl_x2y=1.91 loss_y2x=5.3184e-01 ppl_y2x=1.70 dual_loss=1.0139e+00
Validation X2Y - loss=1.7242e+00 ppl=5.61 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3987e+00 ppl=4.05 best_loss=1.0372e+00 best_ppl=2.82
Iteration:   5%|███▋                                                                             | 1/22 [00:00<?, ?it/s]Epoch 75 - |param|=8.90e+02 |g_param|=8.35e+05 loss_x2y=6.3666e-01 ppl_x2y=1.89 loss_y2x=5.1685e-01 ppl_y2x=1.68 dual_loss=1.0137e+00
Validation X2Y - loss=1.7094e+00 ppl=5.53 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3744e+00 ppl=3.95 best_loss=1.0372e+00 best_ppl=2.82
Epoch 76 - |param|=8.91e+02 |g_param|=7.80e+05 loss_x2y=6.4045e-01 ppl_x2y=1.90 loss_y2x=5.1795e-01 ppl_y2x=1.68 dual_loss=1.0077e+00
Validation X2Y - loss=1.6988e+00 ppl=5.47 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3981e+00 ppl=4.05 best_loss=1.0372e+00 best_ppl=2.82
Epoch 77 - |param|=8.91e+02 |g_param|=7.82e+05 loss_x2y=7.2593e-01 ppl_x2y=2.07 loss_y2x=5.4325e-01 ppl_y2x=1.72 dual_loss=1.3733e+00
Validation X2Y - loss=1.7003e+00 ppl=5.48 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4209e+00 ppl=4.14 best_loss=1.0372e+00 best_ppl=2.82
Epoch 78 - |param|=8.92e+02 |g_param|=8.08e+05 loss_x2y=6.4455e-01 ppl_x2y=1.91 loss_y2x=5.3228e-01 ppl_y2x=1.70 dual_loss=1.1318e+00
Validation X2Y - loss=1.6978e+00 ppl=5.46 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4101e+00 ppl=4.10 best_loss=1.0372e+00 best_ppl=2.82
Epoch 79 - |param|=8.92e+02 |g_param|=7.50e+05 loss_x2y=6.0005e-01 ppl_x2y=1.82 loss_y2x=4.8653e-01 ppl_y2x=1.63 dual_loss=9.7388e-01
Validation X2Y - loss=1.7291e+00 ppl=5.64 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4320e+00 ppl=4.19 best_loss=1.0372e+00 best_ppl=2.82
Epoch 80 - |param|=8.93e+02 |g_param|=8.30e+05 loss_x2y=6.3602e-01 ppl_x2y=1.89 loss_y2x=5.0654e-01 ppl_y2x=1.66 dual_loss=1.0979e+00
Validation X2Y - loss=1.7540e+00 ppl=5.78 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3947e+00 ppl=4.03 best_loss=1.0372e+00 best_ppl=2.82
Epoch 81 - |param|=8.93e+02 |g_param|=7.59e+05 loss_x2y=6.0620e-01 ppl_x2y=1.83 loss_y2x=4.7867e-01 ppl_y2x=1.61 dual_loss=9.6779e-01
Validation X2Y - loss=1.7623e+00 ppl=5.83 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4118e+00 ppl=4.10 best_loss=1.0372e+00 best_ppl=2.82
Epoch 82 - |param|=8.93e+02 |g_param|=7.94e+05 loss_x2y=6.0428e-01 ppl_x2y=1.83 loss_y2x=4.9137e-01 ppl_y2x=1.63 dual_loss=1.0888e+00
Validation X2Y - loss=1.7359e+00 ppl=5.67 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4126e+00 ppl=4.11 best_loss=1.0372e+00 best_ppl=2.82
Epoch 83 - |param|=8.94e+02 |g_param|=7.61e+05 loss_x2y=5.9828e-01 ppl_x2y=1.82 loss_y2x=4.7391e-01 ppl_y2x=1.61 dual_loss=1.0299e+00
Validation X2Y - loss=1.7487e+00 ppl=5.75 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.3772e+00 ppl=3.96 best_loss=1.0372e+00 best_ppl=2.82
Epoch 84 - |param|=8.94e+02 |g_param|=7.74e+05 loss_x2y=5.8812e-01 ppl_x2y=1.80 loss_y2x=4.7476e-01 ppl_y2x=1.61 dual_loss=1.0682e+00
Validation X2Y - loss=1.7353e+00 ppl=5.67 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4276e+00 ppl=4.17 best_loss=1.0372e+00 best_ppl=2.82
Epoch 85 - |param|=8.95e+02 |g_param|=7.45e+05 loss_x2y=5.9516e-01 ppl_x2y=1.81 loss_y2x=4.6467e-01 ppl_y2x=1.59 dual_loss=1.0475e+00
Validation X2Y - loss=1.7419e+00 ppl=5.71 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4495e+00 ppl=4.26 best_loss=1.0372e+00 best_ppl=2.82
Epoch 86 - |param|=8.95e+02 |g_param|=7.99e+05 loss_x2y=5.8162e-01 ppl_x2y=1.79 loss_y2x=4.7095e-01 ppl_y2x=1.60 dual_loss=1.1085e+00
Validation X2Y - loss=1.8070e+00 ppl=6.09 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4727e+00 ppl=4.36 best_loss=1.0372e+00 best_ppl=2.82
Epoch 87 - |param|=8.96e+02 |g_param|=7.63e+05 loss_x2y=5.9869e-01 ppl_x2y=1.82 loss_y2x=4.9297e-01 ppl_y2x=1.64 dual_loss=1.1392e+00
Validation X2Y - loss=1.7477e+00 ppl=5.74 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4572e+00 ppl=4.29 best_loss=1.0372e+00 best_ppl=2.82
Epoch 88 - |param|=8.96e+02 |g_param|=8.08e+05 loss_x2y=5.9305e-01 ppl_x2y=1.81 loss_y2x=4.7589e-01 ppl_y2x=1.61 dual_loss=1.1572e+00
Validation X2Y - loss=1.7676e+00 ppl=5.86 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4404e+00 ppl=4.22 best_loss=1.0372e+00 best_ppl=2.82
Epoch 89 - |param|=8.96e+02 |g_param|=7.47e+05 loss_x2y=5.5884e-01 ppl_x2y=1.75 loss_y2x=4.5424e-01 ppl_y2x=1.57 dual_loss=1.0264e+00
Validation X2Y - loss=1.7809e+00 ppl=5.94 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4439e+00 ppl=4.24 best_loss=1.0372e+00 best_ppl=2.82
Epoch 90 - |param|=8.97e+02 |g_param|=7.73e+05 loss_x2y=5.7600e-01 ppl_x2y=1.78 loss_y2x=4.5865e-01 ppl_y2x=1.58 dual_loss=1.0831e+00
Validation X2Y - loss=1.8055e+00 ppl=6.08 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4189e+00 ppl=4.13 best_loss=1.0372e+00 best_ppl=2.82
Epoch 91 - |param|=8.97e+02 |g_param|=7.89e+05 loss_x2y=5.6900e-01 ppl_x2y=1.77 loss_y2x=4.9066e-01 ppl_y2x=1.63 dual_loss=1.3143e+00
Validation X2Y - loss=1.8286e+00 ppl=6.23 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4992e+00 ppl=4.48 best_loss=1.0372e+00 best_ppl=2.82
Epoch 92 - |param|=8.98e+02 |g_param|=7.85e+05 loss_x2y=5.5705e-01 ppl_x2y=1.75 loss_y2x=4.6030e-01 ppl_y2x=1.58 dual_loss=1.1317e+00
Validation X2Y - loss=1.8081e+00 ppl=6.10 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4320e+00 ppl=4.19 best_loss=1.0372e+00 best_ppl=2.82
Epoch 93 - |param|=8.98e+02 |g_param|=7.49e+05 loss_x2y=5.5170e-01 ppl_x2y=1.74 loss_y2x=4.4514e-01 ppl_y2x=1.56 dual_loss=1.1375e+00
Validation X2Y - loss=1.8403e+00 ppl=6.30 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4158e+00 ppl=4.12 best_loss=1.0372e+00 best_ppl=2.82
Epoch 94 - |param|=8.98e+02 |g_param|=7.95e+05 loss_x2y=5.5900e-01 ppl_x2y=1.75 loss_y2x=4.4790e-01 ppl_y2x=1.57 dual_loss=1.0961e+00
Validation X2Y - loss=1.8611e+00 ppl=6.43 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4639e+00 ppl=4.32 best_loss=1.0372e+00 best_ppl=2.82
Epoch 95 - |param|=8.99e+02 |g_param|=7.31e+05 loss_x2y=5.3608e-01 ppl_x2y=1.71 loss_y2x=4.4119e-01 ppl_y2x=1.55 dual_loss=1.1697e+00
Validation X2Y - loss=1.8542e+00 ppl=6.39 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4724e+00 ppl=4.36 best_loss=1.0372e+00 best_ppl=2.82
Epoch 96 - |param|=8.99e+02 |g_param|=7.69e+05 loss_x2y=5.3893e-01 ppl_x2y=1.71 loss_y2x=4.3786e-01 ppl_y2x=1.55 dual_loss=1.0591e+00
Validation X2Y - loss=1.8325e+00 ppl=6.25 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4358e+00 ppl=4.20 best_loss=1.0372e+00 best_ppl=2.82
Epoch 97 - |param|=9.00e+02 |g_param|=7.49e+05 loss_x2y=5.4745e-01 ppl_x2y=1.73 loss_y2x=4.5201e-01 ppl_y2x=1.57 dual_loss=1.2089e+00
Validation X2Y - loss=1.8166e+00 ppl=6.15 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.5033e+00 ppl=4.50 best_loss=1.0372e+00 best_ppl=2.82
Epoch 98 - |param|=9.00e+02 |g_param|=7.78e+05 loss_x2y=5.4899e-01 ppl_x2y=1.73 loss_y2x=4.5870e-01 ppl_y2x=1.58 dual_loss=1.3774e+00
Validation X2Y - loss=1.8151e+00 ppl=6.14 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4507e+00 ppl=4.27 best_loss=1.0372e+00 best_ppl=2.82
Epoch 99 - |param|=9.00e+02 |g_param|=7.65e+05 loss_x2y=5.4084e-01 ppl_x2y=1.72 loss_y2x=4.3409e-01 ppl_y2x=1.54 dual_loss=1.2370e+00
Validation X2Y - loss=1.8112e+00 ppl=6.12 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4798e+00 ppl=4.39 best_loss=1.0372e+00 best_ppl=2.82
Epoch 100 - |param|=9.01e+02 |g_param|=7.54e+05 loss_x2y=4.9307e-01 ppl_x2y=1.64 loss_y2x=4.0702e-01 ppl_y2x=1.50 dual_loss=1.0594e+00
Validation X2Y - loss=1.8221e+00 ppl=6.18 best_loss=1.2214e+00 best_ppl=3.39                                            
Validation Y2X - loss=1.4809e+00 ppl=4.40 best_loss=1.0372e+00 best_ppl=2.82

real	32m56.377s
user	32m24.005s
sys	0m26.211s
```

total training time:  
```
real	168m57.859s
user	166m8.887s
sys	2m34.820s

```

testing/evaluation...  

```
/home/ye/exp/simple-nmt/model/dsl/transformer/mybk-100epoch
Evaluation result for the model: dsl-model-mybk.01.4.46-86.08.4.11-60.96.3.44-31.07.3.13-22.89.pth, mybk
BLEU = 4.43, 20.7/6.0/2.5/1.2 (BP=1.000, ratio=1.065, hyp_len=12175, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.01.4.46-86.08.4.11-60.96.3.44-31.07.3.13-22.89.pth, bkmy
BLEU = 4.56, 28.1/7.5/2.7/0.8 (BP=0.977, ratio=0.977, hyp_len=11949, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.02.3.69-39.96.3.30-26.98.2.99-19.88.2.66-14.33.pth, mybk
BLEU = 1.03, 5.1/1.5/0.6/0.3 (BP=1.000, ratio=4.394, hyp_len=50232, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.02.3.69-39.96.3.30-26.98.2.99-19.88.2.66-14.33.pth, bkmy
BLEU = 6.89, 31.3/10.9/4.2/1.6 (BP=1.000, ratio=1.025, hyp_len=12531, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.03.3.21-24.82.2.83-16.87.2.50-12.12.2.28-9.73.pth, mybk
BLEU = 6.11, 24.4/8.5/3.7/1.8 (BP=1.000, ratio=1.196, hyp_len=13667, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.03.3.21-24.82.2.83-16.87.2.50-12.12.2.28-9.73.pth, bkmy
BLEU = 10.97, 40.4/17.1/7.5/3.4 (BP=0.951, ratio=0.952, hyp_len=11646, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.04.3.01-20.26.2.65-14.18.2.29-9.89.2.05-7.79.pth, mybk
BLEU = 6.09, 20.8/8.5/4.1/1.9 (BP=1.000, ratio=1.792, hyp_len=20483, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.04.3.01-20.26.2.65-14.18.2.29-9.89.2.05-7.79.pth, bkmy
BLEU = 13.66, 41.2/18.9/9.4/4.8 (BP=1.000, ratio=1.023, hyp_len=12513, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.05.2.73-15.38.2.36-10.56.1.99-7.32.1.79-6.02.pth, mybk
BLEU = 12.33, 35.1/16.1/8.6/4.8 (BP=1.000, ratio=1.204, hyp_len=13769, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.05.2.73-15.38.2.36-10.56.1.99-7.32.1.79-6.02.pth, bkmy
BLEU = 17.78, 46.3/24.0/12.8/7.1 (BP=0.998, ratio=0.998, hyp_len=12201, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.06.2.58-13.19.2.26-9.58.1.80-6.05.1.61-5.02.pth, mybk
BLEU = 14.82, 38.1/18.9/10.8/6.2 (BP=1.000, ratio=1.223, hyp_len=13976, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.06.2.58-13.19.2.26-9.58.1.80-6.05.1.61-5.02.pth, bkmy
BLEU = 22.48, 51.9/29.0/16.9/10.0 (BP=1.000, ratio=1.000, hyp_len=12237, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.07.2.43-11.32.2.10-8.19.1.66-5.27.1.49-4.44.pth, mybk
BLEU = 21.75, 49.5/26.7/16.3/10.4 (BP=0.999, ratio=0.999, hyp_len=11420, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.07.2.43-11.32.2.10-8.19.1.66-5.27.1.49-4.44.pth, bkmy
BLEU = 25.58, 52.9/31.7/19.9/12.9 (BP=1.000, ratio=1.042, hyp_len=12750, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.08.2.33-10.29.2.00-7.41.1.50-4.50.1.37-3.95.pth, mybk
BLEU = 25.29, 53.6/31.2/19.5/12.6 (BP=1.000, ratio=1.041, hyp_len=11896, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.08.2.33-10.29.2.00-7.41.1.50-4.50.1.37-3.95.pth, bkmy
BLEU = 29.50, 56.9/35.7/23.5/15.9 (BP=1.000, ratio=1.028, hyp_len=12574, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.09.2.30-9.93.1.99-7.30.1.48-4.39.1.30-3.67.pth, mybk
BLEU = 22.19, 48.2/27.2/17.0/10.9 (BP=1.000, ratio=1.141, hyp_len=13046, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.09.2.30-9.93.1.99-7.30.1.48-4.39.1.30-3.67.pth, bkmy
BLEU = 30.09, 57.9/36.6/23.8/16.2 (BP=1.000, ratio=1.054, hyp_len=12892, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.100.0.49-1.64.0.41-1.50.1.82-6.18.1.48-4.40.pth, mybk
BLEU = 29.48, 55.7/34.4/23.5/16.8 (BP=1.000, ratio=1.062, hyp_len=12141, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.100.0.49-1.64.0.41-1.50.1.82-6.18.1.48-4.40.pth, bkmy
BLEU = 32.36, 57.9/37.9/26.2/19.0 (BP=1.000, ratio=1.100, hyp_len=13453, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.10.2.10-8.16.1.83-6.20.1.41-4.09.1.20-3.33.pth, mybk
BLEU = 28.65, 57.4/34.5/22.5/15.2 (BP=0.999, ratio=0.999, hyp_len=11421, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.10.2.10-8.16.1.83-6.20.1.41-4.09.1.20-3.33.pth, bkmy
BLEU = 33.66, 60.4/40.0/27.4/19.4 (BP=1.000, ratio=1.052, hyp_len=12871, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.11.1.99-7.34.1.73-5.62.1.36-3.89.1.19-3.29.pth, mybk
BLEU = 27.93, 55.4/33.2/22.0/15.1 (BP=1.000, ratio=1.034, hyp_len=11826, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.11.1.99-7.34.1.73-5.62.1.36-3.89.1.19-3.29.pth, bkmy
BLEU = 34.25, 61.2/40.5/27.8/20.0 (BP=1.000, ratio=1.056, hyp_len=12917, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.12.1.95-7.01.1.68-5.39.1.31-3.72.1.13-3.10.pth, mybk
BLEU = 29.22, 57.9/35.2/23.0/15.6 (BP=1.000, ratio=1.039, hyp_len=11881, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.12.1.95-7.01.1.68-5.39.1.31-3.72.1.13-3.10.pth, bkmy
BLEU = 38.39, 66.9/46.1/32.6/23.8 (BP=0.977, ratio=0.977, hyp_len=11948, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.13.1.91-6.74.1.63-5.09.1.25-3.51.1.08-2.94.pth, mybk
BLEU = 29.42, 56.8/35.2/23.3/16.1 (BP=1.000, ratio=1.076, hyp_len=12305, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.13.1.91-6.74.1.63-5.09.1.25-3.51.1.08-2.94.pth, bkmy
BLEU = 36.93, 63.1/43.5/30.6/22.1 (BP=1.000, ratio=1.078, hyp_len=13184, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.14.1.87-6.49.1.59-4.90.1.27-3.57.1.09-2.99.pth, mybk
BLEU = 31.62, 58.8/37.2/25.4/18.0 (BP=1.000, ratio=1.037, hyp_len=11853, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.14.1.87-6.49.1.59-4.90.1.27-3.57.1.09-2.99.pth, bkmy
BLEU = 38.00, 63.4/44.4/31.7/23.4 (BP=1.000, ratio=1.053, hyp_len=12877, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.15.1.71-5.53.1.46-4.32.1.22-3.40.1.06-2.90.pth, mybk
BLEU = 31.60, 59.4/37.7/25.3/17.6 (BP=1.000, ratio=1.063, hyp_len=12152, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.15.1.71-5.53.1.46-4.32.1.22-3.40.1.06-2.90.pth, bkmy
BLEU = 39.74, 65.8/46.3/33.3/24.6 (BP=1.000, ratio=1.028, hyp_len=12577, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.16.1.70-5.45.1.46-4.32.1.25-3.49.1.06-2.88.pth, mybk
BLEU = 32.24, 59.9/38.3/25.8/18.3 (BP=1.000, ratio=1.056, hyp_len=12077, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.16.1.70-5.45.1.46-4.32.1.25-3.49.1.06-2.88.pth, bkmy
BLEU = 39.69, 65.8/46.3/33.2/24.5 (BP=1.000, ratio=1.052, hyp_len=12870, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.17.1.74-5.72.1.45-4.28.1.27-3.56.1.04-2.84.pth, mybk
BLEU = 31.84, 59.3/37.6/25.6/18.0 (BP=1.000, ratio=1.063, hyp_len=12153, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.17.1.74-5.72.1.45-4.28.1.27-3.56.1.04-2.84.pth, bkmy
BLEU = 40.41, 66.6/47.1/33.9/25.0 (BP=1.000, ratio=1.045, hyp_len=12779, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.18.1.67-5.34.1.47-4.36.1.26-3.51.1.07-2.93.pth, mybk
BLEU = 32.75, 60.2/38.5/26.3/18.9 (BP=1.000, ratio=1.056, hyp_len=12077, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.18.1.67-5.34.1.47-4.36.1.26-3.51.1.07-2.93.pth, bkmy
BLEU = 39.31, 65.1/46.0/32.9/24.2 (BP=1.000, ratio=1.076, hyp_len=13155, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.19.1.55-4.72.1.34-3.82.1.23-3.42.1.06-2.87.pth, mybk
BLEU = 32.28, 59.6/38.0/26.0/18.5 (BP=1.000, ratio=1.051, hyp_len=12011, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.19.1.55-4.72.1.34-3.82.1.23-3.42.1.06-2.87.pth, bkmy
BLEU = 41.09, 67.3/47.8/34.5/25.7 (BP=1.000, ratio=1.033, hyp_len=12629, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.20.1.55-4.69.1.32-3.74.1.28-3.58.1.07-2.90.pth, mybk
BLEU = 30.55, 56.9/35.9/24.4/17.5 (BP=1.000, ratio=1.092, hyp_len=12484, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.20.1.55-4.69.1.32-3.74.1.28-3.58.1.07-2.90.pth, bkmy
BLEU = 39.36, 65.2/45.7/32.9/24.5 (BP=1.000, ratio=1.071, hyp_len=13097, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.21.1.46-4.31.1.23-3.43.1.26-3.52.1.07-2.90.pth, mybk
BLEU = 32.81, 59.4/38.3/26.4/19.3 (BP=1.000, ratio=1.064, hyp_len=12158, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.21.1.46-4.31.1.23-3.43.1.26-3.52.1.07-2.90.pth, bkmy
BLEU = 40.23, 65.8/46.5/33.9/25.2 (BP=1.000, ratio=1.080, hyp_len=13213, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.22.1.41-4.09.1.19-3.28.1.26-3.54.1.04-2.84.pth, mybk
BLEU = 32.67, 60.5/38.6/26.2/18.6 (BP=1.000, ratio=1.074, hyp_len=12275, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.22.1.41-4.09.1.19-3.28.1.26-3.54.1.04-2.84.pth, bkmy
BLEU = 43.23, 69.0/49.8/36.7/27.7 (BP=1.000, ratio=1.013, hyp_len=12390, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.23.1.46-4.31.1.25-3.49.1.26-3.52.1.04-2.82.pth, mybk
BLEU = 32.93, 60.6/38.8/26.4/19.0 (BP=1.000, ratio=1.064, hyp_len=12167, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.23.1.46-4.31.1.25-3.49.1.26-3.52.1.04-2.82.pth, bkmy
BLEU = 40.78, 66.4/47.3/34.4/25.6 (BP=1.000, ratio=1.075, hyp_len=13143, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.24.1.40-4.05.1.21-3.35.1.26-3.51.1.05-2.87.pth, mybk
BLEU = 33.50, 61.3/39.3/26.9/19.4 (BP=1.000, ratio=1.030, hyp_len=11775, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.24.1.40-4.05.1.21-3.35.1.26-3.51.1.05-2.87.pth, bkmy
BLEU = 43.03, 69.0/49.4/36.3/27.7 (BP=1.000, ratio=1.014, hyp_len=12401, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.25.1.34-3.82.1.15-3.16.1.22-3.39.1.06-2.87.pth, mybk
BLEU = 34.86, 62.7/40.6/28.3/20.5 (BP=1.000, ratio=1.045, hyp_len=11942, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.25.1.34-3.82.1.15-3.16.1.22-3.39.1.06-2.87.pth, bkmy
BLEU = 41.21, 66.9/47.5/34.7/26.2 (BP=1.000, ratio=1.047, hyp_len=12806, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.26.1.33-3.80.1.17-3.24.1.25-3.48.1.07-2.92.pth, mybk
BLEU = 34.25, 61.6/39.6/27.6/20.4 (BP=1.000, ratio=1.030, hyp_len=11779, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.26.1.33-3.80.1.17-3.24.1.25-3.48.1.07-2.92.pth, bkmy
BLEU = 42.31, 68.4/48.8/35.6/27.0 (BP=1.000, ratio=1.030, hyp_len=12597, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.27.1.28-3.61.1.06-2.90.1.28-3.58.1.05-2.87.pth, mybk
BLEU = 33.52, 60.4/39.1/27.2/19.7 (BP=1.000, ratio=1.077, hyp_len=12308, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.27.1.28-3.61.1.06-2.90.1.28-3.58.1.05-2.87.pth, bkmy
BLEU = 39.82, 65.7/45.8/33.3/25.1 (BP=1.000, ratio=1.037, hyp_len=12688, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.28.1.35-3.84.1.13-3.10.1.28-3.58.1.09-2.96.pth, mybk
BLEU = 32.25, 60.0/38.0/25.7/18.5 (BP=1.000, ratio=1.069, hyp_len=12216, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.28.1.35-3.84.1.13-3.10.1.28-3.58.1.09-2.96.pth, bkmy
BLEU = 38.69, 64.6/45.1/32.2/23.9 (BP=1.000, ratio=1.065, hyp_len=13022, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.29.1.21-3.34.1.01-2.74.1.27-3.56.1.10-3.01.pth, mybk
BLEU = 33.29, 60.2/38.9/26.9/19.5 (BP=1.000, ratio=1.064, hyp_len=12167, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.29.1.21-3.34.1.01-2.74.1.27-3.56.1.10-3.01.pth, bkmy
BLEU = 39.64, 66.1/46.3/33.1/24.4 (BP=1.000, ratio=1.045, hyp_len=12783, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.30.1.20-3.33.1.01-2.76.1.29-3.65.1.07-2.92.pth, mybk
BLEU = 33.06, 60.5/38.9/26.7/19.0 (BP=1.000, ratio=1.051, hyp_len=12020, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.30.1.20-3.33.1.01-2.76.1.29-3.65.1.07-2.92.pth, bkmy
BLEU = 40.01, 65.4/46.2/33.6/25.3 (BP=1.000, ratio=1.069, hyp_len=13070, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.31.1.21-3.34.1.00-2.72.1.31-3.69.1.10-2.99.pth, mybk
BLEU = 31.59, 59.0/37.4/25.3/17.9 (BP=1.000, ratio=1.098, hyp_len=12556, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.31.1.21-3.34.1.00-2.72.1.31-3.69.1.10-2.99.pth, bkmy
BLEU = 41.50, 67.4/47.9/34.9/26.3 (BP=1.000, ratio=1.038, hyp_len=12694, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.32.1.13-3.09.0.94-2.56.1.34-3.83.1.12-3.06.pth, mybk
BLEU = 30.95, 58.4/36.6/24.7/17.4 (BP=1.000, ratio=1.091, hyp_len=12478, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.32.1.13-3.09.0.94-2.56.1.34-3.83.1.12-3.06.pth, bkmy
BLEU = 38.38, 64.1/44.7/32.0/23.6 (BP=1.000, ratio=1.082, hyp_len=13235, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.33.1.15-3.16.0.95-2.59.1.37-3.93.1.11-3.04.pth, mybk
BLEU = 32.50, 59.8/38.0/26.2/18.8 (BP=1.000, ratio=1.052, hyp_len=12032, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.33.1.15-3.16.0.95-2.59.1.37-3.93.1.11-3.04.pth, bkmy
BLEU = 41.06, 66.4/47.0/34.4/26.4 (BP=1.000, ratio=1.033, hyp_len=12636, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.34.1.10-3.02.0.91-2.49.1.36-3.89.1.13-3.09.pth, mybk
BLEU = 32.05, 59.6/37.6/25.6/18.4 (BP=1.000, ratio=1.048, hyp_len=11986, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.34.1.10-3.02.0.91-2.49.1.36-3.89.1.13-3.09.pth, bkmy
BLEU = 38.49, 64.7/44.7/32.0/23.7 (BP=1.000, ratio=1.063, hyp_len=12997, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.35.1.16-3.20.0.94-2.55.1.36-3.91.1.14-3.14.pth, mybk
BLEU = 32.06, 59.2/37.7/25.7/18.4 (BP=1.000, ratio=1.072, hyp_len=12253, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.35.1.16-3.20.0.94-2.55.1.36-3.91.1.14-3.14.pth, bkmy
BLEU = 39.26, 65.2/45.6/32.7/24.4 (BP=1.000, ratio=1.063, hyp_len=13001, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.36.1.08-2.93.0.93-2.54.1.37-3.94.1.14-3.13.pth, mybk
BLEU = 31.17, 58.9/37.0/24.9/17.4 (BP=1.000, ratio=1.050, hyp_len=12004, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.36.1.08-2.93.0.93-2.54.1.37-3.94.1.14-3.13.pth, bkmy
BLEU = 39.73, 65.5/46.0/33.3/24.9 (BP=1.000, ratio=1.032, hyp_len=12624, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.37.1.03-2.81.0.89-2.42.1.39-4.02.1.12-3.08.pth, mybk
BLEU = 32.84, 60.3/38.5/26.4/18.9 (BP=1.000, ratio=1.050, hyp_len=12003, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.37.1.03-2.81.0.89-2.42.1.39-4.02.1.12-3.08.pth, bkmy
BLEU = 40.72, 66.5/46.8/34.2/25.8 (BP=1.000, ratio=1.037, hyp_len=12686, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.38.1.02-2.77.0.85-2.35.1.40-4.06.1.15-3.15.pth, mybk
BLEU = 32.06, 59.8/37.9/25.7/18.1 (BP=1.000, ratio=1.077, hyp_len=12309, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.38.1.02-2.77.0.85-2.35.1.40-4.06.1.15-3.15.pth, bkmy
BLEU = 40.11, 65.6/46.3/33.7/25.3 (BP=1.000, ratio=1.038, hyp_len=12692, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.39.1.05-2.85.0.85-2.34.1.45-4.28.1.15-3.17.pth, mybk
BLEU = 29.63, 56.0/34.9/23.6/16.7 (BP=1.000, ratio=1.105, hyp_len=12637, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.39.1.05-2.85.0.85-2.34.1.45-4.28.1.15-3.17.pth, bkmy
BLEU = 36.79, 61.9/42.4/30.5/22.9 (BP=1.000, ratio=1.096, hyp_len=13402, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.40.0.99-2.69.0.82-2.26.1.45-4.24.1.13-3.10.pth, mybk
BLEU = 32.19, 59.5/37.8/25.8/18.5 (BP=1.000, ratio=1.052, hyp_len=12031, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.40.0.99-2.69.0.82-2.26.1.45-4.24.1.13-3.10.pth, bkmy
BLEU = 39.97, 65.9/46.2/33.4/25.0 (BP=1.000, ratio=1.041, hyp_len=12731, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.41.1.00-2.72.0.86-2.36.1.44-4.21.1.13-3.10.pth, mybk
BLEU = 32.15, 59.6/38.2/25.8/18.2 (BP=1.000, ratio=1.061, hyp_len=12132, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.41.1.00-2.72.0.86-2.36.1.44-4.21.1.13-3.10.pth, bkmy
BLEU = 38.15, 63.8/44.2/31.8/23.6 (BP=1.000, ratio=1.075, hyp_len=13150, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.42.0.98-2.66.0.80-2.23.1.40-4.06.1.16-3.20.pth, mybk
BLEU = 32.00, 59.6/37.8/25.7/18.1 (BP=1.000, ratio=1.068, hyp_len=12213, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.42.0.98-2.66.0.80-2.23.1.40-4.06.1.16-3.20.pth, bkmy
BLEU = 40.64, 66.0/46.6/34.2/25.9 (BP=1.000, ratio=1.052, hyp_len=12866, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.43.0.92-2.51.0.75-2.12.1.41-4.11.1.17-3.23.pth, mybk
BLEU = 31.78, 58.2/37.1/25.6/18.5 (BP=1.000, ratio=1.088, hyp_len=12440, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.43.0.92-2.51.0.75-2.12.1.41-4.11.1.17-3.23.pth, bkmy
BLEU = 39.66, 66.0/46.1/33.1/24.6 (BP=1.000, ratio=1.029, hyp_len=12591, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.44.0.94-2.57.0.77-2.16.1.44-4.22.1.19-3.28.pth, mybk
BLEU = 31.83, 58.8/37.3/25.6/18.3 (BP=1.000, ratio=1.066, hyp_len=12182, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.44.0.94-2.57.0.77-2.16.1.44-4.22.1.19-3.28.pth, bkmy
BLEU = 38.91, 64.4/44.7/32.4/24.5 (BP=1.000, ratio=1.048, hyp_len=12812, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.45.0.90-2.47.0.74-2.10.1.47-4.36.1.18-3.25.pth, mybk
BLEU = 31.55, 58.5/37.1/25.4/18.0 (BP=1.000, ratio=1.061, hyp_len=12132, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.45.0.90-2.47.0.74-2.10.1.47-4.36.1.18-3.25.pth, bkmy
BLEU = 40.18, 65.6/46.5/33.8/25.3 (BP=1.000, ratio=1.050, hyp_len=12845, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.46.0.90-2.46.0.74-2.10.1.48-4.39.1.19-3.28.pth, mybk
BLEU = 32.75, 60.2/38.3/26.4/18.9 (BP=1.000, ratio=1.041, hyp_len=11901, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.46.0.90-2.46.0.74-2.10.1.48-4.39.1.19-3.28.pth, bkmy
BLEU = 37.74, 63.8/43.6/31.1/23.4 (BP=1.000, ratio=1.053, hyp_len=12875, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.47.0.90-2.47.0.75-2.11.1.50-4.50.1.19-3.28.pth, mybk
BLEU = 30.77, 57.7/36.2/24.5/17.5 (BP=1.000, ratio=1.056, hyp_len=12070, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.47.0.90-2.47.0.75-2.11.1.50-4.50.1.19-3.28.pth, bkmy
BLEU = 37.57, 63.5/43.8/31.2/23.0 (BP=1.000, ratio=1.090, hyp_len=13337, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.48.0.95-2.58.0.74-2.10.1.49-4.44.1.26-3.51.pth, mybk
BLEU = 31.41, 58.6/37.1/25.1/17.8 (BP=1.000, ratio=1.060, hyp_len=12122, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.48.0.95-2.58.0.74-2.10.1.49-4.44.1.26-3.51.pth, bkmy
BLEU = 37.01, 62.1/42.5/30.7/23.1 (BP=1.000, ratio=1.066, hyp_len=13040, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.49.0.89-2.43.0.74-2.10.1.47-4.37.1.24-3.45.pth, mybk
BLEU = 31.30, 58.1/36.7/25.0/18.0 (BP=1.000, ratio=1.049, hyp_len=11992, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.49.0.89-2.43.0.74-2.10.1.47-4.37.1.24-3.45.pth, bkmy
BLEU = 38.41, 63.9/44.3/32.0/24.0 (BP=1.000, ratio=1.058, hyp_len=12943, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.50.0.90-2.45.0.73-2.07.1.49-4.46.1.24-3.46.pth, mybk
BLEU = 32.30, 59.1/37.8/26.1/18.7 (BP=1.000, ratio=1.054, hyp_len=12055, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.50.0.90-2.45.0.73-2.07.1.49-4.46.1.24-3.46.pth, bkmy
BLEU = 38.43, 63.9/44.4/31.9/24.1 (BP=1.000, ratio=1.062, hyp_len=12992, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.51.0.84-2.30.0.68-1.97.1.51-4.54.1.29-3.61.pth, mybk
BLEU = 29.24, 56.2/34.8/23.1/16.2 (BP=1.000, ratio=1.096, hyp_len=12527, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.51.0.84-2.30.0.68-1.97.1.51-4.54.1.29-3.61.pth, bkmy
BLEU = 37.82, 63.0/43.5/31.5/23.7 (BP=1.000, ratio=1.069, hyp_len=13070, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.52.0.81-2.24.0.67-1.95.1.51-4.51.1.28-3.59.pth, mybk
BLEU = 32.25, 59.8/38.1/25.8/18.4 (BP=1.000, ratio=1.059, hyp_len=12103, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.52.0.81-2.24.0.67-1.95.1.51-4.51.1.28-3.59.pth, bkmy
BLEU = 36.65, 61.8/42.7/30.4/22.5 (BP=1.000, ratio=1.093, hyp_len=13365, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.53.0.80-2.22.0.65-1.91.1.51-4.53.1.27-3.55.pth, mybk
BLEU = 31.17, 58.3/36.8/24.9/17.7 (BP=1.000, ratio=1.068, hyp_len=12215, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.53.0.80-2.22.0.65-1.91.1.51-4.53.1.27-3.55.pth, bkmy
BLEU = 37.26, 62.6/43.1/30.9/23.2 (BP=1.000, ratio=1.068, hyp_len=13063, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.54.0.80-2.23.0.67-1.95.1.52-4.59.1.23-3.41.pth, mybk
BLEU = 31.48, 57.8/37.0/25.3/18.2 (BP=1.000, ratio=1.086, hyp_len=12411, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.54.0.80-2.23.0.67-1.95.1.52-4.59.1.23-3.41.pth, bkmy
BLEU = 36.14, 62.0/42.2/29.8/21.9 (BP=1.000, ratio=1.079, hyp_len=13202, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.55.0.78-2.17.0.62-1.86.1.56-4.78.1.27-3.57.pth, mybk
BLEU = 30.87, 58.0/36.3/24.6/17.5 (BP=1.000, ratio=1.065, hyp_len=12177, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.55.0.78-2.17.0.62-1.86.1.56-4.78.1.27-3.57.pth, bkmy
BLEU = 37.94, 63.7/44.1/31.5/23.5 (BP=1.000, ratio=1.049, hyp_len=12827, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.56.0.79-2.20.0.64-1.89.1.59-4.88.1.28-3.59.pth, mybk
BLEU = 29.83, 55.8/35.0/23.7/17.1 (BP=1.000, ratio=1.083, hyp_len=12380, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.56.0.79-2.20.0.64-1.89.1.59-4.88.1.28-3.59.pth, bkmy
BLEU = 37.51, 62.7/43.4/31.1/23.4 (BP=1.000, ratio=1.058, hyp_len=12941, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.57.0.79-2.21.0.65-1.91.1.56-4.76.1.28-3.60.pth, mybk
BLEU = 30.71, 57.2/36.0/24.5/17.6 (BP=1.000, ratio=1.061, hyp_len=12133, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.57.0.79-2.21.0.65-1.91.1.56-4.76.1.28-3.60.pth, bkmy
BLEU = 35.71, 61.0/41.4/29.5/21.8 (BP=1.000, ratio=1.085, hyp_len=13276, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.58.0.76-2.14.0.62-1.86.1.58-4.86.1.32-3.75.pth, mybk
BLEU = 30.48, 57.5/35.9/24.3/17.2 (BP=1.000, ratio=1.056, hyp_len=12075, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.58.0.76-2.14.0.62-1.86.1.58-4.86.1.32-3.75.pth, bkmy
BLEU = 37.80, 63.6/43.9/31.4/23.3 (BP=1.000, ratio=1.052, hyp_len=12870, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.59.0.72-2.05.0.60-1.81.1.60-4.93.1.30-3.69.pth, mybk
BLEU = 30.07, 56.7/35.2/23.9/17.1 (BP=1.000, ratio=1.066, hyp_len=12189, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.59.0.72-2.05.0.60-1.81.1.60-4.93.1.30-3.69.pth, bkmy
BLEU = 33.77, 59.4/39.6/27.7/20.0 (BP=1.000, ratio=1.117, hyp_len=13665, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.60.0.74-2.09.0.63-1.88.1.58-4.84.1.31-3.69.pth, mybk
BLEU = 30.28, 57.5/35.8/24.2/16.9 (BP=1.000, ratio=1.079, hyp_len=12330, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.60.0.74-2.09.0.63-1.88.1.58-4.84.1.31-3.69.pth, bkmy
BLEU = 36.64, 62.4/42.6/30.4/22.3 (BP=1.000, ratio=1.067, hyp_len=13049, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.61.0.74-2.09.0.60-1.83.1.61-4.99.1.31-3.72.pth, mybk
BLEU = 29.92, 57.1/35.7/23.8/16.5 (BP=1.000, ratio=1.076, hyp_len=12302, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.61.0.74-2.09.0.60-1.83.1.61-4.99.1.31-3.72.pth, bkmy
BLEU = 36.96, 62.2/42.7/30.7/22.9 (BP=1.000, ratio=1.065, hyp_len=13021, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.62.0.70-2.02.0.59-1.80.1.64-5.17.1.32-3.76.pth, mybk
BLEU = 30.07, 57.4/35.5/23.9/16.8 (BP=1.000, ratio=1.058, hyp_len=12094, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.62.0.70-2.02.0.59-1.80.1.64-5.17.1.32-3.76.pth, bkmy
BLEU = 36.21, 60.9/41.7/30.0/22.5 (BP=1.000, ratio=1.086, hyp_len=13277, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.63.0.71-2.04.0.58-1.78.1.63-5.09.1.35-3.85.pth, mybk
BLEU = 29.18, 56.0/34.5/23.1/16.2 (BP=1.000, ratio=1.074, hyp_len=12279, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.63.0.71-2.04.0.58-1.78.1.63-5.09.1.35-3.85.pth, bkmy
BLEU = 37.60, 62.9/43.2/31.3/23.5 (BP=1.000, ratio=1.055, hyp_len=12900, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.64.0.72-2.05.0.58-1.79.1.61-5.00.1.33-3.79.pth, mybk
BLEU = 30.12, 57.5/35.6/23.9/16.8 (BP=1.000, ratio=1.044, hyp_len=11934, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.64.0.72-2.05.0.58-1.79.1.61-5.00.1.33-3.79.pth, bkmy
BLEU = 36.44, 61.6/42.0/30.1/22.7 (BP=1.000, ratio=1.072, hyp_len=13117, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.65.0.71-2.03.0.61-1.83.1.66-5.23.1.34-3.82.pth, mybk
BLEU = 29.17, 55.3/34.5/23.2/16.3 (BP=1.000, ratio=1.095, hyp_len=12515, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.65.0.71-2.03.0.61-1.83.1.66-5.23.1.34-3.82.pth, bkmy
BLEU = 35.95, 61.4/41.7/29.7/22.0 (BP=1.000, ratio=1.066, hyp_len=13034, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.66.0.67-1.96.0.55-1.73.1.63-5.11.1.36-3.91.pth, mybk
BLEU = 29.00, 55.4/34.4/23.1/16.1 (BP=1.000, ratio=1.084, hyp_len=12390, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.66.0.67-1.96.0.55-1.73.1.63-5.11.1.36-3.91.pth, bkmy
BLEU = 37.50, 62.4/43.1/31.3/23.5 (BP=1.000, ratio=1.057, hyp_len=12930, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.67.0.72-2.06.0.58-1.78.1.61-5.01.1.37-3.94.pth, mybk
BLEU = 31.07, 58.1/36.8/24.9/17.5 (BP=1.000, ratio=1.035, hyp_len=11833, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.67.0.72-2.06.0.58-1.78.1.61-5.01.1.37-3.94.pth, bkmy
BLEU = 34.79, 60.2/40.6/28.5/21.0 (BP=1.000, ratio=1.101, hyp_len=13468, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.68.0.69-2.00.0.60-1.83.1.68-5.35.1.39-4.01.pth, mybk
BLEU = 29.04, 55.3/34.1/23.0/16.4 (BP=1.000, ratio=1.069, hyp_len=12219, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.68.0.69-2.00.0.60-1.83.1.68-5.35.1.39-4.01.pth, bkmy
BLEU = 33.88, 58.8/39.4/27.8/20.4 (BP=1.000, ratio=1.101, hyp_len=13471, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.69.0.69-2.00.0.56-1.75.1.64-5.16.1.40-4.06.pth, mybk
BLEU = 30.39, 57.1/35.7/24.4/17.2 (BP=1.000, ratio=1.063, hyp_len=12151, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.69.0.69-2.00.0.56-1.75.1.64-5.16.1.40-4.06.pth, bkmy
BLEU = 37.23, 62.4/42.8/30.8/23.3 (BP=1.000, ratio=1.052, hyp_len=12872, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.70.0.67-1.96.0.54-1.72.1.67-5.32.1.36-3.91.pth, mybk
BLEU = 30.15, 57.1/35.3/24.0/17.1 (BP=1.000, ratio=1.070, hyp_len=12234, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.70.0.67-1.96.0.54-1.72.1.67-5.32.1.36-3.91.pth, bkmy
BLEU = 36.18, 61.1/41.4/30.0/22.6 (BP=1.000, ratio=1.057, hyp_len=12931, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.71.0.66-1.93.0.54-1.71.1.68-5.35.1.37-3.95.pth, mybk
BLEU = 30.18, 57.1/35.7/24.1/16.9 (BP=1.000, ratio=1.071, hyp_len=12243, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.71.0.66-1.93.0.54-1.71.1.68-5.35.1.37-3.95.pth, bkmy
BLEU = 37.27, 62.5/42.7/30.9/23.4 (BP=1.000, ratio=1.047, hyp_len=12801, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.72.0.72-2.06.0.58-1.79.1.68-5.34.1.37-3.95.pth, mybk
BLEU = 30.80, 57.1/36.2/24.7/17.6 (BP=1.000, ratio=1.066, hyp_len=12188, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.72.0.72-2.06.0.58-1.79.1.68-5.34.1.37-3.95.pth, bkmy
BLEU = 36.33, 61.6/41.7/30.0/22.6 (BP=1.000, ratio=1.052, hyp_len=12868, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.73.0.67-1.96.0.53-1.69.1.73-5.66.1.41-4.11.pth, mybk
BLEU = 30.49, 57.8/36.0/24.4/17.0 (BP=1.000, ratio=1.068, hyp_len=12211, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.73.0.67-1.96.0.53-1.69.1.73-5.66.1.41-4.11.pth, bkmy
BLEU = 35.08, 60.2/40.6/28.8/21.5 (BP=1.000, ratio=1.080, hyp_len=13215, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.74.0.65-1.91.0.53-1.70.1.72-5.61.1.40-4.05.pth, mybk
BLEU = 28.98, 55.1/34.0/23.0/16.4 (BP=1.000, ratio=1.106, hyp_len=12647, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.74.0.65-1.91.0.53-1.70.1.72-5.61.1.40-4.05.pth, bkmy
BLEU = 37.14, 62.1/42.6/30.8/23.3 (BP=1.000, ratio=1.060, hyp_len=12970, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.75.0.64-1.89.0.52-1.68.1.71-5.53.1.37-3.95.pth, mybk
BLEU = 28.60, 55.4/34.1/22.6/15.7 (BP=1.000, ratio=1.093, hyp_len=12496, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.75.0.64-1.89.0.52-1.68.1.71-5.53.1.37-3.95.pth, bkmy
BLEU = 34.00, 59.6/39.7/27.7/20.4 (BP=1.000, ratio=1.095, hyp_len=13391, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.76.0.64-1.90.0.52-1.68.1.70-5.47.1.40-4.05.pth, mybk
BLEU = 30.14, 56.7/35.4/24.0/17.1 (BP=1.000, ratio=1.062, hyp_len=12140, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.76.0.64-1.90.0.52-1.68.1.70-5.47.1.40-4.05.pth, bkmy
BLEU = 35.84, 61.1/41.5/29.5/22.0 (BP=1.000, ratio=1.077, hyp_len=13178, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.77.0.73-2.07.0.54-1.72.1.70-5.48.1.42-4.14.pth, mybk
BLEU = 31.07, 58.0/36.5/24.9/17.6 (BP=1.000, ratio=1.064, hyp_len=12160, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.77.0.73-2.07.0.54-1.72.1.70-5.48.1.42-4.14.pth, bkmy
BLEU = 36.29, 61.3/41.7/29.9/22.7 (BP=1.000, ratio=1.074, hyp_len=13131, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.78.0.64-1.91.0.53-1.70.1.70-5.46.1.41-4.10.pth, mybk
BLEU = 30.60, 58.0/36.3/24.3/17.2 (BP=1.000, ratio=1.062, hyp_len=12136, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.78.0.64-1.91.0.53-1.70.1.70-5.46.1.41-4.10.pth, bkmy
BLEU = 34.98, 60.2/40.4/28.8/21.4 (BP=1.000, ratio=1.065, hyp_len=13025, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.79.0.60-1.82.0.49-1.63.1.73-5.64.1.43-4.19.pth, mybk
BLEU = 28.49, 55.3/33.9/22.6/15.6 (BP=1.000, ratio=1.080, hyp_len=12347, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.79.0.60-1.82.0.49-1.63.1.73-5.64.1.43-4.19.pth, bkmy
BLEU = 33.46, 59.0/39.2/27.4/19.8 (BP=1.000, ratio=1.083, hyp_len=13245, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.80.0.64-1.89.0.51-1.66.1.75-5.78.1.39-4.03.pth, mybk
BLEU = 27.98, 54.1/32.8/22.0/15.7 (BP=1.000, ratio=1.089, hyp_len=12448, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.80.0.64-1.89.0.51-1.66.1.75-5.78.1.39-4.03.pth, bkmy
BLEU = 33.36, 59.2/38.9/27.2/19.8 (BP=1.000, ratio=1.075, hyp_len=13149, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.81.0.61-1.83.0.48-1.61.1.76-5.83.1.41-4.10.pth, mybk
BLEU = 29.04, 56.3/34.3/22.9/16.0 (BP=1.000, ratio=1.077, hyp_len=12314, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.81.0.61-1.83.0.48-1.61.1.76-5.83.1.41-4.10.pth, bkmy
BLEU = 35.66, 61.2/41.2/29.4/21.8 (BP=1.000, ratio=1.054, hyp_len=12887, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.82.0.60-1.83.0.49-1.63.1.74-5.67.1.41-4.11.pth, mybk
BLEU = 29.34, 55.3/34.3/23.5/16.6 (BP=1.000, ratio=1.084, hyp_len=12391, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.82.0.60-1.83.0.49-1.63.1.74-5.67.1.41-4.11.pth, bkmy
BLEU = 34.40, 59.4/39.9/28.3/20.9 (BP=1.000, ratio=1.091, hyp_len=13349, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.83.0.60-1.82.0.47-1.61.1.75-5.75.1.38-3.96.pth, mybk
BLEU = 30.03, 56.2/35.1/24.0/17.2 (BP=1.000, ratio=1.058, hyp_len=12099, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.83.0.60-1.82.0.47-1.61.1.75-5.75.1.38-3.96.pth, bkmy
BLEU = 34.97, 60.2/40.7/28.7/21.3 (BP=1.000, ratio=1.064, hyp_len=13008, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.84.0.59-1.80.0.47-1.61.1.74-5.67.1.43-4.17.pth, mybk
BLEU = 29.92, 56.1/35.1/23.9/17.0 (BP=1.000, ratio=1.069, hyp_len=12220, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.84.0.59-1.80.0.47-1.61.1.74-5.67.1.43-4.17.pth, bkmy
BLEU = 33.80, 58.6/39.3/27.8/20.4 (BP=1.000, ratio=1.081, hyp_len=13222, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.85.0.60-1.81.0.46-1.59.1.74-5.71.1.45-4.26.pth, mybk
BLEU = 28.68, 54.8/33.8/22.7/16.1 (BP=1.000, ratio=1.075, hyp_len=12293, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.85.0.60-1.81.0.46-1.59.1.74-5.71.1.45-4.26.pth, bkmy
BLEU = 34.70, 60.1/40.3/28.5/21.0 (BP=1.000, ratio=1.051, hyp_len=12849, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.86.0.58-1.79.0.47-1.60.1.81-6.09.1.47-4.36.pth, mybk
BLEU = 28.58, 54.6/33.5/22.6/16.1 (BP=1.000, ratio=1.085, hyp_len=12401, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.86.0.58-1.79.0.47-1.60.1.81-6.09.1.47-4.36.pth, bkmy
BLEU = 34.10, 59.2/39.4/28.0/20.7 (BP=1.000, ratio=1.069, hyp_len=13070, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.87.0.60-1.82.0.49-1.64.1.75-5.74.1.46-4.29.pth, mybk
BLEU = 29.86, 56.3/35.0/23.7/17.0 (BP=1.000, ratio=1.075, hyp_len=12286, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.87.0.60-1.82.0.49-1.64.1.75-5.74.1.46-4.29.pth, bkmy
BLEU = 34.04, 59.6/39.8/27.7/20.4 (BP=1.000, ratio=1.078, hyp_len=13183, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.88.0.59-1.81.0.48-1.61.1.77-5.86.1.44-4.22.pth, mybk
BLEU = 29.13, 55.8/34.5/23.1/16.2 (BP=1.000, ratio=1.078, hyp_len=12328, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.88.0.59-1.81.0.48-1.61.1.77-5.86.1.44-4.22.pth, bkmy
BLEU = 32.99, 58.2/38.5/27.0/19.6 (BP=1.000, ratio=1.084, hyp_len=13258, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.89.0.56-1.75.0.45-1.57.1.78-5.94.1.44-4.24.pth, mybk
BLEU = 30.18, 56.7/35.4/24.2/17.1 (BP=1.000, ratio=1.057, hyp_len=12085, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.89.0.56-1.75.0.45-1.57.1.78-5.94.1.44-4.24.pth, bkmy
BLEU = 34.48, 59.6/39.9/28.3/21.0 (BP=1.000, ratio=1.082, hyp_len=13232, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.90.0.58-1.78.0.46-1.58.1.81-6.08.1.42-4.13.pth, mybk
BLEU = 29.84, 56.4/35.2/23.8/16.8 (BP=1.000, ratio=1.060, hyp_len=12115, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.90.0.58-1.78.0.46-1.58.1.81-6.08.1.42-4.13.pth, bkmy
BLEU = 34.30, 59.5/39.6/28.1/20.9 (BP=1.000, ratio=1.067, hyp_len=13056, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.91.0.57-1.77.0.49-1.63.1.83-6.23.1.50-4.48.pth, mybk
BLEU = 28.98, 54.2/33.8/23.2/16.6 (BP=1.000, ratio=1.077, hyp_len=12309, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.91.0.57-1.77.0.49-1.63.1.83-6.23.1.50-4.48.pth, bkmy
BLEU = 32.32, 57.6/37.8/26.2/19.1 (BP=1.000, ratio=1.109, hyp_len=13568, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.92.0.56-1.75.0.46-1.58.1.81-6.10.1.43-4.19.pth, mybk
BLEU = 29.72, 56.7/35.2/23.7/16.5 (BP=1.000, ratio=1.070, hyp_len=12235, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.92.0.56-1.75.0.46-1.58.1.81-6.10.1.43-4.19.pth, bkmy
BLEU = 33.84, 59.4/39.5/27.6/20.3 (BP=1.000, ratio=1.071, hyp_len=13095, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.93.0.55-1.74.0.45-1.56.1.84-6.30.1.42-4.12.pth, mybk
BLEU = 30.71, 57.7/36.2/24.5/17.3 (BP=1.000, ratio=1.044, hyp_len=11937, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.93.0.55-1.74.0.45-1.56.1.84-6.30.1.42-4.12.pth, bkmy
BLEU = 33.96, 59.6/39.5/27.9/20.3 (BP=1.000, ratio=1.081, hyp_len=13219, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.94.0.56-1.75.0.45-1.57.1.86-6.43.1.46-4.32.pth, mybk
BLEU = 28.71, 55.0/33.8/22.7/16.1 (BP=1.000, ratio=1.065, hyp_len=12171, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.94.0.56-1.75.0.45-1.57.1.86-6.43.1.46-4.32.pth, bkmy
BLEU = 33.91, 58.4/38.9/27.8/21.0 (BP=1.000, ratio=1.067, hyp_len=13052, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.95.0.54-1.71.0.44-1.55.1.85-6.39.1.47-4.36.pth, mybk
BLEU = 29.39, 55.3/34.4/23.4/16.8 (BP=1.000, ratio=1.066, hyp_len=12185, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.95.0.54-1.71.0.44-1.55.1.85-6.39.1.47-4.36.pth, bkmy
BLEU = 33.68, 58.7/39.0/27.5/20.4 (BP=1.000, ratio=1.089, hyp_len=13315, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.96.0.54-1.71.0.44-1.55.1.83-6.25.1.44-4.20.pth, mybk
BLEU = 28.70, 55.5/34.1/22.6/15.9 (BP=1.000, ratio=1.069, hyp_len=12220, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.96.0.54-1.71.0.44-1.55.1.83-6.25.1.44-4.20.pth, bkmy
BLEU = 33.73, 59.1/39.1/27.5/20.4 (BP=1.000, ratio=1.075, hyp_len=13145, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.97.0.55-1.73.0.45-1.57.1.82-6.15.1.50-4.50.pth, mybk
BLEU = 29.98, 56.1/34.8/24.0/17.3 (BP=1.000, ratio=1.070, hyp_len=12237, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.97.0.55-1.73.0.45-1.57.1.82-6.15.1.50-4.50.pth, bkmy
BLEU = 35.10, 59.5/40.2/29.0/21.9 (BP=1.000, ratio=1.057, hyp_len=12929, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.98.0.55-1.73.0.46-1.58.1.82-6.14.1.45-4.27.pth, mybk
BLEU = 28.95, 55.0/34.1/23.0/16.3 (BP=1.000, ratio=1.075, hyp_len=12285, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.98.0.55-1.73.0.46-1.58.1.82-6.14.1.45-4.27.pth, bkmy
BLEU = 33.98, 58.7/39.2/27.9/20.8 (BP=1.000, ratio=1.090, hyp_len=13329, ref_len=12231)
Evaluation result for the model: dsl-model-mybk.99.0.54-1.72.0.43-1.54.1.81-6.12.1.48-4.39.pth, mybk
BLEU = 28.53, 54.6/33.5/22.6/16.1 (BP=1.000, ratio=1.092, hyp_len=12485, ref_len=11432)
Evaluation result for the model: dsl-model-mybk.99.0.54-1.72.0.43-1.54.1.81-6.12.1.48-4.39.pth, bkmy
BLEU = 33.96, 58.6/39.0/28.0/20.8 (BP=1.000, ratio=1.080, hyp_len=13215, ref_len=12231)
```

Transformer-DSL မော်ဒယ်အားလုံးအတွက် (30 epoch model to 100 epoch model) testing/evaluation အတွက် စုစုပေါင်း ကြာချိန်က အောက်ပါအတိုင်း  
```
real	299m2.840s
user	287m56.917s
sys	21m41.819s
```

Best model for my-bk က epoch 25 မော်ဒယ် ဖြစ်ပြီးတော့၊ Best BLEU Score က : 34.86   
Best model for bk-my က epoch 22 မော်ဒယ် ဖြစ်ပြီးတော့၊ Best BLEU Score က : 43.23    

## Reference

- [https://stackoverflow.com/questions/42703500/best-way-to-save-a-trained-model-in-pytorch](https://stackoverflow.com/questions/42703500/best-way-to-save-a-trained-model-in-pytorch)
- [(Yingce Xia et. al, 2017, Dual Supervised Learning)](https://arxiv.org/pdf/1707.00415.pdf)  
