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

```

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

```

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

```

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

```

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

```

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

```

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

```

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

```

## Reference

- [https://stackoverflow.com/questions/42703500/best-way-to-save-a-trained-model-in-pytorch](https://stackoverflow.com/questions/42703500/best-way-to-save-a-trained-model-in-pytorch)
- [(Yingce Xia et. al, 2017, Dual Supervised Learning)](https://arxiv.org/pdf/1707.00415.pdf)  