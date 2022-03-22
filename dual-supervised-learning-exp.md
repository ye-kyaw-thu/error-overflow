# Dual Supervised Learning Experiment

## Language Model Building

time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 16 --n_epochs 30 --max_length 100 --dropout .2 \
--word_vec_size 512 --hidden_size 768 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm1.pth

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
> --gpu_id 1 --batch_size 16 --n_epochs 30 --max_length 100 --dropout .2 \
> --word_vec_size 512 --hidden_size 768 --n_layers 4 --max_grad_norm 1e+8 \
> --model_fn ./model/lm/lm1.pth
{   'batch_size': 16,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 768,
    'lang': 'myrk',
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/lm/lm1.pth',
    'n_epochs': 30,
    'n_layers': 4,
    'off_autocast': False,
    'train': '/home/ye/exp/simple-nmt/data/train',
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 512}
[LanguageModel(
  (emb): Embedding(1642, 512, padding_idx=1)
  (rnn): LSTM(512, 768, num_layers=4, batch_first=True, dropout=0.2)
  (out): Linear(in_features=768, out_features=1642, bias=True)
  (log_softmax): LogSoftmax(dim=-1)
), LanguageModel(
  (emb): Embedding(1541, 512, padding_idx=1)
  (rnn): LSTM(512, 768, num_layers=4, batch_first=True, dropout=0.2)
  (out): Linear(in_features=768, out_features=1541, bias=True)
  (log_softmax): LogSoftmax(dim=-1)
)]
Epoch 1 - |param|=9.31e+02 |g_param|=7.58e+04 loss=3.7000e+00 ppl=40.45                                                 
Validation - loss=3.8523e+00 ppl=47.10 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=9.42e+02 |g_param|=7.51e+04 loss=3.2643e+00 ppl=26.16                                                 
Validation - loss=3.4790e+00 ppl=32.43 best_loss=3.8523e+00 best_ppl=47.10                                              
Epoch 3 - |param|=9.55e+02 |g_param|=1.57e+05 loss=3.0518e+00 ppl=21.15                                                 
Validation - loss=3.3538e+00 ppl=28.61 best_loss=3.4790e+00 best_ppl=32.43                                              
Epoch 4 - |param|=9.68e+02 |g_param|=1.40e+05 loss=2.8363e+00 ppl=17.05                                                 
Validation - loss=3.1028e+00 ppl=22.26 best_loss=3.3538e+00 best_ppl=28.61                                              
Epoch 5 - |param|=9.81e+02 |g_param|=1.61e+05 loss=2.6891e+00 ppl=14.72                                                 
Validation - loss=3.0968e+00 ppl=22.13 best_loss=3.1028e+00 best_ppl=22.26                                              
Epoch 6 - |param|=9.95e+02 |g_param|=2.38e+05 loss=2.5259e+00 ppl=12.50                                                 
Validation - loss=2.9632e+00 ppl=19.36 best_loss=3.0968e+00 best_ppl=22.13                                              
Epoch 7 - |param|=1.01e+03 |g_param|=1.69e+05 loss=2.4683e+00 ppl=11.80                                                 
Validation - loss=2.9826e+00 ppl=19.74 best_loss=2.9632e+00 best_ppl=19.36                                              
Epoch 8 - |param|=1.03e+03 |g_param|=1.60e+05 loss=2.3533e+00 ppl=10.52                                                 
Validation - loss=2.9299e+00 ppl=18.73 best_loss=2.9632e+00 best_ppl=19.36                                              
Epoch 9 - |param|=1.04e+03 |g_param|=1.92e+05 loss=2.1994e+00 ppl=9.02                                                  
Validation - loss=2.9509e+00 ppl=19.12 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 10 - |param|=1.06e+03 |g_param|=1.79e+05 loss=2.1607e+00 ppl=8.68                                                 
Validation - loss=2.9793e+00 ppl=19.67 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 11 - |param|=1.08e+03 |g_param|=1.82e+05 loss=2.1189e+00 ppl=8.32                                                 
Validation - loss=2.9815e+00 ppl=19.72 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 12 - |param|=1.09e+03 |g_param|=2.65e+05 loss=1.9626e+00 ppl=7.12                                                 
Validation - loss=3.0006e+00 ppl=20.10 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 13 - |param|=1.11e+03 |g_param|=1.95e+05 loss=1.9484e+00 ppl=7.02                                                 
Validation - loss=3.0413e+00 ppl=20.93 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 14 - |param|=1.13e+03 |g_param|=1.96e+05 loss=1.8306e+00 ppl=6.24                                                 
Validation - loss=3.1192e+00 ppl=22.63 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 15 - |param|=1.14e+03 |g_param|=2.29e+05 loss=1.7180e+00 ppl=5.57                                                 
Validation - loss=3.1043e+00 ppl=22.29 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 16 - |param|=1.16e+03 |g_param|=2.04e+05 loss=1.7089e+00 ppl=5.52                                                 
Validation - loss=3.1717e+00 ppl=23.85 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 17 - |param|=1.17e+03 |g_param|=2.15e+05 loss=1.6442e+00 ppl=5.18                                                 
Validation - loss=3.2505e+00 ppl=25.80 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 18 - |param|=1.19e+03 |g_param|=2.48e+05 loss=1.5497e+00 ppl=4.71                                                 
Validation - loss=3.2335e+00 ppl=25.37 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 19 - |param|=1.20e+03 |g_param|=1.92e+05 loss=1.5401e+00 ppl=4.67                                                 
Validation - loss=3.2704e+00 ppl=26.32 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 20 - |param|=1.22e+03 |g_param|=1.94e+05 loss=1.4871e+00 ppl=4.42                                                 
Validation - loss=3.3395e+00 ppl=28.20 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 21 - |param|=1.23e+03 |g_param|=2.27e+05 loss=1.3912e+00 ppl=4.02                                                 
Validation - loss=3.3574e+00 ppl=28.71 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 22 - |param|=1.24e+03 |g_param|=1.96e+05 loss=1.3767e+00 ppl=3.96                                                 
Validation - loss=3.4222e+00 ppl=30.64 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 23 - |param|=1.25e+03 |g_param|=1.99e+05 loss=1.3252e+00 ppl=3.76                                                 
Validation - loss=3.4620e+00 ppl=31.88 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 24 - |param|=1.27e+03 |g_param|=2.33e+05 loss=1.2673e+00 ppl=3.55                                                 
Validation - loss=3.4868e+00 ppl=32.68 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 25 - |param|=1.28e+03 |g_param|=1.93e+05 loss=1.2818e+00 ppl=3.60                                                 
Validation - loss=3.5292e+00 ppl=34.10 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 26 - |param|=1.29e+03 |g_param|=2.05e+05 loss=1.2191e+00 ppl=3.38                                                 
Validation - loss=3.5886e+00 ppl=36.18 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 27 - |param|=1.30e+03 |g_param|=2.41e+05 loss=1.1942e+00 ppl=3.30                                                 
Validation - loss=3.6250e+00 ppl=37.53 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 28 - |param|=1.31e+03 |g_param|=2.05e+05 loss=1.1919e+00 ppl=3.29                                                 
Validation - loss=3.6557e+00 ppl=38.70 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 29 - |param|=1.32e+03 |g_param|=1.75e+05 loss=1.1546e+00 ppl=3.17                                                 
Validation - loss=3.7111e+00 ppl=40.90 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 30 - |param|=1.33e+03 |g_param|=2.65e+05 loss=1.1298e+00 ppl=3.10                                                 
Validation - loss=3.7328e+00 ppl=41.80 best_loss=2.9299e+00 best_ppl=18.73                                              
Epoch 1 - |param|=8.99e+02 |g_param|=9.93e+04 loss=3.9619e+00 ppl=52.55                                                 
Validation - loss=4.0781e+00 ppl=59.03 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=9.14e+02 |g_param|=7.11e+04 loss=3.3609e+00 ppl=28.82                                                 
Validation - loss=3.5303e+00 ppl=34.13 best_loss=4.0781e+00 best_ppl=59.03                                              
Epoch 3 - |param|=9.27e+02 |g_param|=1.39e+05 loss=3.0843e+00 ppl=21.85                                                 
Validation - loss=3.2964e+00 ppl=27.01 best_loss=3.5303e+00 best_ppl=34.13                                              
Epoch 4 - |param|=9.40e+02 |g_param|=1.47e+05 loss=2.8885e+00 ppl=17.97                                                 
Validation - loss=3.1455e+00 ppl=23.23 best_loss=3.2964e+00 best_ppl=27.01                                              
Epoch 5 - |param|=9.54e+02 |g_param|=9.83e+04 loss=2.7825e+00 ppl=16.16                                                 
Validation - loss=3.0242e+00 ppl=20.58 best_loss=3.1455e+00 best_ppl=23.23                                              
Epoch 6 - |param|=9.69e+02 |g_param|=7.59e+04 loss=2.6783e+00 ppl=14.56                                                 
Validation - loss=3.0030e+00 ppl=20.15 best_loss=3.0242e+00 best_ppl=20.58                                              
Epoch 7 - |param|=9.85e+02 |g_param|=7.26e+04 loss=2.5380e+00 ppl=12.65                                                 
Validation - loss=2.9206e+00 ppl=18.55 best_loss=3.0030e+00 best_ppl=20.15                                              
Epoch 8 - |param|=1.00e+03 |g_param|=1.51e+05 loss=2.4290e+00 ppl=11.35                                                 
Validation - loss=2.8842e+00 ppl=17.89 best_loss=2.9206e+00 best_ppl=18.55                                              
Epoch 9 - |param|=1.02e+03 |g_param|=1.51e+05 loss=2.3206e+00 ppl=10.18                                                 
Validation - loss=2.8515e+00 ppl=17.31 best_loss=2.8842e+00 best_ppl=17.89                                              
Epoch 10 - |param|=1.04e+03 |g_param|=1.69e+05 loss=2.2420e+00 ppl=9.41                                                 
Validation - loss=2.8904e+00 ppl=18.00 best_loss=2.8515e+00 best_ppl=17.31                                              
Epoch 11 - |param|=1.05e+03 |g_param|=2.47e+05 loss=2.1297e+00 ppl=8.41                                                 
Validation - loss=2.8254e+00 ppl=16.87 best_loss=2.8515e+00 best_ppl=17.31                                              
Epoch 12 - |param|=1.07e+03 |g_param|=1.57e+05 loss=2.0441e+00 ppl=7.72                                                 
Validation - loss=2.8554e+00 ppl=17.38 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 13 - |param|=1.09e+03 |g_param|=1.52e+05 loss=1.9490e+00 ppl=7.02                                                 
Validation - loss=2.8559e+00 ppl=17.39 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 14 - |param|=1.10e+03 |g_param|=2.31e+05 loss=1.8812e+00 ppl=6.56                                                 
Validation - loss=2.8688e+00 ppl=17.62 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 15 - |param|=1.12e+03 |g_param|=1.66e+05 loss=1.8203e+00 ppl=6.17                                                 
Validation - loss=2.9135e+00 ppl=18.42 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 16 - |param|=1.14e+03 |g_param|=1.78e+05 loss=1.7194e+00 ppl=5.58                                                 
Validation - loss=2.9636e+00 ppl=19.37 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 17 - |param|=1.15e+03 |g_param|=2.01e+05 loss=1.6747e+00 ppl=5.34                                                 
Validation - loss=2.9447e+00 ppl=19.01 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 18 - |param|=1.17e+03 |g_param|=1.60e+05 loss=1.6271e+00 ppl=5.09                                                 
Validation - loss=2.9782e+00 ppl=19.65 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 19 - |param|=1.18e+03 |g_param|=1.03e+05 loss=1.5455e+00 ppl=4.69                                                 
Validation - loss=3.0118e+00 ppl=20.32 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 20 - |param|=1.19e+03 |g_param|=8.85e+04 loss=1.5462e+00 ppl=4.69                                                 
Validation - loss=3.0784e+00 ppl=21.72 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 21 - |param|=1.21e+03 |g_param|=9.08e+04 loss=1.4500e+00 ppl=4.26                                                 
Validation - loss=3.1272e+00 ppl=22.81 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 22 - |param|=1.22e+03 |g_param|=1.68e+05 loss=1.3921e+00 ppl=4.02                                                 
Validation - loss=3.1308e+00 ppl=22.89 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 23 - |param|=1.23e+03 |g_param|=9.08e+04 loss=1.3417e+00 ppl=3.83                                                 
Validation - loss=3.1573e+00 ppl=23.51 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 24 - |param|=1.25e+03 |g_param|=8.51e+04 loss=1.2997e+00 ppl=3.67                                                 
Validation - loss=3.1984e+00 ppl=24.49 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 25 - |param|=1.26e+03 |g_param|=8.74e+04 loss=1.3049e+00 ppl=3.69                                                 
Validation - loss=3.2433e+00 ppl=25.62 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 26 - |param|=1.27e+03 |g_param|=1.01e+05 loss=1.2319e+00 ppl=3.43                                                 
Validation - loss=3.2739e+00 ppl=26.41 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 27 - |param|=1.28e+03 |g_param|=7.85e+04 loss=1.2312e+00 ppl=3.43                                                 
Validation - loss=3.3270e+00 ppl=27.85 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 28 - |param|=1.29e+03 |g_param|=7.95e+04 loss=1.1765e+00 ppl=3.24                                                 
Validation - loss=3.3487e+00 ppl=28.47 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 29 - |param|=1.30e+03 |g_param|=1.89e+05 loss=1.1491e+00 ppl=3.16                                                 
Validation - loss=3.4161e+00 ppl=30.45 best_loss=2.8254e+00 best_ppl=16.87                                              
Epoch 30 - |param|=1.32e+03 |g_param|=1.62e+05 loss=1.1291e+00 ppl=3.09                                                 
Validation - loss=3.4141e+00 ppl=30.39 best_loss=2.8254e+00 best_ppl=16.87                                              

real	91m9.024s
user	91m0.094s
sys	0m6.828s
(simple-nmt) ye@:~/exp/simple-nmt$
```

```
(simple-nmt) ye@:~/exp/simple-nmt$ ll -h ./model/lm/lm1.pth
-rw-rw-r-- 1 ye ye 154M မတ်   20 12:00 ./model/lm/lm1.pth
```

## Language Model Training with Adjusted Parameters

အထက်ပါ ပထမဆုံး ဆောက်ခဲ့တဲ့ LM ကို သုံးပြီးတော့ dual supervised learning လုပ်ကြည့်တဲ့အခါမှာ memory မနိုင်တဲ့ ပြဿနာပေးနေလို့ LM ကို ရှေ့က ဆောက်ခဲ့တဲ့ seq2seq ရဲ့ parameter တွေနဲ့ ညှိပြီး နောက်တစ်ခေါက် LM ကို ဆောက်ခဲ့...  


time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 30 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm2.pth

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
> --gpu_id 1 --batch_size 64 --n_epochs 30 --max_length 100 --dropout .2 \
> --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
> --model_fn ./model/lm/lm2.pth
{   'batch_size': 64,
    'dropout': 0.2,
    'gpu_id': 1,
    'hidden_size': 128,
    'lang': 'myrk',
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/lm/lm2.pth',
    'n_epochs': 30,
    'n_layers': 4,
    'off_autocast': False,
    'train': '/home/ye/exp/simple-nmt/data/train',
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
[LanguageModel(
  (emb): Embedding(1642, 128, padding_idx=1)
  (rnn): LSTM(128, 128, num_layers=4, batch_first=True, dropout=0.2)
  (out): Linear(in_features=128, out_features=1642, bias=True)
  (log_softmax): LogSoftmax(dim=-1)
), LanguageModel(
  (emb): Embedding(1541, 128, padding_idx=1)
  (rnn): LSTM(128, 128, num_layers=4, batch_first=True, dropout=0.2)
  (out): Linear(in_features=128, out_features=1541, bias=True)
  (log_softmax): LogSoftmax(dim=-1)
)]
Epoch 1 - |param|=4.62e+02 |g_param|=1.44e+05 loss=4.5472e+00 ppl=94.37                                                 
Validation - loss=4.4097e+00 ppl=82.25 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=4.62e+02 |g_param|=1.12e+05 loss=4.4283e+00 ppl=83.79                                                 
Validation - loss=4.4956e+00 ppl=89.62 best_loss=4.4097e+00 best_ppl=82.25                                              
Epoch 3 - |param|=4.62e+02 |g_param|=1.03e+05 loss=4.4320e+00 ppl=84.10                                                 
Validation - loss=4.4248e+00 ppl=83.50 best_loss=4.4097e+00 best_ppl=82.25                                              
Epoch 4 - |param|=4.63e+02 |g_param|=1.04e+05 loss=4.4197e+00 ppl=83.07                                                 
Validation - loss=4.4446e+00 ppl=85.17 best_loss=4.4097e+00 best_ppl=82.25                                              
Epoch 5 - |param|=4.63e+02 |g_param|=9.23e+04 loss=4.3539e+00 ppl=77.78                                                 
Validation - loss=4.4124e+00 ppl=82.47 best_loss=4.4097e+00 best_ppl=82.25                                              
Epoch 6 - |param|=4.64e+02 |g_param|=8.75e+04 loss=4.2703e+00 ppl=71.54                                                 
Validation - loss=4.1470e+00 ppl=63.25 best_loss=4.4097e+00 best_ppl=82.25                                              
Epoch 7 - |param|=4.65e+02 |g_param|=7.43e+04 loss=4.0812e+00 ppl=59.22                                                 
Validation - loss=4.0361e+00 ppl=56.61 best_loss=4.1470e+00 best_ppl=63.25                                              
Epoch 8 - |param|=4.66e+02 |g_param|=5.90e+04 loss=3.8619e+00 ppl=47.56                                                 
Validation - loss=3.8239e+00 ppl=45.78 best_loss=4.0361e+00 best_ppl=56.61                                              
Epoch 9 - |param|=4.68e+02 |g_param|=5.47e+04 loss=3.6746e+00 ppl=39.43                                                 
Validation - loss=3.7045e+00 ppl=40.63 best_loss=3.8239e+00 best_ppl=45.78                                              
Epoch 10 - |param|=4.69e+02 |g_param|=5.14e+04 loss=3.6147e+00 ppl=37.14                                                
Validation - loss=3.6644e+00 ppl=39.03 best_loss=3.7045e+00 best_ppl=40.63                                              
Epoch 11 - |param|=4.70e+02 |g_param|=5.21e+04 loss=3.5470e+00 ppl=34.71                                                
Validation - loss=3.5640e+00 ppl=35.31 best_loss=3.6644e+00 best_ppl=39.03                                              
Epoch 12 - |param|=4.71e+02 |g_param|=9.92e+04 loss=3.5060e+00 ppl=33.32                                                
Validation - loss=3.5468e+00 ppl=34.70 best_loss=3.5640e+00 best_ppl=35.31                                              
Epoch 13 - |param|=4.72e+02 |g_param|=9.19e+04 loss=3.4479e+00 ppl=31.43                                                
Validation - loss=3.4910e+00 ppl=32.82 best_loss=3.5468e+00 best_ppl=34.70                                              
Epoch 14 - |param|=4.73e+02 |g_param|=9.44e+04 loss=3.3430e+00 ppl=28.30                                                
Validation - loss=3.4746e+00 ppl=32.28 best_loss=3.4910e+00 best_ppl=32.82                                              
Epoch 15 - |param|=4.74e+02 |g_param|=9.06e+04 loss=3.3264e+00 ppl=27.84                                                
Validation - loss=3.4056e+00 ppl=30.13 best_loss=3.4746e+00 best_ppl=32.28                                              
Epoch 16 - |param|=4.75e+02 |g_param|=8.97e+04 loss=3.2417e+00 ppl=25.58                                                
Validation - loss=3.3645e+00 ppl=28.92 best_loss=3.4056e+00 best_ppl=30.13                                              
Epoch 17 - |param|=4.76e+02 |g_param|=8.90e+04 loss=3.1940e+00 ppl=24.39                                                
Validation - loss=3.3526e+00 ppl=28.58 best_loss=3.3645e+00 best_ppl=28.92                                              
Epoch 18 - |param|=4.77e+02 |g_param|=9.60e+04 loss=3.1958e+00 ppl=24.43                                                
Validation - loss=3.3329e+00 ppl=28.02 best_loss=3.3526e+00 best_ppl=28.58                                              
Epoch 19 - |param|=4.78e+02 |g_param|=9.09e+04 loss=3.1653e+00 ppl=23.69                                                
Validation - loss=3.3088e+00 ppl=27.35 best_loss=3.3329e+00 best_ppl=28.02                                              
Epoch 20 - |param|=4.80e+02 |g_param|=9.17e+04 loss=3.1340e+00 ppl=22.97                                                
Validation - loss=3.2975e+00 ppl=27.05 best_loss=3.3088e+00 best_ppl=27.35                                              
Epoch 21 - |param|=4.81e+02 |g_param|=9.73e+04 loss=3.1004e+00 ppl=22.21                                                
Validation - loss=3.2418e+00 ppl=25.58 best_loss=3.2975e+00 best_ppl=27.05                                              
Epoch 22 - |param|=4.82e+02 |g_param|=1.85e+05 loss=3.0201e+00 ppl=20.49                                                
Validation - loss=3.2207e+00 ppl=25.05 best_loss=3.2418e+00 best_ppl=25.58                                              
Epoch 23 - |param|=4.83e+02 |g_param|=1.15e+05 loss=3.0226e+00 ppl=20.54                                                
Validation - loss=3.2251e+00 ppl=25.16 best_loss=3.2207e+00 best_ppl=25.05                                              
Epoch 24 - |param|=4.84e+02 |g_param|=1.02e+05 loss=3.0338e+00 ppl=20.78                                                
Validation - loss=3.1999e+00 ppl=24.53 best_loss=3.2207e+00 best_ppl=25.05                                              
Epoch 25 - |param|=4.85e+02 |g_param|=1.03e+05 loss=2.9738e+00 ppl=19.57                                                
Validation - loss=3.2339e+00 ppl=25.38 best_loss=3.1999e+00 best_ppl=24.53                                              
Epoch 26 - |param|=4.86e+02 |g_param|=9.72e+04 loss=2.9444e+00 ppl=19.00                                                
Validation - loss=3.1809e+00 ppl=24.07 best_loss=3.1999e+00 best_ppl=24.53                                              
Epoch 27 - |param|=4.87e+02 |g_param|=1.00e+05 loss=2.9080e+00 ppl=18.32                                                
Validation - loss=3.1893e+00 ppl=24.27 best_loss=3.1809e+00 best_ppl=24.07                                              
Epoch 28 - |param|=4.89e+02 |g_param|=1.04e+05 loss=2.9025e+00 ppl=18.22                                                
Validation - loss=3.1937e+00 ppl=24.38 best_loss=3.1809e+00 best_ppl=24.07                                              
Epoch 29 - |param|=4.90e+02 |g_param|=9.77e+04 loss=2.8358e+00 ppl=17.04                                                
Validation - loss=3.1347e+00 ppl=22.98 best_loss=3.1809e+00 best_ppl=24.07                                              
Epoch 30 - |param|=4.91e+02 |g_param|=1.02e+05 loss=2.8521e+00 ppl=17.32                                                
Validation - loss=3.1507e+00 ppl=23.35 best_loss=3.1347e+00 best_ppl=22.98                                              
Epoch 1 - |param|=4.46e+02 |g_param|=2.11e+05 loss=4.6308e+00 ppl=102.60                                                
Validation - loss=4.4291e+00 ppl=83.86 best_loss=inf best_ppl=inf                                                       
Epoch 2 - |param|=4.46e+02 |g_param|=1.04e+05 loss=4.4252e+00 ppl=83.53                                                 
Validation - loss=4.4667e+00 ppl=87.07 best_loss=4.4291e+00 best_ppl=83.86                                              
Epoch 3 - |param|=4.47e+02 |g_param|=1.01e+05 loss=4.4159e+00 ppl=82.76                                                 
Validation - loss=4.4863e+00 ppl=88.79 best_loss=4.4291e+00 best_ppl=83.86                                              
Epoch 4 - |param|=4.48e+02 |g_param|=9.51e+04 loss=4.1701e+00 ppl=64.72                                                 
Validation - loss=4.0614e+00 ppl=58.05 best_loss=4.4291e+00 best_ppl=83.86                                              
Epoch 5 - |param|=4.49e+02 |g_param|=5.67e+04 loss=3.8607e+00 ppl=47.50                                                 
Validation - loss=3.7625e+00 ppl=43.06 best_loss=4.0614e+00 best_ppl=58.05                                              
Epoch 6 - |param|=4.50e+02 |g_param|=5.69e+04 loss=3.7269e+00 ppl=41.55                                                 
Validation - loss=3.6587e+00 ppl=38.81 best_loss=3.7625e+00 best_ppl=43.06                                              
Epoch 7 - |param|=4.51e+02 |g_param|=4.82e+04 loss=3.5991e+00 ppl=36.56                                                 
Validation - loss=3.5558e+00 ppl=35.01 best_loss=3.6587e+00 best_ppl=38.81                                              
Epoch 8 - |param|=4.52e+02 |g_param|=5.17e+04 loss=3.5531e+00 ppl=34.92                                                 
Validation - loss=3.5144e+00 ppl=33.60 best_loss=3.5558e+00 best_ppl=35.01                                              
Epoch 9 - |param|=4.53e+02 |g_param|=4.88e+04 loss=3.4466e+00 ppl=31.39                                                 
Validation - loss=3.4503e+00 ppl=31.51 best_loss=3.5144e+00 best_ppl=33.60                                              
Epoch 10 - |param|=4.54e+02 |g_param|=4.90e+04 loss=3.4278e+00 ppl=30.81                                                
Validation - loss=3.4128e+00 ppl=30.35 best_loss=3.4503e+00 best_ppl=31.51                                              
Epoch 11 - |param|=4.55e+02 |g_param|=5.05e+04 loss=3.3698e+00 ppl=29.07                                                
Validation - loss=3.3871e+00 ppl=29.58 best_loss=3.4128e+00 best_ppl=30.35                                              
Epoch 12 - |param|=4.56e+02 |g_param|=9.48e+04 loss=3.2804e+00 ppl=26.59                                                
Validation - loss=3.3157e+00 ppl=27.54 best_loss=3.3871e+00 best_ppl=29.58                                              
Epoch 13 - |param|=4.57e+02 |g_param|=9.98e+04 loss=3.2902e+00 ppl=26.85                                                
Validation - loss=3.3145e+00 ppl=27.51 best_loss=3.3157e+00 best_ppl=27.54                                              
Epoch 14 - |param|=4.58e+02 |g_param|=1.04e+05 loss=3.2514e+00 ppl=25.83                                                
Validation - loss=3.2888e+00 ppl=26.81 best_loss=3.3145e+00 best_ppl=27.51                                              
Epoch 15 - |param|=4.59e+02 |g_param|=9.86e+04 loss=3.1933e+00 ppl=24.37                                                
Validation - loss=3.2558e+00 ppl=25.94 best_loss=3.2888e+00 best_ppl=26.81                                              
Epoch 16 - |param|=4.60e+02 |g_param|=1.04e+05 loss=3.1925e+00 ppl=24.35                                                
Validation - loss=3.2803e+00 ppl=26.58 best_loss=3.2558e+00 best_ppl=25.94                                              
Epoch 17 - |param|=4.61e+02 |g_param|=9.99e+04 loss=3.1625e+00 ppl=23.63                                                
Validation - loss=3.2411e+00 ppl=25.56 best_loss=3.2558e+00 best_ppl=25.94                                              
Epoch 18 - |param|=4.62e+02 |g_param|=1.00e+05 loss=3.0781e+00 ppl=21.72                                                
Validation - loss=3.1938e+00 ppl=24.38 best_loss=3.2411e+00 best_ppl=25.56                                              
Epoch 19 - |param|=4.63e+02 |g_param|=1.02e+05 loss=3.0444e+00 ppl=21.00                                                
Validation - loss=3.1538e+00 ppl=23.43 best_loss=3.1938e+00 best_ppl=24.38                                              
Epoch 20 - |param|=4.64e+02 |g_param|=9.94e+04 loss=3.0375e+00 ppl=20.85                                                
Validation - loss=3.1444e+00 ppl=23.20 best_loss=3.1538e+00 best_ppl=23.43                                              
Epoch 21 - |param|=4.65e+02 |g_param|=1.04e+05 loss=3.0158e+00 ppl=20.41                                                
Validation - loss=3.1211e+00 ppl=22.67 best_loss=3.1444e+00 best_ppl=23.20                                              
Epoch 22 - |param|=4.67e+02 |g_param|=2.09e+05 loss=2.9853e+00 ppl=19.79                                                
Validation - loss=3.1156e+00 ppl=22.55 best_loss=3.1211e+00 best_ppl=22.67                                              
Epoch 23 - |param|=4.68e+02 |g_param|=2.14e+05 loss=2.9465e+00 ppl=19.04                                                
Validation - loss=3.1032e+00 ppl=22.27 best_loss=3.1156e+00 best_ppl=22.55                                              
Epoch 24 - |param|=4.69e+02 |g_param|=2.13e+05 loss=2.9214e+00 ppl=18.57                                                
Validation - loss=3.0790e+00 ppl=21.74 best_loss=3.1032e+00 best_ppl=22.27                                              
Epoch 25 - |param|=4.70e+02 |g_param|=2.03e+05 loss=2.8675e+00 ppl=17.59                                                
Validation - loss=3.0540e+00 ppl=21.20 best_loss=3.0790e+00 best_ppl=21.74                                              
Epoch 26 - |param|=4.71e+02 |g_param|=2.03e+05 loss=2.8436e+00 ppl=17.18                                                
Validation - loss=3.0238e+00 ppl=20.57 best_loss=3.0540e+00 best_ppl=21.20                                              
Epoch 27 - |param|=4.73e+02 |g_param|=2.07e+05 loss=2.8094e+00 ppl=16.60                                                
Validation - loss=3.0223e+00 ppl=20.54 best_loss=3.0238e+00 best_ppl=20.57                                              
Epoch 28 - |param|=4.74e+02 |g_param|=2.14e+05 loss=2.8165e+00 ppl=16.72                                                
Validation - loss=3.0310e+00 ppl=20.72 best_loss=3.0223e+00 best_ppl=20.54                                              
Epoch 29 - |param|=4.75e+02 |g_param|=2.25e+05 loss=2.8309e+00 ppl=16.96                                                
Validation - loss=3.0626e+00 ppl=21.38 best_loss=3.0223e+00 best_ppl=20.54                                              
Epoch 30 - |param|=4.77e+02 |g_param|=2.17e+05 loss=2.7703e+00 ppl=15.96                                                
Validation - loss=2.9959e+00 ppl=20.00 best_loss=3.0223e+00 best_ppl=20.54                                              

real	3m39.891s
user	3m38.407s
sys	0m1.992s
(simple-nmt) ye@:~/exp/simple-nmt$
```

## Train Dual Supervised Learning

ပထမဆုံး စမ်း training လုပ်ကြည့်တာမို့လို့ e.g. command line ကို အနည်းငယ်ပဲ ပြင်ပြီးတော့ model ဆောက်ပေးနိုင်သလား၊ error ပေးသလား ဆိုတာကို confirmation လုပ်ခဲ့...  

time python dual_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 30 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 \
--dsl_n_warmup_epochs 20 --dsl_lambda 1e-2 \
--lm_fn ./model/lm/lm2.pth \
--model_fn ./model/dsl/dsl-model-myrk1.pth  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python dual_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
> --gpu_id 1 --batch_size 64 --n_epochs 30 --max_length 100 --dropout .2 \
> --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 \
> --dsl_n_warmup_epochs 20 --dsl_lambda 1e-2 \
> --lm_fn ./model/lm/lm2.pth \
> --model_fn ./model/dsl/dsl-model-myrk1.pth
{   'batch_size': 64,
    'dropout': 0.2,
    'dsl_lambda': 0.01,
    'dsl_n_warmup_epochs': 20,
    'gpu_id': 1,
    'hidden_size': 128,
    'init_epoch': 1,
    'iteration_per_update': 2,
    'lang': 'myrk',
    'lm_fn': './model/lm/lm2.pth',
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/dsl/dsl-model-myrk1.pth',
    'n_epochs': 30,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
[LanguageModel(
  (emb): Embedding(1642, 128, padding_idx=1)
  (rnn): LSTM(128, 128, num_layers=4, batch_first=True, dropout=0.2)
  (out): Linear(in_features=128, out_features=1642, bias=True)
  (log_softmax): LogSoftmax(dim=-1)
), LanguageModel(
  (emb): Embedding(1541, 128, padding_idx=1)
  (rnn): LSTM(128, 128, num_layers=4, batch_first=True, dropout=0.2)
  (out): Linear(in_features=128, out_features=1541, bias=True)
  (log_softmax): LogSoftmax(dim=-1)
)]
[Seq2Seq(
  (emb_src): Embedding(1541, 128)
  (emb_dec): Embedding(1642, 128)
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
    (output): Linear(in_features=128, out_features=1642, bias=True)
    (softmax): LogSoftmax(dim=-1)
  )
), Seq2Seq(
  (emb_src): Embedding(1642, 128)
  (emb_dec): Embedding(1541, 128)
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
    (output): Linear(in_features=128, out_features=1541, bias=True)
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
Epoch 1 - |param|=9.09e+02 |g_param|=2.34e+05 loss_x2y=4.4305e+00 ppl_x2y=83.97 loss_y2x=4.4450e+00 ppl_y2x=85.20 dual_loss=0.0000e+00
Validation X2Y - loss=4.0416e+00 ppl=56.92 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=4.0672e+00 ppl=58.39 best_loss=inf best_ppl=inf
Epoch 2 - |param|=9.09e+02 |g_param|=1.96e+05 loss_x2y=4.1231e+00 ppl_x2y=61.75 loss_y2x=4.1513e+00 ppl_y2x=63.51 dual_loss=0.0000e+00
Validation X2Y - loss=3.8715e+00 ppl=48.02 best_loss=4.0416e+00 best_ppl=56.92                                          
Validation Y2X - loss=3.8931e+00 ppl=49.06 best_loss=4.0672e+00 best_ppl=58.39
Epoch 3 - |param|=9.09e+02 |g_param|=2.13e+05 loss_x2y=4.0006e+00 ppl_x2y=54.63 loss_y2x=4.0434e+00 ppl_y2x=57.02 dual_loss=0.0000e+00
Validation X2Y - loss=3.7450e+00 ppl=42.31 best_loss=3.8715e+00 best_ppl=48.02                                          
Validation Y2X - loss=3.8132e+00 ppl=45.30 best_loss=3.8931e+00 best_ppl=49.06
Epoch 4 - |param|=9.10e+02 |g_param|=1.97e+05 loss_x2y=3.8390e+00 ppl_x2y=46.48 loss_y2x=3.9306e+00 ppl_y2x=50.94 dual_loss=0.0000e+00
Validation X2Y - loss=3.6128e+00 ppl=37.07 best_loss=3.7450e+00 best_ppl=42.31                                          
Validation Y2X - loss=3.7277e+00 ppl=41.58 best_loss=3.8132e+00 best_ppl=45.30
Epoch 5 - |param|=9.10e+02 |g_param|=2.13e+05 loss_x2y=3.7566e+00 ppl_x2y=42.80 loss_y2x=3.8839e+00 ppl_y2x=48.61 dual_loss=0.0000e+00
Validation X2Y - loss=3.5253e+00 ppl=33.96 best_loss=3.6128e+00 best_ppl=37.07                                          
Validation Y2X - loss=3.6473e+00 ppl=38.37 best_loss=3.7277e+00 best_ppl=41.58
Epoch 6 - |param|=9.10e+02 |g_param|=2.26e+05 loss_x2y=3.6427e+00 ppl_x2y=38.19 loss_y2x=3.7887e+00 ppl_y2x=44.20 dual_loss=0.0000e+00
Validation X2Y - loss=3.4289e+00 ppl=30.84 best_loss=3.5253e+00 best_ppl=33.96                                          
Validation Y2X - loss=3.5922e+00 ppl=36.31 best_loss=3.6473e+00 best_ppl=38.37
Epoch 7 - |param|=9.11e+02 |g_param|=2.18e+05 loss_x2y=3.5416e+00 ppl_x2y=34.52 loss_y2x=3.7261e+00 ppl_y2x=41.52 dual_loss=0.0000e+00
Validation X2Y - loss=3.3051e+00 ppl=27.25 best_loss=3.4289e+00 best_ppl=30.84                                          
Validation Y2X - loss=3.4868e+00 ppl=32.68 best_loss=3.5922e+00 best_ppl=36.31
Epoch 8 - |param|=9.12e+02 |g_param|=2.50e+05 loss_x2y=3.4475e+00 ppl_x2y=31.42 loss_y2x=3.6750e+00 ppl_y2x=39.45 dual_loss=0.0000e+00
Validation X2Y - loss=3.1792e+00 ppl=24.03 best_loss=3.3051e+00 best_ppl=27.25                                          
Validation Y2X - loss=3.4062e+00 ppl=30.15 best_loss=3.4868e+00 best_ppl=32.68
Epoch 9 - |param|=9.13e+02 |g_param|=2.19e+05 loss_x2y=3.1566e+00 ppl_x2y=23.49 loss_y2x=3.4336e+00 ppl_y2x=30.99 dual_loss=0.0000e+00
Validation X2Y - loss=2.9644e+00 ppl=19.38 best_loss=3.1792e+00 best_ppl=24.03                                          
Validation Y2X - loss=3.2414e+00 ppl=25.57 best_loss=3.4062e+00 best_ppl=30.15
Epoch 10 - |param|=9.14e+02 |g_param|=3.34e+05 loss_x2y=3.0565e+00 ppl_x2y=21.25 loss_y2x=3.3154e+00 ppl_y2x=27.53 dual_loss=0.0000e+00
Validation X2Y - loss=2.8790e+00 ppl=17.80 best_loss=2.9644e+00 best_ppl=19.38                                          
Validation Y2X - loss=3.1039e+00 ppl=22.28 best_loss=3.2414e+00 best_ppl=25.57
Epoch 11 - |param|=9.15e+02 |g_param|=2.15e+05 loss_x2y=2.7885e+00 ppl_x2y=16.26 loss_y2x=3.0846e+00 ppl_y2x=21.86 dual_loss=0.0000e+00
Validation X2Y - loss=2.6010e+00 ppl=13.48 best_loss=2.8790e+00 best_ppl=17.80                                          
Validation Y2X - loss=2.8509e+00 ppl=17.30 best_loss=3.1039e+00 best_ppl=22.28
Epoch 12 - |param|=9.16e+02 |g_param|=1.97e+05 loss_x2y=2.5465e+00 ppl_x2y=12.76 loss_y2x=2.7997e+00 ppl_y2x=16.44 dual_loss=0.0000e+00
Validation X2Y - loss=2.4079e+00 ppl=11.11 best_loss=2.6010e+00 best_ppl=13.48                                          
Validation Y2X - loss=2.6007e+00 ppl=13.47 best_loss=2.8509e+00 best_ppl=17.30
Epoch 13 - |param|=9.17e+02 |g_param|=2.69e+05 loss_x2y=2.4800e+00 ppl_x2y=11.94 loss_y2x=2.5884e+00 ppl_y2x=13.31 dual_loss=0.0000e+00
Validation X2Y - loss=2.4282e+00 ppl=11.34 best_loss=2.4079e+00 best_ppl=11.11                                          
Validation Y2X - loss=2.4224e+00 ppl=11.27 best_loss=2.6007e+00 best_ppl=13.47
Epoch 14 - |param|=9.18e+02 |g_param|=1.67e+05 loss_x2y=2.2431e+00 ppl_x2y=9.42 loss_y2x=2.4169e+00 ppl_y2x=11.21 dual_loss=0.0000e+00
Validation X2Y - loss=2.1837e+00 ppl=8.88 best_loss=2.4079e+00 best_ppl=11.11                                           
Validation Y2X - loss=2.3210e+00 ppl=10.19 best_loss=2.4224e+00 best_ppl=11.27
Epoch 15 - |param|=9.19e+02 |g_param|=2.31e+05 loss_x2y=2.2584e+00 ppl_x2y=9.57 loss_y2x=2.3212e+00 ppl_y2x=10.19 dual_loss=0.0000e+00
Validation X2Y - loss=2.2727e+00 ppl=9.71 best_loss=2.1837e+00 best_ppl=8.88                                            
Validation Y2X - loss=2.1831e+00 ppl=8.87 best_loss=2.3210e+00 best_ppl=10.19
Epoch 16 - |param|=9.19e+02 |g_param|=1.74e+05 loss_x2y=2.0684e+00 ppl_x2y=7.91 loss_y2x=2.0913e+00 ppl_y2x=8.10 dual_loss=0.0000e+00
Validation X2Y - loss=2.0099e+00 ppl=7.46 best_loss=2.1837e+00 best_ppl=8.88                                            
Validation Y2X - loss=1.9749e+00 ppl=7.21 best_loss=2.1831e+00 best_ppl=8.87
Epoch 17 - |param|=9.20e+02 |g_param|=2.21e+05 loss_x2y=1.9329e+00 ppl_x2y=6.91 loss_y2x=1.8976e+00 ppl_y2x=6.67 dual_loss=0.0000e+00
Validation X2Y - loss=1.9265e+00 ppl=6.87 best_loss=2.0099e+00 best_ppl=7.46                                            
Validation Y2X - loss=1.8929e+00 ppl=6.64 best_loss=1.9749e+00 best_ppl=7.21
Epoch 18 - |param|=9.21e+02 |g_param|=2.14e+05 loss_x2y=1.8586e+00 ppl_x2y=6.41 loss_y2x=1.8951e+00 ppl_y2x=6.65 dual_loss=0.0000e+00
Validation X2Y - loss=1.8329e+00 ppl=6.25 best_loss=1.9265e+00 best_ppl=6.87                                            
Validation Y2X - loss=1.8077e+00 ppl=6.10 best_loss=1.8929e+00 best_ppl=6.64
Epoch 19 - |param|=9.22e+02 |g_param|=1.77e+05 loss_x2y=1.7039e+00 ppl_x2y=5.50 loss_y2x=1.6735e+00 ppl_y2x=5.33 dual_loss=0.0000e+00
Validation X2Y - loss=1.7367e+00 ppl=5.68 best_loss=1.8329e+00 best_ppl=6.25                                            
Validation Y2X - loss=1.6819e+00 ppl=5.38 best_loss=1.8077e+00 best_ppl=6.10
Epoch 20 - |param|=9.23e+02 |g_param|=2.02e+05 loss_x2y=1.6057e+00 ppl_x2y=4.98 loss_y2x=1.5791e+00 ppl_y2x=4.85 dual_loss=0.0000e+00
Validation X2Y - loss=1.7147e+00 ppl=5.56 best_loss=1.7367e+00 best_ppl=5.68                                            
Validation Y2X - loss=1.6078e+00 ppl=4.99 best_loss=1.6819e+00 best_ppl=5.38
Epoch 21 - |param|=9.24e+02 |g_param|=1.88e+05 loss_x2y=1.5936e+00 ppl_x2y=4.92 loss_y2x=1.6035e+00 ppl_y2x=4.97 dual_loss=1.1789e+00
Validation X2Y - loss=1.8196e+00 ppl=6.17 best_loss=1.7147e+00 best_ppl=5.56                                            
Validation Y2X - loss=1.5394e+00 ppl=4.66 best_loss=1.6078e+00 best_ppl=4.99
Epoch 22 - |param|=9.24e+02 |g_param|=1.94e+05 loss_x2y=1.6604e+00 ppl_x2y=5.26 loss_y2x=1.4369e+00 ppl_y2x=4.21 dual_loss=1.3082e+00
Validation X2Y - loss=1.6280e+00 ppl=5.09 best_loss=1.7147e+00 best_ppl=5.56                                            
Validation Y2X - loss=1.4100e+00 ppl=4.10 best_loss=1.5394e+00 best_ppl=4.66
Epoch 23 - |param|=9.25e+02 |g_param|=8.93e+04 loss_x2y=1.4219e+00 ppl_x2y=4.14 loss_y2x=1.3369e+00 ppl_y2x=3.81 dual_loss=8.0811e-01
Validation X2Y - loss=1.5285e+00 ppl=4.61 best_loss=1.6280e+00 best_ppl=5.09                                            
Validation Y2X - loss=1.3789e+00 ppl=3.97 best_loss=1.4100e+00 best_ppl=4.10
Epoch 24 - |param|=9.26e+02 |g_param|=1.09e+05 loss_x2y=1.5485e+00 ppl_x2y=4.70 loss_y2x=1.3084e+00 ppl_y2x=3.70 dual_loss=1.7499e+00
Validation X2Y - loss=1.5400e+00 ppl=4.66 best_loss=1.5285e+00 best_ppl=4.61                                            
Validation Y2X - loss=1.2992e+00 ppl=3.67 best_loss=1.3789e+00 best_ppl=3.97
Epoch 25 - |param|=9.26e+02 |g_param|=7.31e+04 loss_x2y=1.3484e+00 ppl_x2y=3.85 loss_y2x=1.2452e+00 ppl_y2x=3.47 dual_loss=8.4450e-01
Validation X2Y - loss=1.4514e+00 ppl=4.27 best_loss=1.5285e+00 best_ppl=4.61                                            
Validation Y2X - loss=1.2560e+00 ppl=3.51 best_loss=1.2992e+00 best_ppl=3.67
Epoch 26 - |param|=9.27e+02 |g_param|=6.24e+04 loss_x2y=1.2573e+00 ppl_x2y=3.52 loss_y2x=1.1104e+00 ppl_y2x=3.04 dual_loss=1.1369e+00
Validation X2Y - loss=1.5347e+00 ppl=4.64 best_loss=1.4514e+00 best_ppl=4.27                                            
Validation Y2X - loss=1.1740e+00 ppl=3.23 best_loss=1.2560e+00 best_ppl=3.51
Epoch 27 - |param|=9.28e+02 |g_param|=8.70e+04 loss_x2y=1.3564e+00 ppl_x2y=3.88 loss_y2x=1.1159e+00 ppl_y2x=3.05 dual_loss=1.7304e+00
Validation X2Y - loss=1.5102e+00 ppl=4.53 best_loss=1.4514e+00 best_ppl=4.27                                            
Validation Y2X - loss=1.1756e+00 ppl=3.24 best_loss=1.1740e+00 best_ppl=3.23
Epoch 28 - |param|=9.28e+02 |g_param|=6.63e+04 loss_x2y=1.3461e+00 ppl_x2y=3.84 loss_y2x=1.0609e+00 ppl_y2x=2.89 dual_loss=1.6333e+00
Validation X2Y - loss=1.3506e+00 ppl=3.86 best_loss=1.4514e+00 best_ppl=4.27                                            
Validation Y2X - loss=1.1094e+00 ppl=3.03 best_loss=1.1740e+00 best_ppl=3.23
Epoch 29 - |param|=9.29e+02 |g_param|=6.51e+04 loss_x2y=1.0872e+00 ppl_x2y=2.97 loss_y2x=1.0185e+00 ppl_y2x=2.77 dual_loss=7.8716e-01
Validation X2Y - loss=1.2833e+00 ppl=3.61 best_loss=1.3506e+00 best_ppl=3.86                                            
Validation Y2X - loss=1.1234e+00 ppl=3.08 best_loss=1.1094e+00 best_ppl=3.03
Epoch 30 - |param|=9.30e+02 |g_param|=5.60e+04 loss_x2y=1.0422e+00 ppl_x2y=2.84 loss_y2x=1.1132e+00 ppl_y2x=3.04 dual_loss=1.3050e+00
Validation X2Y - loss=1.2391e+00 ppl=3.45 best_loss=1.2833e+00 best_ppl=3.61                                            
Validation Y2X - loss=1.0957e+00 ppl=2.99 best_loss=1.1094e+00 best_ppl=3.03

real	19m41.507s
user	19m24.809s
sys	0m14.812s
(simple-nmt) ye@:~/exp/simple-nmt
```

testing/evaluatin ...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/dsl/30epoch$ time ./test-eval-loop.sh 
Evaluation result for the model: dsl-model-myrk1.01.4.43-83.97.4.45-85.20.4.04-56.92.4.07-58.39.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 13.7/0.1/0.0/0.0 (BP=1.000, ratio=1.003, hyp_len=23233, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.02.4.12-61.75.4.15-63.51.3.87-48.02.3.89-49.06.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 17.3/1.7/0.0/0.0 (BP=1.000, ratio=1.022, hyp_len=23678, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.03.4.00-54.63.4.04-57.02.3.75-42.31.3.81-45.30.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.8/2.0/0.0/0.0 (BP=1.000, ratio=1.001, hyp_len=23191, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.04.3.84-46.48.3.93-50.94.3.61-37.07.3.73-41.58.pth
BLEU = 0.36, 24.5/2.9/0.0/0.0 (BP=0.998, ratio=0.998, hyp_len=23123, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.05.3.76-42.80.3.88-48.61.3.53-33.96.3.65-38.37.pth
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 24.5/3.7/0.2/0.0 (BP=1.000, ratio=1.017, hyp_len=23546, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.06.3.64-38.19.3.79-44.20.3.43-30.84.3.59-36.31.pth
BLEU = 0.78, 27.2/4.7/0.5/0.0 (BP=1.000, ratio=1.014, hyp_len=23479, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.07.3.54-34.52.3.73-41.52.3.31-27.25.3.49-32.68.pth
BLEU = 1.55, 29.2/6.1/0.7/0.0 (BP=1.000, ratio=1.002, hyp_len=23202, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.08.3.45-31.42.3.68-39.45.3.18-24.03.3.41-30.15.pth
BLEU = 3.51, 32.8/8.9/1.8/0.3 (BP=1.000, ratio=1.010, hyp_len=23390, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.09.3.16-23.49.3.43-30.99.2.96-19.38.3.24-25.57.pth
BLEU = 5.43, 38.1/12.5/3.1/0.6 (BP=1.000, ratio=1.003, hyp_len=23228, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.10.3.06-21.25.3.32-27.53.2.88-17.80.3.10-22.28.pth
BLEU = 5.33, 38.7/13.2/2.9/0.5 (BP=1.000, ratio=1.025, hyp_len=23731, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.11.2.79-16.26.3.08-21.86.2.60-13.48.2.85-17.30.pth
BLEU = 10.70, 44.6/18.5/6.8/2.5 (BP=0.986, ratio=0.986, hyp_len=22842, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.12.2.55-12.76.2.80-16.44.2.41-11.11.2.60-13.47.pth
BLEU = 15.38, 48.8/23.2/10.5/4.7 (BP=1.000, ratio=1.011, hyp_len=23413, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.13.2.48-11.94.2.59-13.31.2.43-11.34.2.42-11.27.pth
BLEU = 14.93, 50.2/23.2/10.3/4.5 (BP=0.977, ratio=0.977, hyp_len=22628, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.14.2.24-9.42.2.42-11.21.2.18-8.88.2.32-10.19.pth
BLEU = 22.07, 55.4/30.1/16.3/8.7 (BP=1.000, ratio=1.000, hyp_len=23160, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.15.2.26-9.57.2.32-10.19.2.27-9.71.2.18-8.87.pth
BLEU = 19.61, 53.4/28.7/13.9/6.9 (BP=1.000, ratio=1.030, hyp_len=23844, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.16.2.07-7.91.2.09-8.10.2.01-7.46.1.97-7.21.pth
BLEU = 27.28, 60.6/35.8/21.1/12.3 (BP=0.996, ratio=0.996, hyp_len=23070, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.17.1.93-6.91.1.90-6.67.1.93-6.87.1.89-6.64.pth
BLEU = 30.81, 62.8/39.2/24.5/15.3 (BP=0.994, ratio=0.994, hyp_len=23014, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.18.1.86-6.41.1.90-6.65.1.83-6.25.1.81-6.10.pth
BLEU = 34.28, 65.1/42.1/27.7/18.2 (BP=1.000, ratio=1.001, hyp_len=23181, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.19.1.70-5.50.1.67-5.33.1.74-5.68.1.68-5.38.pth
BLEU = 38.30, 67.8/46.1/31.4/21.9 (BP=1.000, ratio=1.011, hyp_len=23407, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.20.1.61-4.98.1.58-4.85.1.71-5.56.1.61-4.99.pth
BLEU = 40.37, 69.0/48.0/33.6/23.8 (BP=1.000, ratio=1.012, hyp_len=23438, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.21.1.59-4.92.1.60-4.97.1.82-6.17.1.54-4.66.pth
BLEU = 35.37, 66.2/43.7/28.4/19.0 (BP=1.000, ratio=1.016, hyp_len=23519, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.22.1.66-5.26.1.44-4.21.1.63-5.09.1.41-4.10.pth
BLEU = 41.12, 69.4/48.9/34.2/24.6 (BP=1.000, ratio=1.024, hyp_len=23716, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.23.1.42-4.14.1.34-3.81.1.53-4.61.1.38-3.97.pth
BLEU = 46.44, 73.3/54.0/39.7/29.6 (BP=1.000, ratio=1.004, hyp_len=23257, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.24.1.55-4.70.1.31-3.70.1.54-4.66.1.30-3.67.pth
BLEU = 45.20, 72.4/53.4/38.1/28.3 (BP=1.000, ratio=1.026, hyp_len=23756, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.25.1.35-3.85.1.25-3.47.1.45-4.27.1.26-3.51.pth
BLEU = 50.70, 75.5/57.6/44.2/34.4 (BP=1.000, ratio=1.014, hyp_len=23495, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.26.1.26-3.52.1.11-3.04.1.53-4.64.1.17-3.23.pth
BLEU = 43.98, 72.3/52.4/37.0/26.6 (BP=1.000, ratio=1.014, hyp_len=23490, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.27.1.36-3.88.1.12-3.05.1.51-4.53.1.18-3.24.pth
BLEU = 47.44, 73.3/55.0/40.7/30.8 (BP=1.000, ratio=1.019, hyp_len=23602, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.28.1.35-3.84.1.06-2.89.1.35-3.86.1.11-3.03.pth
BLEU = 53.57, 77.6/60.6/47.1/37.2 (BP=1.000, ratio=1.010, hyp_len=23401, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.29.1.09-2.97.1.02-2.77.1.28-3.61.1.12-3.08.pth
BLEU = 56.94, 79.4/63.4/50.7/41.2 (BP=1.000, ratio=1.012, hyp_len=23441, ref_len=23160)
Evaluation result for the model: dsl-model-myrk1.30.1.04-2.84.1.11-3.04.1.24-3.45.1.10-2.99.pth
BLEU = 58.96, 80.4/65.2/52.9/43.5 (BP=1.000, ratio=1.010, hyp_len=23381, ref_len=23160)

real	10m2.445s
user	9m47.094s
sys	0m33.020s
(simple-nmt) ye@:~/exp/simple-nmt/model/dsl/30epoch$
```

## Can We Continue with Seq2Seq Model?!

ရှေ့မှာ ဆောက်ထားခဲ့တဲ့ baseline model တွေ ဖြစ်တဲ့ Seq2Seq/Transformer မော်ဒယ်တွေကို parse လုပ်ပြီးတော့ ```continue_dual_train.py``` နဲ့တော့ ဆက် training လုပ်လို့တော့ မရနိုင်ဘူးလို့ ယူဆတယ်။  
သေချာအောင် run ကြည့်ခဲ့...  

testing with seq2seq baseline model:  

seq2seq baseline မော်ဒယ်ကို training လုပ်ခဲ့တဲ့ command က အောက်ပါအတိုင်း  

```
time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 64 --n_epochs 40 --max_length 100 --dropout .2 --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0 --model_fn ./model/seq2seq/baseline/myrk-40epoch/seq-model-myrk.pth;
```

အကောင်းဆုံး BLEU score ပေးခဲ့တဲ့ path က အောက်ပါအတိုင်း...  

```
./model/seq2seq/baseline/myrk-40epoch/seq-model-myrk.40.0.55-1.74.0.89-2.44.pth  
```


```
time python continue_dual_train.py --load_fn ./model/seq2seq/baseline/myrk-40epoch/seq-model-myrk.40.0.55-1.74.0.89-2.44.pth --model_fn ./model/dsl/continue/seq-dsl-model-myrk-test.pth --lm_fn ./model/lm/lm2.pth --init_epoch 40 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100
```

run ကြည့်တော့ အောက်ပါအတိုင်း ERROR ပေးပြီး ရပ်သွားတာကို တွေ့ခဲ့ရ...  

```
(simple-nmt) ye@:~/exp/simple-nmt$ time python continue_dual_train.py --load_fn ./model/seq2seq/baseline/myrk-40epoch/seq-model-myrk.40.0.55-1.74.0.89-2.44.pth --model_fn ./model/dsl/continue/seq-dsl-model-myrk-test.pth --lm_fn ./model/lm/lm2.pth --init_epoch 40 --iteration_per_update 2 --max_grad_norm 1e+8 --n_epochs 100
WARNING!!! Argument "--lr" is not found in current argument parser.	Ignore saved value: 0.001
WARNING!!! Argument "--lr_step" is not found in current argument parser.	Ignore saved value: 0
WARNING!!! Argument "--lr_gamma" is not found in current argument parser.	Ignore saved value: 0.5
WARNING!!! Argument "--lr_decay_start" is not found in current argument parser.	Ignore saved value: 10
WARNING!!! Argument "--use_adam" is not found in current argument parser.	Ignore saved value: True
WARNING!!! Argument "--use_radam" is not found in current argument parser.	Ignore saved value: False
WARNING!!! Argument "--rl_lr" is not found in current argument parser.	Ignore saved value: 0.01
WARNING!!! Argument "--rl_n_samples" is not found in current argument parser.	Ignore saved value: 1
WARNING!!! Argument "--rl_n_epochs" is not found in current argument parser.	Ignore saved value: 0
WARNING!!! Argument "--rl_n_gram" is not found in current argument parser.	Ignore saved value: 6
WARNING!!! Argument "--rl_reward" is not found in current argument parser.	Ignore saved value: gleu
WARNING!!! Argument "--load_fn" is not found in saved model.	Use current value: ./model/seq2seq/baseline/myrk-40epoch/seq-model-myrk.40.0.55-1.74.0.89-2.44.pth
WARNING!!! You changed value for argument "--model_fn".	Use current value: ./model/dsl/continue/seq-dsl-model-myrk-test.pth
WARNING!!! Argument "--lm_fn" is not found in saved model.	Use current value: ./model/lm/lm2.pth
WARNING!!! You changed value for argument "--n_epochs".	Use current value: 100
WARNING!!! You changed value for argument "--init_epoch".	Use current value: 40
WARNING!!! Argument "--dsl_n_warmup_epochs" is not found in saved model.	Use current value: 2
WARNING!!! Argument "--dsl_lambda" is not found in saved model.	Use current value: 0.001
{   'batch_size': 64,
    'dropout': 0.2,
    'dsl_lambda': 0.001,
    'dsl_n_warmup_epochs': 2,
    'gpu_id': 0,
    'hidden_size': 128,
    'init_epoch': 40,
    'iteration_per_update': 2,
    'lang': 'myrk',
    'lm_fn': './model/lm/lm2.pth',
    'load_fn': './model/seq2seq/baseline/myrk-40epoch/seq-model-myrk.40.0.55-1.74.0.89-2.44.pth',
    'max_grad_norm': 100000000.0,
    'max_length': 100,
    'model_fn': './model/dsl/continue/seq-dsl-model-myrk-test.pth',
    'n_epochs': 100,
    'n_layers': 4,
    'n_splits': 8,
    'off_autocast': False,
    'train': '/home/ye/exp/simple-nmt/data/train',
    'use_transformer': False,
    'valid': '/home/ye/exp/simple-nmt/data/dev',
    'verbose': 2,
    'word_vec_size': 128}
Traceback (most recent call last):
  File "continue_dual_train.py", line 15, in <module>
    continue_main(config, main)
  File "/home/ye/exp/simple-nmt/continue_train.py", line 48, in continue_main
    main(config, model_weight=model_weight, opt_weight=opt_weight)
  File "/home/ye/exp/simple-nmt/dual_train.py", line 299, in main
    model.load_state_dict(w)
  File "/home/ye/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/nn/modules/module.py", line 1455, in load_state_dict
    state_dict = state_dict.copy()
AttributeError: 'str' object has no attribute 'copy'

real	0m1.132s
user	0m1.304s
sys	0m1.038s
(simple-nmt) ye@:~/exp/simple-nmt$
```

Error message တွေကနေ ဥပမာ "WARNING!!! Argument "--lm_fn" is not found in saved model.	Use current value: ./model/lm/lm2.pth" သိရတာက DSL နဲ့ training လုပ်ထားတာကိုပဲ ဆက် continue training လုပ်လို့ ရလိမ့်မယ်လို့...  

**အဲဒါကြောင့် RL လိုမျိုး မော်ဒယ် နှစ်ခုကို ဆင့်ပြီး continue လုပ်တဲ့ ပုံစံမျိုး graph တော့ မထုတ်တော့ပဲနဲ့ ဇယားနဲ့ပဲ seq2seq vs DSL ကိုပဲ နှိုင်းယှဉ်ပြဖို့ ဆုံးဖြတ်ခဲ့တယ်**

## Language Model Training with Various Epochs

language model ကိုလည်း epoch အမျိုးမျိုးနဲ့ ကစားပြီး DSL နဲ့ တွဲလို့ ရလိမ့်မယ်။  
DSL ရဲ့ Best socre ဘယ်လောက်ထိ ပေးနိုင်သလဲ ဆိုတာကိုလည်း သိဖို့အတွက်က LM ကိုတော့ epoch အမျိုးမျိုးနဲ့ ကစားသင့်တယ်။  


time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 40 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm-40epoch.pth | tee ./model/lm/lm-40epoch-training.log  

time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 50 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm-50epoch.pth | tee ./model/lm/lm-50epoch-training.log  

time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 60 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm-60epoch.pth | tee ./model/lm/lm-60epoch-training.log  

time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 70 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm-70epoch.pth | tee ./model/lm/lm-70epoch-training.log  

time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 80 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm-80epoch.pth | tee ./model/lm/lm-80epoch-training.log  

time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 90 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm-90epoch.pth | tee ./model/lm/lm-90epoch-training.log  

time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 100 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm-100epoch.pth | tee ./model/lm/lm-100epoch-training.log  

time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 110 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm-110epoch.pth | tee ./model/lm/lm-110epoch-training.log  

time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 120 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm-120epoch.pth | tee ./model/lm/lm-120epoch-training.log  

time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 130 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm-130epoch.pth | tee ./model/lm/lm-130epoch-training.log  

time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 140 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm-140epoch.pth | tee ./model/lm/lm-140epoch-training.log  

time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 150 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm-150epoch.pth | tee ./model/lm/lm-150epoch-training.log  

time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 160 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm-160epoch.pth | tee ./model/lm/lm-160epoch-training.log  

time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 170 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm-170epoch.pth | tee ./model/lm/lm-170epoch-training.log  

time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 180 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm-180epoch.pth | tee ./model/lm/lm-180epoch-training.log  

time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 190 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm-190epoch.pth | tee ./model/lm/lm-190epoch-training.log  

time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 200 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
--model_fn ./model/lm/lm-200epoch.pth | tee ./model/lm/lm-200epoch-training.log  

## Check ppl of LMs

```
(simple-nmt) ye@:~/exp/simple-nmt/model/lm$ for logFile in `ls lm*.log | sort -V`; do tail "$logFile" | head -n 7 | tail -n 2; done
Epoch 30 - |param|=4.77e+02 |g_param|=2.17e+05 loss=2.7703e+00 ppl=15.96                                                
Validation - loss=2.9959e+00 ppl=20.00 best_loss=3.0223e+00 best_ppl=20.54                                              
Epoch 40 - |param|=4.86e+02 |g_param|=2.37e+05 loss=2.6275e+00 ppl=13.84
Validation - loss=3.0482e+00 ppl=21.08 best_loss=3.0233e+00 best_ppl=20.56
Epoch 50 - |param|=5.04e+02 |g_param|=2.35e+05 loss=2.3557e+00 ppl=10.55
Validation - loss=2.8444e+00 ppl=17.19 best_loss=2.8591e+00 best_ppl=17.45
Epoch 60 - |param|=5.09e+02 |g_param|=2.50e+05 loss=2.4141e+00 ppl=11.18
Validation - loss=2.9472e+00 ppl=19.05 best_loss=2.9533e+00 best_ppl=19.17
Epoch 70 - |param|=5.28e+02 |g_param|=1.41e+05 loss=2.2017e+00 ppl=9.04
Validation - loss=2.9186e+00 ppl=18.52 best_loss=2.8766e+00 best_ppl=17.75
Epoch 80 - |param|=5.46e+02 |g_param|=2.75e+05 loss=2.2887e+00 ppl=9.86
Validation - loss=2.9465e+00 ppl=19.04 best_loss=2.9058e+00 best_ppl=18.28
Epoch 90 - |param|=5.72e+02 |g_param|=3.02e+05 loss=2.2898e+00 ppl=9.87
Validation - loss=3.0333e+00 ppl=20.76 best_loss=2.9816e+00 best_ppl=19.72
Epoch 100 - |param|=5.77e+02 |g_param|=2.94e+05 loss=2.1287e+00 ppl=8.40
Validation - loss=3.0035e+00 ppl=20.16 best_loss=2.9302e+00 best_ppl=18.73
Epoch 110 - |param|=5.90e+02 |g_param|=3.14e+05 loss=2.0215e+00 ppl=7.55
Validation - loss=2.9826e+00 ppl=19.74 best_loss=2.8707e+00 best_ppl=17.65
Epoch 120 - |param|=6.32e+02 |g_param|=3.18e+05 loss=2.0920e+00 ppl=8.10
Validation - loss=3.0870e+00 ppl=21.91 best_loss=2.9648e+00 best_ppl=19.39
Epoch 130 - |param|=6.20e+02 |g_param|=2.76e+05 loss=1.9894e+00 ppl=7.31
Validation - loss=3.1016e+00 ppl=22.23 best_loss=2.9528e+00 best_ppl=19.16
Epoch 140 - |param|=6.69e+02 |g_param|=3.13e+05 loss=2.0294e+00 ppl=7.61
Validation - loss=3.1058e+00 ppl=22.33 best_loss=2.9790e+00 best_ppl=19.67
Epoch 150 - |param|=6.44e+02 |g_param|=1.77e+05 loss=1.9434e+00 ppl=6.98
Validation - loss=3.1154e+00 ppl=22.54 best_loss=2.9187e+00 best_ppl=18.52
Epoch 160 - |param|=6.83e+02 |g_param|=1.61e+05 loss=1.9917e+00 ppl=7.33
Validation - loss=3.1295e+00 ppl=22.86 best_loss=2.9526e+00 best_ppl=19.16
Epoch 170 - |param|=6.62e+02 |g_param|=1.83e+05 loss=1.8888e+00 ppl=6.61
Validation - loss=3.1223e+00 ppl=22.70 best_loss=2.9304e+00 best_ppl=18.74
Epoch 180 - |param|=6.96e+02 |g_param|=3.59e+05 loss=1.8745e+00 ppl=6.52
Validation - loss=3.1463e+00 ppl=23.25 best_loss=2.9091e+00 best_ppl=18.34
Epoch 190 - |param|=6.96e+02 |g_param|=1.77e+05 loss=1.8491e+00 ppl=6.35
Validation - loss=3.1808e+00 ppl=24.07 best_loss=2.9306e+00 best_ppl=18.74
Epoch 200 - |param|=7.15e+02 |g_param|=3.41e+05 loss=1.8571e+00 ppl=6.41
Validation - loss=3.1301e+00 ppl=22.88 best_loss=2.9116e+00 best_ppl=18.39
(simple-nmt) ye@:~/exp/simple-nmt/model/lm$
```

print and save training ppl values...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/lm$ export no=20; \
> for logFile in `ls lm*.log | sort -V`; do no=$((no+10)); \
> tail "$logFile" | head -n 7 | tail -n 2| cut -d"=" -f5 |\
> sed -n 'p;n' | nl -v $no ; done | tee  train-ppl.txt
    30	15.96                                                
    40	13.84
    50	10.55
    60	11.18
    70	9.04
    80	9.86
    90	9.87
   100	8.40
   110	7.55
   120	8.10
   130	7.31
   140	7.61
   150	6.98
   160	7.33
   170	6.61
   180	6.52
   190	6.35
   200	6.41
(simple-nmt) ye@:~/exp/simple-nmt/model/lm$
```

print and save validation ppl values...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/lm$ export no=20; \
> for logFile in `ls lm*.log | sort -V`; do no=$((no+10)); \
> tail "$logFile" | head -n 7 | tail -n 2| cut -d"=" -f5 | \
> sed -n 'n;p' | nl -v $no ; done | tee  validation-ppl.txt
    30	20.54                                              
    40	20.56
    50	17.45
    60	19.17
    70	17.75
    80	18.28
    90	19.72
   100	18.73
   110	17.65
   120	19.39
   130	19.16
   140	19.67
   150	18.52
   160	19.16
   170	18.74
   180	18.34
   190	18.74
   200	18.39
(simple-nmt) ye@:~/exp/simple-nmt/model/lm$
```

## Prepare a Python Script for Drawing a Graph

```python
import matplotlib.pyplot as plt
import numpy as np
from scipy.interpolate import make_interp_spline
import os
import sys

# Written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Last Updated: 21 Mar 2022 @Lab
# How to Run: python ./draw-raw.py ./train-ppl.txt ./validation-ppl.txt "Perplexity vs Number of Epochs" ppl-vs-epochs
# Ref:
# https://www.quora.com/How-do-you-plot-one-line-with-two-different-colours-using-Python-matplotlib-Python-matplotlib-development
# https://stackoverflow.com/questions/48425278/plotting-data-from-two-columns-in-a-txt-file-python
# https://www.geeksforgeeks.org/how-to-plot-a-smooth-curve-in-matplotlib/
# https://stackoverflow.com/questions/19023512/error-with-reading-float-from-two-column-text-file-into-an-array-in-python

model1_result = sys.argv[1]
model2_result = sys.argv[2]
graph_title = sys.argv[3]
output_filename = sys.argv[4]

data1 = np.loadtxt(model1_result)

x1 = data1[:,0]
y1 = data1[:,1]

data2 = np.loadtxt(model2_result)

x2 = data2[:,0]
y2 = data2[:,1]

# Plotting the Graph
plt.plot(x1, y1)
plt.plot(x2, y2)
plt.title(graph_title)
plt.xlabel('epoch')
plt.ylabel('ppl (perplexity)')
#plt.annotate(xy=[40,1], s='start RL here')
plt.legend(['training', 'validation'], loc=3)

plt.savefig(output_filename + '.png')
plt.savefig(output_filename + '.pdf')

plt.show()
```

## PPL vs Epochs Graph for Rakhine

```
(simple-nmt) ye@:~/exp/simple-nmt/model/lm$ python ./draw-raw.py ./train-ppl.txt ./validation-ppl.txt "Perplexity vs Number of Epochs" ppl-vs-epochs
```

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/DSL-exp/ppl-vs-epochs-raw.png" alt="ppl vs epoch graph for Rakhine" width="500"/> 
</p>  
<div align="center">
  Fig.1 PPL vs epochs for neural language model of Rakhine language
</div> 

<br />

## Language Model Building for Myanmar Language

ဒီတစ်ခါတော့ bash shell script တစ်ပုဒ်ကို အောက်ပါအတိုင်း ရေးခဲ့...   

```bash
#!/bin/bash

## Written by Ye, LST, NECTEC, Thailand
## Last updated: 21 Mar 2022
## for Neural LM building

for i in {30..200..10}
do

   echo "LM building with ${i} epochs ...";
   time python lm_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang rkmy \
   --gpu_id 1 --batch_size 64 --n_epochs ${i} --max_length 100 --dropout .2 \
   --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 \
   --model_fn ./model/lm/my/lm-${i}epoch-my.pth | tee ./model/lm/my/lm-${i}epoch-training-my.log  

   ls ./model/lm/my/lm-${i}epoch-my.pth 
   tail ./model/lm/lm-${i}epoch-training-my.log 
done
```

အထက်ပါ shell ကို run ခဲ့ပြီး ရလာတဲ့ language model တွေက အောက်ပါအတိုင်း...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/lm/my$ ll -h *.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 09:25 lm-100epoch-my.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 09:38 lm-110epoch-my.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 09:53 lm-120epoch-my.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 10:08 lm-130epoch-my.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 10:25 lm-140epoch-my.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 10:44 lm-150epoch-my.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 11:03 lm-160epoch-my.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 11:24 lm-170epoch-my.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 11:46 lm-180epoch-my.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 12:09 lm-190epoch-my.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 12:37 lm-200epoch-my.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 08:25 lm-30epoch-my.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 08:30 lm-40epoch-my.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 08:36 lm-50epoch-my.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 08:44 lm-60epoch-my.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 08:52 lm-70epoch-my.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 09:02 lm-80epoch-my.pth
-rw-rw-r-- 1 ye ye 7.3M မတ်   21 09:12 lm-90epoch-my.pth
```

log file output က အောက်ပါအတိုင်း...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/lm/my$ ll -h *.log
-rw-rw-r-- 1 ye ye  30K မတ်   21 09:25 lm-100epoch-training-my.log
-rw-rw-r-- 1 ye ye  33K မတ်   21 09:38 lm-110epoch-training-my.log
-rw-rw-r-- 1 ye ye  36K မတ်   21 09:53 lm-120epoch-training-my.log
-rw-rw-r-- 1 ye ye  39K မတ်   21 10:08 lm-130epoch-training-my.log
-rw-rw-r-- 1 ye ye  42K မတ်   21 10:25 lm-140epoch-training-my.log
-rw-rw-r-- 1 ye ye  45K မတ်   21 10:44 lm-150epoch-training-my.log
-rw-rw-r-- 1 ye ye  48K မတ်   21 11:03 lm-160epoch-training-my.log
-rw-rw-r-- 1 ye ye  50K မတ်   21 11:24 lm-170epoch-training-my.log
-rw-rw-r-- 1 ye ye  53K မတ်   21 11:46 lm-180epoch-training-my.log
-rw-rw-r-- 1 ye ye  56K မတ်   21 12:09 lm-190epoch-training-my.log
-rw-rw-r-- 1 ye ye  59K မတ်   21 12:37 lm-200epoch-training-my.log
-rw-rw-r-- 1 ye ye 9.6K မတ်   21 08:25 lm-30epoch-training-my.log
-rw-rw-r-- 1 ye ye  13K မတ်   21 08:30 lm-40epoch-training-my.log
-rw-rw-r-- 1 ye ye  16K မတ်   21 08:36 lm-50epoch-training-my.log
-rw-rw-r-- 1 ye ye  19K မတ်   21 08:44 lm-60epoch-training-my.log
-rw-rw-r-- 1 ye ye  22K မတ်   21 08:52 lm-70epoch-training-my.log
-rw-rw-r-- 1 ye ye  24K မတ်   21 09:02 lm-80epoch-training-my.log
-rw-rw-r-- 1 ye ye  27K မတ်   21 09:12 lm-90epoch-training-my.log
(simple-nmt) ye@:~/exp/simple-nmt/model/lm/my$
```

## PPL vs Epochs Graph for Rakhine

```
(simple-nmt) ye@:~/exp/simple-nmt/model/lm/my$ export no=20; for logFile in `ls lm*.log | sort -V`; do no=$((no+10)); tail -n 2 "$logFile" | cut -d"=" -f5 |sed -n 'p;n' | nl -v $no ; done | tee  train-ppl.txt
    30	19.46
    40	13.69
    50	11.99
    60	11.11
    70	10.14
    80	10.03
    90	8.72
   100	9.12
   110	8.14
   120	8.38
   130	7.90
   140	7.26
   150	7.07
   160	7.07
   170	7.01
   180	6.49
   190	6.10
   200	6.11
(simple-nmt) ye@:~/exp/simple-nmt/model/lm/my$
```

```
(simple-nmt) ye@:~/exp/simple-nmt/model/lm/my$ export no=20; \
> for logFile in `ls lm*.log | sort -V`; do no=$((no+10)); \
> tail -n 2 "$logFile" | cut -d"=" -f5 | \
> sed -n 'n;p' | nl -v $no ; done | tee  validation-ppl.txt
    30	25.28
    40	21.20
    50	20.75
    60	20.87
    70	20.73
    80	21.24
    90	19.89
   100	20.99
   110	20.98
   120	21.94
   130	21.35
   140	20.51
   150	20.61
   160	20.74
   170	21.01
   180	19.93
   190	19.87
   200	19.73
(simple-nmt) ye@:~/exp/simple-nmt/model/lm/my$
```

python script ကို run ခဲ့...  

```
(simple-nmt) ye@:~/exp/simple-nmt/model/lm/my$ python ./draw-raw.py ./train-ppl.txt ./validation-ppl.txt "Perplexity vs Number of Epochs" ppl-vs-epochs-raw-my
```


<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/DSL-exp/ppl-vs-epochs-raw-my.png" alt="ppl vs epoch graph for Myanmar" width="500"/> 
</p>  
<div align="center">
  Fig.1 PPL vs epochs for neural language model of Myanmar language
</div> 

<br />

## Updating test-eval Shell Script

DSL မော်ဒယ်က X-Y, Y-X (ဆိုလိုတာက source-to-target, target-to-source) ကို တပြိုင်နက်တည်း training လုပ်တာမို့လို့ test-eval အတွက်ရေးထားတဲ့ shell script ကို update လုပ်ဖို့ လိုအပ်တယ်။ အောက်ပါအတိုင်း update လုပ်ခဲ့တယ်...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Last Updated: 21 Mar 2022
# find all trained models and parse source/target to translate.py for testing and multi-bleu.perl for evaluation with BLEU score
# *** trained models are Dual Supervised Learning models and thus it support source-to-target and target-to-source testing or translation

for i in *.pth; do
   MODEL=$i;

   # Testing X-Y
   python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang myrk < /home/ye/exp/simple-nmt/data/test.my > $MODEL.myrk.hyp

   # Evaluation with BLEU Score
   echo "Evaluation result for the model: $MODEL, myrk" | tee -a eval-results-xy.txt;
   cat $MODEL.myrk.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/test.rk | tee  -a eval-results-xy.txt;

   # Testing Y-X
   python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang rkmy < /home/ye/exp/simple-nmt/data/test.rk > $MODEL.rkmy.hyp

   # Evaluation with BLEU Score
   echo "Evaluation result for the model: $MODEL, rkmy" | tee -a eval-results-yx.txt;
   cat $MODEL.rkmy.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/test.my | tee  -a eval-results-yx.txt;
done
```

## Thinking

အဲဒါဆိုရင် LM ကလည်း source, target သပ်သပ်ခွဲစရာ မလိုဘူးလို့ ယူဆတယ်။ bi-directional သွားထားတာလို့ ယူဆတယ်။  
စာတမ်းကို ဖတ်ရန်၊ code ကို ကြည့်ရန်...    


## DSL with Seq2Seq

### with LM 200 Epoch

#### Warmup-Epoch 20, Total Epoch 30


time python dual_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev \
--lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 30 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 \
--dsl_n_warmup_epochs 20 --dsl_lambda 1e-2 \
--lm_fn ./model/lm/lm-200epoch.pth \
--model_fn ./model/dsl/myrk-30epoch/dsl-model-myrk.pth | tee ./model/dsl/myrk-30epoch/training.log

```
Epoch 30 - |param|=9.28e+02 |g_param|=1.00e+05 loss_x2y=8.3242e-01 ppl_x2y=2.30 loss_y2x=9.4779e-01 ppl_y2x=2.58 dual_loss=1.5505e+00
Validation X2Y - loss=9.6003e-01 ppl=2.61 best_loss=9.9560e-01 best_ppl=2.71                                            
Validation Y2X - loss=9.4432e-01 ppl=2.57 best_loss=9.8890e-01 best_ppl=2.69
```

testing/evaluation...  

```
(base) ye@:~/exp/simple-nmt/model/dsl/myrk-30epoch$ time ./test-eval-loop-xy.sh 
Evaluation result for the model: dsl-model-myrk.01.4.40-81.45.4.46-86.43.4.02-55.89.4.10-60.07.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 14.6/1.6/0.0/0.0 (BP=1.000, ratio=1.107, hyp_len=25643, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.01.4.40-81.45.4.46-86.43.4.02-55.89.4.10-60.07.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 15.0/0.4/0.0/0.0 (BP=1.000, ratio=1.103, hyp_len=25922, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.02.4.12-61.39.4.17-64.58.3.87-47.93.3.91-50.02.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.6/2.0/0.0/0.0 (BP=1.000, ratio=1.003, hyp_len=23238, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.02.4.12-61.39.4.17-64.58.3.87-47.93.3.91-50.02.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.1/1.9/0.0/0.0 (BP=0.984, ratio=0.984, hyp_len=23139, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.03.4.02-55.63.4.07-58.54.3.77-43.43.3.84-46.64.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.8/1.7/0.0/0.0 (BP=1.000, ratio=1.010, hyp_len=23396, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.03.4.02-55.63.4.07-58.54.3.77-43.43.3.84-46.64.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.3/2.2/0.0/0.0 (BP=0.983, ratio=0.983, hyp_len=23107, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.04.3.89-48.93.3.97-53.15.3.63-37.73.3.73-41.71.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.8/2.2/0.0/0.0 (BP=1.000, ratio=1.002, hyp_len=23209, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.04.3.89-48.93.3.97-53.15.3.63-37.73.3.73-41.71.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.7/2.6/0.3/0.0 (BP=0.978, ratio=0.979, hyp_len=23005, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.05.3.77-43.58.3.89-49.16.3.52-33.77.3.65-38.53.pth, myrk
BLEU = 0.96, 25.3/4.1/0.4/0.0 (BP=1.000, ratio=1.009, hyp_len=23359, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.05.3.77-43.58.3.89-49.16.3.52-33.77.3.65-38.53.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.6/3.7/0.3/0.0 (BP=0.974, ratio=0.974, hyp_len=22903, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.06.3.68-39.70.3.81-45.37.3.44-31.25.3.58-35.79.pth, myrk
BLEU = 1.34, 28.1/5.3/0.6/0.0 (BP=0.997, ratio=0.997, hyp_len=23096, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.06.3.68-39.70.3.81-45.37.3.44-31.25.3.58-35.79.pth, rkmy
BLEU = 0.65, 22.3/3.8/0.4/0.0 (BP=1.000, ratio=1.023, hyp_len=24055, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.07.3.54-34.53.3.70-40.44.3.30-27.05.3.46-31.85.pth, myrk
BLEU = 2.76, 30.8/7.6/1.3/0.2 (BP=0.999, ratio=0.999, hyp_len=23144, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.07.3.54-34.53.3.70-40.44.3.30-27.05.3.46-31.85.pth, rkmy
BLEU = 1.80, 26.4/5.3/0.8/0.1 (BP=0.998, ratio=0.998, hyp_len=23461, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.08.3.45-31.43.3.58-35.94.3.17-23.80.3.28-26.67.pth, myrk
BLEU = 5.11, 34.5/11.1/2.9/0.6 (BP=1.000, ratio=1.021, hyp_len=23640, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.08.3.45-31.43.3.58-35.94.3.17-23.80.3.28-26.67.pth, rkmy
BLEU = 2.71, 29.8/7.1/1.3/0.2 (BP=0.999, ratio=0.999, hyp_len=23478, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.09.3.13-22.93.3.38-29.24.2.88-17.76.3.14-23.14.pth, myrk
BLEU = 7.72, 40.7/15.0/4.5/1.3 (BP=1.000, ratio=1.010, hyp_len=23387, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.09.3.13-22.93.3.38-29.24.2.88-17.76.3.14-23.14.pth, rkmy
BLEU = 2.89, 31.1/8.7/1.7/0.1 (BP=0.999, ratio=0.999, hyp_len=23488, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.10.2.85-17.32.3.26-25.98.2.62-13.80.3.02-20.43.pth, myrk
BLEU = 11.63, 44.9/19.4/7.5/2.8 (BP=1.000, ratio=1.011, hyp_len=23410, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.10.2.85-17.32.3.26-25.98.2.62-13.80.3.02-20.43.pth, rkmy
BLEU = 3.87, 32.6/10.2/2.2/0.3 (BP=0.988, ratio=0.988, hyp_len=23226, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.11.2.58-13.18.3.09-22.09.2.38-10.77.2.87-17.66.pth, myrk
BLEU = 15.96, 49.6/24.1/11.0/5.0 (BP=0.998, ratio=0.998, hyp_len=23119, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.11.2.58-13.18.3.09-22.09.2.38-10.77.2.87-17.66.pth, rkmy
BLEU = 5.59, 34.2/11.8/3.1/0.8 (BP=1.000, ratio=1.008, hyp_len=23701, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.12.2.40-10.98.2.99-19.88.2.22-9.24.2.83-16.93.pth, myrk
BLEU = 19.73, 52.7/27.8/14.4/7.2 (BP=1.000, ratio=1.012, hyp_len=23436, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.12.2.40-10.98.2.99-19.88.2.22-9.24.2.83-16.93.pth, rkmy
BLEU = 6.67, 35.4/12.9/3.9/1.2 (BP=0.992, ratio=0.992, hyp_len=23313, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.13.2.26-9.55.2.84-17.18.2.07-7.92.2.63-13.86.pth, myrk
BLEU = 23.88, 56.3/32.2/18.3/10.0 (BP=0.995, ratio=0.995, hyp_len=23034, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.13.2.26-9.55.2.84-17.18.2.07-7.92.2.63-13.86.pth, rkmy
BLEU = 7.38, 37.2/14.5/4.4/1.3 (BP=1.000, ratio=1.038, hyp_len=24398, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.14.1.99-7.33.2.63-13.89.1.96-7.08.2.47-11.80.pth, myrk
BLEU = 26.98, 59.0/35.2/20.9/12.2 (BP=1.000, ratio=1.009, hyp_len=23380, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.14.1.99-7.33.2.63-13.89.1.96-7.08.2.47-11.80.pth, rkmy
BLEU = 10.15, 40.8/17.6/6.3/2.3 (BP=1.000, ratio=1.041, hyp_len=24476, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.15.1.90-6.70.2.49-12.04.1.83-6.23.2.33-10.23.pth, myrk
BLEU = 30.21, 61.6/38.4/24.0/14.7 (BP=1.000, ratio=1.000, hyp_len=23163, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.15.1.90-6.70.2.49-12.04.1.83-6.23.2.33-10.23.pth, rkmy
BLEU = 12.44, 43.8/20.0/8.3/3.3 (BP=1.000, ratio=1.025, hyp_len=24096, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.16.1.67-5.34.2.29-9.84.1.72-5.61.2.15-8.60.pth, myrk
BLEU = 33.57, 64.1/42.3/27.1/17.3 (BP=1.000, ratio=1.020, hyp_len=23621, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.16.1.67-5.34.2.29-9.84.1.72-5.61.2.15-8.60.pth, rkmy
BLEU = 16.87, 48.0/24.8/12.0/5.7 (BP=1.000, ratio=1.033, hyp_len=24287, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.17.1.64-5.16.2.11-8.24.1.68-5.35.1.96-7.09.pth, myrk
BLEU = 34.27, 64.6/42.6/27.7/18.1 (BP=1.000, ratio=1.010, hyp_len=23397, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.17.1.64-5.16.2.11-8.24.1.68-5.35.1.96-7.09.pth, rkmy
BLEU = 19.82, 52.0/28.1/14.5/7.3 (BP=1.000, ratio=1.022, hyp_len=24033, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.18.1.47-4.35.1.90-6.69.1.52-4.58.1.79-6.01.pth, myrk
BLEU = 41.12, 69.3/49.1/34.6/24.3 (BP=1.000, ratio=1.012, hyp_len=23447, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.18.1.47-4.35.1.90-6.69.1.52-4.58.1.79-6.01.pth, rkmy
BLEU = 25.24, 57.1/34.0/19.3/10.8 (BP=1.000, ratio=1.018, hyp_len=23937, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.19.1.46-4.29.1.74-5.70.1.54-4.68.1.66-5.26.pth, myrk
BLEU = 38.56, 68.3/47.0/31.9/21.6 (BP=1.000, ratio=1.002, hyp_len=23217, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.19.1.46-4.29.1.74-5.70.1.54-4.68.1.66-5.26.pth, rkmy
BLEU = 29.72, 60.2/38.2/23.4/14.5 (BP=1.000, ratio=1.025, hyp_len=24098, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.20.1.26-3.54.1.54-4.68.1.36-3.90.1.53-4.61.pth, myrk
BLEU = 47.68, 73.6/55.0/41.2/31.0 (BP=1.000, ratio=1.011, hyp_len=23414, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.20.1.26-3.54.1.54-4.68.1.36-3.90.1.53-4.61.pth, rkmy
BLEU = 34.33, 63.7/42.7/27.9/18.3 (BP=1.000, ratio=1.027, hyp_len=24152, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.21.1.27-3.58.1.64-5.16.1.31-3.70.1.46-4.31.pth, myrk
BLEU = 50.14, 75.1/57.1/43.7/33.7 (BP=1.000, ratio=1.013, hyp_len=23462, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.21.1.27-3.58.1.64-5.16.1.31-3.70.1.46-4.31.pth, rkmy
BLEU = 38.71, 67.2/47.0/32.2/22.1 (BP=1.000, ratio=1.015, hyp_len=23856, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.22.1.18-3.26.1.39-4.03.1.25-3.48.1.34-3.82.pth, myrk
BLEU = 52.90, 76.8/59.6/46.6/36.7 (BP=1.000, ratio=1.007, hyp_len=23320, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.22.1.18-3.26.1.39-4.03.1.25-3.48.1.34-3.82.pth, rkmy
BLEU = 43.03, 69.8/50.9/36.5/26.4 (BP=1.000, ratio=1.024, hyp_len=24077, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.23.1.16-3.18.1.34-3.84.1.22-3.37.1.42-4.15.pth, myrk
BLEU = 54.26, 77.6/60.8/48.1/38.2 (BP=1.000, ratio=1.004, hyp_len=23260, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.23.1.16-3.18.1.34-3.84.1.22-3.37.1.42-4.15.pth, rkmy
BLEU = 41.43, 68.7/49.5/34.9/24.8 (BP=1.000, ratio=1.041, hyp_len=24464, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.24.1.10-3.00.1.23-3.43.1.17-3.23.1.22-3.37.pth, myrk
BLEU = 57.01, 79.2/63.4/51.0/41.3 (BP=1.000, ratio=1.008, hyp_len=23351, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.24.1.10-3.00.1.23-3.43.1.17-3.23.1.22-3.37.pth, rkmy
BLEU = 49.51, 74.2/56.9/43.1/33.0 (BP=1.000, ratio=1.025, hyp_len=24091, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.25.1.07-2.91.1.13-3.09.1.13-3.11.1.15-3.16.pth, myrk
BLEU = 57.51, 79.5/63.7/51.6/41.9 (BP=1.000, ratio=1.010, hyp_len=23395, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.25.1.07-2.91.1.13-3.09.1.13-3.11.1.15-3.16.pth, rkmy
BLEU = 51.96, 75.5/59.1/45.7/35.7 (BP=1.000, ratio=1.016, hyp_len=23888, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.26.0.99-2.69.1.04-2.83.1.12-3.07.1.08-2.95.pth, myrk
BLEU = 58.59, 80.2/64.8/52.7/43.0 (BP=1.000, ratio=1.006, hyp_len=23290, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.26.0.99-2.69.1.04-2.83.1.12-3.07.1.08-2.95.pth, rkmy
BLEU = 55.63, 77.8/62.4/49.6/39.8 (BP=1.000, ratio=1.019, hyp_len=23964, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.27.1.01-2.75.0.95-2.58.1.11-3.02.1.02-2.79.pth, myrk
BLEU = 58.05, 79.6/64.3/52.2/42.5 (BP=1.000, ratio=1.021, hyp_len=23655, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.27.1.01-2.75.0.95-2.58.1.11-3.02.1.02-2.79.pth, rkmy
BLEU = 59.52, 80.0/65.8/53.8/44.3 (BP=1.000, ratio=1.014, hyp_len=23830, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.28.0.91-2.48.0.94-2.55.1.03-2.80.1.01-2.74.pth, myrk
BLEU = 61.95, 82.1/67.7/56.3/47.1 (BP=1.000, ratio=1.008, hyp_len=23339, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.28.0.91-2.48.0.94-2.55.1.03-2.80.1.01-2.74.pth, rkmy
BLEU = 59.45, 80.1/65.8/53.6/44.2 (BP=1.000, ratio=1.014, hyp_len=23845, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.29.0.82-2.27.0.89-2.43.1.00-2.71.0.99-2.69.pth, myrk
BLEU = 64.00, 83.1/69.5/58.6/49.6 (BP=1.000, ratio=1.011, hyp_len=23413, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.29.0.82-2.27.0.89-2.43.1.00-2.71.0.99-2.69.pth, rkmy
BLEU = 60.20, 80.4/66.4/54.4/45.2 (BP=1.000, ratio=1.011, hyp_len=23768, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.30.0.83-2.30.0.95-2.58.0.96-2.61.0.94-2.57.pth, myrk
BLEU = 64.85, 83.5/70.3/59.5/50.7 (BP=1.000, ratio=1.014, hyp_len=23485, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.30.0.83-2.30.0.95-2.58.0.96-2.61.0.94-2.57.pth, rkmy
BLEU = 59.92, 79.9/66.1/54.2/45.0 (BP=1.000, ratio=1.041, hyp_len=24483, ref_len=23509)

real	20m20.638s
user	19m50.351s
sys	1m3.628s
(base) ye@:~/exp/simple-nmt/model/dsl/myrk-30epoch$
```


#### Warmup-Epoch 20, Total Epoch 40


time python dual_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev \
--lang myrk \
--gpu_id 1 --batch_size 64 --n_epochs 40 --max_length 100 --dropout .2 \
--word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 \
--dsl_n_warmup_epochs 20 --dsl_lambda 1e-2 \
--lm_fn ./model/lm/lm-200epoch.pth \
--model_fn ./model/dsl/myrk-40epoch/dsl-model-myrk.pth | tee ./model/dsl/myrk-40epoch/training.log

```
Epoch 40 - |param|=9.34e+02 |g_param|=2.86e+04 loss_x2y=5.9847e-01 ppl_x2y=1.82 loss_y2x=5.6397e-01 ppl_y2x=1.76 dual_loss=7.1126e-01
Validation X2Y - loss=8.2739e-01 ppl=2.29 best_loss=8.5217e-01 best_ppl=2.34
Validation Y2X - loss=7.5925e-01 ppl=2.14 best_loss=7.7146e-01 best_ppl=2.16
```

testing/evaluation ...  

```
(base) ye@:~/exp/simple-nmt/model/dsl/myrk-40epoch$ time ./test-eval-loop-xy.sh 
Evaluation result for the model: dsl-model-myrk.01.4.44-84.46.4.48-88.20.4.05-57.38.4.08-58.87.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 17.8/0.6/0.0/0.0 (BP=0.953, ratio=0.954, hyp_len=22090, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.01.4.44-84.46.4.48-88.20.4.05-57.38.4.08-58.87.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 18.3/0.2/0.0/0.0 (BP=0.973, ratio=0.974, hyp_len=22892, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.02.4.12-61.38.4.15-63.36.3.88-48.45.3.91-50.06.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.2/2.0/0.0/0.0 (BP=0.983, ratio=0.983, hyp_len=22763, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.02.4.12-61.38.4.15-63.36.3.88-48.45.3.91-50.06.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.5/2.5/0.0/0.0 (BP=0.964, ratio=0.965, hyp_len=22676, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.03.4.00-54.68.4.02-55.89.3.81-45.28.3.82-45.80.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 18.7/1.7/0.0/0.0 (BP=1.000, ratio=1.007, hyp_len=23318, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.03.4.00-54.68.4.02-55.89.3.81-45.28.3.82-45.80.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.1/2.1/0.0/0.0 (BP=0.980, ratio=0.981, hyp_len=23054, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.04.3.98-53.58.4.01-54.99.3.72-41.17.3.75-42.35.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 21.3/1.8/0.0/0.0 (BP=1.000, ratio=1.019, hyp_len=23605, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.04.3.98-53.58.4.01-54.99.3.72-41.17.3.75-42.35.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 24.1/2.8/0.3/0.0 (BP=0.975, ratio=0.976, hyp_len=22936, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.05.3.81-45.11.3.87-47.92.3.57-35.61.3.66-38.71.pth, myrk
BLEU = 0.53, 24.4/3.2/0.1/0.0 (BP=1.000, ratio=1.011, hyp_len=23405, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.05.3.81-45.11.3.87-47.92.3.57-35.61.3.66-38.71.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.4/2.8/0.3/0.0 (BP=0.975, ratio=0.975, hyp_len=22931, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.06.3.72-41.11.3.84-46.47.3.44-31.09.3.59-36.15.pth, myrk
BLEU = 0.64, 25.1/4.5/0.3/0.0 (BP=1.000, ratio=1.009, hyp_len=23362, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.06.3.72-41.11.3.84-46.47.3.44-31.09.3.59-36.15.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.5/3.7/0.4/0.0 (BP=0.975, ratio=0.975, hyp_len=22933, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.07.3.54-34.33.3.74-41.91.3.29-26.79.3.50-33.05.pth, myrk
BLEU = 2.43, 30.1/7.1/1.2/0.1 (BP=0.981, ratio=0.981, hyp_len=22724, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.07.3.54-34.33.3.74-41.91.3.29-26.79.3.50-33.05.pth, rkmy
BLEU = 1.60, 24.0/5.0/0.7/0.1 (BP=1.000, ratio=1.000, hyp_len=23511, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.08.3.29-26.78.3.61-36.88.3.01-20.37.3.33-27.80.pth, myrk
BLEU = 4.76, 35.6/11.5/2.6/0.5 (BP=1.000, ratio=1.002, hyp_len=23205, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.08.3.29-26.78.3.61-36.88.3.01-20.37.3.33-27.80.pth, rkmy
BLEU = 2.30, 27.4/6.9/1.2/0.1 (BP=0.971, ratio=0.971, hyp_len=22837, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.09.2.99-19.95.3.43-30.93.2.79-16.32.3.25-25.67.pth, myrk
BLEU = 8.41, 40.2/15.5/5.2/1.6 (BP=1.000, ratio=1.009, hyp_len=23366, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.09.2.99-19.95.3.43-30.93.2.79-16.32.3.25-25.67.pth, rkmy
BLEU = 2.82, 27.6/7.9/1.7/0.2 (BP=0.977, ratio=0.977, hyp_len=22974, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.10.2.73-15.27.3.24-25.60.2.55-12.78.3.03-20.61.pth, myrk
BLEU = 11.96, 44.1/19.3/7.8/3.1 (BP=1.000, ratio=1.003, hyp_len=23232, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.10.2.73-15.27.3.24-25.60.2.55-12.78.3.03-20.61.pth, rkmy
BLEU = 3.83, 30.4/9.1/1.9/0.5 (BP=0.975, ratio=0.975, hyp_len=22925, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.11.2.52-12.48.3.08-21.79.2.46-11.67.2.90-18.20.pth, myrk
BLEU = 13.41, 46.1/21.3/9.1/3.6 (BP=1.000, ratio=1.009, hyp_len=23364, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.11.2.52-12.48.3.08-21.79.2.46-11.67.2.90-18.20.pth, rkmy
BLEU = 5.31, 33.0/11.0/2.9/0.8 (BP=0.994, ratio=0.994, hyp_len=23361, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.12.2.33-10.26.2.91-18.40.2.23-9.31.2.72-15.21.pth, myrk
BLEU = 18.60, 51.7/26.9/13.3/6.5 (BP=1.000, ratio=1.014, hyp_len=23490, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.12.2.33-10.26.2.91-18.40.2.23-9.31.2.72-15.21.pth, rkmy
BLEU = 7.26, 37.4/13.9/4.2/1.3 (BP=0.995, ratio=0.995, hyp_len=23384, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.13.2.24-9.43.2.77-15.91.2.10-8.17.2.55-12.79.pth, myrk
BLEU = 21.91, 54.8/30.5/16.3/8.5 (BP=1.000, ratio=1.007, hyp_len=23313, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.13.2.24-9.43.2.77-15.91.2.10-8.17.2.55-12.79.pth, rkmy
BLEU = 8.91, 39.6/16.0/5.4/1.8 (BP=1.000, ratio=1.017, hyp_len=23912, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.14.2.01-7.48.2.56-12.96.1.97-7.16.2.38-10.76.pth, myrk
BLEU = 25.61, 57.9/34.1/19.6/11.1 (BP=1.000, ratio=1.013, hyp_len=23460, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.14.2.01-7.48.2.56-12.96.1.97-7.16.2.38-10.76.pth, rkmy
BLEU = 11.01, 43.0/18.4/7.0/2.7 (BP=1.000, ratio=1.013, hyp_len=23812, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.15.1.90-6.68.2.28-9.81.1.85-6.37.2.14-8.50.pth, myrk
BLEU = 29.63, 61.0/37.6/23.4/14.3 (BP=1.000, ratio=1.002, hyp_len=23210, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.15.1.90-6.68.2.28-9.81.1.85-6.37.2.14-8.50.pth, rkmy
BLEU = 17.18, 49.0/25.0/12.0/5.9 (BP=1.000, ratio=1.014, hyp_len=23830, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.16.1.83-6.22.2.16-8.66.1.79-6.01.2.02-7.57.pth, myrk
BLEU = 31.00, 62.6/39.5/24.6/15.2 (BP=1.000, ratio=1.001, hyp_len=23184, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.16.1.83-6.22.2.16-8.66.1.79-6.01.2.02-7.57.pth, rkmy
BLEU = 20.25, 52.8/28.5/14.6/7.7 (BP=1.000, ratio=1.013, hyp_len=23817, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.17.1.57-4.83.1.85-6.35.1.64-5.15.1.82-6.19.pth, myrk
BLEU = 37.12, 66.6/45.2/30.6/20.6 (BP=1.000, ratio=1.008, hyp_len=23355, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.17.1.57-4.83.1.85-6.35.1.64-5.15.1.82-6.19.pth, rkmy
BLEU = 25.57, 57.6/34.2/19.5/11.1 (BP=1.000, ratio=1.029, hyp_len=24189, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.18.1.57-4.82.1.74-5.67.1.62-5.04.1.65-5.20.pth, myrk
BLEU = 38.19, 67.3/46.3/31.7/21.5 (BP=1.000, ratio=1.018, hyp_len=23570, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.18.1.57-4.82.1.74-5.67.1.62-5.04.1.65-5.20.pth, rkmy
BLEU = 31.31, 62.0/39.8/24.9/15.7 (BP=1.000, ratio=1.014, hyp_len=23839, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.19.1.47-4.35.1.59-4.92.1.66-5.24.1.62-5.07.pth, myrk
BLEU = 35.17, 65.4/44.0/28.9/18.4 (BP=1.000, ratio=1.039, hyp_len=24062, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.19.1.47-4.35.1.59-4.92.1.66-5.24.1.62-5.07.pth, rkmy
BLEU = 31.11, 62.1/39.7/24.7/15.4 (BP=1.000, ratio=1.022, hyp_len=24033, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.20.1.38-3.99.1.43-4.19.1.42-4.13.1.40-4.05.pth, myrk
BLEU = 43.81, 71.3/51.7/37.3/26.8 (BP=1.000, ratio=1.014, hyp_len=23486, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.20.1.38-3.99.1.43-4.19.1.42-4.13.1.40-4.05.pth, rkmy
BLEU = 42.10, 69.8/50.1/35.5/25.3 (BP=1.000, ratio=1.015, hyp_len=23857, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.21.1.29-3.63.1.46-4.29.1.37-3.94.1.35-3.85.pth, myrk
BLEU = 48.18, 73.7/55.6/41.7/31.5 (BP=1.000, ratio=1.021, hyp_len=23647, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.21.1.29-3.63.1.46-4.29.1.37-3.94.1.35-3.85.pth, rkmy
BLEU = 44.13, 71.0/52.1/37.5/27.3 (BP=1.000, ratio=1.017, hyp_len=23908, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.22.1.26-3.53.1.46-4.29.1.49-4.43.2.10-8.18.pth, myrk
BLEU = 44.24, 70.9/51.6/37.8/27.7 (BP=1.000, ratio=1.003, hyp_len=23222, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.22.1.26-3.53.1.46-4.29.1.49-4.43.2.10-8.18.pth, rkmy
BLEU = 20.92, 54.1/31.4/15.3/7.3 (BP=1.000, ratio=1.017, hyp_len=23906, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.23.1.21-3.36.1.32-3.75.1.25-3.48.1.19-3.30.pth, myrk
BLEU = 53.11, 76.9/60.0/46.9/36.7 (BP=1.000, ratio=1.012, hyp_len=23430, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.23.1.21-3.36.1.32-3.75.1.25-3.48.1.19-3.30.pth, rkmy
BLEU = 50.26, 74.5/57.6/43.9/33.8 (BP=1.000, ratio=1.024, hyp_len=24062, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.24.1.05-2.85.1.06-2.90.1.21-3.34.1.11-3.05.pth, myrk
BLEU = 56.24, 78.7/62.7/50.2/40.4 (BP=1.000, ratio=1.004, hyp_len=23263, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.24.1.05-2.85.1.06-2.90.1.21-3.34.1.11-3.05.pth, rkmy
BLEU = 55.42, 77.6/62.1/49.3/39.7 (BP=1.000, ratio=1.021, hyp_len=23996, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.25.1.10-3.02.1.00-2.73.1.44-4.23.1.06-2.87.pth, myrk
BLEU = 51.33, 76.8/59.1/45.4/35.1 (BP=0.990, ratio=0.990, hyp_len=22920, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.25.1.10-3.02.1.00-2.73.1.44-4.23.1.06-2.87.pth, rkmy
BLEU = 58.35, 79.3/64.8/52.4/43.0 (BP=1.000, ratio=1.017, hyp_len=23916, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.26.1.32-3.76.0.95-2.59.1.21-3.36.1.02-2.76.pth, myrk
BLEU = 53.09, 76.8/60.0/46.9/36.8 (BP=1.000, ratio=1.015, hyp_len=23507, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.26.1.32-3.76.0.95-2.59.1.21-3.36.1.02-2.76.pth, rkmy
BLEU = 60.38, 80.4/66.4/54.7/45.5 (BP=1.000, ratio=1.018, hyp_len=23929, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.27.0.94-2.56.0.84-2.33.1.10-3.00.0.98-2.66.pth, myrk
BLEU = 59.23, 80.4/65.4/53.4/43.8 (BP=1.000, ratio=1.010, hyp_len=23395, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.27.0.94-2.56.0.84-2.33.1.10-3.00.0.98-2.66.pth, rkmy
BLEU = 61.40, 80.9/67.4/55.7/46.7 (BP=1.000, ratio=1.026, hyp_len=24114, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.28.0.92-2.52.0.85-2.34.1.07-2.92.0.96-2.60.pth, myrk
BLEU = 59.64, 80.6/65.9/53.9/44.2 (BP=1.000, ratio=1.018, hyp_len=23577, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.28.0.92-2.52.0.85-2.34.1.07-2.92.0.96-2.60.pth, rkmy
BLEU = 62.70, 81.8/68.6/57.1/48.2 (BP=1.000, ratio=1.020, hyp_len=23977, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.29.0.85-2.34.0.80-2.22.1.05-2.85.0.93-2.54.pth, myrk
BLEU = 62.97, 82.5/68.7/57.5/48.3 (BP=1.000, ratio=1.011, hyp_len=23412, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.29.0.85-2.34.0.80-2.22.1.05-2.85.0.93-2.54.pth, rkmy
BLEU = 64.45, 82.9/70.2/59.0/50.3 (BP=1.000, ratio=1.021, hyp_len=24001, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.30.0.83-2.29.0.75-2.12.1.05-2.84.0.89-2.43.pth, myrk
BLEU = 61.31, 81.3/67.3/55.7/46.3 (BP=1.000, ratio=1.024, hyp_len=23720, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.30.0.83-2.29.0.75-2.12.1.05-2.84.0.89-2.43.pth, rkmy
BLEU = 65.18, 83.0/70.8/59.9/51.3 (BP=1.000, ratio=1.029, hyp_len=24181, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.31.0.83-2.29.0.75-2.11.0.98-2.66.0.87-2.38.pth, myrk
BLEU = 64.16, 83.1/69.8/58.8/49.7 (BP=1.000, ratio=1.015, hyp_len=23496, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.31.0.83-2.29.0.75-2.11.0.98-2.66.0.87-2.38.pth, rkmy
BLEU = 67.21, 84.0/72.4/62.1/54.0 (BP=1.000, ratio=1.022, hyp_len=24033, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.32.0.74-2.10.0.70-2.01.0.97-2.64.0.90-2.45.pth, myrk
BLEU = 64.37, 83.1/69.9/59.0/50.0 (BP=1.000, ratio=1.017, hyp_len=23543, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.32.0.74-2.10.0.70-2.01.0.97-2.64.0.90-2.45.pth, rkmy
BLEU = 66.14, 83.6/71.8/60.9/52.3 (BP=1.000, ratio=1.032, hyp_len=24263, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.33.0.75-2.11.0.70-2.01.0.96-2.60.0.87-2.39.pth, myrk
BLEU = 66.55, 84.2/71.7/61.5/52.9 (BP=1.000, ratio=1.009, hyp_len=23366, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.33.0.75-2.11.0.70-2.01.0.96-2.60.0.87-2.39.pth, rkmy
BLEU = 67.54, 84.4/72.7/62.4/54.3 (BP=1.000, ratio=1.016, hyp_len=23878, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.34.0.69-1.99.0.63-1.87.0.95-2.59.0.93-2.53.pth, myrk
BLEU = 66.21, 84.1/71.4/61.0/52.5 (BP=1.000, ratio=1.008, hyp_len=23344, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.34.0.69-1.99.0.63-1.87.0.95-2.59.0.93-2.53.pth, rkmy
BLEU = 63.54, 81.9/69.4/58.1/49.3 (BP=1.000, ratio=1.038, hyp_len=24402, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.35.0.79-2.19.0.65-1.91.1.00-2.73.0.81-2.24.pth, myrk
BLEU = 65.76, 83.9/70.9/60.5/52.0 (BP=1.000, ratio=1.002, hyp_len=23196, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.35.0.79-2.19.0.65-1.91.1.00-2.73.0.81-2.24.pth, rkmy
BLEU = 68.75, 84.7/73.7/63.8/56.0 (BP=1.000, ratio=1.031, hyp_len=24239, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.36.0.71-2.03.0.58-1.79.0.92-2.50.0.79-2.21.pth, myrk
BLEU = 66.49, 83.9/71.7/61.5/52.9 (BP=1.000, ratio=1.024, hyp_len=23713, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.36.0.71-2.03.0.58-1.79.0.92-2.50.0.79-2.21.pth, rkmy
BLEU = 69.82, 85.4/74.7/65.0/57.4 (BP=1.000, ratio=1.025, hyp_len=24102, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.37.0.68-1.96.0.53-1.70.0.88-2.42.0.77-2.16.pth, myrk
BLEU = 67.86, 84.8/72.8/62.9/54.6 (BP=1.000, ratio=1.013, hyp_len=23467, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.37.0.68-1.96.0.53-1.70.0.88-2.42.0.77-2.16.pth, rkmy
BLEU = 70.95, 85.9/75.6/66.3/58.9 (BP=1.000, ratio=1.025, hyp_len=24097, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.38.0.64-1.89.0.54-1.72.0.87-2.39.0.77-2.16.pth, myrk
BLEU = 68.16, 84.9/73.1/63.3/54.9 (BP=1.000, ratio=1.013, hyp_len=23466, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.38.0.64-1.89.0.54-1.72.0.87-2.39.0.77-2.16.pth, rkmy
BLEU = 69.97, 85.5/74.8/65.1/57.5 (BP=1.000, ratio=1.034, hyp_len=24301, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.39.0.70-2.01.0.55-1.73.0.85-2.34.0.78-2.17.pth, myrk
BLEU = 68.16, 84.8/73.1/63.3/55.1 (BP=1.000, ratio=1.021, hyp_len=23638, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.39.0.70-2.01.0.55-1.73.0.85-2.34.0.78-2.17.pth, rkmy
BLEU = 71.25, 86.0/75.9/66.6/59.3 (BP=1.000, ratio=1.024, hyp_len=24077, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.40.0.60-1.82.0.56-1.76.0.83-2.29.0.76-2.14.pth, myrk
BLEU = 69.86, 85.6/74.5/65.2/57.3 (BP=1.000, ratio=1.018, hyp_len=23575, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.40.0.60-1.82.0.56-1.76.0.83-2.29.0.76-2.14.pth, rkmy
BLEU = 71.07, 86.0/75.7/66.4/59.1 (BP=1.000, ratio=1.028, hyp_len=24171, ref_len=23509)

real	26m42.743s
user	26m9.109s
sys	1m24.701s
(base) ye@:~/exp/simple-nmt/model/dsl/myrk-40epoch$
```

## Write a Shell Script for DSL Training Loop

```bash
#!/bin/bash

# Written by Ye, LST, NECTEC, Thailand
# Last Updated: 21 Mar 2022
# for training Dual Supervised Learning models

for i in {50,60,70,80,90,100}
do
   echo "training start for ${i} epochs...";
   time python dual_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev \
   --lang myrk \
   --gpu_id 0 --batch_size 64 --n_epochs ${i} --max_length 100 --dropout .2 \
   --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 \
   --dsl_n_warmup_epochs 20 --dsl_lambda 1e-2 \
   --lm_fn ./model/lm/lm-200epoch.pth \
   --model_fn ./model/dsl/myrk-${i}epoch/dsl-model-myrk.pth | tee ./model/dsl/myrk-${i}epoch/training.log;
   
done
```


#### Warmup-Epoch 20, Total Epoch 50

```
Epoch 1 - |param|=9.08e+02 |g_param|=3.32e+05 loss_x2y=4.4372e+00 ppl_x2y=84.54 loss_y2x=4.5068e+00 ppl_y2x=90.63 dual_loss=0.0000e+00
Validation X2Y - loss=4.0436e+00 ppl=57.03 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=4.1308e+00 ppl=62.23 best_loss=inf best_ppl=inf
Epoch 2 - |param|=9.08e+02 |g_param|=2.79e+05 loss_x2y=4.1676e+00 ppl_x2y=64.56 loss_y2x=4.2146e+00 ppl_y2x=67.67 dual_loss=0.0000e+00
Validation X2Y - loss=3.8723e+00 ppl=48.05 best_loss=4.0436e+00 best_ppl=57.03                                          
Validation Y2X - loss=3.9127e+00 ppl=50.03 best_loss=4.1308e+00 best_ppl=62.23
Epoch 3 - |param|=9.08e+02 |g_param|=2.80e+05 loss_x2y=4.0689e+00 ppl_x2y=58.49 loss_y2x=4.1220e+00 ppl_y2x=61.69 dual_loss=0.0000e+00
Validation X2Y - loss=3.7736e+00 ppl=43.54 best_loss=3.8723e+00 best_ppl=48.05                                          
Validation Y2X - loss=3.8121e+00 ppl=45.25 best_loss=3.9127e+00 best_ppl=50.03
Epoch 4 - |param|=9.09e+02 |g_param|=2.65e+05 loss_x2y=3.9256e+00 ppl_x2y=50.69 loss_y2x=3.9727e+00 ppl_y2x=53.13 dual_loss=0.0000e+00
Validation X2Y - loss=3.6944e+00 ppl=40.22 best_loss=3.7736e+00 best_ppl=43.54                                          
Validation Y2X - loss=3.7202e+00 ppl=41.27 best_loss=3.8121e+00 best_ppl=45.25
Epoch 5 - |param|=9.09e+02 |g_param|=2.52e+05 loss_x2y=3.7756e+00 ppl_x2y=43.62 loss_y2x=3.8270e+00 ppl_y2x=45.92 dual_loss=0.0000e+00
Validation X2Y - loss=3.5817e+00 ppl=35.94 best_loss=3.6944e+00 best_ppl=40.22                                          
Validation Y2X - loss=3.6328e+00 ppl=37.82 best_loss=3.7202e+00 best_ppl=41.27
Epoch 6 - |param|=9.10e+02 |g_param|=2.64e+05 loss_x2y=3.7960e+00 ppl_x2y=44.52 loss_y2x=3.8332e+00 ppl_y2x=46.21 dual_loss=0.0000e+00
Validation X2Y - loss=3.5006e+00 ppl=33.14 best_loss=3.5817e+00 best_ppl=35.94                                          
Validation Y2X - loss=3.5333e+00 ppl=34.24 best_loss=3.6328e+00 best_ppl=37.82
Epoch 7 - |param|=9.10e+02 |g_param|=2.56e+05 loss_x2y=3.5575e+00 ppl_x2y=35.08 loss_y2x=3.6353e+00 ppl_y2x=37.91 dual_loss=0.0000e+00
Validation X2Y - loss=3.3247e+00 ppl=27.79 best_loss=3.5006e+00 best_ppl=33.14                                          
Validation Y2X - loss=3.3793e+00 ppl=29.35 best_loss=3.5333e+00 best_ppl=34.24
Epoch 8 - |param|=9.11e+02 |g_param|=2.54e+05 loss_x2y=3.4295e+00 ppl_x2y=30.86 loss_y2x=3.4975e+00 ppl_y2x=33.03 dual_loss=0.0000e+00
Validation X2Y - loss=3.1868e+00 ppl=24.21 best_loss=3.3247e+00 best_ppl=27.79                                          
Validation Y2X - loss=3.2272e+00 ppl=25.21 best_loss=3.3793e+00 best_ppl=29.35
Epoch 9 - |param|=9.12e+02 |g_param|=2.55e+05 loss_x2y=3.2047e+00 ppl_x2y=24.65 loss_y2x=3.2713e+00 ppl_y2x=26.35 dual_loss=0.0000e+00
Validation X2Y - loss=3.0222e+00 ppl=20.54 best_loss=3.1868e+00 best_ppl=24.21                                          
Validation Y2X - loss=3.0662e+00 ppl=21.46 best_loss=3.2272e+00 best_ppl=25.21
Epoch 10 - |param|=9.13e+02 |g_param|=3.19e+05 loss_x2y=3.0845e+00 ppl_x2y=21.86 loss_y2x=3.1335e+00 ppl_y2x=22.95 dual_loss=0.0000e+00
Validation X2Y - loss=2.9133e+00 ppl=18.42 best_loss=3.0222e+00 best_ppl=20.54                                          
Validation Y2X - loss=2.9359e+00 ppl=18.84 best_loss=3.0662e+00 best_ppl=21.46
Epoch 11 - |param|=9.14e+02 |g_param|=2.50e+05 loss_x2y=2.9077e+00 ppl_x2y=18.32 loss_y2x=2.9362e+00 ppl_y2x=18.84 dual_loss=0.0000e+00
Validation X2Y - loss=2.7713e+00 ppl=15.98 best_loss=2.9133e+00 best_ppl=18.42                                          
Validation Y2X - loss=2.7848e+00 ppl=16.20 best_loss=2.9359e+00 best_ppl=18.84
Epoch 12 - |param|=9.15e+02 |g_param|=3.46e+05 loss_x2y=2.7621e+00 ppl_x2y=15.83 loss_y2x=2.8317e+00 ppl_y2x=16.97 dual_loss=0.0000e+00
Validation X2Y - loss=2.5745e+00 ppl=13.12 best_loss=2.7713e+00 best_ppl=15.98                                          
Validation Y2X - loss=2.6207e+00 ppl=13.75 best_loss=2.7848e+00 best_ppl=16.20
Epoch 13 - |param|=9.16e+02 |g_param|=2.47e+05 loss_x2y=2.5141e+00 ppl_x2y=12.36 loss_y2x=2.5927e+00 ppl_y2x=13.37 dual_loss=0.0000e+00
Validation X2Y - loss=2.3808e+00 ppl=10.81 best_loss=2.5745e+00 best_ppl=13.12                                          
Validation Y2X - loss=2.4189e+00 ppl=11.23 best_loss=2.6207e+00 best_ppl=13.75
Epoch 14 - |param|=9.17e+02 |g_param|=2.04e+05 loss_x2y=2.2968e+00 ppl_x2y=9.94 loss_y2x=2.3663e+00 ppl_y2x=10.66 dual_loss=0.0000e+00
Validation X2Y - loss=2.2096e+00 ppl=9.11 best_loss=2.3808e+00 best_ppl=10.81                                           
Validation Y2X - loss=2.2181e+00 ppl=9.19 best_loss=2.4189e+00 best_ppl=11.23
Epoch 15 - |param|=9.18e+02 |g_param|=2.03e+05 loss_x2y=2.1631e+00 ppl_x2y=8.70 loss_y2x=2.2161e+00 ppl_y2x=9.17 dual_loss=0.0000e+00
Validation X2Y - loss=2.0511e+00 ppl=7.78 best_loss=2.2096e+00 best_ppl=9.11                                            
Validation Y2X - loss=2.0791e+00 ppl=8.00 best_loss=2.2181e+00 best_ppl=9.19
Epoch 16 - |param|=9.19e+02 |g_param|=2.22e+05 loss_x2y=2.0126e+00 ppl_x2y=7.48 loss_y2x=2.0196e+00 ppl_y2x=7.54 dual_loss=0.0000e+00
Validation X2Y - loss=1.9486e+00 ppl=7.02 best_loss=2.0511e+00 best_ppl=7.78                                            
Validation Y2X - loss=1.9388e+00 ppl=6.95 best_loss=2.0791e+00 best_ppl=8.00
Epoch 17 - |param|=9.20e+02 |g_param|=2.10e+05 loss_x2y=1.8580e+00 ppl_x2y=6.41 loss_y2x=1.8400e+00 ppl_y2x=6.30 dual_loss=0.0000e+00
Validation X2Y - loss=1.8205e+00 ppl=6.17 best_loss=1.9486e+00 best_ppl=7.02                                            
Validation Y2X - loss=1.7520e+00 ppl=5.77 best_loss=1.9388e+00 best_ppl=6.95
Epoch 18 - |param|=9.21e+02 |g_param|=1.56e+05 loss_x2y=1.6528e+00 ppl_x2y=5.22 loss_y2x=1.6063e+00 ppl_y2x=4.98 dual_loss=0.0000e+00
Validation X2Y - loss=1.6942e+00 ppl=5.44 best_loss=1.8205e+00 best_ppl=6.17                                            
Validation Y2X - loss=1.6175e+00 ppl=5.04 best_loss=1.7520e+00 best_ppl=5.77
Epoch 19 - |param|=9.22e+02 |g_param|=1.54e+05 loss_x2y=1.6032e+00 ppl_x2y=4.97 loss_y2x=1.5698e+00 ppl_y2x=4.81 dual_loss=0.0000e+00
Validation X2Y - loss=1.5728e+00 ppl=4.82 best_loss=1.6942e+00 best_ppl=5.44                                            
Validation Y2X - loss=1.5469e+00 ppl=4.70 best_loss=1.6175e+00 best_ppl=5.04
Epoch 20 - |param|=9.23e+02 |g_param|=1.99e+05 loss_x2y=1.5017e+00 ppl_x2y=4.49 loss_y2x=1.4864e+00 ppl_y2x=4.42 dual_loss=0.0000e+00
Validation X2Y - loss=1.5236e+00 ppl=4.59 best_loss=1.5728e+00 best_ppl=4.82                                            
Validation Y2X - loss=1.4655e+00 ppl=4.33 best_loss=1.5469e+00 best_ppl=4.70
Epoch 21 - |param|=9.23e+02 |g_param|=1.20e+05 loss_x2y=1.3715e+00 ppl_x2y=3.94 loss_y2x=1.4705e+00 ppl_y2x=4.35 dual_loss=1.3560e+00
Validation X2Y - loss=1.3711e+00 ppl=3.94 best_loss=1.5236e+00 best_ppl=4.59                                            
Validation Y2X - loss=1.3655e+00 ppl=3.92 best_loss=1.4655e+00 best_ppl=4.33
Epoch 22 - |param|=9.24e+02 |g_param|=1.16e+05 loss_x2y=1.2972e+00 ppl_x2y=3.66 loss_y2x=1.3859e+00 ppl_y2x=4.00 dual_loss=1.1751e+00
Validation X2Y - loss=1.3700e+00 ppl=3.94 best_loss=1.3711e+00 best_ppl=3.94                                            
Validation Y2X - loss=1.3505e+00 ppl=3.86 best_loss=1.3655e+00 best_ppl=3.92
Epoch 23 - |param|=9.25e+02 |g_param|=9.61e+04 loss_x2y=1.1442e+00 ppl_x2y=3.14 loss_y2x=1.2150e+00 ppl_y2x=3.37 dual_loss=8.0263e-01
Validation X2Y - loss=1.2603e+00 ppl=3.53 best_loss=1.3700e+00 best_ppl=3.94                                            
Validation Y2X - loss=1.2482e+00 ppl=3.48 best_loss=1.3505e+00 best_ppl=3.86
Epoch 24 - |param|=9.26e+02 |g_param|=1.23e+05 loss_x2y=1.1070e+00 ppl_x2y=3.03 loss_y2x=1.1075e+00 ppl_y2x=3.03 dual_loss=6.9380e-01
Validation X2Y - loss=1.2445e+00 ppl=3.47 best_loss=1.2603e+00 best_ppl=3.53                                            
Validation Y2X - loss=1.1617e+00 ppl=3.20 best_loss=1.2482e+00 best_ppl=3.48
Epoch 25 - |param|=9.26e+02 |g_param|=4.88e+04 loss_x2y=1.1818e+00 ppl_x2y=3.26 loss_y2x=1.0135e+00 ppl_y2x=2.76 dual_loss=1.4836e+00
Validation X2Y - loss=1.1895e+00 ppl=3.29 best_loss=1.2445e+00 best_ppl=3.47                                            
Validation Y2X - loss=1.0802e+00 ppl=2.95 best_loss=1.1617e+00 best_ppl=3.20
Epoch 26 - |param|=9.27e+02 |g_param|=4.19e+04 loss_x2y=9.9390e-01 ppl_x2y=2.70 loss_y2x=9.5562e-01 ppl_y2x=2.60 dual_loss=5.5752e-01
Validation X2Y - loss=1.0888e+00 ppl=2.97 best_loss=1.1895e+00 best_ppl=3.29                                            
Validation Y2X - loss=1.0491e+00 ppl=2.86 best_loss=1.0802e+00 best_ppl=2.95
Epoch 27 - |param|=9.28e+02 |g_param|=4.45e+04 loss_x2y=9.2595e-01 ppl_x2y=2.52 loss_y2x=9.0419e-01 ppl_y2x=2.47 dual_loss=5.1908e-01
Validation X2Y - loss=1.0757e+00 ppl=2.93 best_loss=1.0888e+00 best_ppl=2.97                                            
Validation Y2X - loss=1.0248e+00 ppl=2.79 best_loss=1.0491e+00 best_ppl=2.86
Epoch 28 - |param|=9.28e+02 |g_param|=4.51e+04 loss_x2y=1.1151e+00 ppl_x2y=3.05 loss_y2x=8.9779e-01 ppl_y2x=2.45 dual_loss=1.6685e+00
Validation X2Y - loss=1.1650e+00 ppl=3.21 best_loss=1.0757e+00 best_ppl=2.93                                            
Validation Y2X - loss=9.7193e-01 ppl=2.64 best_loss=1.0248e+00 best_ppl=2.79
Epoch 29 - |param|=9.29e+02 |g_param|=3.79e+04 loss_x2y=1.0052e+00 ppl_x2y=2.73 loss_y2x=8.3529e-01 ppl_y2x=2.31 dual_loss=8.1863e-01
Validation X2Y - loss=1.0497e+00 ppl=2.86 best_loss=1.0757e+00 best_ppl=2.93                                            
Validation Y2X - loss=9.5796e-01 ppl=2.61 best_loss=9.7193e-01 best_ppl=2.64
Epoch 30 - |param|=9.30e+02 |g_param|=4.37e+04 loss_x2y=9.7328e-01 ppl_x2y=2.65 loss_y2x=8.1620e-01 ppl_y2x=2.26 dual_loss=7.5147e-01
Validation X2Y - loss=1.0080e+00 ppl=2.74 best_loss=1.0497e+00 best_ppl=2.86                                            
Validation Y2X - loss=9.2893e-01 ppl=2.53 best_loss=9.5796e-01 best_ppl=2.61
Epoch 31 - |param|=9.30e+02 |g_param|=1.43e+05 loss_x2y=8.9094e-01 ppl_x2y=2.44 loss_y2x=1.2007e+00 ppl_y2x=3.32 dual_loss=3.1026e+00
Validation X2Y - loss=9.4579e-01 ppl=2.57 best_loss=1.0080e+00 best_ppl=2.74                                            
Validation Y2X - loss=1.0764e+00 ppl=2.93 best_loss=9.2893e-01 best_ppl=2.53
Epoch 32 - |param|=9.31e+02 |g_param|=4.89e+04 loss_x2y=7.9008e-01 ppl_x2y=2.20 loss_y2x=8.9027e-01 ppl_y2x=2.44 dual_loss=1.8267e+00
Validation X2Y - loss=9.5575e-01 ppl=2.60 best_loss=9.4579e-01 best_ppl=2.57                                            
Validation Y2X - loss=9.3641e-01 ppl=2.55 best_loss=9.2893e-01 best_ppl=2.53
Epoch 33 - |param|=9.31e+02 |g_param|=1.86e+04 loss_x2y=7.3546e-01 ppl_x2y=2.09 loss_y2x=7.3424e-01 ppl_y2x=2.08 dual_loss=5.2583e-01
Validation X2Y - loss=9.1066e-01 ppl=2.49 best_loss=9.4579e-01 best_ppl=2.57                                            
Validation Y2X - loss=8.7584e-01 ppl=2.40 best_loss=9.2893e-01 best_ppl=2.53
Epoch 34 - |param|=9.32e+02 |g_param|=1.89e+04 loss_x2y=6.7633e-01 ppl_x2y=1.97 loss_y2x=6.6953e-01 ppl_y2x=1.95 dual_loss=4.4536e-01
Validation X2Y - loss=8.8565e-01 ppl=2.42 best_loss=9.1066e-01 best_ppl=2.49                                            
Validation Y2X - loss=8.4744e-01 ppl=2.33 best_loss=8.7584e-01 best_ppl=2.40
Epoch 35 - |param|=9.32e+02 |g_param|=2.29e+04 loss_x2y=6.5347e-01 ppl_x2y=1.92 loss_y2x=6.7597e-01 ppl_y2x=1.97 dual_loss=5.6441e-01
Validation X2Y - loss=8.6877e-01 ppl=2.38 best_loss=8.8565e-01 best_ppl=2.42                                            
Validation Y2X - loss=8.4565e-01 ppl=2.33 best_loss=8.4744e-01 best_ppl=2.33
Epoch 36 - |param|=9.33e+02 |g_param|=2.69e+04 loss_x2y=6.4209e-01 ppl_x2y=1.90 loss_y2x=6.9109e-01 ppl_y2x=2.00 dual_loss=7.0072e-01
Validation X2Y - loss=8.7474e-01 ppl=2.40 best_loss=8.6877e-01 best_ppl=2.38                                            
Validation Y2X - loss=8.4111e-01 ppl=2.32 best_loss=8.4565e-01 best_ppl=2.33
Epoch 37 - |param|=9.33e+02 |g_param|=4.57e+04 loss_x2y=6.3508e-01 ppl_x2y=1.89 loss_y2x=7.8518e-01 ppl_y2x=2.19 dual_loss=1.4698e+00
Validation X2Y - loss=8.4787e-01 ppl=2.33 best_loss=8.6877e-01 best_ppl=2.38                                            
Validation Y2X - loss=9.9597e-01 ppl=2.71 best_loss=8.4111e-01 best_ppl=2.32
Epoch 38 - |param|=9.34e+02 |g_param|=2.95e+04 loss_x2y=6.1467e-01 ppl_x2y=1.85 loss_y2x=7.5402e-01 ppl_y2x=2.13 dual_loss=1.1520e+00
Validation X2Y - loss=8.3598e-01 ppl=2.31 best_loss=8.4787e-01 best_ppl=2.33                                            
Validation Y2X - loss=8.5424e-01 ppl=2.35 best_loss=8.4111e-01 best_ppl=2.32
Epoch 39 - |param|=9.34e+02 |g_param|=1.69e+04 loss_x2y=5.8283e-01 ppl_x2y=1.79 loss_y2x=6.1062e-01 ppl_y2x=1.84 dual_loss=4.7533e-01
Validation X2Y - loss=8.3705e-01 ppl=2.31 best_loss=8.3598e-01 best_ppl=2.31                                            
Validation Y2X - loss=7.9745e-01 ppl=2.22 best_loss=8.4111e-01 best_ppl=2.32
Epoch 40 - |param|=9.35e+02 |g_param|=4.24e+04 loss_x2y=9.8403e-01 ppl_x2y=2.68 loss_y2x=6.7680e-01 ppl_y2x=1.97 dual_loss=2.4044e+00
Validation X2Y - loss=1.0197e+00 ppl=2.77 best_loss=8.3598e-01 best_ppl=2.31                                            
Validation Y2X - loss=7.8136e-01 ppl=2.18 best_loss=7.9745e-01 best_ppl=2.22
Epoch 41 - |param|=9.36e+02 |g_param|=2.25e+04 loss_x2y=7.4843e-01 ppl_x2y=2.11 loss_y2x=5.6779e-01 ppl_y2x=1.76 dual_loss=7.7317e-01
Validation X2Y - loss=8.5207e-01 ppl=2.34 best_loss=8.3598e-01 best_ppl=2.31                                            
Validation Y2X - loss=7.6429e-01 ppl=2.15 best_loss=7.8136e-01 best_ppl=2.18
Epoch 42 - |param|=9.36e+02 |g_param|=1.64e+04 loss_x2y=5.7009e-01 ppl_x2y=1.77 loss_y2x=5.3538e-01 ppl_y2x=1.71 dual_loss=3.9388e-01
Validation X2Y - loss=8.0266e-01 ppl=2.23 best_loss=8.3598e-01 best_ppl=2.31                                            
Validation Y2X - loss=7.7098e-01 ppl=2.16 best_loss=7.6429e-01 best_ppl=2.15
Epoch 43 - |param|=9.36e+02 |g_param|=1.82e+04 loss_x2y=5.4811e-01 ppl_x2y=1.73 loss_y2x=5.4334e-01 ppl_y2x=1.72 dual_loss=4.2975e-01
Validation X2Y - loss=7.9238e-01 ppl=2.21 best_loss=8.0266e-01 best_ppl=2.23                                            
Validation Y2X - loss=7.6649e-01 ppl=2.15 best_loss=7.6429e-01 best_ppl=2.15
Epoch 44 - |param|=9.37e+02 |g_param|=1.82e+04 loss_x2y=5.1120e-01 ppl_x2y=1.67 loss_y2x=5.1712e-01 ppl_y2x=1.68 dual_loss=4.1097e-01
Validation X2Y - loss=7.8592e-01 ppl=2.19 best_loss=7.9238e-01 best_ppl=2.21                                            
Validation Y2X - loss=7.8746e-01 ppl=2.20 best_loss=7.6429e-01 best_ppl=2.15
Epoch 45 - |param|=9.37e+02 |g_param|=1.90e+04 loss_x2y=5.1303e-01 ppl_x2y=1.67 loss_y2x=5.4321e-01 ppl_y2x=1.72 dual_loss=4.9414e-01
Validation X2Y - loss=7.6014e-01 ppl=2.14 best_loss=7.8592e-01 best_ppl=2.19                                            
Validation Y2X - loss=7.7793e-01 ppl=2.18 best_loss=7.6429e-01 best_ppl=2.15
Epoch 46 - |param|=9.38e+02 |g_param|=1.74e+04 loss_x2y=4.8473e-01 ppl_x2y=1.62 loss_y2x=4.9615e-01 ppl_y2x=1.64 dual_loss=3.8161e-01
Validation X2Y - loss=7.6593e-01 ppl=2.15 best_loss=7.6014e-01 best_ppl=2.14                                            
Validation Y2X - loss=7.3646e-01 ppl=2.09 best_loss=7.6429e-01 best_ppl=2.15
Epoch 47 - |param|=9.38e+02 |g_param|=1.90e+04 loss_x2y=4.6359e-01 ppl_x2y=1.59 loss_y2x=4.7798e-01 ppl_y2x=1.61 dual_loss=4.2812e-01
Validation X2Y - loss=7.5741e-01 ppl=2.13 best_loss=7.6014e-01 best_ppl=2.14                                            
Validation Y2X - loss=7.4236e-01 ppl=2.10 best_loss=7.3646e-01 best_ppl=2.09
Epoch 48 - |param|=9.38e+02 |g_param|=2.78e+04 loss_x2y=4.7827e-01 ppl_x2y=1.61 loss_y2x=5.1095e-01 ppl_y2x=1.67 dual_loss=6.3378e-01
Validation X2Y - loss=7.5791e-01 ppl=2.13 best_loss=7.5741e-01 best_ppl=2.13                                            
Validation Y2X - loss=7.4726e-01 ppl=2.11 best_loss=7.3646e-01 best_ppl=2.09
Epoch 49 - |param|=9.39e+02 |g_param|=2.58e+04 loss_x2y=4.4524e-01 ppl_x2y=1.56 loss_y2x=5.0281e-01 ppl_y2x=1.65 dual_loss=6.4381e-01
Validation X2Y - loss=7.4161e-01 ppl=2.10 best_loss=7.5741e-01 best_ppl=2.13                                            
Validation Y2X - loss=7.5513e-01 ppl=2.13 best_loss=7.3646e-01 best_ppl=2.09
Epoch 50 - |param|=9.39e+02 |g_param|=3.24e+04 loss_x2y=4.6227e-01 ppl_x2y=1.59 loss_y2x=6.0432e-01 ppl_y2x=1.83 dual_loss=1.2689e+00
Validation X2Y - loss=7.5507e-01 ppl=2.13 best_loss=7.4161e-01 best_ppl=2.10                                            
Validation Y2X - loss=7.8774e-01 ppl=2.20 best_loss=7.3646e-01 best_ppl=2.09

real	21m18.578s
user	21m2.147s
sys	0m15.050s
```


#### Warmup-Epoch 20, Total Epoch 60

```
Epoch 1 - |param|=9.07e+02 |g_param|=2.82e+05 loss_x2y=4.4032e+00 ppl_x2y=81.71 loss_y2x=4.5186e+00 ppl_y2x=91.71 dual_loss=0.0000e+00
Validation X2Y - loss=4.0259e+00 ppl=56.03 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=4.1350e+00 ppl=62.49 best_loss=inf best_ppl=inf
Epoch 2 - |param|=9.07e+02 |g_param|=2.36e+05 loss_x2y=4.0945e+00 ppl_x2y=60.01 loss_y2x=4.1754e+00 ppl_y2x=65.07 dual_loss=0.0000e+00
Validation X2Y - loss=3.8697e+00 ppl=47.93 best_loss=4.0259e+00 best_ppl=56.03                                          
Validation Y2X - loss=3.9348e+00 ppl=51.15 best_loss=4.1350e+00 best_ppl=62.49
Epoch 3 - |param|=9.08e+02 |g_param|=2.67e+05 loss_x2y=4.0066e+00 ppl_x2y=54.96 loss_y2x=4.0753e+00 ppl_y2x=58.87 dual_loss=0.0000e+00
Validation X2Y - loss=3.7889e+00 ppl=44.21 best_loss=3.8697e+00 best_ppl=47.93                                          
Validation Y2X - loss=3.8424e+00 ppl=46.64 best_loss=3.9348e+00 best_ppl=51.15
Epoch 4 - |param|=9.08e+02 |g_param|=2.53e+05 loss_x2y=3.8881e+00 ppl_x2y=48.82 loss_y2x=3.9416e+00 ppl_y2x=51.50 dual_loss=0.0000e+00
Validation X2Y - loss=3.6706e+00 ppl=39.28 best_loss=3.7889e+00 best_ppl=44.21                                          
Validation Y2X - loss=3.7120e+00 ppl=40.94 best_loss=3.8424e+00 best_ppl=46.64
Epoch 5 - |param|=9.09e+02 |g_param|=2.88e+05 loss_x2y=3.8588e+00 ppl_x2y=47.41 loss_y2x=3.8938e+00 ppl_y2x=49.10 dual_loss=0.0000e+00
Validation X2Y - loss=3.5750e+00 ppl=35.69 best_loss=3.6706e+00 best_ppl=39.28                                          
Validation Y2X - loss=3.6087e+00 ppl=36.92 best_loss=3.7120e+00 best_ppl=40.94
Epoch 6 - |param|=9.09e+02 |g_param|=2.88e+05 loss_x2y=3.7523e+00 ppl_x2y=42.62 loss_y2x=3.7800e+00 ppl_y2x=43.82 dual_loss=0.0000e+00
Validation X2Y - loss=3.5000e+00 ppl=33.12 best_loss=3.5750e+00 best_ppl=35.69                                          
Validation Y2X - loss=3.5409e+00 ppl=34.50 best_loss=3.6087e+00 best_ppl=36.92
Epoch 7 - |param|=9.10e+02 |g_param|=2.53e+05 loss_x2y=3.6243e+00 ppl_x2y=37.50 loss_y2x=3.5772e+00 ppl_y2x=35.77 dual_loss=0.0000e+00
Validation X2Y - loss=3.3622e+00 ppl=28.85 best_loss=3.5000e+00 best_ppl=33.12                                          
Validation Y2X - loss=3.2477e+00 ppl=25.73 best_loss=3.5409e+00 best_ppl=34.50
Epoch 8 - |param|=9.11e+02 |g_param|=3.44e+05 loss_x2y=3.4753e+00 ppl_x2y=32.31 loss_y2x=3.2877e+00 ppl_y2x=26.78 dual_loss=0.0000e+00
Validation X2Y - loss=3.2018e+00 ppl=24.58 best_loss=3.3622e+00 best_ppl=28.85                                          
Validation Y2X - loss=3.0166e+00 ppl=20.42 best_loss=3.2477e+00 best_ppl=25.73
Epoch 9 - |param|=9.12e+02 |g_param|=3.36e+05 loss_x2y=3.2707e+00 ppl_x2y=26.33 loss_y2x=3.0485e+00 ppl_y2x=21.08 dual_loss=0.0000e+00
Validation X2Y - loss=3.1127e+00 ppl=22.48 best_loss=3.2018e+00 best_ppl=24.58                                          
Validation Y2X - loss=2.8105e+00 ppl=16.62 best_loss=3.0166e+00 best_ppl=20.42
Epoch 10 - |param|=9.13e+02 |g_param|=2.86e+05 loss_x2y=3.1574e+00 ppl_x2y=23.51 loss_y2x=2.8697e+00 ppl_y2x=17.63 dual_loss=0.0000e+00
Validation X2Y - loss=2.9578e+00 ppl=19.26 best_loss=3.1127e+00 best_ppl=22.48                                          
Validation Y2X - loss=2.6123e+00 ppl=13.63 best_loss=2.8105e+00 best_ppl=16.62
Epoch 11 - |param|=9.14e+02 |g_param|=3.04e+05 loss_x2y=2.9334e+00 ppl_x2y=18.79 loss_y2x=2.6067e+00 ppl_y2x=13.55 dual_loss=0.0000e+00
Validation X2Y - loss=2.7121e+00 ppl=15.06 best_loss=2.9578e+00 best_ppl=19.26                                          
Validation Y2X - loss=2.4045e+00 ppl=11.07 best_loss=2.6123e+00 best_ppl=13.63
Epoch 12 - |param|=9.15e+02 |g_param|=2.38e+05 loss_x2y=2.7150e+00 ppl_x2y=15.10 loss_y2x=2.2905e+00 ppl_y2x=9.88 dual_loss=0.0000e+00
Validation X2Y - loss=2.5103e+00 ppl=12.31 best_loss=2.7121e+00 best_ppl=15.06                                          
Validation Y2X - loss=2.1341e+00 ppl=8.45 best_loss=2.4045e+00 best_ppl=11.07
Epoch 13 - |param|=9.16e+02 |g_param|=2.72e+05 loss_x2y=2.4759e+00 ppl_x2y=11.89 loss_y2x=2.0873e+00 ppl_y2x=8.06 dual_loss=0.0000e+00
Validation X2Y - loss=2.4411e+00 ppl=11.49 best_loss=2.5103e+00 best_ppl=12.31                                          
Validation Y2X - loss=2.0196e+00 ppl=7.54 best_loss=2.1341e+00 best_ppl=8.45
Epoch 14 - |param|=9.17e+02 |g_param|=2.69e+05 loss_x2y=2.3191e+00 ppl_x2y=10.17 loss_y2x=1.9245e+00 ppl_y2x=6.85 dual_loss=0.0000e+00
Validation X2Y - loss=2.2117e+00 ppl=9.13 best_loss=2.4411e+00 best_ppl=11.49                                           
Validation Y2X - loss=1.8410e+00 ppl=6.30 best_loss=2.0196e+00 best_ppl=7.54
Epoch 15 - |param|=9.18e+02 |g_param|=1.50e+05 loss_x2y=2.0988e+00 ppl_x2y=8.16 loss_y2x=1.7177e+00 ppl_y2x=5.57 dual_loss=0.0000e+00
Validation X2Y - loss=2.0729e+00 ppl=7.95 best_loss=2.2117e+00 best_ppl=9.13                                            
Validation Y2X - loss=1.6826e+00 ppl=5.38 best_loss=1.8410e+00 best_ppl=6.30
Epoch 16 - |param|=9.19e+02 |g_param|=1.94e+05 loss_x2y=2.0792e+00 ppl_x2y=8.00 loss_y2x=1.6723e+00 ppl_y2x=5.32 dual_loss=0.0000e+00
Validation X2Y - loss=1.9768e+00 ppl=7.22 best_loss=2.0729e+00 best_ppl=7.95                                            
Validation Y2X - loss=1.5999e+00 ppl=4.95 best_loss=1.6826e+00 best_ppl=5.38
Epoch 17 - |param|=9.20e+02 |g_param|=2.43e+05 loss_x2y=2.0092e+00 ppl_x2y=7.46 loss_y2x=1.6076e+00 ppl_y2x=4.99 dual_loss=0.0000e+00
Validation X2Y - loss=1.9448e+00 ppl=6.99 best_loss=1.9768e+00 best_ppl=7.22                                            
Validation Y2X - loss=1.5025e+00 ppl=4.49 best_loss=1.5999e+00 best_ppl=4.95
Epoch 18 - |param|=9.21e+02 |g_param|=1.49e+05 loss_x2y=1.7684e+00 ppl_x2y=5.86 loss_y2x=1.3388e+00 ppl_y2x=3.81 dual_loss=0.0000e+00
Validation X2Y - loss=1.7789e+00 ppl=5.92 best_loss=1.9448e+00 best_ppl=6.99                                            
Validation Y2X - loss=1.3287e+00 ppl=3.78 best_loss=1.5025e+00 best_ppl=4.49
Epoch 19 - |param|=9.21e+02 |g_param|=1.91e+05 loss_x2y=1.6878e+00 ppl_x2y=5.41 loss_y2x=1.2253e+00 ppl_y2x=3.41 dual_loss=0.0000e+00
Validation X2Y - loss=1.7811e+00 ppl=5.94 best_loss=1.7789e+00 best_ppl=5.92                                            
Validation Y2X - loss=1.2919e+00 ppl=3.64 best_loss=1.3287e+00 best_ppl=3.78
Epoch 20 - |param|=9.22e+02 |g_param|=1.97e+05 loss_x2y=1.6904e+00 ppl_x2y=5.42 loss_y2x=1.1816e+00 ppl_y2x=3.26 dual_loss=0.0000e+00
Validation X2Y - loss=1.9028e+00 ppl=6.70 best_loss=1.7789e+00 best_ppl=5.92                                            
Validation Y2X - loss=1.2567e+00 ppl=3.51 best_loss=1.2919e+00 best_ppl=3.64
Epoch 21 - |param|=9.23e+02 |g_param|=1.52e+05 loss_x2y=1.7160e+00 ppl_x2y=5.56 loss_y2x=1.2099e+00 ppl_y2x=3.35 dual_loss=2.1932e+00
Validation X2Y - loss=1.6271e+00 ppl=5.09 best_loss=1.7789e+00 best_ppl=5.92                                            
Validation Y2X - loss=1.1621e+00 ppl=3.20 best_loss=1.2567e+00 best_ppl=3.51
Epoch 22 - |param|=9.24e+02 |g_param|=1.18e+05 loss_x2y=1.7032e+00 ppl_x2y=5.49 loss_y2x=1.1370e+00 ppl_y2x=3.12 dual_loss=2.2806e+00
Validation X2Y - loss=1.6197e+00 ppl=5.05 best_loss=1.6271e+00 best_ppl=5.09                                            
Validation Y2X - loss=1.0865e+00 ppl=2.96 best_loss=1.1621e+00 best_ppl=3.20
Epoch 23 - |param|=9.24e+02 |g_param|=8.78e+04 loss_x2y=1.4377e+00 ppl_x2y=4.21 loss_y2x=1.0152e+00 ppl_y2x=2.76 dual_loss=1.3729e+00
Validation X2Y - loss=1.5370e+00 ppl=4.65 best_loss=1.6197e+00 best_ppl=5.05                                            
Validation Y2X - loss=1.0729e+00 ppl=2.92 best_loss=1.0865e+00 best_ppl=2.96
Epoch 24 - |param|=9.25e+02 |g_param|=1.42e+05 loss_x2y=1.4311e+00 ppl_x2y=4.18 loss_y2x=1.0374e+00 ppl_y2x=2.82 dual_loss=1.2789e+00
Validation X2Y - loss=1.4921e+00 ppl=4.45 best_loss=1.5370e+00 best_ppl=4.65                                            
Validation Y2X - loss=1.0807e+00 ppl=2.95 best_loss=1.0729e+00 best_ppl=2.92
Epoch 25 - |param|=9.26e+02 |g_param|=8.04e+04 loss_x2y=1.2965e+00 ppl_x2y=3.66 loss_y2x=9.1601e-01 ppl_y2x=2.50 dual_loss=1.1249e+00
Validation X2Y - loss=1.4226e+00 ppl=4.15 best_loss=1.4921e+00 best_ppl=4.45                                            
Validation Y2X - loss=9.9512e-01 ppl=2.71 best_loss=1.0729e+00 best_ppl=2.92
Epoch 26 - |param|=9.26e+02 |g_param|=8.36e+04 loss_x2y=1.2191e+00 ppl_x2y=3.38 loss_y2x=9.3093e-01 ppl_y2x=2.54 dual_loss=9.4630e-01
Validation X2Y - loss=1.3636e+00 ppl=3.91 best_loss=1.4226e+00 best_ppl=4.15                                            
Validation Y2X - loss=1.0144e+00 ppl=2.76 best_loss=9.9512e-01 best_ppl=2.71
Epoch 27 - |param|=9.27e+02 |g_param|=5.25e+04 loss_x2y=1.1687e+00 ppl_x2y=3.22 loss_y2x=9.3537e-01 ppl_y2x=2.55 dual_loss=8.8276e-01
Validation X2Y - loss=1.3627e+00 ppl=3.91 best_loss=1.3636e+00 best_ppl=3.91                                            
Validation Y2X - loss=9.8232e-01 ppl=2.67 best_loss=9.9512e-01 best_ppl=2.71
Epoch 28 - |param|=9.28e+02 |g_param|=3.89e+04 loss_x2y=1.1083e+00 ppl_x2y=3.03 loss_y2x=8.2476e-01 ppl_y2x=2.28 dual_loss=7.7038e-01
Validation X2Y - loss=1.2973e+00 ppl=3.66 best_loss=1.3627e+00 best_ppl=3.91                                            
Validation Y2X - loss=9.3510e-01 ppl=2.55 best_loss=9.8232e-01 best_ppl=2.67
Epoch 29 - |param|=9.28e+02 |g_param|=2.04e+04 loss_x2y=1.0206e+00 ppl_x2y=2.77 loss_y2x=7.6347e-01 ppl_y2x=2.15 dual_loss=8.9417e-01
Validation X2Y - loss=1.2529e+00 ppl=3.50 best_loss=1.2973e+00 best_ppl=3.66                                            
Validation Y2X - loss=8.9181e-01 ppl=2.44 best_loss=9.3510e-01 best_ppl=2.55
Epoch 30 - |param|=9.29e+02 |g_param|=1.99e+04 loss_x2y=9.7241e-01 ppl_x2y=2.64 loss_y2x=7.2501e-01 ppl_y2x=2.06 dual_loss=6.6856e-01
Validation X2Y - loss=1.2492e+00 ppl=3.49 best_loss=1.2529e+00 best_ppl=3.50                                            
Validation Y2X - loss=8.8822e-01 ppl=2.43 best_loss=8.9181e-01 best_ppl=2.44
Epoch 31 - |param|=9.29e+02 |g_param|=2.12e+04 loss_x2y=9.5076e-01 ppl_x2y=2.59 loss_y2x=6.7291e-01 ppl_y2x=1.96 dual_loss=6.9044e-01
Validation X2Y - loss=1.2021e+00 ppl=3.33 best_loss=1.2492e+00 best_ppl=3.49                                            
Validation Y2X - loss=8.4163e-01 ppl=2.32 best_loss=8.8822e-01 best_ppl=2.43
Epoch 32 - |param|=9.30e+02 |g_param|=4.05e+04 loss_x2y=1.4590e+00 ppl_x2y=4.30 loss_y2x=8.0351e-01 ppl_y2x=2.23 dual_loss=3.8068e+00
Validation X2Y - loss=1.3324e+00 ppl=3.79 best_loss=1.2021e+00 best_ppl=3.33                                            
Validation Y2X - loss=8.4074e-01 ppl=2.32 best_loss=8.4163e-01 best_ppl=2.32
Epoch 33 - |param|=9.31e+02 |g_param|=3.24e+04 loss_x2y=1.0810e+00 ppl_x2y=2.95 loss_y2x=6.7501e-01 ppl_y2x=1.96 dual_loss=1.8093e+00
Validation X2Y - loss=1.1634e+00 ppl=3.20 best_loss=1.2021e+00 best_ppl=3.33                                            
Validation Y2X - loss=8.3079e-01 ppl=2.30 best_loss=8.4074e-01 best_ppl=2.32
Epoch 34 - |param|=9.31e+02 |g_param|=2.50e+04 loss_x2y=9.4710e-01 ppl_x2y=2.58 loss_y2x=6.3861e-01 ppl_y2x=1.89 dual_loss=9.3811e-01
Validation X2Y - loss=1.1338e+00 ppl=3.11 best_loss=1.1634e+00 best_ppl=3.20                                            
Validation Y2X - loss=8.4026e-01 ppl=2.32 best_loss=8.3079e-01 best_ppl=2.30
Epoch 35 - |param|=9.32e+02 |g_param|=2.46e+04 loss_x2y=8.6251e-01 ppl_x2y=2.37 loss_y2x=8.5293e-01 ppl_y2x=2.35 dual_loss=1.8488e+00
Validation X2Y - loss=1.0657e+00 ppl=2.90 best_loss=1.1338e+00 best_ppl=3.11                                            
Validation Y2X - loss=9.9818e-01 ppl=2.71 best_loss=8.3079e-01 best_ppl=2.30
Epoch 36 - |param|=9.32e+02 |g_param|=3.57e+04 loss_x2y=8.5142e-01 ppl_x2y=2.34 loss_y2x=8.7800e-01 ppl_y2x=2.41 dual_loss=2.1130e+00
Validation X2Y - loss=1.0577e+00 ppl=2.88 best_loss=1.0657e+00 best_ppl=2.90                                            
Validation Y2X - loss=1.1612e+00 ppl=3.19 best_loss=8.3079e-01 best_ppl=2.30
Epoch 37 - |param|=9.33e+02 |g_param|=1.18e+04 loss_x2y=7.5056e-01 ppl_x2y=2.12 loss_y2x=6.3786e-01 ppl_y2x=1.89 dual_loss=4.8978e-01
Validation X2Y - loss=1.0486e+00 ppl=2.85 best_loss=1.0577e+00 best_ppl=2.88                                            
Validation Y2X - loss=7.9738e-01 ppl=2.22 best_loss=8.3079e-01 best_ppl=2.30
Epoch 38 - |param|=9.33e+02 |g_param|=1.13e+04 loss_x2y=7.3958e-01 ppl_x2y=2.10 loss_y2x=5.8082e-01 ppl_y2x=1.79 dual_loss=4.0918e-01
Validation X2Y - loss=1.0569e+00 ppl=2.88 best_loss=1.0486e+00 best_ppl=2.85                                            
Validation Y2X - loss=7.6937e-01 ppl=2.16 best_loss=7.9738e-01 best_ppl=2.22
Epoch 39 - |param|=9.34e+02 |g_param|=1.22e+04 loss_x2y=7.2810e-01 ppl_x2y=2.07 loss_y2x=5.5110e-01 ppl_y2x=1.74 dual_loss=4.1701e-01
Validation X2Y - loss=1.0319e+00 ppl=2.81 best_loss=1.0486e+00 best_ppl=2.85                                            
Validation Y2X - loss=7.6035e-01 ppl=2.14 best_loss=7.6937e-01 best_ppl=2.16
Epoch 40 - |param|=9.34e+02 |g_param|=1.25e+04 loss_x2y=7.3420e-01 ppl_x2y=2.08 loss_y2x=5.5801e-01 ppl_y2x=1.75 dual_loss=4.2007e-01
Validation X2Y - loss=1.0179e+00 ppl=2.77 best_loss=1.0319e+00 best_ppl=2.81                                            
Validation Y2X - loss=7.5448e-01 ppl=2.13 best_loss=7.6035e-01 best_ppl=2.14
Epoch 41 - |param|=9.35e+02 |g_param|=1.23e+04 loss_x2y=6.6328e-01 ppl_x2y=1.94 loss_y2x=5.0333e-01 ppl_y2x=1.65 dual_loss=3.7090e-01
Validation X2Y - loss=1.0361e+00 ppl=2.82 best_loss=1.0179e+00 best_ppl=2.77                                            
Validation Y2X - loss=7.5065e-01 ppl=2.12 best_loss=7.5448e-01 best_ppl=2.13
Epoch 42 - |param|=9.35e+02 |g_param|=2.05e+04 loss_x2y=7.3147e-01 ppl_x2y=2.08 loss_y2x=5.2941e-01 ppl_y2x=1.70 dual_loss=6.9735e-01
Validation X2Y - loss=1.0323e+00 ppl=2.81 best_loss=1.0179e+00 best_ppl=2.77                                            
Validation Y2X - loss=7.4401e-01 ppl=2.10 best_loss=7.5065e-01 best_ppl=2.12
Epoch 43 - |param|=9.36e+02 |g_param|=1.94e+04 loss_x2y=6.9867e-01 ppl_x2y=2.01 loss_y2x=4.9762e-01 ppl_y2x=1.64 dual_loss=8.6322e-01
Validation X2Y - loss=1.0422e+00 ppl=2.84 best_loss=1.0179e+00 best_ppl=2.77                                            
Validation Y2X - loss=7.3561e-01 ppl=2.09 best_loss=7.4401e-01 best_ppl=2.10
Epoch 44 - |param|=9.36e+02 |g_param|=1.59e+04 loss_x2y=7.2920e-01 ppl_x2y=2.07 loss_y2x=4.8099e-01 ppl_y2x=1.62 dual_loss=6.6295e-01
Validation X2Y - loss=9.5233e-01 ppl=2.59 best_loss=1.0179e+00 best_ppl=2.77                                            
Validation Y2X - loss=7.3654e-01 ppl=2.09 best_loss=7.3561e-01 best_ppl=2.09
Epoch 45 - |param|=9.37e+02 |g_param|=1.20e+04 loss_x2y=6.7520e-01 ppl_x2y=1.96 loss_y2x=4.7848e-01 ppl_y2x=1.61 dual_loss=4.7036e-01
Validation X2Y - loss=9.5548e-01 ppl=2.60 best_loss=9.5233e-01 best_ppl=2.59                                            
Validation Y2X - loss=7.2523e-01 ppl=2.07 best_loss=7.3561e-01 best_ppl=2.09
Epoch 46 - |param|=9.37e+02 |g_param|=1.06e+04 loss_x2y=6.1224e-01 ppl_x2y=1.84 loss_y2x=4.6713e-01 ppl_y2x=1.60 dual_loss=3.6470e-01
Validation X2Y - loss=9.2029e-01 ppl=2.51 best_loss=9.5233e-01 best_ppl=2.59                                            
Validation Y2X - loss=7.3408e-01 ppl=2.08 best_loss=7.2523e-01 best_ppl=2.07
Epoch 47 - |param|=9.37e+02 |g_param|=1.01e+04 loss_x2y=5.8646e-01 ppl_x2y=1.80 loss_y2x=4.7472e-01 ppl_y2x=1.61 dual_loss=3.3886e-01
Validation X2Y - loss=9.1967e-01 ppl=2.51 best_loss=9.2029e-01 best_ppl=2.51                                            
Validation Y2X - loss=7.2078e-01 ppl=2.06 best_loss=7.2523e-01 best_ppl=2.07
Epoch 48 - |param|=9.38e+02 |g_param|=1.48e+04 loss_x2y=5.6050e-01 ppl_x2y=1.75 loss_y2x=4.5631e-01 ppl_y2x=1.58 dual_loss=3.9161e-01
Validation X2Y - loss=9.1616e-01 ppl=2.50 best_loss=9.1967e-01 best_ppl=2.51                                            
Validation Y2X - loss=7.9257e-01 ppl=2.21 best_loss=7.2078e-01 best_ppl=2.06
Epoch 49 - |param|=9.38e+02 |g_param|=1.49e+04 loss_x2y=5.8259e-01 ppl_x2y=1.79 loss_y2x=5.5837e-01 ppl_y2x=1.75 dual_loss=1.5273e+00
Validation X2Y - loss=9.4122e-01 ppl=2.56 best_loss=9.1616e-01 best_ppl=2.50                                            
Validation Y2X - loss=7.3717e-01 ppl=2.09 best_loss=7.2078e-01 best_ppl=2.06
Epoch 50 - |param|=9.39e+02 |g_param|=1.39e+04 loss_x2y=5.3670e-01 ppl_x2y=1.71 loss_y2x=4.6575e-01 ppl_y2x=1.59 dual_loss=3.7375e-01
Validation X2Y - loss=9.0262e-01 ppl=2.47 best_loss=9.1616e-01 best_ppl=2.50                                            
Validation Y2X - loss=7.2869e-01 ppl=2.07 best_loss=7.2078e-01 best_ppl=2.06
Epoch 51 - |param|=9.39e+02 |g_param|=1.59e+04 loss_x2y=5.2087e-01 ppl_x2y=1.68 loss_y2x=4.5894e-01 ppl_y2x=1.58 dual_loss=4.0295e-01
Validation X2Y - loss=8.9882e-01 ppl=2.46 best_loss=9.0262e-01 best_ppl=2.47                                            
Validation Y2X - loss=7.3160e-01 ppl=2.08 best_loss=7.2078e-01 best_ppl=2.06
Epoch 52 - |param|=9.40e+02 |g_param|=1.49e+04 loss_x2y=5.1203e-01 ppl_x2y=1.67 loss_y2x=4.4871e-01 ppl_y2x=1.57 dual_loss=3.6589e-01
Validation X2Y - loss=8.8116e-01 ppl=2.41 best_loss=8.9882e-01 best_ppl=2.46                                            
Validation Y2X - loss=7.2247e-01 ppl=2.06 best_loss=7.2078e-01 best_ppl=2.06
Epoch 53 - |param|=9.40e+02 |g_param|=1.36e+04 loss_x2y=4.9947e-01 ppl_x2y=1.65 loss_y2x=4.2299e-01 ppl_y2x=1.53 dual_loss=3.2234e-01
Validation X2Y - loss=8.7530e-01 ppl=2.40 best_loss=8.8116e-01 best_ppl=2.41                                            
Validation Y2X - loss=7.2134e-01 ppl=2.06 best_loss=7.2078e-01 best_ppl=2.06
Epoch 54 - |param|=9.41e+02 |g_param|=1.78e+04 loss_x2y=5.3264e-01 ppl_x2y=1.70 loss_y2x=5.5681e-01 ppl_y2x=1.75 dual_loss=1.0334e+00
Validation X2Y - loss=8.7730e-01 ppl=2.40 best_loss=8.7530e-01 best_ppl=2.40                                            
Validation Y2X - loss=8.3324e-01 ppl=2.30 best_loss=7.2078e-01 best_ppl=2.06
Epoch 55 - |param|=9.41e+02 |g_param|=1.41e+04 loss_x2y=4.9222e-01 ppl_x2y=1.64 loss_y2x=4.4822e-01 ppl_y2x=1.57 dual_loss=4.2702e-01
Validation X2Y - loss=8.8450e-01 ppl=2.42 best_loss=8.7530e-01 best_ppl=2.40                                            
Validation Y2X - loss=7.2618e-01 ppl=2.07 best_loss=7.2078e-01 best_ppl=2.06
Epoch 56 - |param|=9.41e+02 |g_param|=1.89e+04 loss_x2y=4.9471e-01 ppl_x2y=1.64 loss_y2x=4.0603e-01 ppl_y2x=1.50 dual_loss=4.5999e-01
Validation X2Y - loss=8.6588e-01 ppl=2.38 best_loss=8.7530e-01 best_ppl=2.40                                            
Validation Y2X - loss=6.9009e-01 ppl=1.99 best_loss=7.2078e-01 best_ppl=2.06
Epoch 57 - |param|=9.42e+02 |g_param|=2.20e+04 loss_x2y=5.2307e-01 ppl_x2y=1.69 loss_y2x=3.8688e-01 ppl_y2x=1.47 dual_loss=3.9165e-01
Validation X2Y - loss=8.8304e-01 ppl=2.42 best_loss=8.6588e-01 best_ppl=2.38                                            
Validation Y2X - loss=6.8616e-01 ppl=1.99 best_loss=6.9009e-01 best_ppl=1.99
Epoch 58 - |param|=9.42e+02 |g_param|=1.91e+04 loss_x2y=4.6909e-01 ppl_x2y=1.60 loss_y2x=3.6531e-01 ppl_y2x=1.44 dual_loss=2.7315e-01
Validation X2Y - loss=8.8027e-01 ppl=2.41 best_loss=8.6588e-01 best_ppl=2.38                                            
Validation Y2X - loss=6.8006e-01 ppl=1.97 best_loss=6.8616e-01 best_ppl=1.99
Epoch 59 - |param|=9.43e+02 |g_param|=5.07e+04 loss_x2y=5.9599e-01 ppl_x2y=1.81 loss_y2x=3.8319e-01 ppl_y2x=1.47 dual_loss=8.7559e-01
Validation X2Y - loss=9.1451e-01 ppl=2.50 best_loss=8.6588e-01 best_ppl=2.38                                            
Validation Y2X - loss=6.7988e-01 ppl=1.97 best_loss=6.8006e-01 best_ppl=1.97
Epoch 60 - |param|=9.43e+02 |g_param|=1.85e+04 loss_x2y=4.9881e-01 ppl_x2y=1.65 loss_y2x=3.6361e-01 ppl_y2x=1.44 dual_loss=3.3730e-01
Validation X2Y - loss=8.4694e-01 ppl=2.33 best_loss=8.6588e-01 best_ppl=2.38                                            
Validation Y2X - loss=6.7878e-01 ppl=1.97 best_loss=6.7988e-01 best_ppl=1.97

real	25m15.328s
user	24m59.098s
sys	0m16.652s
```

#### Warmup-Epoch 20, Total Epoch 70

```
Epoch 1 - |param|=9.08e+02 |g_param|=3.47e+05 loss_x2y=4.4457e+00 ppl_x2y=85.26 loss_y2x=4.4581e+00 ppl_y2x=86.32 dual_loss=0.0000e+00
Validation X2Y - loss=4.0533e+00 ppl=57.59 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=4.0664e+00 ppl=58.35 best_loss=inf best_ppl=inf
Epoch 2 - |param|=9.08e+02 |g_param|=2.55e+05 loss_x2y=4.1843e+00 ppl_x2y=65.65 loss_y2x=4.2078e+00 ppl_y2x=67.21 dual_loss=0.0000e+00
Validation X2Y - loss=3.9028e+00 ppl=49.54 best_loss=4.0533e+00 best_ppl=57.59                                          
Validation Y2X - loss=3.9101e+00 ppl=49.90 best_loss=4.0664e+00 best_ppl=58.35
Epoch 3 - |param|=9.08e+02 |g_param|=2.48e+05 loss_x2y=4.0224e+00 ppl_x2y=55.83 loss_y2x=4.0458e+00 ppl_y2x=57.16 dual_loss=0.0000e+00
Validation X2Y - loss=3.8085e+00 ppl=45.08 best_loss=3.9028e+00 best_ppl=49.54                                          
Validation Y2X - loss=3.8085e+00 ppl=45.08 best_loss=3.9101e+00 best_ppl=49.90
Epoch 4 - |param|=9.08e+02 |g_param|=2.71e+05 loss_x2y=3.9631e+00 ppl_x2y=52.62 loss_y2x=3.9527e+00 ppl_y2x=52.08 dual_loss=0.0000e+00
Validation X2Y - loss=3.7122e+00 ppl=40.94 best_loss=3.8085e+00 best_ppl=45.08                                          
Validation Y2X - loss=3.7032e+00 ppl=40.58 best_loss=3.8085e+00 best_ppl=45.08
Epoch 5 - |param|=9.09e+02 |g_param|=2.71e+05 loss_x2y=3.8578e+00 ppl_x2y=47.36 loss_y2x=3.8744e+00 ppl_y2x=48.16 dual_loss=0.0000e+00
Validation X2Y - loss=3.5986e+00 ppl=36.55 best_loss=3.7122e+00 best_ppl=40.94                                          
Validation Y2X - loss=3.6139e+00 ppl=37.11 best_loss=3.7032e+00 best_ppl=40.58
Epoch 6 - |param|=9.10e+02 |g_param|=2.82e+05 loss_x2y=3.7487e+00 ppl_x2y=42.47 loss_y2x=3.7777e+00 ppl_y2x=43.72 dual_loss=0.0000e+00
Validation X2Y - loss=3.5021e+00 ppl=33.19 best_loss=3.5986e+00 best_ppl=36.55                                          
Validation Y2X - loss=3.5384e+00 ppl=34.41 best_loss=3.6139e+00 best_ppl=37.11
Epoch 7 - |param|=9.11e+02 |g_param|=2.00e+05 loss_x2y=3.5873e+00 ppl_x2y=36.13 loss_y2x=3.5831e+00 ppl_y2x=35.98 dual_loss=0.0000e+00
Validation X2Y - loss=3.3265e+00 ppl=27.84 best_loss=3.5021e+00 best_ppl=33.19                                          
Validation Y2X - loss=3.3317e+00 ppl=27.99 best_loss=3.5384e+00 best_ppl=34.41
Epoch 8 - |param|=9.11e+02 |g_param|=2.11e+05 loss_x2y=3.4293e+00 ppl_x2y=30.86 loss_y2x=3.4385e+00 ppl_y2x=31.14 dual_loss=0.0000e+00
Validation X2Y - loss=3.1500e+00 ppl=23.34 best_loss=3.3265e+00 best_ppl=27.84                                          
Validation Y2X - loss=3.1659e+00 ppl=23.71 best_loss=3.3317e+00 best_ppl=27.99
Epoch 9 - |param|=9.12e+02 |g_param|=2.63e+05 loss_x2y=3.2793e+00 ppl_x2y=26.56 loss_y2x=3.3001e+00 ppl_y2x=27.11 dual_loss=0.0000e+00
Validation X2Y - loss=3.0317e+00 ppl=20.73 best_loss=3.1500e+00 best_ppl=23.34                                          
Validation Y2X - loss=3.0344e+00 ppl=20.79 best_loss=3.1659e+00 best_ppl=23.71
Epoch 10 - |param|=9.13e+02 |g_param|=2.62e+05 loss_x2y=3.0119e+00 ppl_x2y=20.33 loss_y2x=3.1232e+00 ppl_y2x=22.72 dual_loss=0.0000e+00
Validation X2Y - loss=2.7697e+00 ppl=15.95 best_loss=3.0317e+00 best_ppl=20.73                                          
Validation Y2X - loss=2.8841e+00 ppl=17.89 best_loss=3.0344e+00 best_ppl=20.79
Epoch 11 - |param|=9.14e+02 |g_param|=3.15e+05 loss_x2y=2.7489e+00 ppl_x2y=15.63 loss_y2x=2.9128e+00 ppl_y2x=18.41 dual_loss=0.0000e+00
Validation X2Y - loss=2.5887e+00 ppl=13.31 best_loss=2.7697e+00 best_ppl=15.95                                          
Validation Y2X - loss=2.7312e+00 ppl=15.35 best_loss=2.8841e+00 best_ppl=17.89
Epoch 12 - |param|=9.15e+02 |g_param|=1.96e+05 loss_x2y=2.6182e+00 ppl_x2y=13.71 loss_y2x=2.7453e+00 ppl_y2x=15.57 dual_loss=0.0000e+00
Validation X2Y - loss=2.4557e+00 ppl=11.65 best_loss=2.5887e+00 best_ppl=13.31                                          
Validation Y2X - loss=2.5875e+00 ppl=13.30 best_loss=2.7312e+00 best_ppl=15.35
Epoch 13 - |param|=9.16e+02 |g_param|=1.63e+05 loss_x2y=2.4789e+00 ppl_x2y=11.93 loss_y2x=2.6490e+00 ppl_y2x=14.14 dual_loss=0.0000e+00
Validation X2Y - loss=2.3031e+00 ppl=10.00 best_loss=2.4557e+00 best_ppl=11.65                                          
Validation Y2X - loss=2.4312e+00 ppl=11.37 best_loss=2.5875e+00 best_ppl=13.30
Epoch 14 - |param|=9.17e+02 |g_param|=1.36e+05 loss_x2y=2.3047e+00 ppl_x2y=10.02 loss_y2x=2.4162e+00 ppl_y2x=11.20 dual_loss=0.0000e+00
Validation X2Y - loss=2.1902e+00 ppl=8.94 best_loss=2.3031e+00 best_ppl=10.00                                           
Validation Y2X - loss=2.2141e+00 ppl=9.15 best_loss=2.4312e+00 best_ppl=11.37
Epoch 15 - |param|=9.18e+02 |g_param|=1.44e+05 loss_x2y=2.1190e+00 ppl_x2y=8.32 loss_y2x=2.1863e+00 ppl_y2x=8.90 dual_loss=0.0000e+00
Validation X2Y - loss=2.0738e+00 ppl=7.96 best_loss=2.1902e+00 best_ppl=8.94                                            
Validation Y2X - loss=2.1011e+00 ppl=8.17 best_loss=2.2141e+00 best_ppl=9.15
Epoch 16 - |param|=9.18e+02 |g_param|=1.24e+05 loss_x2y=1.9776e+00 ppl_x2y=7.23 loss_y2x=1.9860e+00 ppl_y2x=7.29 dual_loss=0.0000e+00
Validation X2Y - loss=1.9480e+00 ppl=7.01 best_loss=2.0738e+00 best_ppl=7.96                                            
Validation Y2X - loss=1.8638e+00 ppl=6.45 best_loss=2.1011e+00 best_ppl=8.17
Epoch 17 - |param|=9.19e+02 |g_param|=1.24e+05 loss_x2y=1.8140e+00 ppl_x2y=6.13 loss_y2x=1.8005e+00 ppl_y2x=6.05 dual_loss=0.0000e+00
Validation X2Y - loss=1.8218e+00 ppl=6.18 best_loss=1.9480e+00 best_ppl=7.01                                            
Validation Y2X - loss=1.7349e+00 ppl=5.67 best_loss=1.8638e+00 best_ppl=6.45
Epoch 18 - |param|=9.20e+02 |g_param|=1.65e+05 loss_x2y=1.7246e+00 ppl_x2y=5.61 loss_y2x=1.7150e+00 ppl_y2x=5.56 dual_loss=0.0000e+00
Validation X2Y - loss=1.7400e+00 ppl=5.70 best_loss=1.8218e+00 best_ppl=6.18                                            
Validation Y2X - loss=1.6532e+00 ppl=5.22 best_loss=1.7349e+00 best_ppl=5.67
Epoch 19 - |param|=9.21e+02 |g_param|=1.83e+05 loss_x2y=1.6279e+00 ppl_x2y=5.09 loss_y2x=1.6915e+00 ppl_y2x=5.43 dual_loss=0.0000e+00
Validation X2Y - loss=1.6927e+00 ppl=5.43 best_loss=1.7400e+00 best_ppl=5.70                                            
Validation Y2X - loss=1.7052e+00 ppl=5.50 best_loss=1.6532e+00 best_ppl=5.22
Epoch 20 - |param|=9.21e+02 |g_param|=1.69e+05 loss_x2y=1.5659e+00 ppl_x2y=4.79 loss_y2x=1.5202e+00 ppl_y2x=4.57 dual_loss=0.0000e+00
Validation X2Y - loss=1.5590e+00 ppl=4.75 best_loss=1.6927e+00 best_ppl=5.43                                            
Validation Y2X - loss=1.4878e+00 ppl=4.43 best_loss=1.6532e+00 best_ppl=5.22
Epoch 21 - |param|=9.22e+02 |g_param|=1.47e+05 loss_x2y=1.4542e+00 ppl_x2y=4.28 loss_y2x=1.4383e+00 ppl_y2x=4.21 dual_loss=7.8841e-01
Validation X2Y - loss=1.4232e+00 ppl=4.15 best_loss=1.5590e+00 best_ppl=4.75                                            
Validation Y2X - loss=1.3527e+00 ppl=3.87 best_loss=1.4878e+00 best_ppl=4.43
Epoch 22 - |param|=9.23e+02 |g_param|=1.41e+05 loss_x2y=1.2893e+00 ppl_x2y=3.63 loss_y2x=1.3905e+00 ppl_y2x=4.02 dual_loss=1.3265e+00
Validation X2Y - loss=1.3527e+00 ppl=3.87 best_loss=1.4232e+00 best_ppl=4.15                                            
Validation Y2X - loss=1.3906e+00 ppl=4.02 best_loss=1.3527e+00 best_ppl=3.87
Epoch 23 - |param|=9.24e+02 |g_param|=8.17e+04 loss_x2y=1.1706e+00 ppl_x2y=3.22 loss_y2x=1.2479e+00 ppl_y2x=3.48 dual_loss=8.4103e-01
Validation X2Y - loss=1.2800e+00 ppl=3.60 best_loss=1.3527e+00 best_ppl=3.87                                            
Validation Y2X - loss=1.2599e+00 ppl=3.53 best_loss=1.3527e+00 best_ppl=3.87
Epoch 24 - |param|=9.24e+02 |g_param|=1.09e+05 loss_x2y=1.1473e+00 ppl_x2y=3.15 loss_y2x=1.2036e+00 ppl_y2x=3.33 dual_loss=8.3319e-01
Validation X2Y - loss=1.3657e+00 ppl=3.92 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.3328e+00 ppl=3.79 best_loss=1.2599e+00 best_ppl=3.53
Epoch 25 - |param|=9.25e+02 |g_param|=7.44e+04 loss_x2y=1.1123e+00 ppl_x2y=3.04 loss_y2x=1.1161e+00 ppl_y2x=3.05 dual_loss=6.3620e-01
Validation X2Y - loss=1.1847e+00 ppl=3.27 best_loss=1.2800e+00 best_ppl=3.60                                            
Validation Y2X - loss=1.1568e+00 ppl=3.18 best_loss=1.2599e+00 best_ppl=3.53
Epoch 26 - |param|=9.25e+02 |g_param|=8.15e+04 loss_x2y=1.0734e+00 ppl_x2y=2.93 loss_y2x=1.1125e+00 ppl_y2x=3.04 dual_loss=7.2342e-01
Validation X2Y - loss=1.1774e+00 ppl=3.25 best_loss=1.1847e+00 best_ppl=3.27                                            
Validation Y2X - loss=1.1829e+00 ppl=3.26 best_loss=1.1568e+00 best_ppl=3.18
Epoch 27 - |param|=9.26e+02 |g_param|=9.44e+04 loss_x2y=1.1593e+00 ppl_x2y=3.19 loss_y2x=1.0041e+00 ppl_y2x=2.73 dual_loss=8.6538e-01
Validation X2Y - loss=1.1794e+00 ppl=3.25 best_loss=1.1774e+00 best_ppl=3.25                                            
Validation Y2X - loss=1.0844e+00 ppl=2.96 best_loss=1.1568e+00 best_ppl=3.18
Epoch 28 - |param|=9.27e+02 |g_param|=7.30e+04 loss_x2y=9.6158e-01 ppl_x2y=2.62 loss_y2x=9.2400e-01 ppl_y2x=2.52 dual_loss=5.5629e-01
Validation X2Y - loss=1.1216e+00 ppl=3.07 best_loss=1.1774e+00 best_ppl=3.25                                            
Validation Y2X - loss=1.0453e+00 ppl=2.84 best_loss=1.0844e+00 best_ppl=2.96
Epoch 29 - |param|=9.27e+02 |g_param|=5.80e+04 loss_x2y=8.6831e-01 ppl_x2y=2.38 loss_y2x=8.5107e-01 ppl_y2x=2.34 dual_loss=5.0743e-01
Validation X2Y - loss=1.0581e+00 ppl=2.88 best_loss=1.1216e+00 best_ppl=3.07                                            
Validation Y2X - loss=9.9278e-01 ppl=2.70 best_loss=1.0453e+00 best_ppl=2.84
Epoch 30 - |param|=9.28e+02 |g_param|=6.63e+04 loss_x2y=1.0121e+00 ppl_x2y=2.75 loss_y2x=8.4210e-01 ppl_y2x=2.32 dual_loss=1.2393e+00
Validation X2Y - loss=1.3752e+00 ppl=3.96 best_loss=1.0581e+00 best_ppl=2.88                                            
Validation Y2X - loss=9.5161e-01 ppl=2.59 best_loss=9.9278e-01 best_ppl=2.70
Epoch 31 - |param|=9.28e+02 |g_param|=4.27e+04 loss_x2y=9.6188e-01 ppl_x2y=2.62 loss_y2x=8.1141e-01 ppl_y2x=2.25 dual_loss=9.4054e-01
Validation X2Y - loss=1.0059e+00 ppl=2.73 best_loss=1.0581e+00 best_ppl=2.88                                            
Validation Y2X - loss=9.4194e-01 ppl=2.56 best_loss=9.5161e-01 best_ppl=2.59
Epoch 32 - |param|=9.29e+02 |g_param|=6.46e+04 loss_x2y=8.2650e-01 ppl_x2y=2.29 loss_y2x=8.6570e-01 ppl_y2x=2.38 dual_loss=8.7541e-01
Validation X2Y - loss=9.4684e-01 ppl=2.58 best_loss=1.0059e+00 best_ppl=2.73                                            
Validation Y2X - loss=9.7664e-01 ppl=2.66 best_loss=9.4194e-01 best_ppl=2.56
Epoch 33 - |param|=9.30e+02 |g_param|=3.73e+04 loss_x2y=7.3813e-01 ppl_x2y=2.09 loss_y2x=7.5270e-01 ppl_y2x=2.12 dual_loss=5.1439e-01
Validation X2Y - loss=9.2281e-01 ppl=2.52 best_loss=9.4684e-01 best_ppl=2.58                                            
Validation Y2X - loss=9.5603e-01 ppl=2.60 best_loss=9.4194e-01 best_ppl=2.56
Epoch 34 - |param|=9.30e+02 |g_param|=4.68e+04 loss_x2y=7.2988e-01 ppl_x2y=2.07 loss_y2x=7.5542e-01 ppl_y2x=2.13 dual_loss=5.9736e-01
Validation X2Y - loss=9.0454e-01 ppl=2.47 best_loss=9.2281e-01 best_ppl=2.52                                            
Validation Y2X - loss=9.1491e-01 ppl=2.50 best_loss=9.4194e-01 best_ppl=2.56
Epoch 35 - |param|=9.31e+02 |g_param|=5.24e+04 loss_x2y=7.1384e-01 ppl_x2y=2.04 loss_y2x=7.7300e-01 ppl_y2x=2.17 dual_loss=6.9864e-01
Validation X2Y - loss=8.7172e-01 ppl=2.39 best_loss=9.0454e-01 best_ppl=2.47                                            
Validation Y2X - loss=8.8210e-01 ppl=2.42 best_loss=9.1491e-01 best_ppl=2.50
Epoch 36 - |param|=9.31e+02 |g_param|=3.50e+04 loss_x2y=6.5818e-01 ppl_x2y=1.93 loss_y2x=6.7538e-01 ppl_y2x=1.96 dual_loss=4.9583e-01
Validation X2Y - loss=8.6216e-01 ppl=2.37 best_loss=8.7172e-01 best_ppl=2.39                                            
Validation Y2X - loss=8.3539e-01 ppl=2.31 best_loss=8.8210e-01 best_ppl=2.42
Epoch 37 - |param|=9.32e+02 |g_param|=2.73e+04 loss_x2y=6.6090e-01 ppl_x2y=1.94 loss_y2x=7.2775e-01 ppl_y2x=2.07 dual_loss=8.2980e-01
Validation X2Y - loss=8.5285e-01 ppl=2.35 best_loss=8.6216e-01 best_ppl=2.37                                            
Validation Y2X - loss=8.6550e-01 ppl=2.38 best_loss=8.3539e-01 best_ppl=2.31
Epoch 38 - |param|=9.32e+02 |g_param|=1.94e+04 loss_x2y=6.1159e-01 ppl_x2y=1.84 loss_y2x=6.3734e-01 ppl_y2x=1.89 dual_loss=5.6218e-01
Validation X2Y - loss=8.4956e-01 ppl=2.34 best_loss=8.5285e-01 best_ppl=2.35                                            
Validation Y2X - loss=8.6331e-01 ppl=2.37 best_loss=8.3539e-01 best_ppl=2.31
Epoch 39 - |param|=9.33e+02 |g_param|=1.92e+04 loss_x2y=5.9954e-01 ppl_x2y=1.82 loss_y2x=6.3911e-01 ppl_y2x=1.89 dual_loss=6.4202e-01
Validation X2Y - loss=8.2780e-01 ppl=2.29 best_loss=8.4956e-01 best_ppl=2.34                                            
Validation Y2X - loss=8.2457e-01 ppl=2.28 best_loss=8.3539e-01 best_ppl=2.31
Epoch 40 - |param|=9.33e+02 |g_param|=1.67e+04 loss_x2y=5.8033e-01 ppl_x2y=1.79 loss_y2x=5.9708e-01 ppl_y2x=1.82 dual_loss=4.7431e-01
Validation X2Y - loss=8.2428e-01 ppl=2.28 best_loss=8.2780e-01 best_ppl=2.29                                            
Validation Y2X - loss=8.0066e-01 ppl=2.23 best_loss=8.2457e-01 best_ppl=2.28
Epoch 41 - |param|=9.34e+02 |g_param|=3.27e+04 loss_x2y=8.2220e-01 ppl_x2y=2.28 loss_y2x=6.2370e-01 ppl_y2x=1.87 dual_loss=1.4836e+00
Validation X2Y - loss=1.1465e+00 ppl=3.15 best_loss=8.2428e-01 best_ppl=2.28                                            
Validation Y2X - loss=7.8240e-01 ppl=2.19 best_loss=8.0066e-01 best_ppl=2.23
Epoch 42 - |param|=9.34e+02 |g_param|=2.26e+04 loss_x2y=7.1133e-01 ppl_x2y=2.04 loss_y2x=5.4957e-01 ppl_y2x=1.73 dual_loss=5.9890e-01
Validation X2Y - loss=8.3308e-01 ppl=2.30 best_loss=8.2428e-01 best_ppl=2.28                                            
Validation Y2X - loss=7.6596e-01 ppl=2.15 best_loss=7.8240e-01 best_ppl=2.19
Epoch 43 - |param|=9.35e+02 |g_param|=2.01e+04 loss_x2y=5.7430e-01 ppl_x2y=1.78 loss_y2x=5.5815e-01 ppl_y2x=1.75 dual_loss=5.0671e-01
Validation X2Y - loss=8.0018e-01 ppl=2.23 best_loss=8.2428e-01 best_ppl=2.28                                            
Validation Y2X - loss=7.7905e-01 ppl=2.18 best_loss=7.6596e-01 best_ppl=2.15
Epoch 44 - |param|=9.35e+02 |g_param|=1.95e+04 loss_x2y=5.2542e-01 ppl_x2y=1.69 loss_y2x=5.4041e-01 ppl_y2x=1.72 dual_loss=5.5652e-01
Validation X2Y - loss=7.7475e-01 ppl=2.17 best_loss=8.0018e-01 best_ppl=2.23                                            
Validation Y2X - loss=8.0445e-01 ppl=2.24 best_loss=7.6596e-01 best_ppl=2.15
Epoch 45 - |param|=9.36e+02 |g_param|=1.67e+04 loss_x2y=5.2284e-01 ppl_x2y=1.69 loss_y2x=5.2527e-01 ppl_y2x=1.69 dual_loss=4.6693e-01
Validation X2Y - loss=7.7653e-01 ppl=2.17 best_loss=7.7475e-01 best_ppl=2.17                                            
Validation Y2X - loss=7.6231e-01 ppl=2.14 best_loss=7.6596e-01 best_ppl=2.15
Epoch 46 - |param|=9.36e+02 |g_param|=2.20e+04 loss_x2y=4.8926e-01 ppl_x2y=1.63 loss_y2x=5.0266e-01 ppl_y2x=1.65 dual_loss=5.0056e-01
Validation X2Y - loss=7.6646e-01 ppl=2.15 best_loss=7.7475e-01 best_ppl=2.17                                            
Validation Y2X - loss=7.6674e-01 ppl=2.15 best_loss=7.6231e-01 best_ppl=2.14
Epoch 47 - |param|=9.36e+02 |g_param|=1.82e+04 loss_x2y=4.8909e-01 ppl_x2y=1.63 loss_y2x=4.9852e-01 ppl_y2x=1.65 dual_loss=4.3982e-01
Validation X2Y - loss=7.7540e-01 ppl=2.17 best_loss=7.6646e-01 best_ppl=2.15                                            
Validation Y2X - loss=7.5638e-01 ppl=2.13 best_loss=7.6231e-01 best_ppl=2.14
Epoch 48 - |param|=9.37e+02 |g_param|=1.49e+04 loss_x2y=4.9253e-01 ppl_x2y=1.64 loss_y2x=4.8769e-01 ppl_y2x=1.63 dual_loss=4.0459e-01
Validation X2Y - loss=7.5632e-01 ppl=2.13 best_loss=7.6646e-01 best_ppl=2.15                                            
Validation Y2X - loss=7.2281e-01 ppl=2.06 best_loss=7.5638e-01 best_ppl=2.13
Epoch 49 - |param|=9.37e+02 |g_param|=1.41e+04 loss_x2y=4.5263e-01 ppl_x2y=1.57 loss_y2x=4.5352e-01 ppl_y2x=1.57 dual_loss=3.7738e-01
Validation X2Y - loss=7.4931e-01 ppl=2.12 best_loss=7.5632e-01 best_ppl=2.13                                            
Validation Y2X - loss=7.3809e-01 ppl=2.09 best_loss=7.2281e-01 best_ppl=2.06
Epoch 50 - |param|=9.38e+02 |g_param|=1.81e+04 loss_x2y=4.6235e-01 ppl_x2y=1.59 loss_y2x=4.7691e-01 ppl_y2x=1.61 dual_loss=4.8380e-01
Validation X2Y - loss=7.4436e-01 ppl=2.11 best_loss=7.4931e-01 best_ppl=2.12                                            
Validation Y2X - loss=7.3327e-01 ppl=2.08 best_loss=7.2281e-01 best_ppl=2.06
Epoch 51 - |param|=9.38e+02 |g_param|=2.64e+04 loss_x2y=4.4954e-01 ppl_x2y=1.57 loss_y2x=5.0623e-01 ppl_y2x=1.66 dual_loss=6.6039e-01
Validation X2Y - loss=7.4434e-01 ppl=2.11 best_loss=7.4436e-01 best_ppl=2.11                                            
Validation Y2X - loss=7.5127e-01 ppl=2.12 best_loss=7.2281e-01 best_ppl=2.06
Epoch 52 - |param|=9.39e+02 |g_param|=2.11e+04 loss_x2y=4.2899e-01 ppl_x2y=1.54 loss_y2x=4.7130e-01 ppl_y2x=1.60 dual_loss=5.1872e-01
Validation X2Y - loss=7.1857e-01 ppl=2.05 best_loss=7.4434e-01 best_ppl=2.11                                            
Validation Y2X - loss=7.2342e-01 ppl=2.06 best_loss=7.2281e-01 best_ppl=2.06
Epoch 53 - |param|=9.39e+02 |g_param|=2.07e+04 loss_x2y=4.3606e-01 ppl_x2y=1.55 loss_y2x=4.5916e-01 ppl_y2x=1.58 dual_loss=5.1914e-01
Validation X2Y - loss=7.2457e-01 ppl=2.06 best_loss=7.1857e-01 best_ppl=2.05                                            
Validation Y2X - loss=7.2436e-01 ppl=2.06 best_loss=7.2281e-01 best_ppl=2.06
Epoch 54 - |param|=9.40e+02 |g_param|=2.30e+04 loss_x2y=4.1742e-01 ppl_x2y=1.52 loss_y2x=4.5629e-01 ppl_y2x=1.58 dual_loss=5.5631e-01
Validation X2Y - loss=7.2125e-01 ppl=2.06 best_loss=7.1857e-01 best_ppl=2.05                                            
Validation Y2X - loss=7.1130e-01 ppl=2.04 best_loss=7.2281e-01 best_ppl=2.06
Epoch 55 - |param|=9.40e+02 |g_param|=2.40e+04 loss_x2y=4.2620e-01 ppl_x2y=1.53 loss_y2x=4.3233e-01 ppl_y2x=1.54 dual_loss=4.3586e-01
Validation X2Y - loss=7.2960e-01 ppl=2.07 best_loss=7.1857e-01 best_ppl=2.05                                            
Validation Y2X - loss=7.0606e-01 ppl=2.03 best_loss=7.1130e-01 best_ppl=2.04
Epoch 56 - |param|=9.40e+02 |g_param|=2.16e+04 loss_x2y=4.2606e-01 ppl_x2y=1.53 loss_y2x=4.1560e-01 ppl_y2x=1.52 dual_loss=4.9533e-01
Validation X2Y - loss=7.1972e-01 ppl=2.05 best_loss=7.1857e-01 best_ppl=2.05                                            
Validation Y2X - loss=6.8664e-01 ppl=1.99 best_loss=7.0606e-01 best_ppl=2.03
Epoch 57 - |param|=9.41e+02 |g_param|=4.12e+04 loss_x2y=5.0217e-01 ppl_x2y=1.65 loss_y2x=4.0592e-01 ppl_y2x=1.50 dual_loss=5.6679e-01
Validation X2Y - loss=7.8586e-01 ppl=2.19 best_loss=7.1857e-01 best_ppl=2.05                                            
Validation Y2X - loss=6.6462e-01 ppl=1.94 best_loss=6.8664e-01 best_ppl=1.99
Epoch 58 - |param|=9.41e+02 |g_param|=2.99e+04 loss_x2y=4.6811e-01 ppl_x2y=1.60 loss_y2x=3.7994e-01 ppl_y2x=1.46 dual_loss=3.5101e-01
Validation X2Y - loss=7.2967e-01 ppl=2.07 best_loss=7.1857e-01 best_ppl=2.05                                            
Validation Y2X - loss=6.7394e-01 ppl=1.96 best_loss=6.6462e-01 best_ppl=1.94
Epoch 59 - |param|=9.42e+02 |g_param|=2.65e+04 loss_x2y=4.0656e-01 ppl_x2y=1.50 loss_y2x=3.7320e-01 ppl_y2x=1.45 dual_loss=3.7088e-01
Validation X2Y - loss=7.1817e-01 ppl=2.05 best_loss=7.1857e-01 best_ppl=2.05                                            
Validation Y2X - loss=6.7500e-01 ppl=1.96 best_loss=6.6462e-01 best_ppl=1.94
Epoch 60 - |param|=9.42e+02 |g_param|=3.60e+04 loss_x2y=4.9280e-01 ppl_x2y=1.64 loss_y2x=3.7713e-01 ppl_y2x=1.46 dual_loss=5.1265e-01
Validation X2Y - loss=7.7917e-01 ppl=2.18 best_loss=7.1817e-01 best_ppl=2.05                                            
Validation Y2X - loss=6.8293e-01 ppl=1.98 best_loss=6.6462e-01 best_ppl=1.94
Epoch 61 - |param|=9.43e+02 |g_param|=2.78e+04 loss_x2y=4.0279e-01 ppl_x2y=1.50 loss_y2x=3.6610e-01 ppl_y2x=1.44 dual_loss=3.1582e-01
Validation X2Y - loss=6.8681e-01 ppl=1.99 best_loss=7.1817e-01 best_ppl=2.05                                            
Validation Y2X - loss=6.7711e-01 ppl=1.97 best_loss=6.6462e-01 best_ppl=1.94
Epoch 62 - |param|=9.43e+02 |g_param|=1.93e+04 loss_x2y=3.7579e-01 ppl_x2y=1.46 loss_y2x=3.7900e-01 ppl_y2x=1.46 dual_loss=4.5168e-01
Validation X2Y - loss=6.7672e-01 ppl=1.97 best_loss=6.8681e-01 best_ppl=1.99                                            
Validation Y2X - loss=6.7973e-01 ppl=1.97 best_loss=6.6462e-01 best_ppl=1.94
Epoch 63 - |param|=9.44e+02 |g_param|=1.94e+04 loss_x2y=3.7732e-01 ppl_x2y=1.46 loss_y2x=3.5842e-01 ppl_y2x=1.43 dual_loss=3.9056e-01
Validation X2Y - loss=7.1946e-01 ppl=2.05 best_loss=6.7672e-01 best_ppl=1.97                                            
Validation Y2X - loss=6.8200e-01 ppl=1.98 best_loss=6.6462e-01 best_ppl=1.94
Epoch 64 - |param|=9.44e+02 |g_param|=1.64e+04 loss_x2y=3.7842e-01 ppl_x2y=1.46 loss_y2x=3.5879e-01 ppl_y2x=1.43 dual_loss=3.1010e-01
Validation X2Y - loss=6.9879e-01 ppl=2.01 best_loss=6.7672e-01 best_ppl=1.97                                            
Validation Y2X - loss=6.7251e-01 ppl=1.96 best_loss=6.6462e-01 best_ppl=1.94
Epoch 65 - |param|=9.44e+02 |g_param|=1.70e+04 loss_x2y=3.5835e-01 ppl_x2y=1.43 loss_y2x=3.4985e-01 ppl_y2x=1.42 dual_loss=3.3007e-01
Validation X2Y - loss=6.8159e-01 ppl=1.98 best_loss=6.7672e-01 best_ppl=1.97                                            
Validation Y2X - loss=6.6974e-01 ppl=1.95 best_loss=6.6462e-01 best_ppl=1.94
Epoch 66 - |param|=9.45e+02 |g_param|=1.83e+04 loss_x2y=3.5726e-01 ppl_x2y=1.43 loss_y2x=3.7410e-01 ppl_y2x=1.45 dual_loss=4.1302e-01
Validation X2Y - loss=6.7309e-01 ppl=1.96 best_loss=6.7672e-01 best_ppl=1.97                                            
Validation Y2X - loss=6.6307e-01 ppl=1.94 best_loss=6.6462e-01 best_ppl=1.94
Epoch 67 - |param|=9.45e+02 |g_param|=1.61e+04 loss_x2y=3.3253e-01 ppl_x2y=1.39 loss_y2x=3.4510e-01 ppl_y2x=1.41 dual_loss=3.9197e-01
Validation X2Y - loss=6.6859e-01 ppl=1.95 best_loss=6.7309e-01 best_ppl=1.96                                            
Validation Y2X - loss=6.6687e-01 ppl=1.95 best_loss=6.6307e-01 best_ppl=1.94
Epoch 68 - |param|=9.46e+02 |g_param|=1.69e+04 loss_x2y=3.4725e-01 ppl_x2y=1.42 loss_y2x=3.5477e-01 ppl_y2x=1.43 dual_loss=3.7801e-01
Validation X2Y - loss=6.7193e-01 ppl=1.96 best_loss=6.6859e-01 best_ppl=1.95                                            
Validation Y2X - loss=6.8089e-01 ppl=1.98 best_loss=6.6307e-01 best_ppl=1.94
Epoch 69 - |param|=9.46e+02 |g_param|=1.53e+04 loss_x2y=3.1571e-01 ppl_x2y=1.37 loss_y2x=3.1188e-01 ppl_y2x=1.37 dual_loss=3.9072e-01
Validation X2Y - loss=6.8147e-01 ppl=1.98 best_loss=6.6859e-01 best_ppl=1.95                                            
Validation Y2X - loss=6.8352e-01 ppl=1.98 best_loss=6.6307e-01 best_ppl=1.94
Epoch 70 - |param|=9.47e+02 |g_param|=2.03e+04 loss_x2y=3.2198e-01 ppl_x2y=1.38 loss_y2x=3.5420e-01 ppl_y2x=1.43 dual_loss=4.5396e-01
Validation X2Y - loss=6.8578e-01 ppl=1.99 best_loss=6.6859e-01 best_ppl=1.95                                            
Validation Y2X - loss=6.9793e-01 ppl=2.01 best_loss=6.6307e-01 best_ppl=1.94

real	29m18.105s
user	28m59.898s
sys	0m19.032s
```

#### Warmup-Epoch 20, Total Epoch 80

```
Epoch 1 - |param|=9.07e+02 |g_param|=2.37e+05 loss_x2y=4.4215e+00 ppl_x2y=83.22 loss_y2x=4.4449e+00 ppl_y2x=85.19 dual_loss=0.0000e+00
Validation X2Y - loss=4.0572e+00 ppl=57.81 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=4.0756e+00 ppl=58.89 best_loss=inf best_ppl=inf
Epoch 2 - |param|=9.07e+02 |g_param|=2.01e+05 loss_x2y=4.1754e+00 ppl_x2y=65.07 loss_y2x=4.1953e+00 ppl_y2x=66.37 dual_loss=0.0000e+00
Validation X2Y - loss=3.8950e+00 ppl=49.16 best_loss=4.0572e+00 best_ppl=57.81                                          
Validation Y2X - loss=3.9161e+00 ppl=50.21 best_loss=4.0756e+00 best_ppl=58.89
Epoch 3 - |param|=9.07e+02 |g_param|=2.15e+05 loss_x2y=4.0078e+00 ppl_x2y=55.02 loss_y2x=4.0434e+00 ppl_y2x=57.02 dual_loss=0.0000e+00
Validation X2Y - loss=3.8694e+00 ppl=47.91 best_loss=3.8950e+00 best_ppl=49.16                                          
Validation Y2X - loss=3.8444e+00 ppl=46.73 best_loss=3.9161e+00 best_ppl=50.21
Epoch 4 - |param|=9.08e+02 |g_param|=2.06e+05 loss_x2y=3.9675e+00 ppl_x2y=52.85 loss_y2x=4.0110e+00 ppl_y2x=55.20 dual_loss=0.0000e+00
Validation X2Y - loss=3.7228e+00 ppl=41.38 best_loss=3.8694e+00 best_ppl=47.91                                          
Validation Y2X - loss=3.7753e+00 ppl=43.61 best_loss=3.8444e+00 best_ppl=46.73
Epoch 5 - |param|=9.08e+02 |g_param|=1.93e+05 loss_x2y=3.8906e+00 ppl_x2y=48.94 loss_y2x=3.9582e+00 ppl_y2x=52.36 dual_loss=0.0000e+00
Validation X2Y - loss=3.6090e+00 ppl=36.93 best_loss=3.7228e+00 best_ppl=41.38                                          
Validation Y2X - loss=3.7011e+00 ppl=40.49 best_loss=3.7753e+00 best_ppl=43.61
Epoch 6 - |param|=9.09e+02 |g_param|=2.06e+05 loss_x2y=3.8032e+00 ppl_x2y=44.85 loss_y2x=3.8747e+00 ppl_y2x=48.17 dual_loss=0.0000e+00
Validation X2Y - loss=3.5554e+00 ppl=35.00 best_loss=3.6090e+00 best_ppl=36.93                                          
Validation Y2X - loss=3.6191e+00 ppl=37.31 best_loss=3.7011e+00 best_ppl=40.49
Epoch 7 - |param|=9.09e+02 |g_param|=2.06e+05 loss_x2y=3.6919e+00 ppl_x2y=40.12 loss_y2x=3.8075e+00 ppl_y2x=45.04 dual_loss=0.0000e+00
Validation X2Y - loss=3.3918e+00 ppl=29.72 best_loss=3.5554e+00 best_ppl=35.00                                          
Validation Y2X - loss=3.5886e+00 ppl=36.18 best_loss=3.6191e+00 best_ppl=37.31
Epoch 8 - |param|=9.10e+02 |g_param|=2.04e+05 loss_x2y=3.4480e+00 ppl_x2y=31.44 loss_y2x=3.6399e+00 ppl_y2x=38.09 dual_loss=0.0000e+00
Validation X2Y - loss=3.2559e+00 ppl=25.94 best_loss=3.3918e+00 best_ppl=29.72                                          
Validation Y2X - loss=3.4294e+00 ppl=30.86 best_loss=3.5886e+00 best_ppl=36.18
Epoch 9 - |param|=9.11e+02 |g_param|=2.00e+05 loss_x2y=3.2693e+00 ppl_x2y=26.29 loss_y2x=3.3906e+00 ppl_y2x=29.68 dual_loss=0.0000e+00
Validation X2Y - loss=3.1228e+00 ppl=22.71 best_loss=3.2559e+00 best_ppl=25.94                                          
Validation Y2X - loss=3.2180e+00 ppl=24.98 best_loss=3.4294e+00 best_ppl=30.86
Epoch 10 - |param|=9.12e+02 |g_param|=2.96e+05 loss_x2y=3.2340e+00 ppl_x2y=25.38 loss_y2x=3.3335e+00 ppl_y2x=28.04 dual_loss=0.0000e+00
Validation X2Y - loss=3.0750e+00 ppl=21.65 best_loss=3.1228e+00 best_ppl=22.71                                          
Validation Y2X - loss=3.1091e+00 ppl=22.40 best_loss=3.2180e+00 best_ppl=24.98
Epoch 11 - |param|=9.13e+02 |g_param|=3.02e+05 loss_x2y=3.1027e+00 ppl_x2y=22.26 loss_y2x=3.1446e+00 ppl_y2x=23.21 dual_loss=0.0000e+00
Validation X2Y - loss=2.8993e+00 ppl=18.16 best_loss=3.0750e+00 best_ppl=21.65                                          
Validation Y2X - loss=2.9234e+00 ppl=18.60 best_loss=3.1091e+00 best_ppl=22.40
Epoch 12 - |param|=9.14e+02 |g_param|=1.71e+05 loss_x2y=2.9496e+00 ppl_x2y=19.10 loss_y2x=2.9407e+00 ppl_y2x=18.93 dual_loss=0.0000e+00
Validation X2Y - loss=2.7712e+00 ppl=15.98 best_loss=2.8993e+00 best_ppl=18.16                                          
Validation Y2X - loss=2.7696e+00 ppl=15.95 best_loss=2.9234e+00 best_ppl=18.60
Epoch 13 - |param|=9.15e+02 |g_param|=2.06e+05 loss_x2y=2.7721e+00 ppl_x2y=15.99 loss_y2x=2.8389e+00 ppl_y2x=17.10 dual_loss=0.0000e+00
Validation X2Y - loss=2.6187e+00 ppl=13.72 best_loss=2.7712e+00 best_ppl=15.98                                          
Validation Y2X - loss=2.6156e+00 ppl=13.67 best_loss=2.7696e+00 best_ppl=15.95
Epoch 14 - |param|=9.16e+02 |g_param|=1.83e+05 loss_x2y=2.5978e+00 ppl_x2y=13.43 loss_y2x=2.5772e+00 ppl_y2x=13.16 dual_loss=0.0000e+00
Validation X2Y - loss=2.4684e+00 ppl=11.80 best_loss=2.6187e+00 best_ppl=13.72                                          
Validation Y2X - loss=2.4641e+00 ppl=11.75 best_loss=2.6156e+00 best_ppl=13.67
Epoch 15 - |param|=9.17e+02 |g_param|=2.12e+05 loss_x2y=2.4083e+00 ppl_x2y=11.11 loss_y2x=2.4929e+00 ppl_y2x=12.10 dual_loss=0.0000e+00
Validation X2Y - loss=2.2422e+00 ppl=9.41 best_loss=2.4684e+00 best_ppl=11.80                                           
Validation Y2X - loss=2.3329e+00 ppl=10.31 best_loss=2.4641e+00 best_ppl=11.75
Epoch 16 - |param|=9.17e+02 |g_param|=2.01e+05 loss_x2y=2.2075e+00 ppl_x2y=9.09 loss_y2x=2.3842e+00 ppl_y2x=10.85 dual_loss=0.0000e+00
Validation X2Y - loss=2.0851e+00 ppl=8.05 best_loss=2.2422e+00 best_ppl=9.41                                            
Validation Y2X - loss=2.2253e+00 ppl=9.26 best_loss=2.3329e+00 best_ppl=10.31
Epoch 17 - |param|=9.18e+02 |g_param|=2.16e+05 loss_x2y=2.0243e+00 ppl_x2y=7.57 loss_y2x=2.2066e+00 ppl_y2x=9.08 dual_loss=0.0000e+00
Validation X2Y - loss=1.8909e+00 ppl=6.63 best_loss=2.0851e+00 best_ppl=8.05                                            
Validation Y2X - loss=2.1112e+00 ppl=8.26 best_loss=2.2253e+00 best_ppl=9.26
Epoch 18 - |param|=9.19e+02 |g_param|=2.55e+05 loss_x2y=1.8343e+00 ppl_x2y=6.26 loss_y2x=2.0701e+00 ppl_y2x=7.93 dual_loss=0.0000e+00
Validation X2Y - loss=1.8596e+00 ppl=6.42 best_loss=1.8909e+00 best_ppl=6.63                                            
Validation Y2X - loss=2.0495e+00 ppl=7.76 best_loss=2.1112e+00 best_ppl=8.26
Epoch 19 - |param|=9.20e+02 |g_param|=3.03e+05 loss_x2y=1.6696e+00 ppl_x2y=5.31 loss_y2x=1.9331e+00 ppl_y2x=6.91 dual_loss=0.0000e+00
Validation X2Y - loss=1.7016e+00 ppl=5.48 best_loss=1.8596e+00 best_ppl=6.42                                            
Validation Y2X - loss=1.9318e+00 ppl=6.90 best_loss=2.0495e+00 best_ppl=7.76
Epoch 20 - |param|=9.21e+02 |g_param|=2.28e+05 loss_x2y=1.5038e+00 ppl_x2y=4.50 loss_y2x=1.7767e+00 ppl_y2x=5.91 dual_loss=0.0000e+00
Validation X2Y - loss=1.4794e+00 ppl=4.39 best_loss=1.7016e+00 best_ppl=5.48                                            
Validation Y2X - loss=1.7452e+00 ppl=5.73 best_loss=1.9318e+00 best_ppl=6.90
Epoch 21 - |param|=9.22e+02 |g_param|=1.35e+05 loss_x2y=1.4590e+00 ppl_x2y=4.30 loss_y2x=1.7884e+00 ppl_y2x=5.98 dual_loss=2.8316e+00
Validation X2Y - loss=1.4050e+00 ppl=4.08 best_loss=1.4794e+00 best_ppl=4.39                                            
Validation Y2X - loss=1.6453e+00 ppl=5.18 best_loss=1.7452e+00 best_ppl=5.73
Epoch 22 - |param|=9.22e+02 |g_param|=7.88e+04 loss_x2y=1.3132e+00 ppl_x2y=3.72 loss_y2x=1.6564e+00 ppl_y2x=5.24 dual_loss=2.2440e+00
Validation X2Y - loss=1.3199e+00 ppl=3.74 best_loss=1.4050e+00 best_ppl=4.08                                            
Validation Y2X - loss=1.7217e+00 ppl=5.59 best_loss=1.6453e+00 best_ppl=5.18
Epoch 23 - |param|=9.23e+02 |g_param|=7.70e+04 loss_x2y=1.2400e+00 ppl_x2y=3.46 loss_y2x=1.6681e+00 ppl_y2x=5.30 dual_loss=2.4596e+00
Validation X2Y - loss=1.2649e+00 ppl=3.54 best_loss=1.3199e+00 best_ppl=3.74                                            
Validation Y2X - loss=1.5805e+00 ppl=4.86 best_loss=1.6453e+00 best_ppl=5.18
Epoch 24 - |param|=9.24e+02 |g_param|=8.45e+04 loss_x2y=1.2277e+00 ppl_x2y=3.41 loss_y2x=1.5143e+00 ppl_y2x=4.55 dual_loss=1.9698e+00
Validation X2Y - loss=1.2134e+00 ppl=3.36 best_loss=1.2649e+00 best_ppl=3.54                                            
Validation Y2X - loss=1.4712e+00 ppl=4.35 best_loss=1.5805e+00 best_ppl=4.86
Epoch 25 - |param|=9.25e+02 |g_param|=8.65e+04 loss_x2y=1.0972e+00 ppl_x2y=3.00 loss_y2x=1.4063e+00 ppl_y2x=4.08 dual_loss=1.9842e+00
Validation X2Y - loss=1.1764e+00 ppl=3.24 best_loss=1.2134e+00 best_ppl=3.36                                            
Validation Y2X - loss=1.4824e+00 ppl=4.40 best_loss=1.4712e+00 best_ppl=4.35
Epoch 26 - |param|=9.25e+02 |g_param|=1.67e+05 loss_x2y=1.2170e+00 ppl_x2y=3.38 loss_y2x=1.2809e+00 ppl_y2x=3.60 dual_loss=1.2912e+00
Validation X2Y - loss=1.3335e+00 ppl=3.79 best_loss=1.1764e+00 best_ppl=3.24                                            
Validation Y2X - loss=1.3341e+00 ppl=3.80 best_loss=1.4712e+00 best_ppl=4.35
Epoch 27 - |param|=9.26e+02 |g_param|=8.54e+04 loss_x2y=1.1477e+00 ppl_x2y=3.15 loss_y2x=1.1949e+00 ppl_y2x=3.30 dual_loss=1.0615e+00
Validation X2Y - loss=1.1762e+00 ppl=3.24 best_loss=1.1764e+00 best_ppl=3.24                                            
Validation Y2X - loss=1.2657e+00 ppl=3.55 best_loss=1.3341e+00 best_ppl=3.80
Epoch 28 - |param|=9.27e+02 |g_param|=4.27e+04 loss_x2y=9.4003e-01 ppl_x2y=2.56 loss_y2x=1.1846e+00 ppl_y2x=3.27 dual_loss=1.3807e+00
Validation X2Y - loss=1.0270e+00 ppl=2.79 best_loss=1.1762e+00 best_ppl=3.24                                            
Validation Y2X - loss=1.2585e+00 ppl=3.52 best_loss=1.2657e+00 best_ppl=3.55
Epoch 29 - |param|=9.27e+02 |g_param|=5.35e+04 loss_x2y=9.0646e-01 ppl_x2y=2.48 loss_y2x=1.0845e+00 ppl_y2x=2.96 dual_loss=1.0649e+00
Validation X2Y - loss=1.0312e+00 ppl=2.80 best_loss=1.0270e+00 best_ppl=2.79                                            
Validation Y2X - loss=1.2245e+00 ppl=3.40 best_loss=1.2585e+00 best_ppl=3.52
Epoch 30 - |param|=9.28e+02 |g_param|=8.73e+04 loss_x2y=1.0239e+00 ppl_x2y=2.78 loss_y2x=1.5002e+00 ppl_y2x=4.48 dual_loss=4.2549e+00
Validation X2Y - loss=9.7481e-01 ppl=2.65 best_loss=1.0270e+00 best_ppl=2.79                                            
Validation Y2X - loss=1.3595e+00 ppl=3.89 best_loss=1.2245e+00 best_ppl=3.40
Epoch 31 - |param|=9.28e+02 |g_param|=4.78e+04 loss_x2y=8.8149e-01 ppl_x2y=2.41 loss_y2x=1.1261e+00 ppl_y2x=3.08 dual_loss=1.3946e+00
Validation X2Y - loss=9.5021e-01 ppl=2.59 best_loss=9.7481e-01 best_ppl=2.65                                            
Validation Y2X - loss=1.1545e+00 ppl=3.17 best_loss=1.2245e+00 best_ppl=3.40
Epoch 32 - |param|=9.29e+02 |g_param|=3.32e+04 loss_x2y=7.4722e-01 ppl_x2y=2.11 loss_y2x=9.4367e-01 ppl_y2x=2.57 dual_loss=9.3638e-01
Validation X2Y - loss=9.3525e-01 ppl=2.55 best_loss=9.5021e-01 best_ppl=2.59                                            
Validation Y2X - loss=1.1182e+00 ppl=3.06 best_loss=1.1545e+00 best_ppl=3.17
Epoch 33 - |param|=9.29e+02 |g_param|=3.40e+04 loss_x2y=7.1188e-01 ppl_x2y=2.04 loss_y2x=9.0738e-01 ppl_y2x=2.48 dual_loss=9.1214e-01
Validation X2Y - loss=8.8874e-01 ppl=2.43 best_loss=9.3525e-01 best_ppl=2.55                                            
Validation Y2X - loss=1.0830e+00 ppl=2.95 best_loss=1.1182e+00 best_ppl=3.06
Epoch 34 - |param|=9.30e+02 |g_param|=4.12e+04 loss_x2y=7.1990e-01 ppl_x2y=2.05 loss_y2x=9.1540e-01 ppl_y2x=2.50 dual_loss=9.9721e-01
Validation X2Y - loss=8.7937e-01 ppl=2.41 best_loss=8.8874e-01 best_ppl=2.43                                            
Validation Y2X - loss=1.0740e+00 ppl=2.93 best_loss=1.0830e+00 best_ppl=2.95
Epoch 35 - |param|=9.30e+02 |g_param|=3.82e+04 loss_x2y=7.0141e-01 ppl_x2y=2.02 loss_y2x=8.8399e-01 ppl_y2x=2.42 dual_loss=1.0227e+00
Validation X2Y - loss=8.8025e-01 ppl=2.41 best_loss=8.7937e-01 best_ppl=2.41                                            
Validation Y2X - loss=1.0553e+00 ppl=2.87 best_loss=1.0740e+00 best_ppl=2.93
Epoch 36 - |param|=9.31e+02 |g_param|=5.26e+04 loss_x2y=6.8043e-01 ppl_x2y=1.97 loss_y2x=8.6725e-01 ppl_y2x=2.38 dual_loss=9.8277e-01
Validation X2Y - loss=9.0269e-01 ppl=2.47 best_loss=8.7937e-01 best_ppl=2.41                                            
Validation Y2X - loss=1.0719e+00 ppl=2.92 best_loss=1.0553e+00 best_ppl=2.87
Epoch 37 - |param|=9.31e+02 |g_param|=5.23e+04 loss_x2y=7.3703e-01 ppl_x2y=2.09 loss_y2x=8.4365e-01 ppl_y2x=2.32 dual_loss=8.0959e-01
Validation X2Y - loss=8.8137e-01 ppl=2.41 best_loss=8.7937e-01 best_ppl=2.41                                            
Validation Y2X - loss=9.9082e-01 ppl=2.69 best_loss=1.0553e+00 best_ppl=2.87
Epoch 38 - |param|=9.32e+02 |g_param|=3.03e+04 loss_x2y=6.1164e-01 ppl_x2y=1.84 loss_y2x=7.5640e-01 ppl_y2x=2.13 dual_loss=7.7427e-01
Validation X2Y - loss=8.2405e-01 ppl=2.28 best_loss=8.7937e-01 best_ppl=2.41                                            
Validation Y2X - loss=9.6615e-01 ppl=2.63 best_loss=9.9082e-01 best_ppl=2.69
Epoch 39 - |param|=9.32e+02 |g_param|=3.44e+04 loss_x2y=6.1483e-01 ppl_x2y=1.85 loss_y2x=7.6308e-01 ppl_y2x=2.14 dual_loss=9.1286e-01
Validation X2Y - loss=8.3209e-01 ppl=2.30 best_loss=8.2405e-01 best_ppl=2.28                                            
Validation Y2X - loss=9.8445e-01 ppl=2.68 best_loss=9.6615e-01 best_ppl=2.63
Epoch 40 - |param|=9.33e+02 |g_param|=3.52e+04 loss_x2y=5.7139e-01 ppl_x2y=1.77 loss_y2x=7.1829e-01 ppl_y2x=2.05 dual_loss=8.0936e-01
Validation X2Y - loss=8.1056e-01 ppl=2.25 best_loss=8.2405e-01 best_ppl=2.28                                            
Validation Y2X - loss=9.8257e-01 ppl=2.67 best_loss=9.6615e-01 best_ppl=2.63
Epoch 41 - |param|=9.33e+02 |g_param|=7.05e+04 loss_x2y=6.5170e-01 ppl_x2y=1.92 loss_y2x=9.1825e-01 ppl_y2x=2.50 dual_loss=2.6915e+00
Validation X2Y - loss=8.3242e-01 ppl=2.30 best_loss=8.1056e-01 best_ppl=2.25                                            
Validation Y2X - loss=9.9410e-01 ppl=2.70 best_loss=9.6615e-01 best_ppl=2.63
Epoch 42 - |param|=9.34e+02 |g_param|=6.08e+04 loss_x2y=6.7352e-01 ppl_x2y=1.96 loss_y2x=7.5825e-01 ppl_y2x=2.13 dual_loss=9.2401e-01
Validation X2Y - loss=8.4853e-01 ppl=2.34 best_loss=8.1056e-01 best_ppl=2.25                                            
Validation Y2X - loss=9.7423e-01 ppl=2.65 best_loss=9.6615e-01 best_ppl=2.63
Epoch 43 - |param|=9.35e+02 |g_param|=4.47e+04 loss_x2y=5.6989e-01 ppl_x2y=1.77 loss_y2x=6.9167e-01 ppl_y2x=2.00 dual_loss=7.2670e-01
Validation X2Y - loss=7.6586e-01 ppl=2.15 best_loss=8.1056e-01 best_ppl=2.25                                            
Validation Y2X - loss=9.1514e-01 ppl=2.50 best_loss=9.6615e-01 best_ppl=2.63
Epoch 44 - |param|=9.35e+02 |g_param|=4.39e+04 loss_x2y=5.4730e-01 ppl_x2y=1.73 loss_y2x=6.7066e-01 ppl_y2x=1.96 dual_loss=8.3512e-01
Validation X2Y - loss=7.8930e-01 ppl=2.20 best_loss=7.6586e-01 best_ppl=2.15                                            
Validation Y2X - loss=9.0505e-01 ppl=2.47 best_loss=9.1514e-01 best_ppl=2.50
Epoch 45 - |param|=9.35e+02 |g_param|=3.93e+04 loss_x2y=5.0931e-01 ppl_x2y=1.66 loss_y2x=6.3899e-01 ppl_y2x=1.89 dual_loss=7.4002e-01
Validation X2Y - loss=7.7480e-01 ppl=2.17 best_loss=7.6586e-01 best_ppl=2.15                                            
Validation Y2X - loss=8.8201e-01 ppl=2.42 best_loss=9.0505e-01 best_ppl=2.47
Epoch 46 - |param|=9.36e+02 |g_param|=4.74e+04 loss_x2y=5.1233e-01 ppl_x2y=1.67 loss_y2x=6.3235e-01 ppl_y2x=1.88 dual_loss=6.7781e-01
Validation X2Y - loss=7.6833e-01 ppl=2.16 best_loss=7.6586e-01 best_ppl=2.15                                            
Validation Y2X - loss=8.9005e-01 ppl=2.44 best_loss=8.8201e-01 best_ppl=2.42
Epoch 47 - |param|=9.36e+02 |g_param|=5.82e+04 loss_x2y=5.0730e-01 ppl_x2y=1.66 loss_y2x=6.2404e-01 ppl_y2x=1.87 dual_loss=8.3595e-01
Validation X2Y - loss=7.6192e-01 ppl=2.14 best_loss=7.6586e-01 best_ppl=2.15                                            
Validation Y2X - loss=8.7168e-01 ppl=2.39 best_loss=8.8201e-01 best_ppl=2.42
Epoch 48 - |param|=9.37e+02 |g_param|=6.04e+04 loss_x2y=4.7385e-01 ppl_x2y=1.61 loss_y2x=6.2375e-01 ppl_y2x=1.87 dual_loss=8.4149e-01
Validation X2Y - loss=7.6018e-01 ppl=2.14 best_loss=7.6192e-01 best_ppl=2.14                                            
Validation Y2X - loss=8.5690e-01 ppl=2.36 best_loss=8.7168e-01 best_ppl=2.39
Epoch 49 - |param|=9.37e+02 |g_param|=5.68e+04 loss_x2y=4.7278e-01 ppl_x2y=1.60 loss_y2x=5.9965e-01 ppl_y2x=1.82 dual_loss=6.9867e-01
Validation X2Y - loss=7.5254e-01 ppl=2.12 best_loss=7.6018e-01 best_ppl=2.14                                            
Validation Y2X - loss=8.6493e-01 ppl=2.37 best_loss=8.5690e-01 best_ppl=2.36
Epoch 50 - |param|=9.37e+02 |g_param|=6.26e+04 loss_x2y=4.5426e-01 ppl_x2y=1.58 loss_y2x=5.9509e-01 ppl_y2x=1.81 dual_loss=7.1820e-01
Validation X2Y - loss=7.3827e-01 ppl=2.09 best_loss=7.5254e-01 best_ppl=2.12                                            
Validation Y2X - loss=8.5725e-01 ppl=2.36 best_loss=8.5690e-01 best_ppl=2.36
Epoch 51 - |param|=9.38e+02 |g_param|=6.25e+04 loss_x2y=4.4834e-01 ppl_x2y=1.57 loss_y2x=5.5687e-01 ppl_y2x=1.75 dual_loss=6.7973e-01
Validation X2Y - loss=7.3914e-01 ppl=2.09 best_loss=7.3827e-01 best_ppl=2.09                                            
Validation Y2X - loss=8.5487e-01 ppl=2.35 best_loss=8.5690e-01 best_ppl=2.36
Epoch 52 - |param|=9.38e+02 |g_param|=4.57e+04 loss_x2y=4.6845e-01 ppl_x2y=1.60 loss_y2x=5.4534e-01 ppl_y2x=1.73 dual_loss=5.9328e-01
Validation X2Y - loss=7.3029e-01 ppl=2.08 best_loss=7.3827e-01 best_ppl=2.09                                            
Validation Y2X - loss=8.2047e-01 ppl=2.27 best_loss=8.5487e-01 best_ppl=2.35
Epoch 53 - |param|=9.39e+02 |g_param|=4.03e+04 loss_x2y=4.2400e-01 ppl_x2y=1.53 loss_y2x=5.2476e-01 ppl_y2x=1.69 dual_loss=6.0454e-01
Validation X2Y - loss=7.2680e-01 ppl=2.07 best_loss=7.3029e-01 best_ppl=2.08                                            
Validation Y2X - loss=8.2862e-01 ppl=2.29 best_loss=8.2047e-01 best_ppl=2.27
Epoch 54 - |param|=9.39e+02 |g_param|=4.90e+04 loss_x2y=4.3066e-01 ppl_x2y=1.54 loss_y2x=5.2887e-01 ppl_y2x=1.70 dual_loss=6.3859e-01
Validation X2Y - loss=7.2993e-01 ppl=2.07 best_loss=7.2680e-01 best_ppl=2.07                                            
Validation Y2X - loss=8.2559e-01 ppl=2.28 best_loss=8.2047e-01 best_ppl=2.27
Epoch 55 - |param|=9.40e+02 |g_param|=3.71e+04 loss_x2y=4.3073e-01 ppl_x2y=1.54 loss_y2x=5.2811e-01 ppl_y2x=1.70 dual_loss=5.6333e-01
Validation X2Y - loss=7.2859e-01 ppl=2.07 best_loss=7.2680e-01 best_ppl=2.07                                            
Validation Y2X - loss=8.1118e-01 ppl=2.25 best_loss=8.2047e-01 best_ppl=2.27
Epoch 56 - |param|=9.40e+02 |g_param|=4.32e+04 loss_x2y=4.0477e-01 ppl_x2y=1.50 loss_y2x=4.9380e-01 ppl_y2x=1.64 dual_loss=5.7167e-01
Validation X2Y - loss=7.1362e-01 ppl=2.04 best_loss=7.2680e-01 best_ppl=2.07                                            
Validation Y2X - loss=8.1424e-01 ppl=2.26 best_loss=8.1118e-01 best_ppl=2.25
Epoch 57 - |param|=9.41e+02 |g_param|=4.41e+04 loss_x2y=4.0467e-01 ppl_x2y=1.50 loss_y2x=4.9225e-01 ppl_y2x=1.64 dual_loss=6.3868e-01
Validation X2Y - loss=7.2799e-01 ppl=2.07 best_loss=7.1362e-01 best_ppl=2.04                                            
Validation Y2X - loss=7.9929e-01 ppl=2.22 best_loss=8.1118e-01 best_ppl=2.25
Epoch 58 - |param|=9.41e+02 |g_param|=3.60e+04 loss_x2y=4.3839e-01 ppl_x2y=1.55 loss_y2x=4.6820e-01 ppl_y2x=1.60 dual_loss=4.6402e-01
Validation X2Y - loss=7.2485e-01 ppl=2.06 best_loss=7.1362e-01 best_ppl=2.04                                            
Validation Y2X - loss=8.0613e-01 ppl=2.24 best_loss=7.9929e-01 best_ppl=2.22
Epoch 59 - |param|=9.41e+02 |g_param|=3.80e+04 loss_x2y=3.9003e-01 ppl_x2y=1.48 loss_y2x=4.5836e-01 ppl_y2x=1.58 dual_loss=5.2207e-01
Validation X2Y - loss=7.3764e-01 ppl=2.09 best_loss=7.1362e-01 best_ppl=2.04                                            
Validation Y2X - loss=8.4117e-01 ppl=2.32 best_loss=7.9929e-01 best_ppl=2.22
Epoch 60 - |param|=9.42e+02 |g_param|=6.79e+04 loss_x2y=3.8954e-01 ppl_x2y=1.48 loss_y2x=5.4791e-01 ppl_y2x=1.73 dual_loss=9.6435e-01
Validation X2Y - loss=7.1671e-01 ppl=2.05 best_loss=7.1362e-01 best_ppl=2.04                                            
Validation Y2X - loss=8.3441e-01 ppl=2.30 best_loss=7.9929e-01 best_ppl=2.22
Epoch 61 - |param|=9.42e+02 |g_param|=3.49e+04 loss_x2y=3.8618e-01 ppl_x2y=1.47 loss_y2x=5.0534e-01 ppl_y2x=1.66 dual_loss=6.7903e-01
Validation X2Y - loss=7.2956e-01 ppl=2.07 best_loss=7.1362e-01 best_ppl=2.04                                            
Validation Y2X - loss=7.7810e-01 ppl=2.18 best_loss=7.9929e-01 best_ppl=2.22
Epoch 62 - |param|=9.43e+02 |g_param|=4.60e+04 loss_x2y=3.6330e-01 ppl_x2y=1.44 loss_y2x=4.7171e-01 ppl_y2x=1.60 dual_loss=7.1463e-01
Validation X2Y - loss=7.2170e-01 ppl=2.06 best_loss=7.1362e-01 best_ppl=2.04                                            
Validation Y2X - loss=8.0437e-01 ppl=2.24 best_loss=7.7810e-01 best_ppl=2.18
Epoch 63 - |param|=9.43e+02 |g_param|=1.29e+05 loss_x2y=4.0393e-01 ppl_x2y=1.50 loss_y2x=5.5981e-01 ppl_y2x=1.75 dual_loss=1.0417e+00
Validation X2Y - loss=7.5297e-01 ppl=2.12 best_loss=7.1362e-01 best_ppl=2.04                                            
Validation Y2X - loss=8.8288e-01 ppl=2.42 best_loss=7.7810e-01 best_ppl=2.18
Epoch 64 - |param|=9.44e+02 |g_param|=8.82e+04 loss_x2y=3.5928e-01 ppl_x2y=1.43 loss_y2x=4.5368e-01 ppl_y2x=1.57 dual_loss=7.3494e-01
Validation X2Y - loss=7.4177e-01 ppl=2.10 best_loss=7.1362e-01 best_ppl=2.04                                            
Validation Y2X - loss=7.7827e-01 ppl=2.18 best_loss=7.7810e-01 best_ppl=2.18
Epoch 65 - |param|=9.44e+02 |g_param|=4.11e+04 loss_x2y=3.6980e-01 ppl_x2y=1.45 loss_y2x=4.6487e-01 ppl_y2x=1.59 dual_loss=6.0411e-01
Validation X2Y - loss=7.3218e-01 ppl=2.08 best_loss=7.1362e-01 best_ppl=2.04                                            
Validation Y2X - loss=7.8177e-01 ppl=2.19 best_loss=7.7810e-01 best_ppl=2.18
Epoch 66 - |param|=9.45e+02 |g_param|=5.66e+04 loss_x2y=3.4750e-01 ppl_x2y=1.42 loss_y2x=4.7138e-01 ppl_y2x=1.60 dual_loss=7.3597e-01
Validation X2Y - loss=7.3136e-01 ppl=2.08 best_loss=7.1362e-01 best_ppl=2.04                                            
Validation Y2X - loss=8.8096e-01 ppl=2.41 best_loss=7.7810e-01 best_ppl=2.18
Epoch 67 - |param|=9.45e+02 |g_param|=2.46e+04 loss_x2y=3.4687e-01 ppl_x2y=1.41 loss_y2x=4.5238e-01 ppl_y2x=1.57 dual_loss=7.4084e-01
Validation X2Y - loss=7.1945e-01 ppl=2.05 best_loss=7.1362e-01 best_ppl=2.04                                            
Validation Y2X - loss=7.8797e-01 ppl=2.20 best_loss=7.7810e-01 best_ppl=2.18
Epoch 68 - |param|=9.46e+02 |g_param|=2.15e+04 loss_x2y=3.3452e-01 ppl_x2y=1.40 loss_y2x=4.4415e-01 ppl_y2x=1.56 dual_loss=6.0944e-01
Validation X2Y - loss=7.2298e-01 ppl=2.06 best_loss=7.1362e-01 best_ppl=2.04                                            
Validation Y2X - loss=7.8431e-01 ppl=2.19 best_loss=7.7810e-01 best_ppl=2.18
Epoch 69 - |param|=9.46e+02 |g_param|=1.83e+04 loss_x2y=3.4538e-01 ppl_x2y=1.41 loss_y2x=4.3835e-01 ppl_y2x=1.55 dual_loss=6.1939e-01
Validation X2Y - loss=7.1281e-01 ppl=2.04 best_loss=7.1362e-01 best_ppl=2.04                                            
Validation Y2X - loss=7.6001e-01 ppl=2.14 best_loss=7.7810e-01 best_ppl=2.18
Epoch 70 - |param|=9.46e+02 |g_param|=1.66e+04 loss_x2y=3.2278e-01 ppl_x2y=1.38 loss_y2x=4.0388e-01 ppl_y2x=1.50 dual_loss=5.1769e-01
Validation X2Y - loss=7.0716e-01 ppl=2.03 best_loss=7.1281e-01 best_ppl=2.04                                            
Validation Y2X - loss=7.5851e-01 ppl=2.14 best_loss=7.6001e-01 best_ppl=2.14
Epoch 71 - |param|=9.47e+02 |g_param|=2.21e+04 loss_x2y=3.6399e-01 ppl_x2y=1.44 loss_y2x=3.9588e-01 ppl_y2x=1.49 dual_loss=4.3186e-01
Validation X2Y - loss=7.4285e-01 ppl=2.10 best_loss=7.0716e-01 best_ppl=2.03                                            
Validation Y2X - loss=7.6095e-01 ppl=2.14 best_loss=7.5851e-01 best_ppl=2.14
Epoch 72 - |param|=9.47e+02 |g_param|=3.61e+04 loss_x2y=4.1971e-01 ppl_x2y=1.52 loss_y2x=3.7729e-01 ppl_y2x=1.46 dual_loss=8.1002e-01
Validation X2Y - loss=7.7544e-01 ppl=2.17 best_loss=7.0716e-01 best_ppl=2.03                                            
Validation Y2X - loss=7.5702e-01 ppl=2.13 best_loss=7.5851e-01 best_ppl=2.14
Epoch 73 - |param|=9.48e+02 |g_param|=3.15e+04 loss_x2y=4.8171e-01 ppl_x2y=1.62 loss_y2x=3.8024e-01 ppl_y2x=1.46 dual_loss=6.5912e-01
Validation X2Y - loss=7.3993e-01 ppl=2.10 best_loss=7.0716e-01 best_ppl=2.03                                            
Validation Y2X - loss=7.6132e-01 ppl=2.14 best_loss=7.5702e-01 best_ppl=2.13
Epoch 74 - |param|=9.48e+02 |g_param|=2.30e+04 loss_x2y=3.9824e-01 ppl_x2y=1.49 loss_y2x=3.7975e-01 ppl_y2x=1.46 dual_loss=4.0306e-01
Validation X2Y - loss=6.9231e-01 ppl=2.00 best_loss=7.0716e-01 best_ppl=2.03                                            
Validation Y2X - loss=7.3877e-01 ppl=2.09 best_loss=7.5702e-01 best_ppl=2.13
Epoch 75 - |param|=9.49e+02 |g_param|=1.63e+04 loss_x2y=3.3387e-01 ppl_x2y=1.40 loss_y2x=3.6399e-01 ppl_y2x=1.44 dual_loss=3.8039e-01
Validation X2Y - loss=6.8600e-01 ppl=1.99 best_loss=6.9231e-01 best_ppl=2.00                                            
Validation Y2X - loss=7.4956e-01 ppl=2.12 best_loss=7.3877e-01 best_ppl=2.09
Epoch 76 - |param|=9.49e+02 |g_param|=2.03e+04 loss_x2y=3.2075e-01 ppl_x2y=1.38 loss_y2x=3.8767e-01 ppl_y2x=1.47 dual_loss=5.4124e-01
Validation X2Y - loss=6.8139e-01 ppl=1.98 best_loss=6.8600e-01 best_ppl=1.99                                            
Validation Y2X - loss=7.7639e-01 ppl=2.17 best_loss=7.3877e-01 best_ppl=2.09
Epoch 77 - |param|=9.50e+02 |g_param|=4.01e+04 loss_x2y=4.6507e-01 ppl_x2y=1.59 loss_y2x=8.1286e-01 ppl_y2x=2.25 dual_loss=3.6321e+00
Validation X2Y - loss=7.0009e-01 ppl=2.01 best_loss=6.8139e-01 best_ppl=1.98                                            
Validation Y2X - loss=7.9276e-01 ppl=2.21 best_loss=7.3877e-01 best_ppl=2.09
Epoch 78 - |param|=9.50e+02 |g_param|=2.34e+04 loss_x2y=3.4992e-01 ppl_x2y=1.42 loss_y2x=4.8133e-01 ppl_y2x=1.62 dual_loss=9.8237e-01
Validation X2Y - loss=7.1555e-01 ppl=2.05 best_loss=6.8139e-01 best_ppl=1.98                                            
Validation Y2X - loss=7.5547e-01 ppl=2.13 best_loss=7.3877e-01 best_ppl=2.09
Epoch 79 - |param|=9.51e+02 |g_param|=1.94e+04 loss_x2y=3.1954e-01 ppl_x2y=1.38 loss_y2x=4.3894e-01 ppl_y2x=1.55 dual_loss=7.7158e-01
Validation X2Y - loss=6.9519e-01 ppl=2.00 best_loss=6.8139e-01 best_ppl=1.98                                            
Validation Y2X - loss=7.3949e-01 ppl=2.09 best_loss=7.3877e-01 best_ppl=2.09
Epoch 80 - |param|=9.51e+02 |g_param|=1.71e+04 loss_x2y=2.9520e-01 ppl_x2y=1.34 loss_y2x=3.8720e-01 ppl_y2x=1.47 dual_loss=5.8116e-01
Validation X2Y - loss=6.9374e-01 ppl=2.00 best_loss=6.8139e-01 best_ppl=1.98                                            
Validation Y2X - loss=7.4378e-01 ppl=2.10 best_loss=7.3877e-01 best_ppl=2.09

real	33m27.653s
user	33m6.188s
sys	0m22.361s
```

#### Warmup-Epoch 20, Total Epoch 90

```
Epoch 1 - |param|=9.09e+02 |g_param|=2.68e+05 loss_x2y=4.4585e+00 ppl_x2y=86.36 loss_y2x=4.4819e+00 ppl_y2x=88.41 dual_loss=0.0000e+00
Validation X2Y - loss=4.0356e+00 ppl=56.58 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=4.0664e+00 ppl=58.34 best_loss=inf best_ppl=inf
Epoch 2 - |param|=9.09e+02 |g_param|=2.00e+05 loss_x2y=4.0878e+00 ppl_x2y=59.61 loss_y2x=4.1205e+00 ppl_y2x=61.59 dual_loss=0.0000e+00
Validation X2Y - loss=3.9342e+00 ppl=51.12 best_loss=4.0356e+00 best_ppl=56.58                                          
Validation Y2X - loss=3.9099e+00 ppl=49.89 best_loss=4.0664e+00 best_ppl=58.34
Epoch 3 - |param|=9.09e+02 |g_param|=1.99e+05 loss_x2y=4.0054e+00 ppl_x2y=54.90 loss_y2x=4.0167e+00 ppl_y2x=55.52 dual_loss=0.0000e+00
Validation X2Y - loss=3.8125e+00 ppl=45.26 best_loss=3.9342e+00 best_ppl=51.12                                          
Validation Y2X - loss=3.8215e+00 ppl=45.67 best_loss=3.9099e+00 best_ppl=49.89
Epoch 4 - |param|=9.09e+02 |g_param|=1.93e+05 loss_x2y=3.9390e+00 ppl_x2y=51.37 loss_y2x=3.9532e+00 ppl_y2x=52.10 dual_loss=0.0000e+00
Validation X2Y - loss=3.7282e+00 ppl=41.60 best_loss=3.8125e+00 best_ppl=45.26                                          
Validation Y2X - loss=3.7419e+00 ppl=42.18 best_loss=3.8215e+00 best_ppl=45.67
Epoch 5 - |param|=9.10e+02 |g_param|=1.94e+05 loss_x2y=3.8603e+00 ppl_x2y=47.48 loss_y2x=3.9089e+00 ppl_y2x=49.85 dual_loss=0.0000e+00
Validation X2Y - loss=3.5983e+00 ppl=36.54 best_loss=3.7282e+00 best_ppl=41.60                                          
Validation Y2X - loss=3.6476e+00 ppl=38.38 best_loss=3.7419e+00 best_ppl=42.18
Epoch 6 - |param|=9.10e+02 |g_param|=2.07e+05 loss_x2y=3.7444e+00 ppl_x2y=42.28 loss_y2x=3.7867e+00 ppl_y2x=44.11 dual_loss=0.0000e+00
Validation X2Y - loss=3.5091e+00 ppl=33.42 best_loss=3.5983e+00 best_ppl=36.54                                          
Validation Y2X - loss=3.5438e+00 ppl=34.60 best_loss=3.6476e+00 best_ppl=38.38
Epoch 7 - |param|=9.11e+02 |g_param|=1.98e+05 loss_x2y=3.5723e+00 ppl_x2y=35.60 loss_y2x=3.6328e+00 ppl_y2x=37.82 dual_loss=0.0000e+00
Validation X2Y - loss=3.3831e+00 ppl=29.46 best_loss=3.5091e+00 best_ppl=33.42                                          
Validation Y2X - loss=3.4487e+00 ppl=31.46 best_loss=3.5438e+00 best_ppl=34.60
Epoch 8 - |param|=9.12e+02 |g_param|=2.52e+05 loss_x2y=3.4339e+00 ppl_x2y=31.00 loss_y2x=3.5360e+00 ppl_y2x=34.33 dual_loss=0.0000e+00
Validation X2Y - loss=3.2279e+00 ppl=25.23 best_loss=3.3831e+00 best_ppl=29.46                                          
Validation Y2X - loss=3.3411e+00 ppl=28.25 best_loss=3.4487e+00 best_ppl=31.46
Epoch 9 - |param|=9.13e+02 |g_param|=2.57e+05 loss_x2y=3.1756e+00 ppl_x2y=23.94 loss_y2x=3.3263e+00 ppl_y2x=27.83 dual_loss=0.0000e+00
Validation X2Y - loss=2.9935e+00 ppl=19.96 best_loss=3.2279e+00 best_ppl=25.23                                          
Validation Y2X - loss=3.1605e+00 ppl=23.58 best_loss=3.3411e+00 best_ppl=28.25
Epoch 10 - |param|=9.14e+02 |g_param|=3.20e+05 loss_x2y=3.0767e+00 ppl_x2y=21.69 loss_y2x=3.2521e+00 ppl_y2x=25.85 dual_loss=0.0000e+00
Validation X2Y - loss=2.7793e+00 ppl=16.11 best_loss=2.9935e+00 best_ppl=19.96                                          
Validation Y2X - loss=2.9738e+00 ppl=19.57 best_loss=3.1605e+00 best_ppl=23.58
Epoch 11 - |param|=9.15e+02 |g_param|=3.23e+05 loss_x2y=2.7293e+00 ppl_x2y=15.32 loss_y2x=2.9059e+00 ppl_y2x=18.28 dual_loss=0.0000e+00
Validation X2Y - loss=2.6344e+00 ppl=13.94 best_loss=2.7793e+00 best_ppl=16.11                                          
Validation Y2X - loss=2.7633e+00 ppl=15.85 best_loss=2.9738e+00 best_ppl=19.57
Epoch 12 - |param|=9.16e+02 |g_param|=2.35e+05 loss_x2y=2.5542e+00 ppl_x2y=12.86 loss_y2x=2.6434e+00 ppl_y2x=14.06 dual_loss=0.0000e+00
Validation X2Y - loss=2.4432e+00 ppl=11.51 best_loss=2.6344e+00 best_ppl=13.94                                          
Validation Y2X - loss=2.4716e+00 ppl=11.84 best_loss=2.7633e+00 best_ppl=15.85
Epoch 13 - |param|=9.17e+02 |g_param|=2.08e+05 loss_x2y=2.3417e+00 ppl_x2y=10.40 loss_y2x=2.4463e+00 ppl_y2x=11.55 dual_loss=0.0000e+00
Validation X2Y - loss=2.3446e+00 ppl=10.43 best_loss=2.4432e+00 best_ppl=11.51                                          
Validation Y2X - loss=2.2968e+00 ppl=9.94 best_loss=2.4716e+00 best_ppl=11.84
Epoch 14 - |param|=9.18e+02 |g_param|=2.26e+05 loss_x2y=2.1649e+00 ppl_x2y=8.71 loss_y2x=2.2500e+00 ppl_y2x=9.49 dual_loss=0.0000e+00
Validation X2Y - loss=2.1245e+00 ppl=8.37 best_loss=2.3446e+00 best_ppl=10.43                                           
Validation Y2X - loss=2.1488e+00 ppl=8.57 best_loss=2.2968e+00 best_ppl=9.94
Epoch 15 - |param|=9.18e+02 |g_param|=2.23e+05 loss_x2y=1.9588e+00 ppl_x2y=7.09 loss_y2x=2.0437e+00 ppl_y2x=7.72 dual_loss=0.0000e+00
Validation X2Y - loss=1.9577e+00 ppl=7.08 best_loss=2.1245e+00 best_ppl=8.37                                            
Validation Y2X - loss=1.9306e+00 ppl=6.89 best_loss=2.1488e+00 best_ppl=8.57
Epoch 16 - |param|=9.19e+02 |g_param|=2.25e+05 loss_x2y=1.9315e+00 ppl_x2y=6.90 loss_y2x=1.9797e+00 ppl_y2x=7.24 dual_loss=0.0000e+00
Validation X2Y - loss=1.9283e+00 ppl=6.88 best_loss=1.9577e+00 best_ppl=7.08                                            
Validation Y2X - loss=1.8565e+00 ppl=6.40 best_loss=1.9306e+00 best_ppl=6.89
Epoch 17 - |param|=9.20e+02 |g_param|=1.59e+05 loss_x2y=1.7469e+00 ppl_x2y=5.74 loss_y2x=1.7945e+00 ppl_y2x=6.02 dual_loss=0.0000e+00
Validation X2Y - loss=1.7673e+00 ppl=5.86 best_loss=1.9283e+00 best_ppl=6.88                                            
Validation Y2X - loss=1.7156e+00 ppl=5.56 best_loss=1.8565e+00 best_ppl=6.40
Epoch 18 - |param|=9.21e+02 |g_param|=2.49e+05 loss_x2y=1.7662e+00 ppl_x2y=5.85 loss_y2x=1.8097e+00 ppl_y2x=6.11 dual_loss=0.0000e+00
Validation X2Y - loss=1.7264e+00 ppl=5.62 best_loss=1.7673e+00 best_ppl=5.86                                            
Validation Y2X - loss=1.7314e+00 ppl=5.65 best_loss=1.7156e+00 best_ppl=5.56
Epoch 19 - |param|=9.22e+02 |g_param|=2.06e+05 loss_x2y=1.5755e+00 ppl_x2y=4.83 loss_y2x=1.6257e+00 ppl_y2x=5.08 dual_loss=0.0000e+00
Validation X2Y - loss=1.6601e+00 ppl=5.26 best_loss=1.7264e+00 best_ppl=5.62                                            
Validation Y2X - loss=1.5970e+00 ppl=4.94 best_loss=1.7156e+00 best_ppl=5.56
Epoch 20 - |param|=9.23e+02 |g_param|=1.50e+05 loss_x2y=1.4620e+00 ppl_x2y=4.31 loss_y2x=1.5683e+00 ppl_y2x=4.80 dual_loss=0.0000e+00
Validation X2Y - loss=1.5507e+00 ppl=4.71 best_loss=1.6601e+00 best_ppl=5.26                                            
Validation Y2X - loss=1.4972e+00 ppl=4.47 best_loss=1.5970e+00 best_ppl=4.94
Epoch 21 - |param|=9.23e+02 |g_param|=1.53e+05 loss_x2y=1.4267e+00 ppl_x2y=4.16 loss_y2x=1.5836e+00 ppl_y2x=4.87 dual_loss=2.1550e+00
Validation X2Y - loss=1.4981e+00 ppl=4.47 best_loss=1.5507e+00 best_ppl=4.71                                            
Validation Y2X - loss=1.4748e+00 ppl=4.37 best_loss=1.4972e+00 best_ppl=4.47
Epoch 22 - |param|=9.24e+02 |g_param|=1.22e+05 loss_x2y=1.3594e+00 ppl_x2y=3.89 loss_y2x=1.4996e+00 ppl_y2x=4.48 dual_loss=1.6432e+00
Validation X2Y - loss=1.4401e+00 ppl=4.22 best_loss=1.4981e+00 best_ppl=4.47                                            
Validation Y2X - loss=1.3957e+00 ppl=4.04 best_loss=1.4748e+00 best_ppl=4.37
Epoch 23 - |param|=9.25e+02 |g_param|=9.14e+04 loss_x2y=1.2694e+00 ppl_x2y=3.56 loss_y2x=1.4403e+00 ppl_y2x=4.22 dual_loss=2.1832e+00
Validation X2Y - loss=1.4124e+00 ppl=4.11 best_loss=1.4401e+00 best_ppl=4.22                                            
Validation Y2X - loss=1.3770e+00 ppl=3.96 best_loss=1.3957e+00 best_ppl=4.04
Epoch 24 - |param|=9.25e+02 |g_param|=8.42e+04 loss_x2y=1.2780e+00 ppl_x2y=3.59 loss_y2x=1.5710e+00 ppl_y2x=4.81 dual_loss=2.7810e+00
Validation X2Y - loss=1.3893e+00 ppl=4.01 best_loss=1.4124e+00 best_ppl=4.11                                            
Validation Y2X - loss=1.4462e+00 ppl=4.25 best_loss=1.3770e+00 best_ppl=3.96
Epoch 25 - |param|=9.26e+02 |g_param|=9.96e+04 loss_x2y=1.2086e+00 ppl_x2y=3.35 loss_y2x=1.2507e+00 ppl_y2x=3.49 dual_loss=9.7214e-01
Validation X2Y - loss=1.3419e+00 ppl=3.83 best_loss=1.3893e+00 best_ppl=4.01                                            
Validation Y2X - loss=1.2796e+00 ppl=3.60 best_loss=1.3770e+00 best_ppl=3.96
Epoch 26 - |param|=9.27e+02 |g_param|=7.96e+04 loss_x2y=1.1998e+00 ppl_x2y=3.32 loss_y2x=1.1083e+00 ppl_y2x=3.03 dual_loss=7.7695e-01
Validation X2Y - loss=1.4338e+00 ppl=4.19 best_loss=1.3419e+00 best_ppl=3.83                                            
Validation Y2X - loss=1.2504e+00 ppl=3.49 best_loss=1.2796e+00 best_ppl=3.60
Epoch 27 - |param|=9.27e+02 |g_param|=6.15e+04 loss_x2y=1.1458e+00 ppl_x2y=3.14 loss_y2x=1.2195e+00 ppl_y2x=3.39 dual_loss=1.4101e+00
Validation X2Y - loss=1.2916e+00 ppl=3.64 best_loss=1.3419e+00 best_ppl=3.83                                            
Validation Y2X - loss=1.2965e+00 ppl=3.66 best_loss=1.2504e+00 best_ppl=3.49
Epoch 28 - |param|=9.28e+02 |g_param|=7.39e+04 loss_x2y=1.0850e+00 ppl_x2y=2.96 loss_y2x=1.2778e+00 ppl_y2x=3.59 dual_loss=2.5350e+00
Validation X2Y - loss=1.2337e+00 ppl=3.43 best_loss=1.2916e+00 best_ppl=3.64                                            
Validation Y2X - loss=1.4083e+00 ppl=4.09 best_loss=1.2504e+00 best_ppl=3.49
Epoch 29 - |param|=9.28e+02 |g_param|=6.33e+04 loss_x2y=1.0030e+00 ppl_x2y=2.73 loss_y2x=1.1131e+00 ppl_y2x=3.04 dual_loss=1.2696e+00
Validation X2Y - loss=1.1945e+00 ppl=3.30 best_loss=1.2337e+00 best_ppl=3.43                                            
Validation Y2X - loss=1.1117e+00 ppl=3.04 best_loss=1.2504e+00 best_ppl=3.49
Epoch 30 - |param|=9.29e+02 |g_param|=4.18e+04 loss_x2y=9.7346e-01 ppl_x2y=2.65 loss_y2x=1.0251e+00 ppl_y2x=2.79 dual_loss=1.0133e+00
Validation X2Y - loss=1.1621e+00 ppl=3.20 best_loss=1.1945e+00 best_ppl=3.30                                            
Validation Y2X - loss=1.1548e+00 ppl=3.17 best_loss=1.1117e+00 best_ppl=3.04
Epoch 31 - |param|=9.30e+02 |g_param|=6.11e+04 loss_x2y=9.6519e-01 ppl_x2y=2.63 loss_y2x=1.1747e+00 ppl_y2x=3.24 dual_loss=1.7573e+00
Validation X2Y - loss=1.1436e+00 ppl=3.14 best_loss=1.1621e+00 best_ppl=3.20                                            
Validation Y2X - loss=1.1131e+00 ppl=3.04 best_loss=1.1117e+00 best_ppl=3.04
Epoch 32 - |param|=9.30e+02 |g_param|=5.43e+04 loss_x2y=9.0566e-01 ppl_x2y=2.47 loss_y2x=9.5437e-01 ppl_y2x=2.60 dual_loss=9.3710e-01
Validation X2Y - loss=1.1952e+00 ppl=3.30 best_loss=1.1436e+00 best_ppl=3.14                                            
Validation Y2X - loss=1.0401e+00 ppl=2.83 best_loss=1.1117e+00 best_ppl=3.04
Epoch 33 - |param|=9.31e+02 |g_param|=5.75e+04 loss_x2y=1.2431e+00 ppl_x2y=3.47 loss_y2x=9.2435e-01 ppl_y2x=2.52 dual_loss=1.6099e+00
Validation X2Y - loss=1.2832e+00 ppl=3.61 best_loss=1.1436e+00 best_ppl=3.14                                            
Validation Y2X - loss=9.7545e-01 ppl=2.65 best_loss=1.0401e+00 best_ppl=2.83
Epoch 34 - |param|=9.31e+02 |g_param|=3.59e+04 loss_x2y=9.9217e-01 ppl_x2y=2.70 loss_y2x=7.9640e-01 ppl_y2x=2.22 dual_loss=8.2394e-01
Validation X2Y - loss=1.0999e+00 ppl=3.00 best_loss=1.1436e+00 best_ppl=3.14                                            
Validation Y2X - loss=9.7770e-01 ppl=2.66 best_loss=9.7545e-01 best_ppl=2.65
Epoch 35 - |param|=9.32e+02 |g_param|=4.38e+04 loss_x2y=8.2375e-01 ppl_x2y=2.28 loss_y2x=8.4914e-01 ppl_y2x=2.34 dual_loss=7.8384e-01
Validation X2Y - loss=1.0436e+00 ppl=2.84 best_loss=1.0999e+00 best_ppl=3.00                                            
Validation Y2X - loss=1.0202e+00 ppl=2.77 best_loss=9.7545e-01 best_ppl=2.65
Epoch 36 - |param|=9.32e+02 |g_param|=3.10e+04 loss_x2y=7.6185e-01 ppl_x2y=2.14 loss_y2x=7.9295e-01 ppl_y2x=2.21 dual_loss=7.1138e-01
Validation X2Y - loss=1.0176e+00 ppl=2.77 best_loss=1.0436e+00 best_ppl=2.84                                            
Validation Y2X - loss=9.8195e-01 ppl=2.67 best_loss=9.7545e-01 best_ppl=2.65
Epoch 37 - |param|=9.33e+02 |g_param|=5.28e+04 loss_x2y=8.3211e-01 ppl_x2y=2.30 loss_y2x=9.8109e-01 ppl_y2x=2.67 dual_loss=1.8433e+00
Validation X2Y - loss=1.0117e+00 ppl=2.75 best_loss=1.0176e+00 best_ppl=2.77                                            
Validation Y2X - loss=9.9327e-01 ppl=2.70 best_loss=9.7545e-01 best_ppl=2.65
Epoch 38 - |param|=9.33e+02 |g_param|=3.40e+04 loss_x2y=7.2361e-01 ppl_x2y=2.06 loss_y2x=8.0725e-01 ppl_y2x=2.24 dual_loss=9.1018e-01
Validation X2Y - loss=9.7483e-01 ppl=2.65 best_loss=1.0117e+00 best_ppl=2.75                                            
Validation Y2X - loss=9.7917e-01 ppl=2.66 best_loss=9.7545e-01 best_ppl=2.65
Epoch 39 - |param|=9.34e+02 |g_param|=4.21e+04 loss_x2y=7.0310e-01 ppl_x2y=2.02 loss_y2x=7.7759e-01 ppl_y2x=2.18 dual_loss=1.0811e+00
Validation X2Y - loss=9.7172e-01 ppl=2.64 best_loss=9.7483e-01 best_ppl=2.65                                            
Validation Y2X - loss=9.2386e-01 ppl=2.52 best_loss=9.7545e-01 best_ppl=2.65
Epoch 40 - |param|=9.34e+02 |g_param|=2.60e+04 loss_x2y=7.0146e-01 ppl_x2y=2.02 loss_y2x=7.0803e-01 ppl_y2x=2.03 dual_loss=6.4538e-01
Validation X2Y - loss=1.0521e+00 ppl=2.86 best_loss=9.7172e-01 best_ppl=2.64                                            
Validation Y2X - loss=8.8508e-01 ppl=2.42 best_loss=9.2386e-01 best_ppl=2.52
Epoch 41 - |param|=9.35e+02 |g_param|=3.29e+04 loss_x2y=7.7075e-01 ppl_x2y=2.16 loss_y2x=6.7861e-01 ppl_y2x=1.97 dual_loss=6.9994e-01
Validation X2Y - loss=9.9107e-01 ppl=2.69 best_loss=9.7172e-01 best_ppl=2.64                                            
Validation Y2X - loss=8.5338e-01 ppl=2.35 best_loss=8.8508e-01 best_ppl=2.42
Epoch 42 - |param|=9.35e+02 |g_param|=3.14e+04 loss_x2y=7.0164e-01 ppl_x2y=2.02 loss_y2x=6.4839e-01 ppl_y2x=1.91 dual_loss=4.9930e-01
Validation X2Y - loss=9.2458e-01 ppl=2.52 best_loss=9.7172e-01 best_ppl=2.64                                            
Validation Y2X - loss=8.6604e-01 ppl=2.38 best_loss=8.5338e-01 best_ppl=2.35
Epoch 43 - |param|=9.36e+02 |g_param|=2.31e+04 loss_x2y=6.3125e-01 ppl_x2y=1.88 loss_y2x=6.2071e-01 ppl_y2x=1.86 dual_loss=5.2141e-01
Validation X2Y - loss=9.0197e-01 ppl=2.46 best_loss=9.2458e-01 best_ppl=2.52                                            
Validation Y2X - loss=8.3860e-01 ppl=2.31 best_loss=8.5338e-01 best_ppl=2.35
Epoch 44 - |param|=9.36e+02 |g_param|=5.34e+04 loss_x2y=6.3288e-01 ppl_x2y=1.88 loss_y2x=7.0350e-01 ppl_y2x=2.02 dual_loss=1.3177e+00
Validation X2Y - loss=9.0303e-01 ppl=2.47 best_loss=9.0197e-01 best_ppl=2.46                                            
Validation Y2X - loss=8.5946e-01 ppl=2.36 best_loss=8.3860e-01 best_ppl=2.31
Epoch 45 - |param|=9.37e+02 |g_param|=2.43e+04 loss_x2y=5.6949e-01 ppl_x2y=1.77 loss_y2x=5.8388e-01 ppl_y2x=1.79 dual_loss=5.1745e-01
Validation X2Y - loss=8.9267e-01 ppl=2.44 best_loss=9.0197e-01 best_ppl=2.46                                            
Validation Y2X - loss=8.5645e-01 ppl=2.35 best_loss=8.3860e-01 best_ppl=2.31
Epoch 46 - |param|=9.37e+02 |g_param|=5.35e+04 loss_x2y=6.0745e-01 ppl_x2y=1.84 loss_y2x=7.7124e-01 ppl_y2x=2.16 dual_loss=1.7976e+00
Validation X2Y - loss=8.8531e-01 ppl=2.42 best_loss=8.9267e-01 best_ppl=2.44                                            
Validation Y2X - loss=9.6058e-01 ppl=2.61 best_loss=8.3860e-01 best_ppl=2.31
Epoch 47 - |param|=9.38e+02 |g_param|=3.56e+04 loss_x2y=6.6744e-01 ppl_x2y=1.95 loss_y2x=6.4723e-01 ppl_y2x=1.91 dual_loss=2.1679e+00
Validation X2Y - loss=1.0095e+00 ppl=2.74 best_loss=8.8531e-01 best_ppl=2.42                                            
Validation Y2X - loss=8.3358e-01 ppl=2.30 best_loss=8.3860e-01 best_ppl=2.31
Epoch 48 - |param|=9.38e+02 |g_param|=2.82e+04 loss_x2y=6.5420e-01 ppl_x2y=1.92 loss_y2x=5.9157e-01 ppl_y2x=1.81 dual_loss=9.3395e-01
Validation X2Y - loss=9.6006e-01 ppl=2.61 best_loss=8.8531e-01 best_ppl=2.42                                            
Validation Y2X - loss=8.0715e-01 ppl=2.24 best_loss=8.3358e-01 best_ppl=2.30
Epoch 49 - |param|=9.39e+02 |g_param|=3.17e+04 loss_x2y=5.7862e-01 ppl_x2y=1.78 loss_y2x=5.3342e-01 ppl_y2x=1.70 dual_loss=7.2941e-01
Validation X2Y - loss=8.9967e-01 ppl=2.46 best_loss=8.8531e-01 best_ppl=2.42                                            
Validation Y2X - loss=7.9694e-01 ppl=2.22 best_loss=8.0715e-01 best_ppl=2.24
Epoch 50 - |param|=9.39e+02 |g_param|=2.07e+04 loss_x2y=5.8255e-01 ppl_x2y=1.79 loss_y2x=5.0501e-01 ppl_y2x=1.66 dual_loss=4.1241e-01
Validation X2Y - loss=8.7566e-01 ppl=2.40 best_loss=8.8531e-01 best_ppl=2.42                                            
Validation Y2X - loss=7.8987e-01 ppl=2.20 best_loss=7.9694e-01 best_ppl=2.22
Epoch 51 - |param|=9.40e+02 |g_param|=2.12e+04 loss_x2y=5.4749e-01 ppl_x2y=1.73 loss_y2x=5.3224e-01 ppl_y2x=1.70 dual_loss=5.2048e-01
Validation X2Y - loss=8.4623e-01 ppl=2.33 best_loss=8.7566e-01 best_ppl=2.40                                            
Validation Y2X - loss=7.8349e-01 ppl=2.19 best_loss=7.8987e-01 best_ppl=2.20
Epoch 52 - |param|=9.40e+02 |g_param|=2.63e+04 loss_x2y=5.5235e-01 ppl_x2y=1.74 loss_y2x=4.9996e-01 ppl_y2x=1.65 dual_loss=4.6176e-01
Validation X2Y - loss=8.6535e-01 ppl=2.38 best_loss=8.4623e-01 best_ppl=2.33                                            
Validation Y2X - loss=7.8209e-01 ppl=2.19 best_loss=7.8349e-01 best_ppl=2.19
Epoch 53 - |param|=9.40e+02 |g_param|=3.92e+04 loss_x2y=5.5762e-01 ppl_x2y=1.75 loss_y2x=6.7303e-01 ppl_y2x=1.96 dual_loss=1.2556e+00
Validation X2Y - loss=8.1593e-01 ppl=2.26 best_loss=8.4623e-01 best_ppl=2.33                                            
Validation Y2X - loss=8.1451e-01 ppl=2.26 best_loss=7.8209e-01 best_ppl=2.19
Epoch 54 - |param|=9.41e+02 |g_param|=2.78e+04 loss_x2y=5.0361e-01 ppl_x2y=1.65 loss_y2x=5.5069e-01 ppl_y2x=1.73 dual_loss=6.3891e-01
Validation X2Y - loss=8.0646e-01 ppl=2.24 best_loss=8.1593e-01 best_ppl=2.26                                            
Validation Y2X - loss=7.9413e-01 ppl=2.21 best_loss=7.8209e-01 best_ppl=2.19
Epoch 55 - |param|=9.41e+02 |g_param|=2.57e+04 loss_x2y=4.8808e-01 ppl_x2y=1.63 loss_y2x=4.9435e-01 ppl_y2x=1.64 dual_loss=4.8306e-01
Validation X2Y - loss=8.0817e-01 ppl=2.24 best_loss=8.0646e-01 best_ppl=2.24                                            
Validation Y2X - loss=7.6923e-01 ppl=2.16 best_loss=7.8209e-01 best_ppl=2.19
Epoch 56 - |param|=9.42e+02 |g_param|=2.45e+04 loss_x2y=4.6974e-01 ppl_x2y=1.60 loss_y2x=4.6816e-01 ppl_y2x=1.60 dual_loss=4.6323e-01
Validation X2Y - loss=8.0928e-01 ppl=2.25 best_loss=8.0646e-01 best_ppl=2.24                                            
Validation Y2X - loss=7.7913e-01 ppl=2.18 best_loss=7.6923e-01 best_ppl=2.16
Epoch 57 - |param|=9.42e+02 |g_param|=2.72e+04 loss_x2y=4.5128e-01 ppl_x2y=1.57 loss_y2x=4.4481e-01 ppl_y2x=1.56 dual_loss=4.4187e-01
Validation X2Y - loss=8.0090e-01 ppl=2.23 best_loss=8.0646e-01 best_ppl=2.24                                            
Validation Y2X - loss=7.6570e-01 ppl=2.15 best_loss=7.6923e-01 best_ppl=2.16
Epoch 58 - |param|=9.43e+02 |g_param|=2.33e+04 loss_x2y=4.4033e-01 ppl_x2y=1.55 loss_y2x=4.3902e-01 ppl_y2x=1.55 dual_loss=3.5556e-01
Validation X2Y - loss=8.0288e-01 ppl=2.23 best_loss=8.0090e-01 best_ppl=2.23                                            
Validation Y2X - loss=7.5244e-01 ppl=2.12 best_loss=7.6570e-01 best_ppl=2.15
Epoch 59 - |param|=9.43e+02 |g_param|=2.10e+04 loss_x2y=4.3983e-01 ppl_x2y=1.55 loss_y2x=4.3724e-01 ppl_y2x=1.55 dual_loss=3.6052e-01
Validation X2Y - loss=7.9020e-01 ppl=2.20 best_loss=8.0090e-01 best_ppl=2.23                                            
Validation Y2X - loss=7.4439e-01 ppl=2.11 best_loss=7.5244e-01 best_ppl=2.12
Epoch 60 - |param|=9.43e+02 |g_param|=2.35e+04 loss_x2y=4.2590e-01 ppl_x2y=1.53 loss_y2x=4.1660e-01 ppl_y2x=1.52 dual_loss=3.5748e-01
Validation X2Y - loss=7.7926e-01 ppl=2.18 best_loss=7.9020e-01 best_ppl=2.20                                            
Validation Y2X - loss=7.4284e-01 ppl=2.10 best_loss=7.4439e-01 best_ppl=2.11
Epoch 61 - |param|=9.44e+02 |g_param|=2.32e+04 loss_x2y=4.1411e-01 ppl_x2y=1.51 loss_y2x=4.1373e-01 ppl_y2x=1.51 dual_loss=4.0423e-01
Validation X2Y - loss=7.8365e-01 ppl=2.19 best_loss=7.7926e-01 best_ppl=2.18                                            
Validation Y2X - loss=7.4397e-01 ppl=2.10 best_loss=7.4284e-01 best_ppl=2.10
Epoch 62 - |param|=9.44e+02 |g_param|=2.15e+04 loss_x2y=4.0147e-01 ppl_x2y=1.49 loss_y2x=4.0064e-01 ppl_y2x=1.49 dual_loss=3.4425e-01
Validation X2Y - loss=7.8410e-01 ppl=2.19 best_loss=7.7926e-01 best_ppl=2.18                                            
Validation Y2X - loss=7.4915e-01 ppl=2.12 best_loss=7.4284e-01 best_ppl=2.10
Epoch 63 - |param|=9.44e+02 |g_param|=2.53e+04 loss_x2y=4.0087e-01 ppl_x2y=1.49 loss_y2x=3.9611e-01 ppl_y2x=1.49 dual_loss=4.0095e-01
Validation X2Y - loss=7.7308e-01 ppl=2.17 best_loss=7.7926e-01 best_ppl=2.18                                            
Validation Y2X - loss=7.4282e-01 ppl=2.10 best_loss=7.4284e-01 best_ppl=2.10
Epoch 64 - |param|=9.45e+02 |g_param|=2.75e+04 loss_x2y=4.0080e-01 ppl_x2y=1.49 loss_y2x=4.1385e-01 ppl_y2x=1.51 dual_loss=5.5748e-01
Validation X2Y - loss=7.8442e-01 ppl=2.19 best_loss=7.7308e-01 best_ppl=2.17                                            
Validation Y2X - loss=8.2896e-01 ppl=2.29 best_loss=7.4282e-01 best_ppl=2.10
Epoch 65 - |param|=9.45e+02 |g_param|=4.60e+04 loss_x2y=5.1650e-01 ppl_x2y=1.68 loss_y2x=6.9739e-01 ppl_y2x=2.01 dual_loss=1.8479e+00
Validation X2Y - loss=7.8240e-01 ppl=2.19 best_loss=7.7308e-01 best_ppl=2.17                                            
Validation Y2X - loss=9.2441e-01 ppl=2.52 best_loss=7.4282e-01 best_ppl=2.10
Epoch 66 - |param|=9.46e+02 |g_param|=2.03e+04 loss_x2y=4.2647e-01 ppl_x2y=1.53 loss_y2x=4.8662e-01 ppl_y2x=1.63 dual_loss=7.0178e-01
Validation X2Y - loss=7.7577e-01 ppl=2.17 best_loss=7.7308e-01 best_ppl=2.17                                            
Validation Y2X - loss=7.4184e-01 ppl=2.10 best_loss=7.4282e-01 best_ppl=2.10
Epoch 67 - |param|=9.46e+02 |g_param|=2.32e+04 loss_x2y=4.0952e-01 ppl_x2y=1.51 loss_y2x=4.3641e-01 ppl_y2x=1.55 dual_loss=6.3735e-01
Validation X2Y - loss=8.2820e-01 ppl=2.29 best_loss=7.7308e-01 best_ppl=2.17                                            
Validation Y2X - loss=7.9462e-01 ppl=2.21 best_loss=7.4184e-01 best_ppl=2.10
Epoch 68 - |param|=9.47e+02 |g_param|=2.74e+04 loss_x2y=3.9658e-01 ppl_x2y=1.49 loss_y2x=4.2268e-01 ppl_y2x=1.53 dual_loss=5.6481e-01
Validation X2Y - loss=7.9458e-01 ppl=2.21 best_loss=7.7308e-01 best_ppl=2.17                                            
Validation Y2X - loss=8.5020e-01 ppl=2.34 best_loss=7.4184e-01 best_ppl=2.10
Epoch 69 - |param|=9.47e+02 |g_param|=2.35e+04 loss_x2y=3.9765e-01 ppl_x2y=1.49 loss_y2x=4.3947e-01 ppl_y2x=1.55 dual_loss=6.4901e-01
Validation X2Y - loss=7.5578e-01 ppl=2.13 best_loss=7.7308e-01 best_ppl=2.17                                            
Validation Y2X - loss=7.1609e-01 ppl=2.05 best_loss=7.4184e-01 best_ppl=2.10
Epoch 70 - |param|=9.48e+02 |g_param|=1.63e+04 loss_x2y=3.8418e-01 ppl_x2y=1.47 loss_y2x=3.9950e-01 ppl_y2x=1.49 dual_loss=3.6878e-01
Validation X2Y - loss=7.5481e-01 ppl=2.13 best_loss=7.5578e-01 best_ppl=2.13                                            
Validation Y2X - loss=6.9324e-01 ppl=2.00 best_loss=7.1609e-01 best_ppl=2.05
Epoch 71 - |param|=9.48e+02 |g_param|=1.74e+04 loss_x2y=3.8105e-01 ppl_x2y=1.46 loss_y2x=3.8469e-01 ppl_y2x=1.47 dual_loss=3.8600e-01
Validation X2Y - loss=7.6957e-01 ppl=2.16 best_loss=7.5481e-01 best_ppl=2.13                                            
Validation Y2X - loss=7.0392e-01 ppl=2.02 best_loss=6.9324e-01 best_ppl=2.00
Epoch 72 - |param|=9.48e+02 |g_param|=3.13e+04 loss_x2y=4.2404e-01 ppl_x2y=1.53 loss_y2x=3.9202e-01 ppl_y2x=1.48 dual_loss=4.0029e-01
Validation X2Y - loss=7.9161e-01 ppl=2.21 best_loss=7.5481e-01 best_ppl=2.13                                            
Validation Y2X - loss=7.0018e-01 ppl=2.01 best_loss=6.9324e-01 best_ppl=2.00
Epoch 73 - |param|=9.49e+02 |g_param|=9.35e+04 loss_x2y=1.1186e+00 ppl_x2y=3.06 loss_y2x=5.6522e-01 ppl_y2x=1.76 dual_loss=5.1476e+00
Validation X2Y - loss=9.8480e-01 ppl=2.68 best_loss=7.5481e-01 best_ppl=2.13                                            
Validation Y2X - loss=7.0495e-01 ppl=2.02 best_loss=6.9324e-01 best_ppl=2.00
Epoch 74 - |param|=9.50e+02 |g_param|=2.63e+04 loss_x2y=4.7397e-01 ppl_x2y=1.61 loss_y2x=3.5152e-01 ppl_y2x=1.42 dual_loss=4.9353e-01
Validation X2Y - loss=7.6078e-01 ppl=2.14 best_loss=7.5481e-01 best_ppl=2.13                                            
Validation Y2X - loss=6.9660e-01 ppl=2.01 best_loss=6.9324e-01 best_ppl=2.00
Epoch 75 - |param|=9.50e+02 |g_param|=1.59e+04 loss_x2y=3.8438e-01 ppl_x2y=1.47 loss_y2x=3.3469e-01 ppl_y2x=1.40 dual_loss=3.4724e-01
Validation X2Y - loss=7.3674e-01 ppl=2.09 best_loss=7.5481e-01 best_ppl=2.13                                            
Validation Y2X - loss=6.9112e-01 ppl=2.00 best_loss=6.9324e-01 best_ppl=2.00
Epoch 76 - |param|=9.50e+02 |g_param|=2.10e+04 loss_x2y=3.8146e-01 ppl_x2y=1.46 loss_y2x=3.5855e-01 ppl_y2x=1.43 dual_loss=4.6657e-01
Validation X2Y - loss=7.3901e-01 ppl=2.09 best_loss=7.3674e-01 best_ppl=2.09                                            
Validation Y2X - loss=7.0178e-01 ppl=2.02 best_loss=6.9112e-01 best_ppl=2.00
Epoch 77 - |param|=9.51e+02 |g_param|=1.50e+04 loss_x2y=3.5111e-01 ppl_x2y=1.42 loss_y2x=3.3247e-01 ppl_y2x=1.39 dual_loss=3.2922e-01
Validation X2Y - loss=7.4039e-01 ppl=2.10 best_loss=7.3674e-01 best_ppl=2.09                                            
Validation Y2X - loss=6.9889e-01 ppl=2.01 best_loss=6.9112e-01 best_ppl=2.00
Epoch 78 - |param|=9.51e+02 |g_param|=1.65e+04 loss_x2y=3.4317e-01 ppl_x2y=1.41 loss_y2x=3.2979e-01 ppl_y2x=1.39 dual_loss=3.3307e-01
Validation X2Y - loss=7.3831e-01 ppl=2.09 best_loss=7.3674e-01 best_ppl=2.09                                            
Validation Y2X - loss=7.1012e-01 ppl=2.03 best_loss=6.9112e-01 best_ppl=2.00
Epoch 79 - |param|=9.51e+02 |g_param|=2.15e+04 loss_x2y=3.3976e-01 ppl_x2y=1.40 loss_y2x=3.4708e-01 ppl_y2x=1.41 dual_loss=4.7793e-01
Validation X2Y - loss=7.3670e-01 ppl=2.09 best_loss=7.3674e-01 best_ppl=2.09                                            
Validation Y2X - loss=6.9220e-01 ppl=2.00 best_loss=6.9112e-01 best_ppl=2.00
Epoch 80 - |param|=9.52e+02 |g_param|=3.32e+04 loss_x2y=3.5344e-01 ppl_x2y=1.42 loss_y2x=3.9362e-01 ppl_y2x=1.48 dual_loss=7.0452e-01
Validation X2Y - loss=7.3353e-01 ppl=2.08 best_loss=7.3670e-01 best_ppl=2.09                                            
Validation Y2X - loss=7.2664e-01 ppl=2.07 best_loss=6.9112e-01 best_ppl=2.00
Epoch 81 - |param|=9.52e+02 |g_param|=2.35e+04 loss_x2y=3.4459e-01 ppl_x2y=1.41 loss_y2x=4.1236e-01 ppl_y2x=1.51 dual_loss=7.1423e-01
Validation X2Y - loss=7.3741e-01 ppl=2.09 best_loss=7.3353e-01 best_ppl=2.08                                            
Validation Y2X - loss=6.9832e-01 ppl=2.01 best_loss=6.9112e-01 best_ppl=2.00
Epoch 82 - |param|=9.52e+02 |g_param|=2.09e+04 loss_x2y=3.3464e-01 ppl_x2y=1.40 loss_y2x=3.6536e-01 ppl_y2x=1.44 dual_loss=5.5519e-01
Validation X2Y - loss=7.6745e-01 ppl=2.15 best_loss=7.3353e-01 best_ppl=2.08                                            
Validation Y2X - loss=6.7712e-01 ppl=1.97 best_loss=6.9112e-01 best_ppl=2.00
Epoch 83 - |param|=9.53e+02 |g_param|=1.46e+04 loss_x2y=3.2643e-01 ppl_x2y=1.39 loss_y2x=3.2899e-01 ppl_y2x=1.39 dual_loss=3.3556e-01
Validation X2Y - loss=7.2926e-01 ppl=2.07 best_loss=7.3353e-01 best_ppl=2.08                                            
Validation Y2X - loss=6.7812e-01 ppl=1.97 best_loss=6.7712e-01 best_ppl=1.97
Epoch 84 - |param|=9.53e+02 |g_param|=1.29e+04 loss_x2y=3.1495e-01 ppl_x2y=1.37 loss_y2x=3.1651e-01 ppl_y2x=1.37 dual_loss=3.2180e-01
Validation X2Y - loss=7.3862e-01 ppl=2.09 best_loss=7.2926e-01 best_ppl=2.07                                            
Validation Y2X - loss=6.8268e-01 ppl=1.98 best_loss=6.7712e-01 best_ppl=1.97
Epoch 85 - |param|=9.53e+02 |g_param|=1.45e+04 loss_x2y=3.0853e-01 ppl_x2y=1.36 loss_y2x=3.0394e-01 ppl_y2x=1.36 dual_loss=3.3750e-01
Validation X2Y - loss=7.3294e-01 ppl=2.08 best_loss=7.2926e-01 best_ppl=2.07                                            
Validation Y2X - loss=6.8837e-01 ppl=1.99 best_loss=6.7712e-01 best_ppl=1.97
Epoch 86 - |param|=9.54e+02 |g_param|=1.61e+04 loss_x2y=3.0956e-01 ppl_x2y=1.36 loss_y2x=3.1484e-01 ppl_y2x=1.37 dual_loss=3.4031e-01
Validation X2Y - loss=7.3889e-01 ppl=2.09 best_loss=7.2926e-01 best_ppl=2.07                                            
Validation Y2X - loss=6.9809e-01 ppl=2.01 best_loss=6.7712e-01 best_ppl=1.97
Epoch 87 - |param|=9.54e+02 |g_param|=2.43e+04 loss_x2y=2.9879e-01 ppl_x2y=1.35 loss_y2x=3.1529e-01 ppl_y2x=1.37 dual_loss=4.3374e-01
Validation X2Y - loss=7.3721e-01 ppl=2.09 best_loss=7.2926e-01 best_ppl=2.07                                            
Validation Y2X - loss=7.2231e-01 ppl=2.06 best_loss=6.7712e-01 best_ppl=1.97
Epoch 88 - |param|=9.55e+02 |g_param|=2.90e+04 loss_x2y=2.8991e-01 ppl_x2y=1.34 loss_y2x=3.0648e-01 ppl_y2x=1.36 dual_loss=3.7632e-01
Validation X2Y - loss=7.3241e-01 ppl=2.08 best_loss=7.2926e-01 best_ppl=2.07                                            
Validation Y2X - loss=7.0318e-01 ppl=2.02 best_loss=6.7712e-01 best_ppl=1.97
Epoch 89 - |param|=9.55e+02 |g_param|=2.73e+04 loss_x2y=2.9500e-01 ppl_x2y=1.34 loss_y2x=2.9447e-01 ppl_y2x=1.34 dual_loss=3.3118e-01
Validation X2Y - loss=7.2086e-01 ppl=2.06 best_loss=7.2926e-01 best_ppl=2.07                                            
Validation Y2X - loss=6.9159e-01 ppl=2.00 best_loss=6.7712e-01 best_ppl=1.97
Epoch 90 - |param|=9.55e+02 |g_param|=2.84e+04 loss_x2y=2.7791e-01 ppl_x2y=1.32 loss_y2x=2.7699e-01 ppl_y2x=1.32 dual_loss=3.2111e-01
Validation X2Y - loss=7.3617e-01 ppl=2.09 best_loss=7.2086e-01 best_ppl=2.06                                            
Validation Y2X - loss=7.1364e-01 ppl=2.04 best_loss=6.7712e-01 best_ppl=1.97

real	38m1.475s
user	37m37.993s
sys	0m24.177s
```

#### Warmup-Epoch 20, Total Epoch 100

```
Epoch 1 - |param|=9.08e+02 |g_param|=3.07e+05 loss_x2y=4.4611e+00 ppl_x2y=86.58 loss_y2x=4.4826e+00 ppl_y2x=88.46 dual_loss=0.0000e+00
Validation X2Y - loss=4.0492e+00 ppl=57.35 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=4.0956e+00 ppl=60.07 best_loss=inf best_ppl=inf
Epoch 2 - |param|=9.08e+02 |g_param|=2.46e+05 loss_x2y=4.0987e+00 ppl_x2y=60.26 loss_y2x=4.1335e+00 ppl_y2x=62.39 dual_loss=0.0000e+00
Validation X2Y - loss=3.8824e+00 ppl=48.54 best_loss=4.0492e+00 best_ppl=57.35                                          
Validation Y2X - loss=3.9028e+00 ppl=49.54 best_loss=4.0956e+00 best_ppl=60.07
Epoch 3 - |param|=9.09e+02 |g_param|=2.63e+05 loss_x2y=4.0326e+00 ppl_x2y=56.41 loss_y2x=4.0738e+00 ppl_y2x=58.78 dual_loss=0.0000e+00
Validation X2Y - loss=3.7995e+00 ppl=44.68 best_loss=3.8824e+00 best_ppl=48.54                                          
Validation Y2X - loss=3.8388e+00 ppl=46.47 best_loss=3.9028e+00 best_ppl=49.54
Epoch 4 - |param|=9.09e+02 |g_param|=2.68e+05 loss_x2y=3.9016e+00 ppl_x2y=49.48 loss_y2x=3.9607e+00 ppl_y2x=52.49 dual_loss=0.0000e+00
Validation X2Y - loss=3.6721e+00 ppl=39.33 best_loss=3.7995e+00 best_ppl=44.68                                          
Validation Y2X - loss=3.7381e+00 ppl=42.02 best_loss=3.8388e+00 best_ppl=46.47
Epoch 5 - |param|=9.09e+02 |g_param|=2.51e+05 loss_x2y=3.8274e+00 ppl_x2y=45.94 loss_y2x=3.9116e+00 ppl_y2x=49.98 dual_loss=0.0000e+00
Validation X2Y - loss=3.5743e+00 ppl=35.67 best_loss=3.6721e+00 best_ppl=39.33                                          
Validation Y2X - loss=3.6624e+00 ppl=38.96 best_loss=3.7381e+00 best_ppl=42.02
Epoch 6 - |param|=9.10e+02 |g_param|=2.48e+05 loss_x2y=3.6616e+00 ppl_x2y=38.93 loss_y2x=3.7706e+00 ppl_y2x=43.40 dual_loss=0.0000e+00
Validation X2Y - loss=3.4801e+00 ppl=32.46 best_loss=3.5743e+00 best_ppl=35.67                                          
Validation Y2X - loss=3.5823e+00 ppl=35.96 best_loss=3.6624e+00 best_ppl=38.96
Epoch 7 - |param|=9.10e+02 |g_param|=2.75e+05 loss_x2y=3.6411e+00 ppl_x2y=38.13 loss_y2x=3.7591e+00 ppl_y2x=42.91 dual_loss=0.0000e+00
Validation X2Y - loss=3.3823e+00 ppl=29.44 best_loss=3.4801e+00 best_ppl=32.46                                          
Validation Y2X - loss=3.5095e+00 ppl=33.43 best_loss=3.5823e+00 best_ppl=35.96
Epoch 8 - |param|=9.11e+02 |g_param|=3.02e+05 loss_x2y=3.5249e+00 ppl_x2y=33.95 loss_y2x=3.6722e+00 ppl_y2x=39.34 dual_loss=0.0000e+00
Validation X2Y - loss=3.2735e+00 ppl=26.40 best_loss=3.3823e+00 best_ppl=29.44                                          
Validation Y2X - loss=3.4016e+00 ppl=30.01 best_loss=3.5095e+00 best_ppl=33.43
Epoch 9 - |param|=9.12e+02 |g_param|=3.59e+05 loss_x2y=3.3189e+00 ppl_x2y=27.63 loss_y2x=3.4842e+00 ppl_y2x=32.60 dual_loss=0.0000e+00
Validation X2Y - loss=3.1414e+00 ppl=23.14 best_loss=3.2735e+00 best_ppl=26.40                                          
Validation Y2X - loss=3.2389e+00 ppl=25.50 best_loss=3.4016e+00 best_ppl=30.01
Epoch 10 - |param|=9.13e+02 |g_param|=4.42e+05 loss_x2y=3.2540e+00 ppl_x2y=25.89 loss_y2x=3.3873e+00 ppl_y2x=29.59 dual_loss=0.0000e+00
Validation X2Y - loss=2.9528e+00 ppl=19.16 best_loss=3.1414e+00 best_ppl=23.14                                          
Validation Y2X - loss=3.0694e+00 ppl=21.53 best_loss=3.2389e+00 best_ppl=25.50
Epoch 11 - |param|=9.14e+02 |g_param|=4.37e+05 loss_x2y=2.9443e+00 ppl_x2y=19.00 loss_y2x=3.1615e+00 ppl_y2x=23.61 dual_loss=0.0000e+00
Validation X2Y - loss=2.7236e+00 ppl=15.24 best_loss=2.9528e+00 best_ppl=19.16                                          
Validation Y2X - loss=2.9105e+00 ppl=18.37 best_loss=3.0694e+00 best_ppl=21.53
Epoch 12 - |param|=9.15e+02 |g_param|=2.56e+05 loss_x2y=2.6595e+00 ppl_x2y=14.29 loss_y2x=2.8796e+00 ppl_y2x=17.81 dual_loss=0.0000e+00
Validation X2Y - loss=2.4979e+00 ppl=12.16 best_loss=2.7236e+00 best_ppl=15.24                                          
Validation Y2X - loss=2.6819e+00 ppl=14.61 best_loss=2.9105e+00 best_ppl=18.37
Epoch 13 - |param|=9.16e+02 |g_param|=2.03e+05 loss_x2y=2.5186e+00 ppl_x2y=12.41 loss_y2x=2.7048e+00 ppl_y2x=14.95 dual_loss=0.0000e+00
Validation X2Y - loss=2.3346e+00 ppl=10.33 best_loss=2.4979e+00 best_ppl=12.16                                          
Validation Y2X - loss=2.5089e+00 ppl=12.29 best_loss=2.6819e+00 best_ppl=14.61
Epoch 14 - |param|=9.17e+02 |g_param|=2.48e+05 loss_x2y=2.2957e+00 ppl_x2y=9.93 loss_y2x=2.5349e+00 ppl_y2x=12.61 dual_loss=0.0000e+00
Validation X2Y - loss=2.1761e+00 ppl=8.81 best_loss=2.3346e+00 best_ppl=10.33                                           
Validation Y2X - loss=2.4025e+00 ppl=11.05 best_loss=2.5089e+00 best_ppl=12.29
Epoch 15 - |param|=9.18e+02 |g_param|=1.96e+05 loss_x2y=2.1132e+00 ppl_x2y=8.27 loss_y2x=2.2938e+00 ppl_y2x=9.91 dual_loss=0.0000e+00
Validation X2Y - loss=2.0189e+00 ppl=7.53 best_loss=2.1761e+00 best_ppl=8.81                                            
Validation Y2X - loss=2.1823e+00 ppl=8.87 best_loss=2.4025e+00 best_ppl=11.05
Epoch 16 - |param|=9.19e+02 |g_param|=2.48e+05 loss_x2y=2.0112e+00 ppl_x2y=7.47 loss_y2x=2.2098e+00 ppl_y2x=9.11 dual_loss=0.0000e+00
Validation X2Y - loss=1.9219e+00 ppl=6.83 best_loss=2.0189e+00 best_ppl=7.53                                            
Validation Y2X - loss=2.0456e+00 ppl=7.73 best_loss=2.1823e+00 best_ppl=8.87
Epoch 17 - |param|=9.20e+02 |g_param|=2.29e+05 loss_x2y=1.8749e+00 ppl_x2y=6.52 loss_y2x=1.9889e+00 ppl_y2x=7.31 dual_loss=0.0000e+00
Validation X2Y - loss=1.8149e+00 ppl=6.14 best_loss=1.9219e+00 best_ppl=6.83                                            
Validation Y2X - loss=1.8774e+00 ppl=6.54 best_loss=2.0456e+00 best_ppl=7.73
Epoch 18 - |param|=9.21e+02 |g_param|=2.29e+05 loss_x2y=1.7461e+00 ppl_x2y=5.73 loss_y2x=1.8410e+00 ppl_y2x=6.30 dual_loss=0.0000e+00
Validation X2Y - loss=1.6898e+00 ppl=5.42 best_loss=1.8149e+00 best_ppl=6.14                                            
Validation Y2X - loss=1.7408e+00 ppl=5.70 best_loss=1.8774e+00 best_ppl=6.54
Epoch 19 - |param|=9.22e+02 |g_param|=2.01e+05 loss_x2y=1.5873e+00 ppl_x2y=4.89 loss_y2x=1.6929e+00 ppl_y2x=5.44 dual_loss=0.0000e+00
Validation X2Y - loss=1.6207e+00 ppl=5.06 best_loss=1.6898e+00 best_ppl=5.42                                            
Validation Y2X - loss=1.6606e+00 ppl=5.26 best_loss=1.7408e+00 best_ppl=5.70
Epoch 20 - |param|=9.22e+02 |g_param|=2.08e+05 loss_x2y=1.5574e+00 ppl_x2y=4.75 loss_y2x=1.5849e+00 ppl_y2x=4.88 dual_loss=0.0000e+00
Validation X2Y - loss=1.6134e+00 ppl=5.02 best_loss=1.6207e+00 best_ppl=5.06                                            
Validation Y2X - loss=1.6343e+00 ppl=5.13 best_loss=1.6606e+00 best_ppl=5.26
Epoch 21 - |param|=9.23e+02 |g_param|=1.17e+05 loss_x2y=1.4561e+00 ppl_x2y=4.29 loss_y2x=1.5216e+00 ppl_y2x=4.58 dual_loss=1.2831e+00
Validation X2Y - loss=1.4473e+00 ppl=4.25 best_loss=1.6134e+00 best_ppl=5.02                                            
Validation Y2X - loss=1.8315e+00 ppl=6.24 best_loss=1.6343e+00 best_ppl=5.13
Epoch 22 - |param|=9.24e+02 |g_param|=1.45e+05 loss_x2y=1.3957e+00 ppl_x2y=4.04 loss_y2x=1.7141e+00 ppl_y2x=5.55 dual_loss=2.7043e+00
Validation X2Y - loss=1.4132e+00 ppl=4.11 best_loss=1.4473e+00 best_ppl=4.25                                            
Validation Y2X - loss=1.6206e+00 ppl=5.06 best_loss=1.6343e+00 best_ppl=5.13
Epoch 23 - |param|=9.25e+02 |g_param|=1.49e+05 loss_x2y=1.3033e+00 ppl_x2y=3.68 loss_y2x=1.2797e+00 ppl_y2x=3.60 dual_loss=7.1889e-01
Validation X2Y - loss=1.3599e+00 ppl=3.90 best_loss=1.4132e+00 best_ppl=4.11                                            
Validation Y2X - loss=1.3318e+00 ppl=3.79 best_loss=1.6206e+00 best_ppl=5.06
Epoch 24 - |param|=9.25e+02 |g_param|=1.71e+05 loss_x2y=1.3462e+00 ppl_x2y=3.84 loss_y2x=1.2566e+00 ppl_y2x=3.51 dual_loss=7.9049e-01
Validation X2Y - loss=1.3348e+00 ppl=3.80 best_loss=1.3599e+00 best_ppl=3.90                                            
Validation Y2X - loss=1.2625e+00 ppl=3.53 best_loss=1.3318e+00 best_ppl=3.79
Epoch 25 - |param|=9.26e+02 |g_param|=9.80e+04 loss_x2y=1.1438e+00 ppl_x2y=3.14 loss_y2x=1.1265e+00 ppl_y2x=3.08 dual_loss=6.5920e-01
Validation X2Y - loss=1.2163e+00 ppl=3.37 best_loss=1.3348e+00 best_ppl=3.80                                            
Validation Y2X - loss=1.2380e+00 ppl=3.45 best_loss=1.2625e+00 best_ppl=3.53
Epoch 26 - |param|=9.27e+02 |g_param|=1.04e+05 loss_x2y=1.1078e+00 ppl_x2y=3.03 loss_y2x=1.1094e+00 ppl_y2x=3.03 dual_loss=7.2930e-01
Validation X2Y - loss=1.1789e+00 ppl=3.25 best_loss=1.2163e+00 best_ppl=3.37                                            
Validation Y2X - loss=1.1557e+00 ppl=3.18 best_loss=1.2380e+00 best_ppl=3.45
Epoch 27 - |param|=9.27e+02 |g_param|=6.85e+04 loss_x2y=1.0821e+00 ppl_x2y=2.95 loss_y2x=1.0510e+00 ppl_y2x=2.86 dual_loss=6.1091e-01
Validation X2Y - loss=1.1527e+00 ppl=3.17 best_loss=1.1789e+00 best_ppl=3.25                                            
Validation Y2X - loss=1.1309e+00 ppl=3.10 best_loss=1.1557e+00 best_ppl=3.18
Epoch 28 - |param|=9.28e+02 |g_param|=6.76e+04 loss_x2y=9.6366e-01 ppl_x2y=2.62 loss_y2x=9.6693e-01 ppl_y2x=2.63 dual_loss=6.1012e-01
Validation X2Y - loss=1.1150e+00 ppl=3.05 best_loss=1.1527e+00 best_ppl=3.17                                            
Validation Y2X - loss=1.0688e+00 ppl=2.91 best_loss=1.1309e+00 best_ppl=3.10
Epoch 29 - |param|=9.28e+02 |g_param|=9.65e+04 loss_x2y=1.0562e+00 ppl_x2y=2.88 loss_y2x=1.0440e+00 ppl_y2x=2.84 dual_loss=1.0807e+00
Validation X2Y - loss=1.1029e+00 ppl=3.01 best_loss=1.1150e+00 best_ppl=3.05                                            
Validation Y2X - loss=1.1452e+00 ppl=3.14 best_loss=1.0688e+00 best_ppl=2.91
Epoch 30 - |param|=9.29e+02 |g_param|=1.93e+05 loss_x2y=1.3656e+00 ppl_x2y=3.92 loss_y2x=9.7523e-01 ppl_y2x=2.65 dual_loss=3.1373e+00
Validation X2Y - loss=1.5930e+00 ppl=4.92 best_loss=1.1029e+00 best_ppl=3.01                                            
Validation Y2X - loss=1.0105e+00 ppl=2.75 best_loss=1.0688e+00 best_ppl=2.91
Epoch 31 - |param|=9.30e+02 |g_param|=3.42e+04 loss_x2y=9.6982e-01 ppl_x2y=2.64 loss_y2x=8.7178e-01 ppl_y2x=2.39 dual_loss=6.8696e-01
Validation X2Y - loss=1.0448e+00 ppl=2.84 best_loss=1.1029e+00 best_ppl=3.01                                            
Validation Y2X - loss=9.8966e-01 ppl=2.69 best_loss=1.0105e+00 best_ppl=2.75
Epoch 32 - |param|=9.30e+02 |g_param|=4.07e+04 loss_x2y=8.3841e-01 ppl_x2y=2.31 loss_y2x=8.9085e-01 ppl_y2x=2.44 dual_loss=9.4826e-01
Validation X2Y - loss=1.0077e+00 ppl=2.74 best_loss=1.0448e+00 best_ppl=2.84                                            
Validation Y2X - loss=1.0695e+00 ppl=2.91 best_loss=9.8966e-01 best_ppl=2.69
Epoch 33 - |param|=9.31e+02 |g_param|=2.60e+04 loss_x2y=7.9099e-01 ppl_x2y=2.21 loss_y2x=7.8779e-01 ppl_y2x=2.20 dual_loss=5.4357e-01
Validation X2Y - loss=9.8032e-01 ppl=2.67 best_loss=1.0077e+00 best_ppl=2.74                                            
Validation Y2X - loss=9.4790e-01 ppl=2.58 best_loss=9.8966e-01 best_ppl=2.69
Epoch 34 - |param|=9.31e+02 |g_param|=3.54e+04 loss_x2y=8.0196e-01 ppl_x2y=2.23 loss_y2x=8.1586e-01 ppl_y2x=2.26 dual_loss=6.6231e-01
Validation X2Y - loss=9.5349e-01 ppl=2.59 best_loss=9.8032e-01 best_ppl=2.67                                            
Validation Y2X - loss=9.1031e-01 ppl=2.49 best_loss=9.4790e-01 best_ppl=2.58
Epoch 35 - |param|=9.32e+02 |g_param|=3.26e+04 loss_x2y=7.5326e-01 ppl_x2y=2.12 loss_y2x=7.9642e-01 ppl_y2x=2.22 dual_loss=7.4157e-01
Validation X2Y - loss=9.3514e-01 ppl=2.55 best_loss=9.5349e-01 best_ppl=2.59                                            
Validation Y2X - loss=9.4080e-01 ppl=2.56 best_loss=9.1031e-01 best_ppl=2.49
Epoch 36 - |param|=9.32e+02 |g_param|=4.07e+04 loss_x2y=7.4288e-01 ppl_x2y=2.10 loss_y2x=8.6737e-01 ppl_y2x=2.38 dual_loss=1.3411e+00
Validation X2Y - loss=9.1058e-01 ppl=2.49 best_loss=9.3514e-01 best_ppl=2.55                                            
Validation Y2X - loss=9.2943e-01 ppl=2.53 best_loss=9.1031e-01 best_ppl=2.49
Epoch 37 - |param|=9.33e+02 |g_param|=2.72e+04 loss_x2y=7.2886e-01 ppl_x2y=2.07 loss_y2x=7.3749e-01 ppl_y2x=2.09 dual_loss=5.2177e-01
Validation X2Y - loss=9.0891e-01 ppl=2.48 best_loss=9.1058e-01 best_ppl=2.49                                            
Validation Y2X - loss=8.4572e-01 ppl=2.33 best_loss=9.1031e-01 best_ppl=2.49
Epoch 38 - |param|=9.33e+02 |g_param|=2.06e+04 loss_x2y=6.2539e-01 ppl_x2y=1.87 loss_y2x=6.2115e-01 ppl_y2x=1.86 dual_loss=3.5571e-01
Validation X2Y - loss=8.9466e-01 ppl=2.45 best_loss=9.0891e-01 best_ppl=2.48                                            
Validation Y2X - loss=8.4871e-01 ppl=2.34 best_loss=8.4572e-01 best_ppl=2.33
Epoch 39 - |param|=9.34e+02 |g_param|=3.27e+04 loss_x2y=6.9598e-01 ppl_x2y=2.01 loss_y2x=6.5314e-01 ppl_y2x=1.92 dual_loss=4.6608e-01
Validation X2Y - loss=9.1241e-01 ppl=2.49 best_loss=8.9466e-01 best_ppl=2.45                                            
Validation Y2X - loss=8.2350e-01 ppl=2.28 best_loss=8.4572e-01 best_ppl=2.33
Epoch 40 - |param|=9.34e+02 |g_param|=2.98e+04 loss_x2y=6.1155e-01 ppl_x2y=1.84 loss_y2x=5.9716e-01 ppl_y2x=1.82 dual_loss=5.2802e-01
Validation X2Y - loss=8.9095e-01 ppl=2.44 best_loss=8.9466e-01 best_ppl=2.45                                            
Validation Y2X - loss=9.1297e-01 ppl=2.49 best_loss=8.2350e-01 best_ppl=2.28
Epoch 41 - |param|=9.35e+02 |g_param|=3.53e+04 loss_x2y=6.3233e-01 ppl_x2y=1.88 loss_y2x=6.6195e-01 ppl_y2x=1.94 dual_loss=7.6797e-01
Validation X2Y - loss=8.7613e-01 ppl=2.40 best_loss=8.9095e-01 best_ppl=2.44                                            
Validation Y2X - loss=8.7638e-01 ppl=2.40 best_loss=8.2350e-01 best_ppl=2.28
Epoch 42 - |param|=9.35e+02 |g_param|=2.40e+04 loss_x2y=5.8791e-01 ppl_x2y=1.80 loss_y2x=6.1315e-01 ppl_y2x=1.85 dual_loss=5.4345e-01
Validation X2Y - loss=8.6170e-01 ppl=2.37 best_loss=8.7613e-01 best_ppl=2.40                                            
Validation Y2X - loss=8.1693e-01 ppl=2.26 best_loss=8.2350e-01 best_ppl=2.28
Epoch 43 - |param|=9.36e+02 |g_param|=7.33e+04 loss_x2y=8.6505e-01 ppl_x2y=2.38 loss_y2x=6.3972e-01 ppl_y2x=1.90 dual_loss=1.6814e+00
Validation X2Y - loss=1.0468e+00 ppl=2.85 best_loss=8.6170e-01 best_ppl=2.37                                            
Validation Y2X - loss=8.0603e-01 ppl=2.24 best_loss=8.1693e-01 best_ppl=2.26
Epoch 44 - |param|=9.36e+02 |g_param|=8.21e+04 loss_x2y=1.1394e+00 ppl_x2y=3.13 loss_y2x=7.5832e-01 ppl_y2x=2.13 dual_loss=3.2479e+00
Validation X2Y - loss=1.0183e+00 ppl=2.77 best_loss=8.6170e-01 best_ppl=2.37                                            
Validation Y2X - loss=8.9021e-01 ppl=2.44 best_loss=8.0603e-01 best_ppl=2.24
Epoch 45 - |param|=9.37e+02 |g_param|=4.27e+04 loss_x2y=7.1619e-01 ppl_x2y=2.05 loss_y2x=8.0103e-01 ppl_y2x=2.23 dual_loss=1.8221e+00
Validation X2Y - loss=8.3322e-01 ppl=2.30 best_loss=8.6170e-01 best_ppl=2.37                                            
Validation Y2X - loss=8.6283e-01 ppl=2.37 best_loss=8.0603e-01 best_ppl=2.24
Epoch 46 - |param|=9.37e+02 |g_param|=3.02e+04 loss_x2y=5.9837e-01 ppl_x2y=1.82 loss_y2x=6.5948e-01 ppl_y2x=1.93 dual_loss=1.2261e+00
Validation X2Y - loss=8.2640e-01 ppl=2.29 best_loss=8.3322e-01 best_ppl=2.30                                            
Validation Y2X - loss=8.6231e-01 ppl=2.37 best_loss=8.0603e-01 best_ppl=2.24
Epoch 47 - |param|=9.38e+02 |g_param|=1.65e+04 loss_x2y=5.5455e-01 ppl_x2y=1.74 loss_y2x=5.6946e-01 ppl_y2x=1.77 dual_loss=5.6147e-01
Validation X2Y - loss=8.1713e-01 ppl=2.26 best_loss=8.2640e-01 best_ppl=2.29                                            
Validation Y2X - loss=7.8324e-01 ppl=2.19 best_loss=8.0603e-01 best_ppl=2.24
Epoch 48 - |param|=9.38e+02 |g_param|=3.77e+04 loss_x2y=6.3092e-01 ppl_x2y=1.88 loss_y2x=8.6400e-01 ppl_y2x=2.37 dual_loss=2.3210e+00
Validation X2Y - loss=8.0564e-01 ppl=2.24 best_loss=8.1713e-01 best_ppl=2.26                                            
Validation Y2X - loss=9.2241e-01 ppl=2.52 best_loss=7.8324e-01 best_ppl=2.19
Epoch 49 - |param|=9.39e+02 |g_param|=1.76e+04 loss_x2y=5.0451e-01 ppl_x2y=1.66 loss_y2x=5.7335e-01 ppl_y2x=1.77 dual_loss=6.7260e-01
Validation X2Y - loss=8.0007e-01 ppl=2.23 best_loss=8.0564e-01 best_ppl=2.24                                            
Validation Y2X - loss=7.9001e-01 ppl=2.20 best_loss=7.8324e-01 best_ppl=2.19
Epoch 50 - |param|=9.39e+02 |g_param|=1.64e+04 loss_x2y=5.0482e-01 ppl_x2y=1.66 loss_y2x=5.3381e-01 ppl_y2x=1.71 dual_loss=5.0014e-01
Validation X2Y - loss=7.9107e-01 ppl=2.21 best_loss=8.0007e-01 best_ppl=2.23                                            
Validation Y2X - loss=7.3744e-01 ppl=2.09 best_loss=7.8324e-01 best_ppl=2.19
Epoch 51 - |param|=9.39e+02 |g_param|=2.36e+04 loss_x2y=5.0875e-01 ppl_x2y=1.66 loss_y2x=5.3065e-01 ppl_y2x=1.70 dual_loss=4.8227e-01
Validation X2Y - loss=7.8076e-01 ppl=2.18 best_loss=7.9107e-01 best_ppl=2.21                                            
Validation Y2X - loss=7.3887e-01 ppl=2.09 best_loss=7.3744e-01 best_ppl=2.09
Epoch 52 - |param|=9.40e+02 |g_param|=2.40e+04 loss_x2y=4.8272e-01 ppl_x2y=1.62 loss_y2x=4.8762e-01 ppl_y2x=1.63 dual_loss=4.0987e-01
Validation X2Y - loss=7.8466e-01 ppl=2.19 best_loss=7.8076e-01 best_ppl=2.18                                            
Validation Y2X - loss=7.3276e-01 ppl=2.08 best_loss=7.3744e-01 best_ppl=2.09
Epoch 53 - |param|=9.40e+02 |g_param|=2.13e+04 loss_x2y=4.5280e-01 ppl_x2y=1.57 loss_y2x=4.4987e-01 ppl_y2x=1.57 dual_loss=3.5998e-01
Validation X2Y - loss=7.7277e-01 ppl=2.17 best_loss=7.8076e-01 best_ppl=2.18                                            
Validation Y2X - loss=7.2765e-01 ppl=2.07 best_loss=7.3276e-01 best_ppl=2.08
Epoch 54 - |param|=9.41e+02 |g_param|=2.46e+04 loss_x2y=4.6130e-01 ppl_x2y=1.59 loss_y2x=4.7341e-01 ppl_y2x=1.61 dual_loss=4.4338e-01
Validation X2Y - loss=7.7209e-01 ppl=2.16 best_loss=7.7277e-01 best_ppl=2.17                                            
Validation Y2X - loss=7.1542e-01 ppl=2.05 best_loss=7.2765e-01 best_ppl=2.07
Epoch 55 - |param|=9.41e+02 |g_param|=2.25e+04 loss_x2y=4.6646e-01 ppl_x2y=1.59 loss_y2x=4.7365e-01 ppl_y2x=1.61 dual_loss=3.9908e-01
Validation X2Y - loss=7.7936e-01 ppl=2.18 best_loss=7.7209e-01 best_ppl=2.16                                            
Validation Y2X - loss=7.1894e-01 ppl=2.05 best_loss=7.1542e-01 best_ppl=2.05
Epoch 56 - |param|=9.41e+02 |g_param|=2.21e+04 loss_x2y=4.3727e-01 ppl_x2y=1.55 loss_y2x=4.5123e-01 ppl_y2x=1.57 dual_loss=3.9114e-01
Validation X2Y - loss=7.7374e-01 ppl=2.17 best_loss=7.7209e-01 best_ppl=2.16                                            
Validation Y2X - loss=7.0177e-01 ppl=2.02 best_loss=7.1542e-01 best_ppl=2.05
Epoch 57 - |param|=9.42e+02 |g_param|=2.37e+04 loss_x2y=4.2083e-01 ppl_x2y=1.52 loss_y2x=4.2532e-01 ppl_y2x=1.53 dual_loss=3.6642e-01
Validation X2Y - loss=7.6291e-01 ppl=2.14 best_loss=7.7209e-01 best_ppl=2.16                                            
Validation Y2X - loss=7.0998e-01 ppl=2.03 best_loss=7.0177e-01 best_ppl=2.02
Epoch 58 - |param|=9.42e+02 |g_param|=2.38e+04 loss_x2y=4.2085e-01 ppl_x2y=1.52 loss_y2x=4.2407e-01 ppl_y2x=1.53 dual_loss=3.5541e-01
Validation X2Y - loss=7.5508e-01 ppl=2.13 best_loss=7.6291e-01 best_ppl=2.14                                            
Validation Y2X - loss=7.0193e-01 ppl=2.02 best_loss=7.0177e-01 best_ppl=2.02
Epoch 59 - |param|=9.42e+02 |g_param|=2.34e+04 loss_x2y=4.1821e-01 ppl_x2y=1.52 loss_y2x=4.2155e-01 ppl_y2x=1.52 dual_loss=4.1595e-01
Validation X2Y - loss=7.5977e-01 ppl=2.14 best_loss=7.5508e-01 best_ppl=2.13                                            
Validation Y2X - loss=6.9794e-01 ppl=2.01 best_loss=7.0177e-01 best_ppl=2.02
Epoch 60 - |param|=9.43e+02 |g_param|=2.94e+04 loss_x2y=4.3246e-01 ppl_x2y=1.54 loss_y2x=4.2189e-01 ppl_y2x=1.52 dual_loss=3.8616e-01
Validation X2Y - loss=7.6099e-01 ppl=2.14 best_loss=7.5508e-01 best_ppl=2.13                                            
Validation Y2X - loss=7.0381e-01 ppl=2.02 best_loss=6.9794e-01 best_ppl=2.01
Epoch 61 - |param|=9.43e+02 |g_param|=2.60e+04 loss_x2y=4.0645e-01 ppl_x2y=1.50 loss_y2x=4.1261e-01 ppl_y2x=1.51 dual_loss=3.9723e-01
Validation X2Y - loss=7.6024e-01 ppl=2.14 best_loss=7.5508e-01 best_ppl=2.13                                            
Validation Y2X - loss=7.0792e-01 ppl=2.03 best_loss=6.9794e-01 best_ppl=2.01
Epoch 62 - |param|=9.44e+02 |g_param|=2.59e+04 loss_x2y=4.1385e-01 ppl_x2y=1.51 loss_y2x=4.3268e-01 ppl_y2x=1.54 dual_loss=4.7709e-01
Validation X2Y - loss=7.4205e-01 ppl=2.10 best_loss=7.5508e-01 best_ppl=2.13                                            
Validation Y2X - loss=7.1203e-01 ppl=2.04 best_loss=6.9794e-01 best_ppl=2.01
Epoch 63 - |param|=9.44e+02 |g_param|=2.31e+04 loss_x2y=4.0822e-01 ppl_x2y=1.50 loss_y2x=4.4020e-01 ppl_y2x=1.55 dual_loss=4.8402e-01
Validation X2Y - loss=7.4354e-01 ppl=2.10 best_loss=7.4205e-01 best_ppl=2.10                                            
Validation Y2X - loss=7.0051e-01 ppl=2.01 best_loss=6.9794e-01 best_ppl=2.01
Epoch 64 - |param|=9.45e+02 |g_param|=2.48e+04 loss_x2y=3.8937e-01 ppl_x2y=1.48 loss_y2x=4.0385e-01 ppl_y2x=1.50 dual_loss=4.4106e-01
Validation X2Y - loss=7.4374e-01 ppl=2.10 best_loss=7.4205e-01 best_ppl=2.10                                            
Validation Y2X - loss=6.8812e-01 ppl=1.99 best_loss=6.9794e-01 best_ppl=2.01
Epoch 65 - |param|=9.45e+02 |g_param|=2.28e+04 loss_x2y=3.9420e-01 ppl_x2y=1.48 loss_y2x=4.0959e-01 ppl_y2x=1.51 dual_loss=4.2917e-01
Validation X2Y - loss=7.5348e-01 ppl=2.12 best_loss=7.4205e-01 best_ppl=2.10                                            
Validation Y2X - loss=6.9952e-01 ppl=2.01 best_loss=6.8812e-01 best_ppl=1.99
Epoch 66 - |param|=9.45e+02 |g_param|=2.90e+04 loss_x2y=3.6906e-01 ppl_x2y=1.45 loss_y2x=3.7232e-01 ppl_y2x=1.45 dual_loss=3.8182e-01
Validation X2Y - loss=7.3318e-01 ppl=2.08 best_loss=7.4205e-01 best_ppl=2.10                                            
Validation Y2X - loss=6.8098e-01 ppl=1.98 best_loss=6.8812e-01 best_ppl=1.99
Epoch 67 - |param|=9.46e+02 |g_param|=2.53e+04 loss_x2y=3.6948e-01 ppl_x2y=1.45 loss_y2x=3.7053e-01 ppl_y2x=1.45 dual_loss=3.3961e-01
Validation X2Y - loss=7.3378e-01 ppl=2.08 best_loss=7.3318e-01 best_ppl=2.08                                            
Validation Y2X - loss=6.9006e-01 ppl=1.99 best_loss=6.8098e-01 best_ppl=1.98
Epoch 68 - |param|=9.46e+02 |g_param|=3.46e+04 loss_x2y=3.8983e-01 ppl_x2y=1.48 loss_y2x=3.7435e-01 ppl_y2x=1.45 dual_loss=3.6194e-01
Validation X2Y - loss=7.3433e-01 ppl=2.08 best_loss=7.3318e-01 best_ppl=2.08                                            
Validation Y2X - loss=6.9172e-01 ppl=2.00 best_loss=6.8098e-01 best_ppl=1.98
Epoch 69 - |param|=9.47e+02 |g_param|=9.34e+04 loss_x2y=4.9712e-01 ppl_x2y=1.64 loss_y2x=3.8183e-01 ppl_y2x=1.46 dual_loss=6.4906e-01
Validation X2Y - loss=7.8098e-01 ppl=2.18 best_loss=7.3318e-01 best_ppl=2.08                                            
Validation Y2X - loss=6.7640e-01 ppl=1.97 best_loss=6.8098e-01 best_ppl=1.98
Epoch 70 - |param|=9.47e+02 |g_param|=2.87e+04 loss_x2y=4.6099e-01 ppl_x2y=1.59 loss_y2x=3.5494e-01 ppl_y2x=1.43 dual_loss=6.9691e-01
Validation X2Y - loss=7.2288e-01 ppl=2.06 best_loss=7.3318e-01 best_ppl=2.08                                            
Validation Y2X - loss=6.7183e-01 ppl=1.96 best_loss=6.7640e-01 best_ppl=1.97
Epoch 71 - |param|=9.48e+02 |g_param|=1.92e+04 loss_x2y=4.0476e-01 ppl_x2y=1.50 loss_y2x=3.5096e-01 ppl_y2x=1.42 dual_loss=3.3644e-01
Validation X2Y - loss=7.1885e-01 ppl=2.05 best_loss=7.2288e-01 best_ppl=2.06                                            
Validation Y2X - loss=6.7083e-01 ppl=1.96 best_loss=6.7183e-01 best_ppl=1.96
Epoch 72 - |param|=9.48e+02 |g_param|=1.76e+04 loss_x2y=3.8497e-01 ppl_x2y=1.47 loss_y2x=3.6129e-01 ppl_y2x=1.44 dual_loss=3.3248e-01
Validation X2Y - loss=7.0855e-01 ppl=2.03 best_loss=7.1885e-01 best_ppl=2.05                                            
Validation Y2X - loss=6.8437e-01 ppl=1.98 best_loss=6.7083e-01 best_ppl=1.96
Epoch 73 - |param|=9.48e+02 |g_param|=1.46e+04 loss_x2y=3.5256e-01 ppl_x2y=1.42 loss_y2x=3.4232e-01 ppl_y2x=1.41 dual_loss=3.1965e-01
Validation X2Y - loss=7.2798e-01 ppl=2.07 best_loss=7.0855e-01 best_ppl=2.03                                            
Validation Y2X - loss=6.6968e-01 ppl=1.95 best_loss=6.7083e-01 best_ppl=1.96
Epoch 74 - |param|=9.49e+02 |g_param|=1.67e+04 loss_x2y=3.5726e-01 ppl_x2y=1.43 loss_y2x=3.5312e-01 ppl_y2x=1.42 dual_loss=4.2957e-01
Validation X2Y - loss=7.0834e-01 ppl=2.03 best_loss=7.0855e-01 best_ppl=2.03                                            
Validation Y2X - loss=6.7648e-01 ppl=1.97 best_loss=6.6968e-01 best_ppl=1.95
Epoch 75 - |param|=9.49e+02 |g_param|=2.04e+04 loss_x2y=3.4807e-01 ppl_x2y=1.42 loss_y2x=3.6680e-01 ppl_y2x=1.44 dual_loss=4.5685e-01
Validation X2Y - loss=7.1263e-01 ppl=2.04 best_loss=7.0834e-01 best_ppl=2.03                                            
Validation Y2X - loss=6.9052e-01 ppl=1.99 best_loss=6.6968e-01 best_ppl=1.95
Epoch 76 - |param|=9.50e+02 |g_param|=2.52e+04 loss_x2y=3.3677e-01 ppl_x2y=1.40 loss_y2x=3.8569e-01 ppl_y2x=1.47 dual_loss=5.4957e-01
Validation X2Y - loss=7.2138e-01 ppl=2.06 best_loss=7.0834e-01 best_ppl=2.03                                            
Validation Y2X - loss=6.7670e-01 ppl=1.97 best_loss=6.6968e-01 best_ppl=1.95
Epoch 77 - |param|=9.50e+02 |g_param|=2.45e+04 loss_x2y=3.3890e-01 ppl_x2y=1.40 loss_y2x=4.1203e-01 ppl_y2x=1.51 dual_loss=6.8283e-01
Validation X2Y - loss=7.1418e-01 ppl=2.04 best_loss=7.0834e-01 best_ppl=2.03                                            
Validation Y2X - loss=7.0495e-01 ppl=2.02 best_loss=6.6968e-01 best_ppl=1.95
Epoch 78 - |param|=9.51e+02 |g_param|=4.43e+04 loss_x2y=3.8111e-01 ppl_x2y=1.46 loss_y2x=5.1683e-01 ppl_y2x=1.68 dual_loss=1.7026e+00
Validation X2Y - loss=7.3057e-01 ppl=2.08 best_loss=7.0834e-01 best_ppl=2.03                                            
Validation Y2X - loss=7.6830e-01 ppl=2.16 best_loss=6.6968e-01 best_ppl=1.95
Epoch 79 - |param|=9.51e+02 |g_param|=2.44e+04 loss_x2y=3.2351e-01 ppl_x2y=1.38 loss_y2x=3.6857e-01 ppl_y2x=1.45 dual_loss=5.7478e-01
Validation X2Y - loss=7.0801e-01 ppl=2.03 best_loss=7.0834e-01 best_ppl=2.03                                            
Validation Y2X - loss=6.8396e-01 ppl=1.98 best_loss=6.6968e-01 best_ppl=1.95
Epoch 80 - |param|=9.51e+02 |g_param|=2.31e+04 loss_x2y=3.2311e-01 ppl_x2y=1.38 loss_y2x=3.7588e-01 ppl_y2x=1.46 dual_loss=5.6463e-01
Validation X2Y - loss=7.1607e-01 ppl=2.05 best_loss=7.0801e-01 best_ppl=2.03                                            
Validation Y2X - loss=6.6427e-01 ppl=1.94 best_loss=6.6968e-01 best_ppl=1.95
Epoch 81 - |param|=9.52e+02 |g_param|=1.54e+04 loss_x2y=3.0575e-01 ppl_x2y=1.36 loss_y2x=3.2779e-01 ppl_y2x=1.39 dual_loss=4.0520e-01
Validation X2Y - loss=7.2310e-01 ppl=2.06 best_loss=7.0801e-01 best_ppl=2.03                                            
Validation Y2X - loss=6.4644e-01 ppl=1.91 best_loss=6.6427e-01 best_ppl=1.94
Epoch 82 - |param|=9.52e+02 |g_param|=1.44e+04 loss_x2y=3.0381e-01 ppl_x2y=1.36 loss_y2x=3.1348e-01 ppl_y2x=1.37 dual_loss=3.7691e-01
Validation X2Y - loss=7.1510e-01 ppl=2.04 best_loss=7.0801e-01 best_ppl=2.03                                            
Validation Y2X - loss=6.5228e-01 ppl=1.92 best_loss=6.4644e-01 best_ppl=1.91
Epoch 83 - |param|=9.53e+02 |g_param|=1.41e+04 loss_x2y=3.0229e-01 ppl_x2y=1.35 loss_y2x=3.0659e-01 ppl_y2x=1.36 dual_loss=3.5192e-01
Validation X2Y - loss=7.0882e-01 ppl=2.03 best_loss=7.0801e-01 best_ppl=2.03                                            
Validation Y2X - loss=6.5311e-01 ppl=1.92 best_loss=6.4644e-01 best_ppl=1.91
Epoch 84 - |param|=9.53e+02 |g_param|=1.37e+04 loss_x2y=2.9761e-01 ppl_x2y=1.35 loss_y2x=3.0206e-01 ppl_y2x=1.35 dual_loss=3.3279e-01
Validation X2Y - loss=7.1092e-01 ppl=2.04 best_loss=7.0801e-01 best_ppl=2.03                                            
Validation Y2X - loss=6.5394e-01 ppl=1.92 best_loss=6.4644e-01 best_ppl=1.91
Epoch 85 - |param|=9.53e+02 |g_param|=1.86e+04 loss_x2y=3.1497e-01 ppl_x2y=1.37 loss_y2x=2.9908e-01 ppl_y2x=1.35 dual_loss=3.3370e-01
Validation X2Y - loss=7.3010e-01 ppl=2.08 best_loss=7.0801e-01 best_ppl=2.03                                            
Validation Y2X - loss=6.5757e-01 ppl=1.93 best_loss=6.4644e-01 best_ppl=1.91
Epoch 86 - |param|=9.54e+02 |g_param|=2.86e+04 loss_x2y=3.2610e-01 ppl_x2y=1.39 loss_y2x=2.9612e-01 ppl_y2x=1.34 dual_loss=4.9691e-01
Validation X2Y - loss=7.7570e-01 ppl=2.17 best_loss=7.0801e-01 best_ppl=2.03                                            
Validation Y2X - loss=6.5529e-01 ppl=1.93 best_loss=6.4644e-01 best_ppl=1.91
Epoch 87 - |param|=9.54e+02 |g_param|=3.18e+04 loss_x2y=4.0831e-01 ppl_x2y=1.50 loss_y2x=2.9467e-01 ppl_y2x=1.34 dual_loss=5.5200e-01
Validation X2Y - loss=7.4220e-01 ppl=2.10 best_loss=7.0801e-01 best_ppl=2.03                                            
Validation Y2X - loss=6.4959e-01 ppl=1.91 best_loss=6.4644e-01 best_ppl=1.91
Epoch 88 - |param|=9.55e+02 |g_param|=1.89e+04 loss_x2y=3.3457e-01 ppl_x2y=1.40 loss_y2x=2.7004e-01 ppl_y2x=1.31 dual_loss=3.1724e-01
Validation X2Y - loss=7.0501e-01 ppl=2.02 best_loss=7.0801e-01 best_ppl=2.03                                            
Validation Y2X - loss=6.4843e-01 ppl=1.91 best_loss=6.4644e-01 best_ppl=1.91
Epoch 89 - |param|=9.55e+02 |g_param|=1.86e+04 loss_x2y=3.1214e-01 ppl_x2y=1.37 loss_y2x=2.7972e-01 ppl_y2x=1.32 dual_loss=2.7069e-01
Validation X2Y - loss=6.9799e-01 ppl=2.01 best_loss=7.0501e-01 best_ppl=2.02                                            
Validation Y2X - loss=6.4428e-01 ppl=1.90 best_loss=6.4644e-01 best_ppl=1.91
Epoch 90 - |param|=9.56e+02 |g_param|=2.81e+04 loss_x2y=4.2594e-01 ppl_x2y=1.53 loss_y2x=2.8838e-01 ppl_y2x=1.33 dual_loss=7.1482e-01
Validation X2Y - loss=7.8740e-01 ppl=2.20 best_loss=6.9799e-01 best_ppl=2.01                                            
Validation Y2X - loss=6.5164e-01 ppl=1.92 best_loss=6.4428e-01 best_ppl=1.90
Epoch 91 - |param|=9.56e+02 |g_param|=1.94e+04 loss_x2y=3.3055e-01 ppl_x2y=1.39 loss_y2x=2.6984e-01 ppl_y2x=1.31 dual_loss=2.9329e-01
Validation X2Y - loss=7.0659e-01 ppl=2.03 best_loss=6.9799e-01 best_ppl=2.01                                            
Validation Y2X - loss=6.4925e-01 ppl=1.91 best_loss=6.4428e-01 best_ppl=1.90
Epoch 92 - |param|=9.56e+02 |g_param|=2.21e+04 loss_x2y=3.0242e-01 ppl_x2y=1.35 loss_y2x=2.7377e-01 ppl_y2x=1.31 dual_loss=2.9317e-01
Validation X2Y - loss=7.0241e-01 ppl=2.02 best_loss=6.9799e-01 best_ppl=2.01                                            
Validation Y2X - loss=6.4534e-01 ppl=1.91 best_loss=6.4428e-01 best_ppl=1.90
Epoch 93 - |param|=9.57e+02 |g_param|=2.11e+04 loss_x2y=2.7648e-01 ppl_x2y=1.32 loss_y2x=2.6561e-01 ppl_y2x=1.30 dual_loss=2.9259e-01
Validation X2Y - loss=6.9704e-01 ppl=2.01 best_loss=6.9799e-01 best_ppl=2.01                                            
Validation Y2X - loss=6.6189e-01 ppl=1.94 best_loss=6.4428e-01 best_ppl=1.90
Epoch 94 - |param|=9.57e+02 |g_param|=1.89e+04 loss_x2y=2.6497e-01 ppl_x2y=1.30 loss_y2x=2.5734e-01 ppl_y2x=1.29 dual_loss=2.6704e-01
Validation X2Y - loss=7.0394e-01 ppl=2.02 best_loss=6.9704e-01 best_ppl=2.01                                            
Validation Y2X - loss=6.5111e-01 ppl=1.92 best_loss=6.4428e-01 best_ppl=1.90
Epoch 95 - |param|=9.57e+02 |g_param|=2.55e+04 loss_x2y=2.7341e-01 ppl_x2y=1.31 loss_y2x=2.7544e-01 ppl_y2x=1.32 dual_loss=3.4653e-01
Validation X2Y - loss=6.9454e-01 ppl=2.00 best_loss=6.9704e-01 best_ppl=2.01                                            
Validation Y2X - loss=6.5532e-01 ppl=1.93 best_loss=6.4428e-01 best_ppl=1.90
Epoch 96 - |param|=9.58e+02 |g_param|=3.48e+04 loss_x2y=2.7480e-01 ppl_x2y=1.32 loss_y2x=3.1222e-01 ppl_y2x=1.37 dual_loss=4.5760e-01
Validation X2Y - loss=7.0077e-01 ppl=2.02 best_loss=6.9454e-01 best_ppl=2.00                                            
Validation Y2X - loss=6.6637e-01 ppl=1.95 best_loss=6.4428e-01 best_ppl=1.90
Epoch 97 - |param|=9.58e+02 |g_param|=2.90e+04 loss_x2y=2.7518e-01 ppl_x2y=1.32 loss_y2x=2.8943e-01 ppl_y2x=1.34 dual_loss=4.9334e-01
Validation X2Y - loss=7.0006e-01 ppl=2.01 best_loss=6.9454e-01 best_ppl=2.00                                            
Validation Y2X - loss=6.6214e-01 ppl=1.94 best_loss=6.4428e-01 best_ppl=1.90
Epoch 98 - |param|=9.59e+02 |g_param|=3.74e+04 loss_x2y=2.6498e-01 ppl_x2y=1.30 loss_y2x=2.7007e-01 ppl_y2x=1.31 dual_loss=4.7453e-01
Validation X2Y - loss=7.0319e-01 ppl=2.02 best_loss=6.9454e-01 best_ppl=2.00                                            
Validation Y2X - loss=6.5119e-01 ppl=1.92 best_loss=6.4428e-01 best_ppl=1.90
Epoch 99 - |param|=9.59e+02 |g_param|=2.25e+04 loss_x2y=2.6247e-01 ppl_x2y=1.30 loss_y2x=2.9855e-01 ppl_y2x=1.35 dual_loss=6.6862e-01
Validation X2Y - loss=7.1012e-01 ppl=2.03 best_loss=6.9454e-01 best_ppl=2.00                                            
Validation Y2X - loss=6.6452e-01 ppl=1.94 best_loss=6.4428e-01 best_ppl=1.90
Epoch 100 - |param|=9.59e+02 |g_param|=1.31e+04 loss_x2y=2.6312e-01 ppl_x2y=1.30 loss_y2x=2.7954e-01 ppl_y2x=1.32 dual_loss=3.7921e-01
Validation X2Y - loss=7.0515e-01 ppl=2.02 best_loss=6.9454e-01 best_ppl=2.00                                            
Validation Y2X - loss=6.6946e-01 ppl=1.95 best_loss=6.4428e-01 best_ppl=1.90

real	42m0.940s
user	41m34.245s
sys	0m27.635s
```

## DSL with Transformer

### Preparing a Shell Script

```bash
#!/bin/bash

# Written by Ye, LST, NECTEC, Thailand
# Last Updated: 22 Mar 2022
# for training Dual Supervised Learning models

#Reference of Transformer Command
#time python train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev --lang myrk --gpu_id 0 --batch_size 16 --n_epochs 40 --max_length 100 --dropout .2 --hidden_size 32 --n_layers 6 --max_grad_norm 1e+8 --iteration_per_update 32 --lr 1e-3 --lr_step 0 --use_adam --use_transformer --rl_n_epochs 0 --init_epoch 1 --model_fn ./model/transformer/baseline/myrk-40epoch/myrk-transformer-model.pth
# အထက်ပါ command ကို အခြေခံပြီး run ပေမဲ့ အောက်ပါ error ပေးတယ်။ တချို့ parameter တွေကို မသိဘူး
# dual_train.py: error: unrecognized arguments: --lr 1e-3 --lr_step 0 --use_adam --rl_n_epochs 0

for i in {30,40,50,60,70,80,90,100}
do
   echo "training start for ${i} epochs...";
   time python dual_train.py --train /home/ye/exp/simple-nmt/data/train --valid /home/ye/exp/simple-nmt/data/dev \
   --lang myrk \
   --gpu_id 1 --batch_size 64 --n_epochs ${i} --max_length 100 --dropout .2 \
   --word_vec_size 128 --hidden_size 128 --n_layers 4 --max_grad_norm 1e+8 --iteration_per_update 2 \
   --dsl_n_warmup_epochs 20 --dsl_lambda 1e-2 \
   --lm_fn ./model/lm/lm-200epoch.pth \
   --use_transformer --init_epoch 1\
   --model_fn ./model/dsl/transformer/myrk-${i}epoch/dsl-model-myrk.pth | tee ./model/dsl/transformer/myrk-${i}epoch/training.log;
done

```

### with LM 200 Epoch

#### Warmup-Epoch 20, Total Epoch 30

```
Epoch 1 - |param|=9.11e+02 |g_param|=1.70e+05 loss_x2y=3.5651e+00 ppl_x2y=35.34 loss_y2x=3.5190e+00 ppl_y2x=33.75 dual_loss=0.0000e+00
Validation X2Y - loss=2.9831e+00 ppl=19.75 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=2.8470e+00 ppl=17.24 best_loss=inf best_ppl=inf
Epoch 2 - |param|=9.12e+02 |g_param|=2.07e+05 loss_x2y=2.5002e+00 ppl_x2y=12.18 loss_y2x=2.3877e+00 ppl_y2x=10.89 dual_loss=0.0000e+00
Validation X2Y - loss=2.0886e+00 ppl=8.07 best_loss=2.9831e+00 best_ppl=19.75                                           
Validation Y2X - loss=1.9488e+00 ppl=7.02 best_loss=2.8470e+00 best_ppl=17.24
Epoch 3 - |param|=9.12e+02 |g_param|=2.38e+05 loss_x2y=1.8428e+00 ppl_x2y=6.31 loss_y2x=1.7545e+00 ppl_y2x=5.78 dual_loss=0.0000e+00
Validation X2Y - loss=1.4868e+00 ppl=4.42 best_loss=2.0886e+00 best_ppl=8.07                                            
Validation Y2X - loss=1.4049e+00 ppl=4.08 best_loss=1.9488e+00 best_ppl=7.02
Epoch 4 - |param|=9.13e+02 |g_param|=2.33e+05 loss_x2y=1.3393e+00 ppl_x2y=3.82 loss_y2x=1.3072e+00 ppl_y2x=3.70 dual_loss=0.0000e+00
Validation X2Y - loss=1.1512e+00 ppl=3.16 best_loss=1.4868e+00 best_ppl=4.42                                            
Validation Y2X - loss=1.1156e+00 ppl=3.05 best_loss=1.4049e+00 best_ppl=4.08
Epoch 5 - |param|=9.13e+02 |g_param|=2.03e+05 loss_x2y=1.1216e+00 ppl_x2y=3.07 loss_y2x=1.1369e+00 ppl_y2x=3.12 dual_loss=0.0000e+00
Validation X2Y - loss=9.8886e-01 ppl=2.69 best_loss=1.1512e+00 best_ppl=3.16                                            
Validation Y2X - loss=9.5867e-01 ppl=2.61 best_loss=1.1156e+00 best_ppl=3.05
Epoch 6 - |param|=9.13e+02 |g_param|=2.05e+05 loss_x2y=9.4599e-01 ppl_x2y=2.58 loss_y2x=9.4084e-01 ppl_y2x=2.56 dual_loss=0.0000e+00
Validation X2Y - loss=8.7381e-01 ppl=2.40 best_loss=9.8886e-01 best_ppl=2.69                                            
Validation Y2X - loss=8.6823e-01 ppl=2.38 best_loss=9.5867e-01 best_ppl=2.61
Epoch 7 - |param|=9.14e+02 |g_param|=1.87e+05 loss_x2y=8.2682e-01 ppl_x2y=2.29 loss_y2x=8.2537e-01 ppl_y2x=2.28 dual_loss=0.0000e+00
Validation X2Y - loss=8.1671e-01 ppl=2.26 best_loss=8.7381e-01 best_ppl=2.40                                            
Validation Y2X - loss=8.1485e-01 ppl=2.26 best_loss=8.6823e-01 best_ppl=2.38
Epoch 8 - |param|=9.14e+02 |g_param|=1.92e+05 loss_x2y=7.6067e-01 ppl_x2y=2.14 loss_y2x=7.6325e-01 ppl_y2x=2.15 dual_loss=0.0000e+00
Validation X2Y - loss=7.4610e-01 ppl=2.11 best_loss=8.1671e-01 best_ppl=2.26                                            
Validation Y2X - loss=7.8175e-01 ppl=2.19 best_loss=8.1485e-01 best_ppl=2.26
Epoch 9 - |param|=9.14e+02 |g_param|=1.75e+05 loss_x2y=6.7541e-01 ppl_x2y=1.96 loss_y2x=6.6980e-01 ppl_y2x=1.95 dual_loss=0.0000e+00
Validation X2Y - loss=7.2416e-01 ppl=2.06 best_loss=7.4610e-01 best_ppl=2.11                                            
Validation Y2X - loss=6.8677e-01 ppl=1.99 best_loss=7.8175e-01 best_ppl=2.19
Epoch 10 - |param|=9.15e+02 |g_param|=1.87e+05 loss_x2y=6.1698e-01 ppl_x2y=1.85 loss_y2x=6.2395e-01 ppl_y2x=1.87 dual_loss=0.0000e+00
Validation X2Y - loss=7.1777e-01 ppl=2.05 best_loss=7.2416e-01 best_ppl=2.06                                            
Validation Y2X - loss=6.7458e-01 ppl=1.96 best_loss=6.8677e-01 best_ppl=1.99
Epoch 11 - |param|=9.15e+02 |g_param|=1.77e+05 loss_x2y=5.7556e-01 ppl_x2y=1.78 loss_y2x=5.6258e-01 ppl_y2x=1.76 dual_loss=0.0000e+00
Validation X2Y - loss=7.0021e-01 ppl=2.01 best_loss=7.1777e-01 best_ppl=2.05                                            
Validation Y2X - loss=6.4422e-01 ppl=1.90 best_loss=6.7458e-01 best_ppl=1.96
Epoch 12 - |param|=9.15e+02 |g_param|=1.27e+05 loss_x2y=5.2544e-01 ppl_x2y=1.69 loss_y2x=5.3257e-01 ppl_y2x=1.70 dual_loss=0.0000e+00
Validation X2Y - loss=6.7986e-01 ppl=1.97 best_loss=7.0021e-01 best_ppl=2.01                                            
Validation Y2X - loss=6.2216e-01 ppl=1.86 best_loss=6.4422e-01 best_ppl=1.90
Epoch 13 - |param|=9.16e+02 |g_param|=1.14e+05 loss_x2y=4.6511e-01 ppl_x2y=1.59 loss_y2x=4.5968e-01 ppl_y2x=1.58 dual_loss=0.0000e+00
Validation X2Y - loss=7.0525e-01 ppl=2.02 best_loss=6.7986e-01 best_ppl=1.97                                            
Validation Y2X - loss=6.1064e-01 ppl=1.84 best_loss=6.2216e-01 best_ppl=1.86
Epoch 14 - |param|=9.16e+02 |g_param|=1.02e+05 loss_x2y=4.6903e-01 ppl_x2y=1.60 loss_y2x=4.6461e-01 ppl_y2x=1.59 dual_loss=0.0000e+00
Validation X2Y - loss=6.7017e-01 ppl=1.95 best_loss=6.7986e-01 best_ppl=1.97                                            
Validation Y2X - loss=6.0004e-01 ppl=1.82 best_loss=6.1064e-01 best_ppl=1.84
Epoch 15 - |param|=9.16e+02 |g_param|=9.76e+04 loss_x2y=4.5812e-01 ppl_x2y=1.58 loss_y2x=4.4335e-01 ppl_y2x=1.56 dual_loss=0.0000e+00
Validation X2Y - loss=6.6291e-01 ppl=1.94 best_loss=6.7017e-01 best_ppl=1.95                                            
Validation Y2X - loss=5.8706e-01 ppl=1.80 best_loss=6.0004e-01 best_ppl=1.82
Epoch 16 - |param|=9.17e+02 |g_param|=9.33e+04 loss_x2y=4.2483e-01 ppl_x2y=1.53 loss_y2x=4.2700e-01 ppl_y2x=1.53 dual_loss=0.0000e+00
Validation X2Y - loss=6.5375e-01 ppl=1.92 best_loss=6.6291e-01 best_ppl=1.94                                            
Validation Y2X - loss=6.0268e-01 ppl=1.83 best_loss=5.8706e-01 best_ppl=1.80
Epoch 17 - |param|=9.17e+02 |g_param|=1.06e+05 loss_x2y=3.9681e-01 ppl_x2y=1.49 loss_y2x=4.0088e-01 ppl_y2x=1.49 dual_loss=0.0000e+00
Validation X2Y - loss=6.4252e-01 ppl=1.90 best_loss=6.5375e-01 best_ppl=1.92                                            
Validation Y2X - loss=5.8691e-01 ppl=1.80 best_loss=5.8706e-01 best_ppl=1.80
Epoch 18 - |param|=9.17e+02 |g_param|=1.03e+05 loss_x2y=3.9700e-01 ppl_x2y=1.49 loss_y2x=3.9435e-01 ppl_y2x=1.48 dual_loss=0.0000e+00
Validation X2Y - loss=6.5916e-01 ppl=1.93 best_loss=6.4252e-01 best_ppl=1.90                                            
Validation Y2X - loss=5.9134e-01 ppl=1.81 best_loss=5.8691e-01 best_ppl=1.80
Epoch 19 - |param|=9.18e+02 |g_param|=9.23e+04 loss_x2y=3.4409e-01 ppl_x2y=1.41 loss_y2x=3.3935e-01 ppl_y2x=1.40 dual_loss=0.0000e+00
Validation X2Y - loss=6.5863e-01 ppl=1.93 best_loss=6.4252e-01 best_ppl=1.90                                            
Validation Y2X - loss=5.8228e-01 ppl=1.79 best_loss=5.8691e-01 best_ppl=1.80
Epoch 20 - |param|=9.18e+02 |g_param|=8.97e+04 loss_x2y=3.5294e-01 ppl_x2y=1.42 loss_y2x=3.4664e-01 ppl_y2x=1.41 dual_loss=0.0000e+00
Validation X2Y - loss=6.4482e-01 ppl=1.91 best_loss=6.4252e-01 best_ppl=1.90                                            
Validation Y2X - loss=5.6170e-01 ppl=1.75 best_loss=5.8228e-01 best_ppl=1.79
Epoch 21 - |param|=9.19e+02 |g_param|=1.05e+05 loss_x2y=3.5314e-01 ppl_x2y=1.42 loss_y2x=3.5309e-01 ppl_y2x=1.42 dual_loss=6.2018e-01
Validation X2Y - loss=6.3535e-01 ppl=1.89 best_loss=6.4252e-01 best_ppl=1.90                                            
Validation Y2X - loss=5.9070e-01 ppl=1.81 best_loss=5.6170e-01 best_ppl=1.75
Epoch 22 - |param|=9.19e+02 |g_param|=9.92e+04 loss_x2y=3.4514e-01 ppl_x2y=1.41 loss_y2x=3.3391e-01 ppl_y2x=1.40 dual_loss=4.5185e-01
Validation X2Y - loss=6.4305e-01 ppl=1.90 best_loss=6.3535e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9933e-01 ppl=1.82 best_loss=5.6170e-01 best_ppl=1.75
Epoch 23 - |param|=9.19e+02 |g_param|=1.05e+05 loss_x2y=3.3129e-01 ppl_x2y=1.39 loss_y2x=3.2088e-01 ppl_y2x=1.38 dual_loss=3.9361e-01
Validation X2Y - loss=6.4564e-01 ppl=1.91 best_loss=6.3535e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.8434e-01 ppl=1.79 best_loss=5.6170e-01 best_ppl=1.75
Epoch 24 - |param|=9.20e+02 |g_param|=9.55e+04 loss_x2y=3.0811e-01 ppl_x2y=1.36 loss_y2x=3.2193e-01 ppl_y2x=1.38 dual_loss=3.9020e-01
Validation X2Y - loss=6.3293e-01 ppl=1.88 best_loss=6.3535e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.8136e-01 ppl=1.79 best_loss=5.6170e-01 best_ppl=1.75
Epoch 25 - |param|=9.20e+02 |g_param|=9.22e+04 loss_x2y=3.0306e-01 ppl_x2y=1.35 loss_y2x=3.1424e-01 ppl_y2x=1.37 dual_loss=4.2407e-01
Validation X2Y - loss=6.5627e-01 ppl=1.93 best_loss=6.3293e-01 best_ppl=1.88                                            
Validation Y2X - loss=5.8804e-01 ppl=1.80 best_loss=5.6170e-01 best_ppl=1.75
Epoch 26 - |param|=9.21e+02 |g_param|=1.62e+05 loss_x2y=2.9222e-01 ppl_x2y=1.34 loss_y2x=2.8044e-01 ppl_y2x=1.32 dual_loss=3.4005e-01
Validation X2Y - loss=6.6677e-01 ppl=1.95 best_loss=6.3293e-01 best_ppl=1.88                                            
Validation Y2X - loss=6.5120e-01 ppl=1.92 best_loss=5.6170e-01 best_ppl=1.75
Epoch 27 - |param|=9.21e+02 |g_param|=1.35e+05 loss_x2y=2.9776e-01 ppl_x2y=1.35 loss_y2x=2.9773e-01 ppl_y2x=1.35 dual_loss=4.1239e-01
Validation X2Y - loss=6.4940e-01 ppl=1.91 best_loss=6.3293e-01 best_ppl=1.88                                            
Validation Y2X - loss=5.7978e-01 ppl=1.79 best_loss=5.6170e-01 best_ppl=1.75
Epoch 28 - |param|=9.21e+02 |g_param|=1.33e+05 loss_x2y=2.8437e-01 ppl_x2y=1.33 loss_y2x=2.9646e-01 ppl_y2x=1.35 dual_loss=4.4742e-01
Validation X2Y - loss=6.5885e-01 ppl=1.93 best_loss=6.3293e-01 best_ppl=1.88                                            
Validation Y2X - loss=5.8634e-01 ppl=1.80 best_loss=5.6170e-01 best_ppl=1.75
Epoch 29 - |param|=9.22e+02 |g_param|=1.30e+05 loss_x2y=2.7309e-01 ppl_x2y=1.31 loss_y2x=2.7342e-01 ppl_y2x=1.31 dual_loss=3.5199e-01
Validation X2Y - loss=6.5033e-01 ppl=1.92 best_loss=6.3293e-01 best_ppl=1.88                                            
Validation Y2X - loss=5.7922e-01 ppl=1.78 best_loss=5.6170e-01 best_ppl=1.75
Epoch 30 - |param|=9.22e+02 |g_param|=1.37e+05 loss_x2y=2.8325e-01 ppl_x2y=1.33 loss_y2x=2.7698e-01 ppl_y2x=1.32 dual_loss=3.7097e-01
Validation X2Y - loss=6.4966e-01 ppl=1.91 best_loss=6.3293e-01 best_ppl=1.88                                            
Validation Y2X - loss=5.9366e-01 ppl=1.81 best_loss=5.6170e-01 best_ppl=1.75

real	15m14.826s
user	14m54.579s
sys	0m20.827s
```

#### Warmup-Epoch 20, Total Epoch 40

```
Epoch 1 - |param|=9.12e+02 |g_param|=3.32e+05 loss_x2y=3.5918e+00 ppl_x2y=36.30 loss_y2x=3.5543e+00 ppl_y2x=34.96 dual_loss=0.0000e+00
Validation X2Y - loss=2.9263e+00 ppl=18.66 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=2.9142e+00 ppl=18.43 best_loss=inf best_ppl=inf
Epoch 2 - |param|=9.13e+02 |g_param|=3.72e+05 loss_x2y=2.3807e+00 ppl_x2y=10.81 loss_y2x=2.3996e+00 ppl_y2x=11.02 dual_loss=0.0000e+00
Validation X2Y - loss=2.0004e+00 ppl=7.39 best_loss=2.9263e+00 best_ppl=18.66                                           
Validation Y2X - loss=1.9966e+00 ppl=7.36 best_loss=2.9142e+00 best_ppl=18.43
Epoch 3 - |param|=9.13e+02 |g_param|=2.43e+05 loss_x2y=1.7121e+00 ppl_x2y=5.54 loss_y2x=1.7410e+00 ppl_y2x=5.70 dual_loss=0.0000e+00
Validation X2Y - loss=1.4228e+00 ppl=4.15 best_loss=2.0004e+00 best_ppl=7.39                                            
Validation Y2X - loss=1.4694e+00 ppl=4.35 best_loss=1.9966e+00 best_ppl=7.36
Epoch 4 - |param|=9.13e+02 |g_param|=2.46e+05 loss_x2y=1.3631e+00 ppl_x2y=3.91 loss_y2x=1.3924e+00 ppl_y2x=4.02 dual_loss=0.0000e+00
Validation X2Y - loss=1.0916e+00 ppl=2.98 best_loss=1.4228e+00 best_ppl=4.15                                            
Validation Y2X - loss=1.1236e+00 ppl=3.08 best_loss=1.4694e+00 best_ppl=4.35
Epoch 5 - |param|=9.14e+02 |g_param|=2.32e+05 loss_x2y=1.0620e+00 ppl_x2y=2.89 loss_y2x=1.0853e+00 ppl_y2x=2.96 dual_loss=0.0000e+00
Validation X2Y - loss=9.4231e-01 ppl=2.57 best_loss=1.0916e+00 best_ppl=2.98                                            
Validation Y2X - loss=9.3516e-01 ppl=2.55 best_loss=1.1236e+00 best_ppl=3.08
Epoch 6 - |param|=9.14e+02 |g_param|=2.46e+05 loss_x2y=9.2772e-01 ppl_x2y=2.53 loss_y2x=9.6138e-01 ppl_y2x=2.62 dual_loss=0.0000e+00
Validation X2Y - loss=8.3655e-01 ppl=2.31 best_loss=9.4231e-01 best_ppl=2.57                                            
Validation Y2X - loss=8.4912e-01 ppl=2.34 best_loss=9.3516e-01 best_ppl=2.55
Epoch 7 - |param|=9.14e+02 |g_param|=2.72e+05 loss_x2y=8.2969e-01 ppl_x2y=2.29 loss_y2x=8.5682e-01 ppl_y2x=2.36 dual_loss=0.0000e+00
Validation X2Y - loss=7.7824e-01 ppl=2.18 best_loss=8.3655e-01 best_ppl=2.31                                            
Validation Y2X - loss=7.6565e-01 ppl=2.15 best_loss=8.4912e-01 best_ppl=2.34
Epoch 8 - |param|=9.14e+02 |g_param|=2.30e+05 loss_x2y=6.8144e-01 ppl_x2y=1.98 loss_y2x=7.0834e-01 ppl_y2x=2.03 dual_loss=0.0000e+00
Validation X2Y - loss=7.5644e-01 ppl=2.13 best_loss=7.7824e-01 best_ppl=2.18                                            
Validation Y2X - loss=6.9569e-01 ppl=2.01 best_loss=7.6565e-01 best_ppl=2.15
Epoch 9 - |param|=9.15e+02 |g_param|=2.39e+05 loss_x2y=6.5167e-01 ppl_x2y=1.92 loss_y2x=6.9950e-01 ppl_y2x=2.01 dual_loss=0.0000e+00
Validation X2Y - loss=7.3400e-01 ppl=2.08 best_loss=7.5644e-01 best_ppl=2.13                                            
Validation Y2X - loss=6.9631e-01 ppl=2.01 best_loss=6.9569e-01 best_ppl=2.01
Epoch 10 - |param|=9.15e+02 |g_param|=2.12e+05 loss_x2y=5.6593e-01 ppl_x2y=1.76 loss_y2x=5.7855e-01 ppl_y2x=1.78 dual_loss=0.0000e+00
Validation X2Y - loss=6.9317e-01 ppl=2.00 best_loss=7.3400e-01 best_ppl=2.08                                            
Validation Y2X - loss=6.5948e-01 ppl=1.93 best_loss=6.9569e-01 best_ppl=2.01
Epoch 11 - |param|=9.15e+02 |g_param|=1.87e+05 loss_x2y=5.5572e-01 ppl_x2y=1.74 loss_y2x=5.7978e-01 ppl_y2x=1.79 dual_loss=0.0000e+00
Validation X2Y - loss=6.8114e-01 ppl=1.98 best_loss=6.9317e-01 best_ppl=2.00                                            
Validation Y2X - loss=6.5388e-01 ppl=1.92 best_loss=6.5948e-01 best_ppl=1.93
Epoch 12 - |param|=9.16e+02 |g_param|=1.79e+05 loss_x2y=4.9864e-01 ppl_x2y=1.65 loss_y2x=5.2871e-01 ppl_y2x=1.70 dual_loss=0.0000e+00
Validation X2Y - loss=6.4681e-01 ppl=1.91 best_loss=6.8114e-01 best_ppl=1.98                                            
Validation Y2X - loss=6.2766e-01 ppl=1.87 best_loss=6.5388e-01 best_ppl=1.92
Epoch 13 - |param|=9.16e+02 |g_param|=1.66e+05 loss_x2y=4.8910e-01 ppl_x2y=1.63 loss_y2x=5.0320e-01 ppl_y2x=1.65 dual_loss=0.0000e+00
Validation X2Y - loss=6.6121e-01 ppl=1.94 best_loss=6.4681e-01 best_ppl=1.91                                            
Validation Y2X - loss=5.9703e-01 ppl=1.82 best_loss=6.2766e-01 best_ppl=1.87
Epoch 14 - |param|=9.16e+02 |g_param|=1.84e+05 loss_x2y=4.7863e-01 ppl_x2y=1.61 loss_y2x=5.0308e-01 ppl_y2x=1.65 dual_loss=0.0000e+00
Validation X2Y - loss=6.3547e-01 ppl=1.89 best_loss=6.4681e-01 best_ppl=1.91                                            
Validation Y2X - loss=6.2407e-01 ppl=1.87 best_loss=5.9703e-01 best_ppl=1.82
Epoch 15 - |param|=9.17e+02 |g_param|=1.51e+05 loss_x2y=4.0792e-01 ppl_x2y=1.50 loss_y2x=4.1767e-01 ppl_y2x=1.52 dual_loss=0.0000e+00
Validation X2Y - loss=6.6090e-01 ppl=1.94 best_loss=6.3547e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9055e-01 ppl=1.80 best_loss=5.9703e-01 best_ppl=1.82
Epoch 16 - |param|=9.17e+02 |g_param|=1.57e+05 loss_x2y=4.2646e-01 ppl_x2y=1.53 loss_y2x=4.2807e-01 ppl_y2x=1.53 dual_loss=0.0000e+00
Validation X2Y - loss=6.4247e-01 ppl=1.90 best_loss=6.3547e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.8588e-01 ppl=1.80 best_loss=5.9055e-01 best_ppl=1.80
Epoch 17 - |param|=9.18e+02 |g_param|=1.63e+05 loss_x2y=3.9570e-01 ppl_x2y=1.49 loss_y2x=3.8906e-01 ppl_y2x=1.48 dual_loss=0.0000e+00
Validation X2Y - loss=6.4180e-01 ppl=1.90 best_loss=6.3547e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9469e-01 ppl=1.81 best_loss=5.8588e-01 best_ppl=1.80
Epoch 18 - |param|=9.18e+02 |g_param|=1.55e+05 loss_x2y=3.7220e-01 ppl_x2y=1.45 loss_y2x=3.8739e-01 ppl_y2x=1.47 dual_loss=0.0000e+00
Validation X2Y - loss=6.2655e-01 ppl=1.87 best_loss=6.3547e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.0792e-01 ppl=1.84 best_loss=5.8588e-01 best_ppl=1.80
Epoch 19 - |param|=9.18e+02 |g_param|=1.47e+05 loss_x2y=3.5426e-01 ppl_x2y=1.43 loss_y2x=3.5465e-01 ppl_y2x=1.43 dual_loss=0.0000e+00
Validation X2Y - loss=6.3479e-01 ppl=1.89 best_loss=6.2655e-01 best_ppl=1.87                                            
Validation Y2X - loss=5.8732e-01 ppl=1.80 best_loss=5.8588e-01 best_ppl=1.80
Epoch 20 - |param|=9.19e+02 |g_param|=1.45e+05 loss_x2y=3.3819e-01 ppl_x2y=1.40 loss_y2x=3.3748e-01 ppl_y2x=1.40 dual_loss=0.0000e+00
Validation X2Y - loss=6.4904e-01 ppl=1.91 best_loss=6.2655e-01 best_ppl=1.87                                            
Validation Y2X - loss=5.9074e-01 ppl=1.81 best_loss=5.8588e-01 best_ppl=1.80
Epoch 21 - |param|=9.19e+02 |g_param|=1.70e+05 loss_x2y=3.5222e-01 ppl_x2y=1.42 loss_y2x=3.5626e-01 ppl_y2x=1.43 dual_loss=5.1152e-01
Validation X2Y - loss=6.2798e-01 ppl=1.87 best_loss=6.2655e-01 best_ppl=1.87                                            
Validation Y2X - loss=5.9243e-01 ppl=1.81 best_loss=5.8588e-01 best_ppl=1.80
Epoch 22 - |param|=9.20e+02 |g_param|=1.48e+05 loss_x2y=3.1746e-01 ppl_x2y=1.37 loss_y2x=3.3197e-01 ppl_y2x=1.39 dual_loss=4.0665e-01
Validation X2Y - loss=6.2377e-01 ppl=1.87 best_loss=6.2655e-01 best_ppl=1.87                                            
Validation Y2X - loss=5.8018e-01 ppl=1.79 best_loss=5.8588e-01 best_ppl=1.80
Epoch 23 - |param|=9.20e+02 |g_param|=2.23e+05 loss_x2y=3.1194e-01 ppl_x2y=1.37 loss_y2x=3.2435e-01 ppl_y2x=1.38 dual_loss=3.7517e-01
Validation X2Y - loss=6.2373e-01 ppl=1.87 best_loss=6.2377e-01 best_ppl=1.87                                            
Validation Y2X - loss=5.7475e-01 ppl=1.78 best_loss=5.8018e-01 best_ppl=1.79
Epoch 24 - |param|=9.20e+02 |g_param|=3.50e+05 loss_x2y=3.1112e-01 ppl_x2y=1.36 loss_y2x=3.4468e-01 ppl_y2x=1.41 dual_loss=5.5593e-01
Validation X2Y - loss=6.2602e-01 ppl=1.87 best_loss=6.2373e-01 best_ppl=1.87                                            
Validation Y2X - loss=5.8284e-01 ppl=1.79 best_loss=5.7475e-01 best_ppl=1.78
Epoch 25 - |param|=9.21e+02 |g_param|=2.58e+05 loss_x2y=2.9229e-01 ppl_x2y=1.34 loss_y2x=2.9445e-01 ppl_y2x=1.34 dual_loss=3.5661e-01
Validation X2Y - loss=6.3015e-01 ppl=1.88 best_loss=6.2373e-01 best_ppl=1.87                                            
Validation Y2X - loss=6.0189e-01 ppl=1.83 best_loss=5.7475e-01 best_ppl=1.78
Epoch 26 - |param|=9.21e+02 |g_param|=3.07e+05 loss_x2y=2.9355e-01 ppl_x2y=1.34 loss_y2x=3.0881e-01 ppl_y2x=1.36 dual_loss=4.2631e-01
Validation X2Y - loss=6.2556e-01 ppl=1.87 best_loss=6.2373e-01 best_ppl=1.87                                            
Validation Y2X - loss=5.8017e-01 ppl=1.79 best_loss=5.7475e-01 best_ppl=1.78
Epoch 27 - |param|=9.22e+02 |g_param|=2.69e+05 loss_x2y=2.6725e-01 ppl_x2y=1.31 loss_y2x=2.7299e-01 ppl_y2x=1.31 dual_loss=3.5842e-01
Validation X2Y - loss=6.2499e-01 ppl=1.87 best_loss=6.2373e-01 best_ppl=1.87                                            
Validation Y2X - loss=5.6297e-01 ppl=1.76 best_loss=5.7475e-01 best_ppl=1.78
Epoch 28 - |param|=9.22e+02 |g_param|=2.97e+05 loss_x2y=2.9232e-01 ppl_x2y=1.34 loss_y2x=2.9823e-01 ppl_y2x=1.35 dual_loss=4.2347e-01
Validation X2Y - loss=6.3566e-01 ppl=1.89 best_loss=6.2373e-01 best_ppl=1.87                                            
Validation Y2X - loss=5.7092e-01 ppl=1.77 best_loss=5.6297e-01 best_ppl=1.76
Epoch 29 - |param|=9.22e+02 |g_param|=2.69e+05 loss_x2y=2.6905e-01 ppl_x2y=1.31 loss_y2x=2.7291e-01 ppl_y2x=1.31 dual_loss=3.6977e-01
Validation X2Y - loss=6.0827e-01 ppl=1.84 best_loss=6.2373e-01 best_ppl=1.87                                            
Validation Y2X - loss=5.6852e-01 ppl=1.77 best_loss=5.6297e-01 best_ppl=1.76
Epoch 30 - |param|=9.23e+02 |g_param|=2.68e+05 loss_x2y=2.6302e-01 ppl_x2y=1.30 loss_y2x=2.6667e-01 ppl_y2x=1.31 dual_loss=3.6385e-01
Validation X2Y - loss=6.2681e-01 ppl=1.87 best_loss=6.0827e-01 best_ppl=1.84                                            
Validation Y2X - loss=6.1207e-01 ppl=1.84 best_loss=5.6297e-01 best_ppl=1.76
Epoch 31 - |param|=9.23e+02 |g_param|=2.56e+05 loss_x2y=2.5435e-01 ppl_x2y=1.29 loss_y2x=2.4377e-01 ppl_y2x=1.28 dual_loss=3.3014e-01
Validation X2Y - loss=6.4570e-01 ppl=1.91 best_loss=6.0827e-01 best_ppl=1.84                                            
Validation Y2X - loss=5.8274e-01 ppl=1.79 best_loss=5.6297e-01 best_ppl=1.76
Epoch 32 - |param|=9.24e+02 |g_param|=2.87e+05 loss_x2y=2.5264e-01 ppl_x2y=1.29 loss_y2x=2.5018e-01 ppl_y2x=1.28 dual_loss=3.7052e-01
Validation X2Y - loss=6.3673e-01 ppl=1.89 best_loss=6.0827e-01 best_ppl=1.84                                            
Validation Y2X - loss=6.2978e-01 ppl=1.88 best_loss=5.6297e-01 best_ppl=1.76
Epoch 33 - |param|=9.24e+02 |g_param|=2.94e+05 loss_x2y=2.3612e-01 ppl_x2y=1.27 loss_y2x=2.4085e-01 ppl_y2x=1.27 dual_loss=3.7147e-01
Validation X2Y - loss=6.3391e-01 ppl=1.88 best_loss=6.0827e-01 best_ppl=1.84                                            
Validation Y2X - loss=5.8025e-01 ppl=1.79 best_loss=5.6297e-01 best_ppl=1.76
Epoch 34 - |param|=9.24e+02 |g_param|=2.92e+05 loss_x2y=2.3518e-01 ppl_x2y=1.27 loss_y2x=2.4453e-01 ppl_y2x=1.28 dual_loss=4.0739e-01
Validation X2Y - loss=6.4847e-01 ppl=1.91 best_loss=6.0827e-01 best_ppl=1.84                                            
Validation Y2X - loss=5.8373e-01 ppl=1.79 best_loss=5.6297e-01 best_ppl=1.76
Epoch 35 - |param|=9.25e+02 |g_param|=2.96e+05 loss_x2y=2.2749e-01 ppl_x2y=1.26 loss_y2x=2.3565e-01 ppl_y2x=1.27 dual_loss=3.9142e-01
Validation X2Y - loss=6.4286e-01 ppl=1.90 best_loss=6.0827e-01 best_ppl=1.84                                            
Validation Y2X - loss=5.8077e-01 ppl=1.79 best_loss=5.6297e-01 best_ppl=1.76
Epoch 36 - |param|=9.25e+02 |g_param|=2.96e+05 loss_x2y=2.3089e-01 ppl_x2y=1.26 loss_y2x=2.3258e-01 ppl_y2x=1.26 dual_loss=3.6213e-01
Validation X2Y - loss=6.3793e-01 ppl=1.89 best_loss=6.0827e-01 best_ppl=1.84                                            
Validation Y2X - loss=5.9726e-01 ppl=1.82 best_loss=5.6297e-01 best_ppl=1.76
Epoch 37 - |param|=9.26e+02 |g_param|=2.37e+05 loss_x2y=2.2438e-01 ppl_x2y=1.25 loss_y2x=2.3391e-01 ppl_y2x=1.26 dual_loss=4.3340e-01
Validation X2Y - loss=6.4254e-01 ppl=1.90 best_loss=6.0827e-01 best_ppl=1.84                                            
Validation Y2X - loss=6.1330e-01 ppl=1.85 best_loss=5.6297e-01 best_ppl=1.76
Epoch 38 - |param|=9.26e+02 |g_param|=1.72e+05 loss_x2y=2.1452e-01 ppl_x2y=1.24 loss_y2x=2.2036e-01 ppl_y2x=1.25 dual_loss=3.6880e-01
Validation X2Y - loss=6.4708e-01 ppl=1.91 best_loss=6.0827e-01 best_ppl=1.84                                            
Validation Y2X - loss=5.9414e-01 ppl=1.81 best_loss=5.6297e-01 best_ppl=1.76
Epoch 39 - |param|=9.26e+02 |g_param|=1.56e+05 loss_x2y=2.0569e-01 ppl_x2y=1.23 loss_y2x=1.9935e-01 ppl_y2x=1.22 dual_loss=3.5709e-01
Validation X2Y - loss=6.4612e-01 ppl=1.91 best_loss=6.0827e-01 best_ppl=1.84                                            
Validation Y2X - loss=6.1802e-01 ppl=1.86 best_loss=5.6297e-01 best_ppl=1.76
Epoch 40 - |param|=9.27e+02 |g_param|=1.66e+05 loss_x2y=1.9882e-01 ppl_x2y=1.22 loss_y2x=2.0697e-01 ppl_y2x=1.23 dual_loss=3.4936e-01
Validation X2Y - loss=6.5158e-01 ppl=1.92 best_loss=6.0827e-01 best_ppl=1.84                                            
Validation Y2X - loss=5.9404e-01 ppl=1.81 best_loss=5.6297e-01 best_ppl=1.76

real	20m38.259s
user	20m14.162s
sys	0m24.053s

```

#### Warmup-Epoch 20, Total Epoch 50

```
Epoch 1 - |param|=9.11e+02 |g_param|=2.27e+05 loss_x2y=3.5584e+00 ppl_x2y=35.11 loss_y2x=3.5181e+00 ppl_y2x=33.72 dual_loss=0.0000e+00
Validation X2Y - loss=2.9389e+00 ppl=18.90 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=2.9440e+00 ppl=18.99 best_loss=inf best_ppl=inf
Epoch 2 - |param|=9.12e+02 |g_param|=2.07e+05 loss_x2y=2.4308e+00 ppl_x2y=11.37 loss_y2x=2.4211e+00 ppl_y2x=11.26 dual_loss=0.0000e+00
Validation X2Y - loss=1.9746e+00 ppl=7.20 best_loss=2.9389e+00 best_ppl=18.90                                           
Validation Y2X - loss=1.9743e+00 ppl=7.20 best_loss=2.9440e+00 best_ppl=18.99
Epoch 3 - |param|=9.12e+02 |g_param|=2.41e+05 loss_x2y=1.7251e+00 ppl_x2y=5.61 loss_y2x=1.7149e+00 ppl_y2x=5.56 dual_loss=0.0000e+00
Validation X2Y - loss=1.4908e+00 ppl=4.44 best_loss=1.9746e+00 best_ppl=7.20                                            
Validation Y2X - loss=1.4738e+00 ppl=4.37 best_loss=1.9743e+00 best_ppl=7.20
Epoch 4 - |param|=9.13e+02 |g_param|=2.47e+05 loss_x2y=1.3209e+00 ppl_x2y=3.75 loss_y2x=1.3614e+00 ppl_y2x=3.90 dual_loss=0.0000e+00
Validation X2Y - loss=1.1911e+00 ppl=3.29 best_loss=1.4908e+00 best_ppl=4.44                                            
Validation Y2X - loss=1.1818e+00 ppl=3.26 best_loss=1.4738e+00 best_ppl=4.37
Epoch 5 - |param|=9.13e+02 |g_param|=2.64e+05 loss_x2y=1.1159e+00 ppl_x2y=3.05 loss_y2x=1.1554e+00 ppl_y2x=3.18 dual_loss=0.0000e+00
Validation X2Y - loss=1.0119e+00 ppl=2.75 best_loss=1.1911e+00 best_ppl=3.29                                            
Validation Y2X - loss=1.0062e+00 ppl=2.74 best_loss=1.1818e+00 best_ppl=3.26
Epoch 6 - |param|=9.13e+02 |g_param|=2.41e+05 loss_x2y=9.4421e-01 ppl_x2y=2.57 loss_y2x=9.6344e-01 ppl_y2x=2.62 dual_loss=0.0000e+00
Validation X2Y - loss=9.0502e-01 ppl=2.47 best_loss=1.0119e+00 best_ppl=2.75                                            
Validation Y2X - loss=9.2085e-01 ppl=2.51 best_loss=1.0062e+00 best_ppl=2.74
Epoch 7 - |param|=9.14e+02 |g_param|=2.45e+05 loss_x2y=8.3527e-01 ppl_x2y=2.31 loss_y2x=8.5188e-01 ppl_y2x=2.34 dual_loss=0.0000e+00
Validation X2Y - loss=8.2814e-01 ppl=2.29 best_loss=9.0502e-01 best_ppl=2.47                                            
Validation Y2X - loss=8.1872e-01 ppl=2.27 best_loss=9.2085e-01 best_ppl=2.51
Epoch 8 - |param|=9.14e+02 |g_param|=2.44e+05 loss_x2y=7.2332e-01 ppl_x2y=2.06 loss_y2x=7.6175e-01 ppl_y2x=2.14 dual_loss=0.0000e+00
Validation X2Y - loss=8.0966e-01 ppl=2.25 best_loss=8.2814e-01 best_ppl=2.29                                            
Validation Y2X - loss=8.1291e-01 ppl=2.25 best_loss=8.1872e-01 best_ppl=2.27
Epoch 9 - |param|=9.14e+02 |g_param|=2.54e+05 loss_x2y=6.6974e-01 ppl_x2y=1.95 loss_y2x=6.7593e-01 ppl_y2x=1.97 dual_loss=0.0000e+00
Validation X2Y - loss=7.6443e-01 ppl=2.15 best_loss=8.0966e-01 best_ppl=2.25                                            
Validation Y2X - loss=7.2608e-01 ppl=2.07 best_loss=8.1291e-01 best_ppl=2.25
Epoch 10 - |param|=9.14e+02 |g_param|=2.68e+05 loss_x2y=6.5437e-01 ppl_x2y=1.92 loss_y2x=6.6845e-01 ppl_y2x=1.95 dual_loss=0.0000e+00
Validation X2Y - loss=7.5902e-01 ppl=2.14 best_loss=7.6443e-01 best_ppl=2.15                                            
Validation Y2X - loss=6.9329e-01 ppl=2.00 best_loss=7.2608e-01 best_ppl=2.07
Epoch 11 - |param|=9.15e+02 |g_param|=2.27e+05 loss_x2y=5.9575e-01 ppl_x2y=1.81 loss_y2x=6.0379e-01 ppl_y2x=1.83 dual_loss=0.0000e+00
Validation X2Y - loss=7.2549e-01 ppl=2.07 best_loss=7.5902e-01 best_ppl=2.14                                            
Validation Y2X - loss=6.4489e-01 ppl=1.91 best_loss=6.9329e-01 best_ppl=2.00
Epoch 12 - |param|=9.15e+02 |g_param|=2.32e+05 loss_x2y=5.4353e-01 ppl_x2y=1.72 loss_y2x=5.5721e-01 ppl_y2x=1.75 dual_loss=0.0000e+00
Validation X2Y - loss=6.9544e-01 ppl=2.00 best_loss=7.2549e-01 best_ppl=2.07                                            
Validation Y2X - loss=6.3803e-01 ppl=1.89 best_loss=6.4489e-01 best_ppl=1.91
Epoch 13 - |param|=9.15e+02 |g_param|=2.03e+05 loss_x2y=4.9157e-01 ppl_x2y=1.63 loss_y2x=5.0064e-01 ppl_y2x=1.65 dual_loss=0.0000e+00
Validation X2Y - loss=6.9451e-01 ppl=2.00 best_loss=6.9544e-01 best_ppl=2.00                                            
Validation Y2X - loss=6.2538e-01 ppl=1.87 best_loss=6.3803e-01 best_ppl=1.89
Epoch 14 - |param|=9.16e+02 |g_param|=2.09e+05 loss_x2y=4.6255e-01 ppl_x2y=1.59 loss_y2x=4.7511e-01 ppl_y2x=1.61 dual_loss=0.0000e+00
Validation X2Y - loss=6.7859e-01 ppl=1.97 best_loss=6.9451e-01 best_ppl=2.00                                            
Validation Y2X - loss=6.1738e-01 ppl=1.85 best_loss=6.2538e-01 best_ppl=1.87
Epoch 15 - |param|=9.16e+02 |g_param|=2.18e+05 loss_x2y=4.5687e-01 ppl_x2y=1.58 loss_y2x=4.5375e-01 ppl_y2x=1.57 dual_loss=0.0000e+00
Validation X2Y - loss=6.6979e-01 ppl=1.95 best_loss=6.7859e-01 best_ppl=1.97                                            
Validation Y2X - loss=6.2110e-01 ppl=1.86 best_loss=6.1738e-01 best_ppl=1.85
Epoch 16 - |param|=9.17e+02 |g_param|=1.86e+05 loss_x2y=4.0224e-01 ppl_x2y=1.50 loss_y2x=4.0621e-01 ppl_y2x=1.50 dual_loss=0.0000e+00
Validation X2Y - loss=6.7365e-01 ppl=1.96 best_loss=6.6979e-01 best_ppl=1.95                                            
Validation Y2X - loss=5.9730e-01 ppl=1.82 best_loss=6.1738e-01 best_ppl=1.85
Epoch 17 - |param|=9.17e+02 |g_param|=1.88e+05 loss_x2y=3.8073e-01 ppl_x2y=1.46 loss_y2x=3.8780e-01 ppl_y2x=1.47 dual_loss=0.0000e+00
Validation X2Y - loss=6.5245e-01 ppl=1.92 best_loss=6.6979e-01 best_ppl=1.95                                            
Validation Y2X - loss=6.1069e-01 ppl=1.84 best_loss=5.9730e-01 best_ppl=1.82
Epoch 18 - |param|=9.17e+02 |g_param|=2.07e+05 loss_x2y=3.6569e-01 ppl_x2y=1.44 loss_y2x=3.7298e-01 ppl_y2x=1.45 dual_loss=0.0000e+00
Validation X2Y - loss=6.4487e-01 ppl=1.91 best_loss=6.5245e-01 best_ppl=1.92                                            
Validation Y2X - loss=6.0807e-01 ppl=1.84 best_loss=5.9730e-01 best_ppl=1.82
Epoch 19 - |param|=9.18e+02 |g_param|=2.08e+05 loss_x2y=3.8042e-01 ppl_x2y=1.46 loss_y2x=3.7614e-01 ppl_y2x=1.46 dual_loss=0.0000e+00
Validation X2Y - loss=6.7201e-01 ppl=1.96 best_loss=6.4487e-01 best_ppl=1.91                                            
Validation Y2X - loss=5.8217e-01 ppl=1.79 best_loss=5.9730e-01 best_ppl=1.82
Epoch 20 - |param|=9.18e+02 |g_param|=2.07e+05 loss_x2y=3.4535e-01 ppl_x2y=1.41 loss_y2x=3.5652e-01 ppl_y2x=1.43 dual_loss=0.0000e+00
Validation X2Y - loss=6.6156e-01 ppl=1.94 best_loss=6.4487e-01 best_ppl=1.91                                            
Validation Y2X - loss=5.9045e-01 ppl=1.80 best_loss=5.8217e-01 best_ppl=1.79
Epoch 21 - |param|=9.19e+02 |g_param|=3.37e+05 loss_x2y=3.7457e-01 ppl_x2y=1.45 loss_y2x=3.6913e-01 ppl_y2x=1.45 dual_loss=4.7004e-01
Validation X2Y - loss=6.7403e-01 ppl=1.96 best_loss=6.4487e-01 best_ppl=1.91                                            
Validation Y2X - loss=6.1553e-01 ppl=1.85 best_loss=5.8217e-01 best_ppl=1.79
Epoch 22 - |param|=9.19e+02 |g_param|=3.67e+05 loss_x2y=3.3390e-01 ppl_x2y=1.40 loss_y2x=3.3939e-01 ppl_y2x=1.40 dual_loss=4.7117e-01
Validation X2Y - loss=6.4804e-01 ppl=1.91 best_loss=6.4487e-01 best_ppl=1.91                                            
Validation Y2X - loss=6.0576e-01 ppl=1.83 best_loss=5.8217e-01 best_ppl=1.79
Epoch 23 - |param|=9.19e+02 |g_param|=3.66e+05 loss_x2y=3.1628e-01 ppl_x2y=1.37 loss_y2x=3.3048e-01 ppl_y2x=1.39 dual_loss=4.6697e-01
Validation X2Y - loss=6.5907e-01 ppl=1.93 best_loss=6.4487e-01 best_ppl=1.91                                            
Validation Y2X - loss=6.1850e-01 ppl=1.86 best_loss=5.8217e-01 best_ppl=1.79
Epoch 24 - |param|=9.20e+02 |g_param|=3.89e+05 loss_x2y=3.1579e-01 ppl_x2y=1.37 loss_y2x=3.2800e-01 ppl_y2x=1.39 dual_loss=4.9197e-01
Validation X2Y - loss=6.6309e-01 ppl=1.94 best_loss=6.4487e-01 best_ppl=1.91                                            
Validation Y2X - loss=6.2432e-01 ppl=1.87 best_loss=5.8217e-01 best_ppl=1.79
Epoch 25 - |param|=9.20e+02 |g_param|=3.84e+05 loss_x2y=3.2114e-01 ppl_x2y=1.38 loss_y2x=3.2400e-01 ppl_y2x=1.38 dual_loss=4.4894e-01
Validation X2Y - loss=6.6487e-01 ppl=1.94 best_loss=6.4487e-01 best_ppl=1.91                                            
Validation Y2X - loss=5.9912e-01 ppl=1.82 best_loss=5.8217e-01 best_ppl=1.79
Epoch 26 - |param|=9.21e+02 |g_param|=3.77e+05 loss_x2y=2.9544e-01 ppl_x2y=1.34 loss_y2x=3.0012e-01 ppl_y2x=1.35 dual_loss=3.8776e-01
Validation X2Y - loss=6.7953e-01 ppl=1.97 best_loss=6.4487e-01 best_ppl=1.91                                            
Validation Y2X - loss=6.0266e-01 ppl=1.83 best_loss=5.8217e-01 best_ppl=1.79
Epoch 27 - |param|=9.21e+02 |g_param|=3.75e+05 loss_x2y=2.8565e-01 ppl_x2y=1.33 loss_y2x=2.9204e-01 ppl_y2x=1.34 dual_loss=3.5310e-01
Validation X2Y - loss=6.8239e-01 ppl=1.98 best_loss=6.4487e-01 best_ppl=1.91                                            
Validation Y2X - loss=5.7940e-01 ppl=1.78 best_loss=5.8217e-01 best_ppl=1.79
Epoch 28 - |param|=9.21e+02 |g_param|=3.87e+05 loss_x2y=2.6832e-01 ppl_x2y=1.31 loss_y2x=2.7403e-01 ppl_y2x=1.32 dual_loss=3.7641e-01
Validation X2Y - loss=6.7367e-01 ppl=1.96 best_loss=6.4487e-01 best_ppl=1.91                                            
Validation Y2X - loss=6.2437e-01 ppl=1.87 best_loss=5.7940e-01 best_ppl=1.78
Epoch 29 - |param|=9.22e+02 |g_param|=3.43e+05 loss_x2y=2.7240e-01 ppl_x2y=1.31 loss_y2x=2.6734e-01 ppl_y2x=1.31 dual_loss=3.4118e-01
Validation X2Y - loss=6.4441e-01 ppl=1.90 best_loss=6.4487e-01 best_ppl=1.91                                            
Validation Y2X - loss=5.8704e-01 ppl=1.80 best_loss=5.7940e-01 best_ppl=1.78
Epoch 30 - |param|=9.22e+02 |g_param|=3.67e+05 loss_x2y=2.6413e-01 ppl_x2y=1.30 loss_y2x=2.6321e-01 ppl_y2x=1.30 dual_loss=4.1747e-01
Validation X2Y - loss=6.4689e-01 ppl=1.91 best_loss=6.4441e-01 best_ppl=1.90                                            
Validation Y2X - loss=6.1134e-01 ppl=1.84 best_loss=5.7940e-01 best_ppl=1.78
Epoch 31 - |param|=9.23e+02 |g_param|=3.75e+05 loss_x2y=2.5443e-01 ppl_x2y=1.29 loss_y2x=2.6948e-01 ppl_y2x=1.31 dual_loss=4.1512e-01
Validation X2Y - loss=6.6083e-01 ppl=1.94 best_loss=6.4441e-01 best_ppl=1.90                                            
Validation Y2X - loss=5.9271e-01 ppl=1.81 best_loss=5.7940e-01 best_ppl=1.78
Epoch 32 - |param|=9.23e+02 |g_param|=3.64e+05 loss_x2y=2.5252e-01 ppl_x2y=1.29 loss_y2x=2.5654e-01 ppl_y2x=1.29 dual_loss=3.9978e-01
Validation X2Y - loss=6.3566e-01 ppl=1.89 best_loss=6.4441e-01 best_ppl=1.90                                            
Validation Y2X - loss=6.2014e-01 ppl=1.86 best_loss=5.7940e-01 best_ppl=1.78
Epoch 33 - |param|=9.23e+02 |g_param|=3.77e+05 loss_x2y=2.4612e-01 ppl_x2y=1.28 loss_y2x=2.4522e-01 ppl_y2x=1.28 dual_loss=3.7251e-01
Validation X2Y - loss=6.7263e-01 ppl=1.96 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1175e-01 ppl=1.84 best_loss=5.7940e-01 best_ppl=1.78
Epoch 34 - |param|=9.24e+02 |g_param|=3.60e+05 loss_x2y=2.3693e-01 ppl_x2y=1.27 loss_y2x=2.3912e-01 ppl_y2x=1.27 dual_loss=3.9401e-01
Validation X2Y - loss=6.7179e-01 ppl=1.96 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.8939e-01 ppl=1.80 best_loss=5.7940e-01 best_ppl=1.78
Epoch 35 - |param|=9.24e+02 |g_param|=3.76e+05 loss_x2y=2.4940e-01 ppl_x2y=1.28 loss_y2x=2.2800e-01 ppl_y2x=1.26 dual_loss=3.6339e-01
Validation X2Y - loss=7.0100e-01 ppl=2.02 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.2251e-01 ppl=1.86 best_loss=5.7940e-01 best_ppl=1.78
Epoch 36 - |param|=9.25e+02 |g_param|=3.36e+05 loss_x2y=2.2993e-01 ppl_x2y=1.26 loss_y2x=2.3273e-01 ppl_y2x=1.26 dual_loss=3.7384e-01
Validation X2Y - loss=6.7036e-01 ppl=1.95 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.7946e-01 ppl=1.79 best_loss=5.7940e-01 best_ppl=1.78
Epoch 37 - |param|=9.25e+02 |g_param|=3.28e+05 loss_x2y=2.2109e-01 ppl_x2y=1.25 loss_y2x=2.1867e-01 ppl_y2x=1.24 dual_loss=3.2571e-01
Validation X2Y - loss=6.6226e-01 ppl=1.94 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.2852e-01 ppl=1.87 best_loss=5.7940e-01 best_ppl=1.78
Epoch 38 - |param|=9.25e+02 |g_param|=3.16e+05 loss_x2y=2.1068e-01 ppl_x2y=1.23 loss_y2x=2.1413e-01 ppl_y2x=1.24 dual_loss=3.6731e-01
Validation X2Y - loss=6.9046e-01 ppl=1.99 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3200e-01 ppl=1.88 best_loss=5.7940e-01 best_ppl=1.78
Epoch 39 - |param|=9.26e+02 |g_param|=3.17e+05 loss_x2y=2.0618e-01 ppl_x2y=1.23 loss_y2x=2.0525e-01 ppl_y2x=1.23 dual_loss=3.4385e-01
Validation X2Y - loss=7.0370e-01 ppl=2.02 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1240e-01 ppl=1.84 best_loss=5.7940e-01 best_ppl=1.78
Epoch 40 - |param|=9.26e+02 |g_param|=3.40e+05 loss_x2y=2.0442e-01 ppl_x2y=1.23 loss_y2x=2.0715e-01 ppl_y2x=1.23 dual_loss=4.0565e-01
Validation X2Y - loss=6.7028e-01 ppl=1.95 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.2288e-01 ppl=1.86 best_loss=5.7940e-01 best_ppl=1.78
Epoch 41 - |param|=9.27e+02 |g_param|=4.54e+05 loss_x2y=2.0873e-01 ppl_x2y=1.23 loss_y2x=2.0530e-01 ppl_y2x=1.23 dual_loss=3.9132e-01
Validation X2Y - loss=6.9671e-01 ppl=2.01 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.2749e-01 ppl=1.87 best_loss=5.7940e-01 best_ppl=1.78
Epoch 42 - |param|=9.27e+02 |g_param|=6.87e+05 loss_x2y=2.1563e-01 ppl_x2y=1.24 loss_y2x=2.0546e-01 ppl_y2x=1.23 dual_loss=3.7751e-01
Validation X2Y - loss=6.8218e-01 ppl=1.98 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.2907e-01 ppl=1.88 best_loss=5.7940e-01 best_ppl=1.78
Epoch 43 - |param|=9.28e+02 |g_param|=6.74e+05 loss_x2y=1.9617e-01 ppl_x2y=1.22 loss_y2x=1.9579e-01 ppl_y2x=1.22 dual_loss=4.5275e-01
Validation X2Y - loss=7.0040e-01 ppl=2.01 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.0727e-01 ppl=1.84 best_loss=5.7940e-01 best_ppl=1.78
Epoch 44 - |param|=9.28e+02 |g_param|=6.34e+05 loss_x2y=1.8618e-01 ppl_x2y=1.20 loss_y2x=1.8230e-01 ppl_y2x=1.20 dual_loss=3.1042e-01
Validation X2Y - loss=7.0444e-01 ppl=2.02 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1417e-01 ppl=1.85 best_loss=5.7940e-01 best_ppl=1.78
Epoch 45 - |param|=9.28e+02 |g_param|=6.46e+05 loss_x2y=1.8861e-01 ppl_x2y=1.21 loss_y2x=1.8130e-01 ppl_y2x=1.20 dual_loss=4.0849e-01
Validation X2Y - loss=7.1030e-01 ppl=2.03 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.0872e-01 ppl=1.84 best_loss=5.7940e-01 best_ppl=1.78
Epoch 46 - |param|=9.29e+02 |g_param|=6.10e+05 loss_x2y=1.7740e-01 ppl_x2y=1.19 loss_y2x=1.7582e-01 ppl_y2x=1.19 dual_loss=3.2835e-01
Validation X2Y - loss=6.9709e-01 ppl=2.01 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1800e-01 ppl=1.86 best_loss=5.7940e-01 best_ppl=1.78
Epoch 47 - |param|=9.29e+02 |g_param|=5.03e+05 loss_x2y=1.7778e-01 ppl_x2y=1.19 loss_y2x=1.7373e-01 ppl_y2x=1.19 dual_loss=3.3475e-01
Validation X2Y - loss=6.9671e-01 ppl=2.01 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3420e-01 ppl=1.89 best_loss=5.7940e-01 best_ppl=1.78
Epoch 48 - |param|=9.30e+02 |g_param|=4.89e+05 loss_x2y=1.7188e-01 ppl_x2y=1.19 loss_y2x=1.7682e-01 ppl_y2x=1.19 dual_loss=3.9114e-01
Validation X2Y - loss=6.9890e-01 ppl=2.01 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3571e-01 ppl=1.89 best_loss=5.7940e-01 best_ppl=1.78
Epoch 49 - |param|=9.30e+02 |g_param|=5.06e+05 loss_x2y=1.6977e-01 ppl_x2y=1.19 loss_y2x=1.6188e-01 ppl_y2x=1.18 dual_loss=3.4668e-01
Validation X2Y - loss=7.1490e-01 ppl=2.04 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.5706e-01 ppl=1.93 best_loss=5.7940e-01 best_ppl=1.78
Epoch 50 - |param|=9.30e+02 |g_param|=4.40e+05 loss_x2y=1.6728e-01 ppl_x2y=1.18 loss_y2x=1.6903e-01 ppl_y2x=1.18 dual_loss=3.2497e-01
Validation X2Y - loss=7.1814e-01 ppl=2.05 best_loss=6.3566e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4335e-01 ppl=1.90 best_loss=5.7940e-01 best_ppl=1.78

real	25m57.088s
user	25m29.788s
sys	0m27.334s
```

#### Warmup-Epoch 20, Total Epoch 60

```
Epoch 1 - |param|=9.12e+02 |g_param|=1.52e+05 loss_x2y=3.5075e+00 ppl_x2y=33.36 loss_y2x=3.5412e+00 ppl_y2x=34.51 dual_loss=0.0000e+00
Validation X2Y - loss=2.9524e+00 ppl=19.15 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=2.9277e+00 ppl=18.68 best_loss=inf best_ppl=inf
Epoch 2 - |param|=9.13e+02 |g_param|=1.83e+05 loss_x2y=2.3422e+00 ppl_x2y=10.40 loss_y2x=2.3741e+00 ppl_y2x=10.74 dual_loss=0.0000e+00
Validation X2Y - loss=1.9678e+00 ppl=7.15 best_loss=2.9524e+00 best_ppl=19.15                                           
Validation Y2X - loss=1.9658e+00 ppl=7.14 best_loss=2.9277e+00 best_ppl=18.68
Epoch 3 - |param|=9.13e+02 |g_param|=2.25e+05 loss_x2y=1.7174e+00 ppl_x2y=5.57 loss_y2x=1.7335e+00 ppl_y2x=5.66 dual_loss=0.0000e+00
Validation X2Y - loss=1.4173e+00 ppl=4.13 best_loss=1.9678e+00 best_ppl=7.15                                            
Validation Y2X - loss=1.4542e+00 ppl=4.28 best_loss=1.9658e+00 best_ppl=7.14
Epoch 4 - |param|=9.14e+02 |g_param|=2.33e+05 loss_x2y=1.3371e+00 ppl_x2y=3.81 loss_y2x=1.3270e+00 ppl_y2x=3.77 dual_loss=0.0000e+00
Validation X2Y - loss=1.1659e+00 ppl=3.21 best_loss=1.4173e+00 best_ppl=4.13                                            
Validation Y2X - loss=1.1049e+00 ppl=3.02 best_loss=1.4542e+00 best_ppl=4.28
Epoch 5 - |param|=9.14e+02 |g_param|=2.27e+05 loss_x2y=1.0557e+00 ppl_x2y=2.87 loss_y2x=1.0520e+00 ppl_y2x=2.86 dual_loss=0.0000e+00
Validation X2Y - loss=9.5842e-01 ppl=2.61 best_loss=1.1659e+00 best_ppl=3.21                                            
Validation Y2X - loss=9.2226e-01 ppl=2.51 best_loss=1.1049e+00 best_ppl=3.02
Epoch 6 - |param|=9.14e+02 |g_param|=2.33e+05 loss_x2y=8.8158e-01 ppl_x2y=2.41 loss_y2x=8.9898e-01 ppl_y2x=2.46 dual_loss=0.0000e+00
Validation X2Y - loss=8.6200e-01 ppl=2.37 best_loss=9.5842e-01 best_ppl=2.61                                            
Validation Y2X - loss=8.5430e-01 ppl=2.35 best_loss=9.2226e-01 best_ppl=2.51
Epoch 7 - |param|=9.15e+02 |g_param|=2.37e+05 loss_x2y=8.2291e-01 ppl_x2y=2.28 loss_y2x=8.1845e-01 ppl_y2x=2.27 dual_loss=0.0000e+00
Validation X2Y - loss=7.9619e-01 ppl=2.22 best_loss=8.6200e-01 best_ppl=2.37                                            
Validation Y2X - loss=7.8413e-01 ppl=2.19 best_loss=8.5430e-01 best_ppl=2.35
Epoch 8 - |param|=9.15e+02 |g_param|=2.31e+05 loss_x2y=7.0384e-01 ppl_x2y=2.02 loss_y2x=7.1432e-01 ppl_y2x=2.04 dual_loss=0.0000e+00
Validation X2Y - loss=7.5530e-01 ppl=2.13 best_loss=7.9619e-01 best_ppl=2.22                                            
Validation Y2X - loss=7.3328e-01 ppl=2.08 best_loss=7.8413e-01 best_ppl=2.19
Epoch 9 - |param|=9.15e+02 |g_param|=2.14e+05 loss_x2y=6.6222e-01 ppl_x2y=1.94 loss_y2x=6.5773e-01 ppl_y2x=1.93 dual_loss=0.0000e+00
Validation X2Y - loss=7.4133e-01 ppl=2.10 best_loss=7.5530e-01 best_ppl=2.13                                            
Validation Y2X - loss=7.0051e-01 ppl=2.01 best_loss=7.3328e-01 best_ppl=2.08
Epoch 10 - |param|=9.15e+02 |g_param|=2.18e+05 loss_x2y=6.1285e-01 ppl_x2y=1.85 loss_y2x=6.1921e-01 ppl_y2x=1.86 dual_loss=0.0000e+00
Validation X2Y - loss=7.1204e-01 ppl=2.04 best_loss=7.4133e-01 best_ppl=2.10                                            
Validation Y2X - loss=7.0472e-01 ppl=2.02 best_loss=7.0051e-01 best_ppl=2.01
Epoch 11 - |param|=9.16e+02 |g_param|=2.19e+05 loss_x2y=5.7513e-01 ppl_x2y=1.78 loss_y2x=5.9512e-01 ppl_y2x=1.81 dual_loss=0.0000e+00
Validation X2Y - loss=7.0334e-01 ppl=2.02 best_loss=7.1204e-01 best_ppl=2.04                                            
Validation Y2X - loss=6.4016e-01 ppl=1.90 best_loss=7.0051e-01 best_ppl=2.01
Epoch 12 - |param|=9.16e+02 |g_param|=1.92e+05 loss_x2y=4.8552e-01 ppl_x2y=1.63 loss_y2x=4.9550e-01 ppl_y2x=1.64 dual_loss=0.0000e+00
Validation X2Y - loss=6.9677e-01 ppl=2.01 best_loss=7.0334e-01 best_ppl=2.02                                            
Validation Y2X - loss=6.1809e-01 ppl=1.86 best_loss=6.4016e-01 best_ppl=1.90
Epoch 13 - |param|=9.16e+02 |g_param|=2.35e+05 loss_x2y=4.8316e-01 ppl_x2y=1.62 loss_y2x=4.9817e-01 ppl_y2x=1.65 dual_loss=0.0000e+00
Validation X2Y - loss=6.7915e-01 ppl=1.97 best_loss=6.9677e-01 best_ppl=2.01                                            
Validation Y2X - loss=7.1930e-01 ppl=2.05 best_loss=6.1809e-01 best_ppl=1.86
Epoch 14 - |param|=9.17e+02 |g_param|=2.11e+05 loss_x2y=4.6553e-01 ppl_x2y=1.59 loss_y2x=4.5160e-01 ppl_y2x=1.57 dual_loss=0.0000e+00
Validation X2Y - loss=6.8910e-01 ppl=1.99 best_loss=6.7915e-01 best_ppl=1.97                                            
Validation Y2X - loss=6.1545e-01 ppl=1.85 best_loss=6.1809e-01 best_ppl=1.86
Epoch 15 - |param|=9.17e+02 |g_param|=2.39e+05 loss_x2y=4.4577e-01 ppl_x2y=1.56 loss_y2x=4.6744e-01 ppl_y2x=1.60 dual_loss=0.0000e+00
Validation X2Y - loss=6.9731e-01 ppl=2.01 best_loss=6.7915e-01 best_ppl=1.97                                            
Validation Y2X - loss=6.1386e-01 ppl=1.85 best_loss=6.1545e-01 best_ppl=1.85
Epoch 16 - |param|=9.18e+02 |g_param|=2.01e+05 loss_x2y=4.1582e-01 ppl_x2y=1.52 loss_y2x=4.1449e-01 ppl_y2x=1.51 dual_loss=0.0000e+00
Validation X2Y - loss=6.6260e-01 ppl=1.94 best_loss=6.7915e-01 best_ppl=1.97                                            
Validation Y2X - loss=6.1970e-01 ppl=1.86 best_loss=6.1386e-01 best_ppl=1.85
Epoch 17 - |param|=9.18e+02 |g_param|=1.83e+05 loss_x2y=3.8111e-01 ppl_x2y=1.46 loss_y2x=3.8876e-01 ppl_y2x=1.48 dual_loss=0.0000e+00
Validation X2Y - loss=6.6687e-01 ppl=1.95 best_loss=6.6260e-01 best_ppl=1.94                                            
Validation Y2X - loss=6.3226e-01 ppl=1.88 best_loss=6.1386e-01 best_ppl=1.85
Epoch 18 - |param|=9.18e+02 |g_param|=1.98e+05 loss_x2y=3.9050e-01 ppl_x2y=1.48 loss_y2x=3.8449e-01 ppl_y2x=1.47 dual_loss=0.0000e+00
Validation X2Y - loss=6.7365e-01 ppl=1.96 best_loss=6.6260e-01 best_ppl=1.94                                            
Validation Y2X - loss=5.9804e-01 ppl=1.82 best_loss=6.1386e-01 best_ppl=1.85
Epoch 19 - |param|=9.19e+02 |g_param|=1.78e+05 loss_x2y=3.3642e-01 ppl_x2y=1.40 loss_y2x=3.3327e-01 ppl_y2x=1.40 dual_loss=0.0000e+00
Validation X2Y - loss=6.5772e-01 ppl=1.93 best_loss=6.6260e-01 best_ppl=1.94                                            
Validation Y2X - loss=5.9978e-01 ppl=1.82 best_loss=5.9804e-01 best_ppl=1.82
Epoch 20 - |param|=9.19e+02 |g_param|=1.98e+05 loss_x2y=3.4979e-01 ppl_x2y=1.42 loss_y2x=3.5683e-01 ppl_y2x=1.43 dual_loss=0.0000e+00
Validation X2Y - loss=6.6222e-01 ppl=1.94 best_loss=6.5772e-01 best_ppl=1.93                                            
Validation Y2X - loss=5.8272e-01 ppl=1.79 best_loss=5.9804e-01 best_ppl=1.82
Epoch 21 - |param|=9.20e+02 |g_param|=3.80e+05 loss_x2y=3.3110e-01 ppl_x2y=1.39 loss_y2x=3.5479e-01 ppl_y2x=1.43 dual_loss=5.7498e-01
Validation X2Y - loss=6.4014e-01 ppl=1.90 best_loss=6.5772e-01 best_ppl=1.93                                            
Validation Y2X - loss=5.9792e-01 ppl=1.82 best_loss=5.8272e-01 best_ppl=1.79
Epoch 22 - |param|=9.20e+02 |g_param|=2.92e+05 loss_x2y=3.4395e-01 ppl_x2y=1.41 loss_y2x=3.4625e-01 ppl_y2x=1.41 dual_loss=4.5372e-01
Validation X2Y - loss=6.3592e-01 ppl=1.89 best_loss=6.4014e-01 best_ppl=1.90                                            
Validation Y2X - loss=5.6604e-01 ppl=1.76 best_loss=5.8272e-01 best_ppl=1.79
Epoch 23 - |param|=9.20e+02 |g_param|=2.94e+05 loss_x2y=3.3408e-01 ppl_x2y=1.40 loss_y2x=3.3418e-01 ppl_y2x=1.40 dual_loss=3.6396e-01
Validation X2Y - loss=6.5939e-01 ppl=1.93 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.7659e-01 ppl=1.78 best_loss=5.6604e-01 best_ppl=1.76
Epoch 24 - |param|=9.21e+02 |g_param|=2.69e+05 loss_x2y=3.0972e-01 ppl_x2y=1.36 loss_y2x=3.1794e-01 ppl_y2x=1.37 dual_loss=4.4751e-01
Validation X2Y - loss=6.5965e-01 ppl=1.93 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.8426e-01 ppl=1.79 best_loss=5.6604e-01 best_ppl=1.76
Epoch 25 - |param|=9.21e+02 |g_param|=2.72e+05 loss_x2y=2.9493e-01 ppl_x2y=1.34 loss_y2x=3.0152e-01 ppl_y2x=1.35 dual_loss=3.9002e-01
Validation X2Y - loss=6.5037e-01 ppl=1.92 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.7426e-01 ppl=1.78 best_loss=5.6604e-01 best_ppl=1.76
Epoch 26 - |param|=9.22e+02 |g_param|=2.74e+05 loss_x2y=2.8802e-01 ppl_x2y=1.33 loss_y2x=2.9223e-01 ppl_y2x=1.34 dual_loss=3.7656e-01
Validation X2Y - loss=6.6474e-01 ppl=1.94 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.8898e-01 ppl=1.80 best_loss=5.6604e-01 best_ppl=1.76
Epoch 27 - |param|=9.22e+02 |g_param|=2.69e+05 loss_x2y=2.8374e-01 ppl_x2y=1.33 loss_y2x=2.9458e-01 ppl_y2x=1.34 dual_loss=4.0268e-01
Validation X2Y - loss=6.5584e-01 ppl=1.93 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9168e-01 ppl=1.81 best_loss=5.6604e-01 best_ppl=1.76
Epoch 28 - |param|=9.22e+02 |g_param|=2.78e+05 loss_x2y=2.7897e-01 ppl_x2y=1.32 loss_y2x=2.9095e-01 ppl_y2x=1.34 dual_loss=4.1601e-01
Validation X2Y - loss=6.6587e-01 ppl=1.95 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3695e-01 ppl=1.89 best_loss=5.6604e-01 best_ppl=1.76
Epoch 29 - |param|=9.23e+02 |g_param|=2.85e+05 loss_x2y=2.7120e-01 ppl_x2y=1.31 loss_y2x=2.6520e-01 ppl_y2x=1.30 dual_loss=3.5427e-01
Validation X2Y - loss=6.6486e-01 ppl=1.94 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9542e-01 ppl=1.81 best_loss=5.6604e-01 best_ppl=1.76
Epoch 30 - |param|=9.23e+02 |g_param|=2.39e+05 loss_x2y=2.5067e-01 ppl_x2y=1.28 loss_y2x=2.5370e-01 ppl_y2x=1.29 dual_loss=3.7586e-01
Validation X2Y - loss=6.5705e-01 ppl=1.93 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9406e-01 ppl=1.81 best_loss=5.6604e-01 best_ppl=1.76
Epoch 31 - |param|=9.24e+02 |g_param|=2.69e+05 loss_x2y=2.4436e-01 ppl_x2y=1.28 loss_y2x=2.6394e-01 ppl_y2x=1.30 dual_loss=4.3589e-01
Validation X2Y - loss=6.7581e-01 ppl=1.97 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.5465e-01 ppl=1.92 best_loss=5.6604e-01 best_ppl=1.76
Epoch 32 - |param|=9.24e+02 |g_param|=2.54e+05 loss_x2y=2.4039e-01 ppl_x2y=1.27 loss_y2x=2.4247e-01 ppl_y2x=1.27 dual_loss=3.6025e-01
Validation X2Y - loss=6.7024e-01 ppl=1.95 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.0773e-01 ppl=1.84 best_loss=5.6604e-01 best_ppl=1.76
Epoch 33 - |param|=9.24e+02 |g_param|=2.64e+05 loss_x2y=2.4881e-01 ppl_x2y=1.28 loss_y2x=2.4246e-01 ppl_y2x=1.27 dual_loss=3.5953e-01
Validation X2Y - loss=6.6528e-01 ppl=1.95 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4293e-01 ppl=1.90 best_loss=5.6604e-01 best_ppl=1.76
Epoch 34 - |param|=9.25e+02 |g_param|=2.67e+05 loss_x2y=2.3648e-01 ppl_x2y=1.27 loss_y2x=2.3475e-01 ppl_y2x=1.26 dual_loss=3.6205e-01
Validation X2Y - loss=6.7568e-01 ppl=1.97 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1593e-01 ppl=1.85 best_loss=5.6604e-01 best_ppl=1.76
Epoch 35 - |param|=9.25e+02 |g_param|=2.46e+05 loss_x2y=2.2496e-01 ppl_x2y=1.25 loss_y2x=2.2898e-01 ppl_y2x=1.26 dual_loss=3.5154e-01
Validation X2Y - loss=7.0751e-01 ppl=2.03 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.0833e-01 ppl=1.84 best_loss=5.6604e-01 best_ppl=1.76
Epoch 36 - |param|=9.26e+02 |g_param|=2.54e+05 loss_x2y=2.2215e-01 ppl_x2y=1.25 loss_y2x=2.3286e-01 ppl_y2x=1.26 dual_loss=4.2313e-01
Validation X2Y - loss=6.5985e-01 ppl=1.93 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.2313e-01 ppl=1.86 best_loss=5.6604e-01 best_ppl=1.76
Epoch 37 - |param|=9.26e+02 |g_param|=2.39e+05 loss_x2y=2.1328e-01 ppl_x2y=1.24 loss_y2x=2.2152e-01 ppl_y2x=1.25 dual_loss=3.7104e-01
Validation X2Y - loss=6.7929e-01 ppl=1.97 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.0845e-01 ppl=1.84 best_loss=5.6604e-01 best_ppl=1.76
Epoch 38 - |param|=9.26e+02 |g_param|=2.26e+05 loss_x2y=1.9910e-01 ppl_x2y=1.22 loss_y2x=2.0291e-01 ppl_y2x=1.22 dual_loss=3.1675e-01
Validation X2Y - loss=6.7283e-01 ppl=1.96 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1784e-01 ppl=1.85 best_loss=5.6604e-01 best_ppl=1.76
Epoch 39 - |param|=9.27e+02 |g_param|=2.53e+05 loss_x2y=2.1326e-01 ppl_x2y=1.24 loss_y2x=2.0911e-01 ppl_y2x=1.23 dual_loss=3.6421e-01
Validation X2Y - loss=6.7262e-01 ppl=1.96 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3123e-01 ppl=1.88 best_loss=5.6604e-01 best_ppl=1.76
Epoch 40 - |param|=9.27e+02 |g_param|=2.44e+05 loss_x2y=1.9995e-01 ppl_x2y=1.22 loss_y2x=2.0368e-01 ppl_y2x=1.23 dual_loss=3.5537e-01
Validation X2Y - loss=6.7871e-01 ppl=1.97 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3624e-01 ppl=1.89 best_loss=5.6604e-01 best_ppl=1.76
Epoch 41 - |param|=9.28e+02 |g_param|=3.88e+05 loss_x2y=1.8806e-01 ppl_x2y=1.21 loss_y2x=1.9169e-01 ppl_y2x=1.21 dual_loss=3.6578e-01
Validation X2Y - loss=7.0402e-01 ppl=2.02 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.2834e-01 ppl=1.87 best_loss=5.6604e-01 best_ppl=1.76
Epoch 42 - |param|=9.28e+02 |g_param|=3.66e+05 loss_x2y=1.9836e-01 ppl_x2y=1.22 loss_y2x=1.9654e-01 ppl_y2x=1.22 dual_loss=4.0645e-01
Validation X2Y - loss=7.0259e-01 ppl=2.02 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.2585e-01 ppl=1.87 best_loss=5.6604e-01 best_ppl=1.76
Epoch 43 - |param|=9.29e+02 |g_param|=3.52e+05 loss_x2y=1.9869e-01 ppl_x2y=1.22 loss_y2x=2.1190e-01 ppl_y2x=1.24 dual_loss=4.4988e-01
Validation X2Y - loss=7.1428e-01 ppl=2.04 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4291e-01 ppl=1.90 best_loss=5.6604e-01 best_ppl=1.76
Epoch 44 - |param|=9.29e+02 |g_param|=3.23e+05 loss_x2y=1.8752e-01 ppl_x2y=1.21 loss_y2x=1.8798e-01 ppl_y2x=1.21 dual_loss=3.7245e-01
Validation X2Y - loss=6.8212e-01 ppl=1.98 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.2027e-01 ppl=1.86 best_loss=5.6604e-01 best_ppl=1.76
Epoch 45 - |param|=9.29e+02 |g_param|=3.23e+05 loss_x2y=1.8479e-01 ppl_x2y=1.20 loss_y2x=1.8395e-01 ppl_y2x=1.20 dual_loss=3.3032e-01
Validation X2Y - loss=6.8486e-01 ppl=1.98 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1507e-01 ppl=1.85 best_loss=5.6604e-01 best_ppl=1.76
Epoch 46 - |param|=9.30e+02 |g_param|=3.23e+05 loss_x2y=1.7938e-01 ppl_x2y=1.20 loss_y2x=1.8571e-01 ppl_y2x=1.20 dual_loss=3.7950e-01
Validation X2Y - loss=7.1116e-01 ppl=2.04 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.5746e-01 ppl=1.93 best_loss=5.6604e-01 best_ppl=1.76
Epoch 47 - |param|=9.30e+02 |g_param|=3.06e+05 loss_x2y=1.8242e-01 ppl_x2y=1.20 loss_y2x=1.8450e-01 ppl_y2x=1.20 dual_loss=3.9241e-01
Validation X2Y - loss=6.9502e-01 ppl=2.00 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3853e-01 ppl=1.89 best_loss=5.6604e-01 best_ppl=1.76
Epoch 48 - |param|=9.31e+02 |g_param|=3.44e+05 loss_x2y=1.7499e-01 ppl_x2y=1.19 loss_y2x=1.7489e-01 ppl_y2x=1.19 dual_loss=4.4606e-01
Validation X2Y - loss=7.1490e-01 ppl=2.04 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.5736e-01 ppl=1.93 best_loss=5.6604e-01 best_ppl=1.76
Epoch 49 - |param|=9.31e+02 |g_param|=3.25e+05 loss_x2y=1.7635e-01 ppl_x2y=1.19 loss_y2x=1.8183e-01 ppl_y2x=1.20 dual_loss=4.2319e-01
Validation X2Y - loss=6.9953e-01 ppl=2.01 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4236e-01 ppl=1.90 best_loss=5.6604e-01 best_ppl=1.76
Epoch 50 - |param|=9.31e+02 |g_param|=3.06e+05 loss_x2y=1.6234e-01 ppl_x2y=1.18 loss_y2x=1.7066e-01 ppl_y2x=1.19 dual_loss=3.4451e-01
Validation X2Y - loss=7.2026e-01 ppl=2.05 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4272e-01 ppl=1.90 best_loss=5.6604e-01 best_ppl=1.76
Epoch 51 - |param|=9.32e+02 |g_param|=2.84e+05 loss_x2y=1.6097e-01 ppl_x2y=1.17 loss_y2x=1.6076e-01 ppl_y2x=1.17 dual_loss=3.2281e-01
Validation X2Y - loss=7.1590e-01 ppl=2.05 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.7539e-01 ppl=1.96 best_loss=5.6604e-01 best_ppl=1.76
Epoch 52 - |param|=9.32e+02 |g_param|=3.51e+05 loss_x2y=1.6750e-01 ppl_x2y=1.18 loss_y2x=1.7155e-01 ppl_y2x=1.19 dual_loss=4.3814e-01
Validation X2Y - loss=7.0606e-01 ppl=2.03 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4797e-01 ppl=1.91 best_loss=5.6604e-01 best_ppl=1.76
Epoch 53 - |param|=9.33e+02 |g_param|=2.93e+05 loss_x2y=1.6029e-01 ppl_x2y=1.17 loss_y2x=1.5699e-01 ppl_y2x=1.17 dual_loss=3.4823e-01
Validation X2Y - loss=7.1809e-01 ppl=2.05 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4163e-01 ppl=1.90 best_loss=5.6604e-01 best_ppl=1.76
Epoch 54 - |param|=9.33e+02 |g_param|=3.14e+05 loss_x2y=1.5645e-01 ppl_x2y=1.17 loss_y2x=1.5776e-01 ppl_y2x=1.17 dual_loss=4.0498e-01
Validation X2Y - loss=7.1184e-01 ppl=2.04 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4852e-01 ppl=1.91 best_loss=5.6604e-01 best_ppl=1.76
Epoch 55 - |param|=9.33e+02 |g_param|=3.21e+05 loss_x2y=1.6434e-01 ppl_x2y=1.18 loss_y2x=1.6466e-01 ppl_y2x=1.18 dual_loss=4.1793e-01
Validation X2Y - loss=6.9261e-01 ppl=2.00 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1806e-01 ppl=1.86 best_loss=5.6604e-01 best_ppl=1.76
Epoch 56 - |param|=9.34e+02 |g_param|=3.10e+05 loss_x2y=1.5553e-01 ppl_x2y=1.17 loss_y2x=1.6205e-01 ppl_y2x=1.18 dual_loss=3.8273e-01
Validation X2Y - loss=7.3107e-01 ppl=2.08 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4986e-01 ppl=1.92 best_loss=5.6604e-01 best_ppl=1.76
Epoch 57 - |param|=9.34e+02 |g_param|=3.15e+05 loss_x2y=1.4973e-01 ppl_x2y=1.16 loss_y2x=1.5236e-01 ppl_y2x=1.16 dual_loss=3.9368e-01
Validation X2Y - loss=7.1636e-01 ppl=2.05 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4560e-01 ppl=1.91 best_loss=5.6604e-01 best_ppl=1.76
Epoch 58 - |param|=9.35e+02 |g_param|=3.02e+05 loss_x2y=1.4821e-01 ppl_x2y=1.16 loss_y2x=1.4898e-01 ppl_y2x=1.16 dual_loss=3.8377e-01
Validation X2Y - loss=7.1339e-01 ppl=2.04 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4139e-01 ppl=1.90 best_loss=5.6604e-01 best_ppl=1.76
Epoch 59 - |param|=9.35e+02 |g_param|=2.92e+05 loss_x2y=1.4811e-01 ppl_x2y=1.16 loss_y2x=1.5037e-01 ppl_y2x=1.16 dual_loss=3.7209e-01
Validation X2Y - loss=7.6558e-01 ppl=2.15 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3913e-01 ppl=1.89 best_loss=5.6604e-01 best_ppl=1.76
Epoch 60 - |param|=9.35e+02 |g_param|=3.20e+05 loss_x2y=1.4363e-01 ppl_x2y=1.15 loss_y2x=1.4391e-01 ppl_y2x=1.15 dual_loss=4.5823e-01
Validation X2Y - loss=7.4009e-01 ppl=2.10 best_loss=6.3592e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3821e-01 ppl=1.89 best_loss=5.6604e-01 best_ppl=1.76

real	31m12.314s
user	30m38.657s
sys	0m32.034s
```

#### Warmup-Epoch 20, Total Epoch 70

```
Epoch 1 - |param|=9.10e+02 |g_param|=1.66e+05 loss_x2y=3.4702e+00 ppl_x2y=32.14 loss_y2x=3.4493e+00 ppl_y2x=31.48 dual_loss=0.0000e+00
Validation X2Y - loss=2.9385e+00 ppl=18.89 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=2.8693e+00 ppl=17.63 best_loss=inf best_ppl=inf
Epoch 2 - |param|=9.11e+02 |g_param|=2.16e+05 loss_x2y=2.3892e+00 ppl_x2y=10.90 loss_y2x=2.3360e+00 ppl_y2x=10.34 dual_loss=0.0000e+00
Validation X2Y - loss=2.0973e+00 ppl=8.14 best_loss=2.9385e+00 best_ppl=18.89                                           
Validation Y2X - loss=1.9707e+00 ppl=7.18 best_loss=2.8693e+00 best_ppl=17.63
Epoch 3 - |param|=9.12e+02 |g_param|=2.47e+05 loss_x2y=1.8116e+00 ppl_x2y=6.12 loss_y2x=1.7629e+00 ppl_y2x=5.83 dual_loss=0.0000e+00
Validation X2Y - loss=1.5158e+00 ppl=4.55 best_loss=2.0973e+00 best_ppl=8.14                                            
Validation Y2X - loss=1.4712e+00 ppl=4.35 best_loss=1.9707e+00 best_ppl=7.18
Epoch 4 - |param|=9.12e+02 |g_param|=2.46e+05 loss_x2y=1.3297e+00 ppl_x2y=3.78 loss_y2x=1.3096e+00 ppl_y2x=3.70 dual_loss=0.0000e+00
Validation X2Y - loss=1.1892e+00 ppl=3.28 best_loss=1.5158e+00 best_ppl=4.55                                            
Validation Y2X - loss=1.1408e+00 ppl=3.13 best_loss=1.4712e+00 best_ppl=4.35
Epoch 5 - |param|=9.12e+02 |g_param|=2.54e+05 loss_x2y=1.0978e+00 ppl_x2y=3.00 loss_y2x=1.0853e+00 ppl_y2x=2.96 dual_loss=0.0000e+00
Validation X2Y - loss=1.0005e+00 ppl=2.72 best_loss=1.1892e+00 best_ppl=3.28                                            
Validation Y2X - loss=9.7306e-01 ppl=2.65 best_loss=1.1408e+00 best_ppl=3.13
Epoch 6 - |param|=9.13e+02 |g_param|=2.39e+05 loss_x2y=9.7808e-01 ppl_x2y=2.66 loss_y2x=9.4034e-01 ppl_y2x=2.56 dual_loss=0.0000e+00
Validation X2Y - loss=8.6696e-01 ppl=2.38 best_loss=1.0005e+00 best_ppl=2.72                                            
Validation Y2X - loss=8.6168e-01 ppl=2.37 best_loss=9.7306e-01 best_ppl=2.65
Epoch 7 - |param|=9.13e+02 |g_param|=2.32e+05 loss_x2y=8.5394e-01 ppl_x2y=2.35 loss_y2x=8.4187e-01 ppl_y2x=2.32 dual_loss=0.0000e+00
Validation X2Y - loss=8.2426e-01 ppl=2.28 best_loss=8.6696e-01 best_ppl=2.38                                            
Validation Y2X - loss=7.7127e-01 ppl=2.16 best_loss=8.6168e-01 best_ppl=2.37
Epoch 8 - |param|=9.13e+02 |g_param|=2.37e+05 loss_x2y=7.1960e-01 ppl_x2y=2.05 loss_y2x=7.0287e-01 ppl_y2x=2.02 dual_loss=0.0000e+00
Validation X2Y - loss=7.6364e-01 ppl=2.15 best_loss=8.2426e-01 best_ppl=2.28                                            
Validation Y2X - loss=7.6218e-01 ppl=2.14 best_loss=7.7127e-01 best_ppl=2.16
Epoch 9 - |param|=9.13e+02 |g_param|=2.22e+05 loss_x2y=6.5547e-01 ppl_x2y=1.93 loss_y2x=6.4445e-01 ppl_y2x=1.90 dual_loss=0.0000e+00
Validation X2Y - loss=7.6188e-01 ppl=2.14 best_loss=7.6364e-01 best_ppl=2.15                                            
Validation Y2X - loss=6.9602e-01 ppl=2.01 best_loss=7.6218e-01 best_ppl=2.14
Epoch 10 - |param|=9.14e+02 |g_param|=2.46e+05 loss_x2y=6.2983e-01 ppl_x2y=1.88 loss_y2x=6.3873e-01 ppl_y2x=1.89 dual_loss=0.0000e+00
Validation X2Y - loss=7.1205e-01 ppl=2.04 best_loss=7.6188e-01 best_ppl=2.14                                            
Validation Y2X - loss=6.5254e-01 ppl=1.92 best_loss=6.9602e-01 best_ppl=2.01
Epoch 11 - |param|=9.14e+02 |g_param|=2.32e+05 loss_x2y=5.7695e-01 ppl_x2y=1.78 loss_y2x=5.6466e-01 ppl_y2x=1.76 dual_loss=0.0000e+00
Validation X2Y - loss=6.9699e-01 ppl=2.01 best_loss=7.1205e-01 best_ppl=2.04                                            
Validation Y2X - loss=6.6127e-01 ppl=1.94 best_loss=6.5254e-01 best_ppl=1.92
Epoch 12 - |param|=9.14e+02 |g_param|=2.47e+05 loss_x2y=5.2454e-01 ppl_x2y=1.69 loss_y2x=5.3844e-01 ppl_y2x=1.71 dual_loss=0.0000e+00
Validation X2Y - loss=6.9802e-01 ppl=2.01 best_loss=6.9699e-01 best_ppl=2.01                                            
Validation Y2X - loss=6.3624e-01 ppl=1.89 best_loss=6.5254e-01 best_ppl=1.92
Epoch 13 - |param|=9.15e+02 |g_param|=1.89e+05 loss_x2y=4.5819e-01 ppl_x2y=1.58 loss_y2x=4.4830e-01 ppl_y2x=1.57 dual_loss=0.0000e+00
Validation X2Y - loss=6.6232e-01 ppl=1.94 best_loss=6.9699e-01 best_ppl=2.01                                            
Validation Y2X - loss=6.3129e-01 ppl=1.88 best_loss=6.3624e-01 best_ppl=1.89
Epoch 14 - |param|=9.15e+02 |g_param|=2.26e+05 loss_x2y=4.8863e-01 ppl_x2y=1.63 loss_y2x=4.8268e-01 ppl_y2x=1.62 dual_loss=0.0000e+00
Validation X2Y - loss=6.6293e-01 ppl=1.94 best_loss=6.6232e-01 best_ppl=1.94                                            
Validation Y2X - loss=6.0472e-01 ppl=1.83 best_loss=6.3129e-01 best_ppl=1.88
Epoch 15 - |param|=9.15e+02 |g_param|=2.09e+05 loss_x2y=4.6769e-01 ppl_x2y=1.60 loss_y2x=4.5215e-01 ppl_y2x=1.57 dual_loss=0.0000e+00
Validation X2Y - loss=6.6725e-01 ppl=1.95 best_loss=6.6232e-01 best_ppl=1.94                                            
Validation Y2X - loss=6.1814e-01 ppl=1.86 best_loss=6.0472e-01 best_ppl=1.83
Epoch 16 - |param|=9.16e+02 |g_param|=1.78e+05 loss_x2y=3.8719e-01 ppl_x2y=1.47 loss_y2x=3.8053e-01 ppl_y2x=1.46 dual_loss=0.0000e+00
Validation X2Y - loss=6.6133e-01 ppl=1.94 best_loss=6.6232e-01 best_ppl=1.94                                            
Validation Y2X - loss=5.9194e-01 ppl=1.81 best_loss=6.0472e-01 best_ppl=1.83
Epoch 17 - |param|=9.16e+02 |g_param|=2.07e+05 loss_x2y=4.0357e-01 ppl_x2y=1.50 loss_y2x=3.9772e-01 ppl_y2x=1.49 dual_loss=0.0000e+00
Validation X2Y - loss=6.3887e-01 ppl=1.89 best_loss=6.6133e-01 best_ppl=1.94                                            
Validation Y2X - loss=5.8574e-01 ppl=1.80 best_loss=5.9194e-01 best_ppl=1.81
Epoch 18 - |param|=9.17e+02 |g_param|=1.91e+05 loss_x2y=3.8032e-01 ppl_x2y=1.46 loss_y2x=3.7162e-01 ppl_y2x=1.45 dual_loss=0.0000e+00
Validation X2Y - loss=6.5334e-01 ppl=1.92 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9717e-01 ppl=1.82 best_loss=5.8574e-01 best_ppl=1.80
Epoch 19 - |param|=9.17e+02 |g_param|=1.81e+05 loss_x2y=3.5761e-01 ppl_x2y=1.43 loss_y2x=3.4546e-01 ppl_y2x=1.41 dual_loss=0.0000e+00
Validation X2Y - loss=6.6774e-01 ppl=1.95 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.7924e-01 ppl=1.78 best_loss=5.8574e-01 best_ppl=1.80
Epoch 20 - |param|=9.17e+02 |g_param|=2.04e+05 loss_x2y=3.4439e-01 ppl_x2y=1.41 loss_y2x=3.3588e-01 ppl_y2x=1.40 dual_loss=0.0000e+00
Validation X2Y - loss=6.4799e-01 ppl=1.91 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.7859e-01 ppl=1.78 best_loss=5.7924e-01 best_ppl=1.78
Epoch 21 - |param|=9.18e+02 |g_param|=2.56e+05 loss_x2y=3.5085e-01 ppl_x2y=1.42 loss_y2x=3.5513e-01 ppl_y2x=1.43 dual_loss=5.3300e-01
Validation X2Y - loss=6.5045e-01 ppl=1.92 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9897e-01 ppl=1.82 best_loss=5.7859e-01 best_ppl=1.78
Epoch 22 - |param|=9.18e+02 |g_param|=2.68e+05 loss_x2y=3.2456e-01 ppl_x2y=1.38 loss_y2x=3.2795e-01 ppl_y2x=1.39 dual_loss=4.3073e-01
Validation X2Y - loss=6.6125e-01 ppl=1.94 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.8990e-01 ppl=1.80 best_loss=5.7859e-01 best_ppl=1.78
Epoch 23 - |param|=9.19e+02 |g_param|=2.84e+05 loss_x2y=3.2876e-01 ppl_x2y=1.39 loss_y2x=3.1375e-01 ppl_y2x=1.37 dual_loss=3.9889e-01
Validation X2Y - loss=6.5141e-01 ppl=1.92 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.7574e-01 ppl=1.78 best_loss=5.7859e-01 best_ppl=1.78
Epoch 24 - |param|=9.19e+02 |g_param|=2.99e+05 loss_x2y=3.1838e-01 ppl_x2y=1.37 loss_y2x=3.1994e-01 ppl_y2x=1.38 dual_loss=4.7606e-01
Validation X2Y - loss=6.5941e-01 ppl=1.93 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.8678e-01 ppl=1.80 best_loss=5.7574e-01 best_ppl=1.78
Epoch 25 - |param|=9.19e+02 |g_param|=2.55e+05 loss_x2y=2.8876e-01 ppl_x2y=1.33 loss_y2x=2.8388e-01 ppl_y2x=1.33 dual_loss=3.6022e-01
Validation X2Y - loss=6.5841e-01 ppl=1.93 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.7816e-01 ppl=1.78 best_loss=5.7574e-01 best_ppl=1.78
Epoch 26 - |param|=9.20e+02 |g_param|=2.88e+05 loss_x2y=3.0356e-01 ppl_x2y=1.35 loss_y2x=3.0213e-01 ppl_y2x=1.35 dual_loss=3.8221e-01
Validation X2Y - loss=6.5662e-01 ppl=1.93 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9253e-01 ppl=1.81 best_loss=5.7574e-01 best_ppl=1.78
Epoch 27 - |param|=9.20e+02 |g_param|=2.65e+05 loss_x2y=2.7488e-01 ppl_x2y=1.32 loss_y2x=2.7230e-01 ppl_y2x=1.31 dual_loss=4.1157e-01
Validation X2Y - loss=6.5684e-01 ppl=1.93 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1559e-01 ppl=1.85 best_loss=5.7574e-01 best_ppl=1.78
Epoch 28 - |param|=9.21e+02 |g_param|=2.81e+05 loss_x2y=2.7275e-01 ppl_x2y=1.31 loss_y2x=2.5800e-01 ppl_y2x=1.29 dual_loss=3.1856e-01
Validation X2Y - loss=6.6709e-01 ppl=1.95 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.0461e-01 ppl=1.83 best_loss=5.7574e-01 best_ppl=1.78
Epoch 29 - |param|=9.21e+02 |g_param|=2.49e+05 loss_x2y=2.6176e-01 ppl_x2y=1.30 loss_y2x=2.5964e-01 ppl_y2x=1.30 dual_loss=3.3691e-01
Validation X2Y - loss=6.5149e-01 ppl=1.92 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9602e-01 ppl=1.81 best_loss=5.7574e-01 best_ppl=1.78
Epoch 30 - |param|=9.21e+02 |g_param|=2.61e+05 loss_x2y=2.5571e-01 ppl_x2y=1.29 loss_y2x=2.5732e-01 ppl_y2x=1.29 dual_loss=3.5166e-01
Validation X2Y - loss=6.5881e-01 ppl=1.93 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.7362e-01 ppl=1.77 best_loss=5.7574e-01 best_ppl=1.78
Epoch 31 - |param|=9.22e+02 |g_param|=2.47e+05 loss_x2y=2.4237e-01 ppl_x2y=1.27 loss_y2x=2.4147e-01 ppl_y2x=1.27 dual_loss=3.1720e-01
Validation X2Y - loss=6.5936e-01 ppl=1.93 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.7541e-01 ppl=1.78 best_loss=5.7362e-01 best_ppl=1.77
Epoch 32 - |param|=9.22e+02 |g_param|=2.50e+05 loss_x2y=2.4223e-01 ppl_x2y=1.27 loss_y2x=2.3423e-01 ppl_y2x=1.26 dual_loss=2.9984e-01
Validation X2Y - loss=6.7963e-01 ppl=1.97 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.8209e-01 ppl=1.79 best_loss=5.7362e-01 best_ppl=1.77
Epoch 33 - |param|=9.23e+02 |g_param|=2.52e+05 loss_x2y=2.3930e-01 ppl_x2y=1.27 loss_y2x=2.3750e-01 ppl_y2x=1.27 dual_loss=3.4092e-01
Validation X2Y - loss=6.8232e-01 ppl=1.98 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.7704e-01 ppl=1.78 best_loss=5.7362e-01 best_ppl=1.77
Epoch 34 - |param|=9.23e+02 |g_param|=2.47e+05 loss_x2y=2.2905e-01 ppl_x2y=1.26 loss_y2x=2.2931e-01 ppl_y2x=1.26 dual_loss=3.6457e-01
Validation X2Y - loss=6.8197e-01 ppl=1.98 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9145e-01 ppl=1.81 best_loss=5.7362e-01 best_ppl=1.77
Epoch 35 - |param|=9.23e+02 |g_param|=2.60e+05 loss_x2y=2.3425e-01 ppl_x2y=1.26 loss_y2x=2.3262e-01 ppl_y2x=1.26 dual_loss=4.2682e-01
Validation X2Y - loss=6.8292e-01 ppl=1.98 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.8877e-01 ppl=1.80 best_loss=5.7362e-01 best_ppl=1.77
Epoch 36 - |param|=9.24e+02 |g_param|=2.62e+05 loss_x2y=2.3536e-01 ppl_x2y=1.27 loss_y2x=2.2068e-01 ppl_y2x=1.25 dual_loss=3.3149e-01
Validation X2Y - loss=6.8522e-01 ppl=1.98 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.8669e-01 ppl=1.80 best_loss=5.7362e-01 best_ppl=1.77
Epoch 37 - |param|=9.24e+02 |g_param|=2.20e+05 loss_x2y=2.0363e-01 ppl_x2y=1.23 loss_y2x=2.0495e-01 ppl_y2x=1.23 dual_loss=3.0892e-01
Validation X2Y - loss=6.7260e-01 ppl=1.96 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.7745e-01 ppl=1.78 best_loss=5.7362e-01 best_ppl=1.77
Epoch 38 - |param|=9.25e+02 |g_param|=2.62e+05 loss_x2y=2.2200e-01 ppl_x2y=1.25 loss_y2x=2.1303e-01 ppl_y2x=1.24 dual_loss=4.1532e-01
Validation X2Y - loss=6.9007e-01 ppl=1.99 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.6803e-01 ppl=1.76 best_loss=5.7362e-01 best_ppl=1.77
Epoch 39 - |param|=9.25e+02 |g_param|=2.52e+05 loss_x2y=2.0831e-01 ppl_x2y=1.23 loss_y2x=2.0203e-01 ppl_y2x=1.22 dual_loss=3.3867e-01
Validation X2Y - loss=6.7407e-01 ppl=1.96 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.7932e-01 ppl=1.78 best_loss=5.6803e-01 best_ppl=1.76
Epoch 40 - |param|=9.25e+02 |g_param|=2.43e+05 loss_x2y=2.0750e-01 ppl_x2y=1.23 loss_y2x=2.0987e-01 ppl_y2x=1.23 dual_loss=3.7487e-01
Validation X2Y - loss=6.9371e-01 ppl=2.00 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9750e-01 ppl=1.82 best_loss=5.6803e-01 best_ppl=1.76
Epoch 41 - |param|=9.26e+02 |g_param|=2.85e+05 loss_x2y=2.0050e-01 ppl_x2y=1.22 loss_y2x=1.8767e-01 ppl_y2x=1.21 dual_loss=3.2120e-01
Validation X2Y - loss=7.2298e-01 ppl=2.06 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.0482e-01 ppl=1.83 best_loss=5.6803e-01 best_ppl=1.76
Epoch 42 - |param|=9.26e+02 |g_param|=4.92e+05 loss_x2y=1.9757e-01 ppl_x2y=1.22 loss_y2x=2.0287e-01 ppl_y2x=1.22 dual_loss=3.5114e-01
Validation X2Y - loss=6.8782e-01 ppl=1.99 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1032e-01 ppl=1.84 best_loss=5.6803e-01 best_ppl=1.76
Epoch 43 - |param|=9.27e+02 |g_param|=4.83e+05 loss_x2y=2.0095e-01 ppl_x2y=1.22 loss_y2x=2.1042e-01 ppl_y2x=1.23 dual_loss=4.0222e-01
Validation X2Y - loss=7.2129e-01 ppl=2.06 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4444e-01 ppl=1.90 best_loss=5.6803e-01 best_ppl=1.76
Epoch 44 - |param|=9.27e+02 |g_param|=4.98e+05 loss_x2y=1.9110e-01 ppl_x2y=1.21 loss_y2x=1.8117e-01 ppl_y2x=1.20 dual_loss=3.6013e-01
Validation X2Y - loss=6.9942e-01 ppl=2.01 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.8450e-01 ppl=1.79 best_loss=5.6803e-01 best_ppl=1.76
Epoch 45 - |param|=9.27e+02 |g_param|=4.72e+05 loss_x2y=1.8152e-01 ppl_x2y=1.20 loss_y2x=1.7467e-01 ppl_y2x=1.19 dual_loss=3.0881e-01
Validation X2Y - loss=7.2005e-01 ppl=2.05 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1085e-01 ppl=1.84 best_loss=5.6803e-01 best_ppl=1.76
Epoch 46 - |param|=9.28e+02 |g_param|=4.76e+05 loss_x2y=1.8652e-01 ppl_x2y=1.21 loss_y2x=1.8425e-01 ppl_y2x=1.20 dual_loss=3.9069e-01
Validation X2Y - loss=7.0517e-01 ppl=2.02 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3353e-01 ppl=1.88 best_loss=5.6803e-01 best_ppl=1.76
Epoch 47 - |param|=9.28e+02 |g_param|=4.67e+05 loss_x2y=1.7501e-01 ppl_x2y=1.19 loss_y2x=1.7143e-01 ppl_y2x=1.19 dual_loss=3.5220e-01
Validation X2Y - loss=7.3280e-01 ppl=2.08 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1373e-01 ppl=1.85 best_loss=5.6803e-01 best_ppl=1.76
Epoch 48 - |param|=9.29e+02 |g_param|=4.93e+05 loss_x2y=1.8074e-01 ppl_x2y=1.20 loss_y2x=1.7166e-01 ppl_y2x=1.19 dual_loss=3.9701e-01
Validation X2Y - loss=7.2208e-01 ppl=2.06 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1432e-01 ppl=1.85 best_loss=5.6803e-01 best_ppl=1.76
Epoch 49 - |param|=9.29e+02 |g_param|=4.22e+05 loss_x2y=1.6425e-01 ppl_x2y=1.18 loss_y2x=1.6560e-01 ppl_y2x=1.18 dual_loss=3.1356e-01
Validation X2Y - loss=7.0838e-01 ppl=2.03 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1194e-01 ppl=1.84 best_loss=5.6803e-01 best_ppl=1.76
Epoch 50 - |param|=9.29e+02 |g_param|=4.67e+05 loss_x2y=1.6753e-01 ppl_x2y=1.18 loss_y2x=1.6857e-01 ppl_y2x=1.18 dual_loss=3.8702e-01
Validation X2Y - loss=7.2228e-01 ppl=2.06 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4512e-01 ppl=1.91 best_loss=5.6803e-01 best_ppl=1.76
Epoch 51 - |param|=9.30e+02 |g_param|=4.60e+05 loss_x2y=1.7130e-01 ppl_x2y=1.19 loss_y2x=1.6634e-01 ppl_y2x=1.18 dual_loss=3.8303e-01
Validation X2Y - loss=7.4719e-01 ppl=2.11 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.2169e-01 ppl=1.86 best_loss=5.6803e-01 best_ppl=1.76
Epoch 52 - |param|=9.30e+02 |g_param|=4.54e+05 loss_x2y=1.6189e-01 ppl_x2y=1.18 loss_y2x=1.6119e-01 ppl_y2x=1.17 dual_loss=3.8645e-01
Validation X2Y - loss=7.3542e-01 ppl=2.09 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3230e-01 ppl=1.88 best_loss=5.6803e-01 best_ppl=1.76
Epoch 53 - |param|=9.31e+02 |g_param|=3.60e+05 loss_x2y=1.7638e-01 ppl_x2y=1.19 loss_y2x=1.6313e-01 ppl_y2x=1.18 dual_loss=3.8903e-01
Validation X2Y - loss=7.3367e-01 ppl=2.08 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3658e-01 ppl=1.89 best_loss=5.6803e-01 best_ppl=1.76
Epoch 54 - |param|=9.31e+02 |g_param|=3.03e+05 loss_x2y=1.5576e-01 ppl_x2y=1.17 loss_y2x=1.5823e-01 ppl_y2x=1.17 dual_loss=3.6345e-01
Validation X2Y - loss=7.3127e-01 ppl=2.08 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3192e-01 ppl=1.88 best_loss=5.6803e-01 best_ppl=1.76
Epoch 55 - |param|=9.31e+02 |g_param|=3.01e+05 loss_x2y=1.5843e-01 ppl_x2y=1.17 loss_y2x=1.5424e-01 ppl_y2x=1.17 dual_loss=3.6992e-01
Validation X2Y - loss=7.3169e-01 ppl=2.08 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4311e-01 ppl=1.90 best_loss=5.6803e-01 best_ppl=1.76
Epoch 56 - |param|=9.32e+02 |g_param|=3.41e+05 loss_x2y=1.5869e-01 ppl_x2y=1.17 loss_y2x=1.6041e-01 ppl_y2x=1.17 dual_loss=4.4156e-01
Validation X2Y - loss=7.3647e-01 ppl=2.09 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3270e-01 ppl=1.88 best_loss=5.6803e-01 best_ppl=1.76
Epoch 57 - |param|=9.32e+02 |g_param|=2.99e+05 loss_x2y=1.4354e-01 ppl_x2y=1.15 loss_y2x=1.4428e-01 ppl_y2x=1.16 dual_loss=3.6569e-01
Validation X2Y - loss=7.3595e-01 ppl=2.09 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6020e-01 ppl=1.94 best_loss=5.6803e-01 best_ppl=1.76
Epoch 58 - |param|=9.33e+02 |g_param|=2.82e+05 loss_x2y=1.4592e-01 ppl_x2y=1.16 loss_y2x=1.4761e-01 ppl_y2x=1.16 dual_loss=3.2548e-01
Validation X2Y - loss=7.5020e-01 ppl=2.12 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4652e-01 ppl=1.91 best_loss=5.6803e-01 best_ppl=1.76
Epoch 59 - |param|=9.33e+02 |g_param|=2.77e+05 loss_x2y=1.4301e-01 ppl_x2y=1.15 loss_y2x=1.3961e-01 ppl_y2x=1.15 dual_loss=3.4482e-01
Validation X2Y - loss=7.7372e-01 ppl=2.17 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3116e-01 ppl=1.88 best_loss=5.6803e-01 best_ppl=1.76
Epoch 60 - |param|=9.33e+02 |g_param|=2.85e+05 loss_x2y=1.4418e-01 ppl_x2y=1.16 loss_y2x=1.4048e-01 ppl_y2x=1.15 dual_loss=3.5568e-01
Validation X2Y - loss=7.6177e-01 ppl=2.14 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6123e-01 ppl=1.94 best_loss=5.6803e-01 best_ppl=1.76
Epoch 61 - |param|=9.34e+02 |g_param|=3.25e+05 loss_x2y=1.5853e-01 ppl_x2y=1.17 loss_y2x=1.4679e-01 ppl_y2x=1.16 dual_loss=3.6982e-01
Validation X2Y - loss=7.6887e-01 ppl=2.16 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4667e-01 ppl=1.91 best_loss=5.6803e-01 best_ppl=1.76
Epoch 62 - |param|=9.34e+02 |g_param|=5.04e+05 loss_x2y=1.4121e-01 ppl_x2y=1.15 loss_y2x=1.3910e-01 ppl_y2x=1.15 dual_loss=3.7342e-01
Validation X2Y - loss=7.7919e-01 ppl=2.18 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6356e-01 ppl=1.94 best_loss=5.6803e-01 best_ppl=1.76
Epoch 63 - |param|=9.35e+02 |g_param|=5.01e+05 loss_x2y=1.3906e-01 ppl_x2y=1.15 loss_y2x=1.3684e-01 ppl_y2x=1.15 dual_loss=3.4497e-01
Validation X2Y - loss=7.7179e-01 ppl=2.16 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4685e-01 ppl=1.91 best_loss=5.6803e-01 best_ppl=1.76
Epoch 64 - |param|=9.35e+02 |g_param|=4.53e+05 loss_x2y=1.3304e-01 ppl_x2y=1.14 loss_y2x=1.2918e-01 ppl_y2x=1.14 dual_loss=3.4071e-01
Validation X2Y - loss=7.9283e-01 ppl=2.21 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3396e-01 ppl=1.89 best_loss=5.6803e-01 best_ppl=1.76
Epoch 65 - |param|=9.35e+02 |g_param|=3.79e+05 loss_x2y=1.3384e-01 ppl_x2y=1.14 loss_y2x=1.3556e-01 ppl_y2x=1.15 dual_loss=3.7588e-01
Validation X2Y - loss=7.8453e-01 ppl=2.19 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6350e-01 ppl=1.94 best_loss=5.6803e-01 best_ppl=1.76
Epoch 66 - |param|=9.36e+02 |g_param|=2.76e+05 loss_x2y=1.2913e-01 ppl_x2y=1.14 loss_y2x=1.2761e-01 ppl_y2x=1.14 dual_loss=3.5429e-01
Validation X2Y - loss=7.7818e-01 ppl=2.18 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.7403e-01 ppl=1.96 best_loss=5.6803e-01 best_ppl=1.76
Epoch 67 - |param|=9.36e+02 |g_param|=2.98e+05 loss_x2y=1.3572e-01 ppl_x2y=1.15 loss_y2x=1.3068e-01 ppl_y2x=1.14 dual_loss=3.6507e-01
Validation X2Y - loss=8.0880e-01 ppl=2.25 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4218e-01 ppl=1.90 best_loss=5.6803e-01 best_ppl=1.76
Epoch 68 - |param|=9.36e+02 |g_param|=2.87e+05 loss_x2y=1.3133e-01 ppl_x2y=1.14 loss_y2x=1.2963e-01 ppl_y2x=1.14 dual_loss=3.8264e-01
Validation X2Y - loss=7.9211e-01 ppl=2.21 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.8063e-01 ppl=1.98 best_loss=5.6803e-01 best_ppl=1.76
Epoch 69 - |param|=9.37e+02 |g_param|=2.79e+05 loss_x2y=1.2915e-01 ppl_x2y=1.14 loss_y2x=1.2586e-01 ppl_y2x=1.13 dual_loss=3.6066e-01
Validation X2Y - loss=8.0283e-01 ppl=2.23 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.9063e-01 ppl=1.99 best_loss=5.6803e-01 best_ppl=1.76
Epoch 70 - |param|=9.37e+02 |g_param|=2.81e+05 loss_x2y=1.3014e-01 ppl_x2y=1.14 loss_y2x=1.2908e-01 ppl_y2x=1.14 dual_loss=3.5860e-01
Validation X2Y - loss=7.9974e-01 ppl=2.22 best_loss=6.3887e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.1006e-01 ppl=2.03 best_loss=5.6803e-01 best_ppl=1.76

real	36m45.142s
user	36m10.800s
sys	0m32.811s
```

#### Warmup-Epoch 20, Total Epoch 80

```
Epoch 1 - |param|=9.12e+02 |g_param|=1.55e+05 loss_x2y=3.6004e+00 ppl_x2y=36.61 loss_y2x=3.5885e+00 ppl_y2x=36.18 dual_loss=0.0000e+00
Validation X2Y - loss=3.0677e+00 ppl=21.49 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=2.9874e+00 ppl=19.83 best_loss=inf best_ppl=inf
Epoch 2 - |param|=9.12e+02 |g_param|=2.12e+05 loss_x2y=2.5225e+00 ppl_x2y=12.46 loss_y2x=2.4821e+00 ppl_y2x=11.97 dual_loss=0.0000e+00
Validation X2Y - loss=2.1249e+00 ppl=8.37 best_loss=3.0677e+00 best_ppl=21.49                                           
Validation Y2X - loss=2.0794e+00 ppl=8.00 best_loss=2.9874e+00 best_ppl=19.83
Epoch 3 - |param|=9.13e+02 |g_param|=2.16e+05 loss_x2y=1.7553e+00 ppl_x2y=5.79 loss_y2x=1.7515e+00 ppl_y2x=5.76 dual_loss=0.0000e+00
Validation X2Y - loss=1.5196e+00 ppl=4.57 best_loss=2.1249e+00 best_ppl=8.37                                            
Validation Y2X - loss=1.5189e+00 ppl=4.57 best_loss=2.0794e+00 best_ppl=8.00
Epoch 4 - |param|=9.13e+02 |g_param|=2.41e+05 loss_x2y=1.4150e+00 ppl_x2y=4.12 loss_y2x=1.4089e+00 ppl_y2x=4.09 dual_loss=0.0000e+00
Validation X2Y - loss=1.1715e+00 ppl=3.23 best_loss=1.5196e+00 best_ppl=4.57                                            
Validation Y2X - loss=1.1986e+00 ppl=3.32 best_loss=1.5189e+00 best_ppl=4.57
Epoch 5 - |param|=9.14e+02 |g_param|=2.25e+05 loss_x2y=1.1229e+00 ppl_x2y=3.07 loss_y2x=1.1467e+00 ppl_y2x=3.15 dual_loss=0.0000e+00
Validation X2Y - loss=9.9273e-01 ppl=2.70 best_loss=1.1715e+00 best_ppl=3.23                                            
Validation Y2X - loss=9.9692e-01 ppl=2.71 best_loss=1.1986e+00 best_ppl=3.32
Epoch 6 - |param|=9.14e+02 |g_param|=2.52e+05 loss_x2y=9.3384e-01 ppl_x2y=2.54 loss_y2x=9.4659e-01 ppl_y2x=2.58 dual_loss=0.0000e+00
Validation X2Y - loss=8.6040e-01 ppl=2.36 best_loss=9.9273e-01 best_ppl=2.70                                            
Validation Y2X - loss=8.7535e-01 ppl=2.40 best_loss=9.9692e-01 best_ppl=2.71
Epoch 7 - |param|=9.14e+02 |g_param|=2.24e+05 loss_x2y=8.1486e-01 ppl_x2y=2.26 loss_y2x=8.3044e-01 ppl_y2x=2.29 dual_loss=0.0000e+00
Validation X2Y - loss=7.9204e-01 ppl=2.21 best_loss=8.6040e-01 best_ppl=2.36                                            
Validation Y2X - loss=8.0639e-01 ppl=2.24 best_loss=8.7535e-01 best_ppl=2.40
Epoch 8 - |param|=9.14e+02 |g_param|=2.55e+05 loss_x2y=7.9508e-01 ppl_x2y=2.21 loss_y2x=8.0229e-01 ppl_y2x=2.23 dual_loss=0.0000e+00
Validation X2Y - loss=7.8830e-01 ppl=2.20 best_loss=7.9204e-01 best_ppl=2.21                                            
Validation Y2X - loss=7.9564e-01 ppl=2.22 best_loss=8.0639e-01 best_ppl=2.24
Epoch 9 - |param|=9.15e+02 |g_param|=2.17e+05 loss_x2y=6.5221e-01 ppl_x2y=1.92 loss_y2x=6.4801e-01 ppl_y2x=1.91 dual_loss=0.0000e+00
Validation X2Y - loss=7.0254e-01 ppl=2.02 best_loss=7.8830e-01 best_ppl=2.20                                            
Validation Y2X - loss=7.0132e-01 ppl=2.02 best_loss=7.9564e-01 best_ppl=2.22
Epoch 10 - |param|=9.15e+02 |g_param|=2.26e+05 loss_x2y=6.1213e-01 ppl_x2y=1.84 loss_y2x=6.1405e-01 ppl_y2x=1.85 dual_loss=0.0000e+00
Validation X2Y - loss=7.4892e-01 ppl=2.11 best_loss=7.0254e-01 best_ppl=2.02                                            
Validation Y2X - loss=6.6233e-01 ppl=1.94 best_loss=7.0132e-01 best_ppl=2.02
Epoch 11 - |param|=9.15e+02 |g_param|=2.20e+05 loss_x2y=5.7558e-01 ppl_x2y=1.78 loss_y2x=5.8646e-01 ppl_y2x=1.80 dual_loss=0.0000e+00
Validation X2Y - loss=6.7300e-01 ppl=1.96 best_loss=7.0254e-01 best_ppl=2.02                                            
Validation Y2X - loss=6.4336e-01 ppl=1.90 best_loss=6.6233e-01 best_ppl=1.94
Epoch 12 - |param|=9.16e+02 |g_param|=2.10e+05 loss_x2y=5.2612e-01 ppl_x2y=1.69 loss_y2x=5.2960e-01 ppl_y2x=1.70 dual_loss=0.0000e+00
Validation X2Y - loss=6.5562e-01 ppl=1.93 best_loss=6.7300e-01 best_ppl=1.96                                            
Validation Y2X - loss=6.3126e-01 ppl=1.88 best_loss=6.4336e-01 best_ppl=1.90
Epoch 13 - |param|=9.16e+02 |g_param|=2.07e+05 loss_x2y=4.8427e-01 ppl_x2y=1.62 loss_y2x=4.8176e-01 ppl_y2x=1.62 dual_loss=0.0000e+00
Validation X2Y - loss=6.4745e-01 ppl=1.91 best_loss=6.5562e-01 best_ppl=1.93                                            
Validation Y2X - loss=6.2587e-01 ppl=1.87 best_loss=6.3126e-01 best_ppl=1.88
Epoch 14 - |param|=9.16e+02 |g_param|=2.24e+05 loss_x2y=4.6643e-01 ppl_x2y=1.59 loss_y2x=4.6745e-01 ppl_y2x=1.60 dual_loss=0.0000e+00
Validation X2Y - loss=6.7221e-01 ppl=1.96 best_loss=6.4745e-01 best_ppl=1.91                                            
Validation Y2X - loss=6.3460e-01 ppl=1.89 best_loss=6.2587e-01 best_ppl=1.87
Epoch 15 - |param|=9.17e+02 |g_param|=2.18e+05 loss_x2y=4.3818e-01 ppl_x2y=1.55 loss_y2x=4.3713e-01 ppl_y2x=1.55 dual_loss=0.0000e+00
Validation X2Y - loss=6.4703e-01 ppl=1.91 best_loss=6.4745e-01 best_ppl=1.91                                            
Validation Y2X - loss=5.8684e-01 ppl=1.80 best_loss=6.2587e-01 best_ppl=1.87
Epoch 16 - |param|=9.17e+02 |g_param|=1.80e+05 loss_x2y=3.9260e-01 ppl_x2y=1.48 loss_y2x=3.9241e-01 ppl_y2x=1.48 dual_loss=0.0000e+00
Validation X2Y - loss=6.4660e-01 ppl=1.91 best_loss=6.4703e-01 best_ppl=1.91                                            
Validation Y2X - loss=5.9480e-01 ppl=1.81 best_loss=5.8684e-01 best_ppl=1.80
Epoch 17 - |param|=9.18e+02 |g_param|=1.93e+05 loss_x2y=3.9749e-01 ppl_x2y=1.49 loss_y2x=3.8909e-01 ppl_y2x=1.48 dual_loss=0.0000e+00
Validation X2Y - loss=6.2909e-01 ppl=1.88 best_loss=6.4660e-01 best_ppl=1.91                                            
Validation Y2X - loss=5.8757e-01 ppl=1.80 best_loss=5.8684e-01 best_ppl=1.80
Epoch 18 - |param|=9.18e+02 |g_param|=1.81e+05 loss_x2y=3.6635e-01 ppl_x2y=1.44 loss_y2x=3.5625e-01 ppl_y2x=1.43 dual_loss=0.0000e+00
Validation X2Y - loss=6.3536e-01 ppl=1.89 best_loss=6.2909e-01 best_ppl=1.88                                            
Validation Y2X - loss=6.0151e-01 ppl=1.82 best_loss=5.8684e-01 best_ppl=1.80
Epoch 19 - |param|=9.18e+02 |g_param|=2.18e+05 loss_x2y=3.6727e-01 ppl_x2y=1.44 loss_y2x=3.7170e-01 ppl_y2x=1.45 dual_loss=0.0000e+00
Validation X2Y - loss=6.1665e-01 ppl=1.85 best_loss=6.2909e-01 best_ppl=1.88                                            
Validation Y2X - loss=5.6778e-01 ppl=1.76 best_loss=5.8684e-01 best_ppl=1.80
Epoch 20 - |param|=9.19e+02 |g_param|=1.92e+05 loss_x2y=3.4205e-01 ppl_x2y=1.41 loss_y2x=3.3450e-01 ppl_y2x=1.40 dual_loss=0.0000e+00
Validation X2Y - loss=6.3635e-01 ppl=1.89 best_loss=6.1665e-01 best_ppl=1.85                                            
Validation Y2X - loss=5.7984e-01 ppl=1.79 best_loss=5.6778e-01 best_ppl=1.76
Epoch 21 - |param|=9.19e+02 |g_param|=3.60e+05 loss_x2y=3.4075e-01 ppl_x2y=1.41 loss_y2x=3.5419e-01 ppl_y2x=1.43 dual_loss=5.0739e-01
Validation X2Y - loss=6.1695e-01 ppl=1.85 best_loss=6.1665e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.1416e-01 ppl=1.85 best_loss=5.6778e-01 best_ppl=1.76
Epoch 22 - |param|=9.20e+02 |g_param|=2.86e+05 loss_x2y=3.4157e-01 ppl_x2y=1.41 loss_y2x=3.4028e-01 ppl_y2x=1.41 dual_loss=4.1401e-01
Validation X2Y - loss=6.1444e-01 ppl=1.85 best_loss=6.1665e-01 best_ppl=1.85                                            
Validation Y2X - loss=5.7974e-01 ppl=1.79 best_loss=5.6778e-01 best_ppl=1.76
Epoch 23 - |param|=9.20e+02 |g_param|=2.67e+05 loss_x2y=3.2182e-01 ppl_x2y=1.38 loss_y2x=3.4243e-01 ppl_y2x=1.41 dual_loss=5.0355e-01
Validation X2Y - loss=6.3222e-01 ppl=1.88 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=5.5817e-01 ppl=1.75 best_loss=5.6778e-01 best_ppl=1.76
Epoch 24 - |param|=9.20e+02 |g_param|=2.83e+05 loss_x2y=3.1542e-01 ppl_x2y=1.37 loss_y2x=3.0704e-01 ppl_y2x=1.36 dual_loss=4.0667e-01
Validation X2Y - loss=6.3040e-01 ppl=1.88 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=5.7265e-01 ppl=1.77 best_loss=5.5817e-01 best_ppl=1.75
Epoch 25 - |param|=9.21e+02 |g_param|=2.91e+05 loss_x2y=3.1620e-01 ppl_x2y=1.37 loss_y2x=3.3678e-01 ppl_y2x=1.40 dual_loss=5.2459e-01
Validation X2Y - loss=6.1820e-01 ppl=1.86 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=5.7507e-01 ppl=1.78 best_loss=5.5817e-01 best_ppl=1.75
Epoch 26 - |param|=9.21e+02 |g_param|=2.14e+05 loss_x2y=2.9857e-01 ppl_x2y=1.35 loss_y2x=2.8227e-01 ppl_y2x=1.33 dual_loss=3.7299e-01
Validation X2Y - loss=6.4745e-01 ppl=1.91 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=5.8620e-01 ppl=1.80 best_loss=5.5817e-01 best_ppl=1.75
Epoch 27 - |param|=9.22e+02 |g_param|=1.85e+05 loss_x2y=2.8433e-01 ppl_x2y=1.33 loss_y2x=2.8649e-01 ppl_y2x=1.33 dual_loss=3.7063e-01
Validation X2Y - loss=6.3803e-01 ppl=1.89 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=5.7845e-01 ppl=1.78 best_loss=5.5817e-01 best_ppl=1.75
Epoch 28 - |param|=9.22e+02 |g_param|=1.80e+05 loss_x2y=2.7666e-01 ppl_x2y=1.32 loss_y2x=2.7491e-01 ppl_y2x=1.32 dual_loss=3.5644e-01
Validation X2Y - loss=6.1940e-01 ppl=1.86 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.0705e-01 ppl=1.84 best_loss=5.5817e-01 best_ppl=1.75
Epoch 29 - |param|=9.22e+02 |g_param|=1.79e+05 loss_x2y=2.7419e-01 ppl_x2y=1.32 loss_y2x=2.6596e-01 ppl_y2x=1.30 dual_loss=3.8787e-01
Validation X2Y - loss=6.7298e-01 ppl=1.96 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.0716e-01 ppl=1.84 best_loss=5.5817e-01 best_ppl=1.75
Epoch 30 - |param|=9.23e+02 |g_param|=1.85e+05 loss_x2y=2.5685e-01 ppl_x2y=1.29 loss_y2x=2.5104e-01 ppl_y2x=1.29 dual_loss=3.4916e-01
Validation X2Y - loss=6.2973e-01 ppl=1.88 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.0896e-01 ppl=1.84 best_loss=5.5817e-01 best_ppl=1.75
Epoch 31 - |param|=9.23e+02 |g_param|=1.69e+05 loss_x2y=2.4836e-01 ppl_x2y=1.28 loss_y2x=2.4950e-01 ppl_y2x=1.28 dual_loss=3.6217e-01
Validation X2Y - loss=6.4463e-01 ppl=1.91 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=5.9516e-01 ppl=1.81 best_loss=5.5817e-01 best_ppl=1.75
Epoch 32 - |param|=9.24e+02 |g_param|=1.74e+05 loss_x2y=2.4720e-01 ppl_x2y=1.28 loss_y2x=2.4723e-01 ppl_y2x=1.28 dual_loss=3.6171e-01
Validation X2Y - loss=6.5144e-01 ppl=1.92 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=5.9532e-01 ppl=1.81 best_loss=5.5817e-01 best_ppl=1.75
Epoch 33 - |param|=9.24e+02 |g_param|=1.65e+05 loss_x2y=2.2947e-01 ppl_x2y=1.26 loss_y2x=2.2772e-01 ppl_y2x=1.26 dual_loss=3.5771e-01
Validation X2Y - loss=6.7347e-01 ppl=1.96 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.1025e-01 ppl=1.84 best_loss=5.5817e-01 best_ppl=1.75
Epoch 34 - |param|=9.24e+02 |g_param|=1.80e+05 loss_x2y=2.3894e-01 ppl_x2y=1.27 loss_y2x=2.3724e-01 ppl_y2x=1.27 dual_loss=3.6091e-01
Validation X2Y - loss=6.4871e-01 ppl=1.91 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=5.9460e-01 ppl=1.81 best_loss=5.5817e-01 best_ppl=1.75
Epoch 35 - |param|=9.25e+02 |g_param|=1.56e+05 loss_x2y=2.1992e-01 ppl_x2y=1.25 loss_y2x=2.1820e-01 ppl_y2x=1.24 dual_loss=3.1726e-01
Validation X2Y - loss=6.4672e-01 ppl=1.91 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=5.9617e-01 ppl=1.82 best_loss=5.5817e-01 best_ppl=1.75
Epoch 36 - |param|=9.25e+02 |g_param|=1.75e+05 loss_x2y=2.2253e-01 ppl_x2y=1.25 loss_y2x=2.1887e-01 ppl_y2x=1.24 dual_loss=3.3428e-01
Validation X2Y - loss=6.5936e-01 ppl=1.93 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.1798e-01 ppl=1.86 best_loss=5.5817e-01 best_ppl=1.75
Epoch 37 - |param|=9.26e+02 |g_param|=1.81e+05 loss_x2y=2.1988e-01 ppl_x2y=1.25 loss_y2x=2.2650e-01 ppl_y2x=1.25 dual_loss=3.5494e-01
Validation X2Y - loss=6.6058e-01 ppl=1.94 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=5.8495e-01 ppl=1.79 best_loss=5.5817e-01 best_ppl=1.75
Epoch 38 - |param|=9.26e+02 |g_param|=1.70e+05 loss_x2y=2.1011e-01 ppl_x2y=1.23 loss_y2x=2.0939e-01 ppl_y2x=1.23 dual_loss=3.4576e-01
Validation X2Y - loss=6.5967e-01 ppl=1.93 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=5.9201e-01 ppl=1.81 best_loss=5.5817e-01 best_ppl=1.75
Epoch 39 - |param|=9.26e+02 |g_param|=1.70e+05 loss_x2y=2.1659e-01 ppl_x2y=1.24 loss_y2x=2.0817e-01 ppl_y2x=1.23 dual_loss=3.4783e-01
Validation X2Y - loss=6.6122e-01 ppl=1.94 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.0439e-01 ppl=1.83 best_loss=5.5817e-01 best_ppl=1.75
Epoch 40 - |param|=9.27e+02 |g_param|=1.62e+05 loss_x2y=2.0390e-01 ppl_x2y=1.23 loss_y2x=2.1021e-01 ppl_y2x=1.23 dual_loss=3.7480e-01
Validation X2Y - loss=6.5803e-01 ppl=1.93 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.1438e-01 ppl=1.85 best_loss=5.5817e-01 best_ppl=1.75
Epoch 41 - |param|=9.27e+02 |g_param|=1.60e+05 loss_x2y=1.9908e-01 ppl_x2y=1.22 loss_y2x=1.9390e-01 ppl_y2x=1.21 dual_loss=3.3130e-01
Validation X2Y - loss=6.6967e-01 ppl=1.95 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.0543e-01 ppl=1.83 best_loss=5.5817e-01 best_ppl=1.75
Epoch 42 - |param|=9.28e+02 |g_param|=1.89e+05 loss_x2y=1.8983e-01 ppl_x2y=1.21 loss_y2x=1.9087e-01 ppl_y2x=1.21 dual_loss=3.3566e-01
Validation X2Y - loss=6.7640e-01 ppl=1.97 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=5.9915e-01 ppl=1.82 best_loss=5.5817e-01 best_ppl=1.75
Epoch 43 - |param|=9.28e+02 |g_param|=2.82e+05 loss_x2y=1.9843e-01 ppl_x2y=1.22 loss_y2x=1.9900e-01 ppl_y2x=1.22 dual_loss=3.8885e-01
Validation X2Y - loss=6.8188e-01 ppl=1.98 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=5.9779e-01 ppl=1.82 best_loss=5.5817e-01 best_ppl=1.75
Epoch 44 - |param|=9.28e+02 |g_param|=2.84e+05 loss_x2y=1.9277e-01 ppl_x2y=1.21 loss_y2x=1.9690e-01 ppl_y2x=1.22 dual_loss=3.5155e-01
Validation X2Y - loss=6.8515e-01 ppl=1.98 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.0332e-01 ppl=1.83 best_loss=5.5817e-01 best_ppl=1.75
Epoch 45 - |param|=9.29e+02 |g_param|=2.63e+05 loss_x2y=1.8709e-01 ppl_x2y=1.21 loss_y2x=1.8669e-01 ppl_y2x=1.21 dual_loss=3.3999e-01
Validation X2Y - loss=6.7933e-01 ppl=1.97 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.1274e-01 ppl=1.85 best_loss=5.5817e-01 best_ppl=1.75
Epoch 46 - |param|=9.29e+02 |g_param|=2.76e+05 loss_x2y=1.7766e-01 ppl_x2y=1.19 loss_y2x=1.7879e-01 ppl_y2x=1.20 dual_loss=3.3545e-01
Validation X2Y - loss=6.8686e-01 ppl=1.99 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.1284e-01 ppl=1.85 best_loss=5.5817e-01 best_ppl=1.75
Epoch 47 - |param|=9.30e+02 |g_param|=3.01e+05 loss_x2y=1.7786e-01 ppl_x2y=1.19 loss_y2x=1.7653e-01 ppl_y2x=1.19 dual_loss=3.2421e-01
Validation X2Y - loss=6.8729e-01 ppl=1.99 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.1754e-01 ppl=1.85 best_loss=5.5817e-01 best_ppl=1.75
Epoch 48 - |param|=9.30e+02 |g_param|=3.18e+05 loss_x2y=1.8022e-01 ppl_x2y=1.20 loss_y2x=1.7731e-01 ppl_y2x=1.19 dual_loss=3.9254e-01
Validation X2Y - loss=6.7331e-01 ppl=1.96 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.1213e-01 ppl=1.84 best_loss=5.5817e-01 best_ppl=1.75
Epoch 49 - |param|=9.30e+02 |g_param|=3.27e+05 loss_x2y=1.7941e-01 ppl_x2y=1.20 loss_y2x=1.8628e-01 ppl_y2x=1.20 dual_loss=4.3891e-01
Validation X2Y - loss=6.9097e-01 ppl=2.00 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.3523e-01 ppl=1.89 best_loss=5.5817e-01 best_ppl=1.75
Epoch 50 - |param|=9.31e+02 |g_param|=3.21e+05 loss_x2y=1.7040e-01 ppl_x2y=1.19 loss_y2x=1.6777e-01 ppl_y2x=1.18 dual_loss=3.5167e-01
Validation X2Y - loss=6.8821e-01 ppl=1.99 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.2468e-01 ppl=1.87 best_loss=5.5817e-01 best_ppl=1.75
Epoch 51 - |param|=9.31e+02 |g_param|=3.15e+05 loss_x2y=1.6145e-01 ppl_x2y=1.18 loss_y2x=1.6105e-01 ppl_y2x=1.17 dual_loss=3.5967e-01
Validation X2Y - loss=7.0462e-01 ppl=2.02 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.2404e-01 ppl=1.87 best_loss=5.5817e-01 best_ppl=1.75
Epoch 52 - |param|=9.32e+02 |g_param|=3.28e+05 loss_x2y=1.6354e-01 ppl_x2y=1.18 loss_y2x=1.5965e-01 ppl_y2x=1.17 dual_loss=3.7813e-01
Validation X2Y - loss=7.1705e-01 ppl=2.05 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.6243e-01 ppl=1.94 best_loss=5.5817e-01 best_ppl=1.75
Epoch 53 - |param|=9.32e+02 |g_param|=3.20e+05 loss_x2y=1.6943e-01 ppl_x2y=1.18 loss_y2x=1.6054e-01 ppl_y2x=1.17 dual_loss=3.7945e-01
Validation X2Y - loss=6.8611e-01 ppl=1.99 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.2260e-01 ppl=1.86 best_loss=5.5817e-01 best_ppl=1.75
Epoch 54 - |param|=9.32e+02 |g_param|=2.89e+05 loss_x2y=1.4783e-01 ppl_x2y=1.16 loss_y2x=1.5177e-01 ppl_y2x=1.16 dual_loss=3.2121e-01
Validation X2Y - loss=6.9657e-01 ppl=2.01 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.3395e-01 ppl=1.89 best_loss=5.5817e-01 best_ppl=1.75
Epoch 55 - |param|=9.33e+02 |g_param|=3.12e+05 loss_x2y=1.5562e-01 ppl_x2y=1.17 loss_y2x=1.5627e-01 ppl_y2x=1.17 dual_loss=3.7807e-01
Validation X2Y - loss=7.0201e-01 ppl=2.02 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.4769e-01 ppl=1.91 best_loss=5.5817e-01 best_ppl=1.75
Epoch 56 - |param|=9.33e+02 |g_param|=2.99e+05 loss_x2y=1.5362e-01 ppl_x2y=1.17 loss_y2x=1.5267e-01 ppl_y2x=1.16 dual_loss=3.6212e-01
Validation X2Y - loss=7.1376e-01 ppl=2.04 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.5185e-01 ppl=1.92 best_loss=5.5817e-01 best_ppl=1.75
Epoch 57 - |param|=9.34e+02 |g_param|=3.24e+05 loss_x2y=1.5701e-01 ppl_x2y=1.17 loss_y2x=1.5379e-01 ppl_y2x=1.17 dual_loss=3.5713e-01
Validation X2Y - loss=7.1075e-01 ppl=2.04 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.5854e-01 ppl=1.93 best_loss=5.5817e-01 best_ppl=1.75
Epoch 58 - |param|=9.34e+02 |g_param|=2.84e+05 loss_x2y=1.4664e-01 ppl_x2y=1.16 loss_y2x=1.4402e-01 ppl_y2x=1.15 dual_loss=3.4211e-01
Validation X2Y - loss=7.2099e-01 ppl=2.06 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.3947e-01 ppl=1.90 best_loss=5.5817e-01 best_ppl=1.75
Epoch 59 - |param|=9.34e+02 |g_param|=2.97e+05 loss_x2y=1.4283e-01 ppl_x2y=1.15 loss_y2x=1.4556e-01 ppl_y2x=1.16 dual_loss=3.7095e-01
Validation X2Y - loss=7.0568e-01 ppl=2.03 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.5216e-01 ppl=1.92 best_loss=5.5817e-01 best_ppl=1.75
Epoch 60 - |param|=9.35e+02 |g_param|=2.93e+05 loss_x2y=1.4521e-01 ppl_x2y=1.16 loss_y2x=1.4219e-01 ppl_y2x=1.15 dual_loss=3.8359e-01
Validation X2Y - loss=7.4764e-01 ppl=2.11 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.4922e-01 ppl=1.91 best_loss=5.5817e-01 best_ppl=1.75
Epoch 61 - |param|=9.35e+02 |g_param|=2.94e+05 loss_x2y=1.3793e-01 ppl_x2y=1.15 loss_y2x=1.4138e-01 ppl_y2x=1.15 dual_loss=3.5398e-01
Validation X2Y - loss=7.4729e-01 ppl=2.11 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.5345e-01 ppl=1.92 best_loss=5.5817e-01 best_ppl=1.75
Epoch 62 - |param|=9.36e+02 |g_param|=3.32e+05 loss_x2y=1.4601e-01 ppl_x2y=1.16 loss_y2x=1.4610e-01 ppl_y2x=1.16 dual_loss=4.3296e-01
Validation X2Y - loss=7.1755e-01 ppl=2.05 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.6099e-01 ppl=1.94 best_loss=5.5817e-01 best_ppl=1.75
Epoch 63 - |param|=9.36e+02 |g_param|=4.67e+05 loss_x2y=1.4326e-01 ppl_x2y=1.15 loss_y2x=1.4006e-01 ppl_y2x=1.15 dual_loss=3.6791e-01
Validation X2Y - loss=7.3421e-01 ppl=2.08 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.4679e-01 ppl=1.91 best_loss=5.5817e-01 best_ppl=1.75
Epoch 64 - |param|=9.36e+02 |g_param|=4.87e+05 loss_x2y=1.3652e-01 ppl_x2y=1.15 loss_y2x=1.3591e-01 ppl_y2x=1.15 dual_loss=3.8586e-01
Validation X2Y - loss=7.5015e-01 ppl=2.12 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.5723e-01 ppl=1.93 best_loss=5.5817e-01 best_ppl=1.75
Epoch 65 - |param|=9.37e+02 |g_param|=4.83e+05 loss_x2y=1.3222e-01 ppl_x2y=1.14 loss_y2x=1.3487e-01 ppl_y2x=1.14 dual_loss=3.5885e-01
Validation X2Y - loss=7.3894e-01 ppl=2.09 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.5691e-01 ppl=1.93 best_loss=5.5817e-01 best_ppl=1.75
Epoch 66 - |param|=9.37e+02 |g_param|=5.12e+05 loss_x2y=1.3604e-01 ppl_x2y=1.15 loss_y2x=1.3916e-01 ppl_y2x=1.15 dual_loss=3.9940e-01
Validation X2Y - loss=7.3571e-01 ppl=2.09 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.5705e-01 ppl=1.93 best_loss=5.5817e-01 best_ppl=1.75
Epoch 67 - |param|=9.38e+02 |g_param|=5.50e+05 loss_x2y=1.3514e-01 ppl_x2y=1.14 loss_y2x=1.3346e-01 ppl_y2x=1.14 dual_loss=4.0399e-01
Validation X2Y - loss=7.4878e-01 ppl=2.11 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.5535e-01 ppl=1.93 best_loss=5.5817e-01 best_ppl=1.75
Epoch 68 - |param|=9.38e+02 |g_param|=5.54e+05 loss_x2y=1.2697e-01 ppl_x2y=1.14 loss_y2x=1.2866e-01 ppl_y2x=1.14 dual_loss=3.6282e-01
Validation X2Y - loss=7.2018e-01 ppl=2.05 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.6691e-01 ppl=1.95 best_loss=5.5817e-01 best_ppl=1.75
Epoch 69 - |param|=9.38e+02 |g_param|=4.17e+05 loss_x2y=1.2738e-01 ppl_x2y=1.14 loss_y2x=1.2326e-01 ppl_y2x=1.13 dual_loss=3.6367e-01
Validation X2Y - loss=7.4280e-01 ppl=2.10 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.7658e-01 ppl=1.97 best_loss=5.5817e-01 best_ppl=1.75
Epoch 70 - |param|=9.39e+02 |g_param|=4.36e+05 loss_x2y=1.2997e-01 ppl_x2y=1.14 loss_y2x=1.2897e-01 ppl_y2x=1.14 dual_loss=4.1396e-01
Validation X2Y - loss=7.7605e-01 ppl=2.17 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.7625e-01 ppl=1.97 best_loss=5.5817e-01 best_ppl=1.75
Epoch 71 - |param|=9.39e+02 |g_param|=4.16e+05 loss_x2y=1.2577e-01 ppl_x2y=1.13 loss_y2x=1.2649e-01 ppl_y2x=1.13 dual_loss=3.8339e-01
Validation X2Y - loss=7.4462e-01 ppl=2.11 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.5732e-01 ppl=1.93 best_loss=5.5817e-01 best_ppl=1.75
Epoch 72 - |param|=9.39e+02 |g_param|=4.47e+05 loss_x2y=1.2861e-01 ppl_x2y=1.14 loss_y2x=1.2608e-01 ppl_y2x=1.13 dual_loss=4.1536e-01
Validation X2Y - loss=7.5674e-01 ppl=2.13 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.6089e-01 ppl=1.94 best_loss=5.5817e-01 best_ppl=1.75
Epoch 73 - |param|=9.40e+02 |g_param|=4.27e+05 loss_x2y=1.3011e-01 ppl_x2y=1.14 loss_y2x=1.2537e-01 ppl_y2x=1.13 dual_loss=3.7407e-01
Validation X2Y - loss=7.5983e-01 ppl=2.14 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.5834e-01 ppl=1.93 best_loss=5.5817e-01 best_ppl=1.75
Epoch 74 - |param|=9.40e+02 |g_param|=4.12e+05 loss_x2y=1.2006e-01 ppl_x2y=1.13 loss_y2x=1.1679e-01 ppl_y2x=1.12 dual_loss=3.4324e-01
Validation X2Y - loss=7.4428e-01 ppl=2.10 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.6971e-01 ppl=1.95 best_loss=5.5817e-01 best_ppl=1.75
Epoch 75 - |param|=9.41e+02 |g_param|=4.21e+05 loss_x2y=1.1985e-01 ppl_x2y=1.13 loss_y2x=1.2280e-01 ppl_y2x=1.13 dual_loss=4.0527e-01
Validation X2Y - loss=7.7398e-01 ppl=2.17 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.7525e-01 ppl=1.96 best_loss=5.5817e-01 best_ppl=1.75
Epoch 76 - |param|=9.41e+02 |g_param|=4.17e+05 loss_x2y=1.1969e-01 ppl_x2y=1.13 loss_y2x=1.1791e-01 ppl_y2x=1.13 dual_loss=4.1187e-01
Validation X2Y - loss=7.8949e-01 ppl=2.20 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.6624e-01 ppl=1.95 best_loss=5.5817e-01 best_ppl=1.75
Epoch 77 - |param|=9.41e+02 |g_param|=3.98e+05 loss_x2y=1.1696e-01 ppl_x2y=1.12 loss_y2x=1.1341e-01 ppl_y2x=1.12 dual_loss=3.5228e-01
Validation X2Y - loss=7.7010e-01 ppl=2.16 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.5838e-01 ppl=1.93 best_loss=5.5817e-01 best_ppl=1.75
Epoch 78 - |param|=9.42e+02 |g_param|=4.43e+05 loss_x2y=1.1789e-01 ppl_x2y=1.13 loss_y2x=1.1887e-01 ppl_y2x=1.13 dual_loss=4.6835e-01
Validation X2Y - loss=7.6794e-01 ppl=2.16 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.7527e-01 ppl=1.96 best_loss=5.5817e-01 best_ppl=1.75
Epoch 79 - |param|=9.42e+02 |g_param|=3.95e+05 loss_x2y=1.1415e-01 ppl_x2y=1.12 loss_y2x=1.1833e-01 ppl_y2x=1.13 dual_loss=3.7700e-01
Validation X2Y - loss=7.8819e-01 ppl=2.20 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.7674e-01 ppl=1.97 best_loss=5.5817e-01 best_ppl=1.75
Epoch 80 - |param|=9.43e+02 |g_param|=3.98e+05 loss_x2y=1.1207e-01 ppl_x2y=1.12 loss_y2x=1.1044e-01 ppl_y2x=1.12 dual_loss=3.4369e-01
Validation X2Y - loss=7.8563e-01 ppl=2.19 best_loss=6.1444e-01 best_ppl=1.85                                            
Validation Y2X - loss=6.9737e-01 ppl=2.01 best_loss=5.5817e-01 best_ppl=1.75

real	42m1.904s
user	41m22.301s
sys	0m36.888s
```

#### Warmup-Epoch 20, Total Epoch 90

```

```

#### Warmup-Epoch 20, Total Epoch 100

```

```

## DSL-NMT Performance for My-RK 

ဇယားနဲ့ ပြမယ်လို့ စိတ်ကူးထား ...  



## Reference

- [https://stackoverflow.com/questions/42703500/best-way-to-save-a-trained-model-in-pytorch](https://stackoverflow.com/questions/42703500/best-way-to-save-a-trained-model-in-pytorch)
- [(Yingce Xia et. al, 2017, Dual Supervised Learning)](https://arxiv.org/pdf/1707.00415.pdf)  
