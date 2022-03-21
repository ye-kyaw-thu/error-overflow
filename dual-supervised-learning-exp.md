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




#### Warmup-Epoch 20, Total Epoch 60





#### Warmup-Epoch 20, Total Epoch 70



#### Warmup-Epoch 20, Total Epoch 80




#### Warmup-Epoch 20, Total Epoch 90




#### Warmup-Epoch 20, Total Epoch 100




## DSL with Transformer

### with LM 200 Epoch

#### Warmup-Epoch 20, Total Epoch 30


#### Warmup-Epoch 20, Total Epoch 40



#### Warmup-Epoch 20, Total Epoch 50



#### Warmup-Epoch 20, Total Epoch 60


#### Warmup-Epoch 20, Total Epoch 70


#### Warmup-Epoch 20, Total Epoch 80



#### Warmup-Epoch 20, Total Epoch 90


#### Warmup-Epoch 20, Total Epoch 100




## Reference

- [https://stackoverflow.com/questions/42703500/best-way-to-save-a-trained-model-in-pytorch](https://stackoverflow.com/questions/42703500/best-way-to-save-a-trained-model-in-pytorch)
- [(Yingce Xia et. al, 2017, Dual Supervised Learning)](https://arxiv.org/pdf/1707.00415.pdf)  
