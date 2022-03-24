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

## Write a Shell Script for Seq2Seq-DSL Training Loop

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

## Write a Shell Script for Seq2Seq-DSL Testing/Evaluation Loop

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Last Updated: 23 Mar 2022
# find all models and parse to translate.py for testing and multi-bleu.perl for evaluation with BLEU score
# used for seq2seq-DSL evaluation

#for folder in {myrk-30epoch,myrk-40epoch,myrk-50epoch,myrk-60epoch,myrk-70epoch,myrk-80epoch,myrk-90epoch,myrk-100epoch};
# 30epoch, 40epoch က ပထမဆုံး စမ်း run ရင်းနဲ့ testing/evaluation ပါ လုပ်ထားပြီးပြီမို့...  
for folder in {myrk-50epoch,myrk-60epoch,myrk-70epoch,myrk-80epoch,myrk-90epoch,myrk-100epoch};
do
   cd ./model/dsl/${folder};
   pwd;
   for i in *.pth;
   do
      MODEL=$i;

      # Testing X-Y
      python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang myrk < /home/ye/exp/simple-nmt/data/test.my > $MODEL.myrk.hyp

      # Evaluation with BLEU Score
      echo "Evaluation result for the model: $MODEL, myrk" | tee -a eval-results-xy-seq2seq.txt;
      cat $MODEL.myrk.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/test.rk | tee  -a eval-results-xy-seq2seq.txt;

      # Testing Y-X
      python /home/ye/exp/simple-nmt/translate.py --model_fn $MODEL --gpu_id 0 --lang rkmy < /home/ye/exp/simple-nmt/data/test.rk > $MODEL.rkmy.hyp

      # Evaluation with BLEU Score
      echo "Evaluation result for the model: $MODEL, rkmy" | tee -a eval-results-yx-seq2seq.txt;
      cat $MODEL.rkmy.hyp | perl /home/ye/exp/simple-nmt/test/multi-bleu.perl /home/ye/exp/simple-nmt/data/test.my | tee  -a eval-results-yx-seq2seq.txt;
   done
   cd ~/exp/simple-nmt/;
   echo "==========";
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

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/myrk-50epoch
Evaluation result for the model: dsl-model-myrk.01.4.44-84.54.4.51-90.63.4.04-57.03.4.13-62.23.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 15.0/2.0/0.0/0.0 (BP=1.000, ratio=1.092, hyp_len=25289, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.01.4.44-84.54.4.51-90.63.4.04-57.03.4.13-62.23.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 11.0/0.0/0.0/0.0 (BP=1.000, ratio=1.178, hyp_len=27683, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.02.4.17-64.56.4.21-67.67.3.87-48.05.3.91-50.03.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 17.8/1.6/0.0/0.0 (BP=1.000, ratio=1.006, hyp_len=23304, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.02.4.17-64.56.4.21-67.67.3.87-48.05.3.91-50.03.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 19.6/2.2/0.0/0.0 (BP=0.985, ratio=0.985, hyp_len=23165, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.03.4.07-58.49.4.12-61.69.3.77-43.54.3.81-45.25.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.2/1.6/0.0/0.0 (BP=1.000, ratio=1.011, hyp_len=23419, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.03.4.07-58.49.4.12-61.69.3.77-43.54.3.81-45.25.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.8/2.5/0.0/0.0 (BP=0.981, ratio=0.981, hyp_len=23058, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.04.3.93-50.69.3.97-53.13.3.69-40.22.3.72-41.27.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 19.7/1.7/0.0/0.0 (BP=1.000, ratio=1.034, hyp_len=23952, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.04.3.93-50.69.3.97-53.13.3.69-40.22.3.72-41.27.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.3/2.8/0.2/0.0 (BP=0.974, ratio=0.975, hyp_len=22910, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.05.3.78-43.62.3.83-45.92.3.58-35.94.3.63-37.82.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.8/2.5/0.1/0.0 (BP=0.998, ratio=0.998, hyp_len=23111, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.05.3.78-43.62.3.83-45.92.3.58-35.94.3.63-37.82.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.6/3.5/0.5/0.0 (BP=0.991, ratio=0.991, hyp_len=23289, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.06.3.80-44.52.3.83-46.21.3.50-33.14.3.53-34.24.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 24.3/3.8/0.3/0.0 (BP=1.000, ratio=1.001, hyp_len=23182, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.06.3.80-44.52.3.83-46.21.3.50-33.14.3.53-34.24.pth, rkmy
BLEU = 0.73, 22.5/4.5/0.5/0.0 (BP=1.000, ratio=1.006, hyp_len=23642, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.07.3.56-35.08.3.64-37.91.3.32-27.79.3.38-29.35.pth, myrk
BLEU = 1.05, 27.8/5.2/0.5/0.0 (BP=0.996, ratio=0.996, hyp_len=23065, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.07.3.56-35.08.3.64-37.91.3.32-27.79.3.38-29.35.pth, rkmy
BLEU = 1.24, 25.1/6.0/1.0/0.0 (BP=0.993, ratio=0.993, hyp_len=23356, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.08.3.43-30.86.3.50-33.03.3.19-24.21.3.23-25.21.pth, myrk
BLEU = 2.23, 29.4/6.1/1.1/0.1 (BP=1.000, ratio=1.006, hyp_len=23295, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.08.3.43-30.86.3.50-33.03.3.19-24.21.3.23-25.21.pth, rkmy
BLEU = 2.59, 27.7/7.4/1.5/0.2 (BP=0.993, ratio=0.993, hyp_len=23349, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.09.3.20-24.65.3.27-26.35.3.02-20.54.3.07-21.46.pth, myrk
BLEU = 5.45, 32.8/9.9/3.0/0.9 (BP=1.000, ratio=1.002, hyp_len=23206, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.09.3.20-24.65.3.27-26.35.3.02-20.54.3.07-21.46.pth, rkmy
BLEU = 4.05, 29.7/8.9/2.0/0.5 (BP=1.000, ratio=1.017, hyp_len=23900, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.10.3.08-21.86.3.13-22.95.2.91-18.42.2.94-18.84.pth, myrk
BLEU = 6.71, 35.5/11.6/3.9/1.3 (BP=1.000, ratio=1.009, hyp_len=23370, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.10.3.08-21.86.3.13-22.95.2.91-18.42.2.94-18.84.pth, rkmy
BLEU = 4.90, 32.6/10.2/2.4/0.7 (BP=1.000, ratio=1.012, hyp_len=23801, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.11.2.91-18.32.2.94-18.84.2.77-15.98.2.78-16.20.pth, myrk
BLEU = 7.99, 38.2/14.0/4.9/1.6 (BP=1.000, ratio=1.014, hyp_len=23484, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.11.2.91-18.32.2.94-18.84.2.77-15.98.2.78-16.20.pth, rkmy
BLEU = 6.57, 36.0/13.0/3.6/1.1 (BP=1.000, ratio=1.010, hyp_len=23736, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.12.2.76-15.83.2.83-16.97.2.57-13.12.2.62-13.75.pth, myrk
BLEU = 11.62, 43.3/18.0/7.5/3.1 (BP=1.000, ratio=1.003, hyp_len=23219, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.12.2.76-15.83.2.83-16.97.2.57-13.12.2.62-13.75.pth, rkmy
BLEU = 9.10, 39.7/16.2/5.5/2.0 (BP=1.000, ratio=1.003, hyp_len=23582, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.13.2.51-12.36.2.59-13.37.2.38-10.81.2.42-11.23.pth, myrk
BLEU = 15.79, 47.9/23.1/11.0/5.1 (BP=1.000, ratio=1.003, hyp_len=23225, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.13.2.51-12.36.2.59-13.37.2.38-10.81.2.42-11.23.pth, rkmy
BLEU = 11.31, 42.5/18.9/7.2/2.8 (BP=1.000, ratio=1.021, hyp_len=23998, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.14.2.30-9.94.2.37-10.66.2.21-9.11.2.22-9.19.pth, myrk
BLEU = 17.53, 50.0/25.3/12.5/6.0 (BP=1.000, ratio=1.018, hyp_len=23576, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.14.2.30-9.94.2.37-10.66.2.21-9.11.2.22-9.19.pth, rkmy
BLEU = 14.81, 47.0/22.9/10.0/4.5 (BP=1.000, ratio=1.011, hyp_len=23769, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.15.2.16-8.70.2.22-9.17.2.05-7.78.2.08-8.00.pth, myrk
BLEU = 21.63, 53.6/29.3/16.1/8.7 (BP=1.000, ratio=1.015, hyp_len=23512, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.15.2.16-8.70.2.22-9.17.2.05-7.78.2.08-8.00.pth, rkmy
BLEU = 18.44, 50.7/26.8/13.1/6.5 (BP=1.000, ratio=1.034, hyp_len=24301, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.16.2.01-7.48.2.02-7.54.1.95-7.02.1.94-6.95.pth, myrk
BLEU = 24.90, 56.7/32.9/19.0/10.9 (BP=1.000, ratio=1.010, hyp_len=23392, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.16.2.01-7.48.2.02-7.54.1.95-7.02.1.94-6.95.pth, rkmy
BLEU = 22.06, 54.2/30.6/16.2/8.8 (BP=1.000, ratio=1.041, hyp_len=24481, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.17.1.86-6.41.1.84-6.30.1.82-6.17.1.75-5.77.pth, myrk
BLEU = 28.82, 59.5/36.8/22.8/13.8 (BP=1.000, ratio=1.031, hyp_len=23876, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.17.1.86-6.41.1.84-6.30.1.82-6.17.1.75-5.77.pth, rkmy
BLEU = 28.21, 59.5/36.7/22.0/13.2 (BP=1.000, ratio=1.012, hyp_len=23801, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.18.1.65-5.22.1.61-4.98.1.69-5.44.1.62-5.04.pth, myrk
BLEU = 31.85, 62.4/40.2/25.6/16.0 (BP=1.000, ratio=1.028, hyp_len=23818, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.18.1.65-5.22.1.61-4.98.1.69-5.44.1.62-5.04.pth, rkmy
BLEU = 32.38, 63.1/40.9/25.8/16.5 (BP=1.000, ratio=1.013, hyp_len=23822, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.19.1.60-4.97.1.57-4.81.1.57-4.82.1.55-4.70.pth, myrk
BLEU = 36.84, 66.3/45.0/30.4/20.3 (BP=1.000, ratio=1.009, hyp_len=23359, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.19.1.60-4.97.1.57-4.81.1.57-4.82.1.55-4.70.pth, rkmy
BLEU = 37.02, 66.8/45.6/30.5/20.5 (BP=0.997, ratio=0.997, hyp_len=23427, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.20.1.50-4.49.1.49-4.42.1.52-4.59.1.47-4.33.pth, myrk
BLEU = 39.22, 68.5/47.4/32.9/22.9 (BP=0.992, ratio=0.992, hyp_len=22974, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.20.1.50-4.49.1.49-4.42.1.52-4.59.1.47-4.33.pth, rkmy
BLEU = 40.85, 68.6/48.8/34.2/24.3 (BP=1.000, ratio=1.021, hyp_len=24004, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.21.1.37-3.94.1.47-4.35.1.37-3.94.1.37-3.92.pth, myrk
BLEU = 45.29, 71.8/52.7/38.9/28.6 (BP=1.000, ratio=1.014, hyp_len=23495, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.21.1.37-3.94.1.47-4.35.1.37-3.94.1.37-3.92.pth, rkmy
BLEU = 43.78, 70.8/51.8/37.1/27.0 (BP=1.000, ratio=1.023, hyp_len=24039, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.22.1.30-3.66.1.39-4.00.1.37-3.94.1.35-3.86.pth, myrk
BLEU = 46.38, 72.6/53.9/40.0/29.6 (BP=1.000, ratio=1.032, hyp_len=23910, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.22.1.30-3.66.1.39-4.00.1.37-3.94.1.35-3.86.pth, rkmy
BLEU = 44.10, 71.1/52.1/37.5/27.3 (BP=1.000, ratio=1.014, hyp_len=23845, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.23.1.14-3.14.1.21-3.37.1.26-3.53.1.25-3.48.pth, myrk
BLEU = 50.99, 75.3/58.0/44.8/34.6 (BP=1.000, ratio=1.021, hyp_len=23646, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.23.1.14-3.14.1.21-3.37.1.26-3.53.1.25-3.48.pth, rkmy
BLEU = 48.59, 74.0/56.1/42.1/31.9 (BP=1.000, ratio=1.010, hyp_len=23737, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.24.1.11-3.03.1.11-3.03.1.24-3.47.1.16-3.20.pth, myrk
BLEU = 53.05, 76.7/59.8/46.9/36.9 (BP=1.000, ratio=1.009, hyp_len=23376, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.24.1.11-3.03.1.11-3.03.1.24-3.47.1.16-3.20.pth, rkmy
BLEU = 53.21, 76.4/60.3/46.9/37.1 (BP=1.000, ratio=1.019, hyp_len=23960, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.25.1.18-3.26.1.01-2.76.1.19-3.29.1.08-2.95.pth, myrk
BLEU = 54.77, 77.5/61.2/48.8/38.9 (BP=1.000, ratio=1.014, hyp_len=23490, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.25.1.18-3.26.1.01-2.76.1.19-3.29.1.08-2.95.pth, rkmy
BLEU = 57.42, 79.0/64.0/51.3/41.9 (BP=1.000, ratio=1.014, hyp_len=23836, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.26.0.99-2.70.0.96-2.60.1.09-2.97.1.05-2.86.pth, myrk
BLEU = 58.10, 79.6/64.2/52.3/42.6 (BP=1.000, ratio=1.011, hyp_len=23414, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.26.0.99-2.70.0.96-2.60.1.09-2.97.1.05-2.86.pth, rkmy
BLEU = 57.19, 78.8/64.0/51.1/41.6 (BP=1.000, ratio=1.028, hyp_len=24167, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.27.0.93-2.52.0.90-2.47.1.08-2.93.1.02-2.79.pth, myrk
BLEU = 59.44, 80.5/65.5/53.7/44.2 (BP=1.000, ratio=1.010, hyp_len=23396, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.27.0.93-2.52.0.90-2.47.1.08-2.93.1.02-2.79.pth, rkmy
BLEU = 60.42, 80.7/66.6/54.6/45.4 (BP=1.000, ratio=1.013, hyp_len=23804, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.28.1.12-3.05.0.90-2.45.1.16-3.21.0.97-2.64.pth, myrk
BLEU = 53.63, 76.4/60.2/47.6/37.8 (BP=1.000, ratio=1.023, hyp_len=23686, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.28.1.12-3.05.0.90-2.45.1.16-3.21.0.97-2.64.pth, rkmy
BLEU = 61.98, 81.5/68.0/56.2/47.3 (BP=1.000, ratio=1.018, hyp_len=23939, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.29.1.01-2.73.0.84-2.31.1.05-2.86.0.96-2.61.pth, myrk
BLEU = 59.62, 80.4/65.6/53.9/44.4 (BP=1.000, ratio=1.013, hyp_len=23461, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.29.1.01-2.73.0.84-2.31.1.05-2.86.0.96-2.61.pth, rkmy
BLEU = 63.44, 82.3/69.3/57.9/49.1 (BP=1.000, ratio=1.014, hyp_len=23847, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.30.0.97-2.65.0.82-2.26.1.01-2.74.0.93-2.53.pth, myrk
BLEU = 61.62, 81.7/67.3/56.0/46.8 (BP=1.000, ratio=1.007, hyp_len=23317, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.30.0.97-2.65.0.82-2.26.1.01-2.74.0.93-2.53.pth, rkmy
BLEU = 63.89, 82.3/69.6/58.4/49.8 (BP=1.000, ratio=1.021, hyp_len=24001, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.31.0.89-2.44.1.20-3.32.0.95-2.57.1.08-2.93.pth, myrk
BLEU = 64.71, 83.3/70.0/59.4/50.6 (BP=1.000, ratio=1.010, hyp_len=23399, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.31.0.89-2.44.1.20-3.32.0.95-2.57.1.08-2.93.pth, rkmy
BLEU = 58.15, 79.3/64.6/52.1/42.8 (BP=1.000, ratio=1.013, hyp_len=23816, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.32.0.79-2.20.0.89-2.44.0.96-2.60.0.94-2.55.pth, myrk
BLEU = 64.10, 82.9/69.5/58.8/49.8 (BP=1.000, ratio=1.011, hyp_len=23410, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.32.0.79-2.20.0.89-2.44.0.96-2.60.0.94-2.55.pth, rkmy
BLEU = 64.23, 82.5/69.8/58.8/50.2 (BP=1.000, ratio=1.016, hyp_len=23890, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.33.0.74-2.09.0.73-2.08.0.91-2.49.0.88-2.40.pth, myrk
BLEU = 65.91, 83.7/71.1/60.8/52.2 (BP=1.000, ratio=1.015, hyp_len=23504, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.33.0.74-2.09.0.73-2.08.0.91-2.49.0.88-2.40.pth, rkmy
BLEU = 66.07, 83.5/71.5/60.8/52.5 (BP=1.000, ratio=1.024, hyp_len=24067, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.34.0.68-1.97.0.67-1.95.0.89-2.42.0.85-2.33.pth, myrk
BLEU = 66.71, 84.1/71.8/61.6/53.2 (BP=1.000, ratio=1.020, hyp_len=23621, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.34.0.68-1.97.0.67-1.95.0.89-2.42.0.85-2.33.pth, rkmy
BLEU = 67.72, 84.3/72.9/62.6/54.6 (BP=1.000, ratio=1.021, hyp_len=23995, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.35.0.65-1.92.0.68-1.97.0.87-2.38.0.85-2.33.pth, myrk
BLEU = 67.84, 84.7/72.8/62.9/54.6 (BP=1.000, ratio=1.018, hyp_len=23587, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.35.0.65-1.92.0.68-1.97.0.87-2.38.0.85-2.33.pth, rkmy
BLEU = 68.26, 84.6/73.4/63.3/55.3 (BP=1.000, ratio=1.017, hyp_len=23917, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.36.0.64-1.90.0.69-2.00.0.87-2.40.0.84-2.32.pth, myrk
BLEU = 67.94, 84.6/72.8/63.1/54.8 (BP=1.000, ratio=1.024, hyp_len=23717, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.36.0.64-1.90.0.69-2.00.0.87-2.40.0.84-2.32.pth, rkmy
BLEU = 68.82, 85.0/73.9/63.9/55.9 (BP=1.000, ratio=1.015, hyp_len=23856, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.37.0.64-1.89.0.79-2.19.0.85-2.33.1.00-2.71.pth, myrk
BLEU = 68.59, 85.2/73.5/63.7/55.5 (BP=1.000, ratio=1.018, hyp_len=23571, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.37.0.64-1.89.0.79-2.19.0.85-2.33.1.00-2.71.pth, rkmy
BLEU = 65.18, 83.4/70.7/59.8/51.2 (BP=1.000, ratio=1.005, hyp_len=23627, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.38.0.61-1.85.0.75-2.13.0.84-2.31.0.85-2.35.pth, myrk
BLEU = 69.56, 85.5/74.2/64.9/56.8 (BP=1.000, ratio=1.016, hyp_len=23525, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.38.0.61-1.85.0.75-2.13.0.84-2.31.0.85-2.35.pth, rkmy
BLEU = 67.25, 84.0/72.4/62.2/54.1 (BP=1.000, ratio=1.022, hyp_len=24036, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.39.0.58-1.79.0.61-1.84.0.84-2.31.0.80-2.22.pth, myrk
BLEU = 69.52, 85.6/74.2/64.8/56.7 (BP=1.000, ratio=1.021, hyp_len=23636, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.39.0.58-1.79.0.61-1.84.0.84-2.31.0.80-2.22.pth, rkmy
BLEU = 69.55, 85.2/74.4/64.7/57.1 (BP=1.000, ratio=1.021, hyp_len=24003, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.40.0.98-2.68.0.68-1.97.1.02-2.77.0.78-2.18.pth, myrk
BLEU = 60.29, 80.6/66.6/54.6/45.0 (BP=1.000, ratio=1.021, hyp_len=23650, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.40.0.98-2.68.0.68-1.97.1.02-2.77.0.78-2.18.pth, rkmy
BLEU = 70.80, 85.8/75.4/66.1/58.8 (BP=1.000, ratio=1.022, hyp_len=24024, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.41.0.75-2.11.0.57-1.76.0.85-2.34.0.76-2.15.pth, myrk
BLEU = 65.66, 83.5/71.0/60.5/51.8 (BP=1.000, ratio=1.031, hyp_len=23885, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.41.0.75-2.11.0.57-1.76.0.85-2.34.0.76-2.15.pth, rkmy
BLEU = 71.16, 86.1/75.8/66.5/59.2 (BP=1.000, ratio=1.025, hyp_len=24108, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.42.0.57-1.77.0.54-1.71.0.80-2.23.0.77-2.16.pth, myrk
BLEU = 69.46, 85.5/74.1/64.8/56.7 (BP=1.000, ratio=1.021, hyp_len=23652, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.42.0.57-1.77.0.54-1.71.0.80-2.23.0.77-2.16.pth, rkmy
BLEU = 71.05, 86.0/75.7/66.3/59.0 (BP=1.000, ratio=1.025, hyp_len=24105, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.43.0.55-1.73.0.54-1.72.0.79-2.21.0.77-2.15.pth, myrk
BLEU = 70.06, 85.6/74.6/65.5/57.6 (BP=1.000, ratio=1.023, hyp_len=23703, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.43.0.55-1.73.0.54-1.72.0.79-2.21.0.77-2.15.pth, rkmy
BLEU = 71.12, 85.9/75.7/66.5/59.2 (BP=1.000, ratio=1.028, hyp_len=24170, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.44.0.51-1.67.0.52-1.68.0.79-2.19.0.79-2.20.pth, myrk
BLEU = 69.91, 85.4/74.5/65.3/57.5 (BP=1.000, ratio=1.029, hyp_len=23834, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.44.0.51-1.67.0.52-1.68.0.79-2.19.0.79-2.20.pth, rkmy
BLEU = 70.98, 85.8/75.6/66.3/59.0 (BP=1.000, ratio=1.025, hyp_len=24097, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.45.0.51-1.67.0.54-1.72.0.76-2.14.0.78-2.18.pth, myrk
BLEU = 71.31, 86.3/75.6/66.8/59.3 (BP=1.000, ratio=1.020, hyp_len=23622, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.45.0.51-1.67.0.54-1.72.0.76-2.14.0.78-2.18.pth, rkmy
BLEU = 69.78, 85.0/74.6/65.0/57.5 (BP=1.000, ratio=1.041, hyp_len=24465, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.46.0.48-1.62.0.50-1.64.0.77-2.15.0.74-2.09.pth, myrk
BLEU = 71.83, 86.5/76.1/67.5/59.9 (BP=1.000, ratio=1.022, hyp_len=23670, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.46.0.48-1.62.0.50-1.64.0.77-2.15.0.74-2.09.pth, rkmy
BLEU = 72.34, 86.5/76.7/67.8/60.8 (BP=1.000, ratio=1.027, hyp_len=24139, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.47.0.46-1.59.0.48-1.61.0.76-2.13.0.74-2.10.pth, myrk
BLEU = 71.29, 86.1/75.6/66.8/59.4 (BP=1.000, ratio=1.025, hyp_len=23748, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.47.0.46-1.59.0.48-1.61.0.76-2.13.0.74-2.10.pth, rkmy
BLEU = 73.21, 87.1/77.5/68.8/61.9 (BP=1.000, ratio=1.020, hyp_len=23973, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.48.0.48-1.61.0.51-1.67.0.76-2.13.0.75-2.11.pth, myrk
BLEU = 71.54, 86.2/75.8/67.1/59.7 (BP=1.000, ratio=1.025, hyp_len=23747, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.48.0.48-1.61.0.51-1.67.0.76-2.13.0.75-2.11.pth, rkmy
BLEU = 71.06, 86.0/75.8/66.4/58.9 (BP=1.000, ratio=1.034, hyp_len=24301, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.49.0.45-1.56.0.50-1.65.0.74-2.10.0.76-2.13.pth, myrk
BLEU = 73.02, 87.3/77.1/68.7/61.5 (BP=1.000, ratio=1.019, hyp_len=23595, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.49.0.45-1.56.0.50-1.65.0.74-2.10.0.76-2.13.pth, rkmy
BLEU = 71.92, 86.2/76.4/67.4/60.2 (BP=1.000, ratio=1.031, hyp_len=24228, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.50.0.46-1.59.0.60-1.83.0.76-2.13.0.79-2.20.pth, myrk
BLEU = 71.93, 86.4/76.1/67.6/60.2 (BP=1.000, ratio=1.026, hyp_len=23754, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.50.0.46-1.59.0.60-1.83.0.76-2.13.0.79-2.20.pth, rkmy
BLEU = 71.72, 86.3/76.2/67.1/60.0 (BP=1.000, ratio=1.019, hyp_len=23966, ref_len=23509)
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

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/myrk-60epoch
Evaluation result for the model: dsl-model-myrk.01.4.40-81.71.4.52-91.71.4.03-56.03.4.14-62.49.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 14.7/0.2/0.0/0.0 (BP=1.000, ratio=1.042, hyp_len=24142, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.01.4.40-81.71.4.52-91.71.4.03-56.03.4.14-62.49.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 15.4/0.7/0.0/0.0 (BP=1.000, ratio=1.060, hyp_len=24924, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.02.4.09-60.01.4.18-65.07.3.87-47.93.3.93-51.15.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 19.8/1.6/0.0/0.0 (BP=1.000, ratio=1.017, hyp_len=23544, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.02.4.09-60.01.4.18-65.07.3.87-47.93.3.93-51.15.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 19.8/2.3/0.0/0.0 (BP=0.987, ratio=0.987, hyp_len=23206, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.03.4.01-54.96.4.08-58.87.3.79-44.21.3.84-46.64.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 19.5/1.9/0.0/0.0 (BP=1.000, ratio=1.011, hyp_len=23409, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.03.4.01-54.96.4.08-58.87.3.79-44.21.3.84-46.64.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 19.0/1.1/0.0/0.0 (BP=0.983, ratio=0.983, hyp_len=23110, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.04.3.89-48.82.3.94-51.50.3.67-39.28.3.71-40.94.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.6/1.9/0.0/0.0 (BP=0.996, ratio=0.996, hyp_len=23060, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.04.3.89-48.82.3.94-51.50.3.67-39.28.3.71-40.94.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.4/2.6/0.0/0.0 (BP=0.979, ratio=0.979, hyp_len=23026, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.05.3.86-47.41.3.89-49.10.3.57-35.69.3.61-36.92.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 24.7/3.4/0.2/0.0 (BP=1.000, ratio=1.007, hyp_len=23311, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.05.3.86-47.41.3.89-49.10.3.57-35.69.3.61-36.92.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 21.9/3.1/0.2/0.0 (BP=1.000, ratio=1.015, hyp_len=23872, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.06.3.75-42.62.3.78-43.82.3.50-33.12.3.54-34.50.pth, myrk
BLEU = 0.86, 24.8/4.2/0.3/0.0 (BP=1.000, ratio=1.016, hyp_len=23531, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.06.3.75-42.62.3.78-43.82.3.50-33.12.3.54-34.50.pth, rkmy
BLEU = 1.12, 24.6/5.5/0.7/0.0 (BP=0.986, ratio=0.986, hyp_len=23172, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.07.3.62-37.50.3.58-35.77.3.36-28.85.3.25-25.73.pth, myrk
BLEU = 1.91, 29.9/7.4/1.4/0.0 (BP=1.000, ratio=1.009, hyp_len=23379, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.07.3.62-37.50.3.58-35.77.3.36-28.85.3.25-25.73.pth, rkmy
BLEU = 1.49, 28.7/8.2/1.3/0.0 (BP=0.994, ratio=0.994, hyp_len=23372, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.08.3.48-32.31.3.29-26.78.3.20-24.58.3.02-20.42.pth, myrk
BLEU = 2.77, 33.2/9.4/1.7/0.1 (BP=1.000, ratio=1.009, hyp_len=23364, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.08.3.48-32.31.3.29-26.78.3.20-24.58.3.02-20.42.pth, rkmy
BLEU = 4.02, 31.0/9.9/1.9/0.5 (BP=1.000, ratio=1.019, hyp_len=23955, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.09.3.27-26.33.3.05-21.08.3.11-22.48.2.81-16.62.pth, myrk
BLEU = 4.37, 35.6/12.1/2.6/0.3 (BP=1.000, ratio=1.026, hyp_len=23751, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.09.3.27-26.33.3.05-21.08.3.11-22.48.2.81-16.62.pth, rkmy
BLEU = 6.64, 36.5/13.2/3.7/1.1 (BP=1.000, ratio=1.001, hyp_len=23525, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.10.3.16-23.51.2.87-17.63.2.96-19.26.2.61-13.63.pth, myrk
BLEU = 7.95, 39.4/15.3/4.9/1.4 (BP=1.000, ratio=1.004, hyp_len=23247, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.10.3.16-23.51.2.87-17.63.2.96-19.26.2.61-13.63.pth, rkmy
BLEU = 8.69, 38.5/15.8/5.3/1.8 (BP=1.000, ratio=1.034, hyp_len=24312, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.11.2.93-18.79.2.61-13.55.2.71-15.06.2.40-11.07.pth, myrk
BLEU = 11.35, 43.9/18.9/7.4/2.7 (BP=1.000, ratio=1.012, hyp_len=23431, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.11.2.93-18.79.2.61-13.55.2.71-15.06.2.40-11.07.pth, rkmy
BLEU = 11.99, 43.7/19.4/7.7/3.2 (BP=1.000, ratio=1.017, hyp_len=23910, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.12.2.71-15.10.2.29-9.88.2.51-12.31.2.13-8.45.pth, myrk
BLEU = 14.25, 47.5/22.3/9.7/4.1 (BP=0.996, ratio=0.996, hyp_len=23074, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.12.2.71-15.10.2.29-9.88.2.51-12.31.2.13-8.45.pth, rkmy
BLEU = 16.94, 49.1/25.0/11.8/5.7 (BP=1.000, ratio=1.020, hyp_len=23990, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.13.2.48-11.89.2.09-8.06.2.44-11.49.2.02-7.54.pth, myrk
BLEU = 15.60, 50.1/24.4/10.8/4.7 (BP=0.989, ratio=0.989, hyp_len=22915, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.13.2.48-11.89.2.09-8.06.2.44-11.49.2.02-7.54.pth, rkmy
BLEU = 20.27, 53.1/28.6/14.7/7.7 (BP=0.995, ratio=0.995, hyp_len=23393, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.14.2.32-10.17.1.92-6.85.2.21-9.13.1.84-6.30.pth, myrk
BLEU = 20.45, 53.7/28.7/14.9/7.6 (BP=1.000, ratio=1.007, hyp_len=23319, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.14.2.32-10.17.1.92-6.85.2.21-9.13.1.84-6.30.pth, rkmy
BLEU = 26.65, 59.2/35.5/20.6/11.9 (BP=0.995, ratio=0.995, hyp_len=23382, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.15.2.10-8.16.1.72-5.57.2.07-7.95.1.68-5.38.pth, myrk
BLEU = 24.43, 57.8/33.1/18.3/10.1 (BP=1.000, ratio=1.000, hyp_len=23161, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.15.2.10-8.16.1.72-5.57.2.07-7.95.1.68-5.38.pth, rkmy
BLEU = 29.60, 60.6/38.1/23.2/14.3 (BP=1.000, ratio=1.036, hyp_len=24358, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.16.2.08-8.00.1.67-5.32.1.98-7.22.1.60-4.95.pth, myrk
BLEU = 27.78, 60.8/36.6/21.7/12.7 (BP=0.992, ratio=0.992, hyp_len=22977, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.16.2.08-8.00.1.67-5.32.1.98-7.22.1.60-4.95.pth, rkmy
BLEU = 34.11, 64.2/42.6/27.6/18.0 (BP=1.000, ratio=1.020, hyp_len=23972, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.17.2.01-7.46.1.61-4.99.1.94-6.99.1.50-4.49.pth, myrk
BLEU = 29.48, 60.9/37.7/23.1/14.2 (BP=1.000, ratio=1.004, hyp_len=23264, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.17.2.01-7.46.1.61-4.99.1.94-6.99.1.50-4.49.pth, rkmy
BLEU = 38.38, 67.4/46.9/31.7/21.7 (BP=1.000, ratio=1.017, hyp_len=23910, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.18.1.77-5.86.1.34-3.81.1.78-5.92.1.33-3.78.pth, myrk
BLEU = 34.36, 64.9/42.4/27.8/18.2 (BP=1.000, ratio=1.002, hyp_len=23212, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.18.1.77-5.86.1.34-3.81.1.78-5.92.1.33-3.78.pth, rkmy
BLEU = 46.09, 72.5/53.9/39.5/29.2 (BP=1.000, ratio=1.012, hyp_len=23790, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.19.1.69-5.41.1.23-3.41.1.78-5.94.1.29-3.64.pth, myrk
BLEU = 35.67, 66.1/43.9/29.2/19.5 (BP=0.995, ratio=0.995, hyp_len=23045, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.19.1.69-5.41.1.23-3.41.1.78-5.94.1.29-3.64.pth, rkmy
BLEU = 47.90, 73.1/55.6/41.4/31.3 (BP=1.000, ratio=1.035, hyp_len=24337, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.20.1.69-5.42.1.18-3.26.1.90-6.70.1.26-3.51.pth, myrk
BLEU = 28.23, 60.5/36.8/21.9/13.1 (BP=1.000, ratio=1.017, hyp_len=23553, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.20.1.69-5.42.1.18-3.26.1.90-6.70.1.26-3.51.pth, rkmy
BLEU = 48.94, 74.6/57.0/42.4/31.8 (BP=1.000, ratio=1.010, hyp_len=23743, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.21.1.72-5.56.1.21-3.35.1.63-5.09.1.16-3.20.pth, myrk
BLEU = 38.31, 67.4/46.2/31.6/21.9 (BP=1.000, ratio=1.011, hyp_len=23413, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.21.1.72-5.56.1.21-3.35.1.63-5.09.1.16-3.20.pth, rkmy
BLEU = 54.06, 76.9/60.9/47.9/38.1 (BP=1.000, ratio=1.016, hyp_len=23883, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.22.1.70-5.49.1.14-3.12.1.62-5.05.1.09-2.96.pth, myrk
BLEU = 40.57, 69.3/48.3/33.8/23.9 (BP=1.000, ratio=1.002, hyp_len=23210, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.22.1.70-5.49.1.14-3.12.1.62-5.05.1.09-2.96.pth, rkmy
BLEU = 57.24, 78.9/63.9/51.3/41.5 (BP=1.000, ratio=1.015, hyp_len=23864, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.23.1.44-4.21.1.02-2.76.1.54-4.65.1.07-2.92.pth, myrk
BLEU = 42.20, 70.3/49.9/35.5/25.4 (BP=1.000, ratio=1.006, hyp_len=23290, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.23.1.44-4.21.1.02-2.76.1.54-4.65.1.07-2.92.pth, rkmy
BLEU = 58.13, 79.4/64.7/52.2/42.6 (BP=1.000, ratio=1.023, hyp_len=24040, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.24.1.43-4.18.1.04-2.82.1.49-4.45.1.08-2.95.pth, myrk
BLEU = 45.77, 72.4/53.2/39.2/29.1 (BP=1.000, ratio=1.013, hyp_len=23452, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.24.1.43-4.18.1.04-2.82.1.49-4.45.1.08-2.95.pth, rkmy
BLEU = 59.17, 80.1/65.6/53.3/43.7 (BP=1.000, ratio=1.011, hyp_len=23761, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.25.1.30-3.66.0.92-2.50.1.42-4.15.1.00-2.71.pth, myrk
BLEU = 49.12, 74.8/56.2/42.6/32.5 (BP=1.000, ratio=1.005, hyp_len=23281, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.25.1.30-3.66.0.92-2.50.1.42-4.15.1.00-2.71.pth, rkmy
BLEU = 61.66, 81.2/67.6/56.1/47.0 (BP=1.000, ratio=1.019, hyp_len=23944, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.26.1.22-3.38.0.93-2.54.1.36-3.91.1.01-2.76.pth, myrk
BLEU = 50.59, 75.4/57.5/44.2/34.2 (BP=1.000, ratio=1.015, hyp_len=23509, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.26.1.22-3.38.0.93-2.54.1.36-3.91.1.01-2.76.pth, rkmy
BLEU = 60.15, 80.3/66.4/54.5/45.1 (BP=1.000, ratio=1.022, hyp_len=24019, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.27.1.17-3.22.0.94-2.55.1.36-3.91.0.98-2.67.pth, myrk
BLEU = 52.97, 77.3/59.9/46.7/36.4 (BP=1.000, ratio=1.002, hyp_len=23197, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.27.1.17-3.22.0.94-2.55.1.36-3.91.0.98-2.67.pth, rkmy
BLEU = 60.95, 80.5/67.0/55.3/46.2 (BP=1.000, ratio=1.020, hyp_len=23971, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.28.1.11-3.03.0.82-2.28.1.30-3.66.0.94-2.55.pth, myrk
BLEU = 54.60, 78.0/61.1/48.4/38.5 (BP=1.000, ratio=1.004, hyp_len=23252, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.28.1.11-3.03.0.82-2.28.1.30-3.66.0.94-2.55.pth, rkmy
BLEU = 64.26, 82.6/69.9/58.8/50.2 (BP=1.000, ratio=1.023, hyp_len=24046, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.29.1.02-2.77.0.76-2.15.1.25-3.50.0.89-2.44.pth, myrk
BLEU = 57.31, 79.5/63.5/51.3/41.6 (BP=1.000, ratio=1.006, hyp_len=23300, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.29.1.02-2.77.0.76-2.15.1.25-3.50.0.89-2.44.pth, rkmy
BLEU = 65.35, 83.2/70.9/60.0/51.5 (BP=1.000, ratio=1.025, hyp_len=24086, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.30.0.97-2.64.0.73-2.06.1.25-3.49.0.89-2.43.pth, myrk
BLEU = 57.46, 79.8/63.9/51.5/41.6 (BP=1.000, ratio=1.008, hyp_len=23346, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.30.0.97-2.64.0.73-2.06.1.25-3.49.0.89-2.43.pth, rkmy
BLEU = 66.02, 83.6/71.5/60.8/52.3 (BP=1.000, ratio=1.023, hyp_len=24040, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.31.0.95-2.59.0.67-1.96.1.20-3.33.0.84-2.32.pth, myrk
BLEU = 59.19, 80.3/65.2/53.4/44.0 (BP=1.000, ratio=1.017, hyp_len=23545, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.31.0.95-2.59.0.67-1.96.1.20-3.33.0.84-2.32.pth, rkmy
BLEU = 67.89, 84.7/73.1/62.7/54.6 (BP=1.000, ratio=1.020, hyp_len=23980, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.32.1.46-4.30.0.80-2.23.1.33-3.79.0.84-2.32.pth, myrk
BLEU = 50.74, 75.5/57.8/44.4/34.2 (BP=1.000, ratio=1.027, hyp_len=23789, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.32.1.46-4.30.0.80-2.23.1.33-3.79.0.84-2.32.pth, rkmy
BLEU = 67.25, 84.1/72.5/62.1/54.0 (BP=1.000, ratio=1.026, hyp_len=24124, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.33.1.08-2.95.0.68-1.96.1.16-3.20.0.83-2.30.pth, myrk
BLEU = 57.43, 79.7/63.9/51.5/41.5 (BP=1.000, ratio=1.003, hyp_len=23240, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.33.1.08-2.95.0.68-1.96.1.16-3.20.0.83-2.30.pth, rkmy
BLEU = 68.27, 84.6/73.4/63.3/55.3 (BP=1.000, ratio=1.027, hyp_len=24155, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.34.0.95-2.58.0.64-1.89.1.13-3.11.0.84-2.32.pth, myrk
BLEU = 59.92, 80.7/66.0/54.2/44.6 (BP=1.000, ratio=1.020, hyp_len=23622, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.34.0.95-2.58.0.64-1.89.1.13-3.11.0.84-2.32.pth, rkmy
BLEU = 68.57, 84.9/73.7/63.5/55.7 (BP=1.000, ratio=1.020, hyp_len=23987, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.35.0.86-2.37.0.85-2.35.1.07-2.90.1.00-2.71.pth, myrk
BLEU = 62.43, 82.1/68.1/56.9/47.7 (BP=1.000, ratio=1.014, hyp_len=23480, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.35.0.86-2.37.0.85-2.35.1.07-2.90.1.00-2.71.pth, rkmy
BLEU = 60.09, 78.9/66.3/54.8/45.5 (BP=1.000, ratio=1.071, hyp_len=25188, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.36.0.85-2.34.0.88-2.41.1.06-2.88.1.16-3.19.pth, myrk
BLEU = 64.19, 83.2/69.6/58.8/49.8 (BP=1.000, ratio=1.008, hyp_len=23353, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.36.0.85-2.34.0.88-2.41.1.06-2.88.1.16-3.19.pth, rkmy
BLEU = 54.02, 74.4/60.7/48.4/38.9 (BP=1.000, ratio=1.112, hyp_len=26137, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.37.0.75-2.12.0.64-1.89.1.05-2.85.0.80-2.22.pth, myrk
BLEU = 63.82, 83.0/69.3/58.4/49.4 (BP=1.000, ratio=1.010, hyp_len=23390, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.37.0.75-2.12.0.64-1.89.1.05-2.85.0.80-2.22.pth, rkmy
BLEU = 68.54, 84.8/73.6/63.6/55.6 (BP=1.000, ratio=1.028, hyp_len=24168, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.38.0.74-2.10.0.58-1.79.1.06-2.88.0.77-2.16.pth, myrk
BLEU = 63.65, 82.8/69.2/58.2/49.2 (BP=1.000, ratio=1.016, hyp_len=23542, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.38.0.74-2.10.0.58-1.79.1.06-2.88.0.77-2.16.pth, rkmy
BLEU = 70.30, 85.6/75.1/65.5/58.0 (BP=1.000, ratio=1.027, hyp_len=24142, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.39.0.73-2.07.0.55-1.74.1.03-2.81.0.76-2.14.pth, myrk
BLEU = 65.19, 83.5/70.6/59.9/51.1 (BP=1.000, ratio=1.018, hyp_len=23571, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.39.0.73-2.07.0.55-1.74.1.03-2.81.0.76-2.14.pth, rkmy
BLEU = 70.21, 85.4/74.9/65.5/58.0 (BP=1.000, ratio=1.032, hyp_len=24255, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.40.0.73-2.08.0.56-1.75.1.02-2.77.0.75-2.13.pth, myrk
BLEU = 65.71, 83.7/70.9/60.5/51.9 (BP=1.000, ratio=1.019, hyp_len=23591, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.40.0.73-2.08.0.56-1.75.1.02-2.77.0.75-2.13.pth, rkmy
BLEU = 71.29, 86.1/75.9/66.6/59.3 (BP=1.000, ratio=1.027, hyp_len=24140, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.41.0.66-1.94.0.50-1.65.1.04-2.82.0.75-2.12.pth, myrk
BLEU = 64.93, 83.7/70.3/59.6/50.7 (BP=1.000, ratio=1.014, hyp_len=23477, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.41.0.66-1.94.0.50-1.65.1.04-2.82.0.75-2.12.pth, rkmy
BLEU = 71.77, 86.4/76.4/67.1/59.9 (BP=1.000, ratio=1.026, hyp_len=24121, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.42.0.73-2.08.0.53-1.70.1.03-2.81.0.74-2.10.pth, myrk
BLEU = 63.96, 82.9/69.6/58.6/49.4 (BP=1.000, ratio=1.027, hyp_len=23779, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.42.0.73-2.08.0.53-1.70.1.03-2.81.0.74-2.10.pth, rkmy
BLEU = 71.40, 86.0/75.9/66.8/59.6 (BP=1.000, ratio=1.030, hyp_len=24220, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.43.0.70-2.01.0.50-1.64.1.04-2.84.0.74-2.09.pth, myrk
BLEU = 64.54, 82.9/70.0/59.3/50.4 (BP=1.000, ratio=1.023, hyp_len=23703, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.43.0.70-2.01.0.50-1.64.1.04-2.84.0.74-2.09.pth, rkmy
BLEU = 71.88, 86.3/76.3/67.3/60.2 (BP=1.000, ratio=1.031, hyp_len=24233, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.44.0.73-2.07.0.48-1.62.0.95-2.59.0.74-2.09.pth, myrk
BLEU = 66.78, 84.4/71.9/61.7/53.1 (BP=1.000, ratio=1.017, hyp_len=23546, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.44.0.73-2.07.0.48-1.62.0.95-2.59.0.74-2.09.pth, rkmy
BLEU = 72.02, 86.3/76.5/67.5/60.4 (BP=1.000, ratio=1.034, hyp_len=24299, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.45.0.68-1.96.0.48-1.61.0.96-2.60.0.73-2.07.pth, myrk
BLEU = 67.16, 84.6/72.3/62.1/53.6 (BP=1.000, ratio=1.019, hyp_len=23590, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.45.0.68-1.96.0.48-1.61.0.96-2.60.0.73-2.07.pth, rkmy
BLEU = 72.30, 86.6/76.7/67.8/60.7 (BP=1.000, ratio=1.029, hyp_len=24191, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.46.0.61-1.84.0.47-1.60.0.92-2.51.0.73-2.08.pth, myrk
BLEU = 68.43, 85.1/73.2/63.5/55.4 (BP=1.000, ratio=1.016, hyp_len=23536, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.46.0.61-1.84.0.47-1.60.0.92-2.51.0.73-2.08.pth, rkmy
BLEU = 71.64, 86.2/76.1/67.0/59.9 (BP=1.000, ratio=1.028, hyp_len=24174, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.47.0.59-1.80.0.47-1.61.0.92-2.51.0.72-2.06.pth, myrk
BLEU = 69.45, 85.6/74.1/64.7/56.7 (BP=1.000, ratio=1.016, hyp_len=23525, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.47.0.59-1.80.0.47-1.61.0.92-2.51.0.72-2.06.pth, rkmy
BLEU = 71.92, 86.3/76.3/67.4/60.3 (BP=1.000, ratio=1.034, hyp_len=24320, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.48.0.56-1.75.0.46-1.58.0.92-2.50.0.79-2.21.pth, myrk
BLEU = 69.56, 85.6/74.1/64.8/56.9 (BP=1.000, ratio=1.016, hyp_len=23530, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.48.0.56-1.75.0.46-1.58.0.92-2.50.0.79-2.21.pth, rkmy
BLEU = 69.51, 84.7/74.2/64.8/57.3 (BP=1.000, ratio=1.048, hyp_len=24645, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.49.0.58-1.79.0.56-1.75.0.94-2.56.0.74-2.09.pth, myrk
BLEU = 69.80, 85.8/74.4/65.1/57.1 (BP=1.000, ratio=1.016, hyp_len=23529, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.49.0.58-1.79.0.56-1.75.0.94-2.56.0.74-2.09.pth, rkmy
BLEU = 71.53, 86.1/76.0/66.9/59.8 (BP=1.000, ratio=1.032, hyp_len=24253, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.50.0.54-1.71.0.47-1.59.0.90-2.47.0.73-2.07.pth, myrk
BLEU = 70.61, 86.4/75.2/65.9/58.1 (BP=1.000, ratio=1.012, hyp_len=23443, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.50.0.54-1.71.0.47-1.59.0.90-2.47.0.73-2.07.pth, rkmy
BLEU = 71.81, 86.4/76.2/67.2/60.1 (BP=1.000, ratio=1.027, hyp_len=24150, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.51.0.52-1.68.0.46-1.58.0.90-2.46.0.73-2.08.pth, myrk
BLEU = 70.50, 86.1/75.0/65.9/58.1 (BP=1.000, ratio=1.020, hyp_len=23629, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.51.0.52-1.68.0.46-1.58.0.90-2.46.0.73-2.08.pth, rkmy
BLEU = 71.76, 86.2/76.2/67.2/60.1 (BP=1.000, ratio=1.027, hyp_len=24146, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.52.0.51-1.67.0.45-1.57.0.88-2.41.0.72-2.06.pth, myrk
BLEU = 70.19, 85.8/74.7/65.6/57.8 (BP=1.000, ratio=1.020, hyp_len=23618, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.52.0.51-1.67.0.45-1.57.0.88-2.41.0.72-2.06.pth, rkmy
BLEU = 72.80, 86.7/77.0/68.3/61.6 (BP=1.000, ratio=1.029, hyp_len=24181, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.53.0.50-1.65.0.42-1.53.0.88-2.40.0.72-2.06.pth, myrk
BLEU = 70.94, 86.2/75.3/66.4/58.8 (BP=1.000, ratio=1.018, hyp_len=23581, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.53.0.50-1.65.0.42-1.53.0.88-2.40.0.72-2.06.pth, rkmy
BLEU = 70.57, 85.2/75.1/65.9/58.8 (BP=1.000, ratio=1.048, hyp_len=24637, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.54.0.53-1.70.0.56-1.75.0.88-2.40.0.83-2.30.pth, myrk
BLEU = 71.09, 86.4/75.5/66.5/58.9 (BP=1.000, ratio=1.020, hyp_len=23621, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.54.0.53-1.70.0.56-1.75.0.88-2.40.0.83-2.30.pth, rkmy
BLEU = 69.66, 85.2/74.7/64.9/57.0 (BP=1.000, ratio=1.036, hyp_len=24356, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.55.0.49-1.64.0.45-1.57.0.88-2.42.0.73-2.07.pth, myrk
BLEU = 70.59, 86.0/75.1/66.0/58.3 (BP=1.000, ratio=1.019, hyp_len=23600, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.55.0.49-1.64.0.45-1.57.0.88-2.42.0.73-2.07.pth, rkmy
BLEU = 71.06, 85.8/75.7/66.4/59.1 (BP=1.000, ratio=1.035, hyp_len=24330, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.56.0.49-1.64.0.41-1.50.0.87-2.38.0.69-1.99.pth, myrk
BLEU = 70.60, 85.9/75.0/66.0/58.4 (BP=1.000, ratio=1.020, hyp_len=23628, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.56.0.49-1.64.0.41-1.50.0.87-2.38.0.69-1.99.pth, rkmy
BLEU = 73.73, 87.4/78.0/69.4/62.5 (BP=1.000, ratio=1.026, hyp_len=24121, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.57.0.52-1.69.0.39-1.47.0.88-2.42.0.69-1.99.pth, myrk
BLEU = 70.07, 85.6/74.6/65.4/57.7 (BP=1.000, ratio=1.025, hyp_len=23737, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.57.0.52-1.69.0.39-1.47.0.88-2.42.0.69-1.99.pth, rkmy
BLEU = 73.47, 87.1/77.6/69.1/62.4 (BP=1.000, ratio=1.034, hyp_len=24318, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.58.0.47-1.60.0.37-1.44.0.88-2.41.0.68-1.97.pth, myrk
BLEU = 70.27, 85.7/74.8/65.7/57.9 (BP=1.000, ratio=1.027, hyp_len=23778, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.58.0.47-1.60.0.37-1.44.0.88-2.41.0.68-1.97.pth, rkmy
BLEU = 73.44, 87.0/77.6/69.0/62.4 (BP=1.000, ratio=1.034, hyp_len=24311, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.59.0.60-1.81.0.38-1.47.0.91-2.50.0.68-1.97.pth, myrk
BLEU = 67.91, 84.6/72.8/63.0/54.9 (BP=1.000, ratio=1.029, hyp_len=23836, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.59.0.60-1.81.0.38-1.47.0.91-2.50.0.68-1.97.pth, rkmy
BLEU = 74.06, 87.4/78.2/69.7/63.2 (BP=1.000, ratio=1.031, hyp_len=24248, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.60.0.50-1.65.0.36-1.44.0.85-2.33.0.68-1.97.pth, myrk
BLEU = 71.40, 86.4/75.7/66.9/59.4 (BP=1.000, ratio=1.019, hyp_len=23608, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.60.0.50-1.65.0.36-1.44.0.85-2.33.0.68-1.97.pth, rkmy
BLEU = 73.70, 87.1/77.8/69.4/62.8 (BP=1.000, ratio=1.036, hyp_len=24346, ref_len=23509)
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

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/myrk-70epoch
Evaluation result for the model: dsl-model-myrk.01.4.45-85.26.4.46-86.32.4.05-57.59.4.07-58.35.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 13.7/0.1/0.0/0.0 (BP=1.000, ratio=1.004, hyp_len=23253, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.01.4.45-85.26.4.46-86.32.4.05-57.59.4.07-58.35.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 12.2/0.0/0.0/0.0 (BP=1.000, ratio=1.061, hyp_len=24953, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.02.4.18-65.65.4.21-67.21.3.90-49.54.3.91-49.90.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 17.5/2.2/0.0/0.0 (BP=1.000, ratio=1.036, hyp_len=24002, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.02.4.18-65.65.4.21-67.21.3.90-49.54.3.91-49.90.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 19.1/2.4/0.0/0.0 (BP=0.986, ratio=0.986, hyp_len=23177, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.03.4.02-55.83.4.05-57.16.3.81-45.08.3.81-45.08.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 21.1/1.7/0.0/0.0 (BP=0.998, ratio=0.998, hyp_len=23114, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.03.4.02-55.83.4.05-57.16.3.81-45.08.3.81-45.08.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 21.6/2.9/0.2/0.0 (BP=0.980, ratio=0.980, hyp_len=23033, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.04.3.96-52.62.3.95-52.08.3.71-40.94.3.70-40.58.pth, myrk
BLEU = 0.47, 24.4/2.7/0.1/0.0 (BP=1.000, ratio=1.007, hyp_len=23315, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.04.3.96-52.62.3.95-52.08.3.71-40.94.3.70-40.58.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.5/2.6/0.2/0.0 (BP=0.979, ratio=0.979, hyp_len=23016, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.05.3.86-47.36.3.87-48.16.3.60-36.55.3.61-37.11.pth, myrk
BLEU = 0.64, 24.0/3.4/0.2/0.0 (BP=1.000, ratio=1.019, hyp_len=23603, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.05.3.86-47.36.3.87-48.16.3.60-36.55.3.61-37.11.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.5/4.1/0.4/0.0 (BP=0.977, ratio=0.977, hyp_len=22978, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.06.3.75-42.47.3.78-43.72.3.50-33.19.3.54-34.41.pth, myrk
BLEU = 0.66, 26.4/4.2/0.3/0.0 (BP=0.997, ratio=0.997, hyp_len=23086, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.06.3.75-42.47.3.78-43.72.3.50-33.19.3.54-34.41.pth, rkmy
BLEU = 0.90, 22.3/4.5/0.4/0.0 (BP=1.000, ratio=1.053, hyp_len=24751, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.07.3.59-36.13.3.58-35.98.3.33-27.84.3.33-27.99.pth, myrk
BLEU = 1.73, 28.2/5.9/0.7/0.1 (BP=0.994, ratio=0.994, hyp_len=23030, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.07.3.59-36.13.3.58-35.98.3.33-27.84.3.33-27.99.pth, rkmy
BLEU = 1.59, 25.2/5.7/0.8/0.1 (BP=0.984, ratio=0.984, hyp_len=23135, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.08.3.43-30.86.3.44-31.14.3.15-23.34.3.17-23.71.pth, myrk
BLEU = 3.07, 32.0/8.5/1.5/0.2 (BP=1.000, ratio=1.005, hyp_len=23286, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.08.3.43-30.86.3.44-31.14.3.15-23.34.3.17-23.71.pth, rkmy
BLEU = 2.94, 28.3/7.2/1.4/0.3 (BP=1.000, ratio=1.001, hyp_len=23527, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.09.3.28-26.56.3.30-27.11.3.03-20.73.3.03-20.79.pth, myrk
BLEU = 5.25, 33.9/11.2/2.9/0.7 (BP=1.000, ratio=1.002, hyp_len=23213, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.09.3.28-26.56.3.30-27.11.3.03-20.73.3.03-20.79.pth, rkmy
BLEU = 3.71, 31.4/9.1/1.8/0.4 (BP=1.000, ratio=1.008, hyp_len=23697, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.10.3.01-20.33.3.12-22.72.2.77-15.95.2.88-17.89.pth, myrk
BLEU = 8.75, 39.7/15.6/5.1/1.9 (BP=1.000, ratio=1.008, hyp_len=23352, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.10.3.01-20.33.3.12-22.72.2.77-15.95.2.88-17.89.pth, rkmy
BLEU = 5.04, 32.6/10.5/2.6/0.7 (BP=1.000, ratio=1.002, hyp_len=23567, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.11.2.75-15.63.2.91-18.41.2.59-13.31.2.73-15.35.pth, myrk
BLEU = 11.64, 43.3/18.9/7.5/3.0 (BP=1.000, ratio=1.006, hyp_len=23288, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.11.2.75-15.63.2.91-18.41.2.59-13.31.2.73-15.35.pth, rkmy
BLEU = 6.65, 35.0/12.9/3.8/1.1 (BP=1.000, ratio=1.016, hyp_len=23884, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.12.2.62-13.71.2.75-15.57.2.46-11.65.2.59-13.30.pth, myrk
BLEU = 14.27, 46.0/21.8/9.7/4.3 (BP=1.000, ratio=1.014, hyp_len=23494, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.12.2.62-13.71.2.75-15.57.2.46-11.65.2.59-13.30.pth, rkmy
BLEU = 9.00, 38.7/15.8/5.5/1.9 (BP=0.999, ratio=0.999, hyp_len=23488, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.13.2.48-11.93.2.65-14.14.2.30-10.00.2.43-11.37.pth, myrk
BLEU = 16.81, 48.9/24.3/11.8/5.7 (BP=1.000, ratio=1.005, hyp_len=23281, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.13.2.48-11.93.2.65-14.14.2.30-10.00.2.43-11.37.pth, rkmy
BLEU = 10.88, 41.1/17.9/7.0/2.7 (BP=1.000, ratio=1.022, hyp_len=24023, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.14.2.30-10.02.2.42-11.20.2.19-8.94.2.21-9.15.pth, myrk
BLEU = 18.88, 51.2/26.6/13.7/6.8 (BP=1.000, ratio=1.019, hyp_len=23602, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.14.2.30-10.02.2.42-11.20.2.19-8.94.2.21-9.15.pth, rkmy
BLEU = 13.68, 44.4/21.3/9.2/4.0 (BP=1.000, ratio=1.040, hyp_len=24449, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.15.2.12-8.32.2.19-8.90.2.07-7.96.2.10-8.17.pth, myrk
BLEU = 22.49, 55.5/30.8/16.9/9.1 (BP=0.993, ratio=0.993, hyp_len=22998, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.15.2.12-8.32.2.19-8.90.2.07-7.96.2.10-8.17.pth, rkmy
BLEU = 16.33, 48.4/24.5/11.3/5.3 (BP=1.000, ratio=1.047, hyp_len=24618, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.16.1.98-7.23.1.99-7.29.1.95-7.01.1.86-6.45.pth, myrk
BLEU = 26.05, 57.9/34.5/20.2/11.5 (BP=1.000, ratio=1.008, hyp_len=23354, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.16.1.98-7.23.1.99-7.29.1.95-7.01.1.86-6.45.pth, rkmy
BLEU = 23.46, 55.5/31.9/17.5/9.8 (BP=1.000, ratio=1.017, hyp_len=23904, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.17.1.81-6.13.1.80-6.05.1.82-6.18.1.73-5.67.pth, myrk
BLEU = 29.48, 61.0/37.9/23.2/14.1 (BP=1.000, ratio=1.016, hyp_len=23521, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.17.1.81-6.13.1.80-6.05.1.82-6.18.1.73-5.67.pth, rkmy
BLEU = 28.24, 59.2/36.7/22.0/13.3 (BP=1.000, ratio=1.017, hyp_len=23899, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.18.1.72-5.61.1.71-5.56.1.74-5.70.1.65-5.22.pth, myrk
BLEU = 32.64, 63.2/41.1/26.3/16.6 (BP=1.000, ratio=1.027, hyp_len=23794, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.18.1.72-5.61.1.71-5.56.1.74-5.70.1.65-5.22.pth, rkmy
BLEU = 29.97, 60.6/38.6/23.7/14.6 (BP=1.000, ratio=1.025, hyp_len=24089, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.19.1.63-5.09.1.69-5.43.1.69-5.43.1.71-5.50.pth, myrk
BLEU = 33.82, 64.3/42.1/27.3/17.7 (BP=1.000, ratio=1.011, hyp_len=23406, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.19.1.63-5.09.1.69-5.43.1.69-5.43.1.71-5.50.pth, rkmy
BLEU = 27.84, 58.9/36.6/21.6/12.9 (BP=1.000, ratio=1.035, hyp_len=24339, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.20.1.57-4.79.1.52-4.57.1.56-4.75.1.49-4.43.pth, myrk
BLEU = 38.89, 67.6/46.9/32.5/22.2 (BP=1.000, ratio=1.017, hyp_len=23547, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.20.1.57-4.79.1.52-4.57.1.56-4.75.1.49-4.43.pth, rkmy
BLEU = 36.19, 64.9/44.5/29.7/20.0 (BP=1.000, ratio=1.036, hyp_len=24357, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.21.1.45-4.28.1.44-4.21.1.42-4.15.1.35-3.87.pth, myrk
BLEU = 45.01, 72.0/52.7/38.5/28.1 (BP=1.000, ratio=1.013, hyp_len=23461, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.21.1.45-4.28.1.44-4.21.1.42-4.15.1.35-3.87.pth, rkmy
BLEU = 41.43, 68.9/49.5/34.9/24.8 (BP=1.000, ratio=1.027, hyp_len=24150, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.22.1.29-3.63.1.39-4.02.1.35-3.87.1.39-4.02.pth, myrk
BLEU = 47.36, 73.3/54.9/41.0/30.5 (BP=1.000, ratio=1.013, hyp_len=23463, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.22.1.29-3.63.1.39-4.02.1.35-3.87.1.39-4.02.pth, rkmy
BLEU = 41.81, 68.8/49.8/35.2/25.3 (BP=1.000, ratio=1.036, hyp_len=24355, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.23.1.17-3.22.1.25-3.48.1.28-3.60.1.26-3.53.pth, myrk
BLEU = 51.39, 75.9/58.5/45.1/34.8 (BP=1.000, ratio=1.007, hyp_len=23329, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.23.1.17-3.22.1.25-3.48.1.28-3.60.1.26-3.53.pth, rkmy
BLEU = 47.37, 72.7/54.8/40.9/30.9 (BP=1.000, ratio=1.018, hyp_len=23931, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.24.1.15-3.15.1.20-3.33.1.37-3.92.1.33-3.79.pth, myrk
BLEU = 48.52, 73.6/55.8/42.3/31.9 (BP=1.000, ratio=1.038, hyp_len=24048, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.24.1.15-3.15.1.20-3.33.1.37-3.92.1.33-3.79.pth, rkmy
BLEU = 49.37, 74.9/57.4/43.5/33.4 (BP=0.988, ratio=0.988, hyp_len=23223, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.25.1.11-3.04.1.12-3.05.1.18-3.27.1.16-3.18.pth, myrk
BLEU = 55.76, 78.6/62.4/49.7/39.7 (BP=1.000, ratio=1.007, hyp_len=23325, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.25.1.11-3.04.1.12-3.05.1.18-3.27.1.16-3.18.pth, rkmy
BLEU = 52.35, 75.6/59.4/46.1/36.3 (BP=1.000, ratio=1.025, hyp_len=24098, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.26.1.07-2.93.1.11-3.04.1.18-3.25.1.18-3.26.pth, myrk
BLEU = 56.10, 78.7/62.6/50.1/40.2 (BP=1.000, ratio=1.006, hyp_len=23296, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.26.1.07-2.93.1.11-3.04.1.18-3.25.1.18-3.26.pth, rkmy
BLEU = 52.52, 75.9/59.6/46.3/36.3 (BP=1.000, ratio=1.007, hyp_len=23684, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.27.1.16-3.19.1.00-2.73.1.18-3.25.1.08-2.96.pth, myrk
BLEU = 55.67, 78.8/62.4/49.8/39.8 (BP=0.997, ratio=0.997, hyp_len=23082, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.27.1.16-3.19.1.00-2.73.1.18-3.25.1.08-2.96.pth, rkmy
BLEU = 57.19, 78.6/63.7/51.2/41.7 (BP=1.000, ratio=1.012, hyp_len=23786, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.28.0.96-2.62.0.92-2.52.1.12-3.07.1.05-2.84.pth, myrk
BLEU = 55.88, 77.9/62.6/50.0/40.0 (BP=1.000, ratio=1.037, hyp_len=24017, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.28.0.96-2.62.0.92-2.52.1.12-3.07.1.05-2.84.pth, rkmy
BLEU = 58.30, 79.3/64.7/52.4/43.0 (BP=1.000, ratio=1.015, hyp_len=23866, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.29.0.87-2.38.0.85-2.34.1.06-2.88.0.99-2.70.pth, myrk
BLEU = 59.81, 80.2/65.8/54.2/44.7 (BP=1.000, ratio=1.023, hyp_len=23687, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.29.0.87-2.38.0.85-2.34.1.06-2.88.0.99-2.70.pth, rkmy
BLEU = 60.37, 80.3/66.5/54.7/45.5 (BP=1.000, ratio=1.021, hyp_len=23999, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.30.1.01-2.75.0.84-2.32.1.38-3.96.0.95-2.59.pth, myrk
BLEU = 49.02, 72.7/56.1/43.2/32.8 (BP=1.000, ratio=1.033, hyp_len=23921, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.30.1.01-2.75.0.84-2.32.1.38-3.96.0.95-2.59.pth, rkmy
BLEU = 61.92, 81.2/67.9/56.3/47.3 (BP=1.000, ratio=1.025, hyp_len=24102, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.31.0.96-2.62.0.81-2.25.1.01-2.73.0.94-2.56.pth, myrk
BLEU = 63.34, 82.7/68.9/57.9/48.9 (BP=1.000, ratio=1.005, hyp_len=23287, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.31.0.96-2.62.0.81-2.25.1.01-2.73.0.94-2.56.pth, rkmy
BLEU = 63.15, 82.1/69.0/57.6/48.7 (BP=1.000, ratio=1.016, hyp_len=23877, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.32.0.83-2.29.0.87-2.38.0.95-2.58.0.98-2.66.pth, myrk
BLEU = 64.95, 83.5/70.5/59.6/50.7 (BP=1.000, ratio=1.015, hyp_len=23512, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.32.0.83-2.29.0.87-2.38.0.95-2.58.0.98-2.66.pth, rkmy
BLEU = 61.72, 81.1/67.8/56.2/47.0 (BP=1.000, ratio=1.020, hyp_len=23984, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.33.0.74-2.09.0.75-2.12.0.92-2.52.0.96-2.60.pth, myrk
BLEU = 65.56, 83.7/70.9/60.3/51.6 (BP=1.000, ratio=1.019, hyp_len=23589, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.33.0.74-2.09.0.75-2.12.0.92-2.52.0.96-2.60.pth, rkmy
BLEU = 63.95, 82.5/69.7/58.5/49.8 (BP=1.000, ratio=1.014, hyp_len=23827, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.34.0.73-2.07.0.76-2.13.0.90-2.47.0.91-2.50.pth, myrk
BLEU = 66.15, 83.5/71.3/61.1/52.6 (BP=1.000, ratio=1.028, hyp_len=23808, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.34.0.73-2.07.0.76-2.13.0.90-2.47.0.91-2.50.pth, rkmy
BLEU = 64.35, 82.5/70.0/59.0/50.4 (BP=1.000, ratio=1.031, hyp_len=24243, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.35.0.71-2.04.0.77-2.17.0.87-2.39.0.88-2.42.pth, myrk
BLEU = 68.06, 85.0/73.1/63.1/54.7 (BP=1.000, ratio=1.014, hyp_len=23490, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.35.0.71-2.04.0.77-2.17.0.87-2.39.0.88-2.42.pth, rkmy
BLEU = 65.60, 83.3/71.2/60.3/51.8 (BP=1.000, ratio=1.023, hyp_len=24051, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.36.0.66-1.93.0.68-1.96.0.86-2.37.0.84-2.31.pth, myrk
BLEU = 69.14, 85.6/73.9/64.3/56.2 (BP=1.000, ratio=1.013, hyp_len=23472, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.36.0.66-1.93.0.68-1.96.0.86-2.37.0.84-2.31.pth, rkmy
BLEU = 66.74, 83.8/72.0/61.6/53.4 (BP=1.000, ratio=1.026, hyp_len=24127, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.37.0.66-1.94.0.73-2.07.0.85-2.35.0.87-2.38.pth, myrk
BLEU = 68.72, 85.2/73.6/63.9/55.7 (BP=1.000, ratio=1.021, hyp_len=23641, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.37.0.66-1.94.0.73-2.07.0.85-2.35.0.87-2.38.pth, rkmy
BLEU = 67.66, 84.7/72.9/62.5/54.3 (BP=1.000, ratio=1.013, hyp_len=23819, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.38.0.61-1.84.0.64-1.89.0.85-2.34.0.86-2.37.pth, myrk
BLEU = 69.68, 85.8/74.4/64.9/56.9 (BP=1.000, ratio=1.015, hyp_len=23509, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.38.0.61-1.84.0.64-1.89.0.85-2.34.0.86-2.37.pth, rkmy
BLEU = 66.42, 83.4/71.7/61.2/53.1 (BP=1.000, ratio=1.023, hyp_len=24047, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.39.0.60-1.82.0.64-1.89.0.83-2.29.0.82-2.28.pth, myrk
BLEU = 70.25, 86.2/74.9/65.5/57.6 (BP=1.000, ratio=1.016, hyp_len=23534, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.39.0.60-1.82.0.64-1.89.0.83-2.29.0.82-2.28.pth, rkmy
BLEU = 67.30, 84.1/72.6/62.2/54.1 (BP=1.000, ratio=1.028, hyp_len=24169, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.40.0.58-1.79.0.60-1.82.0.82-2.28.0.80-2.23.pth, myrk
BLEU = 70.55, 86.2/75.1/65.9/58.0 (BP=1.000, ratio=1.012, hyp_len=23434, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.40.0.58-1.79.0.60-1.82.0.82-2.28.0.80-2.23.pth, rkmy
BLEU = 68.78, 84.7/73.7/63.8/56.2 (BP=1.000, ratio=1.032, hyp_len=24265, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.41.0.82-2.28.0.62-1.87.1.15-3.15.0.78-2.19.pth, myrk
BLEU = 56.43, 78.0/62.6/50.6/41.0 (BP=1.000, ratio=1.010, hyp_len=23396, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.41.0.82-2.28.0.62-1.87.1.15-3.15.0.78-2.19.pth, rkmy
BLEU = 69.23, 85.1/74.1/64.3/56.7 (BP=1.000, ratio=1.032, hyp_len=24265, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.42.0.71-2.04.0.55-1.73.0.83-2.30.0.77-2.15.pth, myrk
BLEU = 68.74, 85.2/73.6/64.0/55.7 (BP=1.000, ratio=1.020, hyp_len=23619, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.42.0.71-2.04.0.55-1.73.0.83-2.30.0.77-2.15.pth, rkmy
BLEU = 70.83, 85.8/75.4/66.1/58.8 (BP=1.000, ratio=1.028, hyp_len=24170, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.43.0.57-1.78.0.56-1.75.0.80-2.23.0.78-2.18.pth, myrk
BLEU = 71.04, 86.3/75.5/66.5/58.8 (BP=1.000, ratio=1.017, hyp_len=23563, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.43.0.57-1.78.0.56-1.75.0.80-2.23.0.78-2.18.pth, rkmy
BLEU = 69.96, 85.4/74.8/65.2/57.6 (BP=1.000, ratio=1.030, hyp_len=24204, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.44.0.53-1.69.0.54-1.72.0.77-2.17.0.80-2.24.pth, myrk
BLEU = 71.30, 86.4/75.7/66.8/59.2 (BP=1.000, ratio=1.020, hyp_len=23619, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.44.0.53-1.69.0.54-1.72.0.77-2.17.0.80-2.24.pth, rkmy
BLEU = 68.86, 84.6/73.8/64.1/56.2 (BP=1.000, ratio=1.032, hyp_len=24250, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.45.0.52-1.69.0.53-1.69.0.78-2.17.0.76-2.14.pth, myrk
BLEU = 71.33, 86.2/75.6/66.9/59.4 (BP=1.000, ratio=1.022, hyp_len=23679, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.45.0.52-1.69.0.53-1.69.0.78-2.17.0.76-2.14.pth, rkmy
BLEU = 71.17, 86.0/75.8/66.5/59.2 (BP=1.000, ratio=1.029, hyp_len=24188, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.46.0.49-1.63.0.50-1.65.0.77-2.15.0.77-2.15.pth, myrk
BLEU = 71.91, 86.7/76.2/67.5/60.0 (BP=1.000, ratio=1.020, hyp_len=23626, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.46.0.49-1.63.0.50-1.65.0.77-2.15.0.77-2.15.pth, rkmy
BLEU = 70.71, 85.9/75.5/65.9/58.5 (BP=1.000, ratio=1.028, hyp_len=24160, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.47.0.49-1.63.0.50-1.65.0.78-2.17.0.76-2.13.pth, myrk
BLEU = 71.48, 86.3/75.7/67.0/59.6 (BP=1.000, ratio=1.025, hyp_len=23733, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.47.0.49-1.63.0.50-1.65.0.78-2.17.0.76-2.13.pth, rkmy
BLEU = 71.59, 86.3/76.1/66.9/59.7 (BP=1.000, ratio=1.029, hyp_len=24185, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.48.0.49-1.64.0.49-1.63.0.76-2.13.0.72-2.06.pth, myrk
BLEU = 72.04, 86.6/76.3/67.7/60.3 (BP=1.000, ratio=1.022, hyp_len=23675, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.48.0.49-1.64.0.49-1.63.0.76-2.13.0.72-2.06.pth, rkmy
BLEU = 71.77, 86.1/76.2/67.2/60.2 (BP=1.000, ratio=1.036, hyp_len=24344, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.49.0.45-1.57.0.45-1.57.0.75-2.12.0.74-2.09.pth, myrk
BLEU = 72.76, 87.0/76.8/68.5/61.2 (BP=1.000, ratio=1.019, hyp_len=23589, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.49.0.45-1.57.0.45-1.57.0.75-2.12.0.74-2.09.pth, rkmy
BLEU = 71.56, 86.1/76.0/67.0/59.8 (BP=1.000, ratio=1.031, hyp_len=24236, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.50.0.46-1.59.0.48-1.61.0.74-2.11.0.73-2.08.pth, myrk
BLEU = 72.65, 86.9/76.7/68.4/61.2 (BP=1.000, ratio=1.023, hyp_len=23704, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.50.0.46-1.59.0.48-1.61.0.74-2.11.0.73-2.08.pth, rkmy
BLEU = 72.63, 86.8/77.0/68.1/61.1 (BP=1.000, ratio=1.025, hyp_len=24107, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.51.0.45-1.57.0.51-1.66.0.74-2.11.0.75-2.12.pth, myrk
BLEU = 72.49, 86.8/76.6/68.2/60.9 (BP=1.000, ratio=1.025, hyp_len=23739, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.51.0.45-1.57.0.51-1.66.0.74-2.11.0.75-2.12.pth, rkmy
BLEU = 71.58, 86.1/76.2/67.0/59.7 (BP=1.000, ratio=1.034, hyp_len=24318, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.52.0.43-1.54.0.47-1.60.0.72-2.05.0.72-2.06.pth, myrk
BLEU = 73.66, 87.4/77.6/69.5/62.5 (BP=1.000, ratio=1.019, hyp_len=23594, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.52.0.43-1.54.0.47-1.60.0.72-2.05.0.72-2.06.pth, rkmy
BLEU = 72.74, 86.8/77.0/68.2/61.4 (BP=1.000, ratio=1.030, hyp_len=24217, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.53.0.44-1.55.0.46-1.58.0.72-2.06.0.72-2.06.pth, myrk
BLEU = 72.87, 86.9/76.9/68.6/61.5 (BP=1.000, ratio=1.025, hyp_len=23736, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.53.0.44-1.55.0.46-1.58.0.72-2.06.0.72-2.06.pth, rkmy
BLEU = 71.88, 86.3/76.4/67.3/60.2 (BP=1.000, ratio=1.033, hyp_len=24288, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.54.0.42-1.52.0.46-1.58.0.72-2.06.0.71-2.04.pth, myrk
BLEU = 73.21, 87.1/77.1/68.9/62.0 (BP=1.000, ratio=1.025, hyp_len=23747, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.54.0.42-1.52.0.46-1.58.0.72-2.06.0.71-2.04.pth, rkmy
BLEU = 72.78, 86.8/77.0/68.3/61.5 (BP=1.000, ratio=1.030, hyp_len=24225, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.55.0.43-1.53.0.43-1.54.0.73-2.07.0.71-2.03.pth, myrk
BLEU = 72.53, 86.7/76.6/68.2/61.1 (BP=1.000, ratio=1.027, hyp_len=23780, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.55.0.43-1.53.0.43-1.54.0.73-2.07.0.71-2.03.pth, rkmy
BLEU = 73.06, 86.8/77.3/68.7/61.8 (BP=1.000, ratio=1.031, hyp_len=24246, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.56.0.43-1.53.0.42-1.52.0.72-2.05.0.69-1.99.pth, myrk
BLEU = 73.13, 87.0/77.1/68.9/61.9 (BP=1.000, ratio=1.027, hyp_len=23789, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.56.0.43-1.53.0.42-1.52.0.72-2.05.0.69-1.99.pth, rkmy
BLEU = 72.66, 86.6/76.9/68.2/61.3 (BP=1.000, ratio=1.036, hyp_len=24349, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.57.0.50-1.65.0.41-1.50.0.79-2.19.0.66-1.94.pth, myrk
BLEU = 72.63, 87.3/76.7/68.2/60.9 (BP=1.000, ratio=1.006, hyp_len=23295, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.57.0.50-1.65.0.41-1.50.0.79-2.19.0.66-1.94.pth, rkmy
BLEU = 73.84, 87.1/77.9/69.5/63.0 (BP=1.000, ratio=1.032, hyp_len=24250, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.58.0.47-1.60.0.38-1.46.0.73-2.07.0.67-1.96.pth, myrk
BLEU = 72.48, 86.7/76.6/68.1/61.0 (BP=1.000, ratio=1.024, hyp_len=23716, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.58.0.47-1.60.0.38-1.46.0.73-2.07.0.67-1.96.pth, rkmy
BLEU = 73.84, 87.1/77.9/69.5/63.0 (BP=1.000, ratio=1.034, hyp_len=24314, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.59.0.41-1.50.0.37-1.45.0.72-2.05.0.68-1.96.pth, myrk
BLEU = 72.69, 86.8/76.8/68.4/61.1 (BP=1.000, ratio=1.022, hyp_len=23681, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.59.0.41-1.50.0.37-1.45.0.72-2.05.0.68-1.96.pth, rkmy
BLEU = 73.52, 87.1/77.6/69.1/62.6 (BP=1.000, ratio=1.035, hyp_len=24334, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.60.0.49-1.64.0.38-1.46.0.78-2.18.0.68-1.98.pth, myrk
BLEU = 69.72, 85.3/74.4/65.1/57.2 (BP=1.000, ratio=1.038, hyp_len=24045, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.60.0.49-1.64.0.38-1.46.0.78-2.18.0.68-1.98.pth, rkmy
BLEU = 73.01, 86.8/77.2/68.6/61.8 (BP=1.000, ratio=1.039, hyp_len=24430, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.61.0.40-1.50.0.37-1.44.0.69-1.99.0.68-1.97.pth, myrk
BLEU = 73.17, 86.9/77.1/69.0/62.0 (BP=1.000, ratio=1.027, hyp_len=23795, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.61.0.40-1.50.0.37-1.44.0.69-1.99.0.68-1.97.pth, rkmy
BLEU = 73.22, 86.9/77.4/68.8/62.1 (BP=1.000, ratio=1.038, hyp_len=24413, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.62.0.38-1.46.0.38-1.46.0.68-1.97.0.68-1.97.pth, myrk
BLEU = 74.01, 87.5/77.8/69.9/63.1 (BP=1.000, ratio=1.024, hyp_len=23705, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.62.0.38-1.46.0.38-1.46.0.68-1.97.0.68-1.97.pth, rkmy
BLEU = 73.67, 87.1/77.8/69.3/62.7 (BP=1.000, ratio=1.034, hyp_len=24318, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.63.0.38-1.46.0.36-1.43.0.72-2.05.0.68-1.98.pth, myrk
BLEU = 71.83, 86.1/75.9/67.5/60.3 (BP=1.000, ratio=1.037, hyp_len=24012, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.63.0.38-1.46.0.36-1.43.0.72-2.05.0.68-1.98.pth, rkmy
BLEU = 74.54, 87.5/78.5/70.3/64.0 (BP=1.000, ratio=1.028, hyp_len=24179, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.64.0.38-1.46.0.36-1.43.0.70-2.01.0.67-1.96.pth, myrk
BLEU = 73.40, 87.0/77.3/69.3/62.3 (BP=1.000, ratio=1.028, hyp_len=23813, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.64.0.38-1.46.0.36-1.43.0.70-2.01.0.67-1.96.pth, rkmy
BLEU = 73.66, 87.1/77.8/69.2/62.7 (BP=1.000, ratio=1.036, hyp_len=24347, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.65.0.36-1.43.0.35-1.42.0.68-1.98.0.67-1.95.pth, myrk
BLEU = 73.87, 87.2/77.7/69.8/63.0 (BP=1.000, ratio=1.025, hyp_len=23749, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.65.0.36-1.43.0.35-1.42.0.68-1.98.0.67-1.95.pth, rkmy
BLEU = 73.06, 86.7/77.2/68.6/62.0 (BP=1.000, ratio=1.038, hyp_len=24398, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.66.0.36-1.43.0.37-1.45.0.67-1.96.0.66-1.94.pth, myrk
BLEU = 74.07, 87.3/77.8/70.0/63.3 (BP=1.000, ratio=1.028, hyp_len=23820, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.66.0.36-1.43.0.37-1.45.0.67-1.96.0.66-1.94.pth, rkmy
BLEU = 72.53, 86.4/76.7/68.1/61.3 (BP=1.000, ratio=1.042, hyp_len=24505, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.67.0.33-1.39.0.35-1.41.0.67-1.95.0.67-1.95.pth, myrk
BLEU = 73.62, 87.3/77.5/69.4/62.5 (BP=1.000, ratio=1.028, hyp_len=23818, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.67.0.33-1.39.0.35-1.41.0.67-1.95.0.67-1.95.pth, rkmy
BLEU = 74.77, 87.8/78.7/70.5/64.1 (BP=1.000, ratio=1.030, hyp_len=24203, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.68.0.35-1.42.0.35-1.43.0.67-1.96.0.68-1.98.pth, myrk
BLEU = 73.67, 87.1/77.5/69.5/62.7 (BP=1.000, ratio=1.029, hyp_len=23830, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.68.0.35-1.42.0.35-1.43.0.67-1.96.0.68-1.98.pth, rkmy
BLEU = 74.05, 87.3/78.1/69.7/63.3 (BP=1.000, ratio=1.034, hyp_len=24300, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.69.0.32-1.37.0.31-1.37.0.68-1.98.0.68-1.98.pth, myrk
BLEU = 74.48, 87.5/78.2/70.4/63.8 (BP=1.000, ratio=1.025, hyp_len=23735, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.69.0.32-1.37.0.31-1.37.0.68-1.98.0.68-1.98.pth, rkmy
BLEU = 73.11, 86.7/77.2/68.7/62.1 (BP=1.000, ratio=1.044, hyp_len=24532, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.70.0.32-1.38.0.35-1.43.0.69-1.99.0.70-2.01.pth, myrk
BLEU = 74.85, 87.9/78.5/70.8/64.2 (BP=1.000, ratio=1.022, hyp_len=23658, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.70.0.32-1.38.0.35-1.43.0.69-1.99.0.70-2.01.pth, rkmy
BLEU = 73.81, 87.1/77.8/69.5/63.0 (BP=1.000, ratio=1.034, hyp_len=24297, ref_len=23509)
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

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/myrk-80epoch
Evaluation result for the model: dsl-model-myrk.01.4.42-83.22.4.44-85.19.4.06-57.81.4.08-58.89.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 13.0/0.3/0.0/0.0 (BP=1.000, ratio=1.012, hyp_len=23431, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.01.4.42-83.22.4.44-85.19.4.06-57.81.4.08-58.89.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 17.3/0.1/0.0/0.0 (BP=0.955, ratio=0.956, hyp_len=22464, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.02.4.18-65.07.4.20-66.37.3.90-49.16.3.92-50.21.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 17.2/1.9/0.0/0.0 (BP=1.000, ratio=1.040, hyp_len=24094, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.02.4.18-65.07.4.20-66.37.3.90-49.16.3.92-50.21.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 19.2/2.4/0.0/0.0 (BP=0.986, ratio=0.986, hyp_len=23191, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.03.4.01-55.02.4.04-57.02.3.87-47.91.3.84-46.73.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.2/1.7/0.0/0.0 (BP=1.000, ratio=1.012, hyp_len=23443, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.03.4.01-55.02.4.04-57.02.3.87-47.91.3.84-46.73.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.7/2.5/0.0/0.0 (BP=0.979, ratio=0.979, hyp_len=23025, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.04.3.97-52.85.4.01-55.20.3.72-41.38.3.78-43.61.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.5/2.0/0.0/0.0 (BP=1.000, ratio=1.003, hyp_len=23220, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.04.3.97-52.85.4.01-55.20.3.72-41.38.3.78-43.61.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.0/4.1/0.4/0.0 (BP=0.982, ratio=0.982, hyp_len=23090, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.05.3.89-48.94.3.96-52.36.3.61-36.93.3.70-40.49.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.4/2.5/0.0/0.0 (BP=1.000, ratio=1.003, hyp_len=23237, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.05.3.89-48.94.3.96-52.36.3.61-36.93.3.70-40.49.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.5/2.6/0.0/0.0 (BP=0.978, ratio=0.979, hyp_len=23006, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.06.3.80-44.85.3.87-48.17.3.56-35.00.3.62-37.31.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.4/3.6/0.4/0.0 (BP=1.000, ratio=1.032, hyp_len=23911, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.06.3.80-44.85.3.87-48.17.3.56-35.00.3.62-37.31.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.0/3.6/0.3/0.0 (BP=0.991, ratio=0.992, hyp_len=23310, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.07.3.69-40.12.3.81-45.04.3.39-29.72.3.59-36.18.pth, myrk
BLEU = 1.17, 25.8/4.9/0.7/0.0 (BP=0.985, ratio=0.985, hyp_len=22817, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.07.3.69-40.12.3.81-45.04.3.39-29.72.3.59-36.18.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.9/4.3/0.2/0.0 (BP=1.000, ratio=1.012, hyp_len=23795, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.08.3.45-31.44.3.64-38.09.3.26-25.94.3.43-30.86.pth, myrk
BLEU = 2.80, 27.5/7.3/1.4/0.2 (BP=1.000, ratio=1.011, hyp_len=23426, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.08.3.45-31.44.3.64-38.09.3.26-25.94.3.43-30.86.pth, rkmy
BLEU = 1.62, 26.4/6.2/0.9/0.1 (BP=0.993, ratio=0.993, hyp_len=23351, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.09.3.27-26.29.3.39-29.68.3.12-22.71.3.22-24.98.pth, myrk
BLEU = 3.38, 29.9/8.9/1.8/0.3 (BP=1.000, ratio=1.000, hyp_len=23156, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.09.3.27-26.29.3.39-29.68.3.12-22.71.3.22-24.98.pth, rkmy
BLEU = 1.93, 28.8/8.0/1.2/0.1 (BP=0.996, ratio=0.996, hyp_len=23418, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.10.3.23-25.38.3.33-28.04.3.08-21.65.3.11-22.40.pth, myrk
BLEU = 4.44, 30.3/9.5/2.4/0.6 (BP=1.000, ratio=1.013, hyp_len=23458, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.10.3.23-25.38.3.33-28.04.3.08-21.65.3.11-22.40.pth, rkmy
BLEU = 2.89, 32.2/9.7/1.7/0.1 (BP=0.992, ratio=0.992, hyp_len=23311, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.11.3.10-22.26.3.14-23.21.2.90-18.16.2.92-18.60.pth, myrk
BLEU = 6.21, 34.5/12.2/3.5/1.0 (BP=1.000, ratio=1.012, hyp_len=23440, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.11.3.10-22.26.3.14-23.21.2.90-18.16.2.92-18.60.pth, rkmy
BLEU = 4.46, 33.7/11.0/2.2/0.5 (BP=1.000, ratio=1.005, hyp_len=23630, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.12.2.95-19.10.2.94-18.93.2.77-15.98.2.77-15.95.pth, myrk
BLEU = 8.03, 37.6/14.2/4.9/1.6 (BP=1.000, ratio=1.007, hyp_len=23333, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.12.2.95-19.10.2.94-18.93.2.77-15.98.2.77-15.95.pth, rkmy
BLEU = 7.27, 37.0/14.1/4.1/1.3 (BP=1.000, ratio=1.018, hyp_len=23937, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.13.2.77-15.99.2.84-17.10.2.62-13.72.2.62-13.67.pth, myrk
BLEU = 10.69, 42.2/17.8/6.7/2.6 (BP=1.000, ratio=1.003, hyp_len=23231, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.13.2.77-15.99.2.84-17.10.2.62-13.72.2.62-13.67.pth, rkmy
BLEU = 8.45, 39.2/15.6/5.1/1.6 (BP=1.000, ratio=1.019, hyp_len=23959, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.14.2.60-13.43.2.58-13.16.2.47-11.80.2.46-11.75.pth, myrk
BLEU = 13.22, 44.6/20.3/8.8/3.9 (BP=1.000, ratio=1.029, hyp_len=23824, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.14.2.60-13.43.2.58-13.16.2.47-11.80.2.46-11.75.pth, rkmy
BLEU = 11.12, 43.5/19.2/7.1/2.6 (BP=1.000, ratio=1.000, hyp_len=23504, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.15.2.41-11.11.2.49-12.10.2.24-9.41.2.33-10.31.pth, myrk
BLEU = 17.36, 49.6/24.8/12.2/6.0 (BP=1.000, ratio=1.000, hyp_len=23170, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.15.2.41-11.11.2.49-12.10.2.24-9.41.2.33-10.31.pth, rkmy
BLEU = 12.87, 45.6/21.2/8.5/3.3 (BP=1.000, ratio=1.012, hyp_len=23787, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.16.2.21-9.09.2.38-10.85.2.09-8.05.2.23-9.26.pth, myrk
BLEU = 21.32, 53.5/29.5/15.9/8.2 (BP=1.000, ratio=1.013, hyp_len=23457, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.16.2.21-9.09.2.38-10.85.2.09-8.05.2.23-9.26.pth, rkmy
BLEU = 14.96, 47.5/23.4/10.2/4.4 (BP=1.000, ratio=1.007, hyp_len=23665, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.17.2.02-7.57.2.21-9.08.1.89-6.63.2.11-8.26.pth, myrk
BLEU = 26.28, 58.1/34.7/20.3/11.7 (BP=1.000, ratio=1.009, hyp_len=23371, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.17.2.02-7.57.2.21-9.08.1.89-6.63.2.11-8.26.pth, rkmy
BLEU = 18.87, 51.5/27.4/13.6/6.6 (BP=1.000, ratio=1.015, hyp_len=23852, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.18.1.83-6.26.2.07-7.93.1.86-6.42.2.05-7.76.pth, myrk
BLEU = 28.86, 60.9/37.5/22.8/13.6 (BP=0.995, ratio=0.995, hyp_len=23041, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.18.1.83-6.26.2.07-7.93.1.86-6.42.2.05-7.76.pth, rkmy
BLEU = 21.66, 54.3/30.3/16.0/8.4 (BP=1.000, ratio=1.000, hyp_len=23516, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.19.1.67-5.31.1.93-6.91.1.70-5.48.1.93-6.90.pth, myrk
BLEU = 33.37, 64.3/41.8/26.9/17.1 (BP=1.000, ratio=1.010, hyp_len=23393, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.19.1.67-5.31.1.93-6.91.1.70-5.48.1.93-6.90.pth, rkmy
BLEU = 23.23, 55.8/32.3/17.5/9.2 (BP=1.000, ratio=1.009, hyp_len=23724, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.20.1.50-4.50.1.78-5.91.1.48-4.39.1.75-5.73.pth, myrk
BLEU = 41.62, 69.5/49.4/35.1/24.8 (BP=1.000, ratio=1.012, hyp_len=23432, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.20.1.50-4.50.1.78-5.91.1.48-4.39.1.75-5.73.pth, rkmy
BLEU = 29.98, 61.1/38.6/23.6/14.5 (BP=1.000, ratio=1.010, hyp_len=23743, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.21.1.46-4.30.1.79-5.98.1.41-4.08.1.65-5.18.pth, myrk
BLEU = 45.40, 71.8/52.8/39.0/28.7 (BP=1.000, ratio=1.017, hyp_len=23561, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.21.1.46-4.30.1.79-5.98.1.41-4.08.1.65-5.18.pth, rkmy
BLEU = 33.05, 63.4/41.7/26.6/17.0 (BP=1.000, ratio=1.019, hyp_len=23966, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.22.1.31-3.72.1.66-5.24.1.32-3.74.1.72-5.59.pth, myrk
BLEU = 49.66, 74.6/56.7/43.3/33.2 (BP=1.000, ratio=1.006, hyp_len=23305, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.22.1.31-3.72.1.66-5.24.1.32-3.74.1.72-5.59.pth, rkmy
BLEU = 32.62, 63.5/42.0/26.1/16.3 (BP=1.000, ratio=1.041, hyp_len=24466, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.23.1.24-3.46.1.67-5.30.1.26-3.54.1.58-4.86.pth, myrk
BLEU = 51.55, 75.7/58.4/45.4/35.2 (BP=1.000, ratio=1.020, hyp_len=23619, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.23.1.24-3.46.1.67-5.30.1.26-3.54.1.58-4.86.pth, rkmy
BLEU = 36.40, 65.6/44.9/29.8/20.0 (BP=1.000, ratio=1.016, hyp_len=23880, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.24.1.23-3.41.1.51-4.55.1.21-3.36.1.47-4.35.pth, myrk
BLEU = 53.24, 76.8/60.0/47.1/37.0 (BP=1.000, ratio=1.017, hyp_len=23562, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.24.1.23-3.41.1.51-4.55.1.21-3.36.1.47-4.35.pth, rkmy
BLEU = 42.02, 69.5/50.1/35.5/25.2 (BP=1.000, ratio=1.017, hyp_len=23898, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.25.1.10-3.00.1.41-4.08.1.18-3.24.1.48-4.40.pth, myrk
BLEU = 56.55, 78.9/62.8/50.5/40.8 (BP=1.000, ratio=1.001, hyp_len=23176, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.25.1.10-3.00.1.41-4.08.1.18-3.24.1.48-4.40.pth, rkmy
BLEU = 42.22, 70.8/51.1/35.8/25.3 (BP=0.993, ratio=0.993, hyp_len=23334, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.26.1.22-3.38.1.28-3.60.1.33-3.79.1.33-3.80.pth, myrk
BLEU = 49.08, 74.1/56.4/42.8/32.5 (BP=1.000, ratio=1.022, hyp_len=23680, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.26.1.22-3.38.1.28-3.60.1.33-3.79.1.33-3.80.pth, rkmy
BLEU = 46.57, 72.7/54.5/40.0/29.7 (BP=1.000, ratio=1.020, hyp_len=23975, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.27.1.15-3.15.1.19-3.30.1.18-3.24.1.27-3.55.pth, myrk
BLEU = 51.91, 75.6/59.0/45.8/35.5 (BP=1.000, ratio=1.034, hyp_len=23942, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.27.1.15-3.15.1.19-3.30.1.18-3.24.1.27-3.55.pth, rkmy
BLEU = 50.04, 74.7/57.5/43.6/33.5 (BP=1.000, ratio=1.018, hyp_len=23930, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.28.0.94-2.56.1.18-3.27.1.03-2.79.1.26-3.52.pth, myrk
BLEU = 60.64, 81.1/66.5/55.0/45.6 (BP=1.000, ratio=1.017, hyp_len=23550, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.28.0.94-2.56.1.18-3.27.1.03-2.79.1.26-3.52.pth, rkmy
BLEU = 51.46, 75.6/58.6/45.1/35.1 (BP=1.000, ratio=1.005, hyp_len=23623, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.29.0.91-2.48.1.08-2.96.1.03-2.80.1.22-3.40.pth, myrk
BLEU = 60.65, 81.2/66.6/55.0/45.5 (BP=1.000, ratio=1.020, hyp_len=23619, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.29.0.91-2.48.1.08-2.96.1.03-2.80.1.22-3.40.pth, rkmy
BLEU = 52.22, 76.2/59.6/45.8/35.8 (BP=1.000, ratio=1.018, hyp_len=23938, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.30.1.02-2.78.1.50-4.48.0.97-2.65.1.36-3.89.pth, myrk
BLEU = 62.66, 82.2/68.2/57.2/48.1 (BP=1.000, ratio=1.014, hyp_len=23495, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.30.1.02-2.78.1.50-4.48.0.97-2.65.1.36-3.89.pth, rkmy
BLEU = 46.44, 72.8/54.4/39.8/29.5 (BP=1.000, ratio=1.023, hyp_len=24044, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.31.0.88-2.41.1.13-3.08.0.95-2.59.1.15-3.17.pth, myrk
BLEU = 63.64, 82.7/69.1/58.2/49.3 (BP=1.000, ratio=1.016, hyp_len=23531, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.31.0.88-2.41.1.13-3.08.0.95-2.59.1.15-3.17.pth, rkmy
BLEU = 56.67, 79.0/63.4/50.5/40.8 (BP=1.000, ratio=1.007, hyp_len=23671, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.32.0.75-2.11.0.94-2.57.0.94-2.55.1.12-3.06.pth, myrk
BLEU = 65.61, 83.6/70.8/60.4/51.8 (BP=1.000, ratio=1.014, hyp_len=23483, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.32.0.75-2.11.0.94-2.57.0.94-2.55.1.12-3.06.pth, rkmy
BLEU = 57.58, 79.1/64.3/51.5/41.9 (BP=1.000, ratio=1.027, hyp_len=24132, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.33.0.71-2.04.0.91-2.48.0.89-2.43.1.08-2.95.pth, myrk
BLEU = 66.98, 84.4/72.0/62.0/53.4 (BP=1.000, ratio=1.015, hyp_len=23517, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.33.0.71-2.04.0.91-2.48.0.89-2.43.1.08-2.95.pth, rkmy
BLEU = 59.62, 80.3/66.1/53.7/44.3 (BP=1.000, ratio=1.020, hyp_len=23973, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.34.0.72-2.05.0.92-2.50.0.88-2.41.1.07-2.93.pth, myrk
BLEU = 67.27, 84.6/72.3/62.3/53.8 (BP=1.000, ratio=1.013, hyp_len=23458, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.34.0.72-2.05.0.92-2.50.0.88-2.41.1.07-2.93.pth, rkmy
BLEU = 61.04, 81.2/67.3/55.2/46.0 (BP=1.000, ratio=1.016, hyp_len=23874, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.35.0.70-2.02.0.88-2.42.0.88-2.41.1.06-2.87.pth, myrk
BLEU = 67.27, 84.3/72.2/62.4/54.0 (BP=1.000, ratio=1.022, hyp_len=23664, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.35.0.70-2.02.0.88-2.42.0.88-2.41.1.06-2.87.pth, rkmy
BLEU = 62.39, 81.8/68.4/56.7/47.7 (BP=1.000, ratio=1.010, hyp_len=23750, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.36.0.68-1.97.0.87-2.38.0.90-2.47.1.07-2.92.pth, myrk
BLEU = 66.35, 84.0/71.6/61.3/52.6 (BP=1.000, ratio=1.020, hyp_len=23620, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.36.0.68-1.97.0.87-2.38.0.90-2.47.1.07-2.92.pth, rkmy
BLEU = 62.51, 82.1/68.7/56.8/47.7 (BP=1.000, ratio=1.007, hyp_len=23672, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.37.0.74-2.09.0.84-2.32.0.88-2.41.0.99-2.69.pth, myrk
BLEU = 68.44, 85.0/73.2/63.6/55.4 (BP=1.000, ratio=1.012, hyp_len=23448, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.37.0.74-2.09.0.84-2.32.0.88-2.41.0.99-2.69.pth, rkmy
BLEU = 64.55, 83.0/70.3/59.1/50.3 (BP=1.000, ratio=1.017, hyp_len=23902, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.38.0.61-1.84.0.76-2.13.0.82-2.28.0.97-2.63.pth, myrk
BLEU = 69.74, 85.6/74.3/65.0/57.1 (BP=1.000, ratio=1.018, hyp_len=23569, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.38.0.61-1.84.0.76-2.13.0.82-2.28.0.97-2.63.pth, rkmy
BLEU = 65.16, 83.3/70.8/59.8/51.1 (BP=1.000, ratio=1.018, hyp_len=23941, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.39.0.61-1.85.0.76-2.14.0.83-2.30.0.98-2.68.pth, myrk
BLEU = 69.46, 85.4/74.1/64.8/56.7 (BP=1.000, ratio=1.022, hyp_len=23660, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.39.0.61-1.85.0.76-2.14.0.83-2.30.0.98-2.68.pth, rkmy
BLEU = 65.41, 83.4/71.0/60.0/51.5 (BP=1.000, ratio=1.022, hyp_len=24019, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.40.0.57-1.77.0.72-2.05.0.81-2.25.0.98-2.67.pth, myrk
BLEU = 69.93, 85.5/74.5/65.4/57.4 (BP=1.000, ratio=1.022, hyp_len=23681, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.40.0.57-1.77.0.72-2.05.0.81-2.25.0.98-2.67.pth, rkmy
BLEU = 65.35, 83.3/71.0/60.0/51.4 (BP=1.000, ratio=1.023, hyp_len=24046, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.41.0.65-1.92.0.92-2.50.0.83-2.30.0.99-2.70.pth, myrk
BLEU = 69.29, 85.5/74.1/64.5/56.4 (BP=1.000, ratio=1.019, hyp_len=23607, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.41.0.65-1.92.0.92-2.50.0.83-2.30.0.99-2.70.pth, rkmy
BLEU = 62.44, 81.3/68.5/56.9/48.0 (BP=1.000, ratio=1.030, hyp_len=24217, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.42.0.67-1.96.0.76-2.13.0.85-2.34.0.97-2.65.pth, myrk
BLEU = 68.22, 84.7/73.0/63.4/55.3 (BP=1.000, ratio=1.017, hyp_len=23558, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.42.0.67-1.96.0.76-2.13.0.85-2.34.0.97-2.65.pth, rkmy
BLEU = 65.49, 83.4/71.1/60.1/51.6 (BP=1.000, ratio=1.020, hyp_len=23976, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.43.0.57-1.77.0.69-2.00.0.77-2.15.0.92-2.50.pth, myrk
BLEU = 70.79, 86.1/75.3/66.3/58.5 (BP=1.000, ratio=1.019, hyp_len=23609, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.43.0.57-1.77.0.69-2.00.0.77-2.15.0.92-2.50.pth, rkmy
BLEU = 67.89, 84.5/73.1/62.8/54.7 (BP=1.000, ratio=1.020, hyp_len=23974, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.44.0.55-1.73.0.67-1.96.0.79-2.20.0.91-2.47.pth, myrk
BLEU = 70.86, 86.0/75.3/66.3/58.7 (BP=1.000, ratio=1.026, hyp_len=23765, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.44.0.55-1.73.0.67-1.96.0.79-2.20.0.91-2.47.pth, rkmy
BLEU = 68.66, 85.0/73.8/63.6/55.7 (BP=1.000, ratio=1.015, hyp_len=23870, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.45.0.51-1.66.0.64-1.89.0.77-2.17.0.88-2.42.pth, myrk
BLEU = 71.72, 86.4/76.0/67.3/59.9 (BP=1.000, ratio=1.021, hyp_len=23637, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.45.0.51-1.66.0.64-1.89.0.77-2.17.0.88-2.42.pth, rkmy
BLEU = 68.16, 84.6/73.3/63.1/55.1 (BP=1.000, ratio=1.026, hyp_len=24121, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.46.0.51-1.67.0.63-1.88.0.77-2.16.0.89-2.44.pth, myrk
BLEU = 72.46, 87.1/76.7/68.1/60.6 (BP=1.000, ratio=1.016, hyp_len=23538, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.46.0.51-1.67.0.63-1.88.0.77-2.16.0.89-2.44.pth, rkmy
BLEU = 68.66, 84.9/73.8/63.7/55.7 (BP=1.000, ratio=1.022, hyp_len=24015, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.47.0.51-1.66.0.62-1.87.0.76-2.14.0.87-2.39.pth, myrk
BLEU = 72.22, 86.8/76.5/67.9/60.4 (BP=1.000, ratio=1.021, hyp_len=23655, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.47.0.51-1.66.0.62-1.87.0.76-2.14.0.87-2.39.pth, rkmy
BLEU = 69.58, 85.4/74.6/64.7/56.9 (BP=1.000, ratio=1.021, hyp_len=23999, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.48.0.47-1.61.0.62-1.87.0.76-2.14.0.86-2.36.pth, myrk
BLEU = 71.69, 86.2/75.9/67.4/60.0 (BP=1.000, ratio=1.025, hyp_len=23748, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.48.0.47-1.61.0.62-1.87.0.76-2.14.0.86-2.36.pth, rkmy
BLEU = 69.23, 85.1/74.2/64.2/56.6 (BP=1.000, ratio=1.024, hyp_len=24079, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.49.0.47-1.60.0.60-1.82.0.75-2.12.0.86-2.37.pth, myrk
BLEU = 71.50, 86.3/75.9/67.1/59.5 (BP=1.000, ratio=1.026, hyp_len=23767, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.49.0.47-1.60.0.60-1.82.0.75-2.12.0.86-2.37.pth, rkmy
BLEU = 69.48, 85.4/74.6/64.5/56.7 (BP=1.000, ratio=1.025, hyp_len=24104, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.50.0.45-1.58.0.60-1.81.0.74-2.09.0.86-2.36.pth, myrk
BLEU = 72.07, 86.6/76.3/67.8/60.2 (BP=1.000, ratio=1.026, hyp_len=23756, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.50.0.45-1.58.0.60-1.81.0.74-2.09.0.86-2.36.pth, rkmy
BLEU = 69.32, 85.2/74.3/64.4/56.6 (BP=1.000, ratio=1.030, hyp_len=24206, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.51.0.45-1.57.0.56-1.75.0.74-2.09.0.85-2.35.pth, myrk
BLEU = 72.21, 86.6/76.4/67.9/60.6 (BP=1.000, ratio=1.023, hyp_len=23682, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.51.0.45-1.57.0.56-1.75.0.74-2.09.0.85-2.35.pth, rkmy
BLEU = 69.51, 85.3/74.4/64.6/56.9 (BP=1.000, ratio=1.023, hyp_len=24056, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.52.0.47-1.60.0.55-1.73.0.73-2.08.0.82-2.27.pth, myrk
BLEU = 71.97, 86.3/76.1/67.6/60.4 (BP=1.000, ratio=1.026, hyp_len=23762, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.52.0.47-1.60.0.55-1.73.0.73-2.08.0.82-2.27.pth, rkmy
BLEU = 70.92, 86.1/75.7/66.1/58.7 (BP=1.000, ratio=1.025, hyp_len=24093, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.53.0.42-1.53.0.52-1.69.0.73-2.07.0.83-2.29.pth, myrk
BLEU = 72.24, 86.6/76.4/68.0/60.5 (BP=1.000, ratio=1.025, hyp_len=23747, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.53.0.42-1.53.0.52-1.69.0.73-2.07.0.83-2.29.pth, rkmy
BLEU = 71.82, 86.5/76.4/67.2/60.0 (BP=1.000, ratio=1.021, hyp_len=23996, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.54.0.43-1.54.0.53-1.70.0.73-2.07.0.83-2.28.pth, myrk
BLEU = 72.79, 87.0/77.0/68.5/61.2 (BP=1.000, ratio=1.023, hyp_len=23687, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.54.0.43-1.54.0.53-1.70.0.73-2.07.0.83-2.28.pth, rkmy
BLEU = 71.21, 86.1/75.9/66.6/59.1 (BP=1.000, ratio=1.023, hyp_len=24057, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.55.0.43-1.54.0.53-1.70.0.73-2.07.0.81-2.25.pth, myrk
BLEU = 73.52, 87.4/77.5/69.3/62.2 (BP=1.000, ratio=1.021, hyp_len=23635, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.55.0.43-1.54.0.53-1.70.0.73-2.07.0.81-2.25.pth, rkmy
BLEU = 71.28, 86.0/75.9/66.7/59.4 (BP=1.000, ratio=1.029, hyp_len=24199, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.56.0.40-1.50.0.49-1.64.0.71-2.04.0.81-2.26.pth, myrk
BLEU = 73.48, 87.2/77.4/69.3/62.3 (BP=1.000, ratio=1.024, hyp_len=23725, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.56.0.40-1.50.0.49-1.64.0.71-2.04.0.81-2.26.pth, rkmy
BLEU = 71.87, 86.4/76.4/67.3/60.1 (BP=1.000, ratio=1.028, hyp_len=24166, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.57.0.40-1.50.0.49-1.64.0.73-2.07.0.80-2.22.pth, myrk
BLEU = 73.21, 87.3/77.3/69.0/61.8 (BP=1.000, ratio=1.023, hyp_len=23697, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.57.0.40-1.50.0.49-1.64.0.73-2.07.0.80-2.22.pth, rkmy
BLEU = 70.63, 85.7/75.4/65.9/58.5 (BP=1.000, ratio=1.033, hyp_len=24286, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.58.0.44-1.55.0.47-1.60.0.72-2.06.0.81-2.24.pth, myrk
BLEU = 73.60, 87.4/77.6/69.4/62.3 (BP=1.000, ratio=1.021, hyp_len=23635, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.58.0.44-1.55.0.47-1.60.0.72-2.06.0.81-2.24.pth, rkmy
BLEU = 71.13, 85.9/75.7/66.5/59.2 (BP=1.000, ratio=1.035, hyp_len=24323, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.59.0.39-1.48.0.46-1.58.0.74-2.09.0.84-2.32.pth, myrk
BLEU = 72.21, 86.6/76.4/67.9/60.6 (BP=1.000, ratio=1.033, hyp_len=23929, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.59.0.39-1.48.0.46-1.58.0.74-2.09.0.84-2.32.pth, rkmy
BLEU = 71.27, 86.2/75.9/66.6/59.2 (BP=1.000, ratio=1.022, hyp_len=24022, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.60.0.39-1.48.0.55-1.73.0.72-2.05.0.83-2.30.pth, myrk
BLEU = 73.70, 87.4/77.7/69.5/62.5 (BP=1.000, ratio=1.026, hyp_len=23766, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.60.0.39-1.48.0.55-1.73.0.72-2.05.0.83-2.30.pth, rkmy
BLEU = 71.53, 86.4/76.1/66.9/59.5 (BP=1.000, ratio=1.020, hyp_len=23989, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.61.0.39-1.47.0.51-1.66.0.73-2.07.0.78-2.18.pth, myrk
BLEU = 73.46, 87.1/77.4/69.3/62.3 (BP=1.000, ratio=1.027, hyp_len=23789, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.61.0.39-1.47.0.51-1.66.0.73-2.07.0.78-2.18.pth, rkmy
BLEU = 71.65, 86.2/76.1/67.1/59.9 (BP=1.000, ratio=1.032, hyp_len=24263, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.62.0.36-1.44.0.47-1.60.0.72-2.06.0.80-2.24.pth, myrk
BLEU = 73.95, 87.6/77.9/69.8/62.8 (BP=1.000, ratio=1.026, hyp_len=23768, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.62.0.36-1.44.0.47-1.60.0.72-2.06.0.80-2.24.pth, rkmy
BLEU = 71.49, 86.2/76.0/66.8/59.6 (BP=1.000, ratio=1.029, hyp_len=24183, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.63.0.40-1.50.0.56-1.75.0.75-2.12.0.88-2.42.pth, myrk
BLEU = 72.35, 86.6/76.6/68.1/60.6 (BP=1.000, ratio=1.035, hyp_len=23977, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.63.0.40-1.50.0.56-1.75.0.75-2.12.0.88-2.42.pth, rkmy
BLEU = 68.46, 84.4/73.7/63.6/55.5 (BP=1.000, ratio=1.044, hyp_len=24539, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.64.0.36-1.43.0.45-1.57.0.74-2.10.0.78-2.18.pth, myrk
BLEU = 74.58, 88.1/78.4/70.5/63.6 (BP=1.000, ratio=1.020, hyp_len=23624, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.64.0.36-1.43.0.45-1.57.0.74-2.10.0.78-2.18.pth, rkmy
BLEU = 71.90, 86.4/76.4/67.3/60.2 (BP=1.000, ratio=1.028, hyp_len=24171, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.65.0.37-1.45.0.46-1.59.0.73-2.08.0.78-2.19.pth, myrk
BLEU = 73.97, 87.5/77.9/69.9/62.9 (BP=1.000, ratio=1.023, hyp_len=23703, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.65.0.37-1.45.0.46-1.59.0.73-2.08.0.78-2.19.pth, rkmy
BLEU = 70.75, 85.7/75.3/66.0/58.8 (BP=1.000, ratio=1.035, hyp_len=24328, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.66.0.35-1.42.0.47-1.60.0.73-2.08.0.88-2.41.pth, myrk
BLEU = 73.09, 86.9/77.1/68.9/61.9 (BP=1.000, ratio=1.031, hyp_len=23867, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.66.0.35-1.42.0.47-1.60.0.73-2.08.0.88-2.41.pth, rkmy
BLEU = 72.53, 87.1/77.1/67.9/60.7 (BP=1.000, ratio=1.013, hyp_len=23817, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.67.0.35-1.41.0.45-1.57.0.72-2.05.0.79-2.20.pth, myrk
BLEU = 73.40, 87.1/77.4/69.2/62.2 (BP=1.000, ratio=1.031, hyp_len=23872, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.67.0.35-1.41.0.45-1.57.0.72-2.05.0.79-2.20.pth, rkmy
BLEU = 71.05, 85.8/75.7/66.4/59.1 (BP=1.000, ratio=1.033, hyp_len=24285, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.68.0.33-1.40.0.44-1.56.0.72-2.06.0.78-2.19.pth, myrk
BLEU = 73.82, 87.4/77.8/69.7/62.8 (BP=1.000, ratio=1.028, hyp_len=23799, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.68.0.33-1.40.0.44-1.56.0.72-2.06.0.78-2.19.pth, rkmy
BLEU = 71.95, 86.4/76.5/67.4/60.2 (BP=1.000, ratio=1.033, hyp_len=24291, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.69.0.35-1.41.0.44-1.55.0.71-2.04.0.76-2.14.pth, myrk
BLEU = 73.82, 87.3/77.7/69.7/62.7 (BP=1.000, ratio=1.029, hyp_len=23828, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.69.0.35-1.41.0.44-1.55.0.71-2.04.0.76-2.14.pth, rkmy
BLEU = 72.98, 87.0/77.4/68.5/61.5 (BP=1.000, ratio=1.030, hyp_len=24225, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.70.0.32-1.38.0.40-1.50.0.71-2.03.0.76-2.14.pth, myrk
BLEU = 73.82, 87.3/77.6/69.7/62.9 (BP=1.000, ratio=1.030, hyp_len=23849, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.70.0.32-1.38.0.40-1.50.0.71-2.03.0.76-2.14.pth, rkmy
BLEU = 72.99, 86.9/77.3/68.6/61.6 (BP=1.000, ratio=1.032, hyp_len=24271, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.71.0.36-1.44.0.40-1.49.0.74-2.10.0.76-2.14.pth, myrk
BLEU = 72.57, 86.8/76.8/68.2/61.0 (BP=1.000, ratio=1.037, hyp_len=24007, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.71.0.36-1.44.0.40-1.49.0.74-2.10.0.76-2.14.pth, rkmy
BLEU = 73.20, 87.0/77.5/68.8/61.9 (BP=1.000, ratio=1.031, hyp_len=24233, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.72.0.42-1.52.0.38-1.46.0.78-2.17.0.76-2.13.pth, myrk
BLEU = 68.20, 84.0/72.7/63.5/55.8 (BP=1.000, ratio=1.042, hyp_len=24129, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.72.0.42-1.52.0.38-1.46.0.78-2.17.0.76-2.13.pth, rkmy
BLEU = 72.61, 86.5/76.9/68.1/61.3 (BP=1.000, ratio=1.037, hyp_len=24385, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.73.0.48-1.62.0.38-1.46.0.74-2.10.0.76-2.14.pth, myrk
BLEU = 71.36, 85.7/75.6/67.1/59.7 (BP=1.000, ratio=1.034, hyp_len=23952, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.73.0.48-1.62.0.38-1.46.0.74-2.10.0.76-2.14.pth, rkmy
BLEU = 72.30, 86.4/76.7/67.8/60.8 (BP=1.000, ratio=1.039, hyp_len=24415, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.74.0.40-1.49.0.38-1.46.0.69-2.00.0.74-2.09.pth, myrk
BLEU = 74.13, 87.7/78.1/70.0/62.9 (BP=1.000, ratio=1.019, hyp_len=23610, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.74.0.40-1.49.0.38-1.46.0.69-2.00.0.74-2.09.pth, rkmy
BLEU = 72.53, 86.5/76.8/68.1/61.2 (BP=1.000, ratio=1.038, hyp_len=24403, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.75.0.33-1.40.0.36-1.44.0.69-1.99.0.75-2.12.pth, myrk
BLEU = 73.87, 87.3/77.8/69.8/62.8 (BP=1.000, ratio=1.026, hyp_len=23771, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.75.0.33-1.40.0.36-1.44.0.69-1.99.0.75-2.12.pth, rkmy
BLEU = 73.49, 87.2/77.7/69.1/62.3 (BP=1.000, ratio=1.033, hyp_len=24284, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.76.0.32-1.38.0.39-1.47.0.68-1.98.0.78-2.17.pth, myrk
BLEU = 74.03, 87.3/77.9/70.0/63.1 (BP=1.000, ratio=1.028, hyp_len=23817, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.76.0.32-1.38.0.39-1.47.0.68-1.98.0.78-2.17.pth, rkmy
BLEU = 73.31, 87.1/77.4/68.8/62.2 (BP=1.000, ratio=1.028, hyp_len=24172, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.77.0.47-1.59.0.81-2.25.0.70-2.01.0.79-2.21.pth, myrk
BLEU = 73.56, 87.4/77.6/69.4/62.2 (BP=1.000, ratio=1.029, hyp_len=23827, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.77.0.47-1.59.0.81-2.25.0.70-2.01.0.79-2.21.pth, rkmy
BLEU = 70.81, 85.7/75.5/66.2/58.8 (BP=1.000, ratio=1.028, hyp_len=24173, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.78.0.35-1.42.0.48-1.62.0.72-2.05.0.76-2.13.pth, myrk
BLEU = 73.04, 87.0/77.0/68.8/61.7 (BP=1.000, ratio=1.027, hyp_len=23778, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.78.0.35-1.42.0.48-1.62.0.72-2.05.0.76-2.13.pth, rkmy
BLEU = 71.28, 86.0/75.7/66.6/59.5 (BP=1.000, ratio=1.034, hyp_len=24303, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.79.0.32-1.38.0.44-1.55.0.70-2.00.0.74-2.09.pth, myrk
BLEU = 74.06, 87.4/77.9/70.0/63.1 (BP=1.000, ratio=1.029, hyp_len=23838, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.79.0.32-1.38.0.44-1.55.0.70-2.00.0.74-2.09.pth, rkmy
BLEU = 71.89, 86.2/76.4/67.3/60.2 (BP=1.000, ratio=1.038, hyp_len=24405, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.80.0.30-1.34.0.39-1.47.0.69-2.00.0.74-2.10.pth, myrk
BLEU = 73.74, 87.1/77.6/69.6/62.9 (BP=1.000, ratio=1.033, hyp_len=23914, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.80.0.30-1.34.0.39-1.47.0.69-2.00.0.74-2.10.pth, rkmy
BLEU = 74.43, 87.7/78.6/70.1/63.5 (BP=1.000, ratio=1.022, hyp_len=24034, ref_len=23509)
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

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/myrk-90epoch
Evaluation result for the model: dsl-model-myrk.01.4.46-86.36.4.48-88.41.4.04-56.58.4.07-58.34.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 15.2/2.1/0.0/0.0 (BP=1.000, ratio=1.082, hyp_len=25067, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.01.4.46-86.36.4.48-88.41.4.04-56.58.4.07-58.34.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 15.6/0.1/0.0/0.0 (BP=1.000, ratio=1.075, hyp_len=25271, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.02.4.09-59.61.4.12-61.59.3.93-51.12.3.91-49.89.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 18.7/1.7/0.0/0.0 (BP=1.000, ratio=1.020, hyp_len=23622, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.02.4.09-59.61.4.12-61.59.3.93-51.12.3.91-49.89.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.5/2.7/0.0/0.0 (BP=0.988, ratio=0.988, hyp_len=23217, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.03.4.01-54.90.4.02-55.52.3.81-45.26.3.82-45.67.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 19.0/1.7/0.0/0.0 (BP=1.000, ratio=1.005, hyp_len=23279, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.03.4.01-54.90.4.02-55.52.3.81-45.26.3.82-45.67.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.4/2.3/0.0/0.0 (BP=0.983, ratio=0.983, hyp_len=23119, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.04.3.94-51.37.3.95-52.10.3.73-41.60.3.74-42.18.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.1/1.7/0.0/0.0 (BP=1.000, ratio=1.025, hyp_len=23732, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.04.3.94-51.37.3.95-52.10.3.73-41.60.3.74-42.18.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.3/1.8/0.0/0.0 (BP=0.979, ratio=0.979, hyp_len=23013, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.05.3.86-47.48.3.91-49.85.3.60-36.54.3.65-38.38.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 22.7/2.0/0.0/0.0 (BP=1.000, ratio=1.003, hyp_len=23235, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.05.3.86-47.48.3.91-49.85.3.60-36.54.3.65-38.38.pth, rkmy
BLEU = 0.90, 24.6/4.1/0.4/0.0 (BP=0.983, ratio=0.983, hyp_len=23115, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.06.3.74-42.28.3.79-44.11.3.51-33.42.3.54-34.60.pth, myrk
BLEU = 1.11, 26.2/4.9/0.5/0.0 (BP=1.000, ratio=1.001, hyp_len=23186, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.06.3.74-42.28.3.79-44.11.3.51-33.42.3.54-34.60.pth, rkmy
BLEU = 0.91, 25.8/4.6/0.6/0.0 (BP=0.980, ratio=0.981, hyp_len=23051, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.07.3.57-35.60.3.63-37.82.3.38-29.46.3.45-31.46.pth, myrk
BLEU = 1.14, 28.0/6.4/0.8/0.0 (BP=1.000, ratio=1.009, hyp_len=23377, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.07.3.57-35.60.3.63-37.82.3.38-29.46.3.45-31.46.pth, rkmy
BLEU = 0.86, 27.0/5.6/0.7/0.0 (BP=0.986, ratio=0.986, hyp_len=23173, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.08.3.43-31.00.3.54-34.33.3.23-25.23.3.34-28.25.pth, myrk
BLEU = 2.80, 31.0/8.1/1.5/0.2 (BP=1.000, ratio=1.001, hyp_len=23175, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.08.3.43-31.00.3.54-34.33.3.23-25.23.3.34-28.25.pth, rkmy
BLEU = 2.44, 29.1/7.6/1.5/0.1 (BP=0.997, ratio=0.997, hyp_len=23447, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.09.3.18-23.94.3.33-27.83.2.99-19.96.3.16-23.58.pth, myrk
BLEU = 4.34, 34.9/11.2/2.5/0.4 (BP=0.999, ratio=0.999, hyp_len=23144, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.09.3.18-23.94.3.33-27.83.2.99-19.96.3.16-23.58.pth, rkmy
BLEU = 4.02, 31.5/9.6/2.2/0.4 (BP=1.000, ratio=1.022, hyp_len=24022, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.10.3.08-21.69.3.25-25.85.2.78-16.11.2.97-19.57.pth, myrk
BLEU = 8.17, 40.6/16.2/4.9/1.4 (BP=1.000, ratio=1.001, hyp_len=23180, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.10.3.08-21.69.3.25-25.85.2.78-16.11.2.97-19.57.pth, rkmy
BLEU = 6.50, 34.4/12.5/3.5/1.2 (BP=1.000, ratio=1.072, hyp_len=25193, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.11.2.73-15.32.2.91-18.28.2.63-13.94.2.76-15.85.pth, myrk
BLEU = 11.19, 43.7/19.1/7.3/2.6 (BP=0.996, ratio=0.997, hyp_len=23079, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.11.2.73-15.32.2.91-18.28.2.63-13.94.2.76-15.85.pth, rkmy
BLEU = 7.54, 40.1/15.5/4.6/1.2 (BP=0.993, ratio=0.993, hyp_len=23346, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.12.2.55-12.86.2.64-14.06.2.44-11.51.2.47-11.84.pth, myrk
BLEU = 14.50, 47.1/22.2/10.0/4.2 (BP=1.000, ratio=1.003, hyp_len=23237, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.12.2.55-12.86.2.64-14.06.2.44-11.51.2.47-11.84.pth, rkmy
BLEU = 11.59, 44.1/19.3/7.4/2.9 (BP=1.000, ratio=1.012, hyp_len=23793, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.13.2.34-10.40.2.45-11.55.2.34-10.43.2.30-9.94.pth, myrk
BLEU = 17.68, 49.8/25.3/12.5/6.2 (BP=1.000, ratio=1.019, hyp_len=23603, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.13.2.34-10.40.2.45-11.55.2.34-10.43.2.30-9.94.pth, rkmy
BLEU = 13.97, 47.0/22.6/9.4/3.8 (BP=1.000, ratio=1.015, hyp_len=23858, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.14.2.16-8.71.2.25-9.49.2.12-8.37.2.15-8.57.pth, myrk
BLEU = 21.20, 53.8/29.3/15.5/8.3 (BP=1.000, ratio=1.001, hyp_len=23191, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.14.2.16-8.71.2.25-9.49.2.12-8.37.2.15-8.57.pth, rkmy
BLEU = 17.70, 50.9/26.3/12.4/5.9 (BP=1.000, ratio=1.015, hyp_len=23867, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.15.1.96-7.09.2.04-7.72.1.96-7.08.1.93-6.89.pth, myrk
BLEU = 26.33, 58.6/34.6/20.2/11.7 (BP=1.000, ratio=1.003, hyp_len=23230, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.15.1.96-7.09.2.04-7.72.1.96-7.08.1.93-6.89.pth, rkmy
BLEU = 23.39, 56.3/32.1/17.4/9.5 (BP=1.000, ratio=1.002, hyp_len=23557, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.16.1.93-6.90.1.98-7.24.1.93-6.88.1.86-6.40.pth, myrk
BLEU = 27.43, 60.3/36.1/21.3/12.6 (BP=0.992, ratio=0.992, hyp_len=22977, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.16.1.93-6.90.1.98-7.24.1.93-6.88.1.86-6.40.pth, rkmy
BLEU = 26.56, 58.4/35.2/20.3/11.9 (BP=1.000, ratio=1.020, hyp_len=23986, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.17.1.75-5.74.1.79-6.02.1.77-5.86.1.72-5.56.pth, myrk
BLEU = 32.33, 63.0/40.4/25.8/16.6 (BP=1.000, ratio=1.004, hyp_len=23260, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.17.1.75-5.74.1.79-6.02.1.77-5.86.1.72-5.56.pth, rkmy
BLEU = 30.66, 61.8/39.4/24.2/15.0 (BP=1.000, ratio=1.019, hyp_len=23963, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.18.1.77-5.85.1.81-6.11.1.73-5.62.1.73-5.65.pth, myrk
BLEU = 34.25, 64.6/42.2/27.8/18.2 (BP=1.000, ratio=1.009, hyp_len=23361, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.18.1.77-5.85.1.81-6.11.1.73-5.62.1.73-5.65.pth, rkmy
BLEU = 30.24, 61.4/38.9/23.8/14.7 (BP=1.000, ratio=1.021, hyp_len=24004, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.19.1.58-4.83.1.63-5.08.1.66-5.26.1.60-4.94.pth, myrk
BLEU = 37.05, 66.8/45.1/30.6/20.8 (BP=0.996, ratio=0.996, hyp_len=23058, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.19.1.58-4.83.1.63-5.08.1.66-5.26.1.60-4.94.pth, rkmy
BLEU = 35.76, 65.7/44.4/29.1/19.3 (BP=1.000, ratio=1.012, hyp_len=23786, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.20.1.46-4.31.1.57-4.80.1.55-4.71.1.50-4.47.pth, myrk
BLEU = 42.59, 70.2/50.2/36.0/25.9 (BP=1.000, ratio=1.009, hyp_len=23361, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.20.1.46-4.31.1.57-4.80.1.55-4.71.1.50-4.47.pth, rkmy
BLEU = 39.60, 68.2/47.9/32.9/22.9 (BP=1.000, ratio=1.014, hyp_len=23834, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.21.1.43-4.16.1.58-4.87.1.50-4.47.1.47-4.37.pth, myrk
BLEU = 44.23, 71.4/51.6/37.7/27.6 (BP=1.000, ratio=1.004, hyp_len=23255, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.21.1.43-4.16.1.58-4.87.1.50-4.47.1.47-4.37.pth, rkmy
BLEU = 40.49, 68.7/48.6/33.8/23.8 (BP=1.000, ratio=1.007, hyp_len=23679, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.22.1.36-3.89.1.50-4.48.1.44-4.22.1.40-4.04.pth, myrk
BLEU = 47.36, 73.2/54.5/40.9/30.8 (BP=1.000, ratio=1.009, hyp_len=23367, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.22.1.36-3.89.1.50-4.48.1.44-4.22.1.40-4.04.pth, rkmy
BLEU = 43.53, 70.2/51.3/37.0/27.0 (BP=1.000, ratio=1.020, hyp_len=23980, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.23.1.27-3.56.1.44-4.22.1.41-4.11.1.38-3.96.pth, myrk
BLEU = 48.63, 74.1/55.8/42.2/32.1 (BP=1.000, ratio=1.009, hyp_len=23371, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.23.1.27-3.56.1.44-4.22.1.41-4.11.1.38-3.96.pth, rkmy
BLEU = 45.96, 72.3/53.6/39.3/29.3 (BP=1.000, ratio=1.001, hyp_len=23525, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.24.1.28-3.59.1.57-4.81.1.39-4.01.1.45-4.25.pth, myrk
BLEU = 50.55, 75.4/57.5/44.2/34.1 (BP=1.000, ratio=1.000, hyp_len=23164, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.24.1.28-3.59.1.57-4.81.1.39-4.01.1.45-4.25.pth, rkmy
BLEU = 42.05, 69.6/50.1/35.3/25.3 (BP=1.000, ratio=1.009, hyp_len=23731, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.25.1.21-3.35.1.25-3.49.1.34-3.83.1.28-3.60.pth, myrk
BLEU = 51.47, 76.0/58.5/45.1/35.0 (BP=1.000, ratio=1.009, hyp_len=23377, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.25.1.21-3.35.1.25-3.49.1.34-3.83.1.28-3.60.pth, rkmy
BLEU = 48.14, 73.3/55.5/41.6/31.7 (BP=1.000, ratio=1.014, hyp_len=23843, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.26.1.20-3.32.1.11-3.03.1.43-4.19.1.25-3.49.pth, myrk
BLEU = 51.32, 76.9/59.1/45.7/35.4 (BP=0.985, ratio=0.986, hyp_len=22826, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.26.1.20-3.32.1.11-3.03.1.43-4.19.1.25-3.49.pth, rkmy
BLEU = 50.26, 74.6/57.7/43.8/33.8 (BP=1.000, ratio=1.027, hyp_len=24149, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.27.1.15-3.14.1.22-3.39.1.29-3.64.1.30-3.66.pth, myrk
BLEU = 54.41, 77.6/61.0/48.2/38.4 (BP=1.000, ratio=1.005, hyp_len=23271, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.27.1.15-3.14.1.22-3.39.1.29-3.64.1.30-3.66.pth, rkmy
BLEU = 47.55, 73.1/55.3/41.0/30.9 (BP=1.000, ratio=1.022, hyp_len=24033, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.28.1.09-2.96.1.28-3.59.1.23-3.43.1.41-4.09.pth, myrk
BLEU = 56.98, 79.0/63.2/51.0/41.4 (BP=1.000, ratio=1.012, hyp_len=23448, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.28.1.09-2.96.1.28-3.59.1.23-3.43.1.41-4.09.pth, rkmy
BLEU = 48.29, 73.9/56.4/41.7/31.3 (BP=1.000, ratio=1.028, hyp_len=24168, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.29.1.00-2.73.1.11-3.04.1.19-3.30.1.11-3.04.pth, myrk
BLEU = 58.34, 79.7/64.4/52.5/43.0 (BP=1.000, ratio=1.009, hyp_len=23376, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.29.1.00-2.73.1.11-3.04.1.19-3.30.1.11-3.04.pth, rkmy
BLEU = 54.44, 77.0/61.4/48.2/38.5 (BP=1.000, ratio=1.028, hyp_len=24177, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.30.0.97-2.65.1.03-2.79.1.16-3.20.1.15-3.17.pth, myrk
BLEU = 60.39, 80.9/66.2/54.6/45.4 (BP=1.000, ratio=1.007, hyp_len=23317, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.30.0.97-2.65.1.03-2.79.1.16-3.20.1.15-3.17.pth, rkmy
BLEU = 51.52, 75.4/58.7/45.2/35.3 (BP=1.000, ratio=1.023, hyp_len=24046, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.31.0.97-2.63.1.17-3.24.1.14-3.14.1.11-3.04.pth, myrk
BLEU = 60.57, 80.8/66.4/54.9/45.7 (BP=1.000, ratio=1.013, hyp_len=23457, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.31.0.97-2.63.1.17-3.24.1.14-3.14.1.11-3.04.pth, rkmy
BLEU = 55.26, 77.8/62.2/49.1/39.2 (BP=1.000, ratio=1.020, hyp_len=23970, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.32.0.91-2.47.0.95-2.60.1.20-3.30.1.04-2.83.pth, myrk
BLEU = 61.50, 81.9/67.5/56.0/46.7 (BP=0.998, ratio=0.998, hyp_len=23110, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.32.0.91-2.47.0.95-2.60.1.20-3.30.1.04-2.83.pth, rkmy
BLEU = 60.01, 80.5/66.4/54.1/44.8 (BP=1.000, ratio=1.016, hyp_len=23878, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.33.1.24-3.47.0.92-2.52.1.28-3.61.0.98-2.65.pth, myrk
BLEU = 54.19, 77.5/60.9/48.0/38.1 (BP=1.000, ratio=1.019, hyp_len=23610, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.33.1.24-3.47.0.92-2.52.1.28-3.61.0.98-2.65.pth, rkmy
BLEU = 60.89, 80.7/67.1/55.1/46.1 (BP=1.000, ratio=1.025, hyp_len=24095, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.34.0.99-2.70.0.80-2.22.1.10-3.00.0.98-2.66.pth, myrk
BLEU = 60.16, 80.8/66.2/54.4/45.0 (BP=1.000, ratio=1.017, hyp_len=23559, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.34.0.99-2.70.0.80-2.22.1.10-3.00.0.98-2.66.pth, rkmy
BLEU = 62.83, 81.9/68.7/57.2/48.4 (BP=1.000, ratio=1.017, hyp_len=23914, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.35.0.82-2.28.0.85-2.34.1.04-2.84.1.02-2.77.pth, myrk
BLEU = 63.75, 82.8/69.4/58.3/49.3 (BP=1.000, ratio=1.013, hyp_len=23469, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.35.0.82-2.28.0.85-2.34.1.04-2.84.1.02-2.77.pth, rkmy
BLEU = 61.62, 81.7/67.7/55.8/46.7 (BP=1.000, ratio=1.003, hyp_len=23578, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.36.0.76-2.14.0.79-2.21.1.02-2.77.0.98-2.67.pth, myrk
BLEU = 64.51, 83.2/70.0/59.2/50.2 (BP=1.000, ratio=1.015, hyp_len=23516, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.36.0.76-2.14.0.79-2.21.1.02-2.77.0.98-2.67.pth, rkmy
BLEU = 61.74, 81.1/67.9/56.1/47.0 (BP=1.000, ratio=1.035, hyp_len=24323, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.37.0.83-2.30.0.98-2.67.1.01-2.75.0.99-2.70.pth, myrk
BLEU = 65.54, 83.8/70.8/60.3/51.6 (BP=1.000, ratio=1.012, hyp_len=23427, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.37.0.83-2.30.0.98-2.67.1.01-2.75.0.99-2.70.pth, rkmy
BLEU = 61.55, 81.1/67.5/55.9/46.9 (BP=1.000, ratio=1.017, hyp_len=23919, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.38.0.72-2.06.0.81-2.24.0.97-2.65.0.98-2.66.pth, myrk
BLEU = 66.61, 84.0/71.7/61.5/53.1 (BP=1.000, ratio=1.016, hyp_len=23531, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.38.0.72-2.06.0.81-2.24.0.97-2.65.0.98-2.66.pth, rkmy
BLEU = 64.32, 83.1/70.1/58.8/50.0 (BP=1.000, ratio=1.007, hyp_len=23665, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.39.0.70-2.02.0.78-2.18.0.97-2.64.0.92-2.52.pth, myrk
BLEU = 66.91, 84.3/72.0/61.9/53.4 (BP=1.000, ratio=1.014, hyp_len=23485, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.39.0.70-2.02.0.78-2.18.0.97-2.64.0.92-2.52.pth, rkmy
BLEU = 64.29, 82.5/69.9/58.9/50.3 (BP=1.000, ratio=1.020, hyp_len=23975, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.40.0.70-2.02.0.71-2.03.1.05-2.86.0.89-2.42.pth, myrk
BLEU = 65.98, 83.9/71.1/60.8/52.3 (BP=1.000, ratio=1.003, hyp_len=23223, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.40.0.70-2.02.0.71-2.03.1.05-2.86.0.89-2.42.pth, rkmy
BLEU = 66.37, 83.7/71.8/61.1/52.8 (BP=1.000, ratio=1.023, hyp_len=24047, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.41.0.77-2.16.0.68-1.97.0.99-2.69.0.85-2.35.pth, myrk
BLEU = 65.28, 83.3/70.5/60.1/51.4 (BP=1.000, ratio=1.010, hyp_len=23403, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.41.0.77-2.16.0.68-1.97.0.99-2.69.0.85-2.35.pth, rkmy
BLEU = 66.35, 83.5/71.7/61.2/53.0 (BP=1.000, ratio=1.030, hyp_len=24205, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.42.0.70-2.02.0.65-1.91.0.92-2.52.0.87-2.38.pth, myrk
BLEU = 67.54, 84.3/72.4/62.7/54.4 (BP=1.000, ratio=1.020, hyp_len=23628, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.42.0.70-2.02.0.65-1.91.0.92-2.52.0.87-2.38.pth, rkmy
BLEU = 67.17, 84.2/72.5/62.0/53.8 (BP=1.000, ratio=1.025, hyp_len=24085, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.43.0.63-1.88.0.62-1.86.0.90-2.46.0.84-2.31.pth, myrk
BLEU = 68.79, 85.2/73.6/64.0/55.8 (BP=1.000, ratio=1.015, hyp_len=23501, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.43.0.63-1.88.0.62-1.86.0.90-2.46.0.84-2.31.pth, rkmy
BLEU = 67.20, 84.0/72.4/62.1/54.0 (BP=1.000, ratio=1.033, hyp_len=24287, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.44.0.63-1.88.0.70-2.02.0.90-2.47.0.86-2.36.pth, myrk
BLEU = 69.44, 85.4/74.1/64.7/56.7 (BP=1.000, ratio=1.017, hyp_len=23548, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.44.0.63-1.88.0.70-2.02.0.90-2.47.0.86-2.36.pth, rkmy
BLEU = 68.40, 84.6/73.3/63.4/55.6 (BP=1.000, ratio=1.022, hyp_len=24016, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.45.0.57-1.77.0.58-1.79.0.89-2.44.0.86-2.35.pth, myrk
BLEU = 70.22, 85.8/74.8/65.6/57.7 (BP=1.000, ratio=1.020, hyp_len=23617, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.45.0.57-1.77.0.58-1.79.0.89-2.44.0.86-2.35.pth, rkmy
BLEU = 68.34, 84.9/73.5/63.3/55.2 (BP=1.000, ratio=1.019, hyp_len=23950, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.46.0.61-1.84.0.77-2.16.0.89-2.42.0.96-2.61.pth, myrk
BLEU = 69.78, 85.4/74.4/65.1/57.3 (BP=1.000, ratio=1.023, hyp_len=23691, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.46.0.61-1.84.0.77-2.16.0.89-2.42.0.96-2.61.pth, rkmy
BLEU = 66.38, 84.0/71.9/61.1/52.6 (BP=1.000, ratio=1.013, hyp_len=23813, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.47.0.67-1.95.0.65-1.91.1.01-2.74.0.83-2.30.pth, myrk
BLEU = 64.30, 82.5/69.7/59.1/50.3 (BP=1.000, ratio=1.026, hyp_len=23758, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.47.0.67-1.95.0.65-1.91.1.01-2.74.0.83-2.30.pth, rkmy
BLEU = 67.70, 84.1/72.8/62.7/54.7 (BP=1.000, ratio=1.037, hyp_len=24372, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.48.0.65-1.92.0.59-1.81.0.96-2.61.0.81-2.24.pth, myrk
BLEU = 66.54, 83.9/71.6/61.6/53.0 (BP=1.000, ratio=1.016, hyp_len=23534, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.48.0.65-1.92.0.59-1.81.0.96-2.61.0.81-2.24.pth, rkmy
BLEU = 68.86, 84.7/73.9/63.9/56.2 (BP=1.000, ratio=1.033, hyp_len=24289, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.49.0.58-1.78.0.53-1.70.0.90-2.46.0.80-2.22.pth, myrk
BLEU = 67.27, 84.3/72.3/62.3/54.0 (BP=1.000, ratio=1.018, hyp_len=23584, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.49.0.58-1.78.0.53-1.70.0.90-2.46.0.80-2.22.pth, rkmy
BLEU = 70.48, 85.8/75.2/65.7/58.2 (BP=1.000, ratio=1.027, hyp_len=24139, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.50.0.58-1.79.0.51-1.66.0.88-2.40.0.79-2.20.pth, myrk
BLEU = 69.38, 85.3/74.0/64.7/56.8 (BP=1.000, ratio=1.013, hyp_len=23472, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.50.0.58-1.79.0.51-1.66.0.88-2.40.0.79-2.20.pth, rkmy
BLEU = 70.33, 85.5/75.1/65.6/58.1 (BP=1.000, ratio=1.034, hyp_len=24302, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.51.0.55-1.73.0.53-1.70.0.85-2.33.0.78-2.19.pth, myrk
BLEU = 69.36, 85.0/73.9/64.8/56.8 (BP=1.000, ratio=1.025, hyp_len=23731, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.51.0.55-1.73.0.53-1.70.0.85-2.33.0.78-2.19.pth, rkmy
BLEU = 69.41, 84.9/74.3/64.6/56.9 (BP=1.000, ratio=1.038, hyp_len=24407, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.52.0.55-1.74.0.50-1.65.0.87-2.38.0.78-2.19.pth, myrk
BLEU = 69.15, 85.1/73.9/64.4/56.4 (BP=1.000, ratio=1.030, hyp_len=23858, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.52.0.55-1.74.0.50-1.65.0.87-2.38.0.78-2.19.pth, rkmy
BLEU = 70.40, 85.6/75.2/65.7/58.1 (BP=1.000, ratio=1.031, hyp_len=24244, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.53.0.56-1.75.0.67-1.96.0.82-2.26.0.81-2.26.pth, myrk
BLEU = 71.12, 86.0/75.4/66.7/59.1 (BP=1.000, ratio=1.021, hyp_len=23639, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.53.0.56-1.75.0.67-1.96.0.82-2.26.0.81-2.26.pth, rkmy
BLEU = 69.49, 85.4/74.5/64.5/56.8 (BP=1.000, ratio=1.023, hyp_len=24058, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.54.0.50-1.65.0.55-1.73.0.81-2.24.0.79-2.21.pth, myrk
BLEU = 71.07, 86.0/75.4/66.6/59.0 (BP=1.000, ratio=1.022, hyp_len=23668, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.54.0.50-1.65.0.55-1.73.0.81-2.24.0.79-2.21.pth, rkmy
BLEU = 70.80, 85.8/75.4/66.1/58.8 (BP=1.000, ratio=1.025, hyp_len=24101, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.55.0.49-1.63.0.49-1.64.0.81-2.24.0.77-2.16.pth, myrk
BLEU = 71.88, 86.4/76.0/67.5/60.2 (BP=1.000, ratio=1.023, hyp_len=23699, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.55.0.49-1.63.0.49-1.64.0.81-2.24.0.77-2.16.pth, rkmy
BLEU = 72.00, 86.4/76.4/67.4/60.4 (BP=1.000, ratio=1.027, hyp_len=24140, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.56.0.47-1.60.0.47-1.60.0.81-2.25.0.78-2.18.pth, myrk
BLEU = 71.76, 86.6/76.1/67.3/59.8 (BP=1.000, ratio=1.018, hyp_len=23587, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.56.0.47-1.60.0.47-1.60.0.81-2.25.0.78-2.18.pth, rkmy
BLEU = 72.06, 86.4/76.5/67.5/60.3 (BP=1.000, ratio=1.030, hyp_len=24213, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.57.0.45-1.57.0.44-1.56.0.80-2.23.0.77-2.15.pth, myrk
BLEU = 71.20, 86.0/75.5/66.7/59.3 (BP=1.000, ratio=1.027, hyp_len=23780, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.57.0.45-1.57.0.44-1.56.0.80-2.23.0.77-2.15.pth, rkmy
BLEU = 73.07, 87.1/77.4/68.6/61.7 (BP=1.000, ratio=1.020, hyp_len=23978, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.58.0.44-1.55.0.44-1.55.0.80-2.23.0.75-2.12.pth, myrk
BLEU = 72.26, 86.7/76.5/67.9/60.6 (BP=1.000, ratio=1.025, hyp_len=23746, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.58.0.44-1.55.0.44-1.55.0.80-2.23.0.75-2.12.pth, rkmy
BLEU = 72.44, 86.7/76.9/67.9/60.9 (BP=1.000, ratio=1.030, hyp_len=24218, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.59.0.44-1.55.0.44-1.55.0.79-2.20.0.74-2.11.pth, myrk
BLEU = 72.02, 86.4/76.2/67.7/60.4 (BP=1.000, ratio=1.026, hyp_len=23754, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.59.0.44-1.55.0.44-1.55.0.79-2.20.0.74-2.11.pth, rkmy
BLEU = 72.36, 86.5/76.7/67.8/60.9 (BP=1.000, ratio=1.033, hyp_len=24286, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.60.0.43-1.53.0.42-1.52.0.78-2.18.0.74-2.10.pth, myrk
BLEU = 71.89, 86.2/76.0/67.5/60.3 (BP=1.000, ratio=1.028, hyp_len=23806, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.60.0.43-1.53.0.42-1.52.0.78-2.18.0.74-2.10.pth, rkmy
BLEU = 72.60, 86.5/76.9/68.2/61.3 (BP=1.000, ratio=1.033, hyp_len=24296, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.61.0.41-1.51.0.41-1.51.0.78-2.19.0.74-2.10.pth, myrk
BLEU = 72.61, 86.8/76.7/68.2/61.2 (BP=1.000, ratio=1.025, hyp_len=23732, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.61.0.41-1.51.0.41-1.51.0.78-2.19.0.74-2.10.pth, rkmy
BLEU = 72.66, 86.6/77.0/68.2/61.2 (BP=1.000, ratio=1.035, hyp_len=24321, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.62.0.40-1.49.0.40-1.49.0.78-2.19.0.75-2.12.pth, myrk
BLEU = 72.78, 86.7/76.8/68.5/61.5 (BP=1.000, ratio=1.024, hyp_len=23720, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.62.0.40-1.49.0.40-1.49.0.78-2.19.0.75-2.12.pth, rkmy
BLEU = 72.73, 86.6/76.9/68.3/61.5 (BP=1.000, ratio=1.034, hyp_len=24319, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.63.0.40-1.49.0.40-1.49.0.77-2.17.0.74-2.10.pth, myrk
BLEU = 72.62, 86.7/76.7/68.3/61.2 (BP=1.000, ratio=1.024, hyp_len=23709, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.63.0.40-1.49.0.40-1.49.0.77-2.17.0.74-2.10.pth, rkmy
BLEU = 72.79, 86.7/77.1/68.4/61.4 (BP=1.000, ratio=1.033, hyp_len=24291, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.64.0.40-1.49.0.41-1.51.0.78-2.19.0.83-2.29.pth, myrk
BLEU = 72.90, 86.9/77.0/68.7/61.5 (BP=1.000, ratio=1.026, hyp_len=23768, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.64.0.40-1.49.0.41-1.51.0.78-2.19.0.83-2.29.pth, rkmy
BLEU = 69.66, 84.8/74.5/65.0/57.4 (BP=1.000, ratio=1.047, hyp_len=24622, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.65.0.52-1.68.0.70-2.01.0.78-2.19.0.92-2.52.pth, myrk
BLEU = 72.06, 86.5/76.3/67.7/60.4 (BP=1.000, ratio=1.029, hyp_len=23842, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.65.0.52-1.68.0.70-2.01.0.78-2.19.0.92-2.52.pth, rkmy
BLEU = 69.00, 84.6/73.9/64.2/56.4 (BP=1.000, ratio=1.039, hyp_len=24427, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.66.0.43-1.53.0.49-1.63.0.78-2.17.0.74-2.10.pth, myrk
BLEU = 71.43, 86.1/75.7/67.0/59.6 (BP=1.000, ratio=1.030, hyp_len=23858, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.66.0.43-1.53.0.49-1.63.0.78-2.17.0.74-2.10.pth, rkmy
BLEU = 71.23, 86.0/75.8/66.6/59.3 (BP=1.000, ratio=1.035, hyp_len=24327, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.67.0.41-1.51.0.44-1.55.0.83-2.29.0.79-2.21.pth, myrk
BLEU = 70.44, 85.4/74.9/66.0/58.3 (BP=1.000, ratio=1.035, hyp_len=23962, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.67.0.41-1.51.0.44-1.55.0.83-2.29.0.79-2.21.pth, rkmy
BLEU = 69.96, 84.9/74.7/65.3/57.8 (BP=1.000, ratio=1.044, hyp_len=24547, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.68.0.40-1.49.0.42-1.53.0.79-2.21.0.85-2.34.pth, myrk
BLEU = 72.01, 86.4/76.3/67.6/60.3 (BP=1.000, ratio=1.029, hyp_len=23822, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.68.0.40-1.49.0.42-1.53.0.79-2.21.0.85-2.34.pth, rkmy
BLEU = 68.86, 84.2/73.9/64.3/56.3 (BP=1.000, ratio=1.052, hyp_len=24741, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.69.0.40-1.49.0.44-1.55.0.76-2.13.0.72-2.05.pth, myrk
BLEU = 72.57, 86.5/76.6/68.3/61.3 (BP=1.000, ratio=1.029, hyp_len=23821, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.69.0.40-1.49.0.44-1.55.0.76-2.13.0.72-2.05.pth, rkmy
BLEU = 72.53, 86.5/76.8/68.0/61.2 (BP=1.000, ratio=1.035, hyp_len=24329, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.70.0.38-1.47.0.40-1.49.0.75-2.13.0.69-2.00.pth, myrk
BLEU = 72.88, 86.7/76.9/68.6/61.6 (BP=1.000, ratio=1.029, hyp_len=23822, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.70.0.38-1.47.0.40-1.49.0.75-2.13.0.69-2.00.pth, rkmy
BLEU = 72.75, 86.6/77.0/68.3/61.4 (BP=1.000, ratio=1.037, hyp_len=24389, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.71.0.38-1.46.0.38-1.47.0.77-2.16.0.70-2.02.pth, myrk
BLEU = 72.60, 86.6/76.7/68.3/61.2 (BP=1.000, ratio=1.027, hyp_len=23789, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.71.0.38-1.46.0.38-1.47.0.77-2.16.0.70-2.02.pth, rkmy
BLEU = 73.42, 86.9/77.6/69.1/62.4 (BP=1.000, ratio=1.032, hyp_len=24253, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.72.0.42-1.53.0.39-1.48.0.79-2.21.0.70-2.01.pth, myrk
BLEU = 72.13, 86.6/76.3/67.7/60.4 (BP=1.000, ratio=1.019, hyp_len=23601, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.72.0.42-1.53.0.39-1.48.0.79-2.21.0.70-2.01.pth, rkmy
BLEU = 71.72, 85.9/76.1/67.2/60.2 (BP=1.000, ratio=1.046, hyp_len=24602, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.73.1.12-3.06.0.57-1.76.0.98-2.68.0.70-2.02.pth, myrk
BLEU = 62.32, 81.5/68.3/56.9/47.7 (BP=1.000, ratio=1.042, hyp_len=24123, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.73.1.12-3.06.0.57-1.76.0.98-2.68.0.70-2.02.pth, rkmy
BLEU = 72.70, 86.6/76.9/68.3/61.4 (BP=1.000, ratio=1.038, hyp_len=24413, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.74.0.47-1.61.0.35-1.42.0.76-2.14.0.70-2.01.pth, myrk
BLEU = 72.71, 87.0/76.8/68.4/61.2 (BP=1.000, ratio=1.022, hyp_len=23673, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.74.0.47-1.61.0.35-1.42.0.76-2.14.0.70-2.01.pth, rkmy
BLEU = 74.14, 87.3/78.2/69.9/63.3 (BP=1.000, ratio=1.032, hyp_len=24268, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.75.0.38-1.47.0.33-1.40.0.74-2.09.0.69-2.00.pth, myrk
BLEU = 72.91, 86.7/76.9/68.7/61.7 (BP=1.000, ratio=1.028, hyp_len=23810, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.75.0.38-1.47.0.33-1.40.0.74-2.09.0.69-2.00.pth, rkmy
BLEU = 73.94, 87.2/78.0/69.7/63.1 (BP=1.000, ratio=1.034, hyp_len=24306, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.76.0.38-1.46.0.36-1.43.0.74-2.09.0.70-2.02.pth, myrk
BLEU = 73.54, 87.2/77.5/69.3/62.4 (BP=1.000, ratio=1.025, hyp_len=23739, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.76.0.38-1.46.0.36-1.43.0.74-2.09.0.70-2.02.pth, rkmy
BLEU = 73.39, 86.9/77.4/69.0/62.4 (BP=1.000, ratio=1.035, hyp_len=24333, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.77.0.35-1.42.0.33-1.39.0.74-2.10.0.70-2.01.pth, myrk
BLEU = 73.34, 87.2/77.3/69.1/62.1 (BP=1.000, ratio=1.028, hyp_len=23810, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.77.0.35-1.42.0.33-1.39.0.74-2.10.0.70-2.01.pth, rkmy
BLEU = 74.37, 87.4/78.3/70.2/63.7 (BP=1.000, ratio=1.033, hyp_len=24289, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.78.0.34-1.41.0.33-1.39.0.74-2.09.0.71-2.03.pth, myrk
BLEU = 73.72, 87.2/77.6/69.6/62.7 (BP=1.000, ratio=1.028, hyp_len=23803, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.78.0.34-1.41.0.33-1.39.0.74-2.09.0.71-2.03.pth, rkmy
BLEU = 72.74, 86.5/77.0/68.4/61.5 (BP=1.000, ratio=1.040, hyp_len=24461, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.79.0.34-1.40.0.35-1.41.0.74-2.09.0.69-2.00.pth, myrk
BLEU = 73.25, 87.0/77.3/69.0/62.0 (BP=1.000, ratio=1.029, hyp_len=23836, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.79.0.34-1.40.0.35-1.41.0.74-2.09.0.69-2.00.pth, rkmy
BLEU = 73.02, 86.6/77.2/68.6/61.9 (BP=1.000, ratio=1.042, hyp_len=24485, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.80.0.35-1.42.0.39-1.48.0.73-2.08.0.73-2.07.pth, myrk
BLEU = 73.44, 87.0/77.4/69.3/62.3 (BP=1.000, ratio=1.027, hyp_len=23789, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.80.0.35-1.42.0.39-1.48.0.73-2.08.0.73-2.07.pth, rkmy
BLEU = 71.98, 85.9/76.4/67.6/60.5 (BP=1.000, ratio=1.044, hyp_len=24537, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.81.0.34-1.41.0.41-1.51.0.74-2.09.0.70-2.01.pth, myrk
BLEU = 72.94, 86.6/76.9/68.7/61.8 (BP=1.000, ratio=1.031, hyp_len=23885, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.81.0.34-1.41.0.41-1.51.0.74-2.09.0.70-2.01.pth, rkmy
BLEU = 72.83, 86.7/77.1/68.4/61.6 (BP=1.000, ratio=1.034, hyp_len=24305, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.82.0.33-1.40.0.37-1.44.0.77-2.15.0.68-1.97.pth, myrk
BLEU = 73.73, 87.1/77.6/69.6/62.8 (BP=1.000, ratio=1.024, hyp_len=23713, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.82.0.33-1.40.0.37-1.44.0.77-2.15.0.68-1.97.pth, rkmy
BLEU = 72.56, 86.3/76.7/68.1/61.4 (BP=1.000, ratio=1.044, hyp_len=24542, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.83.0.33-1.39.0.33-1.39.0.73-2.07.0.68-1.97.pth, myrk
BLEU = 73.39, 86.8/77.2/69.3/62.4 (BP=1.000, ratio=1.031, hyp_len=23884, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.83.0.33-1.39.0.33-1.39.0.73-2.07.0.68-1.97.pth, rkmy
BLEU = 73.24, 86.8/77.4/68.8/62.2 (BP=1.000, ratio=1.041, hyp_len=24463, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.84.0.31-1.37.0.32-1.37.0.74-2.09.0.68-1.98.pth, myrk
BLEU = 73.61, 87.0/77.5/69.5/62.7 (BP=1.000, ratio=1.029, hyp_len=23839, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.84.0.31-1.37.0.32-1.37.0.74-2.09.0.68-1.98.pth, rkmy
BLEU = 73.96, 87.1/77.9/69.7/63.3 (BP=1.000, ratio=1.038, hyp_len=24411, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.85.0.31-1.36.0.30-1.36.0.73-2.08.0.69-1.99.pth, myrk
BLEU = 74.11, 87.3/77.9/70.1/63.3 (BP=1.000, ratio=1.029, hyp_len=23826, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.85.0.31-1.36.0.30-1.36.0.73-2.08.0.69-1.99.pth, rkmy
BLEU = 74.00, 87.3/78.0/69.7/63.1 (BP=1.000, ratio=1.037, hyp_len=24385, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.86.0.31-1.36.0.31-1.37.0.74-2.09.0.70-2.01.pth, myrk
BLEU = 73.47, 86.8/77.3/69.4/62.6 (BP=1.000, ratio=1.031, hyp_len=23872, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.86.0.31-1.36.0.31-1.37.0.74-2.09.0.70-2.01.pth, rkmy
BLEU = 73.74, 87.0/77.8/69.4/62.9 (BP=1.000, ratio=1.036, hyp_len=24367, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.87.0.30-1.35.0.32-1.37.0.74-2.09.0.72-2.06.pth, myrk
BLEU = 74.12, 87.4/78.0/70.1/63.2 (BP=1.000, ratio=1.027, hyp_len=23788, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.87.0.30-1.35.0.32-1.37.0.74-2.09.0.72-2.06.pth, rkmy
BLEU = 73.78, 87.1/77.8/69.5/63.0 (BP=1.000, ratio=1.034, hyp_len=24306, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.88.0.29-1.34.0.31-1.36.0.73-2.08.0.70-2.02.pth, myrk
BLEU = 74.31, 87.5/78.1/70.2/63.5 (BP=1.000, ratio=1.027, hyp_len=23796, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.88.0.29-1.34.0.31-1.36.0.73-2.08.0.70-2.02.pth, rkmy
BLEU = 72.75, 86.3/76.8/68.4/61.8 (BP=1.000, ratio=1.046, hyp_len=24584, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.89.0.30-1.34.0.29-1.34.0.72-2.06.0.69-2.00.pth, myrk
BLEU = 73.57, 87.0/77.5/69.4/62.6 (BP=1.000, ratio=1.030, hyp_len=23850, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.89.0.30-1.34.0.29-1.34.0.72-2.06.0.69-2.00.pth, rkmy
BLEU = 72.63, 86.5/76.8/68.2/61.4 (BP=1.000, ratio=1.046, hyp_len=24600, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.90.0.28-1.32.0.28-1.32.0.74-2.09.0.71-2.04.pth, myrk
BLEU = 73.75, 86.9/77.6/69.7/62.9 (BP=1.000, ratio=1.031, hyp_len=23883, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.90.0.28-1.32.0.28-1.32.0.74-2.09.0.71-2.04.pth, rkmy
BLEU = 74.64, 87.5/78.5/70.4/64.1 (BP=1.000, ratio=1.035, hyp_len=24326, ref_len=23509)
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

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/myrk-100epoch
Evaluation result for the model: dsl-model-myrk.01.4.46-86.58.4.48-88.46.4.05-57.35.4.10-60.07.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 13.2/0.1/0.0/0.0 (BP=1.000, ratio=1.034, hyp_len=23943, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.01.4.46-86.58.4.48-88.46.4.05-57.35.4.10-60.07.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 17.5/0.0/0.0/0.0 (BP=1.000, ratio=1.052, hyp_len=24728, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.02.4.10-60.26.4.13-62.39.3.88-48.54.3.90-49.54.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 19.2/1.8/0.0/0.0 (BP=1.000, ratio=1.027, hyp_len=23776, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.02.4.10-60.26.4.13-62.39.3.88-48.54.3.90-49.54.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 19.1/1.2/0.1/0.0 (BP=0.972, ratio=0.973, hyp_len=22863, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.03.4.03-56.41.4.07-58.78.3.80-44.68.3.84-46.47.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 18.9/1.7/0.0/0.0 (BP=1.000, ratio=1.010, hyp_len=23390, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.03.4.03-56.41.4.07-58.78.3.80-44.68.3.84-46.47.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 20.5/2.4/0.0/0.0 (BP=0.996, ratio=0.996, hyp_len=23409, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.04.3.90-49.48.3.96-52.49.3.67-39.33.3.74-42.02.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.1/2.0/0.0/0.0 (BP=1.000, ratio=1.006, hyp_len=23310, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.04.3.90-49.48.3.96-52.49.3.67-39.33.3.74-42.02.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.6/2.7/0.3/0.0 (BP=0.978, ratio=0.978, hyp_len=22987, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.05.3.83-45.94.3.91-49.98.3.57-35.67.3.66-38.96.pth, myrk
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 25.4/3.5/0.2/0.0 (BP=1.000, ratio=1.011, hyp_len=23404, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.05.3.83-45.94.3.91-49.98.3.57-35.67.3.66-38.96.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.1/3.0/0.2/0.0 (BP=0.978, ratio=0.978, hyp_len=22993, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.06.3.66-38.93.3.77-43.40.3.48-32.46.3.58-35.96.pth, myrk
BLEU = 0.99, 24.6/3.8/0.3/0.0 (BP=1.000, ratio=1.006, hyp_len=23289, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.06.3.66-38.93.3.77-43.40.3.48-32.46.3.58-35.96.pth, rkmy
Use of uninitialized value in division (/) at /home/ye/exp/simple-nmt/test/multi-bleu.perl line 139, <STDIN> line 1811.
BLEU = 0.00, 23.0/3.7/0.4/0.0 (BP=0.989, ratio=0.989, hyp_len=23241, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.07.3.64-38.13.3.76-42.91.3.38-29.44.3.51-33.43.pth, myrk
BLEU = 1.64, 27.5/5.6/0.8/0.1 (BP=1.000, ratio=1.003, hyp_len=23220, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.07.3.64-38.13.3.76-42.91.3.38-29.44.3.51-33.43.pth, rkmy
BLEU = 1.14, 24.1/4.8/0.6/0.0 (BP=0.987, ratio=0.987, hyp_len=23210, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.08.3.52-33.95.3.67-39.34.3.27-26.40.3.40-30.01.pth, myrk
BLEU = 2.39, 29.8/7.0/0.8/0.2 (BP=1.000, ratio=1.011, hyp_len=23424, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.08.3.52-33.95.3.67-39.34.3.27-26.40.3.40-30.01.pth, rkmy
BLEU = 1.42, 25.5/6.3/1.0/0.0 (BP=0.990, ratio=0.990, hyp_len=23266, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.09.3.32-27.63.3.48-32.60.3.14-23.14.3.24-25.50.pth, myrk
BLEU = 5.40, 34.8/11.8/3.1/0.7 (BP=1.000, ratio=1.004, hyp_len=23248, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.09.3.32-27.63.3.48-32.60.3.14-23.14.3.24-25.50.pth, rkmy
BLEU = 1.70, 28.5/7.2/1.3/0.0 (BP=0.983, ratio=0.983, hyp_len=23113, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.100.0.26-1.30.0.28-1.32.0.71-2.02.0.67-1.95.pth, myrk
BLEU = 74.87, 87.8/78.5/70.9/64.3 (BP=1.000, ratio=1.026, hyp_len=23769, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.100.0.26-1.30.0.28-1.32.0.71-2.02.0.67-1.95.pth, rkmy
BLEU = 72.15, 86.1/76.4/67.7/60.9 (BP=1.000, ratio=1.050, hyp_len=24673, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.10.3.25-25.89.3.39-29.59.2.95-19.16.3.07-21.53.pth, myrk
BLEU = 7.03, 38.5/14.8/4.3/1.0 (BP=1.000, ratio=1.010, hyp_len=23394, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.10.3.25-25.89.3.39-29.59.2.95-19.16.3.07-21.53.pth, rkmy
BLEU = 2.56, 31.5/9.0/1.5/0.1 (BP=0.976, ratio=0.977, hyp_len=22960, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.11.2.94-19.00.3.16-23.61.2.72-15.24.2.91-18.37.pth, myrk
BLEU = 10.99, 43.7/18.7/7.1/2.5 (BP=0.999, ratio=0.999, hyp_len=23127, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.11.2.94-19.00.3.16-23.61.2.72-15.24.2.91-18.37.pth, rkmy
BLEU = 4.79, 34.8/11.2/2.5/0.6 (BP=0.970, ratio=0.970, hyp_len=22804, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.12.2.66-14.29.2.88-17.81.2.50-12.16.2.68-14.61.pth, myrk
BLEU = 14.13, 47.1/22.1/9.5/4.0 (BP=1.000, ratio=1.009, hyp_len=23368, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.12.2.66-14.29.2.88-17.81.2.50-12.16.2.68-14.61.pth, rkmy
BLEU = 7.37, 37.8/14.0/4.2/1.3 (BP=1.000, ratio=1.005, hyp_len=23632, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.13.2.52-12.41.2.70-14.95.2.33-10.33.2.51-12.29.pth, myrk
BLEU = 16.02, 49.2/24.3/11.2/4.9 (BP=1.000, ratio=1.007, hyp_len=23320, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.13.2.52-12.41.2.70-14.95.2.33-10.33.2.51-12.29.pth, rkmy
BLEU = 9.56, 40.6/17.0/6.0/2.0 (BP=1.000, ratio=1.025, hyp_len=24103, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.14.2.30-9.93.2.53-12.61.2.18-8.81.2.40-11.05.pth, myrk
BLEU = 20.05, 53.5/28.4/14.5/7.4 (BP=1.000, ratio=1.001, hyp_len=23186, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.14.2.30-9.93.2.53-12.61.2.18-8.81.2.40-11.05.pth, rkmy
BLEU = 11.28, 43.1/19.0/7.3/2.7 (BP=0.999, ratio=0.999, hyp_len=23493, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.15.2.11-8.27.2.29-9.91.2.02-7.53.2.18-8.87.pth, myrk
BLEU = 24.92, 58.0/33.3/18.9/10.6 (BP=1.000, ratio=1.004, hyp_len=23262, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.15.2.11-8.27.2.29-9.91.2.02-7.53.2.18-8.87.pth, rkmy
BLEU = 17.25, 49.2/25.3/12.2/5.8 (BP=1.000, ratio=1.017, hyp_len=23903, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.16.2.01-7.47.2.21-9.11.1.92-6.83.2.05-7.73.pth, myrk
BLEU = 28.25, 60.5/36.6/22.0/13.1 (BP=1.000, ratio=1.004, hyp_len=23246, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.16.2.01-7.47.2.21-9.11.1.92-6.83.2.05-7.73.pth, rkmy
BLEU = 19.59, 51.9/28.1/14.1/7.2 (BP=1.000, ratio=1.012, hyp_len=23799, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.17.1.87-6.52.1.99-7.31.1.81-6.14.1.88-6.54.pth, myrk
BLEU = 32.37, 63.9/40.6/25.9/16.5 (BP=0.997, ratio=0.997, hyp_len=23095, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.17.1.87-6.52.1.99-7.31.1.81-6.14.1.88-6.54.pth, rkmy
BLEU = 24.43, 56.1/33.0/18.5/10.4 (BP=1.000, ratio=1.018, hyp_len=23921, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.18.1.75-5.73.1.84-6.30.1.69-5.42.1.74-5.70.pth, myrk
BLEU = 36.49, 66.8/44.7/29.8/19.9 (BP=1.000, ratio=1.000, hyp_len=23168, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.18.1.75-5.73.1.84-6.30.1.69-5.42.1.74-5.70.pth, rkmy
BLEU = 28.53, 59.5/37.1/22.4/13.4 (BP=1.000, ratio=1.017, hyp_len=23901, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.19.1.59-4.89.1.69-5.44.1.62-5.06.1.66-5.26.pth, myrk
BLEU = 38.53, 68.2/46.9/31.9/21.6 (BP=1.000, ratio=1.008, hyp_len=23341, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.19.1.59-4.89.1.69-5.44.1.62-5.06.1.66-5.26.pth, rkmy
BLEU = 31.63, 62.6/40.4/25.3/15.8 (BP=0.998, ratio=0.998, hyp_len=23453, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.20.1.56-4.75.1.58-4.88.1.61-5.02.1.63-5.13.pth, myrk
BLEU = 38.79, 68.0/47.1/32.2/22.0 (BP=1.000, ratio=1.016, hyp_len=23539, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.20.1.56-4.75.1.58-4.88.1.61-5.02.1.63-5.13.pth, rkmy
BLEU = 34.08, 65.0/43.1/28.0/18.2 (BP=0.986, ratio=0.986, hyp_len=23184, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.21.1.46-4.29.1.52-4.58.1.45-4.25.1.83-6.24.pth, myrk
BLEU = 45.41, 72.4/53.0/38.9/28.5 (BP=1.000, ratio=1.013, hyp_len=23461, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.21.1.46-4.29.1.52-4.58.1.45-4.25.1.83-6.24.pth, rkmy
BLEU = 27.48, 59.7/36.4/21.5/12.5 (BP=0.996, ratio=0.996, hyp_len=23404, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.22.1.40-4.04.1.71-5.55.1.41-4.11.1.62-5.06.pth, myrk
BLEU = 47.30, 73.4/54.6/40.8/30.6 (BP=1.000, ratio=1.016, hyp_len=23520, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.22.1.40-4.04.1.71-5.55.1.41-4.11.1.62-5.06.pth, rkmy
BLEU = 34.48, 64.7/43.3/27.9/18.1 (BP=1.000, ratio=1.021, hyp_len=23996, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.23.1.30-3.68.1.28-3.60.1.36-3.90.1.33-3.79.pth, myrk
BLEU = 49.18, 74.7/56.2/42.6/32.7 (BP=1.000, ratio=1.009, hyp_len=23378, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.23.1.30-3.68.1.28-3.60.1.36-3.90.1.33-3.79.pth, rkmy
BLEU = 45.94, 71.8/53.5/39.5/29.4 (BP=1.000, ratio=1.014, hyp_len=23841, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.24.1.35-3.84.1.26-3.51.1.33-3.80.1.26-3.53.pth, myrk
BLEU = 50.00, 75.3/57.2/43.6/33.3 (BP=1.000, ratio=1.014, hyp_len=23485, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.24.1.35-3.84.1.26-3.51.1.33-3.80.1.26-3.53.pth, rkmy
BLEU = 49.11, 73.7/56.4/42.7/32.8 (BP=1.000, ratio=1.021, hyp_len=23994, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.25.1.14-3.14.1.13-3.08.1.22-3.37.1.24-3.45.pth, myrk
BLEU = 53.64, 77.4/60.5/47.4/37.3 (BP=1.000, ratio=1.014, hyp_len=23485, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.25.1.14-3.14.1.13-3.08.1.22-3.37.1.24-3.45.pth, rkmy
BLEU = 49.99, 74.4/57.3/43.6/33.6 (BP=1.000, ratio=1.023, hyp_len=24061, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.26.1.11-3.03.1.11-3.03.1.18-3.25.1.16-3.18.pth, myrk
BLEU = 55.50, 78.5/62.1/49.3/39.5 (BP=1.000, ratio=1.018, hyp_len=23578, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.26.1.11-3.03.1.11-3.03.1.18-3.25.1.16-3.18.pth, rkmy
BLEU = 53.80, 76.6/60.6/47.7/37.9 (BP=1.000, ratio=1.018, hyp_len=23921, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.27.1.08-2.95.1.05-2.86.1.15-3.17.1.13-3.10.pth, myrk
BLEU = 56.93, 79.2/63.4/50.9/41.1 (BP=1.000, ratio=1.016, hyp_len=23525, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.27.1.08-2.95.1.05-2.86.1.15-3.17.1.13-3.10.pth, rkmy
BLEU = 56.27, 78.3/62.9/50.1/40.6 (BP=1.000, ratio=1.015, hyp_len=23864, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.28.0.96-2.62.0.97-2.63.1.12-3.05.1.07-2.91.pth, myrk
BLEU = 59.26, 80.6/65.4/53.3/43.9 (BP=1.000, ratio=1.013, hyp_len=23469, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.28.0.96-2.62.0.97-2.63.1.12-3.05.1.07-2.91.pth, rkmy
BLEU = 57.58, 79.0/64.0/51.6/42.1 (BP=1.000, ratio=1.015, hyp_len=23866, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.29.1.06-2.88.1.04-2.84.1.10-3.01.1.15-3.14.pth, myrk
BLEU = 60.10, 81.3/66.2/54.3/44.7 (BP=1.000, ratio=1.000, hyp_len=23171, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.29.1.06-2.88.1.04-2.84.1.10-3.01.1.15-3.14.pth, rkmy
BLEU = 57.49, 79.4/64.1/51.4/41.7 (BP=1.000, ratio=1.000, hyp_len=23520, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.30.1.37-3.92.0.98-2.65.1.59-4.92.1.01-2.75.pth, myrk
BLEU = 45.74, 73.7/53.8/38.9/28.4 (BP=1.000, ratio=1.001, hyp_len=23173, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.30.1.37-3.92.0.98-2.65.1.59-4.92.1.01-2.75.pth, rkmy
BLEU = 59.90, 80.1/66.0/54.1/45.0 (BP=1.000, ratio=1.014, hyp_len=23841, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.31.0.97-2.64.0.87-2.39.1.04-2.84.0.99-2.69.pth, myrk
BLEU = 62.14, 82.0/67.9/56.5/47.3 (BP=1.000, ratio=1.008, hyp_len=23341, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.31.0.97-2.64.0.87-2.39.1.04-2.84.0.99-2.69.pth, rkmy
BLEU = 61.05, 80.9/67.2/55.4/46.2 (BP=1.000, ratio=1.020, hyp_len=23973, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.32.0.84-2.31.0.89-2.44.1.01-2.74.1.07-2.91.pth, myrk
BLEU = 63.95, 83.1/69.5/58.5/49.5 (BP=1.000, ratio=1.014, hyp_len=23477, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.32.0.84-2.31.0.89-2.44.1.01-2.74.1.07-2.91.pth, rkmy
BLEU = 58.40, 79.4/65.0/52.5/42.9 (BP=1.000, ratio=1.033, hyp_len=24278, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.33.0.79-2.21.0.79-2.20.0.98-2.67.0.95-2.58.pth, myrk
BLEU = 65.13, 83.9/70.6/59.8/50.9 (BP=1.000, ratio=1.008, hyp_len=23350, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.33.0.79-2.21.0.79-2.20.0.98-2.67.0.95-2.58.pth, rkmy
BLEU = 62.22, 81.5/68.1/56.6/47.7 (BP=1.000, ratio=1.023, hyp_len=24038, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.34.0.80-2.23.0.82-2.26.0.95-2.59.0.91-2.49.pth, myrk
BLEU = 65.04, 83.7/70.6/59.6/50.8 (BP=1.000, ratio=1.018, hyp_len=23585, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.34.0.80-2.23.0.82-2.26.0.95-2.59.0.91-2.49.pth, rkmy
BLEU = 64.09, 82.4/69.8/58.7/49.9 (BP=1.000, ratio=1.027, hyp_len=24140, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.35.0.75-2.12.0.80-2.22.0.94-2.55.0.94-2.56.pth, myrk
BLEU = 67.50, 84.8/72.6/62.4/54.0 (BP=1.000, ratio=1.014, hyp_len=23483, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.35.0.75-2.12.0.80-2.22.0.94-2.55.0.94-2.56.pth, rkmy
BLEU = 63.27, 81.9/69.0/57.7/49.1 (BP=1.000, ratio=1.023, hyp_len=24038, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.36.0.74-2.10.0.87-2.38.0.91-2.49.0.93-2.53.pth, myrk
BLEU = 67.53, 84.9/72.7/62.4/54.0 (BP=1.000, ratio=1.017, hyp_len=23547, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.36.0.74-2.10.0.87-2.38.0.91-2.49.0.93-2.53.pth, rkmy
BLEU = 62.63, 81.6/68.5/57.1/48.2 (BP=1.000, ratio=1.032, hyp_len=24257, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.37.0.73-2.07.0.74-2.09.0.91-2.48.0.85-2.33.pth, myrk
BLEU = 66.89, 84.5/72.1/61.7/53.3 (BP=1.000, ratio=1.024, hyp_len=23714, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.37.0.73-2.07.0.74-2.09.0.91-2.48.0.85-2.33.pth, rkmy
BLEU = 67.34, 84.3/72.5/62.2/54.0 (BP=1.000, ratio=1.019, hyp_len=23950, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.38.0.63-1.87.0.62-1.86.0.89-2.45.0.85-2.34.pth, myrk
BLEU = 68.95, 85.8/73.9/64.0/55.7 (BP=1.000, ratio=1.012, hyp_len=23441, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.38.0.63-1.87.0.62-1.86.0.89-2.45.0.85-2.34.pth, rkmy
BLEU = 67.32, 84.1/72.5/62.2/54.1 (BP=1.000, ratio=1.024, hyp_len=24073, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.39.0.70-2.01.0.65-1.92.0.91-2.49.0.82-2.28.pth, myrk
BLEU = 67.04, 84.7/72.3/61.9/53.4 (BP=1.000, ratio=1.018, hyp_len=23571, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.39.0.70-2.01.0.65-1.92.0.91-2.49.0.82-2.28.pth, rkmy
BLEU = 67.82, 84.4/72.9/62.8/54.8 (BP=1.000, ratio=1.026, hyp_len=24122, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.40.0.61-1.84.0.60-1.82.0.89-2.44.0.91-2.49.pth, myrk
BLEU = 69.52, 85.8/74.4/64.8/56.5 (BP=1.000, ratio=1.018, hyp_len=23569, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.40.0.61-1.84.0.60-1.82.0.89-2.44.0.91-2.49.pth, rkmy
BLEU = 69.13, 85.8/74.2/64.1/56.1 (BP=1.000, ratio=1.000, hyp_len=23499, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.41.0.63-1.88.0.66-1.94.0.88-2.40.0.88-2.40.pth, myrk
BLEU = 70.18, 86.1/74.8/65.4/57.5 (BP=1.000, ratio=1.015, hyp_len=23510, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.41.0.63-1.88.0.66-1.94.0.88-2.40.0.88-2.40.pth, rkmy
BLEU = 64.96, 82.9/70.6/59.6/51.1 (BP=1.000, ratio=1.035, hyp_len=24321, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.42.0.59-1.80.0.61-1.85.0.86-2.37.0.82-2.26.pth, myrk
BLEU = 70.64, 86.3/75.2/66.0/58.1 (BP=1.000, ratio=1.016, hyp_len=23528, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.42.0.59-1.80.0.61-1.85.0.86-2.37.0.82-2.26.pth, rkmy
BLEU = 68.67, 84.8/73.6/63.7/55.9 (BP=1.000, ratio=1.025, hyp_len=24085, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.43.0.87-2.38.0.64-1.90.1.05-2.85.0.81-2.24.pth, myrk
BLEU = 64.31, 83.7/70.0/58.8/49.7 (BP=1.000, ratio=1.000, hyp_len=23171, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.43.0.87-2.38.0.64-1.90.1.05-2.85.0.81-2.24.pth, rkmy
BLEU = 68.46, 84.7/73.5/63.5/55.6 (BP=1.000, ratio=1.030, hyp_len=24218, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.44.1.14-3.13.0.76-2.13.1.02-2.77.0.89-2.44.pth, myrk
BLEU = 58.72, 79.1/64.9/53.2/43.5 (BP=1.000, ratio=1.044, hyp_len=24176, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.44.1.14-3.13.0.76-2.13.1.02-2.77.0.89-2.44.pth, rkmy
BLEU = 66.34, 83.7/71.6/61.1/52.8 (BP=1.000, ratio=1.016, hyp_len=23876, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.45.0.72-2.05.0.80-2.23.0.83-2.30.0.86-2.37.pth, myrk
BLEU = 70.32, 86.1/74.9/65.6/57.7 (BP=1.000, ratio=1.018, hyp_len=23576, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.45.0.72-2.05.0.80-2.23.0.83-2.30.0.86-2.37.pth, rkmy
BLEU = 66.74, 83.8/71.9/61.6/53.4 (BP=1.000, ratio=1.025, hyp_len=24106, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.46.0.60-1.82.0.66-1.93.0.83-2.29.0.86-2.37.pth, myrk
BLEU = 71.37, 86.7/75.9/66.7/59.1 (BP=1.000, ratio=1.015, hyp_len=23518, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.46.0.60-1.82.0.66-1.93.0.83-2.29.0.86-2.37.pth, rkmy
BLEU = 66.36, 83.8/71.6/61.1/52.9 (BP=1.000, ratio=1.019, hyp_len=23965, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.47.0.55-1.74.0.57-1.77.0.82-2.26.0.78-2.19.pth, myrk
BLEU = 71.57, 86.7/76.0/67.0/59.5 (BP=1.000, ratio=1.017, hyp_len=23547, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.47.0.55-1.74.0.57-1.77.0.82-2.26.0.78-2.19.pth, rkmy
BLEU = 70.11, 85.6/74.9/65.3/57.8 (BP=1.000, ratio=1.026, hyp_len=24115, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.48.0.63-1.88.0.86-2.37.0.81-2.24.0.92-2.52.pth, myrk
BLEU = 71.92, 86.8/76.3/67.4/60.0 (BP=1.000, ratio=1.019, hyp_len=23592, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.48.0.63-1.88.0.86-2.37.0.81-2.24.0.92-2.52.pth, rkmy
BLEU = 64.40, 82.6/69.9/58.9/50.6 (BP=1.000, ratio=1.021, hyp_len=24007, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.49.0.50-1.66.0.57-1.77.0.80-2.23.0.79-2.20.pth, myrk
BLEU = 72.33, 87.0/76.6/67.9/60.5 (BP=1.000, ratio=1.019, hyp_len=23608, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.49.0.50-1.66.0.57-1.77.0.80-2.23.0.79-2.20.pth, rkmy
BLEU = 69.74, 85.5/74.5/64.8/57.2 (BP=1.000, ratio=1.017, hyp_len=23901, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.50.0.50-1.66.0.53-1.71.0.79-2.21.0.74-2.09.pth, myrk
BLEU = 72.00, 86.8/76.3/67.5/60.1 (BP=1.000, ratio=1.020, hyp_len=23625, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.50.0.50-1.66.0.53-1.71.0.79-2.21.0.74-2.09.pth, rkmy
BLEU = 70.68, 85.7/75.3/66.0/58.6 (BP=1.000, ratio=1.032, hyp_len=24268, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.51.0.51-1.66.0.53-1.70.0.78-2.18.0.74-2.09.pth, myrk
BLEU = 72.60, 87.1/76.8/68.2/60.9 (BP=1.000, ratio=1.019, hyp_len=23608, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.51.0.51-1.66.0.53-1.70.0.78-2.18.0.74-2.09.pth, rkmy
BLEU = 71.29, 86.1/75.8/66.6/59.4 (BP=1.000, ratio=1.028, hyp_len=24175, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.52.0.48-1.62.0.49-1.63.0.78-2.19.0.73-2.08.pth, myrk
BLEU = 72.47, 86.9/76.7/68.1/60.8 (BP=1.000, ratio=1.022, hyp_len=23678, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.52.0.48-1.62.0.49-1.63.0.78-2.19.0.73-2.08.pth, rkmy
BLEU = 72.18, 86.7/76.6/67.6/60.5 (BP=1.000, ratio=1.025, hyp_len=24085, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.53.0.45-1.57.0.45-1.57.0.77-2.17.0.73-2.07.pth, myrk
BLEU = 72.72, 87.0/76.9/68.4/61.2 (BP=1.000, ratio=1.021, hyp_len=23646, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.53.0.45-1.57.0.45-1.57.0.77-2.17.0.73-2.07.pth, rkmy
BLEU = 72.81, 86.9/77.1/68.3/61.4 (BP=1.000, ratio=1.025, hyp_len=24102, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.54.0.46-1.59.0.47-1.61.0.77-2.16.0.72-2.05.pth, myrk
BLEU = 73.69, 87.7/77.7/69.4/62.3 (BP=1.000, ratio=1.016, hyp_len=23520, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.54.0.46-1.59.0.47-1.61.0.77-2.16.0.72-2.05.pth, rkmy
BLEU = 71.60, 86.2/76.1/67.0/59.8 (BP=1.000, ratio=1.033, hyp_len=24292, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.55.0.47-1.59.0.47-1.61.0.78-2.18.0.72-2.05.pth, myrk
BLEU = 72.61, 86.9/76.8/68.3/61.0 (BP=1.000, ratio=1.023, hyp_len=23700, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.55.0.47-1.59.0.47-1.61.0.78-2.18.0.72-2.05.pth, rkmy
BLEU = 71.90, 86.3/76.2/67.4/60.3 (BP=1.000, ratio=1.032, hyp_len=24273, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.56.0.44-1.55.0.45-1.57.0.77-2.17.0.70-2.02.pth, myrk
BLEU = 73.05, 87.3/77.2/68.7/61.5 (BP=1.000, ratio=1.022, hyp_len=23671, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.56.0.44-1.55.0.45-1.57.0.77-2.17.0.70-2.02.pth, rkmy
BLEU = 72.19, 86.4/76.5/67.7/60.7 (BP=1.000, ratio=1.032, hyp_len=24258, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.57.0.42-1.52.0.43-1.53.0.76-2.14.0.71-2.03.pth, myrk
BLEU = 73.30, 87.2/77.3/69.1/62.0 (BP=1.000, ratio=1.022, hyp_len=23661, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.57.0.42-1.52.0.43-1.53.0.76-2.14.0.71-2.03.pth, rkmy
BLEU = 72.40, 86.6/76.7/67.8/60.9 (BP=1.000, ratio=1.030, hyp_len=24218, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.58.0.42-1.52.0.42-1.53.0.76-2.13.0.70-2.02.pth, myrk
BLEU = 72.91, 86.9/76.9/68.6/61.6 (BP=1.000, ratio=1.023, hyp_len=23699, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.58.0.42-1.52.0.42-1.53.0.76-2.13.0.70-2.02.pth, rkmy
BLEU = 72.28, 86.5/76.6/67.7/60.8 (BP=1.000, ratio=1.033, hyp_len=24294, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.59.0.42-1.52.0.42-1.52.0.76-2.14.0.70-2.01.pth, myrk
BLEU = 73.43, 87.4/77.5/69.2/62.1 (BP=1.000, ratio=1.022, hyp_len=23665, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.59.0.42-1.52.0.42-1.52.0.76-2.14.0.70-2.01.pth, rkmy
BLEU = 73.04, 86.9/77.3/68.5/61.9 (BP=1.000, ratio=1.032, hyp_len=24268, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.60.0.43-1.54.0.42-1.52.0.76-2.14.0.70-2.02.pth, myrk
BLEU = 72.04, 86.4/76.3/67.7/60.4 (BP=1.000, ratio=1.028, hyp_len=23814, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.60.0.43-1.54.0.42-1.52.0.76-2.14.0.70-2.02.pth, rkmy
BLEU = 72.15, 86.3/76.4/67.6/60.8 (BP=1.000, ratio=1.036, hyp_len=24357, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.61.0.41-1.50.0.41-1.51.0.76-2.14.0.71-2.03.pth, myrk
BLEU = 72.91, 86.9/77.0/68.6/61.5 (BP=1.000, ratio=1.023, hyp_len=23700, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.61.0.41-1.50.0.41-1.51.0.76-2.14.0.71-2.03.pth, rkmy
BLEU = 72.63, 86.8/77.0/68.1/61.1 (BP=1.000, ratio=1.028, hyp_len=24176, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.62.0.41-1.51.0.43-1.54.0.74-2.10.0.71-2.04.pth, myrk
BLEU = 73.11, 87.0/77.1/68.9/61.8 (BP=1.000, ratio=1.025, hyp_len=23746, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.62.0.41-1.51.0.43-1.54.0.74-2.10.0.71-2.04.pth, rkmy
BLEU = 71.09, 85.7/75.5/66.4/59.4 (BP=1.000, ratio=1.043, hyp_len=24529, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.63.0.41-1.50.0.44-1.55.0.74-2.10.0.70-2.01.pth, myrk
BLEU = 73.91, 87.3/77.7/69.8/63.0 (BP=1.000, ratio=1.024, hyp_len=23709, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.63.0.41-1.50.0.44-1.55.0.74-2.10.0.70-2.01.pth, rkmy
BLEU = 72.71, 86.8/77.1/68.2/61.3 (BP=1.000, ratio=1.032, hyp_len=24270, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.64.0.39-1.48.0.40-1.50.0.74-2.10.0.69-1.99.pth, myrk
BLEU = 72.78, 86.8/76.9/68.5/61.4 (BP=1.000, ratio=1.029, hyp_len=23823, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.64.0.39-1.48.0.40-1.50.0.74-2.10.0.69-1.99.pth, rkmy
BLEU = 72.57, 86.7/76.9/68.1/61.1 (BP=1.000, ratio=1.034, hyp_len=24309, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.65.0.39-1.48.0.41-1.51.0.75-2.12.0.70-2.01.pth, myrk
BLEU = 73.30, 87.1/77.3/69.1/62.1 (BP=1.000, ratio=1.024, hyp_len=23711, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.65.0.39-1.48.0.41-1.51.0.75-2.12.0.70-2.01.pth, rkmy
BLEU = 71.73, 86.1/76.1/67.1/60.2 (BP=1.000, ratio=1.041, hyp_len=24476, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.66.0.37-1.45.0.37-1.45.0.73-2.08.0.68-1.98.pth, myrk
BLEU = 73.35, 87.1/77.3/69.1/62.3 (BP=1.000, ratio=1.026, hyp_len=23766, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.66.0.37-1.45.0.37-1.45.0.73-2.08.0.68-1.98.pth, rkmy
BLEU = 72.88, 86.7/77.1/68.4/61.8 (BP=1.000, ratio=1.037, hyp_len=24371, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.67.0.37-1.45.0.37-1.45.0.73-2.08.0.69-1.99.pth, myrk
BLEU = 73.39, 87.1/77.3/69.2/62.3 (BP=1.000, ratio=1.025, hyp_len=23746, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.67.0.37-1.45.0.37-1.45.0.73-2.08.0.69-1.99.pth, rkmy
BLEU = 73.16, 86.8/77.3/68.8/62.1 (BP=1.000, ratio=1.035, hyp_len=24326, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.68.0.39-1.48.0.37-1.45.0.73-2.08.0.69-2.00.pth, myrk
BLEU = 73.15, 86.9/77.2/69.0/61.9 (BP=1.000, ratio=1.026, hyp_len=23767, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.68.0.39-1.48.0.37-1.45.0.73-2.08.0.69-2.00.pth, rkmy
BLEU = 71.90, 86.2/76.3/67.3/60.3 (BP=1.000, ratio=1.045, hyp_len=24564, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.69.0.50-1.64.0.38-1.46.0.78-2.18.0.68-1.97.pth, myrk
BLEU = 73.03, 87.1/77.2/68.7/61.6 (BP=1.000, ratio=1.016, hyp_len=23519, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.69.0.50-1.64.0.38-1.46.0.78-2.18.0.68-1.97.pth, rkmy
BLEU = 72.90, 86.7/77.1/68.4/61.8 (BP=1.000, ratio=1.038, hyp_len=24405, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.70.0.46-1.59.0.35-1.43.0.72-2.06.0.67-1.96.pth, myrk
BLEU = 73.08, 87.0/77.0/68.8/61.9 (BP=1.000, ratio=1.022, hyp_len=23679, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.70.0.46-1.59.0.35-1.43.0.72-2.06.0.67-1.96.pth, rkmy
BLEU = 73.28, 86.9/77.5/68.9/62.1 (BP=1.000, ratio=1.035, hyp_len=24337, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.71.0.40-1.50.0.35-1.42.0.72-2.05.0.67-1.96.pth, myrk
BLEU = 73.35, 87.2/77.4/69.1/62.1 (BP=1.000, ratio=1.025, hyp_len=23738, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.71.0.40-1.50.0.35-1.42.0.72-2.05.0.67-1.96.pth, rkmy
BLEU = 73.16, 86.9/77.3/68.7/62.0 (BP=1.000, ratio=1.036, hyp_len=24365, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.72.0.38-1.47.0.36-1.44.0.71-2.03.0.68-1.98.pth, myrk
BLEU = 73.86, 87.2/77.7/69.7/62.9 (BP=1.000, ratio=1.025, hyp_len=23738, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.72.0.38-1.47.0.36-1.44.0.71-2.03.0.68-1.98.pth, rkmy
BLEU = 71.24, 85.8/75.7/66.6/59.5 (BP=1.000, ratio=1.044, hyp_len=24539, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.73.0.35-1.42.0.34-1.41.0.73-2.07.0.67-1.95.pth, myrk
BLEU = 73.94, 87.4/77.9/69.8/62.9 (BP=1.000, ratio=1.025, hyp_len=23733, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.73.0.35-1.42.0.34-1.41.0.73-2.07.0.67-1.95.pth, rkmy
BLEU = 73.46, 87.0/77.6/69.1/62.4 (BP=1.000, ratio=1.035, hyp_len=24324, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.74.0.36-1.43.0.35-1.42.0.71-2.03.0.68-1.97.pth, myrk
BLEU = 73.32, 86.9/77.3/69.2/62.2 (BP=1.000, ratio=1.029, hyp_len=23837, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.74.0.36-1.43.0.35-1.42.0.71-2.03.0.68-1.97.pth, rkmy
BLEU = 72.48, 86.4/76.7/68.0/61.3 (BP=1.000, ratio=1.040, hyp_len=24449, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.75.0.35-1.42.0.37-1.44.0.71-2.04.0.69-1.99.pth, myrk
BLEU = 74.15, 87.3/77.9/70.1/63.4 (BP=1.000, ratio=1.025, hyp_len=23729, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.75.0.35-1.42.0.37-1.44.0.71-2.04.0.69-1.99.pth, rkmy
BLEU = 72.19, 86.2/76.4/67.7/60.9 (BP=1.000, ratio=1.042, hyp_len=24488, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.76.0.34-1.40.0.39-1.47.0.72-2.06.0.68-1.97.pth, myrk
BLEU = 74.32, 87.6/78.1/70.3/63.5 (BP=1.000, ratio=1.025, hyp_len=23730, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.76.0.34-1.40.0.39-1.47.0.72-2.06.0.68-1.97.pth, rkmy
BLEU = 72.02, 86.3/76.4/67.4/60.6 (BP=1.000, ratio=1.041, hyp_len=24464, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.77.0.34-1.40.0.41-1.51.0.71-2.04.0.70-2.02.pth, myrk
BLEU = 73.63, 87.0/77.4/69.5/62.7 (BP=1.000, ratio=1.030, hyp_len=23864, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.77.0.34-1.40.0.41-1.51.0.71-2.04.0.70-2.02.pth, rkmy
BLEU = 73.80, 87.5/78.0/69.4/62.6 (BP=1.000, ratio=1.021, hyp_len=24003, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.78.0.38-1.46.0.52-1.68.0.73-2.08.0.77-2.16.pth, myrk
BLEU = 73.02, 86.7/76.9/68.8/61.9 (BP=1.000, ratio=1.032, hyp_len=23897, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.78.0.38-1.46.0.52-1.68.0.73-2.08.0.77-2.16.pth, rkmy
BLEU = 69.75, 85.4/74.6/64.9/57.2 (BP=1.000, ratio=1.021, hyp_len=24011, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.79.0.32-1.38.0.37-1.45.0.71-2.03.0.68-1.98.pth, myrk
BLEU = 74.05, 87.3/77.8/70.0/63.2 (BP=1.000, ratio=1.026, hyp_len=23762, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.79.0.32-1.38.0.37-1.45.0.71-2.03.0.68-1.98.pth, rkmy
BLEU = 71.76, 86.0/76.2/67.3/60.2 (BP=1.000, ratio=1.043, hyp_len=24524, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.80.0.32-1.38.0.38-1.46.0.72-2.05.0.66-1.94.pth, myrk
BLEU = 73.99, 87.3/77.8/69.9/63.1 (BP=1.000, ratio=1.026, hyp_len=23769, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.80.0.32-1.38.0.38-1.46.0.72-2.05.0.66-1.94.pth, rkmy
BLEU = 72.41, 86.3/76.8/67.9/61.1 (BP=1.000, ratio=1.041, hyp_len=24484, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.81.0.31-1.36.0.33-1.39.0.72-2.06.0.65-1.91.pth, myrk
BLEU = 74.52, 87.5/78.2/70.5/64.0 (BP=1.000, ratio=1.024, hyp_len=23725, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.81.0.31-1.36.0.33-1.39.0.72-2.06.0.65-1.91.pth, rkmy
BLEU = 73.05, 86.7/77.3/68.7/61.9 (BP=1.000, ratio=1.041, hyp_len=24475, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.82.0.30-1.36.0.31-1.37.0.72-2.04.0.65-1.92.pth, myrk
BLEU = 74.75, 87.8/78.5/70.7/64.1 (BP=1.000, ratio=1.024, hyp_len=23715, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.82.0.30-1.36.0.31-1.37.0.72-2.04.0.65-1.92.pth, rkmy
BLEU = 73.38, 86.9/77.5/69.0/62.4 (BP=1.000, ratio=1.040, hyp_len=24445, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.83.0.30-1.35.0.31-1.36.0.71-2.03.0.65-1.92.pth, myrk
BLEU = 73.82, 87.1/77.6/69.7/63.0 (BP=1.000, ratio=1.030, hyp_len=23853, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.83.0.30-1.35.0.31-1.36.0.71-2.03.0.65-1.92.pth, rkmy
BLEU = 73.81, 87.1/77.8/69.5/63.0 (BP=1.000, ratio=1.039, hyp_len=24423, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.84.0.30-1.35.0.30-1.35.0.71-2.04.0.65-1.92.pth, myrk
BLEU = 74.01, 87.2/77.7/70.0/63.3 (BP=1.000, ratio=1.027, hyp_len=23791, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.84.0.30-1.35.0.30-1.35.0.71-2.04.0.65-1.92.pth, rkmy
BLEU = 73.31, 86.9/77.5/68.9/62.2 (BP=1.000, ratio=1.041, hyp_len=24468, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.85.0.31-1.37.0.30-1.35.0.73-2.08.0.66-1.93.pth, myrk
BLEU = 73.95, 87.4/77.9/69.8/62.9 (BP=1.000, ratio=1.026, hyp_len=23773, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.85.0.31-1.37.0.30-1.35.0.73-2.08.0.66-1.93.pth, rkmy
BLEU = 74.19, 87.3/78.2/69.9/63.5 (BP=1.000, ratio=1.037, hyp_len=24372, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.86.0.33-1.39.0.30-1.34.0.78-2.17.0.66-1.93.pth, myrk
BLEU = 70.66, 85.7/75.1/66.1/58.6 (BP=1.000, ratio=1.035, hyp_len=23973, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.86.0.33-1.39.0.30-1.34.0.78-2.17.0.66-1.93.pth, rkmy
BLEU = 73.95, 87.2/77.9/69.6/63.2 (BP=1.000, ratio=1.036, hyp_len=24356, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.87.0.41-1.50.0.29-1.34.0.74-2.10.0.65-1.91.pth, myrk
BLEU = 73.65, 87.5/77.6/69.4/62.4 (BP=1.000, ratio=1.017, hyp_len=23565, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.87.0.41-1.50.0.29-1.34.0.74-2.10.0.65-1.91.pth, rkmy
BLEU = 74.06, 87.2/78.0/69.8/63.4 (BP=1.000, ratio=1.038, hyp_len=24398, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.88.0.33-1.40.0.27-1.31.0.71-2.02.0.65-1.91.pth, myrk
BLEU = 73.75, 87.1/77.6/69.6/62.8 (BP=1.000, ratio=1.029, hyp_len=23836, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.88.0.33-1.40.0.27-1.31.0.71-2.02.0.65-1.91.pth, rkmy
BLEU = 74.30, 87.5/78.3/70.0/63.6 (BP=1.000, ratio=1.036, hyp_len=24347, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.89.0.31-1.37.0.28-1.32.0.70-2.01.0.64-1.90.pth, myrk
BLEU = 73.75, 87.0/77.6/69.7/62.9 (BP=1.000, ratio=1.028, hyp_len=23810, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.89.0.31-1.37.0.28-1.32.0.70-2.01.0.64-1.90.pth, rkmy
BLEU = 72.66, 86.4/76.9/68.2/61.5 (BP=1.000, ratio=1.047, hyp_len=24614, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.90.0.43-1.53.0.29-1.33.0.79-2.20.0.65-1.92.pth, myrk
BLEU = 69.39, 84.8/74.1/64.9/56.9 (BP=1.000, ratio=1.050, hyp_len=24316, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.90.0.43-1.53.0.29-1.33.0.79-2.20.0.65-1.92.pth, rkmy
BLEU = 73.08, 86.7/77.3/68.6/62.0 (BP=1.000, ratio=1.043, hyp_len=24512, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.91.0.33-1.39.0.27-1.31.0.71-2.03.0.65-1.91.pth, myrk
BLEU = 73.88, 87.1/77.6/69.8/63.2 (BP=1.000, ratio=1.024, hyp_len=23725, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.91.0.33-1.39.0.27-1.31.0.71-2.03.0.65-1.91.pth, rkmy
BLEU = 73.29, 86.9/77.5/68.9/62.2 (BP=1.000, ratio=1.041, hyp_len=24463, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.92.0.30-1.35.0.27-1.31.0.70-2.02.0.65-1.91.pth, myrk
BLEU = 73.58, 87.0/77.4/69.4/62.7 (BP=1.000, ratio=1.031, hyp_len=23873, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.92.0.30-1.35.0.27-1.31.0.70-2.02.0.65-1.91.pth, rkmy
BLEU = 73.98, 87.2/78.0/69.7/63.2 (BP=1.000, ratio=1.037, hyp_len=24388, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.93.0.28-1.32.0.27-1.30.0.70-2.01.0.66-1.94.pth, myrk
BLEU = 74.44, 87.4/78.1/70.4/63.9 (BP=1.000, ratio=1.029, hyp_len=23842, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.93.0.28-1.32.0.27-1.30.0.70-2.01.0.66-1.94.pth, rkmy
BLEU = 74.01, 87.2/78.0/69.7/63.3 (BP=1.000, ratio=1.038, hyp_len=24408, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.94.0.26-1.30.0.26-1.29.0.70-2.02.0.65-1.92.pth, myrk
BLEU = 74.55, 87.5/78.2/70.5/64.0 (BP=1.000, ratio=1.028, hyp_len=23818, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.94.0.26-1.30.0.26-1.29.0.70-2.02.0.65-1.92.pth, rkmy
BLEU = 73.90, 87.2/78.0/69.6/63.0 (BP=1.000, ratio=1.037, hyp_len=24389, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.95.0.27-1.31.0.28-1.32.0.69-2.00.0.66-1.93.pth, myrk
BLEU = 74.17, 87.4/77.9/70.1/63.4 (BP=1.000, ratio=1.029, hyp_len=23833, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.95.0.27-1.31.0.28-1.32.0.69-2.00.0.66-1.93.pth, rkmy
BLEU = 72.43, 86.3/76.7/68.0/61.2 (BP=1.000, ratio=1.049, hyp_len=24656, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.96.0.27-1.32.0.31-1.37.0.70-2.02.0.67-1.95.pth, myrk
BLEU = 74.05, 87.1/77.8/70.0/63.4 (BP=1.000, ratio=1.031, hyp_len=23875, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.96.0.27-1.32.0.31-1.37.0.70-2.02.0.67-1.95.pth, rkmy
BLEU = 73.74, 87.0/77.8/69.5/62.9 (BP=1.000, ratio=1.035, hyp_len=24333, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.97.0.28-1.32.0.29-1.34.0.70-2.01.0.66-1.94.pth, myrk
BLEU = 74.00, 87.2/77.8/69.9/63.3 (BP=1.000, ratio=1.030, hyp_len=23850, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.97.0.28-1.32.0.29-1.34.0.70-2.01.0.66-1.94.pth, rkmy
BLEU = 74.56, 87.5/78.5/70.4/63.9 (BP=1.000, ratio=1.035, hyp_len=24337, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.98.0.26-1.30.0.27-1.31.0.70-2.02.0.65-1.92.pth, myrk
BLEU = 74.57, 87.5/78.2/70.5/64.0 (BP=1.000, ratio=1.030, hyp_len=23857, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.98.0.26-1.30.0.27-1.31.0.70-2.02.0.65-1.92.pth, rkmy
BLEU = 73.07, 86.8/77.3/68.7/61.8 (BP=1.000, ratio=1.035, hyp_len=24328, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.99.0.26-1.30.0.30-1.35.0.71-2.03.0.66-1.94.pth, myrk
BLEU = 74.40, 87.4/78.1/70.4/63.8 (BP=1.000, ratio=1.031, hyp_len=23868, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.99.0.26-1.30.0.30-1.35.0.71-2.03.0.66-1.94.pth, rkmy
BLEU = 73.48, 86.9/77.7/69.2/62.4 (BP=1.000, ratio=1.034, hyp_len=24313, ref_len=23509)
```

seq2seq-DSL ကို training အကုန်လုပ်တာ (i.e. 30 epoch, 40 epoch, ... , 100 epoch) ကြာခဲ့တဲ့ အချိန်က အောက်ပါအတိုင်း...  

```
real	305m9.036s
user	297m36.164s
sys	17m3.436s
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

testing/evaluation  

```
Evaluation result for the model: dsl-model-myrk.01.3.57-35.34.3.52-33.75.2.98-19.75.2.85-17.24.pth, myrk
BLEU = 8.04, 47.1/19.3/6.2/1.8 (BP=0.799, ratio=0.817, hyp_len=18917, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.01.3.57-35.34.3.52-33.75.2.98-19.75.2.85-17.24.pth, rkmy
BLEU = 4.45, 20.7/8.3/2.7/0.8 (BP=1.000, ratio=1.871, hyp_len=43994, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.02.2.50-12.18.2.39-10.89.2.09-8.07.1.95-7.02.pth, myrk
BLEU = 23.93, 58.5/33.9/19.0/10.4 (BP=0.956, ratio=0.957, hyp_len=22161, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.02.2.50-12.18.2.39-10.89.2.09-8.07.1.95-7.02.pth, rkmy
BLEU = 21.78, 50.9/29.8/16.4/9.0 (BP=1.000, ratio=1.120, hyp_len=26320, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.03.1.84-6.31.1.75-5.78.1.49-4.42.1.40-4.08.pth, myrk
BLEU = 38.93, 67.2/47.3/32.6/22.2 (BP=1.000, ratio=1.062, hyp_len=24602, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.03.1.84-6.31.1.75-5.78.1.49-4.42.1.40-4.08.pth, rkmy
BLEU = 41.52, 68.7/49.3/34.9/25.1 (BP=1.000, ratio=1.013, hyp_len=23820, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.04.1.34-3.82.1.31-3.70.1.15-3.16.1.12-3.05.pth, myrk
BLEU = 50.59, 75.2/58.1/44.4/33.8 (BP=1.000, ratio=1.045, hyp_len=24202, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.04.1.34-3.82.1.31-3.70.1.15-3.16.1.12-3.05.pth, rkmy
BLEU = 50.39, 75.1/58.1/44.0/33.6 (BP=1.000, ratio=1.028, hyp_len=24178, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.05.1.12-3.07.1.14-3.12.0.99-2.69.0.96-2.61.pth, myrk
BLEU = 57.80, 80.5/64.6/51.7/41.4 (BP=1.000, ratio=1.013, hyp_len=23469, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.05.1.12-3.07.1.14-3.12.0.99-2.69.0.96-2.61.pth, rkmy
BLEU = 57.11, 79.5/64.1/50.9/40.9 (BP=1.000, ratio=1.013, hyp_len=23808, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.06.0.95-2.58.0.94-2.56.0.87-2.40.0.87-2.38.pth, myrk
BLEU = 59.90, 81.4/66.7/54.2/43.8 (BP=1.000, ratio=1.027, hyp_len=23777, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.06.0.95-2.58.0.94-2.56.0.87-2.40.0.87-2.38.pth, rkmy
BLEU = 53.29, 73.2/59.8/47.8/38.5 (BP=1.000, ratio=1.136, hyp_len=26715, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.07.0.83-2.29.0.83-2.28.0.82-2.26.0.81-2.26.pth, myrk
BLEU = 61.33, 81.7/67.7/55.8/45.8 (BP=1.000, ratio=1.045, hyp_len=24209, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.07.0.83-2.29.0.83-2.28.0.82-2.26.0.81-2.26.pth, rkmy
BLEU = 62.56, 82.6/68.6/56.8/47.5 (BP=1.000, ratio=1.005, hyp_len=23631, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.08.0.76-2.14.0.76-2.15.0.75-2.11.0.78-2.19.pth, myrk
BLEU = 62.72, 81.8/68.4/57.4/48.2 (BP=1.000, ratio=1.052, hyp_len=24371, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.08.0.76-2.14.0.76-2.15.0.75-2.11.0.78-2.19.pth, rkmy
BLEU = 56.28, 76.2/63.5/51.0/40.6 (BP=1.000, ratio=1.124, hyp_len=26418, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.09.0.68-1.96.0.67-1.95.0.72-2.06.0.69-1.99.pth, myrk
BLEU = 63.67, 83.1/70.0/58.4/48.3 (BP=1.000, ratio=1.047, hyp_len=24249, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.09.0.68-1.96.0.67-1.95.0.72-2.06.0.69-1.99.pth, rkmy
BLEU = 63.57, 82.5/69.8/58.2/48.8 (BP=1.000, ratio=1.047, hyp_len=24616, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.10.0.62-1.85.0.62-1.87.0.72-2.05.0.67-1.96.pth, myrk
BLEU = 61.12, 79.0/66.6/56.1/47.2 (BP=1.000, ratio=1.094, hyp_len=25336, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.10.0.62-1.85.0.62-1.87.0.72-2.05.0.67-1.96.pth, rkmy
BLEU = 57.60, 75.5/63.3/52.5/43.8 (BP=1.000, ratio=1.149, hyp_len=27015, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.11.0.58-1.78.0.56-1.76.0.70-2.01.0.64-1.90.pth, myrk
BLEU = 65.39, 84.0/71.1/60.2/50.9 (BP=1.000, ratio=1.035, hyp_len=23960, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.11.0.58-1.78.0.56-1.76.0.70-2.01.0.64-1.90.pth, rkmy
BLEU = 66.44, 83.7/72.0/61.4/52.6 (BP=1.000, ratio=1.043, hyp_len=24514, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.12.0.53-1.69.0.53-1.70.0.68-1.97.0.62-1.86.pth, myrk
BLEU = 67.22, 84.9/72.6/62.1/53.3 (BP=1.000, ratio=1.031, hyp_len=23874, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.12.0.53-1.69.0.53-1.70.0.68-1.97.0.62-1.86.pth, rkmy
BLEU = 66.05, 83.8/71.9/60.9/51.9 (BP=1.000, ratio=1.042, hyp_len=24496, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.13.0.47-1.59.0.46-1.58.0.71-2.02.0.61-1.84.pth, myrk
BLEU = 66.50, 84.4/72.4/61.5/52.1 (BP=1.000, ratio=1.043, hyp_len=24162, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.13.0.47-1.59.0.46-1.58.0.71-2.02.0.61-1.84.pth, rkmy
BLEU = 61.56, 78.5/67.0/56.7/48.2 (BP=1.000, ratio=1.121, hyp_len=26354, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.14.0.47-1.60.0.46-1.59.0.67-1.95.0.60-1.82.pth, myrk
BLEU = 66.95, 84.4/72.4/62.0/53.1 (BP=1.000, ratio=1.046, hyp_len=24226, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.14.0.47-1.60.0.46-1.59.0.67-1.95.0.60-1.82.pth, rkmy
BLEU = 67.94, 84.6/73.2/62.9/54.6 (BP=1.000, ratio=1.043, hyp_len=24512, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.15.0.46-1.58.0.44-1.56.0.66-1.94.0.59-1.80.pth, myrk
BLEU = 65.16, 82.3/70.6/60.3/51.4 (BP=1.000, ratio=1.072, hyp_len=24828, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.15.0.46-1.58.0.44-1.56.0.66-1.94.0.59-1.80.pth, rkmy
BLEU = 67.42, 83.5/72.5/62.6/54.5 (BP=1.000, ratio=1.060, hyp_len=24927, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.16.0.42-1.53.0.43-1.53.0.65-1.92.0.60-1.83.pth, myrk
BLEU = 68.93, 85.9/74.1/64.0/55.4 (BP=1.000, ratio=1.028, hyp_len=23811, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.16.0.42-1.53.0.43-1.53.0.65-1.92.0.60-1.83.pth, rkmy
BLEU = 66.60, 83.8/72.4/61.6/52.6 (BP=1.000, ratio=1.057, hyp_len=24841, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.17.0.40-1.49.0.40-1.49.0.64-1.90.0.59-1.80.pth, myrk
BLEU = 67.62, 84.8/72.8/62.7/54.0 (BP=1.000, ratio=1.036, hyp_len=23990, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.17.0.40-1.49.0.40-1.49.0.64-1.90.0.59-1.80.pth, rkmy
BLEU = 62.58, 79.8/68.4/57.7/48.7 (BP=1.000, ratio=1.109, hyp_len=26069, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.18.0.40-1.49.0.39-1.48.0.66-1.93.0.59-1.81.pth, myrk
BLEU = 68.29, 85.2/73.5/63.4/54.7 (BP=1.000, ratio=1.041, hyp_len=24107, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.18.0.40-1.49.0.39-1.48.0.66-1.93.0.59-1.81.pth, rkmy
BLEU = 67.38, 83.8/72.7/62.5/54.2 (BP=1.000, ratio=1.057, hyp_len=24854, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.19.0.34-1.41.0.34-1.40.0.66-1.93.0.58-1.79.pth, myrk
BLEU = 70.35, 86.5/75.3/65.7/57.3 (BP=1.000, ratio=1.031, hyp_len=23876, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.19.0.34-1.41.0.34-1.40.0.66-1.93.0.58-1.79.pth, rkmy
BLEU = 68.49, 84.6/73.8/63.7/55.4 (BP=1.000, ratio=1.054, hyp_len=24788, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.20.0.35-1.42.0.35-1.41.0.64-1.91.0.56-1.75.pth, myrk
BLEU = 67.16, 84.6/72.5/62.2/53.4 (BP=1.000, ratio=1.048, hyp_len=24269, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.20.0.35-1.42.0.35-1.41.0.64-1.91.0.56-1.75.pth, rkmy
BLEU = 68.21, 84.6/73.4/63.2/55.2 (BP=1.000, ratio=1.049, hyp_len=24655, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.21.0.35-1.42.0.35-1.42.0.64-1.89.0.59-1.81.pth, myrk
BLEU = 69.24, 85.6/74.2/64.5/56.2 (BP=1.000, ratio=1.041, hyp_len=24104, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.21.0.35-1.42.0.35-1.42.0.64-1.89.0.59-1.81.pth, rkmy
BLEU = 67.22, 84.0/72.7/62.2/53.7 (BP=1.000, ratio=1.062, hyp_len=24977, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.22.0.35-1.41.0.33-1.40.0.64-1.90.0.60-1.82.pth, myrk
BLEU = 70.11, 86.3/74.9/65.3/57.2 (BP=1.000, ratio=1.030, hyp_len=23847, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.22.0.35-1.41.0.33-1.40.0.64-1.90.0.60-1.82.pth, rkmy
BLEU = 68.87, 85.4/74.3/63.9/55.5 (BP=1.000, ratio=1.048, hyp_len=24639, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.23.0.33-1.39.0.32-1.38.0.65-1.91.0.58-1.79.pth, myrk
BLEU = 67.80, 84.6/72.9/63.0/54.5 (BP=1.000, ratio=1.054, hyp_len=24406, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.23.0.33-1.39.0.32-1.38.0.65-1.91.0.58-1.79.pth, rkmy
BLEU = 67.30, 83.9/72.8/62.4/53.8 (BP=1.000, ratio=1.062, hyp_len=24974, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.24.0.31-1.36.0.32-1.38.0.63-1.88.0.58-1.79.pth, myrk
BLEU = 68.81, 85.1/73.7/64.1/55.8 (BP=1.000, ratio=1.044, hyp_len=24184, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.24.0.31-1.36.0.32-1.38.0.63-1.88.0.58-1.79.pth, rkmy
BLEU = 66.71, 83.4/72.0/61.7/53.5 (BP=1.000, ratio=1.070, hyp_len=25153, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.25.0.30-1.35.0.31-1.37.0.66-1.93.0.59-1.80.pth, myrk
BLEU = 68.99, 85.4/74.0/64.2/55.8 (BP=1.000, ratio=1.043, hyp_len=24155, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.25.0.30-1.35.0.31-1.37.0.66-1.93.0.59-1.80.pth, rkmy
BLEU = 69.26, 85.0/74.3/64.5/56.4 (BP=1.000, ratio=1.050, hyp_len=24680, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.26.0.29-1.34.0.28-1.32.0.67-1.95.0.65-1.92.pth, myrk
BLEU = 62.43, 78.5/67.3/57.8/49.8 (BP=1.000, ratio=1.137, hyp_len=26328, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.26.0.29-1.34.0.28-1.32.0.67-1.95.0.65-1.92.pth, rkmy
BLEU = 64.68, 81.7/70.8/60.0/50.4 (BP=1.000, ratio=1.096, hyp_len=25760, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.27.0.30-1.35.0.30-1.35.0.65-1.91.0.58-1.79.pth, myrk
BLEU = 69.09, 85.2/74.0/64.4/56.1 (BP=1.000, ratio=1.046, hyp_len=24220, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.27.0.30-1.35.0.30-1.35.0.65-1.91.0.58-1.79.pth, rkmy
BLEU = 67.68, 84.0/72.9/62.8/54.5 (BP=1.000, ratio=1.066, hyp_len=25071, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.28.0.28-1.33.0.30-1.35.0.66-1.93.0.59-1.80.pth, myrk
BLEU = 68.44, 85.3/73.5/63.6/55.0 (BP=1.000, ratio=1.048, hyp_len=24281, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.28.0.28-1.33.0.30-1.35.0.66-1.93.0.59-1.80.pth, rkmy
BLEU = 68.65, 84.7/73.7/63.7/55.9 (BP=1.000, ratio=1.057, hyp_len=24854, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.29.0.27-1.31.0.27-1.31.0.65-1.92.0.58-1.78.pth, myrk
BLEU = 68.53, 85.2/73.6/63.7/55.3 (BP=1.000, ratio=1.047, hyp_len=24244, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.29.0.27-1.31.0.27-1.31.0.65-1.92.0.58-1.78.pth, rkmy
BLEU = 68.96, 85.1/74.0/64.1/56.0 (BP=1.000, ratio=1.047, hyp_len=24606, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.30.0.28-1.33.0.28-1.32.0.65-1.91.0.59-1.81.pth, myrk
BLEU = 67.81, 84.0/72.7/63.1/54.8 (BP=1.000, ratio=1.055, hyp_len=24427, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.30.0.28-1.33.0.28-1.32.0.65-1.91.0.59-1.81.pth, rkmy
BLEU = 66.55, 82.9/71.7/61.7/53.5 (BP=1.000, ratio=1.080, hyp_len=25387, ref_len=23509)
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

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/transformer/myrk-40epoch
Evaluation result for the model: dsl-model-myrk.01.3.59-36.30.3.55-34.96.2.93-18.66.2.91-18.43.pth, myrk
BLEU = 9.50, 43.6/18.6/6.8/2.2 (BP=0.903, ratio=0.908, hyp_len=21022, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.01.3.59-36.30.3.55-34.96.2.93-18.66.2.91-18.43.pth, rkmy
BLEU = 5.07, 25.3/10.0/3.0/0.9 (BP=1.000, ratio=1.496, hyp_len=35163, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.02.2.38-10.81.2.40-11.02.2.00-7.39.2.00-7.36.pth, myrk
BLEU = 26.95, 59.6/35.9/21.0/11.9 (BP=0.996, ratio=0.997, hyp_len=23079, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.02.2.38-10.81.2.40-11.02.2.00-7.39.2.00-7.36.pth, rkmy
BLEU = 24.34, 56.9/33.5/18.7/10.3 (BP=0.989, ratio=0.989, hyp_len=23256, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.03.1.71-5.54.1.74-5.70.1.42-4.15.1.47-4.35.pth, myrk
BLEU = 42.70, 71.4/51.1/36.1/25.3 (BP=1.000, ratio=1.013, hyp_len=23472, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.03.1.71-5.54.1.74-5.70.1.42-4.15.1.47-4.35.pth, rkmy
BLEU = 39.74, 68.5/48.6/33.2/22.6 (BP=1.000, ratio=1.019, hyp_len=23960, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.04.1.36-3.91.1.39-4.02.1.09-2.98.1.12-3.08.pth, myrk
BLEU = 51.46, 75.6/58.6/45.3/34.9 (BP=1.000, ratio=1.047, hyp_len=24237, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.04.1.36-3.91.1.39-4.02.1.09-2.98.1.12-3.08.pth, rkmy
BLEU = 44.56, 68.5/52.1/38.6/28.6 (BP=1.000, ratio=1.126, hyp_len=26481, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.05.1.06-2.89.1.09-2.96.0.94-2.57.0.94-2.55.pth, myrk
BLEU = 59.44, 82.4/67.0/54.2/44.1 (BP=0.986, ratio=0.986, hyp_len=22844, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.05.1.06-2.89.1.09-2.96.0.94-2.57.0.94-2.55.pth, rkmy
BLEU = 53.48, 76.3/60.9/47.5/37.1 (BP=1.000, ratio=1.047, hyp_len=24622, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.06.0.93-2.53.0.96-2.62.0.84-2.31.0.85-2.34.pth, myrk
BLEU = 60.57, 82.0/67.2/54.8/44.6 (BP=1.000, ratio=1.022, hyp_len=23670, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.06.0.93-2.53.0.96-2.62.0.84-2.31.0.85-2.34.pth, rkmy
BLEU = 58.93, 80.4/65.9/53.0/43.0 (BP=1.000, ratio=1.027, hyp_len=24151, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.07.0.83-2.29.0.86-2.36.0.78-2.18.0.77-2.15.pth, myrk
BLEU = 62.88, 83.0/69.4/57.5/47.2 (BP=1.000, ratio=1.034, hyp_len=23936, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.07.0.83-2.29.0.86-2.36.0.78-2.18.0.77-2.15.pth, rkmy
BLEU = 60.19, 80.7/66.8/54.5/44.7 (BP=1.000, ratio=1.046, hyp_len=24597, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.08.0.68-1.98.0.71-2.03.0.76-2.13.0.70-2.01.pth, myrk
BLEU = 58.55, 77.2/64.6/53.4/44.1 (BP=1.000, ratio=1.121, hyp_len=25969, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.08.0.68-1.98.0.71-2.03.0.76-2.13.0.70-2.01.pth, rkmy
BLEU = 61.29, 80.5/67.4/55.8/46.6 (BP=1.000, ratio=1.059, hyp_len=24901, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.09.0.65-1.92.0.70-2.01.0.73-2.08.0.70-2.01.pth, myrk
BLEU = 57.68, 76.8/64.3/52.7/42.5 (BP=1.000, ratio=1.139, hyp_len=26384, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.09.0.65-1.92.0.70-2.01.0.73-2.08.0.70-2.01.pth, rkmy
BLEU = 62.84, 82.6/69.3/57.2/47.6 (BP=1.000, ratio=1.031, hyp_len=24235, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.10.0.57-1.76.0.58-1.78.0.69-2.00.0.66-1.93.pth, myrk
BLEU = 65.48, 84.2/71.4/60.2/50.8 (BP=1.000, ratio=1.037, hyp_len=24017, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.10.0.57-1.76.0.58-1.78.0.69-2.00.0.66-1.93.pth, rkmy
BLEU = 65.96, 84.1/71.6/60.6/51.8 (BP=1.000, ratio=1.027, hyp_len=24151, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.11.0.56-1.74.0.58-1.79.0.68-1.98.0.65-1.92.pth, myrk
BLEU = 66.93, 84.7/72.4/61.9/52.9 (BP=1.000, ratio=1.028, hyp_len=23809, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.11.0.56-1.74.0.58-1.79.0.68-1.98.0.65-1.92.pth, rkmy
BLEU = 64.71, 83.0/70.5/59.4/50.5 (BP=1.000, ratio=1.043, hyp_len=24529, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.12.0.50-1.65.0.53-1.70.0.65-1.91.0.63-1.87.pth, myrk
BLEU = 64.12, 81.6/69.6/59.2/50.3 (BP=1.000, ratio=1.079, hyp_len=24984, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.12.0.50-1.65.0.53-1.70.0.65-1.91.0.63-1.87.pth, rkmy
BLEU = 67.12, 84.8/72.7/61.9/53.2 (BP=1.000, ratio=1.029, hyp_len=24181, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.13.0.49-1.63.0.50-1.65.0.66-1.94.0.60-1.82.pth, myrk
BLEU = 66.30, 84.2/72.0/61.3/52.0 (BP=1.000, ratio=1.049, hyp_len=24284, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.13.0.49-1.63.0.50-1.65.0.66-1.94.0.60-1.82.pth, rkmy
BLEU = 66.57, 83.6/71.9/61.6/53.1 (BP=1.000, ratio=1.054, hyp_len=24790, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.14.0.48-1.61.0.50-1.65.0.64-1.89.0.62-1.87.pth, myrk
BLEU = 67.48, 84.7/72.9/62.5/53.8 (BP=1.000, ratio=1.037, hyp_len=24025, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.14.0.48-1.61.0.50-1.65.0.64-1.89.0.62-1.87.pth, rkmy
BLEU = 66.72, 84.2/72.6/61.7/52.6 (BP=1.000, ratio=1.041, hyp_len=24476, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.15.0.41-1.50.0.42-1.52.0.66-1.94.0.59-1.80.pth, myrk
BLEU = 67.49, 84.5/72.5/62.6/54.1 (BP=1.000, ratio=1.039, hyp_len=24073, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.15.0.41-1.50.0.42-1.52.0.66-1.94.0.59-1.80.pth, rkmy
BLEU = 67.80, 84.8/73.3/62.8/54.1 (BP=1.000, ratio=1.031, hyp_len=24243, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.16.0.43-1.53.0.43-1.53.0.64-1.90.0.59-1.80.pth, myrk
BLEU = 67.31, 83.3/72.3/62.7/54.4 (BP=1.000, ratio=1.069, hyp_len=24755, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.16.0.43-1.53.0.43-1.53.0.64-1.90.0.59-1.80.pth, rkmy
BLEU = 68.00, 84.6/73.3/63.0/54.8 (BP=1.000, ratio=1.044, hyp_len=24536, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.17.0.40-1.49.0.39-1.48.0.64-1.90.0.59-1.81.pth, myrk
BLEU = 65.16, 81.5/70.0/60.4/52.3 (BP=1.000, ratio=1.091, hyp_len=25265, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.17.0.40-1.49.0.39-1.48.0.64-1.90.0.59-1.81.pth, rkmy
BLEU = 68.66, 85.0/73.9/63.8/55.5 (BP=1.000, ratio=1.039, hyp_len=24433, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.18.0.37-1.45.0.39-1.47.0.63-1.87.0.61-1.84.pth, myrk
BLEU = 69.52, 85.9/74.4/64.8/56.4 (BP=1.000, ratio=1.034, hyp_len=23944, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.18.0.37-1.45.0.39-1.47.0.63-1.87.0.61-1.84.pth, rkmy
BLEU = 67.44, 84.3/73.0/62.5/53.7 (BP=1.000, ratio=1.054, hyp_len=24789, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.19.0.35-1.43.0.35-1.43.0.63-1.89.0.59-1.80.pth, myrk
BLEU = 69.81, 86.0/74.6/65.0/56.9 (BP=1.000, ratio=1.034, hyp_len=23943, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.19.0.35-1.43.0.35-1.43.0.63-1.89.0.59-1.80.pth, rkmy
BLEU = 68.44, 84.8/74.0/63.7/54.9 (BP=1.000, ratio=1.050, hyp_len=24684, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.20.0.34-1.40.0.34-1.40.0.65-1.91.0.59-1.81.pth, myrk
BLEU = 70.44, 86.2/75.3/65.8/57.7 (BP=1.000, ratio=1.029, hyp_len=23830, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.20.0.34-1.40.0.34-1.40.0.65-1.91.0.59-1.81.pth, rkmy
BLEU = 67.43, 83.7/72.5/62.5/54.5 (BP=1.000, ratio=1.060, hyp_len=24917, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.21.0.35-1.42.0.36-1.43.0.63-1.87.0.59-1.81.pth, myrk
BLEU = 65.81, 82.7/71.3/61.2/52.1 (BP=1.000, ratio=1.073, hyp_len=24862, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.21.0.35-1.42.0.36-1.43.0.63-1.87.0.59-1.81.pth, rkmy
BLEU = 67.50, 84.3/72.7/62.4/54.3 (BP=1.000, ratio=1.049, hyp_len=24655, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.22.0.32-1.37.0.33-1.39.0.62-1.87.0.58-1.79.pth, myrk
BLEU = 69.22, 85.3/74.0/64.4/56.4 (BP=1.000, ratio=1.044, hyp_len=24183, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.22.0.32-1.37.0.33-1.39.0.62-1.87.0.58-1.79.pth, rkmy
BLEU = 69.24, 85.4/74.3/64.4/56.2 (BP=1.000, ratio=1.042, hyp_len=24490, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.23.0.31-1.37.0.32-1.38.0.62-1.87.0.57-1.78.pth, myrk
BLEU = 66.68, 82.7/71.6/62.1/53.8 (BP=1.000, ratio=1.077, hyp_len=24953, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.23.0.31-1.37.0.32-1.38.0.62-1.87.0.57-1.78.pth, rkmy
BLEU = 69.48, 85.5/74.6/64.6/56.6 (BP=1.000, ratio=1.040, hyp_len=24458, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.24.0.31-1.36.0.34-1.41.0.63-1.87.0.58-1.79.pth, myrk
BLEU = 69.17, 85.3/74.2/64.5/56.1 (BP=1.000, ratio=1.044, hyp_len=24183, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.24.0.31-1.36.0.34-1.41.0.63-1.87.0.58-1.79.pth, rkmy
BLEU = 68.70, 85.0/73.9/63.8/55.6 (BP=1.000, ratio=1.043, hyp_len=24516, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.25.0.29-1.34.0.29-1.34.0.63-1.88.0.60-1.83.pth, myrk
BLEU = 67.83, 84.0/72.8/63.0/54.9 (BP=1.000, ratio=1.060, hyp_len=24547, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.25.0.29-1.34.0.29-1.34.0.63-1.88.0.60-1.83.pth, rkmy
BLEU = 68.37, 84.7/73.4/63.4/55.4 (BP=1.000, ratio=1.050, hyp_len=24677, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.26.0.29-1.34.0.31-1.36.0.63-1.87.0.58-1.79.pth, myrk
BLEU = 67.37, 84.1/72.5/62.5/54.0 (BP=1.000, ratio=1.059, hyp_len=24537, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.26.0.29-1.34.0.31-1.36.0.63-1.87.0.58-1.79.pth, rkmy
BLEU = 69.47, 85.4/74.5/64.7/56.6 (BP=1.000, ratio=1.041, hyp_len=24468, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.27.0.27-1.31.0.27-1.31.0.62-1.87.0.56-1.76.pth, myrk
BLEU = 69.84, 85.6/74.6/65.2/57.2 (BP=1.000, ratio=1.046, hyp_len=24223, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.27.0.27-1.31.0.27-1.31.0.62-1.87.0.56-1.76.pth, rkmy
BLEU = 68.10, 84.4/73.3/63.2/55.0 (BP=1.000, ratio=1.061, hyp_len=24952, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.28.0.29-1.34.0.30-1.35.0.64-1.89.0.57-1.77.pth, myrk
BLEU = 68.85, 85.1/73.8/64.1/55.8 (BP=1.000, ratio=1.047, hyp_len=24256, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.28.0.29-1.34.0.30-1.35.0.64-1.89.0.57-1.77.pth, rkmy
BLEU = 69.63, 85.2/74.6/64.9/57.0 (BP=1.000, ratio=1.049, hyp_len=24664, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.29.0.27-1.31.0.27-1.31.0.61-1.84.0.57-1.77.pth, myrk
BLEU = 66.66, 83.0/71.6/61.9/53.7 (BP=1.000, ratio=1.075, hyp_len=24895, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.29.0.27-1.31.0.27-1.31.0.61-1.84.0.57-1.77.pth, rkmy
BLEU = 69.70, 85.5/74.6/64.8/57.0 (BP=1.000, ratio=1.042, hyp_len=24500, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.30.0.26-1.30.0.27-1.31.0.63-1.87.0.61-1.84.pth, myrk
BLEU = 70.19, 86.0/74.9/65.5/57.6 (BP=1.000, ratio=1.033, hyp_len=23914, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.30.0.26-1.30.0.27-1.31.0.63-1.87.0.61-1.84.pth, rkmy
BLEU = 69.01, 84.9/73.8/64.2/56.4 (BP=1.000, ratio=1.053, hyp_len=24764, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.31.0.25-1.29.0.24-1.28.0.65-1.91.0.58-1.79.pth, myrk
BLEU = 71.09, 86.8/75.7/66.5/58.5 (BP=1.000, ratio=1.031, hyp_len=23877, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.31.0.25-1.29.0.24-1.28.0.65-1.91.0.58-1.79.pth, rkmy
BLEU = 68.17, 84.3/73.3/63.3/55.2 (BP=1.000, ratio=1.060, hyp_len=24913, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.32.0.25-1.29.0.25-1.28.0.64-1.89.0.63-1.88.pth, myrk
BLEU = 69.19, 85.2/74.0/64.5/56.3 (BP=1.000, ratio=1.044, hyp_len=24180, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.32.0.25-1.29.0.25-1.28.0.64-1.89.0.63-1.88.pth, rkmy
BLEU = 69.64, 85.4/74.7/64.8/56.9 (BP=1.000, ratio=1.045, hyp_len=24570, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.33.0.24-1.27.0.24-1.27.0.63-1.88.0.58-1.79.pth, myrk
BLEU = 68.86, 85.2/73.9/64.1/55.7 (BP=1.000, ratio=1.051, hyp_len=24346, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.33.0.24-1.27.0.24-1.27.0.63-1.88.0.58-1.79.pth, rkmy
BLEU = 70.18, 85.6/75.1/65.4/57.7 (BP=1.000, ratio=1.044, hyp_len=24532, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.34.0.24-1.27.0.24-1.28.0.65-1.91.0.58-1.79.pth, myrk
BLEU = 69.79, 85.6/74.6/65.2/57.0 (BP=1.000, ratio=1.044, hyp_len=24184, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.34.0.24-1.27.0.24-1.28.0.65-1.91.0.58-1.79.pth, rkmy
BLEU = 68.30, 84.5/73.4/63.4/55.4 (BP=1.000, ratio=1.055, hyp_len=24800, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.35.0.23-1.26.0.24-1.27.0.64-1.90.0.58-1.79.pth, myrk
BLEU = 69.60, 85.2/74.3/65.1/57.0 (BP=1.000, ratio=1.047, hyp_len=24260, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.35.0.23-1.26.0.24-1.27.0.64-1.90.0.58-1.79.pth, rkmy
BLEU = 68.07, 84.3/73.3/63.2/55.0 (BP=1.000, ratio=1.060, hyp_len=24915, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.36.0.23-1.26.0.23-1.26.0.64-1.89.0.60-1.82.pth, myrk
BLEU = 68.47, 85.0/73.6/63.8/55.1 (BP=1.000, ratio=1.051, hyp_len=24332, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.36.0.23-1.26.0.23-1.26.0.64-1.89.0.60-1.82.pth, rkmy
BLEU = 69.89, 85.8/74.8/64.9/57.2 (BP=1.000, ratio=1.045, hyp_len=24572, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.37.0.22-1.25.0.23-1.26.0.64-1.90.0.61-1.85.pth, myrk
BLEU = 67.75, 83.9/72.6/63.1/54.9 (BP=1.000, ratio=1.066, hyp_len=24684, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.37.0.22-1.25.0.23-1.26.0.64-1.90.0.61-1.85.pth, rkmy
BLEU = 70.49, 85.8/75.3/65.8/58.0 (BP=1.000, ratio=1.040, hyp_len=24457, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.38.0.21-1.24.0.22-1.25.0.65-1.91.0.59-1.81.pth, myrk
BLEU = 69.97, 86.0/74.8/65.2/57.1 (BP=1.000, ratio=1.038, hyp_len=24049, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.38.0.21-1.24.0.22-1.25.0.65-1.91.0.59-1.81.pth, rkmy
BLEU = 69.53, 85.4/74.6/64.7/56.8 (BP=1.000, ratio=1.052, hyp_len=24722, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.39.0.21-1.23.0.20-1.22.0.65-1.91.0.62-1.86.pth, myrk
BLEU = 69.72, 85.5/74.3/65.1/57.1 (BP=1.000, ratio=1.044, hyp_len=24183, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.39.0.21-1.23.0.20-1.22.0.65-1.91.0.62-1.86.pth, rkmy
BLEU = 69.37, 85.2/74.4/64.5/56.7 (BP=1.000, ratio=1.051, hyp_len=24709, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.40.0.20-1.22.0.21-1.23.0.65-1.92.0.59-1.81.pth, myrk
BLEU = 69.12, 85.2/74.0/64.4/56.2 (BP=1.000, ratio=1.045, hyp_len=24195, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.40.0.20-1.22.0.21-1.23.0.65-1.92.0.59-1.81.pth, rkmy
BLEU = 66.76, 83.4/72.0/61.7/53.6 (BP=1.000, ratio=1.068, hyp_len=25117, ref_len=23509)
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

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/transformer/myrk-50epoch
Evaluation result for the model: dsl-model-myrk.01.3.56-35.11.3.52-33.72.2.94-18.90.2.94-18.99.pth, myrk
BLEU = 8.68, 41.2/17.3/5.8/1.7 (BP=0.944, ratio=0.946, hyp_len=21898, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.01.3.56-35.11.3.52-33.72.2.94-18.90.2.94-18.99.pth, rkmy
BLEU = 6.29, 28.2/11.6/3.9/1.2 (BP=1.000, ratio=1.402, hyp_len=32965, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.02.2.43-11.37.2.42-11.26.1.97-7.20.1.97-7.20.pth, myrk
BLEU = 23.31, 53.0/31.2/17.9/10.0 (BP=1.000, ratio=1.123, hyp_len=26005, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.02.2.43-11.37.2.42-11.26.1.97-7.20.1.97-7.20.pth, rkmy
BLEU = 24.27, 56.1/33.0/18.5/10.2 (BP=1.000, ratio=1.025, hyp_len=24093, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.03.1.73-5.61.1.71-5.56.1.49-4.44.1.47-4.37.pth, myrk
BLEU = 38.09, 66.1/46.3/31.8/21.6 (BP=1.000, ratio=1.074, hyp_len=24871, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.03.1.73-5.61.1.71-5.56.1.49-4.44.1.47-4.37.pth, rkmy
BLEU = 36.20, 63.3/44.1/29.9/20.6 (BP=1.000, ratio=1.092, hyp_len=25674, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.04.1.32-3.75.1.36-3.90.1.19-3.29.1.18-3.26.pth, myrk
BLEU = 50.72, 76.2/58.7/44.5/33.3 (BP=1.000, ratio=1.028, hyp_len=23801, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.04.1.32-3.75.1.36-3.90.1.19-3.29.1.18-3.26.pth, rkmy
BLEU = 48.94, 74.9/57.0/42.4/31.8 (BP=0.999, ratio=0.999, hyp_len=23491, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.05.1.12-3.05.1.16-3.18.1.01-2.75.1.01-2.74.pth, myrk
BLEU = 53.61, 76.2/60.5/47.8/37.4 (BP=1.000, ratio=1.072, hyp_len=24830, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.05.1.12-3.05.1.16-3.18.1.01-2.75.1.01-2.74.pth, rkmy
BLEU = 54.92, 78.5/62.4/48.6/38.2 (BP=1.000, ratio=1.009, hyp_len=23728, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.06.0.94-2.57.0.96-2.62.0.91-2.47.0.92-2.51.pth, myrk
BLEU = 60.66, 82.8/67.7/55.2/44.8 (BP=0.994, ratio=0.994, hyp_len=23015, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.06.0.94-2.57.0.96-2.62.0.91-2.47.0.92-2.51.pth, rkmy
BLEU = 56.76, 79.0/64.2/50.8/40.2 (BP=1.000, ratio=1.041, hyp_len=24478, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.07.0.84-2.31.0.85-2.34.0.83-2.29.0.82-2.27.pth, myrk
BLEU = 61.45, 82.0/68.3/55.9/45.5 (BP=1.000, ratio=1.034, hyp_len=23952, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.07.0.84-2.31.0.85-2.34.0.83-2.29.0.82-2.27.pth, rkmy
BLEU = 59.50, 80.8/66.4/53.6/43.6 (BP=1.000, ratio=1.036, hyp_len=24363, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.08.0.72-2.06.0.76-2.14.0.81-2.25.0.81-2.25.pth, myrk
BLEU = 61.91, 81.4/67.8/56.4/47.1 (BP=1.000, ratio=1.041, hyp_len=24105, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.08.0.72-2.06.0.76-2.14.0.81-2.25.0.81-2.25.pth, rkmy
BLEU = 58.97, 79.8/66.5/53.6/42.5 (BP=1.000, ratio=1.051, hyp_len=24703, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.09.0.67-1.95.0.68-1.97.0.76-2.15.0.73-2.07.pth, myrk
BLEU = 63.87, 82.8/69.8/58.6/49.2 (BP=1.000, ratio=1.040, hyp_len=24077, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.09.0.67-1.95.0.68-1.97.0.76-2.15.0.73-2.07.pth, rkmy
BLEU = 65.71, 84.0/71.5/60.3/51.5 (BP=1.000, ratio=1.009, hyp_len=23731, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.10.0.65-1.92.0.67-1.95.0.76-2.14.0.69-2.00.pth, myrk
BLEU = 63.03, 81.0/68.6/58.0/49.0 (BP=1.000, ratio=1.070, hyp_len=24771, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.10.0.65-1.92.0.67-1.95.0.76-2.14.0.69-2.00.pth, rkmy
BLEU = 61.67, 80.1/67.9/56.5/47.1 (BP=1.000, ratio=1.083, hyp_len=25469, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.11.0.60-1.81.0.60-1.83.0.73-2.07.0.64-1.91.pth, myrk
BLEU = 64.89, 82.9/70.4/59.8/50.8 (BP=1.000, ratio=1.050, hyp_len=24324, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.11.0.60-1.81.0.60-1.83.0.73-2.07.0.64-1.91.pth, rkmy
BLEU = 60.63, 77.9/66.3/55.7/47.1 (BP=1.000, ratio=1.125, hyp_len=26458, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.12.0.54-1.72.0.56-1.75.0.70-2.00.0.64-1.89.pth, myrk
BLEU = 66.23, 83.9/71.5/61.2/52.4 (BP=1.000, ratio=1.047, hyp_len=24249, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.12.0.54-1.72.0.56-1.75.0.70-2.00.0.64-1.89.pth, rkmy
BLEU = 65.47, 83.5/71.4/60.2/51.2 (BP=1.000, ratio=1.044, hyp_len=24549, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.13.0.49-1.63.0.50-1.65.0.69-2.00.0.63-1.87.pth, myrk
BLEU = 68.22, 85.6/73.3/63.2/54.6 (BP=1.000, ratio=1.021, hyp_len=23656, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.13.0.49-1.63.0.50-1.65.0.69-2.00.0.63-1.87.pth, rkmy
BLEU = 61.86, 79.7/67.9/56.8/47.7 (BP=1.000, ratio=1.109, hyp_len=26062, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.14.0.46-1.59.0.48-1.61.0.68-1.97.0.62-1.85.pth, myrk
BLEU = 65.68, 83.9/71.7/60.7/51.0 (BP=1.000, ratio=1.053, hyp_len=24387, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.14.0.46-1.59.0.48-1.61.0.68-1.97.0.62-1.85.pth, rkmy
BLEU = 67.11, 84.3/72.8/62.1/53.2 (BP=1.000, ratio=1.042, hyp_len=24488, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.15.0.46-1.58.0.45-1.57.0.67-1.95.0.62-1.86.pth, myrk
BLEU = 67.86, 85.0/72.9/63.0/54.3 (BP=1.000, ratio=1.036, hyp_len=23995, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.15.0.46-1.58.0.45-1.57.0.67-1.95.0.62-1.86.pth, rkmy
BLEU = 67.27, 84.4/72.8/62.2/53.6 (BP=1.000, ratio=1.042, hyp_len=24503, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.16.0.40-1.50.0.41-1.50.0.67-1.96.0.60-1.82.pth, myrk
BLEU = 68.90, 85.9/74.0/64.0/55.4 (BP=1.000, ratio=1.027, hyp_len=23796, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.16.0.40-1.50.0.41-1.50.0.67-1.96.0.60-1.82.pth, rkmy
BLEU = 65.12, 82.4/70.7/60.0/51.4 (BP=1.000, ratio=1.073, hyp_len=25221, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.17.0.38-1.46.0.39-1.47.0.65-1.92.0.61-1.84.pth, myrk
BLEU = 68.60, 85.4/73.8/63.8/55.1 (BP=1.000, ratio=1.036, hyp_len=24004, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.17.0.38-1.46.0.39-1.47.0.65-1.92.0.61-1.84.pth, rkmy
BLEU = 66.91, 84.2/72.6/61.9/53.0 (BP=1.000, ratio=1.054, hyp_len=24790, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.18.0.37-1.44.0.37-1.45.0.64-1.91.0.61-1.84.pth, myrk
BLEU = 67.29, 84.0/72.4/62.5/54.0 (BP=1.000, ratio=1.057, hyp_len=24470, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.18.0.37-1.44.0.37-1.45.0.64-1.91.0.61-1.84.pth, rkmy
BLEU = 67.99, 84.6/73.3/63.1/54.6 (BP=1.000, ratio=1.048, hyp_len=24645, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.19.0.38-1.46.0.38-1.46.0.67-1.96.0.58-1.79.pth, myrk
BLEU = 69.14, 85.7/74.2/64.3/55.9 (BP=1.000, ratio=1.031, hyp_len=23880, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.19.0.38-1.46.0.38-1.46.0.67-1.96.0.58-1.79.pth, rkmy
BLEU = 67.33, 84.4/73.1/62.3/53.4 (BP=1.000, ratio=1.054, hyp_len=24770, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.20.0.35-1.41.0.36-1.43.0.66-1.94.0.59-1.80.pth, myrk
BLEU = 67.72, 84.4/72.9/62.9/54.4 (BP=1.000, ratio=1.054, hyp_len=24419, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.20.0.35-1.41.0.36-1.43.0.66-1.94.0.59-1.80.pth, rkmy
BLEU = 66.90, 83.4/72.2/62.0/53.7 (BP=1.000, ratio=1.064, hyp_len=25005, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.21.0.37-1.45.0.37-1.45.0.67-1.96.0.62-1.85.pth, myrk
BLEU = 67.39, 84.2/72.5/62.5/54.0 (BP=1.000, ratio=1.051, hyp_len=24352, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.21.0.37-1.45.0.37-1.45.0.67-1.96.0.62-1.85.pth, rkmy
BLEU = 68.04, 84.6/73.4/63.1/54.6 (BP=1.000, ratio=1.050, hyp_len=24686, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.22.0.33-1.40.0.34-1.40.0.65-1.91.0.61-1.83.pth, myrk
BLEU = 69.53, 85.8/74.5/64.8/56.4 (BP=1.000, ratio=1.036, hyp_len=23990, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.22.0.33-1.40.0.34-1.40.0.65-1.91.0.61-1.83.pth, rkmy
BLEU = 67.47, 83.8/72.8/62.6/54.3 (BP=1.000, ratio=1.067, hyp_len=25077, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.23.0.32-1.37.0.33-1.39.0.66-1.93.0.62-1.86.pth, myrk
BLEU = 69.39, 85.9/74.4/64.6/56.2 (BP=1.000, ratio=1.036, hyp_len=23992, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.23.0.32-1.37.0.33-1.39.0.66-1.93.0.62-1.86.pth, rkmy
BLEU = 69.38, 85.4/74.4/64.5/56.6 (BP=1.000, ratio=1.043, hyp_len=24524, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.24.0.32-1.37.0.33-1.39.0.66-1.94.0.62-1.87.pth, myrk
BLEU = 68.96, 85.1/73.9/64.2/56.0 (BP=1.000, ratio=1.046, hyp_len=24234, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.24.0.32-1.37.0.33-1.39.0.66-1.94.0.62-1.87.pth, rkmy
BLEU = 69.92, 85.6/74.9/65.1/57.3 (BP=1.000, ratio=1.042, hyp_len=24507, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.25.0.32-1.38.0.32-1.38.0.66-1.94.0.60-1.82.pth, myrk
BLEU = 68.44, 85.0/73.5/63.6/55.2 (BP=1.000, ratio=1.042, hyp_len=24133, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.25.0.32-1.38.0.32-1.38.0.66-1.94.0.60-1.82.pth, rkmy
BLEU = 65.55, 81.5/70.5/60.7/52.9 (BP=1.000, ratio=1.093, hyp_len=25700, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.26.0.30-1.34.0.30-1.35.0.68-1.97.0.60-1.83.pth, myrk
BLEU = 69.94, 86.0/74.7/65.2/57.1 (BP=1.000, ratio=1.037, hyp_len=24020, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.26.0.30-1.34.0.30-1.35.0.68-1.97.0.60-1.83.pth, rkmy
BLEU = 67.93, 84.4/73.0/63.0/54.9 (BP=1.000, ratio=1.060, hyp_len=24912, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.27.0.29-1.33.0.29-1.34.0.68-1.98.0.58-1.78.pth, myrk
BLEU = 68.87, 85.4/73.9/64.0/55.7 (BP=1.000, ratio=1.042, hyp_len=24135, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.27.0.29-1.33.0.29-1.34.0.68-1.98.0.58-1.78.pth, rkmy
BLEU = 69.06, 85.2/74.3/64.2/56.0 (BP=1.000, ratio=1.051, hyp_len=24702, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.28.0.27-1.31.0.27-1.32.0.67-1.96.0.62-1.87.pth, myrk
BLEU = 69.67, 85.6/74.4/65.0/57.0 (BP=1.000, ratio=1.034, hyp_len=23939, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.28.0.27-1.31.0.27-1.32.0.67-1.96.0.62-1.87.pth, rkmy
BLEU = 65.81, 82.6/71.3/60.9/52.4 (BP=1.000, ratio=1.084, hyp_len=25474, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.29.0.27-1.31.0.27-1.31.0.64-1.90.0.59-1.80.pth, myrk
BLEU = 65.81, 82.3/70.8/61.1/52.7 (BP=1.000, ratio=1.080, hyp_len=25017, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.29.0.27-1.31.0.27-1.31.0.64-1.90.0.59-1.80.pth, rkmy
BLEU = 67.93, 84.1/73.0/63.0/55.1 (BP=1.000, ratio=1.065, hyp_len=25040, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.30.0.26-1.30.0.26-1.30.0.65-1.91.0.61-1.84.pth, myrk
BLEU = 68.81, 84.7/73.7/64.2/55.9 (BP=1.000, ratio=1.056, hyp_len=24462, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.30.0.26-1.30.0.26-1.30.0.65-1.91.0.61-1.84.pth, rkmy
BLEU = 69.33, 85.2/74.3/64.4/56.6 (BP=1.000, ratio=1.052, hyp_len=24730, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.31.0.25-1.29.0.27-1.31.0.66-1.94.0.59-1.81.pth, myrk
BLEU = 70.22, 86.0/74.9/65.6/57.6 (BP=1.000, ratio=1.037, hyp_len=24028, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.31.0.25-1.29.0.27-1.31.0.66-1.94.0.59-1.81.pth, rkmy
BLEU = 68.07, 84.3/73.2/63.2/55.1 (BP=1.000, ratio=1.062, hyp_len=24972, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.32.0.25-1.29.0.26-1.29.0.64-1.89.0.62-1.86.pth, myrk
BLEU = 69.93, 85.4/74.6/65.4/57.5 (BP=1.000, ratio=1.045, hyp_len=24209, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.32.0.25-1.29.0.26-1.29.0.64-1.89.0.62-1.86.pth, rkmy
BLEU = 68.66, 84.8/73.8/63.7/55.7 (BP=1.000, ratio=1.058, hyp_len=24866, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.33.0.25-1.28.0.25-1.28.0.67-1.96.0.61-1.84.pth, myrk
BLEU = 68.70, 84.2/73.3/64.1/56.3 (BP=1.000, ratio=1.055, hyp_len=24437, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.33.0.25-1.28.0.25-1.28.0.67-1.96.0.61-1.84.pth, rkmy
BLEU = 68.16, 84.2/73.3/63.3/55.2 (BP=1.000, ratio=1.061, hyp_len=24940, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.34.0.24-1.27.0.24-1.27.0.67-1.96.0.59-1.80.pth, myrk
BLEU = 69.06, 84.8/73.8/64.5/56.3 (BP=1.000, ratio=1.053, hyp_len=24392, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.34.0.24-1.27.0.24-1.27.0.67-1.96.0.59-1.80.pth, rkmy
BLEU = 68.88, 85.0/74.1/63.9/55.9 (BP=1.000, ratio=1.053, hyp_len=24749, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.35.0.25-1.28.0.23-1.26.0.70-2.02.0.62-1.86.pth, myrk
BLEU = 67.33, 83.9/72.6/62.6/53.8 (BP=1.000, ratio=1.061, hyp_len=24582, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.35.0.25-1.28.0.23-1.26.0.70-2.02.0.62-1.86.pth, rkmy
BLEU = 69.20, 85.1/74.1/64.3/56.6 (BP=1.000, ratio=1.052, hyp_len=24736, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.36.0.23-1.26.0.23-1.26.0.67-1.95.0.58-1.79.pth, myrk
BLEU = 68.53, 85.0/73.6/63.7/55.3 (BP=1.000, ratio=1.050, hyp_len=24319, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.36.0.23-1.26.0.23-1.26.0.67-1.95.0.58-1.79.pth, rkmy
BLEU = 68.45, 84.5/73.6/63.6/55.5 (BP=1.000, ratio=1.061, hyp_len=24939, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.37.0.22-1.25.0.22-1.24.0.66-1.94.0.63-1.87.pth, myrk
BLEU = 69.62, 85.6/74.4/64.9/56.8 (BP=1.000, ratio=1.046, hyp_len=24218, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.37.0.22-1.25.0.22-1.24.0.66-1.94.0.63-1.87.pth, rkmy
BLEU = 69.47, 85.3/74.6/64.7/56.6 (BP=1.000, ratio=1.054, hyp_len=24783, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.38.0.21-1.23.0.21-1.24.0.69-1.99.0.63-1.88.pth, myrk
BLEU = 68.21, 84.8/73.2/63.4/55.0 (BP=1.000, ratio=1.056, hyp_len=24453, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.38.0.21-1.23.0.21-1.24.0.69-1.99.0.63-1.88.pth, rkmy
BLEU = 69.31, 85.3/74.5/64.4/56.3 (BP=1.000, ratio=1.052, hyp_len=24728, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.39.0.21-1.23.0.21-1.23.0.70-2.02.0.61-1.84.pth, myrk
BLEU = 69.42, 85.3/74.1/64.7/56.8 (BP=1.000, ratio=1.041, hyp_len=24112, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.39.0.21-1.23.0.21-1.23.0.70-2.02.0.61-1.84.pth, rkmy
BLEU = 67.30, 83.5/72.5/62.4/54.3 (BP=1.000, ratio=1.073, hyp_len=25220, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.40.0.20-1.23.0.21-1.23.0.67-1.95.0.62-1.86.pth, myrk
BLEU = 69.26, 85.3/74.1/64.6/56.4 (BP=1.000, ratio=1.050, hyp_len=24320, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.40.0.20-1.23.0.21-1.23.0.67-1.95.0.62-1.86.pth, rkmy
BLEU = 67.68, 84.0/72.8/62.8/54.6 (BP=1.000, ratio=1.067, hyp_len=25083, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.41.0.21-1.23.0.21-1.23.0.70-2.01.0.63-1.87.pth, myrk
BLEU = 69.82, 85.5/74.4/65.2/57.3 (BP=1.000, ratio=1.043, hyp_len=24166, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.41.0.21-1.23.0.21-1.23.0.70-2.01.0.63-1.87.pth, rkmy
BLEU = 69.33, 85.0/74.1/64.5/56.8 (BP=1.000, ratio=1.051, hyp_len=24708, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.42.0.22-1.24.0.21-1.23.0.68-1.98.0.63-1.88.pth, myrk
BLEU = 69.86, 85.7/74.6/65.1/57.2 (BP=1.000, ratio=1.045, hyp_len=24209, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.42.0.22-1.24.0.21-1.23.0.68-1.98.0.63-1.88.pth, rkmy
BLEU = 67.64, 83.8/72.7/62.7/54.8 (BP=1.000, ratio=1.070, hyp_len=25143, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.43.0.20-1.22.0.20-1.22.0.70-2.01.0.61-1.84.pth, myrk
BLEU = 69.84, 85.3/74.5/65.3/57.3 (BP=1.000, ratio=1.046, hyp_len=24229, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.43.0.20-1.22.0.20-1.22.0.70-2.01.0.61-1.84.pth, rkmy
BLEU = 69.15, 85.0/74.3/64.4/56.3 (BP=1.000, ratio=1.060, hyp_len=24922, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.44.0.19-1.20.0.18-1.20.0.70-2.02.0.61-1.85.pth, myrk
BLEU = 70.01, 85.6/74.6/65.4/57.5 (BP=1.000, ratio=1.041, hyp_len=24116, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.44.0.19-1.20.0.18-1.20.0.70-2.02.0.61-1.85.pth, rkmy
BLEU = 68.98, 84.6/73.9/64.2/56.4 (BP=1.000, ratio=1.065, hyp_len=25034, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.45.0.19-1.21.0.18-1.20.0.71-2.03.0.61-1.84.pth, myrk
BLEU = 68.42, 84.6/73.4/63.7/55.4 (BP=1.000, ratio=1.052, hyp_len=24374, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.45.0.19-1.21.0.18-1.20.0.71-2.03.0.61-1.84.pth, rkmy
BLEU = 69.68, 85.3/74.6/64.9/57.0 (BP=1.000, ratio=1.053, hyp_len=24750, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.46.0.18-1.19.0.18-1.19.0.70-2.01.0.62-1.86.pth, myrk
BLEU = 69.59, 85.4/74.3/64.9/56.9 (BP=1.000, ratio=1.048, hyp_len=24265, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.46.0.18-1.19.0.18-1.19.0.70-2.01.0.62-1.86.pth, rkmy
BLEU = 69.47, 85.2/74.4/64.7/56.8 (BP=1.000, ratio=1.056, hyp_len=24834, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.47.0.18-1.19.0.17-1.19.0.70-2.01.0.63-1.89.pth, myrk
BLEU = 67.68, 83.6/72.5/63.0/55.0 (BP=1.000, ratio=1.067, hyp_len=24719, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.47.0.18-1.19.0.17-1.19.0.70-2.01.0.63-1.89.pth, rkmy
BLEU = 69.83, 85.2/74.8/65.2/57.2 (BP=1.000, ratio=1.053, hyp_len=24766, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.48.0.17-1.19.0.18-1.19.0.70-2.01.0.64-1.89.pth, myrk
BLEU = 68.92, 84.4/73.5/64.4/56.5 (BP=1.000, ratio=1.060, hyp_len=24540, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.48.0.17-1.19.0.18-1.19.0.70-2.01.0.64-1.89.pth, rkmy
BLEU = 71.04, 86.3/75.8/66.4/58.7 (BP=1.000, ratio=1.041, hyp_len=24475, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.49.0.17-1.19.0.16-1.18.0.71-2.04.0.66-1.93.pth, myrk
BLEU = 69.81, 85.2/74.5/65.3/57.3 (BP=1.000, ratio=1.046, hyp_len=24215, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.49.0.17-1.19.0.16-1.18.0.71-2.04.0.66-1.93.pth, rkmy
BLEU = 69.02, 84.5/73.9/64.3/56.5 (BP=1.000, ratio=1.065, hyp_len=25027, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.50.0.17-1.18.0.17-1.18.0.72-2.05.0.64-1.90.pth, myrk
BLEU = 69.98, 85.4/74.5/65.4/57.6 (BP=1.000, ratio=1.043, hyp_len=24147, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.50.0.17-1.18.0.17-1.18.0.72-2.05.0.64-1.90.pth, rkmy
BLEU = 69.38, 85.1/74.2/64.5/56.8 (BP=1.000, ratio=1.053, hyp_len=24762, ref_len=23509)
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

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/transformer/myrk-60epoch
Evaluation result for the model: dsl-model-myrk.01.3.51-33.36.3.54-34.51.2.95-19.15.2.93-18.68.pth, myrk
BLEU = 9.04, 43.4/18.5/6.5/1.9 (BP=0.903, ratio=0.907, hyp_len=21011, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.01.3.51-33.36.3.54-34.51.2.95-19.15.2.93-18.68.pth, rkmy
BLEU = 7.28, 37.8/15.6/4.6/1.3 (BP=0.946, ratio=0.947, hyp_len=22268, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.02.2.34-10.40.2.37-10.74.1.97-7.15.1.97-7.14.pth, myrk
BLEU = 27.36, 59.4/35.8/21.2/12.4 (BP=1.000, ratio=1.009, hyp_len=23373, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.02.2.34-10.40.2.37-10.74.1.97-7.15.1.97-7.14.pth, rkmy
BLEU = 21.07, 50.7/29.1/15.7/8.5 (BP=1.000, ratio=1.105, hyp_len=25989, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.03.1.72-5.57.1.73-5.66.1.42-4.13.1.45-4.28.pth, myrk
BLEU = 44.26, 73.4/53.2/38.3/27.6 (BP=0.982, ratio=0.982, hyp_len=22743, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.03.1.72-5.57.1.73-5.66.1.42-4.13.1.45-4.28.pth, rkmy
BLEU = 39.45, 67.9/48.3/33.1/22.3 (BP=1.000, ratio=1.037, hyp_len=24368, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.04.1.34-3.81.1.33-3.77.1.17-3.21.1.10-3.02.pth, myrk
BLEU = 52.95, 78.6/61.0/47.0/36.3 (BP=0.990, ratio=0.991, hyp_len=22941, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.04.1.34-3.81.1.33-3.77.1.17-3.21.1.10-3.02.pth, rkmy
BLEU = 45.07, 69.7/52.7/39.0/28.8 (BP=1.000, ratio=1.105, hyp_len=25978, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.05.1.06-2.87.1.05-2.86.0.96-2.61.0.92-2.51.pth, myrk
BLEU = 57.08, 78.9/64.0/51.4/40.9 (BP=1.000, ratio=1.049, hyp_len=24284, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.05.1.06-2.87.1.05-2.86.0.96-2.61.0.92-2.51.pth, rkmy
BLEU = 56.08, 78.7/63.5/50.1/39.5 (BP=1.000, ratio=1.032, hyp_len=24270, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.06.0.88-2.41.0.90-2.46.0.86-2.37.0.85-2.35.pth, myrk
BLEU = 62.78, 82.7/68.8/57.2/47.8 (BP=1.000, ratio=1.018, hyp_len=23585, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.06.0.88-2.41.0.90-2.46.0.86-2.37.0.85-2.35.pth, rkmy
BLEU = 60.51, 81.5/67.2/54.7/44.7 (BP=1.000, ratio=1.015, hyp_len=23850, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.07.0.82-2.28.0.82-2.27.0.80-2.22.0.78-2.19.pth, myrk
BLEU = 60.16, 79.5/66.4/55.0/45.2 (BP=1.000, ratio=1.081, hyp_len=25039, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.07.0.82-2.28.0.82-2.27.0.80-2.22.0.78-2.19.pth, rkmy
BLEU = 60.54, 80.8/67.4/55.0/44.8 (BP=1.000, ratio=1.051, hyp_len=24702, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.08.0.70-2.02.0.71-2.04.0.76-2.13.0.73-2.08.pth, myrk
BLEU = 64.04, 83.0/70.2/58.8/49.1 (BP=1.000, ratio=1.040, hyp_len=24082, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.08.0.70-2.02.0.71-2.04.0.76-2.13.0.73-2.08.pth, rkmy
BLEU = 63.78, 83.0/69.9/58.4/48.9 (BP=1.000, ratio=1.024, hyp_len=24073, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.09.0.66-1.94.0.66-1.93.0.74-2.10.0.70-2.01.pth, myrk
BLEU = 60.25, 78.2/66.0/55.3/46.2 (BP=1.000, ratio=1.107, hyp_len=25639, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.09.0.66-1.94.0.66-1.93.0.74-2.10.0.70-2.01.pth, rkmy
BLEU = 63.63, 82.4/69.6/58.1/49.2 (BP=1.000, ratio=1.039, hyp_len=24428, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.10.0.61-1.85.0.62-1.86.0.71-2.04.0.70-2.02.pth, myrk
BLEU = 65.46, 83.2/71.1/60.5/51.2 (BP=1.000, ratio=1.049, hyp_len=24293, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.10.0.61-1.85.0.62-1.86.0.71-2.04.0.70-2.02.pth, rkmy
BLEU = 64.87, 83.1/70.9/59.7/50.4 (BP=1.000, ratio=1.047, hyp_len=24609, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.11.0.58-1.78.0.60-1.81.0.70-2.02.0.64-1.90.pth, myrk
BLEU = 63.94, 81.4/69.5/59.1/49.9 (BP=1.000, ratio=1.077, hyp_len=24937, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.11.0.58-1.78.0.60-1.81.0.70-2.02.0.64-1.90.pth, rkmy
BLEU = 62.01, 80.0/67.7/56.9/48.0 (BP=1.000, ratio=1.090, hyp_len=25633, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.12.0.49-1.63.0.50-1.64.0.70-2.01.0.62-1.86.pth, myrk
BLEU = 66.17, 83.6/71.6/61.2/52.4 (BP=1.000, ratio=1.049, hyp_len=24303, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.12.0.49-1.63.0.50-1.64.0.70-2.01.0.62-1.86.pth, rkmy
BLEU = 66.06, 83.6/71.8/61.0/52.0 (BP=1.000, ratio=1.047, hyp_len=24611, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.13.0.48-1.62.0.50-1.65.0.68-1.97.0.72-2.05.pth, myrk
BLEU = 66.12, 83.5/71.7/61.3/52.1 (BP=1.000, ratio=1.052, hyp_len=24362, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.13.0.48-1.62.0.50-1.65.0.68-1.97.0.72-2.05.pth, rkmy
BLEU = 60.82, 79.6/67.7/55.9/45.5 (BP=1.000, ratio=1.101, hyp_len=25876, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.14.0.47-1.59.0.45-1.57.0.69-1.99.0.62-1.85.pth, myrk
BLEU = 65.35, 83.1/71.1/60.4/51.1 (BP=1.000, ratio=1.055, hyp_len=24445, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.14.0.47-1.59.0.45-1.57.0.69-1.99.0.62-1.85.pth, rkmy
BLEU = 66.37, 84.4/72.1/61.2/52.1 (BP=1.000, ratio=1.040, hyp_len=24438, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.15.0.45-1.56.0.47-1.60.0.70-2.01.0.61-1.85.pth, myrk
BLEU = 67.53, 84.5/73.2/62.8/53.5 (BP=1.000, ratio=1.046, hyp_len=24231, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.15.0.45-1.56.0.47-1.60.0.70-2.01.0.61-1.85.pth, rkmy
BLEU = 67.48, 84.4/72.9/62.5/53.9 (BP=1.000, ratio=1.040, hyp_len=24454, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.16.0.42-1.52.0.41-1.51.0.66-1.94.0.62-1.86.pth, myrk
BLEU = 63.37, 80.1/68.5/58.6/50.2 (BP=1.000, ratio=1.106, hyp_len=25605, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.16.0.42-1.52.0.41-1.51.0.66-1.94.0.62-1.86.pth, rkmy
BLEU = 65.32, 83.3/71.2/60.1/51.1 (BP=1.000, ratio=1.055, hyp_len=24792, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.17.0.38-1.46.0.39-1.48.0.67-1.95.0.63-1.88.pth, myrk
BLEU = 70.40, 86.2/75.1/65.8/57.7 (BP=1.000, ratio=1.029, hyp_len=23824, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.17.0.38-1.46.0.39-1.48.0.67-1.95.0.63-1.88.pth, rkmy
BLEU = 63.64, 81.3/69.5/58.6/49.5 (BP=1.000, ratio=1.088, hyp_len=25573, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.18.0.39-1.48.0.38-1.47.0.67-1.96.0.60-1.82.pth, myrk
BLEU = 68.26, 84.8/73.4/63.4/54.9 (BP=1.000, ratio=1.038, hyp_len=24029, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.18.0.39-1.48.0.38-1.47.0.67-1.96.0.60-1.82.pth, rkmy
BLEU = 67.65, 84.7/73.1/62.6/54.0 (BP=1.000, ratio=1.044, hyp_len=24550, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.19.0.34-1.40.0.33-1.40.0.66-1.93.0.60-1.82.pth, myrk
BLEU = 69.73, 85.9/74.8/65.0/56.6 (BP=1.000, ratio=1.033, hyp_len=23915, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.19.0.34-1.40.0.33-1.40.0.66-1.93.0.60-1.82.pth, rkmy
BLEU = 69.11, 85.8/74.2/64.0/56.0 (BP=1.000, ratio=1.027, hyp_len=24149, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.20.0.35-1.42.0.36-1.43.0.66-1.94.0.58-1.79.pth, myrk
BLEU = 67.78, 84.1/72.7/63.1/54.7 (BP=1.000, ratio=1.050, hyp_len=24325, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.20.0.35-1.42.0.36-1.43.0.66-1.94.0.58-1.79.pth, rkmy
BLEU = 66.25, 83.8/72.0/61.2/52.2 (BP=1.000, ratio=1.058, hyp_len=24876, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.21.0.33-1.39.0.35-1.43.0.64-1.90.0.60-1.82.pth, myrk
BLEU = 67.66, 84.3/72.8/62.9/54.3 (BP=1.000, ratio=1.051, hyp_len=24342, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.21.0.33-1.39.0.35-1.43.0.64-1.90.0.60-1.82.pth, rkmy
BLEU = 66.89, 84.1/72.4/61.8/53.2 (BP=1.000, ratio=1.054, hyp_len=24769, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.22.0.34-1.41.0.35-1.41.0.64-1.89.0.57-1.76.pth, myrk
BLEU = 69.50, 85.0/74.1/64.9/57.1 (BP=1.000, ratio=1.042, hyp_len=24143, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.22.0.34-1.41.0.35-1.41.0.64-1.89.0.57-1.76.pth, rkmy
BLEU = 67.86, 84.7/73.5/62.9/54.2 (BP=1.000, ratio=1.053, hyp_len=24754, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.23.0.33-1.40.0.33-1.40.0.66-1.93.0.58-1.78.pth, myrk
BLEU = 67.80, 84.2/72.8/63.0/54.7 (BP=1.000, ratio=1.052, hyp_len=24362, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.23.0.33-1.40.0.33-1.40.0.66-1.93.0.58-1.78.pth, rkmy
BLEU = 67.84, 84.5/73.2/62.9/54.4 (BP=1.000, ratio=1.056, hyp_len=24824, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.24.0.31-1.36.0.32-1.37.0.66-1.93.0.58-1.79.pth, myrk
BLEU = 69.46, 85.5/74.2/64.7/56.7 (BP=1.000, ratio=1.040, hyp_len=24096, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.24.0.31-1.36.0.32-1.37.0.66-1.93.0.58-1.79.pth, rkmy
BLEU = 68.01, 84.7/73.4/63.1/54.6 (BP=1.000, ratio=1.048, hyp_len=24648, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.25.0.29-1.34.0.30-1.35.0.65-1.92.0.57-1.78.pth, myrk
BLEU = 67.88, 83.6/72.7/63.3/55.1 (BP=1.000, ratio=1.063, hyp_len=24623, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.25.0.29-1.34.0.30-1.35.0.65-1.92.0.57-1.78.pth, rkmy
BLEU = 68.71, 85.1/74.0/63.8/55.5 (BP=1.000, ratio=1.048, hyp_len=24645, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.26.0.29-1.33.0.29-1.34.0.66-1.94.0.59-1.80.pth, myrk
BLEU = 69.00, 85.2/74.1/64.4/55.8 (BP=1.000, ratio=1.048, hyp_len=24271, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.26.0.29-1.33.0.29-1.34.0.66-1.94.0.59-1.80.pth, rkmy
BLEU = 69.18, 85.7/74.4/64.2/55.9 (BP=1.000, ratio=1.040, hyp_len=24447, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.27.0.28-1.33.0.29-1.34.0.66-1.93.0.59-1.81.pth, myrk
BLEU = 67.90, 84.1/73.1/63.3/54.7 (BP=1.000, ratio=1.060, hyp_len=24549, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.27.0.28-1.33.0.29-1.34.0.66-1.93.0.59-1.81.pth, rkmy
BLEU = 66.65, 83.6/72.2/61.6/53.0 (BP=1.000, ratio=1.061, hyp_len=24947, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.28.0.28-1.32.0.29-1.34.0.67-1.95.0.64-1.89.pth, myrk
BLEU = 69.22, 85.3/74.1/64.5/56.3 (BP=1.000, ratio=1.039, hyp_len=24071, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.28.0.28-1.32.0.29-1.34.0.67-1.95.0.64-1.89.pth, rkmy
BLEU = 67.65, 84.3/73.1/62.6/54.3 (BP=1.000, ratio=1.056, hyp_len=24829, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.29.0.27-1.31.0.27-1.30.0.66-1.94.0.60-1.81.pth, myrk
BLEU = 67.46, 83.5/72.5/62.8/54.5 (BP=1.000, ratio=1.062, hyp_len=24603, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.29.0.27-1.31.0.27-1.30.0.66-1.94.0.60-1.81.pth, rkmy
BLEU = 69.11, 85.4/74.4/64.2/55.9 (BP=1.000, ratio=1.048, hyp_len=24627, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.30.0.25-1.28.0.25-1.29.0.66-1.93.0.59-1.81.pth, myrk
BLEU = 68.70, 84.6/73.6/64.1/55.8 (BP=1.000, ratio=1.052, hyp_len=24375, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.30.0.25-1.28.0.25-1.29.0.66-1.93.0.59-1.81.pth, rkmy
BLEU = 67.16, 83.8/72.3/62.2/54.0 (BP=1.000, ratio=1.064, hyp_len=25022, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.31.0.24-1.28.0.26-1.30.0.68-1.97.0.65-1.92.pth, myrk
BLEU = 69.38, 85.2/74.1/64.8/56.7 (BP=1.000, ratio=1.046, hyp_len=24235, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.31.0.24-1.28.0.26-1.30.0.68-1.97.0.65-1.92.pth, rkmy
BLEU = 68.06, 84.2/73.1/63.2/55.1 (BP=1.000, ratio=1.059, hyp_len=24894, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.32.0.24-1.27.0.24-1.27.0.67-1.95.0.61-1.84.pth, myrk
BLEU = 69.35, 85.0/74.1/64.7/56.8 (BP=1.000, ratio=1.054, hyp_len=24411, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.32.0.24-1.27.0.24-1.27.0.67-1.95.0.61-1.84.pth, rkmy
BLEU = 67.41, 83.9/72.8/62.6/54.1 (BP=1.000, ratio=1.066, hyp_len=25067, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.33.0.25-1.28.0.24-1.27.0.67-1.95.0.64-1.90.pth, myrk
BLEU = 70.13, 85.8/75.0/65.6/57.3 (BP=1.000, ratio=1.037, hyp_len=24011, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.33.0.25-1.28.0.24-1.27.0.67-1.95.0.64-1.90.pth, rkmy
BLEU = 67.42, 84.4/72.9/62.3/53.9 (BP=1.000, ratio=1.055, hyp_len=24798, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.34.0.24-1.27.0.23-1.26.0.68-1.97.0.62-1.85.pth, myrk
BLEU = 68.74, 84.4/73.4/64.2/56.2 (BP=1.000, ratio=1.059, hyp_len=24535, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.34.0.24-1.27.0.23-1.26.0.68-1.97.0.62-1.85.pth, rkmy
BLEU = 68.79, 85.5/74.2/63.8/55.4 (BP=1.000, ratio=1.045, hyp_len=24566, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.35.0.22-1.25.0.23-1.26.0.71-2.03.0.61-1.84.pth, myrk
BLEU = 68.88, 84.7/73.7/64.2/56.2 (BP=1.000, ratio=1.050, hyp_len=24317, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.35.0.22-1.25.0.23-1.26.0.71-2.03.0.61-1.84.pth, rkmy
BLEU = 67.65, 84.3/72.9/62.7/54.4 (BP=1.000, ratio=1.061, hyp_len=24944, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.36.0.22-1.25.0.23-1.26.0.66-1.93.0.62-1.86.pth, myrk
BLEU = 68.61, 84.8/73.6/63.9/55.5 (BP=1.000, ratio=1.051, hyp_len=24347, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.36.0.22-1.25.0.23-1.26.0.66-1.93.0.62-1.86.pth, rkmy
BLEU = 68.22, 84.7/73.5/63.2/55.0 (BP=1.000, ratio=1.052, hyp_len=24736, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.37.0.21-1.24.0.22-1.25.0.68-1.97.0.61-1.84.pth, myrk
BLEU = 69.14, 85.1/74.0/64.5/56.3 (BP=1.000, ratio=1.051, hyp_len=24352, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.37.0.21-1.24.0.22-1.25.0.68-1.97.0.61-1.84.pth, rkmy
BLEU = 69.18, 85.5/74.2/64.2/56.2 (BP=1.000, ratio=1.043, hyp_len=24525, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.38.0.20-1.22.0.20-1.22.0.67-1.96.0.62-1.85.pth, myrk
BLEU = 69.82, 85.2/74.5/65.3/57.4 (BP=1.000, ratio=1.051, hyp_len=24336, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.38.0.20-1.22.0.20-1.22.0.67-1.96.0.62-1.85.pth, rkmy
BLEU = 68.64, 85.0/73.9/63.8/55.4 (BP=1.000, ratio=1.052, hyp_len=24738, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.39.0.21-1.24.0.21-1.23.0.67-1.96.0.63-1.88.pth, myrk
BLEU = 68.83, 84.5/73.6/64.2/56.2 (BP=1.000, ratio=1.057, hyp_len=24477, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.39.0.21-1.24.0.21-1.23.0.67-1.96.0.63-1.88.pth, rkmy
BLEU = 68.95, 85.2/74.0/64.1/55.9 (BP=1.000, ratio=1.049, hyp_len=24665, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.40.0.20-1.22.0.20-1.23.0.68-1.97.0.64-1.89.pth, myrk
BLEU = 70.14, 85.6/75.0/65.7/57.5 (BP=1.000, ratio=1.048, hyp_len=24273, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.40.0.20-1.22.0.20-1.23.0.68-1.97.0.64-1.89.pth, rkmy
BLEU = 69.46, 85.4/74.5/64.6/56.6 (BP=1.000, ratio=1.050, hyp_len=24676, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.41.0.19-1.21.0.19-1.21.0.70-2.02.0.63-1.87.pth, myrk
BLEU = 68.22, 83.8/72.9/63.7/55.7 (BP=1.000, ratio=1.065, hyp_len=24662, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.41.0.19-1.21.0.19-1.21.0.70-2.02.0.63-1.87.pth, rkmy
BLEU = 68.06, 84.5/73.4/63.2/54.8 (BP=1.000, ratio=1.057, hyp_len=24848, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.42.0.20-1.22.0.20-1.22.0.70-2.02.0.63-1.87.pth, myrk
BLEU = 68.49, 84.3/73.5/63.9/55.5 (BP=1.000, ratio=1.059, hyp_len=24520, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.42.0.20-1.22.0.20-1.22.0.70-2.02.0.63-1.87.pth, rkmy
BLEU = 68.57, 85.0/73.8/63.6/55.4 (BP=1.000, ratio=1.053, hyp_len=24752, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.43.0.20-1.22.0.21-1.24.0.71-2.04.0.64-1.90.pth, myrk
BLEU = 68.98, 85.0/74.0/64.4/55.9 (BP=1.000, ratio=1.053, hyp_len=24384, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.43.0.20-1.22.0.21-1.24.0.71-2.04.0.64-1.90.pth, rkmy
BLEU = 67.48, 83.8/72.6/62.6/54.4 (BP=1.000, ratio=1.067, hyp_len=25084, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.44.0.19-1.21.0.19-1.21.0.68-1.98.0.62-1.86.pth, myrk
BLEU = 69.09, 84.9/73.8/64.5/56.4 (BP=1.000, ratio=1.056, hyp_len=24462, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.44.0.19-1.21.0.19-1.21.0.68-1.98.0.62-1.86.pth, rkmy
BLEU = 69.33, 85.3/74.4/64.4/56.4 (BP=1.000, ratio=1.054, hyp_len=24790, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.45.0.18-1.20.0.18-1.20.0.68-1.98.0.62-1.85.pth, myrk
BLEU = 68.03, 83.8/72.8/63.4/55.3 (BP=1.000, ratio=1.066, hyp_len=24689, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.45.0.18-1.20.0.18-1.20.0.68-1.98.0.62-1.85.pth, rkmy
BLEU = 67.62, 84.5/73.2/62.6/54.0 (BP=1.000, ratio=1.062, hyp_len=24968, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.46.0.18-1.20.0.19-1.20.0.71-2.04.0.66-1.93.pth, myrk
BLEU = 70.13, 85.1/74.6/65.7/58.0 (BP=1.000, ratio=1.058, hyp_len=24502, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.46.0.18-1.20.0.19-1.20.0.71-2.04.0.66-1.93.pth, rkmy
BLEU = 68.99, 85.1/74.1/64.1/56.0 (BP=1.000, ratio=1.051, hyp_len=24718, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.47.0.18-1.20.0.18-1.20.0.70-2.00.0.64-1.89.pth, myrk
BLEU = 70.05, 85.3/74.6/65.5/57.7 (BP=1.000, ratio=1.042, hyp_len=24143, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.47.0.18-1.20.0.18-1.20.0.70-2.00.0.64-1.89.pth, rkmy
BLEU = 68.00, 84.4/73.1/63.0/55.0 (BP=1.000, ratio=1.059, hyp_len=24888, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.48.0.17-1.19.0.17-1.19.0.71-2.04.0.66-1.93.pth, myrk
BLEU = 70.03, 85.6/74.8/65.4/57.5 (BP=1.000, ratio=1.045, hyp_len=24197, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.48.0.17-1.19.0.17-1.19.0.71-2.04.0.66-1.93.pth, rkmy
BLEU = 70.96, 86.4/75.8/66.3/58.4 (BP=1.000, ratio=1.038, hyp_len=24398, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.49.0.18-1.19.0.18-1.20.0.70-2.01.0.64-1.90.pth, myrk
BLEU = 68.96, 84.4/73.7/64.4/56.5 (BP=1.000, ratio=1.061, hyp_len=24565, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.49.0.18-1.19.0.18-1.20.0.70-2.01.0.64-1.90.pth, rkmy
BLEU = 68.91, 85.1/73.9/64.0/56.0 (BP=1.000, ratio=1.052, hyp_len=24729, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.50.0.16-1.18.0.17-1.19.0.72-2.05.0.64-1.90.pth, myrk
BLEU = 69.57, 85.4/74.3/64.9/56.9 (BP=1.000, ratio=1.045, hyp_len=24210, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.50.0.16-1.18.0.17-1.19.0.72-2.05.0.64-1.90.pth, rkmy
BLEU = 69.17, 85.0/74.1/64.4/56.5 (BP=1.000, ratio=1.055, hyp_len=24797, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.51.0.16-1.17.0.16-1.17.0.72-2.05.0.68-1.96.pth, myrk
BLEU = 70.30, 85.6/74.8/65.7/58.1 (BP=1.000, ratio=1.044, hyp_len=24187, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.51.0.16-1.17.0.16-1.17.0.72-2.05.0.68-1.96.pth, rkmy
BLEU = 68.46, 84.7/73.6/63.6/55.5 (BP=1.000, ratio=1.059, hyp_len=24898, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.52.0.17-1.18.0.17-1.19.0.71-2.03.0.65-1.91.pth, myrk
BLEU = 68.99, 84.5/73.6/64.4/56.5 (BP=1.000, ratio=1.057, hyp_len=24478, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.52.0.17-1.18.0.17-1.19.0.71-2.03.0.65-1.91.pth, rkmy
BLEU = 69.55, 85.5/74.4/64.7/56.8 (BP=1.000, ratio=1.047, hyp_len=24605, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.53.0.16-1.17.0.16-1.17.0.72-2.05.0.64-1.90.pth, myrk
BLEU = 70.48, 85.9/75.1/66.0/58.1 (BP=1.000, ratio=1.045, hyp_len=24205, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.53.0.16-1.17.0.16-1.17.0.72-2.05.0.64-1.90.pth, rkmy
BLEU = 69.62, 85.5/74.5/64.8/56.9 (BP=1.000, ratio=1.048, hyp_len=24649, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.54.0.16-1.17.0.16-1.17.0.71-2.04.0.65-1.91.pth, myrk
BLEU = 68.56, 84.0/73.3/64.1/56.0 (BP=1.000, ratio=1.066, hyp_len=24691, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.54.0.16-1.17.0.16-1.17.0.71-2.04.0.65-1.91.pth, rkmy
BLEU = 68.47, 84.8/73.6/63.6/55.4 (BP=1.000, ratio=1.054, hyp_len=24770, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.55.0.16-1.18.0.16-1.18.0.69-2.00.0.62-1.86.pth, myrk
BLEU = 68.11, 83.5/72.9/63.6/55.6 (BP=1.000, ratio=1.068, hyp_len=24738, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.55.0.16-1.18.0.16-1.18.0.69-2.00.0.62-1.86.pth, rkmy
BLEU = 68.15, 84.6/73.2/63.2/55.1 (BP=1.000, ratio=1.058, hyp_len=24872, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.56.0.16-1.17.0.16-1.18.0.73-2.08.0.65-1.92.pth, myrk
BLEU = 69.65, 85.0/74.3/65.1/57.2 (BP=1.000, ratio=1.050, hyp_len=24324, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.56.0.16-1.17.0.16-1.18.0.73-2.08.0.65-1.92.pth, rkmy
BLEU = 69.67, 85.4/74.6/64.9/57.0 (BP=1.000, ratio=1.051, hyp_len=24701, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.57.0.15-1.16.0.15-1.16.0.72-2.05.0.65-1.91.pth, myrk
BLEU = 70.53, 85.4/74.9/66.1/58.5 (BP=1.000, ratio=1.045, hyp_len=24210, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.57.0.15-1.16.0.15-1.16.0.72-2.05.0.65-1.91.pth, rkmy
BLEU = 68.25, 84.4/73.4/63.4/55.2 (BP=1.000, ratio=1.061, hyp_len=24948, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.58.0.15-1.16.0.15-1.16.0.71-2.04.0.64-1.90.pth, myrk
BLEU = 68.95, 83.7/73.3/64.5/57.1 (BP=1.000, ratio=1.064, hyp_len=24632, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.58.0.15-1.16.0.15-1.16.0.71-2.04.0.64-1.90.pth, rkmy
BLEU = 66.94, 83.9/72.5/62.0/53.3 (BP=1.000, ratio=1.068, hyp_len=25101, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.59.0.15-1.16.0.15-1.16.0.77-2.15.0.64-1.89.pth, myrk
BLEU = 69.55, 84.8/74.0/65.1/57.3 (BP=1.000, ratio=1.053, hyp_len=24399, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.59.0.15-1.16.0.15-1.16.0.77-2.15.0.64-1.89.pth, rkmy
BLEU = 68.21, 84.7/73.3/63.3/55.1 (BP=1.000, ratio=1.055, hyp_len=24806, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.60.0.14-1.15.0.14-1.15.0.74-2.10.0.64-1.89.pth, myrk
BLEU = 70.48, 85.5/74.8/66.0/58.5 (BP=1.000, ratio=1.049, hyp_len=24301, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.60.0.14-1.15.0.14-1.15.0.74-2.10.0.64-1.89.pth, rkmy
BLEU = 69.45, 85.2/74.4/64.7/56.7 (BP=1.000, ratio=1.053, hyp_len=24748, ref_len=23509)

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

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/transformer/myrk-70epoch
Evaluation result for the model: dsl-model-myrk.01.3.47-32.14.3.45-31.48.2.94-18.89.2.87-17.63.pth, myrk
BLEU = 3.06, 14.8/5.7/1.9/0.6 (BP=1.000, ratio=2.718, hyp_len=62959, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.01.3.47-32.14.3.45-31.48.2.94-18.89.2.87-17.63.pth, rkmy
BLEU = 7.94, 34.5/14.1/4.8/1.7 (BP=1.000, ratio=1.126, hyp_len=26466, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.02.2.39-10.90.2.34-10.34.2.10-8.14.1.97-7.18.pth, myrk
BLEU = 20.67, 48.8/28.0/15.7/8.5 (BP=1.000, ratio=1.190, hyp_len=27563, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.02.2.39-10.90.2.34-10.34.2.10-8.14.1.97-7.18.pth, rkmy
BLEU = 24.59, 56.5/33.3/18.7/10.4 (BP=0.999, ratio=0.999, hyp_len=23495, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.03.1.81-6.12.1.76-5.83.1.52-4.55.1.47-4.35.pth, myrk
BLEU = 40.89, 70.6/49.9/34.6/23.7 (BP=0.992, ratio=0.992, hyp_len=22972, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.03.1.81-6.12.1.76-5.83.1.52-4.55.1.47-4.35.pth, rkmy
BLEU = 37.20, 64.7/45.1/30.9/21.2 (BP=1.000, ratio=1.058, hyp_len=24878, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.04.1.33-3.78.1.31-3.70.1.19-3.28.1.14-3.13.pth, myrk
BLEU = 51.22, 75.5/58.5/45.1/34.6 (BP=1.000, ratio=1.034, hyp_len=23953, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.04.1.33-3.78.1.31-3.70.1.19-3.28.1.14-3.13.pth, rkmy
BLEU = 45.93, 70.1/53.4/39.8/29.9 (BP=1.000, ratio=1.095, hyp_len=25735, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.05.1.10-3.00.1.09-2.96.1.00-2.72.0.97-2.65.pth, myrk
BLEU = 59.57, 82.1/66.4/54.0/44.1 (BP=0.992, ratio=0.992, hyp_len=22980, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.05.1.10-3.00.1.09-2.96.1.00-2.72.0.97-2.65.pth, rkmy
BLEU = 55.86, 78.6/63.3/49.8/39.3 (BP=1.000, ratio=1.027, hyp_len=24155, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.06.0.98-2.66.0.94-2.56.0.87-2.38.0.86-2.37.pth, myrk
BLEU = 58.84, 80.1/65.6/53.3/42.8 (BP=1.000, ratio=1.052, hyp_len=24356, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.06.0.98-2.66.0.94-2.56.0.87-2.38.0.86-2.37.pth, rkmy
BLEU = 58.65, 80.1/65.5/52.8/42.7 (BP=1.000, ratio=1.034, hyp_len=24311, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.07.0.85-2.35.0.84-2.32.0.82-2.28.0.77-2.16.pth, myrk
BLEU = 62.61, 83.0/68.9/57.1/47.0 (BP=1.000, ratio=1.019, hyp_len=23597, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.07.0.85-2.35.0.84-2.32.0.82-2.28.0.77-2.16.pth, rkmy
BLEU = 61.13, 80.3/67.2/55.7/46.4 (BP=1.000, ratio=1.051, hyp_len=24711, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.08.0.72-2.05.0.70-2.02.0.76-2.15.0.76-2.14.pth, myrk
BLEU = 62.97, 82.6/69.3/57.6/47.7 (BP=1.000, ratio=1.039, hyp_len=24054, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.08.0.72-2.05.0.70-2.02.0.76-2.15.0.76-2.14.pth, rkmy
BLEU = 61.31, 81.3/67.9/55.8/45.9 (BP=1.000, ratio=1.039, hyp_len=24432, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.09.0.66-1.93.0.64-1.90.0.76-2.14.0.70-2.01.pth, myrk
BLEU = 65.62, 84.2/71.5/60.4/51.0 (BP=1.000, ratio=1.028, hyp_len=23801, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.09.0.66-1.93.0.64-1.90.0.76-2.14.0.70-2.01.pth, rkmy
BLEU = 63.05, 81.7/69.2/57.8/48.4 (BP=1.000, ratio=1.054, hyp_len=24782, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.10.0.63-1.88.0.64-1.89.0.71-2.04.0.65-1.92.pth, myrk
BLEU = 67.12, 85.2/72.6/62.0/52.9 (BP=1.000, ratio=1.025, hyp_len=23728, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.10.0.63-1.88.0.64-1.89.0.71-2.04.0.65-1.92.pth, rkmy
BLEU = 64.25, 82.6/70.0/58.9/50.0 (BP=1.000, ratio=1.050, hyp_len=24684, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.11.0.58-1.78.0.56-1.76.0.70-2.01.0.66-1.94.pth, myrk
BLEU = 63.10, 81.3/68.5/57.9/49.1 (BP=1.000, ratio=1.073, hyp_len=24853, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.11.0.58-1.78.0.56-1.76.0.70-2.01.0.66-1.94.pth, rkmy
BLEU = 62.78, 80.8/68.6/57.5/48.7 (BP=1.000, ratio=1.077, hyp_len=25327, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.12.0.52-1.69.0.54-1.71.0.70-2.01.0.64-1.89.pth, myrk
BLEU = 66.64, 84.7/72.1/61.5/52.6 (BP=1.000, ratio=1.032, hyp_len=23895, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.12.0.52-1.69.0.54-1.71.0.70-2.01.0.64-1.89.pth, rkmy
BLEU = 65.13, 82.8/70.9/60.0/51.1 (BP=1.000, ratio=1.058, hyp_len=24878, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.13.0.46-1.58.0.45-1.57.0.66-1.94.0.63-1.88.pth, myrk
BLEU = 66.00, 84.2/71.7/61.0/51.6 (BP=1.000, ratio=1.047, hyp_len=24240, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.13.0.46-1.58.0.45-1.57.0.66-1.94.0.63-1.88.pth, rkmy
BLEU = 67.21, 84.5/72.7/62.0/53.6 (BP=1.000, ratio=1.039, hyp_len=24415, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.14.0.49-1.63.0.48-1.62.0.66-1.94.0.60-1.83.pth, myrk
BLEU = 68.69, 86.2/74.1/63.7/54.8 (BP=1.000, ratio=1.019, hyp_len=23611, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.14.0.49-1.63.0.48-1.62.0.66-1.94.0.60-1.83.pth, rkmy
BLEU = 66.21, 83.4/71.9/61.1/52.5 (BP=1.000, ratio=1.055, hyp_len=24802, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.15.0.47-1.60.0.45-1.57.0.67-1.95.0.62-1.86.pth, myrk
BLEU = 67.09, 84.8/72.6/62.1/53.0 (BP=1.000, ratio=1.035, hyp_len=23973, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.15.0.47-1.60.0.45-1.57.0.67-1.95.0.62-1.86.pth, rkmy
BLEU = 67.41, 84.6/72.8/62.2/53.9 (BP=1.000, ratio=1.035, hyp_len=24342, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.16.0.39-1.47.0.38-1.46.0.66-1.94.0.59-1.81.pth, myrk
BLEU = 68.13, 85.2/73.4/63.2/54.5 (BP=1.000, ratio=1.035, hyp_len=23963, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.16.0.39-1.47.0.38-1.46.0.66-1.94.0.59-1.81.pth, rkmy
BLEU = 67.83, 84.5/73.0/62.8/54.7 (BP=1.000, ratio=1.045, hyp_len=24574, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.17.0.40-1.50.0.40-1.49.0.64-1.89.0.59-1.80.pth, myrk
BLEU = 67.25, 84.4/72.5/62.3/53.7 (BP=1.000, ratio=1.051, hyp_len=24334, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.17.0.40-1.50.0.40-1.49.0.64-1.89.0.59-1.80.pth, rkmy
BLEU = 68.77, 85.1/74.1/63.9/55.5 (BP=1.000, ratio=1.042, hyp_len=24487, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.18.0.38-1.46.0.37-1.45.0.65-1.92.0.60-1.82.pth, myrk
BLEU = 68.57, 85.3/73.5/63.7/55.3 (BP=1.000, ratio=1.035, hyp_len=23977, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.18.0.38-1.46.0.37-1.45.0.65-1.92.0.60-1.82.pth, rkmy
BLEU = 67.57, 84.3/73.0/62.5/54.2 (BP=1.000, ratio=1.052, hyp_len=24742, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.19.0.36-1.43.0.35-1.41.0.67-1.95.0.58-1.78.pth, myrk
BLEU = 63.46, 80.5/69.0/58.7/49.7 (BP=1.000, ratio=1.107, hyp_len=25641, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.19.0.36-1.43.0.35-1.41.0.67-1.95.0.58-1.78.pth, rkmy
BLEU = 68.66, 85.2/74.0/63.7/55.3 (BP=1.000, ratio=1.041, hyp_len=24465, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.20.0.34-1.41.0.34-1.40.0.65-1.91.0.58-1.78.pth, myrk
BLEU = 62.49, 79.2/68.0/57.9/48.9 (BP=1.000, ratio=1.119, hyp_len=25924, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.20.0.34-1.41.0.34-1.40.0.65-1.91.0.58-1.78.pth, rkmy
BLEU = 61.71, 78.0/66.7/56.9/49.0 (BP=1.000, ratio=1.133, hyp_len=26642, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.21.0.35-1.42.0.36-1.43.0.65-1.92.0.60-1.82.pth, myrk
BLEU = 69.21, 85.8/74.1/64.3/56.1 (BP=1.000, ratio=1.032, hyp_len=23899, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.21.0.35-1.42.0.36-1.43.0.65-1.92.0.60-1.82.pth, rkmy
BLEU = 67.87, 84.9/73.4/62.7/54.3 (BP=1.000, ratio=1.042, hyp_len=24503, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.22.0.32-1.38.0.33-1.39.0.66-1.94.0.59-1.80.pth, myrk
BLEU = 69.80, 86.1/74.6/65.0/56.9 (BP=1.000, ratio=1.036, hyp_len=23983, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.22.0.32-1.38.0.33-1.39.0.66-1.94.0.59-1.80.pth, rkmy
BLEU = 67.36, 83.6/72.7/62.6/54.1 (BP=1.000, ratio=1.069, hyp_len=25139, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.23.0.33-1.39.0.31-1.37.0.65-1.92.0.58-1.78.pth, myrk
BLEU = 68.80, 85.0/73.6/64.0/55.9 (BP=1.000, ratio=1.047, hyp_len=24260, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.23.0.33-1.39.0.31-1.37.0.65-1.92.0.58-1.78.pth, rkmy
BLEU = 69.29, 85.4/74.3/64.5/56.3 (BP=1.000, ratio=1.041, hyp_len=24475, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.24.0.32-1.37.0.32-1.38.0.66-1.93.0.59-1.80.pth, myrk
BLEU = 69.06, 85.4/74.0/64.2/56.0 (BP=1.000, ratio=1.045, hyp_len=24212, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.24.0.32-1.37.0.32-1.38.0.66-1.93.0.59-1.80.pth, rkmy
BLEU = 69.69, 85.5/74.8/64.9/56.9 (BP=1.000, ratio=1.045, hyp_len=24565, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.25.0.29-1.33.0.28-1.33.0.66-1.93.0.58-1.78.pth, myrk
BLEU = 69.76, 86.1/74.5/65.0/56.8 (BP=1.000, ratio=1.036, hyp_len=23992, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.25.0.29-1.33.0.28-1.33.0.66-1.93.0.58-1.78.pth, rkmy
BLEU = 70.01, 85.8/75.2/65.3/57.1 (BP=1.000, ratio=1.041, hyp_len=24472, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.26.0.30-1.35.0.30-1.35.0.66-1.93.0.59-1.81.pth, myrk
BLEU = 70.15, 86.3/74.9/65.4/57.3 (BP=1.000, ratio=1.020, hyp_len=23620, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.26.0.30-1.35.0.30-1.35.0.66-1.93.0.59-1.81.pth, rkmy
BLEU = 68.71, 85.0/74.1/63.8/55.5 (BP=1.000, ratio=1.054, hyp_len=24775, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.27.0.27-1.32.0.27-1.31.0.66-1.93.0.62-1.85.pth, myrk
BLEU = 69.32, 85.8/74.2/64.5/56.2 (BP=1.000, ratio=1.042, hyp_len=24123, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.27.0.27-1.32.0.27-1.31.0.66-1.93.0.62-1.85.pth, rkmy
BLEU = 61.65, 76.7/66.5/57.2/49.5 (BP=1.000, ratio=1.170, hyp_len=27495, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.28.0.27-1.31.0.26-1.29.0.67-1.95.0.60-1.83.pth, myrk
BLEU = 69.59, 85.6/74.4/64.9/56.8 (BP=1.000, ratio=1.043, hyp_len=24146, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.28.0.27-1.31.0.26-1.29.0.67-1.95.0.60-1.83.pth, rkmy
BLEU = 67.35, 83.8/72.7/62.5/54.0 (BP=1.000, ratio=1.067, hyp_len=25076, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.29.0.26-1.30.0.26-1.30.0.65-1.92.0.60-1.81.pth, myrk
BLEU = 69.71, 85.4/74.3/65.1/57.1 (BP=1.000, ratio=1.047, hyp_len=24242, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.29.0.26-1.30.0.26-1.30.0.65-1.92.0.60-1.81.pth, rkmy
BLEU = 68.39, 84.2/73.6/63.7/55.5 (BP=1.000, ratio=1.061, hyp_len=24949, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.30.0.26-1.29.0.26-1.29.0.66-1.93.0.57-1.77.pth, myrk
BLEU = 69.33, 85.3/74.0/64.6/56.6 (BP=1.000, ratio=1.045, hyp_len=24199, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.30.0.26-1.29.0.26-1.29.0.66-1.93.0.57-1.77.pth, rkmy
BLEU = 67.14, 82.9/72.2/62.3/54.5 (BP=1.000, ratio=1.079, hyp_len=25366, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.31.0.24-1.27.0.24-1.27.0.66-1.93.0.58-1.78.pth, myrk
BLEU = 70.13, 85.9/74.8/65.5/57.4 (BP=1.000, ratio=1.039, hyp_len=24066, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.31.0.24-1.27.0.24-1.27.0.66-1.93.0.58-1.78.pth, rkmy
BLEU = 69.94, 85.5/75.0/65.3/57.2 (BP=1.000, ratio=1.047, hyp_len=24609, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.32.0.24-1.27.0.23-1.26.0.68-1.97.0.58-1.79.pth, myrk
BLEU = 67.00, 83.4/72.1/62.3/53.8 (BP=1.000, ratio=1.067, hyp_len=24708, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.32.0.24-1.27.0.23-1.26.0.68-1.97.0.58-1.79.pth, rkmy
BLEU = 69.76, 85.4/74.8/65.0/57.0 (BP=1.000, ratio=1.045, hyp_len=24557, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.33.0.24-1.27.0.24-1.27.0.68-1.98.0.58-1.78.pth, myrk
BLEU = 70.67, 86.2/75.1/66.0/58.3 (BP=1.000, ratio=1.031, hyp_len=23883, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.33.0.24-1.27.0.24-1.27.0.68-1.98.0.58-1.78.pth, rkmy
BLEU = 69.34, 85.5/74.6/64.5/56.2 (BP=1.000, ratio=1.049, hyp_len=24666, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.34.0.23-1.26.0.23-1.26.0.68-1.98.0.59-1.81.pth, myrk
BLEU = 69.76, 85.4/74.3/65.1/57.3 (BP=1.000, ratio=1.046, hyp_len=24226, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.34.0.23-1.26.0.23-1.26.0.68-1.98.0.59-1.81.pth, rkmy
BLEU = 68.72, 84.8/73.9/63.9/55.7 (BP=1.000, ratio=1.058, hyp_len=24866, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.35.0.23-1.26.0.23-1.26.0.68-1.98.0.59-1.80.pth, myrk
BLEU = 69.68, 85.4/74.4/65.0/57.1 (BP=1.000, ratio=1.043, hyp_len=24162, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.35.0.23-1.26.0.23-1.26.0.68-1.98.0.59-1.80.pth, rkmy
BLEU = 69.51, 85.2/74.5/64.8/56.8 (BP=1.000, ratio=1.050, hyp_len=24690, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.36.0.24-1.27.0.22-1.25.0.69-1.98.0.59-1.80.pth, myrk
BLEU = 69.87, 85.4/74.6/65.3/57.3 (BP=1.000, ratio=1.042, hyp_len=24135, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.36.0.24-1.27.0.22-1.25.0.69-1.98.0.59-1.80.pth, rkmy
BLEU = 70.34, 85.9/75.2/65.5/57.8 (BP=1.000, ratio=1.045, hyp_len=24569, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.37.0.20-1.23.0.20-1.23.0.67-1.96.0.58-1.78.pth, myrk
BLEU = 69.43, 85.1/73.9/64.8/57.0 (BP=1.000, ratio=1.052, hyp_len=24370, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.37.0.20-1.23.0.20-1.23.0.67-1.96.0.58-1.78.pth, rkmy
BLEU = 68.50, 84.9/73.7/63.5/55.4 (BP=1.000, ratio=1.052, hyp_len=24735, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.38.0.22-1.25.0.21-1.24.0.69-1.99.0.57-1.76.pth, myrk
BLEU = 68.91, 85.4/74.1/64.2/55.5 (BP=1.000, ratio=1.053, hyp_len=24383, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.38.0.22-1.25.0.21-1.24.0.69-1.99.0.57-1.76.pth, rkmy
BLEU = 69.40, 85.1/74.4/64.6/56.6 (BP=1.000, ratio=1.054, hyp_len=24772, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.39.0.21-1.23.0.20-1.22.0.67-1.96.0.58-1.78.pth, myrk
BLEU = 69.46, 85.4/74.2/64.8/56.7 (BP=1.000, ratio=1.045, hyp_len=24195, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.39.0.21-1.23.0.20-1.22.0.67-1.96.0.58-1.78.pth, rkmy
BLEU = 68.46, 84.7/73.7/63.6/55.4 (BP=1.000, ratio=1.058, hyp_len=24868, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.40.0.21-1.23.0.21-1.23.0.69-2.00.0.60-1.82.pth, myrk
BLEU = 69.94, 85.5/74.4/65.3/57.6 (BP=1.000, ratio=1.040, hyp_len=24087, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.40.0.21-1.23.0.21-1.23.0.69-2.00.0.60-1.82.pth, rkmy
BLEU = 67.47, 83.7/72.7/62.6/54.4 (BP=1.000, ratio=1.071, hyp_len=25175, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.41.0.20-1.22.0.19-1.21.0.72-2.06.0.60-1.83.pth, myrk
BLEU = 69.58, 85.7/74.4/64.8/56.7 (BP=1.000, ratio=1.042, hyp_len=24133, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.41.0.20-1.22.0.19-1.21.0.72-2.06.0.60-1.83.pth, rkmy
BLEU = 69.70, 84.9/74.5/65.0/57.4 (BP=1.000, ratio=1.056, hyp_len=24820, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.42.0.20-1.22.0.20-1.22.0.69-1.99.0.61-1.84.pth, myrk
BLEU = 69.56, 85.1/74.3/65.0/57.0 (BP=1.000, ratio=1.049, hyp_len=24289, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.42.0.20-1.22.0.20-1.22.0.69-1.99.0.61-1.84.pth, rkmy
BLEU = 67.84, 84.0/72.9/62.9/55.0 (BP=1.000, ratio=1.065, hyp_len=25033, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.43.0.20-1.22.0.21-1.23.0.72-2.06.0.64-1.90.pth, myrk
BLEU = 70.45, 85.7/74.9/65.9/58.2 (BP=1.000, ratio=1.039, hyp_len=24072, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.43.0.20-1.22.0.21-1.23.0.72-2.06.0.64-1.90.pth, rkmy
BLEU = 68.32, 84.9/73.6/63.3/55.1 (BP=1.000, ratio=1.039, hyp_len=24416, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.44.0.19-1.21.0.18-1.20.0.70-2.01.0.58-1.79.pth, myrk
BLEU = 69.96, 85.8/74.7/65.3/57.3 (BP=1.000, ratio=1.045, hyp_len=24210, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.44.0.19-1.21.0.18-1.20.0.70-2.01.0.58-1.79.pth, rkmy
BLEU = 69.20, 85.0/74.3/64.5/56.3 (BP=1.000, ratio=1.054, hyp_len=24782, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.45.0.18-1.20.0.17-1.19.0.72-2.05.0.61-1.84.pth, myrk
BLEU = 71.08, 86.0/75.4/66.6/59.0 (BP=1.000, ratio=1.037, hyp_len=24023, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.45.0.18-1.20.0.17-1.19.0.72-2.05.0.61-1.84.pth, rkmy
BLEU = 68.76, 84.7/73.8/64.0/55.9 (BP=1.000, ratio=1.062, hyp_len=24973, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.46.0.19-1.21.0.18-1.20.0.71-2.02.0.63-1.88.pth, myrk
BLEU = 69.32, 85.4/74.1/64.7/56.5 (BP=1.000, ratio=1.047, hyp_len=24255, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.46.0.19-1.21.0.18-1.20.0.71-2.02.0.63-1.88.pth, rkmy
BLEU = 68.67, 84.3/73.6/63.9/56.1 (BP=1.000, ratio=1.065, hyp_len=25029, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.47.0.18-1.19.0.17-1.19.0.73-2.08.0.61-1.85.pth, myrk
BLEU = 69.29, 85.3/74.0/64.5/56.6 (BP=1.000, ratio=1.048, hyp_len=24275, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.47.0.18-1.19.0.17-1.19.0.73-2.08.0.61-1.85.pth, rkmy
BLEU = 69.92, 85.4/74.8/65.2/57.4 (BP=1.000, ratio=1.054, hyp_len=24776, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.48.0.18-1.20.0.17-1.19.0.72-2.06.0.61-1.85.pth, myrk
BLEU = 70.67, 86.2/75.3/66.0/58.2 (BP=1.000, ratio=1.034, hyp_len=23948, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.48.0.18-1.20.0.17-1.19.0.72-2.06.0.61-1.85.pth, rkmy
BLEU = 68.04, 83.9/73.0/63.3/55.3 (BP=1.000, ratio=1.072, hyp_len=25203, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.49.0.16-1.18.0.17-1.18.0.71-2.03.0.61-1.84.pth, myrk
BLEU = 70.20, 85.9/74.8/65.6/57.7 (BP=1.000, ratio=1.043, hyp_len=24161, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.49.0.16-1.18.0.17-1.18.0.71-2.03.0.61-1.84.pth, rkmy
BLEU = 69.08, 84.9/74.2/64.3/56.3 (BP=1.000, ratio=1.056, hyp_len=24828, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.50.0.17-1.18.0.17-1.18.0.72-2.06.0.65-1.91.pth, myrk
BLEU = 70.45, 85.9/75.0/65.9/58.0 (BP=1.000, ratio=1.044, hyp_len=24171, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.50.0.17-1.18.0.17-1.18.0.72-2.06.0.65-1.91.pth, rkmy
BLEU = 68.59, 84.6/73.7/63.7/55.7 (BP=1.000, ratio=1.061, hyp_len=24950, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.51.0.17-1.19.0.17-1.18.0.75-2.11.0.62-1.86.pth, myrk
BLEU = 69.87, 85.0/74.3/65.4/57.7 (BP=1.000, ratio=1.049, hyp_len=24293, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.51.0.17-1.19.0.17-1.18.0.75-2.11.0.62-1.86.pth, rkmy
BLEU = 70.55, 85.9/75.3/65.8/58.2 (BP=1.000, ratio=1.043, hyp_len=24525, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.52.0.16-1.18.0.16-1.17.0.74-2.09.0.63-1.88.pth, myrk
BLEU = 69.70, 85.2/74.3/65.1/57.2 (BP=1.000, ratio=1.047, hyp_len=24239, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.52.0.16-1.18.0.16-1.17.0.74-2.09.0.63-1.88.pth, rkmy
BLEU = 70.02, 85.3/74.8/65.4/57.6 (BP=1.000, ratio=1.054, hyp_len=24773, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.53.0.18-1.19.0.16-1.18.0.73-2.08.0.64-1.89.pth, myrk
BLEU = 69.98, 85.4/74.4/65.4/57.7 (BP=1.000, ratio=1.045, hyp_len=24204, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.53.0.18-1.19.0.16-1.18.0.73-2.08.0.64-1.89.pth, rkmy
BLEU = 68.15, 84.4/73.2/63.2/55.3 (BP=1.000, ratio=1.061, hyp_len=24940, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.54.0.16-1.17.0.16-1.17.0.73-2.08.0.63-1.88.pth, myrk
BLEU = 70.02, 85.7/74.7/65.4/57.3 (BP=1.000, ratio=1.044, hyp_len=24190, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.54.0.16-1.17.0.16-1.17.0.73-2.08.0.63-1.88.pth, rkmy
BLEU = 68.95, 84.9/73.9/64.2/56.1 (BP=1.000, ratio=1.060, hyp_len=24918, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.55.0.16-1.17.0.15-1.17.0.73-2.08.0.64-1.90.pth, myrk
BLEU = 69.42, 85.2/74.1/64.8/56.7 (BP=1.000, ratio=1.045, hyp_len=24207, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.55.0.16-1.17.0.15-1.17.0.73-2.08.0.64-1.90.pth, rkmy
BLEU = 68.65, 84.5/73.6/63.9/55.9 (BP=1.000, ratio=1.066, hyp_len=25068, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.56.0.16-1.17.0.16-1.17.0.74-2.09.0.63-1.88.pth, myrk
BLEU = 69.01, 84.8/73.8/64.4/56.3 (BP=1.000, ratio=1.049, hyp_len=24303, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.56.0.16-1.17.0.16-1.17.0.74-2.09.0.63-1.88.pth, rkmy
BLEU = 69.31, 85.2/74.3/64.5/56.5 (BP=1.000, ratio=1.053, hyp_len=24747, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.57.0.14-1.15.0.14-1.16.0.74-2.09.0.66-1.94.pth, myrk
BLEU = 69.78, 85.2/74.2/65.2/57.6 (BP=1.000, ratio=1.047, hyp_len=24242, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.57.0.14-1.15.0.14-1.16.0.74-2.09.0.66-1.94.pth, rkmy
BLEU = 69.64, 84.8/74.5/65.0/57.2 (BP=1.000, ratio=1.061, hyp_len=24947, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.58.0.15-1.16.0.15-1.16.0.75-2.12.0.65-1.91.pth, myrk
BLEU = 70.00, 85.3/74.6/65.5/57.6 (BP=1.000, ratio=1.043, hyp_len=24158, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.58.0.15-1.16.0.15-1.16.0.75-2.12.0.65-1.91.pth, rkmy
BLEU = 69.83, 85.4/74.8/65.1/57.3 (BP=1.000, ratio=1.053, hyp_len=24755, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.59.0.14-1.15.0.14-1.15.0.77-2.17.0.63-1.88.pth, myrk
BLEU = 70.03, 85.7/74.7/65.4/57.5 (BP=1.000, ratio=1.038, hyp_len=24050, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.59.0.14-1.15.0.14-1.15.0.77-2.17.0.63-1.88.pth, rkmy
BLEU = 70.20, 85.6/75.1/65.5/57.7 (BP=1.000, ratio=1.052, hyp_len=24727, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.60.0.14-1.16.0.14-1.15.0.76-2.14.0.66-1.94.pth, myrk
BLEU = 69.44, 85.1/74.1/64.8/56.9 (BP=1.000, ratio=1.047, hyp_len=24259, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.60.0.14-1.16.0.14-1.15.0.76-2.14.0.66-1.94.pth, rkmy
BLEU = 70.22, 85.6/75.1/65.5/57.8 (BP=1.000, ratio=1.052, hyp_len=24732, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.61.0.16-1.17.0.15-1.16.0.77-2.16.0.65-1.91.pth, myrk
BLEU = 68.55, 84.4/73.3/63.9/55.8 (BP=1.000, ratio=1.055, hyp_len=24440, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.61.0.16-1.17.0.15-1.16.0.77-2.16.0.65-1.91.pth, rkmy
BLEU = 69.73, 85.3/74.5/65.0/57.2 (BP=1.000, ratio=1.054, hyp_len=24779, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.62.0.14-1.15.0.14-1.15.0.78-2.18.0.66-1.94.pth, myrk
BLEU = 69.14, 84.9/73.8/64.6/56.4 (BP=1.000, ratio=1.052, hyp_len=24367, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.62.0.14-1.15.0.14-1.15.0.78-2.18.0.66-1.94.pth, rkmy
BLEU = 70.75, 86.1/75.5/66.0/58.3 (BP=1.000, ratio=1.043, hyp_len=24527, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.63.0.14-1.15.0.14-1.15.0.77-2.16.0.65-1.91.pth, myrk
BLEU = 68.10, 84.5/73.0/63.3/55.1 (BP=1.000, ratio=1.053, hyp_len=24396, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.63.0.14-1.15.0.14-1.15.0.77-2.16.0.65-1.91.pth, rkmy
BLEU = 70.07, 85.3/74.8/65.4/57.8 (BP=1.000, ratio=1.056, hyp_len=24817, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.64.0.13-1.14.0.13-1.14.0.79-2.21.0.63-1.89.pth, myrk
BLEU = 69.04, 84.8/73.6/64.4/56.5 (BP=1.000, ratio=1.049, hyp_len=24304, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.64.0.13-1.14.0.13-1.14.0.79-2.21.0.63-1.89.pth, rkmy
BLEU = 69.88, 85.6/74.9/65.2/57.1 (BP=1.000, ratio=1.053, hyp_len=24761, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.65.0.13-1.14.0.14-1.15.0.78-2.19.0.66-1.94.pth, myrk
BLEU = 69.54, 85.4/74.4/64.9/56.7 (BP=1.000, ratio=1.047, hyp_len=24244, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.65.0.13-1.14.0.14-1.15.0.78-2.19.0.66-1.94.pth, rkmy
BLEU = 69.61, 85.2/74.7/64.9/56.8 (BP=1.000, ratio=1.057, hyp_len=24850, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.66.0.13-1.14.0.13-1.14.0.78-2.18.0.67-1.96.pth, myrk
BLEU = 69.89, 85.5/74.5/65.3/57.4 (BP=1.000, ratio=1.046, hyp_len=24235, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.66.0.13-1.14.0.13-1.14.0.78-2.18.0.67-1.96.pth, rkmy
BLEU = 71.57, 86.7/76.4/66.9/59.2 (BP=1.000, ratio=1.039, hyp_len=24435, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.67.0.14-1.15.0.13-1.14.0.81-2.25.0.64-1.90.pth, myrk
BLEU = 69.48, 85.2/74.2/64.9/56.8 (BP=1.000, ratio=1.047, hyp_len=24256, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.67.0.14-1.15.0.13-1.14.0.81-2.25.0.64-1.90.pth, rkmy
BLEU = 69.89, 85.4/74.8/65.2/57.4 (BP=1.000, ratio=1.053, hyp_len=24760, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.68.0.13-1.14.0.13-1.14.0.79-2.21.0.68-1.98.pth, myrk
BLEU = 69.92, 85.6/74.6/65.3/57.4 (BP=1.000, ratio=1.041, hyp_len=24118, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.68.0.13-1.14.0.13-1.14.0.79-2.21.0.68-1.98.pth, rkmy
BLEU = 68.96, 85.0/74.1/64.1/56.0 (BP=1.000, ratio=1.058, hyp_len=24884, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.69.0.13-1.14.0.13-1.13.0.80-2.23.0.69-1.99.pth, myrk
BLEU = 69.90, 85.3/74.4/65.3/57.6 (BP=1.000, ratio=1.046, hyp_len=24220, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.69.0.13-1.14.0.13-1.13.0.80-2.23.0.69-1.99.pth, rkmy
BLEU = 68.55, 84.4/73.6/63.8/55.7 (BP=1.000, ratio=1.061, hyp_len=24951, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.70.0.13-1.14.0.13-1.14.0.80-2.22.0.71-2.03.pth, myrk
BLEU = 69.43, 85.3/74.2/64.8/56.7 (BP=1.000, ratio=1.047, hyp_len=24242, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.70.0.13-1.14.0.13-1.14.0.80-2.22.0.71-2.03.pth, rkmy
BLEU = 69.21, 84.8/74.1/64.6/56.5 (BP=1.000, ratio=1.065, hyp_len=25035, ref_len=23509)
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

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/transformer/myrk-80epoch
Evaluation result for the model: dsl-model-myrk.01.3.60-36.61.3.59-36.18.3.07-21.49.2.99-19.83.pth, myrk
BLEU = 4.33, 23.2/8.5/2.6/0.7 (BP=1.000, ratio=1.622, hyp_len=37558, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.01.3.60-36.61.3.59-36.18.3.07-21.49.2.99-19.83.pth, rkmy
BLEU = 1.82, 10.1/3.6/1.1/0.3 (BP=1.000, ratio=3.391, hyp_len=79721, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.02.2.52-12.46.2.48-11.97.2.12-8.37.2.08-8.00.pth, myrk
BLEU = 21.16, 51.0/29.1/15.9/8.5 (BP=1.000, ratio=1.100, hyp_len=25469, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.02.2.52-12.46.2.48-11.97.2.12-8.37.2.08-8.00.pth, rkmy
BLEU = 22.01, 53.6/30.4/16.4/8.8 (BP=1.000, ratio=1.021, hyp_len=24008, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.03.1.76-5.79.1.75-5.76.1.52-4.57.1.52-4.57.pth, myrk
BLEU = 40.64, 71.5/50.6/35.2/24.4 (BP=0.968, ratio=0.968, hyp_len=22422, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.03.1.76-5.79.1.75-5.76.1.52-4.57.1.52-4.57.pth, rkmy
BLEU = 32.79, 59.2/40.4/26.9/18.0 (BP=1.000, ratio=1.166, hyp_len=27410, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.04.1.41-4.12.1.41-4.09.1.17-3.23.1.20-3.32.pth, myrk
BLEU = 51.51, 76.6/58.7/45.1/34.8 (BP=1.000, ratio=1.015, hyp_len=23506, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.04.1.41-4.12.1.41-4.09.1.17-3.23.1.20-3.32.pth, rkmy
BLEU = 44.11, 68.9/52.0/38.1/27.7 (BP=1.000, ratio=1.111, hyp_len=26128, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.05.1.12-3.07.1.15-3.15.0.99-2.70.1.00-2.71.pth, myrk
BLEU = 53.46, 76.2/61.0/47.7/36.8 (BP=1.000, ratio=1.077, hyp_len=24948, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.05.1.12-3.07.1.15-3.15.0.99-2.70.1.00-2.71.pth, rkmy
BLEU = 53.32, 75.8/60.4/47.4/37.2 (BP=1.000, ratio=1.054, hyp_len=24780, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.06.0.93-2.54.0.95-2.58.0.86-2.36.0.88-2.40.pth, myrk
BLEU = 55.69, 76.9/62.2/50.1/40.1 (BP=1.000, ratio=1.086, hyp_len=25152, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.06.0.93-2.54.0.95-2.58.0.86-2.36.0.88-2.40.pth, rkmy
BLEU = 58.15, 79.3/64.8/52.3/42.5 (BP=1.000, ratio=1.035, hyp_len=24330, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.07.0.81-2.26.0.83-2.29.0.79-2.21.0.81-2.24.pth, myrk
BLEU = 62.77, 82.6/69.0/57.3/47.5 (BP=1.000, ratio=1.032, hyp_len=23892, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.07.0.81-2.26.0.83-2.29.0.79-2.21.0.81-2.24.pth, rkmy
BLEU = 58.46, 78.3/64.9/52.9/43.4 (BP=1.000, ratio=1.080, hyp_len=25379, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.08.0.80-2.21.0.80-2.23.0.79-2.20.0.80-2.22.pth, myrk
BLEU = 63.63, 84.1/69.8/58.0/48.1 (BP=1.000, ratio=1.011, hyp_len=23404, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.08.0.80-2.21.0.80-2.23.0.79-2.20.0.80-2.22.pth, rkmy
BLEU = 59.28, 79.7/66.3/53.7/43.5 (BP=1.000, ratio=1.064, hyp_len=25017, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.09.0.65-1.92.0.65-1.91.0.70-2.02.0.70-2.02.pth, myrk
BLEU = 65.01, 84.2/70.8/59.6/50.3 (BP=1.000, ratio=1.027, hyp_len=23775, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.09.0.65-1.92.0.65-1.91.0.70-2.02.0.70-2.02.pth, rkmy
BLEU = 64.09, 82.7/70.3/58.8/49.4 (BP=1.000, ratio=1.045, hyp_len=24556, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.10.0.61-1.84.0.61-1.85.0.75-2.11.0.66-1.94.pth, myrk
BLEU = 64.49, 83.7/70.7/59.3/49.3 (BP=1.000, ratio=1.035, hyp_len=23978, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.10.0.61-1.84.0.61-1.85.0.75-2.11.0.66-1.94.pth, rkmy
BLEU = 62.84, 81.6/68.9/57.5/48.3 (BP=1.000, ratio=1.056, hyp_len=24836, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.11.0.58-1.78.0.59-1.80.0.67-1.96.0.64-1.90.pth, myrk
BLEU = 63.88, 83.3/70.3/58.7/48.4 (BP=1.000, ratio=1.048, hyp_len=24271, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.11.0.58-1.78.0.59-1.80.0.67-1.96.0.64-1.90.pth, rkmy
BLEU = 62.60, 80.9/68.6/57.5/48.1 (BP=1.000, ratio=1.078, hyp_len=25338, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.12.0.53-1.69.0.53-1.70.0.66-1.93.0.63-1.88.pth, myrk
BLEU = 66.40, 84.2/71.9/61.4/52.2 (BP=1.000, ratio=1.039, hyp_len=24055, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.12.0.53-1.69.0.53-1.70.0.66-1.93.0.63-1.88.pth, rkmy
BLEU = 64.68, 82.9/70.8/59.5/50.1 (BP=1.000, ratio=1.060, hyp_len=24911, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.13.0.48-1.62.0.48-1.62.0.65-1.91.0.63-1.87.pth, myrk
BLEU = 67.33, 84.8/72.7/62.3/53.4 (BP=1.000, ratio=1.033, hyp_len=23926, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.13.0.48-1.62.0.48-1.62.0.65-1.91.0.63-1.87.pth, rkmy
BLEU = 65.53, 83.3/71.5/60.4/51.3 (BP=1.000, ratio=1.053, hyp_len=24753, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.14.0.47-1.59.0.47-1.60.0.67-1.96.0.63-1.89.pth, myrk
BLEU = 66.78, 84.9/72.2/61.5/52.7 (BP=1.000, ratio=1.033, hyp_len=23929, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.14.0.47-1.59.0.47-1.60.0.67-1.96.0.63-1.89.pth, rkmy
BLEU = 64.30, 82.0/70.5/59.2/50.0 (BP=1.000, ratio=1.073, hyp_len=25216, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.15.0.44-1.55.0.44-1.55.0.65-1.91.0.59-1.80.pth, myrk
BLEU = 61.83, 79.7/67.5/56.9/47.7 (BP=1.000, ratio=1.116, hyp_len=25850, ref_len=23160)
^[[1;2BEvaluation result for the model: dsl-model-myrk.15.0.44-1.55.0.44-1.55.0.65-1.91.0.59-1.80.pth, rkmy
BLEU = 65.28, 82.1/70.8/60.3/51.8 (BP=1.000, ratio=1.080, hyp_len=25397, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.16.0.39-1.48.0.39-1.48.0.65-1.91.0.59-1.81.pth, myrk
BLEU = 67.89, 85.4/73.3/62.9/53.9 (BP=1.000, ratio=1.029, hyp_len=23823, ref_len=23160)
^[[1;2BEvaluation result for the model: dsl-model-myrk.16.0.39-1.48.0.39-1.48.0.65-1.91.0.59-1.81.pth, rkmy
BLEU = 68.18, 85.0/73.7/63.2/54.6 (BP=1.000, ratio=1.041, hyp_len=24473, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.17.0.40-1.49.0.39-1.48.0.63-1.88.0.59-1.80.pth, myrk
BLEU = 67.05, 84.2/72.2/62.0/53.6 (BP=1.000, ratio=1.043, hyp_len=24153, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.17.0.40-1.49.0.39-1.48.0.63-1.88.0.59-1.80.pth, rkmy
BLEU = 67.16, 84.3/72.8/62.1/53.4 (BP=1.000, ratio=1.052, hyp_len=24731, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.18.0.37-1.44.0.36-1.43.0.64-1.89.0.60-1.82.pth, myrk
BLEU = 68.00, 84.9/73.0/63.1/54.6 (BP=1.000, ratio=1.040, hyp_len=24095, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.18.0.37-1.44.0.36-1.43.0.64-1.89.0.60-1.82.pth, rkmy
BLEU = 68.17, 84.8/73.8/63.3/54.5 (BP=1.000, ratio=1.048, hyp_len=24628, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.19.0.37-1.44.0.37-1.45.0.62-1.85.0.57-1.76.pth, myrk
BLEU = 69.74, 86.1/74.7/64.9/56.7 (BP=1.000, ratio=1.034, hyp_len=23937, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.19.0.37-1.44.0.37-1.45.0.62-1.85.0.57-1.76.pth, rkmy
BLEU = 68.34, 84.8/73.7/63.4/55.1 (BP=1.000, ratio=1.050, hyp_len=24689, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.20.0.34-1.41.0.33-1.40.0.64-1.89.0.58-1.79.pth, myrk
BLEU = 67.97, 84.8/73.1/63.1/54.5 (BP=1.000, ratio=1.040, hyp_len=24090, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.20.0.34-1.41.0.33-1.40.0.64-1.89.0.58-1.79.pth, rkmy
BLEU = 68.11, 84.6/73.3/63.1/55.0 (BP=1.000, ratio=1.053, hyp_len=24748, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.21.0.34-1.41.0.35-1.43.0.62-1.85.0.61-1.85.pth, myrk
BLEU = 69.54, 85.8/74.4/64.8/56.6 (BP=1.000, ratio=1.033, hyp_len=23934, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.21.0.34-1.41.0.35-1.43.0.62-1.85.0.61-1.85.pth, rkmy
BLEU = 62.35, 78.0/67.3/57.7/49.9 (BP=1.000, ratio=1.138, hyp_len=26752, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.22.0.34-1.41.0.34-1.41.0.61-1.85.0.58-1.79.pth, myrk
BLEU = 69.49, 85.5/74.2/64.8/56.7 (BP=1.000, ratio=1.036, hyp_len=23991, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.22.0.34-1.41.0.34-1.41.0.61-1.85.0.58-1.79.pth, rkmy
BLEU = 68.42, 85.1/73.8/63.3/55.1 (BP=1.000, ratio=1.045, hyp_len=24577, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.23.0.32-1.38.0.34-1.41.0.63-1.88.0.56-1.75.pth, myrk
BLEU = 69.78, 85.5/74.5/65.1/57.1 (BP=1.000, ratio=1.042, hyp_len=24129, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.23.0.32-1.38.0.34-1.41.0.63-1.88.0.56-1.75.pth, rkmy
BLEU = 67.91, 84.2/73.1/63.0/54.9 (BP=1.000, ratio=1.061, hyp_len=24936, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.24.0.32-1.37.0.31-1.36.0.63-1.88.0.57-1.77.pth, myrk
BLEU = 68.11, 84.7/73.3/63.3/54.7 (BP=1.000, ratio=1.049, hyp_len=24289, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.24.0.32-1.37.0.31-1.36.0.63-1.88.0.57-1.77.pth, rkmy
BLEU = 69.09, 85.3/74.2/64.1/56.1 (BP=1.000, ratio=1.048, hyp_len=24626, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.25.0.32-1.37.0.34-1.40.0.62-1.86.0.58-1.78.pth, myrk
BLEU = 68.95, 85.4/74.0/64.2/55.7 (BP=1.000, ratio=1.042, hyp_len=24144, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.25.0.32-1.37.0.34-1.40.0.62-1.86.0.58-1.78.pth, rkmy
BLEU = 68.42, 84.8/73.6/63.4/55.3 (BP=1.000, ratio=1.050, hyp_len=24696, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.26.0.30-1.35.0.28-1.33.0.65-1.91.0.59-1.80.pth, myrk
BLEU = 68.97, 85.4/73.9/64.2/55.9 (BP=1.000, ratio=1.040, hyp_len=24085, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.26.0.30-1.35.0.28-1.33.0.65-1.91.0.59-1.80.pth, rkmy
BLEU = 69.42, 84.8/74.3/64.8/57.0 (BP=1.000, ratio=1.055, hyp_len=24803, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.27.0.28-1.33.0.29-1.33.0.64-1.89.0.58-1.78.pth, myrk
BLEU = 68.35, 84.2/73.0/63.7/55.8 (BP=1.000, ratio=1.057, hyp_len=24473, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.27.0.28-1.33.0.29-1.33.0.64-1.89.0.58-1.78.pth, rkmy
BLEU = 68.00, 84.1/73.3/63.2/54.9 (BP=1.000, ratio=1.066, hyp_len=25059, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.28.0.28-1.32.0.27-1.32.0.62-1.86.0.61-1.84.pth, myrk
BLEU = 68.54, 84.7/73.3/63.9/55.6 (BP=1.000, ratio=1.053, hyp_len=24395, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.28.0.28-1.32.0.27-1.32.0.62-1.86.0.61-1.84.pth, rkmy
BLEU = 70.44, 86.1/75.5/65.7/57.7 (BP=1.000, ratio=1.039, hyp_len=24416, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.29.0.27-1.32.0.27-1.30.0.67-1.96.0.61-1.84.pth, myrk
BLEU = 69.20, 85.4/74.1/64.5/56.1 (BP=1.000, ratio=1.030, hyp_len=23860, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.29.0.27-1.32.0.27-1.30.0.67-1.96.0.61-1.84.pth, rkmy
BLEU = 68.51, 85.0/73.7/63.5/55.3 (BP=1.000, ratio=1.051, hyp_len=24709, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.30.0.26-1.29.0.25-1.29.0.63-1.88.0.61-1.84.pth, myrk
BLEU = 69.87, 85.6/74.6/65.2/57.2 (BP=1.000, ratio=1.040, hyp_len=24080, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.30.0.26-1.29.0.25-1.29.0.63-1.88.0.61-1.84.pth, rkmy
BLEU = 67.12, 82.7/72.0/62.4/54.6 (BP=1.000, ratio=1.084, hyp_len=25483, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.31.0.25-1.28.0.25-1.28.0.64-1.91.0.60-1.81.pth, myrk
BLEU = 69.81, 85.4/74.5/65.2/57.2 (BP=1.000, ratio=1.036, hyp_len=23985, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.31.0.25-1.28.0.25-1.28.0.64-1.91.0.60-1.81.pth, rkmy
BLEU = 68.16, 84.5/73.5/63.3/54.9 (BP=1.000, ratio=1.057, hyp_len=24850, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.32.0.25-1.28.0.25-1.28.0.65-1.92.0.60-1.81.pth, myrk
BLEU = 69.59, 85.5/74.3/64.9/56.9 (BP=1.000, ratio=1.033, hyp_len=23929, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.32.0.25-1.28.0.25-1.28.0.65-1.92.0.60-1.81.pth, rkmy
BLEU = 68.55, 84.7/73.7/63.8/55.5 (BP=1.000, ratio=1.054, hyp_len=24782, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.33.0.23-1.26.0.23-1.26.0.67-1.96.0.61-1.84.pth, myrk
BLEU = 69.56, 85.6/74.4/64.9/56.7 (BP=1.000, ratio=1.035, hyp_len=23981, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.33.0.23-1.26.0.23-1.26.0.67-1.96.0.61-1.84.pth, rkmy
BLEU = 64.64, 80.2/69.7/60.0/52.0 (BP=1.000, ratio=1.113, hyp_len=26166, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.34.0.24-1.27.0.24-1.27.0.65-1.91.0.59-1.81.pth, myrk
BLEU = 70.34, 86.1/75.0/65.7/57.7 (BP=1.000, ratio=1.032, hyp_len=23897, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.34.0.24-1.27.0.24-1.27.0.65-1.91.0.59-1.81.pth, rkmy
BLEU = 67.45, 83.9/72.7/62.5/54.2 (BP=1.000, ratio=1.063, hyp_len=24991, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.35.0.22-1.25.0.22-1.24.0.65-1.91.0.60-1.82.pth, myrk
BLEU = 70.40, 85.8/75.0/65.8/58.0 (BP=1.000, ratio=1.041, hyp_len=24101, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.35.0.22-1.25.0.22-1.24.0.65-1.91.0.60-1.82.pth, rkmy
BLEU = 69.48, 85.3/74.5/64.6/56.8 (BP=1.000, ratio=1.057, hyp_len=24844, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.36.0.22-1.25.0.22-1.24.0.66-1.93.0.62-1.86.pth, myrk
BLEU = 70.11, 85.7/74.8/65.5/57.5 (BP=1.000, ratio=1.046, hyp_len=24224, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.36.0.22-1.25.0.22-1.24.0.66-1.93.0.62-1.86.pth, rkmy
BLEU = 66.81, 83.7/72.2/61.8/53.4 (BP=1.000, ratio=1.065, hyp_len=25029, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.37.0.22-1.25.0.23-1.25.0.66-1.94.0.58-1.79.pth, myrk
BLEU = 69.26, 85.1/74.0/64.6/56.5 (BP=1.000, ratio=1.049, hyp_len=24294, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.37.0.22-1.25.0.23-1.25.0.66-1.94.0.58-1.79.pth, rkmy
BLEU = 69.13, 85.0/74.3/64.3/56.2 (BP=1.000, ratio=1.051, hyp_len=24719, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.38.0.21-1.23.0.21-1.23.0.66-1.93.0.59-1.81.pth, myrk
BLEU = 69.99, 85.6/74.6/65.4/57.4 (BP=1.000, ratio=1.044, hyp_len=24182, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.38.0.21-1.23.0.21-1.23.0.66-1.93.0.59-1.81.pth, rkmy
BLEU = 67.26, 83.7/72.5/62.3/54.1 (BP=1.000, ratio=1.071, hyp_len=25180, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.39.0.22-1.24.0.21-1.23.0.66-1.94.0.60-1.83.pth, myrk
BLEU = 69.25, 84.9/73.9/64.7/56.7 (BP=1.000, ratio=1.050, hyp_len=24327, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.39.0.22-1.24.0.21-1.23.0.66-1.94.0.60-1.83.pth, rkmy
BLEU = 69.62, 85.3/74.6/64.8/57.0 (BP=1.000, ratio=1.054, hyp_len=24776, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.40.0.20-1.23.0.21-1.23.0.66-1.93.0.61-1.85.pth, myrk
BLEU = 70.34, 85.9/74.9/65.7/57.9 (BP=1.000, ratio=1.042, hyp_len=24134, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.40.0.20-1.23.0.21-1.23.0.66-1.93.0.61-1.85.pth, rkmy
BLEU = 69.23, 84.9/74.3/64.5/56.5 (BP=1.000, ratio=1.053, hyp_len=24751, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.41.0.20-1.22.0.19-1.21.0.67-1.95.0.61-1.83.pth, myrk
BLEU = 69.33, 85.0/74.1/64.8/56.7 (BP=1.000, ratio=1.050, hyp_len=24324, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.41.0.20-1.22.0.19-1.21.0.67-1.95.0.61-1.83.pth, rkmy
BLEU = 70.28, 85.8/75.3/65.6/57.6 (BP=1.000, ratio=1.047, hyp_len=24620, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.42.0.19-1.21.0.19-1.21.0.68-1.97.0.60-1.82.pth, myrk
BLEU = 69.82, 85.4/74.5/65.3/57.3 (BP=1.000, ratio=1.044, hyp_len=24184, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.42.0.19-1.21.0.19-1.21.0.68-1.97.0.60-1.82.pth, rkmy
BLEU = 69.67, 85.3/74.7/64.9/57.0 (BP=1.000, ratio=1.057, hyp_len=24852, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.43.0.20-1.22.0.20-1.22.0.68-1.98.0.60-1.82.pth, myrk
BLEU = 70.14, 85.8/74.8/65.5/57.6 (BP=1.000, ratio=1.036, hyp_len=23995, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.43.0.20-1.22.0.20-1.22.0.68-1.98.0.60-1.82.pth, rkmy
BLEU = 68.33, 84.5/73.5/63.4/55.3 (BP=1.000, ratio=1.063, hyp_len=24981, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.44.0.19-1.21.0.20-1.22.0.69-1.98.0.60-1.83.pth, myrk
BLEU = 70.83, 85.9/75.2/66.4/58.8 (BP=1.000, ratio=1.034, hyp_len=23943, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.44.0.19-1.21.0.20-1.22.0.69-1.98.0.60-1.83.pth, rkmy
BLEU = 69.13, 85.0/74.1/64.3/56.4 (BP=1.000, ratio=1.053, hyp_len=24747, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.45.0.19-1.21.0.19-1.21.0.68-1.97.0.61-1.85.pth, myrk
BLEU = 69.47, 84.8/74.0/64.9/57.1 (BP=1.000, ratio=1.052, hyp_len=24361, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.45.0.19-1.21.0.19-1.21.0.68-1.97.0.61-1.85.pth, rkmy
BLEU = 68.20, 84.1/73.3/63.4/55.3 (BP=1.000, ratio=1.064, hyp_len=25017, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.46.0.18-1.19.0.18-1.20.0.69-1.99.0.61-1.85.pth, myrk
BLEU = 70.29, 85.8/74.9/65.7/57.9 (BP=1.000, ratio=1.038, hyp_len=24034, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.46.0.18-1.19.0.18-1.20.0.69-1.99.0.61-1.85.pth, rkmy
BLEU = 68.48, 84.6/73.8/63.7/55.3 (BP=1.000, ratio=1.063, hyp_len=24982, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.47.0.18-1.19.0.18-1.19.0.69-1.99.0.62-1.85.pth, myrk
BLEU = 70.02, 85.3/74.6/65.5/57.7 (BP=1.000, ratio=1.046, hyp_len=24219, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.47.0.18-1.19.0.18-1.19.0.69-1.99.0.62-1.85.pth, rkmy
BLEU = 70.08, 85.5/74.9/65.3/57.6 (BP=1.000, ratio=1.048, hyp_len=24639, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.48.0.18-1.20.0.18-1.19.0.67-1.96.0.61-1.84.pth, myrk
BLEU = 70.18, 85.5/74.7/65.6/57.9 (BP=1.000, ratio=1.042, hyp_len=24140, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.48.0.18-1.20.0.18-1.19.0.67-1.96.0.61-1.84.pth, rkmy
BLEU = 68.93, 84.7/74.0/64.2/56.1 (BP=1.000, ratio=1.060, hyp_len=24916, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.49.0.18-1.20.0.19-1.20.0.69-2.00.0.64-1.89.pth, myrk
BLEU = 71.02, 86.3/75.5/66.4/58.8 (BP=1.000, ratio=1.034, hyp_len=23948, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.49.0.18-1.20.0.19-1.20.0.69-2.00.0.64-1.89.pth, rkmy
BLEU = 70.55, 85.9/75.3/65.8/58.2 (BP=1.000, ratio=1.045, hyp_len=24576, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.50.0.17-1.19.0.17-1.18.0.69-1.99.0.62-1.87.pth, myrk
BLEU = 70.45, 85.9/75.1/65.9/57.9 (BP=1.000, ratio=1.046, hyp_len=24220, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.50.0.17-1.19.0.17-1.18.0.69-1.99.0.62-1.87.pth, rkmy
BLEU = 70.60, 85.8/75.5/66.0/58.1 (BP=1.000, ratio=1.047, hyp_len=24625, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.51.0.16-1.18.0.16-1.17.0.70-2.02.0.62-1.87.pth, myrk
BLEU = 70.40, 85.6/74.9/65.9/58.1 (BP=1.000, ratio=1.043, hyp_len=24154, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.51.0.16-1.18.0.16-1.17.0.70-2.02.0.62-1.87.pth, rkmy
BLEU = 70.43, 85.7/75.4/65.8/57.8 (BP=1.000, ratio=1.049, hyp_len=24652, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.52.0.16-1.18.0.16-1.17.0.72-2.05.0.66-1.94.pth, myrk
BLEU = 69.84, 85.2/74.5/65.3/57.3 (BP=1.000, ratio=1.041, hyp_len=24115, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.52.0.16-1.18.0.16-1.17.0.72-2.05.0.66-1.94.pth, rkmy
BLEU = 70.72, 85.9/75.6/66.1/58.3 (BP=1.000, ratio=1.048, hyp_len=24635, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.53.0.17-1.18.0.16-1.17.0.69-1.99.0.62-1.86.pth, myrk
BLEU = 70.43, 85.8/75.0/65.9/58.0 (BP=1.000, ratio=1.038, hyp_len=24050, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.53.0.17-1.18.0.16-1.17.0.69-1.99.0.62-1.86.pth, rkmy
BLEU = 70.06, 85.6/74.8/65.3/57.6 (BP=1.000, ratio=1.048, hyp_len=24628, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.54.0.15-1.16.0.15-1.16.0.70-2.01.0.63-1.89.pth, myrk
BLEU = 70.54, 85.7/75.0/66.0/58.3 (BP=1.000, ratio=1.043, hyp_len=24154, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.54.0.15-1.16.0.15-1.16.0.70-2.01.0.63-1.89.pth, rkmy
BLEU = 68.19, 84.4/73.4/63.3/55.1 (BP=1.000, ratio=1.061, hyp_len=24934, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.55.0.16-1.17.0.16-1.17.0.70-2.02.0.65-1.91.pth, myrk
BLEU = 70.79, 85.8/75.1/66.2/58.8 (BP=1.000, ratio=1.035, hyp_len=23975, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.55.0.16-1.17.0.16-1.17.0.70-2.02.0.65-1.91.pth, rkmy
BLEU = 69.95, 85.2/74.8/65.3/57.6 (BP=1.000, ratio=1.054, hyp_len=24774, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.56.0.15-1.17.0.15-1.16.0.71-2.04.0.65-1.92.pth, myrk
BLEU = 69.94, 85.6/74.6/65.3/57.3 (BP=1.000, ratio=1.046, hyp_len=24222, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.56.0.15-1.17.0.15-1.16.0.71-2.04.0.65-1.92.pth, rkmy
BLEU = 69.27, 85.0/74.3/64.4/56.6 (BP=1.000, ratio=1.054, hyp_len=24790, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.57.0.16-1.17.0.15-1.17.0.71-2.04.0.66-1.93.pth, myrk
BLEU = 69.73, 85.1/74.4/65.2/57.2 (BP=1.000, ratio=1.052, hyp_len=24366, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.57.0.16-1.17.0.15-1.17.0.71-2.04.0.66-1.93.pth, rkmy
BLEU = 68.15, 84.4/73.3/63.2/55.2 (BP=1.000, ratio=1.063, hyp_len=24981, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.58.0.15-1.16.0.14-1.15.0.72-2.06.0.64-1.90.pth, myrk
BLEU = 70.06, 85.3/74.5/65.6/57.8 (BP=1.000, ratio=1.043, hyp_len=24163, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.58.0.15-1.16.0.14-1.15.0.72-2.06.0.64-1.90.pth, rkmy
BLEU = 70.59, 85.9/75.4/65.9/58.2 (BP=1.000, ratio=1.045, hyp_len=24574, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.59.0.14-1.15.0.15-1.16.0.71-2.03.0.65-1.92.pth, myrk
BLEU = 69.57, 85.3/74.2/64.9/57.0 (BP=1.000, ratio=1.046, hyp_len=24224, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.59.0.14-1.15.0.15-1.16.0.71-2.03.0.65-1.92.pth, rkmy
BLEU = 69.77, 85.4/74.7/65.0/57.2 (BP=1.000, ratio=1.049, hyp_len=24658, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.60.0.15-1.16.0.14-1.15.0.75-2.11.0.65-1.91.pth, myrk
BLEU = 70.70, 86.0/75.3/66.2/58.3 (BP=1.000, ratio=1.039, hyp_len=24068, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.60.0.15-1.16.0.14-1.15.0.75-2.11.0.65-1.91.pth, rkmy
BLEU = 69.39, 85.1/74.4/64.6/56.7 (BP=1.000, ratio=1.054, hyp_len=24779, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.61.0.14-1.15.0.14-1.15.0.75-2.11.0.65-1.92.pth, myrk
BLEU = 70.38, 85.8/75.0/65.8/57.9 (BP=1.000, ratio=1.039, hyp_len=24064, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.61.0.14-1.15.0.14-1.15.0.75-2.11.0.65-1.92.pth, rkmy
BLEU = 69.80, 85.2/74.7/65.2/57.2 (BP=1.000, ratio=1.055, hyp_len=24806, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.62.0.15-1.16.0.15-1.16.0.72-2.05.0.66-1.94.pth, myrk
BLEU = 71.15, 85.9/75.6/66.8/59.1 (BP=1.000, ratio=1.041, hyp_len=24098, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.62.0.15-1.16.0.15-1.16.0.72-2.05.0.66-1.94.pth, rkmy
BLEU = 69.57, 85.1/74.6/64.8/56.9 (BP=1.000, ratio=1.058, hyp_len=24878, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.63.0.14-1.15.0.14-1.15.0.73-2.08.0.65-1.91.pth, myrk
BLEU = 68.50, 84.6/73.3/63.9/55.6 (BP=1.000, ratio=1.055, hyp_len=24438, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.63.0.14-1.15.0.14-1.15.0.73-2.08.0.65-1.91.pth, rkmy
BLEU = 69.88, 85.2/74.7/65.2/57.5 (BP=1.000, ratio=1.055, hyp_len=24804, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.64.0.14-1.15.0.14-1.15.0.75-2.12.0.66-1.93.pth, myrk
BLEU = 70.71, 85.9/75.2/66.2/58.4 (BP=1.000, ratio=1.041, hyp_len=24109, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.64.0.14-1.15.0.14-1.15.0.75-2.12.0.66-1.93.pth, rkmy
BLEU = 69.29, 85.0/74.3/64.5/56.5 (BP=1.000, ratio=1.058, hyp_len=24874, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.65.0.13-1.14.0.13-1.14.0.74-2.09.0.66-1.93.pth, myrk
BLEU = 69.35, 84.8/74.0/64.8/56.9 (BP=1.000, ratio=1.053, hyp_len=24396, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.65.0.13-1.14.0.13-1.14.0.74-2.09.0.66-1.93.pth, rkmy
BLEU = 69.79, 85.4/74.7/65.1/57.2 (BP=1.000, ratio=1.052, hyp_len=24732, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.66.0.14-1.15.0.14-1.15.0.74-2.09.0.66-1.93.pth, myrk
BLEU = 70.82, 86.1/75.2/66.4/58.6 (BP=1.000, ratio=1.035, hyp_len=23982, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.66.0.14-1.15.0.14-1.15.0.74-2.09.0.66-1.93.pth, rkmy
BLEU = 69.67, 85.1/74.6/65.0/57.1 (BP=1.000, ratio=1.056, hyp_len=24833, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.67.0.14-1.14.0.13-1.14.0.75-2.11.0.66-1.93.pth, myrk
BLEU = 70.30, 85.7/74.8/65.8/58.0 (BP=1.000, ratio=1.046, hyp_len=24224, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.67.0.14-1.14.0.13-1.14.0.75-2.11.0.66-1.93.pth, rkmy
BLEU = 68.98, 84.8/73.9/64.2/56.3 (BP=1.000, ratio=1.059, hyp_len=24891, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.68.0.13-1.14.0.13-1.14.0.72-2.05.0.67-1.95.pth, myrk
BLEU = 68.61, 84.2/73.3/64.1/56.1 (BP=1.000, ratio=1.059, hyp_len=24517, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.68.0.13-1.14.0.13-1.14.0.72-2.05.0.67-1.95.pth, rkmy
BLEU = 68.72, 84.4/73.6/64.0/56.1 (BP=1.000, ratio=1.061, hyp_len=24939, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.69.0.13-1.14.0.12-1.13.0.74-2.10.0.68-1.97.pth, myrk
BLEU = 69.81, 85.2/74.4/65.3/57.4 (BP=1.000, ratio=1.044, hyp_len=24170, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.69.0.13-1.14.0.12-1.13.0.74-2.10.0.68-1.97.pth, rkmy
BLEU = 70.55, 85.6/75.3/66.0/58.3 (BP=1.000, ratio=1.051, hyp_len=24704, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.70.0.13-1.14.0.13-1.14.0.78-2.17.0.68-1.97.pth, myrk
BLEU = 69.32, 85.2/74.1/64.7/56.5 (BP=1.000, ratio=1.052, hyp_len=24363, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.70.0.13-1.14.0.13-1.14.0.78-2.17.0.68-1.97.pth, rkmy
BLEU = 69.16, 84.9/74.1/64.3/56.5 (BP=1.000, ratio=1.060, hyp_len=24921, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.71.0.13-1.13.0.13-1.13.0.74-2.11.0.66-1.93.pth, myrk
BLEU = 69.49, 85.1/74.2/64.9/56.9 (BP=1.000, ratio=1.053, hyp_len=24397, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.71.0.13-1.13.0.13-1.13.0.74-2.11.0.66-1.93.pth, rkmy
BLEU = 69.95, 85.3/74.8/65.3/57.5 (BP=1.000, ratio=1.053, hyp_len=24752, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.72.0.13-1.14.0.13-1.13.0.76-2.13.0.66-1.94.pth, myrk
BLEU = 69.48, 85.0/74.1/65.0/56.9 (BP=1.000, ratio=1.049, hyp_len=24300, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.72.0.13-1.14.0.13-1.13.0.76-2.13.0.66-1.94.pth, rkmy
BLEU = 70.52, 85.7/75.3/65.9/58.2 (BP=1.000, ratio=1.047, hyp_len=24606, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.73.0.13-1.14.0.13-1.13.0.76-2.14.0.66-1.93.pth, myrk
BLEU = 70.42, 85.5/74.9/66.0/58.2 (BP=1.000, ratio=1.042, hyp_len=24134, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.73.0.13-1.14.0.13-1.13.0.76-2.14.0.66-1.93.pth, rkmy
BLEU = 68.24, 84.2/73.2/63.4/55.5 (BP=1.000, ratio=1.065, hyp_len=25037, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.74.0.12-1.13.0.12-1.12.0.74-2.10.0.67-1.95.pth, myrk
BLEU = 70.29, 85.8/74.8/65.7/57.9 (BP=1.000, ratio=1.040, hyp_len=24095, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.74.0.12-1.13.0.12-1.12.0.74-2.10.0.67-1.95.pth, rkmy
BLEU = 68.76, 84.5/73.8/64.0/56.0 (BP=1.000, ratio=1.061, hyp_len=24944, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.75.0.12-1.13.0.12-1.13.0.77-2.17.0.68-1.96.pth, myrk
BLEU = 69.52, 84.8/74.0/65.0/57.2 (BP=1.000, ratio=1.049, hyp_len=24297, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.75.0.12-1.13.0.12-1.13.0.77-2.17.0.68-1.96.pth, rkmy
BLEU = 69.85, 85.3/74.7/65.1/57.4 (BP=1.000, ratio=1.051, hyp_len=24718, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.76.0.12-1.13.0.12-1.13.0.79-2.20.0.67-1.95.pth, myrk
BLEU = 68.69, 84.1/73.3/64.1/56.3 (BP=1.000, ratio=1.060, hyp_len=24560, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.76.0.12-1.13.0.12-1.13.0.79-2.20.0.67-1.95.pth, rkmy
BLEU = 71.07, 86.1/75.7/66.4/59.0 (BP=1.000, ratio=1.044, hyp_len=24549, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.77.0.12-1.12.0.11-1.12.0.77-2.16.0.66-1.93.pth, myrk
BLEU = 69.84, 85.4/74.5/65.3/57.2 (BP=1.000, ratio=1.045, hyp_len=24193, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.77.0.12-1.12.0.11-1.12.0.77-2.16.0.66-1.93.pth, rkmy
BLEU = 69.97, 85.3/74.7/65.3/57.6 (BP=1.000, ratio=1.055, hyp_len=24810, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.78.0.12-1.13.0.12-1.13.0.77-2.16.0.68-1.96.pth, myrk
BLEU = 69.80, 85.4/74.5/65.3/57.1 (BP=1.000, ratio=1.045, hyp_len=24198, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.78.0.12-1.13.0.12-1.13.0.77-2.16.0.68-1.96.pth, rkmy
BLEU = 69.63, 85.0/74.3/64.9/57.3 (BP=1.000, ratio=1.060, hyp_len=24915, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.79.0.11-1.12.0.12-1.13.0.79-2.20.0.68-1.97.pth, myrk
BLEU = 69.49, 85.1/74.1/64.9/57.0 (BP=1.000, ratio=1.046, hyp_len=24221, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.79.0.11-1.12.0.12-1.13.0.79-2.20.0.68-1.97.pth, rkmy
BLEU = 69.82, 85.5/74.9/65.1/57.0 (BP=1.000, ratio=1.056, hyp_len=24822, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.80.0.11-1.12.0.11-1.12.0.79-2.19.0.70-2.01.pth, myrk
BLEU = 70.05, 85.3/74.5/65.5/57.8 (BP=1.000, ratio=1.048, hyp_len=24267, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.80.0.11-1.12.0.11-1.12.0.79-2.19.0.70-2.01.pth, rkmy
BLEU = 69.91, 85.4/74.7/65.1/57.5 (BP=1.000, ratio=1.055, hyp_len=24792, ref_len=23509)
```

#### Warmup-Epoch 20, Total Epoch 90

```
Epoch 1 - |param|=9.10e+02 |g_param|=1.68e+05 loss_x2y=3.5104e+00 ppl_x2y=33.46 loss_y2x=3.5526e+00 ppl_y2x=34.90 dual_loss=0.0000e+00
Validation X2Y - loss=2.9182e+00 ppl=18.51 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=2.9934e+00 ppl=19.95 best_loss=inf best_ppl=inf
Epoch 2 - |param|=9.11e+02 |g_param|=1.87e+05 loss_x2y=2.3667e+00 ppl_x2y=10.66 loss_y2x=2.3843e+00 ppl_y2x=10.85 dual_loss=0.0000e+00
Validation X2Y - loss=1.9821e+00 ppl=7.26 best_loss=2.9182e+00 best_ppl=18.51                                           
Validation Y2X - loss=1.9935e+00 ppl=7.34 best_loss=2.9934e+00 best_ppl=19.95
Epoch 3 - |param|=9.11e+02 |g_param|=2.45e+05 loss_x2y=1.8094e+00 ppl_x2y=6.11 loss_y2x=1.7731e+00 ppl_y2x=5.89 dual_loss=0.0000e+00
Validation X2Y - loss=1.5168e+00 ppl=4.56 best_loss=1.9821e+00 best_ppl=7.26                                            
Validation Y2X - loss=1.4703e+00 ppl=4.35 best_loss=1.9935e+00 best_ppl=7.34
Epoch 4 - |param|=9.12e+02 |g_param|=2.31e+05 loss_x2y=1.3836e+00 ppl_x2y=3.99 loss_y2x=1.3909e+00 ppl_y2x=4.02 dual_loss=0.0000e+00
Validation X2Y - loss=1.1176e+00 ppl=3.06 best_loss=1.5168e+00 best_ppl=4.56                                            
Validation Y2X - loss=1.1739e+00 ppl=3.23 best_loss=1.4703e+00 best_ppl=4.35
Epoch 5 - |param|=9.12e+02 |g_param|=2.39e+05 loss_x2y=1.1285e+00 ppl_x2y=3.09 loss_y2x=1.0917e+00 ppl_y2x=2.98 dual_loss=0.0000e+00
Validation X2Y - loss=9.7086e-01 ppl=2.64 best_loss=1.1176e+00 best_ppl=3.06                                            
Validation Y2X - loss=9.5889e-01 ppl=2.61 best_loss=1.1739e+00 best_ppl=3.23
Epoch 6 - |param|=9.12e+02 |g_param|=2.58e+05 loss_x2y=9.6399e-01 ppl_x2y=2.62 loss_y2x=9.7142e-01 ppl_y2x=2.64 dual_loss=0.0000e+00
Validation X2Y - loss=8.6937e-01 ppl=2.39 best_loss=9.7086e-01 best_ppl=2.64                                            
Validation Y2X - loss=8.7943e-01 ppl=2.41 best_loss=9.5889e-01 best_ppl=2.61
Epoch 7 - |param|=9.13e+02 |g_param|=2.34e+05 loss_x2y=8.5893e-01 ppl_x2y=2.36 loss_y2x=8.6068e-01 ppl_y2x=2.36 dual_loss=0.0000e+00
Validation X2Y - loss=7.9646e-01 ppl=2.22 best_loss=8.6937e-01 best_ppl=2.39                                            
Validation Y2X - loss=7.9564e-01 ppl=2.22 best_loss=8.7943e-01 best_ppl=2.41
Epoch 8 - |param|=9.13e+02 |g_param|=2.29e+05 loss_x2y=7.5583e-01 ppl_x2y=2.13 loss_y2x=7.5806e-01 ppl_y2x=2.13 dual_loss=0.0000e+00
Validation X2Y - loss=7.4017e-01 ppl=2.10 best_loss=7.9646e-01 best_ppl=2.22                                            
Validation Y2X - loss=7.4884e-01 ppl=2.11 best_loss=7.9564e-01 best_ppl=2.22
Epoch 9 - |param|=9.13e+02 |g_param|=2.17e+05 loss_x2y=6.7373e-01 ppl_x2y=1.96 loss_y2x=6.6708e-01 ppl_y2x=1.95 dual_loss=0.0000e+00
Validation X2Y - loss=7.2565e-01 ppl=2.07 best_loss=7.4017e-01 best_ppl=2.10                                            
Validation Y2X - loss=7.1439e-01 ppl=2.04 best_loss=7.4884e-01 best_ppl=2.11
Epoch 10 - |param|=9.13e+02 |g_param|=2.42e+05 loss_x2y=6.5393e-01 ppl_x2y=1.92 loss_y2x=6.3853e-01 ppl_y2x=1.89 dual_loss=0.0000e+00
Validation X2Y - loss=7.1289e-01 ppl=2.04 best_loss=7.2565e-01 best_ppl=2.07                                            
Validation Y2X - loss=6.8324e-01 ppl=1.98 best_loss=7.1439e-01 best_ppl=2.04
Epoch 11 - |param|=9.14e+02 |g_param|=2.13e+05 loss_x2y=5.5539e-01 ppl_x2y=1.74 loss_y2x=5.5112e-01 ppl_y2x=1.74 dual_loss=0.0000e+00
Validation X2Y - loss=7.0917e-01 ppl=2.03 best_loss=7.1289e-01 best_ppl=2.04                                            
Validation Y2X - loss=7.5833e-01 ppl=2.13 best_loss=6.8324e-01 best_ppl=1.98
Epoch 12 - |param|=9.14e+02 |g_param|=2.30e+05 loss_x2y=5.3571e-01 ppl_x2y=1.71 loss_y2x=5.3913e-01 ppl_y2x=1.71 dual_loss=0.0000e+00
Validation X2Y - loss=6.9634e-01 ppl=2.01 best_loss=7.0917e-01 best_ppl=2.03                                            
Validation Y2X - loss=6.8405e-01 ppl=1.98 best_loss=6.8324e-01 best_ppl=1.98
Epoch 13 - |param|=9.14e+02 |g_param|=2.24e+05 loss_x2y=4.9857e-01 ppl_x2y=1.65 loss_y2x=4.8909e-01 ppl_y2x=1.63 dual_loss=0.0000e+00
Validation X2Y - loss=6.5640e-01 ppl=1.93 best_loss=6.9634e-01 best_ppl=2.01                                            
Validation Y2X - loss=6.4193e-01 ppl=1.90 best_loss=6.8324e-01 best_ppl=1.98
Epoch 14 - |param|=9.15e+02 |g_param|=1.99e+05 loss_x2y=4.4217e-01 ppl_x2y=1.56 loss_y2x=4.4314e-01 ppl_y2x=1.56 dual_loss=0.0000e+00
Validation X2Y - loss=6.7546e-01 ppl=1.96 best_loss=6.5640e-01 best_ppl=1.93                                            
Validation Y2X - loss=6.2155e-01 ppl=1.86 best_loss=6.4193e-01 best_ppl=1.90
Epoch 15 - |param|=9.15e+02 |g_param|=2.10e+05 loss_x2y=4.3357e-01 ppl_x2y=1.54 loss_y2x=4.3322e-01 ppl_y2x=1.54 dual_loss=0.0000e+00
Validation X2Y - loss=6.7365e-01 ppl=1.96 best_loss=6.5640e-01 best_ppl=1.93                                            
Validation Y2X - loss=6.1662e-01 ppl=1.85 best_loss=6.2155e-01 best_ppl=1.86
Epoch 16 - |param|=9.15e+02 |g_param|=1.63e+05 loss_x2y=4.2363e-01 ppl_x2y=1.53 loss_y2x=4.2577e-01 ppl_y2x=1.53 dual_loss=0.0000e+00
Validation X2Y - loss=6.6396e-01 ppl=1.94 best_loss=6.5640e-01 best_ppl=1.93                                            
Validation Y2X - loss=6.0970e-01 ppl=1.84 best_loss=6.1662e-01 best_ppl=1.85
Epoch 17 - |param|=9.16e+02 |g_param|=1.48e+05 loss_x2y=3.9427e-01 ppl_x2y=1.48 loss_y2x=3.9830e-01 ppl_y2x=1.49 dual_loss=0.0000e+00
Validation X2Y - loss=6.5877e-01 ppl=1.93 best_loss=6.5640e-01 best_ppl=1.93                                            
Validation Y2X - loss=5.9655e-01 ppl=1.82 best_loss=6.0970e-01 best_ppl=1.84
Epoch 18 - |param|=9.16e+02 |g_param|=1.45e+05 loss_x2y=3.6916e-01 ppl_x2y=1.45 loss_y2x=3.7280e-01 ppl_y2x=1.45 dual_loss=0.0000e+00
Validation X2Y - loss=6.6728e-01 ppl=1.95 best_loss=6.5640e-01 best_ppl=1.93                                            
Validation Y2X - loss=6.0635e-01 ppl=1.83 best_loss=5.9655e-01 best_ppl=1.82
Epoch 19 - |param|=9.16e+02 |g_param|=1.54e+05 loss_x2y=3.5949e-01 ppl_x2y=1.43 loss_y2x=3.4371e-01 ppl_y2x=1.41 dual_loss=0.0000e+00
Validation X2Y - loss=6.6357e-01 ppl=1.94 best_loss=6.5640e-01 best_ppl=1.93                                            
Validation Y2X - loss=5.9234e-01 ppl=1.81 best_loss=5.9655e-01 best_ppl=1.82
Epoch 20 - |param|=9.17e+02 |g_param|=1.45e+05 loss_x2y=3.4129e-01 ppl_x2y=1.41 loss_y2x=3.3829e-01 ppl_y2x=1.40 dual_loss=0.0000e+00
Validation X2Y - loss=6.7553e-01 ppl=1.97 best_loss=6.5640e-01 best_ppl=1.93                                            
Validation Y2X - loss=5.7130e-01 ppl=1.77 best_loss=5.9234e-01 best_ppl=1.81
Epoch 21 - |param|=9.17e+02 |g_param|=2.12e+05 loss_x2y=3.7422e-01 ppl_x2y=1.45 loss_y2x=3.6236e-01 ppl_y2x=1.44 dual_loss=4.8727e-01
Validation X2Y - loss=6.5621e-01 ppl=1.93 best_loss=6.5640e-01 best_ppl=1.93                                            
Validation Y2X - loss=5.7755e-01 ppl=1.78 best_loss=5.7130e-01 best_ppl=1.77
Epoch 22 - |param|=9.18e+02 |g_param|=2.49e+05 loss_x2y=3.4745e-01 ppl_x2y=1.42 loss_y2x=3.5612e-01 ppl_y2x=1.43 dual_loss=6.2044e-01
Validation X2Y - loss=6.5102e-01 ppl=1.92 best_loss=6.5621e-01 best_ppl=1.93                                            
Validation Y2X - loss=5.9566e-01 ppl=1.81 best_loss=5.7130e-01 best_ppl=1.77
Epoch 23 - |param|=9.18e+02 |g_param|=2.53e+05 loss_x2y=3.3343e-01 ppl_x2y=1.40 loss_y2x=3.3074e-01 ppl_y2x=1.39 dual_loss=4.2742e-01
Validation X2Y - loss=6.5787e-01 ppl=1.93 best_loss=6.5102e-01 best_ppl=1.92                                            
Validation Y2X - loss=5.7263e-01 ppl=1.77 best_loss=5.7130e-01 best_ppl=1.77
Epoch 24 - |param|=9.18e+02 |g_param|=2.50e+05 loss_x2y=3.1468e-01 ppl_x2y=1.37 loss_y2x=3.1191e-01 ppl_y2x=1.37 dual_loss=3.4720e-01
Validation X2Y - loss=6.5762e-01 ppl=1.93 best_loss=6.5102e-01 best_ppl=1.92                                            
Validation Y2X - loss=5.8932e-01 ppl=1.80 best_loss=5.7130e-01 best_ppl=1.77
Epoch 25 - |param|=9.19e+02 |g_param|=2.29e+05 loss_x2y=3.1110e-01 ppl_x2y=1.36 loss_y2x=3.1300e-01 ppl_y2x=1.37 dual_loss=4.2950e-01
Validation X2Y - loss=6.3695e-01 ppl=1.89 best_loss=6.5102e-01 best_ppl=1.92                                            
Validation Y2X - loss=5.7653e-01 ppl=1.78 best_loss=5.7130e-01 best_ppl=1.77
Epoch 26 - |param|=9.19e+02 |g_param|=2.53e+05 loss_x2y=3.0855e-01 ppl_x2y=1.36 loss_y2x=2.9095e-01 ppl_y2x=1.34 dual_loss=3.3653e-01
Validation X2Y - loss=6.4586e-01 ppl=1.91 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.7204e-01 ppl=1.77 best_loss=5.7130e-01 best_ppl=1.77
Epoch 27 - |param|=9.20e+02 |g_param|=2.44e+05 loss_x2y=2.9202e-01 ppl_x2y=1.34 loss_y2x=2.8550e-01 ppl_y2x=1.33 dual_loss=3.8423e-01
Validation X2Y - loss=6.3932e-01 ppl=1.90 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9149e-01 ppl=1.81 best_loss=5.7130e-01 best_ppl=1.77
Epoch 28 - |param|=9.20e+02 |g_param|=2.48e+05 loss_x2y=2.9284e-01 ppl_x2y=1.34 loss_y2x=2.8438e-01 ppl_y2x=1.33 dual_loss=3.5607e-01
Validation X2Y - loss=6.7035e-01 ppl=1.95 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9217e-01 ppl=1.81 best_loss=5.7130e-01 best_ppl=1.77
Epoch 29 - |param|=9.20e+02 |g_param|=2.28e+05 loss_x2y=2.7230e-01 ppl_x2y=1.31 loss_y2x=2.6629e-01 ppl_y2x=1.31 dual_loss=3.4998e-01
Validation X2Y - loss=6.4102e-01 ppl=1.90 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.5905e-01 ppl=1.75 best_loss=5.7130e-01 best_ppl=1.77
Epoch 30 - |param|=9.21e+02 |g_param|=2.46e+05 loss_x2y=2.6658e-01 ppl_x2y=1.31 loss_y2x=2.5481e-01 ppl_y2x=1.29 dual_loss=3.4488e-01
Validation X2Y - loss=6.5266e-01 ppl=1.92 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.6710e-01 ppl=1.76 best_loss=5.5905e-01 best_ppl=1.75
Epoch 31 - |param|=9.21e+02 |g_param|=2.15e+05 loss_x2y=2.5147e-01 ppl_x2y=1.29 loss_y2x=2.5653e-01 ppl_y2x=1.29 dual_loss=3.4755e-01
Validation X2Y - loss=6.6004e-01 ppl=1.93 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.6658e-01 ppl=1.76 best_loss=5.5905e-01 best_ppl=1.75
Epoch 32 - |param|=9.22e+02 |g_param|=2.34e+05 loss_x2y=2.5461e-01 ppl_x2y=1.29 loss_y2x=2.5636e-01 ppl_y2x=1.29 dual_loss=3.9583e-01
Validation X2Y - loss=6.5434e-01 ppl=1.92 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.6060e-01 ppl=1.75 best_loss=5.5905e-01 best_ppl=1.75
Epoch 33 - |param|=9.22e+02 |g_param|=2.21e+05 loss_x2y=2.4428e-01 ppl_x2y=1.28 loss_y2x=2.4513e-01 ppl_y2x=1.28 dual_loss=4.0657e-01
Validation X2Y - loss=6.5953e-01 ppl=1.93 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.6678e-01 ppl=1.76 best_loss=5.5905e-01 best_ppl=1.75
Epoch 34 - |param|=9.22e+02 |g_param|=2.30e+05 loss_x2y=2.4014e-01 ppl_x2y=1.27 loss_y2x=2.3306e-01 ppl_y2x=1.26 dual_loss=3.4566e-01
Validation X2Y - loss=6.6138e-01 ppl=1.94 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.5478e-01 ppl=1.74 best_loss=5.5905e-01 best_ppl=1.75
Epoch 35 - |param|=9.23e+02 |g_param|=2.25e+05 loss_x2y=2.2581e-01 ppl_x2y=1.25 loss_y2x=2.2055e-01 ppl_y2x=1.25 dual_loss=3.3991e-01
Validation X2Y - loss=6.6313e-01 ppl=1.94 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1372e-01 ppl=1.85 best_loss=5.5478e-01 best_ppl=1.74
Epoch 36 - |param|=9.23e+02 |g_param|=2.56e+05 loss_x2y=2.3140e-01 ppl_x2y=1.26 loss_y2x=2.2752e-01 ppl_y2x=1.26 dual_loss=3.4876e-01
Validation X2Y - loss=6.5302e-01 ppl=1.92 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.7572e-01 ppl=1.78 best_loss=5.5478e-01 best_ppl=1.74
Epoch 37 - |param|=9.24e+02 |g_param|=2.53e+05 loss_x2y=2.2141e-01 ppl_x2y=1.25 loss_y2x=2.1359e-01 ppl_y2x=1.24 dual_loss=3.7897e-01
Validation X2Y - loss=6.4852e-01 ppl=1.91 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9217e-01 ppl=1.81 best_loss=5.5478e-01 best_ppl=1.74
Epoch 38 - |param|=9.24e+02 |g_param|=2.57e+05 loss_x2y=2.2568e-01 ppl_x2y=1.25 loss_y2x=2.1534e-01 ppl_y2x=1.24 dual_loss=3.4097e-01
Validation X2Y - loss=6.7091e-01 ppl=1.96 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.8384e-01 ppl=1.79 best_loss=5.5478e-01 best_ppl=1.74
Epoch 39 - |param|=9.24e+02 |g_param|=2.47e+05 loss_x2y=2.1491e-01 ppl_x2y=1.24 loss_y2x=2.1435e-01 ppl_y2x=1.24 dual_loss=4.1041e-01
Validation X2Y - loss=6.7022e-01 ppl=1.95 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1846e-01 ppl=1.86 best_loss=5.5478e-01 best_ppl=1.74
Epoch 40 - |param|=9.25e+02 |g_param|=2.55e+05 loss_x2y=2.0696e-01 ppl_x2y=1.23 loss_y2x=2.0117e-01 ppl_y2x=1.22 dual_loss=3.4259e-01
Validation X2Y - loss=6.6973e-01 ppl=1.95 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9693e-01 ppl=1.82 best_loss=5.5478e-01 best_ppl=1.74
Epoch 41 - |param|=9.25e+02 |g_param|=2.54e+05 loss_x2y=1.9998e-01 ppl_x2y=1.22 loss_y2x=1.9408e-01 ppl_y2x=1.21 dual_loss=4.1056e-01
Validation X2Y - loss=6.5736e-01 ppl=1.93 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9315e-01 ppl=1.81 best_loss=5.5478e-01 best_ppl=1.74
Epoch 42 - |param|=9.26e+02 |g_param|=4.21e+05 loss_x2y=1.8931e-01 ppl_x2y=1.21 loss_y2x=1.8787e-01 ppl_y2x=1.21 dual_loss=3.6210e-01
Validation X2Y - loss=7.0830e-01 ppl=2.03 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9919e-01 ppl=1.82 best_loss=5.5478e-01 best_ppl=1.74
Epoch 43 - |param|=9.26e+02 |g_param|=4.08e+05 loss_x2y=1.8978e-01 ppl_x2y=1.21 loss_y2x=1.8997e-01 ppl_y2x=1.21 dual_loss=3.4400e-01
Validation X2Y - loss=6.7759e-01 ppl=1.97 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.2431e-01 ppl=1.87 best_loss=5.5478e-01 best_ppl=1.74
Epoch 44 - |param|=9.26e+02 |g_param|=2.45e+05 loss_x2y=1.7733e-01 ppl_x2y=1.19 loss_y2x=1.8095e-01 ppl_y2x=1.20 dual_loss=3.1516e-01
Validation X2Y - loss=6.6227e-01 ppl=1.94 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.2225e-01 ppl=1.86 best_loss=5.5478e-01 best_ppl=1.74
Epoch 45 - |param|=9.27e+02 |g_param|=2.28e+05 loss_x2y=1.7951e-01 ppl_x2y=1.20 loss_y2x=1.7965e-01 ppl_y2x=1.20 dual_loss=3.0851e-01
Validation X2Y - loss=6.6622e-01 ppl=1.95 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=5.9952e-01 ppl=1.82 best_loss=5.5478e-01 best_ppl=1.74
Epoch 46 - |param|=9.27e+02 |g_param|=2.44e+05 loss_x2y=1.8147e-01 ppl_x2y=1.20 loss_y2x=1.7411e-01 ppl_y2x=1.19 dual_loss=2.9899e-01
Validation X2Y - loss=6.9591e-01 ppl=2.01 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1402e-01 ppl=1.85 best_loss=5.5478e-01 best_ppl=1.74
Epoch 47 - |param|=9.28e+02 |g_param|=1.57e+05 loss_x2y=1.7849e-01 ppl_x2y=1.20 loss_y2x=1.6998e-01 ppl_y2x=1.19 dual_loss=3.1205e-01
Validation X2Y - loss=6.9862e-01 ppl=2.01 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1288e-01 ppl=1.85 best_loss=5.5478e-01 best_ppl=1.74
Epoch 48 - |param|=9.28e+02 |g_param|=1.46e+05 loss_x2y=1.7127e-01 ppl_x2y=1.19 loss_y2x=1.7011e-01 ppl_y2x=1.19 dual_loss=3.1933e-01
Validation X2Y - loss=6.7767e-01 ppl=1.97 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.1085e-01 ppl=1.84 best_loss=5.5478e-01 best_ppl=1.74
Epoch 49 - |param|=9.28e+02 |g_param|=1.53e+05 loss_x2y=1.6997e-01 ppl_x2y=1.19 loss_y2x=1.7261e-01 ppl_y2x=1.19 dual_loss=3.9138e-01
Validation X2Y - loss=7.1832e-01 ppl=2.05 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.5648e-01 ppl=1.93 best_loss=5.5478e-01 best_ppl=1.74
Epoch 50 - |param|=9.29e+02 |g_param|=1.66e+05 loss_x2y=1.7278e-01 ppl_x2y=1.19 loss_y2x=1.7204e-01 ppl_y2x=1.19 dual_loss=3.5807e-01
Validation X2Y - loss=6.8921e-01 ppl=1.99 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3179e-01 ppl=1.88 best_loss=5.5478e-01 best_ppl=1.74
Epoch 51 - |param|=9.29e+02 |g_param|=1.48e+05 loss_x2y=1.6058e-01 ppl_x2y=1.17 loss_y2x=1.6210e-01 ppl_y2x=1.18 dual_loss=3.1382e-01
Validation X2Y - loss=7.0506e-01 ppl=2.02 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.5208e-01 ppl=1.92 best_loss=5.5478e-01 best_ppl=1.74
Epoch 52 - |param|=9.30e+02 |g_param|=1.62e+05 loss_x2y=1.6357e-01 ppl_x2y=1.18 loss_y2x=1.5681e-01 ppl_y2x=1.17 dual_loss=3.5511e-01
Validation X2Y - loss=6.9150e-01 ppl=2.00 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.2481e-01 ppl=1.87 best_loss=5.5478e-01 best_ppl=1.74
Epoch 53 - |param|=9.30e+02 |g_param|=1.53e+05 loss_x2y=1.6285e-01 ppl_x2y=1.18 loss_y2x=1.6324e-01 ppl_y2x=1.18 dual_loss=3.3756e-01
Validation X2Y - loss=6.9567e-01 ppl=2.01 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.7396e-01 ppl=1.96 best_loss=5.5478e-01 best_ppl=1.74
Epoch 54 - |param|=9.30e+02 |g_param|=1.59e+05 loss_x2y=1.6002e-01 ppl_x2y=1.17 loss_y2x=1.6304e-01 ppl_y2x=1.18 dual_loss=3.7061e-01
Validation X2Y - loss=6.9347e-01 ppl=2.00 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4418e-01 ppl=1.90 best_loss=5.5478e-01 best_ppl=1.74
Epoch 55 - |param|=9.31e+02 |g_param|=1.37e+05 loss_x2y=1.4866e-01 ppl_x2y=1.16 loss_y2x=1.5157e-01 ppl_y2x=1.16 dual_loss=3.3362e-01
Validation X2Y - loss=6.9997e-01 ppl=2.01 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3851e-01 ppl=1.89 best_loss=5.5478e-01 best_ppl=1.74
Epoch 56 - |param|=9.31e+02 |g_param|=2.02e+05 loss_x2y=1.5821e-01 ppl_x2y=1.17 loss_y2x=1.5786e-01 ppl_y2x=1.17 dual_loss=3.6770e-01
Validation X2Y - loss=7.0805e-01 ppl=2.03 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4721e-01 ppl=1.91 best_loss=5.5478e-01 best_ppl=1.74
Epoch 57 - |param|=9.32e+02 |g_param|=2.31e+05 loss_x2y=1.4515e-01 ppl_x2y=1.16 loss_y2x=1.4637e-01 ppl_y2x=1.16 dual_loss=3.2993e-01
Validation X2Y - loss=7.0543e-01 ppl=2.02 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.3682e-01 ppl=1.89 best_loss=5.5478e-01 best_ppl=1.74
Epoch 58 - |param|=9.32e+02 |g_param|=2.58e+05 loss_x2y=1.5163e-01 ppl_x2y=1.16 loss_y2x=1.5004e-01 ppl_y2x=1.16 dual_loss=3.7608e-01
Validation X2Y - loss=7.2273e-01 ppl=2.06 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4444e-01 ppl=1.90 best_loss=5.5478e-01 best_ppl=1.74
Epoch 59 - |param|=9.32e+02 |g_param|=2.51e+05 loss_x2y=1.4940e-01 ppl_x2y=1.16 loss_y2x=1.5153e-01 ppl_y2x=1.16 dual_loss=3.7370e-01
Validation X2Y - loss=7.2032e-01 ppl=2.06 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.5121e-01 ppl=1.92 best_loss=5.5478e-01 best_ppl=1.74
Epoch 60 - |param|=9.33e+02 |g_param|=2.30e+05 loss_x2y=1.4335e-01 ppl_x2y=1.15 loss_y2x=1.4185e-01 ppl_y2x=1.15 dual_loss=3.5408e-01
Validation X2Y - loss=7.1594e-01 ppl=2.05 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.5191e-01 ppl=1.92 best_loss=5.5478e-01 best_ppl=1.74
Epoch 61 - |param|=9.33e+02 |g_param|=2.34e+05 loss_x2y=1.3990e-01 ppl_x2y=1.15 loss_y2x=1.3813e-01 ppl_y2x=1.15 dual_loss=3.4316e-01
Validation X2Y - loss=7.1624e-01 ppl=2.05 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6442e-01 ppl=1.94 best_loss=5.5478e-01 best_ppl=1.74
Epoch 62 - |param|=9.34e+02 |g_param|=2.47e+05 loss_x2y=1.3901e-01 ppl_x2y=1.15 loss_y2x=1.4089e-01 ppl_y2x=1.15 dual_loss=3.5442e-01
Validation X2Y - loss=7.4111e-01 ppl=2.10 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6949e-01 ppl=1.95 best_loss=5.5478e-01 best_ppl=1.74
Epoch 63 - |param|=9.34e+02 |g_param|=2.39e+05 loss_x2y=1.3657e-01 ppl_x2y=1.15 loss_y2x=1.3402e-01 ppl_y2x=1.14 dual_loss=3.6802e-01
Validation X2Y - loss=7.1727e-01 ppl=2.05 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.5902e-01 ppl=1.93 best_loss=5.5478e-01 best_ppl=1.74
Epoch 64 - |param|=9.34e+02 |g_param|=2.51e+05 loss_x2y=1.4492e-01 ppl_x2y=1.16 loss_y2x=1.4167e-01 ppl_y2x=1.15 dual_loss=4.3443e-01
Validation X2Y - loss=7.0719e-01 ppl=2.03 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6392e-01 ppl=1.94 best_loss=5.5478e-01 best_ppl=1.74
Epoch 65 - |param|=9.35e+02 |g_param|=2.33e+05 loss_x2y=1.3350e-01 ppl_x2y=1.14 loss_y2x=1.3827e-01 ppl_y2x=1.15 dual_loss=3.7875e-01
Validation X2Y - loss=7.3661e-01 ppl=2.09 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.5531e-01 ppl=1.93 best_loss=5.5478e-01 best_ppl=1.74
Epoch 66 - |param|=9.35e+02 |g_param|=2.56e+05 loss_x2y=1.3401e-01 ppl_x2y=1.14 loss_y2x=1.3690e-01 ppl_y2x=1.15 dual_loss=4.0540e-01
Validation X2Y - loss=7.1420e-01 ppl=2.04 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.5613e-01 ppl=1.93 best_loss=5.5478e-01 best_ppl=1.74
Epoch 67 - |param|=9.36e+02 |g_param|=2.63e+05 loss_x2y=1.2954e-01 ppl_x2y=1.14 loss_y2x=1.3293e-01 ppl_y2x=1.14 dual_loss=3.7201e-01
Validation X2Y - loss=7.5318e-01 ppl=2.12 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6573e-01 ppl=1.95 best_loss=5.5478e-01 best_ppl=1.74
Epoch 68 - |param|=9.36e+02 |g_param|=2.83e+05 loss_x2y=1.2523e-01 ppl_x2y=1.13 loss_y2x=1.2734e-01 ppl_y2x=1.14 dual_loss=3.6784e-01
Validation X2Y - loss=7.4203e-01 ppl=2.10 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6894e-01 ppl=1.95 best_loss=5.5478e-01 best_ppl=1.74
Epoch 69 - |param|=9.36e+02 |g_param|=2.82e+05 loss_x2y=1.2701e-01 ppl_x2y=1.14 loss_y2x=1.2444e-01 ppl_y2x=1.13 dual_loss=3.5506e-01
Validation X2Y - loss=7.7097e-01 ppl=2.16 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6122e-01 ppl=1.94 best_loss=5.5478e-01 best_ppl=1.74
Epoch 70 - |param|=9.37e+02 |g_param|=2.80e+05 loss_x2y=1.2585e-01 ppl_x2y=1.13 loss_y2x=1.2507e-01 ppl_y2x=1.13 dual_loss=4.1799e-01
Validation X2Y - loss=7.5269e-01 ppl=2.12 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.7684e-01 ppl=1.97 best_loss=5.5478e-01 best_ppl=1.74
Epoch 71 - |param|=9.37e+02 |g_param|=2.93e+05 loss_x2y=1.2245e-01 ppl_x2y=1.13 loss_y2x=1.2266e-01 ppl_y2x=1.13 dual_loss=4.1905e-01
Validation X2Y - loss=7.5907e-01 ppl=2.14 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6909e-01 ppl=1.95 best_loss=5.5478e-01 best_ppl=1.74
Epoch 72 - |param|=9.37e+02 |g_param|=2.83e+05 loss_x2y=1.2821e-01 ppl_x2y=1.14 loss_y2x=1.2639e-01 ppl_y2x=1.13 dual_loss=4.0748e-01
Validation X2Y - loss=7.4096e-01 ppl=2.10 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.5997e-01 ppl=1.93 best_loss=5.5478e-01 best_ppl=1.74
Epoch 73 - |param|=9.38e+02 |g_param|=2.80e+05 loss_x2y=1.2177e-01 ppl_x2y=1.13 loss_y2x=1.2750e-01 ppl_y2x=1.14 dual_loss=3.8031e-01
Validation X2Y - loss=7.5115e-01 ppl=2.12 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.8885e-01 ppl=1.99 best_loss=5.5478e-01 best_ppl=1.74
Epoch 74 - |param|=9.38e+02 |g_param|=2.76e+05 loss_x2y=1.2080e-01 ppl_x2y=1.13 loss_y2x=1.2197e-01 ppl_y2x=1.13 dual_loss=3.7944e-01
Validation X2Y - loss=7.3843e-01 ppl=2.09 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.5170e-01 ppl=1.92 best_loss=5.5478e-01 best_ppl=1.74
Epoch 75 - |param|=9.39e+02 |g_param|=2.89e+05 loss_x2y=1.2292e-01 ppl_x2y=1.13 loss_y2x=1.2333e-01 ppl_y2x=1.13 dual_loss=3.7834e-01
Validation X2Y - loss=7.5715e-01 ppl=2.13 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.8540e-01 ppl=1.98 best_loss=5.5478e-01 best_ppl=1.74
Epoch 76 - |param|=9.39e+02 |g_param|=2.83e+05 loss_x2y=1.1869e-01 ppl_x2y=1.13 loss_y2x=1.2277e-01 ppl_y2x=1.13 dual_loss=3.6940e-01
Validation X2Y - loss=7.6644e-01 ppl=2.15 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6831e-01 ppl=1.95 best_loss=5.5478e-01 best_ppl=1.74
Epoch 77 - |param|=9.39e+02 |g_param|=4.57e+05 loss_x2y=1.1396e-01 ppl_x2y=1.12 loss_y2x=1.1953e-01 ppl_y2x=1.13 dual_loss=3.5833e-01
Validation X2Y - loss=7.7999e-01 ppl=2.18 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.4017e-01 ppl=1.90 best_loss=5.5478e-01 best_ppl=1.74
Epoch 78 - |param|=9.40e+02 |g_param|=4.60e+05 loss_x2y=1.1666e-01 ppl_x2y=1.12 loss_y2x=1.1491e-01 ppl_y2x=1.12 dual_loss=4.1075e-01
Validation X2Y - loss=8.0460e-01 ppl=2.24 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6106e-01 ppl=1.94 best_loss=5.5478e-01 best_ppl=1.74
Epoch 79 - |param|=9.40e+02 |g_param|=4.81e+05 loss_x2y=1.1409e-01 ppl_x2y=1.12 loss_y2x=1.1790e-01 ppl_y2x=1.13 dual_loss=4.2749e-01
Validation X2Y - loss=7.7595e-01 ppl=2.17 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.8729e-01 ppl=1.99 best_loss=5.5478e-01 best_ppl=1.74
Epoch 80 - |param|=9.41e+02 |g_param|=4.85e+05 loss_x2y=1.1630e-01 ppl_x2y=1.12 loss_y2x=1.1968e-01 ppl_y2x=1.13 dual_loss=4.3097e-01
Validation X2Y - loss=7.6295e-01 ppl=2.14 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.7824e-01 ppl=1.97 best_loss=5.5478e-01 best_ppl=1.74
Epoch 81 - |param|=9.41e+02 |g_param|=4.36e+05 loss_x2y=1.0991e-01 ppl_x2y=1.12 loss_y2x=1.0995e-01 ppl_y2x=1.12 dual_loss=3.8260e-01
Validation X2Y - loss=7.8845e-01 ppl=2.20 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.6492e-01 ppl=1.94 best_loss=5.5478e-01 best_ppl=1.74
Epoch 82 - |param|=9.41e+02 |g_param|=4.71e+05 loss_x2y=1.1176e-01 ppl_x2y=1.12 loss_y2x=1.1699e-01 ppl_y2x=1.12 dual_loss=4.0924e-01
Validation X2Y - loss=7.8382e-01 ppl=2.19 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.8082e-01 ppl=1.98 best_loss=5.5478e-01 best_ppl=1.74
Epoch 83 - |param|=9.42e+02 |g_param|=4.35e+05 loss_x2y=1.1348e-01 ppl_x2y=1.12 loss_y2x=1.1707e-01 ppl_y2x=1.12 dual_loss=3.8998e-01
Validation X2Y - loss=7.9241e-01 ppl=2.21 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.0257e-01 ppl=2.02 best_loss=5.5478e-01 best_ppl=1.74
Epoch 84 - |param|=9.42e+02 |g_param|=4.29e+05 loss_x2y=1.0614e-01 ppl_x2y=1.11 loss_y2x=1.1033e-01 ppl_y2x=1.12 dual_loss=3.8193e-01
Validation X2Y - loss=7.9945e-01 ppl=2.22 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.7761e-01 ppl=1.97 best_loss=5.5478e-01 best_ppl=1.74
Epoch 85 - |param|=9.42e+02 |g_param|=4.40e+05 loss_x2y=1.0854e-01 ppl_x2y=1.11 loss_y2x=1.0757e-01 ppl_y2x=1.11 dual_loss=4.5252e-01
Validation X2Y - loss=7.8131e-01 ppl=2.18 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=7.1132e-01 ppl=2.04 best_loss=5.5478e-01 best_ppl=1.74
Epoch 86 - |param|=9.43e+02 |g_param|=4.84e+05 loss_x2y=1.0471e-01 ppl_x2y=1.11 loss_y2x=1.1030e-01 ppl_y2x=1.12 dual_loss=4.1095e-01
Validation X2Y - loss=7.8070e-01 ppl=2.18 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.7754e-01 ppl=1.97 best_loss=5.5478e-01 best_ppl=1.74
Epoch 87 - |param|=9.43e+02 |g_param|=4.46e+05 loss_x2y=1.0185e-01 ppl_x2y=1.11 loss_y2x=1.1153e-01 ppl_y2x=1.12 dual_loss=3.7668e-01
Validation X2Y - loss=7.8842e-01 ppl=2.20 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.8732e-01 ppl=1.99 best_loss=5.5478e-01 best_ppl=1.74
Epoch 88 - |param|=9.44e+02 |g_param|=5.49e+05 loss_x2y=1.0697e-01 ppl_x2y=1.11 loss_y2x=1.0599e-01 ppl_y2x=1.11 dual_loss=3.9522e-01
Validation X2Y - loss=7.8681e-01 ppl=2.20 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.8965e-01 ppl=1.99 best_loss=5.5478e-01 best_ppl=1.74
Epoch 89 - |param|=9.44e+02 |g_param|=5.01e+05 loss_x2y=1.0560e-01 ppl_x2y=1.11 loss_y2x=1.0602e-01 ppl_y2x=1.11 dual_loss=3.7936e-01
Validation X2Y - loss=7.9233e-01 ppl=2.21 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.9003e-01 ppl=1.99 best_loss=5.5478e-01 best_ppl=1.74
Epoch 90 - |param|=9.44e+02 |g_param|=4.21e+05 loss_x2y=1.0133e-01 ppl_x2y=1.11 loss_y2x=1.0377e-01 ppl_y2x=1.11 dual_loss=4.1435e-01
Validation X2Y - loss=8.1738e-01 ppl=2.26 best_loss=6.3695e-01 best_ppl=1.89                                            
Validation Y2X - loss=6.7073e-01 ppl=1.96 best_loss=5.5478e-01 best_ppl=1.74

real	47m11.221s
user	46m30.235s
sys	0m40.844s
```

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/transformer/myrk-90epoch
Evaluation result for the model: dsl-model-myrk.01.3.51-33.46.3.55-34.90.2.92-18.51.2.99-19.95.pth, myrk
BLEU = 9.55, 46.2/19.6/6.9/2.4 (BP=0.863, ratio=0.872, hyp_len=20193, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.01.3.51-33.46.3.55-34.90.2.92-18.51.2.99-19.95.pth, rkmy
BLEU = 6.77, 33.7/13.7/3.9/1.2 (BP=1.000, ratio=1.063, hyp_len=24984, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.02.2.37-10.66.2.38-10.85.1.98-7.26.1.99-7.34.pth, myrk
BLEU = 26.57, 62.5/37.7/21.9/12.3 (BP=0.943, ratio=0.944, hyp_len=21867, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.02.2.37-10.66.2.38-10.85.1.98-7.26.1.99-7.34.pth, rkmy
BLEU = 21.92, 52.4/30.2/16.5/8.8 (BP=1.000, ratio=1.069, hyp_len=25131, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.03.1.81-6.11.1.77-5.89.1.52-4.56.1.47-4.35.pth, myrk
BLEU = 39.26, 68.1/47.7/32.9/22.2 (BP=1.000, ratio=1.042, hyp_len=24135, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.03.1.81-6.11.1.77-5.89.1.52-4.56.1.47-4.35.pth, rkmy
BLEU = 39.66, 68.2/47.9/32.9/23.0 (BP=1.000, ratio=1.015, hyp_len=23872, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.04.1.38-3.99.1.39-4.02.1.12-3.06.1.17-3.23.pth, myrk
BLEU = 51.63, 76.8/59.2/45.3/34.5 (BP=1.000, ratio=1.017, hyp_len=23548, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.04.1.38-3.99.1.39-4.02.1.12-3.06.1.17-3.23.pth, rkmy
BLEU = 46.47, 71.7/54.3/40.1/29.8 (BP=1.000, ratio=1.074, hyp_len=25250, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.05.1.13-3.09.1.09-2.98.0.97-2.64.0.96-2.61.pth, myrk
BLEU = 56.78, 79.7/63.8/50.8/40.3 (BP=1.000, ratio=1.023, hyp_len=23693, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.05.1.13-3.09.1.09-2.98.0.97-2.64.0.96-2.61.pth, rkmy
BLEU = 55.35, 78.2/62.6/49.3/38.9 (BP=1.000, ratio=1.033, hyp_len=24288, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.06.0.96-2.62.0.97-2.64.0.87-2.39.0.88-2.41.pth, myrk
BLEU = 60.51, 81.5/67.1/54.8/44.7 (BP=1.000, ratio=1.027, hyp_len=23786, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.06.0.96-2.62.0.97-2.64.0.87-2.39.0.88-2.41.pth, rkmy
BLEU = 51.71, 71.4/57.7/46.3/37.4 (BP=1.000, ratio=1.160, hyp_len=27269, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.07.0.86-2.36.0.86-2.36.0.80-2.22.0.80-2.22.pth, myrk
BLEU = 63.02, 83.2/69.3/57.4/47.7 (BP=1.000, ratio=1.020, hyp_len=23620, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.07.0.86-2.36.0.86-2.36.0.80-2.22.0.80-2.22.pth, rkmy
BLEU = 60.59, 81.0/67.4/55.0/44.9 (BP=1.000, ratio=1.038, hyp_len=24391, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.08.0.76-2.13.0.76-2.13.0.74-2.10.0.75-2.11.pth, myrk
BLEU = 64.59, 84.0/70.6/59.2/49.5 (BP=1.000, ratio=1.021, hyp_len=23646, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.08.0.76-2.13.0.76-2.13.0.74-2.10.0.75-2.11.pth, rkmy
BLEU = 61.43, 81.2/68.2/56.1/45.9 (BP=1.000, ratio=1.049, hyp_len=24663, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.09.0.67-1.96.0.67-1.95.0.73-2.07.0.71-2.04.pth, myrk
BLEU = 64.09, 82.9/69.7/58.7/49.7 (BP=1.000, ratio=1.048, hyp_len=24276, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.09.0.67-1.96.0.67-1.95.0.73-2.07.0.71-2.04.pth, rkmy
BLEU = 61.66, 81.5/68.5/56.2/46.0 (BP=1.000, ratio=1.053, hyp_len=24759, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.10.0.65-1.92.0.64-1.89.0.71-2.04.0.68-1.98.pth, myrk
BLEU = 65.94, 84.4/71.8/60.8/51.3 (BP=1.000, ratio=1.029, hyp_len=23821, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.10.0.65-1.92.0.64-1.89.0.71-2.04.0.68-1.98.pth, rkmy
BLEU = 65.56, 83.9/71.6/60.3/50.9 (BP=1.000, ratio=1.028, hyp_len=24164, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.11.0.56-1.74.0.55-1.74.0.71-2.03.0.76-2.13.pth, myrk
BLEU = 66.37, 84.7/71.8/61.1/52.2 (BP=1.000, ratio=1.027, hyp_len=23785, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.11.0.56-1.74.0.55-1.74.0.71-2.03.0.76-2.13.pth, rkmy
BLEU = 64.87, 83.9/71.0/59.4/49.9 (BP=1.000, ratio=1.011, hyp_len=23764, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.12.0.54-1.71.0.54-1.71.0.70-2.01.0.68-1.98.pth, myrk
BLEU = 69.15, 86.2/74.3/64.2/55.6 (BP=1.000, ratio=1.012, hyp_len=23435, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.12.0.54-1.71.0.54-1.71.0.70-2.01.0.68-1.98.pth, rkmy
BLEU = 65.63, 83.5/71.7/60.6/51.2 (BP=1.000, ratio=1.052, hyp_len=24739, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.13.0.50-1.65.0.49-1.63.0.66-1.93.0.64-1.90.pth, myrk
BLEU = 66.92, 84.4/72.3/61.9/53.1 (BP=1.000, ratio=1.045, hyp_len=24191, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.13.0.50-1.65.0.49-1.63.0.66-1.93.0.64-1.90.pth, rkmy
BLEU = 66.14, 83.4/72.1/61.2/52.1 (BP=1.000, ratio=1.053, hyp_len=24759, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.14.0.44-1.56.0.44-1.56.0.68-1.96.0.62-1.86.pth, myrk
BLEU = 63.90, 80.2/68.8/59.2/51.1 (BP=1.000, ratio=1.102, hyp_len=25525, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.14.0.44-1.56.0.44-1.56.0.68-1.96.0.62-1.86.pth, rkmy
BLEU = 65.39, 81.7/70.7/60.6/52.3 (BP=1.000, ratio=1.083, hyp_len=25466, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.15.0.43-1.54.0.43-1.54.0.67-1.96.0.62-1.85.pth, myrk
BLEU = 69.29, 85.3/74.1/64.6/56.5 (BP=1.000, ratio=1.037, hyp_len=24028, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.15.0.43-1.54.0.43-1.54.0.67-1.96.0.62-1.85.pth, rkmy
BLEU = 63.72, 80.7/69.5/58.9/49.9 (BP=1.000, ratio=1.099, hyp_len=25826, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.16.0.42-1.53.0.43-1.53.0.66-1.94.0.61-1.84.pth, myrk
BLEU = 68.02, 85.0/73.2/63.1/54.5 (BP=1.000, ratio=1.041, hyp_len=24111, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.16.0.42-1.53.0.43-1.53.0.66-1.94.0.61-1.84.pth, rkmy
BLEU = 69.16, 85.4/74.5/64.3/55.9 (BP=1.000, ratio=1.035, hyp_len=24330, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.17.0.39-1.48.0.40-1.49.0.66-1.93.0.60-1.82.pth, myrk
BLEU = 68.01, 84.6/73.1/63.2/54.7 (BP=1.000, ratio=1.041, hyp_len=24107, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.17.0.39-1.48.0.40-1.49.0.66-1.93.0.60-1.82.pth, rkmy
BLEU = 69.82, 85.7/75.0/65.1/56.8 (BP=1.000, ratio=1.039, hyp_len=24415, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.18.0.37-1.45.0.37-1.45.0.67-1.95.0.61-1.83.pth, myrk
BLEU = 67.48, 84.7/72.9/62.6/53.6 (BP=1.000, ratio=1.044, hyp_len=24179, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.18.0.37-1.45.0.37-1.45.0.67-1.95.0.61-1.83.pth, rkmy
BLEU = 69.71, 85.5/74.7/65.0/56.9 (BP=1.000, ratio=1.039, hyp_len=24433, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.19.0.36-1.43.0.34-1.41.0.66-1.94.0.59-1.81.pth, myrk
BLEU = 70.25, 86.5/75.1/65.5/57.3 (BP=1.000, ratio=1.027, hyp_len=23792, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.19.0.36-1.43.0.34-1.41.0.66-1.94.0.59-1.81.pth, rkmy
BLEU = 68.41, 84.8/73.9/63.6/55.0 (BP=1.000, ratio=1.052, hyp_len=24743, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.20.0.34-1.41.0.34-1.40.0.68-1.97.0.57-1.77.pth, myrk
BLEU = 69.54, 85.9/74.4/64.7/56.5 (BP=1.000, ratio=1.032, hyp_len=23911, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.20.0.34-1.41.0.34-1.40.0.68-1.97.0.57-1.77.pth, rkmy
BLEU = 69.74, 85.6/75.0/65.1/56.6 (BP=1.000, ratio=1.043, hyp_len=24526, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.21.0.37-1.45.0.36-1.44.0.66-1.93.0.58-1.78.pth, myrk
BLEU = 67.83, 84.7/73.1/62.9/54.3 (BP=1.000, ratio=1.047, hyp_len=24243, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.21.0.37-1.45.0.36-1.44.0.66-1.93.0.58-1.78.pth, rkmy
BLEU = 67.31, 83.7/72.7/62.5/54.0 (BP=1.000, ratio=1.066, hyp_len=25066, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.22.0.35-1.42.0.36-1.43.0.65-1.92.0.60-1.81.pth, myrk
BLEU = 70.33, 86.2/75.1/65.7/57.6 (BP=1.000, ratio=1.036, hyp_len=23992, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.22.0.35-1.42.0.36-1.43.0.65-1.92.0.60-1.81.pth, rkmy
BLEU = 66.00, 82.8/71.7/61.1/52.2 (BP=1.000, ratio=1.076, hyp_len=25289, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.23.0.33-1.40.0.33-1.39.0.66-1.93.0.57-1.77.pth, myrk
BLEU = 69.45, 85.4/74.3/64.8/56.6 (BP=1.000, ratio=1.040, hyp_len=24092, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.23.0.33-1.40.0.33-1.39.0.66-1.93.0.57-1.77.pth, rkmy
BLEU = 68.77, 85.2/74.0/63.9/55.6 (BP=1.000, ratio=1.044, hyp_len=24532, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.24.0.31-1.37.0.31-1.37.0.66-1.93.0.59-1.80.pth, myrk
BLEU = 69.17, 85.0/73.9/64.6/56.4 (BP=1.000, ratio=1.045, hyp_len=24199, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.24.0.31-1.37.0.31-1.37.0.66-1.93.0.59-1.80.pth, rkmy
BLEU = 68.09, 84.0/73.4/63.4/55.0 (BP=1.000, ratio=1.065, hyp_len=25042, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.25.0.31-1.36.0.31-1.37.0.64-1.89.0.58-1.78.pth, myrk
BLEU = 69.20, 85.4/73.9/64.5/56.3 (BP=1.000, ratio=1.039, hyp_len=24068, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.25.0.31-1.36.0.31-1.37.0.64-1.89.0.58-1.78.pth, rkmy
BLEU = 67.96, 83.7/73.0/63.2/55.2 (BP=1.000, ratio=1.069, hyp_len=25134, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.26.0.31-1.36.0.29-1.34.0.65-1.91.0.57-1.77.pth, myrk
BLEU = 68.61, 85.0/73.6/63.9/55.5 (BP=1.000, ratio=1.044, hyp_len=24171, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.26.0.31-1.36.0.29-1.34.0.65-1.91.0.57-1.77.pth, rkmy
BLEU = 69.03, 84.8/74.1/64.3/56.2 (BP=1.000, ratio=1.055, hyp_len=24811, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.27.0.29-1.34.0.29-1.33.0.64-1.90.0.59-1.81.pth, myrk
BLEU = 66.13, 82.2/71.0/61.5/53.3 (BP=1.000, ratio=1.086, hyp_len=25150, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.27.0.29-1.34.0.29-1.33.0.64-1.90.0.59-1.81.pth, rkmy
BLEU = 68.76, 84.3/73.8/64.1/56.0 (BP=1.000, ratio=1.064, hyp_len=25018, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.28.0.29-1.34.0.28-1.33.0.67-1.95.0.59-1.81.pth, myrk
BLEU = 66.60, 82.9/71.5/61.9/53.6 (BP=1.000, ratio=1.071, hyp_len=24807, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.28.0.29-1.34.0.28-1.33.0.67-1.95.0.59-1.81.pth, rkmy
BLEU = 66.37, 82.9/71.9/61.5/53.0 (BP=1.000, ratio=1.077, hyp_len=25313, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.29.0.27-1.31.0.27-1.31.0.64-1.90.0.56-1.75.pth, myrk
BLEU = 69.45, 85.3/74.2/64.9/56.7 (BP=1.000, ratio=1.045, hyp_len=24203, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.29.0.27-1.31.0.27-1.31.0.64-1.90.0.56-1.75.pth, rkmy
BLEU = 67.30, 83.0/72.2/62.5/54.7 (BP=1.000, ratio=1.078, hyp_len=25333, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.30.0.27-1.31.0.25-1.29.0.65-1.92.0.57-1.76.pth, myrk
BLEU = 68.76, 84.7/73.5/64.2/56.0 (BP=1.000, ratio=1.052, hyp_len=24375, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.30.0.27-1.31.0.25-1.29.0.65-1.92.0.57-1.76.pth, rkmy
BLEU = 67.61, 83.7/72.7/62.7/54.8 (BP=1.000, ratio=1.069, hyp_len=25138, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.31.0.25-1.29.0.26-1.29.0.66-1.93.0.57-1.76.pth, myrk
BLEU = 70.75, 86.0/75.2/66.2/58.5 (BP=1.000, ratio=1.035, hyp_len=23977, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.31.0.25-1.29.0.26-1.29.0.66-1.93.0.57-1.76.pth, rkmy
BLEU = 66.92, 83.1/72.3/62.2/53.7 (BP=1.000, ratio=1.071, hyp_len=25181, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.32.0.25-1.29.0.26-1.29.0.65-1.92.0.56-1.75.pth, myrk
BLEU = 69.33, 85.6/74.3/64.6/56.2 (BP=1.000, ratio=1.043, hyp_len=24166, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.32.0.25-1.29.0.26-1.29.0.65-1.92.0.56-1.75.pth, rkmy
BLEU = 68.45, 84.5/73.5/63.6/55.6 (BP=1.000, ratio=1.058, hyp_len=24875, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.33.0.24-1.28.0.25-1.28.0.66-1.93.0.57-1.76.pth, myrk
BLEU = 68.46, 84.3/73.2/63.9/55.7 (BP=1.000, ratio=1.057, hyp_len=24482, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.33.0.24-1.28.0.25-1.28.0.66-1.93.0.57-1.76.pth, rkmy
BLEU = 67.29, 83.9/72.8/62.4/53.8 (BP=1.000, ratio=1.067, hyp_len=25077, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.34.0.24-1.27.0.23-1.26.0.66-1.94.0.55-1.74.pth, myrk
BLEU = 71.31, 86.5/75.7/66.8/59.1 (BP=1.000, ratio=1.032, hyp_len=23908, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.34.0.24-1.27.0.23-1.26.0.66-1.94.0.55-1.74.pth, rkmy
BLEU = 68.40, 84.2/73.6/63.7/55.5 (BP=1.000, ratio=1.065, hyp_len=25031, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.35.0.23-1.25.0.22-1.25.0.66-1.94.0.61-1.85.pth, myrk
BLEU = 69.87, 85.3/74.4/65.3/57.5 (BP=1.000, ratio=1.050, hyp_len=24313, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.35.0.23-1.25.0.22-1.25.0.66-1.94.0.61-1.85.pth, rkmy
BLEU = 70.40, 85.8/75.5/65.7/57.7 (BP=1.000, ratio=1.044, hyp_len=24536, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.36.0.23-1.26.0.23-1.26.0.65-1.92.0.58-1.78.pth, myrk
BLEU = 69.74, 85.4/74.3/65.1/57.3 (BP=1.000, ratio=1.045, hyp_len=24212, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.36.0.23-1.26.0.23-1.26.0.65-1.92.0.58-1.78.pth, rkmy
BLEU = 69.72, 85.4/74.7/64.9/57.0 (BP=1.000, ratio=1.049, hyp_len=24669, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.37.0.22-1.25.0.21-1.24.0.65-1.91.0.59-1.81.pth, myrk
BLEU = 70.21, 85.7/74.8/65.7/57.7 (BP=1.000, ratio=1.041, hyp_len=24104, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.37.0.22-1.25.0.21-1.24.0.65-1.91.0.59-1.81.pth, rkmy
BLEU = 70.07, 85.7/74.9/65.3/57.5 (BP=1.000, ratio=1.045, hyp_len=24564, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.38.0.23-1.25.0.22-1.24.0.67-1.96.0.58-1.79.pth, myrk
BLEU = 69.50, 85.1/74.1/65.0/57.0 (BP=1.000, ratio=1.052, hyp_len=24355, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.38.0.23-1.25.0.22-1.24.0.67-1.96.0.58-1.79.pth, rkmy
BLEU = 69.72, 85.4/74.8/64.9/57.0 (BP=1.000, ratio=1.053, hyp_len=24752, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.39.0.21-1.24.0.21-1.24.0.67-1.95.0.62-1.86.pth, myrk
BLEU = 69.70, 85.2/74.3/65.1/57.2 (BP=1.000, ratio=1.054, hyp_len=24402, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.39.0.21-1.24.0.21-1.24.0.67-1.95.0.62-1.86.pth, rkmy
BLEU = 69.67, 85.4/74.8/64.9/56.8 (BP=1.000, ratio=1.050, hyp_len=24675, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.40.0.21-1.23.0.20-1.22.0.67-1.95.0.60-1.82.pth, myrk
BLEU = 67.83, 83.8/72.7/63.3/54.9 (BP=1.000, ratio=1.067, hyp_len=24705, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.40.0.21-1.23.0.20-1.22.0.67-1.95.0.60-1.82.pth, rkmy
BLEU = 69.92, 85.8/74.9/65.1/57.1 (BP=1.000, ratio=1.048, hyp_len=24638, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.41.0.20-1.22.0.19-1.21.0.66-1.93.0.59-1.81.pth, myrk
BLEU = 70.85, 85.8/75.3/66.5/58.6 (BP=1.000, ratio=1.046, hyp_len=24225, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.41.0.20-1.22.0.19-1.21.0.66-1.93.0.59-1.81.pth, rkmy
BLEU = 70.63, 86.0/75.4/66.0/58.2 (BP=1.000, ratio=1.044, hyp_len=24548, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.42.0.19-1.21.0.19-1.21.0.71-2.03.0.60-1.82.pth, myrk
BLEU = 70.99, 86.5/75.5/66.3/58.6 (BP=1.000, ratio=1.033, hyp_len=23930, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.42.0.19-1.21.0.19-1.21.0.71-2.03.0.60-1.82.pth, rkmy
BLEU = 68.52, 84.3/73.7/63.8/55.7 (BP=1.000, ratio=1.068, hyp_len=25108, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.43.0.19-1.21.0.19-1.21.0.68-1.97.0.62-1.87.pth, myrk
BLEU = 70.10, 85.6/74.7/65.6/57.6 (BP=1.000, ratio=1.048, hyp_len=24263, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.43.0.19-1.21.0.19-1.21.0.68-1.97.0.62-1.87.pth, rkmy
BLEU = 68.99, 85.0/74.0/64.2/56.1 (BP=1.000, ratio=1.058, hyp_len=24871, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.44.0.18-1.19.0.18-1.20.0.66-1.94.0.62-1.86.pth, myrk
BLEU = 70.50, 85.9/75.0/66.0/58.1 (BP=1.000, ratio=1.042, hyp_len=24139, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.44.0.18-1.19.0.18-1.20.0.66-1.94.0.62-1.86.pth, rkmy
BLEU = 69.71, 85.4/74.7/64.9/57.1 (BP=1.000, ratio=1.057, hyp_len=24840, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.45.0.18-1.20.0.18-1.20.0.67-1.95.0.60-1.82.pth, myrk
BLEU = 69.17, 85.0/73.9/64.6/56.3 (BP=1.000, ratio=1.051, hyp_len=24345, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.45.0.18-1.20.0.18-1.20.0.67-1.95.0.60-1.82.pth, rkmy
BLEU = 69.37, 85.1/74.3/64.5/56.7 (BP=1.000, ratio=1.055, hyp_len=24791, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.46.0.18-1.20.0.17-1.19.0.70-2.01.0.61-1.85.pth, myrk
BLEU = 69.35, 85.4/74.1/64.7/56.5 (BP=1.000, ratio=1.049, hyp_len=24290, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.46.0.18-1.20.0.17-1.19.0.70-2.01.0.61-1.85.pth, rkmy
BLEU = 70.67, 86.0/75.6/65.9/58.2 (BP=1.000, ratio=1.043, hyp_len=24514, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.47.0.18-1.20.0.17-1.19.0.70-2.01.0.61-1.85.pth, myrk
BLEU = 70.90, 86.1/75.3/66.4/58.7 (BP=1.000, ratio=1.035, hyp_len=23966, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.47.0.18-1.20.0.17-1.19.0.70-2.01.0.61-1.85.pth, rkmy
BLEU = 69.58, 85.4/74.6/64.8/56.8 (BP=1.000, ratio=1.053, hyp_len=24750, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.48.0.17-1.19.0.17-1.19.0.68-1.97.0.61-1.84.pth, myrk
BLEU = 70.01, 85.2/74.4/65.5/57.8 (BP=1.000, ratio=1.046, hyp_len=24224, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.48.0.17-1.19.0.17-1.19.0.68-1.97.0.61-1.84.pth, rkmy
BLEU = 70.18, 85.7/75.1/65.5/57.6 (BP=1.000, ratio=1.054, hyp_len=24786, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.49.0.17-1.19.0.17-1.19.0.72-2.05.0.66-1.93.pth, myrk
BLEU = 69.00, 84.6/73.5/64.4/56.6 (BP=1.000, ratio=1.060, hyp_len=24555, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.49.0.17-1.19.0.17-1.19.0.72-2.05.0.66-1.93.pth, rkmy
BLEU = 69.38, 85.1/74.4/64.6/56.7 (BP=1.000, ratio=1.054, hyp_len=24774, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.50.0.17-1.19.0.17-1.19.0.69-1.99.0.63-1.88.pth, myrk
BLEU = 70.26, 85.7/74.8/65.7/57.9 (BP=1.000, ratio=1.045, hyp_len=24207, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.50.0.17-1.19.0.17-1.19.0.69-1.99.0.63-1.88.pth, rkmy
BLEU = 70.39, 85.7/75.2/65.7/58.0 (BP=1.000, ratio=1.051, hyp_len=24716, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.51.0.16-1.17.0.16-1.18.0.71-2.02.0.65-1.92.pth, myrk
BLEU = 69.55, 85.1/74.3/65.0/56.9 (BP=1.000, ratio=1.051, hyp_len=24346, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.51.0.16-1.17.0.16-1.18.0.71-2.02.0.65-1.92.pth, rkmy
BLEU = 71.52, 86.4/76.2/66.9/59.3 (BP=1.000, ratio=1.039, hyp_len=24428, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.52.0.16-1.18.0.16-1.17.0.69-2.00.0.62-1.87.pth, myrk
BLEU = 69.93, 85.2/74.4/65.5/57.6 (BP=1.000, ratio=1.053, hyp_len=24388, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.52.0.16-1.18.0.16-1.17.0.69-2.00.0.62-1.87.pth, rkmy
BLEU = 70.15, 85.5/75.1/65.5/57.6 (BP=1.000, ratio=1.051, hyp_len=24712, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.53.0.16-1.18.0.16-1.18.0.70-2.01.0.67-1.96.pth, myrk
BLEU = 70.74, 86.1/75.2/66.2/58.5 (BP=1.000, ratio=1.036, hyp_len=23998, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.53.0.16-1.18.0.16-1.18.0.70-2.01.0.67-1.96.pth, rkmy
BLEU = 68.66, 84.5/73.8/63.9/55.7 (BP=1.000, ratio=1.062, hyp_len=24976, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.54.0.16-1.17.0.16-1.18.0.69-2.00.0.64-1.90.pth, myrk
BLEU = 70.12, 85.6/74.6/65.6/57.7 (BP=1.000, ratio=1.045, hyp_len=24195, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.54.0.16-1.17.0.16-1.18.0.69-2.00.0.64-1.90.pth, rkmy
BLEU = 68.56, 84.5/73.7/63.7/55.7 (BP=1.000, ratio=1.063, hyp_len=24996, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.55.0.15-1.16.0.15-1.16.0.70-2.01.0.64-1.89.pth, myrk
BLEU = 69.24, 85.2/74.0/64.6/56.5 (BP=1.000, ratio=1.050, hyp_len=24317, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.55.0.15-1.16.0.15-1.16.0.70-2.01.0.64-1.89.pth, rkmy
BLEU = 69.52, 85.2/74.6/64.7/56.8 (BP=1.000, ratio=1.053, hyp_len=24766, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.56.0.16-1.17.0.16-1.17.0.71-2.03.0.65-1.91.pth, myrk
BLEU = 69.70, 84.9/74.1/65.2/57.5 (BP=1.000, ratio=1.050, hyp_len=24316, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.56.0.16-1.17.0.16-1.17.0.71-2.03.0.65-1.91.pth, rkmy
BLEU = 69.60, 85.2/74.5/64.8/57.0 (BP=1.000, ratio=1.055, hyp_len=24808, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.57.0.15-1.16.0.15-1.16.0.71-2.02.0.64-1.89.pth, myrk
BLEU = 70.66, 86.1/75.2/66.1/58.2 (BP=1.000, ratio=1.037, hyp_len=24020, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.57.0.15-1.16.0.15-1.16.0.71-2.02.0.64-1.89.pth, rkmy
BLEU = 69.67, 85.2/74.7/65.0/57.0 (BP=1.000, ratio=1.057, hyp_len=24860, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.58.0.15-1.16.0.15-1.16.0.72-2.06.0.64-1.90.pth, myrk
BLEU = 70.37, 85.7/75.0/65.9/57.9 (BP=1.000, ratio=1.050, hyp_len=24312, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.58.0.15-1.16.0.15-1.16.0.72-2.06.0.64-1.90.pth, rkmy
BLEU = 70.14, 85.5/74.8/65.4/57.8 (BP=1.000, ratio=1.052, hyp_len=24723, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.59.0.15-1.16.0.15-1.16.0.72-2.06.0.65-1.92.pth, myrk
BLEU = 70.25, 85.3/74.6/65.8/58.2 (BP=1.000, ratio=1.045, hyp_len=24201, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.59.0.15-1.16.0.15-1.16.0.72-2.06.0.65-1.92.pth, rkmy
BLEU = 71.26, 86.2/76.0/66.7/59.0 (BP=1.000, ratio=1.043, hyp_len=24531, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.60.0.14-1.15.0.14-1.15.0.72-2.05.0.65-1.92.pth, myrk
BLEU = 70.75, 85.7/75.1/66.3/58.7 (BP=1.000, ratio=1.042, hyp_len=24125, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.60.0.14-1.15.0.14-1.15.0.72-2.05.0.65-1.92.pth, rkmy
BLEU = 70.41, 85.7/75.3/65.7/58.0 (BP=1.000, ratio=1.052, hyp_len=24724, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.61.0.14-1.15.0.14-1.15.0.72-2.05.0.66-1.94.pth, myrk
BLEU = 69.81, 85.1/74.3/65.3/57.5 (BP=1.000, ratio=1.049, hyp_len=24294, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.61.0.14-1.15.0.14-1.15.0.72-2.05.0.66-1.94.pth, rkmy
BLEU = 71.13, 86.2/75.8/66.5/59.0 (BP=1.000, ratio=1.046, hyp_len=24598, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.62.0.14-1.15.0.14-1.15.0.74-2.10.0.67-1.95.pth, myrk
BLEU = 70.44, 85.6/74.9/65.9/58.3 (BP=1.000, ratio=1.046, hyp_len=24236, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.62.0.14-1.15.0.14-1.15.0.74-2.10.0.67-1.95.pth, rkmy
BLEU = 70.40, 85.7/75.3/65.8/57.9 (BP=1.000, ratio=1.051, hyp_len=24715, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.63.0.14-1.15.0.13-1.14.0.72-2.05.0.66-1.93.pth, myrk
BLEU = 70.67, 85.8/75.1/66.2/58.5 (BP=1.000, ratio=1.042, hyp_len=24134, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.63.0.14-1.15.0.13-1.14.0.72-2.05.0.66-1.93.pth, rkmy
BLEU = 70.31, 85.7/75.2/65.6/57.8 (BP=1.000, ratio=1.050, hyp_len=24696, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.64.0.14-1.16.0.14-1.15.0.71-2.03.0.66-1.94.pth, myrk
BLEU = 69.83, 84.9/74.3/65.4/57.7 (BP=1.000, ratio=1.052, hyp_len=24366, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.64.0.14-1.16.0.14-1.15.0.71-2.03.0.66-1.94.pth, rkmy
BLEU = 69.38, 84.9/74.3/64.7/56.8 (BP=1.000, ratio=1.060, hyp_len=24916, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.65.0.13-1.14.0.14-1.15.0.74-2.09.0.66-1.93.pth, myrk
BLEU = 69.32, 84.7/73.9/64.8/56.9 (BP=1.000, ratio=1.054, hyp_len=24411, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.65.0.13-1.14.0.14-1.15.0.74-2.09.0.66-1.93.pth, rkmy
BLEU = 69.85, 85.4/74.7/65.0/57.3 (BP=1.000, ratio=1.052, hyp_len=24724, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.66.0.13-1.14.0.14-1.15.0.71-2.04.0.66-1.93.pth, myrk
BLEU = 70.74, 85.9/75.1/66.3/58.6 (BP=1.000, ratio=1.045, hyp_len=24195, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.66.0.13-1.14.0.14-1.15.0.71-2.04.0.66-1.93.pth, rkmy
BLEU = 69.29, 85.0/74.1/64.5/56.7 (BP=1.000, ratio=1.057, hyp_len=24844, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.67.0.13-1.14.0.13-1.14.0.75-2.12.0.67-1.95.pth, myrk
BLEU = 69.56, 84.6/74.1/65.2/57.3 (BP=1.000, ratio=1.062, hyp_len=24585, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.67.0.13-1.14.0.13-1.14.0.75-2.12.0.67-1.95.pth, rkmy
BLEU = 70.84, 86.0/75.6/66.2/58.5 (BP=1.000, ratio=1.047, hyp_len=24617, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.68.0.13-1.13.0.13-1.14.0.74-2.10.0.67-1.95.pth, myrk
BLEU = 70.28, 85.5/74.7/65.8/58.1 (BP=1.000, ratio=1.040, hyp_len=24094, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.68.0.13-1.13.0.13-1.14.0.74-2.10.0.67-1.95.pth, rkmy
BLEU = 68.64, 84.7/73.7/63.7/55.8 (BP=1.000, ratio=1.060, hyp_len=24912, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.69.0.13-1.14.0.12-1.13.0.77-2.16.0.66-1.94.pth, myrk
BLEU = 70.11, 85.3/74.7/65.7/57.7 (BP=1.000, ratio=1.050, hyp_len=24315, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.69.0.13-1.14.0.12-1.13.0.77-2.16.0.66-1.94.pth, rkmy
BLEU = 70.64, 85.9/75.3/65.9/58.4 (BP=1.000, ratio=1.051, hyp_len=24707, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.70.0.13-1.13.0.13-1.13.0.75-2.12.0.68-1.97.pth, myrk
BLEU = 70.66, 86.1/75.2/66.1/58.2 (BP=1.000, ratio=1.044, hyp_len=24169, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.70.0.13-1.13.0.13-1.13.0.75-2.12.0.68-1.97.pth, rkmy
BLEU = 70.05, 85.5/74.9/65.3/57.6 (BP=1.000, ratio=1.049, hyp_len=24670, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.71.0.12-1.13.0.12-1.13.0.76-2.14.0.67-1.95.pth, myrk
BLEU = 71.52, 86.6/76.0/67.0/59.4 (BP=1.000, ratio=1.038, hyp_len=24036, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.71.0.12-1.13.0.12-1.13.0.76-2.14.0.67-1.95.pth, rkmy
BLEU = 69.49, 85.2/74.5/64.8/56.7 (BP=1.000, ratio=1.055, hyp_len=24798, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.72.0.13-1.14.0.13-1.13.0.74-2.10.0.66-1.93.pth, myrk
BLEU = 71.08, 86.1/75.5/66.6/58.9 (BP=1.000, ratio=1.043, hyp_len=24167, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.72.0.13-1.14.0.13-1.13.0.74-2.10.0.66-1.93.pth, rkmy
BLEU = 70.45, 85.7/75.2/65.8/58.1 (BP=1.000, ratio=1.052, hyp_len=24741, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.73.0.12-1.13.0.13-1.14.0.75-2.12.0.69-1.99.pth, myrk
BLEU = 70.34, 85.7/74.9/65.8/57.9 (BP=1.000, ratio=1.045, hyp_len=24199, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.73.0.12-1.13.0.13-1.14.0.75-2.12.0.69-1.99.pth, rkmy
BLEU = 70.48, 85.7/75.3/65.8/58.0 (BP=1.000, ratio=1.052, hyp_len=24731, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.74.0.12-1.13.0.12-1.13.0.74-2.09.0.65-1.92.pth, myrk
BLEU = 70.07, 85.4/74.6/65.6/57.6 (BP=1.000, ratio=1.050, hyp_len=24315, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.74.0.12-1.13.0.12-1.13.0.74-2.09.0.65-1.92.pth, rkmy
BLEU = 71.10, 85.9/75.8/66.5/59.0 (BP=1.000, ratio=1.049, hyp_len=24653, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.75.0.12-1.13.0.12-1.13.0.76-2.13.0.69-1.98.pth, myrk
BLEU = 70.06, 85.3/74.5/65.6/57.8 (BP=1.000, ratio=1.051, hyp_len=24333, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.75.0.12-1.13.0.12-1.13.0.76-2.13.0.69-1.98.pth, rkmy
BLEU = 69.61, 85.2/74.3/64.8/57.2 (BP=1.000, ratio=1.057, hyp_len=24854, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.76.0.12-1.13.0.12-1.13.0.77-2.15.0.67-1.95.pth, myrk
BLEU = 71.70, 86.4/75.9/67.3/59.9 (BP=1.000, ratio=1.040, hyp_len=24090, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.76.0.12-1.13.0.12-1.13.0.77-2.15.0.67-1.95.pth, rkmy
BLEU = 69.09, 84.6/74.0/64.4/56.5 (BP=1.000, ratio=1.061, hyp_len=24936, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.77.0.11-1.12.0.12-1.13.0.78-2.18.0.64-1.90.pth, myrk
BLEU = 71.18, 86.5/75.7/66.6/58.8 (BP=1.000, ratio=1.041, hyp_len=24111, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.77.0.11-1.12.0.12-1.13.0.78-2.18.0.64-1.90.pth, rkmy
BLEU = 69.82, 85.2/74.6/65.2/57.3 (BP=1.000, ratio=1.060, hyp_len=24930, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.78.0.12-1.12.0.11-1.12.0.80-2.24.0.66-1.94.pth, myrk
BLEU = 70.72, 85.7/75.2/66.4/58.6 (BP=1.000, ratio=1.050, hyp_len=24324, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.78.0.12-1.12.0.11-1.12.0.80-2.24.0.66-1.94.pth, rkmy
BLEU = 69.82, 84.9/74.6/65.2/57.5 (BP=1.000, ratio=1.063, hyp_len=24991, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.79.0.11-1.12.0.12-1.13.0.78-2.17.0.69-1.99.pth, myrk
BLEU = 70.26, 85.4/74.9/65.9/57.8 (BP=1.000, ratio=1.052, hyp_len=24362, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.79.0.11-1.12.0.12-1.13.0.78-2.17.0.69-1.99.pth, rkmy
BLEU = 71.19, 86.1/75.9/66.6/59.0 (BP=1.000, ratio=1.048, hyp_len=24626, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.80.0.12-1.12.0.12-1.13.0.76-2.14.0.68-1.97.pth, myrk
BLEU = 70.51, 85.8/75.0/66.0/58.2 (BP=1.000, ratio=1.045, hyp_len=24204, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.80.0.12-1.12.0.12-1.13.0.76-2.14.0.68-1.97.pth, rkmy
BLEU = 70.06, 85.5/75.0/65.3/57.5 (BP=1.000, ratio=1.054, hyp_len=24782, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.81.0.11-1.12.0.11-1.12.0.79-2.20.0.66-1.94.pth, myrk
BLEU = 71.60, 86.3/76.0/67.3/59.6 (BP=1.000, ratio=1.041, hyp_len=24099, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.81.0.11-1.12.0.11-1.12.0.79-2.20.0.66-1.94.pth, rkmy
BLEU = 69.46, 85.0/74.4/64.7/56.9 (BP=1.000, ratio=1.058, hyp_len=24879, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.82.0.11-1.12.0.12-1.12.0.78-2.19.0.68-1.98.pth, myrk
BLEU = 70.38, 85.7/74.9/65.8/58.0 (BP=1.000, ratio=1.043, hyp_len=24155, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.82.0.11-1.12.0.12-1.12.0.78-2.19.0.68-1.98.pth, rkmy
BLEU = 68.04, 84.3/73.4/63.3/54.7 (BP=1.000, ratio=1.067, hyp_len=25080, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.83.0.11-1.12.0.12-1.12.0.79-2.21.0.70-2.02.pth, myrk
BLEU = 69.16, 84.8/73.8/64.5/56.6 (BP=1.000, ratio=1.055, hyp_len=24432, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.83.0.11-1.12.0.12-1.12.0.79-2.21.0.70-2.02.pth, rkmy
BLEU = 69.14, 85.0/73.9/64.4/56.5 (BP=1.000, ratio=1.061, hyp_len=24939, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.84.0.11-1.11.0.11-1.12.0.80-2.22.0.68-1.97.pth, myrk
BLEU = 70.74, 85.6/75.1/66.4/58.7 (BP=1.000, ratio=1.047, hyp_len=24238, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.84.0.11-1.11.0.11-1.12.0.80-2.22.0.68-1.97.pth, rkmy
BLEU = 70.46, 85.8/75.3/65.7/58.0 (BP=1.000, ratio=1.052, hyp_len=24733, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.85.0.11-1.11.0.11-1.11.0.78-2.18.0.71-2.04.pth, myrk
BLEU = 71.11, 86.0/75.4/66.7/59.1 (BP=1.000, ratio=1.042, hyp_len=24127, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.85.0.11-1.11.0.11-1.11.0.78-2.18.0.71-2.04.pth, rkmy
BLEU = 70.41, 85.7/75.3/65.7/58.0 (BP=1.000, ratio=1.054, hyp_len=24774, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.86.0.10-1.11.0.11-1.12.0.78-2.18.0.68-1.97.pth, myrk
BLEU = 71.31, 86.2/75.7/66.9/59.2 (BP=1.000, ratio=1.043, hyp_len=24148, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.86.0.10-1.11.0.11-1.12.0.78-2.18.0.68-1.97.pth, rkmy
BLEU = 70.92, 86.0/75.6/66.3/58.7 (BP=1.000, ratio=1.050, hyp_len=24683, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.87.0.10-1.11.0.11-1.12.0.79-2.20.0.69-1.99.pth, myrk
BLEU = 69.09, 84.6/73.7/64.6/56.6 (BP=1.000, ratio=1.062, hyp_len=24586, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.87.0.10-1.11.0.11-1.12.0.79-2.20.0.69-1.99.pth, rkmy
BLEU = 70.86, 86.2/75.7/66.2/58.4 (BP=1.000, ratio=1.046, hyp_len=24602, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.88.0.11-1.11.0.11-1.11.0.79-2.20.0.69-1.99.pth, myrk
BLEU = 70.95, 85.9/75.4/66.5/58.8 (BP=1.000, ratio=1.047, hyp_len=24238, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.88.0.11-1.11.0.11-1.11.0.79-2.20.0.69-1.99.pth, rkmy
BLEU = 70.57, 85.9/75.4/65.9/58.0 (BP=1.000, ratio=1.053, hyp_len=24758, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.89.0.11-1.11.0.11-1.11.0.79-2.21.0.69-1.99.pth, myrk
BLEU = 71.63, 86.5/76.0/67.2/59.6 (BP=1.000, ratio=1.040, hyp_len=24075, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.89.0.11-1.11.0.11-1.11.0.79-2.21.0.69-1.99.pth, rkmy
BLEU = 69.90, 85.2/74.7/65.3/57.5 (BP=1.000, ratio=1.055, hyp_len=24796, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.90.0.10-1.11.0.10-1.11.0.82-2.26.0.67-1.96.pth, myrk
BLEU = 71.05, 85.7/75.3/66.6/59.3 (BP=1.000, ratio=1.047, hyp_len=24254, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.90.0.10-1.11.0.10-1.11.0.82-2.26.0.67-1.96.pth, rkmy
BLEU = 69.78, 85.3/74.6/65.1/57.2 (BP=1.000, ratio=1.053, hyp_len=24758, ref_len=23509)
```

#### Warmup-Epoch 20, Total Epoch 100

```
Epoch 1 - |param|=9.11e+02 |g_param|=2.71e+05 loss_x2y=3.6256e+00 ppl_x2y=37.55 loss_y2x=3.6205e+00 ppl_y2x=37.36 dual_loss=0.0000e+00
Validation X2Y - loss=3.0995e+00 ppl=22.19 best_loss=inf best_ppl=inf                                                   
Validation Y2X - loss=3.0143e+00 ppl=20.37 best_loss=inf best_ppl=inf
Epoch 2 - |param|=9.12e+02 |g_param|=2.57e+05 loss_x2y=2.5081e+00 ppl_x2y=12.28 loss_y2x=2.4567e+00 ppl_y2x=11.67 dual_loss=0.0000e+00
Validation X2Y - loss=2.0832e+00 ppl=8.03 best_loss=3.0995e+00 best_ppl=22.19                                           
Validation Y2X - loss=2.0368e+00 ppl=7.67 best_loss=3.0143e+00 best_ppl=20.37
Epoch 3 - |param|=9.13e+02 |g_param|=2.26e+05 loss_x2y=1.8233e+00 ppl_x2y=6.19 loss_y2x=1.7749e+00 ppl_y2x=5.90 dual_loss=0.0000e+00
Validation X2Y - loss=1.5857e+00 ppl=4.88 best_loss=2.0832e+00 best_ppl=8.03                                            
Validation Y2X - loss=1.4724e+00 ppl=4.36 best_loss=2.0368e+00 best_ppl=7.67
Epoch 4 - |param|=9.13e+02 |g_param|=2.24e+05 loss_x2y=1.3753e+00 ppl_x2y=3.96 loss_y2x=1.3485e+00 ppl_y2x=3.85 dual_loss=0.0000e+00
Validation X2Y - loss=1.1858e+00 ppl=3.27 best_loss=1.5857e+00 best_ppl=4.88                                            
Validation Y2X - loss=1.1555e+00 ppl=3.18 best_loss=1.4724e+00 best_ppl=4.36
Epoch 5 - |param|=9.14e+02 |g_param|=2.44e+05 loss_x2y=1.1014e+00 ppl_x2y=3.01 loss_y2x=1.0894e+00 ppl_y2x=2.97 dual_loss=0.0000e+00
Validation X2Y - loss=1.0204e+00 ppl=2.77 best_loss=1.1858e+00 best_ppl=3.27                                            
Validation Y2X - loss=9.7090e-01 ppl=2.64 best_loss=1.1555e+00 best_ppl=3.18
Epoch 6 - |param|=9.14e+02 |g_param|=2.30e+05 loss_x2y=9.9357e-01 ppl_x2y=2.70 loss_y2x=9.8998e-01 ppl_y2x=2.69 dual_loss=0.0000e+00
Validation X2Y - loss=9.1710e-01 ppl=2.50 best_loss=1.0204e+00 best_ppl=2.77                                            
Validation Y2X - loss=8.8176e-01 ppl=2.42 best_loss=9.7090e-01 best_ppl=2.64
Epoch 7 - |param|=9.14e+02 |g_param|=1.82e+05 loss_x2y=7.9643e-01 ppl_x2y=2.22 loss_y2x=7.9461e-01 ppl_y2x=2.21 dual_loss=0.0000e+00
Validation X2Y - loss=8.5002e-01 ppl=2.34 best_loss=9.1710e-01 best_ppl=2.50                                            
Validation Y2X - loss=8.3775e-01 ppl=2.31 best_loss=8.8176e-01 best_ppl=2.42
Epoch 8 - |param|=9.14e+02 |g_param|=1.86e+05 loss_x2y=7.5457e-01 ppl_x2y=2.13 loss_y2x=7.6254e-01 ppl_y2x=2.14 dual_loss=0.0000e+00
Validation X2Y - loss=8.1493e-01 ppl=2.26 best_loss=8.5002e-01 best_ppl=2.34                                            
Validation Y2X - loss=7.3596e-01 ppl=2.09 best_loss=8.3775e-01 best_ppl=2.31
Epoch 9 - |param|=9.15e+02 |g_param|=2.03e+05 loss_x2y=6.9319e-01 ppl_x2y=2.00 loss_y2x=6.8959e-01 ppl_y2x=1.99 dual_loss=0.0000e+00
Validation X2Y - loss=7.2318e-01 ppl=2.06 best_loss=8.1493e-01 best_ppl=2.26                                            
Validation Y2X - loss=6.9032e-01 ppl=1.99 best_loss=7.3596e-01 best_ppl=2.09
Epoch 10 - |param|=9.15e+02 |g_param|=1.82e+05 loss_x2y=6.2171e-01 ppl_x2y=1.86 loss_y2x=6.2270e-01 ppl_y2x=1.86 dual_loss=0.0000e+00
Validation X2Y - loss=7.2507e-01 ppl=2.06 best_loss=7.2318e-01 best_ppl=2.06                                            
Validation Y2X - loss=6.9309e-01 ppl=2.00 best_loss=6.9032e-01 best_ppl=1.99
Epoch 11 - |param|=9.15e+02 |g_param|=1.75e+05 loss_x2y=5.6484e-01 ppl_x2y=1.76 loss_y2x=5.7503e-01 ppl_y2x=1.78 dual_loss=0.0000e+00
Validation X2Y - loss=6.9468e-01 ppl=2.00 best_loss=7.2318e-01 best_ppl=2.06                                            
Validation Y2X - loss=6.7795e-01 ppl=1.97 best_loss=6.9032e-01 best_ppl=1.99
Epoch 12 - |param|=9.16e+02 |g_param|=1.83e+05 loss_x2y=5.4867e-01 ppl_x2y=1.73 loss_y2x=5.5383e-01 ppl_y2x=1.74 dual_loss=0.0000e+00
Validation X2Y - loss=6.7735e-01 ppl=1.97 best_loss=6.9468e-01 best_ppl=2.00                                            
Validation Y2X - loss=6.4444e-01 ppl=1.90 best_loss=6.7795e-01 best_ppl=1.97
Epoch 13 - |param|=9.16e+02 |g_param|=1.58e+05 loss_x2y=4.8556e-01 ppl_x2y=1.63 loss_y2x=4.7355e-01 ppl_y2x=1.61 dual_loss=0.0000e+00
Validation X2Y - loss=6.5920e-01 ppl=1.93 best_loss=6.7735e-01 best_ppl=1.97                                            
Validation Y2X - loss=6.3515e-01 ppl=1.89 best_loss=6.4444e-01 best_ppl=1.90
Epoch 14 - |param|=9.16e+02 |g_param|=1.84e+05 loss_x2y=4.9724e-01 ppl_x2y=1.64 loss_y2x=4.9100e-01 ppl_y2x=1.63 dual_loss=0.0000e+00
Validation X2Y - loss=7.0612e-01 ppl=2.03 best_loss=6.5920e-01 best_ppl=1.93                                            
Validation Y2X - loss=6.5290e-01 ppl=1.92 best_loss=6.3515e-01 best_ppl=1.89
Epoch 15 - |param|=9.17e+02 |g_param|=1.51e+05 loss_x2y=4.2116e-01 ppl_x2y=1.52 loss_y2x=4.1798e-01 ppl_y2x=1.52 dual_loss=0.0000e+00
Validation X2Y - loss=6.4412e-01 ppl=1.90 best_loss=6.5920e-01 best_ppl=1.93                                            
Validation Y2X - loss=6.2905e-01 ppl=1.88 best_loss=6.3515e-01 best_ppl=1.89
Epoch 16 - |param|=9.17e+02 |g_param|=1.66e+05 loss_x2y=4.2649e-01 ppl_x2y=1.53 loss_y2x=4.2721e-01 ppl_y2x=1.53 dual_loss=0.0000e+00
Validation X2Y - loss=6.6464e-01 ppl=1.94 best_loss=6.4412e-01 best_ppl=1.90                                            
Validation Y2X - loss=6.2756e-01 ppl=1.87 best_loss=6.2905e-01 best_ppl=1.88
Epoch 17 - |param|=9.17e+02 |g_param|=1.56e+05 loss_x2y=4.0338e-01 ppl_x2y=1.50 loss_y2x=4.1397e-01 ppl_y2x=1.51 dual_loss=0.0000e+00
Validation X2Y - loss=6.2961e-01 ppl=1.88 best_loss=6.4412e-01 best_ppl=1.90                                            
Validation Y2X - loss=6.1023e-01 ppl=1.84 best_loss=6.2756e-01 best_ppl=1.87
Epoch 18 - |param|=9.18e+02 |g_param|=1.65e+05 loss_x2y=3.8096e-01 ppl_x2y=1.46 loss_y2x=3.8903e-01 ppl_y2x=1.48 dual_loss=0.0000e+00
Validation X2Y - loss=6.4217e-01 ppl=1.90 best_loss=6.2961e-01 best_ppl=1.88                                            
Validation Y2X - loss=6.1100e-01 ppl=1.84 best_loss=6.1023e-01 best_ppl=1.84
Epoch 19 - |param|=9.18e+02 |g_param|=1.48e+05 loss_x2y=3.5668e-01 ppl_x2y=1.43 loss_y2x=3.5501e-01 ppl_y2x=1.43 dual_loss=0.0000e+00
Validation X2Y - loss=6.5551e-01 ppl=1.93 best_loss=6.2961e-01 best_ppl=1.88                                            
Validation Y2X - loss=6.1518e-01 ppl=1.85 best_loss=6.1023e-01 best_ppl=1.84
Epoch 20 - |param|=9.19e+02 |g_param|=1.58e+05 loss_x2y=3.6416e-01 ppl_x2y=1.44 loss_y2x=3.6537e-01 ppl_y2x=1.44 dual_loss=0.0000e+00
Validation X2Y - loss=6.4501e-01 ppl=1.91 best_loss=6.2961e-01 best_ppl=1.88                                            
Validation Y2X - loss=6.1705e-01 ppl=1.85 best_loss=6.1023e-01 best_ppl=1.84
Epoch 21 - |param|=9.19e+02 |g_param|=1.58e+05 loss_x2y=3.4051e-01 ppl_x2y=1.41 loss_y2x=3.5617e-01 ppl_y2x=1.43 dual_loss=4.5806e-01
Validation X2Y - loss=6.6129e-01 ppl=1.94 best_loss=6.2961e-01 best_ppl=1.88                                            
Validation Y2X - loss=5.8595e-01 ppl=1.80 best_loss=6.1023e-01 best_ppl=1.84
Epoch 22 - |param|=9.19e+02 |g_param|=3.59e+05 loss_x2y=3.4024e-01 ppl_x2y=1.41 loss_y2x=3.5051e-01 ppl_y2x=1.42 dual_loss=5.6279e-01
Validation X2Y - loss=6.5333e-01 ppl=1.92 best_loss=6.2961e-01 best_ppl=1.88                                            
Validation Y2X - loss=6.1435e-01 ppl=1.85 best_loss=5.8595e-01 best_ppl=1.80
Epoch 23 - |param|=9.20e+02 |g_param|=3.07e+05 loss_x2y=3.2454e-01 ppl_x2y=1.38 loss_y2x=3.2530e-01 ppl_y2x=1.38 dual_loss=4.0144e-01
Validation X2Y - loss=6.5533e-01 ppl=1.93 best_loss=6.2961e-01 best_ppl=1.88                                            
Validation Y2X - loss=6.0168e-01 ppl=1.83 best_loss=5.8595e-01 best_ppl=1.80
Epoch 24 - |param|=9.20e+02 |g_param|=2.83e+05 loss_x2y=3.2905e-01 ppl_x2y=1.39 loss_y2x=3.1360e-01 ppl_y2x=1.37 dual_loss=3.8478e-01
Validation X2Y - loss=6.3653e-01 ppl=1.89 best_loss=6.2961e-01 best_ppl=1.88                                            
Validation Y2X - loss=5.9567e-01 ppl=1.81 best_loss=5.8595e-01 best_ppl=1.80
Epoch 25 - |param|=9.21e+02 |g_param|=3.02e+05 loss_x2y=2.9812e-01 ppl_x2y=1.35 loss_y2x=3.1942e-01 ppl_y2x=1.38 dual_loss=4.6645e-01
Validation X2Y - loss=6.3956e-01 ppl=1.90 best_loss=6.2961e-01 best_ppl=1.88                                            
Validation Y2X - loss=5.9896e-01 ppl=1.82 best_loss=5.8595e-01 best_ppl=1.80
Epoch 26 - |param|=9.21e+02 |g_param|=2.91e+05 loss_x2y=2.8681e-01 ppl_x2y=1.33 loss_y2x=2.8781e-01 ppl_y2x=1.33 dual_loss=3.8394e-01
Validation X2Y - loss=6.1961e-01 ppl=1.86 best_loss=6.2961e-01 best_ppl=1.88                                            
Validation Y2X - loss=6.2106e-01 ppl=1.86 best_loss=5.8595e-01 best_ppl=1.80
Epoch 27 - |param|=9.21e+02 |g_param|=1.95e+05 loss_x2y=2.9314e-01 ppl_x2y=1.34 loss_y2x=2.8710e-01 ppl_y2x=1.33 dual_loss=3.7074e-01
Validation X2Y - loss=6.3039e-01 ppl=1.88 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=5.8662e-01 ppl=1.80 best_loss=5.8595e-01 best_ppl=1.80
Epoch 28 - |param|=9.22e+02 |g_param|=2.07e+05 loss_x2y=2.8293e-01 ppl_x2y=1.33 loss_y2x=2.8786e-01 ppl_y2x=1.33 dual_loss=4.3505e-01
Validation X2Y - loss=6.4614e-01 ppl=1.91 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=5.8536e-01 ppl=1.80 best_loss=5.8595e-01 best_ppl=1.80
Epoch 29 - |param|=9.22e+02 |g_param|=1.88e+05 loss_x2y=2.7635e-01 ppl_x2y=1.32 loss_y2x=2.8076e-01 ppl_y2x=1.32 dual_loss=4.0774e-01
Validation X2Y - loss=6.3890e-01 ppl=1.89 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.0193e-01 ppl=1.83 best_loss=5.8536e-01 best_ppl=1.80
Epoch 30 - |param|=9.23e+02 |g_param|=1.73e+05 loss_x2y=2.5588e-01 ppl_x2y=1.29 loss_y2x=2.5318e-01 ppl_y2x=1.29 dual_loss=3.4143e-01
Validation X2Y - loss=6.6557e-01 ppl=1.95 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.1861e-01 ppl=1.86 best_loss=5.8536e-01 best_ppl=1.80
Epoch 31 - |param|=9.23e+02 |g_param|=1.74e+05 loss_x2y=2.5285e-01 ppl_x2y=1.29 loss_y2x=2.4462e-01 ppl_y2x=1.28 dual_loss=3.8853e-01
Validation X2Y - loss=6.5407e-01 ppl=1.92 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=5.7073e-01 ppl=1.77 best_loss=5.8536e-01 best_ppl=1.80
Epoch 32 - |param|=9.24e+02 |g_param|=1.84e+05 loss_x2y=2.4831e-01 ppl_x2y=1.28 loss_y2x=2.5099e-01 ppl_y2x=1.29 dual_loss=3.9039e-01
Validation X2Y - loss=6.6084e-01 ppl=1.94 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=5.9018e-01 ppl=1.80 best_loss=5.7073e-01 best_ppl=1.77
Epoch 33 - |param|=9.24e+02 |g_param|=1.66e+05 loss_x2y=2.2752e-01 ppl_x2y=1.26 loss_y2x=2.3771e-01 ppl_y2x=1.27 dual_loss=3.2321e-01
Validation X2Y - loss=6.6597e-01 ppl=1.95 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=5.9416e-01 ppl=1.81 best_loss=5.7073e-01 best_ppl=1.77
Epoch 34 - |param|=9.24e+02 |g_param|=1.66e+05 loss_x2y=2.3268e-01 ppl_x2y=1.26 loss_y2x=2.3193e-01 ppl_y2x=1.26 dual_loss=3.3118e-01
Validation X2Y - loss=6.6235e-01 ppl=1.94 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=5.7202e-01 ppl=1.77 best_loss=5.7073e-01 best_ppl=1.77
Epoch 35 - |param|=9.25e+02 |g_param|=1.64e+05 loss_x2y=2.2854e-01 ppl_x2y=1.26 loss_y2x=2.2711e-01 ppl_y2x=1.25 dual_loss=3.5537e-01
Validation X2Y - loss=6.5937e-01 ppl=1.93 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=5.6645e-01 ppl=1.76 best_loss=5.7073e-01 best_ppl=1.77
Epoch 36 - |param|=9.25e+02 |g_param|=1.72e+05 loss_x2y=2.2523e-01 ppl_x2y=1.25 loss_y2x=2.2953e-01 ppl_y2x=1.26 dual_loss=4.0405e-01
Validation X2Y - loss=6.6581e-01 ppl=1.95 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=5.9499e-01 ppl=1.81 best_loss=5.6645e-01 best_ppl=1.76
Epoch 37 - |param|=9.26e+02 |g_param|=1.72e+05 loss_x2y=2.1541e-01 ppl_x2y=1.24 loss_y2x=2.1272e-01 ppl_y2x=1.24 dual_loss=3.6347e-01
Validation X2Y - loss=6.6891e-01 ppl=1.95 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=5.9174e-01 ppl=1.81 best_loss=5.6645e-01 best_ppl=1.76
Epoch 38 - |param|=9.26e+02 |g_param|=1.71e+05 loss_x2y=2.1360e-01 ppl_x2y=1.24 loss_y2x=2.0881e-01 ppl_y2x=1.23 dual_loss=3.8648e-01
Validation X2Y - loss=6.7100e-01 ppl=1.96 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.0262e-01 ppl=1.83 best_loss=5.6645e-01 best_ppl=1.76
Epoch 39 - |param|=9.26e+02 |g_param|=1.54e+05 loss_x2y=2.0187e-01 ppl_x2y=1.22 loss_y2x=2.0706e-01 ppl_y2x=1.23 dual_loss=3.4191e-01
Validation X2Y - loss=6.6694e-01 ppl=1.95 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=5.9236e-01 ppl=1.81 best_loss=5.6645e-01 best_ppl=1.76
Epoch 40 - |param|=9.27e+02 |g_param|=1.68e+05 loss_x2y=2.0362e-01 ppl_x2y=1.23 loss_y2x=2.0699e-01 ppl_y2x=1.23 dual_loss=3.6844e-01
Validation X2Y - loss=6.7628e-01 ppl=1.97 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.1877e-01 ppl=1.86 best_loss=5.6645e-01 best_ppl=1.76
Epoch 41 - |param|=9.27e+02 |g_param|=1.53e+05 loss_x2y=1.9417e-01 ppl_x2y=1.21 loss_y2x=1.9622e-01 ppl_y2x=1.22 dual_loss=3.2605e-01
Validation X2Y - loss=6.7077e-01 ppl=1.96 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.2148e-01 ppl=1.86 best_loss=5.6645e-01 best_ppl=1.76
Epoch 42 - |param|=9.28e+02 |g_param|=1.52e+05 loss_x2y=1.9160e-01 ppl_x2y=1.21 loss_y2x=1.9273e-01 ppl_y2x=1.21 dual_loss=3.1639e-01
Validation X2Y - loss=7.0908e-01 ppl=2.03 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.0006e-01 ppl=1.82 best_loss=5.6645e-01 best_ppl=1.76
Epoch 43 - |param|=9.28e+02 |g_param|=1.68e+05 loss_x2y=1.9593e-01 ppl_x2y=1.22 loss_y2x=1.9381e-01 ppl_y2x=1.21 dual_loss=3.7958e-01
Validation X2Y - loss=6.6663e-01 ppl=1.95 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.3653e-01 ppl=1.89 best_loss=5.6645e-01 best_ppl=1.76
Epoch 44 - |param|=9.28e+02 |g_param|=1.81e+05 loss_x2y=1.8837e-01 ppl_x2y=1.21 loss_y2x=1.8953e-01 ppl_y2x=1.21 dual_loss=3.7096e-01
Validation X2Y - loss=6.8364e-01 ppl=1.98 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.0798e-01 ppl=1.84 best_loss=5.6645e-01 best_ppl=1.76
Epoch 45 - |param|=9.29e+02 |g_param|=1.60e+05 loss_x2y=1.8900e-01 ppl_x2y=1.21 loss_y2x=1.8741e-01 ppl_y2x=1.21 dual_loss=3.7945e-01
Validation X2Y - loss=6.9950e-01 ppl=2.01 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.4409e-01 ppl=1.90 best_loss=5.6645e-01 best_ppl=1.76
Epoch 46 - |param|=9.29e+02 |g_param|=1.54e+05 loss_x2y=1.7649e-01 ppl_x2y=1.19 loss_y2x=1.7494e-01 ppl_y2x=1.19 dual_loss=3.7480e-01
Validation X2Y - loss=7.0759e-01 ppl=2.03 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.2254e-01 ppl=1.86 best_loss=5.6645e-01 best_ppl=1.76
Epoch 47 - |param|=9.30e+02 |g_param|=2.52e+05 loss_x2y=1.7986e-01 ppl_x2y=1.20 loss_y2x=1.7692e-01 ppl_y2x=1.19 dual_loss=3.5600e-01
Validation X2Y - loss=7.0140e-01 ppl=2.02 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.0241e-01 ppl=1.83 best_loss=5.6645e-01 best_ppl=1.76
Epoch 48 - |param|=9.30e+02 |g_param|=3.10e+05 loss_x2y=1.7733e-01 ppl_x2y=1.19 loss_y2x=1.7461e-01 ppl_y2x=1.19 dual_loss=3.9191e-01
Validation X2Y - loss=7.0475e-01 ppl=2.02 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.0205e-01 ppl=1.83 best_loss=5.6645e-01 best_ppl=1.76
Epoch 49 - |param|=9.30e+02 |g_param|=3.34e+05 loss_x2y=1.7459e-01 ppl_x2y=1.19 loss_y2x=1.6757e-01 ppl_y2x=1.18 dual_loss=3.6185e-01
Validation X2Y - loss=7.1338e-01 ppl=2.04 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.1833e-01 ppl=1.86 best_loss=5.6645e-01 best_ppl=1.76
Epoch 50 - |param|=9.31e+02 |g_param|=3.11e+05 loss_x2y=1.6674e-01 ppl_x2y=1.18 loss_y2x=1.6802e-01 ppl_y2x=1.18 dual_loss=3.5403e-01
Validation X2Y - loss=7.3560e-01 ppl=2.09 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.2955e-01 ppl=1.88 best_loss=5.6645e-01 best_ppl=1.76
Epoch 51 - |param|=9.31e+02 |g_param|=3.41e+05 loss_x2y=1.6588e-01 ppl_x2y=1.18 loss_y2x=1.6785e-01 ppl_y2x=1.18 dual_loss=3.9181e-01
Validation X2Y - loss=7.1757e-01 ppl=2.05 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.2100e-01 ppl=1.86 best_loss=5.6645e-01 best_ppl=1.76
Epoch 52 - |param|=9.32e+02 |g_param|=3.37e+05 loss_x2y=1.6648e-01 ppl_x2y=1.18 loss_y2x=1.6659e-01 ppl_y2x=1.18 dual_loss=4.3886e-01
Validation X2Y - loss=6.9157e-01 ppl=2.00 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.3695e-01 ppl=1.89 best_loss=5.6645e-01 best_ppl=1.76
Epoch 53 - |param|=9.32e+02 |g_param|=3.01e+05 loss_x2y=1.5997e-01 ppl_x2y=1.17 loss_y2x=1.6506e-01 ppl_y2x=1.18 dual_loss=3.3904e-01
Validation X2Y - loss=7.2214e-01 ppl=2.06 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.2727e-01 ppl=1.87 best_loss=5.6645e-01 best_ppl=1.76
Epoch 54 - |param|=9.32e+02 |g_param|=3.05e+05 loss_x2y=1.5828e-01 ppl_x2y=1.17 loss_y2x=1.6041e-01 ppl_y2x=1.17 dual_loss=3.6407e-01
Validation X2Y - loss=6.8791e-01 ppl=1.99 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.3787e-01 ppl=1.89 best_loss=5.6645e-01 best_ppl=1.76
Epoch 55 - |param|=9.33e+02 |g_param|=3.15e+05 loss_x2y=1.5731e-01 ppl_x2y=1.17 loss_y2x=1.5548e-01 ppl_y2x=1.17 dual_loss=4.7847e-01
Validation X2Y - loss=7.1496e-01 ppl=2.04 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.3557e-01 ppl=1.89 best_loss=5.6645e-01 best_ppl=1.76
Epoch 56 - |param|=9.33e+02 |g_param|=3.18e+05 loss_x2y=1.5628e-01 ppl_x2y=1.17 loss_y2x=1.5195e-01 ppl_y2x=1.16 dual_loss=3.3082e-01
Validation X2Y - loss=7.3074e-01 ppl=2.08 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.2330e-01 ppl=1.87 best_loss=5.6645e-01 best_ppl=1.76
Epoch 57 - |param|=9.34e+02 |g_param|=3.03e+05 loss_x2y=1.5550e-01 ppl_x2y=1.17 loss_y2x=1.5225e-01 ppl_y2x=1.16 dual_loss=3.4544e-01
Validation X2Y - loss=7.3307e-01 ppl=2.08 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.4809e-01 ppl=1.91 best_loss=5.6645e-01 best_ppl=1.76
Epoch 58 - |param|=9.34e+02 |g_param|=3.36e+05 loss_x2y=1.5445e-01 ppl_x2y=1.17 loss_y2x=1.5541e-01 ppl_y2x=1.17 dual_loss=3.9716e-01
Validation X2Y - loss=7.3799e-01 ppl=2.09 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.4413e-01 ppl=1.90 best_loss=5.6645e-01 best_ppl=1.76
Epoch 59 - |param|=9.34e+02 |g_param|=3.02e+05 loss_x2y=1.5177e-01 ppl_x2y=1.16 loss_y2x=1.4850e-01 ppl_y2x=1.16 dual_loss=3.9314e-01
Validation X2Y - loss=7.2812e-01 ppl=2.07 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.3940e-01 ppl=1.90 best_loss=5.6645e-01 best_ppl=1.76
Epoch 60 - |param|=9.35e+02 |g_param|=2.98e+05 loss_x2y=1.4477e-01 ppl_x2y=1.16 loss_y2x=1.4647e-01 ppl_y2x=1.16 dual_loss=3.5314e-01
Validation X2Y - loss=7.1842e-01 ppl=2.05 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.4789e-01 ppl=1.91 best_loss=5.6645e-01 best_ppl=1.76
Epoch 61 - |param|=9.35e+02 |g_param|=2.94e+05 loss_x2y=1.4362e-01 ppl_x2y=1.15 loss_y2x=1.4656e-01 ppl_y2x=1.16 dual_loss=3.5568e-01
Validation X2Y - loss=7.3565e-01 ppl=2.09 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.4670e-01 ppl=1.91 best_loss=5.6645e-01 best_ppl=1.76
Epoch 62 - |param|=9.36e+02 |g_param|=3.00e+05 loss_x2y=1.4577e-01 ppl_x2y=1.16 loss_y2x=1.4229e-01 ppl_y2x=1.15 dual_loss=3.6262e-01
Validation X2Y - loss=7.3468e-01 ppl=2.08 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.5749e-01 ppl=1.93 best_loss=5.6645e-01 best_ppl=1.76
Epoch 63 - |param|=9.36e+02 |g_param|=2.75e+05 loss_x2y=1.3493e-01 ppl_x2y=1.14 loss_y2x=1.3512e-01 ppl_y2x=1.14 dual_loss=3.6236e-01
Validation X2Y - loss=7.3133e-01 ppl=2.08 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.4225e-01 ppl=1.90 best_loss=5.6645e-01 best_ppl=1.76
Epoch 64 - |param|=9.36e+02 |g_param|=3.05e+05 loss_x2y=1.3804e-01 ppl_x2y=1.15 loss_y2x=1.3708e-01 ppl_y2x=1.15 dual_loss=3.7784e-01
Validation X2Y - loss=7.4045e-01 ppl=2.10 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.7728e-01 ppl=1.97 best_loss=5.6645e-01 best_ppl=1.76
Epoch 65 - |param|=9.37e+02 |g_param|=2.77e+05 loss_x2y=1.3159e-01 ppl_x2y=1.14 loss_y2x=1.3361e-01 ppl_y2x=1.14 dual_loss=3.5068e-01
Validation X2Y - loss=7.4666e-01 ppl=2.11 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.9910e-01 ppl=2.01 best_loss=5.6645e-01 best_ppl=1.76
Epoch 66 - |param|=9.37e+02 |g_param|=3.26e+05 loss_x2y=1.3396e-01 ppl_x2y=1.14 loss_y2x=1.4425e-01 ppl_y2x=1.16 dual_loss=4.2732e-01
Validation X2Y - loss=7.4607e-01 ppl=2.11 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.5753e-01 ppl=1.93 best_loss=5.6645e-01 best_ppl=1.76
Epoch 67 - |param|=9.37e+02 |g_param|=3.84e+05 loss_x2y=1.3826e-01 ppl_x2y=1.15 loss_y2x=1.3396e-01 ppl_y2x=1.14 dual_loss=3.5591e-01
Validation X2Y - loss=7.6427e-01 ppl=2.15 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.5809e-01 ppl=1.93 best_loss=5.6645e-01 best_ppl=1.76
Epoch 68 - |param|=9.38e+02 |g_param|=5.53e+05 loss_x2y=1.3033e-01 ppl_x2y=1.14 loss_y2x=1.2222e-01 ppl_y2x=1.13 dual_loss=3.6634e-01
Validation X2Y - loss=7.5973e-01 ppl=2.14 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.7308e-01 ppl=1.96 best_loss=5.6645e-01 best_ppl=1.76
Epoch 69 - |param|=9.38e+02 |g_param|=5.75e+05 loss_x2y=1.3788e-01 ppl_x2y=1.15 loss_y2x=1.3340e-01 ppl_y2x=1.14 dual_loss=3.4544e-01
Validation X2Y - loss=7.5458e-01 ppl=2.13 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.5594e-01 ppl=1.93 best_loss=5.6645e-01 best_ppl=1.76
Epoch 70 - |param|=9.39e+02 |g_param|=4.50e+05 loss_x2y=1.2887e-01 ppl_x2y=1.14 loss_y2x=1.3300e-01 ppl_y2x=1.14 dual_loss=4.1552e-01
Validation X2Y - loss=7.6207e-01 ppl=2.14 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.6679e-01 ppl=1.95 best_loss=5.6645e-01 best_ppl=1.76
Epoch 71 - |param|=9.39e+02 |g_param|=4.19e+05 loss_x2y=1.2824e-01 ppl_x2y=1.14 loss_y2x=1.2986e-01 ppl_y2x=1.14 dual_loss=3.6957e-01
Validation X2Y - loss=7.5881e-01 ppl=2.14 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.4358e-01 ppl=1.90 best_loss=5.6645e-01 best_ppl=1.76
Epoch 72 - |param|=9.39e+02 |g_param|=4.36e+05 loss_x2y=1.2818e-01 ppl_x2y=1.14 loss_y2x=1.2450e-01 ppl_y2x=1.13 dual_loss=4.0336e-01
Validation X2Y - loss=7.6373e-01 ppl=2.15 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.4735e-01 ppl=1.91 best_loss=5.6645e-01 best_ppl=1.76
Epoch 73 - |param|=9.40e+02 |g_param|=4.17e+05 loss_x2y=1.2072e-01 ppl_x2y=1.13 loss_y2x=1.2336e-01 ppl_y2x=1.13 dual_loss=3.4952e-01
Validation X2Y - loss=7.4547e-01 ppl=2.11 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.7692e-01 ppl=1.97 best_loss=5.6645e-01 best_ppl=1.76
Epoch 74 - |param|=9.40e+02 |g_param|=4.15e+05 loss_x2y=1.2104e-01 ppl_x2y=1.13 loss_y2x=1.1938e-01 ppl_y2x=1.13 dual_loss=3.6550e-01
Validation X2Y - loss=7.7613e-01 ppl=2.17 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.6472e-01 ppl=1.94 best_loss=5.6645e-01 best_ppl=1.76
Epoch 75 - |param|=9.41e+02 |g_param|=4.03e+05 loss_x2y=1.1707e-01 ppl_x2y=1.12 loss_y2x=1.1553e-01 ppl_y2x=1.12 dual_loss=3.4902e-01
Validation X2Y - loss=7.6863e-01 ppl=2.16 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=7.0270e-01 ppl=2.02 best_loss=5.6645e-01 best_ppl=1.76
Epoch 76 - |param|=9.41e+02 |g_param|=4.45e+05 loss_x2y=1.2358e-01 ppl_x2y=1.13 loss_y2x=1.1951e-01 ppl_y2x=1.13 dual_loss=4.3262e-01
Validation X2Y - loss=7.7043e-01 ppl=2.16 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.7025e-01 ppl=1.95 best_loss=5.6645e-01 best_ppl=1.76
Epoch 77 - |param|=9.41e+02 |g_param|=4.20e+05 loss_x2y=1.1968e-01 ppl_x2y=1.13 loss_y2x=1.2106e-01 ppl_y2x=1.13 dual_loss=4.2679e-01
Validation X2Y - loss=7.8319e-01 ppl=2.19 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.8979e-01 ppl=1.99 best_loss=5.6645e-01 best_ppl=1.76
Epoch 78 - |param|=9.42e+02 |g_param|=4.33e+05 loss_x2y=1.1529e-01 ppl_x2y=1.12 loss_y2x=1.1368e-01 ppl_y2x=1.12 dual_loss=4.0604e-01
Validation X2Y - loss=7.5957e-01 ppl=2.14 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.8119e-01 ppl=1.98 best_loss=5.6645e-01 best_ppl=1.76
Epoch 79 - |param|=9.42e+02 |g_param|=3.91e+05 loss_x2y=1.1713e-01 ppl_x2y=1.12 loss_y2x=1.1203e-01 ppl_y2x=1.12 dual_loss=3.7902e-01
Validation X2Y - loss=7.7741e-01 ppl=2.18 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.8744e-01 ppl=1.99 best_loss=5.6645e-01 best_ppl=1.76
Epoch 80 - |param|=9.43e+02 |g_param|=3.96e+05 loss_x2y=1.1212e-01 ppl_x2y=1.12 loss_y2x=1.1505e-01 ppl_y2x=1.12 dual_loss=3.9992e-01
Validation X2Y - loss=7.7125e-01 ppl=2.16 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.7407e-01 ppl=1.96 best_loss=5.6645e-01 best_ppl=1.76
Epoch 81 - |param|=9.43e+02 |g_param|=3.97e+05 loss_x2y=1.1009e-01 ppl_x2y=1.12 loss_y2x=1.1048e-01 ppl_y2x=1.12 dual_loss=3.8937e-01
Validation X2Y - loss=7.8044e-01 ppl=2.18 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.8091e-01 ppl=1.98 best_loss=5.6645e-01 best_ppl=1.76
Epoch 82 - |param|=9.43e+02 |g_param|=3.97e+05 loss_x2y=1.1068e-01 ppl_x2y=1.12 loss_y2x=1.1172e-01 ppl_y2x=1.12 dual_loss=3.7410e-01
Validation X2Y - loss=7.7866e-01 ppl=2.18 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.8539e-01 ppl=1.98 best_loss=5.6645e-01 best_ppl=1.76
Epoch 83 - |param|=9.44e+02 |g_param|=3.82e+05 loss_x2y=1.1145e-01 ppl_x2y=1.12 loss_y2x=1.1025e-01 ppl_y2x=1.12 dual_loss=3.6869e-01
Validation X2Y - loss=7.9945e-01 ppl=2.22 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.7941e-01 ppl=1.97 best_loss=5.6645e-01 best_ppl=1.76
Epoch 84 - |param|=9.44e+02 |g_param|=3.93e+05 loss_x2y=1.0928e-01 ppl_x2y=1.12 loss_y2x=1.0790e-01 ppl_y2x=1.11 dual_loss=3.6010e-01
Validation X2Y - loss=7.8661e-01 ppl=2.20 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=7.0524e-01 ppl=2.02 best_loss=5.6645e-01 best_ppl=1.76
Epoch 85 - |param|=9.44e+02 |g_param|=4.14e+05 loss_x2y=1.1462e-01 ppl_x2y=1.12 loss_y2x=1.1262e-01 ppl_y2x=1.12 dual_loss=3.9151e-01
Validation X2Y - loss=7.8688e-01 ppl=2.20 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=7.0654e-01 ppl=2.03 best_loss=5.6645e-01 best_ppl=1.76
Epoch 86 - |param|=9.45e+02 |g_param|=4.26e+05 loss_x2y=1.1271e-01 ppl_x2y=1.12 loss_y2x=1.0757e-01 ppl_y2x=1.11 dual_loss=4.1863e-01
Validation X2Y - loss=8.0420e-01 ppl=2.23 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=7.0105e-01 ppl=2.02 best_loss=5.6645e-01 best_ppl=1.76
Epoch 87 - |param|=9.45e+02 |g_param|=4.39e+05 loss_x2y=1.0710e-01 ppl_x2y=1.11 loss_y2x=1.0877e-01 ppl_y2x=1.11 dual_loss=4.3017e-01
Validation X2Y - loss=7.8947e-01 ppl=2.20 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=7.0410e-01 ppl=2.02 best_loss=5.6645e-01 best_ppl=1.76
Epoch 88 - |param|=9.46e+02 |g_param|=4.15e+05 loss_x2y=1.1053e-01 ppl_x2y=1.12 loss_y2x=1.0573e-01 ppl_y2x=1.11 dual_loss=3.7041e-01
Validation X2Y - loss=7.9797e-01 ppl=2.22 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=6.9888e-01 ppl=2.01 best_loss=5.6645e-01 best_ppl=1.76
Epoch 89 - |param|=9.46e+02 |g_param|=3.89e+05 loss_x2y=1.0584e-01 ppl_x2y=1.11 loss_y2x=1.0329e-01 ppl_y2x=1.11 dual_loss=3.4810e-01
Validation X2Y - loss=7.8601e-01 ppl=2.19 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=7.2858e-01 ppl=2.07 best_loss=5.6645e-01 best_ppl=1.76
Epoch 90 - |param|=9.46e+02 |g_param|=3.79e+05 loss_x2y=1.0386e-01 ppl_x2y=1.11 loss_y2x=1.0668e-01 ppl_y2x=1.11 dual_loss=4.1767e-01
Validation X2Y - loss=7.7672e-01 ppl=2.17 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=7.2064e-01 ppl=2.06 best_loss=5.6645e-01 best_ppl=1.76
Epoch 91 - |param|=9.47e+02 |g_param|=5.12e+05 loss_x2y=1.0384e-01 ppl_x2y=1.11 loss_y2x=1.0126e-01 ppl_y2x=1.11 dual_loss=3.8636e-01
Validation X2Y - loss=7.8160e-01 ppl=2.18 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=7.2736e-01 ppl=2.07 best_loss=5.6645e-01 best_ppl=1.76
Epoch 92 - |param|=9.47e+02 |g_param|=5.21e+05 loss_x2y=1.0235e-01 ppl_x2y=1.11 loss_y2x=1.0031e-01 ppl_y2x=1.11 dual_loss=3.7173e-01
Validation X2Y - loss=7.9885e-01 ppl=2.22 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=7.2743e-01 ppl=2.07 best_loss=5.6645e-01 best_ppl=1.76
Epoch 93 - |param|=9.47e+02 |g_param|=4.77e+05 loss_x2y=1.0256e-01 ppl_x2y=1.11 loss_y2x=9.8924e-02 ppl_y2x=1.10 dual_loss=3.7136e-01
Validation X2Y - loss=8.0730e-01 ppl=2.24 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=7.2317e-01 ppl=2.06 best_loss=5.6645e-01 best_ppl=1.76
Epoch 94 - |param|=9.48e+02 |g_param|=5.58e+05 loss_x2y=1.0512e-01 ppl_x2y=1.11 loss_y2x=1.0364e-01 ppl_y2x=1.11 dual_loss=4.2433e-01
Validation X2Y - loss=7.9425e-01 ppl=2.21 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=7.4291e-01 ppl=2.10 best_loss=5.6645e-01 best_ppl=1.76
Epoch 95 - |param|=9.48e+02 |g_param|=5.05e+05 loss_x2y=9.8852e-02 ppl_x2y=1.10 loss_y2x=9.8554e-02 ppl_y2x=1.10 dual_loss=3.7164e-01
Validation X2Y - loss=8.1874e-01 ppl=2.27 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=7.1911e-01 ppl=2.05 best_loss=5.6645e-01 best_ppl=1.76
Epoch 96 - |param|=9.49e+02 |g_param|=5.29e+05 loss_x2y=9.9637e-02 ppl_x2y=1.10 loss_y2x=9.6725e-02 ppl_y2x=1.10 dual_loss=4.2107e-01
Validation X2Y - loss=8.3717e-01 ppl=2.31 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=7.1691e-01 ppl=2.05 best_loss=5.6645e-01 best_ppl=1.76
Epoch 97 - |param|=9.49e+02 |g_param|=5.45e+05 loss_x2y=1.0393e-01 ppl_x2y=1.11 loss_y2x=1.0494e-01 ppl_y2x=1.11 dual_loss=5.2039e-01
Validation X2Y - loss=8.1930e-01 ppl=2.27 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=7.2479e-01 ppl=2.06 best_loss=5.6645e-01 best_ppl=1.76
Epoch 98 - |param|=9.49e+02 |g_param|=5.71e+05 loss_x2y=9.5628e-02 ppl_x2y=1.10 loss_y2x=9.7395e-02 ppl_y2x=1.10 dual_loss=4.3659e-01
Validation X2Y - loss=8.1272e-01 ppl=2.25 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=7.4980e-01 ppl=2.12 best_loss=5.6645e-01 best_ppl=1.76
Epoch 99 - |param|=9.50e+02 |g_param|=4.87e+05 loss_x2y=9.6527e-02 ppl_x2y=1.10 loss_y2x=9.5071e-02 ppl_y2x=1.10 dual_loss=3.8987e-01
Validation X2Y - loss=8.5181e-01 ppl=2.34 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=7.4743e-01 ppl=2.11 best_loss=5.6645e-01 best_ppl=1.76
Epoch 100 - |param|=9.50e+02 |g_param|=4.87e+05 loss_x2y=9.4238e-02 ppl_x2y=1.10 loss_y2x=9.2016e-02 ppl_y2x=1.10 dual_loss=3.7492e-01
Validation X2Y - loss=8.4460e-01 ppl=2.33 best_loss=6.1961e-01 best_ppl=1.86                                            
Validation Y2X - loss=7.3812e-01 ppl=2.09 best_loss=5.6645e-01 best_ppl=1.76

real	52m24.521s
user	51m39.832s
sys	0m45.334s
```

epoch 30 ကနေ 100 အထိ အထက်ပါ training အားလုံးရဲ့ စုစုပေါင်းကြာချိန်က အောက်ပါအတိုင်း...  

```
real	271m25.280s
user	267m0.357s
sys	4m20.127s
```

testing/evaluation ...  

```
/home/ye/exp/simple-nmt/model/dsl/transformer/myrk-100epoch
Evaluation result for the model: dsl-model-myrk.01.3.63-37.55.3.62-37.36.3.10-22.19.3.01-20.37.pth, myrk
BLEU = 5.45, 31.0/11.7/3.1/0.8 (BP=1.000, ratio=1.183, hyp_len=27388, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.01.3.63-37.55.3.62-37.36.3.10-22.19.3.01-20.37.pth, rkmy
BLEU = 4.60, 25.1/9.4/2.7/0.7 (BP=1.000, ratio=1.427, hyp_len=33541, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.02.2.51-12.28.2.46-11.67.2.08-8.03.2.04-7.67.pth, myrk
BLEU = 24.46, 58.1/33.7/19.1/10.4 (BP=0.980, ratio=0.981, hyp_len=22709, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.02.2.51-12.28.2.46-11.67.2.08-8.03.2.04-7.67.pth, rkmy
BLEU = 17.54, 43.1/24.2/13.1/6.9 (BP=1.000, ratio=1.295, hyp_len=30451, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.03.1.82-6.19.1.77-5.90.1.59-4.88.1.47-4.36.pth, myrk
BLEU = 26.70, 49.5/33.2/21.9/14.2 (BP=1.000, ratio=1.393, hyp_len=32259, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.03.1.82-6.19.1.77-5.90.1.59-4.88.1.47-4.36.pth, rkmy
BLEU = 38.69, 66.9/46.9/32.2/22.2 (BP=1.000, ratio=1.028, hyp_len=24174, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.04.1.38-3.96.1.35-3.85.1.19-3.27.1.16-3.18.pth, myrk
BLEU = 48.88, 73.9/56.9/42.8/31.7 (BP=1.000, ratio=1.067, hyp_len=24702, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.04.1.38-3.96.1.35-3.85.1.19-3.27.1.16-3.18.pth, rkmy
BLEU = 48.65, 74.1/56.6/42.2/31.6 (BP=1.000, ratio=1.035, hyp_len=24322, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.05.1.10-3.01.1.09-2.97.1.02-2.77.0.97-2.64.pth, myrk
BLEU = 56.13, 78.9/63.5/50.2/39.5 (BP=1.000, ratio=1.039, hyp_len=24065, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.05.1.10-3.01.1.09-2.97.1.02-2.77.0.97-2.64.pth, rkmy
BLEU = 50.72, 72.6/57.8/45.0/35.1 (BP=1.000, ratio=1.112, hyp_len=26134, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.06.0.99-2.70.0.99-2.69.0.92-2.50.0.88-2.42.pth, myrk
BLEU = 59.39, 80.0/65.6/53.8/44.1 (BP=1.000, ratio=1.046, hyp_len=24217, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.06.0.99-2.70.0.99-2.69.0.92-2.50.0.88-2.42.pth, rkmy
BLEU = 56.04, 78.4/63.7/50.2/39.3 (BP=1.000, ratio=1.053, hyp_len=24750, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.07.0.80-2.22.0.79-2.21.0.85-2.34.0.84-2.31.pth, myrk
BLEU = 59.34, 79.4/65.6/54.0/44.1 (BP=1.000, ratio=1.081, hyp_len=25047, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.07.0.80-2.22.0.79-2.21.0.85-2.34.0.84-2.31.pth, rkmy
BLEU = 57.99, 78.3/64.9/52.6/42.3 (BP=1.000, ratio=1.081, hyp_len=25413, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.08.0.75-2.13.0.76-2.14.0.81-2.26.0.74-2.09.pth, myrk
BLEU = 63.02, 83.3/69.9/57.6/47.1 (BP=1.000, ratio=1.030, hyp_len=23864, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.08.0.75-2.13.0.76-2.14.0.81-2.26.0.74-2.09.pth, rkmy
BLEU = 60.53, 80.4/67.2/55.1/45.1 (BP=1.000, ratio=1.058, hyp_len=24866, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.09.0.69-2.00.0.69-1.99.0.72-2.06.0.69-1.99.pth, myrk
BLEU = 64.88, 84.0/70.9/59.6/49.9 (BP=1.000, ratio=1.039, hyp_len=24058, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.09.0.69-2.00.0.69-1.99.0.72-2.06.0.69-1.99.pth, rkmy
BLEU = 64.62, 83.4/70.6/59.3/49.9 (BP=1.000, ratio=1.031, hyp_len=24237, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.100.0.09-1.10.0.09-1.10.0.84-2.33.0.74-2.09.pth, myrk
BLEU = 69.18, 85.1/73.9/64.6/56.4 (BP=1.000, ratio=1.056, hyp_len=24447, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.100.0.09-1.10.0.09-1.10.0.84-2.33.0.74-2.09.pth, rkmy
BLEU = 70.48, 85.8/75.5/65.9/57.8 (BP=1.000, ratio=1.052, hyp_len=24720, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.10.0.62-1.86.0.62-1.86.0.73-2.06.0.69-2.00.pth, myrk
BLEU = 64.97, 84.2/71.2/59.6/49.9 (BP=1.000, ratio=1.032, hyp_len=23896, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.10.0.62-1.86.0.62-1.86.0.73-2.06.0.69-2.00.pth, rkmy
BLEU = 63.26, 81.7/69.5/58.1/48.6 (BP=1.000, ratio=1.057, hyp_len=24843, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.11.0.56-1.76.0.58-1.78.0.69-2.00.0.68-1.97.pth, myrk
BLEU = 65.74, 84.0/71.5/60.7/51.2 (BP=1.000, ratio=1.039, hyp_len=24070, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.11.0.56-1.76.0.58-1.78.0.69-2.00.0.68-1.97.pth, rkmy
BLEU = 64.67, 82.8/70.8/59.5/50.1 (BP=1.000, ratio=1.047, hyp_len=24622, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.12.0.55-1.73.0.55-1.74.0.68-1.97.0.64-1.90.pth, myrk
BLEU = 68.09, 85.3/73.2/63.0/54.6 (BP=1.000, ratio=1.023, hyp_len=23701, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.12.0.55-1.73.0.55-1.74.0.68-1.97.0.64-1.90.pth, rkmy
BLEU = 64.56, 82.7/70.5/59.3/50.2 (BP=1.000, ratio=1.059, hyp_len=24889, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.13.0.49-1.63.0.47-1.61.0.66-1.93.0.64-1.89.pth, myrk
BLEU = 67.03, 84.3/72.2/62.0/53.5 (BP=1.000, ratio=1.045, hyp_len=24209, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.13.0.49-1.63.0.47-1.61.0.66-1.93.0.64-1.89.pth, rkmy
BLEU = 65.84, 83.1/71.5/60.9/51.9 (BP=1.000, ratio=1.062, hyp_len=24974, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.14.0.50-1.64.0.49-1.63.0.71-2.03.0.65-1.92.pth, myrk
BLEU = 63.70, 81.0/69.1/58.9/49.9 (BP=1.000, ratio=1.087, hyp_len=25171, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.14.0.50-1.64.0.49-1.63.0.71-2.03.0.65-1.92.pth, rkmy
BLEU = 63.71, 81.6/69.5/58.6/49.6 (BP=1.000, ratio=1.073, hyp_len=25215, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.15.0.42-1.52.0.42-1.52.0.64-1.90.0.63-1.88.pth, myrk
BLEU = 68.08, 84.7/73.2/63.3/54.7 (BP=1.000, ratio=1.045, hyp_len=24210, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.15.0.42-1.52.0.42-1.52.0.64-1.90.0.63-1.88.pth, rkmy
BLEU = 66.56, 83.9/72.5/61.6/52.4 (BP=1.000, ratio=1.053, hyp_len=24750, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.16.0.43-1.53.0.43-1.53.0.66-1.94.0.63-1.87.pth, myrk
BLEU = 69.36, 86.0/74.3/64.5/56.1 (BP=1.000, ratio=1.024, hyp_len=23723, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.16.0.43-1.53.0.43-1.53.0.66-1.94.0.63-1.87.pth, rkmy
BLEU = 65.91, 83.0/71.8/61.1/51.9 (BP=1.000, ratio=1.067, hyp_len=25090, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.17.0.40-1.50.0.41-1.51.0.63-1.88.0.61-1.84.pth, myrk
BLEU = 69.88, 85.9/74.9/65.2/56.9 (BP=1.000, ratio=1.028, hyp_len=23803, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.17.0.40-1.50.0.41-1.51.0.63-1.88.0.61-1.84.pth, rkmy
BLEU = 67.83, 84.7/73.1/62.8/54.5 (BP=1.000, ratio=1.047, hyp_len=24623, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.18.0.38-1.46.0.39-1.48.0.64-1.90.0.61-1.84.pth, myrk
BLEU = 68.73, 85.1/73.7/64.0/55.6 (BP=1.000, ratio=1.049, hyp_len=24294, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.18.0.38-1.46.0.39-1.48.0.64-1.90.0.61-1.84.pth, rkmy
BLEU = 66.93, 84.0/72.5/61.9/53.3 (BP=1.000, ratio=1.056, hyp_len=24821, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.19.0.36-1.43.0.36-1.43.0.66-1.93.0.62-1.85.pth, myrk
BLEU = 66.40, 83.0/71.7/61.6/53.0 (BP=1.000, ratio=1.075, hyp_len=24906, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.19.0.36-1.43.0.36-1.43.0.66-1.93.0.62-1.85.pth, rkmy
BLEU = 69.14, 85.3/74.4/64.3/56.0 (BP=1.000, ratio=1.041, hyp_len=24481, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.20.0.36-1.44.0.37-1.44.0.65-1.91.0.62-1.85.pth, myrk
BLEU = 69.18, 85.6/74.1/64.4/56.1 (BP=1.000, ratio=1.035, hyp_len=23971, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.20.0.36-1.44.0.37-1.44.0.65-1.91.0.62-1.85.pth, rkmy
BLEU = 66.82, 84.1/72.8/61.9/52.6 (BP=1.000, ratio=1.057, hyp_len=24845, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.21.0.34-1.41.0.36-1.43.0.66-1.94.0.59-1.80.pth, myrk
BLEU = 68.65, 84.8/73.8/64.0/55.4 (BP=1.000, ratio=1.046, hyp_len=24233, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.21.0.34-1.41.0.36-1.43.0.66-1.94.0.59-1.80.pth, rkmy
BLEU = 67.92, 84.6/73.1/62.9/54.7 (BP=1.000, ratio=1.049, hyp_len=24669, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.22.0.34-1.41.0.35-1.42.0.65-1.92.0.61-1.85.pth, myrk
BLEU = 70.15, 86.2/74.8/65.4/57.4 (BP=1.000, ratio=1.032, hyp_len=23900, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.22.0.34-1.41.0.35-1.42.0.65-1.92.0.61-1.85.pth, rkmy
BLEU = 64.80, 80.5/69.8/60.2/52.2 (BP=1.000, ratio=1.110, hyp_len=26104, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.23.0.32-1.38.0.33-1.38.0.66-1.93.0.60-1.83.pth, myrk
BLEU = 67.54, 84.3/72.7/62.7/54.1 (BP=1.000, ratio=1.047, hyp_len=24256, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.23.0.32-1.38.0.33-1.38.0.66-1.93.0.60-1.83.pth, rkmy
BLEU = 67.43, 83.7/72.7/62.6/54.3 (BP=1.000, ratio=1.067, hyp_len=25079, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.24.0.33-1.39.0.31-1.37.0.64-1.89.0.60-1.81.pth, myrk
BLEU = 68.51, 85.0/73.7/63.8/55.2 (BP=1.000, ratio=1.054, hyp_len=24408, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.24.0.33-1.39.0.31-1.37.0.64-1.89.0.60-1.81.pth, rkmy
BLEU = 70.94, 86.4/75.9/66.2/58.3 (BP=1.000, ratio=1.031, hyp_len=24237, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.25.0.30-1.35.0.32-1.38.0.64-1.90.0.60-1.82.pth, myrk
BLEU = 69.05, 85.5/74.0/64.2/55.9 (BP=1.000, ratio=1.043, hyp_len=24150, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.25.0.30-1.35.0.32-1.38.0.64-1.90.0.60-1.82.pth, rkmy
BLEU = 69.28, 85.3/74.4/64.4/56.3 (BP=1.000, ratio=1.047, hyp_len=24604, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.26.0.29-1.33.0.29-1.33.0.62-1.86.0.62-1.86.pth, myrk
BLEU = 69.73, 85.8/74.5/65.0/56.9 (BP=1.000, ratio=1.039, hyp_len=24061, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.26.0.29-1.33.0.29-1.33.0.62-1.86.0.62-1.86.pth, rkmy
BLEU = 68.85, 85.0/74.2/64.1/55.6 (BP=1.000, ratio=1.049, hyp_len=24672, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.27.0.29-1.34.0.29-1.33.0.63-1.88.0.59-1.80.pth, myrk
BLEU = 70.13, 85.9/75.0/65.5/57.4 (BP=1.000, ratio=1.041, hyp_len=24102, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.27.0.29-1.34.0.29-1.33.0.63-1.88.0.59-1.80.pth, rkmy
BLEU = 70.06, 85.8/75.1/65.2/57.3 (BP=1.000, ratio=1.043, hyp_len=24509, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.28.0.28-1.33.0.29-1.33.0.65-1.91.0.59-1.80.pth, myrk
BLEU = 71.01, 86.3/75.6/66.5/58.6 (BP=1.000, ratio=1.028, hyp_len=23809, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.28.0.28-1.33.0.29-1.33.0.65-1.91.0.59-1.80.pth, rkmy
BLEU = 67.16, 83.7/72.6/62.3/53.7 (BP=1.000, ratio=1.072, hyp_len=25209, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.29.0.28-1.32.0.28-1.32.0.64-1.89.0.60-1.83.pth, myrk
BLEU = 70.19, 86.2/75.1/65.5/57.3 (BP=1.000, ratio=1.040, hyp_len=24092, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.29.0.28-1.32.0.28-1.32.0.64-1.89.0.60-1.83.pth, rkmy
BLEU = 68.95, 85.1/74.3/64.2/55.7 (BP=1.000, ratio=1.046, hyp_len=24579, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.30.0.26-1.29.0.25-1.29.0.67-1.95.0.62-1.86.pth, myrk
BLEU = 68.59, 85.0/73.7/64.0/55.2 (BP=1.000, ratio=1.050, hyp_len=24326, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.30.0.26-1.29.0.25-1.29.0.67-1.95.0.62-1.86.pth, rkmy
BLEU = 69.54, 85.0/74.4/64.9/57.0 (BP=1.000, ratio=1.051, hyp_len=24704, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.31.0.25-1.29.0.24-1.28.0.65-1.92.0.57-1.77.pth, myrk
BLEU = 69.80, 85.4/74.4/65.2/57.2 (BP=1.000, ratio=1.045, hyp_len=24192, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.31.0.25-1.29.0.24-1.28.0.65-1.92.0.57-1.77.pth, rkmy
BLEU = 68.86, 84.7/74.0/64.1/55.9 (BP=1.000, ratio=1.057, hyp_len=24846, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.32.0.25-1.28.0.25-1.29.0.66-1.94.0.59-1.80.pth, myrk
BLEU = 68.16, 84.9/73.4/63.4/54.7 (BP=1.000, ratio=1.045, hyp_len=24212, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.32.0.25-1.28.0.25-1.29.0.66-1.94.0.59-1.80.pth, rkmy
BLEU = 66.38, 82.4/71.5/61.6/53.5 (BP=1.000, ratio=1.087, hyp_len=25550, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.33.0.23-1.26.0.24-1.27.0.67-1.95.0.59-1.81.pth, myrk
BLEU = 69.97, 85.9/74.8/65.3/57.0 (BP=1.000, ratio=1.039, hyp_len=24073, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.33.0.23-1.26.0.24-1.27.0.67-1.95.0.59-1.81.pth, rkmy
BLEU = 69.54, 85.2/74.6/64.9/56.8 (BP=1.000, ratio=1.046, hyp_len=24594, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.34.0.23-1.26.0.23-1.26.0.66-1.94.0.57-1.77.pth, myrk
BLEU = 69.33, 85.3/74.1/64.7/56.5 (BP=1.000, ratio=1.045, hyp_len=24192, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.34.0.23-1.26.0.23-1.26.0.66-1.94.0.57-1.77.pth, rkmy
BLEU = 70.46, 85.9/75.4/65.8/57.9 (BP=1.000, ratio=1.045, hyp_len=24563, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.35.0.23-1.26.0.23-1.25.0.66-1.93.0.57-1.76.pth, myrk
BLEU = 70.59, 86.2/75.3/66.0/57.9 (BP=1.000, ratio=1.038, hyp_len=24034, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.35.0.23-1.26.0.23-1.25.0.66-1.93.0.57-1.76.pth, rkmy
BLEU = 69.48, 85.5/74.4/64.6/56.7 (BP=1.000, ratio=1.049, hyp_len=24667, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.36.0.23-1.25.0.23-1.26.0.67-1.95.0.59-1.81.pth, myrk
BLEU = 70.13, 86.0/74.8/65.4/57.5 (BP=1.000, ratio=1.043, hyp_len=24158, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.36.0.23-1.25.0.23-1.26.0.67-1.95.0.59-1.81.pth, rkmy
BLEU = 69.63, 85.5/74.8/64.9/56.6 (BP=1.000, ratio=1.051, hyp_len=24717, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.37.0.22-1.24.0.21-1.24.0.67-1.95.0.59-1.81.pth, myrk
BLEU = 67.69, 83.8/72.6/63.1/54.7 (BP=1.000, ratio=1.063, hyp_len=24628, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.37.0.22-1.24.0.21-1.24.0.67-1.95.0.59-1.81.pth, rkmy
BLEU = 67.82, 84.3/73.2/63.0/54.4 (BP=1.000, ratio=1.063, hyp_len=24994, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.38.0.21-1.24.0.21-1.23.0.67-1.96.0.60-1.83.pth, myrk
BLEU = 70.11, 86.2/74.9/65.4/57.2 (BP=1.000, ratio=1.036, hyp_len=23998, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.38.0.21-1.24.0.21-1.23.0.67-1.96.0.60-1.83.pth, rkmy
BLEU = 66.18, 82.5/71.4/61.3/53.1 (BP=1.000, ratio=1.082, hyp_len=25438, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.39.0.20-1.22.0.21-1.23.0.67-1.95.0.59-1.81.pth, myrk
BLEU = 69.70, 85.4/74.5/65.2/57.0 (BP=1.000, ratio=1.044, hyp_len=24172, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.39.0.20-1.22.0.21-1.23.0.67-1.95.0.59-1.81.pth, rkmy
BLEU = 69.07, 85.1/74.1/64.2/56.2 (BP=1.000, ratio=1.052, hyp_len=24721, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.40.0.20-1.23.0.21-1.23.0.68-1.97.0.62-1.86.pth, myrk
BLEU = 69.67, 85.6/74.6/65.0/56.7 (BP=1.000, ratio=1.046, hyp_len=24226, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.40.0.20-1.23.0.21-1.23.0.68-1.97.0.62-1.86.pth, rkmy
BLEU = 70.94, 86.3/75.7/66.2/58.6 (BP=1.000, ratio=1.040, hyp_len=24452, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.41.0.19-1.21.0.20-1.22.0.67-1.96.0.62-1.86.pth, myrk
BLEU = 68.85, 84.9/73.8/64.3/55.8 (BP=1.000, ratio=1.051, hyp_len=24333, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.41.0.19-1.21.0.20-1.22.0.67-1.96.0.62-1.86.pth, rkmy
BLEU = 70.61, 86.0/75.5/65.9/58.1 (BP=1.000, ratio=1.041, hyp_len=24462, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.42.0.19-1.21.0.19-1.21.0.71-2.03.0.60-1.82.pth, myrk
BLEU = 70.64, 86.0/75.0/66.1/58.4 (BP=1.000, ratio=1.032, hyp_len=23899, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.42.0.19-1.21.0.19-1.21.0.71-2.03.0.60-1.82.pth, rkmy
BLEU = 68.37, 84.8/73.7/63.4/55.1 (BP=1.000, ratio=1.057, hyp_len=24852, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.43.0.20-1.22.0.19-1.21.0.67-1.95.0.64-1.89.pth, myrk
BLEU = 70.00, 85.6/74.7/65.4/57.4 (BP=1.000, ratio=1.041, hyp_len=24115, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.43.0.20-1.22.0.19-1.21.0.67-1.95.0.64-1.89.pth, rkmy
BLEU = 68.13, 84.4/73.3/63.2/55.1 (BP=1.000, ratio=1.059, hyp_len=24905, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.44.0.19-1.21.0.19-1.21.0.68-1.98.0.61-1.84.pth, myrk
BLEU = 69.28, 85.3/74.1/64.6/56.5 (BP=1.000, ratio=1.047, hyp_len=24252, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.44.0.19-1.21.0.19-1.21.0.68-1.98.0.61-1.84.pth, rkmy
BLEU = 69.46, 84.9/74.3/64.8/56.9 (BP=1.000, ratio=1.059, hyp_len=24890, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.45.0.19-1.21.0.19-1.21.0.70-2.01.0.64-1.90.pth, myrk
BLEU = 70.41, 86.2/75.1/65.8/57.8 (BP=1.000, ratio=1.037, hyp_len=24014, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.45.0.19-1.21.0.19-1.21.0.70-2.01.0.64-1.90.pth, rkmy
BLEU = 68.91, 84.8/73.9/64.0/56.2 (BP=1.000, ratio=1.059, hyp_len=24895, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.46.0.18-1.19.0.17-1.19.0.71-2.03.0.62-1.86.pth, myrk
BLEU = 70.51, 86.2/75.2/65.8/58.0 (BP=1.000, ratio=1.038, hyp_len=24050, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.46.0.18-1.19.0.17-1.19.0.71-2.03.0.62-1.86.pth, rkmy
BLEU = 69.14, 85.0/74.2/64.3/56.3 (BP=1.000, ratio=1.058, hyp_len=24879, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.47.0.18-1.20.0.18-1.19.0.70-2.02.0.60-1.83.pth, myrk
BLEU = 69.95, 85.6/74.6/65.3/57.4 (BP=1.000, ratio=1.046, hyp_len=24224, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.47.0.18-1.20.0.18-1.19.0.70-2.02.0.60-1.83.pth, rkmy
BLEU = 69.13, 85.1/74.1/64.3/56.4 (BP=1.000, ratio=1.053, hyp_len=24744, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.48.0.18-1.19.0.17-1.19.0.70-2.02.0.60-1.83.pth, myrk
BLEU = 70.11, 85.9/74.8/65.5/57.4 (BP=1.000, ratio=1.041, hyp_len=24112, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.48.0.18-1.19.0.17-1.19.0.70-2.02.0.60-1.83.pth, rkmy
BLEU = 67.19, 83.9/72.5/62.2/53.8 (BP=1.000, ratio=1.066, hyp_len=25067, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.49.0.17-1.19.0.17-1.18.0.71-2.04.0.62-1.86.pth, myrk
BLEU = 69.09, 85.3/73.9/64.3/56.2 (BP=1.000, ratio=1.045, hyp_len=24206, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.49.0.17-1.19.0.17-1.18.0.71-2.04.0.62-1.86.pth, rkmy
BLEU = 69.17, 84.9/74.2/64.4/56.4 (BP=1.000, ratio=1.059, hyp_len=24902, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.50.0.17-1.18.0.17-1.18.0.74-2.09.0.63-1.88.pth, myrk
BLEU = 69.64, 85.7/74.4/64.9/56.8 (BP=1.000, ratio=1.040, hyp_len=24082, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.50.0.17-1.18.0.17-1.18.0.74-2.09.0.63-1.88.pth, rkmy
BLEU = 70.23, 85.8/75.2/65.5/57.5 (BP=1.000, ratio=1.051, hyp_len=24712, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.51.0.17-1.18.0.17-1.18.0.72-2.05.0.62-1.86.pth, myrk
BLEU = 70.06, 85.9/74.8/65.4/57.4 (BP=1.000, ratio=1.043, hyp_len=24164, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.51.0.17-1.18.0.17-1.18.0.72-2.05.0.62-1.86.pth, rkmy
BLEU = 69.33, 85.1/74.3/64.6/56.6 (BP=1.000, ratio=1.056, hyp_len=24836, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.52.0.17-1.18.0.17-1.18.0.69-2.00.0.64-1.89.pth, myrk
BLEU = 69.43, 85.1/74.2/64.9/56.8 (BP=1.000, ratio=1.047, hyp_len=24251, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.52.0.17-1.18.0.17-1.18.0.69-2.00.0.64-1.89.pth, rkmy
BLEU = 69.48, 85.4/74.5/64.6/56.7 (BP=1.000, ratio=1.051, hyp_len=24717, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.53.0.16-1.17.0.17-1.18.0.72-2.06.0.63-1.87.pth, myrk
BLEU = 70.44, 85.9/74.9/65.8/58.2 (BP=1.000, ratio=1.040, hyp_len=24083, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.53.0.16-1.17.0.17-1.18.0.72-2.06.0.63-1.87.pth, rkmy
BLEU = 67.75, 83.8/72.8/62.9/54.9 (BP=1.000, ratio=1.071, hyp_len=25179, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.54.0.16-1.17.0.16-1.17.0.69-1.99.0.64-1.89.pth, myrk
BLEU = 70.45, 85.9/75.0/65.9/58.0 (BP=1.000, ratio=1.041, hyp_len=24107, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.54.0.16-1.17.0.16-1.17.0.69-1.99.0.64-1.89.pth, rkmy
BLEU = 68.75, 84.9/73.9/63.9/55.8 (BP=1.000, ratio=1.057, hyp_len=24842, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.55.0.16-1.17.0.16-1.17.0.71-2.04.0.64-1.89.pth, myrk
BLEU = 70.77, 86.1/75.4/66.2/58.4 (BP=1.000, ratio=1.037, hyp_len=24022, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.55.0.16-1.17.0.16-1.17.0.71-2.04.0.64-1.89.pth, rkmy
BLEU = 68.13, 84.4/73.3/63.3/55.1 (BP=1.000, ratio=1.064, hyp_len=25010, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.56.0.16-1.17.0.15-1.16.0.73-2.08.0.62-1.87.pth, myrk
BLEU = 64.76, 80.4/69.4/60.3/52.3 (BP=1.000, ratio=1.111, hyp_len=25726, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.56.0.16-1.17.0.15-1.16.0.73-2.08.0.62-1.87.pth, rkmy
BLEU = 68.09, 84.4/73.2/63.2/55.0 (BP=1.000, ratio=1.065, hyp_len=25046, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.57.0.16-1.17.0.15-1.16.0.73-2.08.0.65-1.91.pth, myrk
BLEU = 69.92, 85.6/74.6/65.3/57.3 (BP=1.000, ratio=1.045, hyp_len=24201, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.57.0.16-1.17.0.15-1.16.0.73-2.08.0.65-1.91.pth, rkmy
BLEU = 68.92, 84.8/74.1/64.2/56.0 (BP=1.000, ratio=1.062, hyp_len=24959, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.58.0.15-1.17.0.16-1.17.0.74-2.09.0.64-1.90.pth, myrk
BLEU = 69.30, 84.8/73.9/64.8/56.8 (BP=1.000, ratio=1.052, hyp_len=24360, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.58.0.15-1.17.0.16-1.17.0.74-2.09.0.64-1.90.pth, rkmy
BLEU = 70.33, 85.8/75.2/65.6/57.8 (BP=1.000, ratio=1.052, hyp_len=24733, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.59.0.15-1.16.0.15-1.16.0.73-2.07.0.64-1.90.pth, myrk
BLEU = 67.10, 82.6/71.7/62.6/54.7 (BP=1.000, ratio=1.086, hyp_len=25143, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.59.0.15-1.16.0.15-1.16.0.73-2.07.0.64-1.90.pth, rkmy
BLEU = 70.63, 85.9/75.5/66.0/58.2 (BP=1.000, ratio=1.046, hyp_len=24601, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.60.0.14-1.16.0.15-1.16.0.72-2.05.0.65-1.91.pth, myrk
BLEU = 69.12, 84.5/73.6/64.6/56.8 (BP=1.000, ratio=1.059, hyp_len=24522, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.60.0.14-1.16.0.15-1.16.0.72-2.05.0.65-1.91.pth, rkmy
BLEU = 69.44, 84.9/74.4/64.8/56.8 (BP=1.000, ratio=1.062, hyp_len=24971, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.61.0.14-1.15.0.15-1.16.0.74-2.09.0.65-1.91.pth, myrk
BLEU = 70.58, 85.9/75.0/66.0/58.3 (BP=1.000, ratio=1.035, hyp_len=23978, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.61.0.14-1.15.0.15-1.16.0.74-2.09.0.65-1.91.pth, rkmy
BLEU = 68.97, 84.5/73.9/64.4/56.3 (BP=1.000, ratio=1.061, hyp_len=24947, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.62.0.15-1.16.0.14-1.15.0.73-2.08.0.66-1.93.pth, myrk
BLEU = 70.05, 85.5/74.6/65.5/57.6 (BP=1.000, ratio=1.041, hyp_len=24114, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.62.0.15-1.16.0.14-1.15.0.73-2.08.0.66-1.93.pth, rkmy
BLEU = 68.14, 84.4/73.2/63.3/55.1 (BP=1.000, ratio=1.067, hyp_len=25086, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.63.0.13-1.14.0.14-1.14.0.73-2.08.0.64-1.90.pth, myrk
BLEU = 71.27, 86.1/75.6/66.9/59.2 (BP=1.000, ratio=1.039, hyp_len=24055, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.63.0.13-1.14.0.14-1.14.0.73-2.08.0.64-1.90.pth, rkmy
BLEU = 69.67, 85.4/74.7/64.9/56.9 (BP=1.000, ratio=1.053, hyp_len=24755, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.64.0.14-1.15.0.14-1.15.0.74-2.10.0.68-1.97.pth, myrk
BLEU = 70.96, 86.2/75.4/66.4/58.7 (BP=1.000, ratio=1.041, hyp_len=24121, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.64.0.14-1.15.0.14-1.15.0.74-2.10.0.68-1.97.pth, rkmy
BLEU = 67.92, 83.8/73.2/63.2/54.9 (BP=1.000, ratio=1.073, hyp_len=25233, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.65.0.13-1.14.0.13-1.14.0.75-2.11.0.70-2.01.pth, myrk
BLEU = 70.15, 85.7/74.8/65.6/57.6 (BP=1.000, ratio=1.044, hyp_len=24189, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.65.0.13-1.14.0.13-1.14.0.75-2.11.0.70-2.01.pth, rkmy
BLEU = 69.69, 84.8/74.4/65.1/57.4 (BP=1.000, ratio=1.061, hyp_len=24949, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.66.0.13-1.14.0.14-1.16.0.75-2.11.0.66-1.93.pth, myrk
BLEU = 70.89, 86.2/75.4/66.4/58.6 (BP=1.000, ratio=1.041, hyp_len=24116, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.66.0.13-1.14.0.14-1.16.0.75-2.11.0.66-1.93.pth, rkmy
BLEU = 68.60, 84.7/73.8/63.8/55.5 (BP=1.000, ratio=1.063, hyp_len=24980, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.67.0.14-1.15.0.13-1.14.0.76-2.15.0.66-1.93.pth, myrk
BLEU = 70.04, 85.6/74.6/65.4/57.6 (BP=1.000, ratio=1.040, hyp_len=24092, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.67.0.14-1.15.0.13-1.14.0.76-2.15.0.66-1.93.pth, rkmy
BLEU = 69.94, 85.4/74.8/65.2/57.5 (BP=1.000, ratio=1.053, hyp_len=24760, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.68.0.13-1.14.0.12-1.13.0.76-2.14.0.67-1.96.pth, myrk
BLEU = 70.31, 85.6/74.9/65.8/58.0 (BP=1.000, ratio=1.042, hyp_len=24143, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.68.0.13-1.14.0.12-1.13.0.76-2.14.0.67-1.96.pth, rkmy
BLEU = 68.63, 84.5/73.7/63.8/55.9 (BP=1.000, ratio=1.071, hyp_len=25170, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.69.0.14-1.15.0.13-1.14.0.75-2.13.0.66-1.93.pth, myrk
BLEU = 69.11, 84.9/73.9/64.5/56.4 (BP=1.000, ratio=1.045, hyp_len=24202, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.69.0.14-1.15.0.13-1.14.0.75-2.13.0.66-1.93.pth, rkmy
BLEU = 68.32, 84.3/73.3/63.4/55.6 (BP=1.000, ratio=1.063, hyp_len=25001, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.70.0.13-1.14.0.13-1.14.0.76-2.14.0.67-1.95.pth, myrk
BLEU = 70.28, 85.9/75.0/65.7/57.7 (BP=1.000, ratio=1.043, hyp_len=24154, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.70.0.13-1.14.0.13-1.14.0.76-2.14.0.67-1.95.pth, rkmy
BLEU = 70.20, 85.2/74.9/65.6/57.9 (BP=1.000, ratio=1.057, hyp_len=24839, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.71.0.13-1.14.0.13-1.14.0.76-2.14.0.64-1.90.pth, myrk
BLEU = 69.62, 85.1/74.4/65.2/57.0 (BP=1.000, ratio=1.053, hyp_len=24379, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.71.0.13-1.14.0.13-1.14.0.76-2.14.0.64-1.90.pth, rkmy
BLEU = 70.10, 85.6/75.0/65.4/57.5 (BP=1.000, ratio=1.054, hyp_len=24784, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.72.0.13-1.14.0.12-1.13.0.76-2.15.0.65-1.91.pth, myrk
BLEU = 70.97, 86.1/75.5/66.5/58.7 (BP=1.000, ratio=1.039, hyp_len=24060, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.72.0.13-1.14.0.12-1.13.0.76-2.15.0.65-1.91.pth, rkmy
BLEU = 69.85, 85.3/74.7/65.1/57.3 (BP=1.000, ratio=1.054, hyp_len=24781, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.73.0.12-1.13.0.12-1.13.0.75-2.11.0.68-1.97.pth, myrk
BLEU = 70.89, 86.1/75.4/66.4/58.6 (BP=1.000, ratio=1.038, hyp_len=24039, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.73.0.12-1.13.0.12-1.13.0.75-2.11.0.68-1.97.pth, rkmy
BLEU = 69.07, 84.8/74.0/64.3/56.4 (BP=1.000, ratio=1.061, hyp_len=24933, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.74.0.12-1.13.0.12-1.13.0.78-2.17.0.66-1.94.pth, myrk
BLEU = 69.96, 85.5/74.5/65.4/57.5 (BP=1.000, ratio=1.045, hyp_len=24211, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.74.0.12-1.13.0.12-1.13.0.78-2.17.0.66-1.94.pth, rkmy
BLEU = 69.89, 85.4/74.8/65.2/57.3 (BP=1.000, ratio=1.058, hyp_len=24874, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.75.0.12-1.12.0.12-1.12.0.77-2.16.0.70-2.02.pth, myrk
BLEU = 69.20, 84.5/73.6/64.7/57.0 (BP=1.000, ratio=1.059, hyp_len=24515, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.75.0.12-1.12.0.12-1.12.0.77-2.16.0.70-2.02.pth, rkmy
BLEU = 71.13, 86.0/75.8/66.6/59.0 (BP=1.000, ratio=1.046, hyp_len=24582, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.76.0.12-1.13.0.12-1.13.0.77-2.16.0.67-1.95.pth, myrk
BLEU = 70.30, 85.7/74.9/65.8/57.8 (BP=1.000, ratio=1.045, hyp_len=24206, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.76.0.12-1.13.0.12-1.13.0.77-2.16.0.67-1.95.pth, rkmy
BLEU = 69.08, 84.8/74.1/64.4/56.2 (BP=1.000, ratio=1.062, hyp_len=24959, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.77.0.12-1.13.0.12-1.13.0.78-2.19.0.69-1.99.pth, myrk
BLEU = 69.60, 85.6/74.3/64.9/56.8 (BP=1.000, ratio=1.045, hyp_len=24191, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.77.0.12-1.13.0.12-1.13.0.78-2.19.0.69-1.99.pth, rkmy
BLEU = 69.37, 84.9/74.3/64.6/56.8 (BP=1.000, ratio=1.062, hyp_len=24959, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.78.0.12-1.12.0.11-1.12.0.76-2.14.0.68-1.98.pth, myrk
BLEU = 69.46, 85.2/74.1/64.8/56.9 (BP=1.000, ratio=1.052, hyp_len=24355, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.78.0.12-1.12.0.11-1.12.0.76-2.14.0.68-1.98.pth, rkmy
BLEU = 71.00, 86.1/75.8/66.4/58.7 (BP=1.000, ratio=1.048, hyp_len=24637, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.79.0.12-1.12.0.11-1.12.0.78-2.18.0.69-1.99.pth, myrk
BLEU = 70.37, 85.8/75.0/65.9/57.9 (BP=1.000, ratio=1.044, hyp_len=24188, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.79.0.12-1.12.0.11-1.12.0.78-2.18.0.69-1.99.pth, rkmy
BLEU = 70.10, 85.4/74.9/65.5/57.6 (BP=1.000, ratio=1.058, hyp_len=24869, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.80.0.11-1.12.0.12-1.12.0.77-2.16.0.67-1.96.pth, myrk
BLEU = 70.26, 85.6/74.7/65.8/57.9 (BP=1.000, ratio=1.044, hyp_len=24172, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.80.0.11-1.12.0.12-1.12.0.77-2.16.0.67-1.96.pth, rkmy
BLEU = 69.72, 85.3/74.6/64.9/57.1 (BP=1.000, ratio=1.055, hyp_len=24803, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.81.0.11-1.12.0.11-1.12.0.78-2.18.0.68-1.98.pth, myrk
BLEU = 69.45, 84.8/74.0/64.9/57.2 (BP=1.000, ratio=1.058, hyp_len=24503, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.81.0.11-1.12.0.11-1.12.0.78-2.18.0.68-1.98.pth, rkmy
BLEU = 66.83, 82.2/71.6/62.3/54.4 (BP=1.000, ratio=1.096, hyp_len=25771, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.82.0.11-1.12.0.11-1.12.0.78-2.18.0.69-1.98.pth, myrk
BLEU = 69.62, 85.2/74.3/65.1/57.0 (BP=1.000, ratio=1.050, hyp_len=24314, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.82.0.11-1.12.0.11-1.12.0.78-2.18.0.69-1.98.pth, rkmy
BLEU = 69.63, 85.4/74.7/64.9/56.8 (BP=1.000, ratio=1.059, hyp_len=24885, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.83.0.11-1.12.0.11-1.12.0.80-2.22.0.68-1.97.pth, myrk
BLEU = 70.08, 85.5/74.6/65.6/57.6 (BP=1.000, ratio=1.046, hyp_len=24214, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.83.0.11-1.12.0.11-1.12.0.80-2.22.0.68-1.97.pth, rkmy
BLEU = 69.69, 85.2/74.5/65.0/57.2 (BP=1.000, ratio=1.060, hyp_len=24909, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.84.0.11-1.12.0.11-1.11.0.79-2.20.0.71-2.02.pth, myrk
BLEU = 68.95, 84.4/73.4/64.4/56.7 (BP=1.000, ratio=1.064, hyp_len=24635, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.84.0.11-1.12.0.11-1.11.0.79-2.20.0.71-2.02.pth, rkmy
BLEU = 69.78, 85.2/74.7/65.1/57.2 (BP=1.000, ratio=1.058, hyp_len=24876, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.85.0.11-1.12.0.11-1.12.0.79-2.20.0.71-2.03.pth, myrk
BLEU = 71.18, 86.3/75.6/66.7/58.9 (BP=1.000, ratio=1.038, hyp_len=24050, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.85.0.11-1.12.0.11-1.12.0.79-2.20.0.71-2.03.pth, rkmy
BLEU = 70.19, 85.4/74.9/65.5/57.9 (BP=1.000, ratio=1.056, hyp_len=24834, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.86.0.11-1.12.0.11-1.11.0.80-2.23.0.70-2.02.pth, myrk
BLEU = 69.37, 85.2/74.0/64.8/56.7 (BP=1.000, ratio=1.051, hyp_len=24331, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.86.0.11-1.12.0.11-1.11.0.80-2.23.0.70-2.02.pth, rkmy
BLEU = 70.59, 86.0/75.4/65.8/58.1 (BP=1.000, ratio=1.051, hyp_len=24719, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.87.0.11-1.11.0.11-1.11.0.79-2.20.0.70-2.02.pth, myrk
BLEU = 67.10, 82.5/71.7/62.6/54.7 (BP=1.000, ratio=1.092, hyp_len=25282, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.87.0.11-1.11.0.11-1.11.0.79-2.20.0.70-2.02.pth, rkmy
BLEU = 68.60, 84.7/73.8/63.8/55.5 (BP=1.000, ratio=1.067, hyp_len=25087, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.88.0.11-1.12.0.11-1.11.0.80-2.22.0.70-2.01.pth, myrk
BLEU = 69.51, 85.1/74.1/65.0/56.9 (BP=1.000, ratio=1.049, hyp_len=24292, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.88.0.11-1.12.0.11-1.11.0.80-2.22.0.70-2.01.pth, rkmy
BLEU = 70.08, 85.3/74.8/65.5/57.8 (BP=1.000, ratio=1.062, hyp_len=24968, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.89.0.11-1.11.0.10-1.11.0.79-2.19.0.73-2.07.pth, myrk
BLEU = 70.33, 85.6/74.8/65.9/58.0 (BP=1.000, ratio=1.044, hyp_len=24187, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.89.0.11-1.11.0.10-1.11.0.79-2.19.0.73-2.07.pth, rkmy
BLEU = 68.85, 84.5/73.6/64.1/56.3 (BP=1.000, ratio=1.065, hyp_len=25036, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.90.0.10-1.11.0.11-1.11.0.78-2.17.0.72-2.06.pth, myrk
BLEU = 69.27, 84.6/73.9/64.8/56.8 (BP=1.000, ratio=1.054, hyp_len=24418, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.90.0.10-1.11.0.11-1.11.0.78-2.17.0.72-2.06.pth, rkmy
BLEU = 70.70, 85.9/75.4/66.0/58.4 (BP=1.000, ratio=1.049, hyp_len=24668, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.91.0.10-1.11.0.10-1.11.0.78-2.18.0.73-2.07.pth, myrk
BLEU = 69.22, 85.1/74.1/64.7/56.3 (BP=1.000, ratio=1.052, hyp_len=24375, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.91.0.10-1.11.0.10-1.11.0.78-2.18.0.73-2.07.pth, rkmy
BLEU = 70.44, 85.5/75.1/65.8/58.2 (BP=1.000, ratio=1.056, hyp_len=24830, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.92.0.10-1.11.0.10-1.11.0.80-2.22.0.73-2.07.pth, myrk
BLEU = 68.46, 84.2/73.2/63.9/55.7 (BP=1.000, ratio=1.057, hyp_len=24489, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.92.0.10-1.11.0.10-1.11.0.80-2.22.0.73-2.07.pth, rkmy
BLEU = 69.26, 85.0/74.2/64.5/56.5 (BP=1.000, ratio=1.059, hyp_len=24892, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.93.0.10-1.11.0.10-1.10.0.81-2.24.0.72-2.06.pth, myrk
BLEU = 68.52, 84.3/73.1/63.9/55.9 (BP=1.000, ratio=1.060, hyp_len=24542, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.93.0.10-1.11.0.10-1.10.0.81-2.24.0.72-2.06.pth, rkmy
BLEU = 69.52, 85.1/74.3/64.8/57.0 (BP=1.000, ratio=1.059, hyp_len=24885, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.94.0.11-1.11.0.10-1.11.0.79-2.21.0.74-2.10.pth, myrk
BLEU = 69.40, 85.1/74.1/64.9/56.7 (BP=1.000, ratio=1.053, hyp_len=24394, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.94.0.11-1.11.0.10-1.11.0.79-2.21.0.74-2.10.pth, rkmy
BLEU = 70.47, 85.6/75.2/65.8/58.2 (BP=1.000, ratio=1.054, hyp_len=24785, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.95.0.10-1.10.0.10-1.10.0.82-2.27.0.72-2.05.pth, myrk
BLEU = 69.24, 85.2/74.0/64.7/56.4 (BP=1.000, ratio=1.053, hyp_len=24380, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.95.0.10-1.10.0.10-1.10.0.82-2.27.0.72-2.05.pth, rkmy
BLEU = 70.64, 85.9/75.4/65.9/58.3 (BP=1.000, ratio=1.050, hyp_len=24690, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.96.0.10-1.10.0.10-1.10.0.84-2.31.0.72-2.05.pth, myrk
BLEU = 69.82, 85.5/74.4/65.2/57.3 (BP=1.000, ratio=1.049, hyp_len=24293, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.96.0.10-1.10.0.10-1.10.0.84-2.31.0.72-2.05.pth, rkmy
BLEU = 69.60, 85.0/74.4/64.9/57.1 (BP=1.000, ratio=1.061, hyp_len=24942, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.97.0.10-1.11.0.10-1.11.0.82-2.27.0.72-2.06.pth, myrk
BLEU = 69.20, 85.2/73.9/64.6/56.4 (BP=1.000, ratio=1.053, hyp_len=24380, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.97.0.10-1.11.0.10-1.11.0.82-2.27.0.72-2.06.pth, rkmy
BLEU = 69.88, 85.5/74.9/65.1/57.2 (BP=1.000, ratio=1.056, hyp_len=24818, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.98.0.10-1.10.0.10-1.10.0.81-2.25.0.75-2.12.pth, myrk
BLEU = 69.67, 85.5/74.4/65.0/57.0 (BP=1.000, ratio=1.047, hyp_len=24246, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.98.0.10-1.10.0.10-1.10.0.81-2.25.0.75-2.12.pth, rkmy
BLEU = 71.50, 86.3/76.1/67.0/59.5 (BP=1.000, ratio=1.049, hyp_len=24667, ref_len=23509)
Evaluation result for the model: dsl-model-myrk.99.0.10-1.10.0.10-1.10.0.85-2.34.0.75-2.11.pth, myrk
BLEU = 70.09, 85.6/74.7/65.5/57.6 (BP=1.000, ratio=1.044, hyp_len=24186, ref_len=23160)
Evaluation result for the model: dsl-model-myrk.99.0.10-1.10.0.10-1.10.0.85-2.34.0.75-2.11.pth, rkmy
BLEU = 70.87, 86.0/75.8/66.2/58.5 (BP=1.000, ratio=1.051, hyp_len=24717, ref_len=23509)
==========
```

transformer-DSL ရဲ့ testing/evaluation အားလုံးအတွက် (i.e. 30 epochs to 100 epochs) စုစုပေါင်းကြာချိန်က အောက်ပါအတိုင်းပါ။  

```
real	583m5.174s
user	572m39.350s
sys	22m30.684s

```

## DSL-NMT Performance for My-RK 

### Update the test-eval shell script

အထက်မှာ ဖော်ပြထားတဲ့ transformer-DSL BLEU Score တွေကို ရဖို့အတွက် သုံးခဲ့တဲ့ bash shell script ပါ။  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Last Updated: 23 Mar 2022
# find all models and parse to translate.py for testing and multi-bleu.perl for evaluation with BLEU score
# used for transformer-DSL evaluation

for folder in {myrk-30epoch,myrk-40epoch,myrk-50epoch,myrk-60epoch,myrk-70epoch,myrk-80epoch,myrk-90epoch,myrk-100epoch};
do
   cd ./model/dsl/transformer/${folder};
   pwd;
   for i in *.pth;
   do
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
   cd ~/exp/simple-nmt/;
   echo "==========";
done
```

ဇယားနဲ့ ပြမယ်လို့ စိတ်ကူးထား ...  


## Preparation for Myanmar-Beik Language Pair

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

   
## Reference

- [https://stackoverflow.com/questions/42703500/best-way-to-save-a-trained-model-in-pytorch](https://stackoverflow.com/questions/42703500/best-way-to-save-a-trained-model-in-pytorch)
- [(Yingce Xia et. al, 2017, Dual Supervised Learning)](https://arxiv.org/pdf/1707.00415.pdf)  
